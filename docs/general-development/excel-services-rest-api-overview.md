---
title: "Excel Services-REST-API (Übersicht)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5872f311-e180-4578-ac80-2519c1081951
ms.openlocfilehash: 624336e751c28d7bacce26f88e6d9f7dc570c93c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-rest-api-overview"></a><span data-ttu-id="ad15d-102">Excel Services-REST-API (Übersicht)</span><span class="sxs-lookup"><span data-stu-id="ad15d-102">Excel Services REST API Overview</span></span>

<span data-ttu-id="ad15d-p101">Die REST-API in Excel Services ist neu in Microsoft SharePoint Server 2010. Mit der REST-API können Sie direkt über eine URL auf Arbeitsmappenteile oder Elemente zugreifen.</span><span class="sxs-lookup"><span data-stu-id="ad15d-p101">The REST API in Excel Services is new in Microsoft SharePoint Server 2010. By using the REST API, you can access workbook parts or elements directly through a URL.</span></span>
  
> [!NOTE]
> <span data-ttu-id="ad15d-105">Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ad15d-105">Note: The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="ad15d-106">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel)-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="ad15d-106">For For Office 365 Education, Business, and Enterprise accounts,, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel) endpoint.</span></span>
  
    
    


<span data-ttu-id="ad15d-107">REST-Dienste basieren auf zwei Anforderungen:</span><span class="sxs-lookup"><span data-stu-id="ad15d-107">REST services are based on two requirements:</span></span>
  
    
    


- <span data-ttu-id="ad15d-108">Ein zum Suchen von Netzwerkressourcen verwendetes Adressierungsschema</span><span class="sxs-lookup"><span data-stu-id="ad15d-108">An addressing scheme used to locate networked resources</span></span>
    
  
- <span data-ttu-id="ad15d-109">Eine Methodik zum Zurückgeben von Darstellungen dieser Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ad15d-109">A methodology for returning representations of these resources</span></span>
    
  
<span data-ttu-id="ad15d-p103">REST-Dienste sind ressourcenorientiert. Mit REST werden Daten in Ressourcen unterteilt, jede Ressource erhält eine URL, und Standardvorgänge werden in den Ressourcen implementiert, die Vorgänge wie das Erstellen, Abrufen, Aktualisieren und Löschen ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="ad15d-p103">REST services are resource-centric. With REST, data is divided into resources, each resource is given a URL, and standard operations are implemented on the resources, which enable operations like creation, retrieval, update, and deletion.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad15d-112">Weitere Informationen zum Unterschied zwischen REST-Diensten und benutzerdefinierten Webdiensten finden Sie unter [Benutzerdefinierter Dienst oder REST-Dienst](http://msdn.microsoft.com/de-DE/magazine/dd882522.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad15d-112">[Note:](http://msdn.microsoft.com/de-DE/magazine/dd882522.aspx) For more information about the difference between REST services and custom Web services, see  Custom Service or RESTful Service.</span></span> 
  
    
    

<span data-ttu-id="ad15d-p104">Mit einer REST-API für Excel Services können Vorgänge für Excel-Arbeitsmappen mithilfe von im HTTP-Standard angegebenen Vorgängen ausgeführt werden. Dies ermöglicht einen flexiblen, sicheren und einfacheren Mechanismus, um auf Excel Services-Inhalte zuzugreifen und diese zu bearbeiten.Mit den in die REST-API von Excel Services integrierten Ermittlungsmechanismen können Entwickler und Benutzer auch den Inhalt der Arbeitsmappe manuell oder programmgesteuert durchsuchen, indem sie einen  [ATOM](http://tools.ietf.org/html/rfc4287)-Feed bereitstellen, der Informationen zu den in einer bestimmten Arbeitsmappe vorhandenen Elementen enthält. Beispiele für die Ressourcen, auf die Sie über die REST-API zugreifen können, sind Diagramme, PivotTables und Tabellen.Mit dem ATOM-Feed der REST-API gelangen Sie einfacher zu den gewünschten Daten. Der Feed enthält durchsuchbare Elemente, mit denen jeder Codeabschnitt ermitteln kann, welche Elemente in einer Arbeitsmappe vorhanden sind.Weitere Informationen zum Zugriff auf den REST-Dienst und zu Beispiel-URIs für den REST-Dienst in Excel Services finden Sie unter  [Grundlegende URI-Struktur und Pfad](basic-uri-structure-and-path.md) und [Beispiel-URI für die REST-API in Excel Services](sample-uri-for-excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="ad15d-p104">A REST API for Excel Services enables operations against Excel workbooks by using operations specified in the HTTP standard. This allows for a flexible, secure, and simpler mechanism to access and manipulate Excel Services content.The discovery mechanisms built into the Excel Services REST API also enable developers and users to explore the content of the workbook manually or programmatically by supplying an  [Atom](http://tools.ietf.org/html/rfc4287) feed that contains information about the elements that reside in a specific workbook. Some examples of the resources that you can access through the REST API are charts, PivotTables, and tables.Using the Atom feed provided by the REST API is an easier way of getting to the data that you care about. The feed contains traversable elements that enable any piece of code to discover what elements exist in a workbook. For information about accessing the REST service and obtaining sample URIs for the REST service in Excel Services, see  [Basic URI Structure and Path](basic-uri-structure-and-path.md) and [Sample URI For Excel Services REST API](sample-uri-for-excel-services-rest-api.md).</span></span>
