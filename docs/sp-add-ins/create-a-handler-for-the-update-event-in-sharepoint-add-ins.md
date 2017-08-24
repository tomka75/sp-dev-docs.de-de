# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a><span data-ttu-id="9e272-101">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9e272-101">Create a handler for the update event in SharePoint Add-ins</span></span>
<span data-ttu-id="9e272-102">Erstellen und verwenden Sie einen Handler für das Ereignis zum Aktualisieren eines SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="9e272-102">Create and use a handler for the update event of a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="9e272-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9e272-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites-for-creating-a-handler-for-the-add-in-update-event"></a><span data-ttu-id="9e272-106">Voraussetzungen für das Erstellen eines Handlers für das Add-In-Updateereignis</span><span class="sxs-lookup"><span data-stu-id="9e272-106">Prerequisites for creating a handler for the add-in update event</span></span>
<span data-ttu-id="9e272-107"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="9e272-107"></span></span>

<span data-ttu-id="9e272-108">Sie sollten umfassend mit den Themen [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) und [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins) sowie den darin aufgeführten Voraussetzungen und Kernkonzepten vertraut sein.</span><span class="sxs-lookup"><span data-stu-id="9e272-108">Be thoroughly familiar with both  [Handling add-in events](handle-events-in-sharepoint-add-ins#HandlingAppEvents) and [Update SharePoint Add-ins](update-sharepoint-add-ins) and the prerequisites and core concepts listed in them.</span></span>
 

 

## <a name="create-an-upgradedeventendpoint-receiver"></a><span data-ttu-id="9e272-109">Erstellen eines UpgradedEventEndpoint-Empfängers</span><span class="sxs-lookup"><span data-stu-id="9e272-109">Create an UpgradedEventEndpoint receiver</span></span>
<span data-ttu-id="9e272-110"><a name="UpgradedEventEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="9e272-110"></span></span>


 <span data-ttu-id="9e272-p102">**HINWEIS**   **Versionsnummerierungssystem:** Aus Konsistenzgründen wird bei diesem Thema davon ausgegangen, dass die App-Versionsnummern 1.0.0.0, 2.0.0.0, 3.0.0.0 usw.lauten. Die Logik und Anweisungen gelten jedoch unabhängig vom Nummerierungssystem, das Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="9e272-p102">**Note**   **Version numbering system:** For consistency, this topic assumes that the add-in version numbers are 1.0.0.0, 2.0.0.0, 3.0.0.0, and so on. However, the logic and guidance applies no matter what your numbering system is.</span></span>
 

<span data-ttu-id="9e272-p103">Für benutzerdefinierte Updatelogik können Sie einen SharePoint-Remoteereignisempfänger erstellen, der das AppUpdated-Ereignis verarbeitet. Sie sollten diese Technik allerdings sparsam einsetzen. Verwenden Sie sie nur für Aktualisierungsschritte, die nicht anderweitig durchgeführt werden können. Außerdem gelten die Hinweise in  [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) für das AppUpdated-Ereignis ebenso wie für die Ereignisse AppInstalled und AppUninstalling. Dies umfasst Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9e272-p103">For custom update logic, you can create a SharePoint remote event receiver that handles the add-in updated event. You should be conservative in using this technique. Use it only for updating steps that can't be done any other way. Also, the guidance found in  [Handling add-in events](handle-events-in-sharepoint-add-ins#HandlingAppEvents) applies for the add-in updated event as much as the add-in installed and add-in uninstalling events. This includes:</span></span>
 

 

- <span data-ttu-id="9e272-p104">Der Handler muss innerhalb von 30 Sekunden abgeschlossen werden und einen Abbruch- oder Fortsetzungsstatus an SharePoint zurückgeben. Andernfalls ruft SharePoint den Handler bis zu drei Mal erneut auf.</span><span class="sxs-lookup"><span data-stu-id="9e272-p104">Your handler has to complete and return either a cancel or a continue status to SharePoint in 30 seconds. If it does not, SharePoint will call the handler again, up to three more times.</span></span>
    
 
- <span data-ttu-id="9e272-120">Wenn der Handler einen Abbruchstatus zurückgibt, versucht SharePoint es bis zu drei Mal erneut.</span><span class="sxs-lookup"><span data-stu-id="9e272-120">If your handler returns a cancel status, SharePoint will retry up to three more times.</span></span> 
    
 
- <span data-ttu-id="9e272-121">ie müssen in der Regel Rollback- und „Bereits erledigt“-Logik in den Ereignishandler einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="9e272-121">You usually need to include rollback and "already done" logic in your handler.</span></span>
    
 
<span data-ttu-id="9e272-p105">Ein Szenario, in dem ein **UpgradedEventEndpoint**-Handler nützlich ist, ist das Hinzufügen eines berechneten Felds zu einer Remotedatenbank. Angenommen, die Spalte „Ort“ wird hinzugefügt, und der Wert wird anhand einer bereits bestehenden Postleitzahl-Spalte berechnet. Ihr Code in einem **UpgradedEventEndpoint**-Handler könnte vorhandene Elemente in der Datenbank durchlaufen und den Wert für das neue Ort-Feld auf Basis des Werts des Postleitzahl-Felds und einer externen Datenquelle, die Postleitzahlen Orten zuordnet, einfügen. Die Änderung am Datenbankschema selbst sollte außerhalb des **UpgradedEventEndpoint**-Handlers mithilfe der bewährten Vorgehensweisen der Datenbankplattform vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="9e272-p105">One scenario in which an **UpgradedEventEndpoint** handler is useful is when a computed field is added to a remote database. Suppose a City column is added, and its value is computed from an already existing Postal Code column. Your code in an **UpgradedEventEndpoint** handler could iterate through existing items in the database and fill in the value for the new City field based on the value of the Postal Code field and some external data source that maps postal codes onto cities. The change to the database schema itself is best done outside the **UpgradedEventEndpoint** handler by using the best practices of the database platform.</span></span>
 

 
<span data-ttu-id="9e272-p106">Ausführliche Informationen dazu, wie Sie einen Handler für das Add-In-Ereignis erstellen, finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins) und [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins). Bei den folgenden Verfahren wird davon ausgegangen, dass Sie das Add-In-Ereignisempfänger-Element zu Ihrem SharePoint-Add-In-Projekt in Visual Studio hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="9e272-p106">For more details about how to create a handler for the app event, see Handling events in apps for SharePoint and How to: Create an app event receiver. The following procedure assumes that you have added the app event receiver item to your spappsing project in vsnv.</span></span> 
 

 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a><span data-ttu-id="9e272-128">So behandeln Sie das Add-In-Updated-Ereignis beim ersten Mal</span><span class="sxs-lookup"><span data-stu-id="9e272-128">To handle the add-in updated event the first time</span></span>


