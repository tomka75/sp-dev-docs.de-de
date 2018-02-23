---
title: "Mandantenweite Lösungsbereitstellung für SharePoint-Framework-Lösungen"
description: "Konfigurieren Sie Ihre SharePoint-Framework-Komponenten, damit diese sofort in dem Mandanten verfügbar sind, wenn das Lösungspaket im Mandanten-App-Katalog installiert ist."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: d48aa779602950cd589b4d5e6dbaab868b698f9e
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a>Mandantenweite Lösungsbereitstellung für SharePoint-Framework-Lösungen

Sie können Ihre SharePoint-Framework-Komponenten konfigurieren, damit diese sofort in dem Mandanten verfügbar sind, wenn das Lösungspaket im Mandanten-App-Katalog installiert ist. Dies kann mit dem **skipFeatureDeployment**-Attribut in der Datei **solution.json-Paket** konfiguriert werden.

Ist dieses Attribut für eine Lösung aktiviert, wird dem Mandantenadministrator bei der Installation des Lösungspakets im App-Katalog des Mandanten angeboten, die Lösung automatisch in allen Websitesammlungen und auf allen Websites im Mandanten verfügbar zu machen. 

Eine Demonstration der mandantenweiten Bereitstellung finden Sie in dem folgenden Video in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=pemHOZCSwZI).

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> [!NOTE] 
> Sie müssen auf die neueste Version der SharePoint-Framework-Yeoman-Vorlage aktualisieren, um diese Funktion nutzen zu können. Aktualisieren können Sie Ihre globale Installation mit dem Befehl `npm install -g @microsoft/generator-sharepoint`. 

## <a name="solution-specific-requirements"></a>Lösungspezifische Anforderungen

Wenn diese Option verwendet wird, werden alle Featureframeworkdefinitionen in der SharePoint-Framework-Lösung ignoriert. Enthält Ihre Lösung Featureframeworkdefinitionen, beispielsweise zur Erstellung einer benutzerdefinierten Liste, sollten Sie diese lösungsspezifische Option nicht nutzen.

Weitere Informationen finden Sie unter [Bereitstellen von SharePoint-Elementen mit Ihrem Lösungspaket](./toolchain/provision-sharepoint-assets.md).

> [!NOTE] 
> Lösungen, für die eine automatische mandantenweite Bereitstellung konfiguriert ist, werden auf Website-Ebene nicht unter „App hinzufügen“ aufgeführt. 

## <a name="configure-solution-to-be-available-across-the-tenant"></a>Konfigurieren von Lösungen für mandantenweite Verfügbarkeit

In der SharePoint-Framework-Yeoman-Vorlage wird eine bestimmte Frage im Zusammenhang mit dieser Option gestellt. Diese Frage wirkt sich direkt auf das **skipFeatureDeployment**-Attribut in der Datei **solution.json-Paket**. 

![Yeoman-Frage zur mandantenweiten Bereitstellung](../images/tenant-deploy-yeoman.png)

<br/>

In der folgenden Beispielkonfiguration ist **skipFeatureDeployment** auf „true“ gesetzt. Das bedeutet, dass die Lösung zentral im gesamten Mandanten bereitgestellt werden kann. 

```json
{
  "solution": {
    "name": "tenant-deploy-client-side-solution",
    "id": "dd4feca4-6f7e-47f1-a0e2-97de8890e3fa",
    "version": "1.0.0.0",
    "skipFeatureDeployment": true
  },
  "paths": {
    "zippedPackage": "solution/tenant-deploy-true.sppkg"
  }
}

```

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a>Genehmigen einer mandantenweiten Bereitstellung im App-Katalog

Wird eine Lösung, für die das Attribut **skipFeatureDeployment** auf **true** gesetzt ist, im App-Katalog eines Mandanten bereitgestellt, wird dem Administrator angeboten, sie zentral für den gesamten Mandantenbereich bereitzustellen.

Standardmäßig ist das Kontrollkästchen **Diese Lösung für alle Websites der Organisation verfügbar machen** nicht aktiviert. Wenn Sie das Kontrollkästchen vom Administrator aktiviert wird, werden Komponenten in den Lösungen automatisch für den gesamten Mandantenbereich angezeigt und verfügbar. 

![Die Einstellung „Diese Lösung für alle Websites der Organisation verfügbar machen“ wird bei der Bereitstellung der Lösung im App-Katalog angezeigt.](../images/tenant-deploy-app-catalog.png)

Da die Lösung und die websitespezifischen Upgradeaktionen nur verfügbar sind, wen Sie das Featureframework verwenden, gibt es keine spezifische Upgradeoption für die zentral bereitgestellten Lösungen. Diese Lösungen können aktualisiert werden, indem lösungsspezifische Objekte im CDN und das Paket im App-Katalog aktualisiert werden. Dabei werden alle vorhandenen Komponenteninstanzen für den gesamten Mandanten automatisch für die Verwendung der neuesten Komponentenobjekte, u. a. JavaScript-Dateien und aktualisierte CSS-Dateien, aktualisiert.

## <a name="client-side-web-part-visibility-on-sharepoint-sites"></a>Sichtbarkeit clientseitiger Webparts auf SharePoint-Websites

In zentral bereitgestellten Lösungen enthaltene Webparts sind sofort in der Webpartauswahl sichtbar, sowohl auf klassischen als auch auf modernen Seiten. 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a>Auswirkungen der Einstellung „skipFeatureDeployment“ auf Erweiterungen

[SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md) sind sofort verfügbar und können auf SharePoint-Websites verwendet werden. Das bedeutet, dass sie den **ClientSideComponentId**-Eigenschaften in bestimmten SharePoint-Elementen, z. B. **Feldern** und **benutzerdefinierten Aktionen** zugeordnet werden können. 

## <a name="see-also"></a>Siehe auch

- [Übersicht über das SharePoint-Framework](sharepoint-framework-overview.md)