---
title: "Aktualisieren von Vorlagen für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 69048e4c-6d6d-4e4e-b74c-7c72ae444354
ms.openlocfilehash: cb8e3849b9853d593ce8504814e92066bf08a540
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="upgrade-web-templates-for-sharepoint"></a><span data-ttu-id="930bb-102">Aktualisieren von Vorlagen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="930bb-102">Upgrade web templates for SharePoint</span></span>
<span data-ttu-id="930bb-p101">Informationen Sie zur Aktualisierung der angepassten SharePoint 2010 Webvorlagen für die Verwendung in SharePoint nach einem Upgrade Self-service. SharePoint hat sich die zugrunde liegenden Komponenten zum Rendern der Darstellung von SharePoint-Websites verwendeten erheblich geändert. Für Standard-Komponenten in SharePoint 2010 vorgenommenen Anpassungen schließen Sie diese neuen Änderungen Formatvorlagen, Seitenlayouts, Masterseiten und Designs.</span><span class="sxs-lookup"><span data-stu-id="930bb-p101">Learn about updating customized SharePoint 2010 web templates for use in SharePoint after a self-service upgrade. SharePoint has significantly changed the underlying components it uses to render the appearance of SharePoint sites. For customizations made to default components in SharePoint 2010, these new changes include styles, page layouts, master pages and themes.</span></span>
  
    
    

<span data-ttu-id="930bb-106">Dieser Artikel enthält Hinweise zur Aktualisierung Ihrer Webvorlagen, damit sie mit dem neuen Framework funktionieren.</span><span class="sxs-lookup"><span data-stu-id="930bb-106">This article provides guidance for updating your web templates so that they work with the new framework.</span></span>
## <a name="possible-behavior-after-a-self-service-site-upgrade"></a><span data-ttu-id="930bb-107">Mögliche Verhalten nach einem Self-service Site-upgrade</span><span class="sxs-lookup"><span data-stu-id="930bb-107">Possible behavior after a self-service site upgrade</span></span>

<span data-ttu-id="930bb-p102">Beim upgrade von eines Servers von SharePoint 2010 auf 2013 werden Websitesammlungsadministratoren einen Link angezeigt, mit der sie ihre Websites schrittweises upgrade aus, oder aktualisieren Sie alle Websites in der Websitesammlung auf einmal. Benutzer können dann aktualisieren und testen diese Websites, die Anpassungen enthalten. Einige der Probleme, die Benutzer nach einem Upgrade einschließen auftreten können:</span><span class="sxs-lookup"><span data-stu-id="930bb-p102">When you upgrade a server from SharePoint 2010 to 2013, site collection administrators are shown a link that lets them upgrade their sites gradually, or upgrade all sites in the site collection at once. Then users can upgrade and test those sites that contain customizations. Some of the problems that users might encounter after an upgrade include:</span></span>
  
    
    

- <span data-ttu-id="930bb-111">Branding auf Websites angewendet, geändert wurde oder vollständig fehlt.</span><span class="sxs-lookup"><span data-stu-id="930bb-111">Branding applied to sites has been changed, or is missing altogether.</span></span>
    
  
- <span data-ttu-id="930bb-112">Benutzerdefinierte Komponenten nicht ordnungsgemäß gerendert.</span><span class="sxs-lookup"><span data-stu-id="930bb-112">Custom components don't render correctly.</span></span>
    
  
- <span data-ttu-id="930bb-113">Nicht in allen Seiten rendern und die Benutzer erhalten eine unbekannte Fehler aus SharePoint.</span><span class="sxs-lookup"><span data-stu-id="930bb-113">Pages don't render at all, and the users receive unknown errors from SharePoint.</span></span>
    
  
- <span data-ttu-id="930bb-114">Features, die standardmäßig aktiviert sind, werden nach dem Upgrade deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="930bb-114">Features that are enabled by default are disabled after upgrade.</span></span>
    
  

## <a name="recommendations-for-upgrading-sites"></a><span data-ttu-id="930bb-115">Empfehlungen für das Aktualisieren von Websites</span><span class="sxs-lookup"><span data-stu-id="930bb-115">Recommendations for upgrading sites</span></span>

