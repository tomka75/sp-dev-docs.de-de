---
title: Erste Schritte mit den Business Connectivity Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6bf3db0-db79-4b13-9834-891d24b2c9e5
ms.openlocfilehash: 71ff8cc2b13f8fc6dd9d65eab41cb2743d713f4f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-business-connectivity-services-in-sharepoint"></a><span data-ttu-id="2ba05-102">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-102">Get started with Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="2ba05-103">Lernen Sie die Grundlagen dessen, was Business Connectivity Services (BCS) für Entwickler von SharePoint-Lösungen bietet, sowie die ersten Schritte beim Verwenden von BCS in verschiedenen Arten von Lösungen.</span><span class="sxs-lookup"><span data-stu-id="2ba05-103">Learn the basics of what Business Connectivity Services (BCS) provides to developers of SharePoint solutions, along with how to get started using BCS in various types of solutions.</span></span>
## <a name="what-is-business-connectivity-services"></a><span data-ttu-id="2ba05-104">Was ist Business Connectivity Services?</span><span class="sxs-lookup"><span data-stu-id="2ba05-104">What is Business Connectivity Services?</span></span>

<span data-ttu-id="2ba05-105">Business Connectivity Services (BCS) wurden in SharePoint Server 2010 als eine Weiterentwicklung des Geschäftsdatenkatalogs in Office SharePoint Server 2007 eingeführt.</span><span class="sxs-lookup"><span data-stu-id="2ba05-105">Business Connectivity Services (BCS) was introduced in SharePoint Server 2010 as an evolution of the Business Data Catalog released in Office SharePoint Server 2007.</span></span> <span data-ttu-id="2ba05-106">BCS ermöglicht SharePoint das Arbeiten mit Daten, die extern gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-106">BCS enables SharePoint to work with data that is hosted externally.</span></span> <span data-ttu-id="2ba05-107">Mögliche Quellen können Datenbanken, Webdienste, Windows Communication Foundation (WCF)-Dienste, Open Data Protocol (OData)-Quellen und andere proprietäre Daten, auf die mithilfe einer benutzerdefinierten .NET-Assembly zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="2ba05-107">Possible sources can include databases, web services, Windows Communication Foundation (WCF) services, Open Data Protocol (OData) sources, and other proprietary data that is accessed by using custom .NET assemblies.</span></span>

<a href="#SP15GettingStartedBCS_WhatDoYouNeed"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_WhatCanYouDo"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_LearnMore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a>

   
<span data-ttu-id="2ba05-108">In einer dynamischen Arbeitsumgebung benötigen Information-Worker Zugriff auf Daten, die in separater Software enthalten sind, z. B.:</span><span class="sxs-lookup"><span data-stu-id="2ba05-108">In a dynamic workplace, information workers need access to data that resides in separate software worlds, for example:</span></span>
  
    
    

