---
title: Listendefinition / list Vorlage in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c4a412493d0cc1768aa103b06cd98e189479d317
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="list-definition--list-template-in-the-sharepoint-add-in-model"></a><span data-ttu-id="0cb22-102">Listendefinition / list Vorlage in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="0cb22-102">List definition / list template in the SharePoint add-in model</span></span>
==============================================================

<a name="summary"></a><span data-ttu-id="0cb22-103">Summary</span><span class="sxs-lookup"><span data-stu-id="0cb22-103">Summary</span></span>
-------

<span data-ttu-id="0cb22-104">Die Vorgehensweise zum Erstellen von Listendefinitionen / Listenvorlagen in unterscheidet das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="0cb22-104">The approach you take to create list definitions / list templates is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="0cb22-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, benutzerdefinierten Listendefinitionen / Listenvorlagen mit deklarativem Code erstellt und über den SharePoint-Lösungen bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="0cb22-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom list definitions / list templates were created with declarative code and deployed via SharePoint Solutions.</span></span> 

<span data-ttu-id="0cb22-106">In einem Szenario mit Modell SharePoint-Add-in kann nicht benutzerdefinierten Listendefinitionen tatsächlich erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-106">In a SharePoint Add-in model scenario, one cannot actually create custom list definitions.</span></span>  <span data-ttu-id="0cb22-107">Es ist nicht dazu einfach möglich.</span><span class="sxs-lookup"><span data-stu-id="0cb22-107">It is simply impossible to do this.</span></span>  <span data-ttu-id="0cb22-108">Allerdings kann das remote provisioning Muster verwendet, um benutzerdefinierte Listenvorlagen (STP-Dateien) für Office 365 bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-108">However, the remote provisioning pattern may used to deploy custom list templates (.stp files) to Office 365.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="0cb22-109">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="0cb22-109">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="0cb22-110">In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Implementieren von Listendefinitionen / Listenvorlagen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-110">As a rule of a thumb, we would like to provide the following high level guidelines to implement list definitions / list templates.</span></span>

- <span data-ttu-id="0cb22-111">Verwenden Sie das remote provisioning Muster zum Bereitstellen von Vorlagen für Bibliothekslisten (STP-Dateien) für SharePoint-Websites.</span><span class="sxs-lookup"><span data-stu-id="0cb22-111">Use the remote provisioning pattern to deploy list templates (.stp files) to SharePoint sites.</span></span>
- <span data-ttu-id="0cb22-112">Sie können die Abwesenheitsnotiz über das Verhalten des Liste Outlook erstellen, die standardisierte Einstellungen gelten für alle Listen in einer SharePoint-Website erstellt außer Kraft setzen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-112">You can override the out of the box list creation behavior to apply standardized settings to all lists created in a SharePoint site.</span></span>  <span data-ttu-id="0cb22-113">Finden Sie weitere Informationen zu diesem Ansatz unten.</span><span class="sxs-lookup"><span data-stu-id="0cb22-113">See more details about this approach below.</span></span>
- <span data-ttu-id="0cb22-114">Sie können ein SharePoint-Add-in zum Erstellen von Listen mit standardisierte Einstellungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-114">You can create a SharePoint Add-in to create lists with standardized settings.</span></span> <span data-ttu-id="0cb22-115">Finden Sie weitere Informationen zu diesem Ansatz unten.</span><span class="sxs-lookup"><span data-stu-id="0cb22-115">See more details about this approach below.</span></span>

<a name="options-to-ensure-standardized-settings-templates-are-applied-to-sharepoint-lists-upon-list-creation"></a><span data-ttu-id="0cb22-116">Optionen, die standardisierte Einstellungen (Vorlagen) gewährleisten angewendet werden mit SharePoint-Listen Liste erstellt worden ist</span><span class="sxs-lookup"><span data-stu-id="0cb22-116">Options to ensure standardized settings (templates) are applied to SharePoint lists upon list creation</span></span>
------------------------------------------------------------------------------------------------------

