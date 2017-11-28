---
title: Inhaltstyphub in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: ecb042a4f741bd2de0698c196fcc78f3bd168567
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="content-type-hub-in-a-sharepoint-multi-geo-tenant"></a>Inhaltstyphub in einem SharePoint Multi-Geo-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Kunden verwenden Sie den Inhaltstyp-Hub von Inhaltstypen in einem zentralen Standort zu definieren, und veröffentlichen Sie die Inhaltstypen für alle Websites in einer SharePoint-Mandanten. In diesem Artikel wird erläutert, wie die inhaltstyphub in einem SharePoint Multi-Geo-Mandanten funktioniert.

Ein Mandant Multi-Geo hat eine inhaltstyphub pro Geo Speicherort. Zum Definieren von Inhaltstypen für jeden Standort Geo erstellen und Veröffentlichen von der folgenden Website.

```
https://<tenant>.sharepoint.com/sites/contenttypehub
```

Es ist jedoch ein wichtiger Unterschied zwischen dem inhaltstyphub in den Standardspeicherort Geo und Satelliten Geo Speicherorte. Wenn Sie erstellen und ein Inhaltstyps in der inhaltstyphub von den Standardspeicherort Geo veröffentlichen, sind diesen Inhaltstyp auf allen Websites in Ihrem Mandanten verfügbar. Im Beispiel in der folgenden Abbildung dargestellt sind in Nordamerika Geo am Standardspeicherort (contenttype1 und contenttype2) erstellte Inhaltstypen auf alle Websites über die Satelliten Geo Standorte für den Mandanten abgelegt. Im Inhaltstyp-Hub für den Speicherort der Europa Satelliten (contenttype3 und contenttype4) erstellte Inhaltstypen sind nur für die Websites in der Europäischen Geo Speicherort abgelegt.

![World Map anzeigt, Inhaltstypen im Standardspeicherort Geo Nordamerika für alle Websites gelten und Inhaltstypen in die Europa und Asien Satelliten Speicherorte nur für diese Geo-Standorte gelten](media/multigeo/multigeocontenttypehub_intro.png)

Die meisten Organisationen sollen konsistente Inhaltstypen über eine SharePoint-Mandanten. Es empfiehlt sich verwenden Sie die inhaltstyphub im Standardspeicherort Geo erstellen und Veröffentlichen von Inhaltstypen. Wenn Sie nicht möchten, dass alle Inhaltstypen in der standardmäßigen Geo Speicherort inhaltstyphub auf allen geografisch Speicherorten veröffentlicht werden, können Sie mithilfe der `Set-SPOTenantContentTypeReplicationParameters` PowerShell-Cmdlet zum Konfigurieren von Inhaltstypen, die Sie veröffentlichen möchten. Dieses Cmdlet ist Teil der [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/confirmation.aspx?id=35588).

Als Alternative zu einem Inhaltstyp bereit können Organisationen Inhaltstyp in ihren Lösungen für die websitebereitstellung Bereitstellung integrieren. Dies bietet mehr Flexibilität und vollständig automatisiert werden.

## <a name="see-also"></a>Siehe auch

- [Inhaltstyp-Veröffentlichung](https://support.office.com/en-US/article/Introduction-to-content-types-and-content-type-publishing-E1277A2E-A1E8-4473-9126-91A0647766E5#__toc256601764)

