---
title: Such-API-Verwendung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c4ad4850f8e76ddf2933981ce550a141bf75d792
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="search-api-usage-in-the-sharepoint-add-in-model"></a><span data-ttu-id="21394-102">Such-API-Verwendung in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="21394-102">Search API usage in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="21394-103">Summary</span><span class="sxs-lookup"><span data-stu-id="21394-103">Summary</span></span>
-------

<span data-ttu-id="21394-104">Ansatz verwenden Sie zum Ausführen der Suche mit den SharePoint-Suchdienst unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="21394-104">The approach you take to execute searches with the SharePoint Search Service is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="21394-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, das SharePoint Server-Side-Objektmodell (vom Webpart für Inhaltsabfragen Außerkraftsetzungen) oder die Search-Webdienste wurden auszuführenden Suche mit den SharePoint-Suchdienst verwendet.</span><span class="sxs-lookup"><span data-stu-id="21394-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the SharePoint server-side object model (Content By Query Web Part overrides) or the Search Web Services were used to execute searches with the SharePoint Search Service.</span></span>

<span data-ttu-id="21394-106">In einem Szenario mit SharePoint-Add-Ins Modell führen Sie Suchvorgänge mit der SharePoint Search-Dienst über das CSOM oder den REST-APIs.</span><span class="sxs-lookup"><span data-stu-id="21394-106">In a SharePoint Add-in model scenario, you execute searches with the SharePoint Search Service via the CSOM or REST APIs.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="21394-107">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="21394-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="21394-108">In der Regel von einer Ziehpunkt möchten wir bieten die folgenden high Level Richtlinien zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="21394-108">As a rule of a thumb, we would like to provide the following high level guidelines to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="21394-109">Verwendung AppOnly ist Authentifizierung nicht für alle Vorgänge Search-Dienst unterstützt.</span><span class="sxs-lookup"><span data-stu-id="21394-109">Using AppOnly authentication is not supported for any Search Service operations.</span></span>
    + <span data-ttu-id="21394-110">Dies ist daran so, dass der Suchdienst greift auf User Profile Service (USV), um Benutzerprofilinformationen zu suchen und die USV AppOnly-Authentifizierung nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="21394-110">This is due to the fact that the Search Service accesses the User Profile Service (UPS) to search user profile information and the UPS does not support AppOnly authentication.</span></span>
    + <span data-ttu-id="21394-111">Aus diesem Grund, da die Relevanz und andere Aspekte der Suche hängen von einem bestimmten Benutzer und deren Profil Attribute der AppOnly authentifizierungsmuster nicht funktionieren.</span><span class="sxs-lookup"><span data-stu-id="21394-111">Therefore, because search relevance and other search facets depend on a given user and their profile attributes the AppOnly authentication pattern will not work.</span></span>

<a name="options-to-execute-searches-with-the-sharepoint-search-service"></a><span data-ttu-id="21394-112">Optionen zum Ausführen der Suche mit den SharePoint-Suchdienst</span><span class="sxs-lookup"><span data-stu-id="21394-112">Options to execute searches with the SharePoint Search Service</span></span>
--------------------------------------------------------------

<span data-ttu-id="21394-113">Sie haben eine Coupé der Optionen zum Suchen mit den SharePoint-Suchdienst ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-113">You have a coupe of options to execute searches with the SharePoint Search Service.</span></span>

- <span data-ttu-id="21394-114">.NET CSOM-API</span><span class="sxs-lookup"><span data-stu-id="21394-114">.Net CSOM API</span></span>
- <span data-ttu-id="21394-115">JavaScript-CSOM (JSOM)-API</span><span class="sxs-lookup"><span data-stu-id="21394-115">JavaScript CSOM (JSOM) API</span></span>
- <span data-ttu-id="21394-116">REST-API</span><span class="sxs-lookup"><span data-stu-id="21394-116">REST API</span></span>  

<a name="net-csom-api"></a><span data-ttu-id="21394-117">.NET CSOM-API</span><span class="sxs-lookup"><span data-stu-id="21394-117">.Net CSOM API</span></span>
-------------
<span data-ttu-id="21394-118">Bei dieser Option verwenden Sie die .net CSOM-API sucht mit den SharePoint-Suchdienst ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-118">In this option you use the .Net CSOM API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="21394-119">Diese API ist nur verfügbar in verwaltetem.</span><span class="sxs-lookup"><span data-stu-id="21394-119">This API is only available in managed .Net code.</span></span>


