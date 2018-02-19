---
title: Verarbeiten von Add-In-Ereignissen in anbietergehosteten Add-Ins
description: "Dieser Artikel beschreibt, wie Sie die Installation eines anbietergehosteten SharePoint-Add-Ins anpassen können. Sie erfahren, wie Sie Ihre Lösung für das Debuggen des Ereignisempfängers konfigurieren, wie Sie den Installationshandler und den Deinstallationshandler erstellen, wie Sie das Add-In ausführen und wie Sie die Handler testen."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 41f809a377fff222955696c34aafb60e102788a8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="handle-add-in-events-in-the-provider-hosted-add-in"></a>Verarbeiten von Add-In-Ereignissen in anbietergehosteten Add-Ins

Dies ist der siebte einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps) finden. 

> [!NOTE]
> Wenn Sie unsere Artikelreihe zum Thema anbietergehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können. Alternativ können Sie das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeAdd-inEventHandlers.sln“ öffnen.

In diesem Artikel passen Sie die Verarbeitung einer bestimmten Art von SharePoint-Ereignissen an: Add-In-Ereignissen. Konkret erstellen Sie Handler für Add-In-Installationsereignisse und Add-In-Deinstallationsereignisse. Auch Listenereignisse und Listenelementereignisse können benutzerdefiniert verarbeitet werden. Wie das funktioniert, erfahren Sie in einem der noch folgenden Artikel in unserer Reihe. Alle diese Ereignisse werden in SharePoint ausgelöst; der benutzerdefinierte Code, der die einzelnen Ereignisse verarbeitet, befindet sich jedoch in Ihrer Remotewebanwendung. Damit SharePoint Ihren benutzerdefinierten Handler aufruft, müssen Sie die URL des Handlers im betreffenden SharePoint-Ereignis registrieren.

## <a name="two-places-to-programmatically-deploy-sharepoint-components"></a>Zwei geeignete Stellen für die programmgesteuerte Bereitstellung von SharePoint-Komponenten

Unser ChainStore-Add-In soll die Listen **Lokale Mitarbeiter** und **Erwartete Lieferungen** automatisch erstellen und bereitstellen. Add-Ins können SharePoint-Komponenten wie benutzerdefinierte Listen jederzeit bereitstellen. Wenn ein Add-In jedoch von einer bestimmten Komponente wie beispielsweise einer benutzerdefinierten Liste abhängig ist, sollte diese Komponente bereitgestellt werden, *bevor* der Benutzer beginnt, mit dem Add-In zu arbeiten. Die benutzerdefinierte Bereitstellungslogik für solche essenziellen Komponenten kann an zwei Stellen platziert werden:

- In einem Handler für das Add-In-Installationsereignis
- In einer Logik für die erste Ausführung, die ausgeführt wird, wenn das Add-In zum ersten Mal in SharePoint gestartet wird

Die Entscheidung, welcher für ein bestimmtes Add-In am besten geeignet ist, ist ein weiterführendes Thema. In diesem Artikel können nur einige Vergleichspunkte erwähnt werden:

- Die Ausführung eines benutzerdefinierten Installationshandlers muss innerhalb von 30 Sekunden abgeschlossen sein. Für die Ausführung von zuerst auszuführender Logik (First-Run-Logik) gibt es kein Zeitlimit.

- Treten während der Add-In-Installation Fehler auf, führt SharePoint ein Rollback aller während der Installation durchgeführten Aktionen aus. Ein benutzerdefinierter Installationshandler wird ausgeführt, *nachdem* SharePoint sämtliche zur Add-In-Installation nötigen Aktionen durchgeführt hat; er kann sich also in dieses System einklinken. 

   Gibt die benutzerdefinierte Logik beispielsweise eine Ausnahme zurück, können Sie SharePoint anweisen, ein Rollback der gesamten Add-In-Installation auszuführen. Tritt jedoch bei der Ausführung einer benutzerdefinierten First-Run-Logik ein Fehler auf, bleibt das Add-In installiert und wird vermutlich nicht mehr korrekt funktionieren.

