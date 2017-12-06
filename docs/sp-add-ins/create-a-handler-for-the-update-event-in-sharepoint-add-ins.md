---
title: "Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins"
description: "Erstellen und verwenden Sie einen Handler und wenden Sie Rollbacklogik für das Updateereignis eines SharePoint-Add-Ins an."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 52d88501ca0918a676588115b81807df4a61bc9b
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a>Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins

Bevor Sie beginnen, sollten Sie sich umfassend mit den Themen [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) und [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) sowie den darin aufgeführten Voraussetzungen und Kernkonzepten vertraut machen.

> [!NOTE]
> **Versionsnummernsystem:** Aus Gründen der Konsistenz wird in diesem Thema davon ausgegangen, dass die Add-In-Versionsnummern 1.0.0.0, 2.0.0.0, 3.0.0.0 usw. sind. Die Logik und Anleitungen gelten jedoch unabhängig davon, welches Nummernsystem Sie verwenden.

<a name="UpgradedEventEndpoint"> </a>
## <a name="create-an-upgradedeventendpoint-receiver"></a>Erstellen eines UpgradedEventEndpoint-Empfängers

Für die benutzerdefinierte Aktualisierungslogik können Sie einen SharePoint-Remoteereignisempfänger erstellen, der das Add-In-Updated-Ereignis verarbeitet. Sie sollten mit dieser Methode vorsichtig sein. Verwenden Sie sie nur, wenn Schritte nicht auf eine andere Weise aktualisiert werden können. Die Anleitung unter [Behandeln von Add-in-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) gilt ebenso für das Add-In-Updated- wie das Add-In-Installed- und das Add-In-Uninstalling-Ereignis. Dies umfasst Folgendes:

- Der Handler muss entweder einen Abbruch- oder einen Fortfahren-Status abschließen und diesen innerhalb von 30 Sekunden an SharePoint zurückgeben. Wenn dies nicht der Fall ist, ruft SharePoint den Handler bis zu drei Mal erneut auf.

- Wenn der Handler einen Abbruchstatus zurückgibt, versucht SharePoint es bis zu drei Mal erneut. 

- ie müssen in der Regel Rollback- und „Bereits erledigt“-Logik in den Ereignishandler einbeziehen.

Ein Szenario, in dem ein **UpgradedEventEndpoint**-Handler nützlich ist, ist wenn ein berechnetes Feld zu einer Remotedatenbank hinzugefügt wird. Angenommen, die Spalte "Ort" wird hinzugefügt, und der Wert wird anhand einer bereits bestehenden Postleitzahl-Spalte berechnet. Ihr Code in einem **UpgradedEventEndpoint**-Handler könnte vorhandene Elemente in der Datenbank durchlaufen und den Wert für das neue Ort-Feld auf Basis des Werts des Postleitzahl-Felds und einer externen Datenquelle, die Postleitzahlen Orten zuordnet, einfügen. Die Änderung am Datenbankschema selbst sollte außerhalb des **UpgradedEventEndpoint**-Handlers mithilfe der bewährten Vorgehensweisen der Datenbankplattform vorgenommen werden.

Weitere Informationen zum Erstellen eines Ereignishandlers für das Add-In-Ereignis finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md) und [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md). 

Im folgende Verfahren wird davon ausgegangen, dass Sie das Add-In-Ereignisempfänger-Element zu einem SharePoint-Add-In-Projekt in Visual Studio hinzugefügt haben. 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a>So behandeln Sie das Add-In-Updated-Ereignis beim ersten Mal

