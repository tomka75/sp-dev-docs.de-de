---
title: Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8d1a4e3a-ae6f-41a5-bd80-3398ba541207
ms.openlocfilehash: d0e4096ec6f79eb75a9ff386e0f66a88c234d7ad
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="upgrade-custom-themes-and-css-to-sharepoint"></a><span data-ttu-id="a426a-102">Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-102">Upgrade custom themes and CSS to SharePoint</span></span>
<span data-ttu-id="a426a-103">Informationen zu Problemen beim Upgrade von Designanpassungen, z. B. benutzerdefinierten CSS-Dateien und benutzerdefinierten Gestaltungsvorlagen, und zum Aktualisieren von Anpassungen für die Verwendung in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a426a-103">Learn about upgrade issues with themes customizations, such as custom CSS and custom master pages, and how to update customizations to work in SharePoint.</span></span>
## <a name="introduction-to-themes-customizations-and-upgraded-sharepoint-sites"></a><span data-ttu-id="a426a-104">Einführung in Designanpassungen und aktualisierte SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="a426a-104">Introduction to themes customizations and upgraded SharePoint sites</span></span>
<span data-ttu-id="a426a-105"><a name="Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="a426a-105"><a name="Intro"> </a></span></span>

<span data-ttu-id="a426a-p101">Die Designerfahrung in SharePoint wurde neu gestaltet, um den Anpassungsvorgang von Websites durch Änderung des Websitelayouts, der Farbpalette, des Schriftartschemas und des Hintergrundbilds zu vereinfachen. Die Design-Benutzeroberfläche wurde neu gestaltet und enthält nun eine Reihe neuer Dateiformate, die im Zusammenhang mit Designs stehen. Benutzerdefinierte Designs, die in SharePoint 2010 erstellt wurden, können auf SharePoint-Websites nicht verwendet werden. Sie müssen diese neu erstellen. Benutzerdefinierte CSS-Dateien auf SharePoint-Websites müssen möglicherweise aktualisiert werden, damit Sie für neue Gestaltungsvorlagen, Farbmodule und andere Designänderungen verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="a426a-p101">The theming experience in SharePoint was redesigned to simplify the process of customizing sites by changing the site layout, color palette, font scheme, and background image. The themes user interface was redesigned and there is a set of new file formats related to themes. Custom themes that were created in SharePoint 2010 cannot be used on SharePoint sites, you must re-create them. Custom CSS files may not work successfully on SharePoint sites until after they are updated to work with the new master pages, color slots, and other theming changes.</span></span>
  
    
    
