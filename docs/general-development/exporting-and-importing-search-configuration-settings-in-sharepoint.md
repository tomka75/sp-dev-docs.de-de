---
title: "Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d00679a3-ffa2-4281-ad8b-70fc2c4a14e2
ms.openlocfilehash: 517e7e941ef0f4b45d77c77581ddf50a8b38311f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="exporting-and-importing-search-configuration-settings-in-sharepoint"></a><span data-ttu-id="b40f8-102">Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b40f8-102">Exporting and importing search configuration settings in SharePoint</span></span>
<span data-ttu-id="b40f8-p101">Rufen Sie Codebeispiele, die Ihnen zeigen, wie exportieren und importieren angepasster suchkonfigurationseinstellungen. Dazu gehören alle benutzerdefinierten Abfrageregeln, ergebnisquellen, Ergebnistypen, Bewertungsmodelle und Website für die Suche. SharePoint wird diese Funktionalität durch den Namespace  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) verfügbar gemacht.Außerdem können Sie die Einstellungen von Websitesammlungen und Websites importieren und Exportieren benutzerdefinierter suchkonfigurationseinstellungen aus einer Suchdienstanwendung (SSA).</span><span class="sxs-lookup"><span data-stu-id="b40f8-p101">Get code examples that show you how to export and import customized search configuration settings. These settings include all customized query rules, result sources, result types, ranking models, and site search settings. SharePoint exposes this functionality through the  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) namespace.You can also export customized search configuration settings from a Search service application (SSA) and import the settings to site collections and sites.</span></span> 

> [!NOTE]
> <span data-ttu-id="b40f8-106">Sie können benutzerdefinierte Suchkonfigurationseinstellungen nicht in eine SSA importieren oder die standardmäßigen Suchkonfigurationseinstellungen exportieren.</span><span class="sxs-lookup"><span data-stu-id="b40f8-106">Note: You can't import customized search configuration settings to an SSA, or export the default search configuration settings.</span></span> 
  
    
    


## <a name="export-search-configuration-settings"></a><span data-ttu-id="b40f8-107">Exportieren von Suchkonfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="b40f8-107">Export search configuration settings</span></span>
<span data-ttu-id="b40f8-108"><a name="SP15_exporting_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="b40f8-108"><a name="SP15_exporting_search_configuration"> </a></span></span>

<span data-ttu-id="b40f8-109">Der folgende Code zeigt, wie Sie mit [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) die Suchkonfigurationseinstellungen Ihrer Website exportieren können.</span><span class="sxs-lookup"><span data-stu-id="b40f8-109">The following code shows how to use  [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) to export your site's search configuration settings.</span></span> <span data-ttu-id="b40f8-110">Der Code verwendet eine Beispielwebsite `http://yoursite/sites/publishing1`, die Sie durch Ihre eigene Website ersetzen.</span><span class="sxs-lookup"><span data-stu-id="b40f8-110">The code uses an example site `http://yoursite/sites/publishing1`, which you'd replace with your own site.</span></span>  <span data-ttu-id="b40f8-111">_fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="b40f8-111">_fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

```

private static void Export(string fileName)
{
    SPSite site = new SPSite("http://yoursite/sites/publishing1");
    SearchConfigurationPortability conf = new SearchConfigurationPortability(site);
    SearchObjectOwner owner = new SearchObjectOwner(SearchObjectLevel.SPWeb, site.OpenWeb());
    var buff = conf.ExportSearchConfiguration(owner);
    File.WriteAllText(fileName, buff);
    site.Close();
}
```


## <a name="import-search-configuration-settings"></a><span data-ttu-id="b40f8-112">Importieren von Suchkonfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="b40f8-112">Import search configuration settings</span></span>
<span data-ttu-id="b40f8-113"><a name="SP15_importing_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="b40f8-113"><a name="SP15_importing_search_configuration"> </a></span></span>

<span data-ttu-id="b40f8-114">Der folgende Code zeigt, die Sie die Suchkonfigurationseinstellungen aus einer Datei mithilfe von [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) importieren und aktuelle Sucheinstellungen auf einer bestimmten Website, `http://yoursite/sites/publishing1`, ersetzen können.</span><span class="sxs-lookup"><span data-stu-id="b40f8-114">The following code shows how to import search configuration settings from a file by using  [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) and replace the existing search settings on a specified site, `http://yoursite/sites/publishing1`.</span></span>  <span data-ttu-id="b40f8-115">_fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="b40f8-115">_fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

```cs

private static void Import(string fileName)
{
    SPSite site = new SPSite("http://yoursite/sites/publishing1");
    SearchConfigurationPortability conf = new SearchConfigurationPortability(site);
    SearchObjectOwner owner = new SearchObjectOwner(SearchObjectLevel.SPWeb, site.OpenWeb());
    conf.ImportSearchConfiguration(owner, File.ReadAllText(fileName));
    site.Close();
}

```


## <a name="see-also"></a><span data-ttu-id="b40f8-116">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b40f8-116">See also</span></span>
<span data-ttu-id="b40f8-117"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b40f8-117"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b40f8-118">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b40f8-118">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  <span data-ttu-id="b40f8-119">[Exportieren und Importieren von benutzerdefinierten Suchkonfigurationseinstellungen in SharePoint](http://technet.microsoft.com/de-DE/library/jj871675.aspx)</span><span class="sxs-lookup"><span data-stu-id="b40f8-119">[Export and import customized search configuration settings in SharePoint](http://technet.microsoft.com/de-DE/library/jj871675.aspx)</span></span>
    
  

  
    
    

