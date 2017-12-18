---
title: "Websiteübergreifende Veröffentlichung in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33f49e69-c1d3-4a6e-8887-5df683cba022
ms.openlocfilehash: e6db277ceb3c45e0f147e27c96b272afe4e585ee
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="cross-site-publishing-in-sharepoint"></a><span data-ttu-id="ad944-102">Websiteübergreifende Veröffentlichung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad944-102">Cross-site publishing in SharePoint</span></span>

<span data-ttu-id="ad944-p101">SharePoint führt ein Cross-Site publishing-Feature, mit dem Sie Inhalte in mehreren Websitesammlungen wiederverwenden kann. Funktionen für die integrierte Suche verwendet, um die Veröffentlichung Szenarien und-Architekturen aktivieren. Bei der ersten können Sie Websites, die SharePoint-Farmen schneidet entwerfen - aktivieren Ihre Websites umfassen die Grenze zwischen Intranets und dem Internet.</span><span class="sxs-lookup"><span data-stu-id="ad944-p101">SharePoint introduces a cross-site publishing feature that enables you to reuse content across multiple site collections. It uses built-in search capabilities to enable publishing scenarios and architectures. For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet.</span></span>
  
    
    

<span data-ttu-id="ad944-p102">Berücksichtigen Sie eine Website mit einer erstellungswebsitesammlung, die mehrere veröffentlichungswebsitesammlungen, mit anderen Domänen feeds alle durchforsteten von öffentlichen Suchmaschinen und für die suchmaschinenoptimierung (SEO) optimiert. Websiteübergreifende Veröffentlichung ermöglicht dieses Szenario und andere gefällt, ohne dass Sie die Bereitstellung von Inhalten verwenden. Websiteübergreifende Veröffentlichung wurde entwickelt, mit einigen häufigen Szenarien berücksichtigen, einschließlich:</span><span class="sxs-lookup"><span data-stu-id="ad944-p102">Consider a site with one authoring site collection that feeds multiple publishing site collections, with different domains, all crawled by public search engines and optimized for search engine optimization (SEO). Cross-site publishing enables this scenario and others like it, without requiring you to use content deployment. Cross-site publishing was designed with some common scenarios in mind, including:</span></span>
  
    
    


- <span data-ttu-id="ad944-109">Freigeben einer Elementliste oder einer Seitenbibliothek als Katalog veröffentlichen</span><span class="sxs-lookup"><span data-stu-id="ad944-109">Share an item list or a page library as a publishing catalog</span></span>
    
  
- <span data-ttu-id="ad944-110">Einen Katalog von Suche nutzen</span><span class="sxs-lookup"><span data-stu-id="ad944-110">Consume a catalog from search</span></span>
    
  
- <span data-ttu-id="ad944-111">Kombinieren Sie websiteübergreifende Veröffentlichung mit dem Variationsfeature zum Aktivieren der Erstellung mehrsprachiger Websites aus einer gemeinsamen erstellungswebsitesammlung</span><span class="sxs-lookup"><span data-stu-id="ad944-111">Combine cross-site publishing with the variations feature to enable authoring multilingual sites from a common authoring site collection</span></span>
    
  

## <a name="catalogs"></a><span data-ttu-id="ad944-112">Kataloge</span><span class="sxs-lookup"><span data-stu-id="ad944-112">Catalogs</span></span>
<span data-ttu-id="ad944-113"><a name="SP15_CrossSitePublising_Catalog"> </a></span><span class="sxs-lookup"><span data-stu-id="ad944-113"><a name="SP15_CrossSitePublising_Catalog"> </a></span></span>

<span data-ttu-id="ad944-p103">Kataloge, eingeführt in SharePoint, umfassen eine Liste oder Bibliothek, die um zu suchenden Auslastung für Veröffentlichungssites freigegeben ist. Kataloge Inhalt zu veröffentlichenden in allen Websitesammlungen aktivieren - die Cross-Site-Veröffentlichungsfeatures hängen Kataloge. Kataloge können wirklich Wiederverwendung von Inhalten an Ihren Standorten und über die Grenze zwischen Ihrer Intranetwebsites, extranet-Websites und Internetwebsites. Kataloge werden für vordefinierte Suchabfragen bei der Suche gekennzeichnet. Sie können Inhalte, die mithilfe der  [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint.md)in Kataloge über Websitesammlungen hinweg offenlegen.</span><span class="sxs-lookup"><span data-stu-id="ad944-p103">Catalogs, introduced in SharePoint, include a list or library that is shared out to search for consumption on publishing sites. Catalogs enable content to be published across site collections—the cross-site publishing features depend on catalogs. You can use catalogs to really reuse content across your sites and across the boundary between your intranet sites, extranet sites, and Internet sites. For predefined search queries, catalogs are flagged in search. You can surface content stored in catalogs across site collections by using the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint.md).</span></span>
  
    
    

