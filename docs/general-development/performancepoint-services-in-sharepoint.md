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
# <a name="performancepoint-services-in-sharepoint"></a>PerformancePoint-Dienste in SharePoint
In diesem Artikel werden die unterstützten Entwicklungsszenarien für die PerformancePoint-Dienste in SharePoint beschrieben sowie deren Erweiterbarkeitsarchitektur.
Bei den PerformancePoint-Diensten handelt es sich um SharePoint-Dienstanwendungen. Mit ihrer Hilfe können Benutzer Business Intelligence-Dashboards (BI-Dashboards) erstellen, die Einblick in die Leistung einer Organisation gewähren. Dabei kann der native Funktionsumfang der PerformancePoint-Dienste um benutzerdefinierte Berichte, Filter, tabellarische Datenquellen und Scorecardtransformationen erweitert werden. So können Sie beispielsweise eine benutzerdefinierte Berichtsvisualisierung speziell für die Medizinbranche erstellen und in eine wiederverwendbare vertikale Lösung integrieren.
  
    
    


## <a name="custom-performancepoint-services-reports-filters-and-tabular-data-sources-in-sharepoint"></a>Benutzerdefinierte Berichte, Filter und tabellarische Datenquellen in den PerformancePoint-Diensten in SharePoint
<a name="bkmk_CreateCustomObjects"> </a>

Sie können systemeigene PerformancePoint-Dienste  [ReportView]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx)) , [Filter]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx)) und tabellarischen [DataSource]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx)) Objekte erweitern, indem Sie benutzerdefinierte Werte für deren Eigenschaften definieren. Benutzerdefinierte Berichte, Filter und tabellarischen Datenquellenerweiterungen umfassen in der Regel drei Komponenten: ein Renderer oder Anbieter, ein Editor-Anwendung und Erweiterungsmetadaten.
  
    
    

### <a name="renderers-and-providers-for-performancepoint-services-extensions"></a>Renderer und Anbietern für PerformancePoint-Dienste-Erweiterungen

Der Typ des Objekts, die Sie erweitern bestimmt, ob es ein Renderer oder ein Anbieter verwendet wird. Berichts- und Erweiterungen Renderern verwenden, und Filtern und Datenquellenerweiterungen verwenden Anbieter.
  
    
    

- Bei Berichterweiterungen ist für die Berichtvisualisierung ein Renderer erforderlich. 
    
  
- Filtererweiterungen erforderlich für das Steuerelement zur Auswahl ein Renderer. Renderer kann eines benutzerdefinierten Renderers oder einer systemeigenen PerformancePoint-Dienste Renderer sein. Wenn Sie einen PerformancePoint-Dienste Renderer verwenden, registrieren Sie einfach in der Erweiterung. Wenn Sie einen benutzerdefinierten Renderer verwenden, müssen Sie auch in der Erweiterung einbeziehen.
    
  
- Filtererweiterungen erfordern einen Verbindung mit der zugrunde liegenden Datenquelle Datenanbieter.
    
  
- Bei Datenquellenerweiterungen ist zum Herstellen der Verbindung mit der zugrunde liegenden Datenquelle ein Anbieter erforderlich.
    
  
Weitere Informationen finden Sie unter den folgenden Themen zum Erstellen von Renderern und Anbieter:
  
    
    