<span data-ttu-id="21394-120">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="21394-120">**When is it a good fit?**</span></span>

- <span data-ttu-id="21394-121">Diese API ist eine optimale Lösung für vom Anbieter gehosteten-Add-ins, lange ausgeführte Vorgänge oder andere serverseitige Szenarien, die auf die .net Plattform ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-121">This API is a great fit for Provider-hosted Add-ins, long running operations, or other server-side scenarios that run on the .Net platform.</span></span>
- <span data-ttu-id="21394-122">Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, ASP.NET Web-API-Diensten, .net-Verwaltungskonsole oder Windows-Anwendungen und Azure Web, stellen.</span><span class="sxs-lookup"><span data-stu-id="21394-122">Some examples of these scenarios are ASP.NET MVC web sites, ASP.NET Web API services, .Net console or Windows applications, and Azure Web Jobs.</span></span>

<span data-ttu-id="21394-123">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="21394-123">**Getting Started**</span></span>

<span data-ttu-id="21394-124">Das folgende Beispiel veranschaulicht, wie Sie mit der SharePoint-Suchdienst mit der .net CSOM-API sucht ausführen.</span><span class="sxs-lookup"><span data-stu-id="21394-124">The following sample demonstrates how to execute searches with the SharePoint Search Service with the .Net CSOM API.</span></span>  <span data-ttu-id="21394-125">Darüber hinaus wird veranschaulicht, wie auf Profil eines Benutzers, um die Suchergebnisse zu personalisieren zugreifen.</span><span class="sxs-lookup"><span data-stu-id="21394-125">This example also demonstrates how to access a user's profile to personalize the search results.</span></span>

- [<span data-ttu-id="21394-126">Search.PersonalizedResults (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="21394-126">Search.PersonalizedResults (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)

![Die API für die Suche und Personalisierung-Seite.](media/Recipes/SearchAPI/Search.PersonalizedResults.png)

<span data-ttu-id="21394-137">[Zum Ausführen von personalisierten Suchabfragen mit CSOM (O365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) führt Sie durch die [Search.PersonalizedResults (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).</span><span class="sxs-lookup"><span data-stu-id="21394-137">The [How to perform personalized search queries with CSOM (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) walks you through the [Search.PersonalizedResults (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).</span></span>

<span data-ttu-id="21394-138">Die **BtnPerformSearch_Click** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) führt eine Suche nach der Textwert, den der Benutzer in das Suchfeld eingibt, und legt den Suchbereich auf alle Inhalte, die in einer Websitesammlung gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="21394-138">The **btnPerformSearch_Click** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) executes a search for the text value the user enters into the search box and scopes the search to all content that is stored in a site collection.</span></span>  <span data-ttu-id="21394-139">Die Contentclass: "STS_Site"-Parameter schränkt den Suchbereich für Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="21394-139">The contentclass:"STS_Site" parameter limits the search scope to site collections.</span></span>

    protected void btnPerformSearch_Click(object sender, EventArgs e)
    {
        var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            // Since in this case we want only site collections, let's filter based on result type
            string query = searchtext.Text + " contentclass:\"STS_Site\"";
            ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
            lblStatus1.Text = FormatResults(results);
        }
    }

<span data-ttu-id="21394-140">Die **BtnPersonalizedSearch_Click** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) führt die gleiche Suche aus, wie die BtnPerformSearch_Click-Methode ist und fügt außerdem einen weiteren Parameter basierend auf dem aktuellen Profil des Benutzers hinzu.</span><span class="sxs-lookup"><span data-stu-id="21394-140">The **btnPersonalizedSearch_Click** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) executes the same search as the btnPerformSearch_Click method does and also adds an additional parameter based on the current user's profile.</span></span>  <span data-ttu-id="21394-141">Die PeopleManager-Klasse wird verwendet, um Benutzerprofileigenschaften für den aktuellen Benutzer zugreifen.</span><span class="sxs-lookup"><span data-stu-id="21394-141">The PeopleManager class is used to access the current user's profile properties.</span></span>

    protected void btnPersonalizedSearch_Click(object sender, EventArgs e)
    {
        var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            // Load user profile properties
            PeopleManager peopleManager = new PeopleManager(clientContext);
            PersonProperties personProperties = peopleManager.GetMyProperties();
            clientContext.Load(personProperties);
            clientContext.ExecuteQuery();
            // Check teh value for About Me to investigate current values
            string aboutMeValue = personProperties.UserProfileProperties["AboutMe"];
            string templateFilter = ResolveAdditionalFilter(aboutMeValue);
            // Let's build the query
            string query = "contentclass:\"STS_Site\" " + templateFilter;
            ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
            lblStatus2.Text = FormatResults(results);
        }
    }

