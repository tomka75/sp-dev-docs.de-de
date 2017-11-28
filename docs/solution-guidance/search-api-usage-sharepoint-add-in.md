---
title: Such-API-Verwendung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c4ad4850f8e76ddf2933981ce550a141bf75d792
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="search-api-usage-in-the-sharepoint-add-in-model"></a>Such-API-Verwendung in der SharePoint-add-in-Objektmodell
===============================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Ausführen der Suche mit den SharePoint-Suchdienst unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, das SharePoint Server-Side-Objektmodell (vom Webpart für Inhaltsabfragen Außerkraftsetzungen) oder die Search-Webdienste wurden auszuführenden Suche mit den SharePoint-Suchdienst verwendet.

In einem Szenario mit SharePoint-Add-Ins Modell führen Sie Suchvorgänge mit der SharePoint Search-Dienst über das CSOM oder den REST-APIs.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir bieten die folgenden high Level Richtlinien zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.

- Verwendung AppOnly ist Authentifizierung nicht für alle Vorgänge Search-Dienst unterstützt.
    + Dies ist daran so, dass der Suchdienst greift auf User Profile Service (USV), um Benutzerprofilinformationen zu suchen und die USV AppOnly-Authentifizierung nicht unterstützt.
    + Aus diesem Grund, da die Relevanz und andere Aspekte der Suche hängen von einem bestimmten Benutzer und deren Profil Attribute der AppOnly authentifizierungsmuster nicht funktionieren.

<a name="options-to-execute-searches-with-the-sharepoint-search-service"></a>Optionen zum Ausführen der Suche mit den SharePoint-Suchdienst
--------------------------------------------------------------

Sie haben eine Coupé der Optionen zum Suchen mit den SharePoint-Suchdienst ausgeführt.

- .NET CSOM-API
- JavaScript-CSOM (JSOM)-API
- REST-API  

<a name="net-csom-api"></a>.NET CSOM-API
-------------
Bei dieser Option verwenden Sie die .net CSOM-API sucht mit den SharePoint-Suchdienst ausgeführt.
    
- Diese API ist nur verfügbar in verwaltetem.


**Wenn sie geeignet ist?**

- Diese API ist eine optimale Lösung für vom Anbieter gehosteten-Add-ins, lange ausgeführte Vorgänge oder andere serverseitige Szenarien, die auf die .net Plattform ausgeführt.
- Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, ASP.NET Web-API-Diensten, .net-Verwaltungskonsole oder Windows-Anwendungen und Azure Web, stellen.

**Erste Schritte**

Das folgende Beispiel veranschaulicht, wie Sie mit der SharePoint-Suchdienst mit der .net CSOM-API sucht ausführen.  Darüber hinaus wird veranschaulicht, wie auf Profil eines Benutzers, um die Suchergebnisse zu personalisieren zugreifen.

- [Search.PersonalizedResults (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)

![Die API für die Suche und Personalisierung-Seite. Text im Bild: Such-API-Suche ausführen. Suchfilter für Mandanten breit Suchabfrage enthalten: Textfeld enthält das Wort Test. Schaltfläche Text: einfache Suche. Führen Sie das Durchsuchen von allen Websitevorlagen mit Profildaten personalisierte. Wenn über mich keinen Text Apptesten enthält suchen wir nur die Sites die Teamwebsites sind (WebTemplate = STS). Wenn Apptesten vorhanden ist, suchen wir alle Websites an. Szenario: Zeigt Websites oder aggregierte Daten aus bestimmte Orte basierend auf dem Benutzerprofil. Beispiel wäre auf aggregierte News-Seiten, die nur mit übereinstimmenden aktuellen Benutzerstandort oder Stadt Bezeichner markiert sind. Schaltfläche Text: personalisierte Suche ausführen.](media/Recipes/SearchAPI/Search.PersonalizedResults.png)

[Zum Ausführen von personalisierten Suchabfragen mit CSOM (O365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) führt Sie durch die [Search.PersonalizedResults (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).

Die **BtnPerformSearch_Click** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) führt eine Suche nach der Textwert, den der Benutzer in das Suchfeld eingibt, und legt den Suchbereich auf alle Inhalte, die in einer Websitesammlung gespeichert ist.  Die Contentclass: "STS_Site"-Parameter schränkt den Suchbereich für Websitesammlungen.

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

Die **BtnPersonalizedSearch_Click** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) führt die gleiche Suche aus, wie die BtnPerformSearch_Click-Methode ist und fügt außerdem einen weiteren Parameter basierend auf dem aktuellen Profil des Benutzers hinzu.  Die PeopleManager-Klasse wird verwendet, um Benutzerprofileigenschaften für den aktuellen Benutzer zugreifen.

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

Die **ResolveAdditionalFilter** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) ausgewertet wird der aktuelle von Benutzerprofileigenschaften und gibt einen entsprechenden Suchparameter zurück. In diesem Beispiel enthält die Benutzerprofileigenschaft AboutMeValue Apptesten und klicken Sie dann die Suchparameter WebTemplate = STS wird zurückgegeben.  Dieser Parameter beschränkt den Suchbereich auf Websites, die mit der Vorlage STS (Teamwebsite) erstellt.
 
    private string ResolveAdditionalFilter(string aboutMeValue)
    {
        if (!aboutMeValue.Contains("AppTest"))
        {
            return "WebTemplate=STS";
        }
        
        return "";
    }