1. <span data-ttu-id="9e272-p107">Öffnen Sie die AppEventReceiver.svc.cs-Datei, und fügen Sie der  **ProcessEvent** -Methode, die testet, ob das Ereignis, das den Handler aufgerufen hat, das Updated-Ereignis ist, eine Bedingungsstruktur hinzu. Ihr Aktualisierungscode wird in diese Struktur eingefügt. Wenn Ihr Code auf SharePoint zugreifen muss, können Sie die SharePoint-CSOM (Client Object Model)- oder REST (Representational State Transfer)-Schnittstelle verwenden. Wo in der Methode sich die Bedingungsstruktur befindet, hängt davon ab, wie Sie den anderen Code in der Methode strukturiert haben. Normalerweise sind die Bedingungsstrukturen, die auf Installations- und Deinstallationsereignisse von Apps testen, ähnlich. Sie kann sich innerhalb einer Bedingungsstruktur befinden, die bestimmte Eigenschaften oder untergeordnete Eigenschaften des **SPRemoteEventProperties** -Objekts testet, das an **ProcessEvent** für **null**-Werte oder andere ungültige Werte übergeben wird. Sie kann sich auch in einem **try**-Block befinden. Hier ist ein Beispiel für die Struktur. Das  _properties_-Objekt ist ein  **SPRemoteEventProperties** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="9e272-p107">Open the AppEventReceiver.svc.cs file and add a conditional structure to the  **ProcessEvent** method that tests whether the event that invoked the handler is the updated event. Your updating code goes inside this structure. If your code needs to access SharePoint, you can use the SharePoint managed code client object model (CSOM) or Representational State Transfer (REST) interface. Where the conditional structure is located in the method depends on how you have structured the other code in the method. Typically, it is a peer of similar conditional structures that test for the add-in installed and add-in uninstalling events. It may be within a conditional structure that tests certain properties or subproperties of the **SPRemoteEventProperties** object that is passed to **ProcessEvent** for **null** values or other invalid values. It may also be within a **try** block. The following is an example of the structure. The _properties_ object is an **SPRemoteEventProperties** object.</span></span>
    
