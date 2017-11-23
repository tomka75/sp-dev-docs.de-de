---
title: "Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d00679a3-ffa2-4281-ad8b-70fc2c4a14e2
ms.openlocfilehash: 2b742f7676a7252a45609d92da05dd670f34b5d4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="exporting-and-importing-search-configuration-settings-in-sharepoint"></a><span data-ttu-id="0a7ba-102">Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a7ba-102">Exporting and importing search configuration settings in SharePoint</span></span>
<span data-ttu-id="0a7ba-p101">Rufen Sie Codebeispiele, die Ihnen zeigen, wie exportieren und importieren angepasster suchkonfigurationseinstellungen. Dazu gehören alle benutzerdefinierten Abfrageregeln, ergebnisquellen, Ergebnistypen, Bewertungsmodelle und Website für die Suche. SharePoint wird diese Funktionalität durch den Namespace  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) verfügbar gemacht.Außerdem können Sie die Einstellungen von Websitesammlungen und Websites importieren und Exportieren benutzerdefinierter suchkonfigurationseinstellungen aus einer Suchdienstanwendung (SSA).</span><span class="sxs-lookup"><span data-stu-id="0a7ba-p101">Get code examples that show you how to export and import customized search configuration settings. These settings include all customized query rules, result sources, result types, ranking models, and site search settings. SharePoint exposes this functionality through the  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) namespace.You can also export customized search configuration settings from a Search service application (SSA) and import the settings to site collections and sites.</span></span> 
> <span data-ttu-id="0a7ba-106">**Hinweis:** Sie können benutzerdefinierte Suchkonfigurationseinstellungen nicht in eine SSA importieren oder die standardmäßigen Suchkonfigurationseinstellungen exportieren.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-106">**Note** You can't import customized search configuration settings to an SSA, or export the default search configuration settings.</span></span> 
  
    
    


## <a name="export-search-configuration-settings"></a><span data-ttu-id="0a7ba-107">Exportieren von Suchkonfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="0a7ba-107">Export search configuration settings</span></span>
<span data-ttu-id="0a7ba-108"><a name="SP15_exporting_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="0a7ba-108"></span></span>

<span data-ttu-id="0a7ba-109">Der folgende Code zeigt, wie Sie mit [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) die Suchkonfigurationseinstellungen Ihrer Website exportieren können.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-109">The following code shows how to use  [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) to export your site's search configuration settings.</span></span> <span data-ttu-id="0a7ba-110">Der Code verwendet eine Beispielwebsite `http://yoursite/sites/publishing1`, die Sie durch Ihre eigene Website ersetzen.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-110">The code uses an example site `http://yoursite/sites/publishing1`, which you'd replace with your own site.</span></span>  <span data-ttu-id="0a7ba-111">_fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-111">The following code shows how to import search configuration settings from a file by using  _SearchConfigurationPortability and replace the existing search settings on a specified site, http://yoursite/sites/publishing1.  fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

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


## <a name="import-search-configuration-settings"></a><span data-ttu-id="0a7ba-112">Importieren von Suchkonfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="0a7ba-112">Import search configuration settings</span></span>
<span data-ttu-id="0a7ba-113"><a name="SP15_importing_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="0a7ba-113"></span></span>

<span data-ttu-id="0a7ba-114">Der folgende Code zeigt, die Sie die Suchkonfigurationseinstellungen aus einer Datei mithilfe von [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) importieren und aktuelle Sucheinstellungen auf einer bestimmten Website, `http://yoursite/sites/publishing1`, ersetzen können.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-114">The following code shows how to import search configuration settings from a file by using  SearchConfigurationPortability and replace the existing search settings on a specified site, http://yoursite/sites/publishing1.  fileName refers to the file where the search configuration settings are stored; owner specifies the SPWeb level at which the search configuration settings are obtained.</span></span>  <span data-ttu-id="0a7ba-115">_fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="0a7ba-115">The following code shows how to import search configuration settings from a file by using  _SearchConfigurationPortability and replace the existing search settings on a specified site, http://yoursite/sites/publishing1.  fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

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


## <a name="additional-resources"></a><span data-ttu-id="0a7ba-116">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0a7ba-116">Additional resources</span></span>
<span data-ttu-id="0a7ba-117"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0a7ba-117"></span></span>


-  [<span data-ttu-id="0a7ba-118">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a7ba-118">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  <span data-ttu-id="0a7ba-119">
  [Exportieren und Importieren von benutzerdefinierten Suchkonfigurationseinstellungen in SharePoint](http://technet.microsoft.com/de-de/library/jj871675.aspx)</span><span class="sxs-lookup"><span data-stu-id="0a7ba-119">[Export and import customized search configuration settings in SharePoint Server 2013](http://technet.microsoft.com/de-de/library/jj871675.aspx)</span></span>
    
  

  
    
    

