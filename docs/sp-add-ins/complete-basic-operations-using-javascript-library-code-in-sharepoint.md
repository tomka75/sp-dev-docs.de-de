---
title: "Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 555ff88386166d381d7ff4c6f3d56f30e5a645e1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="complete-basic-operations-using-javascript-library-code-in-sharepoint"></a><span data-ttu-id="c9d78-102">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9d78-102">Complete basic operations using JavaScript library code in SharePoint</span></span>
<span data-ttu-id="c9d78-103">In diesem Artikel erfahren Sie, wie Sie Code zum Ausführen grundlegender Vorgänge unter Verwendung des JavaScript-Clientobjektmodells in SharePoint schreiben.</span><span class="sxs-lookup"><span data-stu-id="c9d78-103">Learn how to write code to perform basic operations using the JavaScript client object model in SharePoint.</span></span>
 

 <span data-ttu-id="c9d78-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c9d78-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="c9d78-107">**Hinweis** Ein Beispiel-SharePoint-Add-In mit der Komplexität von „Hello World“, das die JavaScript-Bibliothek verwendet, finden Sie unter [Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span><span class="sxs-lookup"><span data-stu-id="c9d78-107">**Note**  For a "Hello World" level sample SharePoint Add-in that uses the JavaScript library, see  [Use the SharePoint JavaScript APIs to work with SharePoint data](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span></span>
 


## <a name="sharepoint-client-apis"></a><span data-ttu-id="c9d78-108">SharePoint-Client-APIs</span><span class="sxs-lookup"><span data-stu-id="c9d78-108">SharePoint client APIs</span></span>
<span data-ttu-id="c9d78-109"><a name="ClientAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-109"></span></span>

<span data-ttu-id="c9d78-p102">Sie können das SharePoint-Clientobjektmodell zum Abrufen, Aktualisieren und Verwalten von Daten in SharePoint verwenden. SharePoint macht das Objektmodell in verschiedener Form verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p102">You can use the SharePoint client object model to retrieve, update, and manage data in SharePoint. SharePoint makes the object model available in several forms.</span></span>
 

 