<span data-ttu-id="0cb22-117">Sie haben verschiedene Optionen, um sicherzustellen, dass standardisierte Einstellungen (Vorlagen) angewendet werden mit SharePoint-Listen Liste erstellt worden ist.</span><span class="sxs-lookup"><span data-stu-id="0cb22-117">You have a couple of options to ensure standardized settings (templates) are applied to SharePoint lists upon list creation.</span></span>

- <span data-ttu-id="0cb22-118">Überschreiben Sie die Abwesenheitsnotiz über das Verhalten des Liste erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-118">Override the out of the box list creation behavior.</span></span>   
- <span data-ttu-id="0cb22-119">Erstellen eines SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="0cb22-119">Create a SharePoint Add-in.</span></span> 

<a name="override-the-out-of-the-box-list-creation-behavior"></a><span data-ttu-id="0cb22-120">Überschreiben Sie die Abwesenheitsnotiz über das Verhalten des Liste erstellen</span><span class="sxs-lookup"><span data-stu-id="0cb22-120">Override the out of the box list creation behavior</span></span>
--------------------------------------------------
<span data-ttu-id="0cb22-121">In diesem Muster ändern Sie die Abwesenheitsnotiz über das Verhalten des Liste Erstellung durch Hinzufügen eines Ereignisempfängers an das ListAdded-Ereignis.</span><span class="sxs-lookup"><span data-stu-id="0cb22-121">In this pattern you modify the out of the box list creation behavior by adding an event receiver to the ListAdded event.</span></span>  <span data-ttu-id="0cb22-122">Klicken Sie dann konfiguriert in den Ereignisdetails Ereignisempfänger für das ListAdded-Ereignis, das Sie das remote provisioning Muster verwenden, um standardisierten Konfigurationen auf jede Liste anzuwenden, die erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="0cb22-122">Then, in the event receiver configured for the ListAdded event you use the remote provisioning pattern to apply standardized configurations to each list that is created.</span></span>

<span data-ttu-id="0cb22-123">Hinzufügen von Inhaltstypen, den Standardinhaltstyp festlegen, Listenspalten hinzufügen, wird die versionneinstellungen, und alle anderen Liste Typ Konfigurationen, die festgelegt werden können, können diese standardisierten Konfigurationen enthalten.</span><span class="sxs-lookup"><span data-stu-id="0cb22-123">These standardized configurations may include adding content types, setting the default content type, adding list columns, setting the version settings, and any other list type configurations that may be set.</span></span> 
    
- <span data-ttu-id="0cb22-124">Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen für alle Listen gelten.</span><span class="sxs-lookup"><span data-stu-id="0cb22-124">This approach allows you to apply standardized settings for all lists.</span></span>
- <span data-ttu-id="0cb22-125">Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen gelten für verschiedene Arten von Listen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-125">This approach allows you to apply standardized settings to different types of lists.</span></span>
    + <span data-ttu-id="0cb22-126">Beispiel: Wenn Sie eine Dokumentbibliothek erstellen und eine Vorgangsliste in den Ereignisempfänger ListAdded feststellen welche Art von Liste Sie erstellt haben und Sie können unterschiedliche anwenden Einstellungen basierend auf den Listentyp standardisierte.</span><span class="sxs-lookup"><span data-stu-id="0cb22-126">For example: If you create a document library and a tasks list you can determine in the ListAdded event receiver which type of list you created and you can apply different standardized settings based on the list type.</span></span>  <span data-ttu-id="0cb22-127">Alle Dokumentbibliotheken benötigen möglicherweise eine Gruppe von Inhaltstypen, die angewendet werden, während alle Aufgabenliste benötigen eine andere Menge von Inhaltstypen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="0cb22-127">Perhaps all document libraries need one set of content types applied to them, while all tasks list need a different set of content types applied to them.</span></span>
