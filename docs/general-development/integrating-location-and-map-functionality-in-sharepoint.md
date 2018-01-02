---
title: Integrieren von Standort- und Kartenfunktionen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 10d4a904-ed27-4513-8c20-d2098aebf22c
ms.openlocfilehash: c6d72161076a589a32b5ca475a6350a2268dcd28
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="integrating-location-and-map-functionality-in-sharepoint"></a><span data-ttu-id="d7bc1-102">Integrieren von Standort- und Kartenfunktionen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-102">Integrating location and map functionality in SharePoint</span></span>
<span data-ttu-id="d7bc1-103">In diesem Artikel erfahren Sie, wie Sie Standortinformationen und Karten in SharePoint-Listen sowie standortbasierte Web-Apps und mobile Apps für SharePoint mithilfe des neuen Felds „Geolocation“ und durch Erstellen Ihrer eigenen auf dem Geolocation-Feld basierenden Feldtypen integrieren.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-103">Learn how to integrate location information and maps in SharePoint lists and location-based web and mobile apps for SharePoint, by using the new Geolocation field, and by creating your own Geolocation-based field types based on Geolocation.</span></span>
## <a name="what-are-the-location-and-map-features-in-sharepoint"></a><span data-ttu-id="d7bc1-104">Welche Standort- und Kartenfunktionen bietet SharePoint?</span><span class="sxs-lookup"><span data-stu-id="d7bc1-104">What are the location and map features in SharePoint?</span></span>
<span data-ttu-id="d7bc1-105"><a name="SP15Integrateloc_what"> </a></span><span class="sxs-lookup"><span data-stu-id="d7bc1-105"><a name="SP15Integrateloc_what"> </a></span></span>

<span data-ttu-id="d7bc1-106">SharePoint bietet jetzt einen neuen Feldtyp namens „Geolocation“, mit dem Sie SharePoint-Listen um Standortinformationen ergänzen können.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-106">SharePoint introduces a new field type named Geolocation that enables you to annotate SharePoint lists with location information.</span></span> <span data-ttu-id="d7bc1-107">In Spalten des Typs „Geolocation“ können Sie Standortinformationen als Paare von Breiten- und Längengraden in Dezimalgrad angeben oder die Koordinaten der aktuellen Position des Benutzers aus dem Browser abrufen, sofern dieser die W3C Geolocation API unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-107">In columns of type Geolocation, you can enter location information as a pair of latitude and longitude coordinates in decimal degrees or retrieve the coordinates of the user's current location from the browser if it implements the W3C Geolocation API.</span></span> <span data-ttu-id="d7bc1-108">In der Liste zeigt SharePoint den Standort dann auf einer über Bing Karten bereitgestellten Karte an.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-108">In the list, SharePoint displays the location on a map powered by Bing Maps.</span></span> <span data-ttu-id="d7bc1-109">Zusätzlich zeigt eine neue Ansicht namens „Kartenansicht“ die Listenelemente als Ortsmarken in einem Bing Karten-Ajax-Steuerelement (V7) an. Die Listenelemente werden als Karten im linken Bereich dargestellt.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-109">In addition, a new view named Map View displays the list items as pushpins on a Bing Maps Ajax control V7 with the list items as cards on the left pane.</span></span> <span data-ttu-id="d7bc1-110">Abbildung 1 gibt einen Überblick über die standardmäßigen Standort- und Kartenfunktionen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-110">Figure 1 summarizes the default location and map features in SharePoint.</span></span> <span data-ttu-id="d7bc1-111">In Kombination integrieren das Geolocation-Feld und die Kartenansicht Daten aus SharePoint in einer Kartenoberfläche und liefern so für jede Information räumlichen Kontext. Ihre Benutzer können auf ganz neue Art mit Ihren webbasierten und mobilen Apps und Lösungen interagieren.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-111">Together, the Geolocation field and the Map View enable you to give a spatial context to any information by integrating data from SharePoint into a mapping experience, and let your users engage in new ways in your web and mobile apps and solutions.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d7bc1-112">Sie müssen ein MSI-Paket mit dem Namen "SQLSysClrTypes.msi" auf jedem SharePoint-Front-End-Webserver installieren, um Geolocation-Feldwerte oder -Daten in einer Liste anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-112">An MSI package named SQLSysClrTypes.msi must be installed on every SharePoint front-end web server to view the geolocation field value or data in a list.</span></span> <span data-ttu-id="d7bc1-113">Dieses Paket installiert Komponenten, welche die neuen Geometrie-, Geografie- und Hierarchie-ID-Typen in SQL Server 2008 implementieren.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-113">This package installs components that implement the new geometry, geography, and hierarchy ID types in SQL Server 2008.</span></span> <span data-ttu-id="d7bc1-114">Für SharePoint Online wird diese Datei standardmäßig installiert.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-114">By default, this file is installed for SharePoint Online.</span></span> <span data-ttu-id="d7bc1-115">Dies gilt jedoch nicht für lokale Bereitstellungen von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-115">However, it is not for an on-premises deployment of SharePoint.</span></span> <span data-ttu-id="d7bc1-116">Sie müssen Mitglied der Gruppe „Farmadministratoren“ sein, um diesen Vorgang ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-116">You must be a member of the Farm Administrators group to perform this operation.</span></span> <span data-ttu-id="d7bc1-117">Herunterladen können Sie das Paket „SQLSysClrTypes.msi“ als Teil des [Microsoft SQL Server 2008 R2 SP1 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=26728) für SQL Server 2008 oder als Teil des [Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=29065) für SQL Server 2012 im Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-117">To download SQLSysClrTypes.msi, see  [Microsoft SQL Server 2008 R2 SP1 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=26728) for SQL Server 2008, or [Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=29065)for SQL Server 2012 in the Microsoft Download Center.</span></span> 
  
    
    


