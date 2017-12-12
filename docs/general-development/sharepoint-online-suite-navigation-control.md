---
title: Navigationssteuerelement SharePoint Online-Suite
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ba93e5c0-e591-48d0-a716-a08ec7ef6cea
ms.openlocfilehash: 531253b34f59c05693cef0c7905e48de0b5c2c89
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-online-suite-navigation-control"></a><span data-ttu-id="a9e5d-102">Navigationssteuerelement SharePoint Online-Suite</span><span class="sxs-lookup"><span data-stu-id="a9e5d-102">SharePoint Online Suite Navigation control</span></span>
<span data-ttu-id="a9e5d-p101">Informationen Sie zu gestaltungsvorlagenmarkup für das Steuerelement Suitenavigation in SharePoint Online. {Einführung einfügen}</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p101">Learn about master page markup for the Suite Navigation control in SharePoint Online. {insert introductory content}</span></span>
  
    
    


## <a name="sharepoint-online-suite-navigation-control"></a><span data-ttu-id="a9e5d-105">Navigationssteuerelement SharePoint Online-Suite</span><span class="sxs-lookup"><span data-stu-id="a9e5d-105">SharePoint Online Suite Navigation control</span></span>

<span data-ttu-id="a9e5d-p102">Das Suite Navigationssteuerelement rendert eine konsistente oberen Navigationsleiste in SharePoint Online. Dieses Steuerelement ist nun ein Teil der nicht angepasste Out-of-Box Gestaltungsvorlagen.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p102">The Suite Navigation control renders a consistent top navigation bar in SharePoint Online. This control is now a part of all uncustomized out-of-the-box master pages.</span></span>
  
    
    
<span data-ttu-id="a9e5d-p103">Wenn eine Gestaltungsvorlage angepasst wurde, werden die neuen Suite Navigationssteuerelement nicht übernommen. Um dieses Steuerelement in Ihre benutzerdefinierte Gestaltungsvorlage hinzuzufügen, ersetzen Sie die  `suiteBar` `<div>` mit dem Markup, das den Typ der Website entspricht, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p103">If a master page was customized, it will not pick up the new Suite Navigation control. To add this control to your custom master page, replace the  `suiteBar` `<div>` with the markup that corresponds to the type of site you're using.</span></span>
  
    
    
<span data-ttu-id="a9e5d-p104">Das neue Suite Navigations-Steuerelement unterstützt auf der Website angewendete Design. Wenn Sie die Farbe der oberen Navigationsleiste ändern möchten, Anwenden eines Designs.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p104">The new Suite Navigation control supports any theme applied to the site. If you want to change the color of the top navigation bar, apply a theme.</span></span>
  
    
    

> <span data-ttu-id="a9e5d-112">**Wichtig:** Best Practice für die Anpassung von Websites ist die Verwendung eines Designs.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-112">**Important:** When customizing a site, the best practice is to apply a theme.</span></span> <span data-ttu-id="a9e5d-113">Zwar können Sie auf Ihre Website auch benutzerdefinierten CSS-Code anwenden; dann besteht jedoch das Risiko, dass der Code nach einer Aktualisierung des Suite Navigation-Steuerelements im Dienst nicht mehr funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-113">While you can apply custom CSS to the site, custom CSS may break in the future if the Suite Navigation control is updated again in the service.</span></span> 
  
    
    


> <span data-ttu-id="a9e5d-114">**Vorsicht:** Wenn Sie das neue Steuerelement nicht verwenden möchten, müssen Sie das Suite Navigation-Markup von Ihrer Masterseite entfernen und benutzerdefiniertes Markup einfügen.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-114">**Caution:** If you do not want to use the new control, remove the Suite Navigation markup from your master page and add custom markup.</span></span> <span data-ttu-id="a9e5d-115">Bedenken Sie dabei jedoch, dass angepasste Masterseiten Aktualisierungen an den Standardsteuerelementen für Masterseiten möglicherweise nicht übernehmen. Dasselbe gilt für neue Funktionen, die zu nicht angepassten Masterseiten hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-115">However, be aware that customized master pages run the risk of not picking up updates to default master page controls or new functionality that is added to uncustomized master pages.</span></span> <span data-ttu-id="a9e5d-116">Wenn Sie Ihre Masterseite anpassen, besteht das Risiko, dass Ihre Website nach einem Dienstupdate nicht mehr korrekt funktioniert oder nicht mehr wie gewünscht aussieht.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-116">Using a customized master page introduces the risk that service updates will break the functionality or style of your site.</span></span> 
  
    
    


