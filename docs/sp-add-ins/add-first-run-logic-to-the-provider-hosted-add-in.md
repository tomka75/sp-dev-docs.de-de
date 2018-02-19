---
title: "Hinzufügen der Logik für die erste Ausführung zum vom Anbieter gehosteten Add-In"
description: "Fügen Sie „Erste Ausführung“-Code zu einer vom Anbieter gehosteten SharePoint Add-In hinzu, indem Sie die grundlegende Klasse für die Bereitstellung von Komponenten erstellen, die grundlegende Startlogik hinzufügen und programmgesteuert eine SharePoint-Liste bereitstellen."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: ee96ec1a846a4f799e15ae4e98bf5c07f8933faf
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-first-run-logic-to-the-provider-hosted-add-in"></a>Hinzufügen von First-Run-Logik zu anbietergehosteten Add-Ins

Dies ist der achte einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps) finden. 

> [!NOTE]
> Wenn Sie unsere Artikelreihe zum Thema anbietergehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können. Sie können auch das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeFirstRunLogic.sln“ öffnen.

In diesem Artikel fügen Sie Code zur Startseite des ChainStore-SharePoint-Add-Ins hinzu, der überprüft, ob die aktuelle Instanz des Add-Ins zum ersten Mal ausgeführt wird. Wenn es das erste Mal ist, stellt Ihr Code die Liste **Lokale Mitarbeiter** und die benutzerdefinierte Menübandschaltfläche bereit.

## <a name="create-the-basic-class-for-deploying-sharepoint-components"></a>Erstellen der Basisklasse für die Bereitstellung von SharePoint-Komponenten

> [!NOTE]
> Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach jedem erneuten Öffnen der Lösung wieder auf die Standardwerte zurückgesetzt. Wann immer Sie beim Durcharbeiten dieser Artikelreihe die Beispiellösung erneut öffnen, müssen Sie umgehend die folgenden Schritte durchführen: 
> 1. Klicken Sie oben im **Projektmappen-Explorer** mit der rechten Maustaste auf den Lösungsknoten, und wählen Sie die Option **Startprojekte festlegen** aus.  
> 2. Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.

1. Klicken Sie im **ChainStoreWeb**-Projekt im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Dienstprogramme**, und wählen Sie dann **Hinzufügen** > **Vorhandenes Element** aus.
    
2. Wechseln Sie vom **Datei-Explorer** zum Projektmappenordner, dem **ChainStoreWeb**-Ordner, und öffnen Sie dann den Ordner **Dienstprogramme**.

3. Wählen Sie „SharePointComponentDeployer.cs“ aus, und wählen Sie dann **Hinzufügen** aus.

4. Öffnen Sie die Datei SharePointComponentDeployer.cs. Sie enthält eine statische Klasse und zwei statische Methoden, die die Add-In-Version in der Tabelle **Mandanten** der Unternehmensdatenbank abrufen und festlegen. Diese Methoden werden nicht besprochen, da diese Artikelreihe nicht dafür vorgesehen ist, Kenntnissse der ASP.NET- oder SQL Server-/Azure-Programmierung zu vermitteln.

5. Fügen Sie die folgenden **using**-Anweisungen an den Anfang der Datei hinzu.
    
    ```C#
      using System.Web;
      using System.Linq;
      using System.Collections.Generic;
      using Microsoft.SharePoint.Client;
    ```

6. Fügen Sie am oberen Rand der `SharePointComponentDeployer`-Klasse die folgenden zwei statischen Felder hinzu. Diese werden in der **Page_Load**-Methode der Add-In-Startseite initialisiert (Sie fügen den Code in einem späteren Schritt hinzu). 

    ```C#
      internal static SharePointContext sPContext;
      internal static Version localVersion;
    ```

   Beachten Sie Folgendes zu diesem Code:
   
   - Das erste Feld enthält das `SharePointContext`-Objekt, das erforderlich ist, um CRUD-Vorgänge in SharePoint durchzuführen. 
   
   - Das zweite Feld enthält die Versionsnummer des Add-Ins, das im Hostweb installiert ist. Dieser Wert weicht anfänglich vom Standardwert (**0000.0000.0000.0000**) ab, der in der **Mandanten**-Tabelle aufgezeichnet wird, wenn der Installationshandler den Mandanten registriert. Die erste Version des Add-Ins lautet z. B. **1.0.0.0**.

