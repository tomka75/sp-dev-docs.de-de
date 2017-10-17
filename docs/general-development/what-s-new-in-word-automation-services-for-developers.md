---
title: "Neuigkeiten in Word Automation Services für Entwickler"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 00d2cf8d-93b0-4aab-8e76-31a6bb2f0dcb
ms.openlocfilehash: c01450d5a61edd71ee767c6028bd94937dd5e124
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-word-automation-services-for-developers"></a><span data-ttu-id="3770c-102">Neuigkeiten in Word Automation Services für Entwickler</span><span class="sxs-lookup"><span data-stu-id="3770c-102">What's new in Word Automation Services for developers</span></span>
<span data-ttu-id="3770c-p101">Dieses Thema bietet eine allgemeine Übersicht über das Hinzufügen und Erweiterungen für Entwickler in Word Automation Services. In Microsoft SharePoint ist die primäre zusätzlich zu Word Automation Services Unterstützung für "on Demand" Datei Konvertierung Anforderungen. Die wichtigste Verbesserung Word Automation Services wird die Unterstützung für die Verwendung von Datenströmen als Eingabe und Ausgabe von Konvertierungsaufgaben hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3770c-p101">This topic provides a high-level overview of the additions and enhancements for developers in Word Automation Services. In Microsoft SharePoint the primary addition to Word Automation Services is support for "on demand" file conversion requests. The most significant enhancement to Word Automation Services is added support for using streams as input to and output from conversion jobs.</span></span>
## <a name="create-an-on-demand-file-conversion"></a><span data-ttu-id="3770c-106">Erstellen Sie eine on Demand dateikonvertierung</span><span class="sxs-lookup"><span data-stu-id="3770c-106">Create an on demand file conversion</span></span>
<span data-ttu-id="3770c-107"><a name="was15CreateOnDemandConversion"> </a></span><span class="sxs-lookup"><span data-stu-id="3770c-107"></span></span>

<span data-ttu-id="3770c-p102">In Word Automation Services in Microsoft SharePoint erstellbare nun bei Bedarf fordert Datei konvertieren, dass das Ergebnis in der Datei Conversionthat werden sofort verarbeitet. In SharePoint 2010 würden Sie ein Konvertierungsauftrags Datei in Ihrem Code erstellen und starten Sie die Konvertierung mithilfe der ConversionJob.Start-Methode. Der Konvertierungsauftrag würde dann basierend festgelegt sind in Word Automation Services dafür, wie oft Konvertierungsaufgaben starten starten. Im Intervall würde SharePoint Zeitgeberauftrag für den Konvertierungsauftrag starten. Die Zeitgeberauftrag für die Basis-Methode verwenden, die frühesten können Sie beginnen eine Konvertierung Auftrag ist eine Minute.</span><span class="sxs-lookup"><span data-stu-id="3770c-p102">In Word Automation Services in Microsoft SharePoint you can now create on demand file conversion requests that result in file conversionthat are processed immediately. In SharePoint 2010, you would create a file conversion job in your code and then start the conversion using the ConversionJob.Start method. The conversion job would then start based on the interval set in Word Automation Services for how often to start conversion jobs. At the interval, the SharePoint Timer Job would start the conversion job. Using the Timer Job based method, the soonest you can start a conversion job is 1 minute.</span></span> 
  
    
    
<span data-ttu-id="3770c-113">In Word Automation Services in Microsoft SharePoint müssen Sie jetzt die Option hinzugefügte, eine Datei Konvertierung Anforderung erstellen, die verarbeitet wird, sobald Sie einreichen und die Konvertierung wird sofort gestartet und hängt SharePoint Zeitgeberauftrag nicht.</span><span class="sxs-lookup"><span data-stu-id="3770c-113">Now, in Word Automation Services in Microsoft SharePoint, you have the added option to create a file conversion request that's processed as soon as you submit it and the conversion is started immediately and does not depend on the SharePoint Timer Job.</span></span> 
  
    
    
