---
title: Suchen Sie in einer Serverfarm mit mehreren geografisch SharePoint Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 463fa7608a4e913ec2be326e9a9f9ad64f118854
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="search-in-a-multi-geo-sharepoint-tenant"></a>Suchen Sie in einer Serverfarm mit mehreren geografisch SharePoint Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

In einem Mandanten Multi-Geo SharePoint hat jeder Standort Geo eigene Suchindex als auch einen eigenen unabhängigen Suchcenter. Beim Konfigurieren eines Suchcenters verwendet standardmäßig im Suchcenter in der folgenden URL-Muster.

```
https://<tenanturl>.sharepoint.com/sites/search
```

Im Szenario mit in der folgenden Abbildung dargestellt hat ein Mandanten Multi-Geo drei Geo-Standorte mit einer geografisch standortspezifische Search-URL.

|**Geo-Speicherort**|**Search-URL**|
|:---------------|:-------------|
|Nordamerika (Standardspeicherort)|https://contoso.SharePoint.com/search|
|Europa (Satelliten Speicherort)|https://contosoeur.SharePoint.com/search|
|Asien (Satelliten Speicherort)|https://contosoapc.SharePoint.com/search|


![World Karte zur Erläuterung von Geo Speicherorte in Nordamerika und Europa Asien mit der Mandanten-spezifische Suche Website-URLs](media/multigeo/multigeosearch_intro.png)

Suche ist aus Sicht des ein Endbenutzer auf den aktuellen Speicherort des Geo beschränkt. Wenn Benutzer von einer Website gehostet in Nordamerika Suchvorgänge ausführen, sehen sie nur Ergebnisse aus dem Speicherort der Geo North America an. Suchvorgänge aus einer Website in Europa gehostet werden Ergebnisse aus Websites in Europa Geo Speicherort zurückgegeben.

> **Hinweis:** Suche wird in der Zukunft Multi-Geo bewusst sein. Eine Suchabfrage führen Sie von einer beliebigen Stelle in den Mandanten wird allen geografisch Standorten in den Mandanten suchen und kombinierten Ergebnisse zurückgibt.

## <a name="working-with-search-programmatically-in-a-multi-geo-tenant"></a>Arbeiten mit der Suche programmgesteuert in einem Multi-Geo-Mandanten
Programmgesteuertes Arbeiten mit der Suche ähnelt dem durch die Endbenutzer-Suche. Wenn Sie eine Suchabfrage ausführen, nur erhalten Ergebnisse für den Speicherort der Geo Sie in denen Sie die Abfrage ausführen. Anwendungen, jedoch mit mehreren geografisch Mandanten Suchvorgänge ausführen können. Zu diesem Zweck durchlaufen die Geo Speicherorte in Ihrem Mandanten, die gleichen Suchabfrage an jedem Standort Geo Problem, und die Ergebnisse verketten.

Dieser Ansatz möglicherweise reicht für in einigen Szenarien (beispielsweise sucht nach Websites eines bestimmten Typs). In einigen Fällen möchten Sie jedoch die Suchergebnissen in der Sortierung nach Relevanz enthalten sein. Dies ist nicht möglich, wenn Sie mehrere Resultsets haben. Wenn Ihr Szenario Suche Rangfolge erforderlich sind, müssen Sie warten, bis eine Umgebung mit mehreren geografisch verfügbar ist.


## <a name="see-also"></a>Siehe auch

- [Verwalten der Suchcenter in SharePoint Online](https://support.office.com/en-us/article/Manage-the-Search-Center-in-SharePoint-Online-174d36e0-2f85-461a-ad9a-8b3f434a4213?ui=en-US&rs=en-US&ad=US)
- [Übersicht über die Suche in SharePoint Online](https://support.office.com/en-us/article/Overview-of-search-in-SharePoint-Online-479cfd6b-900b-46aa-b497-c13787771d3f?ui=en-US&rs=en-US&ad=US)