-  [Vorgehensweise: Erstellen von berichtsrenderern für PerformancePoint Services in SharePoint](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen Filter von Datenanbietern für PerformancePoint Services in SharePoint](how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [How to: Create tabular data source providers for PerformancePoint Services in SharePoint](how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sha.md)
    
  

### <a name="editor-applications-for-performancepoint-services-extensions-in-sharepoint"></a>Editoranwendungen für PerformancePoint-Dienste-Erweiterungen in SharePoint

Benutzerdefinierte Editoren können Benutzer Eigenschaften für ein benutzerdefiniertes Objekt definieren, interagieren Sie mit Objekten im Repository und Endpunkte für benutzerdefinierte Berichte und Filter zu initialisieren. Editor sollte die Eigenschaften verfügbar machen, die Sie Aktivieren von Benutzern anzeigen und ändern möchten. Editoren können von Objekten in PerformancePoint Dashboard-Designer oder Elemente in der PerformancePoint-Inhaltsliste oder PerformancePoint-Datenverbindungsbibliothek geöffnet werden. Um in die für die Webseitenerstellung Dashboard-Designer integrieren, muss der Editor aus einen uniform Resource Identifier (URI) zu öffnen und der URI muss für die benutzerdefiniertes Objekt in der web.config-Datei PerformancePoint-Dienste registriert werden.
  
    
    
Weitere Informationen zum Erstellen von Editoren finden Sie unter den folgenden Themen:
  
    
    

-  [Vorgehensweise: erstellen Bericht-Editoren für PerformancePoint Services in SharePoint](how-to-create-report-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen Filter-Editoren für PerformancePoint Services in SharePoint](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [How to: Create tabular data source editors for PerformancePoint Services in SharePoint](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
> [!NOTE]
> Mit PerformancePoint Dashboard-Designer können Sie Objekte erstellen und löschen. Ihr Editor muss also keine Logik zum Erstellen oder Löschen von Objekten bereitstellen. 
  
    
    


### <a name="configuration-metadata-for-performancepoint-services-extensions-in-sharepoint"></a>Konfigurationsmetadaten für PerformancePoint-Dienste-Erweiterungen in SharePoint

Sie müssen während des Installationsvorgangs Metadaten für die Erweiterung in der PerformancePoint-Dienste web.config-Datei angeben. Die Metadaten enthält **type**, **subType**, **RendererClass**, **EditorURI**und **Resources** Attribute.
  
    
    
Zum Erstellen eines benutzerdefinierten Objekts Dashboard-Designer Ruft Metadaten für das Objekt aus der PerformancePoint-Dienste web.config-Datei und dann das Objekt als einen Inhaltstyp im Repository Dashboard-Designer erstellt. Nach dem Erstellen des benutzerdefinierten Objekts zeigt Dashboard-Designer eine Verknüpfung zum-Editor.
  
    
    
Weitere Informationen zu Erweiterungsmetadaten finden Sie unter [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)).
  
    
    

## <a name="custom-transforms-for-performancepoint-services-scorecards-in-sharepoint"></a>Benutzerdefinierte Transformationen für PerformancePoint-Dienste-Scorecards in SharePoint
<a name="bkmk_CreateCustomObjects"> </a>

Transformationen Ändern der Darstellung, den Inhalt oder die Funktionalität der Scorecards vor Abfragen der Datenquelle nach Abfragen der Datenquelle oder vor dem Rendern der Scorecard im Webpart. Beispielsweise PerformancePoint-Dienste Transformationen verwendet, um verschiedene Vorgänge ausführen, vor dem Rendern einer Scorecardansicht, z. B. das benannte Mengen, erweitern computing Rollups und Netzwerke Aggregations. Diese Änderungen werden während der Laufzeit angewendet, und sie die Definition des scorecardobjekts nicht ändern.
  
    
    
Weitere Informationen zu Scorecardtransformationen finden Sie unter [Gewusst wie: Erstellen von Scorecardtransformationen für PerformancePoint-Dienste in SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).
  
> [!NOTE]
> Wenn eine Transformation die Datenwerte einer Scorecard ändert, werden die Änderungen direkt in Strategiekartenberichte eingefügt, die die Scorecard als Datenquelle verwenden. Darüber hinaus können sich Änderungen an Scorecards auf KPI-Detailberichte auswirken. 
  
    
    


## <a name="extensibility-architecture-for-performancepoint-services-in-sharepoint"></a>Erweiterbarkeitsarchitektur der PerformancePoint-Dienste in SharePoint
<a name="bkmk_PerfPointArch"> </a>

Unterstützte Anwendungserweiterungen führen innerhalb einer Anwendungsinstanz PerformancePoint-Dienste, auf dem Front-End-Webserver oder auf dem Anwendungsserver aus, wie in der folgenden Abbildung dargestellt.
  
    
    

**Abbildung 1. Erweiterbarkeitsarchitektur von PerformancePoint Services**

  
    
    

  
    
    
![Erweiterungspunkte der PerformancePoint-Dienste](../images/SPS14_PerfPoint_ArchOverview.gif)
  
    
    

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-front-end-web-server"></a>Auf dem SharePoint-Front-End-Webserver ausgeführte PerformancePoint-Dienste-Erweiterungen

Benutzerdefinierte Editoren (und andere unterstützten benutzerdefinierten Anwendungen) auf dem Front-End-Webserver in einer Instanz einer Anwendung PerformancePoint-Dienste ausführen. Editoren sind in der Regel als ASPX-Seiten bereitgestellt und in den Pfad  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`installiert sind. Editoren rufen das  [BIMonitoringServiceApplicationProxy]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx)) oder [SPDataStore]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx)) -Objekt für den Autor oder Prozesskonto Content wie folgt:
  
    
    

- Berichts- und Filterobjekte sollten  [SPDataStore]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx)) für alle Repository-Vorgänge verwenden.
    
  
- Datenquellenobjekte sollten  [BIMonitoringServiceApplicationProxy]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx)) verwenden, um **Create** und **Update** Aufgaben ausführen, damit diese Aufgaben im Kontext der PerformancePoint-Dienste-Anwendung ausgeführt werden. **Read** (get) und **Delete** Aufgaben mithilfe von [BIMonitoringServiceApplicationProxy]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx)) oder [SPDataStore]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx)) ausgeführt werden können. (Allerdings können benutzerdefinierte Datenquelle Anwendungen, die auf dem Anwendungsserver ausgeführt [SPDataStore]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx)) direkt aufrufen.)
    
  

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-application-server"></a>Auf dem SharePoint-Anwendungsserver ausgeführte PerformancePoint-Dienste-Erweiterungen

Benutzerdefinierte Renderer, Anbieter und scorecardtransformationen auf dem Anwendungsserver ausgeführt. Der Anwendungsserver gehostet wird, die Middle-Tier-Geschäftslogik für die PerformancePoint-Dienste-Instanz.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bkmk_AdditionalResources"> </a>


-  [Grundlagen der PerformancePoint Services-Entwicklung]((http://msdn.microsoft.com/library/5d2c183b-95f8-4930-b6d0-f3ffe1ee166e%28Office.15%29.aspx))
    
  
-  [Codebeispiele für PerformancePoint Services in SharePoint Server 2010]((http://msdn.microsoft.com/library/97f0cbd4-03ef-44f8-9869-699df9d9c97f%28Office.15%29.aspx))
    
  
-  [Problembehandlung und FAQs für PerformancePoint Services-Entwicklung]((http://msdn.microsoft.com/library/a90156e2-0522-46a1-9fc9-b6c8d2fffad7%28Office.15%29.aspx))
    
  