```C#
  if (properties.EventType == SPRemoteEventType.AppUpgraded)
{
}

```

2. <span data-ttu-id="9e272-p108">Um CSOM im Handler zu verwenden, fügen Sie (innerhalb des Bedingungsblocks) einen **using**-Block hinzu, der ein **ClientContext**-Objekt durch das Aufrufen der **TokenHelper.CreateAppEventClientContext**-Methode abruft. Geben Sie für den zweiten Parameter **true** an, um auf das Add-In-Web zuzugreifen. Geben Sie **false** an, um auf das Hostweb zuzugreifen. Wenn Sie auf beide zugreifen müssen, benötigen Sie zwei unterschiedliche Clientkontextobjekte.</span><span class="sxs-lookup"><span data-stu-id="9e272-p108">To use CSOM in the handler, add (within the conditional block) a **using** block that gets a **ClientContext** object by calling the **TokenHelper.CreateAppEventClientContext** method. Specify **true** for the second parameter to access the add-in web. Specify **false** to access the host web. If you need to access both, you will need two different client context objects.</span></span>
    
 
3. <span data-ttu-id="9e272-p109">Wenn Ihr Handler auf Nicht-SharePoint-Komponenten zugreifen muss, fügen Sie diesen Code außerhalb von Clientkontextblöcken ein. Ihr Code sollte in etwa folgendermaßen strukturiert sein:</span><span class="sxs-lookup"><span data-stu-id="9e272-p109">If your handler needs to access non-SharePoint components, put that code outside any client context blocks. Your code should be structured similarly to the following:</span></span>
    
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

4. <span data-ttu-id="9e272-p110">Um die REST-Schnittstelle zu verwenden, verwendet Ihr Code andere Methoden in der **TokenHelper**-Klasse, um ein Zugriffstoken abzurufen, das dann in die Anforderungen eingefügt wird, die an SharePoint gesendet werden. Weitere Informationen finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints). Ihr Code sollte in etwa folgendermaßen strukturiert sein.</span><span class="sxs-lookup"><span data-stu-id="9e272-p110">To use the REST interface, your code uses other methods in the **TokenHelper** class to get an access token, which is then included in the requests it makes to SharePoint. For more information, see [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-2013-rest-endpoints). Your code should be structured similarly to the following.</span></span>
    
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

5. <span data-ttu-id="9e272-p111">Um auf SharePoint zuzugreifen, muss Ihr REST-Code auch die URL des Hostwebs und/oder App-Webs kennen. Diese URLs sind beide untergeordnete Eigenschaften des  **SPRemoteEventProperties** -Objekts, das an die **ProcessEvent** -Methode übergeben wird. Der folgende Code zeigt, wie Sie die URLs abrufen.</span><span class="sxs-lookup"><span data-stu-id="9e272-p111">To access SharePoint, your REST code also needs to know the URL of the host web or add-in web or both. These URLs are both subproperties of the  **SPRemoteEventProperties** object that is passed to the **ProcessEvent** method. The following code shows how to get them.</span></span>
    
