---
title: Anpassen von "modernen" Websiteseiten
description: "Benutzerdefiniertes branding in SharePoint Online verwenden, programmgesteuert \"moderne\" Seiten hinzufügen und hinzufügen, löschen oder Aktualisieren von Client-Side-Webparts auf \"modernen\" Seiten."
ms.date: 11/09/2017
ms.openlocfilehash: b22eabf437eab007a1f58a3ebfcb9c8b830805f8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="customizing-modern-site-pages"></a><span data-ttu-id="02904-103">Anpassen von "modernen" Websiteseiten</span><span class="sxs-lookup"><span data-stu-id="02904-103">Customizing "modern" site pages</span></span>

<span data-ttu-id="02904-104">Im 2016 wurde die Erfahrung "modernen" Seite vom SharePoint-Team veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="02904-104">In 2016, the "modern" page experience was released by the SharePoint team.</span></span> <span data-ttu-id="02904-105">Websiteseiten modernen Team sind schnell, einfach zu Autor und unterstützen umfangreichen multimedia-Inhalt.</span><span class="sxs-lookup"><span data-stu-id="02904-105">Modern team site pages are fast, easy to author, and support rich multimedia content.</span></span> <span data-ttu-id="02904-106">Darüber hinaus Seiten auf jedem Gerät, das in einem Browser oder innerhalb großartige die mobile SharePoint-app.</span><span class="sxs-lookup"><span data-stu-id="02904-106">Additionally, pages look great on any device, in a browser, or from within the SharePoint mobile app.</span></span> 

<span data-ttu-id="02904-107">SharePoint-Seiten werden mit Webparts, erstellt, die Sie entsprechend Ihren Anforderungen anpassen können.</span><span class="sxs-lookup"><span data-stu-id="02904-107">SharePoint pages are built with web parts, which you can customize according to your needs.</span></span> <span data-ttu-id="02904-108">Sie können Dokumente, Videos, Bilder, Website Aktivitäten, Yammer-Feeds und vieles mehr hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="02904-108">You can add documents, videos, images, site activities, Yammer feeds, and more.</span></span> <span data-ttu-id="02904-109">Nur auswählen die + signieren, und wählen Sie einen Webpart aus der Toolbox Hinzufügens von Inhalt auf der Seite an.</span><span class="sxs-lookup"><span data-stu-id="02904-109">Just select the + sign and pick a web part from the toolbox to add content to your page.</span></span> <span data-ttu-id="02904-110">Das neue "hervorgehoben Inhalte" Webpart können Sie die Kriterien einrichten, damit bestimmte Inhalt automatisch und dynamisch in diesem Bereich der Seite wird.</span><span class="sxs-lookup"><span data-stu-id="02904-110">The new “highlighted content” web part lets you set criteria so that specific content automatically and dynamically populates in that area of the page.</span></span> <span data-ttu-id="02904-111">Mithilfe der SharePoint-Framework können Entwickler benutzerdefinierte Webparts, die nach oben rechts in der Toolbox anzeigen.</span><span class="sxs-lookup"><span data-stu-id="02904-111">By using the SharePoint Framework, developers can build custom web parts that show up right in the toolbox.</span></span>

