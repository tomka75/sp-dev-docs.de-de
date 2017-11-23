---
title: "Aktualisieren von Anpassungen für SharePoint-Websites"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4b515860-69ae-4af8-8013-cd071c0ddca6
ms.openlocfilehash: e2a4c4a29aa71f4a3f1673669ae3dc6ca2795f5e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="upgrade-site-customizations-for-sharepoint"></a><span data-ttu-id="b3ffd-102">Aktualisieren von Anpassungen für SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="b3ffd-102">Upgrade site customizations for SharePoint</span></span>
<span data-ttu-id="b3ffd-p101">Informationen zu potenziellen Problemen und Empfehlungen für das Upgrade Ihrer SharePoint 2010 websiteanpassungen auf SharePoint abrufen. SharePoint führt wurden keine bedeutende Änderungen in der Benutzeroberfläche (UI), mit die Sie Websites mithilfe von schneller und flexiblere Komponenten anpassen kann. Aber wenn Sie von SharePoint 2010 aktualisieren, treten möglicherweise einige Probleme mit den neuen Komponenten, die in SharePoint zum Verarbeiten der Verbesserungen der Benutzeroberfläche erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p101">Learn about potential issues and get recommendations for upgrading your SharePoint 2010 site customizations to SharePoint. SharePoint introduces significant changes to the user interface (UI) that let you customize sites using faster, more agile components. But when you upgrade from SharePoint 2010, you might encounter some issues with the new components that have been built into SharePoint to handle the improvements to the UI.</span></span>
  
    
    

<span data-ttu-id="b3ffd-106">Dieser Artikel hilft SharePoint-Entwickler und die Verantwortlichen für die Verwaltung des Upgradeprozesses von SharePoint 2010 zur Identifizierung potenzieller Probleme nach dem Upgrade.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-106">This article will help SharePoint developers and those responsible for administering the upgrade process from SharePoint 2010 to identify potential problems after upgrading.</span></span>
## <a name="general-recommendations-for-upgrading"></a><span data-ttu-id="b3ffd-107">Allgemeine Empfehlungen für das Upgrade</span><span class="sxs-lookup"><span data-stu-id="b3ffd-107">General recommendations for upgrading</span></span>

<span data-ttu-id="b3ffd-p102">Im Allgemeinen wird empfohlen, dass Sie eine neue "Test" Website erstellen, können Sie Ihre Anpassungen testen und sie für eine Umgebung SharePoint Umgestalten. Weitere Informationen zum Erstellen einer auswertungswebsitesammlung finden Sie unter  [Upgrade einer Websitesammlung](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491).</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p102">In general, we recommend that you create a new "evaluation" site where you can test your customizations and redesign them for a SharePoint environment. For more information about creating an evaluation site collection, see  [Upgrade a site collection](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491).</span></span>
  
    
    

### <a name="upgrading-custom-components"></a><span data-ttu-id="b3ffd-110">Aktualisieren von benutzerdefinierten Komponenten</span><span class="sxs-lookup"><span data-stu-id="b3ffd-110">Upgrading custom components</span></span>

<span data-ttu-id="b3ffd-111">Tabelle 1 werden die möglichen Vorgängen Upgrade Probleme für benutzerdefinierte Komponenten und Informationen zu deren Behebung aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-111">Table 1 lists the possible after-upgrade problems for custom components and information about how to address them.</span></span>
  
    
    

<span data-ttu-id="b3ffd-112">**In Tabelle 1. Durchführen eines Upgrades auf SharePoint auswirkt benutzerdefinierten Komponenten**</span><span class="sxs-lookup"><span data-stu-id="b3ffd-112">**Table 1. Custom components affected by upgrading to SharePoint**</span></span>


