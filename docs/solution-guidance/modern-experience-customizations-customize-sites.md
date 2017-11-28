---
title: Anpassen von "modernen" Teamwebsites
description: Anwenden eines benutzerdefinierten Designs zu einer "modernen" Teamsite in SharePoint Online.
ms.date: 11/08/2017
ms.openlocfilehash: 4341876f6ee07018325c5cc089cc28728538ab10
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="customizing-modern-team-sites"></a><span data-ttu-id="82a4c-103">Anpassen von "modernen" Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="82a4c-103">Customizing "modern" team sites</span></span>

<span data-ttu-id="82a4c-104">Im 2016 veröffentlicht das SharePoint Online-Team Websites "modernen" für die Zusammenarbeit.</span><span class="sxs-lookup"><span data-stu-id="82a4c-104">In 2016, the SharePoint Online team released "modern" collaboration sites.</span></span> <span data-ttu-id="82a4c-105">Diese "modernen" Teamwebsites in Office 365 Gruppen integriert werden und eine erheblich verbesserte Endbenutzers bringen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-105">These "modern" team sites are integrated with Office 365 groups and bring a greatly improved end user experience.</span></span> <span data-ttu-id="82a4c-106">"Modernen" Teamwebsites sind entwurfsbedingt schnell und viel schneller erstellen und aus Sicht der Endbenutzer verwenden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-106">"Modern" team sites are responsive by design and are much faster to create and use from an end user perspective.</span></span> <span data-ttu-id="82a4c-107">Es folgen einige der wichtigsten Vorteile der "modernen" Teamwebsites:</span><span class="sxs-lookup"><span data-stu-id="82a4c-107">Following are some of the key benefits of the "modern" team sites:</span></span>

- <span data-ttu-id="82a4c-108">Entwickelt für die horizontale Skalierung für jedes Gerät systemintern ohne Anpassungen für eine vollständig Reaktionsfähigkeit bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-108">Designed to scale for any device natively without customizations for a fully responsive experience.</span></span>
- <span data-ttu-id="82a4c-109">Enthalten Sie systemeigene News, Quicklinks und Aktivität Funktionen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-109">Contain native news, quick links, and activity capabilities.</span></span> 
- <span data-ttu-id="82a4c-110">Integration mit Office 365-Gruppen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-110">Integrated with Office 365 groups.</span></span> 
- <span data-ttu-id="82a4c-111">Wesentlich schneller websiteerstellung im Vergleich zu Teamwebsites "klassische".</span><span class="sxs-lookup"><span data-stu-id="82a4c-111">Significantly faster site creation compared to "classic" team sites.</span></span>
- <span data-ttu-id="82a4c-112">Einschließen Sie "modernen" Listen und Bibliotheken mit Support für Microsoft Flow und PowerApps.</span><span class="sxs-lookup"><span data-stu-id="82a4c-112">Include "modern" lists and libraries with support for Microsoft Flow and PowerApps.</span></span>
- <span data-ttu-id="82a4c-113">Enthalten Sie "modernen" Seite Bearbeitungsfunktionen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-113">Contain "modern" page editing capabilities.</span></span>
- <span data-ttu-id="82a4c-114">Enthalten Sie eine Seite mit zusätzlichen Insights auf der Websiteverwendung aktualisierte Websiteinhalte.</span><span class="sxs-lookup"><span data-stu-id="82a4c-114">Include an updated site contents page with additional insights on site usage.</span></span>

<span data-ttu-id="82a4c-115">In diesem Artikel konzentriert sich auf die der verfügbaren Erweiterbarkeitsoptionen "modernen" Teamwebsites:</span><span class="sxs-lookup"><span data-stu-id="82a4c-115">This article concentrates on the available extensibility options within "modern" team sites:</span></span>

