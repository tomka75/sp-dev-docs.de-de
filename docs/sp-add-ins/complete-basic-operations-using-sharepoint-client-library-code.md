# <a name="complete-basic-operations-using-sharepoint-client-library-code"></a><span data-ttu-id="f92c0-101">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="f92c0-101">Complete basic operations using SharePoint client library code</span></span>
<span data-ttu-id="f92c0-102">In diesem Artikel erfahren Sie, wie Sie Code zum Ausführen grundlegender Vorgänge mit dem SharePoint .NET Framework-Clientobjektmodell (CSOM) schreiben.</span><span class="sxs-lookup"><span data-stu-id="f92c0-102">Learn how to write code to perform basic operations with the SharePoint .NET Framework client object model (CSOM).</span></span>
 

 <span data-ttu-id="f92c0-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f92c0-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="sharepoint-client-apis"></a><span data-ttu-id="f92c0-106">SharePoint-Client-APIs</span><span class="sxs-lookup"><span data-stu-id="f92c0-106">SharePoint client APIs</span></span>
<span data-ttu-id="f92c0-107"><a name="ClientAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-107"></span></span>

<span data-ttu-id="f92c0-p102">Sie können das SharePoint-Clientobjektmodell (CSOM) zum Abrufen, Aktualisieren und Verwalten von Daten in SharePoint verwenden. SharePoint macht das CSOM in verschiedener Form verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p102">You can use the SharePoint client object model (CSOM) to retrieve, update, and manage data in SharePoint. SharePoint makes the CSOM available in several forms.</span></span> 
 

 

- <span data-ttu-id="f92c0-110">Weitervertreibbare .NET Framework-Assemblys</span><span class="sxs-lookup"><span data-stu-id="f92c0-110">.NET Framework redistributable assemblies</span></span>
    
 
- <span data-ttu-id="f92c0-111">JavaScript-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="f92c0-111">JavaScript library</span></span>
    
 
- <span data-ttu-id="f92c0-112">REST-/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="f92c0-112">REST/OData endpoints</span></span>
    
 
- <span data-ttu-id="f92c0-113">Windows Phone-Assemblys</span><span class="sxs-lookup"><span data-stu-id="f92c0-113">Windows Phone assemblies</span></span>
    
 
- <span data-ttu-id="f92c0-114">Weitervertreibbare Silverlight-Assemblys</span><span class="sxs-lookup"><span data-stu-id="f92c0-114">Silverlight redistributable assemblies</span></span>
    
 
<span data-ttu-id="f92c0-115">Weitere Informationen zu den Gruppen von APIs, die auf der SharePoint-Plattform verfügbar sind, finden Sie unter [Auswählen des richtigen API-Satzes in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f92c0-115">For more details about the sets of APIs available on the SharePoint platform, see  [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span> 
 

 
<span data-ttu-id="f92c0-p103">In diesem Artikel wird beschrieben, wie Sie grundlegende Vorgänge mithilfe des .NET Framework-Objektmodells ausführen, das als weitervertreibbares Paket im Microsoft Download Center verfügbar ist. Suchen Sie nach „SDKs für SharePoint Server 2013-Clientkomponenten" oder „SKDs für SharePoint Online-Clientkomponenten". Informationen zur Verwendung der anderen Client-APIs finden Sie unter  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013),  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints),  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx) und [Verwenden des Silverlight-Objektmodells](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) im SharePoint 2010 SDK.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p103">This article is shows how to perform basic operations using the .NET Framework object model, which is available as a redistributable package on the Microsoft Download Center. Search for "SharePoint Server 2013 Client Components SDK" or "SharePoint Online Client Components SDK". For information about how to use the other client APIs see,  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013),  [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-2013-rest-endpoints),  [Build Windows Phone apps that access SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx), and  [Using the Silverlight Object Model](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) in the SharePoint 2010 SDK.</span></span>
 

 

## <a name="basic-operations-with-the-sharepoint-net-client-object-model"></a><span data-ttu-id="f92c0-119">Grundlegende Vorgänge mit dem SharePoint .NET-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="f92c0-119">Basic operations with the SharePoint .NET client object model</span></span>
<span data-ttu-id="f92c0-120"><a name="BasicOps_SPCSOMOps"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-120"></span></span>

<span data-ttu-id="f92c0-121">In den folgenden Abschnitten werden Aufgaben beschrieben, die programmgesteuert ausgeführt werden können. Die Abschnitte enthalten C#-Codebeispiele, die CSOM-Vorgänge veranschaulichen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-121">The following sections describe tasks that you can complete programmatically, and they include C# code examples that demonstrate CSOM operations.</span></span>
 

 
<span data-ttu-id="f92c0-p104">Wenn Sie in Visual Studio 2012 ein **Add-In für SharePoint**-Projekt erstellen, werden dem Projekt automatisch Verweise auf die .NET Framework-Assemblys **Microsoft.SharePoint.Client.Runtime.dll** und **Microsoft.SharePoint.Client.dll** hinzugefügt. Bei anderen Arten von Projekten, z. B. .NET Framework-Anwendungen oder Konsolenanwendungen, müssen Sie diese Verweise hinzufügen. Die Dateien befinden sich auf jedem SharePoint-Server im Ordner „%ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI“.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p104">When you create an Add-in for SharePoint project in Visual Studio 2012, references to the .NET Framework assemblies, Microsoft.SharePoint.Client.Runtime.dll and Microsoft.SharePoint.Client.dll, are automatically added to the project. For other kinds of projects, such as .NET Framework applications or console applications, you should add these references. The files are located on any SharePoint server at %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15ISAPI.</span></span>
 

 
<span data-ttu-id="f92c0-p105">In allen Beispielen hier wird vorausgesetzt, dass der Code in einer CodeBehind-Datei für eine Microsoft ASP.NET-Webseite enthalten ist. Sie müssen der Codedatei die folgende **using**-Anweisung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p105">All of these examples assume that the code is in a code-behind file for an Microsoft ASP.NET webpage. You must add the following **using** statement to the code file.</span></span>
 

 



```
using Microsoft.SharePoint.Client;
```

