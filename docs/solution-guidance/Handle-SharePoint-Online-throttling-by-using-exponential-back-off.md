---
title: Behandeln von SharePoint Online mithilfe von wieder aus exponentielle Drosselung
ms.date: 11/03/2017
ms.openlocfilehash: 092b5072ae26f7f815eaa6133512865512129874
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="handle-sharepoint-online-throttling-by-using-exponential-back-off"></a>Behandeln von SharePoint Online mithilfe von wieder aus exponentielle Drosselung

Erfahren Sie, wie Drosselungen in SharePoint Online mithilfe der exponentiellen Back-off Technik behandeln. 
    
_**Gilt für:** Office 365 | SharePoint Online | SharePoint Server 2013_

SharePoint Online arbeitet mit Drosselung um zu unterbinden, dass Ressourcen übermäßig verbrauchen. Wenn ein Benutzer CSOM oder REST Code ausgeführt, die die Verwendung Grenzwerte überschreitet wird, anforderungsdrosselungen SharePoint Online weiteren Anforderung vom Benutzer für einen Zeitraum. 
    
Das [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) -Codebeispiel in [Office 365 Developer Mustern und Methoden Repository](https://github.com/SharePoint/PnP) zeigt, wie die exponentielle Back deaktiviert Verfahren zum Verarbeiten von Drosselungen in SharePoint Online zu implementieren. Wenn Sie in SharePoint Online gedrosselt erhalten möchten, wartet die exponentielle Back deaktiviert Technik stetig längere Zeit, bevor Sie den Code, der gedrosselt wurde wiederholen.
    
Weitere Informationen zur Einschränkung in SharePoint Online (beispielsweise Ursachen, Grenzwerte usw.) und eine Erläuterung des Codebeispiels Core.Throttling finden Sie unter [Vorgehensweise: verhindern, dass gedrosselt oder in SharePoint Online blockiert](https://msdn.microsoft.com/library/office/dn889829.aspx). 

Darüber hinaus in der Stichprobe [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) checken Sie die Erweiterungsmethode ExecuteQueryImplementation aus. ExecuteQueryImplementation ist in [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core)enthalten.    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [ClientContextExtensions.cs-Beispiel](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs)
    
-  [Vorgehensweise: verhindern, dass gedrosselt oder blockiert in SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx)
