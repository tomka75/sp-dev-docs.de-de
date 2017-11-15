---
title: Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8ed91929-fdb6-4fde-ba2a-7942870575f3
ms.openlocfilehash: 2ddd19599a6a88523cb38940355104d178500f3d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-using-the-client-object-model-with-external-data-in-sharepoint"></a><span data-ttu-id="d6690-102">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-102">Get started using the client object model with external data in SharePoint</span></span>
<span data-ttu-id="d6690-103">Erfahren Sie, wie Sie das SharePoint-Clientobjektmodell für die Arbeit mit Business Connectivity Services (BCS) in SharePoint verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6690-103">Learn how to use the SharePoint client object model to work with Business Connectivity Services (BCS) in SharePoint.</span></span>
## <a name="what-is-the-sharepoint-client-object-model"></a><span data-ttu-id="d6690-104">Was ist das SharePoint-Clientobjektmodell?</span><span class="sxs-lookup"><span data-stu-id="d6690-104">What is the SharePoint client object model?</span></span>

<span data-ttu-id="d6690-p101">Das Clientobjektmodell für SharePoint setzt sich aus clientbasierten Bibliotheken zusammen, die das Serverobjektmodell darstellen. Sie werden in drei verschiedene DLL-Dateien verpackt, damit sie eine Vielzahl von Entwicklungstypen berücksichtigen können. Das Clientobjektmodell enthält die meisten wesentlichen Funktionen der Server-API. Dies ermöglicht den Zugriff auf die gleichen Funktionstypen von browserbasierten Skripts und .NET-Webanwendungen und Silverlight-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="d6690-p101">The client object model for SharePoint is a set of client-based libraries that represent the server object model. They are packaged in three different DLLs to accommodate a variety of development types. The client object model includes most of the major functions of the server API. This allows access to the same types of functionality from browser scripting and also .NET web applications and Silverlight applications.</span></span>  <br/> <span data-ttu-id="d6690-109">Zur Verbesserung und Erweiterung der Funktionen für die Arbeit mit externen Daten wurde das Clientobjektmodell in Business Connectivity Services (BCS) um zusätzliche Funktionalitäten erweitert.</span><span class="sxs-lookup"><span data-stu-id="d6690-109">To enhance and expand the capabilities for working with external data, Business Connectivity Services (BCS) has expanded the client object model to include additional functionality.</span></span>  <br/> 

<a href="#BCScsom_getstarted"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Tasks"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Learnmore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a></p>

## <a name="get-started-using-the-sharepoint-client-object-model-with-external-data"></a><span data-ttu-id="d6690-110">Erste Schritte der Verwendung des SharePoint-Clientobjektmodells mit externen Daten</span><span class="sxs-lookup"><span data-stu-id="d6690-110">Get started using the SharePoint client object model with external data</span></span>
<span data-ttu-id="d6690-111"><a name="BCScsom_getstarted"> </a></span><span class="sxs-lookup"><span data-stu-id="d6690-111"></span></span>

<span data-ttu-id="d6690-112">Zur Entwicklung von Lösungen mithilfe des SharePoint-Client-Objektmodells (CSOM) benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d6690-112">To develop solutions using the SharePoint client object model (CSOM), you will need the following:</span></span>
  
    
    