<span data-ttu-id="930bb-116">Wenn Sie Websites aktualisieren, sollten im Allgemeinen für die Verwendung der Evaluierungswebsite installieren und Testen Ihre Komponenten für Kompatibilitäts- und Leistungsprobleme.</span><span class="sxs-lookup"><span data-stu-id="930bb-116">When you upgrade sites, we generally recommend that you use the evaluation site to install and test your components for compatibility and performance.</span></span>
  
    
    
<span data-ttu-id="930bb-117">Den folgenden Abschnitten wird erläutert, was Sie in der Webvorlage aktualisieren müssen.</span><span class="sxs-lookup"><span data-stu-id="930bb-117">The following sections detail what you need to update in the web template.</span></span>
  
    
    

### <a name="update-master-page-references"></a><span data-ttu-id="930bb-118">Aktualisieren der Verweise Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="930bb-118">Update master page references</span></span>

<span data-ttu-id="930bb-p103">Nach der Aktualisierung auf SharePoint werden benutzerdefinierte Gestaltungsvorlage, die Ihre Webvorlage enthält Verweise auf die Standardgestaltungsvorlage mit dem Namen **seattle.master** festgelegt werden. Wenn Sie die Standardgestaltungsvorlage SharePoint 2010 angepasst haben, müssen Sie den Verweis auf die benutzerdefinierte Seite in der Reihenfolge für Ihre Anpassungen angezeigt werden zu ändern.</span><span class="sxs-lookup"><span data-stu-id="930bb-p103">After an upgrade to SharePoint, any custom master page references that your web template contains will be set to the default master page named **seattle.master**. If you customized the default master page in SharePoint 2010, you will need to change the reference to that custom page in order for your customizations to appear.</span></span>
  
    
    

### <a name="update-available-features"></a><span data-ttu-id="930bb-121">Aktualisieren Sie die verfügbaren features</span><span class="sxs-lookup"><span data-stu-id="930bb-121">Update available features</span></span>

<span data-ttu-id="930bb-p104">Bei einer Aktualisierung ein Standort mit SharePoint Webvorlagen werden Funktionen, die die Vorlage, werden standardmäßig zugeordnet sind, entfernt. Daher wird die verfügbare Funktionalität einer aktualisierten Webvorlage reduziert.</span><span class="sxs-lookup"><span data-stu-id="930bb-p104">When you upgrade a site to use SharePoint web templates, features that are attached to the template by default are removed. As a consequence, the available functionality of an upgraded web template is reduced.</span></span>
  
    
    
<span data-ttu-id="930bb-p105">Um die Standardfunktionalität wieder die Vorlage hinzuzufügen, müssen Sie die Datei Onet.xml für die Webvorlage ändern, die der Liste der Features enthält. Um die Standardfeatures wieder Ihrer Webvorlage hinzuzufügen, führen Sie folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="930bb-p105">To add the default functionality back to the template, you must modify the Onet.xml file for the web template that contains the feature list. To add the default features back to your web template, do the following:</span></span>
  
    
    

### <a name="to-add-default-features-back-to-the-web-template"></a><span data-ttu-id="930bb-126">Sichern zum Hinzufügen von standardmäßigen Features in der Webvorlage</span><span class="sxs-lookup"><span data-stu-id="930bb-126">To add default features back to the web template</span></span>


1. <span data-ttu-id="930bb-127">Öffnen Sie das Visual Studio-Projekt, das die Webvorlage enthält, den, die Sie aktualisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="930bb-127">Open the Visual Studio project that contains the web template you want to update.</span></span>
    
  
2. <span data-ttu-id="930bb-128">Suchen Sie im **Projektmappen-Explorer** die Datei "onet.xml" in Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="930bb-128">In **Solution Explorer**, find the Onet.xml file in your project.</span></span>
    
  
3. <span data-ttu-id="930bb-129">Onet.xml in einem XML-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="930bb-129">Open Onet.xml in an XML editor.</span></span>
    
  
4. <span data-ttu-id="930bb-130">Stellen Sie sicher, dass der Features in Tabelle 1 sind im Abschnitt **WebFeatures** enthalten.</span><span class="sxs-lookup"><span data-stu-id="930bb-130">Make sure that each of the features in Table 1 are contained in the **WebFeatures** section.</span></span>
    
   <span data-ttu-id="930bb-131">**In Tabelle 1. Standardfeatures für Web-Vorlage**</span><span class="sxs-lookup"><span data-stu-id="930bb-131">**Table 1. Default web template features**</span></span>


