---
title: Dokument-ID-Anbieter in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: a20320887a17b26a4eb247b6c2968b82ab5d715b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="document-id-provider-in-the-sharepoint-add-in-model"></a><span data-ttu-id="cd05e-102">Dokument-ID-Anbieter in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="cd05e-102">Document ID provider in the SharePoint add-in model</span></span>
===================================================

<a name="summary"></a><span data-ttu-id="cd05e-103">Summary</span><span class="sxs-lookup"><span data-stu-id="cd05e-103">Summary</span></span>
-------

<span data-ttu-id="cd05e-104">Der gewählten Ansatz festlegen Eindeutiger Bezeichner für Dokumente in SharePoint unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="cd05e-104">The approach you take to set unique identifiers for documents in SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="cd05e-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Ausführen von SharePoint Server-Side Object Model Code Ereignishandler Element Liste wurden eindeutige Bezeichner für Dokumente festgelegt und sie über die SharePoint-Lösungen bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="cd05e-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list item event handlers running SharePoint Server-side Object Model code were used to set unique identifiers for documents and they were deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="cd05e-106">In einem Modell Szenario SharePoint-Add-in SharePoint mithilfe der clientseitigen Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-API dienen zum eindeutige Bezeichnern für Dokumente festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-106">In an SharePoint Add-in model scenario, the SharePoint Client-side Object Model (CSOM) and/or the SharePoint REST API are used to set unique identifiers for documents.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="cd05e-107">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="cd05e-107">High-level guidelines</span></span>
---------------------

<span data-ttu-id="cd05e-108">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Einstellung eindeutigen Bezeichnern für Dokumente in das neue SharePoint-Add-in-Modell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-108">As a rule of a thumb, we would like to provide the following high-level guidelines for setting unique identifiers for documents in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="cd05e-109">Verwenden Sie die SharePoint-Client Side-Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-APIs zum eindeutige Bezeichnern für Dokumente festlegen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-109">Use the SharePoint Client Side Object Model (CSOM), and/or the SharePoint REST APIs to set unique identifiers for documents.</span></span>
- <span data-ttu-id="cd05e-110">Es ist derzeit keine unterstützte Out-of-Box-Mechanismus zum Zuordnen von remote verarbeiteten Code, um die Out-of-Box-Dokument-ID-Anbieter zu ersetzen, damit diese Funktion nicht nativ unterstützt wird, um mit remote-APIs geändert werden.</span><span class="sxs-lookup"><span data-stu-id="cd05e-110">Currently, there is no supported out-of-the-box mechanism for associating remote processed code to replace the out-of-the-box document ID provider, so this capability is not natively supported to be modified with remote APIs.</span></span>
- <span data-ttu-id="cd05e-111">Allerdings werden wie in vielen Fällen mit dem-Add-in-Objektmodell, alternative Routen untersucht wird.</span><span class="sxs-lookup"><span data-stu-id="cd05e-111">However, like in many cases with the Add-in model, alternative routes are being explored.</span></span>

<a name="how-are-unique-identifiers-set-on-documents"></a><span data-ttu-id="cd05e-112">Wie werden eindeutige Bezeichner für Dokumente werden festgelegt?</span><span class="sxs-lookup"><span data-stu-id="cd05e-112">How are unique identifiers set on documents?</span></span>
--------------------------------------------

<span data-ttu-id="cd05e-113">***Im Wesentlichen durch einen eindeutigen Bezeichner für ein Dokument Mittel Festlegen des Werts einer Spalte in einer SharePoint-Liste /-Dokumentbibliothek festlegen.***</span><span class="sxs-lookup"><span data-stu-id="cd05e-113">***Essentially, setting a unique identifier for a document means setting the value of a column in a SharePoint list/document library.***</span></span>  

<span data-ttu-id="cd05e-114">Die SharePoint-(CSOM) und/oder den REST-APIs können verwendet werden, um die Spaltenwerte festgelegt, und dafür festlegen Eindeutiger Bezeichner für Dokumente genutzt werden können.</span><span class="sxs-lookup"><span data-stu-id="cd05e-114">The SharePoint (CSOM) and/or REST APIs may be used to set column values, and therefor they may be used to set unique identifiers for documents.</span></span> <span data-ttu-id="cd05e-115">Finden Sie die folgenden Artikel enthalten weitere Informationen zu diesen APIs und wie Sie mit diesen Spaltenwerte festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-115">See the following articles to learn more about these APIs and how to set column values with them.</span></span>  

