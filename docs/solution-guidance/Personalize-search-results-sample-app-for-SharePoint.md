---
title: "Personalisieren von Search Results Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e2190e8d60bbca5f3353662823c921c1f59d1c27
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="personalize-search-results-sample-add-in-for-sharepoint"></a><span data-ttu-id="8309b-102">Personalisieren von Search Results Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="8309b-102">Personalize search results sample add-in for SharePoint</span></span>

<span data-ttu-id="8309b-103">Filtern von Informationen, die dem Benutzer basierend auf dem Wert von einer Benutzerprofileigenschaft angezeigt werden, um SharePoint zu personalisieren.</span><span class="sxs-lookup"><span data-stu-id="8309b-103">You can personalize SharePoint by filtering information that is shown to the user based on the value of a user profile property.</span></span>
    
<span data-ttu-id="8309b-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="8309b-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="8309b-105">Das [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) -Codebeispiel wird veranschaulicht, wie Sie SharePoint durch Filterinformationen basierend auf dem Wert von einer Benutzerprofileigenschaft personalisieren können.</span><span class="sxs-lookup"><span data-stu-id="8309b-105">The [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) code sample shows how you can personalize SharePoint by filtering information based on the value of a user profile property.</span></span> <span data-ttu-id="8309b-106">Einige Beispiele für Pesonalization sind:</span><span class="sxs-lookup"><span data-stu-id="8309b-106">Some examples of pesonalization include:</span></span>

- <span data-ttu-id="8309b-107">Newsartikel oder andere Inhalte nach Land oder Speicherort gefiltert.</span><span class="sxs-lookup"><span data-stu-id="8309b-107">News articles or other content filtered by country or location.</span></span>
    
- <span data-ttu-id="8309b-108">Navigationslinks gefiltert basierend auf die Rolle des Benutzers oder der Organisation.</span><span class="sxs-lookup"><span data-stu-id="8309b-108">Navigation links filtered based on the user's role or organization.</span></span>
    
- <span data-ttu-id="8309b-109">Restaurants oder Retail Steckdose Listen basierend auf den Speicherort der Geschäft.</span><span class="sxs-lookup"><span data-stu-id="8309b-109">Restaurants or retail outlet listings based on the location of your place of business.</span></span>
    
<span data-ttu-id="8309b-110">In diesem Codebeispiel verwendet eine vom Anbieter gehosteten-add-in zum Anzeigen der Suchergebnisse für den Benutzer, die enthalten alle Websites oder nur Teamwebsites, denen der Benutzer zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="8309b-110">This code sample uses a provider-hosted add-in to display search results to the user that include either all sites or only team sites that the user has access to.</span></span> <span data-ttu-id="8309b-111">Im Beispiel dazu:</span><span class="sxs-lookup"><span data-stu-id="8309b-111">To do this, the sample:</span></span>

- <span data-ttu-id="8309b-112">Der Wert der Benutzerprofileigenschaft **Mich-Seite** überprüft.</span><span class="sxs-lookup"><span data-stu-id="8309b-112">Checks the value of the  **AboutMe** user profile property.</span></span>
    
- <span data-ttu-id="8309b-113">Erstellt eine Suche Abfragezeichenfolge Filter den Wert der Benutzerprofileigenschaft **Mich-Seite** zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="8309b-113">Builds a search query filter string associated with the value of the  **AboutMe** user profile property.</span></span>
    
- <span data-ttu-id="8309b-114">Führt die Suchabfrage und zeigt die Ergebnisse der Suchabfrage.</span><span class="sxs-lookup"><span data-stu-id="8309b-114">Runs the search query and displays the search query results.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8309b-115">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="8309b-115">Before you begin</span></span>
<span data-ttu-id="8309b-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="8309b-116"></span></span>

