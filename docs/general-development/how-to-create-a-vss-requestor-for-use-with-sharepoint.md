---
title: "Vorgehensweise Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 63b3145b-ece2-4acf-b58a-fd8b50303030
ms.openlocfilehash: f2dbb3c94cc8196f24cbbb48862116854cc47044
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-vss-requestor-for-use-with-sharepoint"></a><span data-ttu-id="76745-102">Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="76745-102">How to: Create a VSS requestor for use with SharePoint</span></span>
 <span data-ttu-id="76745-103">**Zusammenfassung:** Weitere Informationen zum Erstellen einer Anforderers für die Verwendung mit der Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) Writer für Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="76745-103">**Summary:** Learn about how to create a requestor for use with the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint.</span></span>
## <a name="writing-a-requestor"></a><span data-ttu-id="76745-104">Schreiben eines Requestors</span><span class="sxs-lookup"><span data-stu-id="76745-104">Writing a requestor</span></span>

<span data-ttu-id="76745-p101">Verfassen eines Anforderers für das Sichern und Wiederherstellen von SharePoint Foundation mithilfe des VSS ist identisch mit dem zum Schreiben eines Anforderers für jede andere Windows-basierten Anwendung wie Microsoft SQL Server oder Microsoft Exchange Server. Entwickler von backup-Anwendungen sollten die Anweisungen in der  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/de-de/library/aa384649%28VS.85%29.aspx) und [Volume Shadow Copy-API-Referenz](http://msdn.microsoft.com/de-de/library/aa384648%28VS.85%29.aspx) Anwendungen erstellen, die ordnungsgemäß sichern und Wiederherstellen von Daten SharePoint Foundation folgen.</span><span class="sxs-lookup"><span data-stu-id="76745-p101">The process of writing a requestor for backing up and restoring SharePoint Foundation by using VSS is the same as that for writing a requestor for any other Windows-based application such as Microsoft SQL Server or Microsoft Exchange Server. Developers of backup applications should follow the procedures outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/de-de/library/aa384649%28VS.85%29.aspx) and [Volume Shadow Copy API Reference](http://msdn.microsoft.com/de-de/library/aa384648%28VS.85%29.aspx) to build applications that can properly back up and restore SharePoint Foundation data.</span></span>
  
    
    

## <a name="next-steps"></a><span data-ttu-id="76745-107">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="76745-107">Next steps</span></span>
<span data-ttu-id="76745-108"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="76745-108"><a name="Next"> </a></span></span>

<span data-ttu-id="76745-109">Erfahren Sie, wie den Anforderer zum Sichern und Wiederherstellen von SharePoint und Suchanwendungen und Indizes verwendet:</span><span class="sxs-lookup"><span data-stu-id="76745-109">Learn how to use the requestor to back up and restore SharePoint and search applications and indexes:</span></span>
  
    
    

-  [<span data-ttu-id="76745-110">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="76745-110">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="76745-111">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="76745-111">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="76745-112">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="76745-112">Additional resources</span></span>
<span data-ttu-id="76745-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="76745-113"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="76745-114">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="76745-114">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

