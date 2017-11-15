---
title: Business Connectivity Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 64b7d032-4b83-4e9e-bc08-f0a161af5457
ms.openlocfilehash: 20274a51726540bd765b8a7627a4e645e9890b43
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="business-connectivity-services-in-sharepoint"></a>Business Connectivity Services in SharePoint
Erfahren Sie, worum es sich bei Business Connectivity Services (BCS) handelt, welche Möglichkeiten es Ihnen bietet, und wie Sie in die Entwicklung von BCS-Anwendungen in SharePoint einsteigen. Sie können SharePoint als Zentrale für die Erstellung umfangreicher Produktivitäts- und Zusammenarbeitslösungen verwenden, die mit verschiedensten externen Systemen verwendet werden können. Business Connectivity Services (BCS) stellt die Infrastruktur bereit, die es SharePoint ermöglicht, Daten aus diesen externen Systemen in einem zentralen System zusammenzuführen. Die Tatsache, dass BCS eine flexible und umfassende Möglichkeit bietet, die externe Systemdatenquelle und die Interaktion mit dieser zu beschreiben, stellt ein überzeugendes Argument dafür dar, zusätzlich zu neuen SharePoint-Add-InsSharePoint als die zentrale Schnittstelle für die Arbeit mit Legacy-Geschäftssystemen zu verwenden.
  
    
    


## <a name="what-can-bcs-do"></a>Welche Möglichkeiten bietet BCS?
<a name="BCSoverview_Whatcanbcsdo"> </a>

BCS bietet Mechanismen, mit denen erfahrenen Benutzern und Entwicklern sowie IT-Experten der Unternehmenseinheit folgende Aufgaben problemlos ausführen können:
  
    
    

- Offenlegen externer Daten aus Unternehmensanwendungen, Webdiensten und OData-Diensten in SharePoint und Rich-Client-Office-Anwendungen
    
  
- Bereitstellen von Office-Verhaltensweisen (z. B. Kontakte, Aufgaben und Termine) und Funktionen für externe Daten und Dienste.
    
  
- Bereitstellen uneingeschränkter Interaktion mit den Daten, einschließlich Zurückschreibfunktionen von Office-Anwendungen und SharePoint Server in die zugrunde liegenden externen Systemdaten und Geschäftsobjekte
    
  
- Aktivieren der Offlineverwendung von externen Daten und Prozessen
    
  
- Überwinden der Kluft zwischen der Welt unstrukturierter Dokumente und Personen und den entsprechenden strukturierten Daten, die in externen Systemen unerreichbar sind
    
  

## <a name="components-of-bcs"></a>Komponenten von BCS
<a name="bkmk_Components"> </a>

Abbildung 1 zeigt die Features, die in SharePoint und Office 2013 enthalten sind.
  
    
    

**Abbildung 1. Featuregruppe der Business Connectivity Services**

  
    
    

  
    
    
![Business Connectivity Services-Featuregruppe](../images/BCSin2013FeatureSet.jpg)
  
    
    

  
    
    

  
    
    

## <a name="using-external-content-types-in-bcs"></a>Verwenden externer Inhaltstypen in BCS
<a name="bkmk_UsingECTs"> </a>

Externe Inhaltstypen sind der Kern von BCS. Sie können damit die Metadaten und Verhaltensweisen einer Geschäftseinheit (etwa eines Kunden oder einer Bestellung) an einem zentralen Ort verwalten und wiederverwenden. Sie ermöglichen Benutzern, mit diesen externen Daten zu interagieren und sie auf sinnvollere Weise zu verarbeiten.
  
    
    
Nehmen wir als Beispiel eine Geschäftsentität, etwa einen Kunden. Sie möchten in der Lage sein, aus Ihrer proprietären Datenbank Daten zu ziehen und damit in SharePoint zu arbeiten. Außerdem möchten Sie Ihren Außendienstmitarbeitern erlauben, Daten in Outlook 2013 offline zu nehmen. Es kann auch sein, dass Sie möchten, dass der Benutzer aus einer Liste von Kunden in einem Bestellvertragsdokument in Microsoft Word einen Kunden auswählen kann. Für all diese Aufgaben können Sie einen einzelnen externen Inhaltstypen erstellen und ihn dann überall wiederverwenden, wo Sie ihn benötigen.
  
    
    
Weitere Informationen zur Verwendung externer Inhaltstypen in BCS finden Sie unter  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md).
  
    
    

## <a name="developing-solutions-using-bcs"></a>Entwickeln von Lösungen mit BCS
<a name="bkmk_DevelopingSolutionsUsingBCS"> </a>

Sie können in SharePoint mit BCS eine breite Palette von Lösungen erstellen. Dazu zählen einfache Lösungen, die auf nativen Funktionen basieren, für die nur geringfügige oder keine Anpassungen erforderlich sind, mittlere Lösungen, für die Features in SharePoint und Office 2013 angepasst werden müssen, und erweiterte Lösungen, die komplexe Szenarios und reichhaltige Anwendungen ermöglichen, die deren Funktionsumfang erweitern. Für erweiterte Lösungen muss mithilfe von Visual Studio Code geschrieben werden. Dabei kann es sich entweder um vollständige End-to-End-Lösungen oder wiederverwendbare codebasierte Komponenten handeln, die in einer mittleren Lösung enthalten sind.
  
    
    
BCS ermöglicht Geschäftsbenutzern, mithilfe eines Webbrowers oder einer Microsoft Office-Clientanwendung wie Word oder Excel auf schnelle und einfache Weise ein breites Spektrum an Anforderungen bezüglicher externer Daten zu erfüllen. Benutzer können, ohne Code zu schreiben, mithilfe von BCS-Features wie externen Listen und Spalten für externe Daten und wiederverwendbaren BCS-Komponenten, die von Entwicklern erstellt und von der IT genehmigt werden, in Office-Clientanwendungen und SharePoint-Websites kombinierte Lösungen zusammenstellen. Diese Lösungen ermöglichen Geschäftsbenutzern (und ihren Teams), mit externen Daten so einfach wie mit SharePoint-Daten zu arbeiten - entweder offline oder verbunden oder direkt in Office 2013.
  
    
    
Weitere Informationen zum Einstieg finden Sie unter  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).
  
    
    

## <a name="using-odata-with-business-connectivity-services-in-sharepoint"></a>Verwenden von OData mit Business Connectivity Services in SharePoint
<a name="bkmk_ODataInBCS"> </a>

Das Open Data Protocol (OData) ist ein Webprotokoll, mit dem Sie mithilfe von Technologien wie HTTP, JavaScript Object Notation (JSON) und AtomPub dem Web Daten zur Verfügung stellen können. Der Zugriff auf die Daten erfolgt über speziell gestaltete URLs. Diese Architektur erlaubt Ihnen, über eine Vielzahl von Technologien mit Daten zu interagieren.
  
    
    
Weitere Informationen finden Sie unter  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md).
  
    
    

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="bkmk_inthissection"> </a>


-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Externe Ereignisse und Warnungen in SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Add-in-bezogenen externen Inhaltstypen in SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_AdditionalResources"> </a>


-  [Hinzufügen von SharePoint-Funktionen](add-sharepoint-capabilities.md)
    
  
-  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  

