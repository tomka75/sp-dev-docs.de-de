---
title: Zum Bereitstellen von Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 48104bb22245a27be487685f8f668b0de2c559b5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
<a name="how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online"></a><span data-ttu-id="e1001-102">Zum Bereitstellen von Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e1001-102">How to provide add-in app only tenant administrative permissions in SharePoint Online</span></span>
================================================

<span data-ttu-id="e1001-103">Wenn Sie SharePoint-Add-ins entwickeln und diese mit ACS-Modell ("appregnew.aspx" und "appinv.aspx") erfassen möchten, müssen Sie einen speziellen Prozess, folgen, wenn ein Add-in Mandanten Administratorberechtigungen aufgefordert wird und in nur-app-Modus.</span><span class="sxs-lookup"><span data-stu-id="e1001-103">When you are developing SharePoint add-ins and want to register them using the ACS model (appregnew.aspx and appinv.aspx), you will need to follow a special process, when an add-in is requesting tenant admin permissions and in app-only mode.</span></span> 

<span data-ttu-id="e1001-104">Schritte zum Mandanten Administratorberechtigung für die app nur-add-in bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="e1001-104">Steps to provide tenant admin permission for app only add-in:</span></span>

- <span data-ttu-id="e1001-105">Registrieren von app-Id für das Add-in unter normalen Websitesammlung im Mandanten-Add-in dem bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="e1001-105">Register app id for the add-in under normal site collection in the tenant where add-in will be deployed.</span></span> 
  - <span data-ttu-id="e1001-106">URL: *https://[tenant].sharepoint.com/_layouts/15/appregnew.aspx*</span><span class="sxs-lookup"><span data-stu-id="e1001-106">URL: *https://[tenant].sharepoint.com/_layouts/15/appregnew.aspx*</span></span>
- <span data-ttu-id="e1001-107">Geben Sie die erforderliche Informationen für die Registrierung-Add-in und registrieren Sie-ID und geheimen Schlüssel für das Add-in</span><span class="sxs-lookup"><span data-stu-id="e1001-107">Provide necessary details for the add-in registration and register ID and secret for your add-in</span></span>
- <span data-ttu-id="e1001-108">Wechseln Sie zur Seite "appinv.aspx", unter Ihrer Mandanten Admin-Website</span><span class="sxs-lookup"><span data-stu-id="e1001-108">Move to appinv.aspx page under your tenant admin site</span></span>
  - <span data-ttu-id="e1001-109">URL: *https://[tenant]-admin.sharepoint.com/_layouts/15/appinv.aspx*</span><span class="sxs-lookup"><span data-stu-id="e1001-109">URL: *https://[tenant]-admin.sharepoint.com/_layouts/15/appinv.aspx*</span></span>
- <span data-ttu-id="e1001-110">Führen Sie eine Suche für die app-Id in der vorherigen Schritte auf der Seite "appinv.aspx" registriert</span><span class="sxs-lookup"><span data-stu-id="e1001-110">Perform a lookup for the app id registered in previous steps in appinv.aspx page</span></span>
- <span data-ttu-id="e1001-111">Bereitstellen der erforderliche Berechtigungen für Ihre Add-in-Registrierung</span><span class="sxs-lookup"><span data-stu-id="e1001-111">Provide needed permissions for your add-in registration</span></span>
- <span data-ttu-id="e1001-112">Führen Sie die Vertrauensstellung für die aktualisierte-add-in-Registrierung</span><span class="sxs-lookup"><span data-stu-id="e1001-112">Perform trust for the updated add-in registration</span></span>

<span data-ttu-id="e1001-113">Beachten Sie, dass diese Operation hat, unter die Mandantenverwaltungs-Website ausgeführt werden und für diese Vorgänge verwendete Konto Mandanten Administratorberechtigungen verfügen müssen.</span><span class="sxs-lookup"><span data-stu-id="e1001-113">Notice that this operation has to be completed under the tenant administration site and account used for these operations will need to have tenant administrative permissions.</span></span> <span data-ttu-id="e1001-114">Wenn Sie niedriger Berechtigungsstufe für das add-in bereitstellen, können Sie die unter normalen Websitesammlungs-URLs mit niedrigeren Berechtigungen abschließen.</span><span class="sxs-lookup"><span data-stu-id="e1001-114">If you are providing lower level permissions for your add-in, you can complete those under normal site collection URLs with lower permissions.</span></span> 


## <a name="see-also"></a><span data-ttu-id="e1001-115">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e1001-115">See also</span></span>
<span data-ttu-id="e1001-116"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e1001-116"></span></span>

- [<span data-ttu-id="e1001-117">Registrieren von SharePoint-Add-Ins 2013</span><span class="sxs-lookup"><span data-stu-id="e1001-117">Register SharePoint Add-ins 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/jj687469.aspx)
    
- [<span data-ttu-id="e1001-118">Add-in-Berechtigungen in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="e1001-118">Add-in permissions in SharePoint 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)

