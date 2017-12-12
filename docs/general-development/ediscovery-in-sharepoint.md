---
title: eDiscovery in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 45cb324a-75f5-444d-a0fa-5c223df19016
ms.openlocfilehash: 6e2a2d0d2088d8acb62aab9d16a13daad5fb8236
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="ediscovery-in-sharepoint"></a>eDiscovery in SharePoint
In diesem Artikel erhalten Sie Informationen zu eDiscovery-Features in SharePoint. Mit eDiscovery können Anwälte auf Inhalte in elektronischer Form zugreifen.
## <a name="introduction-to-ediscovery-in-sharepoint"></a>Einführung in eDiscovery in SharePoint
<a name="SP15_eDiscoveryInSP_IntroductionToeDiscovery"> </a>

eDiscovery beschreibt den Prozess, wie Datensatzverwalter und Anwälte mit Inhalten in elektronischer Form arbeiten. In der Regel umfasst eDiscovery das Durchsuchen von Dokumenten, Websites und E-Mail-Nachrichten, die auf Laptops, E-Mail-Servern, Dateiservern und weiteren Ressourcen enthalten sind, und das Sammeln von und Arbeiten mit Inhalten, die den Kriterien für einen bestimmten Rechtsfall entsprechen.
  
    
    
In SharePoint Server 2010 hat Microsoft das Archiv- und eDiscovery-Feature eingeführt, mit dem beliebige Websites in ein Archiv verschoben werden und die Benutzer somit diese nicht löschen oder bearbeiten können. In Exchange 2010 wurde eine Möglichkeit eingeführt, eine gesetzliche Aufbewahrungspflicht auf Postfächer anzuwenden, mehrere Postfächer zu durchsuchen und ein Windows PowerShell-Cmdlet zum Exportieren von Postfächern zu verwenden.
  
    
    
eDiscovery in SharePoint und umfasst neue Möglichkeiten zur Senkung von Kosten und Komplexität von Suchprozessen. Diese umfassen:
  
    
    

- **Das eDiscovery Center**, eine zentrale SharePoint-Website, mit der das Archivieren, die Suche und der Export von in Exchange und SharePoint in SharePoint-Farmen und auf Exchange-Servern gespeicherten Inhalten verwaltet werden kann.
    
  
- **Das SharePoint-In-Situ-Archiv**, in dem vollständige SharePoint-Websites enthalten sind. Das In-Situ-Archiv schützt alle Dokumente, Seiten und Listenelemente auf der Website, ermöglicht es jedoch Benutzern, die Inhalte weiterhin zu ändern und zu löschen. 
    
  
- **Das Exchange-In-Situ-Archiv**, in dem Exchange-Postfächer enthalten sind. Das In-Situ-Archiv schützt alle Postfachinhalte über die gleiche Benutzeroberfläche und die APIs, die zum Aufbewahren von SharePoint-Websites verwendet werden.
    
  
- Mit der **abfragebasierten Speicherung** können Benutzer Abfragefilter auf Exchange-Postfächer und SharePoint-Websites anwenden und den gespeicherten Inhalt einschränken.
    
  

## <a name="how-ediscovery-works-in-sharepoint"></a>Funktionsweise von eDiscovery in SharePoint
<a name="SP15_eDiscoveryInSP_HoweDiscoveryWorks"> </a>

eDiscovery nutzt Suchdienstanwendungen zum Durchforsten von SharePoint-Farmen. Sie können Suchanwendungen auf unterschiedliche Weisen konfigurieren, die häufigste ist jedoch die Verwendung einer zentralen Suchdienstfarm, mit der mehrere SharePoint-Farmen durchforstet werden. Sie können diesen Suchdienst zum Durchforsten aller SharePoint-Inhalte oder bestimmter Regionen verwenden, z. B. aller Inhalte in Europa.
  
    
    
Beim Durchforsten einer SharePoint-Farm verwendet die Suche zunächst einen Dienstanwendungsproxy, mit dem eine Verbindung hergestellt wird. Das eDiscovery Center nutzt die Proxyverbindung zum Senden von Aufbewahrungen an SharePoint-Websites in anderer SharePoint-Farmen.
  
    
    

