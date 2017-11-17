---
title: "Neuerungen für Entwickler in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 068d0b99-1762-42de-b6c9-acb1cffc6e31
ms.openlocfilehash: 07e78edc42f4c9277047950a3a8554917a1f4e91
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-for-developers-in-sharepoint"></a>Neuerungen für Entwickler in SharePoint
Informationen zu den Features und Funktionen in SharePoint, einschließlich des neuen Cloud-Add-In-Modells, der Entwicklungstools, Plattformverbesserungen, mobilen Add-Ins und vieles mehr.
## <a name="cloud-add-in-model"></a>Cloud-Add-In-Modell
<a name="bmSpApps"> </a>

SharePoint führt ein Cloud-Add-In-Modell ein, mit dem Sie Add-Ins erstellen können. Ein SharePoint-Add-In ist eine eigenständige Funktion, die die Funktionen von SharePoint-Websites erweitert. Ein Add-In kann SharePoint-Komponenten wie Listen, Workflows und Seiten der Website enthalten, aber es kann auch eine Remote-Webanwendung und Remotedaten in SharePoint zum Vorschein bringen. Ein Add-In hat nur wenige oder keine Abhängigkeiten von einer anderen Software auf dem Gerät oder der Plattform, wo es installiert ist, außer dem, was in die Plattform integriert ist. Aufgrund dieses Merkmals können Add-Ins einfach installiert und sauber deinstalliert werden. Add-Ins haben keinen benutzerdefinierten Code, der auf SharePoint-Servern ausgeführt wird. Stattdessen wird die gesamte benutzerdefinierte Logik „nach oben“ in die Cloud oder „nach unten“ auf Clientcomputer verschoben. Darüber hinaus führt SharePoint ein innovatives Bereitstellungsmodell für SharePoint-Add-Ins ein, das Komponenten wie Office Store und den Add-In-Katalog enthält.

<a href="../sp-add-ins/sharepoint-add-ins.md"><img alt="SharePoint Add-ins" src="../images/wn_cloud_1.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md"><img alt="SharePoint Store" src="../images/wn_cloud_2.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md"><img alt="Add-ins Catalog" src="../images/wn_cloud_3.png" /></a>

## <a name="familiar-programming-model-using-web-standards"></a>Vertrautes Programmiermodell mithilfe von Webstandards
<a name="bmWebStandards"> </a>

Mit SharePoint kann jeder Webentwickler, auch jene, die auf Nicht-Microsoft-Plattformstapeln arbeiten, SharePoint-Lösungen erstellen. Dies ist möglich, da SharePoint auf den üblichen Webstandards wie HTML, CSS und JavaScript basiert. Die Implementierung stützt sich außerdem auf eingeführte Protokolle wie OData und OAuth.
  

  <a href="../sp-add-ins/sharepoint-add-ins.md"><img alt="HTML/JavaScript" src="../images/wn_WebStandards_1.png" /></a>&nbsp;&nbsp;<a href="using-odata-sources-with-business-connectivity-services-in-sharepoint.md"><img alt="OData" src="../images/wn_WebStandards_2.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/get-to-know-the-sharepoint-rest-service.md" target="_blank"><img alt="REST" src="../images/wn_WebStandards_3.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/authorization-and-authentication-of-sharepoint-add-ins.md"><img alt="OAuth" src="../images/wn_WebStandards_4.png" /></a>


## <a name="development-tools"></a>Entwicklungstools
<a name="bmDevTools"> </a>

