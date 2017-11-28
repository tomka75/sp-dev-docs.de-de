---
title: Berechtigungsmodell in OneDrive und SharePoint Online Multi-Geo-Vorschau
ms.date: 11/03/2017
ms.openlocfilehash: 3f0d47ce0f791dd41dce8ca95e877e2e64a35c06
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="permission-model-in-onedrive-and-sharepoint-online-multi-geo-preview"></a><span data-ttu-id="793ea-102">Berechtigungsmodell in OneDrive und SharePoint Online Multi-Geo-Vorschau</span><span class="sxs-lookup"><span data-stu-id="793ea-102">Permission model in OneDrive and SharePoint Online Multi-Geo Preview</span></span>

> <span data-ttu-id="793ea-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="793ea-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="793ea-104">Das Berechtigungsmodell in einem Mandanten OneDrive und SharePoint Online mit mehreren geografisch Preview ist identisch mit der für einen einzelnen Geo-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="793ea-104">The permission model in a OneDrive and SharePoint Online Multi-Geo Preview tenant is the same as that for a single geo tenant.</span></span>

<span data-ttu-id="793ea-105">Ein Mandant Multi-Geo weist eine einzige Azure AD-Umgebung auf allen Speicherorten für alle geografisch verteilt.</span><span class="sxs-lookup"><span data-stu-id="793ea-105">A Multi-Geo tenant has a single Azure AD environment distributed across all all geo locations.</span></span> <span data-ttu-id="793ea-106">Diese Azure AD-Umgebung umfasst:</span><span class="sxs-lookup"><span data-stu-id="793ea-106">This Azure AD environment includes:</span></span> 

- <span data-ttu-id="793ea-107">Alle Benutzer und Gruppen - gelten, wenn Sie einen Benutzer oder Gruppenberechtigungen erteilen diese Berechtigungen an alle Geo-Speicherorte.</span><span class="sxs-lookup"><span data-stu-id="793ea-107">All users and groups - If you grant a user or group permissions, these permissions apply to all geo locations.</span></span>
- <span data-ttu-id="793ea-108">Alle Sicherheitsprinzipale -, ob Sie die Anwendung im Azure Active Directory mithilfe eines der Azure-Portale registrieren oder über Azure Access Control Services (in SharePoint "appregnew.aspx"), die Berechtigungen für alle Geo-Speicherorte gelten.</span><span class="sxs-lookup"><span data-stu-id="793ea-108">All security principals - Whether you register your application in Azure AD using one of the Azure Portals, or via Azure Access Control Services (appregnew.aspx in SharePoint), the permissions granted apply to all geo locations.</span></span>

<span data-ttu-id="793ea-109">Die folgende Abbildung zeigt einen Multi-Geo-Mandanten mit:</span><span class="sxs-lookup"><span data-stu-id="793ea-109">The following image shows a Multi-Geo tenant with:</span></span>

- <span data-ttu-id="793ea-110">Einen Standardspeicherort Geo in Nordamerika</span><span class="sxs-lookup"><span data-stu-id="793ea-110">A default geo location in North America</span></span>
- <span data-ttu-id="793ea-111">Einen Satelliten Geo Speicherort in Europa</span><span class="sxs-lookup"><span data-stu-id="793ea-111">A satellite geo location in Europe</span></span>
- <span data-ttu-id="793ea-112">Einen Satelliten Geo Speicherort in Asien</span><span class="sxs-lookup"><span data-stu-id="793ea-112">A satellite geo location in Asia</span></span>

<span data-ttu-id="793ea-113">Diesen Mandanten verfügt über eine verteilte Azure Active Directory (AD Azure)-Umgebung, die allen Benutzern, Gruppen und Berechtigungen enthält.</span><span class="sxs-lookup"><span data-stu-id="793ea-113">This tenant has one distributed Azure Active Directory (Azure AD) environment that includes all the users, groups, and permissions.</span></span> <span data-ttu-id="793ea-114">Die wichtigsten Azure AD-Instanz an alle Speicherorte geografisch verteilt ist.</span><span class="sxs-lookup"><span data-stu-id="793ea-114">The central Azure AD instance is distributed to all the geo locations.</span></span> 

![Eine Karte zur Erläuterung von eines Standardspeicherorts für geografisch in Nordamerika und Satelliten Geo Speicherorte in Europa und Asien, mit Benutzerkonten und Gruppen in AAD gespeichert world](media/multigeo/multigeopermissions_intro.png)

<span data-ttu-id="793ea-116">Zum Konfigurieren von Anwendungen für Multi-Geo Mandanten in Azure AD finden Sie unter [Einrichten einer Serverfarm mit mehreren geografisch beispielanwendung](multigeo-sampleapplicationsetup.md).</span><span class="sxs-lookup"><span data-stu-id="793ea-116">To configure your applications for Multi-Geo tenants in Azure AD, see [Set up a Multi-Geo sample application](multigeo-sampleapplicationsetup.md).</span></span>

