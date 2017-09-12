---
title: Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint
ms.prod: SHAREPOINT
ms.assetid: 7a87e5bf-4428-4055-b113-7665a93e7326
ms.openlocfilehash: 8d6c1de02776f39f6df582e75eaf47b5ff83ccd5
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="using-odata-sources-with-business-connectivity-services-in-sharepoint"></a>Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint
Erfahren Sie mehr über die ersten Schritte bei der Erstellung externer Inhaltstypen auf der Basis von OData-Quellen und der Verwendung dieser Daten in SharePoint- oder Office 2013-Komponenten.
## <a name="odata-and-the-odata-connector"></a>OData und der OData-Connector
<a name="SP15getstartedOdata_whatisodata"> </a>

Mit dem Open Data-Protokoll (OData) können Sie auf eine Datenquelle wie eine Datenbank zugreifen, indem Sie zu einer speziell zusammengesetzten URL browsen. Dies ermöglicht einen vereinfachten Ansatz für das Verbinden und Arbeiten mit Datenquellen, die in einer Organisation gehostet werden. 
  
    
    
OData ist ein Protokoll, das HTTP, Atom und JavaScript Object Notation (JSON) verwendet, damit Entwickler Anwendungen schreiben können, die mit einer ständig wachsenden Anzahl von Datenquellen kommunizieren können. Microsoft unterstützt die Erstellung dieses Standards als Möglichkeit, den Austausch von Daten zwischen Anwendungen und Datenspeichern zu ermöglichen, auf die aus dem Internet zugegriffen werden kann.
  
    
    
Der neue OData-Connector ermöglicht SharePoint die Kommunikation mit OData-Anbietern.
  
    
    
In SharePoint kann Business Connectivity Services (BCS) mit OData-Quellen, oder Produzenten, ohne direkt an die OData-Quelle codieren zu müssen. Produzenten stellen ihre Daten auf eine strukturierte Weise über einen Webdienst zur Verfügung. Einige Produzenten lassen möglicherweise einige Aktualisierung der zugrunde liegenden Daten zu, andere möglicherweise nur einen schreibgeschützten Zugriff. Für Zwecke der Werbung, welche Vorgänge verfügbar sind, hat der Produzent ein Dienstdokument, das unter einem angegebenen URL-Endpunkt gefunden werden kann. SharePoint ist bereits ein OData-Produzent. SharePoint-Listendaten werden als OData-Quelle für alle Verbraucher zur Verfügung gestellt, die über die entsprechenden Rechte verfügen.
  
    
    

### <a name="examples-of-odata-producers"></a>Beispiele für OData-Produzenten
<a name="ExamplesOfODataProducers"> </a>

Im Folgenden finden Sie einige Beispiele für OData-Implementierungen. Diese Anwendungen und Dienste stellen ihre Daten über das OData-Protokoll zur Verfügung.
  
    
    

- SharePoint Foundation 2010
    
  
- SharePoint Server 2010
    
  
- SQL Azure
    
  
- Microsoft Azure Table Storage
    
  
- Microsoft Azure Marketplace
    
  
-  SQL Server Reporting Services
    
  
- Microsoft Dynamics CRM 2011
    
  
- Windows Live
    
  
Eine Liste der Produzenten von OData-Diensten finden Sie auf der  [Open Data Protocol-Website](http://www.odata.org/ecosystem).
  
    
    

## <a name="prerequisites-for-working-with-the-bcs-odata-connector"></a>Voraussetzungen für das Arbeiten mit dem BCS-OData-Connector
<a name="SP15GetstartedOdata_prereq"> </a>

Zum Entwickeln von OData-basierten externen Inhaltstypen benötigen Sie Folgendes:
  
    
    

- Visual Studio 2012
    
  
- SharePoint
    
  
- Office Developer Tools für Visual Studio 2012
    
  
Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint).
  
    
    

## <a name="creating-external-content-types-for-odata-data-sources"></a>Erstellen von externen Inhaltstypen für OData-Datenquellen
<a name="SP15GetstartedOdata_creatingECT"> </a>

Damit SharePoint die von einem bestimmten OData-Produzenten zur Verfügung gestellten Daten verwenden kann, muss ein externer Inhaltstyp in SharePoint erstellt werden. Wie bei allen externen SharePoint-Inhaltstypen enthält dieser alle Konnektivitätsinformationen, die für die Verbindung und Kommunikation mit dem externen System erforderlich sind.
  
    
    
Das Erstellen eines externen Inhaltstyps, der eine OData-Datenquelle verwendet, ähnelt der Erstellung beliebiger externer Inhaltstypen. Sie können Visual Studio 2012 verwenden, um automatisch externe OData-Inhaltstypen zu generieren. Sie stellen lediglich den REST-Endpunkt (Representational State Transfer) der OData-Quelle bereit, wenn Sie den externen Inhaltstyp erstellen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint).
  
    
    

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="SP15GetstartedOdata_inthissect"> </a>


-  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint)
    
  
-  [Vorgehensweise: Erstellen einer OData-Datendiensts zur Verwendung als einer externen BCS-System](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system)
    
  
-  [Vorgehensweise: Erstellen eine externe Liste mithilfe einer in SharePoint OData-Datenquelle](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15GetstartedOdata_addres"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint)
    
  
-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint)
    
  

