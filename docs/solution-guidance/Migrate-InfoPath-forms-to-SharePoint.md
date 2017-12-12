---
title: Migrieren von InfoPath-Formularen in SharePoint 2013
ms.date: 11/03/2017
ms.openlocfilehash: 9efe83a8e3b5e37c091b2ea9d92bad401ebd0e7b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="migrate-infopath-forms-to-sharepoint-2013"></a><span data-ttu-id="89546-102">Migrieren von InfoPath-Formularen in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="89546-102">Migrate InfoPath forms to SharePoint 2013</span></span>

<span data-ttu-id="89546-103">Migrieren von InfoPath-Formularen in Ihrer SharePoint-Add-ins zu anderen unterstützten Lösungen, wie Access-Anwendungen, sandkastenlösungen oder das Add-In Modell.</span><span class="sxs-lookup"><span data-stu-id="89546-103">Migrate InfoPath forms in your SharePoint add-ins to other supported solutions, such as Access applications, sandbox solutions, or the add-in model.</span></span>

<span data-ttu-id="89546-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="89546-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="89546-105">Wenn Sie InfoPath als Grundlage zum Erstellen von Formularen in Ihrer-add-ins verwenden, ist nun die Zeit bis zur erwägen, zum Migrieren von Formularen zu anderen Lösungen.</span><span class="sxs-lookup"><span data-stu-id="89546-105">If you're using InfoPath as the basis for creating forms in your add-ins, now is the time to start thinking about migrating your forms to other solutions.</span></span> <span data-ttu-id="89546-106">InfoPath derzeit wird zwar unterstützt, InfoPath 2013 ist die letzte Version des Desktops Client InfoPath und InfoPath Forms Services in SharePoint 2013 ist die letzte Version von InfoPath Forms Services.</span><span class="sxs-lookup"><span data-stu-id="89546-106">Although InfoPath is currently supported, InfoPath 2013 is the last release of the desktop InfoPath client, and InfoPath Forms Services in SharePoint 2013 is the last release of InfoPath Forms Services.</span></span> <span data-ttu-id="89546-107">Der Client und der lokalen Version von InfoPath Forms Services in SharePoint 2013 werden bis 2023 vollständig unterstützt.</span><span class="sxs-lookup"><span data-stu-id="89546-107">The client and the on-premises version of InfoPath Forms Services in SharePoint 2013 will be fully supported until 2023.</span></span> <span data-ttu-id="89546-108">Der Forms-Dienst wird in Office 365 bis mindestens die nächste Hauptversion von Office unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="89546-108">The forms service will be supported in Office 365 until at least the next major release of Office.</span></span>

<span data-ttu-id="89546-109">Um von InfoPath-Formularen zu ersetzen, können Sie eine der folgenden alternativen auswählen:</span><span class="sxs-lookup"><span data-stu-id="89546-109">To replace your InfoPath forms, you can choose one of the following alternatives:</span></span>

- <span data-ttu-id="89546-110">Verwenden von Access-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="89546-110">Use Access applications.</span></span>

- <span data-ttu-id="89546-111">Verwenden Sie Microsoft Nachrichtenübermittlung und des Microsoft PowerApps.</span><span class="sxs-lookup"><span data-stu-id="89546-111">Use Microsoft Flow and Microsoft PowerApps.</span></span>
    
- <span data-ttu-id="89546-112">Verschieben Sie komplexe Verhaltensweisen in neue Add-In-Modell und Client Side Entwicklungen.</span><span class="sxs-lookup"><span data-stu-id="89546-112">Move complex behaviors to new add-in model and client side developments.</span></span>
    
<span data-ttu-id="89546-113">Die ersten beiden Lösungen, wird empfohlen, weil Information Worker, die nicht wissen, wie schreiben und Bereitstellen von alternativen codebasierte implementiert werden können.</span><span class="sxs-lookup"><span data-stu-id="89546-113">We recommend the first two solutions, because information workers who don't know how to write and deploy code-based alternatives can implement them.</span></span> <span data-ttu-id="89546-114">Die folgende Tabelle beschreibt die Szenarien für die einzelnen Alternative am besten geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="89546-114">The following table describes the scenarios for which each alternative is best suited.</span></span>

<span data-ttu-id="89546-115">**Alternativen zur InfoPath in SharePoint 2013**</span><span class="sxs-lookup"><span data-stu-id="89546-115">**Alternatives to InfoPath in SharePoint 2013**</span></span>

|<span data-ttu-id="89546-116">**Alternative**</span><span class="sxs-lookup"><span data-stu-id="89546-116">**Alternative**</span></span>|<span data-ttu-id="89546-117">**Szenario**</span><span class="sxs-lookup"><span data-stu-id="89546-117">**Scenario**</span></span>|
|:-----|:-----|
|<span data-ttu-id="89546-118">Access-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="89546-118">Access applications</span></span>|<span data-ttu-id="89546-119">Diese Option unterstützt mehrere Formulare, die relationale Daten in mehrere Tabellen Access, Excel-Tabellen und/oder SharePoint-Listen behandelt.</span><span class="sxs-lookup"><span data-stu-id="89546-119">This option supports multiple forms that handle relational data contained in multiple Access tables, Excel tables, and/or SharePoint lists.</span></span>|
|<span data-ttu-id="89546-120">Verwenden Sie Microsoft Nachrichtenübermittlung und des Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="89546-120">Use Microsoft Flow and Microsoft PowerApps</span></span>|<span data-ttu-id="89546-121">Dies ist die unsere empfohlener Ansatz für die Erweiterung von Listen von SharePoint-Hauptbenutzer.</span><span class="sxs-lookup"><span data-stu-id="89546-121">This is the our recommended approach for extending lists by SharePoint power users .</span></span>|
|<span data-ttu-id="89546-122">Neue Add-In-Modell und Client Side Entwicklungen</span><span class="sxs-lookup"><span data-stu-id="89546-122">New add-in model and client side developments</span></span> |<span data-ttu-id="89546-123">Sie können komplexe Formulare beschäftigte Mitarbeiter umfassende Code in vom Anbieter gehosteten-add-ins oder Client Side-Webparts zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="89546-123">You can convert complex forms driven by extensive code into provider-hosted add-ins or client side web parts.</span></span> <span data-ttu-id="89546-124">Diese Option erfordert Ressourcen für Entwickler.</span><span class="sxs-lookup"><span data-stu-id="89546-124">This option requires developer resources.</span></span>|

## <a name="see-also"></a><span data-ttu-id="89546-125">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="89546-125">See also</span></span>
<span data-ttu-id="89546-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="89546-126"></span></span>

-  [<span data-ttu-id="89546-127">Muster und Methoden für InfoPath-Transformation Anleitungen</span><span class="sxs-lookup"><span data-stu-id="89546-127">Patterns and Practices InfoPath transformation guidance</span></span>](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath) 

-  [<span data-ttu-id="89546-128">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="89546-128">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="89546-129">Office 365-Entwicklungsmuster und -übungen auf GitHub</span><span class="sxs-lookup"><span data-stu-id="89546-129">Office 365 Development Patterns and Practices on GitHub</span></span>](https://github.com/SharePoint/PnP)