## <a name="when-should-i-use-cross-site-publishing"></a><span data-ttu-id="ad944-119">Wann sollte ich die websiteübergreifende Veröffentlichung werden verwendet?</span><span class="sxs-lookup"><span data-stu-id="ad944-119">When should I use cross-site publishing?</span></span>
<span data-ttu-id="ad944-120"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="ad944-120"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span></span>

<span data-ttu-id="ad944-p104">Es gibt einigen Fällen, in dem websiteübergreifende Veröffentlichung nicht effizienter oder geeignet ist. Ihre Entscheidung sollten, ob Sie die externen Datenquellen und wie Sie eine Verbindung mit ihnen, Variationen, Websitetyp, Implementierung von Search-Datenbank verfügen, und Verwenden des Produktkatalogs werden alle Faktoren, die Einfluss auf. Tabelle 1 enthält weitere Informationen zu diesen Entwurfsaspekte.</span><span class="sxs-lookup"><span data-stu-id="ad944-p104">There are some cases where cross-site publishing is not efficient or appropriate. Whether you have external data sources and how you connect to them, variations, site type, search database implementation, and use of the product catalog are all factors that should influence your decision. Table 1 provides more information about these design considerations.</span></span>
  
    
    

<span data-ttu-id="ad944-124">**In Tabelle 1. Entwurfsaspekte für die websiteübergreifende Veröffentlichung**</span><span class="sxs-lookup"><span data-stu-id="ad944-124">**Table 1. Design considerations for cross-site publishing**</span></span>