7. Erstellen Sie die folgende statische Eigenschaft für die Version des Add-Ins, die derzeit in der Tabelle **Mandanten** des Unternehmens aufgezeichnet ist. Sie verwendet die zwei Methoden, die bereits in der Datei vorhanden waren, um diesen Wert abzurufen und festzulegen.
    
    ```C#
      internal static Version RemoteTenantVersion
    {
        get
        {
            return GetTenantVersion();
        }
        set
        {
            SetTenantVersion(value);
        }
    }
    ```

8. Erstellen Sie nun die folgende `IsDeployed`-Eigenschaft. 

    ```C#
      public static bool IsDeployed
    {
        get
        {
            if (RemoteTenantVersion < localVersion)
                return false; 
            else
                return true; 
        }
    }
    ```

   Beachten Sie Folgendes zu diesem Code:

   - Die **Page_Load**-Methode für die Stadtseite des Add-Ins verwendet den Wert dieser Eigenschaft, um zu bestimmen, ob das Add-In zum ersten Mal ausgeführt wird. Der Wert **false** besagt, dass das Add-In zuvor noch nicht auf dem aktuellen Hostweb ausgeführt wurde, also müssen die Komponenten bereitgestellt werden.

   - Dabei ist das entscheidende Kriterium, ob die Versionsnummer in der **Mandanten**-Tabelle niedriger als die aktuell installierte Version ist. Wenn das Add-In zum ersten Mal ausgeführt wird, ist die Version niedriger. Code, den Sie in einem späteren Schritt schreiben, legt die Version in der **Mandanten**-Tabelle auf die gleiche Version wie die tatsächlich installierte fest. Wenn das Add-In also erneut ausgeführt wird, gibt `IsDeployed` den Wert **true** zurück und die Bereitstellungslogik wird nicht noch einmal ausgeführt.
 
9. Fügen Sie der Klasse `SharePointComponentDeployer` die folgende Methode hinzu: Beachten Sie, dass die letzte Aktion, die die Methode ausführt, das Aktualisieren der Mandantenversion ist, die in der Datenbank des Unternehmens registriert ist (**0000.0000.0000.0000**), damit sie mit der aktuellen Version des Add-Ins im Hostweb übereinstimmt (**1.0.0.0**). Sie schließen diese Methode in einem späteren Schritt ab.
    
    ```C#
      internal static void DeployChainStoreComponentsToHostWeb(HttpRequest request)
    {
        // TODO4: Deployment code goes here.

        RemoteTenantVersion = localVersion;
    }
    ```

> [!NOTE]
> Sie Fragen sich nun vielleicht, warum das Add-In den „Versionsnummer niedriger als“-Test durchführt, um die Antwort auf die einfache Ja/Nein-Frage: „Wird das Add-in zum ersten Mal ausgeführt?“ zu bestimmen. Wir könnten auch ein einfaches Zeichenfolgefeld in der **Mandanten**-Tabelle verwenden, das im Installationshandler auf *Noch nicht ausgeführt* gesetzt und dann von der „Erste Ausführung“-Logik auf *Bereits einmal ausgeführt* festgelegt wird, nachdem die SharePoint-Komponenten bereitgestellt wurden. 

> Für das ChainStore-Add-In funktioniert ein einfacher Test. Es empfiehlt sich jedoch im Allgemeinen, Versionsnummern zu verwenden. Der Grund ist, dass ein Produktions-Add-In in Zukunft wahrscheinlich direkt aktualisiert wird, d. h. nachdem es bereits installiert wurde. Dann muss Ihre Add-In-Logik auf mehr als die zwei Möglichkeiten *Noch nicht ausgeführt* und *Bereits einmal ausgeführt* reagieren können. 

