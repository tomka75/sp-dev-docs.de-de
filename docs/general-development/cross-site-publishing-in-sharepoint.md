---
title: "Websiteübergreifende Veröffentlichung in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33f49e69-c1d3-4a6e-8887-5df683cba022
ms.openlocfilehash: cbb1a0eec5d60b8453e3d6c66179142fa1e07630
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="cross-site-publishing-in-sharepoint"></a>Websiteübergreifende Veröffentlichung in SharePoint

SharePoint führt ein Cross-Site publishing-Feature, mit dem Sie Inhalte in mehreren Websitesammlungen wiederverwenden kann. Funktionen für die integrierte Suche verwendet, um die Veröffentlichung Szenarien und-Architekturen aktivieren. Bei der ersten können Sie Websites, die SharePoint-Farmen schneidet entwerfen - aktivieren Ihre Websites umfassen die Grenze zwischen Intranets und dem Internet.
  
    
    

Berücksichtigen Sie eine Website mit einer erstellungswebsitesammlung, die mehrere veröffentlichungswebsitesammlungen, mit anderen Domänen feeds alle durchforsteten von öffentlichen Suchmaschinen und für die suchmaschinenoptimierung (SEO) optimiert. Websiteübergreifende Veröffentlichung ermöglicht dieses Szenario und andere gefällt, ohne dass Sie die Bereitstellung von Inhalten verwenden. Websiteübergreifende Veröffentlichung wurde entwickelt, mit einigen häufigen Szenarien berücksichtigen, einschließlich:
  
    
    


- Freigeben einer Elementliste oder einer Seitenbibliothek als Katalog veröffentlichen
    
  
- Einen Katalog von Suche nutzen
    
  
- Kombinieren Sie websiteübergreifende Veröffentlichung mit dem Variationsfeature zum Aktivieren der Erstellung mehrsprachiger Websites aus einer gemeinsamen erstellungswebsitesammlung
    
  

## <a name="catalogs"></a>Kataloge
<a name="SP15_CrossSitePublising_Catalog"> </a>

Kataloge, eingeführt in SharePoint, umfassen eine Liste oder Bibliothek, die um zu suchenden Auslastung für Veröffentlichungssites freigegeben ist. Kataloge Inhalt zu veröffentlichenden in allen Websitesammlungen aktivieren - die Cross-Site-Veröffentlichungsfeatures hängen Kataloge. Kataloge können wirklich Wiederverwendung von Inhalten an Ihren Standorten und über die Grenze zwischen Ihrer Intranetwebsites, extranet-Websites und Internetwebsites. Kataloge werden für vordefinierte Suchabfragen bei der Suche gekennzeichnet. Sie können Inhalte, die mithilfe der  [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint.md)in Kataloge über Websitesammlungen hinweg offenlegen.
  
    
    

## <a name="when-should-i-use-cross-site-publishing"></a>Wann sollte ich die websiteübergreifende Veröffentlichung werden verwendet?
<a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a>

Es gibt einigen Fällen, in dem websiteübergreifende Veröffentlichung nicht effizienter oder geeignet ist. Ihre Entscheidung sollten, ob Sie die externen Datenquellen und wie Sie eine Verbindung mit ihnen, Variationen, Websitetyp, Implementierung von Search-Datenbank verfügen, und Verwenden des Produktkatalogs werden alle Faktoren, die Einfluss auf. Tabelle 1 enthält weitere Informationen zu diesen Entwurfsaspekte.
  
    
    

**In Tabelle 1. Entwurfsaspekte für die websiteübergreifende Veröffentlichung**


|**Aspekte beim Entwurf**|**Beschreibung**|
|:-----|:-----|
|**Zeitabstand** <br/> |Wenn die Verzögerung zwischen dem Zeitpunkt ein Autor veröffentlicht, einer Seite und wenn sie auf wird die Website ist zu lang nach einer Person hängt davon ab, Sie sollten stattdessen Bereitstellung von Inhalten verwenden möchten.  <br/> |
|**Implementierung von Search-Datenbank** <br/> |Wenn Sie die Suchdatenbank Herstellen einer Verbindung mit einer externen Datenquelle, und eines extern (nicht-SharePoint)-Connectors verwenden, nicht websiteübergreifende Veröffentlichung verwendet werden. Wenn Sie Business Connection Services (BCS) verwenden, können Sie die websiteübergreifende Veröffentlichung verwenden.  <br/> Verwenden websiteübergreifende Veröffentlichung mit der Suchdatenbank ist sinnvoll in einigen Fällen. Sie sollten nicht websiteübergreifende Veröffentlichung verwenden, um aus einer Quellwebsite direkt mit dem Internet auf eine Weise zu veröffentlichen, die nicht der Suchdatenbank in der Implementierung der Planung oder benutzerdefinierten Code enthalten ist.  <br/> |
|**Implementierung von Variationen** <br/> |Wenn Sie eine grundlegende Variationswebsite, durch die Bibliothek für Seiten und eine Dokumentbibliothek, implementieren und allgemeine in einigen Sprachen verfügbar sind, wird die websiteübergreifende Veröffentlichung sinnvoll. Identisch ist True, wenn Sie angeben, dass die verwaltete Navigation oder strukturierte Navigation auf einer Variationswebsite implementieren.<br/>  Websiteübergreifende Veröffentlichung ist für einige Architekturen, aber nicht für andere Benutzer. Beispielsweise können Sie websiteübergreifende Veröffentlichung zum Veröffentlichen von Inhalt aus einer Variationen **SPSite** in einer Veröffentlichungssite mit Variationen aktiviert, wenn die Quelle **SPSite** nicht verarbeiten von Daten aus einer anderen Variationswebsite ist oder Websitesammlung festlegen. <br/> |
|**Catalog-Implementierung** <br/> |Gibt an, ob Sie den Produktkatalog in Ihrer Websitearchitektur implementieren und Implementierung kann es auswirken, ob die websiteübergreifende Veröffentlichung die am häufigsten effektiv oder entsprechenden Wahl ist. Wenn Sie mithilfe des Produktkatalogs einer mehrsprachigen Variationen Standortkonfiguration unterstützen und einer Internetwebsite veröffentlichen, können Sie die websiteübergreifende Veröffentlichung implementieren.  <br/> |
|**Verwaltete navigation** <br/> |Websiteübergreifende Veröffentlichung funktioniert mit den meisten Implementierungen von verwaltete Navigation und den Terminologiespeicher. In einigen Implementierungen Navigation Metadaten Übertragung funktionieren möglicherweise nicht wie erwartet. Beispielsweise, wenn eine Variationswebsite hängt von Metadaten aus einer anderen Variationswebsite Laufwerk Websitenavigation, und Sie websiteübergreifende Veröffentlichung zum Veröffentlichen von Inhalten auf der Zielwebsite verwenden, Navigation Metadaten übertragen funktioniert möglicherweise nicht wie erwartet.  <br/> |
   

