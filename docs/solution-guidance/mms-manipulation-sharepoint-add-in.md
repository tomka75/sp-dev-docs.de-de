---
title: Bearbeiten von MMS in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 0d1509b65fcd33068182b3747f21e1cb1db86238
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="mms-manipulation-in-the-sharepoint-add-in-model"></a><span data-ttu-id="14a43-102">Bearbeiten von MMS in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="14a43-102">MMS manipulation in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="14a43-103">Summary</span><span class="sxs-lookup"><span data-stu-id="14a43-103">Summary</span></span>
-------

<span data-ttu-id="14a43-104">Ansatz verwenden Sie zur Durchführung von Create, Read, Update und Delete (CRUD) Vorgänge in Managed Metadata Service (MMS) unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="14a43-104">The approach you take to perform Create, Read, Update and Delete (CRUD) operations in the Managed Metadata Service (MMS) is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="14a43-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario MMS CRUD-Vorgänge wurden mit SharePoint Server-Side-Objektmodellcode ausgeführt und über Farmlösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="14a43-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, MMS CRUD operations were performed with the SharePoint server-side object model code and deployed via Farm Solutions.</span></span> 

<span data-ttu-id="14a43-106">In einem Szenario mit SharePoint-Add-Ins Modell werden MMS CRUD-Vorgänge mit dem clientseitigen Objektmodell (CSOM) ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="14a43-106">In a SharePoint Add-in model scenario, MMS CRUD operations are performed with the client-side object model (CSOM).</span></span>

<span data-ttu-id="14a43-107">**Das CSOM enthält alle Vorgänge zum Replizieren und Synchronisieren von Daten in die MMS erforderlich.**</span><span class="sxs-lookup"><span data-stu-id="14a43-107">**The CSOM provides all of the operations necessary to replicate and synchronize data in the MMS.**</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="14a43-108">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="14a43-108">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="14a43-109">In der Regel von einer Ziehpunkt empfehlen wir die folgenden allgemeinen Richtlinien für die Durchführung von MMS CRUD-Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="14a43-109">As a rule of a thumb, we recommend the following high-level guidelines for performing MMS CRUD operations.</span></span>

- <span data-ttu-id="14a43-110">MMS CRUD-Vorgänge sollte mit dem clientseitigen Objektmodell implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="14a43-110">MMS CRUD operations should be implemented with the client-side object model.</span></span>
- <span data-ttu-id="14a43-111">Führen Sie den CSOM-Code mit einem Konto mit den entsprechenden Berechtigungen zur Ausführung von MMS CRUD-Vorgänge aus.</span><span class="sxs-lookup"><span data-stu-id="14a43-111">Execute the CSOM code with an account that has the appropriate permissions to perform MMS CRUD operations.</span></span>
- <span data-ttu-id="14a43-112">Bei der Begriff Synchronisierung legt die ChangeInformation-Klasse verwendet werden, da es eine höhere Leistung führt als GetAllTerms verwenden und Auflisten der Begriffe jedes Mal, wenn Sie synchronisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="14a43-112">When synchronizing term sets use the ChangeInformation class because it performs better than using GetAllTerms and enumerating the terms every time you want to sync.</span></span> 


<a name="options-to-copy-and-synchronize-mms-data"></a><span data-ttu-id="14a43-113">Optionen zum Kopieren und Synchronisieren von MMS-Daten</span><span class="sxs-lookup"><span data-stu-id="14a43-113">Options to copy and synchronize MMS data</span></span>
----------------------------------------

<span data-ttu-id="14a43-114">Sie haben verschiedene Optionen zum Kopieren und Synchronisieren von MMS-Daten.</span><span class="sxs-lookup"><span data-stu-id="14a43-114">You have a couple of options to copy and synchronize MMS data.</span></span>

- <span data-ttu-id="14a43-115">Der lokale</span><span class="sxs-lookup"><span data-stu-id="14a43-115">On-premises</span></span>
    + <span data-ttu-id="14a43-116">Kopieren Sie die Datenbank</span><span class="sxs-lookup"><span data-stu-id="14a43-116">Copy database</span></span>
    + <span data-ttu-id="14a43-117">Verwenden Sie CSOM, um Daten zu kopieren</span><span class="sxs-lookup"><span data-stu-id="14a43-117">Use CSOM to copy data</span></span>
    + <span data-ttu-id="14a43-118">Verwenden Sie CSOM, um Daten synchronisieren</span><span class="sxs-lookup"><span data-stu-id="14a43-118">Use CSOM to sync data</span></span>