<span data-ttu-id="21394-142">Die **ResolveAdditionalFilter** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) ausgewertet wird der aktuelle von Benutzerprofileigenschaften und gibt einen entsprechenden Suchparameter zurück.</span><span class="sxs-lookup"><span data-stu-id="21394-142">The **ResolveAdditionalFilter** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) evaluates the current user's profile properties and returns an applicable search parameter.</span></span> <span data-ttu-id="21394-143">In diesem Beispiel enthält die Benutzerprofileigenschaft AboutMeValue Apptesten und klicken Sie dann die Suchparameter WebTemplate = STS wird zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="21394-143">In this example, if the aboutMeValue user profile property contains AppTest then the search parameter WebTemplate=STS is returned.</span></span>  <span data-ttu-id="21394-144">Dieser Parameter beschränkt den Suchbereich auf Websites, die mit der Vorlage STS (Teamwebsite) erstellt.</span><span class="sxs-lookup"><span data-stu-id="21394-144">This parameter limits the search scope to sites built with the STS (Team Site) template.</span></span>
 
    private string ResolveAdditionalFilter(string aboutMeValue)
    {
        if (!aboutMeValue.Contains("AppTest"))
        {
            return "WebTemplate=STS";
        }
        
        return "";
    }

<span data-ttu-id="21394-145">In beiden Fällen verwendet die **ProcessQuery** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) die SearchExecutor-Klasse die Search-Abfrage ausführen und die Ergebnisse zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="21394-145">In both cases, the **ProcessQuery** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) uses the SearchExecutor class to execute the search query and return the results.</span></span> 

    private ClientResult<ResultTableCollection> ProcessQuery(ClientContext ctx, string keywordQueryValue)
    {
        KeywordQuery keywordQuery = new KeywordQuery(ctx);
        keywordQuery.QueryText = keywordQueryValue;
        keywordQuery.RowLimit = 500;
        keywordQuery.StartRow = 0;
        keywordQuery.SelectProperties.Add("Title");
        keywordQuery.SelectProperties.Add("SPSiteUrl");
        keywordQuery.SelectProperties.Add("Description");
        keywordQuery.SelectProperties.Add("WebTemplate");
        keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
        SearchExecutor searchExec = new SearchExecutor(ctx);
        ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
        ctx.ExecuteQuery();
        return results;
    }

<a name="javascript-csom-jsom-api"></a><span data-ttu-id="21394-146">JavaScript-CSOM (JSOM)-API</span><span class="sxs-lookup"><span data-stu-id="21394-146">JavaScript CSOM (JSOM) API</span></span>
--------------------------
<span data-ttu-id="21394-147">Bei dieser Option verwenden Sie die JavaScript CSOM (JSOM) API sucht mit den SharePoint-Suchdienst ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-147">In this option you use the JavaScript CSOM (JSOM) API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="21394-148">Diese API ist nur verfügbar in clientseitige JavaScript-Code.</span><span class="sxs-lookup"><span data-stu-id="21394-148">This API is only available in client-side JavaScript code.</span></span>

<span data-ttu-id="21394-149">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="21394-149">**When is it a good fit?**</span></span>

- <span data-ttu-id="21394-150">Diese API ist eine optimale Lösung für SharePoint-Hosting-Add-ins und vom Anbieter gehosteten-Add-ins, die auf eine beliebige Webplattform ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-150">This API is a great fit for SharePoint-hosted Add-ins and Provider-hosted Add-ins running on any web platform.</span></span>
- <span data-ttu-id="21394-151">Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, PHP-Websites, Websites Python.</span><span class="sxs-lookup"><span data-stu-id="21394-151">Some examples of these scenarios are ASP.NET MVC web sites, PHP web sites, Python web sites, etc.</span></span>

<span data-ttu-id="21394-152">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="21394-152">**Getting Started**</span></span>

