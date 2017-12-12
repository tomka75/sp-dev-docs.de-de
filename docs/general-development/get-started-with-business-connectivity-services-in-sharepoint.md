---
title: Erste Schritte mit den Business Connectivity Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6bf3db0-db79-4b13-9834-891d24b2c9e5
ms.openlocfilehash: 971c338c4d05ddb8ede3cf5f77aa3eabebb2b1b3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-with-business-connectivity-services-in-sharepoint"></a>Erste Schritte mit den Business Connectivity Services in SharePoint
Lernen Sie die Grundlagen dessen, was Business Connectivity Services (BCS) für Entwickler von SharePoint-Lösungen bietet, sowie die ersten Schritte beim Verwenden von BCS in verschiedenen Arten von Lösungen.
## <a name="what-is-business-connectivity-services"></a>Was ist Business Connectivity Services?

Business Connectivity Services (BCS) wurden in SharePoint Server 2010 als eine Weiterentwicklung des Geschäftsdatenkatalogs in Office SharePoint Server 2007 eingeführt. BCS ermöglicht SharePoint das Arbeiten mit Daten, die extern gehostet werden. Mögliche Quellen können Datenbanken, Webdienste, Windows Communication Foundation (WCF)-Dienste, Open Data Protocol (OData)-Quellen und andere proprietäre Daten, auf die mithilfe einer benutzerdefinierten .NET-Assembly zugegriffen werden kann.

<a href="#SP15GettingStartedBCS_WhatDoYouNeed"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_WhatCanYouDo"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_LearnMore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a>

   
In einer dynamischen Arbeitsumgebung benötigen Information-Worker Zugriff auf Daten, die in separater Software enthalten sind, z. B.:
  
    
    