Die aktuelle Version zeigt die enormen Schritte, die für die Optimierung der vorhandenen Entwicklungstools wie Visual Studio und SharePoint Designer unternommen wurden. Daneben wurde auch das neu entwickelte webbasierte Tool Napa Office 365-Entwicklungstools zur Entwicklung von Add-Ins bereitgestellt. Mit dem neuen vereinheitlichten Projektsystem Visual Studio können Sie SharePoint-Add-Ins, Office-Add-Ins und SharePoint-Add-Ins entwickeln, die Office-Add-Ins oder Office-Add-Ins beinhalten, welche von SharePoint gehostet werden. Zusätzlich zu den SharePoint-Projektvorlagen aus früheren Versionen enthält Visual Studio 2012 nun eine neue Add-In-Projektvorlage im Ordner „Add-Ins" namens Add-Ins für SharePoint. Dem Fenster „Eigenschaften" und den Eigenschaftenseiten wurden einige neue Eigenschaften zur Unterstützung von SharePoint-Add-In-Projekten hinzugefügt. Weitere Verbesserungen betreffen umfassende Unterstützung der Entwicklung des Cloud-Add-In-Modells, einschließlich OData- und OAuth-Unterstützung, sowie umfassende Unterstützung der Workflow-Manager-Client 1.0-Plattformentwicklung.

<a href="https://dev.office.com/docs/add-ins/overview/office-add-ins" target="_blank"><img alt="Napa Office 365 Development Tools" src="../images/wn_DevTools_1.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/what-s-new-in-office-developer-tools-for-visual-studio.md"><img alt="Visual Studio" src="../images/wn_DevTools_2.png" /></a>&nbsp;&nbsp;<a href="workflow-development-in-sharepoint-designer-and-visio.md"><img alt="SharePoint Designer" src="../images/wn_DevTools_3.png" /></a>

## <a name="core-platform-enhancements"></a>Zentrale Plattformverbesserungen
<a name="bmPlatformEnhance"> </a>

SharePoint wurde für die Unterstützung der neuen cloudbasierten Architektur und des app-gesteuerten Entwicklungsframework umfassend verbessert und optimiert. Angefangen bei den SharePoint-APIs auf der untersten Ebene, über Konnektivität bis hin zu Integration sozialer Medien ist SharePoint dafür ausgelegt, eine komplette Anwendungsentwicklungsumgebung zu unterstützen. Neben der Verwendung von REST-Endpunkten (Representational State Transfer) für Webdienste, gibt es auch eine neue API für die Server- und die Cliententwicklung. Remoteereignisempfänger werden jetzt auch neben dem clientseitigen Rendering unterstützt. 
  
<a href="https://msdn.microsoft.com/library/fp161347.aspx" target="_blank"><img alt="REST endpoints" src="../images/wn_Platform_1.png" /></a>&nbsp;&nbsp;<a href="choose-the-right-api-set-in-sharepoint.md"><img alt="New client and server APIs" src="../images/wn_Platform_2.png" /></a>&nbsp;&nbsp;<a href="how-to-customize-a-field-type-using-client-side-rendering.md"><img alt="Client-side rendering" src="../images/wn_Platform_3.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/handle-events-in-sharepoint-add-ins.md"><img alt="Remote event receivers" src="../images/wn_Platform_4.png" /></a>

    
    
    

## <a name="mobility"></a>Mobilität
<a name="bmMobility"> </a>

SharePoint ermöglicht Ihnen, Windows Phone 7-Anwendungen mit lokalen SharePoint-Diensten und -Anwendungen bzw. mit in der Cloud ausgeführten Remote-SharePoint-Diensten und -Anwendungen (wie jene, die SharePoint Online verwenden) zu kombinieren, um leistungsfähige Anwendungen zu entwickeln, deren Funktionalität über die herkömmlichen Desktop- oder Laptopfunktionen hinausgehen und eine wirklich mobile und leichter zugängliche Umgebung schaffen. Die neuen Mobilitätsfeatures in SharePoint bauen auf vorhandenen Microsoft-Tools und -Technologien auf, wie SharePoint, Windows Phone 7, Visual Studio und Microsoft Silverlight. Sie können SharePoint-unterstützte mobile Anwendungen für Windows Phone mit dem neuen SharePoint Phone-Anwendungsassistenten Visual Studio für einfache listenbasierte mobile Anwendungen erstellen. Sie können die neuen Features aus SharePoint, wie den Geolocation-Feldtyp, integrieren und Mitteilungen von SharePoint Server mit Push auf Ihre mobilen Anwendungen übertragen.