<span data-ttu-id="8309b-117">Laden Sie Sie zuerst [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="8309b-117">To get started, download the  [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-searchpersonalizedresults-app"></a><span data-ttu-id="8309b-118">Verwenden der app Search.PersonalizedResults</span><span class="sxs-lookup"><span data-stu-id="8309b-118">Using the Search.PersonalizedResults app</span></span>
<span data-ttu-id="8309b-119"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="8309b-119"></span></span>

<span data-ttu-id="8309b-120">Wenn Sie dieses Codebeispiel ausführen, wird eine vom Anbieter gehostete Anwendung angezeigt, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="8309b-120">When you run this code sample, a provider-hosted application appears, as shown in Figure 1.</span></span> 

<span data-ttu-id="8309b-121">**Abbildung 1. Startseite der app Search.PersonalizedResults**</span><span class="sxs-lookup"><span data-stu-id="8309b-121">**Figure 1. Start page of the Search.PersonalizedResults app**</span></span>

![Screenshot, der die Startseite der app Search.PersonalizedResults anzeigt](media/d5df9bb4-fa11-4bd6-91fd-c4d339687a8a.png)

<span data-ttu-id="8309b-123">Dieser Artikel beschreibt das Szenario **personalisierte ausführen das Durchsuchen von allen Websitevorlagen mit Profildaten** .</span><span class="sxs-lookup"><span data-stu-id="8309b-123">This article describes the  **Perform personalized search of all site templates using profile data** scenario.</span></span> <span data-ttu-id="8309b-124">**Personalisierte Suche ausführen** auswählen gibt gefilterte Suchergebnisse, die Teamwebsites nur, siehe Abbildung 2 enthalten.</span><span class="sxs-lookup"><span data-stu-id="8309b-124">Choosing **Perform Personalized Search** returns filtered search results that contain team sites only, as shown in Figure 2.</span></span> <span data-ttu-id="8309b-125">Beachten Sie, dass die **Vorlage** Spalte Websites vom Typ nur **STS** enthält.</span><span class="sxs-lookup"><span data-stu-id="8309b-125">Notice that the **Template** column contains sites of type **STS** only.</span></span>

<span data-ttu-id="8309b-126">**Abbildung 2. Suchergebnisse nur die Teamwebsites anzeigen**</span><span class="sxs-lookup"><span data-stu-id="8309b-126">**Figure 2. Search results showing team sites only**</span></span>

![Screenshot der uchen Ergebnisse anzeigen nur für Teamwebsites](media/dde71d9f-a296-4bee-b48b-964f81193404.png)

<span data-ttu-id="8309b-128">Für die Verarbeitung von Szenarien Personalisierung, können Sie die Suchabfrage durch ändern:</span><span class="sxs-lookup"><span data-stu-id="8309b-128">For handling personalization scenarios, you can change the search query by:</span></span>

- <span data-ttu-id="8309b-129">Lesen und den Wert der Benutzerprofileigenschaften für diesen Benutzer zu testen.</span><span class="sxs-lookup"><span data-stu-id="8309b-129">Reading and testing the value of a user profile property for that user.</span></span> <span data-ttu-id="8309b-130">In diesem Codebeispiel testet die **Über mich** -Eigenschaft für einen Wert der **Apptesten**.</span><span class="sxs-lookup"><span data-stu-id="8309b-130">This code sample tests the  **About Me** property for a value of **AppTest**.</span></span>
    
- <span data-ttu-id="8309b-131">Nutzen einen bestimmten Kurs Aktion basierend auf dem Wert der Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="8309b-131">Taking a specific course of action based on the value of the user profile property.</span></span> <span data-ttu-id="8309b-132">Beispielsweise ist der Wert der **Über mich** Benutzerprofileigenschaft **Apptesten**, dieses Codebeispiel entfernt den Team Site Filter und liefert Suchergebnisse, die alle Websites enthalten.</span><span class="sxs-lookup"><span data-stu-id="8309b-132">For example, if the value of the  **About Me** user profile property is **AppTest**, this code sample removes the team site filter and returns search results that contain all sites.</span></span>

### <a name="to-enter-apptest-in-the-about-me-user-profile-property"></a><span data-ttu-id="8309b-133">Apptesten in über mich Benutzerprofileigenschaft eingeben</span><span class="sxs-lookup"><span data-stu-id="8309b-133">To enter AppTest in the About Me user profile property</span></span>

1. <span data-ttu-id="8309b-134">Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild und dann **Über mich**, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="8309b-134">At the top of your Office 365 site, choose your profile picture, then choose  **About Me**, as shown in Figure 3.</span></span>
    
2. <span data-ttu-id="8309b-135">Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="8309b-135">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="8309b-136">Geben Sie **über mich** **Apptesten**.</span><span class="sxs-lookup"><span data-stu-id="8309b-136">In  **About me**, enter  **AppTest**.</span></span>
    
4. <span data-ttu-id="8309b-137">Wählen Sie **Speichern und schließen**.</span><span class="sxs-lookup"><span data-stu-id="8309b-137">Choose  **Save all and close**.</span></span>

<span data-ttu-id="8309b-138">**Abbildung 3. Navigieren zu Profilseite des Benutzers über mich auswählen**</span><span class="sxs-lookup"><span data-stu-id="8309b-138">**Figure 3. Navigating to a user's profile page by choosing About me**</span></span>

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben.](media/a7eccfcd-68f7-44b9-8f32-14a0d2f60398.png)

<span data-ttu-id="8309b-140">Zurück zu des **Search.PersonalizedResults** vom Anbieter gehosteten-add-Ins, und wählen Sie **Personalisierte Search führen Sie** erneut.</span><span class="sxs-lookup"><span data-stu-id="8309b-140">Return to the  **Search.PersonalizedResults** provider-hosted add-in and choose **Perform Personalized Search** again.</span></span> <span data-ttu-id="8309b-141">Das Add-in ändert den Filter für die Suchabfrage alle Websites anstelle von Teamwebsites nur, wie in Abbildung 4 angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8309b-141">The add-in changes the filter on the search query to show all sites instead of team sites only, as shown in Figure 4.</span></span> <span data-ttu-id="8309b-142">Die **Vorlage** Spalte enthält nun mehrere verschiedene Vorlage Websitetypen.</span><span class="sxs-lookup"><span data-stu-id="8309b-142">The **Template** column now contains several different site template types.</span></span>

<span data-ttu-id="8309b-143">**Abbildung 4. Alle Websites mit Suchergebnissen**</span><span class="sxs-lookup"><span data-stu-id="8309b-143">**Figure 4. Search results showing all sites**</span></span>

![Screenshot von Suchergebnissen alle Websites anzeigen](media/3af49550-cd2d-4e7e-af1d-5227a5603730.png)

<span data-ttu-id="8309b-145">Auswählen von **Personalisierten Suche ausführen** Ruft die **BtnPersonalizedSearch_Click** -Methode in "default.aspx.cs".</span><span class="sxs-lookup"><span data-stu-id="8309b-145">Choosing  **Perform Personalized Search** calls the **btnPersonalizedSearch_Click** method in default.aspx.cs.</span></span> <span data-ttu-id="8309b-146">**BtnPersonalizedSearch_Click** führt die folgenden Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="8309b-146">**btnPersonalizedSearch_Click** performs the following actions:</span></span>

- <span data-ttu-id="8309b-147">Wird mit **PeopleManager** alle Benutzerprofileigenschaften für den Benutzer dieses Add-in ausführt.</span><span class="sxs-lookup"><span data-stu-id="8309b-147">Uses  **PeopleManager** to get all user profile properties for the user running this add-in.</span></span>
    
- <span data-ttu-id="8309b-148">Ruft ab, und der Wert der Benutzerprofileigenschaft **Mich-Seite** überprüft.</span><span class="sxs-lookup"><span data-stu-id="8309b-148">Retrieves and checks the value of the  **AboutMe** user profile property.</span></span> <span data-ttu-id="8309b-149">Wenn der Wert der Eigenschaft **Mich-Seite** **Apptesten**ist, ruft die Suchabfrage alle Websites, die mit der Abfragezeichenfolge `contentclass:"STS_Site"`.</span><span class="sxs-lookup"><span data-stu-id="8309b-149">If the value of the **AboutMe** property is **AppTest**, the search query retrieves all sites using the query string  `contentclass:"STS_Site"`.</span></span> <span data-ttu-id="8309b-150">Wenn der Wert der Eigenschaft **Mich-Seite** nicht **Apptesten**ist, wird der Team Site Filter an die Abfragezeichenfolge angehängt ( `WebTemplate=STS`), und die Suchabfrage nur Teamwebsites abgerufen.</span><span class="sxs-lookup"><span data-stu-id="8309b-150">If the value of the  **AboutMe** property is not **AppTest**, the team site filter is appended to the query string ( `WebTemplate=STS`), and the search query retrieves team sites only.</span></span>
    
- <span data-ttu-id="8309b-151">Ruft die **ProcessQuery** -Methode zum Abrufen der Suchergebnisse basierend auf der angegebenen Abfragezeichenfolge an.</span><span class="sxs-lookup"><span data-stu-id="8309b-151">Calls the  **ProcessQuery** method to retrieve the search results based on the supplied query string.</span></span> <span data-ttu-id="8309b-152">**ProcessQuery** wird veranschaulicht, wie eine Liste mit Eigenschaften mit den Suchergebnissen zurückgegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8309b-152">**ProcessQuery** also demonstrates how to specify a list of properties to return with the search results.</span></span>
    
- <span data-ttu-id="8309b-153">Ruft die **FormatResults** -Methode, um die Suchergebnisse in eine HTML-Tabelle zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="8309b-153">Calls the  **FormatResults** method to format the search results into an HTML table.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="8309b-154">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="8309b-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
protected void btnPersonalizedSearch_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load user profile properties.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties);
                clientContext.ExecuteQuery();
                // Check the value of About Me. 
                string aboutMeValue = personProperties.UserProfileProperties["AboutMe"];
                string templateFilter = ResolveAdditionalFilter(aboutMeValue);
                // Build the query string.
                string query = "contentclass:\"STS_Site\" " + templateFilter;
                ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
                lblStatus2.Text = FormatResults(results);
            }
        }

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
```

## <a name="see-also"></a><span data-ttu-id="8309b-155">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8309b-155">See also</span></span>
<span data-ttu-id="8309b-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8309b-156"></span></span>

-  [<span data-ttu-id="8309b-157">User Profile Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8309b-157">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="8309b-158">Search.PersonalizedResults-app</span><span class="sxs-lookup"><span data-stu-id="8309b-158">Search.PersonalizedResults app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
    
-  [<span data-ttu-id="8309b-159">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="8309b-159">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="8309b-160">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="8309b-160">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
    
-  [<span data-ttu-id="8309b-161">Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="8309b-161">Core.ProfileProperty.Migration</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
