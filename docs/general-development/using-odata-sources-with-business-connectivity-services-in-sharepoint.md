---
title: Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7a87e5bf-4428-4055-b113-7665a93e7326
ms.openlocfilehash: bfa67d4b9d7f3db5306c5bbc3ec1c92b727c1459
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="using-odata-sources-with-business-connectivity-services-in-sharepoint"></a><span data-ttu-id="76fda-102">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-102">Using OData sources with Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="76fda-103">Erfahren Sie mehr über die ersten Schritte bei der Erstellung externer Inhaltstypen auf der Basis von OData-Quellen und der Verwendung dieser Daten in SharePoint- oder Office 2013-Komponenten.</span><span class="sxs-lookup"><span data-stu-id="76fda-103">Learn how to get started creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>
## <a name="odata-and-the-odata-connector"></a><span data-ttu-id="76fda-104">OData und der OData-Connector</span><span class="sxs-lookup"><span data-stu-id="76fda-104">OData and the OData connector</span></span>
<span data-ttu-id="76fda-105"><a name="SP15getstartedOdata_whatisodata"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-105"><a name="SP15getstartedOdata_whatisodata"> </a></span></span>

<span data-ttu-id="76fda-p101">Mit dem Open Data-Protokoll (OData) können Sie auf eine Datenquelle wie eine Datenbank zugreifen, indem Sie zu einer speziell zusammengesetzten URL browsen. Dies ermöglicht einen vereinfachten Ansatz für das Verbinden und Arbeiten mit Datenquellen, die in einer Organisation gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="76fda-p101">The Open Data protocol (OData) lets you access a data source, such as a database, by browsing to a specially constructed URL. This allows for a simplified approach for connecting to and working with data sources that are hosted within an organization.</span></span> 
  
    
    
<span data-ttu-id="76fda-p102">OData ist ein Protokoll, das HTTP, Atom und JavaScript Object Notation (JSON) verwendet, damit Entwickler Anwendungen schreiben können, die mit einer ständig wachsenden Anzahl von Datenquellen kommunizieren können. Microsoft unterstützt die Erstellung dieses Standards als Möglichkeit, den Austausch von Daten zwischen Anwendungen und Datenspeichern zu ermöglichen, auf die aus dem Internet zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="76fda-p102">OData is a protocol that uses HTTP, Atom, and JavaScript Object Notation (JSON) to enable developers to write applications that communicate with an ever-growing number of data sources. Microsoft supports the creation of this standard as a way to enable the exchange of data between applications and data stores that can be accessed from the web.</span></span>
  
    
    
<span data-ttu-id="76fda-110">Der neue OData-Connector ermöglicht SharePoint die Kommunikation mit OData-Anbietern.</span><span class="sxs-lookup"><span data-stu-id="76fda-110">The new OData connector enables SharePoint to communicate with OData providers.</span></span>
  
    
    
<span data-ttu-id="76fda-p103">In SharePoint kann Business Connectivity Services (BCS) mit OData-Quellen, oder Produzenten, ohne direkt an die OData-Quelle codieren zu müssen. Produzenten stellen ihre Daten auf eine strukturierte Weise über einen Webdienst zur Verfügung. Einige Produzenten lassen möglicherweise einige Aktualisierung der zugrunde liegenden Daten zu, andere möglicherweise nur einen schreibgeschützten Zugriff. Für Zwecke der Werbung, welche Vorgänge verfügbar sind, hat der Produzent ein Dienstdokument, das unter einem angegebenen URL-Endpunkt gefunden werden kann. SharePoint ist bereits ein OData-Produzent. SharePoint-Listendaten werden als OData-Quelle für alle Verbraucher zur Verfügung gestellt, die über die entsprechenden Rechte verfügen.</span><span class="sxs-lookup"><span data-stu-id="76fda-p103">In SharePoint, Business Connectivity Services (BCS) can communicate with OData sources, or producers, without having to code directly to the OData source. Producers expose their data in a structured way via a web service. Some producers may allow updating of the underlying data, and some may allow only read access. For purposes of advertising what operations are available, the producer has a service document found at a specified URL endpoint. SharePoint is already a producer of OData. SharePoint list data is exposed as an OData source for any consumer that has the appropriate rights.</span></span>
  
    
    

### <a name="examples-of-odata-producers"></a><span data-ttu-id="76fda-117">Beispiele für OData-Produzenten</span><span class="sxs-lookup"><span data-stu-id="76fda-117">Examples of OData producers</span></span>
<span data-ttu-id="76fda-118"><a name="ExamplesOfODataProducers"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-118"><a name="ExamplesOfODataProducers"> </a></span></span>

<span data-ttu-id="76fda-p104">Im Folgenden finden Sie einige Beispiele für OData-Implementierungen. Diese Anwendungen und Dienste stellen ihre Daten über das OData-Protokoll zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="76fda-p104">The following are some examples of implementations of OData. These applications and services expose their data through the OData protocol.</span></span>
  
    
    