### <a name="suite-navigation-control-for-intranet-sites"></a><span data-ttu-id="a9e5d-117">Suite Navigation-Steuerelement für Intranetwebsites</span><span class="sxs-lookup"><span data-stu-id="a9e5d-117">Suite Navigation control for intranet sites</span></span>

<span data-ttu-id="a9e5d-p107">Verwenden Sie das folgende Markup Gestaltungsvorlage für Intranetwebsites für die Suitenavigation-Steuerelement. Tabelle 1 enthält Websteuerelemente in der Suitenavigation Code verwendet.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p107">For intranet sites, use the following master page markup for the Suite Navigation control. Table 1 lists web controls used in the Suite Navigation code.</span></span>
  
    
    

<span data-ttu-id="a9e5d-120">**In Tabelle 1. Suite Navigation Websteuerelemente für Intranetwebsites**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-120">**Table 1. Suite Navigation web controls for intranet sites**</span></span>


|<span data-ttu-id="a9e5d-121">**Websteuerelement**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-121">**Web Control**</span></span>|<span data-ttu-id="a9e5d-122">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-122">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a9e5d-123">SharePoint:Menu</span><span class="sxs-lookup"><span data-stu-id="a9e5d-123">SharePoint:Menu</span></span>  <br/> |<span data-ttu-id="a9e5d-124">Zeigt ein Menü in einer ASP.NET-Webseite.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-124">Displays a menu in an ASP.NET web page.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-125">SharePoint:MenuItemTemplate</span><span class="sxs-lookup"><span data-stu-id="a9e5d-125">SharePoint:MenuItemTemplate</span></span>  <br/> |<span data-ttu-id="a9e5d-126">Stellt ein Steuerelement dar, das ein Element in einem Dropdownmenü erstellt.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-126">Represents a control that creates an item in a drop-down menu.</span></span>  <br/> |
   

