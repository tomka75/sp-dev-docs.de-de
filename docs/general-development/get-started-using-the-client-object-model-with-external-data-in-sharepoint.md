---
title: Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8ed91929-fdb6-4fde-ba2a-7942870575f3
ms.openlocfilehash: 5efb6f880389b4f1d856ab8bf95f6dcde99bea09
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-using-the-client-object-model-with-external-data-in-sharepoint"></a>Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint
Erfahren Sie, wie Sie das SharePoint-Clientobjektmodell für die Arbeit mit Business Connectivity Services (BCS) in SharePoint verwenden.
## <a name="what-is-the-sharepoint-client-object-model"></a>Was ist das SharePoint-Clientobjektmodell?

Das Clientobjektmodell für SharePoint setzt sich aus clientbasierten Bibliotheken zusammen, die das Serverobjektmodell darstellen. Sie werden in drei verschiedene DLL-Dateien verpackt, damit sie eine Vielzahl von Entwicklungstypen berücksichtigen können. Das Clientobjektmodell enthält die meisten wesentlichen Funktionen der Server-API. Dies ermöglicht den Zugriff auf die gleichen Funktionstypen von browserbasierten Skripts und .NET-Webanwendungen und Silverlight-Anwendungen.  <br/> Zur Verbesserung und Erweiterung der Funktionen für die Arbeit mit externen Daten wurde das Clientobjektmodell in Business Connectivity Services (BCS) um zusätzliche Funktionalitäten erweitert.  <br/> 

<a href="#BCScsom_getstarted"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Tasks"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Learnmore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a></p>

## <a name="get-started-using-the-sharepoint-client-object-model-with-external-data"></a>Erste Schritte der Verwendung des SharePoint-Clientobjektmodells mit externen Daten
<a name="BCScsom_getstarted"> </a>

Zur Entwicklung von Lösungen mithilfe des SharePoint-Client-Objektmodells (CSOM) benötigen Sie Folgendes:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2012
    
  
Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).
  
    
    
Zum Zugreifen auf die vom Clientobjektmodell bereitgestellten Funktionen müssen Sie nur Verweise auf **Microsoft.SharePoint.Client.Runtime.dll**- und **Microsoft.SharePoint.Client.dll**-Dateien in den Projekten hinzufügen. Sie können auch das Clientobjektmodell verwenden, indem Sie auf die folgenden DLL-Dateien im globalen Assemblycache verweisen:
  
    
    

-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.Runtime.dll`
    
  
-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.dll`
    
  

### <a name="sharepoint-client-object-model-essentials"></a>SharePointGrundlegendes zum Clientobjektmodell

Die folgenden Artikel helfen Ihnen dabei, das Clientobjektmodell in SharePoint zu verstehen.
  
    
    