<span data-ttu-id="3770c-p103">Eine Möglichkeit zum Unterschied zwischen auf Anforderung Datei Konvertierung Anfragen und SharePoint für den Zeitgeberauftrag für basierenden Konvertierung vorstellen Aufträge besteht darin, die bei Bedarf Datei Konvertierung Anfragen zu verstehen synchron verarbeitet werden, während der Zeitgeberauftrag für basierenden Konvertierungsaufgaben für SharePoint asynchron erfolgen. Die Architektur Word Automation Services wurde neu gestaltet, zur Unterstützung der neuen Art von bei Bedarf Datei Konvertierung Anforderung und der vorhandenen SharePoint Zeitgeberauftrag basierend Datei Konvertierungen.</span><span class="sxs-lookup"><span data-stu-id="3770c-p103">One way to think about the difference between on demand file conversion requests and the SharePoint Time Job-based conversion jobs is to understand that on demand file conversion requests are handled synchronously, whereas SharePoint Timer Job-based conversion jobs happen asynchronously. The Word Automation Services architecture was redesigned to support both the new kind of on demand file conversion request and the existing SharePoint Timer Job based file conversions.</span></span>
  
    
    

<span data-ttu-id="3770c-116">**Abbildung 1. Word Automation Services 2013-Architektur**</span><span class="sxs-lookup"><span data-stu-id="3770c-116">**Figure 1. Word Automation Services 2013 architecture**</span></span>

  
    
    

  
    
    
![Architektur von Word Automation Services 2013](../images/SPS15CON_WAS_Architecture.png)
  
    
    
<span data-ttu-id="3770c-118">In Abbildung 1, können Sie sehen, dass die Word Automation Services-Architektur beibehält 2 trennen Warteschlangen für Konvertierungen: eine Warteschlange für Demand (unmittelbar) dateikonvertierung Anfragen und eine Warteschlange für SharePoint-Zeitgeberauftrag-basierte Konvertierungsaufgaben bei Bedarf Anfragen im unmittelbaren platziert werden basierend dokumentwarteschlange, in dem die Konvertierungen sofort verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="3770c-118">In figure 1, you can see that the Word Automation Services architecture maintains 2 separate queues for conversions: one queue for on demand (immediate) file conversion requests and one queue for SharePoint Timer Job-based conversion jobs on demand requests are placed in the immediate based document queue where the conversions are processed immediately.</span></span>
  
    
    
<span data-ttu-id="3770c-p104">Im Gegensatz dazu werden der Zeitgeberauftrag für die SharePoint-basierte Konvertierung Aufträge in der Warteschlange Zeitgeberauftrag basierendes Dokument platziert. In dem Intervall für Word Automation Services Konvertierungsaufgaben für diese Anforderungen zu starten. Konvertierung Anforderungen in der Warteschlange sofortige basierendes Dokument haben immer Vorrang gegenüber Konvertierung Aufträge in der Warteschlange Zeitgeberauftrag basierendes Dokument.</span><span class="sxs-lookup"><span data-stu-id="3770c-p104">In contrast, the SharePoint Timer Job-based conversion jobs are placed in the Timer Job-based document queue. Conversion jobs for these requests start at the interval set for Word Automation Services. Conversion requests in the immediate-based document queue always have priority over conversion jobs in the Timer Job-based document queue.</span></span>
  
    
    

### <a name="key-points"></a><span data-ttu-id="3770c-122">Wichtige Punkte</span><span class="sxs-lookup"><span data-stu-id="3770c-122">Key points</span></span>


