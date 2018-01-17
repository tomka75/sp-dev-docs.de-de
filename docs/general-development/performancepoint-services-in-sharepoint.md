---
title: PerformancePoint-Dienste in SharePoint
ms.date: 09/25/2017
keywords: "Zugreifen auf FCO-Definitionen in SharePoint, BI in SharePoint mithilfe der PerformancePoint-Dienste, Business Intelligence in SharePoint, Business Intelligence mithilfe der PerformancePoint-Dienste in SharePoint, Erstellen von Scorecardtransformationen mit PerformancePoint-Diensten in SharePoint, benutzerdefinierte Filtersteuerelemente in SharePoint, benutzerdefinierte PerformancePoint-Erweiterungen, Anpassen von PerformancePoint in SharePoint, Erstellen von Datenquellen in SharePoint, DLL-Dateien für die PerformancePoint-Entwicklung, Erweitern von PerformancePoint-Diensten für SharePoint, FCOs in SharePoint PerformancePoint, Filtererstellung in SharePoint, Filter als FCOs in PPS PerformancePoint, erste Schritte mit den PerformancePoint-Diensten, Integrieren der PerformancePoint-Dienste in SharePoint, PerformancePoint-Assemblys für Entwicklungsprojekte, benutzerdefinierte PerformancePoint-Datenquellen, benutzerdefinierte PerformancePoint-Filter, benutzerdefinierte PerformancePoint-Berichte, benutzerdefinierte PerformancePoint-Scorecardtransformationen, PerformancePoint-Entwicklungsszenarien, Entwickeln von PerformancePoint-Diensten, Entwicklungsszenarien für PerformancePoint-Dienste, Programmieren von PerformancePoint-Diensten, SDK für PerformancePoint-Dienste, benutzerdefinierte PPS-Dashboards in SharePoint, PPS-Entwicklung, PPS-Programmierung, PPS-SDK, Erstellen von Berichten in SharePoint, Berichtsrenderer in SharePoint, SharePoint-Dienstanwendung PerformancePoint"
f1_keywords: accessing fco definitions in SharePoint,bi in SharePoint using performancepoint services,business intelligence in SharePoint,business intelligence using performancepoint services in SharePoint,create scorecard transforms using performancepoint in SharePoint,custom filter control in SharePoint,custom performancepoint extensions,customize performancepoint in sharepoint,data source creation in SharePoint,dlls used for performancepoint development,extending performancepoint services for sharepoint,fcos in sharepoint performancepoint,filter creation in SharePoint,filters as fcos in pps performancepoint,getting started with performancepoint services,integration of performancepoint services in sharepoint,performancepoint assemblies used in development,performancepoint custom data sources,performancepoint custom filters,performancepoint custom reports,performancepoint custom scorecard transforms,performancepoint development scenarios,performancepoint services development,performancepoint services development scenarios,performancepoint services programming,performancepoint services sdk,pps custom dashboards in SharePoint,pps development,pps programming,pps sdk,report creation in SharePoint,report renderer in SharePoint,SharePoint service application PerformancePoint
ms.prod: sharepoint
ms.assetid: fb159708-d6b4-40c1-b5cc-4bb2071a7930
ms.openlocfilehash: ce0a29e9adba8e1606088444a2189f2f62bc4301
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="performancepoint-services-in-sharepoint"></a><span data-ttu-id="0c84f-103">PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-103">PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="0c84f-104">In diesem Artikel werden die unterstützten Entwicklungsszenarien für die PerformancePoint-Dienste in SharePoint beschrieben sowie deren Erweiterbarkeitsarchitektur.</span><span class="sxs-lookup"><span data-stu-id="0c84f-104">Learn about supported development scenarios and the extensibility architecture for PerformancePoint Services in SharePoint.</span></span>
<span data-ttu-id="0c84f-105">Bei den PerformancePoint-Diensten handelt es sich um SharePoint-Dienstanwendungen.</span><span class="sxs-lookup"><span data-stu-id="0c84f-105">PerformancePoint Services is a SharePoint service application.</span></span> <span data-ttu-id="0c84f-106">Mit ihrer Hilfe können Benutzer Business Intelligence-Dashboards (BI-Dashboards) erstellen, die Einblick in die Leistung einer Organisation gewähren.</span><span class="sxs-lookup"><span data-stu-id="0c84f-106">It enables users to create business intelligence (BI) dashboards that provide insight into an organization's performance.</span></span> <span data-ttu-id="0c84f-107">Dabei kann der native Funktionsumfang der PerformancePoint-Dienste um benutzerdefinierte Berichte, Filter, tabellarische Datenquellen und Scorecardtransformationen erweitert werden.</span><span class="sxs-lookup"><span data-stu-id="0c84f-107">You can create custom reports, filters, tabular data sources, and scorecard transforms to extend the native functionality of PerformancePoint Services.</span></span> <span data-ttu-id="0c84f-108">So können Sie beispielsweise eine benutzerdefinierte Berichtsvisualisierung speziell für die Medizinbranche erstellen und in eine wiederverwendbare vertikale Lösung integrieren.</span><span class="sxs-lookup"><span data-stu-id="0c84f-108">For example, you can create a custom report visualization that is optimized for the medical industry and then integrate it into a reusable vertical solution.</span></span>
  
    
    


