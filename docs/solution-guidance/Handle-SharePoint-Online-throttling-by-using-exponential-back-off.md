---
title: Behandeln von SharePoint Online mithilfe von wieder aus exponentielle Drosselung
ms.date: 11/03/2017
ms.openlocfilehash: 5fe327f1d80ba38c67e82bfa82f4743c13e65510
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="handle-sharepoint-online-throttling-by-using-exponential-back-off"></a><span data-ttu-id="55b42-102">Behandeln von SharePoint Online mithilfe von wieder aus exponentielle Drosselung</span><span class="sxs-lookup"><span data-stu-id="55b42-102">Handle SharePoint Online throttling by using exponential back off</span></span>

<span data-ttu-id="55b42-103">Erfahren Sie, wie Drosselungen in SharePoint Online mithilfe der exponentiellen Back-off Technik behandeln.</span><span class="sxs-lookup"><span data-stu-id="55b42-103">Learn how to handle throttling in SharePoint Online by using the exponential back-off technique.</span></span> 
    
<span data-ttu-id="55b42-104">_**Gilt für:** Office 365 | SharePoint Online | SharePoint Server 2013_</span><span class="sxs-lookup"><span data-stu-id="55b42-104">_**Applies to:** Office 365 | SharePoint Online | SharePoint Server 2013_</span></span>

<span data-ttu-id="55b42-105">SharePoint Online arbeitet mit Drosselung um zu unterbinden, dass Ressourcen übermäßig verbrauchen.</span><span class="sxs-lookup"><span data-stu-id="55b42-105">SharePoint Online uses throttling to prevent users from over-consuming resources.</span></span> <span data-ttu-id="55b42-106">Wenn ein Benutzer CSOM oder REST Code ausgeführt, die die Verwendung Grenzwerte überschreitet wird, anforderungsdrosselungen SharePoint Online weiteren Anforderung vom Benutzer für einen Zeitraum.</span><span class="sxs-lookup"><span data-stu-id="55b42-106">When a user runs CSOM or REST code that exceeds usage limits, SharePoint Online throttles any further request from the user for a period of time.</span></span> 
    
<span data-ttu-id="55b42-107">Das [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) -Codebeispiel in [Office 365 Developer Mustern und Methoden Repository](https://github.com/SharePoint/PnP) zeigt, wie die exponentielle Back deaktiviert Verfahren zum Verarbeiten von Drosselungen in SharePoint Online zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="55b42-107">The [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) code sample in the [Office 365 Developer Patterns and Practices repository](https://github.com/SharePoint/PnP) shows how to implement the exponential back off technique to handle throttling in SharePoint Online.</span></span> <span data-ttu-id="55b42-108">Wenn Sie in SharePoint Online gedrosselt erhalten möchten, wartet die exponentielle Back deaktiviert Technik stetig längere Zeit, bevor Sie den Code, der gedrosselt wurde wiederholen.</span><span class="sxs-lookup"><span data-stu-id="55b42-108">When you get throttled in SharePoint Online, the exponential back off technique waits progressively longer periods of time before retrying the code that was throttled.</span></span>
    
<span data-ttu-id="55b42-109">Weitere Informationen zur Einschränkung in SharePoint Online (beispielsweise Ursachen, Grenzwerte usw.) und eine Erläuterung des Codebeispiels Core.Throttling finden Sie unter [Vorgehensweise: verhindern, dass gedrosselt oder in SharePoint Online blockiert](https://msdn.microsoft.com/library/office/dn889829.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b42-109">For more information about throttling in SharePoint Online (for example, causes, limits, and so on), and an explanation of the Core.Throttling code sample, see [How to: Avoid getting throttled or blocked in SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx).</span></span> 

<span data-ttu-id="55b42-110">Darüber hinaus in der Stichprobe [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) checken Sie die Erweiterungsmethode ExecuteQueryImplementation aus.</span><span class="sxs-lookup"><span data-stu-id="55b42-110">Also, in the [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) sample, check out the ExecuteQueryImplementation extension method.</span></span> <span data-ttu-id="55b42-111">ExecuteQueryImplementation ist in [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core)enthalten.</span><span class="sxs-lookup"><span data-stu-id="55b42-111">ExecuteQueryImplementation is included in [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core).</span></span>    

## <a name="additional-resources"></a><span data-ttu-id="55b42-112">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="55b42-112">Additional resources</span></span>
<span data-ttu-id="55b42-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="55b42-113"></span></span>

-  [<span data-ttu-id="55b42-114">Ausgesprochen</span><span class="sxs-lookup"><span data-stu-id="55b42-114">Solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="55b42-115">ClientContextExtensions.cs-Beispiel</span><span class="sxs-lookup"><span data-stu-id="55b42-115">ClientContextExtensions.cs sample</span></span>](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs)
    
-  [<span data-ttu-id="55b42-116">Vorgehensweise: verhindern, dass gedrosselt oder blockiert in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="55b42-116">How to: Avoid getting throttled or blocked in SharePoint Online</span></span>](https://msdn.microsoft.com/library/office/dn889829.aspx)