> Angenommen Sie möchten beispielsweise eine weitere Liste zum Hostweb im Upgrade von Version 1.0.0.0 auf 2.0.0.0 hinzufügen. Sie könnten dies mit einem Updateereignishandler durchführen oder in einer „Erste Ausführung nach Update"-Logik. In beiden Fällen muss Ihre Bereitstellungslogik neue Komponenten bereitstellen, aber auch vermeiden, dass versucht wird, Komponenten erneut bereitzustellen, die in einer früheren Version des Add-Ins bereitgestellt wurden. Die Versionsnummer 1.0.0.0 würde signalisieren, dass die Komponenten der Version 1.0.0.0 bereitgestellt wurden, aber die Logik für die erste Ausführung nach dem Update noch nicht ausgeführt wurde.

## <a name="add-the-basic-startup-logic"></a>Hinzufügen der grundlegenden Startlogik

Das SharePoint-Hostweb muss der Remote-Webanwendung mitteilen, welche Version des Add-Ins installiert ist. Zu diesem Zweck verwenden wir einen Abfrageparameter. 

1. Öffnen Sie im **ChainStore**-Projekt die Datei „AppManifest.xml“. Im Designer finden Sie den Platzhalter *{StandardTokens}* als Wert für das **Abfragezeichenfolge**-Feld. Fügen Sie die Zeichenfolge `"&amp;SPAddInVersion=1.0.0.0"` zum Textende hinzu. 

   Der Manifest-Designer sollte ähnlich wie im folgenden Beispiel aussehen. *Beachten Sie, dass die Versionsnummer, die Sie in der Abfragezeichenfolge übergeben haben, dem Wert des Feldes __Version__ des Designers entsprechen muss.* Wenn Sie das Add-In aktualisieren sollten, müssen Sie diese beiden Werte auf den gleichen Wert erhöhen.

   *Abbildung 1. Registerkarte „Allgemein“ des Manifest-Designers*

   ![Die Registerkarte „Allgemein“ des Manifest-Designers. Das Versionsfeld enthält den Wert „eins null null null“. Der Wert im Feld „Abfragezeichenfolge“ lautet „{StandardTokens}&amp;SPAddInVersion=1.0.0.0“.](../images/db71c411-10c5-43d8-bb5e-3388d2f6f7bc.PNG)

2. Öffnen Sie die Datei „CorporateDataViewer.aspx.cs“, und fügen Sie den folgenden Code zur Methode **Page_Load** hinzu, direkt unter der Zeile, die das `spContext`-Objekt initialisiert. 

    ```C#
     SharePointComponentDeployer.sPContext = spContext;
     SharePointComponentDeployer.localVersion = new Version(Request.QueryString["SPAddInVersion"]);

     if (!SharePointComponentDeployer.IsDeployed)
     {
         SharePointComponentDeployer.DeployChainStoreComponentsToHostWeb(Request);
     }
    ```

   Beachten Sie Folgendes zu diesem Code:

   - Er beginnt mit der Festlegung der zwei statischen Felder in der statischen `SharePointComponentDeployer`-Klasse.  Er übergibt das Objekt **SharePointContext**, da der Code in `SharePointComponentDeployer`SharePoint aufruft und den Abfrageparameter verwendet, den Sie hinzugefügt haben, um die Eigenschaft `localVersion` festzulegen.  

   - Es geschieht nichts, wenn `IsDeployed` „true“ ist, d. h., wenn die erste Ausführungslogik bereits ausgeführt wurde. Andernfalls wird die Bereitstellungsmethode aufgegeben, die das ASP.NET-**Anforderungs**objekt übergibt.

## <a name="programmatically-deploy-a-sharepoint-list"></a>Programmgesteuertes Bereitstellen einer SharePoint-Liste

1. Ersetzen Sie in der Datei „SharePointComponentDeployer.cs“ `TODO4` durch die folgende Zeile. (Im nächsten Schritt erstellen Sie diese Methode.)
    
    ```C#
      CreateLocalEmployeesList();
    ```