|<span data-ttu-id="ad944-125">**Aspekte beim Entwurf**</span><span class="sxs-lookup"><span data-stu-id="ad944-125">**Design Consideration**</span></span>|<span data-ttu-id="ad944-126">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ad944-126">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ad944-127">**Zeitabstand**</span><span class="sxs-lookup"><span data-stu-id="ad944-127">**Lag time**</span></span> <br/> |<span data-ttu-id="ad944-128">Wenn die Verzögerung zwischen dem Zeitpunkt ein Autor veröffentlicht, einer Seite und wenn sie auf wird die Website ist zu lang nach einer Person hängt davon ab, Sie sollten stattdessen Bereitstellung von Inhalten verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="ad944-128">If the delay between the time an author publishes a page and when it shows up on the site is too long for someone who depends on it, you may want to consider using content deployment instead.</span></span>  <br/> |
|<span data-ttu-id="ad944-129">**Implementierung von Search-Datenbank**</span><span class="sxs-lookup"><span data-stu-id="ad944-129">**Search database implementation**</span></span> <br/> |<span data-ttu-id="ad944-p105">Wenn Sie die Suchdatenbank Herstellen einer Verbindung mit einer externen Datenquelle, und eines extern (nicht-SharePoint)-Connectors verwenden, nicht websiteübergreifende Veröffentlichung verwendet werden. Wenn Sie Business Connection Services (BCS) verwenden, können Sie die websiteübergreifende Veröffentlichung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad944-p105">If you connect your search database to an external data source and you use an external (non-SharePoint) connector, you can't use cross-site publishing. If you use business connection services (BCS), you can use cross-site publishing.</span></span>  <br/> <span data-ttu-id="ad944-p106">Verwenden websiteübergreifende Veröffentlichung mit der Suchdatenbank ist sinnvoll in einigen Fällen. Sie sollten nicht websiteübergreifende Veröffentlichung verwenden, um aus einer Quellwebsite direkt mit dem Internet auf eine Weise zu veröffentlichen, die nicht der Suchdatenbank in der Implementierung der Planung oder benutzerdefinierten Code enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="ad944-p106">Using cross-site publishing with the search database makes sense in some cases but not others. You should not use cross-site publishing to publish from a source site directly to the Internet in a way that does not include your search database in the planning or custom code implementation.</span></span>  <br/> |
|<span data-ttu-id="ad944-134">**Implementierung von Variationen**</span><span class="sxs-lookup"><span data-stu-id="ad944-134">**Variations implementation**</span></span> <br/> |<span data-ttu-id="ad944-p107">Wenn Sie eine grundlegende Variationswebsite, durch die Bibliothek für Seiten und eine Dokumentbibliothek, implementieren und allgemeine in einigen Sprachen verfügbar sind, wird die websiteübergreifende Veröffentlichung sinnvoll. Identisch ist True, wenn Sie angeben, dass die verwaltete Navigation oder strukturierte Navigation auf einer Variationswebsite implementieren.</span><span class="sxs-lookup"><span data-stu-id="ad944-p107">If you are implementing a basic variations site that makes a pages library, document library, and general lists available in a few languages, cross-site publishing makes sense. The same is true if you choose to implement managed navigation or structured navigation on a variations site.  </span></span><br/> <span data-ttu-id="ad944-p108"> Websiteübergreifende Veröffentlichung ist für einige Architekturen, aber nicht für andere Benutzer. Beispielsweise können Sie websiteübergreifende Veröffentlichung zum Veröffentlichen von Inhalt aus einer Variationen **SPSite** in einer Veröffentlichungssite mit Variationen aktiviert, wenn die Quelle **SPSite** nicht verarbeiten von Daten aus einer anderen Variationswebsite ist oder Websitesammlung festlegen. </span><span class="sxs-lookup"><span data-stu-id="ad944-p108">Cross-site publishing works for some architectures but not others. For example, you can use cross-site publishing to publish content from a variations **SPSite** to a publishing site with variations enabled if the source **SPSite** is not consuming data from another variations site or site collection. </span></span><br/> |
|<span data-ttu-id="ad944-139">**Catalog-Implementierung**</span><span class="sxs-lookup"><span data-stu-id="ad944-139">**Catalog implementation**</span></span> <br/> |<span data-ttu-id="ad944-p109">Gibt an, ob Sie den Produktkatalog in Ihrer Websitearchitektur implementieren und Implementierung kann es auswirken, ob die websiteübergreifende Veröffentlichung die am häufigsten effektiv oder entsprechenden Wahl ist. Wenn Sie mithilfe des Produktkatalogs einer mehrsprachigen Variationen Standortkonfiguration unterstützen und einer Internetwebsite veröffentlichen, können Sie die websiteübergreifende Veröffentlichung implementieren.</span><span class="sxs-lookup"><span data-stu-id="ad944-p109">Whether you implement the product catalog into your site architecture and how you implement it may affect whether cross-site publishing is the most effective or appropriate choice. If you are using the product catalog to support a multilingual variations site configuration and are publishing to an Internet site, you can implement cross-site publishing.</span></span>  <br/> |
|<span data-ttu-id="ad944-142">**Verwaltete navigation**</span><span class="sxs-lookup"><span data-stu-id="ad944-142">**Managed navigation**</span></span> <br/> |<span data-ttu-id="ad944-p110">Websiteübergreifende Veröffentlichung funktioniert mit den meisten Implementierungen von verwaltete Navigation und den Terminologiespeicher. In einigen Implementierungen Navigation Metadaten Übertragung funktionieren möglicherweise nicht wie erwartet. Beispielsweise, wenn eine Variationswebsite hängt von Metadaten aus einer anderen Variationswebsite Laufwerk Websitenavigation, und Sie websiteübergreifende Veröffentlichung zum Veröffentlichen von Inhalten auf der Zielwebsite verwenden, Navigation Metadaten übertragen funktioniert möglicherweise nicht wie erwartet.</span><span class="sxs-lookup"><span data-stu-id="ad944-p110">Cross-site publishing works with most implementations of managed navigation and the term store. In some implementations, navigation metadata transfer may not work as expected. For example, when one variations site depends on metadata from another variations site to drive site navigation, and you use cross-site publishing to publish content to the target site, navigation metadata transfer may not work as expected.</span></span>  <br/> |
   

## <a name="how-can-i-set-up-a-catalog"></a><span data-ttu-id="ad944-146">Wie kann ich einen Katalog einrichten?</span><span class="sxs-lookup"><span data-stu-id="ad944-146">How can I set up a catalog?</span></span>
<span data-ttu-id="ad944-147"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="ad944-147"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span></span>

