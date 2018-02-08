---
title: "Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins"
description: "Hier erfahren Sie, wie Sie auf einer SharePoint Online-Website oder in einer lokalen Farm eine Entwicklungsumgebung für SharePoint-Add-Ins erstellen können."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 62690d8c3e0949129dd09b57e772911333aa99fd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a><span data-ttu-id="ebc37-103">Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ebc37-103">Tools and environments for developing SharePoint Add-ins</span></span>

<span data-ttu-id="ebc37-104">Es gibt zwei grundlegende Muster für Entwicklungsumgebungen für SharePoint-Add-Ins. Die SharePoint-Website für Tests und Debugging kann gehostet werden:</span><span class="sxs-lookup"><span data-stu-id="ebc37-104">There are two basic patterns for development environments for SharePoint Add-ins. The test and debugging SharePoint website can be on:</span></span>

-  <span data-ttu-id="ebc37-105">**Auf einer SharePoint Online-Website in einem Office 365-Abonnement:**</span><span class="sxs-lookup"><span data-stu-id="ebc37-105">**A SharePoint Online website in an Office 365 subscription.**</span></span> <span data-ttu-id="ebc37-106">In der Regel wird Visual Studio auf einem lokalen Computer installiert. Eine cloudbasierte Visual Studio-Instanz ist aber ebenfalls eine Option.</span><span class="sxs-lookup"><span data-stu-id="ebc37-106">Typically, Visual Studio is installed to a local computer, but a cloud-based Visual Studio is also an option.</span></span>

-  <span data-ttu-id="ebc37-107">**In einer lokalen SharePoint-Farm mit einem einzigen Server:**</span><span class="sxs-lookup"><span data-stu-id="ebc37-107">**An on-premises, one-server SharePoint farm.**</span></span> <span data-ttu-id="ebc37-108">Visual Studio wird auf demselben Computer installiert.</span><span class="sxs-lookup"><span data-stu-id="ebc37-108">Visual Studio is installed on the same computer.</span></span>
 
<span data-ttu-id="ebc37-109">Dabei ist Folgendes zu berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="ebc37-109">Consider the following:</span></span>

- <span data-ttu-id="ebc37-110">Fast alle Add-Ins, die Sie erstellen, können sowohl in SharePoint Online als auch in einer lokalen SharePoint-Farm bereitgestellt werden, unabhängig von der verwendeten Umgebung.</span><span class="sxs-lookup"><span data-stu-id="ebc37-110">Almost any add-in that you create can be deployed to either SharePoint Online or to on-premises SharePoint farms, regardless of which type of environment you use.</span></span> <span data-ttu-id="ebc37-111">Allgemein gilt: Add-Ins, die nicht in SharePoint Online bereitgestellt werden können, können auch nicht mit SharePoint Online entwickelt werden. Das sind beispielsweise Add-Ins, die die [Berechtigung „Vollzugriff“](add-in-permissions-in-sharepoint.md) benötigen, sowie Add-Ins, die das [besonders vertrauenswürdige Autorisierungssystem](creating-sharepoint-add-ins-that-use-high-trust-authorization.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="ebc37-111">As a general rule, add-ins that cannot be deployed to SharePoint Online also cannot be developed with it; for example: add-ins that require [Full Control permissions](add-in-permissions-in-sharepoint.md) and add-ins that use the [high-trust authorization system](creating-sharepoint-add-ins-that-use-high-trust-authorization.md).</span></span>

- <span data-ttu-id="ebc37-112">Sie können mit jeder Umgebung sowohl SharePoint-gehostete SharePoint-Add-Ins als auch anbietergehostete SharePoint-Add-Ins entwickeln.</span><span class="sxs-lookup"><span data-stu-id="ebc37-112">You can develop both SharePoint-hosted and provider-hosted SharePoint Add-ins, regardless of which type of environment you use.</span></span>

- <span data-ttu-id="ebc37-113">Sie können sowohl mit lokalen Testwebsites als auch mit SharePoint Online-Testwebsites arbeiten.</span><span class="sxs-lookup"><span data-stu-id="ebc37-113">You can have both on-premises and SharePoint Online test sites.</span></span>

- <span data-ttu-id="ebc37-114">Insgesamt sind beide Optionen gleich unkompliziert in der Einrichtung.</span><span class="sxs-lookup"><span data-stu-id="ebc37-114">All things considered, the two options are equally easy to set up.</span></span>
    
<span data-ttu-id="ebc37-115">Die **Erstellung einer SharePoint Online-Umgebung** mithilfe eines SharePoint Online-Abonnements für die Entwicklung wird im Artikel [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="ebc37-115">**To create the SharePoint Online environment** by using a SharePoint Online subscription that you can use for development, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
 
<span data-ttu-id="ebc37-116">Eine Anleitung zur **Erstellung einer lokalen Umgebung** finden Sie im Artikel [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="ebc37-116">**To create the on-premises environment**, see [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).</span></span>
 
> [!NOTE]
> <span data-ttu-id="ebc37-117">In diesem Artikel geht es ausschließlich um Umgebungen für die Entwicklung von SharePoint-Add-Ins. Wenn Sie Farmlösungen entwickeln möchten, finden Sie entsprechende Informationen im Artikel [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebc37-117">This topic is only concerned with environments for developing SharePoint Add-ins. If you plan to develop farm solutions, see [Set up a general development environment for SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx).</span></span> 

> <span data-ttu-id="ebc37-118">Wenn Sie Entwicklungsprojekte beider Typen umsetzen möchten, sollten Sie mit letzterem Artikel beginnen und anschließend den Artikel [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md) lesen. Dort finden Sie weitere erforderliche Schritte für die Entwicklung von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="ebc37-118">If you plan to do both kinds of development, start with the latter article, and then see [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md) for additional steps you need to develop SharePoint Add-ins.</span></span>


## <a name="see-also"></a><span data-ttu-id="ebc37-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ebc37-119">See also</span></span>
<span data-ttu-id="ebc37-120"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ebc37-120"><a name="bk_addresources"> </a></span></span>

- [<span data-ttu-id="ebc37-121">SharePoint Add-ins</span><span class="sxs-lookup"><span data-stu-id="ebc37-121">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
- [<span data-ttu-id="ebc37-122">Erstellen von SharePoint-Add-Ins in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebc37-122">Create SharePoint Add-ins in Visual Studio</span></span>](create-sharepoint-add-ins-in-visual-studio.md)
    
 

