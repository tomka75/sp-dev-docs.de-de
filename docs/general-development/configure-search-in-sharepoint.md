---
title: Konfigurieren der Suche in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e447127c-2b11-4d65-b46e-01a18cdcdee5
ms.openlocfilehash: 0fa1ba925fd858ebef033a89bf98f0fe566fb167
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="configure-search-in-sharepoint"></a><span data-ttu-id="20fbf-102">Konfigurieren der Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="20fbf-102">Configure search in SharePoint</span></span>
<span data-ttu-id="20fbf-103">Erfahren Sie mehr über die zwei Arten von Anpassungen unter SharePoint-Suche: Hinzufügen einer benutzerdefinierten Wörtertrennung und Hinzufügen eines benutzerdefinierten Schritts zum Ändern von verwalteter Eigenschaften für die durchforsteten Elemente während der Inhaltsverarbeitung.</span><span class="sxs-lookup"><span data-stu-id="20fbf-103">Learn about the two types of customization in SharePoint Server 2013 search: adding a custom word breaker and adding a custom step to modify managed properties for crawled items during content processing.</span></span>
   

## <a name="adding-a-custom-word-breaker-in-sharepoint"></a><span data-ttu-id="20fbf-104">Hinzufügen einer benutzerdefinierten Wörtertrennung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="20fbf-104">Adding a custom word breaker in SharePoint</span></span>
<span data-ttu-id="20fbf-105"><a name="SP15configsearch_word"> </a></span><span class="sxs-lookup"><span data-stu-id="20fbf-105"></span></span>

<span data-ttu-id="20fbf-p101">Eine benutzerdefinierte Wörtertrennung kann zum Optimieren der Wörtertrennung Verhalten je nach Bedarf hinzugefügt werden. Eine benutzerdefinierte Wörtertrennung können Sie die vorhandenen Wörtertrennung der gleichen Sprache ersetzen. Alternativ können Sie eine benutzerdefinierte Wörtertrennung verwenden, ersetzen Sie die vorhandenen Wörtertrennung mit einer anderen Sprache.</span><span class="sxs-lookup"><span data-stu-id="20fbf-p101">A custom word breaker can be added to tune word breaking behavior according to your needs. You can use a custom word breaker to replace the existing word breaker of the same language. Alternately, you can use a custom word breaker to replace the existing word breaker with that of a different language.</span></span>
  
    
    

## <a name="adding-a-custom-step-to-modify-managed-properties-in-sharepoint"></a><span data-ttu-id="20fbf-109">Hinzufügen eines benutzerdefinierten Schritts zum Ändern von verwalteter Eigenschaften im SharePoint</span><span class="sxs-lookup"><span data-stu-id="20fbf-109">Adding a custom step to modify managed properties in SharePoint</span></span>
<span data-ttu-id="20fbf-110"><a name="SP15ConfigSearch_customstep"> </a></span><span class="sxs-lookup"><span data-stu-id="20fbf-110"></span></span>

<span data-ttu-id="20fbf-p102">So ändern Sie verwaltete Eigenschaften in Form von einem externen Inhaltserweiterung-Webdienst, kann ein benutzerdefinierter Schritt hinzugefügt werden. Der Webdienst Inhaltserweiterung ist ein Dienst, den Sie erstellen können, um eine Legende aus dem Web-Service-Client innerhalb der inhaltsverarbeitungskomponente zu erhalten. Eine konfigurierbare Nutzlast wird dann an den Webdienst übermittelt, und die Antwort wird mit durchforsteten Elements zusammengeführt, bevor es dem Suchindex hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="20fbf-p102">A custom step can be added to modify managed properties in the form of an external content enrichment web service. The content enrichment web service is a service that you can create to receive a callout from the web service client inside the content processing component. A configurable payload is then submitted to the web service, and the response is merged into the crawled item before it is added to the search index.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="20fbf-114">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="20fbf-114">In this section</span></span>
<span data-ttu-id="20fbf-115"><a name="SP15ConfigSearch_customstep"> </a></span><span class="sxs-lookup"><span data-stu-id="20fbf-115"></span></span>


-  [<span data-ttu-id="20fbf-116">Benutzerdefinierte Wörtertrennungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="20fbf-116">Custom word breakers in SharePoint Server 2013</span></span>](custom-word-breakers-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="20fbf-117">Benutzerdefinierte Inhaltsverarbeitung mit der Content Enrichment-Webdienstlegende</span><span class="sxs-lookup"><span data-stu-id="20fbf-117">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="20fbf-118">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="20fbf-118">Additional resources</span></span>
<span data-ttu-id="20fbf-119"><a name="SP15configsearch_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="20fbf-119"></span></span>


-  [<span data-ttu-id="20fbf-120">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="20fbf-120">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="20fbf-121">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="20fbf-121">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

