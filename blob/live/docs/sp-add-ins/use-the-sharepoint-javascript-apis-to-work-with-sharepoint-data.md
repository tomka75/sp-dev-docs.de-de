---
title: Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten
description: "Hier erfahren Sie, wie Sie JavaScript-Code sowie eine Schaltfläche zum Aufrufen des Codes erstellen und Ihr Add-In ausführen und testen können."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 6f28049064cae8323be358b671df29deaeb287b4
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data"></a><span data-ttu-id="b213c-103">Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten</span><span class="sxs-lookup"><span data-stu-id="b213c-103">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>

<span data-ttu-id="b213c-104">Dieser Artikel ist der zehnte Artikel in unserer Artikelreihe zu den Grundlagen der Entwicklung von SharePoint-gehosteten SharePoint-Add-Ins. Vor der Lektüre dieses Artikels sollten Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) vertraut machen und die vorherigen Artikel der Reihe lesen:</span><span class="sxs-lookup"><span data-stu-id="b213c-104">This is the 11th in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="b213c-105">Erste Schritte zum Erstellen SharePoint-gehosteter SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b213c-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="b213c-106">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b213c-106">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-107">Hinzufügen von Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="b213c-107">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-108">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="b213c-108">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md) 
-  [<span data-ttu-id="b213c-109">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="b213c-109">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-110">Hinzufügen eines Workflows zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b213c-110">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-111">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b213c-111">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-112">Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint-gehostetes SharePoint Add-In</span><span class="sxs-lookup"><span data-stu-id="b213c-112">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="b213c-113">Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b213c-113">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
    
> [!NOTE]
> <span data-ttu-id="b213c-114">Wenn Sie unsere Artikelreihe zum Thema SharePoint-gehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können.</span><span class="sxs-lookup"><span data-stu-id="b213c-114">Note  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_SP-hosted_Add-Ins_Tutorials and open the BeforeClientRenderedControl.sln file.</span></span> <span data-ttu-id="b213c-115">Alternativ können Sie das Repository unter [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeJSOM.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="b213c-115">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeJSOM.sln file.</span></span>

<span data-ttu-id="b213c-116">SharePoint-gehostete SharePoint-Add-Ins dürfen keinen serverseitigen Code enthalten. Dennoch können Sie in SharePoint-gehosteten SharePoint-Add-Ins Geschäftslogik und Laufzeitinteraktionen mit SharePoint-Komponenten realisieren, und zwar mithilfe von JavaScript und der SharePoint-Bibliothek für das JavaScript-Clientobjektmodell.</span><span class="sxs-lookup"><span data-stu-id="b213c-116">Even though SharePoint-hosted SharePoint Add-ins cannot have server-side code, you can still have business logic and runtime interaction with SharePoint components in a SharePoint-hosted SharePoint Add-in by using JavaScript and the SharePoint JavaScript client object model library. (We'll call it JSOM. Note the "M" on the end. Don't confuse this with JSO N [JavaScript Object Notation].) In this article you use the JavaScript object model to find and remove old items from the New Employees in Seattle list.</span></span> <span data-ttu-id="b213c-117">Wir bezeichnen dieses Modell als JSOM.</span><span class="sxs-lookup"><span data-stu-id="b213c-117">We'll call it JSOM.</span></span> <span data-ttu-id="b213c-118">Entscheidend ist hier das „M“ am Ende:</span><span class="sxs-lookup"><span data-stu-id="b213c-118">Note the "M" on the end.</span></span> <span data-ttu-id="b213c-119">Das Konzept darf nicht verwechselt werden mit JSO**N** (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="b213c-119">Don't confuse this with JSO**N** (JavaScript Object Notation).</span></span> <span data-ttu-id="b213c-120">In diesem Artikel nutzen Sie das JavaScript-Objektmodell, um in der Liste **Neue Mitarbeiter in Seattle** alte Elemente zu finden und diese Elemente zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="b213c-120">In this article, you use the JavaScript object model to find and remove old items from the **New Employees in Seattle** list.</span></span>

## <a name="create-the-javascript-and-a-button-to-invoke-it"></a><span data-ttu-id="b213c-121">Erstellen des JavaScript-Codes sowie einer Schaltfläche zum Aufrufen des Codes</span><span class="sxs-lookup"><span data-stu-id="b213c-121">Create the JavaScript and a button to invoke it</span></span>

1. <span data-ttu-id="b213c-122">Führen Sie, sofern noch nicht geschehen, den folgenden Schritt aus dem ersten Tutorial dieser Artikelreihe durch:</span><span class="sxs-lookup"><span data-stu-id="b213c-122">Verify that the following step from the first tutorial in this series was completed:</span></span> 
    
   <span data-ttu-id="b213c-123">Öffnen Sie die Datei **/Pages/Default.aspx** im Stammverzeichnis des Projekts.</span><span class="sxs-lookup"><span data-stu-id="b213c-123">Open the file **/Pages/Default.aspx** from the root of the project.</span></span> <span data-ttu-id="b213c-124">Unter anderem lädt diese generierte Datei eines oder beide der zwei Skripts, die in SharePoint gehostet werden: „sp.runtime.js“ und „sp.js“.</span><span class="sxs-lookup"><span data-stu-id="b213c-124">Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js.</span></span> <span data-ttu-id="b213c-125">Das Markup zum Laden dieser Dateien befindet sich im Steuerelement des Typs **Content** mit der ID **PlaceHolderAdditionalPageHead** am Anfang der Datei.</span><span class="sxs-lookup"><span data-stu-id="b213c-125">The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**.</span></span> <span data-ttu-id="b213c-126">Dieses Markup unterscheidet sich je nach der verwendeten Version von **Microsoft Office Developer Tools für Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b213c-126">The markup varies depending on the version of **Microsoft Office Developer Tools for Visual Studio** that you are using.</span></span> 
   
   <span data-ttu-id="b213c-127">Für diese Tutorialreihe müssen beide Dateien geladen werden. Zudem müssen die Dateien mit herkömmlichen HTML-Tags des Typs **\<script\>** geladen werden statt mit Tags des Typs **\<SharePoint:ScriptLink\>**.</span><span class="sxs-lookup"><span data-stu-id="b213c-127">This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags.</span></span> <span data-ttu-id="b213c-128">Stellen Sie sicher, dass das Steuerelement **PlaceHolderAdditionalPageHead** die nachfolgenden Zeilen enthält, und zwar *direkt oberhalb* der Zeile `<meta name="WebPartPageExpansion" content="full" />`:</span><span class="sxs-lookup"><span data-stu-id="b213c-128">Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above* the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>

    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

   <span data-ttu-id="b213c-p105">Durchsuchen Sie anschließend die Datei nach einem anderen Markup, das auch eine oder die andere dieser Dateien lädt, und entfernen Sie das redundante Markup. Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="b213c-p105">Then search the file for any other markup that also loads one or the other of these files and remove the redundant markup. Save and close the file.</span></span>

2. <span data-ttu-id="b213c-131">Möglicherweise wird im Knoten **Skripts** im **Projektmappen-Explorer** bereits eine Datei „Add-in.js“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b213c-131">In the **Scripts** node in **Solution Explorer**, there may already be an Add-in.js file.</span></span> <span data-ttu-id="b213c-132">Falls dem nicht so ist, jedoch eine Datei „App.js“ angezeigt wird, müssen Sie mit der rechten Maustaste auf die Datei **App.js** klicken und sie in **Add-in.js** umbenennen.</span><span class="sxs-lookup"><span data-stu-id="b213c-132">If there isn't, but there is an App.js file, right-click **App.js** and rename it **Add-in.js**.</span></span> <span data-ttu-id="b213c-133">Falls weder eine Datei „Add-in.js“ noch eine Datei „App.js“ vorhanden ist, müssen Sie wie folgt eine Datei erstellen:</span><span class="sxs-lookup"><span data-stu-id="b213c-133">If there isn't an Add-in.js or App.js, create one with these steps:</span></span>
    
   1. <span data-ttu-id="b213c-134">Klicken Sie mit der rechten Maustaste auf den Knoten **Skripts**, und wählen Sie die Option **Hinzufügen** > **Neues Element** > **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="b213c-134">Right-click the  **Scripts** node and choose **Add** > **New Item** > **Web**.</span></span>
   2. <span data-ttu-id="b213c-135">Wählen Sie die Option **JavaScript-Datei** aus, und geben Sie der Datei den Namen **Add-in.js**.</span><span class="sxs-lookup"><span data-stu-id="b213c-135">Select **JavaScript File** and name it **Add-in.js**.</span></span>

3. <span data-ttu-id="b213c-136">Öffnen Sie die Datei „Add-in.js“, und löschen Sie gegebenenfalls vorhandene Dateiinhalte.</span><span class="sxs-lookup"><span data-stu-id="b213c-136">Open Add-in.js and delete its content, if there is any.</span></span>

4. <span data-ttu-id="b213c-137">Fügen Sie die folgenden Zeilen in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-137">Add the following lines to the top of the  file:</span></span> 

    ```
      'use strict';

     var clientContext = SP.ClientContext.get_current(); 
     var employeeList = clientContext.get_web().get_lists().getByTitle('New Employees In Seattle'); 
     var completedItems; 
    ```

   <span data-ttu-id="b213c-138">Zu diesem Code ist Folgendes anzumerken:</span><span class="sxs-lookup"><span data-stu-id="b213c-138">Note the following about this code:</span></span>
    
   - <span data-ttu-id="b213c-139">Die Zeile `'use strict';` sorgt dafür, dass die JavaScript-Laufzeit im Browser eine Ausnahme zurückgibt, wenn Sie versehentlich bestimmte unzulässige Methoden im JavaScript-Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="b213c-139">The  `'use strict';` line ensures that the JavaScript runtime in the browser will throw an exception if you inadvertently use certain bad practices in the JavaScript.</span></span>

   - <span data-ttu-id="b213c-p107">Die Variable `clientContext` enthält ein Objekt des Typs **SP.ClientContext**, das auf die SharePoint-Website verweist. Sämtlicher JSOM-Code erstellt zunächst ein Objekt dieses Typs oder ruft ein Objekt dieses Typs ab.</span><span class="sxs-lookup"><span data-stu-id="b213c-p107">The  `clientContext` variable holds a **SP.ClientContext** object that references the SharePoint website. All JSOM code begins by creating, or getting a reference to, an object of this type.</span></span>

   - <span data-ttu-id="b213c-142">Die Variable `employeeList` enthält einen Verweis auf die Listeninstanz **Neue Mitarbeiter in Seattle**.</span><span class="sxs-lookup"><span data-stu-id="b213c-142">The  `employeeList` variable holds a reference to the list instance **New Employees in Seattle**.</span></span>

   - <span data-ttu-id="b213c-143">Die Variable `completedItems` enthält die Listenelemente, die das Skript löschen wird, d. h. die Elemente, für die das Feld **OrientationStage** auf **Abgeschlossen** gesetzt ist.</span><span class="sxs-lookup"><span data-stu-id="b213c-143">The  `completedItems` variable holds the items from the list that the script will delete: the items whose **OrientationStage** field is set to **Completed**.</span></span>

5. <span data-ttu-id="b213c-144">Das JSOM nutzt ein Batchsystem, um die Anzahl der zwischen dem Clientbrowser und dem SharePoint-Server versendeten Nachrichten möglichst gering zu halten.</span><span class="sxs-lookup"><span data-stu-id="b213c-144">To minimize messages between the client browser and the SharePoint server, the JSOM uses a batching system.</span></span> <span data-ttu-id="b213c-145">Tatsächlich sendet nur eine einzige Funktion Nachrichten an den Server (und erhält Antworten): **SP.ClientContext.executeQueryAsync**.</span><span class="sxs-lookup"><span data-stu-id="b213c-145">Only one function, **SP.ClientContext.executeQueryAsync**, actually sends messages to the server (and receives replies).</span></span> 

   <span data-ttu-id="b213c-146">Aufrufe an die JSOM-APIs, die zwischen Aufrufen von **executeQueryAsync** erfolgen, werden gebündelt und beim nächsten Aufrufen von **executeQueryAsync** als Batch an den Server gesendet.</span><span class="sxs-lookup"><span data-stu-id="b213c-146">Calls to the JSOM APIs that come in between calls of **executeQueryAsync** are bundled up and sent to the server in a batch the next time **executeQueryAsync** is called.</span></span> <span data-ttu-id="b213c-147">Es ist jedoch nicht generell möglich, eine Methode eines JSOM-Objekts aufzurufen, es sei denn, das betreffende Objekt wurde in einem vorherigen Aufruf von **executeQueryAsync** an den Client gesendet.</span><span class="sxs-lookup"><span data-stu-id="b213c-147">However, it is not generally possible to call a method of a JSOM object unless the object has been brought down to the client in a previous call of **executeQueryAsync**.</span></span> 
   
   <span data-ttu-id="b213c-148">Ihr Skript wird die Methode **SP.ListItem.deleteObject** für jedes abgeschlossene Element in der Liste aufrufen. Das bedeutet, es muss zwei Aufrufe von **executeQueryAsync** senden: einen Aufruf zum Abrufen einer Sammlung der abgeschlossenen Listenelemente und einen Aufruf, um die Aufrufe von **deleteObject** in einem Batch zu bündeln und diesen Batch zur Ausführung an den Server zu senden.</span><span class="sxs-lookup"><span data-stu-id="b213c-148">Your script is going to call the **SP.ListItem.deleteObject** method of each completed item on the list, so it has to make two calls of **executeQueryAsync**; one to get a collection of the completed list items, and then a second to batch the calls of **deleteObject** and send them to the server for execution.</span></span>
    
   <span data-ttu-id="b213c-149">Zunächst erstellen Sie eine Methode zum Abrufen der Listenelemente vom Server.</span><span class="sxs-lookup"><span data-stu-id="b213c-149">So, begin by creating a method to get the list items from the server. Add the following code to the file.</span></span> <span data-ttu-id="b213c-150">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-150">Add the following code to the UIStrings.js file.</span></span> 

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

6. <span data-ttu-id="b213c-151">Sobald diese Zeilen an den Server gesendet und dort ausgeführt werden, wird eine Sammlung von Listenelementen erstellt. Das Skript muss diese Sammlung jedoch noch an den Client senden.</span><span class="sxs-lookup"><span data-stu-id="b213c-151">When these lines are sent to server and executed there, they create a collection of list items, but the script must bring that collection down to the client. This is done with a call to the  SP.ClientContext.load function, so add the following line to the method to the end of the method.</span></span> <span data-ttu-id="b213c-152">Dazu muss die Funktion **SP.ClientContext.load** aufgerufen werden. Fügen Sie also die folgende Zeile am Ende der Methode ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-152">When these lines are sent to server and executed there, they create a collection of list items, but the script must bring that collection down to the client. This is done with a call to the  **SP.ClientContext.load** function, so add the following line to the method to the end of the method.</span></span>
    
    ```
      clientContext.load(completedItems);
    ```

7. <span data-ttu-id="b213c-153">Fügen Sie einen Aufruf von **executeQueryAsync** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b213c-153">Add a call of **executeQueryAsync**.</span></span> <span data-ttu-id="b213c-154">Diese Methode hat zwei Parameter; bei beiden handelt es sich um Rückruffunktionen.</span><span class="sxs-lookup"><span data-stu-id="b213c-154">This method has two parameters, both of which are callback functions.</span></span> <span data-ttu-id="b213c-155">Die erste wird ausgeführt, wenn der Server alle Befehle im Batch erfolgreich ausgeführt hat.</span><span class="sxs-lookup"><span data-stu-id="b213c-155">The first runs if the server successfully executes all the commands in the batch.</span></span> <span data-ttu-id="b213c-156">Die zweite wird ausgeführt, wenn die Ausführung auf dem Server aus irgendeinem Grund fehlschlägt.</span><span class="sxs-lookup"><span data-stu-id="b213c-156">The second runs if the server fails for any reason.</span></span> <span data-ttu-id="b213c-157">Sie erstellen diese beiden Funktionen weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="b213c-157">You create these two functions in later steps.</span></span> <span data-ttu-id="b213c-158">Fügen Sie zunächst die folgende Zeile am Ende der Methode ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-158">Add the following line to the body of the  method. You create the  method in a later step.</span></span>
    
    ```
      clientContext.executeQueryAsync(deleteCompletedItems, onGetCompletedItemsFail);
    ```

8. <span data-ttu-id="b213c-159">Fügen Sie nun noch die folgende Zeile am Ende der Methode ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-159">Finally, add the following lines to the end of the macro.</span></span> 

    ```
      return false;
    ```

   <span data-ttu-id="b213c-160">Durch Zurückgeben von **false** an die ASP.NET-Schaltfläche, von der die Funktion aufgerufen wird, wird das Standardverhalten von ASP.NET-Schaltflächen abgebrochen: das Neuladen der Seite.</span><span class="sxs-lookup"><span data-stu-id="b213c-160">By returning **false** to the ASP.NET button that will call the function, we cancel the default behavior of ASP.NET buttons, which is to reload the page.</span></span> <span data-ttu-id="b213c-161">Bei einem Neuladen der Seite würde auch die Datei „Add-in.js“ neu geladen werden.</span><span class="sxs-lookup"><span data-stu-id="b213c-161">A reload of the page would cause a reload of the Add-in.js file.</span></span> <span data-ttu-id="b213c-162">Dadurch wiederum würde das Objekt des Typs `clientContext` reinitialisiert werden.</span><span class="sxs-lookup"><span data-stu-id="b213c-162">That, in turn, would reinitialize the `clientContext` object.</span></span> 
   
   <span data-ttu-id="b213c-163">Wenn nun ein solches Neuladen zwischen dem Senden einer Anforderung durch **executeQueryAsync** und dem Senden der Antwort durch den SharePoint-Server abgeschlossen würde, würde das ursprüngliche Objekt des Typs `clientContext` nicht mehr existieren und könnte folglich die Antwort nicht mehr verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="b213c-163">If this reload completed between the time the **executeQueryAsync** sends its request and the time the SharePoint server sends back the response, the original `clientContext` object is no longer in existence to process the response.</span></span> <span data-ttu-id="b213c-164">Die Funktion würde stoppen, und es würde weder der Erfolg-Rückruf noch der Fehler-Rückruf ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b213c-164">The function would halt with neither the success nor the failure callbacks executed.</span></span> <span data-ttu-id="b213c-165">(Das genaue Verhalten kann je nach Browser variieren.)</span><span class="sxs-lookup"><span data-stu-id="b213c-165">(Exact behavior might vary depending on the browser.)</span></span>

9. <span data-ttu-id="b213c-166">Fügen Sie die nachfolgend aufgeführte Funktion (`deleteCompletedItems`) in die Datei ein.</span><span class="sxs-lookup"><span data-stu-id="b213c-166">Add the following function to the file just below the `deleteCompletedItems` function.</span></span> <span data-ttu-id="b213c-167">Diese Funktion wird ausgeführt, wenn die Funktion `purgeCompletedItems` erfolgreich ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="b213c-167">Add the following function,  , to the file. This is the function that runs if the  `purgeCompletedItems` function is successful. Note the following about this code:</span></span> <span data-ttu-id="b213c-168">Zu diesem Code ist Folgendes anzumerken:</span><span class="sxs-lookup"><span data-stu-id="b213c-168">Note the following about this code:</span></span>
    
   - <span data-ttu-id="b213c-p116">Die Methode **SP.ListItem.get_id** gibt die ID des Listenelements zurück. Jedes Element im Array ist ein Objekt des Typs **SP.ListItem**.</span><span class="sxs-lookup"><span data-stu-id="b213c-p116">The **SP.ListItem.get_id** method returns the ID of the list item. Each item in the array is an **SP.ListItem** object.</span></span>

   - <span data-ttu-id="b213c-171">Die Methode **SP.List.getItemById** gibt das Objekt **SP.ListItem** mit der angegebenen ID zurück.</span><span class="sxs-lookup"><span data-stu-id="b213c-171">The **SP.List.getItemById** method returns the **SP.ListItem** object with the specified ID.</span></span>

   - <span data-ttu-id="b213c-172">Die Methode **SP.ListItem.deleteObject** kennzeichnet bei einem Aufruf von **executeQueryAsync** das Listenelement, das vom Server gelöscht werden soll.</span><span class="sxs-lookup"><span data-stu-id="b213c-172">The **SP.ListItem.deleteObject** method marks the list item to be deleted on the server when the call of **executeQueryAsync** is made.</span></span>

   <span data-ttu-id="b213c-173">Die Listenelemente müssen aus der vom Server gesendeten Sammlung in ein Array kopiert werden, bevor sie gelöscht werden können.</span><span class="sxs-lookup"><span data-stu-id="b213c-173">The list items have to be copied from the collection that is sent down from the server to an array before they can be deleted.</span></span> <span data-ttu-id="b213c-174">Würde das Skript die Methode **deleteObject** für jedes Element direkt in der **while**-Schleife aufrufen, würde der JavaScript-Code einen Fehler zurückgeben und melden, dass die Länge der Sammlung noch während der Enumeration geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="b213c-174">If the script called the **deleteObject** method for each item directly in the **while** loop, the JavaScript would throw an error complaining that the length of the collection is being changed while the enumeration is underway.</span></span> 
   
   <span data-ttu-id="b213c-175">Eine solche Fehlermeldung ist faktisch nicht korrekt, da das Element erst gelöscht wird, nachdem die Aufrufe der Methode **deleteObject** gebündelt und an den Server gesendet wurden; das JSOM ist jedoch so angelegt, dass es genau die Ausnahmen zurückgibt, die auf dem Server zurückgegeben würden (wo Code die Größe einer Sammlung nicht ändern darf, solange die Sammlung noch enumeriert wird).</span><span class="sxs-lookup"><span data-stu-id="b213c-175">The error message isn't literally true, because the item isn't really deleted from anything until the **deleteObject** calls are bundled and sent to the server, but the JSOM is designed to mimic the exception throws that would occur on the server (where code should not change a collection size while the collection is being enumerated).</span></span> <span data-ttu-id="b213c-176">Arrays allerdings haben eine feste Größe: Ein Aufruf von **deleteObject** für ein Element in einem Array löscht das Element aus der Liste, ändert jedoch nicht die Größe des Arrays.</span><span class="sxs-lookup"><span data-stu-id="b213c-176">However, arrays have a fixed size, so calling **deleteObject** on an item in an array deletes the item from the list, but does not change the size of the array.</span></span>

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

10. <span data-ttu-id="b213c-177">Fügen Sie die unten aufgeführte Funktion (`onDeleteCompletedItemsSuccess`) in die Datei ein.</span><span class="sxs-lookup"><span data-stu-id="b213c-177">Add the following function to the file just below the `onDeleteCompletedItemsSuccess` function.</span></span> <span data-ttu-id="b213c-178">Diese Funktion wird ausgeführt, wenn die abgeschlossenen Elemente erfolgreich gelöscht wurden (oder wenn in der Liste keine abgeschlossenen Elemente existieren).</span><span class="sxs-lookup"><span data-stu-id="b213c-178">This is the function that runs if the completed items are successfully deleted (or there aren't any completed items on the list).</span></span> 

   <span data-ttu-id="b213c-179">Die Zeile `location.reload(true);` bewirkt, dass die Seite vom Server neu geladen wird.</span><span class="sxs-lookup"><span data-stu-id="b213c-179">The line `location.reload(true);` causes the page to reload from the server.</span></span> <span data-ttu-id="b213c-180">Das wird aus Komfortgründen implementiert, da das Listenansicht-Webpart auf der Seite die abgeschlossenen Elemente solange anzeigt, bis die Seite aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="b213c-180">This is a convenience because the list view Web Part on the page still shows the completed items until the page is refreshed.</span></span> <span data-ttu-id="b213c-181">Auch die Datei „Add-in.js“ wird durch diese Zeile neu geladen. Das führt hier jedoch nicht zu Problemen, da das Neuladen der Datei keine aktiv ausgeführten JavaScript-Funktionen stört.</span><span class="sxs-lookup"><span data-stu-id="b213c-181">The Add-in.js file is reloaded too, but that doesn't cause a problem because it won't do so in a way that interrupts an ongoing JavaScript function.</span></span>
    
    ```
      function onDeleteCompletedItemsSuccess() {
        alert('Completed orientations have been deleted.');
        location.reload(true);
    }
    ```

11. <span data-ttu-id="b213c-182">Fügen Sie die folgenden beiden bei Fehlern auszuführenden Rückruffunktionen in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b213c-182">Add the following two callback-on-failure functions to the file.</span></span> 
    
    ```
      // Failure callbacks

    function onGetCompletedItemsFail(sender, args) {
        alert('Unable to get completed items. Error:' + args.get_message() + '\n' + args.get_stackTrace());
    }

    function onDeleteCompletedItemsFail(sender, args) {
        alert('Unable to delete completed items. Error:' + args.get_message() + '\n' + args.get_stackTrace());
    }
    ```

12. <span data-ttu-id="b213c-183">Öffnen Sie die Datei „default.aspx“, und suchen Sie nach dem Element des Typs **asp:Content** mit der ID **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="b213c-183">Open the default.aspx file and find the **asp:Content** element with the ID **PlaceHolderMain**.</span></span>

13. <span data-ttu-id="b213c-184">Fügen Sie das folgende Markup zwischen dem Element **WebPartPages:WebPartZone** und dem ersten der beiden Elemente des Typs **asp:Hyperlink** ein.</span><span class="sxs-lookup"><span data-stu-id="b213c-184">Add the following markup between the **WebPartPages:WebPartZone** element and the first of the two **asp:Hyperlink** elements.</span></span> <span data-ttu-id="b213c-185">Wie Sie sehen, hat der Handler **OnClientClick** den Wert `return purgeCompletedItems()` statt nur den Wert `purgeCompletedItems()`.</span><span class="sxs-lookup"><span data-stu-id="b213c-185">Note that the value of the **OnClientClick** handler is `return purgeCompletedItems()` instead of just `purgeCompletedItems()`.</span></span> <span data-ttu-id="b213c-186">Die von der Funktion zurückgegebene Antwort `false` ist für ASP.NET das Signal, dass die Seite nicht neu geladen werden soll.</span><span class="sxs-lookup"><span data-stu-id="b213c-186">The `false` that is returned from the function tells ASP.NET not to reload the page.</span></span>
    
    ```HTML
      <p><asp:Button runat="server" OnClientClick="return purgeCompletedItems()" 
      ID="purgecompleteditemsbutton" Text="Purge Completed Items" /></p>
    ```

14. <span data-ttu-id="b213c-187">Erstellen Sie das Projekt in Visual Studio neu.</span><span class="sxs-lookup"><span data-stu-id="b213c-187">Rebuild the project in Visual Studio.</span></span>

15. <span data-ttu-id="b213c-188">Während Tests des Add-Ins soll es möglichst selten nötig sein, die **Orientierungsphase** von Listenelementen manuell auf **Abgeschlossen** zu setzen. Öffnen Sie die Datei „elements.xml“ der Listeninstanz **NewEmployeesInSeattle** (nicht die Datei „elements.xml“ der Listenvorlage **NewEmployeeOrientation**), und fügen Sie das Markup `<Field Name="OrientationStage">Completed</Field>` als letztes untergeordnetes Element zu einem oder mehreren der Elemente des Typs **Row** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b213c-188">To minimize the need to manually set the **Orientation Stage** of list items toCompleted while testing the add-in, open the elements.xml file for the list instance **NewEmployeesInSeattle** (not the elements.xml for the list template **NewEmployeeOrientation**) and add the markup  `<Field Name="OrientationStage">Completed</Field>` as the last child to one or more of the **Row** elements.</span></span>
    
   <span data-ttu-id="b213c-189">Das Beispiel unten veranschaulicht, wie das Element **Rows** aussehen sollte:</span><span class="sxs-lookup"><span data-stu-id="b213c-189">The following is an example of how the **Rows** element should look.</span></span>

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


## <a name="run-and-test-the-add-in"></a><span data-ttu-id="b213c-190">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b213c-190">Run and test the add-in</span></span>

1. <span data-ttu-id="b213c-191">Aktivieren Sie Popupfenster in dem Browser, den Visual Studio während des Debuggens verwendet.</span><span class="sxs-lookup"><span data-stu-id="b213c-191">Enable popups on the browser that Visual Studio uses when you debug.</span></span>

2. <span data-ttu-id="b213c-p122">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="b213c-p122">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 

3. <span data-ttu-id="b213c-194">Die Startseite des Add-Ins wird geöffnet. In der Liste werden ein oder mehrere Elemente aufgeführt, für die unter **Orientierungsphase** der Wert **Abgeschlossen** eingetragen ist.</span><span class="sxs-lookup"><span data-stu-id="b213c-194">The home page of the add-in opens and there are one or more items on the list with  **Orientation Stage** at **Completed**.</span></span> 
    
   <span data-ttu-id="b213c-195">*Abbildung 1: Liste vor dem Löschen der abgeschlossenen Elemente*</span><span class="sxs-lookup"><span data-stu-id="b213c-195">*List before purge of completed items*</span></span>

   ![Die Liste "Neue Mitarbeiter in Seattle", in der die Spalten "Orientierungsphase" für zwei Elemente auf "Abgeschlossen" festgelegt ist. Unter der Liste befindet sich eine Schaltfläche "Abgeschlossene Elemente löschen".](../images/e5e4eef8-a218-4797-aabc-c52adbd2d96d.PNG)

4. <span data-ttu-id="b213c-198">Warten Sie, bis die Startseite des Add-Ins vollständig geladen wurde. Klicken Sie dann auf die Schaltfläche **Erledigte Elemente dauerhaft löschen**.</span><span class="sxs-lookup"><span data-stu-id="b213c-198">When the start page of the add-in has completely loaded, select the **Purge Completed Items** button.</span></span> <span data-ttu-id="b213c-199">Wird der Vorgang erfolgreich (d. h. ohne Fehlermeldung) ausgeführt, werden alle als **Abgeschlossen** gekennzeichneten Elemente gelöscht, und es wird ein Popupfenster mit der Meldung **Abgeschlossene Einführungen wurden gelöscht** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b213c-199">If the operation succeeds (you don't get any failure message), all the **Completed** items are deleted and you'll see a pop-up window that says **Completed orientations have been deleted**.</span></span> 

5. <span data-ttu-id="b213c-200">Schließen Sie das Popupfenster.</span><span class="sxs-lookup"><span data-stu-id="b213c-200">Close the pop-up window.</span></span> <span data-ttu-id="b213c-201">Die Seite wird neu geladen, und die als **Abgeschlossen** gekennzeichneten Elemente werden nicht mehr im Listenansicht-Webpart aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="b213c-201">Close the popup and the page will reload and the  **Completed** items are no longer in the list view Web Part..</span></span>
    
   <span data-ttu-id="b213c-202">*Abbildung 2: Liste nach dem Löschen der abgeschlossenen Elemente*</span><span class="sxs-lookup"><span data-stu-id="b213c-202">*List after purge of completed items*</span></span>

   ![Die Liste „Neue Mitarbeiter in Seattle“ mit zwei Elementen weniger als zuvor. Für keines ist „Orientierungsphase“ auf „Abgeschlossen“ gesetzt.](../images/a0330fad-1473-4fde-9df2-8be0b37df1a1.PNG)

6. <span data-ttu-id="b213c-204">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b213c-204">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="b213c-205">Wann immer Sie F5 drücken, zieht Visual Studio die bisherige Version des Add-Ins zurück und installiert die jeweils neueste Version.</span><span class="sxs-lookup"><span data-stu-id="b213c-205">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

7. <span data-ttu-id="b213c-206">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung auch in anderen Artikeln arbeiten werden, empfiehlt es sich, das Add-In ein letztes Mal zurückzuziehen, sobald Sie eine Weile nicht mehr an ihm arbeiten werden.</span><span class="sxs-lookup"><span data-stu-id="b213c-206">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="b213c-207">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="b213c-207">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b213c-208">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b213c-208">Next steps</span></span>
<span data-ttu-id="b213c-209"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="b213c-209"></span></span>

<span data-ttu-id="b213c-210">Im nächsten Artikel dieser Reihe fügen Sie JavaScript-Code zu einer Seite im Add-In-Web hinzu, die mit SharePoint-Daten im Hostweb arbeitet: [Arbeiten mit Hostwebdaten aus JavaScript im Add-In-Web](work-with-host-web-data-from-javascript-in-the-add-in-web.md).</span><span class="sxs-lookup"><span data-stu-id="b213c-210">In the next article in this series, you'll add JavaScript to a page on the add-in web that works with SharePoint data on the host web:  [Work with host web data from JavaScript in the add-in web](work-with-host-web-data-from-javascript-in-the-add-in-web.md).</span></span>
 

 

