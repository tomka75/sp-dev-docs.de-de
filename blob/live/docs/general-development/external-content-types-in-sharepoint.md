---
title: Externe Inhaltstypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 11d7adb5-5388-4517-ae03-beb7be1c6981
ms.openlocfilehash: beac2fcaea11c5998a2b8a96291e45dc1ae5313e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="external-content-types-in-sharepoint"></a><span data-ttu-id="f1fe3-102">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-102">External content types in SharePoint</span></span>
<span data-ttu-id="f1fe3-103">Erfahren Sie, welche Möglichkeiten Ihnen externe Inhaltstypen bieten, und was Sie benötigen, um mit deren Erstellung in SharePoint zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-103">Learn what you can do with external content types and what you need to start creating them in SharePoint.</span></span>
## <a name="what-is-an-external-content-type"></a><span data-ttu-id="f1fe3-104">Was ist ein externer Inhaltstyp?</span><span class="sxs-lookup"><span data-stu-id="f1fe3-104">What is an external content type?</span></span>
<span data-ttu-id="f1fe3-105"><a name="SP15ectoverview_what"> </a></span><span class="sxs-lookup"><span data-stu-id="f1fe3-105"><a name="SP15ectoverview_what"> </a></span></span>

<span data-ttu-id="f1fe3-p101">Der externe Inhaltstyp ist ein zentrales Konzept von Business Connectivity Services (BCS). Externe Inhaltstypen werden für sämtliche Funktionen und Dienste verwendet, die von BCS geboten werden, und stellen wiederverwendbare Metadatenbeschreibungen von Konnektivitätsinformationen und Datendefinitionen sowie deren Verhalten dar, die Sie auf eine bestimmte Kategorie externer Daten anwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p101">The external content type is a core concept of Business Connectivity Services (BCS). Used throughout the functionality and services offered by BCS, external content types are reusable metadata descriptions of connectivity information and data definitions plus the behaviors you want to apply to a certain category of external data.</span></span>
  
    
    
<span data-ttu-id="f1fe3-108">Mit externen Inhaltstypen können Sie die Metadaten und Verhaltensweisen einer Geschäftsentität (etwa eines Kunden oder einer Bestellung) an einem zentralen Ort verwalten und wiederverwenden, und Benutzer können mit diesen externen Daten und Prozessen auf sinnvollere Weise interagieren.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-108">External content types enable you to manage and reuse the metadata and behaviors of a business entity, such as a customer or order from a central location, and enable users to interact with that external data and processes in a more meaningful way.</span></span>
  
    
    
<span data-ttu-id="f1fe3-109">Hier einige der Vorteile der Verwendung externer Inhaltstypen:</span><span class="sxs-lookup"><span data-stu-id="f1fe3-109">The following are some of the benefits of using external content types:</span></span>
  
    
    

