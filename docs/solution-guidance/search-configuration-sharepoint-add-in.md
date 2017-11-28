---
title: Konfiguration der Suche im SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 9a84ae5aa1a12322227c9182c9ff0f5fb1798e48
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="search-configuration-in-the-sharepoint-add-in-model"></a><span data-ttu-id="b4304-102">Konfiguration der Suche im SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="b4304-102">Search configuration in the SharePoint add-in model</span></span>
===================================================

<a name="summary"></a><span data-ttu-id="b4304-103">Summary</span><span class="sxs-lookup"><span data-stu-id="b4304-103">Summary</span></span>
-------

<span data-ttu-id="b4304-104">Ansatz verwenden Sie zum Konfigurieren der Suche unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="b4304-104">The approach you take to configure search is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="b4304-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario der SharePoint Server-Side Object Model zum Konfigurieren der Suche und über SharePoint-Lösungen bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="b4304-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the SharePoint Server-side Object Model was used to configure search, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="b4304-106">In einem Szenario mit SharePoint-Add-Ins Modell verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) oder REST-API zum Konfigurieren der Suche.</span><span class="sxs-lookup"><span data-stu-id="b4304-106">In an SharePoint Add-in model scenario, you use the SharePoint Client-side Object Model (CSOM) or REST API to configure search.</span></span> <span data-ttu-id="b4304-107">Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b4304-107">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="b4304-108">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="b4304-108">High-level guidelines</span></span>
---------------------

<span data-ttu-id="b4304-109">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zum Konfigurieren der Suche in das neue SharePoint-Add-in-Modell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="b4304-109">As a rule of a thumb, we would like to provide the following high-level guidelines to configure search in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="b4304-110">Verwenden Sie SharePoint-Client-Side Object Model (CSOM)-API zum Konfigurieren der Suche nach Möglichkeit durch Importieren und Exportieren der Konfiguration für die Suche.</span><span class="sxs-lookup"><span data-stu-id="b4304-110">Use the SharePoint Client-side Object Model (CSOM) API to configure search whenever possible by importing and exporting search configuration settings.</span></span>
- <span data-ttu-id="b4304-111">Nicht alle suchkonfigurationseinstellungen stehen derzeit über die SharePoint-CSOM-API.</span><span class="sxs-lookup"><span data-stu-id="b4304-111">Not all search configuration settings are currently available via the SharePoint CSOM API.</span></span>
    + <span data-ttu-id="b4304-112">Finden Sie unter den [Export und Import suchkonfigurationseinstellungen in SharePoint Server 2013 (TechNet-Artikel)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) eine Liste der suchkonfigurationseinstellungen, die exportiert und importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="b4304-112">See the [Export and import customized search configuration settings in SharePoint Server 2013 (TechNet Article)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) for a list of search configuration settings that can be exported and imported.</span></span>
    + <span data-ttu-id="b4304-113">Wenn ein suchkonfigurationseinstellung nicht mit dem Clientobjektmodell festgelegt werden kann ist die Benutzeroberfläche für die Verwaltung So legen Sie Konfigurationswerte erforderlich.</span><span class="sxs-lookup"><span data-stu-id="b4304-113">If a search configuration setting is not able to be set using the CSOM then the Administration user interface is required to set configuration values.</span></span>
- <span data-ttu-id="b4304-114">Die SharePoint-REST-API kann keinen (zu diesem Zeitpunkt) importieren oder Exportieren von suchkonfigurationseinstellungen.</span><span class="sxs-lookup"><span data-stu-id="b4304-114">The SharePoint REST API is not capable (at this time) of importing or exporting search configuration settings.</span></span>

<span data-ttu-id="b4304-115">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="b4304-115">**Getting started**</span></span>

<span data-ttu-id="b4304-116">Im folgende Beispiel wird gezeigt, wie zum Importieren und Exportieren von Einstellungen für Suchfeld zwischen SharePoint-Mandanten, Websitesammlungen und Websites.</span><span class="sxs-lookup"><span data-stu-id="b4304-116">The following sample demonstrates how to import and export search settings between SharePoint tenants, site collections and sites.</span></span>

- [<span data-ttu-id="b4304-117">Core.SearchSettingsPortability (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="b4304-117">Core.SearchSettingsPortability (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)

<a name="related-links"></a><span data-ttu-id="b4304-118">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="b4304-118">Related links</span></span>
=============

- <span data-ttu-id="b4304-119">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="b4304-119">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="b4304-120">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="b4304-120">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="b4304-121">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="b4304-121">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="b4304-122">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="b4304-122">Related PnP samples</span></span>
===================

- [<span data-ttu-id="b4304-123">Core.SearchSettingsPortability (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="b4304-123">Core.SearchSettingsPortability (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)
- <span data-ttu-id="b4304-124">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="b4304-124">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="b4304-125">Gilt für</span><span class="sxs-lookup"><span data-stu-id="b4304-125">Applies to</span></span>
==========
- <span data-ttu-id="b4304-126">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="b4304-126">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="b4304-127">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="b4304-127">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="b4304-128">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="b4304-128">SharePoint 2013 on-premises</span></span>