- <span data-ttu-id="d6690-113">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-113">SharePoint</span></span>
    
  
- <span data-ttu-id="d6690-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d6690-114">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="d6690-115">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d6690-115">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="d6690-116">Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d6690-116">For information about how to set up your development environment, see  [Setting up a development environment for BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="d6690-p102">Zum Zugreifen auf die vom Clientobjektmodell bereitgestellten Funktionen müssen Sie nur Verweise auf **Microsoft.SharePoint.Client.Runtime.dll**- und **Microsoft.SharePoint.Client.dll**-Dateien in den Projekten hinzufügen. Sie können auch das Clientobjektmodell verwenden, indem Sie auf die folgenden DLL-Dateien im globalen Assemblycache verweisen:</span><span class="sxs-lookup"><span data-stu-id="d6690-p102">To access the capabilities provided by the client object model, you need only to add references to the **Microsoft.SharePoint.Client.Runtime.dll** and **Microsoft.SharePoint.Client.dll** files in their projects. You can also use the client object model by referencing the following DLLs in the global assembly cache:</span></span>
  
    
    

-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.Runtime.dll`
    
  
-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.dll`
    
  

### <a name="sharepoint-client-object-model-essentials"></a><span data-ttu-id="d6690-119">SharePointGrundlegendes zum Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d6690-119">SharePoint client object model essentials</span></span>

<span data-ttu-id="d6690-120">Die folgenden Artikel helfen Ihnen dabei, das Clientobjektmodell in SharePoint zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="d6690-120">The following articles will help you understand more about the client object model in SharePoint.</span></span>
  
    
    

<span data-ttu-id="d6690-121">**Tabelle 1. Grundlegende Konzepte zum Verständnis des Clientobjektmodell**</span><span class="sxs-lookup"><span data-stu-id="d6690-121">**Table 1. Core concepts for understanding the client object model**</span></span>


|<span data-ttu-id="d6690-122">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="d6690-122">**Article**</span></span>|<span data-ttu-id="d6690-123">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d6690-123">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d6690-124">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-124">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="d6690-125">Erfahren Sie, welche Möglichkeiten Ihnen externe Inhaltstypen bieten, und was Sie benötigen, um mit deren Erstellung in SharePoint zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="d6690-125">Learn what you can do with external content types and what you need to start creating them in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="d6690-126">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-126">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="d6690-127">Informationen zu den ersten Schritten bei der Erstellung externer Inhaltstypen auf der Basis von OData-Quellen und der Verwendung dieser Daten in SharePoint- oder Office 2013-Komponenten.</span><span class="sxs-lookup"><span data-stu-id="d6690-127">Provides information to help get started creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>  <br/> |
| [<span data-ttu-id="d6690-128">Auswählen des richtigen API-Satzes in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-128">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md) <br/> |<span data-ttu-id="d6690-129">Erfahren Sie mehr über die verschiedenen API-Gruppen, die in SharePoint bereitgestellt werden, einschließlich des Serverobjektmodells, der verschiedenen Clientobjektmodellen und des REST/OData-Webdiensts.</span><span class="sxs-lookup"><span data-stu-id="d6690-129">Learn about the several sets of APIs that are provided in SharePoint, including the server object model, the various client object models, and the REST/OData web service.</span></span>  <br/> |
| [<span data-ttu-id="d6690-130">.NET-Client-API-Referenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-130">.NET client API reference for SharePoint Online</span></span>](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d6690-131">Hier finden Sie Informationen zu den .NET Client-Klassenbibliotheken in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d6690-131">Find information about the .NET client class libraries in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="d6690-132">JavaScript-API-Referenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-132">JavaScript API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d6690-133">Informationen zu den JavaScript-Objektbibliotheken in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d6690-133">Find information about the JavaScript object libraries in SharePoint.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-the-client-object-model"></a><span data-ttu-id="d6690-134">Welche Verwendungsmöglichkeiten bietet das Clientobjektmodell?</span><span class="sxs-lookup"><span data-stu-id="d6690-134">What can you do with the client object model?</span></span>
<span data-ttu-id="d6690-135"><a name="BCScsom_Tasks"> </a></span><span class="sxs-lookup"><span data-stu-id="d6690-135"></span></span>

<span data-ttu-id="d6690-p103">Sie können das SharePoint-Clientobjektmodell zum Abrufen, Aktualisieren und Verwalten von Daten in SharePoint verwenden. SharePoint bietet die Clientbibliotheken in verschiedenen Formaten, um den Anforderungen der meisten Entwickler gerecht zu werden. Für Webentwickler, die Skriptsprachen verwenden, wird die Clientbibliothek inJavaScript angeboten. Für .NET-Entwickler wird sie als .NET-clientverwaltete DLL-Datei angeboten. Für Entwickler von Silverlight-Anwendungen wird die Clientbibliothek als Silverlight-DLL-Datei bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="d6690-p103">You can use the SharePoint client object model to retrieve, update, and manage data that is contained in SharePoint. SharePoint offers the client libraries in different formats to accommodate most developers. For web developers who are using scripting languages, the client library is offered in JavaScript. For .NET developers, it is offered as a .NET client managed DLL. For developers of Silverlight applications, the client library is provided by a Silverlight DLL.</span></span>
  
    
    
<span data-ttu-id="d6690-141">Weitere Informationen über Verwendungsmöglichkeiten des Clientobjektmodells in SharePoint finden Sie in den in Tabelle 2 aufgeführten Artikeln.</span><span class="sxs-lookup"><span data-stu-id="d6690-141">See the articles in Table 2 for more information about what you can do with the client object model in SharePoint.</span></span>
  
    
    

<span data-ttu-id="d6690-142">**Tabelle 2. Allgemeine Aufgaben beim Verwenden des Clientobjektmodells mit externen Daten**</span><span class="sxs-lookup"><span data-stu-id="d6690-142">**Table 2. Basic tasks for using the client object model with external data**</span></span>


|<span data-ttu-id="d6690-143">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="d6690-143">**Task**</span></span>|<span data-ttu-id="d6690-144">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d6690-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d6690-145">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="d6690-145">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |<span data-ttu-id="d6690-146">Hier erfahren Sie, wie Sie Code zum Ausführen grundlegender Vorgänge mit dem SharePoint-Clientobjektmodell schreiben.</span><span class="sxs-lookup"><span data-stu-id="d6690-146">Learn how to write code to perform basic operations with the SharePoint client object model.</span></span>  <br/> |
| [<span data-ttu-id="d6690-147">Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-147">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="d6690-148">In diesem Artikel erfahren Sie, wie Sie das SharePoint-Clientobjektmodell verwenden, um mit SharePoint BCS-Objekten mithilfe von browserbasierten Skripts zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="d6690-148">Learn how to use the SharePoint client object model to work with SharePoint BCS objects using browser-based scripting.</span></span>  <br/> |
   
<span data-ttu-id="d6690-149">Im folgenden werden einige Beispiele für allgemeine Aufgaben aufgeführt, die Sie mit dem Clientobjektmodell (CSOM) durchführen können.</span><span class="sxs-lookup"><span data-stu-id="d6690-149">The following are some basic examples of tasks you can accomplish using CSOM.</span></span>
  
    
    

### <a name="get-a-specific-entity"></a><span data-ttu-id="d6690-150">Abrufen einer bestimmten Entität</span><span class="sxs-lookup"><span data-stu-id="d6690-150">Get a specific entity</span></span>

<span data-ttu-id="d6690-151">In diesem Beispiel wird gezeigt, wie Sie Kontext aus SharePoint abrufen und dann eine bestimmte Datenquellenentität abrufen.</span><span class="sxs-lookup"><span data-stu-id="d6690-151">This example shows how to get context from SharePoint, and then retrieve a specified data source entity.</span></span>
  
    
    

```cs

ClientContext ctx = new ClientContext("http://sharepointservername"); 
Web web = ctx.Web; 
ctx.Load(web); 
Entity entity = ctx.Web.GetEntity("http://sharepointservername", "EntityName"); 
ctx.Load(entity); 
ctx.ExecuteQuery(); 

```


### <a name="create-a-generic-invoker"></a><span data-ttu-id="d6690-152">Erstellen einer generischen aufrufenden Instanz</span><span class="sxs-lookup"><span data-stu-id="d6690-152">Create a generic invoker</span></span>

<span data-ttu-id="d6690-153">In diesem Beispiel wird gezeigt, wie Sie eine generische aufrufende Instanz schreiben, damit Sie ein Entitätsobjekt für die Verwendung innerhalb des Codes erstellen können.</span><span class="sxs-lookup"><span data-stu-id="d6690-153">This example shows how to write a generic invoker so that you can create an entity object to work within your code.</span></span>
  
    
    

```cs

ObjectCollection myObj; 
entity.Execute("MethodInstanceName", lsi, myObj); 
ctx.Load(myObj); 
ctx.ExecuteQuery(); 

```


### <a name="retrieve-paged-result-sets"></a><span data-ttu-id="d6690-154">Abrufen von seitennummerierten Resultsets</span><span class="sxs-lookup"><span data-stu-id="d6690-154">Retrieve paged result sets</span></span>

<span data-ttu-id="d6690-p104">Das folgende Beispiel zeigt, wie sie ein gefiltertes, seitennummeriertes Dataset abrufen. In diesem Fall beträgt der Seitenwert 50.</span><span class="sxs-lookup"><span data-stu-id="d6690-p104">The following example shows how to retrieve a filtered, paged dataset. In this case, the page value is 50.</span></span>
  
    
    

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


### <a name="query-for-filtered-information"></a><span data-ttu-id="d6690-157">Abfragen gefilterter Informationen</span><span class="sxs-lookup"><span data-stu-id="d6690-157">Query for filtered information</span></span>

<span data-ttu-id="d6690-p105">Im folgenden Beispiel wird veranschaulicht, wie Sie ein gefiltertes Resultset zurückgeben können. In diesem Fall werden die Daten nach dem Feld **X.Y.Z.Country** gefiltert. Der Code such nach allen Elementen mit dem Wert „Indien" und fasst diese dann in einer Sammlung zusammen.</span><span class="sxs-lookup"><span data-stu-id="d6690-p105">The following example demonstrates how to return a filtered result set. In this case, the data column filtered is the **X.Y.Z.Country** field. The code looks for anything with the value of "India", and then puts that into a collection.</span></span>
  
    
    

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


## <a name="beyond-the-basics-learn-more-about-the-client-object-model"></a><span data-ttu-id="d6690-161">Weiterführendes: Weitere Informationen zum Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d6690-161">Beyond the basics: Learn more about the client object model</span></span>
<span data-ttu-id="d6690-162"><a name="BCScsom_Learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="d6690-162"></span></span>

<span data-ttu-id="d6690-163">Weitere Informationen zur Verwendung des Clientobjektmodells in SharePoint, finden Sie in Tabelle 3.</span><span class="sxs-lookup"><span data-stu-id="d6690-163">For more information about using the client object model in SharePoint, see the information in Table 3.</span></span>
  
    
    

<span data-ttu-id="d6690-164">**Tabelle 3. Erweiterte Konzepte für das Clientobjektmodell**</span><span class="sxs-lookup"><span data-stu-id="d6690-164">**Table 3. Advanced concepts for the client object model**</span></span>


|<span data-ttu-id="d6690-165">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="d6690-165">**Article**</span></span>|<span data-ttu-id="d6690-166">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d6690-166">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d6690-167">BCS-Client-Objektmodellreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-167">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md) <br/> |<span data-ttu-id="d6690-168">Zusammenfassung der für das Erstellen clientseitiger Skripts verfügbaren Objekte unter Verwendung des SharePoint-Clientobjektmodells für den Zugriff auf externe von BCS zur Verfügung gestellte Daten.</span><span class="sxs-lookup"><span data-stu-id="d6690-168">Summarizes the objects available for creating client-side scripts using the SharePoint client object model to access external data exposed by BCS.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="d6690-169">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d6690-169">Additional resources</span></span>
<span data-ttu-id="d6690-170"><a name="BCScsom_Learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="d6690-170"></span></span>


-  [<span data-ttu-id="d6690-171">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-171">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d6690-172">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d6690-172">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d6690-173">Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6690-173">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d6690-174">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="d6690-174">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d6690-175">SharePoint: Zugreifen auf komplexe externe Inhaltstypen mit CSOM</span><span class="sxs-lookup"><span data-stu-id="d6690-175">SharePoint: Access complex external content types with CSOM</span></span>](http://code.msdn.microsoft.com/office/SharePoint-Accessing-ccbc24cf)
    
  