2. Fügen Sie der Klasse `SharePointComponentDeployer` die folgende Methode hinzu: 

    ```C#
      private static void CreateLocalEmployeesList()
    {
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())
        {
            var query = from list in clientContext.Web.Lists
                        where list.Title == "Local Employees"
                        select list;
            IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
            clientContext.ExecuteQuery();

            if (matchingLists.Count() == 0)
            {
               // TODO5: Create the list 

               // TODO6: Rename the Title field on the list 

               // TODO7: Add "Added to Corporate DB" field to the list 

               clientContext.ExecuteQuery();
            }
        }
    }
    ```

   Beachten Sie Folgendes zu diesem Code:

   - Er enthält zwei Aufrufe von **ExecuteQuery**. Die erste ist erforderlich, um festzustellen, ob die Liste bereits vorhanden ist. Die zweite erstellt die Liste.

   - Die Methode **ClientContext.LoadQuery** ist vergleichbar mit **ClientContext.Load**-Methode, mit der Ausnahme, dass keine Entität wie z. B. eine Liste, sondern die aufzählbaren Ergebnisse einer Abfrage auf den Client gebracht werden.

3. Ersetzen Sie `TODO5` durch den folgenden Code. 

    ```C#
      ListCreationInformation listInfo = new ListCreationInformation();
      listInfo.Title = "Local Employees";
      listInfo.TemplateType = (int)ListTemplateType.GenericList;
      listInfo.Url = "Lists/Local Employees";
      List localEmployeesList = clientContext.Web.Lists.Add(listInfo);
    ```

   Beachten Sie Folgendes zu diesem Code:

   - Die **ListCreationInformation**-Klasse ist vergleichbar mit der **ListItemCreationInformation**-Klasse, die Sie in einem vorherigen Artikel dieser Reihe bereits gesehen haben. Es handelt sich um eine einfache Klasse, die zum Übersenden von Informationen von der Webanwendung zu SharePoint besser geeignet ist, als die vollständige **Listen**-Klasse.

   - Es gibt viele Arten von Listenvorlagen, z. B. den Typ „Aufgaben" für eine To-Do-Liste und den Typ „Ereignisse" für einen Kalender. Die Liste **Lokale Mitarbeiter**basiert auf der einfachsten Art: dem Typ „Generisch".

   - Die **ListCreationInformation.Url**-Eigenschaft enthält die URL der Liste *relativ* zum Hostweb. Durch die Angabe von `"Lists/LocalEmployees"` setzt der Code die vollständige URL auf `https://{SharePointDomain}/hongkong/_layouts/15/start.aspx#/Lists/Local%20Employees`.

4. Ersetzen Sie `TODO6` mit dem folgenden Code, der den öffentlichen Namen des Felds „Titel“ (Spalte) zu „Name“ ändert. Dies haben Sie auf der Seite **Listeneinstellungen** getan, als Sie die Liste manuell erstellt haben.
    
    ```C#
      Field field = localEmployeesList.Fields.GetByInternalNameOrTitle("Title");
      field.Title = "Name";
      field.Update();
    ```

5. Sie können auch manuell ein Feld namens **Zur Unternehmensdatenbank hinzugefügt** erstellen. Fügen Sie den folgenden Code anstelle von `TODO7` ein, um dies programmgesteuert durchzuführen. 

    ```C#
          localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'"
                                                 +"Type='Boolean'>"
                                                 + "<Default>FALSE</Default></Field>",
                                                 true,
                                                 AddFieldOptions.DefaultValue);
    ```

   Beachten Sie Folgendes zu diesem Code:

   - Die wichtigsten Eigenschaften des Felds werden mit einem XML-Blob angegeben. Dies ist eine Legacy der SharePoint-Architektur, in der Websites, Listen, Felder, Inhaltstypen und die meisten anderen Arten von SharePoint-Komponenten im XML-Format definiert sind. In diesem Fall haben wir den Anzeigename, den Datentyp und den Standardwert des Felds angegeben.

   - Der zweite Parameter bestimmt, ob das Feld in der Standardansicht der Liste angezeigt wird.  Er wird auf **true** festgelegt. 

   - Der dritte Parameter bestimmt, welche Inhaltstypen dem Feld hinzugefügt werden. Das Übergeben des **Standardwerts** bedeutet, dass dieser nur zum Standard-Inhaltstyp der Liste hinzugefügt wird.