- [<span data-ttu-id="cd05e-116">Führen Sie grundlegender Vorgänge unter Verwendung von SharePoint 2013-clientbibliothekscode (MSDN-Artikel aus)</span><span class="sxs-lookup"><span data-stu-id="cd05e-116">Complete basic operations using SharePoint 2013 client library code (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx#BasicOps_SPListItemTasks) 
- [<span data-ttu-id="cd05e-117">Arbeiten mit Listen und Listenelemente mit REST (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="cd05e-117">Working with lists and list items with REST (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/dn292552.aspx#ListItems)

<a name="options-to-set-unique-identifiers-for-documents"></a><span data-ttu-id="cd05e-118">Optionen zum Festlegen der eindeutige Bezeichner für Dokumente</span><span class="sxs-lookup"><span data-stu-id="cd05e-118">Options to set unique identifiers for documents</span></span>
-----------------------------------------------
<span data-ttu-id="cd05e-119">Sie müssen einige Optionen zum eindeutige Bezeichnern für Dokumente in SharePoint gespeicherten festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-119">You have a few options to set unique identifiers for documents stored in SharePoint.</span></span>

- <span data-ttu-id="cd05e-120">Verwenden von remote-Ereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="cd05e-120">Use remote event receivers</span></span>
- <span data-ttu-id="cd05e-121">Verwenden Sie einen Hintergrundprozess</span><span class="sxs-lookup"><span data-stu-id="cd05e-121">Use a background process</span></span>

<a name="use-remote-event-receivers"></a><span data-ttu-id="cd05e-122">Verwenden von remote-Ereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="cd05e-122">Use remote event receivers</span></span>
--------------------------
<span data-ttu-id="cd05e-123">In diesem Muster ausgelöst werden remote-Ereignisempfänger, wenn neue Dokumente in SharePoint-Bibliotheken hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="cd05e-123">In this pattern, remote event receivers fire when new documents are uploaded to SharePoint libraries.</span></span> <span data-ttu-id="cd05e-124">Stellen Sie die remote-Ereignisempfänger CSOM oder REST-API aufruft, um die eindeutigen IDs für Dokumente festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-124">The remote event receivers make CSOM or REST API calls to set unique identifiers for documents.</span></span>

- <span data-ttu-id="cd05e-125">Dieses Muster wird ausgeführt, unmittelbar nachdem ein Dokument in SharePoint hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="cd05e-125">This pattern executes immediately after a document is uploaded to SharePoint.</span></span>
    + <span data-ttu-id="cd05e-126">Solange der Code im Zusammenhang mit der remote-Ereignisempfänger-Dienst in einem angemessenen Zeitraum ausgeführt wird, werden die Dokument-IDs schnell festgelegt, nachdem ein neues Dokument in SharePoint hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="cd05e-126">As long as the code in the service associated with the remote event receiver executes in a timely fashion, the document IDs are set quickly after a new document is uploaded to SharePoint.</span></span>
- <span data-ttu-id="cd05e-127">Dieses Muster gilt nur für neue Dokumente in SharePoint hochgeladen, nicht eindeutige Bezeichnern für Dokumente, die bereits in SharePoint gespeicherten fest.</span><span class="sxs-lookup"><span data-stu-id="cd05e-127">This pattern only operates on new documents uploaded to SharePoint, it does not set unique identifiers for documents already stored in SharePoint.</span></span>
- <span data-ttu-id="cd05e-128">Upload Mengenoperationen werden mehrere Aufrufe an den Dienst zugeordnet der remote-Ereignisempfänger ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="cd05e-128">Bulk upload operations will trigger multiple calls to the service associated with the remote event receiver.</span></span> <span data-ttu-id="cd05e-129">Planen Sie entsprechend um sicherzustellen, dass Mengenoperationen hochladen den Dienst nicht überlastet.</span><span class="sxs-lookup"><span data-stu-id="cd05e-129">Plan accordingly to ensure bulk upload operations will not overload the service.</span></span>
- <span data-ttu-id="cd05e-130">Es gibt keine Möglichkeit für einen remote-Ereignisempfänger SharePoint zu benachrichtigen, wenn eine einzigartige Dokument-ID konnte nicht festlegen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-130">There is no way for a remote event receiver to notify SharePoint if setting a unique document ID failed.</span></span>

<span data-ttu-id="cd05e-131">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="cd05e-131">**When is it a good fit?**</span></span>

<span data-ttu-id="cd05e-132">Wenn Sie eindeutige Bezeichner für Dokumente schnell festgelegt, wenn für SharePoint hochladen, und Sie nicht hochladen Mengenoperationen erwarten müssen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-132">When you need to set unique identifiers for documents quickly after they are uploaded to SharePoint and you do not expect bulk upload operations.</span></span>

<span data-ttu-id="cd05e-133">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="cd05e-133">**Getting started**</span></span>

<span data-ttu-id="cd05e-134">[Ereignisempfänger und Liste-Ereignisempfänger (SharePoint-Add-in-Anleitung)](event-receiver-and-list-event-receiver-sharepoint-add-in.md) wird beschrieben, wie Ereignisempfänger im Add-In-Modell zu implementieren, und enthält Links zu mehreren Artikeln und Beispiele.</span><span class="sxs-lookup"><span data-stu-id="cd05e-134">The [Event Receivers and List Event Receivers (SharePoint Add-in Recipe)](event-receiver-and-list-event-receiver-sharepoint-add-in.md) describes how to implement event receivers in the Add-in model and provides links to several samples and articles.</span></span>

<a name="use-a-background-process"></a><span data-ttu-id="cd05e-135">Verwenden Sie einen Hintergrundprozess</span><span class="sxs-lookup"><span data-stu-id="cd05e-135">Use a background process</span></span>
------------------------
<span data-ttu-id="cd05e-136">In diesem Muster überprüft Prozess im Hintergrund Dokumente in SharePoint zu ermitteln, ob sie einen eindeutigen Bezeichner festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="cd05e-136">In this pattern, a background process checks documents in SharePoint to determine if they have a unique identifier set.</span></span> <span data-ttu-id="cd05e-137">Wenn keine Eindeutiger Bezeichner für ein Dokument gefunden wird, wird der Hintergrund-Prozess einen eindeutigen Bezeichner für das Dokument.</span><span class="sxs-lookup"><span data-stu-id="cd05e-137">If no unique identifier is found for a document, then the background process sets a unique identifier for the document.</span></span> <span data-ttu-id="cd05e-138">Der Hintergrund-Prozess macht CSOM oder REST-API aufruft, um die eindeutigen IDs für Dokumente festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-138">The background process makes CSOM or REST API calls to set unique identifiers for documents.</span></span>

- <span data-ttu-id="cd05e-139">Dieses Muster wird entsprechend den dafür festgelegten Zeitplan ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-139">This pattern executes according to the schedule you define for it.</span></span>
- <span data-ttu-id="cd05e-140">Dieses Muster wirkt sich auf alle Dokumente, die zum Durchforsten der Code geschrieben ist.</span><span class="sxs-lookup"><span data-stu-id="cd05e-140">This pattern operates on all documents the code is written to crawl.</span></span>
- <span data-ttu-id="cd05e-141">Wir empfehlen die Verwendung des SharePoint-Suchdiensts zum Ausführen von Abfragen, die enthalten Filter zum Zurückgeben einer Liste von Dokumenten, die keine eindeutige Bezeichnern für sie festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="cd05e-141">We suggest using the SharePoint search service to execute queries that include filters to return a list of documents that do not have unique identifiers set on them.</span></span>
    + <span data-ttu-id="cd05e-142">Dieses Muster führt der schnellsten und Skalen Abfragen eine höhere Leistung als andere Muster.</span><span class="sxs-lookup"><span data-stu-id="cd05e-142">This pattern performs the fastest and scales better than any other query pattern.</span></span>
    + <span data-ttu-id="cd05e-143">Dieses Muster entfällt benutzerdefinierte Abfragelogik aus dem Hintergrunddienst.</span><span class="sxs-lookup"><span data-stu-id="cd05e-143">This pattern eliminates custom query logic from the background service.</span></span>
    + <span data-ttu-id="cd05e-144">Dieses Muster erfordert einige Suchkonfiguration.</span><span class="sxs-lookup"><span data-stu-id="cd05e-144">This pattern requires some search configuration.</span></span>

        <span data-ttu-id="cd05e-145">Weitere Informationen zum Konfigurieren der Suche finden Sie die [Suchkonfiguration (SharePoint-Add-in-Anleitung)](search-configuration-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="cd05e-145">To learn more about search configuration, see the [Search Configuration (SharePoint Add-in Recipe)](search-configuration-sharepoint-add-in.md).</span></span>
- <span data-ttu-id="cd05e-146">Es wird nicht rekursiv Abfragen und return Metadaten für alle Dokumente in einer SharePoint-Umgebung empfohlen, durch Web- und Liste Objekte durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-146">It is not recommended to recursively query and return metadata about all the documents in a SharePoint environment by looping through web and list objects.</span></span>
    + <span data-ttu-id="cd05e-147">Dieses Muster führt die langsamste und Skalen schlechter als andere Abfragen Muster.</span><span class="sxs-lookup"><span data-stu-id="cd05e-147">This pattern performs the slowest and scales worse than any other query pattern.</span></span>  
    + <span data-ttu-id="cd05e-148">API steuerungsgrenzwerte für auftreten, wenn dieses Muster verwenden.</span><span class="sxs-lookup"><span data-stu-id="cd05e-148">You may encounter API throttle limits when using this pattern.</span></span>
    + <span data-ttu-id="cd05e-149">In diesem Muster enthält benutzerdefinierte Abfragelogik im Hintergrunddienst.</span><span class="sxs-lookup"><span data-stu-id="cd05e-149">This pattern includes custom query logic in the background service.</span></span>
    + <span data-ttu-id="cd05e-150">Dieses Muster kann mit einer Azure-Web-Projekt implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="cd05e-150">This pattern may be implemented with an Azure Web Job.</span></span>

<span data-ttu-id="cd05e-151">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="cd05e-151">**When is it a good fit?**</span></span>

- <span data-ttu-id="cd05e-152">Wenn Sie legen Sie eindeutige Bezeichner für Dokumente und remote-Ereignisempfänger müssen sind keine Option zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="cd05e-152">When you need to set unique identifiers for documents and remote event receivers are not an option available to you.</span></span>
- <span data-ttu-id="cd05e-153">Wenn Sie erwarten, dass Dokumente in einer Sammeloperation hochgeladen haben.</span><span class="sxs-lookup"><span data-stu-id="cd05e-153">When you expect to have documents uploaded in bulk.</span></span>
- <span data-ttu-id="cd05e-154">Wenn Sie benötigen, um sicherzustellen, dass werden einzigartige Dokument-IDs für Dokumente festgelegt.</span><span class="sxs-lookup"><span data-stu-id="cd05e-154">When you need to ensure unique document IDs are set on documents.</span></span>
    + <span data-ttu-id="cd05e-155">Es gibt keine Möglichkeit für einen Ereignisempfänger SharePoint zu benachrichtigen, wenn eine einzigartige Dokument-ID konnte nicht festlegen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-155">There is no way for an event receiver to notify SharePoint if setting a unique document ID failed.</span></span>
- <span data-ttu-id="cd05e-156">Wenn Sie bereits in SharePoint gespeicherten Dokumente verarbeiten müssen.</span><span class="sxs-lookup"><span data-stu-id="cd05e-156">When you need to process documents already stored in SharePoint.</span></span>

<span data-ttu-id="cd05e-157">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="cd05e-157">**Getting Started**</span></span>

<span data-ttu-id="cd05e-158">Die [Remote Zeitgeberaufträge (SharePoint-Add-in-Anleitung)](remote-timer-jobs-sharepoint-add-in.md) beschreibt, wie Sie remote Zeitgeberaufträge im Add-In-Modell zu implementieren und enthält Links zu mehreren Artikeln und Beispiele.</span><span class="sxs-lookup"><span data-stu-id="cd05e-158">The [Remote Timer Jobs (SharePoint Add-in Recipe)](remote-timer-jobs-sharepoint-add-in.md) describes how to implement remote timer jobs in the Add-in model and provides links to several samples and articles.</span></span>

<a name="related-links"></a><span data-ttu-id="cd05e-159">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="cd05e-159">Related links</span></span>
=============
- [<span data-ttu-id="cd05e-160">Ereignisempfänger und Liste-Ereignisempfänger (Anleitung SharePoint-Add-Ins)</span><span class="sxs-lookup"><span data-stu-id="cd05e-160">Event Receivers and List Event Receivers (SharePoint Add-in Recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [<span data-ttu-id="cd05e-161">Konfigurieren der Suche (SharePoint-Add-Ins Anleitung)</span><span class="sxs-lookup"><span data-stu-id="cd05e-161">Search Configuration (SharePoint Add-in Recipe)</span></span>](search-configuration-sharepoint-add-in.md)
- [<span data-ttu-id="cd05e-162">Remote Zeitgeberaufträge (SharePoint-Add-Ins Anleitung)</span><span class="sxs-lookup"><span data-stu-id="cd05e-162">Remote Timer Jobs (SharePoint Add-in Recipe)</span></span>](remote-timer-jobs-sharepoint-add-in.md)
- <span data-ttu-id="cd05e-163">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="cd05e-163">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="cd05e-164">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="cd05e-164">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="cd05e-165">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="cd05e-165">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="cd05e-166">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="cd05e-166">Related PnP samples</span></span>
===================

- [<span data-ttu-id="cd05e-167">OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="cd05e-167">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- <span data-ttu-id="cd05e-168">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="cd05e-168">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="cd05e-169">Gilt für</span><span class="sxs-lookup"><span data-stu-id="cd05e-169">Applies to</span></span>
==========
- <span data-ttu-id="cd05e-170">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="cd05e-170">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="cd05e-171">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="cd05e-171">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="cd05e-172">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="cd05e-172">SharePoint 2013 on-premises</span></span>