- <span data-ttu-id="14a43-119">Office 365</span><span class="sxs-lookup"><span data-stu-id="14a43-119">Office 365</span></span>
    + <span data-ttu-id="14a43-120">Verwenden Sie CSOM, um Daten zu kopieren</span><span class="sxs-lookup"><span data-stu-id="14a43-120">Use CSOM to copy data</span></span>
    + <span data-ttu-id="14a43-121">Verwenden Sie CSOM, um Daten synchronisieren</span><span class="sxs-lookup"><span data-stu-id="14a43-121">Use CSOM to sync data</span></span>

<a name="on-premises---copy-database"></a><span data-ttu-id="14a43-122">Der lokale - Datenbank kopieren</span><span class="sxs-lookup"><span data-stu-id="14a43-122">On-premises - copy database</span></span>
---------------------------
<span data-ttu-id="14a43-123">Wenn Sie eine lokale SharePoint-Umgebung verfügen können Sie die MMS-Datenbank von einer Farm in eine andere Begriffe schnell replizieren kopieren.</span><span class="sxs-lookup"><span data-stu-id="14a43-123">If you have an on-premises SharePoint environment you can copy the MMS database from one farm to another to quickly replicate terms.</span></span>

<span data-ttu-id="14a43-124">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="14a43-124">**When is it a good fit?**</span></span>

<span data-ttu-id="14a43-125">Wenn Sie über eine lokale SharePoint-Umgebung verfügen, und Sie eine unidirektionale Kopie von Ausdrücken durchgeführt werden, ist dies eine gute Wahl, da sie schnell und einfach implementiert werden kann, ohne Code schreiben.</span><span class="sxs-lookup"><span data-stu-id="14a43-125">When you have an on-premises SharePoint environment and you are performing a one-way copy of terms, this is a good option because it may be implemented quickly and easily without writing any code.</span></span>

<a name="on-premises--o365---use-csom-to-copy-data"></a><span data-ttu-id="14a43-126">Lokale & O365 - CSOM verwenden, um Daten zu kopieren</span><span class="sxs-lookup"><span data-stu-id="14a43-126">On-premises & O365 - Use CSOM to copy data</span></span>
------------------------------------------
<span data-ttu-id="14a43-127">Wenn Sie einem lokalen oder Office 365 SharePoint-Umgebung können CSOM zum Kopieren von MMS-Daten aus einer Farm-Instanz in eine andere.</span><span class="sxs-lookup"><span data-stu-id="14a43-127">If you have an on-premises or Office 365 SharePoint environment you can use CSOM to copy MMS data from one farm/tenancy to another.</span></span>  <span data-ttu-id="14a43-128">***Sie können die lokalen und Office 365-Farmen mit diesem Ansatz einschließen.***</span><span class="sxs-lookup"><span data-stu-id="14a43-128">***You can include both on-premises and Office 365 farms with this approach.***</span></span>

<span data-ttu-id="14a43-129">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="14a43-129">**When is it a good fit?**</span></span>

<span data-ttu-id="14a43-130">Wenn Sie eine lokale SharePoint oder Office 365 oder eine hybridumgebung, und Sie werden MMS Daten zwischen mindestens zwei SharePoint-Farmen/Mandanten kopieren, ist dies eine gute Wahl, da Sie die Flexibilität, die MMS-Daten aus einer Farm in eine andere kopiert eine.</span><span class="sxs-lookup"><span data-stu-id="14a43-130">When you have an on-premises SharePoint or Office 365 or a hybrid environment and you are copying MMS data between two or more SharePoint farms/tenancies, this is a good option because it gives you the flexibility to copy the MMS data from one farm to another.</span></span>

<span data-ttu-id="14a43-131">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="14a43-131">**Getting started**</span></span>

