# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a>Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins
Erstellen und verwenden Sie einen Handler für das Ereignis zum Aktualisieren eines SharePoint-Add-Ins.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="prerequisites-for-creating-a-handler-for-the-add-in-update-event"></a>Voraussetzungen für das Erstellen eines Handlers für das Add-In-Updateereignis
<a name="Prerequisites"> </a>

Sie sollten umfassend mit den Themen [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) und [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins) sowie den darin aufgeführten Voraussetzungen und Kernkonzepten vertraut sein.
 

 

## <a name="create-an-upgradedeventendpoint-receiver"></a>Erstellen eines UpgradedEventEndpoint-Empfängers
<a name="UpgradedEventEndpoint"> </a>


 **HINWEIS**   **Versionsnummerierungssystem:** Aus Konsistenzgründen wird bei diesem Thema davon ausgegangen, dass die App-Versionsnummern 1.0.0.0, 2.0.0.0, 3.0.0.0 usw.lauten. Die Logik und Anweisungen gelten jedoch unabhängig vom Nummerierungssystem, das Sie verwenden.
 

Für benutzerdefinierte Updatelogik können Sie einen SharePoint-Remoteereignisempfänger erstellen, der das AppUpdated-Ereignis verarbeitet. Sie sollten diese Technik allerdings sparsam einsetzen. Verwenden Sie sie nur für Aktualisierungsschritte, die nicht anderweitig durchgeführt werden können. Außerdem gelten die Hinweise in  [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) für das AppUpdated-Ereignis ebenso wie für die Ereignisse AppInstalled und AppUninstalling. Dies umfasst Folgendes:
 

 

- Der Handler muss innerhalb von 30 Sekunden abgeschlossen werden und einen Abbruch- oder Fortsetzungsstatus an SharePoint zurückgeben. Andernfalls ruft SharePoint den Handler bis zu drei Mal erneut auf.
    
 
- Wenn der Handler einen Abbruchstatus zurückgibt, versucht SharePoint es bis zu drei Mal erneut. 
    
 
- ie müssen in der Regel Rollback- und „Bereits erledigt“-Logik in den Ereignishandler einbeziehen.
    
 
Ein Szenario, in dem ein **UpgradedEventEndpoint**-Handler nützlich ist, ist das Hinzufügen eines berechneten Felds zu einer Remotedatenbank. Angenommen, die Spalte „Ort“ wird hinzugefügt, und der Wert wird anhand einer bereits bestehenden Postleitzahl-Spalte berechnet. Ihr Code in einem **UpgradedEventEndpoint**-Handler könnte vorhandene Elemente in der Datenbank durchlaufen und den Wert für das neue Ort-Feld auf Basis des Werts des Postleitzahl-Felds und einer externen Datenquelle, die Postleitzahlen Orten zuordnet, einfügen. Die Änderung am Datenbankschema selbst sollte außerhalb des **UpgradedEventEndpoint**-Handlers mithilfe der bewährten Vorgehensweisen der Datenbankplattform vorgenommen werden.
 

 
Ausführliche Informationen dazu, wie Sie einen Handler für das Add-In-Ereignis erstellen, finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins) und [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins). Bei den folgenden Verfahren wird davon ausgegangen, dass Sie das Add-In-Ereignisempfänger-Element zu Ihrem SharePoint-Add-In-Projekt in Visual Studio hinzugefügt haben. 
 

 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a>So behandeln Sie das Add-In-Updated-Ereignis beim ersten Mal


1. Öffnen Sie die AppEventReceiver.svc.cs-Datei, und fügen Sie der  **ProcessEvent** -Methode, die testet, ob das Ereignis, das den Handler aufgerufen hat, das Updated-Ereignis ist, eine Bedingungsstruktur hinzu. Ihr Aktualisierungscode wird in diese Struktur eingefügt. Wenn Ihr Code auf SharePoint zugreifen muss, können Sie die SharePoint-CSOM (Client Object Model)- oder REST (Representational State Transfer)-Schnittstelle verwenden. Wo in der Methode sich die Bedingungsstruktur befindet, hängt davon ab, wie Sie den anderen Code in der Methode strukturiert haben. Normalerweise sind die Bedingungsstrukturen, die auf Installations- und Deinstallationsereignisse von Apps testen, ähnlich. Sie kann sich innerhalb einer Bedingungsstruktur befinden, die bestimmte Eigenschaften oder untergeordnete Eigenschaften des **SPRemoteEventProperties** -Objekts testet, das an **ProcessEvent** für **null**-Werte oder andere ungültige Werte übergeben wird. Sie kann sich auch in einem **try**-Block befinden. Hier ist ein Beispiel für die Struktur. Das  _properties_-Objekt ist ein  **SPRemoteEventProperties** -Objekt.
    
