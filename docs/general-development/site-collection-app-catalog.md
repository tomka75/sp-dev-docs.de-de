---
title: Verwenden des Websitesammlungs-App-Katalogs
ms.date: 12/14/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb1-9951-475b-b058-3285fba77b68
ms.openlocfilehash: 2a2e17f0f33bb6f801872965289663fbcca4e28e
ms.sourcegitcommit: 1845925102fabc55de2c6c60b47c20303b22b173
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="use-the-site-collection-app-catalog"></a>Verwenden des Websitesammlungs-App-Katalogs

_**Gilt für:** Office 365_

Durch Verwendung von Websitesammlungs-App-Katalogs können SharePoint-Mandantenadministratoren die Verwaltung und den Bereich der Bereitstellung von SharePoint-Add-Ins und SharePoint Framework-Lösungen auf bestimmten Websites dezentralisieren.

## <a name="why-site-collection-app-catalogs"></a>Vorteile von Websitesammlungs-App-Katalogen

Bisher mussten alle Add-Ins und SharePoint Framework-Lösungen zentral im Mandanten-App-Katalog verwaltet werden. Mandantenadministratoren konnten zwar den Zugriff für andere Personen im Unternehmen delegieren, in allen Websitesammlungen war jedoch ein bereitgestelltes Paket zu sehen. SharePoint umfasste keine unterstützte Möglichkeit zum Bereitstellen von Add-Ins und SharePoint Framework-Lösungen nur auf bestimmten Websites.

Mit der Einführung von Websitesammlungs-App-Katalogen können Mandantenadministratoren den App-Katalog auf bestimmten Websites aktivieren. Nach der Aktivierung können Websitesammlungsadministratoren SharePoint-Add-Ins und SharePoint Framework-Lösungen bereitstellen, die nur in dieser Websitesammlung verfügbar sind.

Im folgenden Schema ist die Verwendung von Websitesammlungs-App-Katalogen dargestellt:

![Diagramm, in dem das Konzept des Websitesammlungs-App-Katalogs veranschaulicht wird](../images/site-collection-app-catalog-diagram.png)

In Ihrem Office 365-Mandanten haben Sie einen Mandanten-App-Katalog. Lösungen, die in diesem App-Katalog bereitgestellt werden, können in einer beliebigen Websitesammlung im Mandanten installiert werden. Mandantenadministratoren können Websitesammlungs-App-Kataloge in bestimmten Websitesammlungen aktivieren. Lösungen, die in den Websitesammlungs-App-Katalogen bereitgestellt werden, können nur in dieser bestimmten Websitesammlung installiert werden.

## <a name="supported-capabilities"></a>Unterstützte Funktionen

### <a name="support-for-both-sharepoint-add-ins-and-sharepoint-framework-packages"></a>Unterstützung für SharePoint-Add-Ins und SharePoint Framework-Pakete

In Websitesammlungs-App-Katalogen können Sie, genau wie im Mandanten-App-Katalog, sowohl SharePoint-Add-Ins als auch SharePoint Framework-Lösungen (SSPKG) bereitstellen.

### <a name="including-assets-in-solution-packages"></a>Einschließen von Ressourcen in Lösungspakete

SharePoint Framework-Lösungspakete, die Ressourcen enthalten, können in Websitesammlungs-App-Katalogen bereitgestellt werden. Eingeschlossene Ressourcen werden in einer vorkonfigurierten Dokumentbibliothek in derselben Websitesammlung bereitgestellt, in der sich auch der Websitesammlungs-App-Katalog befindet. Wenn das öffentliche Office 365 CDN konfiguriert ist, werden Ressourcen vom CDN bedient. Andernfalls werden Ressourcen direkt von der Dokumentbibliothek bedient.

> [!NOTE]
> Derzeit wird ein Bugfix für die korrekte Unterstützung der Ressourcenverpackung in Websitesammlungs-App-Katalogen eingeführt, der vor Ablauf des Kalenerjahrs 2017 auf allen Mandanten verfügbar sein sollte.

### <a name="tenant-scoped-deployment"></a>Mandantenweite Bereitstellung

Bei der Bereitstellung von SharePoint Framework-Lösungen, die die mandantenweite Bereitstellung in einem Websitesammlungs-App-Katalog unterstützen, werden Sie gefragt, ob Sie diese Lösung auf allen Websites in der Organisation verfügbar machen möchten. Wenn Sie dieses Kontrollkästchen aktivieren, wird die Lösung trotz dieser Formulierung sofort **nur in derselben Websitesammlung verfügbar gemacht, in der sich auch der App-Katalog befindet**. Andere Websitesammlungen in Ihren Organisationen können die Lösung nicht verwenden. Wenn Sie diese Option nicht aktivieren, müssen Sie die Lösung auf Ihrer Website explizit installieren, bevor Sie diese verwenden können.

## <a name="current-limitations"></a>Aktuelle Einschränkungen

### <a name="application-lifecycle-management-alm-apis-are-not-yet-supported"></a>Application Lifecycle Management (ALM)-APIs werden noch nicht unterstützt.