- <span data-ttu-id="f1fe3-p102">**Wiederverwendbarkeit:** Ein externer Inhaltstyp ist eine wiederverwendbare Datendefinition einer Geschäftsentität. Nachdem Sie sie erstellt haben, können Sie sie mit jeder der Präsentationsfeatures in BCS verwenden, um die Interaktion mit externen Daten benutzerfreundlich zu gestalten.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p102">**Provide reusability:** An external content type is a reusable data definition of a business entity. After you create it, you can use it with any of the presentation features in BCS to provide a rich user experience to interact with external data.</span></span>
    
  
- <span data-ttu-id="f1fe3-p103">**Kapseln von Komplexitäten externer Systeme:** Externe Inhaltstypen ermöglichen Information Workern, Geschäftslösungen zusammenzustellen, ohne die Komplexitäten der externen Systeme, wie Konnektivitätsinformationen und Codeschnittstellen, berücksichtigen zu müssen. Sobald ein Benutzer einen externen Inhaltstyp erstellt hat, steht dieser allen Benutzern zur beliebigen Verwendung zur Verfügung (solange sie die Berechtigungen zum Durchführen dieses Vorgangs sowie Zugriff auf die externen Daten besitzen). Der Benutzer muss allerdings nichts über den Speicherort der externen Daten oder die Verbindung zu diesen wissen.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p103">**Encapsulate complexities of external systems:** External content types enable information workers to assemble business solutions without having to handle the complexities of the external systems, such as connectivity information and code interfaces. After someone creates an external content type, it is available to users for use in any way they need (provided they have the permissions to perform that operation and access the external data). However, the user does not need to know anything about the location of the external data or how to connect to it.</span></span>
    
  
- <span data-ttu-id="f1fe3-p104">**Bereitstellen von integriertem Office- und SharePoint-Verhalten:** Externe Inhaltstypen stellen für externe Daten und Services Office-elementartige Verhaltensweisen (wie Kontakte, Aufgaben, Kalender Outlook, Dokumente in Word und Listen in SharePoint Workspace), SharePoint-Verhaltensweisen (wie Listen, Webparts und Profilseiten) und Funktionen (wie die Fähigkeit zur Offlinesuche oder -arbeit) bereit. Dadurch können Benutzer in ihren vertrauten Arbeitsumgebungen arbeiten, ohne nach Daten suchen oder andere (und proprietäre) Benutzeroberflächen verwenden zu müssen.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p104">**Provide built-in Office and SharePoint behavior:** External content types provide Office item-type behaviors (such as Contacts, Tasks, Calendars in Outlook, documents in Word, and lists in SharePoint Workspace); SharePoint behaviors (such as lists, Web Parts, and profile pages); and capabilities (such as the ability to search or work offline) to external data and services. So users can work in their familiar work environments without having to hunt for data or learn and interact with different (and proprietary) user interfaces.</span></span>
    
  
- <span data-ttu-id="f1fe3-p105">**Unterstützung bei der Bereitstellung von sichererem Zugriff:** Externe Inhaltstypen halten die vom externen System und SharePoint verwendeten Sicherheitsmechanismen ein. Durch die Konfiguration von Sicherheitseinstellungen in SharePoint können Sie genau steuern, wer auf welche Daten zugreift.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p105">**Help provide more secure access:** External content types adhere to the security put in place by both the external system and SharePoint. You can have full control of who accesses what data by configuring security in SharePoint.</span></span>
    
  
- <span data-ttu-id="f1fe3-p106">**Vereinfachen der Verwaltung:** Da externe Inhaltstypen einmal erstellt und von mehreren Lösungen in verschiedenen Szenarios verwendet werden können, können Sie sie leicht verwalten. So können Sie z. B. deren Zugriffsberechtigungen sowie deren Verbindungs- und Datendefinitionen an einem zentralen Ort verwalten.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p106">**Simplify maintenance:** Because external content types can be created once and used by multiple solutions in various scenarios, you can manage them easily. For example, you can manage their access permissions and connection and data definitions in one central location.</span></span>
    
  
- <span data-ttu-id="f1fe3-p107">**Ermöglichen einer externen Datensuche:** Sie können von einem Intranetportal aus SharePoint Server-Suchdienst verwenden, um Informationen über einen bestimmten externen Inhaltstyp wie einen Kunden nachzuschlagen. SharePoint Server-Suchdienst ruft die Daten direkt aus dem externen System ab. Daher können Benutzer die Informationen erhalten, die sie benötigen, ohne eine Genehmigung einzuholen oder eine separate Anwendung zu installieren.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p107">**Enable external data search:** You can use SharePoint Server search from an intranet portal to look up information about a specific external content type, such as a customer. SharePoint Server search retrieves the data directly from the external system. Consequently, users can get the information they need without having to get approval or install a separate application.</span></span>
    
  
- <span data-ttu-id="f1fe3-p108">**Ermöglichen von Offlinearbeit:** Sie können externe Inhaltstypen in Outlook 2013 offline verwenden. Business Connectivity Services (BCS) bietet umfangreiche Features für Caching und die Offlinearbeit und unterstützt cachebasierte Vorgänge. Benutzer können externe Daten nahtlos und effizient bearbeiten, auch wenn sie offline sind oder die Serverbindung langsam, unterbrochen oder nicht verfügbar ist. Die Lese-/Schreibvorgänge, die an zwischengespeicherten Geschäftsentitäten durchgeführt werden, werden synchronisiert, sobald eine Verbindung zum Server verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p108">**Enable working offline:** You can take external content types offline in Outlook 2013. Business Connectivity Services (BCS) provides rich cache and offline work features and supports cache-based operations. Users can manipulate external data seamlessly and efficiently, even when they are offline or if the server connectivity is slow, intermittent, or unavailable. The read/write operations performed against cached business entities are synchronized when a connection to the server becomes available.</span></span>
    
  

