---
title: Search customizations for SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: 3bf69aac7b506a68124f57f8c4eafcc3508307c5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="search-customizations-for-sharepoint"></a><span data-ttu-id="e81fa-102">Search customizations for SharePoint</span><span class="sxs-lookup"><span data-stu-id="e81fa-102">Search customizations for SharePoint</span></span>

<span data-ttu-id="e81fa-103">Create customized SharePoint 2013 and SharePoint Online search scenarios by using a search-based site directory, personalized search, or search configuration portability.</span><span class="sxs-lookup"><span data-stu-id="e81fa-103">Create customized SharePoint 2013 and SharePoint Online search scenarios by using a search-based site directory, personalized search, or search configuration portability.</span></span> 

<span data-ttu-id="e81fa-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="e81fa-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

## <a name="search-based-site-directory"></a><span data-ttu-id="e81fa-105">Search-based site directory</span><span class="sxs-lookup"><span data-stu-id="e81fa-105">Search-based site directory</span></span>

<span data-ttu-id="e81fa-106">SharePoint search enables you to create a search-based site directory without writing any custom code.</span><span class="sxs-lookup"><span data-stu-id="e81fa-106">SharePoint search enables you to create a search-based site directory without writing any custom code.</span></span> 

<span data-ttu-id="e81fa-107">To create a site directory:</span><span class="sxs-lookup"><span data-stu-id="e81fa-107">To create a site directory:</span></span>

1. <span data-ttu-id="e81fa-108">Create the site directory display templates.</span><span class="sxs-lookup"><span data-stu-id="e81fa-108">Create the site directory display templates.</span></span>
    
2. <span data-ttu-id="e81fa-109">Define the site directory result type.</span><span class="sxs-lookup"><span data-stu-id="e81fa-109">Define the site directory result type.</span></span>
    
3. <span data-ttu-id="e81fa-110">Create the results page.</span><span class="sxs-lookup"><span data-stu-id="e81fa-110">Create the results page.</span></span>
    
4. <span data-ttu-id="e81fa-111">Edit the Results Web Part properties.</span><span class="sxs-lookup"><span data-stu-id="e81fa-111">Edit the Results Web Part properties.</span></span>
    
<span data-ttu-id="e81fa-112">To create the site directory display templates:</span><span class="sxs-lookup"><span data-stu-id="e81fa-112">To create the site directory display templates:</span></span>

> [!NOTE] 
> <span data-ttu-id="e81fa-113">This procedure uses the site-related display templates without modification.</span><span class="sxs-lookup"><span data-stu-id="e81fa-113">This procedure uses the site-related display templates without modification.</span></span> <span data-ttu-id="e81fa-114">If you want to change how site directory results are displayed, modify the display templates that you create.</span><span class="sxs-lookup"><span data-stu-id="e81fa-114">If you want to change how site directory results are displayed, modify the display templates that you create.</span></span>