In beiden Fällen verwendet die **ProcessQuery** -Methode in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) die SearchExecutor-Klasse die Search-Abfrage ausführen und die Ergebnisse zurückzugeben. 

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

<a name="javascript-csom-jsom-api"></a>JavaScript-CSOM (JSOM)-API
--------------------------
Bei dieser Option verwenden Sie die JavaScript CSOM (JSOM) API sucht mit den SharePoint-Suchdienst ausgeführt.
    
- Diese API ist nur verfügbar in clientseitige JavaScript-Code.

**Wenn sie geeignet ist?**

- Diese API ist eine optimale Lösung für SharePoint-Hosting-Add-ins und vom Anbieter gehosteten-Add-ins, die auf eine beliebige Webplattform ausgeführt.
- Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, PHP-Websites, Websites Python.

**Erste Schritte**

Im folgenden Codebeispiel wird veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit dem JavaScript CSOM (JSOM) API ausgeführt wird.  Dieses Beispiel führt eine Suche für alle Elemente, die den Begriff "Blizzard" enthalten.

    var context = SP.ClientContext.get_current();
    
    var keywordQuery = 
    new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
    
    keywordQuery.set_queryText("Blizzard");
    
    var searchExecutor = 
    new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
    
    results = searchExecutor.executeQuery(keywordQuery);
    
    context.executeQueryAsync(onGetEventsSuccess, onGetEventsFail);

<a name="rest-api"></a>REST-API
--------
Bei dieser Option verwenden Sie die REST-API sucht mit den SharePoint-Suchdienst ausgeführt.
    
- Diese API ist flexibelsten, da es im serverseitige und clientseitige Code verfügbar ist.
- Der REST-API für SharePoint Search Service-Stamm-Endpunkt ist:
    + https://<tenant>/site/_api/search/query
- Es folgen einige einfache Beispiele:
    + Stichwortsuche
    
        ```
        https://tenant/site/_api/search/query?querytext='{Apples}'
        ```
    + Bestimmte Eigenschaften auswählen
    
        ```
        https://tenant/site/_api/search/query?querytext='test'&selectproperties='Rank, Title'
        ```
    + Die Sortierung
    
        ```
        https://tenant/site/_api/search/query?querytext='Oranges'&sortlist='LastModifiedTime:ascending'
        ```

**Wenn sie geeignet ist?**

Diese API ist eine optimale Lösung für SharePoint-Hosting-Add-ins und vom Anbieter gehosteten-Add-ins, die auf eine beliebige Webplattform ausgeführt.
- Einige Beispiele für diese Szenarien sind ASP.NET MVC-Websites, PHP-Websites, Python-Websites, ASP.NET Web-API-Diensten, .net-Verwaltungskonsole oder Windows Azure Webaufträge, Applications usw..

**Erste Schritte**

**Serverseitige Option**

Das folgende Beispiel veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit der REST-API von verwaltetem ausführen.

- [EmployeeDirectory (OfficeDev Schulungsinhalte)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)

Die **Index** -Methode in der [Klasse HomeController.cs](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) führt eine Suche für alle Benutzer, deren Nachname mit dem Text beginnt, der Benutzer klickt auf Wert.

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

[Zum Erstellen von SharePoint-add-ins, die Nutzung von Search (O365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) führt Sie durch die [EmployeeDirectory (OfficeDev Schulung Inhalt)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).

**Mithilfe der clientseitigen Option**

Im folgenden Codebeispiel wird veranschaulicht, wie Suchvorgänge mit den SharePoint-Suchdienst mit der REST-API von JavaScript ausgeführt wird.  Dieses Beispiel führt eine Suche für alle Elemente, die den Begriff "Lacrosse" enthalten.
    
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

<a name="related-links"></a>Verwandte links
=============
- [Zum Ausführen von personalisierten Suchabfragen mit CSOM (O365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM)
- [EmployeeDirectory (OfficeDev Schulungsinhalte)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)
- [Zum Erstellen von SharePoint-add-ins, dass nutzen die Suche (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [Search.PersonalizedResults (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