## <a name="prerequisites-for-working-with-bcs-external-content-types"></a><span data-ttu-id="f1fe3-128">Voraussetzungen für das Arbeiten mit externen BCS-Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="f1fe3-128">Prerequisites for working with BCS external content types</span></span>
<span data-ttu-id="f1fe3-129"><a name="SP15ectoverview_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="f1fe3-129"><a name="SP15ectoverview_prereq"> </a></span></span>

<span data-ttu-id="f1fe3-130">Um mit der Erstellung externer Inhaltstypen beginnen zu können, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f1fe3-130">To get started creating external content types, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="f1fe3-131">SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-131">SharePoint</span></span>
    
  
- <span data-ttu-id="f1fe3-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f1fe3-132">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="f1fe3-133">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f1fe3-133">Office Developer Tools for Visual Studio 2012</span></span>
    
    <span data-ttu-id="f1fe3-134">oder</span><span class="sxs-lookup"><span data-stu-id="f1fe3-134">or</span></span>
    
  
- <span data-ttu-id="f1fe3-135">SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="f1fe3-135">SharePoint Designer 2013</span></span>
    
  
<span data-ttu-id="f1fe3-136">Informationen zur Einrichtung einer Entwicklungsumgebung zur Erstellung externer Inhaltstypen finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f1fe3-136">To set up a development environment for creating external content types, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="what-can-you-do-with-external-content-types"></a><span data-ttu-id="f1fe3-137">Welche Möglichkeiten bieten externe Inhaltstypen?</span><span class="sxs-lookup"><span data-stu-id="f1fe3-137">What can you do with external content types?</span></span>
<span data-ttu-id="f1fe3-138"><a name="SP15ectoverview_whattodo"> </a></span><span class="sxs-lookup"><span data-stu-id="f1fe3-138"><a name="SP15ectoverview_whattodo"> </a></span></span>

<span data-ttu-id="f1fe3-139">Wenn SharePoint so konfiguriert ist, dass es mit dem externen System kommuniziert, können Sie mithilfe der externen Inhaltstypen die folgenden Objekte erstellen, um die zugrunde liegenden Daten darzustellen:</span><span class="sxs-lookup"><span data-stu-id="f1fe3-139">When SharePoint is configured to communicate with the external system, you can use the external content types to create the following objects to present the underlying data:</span></span>
  
    
    

