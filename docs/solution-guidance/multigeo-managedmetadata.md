---
title: Verwaltete Metadaten in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: be12a7d577e0515ef17e83d7acf6b7e7f618a528
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="managed-metadata-in-a-sharepoint-multi-geo-tenant"></a>Verwaltete Metadaten in einem SharePoint Multi-Geo-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Verwaltete Metadaten in SharePoint sind Multi-Geo berücksichtigen. In diesem Artikel wird beschrieben, wie zum Verwalten von Metadaten in einem SharePoint Multi-Geo-Mandanten.

Die verwaltete Metadaten, die Sie für den Standardspeicherort Geo Multi-Geo-Mandanten, automatisch definieren repliziert auf den Mandanten Satelliten Speicherorte. Verwalteter Metadaten, den Sie für einen Satelliten Geo Standort definieren ist nur verfügbar, die Websites, die an diesem Speicherort Geo gehostet werden.

Verwalteter Metadaten, den Sie für den Standardspeicherort Geo Multi-Geo-Mandanten zu definieren, wird automatisch auf den Mandanten Satelliten Speicherorte repliziert. Verwalteter Metadaten, den die in einem Satelliten Geo Speicherort definiert, ist nur verfügbar, die an diesem Speicherort Geo gehosteten Websites.

Im Beispiel in der folgenden Abbildung dargestellt die ausdrucksgruppen TGMain1 und TGMain2 in den Standardspeicherort Geo erstellt wurden und auf alle Satelliten Geo Speicherorte repliziert werden. Daher sind diese Begriffe an allen Speicherorten im Mandanten Multi-Geo verfügbar. Synchronisierung für navigationsausdruckssatz ist unidirektional aus der Standard für die Satelliten Geo-Speicherorte. In den Standardstatus oder anderen Satelliten Geo Speicherorten Synchronisierung Ausdruckssätze an einem Speicherort Satelliten erstellt keine. Beispielsweise sein Begriff Split-Mengen erstellte TGEurope1 nur sind für Websites in Europa gehostet verfügbar.

![World Karte zur Erläuterung von Mandanten mit mehreren geografisch mit den Standardspeicherort Geo in Nordamerika und Satelliten Geo Speicherorten in Europa und Asien und ausdrucksgruppen in Satelliten Geo Speicherorte aus der Standard-Synchronisierung](media/multigeo/multigeomanagedmetadata_intro.png)

Im folgenden sind wichtige Punkte zu verwalteten Metadaten in mehreren geografisch Mandanten bekannt sein:

- Einem Standort, Satelliten Geo-Replikation aus dem Speicherort für geografisch ist **eine Möglichkeit**. Benutzer replizierten Ausdruckssätze in Satelliten Geo Speicherorte können nicht aktualisiert werden, jedoch können Administratoren. Jedoch empfohlen nicht, da es führt zusätzliche Ausdruckssätze und Ausdrücke verfügbar in diesen Satelliten Geo Speicherort würden.
- Erstellen von ausdrucksgruppen, Ausdruckssätze und Ausdrücke im Standardspeicherort Geo. Dadurch wird sichergestellt, dass sie über alle Geo-Standorte in Ihrem Mandanten ständig verfügbar sind.
- Wenn ausdrucksgruppen, Ausdruckssätze und Ausdrücke über Geo Standorte repliziert werden, behalten sie die ID an. Dadurch können Sie verweisen auf ausdrucksgruppen, Ausdruckssätze und Ausdrücke basierend auf ID, unabhängig von der Geo Position in Ihrem Code ausgeführt wird.
- Der inkrementelle Replikationsprozess wird stündlich ausgeführt. Der vollständige Replikation der Auftrag wird alle drei Tage ausgeführt.
- Wenn Sie einen Ausdruckssatz in den Standardspeicherort Geo programmgesteuert erstellen, wird dieser Ausdruckssatz automatisch repliziert. Sie müssen nicht die APIs ändern.
- In einigen Fällen sollten Sie eine Begriffsgruppe, Ausdruckssatz, oder Begriffe nur an einem Speicherort Satelliten - Beispiel verfügbar, einem Begriff, der auf einem vertraulichen Projekt bezieht, die für einen bestimmten Geo Speicherort gilt. In diesem Fall können Sie die entsprechenden Begriffe in den entsprechenden Geo-Speicherort zu erstellen. 
- Wenn Sie der Ausdruck nur in den Standardspeicherort verfügbar sein soll, verwenden Sie die `Set-SPOTenantTaxonomyReplicationParameters` PowerShell-Cmdlet, um explizit angeben, welche Begriff aus den Standardspeicherort gruppiert werden repliziert. Dieses Cmdlet ist Teil der [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/confirmation.aspx?id=35588).


## <a name="see-also"></a>Siehe auch

- [Planen von SharePoint-Taxonomie für Hybrid und Hybrid-Inhaltstypen](https://support.office.com/en-us/article/Plan-hybrid-SharePoint-taxonomy-and-hybrid-content-types-71ae4d00-da98-407b-bee2-8d9972e1875c?ui=en-US&rs=en-US&ad=US) (gilt für Multi-Geo Mandanten)