- SharePoint stellt seine Aktivitäten nach dem Rollback einer Add-In-Installation nicht ein. Stattdessen wird sofort ein erneuter Installationsversuch unternommen. Insgesamt macht SharePoint bis zu vier Versuche. (Dabei gilt das 30-Sekunden-Zeitlimit für jeden Versuch.) Bei jedem erneuten Versuch wird der benutzerdefinierte Installationshandler wieder *komplett ab seinem ersten Schritt* ausgeführt. Angenommen, der Handler konnte vor dem Rollback eine Liste installieren. Bei einem erneuten Installationsversuch würde der Handler dann versuchen, dieselbe Liste nochmals zu installieren. 

   Um dies zu verhindern, müssen Sie den Code in dem Installationshandler so verfassen, dass Aktionen wie die Bereitstellung einer Komponente erst ausgeführt werden, nachdem geprüft wurde, ob die betreffende Aktion bereits zuvor ausgeführt wurde. Das macht die Logik eines Installationshandlers komplexer als First-Run-Logik: First-Run-Logik führt keine erneuten Versuch durch (es sei denn, Sie programmieren sie explizit entsprechend). Darüber hinaus erfordert die Prüfung auf eine bereits zuvor durchgeführte Bereitstellung einer Komponente einen zeitintensiven, internetbasierten Aufruf vom Remotehandler an SharePoint. Wurde die Komponente noch nicht bereitgestellt, ist zur eigentlichen Bereitstellung dann noch ein zweiter Aufruf erforderlich.

In unserem ChainStore-Add-In kombinieren wir diese Strategien. In diesem Artikel erstellen Sie einen Installationshandler, der das Hostweb als Mandant in der Unternehmensdatenbank registriert und anschließend ein Signal setzt, das angibt, ob das Add-In bereits im Hostweb ausgeführt worden ist. 

In einem der folgenden Artikel dieser Reihe platzieren Sie First-Run-Logik in der Methode **Page_Load** der Add-In-Startseite. Diese Logik stellt die zwei benutzerdefinierten Listen bereit und führt verschiedene andere Aktionen durch.

<a name="RERDebug"> </a>
## <a name="configure-the-solution-for-event-receiver-debugging"></a>Konfigurieren der Lösung für das Debuggen des Ereignisempfängers

Das Debuggen von Ereignisempfängern erfordert die Verwendung von Azure Service Bus. Befolgen Sie die Anweisungen unter [Debugging und Problembehandlung eines Remoteereignisempfängers in einem Add-In für SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md). Da Sie eine SharePoint Online-Website als Testwebsite verwenden, müssen Sie die Anweisungen für Remotetestwebsites befolgen. In den übrigen Artikeln dieser Reihe gehen wir davon aus, dass Sie das Debugging erfolgreich konfiguriert haben. 

## <a name="create-the-installation-handler"></a>Erstellen des Installationshandlers

> [!NOTE]
> Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach jedem erneuten Öffnen der Lösung wieder auf die Standardwerte zurückgesetzt. Wann immer Sie beim Durcharbeiten dieser Artikelreihe die Beispiellösung erneut öffnen, müssen Sie umgehend die folgenden Schritte durchführen: 
> 1. Klicken Sie oben im **Projektmappen-Explorer** mit der rechten Maustaste auf den Lösungsknoten, und wählen Sie die Option **Startprojekte festlegen** aus.  
> 2. Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.

1. Wählen Sie im **Projektmappen-Explorer** das Projekt **ChainStore** aus. Die Eigenschaften des Projekts werden im Visual Studio-Bereich **Eigenschaften** angezeigt.

2. Legen Sie für **Installiertes Add-In verarbeiten** den Wert **Wahr ** fest. (Möglicherweise heißt die Option in Ihrer Version noch **Installierte App behandeln**.) Diese Festlegung bewirkt zwei Dinge:
    
   - Ein Ordner mit dem Namen **Dienste** wird im Projekt **ChainStoreWeb** erstellt (nicht im Projekt **ChainStore**), und diesem Ordner werden zwei Dateien hinzugefügt: die Datei „AppEventReceiver.svc“ und deren CodeBehind-Datei „AppEventReceiver.svc.cs“. (Die Dateinamen beginnen mit der Zeichenfolge „App“, weil Add-Ins früher als Apps bezeichnet wurden. *Benennen Sie diese Dateien nicht um!* Office Developer Tools für Visual Studio erwartet, dass die Dateien noch dieselben Namen haben).

   - Die Handler-URL wird im Add-In-Manifest registriert. Dieser Teil des Manifests ist im Manifest-Designer nicht sichtbar. Damit er angezeigt wird, müssen Sie mit der rechten Maustaste auf die Datei „AppManifest.xml“ klicken und die Option **Code anzeigen** auswählen. Ein neues untergeordnetes Element des Elements **Properties** sieht wie folgt aus: 
   
      ```XML
        <InstalledEventEndpoint>~remoteAppUrl/Services/AppEventReceiver.svc</InstalledEventEndpoint>
      ``` 
   
     Dieses Markup weist SharePoint an, die Methode **ProcessEvent** dieses Diensts aufzurufen, sobald alle SharePoint-eigenen Aufgaben zur Installation des Add-Ins ausgeführt wurden. Der benutzerdefinierte Handler ist das letzte Element, das während der Installation ausgeführt wird. Die Zeichenfolge `~remoteAppUrl` ist ein Platzhalter, den Office Developer Tools für Visual Studio durch die Host-URL des Diensts ersetzt. Beim Debuggen wird eine Azure Service Bus-URL eingefügt. Wenn Sie das Paket für die Bereitstellung in der Produktionsumgebung erstellen, wird die Produktions-URL eingefügt.