## <a name="prerequisites"></a>Voraussetzungen
<a name="SP15_eDiscoveryInSP_Prerequisites"> </a>

Vor dem Bereitstellten von SharePoint Server-eDiscovery-Features sollten Sie die Infrastruktur der Suchdienstanwendung für Ihre Organisation planen. Wenn Sie z. B. zwei getrennte Suchdienstanwendungen haben, die jeweils bestimmte SharePoint-Websites durchforsten, benötigen Sie ein eDiscovery Center für jede Suchdienstanwendung.
  
    
    

## <a name="site-holds"></a>Websitearchiv
<a name="SP15_eDiscoveryInSP_SiteHolds"> </a>

SharePoint bewahrt Inhalte auf Websiteebene auf. Wenn Sie eine Website archivieren, werden die zugehörigen Listen, Bibliotheken und Unterwebsites aufbewahrt. Wenn Sie eine Stammwebsitesammlung archivieren, werden alle Dokumente, Seiten, Listen und Unterwebsites in dieser Websitesammlung aufbewahrt.
  
    
    
Erstellen Sie zum Archivieren einer Website einen Discovery-Fall im eDiscovery Center. Ein Fall ist ein Container für alle Abfragen, Inhalte und Aufbewahrungen, die mit einem Rechtstreit zusammenhängen. Erstellen Sie, nachdem Sie den Fall erstellt haben, ein Discoveryset, um die Website anzugeben. Geben Sie zum Prüfen der Website ihre URL-Adresse ein.
  
    
    
In-Situ-Archiv ruft die Inhalte dort ab, wo sie sich nach Abschluss der Discoverysuche befinden. Wenn Inhaltselemente bearbeitet oder gelöscht werden, platziert eDiscovery eine Kopie des Elements in einer bestimmten Dokumentbibliothek, dem permanenten Dokumentarchiv, auf der SharePoint-Website, auf der der Inhalt bearbeitet wurde.
  
    
    
Um Inhalte so zu archivieren, dass Speicherplatz minimiert und Effizienz maximiert wird, verwendet eDiscovery die Funktion Kopie bei Schreibvorgang zum Verwalten identischer Kopien der gleichen Informationen. Da der Großteil der Inhalte im Archiv nicht mehr bearbeitet wird, besteht kein Grund, eine Kopie davon zu erstellen. Stattdessen werden nur Kopien von Elementen erstellt, wenn diese gelöscht werden, oder wenn Sie seit der Archivierung geändert werden. Wenn ein Dokument erneut geändert wird, behält eDiscovery nur die aktuelle eingecheckte oder gelöschte Version und die Version, die zum Zeitpunkt der ursprünglichen Archivierung erstellt wurde bei.
  
    
    
Wenn eine Website mehrfach archiviert wird, wird die nächste Bearbeitung eines Dokuments erneut kopiert, obwohl das Dokument ggf. bereits bei der ersten Archivierung kopiert wurde.
  
    
    

## <a name="ediscovery-programming-model"></a>eDiscovery-Programmierungsmodell
<a name="SP15_eDiscoveryInSP_eDiscoveryProgrammingModel"> </a>

SharePoint bietet ein Microsoft .NET-Serverprogrammierungsmodell, das Sie zum Erstellen von benutzerdefinierten Lösungen und Apps mit eDiscovery-Funktionen verwenden können. In Tabelle 1 werden die Typen im **Microsoft.Office.Server.Discovery**-Namespace aufgeführt.
  
    
    

**Tabelle 1. eDiscovery-Typen**