```C#
  if (properties.EventType == SPRemoteEventType.AppUpgraded)
{
}

```

2. Um CSOM im Handler zu verwenden, fügen Sie (innerhalb des Bedingungsblocks) einen **using**-Block hinzu, der ein **ClientContext**-Objekt durch das Aufrufen der **TokenHelper.CreateAppEventClientContext**-Methode abruft. Geben Sie für den zweiten Parameter **true** an, um auf das Add-In-Web zuzugreifen. Geben Sie **false** an, um auf das Hostweb zuzugreifen. Wenn Sie auf beide zugreifen müssen, benötigen Sie zwei unterschiedliche Clientkontextobjekte.
    
 
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

4. Um die REST-Schnittstelle zu verwenden, verwendet Ihr Code andere Methoden in der **TokenHelper**-Klasse, um ein Zugriffstoken abzurufen, das dann in die Anforderungen eingefügt wird, die an SharePoint gesendet werden. Weitere Informationen finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints). Ihr Code sollte in etwa folgendermaßen strukturiert sein.
    
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

5. Um auf SharePoint zuzugreifen, muss Ihr REST-Code auch die URL des Hostwebs und/oder App-Webs kennen. Diese URLs sind beide untergeordnete Eigenschaften des  **SPRemoteEventProperties** -Objekts, das an die **ProcessEvent** -Methode übergeben wird. Der folgende Code zeigt, wie Sie die URLs abrufen.
    
```C#
  Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
```

Wenn Sie eine App das zweite (oder dritte usw.) Mal aktualisieren, müssen Sie möglicherweise sicherstellen, dass Updatelogik nicht mehrere Male auf der gleichen App-Instanz ausgeführt wird. Das folgende Verfahren zeigt, wie Sie dabei vorgehen.
 

 

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a>So behandeln Sie das App-Updated-Ereignis bei weiteren Updates


1. Öffnen Sie die AppEventReceiver.svc.cs-Datei, und suchen Sie den Code, der beim ersten Update (von 1.0.0.0. auf 2.0.0.0) Updateaktionen implementiert hat. Wir nennen diesen Code den vorherigen Updatecode. (Dieser Code ist normalerweise nach dem Autorisierungscode platziert, der Clientkontext oder Zugriffstoken abruft.) Nachdem Sie jetzt ein erneutes Update (von 2.0.0.0 auf 3.0.0.0) durchführen, befinden sich hier normalerweise Aktionen im vorherigen Updatecode, die nicht noch einmal auf der gleichen App-Instanz ausgeführt werden sollen. Sie sollen aber auf einer App-Instanz ausgeführt werden, die noch nicht auf 2.0.0.0 aktualisiert wurde (in diesem Fall wird die Instanz jetzt direkt von 1.0.0.0. auf 3.0.0.0 aktualisiert).
    
 
2. Umschließen Sie den vorherigen Updatecode mit einer Bedingungsstruktur, die auf die vorherige Version der App-Instanz testet und nur ausgeführt wird, wenn der Code in der Struktur auf dieser App-Instanz zuvor noch nicht ausgeführt wurde. Die vorherige Version der Instanz wird in der untergeordneten  **PreviousVersion** -Eigenschaft des **SPRemoteEventProperties** -Objekts gespeichert.
    
 
3. Fügen Sie Ihre neue Updatelogik (für das Update von 2.0.0.0 auf 3.0.0.0) unterhalb dieser Struktur ein. Hier ist ein Beispiel.
    
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


 **Wichtig** Wenn Sie eine Komponente zu einem Add-In in einem **UpgradedEventEndpoint**-Handler hinzufügen, sollten Sie den gleichen Code zu einem **InstalledEventEndpoint**-Handler hinzufügen, da diese Komponente auch bei einer Neuinstallation im Add-In enthalten sein soll. Außerdem sollten Sie für das Add-In einen [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) hinzufügen (oder diesen überarbeiten), um die Komponente zu entfernen. Fast alles, was durch den **InstalledEventEndpoint** hinzugefügt oder geändert wurde, sollte durch den **UninstallingEventEndpoint** zurückgesetzt oder gelöscht werden. Eine Ausnahme stellen Daten dar, die nach dem Entfernen des Add-Ins aus dem endgültigen Papierkorb weiterhin nützlich sind. Diese sollten nicht gelöscht werden. (Websites, mit Ausnahme des Add-In-Webs, die vom Add-In erstellt werden, sollten als Daten betrachtet werden.)
 


