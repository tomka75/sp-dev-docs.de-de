---
title: "Erstellen eines VSS-Anforderers für die Verwendung mit SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 63b3145b-ece2-4acf-b58a-fd8b50303030
ms.openlocfilehash: 816d3be516ff144c66aad667f6cff1173f9235f5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-vss-requestor-for-use-with-sharepoint"></a><span data-ttu-id="5f6fb-102">Erstellen eines VSS-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f6fb-102">Create a VSS requestor for use with SharePoint</span></span>

<span data-ttu-id="5f6fb-103">Weitere Informationen zum Erstellen eines Anforderers für die Verwendung mit dem VSS-Writer (Volume Shadow Copy Service, Volumeschattenkopie-Dienst) für Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f6fb-103">Summary: Learn about how to create a requestor for use with the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint.</span></span>

## <a name="writing-a-requestor"></a><span data-ttu-id="5f6fb-104">Schreiben eines Requestors</span><span class="sxs-lookup"><span data-stu-id="5f6fb-104">Writing a requestor</span></span>

<span data-ttu-id="5f6fb-p101">Verfassen eines Anforderers für das Sichern und Wiederherstellen von SharePoint Foundation mithilfe des VSS ist identisch mit dem zum Schreiben eines Anforderers für jede andere Windows-basierten Anwendung wie Microsoft SQL Server oder Microsoft Exchange Server. Entwickler von backup-Anwendungen sollten die Anweisungen in der  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/de-DE/library/aa384649%28VS.85%29.aspx) und [Volume Shadow Copy-API-Referenz](http://msdn.microsoft.com/de-DE/library/aa384648%28VS.85%29.aspx) Anwendungen erstellen, die ordnungsgemäß sichern und Wiederherstellen von Daten SharePoint Foundation folgen.</span><span class="sxs-lookup"><span data-stu-id="5f6fb-p101">The process of writing a requestor for backing up and restoring SharePoint Foundation by using VSS is the same as that for writing a requestor for any other Windows-based application such as Microsoft SQL Server or Microsoft Exchange Server. Developers of backup applications should follow the procedures outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/de-DE/library/aa384649%28VS.85%29.aspx) and [Volume Shadow Copy API Reference](http://msdn.microsoft.com/de-DE/library/aa384648%28VS.85%29.aspx) to build applications that can properly back up and restore SharePoint Foundation data.</span></span>
  
    
    

## <a name="next-steps"></a><span data-ttu-id="5f6fb-107">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="5f6fb-107">Next steps</span></span>
<span data-ttu-id="5f6fb-108"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="5f6fb-108"><a name="Next"> </a></span></span>

<span data-ttu-id="5f6fb-109">Erfahren Sie, wie den Anforderer zum Sichern und Wiederherstellen von SharePoint und Suchanwendungen und Indizes verwendet:</span><span class="sxs-lookup"><span data-stu-id="5f6fb-109">Learn how to use the requestor to back up and restore SharePoint and search applications and indexes:</span></span>
  
    
    

-  [<span data-ttu-id="5f6fb-110">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="5f6fb-110">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="5f6fb-111">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="5f6fb-111">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

## <a name="see-also"></a><span data-ttu-id="5f6fb-112">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="5f6fb-112">See also</span></span>
<span data-ttu-id="5f6fb-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5f6fb-113"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="5f6fb-114">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="5f6fb-114">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