## <a name="how-can-i-set-up-a-catalog"></a>Wie kann ich einen Katalog einrichten?
<a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a>

Kategorieseiten und Katalogobjektseiten sind Seitenlayouts, die Sie zum konsistenten Anzeigen von strukturiertem Kataloginhalt auf einer Website verwenden können. SharePoint ermöglicht das Erstellen und Anpassen von Seitenlayouts für SharePoint und höher. Weitere Informationen finden Sie unter [Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint](https://msdn.microsoft.com/en-us/library/office/dn144674.aspx 
).
  
    
    

## <a name="cross-site-publishing-apis"></a>APIs für websiteübergreifende Veröffentlichung
<a name="SP15_CrossSitePublising_CrossSitePublishingAPIs"> </a>

SharePoint stellt die Klassen, die Sie zur Unterstützung von Cross-Site publishing Implementierung in Ihrem Code verwenden können. Diese APIs stehen in der Bibliothek unter .NET Server veröffentlichen. Verwenden sie zum Anpassen von wie SharePoint teilt Listen als Kataloge für die Wiederverwendung von Inhalten, oder einen Katalog von Suche nutzt. Die Mitglieder der folgenden Klassen können in benutzerdefiniertem Code Sie um Cross-Site publishing Aufgaben zu unterstützen:
  
    
    

- Verwenden Sie die **PublishingCatalogUtility** -Klasse zum Abrufen einer Liste der verfügbaren Kataloge, Abrufen von Informationen über Kataloge und deren Status, Abrufen von Informationen zu Listen und Bibliotheken, die Katalogen hergestellt werden können und starten oder beenden Sie die Freigabe Kataloge.
    
    
    


```cs
  
/// Retrieve available catalogs.
public static List<CatalogConnectionSettings> GetPublishingCatalogs(SPSite site, int startRow, int numberOfRows, string filterText, out int totalNumberOfCatalogs)
```


    
    


```cs
  
///Get catalog information that is saved for a list.
public static bool GetCatalogConfiguration(SPList list, out CatalogShareSettings catalogSettings, out string selectedTaxonomyField)
```


    
    


```cs
  
///Stop sharing a list or library as a publishing catalog for cross-publishing content reuse.
public static void UnPublishCatalog(SPList list)
```

- Verwenden Sie die **CatalogCollectionManager** -Klasse, um Kataloge von Suche nutzen. Erfahren Sie mehr über die Verbindung, die ein Katalog suchen und Abrufen von Informationen über sie. Hinzufügen oder Entfernen eines Katalogs aus der internen Auflistung der Kataloge, und in die Warteschlange eines Vorgangs zum Einrichten einer Verbindung in die Warteschlange, der konfiguriert ist, um URLs umzuschreiben, wenn die **Update** -Methode aufgerufen wird.
    
    
    


```cs
  
/// Add catalog or site source into the internal CatalogInfo collection, but the source is not persisted into the property bag.
public void AddCatalogConnection(CatalogConnectionSettings catalogInfo)
```


    
    


```cs
  
/// Queues an Add operation to add a connection configured to rewrite URLs. The connection is added to the store when the Update method is called.
public void AddCatalogConnection(CatalogConnectionSettings catalogInfo, 
string[] orderedPropertiesForUrlRewrite,
string webUrl, 
string catalogTaxonomyManagedProperty,
bool isManualRule)
```


    
    


```cs
  
/// Update existing catalog/site source in the internal CatalogInfo collection. Edits are not committed until the Update method is called.
public void UpdateCatalogConnection(CatalogConnectionSettings catalogInfo)
```


    
    


```cs
  
/// Remove a catalog or site source. Deletion is not committed until the Update method is called.
public void DeleteCatalogConnection(string catalogPath)
```


    
    


```cs
  
/// Determine whether a connection exists to this source from the site.
public bool Contains(string catalogPath)
```


    
    


```cs
  
/// Get the settings for a catalog connected to this site.
public CatalogConnectionSettings GetCatalogConnectionSettings(string catalogPath)
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Veröffentlichen von SharePoint-Websites](publish-sharepoint-sites.md)
    
  

