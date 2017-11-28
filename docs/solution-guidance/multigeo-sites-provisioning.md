---
title: Arbeiten mit Websites in einer Umgebung mit mehreren geografisch
ms.date: 11/03/2017
ms.openlocfilehash: 812c141981e383a35c10ff414dbdb4a199160d00
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/08/2017
---
# <a name="working-with-sites-in-a-multi-geo-environment"></a>Arbeiten mit Websites in einer Umgebung mit mehreren geografisch

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

SharePoint-Websites können über die standardmäßigen und Satelliten Geo Speicherorte Multi-Geo-Mandanten verteilt werden. Wenn Ihre benutzerdefinierte Entwicklung (Skript, app, Konsolenanwendung, node.js app) muss Websites bereitstellen, ist es wichtig, die geografisch Speicherorte in Ihrem Mandanten Multi-Geo beachten. 

### <a name="provisioning-classic-team-sites"></a>Bereitstellung der klassische Teamwebsites
Beim Bereitstellen von klassischen teamwebsitesammlungen (z. B. STS #0-basierte Websitesammlungen) muss eine verwendet die [CSOM `CreateSite` Methode](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) Anruf als erklärt und gezeigt in folgenden Artikeln und Beispiele:
- [Der websitebereitstellung in der SharePoint-add-in-Objektmodell](site-provisioning-sharepoint-add-in.md)
- [Bereitstellen von Websites in Batches mit dem Add-In-Modell](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [Erstellen der Websitesammlung oder Unterwebsite mithilfe der Plug & Play-Websites Core-Bibliothek](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)

Die `CreateSite` Methodenaufruf ausgeführt werden soll auf instanziierten `Tenant` ... und ein Mandant-Objekt müssen Sie Sie zum Angeben einer SPO Admin Center-URL erstellt werden soll. So gehen zum Erstellen einer Teamwebsite klassische folgendermaßen vor:
- Ermitteln Sie zunächst den Geo-Speicherort, der zum Hosten der Websitesammlung (z. B. der Europäischen Satelliten) benötigt
- Sie anhand des Leitfadens im Artikel [Multi-Geo Discovery](multigeo-discovery.md) erläutert den Mandanten Verwaltungssite und SharePoint Stamm-Url für den Speicherort der Geo suchen
- Erstellen einer `Tenant` -Objekts verwenden die gefundenen Admin-Website-Url
- Verwendung der `CreateSite` -Methodenaufrufs Inline an die Websitesammlung erstellen

Unter Beispiel zeigt, wie eine Websitesammlung in der Europäischen Geo-Speicherort bereit:

```C#
// Use the Multi-Geo discovery guidance to discover the tenant admin and root site urls for this geo location
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";
string targetUrl = "https://contoso-europe.sharepoint.com/sites/demosite";
string owner = "UserA@contoso.onmicrosoft.com";

using (var ctx = new ClientRuntimeContext(tenantAdminSiteForMyGeoLocation))
{
    ctx.Credentials = adminCredentials;
    
    var tenant = new Tenant(ctx);
    
    //Create new site
    var newsite = new SiteCreationProperties()
    {
        Url = targetUrl,
        Owner = owner,
        Template = "STS#0",
        Title = title,
        StorageMaximumLevel = 1000,
        StorageWarningLevel = 500,
        TimeZoneId = 7,
    };
    
    var spoOperation = tenant.CreateSite(newsite);
    
    ctx.Load(spoOperation);
    ctx.ExecuteQuery();
    
    while (!spoOperation.IsComplete)
    {
        Thread.Sleep(2000);
        ctx.Load(spoOperation);
        ctx.ExecuteQuery();
        Console.WriteLine("Site creation status: " + (spoOperation.IsComplete ? "waiting" : "complete"));
    }
}
```

>**Hinweis:** Wenn Sie erfahren mehr über die benötigten Berechtigungen und wie Sie Ihre Anwendung konfigurieren, und klicken Sie dann bitte Auschecken im Artikel [Einrichten der Multi-Geo Beispielanwendungen](multigeo-sampleapplicationsetup.md) möchten.

## <a name="resources"></a>Ressourcen
Unterhalb der Liste der Ressourcen sind hilfreich, wenn Sie weitere Informationen zum Arbeiten mit Websites vertraut machen:
- [Bereitstellen von modernen Teamwebsites](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-provisioning-sites)
- [Der websitebereitstellung in der SharePoint-add-in-Objektmodell](site-provisioning-sharepoint-add-in.md)
- [Bereitstellen von Websites in Batches mit dem Add-In-Modell](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [Erstellen der Websitesammlung oder Unterwebsite mithilfe der Plug & Play-Websites Core-Bibliothek](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)