![](https://blogs.office.com/wp-content/uploads/2016/08/New-capabilities-in-SharePoint-Online-team-sites-including-integration-with-Office-365-Groups-1.gif)

<span data-ttu-id="02904-112">Dieser Artikel befasst sich die Erweiterbarkeitsoptionen die Seite "modernen" wünschen.</span><span class="sxs-lookup"><span data-stu-id="02904-112">This article focuses on the extensibility options within the "modern" page experience.</span></span> <span data-ttu-id="02904-113">Allerdings erfahren Sie mehr über die Funktionen von "modernen" dieser Kommunikationskanäle angeboten, finden Sie unter [neue Funktionen in SharePoint Online Teamwebsites einschließlich Integration mit Office 365-Gruppen](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).</span><span class="sxs-lookup"><span data-stu-id="02904-113">However, if you want to learn more about the functionalities offered by the "modern" experiences, see [New capabilities in SharePoint Online team sites including integration with Office 365 Groups](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).</span></span>

<span data-ttu-id="02904-114">Im weiteren Verlauf des Artikels verwenden "modernen" für die neue Benutzeroberfläche und "klassische" für die ältere Benutzeroberfläche wir.</span><span class="sxs-lookup"><span data-stu-id="02904-114">In the remainder of this article, we'll use "modern" for the new user experience and "classic" for the legacy user experience.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="02904-115">Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="02904-115">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="supported-customizations-for-modern-pages"></a><span data-ttu-id="02904-116">Unterstützte Anpassungen für "modernen" Seiten</span><span class="sxs-lookup"><span data-stu-id="02904-116">Supported customizations for "modern" pages</span></span>

<span data-ttu-id="02904-117">Die Anzahl von Anpassungen für "modernen" Seiten verfügbar bleiben, in das Wachstum und in diesem Artikel, wir gebe Details und Beispiele für die unterstützten Optionen.</span><span class="sxs-lookup"><span data-stu-id="02904-117">The number of customizations available for "modern" pages keeps on growing, and in this article, we'll provide details and examples of the supported options.</span></span> <span data-ttu-id="02904-118">SharePoint-Team ist funktionsfähig, um weitere Optionen in der Zukunft zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="02904-118">The SharePoint team is working to support more options in the future.</span></span> <span data-ttu-id="02904-119">Die folgende Liste enthält einen schnellen Überblick über die unterstützten Funktionen für "modernen" Seiten:</span><span class="sxs-lookup"><span data-stu-id="02904-119">The following list gives a quick overview of the supported capabilities for "modern" pages:</span></span>

 - <span data-ttu-id="02904-120">Benutzerdefiniertes branding</span><span class="sxs-lookup"><span data-stu-id="02904-120">Custom branding</span></span>
 - <span data-ttu-id="02904-121">Programmgesteuertes Hinzufügen von "modernen" Seiten</span><span class="sxs-lookup"><span data-stu-id="02904-121">Adding "modern" pages programmatically</span></span>
 - <span data-ttu-id="02904-122">Hinzufügen, löschen und Aktualisieren von Client-Side-Webparts auf "modernen" Seiten</span><span class="sxs-lookup"><span data-stu-id="02904-122">Adding, deleting, and updating client-side web parts on "modern" pages</span></span>
 - <span data-ttu-id="02904-123">Alternative Layouts (siehe Hinweis auf *SharePoint virtuellen Summit*)</span><span class="sxs-lookup"><span data-stu-id="02904-123">Alternative layouts (see note on *SharePoint Virtual Summit*)</span></span>

<span data-ttu-id="02904-124">Für diese Anpassungen werden derzeit nicht für "modernen" Seiten unterstützt:</span><span class="sxs-lookup"><span data-stu-id="02904-124">These customizations are currently not supported for "modern" pages:</span></span>

 - <span data-ttu-id="02904-125">Hinzufügen von "klassische"-Webparts auf Seiten "modern"</span><span class="sxs-lookup"><span data-stu-id="02904-125">Adding "classic" web parts on "modern" pages</span></span>
 - <span data-ttu-id="02904-126">Benutzerdefinierte CSS über AlternateCSSUrl Web-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="02904-126">Custom CSS via AlternateCSSUrl web property</span></span>
 - <span data-ttu-id="02904-127">Benutzerdefiniertes JavaScript eingebettet über benutzerdefinierte Aktionen des Benutzers (siehe Hinweis auf *SharePoint-Framework-Erweiterungen*)</span><span class="sxs-lookup"><span data-stu-id="02904-127">Custom JavaScript embedded via user custom actions (see note on *SharePoint Framework Extensions*)</span></span>
 - <span data-ttu-id="02904-128">Benutzerdefinierte Masterseiten (umfangreichere branding wird unterstützt werden später mit alternativen)</span><span class="sxs-lookup"><span data-stu-id="02904-128">Custom master pages (more extensive branding will be supported later using alternative options)</span></span>
 - <span data-ttu-id="02904-129">Minimale Downloadstrategie (MDS)</span><span class="sxs-lookup"><span data-stu-id="02904-129">Minimal Download Strategy (MDS)</span></span>

> [!NOTE]
> - <span data-ttu-id="02904-130">Es wird nicht empfohlen, "modernen" Seitenfunktionalität mit "klassische" SharePoint veröffentlichungsportale kombiniert.</span><span class="sxs-lookup"><span data-stu-id="02904-130">We don't recommend combining "modern" page functionality with "classic" SharePoint publishing portals.</span></span> <span data-ttu-id="02904-131">Standardmäßig ist die Seitenfunktionalität "modernen" auf "klassische" SharePoint veröffentlichungsportale nicht aktiviert.</span><span class="sxs-lookup"><span data-stu-id="02904-131">By default, the "modern" page functionality is not enabled on "classic" SharePoint publishing portals.</span></span>
> - <span data-ttu-id="02904-132">Im Juni 2017, [SharePoint-Framework-Erweiterungen in Vorschau für Entwickler hinausgehen](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="02904-132">In June 2017, [SharePoint Framework Extensions went into developer preview](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span></span> <span data-ttu-id="02904-133">Dieser Erweiterungen der SharePoint-Framework verwenden, können Sie steuern, das Rendering eines Felds über den benutzerdefinierten Code, und Sie können benutzerdefinierte Aktionen, die Ihre benutzerdefinierten Code auszuführen, Benutzer erstellen.</span><span class="sxs-lookup"><span data-stu-id="02904-133">Using these SharePoint Framework Extensions, you can control the rendering of a field via custom code, and you can create user custom actions that execute your custom code.</span></span> <span data-ttu-id="02904-134">Finden Sie weitere Informationen finden Sie unter [Übersicht über SharePoint Framework Extensions](http://aka.ms/spfx-extensions).</span><span class="sxs-lookup"><span data-stu-id="02904-134">To learn more, see [Overview of SharePoint Framework Extensions](http://aka.ms/spfx-extensions).</span></span> 
> - <span data-ttu-id="02904-135">Im Mai 2017, während die virtuellen SharePoint-Summit angekündigt wir [kommunikationswebsites mit konfigurierbaren Seitenlayouts](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).</span><span class="sxs-lookup"><span data-stu-id="02904-135">In May 2017, during the SharePoint Virtual Summit, we announced [communication sites with configurable page layouts](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).</span></span>  

<span data-ttu-id="02904-136"><a name="themingimpact"> </a></span><span class="sxs-lookup"><span data-stu-id="02904-136"></span></span>
## <a name="custom-branding"></a><span data-ttu-id="02904-137">Benutzerdefiniertes branding</span><span class="sxs-lookup"><span data-stu-id="02904-137">Custom branding</span></span>

<span data-ttu-id="02904-138">Verwenden eines benutzerdefinierten Designs Fall Ihrer Website wird dieses Design "modern" Seite Oberfläche wie im folgenden Beispiel dargestellt berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="02904-138">If your site happens to use a custom theme, this theme is respected in the "modern" page experience as shown in the following sample.</span></span>

<span data-ttu-id="02904-139">*Abbildung 1. Moderne Seite mit benutzerdefinierten branding kommen aus Design-Einstellungen*</span><span class="sxs-lookup"><span data-stu-id="02904-139">*Figure 1. Modern page with custom branding coming from theme settings*</span></span>

<img src="media/modern-experiences/modern-page-with-custom-theme.png" alt="Modern page with custom branding coming from theme settings" width="600">

<span data-ttu-id="02904-140"><a name="sitesversusmodernpages"> </a></span><span class="sxs-lookup"><span data-stu-id="02904-140"></span></span>
## <a name="why-a-site-may-not-have-modern-pages-functionality"></a><span data-ttu-id="02904-141">Warum kann eine Website nicht "modernen" Seiten Funktionen zur Verfügung</span><span class="sxs-lookup"><span data-stu-id="02904-141">Why a site may not have "modern" pages functionality</span></span>

<span data-ttu-id="02904-142">"Modernen" Seiten werden übermittelt, mithilfe der Seiten der Website Webbereich-Funktion (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), damit Wenn dieses Feature aktiviert wird, Ihre Website die Option hat "moderne" Seiten verwenden.</span><span class="sxs-lookup"><span data-stu-id="02904-142">The "modern" pages are delivered by using the Site Pages web scoped feature (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), so when this feature is activated, your site has the option to use "modern" pages.</span></span> <span data-ttu-id="02904-143">Wenn Sie dieses Feature Microsoft gerollt, aktiviert wir dies für alle "modernen" Teamwebsites (Gruppe #0-Websites) und für die meisten "klassische" Teamwebsites (STS #0).</span><span class="sxs-lookup"><span data-stu-id="02904-143">When Microsoft rolled out this feature, we enabled this for all "modern" team sites (GROUP#0 sites) and for most "classic" team sites (STS#0).</span></span> 

<span data-ttu-id="02904-144">Wäre eine Teamwebsite "klassische" eine große Anzahl von Webparts oder Wiki-Seiten, das Feature wurde nicht automatisch aktiviert, und das gleiche gilt für "klassische" Teamwebsites mit Features für die Veröffentlichung aktiviert.</span><span class="sxs-lookup"><span data-stu-id="02904-144">If a "classic" team site had a high count of web parts or wiki pages, the feature was not automatically enabled, and the same applies to "classic" team sites with the publishing feature enabled.</span></span> <span data-ttu-id="02904-145">Wenn "modernen" Seitenfunktionalität auf diesen Websites werden soll, können Sie weiterhin das Seiten der Website-Feature aktivieren.</span><span class="sxs-lookup"><span data-stu-id="02904-145">If you want "modern" page functionality on these sites, you can still activate the Site Pages feature.</span></span> <span data-ttu-id="02904-146">Dies bedeutet auch, dass Websites basierend auf anderen Vorlagen nicht aktivierte "modernen" Seiten-Funktionalität verfügen.</span><span class="sxs-lookup"><span data-stu-id="02904-146">This also implies that sites based on other templates do not have the "modern" pages functionality enabled.</span></span> 

<span data-ttu-id="02904-147">Der vorherige Absatz gesprochen zu wie das Feature "modernen" Seite für vorhandene Websites aktiviert wurde.</span><span class="sxs-lookup"><span data-stu-id="02904-147">The previous paragraph talked about how the "modern" page feature was enabled on existing sites.</span></span> <span data-ttu-id="02904-148">Wenn Sie eine neue "Modern" oder "klassische" team Site (Gruppe #0 oder STS #0), "moderne" Seiten der Website-Feature wird bei der Bereitstellung Zeit aktiviert.</span><span class="sxs-lookup"><span data-stu-id="02904-148">When you create a new "modern" or "classic" team site (GROUP#0 or STS#0), the "modern" Site Pages feature is enabled at provisioning time.</span></span> <span data-ttu-id="02904-149">Das "moderne" Seiten der Website-Feature ist nicht auf Websites aktiviert, die auf andere Vorlagen basieren.</span><span class="sxs-lookup"><span data-stu-id="02904-149">The "modern" Site Pages feature is not enabled on sites that are based on other templates.</span></span>

<span data-ttu-id="02904-150"><a name="configuremodernpages"> </a></span><span class="sxs-lookup"><span data-stu-id="02904-150"></span></span>
## <a name="configuring-the-end-user-experience"></a><span data-ttu-id="02904-151">Konfigurieren des Endbenutzers</span><span class="sxs-lookup"><span data-stu-id="02904-151">Configuring the end user experience</span></span>

<span data-ttu-id="02904-152">Sie haben mehrere Optionen können Sie steuern, ob die Seite "modernen" oder "klassische" Erfahrung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="02904-152">You have multiple options to control whether the "modern" or "classic" page experience is used.</span></span> 

### <a name="tenant-level-configuration"></a><span data-ttu-id="02904-153">Ebene Mandantenkonfiguration</span><span class="sxs-lookup"><span data-stu-id="02904-153">Tenant level configuration</span></span>

<span data-ttu-id="02904-154">Wenn Sie die "moderne" Erfahrung vollständig deaktivieren möchten, empfiehlt es sich mit dem Mandanten für diese Einstellung.</span><span class="sxs-lookup"><span data-stu-id="02904-154">If you want to completely disable the "modern" experience, it's best to use the tenant setting for this.</span></span> <span data-ttu-id="02904-155">Wechseln Sie zu Ihrem Mandanten Administrationscenter (beispielsweise Contoso-admin.sharepoint.com), wechseln Sie zu Einstellungen, und wählen Sie die "klassische" wünschen.</span><span class="sxs-lookup"><span data-stu-id="02904-155">Go to your tenant admin center (for example, contoso-admin.sharepoint.com), go to Settings, and select the "classic" experience.</span></span>

<span data-ttu-id="02904-156">*Abbildung 2. Im Abschnitt Website-Seiten in der SharePoint-Mandanten bezogenen Einstellungen in Admin UI*</span><span class="sxs-lookup"><span data-stu-id="02904-156">*Figure 2. Site Pages section in the SharePoint tenant scoped settings in Admin UI*</span></span>

![Im Abschnitt Website-Seiten in der SharePoint-Mandanten bezogenen Einstellungen in Admin UI](media/modern-experiences/site-pages-setting-admin-ui.png)

> [!NOTE]
> - <span data-ttu-id="02904-158">Die Einstellung der Mandant kann etwas verwirrend sein. **Verhindern, dass Benutzer Seiten der Website erstellen** werden tatsächlich die "klassische" wünschen.</span><span class="sxs-lookup"><span data-stu-id="02904-158">The tenant level setting can be a little confusing; **Prevent users from creating Site Pages** actually brings back the "classic" experience.</span></span>
> - <span data-ttu-id="02904-159">Die aktuelle Konfiguration zwischengespeichert ist, und meldet sich ab sofort die Sitzung mit dem Effekt der von dieser Änderung.</span><span class="sxs-lookup"><span data-stu-id="02904-159">The current configuration is cached, and signing off the session immediately shows the effect of this change.</span></span>

### <a name="web-level-configuration"></a><span data-ttu-id="02904-160">Konfiguration der Web-Ebene</span><span class="sxs-lookup"><span data-stu-id="02904-160">Web level configuration</span></span>

<span data-ttu-id="02904-161">Sie können verhindern, dass eine Web mithilfe der Seite "modernen" Erfahrung durch das Webbereich Feature mit der ID **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** deaktivieren (Name = "Seiten der Website").</span><span class="sxs-lookup"><span data-stu-id="02904-161">You can prevent a web from using the "modern" page experience by disabling the web scoped feature with ID **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** (name = "Site Pages").</span></span> <span data-ttu-id="02904-162">Um die Seite "modernen" Erfahrung auf der Ebene der Webserver wieder zu aktivieren, müssen Sie das Feature wieder aktivieren.</span><span class="sxs-lookup"><span data-stu-id="02904-162">To re-enable the "modern" page experience at the web level, you need to activate the feature again.</span></span>

<span data-ttu-id="02904-163">Verwenden Sie die folgenden [Plug & Play-PowerShell](http://aka.ms/sppnp-powershell) So aktivieren oder deaktivieren Sie die erforderlichen Features:</span><span class="sxs-lookup"><span data-stu-id="02904-163">Use the following [PnP PowerShell](http://aka.ms/sppnp-powershell) to enable/disable the needed features:</span></span>

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent site pages at web level
Disable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
# And again enable site pages at web
#Enable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
```

> [!NOTE]
> <span data-ttu-id="02904-164">Wenn Sie das Feature deaktivieren, können Sie nicht mehr neue "moderne" Seiten erstellen, aber die bereits erstellten Seiten arbeiten, verwenden die "modernen" Benutzeroberfläche bleiben.</span><span class="sxs-lookup"><span data-stu-id="02904-164">When you disable the feature, you can no longer create new "modern" pages, but the already created pages stay working using the "modern" user experience.</span></span> 

### <a name="commenting-configuration"></a><span data-ttu-id="02904-165">Kommentierung Konfiguration</span><span class="sxs-lookup"><span data-stu-id="02904-165">Commenting configuration</span></span>

<span data-ttu-id="02904-166">Standardmäßig können Benutzer Kommentare (Juli 2017) auf "modernen" Seiten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="02904-166">By default, users can add comments (July 2017) on "modern" pages.</span></span> <span data-ttu-id="02904-167">Wenn Ihre Organisation dieses Feature nicht möchte, kann es über den Mandanten Administrationscenter auf der Seite Einstellungen deaktiviert werden.</span><span class="sxs-lookup"><span data-stu-id="02904-167">If your organization does not want this feature, it can be disabled from the tenant Admin center on the Settings page.</span></span>

<span data-ttu-id="02904-168">*Abbildung 3. Aktivieren oder Deaktivieren der Kommentare*</span><span class="sxs-lookup"><span data-stu-id="02904-168">*Figure 3. Enable or disable comments*</span></span>

![Aktivieren oder Deaktivieren der Kommentare](http://i.imgur.com/atl91Vh.png)

> [!NOTE]
> <span data-ttu-id="02904-170">Können Sie auch programmgesteuert das Kommentare Verhalten mithilfe der Website verwalten und Mandanten-Level-APIs (erfordert SharePoint Client-Side Object Model 16.1.6621.1200 (CSOM) oder höher):</span><span class="sxs-lookup"><span data-stu-id="02904-170">You can also programmatically manage the commenting behavior by using site and tenant level APIs (requires SharePoint Client-Side Object Model (CSOM) version 16.1.6621.1200 or later):</span></span>
> - <span data-ttu-id="02904-171">Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled</span><span class="sxs-lookup"><span data-stu-id="02904-171">Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled</span></span> 
> - <span data-ttu-id="02904-172">Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled</span><span class="sxs-lookup"><span data-stu-id="02904-172">Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled</span></span>


## <a name="programming-modern-pages"></a><span data-ttu-id="02904-173">Programmieren von "modernen" Seiten</span><span class="sxs-lookup"><span data-stu-id="02904-173">Programming "modern" pages</span></span>

### <a name="adding-modern-pages"></a><span data-ttu-id="02904-174">Hinzufügen von "modernen" Seiten</span><span class="sxs-lookup"><span data-stu-id="02904-174">Adding "modern" pages</span></span>
<span data-ttu-id="02904-175">Erstellen einer Seite "modernen" darum, Erstellen eines Listenelements in der Seitenbibliothek der Website und Zuweisen des richtigen Inhaltstyps in Kombination mit einige zusätzlichen Eigenschaften festlegen, wie im folgenden Codeausschnitt dargestellt:</span><span class="sxs-lookup"><span data-stu-id="02904-175">Creating a "modern" page comes down to creating a list item in the site pages library and assigning it the correct content type combined with setting some additional properties as shown in the following code snippet:</span></span>

```C#
// pagesLibrary is List object for the "site pages" library of the site
ListItem item = pagesLibrary.RootFolder.Files.AddTemplateFile(serverRelativePageName, TemplateFileType.ClientSidePage).ListItemAllFields;

// Make this page a "modern" page
item["ContentTypeId"] = "0x0101009D1CB255DA76424F860D91F20E6C4118";
item["Title"] = System.IO.Path.GetFileNameWithoutExtension("mypage.aspx");
item["ClientSideApplicationId"] = "b6917cb1-93a0-4b97-a84d-7cf49975d4ec";
item["PageLayoutType"] = "Article";
item["PromotedState"] = "0";
item["CanvasContent1"] = "<div></div>";
item["BannerImageUrl"] = "/_layouts/15/images/sitepagethumbnail.png";
item.Update();
clientContext.Load(item);
clientContext.ExecuteQuery();

```

<br/>

<span data-ttu-id="02904-176">Wenn Sie Plug & Play-(seit der Version März 2017) verwenden, können Sie unsere Erweiterungsmethoden nutzen, erhalten Sie ein Modell für eine Seite auf einfache Weise hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="02904-176">When using PnP (as of the March 2017 release), you can leverage our extension methods, which gives you a model for adding a page easily:</span></span>

```C#
cc.Web.AddClientSidePage("mypage.aspx", true);
```

> [!IMPORTANT]
> <span data-ttu-id="02904-177">Ab September 2017, erstellte Seiten der `AddTemplateFile` Methode haben keine Vorschau, wenn Sie von der Suchergebnisseite darüber bewegen.</span><span class="sxs-lookup"><span data-stu-id="02904-177">As of September 2017, pages created using the `AddTemplateFile` method do not have a preview when you hover over them from the search results page.</span></span> <span data-ttu-id="02904-178">Microsoft arbeitet an einem Fix/Alternative Lösung für dieses.</span><span class="sxs-lookup"><span data-stu-id="02904-178">Microsoft is working on a fix/alternative solution for this.</span></span>

### <a name="using-the-pnp-support-for-modern-pages-and-client-side-web-parts"></a><span data-ttu-id="02904-179">Verwenden die Plug & Play-Unterstützung für "modernen" Seiten und clientseitige Webparts</span><span class="sxs-lookup"><span data-stu-id="02904-179">Using the PnP support for "modern" pages and client-side web parts</span></span>

<span data-ttu-id="02904-180">Die März 2017-Version unterstützt die [Plug & Play-Websites core-Bibliothek](http://aka.ms/sppnp) erstellen, aktualisieren und Löschen von Seiten mithilfe der clientseitigen.</span><span class="sxs-lookup"><span data-stu-id="02904-180">As of the March 2017 release, the [PnP Sites core library](http://aka.ms/sppnp) offers support for creating, updating, and deleting client-side pages.</span></span> <span data-ttu-id="02904-181">In diesem Abschnitt finden Sie Informationen dazu, wie Sie mithilfe der clientseitigen-Seiten, die mithilfe der [Plug & Play-Websites core-Bibliothek auf GitHub](https://github.com/SharePoint/PnP-Sites-Core)entwickelt.</span><span class="sxs-lookup"><span data-stu-id="02904-181">This section gives you information about how to work with client-side pages using the [PnP Sites core library on GitHub](https://github.com/SharePoint/PnP-Sites-Core).</span></span>

#### <a name="create-a-new-page-and-add-a-text-web-part"></a><span data-ttu-id="02904-182">Erstellen einer neuen Seite und Hinzufügen eines Text-Webparts</span><span class="sxs-lookup"><span data-stu-id="02904-182">Create a new page and add a text web part</span></span>

<span data-ttu-id="02904-183">In diesem Beispiel erstellen eine neue Seite mithilfe der clientseitigen im Arbeitsspeicher wir, fügen Sie ein rich-Text-Editor-Steuerelement und schließlich die Seite in der Bibliothek für Seiten Website als mypage.aspx speichern.</span><span class="sxs-lookup"><span data-stu-id="02904-183">In this sample, we create a new client-side page in memory, add a rich text editor control, and finally save the page to the site pages library as mypage.aspx.</span></span> <span data-ttu-id="02904-184">Im erste Schritt wird eine Instanz des ClientSidePage erstellen, und klicken Sie dann wir instanziieren Sie ein Steuerelement, das wir mithilfe von auf der Seite hinzufügen die `AddControl` Methode.</span><span class="sxs-lookup"><span data-stu-id="02904-184">The first step is creating a ClientSidePage instance, and then we instantiate a control that we add on the page by using the `AddControl` method.</span></span> <span data-ttu-id="02904-185">Nachdem ausgeführt wurde, wird die Seite gespeichert.</span><span class="sxs-lookup"><span data-stu-id="02904-185">After that's done, the page is saved.</span></span>

```C#
// cc is the ClientContext instance for the site you're working with
ClientSidePage myPage = new ClientSidePage(cc);

ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks" };
myPage.AddControl(txt1, 0);
myPage.Save("mypage.aspx");
```

#### <a name="load-an-existing-page"></a><span data-ttu-id="02904-186">Laden Sie eine vorhandene Seite</span><span class="sxs-lookup"><span data-stu-id="02904-186">Load an existing page</span></span> 

<span data-ttu-id="02904-187">Wenn Sie ändern oder eine vorhandene Seite kopieren möchten, können Sie diese Seite in der Plug & Play-Client-seitigen Objektmodell laden; das Laden transformiert"" HTML-Inhalte Sie in ein Objektmodell, die Sie bearbeiten können.</span><span class="sxs-lookup"><span data-stu-id="02904-187">When you want to modify or copy an existing page, you can load that page into the PnP client-side object model; the loading "transforms" the HTML content into an object model that you can manipulate.</span></span> <span data-ttu-id="02904-188">Laden eine vorhandene Seite erfolgt mithilfe der `Load` Methode.</span><span class="sxs-lookup"><span data-stu-id="02904-188">Loading an existing page is done by using the `Load` method.</span></span>

```C#
// load the page with name "page3.aspx"
ClientSidePage p = ClientSidePage.Load(cc, "page3.aspx");

// perform your page updates
...

// save the page back to SharePoint
p.Save()
```

#### <a name="add-a-section"></a><span data-ttu-id="02904-189">Hinzufügen eines Abschnitts</span><span class="sxs-lookup"><span data-stu-id="02904-189">Add a section</span></span>

<span data-ttu-id="02904-190">Seiten können ein flexibles Layout haben. Sie können einen oder mehrere Abschnitte auf einer Seite hinzufügen, und diese Abschnitte können bis zu drei Spalten haben.</span><span class="sxs-lookup"><span data-stu-id="02904-190">Pages can have a flexible layout; you can add one or more sections on a page, and these sections can have up to three columns.</span></span> <span data-ttu-id="02904-191">Sie können mithilfe der SharePoint-Benutzeroberfläche von Abschnitten Seiten hinzufügen, oder können Sie dies programmgesteuert tun.</span><span class="sxs-lookup"><span data-stu-id="02904-191">You can add sections to your pages by using the SharePoint user interface, or you can do this programmatically.</span></span>

```C#
var page2 = cc.Web.AddClientSidePage("PageWithSections.aspx", true);
page2.AddSection(CanvasSectionTemplate.ThreeColumn, 5);
page2.AddSection(CanvasSectionTemplate.TwoColumn, 10);
```

#### <a name="add-an-out-of-the-box-web-part"></a><span data-ttu-id="02904-192">Hinzufügen eines Out-of-Box-Webparts</span><span class="sxs-lookup"><span data-stu-id="02904-192">Add an out-of-the-box web part</span></span> 
<span data-ttu-id="02904-193">Das folgende Beispiel zeigt, wie Sie ein Out-of-Box- **Bild** mithilfe der clientseitigen-Webpart auf einer Seite hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="02904-193">The following sample shows how you can add an out-of-the-box **image** client-side web part on a page.</span></span> <span data-ttu-id="02904-194">Beachten Sie, dass wir mithilfe von Webpart-Objekts Instanziieren der `InstantiateDefaultWebPart` -Methodenaufruf.</span><span class="sxs-lookup"><span data-stu-id="02904-194">Note that we instantiate the web part object by using the `InstantiateDefaultWebPart` method call.</span></span> <span data-ttu-id="02904-195">Nachdem das Webpart gestartet wurde, sind die Standardeigenschaften im Webpart-Manifest definiert seine Eigenschaften fest.</span><span class="sxs-lookup"><span data-stu-id="02904-195">After the web part is initiated, its properties are set to the default properties defined in the web part manifest.</span></span> <span data-ttu-id="02904-196">Für die meisten Webparts müssen Sie die Eigenschaften zu aktualisieren, wie in diesem Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="02904-196">For most web parts, you need to update the properties as shown in this sample.</span></span>

```C#
ClientSidePage page5 = new ClientSidePage(cc);
var imageWebPart = page5.InstantiateDefaultWebPart(DefaultClientSideWebParts.Image);
imageWebPart.Properties["imageSourceType"] = 2;
imageWebPart.Properties["siteId"] = "c827cb03-d059-4956-83d0-cd60e02e3b41";
imageWebPart.Properties["webId"] = "9fafd7c0-e8c3-4a3c-9e87-4232c481ca26";
imageWebPart.Properties["listId"] = "78d1b1ac-7590-49e7-b812-55f37c018c4b";
imageWebPart.Properties["uniqueId"] = "3C27A419-66D0-4C36-BF24-BD6147719052";
imageWebPart.Properties["imgWidth"] = 1002;
imageWebPart.Properties["imgHeight"] = 469;
page5.AddControl(imageWebPart);
page5.Save("page5.aspx");

```

#### <a name="add-a-custom-client-side-web-part"></a><span data-ttu-id="02904-197">Hinzufügen eines benutzerdefinierten Webparts mithilfe der clientseitigen</span><span class="sxs-lookup"><span data-stu-id="02904-197">Add a custom client-side web part</span></span>

<span data-ttu-id="02904-198">Vorherigen Beispiele zum Arbeiten mit Webparts Out-of-Box ergab, aber Sie können auch Ihre benutzerdefinierte erstellt mithilfe der clientseitigen-Webparts zu einer Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="02904-198">Previous samples showed how to work with out-of-the-box web parts, but you can also add your custom built client-side web parts to a page.</span></span> <span data-ttu-id="02904-199">Zunächst Abrufen Ihrer Webpart Informationen mithilfe der `AvailableClientSideComponents` -Methode, und suchen Sie nach Ihrem Web Teil, und verwenden Sie die Informationen zur Instanziierung finden Sie eine `ClientSideWebPart` -Instanz, die die Seite im letzten Schritt hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="02904-199">You would start by getting your web part information by using the `AvailableClientSideComponents` method, and then search for your web part and use the information you find to instantiate a `ClientSideWebPart` instance, which is added to the page in the last step.</span></span>

```C#
ClientSidePage p = new ClientSidePage(cc);

// get a list of possible client side web parts that can be added
var components = p.AvailableClientSideComponents();

// Find our custom "HelloWord" web part
var myWebPart = components.Where(s => s.ComponentType == 1 && s.Name == "HelloWorld").FirstOrDefault();
if (myWebPart != null)
{
    // Instantiate a client side web part from our found web part information
    ClientSideWebPart helloWp = new ClientSideWebPart(myWebPart) { Order = 10 };
    // Add the custom client side web part to the page
    p.AddControl(helloWp);
}

// Persist the page to SharePoint
p.Save("PnPRocks.aspx");
```

#### <a name="adjust-control-order"></a><span data-ttu-id="02904-200">Reihenfolge Steuerelements anpassen</span><span class="sxs-lookup"><span data-stu-id="02904-200">Adjust control order</span></span>
<span data-ttu-id="02904-201">Sie haben verschiedene Methoden, um die Reihenfolge zu steuern, in der die Steuerelemente auf der Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="02904-201">You have different methods to control the order in which the controls appear on the page.</span></span> <span data-ttu-id="02904-202">Der wichtige Aspekt ist die `Order` -Attribut für das aktuelle Steuerelement: die Liste der Steuerelemente wird durch den Wert der, die sortiert `Order` Attribut, wenn die HTML-Seite wird generiert, und die Reihenfolge, in der HTML-Code die Reihenfolge auch zur Seite Renderingzeit ist.</span><span class="sxs-lookup"><span data-stu-id="02904-202">The key aspect is the `Order` attribute on the actual control: the list of controls is sorted by the value of that `Order` attribute when the page HTML is generated, and the order in the HTML is also the order at page rendering time.</span></span>

```C#
// Set the order when initiating the control
ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks", Order = 5 };

// Set the order when you add the control to the page, in this case we want the control to be the first
myPage.AddControl(txt1, -1);

// Manipulate the control order on the page...e.g. move a control to the back
myPage.Controls[1].Order = 10;

```

#### <a name="delete-a-control"></a><span data-ttu-id="02904-203">Löschen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="02904-203">Delete a control</span></span>

<span data-ttu-id="02904-204">Wenn Sie ein Steuerelement auf einer Seite löschen möchten, können Sie einfach Aufrufen der `Delete` Methode für das Steuerelement, und speichern Sie die Seite zurück.</span><span class="sxs-lookup"><span data-stu-id="02904-204">If you want to delete a control from a page, you can simply call the `Delete` method on the control and save the page back.</span></span>

```C#
ClientSidePage deleteDemoPage = ClientSidePage.Load(cc, "page3.aspx");
deleteDemoPage.Controls[0].Delete();
deleteDemoPage.Save();
```

#### <a name="delete-a-page"></a><span data-ttu-id="02904-205">Löschen einer Seite</span><span class="sxs-lookup"><span data-stu-id="02904-205">Delete a page</span></span> 

<span data-ttu-id="02904-206">Schließlich können Sie eine Client-seitigen Seite löschen.</span><span class="sxs-lookup"><span data-stu-id="02904-206">Finally, you can delete a client-side page.</span></span>

```C#
ClientSidePage p = ClientSidePage.Load(cc, "deleteme.aspx");
p.Delete();
```

#### <a name="class-model"></a><span data-ttu-id="02904-207">Klassenmodell</span><span class="sxs-lookup"><span data-stu-id="02904-207">Class model</span></span>

<span data-ttu-id="02904-208">Die folgende Abbildung zeigt die wichtigsten Klassen, die, denen Sie beim Verwenden des Plug & Play-Client-seitigen Seite-Objektmodells mit arbeiten werden.</span><span class="sxs-lookup"><span data-stu-id="02904-208">The following figure shows the most important classes you'll be working with when using the PnP client-side page object model.</span></span>

<span data-ttu-id="02904-209">*Abbildung 4. Plug & Play-Client-seitigen Objektmodell*</span><span class="sxs-lookup"><span data-stu-id="02904-209">*Figure 4. PnP client-side object model*</span></span>

![Plug & Play-Client-seitigen Objektmodell](media/pnpclientsideobjectmodel.png)

## <a name="additional-considerations"></a><span data-ttu-id="02904-211">Zusätzliche Überlegungen</span><span class="sxs-lookup"><span data-stu-id="02904-211">Additional considerations</span></span>

<span data-ttu-id="02904-212">Es werden weitere Optionen zur Anpassung der "modernen" Seiten wünschen schrittweise einzuführen.</span><span class="sxs-lookup"><span data-stu-id="02904-212">We'll gradually introduce more customization options for the "modern" pages experience.</span></span> <span data-ttu-id="02904-213">Diese Optionen werden mit der Veröffentlichung von SharePoint-Framework Zusatzfunktionen ausgerichtet.</span><span class="sxs-lookup"><span data-stu-id="02904-213">These options will be aligned with the release of additional SharePoint Framework capabilities.</span></span> <span data-ttu-id="02904-214">Derzeit keine genauen Zeitplan vorhanden ist, aber wir werden in den Artikeln "modernen" Erfahrung aktualisieren, sobald neue Funktionen freigegeben werden.</span><span class="sxs-lookup"><span data-stu-id="02904-214">Currently, there is no exact schedule available, but we'll update the "modern" experience articles whenever new capabilities are released.</span></span>

## <a name="see-also"></a><span data-ttu-id="02904-215">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="02904-215">See also</span></span>

- [<span data-ttu-id="02904-216">Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="02904-216">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="02904-217">Erlauben Sie oder verhindern Sie der Erstellung von modernen Websiteseiten durch Endbenutzer</span><span class="sxs-lookup"><span data-stu-id="02904-217">Allow or prevent creation of modern site pages by end users</span></span>](https://support.office.com/en-us/article/Allow-or-prevent-creation-of-modern-site-pages-by-end-users-c41d9cc8-c5c0-46b4-8b87-ea66abc6e63b?ui=en-US&rs=en-US&ad=US)
