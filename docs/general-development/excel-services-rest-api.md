---
title: Excel Services-REST-API
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32033fea-873c-4781-900a-6946906066b0
ms.openlocfilehash: 9672a0013f82b2878cda45a8936cade24aa29412
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-rest-api"></a><span data-ttu-id="8fd44-102">Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="8fd44-102">Excel Services REST API</span></span>

<span data-ttu-id="8fd44-103">Dieser Abschnitt enthält Informationen zur REST-API (Representational State Transfer) in Excel Services und erläutert deren Verwendungsweise.</span><span class="sxs-lookup"><span data-stu-id="8fd44-103">This section contains information about the Representational State Transfer (REST) API in Excel Services and explains how to use it.</span></span>
  
    
    


> <span data-ttu-id="8fd44-104">**Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal).</span><span class="sxs-lookup"><span data-stu-id="8fd44-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="8fd44-105">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="8fd44-105">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="related-sections"></a><span data-ttu-id="8fd44-106">Verwandte Abschnitte</span><span class="sxs-lookup"><span data-stu-id="8fd44-106">Related sections</span></span>


 [<span data-ttu-id="8fd44-107">Excel Services-REST-API (Übersicht)</span><span class="sxs-lookup"><span data-stu-id="8fd44-107">Excel Services REST API Overview</span></span>](excel-services-rest-api-overview.md)
  
    
    
> <span data-ttu-id="8fd44-108">Informationen zur REST-API in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-108">Learn about the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-109">Grundlegende URI-Struktur und Pfad</span><span class="sxs-lookup"><span data-stu-id="8fd44-109">Basic URI Structure and Path</span></span>](basic-uri-structure-and-path.md)
  
    
    
> <span data-ttu-id="8fd44-110">Informationen zum Erstellen der URI-Struktur und des URI-Pfads für die Befehle des REST-Diensts in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-110">Learn how to construct the URI structure and path for the REST service commands in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-111">Ermittlung in der Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="8fd44-111">Discovery in Excel Services REST API</span></span>](discovery-in-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="8fd44-112">Informationen zu den in die REST-API integrierten Ermittlungsmechanismen in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-112">Learn about the discovery mechanisms built into the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-113">Ressourcen-URI für die REST API in Excel Services</span><span class="sxs-lookup"><span data-stu-id="8fd44-113">Resources URI for Excel Services REST API</span></span>](resources-uri-for-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="8fd44-114">Informationen zu den Entitäten, mit denen Sie mithilfe der REST-API in Excel Services eine direkte Verknüpfung herstellen können.</span><span class="sxs-lookup"><span data-stu-id="8fd44-114">Learn the entities that you can link directly to by using the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-115">Zugreifen auf Bereiche mithilfe von ATOM-Feeds und HTML-Fragmenten</span><span class="sxs-lookup"><span data-stu-id="8fd44-115">Getting Ranges Using Atom Feed and HTML Fragment</span></span>](getting-ranges-using-atom-feed-and-html-fragment.md)
  
    
    
> <span data-ttu-id="8fd44-116">Informationen zum Zugriff auf Bereiche - ATOM-Feeds und HTML-Fragmente - mithilfe der REST-API in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-116">Learn to access ranges—Atom feeds and HTML fragments—by using the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-117">Beispiel-URI für die REST-API in Excel Services</span><span class="sxs-lookup"><span data-stu-id="8fd44-117">Sample URI For Excel Services REST API</span></span>](sample-uri-for-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="8fd44-118">Ein Beispiel-URI für die Befehle des REST-Diensts in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-118">Provides a sample URI for the REST service commands in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-119">Zugreifen auf ein Schema</span><span class="sxs-lookup"><span data-stu-id="8fd44-119">Accessing a Schema</span></span>](accessing-a-schema.md)
  
    
    
> <span data-ttu-id="8fd44-120">Informationen zum Öffnen und Anzeigen eines Schemas für den REST-Dienst in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="8fd44-120">Learn how to access and look at a schema for the REST service in Excel Services.</span></span>
    
  
 [<span data-ttu-id="8fd44-121">Nicht unterstützte Features in der REST-API in Excel Services</span><span class="sxs-lookup"><span data-stu-id="8fd44-121">Unsupported Features in Excel Services REST API</span></span>](unsupported-features-in-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="8fd44-122">Eine Liste wichtiger Features, die derzeit in der REST-API in Excel Services nicht unterstützt werden oder nicht funktionsfähig sind.</span><span class="sxs-lookup"><span data-stu-id="8fd44-122">Lists some of the more important features that are currently not supported or working in the Excel Services REST API.</span></span>
    
  
 [<span data-ttu-id="8fd44-123">Erweiterte Szenarien und weitere Beispiele</span><span class="sxs-lookup"><span data-stu-id="8fd44-123">Advanced Scenarios and Additional Samples</span></span>](advanced-scenarios-and-additional-samples.md)
  
    
    
> <span data-ttu-id="8fd44-124">Eine Beschreibung einiger erweiterter REST-Szenarien sowie Links zu weiteren Beispielen.</span><span class="sxs-lookup"><span data-stu-id="8fd44-124">Describes some advanced REST scenarios and provides links to additional samples.</span></span>
    
  