Derzeit ist es nicht möglich, die vor kurzem veröffentlichten ALM-APIs für die Verwaltung des Lebenszyklus von Lösungen in Websitesammlungs-App-Katalogen zu verwenden. Daran wird derzeit gearbeitet, und dies sollte zu Beginn des Jahres 2018 verfügbar sein.

## <a name="configure-and-manage-site-collection-app-catalogs"></a>Konfigurieren und Verwalten von Websitesammlungs-App-Katalogen

Sie können Websitesammlungs-App-Kataloge mithilfe der SharePoint Online-Verwaltungsshell konfigurieren und verwalten.

> [!NOTE]
> Bevor Sie Websitesammlungs-App-Kataloge in Ihrem Mandanten verwalten können, müssen Sie sicherstellen, dass Sie die [SharePoint Online-Verwaltungshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) vom November 2017 oder eine höhere Version verwenden.

### <a name="create-a-site-collection-app-catalog"></a>Erstellen eines Websitesammlungs-App-Katalogs

> [!NOTE]
> Bevor Sie das folgende Skript ausführen, stellen Sie eine Verbindung zu Ihrem SharePoint Online-Mandanten mithilfe des `Connect-SPOService`-Cmdlets her. Stellen Sie auch sicher, dass Sie einen Mandanten-App-Katalog in Ihrem Mandanten erstellt haben. Wenn Sie dies nicht tun, schlägt das Cmdlet mit dem folgenden Fehler fehl:
> ```text
> Cannot invoke method or retrieve property from null object. Object returned by the
> following call stack is null. "TenantAppCatalog
> RootWeb
> GetSiteByUrl
> new Microsoft.Online.SharePoint.TenantAdministration.Tenant()
> "
> ```

Zum Erstellen eines Websitesammlungs-App-Katalogs verwenden Sie das `Add-SPOSiteCollectionAppCatalog`-Cmdlet, das die Websitesammlung übergibt, wobei der App-Katalog als der `-Site`-Parameter erstellt werden sollte.

```powershell
# get a reference to the site collection where the
# site collection app catalog should be created
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# create site collection app catalog
Add-SPOSiteCollectionAppCatalog -Site $site
```

Nach dem Ausführen dieses Skripts, wird die **Apps für SharePoint**-Bibliothek zu Ihrer Websitesammlung hinzugefügt, wo Sie SharePoint-Add-Ins und SharePoint Framework-Lösungen bereitstellen können.

### <a name="disable-the-site-collection-app-catalog"></a>Deaktivieren des Websitesammlungs-App-Katalogs

> [!NOTE]
> Bevor Sie das folgende Skript ausführen, stellen Sie eine Verbindung zu Ihrem SharePoint Online-Mandanten mithilfe des `Connect-SPOService`-Cmdlets her.

Zum Deaktivieren des Websitesammlungs-App-Katalogs in Ihrer Websitesammlung verwenden Sie das `Remove-SPOSiteCollectionAppCatalog`-Cmdlet, das die Websitesammlung übergibt, wobei der App-Katalog als der `-Site`-Parameter deaktiviert werden sollte. Wenn Sie über die ID Ihrer Websitesammlung verfügen, können Sie alternativ das `Remove-SPOSiteCollectionAppCatalogById`-Cmdlet verwenden.

> [!NOTE]
> Trotz des Namens entfernen die Cmdlets `Remove-SPOSiteCollectionAppCatalog` und `Remove-SPOSiteCollectionAppCatalogById` den Websitesammlungs-App-Katalog nicht aus der Websitesammlung. Sie deaktivieren diesen vielmehr, sodass Sie keine Lösungen darin bereitstellen oder darin bereitgestellte Lösungen verwenden können.

```powershell
# get a reference to the site collection in which
# the site collection app catalog should be disabled
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# disable the site collection app catalog
Remove-SPOSiteCollectionAppCatalog -Site $site
```

Nach dem Ausführen dieses Skript ist die **Apps für SharePoint**-Bibliothek immer noch in Ihrer Websitesammlung sichtbar, Sie können jedoch keine Lösungen darin bereitstellen oder darin bereitgestellte Lösungen verwenden.

## <a name="considerations"></a>Überlegungen

### <a name="governance"></a>Steuerung

Derzeit ist es nicht möglich, alle Websitesammlungen in dem Mandanten aufzuführen, die den Websitesammlungs-App-Katalog aktiviert haben.

### <a name="security"></a>Sicherheit

Vor dem Bereitstellen von Lösungen in Websitesammlungs-App-Katalogen sollten Websitesammlungsadministratoren überprüfen, dass diese Lösungen den Organisationsrichtlinien entsprechen. Lösungen, die in Websitesammlungs-App-Katalogen installiert sind, können zwar nur in diesen bestimmten Websitesammlungen verwendet werden, sie können jedoch möglicherweise auf Ressourcen von anderen Websites in dem Mandanten zugreifen, Administratoren sollten daher sicherstellen, dass die Lösungen, die sie bereitstellen, wie beabsichtigt funktionieren.

## <a name="see-also"></a>Siehe auch

- [Verwalten des Websitesammlungs-App-Katalogs]((https://support.office.com/de-DE/article/Manage-the-Site-Collection-App-Catalog-928b9b61-a9de-4563-a7d1-6231aa9d4d19))