1. Öffnen Sie die Datei AppEventReceiver.svc.cs und fügen Sie eine bedingte Struktur zur **ProcessEvent**-Methode hinzu, die überprüft, ob es sich bei dem Ereignis, das den Handler aufgerufen hat, um das Updated-Ereignis handelt. Der Aktualisierungscode wird in diese Struktur eingefügt. Wenn der Code auf SharePoint zugreifen muss, können Sie das SharePoint-Clientobjektmodell für verwalteten Code (CSOM) oder eine REST-Schnittstelle (Representational State Transfer) verwenden. 

   Wo sich die bedingte Struktur in der Methode befindet, hängt von der Strukturierung des übrigen Codes in der Methode ab. In der Regel handelt es sich um einen Peer mit ähnlichen bedingten Strukturen, der die Add-In-Installed- und Add-In-Uninstalling-Ereignisse überprüft. Er kann sich innerhalb einer bedingten Struktur befinden, die bestimmte Eigenschaften oder untergeordnete Eigenschaften des Objekts **SPRemoteEventProperties**, das an **ProcessEvent** weitergegeben wird, auf **Null**- oder andere ungültige Werte überprüft. Er kann sich auch innerhalb eines **Try**-Blocks befinden. 
   
   Nachfolgend finden Sie ein Beispiel für die Struktur. Das _Eigenschaften_-Objekt ist ein **SPRemoteEventProperties**-Objekt.
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
     }

    ```

2. Wenn Sie CSOM im Ereignishandler verwenden möchten, fügen Sie (im bedingten Block) einen **Using**-Block hinzu, der ein **ClientContext**-Objekt erhält, indem er die **TokenHelper.CreateAppEventClientContext**-Methode abruft. Geben Sie **true** für den zweiten Parameter an, um auf das Add-In-Web zuzugreifen. Geben Sie **false** an, um auf das Hostweb zuzugreifen. Wenn Sie auf beide zugreifen möchten, benötigen Sie zwei verschiedene Clientkontextobjekte.

3. Wenn Ihr Handler auf Nicht-SharePoint-Komponenten zugreifen muss, fügen Sie diesen Code außerhalb von Clientkontextblöcken ein. Ihr Code sollte in etwa folgendermaßen strukturiert sein:
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, true))
         {
             // CSOM code that accesses the add-in web
         }
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, false))
         {
             // CSOM code that accesses the host web
         }
         // Other update code
     }

    ```