```

<SharePoint:AjaxDelta runat="server" id="suiteBarDelta" BlockElement="true" CssClass="ms-dialogHidden ms-fullWidth noindex">
<div id="suiteMenuData" class="ms-hide">
<wssuc:Welcome id="IdWelcomeData" runat="server" EnableViewState="false" RenderDataOnly="true"/>
   <span class="ms-siteactions-root" id="siteactiontd">
   <SharePoint:SiteActions runat="server" accesskey="<%$Resources:wss,tb_SiteActions_AK%>"
id="SiteActionsMenuMainData"
PrefixHtml=""
SuffixHtml=""
ImageUrl="/_layouts/15/images/spcommon.png?rev=32"
ThemeKey="spcommon"
MenuAlignment="Right"
LargeIconMode="false"
>
<CustomTemplate>
<SharePoint:Menu runat="server" Visible="false"/>
<SharePoint:FeatureMenuTemplate runat="server"
FeatureScope="Site"
Location="Microsoft.SharePoint.StandardMenu"
GroupId="SiteActions"
UseShortId="true"
>
  <SharePoint:MenuItemTemplate runat="server"
  id="MenuItem_ShareThisSite"
  Text="<%$Resources:wss,siteactions_sharethissite%>"
  Description="<%$Resources:wss,siteactions_sharethissitedescription%>"
  MenuGroupId="100"
  Sequence="110"
  UseShortId="true"
  PermissionsString="ViewPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_EditPage"
  Text="<%$Resources:wss,siteactions_editpage15%>"
  Description="<%$Resources:wss,siteactions_editpagedescriptionv4%>"
  ImageUrl="/_layouts/15/images/ActionsEditPage.png?rev=32"
  MenuGroupId="200"
  Sequence="210"
  PermissionsString="EditListItems"
  ClientOnClickNavigateUrl="javascript:ChangeLayoutMode(false);" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_CreatePage"
  Text="<%$Resources:wss,siteactions_addpage15%>"
  Description="<%$Resources:wss,siteactions_createpagedesc%>"
  ImageUrl="/_layouts/15/images/NewContentPageHH.png?rev=32"
  MenuGroupId="200"
  Sequence="220"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="OpenCreateWebPageDialog('~siteLayouts/createwebpage.aspx')"
  PermissionsString="AddListItems, EditListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Create"
  Text="<%$Resources:wss,siteactions_addapp15%>"
  Description="<%$Resources:wss,siteactions_createdesc%>"
  MenuGroupId="200"
  Sequence="230"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/addanapp.aspx')"
  PermissionsString="ManageLists, ManageSubwebs"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ViewAllSiteContents"
  Text="<%$Resources:wss,quiklnch_allcontent_15%>"
  Description="<%$Resources:wss,siteactions_allcontentdescription%>"
  ImageUrl="/_layouts/15/images/allcontent32.png?rev=32"
  MenuGroupId="200"
  Sequence="240"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/viewlsts.aspx"
  PermissionsString="ViewFormPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ChangeTheLook"
  Text="<%$Resources:wss,siteactions_changethelook15%>"
  Description="<%$Resources:wss,siteactions_changethelookdesc15%>"
  MenuGroupId="300"
  Sequence="310"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/designgallery.aspx"
  PermissionsString="ApplyThemeAndBorder,ApplyStyleSheets,Open,ViewPages,OpenItems,ViewListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Settings"
  Text="<%$Resources:wss,siteactions_settings15%>"
  Description="<%$Resources:wss,siteactions_sitesettingsdescriptionv4%>"
  ImageUrl="/_layouts/15/images/settingsIcon.png?rev=32"
  MenuGroupId="300"
  Sequence="320"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/settings.aspx')"
  PermissionsString="EnumeratePermissions,ManageWeb,ManageSubwebs,AddAndCustomizePages,ApplyThemeAndBorder,ManageAlerts,ManageLists,ViewUsageData"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_SwitchToMobileView"
  Visible="false"
  Text="<%$Resources:wss,siteactions_switchtomobileview%>"
  Description="<%$Resources:wss,siteactions_switchtomobileviewdesc%>"
  MenuGroupId="300"
  Sequence="330"
  UseShortId="true"
  ClientOnClickScript="STSNavigate(StURLSetVar2(ajaxNavigate.get_href(), 'mobile', '1'));" />
</SharePoint:FeatureMenuTemplate>
</CustomTemplate>
  </SharePoint:SiteActions></span>
</div>
<SharePoint:ScriptBlock runat="server">
var g_navBarHelpDefaultKey = "HelpHome";
</SharePoint:ScriptBlock>
<SharePoint:DelegateControl id="ID_SuiteBarDelegate" ControlId="SuiteBarDelegate" runat="server" />
</SharePoint:AjaxDelta>
```


#### <a name="learning-about-suite-navigation-web-controls-for-public-facing-sites"></a><span data-ttu-id="a9e5d-127">Informationen zu Suitenavigation Websteuerelemente für öffentlich zugängliche Websites</span><span class="sxs-lookup"><span data-stu-id="a9e5d-127">Learning about Suite Navigation web controls for public-facing sites</span></span>

<span data-ttu-id="a9e5d-p108">Verwenden Sie das folgende Markup Gestaltungsvorlage für öffentlich zugängliche Websites für das Navigationssteuerelement Suite. Tabelle 2 sind die Websteuerelemente in der Suitenavigation Code verwendet.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p108">For public-facing sites, use the following master page markup for the Suite Navigation control. Table 2 lists web controls used in the Suite Navigation code.</span></span>
  
    
    

<span data-ttu-id="a9e5d-130">**In Tabelle 2. Suite Navigation Websteuerelemente für öffentlich zugängliche Websites**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-130">**Table 2. Suite Navigation web controls for public-facing sites**</span></span>