<span data-ttu-id="21394-153">Im folgenden Codebeispiel wird veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit dem JavaScript CSOM (JSOM) API ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="21394-153">The following code example demonstrates how to execute searches with the SharePoint Search Service with the JavaScript CSOM (JSOM) API.</span></span>  <span data-ttu-id="21394-154">Dieses Beispiel führt eine Suche für alle Elemente, die den Begriff "Blizzard" enthalten.</span><span class="sxs-lookup"><span data-stu-id="21394-154">This example executes a search for all items that contain the term 'Blizzard'.</span></span>

    var context = SP.ClientContext.get_current();
    
    var keywordQuery = 
    new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
    
    keywordQuery.set_queryText("Blizzard");
    
    var searchExecutor = 
    new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
    
    results = searchExecutor.executeQuery(keywordQuery);
    
    context.executeQueryAsync(onGetEventsSuccess, onGetEventsFail);

<a name="rest-api"></a><span data-ttu-id="21394-155">REST-API</span><span class="sxs-lookup"><span data-stu-id="21394-155">REST API</span></span>
--------
<span data-ttu-id="21394-156">Bei dieser Option verwenden Sie die REST-API sucht mit den SharePoint-Suchdienst ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-156">In this option you use the REST API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="21394-157">Diese API ist flexibelsten, da es im serverseitige und clientseitige Code verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="21394-157">This API is the most flexible because it is available in both server-side and client-side code.</span></span>
- <span data-ttu-id="21394-158">Der REST-API für SharePoint Search Service-Stamm-Endpunkt ist:</span><span class="sxs-lookup"><span data-stu-id="21394-158">The SharePoint Search Service REST API root endpoint is:</span></span>
    + <span data-ttu-id="21394-159">https://<tenant>/site/_api/search/query</span><span class="sxs-lookup"><span data-stu-id="21394-159">https://<tenant>/site/_api/search/query</span></span>
