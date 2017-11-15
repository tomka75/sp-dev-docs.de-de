---
title: "BCS-REST-API-Referenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 364fb8d7-87d9-4be7-affd-90caba3cd0c0
ms.openlocfilehash: f33adf455a216d1a7dba82832d9bcf7051068cb0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="bcs-rest-api-reference-for-sharepoint"></a><span data-ttu-id="eb500-102">BCS-REST-API-Referenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb500-102">BCS REST API reference for SharePoint</span></span>

  
    
    
![Klassenbibliotheken und -verweise](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="eb500-104">Enthält Referenzinformationen zum Erstellen von URLs zum Aufrufen und Bearbeiten von externen Datenquellen, die mit Business Connectivity Services (BCS) in SharePoint Representational State Transfer (REST).</span><span class="sxs-lookup"><span data-stu-id="eb500-104">Contains reference information for constructing Representational State Transfer (REST) URLs to access and manipulate external data sources using Business Connectivity Services (BCS) in SharePoint.</span></span>
## <a name="using-restful-apis-to-access-external-data-in-sharepoint"></a><span data-ttu-id="eb500-105">Mithilfe von Rest-APIs Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb500-105">Using RESTful APIs to access external data in SharePoint</span></span>
<span data-ttu-id="eb500-106"><a name="bkmk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="eb500-106"></span></span>

<span data-ttu-id="eb500-p101">Die REST-Schnittstelle bereitgestellt von SharePoint können Sie die meisten SharePoint Ressourcen durch speziell gestalteten URLs zugreifen. Business Connectivity Services (BCS) verwendet diese Architektur für den Zugriff auf externe Daten.</span><span class="sxs-lookup"><span data-stu-id="eb500-p101">The REST interface provided by SharePoint enables you to access most SharePoint resources through specially constructed URLs. Business Connectivity Services (BCS) uses this architecture to provide access to external data.</span></span>
  
    
    
<span data-ttu-id="eb500-109">Sie können auf externe Daten zugreifen, indem Sie URLs auf gleiche Weise erstellen wie beim Zugriff auf Standardlistenelemente.</span><span class="sxs-lookup"><span data-stu-id="eb500-109">You can access external data by constructing URLs just as you would to access standard list items.</span></span>
  
    
    

> <span data-ttu-id="eb500-110">**Hinweis:** Zugriff auf Entitäten über BDC direkt wird nicht bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="eb500-110">**Note:** Access to entities through the BDC directly is not provided.</span></span> <span data-ttu-id="eb500-111">Zum Arbeiten mit externen Daten müssen Sie eine externe Liste erstellen und die REST-URLs für den Zugriff auf Listenelemente in einer externen Liste verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb500-111">Note Access to entities through the BDC directly is not provided. To work with external data, you must create an external list and use the REST URLs to access the list items contained in the external list.</span></span> 
  
    
    

<span data-ttu-id="eb500-112">Die unterstützten HTTP-Verben für die Arbeit mit externen Listen sind **GET**, **PUT**, **POST** und **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="eb500-112">The supported HTTP verbs for working with external lists are **GET**, **PUT**, **POST**, and **DELETE**.</span></span>
  
    
    
<span data-ttu-id="eb500-p103">Im Gegensatz zu mit normalen Listen können nicht Sie eine externe Liste mithilfe von REST erstellen. Sie müssen dies tun, durch das Erstellen eines BDC-Modells und einer externen Liste mithilfe von Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="eb500-p103">Unlike with normal lists, you can't create an external list using REST. You must do that by creating a BDC model and an external list using Visual Studio 2012.</span></span>
  
    
    
<span data-ttu-id="eb500-115">Die Informationen in Tabelle 1 veranschaulicht das Erstellen von Rest-URLs und die entsprechenden Client Objektmodellaufrufe und Bearbeiten von Daten aus externen Datenquellen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="eb500-115">The information in Table 1 shows how to construct RESTful URLs and the corresponding client object model calls to access and manipulate data from external data sources.</span></span>
  
    
    

<span data-ttu-id="eb500-116">**In Tabelle 1. Rest-URL-Formate für den Zugriff auf externe Daten**</span><span class="sxs-lookup"><span data-stu-id="eb500-116">**Table 1. RESTful URL formats for accessing external data**</span></span>


|<span data-ttu-id="eb500-117">**URL**</span><span class="sxs-lookup"><span data-stu-id="eb500-117">**URL**</span></span>|<span data-ttu-id="eb500-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="eb500-118">**Description**</span></span>|<span data-ttu-id="eb500-119">**HTTP-Methode**</span><span class="sxs-lookup"><span data-stu-id="eb500-119">**HTTP method**</span></span>|
|:-----|:-----|:-----|
| `http://[sharepointsite]/_api` <br/> |<span data-ttu-id="eb500-p104">Die Basis des eine REST-Anforderung. Das virtuelle Verzeichnis _api zugeordnet ist, um Aufrufe client.svc, wo das Clientobjektmodell verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="eb500-p104">The base of any REST request. The _api virtual directory is mapped to call into client.svc, where the client object model can be used.</span></span>  <br/> |<span data-ttu-id="eb500-122">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-122">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/web/title` <br/> |<span data-ttu-id="eb500-123">Ruft den Titel des aktuellen Web ab.</span><span class="sxs-lookup"><span data-stu-id="eb500-123">Retrieves the title of the current web.</span></span>  <br/> |<span data-ttu-id="eb500-124">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-124">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists` <br/> |<span data-ttu-id="eb500-125">Ruft alle Listen auf einer Website ab</span><span class="sxs-lookup"><span data-stu-id="eb500-125">Retrieves all lists on a site.</span></span>  <br/> |<span data-ttu-id="eb500-126">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-126">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')` <br/> |<span data-ttu-id="eb500-127">Ruft die Metadaten für eine angegebene Liste.</span><span class="sxs-lookup"><span data-stu-id="eb500-127">Retrieves the metadata for a specified list.</span></span>  <br/> |<span data-ttu-id="eb500-128">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-128">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')/items` <br/> |<span data-ttu-id="eb500-129">Ruft die Listenelemente in einer angegebenen Liste ab.</span><span class="sxs-lookup"><span data-stu-id="eb500-129">Retrieves the list items in a specified list.</span></span>  <br/> |<span data-ttu-id="eb500-130">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-130">GET</span></span>  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')?select=Title` <br/> |<span data-ttu-id="eb500-131">Ruft den Titel einer bestimmten Liste ab.</span><span class="sxs-lookup"><span data-stu-id="eb500-131">Retrieves the title of a specific list.</span></span>  <br/> |<span data-ttu-id="eb500-132">GET</span><span class="sxs-lookup"><span data-stu-id="eb500-132">GET</span></span>  <br/> |
   

## <a name="constructing-query-strings-for-filtering-data"></a><span data-ttu-id="eb500-133">Erstellen von Abfragezeichenfolgen zum Filtern von Daten</span><span class="sxs-lookup"><span data-stu-id="eb500-133">Constructing query strings for filtering data</span></span>
<span data-ttu-id="eb500-134"><a name="bkmk_constructquery"> </a></span><span class="sxs-lookup"><span data-stu-id="eb500-134"></span></span>

<span data-ttu-id="eb500-135">Um die zurückgegebene Datenmenge beschränken oder mehr Stellen für den Benutzer relevant die Filteroperationen gefunden in Tabelle 2 können Sie.</span><span class="sxs-lookup"><span data-stu-id="eb500-135">In order to limit the amount of data returned, or make it more relevant to the user, you can use the filter operations found in Table 2.</span></span>
  
    
    

<span data-ttu-id="eb500-136">**In Tabelle 2. Operatoren zum Filtern von Daten**</span><span class="sxs-lookup"><span data-stu-id="eb500-136">**Table 2. Operators for filtering data**</span></span>


|<span data-ttu-id="eb500-137">**Operator**</span><span class="sxs-lookup"><span data-stu-id="eb500-137">**Operator**</span></span>|<span data-ttu-id="eb500-138">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="eb500-138">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="eb500-139">EQ</span><span class="sxs-lookup"><span data-stu-id="eb500-139">EQ</span></span>  <br/> |<span data-ttu-id="eb500-140">Gleich</span><span class="sxs-lookup"><span data-stu-id="eb500-140">Equals</span></span>  <br/> <span data-ttu-id="eb500-141">**Hinweis:** Wenn Sie **EQ** zum Filtern verwenden, werden die Filterkriterien an das externe System übergeben, in dem Fall die Filterung auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="eb500-141">When you use **EQ** to filter, the filter criteria are passed to the external system where the filtering happens on the server.</span></span>          |
|<span data-ttu-id="eb500-142">GT</span><span class="sxs-lookup"><span data-stu-id="eb500-142">GT</span></span>  <br/> |<span data-ttu-id="eb500-143">Größer als</span><span class="sxs-lookup"><span data-stu-id="eb500-143">Greater Than</span></span>  <br/> <span data-ttu-id="eb500-144">**Hinweis:** Wenn Sie den **GT**-Operator verwenden, wird nur eine clientseitige Filterung ausgeführt. > Beispiel: `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` gibt alle Titel mit einer durchschnittlichen Bewertung über 3 zurück.</span><span class="sxs-lookup"><span data-stu-id="eb500-144">**Note:** When you use the **GT** operator, only client-side filtering is executed.> For example:  `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` returns all titles with an average rating over 3.</span></span>          |
   

> <span data-ttu-id="eb500-145">**Hinweis:** Zum Abrufen von Spalten, die Teil einer Zuordnung sind, müssen Sie explizit die Spalte in der URL mithilfe von **$select** in der Abfragezeichenfolge mit einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="eb500-145">**Note** To retrieve columns that are part of an association, you must explicitly include the column in the URL using **$select** in the query string.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="eb500-146">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="eb500-146">Additional resources</span></span>
<span data-ttu-id="eb500-147"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="eb500-147"></span></span>


-  [<span data-ttu-id="eb500-148">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb500-148">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="eb500-149">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="eb500-149">Complete basic operations using SharePoint REST endpoints</span></span>](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="eb500-150">Programmieren mit dem SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="eb500-150">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="eb500-151">SharePoint: Durchführen grundlegender Datenzugriffsoperationen mit REST in Apps</span><span class="sxs-lookup"><span data-stu-id="eb500-151">SharePoint: Perform basic data access operations by using REST in apps</span></span>](http://code.msdn.microsoft.com/SharePoint-Perform-335d925b)
    
  
-  [<span data-ttu-id="eb500-152">Auswählen des richtigen API-Satzes in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb500-152">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [<span data-ttu-id="eb500-153">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb500-153">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