## <a name="custom-performancepoint-services-reports-filters-and-tabular-data-sources-in-sharepoint"></a><span data-ttu-id="0c84f-109">Benutzerdefinierte Berichte, Filter und tabellarische Datenquellen in den PerformancePoint-Diensten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-109">Custom PerformancePoint Services reports, filters, and tabular data sources in SharePoint</span></span>
<span data-ttu-id="0c84f-110"><a name="bkmk_CreateCustomObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="0c84f-110"><a name="bkmk_CreateCustomObjects"> </a></span></span>

<span data-ttu-id="0c84f-p102">Sie können systemeigene PerformancePoint-Dienste  [ReportView](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx) , [Filter](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx) und tabellarischen [DataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx) Objekte erweitern, indem Sie benutzerdefinierte Werte für deren Eigenschaften definieren. Benutzerdefinierte Berichte, Filter und tabellarischen Datenquellenerweiterungen umfassen in der Regel drei Komponenten: ein Renderer oder Anbieter, ein Editor-Anwendung und Erweiterungsmetadaten.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p102">You can extend native PerformancePoint Services  [ReportView](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx) , [Filter](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx) , and tabular [DataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx) objects by defining custom values for their properties. Custom report, filter, and tabular data source extensions typically include three components: a renderer or provider, an editor application, and extension metadata.</span></span>
  
    
    

### <a name="renderers-and-providers-for-performancepoint-services-extensions"></a><span data-ttu-id="0c84f-113">Renderer und Anbietern für PerformancePoint-Dienste-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="0c84f-113">Renderers and providers for PerformancePoint Services extensions</span></span>

<span data-ttu-id="0c84f-p103">Der Typ des Objekts, die Sie erweitern bestimmt, ob es ein Renderer oder ein Anbieter verwendet wird. Berichts- und Erweiterungen Renderern verwenden, und Filtern und Datenquellenerweiterungen verwenden Anbieter.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p103">The type of object that you are extending determines whether it uses a renderer or a provider. Report and filter extensions use renderers, and filter and data source extensions use providers.</span></span>
  
    
    

- <span data-ttu-id="0c84f-116">Bei Berichterweiterungen ist für die Berichtvisualisierung ein Renderer erforderlich.</span><span class="sxs-lookup"><span data-stu-id="0c84f-116">Report extensions require a renderer for the report visualization.</span></span> 
    
  
- <span data-ttu-id="0c84f-p104">Filtererweiterungen erforderlich für das Steuerelement zur Auswahl ein Renderer. Renderer kann eines benutzerdefinierten Renderers oder einer systemeigenen PerformancePoint-Dienste Renderer sein. Wenn Sie einen PerformancePoint-Dienste Renderer verwenden, registrieren Sie einfach in der Erweiterung. Wenn Sie einen benutzerdefinierten Renderer verwenden, müssen Sie auch in der Erweiterung einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p104">Filter extensions require a renderer for the selection control. The renderer can be a custom renderer or a native PerformancePoint Services renderer. If you are using a PerformancePoint Services renderer, you simply register it in your extension. If you are using a custom renderer, you must also include it in your extension.</span></span>
    
  
- <span data-ttu-id="0c84f-121">Filtererweiterungen erfordern einen Verbindung mit der zugrunde liegenden Datenquelle Datenanbieter.</span><span class="sxs-lookup"><span data-stu-id="0c84f-121">Filter extensions require a data provider to connect to the underlying data source.</span></span>
    
  
- <span data-ttu-id="0c84f-122">Bei Datenquellenerweiterungen ist zum Herstellen der Verbindung mit der zugrunde liegenden Datenquelle ein Anbieter erforderlich.</span><span class="sxs-lookup"><span data-stu-id="0c84f-122">Data source extensions require a provider to connect to the underlying data source.</span></span>
    
  
<span data-ttu-id="0c84f-123">Weitere Informationen finden Sie unter den folgenden Themen zum Erstellen von Renderern und Anbieter:</span><span class="sxs-lookup"><span data-stu-id="0c84f-123">For more information, see the following topics about creating renderers and providers:</span></span>
  
    
    