- <span data-ttu-id="f1fe3-140">**Externe Listen**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-140">**External lists**</span></span>
    
    <span data-ttu-id="f1fe3-p109">Eine externe Liste ermöglicht auf die gleiche Weise, wie auf SharePoint-Listendaten zugegriffen wird, Zugriff auf Daten in externen Systemen. Externe Listen verwenden externe Inhaltstypen als ihre Datenquellen. Mithilfe externer Listen können Sie die Metadaten verwenden, die bereits über einen externen Inhaltstyp definiert sind, um eine SharePoint-Liste zu erstellen, die externe Daten enthält und das gleiche Aussehen und Verhalten wie jede andere SharePoint-Liste aufweist.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p109">An external list enables access to data from external systems in the same way that SharePoint list data is accessed. External lists use external content types as their data sources. External lists enable you to use the metadata that is already defined about an external content type to create a SharePoint list that has external data that looks and performs like any other SharePoint list.</span></span>
    
    <span data-ttu-id="f1fe3-p110">Sie können externe Listen auch offline nehmen, um sie in Outlook 2013 zu verwenden. So können Sie mit externen Daten wie mit systemeigenen Outlook-Elementtypen wie Kontakten, Aufgaben und Beiträgen arbeiten, und die externen Daten in Office-Clientanwendungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p110">You can also take external lists offline to be used in Outlook 2013. This allows you to work with external data just like native Outlook Item types, such as Contacts, Tasks, and Posts, and use the external data in Office client applications.</span></span>
    
    <span data-ttu-id="f1fe3-p111">Bei externen Listen können Sie in das externe System zurückschreiben, wenn dies vom externen System erlaubt wird und es vom externen Inhaltstyp entsprechend modelliert wurde. Dies impliziert, dass Benutzer externe Daten direkt in der Liste bearbeiten können. Alle Änderungen, die an den Elementen in der Liste vorgenommen wurden, werden automatisch mit dem externen System synchronisiert. Außerdem können Sie mithilfe der Schaltfläche **Daten aktualisieren** in der Liste Daten synchronisieren und aktualisierte Daten vom externen System automatisch erhalten.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p111">External lists enable writing back to the external system if the external system allows it, and if it is modeled accordingly by the external content type. This implies that users can edit external data directly from within. Any changes that were made to the items in the list are synchronized automatically with the external system. Also by using the **Refresh data** button in the list, you can synchronize and get updated data from the external system automatically.</span></span>
    
  
- <span data-ttu-id="f1fe3-150">**Externe Datenspalten**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-150">**External Data Columns**</span></span>
    
    <span data-ttu-id="f1fe3-p112">Mithilfe der externen Datenspalte können Benutzer Daten aus externen Inhaltstypen zu standardmäßigen SharePoint-Listen hinzufügen. Wie eine externe Liste können externe Datenspalten Daten von jedem externen Inhaltstyp anzeigen, der in Business Connectivity Services (BCS) modelliert wurde.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p112">The external data column enables users to add data from external content types to standard SharePoint lists. Just like an external list, external data columns can display data from any external content type that is modeled in Business Connectivity Services (BCS).</span></span>
    
  
- <span data-ttu-id="f1fe3-153">**Geschäftsdaten-Webparts**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-153">**Business Data Web Parts**</span></span>
    
    <span data-ttu-id="f1fe3-154">SharePoint bietet für die Arbeit mit externen Daten fünf verschiedene Webparts: Geschäftsdatenliste, Geschäftsdatenelement, Generator für Geschäftsdatenelemente, Geschäftsdaten-Beziehungsliste und Geschäftsdatenaktionen.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-154">SharePoint provides five different Web Parts for working with external data: Business Data List, Business Data Item, Business Data Item Builder, Business Data Related List, and Business Data Actions.</span></span>
    
  
- <span data-ttu-id="f1fe3-155">**Auswahltool für externe Inhaltstypen**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-155">**External Content Type Picker**</span></span>
    
    <span data-ttu-id="f1fe3-p113">Ein Auswahltool für externe Inhaltstypen stellt dem Benutzer Funktionen zur Auswahl und Auflösung bereit. Sie können ein Auswahltool in ein Formular oder eine Seite einbetten, wenn ein Benutzer aus einer Liste verfügbarer externer Inhaltstypen einen externen Inhaltstyp auswählen können soll.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p113">An External Content Type Picker provides picking and resolving functionality to the user. You can embed a picker in a form or page for scenarios where a user should be able to choose an external content type from the list of available external content types.</span></span> 
    
  
- <span data-ttu-id="f1fe3-158">**Auswahltool für externe Elemente**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-158">**External Item Picker**</span></span>
    
    <span data-ttu-id="f1fe3-p114">Ein Auswahltool für externe Elemente stellt für externe Elemente auf dem Server und in Rich-Client-Office-Anwendungen Funktionen zur Auswahl und Auflösung bereit. Sie können ein Auswahltool in ein Formular oder eine Seite einbetten, wenn ein Benutzer aus einer Liste mit Kunden ein externes Element wie einen Kunden auswählen können soll.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p114">An External Item Picker provides picking and resolving functionality for external items on the server and in rich-client Office applications. You can embed a picker in a form or page for scenarios where a user should be able to pick an external item, such as a customer from a list of customers.</span></span> 
    
  
