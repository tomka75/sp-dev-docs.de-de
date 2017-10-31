---
title: Entwerfen von SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 92272154b37b9a02ed0a2b3ab73d7cdb57054087
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="design-sharepoint-add-ins"></a><span data-ttu-id="f1299-102">Entwerfen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-102">Design SharePoint Add-ins</span></span>
<span data-ttu-id="f1299-103">In diesem Artikel erhalten Sie einen Überblick über die in SharePoint-Add-Ins verfügbaren Entwurfs- und Architekturoptionen und erfahren, wie Sie die richtigen Entscheidungen treffen, um die Entwicklung Ihrer Add-Ins in SharePoint zu erleichtern.</span><span class="sxs-lookup"><span data-stu-id="f1299-103">Get an overview of the design and architecture options that are available in SharePoint Add-ins, and learn how to make the right decisions to ease the development of your add-in in SharePoint.</span></span>
 

 <span data-ttu-id="f1299-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f1299-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="f1299-p102">Angenommen, Sie haben eine großartige Idee für ein Add-In. In diesem Abschnitt führen wir Sie durch die erforderlichen Entwurfsentscheidungen und stellen bewährte Methoden für die Erstellung Ihres Add-Ins bereit. Was macht zum Beispiel eine gute Benutzeroberfläche aus? Welche Add-In-"Formen" sind verfügbar? Nach welchen Kriterien sollten diese ausgewählt werden? Welche Optionen stehen für den Datenzugriff zur Verfügung?</span><span class="sxs-lookup"><span data-stu-id="f1299-p102">Let's say you have a killer idea for an add-in. In this section, we'll guide you through the design decisions you need to make and offer best practices to build your add-in. For example, what makes a good user interface? What are the add-in "shapes" available? When should I use one instead of another? What options do I have for data access?</span></span> 
 

## <a name="start-designing-sharepoint-add-ins"></a><span data-ttu-id="f1299-113">Starten des Entwurfs von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-113">Start designing SharePoint Add-ins</span></span>
<span data-ttu-id="f1299-114"><a name="SP15Design_Startdesigning"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-114"><a name="SP15Design_Startdesigning"> </a></span></span>

<span data-ttu-id="f1299-p103">Da das Cloud-Add-In-Modell in SharePoint so viele Designoptionen ermöglicht, können SharePoint-Add-Ins die unterschiedlichsten Formen und Größen haben. Dieser Abschnitt liefert nützliche Tipps für einige der wichtigsten Entscheidungen, die Sie bei der Planung und beim Entwurf der Architektur und der Benutzerfreundlichkeit Ihres Add-Ins treffen müssen. Dazu zählen das Hosting Ihres Add-Ins, der effiziente und sichere Zugriff auf Daten und die Benutzung.</span><span class="sxs-lookup"><span data-stu-id="f1299-p103">Because the Cloud Add-in Model in SharePoint makes so many design options possible, SharePoint Add-ins can come in many shapes and sizes. This section contains helpful guidance for some of the most important decisions that you need to make as you are planning and designing the architecture and user experience of your add-in—including how you will host your add-in, how your add-in will efficiently and securely access data, and what the user experience will be.</span></span>
 

 
<span data-ttu-id="f1299-117">Eine Übersicht über die Design- und Architekturoptionen für SharePoint-Add-Ins finden Sie unter  [Drei Ansätze, um Entwurfsentscheidungen für Add-Ins für SharePoint zu treffen](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md). Worum es sich bei den SharePoint-Add-Ins handelt, erfahren Sie unter  [SharePoint-Add-Ins](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f1299-117">For an overview of the design and architecture options that are available with SharePoint Add-ins, see  [Three ways to think about design options for SharePoint Add-ins](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md). For an overview of what SharePoint Add-ins are, see  [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 

 

## <a name="choose-the-right-hosting-model-for-your-add-in"></a><span data-ttu-id="f1299-118">Wählen des richtigen Hostingmodells für Ihr Add-In</span><span class="sxs-lookup"><span data-stu-id="f1299-118">Choose the right hosting model for your add-in</span></span>
<span data-ttu-id="f1299-119"><a name="SP15Design_Hostingmodel"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-119"><a name="SP15Design_Hostingmodel"> </a></span></span>

<span data-ttu-id="f1299-p104">SharePoint-Add-Ins unterstützen mehrere Hostingoptionen. Sie können Ihren eigenen Webstapel wählen, Microsoft mit der Bereitstellung von Microsoft Azure und SQL Azure beauftragen oder das Add-In auf SharePoint hosten. In Tabelle 1 ist ein Artikel aufgeführt, der Ihnen bei der Auswahl des richtigen Hostingmodells für Ihr Add-In hilft.</span><span class="sxs-lookup"><span data-stu-id="f1299-p104">SharePoint Add-ins support multiple hosting options. You can choose your own web stack, have Microsoft provision Microsoft Azure and SQL Azure, or have the add-in hosted on SharePoint. Table 1 contains resources that can help you choose the right hosting model for your add-in.</span></span>
 

 

<span data-ttu-id="f1299-123">**Tabelle 1. Ressourcen und Anweisungen für die Wahl des richtigen Hostingmodells für SharePoint-Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="f1299-123">**Table 1. Resources and guidance for choosing the right hosting model for SharePoint Add-ins**</span></span>


|<span data-ttu-id="f1299-124">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="f1299-124">**Article**</span></span>|<span data-ttu-id="f1299-125">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f1299-125">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="f1299-126">Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1299-126">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)|<span data-ttu-id="f1299-127">Lernen Sie die verschiedenen Methoden zum Hosten der Komponenten von SharePoint-Add-Ins kennen.</span><span class="sxs-lookup"><span data-stu-id="f1299-127">Learn about the different ways that you can host the components of SharePoint Add-ins.</span></span>|