3. Öffnen Sie die Datei „AppEventReceiver.svc.cs“.
    
4. Wie Sie sehen, hat Office Developer Tools für Visual Studio eine Beispielimplementierung der Methode **ProcessEvent** erstellt. Alle Implementierungen dieser Methode beginnen mit der Initialisierung eines Objekts des Typs **SPRemoteEventResult** und enden mit der Rückgabe dieses Objekts an SharePoint. Unter anderem teilt dieses Objekt SharePoint mit, ob für das Ereignis ein Rollback ausgeführt werden soll, falls in der benutzerdefinierten Verarbeitungslogik ein Fehler auftritt. 

   Möglicherweise haben die Tools auch einen Block des Typs **using** in die Methode aufgenommen, der ein Objekt des Typs **ClientContext** erstellt. Der benutzerdefinierte Handler im ChainStore-Add-In wird keinen Rückruf an SharePoint senden, daher können Sie diesen Block löschen. Die Methode sollte jetzt wie folgt aussehen:
    
    ```C#
       public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
     {
         SPRemoteEventResult result = new SPRemoteEventResult();

         return result;
     }
    ```

5. Der Ereignisempfänger kann von jedem der drei möglichen Add-In-Ereignisse aufgerufen werden. Fügen Sie deshalb die folgende Struktur des Typs **switch** zur Methode **ProcessEvent** hinzu, zwischen den Zeilen, die das Objekt des Typs `result` erstellen und zurückgeben. (Die Ereignisnamen enthalten die Zeichenfolge „App“, da Add-Ins früher als Apps bezeichnet wurden.)
    
    ```C#
      switch (properties.EventType)
    {
        case SPRemoteEventType.AppInstalled:

            // TODO2: Custom installation logic goes here.

            break;
        case SPRemoteEventType.AppUpgraded:
            // This sample does not implement an add-in upgrade handler.
            break;
        case SPRemoteEventType.AppUninstalling:

            // TODO3: Custom uninstallation logic goes here.         

            break;
    }
    ```

6. Unsere Installationslogik wird eine gespeicherte SQL-Prozedur aufrufen, um den Hongkong-Store als Mandant in der Remotewebanwendung zu registrieren. Es ist sehr wichtig, dass der Handler SharePoint bei einem Fehlschlagen dieses Prozesses signalisiert, ein Rollback der Add-In-Installation auszuführen. Ersetzen Sie daher `TODO2` durch die folgenden Blöcke des Typs **try/catch**: 

    ```C#
      try
    {
        CreateTenant(tenantName);
     }
    catch (Exception e)
    {
         // Tell SharePoint to cancel and roll back the event.
        result.ErrorMessage = e.Message;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;
    }
    ```

   Zu diesem Code ist Folgendes anzumerken:

   - Das Objekt des Typs `tenantName` und die Methode `CreateTenant` erstellen Sie in einem späteren Schritt.
   - Die Eigenschaft **Status** des Objekts **SPRemoteEventResult** kann drei Werte aufweisen: **Continue** (Standard), **CancelNoError** und **CancelWithError**. Die beiden Letzteren weisen SharePoint an, ein Rollback des Ereignisses durchzuführen.

7. Die Hostweb-URL ist der Mandantendiskriminator des Beispielcodes und eine der Informationen, die SharePoint im Parameter **SPRemoteEventProperties** an den Empfänger übergibt. Fügen Sie die folgende Zeile zur Methode **ProcessEvent** hinzu, in der Zeile unmittelbar unterhalb des Codes für die Initialisierung des Objekts des Typs **SPRemoteEventResult**:
    
    ```C#
      string tenantName = properties.AppEventProperties.HostWebFullUrl.ToString();
    ```

