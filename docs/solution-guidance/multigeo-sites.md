---
title: Arbeiten Sie mit Websites in einer Umgebung mit mehreren geografisch
ms.date: 11/03/2017
ms.openlocfilehash: cd7b3889a7299916d96e4e80bb65126c41733494
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="work-with-sites-in-a-multi-geo-environment"></a>Arbeiten Sie mit Websites in einer Umgebung mit mehreren geografisch

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

SharePoint-Websites umfassen die standardmäßige und Satelliten Geo Speicherorte Multi-Geo-Mandanten. Wenn Ihre benutzerdefinierte Lösung muss arbeiten mit SharePoint-Websites und bei der Bereitstellung von Anwendungen, ist es wichtig, die geografisch Speicherorte in Ihrem Mandanten Multi-Geo beachten. 

## <a name="deploying-applications-to-multi-geo-sharepoint-tenants"></a>Bereitstellen von Anwendungen für SharePoint Multi-Geo Mandanten
Wenn Sie Anwendungen wie SharePoint-Add-ins oder SharePoint mithilfe der clientseitigen Webparts basierend auf der SharePoint-Framework bereitstellen müssen Sie im Konto berücksichtigen, dass Anwendungen auf Standortebene Geo bereitgestellt werden. Wenn Sie eine Anwendung im Standardverzeichnis Geo bereitstellen, wird dieser Anwendung in die Satelliten Geo Speicherorte nicht verfügbar. Weitere Informationen zu app-Bereitstellung finden Sie unter [Verwalten von Apps /-Add-ins in einem Multi-Geo-Mandanten](multigeo-apps.md) .

Es wird empfohlen, die Sie bereitstellen und aktualisieren Ihre unternehmensanwendungen an allen Speicherorten. Dadurch wird sichergestellt, dass die Anwendung für alle Benutzer verfügbar ist.

## <a name="enumerating-site-collections"></a>Aufzählen von Websitesammlungen
Um alle Mandanten Websitesammlungen aufgelistet werden, verwenden Sie die [CSOM-GetSitePropertiesFromSharePointByFilters-Methode](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.getsitepropertiesfromsharepointbyfilters.aspx) für ein `Tenant` -Objektinstanz. Da jeder Geo-Speicherort ein Mandanten Administrationscenter hat, müssen Sie zum Auflisten von Websitesammlungen pro Geo Speicherort und Verketten der Ergebnisse, um eine einzelne Mandanten gesamte Liste von Websitesammlungen zu erhalten.

Eine Enumeration Mandanten gesamte Website ausführen:

- [Alle Geo-Speicherorte suchen](multigeo-discovery.md) und deren zugeordneten mandantenadministrator site-URLs.
- Erstellen Sie eine Schleife, die die Speicherorte der Geo durchläuft und erstellt eine `Tenant` -Objekt mit den Geo Speicherort Admin-Website-URL.
    - Verwendung der `GetSitePropertiesFromSharePointByFilters` Methodenaufruf für die `Tenant` Websitesammlungen für diesen Speicherort Geo abzurufenden Objekts.
    - Fügen Sie die Websitesammlungen zu einer Liste an.
- Zurückgeben der Liste der Websitesammlungen.

Finden Sie weitere Informationen finden Sie [MultiGeo.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.SiteEnumeration) .

> [!NOTE] 
> Weitere Informationen zu Berechtigungen und wie Sie die Anwendung konfigurieren finden Sie unter [Einrichten einer Serverfarm mit mehreren geografisch beispielanwendung](multigeo-sampleapplicationsetup.md).

## <a name="performing-tenant-level-operations"></a>Ausführen von Vorgängen auf Mandantenebene
Die `Tenant` Objekt wird auch verwendet, um auf Mandantenebene Einstellungen konfigurieren, wie CDN-Einstellungen und websiteeinstellungen auf Mandantenebene wie die **Website Geo Speicherort Einschränkung**. Um auf Mandantenebene-Vorgänge auszuführen:

- [Alle Geo-Speicherorte suchen](multigeo-discovery.md) und deren zugeordneten mandantenadministrator site-URLs.
- Um Einstellungen auf Mandantenebene zu aktualisieren, die Speicherorte der Geo durchlaufen Sie, und stellen Sie die Änderung pro Geo Speicherort.
- So aktualisieren Sie die Einstellungen auf Mandantenebene-Website: 
    - Verwendung der `GeoLocation` -Eigenschaft des der `Site` abzurufenden den Standort Geo-Objekts 
    - Verwendung der `GetSitePropertiesByUrl` Mandanten für die Website sowie ändern und Anruf Abrufmethode `Update` auf die abgerufenen `SiteProperties` Objekt.

Ausführliche Informationen zum Abrufen einer Website mithilfe von der `GetSitePropertiesByUrl` Methode und beschränken Sie die Website verschoben wird, durch Festlegen der `RestrictedToRegion` -Eigenschaft, finden Sie im Beispiel [MultiGeo.RestrictSiteToGeoLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.RestrictSiteToGeoLocation) . 

## <a name="are-site-urls-a-good-way-to-identify-sites"></a>Sind Sie Website-URLs eine empfehlenswerte Methode zum Identifizieren der Websites?
In einer Serverfarm mit mehreren geografisch Mandanten können Websites zwischen den Geo-Standorten die, die mit einschließt, die die URL dieser Website geändert wird, also speichern die Website-URL als eindeutiger Schlüssel zum Identifizieren eines Standorts wird nicht empfohlen, verschoben werden. Es ist besser zum Speichern von Website-ID, die gleich, unabhängig davon, bleibt, an welche Stelle Geo die Website gehostet wird. 


## <a name="see-also"></a>Siehe auch
- [Verwalten von Apps/Add-ins in einer Serverfarm mit mehreren geografisch Mandanten](multigeo-apps.md)

