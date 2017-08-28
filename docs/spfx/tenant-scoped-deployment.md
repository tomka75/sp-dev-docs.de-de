# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a>Mandantenweite Lösungsbereitstellung für SharePoint Framework-Lösungen

Sie können Ihre SharePoint Framework-Komponenten so konfigurieren, dass sie sofort nach der Installation des Lösungspakets im App-Katalog eines Mandanten mandantenweit verfügbar sind. Hierzu verwenden Sie das Attribut **skipFeatureDeployment** in der Datei **package-solution.json**.

Ist dieses Attribut für eine Lösung aktiviert, wird dem Mandantenadministrator bei der Installation des Lösungspakets im App-Katalog des Mandanten angeboten, die Lösung automatisch in allen Websitesammlungen und auf allen Websites im Mandanten verfügbar zu machen. 

Eine Demonstration der mandantenweiten Bereitstellung finden Sie in dem folgenden Video in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=pemHOZCSwZI).

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> Beachten Sie: Sie müssen auf die neueste Version der SharePoint Framework-Yeoman-Vorlage aktualisieren, um diese Funktion nutzen zu können. Aktualisieren können Sie Ihre globale Installation mit dem Befehl `npm install -g @microsoft/generator-sharepoint`. 

## <a name="solution-specific-requirements"></a>Lösungsspezifische Anforderungen

Wenn diese Option verwendet wird, werden alle Featureframeworkdefinitionen in der SharePoint Framework-Lösung ignoriert. Enthält Ihre Lösung Featureframeworkdefinitionen, beispielsweise zur Erstellung einer benutzerdefinierten Liste, sollten Sie diese lösungsspezifische Option nicht nutzen.

* [Bereitstellen von SharePoint-Objekten mit Ihrem Lösungspaket](#)

> Beachten Sie: Lösungen, für die eine automatische mandantenweite Bereitstellung konfiguriert ist, werden auf Website-Ebene nicht unter „App hinzufügen“ aufgeführt. 

## <a name="configuring-solution-to-be-available-cross-tenant"></a>Konfigurieren von Lösungen für mandantenweite Verfügbarkeit

In der SharePoint Framework-Yeoman-Vorlage ist eine spezifische Frage für diese Option enthalten. Ihre Antwort auf diese Frage hat direkte Auswirkungen auf das Attribut **skipFeatureDeployment** in der Datei **package-solution.json**. 

![Yeoman-Frage zur mandantenweiten Bereitstellung](../../images/tenant-deploy-yeoman.png)

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

Das Kontrollkästchen **Make this solution available to all sites in the organization** ist standardmäßig deaktiviert. Wenn der Administrator das Kontrollkästchen aktiviert, sind die Komponenten der Lösung automatisch im gesamten Mandantenbereich sichtbar und verfügbar. 

![Einstellung „Make this solution available to all sites in an organization“ bei der Bereitstellung der Lösung im App-Katalog](../../images/tenant-deploy-app-catalog.png)

Beachten Sie: Da die lösungs- und websitespezifischen Aktualisierungsaktionen nur bei Verwendung eines Featureframeworks verfügbar sind, gibt es keine spezifische Aktualisierungsoption für zentral bereitgestellte Lösungen. Lösungen dieses Typs lassen sich einfach über eine Aktualisierung der lösungsspezifischen Objekte im CDN sowie eine Aktualisierung des Pakets im App-Katalog aktualisieren. Dadurch werden automatisch sämtliche vorhandenen Komponenteninstanzen im Mandantenbereich so aktualisiert, dass sie die neuesten Komponentenobjekte verwenden (z. B. JavaScript-Dateien und aktualisierte CSS-Dateien).

## <a name="client-side-web-part-visibility-in-sharepoint-sites"></a>Sichtbarkeit clientseitiger Webparts auf SharePoint-Websites

In zentral bereitgestellten Lösungen enthaltene Webparts sind sofort in der Webpartauswahl sichtbar, sowohl auf klassischen als auch auf modernen Seiten. 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a>Auswirkungen der Einstellung „skipFeatureDeployment“ auf Erweiterungen

SharePoint Framework-Erweiterungen stehen sofort zur Verwendung auf SharePoint-Websites zur Verfügung. Das bedeutet, dass sie mit der Eigenschaft **ClientSideComponentId** von SharePoint-Elementen verknüpft werden können, beispielsweise von *Feldern* und *benutzerdefinierten Aktionen von Benutzern*. 