- <span data-ttu-id="0cb22-128">Dieser Ansatz unterstützt Anwenden von mehreren verschiedenen Optionen auf Listen nicht.</span><span class="sxs-lookup"><span data-stu-id="0cb22-128">This approach does not support applying multiple different template options to lists.</span></span>
    + <span data-ttu-id="0cb22-129">Beispiel: Wenn Sie eine Dokumentbibliothek erstellen und eine Vorgangsliste in den Ereignisempfänger ListAdded feststellen welche Art von Liste Sie erstellt haben und Sie können unterschiedliche anwenden Einstellungen basierend auf den Listentyp standardisierte.</span><span class="sxs-lookup"><span data-stu-id="0cb22-129">For example: If you create a document library and a tasks list you can determine in the ListAdded event receiver which type of list you created and you can apply different standardized settings based on the list type.</span></span>  <span data-ttu-id="0cb22-130">Sie können nicht jedoch unterschiedliche Vorlagen in einer Dokumentbibliothek anwenden, die im Vergleich zu einer anderen Dokumentbibliothek zu erstellen, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-130">However, you cannot apply different templates to one document library you create versus another document library you create.</span></span>

<span data-ttu-id="0cb22-131">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="0cb22-131">**When is it a good fit?**</span></span>

<span data-ttu-id="0cb22-132">Wenn Sie standardisierte globale Einstellungen gelten für alle Listen oder Listen eines bestimmten Typs müssen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-132">When you need to apply standardized global settings to all lists or lists of a specific type.</span></span>

<span data-ttu-id="0cb22-133">**Wenn es nicht geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="0cb22-133">**When is it a not good fit?**</span></span>

<span data-ttu-id="0cb22-134">Wenn Sie mehrere Optionen für unterschiedliche Vorlagen auf Listen anwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-134">When you need to apply multiple different templates options to lists.</span></span>

<span data-ttu-id="0cb22-135">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="0cb22-135">**Getting Started**</span></span>

<span data-ttu-id="0cb22-136">Die folgenden SharePoint-Add-Ins Modell Anleitung wird beschrieben, wie Ereignisempfänger implementieren.</span><span class="sxs-lookup"><span data-stu-id="0cb22-136">The following SharePoint Add-in model recipe describes how to implement event receivers.</span></span>