|<span data-ttu-id="a9e5d-131">**Websteuerelement**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-131">**Web Control**</span></span>|<span data-ttu-id="a9e5d-132">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a9e5d-132">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a9e5d-133">SharePoint:DelegateControl</span><span class="sxs-lookup"><span data-stu-id="a9e5d-133">SharePoint:DelegateControl</span></span>  <br/> |<span data-ttu-id="a9e5d-p109">Ein Websteuerelement ASP.NET rendert. Stellvertretungs-Steuerelemente stellen ihre Candidate Steuerelemente austauschbaren und nachverfolgbare.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-p109">Renders an ASP.NET web control. Delegate controls make their candidate controls pluggable and traceable.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-136">SharePoint:FeatureMenuTemplate</span><span class="sxs-lookup"><span data-stu-id="a9e5d-136">SharePoint:FeatureMenuTemplate</span></span>  <br/> |<span data-ttu-id="a9e5d-137">Stellt ein Steuerelement, das eine Vorlage für ein Dropdown Menü erstellt.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-137">Represents a control that creates a template for a drop-down menu.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-138">SharePoint:Menu</span><span class="sxs-lookup"><span data-stu-id="a9e5d-138">SharePoint:Menu</span></span>  <br/> |<span data-ttu-id="a9e5d-139">Zeigt ein Menü in einer ASP.NET-Webseite.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-139">Displays a menu in an ASP.NET web page.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-140">SharePoint:MenuItemTemplate</span><span class="sxs-lookup"><span data-stu-id="a9e5d-140">SharePoint:MenuItemTemplate</span></span>  <br/> |<span data-ttu-id="a9e5d-141">Stellt ein Steuerelement dar, das ein Element in einem Dropdownmenü erstellt.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-141">Represents a control that creates an item in a drop-down menu.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-142">SharePoint:ScriptBlock</span><span class="sxs-lookup"><span data-stu-id="a9e5d-142">SharePoint:ScriptBlock</span></span>  <br/> |<span data-ttu-id="a9e5d-143">Stellt ein Skript Block-Steuerelement auf einer Seite dar.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-143">Represents a script block control on a page.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-144">SharePoint:SiteActions</span><span class="sxs-lookup"><span data-stu-id="a9e5d-144">SharePoint:SiteActions</span></span>  <br/> |<span data-ttu-id="a9e5d-145">Stellt ein Vorlagensteuerelement für das Menü Websiteaktionen.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-145">Represents a template control for the Site Action menu.</span></span>  <br/> |
|<span data-ttu-id="a9e5d-146">SharePoint:SPSecurityTrimmedControl</span><span class="sxs-lookup"><span data-stu-id="a9e5d-146">SharePoint:SPSecurityTrimmedControl</span></span>  <br/> |<span data-ttu-id="a9e5d-147">Rendert bedingt den Inhalt des Steuerelements für dem aktuellen Benutzer nur, wenn der aktuelle Benutzer in der **PermissionString**definierte Berechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="a9e5d-147">Renders conditionally the contents of the control to the current user only if the current user has permissions defined in the **PermissionString**.</span></span>  <br/> |
   

### <a name="suite-navigation-control-for-public-facing-sites"></a><span data-ttu-id="a9e5d-148">Suite Navigationssteuerelement für öffentlich zugängliche Websites</span><span class="sxs-lookup"><span data-stu-id="a9e5d-148">Suite Navigation control for public-facing sites</span></span>


