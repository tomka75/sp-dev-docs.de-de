---
title: Business Connectivity Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 64b7d032-4b83-4e9e-bc08-f0a161af5457
ms.openlocfilehash: 3c29b9a8908930d0346d5206645f42cad8e9fbec
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="business-connectivity-services-in-sharepoint"></a><span data-ttu-id="1ed95-102">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-102">Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="1ed95-p101">Erfahren Sie, worum es sich bei Business Connectivity Services (BCS) handelt, welche Möglichkeiten es Ihnen bietet, und wie Sie in die Entwicklung von BCS-Anwendungen in SharePoint einsteigen. Sie können SharePoint als Zentrale für die Erstellung umfangreicher Produktivitäts- und Zusammenarbeitslösungen verwenden, die mit verschiedensten externen Systemen verwendet werden können. Business Connectivity Services (BCS) stellt die Infrastruktur bereit, die es SharePoint ermöglicht, Daten aus diesen externen Systemen in einem zentralen System zusammenzuführen. Die Tatsache, dass BCS eine flexible und umfassende Möglichkeit bietet, die externe Systemdatenquelle und die Interaktion mit dieser zu beschreiben, stellt ein überzeugendes Argument dafür dar, zusätzlich zu neuen SharePoint-Add-InsSharePoint als die zentrale Schnittstelle für die Arbeit mit Legacy-Geschäftssystemen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p101">Learn what Business Connectivity Services (BCS) is, what you can do with it, and the information you need to get started developing BCS applications in SharePoint. You can use SharePoint as a hub for creating rich productivity and collaboration solutions that can work with a variety of external systems. Business Connectivity Services (BCS) provides the infrastructure that enables SharePoint to bring data from those external systems into a central system. By providing a flexible and extensible means to describe the external system data source and how to interact with it, BCS makes a compelling argument for using SharePoint as the central interface for working with legacy business systems in addition to new SharePoint Add-ins.</span></span>
  
    
    


## <a name="what-can-bcs-do"></a><span data-ttu-id="1ed95-107">Welche Möglichkeiten bietet BCS?</span><span class="sxs-lookup"><span data-stu-id="1ed95-107">What can BCS do?</span></span>
<span data-ttu-id="1ed95-108"><a name="BCSoverview_Whatcanbcsdo"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-108"><a name="BCSoverview_Whatcanbcsdo"> </a></span></span>

<span data-ttu-id="1ed95-109">BCS bietet Mechanismen, mit denen erfahrenen Benutzern und Entwicklern sowie IT-Experten der Unternehmenseinheit folgende Aufgaben problemlos ausführen können:</span><span class="sxs-lookup"><span data-stu-id="1ed95-109">BCS provides mechanisms to enable experienced users, developers, and business unit IT professionals to do the following much more easily:</span></span>
  
    
    

- <span data-ttu-id="1ed95-110">Offenlegen externer Daten aus Unternehmensanwendungen, Webdiensten und OData-Diensten in SharePoint und Rich-Client-Office-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="1ed95-110">Reveal external data from enterprise applications, web services, and OData services in SharePoint and in rich-client Office applications.</span></span>
    
  
- <span data-ttu-id="1ed95-111">Bereitstellen von Office-Verhaltensweisen (z. B. Kontakte, Aufgaben und Termine) und Funktionen für externe Daten und Dienste.</span><span class="sxs-lookup"><span data-stu-id="1ed95-111">Provide Office-type behaviors (such as Contacts, Tasks, and Appointments) and capabilities to external data and services.</span></span>
    
  
- <span data-ttu-id="1ed95-112">Bereitstellen uneingeschränkter Interaktion mit den Daten, einschließlich Zurückschreibfunktionen von Office-Anwendungen und SharePoint Server in die zugrunde liegenden externen Systemdaten und Geschäftsobjekte</span><span class="sxs-lookup"><span data-stu-id="1ed95-112">Provide complete interaction with the data, including write-back capabilities from Office applications and SharePoint Server to the underlying external system data and business objects.</span></span>
    
  
- <span data-ttu-id="1ed95-113">Aktivieren der Offlineverwendung von externen Daten und Prozessen</span><span class="sxs-lookup"><span data-stu-id="1ed95-113">Enable offline use of external data and processes.</span></span>
    
  
- <span data-ttu-id="1ed95-114">Überwinden der Kluft zwischen der Welt unstrukturierter Dokumente und Personen und den entsprechenden strukturierten Daten, die in externen Systemen unerreichbar sind</span><span class="sxs-lookup"><span data-stu-id="1ed95-114">Bridge the unstructured world of documents and people and the appropriate structured data that is locked in external systems.</span></span>
    
  

