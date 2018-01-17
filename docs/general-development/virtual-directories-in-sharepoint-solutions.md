---
title: "Virtuelle Verzeichnisse in SharePoint-Lösungen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c26c4160-31be-4358-89cf-082b8a1e6a6c
ms.openlocfilehash: bba15a4ae1866fe9cc39757442dd8d89fe963950
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="virtual-directories-in-sharepoint-solutions"></a><span data-ttu-id="52a55-102">Virtuelle Verzeichnisse in SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="52a55-102">Virtual directories in SharePoint solutions</span></span>
<span data-ttu-id="52a55-103">Erfahren Sie, wie Änderungen im virtuellen Verzeichnissystem auswirken, wie Sie Farmlösungen in SharePoint erstellen.</span><span class="sxs-lookup"><span data-stu-id="52a55-103">Learn about how changes in the virtual directory system affect how you create farm solutions in SharePoint.</span></span>
## <a name="make-your-solutions-compatible-with-the-new-ui-mode-system"></a><span data-ttu-id="52a55-104">Stellen Sie Ihre Lösungen mit dem neuen Benutzeroberfläche Modus System kompatibel</span><span class="sxs-lookup"><span data-stu-id="52a55-104">Make your solutions compatible with the new UI mode system</span></span>

<span data-ttu-id="52a55-p101">Wenn Sie die Microsoft SharePoint 2010 Software Development Kit (SDK) verwenden, aber für SharePoint entwickeln, ist es eine Änderung im virtuellen Verzeichnissystem, das Sie während der Arbeit berücksichtigen müssen, an. Die Änderung erfolgt ist eine Auswirkung der neuen SharePoint-Feature, mit dem eine Websitesammlung im entweder SharePoint 2010 oder SharePoint Modus ausgeführt. Die Modi werden manchmal Kompatibilität Ebenen oderBenutzeroberflächenversionenbezeichnet. SharePoint muss für die Dateien in die virtuelle Ordner  `_layouts` oder `_controltemplates`die Version der Dateien in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ (den 15 Strukturbezeichnet) oder in den entsprechenden 14 Hive, je nach den Modus der Websitesammlung verwenden. Fügt SharePoint "/ 15" in den Pfad des virtuellen Verzeichnisses nach dem Namen des virtuellen Verzeichnisses zu signalisieren, dass die SharePoint-Dateien verwendet werden soll. Keine zusätzlichen generiert gibt an, dass SharePoint 2010 Dateien verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="52a55-p101">When you are using the Microsoft SharePoint 2010 Software Development Kit (SDK), but developing for SharePoint, there is a change in the virtual directory system that you need to consider as you work. The change is a side effect of the new SharePoint feature that enables a site collection to run in either SharePoint 2010 mode or SharePoint mode. The modes are sometimes called compatibility levels orUI versions. For files in the virtual folders  `_layouts` or `_controltemplates`, SharePoint needs to use the version of the files in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ (sometimes called the 15 hive) or in the corresponding 14 hive, depending on the mode of the site collection. SharePoint adds "/15" into the virtual directory path just after the virtual directory name to signal that the SharePoint files should be used. The absence of that extra string indicates that SharePoint 2010 files should be used.</span></span>
  
    
    
<span data-ttu-id="52a55-p102">Dieses neue System wirkt sich für Sie bei der Entwicklung SharePoint Lösungen und apps, insbesondere, wenn Sie die SharePoint 2010 SDK verwenden. In jeder SharePoint-Add-In (die nur im SharePoint Modus ausgeführt wird) und in jeder SharePoint-Lösung, die Ihnen bekannt ist nur in Websitesammlungen verwendet werden, die im SharePoint Modus ausgeführt werden soll, müssen Sie hinzufügen die "/ 15" sich auf alle  `_layouts` und `_controltemplates` virtuelle Pfade in Ihrer Lösung/App erstellen (es sei denn, Sie der Pfad zu einer ASPX-Datei zeigen) , obwohl diese Zeichenfolge nicht in eine beliebige Anweisungen angezeigt wird Sie in der SharePoint 2010 SDK gelesen. Beispielsweise wenn die SharePoint 2010 SDK Sie `~/_layouts/images/myimage.png`verwenden weist, sollten Sie  `~/_layouts/15/images/myimage.png` verwenden, bei der Entwicklung für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="52a55-p102">This new system has implications for you as you develop SharePoint solutions and apps, particularly when you are using the SharePoint 2010 SDK. In any SharePoint Add-in (which only run in SharePoint mode) and in any SharePoint solution that you know is only going to be used in site collections that run in SharePoint mode, you need to add the "/15" yourself to all the  `_layouts` and `_controltemplates` virtual paths you create in your solution/app. (unless the path is pointing to an *.aspx file), even though this string does not appear in any instructions you read in the SharePoint 2010 SDK. For example, if the SharePoint 2010 SDK instructs you to use `~/_layouts/images/myimage.png`, you should use  `~/_layouts/15/images/myimage.png` when you are developing for SharePoint.</span></span>
  
    
    
