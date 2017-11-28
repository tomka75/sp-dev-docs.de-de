---
title: "Durchsuchen von Anpassungen für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c8afb3e0589e65e100ca3512926e931e966e510a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="search-customizations-for-sharepoint"></a><span data-ttu-id="7f430-102">Durchsuchen von Anpassungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f430-102">Search customizations for SharePoint</span></span>

<span data-ttu-id="7f430-103">Erstellen Sie benutzerdefinierte SharePoint 2013 und SharePoint Online-Suche Szenarien mithilfe von suchbasierten Websiteverzeichnis und eine personalisierte Suche, oder suchen Sie Konfiguration Portabilität.</span><span class="sxs-lookup"><span data-stu-id="7f430-103">Create customized SharePoint 2013 and SharePoint Online search scenarios by using a search-based site directory, personalized search, or search configuration portability.</span></span> 

<span data-ttu-id="7f430-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="7f430-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

## <a name="search-based-site-directory"></a><span data-ttu-id="7f430-105">Suchbasierte Websiteverzeichnis</span><span class="sxs-lookup"><span data-stu-id="7f430-105">Search-based site directory</span></span>

<span data-ttu-id="7f430-106">SharePoint-Suche können Sie eine suchbasierte Websiteverzeichnis ohne Schreiben von benutzerdefiniertem Code erstellen.</span><span class="sxs-lookup"><span data-stu-id="7f430-106">SharePoint search enables you to create a search-based site directory without writing any custom code.</span></span> 

<span data-ttu-id="7f430-107">So erstellen Sie ein Websiteverzeichnis</span><span class="sxs-lookup"><span data-stu-id="7f430-107">To create a site directory:</span></span>

1. <span data-ttu-id="7f430-108">Erstellen der Website Directory Anzeigevorlagen.</span><span class="sxs-lookup"><span data-stu-id="7f430-108">Create the site directory display templates.</span></span>
    
2. <span data-ttu-id="7f430-109">Definieren Sie den Site Directory Ergebnistyp.</span><span class="sxs-lookup"><span data-stu-id="7f430-109">Define the site directory result type.</span></span>
    
3. <span data-ttu-id="7f430-110">Erstellen der Ergebnisseite an.</span><span class="sxs-lookup"><span data-stu-id="7f430-110">Create the results page.</span></span>
    
4. <span data-ttu-id="7f430-111">Bearbeiten Sie die Eigenschaften des Suchergebnisse-Webpart.</span><span class="sxs-lookup"><span data-stu-id="7f430-111">Edit the Results Web Part properties.</span></span>
    
<span data-ttu-id="7f430-112">Zum Erstellen der Website Directory Anzeigevorlagen:</span><span class="sxs-lookup"><span data-stu-id="7f430-112">To create the site directory display templates:</span></span>

<span data-ttu-id="7f430-113">**Hinweis:**  Dieses Verfahren verwendet die Website bezogenen Anzeigevorlagen unverändert.</span><span class="sxs-lookup"><span data-stu-id="7f430-113">**Note:**  This procedure uses the site-related display templates without modification.</span></span> <span data-ttu-id="7f430-114">Wenn Sie ändern, wie Site Directory Ergebnisse angezeigt werden, ändern die Anzeigevorlagen, die Sie erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="7f430-114">If you want to change how site directory results are displayed, modify the display templates that you create.</span></span>