```

<SharePoint:AjaxDelta runat="server" id="suiteBarDelta" BlockElement="true" CssClass="ms-dialogHidden ms-fullWidth noindex">
  <SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AuthenticatedUsersOnly" EmitDiv="true">
<div id="suiteMenuData" class="ms-hide">
<wssuc:Welcome id="IdWelcomeData" runat="server" EnableViewState="false" RenderDataOnly="true"/>
   <span class="ms-siteactions-root" id="siteactiontd">
   <SharePoint:SiteActions runat="server" accesskey="<%$Resources:wss,tb_SiteActions_AK%>"
id="SiteActionsMenuMainData"
PrefixHtml=""
SuffixHtml=""
ImageUrl="/_layouts/15/images/spcommon.png?rev=32"
ThemeKey="spcommon"
MenuAlignment="Right"
LargeIconMode="false"
>
<CustomTemplate>
<SharePoint:Menu runat="server" Visible="false"/>
<SharePoint:FeatureMenuTemplate runat="server"
FeatureScope="Site"
Location="Microsoft.SharePoint.StandardMenu"
GroupId="SiteActions"
UseShortId="true"
>
  <SharePoint:MenuItemTemplate runat="server"
  id="MenuItem_ShareThisSite"
  Text="<%$Resources:wss,siteactions_sharethissite%>"
  Description="<%$Resources:wss,siteactions_sharethissitedescription%>"
  MenuGroupId="100"
  Sequence="110"
  UseShortId="true"
  PermissionsString="ViewPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_EditPage"
  Text="<%$Resources:wss,siteactions_editpage15%>"
  Description="<%$Resources:wss,siteactions_editpagedescriptionv4%>"
  ImageUrl="/_layouts/15/images/ActionsEditPage.png?rev=32"
  MenuGroupId="200"
  Sequence="210"
  PermissionsString="EditListItems"
  ClientOnClickNavigateUrl="javascript:ChangeLayoutMode(false);" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_CreatePage"
  Text="<%$Resources:wss,siteactions_addpage15%>"
  Description="<%$Resources:wss,siteactions_createpagedesc%>"
  ImageUrl="/_layouts/15/images/NewContentPageHH.png?rev=32"
  MenuGroupId="200"
  Sequence="220"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="OpenCreateWebPageDialog('~siteLayouts/createwebpage.aspx')"
  PermissionsString="AddListItems, EditListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Create"
  Text="<%$Resources:wss,siteactions_addapp15%>"
  Description="<%$Resources:wss,siteactions_createdesc%>"
  MenuGroupId="200"
  Sequence="230"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/addanapp.aspx')"
  PermissionsString="ManageLists, ManageSubwebs"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ViewAllSiteContents"
  Text="<%$Resources:wss,quiklnch_allcontent_15%>"
  Description="<%$Resources:wss,siteactions_allcontentdescription%>"
  ImageUrl="/_layouts/15/images/allcontent32.png?rev=32"
  MenuGroupId="200"
  Sequence="240"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/viewlsts.aspx"
  PermissionsString="ViewFormPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ChangeTheLook"
  Text="<%$Resources:wss,siteactions_changethelook15%>"
  Description="<%$Resources:wss,siteactions_changethelookdesc15%>"
  MenuGroupId="300"
  Sequence="310"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/designgallery.aspx"
  PermissionsString="ApplyThemeAndBorder,ApplyStyleSheets,Open,ViewPages,OpenItems,ViewListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Settings"
  Text="<%$Resources:wss,siteactions_settings15%>"
  Description="<%$Resources:wss,siteactions_sitesettingsdescriptionv4%>"
  ImageUrl="/_layouts/15/images/settingsIcon.png?rev=32"
  MenuGroupId="300"
  Sequence="320"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/settings.aspx')"
  PermissionsString="EnumeratePermissions,ManageWeb,ManageSubwebs,AddAndCustomizePages,ApplyThemeAndBorder,ManageAlerts,ManageLists,ViewUsageData"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_SwitchToMobileView"
  Visible="false"
  Text="<%$Resources:wss,siteactions_switchtomobileview%>"
  Description="<%$Resources:wss,siteactions_switchtomobileviewdesc%>"
  MenuGroupId="300"
  Sequence="330"
  UseShortId="true"
  ClientOnClickScript="STSNavigate(StURLSetVar2(ajaxNavigate.get_href(), 'mobile', '1'));" />
</SharePoint:FeatureMenuTemplate>
</CustomTemplate>
  </SharePoint:SiteActions></span>
</div>
<SharePoint:ScriptBlock runat="server">
var g_navBarHelpDefaultKey = "HelpHome";
</SharePoint:ScriptBlock>
<SharePoint:DelegateControl id="ID_SuiteBarDelegate" ControlId="SuiteBarDelegate" runat="server" />
  </SharePoint:SPSecurityTrimmedControl>
```


## <a name="see-also"></a><span data-ttu-id="a9e5d-149">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a9e5d-149">See also</span></span>
<span data-ttu-id="a9e5d-150"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a9e5d-150"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="a9e5d-151">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9e5d-151">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a9e5d-152">Neuerung bei SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="a9e5d-152">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  
-  [<span data-ttu-id="a9e5d-153">Menu control overview (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a9e5d-153">Menu control overview (ASP.NET)</span></span>](http://msdn.microsoft.com/de-DE/library/ecs0x9w5%28v=vs.90%29.aspx.aspx)
    
  