## <a name="components-of-bcs"></a><span data-ttu-id="1ed95-115">Komponenten von BCS</span><span class="sxs-lookup"><span data-stu-id="1ed95-115">Components of BCS</span></span>
<span data-ttu-id="1ed95-116"><a name="bkmk_Components"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-116"><a name="bkmk_Components"> </a></span></span>

<span data-ttu-id="1ed95-117">Abbildung 1 zeigt die Features, die in SharePoint und Office 2013 enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="1ed95-117">Figure 1 shows the features that are included in SharePoint and Office 2013.</span></span>
  
    
    

<span data-ttu-id="1ed95-118">**Abbildung 1. Featuregruppe der Business Connectivity Services**</span><span class="sxs-lookup"><span data-stu-id="1ed95-118">**Figure 1. Business Connectivity Services feature set**</span></span>

  
    
    

  
    
    
![Business Connectivity Services-Featuregruppe](../images/BCSin2013FeatureSet.jpg)
  
    
    

  
    
    

  
    
    

## <a name="using-external-content-types-in-bcs"></a><span data-ttu-id="1ed95-120">Verwenden externer Inhaltstypen in BCS</span><span class="sxs-lookup"><span data-stu-id="1ed95-120">Using external content types in BCS</span></span>
<span data-ttu-id="1ed95-121"><a name="bkmk_UsingECTs"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-121"><a name="bkmk_UsingECTs"> </a></span></span>

<span data-ttu-id="1ed95-p102">Externe Inhaltstypen sind der Kern von BCS. Sie können damit die Metadaten und Verhaltensweisen einer Geschäftseinheit (etwa eines Kunden oder einer Bestellung) an einem zentralen Ort verwalten und wiederverwenden. Sie ermöglichen Benutzern, mit diesen externen Daten zu interagieren und sie auf sinnvollere Weise zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p102">External content types are the core of BCS. They enable you to manage and reuse the metadata and behaviors of a business entity, such as Customer or Order, from a central location. They enable users to interact with that external data and process it in a more meaningful way.</span></span>
  
    
    
<span data-ttu-id="1ed95-p103">Nehmen wir als Beispiel eine Geschäftsentität, etwa einen Kunden. Sie möchten in der Lage sein, aus Ihrer proprietären Datenbank Daten zu ziehen und damit in SharePoint zu arbeiten. Außerdem möchten Sie Ihren Außendienstmitarbeitern erlauben, Daten in Outlook 2013 offline zu nehmen. Es kann auch sein, dass Sie möchten, dass der Benutzer aus einer Liste von Kunden in einem Bestellvertragsdokument in Microsoft Word einen Kunden auswählen kann. Für all diese Aufgaben können Sie einen einzelnen externen Inhaltstypen erstellen und ihn dann überall wiederverwenden, wo Sie ihn benötigen.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p103">For example, consider a business entity, such as a customer. You want to be able to pull data from your proprietary database and work with it in SharePoint. You also want to be able to allow your field salespeople to take data offline in Outlook 2013. Or, you might want the user to be able to choose a customer from a list of customers in an orders contract document inside Microsoft Word. To make all this possible, you can create a single external content type and then reuse it anywhere you need it.</span></span>
  
    
    
<span data-ttu-id="1ed95-130">Weitere Informationen zur Verwendung externer Inhaltstypen in BCS finden Sie unter  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1ed95-130">For more information about using external content types in BCS, see  [External content types in SharePoint](external-content-types-in-sharepoint.md).</span></span>
  
    
    

## <a name="developing-solutions-using-bcs"></a><span data-ttu-id="1ed95-131">Entwickeln von Lösungen mit BCS</span><span class="sxs-lookup"><span data-stu-id="1ed95-131">Developing solutions using BCS</span></span>
<span data-ttu-id="1ed95-132"><a name="bkmk_DevelopingSolutionsUsingBCS"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-132"><a name="bkmk_DevelopingSolutionsUsingBCS"> </a></span></span>

