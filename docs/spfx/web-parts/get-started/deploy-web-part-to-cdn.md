---
title: Bereitstellen Ihres clientseitigen SharePoint-Webparts im Azure CDN
description: "Erstellen Sie ein neues Beispielwebpart, und stellen Sie seine Objekte in einem Azure CDN bereit, statt das Office 365 CDN als Hostinglösung zu verwenden."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 2fe92081817625758c480b1ac7d0af3ac92aa8f1
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="deploy-your-sharepoint-client-side-web-part-to-azure-cdn"></a>Bereitstellen Ihres clientseitigen SharePoint-Webparts im Azure CDN

Erstellen Sie ein neues Beispielwebpart, und stellen Sie seine Objekte in einem Azure Content Delivery Network (CDN) bereit, statt das Office 365 CDN als Hostinglösung zu verwenden. Sie verwenden ein Azure-Speicherkonto, das in ein CDN integriert ist, um Ihre Ressourcen bereitzustellen. Die Buildtools von SharePoint Framework bieten eine sofort nutzbare Unterstützung für die Bereitstellung auf einem Azure-Speicherkonto. Sie können die Dateien jedoch auch manuell an einen CDN-Anbieter Ihrer Wahl oder nach SharePoint hochladen.

> [!NOTE]
> Es gibt mehrere unterschiedliche Hostingoptionen für Webpart-Objekte. In diesem Lernprogramm steht die Option „Azure CDN“ im Vordergrund, Sie können jedoch auch das [Office 365 CDN](./hosting-webpart-from-office-365-cdn.md) verwenden oder einfach Ihre Objekt aus der SharePoint-Bibliothek aus dem Mandanten hosten. Im letzteren Fall würden Sie nicht von den CDN-Leistungssteigerungen profitieren, im Hinblick auf die Funktionalität wäre dies jedoch möglich. Technisch gesehen wäre jeder Ort zum Hosten der Objekte für Endbenutzer denkbar, auf den Endbenutzer über HTTP zugreifen können.

## <a name="configure-an-azure-storage-account"></a>Konfigurieren eines Azure-Speicherkontos