<a href="overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md"><img alt="Visual Studio app templates" src="../images/wn_Mobility_.png" /></a>&nbsp;&nbsp;<a href="how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md"><img alt="Push notifications" src="../images/wn_Mobility_2.png" /></a>&nbsp;&nbsp;<a href="integrating-location-and-map-functionality-in-sharepoint.md"><img alt="Location and maps" src="../images/wn_Mobility_3.png" /></a>

## <a name="social-and-collaboration"></a>Soziale Netzwerke und Zusammenarbeit
<a name="bmSocial"> </a>

Neue und verbesserte Features für soziale Funktionen und Zusammenarbeit erleichtern den Benutzern die Kommunikation, damit sie immer auf dem Laufenden sind. Der verbesserte soziale Meine Website-Feed verbindet Menschen und lässt sie Inhalte tauschen. Das neue Feature Communitywebsite stellt den Benutzern eine reichhaltige Communityumgebung bereit, in der sie nicht nur schnell Informationen finden und teilen können, sondern auch auf Menschen mit gleichen Interessen treffen.

<a href="work-with-social-feeds-in-sharepoint.md"><img alt="Interactive feed" src="../images/wn_Social_1.png" /></a>&nbsp;&nbsp;<a href="what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab"><img alt="Community site" src="../images/wn_Social_2.png" /></a>&nbsp;&nbsp;<a href="follow-people-in-sharepoint.md"><img alt="Follow people" src="../images/wn_Social_3.png" /></a>&nbsp;&nbsp;<a href="follow-content-in-sharepoint.md"><img alt="Follow sites" src="../images/wn_Social_4.png" /></a>

## <a name="search"></a>Suche
<a name="bmSearch"> </a>

Die Suchfunktion in SharePoint enthält mehrere Verbesserungen, kundenspezifische Inhaltsverarbeitung mit dem Webdienst für Inhaltserweiterung und ein neues Framework für die Darstellung der Suchergebnistypen. Außerdem wurde bedeutende Verbesserungen bei der Sprache der Schlüsselwortabfrage (KQL) eingeführt.

<a href="custom-content-processing-with-the-content-enrichment-web-service-callout.md"><img alt="Consolidated search platform" src="../images/wn_search_1.png" /></a>&nbsp;&nbsp;<a href="what-s-new-in-sharepoint-search-for-developers.md"><img alt="Rich results framework" src="../images/wn_search_2.png" /></a>&nbsp;&nbsp;<a href="building-search-queries-in-sharepoint.md"><img alt="KQL enhnacements" src="../images/wn_search_3.png" /></a>

## <a name="workflows"></a>Workflows
<a name="bmWorkflow"> </a>

Workflow-Manager-Client 1.0 ist eine neu entworfene Workflowinfrastruktur, basierend auf Windows Workflow Foundation 4. Sie bringt dem Workflowauthoring in SharePoint mehr Leistungsstärke und Flexibilität. In einer vollständig deklarierten Authoringumgebung können IT-Arbeiter mit SharePoint Designer 2013 leistungsstarke Workflows nutzen. Mit einer Reihe neuer Visual Studio 2012-Workflowprojektvorlagen greifen Entwickler auf intelligentere Features, wie benutzerdefinierte Aktionen, zu. Der wichtigste Punkt aber ist, Workflow-Manager-Client 1.0 ist vollständig mit Modell für SharePoint-Add-Ins integriert. Workflows werden nicht in SharePoint ausgeführt, sondern in der Cloud. Dies bietet enorme Flexibilität bei der Entwicklung von workflowbasierten SharePoint-Add-Ins.

<a href="what-s-new-in-workflows-for-sharepoint.md"><img alt="Execute in the cloud" src="../images/wn_workflow_1.png" /></a>&nbsp;&nbsp;<a href="sharepoint-workflow-fundamentals.md"><img alt="Workflow 4-based infrastructure" src="../images/wn_workflow_2.png" /></a>&nbsp;&nbsp;<a href="workflow-development-in-sharepoint-designer-and-visio.md"><img alt="Declarative authoring" src="../images/wn_workflow_3.png" /></a>&nbsp;&nbsp;<a href="develop-sharepoint-workflows-using-visual-studio.md"><img alt="Designer and project templates" src="../images/wn_workflow_4.png" /></a>