- [<span data-ttu-id="82a4c-116">Neue Funktionen in SharePoint Online, einschließlich der Integration mit Office 365 Gruppen Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="82a4c-116">New capabilities in SharePoint Online team sites including integration with Office 365 Groups</span></span>](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups)
- [<span data-ttu-id="82a4c-117">Erstellen von verbundenen SharePoint Online Teamwebsites in Sekunden</span><span class="sxs-lookup"><span data-stu-id="82a4c-117">Create connected SharePoint Online team sites in seconds</span></span>](https://blogs.office.com/2016/11/08/create-connected-sharepoint-online-team-sites-in-seconds)
- [<span data-ttu-id="82a4c-118">Ermöglichen oder verhindern, dass benutzerdefinierte Skripts</span><span class="sxs-lookup"><span data-stu-id="82a4c-118">Allow or prevent custom script</span></span>](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US)

> [!IMPORTANT]
> <span data-ttu-id="82a4c-119">Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-119">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

<span data-ttu-id="82a4c-120"><a name="supportedcustomizations"> </a></span><span class="sxs-lookup"><span data-stu-id="82a4c-120"></span></span>
## <a name="supported-customizations-on-modern-team-sites"></a><span data-ttu-id="82a4c-121">Unterstützte Anpassungen von "modernen" Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="82a4c-121">Supported customizations on "modern" team sites</span></span>

<span data-ttu-id="82a4c-122">"Modernen" Websites haben eine andere Ebene Anpassungsoptionen im Vergleich zu Teamwebsites "klassische".</span><span class="sxs-lookup"><span data-stu-id="82a4c-122">"Modern" sites have a different level of customization options compared to "classic" team sites.</span></span> <span data-ttu-id="82a4c-123">Über einen Zeitraum wird eine Einführung Weitere Anpassungsoptionen hauptsächlich Konzentration auf Erweiterbarkeit und branding.</span><span class="sxs-lookup"><span data-stu-id="82a4c-123">Over time we'll introduce additional customization options, mainly focusing on extensibility and branding.</span></span> <span data-ttu-id="82a4c-124">Die folgende Liste enthält einen schnellen Überblick über die unterstützten Funktionen für "modernen" Teamwebsites.</span><span class="sxs-lookup"><span data-stu-id="82a4c-124">The following list gives a quick overview of the supported capabilities for "modern" team sites.</span></span> <span data-ttu-id="82a4c-125">Sie haben folgenden Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="82a4c-125">You can:</span></span>

- <span data-ttu-id="82a4c-126">Anwenden eines benutzerdefinierten Designs, oder ändern Sie das Logo.</span><span class="sxs-lookup"><span data-stu-id="82a4c-126">Apply a custom theme or change the logo.</span></span>
- <span data-ttu-id="82a4c-127">Ein Out-of-Box-Design anwenden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-127">Apply an out-of-the-box theme.</span></span>
- <span data-ttu-id="82a4c-128">Erstellen Sie benutzerdefinierte Websitespalten (Felder) und Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-128">Create custom site columns (fields) and content types.</span></span>
- <span data-ttu-id="82a4c-129">Erstellen von Listen und Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="82a4c-129">Create lists and libraries.</span></span>
- <span data-ttu-id="82a4c-130">Konfigurieren von Einstellungen der Website, wie beispielsweise regionale Einstellungen, Sprachen und Überwachungsrichtlinien.</span><span class="sxs-lookup"><span data-stu-id="82a4c-130">Configure site settings, such as regional settings, languages, and auditing settings.</span></span>

> [!NOTE]
> <span data-ttu-id="82a4c-131">Standardmäßig weist eine Teamwebsite "modernen" AppleScript deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="82a4c-131">By default, a "modern" team site has scripting capabilities turned off.</span></span> <span data-ttu-id="82a4c-132">Sie können ein benutzerdefiniertes Design trotzdem anwenden, jedoch können nicht führen Sie ein benutzerdefiniertes Design in den Designkatalog als Option für Endbenutzer.</span><span class="sxs-lookup"><span data-stu-id="82a4c-132">You can still apply a custom theme, but you cannot introduce a custom theme to the theme gallery as an option for end users.</span></span> <span data-ttu-id="82a4c-133">Wenn Sie ein Design in den Designkatalog hinzufügen möchten, müssen Sie auf der Website [Skripts aktivieren möchten](https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f) .</span><span class="sxs-lookup"><span data-stu-id="82a4c-133">If you want to add a theme to the theme gallery, you need to [enable scripting](https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f) on the site.</span></span>

<span data-ttu-id="82a4c-134"><a name="notsupported"> </a></span><span class="sxs-lookup"><span data-stu-id="82a4c-134"></span></span>
### <a name="whats-not-supported-on-modern-team-sites"></a><span data-ttu-id="82a4c-135">Was ist auf "modernen" Teamwebsites nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="82a4c-135">What's not supported on "modern" team sites</span></span>

<span data-ttu-id="82a4c-136">Zahlreiche Bereiche auf den "modernen" Teamwebsites sind die typischen Anpassungen zurzeit nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="82a4c-136">In numerous areas on the "modern" team sites, the typical customizations are not currently available.</span></span> <span data-ttu-id="82a4c-137">Weiterer Unterstützung werden für einige dieser Themen verfügbar sein, wenn sie bereit sind, freigegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="82a4c-137">Further support will be available for some of these topics when they are ready to be released.</span></span> <span data-ttu-id="82a4c-138">Es folgt eine Liste der derzeit nicht unterstützte Anpassungen von "modernen" Teamwebsites:</span><span class="sxs-lookup"><span data-stu-id="82a4c-138">Following is a list of currently unsupported customizations on "modern" team sites:</span></span>

- <span data-ttu-id="82a4c-139">Benutzerdefinierte Masterseiten; eine ausführlichere branding wird später mit alternative Optionen unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-139">Custom master pages; more extensive branding will be supported later using alternative options.</span></span>
- <span data-ttu-id="82a4c-140">Ändern der "modernen" Website "klassische" seattle.master oder oslo.master verwenden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-140">Changing "modern" site to use "classic" seattle.master or oslo.master.</span></span>
- <span data-ttu-id="82a4c-141">Benutzerdefinierten Seitenlayouts; Wir suchen nach wegen, um die Unterstützung für mehrere explizite in der Zukunft haben.</span><span class="sxs-lookup"><span data-stu-id="82a4c-141">Custom page layouts; we are looking to have support for multiple canvases in the future.</span></span>
- <span data-ttu-id="82a4c-142">Aktivieren der Website oder Websitesammlung begrenzt Veröffentlichungsfeatures. Technisch gesehen Features derzeit aktiviert werden können, aber dies wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="82a4c-142">Enabling site or site collection scoped publishing features; technically, features can be currently activated, but this is not a supported configuration.</span></span>
- <span data-ttu-id="82a4c-143">Benutzerdefinierte Benutzeraktionen / benutzerdefiniertes JavaScript; mehr kontrolliert JavaScript auf den Seiten über die SharePoint-Framework-Erweiterungen (derzeit in Developer Preview) eingebettet werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-143">User custom actions / custom JavaScript; there will be a more controlled way to embed JavaScript on the pages through the SharePoint Framework Extensions (currently in dev preview).</span></span>
- <span data-ttu-id="82a4c-144">"Modernen" Unterwebsites; Unterwebsites auf "modernen" Teamwebsites erstellten verwenden der "klassischen" wünschen, aber Sie können die Benutzeroberfläche "modernen" Websites ähnlich sein, um ändern.</span><span class="sxs-lookup"><span data-stu-id="82a4c-144">"Modern" subsites; subsites created on "modern" team sites use the "classic" experience, but you can change the user experience to be similar to "modern" sites.</span></span>
- <span data-ttu-id="82a4c-145">Die Möglichkeit, verfügbaren Unterwebsite Vorlagenoptionen steuern.</span><span class="sxs-lookup"><span data-stu-id="82a4c-145">Ability to control available subsite template options.</span></span>
- <span data-ttu-id="82a4c-146">"Klassische" Veröffentlichen von Features (WCM).</span><span class="sxs-lookup"><span data-stu-id="82a4c-146">"Classic" publishing features (WCM).</span></span>
- <span data-ttu-id="82a4c-147">Aktivierung von Communityfeature oder der Community Unterwebsites unter "modernen" Teamwebsite Creation.</span><span class="sxs-lookup"><span data-stu-id="82a4c-147">Activation of community feature or creation of community subsites under "modern" team site.</span></span>

<span data-ttu-id="82a4c-148">Da "modernen" Teamwebsites auch haben AppleScript deaktiviert (es ist eine so genannte NoScript-Website), zahlreiche Bereiche können nicht angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-148">Because "modern" team sites also have scripting capabilities disabled (it's a so called NoScript site), numerous areas cannot be customized.</span></span> <span data-ttu-id="82a4c-149">Die Auswirkung NoScript ist für "modernen" oder "klassische" Sites identisch.</span><span class="sxs-lookup"><span data-stu-id="82a4c-149">The impact of NoScript is the same for "modern" or "classic" sites.</span></span> <span data-ttu-id="82a4c-150">"Modernen" Websites haben NoScript standardmäßig aktiviert, was bedeutet, dass Skriptfunktionen nicht verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="82a4c-150">"Modern" sites have NoScript enabled by default, meaning that scripting capabilities are not available.</span></span> <span data-ttu-id="82a4c-151">Es ist jedoch möglich und unterstützte NoScript Einstellungen in "modernen" und "klassische" Websites, um weitere einige Funktionen aktivieren deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="82a4c-151">However, it is possible and supported to disable NoScript settings in both "modern" and "classic" sites to further enable some capabilities.</span></span> 

<span data-ttu-id="82a4c-152">Berücksichtigen Sie beim Entwerfen von Lösungen diese Bereiche im Zusammenhang mit der Einstellung NoScript:</span><span class="sxs-lookup"><span data-stu-id="82a4c-152">When you design your solutions, consider these key areas related to the NoScript setting:</span></span>

- <span data-ttu-id="82a4c-153">Sandkastenlösungen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="82a4c-153">Sandbox solutions are not supported.</span></span>
- <span data-ttu-id="82a4c-154">Benutzerdefiniertes JavaScript kann nicht auf den Websites mithilfe von "klassische" Erweiterbarkeitsoptionen (beispielsweise über benutzerdefinierte Benutzeraktionen) aktiviert werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-154">Custom JavaScript cannot be enabled on the sites by using "classic" extensibility options (for example, via user custom actions).</span></span>
- <span data-ttu-id="82a4c-155">Sie können nicht mithilfe von SharePoint Designer Websites zugreifen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-155">You cannot access sites using SharePoint Designer.</span></span>
- <span data-ttu-id="82a4c-156">Einige Webparts sind nicht verfügbar für Endbenutzer.</span><span class="sxs-lookup"><span data-stu-id="82a4c-156">Some web parts are not available for end users.</span></span>
- <span data-ttu-id="82a4c-157">Die Möglichkeit, Access oder Update-Website-Eigenschaft Eigenschaftensammlung Einträge.</span><span class="sxs-lookup"><span data-stu-id="82a4c-157">Ability to access or update site property bag entries.</span></span>

> [!NOTE]
> <span data-ttu-id="82a4c-158">Sie können die vollständige Liste der betroffene Funktionen aus dem Microsoft Support-Artikel suchen [Zulassen oder verhindern, dass benutzerdefinierte Skripts](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US) klicken Sie im Abschnitt "Features betroffen, wenn benutzerdefinierte Skripts blockiert wird".</span><span class="sxs-lookup"><span data-stu-id="82a4c-158">You can find the full list of impacted capabilities from the Microsoft Support article [Allow or prevent custom script](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US) under the "Features affected when custom script is blocked" section.</span></span>

<span data-ttu-id="82a4c-159"><a name="pnpprovisioningengine"> </a></span><span class="sxs-lookup"><span data-stu-id="82a4c-159"></span></span>
### <a name="using-pnp-provisioning-engine-with-modern-team-sites"></a><span data-ttu-id="82a4c-160">Verwenden von Plug & Play-Bereitstellung Engine mit "modernen" Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="82a4c-160">Using PnP provisioning engine with "modern" team sites</span></span>

<span data-ttu-id="82a4c-161">Sie können die [Plug & Play-Bereitstellung Engine](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) mit "modernen" Teamwebsites verwenden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-161">You can use the [PnP provisioning engine](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) with "modern" team sites.</span></span> <span data-ttu-id="82a4c-162">Das Plug & Play-Bereitstellung Modul erkennt automatisch auf, wenn eine Website eine "modernen" Teamwebsite ist und passt dieses Verhalten basierend auf den unterstützten Funktionen an.</span><span class="sxs-lookup"><span data-stu-id="82a4c-162">The PnP provisioning engine automatically detects if a site is a "modern" team site and adjusts its behavior based on the supported capabilities.</span></span> <span data-ttu-id="82a4c-163">Der Prozess entspricht genau der Verwendung der Plug & Play-Bereitstellung Engine mit "klassische" Websites, bei denen die Skriptfunktionen nicht deaktiviert werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-163">The process is exactly the same as using the PnP provisioning engine with "classic" sites where the scripting capabilities are not disabled.</span></span>

<span data-ttu-id="82a4c-164">Die folgenden Elemente werden ignoriert, wenn eine remote-Vorlage auf einer Teamwebsite "modernen" oder einer Website, die NoScript aktiviert hat angewendet wird:</span><span class="sxs-lookup"><span data-stu-id="82a4c-164">The following elements are ignored when a remote template is applied to a "modern" team site or a site that has NoScript enabled:</span></span>

- <span data-ttu-id="82a4c-165">Standortkonfiguration Auflistung **AuditLogTrimmingRetention** in der Überwachungsrichtlinien</span><span class="sxs-lookup"><span data-stu-id="82a4c-165">Site collection **AuditLogTrimmingRetention** configuration in the auditing settings</span></span>
- <span data-ttu-id="82a4c-166">Anwenden eines benutzerdefinierten Designs aus der Vorlage; aktuelle Implementierung hat eine Abhängigkeit zum Speichern von ein benutzerdefiniertes Design auf den Katalog, die nicht unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="82a4c-166">Applying a custom theme from the template; current implementation has a dependency on storing a custom theme to the catalog, which is not supported</span></span>
- <span data-ttu-id="82a4c-167">Formular Einstellungen für Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="82a4c-167">Form settings for content types</span></span>
- <span data-ttu-id="82a4c-168">Hinzufügen von benutzerdefinierten Aktionen zu Websites, Web oder Listenebene</span><span class="sxs-lookup"><span data-stu-id="82a4c-168">Adding custom user actions to site, web, or list level</span></span>
- <span data-ttu-id="82a4c-169">Hinzufügen von Dateien mit Dateitypen der "asmx", "aspx", "aspx", ".htc", "JAR-", "Master", "SWF", "XAP", "xsf"</span><span class="sxs-lookup"><span data-stu-id="82a4c-169">Adding files with file types of ".asmx", ".ascx", ".aspx", ".htc", ".jar", ".master", ".swf", ".xap", ".xsf"</span></span>
- <span data-ttu-id="82a4c-170">Hinzufügen von Dateien zu Bibliotheken mit den folgenden Urls `"_catalogs/theme"`, `"style library"`, `"_catalogs/lt"`,`"_catalogs/wp"`</span><span class="sxs-lookup"><span data-stu-id="82a4c-170">Adding files to libraries with the following urls `"_catalogs/theme"`, `"style library"`, `"_catalogs/lt"`, `"_catalogs/wp"`</span></span>
- <span data-ttu-id="82a4c-171">Hinzufügen von Webparts zu Seiten der Website</span><span class="sxs-lookup"><span data-stu-id="82a4c-171">Adding web parts to site pages</span></span>
- <span data-ttu-id="82a4c-172">Speichern von Vorlage Bereitstellungsinformationen der Eigenschaftensammlung der bereitgestellten Website</span><span class="sxs-lookup"><span data-stu-id="82a4c-172">Storing provisioning template information to the property bag of the provisioned site</span></span>
- <span data-ttu-id="82a4c-173">Hinzufügen oder Aktualisieren der Eigenschaftensammlung der Website-Eigenschaftensammlung</span><span class="sxs-lookup"><span data-stu-id="82a4c-173">Adding or updating property bag entries to the site property bag</span></span>
- <span data-ttu-id="82a4c-174">"Klassische" Veröffentlichen von Einstellungen und Objekte</span><span class="sxs-lookup"><span data-stu-id="82a4c-174">"Classic" publishing settings and assets</span></span>
- <span data-ttu-id="82a4c-175">Website keine Einstellungen für die Durchforstung</span><span class="sxs-lookup"><span data-stu-id="82a4c-175">Site No Crawl settings</span></span>
- <span data-ttu-id="82a4c-176">Einstellungen für die Website-Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="82a4c-176">Site master page settings</span></span>

## <a name="apply-a-custom-theme-to-a-modern-team-site"></a><span data-ttu-id="82a4c-177">Anwenden eines benutzerdefinierten Designs auf einer Teamwebsite "modern"</span><span class="sxs-lookup"><span data-stu-id="82a4c-177">Apply a custom theme to a "modern" team site</span></span>

<span data-ttu-id="82a4c-178">"Modernen" Teamwebsites unterstützen benutzerdefinierte Designs, auch wenn Sie einen neuen Katalog-Eintrag für Endbenutzer Hochladen ist nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="82a4c-178">"Modern" team sites support custom themes even though you cannot upload a new gallery entry for end users.</span></span> <span data-ttu-id="82a4c-179">Dies kann durch Hochladen der benötigten Objekte in der Website, und klicken Sie dann ausführen **ApplyTheme** -Methode erreicht werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-179">This can be achieved by uploading the needed assets to the site and then executing the **ApplyTheme** method.</span></span> <span data-ttu-id="82a4c-180">Das folgende PowerShell-Skript zeigt, wie dies für eine Teamwebsite "modernen" ausführen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-180">The following PowerShell script shows how to perform this for a "modern" team site.</span></span>

```PowerShell

# Connect to a previously created Modern Site
$cred = Get-Credential
Connect-PnPOnline https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Apply a custom theme to a Modern Site

# First, upload the theme assets
Add-PnPFile -Path .\sppnp.spcolor -Folder SiteAssets
Add-PnPFile -Path .\sppnp-bg.png -Folder SiteAssets

# Second, apply the theme assets to the site
$web = Get-PnPWeb
$palette = $web.ServerRelativeUrl + "/SiteAssets/sppnp.spcolor"
$background = $web.ServerRelativeUrl + "/SiteAssets/sppnp-bg.png"

# We use OOTB CSOM operation for this
$web.ApplyTheme($palette, [NullString]::Value, $background, $true)
$web.Update()
# Set timeout as high as possible and execute
$web.Context.RequestTimeout = [System.Threading.Timeout]::Infinite
$web.Context.ExecuteQuery()

```

<br/>

<span data-ttu-id="82a4c-181">*Abbildung 1. "Modernen" Teamwebsite mit benutzerdefinierten Designs*</span><span class="sxs-lookup"><span data-stu-id="82a4c-181">*Figure 1. "Modern" team site with custom theme*</span></span>

!["Modernen" Teamwebsite mit benutzerdefinierten Designs](media/modern-experiences/modern-site-with-custom-theme.png)

> [!NOTE]
> - <span data-ttu-id="82a4c-183">Sie können das [Tool für SharePoint Farbe Palette](https://www.microsoft.com/en-us/download/details.aspx?id=38182) zum Erstellen einer benutzerdefinierten Designs-Datei (.spcolor) mit der Definition von benutzerdefinierten Farbe verwenden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-183">You can use the [SharePoint Color Palette Tool](https://www.microsoft.com/en-us/download/details.aspx?id=38182) to create a custom theme file (.spcolor) with the custom color definition.</span></span> <span data-ttu-id="82a4c-184">Versuchen Sie im Allgemeinen "modernen" Teamwebsites, das Verhalten des Designs durch die Umwandlung der "klassischen" Designoberfläche Websiteelemente automatisch auf der Seite "modernen" beibehalten.</span><span class="sxs-lookup"><span data-stu-id="82a4c-184">In general, "modern" team sites try to preserve the feel of the theme by automatically converting "classic" site theming elements to the "modern" side.</span></span> <span data-ttu-id="82a4c-185">Beibehaltene Bereichen sind Hintergrundbild und die folgenden Design Steckplätze: ContentAccent1 PageBackground und BackgroundOverlay.</span><span class="sxs-lookup"><span data-stu-id="82a4c-185">Preserved areas are background image and the following theme slots: ContentAccent1, PageBackground, and BackgroundOverlay.</span></span>
> - <span data-ttu-id="82a4c-186">Sie können das Logo der Teamwebsite "modernen" ändern, indem die Gruppen Diagramm-API wie von der SharePoint- [Plug & Play-UpdateUnifiedGroup-Methode](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs#L350).</span><span class="sxs-lookup"><span data-stu-id="82a4c-186">You can change the logo of "modern" team site by using the Groups Graph API as shown by the SharePoint [PnP UpdateUnifiedGroup method](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs#L350).</span></span>
> - <span data-ttu-id="82a4c-187">Anwenden eines benutzerdefinierten Designs auf einer Teamwebsite "modernen" kann zu Timeouts führen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-187">Applying a custom theme to a "modern" team site can cause timeouts.</span></span> <span data-ttu-id="82a4c-188">Die Lösung für dieses besteht darin, alle verfügbaren [Benutzeroberflächensprachen](https://support.office.com/en-us/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) für die Website vor dem Anwenden des Designs deaktivieren und anschließend wieder aktivieren.</span><span class="sxs-lookup"><span data-stu-id="82a4c-188">The resolution for this is to turn off all available [user interface languages](https://support.office.com/en-us/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) for the site before applying the theme, and turn them back on afterwards.</span></span>

## <a name="determine-if-a-site-is-a-modern-team-site"></a><span data-ttu-id="82a4c-189">Bestimmen Sie, ob eine Website einer Teamwebsite "moderne" ist</span><span class="sxs-lookup"><span data-stu-id="82a4c-189">Determine if a site is a "modern" team site</span></span>

<span data-ttu-id="82a4c-190">Sie können erkennen, dass eine Website einer Teamwebsite "modernen" wird durch den Wert "Web.WebTemplate" der Website überprüfen.</span><span class="sxs-lookup"><span data-stu-id="82a4c-190">You can detect that a site is a "modern" team site by checking the 'Web.WebTemplate' value of the site.</span></span> <span data-ttu-id="82a4c-191">"Modernen" Teamwebsites verwenden Sie die Vorlage "GROUP".</span><span class="sxs-lookup"><span data-stu-id="82a4c-191">"Modern" team sites use the "GROUP" template.</span></span> <span data-ttu-id="82a4c-192">Da die unterstützten Funktionen für eine "klassische" Teamwebsite identisch, sind Wenn das scripting deaktiviert ist, Sie sollten beide Einstellungen im Code zu bestimmen, das rechte-Verhalten überprüfen oder Funktionen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="82a4c-192">Because the supported capabilities are the same for a "classic" team site when the scripting is disabled, you should be checking both settings in your code to determine the right behavior or supported capabilities.</span></span>

<span data-ttu-id="82a4c-193">Da keine direkte Eigenschaft zu überprüfen, ob die scripting oder nicht aktiviert ist vorhanden ist, können Sie Berechtigungen verwenden, um den aktuellen Status zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="82a4c-193">Because there's no direct property to check if the scripting is enabled or not, you can use permissions to determine the current status.</span></span> <span data-ttu-id="82a4c-194">Wenn scripting aktiviert ist, ist gibt es keine AddAndCustomizePages Berechtigung in die Basisberechtigungen der Website.</span><span class="sxs-lookup"><span data-stu-id="82a4c-194">When scripting is enabled, there's no AddAndCustomizePages permission in the base permissions of the site.</span></span>

```C#
/// <summary>
/// Can be used to check if site has noscript enabled.
/// </summary>
/// <param name="web">site object to inspect</param>
/// <returns>True if no scripting is enabled, False if it's not</returns>
public static bool IsNoScriptSite(Web web)
{
    // Ensure that we have the needed properties - Notice that these are 
    // PnP CSOM extension capabilities
    web.EnsureProperties(w => w.WebTemplate, w => w.EffectiveBasePermissions);

    // Definition of no-script is not having the AddAndCustomizePages permission
    if (!web.EffectiveBasePermissions.Has(PermissionKind.AddAndCustomizePages))
    {
        return true;
    }

    // It's a site without noscript enabled
    return false;
}
```

## <a name="additional-considerations"></a><span data-ttu-id="82a4c-195">Zusätzliche Überlegungen</span><span class="sxs-lookup"><span data-stu-id="82a4c-195">Additional considerations</span></span>

<span data-ttu-id="82a4c-196">Wir werden schrittweise weitere Anpassungsoptionen für "modernen" Teamwebsites einzuführen, die mit der Veröffentlichung von SharePoint-Framework Zusatzfunktionen ausgerichtet wird.</span><span class="sxs-lookup"><span data-stu-id="82a4c-196">We'll gradually introduce more customization options for "modern" team sites that will be aligned with the release of additional SharePoint Framework capabilities.</span></span> <span data-ttu-id="82a4c-197">Derzeit ist kein genauen Zeitplan verfügbar, aber wir werden in den Artikeln "modernen" Erfahrung aktualisieren, sobald neue Funktionen freigegeben werden.</span><span class="sxs-lookup"><span data-stu-id="82a4c-197">Currently there is no exact schedule available, but we'll update the "modern" experience articles whenever new capabilities are released.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82a4c-198">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="82a4c-198">Additional resources</span></span>

- [<span data-ttu-id="82a4c-199">Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="82a4c-199">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="82a4c-200">Plug & Play-Remote-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="82a4c-200">PnP Remote Provisioning</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/pnp-remote-provisioning)