- <span data-ttu-id="f1fe3-161">**Profilseiten**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-161">**Profile Pages**</span></span>
    
    <span data-ttu-id="f1fe3-p115">Profilseiten sind SharePoint-Seiten in SharePoint, auf denen die Details zu einem externen Element angezeigt werden. Wie jedes andere SharePoint-Webparts-Seite können Sie diese Seite so anpassen, dass Details eines externen Elements angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-p115">Profile Pages are SharePoint pages in SharePoint that display the details about an external item. Just like any other SharePoint Web Parts page, you can customize this page to show details of an external item.</span></span>
    
  
- <span data-ttu-id="f1fe3-164">**Benutzerdefinierte Seiten und Anwendungen**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-164">**Custom pages and applications**</span></span>
    
    <span data-ttu-id="f1fe3-165">Sie können die Programmierbarkeitsoptionen von SharePoint verwenden, wie das SharePoint-Objektmodell, das SharePoint-Clientobjektmodell und REST-URLs (Representational State Transfer).</span><span class="sxs-lookup"><span data-stu-id="f1fe3-165">You can use the SharePoint programmability options, such as the SharePoint object model, client object model, and Representational State Transfer (REST) URLs.</span></span>
    
  
<span data-ttu-id="f1fe3-166">Tabelle 1 enthält Beispielaufgaben, mit denen das Arbeiten mit externen Inhaltstypen veranschaulicht wird.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-166">Table 1 contains examples of tasks that illustrate working with external content types.</span></span>
  
    
    

<span data-ttu-id="f1fe3-167">**Tabelle 1. Einfache Aufgaben für das Arbeiten mit externen Inhaltstypen**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-167">**Table 1. Basic tasks for working with external content types**</span></span>


|<span data-ttu-id="f1fe3-168">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-168">**Task**</span></span>|<span data-ttu-id="f1fe3-169">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f1fe3-169">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="f1fe3-170">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-170">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="f1fe3-171">Erfahren Sie, wie Sie mithilfe von Visual Studio 2012 eine veröffentlichte OData-Quelle ermitteln und einen wiederverwendbaren externen Inhaltstyp zur Verwendung in SharePoint Business Connectivity Services (BCS) erstellen.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-171">Learn how to use Visual Studio 2012 to discover a published OData source, and create a reusable external content type for use in SharePoint Business Connectivity Services (BCS).</span></span>  <br/> |
| [<span data-ttu-id="f1fe3-172">Vorgehensweise: Erstellen externer Inhaltstypen für SQL Server in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-172">How to: Create external content types for SQL Server in SharePoint</span></span>](how-to-create-external-content-types-for-sql-server-in-sharepoint.md) <br/> |<span data-ttu-id="f1fe3-173">Erfahren Sie, wie Sie einen externen Inhaltstyp erstellen, der auf einer SQL Server-Datenbank basiert.</span><span class="sxs-lookup"><span data-stu-id="f1fe3-173">Learn how to create an external content type based on a SQL Server database.</span></span>  <br/> |
   

## <a name="see-also"></a><span data-ttu-id="f1fe3-174">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f1fe3-174">See also</span></span>
<span data-ttu-id="f1fe3-175"><a name="SP15ectoverview_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="f1fe3-175"><a name="SP15ectoverview_addres"> </a></span></span>


-  [<span data-ttu-id="f1fe3-176">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-176">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f1fe3-177">Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-177">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f1fe3-178">Vorgehensweise: Erstellen externer Inhaltstypen für SQL Server in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-178">How to: Create external content types for SQL Server in SharePoint</span></span>](how-to-create-external-content-types-for-sql-server-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f1fe3-179">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-179">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f1fe3-180">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1fe3-180">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