```C#
  Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
```

<span data-ttu-id="9e272-p112">Wenn Sie eine App das zweite (oder dritte usw.) Mal aktualisieren, müssen Sie möglicherweise sicherstellen, dass Updatelogik nicht mehrere Male auf der gleichen App-Instanz ausgeführt wird. Das folgende Verfahren zeigt, wie Sie dabei vorgehen.</span><span class="sxs-lookup"><span data-stu-id="9e272-p112">When you update an add-in for the second (or third, and so on) time, you may need to ensure that some update logic does not run multiple times on the same add-in instance. The following procedure shows you how.</span></span>
 

 

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a><span data-ttu-id="9e272-152">So behandeln Sie das App-Updated-Ereignis bei weiteren Updates</span><span class="sxs-lookup"><span data-stu-id="9e272-152">To handle the add-in updated event on subsequent updates</span></span>


1. <span data-ttu-id="9e272-p113">Öffnen Sie die AppEventReceiver.svc.cs-Datei, und suchen Sie den Code, der beim ersten Update (von 1.0.0.0. auf 2.0.0.0) Updateaktionen implementiert hat. Wir nennen diesen Code den vorherigen Updatecode. (Dieser Code ist normalerweise nach dem Autorisierungscode platziert, der Clientkontext oder Zugriffstoken abruft.) Nachdem Sie jetzt ein erneutes Update (von 2.0.0.0 auf 3.0.0.0) durchführen, befinden sich hier normalerweise Aktionen im vorherigen Updatecode, die nicht noch einmal auf der gleichen App-Instanz ausgeführt werden sollen. Sie sollen aber auf einer App-Instanz ausgeführt werden, die noch nicht auf 2.0.0.0 aktualisiert wurde (in diesem Fall wird die Instanz jetzt direkt von 1.0.0.0. auf 3.0.0.0 aktualisiert).</span><span class="sxs-lookup"><span data-stu-id="9e272-p113">Open the AppEventReceiver.svc.cs file, and find the code that implemented update actions in the first update (from 1.0.0.0. to 2.0.0.0). Let's call this the previous update code. (This code is generally located after the authorization code that gets client context or access tokens.) Now that you are updating again (from 2.0.0.0 to 3.0.0.0), there will typically be actions in the previous update code here that you don't want to run again on the same add-in instance, but you do want it to run on a add-in instance that was never updated to 2.0.0.0 (in which case, the instance is now being updated all the way from 1.0.0.0. to 3.0.0.0).</span></span>
    
 
2. <span data-ttu-id="9e272-p114">Umschließen Sie den vorherigen Updatecode mit einer Bedingungsstruktur, die auf die vorherige Version der App-Instanz testet und nur ausgeführt wird, wenn der Code in der Struktur auf dieser App-Instanz zuvor noch nicht ausgeführt wurde. Die vorherige Version der Instanz wird in der untergeordneten  **PreviousVersion** -Eigenschaft des **SPRemoteEventProperties** -Objekts gespeichert.</span><span class="sxs-lookup"><span data-stu-id="9e272-p114">Wrap the previous update code in a conditional structure that tests for the previous version of the add-in instance and executes only if the code in the structure has not run before on this add-in instance. The previous version of the instance is stored in the  **PreviousVersion** subproperty of the **SPRemoteEventProperties** object.</span></span>
    
 
3. <span data-ttu-id="9e272-p115">Fügen Sie Ihre neue Updatelogik (für das Update von 2.0.0.0 auf 3.0.0.0) unterhalb dieser Struktur ein. Hier ist ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="9e272-p115">Add your new update logic (for the update from 2.0.0.0 to 3.0.0.0) below this structure. The following is an example.</span></span>
    