<span data-ttu-id="d7bc1-118">**Abbildung 1: Übersicht über die standardmäßigen Standort- und Kartenfunktionen**</span><span class="sxs-lookup"><span data-stu-id="d7bc1-118">**Figure 1.Summarized view of the default location and map features**</span></span>

  
    
    

  
    
    
![Standardmäßige Standort- und Kartenfunktionen](../images/SP15Con_HowToAddGeolocationColumn_fig.png)
  
    
    

  
    
    

  
    
    

## <a name="what-can-you-do-with-the-location-and-map-features"></a><span data-ttu-id="d7bc1-120">Wofür lassen sich die Standort- und Kartenfunktionen verwenden?</span><span class="sxs-lookup"><span data-stu-id="d7bc1-120">What can you do with the location and map features?</span></span>
<span data-ttu-id="d7bc1-121"><a name="SP15Integrateloc_do"> </a></span><span class="sxs-lookup"><span data-stu-id="d7bc1-121"><a name="SP15Integrateloc_do"> </a></span></span>

<span data-ttu-id="d7bc1-122">Die Standort- und Kartenfunktionen in SharePoint bieten Entwicklern einzigartige Möglichkeiten, Standortdaten, Karten und NEAR-Suchen in ihre webbasierten und mobilen Apps und Lösungen zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-122">The location and map features in SharePoint provide unique opportunities for developers to incorporate location, maps, and proximity search features into their web and mobile apps and solutions.</span></span> <span data-ttu-id="d7bc1-123">In Tabelle 1 finden Sie verschiedene grundlegende Aufgaben, mit denen Sie Standort- und Kartenfunktionen in Ihre Apps und Lösungen integrieren können.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-123">Table 1 contains some basic tasks that help you integrate location and map features in your apps and solutions.</span></span>
  
    
    

<span data-ttu-id="d7bc1-124">**Tabelle 1: Grundlegende Aufgaben zur Integration von Standort- und Kartenfunktionen**</span><span class="sxs-lookup"><span data-stu-id="d7bc1-124">**Table 1. Basic tasks for integrating location and maps functionality**</span></span>


