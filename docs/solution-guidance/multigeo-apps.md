---
title: Verwalten von apps in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/08/2017
ms.openlocfilehash: c6131a1bc49f6bdcf7f4131a0699fc7d62bb8459
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/08/2017
---
# <a name="managing-apps-in-a-sharepoint-multi-geo-tenant"></a>Verwalten von apps in einem SharePoint Multi-Geo-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

In einem Mandanten Multi-Geo müssen Sie einen app-Katalog pro Geo Speicherort ist etwas Konto teilnehmen, wenn Sie Ihre apps an allen geografisch Standorten bereitstellen möchten.

## <a name="where-do-i-need-to-deploy-my-apps-in-a-multi-geo-tenant"></a>Wobei benötige ich meine apps in einer Serverfarm mit mehreren geografisch Mandanten bereitstellen?
Vor dem Bereitstellen von apps wir sprechen zunächst definiert mit apps in diesem Artikel: alle apps, die Sie bereitstellen, indem sie in Ihrem Mandanten app-Katalog hinzufügen werden im Rahmen dieses Handbuchs damit, die SharePoint Add-In (in diesem Fall App-Dateien) enthält, sondern auch Apps für SharePoint-Framework und Extensions (.sppkg-Dateien). In einer Serverfarm mit mehreren geografisch Mandanten müssen Sie eine app-Katalogwebsite pro Geo Speicherort wie unten:

![World Map mit app-Katalog in Nordamerika und Satelliten Speicherorte in Europa und Asien, mit app-Katalog](media/multigeo/multigeoapps_intro.png)

Eine Folge dieser Architektur ist, müssen Sie Ihre app in **allen** app-Kataloge bereitstellen, wenn Sie möchten Ihre app für alle Websites, unabhängig vom Standort Geo verfügbar sein soll, die in die Website gehostet wird. Beachten Sie dies Ihnen 2 zur Verfügung stehen:
- Bereitstellen von Ihrer app manuell in den einzelnen Websites der app-Katalog
- Verwenden Sie die ALM-API zum Automatisieren der bereitstellungs Ihrer Apps: Sie können diese API verwenden, die konsistent bereitgestellt und Ihre apps an allen Speicherorten die Geo Ihres Mandanten Multi-Geo Upgrades Code schreiben.


## <a name="see-also"></a>Siehe auch

- [SharePoint-Apps ALM-API]()
- [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/deploying-and-installing-sharepoint-add-ins-methods-and-options)
- [Mithilfe der clientseitigen hostingwebparts aus Office 365 CDN](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/hosting-webpart-from-office-365-cdn)
- [Host-Erweiterung von Office 365 CDN](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/hosting-extension-from-office365-cdn) 