```C#
  Version ver2OOO = new Version("2.0.0.0");
if (properties.AppEventProperties.PreviousVersion < ver2OOO)
{
    // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
}
// Code to update from 2.0.0.0 to 3.0.0.0 is here.

```

4. <span data-ttu-id="9e272-p116">Wiederholen Sie diese Schritte für jedes weitere Update. Für das Update von 3.0.0.0 auf 4.0.0.0 sollte Ihr Code die folgende Struktur aufweisen.</span><span class="sxs-lookup"><span data-stu-id="9e272-p116">For each subsequent update, repeat these steps. For the update from 3.0.0.0 to 4.0.0.0, your code should have the following structure.</span></span>
    
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


 <span data-ttu-id="9e272-p117">**Wichtig** Wenn Sie eine Komponente zu einem Add-In in einem **UpgradedEventEndpoint**-Handler hinzufügen, sollten Sie den gleichen Code zu einem **InstalledEventEndpoint**-Handler hinzufügen, da diese Komponente auch bei einer Neuinstallation im Add-In enthalten sein soll. Außerdem sollten Sie für das Add-In einen [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) hinzufügen (oder diesen überarbeiten), um die Komponente zu entfernen. Fast alles, was durch den **InstalledEventEndpoint** hinzugefügt oder geändert wurde, sollte durch den **UninstallingEventEndpoint** zurückgesetzt oder gelöscht werden. Eine Ausnahme stellen Daten dar, die nach dem Entfernen des Add-Ins aus dem endgültigen Papierkorb weiterhin nützlich sind. Diese sollten nicht gelöscht werden. (Websites, mit Ausnahme des Add-In-Webs, die vom Add-In erstellt werden, sollten als Daten betrachtet werden.)</span><span class="sxs-lookup"><span data-stu-id="9e272-p117">**Important** If you add a component to an add-in in an **UpgradedEventEndpoint** handler, be sure to add the same code to an **InstalledEventEndpoint** handler because you want that component included in the add-in on a brand new installation as well. Also, you should add an [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) (or revise it) for the add-in to remove the component. For the most part, anything that was added or changed by the **InstalledEventEndpoint** should be reversed or deleted by the **UninstallingEventEndpoint**. One exception is that data that will remain useful after the add-in is removed from the second-stage recycle bin should not be deleted. (Websites, other than the add-in web, that are created by the add-in should be considered data.)</span></span>
 


## <a name="add-rollback-logic-to-the-handler"></a><span data-ttu-id="9e272-169">Hinzufügen von Rollback-Logik zum Handler</span><span class="sxs-lookup"><span data-stu-id="9e272-169">Add rollback logic to the handler</span></span>
<span data-ttu-id="9e272-170"><a name="AddRollbackLogic"> </a></span><span class="sxs-lookup"><span data-stu-id="9e272-170"></span></span>

<span data-ttu-id="9e272-p118">Wenn beim Aktualisieren eines Add-Ins ein Fehler auftritt, stoppt die SharePoint-Infrastruktur den Updatevorgang und setzt die Add-In-Instanz und alle ihre Komponenten auf die vorherige Version der Add-In-Instanz zurück. Da die Infrastruktur nicht wissen kann, was Ihre **UpgradedEventEndpoint**-Handler-Logik tut, kann sie diese nicht immer zurücksetzen. Wenn eine unbehandelte Ausnahme ausgegeben wird, während Ihr **UpgradedEventEndpoint**-Handler ausgeführt wird, ist dies mit großer Sicherheit ein Hinweis darauf, dass der gesamte Add-In-Updateprozess zurückgesetzt werden sollte, was aber nicht passiert, da die Infrastruktur nicht weiß, wie einige Aktionen zurückgesetzt werden sollen, die Ihr **UpgradedEventEndpoint** -Code möglicherweise durchgeführt hat. Aus diesem Grund gilt für den **UpgradedEventEndpoint**-Code Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9e272-p118">If an error occurs when an add-in is being updated, the SharePoint infrastructure stops the update process and rolls back the add-in instance and all its components to the previous version of the add-in instance. But the infrastructure has no way of knowing what your **UpgradedEventEndpoint** handler logic does, so it can't always undo it. An unhandled exception thrown while your **UpgradedEventEndpoint** handler is executing almost certainly indicates that the entire add-in update process should be rolled back, but it won't be because the infrastructure doesn't know how to undo some things your **UpgradedEventEndpoint** code might have done. For this reason, the **UpgradedEventEndpoint** code must:</span></span>
 

 