## <a name="choose-the-right-data-access-technologies-for-your-add-in"></a><span data-ttu-id="f1299-128">Wählen der richtigen Datenzugriffstechnologien für Ihr Add-In</span><span class="sxs-lookup"><span data-stu-id="f1299-128">Choose the right data access technologies for your add-in</span></span>
<span data-ttu-id="f1299-129"><a name="SP15Design_Dataaccess"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-129"><a name="SP15Design_Dataaccess"> </a></span></span>

<span data-ttu-id="f1299-p105">Sie müssen sicherstellen, dass Ihr Add-In effizient und sicher auf Daten zugreift. Für den Zugriff auf SharePoint und die Arbeit mit Daten in Ihrem Add-In stehen verschiedene Datenzugriffstechnologien zur Verfügung. In Tabelle 2 ist ein Artikel aufgeführt, in dem Sie erfahren, welche Optionen es gibt und wie Sie die richtige für Ihr Add-In auswählen.</span><span class="sxs-lookup"><span data-stu-id="f1299-p105">You must ensure that your add-in accesses data efficiently and securely. Various data access technologies are available for accessing SharePoint and working with data in your add-in. Table 2 provides resources to help you learn about your options and choose the one that is right for your add-in.</span></span> 
 

 

<span data-ttu-id="f1299-133">**Tabelle 2. Ressourcen und Anweisungen für die Wahl der Datenzugriffstechnologien zur Verwendung in SharePoint-Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="f1299-133">**Table 2. Resources and guidance for choosing the data access technologies to use in SharePoint Add-ins**</span></span>


|<span data-ttu-id="f1299-134">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="f1299-134">**Article**</span></span>|<span data-ttu-id="f1299-135">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f1299-135">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="f1299-136">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-136">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)| <span data-ttu-id="f1299-137">In diesem Artikel erfahren Sie, welche Datenzugriffsoptionen Sie bei der Erstellung von SharePoint-Add-Ins haben. Erläutert werden auch die Datenkonnektivitätsoptionen für eingehende und ausgehende Daten sowie die APIs, die für den Zugriff auf SharePoint von Ihrem Add-In aus zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="f1299-137">Learn about data access options you have when you build SharePoint Add-ins, including data connectivity options for inbound and outbound data scenarios, and the APIs that are available when you want to access SharePoint data from your add-in.</span></span>|

## <a name="design-the-ux-for-your-add-in"></a><span data-ttu-id="f1299-138">Entwerfen der Benutzeroberfläche für Ihr Add-In</span><span class="sxs-lookup"><span data-stu-id="f1299-138">Design the UX for your add-in</span></span>
<span data-ttu-id="f1299-139"><a name="SP15Design_UX"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-139"><a name="SP15Design_UX"> </a></span></span>

<span data-ttu-id="f1299-p106">Bei der Entwicklung eines Add-Ins sollte es Ihnen vor allem darauf ankommen, dass das Add-In so benutzerfreundlich ist, dass Benutzer die vorgesehenen Funktionen ausführen können. In Tabelle 3 ist ein Artikel aufgeführt, der erläutert, wie Sie erstklassige Add-Ins entwickeln, die bewährten Anforderungen an die Benutzerfreundlichkeit genügen und deren Gestalt und Funktionsweise sich an SharePoint anlehnt.</span><span class="sxs-lookup"><span data-stu-id="f1299-p106">As you design your add-in, your real goal should be to create an experience that enables users to complete the scenarios that you intend for them to accomplish. In Table 3, discover the resources and design guidance that you need to build great add-ins that follow best practices for user experience design and have the familiar appearance and behavior of SharePoint.</span></span>
 

 