-  [<span data-ttu-id="0c84f-124">Vorgehensweise: Erstellen von berichtsrenderern für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-124">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0c84f-125">Vorgehensweise: Erstellen Filter von Datenanbietern für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-125">How to: Create filter data providers for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0c84f-126">How to: Create tabular data source providers for PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-126">How to: Create tabular data source providers for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sha.md)
    
  

### <a name="editor-applications-for-performancepoint-services-extensions-in-sharepoint"></a><span data-ttu-id="0c84f-127">Editoranwendungen für PerformancePoint-Dienste-Erweiterungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-127">Editor applications for PerformancePoint Services extensions in SharePoint</span></span>

<span data-ttu-id="0c84f-p105">Benutzerdefinierte Editoren können Benutzer Eigenschaften für ein benutzerdefiniertes Objekt definieren, interagieren Sie mit Objekten im Repository und Endpunkte für benutzerdefinierte Berichte und Filter zu initialisieren. Editor sollte die Eigenschaften verfügbar machen, die Sie Aktivieren von Benutzern anzeigen und ändern möchten. Editoren können von Objekten in PerformancePoint Dashboard-Designer oder Elemente in der PerformancePoint-Inhaltsliste oder PerformancePoint-Datenverbindungsbibliothek geöffnet werden. Um in die für die Webseitenerstellung Dashboard-Designer integrieren, muss der Editor aus einen uniform Resource Identifier (URI) zu öffnen und der URI muss für die benutzerdefiniertes Objekt in der web.config-Datei PerformancePoint-Dienste registriert werden.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p105">Custom editors enable users to define properties for a custom object, interact with objects in the repository, and initialize endpoints for custom reports and filters. Your editor should expose the properties that you want to enable users to view and modify. Editors can be opened from objects in PerformancePoint Dashboard Designer or from items in the PerformancePoint Content List or PerformancePoint Data Connections Library. To integrate into the Dashboard Designer authoring experience, your editor must be able to open from a uniform resource identifier (URI), and the URI must be registered for the custom object in the PerformancePoint Services web.config file.</span></span>
  
    
    
<span data-ttu-id="0c84f-132">Weitere Informationen zum Erstellen von Editoren finden Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="0c84f-132">For more information about creating editors, see the following topics:</span></span>
  
    
    

-  [<span data-ttu-id="0c84f-133">Vorgehensweise: erstellen Bericht-Editoren für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-133">How to: Create report editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0c84f-134">Vorgehensweise: Erstellen Filter-Editoren für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-134">How to: Create filter editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0c84f-135">How to: Create tabular data source editors for PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-135">How to: Create tabular data source editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
> [!NOTE]
> <span data-ttu-id="0c84f-136">Mit PerformancePoint Dashboard-Designer können Sie Objekte erstellen und löschen. Ihr Editor muss also keine Logik zum Erstellen oder Löschen von Objekten bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0c84f-136">Note: PerformancePoint Dashboard Designer can create and delete custom objects, so your editor does not need to provide logic for creating or deleting objects.</span></span> 
  
    
    


### <a name="configuration-metadata-for-performancepoint-services-extensions-in-sharepoint"></a><span data-ttu-id="0c84f-137">Konfigurationsmetadaten für PerformancePoint-Dienste-Erweiterungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-137">Configuration metadata for PerformancePoint Services extensions in SharePoint</span></span>

<span data-ttu-id="0c84f-p106">Sie müssen während des Installationsvorgangs Metadaten für die Erweiterung in der PerformancePoint-Dienste web.config-Datei angeben. Die Metadaten enthält **type**, **subType**, **RendererClass**, **EditorURI**und **Resources** Attribute.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p106">You must specify metadata for your extension in the PerformancePoint Services web.config file during the installation process. The metadata includes **type**, **subType**, **RendererClass**, **EditorURI**, and **Resources** attributes.</span></span>
  
    
    
<span data-ttu-id="0c84f-p107">Zum Erstellen eines benutzerdefinierten Objekts Dashboard-Designer Ruft Metadaten für das Objekt aus der PerformancePoint-Dienste web.config-Datei und dann das Objekt als einen Inhaltstyp im Repository Dashboard-Designer erstellt. Nach dem Erstellen des benutzerdefinierten Objekts zeigt Dashboard-Designer eine Verknüpfung zum-Editor.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p107">To create a custom object, Dashboard Designer retrieves the object's metadata from the PerformancePoint Services web.config file and then creates the object as a content type in the Dashboard Designer repository. After creating the custom object, Dashboard Designer displays a link to the editor.</span></span>
  
    
    
<span data-ttu-id="0c84f-142">Weitere Informationen zu Erweiterungsmetadaten finden Sie unter [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c84f-142">For more information about extension metadata, see  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="custom-transforms-for-performancepoint-services-scorecards-in-sharepoint"></a><span data-ttu-id="0c84f-143">Benutzerdefinierte Transformationen für PerformancePoint-Dienste-Scorecards in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-143">Custom transforms for PerformancePoint Services scorecards in SharePoint</span></span>
<span data-ttu-id="0c84f-144"><a name="bkmk_CreateCustomObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="0c84f-144"><a name="bkmk_CreateCustomObjects"> </a></span></span>

<span data-ttu-id="0c84f-p108">Transformationen Ändern der Darstellung, den Inhalt oder die Funktionalität der Scorecards vor Abfragen der Datenquelle nach Abfragen der Datenquelle oder vor dem Rendern der Scorecard im Webpart. Beispielsweise PerformancePoint-Dienste Transformationen verwendet, um verschiedene Vorgänge ausführen, vor dem Rendern einer Scorecardansicht, z. B. das benannte Mengen, erweitern computing Rollups und Netzwerke Aggregations. Diese Änderungen werden während der Laufzeit angewendet, und sie die Definition des scorecardobjekts nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p108">Transforms change the appearance, contents, or functionality of scorecards before querying the data source, after querying the data source, or before rendering the scorecard in the Web Part. For example, PerformancePoint Services uses transforms to perform several operations before rendering a scorecard view, such as expanding named sets, computing rollups, and computing aggregations. These changes are applied at run time and they do not modify the definition of the scorecard object.</span></span>
  
    
    
<span data-ttu-id="0c84f-148">Weitere Informationen zu Scorecardtransformationen finden Sie unter [Gewusst wie: Erstellen von Scorecardtransformationen für PerformancePoint-Dienste in SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="0c84f-148">For more information about scorecard transforms, see  [How to: Create scorecard transforms for PerformancePoint Services in SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="0c84f-p109">Wenn eine Transformation die Datenwerte einer Scorecard ändert, werden die Änderungen direkt in Strategiekartenberichte eingefügt, die die Scorecard als Datenquelle verwenden. Darüber hinaus können sich Änderungen an Scorecards auf KPI-Detailberichte auswirken.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p109">If a transform modifies the data values in a scorecard, the changes propagate directly to Strategy Map reports that use the scorecard as a data source. In addition, changes to scorecards may affect KPI Details reports.</span></span> 
  
    
    


## <a name="extensibility-architecture-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="0c84f-151">Erweiterbarkeitsarchitektur der PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c84f-151">Extensibility architecture for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="0c84f-152"><a name="bkmk_PerfPointArch"> </a></span><span class="sxs-lookup"><span data-stu-id="0c84f-152"><a name="bkmk_PerfPointArch"> </a></span></span>

<span data-ttu-id="0c84f-153">Unterstützte Anwendungserweiterungen führen innerhalb einer Anwendungsinstanz PerformancePoint-Dienste, auf dem Front-End-Webserver oder auf dem Anwendungsserver aus, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="0c84f-153">Supported extensions run within a PerformancePoint Services application instance, either on the front-end web server or on the application server, as shown in the following diagram.</span></span>
  
    
    

<span data-ttu-id="0c84f-154">**Abbildung 1. Erweiterbarkeitsarchitektur von PerformancePoint Services**</span><span class="sxs-lookup"><span data-stu-id="0c84f-154">**Figure 1. PerformancePoint Services extensibility architecture**</span></span>

  
    
    

  
    
    
![Erweiterungspunkte der PerformancePoint-Dienste](../images/SPS14_PerfPoint_ArchOverview.gif)
  
    
    

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-front-end-web-server"></a><span data-ttu-id="0c84f-156">Auf dem SharePoint-Front-End-Webserver ausgeführte PerformancePoint-Dienste-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="0c84f-156">PerformancePoint Services extensions that run on the SharePoint front-end web server</span></span>

<span data-ttu-id="0c84f-p110">Benutzerdefinierte Editoren (und andere unterstützten benutzerdefinierten Anwendungen) auf dem Front-End-Webserver in einer Instanz einer Anwendung PerformancePoint-Dienste ausführen. Editoren sind in der Regel als ASPX-Seiten bereitgestellt und in den Pfad  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`installiert sind. Editoren rufen das  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) oder [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) -Objekt für den Autor oder Prozesskonto Content wie folgt:</span><span class="sxs-lookup"><span data-stu-id="0c84f-p110">Custom editors (and other supported custom applications) run on the front-end web server within a PerformancePoint Services application instance. Editors are typically deployed as .aspx pages and are installed in the path  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`. Editors call the  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) object or [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) object to author or process content, as follows:</span></span>
  
    
    

- <span data-ttu-id="0c84f-160">Berichts- und Filterobjekte sollten  [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) für alle Repository-Vorgänge verwenden.</span><span class="sxs-lookup"><span data-stu-id="0c84f-160">Report and filter objects should use  [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) for all repository tasks.</span></span>
    
  
- <span data-ttu-id="0c84f-p111">Datenquellenobjekte sollten  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) verwenden, um **Create** und **Update** Aufgaben ausführen, damit diese Aufgaben im Kontext der PerformancePoint-Dienste-Anwendung ausgeführt werden. **Read** (get) und **Delete** Aufgaben mithilfe von [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) oder [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) ausgeführt werden können. (Allerdings können benutzerdefinierte Datenquelle Anwendungen, die auf dem Anwendungsserver ausgeführt [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) direkt aufrufen.)</span><span class="sxs-lookup"><span data-stu-id="0c84f-p111">Data source objects should use  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) to perform **Create** and **Update** tasks so that these tasks are performed within the context of the PerformancePoint Services service application. **Read** (get) and **Delete** tasks can be performed by using [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) or [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) . (However, custom data source applications that run on the application server can call [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) directly.)</span></span>
    
  

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-application-server"></a><span data-ttu-id="0c84f-164">Auf dem SharePoint-Anwendungsserver ausgeführte PerformancePoint-Dienste-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="0c84f-164">PerformancePoint Services extensions that run on the SharePoint application server</span></span>

<span data-ttu-id="0c84f-p112">Benutzerdefinierte Renderer, Anbieter und scorecardtransformationen auf dem Anwendungsserver ausgeführt. Der Anwendungsserver gehostet wird, die Middle-Tier-Geschäftslogik für die PerformancePoint-Dienste-Instanz.</span><span class="sxs-lookup"><span data-stu-id="0c84f-p112">Custom renderers, providers, and scorecard transforms run on the application server. The application server hosts the middle-tier business logic for the PerformancePoint Services instance.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="0c84f-167">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="0c84f-167">See also</span></span>
<span data-ttu-id="0c84f-168"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="0c84f-168"><a name="bkmk_AdditionalResources"> </a></span></span>


-  <span data-ttu-id="0c84f-169">[Grundlagen der PerformancePoint Services-Entwicklung](http://msdn.microsoft.com/library/5d2c183b-95f8-4930-b6d0-f3ffe1ee166e%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c84f-169">[Fundamentals of PerformancePoint Services Development](http://msdn.microsoft.com/library/5d2c183b-95f8-4930-b6d0-f3ffe1ee166e%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="0c84f-170">[Codebeispiele für PerformancePoint Services in SharePoint Server 2010](http://msdn.microsoft.com/library/97f0cbd4-03ef-44f8-9869-699df9d9c97f%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c84f-170">[Code Samples for PerformancePoint Services in SharePoint Server 2010](http://msdn.microsoft.com/library/97f0cbd4-03ef-44f8-9869-699df9d9c97f%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="0c84f-171">[Problembehandlung und FAQs für PerformancePoint Services-Entwicklung](http://msdn.microsoft.com/library/a90156e2-0522-46a1-9fc9-b6c8d2fffad7%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c84f-171">[Troubleshooting and FAQs for PerformancePoint Services Development](http://msdn.microsoft.com/library/a90156e2-0522-46a1-9fc9-b6c8d2fffad7%28Office.15%29.aspx)</span></span>
    
  