1. <span data-ttu-id="9e272-175">Er muss alle Ausnahmen abfangen.</span><span class="sxs-lookup"><span data-stu-id="9e272-175">Catch all exceptions.</span></span>
    
 
2. <span data-ttu-id="9e272-176">Er muss zu benutzerdefiniertem Rollback-Code verzweigen, um alle bis zu diesem Zeitpunkt erfolgten Aktionen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="9e272-176">Branch to custom rollback code to undo what it has been done to that point.</span></span>
    
 
3. <span data-ttu-id="9e272-177">Er muss der SharePoint-Infrastruktur signalisieren, dass das gesamte App-Update zurückgesetzt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="9e272-177">Signal to the SharePoint infrastructure that the entire add-in update should be rolled back.</span></span>
    
 
4. <span data-ttu-id="9e272-178">Er muss eine Fehlermeldung an die Infrastruktur weiterleiten.</span><span class="sxs-lookup"><span data-stu-id="9e272-178">Pass on an error message to the infrastructure.</span></span>
    
 
<span data-ttu-id="9e272-p119">Nicht alles, was Ihr **UpgradedEventEndpoint** tut, muss im Handler explizit umgekehrt werden. Das Add-In-Web wird von der Infrastruktur zurückgesetzt, sodass Ihr Code keine Änderungen am Add-In-Web rückgängig machen muss. Der **UpgradedEventEndpoint**-Handler muss aber üblicherweise Änderungen rückgängig machen, die er am Hostweb oder anderen Komponenten vorgenommen hat, die sich außerhalb des SharePoint-Add-Ins befinden.</span><span class="sxs-lookup"><span data-stu-id="9e272-p119">Not everything your **UpgradedEventEndpoint** does needs to be explicitly reversed inside the handler. The add-in web is going to be rolled back by the infrastructure, so your code does not have to undo changes to the add-in web. But the **UpgradedEventEndpoint** handler usually does have to reverse changes it has made to the host web or other components that are external to the SharePoint Add-in.</span></span>
 

 
<span data-ttu-id="9e272-p120">Beim zweiten (oder dritten usw.) Update muss Ihre Ausnahmebehandlungslogik die Tatsache berücksichtigen, dass die App-Instanz, die aktualisiert wird, nicht unbedingt die unmittelbar vorhergehende Version ist. Ist sie dies nicht, müssen möglicherweise zwei oder mehr Blöcke mit Updatecode rückgängig gemacht werden. Aus diesem Grund benötigen Sie Bedingungslogik, die auf der Nummer der vorherigen Version basiert. Es folgt ein Beispiel für die Rollback-Logik für ein Update auf Version 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="9e272-p120">On the second (or third, and so on) update, your exception handing logic has to take account of the fact that the add-in instance that is being updated is not necessarily the immediately previous version. If it isn't, there may be two or more blocks of update code that need to be reversed. For this reason, you need conditional logic that is based on the number of the previous version. The following is an example of the rollback logic for an update to version 4.0.0.0.</span></span>
 

 



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

