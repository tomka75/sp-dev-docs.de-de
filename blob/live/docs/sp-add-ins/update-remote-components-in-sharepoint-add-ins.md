---
title: Aktualisieren von Remotekomponenten in SharePoint-Add-Ins
description: Aktualisieren Sie die Remotewebanwendungen und -datenbanken in einem SharePoint-Add-In.
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 756d6d58b32924bdfb491e1aa04805f9877c9366
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a><span data-ttu-id="70aa5-103">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="70aa5-103">Update remote components in SharePoint Add-ins</span></span>

<span data-ttu-id="70aa5-104">Machen Sie sich vor Beginn mit dem Thema [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und den darin aufgeführten erforderlichen Komponenten und Kernkonzepten vertraut.</span><span class="sxs-lookup"><span data-stu-id="70aa5-104">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in it.</span></span>

<span data-ttu-id="70aa5-105">Aufgrund der großen Unterschiede bei Plattformen und Mandantensystemen können zur Aktualisierung der Remotekomponenten größtenteils nur sehr allgemeine Hinweise gegeben werden.</span><span class="sxs-lookup"><span data-stu-id="70aa5-105">For the most part, only very general advice can be provided for updating the remote components because of the wide differences in platforms and tenancy systems. The following two sections provide some guidance.</span></span> <span data-ttu-id="70aa5-106">Im folgende Abschnitt finden Sie einige Richtlinien.</span><span class="sxs-lookup"><span data-stu-id="70aa5-106">The following section provides some guidance.</span></span>

<span data-ttu-id="70aa5-107">Für ein vom Anbieter gehostetes SharePoint-Add-In aktualisieren Sie die Remotekomponenten mit der bewährten Aktualisierungsmethode der Plattform, auf der die Komponenten gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="70aa5-107">For a provider-hosted SharePoint Add-in, you update the remote components using the best update practices of the platform on which the components are hosted. Just as the remote components of a provider-hosted add-in are installed separately from the installation of the SharePoint Add-in itself, they are also updated separately. Some points to consider:</span></span> <span data-ttu-id="70aa5-108">Ebenso wie die Remotekomponenten eines vom Anbieter gehosteten Add-Ins separat von der Installation des SharePoint-Add-Ins installiert werden, werden sie auch separat aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="70aa5-108">For a provider-hosted SharePoint Add-in, you update the remote components using the best update practices of the platform on which the components are hosted. Just as the remote components of a provider-hosted add-in are installed separately from the installation of the SharePoint Add-in itself, they are also updated separately. Some points to consider:</span></span> <span data-ttu-id="70aa5-109">Überlegungen:</span><span class="sxs-lookup"><span data-stu-id="70aa5-109">Some points to consider:</span></span>

- <span data-ttu-id="70aa5-110">Die aktualisierten Remotekomponenten sollten weiterhin mit allen früheren Versionen des SharePoint-Add-Ins verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="70aa5-110">The updated remote components should continue to work with all earlier versions of the SharePoint Add-in.</span></span>

- <span data-ttu-id="70aa5-111">Wenn Sie für Ihre Remotekomponenten ein Mandantenisolationssystem implementiert haben, beachten Sie, dass unterschiedliche Mandanten möglicherweise mehrere Versionen Ihrer App verwenden. Außerdem können auf einem bestimmten Mandanten auf verschiedenen SharePoint-Websites sogar unterschiedliche Versionen installiert sein.</span><span class="sxs-lookup"><span data-stu-id="70aa5-111">If you implemented a tenancy isolation system for your remote components, keep in mind that different tenants might be using multiple versions of your add-in, and a specific tenant might even have different versions installed on various SharePoint websites.</span></span>

<span data-ttu-id="70aa5-112">Für ein vom Anbieter gehostetes SharePoint-Add-In, das Microsoft Azure SQL-Datenbank oder SQL Server verwendet, gibt es mehrere Methoden zum Aktualisieren der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="70aa5-112">For a provider-hosted SharePoint Add-in that uses Microsoft Azure SQL Database or SQL Server, there are multiple methods for updating the database. To get started, see  Upgrade a Data-tier Application.</span></span> <span data-ttu-id="70aa5-113">Lesen Sie zum Einstieg [Upgraden einer Datenschichtanwendung](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span><span class="sxs-lookup"><span data-stu-id="70aa5-113">To get started, see [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70aa5-114">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="70aa5-114">Next steps</span></span>

<span data-ttu-id="70aa5-115">Kehren Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="70aa5-115">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>

-  [<span data-ttu-id="70aa5-116">Aktualisieren von Add-In-Webkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="70aa5-116">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
-  [<span data-ttu-id="70aa5-117">Aktualisieren von Hostwebkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="70aa5-117">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
-  [<span data-ttu-id="70aa5-118">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="70aa5-118">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)

## <a name="additional-resources"></a><span data-ttu-id="70aa5-119">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="70aa5-119">Additional resources</span></span>

-  [<span data-ttu-id="70aa5-120">Aktualisieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="70aa5-120">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
-  [<span data-ttu-id="70aa5-121">Aktualisierungsverfahren für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="70aa5-121">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process.md) 
    
 