<span data-ttu-id="52a55-p103">Wenn Sie Ihre Lösung mit Websitesammlungen der beiden Modi kompatibel vornehmen müssen, müssen Sie bestimmen den Modus der aktuellen Websitesammlung und erstellen den virtuellen Pfad entsprechend Logik für die Verzweigung. Die  [CompatibilityLevel](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx) -Eigenschaft, die in allen SharePoint-Clientobjektmodelle und der REST-Schnittstelle verfügbar ist, wird einer Stelle, wo der Code für den Modus überprüfen können. Die [SPUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx) -Klasse enthält auch mehrere neue Eigenschaften zur Unterstützung bei der Kompatibilitätsebene in Ihren Lösungen verwalten. Diese sind nicht in der Clientobjektmodelle verfügbar. Es gibt mehrere Steuerelemente in SharePoint, die eine **UIVersion** -Eigenschaft verfügbar, die Ihr Code auch verwenden machen, um den aktuellen Kompatibilitätsgrad finden.</span><span class="sxs-lookup"><span data-stu-id="52a55-p103">If you need to make your solution compatible with site collections of either mode, you need branching logic to determine the mode of the current site collection and construct the virtual path accordingly. The  [CompatibilityLevel](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx) property, which is also available in all the SharePoint client object models and the REST interface, is one place where your code can check for the mode. The [SPUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx) class also has several new properties to aid in managing compatibility level in your solutions. These are not available in the client object models. Finally, there are several controls in SharePoint that expose a **UIVersion** property that your code can also use to find the current compatibility level.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="52a55-120">Wenn die Datei im virtuellen Pfad *.aspx ist, erkennt SharePoint automatisch den Modus der aktuellen Websitesammlung und gibt die Datei aus dem entsprechenden Hive zurück.</span><span class="sxs-lookup"><span data-stu-id="52a55-120">Note: If the file in the virtual path is *.aspx, SharePoint will automatically detect the mode of the current site collection and return the file from the appropriate hive.</span></span> <span data-ttu-id="52a55-121">Daher brauchen Sie „/15“ nicht in den virtuellen Pfad einzufügen.</span><span class="sxs-lookup"><span data-stu-id="52a55-121">So you do not have to insert the "/15" into the virtual path.</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="52a55-122">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="52a55-122">See also</span></span>
<span data-ttu-id="52a55-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="52a55-123"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="52a55-124">Erstellen von Farmlösungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="52a55-124">Build farm solutions in SharePoint</span></span>](build-farm-solutions-in-sharepoint.md)
    
  
-  <span data-ttu-id="52a55-125">[Planen der Bereitstellung von Farmlösungen für SharePoint](http://blogs.technet.com/b/mspfe/archive/2013/02/04/planning-deployment-of-farm-solutions-for-sharepoint.aspx)</span><span class="sxs-lookup"><span data-stu-id="52a55-125">[Planning Deployment of Farm Solutions for SharePoint](http://blogs.technet.com/b/mspfe/archive/2013/02/04/planning-deployment-of-farm-solutions-for-sharepoint.aspx)</span></span>
    
  
-  [<span data-ttu-id="52a55-126">SPUtility properties</span><span class="sxs-lookup"><span data-stu-id="52a55-126">SPUtility properties</span></span>](http://msdn.microsoft.com/library/Properties.T:Microsoft.SharePoint.Utilities.SPUtility.aspx)
    
  