<span data-ttu-id="ad944-148">Kategorieseiten und Katalogobjektseiten sind Seitenlayouts, die Sie zum konsistenten Anzeigen von strukturiertem Kataloginhalt auf einer Website verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ad944-148">Category pages and catalog item pages are page layouts that you can use to show structured catalog content consistently across a site.</span></span> <span data-ttu-id="ad944-149">SharePoint ermöglicht das Erstellen und Anpassen von Seitenlayouts für SharePoint und höher.</span><span class="sxs-lookup"><span data-stu-id="ad944-149">SharePoint enables you to create and customize page layouts for SharePoint and above.</span></span> <span data-ttu-id="ad944-150">Weitere Informationen finden Sie unter [Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint](https://msdn.microsoft.com/en-us/library/office/dn144674.aspx 
).</span><span class="sxs-lookup"><span data-stu-id="ad944-150">For more information, see  [Customize page layouts for a catalog-based site in SharePoint](https://msdn.microsoft.com/en-us/library/office/dn144674.aspx 
).</span></span>
  
    
    

## <a name="cross-site-publishing-apis"></a><span data-ttu-id="ad944-151">APIs für websiteübergreifende Veröffentlichung</span><span class="sxs-lookup"><span data-stu-id="ad944-151">Cross-site publishing APIs</span></span>
<span data-ttu-id="ad944-152"><a name="SP15_CrossSitePublising_CrossSitePublishingAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="ad944-152"><a name="SP15_CrossSitePublising_CrossSitePublishingAPIs"> </a></span></span>

<span data-ttu-id="ad944-p112">SharePoint stellt die Klassen, die Sie zur Unterstützung von Cross-Site publishing Implementierung in Ihrem Code verwenden können. Diese APIs stehen in der Bibliothek unter .NET Server veröffentlichen. Verwenden sie zum Anpassen von wie SharePoint teilt Listen als Kataloge für die Wiederverwendung von Inhalten, oder einen Katalog von Suche nutzt. Die Mitglieder der folgenden Klassen können in benutzerdefiniertem Code Sie um Cross-Site publishing Aufgaben zu unterstützen:</span><span class="sxs-lookup"><span data-stu-id="ad944-p112">SharePoint introduces classes that you can use to support cross-site publishing implementation in your code. These APIs are available in the .NET server publishing library. Use them to customize how SharePoint shares lists as catalogs for content reuse or consumes a catalog from search. You can use the members of the following classes in custom code to support cross-site publishing tasks:</span></span>
  
    
    

- <span data-ttu-id="ad944-157">Verwenden Sie die **PublishingCatalogUtility** -Klasse zum Abrufen einer Liste der verfügbaren Kataloge, Abrufen von Informationen über Kataloge und deren Status, Abrufen von Informationen zu Listen und Bibliotheken, die Katalogen hergestellt werden können und starten oder beenden Sie die Freigabe Kataloge.</span><span class="sxs-lookup"><span data-stu-id="ad944-157">Use the **PublishingCatalogUtility** class to retrieve a list of available catalogs, get information about catalogs and their statuses, get information about lists and libraries that can be connected to catalogs, and start or stop sharing catalogs.</span></span>
    
    
    


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

- <span data-ttu-id="ad944-p113">Verwenden Sie die **CatalogCollectionManager** -Klasse, um Kataloge von Suche nutzen. Erfahren Sie mehr über die Verbindung, die ein Katalog suchen und Abrufen von Informationen über sie. Hinzufügen oder Entfernen eines Katalogs aus der internen Auflistung der Kataloge, und in die Warteschlange eines Vorgangs zum Einrichten einer Verbindung in die Warteschlange, der konfiguriert ist, um URLs umzuschreiben, wenn die **Update** -Methode aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="ad944-p113">Use the **CatalogCollectionManager** class to consume catalogs from search. Learn about the connection that a catalog has to search, and get information about it. Add or remove a catalog from the internal collection of catalogs, and queue an operation to queue up a connection that is configured to rewrite URLs when the **Update** method is called.</span></span>
    
    
    


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


## <a name="see-also"></a><span data-ttu-id="ad944-161">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ad944-161">See also</span></span>
<span data-ttu-id="ad944-162"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ad944-162"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ad944-163">Veröffentlichen von SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="ad944-163">Publish SharePoint sites</span></span>](publish-sharepoint-sites.md)
    
  