## <a name="enterprise-content-management"></a>Enterprise Content Management
<a name="bmECM"> </a>

In SharePoint können Sie jetzt .NET-Client, Silverlight, Windows Phone und JavaScript APIs zusätzlich zu der erweiterten Gruppe von .NET-Server-verwalteten APIs verwenden, Um ECM-Bedienerfreundlichkeit und -Verhalten (Enterprise Content Management) anzupassen.

<a href="what-s-new-with-sharepoint-site-development.md"><img alt="Design Manager" src="../images/wn_ecm_1.png" /></a>&nbsp;&nbsp;<a href="managed-navigation-in-sharepoint.md"><img alt="Managed navigation" src="../images/wn_ecm_2.png" /></a>&nbsp;&nbsp;<a href="cross-site-publishing-in-sharepoint.md"><img alt="Cross-site publishing" src="../images/wn_ecm_3.png" /></a>&nbsp;&nbsp;<a href="ediscovery-in-sharepoint.md"><img alt="EDiscovery" src="../images/wn_ecm_4.png" /></a>

## <a name="business-connectivity-services"></a>Business Connectivity Services
<a name="bmBCS"> </a>

Business Connectivity Services (BCS) ermöglicht SharePoint, auf Daten aus externen Systemen, wie SAP, ERP und CRM, zuzugreifen, zusätzlich zu anderen datengesteuerten Anwendungen, die über WCF-Dienste oder OData-Endpunkte dargestellt werden. BCS in SharePoint wurde in vielfacher weise geändert und verbessert. Dazu zählen auch OData-Konnektivität, externe Ereignisse, externe Daten in Add-Ins, Filterung und Sortierung, REST-Unterstützung und anderes mehr.

<a href="using-odata-sources-with-business-connectivity-services-in-sharepoint.md"><img alt="OData connector" src="../images/wn_bcs_1.png" /></a>&nbsp;&nbsp;<a href="add-in-scoped-external-content-types-in-sharepoint.md"><img alt="External data in apps" src="../images/wn_bcs_2.png" /></a>&nbsp;&nbsp;<a href="external-events-and-alerts-in-sharepoint.md"><img alt="External events in SharePoint" src="../images/wn_bcs_3.png" /></a>

## <a name="application-services"></a>Anwendungsdienste
<a name="bmSpServices"> </a>

SharePoint umfasst verschiedene Dienste für das Arbeiten mit den Daten Ihrer SharePoint-Websites. Neu in SharePoint ist der maschinelle Übersetzungsdienst, der Webseiten, Dokumente und Datenströme in mehrere Sprachen übersetzt. SharePoint beinhaltet auch Access Services und ein neues Datenzugriffsmodell. Zum Konvertieren von Dateien und Datenströmen in andere Formate verfügt SharePoint über Word Automation Services und PowerPoint Automation Services (ein neues Feature für SharePoint). SharePoint bietet auch Tools zur Datenanalyse, z. B. PerformancePoint Services und Visio Services, Business Intelligence und leistungsfähigen neuen Features in Excel Services ermöglichen die einfache.

<a href="external-events-and-alerts-in-sharepoint.md"><img alt="Translation Services" src="../images/wn_appServices_1.png" /></a>&nbsp;&nbsp;<a href="powerpoint-automation-services-in-sharepoint.md"><img alt="PowerPoint Automation Services" src="../images/wn_appServices_2.png" /></a>&nbsp;&nbsp;<a href="what-s-new-in-access.md"><img alt="Enhanced Access Services" src="../images/wn_appServices_3.png" /></a>&nbsp;&nbsp;<a href="https://msdn.microsoft.com/library/fp161347.aspx" target="_blank"><img alt="Enhanced Excel Services" src="../images/wn_appServices_4.png" /></a>


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bm_Addres"> </a>


-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  
-  [Entwickeln von Add-Ins für SharePoint](../sp-add-ins/sharepoint-add-ins.md)
    
  
-  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Barrierefreiheit in SharePoint](accessibility-in-sharepoint.md)
    
  