6. Denken Sie daran, dass **Zur Unternehmensdatenbank hinzugefügt** standardmäßig **Nein** (d. h. „false“) ist, die Schaltfläche des benutzerdefinierten Menübands des Add-Ins den Wert jedoch auf **Ja** setzt, nachdem der Mitarbeiter zur Unternehmensdatenbank hinzugefügt wurde. Dieses System funktioniert am besten, wenn Benutzer den Wert des Felds nicht manuell ändern können. Um dies sicherzustellen, blenden Sie das Feld in den Formularen für das Erstellen und Bearbeiten von Elementen in der Liste **Lokale Mitarbeiter** aus. Dazu müssen Sie zwei weitere Attribute zum ersten Parameter hinzufügen, wie im folgenden Code dargestellt.
    
     ```C#
       localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'" 
                                              + " Type='Boolean'"  
                                              + " ShowInEditForm='FALSE' "
                                              + " ShowInNewForm='FALSE'>"
                                              + "<Default>FALSE</Default></Field>",
                                              true,
                                              AddFieldOptions.DefaultValue);
     ```
     
     
7. Die gesamte `CreateLocalEmployeesList` sollte jetzt wie folgt aussehen.

    ```C#
           private static void CreateLocalEmployeesList()
         {
             using (var clientContext = sPContext.CreateUserClientContextForSPHost())
             {
                 var query = from list in clientContext.Web.Lists
                             where list.Title == "Local Employees"
                             select list;
                 IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
                 clientContext.ExecuteQuery();

                 if (matchingLists.Count() == 0)
                 {
                     ListCreationInformation listInfo = new ListCreationInformation();
                     listInfo.Title = "Local Employees";
                     listInfo.TemplateType = (int)ListTemplateType.GenericList;
                     listInfo.Url = "LocalEmployees";
                     List localEmployeesList = clientContext.Web.Lists.Add(listInfo);

                     Field field = localEmployeesList.Fields.GetByInternalNameOrTitle("Title");
                     field.Title = "Name";
                     field.Update();

                     localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'" 
                                                             + " Type='Boolean'"  
                                                            + " ShowInEditForm='FALSE' "
                                                            + " ShowInNewForm='FALSE'>"
                                                            + "<Default>FALSE</Default></Field>",
                                                             true,
                                                             AddFieldOptions.DefaultValue);
                     clientContext.ExecuteQuery();
                 }
             }
         }
    ```

## <a name="temporarily-remove-the-custom-button-from-the-project"></a>Vorübergehendes Entfernen der benutzerdefinierten Schaltfläche aus dem Projekt

Aus technischen Gründen, die wir im nächsten Artikel behandeln, kann die benutzerdefinierte Schaltfläche, die wir erstellt haben, nicht ohne Änderung installiert werden, wenn sie auf dem Menüband einer Liste eingefügt wird, die programmgesteuert bereitgestellt wird. Wir müssen sie vorübergehend aus dem Projekt entfernen, damit wir unsere Logik für die erste Ausführung testen können. Im nächsten Artikel wird die Schaltfläche wieder in das Menüband zurückgebracht.

- Klicken Sie im **Projektmappen-Explorer** im **ChainStore**-Projekt mit der rechten Maustaste auf den Knoten **AddEmployeeToCorpDB**, und wählen Sie dann **Aus Projekt ausschließen** aus.

## <a name="request-permission-to-manage-lists-on-the-host-web"></a>Anfordern der Berechtigung zum Verwalten von Listen im Hostweb

Da das Add-In jetzt eine Liste zum Hostweb und nicht nur Elemente zu einer vorhandenen Liste hinzufügt, müssen die Berechtigungen, die das Add-In anfordert, von „Schreiben" zu „Verwalten" eskaliert werden.

1. Öffnen Sie im **Projektmappen-Explorer** die Datei AppManifest.xml im **ChainStore**-Projekt.

