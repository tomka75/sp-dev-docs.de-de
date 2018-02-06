---
title: Application Lifecycle Management (ALM)-APIs
ms.date: 12/19/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: 59d930854720f75879d38449d93811bfd80e1cc7
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="application-lifecycle-management-alm-apis"></a>Application Lifecycle Management (ALM)-APIs  

ALM-APIs bieten einfache APIs für die Verwaltung der Bereitstellung Ihrer SharePoint-Framework-Lösungen und Add-Ins Ihres Mandanten. ALM-APIs unterstützen die folgenden Funktionen.

- Hinzufügen einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins zu einem Mandanten-App-Katalog
- Aktivieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, damit diese für die Installation in einem Mandanten-App-Katalog verfügbar sind
- Deaktivieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, damit diese nicht für die Installation in einem Mandanten-App-Katalog verfügbar sind
- Installieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins aus einem Mandanten-App-Katalog in eine Seite
- Aktualisieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, wenn eine neuere Version im Mandanten-App-Katalog enthalten ist
- Deinstallieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins von einer Seite

ALM-APIs können verwendet werden, um genau die gleichen Operationen durchzuführen, die über die Benutzeroberfläche verfügbar sind. Wenn diese APIs verwendet werden, können alle typischen Aktionen ausgeführt werden. Nachfolgend finden Sie einige der Eigenschaften für ALM-APIs.

- Installieren und Deinstallieren von Ereignissen werden für vom Anbieter gehostete Add-Ins ausgelöst, wenn entsprechende Vorgänge aufgetreten sind
- ALM-APIs unterstützen Nur-App-basierte Vorgänge

ALM-APIs werden systemeigen über REST-APIs bereitgestellt, aber es gibt auch zusätzliche CSOM-Erweiterungen und PowerShell-Commandlets über SharePoint Patterns and Practices.

> [!NOTE] 
> ALM-APIs werden derzeit für [Websitesammlungs-App-Katalog](../general-development/site-collection-app-catalog.md) nicht unterstützt. Die Unterstützung wird Anfang 2018 hinzugefügt.

## <a name="rest-api"></a>REST-API

### <a name="add-solution-package-to-tenant-app-catalog"></a>Hinzufügen eines Lösungspakets zum Mandanten-App-Katalog 

Fügen Sie eine Lösung zum Mandanten-App-Katalog hinzu. Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.

```
url: /_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-package-in-tenant-app-catalog"></a>Bereitstellen eines Lösungspakets im Mandanten-App-Katalog

Aktivieren Sie die Lösung, damit Sie für die Installation in eine bestimmte Website zur Verfügung steht. Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy
```

> [!NOTE]
> Dieser Vorgang muss nach dem Hinzufügen abgeschlossen werden, damit Sie Pakete in bestimmte Websites integrieren können. 

### <a name="retract-solution-package-in-the-tenant-app-catalog"></a>Zurückziehen eines Lösungspakets in den Mandanten-App-Katalog

Ziehen Sie Lösungen zurück, sodass diese nicht mehr auf Websites zur Verfügung stehen. Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract
```

> [!NOTE]
> Wenn Sie diesen Vorgang nach der Installation von Lösungen in Websites durchführen, funktionieren diese nicht mehr, da die Lösung auf Mandantenebene deaktiviert wurde.

### <a name="remove-solution-package-from-tenant-app-catalog"></a>Entfernen eines Lösungspakets aus dem Mandanten-App-Katalog

Entfernen Sie das Lösungspaket aus dem Mandanten-App-Katalog. Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove
```

> [!NOTE]
> Die Lösung wird ebenfalls automatisch zurückgezogen, wenn dieser Vorgang nicht vor dem Entfernen ausgeführt wurde.

### <a name="list-available-packages-from-tenant-app-catalog"></a>Auflisten verfügbarer Pakete aus dem Mandanten-App-Katalog

Rufen Sie mit der REST-API eine Liste der verfügbaren SharePoint-Framework-Lösungen oder -Add-Ins im Mandanten-App-Katalog ab.

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-on-individual-solution-package-from-tenant-app-catalog"></a>Einzelheiten zu einzelnen Lösungspaketen aus dem Mandanten-App-Katalog