- [<span data-ttu-id="0cb22-137">Ereignisempfänger (SharePoint-Add-Ins Modell Anleitung)</span><span class="sxs-lookup"><span data-stu-id="0cb22-137">Event Receivers (SharePoint Add-in model recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)

<a name="create-a-sharepoint-add-in"></a><span data-ttu-id="0cb22-138">Erstellen eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0cb22-138">Create a SharePoint Add-in</span></span>
--------------------------

<span data-ttu-id="0cb22-139">In diesem Muster erstellen Sie ein SharePoint-Add-in zum Erstellen von Listen mit standardisierte Einstellungen, und weisen Sie die Benutzer auf das SharePoint-Add-in verwenden, um neue Listen erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-139">In this pattern you create a SharePoint Add-in to create lists with standardized settings and instruct your users to use the SharePoint Add-in to create new lists.</span></span>  <span data-ttu-id="0cb22-140">Stellt im Wesentlichen das SharePoint-Add-in Benutzern mit Auswahlmöglichkeiten von verschiedenen Listen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-140">Essentially, the SharePoint Add-in provides users with choices of different lists to create.</span></span>  <span data-ttu-id="0cb22-141">Das SharePoint-Add-in ermöglicht Benutzern das Erstellen von verschiedenen Listen werden vom Unternehmen definiert und von einem Entwickler implementiert.</span><span class="sxs-lookup"><span data-stu-id="0cb22-141">The different lists the SharePoint Add-in allows users to create are defined by the business and implemented by a developer.</span></span> <span data-ttu-id="0cb22-142">Ausfüllen eines Formulars in der SharePoint Add-in für Meta-Listendaten angeben, und wählen bietet welcher Liste Sie aus der Auswahl das Add-in erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-142">Users fill out a form in the SharePoint Add-in to specify the list meta-data and choose which list to create from the choices the Add-in offers.</span></span> <span data-ttu-id="0cb22-143">Das Add-in mithilfe des remote provisioning Musters um entsprechend die Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-143">The Add-in uses the remote provisioning pattern to create the list accordingly.</span></span>
    
- <span data-ttu-id="0cb22-144">Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen für alle Listen gelten.</span><span class="sxs-lookup"><span data-stu-id="0cb22-144">This approach allows you to apply standardized settings for all lists.</span></span>
- <span data-ttu-id="0cb22-145">Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen gelten für verschiedene Arten von Listen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-145">This approach allows you to apply standardized settings to different types of lists.</span></span>
- <span data-ttu-id="0cb22-146">Dieser Ansatz ermöglicht Ihnen mehrere andere Vorlage auf Listen angewendet.</span><span class="sxs-lookup"><span data-stu-id="0cb22-146">This approach allows you to apply multiple different template options to lists.</span></span>

<span data-ttu-id="0cb22-147">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="0cb22-147">**When is it a good fit?**</span></span>

<span data-ttu-id="0cb22-148">Wenn Sie mehrere Optionen für unterschiedliche Vorlagen auf Listen anwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="0cb22-148">When you need to apply multiple different templates options to lists.</span></span>

<span data-ttu-id="0cb22-149">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="0cb22-149">**Getting Started**</span></span>

<span data-ttu-id="0cb22-150">Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie ein SharePoint-Add-in zu erstellen, die eine Benutzeroberfläche bereitstellt, mit die Endbenutzer neue Dokumentbibliotheken erstellen können.</span><span class="sxs-lookup"><span data-stu-id="0cb22-150">The following O365 PnP Code Sample and video demonstrates how to create a SharePoint Add-in that provides a user interface that allows end users to create new document libraries.</span></span>  <span data-ttu-id="0cb22-151">Darüber hinaus wird das Erstellen einer Dokumentbibliothek mit spezifischen Konfigurationen, die gemeinsam eine Vorlage darstellen veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="0cb22-151">It also demonstrates how to create a document library with specific configurations that collectively represent a template.</span></span>

- [<span data-ttu-id="0cb22-152">ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="0cb22-152">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

<span data-ttu-id="0cb22-153">Im folgende Video durchlaufen im Codebeispiel.</span><span class="sxs-lookup"><span data-stu-id="0cb22-153">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="0cb22-154">Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="0cb22-154">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

<a name="related-links"></a><span data-ttu-id="0cb22-155">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="0cb22-155">Related links</span></span>
=============

- [<span data-ttu-id="0cb22-156">Listeninstanz (SharePoint-Add-Ins Modell Anleitung)</span><span class="sxs-lookup"><span data-stu-id="0cb22-156">List Instance (SharePoint Add-in model recipe)</span></span>](list-instance-sharepoint-add-in.md)
- [<span data-ttu-id="0cb22-157">Ereignisempfänger (SharePoint-Add-Ins Modell Anleitung)</span><span class="sxs-lookup"><span data-stu-id="0cb22-157">Event Receivers (SharePoint Add-in model recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [<span data-ttu-id="0cb22-158">Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="0cb22-158">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- <span data-ttu-id="0cb22-159">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="0cb22-159">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="0cb22-160">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="0cb22-160">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="0cb22-161">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="0cb22-161">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="0cb22-162">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="0cb22-162">Related PnP samples</span></span>
===================

- [<span data-ttu-id="0cb22-163">ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="0cb22-163">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- <span data-ttu-id="0cb22-164">Beispiele und Inhalte am https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="0cb22-164">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="0cb22-165">Gilt für</span><span class="sxs-lookup"><span data-stu-id="0cb22-165">Applies to</span></span>
==========
- <span data-ttu-id="0cb22-166">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="0cb22-166">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="0cb22-167">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="0cb22-167">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="0cb22-168">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="0cb22-168">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="0cb22-169">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="0cb22-169">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
