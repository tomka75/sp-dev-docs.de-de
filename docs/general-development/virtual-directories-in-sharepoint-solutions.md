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
# <a name="virtual-directories-in-sharepoint-solutions"></a>Virtuelle Verzeichnisse in SharePoint-Lösungen
Erfahren Sie, wie Änderungen im virtuellen Verzeichnissystem auswirken, wie Sie Farmlösungen in SharePoint erstellen.
## <a name="make-your-solutions-compatible-with-the-new-ui-mode-system"></a>Stellen Sie Ihre Lösungen mit dem neuen Benutzeroberfläche Modus System kompatibel

Wenn Sie die Microsoft SharePoint 2010 Software Development Kit (SDK) verwenden, aber für SharePoint entwickeln, ist es eine Änderung im virtuellen Verzeichnissystem, das Sie während der Arbeit berücksichtigen müssen, an. Die Änderung erfolgt ist eine Auswirkung der neuen SharePoint-Feature, mit dem eine Websitesammlung im entweder SharePoint 2010 oder SharePoint Modus ausgeführt. Die Modi werden manchmal Kompatibilität Ebenen oderBenutzeroberflächenversionenbezeichnet. SharePoint muss für die Dateien in die virtuelle Ordner  `_layouts` oder `_controltemplates`die Version der Dateien in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ (den 15 Strukturbezeichnet) oder in den entsprechenden 14 Hive, je nach den Modus der Websitesammlung verwenden. Fügt SharePoint "/ 15" in den Pfad des virtuellen Verzeichnisses nach dem Namen des virtuellen Verzeichnisses zu signalisieren, dass die SharePoint-Dateien verwendet werden soll. Keine zusätzlichen generiert gibt an, dass SharePoint 2010 Dateien verwendet werden soll.
  
    
    
Dieses neue System wirkt sich für Sie bei der Entwicklung SharePoint Lösungen und apps, insbesondere, wenn Sie die SharePoint 2010 SDK verwenden. In jeder SharePoint-Add-In (die nur im SharePoint Modus ausgeführt wird) und in jeder SharePoint-Lösung, die Ihnen bekannt ist nur in Websitesammlungen verwendet werden, die im SharePoint Modus ausgeführt werden soll, müssen Sie hinzufügen die "/ 15" sich auf alle  `_layouts` und `_controltemplates` virtuelle Pfade in Ihrer Lösung/App erstellen (es sei denn, Sie der Pfad zu einer ASPX-Datei zeigen) , obwohl diese Zeichenfolge nicht in eine beliebige Anweisungen angezeigt wird Sie in der SharePoint 2010 SDK gelesen. Beispielsweise wenn die SharePoint 2010 SDK Sie `~/_layouts/images/myimage.png`verwenden weist, sollten Sie  `~/_layouts/15/images/myimage.png` verwenden, bei der Entwicklung für SharePoint.
  
    
    
Wenn Sie Ihre Lösung mit Websitesammlungen der beiden Modi kompatibel vornehmen müssen, müssen Sie bestimmen den Modus der aktuellen Websitesammlung und erstellen den virtuellen Pfad entsprechend Logik für die Verzweigung. Die  [CompatibilityLevel]((https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx)) -Eigenschaft, die in allen SharePoint-Clientobjektmodelle und der REST-Schnittstelle verfügbar ist, wird einer Stelle, wo der Code für den Modus überprüfen können. Die [SPUtility]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx)) -Klasse enthält auch mehrere neue Eigenschaften zur Unterstützung bei der Kompatibilitätsebene in Ihren Lösungen verwalten. Diese sind nicht in der Clientobjektmodelle verfügbar. Es gibt mehrere Steuerelemente in SharePoint, die eine **UIVersion** -Eigenschaft verfügbar, die Ihr Code auch verwenden machen, um den aktuellen Kompatibilitätsgrad finden.
  
> [!NOTE] 
> Wenn die Datei im virtuellen Pfad *.aspx ist, erkennt SharePoint automatisch den Modus der aktuellen Websitesammlung und gibt die Datei aus dem entsprechenden Hive zurück. Daher brauchen Sie „/15“ nicht in den virtuellen Pfad einzufügen. 
  
    
    


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Erstellen von Farmlösungen in SharePoint](build-farm-solutions-in-sharepoint.md)
    
  
-  [Planen der Bereitstellung von Farmlösungen für SharePoint]((http://blogs.technet.com/b/mspfe/archive/2013/02/04/planning-deployment-of-farm-solutions-for-sharepoint.aspx))
    
  
-  [SPUtility properties](http://msdn.microsoft.com/library/Properties.T:Microsoft.SharePoint.Utilities.SPUtility.aspx)
    
  