1. <span data-ttu-id="e81fa-115">Open the mapped network drive to the  **Master Page Gallery**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-115">Open the mapped network drive to the  **Master Page Gallery**.</span></span> <span data-ttu-id="e81fa-116">For more information, see [How to: Map a network drive to the SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e81fa-116">For more information, see [How to: Map a network drive to the SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span></span>
    
2. <span data-ttu-id="e81fa-117">Make copies of the display template HTML files that best map what you're trying to do.</span><span class="sxs-lookup"><span data-stu-id="e81fa-117">Make copies of the display template HTML files that best map what you're trying to do.</span></span> <span data-ttu-id="e81fa-118">For the site directory scenario, this will be Item_Site.html and Item_Site_HoverPanel.html.</span><span class="sxs-lookup"><span data-stu-id="e81fa-118">For the site directory scenario, this will be Item_Site.html and Item_Site_HoverPanel.html.</span></span> <span data-ttu-id="e81fa-119">Both files are located in the  `\Display Templates\Search` folder in the mapped network drive.</span><span class="sxs-lookup"><span data-stu-id="e81fa-119">Both files are located in the  `\Display Templates\Search` folder in the mapped network drive.</span></span>
    
3. <span data-ttu-id="e81fa-120">Rename the copies that you made of the Item_SiteDirectory.html and Item_SiteDirectory_HoverPanel.html files as shown.</span><span class="sxs-lookup"><span data-stu-id="e81fa-120">Rename the copies that you made of the Item_SiteDirectory.html and Item_SiteDirectory_HoverPanel.html files as shown.</span></span>
    
    <span data-ttu-id="e81fa-121">**Figure 1. Site directory display templates**</span><span class="sxs-lookup"><span data-stu-id="e81fa-121">**Figure 1. Site directory display templates**</span></span>

    ![Site directory display templates](media/search-customizations-for-sharepoint/4c084d31-bad4-45f0-950b-ba214f9487f7.png)

4. <span data-ttu-id="e81fa-123">Open the Item_SiteDirectory.html file and make the following changes:</span><span class="sxs-lookup"><span data-stu-id="e81fa-123">Open the Item_SiteDirectory.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="e81fa-124">Change the  `<title>` tag value from "Site Item" to "Site Directory".</span><span class="sxs-lookup"><span data-stu-id="e81fa-124">Change the  `<title>` tag value from "Site Item" to "Site Directory".</span></span>
    
    - <span data-ttu-id="e81fa-125">Change the first  `<div>` tag after the opening `<body>` tag from `<div id="Item_Site">` to `<div id="Item_SiteDirectory">`.</span><span class="sxs-lookup"><span data-stu-id="e81fa-125">Change the first  `<div>` tag after the opening `<body>` tag from `<div id="Item_Site">` to `<div id="Item_SiteDirectory">`.</span></span>
    
    - <span data-ttu-id="e81fa-126">Change the hover panel display template JavaScript file name from: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`to: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span><span class="sxs-lookup"><span data-stu-id="e81fa-126">Change the hover panel display template JavaScript file name from: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`to: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span></span>
    
5. <span data-ttu-id="e81fa-127">Open the Item_SiteDirectory_HoverPanel.html file and make the following changes:</span><span class="sxs-lookup"><span data-stu-id="e81fa-127">Open the Item_SiteDirectory_HoverPanel.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="e81fa-128">Change the  `<div>` tag following the opening `<body>` tag from: `<title>Site Hover Panel Test</title>`to: `<title>Site Directory Hover Panel</title>`</span><span class="sxs-lookup"><span data-stu-id="e81fa-128">Change the  `<div>` tag following the opening `<body>` tag from: `<title>Site Hover Panel Test</title>`to: `<title>Site Directory Hover Panel</title>`</span></span>
    
    - <span data-ttu-id="e81fa-129">Change the  `<title>` tag from: `<div id="Item_Site_HoverPanel">`to: `<div id="Item_SiteDirectory_HoverPanel">`</span><span class="sxs-lookup"><span data-stu-id="e81fa-129">Change the  `<title>` tag from: `<div id="Item_Site_HoverPanel">`to: `<div id="Item_SiteDirectory_HoverPanel">`</span></span>
    
<span data-ttu-id="e81fa-130">To define the site directory result type:</span><span class="sxs-lookup"><span data-stu-id="e81fa-130">To define the site directory result type:</span></span>

1. <span data-ttu-id="e81fa-131">Go to  **Site Settings** > **Search** > **Result Types**, and then choose  **New Result Type**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-131">Go to  **Site Settings** > **Search** > **Result Types**, and then choose  **New Result Type**.</span></span>
    
2. <span data-ttu-id="e81fa-132">Name your new result type "Basic Site Directory".</span><span class="sxs-lookup"><span data-stu-id="e81fa-132">Name your new result type "Basic Site Directory".</span></span>
    
3. <span data-ttu-id="e81fa-133">In the  **What should these results look like?** box, select **Site Directory**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-133">In the  **What should these results look like?** box, select **Site Directory**.</span></span>
    
    <span data-ttu-id="e81fa-134">**Figure 2. Site result configuration**</span><span class="sxs-lookup"><span data-stu-id="e81fa-134">**Figure 2. Site result configuration**</span></span>

    ![Example site result configuration](media/search-customizations-for-sharepoint/4f42a7c4-326b-4508-b9a7-e030ef34cd33.png)

4. <span data-ttu-id="e81fa-136">Choose  **Save**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-136">Choose  **Save**.</span></span>
    
<span data-ttu-id="e81fa-137">To create the results page:</span><span class="sxs-lookup"><span data-stu-id="e81fa-137">To create the results page:</span></span>

1. <span data-ttu-id="e81fa-138">On the  **Site Settings** menu, select **Site contents**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-138">On the  **Site Settings** menu, select **Site contents**.</span></span>
    
2. <span data-ttu-id="e81fa-139">Select  **Pages**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-139">Select  **Pages**.</span></span>
    
3. <span data-ttu-id="e81fa-140">In the  **Pages** library, select **Files** > **New Document** > **Page**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-140">In the  **Pages** library, select **Files** > **New Document** > **Page**.</span></span>
    
4. <span data-ttu-id="e81fa-141">On the  **Create Page** page, specify "Site Directory" for **Title** and "sitedirectory" for **URL Name**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-141">On the  **Create Page** page, specify "Site Directory" for **Title** and "sitedirectory" for **URL Name**.</span></span>
    
5. <span data-ttu-id="e81fa-142">Choose  **Create**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-142">Choose  **Create**.</span></span>
    
<span data-ttu-id="e81fa-143">To edit the Results Web Part properties:</span><span class="sxs-lookup"><span data-stu-id="e81fa-143">To edit the Results Web Part properties:</span></span>

1. <span data-ttu-id="e81fa-144">On the  **Site Directory** page, choose **Settings** > **Edit Page**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-144">On the  **Site Directory** page, choose **Settings** > **Edit Page**.</span></span>
    
2. <span data-ttu-id="e81fa-145">In the  **Search Results Web Part**, choose the  **Web Part** menu, and then choose **Edit Web Part**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-145">In the  **Search Results Web Part**, choose the  **Web Part** menu, and then choose **Edit Web Part**.</span></span>
    
    <span data-ttu-id="e81fa-146">**Figure 3. Web Part menu**</span><span class="sxs-lookup"><span data-stu-id="e81fa-146">**Figure 3. Web Part menu**</span></span>

    ![fig 3](media/search-customizations-for-sharepoint/1b01ac59-3bc1-42eb-a63d-61c2ad15cee4.png)

3. <span data-ttu-id="e81fa-148">In the Web Part tool pane, choose  **Change query** to open the Query Builder.</span><span class="sxs-lookup"><span data-stu-id="e81fa-148">In the Web Part tool pane, choose  **Change query** to open the Query Builder.</span></span>
    
4. <span data-ttu-id="e81fa-149">In the  **Query text** field, enter the following: `ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span><span class="sxs-lookup"><span data-stu-id="e81fa-149">In the  **Query text** field, enter the following: `ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span></span>
    
5. <span data-ttu-id="e81fa-150">Choose  **Test query** to confirm that the syntax is correct.</span><span class="sxs-lookup"><span data-stu-id="e81fa-150">Choose  **Test query** to confirm that the syntax is correct.</span></span> <span data-ttu-id="e81fa-151">The **Search Results Preview** pane should display subsites within the site you specified for _path_ in the **Query text**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-151">The **Search Results Preview** pane should display subsites within the site you specified for _path_ in the **Query text**.</span></span>
    
    <span data-ttu-id="e81fa-152">**Figure 4. Search results Web Part query builder**</span><span class="sxs-lookup"><span data-stu-id="e81fa-152">**Figure 4. Search results Web Part query builder**</span></span>

    ![Search results web part query builder](media/search-customizations-for-sharepoint/7b55c821-4772-4874-bbcb-c757e2723599.png)

6. <span data-ttu-id="e81fa-154">Choose  **OK** to close the Query Builder.</span><span class="sxs-lookup"><span data-stu-id="e81fa-154">Choose  **OK** to close the Query Builder.</span></span>
    
7. <span data-ttu-id="e81fa-155">In  **Display Templates**, select  **Use result types to display items**.</span><span class="sxs-lookup"><span data-stu-id="e81fa-155">In  **Display Templates**, select  **Use result types to display items**.</span></span>
    
8. <span data-ttu-id="e81fa-156">Select  **Basic Site Directory** in the **Result type for item** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e81fa-156">Select  **Basic Site Directory** in the **Result type for item** drop-down list.</span></span>
    
9. <span data-ttu-id="e81fa-157">In the  **Appearance** section, change the **Title** to "Sites I have access to".</span><span class="sxs-lookup"><span data-stu-id="e81fa-157">In the  **Appearance** section, change the **Title** to "Sites I have access to".</span></span>
    
10. <span data-ttu-id="e81fa-158">Choose  **OK** to save the changes to the Web Part and to close the Web Part tool pane.</span><span class="sxs-lookup"><span data-stu-id="e81fa-158">Choose  **OK** to save the changes to the Web Part and to close the Web Part tool pane.</span></span> <span data-ttu-id="e81fa-159">The following figure shows an example of a search-based site directory page.</span><span class="sxs-lookup"><span data-stu-id="e81fa-159">The following figure shows an example of a search-based site directory page.</span></span>
    
    <span data-ttu-id="e81fa-160">**Figure 5. Contoso search-based site directory example**</span><span class="sxs-lookup"><span data-stu-id="e81fa-160">**Figure 5. Contoso search-based site directory example**</span></span>

    ![Contoso search-based site directory example](media/search-customizations-for-sharepoint/5d1317d5-2e82-4819-b5a4-5bb515898a7b.png)

## <a name="personalized-search-results"></a><span data-ttu-id="e81fa-162">Personalized search results</span><span class="sxs-lookup"><span data-stu-id="e81fa-162">Personalized search results</span></span>

<span data-ttu-id="e81fa-163">Personalized search is when you show search results targeted to the user submitting the search request.</span><span class="sxs-lookup"><span data-stu-id="e81fa-163">Personalized search is when you show search results targeted to the user submitting the search request.</span></span> <span data-ttu-id="e81fa-164">This section describes some scenarios for personalized search and how you might implement them.</span><span class="sxs-lookup"><span data-stu-id="e81fa-164">This section describes some scenarios for personalized search and how you might implement them.</span></span>

### <a name="your-news-scenario"></a><span data-ttu-id="e81fa-165">Your news scenario</span><span class="sxs-lookup"><span data-stu-id="e81fa-165">Your news scenario</span></span>

<span data-ttu-id="e81fa-166">In this scenario, you create a search add-in that shows relevant content, such as news and events, targeted to the user.</span><span class="sxs-lookup"><span data-stu-id="e81fa-166">In this scenario, you create a search add-in that shows relevant content, such as news and events, targeted to the user.</span></span>

<span data-ttu-id="e81fa-167">**Figure 6. Your News personalized search scenario**</span><span class="sxs-lookup"><span data-stu-id="e81fa-167">**Figure 6. Your News personalized search scenario**</span></span>

![Your News personalized search scenario](media/search-customizations-for-sharepoint/188af4d1-b8bb-4212-bfdb-c29a13f30286.png)

<span data-ttu-id="e81fa-169">To implement the news scenario, use the SharePoint search results Web Part and default display templates to display the news information, including title, description, and rollup image.</span><span class="sxs-lookup"><span data-stu-id="e81fa-169">To implement the news scenario, use the SharePoint search results Web Part and default display templates to display the news information, including title, description, and rollup image.</span></span> <span data-ttu-id="e81fa-170">Show the first 10 news items.</span><span class="sxs-lookup"><span data-stu-id="e81fa-170">Show the first 10 news items.</span></span> <span data-ttu-id="e81fa-171">When the user chooses the rollup image, title, or Read More link, the news article page is loaded.</span><span class="sxs-lookup"><span data-stu-id="e81fa-171">When the user chooses the rollup image, title, or Read More link, the news article page is loaded.</span></span>

<span data-ttu-id="e81fa-172">Alternatively, you can create a search add-in using the query API (CSOM or REST).</span><span class="sxs-lookup"><span data-stu-id="e81fa-172">Alternatively, you can create a search add-in using the query API (CSOM or REST).</span></span> <span data-ttu-id="e81fa-173">You can make the number of news items to be displayed configurable by using the search add-in properties.</span><span class="sxs-lookup"><span data-stu-id="e81fa-173">You can make the number of news items to be displayed configurable by using the search add-in properties.</span></span>

<span data-ttu-id="e81fa-174">Another option is to use the query API to add the query API code that retrieves the search results directly to the page layout.</span><span class="sxs-lookup"><span data-stu-id="e81fa-174">Another option is to use the query API to add the query API code that retrieves the search results directly to the page layout.</span></span>

<span data-ttu-id="e81fa-175">To display the news and event information specific to the user:</span><span class="sxs-lookup"><span data-stu-id="e81fa-175">To display the news and event information specific to the user:</span></span>

1. <span data-ttu-id="e81fa-176">Modify the query to filter news and event results based on user profile properties like business unit, region, and language.</span><span class="sxs-lookup"><span data-stu-id="e81fa-176">Modify the query to filter news and event results based on user profile properties like business unit, region, and language.</span></span>
    
2. <span data-ttu-id="e81fa-177">Retrieve the Title, Description, rollup image, and URL properties for the news or event items.</span><span class="sxs-lookup"><span data-stu-id="e81fa-177">Retrieve the Title, Description, rollup image, and URL properties for the news or event items.</span></span>
    
3. <span data-ttu-id="e81fa-178">Implement sorting logic for the combined news and events based on the  **LastModifiedDate** property.</span><span class="sxs-lookup"><span data-stu-id="e81fa-178">Implement sorting logic for the combined news and events based on the  **LastModifiedDate** property.</span></span>

### <a name="upcoming-events-scenario"></a><span data-ttu-id="e81fa-179">Upcoming events scenario</span><span class="sxs-lookup"><span data-stu-id="e81fa-179">Upcoming events scenario</span></span>

<span data-ttu-id="e81fa-180">In this scenario, the search add-in shows relevant events targeted to the user.</span><span class="sxs-lookup"><span data-stu-id="e81fa-180">In this scenario, the search add-in shows relevant events targeted to the user.</span></span>

<span data-ttu-id="e81fa-181">**Figure 7. Upcoming Events personalized search scenario**</span><span class="sxs-lookup"><span data-stu-id="e81fa-181">**Figure 7. Upcoming Events personalized search scenario**</span></span>

![Upcoming Events personalized search scenario](media/search-customizations-for-sharepoint/35afac63-b4e9-4d94-abc1-a5fa11cc2dbf.png)

<span data-ttu-id="e81fa-183">To implement this scenario, you can configure the SharePoint search results Web Part to change the query to only retrieve upcoming event information.</span><span class="sxs-lookup"><span data-stu-id="e81fa-183">To implement this scenario, you can configure the SharePoint search results Web Part to change the query to only retrieve upcoming event information.</span></span> <span data-ttu-id="e81fa-184">To do this, specify  `ContentClass:STS_ListItem_Events` for the Web Part's query text.</span><span class="sxs-lookup"><span data-stu-id="e81fa-184">To do this, specify  `ContentClass:STS_ListItem_Events` for the Web Part's query text.</span></span> <span data-ttu-id="e81fa-185">To change how event results are displayed, create custom display templates to render the event information.</span><span class="sxs-lookup"><span data-stu-id="e81fa-185">To change how event results are displayed, create custom display templates to render the event information.</span></span>

<span data-ttu-id="e81fa-186">You can modify the item display template so that when the user chooses the image, title, or Read More link, the event information page is loaded.</span><span class="sxs-lookup"><span data-stu-id="e81fa-186">You can modify the item display template so that when the user chooses the image, title, or Read More link, the event information page is loaded.</span></span> <span data-ttu-id="e81fa-187">You can also modify the control display template so that when the user chooses  **See More**, the next 10 event results are displayed in the Web Part.</span><span class="sxs-lookup"><span data-stu-id="e81fa-187">You can also modify the control display template so that when the user chooses  **See More**, the next 10 event results are displayed in the Web Part.</span></span>

<span data-ttu-id="e81fa-188">You can also create a search add-in that uses the query API to retrieve even results.</span><span class="sxs-lookup"><span data-stu-id="e81fa-188">You can also create a search add-in that uses the query API to retrieve even results.</span></span> <span data-ttu-id="e81fa-189">You can configure the search add-in to show, by default, only 10 of the latest upcoming events, but make this setting configurable through the search add-in properties.</span><span class="sxs-lookup"><span data-stu-id="e81fa-189">You can configure the search add-in to show, by default, only 10 of the latest upcoming events, but make this setting configurable through the search add-in properties.</span></span> 

### <a name="featured-news-scenario"></a><span data-ttu-id="e81fa-190">Featured news scenario</span><span class="sxs-lookup"><span data-stu-id="e81fa-190">Featured news scenario</span></span>

<span data-ttu-id="e81fa-191">In this scenario, the search add-in shows search results as featured content targeted to your users in places such as corporate intranet and divisional landing pages.</span><span class="sxs-lookup"><span data-stu-id="e81fa-191">In this scenario, the search add-in shows search results as featured content targeted to your users in places such as corporate intranet and divisional landing pages.</span></span> <span data-ttu-id="e81fa-192">You can implement this with an add-in part that contains a jQuery plugin with HTML, that uses the search REST service or the query CSOM to get search results from SharePoint and display the results.</span><span class="sxs-lookup"><span data-stu-id="e81fa-192">You can implement this with an add-in part that contains a jQuery plugin with HTML, that uses the search REST service or the query CSOM to get search results from SharePoint and display the results.</span></span>

### <a name="code-sample-for-personalized-search"></a><span data-ttu-id="e81fa-193">Code sample for personalized search</span><span class="sxs-lookup"><span data-stu-id="e81fa-193">Code sample for personalized search</span></span>

<span data-ttu-id="e81fa-194">The [SharePoint 2013: Personalizing search results in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) sample shows a basic search example and a personalized search results example that uses the search query CSOM.</span><span class="sxs-lookup"><span data-stu-id="e81fa-194">The [SharePoint 2013: Personalizing search results in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) sample shows a basic search example and a personalized search results example that uses the search query CSOM.</span></span> <span data-ttu-id="e81fa-195">The basic search example lets the user provide a search filter to use for a tenant-wide search.</span><span class="sxs-lookup"><span data-stu-id="e81fa-195">The basic search example lets the user provide a search filter to use for a tenant-wide search.</span></span> <span data-ttu-id="e81fa-196">Sites are searched based on that user-supplied filter.</span><span class="sxs-lookup"><span data-stu-id="e81fa-196">Sites are searched based on that user-supplied filter.</span></span>

<span data-ttu-id="e81fa-197">The example first gets SharePoint context by using the  **SharePointContextProvider** class.</span><span class="sxs-lookup"><span data-stu-id="e81fa-197">The example first gets SharePoint context by using the  **SharePointContextProvider** class.</span></span>

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
```

<span data-ttu-id="e81fa-198">Next, it builds the query based on what the user entered.</span><span class="sxs-lookup"><span data-stu-id="e81fa-198">Next, it builds the query based on what the user entered.</span></span> <span data-ttu-id="e81fa-199">It restricts the query to site collections, and then calls the  **ProcessQuery** method, passing the context and the query in the method call.</span><span class="sxs-lookup"><span data-stu-id="e81fa-199">It restricts the query to site collections, and then calls the  **ProcessQuery** method, passing the context and the query in the method call.</span></span> <span data-ttu-id="e81fa-200">It then returns the **ProcessQuery** results as a result table, which is then parsed by the **FormatResults** method.</span><span class="sxs-lookup"><span data-stu-id="e81fa-200">It then returns the **ProcessQuery** results as a result table, which is then parsed by the **FormatResults** method.</span></span>

```
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    string query = searchtext.Text + " contentclass:\"STS_Site\"";
    ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
    lblStatus1.Text = FormatResults(results);
}
```

<span data-ttu-id="e81fa-201">The  **ProcessQuery** method builds a **KeywordQuery** object that represents the search query.</span><span class="sxs-lookup"><span data-stu-id="e81fa-201">The  **ProcessQuery** method builds a **KeywordQuery** object that represents the search query.</span></span>

```
KeywordQuery keywordQuery = new KeywordQuery(ctx);
keywordQuery.QueryText = keywordQueryValue;
keywordQuery.RowLimit = 500;
keywordQuery.StartRow = 0;
keywordQuery.SelectProperties.Add("Title");
keywordQuery.SelectProperties.Add("SPSiteUrl");
keywordQuery.SelectProperties.Add("Description");
keywordQuery.SelectProperties.Add("WebTemplate");
keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
```

<span data-ttu-id="e81fa-202">The search query is then submitted to SharePoint by calling the  **ExecuteQuery_Client(Query)** method.</span><span class="sxs-lookup"><span data-stu-id="e81fa-202">The search query is then submitted to SharePoint by calling the  **ExecuteQuery_Client(Query)** method.</span></span> <span data-ttu-id="e81fa-203">Results are returned to the **ClientResult<T&gt;** object.</span><span class="sxs-lookup"><span data-stu-id="e81fa-203">Results are returned to the **ClientResult<T&gt;** object.</span></span>

```
SearchExecutor searchExec = new SearchExecutor(ctx);
ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
ctx.ExecuteQuery();
```

<span data-ttu-id="e81fa-204">The  **FormatResults** method iterates through the results and constructs an HTML table to display the result values.</span><span class="sxs-lookup"><span data-stu-id="e81fa-204">The  **FormatResults** method iterates through the results and constructs an HTML table to display the result values.</span></span>

```
string responseHtml = "<h3>Results</h3>";
responseHtml += "<table>";
responseHtml += "<tr><th>Title</th><th>Site URL</th><th>Description</th><th>Template</th></tr>";
if (results.Value[0].RowCount > 0)
{
 foreach (var row in results.Value[0].ResultRows)
 {
   responseHtml += "<tr>";
   responseHtml += string.Format("<td>{0}</td>", row["Title"] != null ? row["Title"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["SPSiteUrl"] != null ? row["SPSiteUrl"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["Description"] != null ? row["Description"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["WebTemplate"] != null ? row["WebTemplate"].ToString() : "");
   responseHtml += "</tr>";
 }
}
responseHtml += "</table>";
```

<span data-ttu-id="e81fa-205">The  **ResolveAdditionalFilter** method checks for "Apptest".</span><span class="sxs-lookup"><span data-stu-id="e81fa-205">The  **ResolveAdditionalFilter** method checks for "Apptest".</span></span> <span data-ttu-id="e81fa-206">If it is found, a list of site templates of any type is returned in the search results.</span><span class="sxs-lookup"><span data-stu-id="e81fa-206">If it is found, a list of site templates of any type is returned in the search results.</span></span> <span data-ttu-id="e81fa-207">If it is not found, only STS web templates are returned in the search results.</span><span class="sxs-lookup"><span data-stu-id="e81fa-207">If it is not found, only STS web templates are returned in the search results.</span></span>

```
private string ResolveAdditionalFilter(string aboutMeValue)
{
    if (!aboutMeValue.Contains("AppTest"))
    {
        return "WebTemplate=STS";
    }
    return "";
}
```

<span data-ttu-id="e81fa-208">The example then constructs the query and calls the  **ProcessQuery** and **FormatResults** methods to retrieve, format, and display the search results.</span><span class="sxs-lookup"><span data-stu-id="e81fa-208">The example then constructs the query and calls the  **ProcessQuery** and **FormatResults** methods to retrieve, format, and display the search results.</span></span>

```
string query = "contentclass:\"STS_Site\" " + templateFilter;
ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
lblStatus2.Text = FormatResults(results);
```

<span data-ttu-id="e81fa-209">You can see the UI for this example in the following figure.</span><span class="sxs-lookup"><span data-stu-id="e81fa-209">You can see the UI for this example in the following figure.</span></span>

<span data-ttu-id="e81fa-210">**Figure 8. Personalized search results sample UI**</span><span class="sxs-lookup"><span data-stu-id="e81fa-210">**Figure 8. Personalized search results sample UI**</span></span>

![Personalized search results sample UI](media/search-customizations-for-sharepoint/8e1c412b-71a7-42e2-b9f3-b7d045df3bde.png)

## <a name="search-configuration-portability"></a><span data-ttu-id="e81fa-212">Search configuration portability</span><span class="sxs-lookup"><span data-stu-id="e81fa-212">Search configuration portability</span></span>

<span data-ttu-id="e81fa-213">In SharePoint 2013 and SharePoint Online, you can export and import customized search configuration settings between site collections and sites.</span><span class="sxs-lookup"><span data-stu-id="e81fa-213">In SharePoint 2013 and SharePoint Online, you can export and import customized search configuration settings between site collections and sites.</span></span> <span data-ttu-id="e81fa-214">You can only export customized search configuration settings at the Search service application (SSA) level, and you have to use the search APIs to do this programmatically.</span><span class="sxs-lookup"><span data-stu-id="e81fa-214">You can only export customized search configuration settings at the Search service application (SSA) level, and you have to use the search APIs to do this programmatically.</span></span> <span data-ttu-id="e81fa-215">The export option is not available in the SharePoint UI.</span><span class="sxs-lookup"><span data-stu-id="e81fa-215">The export option is not available in the SharePoint UI.</span></span>

<span data-ttu-id="e81fa-216">The [SharePoint 2013: Import and Export search settings for SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) sample show how to import and export search settings for a SharePoint Online site using the search CSOM in a console application.</span><span class="sxs-lookup"><span data-stu-id="e81fa-216">The [SharePoint 2013: Import and Export search settings for SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) sample show how to import and export search settings for a SharePoint Online site using the search CSOM in a console application.</span></span>

### <a name="configuration-settings-that-are-portable"></a><span data-ttu-id="e81fa-217">Configuration settings that are portable</span><span class="sxs-lookup"><span data-stu-id="e81fa-217">Configuration settings that are portable</span></span>

<span data-ttu-id="e81fa-218">When you export customized search configuration settings, SharePoint 2013 creates a search configuration file in XML format.</span><span class="sxs-lookup"><span data-stu-id="e81fa-218">When you export customized search configuration settings, SharePoint 2013 creates a search configuration file in XML format.</span></span> <span data-ttu-id="e81fa-219">This search configuration file includes all exportable customized search configuration settings at the SSA, site collection, or site level from where you start the export.</span><span class="sxs-lookup"><span data-stu-id="e81fa-219">This search configuration file includes all exportable customized search configuration settings at the SSA, site collection, or site level from where you start the export.</span></span> <span data-ttu-id="e81fa-220">A search configuration file for a site collection does not contain search configuration settings from the individual sites within the site collection.</span><span class="sxs-lookup"><span data-stu-id="e81fa-220">A search configuration file for a site collection does not contain search configuration settings from the individual sites within the site collection.</span></span>

<span data-ttu-id="e81fa-221">When you import a search configuration file, SharePoint 2013 creates and enables each customized search configuration setting in the site collection or site from where you start the import.</span><span class="sxs-lookup"><span data-stu-id="e81fa-221">When you import a search configuration file, SharePoint 2013 creates and enables each customized search configuration setting in the site collection or site from where you start the import.</span></span>

<span data-ttu-id="e81fa-222">Table 1 lists the settings that you can export and import and any dependencies on other customized search configuration settings.</span><span class="sxs-lookup"><span data-stu-id="e81fa-222">Table 1 lists the settings that you can export and import and any dependencies on other customized search configuration settings.</span></span> <span data-ttu-id="e81fa-223">If the customized search configuration settings depend on a customized search configuration setting at a different level, you must export and import settings at all relevant levels.</span><span class="sxs-lookup"><span data-stu-id="e81fa-223">If the customized search configuration settings depend on a customized search configuration setting at a different level, you must export and import settings at all relevant levels.</span></span>

<span data-ttu-id="e81fa-224">**Table 1. Search settings that you can export and import**</span><span class="sxs-lookup"><span data-stu-id="e81fa-224">**Table 1. Search settings that you can export and import**</span></span>

|<span data-ttu-id="e81fa-225">**Configuration setting**</span><span class="sxs-lookup"><span data-stu-id="e81fa-225">**Configuration setting**</span></span>|<span data-ttu-id="e81fa-226">**Dependencies**</span><span class="sxs-lookup"><span data-stu-id="e81fa-226">**Dependencies**</span></span>|
|:-----|:-----|
|<span data-ttu-id="e81fa-227">Query rules, including result blocs, promoted results, and user segments</span><span class="sxs-lookup"><span data-stu-id="e81fa-227">Query rules, including result blocs, promoted results, and user segments</span></span>|<span data-ttu-id="e81fa-228">Result sources, result types, search schema, ranking model</span><span class="sxs-lookup"><span data-stu-id="e81fa-228">Result sources, result types, search schema, ranking model</span></span>|
|<span data-ttu-id="e81fa-229">Result sources</span><span class="sxs-lookup"><span data-stu-id="e81fa-229">Result sources</span></span>|<span data-ttu-id="e81fa-230">Search schema</span><span class="sxs-lookup"><span data-stu-id="e81fa-230">Search schema</span></span>|
|<span data-ttu-id="e81fa-231">Result types</span><span class="sxs-lookup"><span data-stu-id="e81fa-231">Result types</span></span>|<span data-ttu-id="e81fa-232">Search schema, result sources, display templates</span><span class="sxs-lookup"><span data-stu-id="e81fa-232">Search schema, result sources, display templates</span></span>|
|<span data-ttu-id="e81fa-233">Search schema</span><span class="sxs-lookup"><span data-stu-id="e81fa-233">Search schema</span></span>|<span data-ttu-id="e81fa-234">Keine</span><span class="sxs-lookup"><span data-stu-id="e81fa-234">None</span></span>|
|<span data-ttu-id="e81fa-235">Ranking model</span><span class="sxs-lookup"><span data-stu-id="e81fa-235">Ranking model</span></span>|<span data-ttu-id="e81fa-236">Search schema</span><span class="sxs-lookup"><span data-stu-id="e81fa-236">Search schema</span></span>|

<span data-ttu-id="e81fa-237">You can export customized search configuration settings from an SSA and import the settings to site collections and sites.</span><span class="sxs-lookup"><span data-stu-id="e81fa-237">You can export customized search configuration settings from an SSA and import the settings to site collections and sites.</span></span> <span data-ttu-id="e81fa-238">But you can't import customized search configuration settings to an SSA.</span><span class="sxs-lookup"><span data-stu-id="e81fa-238">But you can't import customized search configuration settings to an SSA.</span></span> <span data-ttu-id="e81fa-239">You also can't export the default search configuration settings.</span><span class="sxs-lookup"><span data-stu-id="e81fa-239">You also can't export the default search configuration settings.</span></span>

<span data-ttu-id="e81fa-240">At the site or site collection level, you can export or import search configuration settings by using the SharePoint UI.</span><span class="sxs-lookup"><span data-stu-id="e81fa-240">At the site or site collection level, you can export or import search configuration settings by using the SharePoint UI.</span></span> <span data-ttu-id="e81fa-241">These settings are located in the  **Search** section of the **Site Settings** page.</span><span class="sxs-lookup"><span data-stu-id="e81fa-241">These settings are located in the  **Search** section of the **Site Settings** page.</span></span>

<span data-ttu-id="e81fa-242">**Site Settings - Search**</span><span class="sxs-lookup"><span data-stu-id="e81fa-242">**Site Settings - Search**</span></span>

![Site Settings - Search](media/search-customizations-for-sharepoint/ada14bf4-d721-4974-ad50-a1f8ce01933f.png)

<span data-ttu-id="e81fa-244">These settings are also available in the  **Site Collection Administration** section.</span><span class="sxs-lookup"><span data-stu-id="e81fa-244">These settings are also available in the  **Site Collection Administration** section.</span></span> <span data-ttu-id="e81fa-245">Alternatively, you can programmatically import and export these settings by using the SharePoint 2013 search CSOM.</span><span class="sxs-lookup"><span data-stu-id="e81fa-245">Alternatively, you can programmatically import and export these settings by using the SharePoint 2013 search CSOM.</span></span>

### <a name="search-configuration-files"></a><span data-ttu-id="e81fa-246">Search configuration files</span><span class="sxs-lookup"><span data-stu-id="e81fa-246">Search configuration files</span></span>

<span data-ttu-id="e81fa-247">The following table lists schema files that support a search configuration.</span><span class="sxs-lookup"><span data-stu-id="e81fa-247">The following table lists schema files that support a search configuration.</span></span> <span data-ttu-id="e81fa-248">For information about the schema format, see [Share Point search settings portability schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e81fa-248">For information about the schema format, see [Share Point search settings portability schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span></span>

> [!NOTE] 
> <span data-ttu-id="e81fa-249">You can download the schema files from [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip).</span><span class="sxs-lookup"><span data-stu-id="e81fa-249">You can download the schema files from [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip).</span></span> 

<span data-ttu-id="e81fa-250">**Table 2. Search settings portability schemas**</span><span class="sxs-lookup"><span data-stu-id="e81fa-250">**Table 2. Search settings portability schemas**</span></span>

|<span data-ttu-id="e81fa-251">**Schema**</span><span class="sxs-lookup"><span data-stu-id="e81fa-251">**Schema**</span></span>|<span data-ttu-id="e81fa-252">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="e81fa-252">**Description**</span></span>|
|:-----|:-----|
|[<span data-ttu-id="e81fa-253">SPS15XSDSearchSet1</span><span class="sxs-lookup"><span data-stu-id="e81fa-253">SPS15XSDSearchSet1</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639116%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-254">Specifies XML that represents result sources.</span><span class="sxs-lookup"><span data-stu-id="e81fa-254">Specifies XML that represents result sources.</span></span>|
|[<span data-ttu-id="e81fa-255">SPS15XSDSearchSet2</span><span class="sxs-lookup"><span data-stu-id="e81fa-255">SPS15XSDSearchSet2</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639118%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-256">Specifies XML that represents administrative types and members for managing an SSA search instance.</span><span class="sxs-lookup"><span data-stu-id="e81fa-256">Specifies XML that represents administrative types and members for managing an SSA search instance.</span></span> <span data-ttu-id="e81fa-257">This includes result item types and property rule settings.</span><span class="sxs-lookup"><span data-stu-id="e81fa-257">This includes result item types and property rule settings.</span></span>|
|[<span data-ttu-id="e81fa-258">SPS15XSDSearchSet3</span><span class="sxs-lookup"><span data-stu-id="e81fa-258">SPS15XSDSearchSet3</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639120%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-259">Specifies XML that represents settings that include query rules, result sources, managed properties, crawled properties, and ranking models.</span><span class="sxs-lookup"><span data-stu-id="e81fa-259">Specifies XML that represents settings that include query rules, result sources, managed properties, crawled properties, and ranking models.</span></span>|
|[<span data-ttu-id="e81fa-260">SPS15XSDSearchSet4</span><span class="sxs-lookup"><span data-stu-id="e81fa-260">SPS15XSDSearchSet4</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639117%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-261">Specifies XML that represents enumerations used in other schemas.</span><span class="sxs-lookup"><span data-stu-id="e81fa-261">Specifies XML that represents enumerations used in other schemas.</span></span>|
|[<span data-ttu-id="e81fa-262">SPS15XSDSearchSet5</span><span class="sxs-lookup"><span data-stu-id="e81fa-262">SPS15XSDSearchSet5</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639119%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-263">Specifies XML that represents enumerations like  **ResultType** that are used in other schemas.</span><span class="sxs-lookup"><span data-stu-id="e81fa-263">Specifies XML that represents enumerations like  **ResultType** that are used in other schemas.</span></span>|
|[<span data-ttu-id="e81fa-264">SPS15XSDSearchSet6</span><span class="sxs-lookup"><span data-stu-id="e81fa-264">SPS15XSDSearchSet6</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639115%28v=office.15%29.aspx)|<span data-ttu-id="e81fa-265">Specifies XML that represents enumerations used in the  **Microsoft.Office.Server.Search.Administration** schema.</span><span class="sxs-lookup"><span data-stu-id="e81fa-265">Specifies XML that represents enumerations used in the  **Microsoft.Office.Server.Search.Administration** schema.</span></span>|

### <a name="using-csom-to-port-configuration-settings"></a><span data-ttu-id="e81fa-266">Using CSOM to port configuration settings</span><span class="sxs-lookup"><span data-stu-id="e81fa-266">Using CSOM to port configuration settings</span></span>

<span data-ttu-id="e81fa-267">The CSOM APIs that you need in order to import and export your search configuration settings are in the  **SearchConfigurationPortability** class in the **Microsoft.SharePoint.Client.Search.Portability** namespace.</span><span class="sxs-lookup"><span data-stu-id="e81fa-267">The CSOM APIs that you need in order to import and export your search configuration settings are in the  **SearchConfigurationPortability** class in the **Microsoft.SharePoint.Client.Search.Portability** namespace.</span></span>

<span data-ttu-id="e81fa-268">The following code example shows how to export a site's search configuration settings.</span><span class="sxs-lookup"><span data-stu-id="e81fa-268">The following code example shows how to export a site's search configuration settings.</span></span>

```
private static void ExportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   ClientResult<string> configresults = sconfig.ExportSearchConfiguration(owner);
   context.ExecuteQuery();
   string results = configresults.Value;
   System.IO.File.WriteAllText(settingsFile, results);
}
```

<span data-ttu-id="e81fa-269">The following code shows how to import a site's search configuration settings.</span><span class="sxs-lookup"><span data-stu-id="e81fa-269">The following code shows how to import a site's search configuration settings.</span></span>

```
private static void ImportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   sconfig.ImportSearchConfiguration(owner, System.IO.File.ReadAllText(settingsFile));
   context.ExecuteQuery();            
}
```

## <a name="see-also"></a><span data-ttu-id="e81fa-270">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e81fa-270">See also</span></span>
<span data-ttu-id="e81fa-271"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e81fa-271"></span></span>

- [<span data-ttu-id="e81fa-272">Search solutions in SharePoint 2013 and SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e81fa-272">Search solutions in SharePoint 2013 and SharePoint Online</span></span>](search-solutions-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="e81fa-273">SharePoint 2013: Import and Export search settings for SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e81fa-273">SharePoint 2013: Import and Export search settings for SharePoint Online</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac)
    
- [<span data-ttu-id="e81fa-274">SharePoint 2013: Personalizing search results in a SharePoint Add-in</span><span class="sxs-lookup"><span data-stu-id="e81fa-274">SharePoint 2013: Personalizing search results in a SharePoint Add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9)