|<span data-ttu-id="d7bc1-125">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="d7bc1-125">**Task**</span></span>|<span data-ttu-id="d7bc1-126">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d7bc1-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d7bc1-127">How to: Set the Bing Maps key at the web and farm level in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-127">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md) <br/> |<span data-ttu-id="d7bc1-128">SharePoint verwendet Bing Karten zum Rendern von Standortkarten.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-128">SharePoint uses Bings Maps to render the map of the location.</span></span> <span data-ttu-id="d7bc1-129">Um Bing Karten verwenden zu können, müssen Sie einen Bing Karten-Schlüssel erstellen und auf Website- oder Farmebene festlegen.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-129">To be able to use the Bing Maps feature, you need to create a Bing Maps key and set the key at the web or farm level.</span></span> <span data-ttu-id="d7bc1-130">In diesem Artikel werden die verschiedenen Optionen zur Festlegung des Schlüssels in SharePoint beschrieben. Außerdem erfahren Sie, wann Sie welche Option verwenden sollten.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-130">The article shows the various ways you can set the key in SharePoint and when to choose which option.</span></span> <span data-ttu-id="d7bc1-131">Wenn Sie keinen gültigen Bing Karten-Schlüssel verwenden oder kein Schlüssel auf Ebene der Farm oder der Website festgelegt ist, die die Liste enthält, wird eine Fehlermeldung auf der Karte angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-131">You see an error message on the map if you do not use a valid Bing Maps key or if a key is not set at the web that contains the list or at the farm level.</span></span>  <br/> |
| [<span data-ttu-id="d7bc1-132">How to: Add a Geolocation column to a list programmatically in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-132">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md) <br/> |<span data-ttu-id="d7bc1-p105">Die Geolocation-Spalte ist standardmäßig nicht in SharePoint-Listen für Benutzer verfügbar. Um die Spalte zu einer SharePoint-Liste hinzuzufügen, müssen Sie Code schreiben. Erfahren Sie in diesem Thema, wie das Geolocation-Feld programmgesteuert zu einer Liste hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-p105">The Geolocation column is not available in SharePoint lists for users, by default. To add the column to a SharePoint list, you need to write code. In this topic, learn how to add the Geolocation field to a list programmatically.</span></span>  <br/> |
| [<span data-ttu-id="d7bc1-136">Vorgehensweise: Erweitern des Geolocation-Feldtyps mithilfe von clientseitigem Rendering</span><span class="sxs-lookup"><span data-stu-id="d7bc1-136">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md) <br/> |<span data-ttu-id="d7bc1-137">Sie können eigenes Rendering auf die Standardbenutzeroberfläche (UI.md), die Logik und das Verhalten des Geolocation-Felds anwenden. Dazu erstellen Sie benutzerdefinierte Feldtypen, die vom Geolocation-Feld abgeleitet sind.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-137">You can provide your own rendering to default user interface (UI.md), logic, and behavior of the Geolocation field by creating custom field types that derive from the Geolocation field.</span></span> <span data-ttu-id="d7bc1-138">SharePoint erlaubt die Ausführung von JavaScript und vereinfacht so die Erstellung von benutzerdefinierten Feldtypen. In der Klasse für Geolocation-Felder steht jetzt eine neue JSLink-Eigenschaft zur Verfügung, die auf eine benutzerdefinierte .js-Datei verweist. Diese Datei wiederum rendert das Feld.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-138">SharePoint simplifies the creation of custom field types by enabling you to run JavaScript by providing a new JSLink property in the Geolocation field class, which points to a custom .js file that renders the field.</span></span>  <br/><br/> <span data-ttu-id="d7bc1-139">**Hinweis:** Die JSLink-Eigenschaft wird für Umfrage- oder Ereignislisten nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-139">**Note:** The JSLink property is not supported on Survey or Events lists.</span></span> <span data-ttu-id="d7bc1-140">SharePoint-Kalender sind Terminlisten.</span><span class="sxs-lookup"><span data-stu-id="d7bc1-140">A SharePoint calendar is an Events list.</span></span>           |
   

## <a name="see-also"></a><span data-ttu-id="d7bc1-141">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d7bc1-141">See also</span></span>
<span data-ttu-id="d7bc1-142"><a name="SP15Integrateloc_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d7bc1-142"><a name="SP15Integrateloc_addlresources"> </a></span></span>


-  [<span data-ttu-id="d7bc1-143">How to: Add a Geolocation column to a list programmatically in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-143">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d7bc1-144">Vorgehensweise: Legen Sie die Bing Maps-Taste auf Ordnerebene Web und Farm in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-144">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d7bc1-145">Vorgehensweise: Erweitern des Geolocation-Feldtyps mithilfe von clientseitigem Rendering</span><span class="sxs-lookup"><span data-stu-id="d7bc1-145">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  
-  [<span data-ttu-id="d7bc1-146">How to: Integrate maps with Windows Phone apps and SharePoint lists</span><span class="sxs-lookup"><span data-stu-id="d7bc1-146">How to: Integrate maps with Windows Phone apps and SharePoint lists</span></span>](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [<span data-ttu-id="d7bc1-147">Verwenden des Standortfeldtyps in mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7bc1-147">Use the SharePoint location field type in mobile applications</span></span>](http://technet.microsoft.com/de-DE/library/fp161355%28v=office.15%29.aspx)
    
  