Rufen Sie mit der REST-API Einzelheiten zu einzelnen SharePoint-Framework-Lösungen oder -Add-Ins im Mandanten-App-Katalog ab.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-tenant-app-catalog-to-sharepoint-site"></a>Integrieren eines Lösungspakets aus dem Mandanten-App-Katalog in eine SharePoint-Website

Integrieren Sie ein Lösungspaket mit bestimmten Bezeichnern aus einem Mandanten-App-Katalog in eine auf URL-Kontext basierende Website. Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Installationsvorgang ausgeführt werden soll.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install
method: POST
```

### <a name="upgrade-solution-package-in-sharepoint-site"></a>Aktualisieren eines Lösungspakets einer SharePoint-Website

Aktualisieren Sie ein Lösungspaket der Seite auf eine neuere, im Mandanten-App-Katalog verfügbare Version. Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Aktualisierungsvorgang ausgeführt werden soll.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade
method: POST
```

### <a name="uninstall-solution-package-from-sharepoint-site"></a>Deinstallieren eines Lösungspakets von einer SharePoint-Website

Deinstallieren Sie ein Lösungspaket von einer SharePoint-Website. Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Deinstallationsvorgang ausgeführt werden soll.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall
method: POST
```
> [!NOTE]
> Wenn Sie die REST-API verwenden, um ein Lösungspaket von der Website zu deinstallieren, wird es nicht in den Papierkorb verschoben.


## <a name="sharepoint-pnp-powershell-cmdlets-to-programmatically-add-and-deploy-sharepoint-apps"></a>SharePoint PnP PowerShell-Cmdlets zum programmgesteuerten Hinzufügen und Bereitstellen von SharePoint-Apps

Mit [PnP PowerShell](https://msdn.microsoft.com/de-DE/pnp_powershell/pnp-powershell-overview) können Sie die Bereitstellung, Veröffentlichung, Installation, Aktualisierung und das Zurückziehen Ihrer Apps automatisieren. Sehen Sie sich das Kapitel unten an, um mehr über Cmdlets zu erfahren.

### <a name="adding-and-publishing-your-app-to-the-app-catalog"></a>Hinzufügen Ihrer App zum App-Katalog und Veröffentlichen Ihrer App im App-Katalog
Sie müssen Ihre App (.sppkg-Datei, .app-Datei) zu Ihrem Mandanten-App-Katalog hinzufügen, damit Sie sie später auf Ihrer SharePoint-Seite zur Verfügung stellen können. Dieser Vorgang kann mit einem einfachen cmdlet durchgeführt werden:

```PowerShell
Add-PnPApp -Path ./myapp.sppkg
```

Nachdem Sie die App hinzugefügt haben, müssen Sie sie veröffentlichen, damit sie von anderen Benutzern Ihres Mandanten verwendet werden kann. Unter PnP PowerShell-Cmdlets finden Sie die entsprechende Vorgehensweise:

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> Verwenden Sie die Kennzeichnung SkipFeatureDeployment, damit eine App, die für die Mandanten-weite Bereitstellung entwickelt wurde, auch tatsächlich als Mandanten-weit bereitgestellte App verfügbar ist.



### <a name="removing-the-app-from-the-app-catalog"></a>Entfernen der App aus dem App-Katalog
Möglicherweise möchten Sie auch eine zuvor hinzugefügte App entfernen. Dieser Vorgang kann mit dem folgenden Cmdlet ausgeführt werden:

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="using-apps-on-your-site"></a>Verwenden von Apps auf Ihrer Website
Nachdem die App zum App-Katalog hinzugefügt und veröffentlicht wurde, können Sie mit der Installation der App in Ihre Website beginnen.

```PowerShell
Install-PnPApp -Identity <app id>
```


Eine hinzugefügte App muss außerdem aktualisiert werden:

```PowerShell
Update-PnPApp -Identity <app id>
```


Möglicherweise möchten Sie die App auch von Ihrer Seite deinstallieren:

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> Wenn Sie eine App von Ihrer Website deinstallieren, wird die App vollständig gelöscht, sodass sie nicht im Papierkorb der Website landen.



### <a name="knowing-which-apps-are-there-for-you-to-use"></a>Informieren Sie sich, welche Apps für die Verwendung zur Verfügung stehen.
Sie können eine Liste der Apps abrufen, die zu der Website hinzugefügt werden können:

```PowerShell
Get-PnPApp
```