**Tabelle 1. Grundlegende Konzepte zum Verständnis des Clientobjektmodell**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md) <br/> |Erfahren Sie, welche Möglichkeiten Ihnen externe Inhaltstypen bieten, und was Sie benötigen, um mit deren Erstellung in SharePoint zu beginnen.  <br/> |
| [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |Informationen zu den ersten Schritten bei der Erstellung externer Inhaltstypen auf der Basis von OData-Quellen und der Verwendung dieser Daten in SharePoint- oder Office 2013-Komponenten.  <br/> |
| [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md) <br/> |Erfahren Sie mehr über die verschiedenen API-Gruppen, die in SharePoint bereitgestellt werden, einschließlich des Serverobjektmodells, der verschiedenen Clientobjektmodellen und des REST/OData-Webdiensts.  <br/> |
| [.NET-Client-API-Referenz für SharePoint](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx) <br/> |Hier finden Sie Informationen zu den .NET Client-Klassenbibliotheken in SharePoint.  <br/> |
| [JavaScript-API-Referenz für SharePoint](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx) <br/> |Informationen zu den JavaScript-Objektbibliotheken in SharePoint.  <br/> |
   

## <a name="what-can-you-do-with-the-client-object-model"></a>Welche Verwendungsmöglichkeiten bietet das Clientobjektmodell?
<a name="BCScsom_Tasks"> </a>

Sie können das SharePoint-Clientobjektmodell zum Abrufen, Aktualisieren und Verwalten von Daten in SharePoint verwenden. SharePoint bietet die Clientbibliotheken in verschiedenen Formaten, um den Anforderungen der meisten Entwickler gerecht zu werden. Für Webentwickler, die Skriptsprachen verwenden, wird die Clientbibliothek inJavaScript angeboten. Für .NET-Entwickler wird sie als .NET-clientverwaltete DLL-Datei angeboten. Für Entwickler von Silverlight-Anwendungen wird die Clientbibliothek als Silverlight-DLL-Datei bereitgestellt.
  
    
    
Weitere Informationen über Verwendungsmöglichkeiten des Clientobjektmodells in SharePoint finden Sie in den in Tabelle 2 aufgeführten Artikeln.
  
    
    

**Tabelle 2. Allgemeine Aufgaben beim Verwenden des Clientobjektmodells mit externen Daten**


|**Aufgabe**|**Beschreibung**|
|:-----|:-----|
| [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |Hier erfahren Sie, wie Sie Code zum Ausführen grundlegender Vorgänge mit dem SharePoint-Clientobjektmodell schreiben.  <br/> |
| [Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |In diesem Artikel erfahren Sie, wie Sie das SharePoint-Clientobjektmodell verwenden, um mit SharePoint BCS-Objekten mithilfe von browserbasierten Skripts zu arbeiten.  <br/> |
   
Im folgenden werden einige Beispiele für allgemeine Aufgaben aufgeführt, die Sie mit dem Clientobjektmodell (CSOM) durchführen können.
  
    
    

### <a name="get-a-specific-entity"></a>Abrufen einer bestimmten Entität

In diesem Beispiel wird gezeigt, wie Sie Kontext aus SharePoint abrufen und dann eine bestimmte Datenquellenentität abrufen.
  
    
    

```cs

ClientContext ctx = new ClientContext("http://sharepointservername"); 
Web web = ctx.Web; 
ctx.Load(web); 
Entity entity = ctx.Web.GetEntity("http://sharepointservername", "EntityName"); 
ctx.Load(entity); 
ctx.ExecuteQuery(); 

```


### <a name="create-a-generic-invoker"></a>Erstellen einer generischen aufrufenden Instanz

In diesem Beispiel wird gezeigt, wie Sie eine generische aufrufende Instanz schreiben, damit Sie ein Entitätsobjekt für die Verwendung innerhalb des Codes erstellen können.
  
    
    

```cs

ObjectCollection myObj; 
entity.Execute("MethodInstanceName", lsi, myObj); 
ctx.Load(myObj); 
ctx.ExecuteQuery(); 

```


### <a name="retrieve-paged-result-sets"></a>Abrufen von seitennummerierten Resultsets

Das folgende Beispiel zeigt, wie sie ein gefiltertes, seitennummeriertes Dataset abrufen. In diesem Fall beträgt der Seitenwert 50.
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
    if(filter.FilterType == FilterType.Limit) 
    { 
        filter.FilterValue = 50; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


### <a name="query-for-filtered-information"></a>Abfragen gefilterter Informationen

Im folgenden Beispiel wird veranschaulicht, wie Sie ein gefiltertes Resultset zurückgeben können. In diesem Fall werden die Daten nach dem Feld **X.Y.Z.Country** gefiltert. Der Code such nach allen Elementen mit dem Wert „Indien" und fasst diese dann in einer Sammlung zusammen.
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


## <a name="beyond-the-basics-learn-more-about-the-client-object-model"></a>Weiterführendes: Weitere Informationen zum Clientobjektmodell
<a name="BCScsom_Learnmore"> </a>

Weitere Informationen zur Verwendung des Clientobjektmodells in SharePoint, finden Sie in Tabelle 3.
  
    
    

**Tabelle 3. Erweiterte Konzepte für das Clientobjektmodell**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [BCS-Client-Objektmodellreferenz für SharePoint](bcs-client-object-model-reference-for-sharepoint.md) <br/> |Zusammenfassung der für das Erstellen clientseitiger Skripts verfügbaren Objekte unter Verwendung des SharePoint-Clientobjektmodells für den Zugriff auf externe von BCS zur Verfügung gestellte Daten.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="BCScsom_Learnmore"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [SharePoint: Zugreifen auf komplexe externe Inhaltstypen mit CSOM](http://code.msdn.microsoft.com/office/SharePoint-Accessing-ccbc24cf)
    
  