8. Jetzt müssen Sie in Ihrem Code noch eine kleine Besonderheit der Eigenschaft **AppEventProperties.HostWebFullUrl** berücksichtigen: Da SharePoint in den meisten anderen Kontexten `"/"` als abschließendes Zeichen am Ende der Hostweb-URL setzt, erwartet die Logik unseres Codebeispiels dieses Zeichen ebenfalls. Jedoch setzt SharePoint dieses Zeichen am Ende des Werts **HostWebFullUrl** ausschließlich dann, wenn das Hostweb das Stammweb einer Websitesammlung ist. Da unsere Hongkong-Website eine Unterwebsite in der Websitesammlung ist, müssen Sie dieses Symbol hinzufügen, damit überall im Beispielcode dieselbe Zeichenfolge als Mandantenname verwendet wird. 

   Fügen Sie den folgenden Code unterhalb des Codes für die Initialisierung des Objekts des Typs `tenantName` ein:
    
    ```C#
      if (!tenantName.EndsWith("/"))
    {
        tenantName += "/";
    }
    ```

9. Fügen Sie die folgenden Anweisungen des Typs **using** oben in der Datei ein:
    
    ```C#
      using System.Data.SqlClient;
      using System.Data;
      using ChainStoreWeb.Utilities;
    ```

10. Fügen Sie der Klasse `AppEventReceiver` die unten aufgeführte Methode hinzu. Auf diesen Schritt gehen wir an dieser Stelle nicht im Detail ein, weil wir uns in dieser Artikelreihe auf die Programmierung von SharePoint-Add-Ins konzentrieren, nicht auf die SQL Server/Azure-Programmierung.

     ```C#
       private void CreateTenant(string tenantName)
     {
         // Do not catch exceptions. Allow them to bubble up and trigger roll back
         // of installation.

         using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
         using (SqlCommand cmd = conn.CreateCommand())
         {
             conn.Open();
             cmd.CommandText = "AddTenant";
             cmd.CommandType = CommandType.StoredProcedure;
             SqlParameter name = cmd.Parameters.Add("@Name", SqlDbType.NVarChar);
             name.Value = tenantName;
             cmd.ExecuteNonQuery();
         }//dispose conn and cmd
     }
     ```

    Diese Methode erstellt eine Zeile in einer Datenbanktabelle namens **Mandanten**. Neben der Spalte **Name** enthält diese Tabelle auch eine Spalte **Version** mit einem Standardwert von „0000.0000.0000.0000“. In einem der nachfolgenden Artikel dieser Reihe erstellen Sie First-Run-Logik, die anhand dieses Wertes ermittelt, ob das Add-In bereits im Hostweb installiert worden ist. Wenn als Version „0000.0000.0000.0000“ gesetzt ist, stellt der Code die Listen **Lokale Mitarbeiter** und **Erwartete Lieferungen** bereit und setzt anschließend die Versionsnummer herauf.
    
## <a name="create-the-uninstallation-handler"></a>Erstellen des Deinstallationshandlers

Wenn Sie das Installationsereignis verarbeiten, empfiehlt es sich in der Regel immer, auch das Deinstallationsereignis zu verarbeiten. Von der grundlegenden Idee her löscht oder recycelt der Deinstallationshandler Komponenten, die der Installationshandler bereitgestellt hat. Jedoch gibt es hier zahlreiche Ausnahmen, sodass Sie sich immer zunächst über die Anwendungsfälle Ihres Add-Ins klar werden müssen. Ein Beispiel: Eine Liste, die mit einem Add-In bereitgestellt und befüllt wird, ist möglicherweise auch nach der Deinstallation des Add-Ins noch nützlich. Dann sollte der Deinstallationsereignishandler diese Liste nicht deinstallieren. 

Erwartungsgemäß wird das Deinstallationsereignis nicht ausgeführt, wenn ein Benutzer das Add-In von der Seite **Websiteinhalte** entfernt. Dadurch verschiebt er das Add-In lediglich in den Papierkorb der Website. Der Benutzer könnte das Add-In zwar anschließend wiederherstellen, dann würde jedoch der Installationsereignishandler nicht wieder ausgeführt werden. Alle Komponenten, die vom Installationsereignishandler bereitgestellt wurden, sollten also noch vorhanden sein, wenn das Add-In wiederhergestellt wird. SharePoint-Komponenten können aus dem Papierkorb in den endgültigen Papierkorb verschoben werden. Das Deinstallationsereignis wird nur ausgeführt, wenn ein Add-In aus dem endgültigen Papierkorb gelöscht wird. Tut ein Benutzer das, lässt sich das betreffende Add-In nicht wiederherstellen. In diesem Fall soll der Mandant des Hongkong-Stores aus der Unternehmensdatenbank entfernt werden.