- <span data-ttu-id="c9d78-112">Weitervertreibbare Assemblys für .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c9d78-112">.NET Framework redistributable assemblies</span></span>
    
 
- <span data-ttu-id="c9d78-113">JavaScript-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-113">JavaScript library</span></span>
    
 
- <span data-ttu-id="c9d78-114">REST-/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="c9d78-114">REST/OData endpoints</span></span>
    
 
- <span data-ttu-id="c9d78-115">Windows Phone-Assemblys</span><span class="sxs-lookup"><span data-stu-id="c9d78-115">Windows Phone assemblies</span></span>
    
 
- <span data-ttu-id="c9d78-116">Weitervertreibbare Silverlight-Assemblys</span><span class="sxs-lookup"><span data-stu-id="c9d78-116">Silverlight redistributable assemblies</span></span>
    
 
<span data-ttu-id="c9d78-117">Weitere Information zu den Gruppen von APIs, die für SharePoint verfügbar sind, finden Sie unter [Auswählen des richtigen API-Satzes in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9d78-117">For more information about the sets of APIs that are available for SharePoint, see  [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span> 
 

 
<span data-ttu-id="c9d78-p103">In diesem Artikel wird erklärt, wie Sie mithilfe des JavaScript-Objektmodells grundlegende Aufgaben ausführen. Sie können mit den HTML-<script>-Tags einen Verweis auf das Objektmodell hinzufügen. Informationen zur Verwendung anderer Client-APIs finden Sie unter folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="c9d78-p103">This article shows how to perform basic operations using the JavaScript object model. You can add a reference to the object model using HTML <script> tags. For information about how to use the other client APIs, see the following:</span></span>
 

 

-  [<span data-ttu-id="c9d78-121">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="c9d78-121">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [<span data-ttu-id="c9d78-122">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="c9d78-122">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="c9d78-123">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="c9d78-123">Build Windows Phone apps that access SharePoint</span></span>](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="c9d78-124">Verwenden des Silverlight-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="c9d78-124">Using the Silverlight Object Model</span></span>](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx)
    
 

## <a name="perform-basic-tasks-in-sharepoint-using-the-javascript-client-object-model"></a><span data-ttu-id="c9d78-125">Ausführen grundlegender Aufgaben in SharePoint unter Verwendung des JavaScript-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="c9d78-125">Perform basic tasks in SharePoint using the JavaScript client object model</span></span>
<span data-ttu-id="c9d78-126"><a name="BasicOps_SPJSOMOps"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-126"></span></span>

<span data-ttu-id="c9d78-127">In den folgenden Abschnitten werden Aufgaben beschrieben, die Sie programmgesteuert ausführen können. Diese Abschnitte enthalten JavaScript-Codebeispiele zur Veranschaulichung der Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="c9d78-127">The following sections describe tasks that you can complete programmatically, and they include JavaScript code examples that demonstrate the operations.</span></span>
 

 
<span data-ttu-id="c9d78-p104">Beim Erstellen eines in der Cloud gehosteten Add-Ins können Sie dem Objektmodell mithilfe der HTML-<script>-Tags einen Verweis hinzufügen. Es wird empfohlen, einen Verweis auf das Hostweb einzufügen, da das Add-In-Web möglicherweise nicht in allen Szenarien von in der Cloud gehosteten Add-Ins verfügbar ist. Sie können die URL des Hostwebs aus dem  _SPHostUrl_-Abfragezeichenfolgenparameter abrufen, wenn Sie das Token **{StandardTokens}** verwenden. Zudem können Sie den benutzerdefinierten Abfragezeichenfolgenparameter verwenden, wenn Sie das **{HostUrl}**-Token verwenden. Nachdem Sie die URL des Hostwebs ermittelt haben, müssen Sie den Verweis auf das Objektmodell mit JavaScript-Code dynamisch erstellen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p104">When you create a cloud-hosted add-in, you can add a reference to the object model by using HTML <script> tags. We recommend that you reference the host web because the add-in web may not exist in every scenario in cloud-hosted add-ins. You can retrieve the host web URL from the  _SPHostUrl_ query string parameter if you are using the **{StandardTokens}** token. You can also use your custom defined query string parameter if you are using the **{HostUrl}** token. After you have the host web URL, you must use JavaScript code to dynamically create the reference to the object model.</span></span>
 

 
<span data-ttu-id="c9d78-132">Im folgenden Codebeispiel werden die folgenden Aufgaben ausgeführt, um einen Verweis auf das JavaScript-Objektmodell hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="c9d78-132">The following code example performs these tasks to add a reference to the JavaScript object model:</span></span>
 

 

- <span data-ttu-id="c9d78-133">Es wird auf die AJAX-Bibliothek aus dem Microsoft Netzwerk für die Inhaltsübermittlung (CDN) verwiesen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-133">References the AJAX library from the Microsoft Content Delivery Network (CDN).</span></span>
    
 
- <span data-ttu-id="c9d78-134">Es wird auf die jQuery-Bibliothek aus dem Microsoft CDN verwiesen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-134">References the jQuery library from the Microsoft CDN.</span></span>
    
 
- <span data-ttu-id="c9d78-135">Die URL des Hostwebs wird aus der Abfragezeichenfolge extrahiert.</span><span class="sxs-lookup"><span data-stu-id="c9d78-135">Extracts the host web URL from the query string.</span></span>
    
 
- <span data-ttu-id="c9d78-p105">Die Dateien „SP.Runtime.js“ und „SP.js“ werden mithilfe der **getScript**-Funktion in jQuery geladen. Nachdem die Dateien geladen wurden, hat das Programm Zugriff auf das JavaScript-Objektmodell für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p105">Loads the SP.Runtime.js and SP.js files by using the  **getScript** function in jQuery. After loading the files, your program has access to the JavaScript object model for SharePoint.</span></span>
    
 
- <span data-ttu-id="c9d78-138">Der Programmablauf wird in der **execOperation**-Funktion fortgesetzt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-138">Continues the flow in the  **execOperation** function.</span></span>
    
 



```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script
    type="text/javascript"
    src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
</script>
<script type="text/javascript">
    var hostweburl;

    // Load the required SharePoint libraries.
    $(document).ready(function () {

        // Get the URI decoded URLs.
        hostweburl =
            decodeURIComponent(
                getQueryStringParameter("SPHostUrl")
        );

        // The js files are in a URL in the form:
        // web_url/_layouts/15/resource_file
        var scriptbase = hostweburl + "/_layouts/15/";

        // Load the js files and continue to
        // the execOperation function.
        $.getScript(scriptbase + "SP.Runtime.js",
            function () {
                $.getScript(scriptbase + "SP.js", execOperation);
            }
        );
    });

    // Function to execute basic operations.
    function execOperation() {

        // Continue your program flow here.

    }

    // Function to retrieve a query string value.
    // For production purposes you may want to use
    // a library to handle the query string.
    function getQueryStringParameter(paramToRetrieve) {
        var params =
            document.URL.split("?")[1].split("&amp;");
        var strParams = "";
        for (var i = 0; i < params.length; i = i + 1) {
            var singleParam = params[i].split("=");
            if (singleParam[0] == paramToRetrieve)
                return singleParam[1];
        }
    }
</script>

```

<span data-ttu-id="c9d78-p106">Beim Erstellen eines in SharePoint gehosteten Add-Ins können Sie mithilfe der HTML-Tags <script> einen Verweis auf das Objektmodell hinzufügen. Mithilfe des Add-In-Webs in einem von SharePoint gehosteten Add-In können Sie relative Pfade verwenden, um auf die erforderlichen Dateien zur Verwendung des JavaScript-Objektmodells zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p106">When you create a SharePoint-hosted add-in, you can add a reference to the object model by using HTML <script> tags. The add-in web in a SharePoint-hosted add-in allows you to use relative paths to reference the required files to use the JavaScript object model.</span></span>
 

 
<span data-ttu-id="c9d78-141">Im folgenden Markup werden diese Aufgaben ausgeführt, um einen Verweis auf das JavaScript-Objektmodell hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="c9d78-141">The following markup performs these tasks to add a reference to the JavaScript object model:</span></span>
 

 

- <span data-ttu-id="c9d78-142">Es wird auf die AJAX-Bibliothek aus dem Microsoft CDN verwiesen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-142">References the AJAX library from the Microsoft CDN.</span></span>
    
 
- <span data-ttu-id="c9d78-143">Über eine auf das Add-In-Web bezogene URL wird auf die Datei SP.Runtime.js verwiesen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-143">References the SP.Runtime.js file by using a URL relative to the add-in web.</span></span>
    
 
- <span data-ttu-id="c9d78-144">Über eine auf das Add-In-Web bezogene URL wird auf die Datei SP.js verwiesen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-144">References the SP.js file by using a URL relative to the add-in web.</span></span>
    
 



```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.runtime.js">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.js">
</script>
<script type="text/javascript">

    // Continue your program flow here.

</script>
```


## <a name="sharepoint-website-tasks"></a><span data-ttu-id="c9d78-145">SharePoint-Websiteaufgaben</span><span class="sxs-lookup"><span data-stu-id="c9d78-145">SharePoint website tasks</span></span>
<span data-ttu-id="c9d78-146"><a name="BasicOps_SPWebTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-146"></span></span>

<span data-ttu-id="c9d78-147">Wenn Sie Websites mithilfe von JavaScript bearbeiten möchten, verwenden Sie zuerst den **ClientContext(serverRelativeUrl)**-Konstruktor und übergeben eine URL oder einen URI, um einen bestimmten Anforderungskontext zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="c9d78-147">To work with websites using JavaScript, start by using the  **ClientContext(serverRelativeUrl)** constructor and pass a URL or URI to return a specific request context.</span></span>
 

 

### <a name="retrieve-the-properties-of-a-website"></a><span data-ttu-id="c9d78-148">Abrufen der Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="c9d78-148">Retrieve the properties of a website</span></span>

<span data-ttu-id="c9d78-p107">Verwenden Sie die web-Eigenschaft der **ClientContext**-Klasse, um die Eigenschaften des Website-Objekts abzurufen, das sich an der angegebenen Kontext-URL befindet. Nachdem das Website-Objekt über die **load(clientObject)**-Methode geladen und anschließend **executeQueryAsync(succeededCallback, failedCallback)** aufgerufen wurde, können Sie Zugriff auf alle Eigenschaften dieser Website erhalten. Im folgenden Beispiel werden Titel und Beschreibung der angegebenen Website angezeigt, obwohl alle anderen standardmäßig zurückgegebenen Eigenschaften verfügbar werden, nachdem das Websiteobjekt geladen und die Abfrage ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p107">Use the web property of the  **ClientContext** class to specify the properties of the website object that is located at the specified context URL. After you load the website object through the **load(clientObject)** method and then call **executeQueryAsync(succeededCallback, failedCallback)**, you acquire access to all the properties of that website. The following example displays the title and description of the specified website, although all other properties that are returned by default become available after you load the website object and execute the query.</span></span>
 

 

```

function retrieveWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="retrieve-only-selected-properties-of-a-website"></a><span data-ttu-id="c9d78-152">Abrufen nur ausgewählter Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="c9d78-152">Retrieve only selected properties of a website</span></span>

<span data-ttu-id="c9d78-p108">Sie können die unnötige Übertragung von Daten zwischen Client und Server reduzieren, indem Sie nicht alle, sondern nur angegebene Eigenschaften des Websiteobjekts zurückgeben. In diesem Fall verwenden Sie LINQ-Abfragen oder die Lambda-Ausdruckssyntax mit der **load(clientObject)**-Methode, um anzugeben, welche Eigenschaften vom Server zurückgegeben werden sollen. Im folgenden Beispiel werden nur der Titel und das Erstellungsdatum des Websiteobjekts verfügbar, nachdem **executeQueryAsync(succeededCallback, failedCallback)** aufgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p108">To reduce unnecessary data transference between client and server, you might want to return only specified properties of the website object, not all of its properties. In this case, use LINQ query or lambda expression syntax with the  **load(clientObject)** method to specify which properties to return from the server. In the following example, only the title and creation date of the website object become available after **executeQueryAsync(succeededCallback, failedCallback)** is called.</span></span>
 

 

```
function retrieveWebSiteProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite, 'Title', 'Created');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Created: ' + this.oWebsite.get_created());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


 <span data-ttu-id="c9d78-156">**Hinweis** Beim Versuch, auf andere Eigenschaften zuzugreifen, wird eine Ausnahme ausgelöst, weil keine anderen Eigenschaften verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="c9d78-156">**Note**  If you try to access other properties, the code throws an exception because other properties are not available.</span></span>
 


### <a name="write-to-a-websites-properties"></a><span data-ttu-id="c9d78-157">Festlegen der Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="c9d78-157">Write to a website's properties</span></span>

<span data-ttu-id="c9d78-p109">Zum Ändern einer Website legen Sie deren Eigenschaften fest und rufen ähnlich wie im Serverobjektmodell die **update()**-Methode auf. Im Clientobjektmodell müssen Sie jedoch **executeQueryAsync(succeededCallback, failedCallback)** aufrufen, um die Batchverarbeitung aller angegebenen Befehle anzufordern. Im folgenden Beispiel werden der Titel und die Beschreibung einer angegebenen Website geändert.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p109">To modify a website, you set its properties and call the  **update()** method, similarly to how the server object model functions. However, in the client object model, you must call **executeQueryAsync(succeededCallback, failedCallback)** to request batch processing of all commands that you specify. The following example changes the title and description of a specified website.</span></span>
 

 

```
function updateWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    this.oWebsite.set_title('Updated Web Site');
    this.oWebsite.set_description('This is an updated Web site.');
    this.oWebsite.update();

    clientContext.load(this.oWebsite, 'Title', 'Description');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="sharepoint-list-tasks"></a><span data-ttu-id="c9d78-161">SharePoint-Listenaufgaben</span><span class="sxs-lookup"><span data-stu-id="c9d78-161">SharePoint list tasks</span></span>
<span data-ttu-id="c9d78-162"><a name="BasicOps_SPListTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-162"></span></span>

<span data-ttu-id="c9d78-p110">Das Arbeiten mit Listenobjekten in JavaScript ähnelt dem Arbeiten mit Websiteobjekten. Beginnen Sie, indem Sie den **ClientContext(serverRelativeUrl)**-Konstruktor verwenden und eine URL oder einen URI übergeben, um einen bestimmten Anforderungskontext zurückzugeben. Sie können mithilfe der **lists**-Eigenschaft der **Web**-Klasse die Auflistung der Listen einer Website abrufen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p110">Working with list objects using JavaScript is similar to working with website objects. Start by using the  **ClientContext(serverRelativeUrl)** constructor and passing a URL or URI to return a specific request context. You can then use the **lists** property of the **Web** class to get the collection of lists in the website.</span></span>
 

 

### <a name="retrieve-all-properties-of-all-lists-in-a-website"></a><span data-ttu-id="c9d78-166">Abrufen aller Eigenschaften aller Listen einer Website</span><span class="sxs-lookup"><span data-stu-id="c9d78-166">Retrieve all properties of all lists in a website</span></span>

<span data-ttu-id="c9d78-p111">Zum Zurückgeben aller Listen einer Website laden Sie die Listenauflistung über die **load(clientObject)**-Methode, und rufen Sie dann **executeQueryAsync(succeededCallback, failedCallback)** auf. Im folgenden Beispiel werden die URL der Website sowie das Datum und die Uhrzeit der Erstellung der Liste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p111">To return all the lists of a website, load the list collection through the  **load(clientObject)** method, and then call **executeQueryAsync(succeededCallback, failedCallback)**. The following example displays the URL of the website and the date and time that the list was created.</span></span>
 

 

```
function retrieveAllListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();
    clientContext.load(collList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + ' Created: ' + 
            oList.get_created().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="retrieve-only-specified-properties-of-lists"></a><span data-ttu-id="c9d78-169">Abrufen der angegebenen Eigenschaften von Listen</span><span class="sxs-lookup"><span data-stu-id="c9d78-169">Retrieve only specified properties of lists</span></span>

<span data-ttu-id="c9d78-p112">Im vorhergehenden Beispiel wurden alle Eigenschaften der Listen einer Website zurückgegeben. Um unnötige Datenübertragungen zwischen Client und Server zu vermeiden, können Sie mit LINQ-Abfrageausdrücken angeben, welche Eigenschaften zurückgegeben werden sollen. In JavaScript geben Sie mit **Include** innerhalb der Abfragezeichenfolge, die der **load(clientObject)**-Methode übergeben wird, die Eigenschaften an, die zurückgegeben werden sollen. Im folgenden Beispiel werden auf diese Weise nur der Titel und die ID der einzelnen Listen der Auflistung zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p112">The previous example returns all properties of the lists in a website. To reduce unnecessary data transference between client and server, you can use LINQ query expressions to specify which properties to return. In JavaScript, you specify  **Include** as part of the query string that is passed to the **load(clientObject)** method to specify which properties to return. The following example uses this approach to return only the title and ID of each list in the collection.</span></span>
 

 

```
function retrieveSpecificListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();

    clientContext.load(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```


### <a name="store-retrieved-lists-in-a-collection"></a><span data-ttu-id="c9d78-174">Speichern abgerufener Listen in einer Auflistung</span><span class="sxs-lookup"><span data-stu-id="c9d78-174">Store retrieved lists in a collection</span></span>

<span data-ttu-id="c9d78-175">Wie im folgenden Beispiel dargestellt, können Sie die **loadQuery(clientObjectCollection, exp)**-Methode anstelle der **load(clientObject)**-Methode verwenden, um den Rückgabewert in einer anderen Auflistung anstatt in der entsprechenden Listeneigenschaft zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c9d78-175">As the following example shows, you can use the  **loadQuery(clientObjectCollection, exp)** method instead of the **load(clientObject)** method to store the return value in another collection instead of storing it in the lists property.</span></span>
 

 

```
function retrieveSpecificListPropertiesToCollection(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoCollection = clientContext.loadQuery(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoCollection.length; i++) {
        var oList = this.listInfoCollection[i];
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString();
    }
    alert(listInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="apply-filters-to-list-retrieval"></a><span data-ttu-id="c9d78-176">Anwenden von Filtern auf den Listenabruf</span><span class="sxs-lookup"><span data-stu-id="c9d78-176">Apply filters to list retrieval</span></span>

<span data-ttu-id="c9d78-p113">Wie das folgende Beispiel zeigt, können Sie **Include**-Anweisungen in einer JavaScript-Abfrage schachteln, um Metadaten sowohl für eine Liste als auch für deren Felder zurückzugeben. In diesem Beispiel werden alle Felder aus allen Listen einer Website zurückgegeben und der Titel und der interne Name aller Felder angezeigt, deren interner Name die Zeichenfolge „name“ enthält.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p113">As the following example shows, you can nest  **Include** statements in a JavaScript query to return metadata for both a list and its fields. The example returns all fields from all lists within a website and displays the title and internal name of all fields whose internal name contains the string "name".</span></span>
 

 

```
function retrieveAllListsAllFields(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoArray = clientContext.loadQuery(collList, 
        'Include(Title,Fields.Include(Title,InternalName))');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this._onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoArray.length; i++) {
        var oList = this.listInfoArray[i];
        var collField = oList.get_fields();
        var fieldEnumerator = collField.getEnumerator();
            
        while (fieldEnumerator.moveNext()) {
            var oField = fieldEnumerator.get_current();
            var regEx = new RegExp('name', 'ig');
            
            if (regEx.test(oField.get_internalName())) {
                listInfo += '\nList: ' + oList.get_title() + 
                    '\n\tField Title: ' + oField.get_title() + 
                    '\n\tField Name: ' + oField.get_internalName();
            }
        }
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```


## <a name="create-update-and-delete-lists"></a><span data-ttu-id="c9d78-179">Erstellen, Aktualisieren und Löschen von Listen</span><span class="sxs-lookup"><span data-stu-id="c9d78-179">Create, update, and delete lists</span></span>
<span data-ttu-id="c9d78-180"><a name="BasicOps_SPListCRUD"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-180"></span></span>

<span data-ttu-id="c9d78-181">Zum Erstellen, Aktualisieren und Löschen von Listen über das Clientobjektmodell gehen Sie ähnlich vor wie beim Ausführen dieser Aufgaben über das .NET-Clientobjektmodell. Allerdings werden die Clientvorgänge erst abgeschlossen, wenn die **executeQueryAsync(succeededCallback, failedCallback)**-Funktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c9d78-181">Creating, updating, and deleting lists through the client object model works similarly to how you perform these tasks using the .NET client object model, although client operations do not complete until you call the  **executeQueryAsync(succeededCallback, failedCallback)** function.</span></span>
 

 

### <a name="create-and-update-a-list"></a><span data-ttu-id="c9d78-182">Erstellen und Aktualisieren von Listen</span><span class="sxs-lookup"><span data-stu-id="c9d78-182">Create and update a list</span></span>

<span data-ttu-id="c9d78-p114">Zum Erstellen eines Listenobjekts mit JavaScript definieren Sie unter Verwendung des **ListCreationInformation**-Objekts dessen Eigenschaften. Übergeben Sie dann dieses Objekt der **add(parameters)**-Funktion des **ListCollection**-Objekts. Im folgenden Beispiel wird eine neue Liste mit dem Titel „My Announcements List“ erstellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p114">To create a list object using JavaScript, use the  **ListCreationInformation** object to define its properties, and then pass this object to the **add(parameters)** function of the **ListCollection** object. The following example creates a new announcements list.</span></span>
 

 

```
function createList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    
    var listCreationInfo = new SP.ListCreationInformation();
    listCreationInfo.set_title('My Announcements List');
    listCreationInfo.set_templateType(SP.ListTemplateType.announcements);

    this.oList = oWebsite.get_lists().add(listCreationInfo);

    clientContext.load(oList);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oList.get_title() + ' created.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<span data-ttu-id="c9d78-185">Wenn Sie eine Liste nach ihrer Erstellung aktualisieren müssen, können Sie die entsprechenden Listeneigenschaften festlegen und die **update()**-Funktion vor dem Aufruf von **executeQueryAsync(succeededCallback, failedCallback)** aufrufen. Die folgenden Änderungen am vorhergehenden Beispiel zeigen dieses Vorgehen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-185">If you need to update the list after it has been created, you can set list properties and call the  **update()** function before calling **executeQueryAsync(succeededCallback, failedCallback)**, as shown in the following modifications of the previous example.</span></span>
 

 



```
.
.
.
.
this.oList = oWebsite.get_lists().add(listCreationInfo);

oList.set_description('New Announcements List');
oList.update();

clientContext.load(oList);
clientContext.executeQueryAsync(
    Function.createDelegate(this, this.onQuerySucceeded), 
    Function.createDelegate(this, this.onQueryFailed)
);
```


### <a name="add-a-field-to-a-list"></a><span data-ttu-id="c9d78-186">Hinzufügen von Feldern zu einer Liste</span><span class="sxs-lookup"><span data-stu-id="c9d78-186">Add a field to a list</span></span>

<span data-ttu-id="c9d78-p115">Verwenden Sie die **add(field)**-Funktion oder die **addFieldAsXml(schemaXml, addToDefaultView, options)**-Funktion des **FieldCollection**-Objekts, um der Feldauflistung einer Liste ein Feld hinzuzufügen. Im folgenden Beispiel wird ein Feld erstellt, das dann vor dem Aufruf von **executeQueryAsync(succeededCallback, failedCallback)** aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p115">Use the  **add(field)** or **addFieldAsXml(schemaXml, addToDefaultView, options)** function of the **FieldCollection** object to add a field to the field collection of a list. The following example creates a field and then updates it before calling **executeQueryAsync(succeededCallback, failedCallback)**.</span></span>
 

 

```
function addFieldToList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);

    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oField = oList.get_fields().addFieldAsXml(
        '<Field DisplayName=\'MyField\' Type=\'Number\' />', 
        true, 
        SP.AddFieldOptions.defaultValue
    );

    var fieldNumber = clientContext.castTo(oField,SP.FieldNumber);
    fieldNumber.set_maximumValue(100);
    fieldNumber.set_minimumValue(35);
    fieldNumber.update();

    clientContext.load(oField);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oField.get_title() + ' added.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="delete-a-list"></a><span data-ttu-id="c9d78-189">Löschen einer Liste</span><span class="sxs-lookup"><span data-stu-id="c9d78-189">Delete a list</span></span>

<span data-ttu-id="c9d78-190">Zum Löschen einer Liste rufen Sie die **deleteObject()**-Funktion des Listenobjekts auf, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-190">To delete a list, call the  **deleteObject()** function of the list object, as shown in the following example.</span></span>
 

 

```
function deleteList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.listTitle = 'My Announcements List';

    this.oList = oWebsite.get_lists().getByTitle(listTitle);
    oList.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = listTitle + ' deleted.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="create-update-and-delete-folders"></a><span data-ttu-id="c9d78-191">Erstellen, Aktualisieren und Löschen von Ordnern</span><span class="sxs-lookup"><span data-stu-id="c9d78-191">Create, update, and delete folders</span></span>
<span data-ttu-id="c9d78-192"><a name="BasicOps_FolderTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-192"></span></span>

<span data-ttu-id="c9d78-p116">Sie können Ordner für die Organisation Ihrer Inhalte anpassen, indem Sie das JavaScript-Objektmodell verwenden. In den folgenden Abschnitten ist beschrieben, wie Sie grundlegende Schritte für Ordner ausführen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p116">You can manipulate folders to organize your content by using the JavaScript object model. The following sections show you how to perform basic operations on folders.</span></span>
 

 

### <a name="create-a-folder-in-a-document-library"></a><span data-ttu-id="c9d78-195">Erstellen eines Ordners in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-195">Create a folder in a document library</span></span>

<span data-ttu-id="c9d78-p117">Zum Erstellen eines Ordners verwenden Sie ein **ListItemCreationInformation**-Objekt, legen den zugrunde liegenden Objekttyp auf **SP.FileSystemObjectType.folder** fest und übergeben diesen als Parameter an die **addItem(parameters)**-Funktion des **List**-Objekts. Legen Sie Eigenschaften für das von dieser Methode zurückgegebene Listenelementobjekt fest, und rufen Sie dann die **update()**-Funktion auf. Dies ist im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p117">To create a folder, you use a  **ListItemCreationInformation** object, set the underlying object type to **SP.FileSystemObjectType.folder**, and pass it as parameter to the  **addItem(parameters)** function of the **List** object. Set properties on the list item object that this method returns, and then call the **update()** function, as shown in the following example.</span></span>
 

 

```
function createFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var itemCreateInfo;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    itemCreateInfo = new SP.ListItemCreationInformation();
    itemCreateInfo.set_underlyingObjectType(SP.FileSystemObjectType.folder);
    itemCreateInfo.set_leafName("My new folder!");
    this.oListItem = oList.addItem(itemCreateInfo);
    this.oListItem.set_item("Title", "My new folder!");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="update-a-folder-in-a-document-library"></a><span data-ttu-id="c9d78-198">Aktualisieren eines Ordners in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-198">Update a folder in a document library</span></span>

<span data-ttu-id="c9d78-199">Zum Aktualisieren des Ordnernamens können Sie in die **FileLeafRef**-Eigenschaft schreiben und die **update()**-Funktion aufrufen, damit Änderungen wirksam werden, wenn Sie die **executeQueryAsync**-Methode aufrufen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-199">To update the folder name, you can write to the  **FileLeafRef** property and call the **update()** function so that changes take effect when you call the **executeQueryAsync** method.</span></span>
 

 

```
function updateFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    this.oListItem = oList.getItemById(1);
    this.oListItem.set_item("FileLeafRef", "My updated folder");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your updated folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="delete-a-folder-in-a-document-library"></a><span data-ttu-id="c9d78-200">Löschen eines Ordners in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-200">Delete a folder in a document library</span></span>

<span data-ttu-id="c9d78-p118">Zum Löschen eines Ordners rufen Sie die **deleteObject()**-Funktion für das Objekt auf. Im folgenden Beispiel wird die **getFolderByServerRelativeUrl**-Methode verwendet, um den Ordner aus der Dokumentbibliothek abzurufen, und anschließend wird das Element gelöscht.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p118">To delete a folder, call the  **deleteObject()** function on the object. The following example uses the **getFolderByServerRelativeUrl** method to retrieve the folder from the document library and then deletes the item.</span></span>
 

 

```
function deleteFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var folderUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        folderUrl = oWebsite.get_serverRelativeUrl() + "/Lists/Shared Documents/Folder1";
        this.folderToDelete = oWebsite.getFolderByServerRelativeUrl(folderUrl);
        this.folderToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to make sure the folder is no longer there.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


## <a name="create-read-update-and-delete-files"></a><span data-ttu-id="c9d78-203">Erstellen, Lesen, Aktualisieren und Löschen von Dateien</span><span class="sxs-lookup"><span data-stu-id="c9d78-203">Create, read, update, and delete files</span></span>
<span data-ttu-id="c9d78-204"><a name="BasicOps_FileTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-204"></span></span>

<span data-ttu-id="c9d78-p119">Sie können Dateien mithilfe des JavaScript-Objektmodells anpassen. In den folgenden Abschnitten ist beschrieben, wie Sie grundlegende Schritte für Dateien ausführen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p119">You can manipulate files by using the JavaScript object model. The following sections show you how to perform basic operations on files.</span></span>
 

 

 <span data-ttu-id="c9d78-p120">**Hinweis** Sie können nur Dateien mit einer Größe von bis zu 1,5 MB verwenden, wenn Sie das JavaScript-Objektmodell nutzen. Um größere Dateien hochzuladen, müssen Sie REST (Representational State Transfer) nutzen. Weitere Informationen finden Sie unter [](complete-basic-operations-using-sharepoint-rest-endpoints#LargeFiles.md).</span><span class="sxs-lookup"><span data-stu-id="c9d78-p120">**Note**  You can only work with files up to 1.5 MB by using the JavaScript object model. To upload larger files, use REST (Representational State Transfer). For more information, see  [](complete-basic-operations-using-sharepoint-rest-endpoints#LargeFiles.md).</span></span>
 


### <a name="create-a-file-in-a-document-library"></a><span data-ttu-id="c9d78-210">Erstellen einer Datei in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-210">Create a file in a document library</span></span>

<span data-ttu-id="c9d78-211">Zum Erstellen von Dateien verwenden Sie ein **FileCreationInformation**-Objekt, legen das URL-Attribut fest und fügen Inhalte als base64-codiertes Bytearray an. Dies ist im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-211">To create files, you use a  **FileCreationInformation** object, set the URL attribute, and append content as a base64 encoded array of bytes, as shown in this example.</span></span>
 

 

```
function createFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("my new file.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileContent = "The content of my new file";

    for (var i = 0; i < fileContent.length; i++) {
        
        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.newFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.newFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new file.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="read-a-file-in-a-document-library"></a><span data-ttu-id="c9d78-212">Lesen einer Datei in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-212">Read a file in a document library</span></span>

<span data-ttu-id="c9d78-213">Zum Lesen des Inhalts einer Datei führen Sie einen **GET**-Vorgang für die URL der Datei durch. Dies ist im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-213">To read a file's content, you perform a  **GET** operation on the file's URL, as shown in the following example.</span></span>
 

 

```
function readFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        $.ajax({
            url: fileUrl,
            type: "GET"
        })
            .done(Function.createDelegate(this, successHandler))
            .error(Function.createDelegate(this, errorHandler));
    }, errorHandler);

    function successHandler(data) {
        resultpanel.innerHTML =
            "The content of file \"TextFile1.txt\": " + data
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[2];
    }
}
```


### <a name="update-a-file-in-a-document-library"></a><span data-ttu-id="c9d78-214">Aktualisieren einer Datei in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-214">Update a file in a document library</span></span>

<span data-ttu-id="c9d78-215">Zum Aktualisieren des Inhalts der Datei können Sie ein **FileCreationInformation**-Objekt verwenden und das overwrite-Attribut auf „true“ festlegen, indem Sie die **set_overwrite()**-Methode verwenden. Dies ist in diesem Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-215">To update the file's content, you can use a  **FileCreationInformation** object, and set the overwrite attribute to true by using the **set_overwrite()** method, as shown in this example.</span></span>
 

 

```
function updateFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("TextFile1.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileCreateInfo.set_overwrite(true);
    fileContent = "The updated content of my file";

    for (var i = 0; i < fileContent.length; i++) {

        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.existingFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.existingFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see the updated \"TextFile1.txt\" file.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="delete-a-file-in-a-document-library"></a><span data-ttu-id="c9d78-216">Löschen einer Datei in einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="c9d78-216">Delete a file in a document library</span></span>

<span data-ttu-id="c9d78-p121">Zum Löschen einer Datei rufen Sie die **deleteObject()**-Funktion für das Objekt auf. Im folgenden Beispiel wird die **getFileByServerRelativeUrl**-Methode verwendet, um die Datei aus der Dokumentbibliothek abzurufen, und anschließend wird das Element gelöscht.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p121">To delete a file, call the  **deleteObject()** function on the object. The following example uses the **getFileByServerRelativeUrl** method to retrieve the file from the document library, and then deletes the item.</span></span>
 

 

```
function deleteFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        this.fileToDelete = oWebsite.getFileByServerRelativeUrl(fileUrl);
        this.fileToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to confirm that the \"TextFile1.txt\" file has been deleted.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


## <a name="sharepoint-list-item-tasks"></a><span data-ttu-id="c9d78-219">SharePoint-Listenelementaufgaben</span><span class="sxs-lookup"><span data-stu-id="c9d78-219">SharePoint list item tasks</span></span>
<span data-ttu-id="c9d78-220"><a name="BasicOps_SPListItemTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-220"></span></span>

<span data-ttu-id="c9d78-p122">Um unter Verwendung von JavaScript Elemente einer Liste zurückzugeben, verwenden Sie die **getItemById(id)**-Funktion zum Zurückgeben eines einzelnen Elements oder die **getItems(query)**-Funktion zum Zurückgeben mehrerer Elemente. Mit der **load(clientObject)**-Funktion können Sie dann Listenelementobjekte abrufen, die diese Elemente darstellen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p122">To return items from a list using JavaScript, use the  **getItemById(id)** function to return a single item, or use the **getItems(query)** function to return multiple items. You then use the **load(clientObject)** function to attain list item objects that represent the items.</span></span>
 

 

### <a name="retrieve-items-from-a-list"></a><span data-ttu-id="c9d78-223">Abrufen von Listenelementen</span><span class="sxs-lookup"><span data-stu-id="c9d78-223">Retrieve items from a list</span></span>

<span data-ttu-id="c9d78-p123">Mit der **getItems(query)**-Funktion können Sie eine CAML-Abfrage (Collaborative Application Markup Language) definieren, die angibt, welche Elemente zurückgegeben werden sollen. Sie können ein undefiniertes **CamlQuery**-Objekt übergeben, um alle Elemente der Liste zurückzugeben, oder mit der **set_viewXml**-Funktion eine CAML-Abfrage definieren und nur Elemente zurückgeben, die bestimmte Kriterien erfüllen. Im folgenden Beispiel werden neben den Werten der Spalten „Title“ und „Body“ die IDs der ersten 100 Elemente der Liste „Announcements“ angezeigt, wobei mit den Listenelementen begonnen wird, deren ID größer als 10 ist.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p123">The  **getItems(query)** function enables you to define a Collaborative Application Markup Language (CAML) query that specifies which items to return. You can pass an undefined **CamlQuery** object to return all items from the list, or use the **set_viewXml** function to define a CAML query and return items that meet specific criteria. The following example displays the ID, in addition to the Title and Body column values, of the first 100 items in the Announcements list, starting with list items whose collection ID is greater than 10.</span></span>
 

 

```
function retrieveListItems(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml(
        '<View><Query><Where><Geq><FieldRef Name=\'ID\'/>' + 
        '<Value Type=\'Number\'>1</Value></Geq></Where></Query>' + 
        '<RowLimit>10</RowLimit></View>'
    );
    this.collListItem = oList.getItems(camlQuery);
        
    clientContext.load(collListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    ); 
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nTitle: ' + oListItem.get_item('Title') + 
            '\nBody: ' + oListItem.get_item('Body');
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="use-the-include-method-to-access-properties-of-listitem-objects"></a><span data-ttu-id="c9d78-227">Zugreifen auf Eigenschafen von ListItem-Objekten mit der Include-Methode</span><span class="sxs-lookup"><span data-stu-id="c9d78-227">Use the Include method to access properties of ListItem objects</span></span>

<span data-ttu-id="c9d78-p124">Vier Eigenschaften von **ListItem**-Objekten sind standardmäßig nicht verfügbar, wenn Listenelemente zurückgegeben werden: **displayName**, **effectiveBasePermissions**, **hasUniqueRoleAssignments** und **roleAssignments**. Im vorhergehenden Beispiel wird eine Ausnahme vom Typ **PropertyOrFieldNotInitializedException** zurückgegeben, wenn Sie auf eine dieser Eigenschaften zuzugreifen versuchen. Um auf diese Eigenschaften zuzugreifen, geben Sie die **Include**-Methode in der Abfragezeichenfolge an, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p124">Four properties of  **ListItem** objects are not available by default when you return list items??? **displayName**,  **effectiveBasePermissions**,  **hasUniqueRoleAssignments**, and  **roleAssignments**. The previous example returns a  **PropertyOrFieldNotInitializedException** if you try to access one of these properties. To access these properties, use the **Include** method as part of the query string, as shown in the following example.</span></span>
 

 

 <span data-ttu-id="c9d78-232">**Hinweis** Wenn Sie mit LINQ das Clientobjektmodell abfragen, verwenden Sie [LINQ to Objects](http://msdn.microsoft.com/library/bb397919), nicht den [LINQ to SharePoint-Anbieter](http://msdn.microsoft.com/library/ee535491), der nur in Code zum Abfragen des Serverobjektmodells verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="c9d78-232">**Note**  When you use LINQ to create queries against the client object model, you are using  [LINQ to Objects](http://msdn.microsoft.com/library/bb397919), not the  [LINQ to SharePoint provider](http://msdn.microsoft.com/library/ee535491), which can only be used when you write code against the server object model.</span></span>
 


```
function retrieveListItemsInclude(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml('<View><RowLimit>100</RowLimit></View>');
    this.collListItem = oList.getItems(camlQuery);

    clientContext.load(
        collListItem, 
        'Include(Id, DisplayName, HasUniqueRoleAssignments)'
    );
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nDisplay name: ' + oListItem.get_displayName() + 
            '\nUnique role assignments: ' + 
            oListItem.get_hasUniqueRoleAssignments();
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```

<span data-ttu-id="c9d78-p125">Weil in diesem Beispiel die **Include**-Methode verwendet wird, sind nach der Ausführung der Abfrage nur die angegebenen Eigenschaften verfügbar. Daher wird eine **PropertyOrFieldNotInitializedException**-Ausnahme ausgelöst, wenn Sie versuchen, auf andere als die genannten Eigenschaften zuzugreifen. Zudem erhalten Sie diesen Fehler, wenn Sie mit Funktionen wie **get_contentType** oder **get_parentList** auf Eigenschaften von übergeordneten Objekten zuzugreifen versuchen.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p125">Because this example uses an  **Include**, only the specified properties are available after query execution. Therefore, you receive a  **PropertyOrFieldNotInitializedException** if you try to access other properties beyond those that have been specified. In addition, you receive this error if you try to use functions such as **get_contentType** or **get_parentList** to access the properties of containing objects.</span></span>
 

 

### <a name="restrictions-on-retrieving-items"></a><span data-ttu-id="c9d78-236">Beschränkungen beim Abrufen von Elementen</span><span class="sxs-lookup"><span data-stu-id="c9d78-236">Restrictions on retrieving items</span></span>

<span data-ttu-id="c9d78-237">Die **loadQuery(clientObjectCollection, exp)**-Methode des JavaScript-Objektmodells in SharePoint Foundation 2010 unterstützt die LINQ-Methoden und -Operatoren nicht, die im verwalteten Objektmodell verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c9d78-237">The  **loadQuery(clientObjectCollection, exp)** method of the JavaScript object model in SharePoint Foundation 2010 does not support LINQ methods and operators that are used by the managed object model.</span></span>
 

 

## <a name="create-update-and-delete-list-items"></a><span data-ttu-id="c9d78-238">Erstellen, Aktualisieren und Löschen von Listenelementen</span><span class="sxs-lookup"><span data-stu-id="c9d78-238">Create, update, and delete list items</span></span>
<span data-ttu-id="c9d78-239"><a name="BasicOps_SPListItemCRUD"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-239"></span></span>

<span data-ttu-id="c9d78-p126">Das Erstellen, Aktualisieren oder Löschen von Listenelementen über das Clientobjektmodell funktioniert ähnlich wie das Ausführen dieser Aufgaben über das Serverobjektmodell. Sie erstellen ein Listenelementobjekt, legen seine Eigenschaften fest und aktualisieren dann das Objekt. Verwenden Sie zum Ändern oder Löschen eines Listenelementobjekts die **getById(id)**-Methode der **ListItemCollection**-Klasse, um das Objekt zurückzugeben, und legen Sie dann entweder Eigenschaften fest und rufen Sie die Aktualisierung des Objekts auf, das von dieser Methode zurückgegeben wird, oder rufen Sie die objekteigene Methode zum Löschen auf. Anders als beim Serverobjektmodell muss jeder dieser Vorgänge im Clientobjektmodell mit einem Aufruf von **executeQueryAsync(succeededCallback, failedCallback)** beendet werden, damit die Änderungen auf dem Server übernommen werden.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p126">Creating, updating, or deleting list items through the client object model works similarly to performing these tasks through the server object model. You create a list item object, set its properties, and then update the object. To modify or delete a list item object, use the  **getById(id)** function of the **ListItemCollection** object to return the object, and then either set properties and call update on the object that this method returns, or call the object's own method for deletion. Unlike the server object model, each of these operations in the client object model must conclude with a call **to executeQueryAsync(succeededCallback, failedCallback)** for changes to take effect on the server.</span></span>
 

 

### <a name="create-a-list-item"></a><span data-ttu-id="c9d78-244">Erstellen eines Listenelements</span><span class="sxs-lookup"><span data-stu-id="c9d78-244">Create a list item</span></span>

<span data-ttu-id="c9d78-p127">Zum Erstellen von Listenelementen erstellen Sie ein **ListItemCreationInformation**-Objekt, legen dessen Eigenschaften fest und übergeben das Objekt als Parameter an die **addItem(parameters)**-Funktion des **List**-Objekts. Legen Sie Eigenschaften für das von dieser Methode zurückgegebene Listenelementobjekt fest, und rufen Sie dann **update()** auf. Dies ist im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p127">To create list items, you create a  **ListItemCreationInformation** object, set its properties, and pass it as parameter to the **addItem(parameters)** function of the **List** object. Set properties on the list item object that this method returns, and then call the **update()** function, as shown in the following example.</span></span>
 

 

```
function createListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var itemCreateInfo = new SP.ListItemCreationInformation();
    this.oListItem = oList.addItem(itemCreateInfo);
    oListItem.set_item('Title', 'My New Item!');
    oListItem.set_item('Body', 'Hello World!');
    oListItem.update();

    clientContext.load(oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item created: ' + oListItem.get_id());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="update-a-list-item"></a><span data-ttu-id="c9d78-247">Aktualisieren eines Listenelements</span><span class="sxs-lookup"><span data-stu-id="c9d78-247">Update a list item</span></span>

<span data-ttu-id="c9d78-p128">Zum Festlegen der meisten Listenelementeigenschaften können Sie mithilfe eines Spaltenindexers eine Zuweisung definieren und die **update()**-Funktion aufrufen, sodass Änderungen übernommen werden, wenn Sie **executeQueryAsync(succeededCallback, failedCallback)** aufrufen. Im folgenden Beispiel wird der Titel des dritten Elements der Liste „Announcements“ festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p128">To set most list item properties, you can use a column indexer to make an assignment, and call the  **update()** function so that changes will take effect when you call **executeQueryAsync(succeededCallback, failedCallback)**. The following example sets the title of the third item in the Announcements list.</span></span>
 

 

```
function updateListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    this.oListItem = oList.getItemById(3);
    oListItem.set_item('Title', 'My Updated Title');
    oListItem.update();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item updated!');
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="delete-a-list-item"></a><span data-ttu-id="c9d78-250">Löschen eines Listenelements</span><span class="sxs-lookup"><span data-stu-id="c9d78-250">Delete a list item</span></span>

<span data-ttu-id="c9d78-p129">Rufen Sie zum Löschen eines Listenelements die **deleteObject()**-Methode für das Objekt auf. Im folgenden Beispiel wird die **getItemById(id)**-Methode verwendet, um das zweite Element aus der Liste zurückzugeben. Anschließend wird das Element gelöscht. SharePoint behält die ganzzahligen IDs der Elemente innerhalb von Auflistungen selbst dann bei, wenn die Elemente gelöscht wurden. Daher kann das zweite Element einer Liste unter Umständen eine andere ID als 2 besitzen. Es wird eine Ausnahme vom Typ **ServerException** zurückgegeben, wenn die **deleteObject()**-Methode für ein nicht vorhandenes Element aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p129">To delete a list item, call the  **deleteObject()** function on the object. The following example uses the **getItemById(id)** function to return the second item from the list, and then deletes the item. SharePoint maintains the integer IDs of items within collections, even if they have been deleted. So, for example, the second item in a list might not have 2 as its identifier. A **ServerException** is returned if the **deleteObject()** function is called for an item that does not exist.</span></span>
 

 

```
function deleteListItem(siteUrl) {
    this.itemId = 2;
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item deleted: ' + itemId);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<span data-ttu-id="c9d78-p130">Wenn Sie z. B. die neue Elementanzahl abrufen möchten, die das Ergebnis eines Löschvorgangs ist, schließen Sie einen Aufruf der update()-Methode ein, um die Liste zu aktualisieren. Zudem müssen Sie entweder das Listenobjekt oder die **itemCount**-Eigenschaft für das Listenobjekt aufrufen, bevor Sie die Abfrage ausführen. Wenn Sie die Anzahl der Listenelemente am Anfang und am Ende abrufen möchten, müssen Sie zwei Abfragen ausführen und die Elementanzahl zweimal zurückgeben, wie es in der folgenden Änderung des vorherigen Beispiels gezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="c9d78-p130">If you want to retrieve, for example, the new item count that results from a delete operation, include a call to the update() method to refresh the list. In addition, you must load either the list object itself or the  **itemCount** property on the list object before executing the query. If you want to retrieve both a start and end count of the list items, you must execute two queries and return the item count twice, as shown in the following modification of the previous example.</span></span>
 

 



```
function deleteListItemDisplayCount(siteUrl) {
    this.clientContext = new SP.ClientContext(siteUrl);
    this.oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    clientContext.load(oList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.deleteItem), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function deleteItem() {
    this.itemId = 58;
    this.startCount = oList.get_itemCount();
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    oList.update();
    clientContext.load(oList);
        
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.displayCount), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function displayCount() {
    var endCount = oList.get_itemCount();
    var listItemInfo = 'Item deleted: ' + itemId + 
        '\nStart Count: ' +  startCount + 
        ' End Count: ' + endCount;
        
    alert(listItemInfo)
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="access-objects-in-the-host-web"></a><span data-ttu-id="c9d78-259">Zugreifen auf Objekte im Hostweb</span><span class="sxs-lookup"><span data-stu-id="c9d78-259">Access objects in the host web</span></span>
<span data-ttu-id="c9d78-260"><a name="BasicOps_AccessHostweb"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-260"></span></span>

<span data-ttu-id="c9d78-p131">Beim Entwickeln des Add-Ins müssen Sie möglicherweise auf das Hostweb zugreifen, um mit den darin enthaltenen Elementen zu interagieren. Verwenden Sie das **AppContextSite**-Objekt, um auf das Hostweb oder andere SharePoint-Websites zu verweisen. Dies ist im folgenden Beispiel dargestellt. Ein vollständiges Codebeispiel finden Sie unter [Abrufen des Hostwebtitels mithilfe der domänenübergreifenden Bibliothek (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-Get-the-563f2a3d).</span><span class="sxs-lookup"><span data-stu-id="c9d78-p131">While developing your add-in, you might need to access the host web to interact with items in it. Use the  **AppContextSite** object to reference the host web or other SharePoint sites, as shown in the following example. For a full code sample, see [Get the host web title using the cross-domain library (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-Get-the-563f2a3d).</span></span>
 

 

```
function execCrossDomainRequest(appweburl, hostweburl) {
    // context: The ClientContext object provides access to
    //      the web and lists objects.
    // factory: Initialize the factory object with the
    //      add-in web URL.
    var context;
    var factory;
    var appContextSite;

    context = new SP.ClientContext(appweburl);
    factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
    context.set_webRequestExecutorFactory(factory);
    appContextSite = new SP.AppContextSite(context, hostweburl);

    this.web = appContextSite.get_web();
    context.load(this.web);

    // Execute the query with all the previous 
    //  options and parameters.
    context.executeQueryAsync(
        Function.createDelegate(this, successHandler), 
        Function.createDelegate(this, errorHandler)
    );

    // Function to handle the success event.
    // Prints the host web's title to the page.
    function successHandler() {
        alert(this.web.get_title());
    }

    // Function to handle the error event.
    // Prints the error message to the page.
    function errorHandler(data, errorCode, errorMessage) {
        alert("Could not complete cross-domain call: " + errorMessage);
    }
}
```

<span data-ttu-id="c9d78-p132">Im vorherigen Beispiel wird die domänenübergreifende Bibliothek in SharePoint zum Zugreifen auf das Hostweb verwendet. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="c9d78-p132">The previous example uses the cross-domain library in SharePoint to access the host web. For more information, see  [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="c9d78-266">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c9d78-266">Additional resources</span></span>
<span data-ttu-id="c9d78-267"><a name="BasicOps_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="c9d78-267"></span></span>


-  [<span data-ttu-id="c9d78-268">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="c9d78-268">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [<span data-ttu-id="c9d78-269">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="c9d78-269">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="c9d78-270">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="c9d78-270">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="c9d78-271">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c9d78-271">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="c9d78-272">Arbeiten mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9d78-272">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
    
 