<span data-ttu-id="9e272-p121">Ihr Fehlerbehandlung sollte dem  **SPRemoteEventResult** -Objekt, das die **ProcessEvent**-Methode an die SharePoint-Updateinfrastruktur zurückgibt, auf keinen Fall eine Fehlermeldung oder einen Abbruchstatus zuweisen. Hier ein Beispiel: In diesem Code ist  _Ergebnis_ ein **SPRemoteEventResult**-Objekt, das zuvor in der **ProcessEvent**-Methode deklariert wurde.</span><span class="sxs-lookup"><span data-stu-id="9e272-p121">The last things your error handling should do is assign an error message and a cancel status to the  **SPRemoteEventResult** object that the **ProcessEvent** method returns to the SharePoint update infrastructure. The following is an example. In this code, _result_ is an **SPRemoteEventResult** object that has been declared earlier in the **ProcessEvent** method.</span></span>
 

 



```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```


 <span data-ttu-id="9e272-p122">**Wichtig** Wichtig ist, der **Status**-Eigenschaft **SPRemoteEventServiceStatus.CancelWithError** (oder **SPRemoteEventServiceStatus.CancelNoError**) zuzuweisen. Diese Eigenschaft signalisiert der Infrastruktur, das Update zurückzusetzen. Aber SharePoint ruft den Handler bis zu drei Mal auf, bevor das Update zurückgesetzt wird.</span><span class="sxs-lookup"><span data-stu-id="9e272-p122">**Important** Assigning **SPRemoteEventServiceStatus.CancelWithError** (or **SPRemoteEventServiceStatus.CancelNoError**) to the  **Status** property is crucial. This property is what signals the infrastructure to roll back the update. But SharePoint will retry your handler three times before it rolls back the update.</span></span>
 


### <a name="use-the-handler-delegation-strategy"></a><span data-ttu-id="9e272-192">Verwenden der Handlerdelegierungsstrategie</span><span class="sxs-lookup"><span data-stu-id="9e272-192">Use the handler delegation strategy</span></span>

<span data-ttu-id="9e272-p123">Die Handlerdelegierungsstrategie, die in  [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins#HandlingAppEvents) beschrieben ist, kann ebenfalls in einem **UpdatedEventHandler** verwendet werden. Nicht nur Ihre Rollback- und "Bereits erledigt"-Logik sind gebündelt und werden auf der Remotekomponente ausgeführt, sondern auch Ihre Logik für die Versionsverwaltung. Die Einschränkungen der Strategie gelten hier ebenfalls: In der Regel können Sie damit nicht mehr als ein Remotesystem aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9e272-p123">The handler delegation strategy that is described in  [Handling add-in events](handle-events-in-sharepoint-add-ins#HandlingAppEvents) can be used in an **UpdatedEventHandler** too. Not only is your rollback and "already done" logic bundled and run on the remote component, but your versioning logic is too. The limitations of the strategy apply here too: you usually can't use it to update more than one remote system.</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="9e272-196">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="9e272-196">Next steps</span></span>
<span data-ttu-id="9e272-197"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="9e272-197"></span></span>

<span data-ttu-id="9e272-198">Kehren Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9e272-198">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="9e272-199">Aktualisieren von Add-In-Webkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9e272-199">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="9e272-200">Aktualisieren von Hostwebkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9e272-200">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="9e272-201">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9e272-201">Update remote components in SharePoint Add-ins</span></span>](update-remote-components-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="9e272-202">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9e272-202">Additional resources</span></span>
<span data-ttu-id="9e272-203"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9e272-203"></span></span>


-  [<span data-ttu-id="9e272-204">Aktualisieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9e272-204">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9e272-205">UpgradedEventEndpoint-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In-Manifest)</span><span class="sxs-lookup"><span data-stu-id="9e272-205">UpgradedEventEndpoint element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)</span></span>](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="9e272-206">Behandeln von Ereignissen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9e272-206">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9e272-207">Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9e272-207">Create an add-in event receiver in SharePoint Add-ins</span></span>](create-an-add-in-event-receiver-in-sharepoint-add-ins)
    
 