1. <span data-ttu-id="7f430-115">Öffnen Sie das den **Gestaltungsvorlagenkatalog**zugeordnetes Netzwerklaufwerk.</span><span class="sxs-lookup"><span data-stu-id="7f430-115">Open the mapped network drive to the  **Master Page Gallery**.</span></span> <span data-ttu-id="7f430-116">Weitere Informationen finden Sie unter [wie: Zuordnen eines Netzlaufwerks zum SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f430-116">For more information, see [How to: Map a network drive to the SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span></span>
    
2. <span data-ttu-id="7f430-117">Erstellen Sie Kopien der Anzeigevorlage HTML-Dateien, die am besten zuordnen, was Sie tun möchten.</span><span class="sxs-lookup"><span data-stu-id="7f430-117">Make copies of the display template HTML files that best map what you're trying to do.</span></span> <span data-ttu-id="7f430-118">Für die Website verzeichnisszenario wird dies Item_Site.html und Item_Site_HoverPanel.html sein.</span><span class="sxs-lookup"><span data-stu-id="7f430-118">For the site directory scenario, this will be Item_Site.html and Item_Site_HoverPanel.html.</span></span> <span data-ttu-id="7f430-119">Beide Dateien befinden sich der `\Display Templates\Search` Ordner in der zugeordnetes Netzwerklaufwerk.</span><span class="sxs-lookup"><span data-stu-id="7f430-119">Both files are located in the  `\Display Templates\Search` folder in the mapped network drive.</span></span>
    
3. <span data-ttu-id="7f430-120">Benennen Sie die Kopien, die Sie der Item_SiteDirectory.html und Item_SiteDirectory_HoverPanel.html-Dateien vorgenommen, wie dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-120">Rename the copies that you made of the Item_SiteDirectory.html and Item_SiteDirectory_HoverPanel.html files as shown.</span></span>
    
    <span data-ttu-id="7f430-121">**Abbildung 1. Site Directory Anzeigevorlagen**</span><span class="sxs-lookup"><span data-stu-id="7f430-121">**Figure 1. Site directory display templates**</span></span>

    ![Site Directory Anzeigevorlagen](media/search-customizations-for-sharepoint/4c084d31-bad4-45f0-950b-ba214f9487f7.png)

4. <span data-ttu-id="7f430-123">Öffnen Sie die Datei Item_SiteDirectory.html, und stellen Sie wie folgt geändert:</span><span class="sxs-lookup"><span data-stu-id="7f430-123">Open the Item_SiteDirectory.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="7f430-124">Ändern der `<title>` Wert von "Websiteelements" bis "Websiteverzeichnis" markieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-124">Change the  `<title>` tag value from "Site Item" to "Site Directory".</span></span>
    
    - <span data-ttu-id="7f430-125">Ändern Sie die erste `<div>` Tag nach dem öffnenden `<body>` Markieren von `<div id="Item_Site">` auf `<div id="Item_SiteDirectory">`.</span><span class="sxs-lookup"><span data-stu-id="7f430-125">Change the first  `<div>` tag after the opening `<body>` tag from `<div id="Item_Site">` to `<div id="Item_SiteDirectory">`.</span></span>
    
    - <span data-ttu-id="7f430-126">Ändern der beim Daraufzeigen Systemsteuerung Vorlage JavaScript-Datei des Anzeigenamens von: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`an:`var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span><span class="sxs-lookup"><span data-stu-id="7f430-126">Change the hover panel display template JavaScript file name from: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`to: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span></span>
    
5. <span data-ttu-id="7f430-127">Öffnen Sie die Datei Item_SiteDirectory_HoverPanel.html, und stellen Sie wie folgt geändert:</span><span class="sxs-lookup"><span data-stu-id="7f430-127">Open the Item_SiteDirectory_HoverPanel.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="7f430-128">Ändern der `<div>` Tag nach dem öffnenden `<body>` markieren aus: `<title>Site Hover Panel Test</title>`an:`<title>Site Directory Hover Panel</title>`</span><span class="sxs-lookup"><span data-stu-id="7f430-128">Change the  `<div>` tag following the opening `<body>` tag from: `<title>Site Hover Panel Test</title>`to: `<title>Site Directory Hover Panel</title>`</span></span>
    
    - <span data-ttu-id="7f430-129">Ändern der `<title>` markieren aus: `<div id="Item_Site_HoverPanel">`an:`<div id="Item_SiteDirectory_HoverPanel">`</span><span class="sxs-lookup"><span data-stu-id="7f430-129">Change the  `<title>` tag from: `<div id="Item_Site_HoverPanel">`to: `<div id="Item_SiteDirectory_HoverPanel">`</span></span>
    
<span data-ttu-id="7f430-130">So definieren Sie den Website Directory Ergebnistyp</span><span class="sxs-lookup"><span data-stu-id="7f430-130">To define the site directory result type:</span></span>

1. <span data-ttu-id="7f430-131">Wechseln Sie zu **Websiteeinstellungen** > **Suche** > **Ergebnistypen**, und klicken Sie dann auf **Neuer Ergebnistyp**.</span><span class="sxs-lookup"><span data-stu-id="7f430-131">Go to  **Site Settings** > **Search** > **Result Types**, and then choose  **New Result Type**.</span></span>
    
2. <span data-ttu-id="7f430-132">Name des neuen Ergebnistyps "Grundlegende Websiteverzeichnis".</span><span class="sxs-lookup"><span data-stu-id="7f430-132">Name your new result type "Basic Site Directory".</span></span>
    
3. <span data-ttu-id="7f430-133">In der **wie sollen diese Ergebnisse aussehen?** **Websiteverzeichnis**wählen Sie im Feld.</span><span class="sxs-lookup"><span data-stu-id="7f430-133">In the  **What should these results look like?** box, select **Site Directory**.</span></span>
    
    <span data-ttu-id="7f430-134">**Abbildung 2. Ergebnis Standortkonfiguration**</span><span class="sxs-lookup"><span data-stu-id="7f430-134">**Figure 2. Site result configuration**</span></span>

    ![Beispiel für Ergebnis Standortkonfiguration](media/search-customizations-for-sharepoint/4f42a7c4-326b-4508-b9a7-e030ef34cd33.png)

4. <span data-ttu-id="7f430-136">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="7f430-136">Choose  **Save**.</span></span>
    
<span data-ttu-id="7f430-137">Auf die Ergebnisseite zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="7f430-137">To create the results page:</span></span>

1. <span data-ttu-id="7f430-138">Klicken Sie im Menü **Einstellungen** **auf Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="7f430-138">On the  **Site Settings** menu, select **Site contents**.</span></span>
    
2. <span data-ttu-id="7f430-139">Wählen Sie **Seiten**.</span><span class="sxs-lookup"><span data-stu-id="7f430-139">Select  **Pages**.</span></span>
    
3. <span data-ttu-id="7f430-140">Wählen Sie in der Bibliothek für **Seiten** , **Dateien** > **Neues Dokument** > **Seite**.</span><span class="sxs-lookup"><span data-stu-id="7f430-140">In the  **Pages** library, select **Files** > **New Document** > **Page**.</span></span>
    
4. <span data-ttu-id="7f430-141">Geben Sie auf der Seite **Seite erstellen** "Websiteverzeichnis" für den **Titel** und "Sitedirectory" für **URL-Name**.</span><span class="sxs-lookup"><span data-stu-id="7f430-141">On the  **Create Page** page, specify "Site Directory" for **Title** and "sitedirectory" for **URL Name**.</span></span>
    
5. <span data-ttu-id="7f430-142">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="7f430-142">Choose  **Create**.</span></span>
    
<span data-ttu-id="7f430-143">So bearbeiten Sie die Eigenschaften des Suchergebnisse-Webpart</span><span class="sxs-lookup"><span data-stu-id="7f430-143">To edit the Results Web Part properties:</span></span>

1. <span data-ttu-id="7f430-144">Wählen Sie auf der Seite **Websiteverzeichnis** **Einstellungen** > **Seite bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="7f430-144">On the  **Site Directory** page, choose **Settings** > **Edit Page**.</span></span>
    
2. <span data-ttu-id="7f430-145">Wählen Sie in den **Suchergebnisse-Webpart**im **Webpart** -Menü, und wählen Sie dann auf **Webpart bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="7f430-145">In the  **Search Results Web Part**, choose the  **Web Part** menu, and then choose **Edit Web Part**.</span></span>
    
    <span data-ttu-id="7f430-146">**Abbildung 3. Webpart-Menü**</span><span class="sxs-lookup"><span data-stu-id="7f430-146">**Figure 3. Web Part menu**</span></span>

    ![Abb. 3](media/search-customizations-for-sharepoint/1b01ac59-3bc1-42eb-a63d-61c2ad15cee4.png)

3. <span data-ttu-id="7f430-148">Wählen Sie im Webpart-Toolbereich **Abfrage ändern** , um den Abfrage-Generator zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="7f430-148">In the Web Part tool pane, choose  **Change query** to open the Query Builder.</span></span>
    
4. <span data-ttu-id="7f430-149">Geben Sie im Feld **Abfragetext** Folgendes ein:`ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span><span class="sxs-lookup"><span data-stu-id="7f430-149">In the  **Query text** field, enter the following: `ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span></span>
    
5. <span data-ttu-id="7f430-150">Wählen Sie die **Abfrage testen** zu bestätigen, dass die Syntax korrekt ist.</span><span class="sxs-lookup"><span data-stu-id="7f430-150">Choose  **Test query** to confirm that the syntax is correct.</span></span> <span data-ttu-id="7f430-151">**Search Results** Vorschaubereich sollte Unterwebsites der Website angezeigt werden, die Sie für den _Pfad_ des **Abfragetext**angegeben.</span><span class="sxs-lookup"><span data-stu-id="7f430-151">The **Search Results Preview** pane should display subsites within the site you specified for _path_ in the **Query text**.</span></span>
    
    <span data-ttu-id="7f430-152">**Abbildung 4. Search Results-Webpart-Abfrage-Generator**</span><span class="sxs-lookup"><span data-stu-id="7f430-152">**Figure 4. Search results Web Part query builder**</span></span>

    ![Search Results Webpart Abfrage-Generator](media/search-customizations-for-sharepoint/7b55c821-4772-4874-bbcb-c757e2723599.png)

6. <span data-ttu-id="7f430-154">Wählen Sie **OK** , um den Abfrage-Generator zu schließen.</span><span class="sxs-lookup"><span data-stu-id="7f430-154">Choose  **OK** to close the Query Builder.</span></span>
    
7. <span data-ttu-id="7f430-155">Wählen Sie im **Anzeigevorlagen** **Ergebnistypen zum Anzeigen von Elementen verwenden**.</span><span class="sxs-lookup"><span data-stu-id="7f430-155">In  **Display Templates**, select  **Use result types to display items**.</span></span>
    
8. <span data-ttu-id="7f430-156">Wählen Sie in der Dropdownliste **Ergebnistyp für Artikel** **Grundlegende Websiteverzeichnis** .</span><span class="sxs-lookup"><span data-stu-id="7f430-156">Select  **Basic Site Directory** in the **Result type for item** drop-down list.</span></span>
    
9. <span data-ttu-id="7f430-157">Klicken Sie im Abschnitt **Darstellung** ändern Sie den **Titel** in "sind Websites ich Zugriff auf".</span><span class="sxs-lookup"><span data-stu-id="7f430-157">In the  **Appearance** section, change the **Title** to "Sites I have access to".</span></span>
    
10. <span data-ttu-id="7f430-158">Wählen Sie **OK** , um die Änderungen am Webpart zu speichern und schließen den Webpart-Toolbereich.</span><span class="sxs-lookup"><span data-stu-id="7f430-158">Choose  **OK** to save the changes to the Web Part and to close the Web Part tool pane.</span></span> <span data-ttu-id="7f430-159">Die folgende Abbildung zeigt ein Beispiel für eine suchbasierte Directory Websiteseite.</span><span class="sxs-lookup"><span data-stu-id="7f430-159">The following figure shows an example of a search-based site directory page.</span></span>
    
    <span data-ttu-id="7f430-160">**Abbildung 5. Beispiel für Contoso suchbasierte Website-Verzeichnis**</span><span class="sxs-lookup"><span data-stu-id="7f430-160">**Figure 5. Contoso search-based site directory example**</span></span>

    ![Beispiel für Contoso suchbasierte Website-Verzeichnis](media/search-customizations-for-sharepoint/5d1317d5-2e82-4819-b5a4-5bb515898a7b.png)

## <a name="personalized-search-results"></a><span data-ttu-id="7f430-162">Personalisierte Suchergebnisse</span><span class="sxs-lookup"><span data-stu-id="7f430-162">Personalized search results</span></span>

<span data-ttu-id="7f430-163">Personalisierte Suche ist beim Anzeigen von Suchergebnissen angegeben, an den Benutzer senden von der Suchanfrage vorgesehen sind.</span><span class="sxs-lookup"><span data-stu-id="7f430-163">Personalized search is when you show search results targeted to the user submitting the search request.</span></span> <span data-ttu-id="7f430-164">Dieser Abschnitt beschreibt einige Szenarien für personalisierte Such- und wie Sie sie implementieren können.</span><span class="sxs-lookup"><span data-stu-id="7f430-164">This section describes some scenarios for personalized search and how you might implement them.</span></span>

### <a name="your-news-scenario"></a><span data-ttu-id="7f430-165">Die News-Szenario</span><span class="sxs-lookup"><span data-stu-id="7f430-165">Your news scenario</span></span>

<span data-ttu-id="7f430-166">In diesem Szenario erstellen Sie ein Search-add-in, das relevante Inhalte, wie Nachrichten und Ereignisse, geplant, für den Benutzer anzeigt.</span><span class="sxs-lookup"><span data-stu-id="7f430-166">In this scenario, you create a search add-in that shows relevant content, such as news and events, targeted to the user.</span></span>

<span data-ttu-id="7f430-167">**Abbildung 6. Ihr News personalisierte Search-Szenario**</span><span class="sxs-lookup"><span data-stu-id="7f430-167">**Figure 6. Your News personalized search scenario**</span></span>

![Ihr News personalisierte Search-Szenario](media/search-customizations-for-sharepoint/188af4d1-b8bb-4212-bfdb-c29a13f30286.png)

<span data-ttu-id="7f430-169">Um die News-Szenario zu implementieren, mit der die SharePoint-Suchergebnisse-Webparts und Anzeigevorlagen standardmäßig die News-Informationen, einschließlich Titel, Beschreibung und rollupbild angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7f430-169">To implement the news scenario, use the SharePoint search results Web Part and default display templates to display the news information, including title, description, and rollup image.</span></span> <span data-ttu-id="7f430-170">Die ersten 10 Elemente News anzeigen.</span><span class="sxs-lookup"><span data-stu-id="7f430-170">Show the first 10 news items.</span></span> <span data-ttu-id="7f430-171">Wenn der Benutzer die rollupbild, Titel oder mehr lesen Link klickt, wird die Seite Neuigkeiten Artikel geladen.</span><span class="sxs-lookup"><span data-stu-id="7f430-171">When the user chooses the rollup image, title, or Read More link, the news article page is loaded.</span></span>

<span data-ttu-id="7f430-172">Alternativ können Sie eine Suche-add-Ins mithilfe der Abfrage-API (CSOM oder REST) erstellen.</span><span class="sxs-lookup"><span data-stu-id="7f430-172">Alternatively, you can create a search add-in using the query API (CSOM or REST).</span></span> <span data-ttu-id="7f430-173">Sie können die Anzahl der Nachrichtenelementen anzuzeigende mithilfe des add-ins Sucheigenschaften konfigurierbar machen.</span><span class="sxs-lookup"><span data-stu-id="7f430-173">You can make the number of news items to be displayed configurable by using the search add-in properties.</span></span>

<span data-ttu-id="7f430-174">Eine weitere Option ist mit der Abfrage-API die Abfrage-API-Code hinzufügen, der die Suchergebnisse direkt auf das Seitenlayout abruft.</span><span class="sxs-lookup"><span data-stu-id="7f430-174">Another option is to use the query API to add the query API code that retrieves the search results directly to the page layout.</span></span>

<span data-ttu-id="7f430-175">News und Ereignis Informationen, die speziell für den Benutzer angezeigt:</span><span class="sxs-lookup"><span data-stu-id="7f430-175">To display the news and event information specific to the user:</span></span>

1. <span data-ttu-id="7f430-176">Ändern der Abfrage zum Filtern von Nachrichten und Ereignis Ergebnisse basierend auf Benutzerprofileigenschaften wie Unternehmenseinheit, Region und Sprache.</span><span class="sxs-lookup"><span data-stu-id="7f430-176">Modify the query to filter news and event results based on user profile properties like business unit, region, and language.</span></span>
    
2. <span data-ttu-id="7f430-177">Abrufen der Titel, Beschreibung, rollupbild und URL-Eigenschaften für die Elemente News oder Ereignis.</span><span class="sxs-lookup"><span data-stu-id="7f430-177">Retrieve the Title, Description, rollup image, and URL properties for the news or event items.</span></span>
    
3. <span data-ttu-id="7f430-178">Sortieren der Logik für die kombinierte Neuigkeiten und Ereignisse, die auf Basis der **LastModifiedDate** -Eigenschaft implementieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-178">Implement sorting logic for the combined news and events based on the  **LastModifiedDate** property.</span></span>

### <a name="upcoming-events-scenario"></a><span data-ttu-id="7f430-179">Anstehende Ereignisse-Szenario</span><span class="sxs-lookup"><span data-stu-id="7f430-179">Upcoming events scenario</span></span>

<span data-ttu-id="7f430-180">In diesem Szenario zeigt die Search-add-ins relevanten Ereignisse geplant, für den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="7f430-180">In this scenario, the search add-in shows relevant events targeted to the user.</span></span>

<span data-ttu-id="7f430-181">**Abbildung 7. Anstehende Ereignisse personalisierte Search-Szenario**</span><span class="sxs-lookup"><span data-stu-id="7f430-181">**Figure 7. Upcoming Events personalized search scenario**</span></span>

![Anstehende Ereignisse personalisierte Search-Szenario](media/search-customizations-for-sharepoint/35afac63-b4e9-4d94-abc1-a5fa11cc2dbf.png)

<span data-ttu-id="7f430-183">Zum Implementieren dieses Szenarios können Sie die SharePoint-Suchergebnisse-Webpart so ändern Sie die Abfrage aus, um nur in Kürze verfügbare Ereignisinformationen abrufen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-183">To implement this scenario, you can configure the SharePoint search results Web Part to change the query to only retrieve upcoming event information.</span></span> <span data-ttu-id="7f430-184">Geben Sie hierzu `ContentClass:STS_ListItem_Events` für das Webpart Abfragetext.</span><span class="sxs-lookup"><span data-stu-id="7f430-184">To do this, specify  `ContentClass:STS_ListItem_Events` for the Web Part's query text.</span></span> <span data-ttu-id="7f430-185">Erstellen Sie zum Ändern der Anzeige von Ereignis tritt auf, benutzerdefinierte Anzeigevorlagen, um die Ereignisinformationen zu rendern.</span><span class="sxs-lookup"><span data-stu-id="7f430-185">To change how event results are displayed, create custom display templates to render the event information.</span></span>

<span data-ttu-id="7f430-186">Sie können die elementanzeigevorlage ändern, sodass, wenn der Benutzer das Bild, Titel oder mehr lesen Link auswählt, die Informationsseite Ereignis geladen wird.</span><span class="sxs-lookup"><span data-stu-id="7f430-186">You can modify the item display template so that when the user chooses the image, title, or Read More link, the event information page is loaded.</span></span> <span data-ttu-id="7f430-187">Sie können auch die Steuerelement-Anzeigevorlage ändern, sodass die nächsten 10-Ereignisergebnisse im Webpart, wenn der Benutzer **Weitere**auswählt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="7f430-187">You can also modify the control display template so that when the user chooses  **See More**, the next 10 event results are displayed in the Web Part.</span></span>

<span data-ttu-id="7f430-188">Sie können auch ein Search-add-in erstellen, die die Abfrage-API verwendet, sogar Ergebnisse abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7f430-188">You can also create a search add-in that uses the query API to retrieve even results.</span></span> <span data-ttu-id="7f430-189">Sie können das Search-add-in, um anzuzeigen, werden standardmäßig nur 10 der neuesten anstehende Ereignisse, aber stellen Sie diese Einstellung über die Add-in-Sucheigenschaften konfigurierbar konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-189">You can configure the search add-in to show, by default, only 10 of the latest upcoming events, but make this setting configurable through the search add-in properties.</span></span> 

### <a name="featured-news-scenario"></a><span data-ttu-id="7f430-190">Empfohlene News-Szenario</span><span class="sxs-lookup"><span data-stu-id="7f430-190">Featured news scenario</span></span>

<span data-ttu-id="7f430-191">In diesem Szenario Suchergebnisse der Suche-add-Ins dargestellt als Ziel für die Benutzer an Stellen wie Unternehmensintranet und Abteilungen Angebotsseiten Empfohlener Inhalt.</span><span class="sxs-lookup"><span data-stu-id="7f430-191">In this scenario, the search add-in shows search results as featured content targeted to your users in places such as corporate intranet and divisional landing pages.</span></span> <span data-ttu-id="7f430-192">Sie können dies mit einem Webpart-Add-in implementieren, die eine jQuery-Plug-in mit HTML-Code enthält, die der Search REST-Dienst oder die CSOM-Abfrage zum Abrufen von Suchergebnissen aus SharePoint und Anzeigen der Ergebnisse verwendet.</span><span class="sxs-lookup"><span data-stu-id="7f430-192">You can implement this with an add-in part that contains a jQuery plugin with HTML, that uses the search REST service or the query CSOM to get search results from SharePoint and display the results.</span></span>

### <a name="code-sample-for-personalized-search"></a><span data-ttu-id="7f430-193">Codebeispiel für personalisierte Suche</span><span class="sxs-lookup"><span data-stu-id="7f430-193">Code sample for personalized search</span></span>

<span data-ttu-id="7f430-194">Die [SharePoint 2013: Personalisieren von Suchergebnisse in ein SharePoint-Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) Beispiel zeigt ein Beispiel für einfache Suche und eine personalisierte Suchergebnisse Beispiel, die die Suchabfrage CSOM verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7f430-194">The [SharePoint 2013: Personalizing search results in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) sample shows a basic search example and a personalized search results example that uses the search query CSOM.</span></span> <span data-ttu-id="7f430-195">Im Beispiel einfache Suche kann den Benutzer, die einen Suchfilter für einen Mandanten geltende Suche bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7f430-195">The basic search example lets the user provide a search filter to use for a tenant-wide search.</span></span> <span data-ttu-id="7f430-196">Websites werden basierend auf den benutzerdefinierten Filter durchsucht.</span><span class="sxs-lookup"><span data-stu-id="7f430-196">Sites are searched based on that user-supplied filter.</span></span>

<span data-ttu-id="7f430-197">Im Beispiel wird zunächst SharePoint Kontext mithilfe der **SharePointContextProvider** -Klasse.</span><span class="sxs-lookup"><span data-stu-id="7f430-197">The example first gets SharePoint context by using the  **SharePointContextProvider** class.</span></span>

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
```

<span data-ttu-id="7f430-198">Im nächsten Schritt wird die Abfrage basierend auf der Benutzereingabe erstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-198">Next, it builds the query based on what the user entered.</span></span> <span data-ttu-id="7f430-199">Es beschränkt die Abfrage für Websitesammlungen und ruft dann die **ProcessQuery** -Methode, die den Kontext und die Abfrage im Methodenaufruf übergeben.</span><span class="sxs-lookup"><span data-stu-id="7f430-199">It restricts the query to site collections, and then calls the  **ProcessQuery** method, passing the context and the query in the method call.</span></span> <span data-ttu-id="7f430-200">Anschließend wird, dass die Ergebnisse **ProcessQuery** dementsprechend Tabelle die dann von der **FormatResults** -Methode analysiert, zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7f430-200">It then returns the **ProcessQuery** results as a result table, which is then parsed by the **FormatResults** method.</span></span>

```
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    string query = searchtext.Text + " contentclass:\"STS_Site\"";
    ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
    lblStatus1.Text = FormatResults(results);
}
```

<span data-ttu-id="7f430-201">Die **ProcessQuery** -Methode erstellt ein **KeywordQuery** -Objekt, das die Suchabfrage darstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-201">The  **ProcessQuery** method builds a **KeywordQuery** object that represents the search query.</span></span>

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

<span data-ttu-id="7f430-202">Die Suchabfrage wird dann in SharePoint durch Aufrufen der Methode **ExecuteQuery_Client(Query)** versendet.</span><span class="sxs-lookup"><span data-stu-id="7f430-202">The search query is then submitted to SharePoint by calling the  **ExecuteQuery_Client(Query)** method.</span></span> <span data-ttu-id="7f430-203">Die Ergebnisse zurückgegeben werden, die **ClientResult < T&gt; ** Objekt.</span><span class="sxs-lookup"><span data-stu-id="7f430-203">Results are returned to the **ClientResult<T&gt;** object.</span></span>

```
SearchExecutor searchExec = new SearchExecutor(ctx);
ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
ctx.ExecuteQuery();
```

<span data-ttu-id="7f430-204">Die **FormatResults** -Methode durchlaufen und die Ergebnisse und erstellt eine HTML-Tabelle, um die Ergebniswerte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7f430-204">The  **FormatResults** method iterates through the results and constructs an HTML table to display the result values.</span></span>

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

<span data-ttu-id="7f430-205">"Apptesten" überprüft die **ResolveAdditionalFilter** -Methode.</span><span class="sxs-lookup"><span data-stu-id="7f430-205">The  **ResolveAdditionalFilter** method checks for "Apptest".</span></span> <span data-ttu-id="7f430-206">Wenn sie gefunden wird, wird eine Liste mit Websitevorlagen eines beliebigen Typs in den Suchergebnissen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7f430-206">If it is found, a list of site templates of any type is returned in the search results.</span></span> <span data-ttu-id="7f430-207">Wenn es nicht gefunden wird, werden nur STS Webvorlagen in den Suchergebnissen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7f430-207">If it is not found, only STS web templates are returned in the search results.</span></span>

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

<span data-ttu-id="7f430-208">Im Beispiel wird dann die Abfrage erstellt und ruft die **ProcessQuery** und **FormatResults** Methoden zum Abrufen, Format, und die Suchergebnisse angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7f430-208">The example then constructs the query and calls the  **ProcessQuery** and **FormatResults** methods to retrieve, format, and display the search results.</span></span>

```
string query = "contentclass:\"STS_Site\" " + templateFilter;
ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
lblStatus2.Text = FormatResults(results);
```

<span data-ttu-id="7f430-209">Sie können die Benutzeroberfläche für die in diesem Beispiel wird in der folgenden Abbildung sehen.</span><span class="sxs-lookup"><span data-stu-id="7f430-209">You can see the UI for this example in the following figure.</span></span>

<span data-ttu-id="7f430-210">**Abbildung 8. Personalisierte Suchergebnisse Beispiel-UI**</span><span class="sxs-lookup"><span data-stu-id="7f430-210">**Figure 8. Personalized search results sample UI**</span></span>

![Personalisierte Suchergebnisse Beispiel-UI](media/search-customizations-for-sharepoint/8e1c412b-71a7-42e2-b9f3-b7d045df3bde.png)

## <a name="search-configuration-portability"></a><span data-ttu-id="7f430-212">Suche Konfiguration Portabilität</span><span class="sxs-lookup"><span data-stu-id="7f430-212">Search configuration portability</span></span>

<span data-ttu-id="7f430-213">In SharePoint 2013 und SharePoint Online können Sie exportieren und importieren angepasster suchkonfigurationseinstellungen zwischen Websitesammlungen und Websites.</span><span class="sxs-lookup"><span data-stu-id="7f430-213">In SharePoint 2013 and SharePoint Online, you can export and import customized search configuration settings between site collections and sites.</span></span> <span data-ttu-id="7f430-214">Sie können nur exportieren angepasster suchkonfigurationseinstellungen auf der Ebene Search Service Application (SSA), und Sie müssen die Suche APIs programmgesteuert dazu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7f430-214">You can only export customized search configuration settings at the Search service application (SSA) level, and you have to use the search APIs to do this programmatically.</span></span> <span data-ttu-id="7f430-215">Die Export-Option ist nicht in der SharePoint-UI verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7f430-215">The export option is not available in the SharePoint UI.</span></span>

<span data-ttu-id="7f430-216">Die [SharePoint 2013: Import und Export der sucheinstellungen für SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) Beispiel gezeigt, wie Sie zum Importieren und Exportieren von sucheinstellungen für eine SharePoint Online-Website verwenden des Suchdiensts CSOM in eine Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="7f430-216">The [SharePoint 2013: Import and Export search settings for SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) sample show how to import and export search settings for a SharePoint Online site using the search CSOM in a console application.</span></span>

### <a name="configuration-settings-that-are-portable"></a><span data-ttu-id="7f430-217">Konfigurationseinstellungen, die portabel sind</span><span class="sxs-lookup"><span data-stu-id="7f430-217">Configuration settings that are portable</span></span>

<span data-ttu-id="7f430-218">Beim Exportieren angepasster suchkonfigurationseinstellungen erstellt SharePoint 2013 eine suchkonfigurationsdatei im XML-Format.</span><span class="sxs-lookup"><span data-stu-id="7f430-218">When you export customized search configuration settings, SharePoint 2013 creates a search configuration file in XML format.</span></span> <span data-ttu-id="7f430-219">Mit dieser Konfigurationsdatei Suche enthält alle exportierbar suchkonfigurationseinstellungen auf SSA, Websitesammlung oder der Websiteebene aus, in dem Sie den Export starten.</span><span class="sxs-lookup"><span data-stu-id="7f430-219">This search configuration file includes all exportable customized search configuration settings at the SSA, site collection, or site level from where you start the export.</span></span> <span data-ttu-id="7f430-220">Eine suchkonfigurationsdatei für eine Websitesammlung enthält keine suchkonfigurationseinstellungen aus den einzelnen Standorten innerhalb der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="7f430-220">A search configuration file for a site collection does not contain search configuration settings from the individual sites within the site collection.</span></span>

<span data-ttu-id="7f430-221">Beim Importieren einer suchkonfigurationsdatei SharePoint 2013 erstellt und aktiviert jede benutzerdefinierte suchkonfigurationseinstellung in der Websitesammlung oder Website aus, in dem Sie den Import starten.</span><span class="sxs-lookup"><span data-stu-id="7f430-221">When you import a search configuration file, SharePoint 2013 creates and enables each customized search configuration setting in the site collection or site from where you start the import.</span></span>

<span data-ttu-id="7f430-222">In Tabelle 1 werden die Einstellungen, die Sie exportieren und importieren können und Abhängigkeiten von anderen angepassten suchkonfigurationseinstellungen.</span><span class="sxs-lookup"><span data-stu-id="7f430-222">Table 1 lists the settings that you can export and import and any dependencies on other customized search configuration settings.</span></span> <span data-ttu-id="7f430-223">Wenn eine benutzerdefinierte suchkonfigurationseinstellung auf einer anderen Ebene die suchkonfigurationseinstellungen abhängen, müssen Sie exportieren und Importieren von Einstellungen in allen relevante Ebenen.</span><span class="sxs-lookup"><span data-stu-id="7f430-223">If the customized search configuration settings depend on a customized search configuration setting at a different level, you must export and import settings at all relevant levels.</span></span>

<span data-ttu-id="7f430-224">**In Tabelle 1. Für die Suche, die Sie exportieren und importieren können**</span><span class="sxs-lookup"><span data-stu-id="7f430-224">**Table 1. Search settings that you can export and import**</span></span>

|<span data-ttu-id="7f430-225">**Einstellung für die Konfiguration**</span><span class="sxs-lookup"><span data-stu-id="7f430-225">**Configuration setting**</span></span>|<span data-ttu-id="7f430-226">**Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="7f430-226">**Dependencies**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7f430-227">Abfrageregeln, einschließlich Ergebnis Blocs, heraufgestufte Ergebnisse und Benutzersegmente</span><span class="sxs-lookup"><span data-stu-id="7f430-227">Query rules, including result blocs, promoted results, and user segments</span></span>|<span data-ttu-id="7f430-228">Ergebnisquellen, Ergebnistypen, Suchschema, Bewertungsmodell</span><span class="sxs-lookup"><span data-stu-id="7f430-228">Result sources, result types, search schema, ranking model</span></span>|
|<span data-ttu-id="7f430-229">Ergebnisquellen</span><span class="sxs-lookup"><span data-stu-id="7f430-229">Result sources</span></span>|<span data-ttu-id="7f430-230">Suchschema</span><span class="sxs-lookup"><span data-stu-id="7f430-230">Search schema</span></span>|
|<span data-ttu-id="7f430-231">Ergebnistypen</span><span class="sxs-lookup"><span data-stu-id="7f430-231">Result types</span></span>|<span data-ttu-id="7f430-232">Suchschema, ergebnisquellen, Anzeigevorlagen</span><span class="sxs-lookup"><span data-stu-id="7f430-232">Search schema, result sources, display templates</span></span>|
|<span data-ttu-id="7f430-233">Suchschema</span><span class="sxs-lookup"><span data-stu-id="7f430-233">Search schema</span></span>|<span data-ttu-id="7f430-234">Keine</span><span class="sxs-lookup"><span data-stu-id="7f430-234">None</span></span>|
|<span data-ttu-id="7f430-235">Bewertungsmodell</span><span class="sxs-lookup"><span data-stu-id="7f430-235">Ranking model</span></span>|<span data-ttu-id="7f430-236">Suchschema</span><span class="sxs-lookup"><span data-stu-id="7f430-236">Search schema</span></span>|

<span data-ttu-id="7f430-237">Sie können suchkonfigurationseinstellungen aus einer SSA exportieren und importieren die Einstellungen von Websitesammlungen und Websites.</span><span class="sxs-lookup"><span data-stu-id="7f430-237">You can export customized search configuration settings from an SSA and import the settings to site collections and sites.</span></span> <span data-ttu-id="7f430-238">Aber kann nicht importieren angepasster suchkonfigurationseinstellungen in eine SSA.</span><span class="sxs-lookup"><span data-stu-id="7f430-238">But you can't import customized search configuration settings to an SSA.</span></span> <span data-ttu-id="7f430-239">Auch können nicht die standardmäßige suchkonfigurationseinstellungen exportiert werden.</span><span class="sxs-lookup"><span data-stu-id="7f430-239">You also can't export the default search configuration settings.</span></span>

<span data-ttu-id="7f430-240">Auf Ebene der Websitesammlung oder Website können Sie exportieren oder importieren suchkonfigurationseinstellungen mithilfe der SharePoint-UI.</span><span class="sxs-lookup"><span data-stu-id="7f430-240">At the site or site collection level, you can export or import search configuration settings by using the SharePoint UI.</span></span> <span data-ttu-id="7f430-241">Diese Einstellungen befinden sich im Abschnitt **Suchen** der Seite **Websiteeinstellungen** .</span><span class="sxs-lookup"><span data-stu-id="7f430-241">These settings are located in the  **Search** section of the **Site Settings** page.</span></span>

<span data-ttu-id="7f430-242">**Websiteeinstellungen - Suche**</span><span class="sxs-lookup"><span data-stu-id="7f430-242">**Site Settings - Search**</span></span>

![Websiteeinstellungen - Suche](media/search-customizations-for-sharepoint/ada14bf4-d721-4974-ad50-a1f8ce01933f.png)

<span data-ttu-id="7f430-244">Diese Einstellungen sind auch im Abschnitt **Verwaltung der Websitesammlung** verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7f430-244">These settings are also available in the  **Site Collection Administration** section.</span></span> <span data-ttu-id="7f430-245">Alternativ können Sie programmgesteuert importieren und Exportieren diese Einstellungen mithilfe der SharePoint 2013-Suche CSOM.</span><span class="sxs-lookup"><span data-stu-id="7f430-245">Alternatively, you can programmatically import and export these settings by using the SharePoint 2013 search CSOM.</span></span>

### <a name="search-configuration-files"></a><span data-ttu-id="7f430-246">Konfigurationsdateien für die Suche</span><span class="sxs-lookup"><span data-stu-id="7f430-246">Search configuration files</span></span>

<span data-ttu-id="7f430-247">Die folgende Tabelle enthält die Schemadateien, die eine Suchkonfiguration unterstützen.</span><span class="sxs-lookup"><span data-stu-id="7f430-247">The following table lists schema files that support a search configuration.</span></span> <span data-ttu-id="7f430-248">Informationen zum Schemaformat finden Sie unter [Share Point Search Settings Portability Schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f430-248">For information about the schema format, see [Share Point search settings portability schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span></span>

<span data-ttu-id="7f430-249">**Hinweis:**  Sie können die Schemadateien [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip)heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="7f430-249">**Note:**  You can download the schema files from [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip).</span></span> 

<span data-ttu-id="7f430-250">**In Tabelle 2. Search Settings Portability schemas**</span><span class="sxs-lookup"><span data-stu-id="7f430-250">**Table 2. Search settings portability schemas**</span></span>

|<span data-ttu-id="7f430-251">**Schema**</span><span class="sxs-lookup"><span data-stu-id="7f430-251">**Schema**</span></span>|<span data-ttu-id="7f430-252">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="7f430-252">**Description**</span></span>|
|:-----|:-----|
|[<span data-ttu-id="7f430-253">SPS15XSDSearchSet1</span><span class="sxs-lookup"><span data-stu-id="7f430-253">SPS15XSDSearchSet1</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639116%28v=office.15%29.aspx)|<span data-ttu-id="7f430-254">Gibt an, XML, das ergebnisquellen darstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-254">Specifies XML that represents result sources.</span></span>|
|[<span data-ttu-id="7f430-255">SPS15XSDSearchSet2</span><span class="sxs-lookup"><span data-stu-id="7f430-255">SPS15XSDSearchSet2</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639118%28v=office.15%29.aspx)|<span data-ttu-id="7f430-256">Gibt an, XML, das administrative Typen und Member zum Verwalten von einer Instanz der SSA Suche darstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-256">Specifies XML that represents administrative types and members for managing an SSA search instance.</span></span> <span data-ttu-id="7f430-257">Dazu gehören ergebniselementtypen und Einstellungen der Regel.</span><span class="sxs-lookup"><span data-stu-id="7f430-257">This includes result item types and property rule settings.</span></span>|
|[<span data-ttu-id="7f430-258">SPS15XSDSearchSet3</span><span class="sxs-lookup"><span data-stu-id="7f430-258">SPS15XSDSearchSet3</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639120%28v=office.15%29.aspx)|<span data-ttu-id="7f430-259">Gibt an, die Einstellungen darstellt, die Abfrageregeln, enthalten XML ergebnisquellen, verwalteten Eigenschaften, durchforstete Eigenschaften und rangmodelle.</span><span class="sxs-lookup"><span data-stu-id="7f430-259">Specifies XML that represents settings that include query rules, result sources, managed properties, crawled properties, and ranking models.</span></span>|
|[<span data-ttu-id="7f430-260">SPS15XSDSearchSet4</span><span class="sxs-lookup"><span data-stu-id="7f430-260">SPS15XSDSearchSet4</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639117%28v=office.15%29.aspx)|<span data-ttu-id="7f430-261">Gibt an, XML, Enumerationen, die in anderen Schemas verwendet darstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-261">Specifies XML that represents enumerations used in other schemas.</span></span>|
|[<span data-ttu-id="7f430-262">SPS15XSDSearchSet5</span><span class="sxs-lookup"><span data-stu-id="7f430-262">SPS15XSDSearchSet5</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639119%28v=office.15%29.aspx)|<span data-ttu-id="7f430-263">Gibt an, XML, Enumerationen wie **ResultType-Wert** darstellt, die in anderen Schemas verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7f430-263">Specifies XML that represents enumerations like  **ResultType** that are used in other schemas.</span></span>|
|[<span data-ttu-id="7f430-264">SPS15XSDSearchSet6</span><span class="sxs-lookup"><span data-stu-id="7f430-264">SPS15XSDSearchSet6</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639115%28v=office.15%29.aspx)|<span data-ttu-id="7f430-265">Gibt an, XML, Enumerationen im Schema **Microsoft.Office.Server.Search.Administration** verwendet darstellt.</span><span class="sxs-lookup"><span data-stu-id="7f430-265">Specifies XML that represents enumerations used in the  **Microsoft.Office.Server.Search.Administration** schema.</span></span>|

### <a name="using-csom-to-port-configuration-settings"></a><span data-ttu-id="7f430-266">Verwenden CSOM zum Port-Konfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="7f430-266">Using CSOM to port configuration settings</span></span>

<span data-ttu-id="7f430-267">Die CSOM-APIs, die Sie benötigen, um das Importieren und Exportieren von Ihrer suchkonfigurationseinstellungen sind in der **SearchConfigurationPortability** -Klasse im **Microsoft.SharePoint.Client.Search.Portability** -Namespace.</span><span class="sxs-lookup"><span data-stu-id="7f430-267">The CSOM APIs that you need in order to import and export your search configuration settings are in the  **SearchConfigurationPortability** class in the **Microsoft.SharePoint.Client.Search.Portability** namespace.</span></span>

<span data-ttu-id="7f430-268">Im folgenden Codebeispiel wird veranschaulicht, wie suchkonfigurationseinstellungen für eine Website exportieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-268">The following code example shows how to export a site's search configuration settings.</span></span>

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

<span data-ttu-id="7f430-269">Der folgende Code zeigt, wie Sie eine Website suchkonfigurationseinstellungen importieren.</span><span class="sxs-lookup"><span data-stu-id="7f430-269">The following code shows how to import a site's search configuration settings.</span></span>

```
private static void ImportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   sconfig.ImportSearchConfiguration(owner, System.IO.File.ReadAllText(settingsFile));
   context.ExecuteQuery();            
}
```

## <a name="additional-resources"></a><span data-ttu-id="7f430-270">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7f430-270">Additional resources</span></span>
<span data-ttu-id="7f430-271"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7f430-271"></span></span>

- [<span data-ttu-id="7f430-272">Suchlösungen in SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7f430-272">Search solutions in SharePoint 2013 and SharePoint Online</span></span>](search-solutions-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="7f430-273">SharePoint 2013: Import und Export der sucheinstellungen für SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7f430-273">SharePoint 2013: Import and Export search settings for SharePoint Online</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac)
    
- [<span data-ttu-id="7f430-274">SharePoint 2013: Führt zu personalisieren der Suche in einer SharePoint-Add-in</span><span class="sxs-lookup"><span data-stu-id="7f430-274">SharePoint 2013: Personalizing search results in a SharePoint Add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9)