- <span data-ttu-id="76fda-121">SharePoint Foundation 2010</span><span class="sxs-lookup"><span data-stu-id="76fda-121">SharePoint Foundation 2010</span></span>
    
  
- <span data-ttu-id="76fda-122">SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="76fda-122">SharePoint Server 2010</span></span>
    
  
- <span data-ttu-id="76fda-123">SQL Azure</span><span class="sxs-lookup"><span data-stu-id="76fda-123">SQL Azure</span></span>
    
  
- <span data-ttu-id="76fda-124">Microsoft Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="76fda-124">Microsoft Azure Table Storage</span></span>
    
  
- <span data-ttu-id="76fda-125">Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="76fda-125">Microsoft Azure Marketplace</span></span>
    
  
-  <span data-ttu-id="76fda-126">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="76fda-126">SQL Server Reporting Services</span></span>
    
  
- <span data-ttu-id="76fda-127">Microsoft Dynamics CRM 2011</span><span class="sxs-lookup"><span data-stu-id="76fda-127">Microsoft Dynamics CRM 2011</span></span>
    
  
- <span data-ttu-id="76fda-128">Windows Live</span><span class="sxs-lookup"><span data-stu-id="76fda-128">Windows Live</span></span>
    
  
<span data-ttu-id="76fda-129">Eine Liste der Produzenten von OData-Diensten finden Sie auf der  [Open Data Protocol-Website](http://www.odata.org/ecosystem).</span><span class="sxs-lookup"><span data-stu-id="76fda-129">For a list of producers of OData services, see the  [Open Data Protocol website](http://www.odata.org/ecosystem).</span></span>
  
    
    

## <a name="prerequisites-for-working-with-the-bcs-odata-connector"></a><span data-ttu-id="76fda-130">Voraussetzungen für das Arbeiten mit dem BCS-OData-Connector</span><span class="sxs-lookup"><span data-stu-id="76fda-130">Prerequisites for working with the BCS OData connector</span></span>
<span data-ttu-id="76fda-131"><a name="SP15GetstartedOdata_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-131"><a name="SP15GetstartedOdata_prereq"> </a></span></span>

<span data-ttu-id="76fda-132">Zum Entwickeln von OData-basierten externen Inhaltstypen benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="76fda-132">To develop OData-based external content types, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="76fda-133">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="76fda-133">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="76fda-134">SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-134">SharePoint</span></span>
    
  
- <span data-ttu-id="76fda-135">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="76fda-135">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="76fda-136">Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76fda-136">For information about how to set up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="creating-external-content-types-for-odata-data-sources"></a><span data-ttu-id="76fda-137">Erstellen von externen Inhaltstypen für OData-Datenquellen</span><span class="sxs-lookup"><span data-stu-id="76fda-137">Creating external content types for OData data sources</span></span>
<span data-ttu-id="76fda-138"><a name="SP15GetstartedOdata_creatingECT"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-138"><a name="SP15GetstartedOdata_creatingECT"> </a></span></span>

<span data-ttu-id="76fda-p105">Damit SharePoint die von einem bestimmten OData-Produzenten zur Verfügung gestellten Daten verwenden kann, muss ein externer Inhaltstyp in SharePoint erstellt werden. Wie bei allen externen SharePoint-Inhaltstypen enthält dieser alle Konnektivitätsinformationen, die für die Verbindung und Kommunikation mit dem externen System erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="76fda-p105">For SharePoint to use the data exposed by a specific OData producer, an external content type must be created inside SharePoint. As with all SharePoint external content types, it contains all the connectivity information that is needed to connect and communicate with the external system.</span></span>
  
    
    
<span data-ttu-id="76fda-p106">Das Erstellen eines externen Inhaltstyps, der eine OData-Datenquelle verwendet, ähnelt der Erstellung beliebiger externer Inhaltstypen. Sie können Visual Studio 2012 verwenden, um automatisch externe OData-Inhaltstypen zu generieren. Sie stellen lediglich den REST-Endpunkt (Representational State Transfer) der OData-Quelle bereit, wenn Sie den externen Inhaltstyp erstellen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76fda-p106">Creating an external content type that uses an OData data source is similar to creating any external content type. You can use Visual Studio 2012 to automatically generate OData external content types. You merely provide the Representational State Transfer (REST) endpoint of the OData source when you create the external content type. For more information see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="76fda-145">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="76fda-145">In this section</span></span>
<span data-ttu-id="76fda-146"><a name="SP15GetstartedOdata_inthissect"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-146"><a name="SP15GetstartedOdata_inthissect"> </a></span></span>


-  [<span data-ttu-id="76fda-147">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-147">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76fda-148">Vorgehensweise: Erstellen einer OData-Datendiensts zur Verwendung als einer externen BCS-System</span><span class="sxs-lookup"><span data-stu-id="76fda-148">How to: Create an OData data service for use as a BCS external system</span></span>](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md)
    
  
-  [<span data-ttu-id="76fda-149">Vorgehensweise: Erstellen eine externe Liste mithilfe einer in SharePoint OData-Datenquelle</span><span class="sxs-lookup"><span data-stu-id="76fda-149">How to: Create an external list using an OData data source in SharePoint</span></span>](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="76fda-150">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="76fda-150">Additional resources</span></span>
<span data-ttu-id="76fda-151"><a name="SP15GetstartedOdata_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="76fda-151"><a name="SP15GetstartedOdata_addres"> </a></span></span>


-  [<span data-ttu-id="76fda-152">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-152">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76fda-153">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-153">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76fda-154">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-154">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76fda-155">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="76fda-155">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