<span data-ttu-id="14a43-132">Im folgende Beispiel veranschaulicht, wie MMS CRUD-Vorgänge auszuführen.</span><span class="sxs-lookup"><span data-stu-id="14a43-132">The following sample demonstrates how to perform MMS CRUD operations.</span></span>

- [<span data-ttu-id="14a43-133">Core.MMS (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="14a43-133">Core.MMS (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)

<a name="on-premises--o365---use-csom-to-sync-data"></a><span data-ttu-id="14a43-134">Lokale & O365 - CSOM zum Synchronisieren von Daten verwenden</span><span class="sxs-lookup"><span data-stu-id="14a43-134">On-premises & O365 - Use CSOM to sync data</span></span>
------------------------------------------
<span data-ttu-id="14a43-135">Wenn Sie eine lokale SharePoint-Umgebung verfügen, können Sie CSOM auf Sync MMS Daten zwischen Farmen verwenden.</span><span class="sxs-lookup"><span data-stu-id="14a43-135">If you have an on-premises SharePoint environment you can use CSOM to sync MMS data between farms.</span></span> <span data-ttu-id="14a43-136">***Sie können die lokalen und Office 365-Farmen/Mandanten mit diesem Ansatz einschließen.***</span><span class="sxs-lookup"><span data-stu-id="14a43-136">***You can include both on-premises and Office 365 farms/tenancies with this approach.***</span></span>

<span data-ttu-id="14a43-137">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="14a43-137">**When is it a good fit?**</span></span>

<span data-ttu-id="14a43-138">Wenn Sie ein lokales SharePoint oder Office 365 oder eine hybridumgebung und Sie Daten zwischen zwei oder mehr SharePoint-Farmen/Mandanten MMS synchronisiert werden, ist dies eine gute Wahl, da es Sie, die Flexibilität auf true Synchronisierung durchführen, und fügen Sie als viele Quellen aus.</span><span class="sxs-lookup"><span data-stu-id="14a43-138">When you have an on-premises SharePoint or Office 365 or a hybrid environment and you are synchronizing MMS data between two or more SharePoint farms/tenancies, this is a good option because it gives you the flexibility to perform true synchronization and include as many sources as you like.</span></span>

<span data-ttu-id="14a43-139">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="14a43-139">**Getting started**</span></span>

<span data-ttu-id="14a43-140">Im folgende Beispiel wird gezeigt, wie eine Synchronisierungstool für MMS Daten erstellen.</span><span class="sxs-lookup"><span data-stu-id="14a43-140">The following sample demonstrates how to build a synchronization tool for MMS data.</span></span>

- [<span data-ttu-id="14a43-141">Core.MMSSync (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="14a43-141">Core.MMSSync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)

<a name="related-links"></a><span data-ttu-id="14a43-142">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="14a43-142">Related links</span></span>
=============
- [<span data-ttu-id="14a43-143">Synchronisieren von Ausdruckssätzen mit CSOM (MSDN-Blog-Artikel Dokumentation)</span><span class="sxs-lookup"><span data-stu-id="14a43-143">Synchronize term sets using CSOM (MSDN Blog Article Documentation)</span></span>](http://blogs.msdn.com/b/frank_marasco/archive/2014/06/29/synchronize-term-sets-with-the-term-store-csom.aspx)
- <span data-ttu-id="14a43-144">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="14a43-144">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="14a43-145">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="14a43-145">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="14a43-146">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="14a43-146">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="14a43-147">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="14a43-147">Related PnP samples</span></span>
===================

- [<span data-ttu-id="14a43-148">Core.MMS (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="14a43-148">Core.MMS (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
- [<span data-ttu-id="14a43-149">Core.MMSSync (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="14a43-149">Core.MMSSync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
- <span data-ttu-id="14a43-150">Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="14a43-150">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="14a43-151">Gilt für</span><span class="sxs-lookup"><span data-stu-id="14a43-151">Applies to</span></span>
==========
- <span data-ttu-id="14a43-152">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="14a43-152">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="14a43-153">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="14a43-153">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="14a43-154">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="14a43-154">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="14a43-155">*Muster für dedizierte und lokalen sind identisch mit-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="14a43-155">*Patterns for dedicated and on-premises are identical with Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