- <span data-ttu-id="21394-160">Es folgen einige einfache Beispiele:</span><span class="sxs-lookup"><span data-stu-id="21394-160">Here are some simple examples:</span></span>
    + <span data-ttu-id="21394-161">Stichwortsuche</span><span class="sxs-lookup"><span data-stu-id="21394-161">Keyword search</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='{Apples}'
        ```
    + <span data-ttu-id="21394-162">Bestimmte Eigenschaften auswählen</span><span class="sxs-lookup"><span data-stu-id="21394-162">Selecting specific properties</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='test'&selectproperties='Rank, Title'
        ```
    + <span data-ttu-id="21394-163">Die Sortierung</span><span class="sxs-lookup"><span data-stu-id="21394-163">Sorting</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='Oranges'&sortlist='LastModifiedTime:ascending'
        ```

<span data-ttu-id="21394-164">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="21394-164">**When is it a good fit?**</span></span>

<span data-ttu-id="21394-165">Diese API ist eine optimale Lösung für SharePoint-Hosting-Add-ins und vom Anbieter gehosteten-Add-ins, die auf eine beliebige Webplattform ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="21394-165">This API is a great fit for SharePoint-hosted Add-ins and Provider-hosted Add-ins running on any web platform.</span></span>
- <span data-ttu-id="21394-166">Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, PHP-Websites, Python-Websites, ASP.NET Web-API-Diensten, .net-Verwaltungskonsole oder Windows Azure Webaufträge, Applications usw..</span><span class="sxs-lookup"><span data-stu-id="21394-166">Some examples of these scenarios are ASP.NET MVC web sites, PHP web sites, Python web sites, ASP.NET Web API services, .Net console or Windows applications, Azure Web Jobs, etc.</span></span>

<span data-ttu-id="21394-167">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="21394-167">**Getting Started**</span></span>

<span data-ttu-id="21394-168">**Serverseitige Option**</span><span class="sxs-lookup"><span data-stu-id="21394-168">**Server-side Option**</span></span>

<span data-ttu-id="21394-169">Das folgende Beispiel veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit der REST-API von verwaltetem ausführen.</span><span class="sxs-lookup"><span data-stu-id="21394-169">The following sample demonstrates how to execute searches with the SharePoint Search Service with the REST API from managed .Net code.</span></span>

- [<span data-ttu-id="21394-170">EmployeeDirectory (OfficeDev Schulungsinhalte)</span><span class="sxs-lookup"><span data-stu-id="21394-170">EmployeeDirectory (OfficeDev Training Content)</span></span>](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)

<span data-ttu-id="21394-171">Die **Index** -Methode in der [Klasse HomeController.cs](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) führt eine Suche für alle Benutzer, deren Nachname mit dem Text beginnt, der Benutzer klickt auf Wert.</span><span class="sxs-lookup"><span data-stu-id="21394-171">The **Index** method in the [HomeController.cs class](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) executes a search for  all users whose last name begins with the text value the user clicks.</span></span>

    var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    string accessToken = spContext.UserAccessTokenForSPHost;

    //Build the REST API request
    StringBuilder requestUri = new StringBuilder()
    .Append(spContext.SPHostUrl)
    .Append("/_api/search/query?querytext='LastName:")
    .Append(startLetter)
    .Append("*'&selectproperties='LastName,FirstName,WorkEmail,WorkPhone'&sourceid='B09A7990-05EA-4AF9-81EF-EDFAB16C4E31'&sortlist='FirstName:ascending'");

    //Create HTTP Client
    HttpClient client = new HttpClient();
    //Add the REST API request
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, requestUri.ToString());
    //Set accept header
    request.Headers.Accept.Add(new MediaTypeWithQualityHeaderValue("application/xml"));
    //Set Bearer header equal to access token
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);

    //Send the REST API request
    HttpResponseMessage response = await client.SendAsync(request);
    //Set the response
    string responseString = await response.Content.ReadAsStringAsync();

<span data-ttu-id="21394-172">[Zum Erstellen von SharePoint-add-ins, die Nutzung von Search (O365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) führt Sie durch die [EmployeeDirectory (OfficeDev Schulung Inhalt)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).</span><span class="sxs-lookup"><span data-stu-id="21394-172">The [How to build SharePoint add-ins that leverage search (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) walks you through the [EmployeeDirectory (OfficeDev Training Content)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).</span></span>

<span data-ttu-id="21394-173">**Mithilfe der clientseitigen Option**</span><span class="sxs-lookup"><span data-stu-id="21394-173">**Client-side Option**</span></span>

<span data-ttu-id="21394-174">Im folgenden Codebeispiel wird veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit der REST-API von JavaScript ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="21394-174">The following code example demonstrates how to execute searches with the SharePoint Search Service with the REST API from JavaScript.</span></span>  <span data-ttu-id="21394-175">Dieses Beispiel führt eine Suche für alle Elemente, die den Begriff "Lacrosse" enthalten.</span><span class="sxs-lookup"><span data-stu-id="21394-175">This example executes a search for all items that contain the term 'Lacrosse'.</span></span>
    
    $.ajax(
            {
                url: "http://site/_api/search/" +
                     "query?querytext='{Lacrosse}‘",
                method: "GET",
                headers: {
                    "accept": "application/json;odata=verbose",
                },
                success: onSuccess,
                error: onError
            }
        );

<a name="related-links"></a><span data-ttu-id="21394-176">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="21394-176">Related links</span></span>
=============
- [<span data-ttu-id="21394-177">Zum Ausführen von personalisierten Suchabfragen mit CSOM (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="21394-177">How to perform personalized search queries with CSOM (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM)
- [<span data-ttu-id="21394-178">EmployeeDirectory (OfficeDev Schulungsinhalte)</span><span class="sxs-lookup"><span data-stu-id="21394-178">EmployeeDirectory (OfficeDev Training Content)</span></span>](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)
- [<span data-ttu-id="21394-179">Zum Erstellen von SharePoint-add-ins, dass nutzen die Suche (Office 365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="21394-179">How to build SharePoint add-ins that leverage search (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search)
- <span data-ttu-id="21394-180">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="21394-180">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="21394-181">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="21394-181">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="21394-182">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="21394-182">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="21394-183">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="21394-183">Related PnP samples</span></span>
===================
- [<span data-ttu-id="21394-184">Search.PersonalizedResults (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="21394-184">Search.PersonalizedResults (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
- <span data-ttu-id="21394-185">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="21394-185">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="21394-186">Gilt für</span><span class="sxs-lookup"><span data-stu-id="21394-186">Applies to</span></span>
==========
- <span data-ttu-id="21394-187">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="21394-187">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="21394-188">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="21394-188">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="21394-189">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="21394-189">SharePoint 2013 on-premises</span></span>