- <span data-ttu-id="3770c-p105">Eine on Demand Datei Konvertierung Anforderung ist ein zusätzliches Feature und nicht ersetzen den vorhandenen SharePoint-Zeitgeberauftrag-basierte Konvertierungsauftrag. Dies bedeutet, dass die Lösungen, die kompiliert und in SharePoint 2010 ausgeführt werden hingegen weiterhin kompilieren und Ausführen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3770c-p105">An on demand file conversion request is an additional feature and doesn't replace the existing SharePoint Timer Job-based conversion job. That means that solutions that compiled and ran in SharePoint 2010 will continue to compile and run in SharePoint.</span></span>
    
  
- <span data-ttu-id="3770c-125">Sie können bei Bedarf Datei Konvertierung Anfragen nur für eine Datei zu einem Zeitpunkt tätigen</span><span class="sxs-lookup"><span data-stu-id="3770c-125">You can make on demand file conversion requests for only one file at a time</span></span>
    
  
- <span data-ttu-id="3770c-p106">Word Automation Services wird immer auf Anforderung Datei Konvertierungsaufgaben über Konvertierungsaufgaben basierend auf den Zeitgeberauftrag SharePoint bevorzugen. Wenn Word Automation Services bereits auf eine Datei Konvertierungsauftrag, die die SharePoint Zeitgeberauftrag verwendet funktionsfähig ist, wird Word Automation Services unterbrechen diese Aufgabe und an bis zum Abschluss der on Demand Datei Konvertierungsauftrag arbeiten zu wechseln. Wechselt dann zurück, um den SharePoint Zeitgeberauftrag für basierenden Datei Konvertierungsauftrag arbeiten</span><span class="sxs-lookup"><span data-stu-id="3770c-p106">Word Automation Services will always prioritize on demand file conversion jobs over conversion jobs based on the SharePoint Timer Job. If Word Automation Services is already working on a file conversion job that uses the SharePoint Timer Job, Word Automation Services will interrupt that job and switch over to work on the on demand file conversion job until it is completed. It will then switch back to work on the SharePoint Timer Job-based file conversion job</span></span>
    
  

## <a name="perform-file-conversions-on-streams"></a><span data-ttu-id="3770c-129">Führen Sie die Datei Konvertierungen auf Datenströme</span><span class="sxs-lookup"><span data-stu-id="3770c-129">Perform file conversions on streams</span></span>
<span data-ttu-id="3770c-130"><a name="was15PerformStreamConversion"> </a></span><span class="sxs-lookup"><span data-stu-id="3770c-130"></span></span>

<span data-ttu-id="3770c-p107">Das neue Feature in Word Automation Services in Microsoft SharePoint wird unterstützt für die Konvertierung von Streams. In SharePoint 2010 können Sie nur Dateien konvertieren, die in SharePoint Bibliotheken gespeichert wurden. Jetzt können Sie Dateien konvertieren, die außerhalb der SharePoint mithilfe von Streams gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="3770c-p107">The other new feature in Word Automation Services in Microsoft SharePoint is support for converting streams. In SharePoint 2010, you could only convert files that were stored in SharePoint libraries. Now you can also convert files that are stored outside SharePoint using streams.</span></span>
  
    
    

### <a name="key-points"></a><span data-ttu-id="3770c-134">Wichtige Punkte</span><span class="sxs-lookup"><span data-stu-id="3770c-134">Key points</span></span>


- <span data-ttu-id="3770c-135">Sie können nur Datenströme als Eingabe verwenden, beim Erstellen einer on Demand Datei Konvertierungsauftrag</span><span class="sxs-lookup"><span data-stu-id="3770c-135">You can only use streams as input when you're creating an on demand file conversion job</span></span>
    
  
- <span data-ttu-id="3770c-136">Aufgrund der vorstehenden Punkt können Sie nur einen Datenstrom zu einem Zeitpunkt konvertieren</span><span class="sxs-lookup"><span data-stu-id="3770c-136">Because of the foregoing point, you can only convert one stream at a time</span></span>
    
  
<span data-ttu-id="3770c-137">Durch die hinzugefügte auf Anforderung Datei Konvertierung Anfragen und Unterstützung für das Konvertieren von Datenströmen wurde Word Automation Services erheblich verbessert, um einen größeren Wertebereich dokumentkonvertierung Szenarien zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="3770c-137">With the addition of on demand file conversion requests and support for converting streams, Word Automation Services has been significantly enhanced to enable a greater range of document conversion scenarios.</span></span>
  
    
    

### <a name="additional-resources"></a><span data-ttu-id="3770c-138">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3770c-138">Additional resources</span></span>
<span data-ttu-id="3770c-139"><a name="was15AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3770c-139"></span></span>


-  [<span data-ttu-id="3770c-140">Word Automation Services in SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="3770c-140">Word Automation Services in SharePoint Server 2010</span></span>](http://msdn.microsoft.com/en-us/library/ee558278)
    
  
-  [<span data-ttu-id="3770c-141">Word Automation Services-Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="3770c-141">Word Automation Services Class Library</span></span>](http://msdn.microsoft.com/en-us/library/ee559408)
    
  