|<span data-ttu-id="b3ffd-113">**Wenn Sie angepasst haben**</span><span class="sxs-lookup"><span data-stu-id="b3ffd-113">**If you have customized**</span></span>|<span data-ttu-id="b3ffd-114">**Auftreten können**</span><span class="sxs-lookup"><span data-stu-id="b3ffd-114">**You might encounter**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b3ffd-115">CSS-Formate</span><span class="sxs-lookup"><span data-stu-id="b3ffd-115">CSS styles</span></span>  <br/> |<span data-ttu-id="b3ffd-p103">Während des Upgrades wird Ihre Website auf die CSS-Dateien in die Seite default.master genannten zurückgesetzt. Daher ändert sich Anpassungen, die Sie an die Darstellung der Seiten vorgenommen haben, und Seiten mit der Standardarten gefunden in einer Standardinstallation rendert.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p103">During upgrade, your site will revert to the CSS files referred to in the default.master page. As a result, any customizations you have made to the appearance of your pages will change, and pages will render with the default styles found in a default installation.</span></span>  <br/> |
|<span data-ttu-id="b3ffd-118">Designs</span><span class="sxs-lookup"><span data-stu-id="b3ffd-118">Themes</span></span>  <br/> |<span data-ttu-id="b3ffd-p104">Für SharePoint 2010 können Sie benutzerdefinierte Designs erstellt haben, die eine corporate branding für eine vollständige Website definieren. Sie erstellen diese als thmx-Dateien, die in der Websitesammlung hochgeladen und vom Administrator angewendet werden können.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p104">For SharePoint 2010, you may have created custom themes that define a corporate branding for an entire site. You create these as .thmx files that can be uploaded to the site collection and applied by the administrator.</span></span>  <br/> <span data-ttu-id="b3ffd-p105">In SharePoint wurde die Designmodul vollständig flexibler und leistungsfähiger sein und für zukünftige Updates einfacher bereitstellen überarbeitet. Als Ergebnis dieser Umgestalten Aktualisieren von SharePoint 2010 auf SharePoint Designs wird nicht unterstützt und erfordert, dass Sie diese SharePoint neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p105">In SharePoint, the theming engine has been completely redesigned to be more flexible and powerful and to provide for easier future upgrades. As a result of this redesign, upgrading from SharePoint 2010 to SharePoint themes is not supported and will require you to re-create them for SharePoint.</span></span>  <br/> |
|<span data-ttu-id="b3ffd-123">Webvorlagen</span><span class="sxs-lookup"><span data-stu-id="b3ffd-123">Web templates</span></span>  <br/> |<span data-ttu-id="b3ffd-p106">Webvorlagen wurden in SharePoint 2010 zu bieten die Möglichkeit, Paket Features, Layouts, Stile und anderer Komponenten, die Sie dann verwenden können, erstellen Sie neue Webs eingeführt. Sie sind ähnlich wie in Funktion, die beim Erstellen von Websitedefinitionen, aber mit Webvorlagen, können Sie Veröffentlichungsfeatures hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p106">Web templates were introduced in SharePoint 2010 to provide a way to package features, layouts, styles, and other components that you can then use to create new webs. They are similar in function to creating site definitions, but with web templates, you can add publishing features.  </span></span><br/> <span data-ttu-id="b3ffd-126">Aufgrund der Änderungen in SharePoint funktionieren Ihre benutzerdefinierte Webvorlagen nicht unmittelbar nach dem Upgrade.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-126">Due to the changes made in SharePoint, your customized web templates will not work immediately after upgrade.</span></span>  <br/> <span data-ttu-id="b3ffd-127">Um festzustellen, welche Änderungen an Webvorlagen vorgenommen wurden und dadurch Probleme zu beheben, finden Sie unter  [Aktualisieren von Vorlagen für SharePoint](upgrade-web-templates-for-sharepoint.md) Empfehlungen und bewährte Methoden.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-127">To see what changes have been made to web templates and to fix issues resulting from this, see  [Upgrade web templates for SharePoint](upgrade-web-templates-for-sharepoint.md) for recommendations and best practices.</span></span> <br/> |
|<span data-ttu-id="b3ffd-128">Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="b3ffd-128">Master pages</span></span>  <br/> |<span data-ttu-id="b3ffd-p107">Während des Upgrades werden alle Verweise auf benutzerdefinierte Masterseiten, die Sie erstellt haben, wieder auf der Seite default.master zurückgesetzt. Dies kann Fehler aufgrund von Verweisen auf die benutzerdefinierten Seite auf fehlenden Komponenten in SharePoint führen.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-p107">During upgrade, any references to custom master pages you have created are reverted back to the default.master page. This may cause errors in SharePoint due to references on the custom page to missing components.</span></span>  <br/> <span data-ttu-id="b3ffd-131">Um dieses Problem zu beheben, müssen Sie die Verweise auf alle benutzerdefinierten Gestaltungsvorlagen ändern.</span><span class="sxs-lookup"><span data-stu-id="b3ffd-131">To fix this, you have to change the references to any custom master pages.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="b3ffd-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b3ffd-132">Additional resources</span></span>
<span data-ttu-id="b3ffd-133"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b3ffd-133"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b3ffd-134">Planen eines Upgrades eine Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="b3ffd-134">Plan to upgrade a site collection</span></span>](https://technet.microsoft.com/de-de/library/ff191199.aspx)
    
  
-  [<span data-ttu-id="b3ffd-135">Branding-Probleme, die beim Upgrade auf SharePoint auftreten können</span><span class="sxs-lookup"><span data-stu-id="b3ffd-135">Branding issues that may occur when upgrading to SharePoint</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/branding-issues-that-may-occur-when-upgrading-to-sharepoint-HA104052656.aspx?CTT=5&amp;origin=HA104034491)
    
  
-  [<span data-ttu-id="b3ffd-136">Upgrade einer Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="b3ffd-136">Upgrade a site collection</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491)
    
  
-  [<span data-ttu-id="b3ffd-137">Upgrade von Websitesammlungen Troubleshoot Probleme</span><span class="sxs-lookup"><span data-stu-id="b3ffd-137">Troubleshoot site collection upgrade issues</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/troubleshoot-site-collection-upgrade-issues-HA104037311.aspx?CTT=5&amp;origin=HA104034491)
    
  