1. Legen Sie für **Deinstallation des Add-Ins verarbeiten** den Wert **Wahr** fest. (Möglicherweise heißt die Option in Ihrer Version noch **Handle App Uninstalling**.) Dadurch wird der Handler in der Datei „AppManifest.xml“ registriert, genauso wie zuvor der Installationshandler registriert wurde. Wie Sie sehen, haben die beiden Handler exakt dieselbe URL. Office Developer Tools für Visual Studio erwartet, dass Sie dieselbe \*.svc-Datei verwenden. Das ist eine Standardvorgehensweise, an die wir uns auch in diesem Codebeispiel halten. 

2. Fügen Sie den folgenden Code anstelle von `TODO3` in die Datei „AppEventReceiver.svc.cs“ ein: 

    ```C#
      try
    {
        DeleteTenant(tenantName);
     }
    catch (Exception e)
    {
         // Tell SharePoint to cancel and roll back the event.
        result.ErrorMessage = e.Message;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;
    }
    ```

   Zu diesem Code ist Folgendes anzumerken:

   - Die Methode `DeleteTenant` wird im nächsten Schritt hinzugefügt.
   - Nach einem Rollback der Add-In-Deinstallation verbleibt das Add-In im endgültigen Papierkorb, aus dem es immer noch wiederhergestellt werden kann.

3. Fügen Sie der Klasse `AppEventReceiver` die unten aufgeführte Methode hinzu.
    
    ```C#
      private void DeleteTenant(string tenantName)
    {
        // Do not catch exceptions. Allow them to bubble up and trigger roll back
        // of un-installation (removal from 2nd level Recycle Bin).

        using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
        using (SqlCommand cmd = conn.CreateCommand())
        {
            conn.Open();
            cmd.CommandText = "RemoveTenant";
            cmd.CommandType = CommandType.StoredProcedure;
            SqlParameter name = cmd.Parameters.Add("@Name", SqlDbType.NVarChar);
            name.Value = tenantName;
            cmd.ExecuteNonQuery();                
        }//dispose conn and cmd
    }
    ```

> [!NOTE]
> In einem der vorangegangenen Artikel dieser Reihe haben Sie das Projekt so konfiguriert, dass die Unternehmensdatenbank jedes Mal neu erstellt wird, wenn Sie F5 drücken. Dann wird die Tabelle **Mandanten** geleert.

## <a name="run-the-add-in-and-test-the-installation-handler"></a>Ausführen des Add-Ins und Testen des Installationshandlers

1. Drücken Sie die Taste F5, um das Add-In bereitzustellen und auszuführen. Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express. Zudem installiert Visual Studio das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite, führt den Installationsereignishandler aus und führt anschließend sofort das Add-In aus. Bevor die Startseite des Add-Ins geöffnet wird, werden Sie aufgefordert, dem Add-In Berechtigungen zu erteilen. 

2. Die Startseite des Add-Ins wird geöffnet. Klicken Sie oben im Chromsteuerelement auf das Zahnradsymbol, und wählen Sie die Option **Kontoeinstellungen** aus.

3. Klicken Sie auf der Seite **Kontoeinstellungen** auf die Schaltfläche **Add-In-Version anzeigen**. Als Version wird „0000.0000.0000.0000“ angezeigt.
    
   *Abbildung 1: Seite „Kontoeinstellungen“*

   ![Seite „Kontoeinstellungen“ mit der Überschrift „Kontoeinstellungen“, einer Schaltfläche „Add-In-Version anzeigen“ und einer Textzeile „Registrierte Version: 0000.0000.0000.0000“](../images/2a905b7d-89c7-456a-8456-21a9b7e9efc5.PNG)

4. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Wann immer Sie F5 drücken, zieht Visual Studio die bisherige Version des Add-Ins zurück und installiert die jeweils neueste Version.

5. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung auch in anderen Artikeln arbeiten werden, empfiehlt es sich, das Add-In ein letztes Mal zurückzuziehen, sobald Sie eine Weile nicht mehr an ihm arbeiten werden. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Im nächsten Artikel unserer Reihe fügen Sie dem Add-In First-Run-Logik hinzu, die die Liste **Lokale Mitarbeiter** und die benutzerdefinierte Menübandschaltfläche programmgesteuert bereitstellt: [Hinzufügen der Logik für die erste Ausführung zum vom Anbieter gehosteten Add-In](add-first-run-logic-to-the-provider-hosted-add-in.md).
 

 