## <a name="add-rollback-logic-to-the-handler"></a>Hinzufügen von Rollback-Logik zum Handler
<a name="AddRollbackLogic"> </a>

Wenn beim Aktualisieren eines Add-Ins ein Fehler auftritt, stoppt die SharePoint-Infrastruktur den Updatevorgang und setzt die Add-In-Instanz und alle ihre Komponenten auf die vorherige Version der Add-In-Instanz zurück. Da die Infrastruktur nicht wissen kann, was Ihre **UpgradedEventEndpoint**-Handler-Logik tut, kann sie diese nicht immer zurücksetzen. Wenn eine unbehandelte Ausnahme ausgegeben wird, während Ihr **UpgradedEventEndpoint**-Handler ausgeführt wird, ist dies mit großer Sicherheit ein Hinweis darauf, dass der gesamte Add-In-Updateprozess zurückgesetzt werden sollte, was aber nicht passiert, da die Infrastruktur nicht weiß, wie einige Aktionen zurückgesetzt werden sollen, die Ihr **UpgradedEventEndpoint** -Code möglicherweise durchgeführt hat. Aus diesem Grund gilt für den **UpgradedEventEndpoint**-Code Folgendes:
 

 

1. Er muss alle Ausnahmen abfangen.
    
 
2. Er muss zu benutzerdefiniertem Rollback-Code verzweigen, um alle bis zu diesem Zeitpunkt erfolgten Aktionen zurückzusetzen.
    
 
3. Er muss der SharePoint-Infrastruktur signalisieren, dass das gesamte App-Update zurückgesetzt werden sollte.
    
 
4. Er muss eine Fehlermeldung an die Infrastruktur weiterleiten.
    
 
Nicht alles, was Ihr **UpgradedEventEndpoint** tut, muss im Handler explizit umgekehrt werden. Das Add-In-Web wird von der Infrastruktur zurückgesetzt, sodass Ihr Code keine Änderungen am Add-In-Web rückgängig machen muss. Der **UpgradedEventEndpoint**-Handler muss aber üblicherweise Änderungen rückgängig machen, die er am Hostweb oder anderen Komponenten vorgenommen hat, die sich außerhalb des SharePoint-Add-Ins befinden.
 

 
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

Ihr Fehlerbehandlung sollte dem  **SPRemoteEventResult** -Objekt, das die **ProcessEvent**-Methode an die SharePoint-Updateinfrastruktur zurückgibt, auf keinen Fall eine Fehlermeldung oder einen Abbruchstatus zuweisen. Hier ein Beispiel: In diesem Code ist  _Ergebnis_ ein **SPRemoteEventResult**-Objekt, das zuvor in der **ProcessEvent**-Methode deklariert wurde.
 

 



```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```


 **Wichtig** Wichtig ist, der **Status**-Eigenschaft **SPRemoteEventServiceStatus.CancelWithError** (oder **SPRemoteEventServiceStatus.CancelNoError**) zuzuweisen. Diese Eigenschaft signalisiert der Infrastruktur, das Update zurückzusetzen. Aber SharePoint ruft den Handler bis zu drei Mal auf, bevor das Update zurückgesetzt wird.
 


### <a name="use-the-handler-delegation-strategy"></a>Verwenden der Handlerdelegierungsstrategie

Die Handlerdelegierungsstrategie, die in  [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) beschrieben ist, kann ebenfalls in einem **UpdatedEventHandler** verwendet werden. Nicht nur Ihre Rollback- und "Bereits erledigt"-Logik sind gebündelt und werden auf der Remotekomponente ausgeführt, sondern auch Ihre Logik für die Versionsverwaltung. Die Einschränkungen der Strategie gelten hier ebenfalls: In der Regel können Sie damit nicht mehr als ein Remotesystem aktualisieren.
 

 

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Kehren Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.
 

 

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint-2013)
    
 
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins)
    
 
-  [UpgradedEventEndpoint-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In-Manifest)](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
    
 
-  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins)
    
 
-  [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins)
    
 