2. Behalten Sie auf der Registerkarte **Berechtigungen** für den Wert **Bereich** die Einstellung „Web“ bei, aber wählen Sie im Feld **Berechtigung** die Option **Verwalten** aus der Dropdownliste.
 
3. Speichern Sie die Datei.

## <a name="run-the-add-in-and-test-the-first-run-logic"></a>Ausführen des Add-Ins und Testen der Logik für die erste Ausführung

1. Öffnen Sie die Seite **Websiteinhalte** der Website des Hongkong-Stores, und entfernen Sie dann die Liste **Lokale Mitarbeiter**. 

2. Drücken Sie auf die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express. Zudem installiert Visual Studio das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite und führt es sofort aus. Bevor die Startseite des Add-Ins geöffnet wird, werden Sie aufgefordert, dem Add-In Berechtigungen zu erteilen.

3. Wenn die Add-In-Startseite geöffnet wird, wählen Sie den Link **Zurück zur Website** auf dem Chromesteuerelement im oberen Bereich aus.

4. Wechseln Sie auf die Seite **Websiteinhalte**. Die Liste **Lokale Mitarbeiter** wird angezeigt, da sie von der First-Run-Logik hinzugefügt wurde.
    
   > [!NOTE]
   > Falls die Liste nicht angezeigt wird oder Sie Grund zu der Annahme haben, dass die First-Run-Logik nicht ausgeführt wird, kann das daran liegen, wird möglicherweise die Tabelle **Mandanten** beim Drücken von F5 nicht in den leeren Zustand zurückgesetzt. Die häufigste Ursache hierfür: Das Projekt **ChainCorporateDB** ist in Visual Studio nicht mehr als Startprojekt gekennzeichnet. Eine Lösung für dieses Problem finden Sie in dem [Hinweis oben in diesem Artikel](#create-the-basic-class-for-deploying-sharepoint-components). Vergewissern Sie sich außerdem, dass die Datenbank so konfiguriert ist, dass sie neu erstellt wird (siehe [Konfigurieren von Visual Studio zum Neuerstellen der Unternehmensdatenbank in jeder Debugsitzung](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild)).

5. Öffnen Sie die Liste, und fügen Sie ein Element hinzu. Beachten Sie, dass im Formular für neue Elemente das Feld **Zu Unternehmens-DB hinzugefügt** nicht mehr vorhanden ist und deshalb nicht manuell festgelegt werden kann. Dies gilt auch für das Formular zum Bearbeiten von Elementen.
    
   *Abbildung 2. Neues Elementformular für die Liste der lokalen Mitarbeiter*

   ![Neues Elementformular für die Liste der lokalen Mitarbeiter Das Feld „Zur Unternehmensdatenbank hinzugefügt" ist nicht mehr im Formular enthalten, sondern nur noch das Namensfeld und die Schaltflächen für OK und Abbrechen.](../images/3fdc6752-4184-4928-9423-0bc7c0206c62.PNG)

6. Klicken Sie im Browser auf die Schaltfläche „Zurück“, um zurück zur Startseite für das Add-In zu navigieren.

7. Wählen Sie das Zahnradsymbol des Chromsteuerelements im oberen Bereich, und wählen Sie dann **Kontoeinstellungen** aus.

8. Klicken Sie auf der Seite **Kontoeinstellungen** auf die Schaltfläche **Add-In-Version anzeigen**. Die Version wird als **1.0.0.0** angezeigt, da die erste Ausführungslogik die Version geändert hat.
  
   *Abbildung 3: Seite „Kontoeinstellungen“*

   ![Der Kontoeinstellungsseite mit der Versionsnummer 1.0.0.0.](../images/4c6d82a7-7c40-4190-b7e3-1337275e1e60.PNG)

9. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.

10. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Im nächsten Artikel wird gezeigt, wie Sie die benutzerdefinierte Schaltfläche für das Menüband **Lokale Mitarbeiter** zurück in das Add-In bringen, nachdem die Liste jetzt programmgesteuert bereitgestellt wird: [Programmgesteuerte Bereitstellung einer benutzerdefinierten Schaltfläche im vom Anbieter gehosteten Add-In](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in.md)
 

 

