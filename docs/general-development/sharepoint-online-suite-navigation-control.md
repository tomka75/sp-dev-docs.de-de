---
title: Navigationssteuerelement SharePoint Online-Suite
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ba93e5c0-e591-48d0-a716-a08ec7ef6cea
ms.openlocfilehash: d2f13eba8daea7cdf8fb865c3762ce6fad95da92
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-online-suite-navigation-control"></a>Navigationssteuerelement SharePoint Online-Suite
Informationen Sie zu gestaltungsvorlagenmarkup für das Steuerelement Suitenavigation in SharePoint Online. {Einführung einfügen}
  
    
    


## <a name="sharepoint-online-suite-navigation-control"></a>Navigationssteuerelement SharePoint Online-Suite

Das Suite Navigationssteuerelement rendert eine konsistente oberen Navigationsleiste in SharePoint Online. Dieses Steuerelement ist nun ein Teil der nicht angepasste Out-of-Box Gestaltungsvorlagen.
  
    
    
Wenn eine Gestaltungsvorlage angepasst wurde, werden die neuen Suite Navigationssteuerelement nicht übernommen. Um dieses Steuerelement in Ihre benutzerdefinierte Gestaltungsvorlage hinzuzufügen, ersetzen Sie die  `suiteBar` `<div>` mit dem Markup, das den Typ der Website entspricht, die Sie verwenden.
  
    
    
Das neue Suite Navigations-Steuerelement unterstützt auf der Website angewendete Design. Wenn Sie die Farbe der oberen Navigationsleiste ändern möchten, Anwenden eines Designs.
  
    
    

> **Wichtig:** Best Practice für die Anpassung von Websites ist die Verwendung eines Designs. Zwar können Sie auf Ihre Website auch benutzerdefinierten CSS-Code anwenden; dann besteht jedoch das Risiko, dass der Code nach einer Aktualisierung des Suite Navigation-Steuerelements im Dienst nicht mehr funktioniert. 
  
    
    


> **Vorsicht:** Wenn Sie das neue Steuerelement nicht verwenden möchten, müssen Sie das Suite Navigation-Markup von Ihrer Masterseite entfernen und benutzerdefiniertes Markup einfügen. Bedenken Sie dabei jedoch, dass angepasste Masterseiten Aktualisierungen an den Standardsteuerelementen für Masterseiten möglicherweise nicht übernehmen. Dasselbe gilt für neue Funktionen, die zu nicht angepassten Masterseiten hinzugefügt werden. Wenn Sie Ihre Masterseite anpassen, besteht das Risiko, dass Ihre Website nach einem Dienstupdate nicht mehr korrekt funktioniert oder nicht mehr wie gewünscht aussieht. 
  
    
    


### <a name="suite-navigation-control-for-intranet-sites"></a>Suite Navigation-Steuerelement für Intranetwebsites

Verwenden Sie das folgende Markup Gestaltungsvorlage für Intranetwebsites für die Suitenavigation-Steuerelement. Tabelle 1 enthält Websteuerelemente in der Suitenavigation Code verwendet.
  
    
    

**In Tabelle 1. Suite Navigation Websteuerelemente für Intranetwebsites**


|**Websteuerelement**|**Beschreibung**|
|:-----|:-----|
|SharePoint:Menu  <br/> |Zeigt ein Menü in einer ASP.NET-Webseite.  <br/> |
|SharePoint:MenuItemTemplate  <br/> |Stellt ein Steuerelement dar, das ein Element in einem Dropdownmenü erstellt.  <br/> |
   

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


#### <a name="learning-about-suite-navigation-web-controls-for-public-facing-sites"></a>Informationen zu Suitenavigation Websteuerelemente für öffentlich zugängliche Websites

Verwenden Sie das folgende Markup Gestaltungsvorlage für öffentlich zugängliche Websites für das Navigationssteuerelement Suite. Tabelle 2 sind die Websteuerelemente in der Suitenavigation Code verwendet.
  
    
    

**In Tabelle 2. Suite Navigation Websteuerelemente für öffentlich zugängliche Websites**


|**Websteuerelement**|**Beschreibung**|
|:-----|:-----|
|SharePoint:DelegateControl  <br/> |Ein Websteuerelement ASP.NET rendert. Stellvertretungs-Steuerelemente stellen ihre Candidate Steuerelemente austauschbaren und nachverfolgbare.  <br/> |
|SharePoint:FeatureMenuTemplate  <br/> |Stellt ein Steuerelement, das eine Vorlage für ein Dropdown Menü erstellt.  <br/> |
|SharePoint:Menu  <br/> |Zeigt ein Menü in einer ASP.NET-Webseite.  <br/> |
|SharePoint:MenuItemTemplate  <br/> |Stellt ein Steuerelement dar, das ein Element in einem Dropdownmenü erstellt.  <br/> |
|SharePoint:ScriptBlock  <br/> |Stellt ein Skript Block-Steuerelement auf einer Seite dar.  <br/> |
|SharePoint:SiteActions  <br/> |Stellt ein Vorlagensteuerelement für das Menü Websiteaktionen.  <br/> |
|SharePoint:SPSecurityTrimmedControl  <br/> |Rendert bedingt den Inhalt des Steuerelements für dem aktuellen Benutzer nur, wenn der aktuelle Benutzer in der **PermissionString**definierte Berechtigungen verfügt.  <br/> |
   

### <a name="suite-navigation-control-for-public-facing-sites"></a>Suite Navigationssteuerelement für öffentlich zugängliche Websites


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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Neuerung bei SharePoint-Websiteentwicklung](what-s-new-with-sharepoint-site-development.md)
    
  
-  [Menu control overview (ASP.NET)](http://msdn.microsoft.com/de-DE/library/ecs0x9w5%28v=vs.90%29.aspx.aspx)
    
  