Um ein Azure-Speicherkonto zu konfigurieren und in das CDN zu integrieren, befolgen Sie die Anweisungen unter [Integrieren eines Azure-Speicherkontos in CDN](https://docs.microsoft.com/de-DE/azure/cdn/cdn-create-a-storage-account-with-cdn) sowie die detaillierten Schritte in diesem Artikel. 

### <a name="storage-account-name"></a>Speicherkontoname

Dies ist der Name, den Sie zum Erstellen des Speicherkontos verwendet haben, wie in [Schritt 1: Erstellen eines Speicherkontos](https://docs.microsoft.com/de-DE/azure/cdn/cdn-create-a-storage-account-with-cdn#step-1-create-a-storage-account) beschrieben.

Im folgenden Screenshot ist **spfxsamples** der Name des Speicherkontos.

![Screenshot, auf dem die Seite „Erstellen eines neues Speicherkontos“ dargestellt ist](../../../images/deploy-create-storage-account.png)

Auf diese Weise wird der neue Speicherkontoendpunkt **spfxsamples.blob.core.windows.net** erstellt. 

> [!NOTE]
> Sie müssen einen eindeutigen Speicherkontonamen für Ihre eigenen SharePoint-Framework-Projekte erstellen.

### <a name="blob-container-name"></a>Name des BLOB-Containers

Erstellen Sie einen neuen Blob-Dienstcontainer. Dieser ist im Dashboard des Speicherkontos verfügbar.

Wählen Sie **+ Container** aus, und erstellen Sie einen neuen Container mit den folgenden Angaben:

* Name: **azurehosted-webpart**
* Zugriffstyp: Container

![Bild, das die Option zum Erstellen von Blob-Containern zeigt](../../../images/deploy-option-blob-container.png)

### <a name="storage-account-access-key"></a>Tastenkombination für Speicherkonto

Wählen Sie im Dashboard des Speicherkontos die Option **Tastenkombination** im Dashboard aus, und kopieren Sie eine der Tastenkombinationen.

![Bild, das die Tastenkombination für das Speicherkonto zeigt](../../../images/deploy-storage-account-accesskey.png)

### <a name="cdn-profile-and-endpoint"></a>CDN-Profil und Endpunkt

Erstellen Sie ein neues CDN-Profil, und weisen Sie den CDN-Endpunkt diesem BLOB-Container zu.

1. Erstellen Sie ein neues CDN-Profil, wie unter [Schritt 2: Aktivieren von CDN für das Speicherkonto](https://docs.microsoft.com/de-DE/azure/cdn/cdn-create-a-storage-account-with-cdn#step-2-enable-cdn-for-the-storage-account) beschrieben (Scrollen Sie in Schritt 2 nach unten zu **So erstellen Sie ein neues CDN-Profil**).

  Im folgenden Screenshot ist **spfxwebparts** der Name des CDN-Profils.

  ![Screenshot zur Erstellung eines neuen CDN-Profils](../../../images/deploy-create-cdn-profile.png)

2. Erstellen Sie einen CDN-Endpunkt, wie unter [Schritt 2: Aktivieren von CDN für das Speicherkonto](https://docs.microsoft.com/de-DE/azure/cdn/cdn-create-a-storage-account-with-cdn#step-2-enable-cdn-for-the-storage-account) beschrieben. Der CDN-Endpunkt wird mit der folgenden URL erstellt:`http://spfxsamples.azureedge.net`

  Im folgenden Screenshot ist **spfxsamples** beispielsweise der Endpunktname **Speicher** ist der Ursprungstyp, und **spfxsamples.blob.core.windows.net** ist das Speicherkonto.

  <img alt="Screenshot of create CDN endpoint" src="../../../images/deploy-create-cdn-endpoint.png" width="700">

Da Sie den CDN-Endpunkt dem Speicherkonto zugeordnet haben, können Sie auch unter der folgenden URL auf den BLOB-Container zugreifen: `http://spfxsamples.azureedge.net/azurehosted-webpart/`

Beachten Sie jedoch, dass Sie die Dateien noch nicht bereitgestellt haben.

## <a name="create-a-new-web-part-project"></a>Erstellen eines neuen Webpart-Projekts

1. Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:

  ```
  md azurehosted-webpart
  ```

2. Wechseln Sie in das Projektverzeichnis:

  ```
  cd azurehosted-webpart
  ```

3. Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue SharePoint Framework-Lösung zu erstellen:

  ```
  yo @microsoft/sharepoint
  ```
    
4. Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

  * Akzeptieren Sie den Standardnamen **azurehosted-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.
  * Wählen Sie **SharePoint Online only (latest)**aus, und drücken Sie die **EINGABETASTE**.
  * Wählen Sie als Speicherort für die Dateien die Option **Use the current folder** aus.
  * Wählen Sie **y** aus, um die mandantenweite Bereitstellung zu verwenden, mit der das Webpart auf allen Websites zur Verfügung steht, sobald es bereitgestellt wird. 
  * Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus. 

5. Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:

  * Verwenden Sie **AzureCDN** als Namen des Webparts, und drücken Sie die **EINGABETASTE**.
  * Akzeptieren Sie die Standardbeschreibung **AzureCDN description** als Beschreibung für Ihr Webpart, und drücken Sie die **EINGABETASTE**.
  * Akzeptieren Sie die Standardeinstellung **No javaScript web framework** als das zu verwendende Framework, und drücken Sie dann die **EINGABETASTE**.

  ![Yeoman-Generator-Fragen für das neu erstellte Webpart](../../../images/cdn-azure-create-webpart-yo.png)

  An diesem Punkt erstellt Yeoman ein Gerüst für die Lösungsdateien und installiert die erforderlichen Abhängigkeiten. Das kann einige Minuten dauern. Yeoman nimmt auch Ihr benutzerdefiniertes Webpart in das Projektgerüst auf.

6. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

  ```sh
  npm shrinkwrap
  ```

7. Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:

  ```
  code .
  ```

## <a name="configure-the-solution-not-to-use-default-settings"></a>Konfigurieren der Lösung für die Nichtverwendung der Standardeinstellungen

1. Öffnen Sie **package-solution.json** im Ordner **config**.

  Hier werden die Lösungspakete gesteuert.

2. Ändern Sie den `includeClientSideAssets`-Wert zu **false**, damit clientseitige Objekte nicht in die .sppkg-Datei gepackt werden, was dem Standardverhalten entspricht. Da Objekte aus einem externen CDN gehostet werden, sollen sie nicht im Lösungspaket enthalten sein. Die Konfiguration sollte etwa wie folgt aussehen.

  ``` json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "azurehosted-webpart-client-side-solution",
      "id": "a4e95ed1-d096-4573-8a57-d0cc3b52da6a",
      "version": "1.0.0.0",
      "includeClientSideAssets": false,
      "skipFeatureDeployment": true
    },
    "paths": {
      "zippedPackage": "solution/azurehosted-webpart.sppkg"
    }
  }
  ```

  > [!NOTE]
  > Die `skipFeatureDeployment`-Einstellung lautet **true**, da die Antwort für die mandantenweite Bereitstellung in dem Yeoman-Ablauf „y“ lautete. Dies bedeutet, dass Sie die Lösung erst auf der Website installieren müssen, wenn das Webpart verfügbar ist. Die Bereitstellung und Genehmigung des Lösungspakets in dem App-Katalog des Mandanten reicht aus, damit das Webpart auf allen Websites in dem jeweiligen Mandanten zur Verfügung steht.


## <a name="configure-azure-storage-account-details"></a>Konfigurieren der Details eines Azure-Speicherkontos

1. Öffnen Sie **deploy-azure-storage.json** im Ordner **config**.

  Das ist die Datei, die die Details zu Ihrem Speicherkonto enthält.

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/deploy-azure-storage.schema.json",
    "workingDir": "./temp/deploy/",
    "account": "<!-- STORAGE ACCOUNT NAME -->",
    "container": "azurehosted-webpart",
    "accessKey": "<!-- ACCESS KEY -->"
  }
  ```

2. Ersetzen Sie **account**, **container** und **accessKey** jeweils mit dem Speicherkontonamen, dem BLOB-Container und der Tastenkombination für das Speicherkonto.

  **workingDir** ist das Verzeichnis, in dem sich die Webpartressourcen befinden.

  In diesem Beispiel sieht diese Datei mit dem zuvor erstellten Speicherkonto wie folgt aus:

  ```json
  {
    "workingDir": "./temp/deploy/",
    "account": "spfxsamples",
    "container": "azurehosted-webpart",
    "accessKey": "q1UsGWocj+CnlLuv9ZpriOCj46ikgBbDBCaQ0FfE8+qKVbDTVSbRGj41avlG73rynbvKizZpIKK9XpnpA=="
  }
  ```

3. Speichern Sie die Datei.

## <a name="configure-the-web-part-to-load-from-cdn"></a>Konfigurieren des Webparts für das Laden aus dem CDN

Damit das Webpart aus Ihrem CDN geladen wird, müssen Sie ihm den CDN-Pfad mitteilen.

1. Wechseln Sie zu Visual Studio Code, und öffnen Sie **write-manifests.json** aus dem Ordner **config**.

2. Geben Sie den Pfad der CDN-Basis für die **cdnBasePath**-Eigenschaft ein.

  ```json
  {
    "cdnBasePath": "<!-- PATH TO CDN -->"
  }
  ```

  In diesem Beispiel sieht diese Datei mit dem zuvor erstellten CDN-Profil wie folgt aus:

  ```json
  {
    "cdnBasePath": "https://spfxsamples.azureedge.net/azurehosted-webpart/"
  }
  ```

  > [!NOTE]
  > Der CDN-Basispfad ist der CDN-Endpunkt mit dem BLOB-Container.

3. Speichern Sie die Datei.


## <a name="prepare-the-web-part-assets-to-deploy"></a>Vorbereiten der bereitzustellenden Webpartressourcen

Bevor Sie die Ressourcen in das CDN hochladen, müssen Sie sie erstellen.

1. Wechseln Sie zur Konsole, und führen Sie die folgende `gulp`-Aufgabe aus:

  ```
  gulp bundle --ship
  ```

  Dadurch werden die minimierten Ressourcen erstellt, die zum Hochladen an den CDN-Anbieter erforderlich sind. In `--ship` ist das Buildtool zum Erstellen für die Verteilung dargestellt. Beachten Sie außerdem, dass die Ausgabe der Buildtools angibt, dass das Build-Ziel SHIP ist.

  ```
  Build target: SHIP
  [21:23:01] Using gulpfile ~/apps/azurehosted-webpart/gulpfile.js
  [21:23:01] Starting gulp
  [21:23:01] Starting 'default'...
  ```

  Die minimierten Ressourcen befinden sich im `temp\deploy`-Verzeichnis.

## <a name="deploy-assets-to-azure-storage"></a>Bereitstellen von Ressourcen für Azure Storage

1. Wechseln Sie zur Konsole des **azurehosted-webpart**-Projektverzeichnisses.

2. Geben Sie die gulp-Aufgabe ein, um die Ressourcen in Ihrem Speicherkonto bereitzustellen:

  ```
  gulp deploy-azure-storage
  ```

  Dadurch wird das Webpartbundle zusammen mit anderen Ressourcen wie JavaScript- und CSS-Dateien im CDN bereitgestellt.

## <a name="deploy-the-updated-package"></a>Bereitstellen des aktualisierten Pakets

### <a name="to-package-the-solution"></a>So verpacken Sie die Lösung

Da Sie das Webpartbundle geändert haben, müssen Sie das Paket erneut im App-Katalog bereitstellen. Sie haben **--ship** verwendet, um minimierte Ressourcen für die Verteilung zu generieren.

1. Wechseln Sie zur Konsole des **azurehosted-webpart**-Projektverzeichnisses.

2. Geben Sie die gulp-Aufgabe zum Verpacken der clientseitigen Lösung an, dieses Mal mit gesetztem `--ship`-Flag. Dadurch wird die Aufgabe gezwungen, den im vorherigen Schritt konfigurierten CDN-Basispfad aufzugreifen:

  ```
  gulp package-solution --ship
  ```

  Dadurch wird das aktualisierte clientseitige Lösungspaket im Ordner **sharepoint\solution** erstellt.

### <a name="to-upload-to-your-app-catalog"></a>So laden Sie in den App-Katalog hoch

1. Laden Sie das clientseitige Lösungspaket in den App-Catalog hoch, oder verwenden Sie Drag & Drop. Beachten Sie, dass die URL auf die in den vorherigen Schritten konfigurierte URL des Azure CDN verweist. 

2. Aktivieren Sie das Kontrollkästchen, um anzugeben, dass die Lösung automatisch auf allen Websites in der Organisation bereitgestellt werden kann.

  ![Screenshot der Aufforderung für die Vertrauensstellung zum clientseitigen Lösungspaket](../../../images/cdn-azure-trust-hosted-app-catalog.png)

3. Wählen Sie **Bereitstellen**.

  Der App-Katalog verfügt nun über das clientseitige Lösungspaket, in das das Webpartbundle aus dem CDN geladen wird.

## <a name="test-the-helloworld-web-part"></a>Testen des HelloWorld-Webparts

1. Wechseln Sie zu einer beliebigen SharePoint-Website in Ihrem Mandanten, und wählen Sie **Seite hinzufügen** in dem Menü mit dem *Zahnrad* aus.

2. **Bearbeiten** Sie die Seite, und wählen Sie das **AzureCDN**-Webpart in der Webpartauswahl aus, um zu bestätigen, dass die Bereitstellung erfolgreich war.

  ![Screenshot der Aufforderung für die Vertrauensstellung zum clientseitigen Lösungspaket](../../../images/cdn-azure-picker-selection-page.png)

3. Beachten Sie, dass **gulp serve** nicht ausgeführt wird und dass deshalb nichts von **localhost** kommt. Inhalt wird vom Azure CDN bereitgestellt. Sie können dies auch prüfen, indem Sie in Ihrem Browser F12 drücken und sicherstellen, dass das Azure CDN als Quelle für die Seitenobjekte angezeigt wird.

  ![Quellen mit der URL des Azure CDN](../../../images/cdn-azure-sources-browser-dev-tools.png)

## <a name="deploy-to-other-cdns"></a>Bereitstellen auf anderen CDNs

Um die Ressourcen auf Ihrem bevorzugten CDN-Anbieter bereitzustellen, können Sie die Dateien aus dem Ordner **tmp\deploy** kopieren. Zum Generieren der Ressourcen für die Verteilung führen Sie den folgenden gulp-Befehl wie zuvor mit dem Parameter **--ship** aus:

```
gulp bundle --ship
```

Solange Sie die **cdnBasePath**-Eigenschaft entsprechend aktualisieren, werden Ihre Dateien ordnungsgemäß geladen.

> [!NOTE]
> Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues). Vielen Dank im Voraus für Ihr Feedback.

## <a name="see-also"></a>Weitere Artikel

- [Erstellen des ersten clientseitigen SharePoint-Webparts](build-a-hello-world-web-part.md)