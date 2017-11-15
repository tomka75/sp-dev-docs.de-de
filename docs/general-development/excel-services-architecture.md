---
title: Excel Services-Architektur
ms.date: 09/25/2017
keywords: excel services design
f1_keywords: excel services design
ms.prod: sharepoint
ms.assetid: e0349b4a-2d52-46c4-a167-801e9c24eaca
ms.openlocfilehash: c1abeb724ec1174e66355530e58f9b4d3ab07453
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-architecture"></a>Excel Services-Architektur

Excel Services ist Bestandteil von Microsoft SharePoint Server 2010. Excel Services basiert auf ASP.NET- und SharePoint Foundation-Technologien. Im Anschluss finden Sie die Hauptkomponenten in Excel Services:
  
    
    


- Excel Web Access
    
  
- Excel-Webdienste
    
  
- Benutzerdefinierte Funktionen (User-Defined Functions, UDFs)
    
  
- ECMAScript (JavaScript, JScript)
    
  
- REST (Representational State Transfer)-Dienst
    
  
- Dienste für Excel-Berechnungen
    
  

> **Hinweis:** In Microsoft Excel Online, Bestandteil von Office Online, werden auch Excel-Arbeitsmappen im Browser unterstützt. Weitere Informationen zu Excel Online finden Sie in der [Dokumentation zu Office Web Apps](https://technet.microsoft.com/en-us/library/ee855124.aspx). 
  
    
    

Die Komponenten von Excel Web Access, Excel Web Services, UDFs, JavaScript, des REST-Diensts und von Dienste für Excel-Berechnungen können in zwei Hauptgruppen unterteilt werden: die Komponenten auf einem Front-End-Server (auch als "Web-Front-End" bezeichnet) und die Komponente auf einem Back-End-Anwendungsserver. **Komponenten auf einem Web-Front-End und auf einem Back-End-Anwendungsserver**

  
    
    

  
    
    
![Ein Web-Frontend- und ein Backend-Anwendungsserver](../images/ed480e23-e0e8-4896-93b1-98a94f50b9a0.gif)
  
    
    

  
    
    

  
    
    

## <a name="web-front-end-servers-and-back-end-application-servers"></a>Web-Front-End-Server und Back-End-Anwendungsserver

Die Komponenten von Excel Web Access, Excel Web Services, UDFs, JavaScript, des REST-Diensts und von Dienste für Excel-Berechnungen können in Komponenten auf dem Web-Front-End-Server und Komponenten unterteilt werden, die auf einem Back-End-Anwendungsserver gespeichert sind. Zu den Komponenten auf dem Web-Front-End gehören Excel Web Access, JavaScript, der REST-Dienst und Excel Web Services. Die Dienste für Excel-Berechnungen-Komponente befindet sich auf dem Back-End-Anwendungsserver, zusammen mit allen UDF-Assemblies, die von einem Administrator hinzugefügt wurden.
  
    
    
In der einfachsten Konfiguration in SharePoint Server 2010, das heißt, auf einem einzelnen Computer, auf dem SharePoint Server 2010 als eigenständige Installation ausgeführt wird, werden alle fünf Komponenten auf dem gleichen Computer installiert. In einer typischen Unternehmensumgebung mit zahlreichen Benutzern befinden sich die Komponenten auf dem Web-Front-End-Server und die Komponenten auf dem Back-End-Anwendungsserver jedoch auf unterschiedlichen Computern in einer Farmkonfiguration. Es besteht die Möglichkeit, den Web-Front-End-Server unabhängig vom Back-End-Anwendungsserver zu skalieren. So können Sie beispielsweise die Anzahl der Web-Front-End-Server oder der Back-End-Anwendungsserver in Abhängigkeit von den Anforderungen Ihres Unternehmens erhöhen.
  
    
    
Informationen zu Excel Services Topologie, Skalierbarkeit, Leistung und Sicherheit finden Sie unter der SharePoint Server 2010-Dokumentation auf  [TechNet](http://technet.microsoft.com/en-us/library/cc303422%28office.14%29.aspx). 
  
    
    

## <a name="excel-web-access"></a>Excel Web Access

Excel Web Access ist eine Anzeigeseite und ein Excel Services-Webpart, die einer beliebigen Webpart-Seite in SharePoint Server 2010 hinzugefügt werden können. Excel Web Access rendert (in anderen Worten erstellt den HTML-Code für) aktive Excel-Arbeitsmappen auf einer Webseite und ermöglicht dem Benutzer, mit diesen Arbeitsmappen zu interagieren und diese zu durchsuchen. Excel Web Access ist die sichtbare Excel Services-Komponente für den Benutzer. Sie können Excel Web Access wie alle anderen Webparts in SharePoint Server 2010 verwenden. Excel Web Access erfordert keinerlei Installation auf dem Clientcomputer.
  
    
    
Die Eigenschaften des Excel Web Access-Webparts können auch angepasst werden. Weitere Informationen finden Sie in der Referenzdokumentation zum Namespace **Microsoft.Office.Excel.Server.WebUI**.
  
    
    

## <a name="excel-web-services"></a>Excel Web Services

Excel Web Services ist die Excel Services-Komponente, die programmgesteuerten Zugriff auf seinen Webdienst bereitstellt. Sie können Anwendungen entwickeln, die Excel Web Services aufrufen, um Werte aus Arbeitsmappen zu berechnen, festzulegen und zu extrahieren und um externe Datenverbindungen zu aktualisieren. Wenn Sie Excel Web Services verwenden, können Sie serverseitige Arbeitsmappenlogik in eine Anwendung integrieren, die Aktualisierung von Excel-Arbeitsmappen automatisieren und anwendungsspezifische Benutzeroberflächen für serverseitige Excel-Berechnungen erstellen. 
  
    
    

> **Hinweis:** Wenn Sie Änderungen an einer Arbeitsmappe vornehmen, z. B. durch Festlegen von Werten für einen Bereich mithilfe von Excel Web Services, bleiben die Änderungen an der Arbeitsmappe nur für die jeweilige Sitzung erhalten. Die Änderungen werden nicht in der ursprünglichen Arbeitsmappe gespeichert oder persistent gemacht. Wenn die aktuelle Arbeitsmappensitzung endet (z. B. beim Aufruf der Methode **CloseWorkbook** oder bei einem Sitzungstimeout), gehen die vorgenommenen Änderungen verloren. Wenn Sie Änderungen speichern möchten, die Sie an einer Arbeitsmappe vornehmen, können Sie die Methode **GetWorkbook** verwenden und die Arbeitsmappe dann speichern. Weitere Informationen finden Sie unter [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) . Sie können die Arbeitsmappe auch im Bearbeitungsmodus öffnen und die Änderungen speichern.
  
    
    

Weitere Informationen zu Excel Web Services finden Sie unter [Excel Services-Entwicklungsroadmap](excel-services-development-roadmap.md).
  
    
    

## <a name="user-defined-functions-udfs"></a>Benutzerdefinierte Funktionen (User-Defined Functions, UDFs)

Excel Services-UDFs ermöglichen Ihnen die Verwendung von Formeln in Zellen zum Aufrufen von benutzerdefinierten Funktionen, die in verwaltetem Code geschrieben und in SharePoint Server 2010 bereitgestellt werden. Weitere Informationen zu UDFs in Excel Services finden Sie unter  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).
  
    
    

## <a name="ecmascript-javascript-jscript"></a>ECMAScript (JavaScript, JScript)

Das JavaScript-Objektmodell in Excel Services ermöglicht Entwicklern, die Excel Web Access-Webpartsteuerung auf einer Seite anzupassen, zu automatisieren und auszuführen. Durch die Verwendung des JavaScript-Objektmodells können Sie Mashups und andere integrierte Lösungen erstellen, die mit einem oder mehreren Excel Web Access-Webpart-Steuerelementen auf einer Seite oder in einem **iframe** mit Skript auf der Seite interagieren. Sie haben auch die Möglichkeit, Ihren Arbeitsmappen und dem umgebenden Code weitere Funktionen hinzuzufügen.
  
    
    
For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.
  
    
    

## <a name="rest-api"></a>REST-API

Mithilfe der REST-API in Excel Services können Sie direkt über eine URL auf Arbeitsmappenteile oder -elemente zugreifen. Die URL enthält einen „Markierungspfad“, bei dem es sich um den Einstiegspunkt zu einer ASPX-Seite, zum Speicherort der Arbeitsmappendatei und zum Pfad zum angeforderten Element in der Arbeitsmappe handelt. 
  
    
    
Der in der Excel Services-REST-API integrierte Ermittlungsmechanismus ermöglicht Entwicklern und Benutzern, den Inhalt einer Arbeitsmappe manuell oder programmgesteuert zu durchsuchen. 
  
    
    
Weitere Informationen zur REST-API in Excel Services finden Sie unter  [Excel Services-REST-API](excel-services-rest-api.md). 
  
    
    

## <a name="excel-calculation-services"></a>Dienste für Excel-Berechnungen

Die Aufgabe von Dienste für Excel-Berechnungen ist das Laden von Arbeitsmappen, die Berechung von Arbeitsmappen, das Aufrufen von benutzerdefiniertem Code (UDFs) und die Aktualisierung von externen Daten. Diese halten auch den Sitzungsstatus für die Interaktivität aufrecht. Dienste für Excel-Berechnungen hält eine Sitzung für die Dauer der Interaktionen mit der gleichen Arbeitsmappe durch einen Benutzer oder Aufrufer aufrecht. Eine Sitzung wird geschlossen, wenn diese vom Aufrufer explizit geschlossen wird, oder wenn die Sitzung das Zeitlimit auf dem Server überschreitet. Excel Services führt zur Leistungsverbesserung bei einem Zugriff von mehreren Benutzern auf den gleichen Arbeitsmappensatz eine Zwischenspeicherung der geöffneten Excel-Arbeitsmappen aus, berechnen den Status und externe Datenabfrageergebnisse.
  
    
    

## <a name="load-balancing"></a>Lastenausgleich

In Konfigurationen mit mehreren Servern führt Excel Services eine Lastausgleich für Anforderungen über mehrere Dienste für Excel-Berechnungen-Vorkommen in einer Farmkonfiguration aus. Wenn Ihre Installation mehrere Anwendungsserver enthält, gleicht Excel Services die Last aus, um sicherzustellen, dass kein einzelner Anwendungsserver durch Anforderungen überlastet wird.
  
    
    
Das Lastausgleichsverhalten kann von Administratoren konfiguriert werden.
  
    
    

## <a name="see-also"></a>Siehe auch


#### <a name="concepts"></a>Konzepte


  
    
    
 [Excel Services (Übersicht)](excel-services-overview.md)
  
    
    
 [Excel Services Development Roadmap](excel-services-development-roadmap.md)
  
    
    
 [Unterstützte und nicht unterstützte Features](supported-and-unsupported-features.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