|<span data-ttu-id="930bb-132">**Anzeigename**</span><span class="sxs-lookup"><span data-stu-id="930bb-132">**DisplayName**</span></span>|<span data-ttu-id="930bb-133">**Feature-ID**</span><span class="sxs-lookup"><span data-stu-id="930bb-133">**Feature ID**</span></span>|
|:-----|:-----|
|<span data-ttu-id="930bb-134">AccSvcAddAccessApp</span><span class="sxs-lookup"><span data-stu-id="930bb-134">AccSvcAddAccessApp</span></span>  <br/> |<span data-ttu-id="930bb-135">d2b9ec23-526b-42c5-87b6-852bd83e0364</span><span class="sxs-lookup"><span data-stu-id="930bb-135">d2b9ec23-526b-42c5-87b6-852bd83e0364</span></span>  <br/> |
|<span data-ttu-id="930bb-136">AnnouncementsList</span><span class="sxs-lookup"><span data-stu-id="930bb-136">AnnouncementsList</span></span>  <br/> |<span data-ttu-id="930bb-137">00BFEA71-D1CE-42de-9C63-A44004CE0104</span><span class="sxs-lookup"><span data-stu-id="930bb-137">00bfea71-d1ce-42de-9c63-a44004ce0104</span></span>  <br/> |
|<span data-ttu-id="930bb-138">BaseWeb</span><span class="sxs-lookup"><span data-stu-id="930bb-138">BaseWeb</span></span>  <br/> |<span data-ttu-id="930bb-139">99fe402e-89a0-45aa-9163-85342e865dc8</span><span class="sxs-lookup"><span data-stu-id="930bb-139">99fe402e-89a0-45aa-9163-85342e865dc8</span></span>  <br/> |
|<span data-ttu-id="930bb-140">BizAppsListTemplates</span><span class="sxs-lookup"><span data-stu-id="930bb-140">BizAppsListTemplates</span></span>  <br/> |<span data-ttu-id="930bb-141">065c78be-5231-477e-a972-14177cc5b3c7</span><span class="sxs-lookup"><span data-stu-id="930bb-141">065c78be-5231-477e-a972-14177cc5b3c7</span></span>  <br/> |
|<span data-ttu-id="930bb-142">ContactsList</span><span class="sxs-lookup"><span data-stu-id="930bb-142">ContactsList</span></span>  <br/> |<span data-ttu-id="930bb-143">00BFEA71-7E6D-4186-9BA8-C047AC750105</span><span class="sxs-lookup"><span data-stu-id="930bb-143">00bfea71-7e6d-4186-9ba8-c047ac750105</span></span>  <br/> |
|<span data-ttu-id="930bb-144">ContactsList</span><span class="sxs-lookup"><span data-stu-id="930bb-144">ContactsList</span></span>  <br/> |<span data-ttu-id="930bb-145">00BFEA71-7E6D-4186-9BA8-C047AC750105</span><span class="sxs-lookup"><span data-stu-id="930bb-145">00bfea71-7e6d-4186-9ba8-c047ac750105</span></span>  <br/> |
|<span data-ttu-id="930bb-146">CustomList</span><span class="sxs-lookup"><span data-stu-id="930bb-146">CustomList</span></span>  <br/> |<span data-ttu-id="930bb-147">00BFEA71-DE22-43B2-A848-C05709900100</span><span class="sxs-lookup"><span data-stu-id="930bb-147">00bfea71-de22-43b2-a848-c05709900100</span></span>  <br/> |
|<span data-ttu-id="930bb-148">DataConnectionLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-148">DataConnectionLibrary</span></span>  <br/> |<span data-ttu-id="930bb-149">00bfea71-dbd7-4f72-b8cb-da7ac0440130</span><span class="sxs-lookup"><span data-stu-id="930bb-149">00bfea71-dbd7-4f72-b8cb-da7ac0440130</span></span>  <br/> |
|<span data-ttu-id="930bb-150">DataSourceLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-150">DataSourceLibrary</span></span>  <br/> |<span data-ttu-id="930bb-151">00BFEA71-F381-423D-B9D1-DA7A54C50110</span><span class="sxs-lookup"><span data-stu-id="930bb-151">00bfea71-f381-423d-b9d1-da7a54c50110</span></span>  <br/> |
|<span data-ttu-id="930bb-152">DiscussionsList</span><span class="sxs-lookup"><span data-stu-id="930bb-152">DiscussionsList</span></span>  <br/> |<span data-ttu-id="930bb-153">00BFEA71-6A49-43FA-B535-D15C05500108</span><span class="sxs-lookup"><span data-stu-id="930bb-153">00bfea71-6a49-43fa-b535-d15c05500108</span></span>  <br/> |
|<span data-ttu-id="930bb-154">DocumentLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-154">DocumentLibrary</span></span>  <br/> |<span data-ttu-id="930bb-155">00BFEA71-E717-4E80-AA17-D0C71B360101</span><span class="sxs-lookup"><span data-stu-id="930bb-155">00bfea71-e717-4e80-aa17-d0c71b360101</span></span>  <br/> |
|<span data-ttu-id="930bb-156">EventsList</span><span class="sxs-lookup"><span data-stu-id="930bb-156">EventsList</span></span>  <br/> |<span data-ttu-id="930bb-157">00BFEA71-EC85-4903-972D-EBE475780106</span><span class="sxs-lookup"><span data-stu-id="930bb-157">00bfea71-ec85-4903-972d-ebe475780106</span></span>  <br/> |
|<span data-ttu-id="930bb-158">EventsList</span><span class="sxs-lookup"><span data-stu-id="930bb-158">EventsList</span></span>  <br/> |<span data-ttu-id="930bb-159">00BFEA71-EC85-4903-972D-EBE475780106</span><span class="sxs-lookup"><span data-stu-id="930bb-159">00bfea71-ec85-4903-972d-ebe475780106</span></span>  <br/> |
|<span data-ttu-id="930bb-160">ExternalList</span><span class="sxs-lookup"><span data-stu-id="930bb-160">ExternalList</span></span>  <br/> |<span data-ttu-id="930bb-161">00bfea71-9549-43f8-b978-e47e54a10600</span><span class="sxs-lookup"><span data-stu-id="930bb-161">00bfea71-9549-43f8-b978-e47e54a10600</span></span>  <br/> |
|<span data-ttu-id="930bb-162">FollowingContent</span><span class="sxs-lookup"><span data-stu-id="930bb-162">FollowingContent</span></span>  <br/> |<span data-ttu-id="930bb-163">a7a2793e-67cd-4dc1-9fd0-43f61581207a</span><span class="sxs-lookup"><span data-stu-id="930bb-163">a7a2793e-67cd-4dc1-9fd0-43f61581207a</span></span>  <br/> |
|<span data-ttu-id="930bb-164">GanttTasksList</span><span class="sxs-lookup"><span data-stu-id="930bb-164">GanttTasksList</span></span>  <br/> |<span data-ttu-id="930bb-165">00BFEA71-513D-4CA0-96C2-6A47775C0119</span><span class="sxs-lookup"><span data-stu-id="930bb-165">00bfea71-513d-4ca0-96c2-6a47775c0119</span></span>  <br/> |
|<span data-ttu-id="930bb-166">GettingStarted</span><span class="sxs-lookup"><span data-stu-id="930bb-166">GettingStarted</span></span>  <br/> |<span data-ttu-id="930bb-167">4aec7207-0d02-4f4f-aa07-b370199cd0c7</span><span class="sxs-lookup"><span data-stu-id="930bb-167">4aec7207-0d02-4f4f-aa07-b370199cd0c7</span></span>  <br/> |
|<span data-ttu-id="930bb-168">GridList</span><span class="sxs-lookup"><span data-stu-id="930bb-168">GridList</span></span>  <br/> |<span data-ttu-id="930bb-169">00BFEA71-3A1D-41D3-A0EE-651D11570120</span><span class="sxs-lookup"><span data-stu-id="930bb-169">00bfea71-3a1d-41d3-a0ee-651d11570120</span></span>  <br/> |
|<span data-ttu-id="930bb-170">HierarchyTasksList</span><span class="sxs-lookup"><span data-stu-id="930bb-170">HierarchyTasksList</span></span>  <br/> |<span data-ttu-id="930bb-171">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span><span class="sxs-lookup"><span data-stu-id="930bb-171">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span></span>  <br/> |
|<span data-ttu-id="930bb-172">IPFSWebFeatures</span><span class="sxs-lookup"><span data-stu-id="930bb-172">IPFSWebFeatures</span></span>  <br/> |<span data-ttu-id="930bb-173">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span><span class="sxs-lookup"><span data-stu-id="930bb-173">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span></span>  <br/> |
|<span data-ttu-id="930bb-174">IssuesList</span><span class="sxs-lookup"><span data-stu-id="930bb-174">IssuesList</span></span>  <br/> |<span data-ttu-id="930bb-175">00BFEA71-5932-4F9C-AD71-1557E5751100</span><span class="sxs-lookup"><span data-stu-id="930bb-175">00bfea71-5932-4f9c-ad71-1557e5751100</span></span>  <br/> |
|<span data-ttu-id="930bb-176">LinksList</span><span class="sxs-lookup"><span data-stu-id="930bb-176">LinksList</span></span>  <br/> |<span data-ttu-id="930bb-177">00BFEA71-5932-4F9C-AD71-1557E5751100</span><span class="sxs-lookup"><span data-stu-id="930bb-177">00bfea71-5932-4f9c-ad71-1557e5751100</span></span>  <br/> |
|<span data-ttu-id="930bb-178">MBrowserRedirect</span><span class="sxs-lookup"><span data-stu-id="930bb-178">MBrowserRedirect</span></span>  <br/> |<span data-ttu-id="930bb-179">d95c97f3-e528-4da2-ae9f-32b3535fbb59</span><span class="sxs-lookup"><span data-stu-id="930bb-179">d95c97f3-e528-4da2-ae9f-32b3535fbb59</span></span>  <br/> |
|<span data-ttu-id="930bb-180">MDSFeature</span><span class="sxs-lookup"><span data-stu-id="930bb-180">MDSFeature</span></span>  <br/> |<span data-ttu-id="930bb-181">87294c72-f260-42f3-a41b-981a2ffce37a</span><span class="sxs-lookup"><span data-stu-id="930bb-181">87294c72-f260-42f3-a41b-981a2ffce37a</span></span>  <br/> |
|<span data-ttu-id="930bb-182">MobilityRedirect</span><span class="sxs-lookup"><span data-stu-id="930bb-182">MobilityRedirect</span></span>  <br/> |<span data-ttu-id="930bb-183">f41cc668-37e5-4743-b4a8-74d1db3fd8a4</span><span class="sxs-lookup"><span data-stu-id="930bb-183">f41cc668-37e5-4743-b4a8-74d1db3fd8a4</span></span>  <br/> |
|<span data-ttu-id="930bb-184">MySiteMicroBlog</span><span class="sxs-lookup"><span data-stu-id="930bb-184">MySiteMicroBlog</span></span>  <br/> |<span data-ttu-id="930bb-185">ea23650b-0340-4708-b465-441a41c37af7</span><span class="sxs-lookup"><span data-stu-id="930bb-185">ea23650b-0340-4708-b465-441a41c37af7</span></span>  <br/> |
|<span data-ttu-id="930bb-186">NoCodeWorkflowLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-186">NoCodeWorkflowLibrary</span></span>  <br/> |<span data-ttu-id="930bb-187">00BFEA71-F600-43F6-A895-40C0DE7B0117</span><span class="sxs-lookup"><span data-stu-id="930bb-187">00bfea71-f600-43f6-a895-40c0de7b0117</span></span>  <br/> |
|<span data-ttu-id="930bb-188">PictureLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-188">PictureLibrary</span></span>  <br/> |<span data-ttu-id="930bb-189">00BFEA71-52D4-45B3-B544-B1C71B620109</span><span class="sxs-lookup"><span data-stu-id="930bb-189">00bfea71-52d4-45b3-b544-b1c71b620109</span></span>  <br/> |
|<span data-ttu-id="930bb-190">PremiumWeb</span><span class="sxs-lookup"><span data-stu-id="930bb-190">PremiumWeb</span></span>  <br/> |<span data-ttu-id="930bb-191">0806d127-06e6-447a-980e-2e90b03101b8</span><span class="sxs-lookup"><span data-stu-id="930bb-191">0806d127-06e6-447a-980e-2e90b03101b8</span></span>  <br/> |
|<span data-ttu-id="930bb-192">PromotedLinksList</span><span class="sxs-lookup"><span data-stu-id="930bb-192">PromotedLinksList</span></span>  <br/> |<span data-ttu-id="930bb-193">192efa95-e50c-475e-87ab-361cede5dd7f</span><span class="sxs-lookup"><span data-stu-id="930bb-193">192efa95-e50c-475e-87ab-361cede5dd7f</span></span>  <br/> |
|<span data-ttu-id="930bb-194">ReportListTemplate</span><span class="sxs-lookup"><span data-stu-id="930bb-194">ReportListTemplate</span></span>  <br/> |<span data-ttu-id="930bb-195">2510d73f-7109-4ccc-8a1c-314894deeb3a</span><span class="sxs-lookup"><span data-stu-id="930bb-195">2510d73f-7109-4ccc-8a1c-314894deeb3a</span></span>  <br/> |
|<span data-ttu-id="930bb-196">SiteFeed</span><span class="sxs-lookup"><span data-stu-id="930bb-196">SiteFeed</span></span>  <br/> |<span data-ttu-id="930bb-197">15a572c6-e545-4d32-897a-bab6f5846e18</span><span class="sxs-lookup"><span data-stu-id="930bb-197">15a572c6-e545-4d32-897a-bab6f5846e18</span></span>  <br/> |
|<span data-ttu-id="930bb-198">SiteFeedController</span><span class="sxs-lookup"><span data-stu-id="930bb-198">SiteFeedController</span></span>  <br/> |<span data-ttu-id="930bb-199">5153156a-63af-4fac-b557-91bd8c315432</span><span class="sxs-lookup"><span data-stu-id="930bb-199">5153156a-63af-4fac-b557-91bd8c315432</span></span>  <br/> |
|<span data-ttu-id="930bb-200">SurveysList</span><span class="sxs-lookup"><span data-stu-id="930bb-200">SurveysList</span></span>  <br/> |<span data-ttu-id="930bb-201">00BFEA71-EB8A-40B1-80C7-506BE7590102</span><span class="sxs-lookup"><span data-stu-id="930bb-201">00bfea71-eb8a-40b1-80c7-506be7590102</span></span>  <br/> |
|<span data-ttu-id="930bb-202">TaskListNewsFeed</span><span class="sxs-lookup"><span data-stu-id="930bb-202">TaskListNewsFeed</span></span>  <br/> |<span data-ttu-id="930bb-203">ff13819a-a9ac-46fb-8163-9d53357ef98d</span><span class="sxs-lookup"><span data-stu-id="930bb-203">ff13819a-a9ac-46fb-8163-9d53357ef98d</span></span>  <br/> |
|<span data-ttu-id="930bb-204">TasksList</span><span class="sxs-lookup"><span data-stu-id="930bb-204">TasksList</span></span>  <br/> |<span data-ttu-id="930bb-205">00BFEA71-A83E-497E-9BA0-7A5C597D0107</span><span class="sxs-lookup"><span data-stu-id="930bb-205">00bfea71-a83e-497e-9ba0-7a5c597d0107</span></span>  <br/> |
|<span data-ttu-id="930bb-206">TeamCollab</span><span class="sxs-lookup"><span data-stu-id="930bb-206">TeamCollab</span></span>  <br/> |<span data-ttu-id="930bb-207">00bfea71-4ea5-48d4-a4ad-7ea5c011abe5</span><span class="sxs-lookup"><span data-stu-id="930bb-207">00bfea71-4ea5-48d4-a4ad-7ea5c011abe5</span></span>  <br/> |
|<span data-ttu-id="930bb-208">WebPageLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-208">WebPageLibrary</span></span>  <br/> |<span data-ttu-id="930bb-209">00BFEA71-C796-4402-9F2F-0EB9A6E71B18</span><span class="sxs-lookup"><span data-stu-id="930bb-209">00bfea71-c796-4402-9f2f-0eb9a6e71b18</span></span>  <br/> |
|<span data-ttu-id="930bb-210">WikiPageHomePage</span><span class="sxs-lookup"><span data-stu-id="930bb-210">WikiPageHomePage</span></span>  <br/> |<span data-ttu-id="930bb-211">00bfea71-d8fe-4fec-8dad-01c19a6e4053</span><span class="sxs-lookup"><span data-stu-id="930bb-211">00bfea71-d8fe-4fec-8dad-01c19a6e4053</span></span>  <br/> |
|<span data-ttu-id="930bb-212">WorkflowHistoryList</span><span class="sxs-lookup"><span data-stu-id="930bb-212">WorkflowHistoryList</span></span>  <br/> |<span data-ttu-id="930bb-213">00BFEA71-4EA5-48D4-A4AD-305CF7030140</span><span class="sxs-lookup"><span data-stu-id="930bb-213">00bfea71-4ea5-48d4-a4ad-305cf7030140</span></span>  <br/> |
|<span data-ttu-id="930bb-214">workflowProcessList</span><span class="sxs-lookup"><span data-stu-id="930bb-214">workflowProcessList</span></span>  <br/> |<span data-ttu-id="930bb-215">00BFEA71-2D77-4A75-9FCA-76516689E21A</span><span class="sxs-lookup"><span data-stu-id="930bb-215">00bfea71-2d77-4a75-9fca-76516689e21a</span></span>  <br/> |
|<span data-ttu-id="930bb-216">WorkflowServiceStore</span><span class="sxs-lookup"><span data-stu-id="930bb-216">WorkflowServiceStore</span></span>  <br/> |<span data-ttu-id="930bb-217">2c63df2b-ceab-42c6-aeff-b3968162d4b1</span><span class="sxs-lookup"><span data-stu-id="930bb-217">2c63df2b-ceab-42c6-aeff-b3968162d4b1</span></span>  <br/> |
|<span data-ttu-id="930bb-218">WorkflowTask</span><span class="sxs-lookup"><span data-stu-id="930bb-218">WorkflowTask Object</span></span>  <br/> |<span data-ttu-id="930bb-219">57311b7a-9afd-4ff0-866e-9393ad6647b1</span><span class="sxs-lookup"><span data-stu-id="930bb-219">57311b7a-9afd-4ff0-866e-9393ad6647b1</span></span>  <br/> |
|<span data-ttu-id="930bb-220">XmlFormLibrary</span><span class="sxs-lookup"><span data-stu-id="930bb-220">XmlFormLibrary</span></span>  <br/> |<span data-ttu-id="930bb-221">00BFEA71-1E1D-4562-B56A-F05371BB0115</span><span class="sxs-lookup"><span data-stu-id="930bb-221">00bfea71-1e1d-4562-b56a-f05371bb0115</span></span>  <br/> |
   