<span data-ttu-id="f92c0-p106">Sofern nicht ausdrücklich etwas Anderes angegeben wird, kann davon ausgegangen werden, dass jedes dieser Beispiele in einer parameterlosen Methode enthalten ist, die in der Klasse der Seite definiert ist. Zudem gilt, dass  `label1`,  `label2` usw. die Namen von auf der Seite befindlichen [Label](http://msdn2.microsoft.com/EN-US/library/620f4ses) -Objekten sind.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p106">Except where specified otherwise, you can assume that each of these examples is in a parameterless method that is defined in the page's class. Also,  `label1`,  `label2`, and so on, are the names of  [Label](http://msdn2.microsoft.com/EN-US/library/620f4ses) objects on the page.</span></span>
 

 

 <span data-ttu-id="f92c0-p107">**Hinweis** Wenn Sie ein vom Anbieter gehostetes SharePoint-Add-In mit einer ASP.NET-Webanwendung erstellen und einen Verweis zu einer Assembly des Webanwendungsprojekts in Visual Studio hinzufügen, müssen Sie die Eigenschaft **Lokal kopieren** der Assembly auf **True** festlegen, sofern Sie nicht sicher wissen, dass die Assembly bereits auf dem Web-Server installiert ist, oder Sie sicherstellen können, dass sie installiert wird, bevor Sie das Add-In bereitstellen. .NET Framework wird in Microsoft Azure-Webrollen und Azure-Websites installiert. Die SharePoint-Client-Assemblys und die verschiedenen Erweiterungen durch verwalteten Code und Foundations von Microsoft werden nicht installiert. Office Developer Tools für Visual Studio 2012 fügt zu häufig in SharePoint-Add-Ins verwendeten Assemblys automatisch Verweise hinzu und legt die Eigenschaft **Lokal kopieren** fest.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p107">**Note** When you are making a provider-hosted SharePoint Add-in with an ASP.NET web application and you add a reference to an assembly to the web application project in Visual Studio, set the **Copy Local** property of the assembly to **True**, unless you know that the assembly is already installed on the web server, or you can ensure that it is installed before you deploy your add-in. The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites. But the SharePoint client assemblies and the various Microsoft managed code extensions and foundations are not installed. Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the **Copy Local** property.</span></span>
 


## <a name="sharepoint-website-tasks"></a><span data-ttu-id="f92c0-133">SharePoint-Websiteaufgaben</span><span class="sxs-lookup"><span data-stu-id="f92c0-133">SharePoint website tasks</span></span>
<span data-ttu-id="f92c0-134"><a name="BasicOps_SPWebTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-134"></span></span>

<span data-ttu-id="f92c0-135">In diesen Beispielen wird gezeigt, wie Sie mit dem .NET Framework-CSOM Aufgaben ausführen, die Websites betreffen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-135">These examples show how to use the .NET Framework CSOM to complete website-related tasks.</span></span>
 

 

### <a name="retrieve-the-properties-of-a-website"></a><span data-ttu-id="f92c0-136">Abrufen der Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="f92c0-136">Retrieve the properties of a website</span></span>

<span data-ttu-id="f92c0-137">Rufen Sie den Titel einer SharePoint-Website ab.</span><span class="sxs-lookup"><span data-stu-id="f92c0-137">Retrieve the title of a SharePoint website.</span></span>
 

 

```C#

// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// We want to retrieve the web's properties.
context.Load(web); 

// Execute the query to the server.
context.ExecuteQuery(); 

// Now, the web's properties are available and we could display 
// web properties, such as title. 
label1.Text = web.Title;

```


### <a name="retrieve-only-selected-properties-of-a-website"></a><span data-ttu-id="f92c0-138">Abrufen nur ausgewählter Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="f92c0-138">Retrieve only selected properties of a website</span></span>

<span data-ttu-id="f92c0-p108">Manchmal ist der Client nur an einigen Eigenschaften eines Objekts interessiert. Im SharePoint .NET Framework-CSOM ist es nicht erforderlich, alle Eigenschaften des Objekts auf dem Server abzurufen. Sie können mit anonymen Methoden, bei denen es sich um lambda-Ausdrücke handeln kann, bestimmte Eigenschaftennamen anfordern. Die Clientbibliothek fragt dann nur diese Eigenschaften vom Server ab, und der Server sendet nur diese Eigenschafen an den Client. Diese Technik bewirkt, dass weniger unnötige Daten zwischen Client und Server übermittelt werden. Sie ist auch hilfreich, wenn der Benutzer nicht berechtigt ist, auf eine oder mehrere der anderen, nicht verwendeten Eigenschaften des Objekts zuzugreifen. Beachten Sie, dass Sie eine **using**-Anweisung für  [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen müssen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p108">Sometimes, the client is interested only in a few properties of an object. The SharePoint .NET Framework CSOM does not require you to get all properties from the object on a server—you can use anonymous methods, which can be lambda expressions, to specifically request property names. The client library will query only for those properties on the server, and the server will send only those properties to the client. This technique reduces unnecessary data transfer between the client and the server. It is also useful when the user does not have permission to one or more of the other, unused properties on an object. Note that you will need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) .</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// We want to retrieve the web's title and description. 
context.Load(web, w => w.Title, w => w.Description); 

// Execute the query to server.
context.ExecuteQuery(); 

// Now, only the web's title and description are available. If you 
// try to print out other properties, the code will throw 
// an exception because other properties are not available. 
label1.Text = web.Title;
label1.Text = web. Description;

```


 <span data-ttu-id="f92c0-145">**Hinweis** Beim Versuch, auf andere Eigenschaften zuzugreifen, wird eine Ausnahme ausgelöst, weil keine anderen Eigenschaften verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="f92c0-145">**Note** If you try to access other properties, the code throws an exception because other properties are not available.</span></span>
 


### <a name="write-to-websites-properties"></a><span data-ttu-id="f92c0-146">Festlegen der Eigenschaften einer Website</span><span class="sxs-lookup"><span data-stu-id="f92c0-146">Write to website's properties</span></span>

<span data-ttu-id="f92c0-147">In diesem Beispiel wird gezeigt, wie Sie Eigenschaften einer Website festlegen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-147">This example shows how to write to the website's properties.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

web.Title = "New Title"; 
web.Description = "New Description"; 

// Note that the web.Update() does not trigger a request to the server
// because the client library until ExecuteQuery() is called. 
web.Update(); 

// Execute the query to server.
context.ExecuteQuery(); 

```


### <a name="create-a-new-sharepoint-website"></a><span data-ttu-id="f92c0-148">Erstellen einer neuen SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="f92c0-148">Create a new SharePoint website</span></span>

<span data-ttu-id="f92c0-p109">In diesem Beispiel wird gezeigt, wie Sie eine SharePoint-Website als untergeordnete Website der aktuellen Website erstellen. Verwenden Sie die  **WebCreationInformation** -Klasse zum Erstellen einer neuen Website. Zudem müssen Sie **using**-Anweisungen für  [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) und [System.Text](http://msdn2.microsoft.com/EN-US/library/x76y3wky) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p109">This example shows how to create a new SharePoint site as a subsite of the current website. Use the  **WebCreationInformation** class to create a new website. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Text](http://msdn2.microsoft.com/EN-US/library/x76y3wky) .</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

WebCreationInformation creation = new WebCreationInformation(); 
creation.Url = "web1"; 
creation.Title = "Hello web1"; 
Web newWeb = context.Web.Webs.Add(creation); 

// Retrieve the new web information. 
context.Load(newWeb, w => w.Title); 
context.ExecuteQuery(); 

label1.Text = newWeb.Title; 

```


## <a name="sharepoint-list-tasks"></a><span data-ttu-id="f92c0-152">SharePoint-Listenaufgaben</span><span class="sxs-lookup"><span data-stu-id="f92c0-152">SharePoint list tasks</span></span>
<span data-ttu-id="f92c0-153"><a name="BasicOps_SPListTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-153"></span></span>

<span data-ttu-id="f92c0-154">In diesen Beispielen wird gezeigt, wie Sie mit dem .NET Framework-CSOM Aufgaben ausführen, die Listen betreffen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-154">These examples show how to use the .NET Framework CSOM to complete list-related tasks.</span></span>
 

 

### <a name="retrieve-all-sharepoint-lists-in-a-web"></a><span data-ttu-id="f92c0-155">Abrufen aller SharePoint-Listen in einem Web</span><span class="sxs-lookup"><span data-stu-id="f92c0-155">Retrieve all SharePoint lists in a web</span></span>

<span data-ttu-id="f92c0-p110">In diesem Beispiel werden alle SharePoint-Listen in einer SharePoint-Website abgerufen. Zum Kompilieren dieses Codes müssen Sie eine **using**-Anweisung für  [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p110">This example retrieves all SharePoint lists in a SharePoint website. To compile this code you will need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) .</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// Retrieve all lists from the server. 
context.Load(web.Lists, 
             lists => lists.Include(list => list.Title, // For each list, retrieve Title and Id. 
                                    list => list.Id)); 

// Execute query. 
context.ExecuteQuery(); 

// Enumerate the web.Lists. 
foreach (List list in web.Lists) 
{ 
    label1.Text = label1.Text + ", " + list.Title; 
} 

```


 <span data-ttu-id="f92c0-p111">**Hinweis** Stattdessen können Sie den Rückgabewert mithilfe der **LoadQuery**-Methode auch in einer anderen Auflistung statt der **web.Lists**-Eigenschaft speichern. Zudem müssen Sie **using**-Anweisungen für  [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) und [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Fügen Sie der using-Anweisung für den **Microsoft.SharePoint.Client** -Namespace einen Alias hinzu, damit Sie unzweideutig auf die Klassen dieses Namespace verweisen können. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p111">**Note** Alternatively, you can use the **LoadQuery** method to store the return value in another collection, rather than use the **web.Lists** property. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the using statement for **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// Retrieve all lists from the server, and put the return value in another 
// collection instead of the web.Lists. 
IEnumerable<SP.List> result = context.LoadQuery(web.Lists.Include( // For each list, retrieve Title and Id.
                                                                   list => list.Title, 
                                                                   list => list.Id)); 

// Execute query. 
context.ExecuteQuery(); 

// Enumerate the result. 
foreach (List list in web.Lists) 
{ 
    label1.Text = label1.Text + ", " + list.Title; 
} 

```


### <a name="create-and-update-a-sharepoint-list"></a><span data-ttu-id="f92c0-162">Erstellen und Aktualisieren einer SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-162">Create and update a SharePoint list</span></span>

<span data-ttu-id="f92c0-163">In diesem Beispiel wird eine mithilfe der **ListCreationInformation**-Klasse SharePoint-Liste erstellt und aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="f92c0-163">This example creates a SharePoint list and updates it using the  **ListCreationInformation** class.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Title = "My List"; 
creationInfo.TemplateType = (int)ListTemplateType.Announcements; 
List list = web.Lists.Add(creationInfo); 
list.Description = "New Description"; 

list.Update(); 
context.ExecuteQuery(); 

```


### <a name="delete-a-sharepoint-list"></a><span data-ttu-id="f92c0-164">Löschen einer SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-164">Delete a SharePoint list</span></span>

<span data-ttu-id="f92c0-165">In diesem Beispiel wird eine SharePoint-Liste gelöscht.</span><span class="sxs-lookup"><span data-stu-id="f92c0-165">This example deletes a SharePoint list.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

List list = web.Lists.GetByTitle("My List"); 
list.DeleteObject(); 

context.ExecuteQuery();  

```


### <a name="add-a-field-to-a-sharepoint-list"></a><span data-ttu-id="f92c0-166">Hinzufügen eines Felds zu einer SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-166">Add a field to a SharePoint list</span></span>

<span data-ttu-id="f92c0-p112">In diesem Beispiel wird ein Feld zu einer SharePoint-Liste hinzugefügt. Fügen Sie der using-Anweisung für den  **Microsoft.SharePoint.Client** -Namespace einen Alias hinzu, damit Sie unzweideutig auf dessen Klassen verweisen können. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p112">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="f92c0-p113">**Hinweis** In diesem Beispiel wird mit **context.CastTo** eine Typumwandlung durchgeführt. Vor der Ausführung der Abfrage weiß die Clientbibliothek nicht, welchen Typ das zurückgegebene Objekt "field" eigentlich hat, und **SharePoint.Field** ist der einzig mögliche Typ. Wenn Sie den tatsächlichen Typ kennen, können Sie den Objekttyp mit der **ClientContext.CastTo<RealType>**-Methode umwandeln.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p113">**Note** The example uses **context.CastTo** to do a cast. Before executing the query, the client library does not know the real type of the returned object "field" and **SharePoint.Field** is the only possible type. If you know the real type, you can use the **ClientContext.CastTo<RealType>** method to cast the object.</span></span>
 


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Announcements"); 

SP.Field field = list.Fields.AddFieldAsXml("<Field DisplayName='MyField2' Type='Number' />", 
                                           true, 
                                           AddFieldOptions.DefaultValue); 
SP.FieldNumber fldNumber = context.CastTo<FieldNumber>(field); 
fldNumber.MaximumValue = 100; 
fldNumber.MinimumValue = 35; 
fldNumber.Update(); 

context.ExecuteQuery();  

```


## <a name="sharepoint-list-item-tasks"></a><span data-ttu-id="f92c0-173">SharePoint-Listenelementaufgaben</span><span class="sxs-lookup"><span data-stu-id="f92c0-173">SharePoint list item tasks</span></span>
<span data-ttu-id="f92c0-174"><a name="BasicOps_SPListItemTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-174"></span></span>

<span data-ttu-id="f92c0-175">In diesen Beispielen wird gezeigt, wie Sie das .NET Framework-CSOM zum Ausführen auf Listenelemente bezogener Aufgaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-175">These examples demonstrate how to use the .NET Framework CSOM to complete tasks that are related to list items.</span></span>
 

 

### <a name="retrieve-items-from-a-sharepoint-list"></a><span data-ttu-id="f92c0-176">Abrufen von Elementen aus einer SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-176">Retrieve items from a SharePoint list</span></span>

<span data-ttu-id="f92c0-p114">In diesem Beispiel werden die Elemente einer SharePoint-Liste abgerufen. Zudem müssen Sie eine **using**-Anweisung für  **Microsoft.SharePoint.Client.QueryExpression** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p114">This example retrieves the items in a SharePoint list. You will also need to add a **using** statement for **Microsoft.SharePoint.Client.QueryExpression** .</span></span>
 

 

 <span data-ttu-id="f92c0-179">**Hinweis** Sie können die **FolderServerRelativeUrl** -Eigenschaft verwenden, um die Elemente, die zurückgegeben werden, weiter auf die Elemente eines angegebenen Ordners zu beschränken.</span><span class="sxs-lookup"><span data-stu-id="f92c0-179">**Note** You can use the  **FolderServerRelativeUrl** property to further restrict the items that are returned to those in a specified folder.</span></span>
 


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// This creates a CamlQuery that has a RowLimit of 100, and also specifies Scope="RecursiveAll" 
// so that it grabs all list items, regardless of the folder they are in. 
CamlQuery query = CamlQuery.CreateAllItemsQuery(100); 
ListItemCollection items = announcementsList.GetItems(query); 

// Retrieve all items in the ListItemCollection from List.GetItems(Query). 
context.Load(items); 
context.ExecuteQuery(); 
foreach (ListItem listItem in items) 
{ 
    // We have all the list item data. For example, Title. 
    label1.Text = label1.Text + ", " + listItem["Title"]; 
} 

```


### <a name="create-a-new-list-item"></a><span data-ttu-id="f92c0-180">Erstellen eines neuen Listenelements</span><span class="sxs-lookup"><span data-stu-id="f92c0-180">Create a new list item</span></span>

<span data-ttu-id="f92c0-181">In diesem Beispiel wird ein neues SharePoint-Listenelement mit der **ListItemCreationInformation**-Klasse erstellt.</span><span class="sxs-lookup"><span data-stu-id="f92c0-181">This example creates a new SharePoint list item using the  **ListItemCreationInformation** class.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// We are just creating a regular list item, so we don't need to 
// set any properties. If we wanted to create a new folder, for 
// example, we would have to set properties such as 
// UnderlyingObjectType to FileSystemObjectType.Folder. 
ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation(); 
ListItem newItem = announcementsList.AddItem(itemCreateInfo); 
newItem["Title"] = "My New Item!"; 
newItem["Body"] = "Hello World!"; 
newItem.Update(); 

context.ExecuteQuery();  

```


### <a name="update-a-list-item"></a><span data-ttu-id="f92c0-182">Aktualisieren eines Listenelements</span><span class="sxs-lookup"><span data-stu-id="f92c0-182">Update a list item</span></span>

<span data-ttu-id="f92c0-183">In diesem Beispiel wird ein SharePoint-Listenelement aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="f92c0-183">This example updates a SharePoint list item.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// Assume there is a list item with ID=1. 
ListItem listItem = announcementsList.GetItemById(1); 

// Write a new value to the Body field of the Announcement item.
listItem["Body"] = "This is my new value!!"; 
listItem.Update(); 

context.ExecuteQuery();  

```


### <a name="delete-a-list-item"></a><span data-ttu-id="f92c0-184">Löschen eines Listenelements</span><span class="sxs-lookup"><span data-stu-id="f92c0-184">Delete a list item</span></span>

<span data-ttu-id="f92c0-185">In diesem Beispiel wird ein SharePoint-Listenelement gelöscht.</span><span class="sxs-lookup"><span data-stu-id="f92c0-185">This example deletes a SharePoint list item.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// Assume that there is a list item with ID=2. 
ListItem listItem = announcementsList.GetItemById(2); 
listItem.DeleteObject(); 

context.ExecuteQuery(); } 

```


## <a name="sharepoint-field-tasks"></a><span data-ttu-id="f92c0-186">SharePoint-Feldaufgaben</span><span class="sxs-lookup"><span data-stu-id="f92c0-186">SharePoint field tasks</span></span>
<span data-ttu-id="f92c0-187"><a name="BasicOps_SPFieldTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-187"></span></span>

<span data-ttu-id="f92c0-188">In diesen Beispielen wird gezeigt, wie Sie das SharePoint-.NET Framework-CSOM zum Ausführen auf Felder bezogener Aufgaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-188">These examples show how to use the SharePoint .NET Framework CSOM to complete field-related tasks.</span></span> 
 

 

### <a name="retrieve-all-of-the-fields-in-a-list"></a><span data-ttu-id="f92c0-189">Abrufen aller Felder einer Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-189">Retrieve all of the fields in a list</span></span>

<span data-ttu-id="f92c0-p115">In diesem Beispiel werden alle Felder aus einer SharePoint-Liste abgerufen. Sie müssen zudem der **using**-Anweisung für den **Microsoft.SharePoint.Client**-Namespace einen Alias hinzufügen, damit Sie unzweideutig auf dessen Klassen verweisen können; zum Beispiel `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p115">This example retrieves all of the fields in a SharePoint list. You will also need to add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously; for example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Shared Documents"); 
context.Load(list.Fields); 

// We must call ExecuteQuery before enumerate list.Fields. 
context.ExecuteQuery(); 

foreach (SP.Field field in list.Fields) 
{ 
    label1.Text = label1.Text + ", " + field.InternalName;
} 

```


### <a name="retrieve-a-specific-field-from-the-list"></a><span data-ttu-id="f92c0-192">Verweisen auf ein bestimmtes Feld der Liste</span><span class="sxs-lookup"><span data-stu-id="f92c0-192">Retrieve a specific field from the list</span></span>

<span data-ttu-id="f92c0-p116">Wenn Sie Informationen aus einem bestimmten Feld abrufen möchten, verwenden Sie die **Fields.GetByInternalNameOrTitle**-Methode. Diese Methode hat den Rückgabetyp **Field**. Vor der Ausführung der Abfrage weiß der Client nicht, welchen Typ das Objekt hat, und die C#-Syntax ist nicht zur Umwandlung des Objekttyps in den abgeleiteten Typ verfügbar. Daher wandeln Sie den Typ mit der **ClientContext.CastTo**-Methode um, welche die Clientbibliothek anweist, das Objekt neu zu erstellen. Zudem müssen Sie eine **using**-Anweisung für  [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) hinzufügen. Außerdem müssen Sie der **using**-Anweisung für den  **Microsoft.SharePoint.Client** -Namespace einen Alias hinzufügen, damit Sie eindeutig auf dessen Klassen verweisen können. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p116">If you want to retrieve information about a specific field, use the **Fields.GetByInternalNameOrTitle** method. The return type of this method is **Field**. Before the query is executed, the client does not know the type of object, and C# syntax is not available for casting it to the derived type. Therefore, use the **ClientContext.CastTo** method to cast it, which instructs the client library to recreate an object. You will also need to add a **using** statement for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) . You will also need to add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="f92c0-p117">**Hinweis** Die in diesem Beispiel verwendete **GetByInternalNameOrTitle**-Methode ist eine Remotemethode. Sie verwendet selbst dann nicht die Daten aus der Clientauflistung, wenn diese bereits Daten enthält.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p117">**Note** The  **GetByInternalNameOrTitle** method used in this example is a remote method. It does not use the data from the client collection even if the client collection is already populated.</span></span>
 


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Shared Documents"); 
SP.Field field = list.Fields.GetByInternalNameOrTitle("Title"); 
FieldText textField = context.CastTo<FieldText>(field); 
context.Load(textField); 
context.ExecuteQuery(); 

// Now, we can access the specific text field properties. 
label1.Text = textField.MaxLength; 

```


## <a name="sharepoint-user-tasks"></a><span data-ttu-id="f92c0-202">SharePoint-Benutzeraufgaben</span><span class="sxs-lookup"><span data-stu-id="f92c0-202">SharePoint user tasks</span></span>
<span data-ttu-id="f92c0-203"><a name="BasicOps_SPSecurityTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-203"></span></span>

<span data-ttu-id="f92c0-204">Sie können mithilfe des SharePoint-.NET Framework-CSOM SharePoint-Benutzer-, -Gruppen und -Benutzersicherheit verwalten.</span><span class="sxs-lookup"><span data-stu-id="f92c0-204">You can use the SharePoint .NET Framework CSOM to manage SharePoint users, groups, and user security.</span></span> 
 

 

### <a name="add-a-user-to-a-sharepoint-group"></a><span data-ttu-id="f92c0-205">Hinzufügen eines Benutzers zu einer SharePoint-Gruppe</span><span class="sxs-lookup"><span data-stu-id="f92c0-205">Add a user to a SharePoint group</span></span>

<span data-ttu-id="f92c0-206">In diesem Beispiel werden ein Benutzer und einige Benutzerinformationen einer SharePoint-Gruppe namens "Members" hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f92c0-206">This example adds a user and some user information to a SharePoint group named Members.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

GroupCollection siteGroups = context.Web.SiteGroups; 

// Assume that there is a "Members" group, and the ID=5. 
Group membersGroup = siteGroups.GetById(5); 

// Let's set up the new user info. 
UserCreationInformation userCreationInfo = new UserCreationInformation(); 
userCreationInfo.Email = "user@domain.com"; 
userCreationInfo.LoginName = "domain\\user"; 
userCreationInfo.Title = "Mr User"; 

// Let's add the user to the group. 
User newUser = membersGroup.Users.Add(userCreationInfo); 

context.ExecuteQuery();  

```


### <a name="retrieve-all-users-in-a-sharepoint-group"></a><span data-ttu-id="f92c0-207">Abrufen aller Benutzer einer SharePoint-Gruppe</span><span class="sxs-lookup"><span data-stu-id="f92c0-207">Retrieve all users in a SharePoint group</span></span>

<span data-ttu-id="f92c0-208">In diesem Beispiel werden Informationen zu allen Benutzern einer SharePoint-Gruppe namens "Members" abgerufen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-208">This example retrieves information about all users from a SharePoint group named Members.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

GroupCollection siteGroups = context.Web.SiteGroups; 

// Assume that there is a "Members" group, and the ID=5. 
Group membersGroup = siteGroups.GetById(5); 
context.Load(membersGroup.Users); 
context.ExecuteQuery(); 

foreach (User member in membersGroup.Users) 
{ 
    // We have all the user info. For example, Title. 
    label1.Text = label1.Text + ", " + member.Title; 
}  

```


### <a name="create-a-role"></a><span data-ttu-id="f92c0-209">Erstellen einer Rolle</span><span class="sxs-lookup"><span data-stu-id="f92c0-209">Create a role</span></span>

<span data-ttu-id="f92c0-210">In diesem Beispiel wird eine Rolle erstellt, die über Berechtigungen zum Erstellen und Verwalten von Benachrichtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="f92c0-210">This example creates a role that has create and manage alerts permissions.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

BasePermissions perm = new BasePermissions(); 
perm.Set(PermissionKind.CreateAlerts); 
perm.Set(PermissionKind.ManageAlerts); 

RoleDefinitionCreationInformation creationInfo = new RoleDefinitionCreationInformation(); 
creationInfo.BasePermissions = perm; 
creationInfo.Description = "A role with create and manage alerts permission"; 
creationInfo.Name = "Alert Manager Role"; 
creationInfo.Order = 0; 
RoleDefinition rd = context.Web.RoleDefinitions.Add(creationInfo); 

context.ExecuteQuery();  

```


### <a name="add-a-user-to-a-role"></a><span data-ttu-id="f92c0-211">Hinzufügen eines Benutzers zu einer Rolle</span><span class="sxs-lookup"><span data-stu-id="f92c0-211">Add a user to a role</span></span>

<span data-ttu-id="f92c0-212">In diesem Beispiel wird ein Benutzer einer Rolle hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f92c0-212">This example adds a user to a role.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that we have a SiteUser with Login user. 
Principal user = context.Web.SiteUsers.GetByLoginName(@"domain\user"); 

// Assume that we have a RoleDefinition named "Read". 
RoleDefinition readDef = context.Web.RoleDefinitions.GetByName("Read"); 
RoleDefinitionBindingCollection roleDefCollection = new RoleDefinitionBindingCollection(context); 
roleDefCollection.Add(readDef); 
RoleAssignment newRoleAssignment = context.Web.RoleAssignments.Add(user, roleDefCollection); 

context.ExecuteQuery();  

```


## <a name="rules-and-best-practices-for-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="f92c0-213">Regeln und bewährte Methoden für die Verwendung des SharePoint .NET-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="f92c0-213">Rules and best practices for using the SharePoint .NET client object model</span></span>
<span data-ttu-id="f92c0-214"><a name="Best"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-214"></span></span>

<span data-ttu-id="f92c0-215">In diesen Beispielen werden einige wichtige bewährte Methoden und Anforderungen veranschaulicht, die Sie bei Verwendung des SharePoint-.NET Framework-CSOM beachten müssen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-215">These examples illustrate some important best practices and requirements you should conform to when using the SharePoint .NET Framework CSOM.</span></span>
 

 

### <a name="call-clientcontextexecutequery-before-accessing-any-value-properties"></a><span data-ttu-id="f92c0-216">Aufrufen von ClientContext.ExecuteQuery vor dem Zugriff auf Werteigenschaften</span><span class="sxs-lookup"><span data-stu-id="f92c0-216">Call ClientContext.ExecuteQuery before accessing any value properties</span></span>

<span data-ttu-id="f92c0-p118">Im SharePoint .NET Framework-CSOM müssen Sie ein Programmiermuster im Stil von SQL verwenden: Sie deklarieren, was gewünscht ist, und führen die Abfrage aus, bevor Sie auf die Daten zugreifen. Beispielsweise löst der folgende Code, mit dem der Titel einer SharePoint-Website angezeigt werden soll, eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p118">The SharePoint .NET Framework CSOM requires that you use a SQL-like programming pattern: declare what you want and execute the query before you access the data. For example, the following code, attempts to display the SharePoint website's title, will throw an exception.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
label1.Text = web.Title;  

```

<span data-ttu-id="f92c0-219">Dieser Code verursacht einen Fehler, weil SharePoint .NET Framework-CSOM-Code folgende Aktionen ausführen muss:</span><span class="sxs-lookup"><span data-stu-id="f92c0-219">This code fails because SharePoint .NET Framework CSOM code must:</span></span>
 

 

1. <span data-ttu-id="f92c0-220">Entweder eine Ad-hoc-SQL-Abfrage oder eine gespeicherte Prozedur erstellen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-220">Build either an ad hoc SQL query or a stored procedure.</span></span>
    
 
2. <span data-ttu-id="f92c0-221">Die SQL-Abfrage ausführen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-221">Execute the SQL query.</span></span>
    
 
3. <span data-ttu-id="f92c0-222">Die Ergebnisse der SQL-Abfrage lesen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-222">Read results from SQL.</span></span>
    
 
<span data-ttu-id="f92c0-p119">Wenn Sie im SharePoint .NET Framework-CSOM eine Methode aufrufen, erstellen Sie eine Abfrage. Die Abfragen werden gesammelt und erst beim Aufruf von **ExecuteQuery** an den Server gesendet. Das folgende Beispiel enthält den Code, der erforderlich ist, um den Titel der Website anzuzeigen. Zudem müssen Sie eine **using**-Anweisung für [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Fügen Sie außerdem der **using**-Anweisung für den **Microsoft.SharePoint.Client** -Namespace einen Alias hinzu, damit Verweise auf Klassen dieses Namespace eindeutig sind. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p119">In SharePoint .NET Framework CSOM , when you call a method you build a query. Queries accumulate and are not sent to the server until  **ExecuteQuery** is called. The following example shows the code that is required to display the website's title. You will also need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 

context.Load(web, w => w.Title); 

context.ExecuteQuery(); 

label1.Text = web.Title;   

```

<span data-ttu-id="f92c0-229">Der Unterschied besteht in der Hinzufügung der folgenden Zeilen:</span><span class="sxs-lookup"><span data-stu-id="f92c0-229">The differences are the addition of these lines:</span></span>
 

 



```
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 

```

<span data-ttu-id="f92c0-p120">In der ersten Zeile wird eine Abfrage für die **Title**-Eigenschaft der Website erstellt. In der zweiten Zeile wird die Abfrage ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p120">The first line creates a query for the web's **Title** property. The second line executes the query.</span></span>
 

 

### <a name="do-not-use-value-objects-returned-from-methods-or-properties-in-the-same-query"></a><span data-ttu-id="f92c0-232">Von Methoden oder Eigenschaften zurückgegebene Wertobjekte dürfen nicht in derselben Abfrage verwendet werden</span><span class="sxs-lookup"><span data-stu-id="f92c0-232">Do not use value objects returned from methods or properties in the same query</span></span>

<span data-ttu-id="f92c0-p121">Wenn ein Wertobjekt von einer Methode oder Eigenschaft zurückgegeben wird, kann dieses Objekt erst verwendet werden, nachdem die Abfrage ausgeführt worden ist. Beispielsweise wird im folgenden Code versucht, eine SharePoint-Liste zu erstellen, die den gleichen Titel wie die übergeordnete Website hat. Der Code löst jedoch eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p121">When a value object is returned from a method or property, you cannot use that object until after you have executed the query. For example, the following code tries to create a SharePoint list that has the same title as the parent website, but it will throw an exception.</span></span> 
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Description = web.Title; 
creationInfo.Title = web.Title; 
List newList = web.Lists.Add(creationInfo);  

```

<span data-ttu-id="f92c0-p122">Es wird eine Ausnahme ausgelöst, weil die Eigenschaft vor der Ausführung der Abfrage nicht verfügbar ist. In SQL würden Sie eine lokale Variable erstellen, um den Wert für `web.Title` zu speichern, und diese lokale Variable dann zur Weberstellung verwenden. Die Clientbibliothek bietet nicht die Möglichkeit zur Erstellung lokaler Variablen. Sie müssen die Funktionalität in zwei getrennte Abfragen aufteilen, wie im folgenden Beispiel gezeigt. Zudem müssen Sie eine **using**-Anweisung für [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Fügen Sie außerdem der using-Anweisung für den **Microsoft.SharePoint.Client**-Namespace einen Alias hinzu, damit Verweise auf Klassen dieses Namespace eindeutig sind. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p122">An exception is thrown because the property is not available before you execute the query. In SQL, you would declare a local variable to hold the value for  `web.Title` and use the local variable for web creation. In the client library, you can't create a local variable. You have to split functionality into two separate queries as is shown in the following example. You will also need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the using statement for **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 

context.Load(web, w => w.Title); 

context.ExecuteQuery(); 

ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Description = web.Description; 
creationInfo.Title = web.Title; 
SP.List newList = web.Lists.Add(creationInfo); 

context.ExecuteQuery();  

```

<span data-ttu-id="f92c0-242">Unterschiedlich sind die folgenden drei Zeilen:</span><span class="sxs-lookup"><span data-stu-id="f92c0-242">The difference is the following three lines:</span></span>
 

 



```C#
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 
...
context.ExecuteQuery(); 

```


### <a name="using-methods-or-properties-that-return-client-objects-in-another-method-call-in-the-same-query"></a><span data-ttu-id="f92c0-243">Verwenden von Methoden oder Eigenschaften, die Clientobjekte zurückgeben, in einem anderen Methodenaufruf derselben Abfrage</span><span class="sxs-lookup"><span data-stu-id="f92c0-243">Using methods or properties that return client objects in another method call in the same query</span></span>

<span data-ttu-id="f92c0-244">Im Gegensatz zu Wertobjekten können Clientobjekte in einem anderen Methodenaufruf derselben Abfrage verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-244">Unlike a value object, a client object can be used in another method call in the same query.</span></span> 
 

 
<span data-ttu-id="f92c0-p123">In .NET Remoting ist das Wertobjekt eine Klasse oder eine Struktur, die nach dem Wert gemarshallt wird, während ein Clientobjekt eine Klasse oder Struktur darstellt, die nach dem Verweis gemarshallt wird. Beispielsweise ist **ListItem** ein Clientobjekt, und **UrlFieldValue** und andere Feldwerte sind dagegen Wertobjekte.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p123">In .NET remoting, the value object is a class or struct that is marshaled by value, while the client object is a class or struct that is marshaled by reference. For example, the **ListItem** is a client object, while the **UrlFieldValue** and other field values are value objects.</span></span>
 

 
<span data-ttu-id="f92c0-p124">In der Clientbibliothek verfügt das entsprechende Serverobjekt über das  `[ClientCallable(ValueObject = true)]`-Attribut. Diese Werte können nur Eigenschaften und keine Methoden besitzen. Einfache Typen, wie beispielsweise Zeichenfolgen und Ganzzahlen, werden wie Wertobjekte behandelt. Alle Werte werden zwischen Client und Server gemarshallt. Der Standardwert von **ValueObject** lautet **false**.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p124">In the client library, the corresponding server object has the  `[ClientCallable(ValueObject = true)]` attribute. Those values could have only properties and no methods. Primitive types, such as strings and ints, are treated as value objects. All the values are marshaled between the client and the server. The default value of the **ValueObject** is **false**.</span></span> 
 

 
<span data-ttu-id="f92c0-p125">Das Clientobjekt ist das Gegenstück zum Wertobjekt. Wenn das entsprechende Serverobjekt über das **[ClientCallable(ValueObject = false)]**-Attribut verfügt, ist das Objekt ein Clientobjekt. Bei Clientobjekten wird verfolgt, wie das Objekt erstellt wird; dies wird in der Clientbibliotheksimplementierung als **ObjectPath** bezeichnet. Wenn beispielsweise Code wie der Folgende vorliegt:</span><span class="sxs-lookup"><span data-stu-id="f92c0-p125">The counterpart to the value object is the client object. If the corresponding server object has the **[ClientCallable(ValueObject = false)]** attribute, the object is a client object. For client objects, we keep track of how the object is created; this is called **ObjectPath** in the client library implementation. For example, if we have code like the following:</span></span>
 

 



```C#
ClientContext context = new ClientContext("http://SiteUrl"); 
Web web = context.Web; 
SP.List list = web.Lists.GetByTitle("Announcements"); 

```

<span data-ttu-id="f92c0-256">Wir wissen, dass die Liste wie folgt erstellt wird:</span><span class="sxs-lookup"><span data-stu-id="f92c0-256">We know that the list is created by:</span></span>
 

 

- <span data-ttu-id="f92c0-257">Abrufen der **Web**-Eigenschaft aus dem Kontext.</span><span class="sxs-lookup"><span data-stu-id="f92c0-257">Getting the **Web** property from the context.</span></span>
    
 
- <span data-ttu-id="f92c0-258">Abrufen der **Lists**-Eigenschaft aus dem obigen Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="f92c0-258">Getting the **Lists** property from the above result.</span></span>
    
 
- <span data-ttu-id="f92c0-259">Aufrufen der **GetByTitle**-Methode mit dem _Announcements_-Parameter aus dem obigen Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="f92c0-259">Invoking the **GetByTitle** method with the _Announcements_ parameter from the above result.</span></span>
    
 
<span data-ttu-id="f92c0-p126">Wenn das SharePoint .NET Framework-CSOM diese Informationen an den Server übergibt, können Sie das Objekt auf dem Server neu erstellen. In der Clientbibliothek können Sie den **ObjectPath** der Clientobjekterstellung verfolgen. Weil Sie wissen, wie das Objekt erstellt wird, können Sie das Objekt als Parameter zum Aufruf anderer Methoden innerhalb derselben Abfrage verwenden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p126">When the SharePoint .NET Framework CSOM passes this information to the server, you can recreate the object on the server. In the client library, you can keep track of the **ObjectPath** that the client object is created. Because you know how the object is created, you could use the object as a parameter to invoke other methods within the same query.</span></span>
 

 

### <a name="group-data-retrieval-on-the-same-object-together-to-improve-performance"></a><span data-ttu-id="f92c0-263">Gruppieren des Abrufs von Daten vom selben Objekt zur Optimierung der Leistung</span><span class="sxs-lookup"><span data-stu-id="f92c0-263">Group data retrieval on the same object together to improve performance</span></span>

<span data-ttu-id="f92c0-p127">Wenn verschiedene Datenelemente aus demselben Objekt gelesen werden, sollten Sie versuchen, alle Daten in einer Abfrage zu erfassen, d. h. in einem Aufruf der **Load<T>(T, [])**-Methode. Im folgenden Code werden zwei Möglichkeiten gezeigt, wie der Titel und die Beschreibung einer Website und die Beschreibung der Liste **Announcements** abgerufen werden können. Zum Kompilieren dieses Codes müssen Sie eine **using**-Anweisung für  [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Fügen Sie außerdem der using-Anweisung **statement** für den **Microsoft.SharePoint.Client** -Namespace einen Alias hinzu, damit Verweise auf Klassen dieses Namespace eindeutig sind. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p127">When reading multiple pieces of data from the same object, you should try to get all of it in a single query; that is, a single call to the **Load<T>(T, [])** method. The following code shows two ways to retrieve a website's title and description and the **Announcements** list's description. To compile this code, you need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the using **statement** for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span> 
 

 

```C#

static void Method1() 
{ 
    ClientContext context = new ClientContext("http://SiteUrl"); 
    Web web = context.Web; 
    SP.List list = web.Lists.GetByTitle("Announcements"); 
    context.Load(web, w => w.Title, w => w.Description); 
    context.Load(list, l => l.Description); 
    context.ExecuteQuery(); 
} 

static void Method2() 
{ 
    ClientContext context = new ClientContext("http://SiteUrl"); 
    Web web = context.Web; 
    SP.List list = web.Lists.GetByTitle("Announcements"); 
    context.Load(web, w => w.Title); 
    context.Load(list, l => l.Description); 
    context.Load(web, w => w.Description); 
    context.ExecuteQuery();  
} 

```

<span data-ttu-id="f92c0-p128">Diese Methoden sind nicht gleich effizient. In **Method1** wurde der Code zum Abrufen des Titels und der Beschreibung der Website zusammen gruppiert. In **Method2** wird der Code zum Abrufen des Titels und der Beschreibung der Website durch andere Aktionen unterbrochen. Daher löst **Method2** zwei getrennte Abfragen für dasselbe Webobjekt aus, und es werden zwei Ergebnismengen für dasselbe Web erzeugt. Weil die Clientbibliothek versucht, konsistente Daten zurückzugeben, enthält die zweite Ergebnismenge sowohl den Titel als auch die Beschreibung. Der obige Code lässt sich auch so darstellen.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p128">These are not equally efficient. In **Method1**, the code to retrieve the web's title and description is grouped together. In **Method2**, the code to retrieve the web's title and description is separated by other actions. This means that **Method2** will trigger two separated queries on the same web object, and there will be two result sets for the same web. Because the client library tries to return consistent data, the second result set will include both the title and description. You could think of the previous code as the following.</span></span>
 

 



```
Method1: 
SELECT Title, Description FROM Webs WHERE ... 
SELECT Description FROM Lists WHERE … 

Method2: 
SELECT Title FROM Webs WHERE … 
SELECT Description FROM Lists WHERE … 
SELECT Title, Description FROM Webs WHERE … 

```


### <a name="specify-which-properties-of-objects-you-want-to-return"></a><span data-ttu-id="f92c0-275">Angeben, welche Objekteigenschaften zurückgegeben werden sollen</span><span class="sxs-lookup"><span data-stu-id="f92c0-275">Specify which properties of objects you want to return</span></span>

<span data-ttu-id="f92c0-p129">Im SharePoint-Serverobjektmodell können alle Eigenschaften eines **SPWeb**-Objekts untersucht werden. Um in SQL alle Spalten einer Tabelle zu erhalten, können Sie folgende Anweisung ausführen:</span><span class="sxs-lookup"><span data-stu-id="f92c0-p129">In the SharePoint server object model, if you get an **SPWeb** object, you can inspect all of its properties. In SQL, to get all of the columns of a table you can run:</span></span>
 

 

```
SELECT * FROM Webs 
```

<span data-ttu-id="f92c0-p130">In der Clientbibliothek gibt weder **Load<T>** noch irgend eine andere Methode alle Eigenschaften zurück. Sie müssen daher explizit angeben, was zurückgegeben werden soll. Beispielsweise wird im folgenden Code das Websiteobjekt ohne Angabe der gewünschten Eigenschaften abgerufen. Dann wird versucht, zwei Eigenschaften zu lesen, und eine Eigenschaft ist nicht unter den Eigenschaften, die von **Load** automatisch zurückgegeben werden. Dieser Code löst eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p130">In the client library, neither **Load<T>** nor any other method returns all properties, so you have to explicitly specify what you want. For example, the following code retrieves the website object without specifying which properties to return. It then tries to read two properties and one of them is not among the properties that is automatically returned by **Load**. This code throws an exception.</span></span> 
 

 



```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
context.Load(web); 
context.ExecuteQuery(); 

Console.WriteLine(web.Title); 
Console.WriteLine(web.HasUniqueRoleAssignments);  

```

 <span data-ttu-id="f92c0-p131">Damit der Code erfolgreich kompiliert wird, müssen Sie ihn wie folgt aktualisieren. Sie müssen eine **using**-Anweisung für [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Fügen Sie außerdem der **using**-Anweisung für den **Microsoft.SharePoint.Client**-Namespace einen Alias hinzu, damit Verweise auf Klassen dieses Namespace eindeutig sind. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p131">To get the code to compile successfully, update it to the following. To compile this code, you need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
context.Load(web); 
context.Load(web, web => web.HasUniqueRoleAssignments); 
context.ExecuteQuery(); 

Console.WriteLine(web.Title); 
Console.WriteLine(web.HasUniqueRoleAssignments);  

```


### <a name="use-conditional-scope-to-test-for-preconditions-before-loading-data"></a><span data-ttu-id="f92c0-286">Verwenden eines bedingten Bereichs zum Testen von Vorbedingungen vor dem Laden von Daten</span><span class="sxs-lookup"><span data-stu-id="f92c0-286">Use conditional scope to test for preconditions before loading data</span></span>

<span data-ttu-id="f92c0-p132">Zur bedingten Ausführung von Code legen Sie unter Verwendung eines **ConditionalScope**-Objekts einen bedingten Bereich fest. Sie rufen beispielsweise die Listeneigenschaft ab, wenn die Liste nicht leer ist. Zudem müssen Sie **using**-Anweisungen für  [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) und [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) hinzufügen. Außerdem müssen Sie der **using**-Anweisung für den  **Microsoft.SharePoint.Client** -Namespace einen Alias hinzufügen, damit Sie eindeutig auf die Klassen dieses Namespace verweisen können. Beispiel: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p132">To conditionally execute code, set a conditional scope by using a  **ConditionalScope** object. For example, retrieve the list property when the list is not null. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768) . Also, add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="f92c0-p133">**Hinweis** Es ist nicht zulässig, in einem bedingten Bereich Methoden aufzurufen und Eigenschaften festzulegen, weil die Clientbibliothek die Nebenwirkungen der Methodenaufrufe und Eigenschafteneinstellungen nicht verfolgen kann. Im bedingten Bereich sollten Sie nur **Load** verwenden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p133">**Note** Calling method and setting properties within a conditional scope are not permitted, because the client library does not track the side effects of method calls and property settings. You should use only **Load** inside the conditional scope.</span></span>
 


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.GetCatalog(ListTemplateType.WebPartCatalog); 
BasePermissions perm = new BasePermissions(); 
perm.Set(PermissionKind.ManageLists); 

ConditionalScope scope = 
    new ConditionalScope(context, 
                         () => list.ServerObjectIsNull &amp;&amp; context.Web.DoesUserHavePermissions(perm).Value); 
using (scope.StartScope()) 
{ 
    context.Load(list, l => l.Title); 
} 
context.ExecuteQuery(); 

label1.Text = scope.TestResult.Value; 

if (scope.TestResult.Value) 
{ 
    label1.Text = list.Title; 
}  

```


### <a name="use-an-exception-handling-scope-to-catch-exceptions"></a><span data-ttu-id="f92c0-294">Verwenden eines Ausnahmebehandlungsbereichs zum Abfangen von Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="f92c0-294">Use an exception handling scope to catch exceptions</span></span>

<span data-ttu-id="f92c0-p134">In diesem Beispiel wird gezeigt, wie Sie mit einem  **ExceptionHandlingScope** -Objekt einen Ausnahmebehandlungsbereich erstellen und verwenden. In diesem Szenario soll die Beschreibung einer Liste aktualisiert und die Ordnererstellung ermöglicht werden. Die Liste ist möglicherweise nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="f92c0-p134">This example shows how to create and use an exception handling scope with an  **ExceptionHandlingScope** object. The scenario is to update the description of a list and also enable folder creation. There is a possibility that the list might not exist.</span></span>
 

 

```C#


// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

ExceptionHandlingScope scope = new ExceptionHandlingScope(context); 

using (scope.StartScope()) 
{ 
    using (scope.StartTry()) 
    { 
        List fooList = context.Web.Lists.GetByTitle("Sample"); 
        fooList.Description = "In Try Block"; 
        fooList.Update(); 
    } 
    using (scope.StartCatch()) 
    { 
        // Assume that if there's an exception, 
        // it can be only because there was no "Sample" list. 
        ListCreationInformation listCreateInfo = new ListCreationInformation(); 
        listCreateInfo.Title = "Sample"; 
        listCreateInfo.Description = "In Catch Block"; 
        listCreateInfo.TemplateType = (int)ListTemplateType.Announcements; 
        List fooList = context.Web.Lists.Add(listCreateInfo); 
    } 
    using (scope.StartFinally()) 
    { 
        List fooList = context.Web.Lists.GetByTitle("Sample"); 
        fooList.EnableFolderCreation = true; 
        fooList.Update(); 
    } 
} 

context.ExecuteQuery();  

```


## <a name="additional-resources"></a><span data-ttu-id="f92c0-298">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f92c0-298">Additional resources</span></span>
<span data-ttu-id="f92c0-299"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f92c0-299"></span></span>


-  [<span data-ttu-id="f92c0-300">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f92c0-300">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="f92c0-301">Entwickeln von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f92c0-301">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f92c0-302">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f92c0-302">Build sites for SharePoint</span></span>](http://msdn.microsoft.com/library/3b372a63-7cdf-462a-abb4-750e611e967d%28Office.15%29.aspx)
    
 