<span data-ttu-id="1ed95-p104">Sie können in SharePoint mit BCS eine breite Palette von Lösungen erstellen. Dazu zählen einfache Lösungen, die auf nativen Funktionen basieren, für die nur geringfügige oder keine Anpassungen erforderlich sind, mittlere Lösungen, für die Features in SharePoint und Office 2013 angepasst werden müssen, und erweiterte Lösungen, die komplexe Szenarios und reichhaltige Anwendungen ermöglichen, die deren Funktionsumfang erweitern. Für erweiterte Lösungen muss mithilfe von Visual Studio Code geschrieben werden. Dabei kann es sich entweder um vollständige End-to-End-Lösungen oder wiederverwendbare codebasierte Komponenten handeln, die in einer mittleren Lösung enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p104">You can build a broad spectrum of solutions in SharePoint by using BCS. These include simple solutions that rely on native capabilities with little or no customization, intermediate solutions that involve customizing features in SharePoint and Office 2013, and advanced solutions that enable complex scenarios and rich applications that extend their functionality. Advanced solutions involve writing code using Visual Studio. They can be either complete end-to-end solutions, or reusable code-based components that are included in an intermediate solution.</span></span>
  
    
    
<span data-ttu-id="1ed95-p105">BCS ermöglicht Geschäftsbenutzern, mithilfe eines Webbrowers oder einer Microsoft Office-Clientanwendung wie Word oder Excel auf schnelle und einfache Weise ein breites Spektrum an Anforderungen bezüglicher externer Daten zu erfüllen. Benutzer können, ohne Code zu schreiben, mithilfe von BCS-Features wie externen Listen und Spalten für externe Daten und wiederverwendbaren BCS-Komponenten, die von Entwicklern erstellt und von der IT genehmigt werden, in Office-Clientanwendungen und SharePoint-Websites kombinierte Lösungen zusammenstellen. Diese Lösungen ermöglichen Geschäftsbenutzern (und ihren Teams), mit externen Daten so einfach wie mit SharePoint-Daten zu arbeiten - entweder offline oder verbunden oder direkt in Office 2013.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p105">BCS empowers business users to quickly and easily address a broad array of external data needs by using a web browser and a Microsoft Office client application, such as Word or Excel. Without writing code, users can assemble composite solutions by using BCS features, such as external lists and external data columns, and reusable BCS components, which are created by developers and approved by IT, in Office client applications and SharePoint sites. These solutions enable business users (and their teams) to work with external data as easily as with SharePoint data, either offline or connected, or directly in Office 2013.</span></span>
  
    
    
<span data-ttu-id="1ed95-140">Weitere Informationen zum Einstieg finden Sie unter  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1ed95-140">For information about how to get started, see  [Setting up a development environment for BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span></span>
  
    
    

## <a name="using-odata-with-business-connectivity-services-in-sharepoint"></a><span data-ttu-id="1ed95-141">Verwenden von OData mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-141">Using OData with Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="1ed95-142"><a name="bkmk_ODataInBCS"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-142"><a name="bkmk_ODataInBCS"> </a></span></span>

<span data-ttu-id="1ed95-p106">Das Open Data Protocol (OData) ist ein Webprotokoll, mit dem Sie mithilfe von Technologien wie HTTP, JavaScript Object Notation (JSON) und AtomPub dem Web Daten zur Verfügung stellen können. Der Zugriff auf die Daten erfolgt über speziell gestaltete URLs. Diese Architektur erlaubt Ihnen, über eine Vielzahl von Technologien mit Daten zu interagieren.</span><span class="sxs-lookup"><span data-stu-id="1ed95-p106">The Open Data Protocol (OData) is a web protocol that lets you expose data to the web using technologies such as HTTP, JavaScript Object Notation (JSON), and AtomPub. Access to the data is through specially constructed URLs. This architecture lets you interact with data using a variety of technologies.</span></span>
  
    
    
<span data-ttu-id="1ed95-146">Weitere Informationen finden Sie unter  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1ed95-146">For more information, see  [Using OData sources with Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="1ed95-147">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="1ed95-147">In this section</span></span>
<span data-ttu-id="1ed95-148"><a name="bkmk_inthissection"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-148"><a name="bkmk_inthissection"> </a></span></span>


-  [<span data-ttu-id="1ed95-149">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-149">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-150">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-150">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-151">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-151">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-152">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-152">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-153">Externe Ereignisse und Warnungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-153">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-154">Add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-154">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-155">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-155">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-156">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-156">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

## <a name="see-also"></a><span data-ttu-id="1ed95-157">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1ed95-157">See also</span></span>
<span data-ttu-id="1ed95-158"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed95-158"><a name="bkmk_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="1ed95-159">Hinzufügen von SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="1ed95-159">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="1ed95-160">Einrichten einer Entwicklungsumgebung für BCS in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed95-160">Setting up a development environment for BCS in SharePoint</span></span>](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1ed95-161">Übersicht über die SharePoint-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="1ed95-161">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  

