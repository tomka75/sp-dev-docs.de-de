---
title: Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 75716bd2be1793b8df91e7d9bdac06b762d622fb
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data"></a><span data-ttu-id="4daab-102">Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten</span><span class="sxs-lookup"><span data-stu-id="4daab-102">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>
<span data-ttu-id="4daab-103">Verwenden Sie das SharePoint-JavaScript-Objektmodell, um mit SharePoint-Daten aus JavaScript auf Seiten im Add-In-Web zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="4daab-103">Use the SharePoint JavaScript object model to work with SharePoint data from JavaScript on pages in the add-in web.</span></span>
 

 <span data-ttu-id="4daab-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="4daab-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="4daab-107">Dies ist der zehnte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="4daab-107">This is the 10th in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="4daab-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="4daab-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="4daab-109">Bereitstellung und Installation eines von SharePoint gehosteten Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-110">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-111">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-112">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-113">Hinzufügen eines Workflows zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-114">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="4daab-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-115">Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint-gehostetes SharePoint Add-In</span><span class="sxs-lookup"><span data-stu-id="4daab-115">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="4daab-116">Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="4daab-116">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
    
 

 <span data-ttu-id="4daab-p102">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Lösung, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter  [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeJSOM.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="4daab-p102">**Note**  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeJSOM.sln file.</span></span>
 

<span data-ttu-id="4daab-p103">Obwohl von SharePoint gehostete SharePoint-Add-Ins keinen serverseitigen Code enthalten können, können Sie dennoch über eine Geschäftslogik und Laufzeitinteraktion mit SharePoint-Komponenten in einer von SharePoint-gehosteten SharePoint-Add-In verfügen, indem Sie JavaScript und die SharePoint-JavaScript-Clientobjektmodell-Bibliothek verwenden. (Wir nennen sie JSOM. Beachten Sie das „M" am Ende. Verwechseln Sie dies nicht mit JSO **N** [JavaScript Object Notation].) In diesem Artikel verwenden Sie das JavaScript-Objektmodell, um alte Elemente in der Liste **Neue Mitarbeiter in Seattle** zu suchen und daraus zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="4daab-p103">Even though SharePoint-hosted SharePoint Add-ins cannot have server-side code, you can still have business logic and runtime interaction with SharePoint components in a SharePoint-hosted SharePoint Add-in by using JavaScript and the SharePoint JavaScript client object model library. (We'll call it JSOM. Note the "M" on the end. Don't confuse this with JSO **N** [JavaScript Object Notation].) In this article you use the JavaScript object model to find and remove old items from the **New Employees in Seattle** list.</span></span>
 

## <a name="create-the-javascript-and-a-button-to-invoke-it"></a><span data-ttu-id="4daab-123">Erstellen des JavaScript und einer Schaltfläche zum Aufrufen</span><span class="sxs-lookup"><span data-stu-id="4daab-123">Create the JavaScript and a button to invoke it</span></span>


1. <span data-ttu-id="4daab-124">Stellen Sie sicher, dass der folgende Schritt aus dem ersten Lernprogramm in dieser Reihe abgeschlossen wurde:</span><span class="sxs-lookup"><span data-stu-id="4daab-124">Verify that the following step from the first tutorial in this series was completed:</span></span> 
    
    <span data-ttu-id="4daab-p104">Öffnen Sie die Datei **/Pages/Default.aspx** aus dem Stammverzeichnis des Projekts. Unter anderem lädt diese generierte Datei eines oder beide der zwei Skripts, die auf SharePoint: sp.runtime.js und sp.js gehostet werden. Das Markup zum Laden dieser Dateien befindet sich im **Content**-Steuerelement im oberen Bereich der Datei mit der ID **PlaceHolderAdditionalPageHead**. Das Markup variiert in Abhängigkeit von der **Microsoft Office-Entwicklertools für Visual Studio**-Version, die Sie verwenden. Diese Reihe von Lernprogrammen erfordert, dass beide Dateien geladen werden und sie mit normalen HTML **\<Skript\>**-Tags und nicht mit **\<SharePoint:ScriptLink\>**-Tags geladen werden. Stellen Sie sicher, dass die folgenden Zeilen im **PlaceHolderAdditionalPageHead**-Steuerelement *über* der Zeile `<meta name="WebPartPageExpansion" content="full" />` enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="4daab-p104">Open the file  **/Pages/Default.aspx** from the root of the project. Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js. The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**. The markup varies depending on the version of  **Microsoft Office Developer Tools for Visual Studio** that you are using. This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags. Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above*  the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>
    


```
  <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
<script type="text/javascript" src="/_layouts/15/sp.js"></script> 

```


    Then search the file for any other markup that also loads one or the other of these files and remove the redundant markup. Save and close the file.
    
 
2. <span data-ttu-id="4daab-p105">In Knoten **Skripts** im **Projektmappen-Explorer** ist möglicherweise bereits eine Add-in.js-Datei vorhanden. Ist dies nicht der Fall, aber eine App.js-Datei vorhanden, klicken Sie mit der rechten Maustaste auf App.js, und benennen Sie sie in Add-in.js um. Wenn weder Add-in.js noch App.js vorhanden ist, erstellen Sie die Datei mit den folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="4daab-p105">In the  **Scripts** node in **Solution Explorer**, there may already be an Add-in.js file. If there isn't, but there is an App.js, right-click App.js and rename it Add-in.js. If there isn't either an Add-in.js or App.js, create one with these steps:</span></span>
    
      1. <span data-ttu-id="4daab-134">Klicken Sie mit der rechten Maustaste auf den Knoten **Scripts**, und wählen Sie **Hinzufügen** > **Neues Element** > **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="4daab-134">Right-click the  **Scripts** node and choose **Add** > **New Item** > **Web**.</span></span>
    
 
  2. <span data-ttu-id="4daab-135">Wählen Sie **JavaScript-Datei** aus, und nennen Sie die DateiAdd-in.js.</span><span class="sxs-lookup"><span data-stu-id="4daab-135">Choose  **JavaScript File** and name itAdd-in.js.</span></span>
    
 
3. <span data-ttu-id="4daab-136">Öffnen Sie Add-in.js, und löschen Sie ihren Inhalt, falls vorhanden.</span><span class="sxs-lookup"><span data-stu-id="4daab-136">Open Add-in.js and delete its content, if there is any.</span></span>
    
 
4. <span data-ttu-id="4daab-p106">Fügen Sie der Datei die folgenden Zeilen hinzu. Beachten Sie Folgendes zu diesem Code:</span><span class="sxs-lookup"><span data-stu-id="4daab-p106">Add the following lines to the file. Note the following about this code:</span></span>
    
      - <span data-ttu-id="4daab-139">Die Zeile  `'use strict';` sorgt dafür, dass dass die JavaScript-Laufzeit im Browser eine Ausnahme auslöst, wenn Sie versehentlich bestimmte ungültige Methoden in JavaScript verwenden.</span><span class="sxs-lookup"><span data-stu-id="4daab-139">The  `'use strict';` line ensures that the JavaScript runtime in the browser will throw an exception if you inadvertently use certain bad practices in the JavaScript.</span></span>
    
 
  - <span data-ttu-id="4daab-p107">Die Variable  `clientContext` enthält ein **SP.ClientContext**-Objekt, das auf die SharePoint-Website verweist. Jeder JSOM-Code beginnt mit dem Erstellen eines Objekts dieses Typs oder dem Abrufen eines Verweises auf ein solches Objekt.</span><span class="sxs-lookup"><span data-stu-id="4daab-p107">The  `clientContext` variable holds a **SP.ClientContext** object that references the SharePoint website. All JSOM code begins by creating, or getting a reference to, an object of this type.</span></span>
    
 
  - <span data-ttu-id="4daab-142">Die Variable  `employeeList` enthält einen Verweis auf die Listeninstanz **Neue Mitarbeiter in Seattle**.</span><span class="sxs-lookup"><span data-stu-id="4daab-142">The  `employeeList` variable holds a reference to the list instance **New Employees in Seattle**.</span></span>
    
 
  - <span data-ttu-id="4daab-143">Die Variable `completedItems` enthält die Elemente aus der Liste, die das Skript löscht: die Elemente, deren Feld **OrientationStage** auf **Abgeschlossen** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="4daab-143">The  `completedItems` variable holds the items from the list that the script will delete: the items whose **OrientationStage** field is set to **Completed**.</span></span>
    
 

```
  'use strict';

var clientContext = SP.ClientContext.get_current(); 
var employeeList = clientContext.get_web().get_lists().getByTitle('New Employees In Seattle'); 
var completedItems; 
```

5. <span data-ttu-id="4daab-p108">Um Nachrichten zwischen dem Clientbrowser und dem SharePoint-Server zu minimieren, verwendet JSOM ein Batchverarbeitungssystem. Nur eine Funktion, **SP.ClientContext.executeQueryAsync**, sendet tatsächlich Nachrichten an den Server (und empfängt Antworten). Aufrufe an die JSOM-APIs, die zwischen Aufrufen von **executeQueryAsync** stattfinden, werden gebündelt und in einem Batch beim nächsten Mal an den Server gesendet, wenn **executeQueryAsync** aufgerufen wird. Allerdings ist es in der Regel nicht möglich, eine Methode eines JSOM-Objekts aufzurufen, es sei denn, das Objekt wurde in einem vorherigen Aufruf von **executeQueryAsync** zum Client gebracht. Das Skript ruft die Methode **SP.ListItem.deleteObject** jedes abgeschlossenen Elements in der Liste auf, muss **executeQueryAsync** also zweimal aufrufen, einmal, um eine Auflistung von abgeschlossenen Listenelementen abzurufen, und ein zweites Mal, um die Aufrufe von **deleteObject** in einem Batch zusammenzufassen und zur Ausführung an den Server zu senden.</span><span class="sxs-lookup"><span data-stu-id="4daab-p108">To minimize messages between the client browser and the SharePoint server, the JSOM uses a batching system. Only one function,  **SP.ClientContext.executeQueryAsync**, actually sends messages to the server (and receives replies) . Calls to the JSOM APIs that come in between calls of  **executeQueryAsync** are bundled up and sent to the server in a batch the next time **executeQueryAsync** is called. However, it is not generally possible to call a method of a JSOM object unless the object has been brought down to the client in a previous call of **executeQueryAsync**. Your script is going to call the  **SP.ListItem.deleteObject** method of each completed item on the list, so it has to make two calls of **executeQueryAsync**; one to get a collection of the completed list items, and then a second to batch the calls of  **deleteObject** and send them to the server for execution.</span></span>
    
    <span data-ttu-id="4daab-p109">Beginnen Sie also damit, eine Methode zu erstellen, um die Listenelemente vom Server abzurufen. Fügen Sie den folgenden Code in die Datei ein.</span><span class="sxs-lookup"><span data-stu-id="4daab-p109">So, begin by creating a method to get the list items from the server. Add the following code to the file.</span></span> 
    


```
  function purgeCompletedItems() {

   var camlQuery = new SP.CamlQuery(); 
   camlQuery.set_viewXml( 
         '<View><Query><Where><Eq>' + 
           '<FieldRef Name=\'OrientationStage\'/><Value Type=\'Choice\'>Completed</Value>' + 
         '</Eq></Where></Query></View>'); 
     completedItems = employeeList.getItems(camlQuery); 
}
```

6. <span data-ttu-id="4daab-p110">Wenn diese Zeilen an den Server gesendet und dort ausgeführt werden, erstellen Sie eine Auflistung von Listenelementen, aber das Skript muss diese Auflistung zum Client bringen. Dies erfolgt durch einen Aufruf an die Funktion **SP.ClientContext.load**. Fügen Sie also die folgende Zeile am Ende der Methode zur Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="4daab-p110">When these lines are sent to server and executed there, they create a collection of list items, but the script must bring that collection down to the client. This is done with a call to the  **SP.ClientContext.load** function, so add the following line to the method to the end of the method.</span></span>
    
```
  clientContext.load(completedItems);
```

7. <span data-ttu-id="4daab-p111">Fügen Sie einen Aufruf von **executeQueryAsync** hinzu. Diese Methode hat zwei Parameter, die beide Rückruffunktionen sind. Die erste wird ausgeführt, wenn der Server erfolgreich alle Befehle im Batch ausführt. Die zweite wird ausgeführt, wenn auf dem Server aus irgendeinem Grund ein Fehler auftritt. Sie erstellen diese beiden Funktionen in späteren Schritten. Fügen Sie die folgende Zeile am Ende der Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="4daab-p111">Add a call of  **executeQueryAsync**. This method has two parameters, both of which are callback functions. The first runs if server successfully executes all the commands in the batch. The second runs if the server fails for any reason. You create these two functions in later steps. Add the following line to the end of the method.</span></span>
    
```
  clientContext.executeQueryAsync(deleteCompletedItems, onGetCompletedItemsFail);
```

8. <span data-ttu-id="4daab-p112">Schließlich fügen Sie die folgende Zeile am Ende der Methode hinzu. Durch Rückgabe von **false** an die ASP.NET-Schaltfläche, die die Funktion aufrufen wird, wird das Standardverhalten von ASP.NET-Schaltflächen abgebrochen, das im erneuten Laden der Seite besteht. Ein erneutes Laden der Seite würde ein erneutes Laden der Datei Add-in.js verursachen. Das würde wiederum das Objekt `clientContext` erneut initialisieren. Wenn dieses erneute Laden zwischen dem Zeitpunkt, an dem **executeQueryAsync** seine Anforderung sendet, und dem Zeitpunkt, an dem der SharePoint-Server die Antwort zurücksendet, abgeschlossen wird, ist das ursprüngliche `clientContext`-Objekt nicht mehr vorhanden, um die Antwort zu verarbeiten. Die Funktion würde angehalten werden, ohne dass die Erfolgs- oder Fehlerrückrufe ausgeführt wurden. (Das genaue Verhalten kann je nach Browser unterschiedlich sein.)</span><span class="sxs-lookup"><span data-stu-id="4daab-p112">Finally, add the following line to the end of the method. By returning  **false** to the ASP.NET button that will call the function, we cancel the default behavior of ASP.NET buttons, which is to reload the page. A reload of the page would cause a reload of the Add-in.js file. That, in turn, would reinitialize the `clientContext` object. If this reload completed between the time the **executeQueryAsync** sends its request and the time the SharePoint server sends back the response, then the original `clientContext` object is no longer in existence to process the response. The function would halt with neither the success nor the failure callbacks executed. (Exact behavior might vary depending on the browser.)</span></span>
    
```
  return false;
```

9. <span data-ttu-id="4daab-p113">Fügen Sie der Datei die folgende Funktion,  `deleteCompletedItems`, hinzu. Diese Funktion wird ausgeführt, wenn die Funktion  `purgeCompletedItems` erfolgreich ist. Beachten Sie Folgendes zu diesem Code:</span><span class="sxs-lookup"><span data-stu-id="4daab-p113">Add the following function,  `deleteCompletedItems`, to the file. This is the function that runs if the  `purgeCompletedItems` function is successful. Note the following about this code:</span></span>
    
      - <span data-ttu-id="4daab-p114">Die Methode **SP.ListItem.get_id** Methode gibt die ID des Listenelements zurück. Jedes Element im Array ist ein **SP.ListItem**-Objekt.</span><span class="sxs-lookup"><span data-stu-id="4daab-p114">The  **SP.ListItem.get_id** method returns the ID of the list item. Each item in the array is an **SP.ListItem** object.</span></span>
    
 
  - <span data-ttu-id="4daab-171">Die Methode **SP.List.getItemById** gibt das Objekt **SP.ListItem** mit der angegebenen ID zurück.</span><span class="sxs-lookup"><span data-stu-id="4daab-171">The  **SP.List.getItemById** method returns the **SP.ListItem** object with the specified ID.</span></span>
    
 
  - <span data-ttu-id="4daab-172">Die Methode **SP.ListItem.deleteObject** kennzeichnet das auf dem Server zu löschende Listenelement, wenn der Aufruf von **executeQueryAsync** vorgenommen wird.</span><span class="sxs-lookup"><span data-stu-id="4daab-172">The  **SP.ListItem.deleteObject** method marks the list item to be deleted on the server when the call of **executeQueryAsync** is made.</span></span>
    
 
  - <span data-ttu-id="4daab-p115">Die Listenelemente müssen aus der Auflistung kopiert werden, die vom Server zu einem Array gesendet wird, bevor sie gelöscht werden können. Wenn das Skript die Methode **deleteObject** für jedes Element direkt in der **while**-Schleife aufgerufen hat, löst JavaScript einen Fehler aus, dass die Länge der Auflistung geändert wird, während die Enumeration ausgeführt wird. Die Fehlermeldung ist nicht wirklich wahr, da das Element nicht wirklich gelöscht wird, bis die **deleteObject**-Aufrufe gebündelt und an den Server gesendet werden, aber JSOM ist darauf ausgelegt, um die Ausnahmeauslöser zu imitieren, die auf dem Server auftreten würden (auf dem Code eine Auflistungsgröße nicht ändern sollte, während eine Enumeration der Auflistung erfolgt). Arrays haben jedoch eine feste Größe, deshalb wird beim Aufrufen von **deleteObject** für ein Element in einem Array das Element aus der Liste gelöscht, aber die Größe des Arrays wird nicht geändert.</span><span class="sxs-lookup"><span data-stu-id="4daab-p115">The list items have to be copied from the collection that is sent down from the server to an array before they can be deleted. If the script called the  **deleteObject** method for each item directly in the **while** loop, the JavaScript would throw an error complaining that the length of the collection is being changed while the enumeration is underway. The error message isn't literally true, because the item isn't really deleted from anything until the **deleteObject** calls are bundled and sent to the server, but the JSOM is designed to mimic the exception throws that would occur on the server (where code should not change a collection size while the collection is being enumerated). However, arrays have a fixed size, so calling **deleteObject** on an item in an array deletes the item from the list, but does not change the size of the array.</span></span>
    
 

```
  function deleteCompletedItems() {

    var itemArray = new Array();
    var listItemEnumerator = completedItems.getEnumerator();

    while (listItemEnumerator.moveNext()) {
        var item = listItemEnumerator.get_current();
        itemArray.push(item);
    }

    var i;
    for (i = 0; i < itemArray.length; i++) {
        employeeList.getItemById(itemArray[i].get_id()).deleteObject();
    }

    clientContext.executeQueryAsync(onDeleteCompletedItemsSuccess, onDeleteCompletedItemsFail);
}
```

10. <span data-ttu-id="4daab-p116">Fügen Sie die folgende Funktion,  `onDeleteCompletedItemsSuccess`, zur Datei hinzu. Dies ist die Funktion, die ausgeführt wird, wenn die abgeschlossenen Elemente erfolgreich gelöscht werden (oder keine abgeschlossenen Elemente in der Liste vorhanden sind). Die zweite Zeile,  `location.reload(true);`, bewirkt, dass die Seite vom Server neu geladen wird. Dies erfolgt aus Gründen der Einfachheit, da das Listenansicht-Webpart auf der Seite weiterhin abgeschlossene Elemente angezeigt, bis die Seite aktualisiert wird. (Die Datei Add-in.js wird ebenfalls neu geladen, was aber kein Problem verursacht, da dies nicht in einer Weise erfolgt, die eine laufende JavaScript-Funktion unterbricht.)</span><span class="sxs-lookup"><span data-stu-id="4daab-p116">Add the following function,  `onDeleteCompletedItemsSuccess`, to the file. This is the function that runs if the completed items are successfully deleted (or there aren't any completed items on the list). The second line,  `location.reload(true);`, causes the page to reload from the server. This is a convenience because the list view Web Part on the page still shows the completed items until the page is refreshed. (The Add-in.js file is reloaded too, but that doesn't cause a problem because it won't do so in a way that interrupts an ongoing JavaScript function.</span></span>
    
```
  function onDeleteCompletedItemsSuccess() {
    alert('Completed orientations have been deleted.');
    location.reload(true);
}
```

11. <span data-ttu-id="4daab-182">Fügen Sie die folgenden zwei Rückruf-bei-Fehler-Funktionen zu der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="4daab-182">Add the following two callback-on-failure functions to the file.</span></span> 
    
```
  // Failure callbacks

function onGetCompletedItemsFail(sender, args) {
    alert('Unable to get completed items. Error:' + args.get_message() + '\n' + args.get_stackTrace());
}

function onDeleteCompletedItemsFail(sender, args) {
    alert('Unable to delete completed items. Error:' + args.get_message() + '\n' + args.get_stackTrace());
}
```

12. <span data-ttu-id="4daab-183">Öffnen Sie die Datei „default.aspx“, und suchen Sie nach dem **asp:Content**-Element mit der ID **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="4daab-183">Open the default.aspx file and find the  **asp:Content** element with the ID **PlaceHolderMain**.</span></span>
    
 
13. <span data-ttu-id="4daab-p117">Fügen Sie das folgende Markup zwischen dem Element **WebPartPages:WebPartZone** und dem ersten der zwei **asp:Hyperlink**-Elemente hinzu. Beachten Sie, dass der Wert des **OnClientClick**-Handlers  `return purgeCompletedItems()` statt nur `purgeCompletedItems()` ist. Der von der Funktion zurückgegebene Wert `false` weist ASP.NET an, die Seite nicht erneut zu laden.</span><span class="sxs-lookup"><span data-stu-id="4daab-p117">Add the following markup between the  **WebPartPages:WebPartZone** element and the first of the two **asp:Hyperlink** elements. Note that the value of the **OnClientClick** handler is `return purgeCompletedItems()` instead of just `purgeCompletedItems()`. The  `false` that is returned from the function tells ASP.NET not to reload the page.</span></span>
    
```HTML
  <p><asp:Button runat="server" OnClientClick="return purgeCompletedItems()" 
  ID="purgecompleteditemsbutton" Text="Purge Completed Items" /></p>
```

14. <span data-ttu-id="4daab-187">Erstellen Sie das Projekt in Visual Studio neu.</span><span class="sxs-lookup"><span data-stu-id="4daab-187">Rebuild the project in Visual Studio.</span></span>
    
 
15. <span data-ttu-id="4daab-188">Um die Notwendigkeit zu minimieren, die **Einführungsphase** von Listenelementen manuell auf „Abgeschlossen“ beim Testen des Add-Ins festzulegen zu müssen, öffnen Sie die Datei elements.xml für die Listeninstanz **NeueMitarbeiterInSeattle** (nicht die elements.xml für die Listenvorlage **EinführungNeuerMitarbeiter**), und fügen Sie das Markup  `<Field Name="OrientationStage">Completed</Field>` als letztes untergeordnetes Element zu einem oder mehreren der **Row**-Elemente hinzu.</span><span class="sxs-lookup"><span data-stu-id="4daab-188">To minimize the need to manually set the  **Orientation Stage** of list items toCompleted while testing the add-in, open the elements.xml file for the list instance **NewEmployeesInSeattle** (not the elements.xml for the list template **NewEmployeeOrientation**) and add the markup  `<Field Name="OrientationStage">Completed</Field>` as the last child to one or more of the **Row** elements.</span></span>
    
    <span data-ttu-id="4daab-189">Im Folgenden sehen Sie ein Beispiel, wie das Element **Rows** aussehen sollte.</span><span class="sxs-lookup"><span data-stu-id="4daab-189">The following is an example of how the  **Rows** element should look.</span></span>
    


```
  <Rows>
  <Row>
    <Field Name="Title">Tom Higginbotham</Field>
    <Field Name="Division">Manufacturing</Field>
    <Field Name="OrientationStage">Completed</Field>
  </Row>
  <Row>
    <Field Name="Title">Satomi Hayakawa</Field>
    <Field Name="OrientationStage">Completed</Field>
  </Row>
  <Row>
    <Field Name="Title">Cassi Hicks</Field>
  </Row>
  <Row>
    <Field Name="Title">Lertchai Treetawatchaiwong</Field>
  </Row>
</Rows>
```


## <a name="run-and-test-the-add-in"></a><span data-ttu-id="4daab-190">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="4daab-190">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="4daab-191">Aktivieren Sie Popups im Browser, den Visual Studio beim Debuggen verwendet.</span><span class="sxs-lookup"><span data-stu-id="4daab-191">Enable popups on the browser that Visual Studio uses when you debug.</span></span>
    
 
2. <span data-ttu-id="4daab-p118">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="4daab-p118">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
3. <span data-ttu-id="4daab-194">Die Startseite des Add-Ins wird geöffnet, und es gibt ein oder mehrere Elemente in der Liste, für die **Einführungsphase** auf **Abgeschlossen** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="4daab-194">The home page of the add-in opens and there are one or more items on the list with  **Orientation Stage** at **Completed**.</span></span> 
    
    <span data-ttu-id="4daab-195">**Liste vor dem Löschen abgeschlossener Elemente**</span><span class="sxs-lookup"><span data-stu-id="4daab-195">**List before purge of completed items**</span></span>

 

  ![Die Liste "Neue Mitarbeiter in Seattle", in der die Spalten "Orientierungsphase" für zwei Elemente auf "Abgeschlossen" festgelegt ist. Unter der Liste befindet sich eine Schaltfläche "Abgeschlossene Elemente löschen".](../images/e5e4eef8-a218-4797-aabc-c52adbd2d96d.PNG)
 

 

 
4. <span data-ttu-id="4daab-p120">Wenn die Startseite des Add-Ins vollständig geladen wurde, klicken Sie auf die Schaltlfäche **Abgeschlossene Elemente löschen**. Wenn der Vorgang erfolgreich ist (und Sie keine Fehlermeldung erhalten), werden alle **abgeschlossenen** Elemente gelöscht, und Sie sehen das Feld mit der Popupmeldung **Abgeschlossene Einführungen wurden gelöscht**.</span><span class="sxs-lookup"><span data-stu-id="4daab-p120">When the start page of the add-in has completely loaded, choose the  **Purge Completed Items** button. If the operation succeeds (you don't get any failure message), then all the **Complete** items are deleted and you'll see the popup message box saying **Completed orientations have been deleted**.</span></span> 
    
 
5. <span data-ttu-id="4daab-200">Schließen Sie das Popup. Die Seite wird erneut geladen und die **abgeschlossenen** Elemente sind nicht mehr im Listenansicht-Webpart vorhanden...</span><span class="sxs-lookup"><span data-stu-id="4daab-200">Close the popup and the page will reload and the  **Completed** items are no longer in the list view Web Part..</span></span>
    
    <span data-ttu-id="4daab-201">**Liste nach dem Löschen abgeschlossener Elemente**</span><span class="sxs-lookup"><span data-stu-id="4daab-201">**List after purge of completed items**</span></span>

 

  ![Die Liste "Neue Mitarbeiter in Seattle" mit zwei Elementen weniger als zuvor. Für keines ist "Orientierungsphase" auf "Abgeschlossen" festgelegt.](../images/a0330fad-1473-4fde-9df2-8be0b37df1a1.PNG)
 

 

 
6. <span data-ttu-id="4daab-p121">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="4daab-p121">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="4daab-p122">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewähr, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="4daab-p122">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="4daab-207"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="4daab-207"></span></span>

<span data-ttu-id="4daab-208">Im nächsten Artikel dieser Reihe fügen Sie JavaScript zu einer Seite im Add-In-Web hinzu, das mit SharePoint-Daten im Hostweb arbeitet:  [Arbeiten mit Hostwebdaten aus JavaScript im Add-In-Webpart](work-with-host-web-data-from-javascript-in-the-add-in-web.md).</span><span class="sxs-lookup"><span data-stu-id="4daab-208">In the next article in this series, you'll add JavaScript to a page on the add-in web that works with SharePoint data on the host web:  [Work with host web data from JavaScript in the add-in web](work-with-host-web-data-from-javascript-in-the-add-in-web.md).</span></span>
 

 