<span data-ttu-id="f1299-142">**Tabelle 3. Ressourcen und Anweisungen für das Entwerfen einer ansprechenden Benutzeroberfläche für SharePoint-Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="f1299-142">**Table 3. Resources and guidance for designing a great user experience for SharePoint Add-ins**</span></span>


|<span data-ttu-id="f1299-143">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="f1299-143">**Article**</span></span>|<span data-ttu-id="f1299-144">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f1299-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="f1299-145">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-145">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)|<span data-ttu-id="f1299-146">Hier erfahren Sie mehr über die UX (User Experience)-Optionen, die Ihnen beim Erstellen von SharePoint-Add-Ins zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="f1299-146">Learn about the user experience options that you have when you build SharePoint Add-ins.</span></span>|

## <a name="design-with-update-in-mind"></a><span data-ttu-id="f1299-147">Berücksichtigen späterer Updates beim Entwurf</span><span class="sxs-lookup"><span data-stu-id="f1299-147">Design with update in mind</span></span>
<span data-ttu-id="f1299-148"><a name="Upgrade"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-148"><a name="Upgrade"> </a></span></span>

<span data-ttu-id="f1299-p107">Irgendwann möchten Sie ein Update Ihres Add-Ins erstellen und in den Office Store oder den Add-In-Katalog eines Unternehmens hochladen. Dies ist erheblich einfacher, wenn Sie spätere Updates des Add-Ins bereits beim Entwurf der ersten Version berücksichtigen. Daher sollten Sie die folgenden Artikel zu einem frühen Zeitpunkt in der Entwurfsphase lesen:  [Aktualisierungsverfahren für Add-Ins für SharePoint](sharepoint-add-ins-update-process.md) und [Aktualisieren von Add-Ins für SharePoint](update-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f1299-p107">Someday you may want to produce an update of your add-in and upload it to the Office Store or an organization's add-in catalog. That task will be a lot easier if you think about how you would update the add-in while you are designing the first version. We recommend that you read the following articles early in the design phase:  [SharePoint Add-ins update process](sharepoint-add-ins-update-process.md) and [Update SharePoint Add-ins](update-sharepoint-add-ins.md).</span></span> 
 

 

## <a name="next-steps-develop-and-publish-your-add-in"></a><span data-ttu-id="f1299-152">Nächste Schritte: Entwickeln und Veröffentlichen Ihres Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-152">Next steps: Develop and publish your add-in</span></span>
<span data-ttu-id="f1299-153"><a name="SP15Design_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-153"><a name="SP15Design_Next"> </a></span></span>

<span data-ttu-id="f1299-p108">Haben Sie ein solides Konzept für Ihr Add-In? Dann können Sie direkt mit der Erstellung des Add-Ins und seiner Veröffentlichung loslegen. Die in Tabelle 4 aufgeführten Artikel helfen Ihnen dabei.</span><span class="sxs-lookup"><span data-stu-id="f1299-p108">Have a solid design for your add-in? Get ready to build your add-in and publish it. The resources provided in Table 4 can help you get started.</span></span>
 

 

<span data-ttu-id="f1299-157">**Tabelle 4. Ressourcen und Anweisungen für die Entwicklung und Veröffentlichung von SharePoint-Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="f1299-157">**Table 4. Resources and guidance for developing and publishing SharePoint Add-ins**</span></span>


|<span data-ttu-id="f1299-158">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="f1299-158">**Article**</span></span>|<span data-ttu-id="f1299-159">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f1299-159">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="f1299-160">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="f1299-160">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)|<span data-ttu-id="f1299-161">Erläutert erweiterte Konzepte und Funktionen des Add-In-Modells.</span><span class="sxs-lookup"><span data-stu-id="f1299-161">Discusses advanced concepts and capabilities of the add-in model.</span></span>|
| [<span data-ttu-id="f1299-162">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-162">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins.md)|<span data-ttu-id="f1299-163">Beschreibt das Verfahren und die Anforderungen für die Veröffentlichung von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="f1299-163">Describes the process and requirements for publishing SharePoint Add-ins.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="f1299-164">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f1299-164">Additional resources</span></span>
<span data-ttu-id="f1299-165"><a name="SP15Design_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="f1299-165"><a name="SP15Design_AddRes"> </a></span></span>


-  [<span data-ttu-id="f1299-166">Beispielpaket für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-166">SharePoint Add-ins sample pack</span></span>](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)
    
 
-  [<span data-ttu-id="f1299-167">Reimagine SharePoint development</span><span class="sxs-lookup"><span data-stu-id="f1299-167">Reimagine SharePoint development</span></span>](http://msdn.microsoft.com/en-US/office/apps/dn133840)
    
 
-  [<span data-ttu-id="f1299-168">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-168">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f1299-169">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="f1299-169">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f1299-170">Blog für Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f1299-170">Blog for add-ins</span></span>](http://blogs.msdn.com/b/spoffapps)
    
 