- Strukturierte Daten in den Unternehmensanwendungen der Organisation, z. B. ERP- und CRM-Anwendungen
    
  
- Unstrukturierte Daten in Geschäftsproduktivitätsanwendungen, z. B. solche in Microsoft Office, in Team- und Zusammenarbeitsanwendungen wie SharePoint und in Web 2.0-Diensten wie Internetanwendungen, Wikis, Blogs und sozialen Netzwerken.
    
  
Obwohl die meisten Information-Worker die größte Zeit über innerhalb der Produktivitätsanwendungen arbeiten (z. B. der Microsoft Office-Umgebung, benötigen sie auch eine Möglichkeit zum Integrieren dieser Umgebung in die verwendeten Unternehmensanwendungen und Zusammenarbeitssoftware und Dienste. Der Geschäftsdatendatenkatalog stellt diese Funktion in SharePoint bereit.
  
    
    

## <a name="get-started-with-business-connectivity-services"></a>Erste Schritte mit den Business Connectivity Services
<a name="SP15GettingStartedBCS_WhatDoYouNeed"> </a>

Sie benötigen zunächst Folgendes, um mit der Entwicklung mit Business Connectivity Services zu beginnen:
  
    
    

- SharePoint
    
  
- Visual Studio
    
  
- Office Developer Tools für Visual Studio 2012
    
    oder
    
  
- SharePoint Designer
    
  
Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="business-connectivity-services-essentials"></a>Grundlagen zu Business Connectivity Services

Die folgende Tabelle zeigt die Kernkonzepte, mit denen Sie sich vertraut machen müssen, bevor Sie mit der Entwicklung von BCS-Lösungen beginnen.
  
    
    

**Tabelle 1. Kernkonzepte zum Verständnis von BSC.**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Entity Data Model - Schlüsselkonzepte](http://msdn.microsoft.com/de-DE/library/ee382840.aspx) <br/> |Das Entity Data Model (EDM) verwendet drei Schlüsselkonzepte zum Beschreiben der Datenstruktur: Entitätstyp, Zuordnungstyp und Eigenschaft. Dies sind die wichtigsten Konzepte beim Beschreiben der Datenstruktur in allen Implementierungen von EDM.  <br/> |
| [Grundlegende Sicherheitsmaßnahmen für Webanwendungen](http://msdn.microsoft.com/de-DE/library/zdh19h94.aspx) <br/> |Das Erstellen sicherer Webanwendungen ist ein sehr umfangreiches Thema. Sie müssen sich auch mit den Sicherheitsfunktionen des Windows-Betriebssystems vertraut machen, .NET Framework und ASP.NET. Es ist wichtig, zu verstehen, wie diese Sicherheitsfunktionen zu verwenden sind, um Bedrohungen entgegenzuwirken.  <br/> |
| [WCF Data Services](http://msdn.microsoft.com/de-DE/data/odata.aspx) <br/> |WCF Data Services, früher ADO.NET Data Services genannt, ermöglichen die Erstellung und Verarbeitung von OData-Diensten für das Web.  <br/> |
| [Open Data Protocol (OData)](http://www.odata.org) <br/> |OData ist ein Industriestandardprotokoll für den Zugriff auf Daten über URLs. Es befindet sich im Grunde über dem HTTP-Protokoll, um Funktionen mithilfe von vorhandenen HTTP-Verben zu lesen und zu schreiben.  <br/> |
| [Internetinformationsdienste](http://www.iis.net/) <br/> |Internetinformationsdienste (IIS) ist eine Plattform, auf der SharePoint ausgeführt wird. Sie müssen nachvollziehen können, wie Websites, virtuelle Verzeichnisse, Webdienste, URLs, Websicherheit und weitere mit IIS verwandte Technologien erstellt werden können.  <br/> |
| [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md) <br/> |Externe Inhaltstypen sind Beschreibungen externer Systeme, die sie darstellen. Sie können wiederverwendet werden, wenn sie in SharePoint importiert werden, und können zum Erstellen komplexer codefreier Lösungen mithilfe von SharePoint Designer 2013, Outlook 2013, Webparts, externen Listen und benutzerdefinierten Clientanwendungen verwendet werden.  <br/> |
| [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md) <br/> |SharePointbietet die Möglichkeit, auf alle Objekte über eine sorgfältig erstellte URL zuzugreifen. BCS wurde erweitert, um diese Funktionalität bereitzustellen.  <br/> |
   

## <a name="what-can-you-do-with-business-connectivity-services"></a>Welche Möglichkeiten bieten Business Connectivity Services?
<a name="SP15GettingStartedBCS_WhatCanYouDo"> </a>

Mit BCS können Sie Informationen aus verschiedenen Quellen zu SharePoint verschieben. Sie können beispielsweise Daten aus einer externen SQL Server-Datenbank, einem gewöhnlichen Webdienst, einem WCF-Dienst, aus proprietären Systemen und OData-Diensten zu SharePoint verschieben.
  
    
    

**Tabelle 2. Allgemeine Aufgaben beim Arbeiten mit Business Connectivity Services**


|**Aufgabe**|**Beschreibung**|
|:-----|:-----|
| [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md) <br/> |Informationen zum Erstellen von externen Business Connectivity Services (BCS)-Inhaltstypen.  <br/> |
| [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |Hier erhalten Sie Informationen zu den ersten Schritten bei der Erstellung von auf OData-Quellen basierenden externen Inhaltstypen und der Verwendung dieser Daten in SharePoint oder Office-Komponenten.  <br/> |
| [Vorgehensweise: Erstellen von externen Ereignisempfängern](how-to-create-external-event-receivers.md) <br/> |Informationen zu Konzepten hinter dem Erstellen von Ereignisempfängern, die externen Listen angefügt und ausgeführt werden, wenn die von dieser Liste dargestellten externen Daten aktualisiert werden.  <br/> |
| [Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie externe Inhaltstypen erstellen, die auf App-Ebene installiert oder vorhanden sind, und Entwicklern das Erstellen von Apps mit hohem Datenaufkommen mithilfe von externen Datenquellen ermöglichen.  <br/> |
| [Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie das SharePoint-Clientobjektmodell für die Arbeit mit BCS in SharePoint verwenden.  <br/> |
   

## <a name="beyond-the-basics-learn-more-about-business-connectivity-services"></a>Weiterführendes: Weitere Informationen zu Business Connectivity Services
<a name="SP15GettingStartedBCS_LearnMore"> </a>

Wenn Sie die grundlegenden Konzepte von BCS beherrschen, können Sie erweiterte Funktionen zum Erstellen leistungsstarker Lösungen verwenden.
  
    
    

**Tabelle 3. Erweiterte Konzepte in BCS**


|**Thema**|**Beschreibung**|
|:-----|:-----|
| [Vorgehensweise: Erstellen einer OData-Datendiensts zur Verwendung als einer externen BCS-System](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |In diesem Artikel erfahren sie, wie Sie einen im Internet aufrufbaren WCF-Dienst erstellen, der OData zum Senden von Benachrichtigungen an SharePoint verwendet, wenn die zugrunde liegenden Daten geändert werden. Mithilfe dieser Benachrichtigungen werden Ereignisse ausgelöst, die mit externen Listen verknüpft sind.  <br/> |
| [BDC-Modell-Schemareferenz für SharePoint](bdc-model-schema-reference-for-sharepoint.md) <br/> |Hier finden Sie die Referenzdokumentation zum Schema des BDC-Modells.  <br/> |
| [BCS-Client-Objektmodellreferenz für SharePoint](bcs-client-object-model-reference-for-sharepoint.md) <br/> |Zusammenfassung der für das Erstellen clientseitiger Skripts verfügbaren Objekte unter Verwendung des SharePoint-Clientobjektmodells für den Zugriff auf externe von Business Connectivity Services (BCS) zur Verfügung gestellte Daten.  <br/> |
| [BCS-REST-API-Referenz für SharePoint](bcs-rest-api-reference-for-sharepoint.md) <br/> |Hier erhalten Sie Referenzinformationen für das Erstellen von REST-URIs, die für den Zugriff und die Manipulation von OData-Quellen verwendet werden.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="SP15GettingStartedBCS_LearnMore"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Open Data Protocol-Website](http://www.odata.org/)
    
  
-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Externe Ereignisse und Warnungen in SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Add-in-bezogenen externen Inhaltstypen in SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