5. <span data-ttu-id="930bb-222">Speichern Sie Ihre Änderungen, und führen Sie die Bereitstellung wie gewohnt durch.</span><span class="sxs-lookup"><span data-stu-id="930bb-222">Save your changes, and deploy as you would normally.</span></span>
    
  

> <span data-ttu-id="930bb-223">**Hinweis:** Möglicherweise müssen Sie diese Features auch in der Zentraladministration aktivieren.</span><span class="sxs-lookup"><span data-stu-id="930bb-223">**Note** You may also need to activate these features in the Central Administration utility.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="930bb-224">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="930bb-224">Additional resources</span></span>
<span data-ttu-id="930bb-225"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="930bb-225"></span></span>


-  [<span data-ttu-id="930bb-226">Aktualisieren von Anpassungen für SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="930bb-226">Upgrade site customizations for SharePoint</span></span>](upgrade-site-customizations-for-sharepoint.md)
    
  
-  [<span data-ttu-id="930bb-227">SharePoint 2010 und Webvorlagen</span><span class="sxs-lookup"><span data-stu-id="930bb-227">SharePoint 2010 and web templates</span></span>](http://blogs.msdn.com/b/vesku/archive/2010/10/14/sharepoint-2010-and-web-templates.aspx)
    
  
-  [<span data-ttu-id="930bb-228">Planen eines Upgrades eine Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="930bb-228">Plan to upgrade a site collection</span></span>](https://technet.microsoft.com/de-DE/library/ff191199.aspx)
    
  
-  [<span data-ttu-id="930bb-229">Planen von websitesammlungsupgrades in SharePoint</span><span class="sxs-lookup"><span data-stu-id="930bb-229">Plan for site collection upgrades in SharePoint</span></span>](http://technet.microsoft.com/de-DE/library/ff191199.aspx)
    
  

  
    
    