- <span data-ttu-id="2ba05-109">Strukturierte Daten in den Unternehmensanwendungen der Organisation, z. B. ERP- und CRM-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="2ba05-109">Structured data that exists in the organization's enterprise applications, such as enterprise resource planning (ERP) and customer resource management (CRM) applications.</span></span>
    
  
- <span data-ttu-id="2ba05-110">Unstrukturierte Daten in Geschäftsproduktivitätsanwendungen, z. B. solche in Microsoft Office, in Team- und Zusammenarbeitsanwendungen wie SharePoint und in Web 2.0-Diensten wie Internetanwendungen, Wikis, Blogs und sozialen Netzwerken.</span><span class="sxs-lookup"><span data-stu-id="2ba05-110">Unstructured data in business productivity applications, such as those in Microsoft Office, in team and collaboration applications such as SharePoint, and in Web 2.0 services such as Internet applications, wikis, blogs, and social networking sites.</span></span>
    
  
<span data-ttu-id="2ba05-p102">Obwohl die meisten Information-Worker die größte Zeit über innerhalb der Produktivitätsanwendungen arbeiten (z. B. der Microsoft Office-Umgebung, benötigen sie auch eine Möglichkeit zum Integrieren dieser Umgebung in die verwendeten Unternehmensanwendungen und Zusammenarbeitssoftware und Dienste. Der Geschäftsdatendatenkatalog stellt diese Funktion in SharePoint bereit.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p102">Although most information workers spend much of their work time within the productivity applications (for example, the Microsoft Office environment), they also need a way to integrate that environment with the enterprise applications and collaboration software and services they use. BCS provides that capability in SharePoint.</span></span>
  
    
    

## <a name="get-started-with-business-connectivity-services"></a><span data-ttu-id="2ba05-113">Erste Schritte mit den Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="2ba05-113">Get started with Business Connectivity Services</span></span>
<span data-ttu-id="2ba05-114"><a name="SP15GettingStartedBCS_WhatDoYouNeed"> </a></span><span class="sxs-lookup"><span data-stu-id="2ba05-114"></span></span>

<span data-ttu-id="2ba05-115">Sie benötigen zunächst Folgendes, um mit der Entwicklung mit Business Connectivity Services zu beginnen:</span><span class="sxs-lookup"><span data-stu-id="2ba05-115">To get started developing with BCS, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="2ba05-116">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-116">SharePoint</span></span>
    
  
- <span data-ttu-id="2ba05-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ba05-117">Visual Studio</span></span>
    
  
- <span data-ttu-id="2ba05-118">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2ba05-118">Office Developer Tools for Visual Studio 2012</span></span>
    
    <span data-ttu-id="2ba05-119">oder</span><span class="sxs-lookup"><span data-stu-id="2ba05-119">or</span></span>
    
  
- <span data-ttu-id="2ba05-120">SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="2ba05-120">SharePoint Designer</span></span>
    
  
<span data-ttu-id="2ba05-121">Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="2ba05-121">For information about how to set up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="business-connectivity-services-essentials"></a><span data-ttu-id="2ba05-122">Grundlagen zu Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="2ba05-122">Business Connectivity Services essentials</span></span>

<span data-ttu-id="2ba05-123">Die folgende Tabelle zeigt die Kernkonzepte, mit denen Sie sich vertraut machen müssen, bevor Sie mit der Entwicklung von BCS-Lösungen beginnen.</span><span class="sxs-lookup"><span data-stu-id="2ba05-123">The following table highlights the core concepts that you will need to be familiar with to start developing BCS solutions.</span></span>
  
    
    

<span data-ttu-id="2ba05-124">**Tabelle 1. Kernkonzepte zum Verständnis von BSC.**</span><span class="sxs-lookup"><span data-stu-id="2ba05-124">**Table 1. Core concepts for understanding BCS**</span></span>


|<span data-ttu-id="2ba05-125">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="2ba05-125">**Article**</span></span>|<span data-ttu-id="2ba05-126">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2ba05-126">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="2ba05-127">
  [Entity Data Model - Schlüsselkonzepte](http://msdn.microsoft.com/de-de/library/ee382840.aspx)</span><span class="sxs-lookup"><span data-stu-id="2ba05-127">[Entity Data Model Key Concepts](http://msdn.microsoft.com/de-de/library/ee382840.aspx)</span></span> <br/> |<span data-ttu-id="2ba05-p103">Das Entity Data Model (EDM) verwendet drei Schlüsselkonzepte zum Beschreiben der Datenstruktur: Entitätstyp, Zuordnungstyp und Eigenschaft. Dies sind die wichtigsten Konzepte beim Beschreiben der Datenstruktur in allen Implementierungen von EDM.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p103">The Entity Data Model (EDM) uses three key concepts to describe the structure of data: entity type, association type, and property. These are the most important concepts in describing the structure of data in any implementation of the EDM.</span></span>  <br/> |
| <span data-ttu-id="2ba05-130">
  [Grundlegende Sicherheitsmaßnahmen für Webanwendungen](http://msdn.microsoft.com/de-de/library/zdh19h94.aspx)</span><span class="sxs-lookup"><span data-stu-id="2ba05-130">[Basic Security Practices for Web Applications](http://msdn.microsoft.com/de-de/library/zdh19h94.aspx)</span></span> <br/> |<span data-ttu-id="2ba05-p104">Das Erstellen sicherer Webanwendungen ist ein sehr umfangreiches Thema. Sie müssen sich auch mit den Sicherheitsfunktionen des Windows-Betriebssystems vertraut machen, .NET Framework und ASP.NET. Es ist wichtig, zu verstehen, wie diese Sicherheitsfunktionen zu verwenden sind, um Bedrohungen entgegenzuwirken.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p104">The topic of creating a secure web application is extensive. It requires study to understand security vulnerabilities. You also need to become familiar with the security facilities of the Windows operating system, the .NET Framework, and ASP.NET. Finally, it is essential to understand how to use these security features to counter threats.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-135">WCF Data Services</span><span class="sxs-lookup"><span data-stu-id="2ba05-135">WCF Data Services</span></span>](http://msdn.microsoft.com/en-us/data/odata.aspx) <br/> |<span data-ttu-id="2ba05-136">WCF Data Services, früher ADO.NET Data Services genannt, ermöglichen die Erstellung und Verarbeitung von OData-Diensten für das Web.</span><span class="sxs-lookup"><span data-stu-id="2ba05-136">WCF Data Services, formerly known as ADO.NET Data Services, enable the creation and consumption of OData services for the web.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-137">Open Data Protocol (OData)</span><span class="sxs-lookup"><span data-stu-id="2ba05-137">Open Data Protocol (OData)</span></span>](http://www.odata.org) <br/> |<span data-ttu-id="2ba05-p105">OData ist ein Industriestandardprotokoll für den Zugriff auf Daten über URLs. Es befindet sich im Grunde über dem HTTP-Protokoll, um Funktionen mithilfe von vorhandenen HTTP-Verben zu lesen und zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p105">OData is an industry standard protocol for accessing data through URLs. It basically sits on top of the HTTP protocol to provide read and write functions using existing HTTP verbs.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-140">Internetinformationsdienste</span><span class="sxs-lookup"><span data-stu-id="2ba05-140">Internet Information Services</span></span>](http://www.iis.net/) <br/> |<span data-ttu-id="2ba05-p106">Internetinformationsdienste (IIS) ist eine Plattform, auf der SharePoint ausgeführt wird. Sie müssen nachvollziehen können, wie Websites, virtuelle Verzeichnisse, Webdienste, URLs, Websicherheit und weitere mit IIS verwandte Technologien erstellt werden können.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p106">Internet Information Services (IIS) is the platform that SharePoint runs on. You should understand how to create websites, virtual directories, web services, URLs, web security, and other technologies related to IIS.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-143">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-143">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-p107">Externe Inhaltstypen sind Beschreibungen externer Systeme, die sie darstellen. Sie können wiederverwendet werden, wenn sie in SharePoint importiert werden, und können zum Erstellen komplexer codefreier Lösungen mithilfe von SharePoint Designer 2013, Outlook 2013, Webparts, externen Listen und benutzerdefinierten Clientanwendungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p107">External content types are descriptions of the external systems that they represent. They are reusable when imported into SharePoint and can be used to create complex code-free solutions using SharePoint Designer 2013, Outlook 2013, Web Parts, external lists, and custom client applications.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-146">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-146">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-p108">SharePointbietet die Möglichkeit, auf alle Objekte über eine sorgfältig erstellte URL zuzugreifen. BCS wurde erweitert, um diese Funktionalität bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p108">SharePoint provides the ability to access all objects through a carefully constructed URL. BCS has been extended to provide this same functionality.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-business-connectivity-services"></a><span data-ttu-id="2ba05-149">Welche Möglichkeiten bieten Business Connectivity Services?</span><span class="sxs-lookup"><span data-stu-id="2ba05-149">What can you do with Business Connectivity Services?</span></span>
<span data-ttu-id="2ba05-150"><a name="SP15GettingStartedBCS_WhatCanYouDo"> </a></span><span class="sxs-lookup"><span data-stu-id="2ba05-150"></span></span>

<span data-ttu-id="2ba05-p109">Mit BCS können Sie Informationen aus verschiedenen Quellen zu SharePoint verschieben. Sie können beispielsweise Daten aus einer externen SQL Server-Datenbank, einem gewöhnlichen Webdienst, einem WCF-Dienst, aus proprietären Systemen und OData-Diensten zu SharePoint verschieben.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p109">With BCS, you can bring information into SharePoint from many different sources. For example, you can bring data from an external SQL Server database, a traditional web service, a WCF service, proprietary systems, and OData services.</span></span>
  
    
    

<span data-ttu-id="2ba05-153">**Tabelle 2. Allgemeine Aufgaben beim Arbeiten mit Business Connectivity Services**</span><span class="sxs-lookup"><span data-stu-id="2ba05-153">**Table 2. Basic tasks for working with Business Connectivity Services**</span></span>


|<span data-ttu-id="2ba05-154">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="2ba05-154">**Task**</span></span>|<span data-ttu-id="2ba05-155">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2ba05-155">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2ba05-156">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-156">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-157">Informationen zum Erstellen von externen Business Connectivity Services (BCS)-Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="2ba05-157">Learn about creating Business Connectivity Services (BCS) external content types.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-158">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-158">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-159">Hier erhalten Sie Informationen zu den ersten Schritten bei der Erstellung von auf OData-Quellen basierenden externen Inhaltstypen und der Verwendung dieser Daten in SharePoint oder Office-Komponenten.</span><span class="sxs-lookup"><span data-stu-id="2ba05-159">Find information that is needed to get started creating external content types based on OData sources and using that data in SharePoint or Office components.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-160">Vorgehensweise: Erstellen von externen Ereignisempfängern</span><span class="sxs-lookup"><span data-stu-id="2ba05-160">How to: Create external event receivers</span></span>](how-to-create-external-event-receivers.md) <br/> |<span data-ttu-id="2ba05-161">Informationen zu Konzepten hinter dem Erstellen von Ereignisempfängern, die externen Listen angefügt und ausgeführt werden, wenn die von dieser Liste dargestellten externen Daten aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-161">Learn the concepts behind creating event receivers that can be attached to external lists and will execute when the external data that the list represents is updated.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-162">Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-162">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-163">Erfahren Sie, wie Sie externe Inhaltstypen erstellen, die auf App-Ebene installiert oder vorhanden sind, und Entwicklern das Erstellen von Apps mit hohem Datenaufkommen mithilfe von externen Datenquellen ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="2ba05-163">Learn how to create external content types that are installed or scoped at the app level, enabling developers to create data-rich apps using external data sources.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-164">Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-164">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="2ba05-165">Erfahren Sie, wie Sie das SharePoint-Clientobjektmodell für die Arbeit mit BCS in SharePoint verwenden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-165">Learn how to use the SharePoint client object model to work with BCS in SharePoint.</span></span>  <br/> |
   

## <a name="beyond-the-basics-learn-more-about-business-connectivity-services"></a><span data-ttu-id="2ba05-166">Weiterführendes: Weitere Informationen zu Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="2ba05-166">Beyond the basics: Learn more about Business Connectivity Services</span></span>
<span data-ttu-id="2ba05-167"><a name="SP15GettingStartedBCS_LearnMore"> </a></span><span class="sxs-lookup"><span data-stu-id="2ba05-167"></span></span>

<span data-ttu-id="2ba05-168">Wenn Sie die grundlegenden Konzepte von BCS beherrschen, können Sie erweiterte Funktionen zum Erstellen leistungsstarker Lösungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-168">When you master the basic concepts of BCS, you can use the more advanced features to build many powerful types of solutions.</span></span>
  
    
    

<span data-ttu-id="2ba05-169">**Tabelle 3. Erweiterte Konzepte in BCS**</span><span class="sxs-lookup"><span data-stu-id="2ba05-169">**Table 3. Advanced concepts in BCS**</span></span>


|<span data-ttu-id="2ba05-170">**Thema**</span><span class="sxs-lookup"><span data-stu-id="2ba05-170">**Topic**</span></span>|<span data-ttu-id="2ba05-171">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2ba05-171">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2ba05-172">Vorgehensweise: Erstellen einer OData-Datendiensts zur Verwendung als einer externen BCS-System</span><span class="sxs-lookup"><span data-stu-id="2ba05-172">How to: Create an OData data service for use as a BCS external system</span></span>](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |<span data-ttu-id="2ba05-p110">In diesem Artikel erfahren sie, wie Sie einen im Internet aufrufbaren WCF-Dienst erstellen, der OData zum Senden von Benachrichtigungen an SharePoint verwendet, wenn die zugrunde liegenden Daten geändert werden. Mithilfe dieser Benachrichtigungen werden Ereignisse ausgelöst, die mit externen Listen verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="2ba05-p110">Learn how to create an Internet-addressable WCF service that uses OData to send notifications to SharePoint when the underlying data changes. These notifications are used to trigger events that are attached to external lists.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-175">BDC-Modell-Schemareferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-175">BDC model schema reference for SharePoint</span></span>](bdc-model-schema-reference-for-sharepoint.md) <br/> |<span data-ttu-id="2ba05-176">Hier finden Sie die Referenzdokumentation zum Schema des BDC-Modells.</span><span class="sxs-lookup"><span data-stu-id="2ba05-176">Find reference documentation for the schema of the BDC model.</span></span>  <br/> |
| [<span data-ttu-id="2ba05-177">BCS-Client-Objektmodellreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-177">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md) <br/> |<span data-ttu-id="2ba05-178">Zusammenfassung der für das Erstellen clientseitiger Skripts verfügbaren Objekte unter Verwendung des SharePoint-Clientobjektmodells für den Zugriff auf externe von Business Connectivity Services (BCS) zur Verfügung gestellte Daten.</span><span class="sxs-lookup"><span data-stu-id="2ba05-178">Get a summary of the objects that are available for creating client-side scripts using the SharePoint client object model to access external data exposed by Business Connectivity Services (BCS).</span></span>  <br/> |
| [<span data-ttu-id="2ba05-179">BCS-REST-API-Referenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-179">BCS REST API reference for SharePoint</span></span>](bcs-rest-api-reference-for-sharepoint.md) <br/> |<span data-ttu-id="2ba05-180">Hier erhalten Sie Referenzinformationen für das Erstellen von REST-URIs, die für den Zugriff und die Manipulation von OData-Quellen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2ba05-180">Find reference information for constructing Representational State Transfer (REST) URIs used for accessing and manipulating OData sources.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="2ba05-181">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2ba05-181">Additional resources</span></span>
<span data-ttu-id="2ba05-182"><a name="SP15GettingStartedBCS_LearnMore"> </a></span><span class="sxs-lookup"><span data-stu-id="2ba05-182"></span></span>


-  [<span data-ttu-id="2ba05-183">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-183">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ba05-184">Open Data Protocol-Website</span><span class="sxs-lookup"><span data-stu-id="2ba05-184">Open Data Protocol website</span></span>](http://www.odata.org/)
    
  
-  [<span data-ttu-id="2ba05-185">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-185">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ba05-186">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-186">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ba05-187">Externe Ereignisse und Warnungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-187">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ba05-188">Add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-188">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ba05-189">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ba05-189">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
