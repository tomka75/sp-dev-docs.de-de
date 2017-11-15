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
# <a name="exporting-and-importing-search-configuration-settings-in-sharepoint"></a>Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint
Rufen Sie Codebeispiele, die Ihnen zeigen, wie exportieren und importieren angepasster suchkonfigurationseinstellungen. Dazu gehören alle benutzerdefinierten Abfrageregeln, ergebnisquellen, Ergebnistypen, Bewertungsmodelle und Website für die Suche. SharePoint wird diese Funktionalität durch den Namespace  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) verfügbar gemacht.Außerdem können Sie die Einstellungen von Websitesammlungen und Websites importieren und Exportieren benutzerdefinierter suchkonfigurationseinstellungen aus einer Suchdienstanwendung (SSA). 
> **Hinweis:** Sie können benutzerdefinierte Suchkonfigurationseinstellungen nicht in eine SSA importieren oder die standardmäßigen Suchkonfigurationseinstellungen exportieren. 
  
    
    


## <a name="export-search-configuration-settings"></a>Exportieren von Suchkonfigurationseinstellungen
<a name="SP15_exporting_search_configuration"> </a>

Der folgende Code zeigt, wie Sie mit [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) die Suchkonfigurationseinstellungen Ihrer Website exportieren können. Der Code verwendet eine Beispielwebsite `http://yoursite/sites/publishing1`, die Sie durch Ihre eigene Website ersetzen.  _fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.
  
    
    

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


## <a name="import-search-configuration-settings"></a>Importieren von Suchkonfigurationseinstellungen
<a name="SP15_importing_search_configuration"> </a>

Der folgende Code zeigt, die Sie die Suchkonfigurationseinstellungen aus einer Datei mithilfe von [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) importieren und aktuelle Sucheinstellungen auf einer bestimmten Website, `http://yoursite/sites/publishing1`, ersetzen können.  _fileName_ bezieht sich auf die Datei mit den Suchkonfigurationseinstellungen; _owner_ gibt die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx)-Ebene an, auf der die Suchkonfigurationseinstellungen abgerufen werden.
  
    
    

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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Suche in SharePoint](search-in-sharepoint.md)
    
  
-  
  [Exportieren und Importieren von benutzerdefinierten Suchkonfigurationseinstellungen in SharePoint](http://technet.microsoft.com/en-us/library/jj871675.aspx)
    
  

  
    
    

