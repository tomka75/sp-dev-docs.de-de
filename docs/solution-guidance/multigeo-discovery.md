---
title: "Entdecken Sie eine Multi-Geo-Konfiguration für einen SharePoint-Mandanten"
ms.date: 11/03/2017
ms.openlocfilehash: f33e63a49dd8ec52b5ba6cb83874bbdafb916b8d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="discover-a-multi-geo-configuration-for-a-sharepoint-tenant"></a>Entdecken Sie eine Multi-Geo-Konfiguration für einen SharePoint-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Bei der Arbeit mit einer SharePoint-Mandanten, müssen Sie erkennen können, ob es sich um einen Mandanten Multi-Geo ist, und identifizieren Sie die standardmäßige und Satelliten Geo-Speicherorte. 

Die folgende Abbildung zeigt einen Multi-Geo-Mandanten mit:

- Einen Standardspeicherort Geo in Nordamerika
- Einen Satelliten Geo Speicherort in Europa
- Einen Satelliten Geo Speicherort in Asien

![Ein World Karte zur Erläuterung von einen Standardspeicherort Geo in Nordamerika und Satelliten Geo Speicherorte in Europa und Asien, mit sprachspezifischen mandantenadministrator, Stamm und Meine Website-URLs](media/multigeo/multigeodiscovery_intro.png)

Je nach Szenario können eine oder eine Kombination der folgenden APIs Sie eine Serverfarm mit mehreren geografisch Mandanten-Website zugreifen:

- **Die Microsoft Graph-API** - Multi-Geo berücksichtigen. Es wird empfohlen, dass Sie Microsoft Graph auf Access Multi-Geo Mandanten Websites verwenden. 
- **SharePoint-CSOM-API** - nicht Multi-Geo berücksichtigen. Je nach Szenario müssen Sie die richtige Geo Zielspeicherort (beispielsweise, um ein Benutzerprofil zugreifen oder Mandanten API Vorgänge ausführen).
- **SharePoint-REST-API** - normalerweise diese API ist im Kontext einer Website-URL verwendet und, ob der Mandant Multi-Geo ist also kein Faktor. Einige Szenarien REST-API (wie Suche oder User Profile) erfordern möglicherweise Anrufe pro Standort Geo tätigen.

## <a name="get-multi-geo-tenant-configuration-information"></a>Abrufen von Multi-Geo Mandanten Konfigurationsinformationen

Sie können die Geo Standortinformationen für einen Mandanten mithilfe von Microsoft Graph abrufen. Im folgenden Beispiel wird eine Auflistung mit einem Objekt pro Geo-Standort zurückgegeben.

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

Beispielantwort für einen Mandanten Multi-Geo:
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://contoso.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"NAM",
                "hostname": "contoso.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoeur.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"EUR",
                "hostname": "contosoeur.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoapc.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"APC",
                "hostname": "contosoapc.sharepoint.com"
            }
        }
    ]
}
```

Finden Sie weitere Informationen finden Sie [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) .

>**Hinweis:** Weitere Informationen zu Berechtigungen und wie Sie die Anwendung konfigurieren finden Sie unter [Einrichten einer Serverfarm mit mehreren geografisch beispielanwendung](multigeo-sampleapplicationsetup.md).

## <a name="discover-whether-your-tenant-is-multi-geo"></a>Ermitteln Sie, ob es sich bei Ihrem Mandanten Multi-Geo ist 

Microsoft Graph können Sie ermitteln, ob ein Mandant Multi-Geo ist, da Anforderungen über Microsoft Graph an mehreren geografisch Mandanten Weitere klicken Sie dann ein Element in der Auflistung zurück. Das folgende Beispiel zeigt die Ergebnisse eines Microsoft Graph-Anrufs auf einen einzelnen Geo-Mandanten.

<!-- Not sure where the output for a Multi-Geo tenant is. Provide a link? -->

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

Beispielantwort für einen einzelnen Geo-Mandanten:
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://singlegeotest.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"",
                "hostname": "singlegeotest.sharepoint.com"
            }
        }
    ]
}
```

## <a name="see-also"></a>Siehe auch

- [Developercenter für Microsoft Graph](https://developer.microsoft.com/en-us/graph)
- [Microsoft Graph-Dokumentation](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [Diagramm-Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