4. Um die REST-Schnittstelle zu verwenden, verwendet Ihr Code andere Methoden in der **TokenHelper**-Klasse, um ein Zugriffstoken zu erhalten, das dann in die Anforderungen eingefügt wird, die an SharePoint gesendet werden. Weitere Informationen finden Sie in  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md). Ihr Code sollte in etwa folgendermaßen strukturiert sein.
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);
         if (contextTokenString != null)
         {
             contextToken = TokenHelper.ReadAndValidateContextToken(contextTokenString, 
                                                                                                                       Request.Url.Authority);
             accessToken = TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                        .AccessToken;

            // REST code that accesses SharePoint
         }  
         // Other update code
     }

    ```

5. Für den Zugriff auf SharePoint muss der REST-Code zudem die URL des Hostwebs und/oder des Add-In-Webs kennen. Diese URLs sind beide untergeordnete Eigenschaften des **SPRemoteEventProperties**-Objekts, das an die **ProcessEvent**-Methode übergeben wird. Der folgende Code veranschaulicht das Abrufen der URLs.
    
    ```C#
       Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
       Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
    ```

Wenn Sie eine App das zweite (oder dritte usw.) Mal aktualisieren, müssen Sie möglicherweise sicherstellen, dass Updatelogik nicht mehrere Male auf der gleichen App-Instanz ausgeführt wird. Das folgende Verfahren zeigt, wie Sie dabei vorgehen.

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a>So behandeln Sie das Add-In-Updated-Ereignis bei weiteren Updates

1. Öffnen Sie die Datei AppEventReceiver.svc.cs und suchen Sie den Code, der beim ersten Update (von 1.0.0.0. auf 2.0.0.0) Updateaktionen implementiert hat. Wir bezeichnen diesen Code als vorherigen Updatecode. (Dieser Code ist normalerweise nach dem Autorisierungscode platziert, der Clientkontext oder Zugriffstoken abruft.) Nachdem Sie jetzt ein erneutes Update (von 2.0.0.0 auf 3.0.0.0) durchführen, befinden sich hier normalerweise Aktionen im vorherigen Updatecode, die nicht noch einmal auf der gleichen App-Instanz ausgeführt werden sollen. Sie sollen aber auf einer App-Instanz ausgeführt werden, die noch nicht auf 2.0.0.0 aktualisiert wurde (in diesem Fall wird die Instanz jetzt direkt von 1.0.0.0. auf 3.0.0.0 aktualisiert).

2. Umschließen Sie den vorherigen Updatecode mit einer Bedingungsstruktur, die auf die vorherige Version der App-Instanz testet und nur ausgeführt wird, wenn der Code in der Struktur auf dieser App-Instanz zuvor noch nicht ausgeführt wurde. Die vorherige Version der Instanz wird in der untergeordneten **PreviousVersion** -Eigenschaft des **SPRemoteEventProperties**-Objekts gespeichert.

3. Fügen Sie die neue Updatelogik (für die Aktualisierung von 2.0.0.0 auf 3.0.0.0) zu dieser Struktur hinzu. Es folgt ein Beispiel.
    
    ```C#
       Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
     }
     // Code to update from 2.0.0.0 to 3.0.0.0 is here.

    ```

4. Wiederholen Sie diese Schritte für jedes weitere Update. Für das Update von 3.0.0.0 auf 4.0.0.0 sollte Ihr Code die folgende Struktur aufweisen.
    
    ```C#
     Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 is here.
     }

     Version ver3OOO = new Version("3.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver3OOO)
     {
         // Code to update from 2.0.0.0 to 3.0.0.0 (previous update code) is here.
     }
     // Code to update from 3.0.0.0 to 4.0.0.0 is here.

    ```

> [!IMPORTANT]
> Wenn Sie eine Komponente zu einem Add-In in einem **UpgradedEventEndpoint**-Handler hinzufügen, stellen Sie sicher, dass Sie den gleichen Code zum **InstalledEventEndpoint**-Handler hinzufügen, da diese Komponente ebenfalls im Add-In einer völlig neuen Installation enthalten sein soll. Darüber hinaus sollten Sie einen [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) für das Add-In hinzufügen (oder überarbeiten), um die Komponente zu entfernen. 

> In den meisten Fällen sollte alles, was durch den **InstalledEventEndpoint** hinzugefügt oder geändert wurde, vom **UninstallingEventEndpoint** bearbeitet oder gelöscht werden. Eine Ausnahme bilden Daten, die nach dem Löschen des Add-Ins weiterhin nützlich sind. Diese Daten sollten nicht aus dem endgültigen Papierkorb gelöscht werden. (Websites zusätzlich zum Add-In-Web, die durch das Add-in erstellt werden, sollten als Daten betrachtet werden.)

<a name="AddRollbackLogic"> </a>
## <a name="add-rollback-logic-to-the-handler"></a>Hinzufügen von Rollbacklogik zum Handler

Wenn ein Fehler bei der Aktualisierung eines Add-Ins auftritt, stoppt die SharePoint-Infrastruktur den Updatevorgang und führt ein Rollback der Add-In-Instanz und aller dazugehörigen Komponenten auf die vorherige Version der Add-In-Instanz durch. Da die Infrastruktur nicht wissen kann, was Ihre **UpgradedEventEndpoint**-Handlerlogik tut, können diese Vorgänge nicht immer rückgängig gemacht werden. Wenn ein unbehandelter Ausnahmefehler bei der Ausführung des **UpgradedEventEndpoint**-Handlers ausgelöst wird, bedeutet dies fast immer, dass der gesamte Add-In-Updatevorgang rückgängig gemacht werden sollte, dies aber nicht möglich ist, da die Infrastruktur nicht weiß, wie sie Aktionen rückgängig machen kann, die der **UpgradedEventEndpoint**-Code durchgeführt hat. Aus diesem Grund muss der **UpgradedEventEndpoint**-Code folgende Aufgaben ausführen:

- Er muss alle Ausnahmen abfangen.
    
- Er muss zu benutzerdefiniertem Rollback-Code verzweigen, um alle bis zu diesem Zeitpunkt erfolgten Aktionen zurückzusetzen.
    
- Er muss der SharePoint-Infrastruktur signalisieren, dass das gesamte App-Update zurückgesetzt werden sollte.
    
- Er muss eine Fehlermeldung an die Infrastruktur weiterleiten.

Nicht alle Aktionen des **UpgradedEventEndpoint** müssen explizit im Handler rückgängig gemacht werden. Das Add-In-Web wird von der Infrastruktur zurückgesetzt, sodass der Code keine Änderungen am Add-In-Web rückgängig machen muss. Der **UpgradedEventEndpoint**-Handler muss jedoch in der Regel die Änderungen rückgängig machen, die er am Hostweb oder anderen Komponenten vorgenommen hat, die sich außerhalb des SharePoint-Add-Ins befinden.

Beim zweiten (oder dritten usw.) Update muss Ihre Ausnahmebehandlungslogik die Tatsache berücksichtigen, dass die App-Instanz, die aktualisiert wird, nicht unbedingt die unmittelbar vorhergehende Version ist. Ist sie dies nicht, müssen möglicherweise zwei oder mehr Blöcke mit Updatecode rückgängig gemacht werden. Aus diesem Grund benötigen Sie Bedingungslogik, die auf der Nummer der vorherigen Version basiert. Es folgt ein Beispiel für die Rollback-Logik für ein Update auf Version 4.0.0.0.

```C#
catch (Exception e)
{ 
    // Rollback of the 3.0.0.0 to 4.0.0.0 update logic goes here.

    Version ver3OOO = new Version("3.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver3OOO)
    {
        // Rollback of the 2.0.0.0 to 3.0.0.0 update logic goes here.
    }

    Version ver2OOO = new Version("2.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver2OOO)
    {
        // Rollback of the 1.0.0.0 to 2.0.0.0 update logic goes here.
    }
}
```

Als letzter Schritt der Fehlerbehandlung sollten dem **SPRemoteEventResult** -Objekt eine Fehlermeldung und ein Abbruchstatus zugewiesen werden, die von der **ProcessEvent**-Methode an die SharePoint-Update-Infrastruktur zurückgegeben werden. Es folgt ein Beispiel. In diesem Code ist das _Ergebnis_ ein **SPRemoteEventResult**-Objekt, das zuvor in der **ProcessEvent**-Methode deklariert wurde.

```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```

> [!IMPORTANT]
> Das Zuweisen von **SPRemoteEventServiceStatus.CancelWithError** (oder **SPRemoteEventServiceStatus.CancelNoError**) zu der Eigenschaft **Status** ist von entscheidender Bedeutung. Diese Eigenschaft signalisiert der Infrastruktur, dass ein Rollback des Updates durchgeführt werden soll. SharePoint ruft den Handler drei Mal auf, bevor das Rollback des Updates erfolgt.

### <a name="use-the-handler-delegation-strategy"></a>Verwenden der Handlerdelegierungsstrategie

Die unter [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) beschriebene Handlerdelegierungsstrategie kann ebenfalls in einem **UpdatedEventHandler** verwendet werden. Nicht nur die Rollback- und die „Bereits erledigt“-Logik werden gebündelt und auf der Remotekomponente ausgeführt, sondern auch die Versionsverwaltungslogik. Die Grenzen dieser Strategie gelten auch hier; Sie können sie in der Regel nur für die Aktualisierung eines Remotesystems verwenden.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md)
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md)
-  [UpgradedEventEndpoint-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In-Manifest)](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
-  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md)
-  [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md)
    
 

