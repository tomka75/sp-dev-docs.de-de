---
title: "Vorgehensweise Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint"
ms.prod: SHAREPOINT
ms.assetid: 63b3145b-ece2-4acf-b58a-fd8b50303030
ms.openlocfilehash: 88876b33f5fdafcab57ada0fea4c3bd763c7ca45
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="how-to-create-a-vss-requestor-for-use-with-sharepoint"></a><span data-ttu-id="674c4-102">Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="674c4-102">How to: Create a VSS requestor for use with SharePoint</span></span>
 <span data-ttu-id="674c4-103">**Zusammenfassung:** Weitere Informationen zum Erstellen einer Anforderers für die Verwendung mit der Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) Writer für Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="674c4-103">**Summary:** Learn about how to create a requestor for use with the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint.</span></span>
## <a name="writing-a-requestor"></a><span data-ttu-id="674c4-104">Schreiben eines Requestors</span><span class="sxs-lookup"><span data-stu-id="674c4-104">Writing a requestor</span></span>

<span data-ttu-id="674c4-p101">Verfassen eines Anforderers für das Sichern und Wiederherstellen von SharePoint Foundation mithilfe des VSS ist identisch mit dem zum Schreiben eines Anforderers für jede andere Windows-basierten Anwendung wie Microsoft SQL Server oder Microsoft Exchange Server. Entwickler von backup-Anwendungen sollten die Anweisungen in der  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx) und [Volume Shadow Copy-API-Referenz](http://msdn.microsoft.com/en-us/library/aa384648%28VS.85%29.aspx) Anwendungen erstellen, die ordnungsgemäß sichern und Wiederherstellen von Daten SharePoint Foundation folgen.</span><span class="sxs-lookup"><span data-stu-id="674c4-p101">The process of writing a requestor for backing up and restoring SharePoint Foundation by using VSS is the same as that for writing a requestor for any other Windows-based application such as Microsoft SQL Server or Microsoft Exchange Server. Developers of backup applications should follow the procedures outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx) and [Volume Shadow Copy API Reference](http://msdn.microsoft.com/en-us/library/aa384648%28VS.85%29.aspx) to build applications that can properly back up and restore SharePoint Foundation data.</span></span>
  
    
    

## <a name="next-steps"></a><span data-ttu-id="674c4-107">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="674c4-107">Next steps</span></span>
<span data-ttu-id="674c4-108"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="674c4-108"></span></span>

<span data-ttu-id="674c4-109">Erfahren Sie, wie den Anforderer zum Sichern und Wiederherstellen von SharePoint und Suchanwendungen und Indizes verwendet:</span><span class="sxs-lookup"><span data-stu-id="674c4-109">Learn how to use the requestor to back up and restore SharePoint and search applications and indexes:</span></span>
  
    
    

-  [<span data-ttu-id="674c4-110">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="674c4-110">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor)
    
  
-  [<span data-ttu-id="674c4-111">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="674c4-111">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using)
    
  

## <a name="additional-resources"></a><span data-ttu-id="674c4-112">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="674c4-112">Additional resources</span></span>
<span data-ttu-id="674c4-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="674c4-113"></span></span>


-  [<span data-ttu-id="674c4-114">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="674c4-114">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service)
    
  

