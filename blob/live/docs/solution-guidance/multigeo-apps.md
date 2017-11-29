---
title: Verwalten von apps in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/08/2017
ms.openlocfilehash: c6131a1bc49f6bdcf7f4131a0699fc7d62bb8459
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/08/2017
---
# <a name="managing-apps-in-a-sharepoint-multi-geo-tenant"></a><span data-ttu-id="42a4d-102">Verwalten von apps in einem SharePoint Multi-Geo-Mandanten</span><span class="sxs-lookup"><span data-stu-id="42a4d-102">Managing apps in a SharePoint Multi-Geo tenant</span></span>

> <span data-ttu-id="42a4d-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="42a4d-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="42a4d-104">In einem Mandanten Multi-Geo müssen Sie einen app-Katalog pro Geo Speicherort ist etwas Konto teilnehmen, wenn Sie Ihre apps an allen geografisch Standorten bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="42a4d-104">In a Multi-Geo tenant, you'll have an app catalog per geo location which is something to take in account if you want to deploy your apps across all geo locations.</span></span>

## <a name="where-do-i-need-to-deploy-my-apps-in-a-multi-geo-tenant"></a><span data-ttu-id="42a4d-105">Wobei benötige ich meine apps in einer Serverfarm mit mehreren geografisch Mandanten bereitstellen?</span><span class="sxs-lookup"><span data-stu-id="42a4d-105">Where do I need to deploy my apps in a Multi-Geo tenant?</span></span>
<span data-ttu-id="42a4d-106">Vor dem Bereitstellen von apps wir sprechen zunächst definiert mit apps in diesem Artikel: alle apps, die Sie bereitstellen, indem sie in Ihrem Mandanten app-Katalog hinzufügen werden im Rahmen dieses Handbuchs damit, die SharePoint Add-In (in diesem Fall App-Dateien) enthält, sondern auch Apps für SharePoint-Framework und Extensions (.sppkg-Dateien).</span><span class="sxs-lookup"><span data-stu-id="42a4d-106">Before talking about deploying apps let's first define what's meant with apps in this article: all apps that you deploy by first adding them to your tenant app catalog are in scope of this guidance, so that includes SharePoint Add-In's (so .app files) but also SharePoint Framework Apps and Extensions (the .sppkg files).</span></span> <span data-ttu-id="42a4d-107">In einer Serverfarm mit mehreren geografisch Mandanten müssen Sie eine app-Katalogwebsite pro Geo Speicherort wie unten:</span><span class="sxs-lookup"><span data-stu-id="42a4d-107">In a Multi-Geo tenant you'll have one app catalog site per geo location as show below:</span></span>

![World Map mit app-Katalog in Nordamerika und Satelliten Speicherorte in Europa und Asien, mit app-Katalog](media/multigeo/multigeoapps_intro.png)

<span data-ttu-id="42a4d-109">Eine Folge dieser Architektur ist, müssen Sie Ihre app in **allen** app-Kataloge bereitstellen, wenn Sie möchten Ihre app für alle Websites, unabhängig vom Standort Geo verfügbar sein soll, die in die Website gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="42a4d-109">A consequence of this architecture is that you'll need to deploy your app in **all** app catalogs if you want your app to be available for all sites, regardless of the geo location the site is hosted in.</span></span> <span data-ttu-id="42a4d-110">Beachten Sie dies Ihnen 2 zur Verfügung stehen:</span><span class="sxs-lookup"><span data-stu-id="42a4d-110">To realize this you have 2 options:</span></span>
- <span data-ttu-id="42a4d-111">Bereitstellen von Ihrer app manuell in den einzelnen Websites der app-Katalog</span><span class="sxs-lookup"><span data-stu-id="42a4d-111">Deploy your app manually in each of the app catalog sites</span></span>
- <span data-ttu-id="42a4d-112">Verwenden Sie die ALM-API zum Automatisieren der bereitstellungs Ihrer Apps: Sie können diese API verwenden, die konsistent bereitgestellt und Ihre apps an allen Speicherorten die Geo Ihres Mandanten Multi-Geo Upgrades Code schreiben.</span><span class="sxs-lookup"><span data-stu-id="42a4d-112">Use the ALM API's to automate the deployment of your apps: using these API's you can write code that consistently deploys/upgrades your apps in all the geo locations of your Multi-Geo tenant.</span></span>


## <a name="see-also"></a><span data-ttu-id="42a4d-113">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="42a4d-113">See also</span></span>

- [<span data-ttu-id="42a4d-114">SharePoint-Apps ALM-API</span><span class="sxs-lookup"><span data-stu-id="42a4d-114">SharePoint Apps ALM API's</span></span>]()
- [<span data-ttu-id="42a4d-115">Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen</span><span class="sxs-lookup"><span data-stu-id="42a4d-115">Deploying and installing SharePoint Add-ins: methods and options</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/deploying-and-installing-sharepoint-add-ins-methods-and-options)
- [<span data-ttu-id="42a4d-116">Mithilfe der clientseitigen hostingwebparts aus Office 365 CDN</span><span class="sxs-lookup"><span data-stu-id="42a4d-116">Hosting client-side web part from Office 365 CDN</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/hosting-webpart-from-office-365-cdn)
- [<span data-ttu-id="42a4d-117">Host-Erweiterung von Office 365 CDN</span><span class="sxs-lookup"><span data-stu-id="42a4d-117">Host extension from Office 365 CDN</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/hosting-extension-from-office365-cdn) 