<span data-ttu-id="a426a-p102">Dieser Artikel beschreibt die Probleme, die beim Verwenden benutzerdefinierter SharePoint 2010-Designs, SharePoint 2010 CSS-Dateien und benutzerdefinierter CSS-Dateien mit der neuen Designerfahrung auftreten können. Darüber hinaus werden Änderungen erläutert, die Sie an Ihren benutzerdefinierten SharePoint 2010-Designs, SharePoint 2010 CSS-Dateien und benutzerdefinierten CSS-Dateien vornehmen müssen, um sie auf SharePoint-Websites zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a426a-p102">This article describes the issues that may occur when you try to use custom SharePoint 2010 themes, SharePoint 2010 CSS, and custom CSS with the new theming experience. It also explains the changes you have to make to your custom SharePoint 2010 themes, SharePoint 2010 CSS, and custom CSS if you want to use them in SharePoint sites.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="a426a-112">SharePoint 2010-Designs können auf Websitesammlungen angewendet werden, die im 2010-Modus ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a426a-112">Note: SharePoint 2010 themes can be used on site collections that are running in 2010 mode.</span></span> <span data-ttu-id="a426a-113">Weitere Informationen zu Websitesammlungsmodi finden Sie unter [Planen von Websitesammlungsupgrades in SharePoint]((http://technet.microsoft.com/de-DE/library/ff191199.aspx)) oder unter [Planen des Upgrades auf SharePoint]((https://technet.microsoft.com/de-DE/library/cc303429.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a426a-113">For more information about site collection modes, see  [Plan for site collection upgrades in SharePoint]((http://technet.microsoft.com/de-DE/library/ff191199.aspx)) or [Plan for upgrade to SharePoint]((https://technet.microsoft.com/de-DE/library/cc303429.aspx)).</span></span> 
  
    
    

<span data-ttu-id="a426a-114">Weitere Informationen zu Designs finden Sie unter [Themes overview for SharePoint](themes-overview-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a426a-114">For more information about themes, see  [Themes overview for SharePoint](themes-overview-for-sharepoint.md).</span></span>
  
    
    

## <a name="custom-sharepoint-2010-themes-in-sharepoint"></a><span data-ttu-id="a426a-115">Benutzerdefinierte SharePoint 2010-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-115">Custom SharePoint 2010 themes in SharePoint</span></span>
<span data-ttu-id="a426a-116"><a name="themes"> </a></span><span class="sxs-lookup"><span data-stu-id="a426a-116"><a name="themes"> </a></span></span>

<span data-ttu-id="a426a-p104">Designs wurden in SharePoint 2010 als THMX-Dateien gespeichert. In SharePoint, gibt es im Zusammenhang mit Designs eine Reihe neuer Dateiformate. Farbpaletten und Schriftartschemas werden in separaten XML-Dateien gespeichert (SPCOLOR- und SPFONT-Dateien).</span><span class="sxs-lookup"><span data-stu-id="a426a-p104">In SharePoint 2010, themes were stored in THMX files. In SharePoint, there is a set of new file formats related to themes. Color palettes and font schemes are stored in separate XML files (.spcolor and .spfont files, respectively).</span></span> 
  
    
    
<span data-ttu-id="a426a-p105">Sie können kein Upgrade einer THMX-Datei von SharePoint 2010 auf SharePoint durchführen. Wenn Sie ein benutzerdefiniertes Design auf Ihre SharePoint 2010-Website angewendet haben, bleiben beim Upgrade auf SharePoint, die Designdateien erhalten, das Design wird jedoch nicht mehr auf die Website angewendet und die Website wird auf das Standarddesign zurückgesetzt. Wenn Sie Ihre SharePoint 2010-Designanpassungen auf SharePoint-Websites verwenden möchten, müssen Sie sie mithilfe der Anleitung zur SharePoint-Designerstellung neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a426a-p105">You cannot upgrade a THMX file from SharePoint 2010 to SharePoint. If you applied a custom theme to your SharePoint 2010 site, when you upgrade to SharePoint, the theme files remain in place, but the theme is no longer applied to the site, and the site reverts to the default theme. If you want to use your SharePoint 2010 themes customizations on SharePoint sites, you must re-create them using the SharePoint theming guidance.</span></span>
  
    
    
<span data-ttu-id="a426a-p106">Weitere Informationen zum Erstellen von Designanpassungen finden Sie unter  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) und [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md). Sie können auch das SharePoint-Farbpalettentool zum Erstellen von SharePoint-Designs verwenden. Sie können  [das SharePoint-Farbpalettentool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) im Microsoft Download Center herunterladen.</span><span class="sxs-lookup"><span data-stu-id="a426a-p106">For more information about creating themes customizations, see  [How to: Deploy a custom theme in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) and [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md). You can also use the SharePoint color palette tool to help you create SharePoint designs. You can  [ download the SharePoint color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) from the Microsoft Download Center.</span></span>
  
    
    

> <span data-ttu-id="a426a-126">**Tipp:** Sie können THMX-Dateien in PowerPoint öffnen, um die Farbdefinitionen des benutzerdefinierten Designs zu sehen. Anschließend können Sie die Farben mithilfe des Farbpalettentools als Farbpalettendatei (.spcolor-Datei) kopieren.</span><span class="sxs-lookup"><span data-stu-id="a426a-126">**Tip:** You can open a THMX file in PowerPoint to see how the colors are defined in the custom theme and then use the color palette tool to re-create the colors as a color palette file (an .spcolor file).</span></span> <span data-ttu-id="a426a-127">Eine Farbpalette ist die Kombination aller Farben, die auf einer SharePoint-Website verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a426a-127">A color palette is the combination of colors that are used in a SharePoint site.</span></span> 
  
    
    

<span data-ttu-id="a426a-p108">Sie können auch eins der vorinstallierten der SharePoint-Designs verwenden. Weitere Informationen finden Sie unter  [Auswählen eines Designs für Ihre Veröffentlichungswebsite](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx?CTT=1) auf Office.com.</span><span class="sxs-lookup"><span data-stu-id="a426a-p108">You can also decide to use one of the preinstalled SharePoint themes. For more information, see  [Choose a theme for your publishing site](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx?CTT=1) on Office.com.</span></span>
  
    
    

## <a name="upgrading-customized-master-pages"></a><span data-ttu-id="a426a-130">Aktualisieren angepasster Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="a426a-130">Upgrading customized master pages</span></span>
<span data-ttu-id="a426a-131"><a name="MasterPages"> </a></span><span class="sxs-lookup"><span data-stu-id="a426a-131"><a name="MasterPages"> </a></span></span>

<span data-ttu-id="a426a-p109">Bei einem Upgrade einer SharePoint 2010-Website auf SharePoint wird die Website zum Verwenden der Standardgestaltungsvorlage für SharePoint konfiguriert. Wenn Sie eine benutzerdefinierte Gestaltungsvorlage für Ihre SharePoint 2010-Website verwendet haben, ist die weiterhin auf der Website vorhanden, und Sie können sie auf die SharePoint-Website anwenden. Sie können die SharePoint-Benutzeroberfläche oder die **SPWeb**-Klasse verwenden, um die benutzerdefinierte Gestaltungsvorlage auf die aktualisierte Website anzuwenden. Weitere Informationen zum Ändern von Gestaltungsvorlagen finden Sie unter  [Vorgehensweise: Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint](how-to-apply-a-master-page-to-a-site-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a426a-p109">When you upgrade a SharePoint 2010 site to SharePoint, the site is configured to use the default master page for SharePoint. If you had a custom master page for your SharePoint 2010 site, it still resides in the site and you can apply it to the SharePoint site. You can use the SharePoint user interface or the **SPWeb** class to apply the custom master page to the upgraded site. For more information about how to change the master page, see [How to: Apply a master page to a site in SharePoint](how-to-apply-a-master-page-to-a-site-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="a426a-136">Beachten Sie Folgendes, bevor Sie sich zum Anwenden der benutzerdefinierten SharePoint 2010Gestaltungsvorlage auf die aktualisierte SharePoint-Website entscheiden:</span><span class="sxs-lookup"><span data-stu-id="a426a-136">Consider the following before you decide whether to apply the SharePoint 2010 custom master page to the upgraded SharePoint site:</span></span>
  
    
    

- <span data-ttu-id="a426a-p110">**Wenn die benutzerdefinierte Gestaltungsvorlage von benutzerdefinierten CSS-Dateien abhängig ist:** Beim Anwenden der benutzerdefinierten Gestaltungsvorlage auf die aktualisierte Website, wird die Website auf das standardmäßige 2010-Design zurückgesetzt. Sie können jedoch ein SharePoint-Design auf die Website anwenden.</span><span class="sxs-lookup"><span data-stu-id="a426a-p110">**If the custom master page depends on custom CSS files:** Applying the custom master page to the upgraded site should return the site to its original 2010 experience. But, you will be unable to apply a SharePoint theme to the site.</span></span>
    
    <span data-ttu-id="a426a-p111">Wenn Sie die benutzerdefinierte Gestaltungsvorlage und die benutzerdefinierten CSS-Dateien mit der SharePoint-Designerfahrung verwenden möchten, müssen Sie die CSS-Dateien aktualisieren, um die neuen SharePoint-Farbmodule zu verwenden. Wenn Sie über die Design-Benutzeroberfläche auf die benutzerdefinierte Gestaltungsvorlage zugreifen möchten, müssen Sie auch eine Gestaltungsvorlagen-Vorschaudatei erstellen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="a426a-p111">If you want to use the custom master page and custom CSS files together with the SharePoint theming experience, you must update the CSS files to use the new SharePoint color slots. If you want to access the custom master page from the themes user interface, you also have to create a master page preview file. For more information, see  [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="a426a-p112">**Wenn die benutzerdefinierte Gestaltungsvorlage von SharePoint 2010-CSS-Dateien abhängig ist:** Die CSS-Dateien wurden in SharePoint im Vergleich zu SharePoint 2010 erheblich geändert. In vielen Fällen müssen Sie die Gestaltungsvorlage für die Verwendung mit den neuen Klassen überarbeiten, bevor Sie erfolgreich auf die aktualisierte Website angewendet werden kann. Weitere Informationen zu CSS-Klassen finden Sie im Abschnitt **Verwenden von Hostweb-CSS-Dateien in Apps für SharePoint** in den [Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint]((http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a426a-p112">**If the custom master page depends on SharePoint 2010 CSS files:** CSS files have changed significantly from SharePoint 2010 to SharePoint. In many cases, you will have to rework the master page so that it can work with new classes before you can successfully apply it to the upgraded site. For more information about CSS classes, see the **Using the host web CSS in apps for SharePoint** section in [SharePoint Add-ins UX design guidelines]((http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx)).</span></span>
    
  

## <a name="sharepoint-2010-css-and-custom-css-files"></a><span data-ttu-id="a426a-145">SharePoint 2010-CSS- und benutzerdefinierte CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="a426a-145">SharePoint 2010 CSS and custom CSS files</span></span>
<span data-ttu-id="a426a-146"><a name="CSS"> </a></span><span class="sxs-lookup"><span data-stu-id="a426a-146"><a name="CSS"> </a></span></span>

<span data-ttu-id="a426a-p113">Unveränderte SharePoint 2010-CSS-Dateien und benutzerdefinierte CSS-Dateien können auf SharePoint-Websites nicht verwendet werden. Im Folgenden werden die Änderungen in SharePoint beschrieben, die für SharePoint 2010-CSS- und benutzerdefinierte CSS-Dateien gelten:</span><span class="sxs-lookup"><span data-stu-id="a426a-p113">Unmodified SharePoint 2010 CSS files and custom CSS files cannot be used on SharePoint sites. The following describes SharePoint changes that apply to SharePoint 2010 CSS and custom CSS files:</span></span>
  
    
    

- <span data-ttu-id="a426a-p114">**Farbmodule**. Die Anzahl der verfügbaren Farbmodule wurde in SharePoint wesentlich erhöht. Sie müssen die Farbmodule in SharePoint 2010-CSS-Dateien aktualisieren, bevor sie in der neuen Designerfahrung verwendet werden können. Weitere Informationen finden Sie im Abschnitt  [Zuordnen von Farbplätzen](color-palettes-and-fonts-in-sharepoint.md#colorSlots) unter [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a426a-p114">**Color slots**. The number of available color slots has increased significantly in SharePoint. You must update the color slots in SharePoint 2010 CSS files before they can be used in the new theming experience. For more information, see the  [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="a426a-p115">**Schriftartmodule**. Sie sollten die Liste der verfügbaren Schriftartmodule prüfen und sicherstellen, dass die CSS-Dateien, die Sie in SharePoint verwenden möchten, die richtigen Schriftartmodule verwenden. Weitere Informationen finden Sie im Abschnitt  [Schriftartenplätze](color-palettes-and-fonts-in-sharepoint.md#fontSlot) unter [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a426a-p115">**Font slots**. You should review the list of available font slots and verify that the CSS files you want to use in SharePoint are using the correct font slots. For more information, see the  [Font slots](color-palettes-and-fonts-in-sharepoint.md#fontSlot) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="a426a-p116">**Neue Anmerkung**. SharePoint verfügt über eine neue Anmerkung, mit der Sie das Hintergrundbild ersetzen können. Weitere Informationen finden Sie unter  [Gewusst wie: Benutzerdefinierte CSS-Dateien in SharePoint designfähig gestalten](how-to-make-custom-css-files-themable-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a426a-p116">**New annotation**. SharePoint has a new annotation that lets you replace the background image. For more information, see  [How to: Make custom CSS files themable in SharePoint](how-to-make-custom-css-files-themable-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="a426a-p117">**Neue Klassen**. Möglicherweise müssen Sie die CSS-Dateien für die Verwendung mit den neuen Klassen in SharePoint aktualisieren. Weitere Informationen zu CSS-Klassen (auch CSS-Formatvorlagen genannt) finden Sie im Abschnitt **Verwenden von Hostweb-CSS-Dateien in Apps für SharePoint** in den [Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint]((http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a426a-p117">**New classes**. You may have to update CSS files to work with the new classes in SharePoint. For more information about CSS classes (also referred to as CSS styles), see the **Using the host web CSS in apps for SharePoint** section in [SharePoint Add-ins UX design guidelines]((http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx)).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="a426a-162">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a426a-162">See also</span></span>
<span data-ttu-id="a426a-163"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a426a-163"><a name="addresources"> </a></span></span>


-  [<span data-ttu-id="a426a-164">Übersicht über Designs für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-164">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a426a-165">Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-165">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a426a-166">Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-166">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a426a-167">Farbpaletten und Schriftarten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a426a-167">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  <span data-ttu-id="a426a-168">[SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs]((http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx))</span><span class="sxs-lookup"><span data-stu-id="a426a-168">[SharePoint Team Blog: Show off your style with SharePoint theming]((http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx))</span></span>
    
  
-  [<span data-ttu-id="a426a-169">SharePoint Design Manager - Branding- und Designfunktionen</span><span class="sxs-lookup"><span data-stu-id="a426a-169">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