|**Typ**|**Beschreibung**|
|:-----|:-----|
| [Case](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.Case.aspx) <br/> |Stellt ein eDiscovery-Fall dar. Einem bestimmten  [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) -Objekt zugeordnet, kann ein Fall mithilfe eines bestimmten Datums oder einer bestimmten Aktion beendet werden. Fälle können Quellgruppen und Speicherorte in diesem **Case**-Objekt enthalten.  <br/> |
| [Custodian](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.Custodian.aspx) <br/> |Stellt die Person dar, die für die Aufbewahrung von Datensätzen für einen eDiscovery-Fall zuständig ist.  <br/> |
| [CustodianCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.CustodianCollection.aspx) <br/> |Steht für eine Auflistung von **Custodian**-Objekten. <br/> |
| **DiscoveryDuplicateSourceCollection** <br/> |Eine Ausnahme, die zurückgegeben wird, wenn der Wert des **Source**-Objekts nicht eindeutig ist. <br/> |
| [DiscoveryException](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.DiscoveryException.aspx) <br/> |Eine für die eDiscovery-API spezifische Ausnahme, die eine Nachricht oder eine interne Ausnahme aufnimmt.  <br/> |
| [Export](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.Export.aspx) <br/> |Steht für einen Export, der einem bestimmten **Case**-Objekt zugeordnet ist. Das **Export**-Objekt kann aus einem **T:Microsoft.SharePoint.SPListItem**-Objekt bestehen. Sie können ein **SavedSearch**-Objekt zu einem **Export**-Objekt hinzufügen und optional die Rechteverwaltung anwenden und das **Export**-Objekt herunterladen.  <br/> |
| [ExportCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.ExportCollection.aspx) <br/> |Steht für eine Auflistung von **Export**-Objekten. <br/> |
| [ExportStatus](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.ExportStatus.aspx) <br/> |Steht für den Status des Exports, der angibt, ob der Export gestartet, nicht gestartet, beendet oder mit Fehlern abgeschlossen wurde.  <br/> |
| [SavedSearch](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SavedSearch.aspx) <br/> |Steht für eine gespeicherte eDiscovery-Suche. **SavedSearch**-Objekte können kopiert, gelöscht oder aktualisiert werden. Statistiken, die einer gespeicherten Suche zugeordnet sind, können aktualisiert werden. Suchfilter, Exchange 2013-Filter, Quell-IDs, Quellgruppen-IDs, Abfragen und Filter können einem **SavedSearch**-Objekt zugeordnet werden.  <br/> |
| [SavedSearchCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SavedSearchCollection.aspx) <br/> |Steht für eine Auflistung von **SavedSearch**-Objekten. <br/> |
| [Source](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.Source.aspx) <br/> |Steht für den Datenquelltyp, der in eDiscovery-Vorgängen verwendet wird. Ein **Source**-Objekt akzeptiert ein **Case**-Objekt, einen Datenquelltyp und einen Filter (d. h. eine partielle oder vollständige Spezifikation des Containers, der die Quelle identifiziert) als Parameter. Informationen zur Quelle können zurückgegeben werden, z. B. Aufbewahrungsstatus, Speicherort der Quelle wie in SharePoint indexiert sowie, ob die Quelle ein Postfach ist.  <br/> |
| [SourceCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceCollection.aspx) <br/> |Steht für eine Auflistung von **Source**-Objekten. <br/> |
| [SourceGroup](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceGroup.aspx) <br/> |Steht für eine Gruppe von **Source**-Objekten. <br/> |
| [SourceGroupCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceGroupCollection.aspx) <br/> |Steht für eine Auflistung von **SourceGroup**-Objekten. <br/> |
| [SourceManagementType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceManagementType.aspx) <br/> |Steht für die Skala für die Verwaltung von Quellen. Optionen umfassen die Quelle, die Quellgruppe und den gesamten Inhalt.  <br/> |
| [SourceType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceType.aspx) <br/> |Steht für den Typ der Quelle. Quelltypen umfassen Exchange 2013, aktuelle und ältere Versionen von SharePoint Server und Dateifreigaben.  <br/> |
| [SourceValidation](https://msdn.microsoft.com/library/Microsoft.Office.Server.Discovery.SourceValidation.aspx) <br/> |Gibt an, ob die Quelle gültig ist.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="SP15_eDiscoveryInSP_AdditionalResources"> </a>


-  [Neuigkeiten in SharePoint eDiscovery und Einhaltung von Bestimmungen](what-s-new-in-sharepoint-ediscovery-and-compliance.md)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  

