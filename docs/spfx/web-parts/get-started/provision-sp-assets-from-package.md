---
title: Bereitstellen von SharePoint-Ressourcen aus Ihrem clientseitigen SharePoint-Webpart
description: "SharePoint-Objekte können im Rahmen der SharePoint Framework-Lösung bereitgestellt werden und werden auf SharePoint-Websites bereitgestellt, wenn die Lösung darauf installiert wird."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 73fc74a900be49b6647506f84ed04b06286bad8c
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="provision-sharepoint-assets-from-your-sharepoint-client-side-web-part"></a>Bereitstellen von SharePoint-Ressourcen aus Ihrem clientseitigen SharePoint-Webpart

SharePoint-Objekte können im Rahmen der SharePoint Framework-Lösung bereitgestellt werden und werden auf SharePoint-Websites bereitgestellt, wenn die Lösung darauf installiert wird. 

Bevor Sie beginnen, führen Sie die Schritte in den folgenden Artikeln aus, um sicherzustellen, dass Sie den grundlegenden Fluss des Erstellens eines benutzerdefinierten, clientseitigen Webparts verstehen:

* [Erstellen des ersten Webparts](build-a-hello-world-web-part.md)
* [Verbinden des Webparts mit SharePoint](connect-to-sharepoint.md) 

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=qAqNk_X82QM&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=8) nachvollziehen. 

<a href="https://www.youtube.com/watch?v=qAqNk_X82QM&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=8">
<img src="../../../images/spfx-youtube-tutorial7.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a>Erstellen eines neuen Webpart-Projekts

1. Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:

  ```
  md asset-deployment-webpart
  ```

2. Wechseln Sie in das Projektverzeichnis:

  ```
  cd asset-deployment-webpart
  ```
    
3. Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue clientseitige Webpartlösung zu erstellen:

  ```
  yo @microsoft/sharepoint
  ```

4. Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

  * Akzeptieren Sie den Standardnamen **asset-deployment-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.
  * Wählen Sie **SharePoint Online only (latest)**, und drücken Sie dann die **EINGABETASTE**.
  * Wählen Sie **Aktuellen Ordner verwenden** als Speicherort für die Dateien aus.
  * Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird. 
  * Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus. 

5. Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:

  * Geben Sie **AssetDeployment** als Webpartnamen ein, und drücken Sie die **EINGABETASTE**.
  * Geben Sie**AssetDeployment-Webpart** als Beschreibung des Webparts ein, und drücken Sie die **EINGABETASTE**. 
  * Akzeptieren Sie die Standardeinstellung **No javascript web framework** als Framework, und drücken Sie dann die **EINGABETASTE**, um fortzufahren.

  ![Yeoman-Eingabeaufforderungen](../../../images/asset-deployment-yeoman.png)

  An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien. Das kann einige Minuten dauern. Yeoman erstellt ein Gerüst für das Projekt, um auch das **AssetDeployment**-Webpart einzuschließen.

6. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

  ```sh
  npm shrinkwrap
  ```

7. Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:

  ```
  code .
  ```

## <a name="create-folder-structure-for-your-sharepoint-assets"></a>Erstellen der Ordnerstruktur für Ihre SharePoint-Ressourcen

Wir müssen zuerst einen **Ressourcen**ordner erstellen, in dem die gesamten Featureframeworkressourcen platziert werden, die zum Bereitstellen von SharePoint-Strukturen verwendet werden, wenn das Paket installiert wird.

1. Erstellen Sie einen Ordner mit dem Namen **Sharepoint** auf der Stammebene der Lösung.

2. Erstellen Sie einen Ordner mit dem Namen **Ressourcen** als Unterordner für den soeben erstellten **Sharepoint**-Ordner

  Die Lösungsstruktur sollte in etwa wie folgt aussehen:

  ![Screenshot, in dem der Ressourcenordner unter dem SharePoint-Ordner in der Lösungsstruktur angezeigt wird](../../../images/tutorial-feature-solution-initial-structure.png)


## <a name="create-feature-framework-files-for-initial-deployment"></a>Erstellen von Featureframeworkdateien für die anfängliche Bereitstellung

Um SharePoint-Ressourcen auf Websites mit Featureframeworkelementen bereitstellen zu können, müssen wir die erforderlichen XML-Dateien für den Ressourcenordner erstellen. Unterstützte Elemente für die SharePoint Framework-Lösungspakete sind wie folgt:

* Felder/Websitespalten
* Inhaltstypen
* Listeninstanzen
* Listeninstanzen mit benutzerdefiniertem Schema

In den folgenden Schritten wird die erforderliche Struktur definiert, die bereitgestellt werden soll.

### <a name="to-add-an-elementxml-file-for-sharepoint-definitions"></a>So fügen Sie die Datei „elements.xml“ für SharePoint-Definitionen hinzu

1. Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements.xml**.

2. Kopieren Sie die folgende XML-Struktur in **elements.xml**.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">

      <Field ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}"
              Name="SPFxAmount"
              DisplayName="Amount"
              Type="Currency"
              Decimals="2"
              Min="0"
              Required="FALSE"
              Group="SPFx Columns" />

      <Field ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}"
              Name="SPFxCostCenter"
              DisplayName="Cost Center"
              Type="Choice"
              Required="FALSE"
              Group="SPFx Columns">
          <CHOICES>
          <CHOICE>Administration</CHOICE>
          <CHOICE>Information</CHOICE>
          <CHOICE>Facilities</CHOICE>
          <CHOICE>Operations</CHOICE>
          <CHOICE>Sales</CHOICE>
          <CHOICE>Marketing</CHOICE>
          </CHOICES>
      </Field>

      <ContentType ID="0x010042D0C1C200A14B6887742B6344675C8B" 
              Name="Cost Center" 
              Group="SPFx Content Types" 
              Description="Sample content types from web part solution">
          <FieldRefs>
              <FieldRef ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}" /> 
              <FieldRef ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}" />
          </FieldRefs>
      </ContentType> 

      <ListInstance 
              CustomSchema="schema.xml"
              FeatureId="00bfea71-de22-43b2-a848-c05709900100"
              Title="SPFx List" 
              Description="SPFx List"
              TemplateType="100"
              Url="Lists/SPFxList">
      </ListInstance>

  </Elements>
  ```

  Beachten Sie zu der eingefügten XML-Struktur Folgendes:
  * Wir stellen zwei Felder, den Inhaltstyp und eine Listeninstanz mit benutzerdefiniertem Schema auf der Website bereit.
  * Definitionen verwenden das Standardschema für das Featureframework, das SharePoint-Entwickler gut kennen.
  * Auf benutzerdefinierte Felder wird in dem eingeführten Inhaltstyp verwiesen.
  * Wir verwenden das **CustomSchema**-Attribut im **ListInstance**-Element, um die Bereitstellungszeit der schema.xml-Datei für die Liste zu definieren. Auf diese Weise basiert die Liste immer noch auf der einsatzbereiten Listenvorlage (die normale benutzerdefinierte Liste „100“ in diesem Fall), es kann jedoch während der anfänglichen Bereitstellung eine alternative Bereitstellungsdefinition definiert werden.

  Weitere Informationen zu den verwendeten Schemastrukturen finden Sie unter [Verwenden von Funktionen in SharePoint Foundation](https://msdn.microsoft.com/en-us/library/office/ms460318(v=office.14).aspx) auf MSDN.

### <a name="to-add-a-schemaxml-file-for-defining-list-structure"></a>So fügen Sie die Datei „schema.xml“ zum Definieren der Listenstruktur hinzu

Im vorherigen Schritt haben wir auf die Datei **schema.xml** im **CustomSchema**-Attribut des **ListInstance**-Elements verwiesen, dies muss also in das Paket eingeschlossen werden. 

1. Erstellen Sie eine neue Datei innerhalb des Ordners **SharePoint\Ressourcen** mit dem Namen **schema.xml**.

2. Kopieren Sie die folgende XML-Struktur in **schema.xml**.

  ```xml
  <List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE" Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
    <MetaData>
      <ContentTypes>
        <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
      </ContentTypes>
      <Fields></Fields>
      <Views>
        <View BaseViewID="1" Type="HTML" WebPartZoneID="Main" DisplayName="$Resources:core,objectiv_schema_mwsidcamlidC24;" DefaultView="TRUE" MobileView="TRUE" MobileDefaultView="TRUE" SetupPath="pages\viewpage.aspx" ImageUrl="/_layouts/images/generic.png" Url="AllItems.aspx">
          <XslLink Default="TRUE">main.xsl</XslLink>
          <JSLink>clienttemplates.js</JSLink>
          <RowLimit Paged="TRUE">30</RowLimit>
          <Toolbar Type="Standard" />
          <ViewFields>
            <FieldRef Name="LinkTitle"></FieldRef>
            <FieldRef Name="SPFxAmount"></FieldRef>
            <FieldRef Name="SPFxCostCenter"></FieldRef>
          </ViewFields>
          <Query>
            <OrderBy>
              <FieldRef Name="ID" />
            </OrderBy>
          </Query>
        </View>
      </Views>
      <Forms>
        <Form Type="DisplayForm" Url="DispForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
        <Form Type="EditForm" Url="EditForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
        <Form Type="NewForm" Url="NewForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      </Forms>
    </MetaData>
  </List>
  ```

Beachten Sie zu der eingefügten XML-Struktur Folgendes:
* Auf den benutzerdefinierten Inhaltstyp, der unter Verwendung der Datei **elements.xml** bereitgestellt wird, wird im **ContentTypeRef**-Element verwiesen.
* Auf benutzerdefinierte Felder mit dem Namen **SPFxAmount** und **SPFxCostCenter** wird im **FieldRef**-Element verwiesen.

Weitere Einzelheiten zu den verwendeten Schemastrukturen finden Sie im Artikel [Grundlegendes zu Schema.xml-Dateien](https://msdn.microsoft.com/en-us/library/office/ms459356(v=office.14).aspx) auf MSDN.

## <a name="ensure-that-definitions-are-taken-into-use-in-build-pipeline"></a>Sicherstellen, dass Definitionen in der Buildpipeline verwendet werden

Nun haben wir die erforderlichen Strukturen für das Bereitstellen von SharePoint-Ressourcen automatisch aus der Lösung erstellt, wenn diese bereitgestellt wird. Der nächste Schritt besteht darin, sicherzustellen, dass diese XML-Dateien als Teil der Lösungsdatei verpackt werden.

1. Öffnen Sie **package-solution.json** im Ordner „config“.

  Die Datei **package-solution.json** definiert die Paketmetadaten, wie im folgenden Code dargestellt:

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "1.0.0.0",
      "includeClientSideAssets": true
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }

  ```

2. Um sicherzustellen, dass unsere neu hinzugefügten Featureframeworkdateien beim Verpacken der Lösung berücksichtigt werden, müssen wir eine Featureframework-Featuredefinition für das Lösungspaket einschließen. Wir werden eine JSON-Definition für erforderliche Features innerhalb der Lösungsstruktur einschließen, wie im folgenden Code dargestellt.

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "1.0.0.0",
      "includeClientSideAssets": true,
      "features": [{
        "title": "asset-deployment-webpart-client-side-solution",
        "description": "asset-deployment-webpart-client-side-solution",
        "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ],
          "elementFiles":[
            "schema.xml"
          ]
        }
      }]
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }
  ```

Beachten Sie Folgendes zu den hinzugefügten JSON-Definitionen:

* Technisch gesehen können mehrere Features in dem Paket vorhanden sein, da es sich bei **Features** um eine Sammlung handelt. Dies wird aber nicht empfohlen.

* Auf **elements.xml** wird unter „elementManifests“ verwiesen, sodass es für die tatsächliche Feature-XML-Struktur ordnungsgemäß als Elementmanifestdatei verpackt wird.

* In der Definition können mehrere element.xml-Dateien vorhanden sein, und diese würden in der Reihenfolge ausgeführt, in der sie in der JSON-Definition erwähnt werden. Im Allgemeinen sollten Sie die Verwendung mehrerer „element.xml“-Dateien vermeiden, da dadurch eine unnötige Komplexität entsteht. Sie können alle erforderlichen Ressourcen in einer einzigen „element.xml“-Datei definieren.

## <a name="deploy-and-test-asset-provisioning"></a>Bereitstellen und Testen der Bereitstellung von Ressourcen

Jetzt sind Sie bereit, die Lösung in SharePoint bereitzustellen. Da wir Ressourcen direkt auf SharePoint-Websites bereitstellen, wenn die Lösung installiert wird, können Sie die Funktion in der lokalen oder Online-Workbench nicht testen.

1. Geben Sie im Konsolenfenster den folgenden Befehl ein, um Ihre clientseitige Lösung, die das Webpart enthält, zu verpacken, damit die grundlegende Struktur für das Verpacken vorbereitet wird:

  ```
  gulp bundle
  ```

2. Führen Sie den folgenden Befehl aus, um das Lösungspaket zu erstellen:

  ```
  gulp package-solution
  ```

  Der Befehl erstellt das Paket im `sharepoint/solution`-Ordner:

  ```
  asset-deployment-webpart.sppkg
  ```

3. Vor dem Testen des Pakets in SharePoint sehen wir uns schnell die Standardstrukturen an, die für das Paket um die definierten Featureframeworkelemente herum erstellt wurden. Wechseln Sie zurück zur Seite von Visual Studio Code, und erweitern Sie den Ordner `sharepoint/solution/debug`, der die raw.xml-Strukturen enthält, die in das tatsächliche **sppkg**-Paket eingeschlossen werden sollen.

  ![Screenshot, in dem der Debugordner unter dem SharePoint-Ordner in der Lösungsstruktur angezeigt wird](../../../images/tutorial-feature-solution-debug-folder.png)

4. Stellen Sie das Paket, das generiert wurde, im App-Katalog bereit. Wechseln Sie zum App-Katalog des Mandanten.

5. Laden Sie das Paket „asset-deployment-webpart.sppkg“, das sich im Ordner `sharepoint/solution` befindet, in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop. In SharePoint wird ein Dialogfeld angezeigt, und Sie werden aufgefordert, der clientseitigen Lösung, die bereitgestellt werden soll, zu vertrauen.

  ![Dialogfeld für die Vertrauensstellung für die Bereitstellung des Lösungspakets](../../../images/tutorial-feature-solution-trust-app-catalog.png)

  > [!NOTE]
  > SharePoint überprüft das veröffentlichte Paket, wenn es bereitgestellt wird, und Sie sehen nur das Dialogfeld für die Vertrauensstellung, wenn das Paket bereitgestellt werden kann. Sie können auch den Status dieser Überprüfung in der Spalte „Gültiges App-Paket“ im App-Katalog anzeigen.

6. Wechseln Sie zu der Website, auf der Sie die Bereitstellung der SharePoint-Ressource testen möchten. Dies könnte eine Websitesammlung im Mandanten sein, auf dem Sie dieses Lösungspaket bereitgestellt haben.

7. Klicken Sie auf der oberen Navigationsleiste rechts auf das Zahnradsymbol und anschließend auf **App hinzufügen**, um Ihre Apps-Seite aufzurufen.

8. Geben Sie in das **Suchfeld** die Zeichenfolge **deployment** ein, und drücken Sie die **EINGABETASTE**, um Ihre Apps zu filtern.

  ![Suchen nach der App auf der Website](../../../images/tutorial-feature-solution-add-app.png)

9. Wählen Sie die App **asset-deployment-webpart-client-side-solution** aus, um die App auf der Website zu installieren. Wenn die Installation abgeschlossen ist, aktualisieren Sie die Seite, indem Sie **F5** drücken. Beachten Sie, dass die benutzerdefinierte **SPFx-Liste** auf der Website als Teil der Lösungspaketbereitstellung bereitgestellt wurde.

  ![Neue SPFx-Liste und App, die auf der Websiteinhaltsseite sichtbar sind, nachdem die Lösung bereitgestellt wurde](../../../images/tutorial-feature-solution-provision-app.png)


10. Klicken Sie auf **SPFx-Liste**, um zu der Liste zu wechseln. Beachten Sie, dass die benutzerdefinierten Felder **Betrag** und **Kostenstelle** automatisch in der Standardansicht der Liste angezeigt werden. 

  ![Standardmäßige Listenansicht für eine benutzerdefinierte Liste, in der standardmäßig zusätzliche Felder angezeigt werden](../../../images/tutorial-feature-solution-list-view.png)


## <a name="define-upgrade-actions-for-new-version"></a>Definieren von Upgradeaktionen für die neue Version

Immer dann, wenn Sie eine neue Version Ihrer SharePoint Framework-Lösung erstellen, gibt es möglicherweise erforderliche Änderungen an den bereitgestellten SharePoint-Ressourcen. Sie können die Unterstützung der Upgradeaktion für das Featureframework nutzen, wenn eine neue Version des Pakets bereitgestellt wird. 

SharePoint Framework-Lösungen unterstützen die folgenden Upgradeaktionsdefinitionen für das Featureframework:

* ApplyElementManifest
* AddContentTypeField

> [!TIP]
> Weitere Informationen zu den Upgradeaktionsdefinitionen für das Featureframework finden Sie im Artikel [Aktualisierungsverfahren für Add-Ins für SharePoint](../../../sp-add-ins/sharepoint-add-ins-update-process.md).

### <a name="to-add-a-new-elementxml-file-for-the-new-version"></a>So fügen Sie eine neue „element.xml“-Datei für die neue Version hinzu

1. Wechseln Sie zurück zu Ihrer Lösung in Visual Studio Code.

2. Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements-v2.xml**.

3. Kopieren Sie die folgende XML-Struktur in die Datei **elements-v2.xml**, in der eine neue SharePoint-Liste definiert wird, die mit dem Titel **Neue Liste** bereitgestellt werden soll.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">

      <ListInstance 
              FeatureId="00bfea71-de22-43b2-a848-c05709900100"
              Title="New List" 
              Description="New list provisioned from v2"
              TemplateType="100"
              Url="Lists/NewList">
      </ListInstance>

  </Elements>
  ```

4. Außerdem wird eine Definition für die tatsächlichen Upgradeaktionen für das Featureframework benötigten, erstellen Sie daher eine neue Datei innerhalb des Ordners **Sharepoint\Ressourcen** mit dem Namen **upgrade-actions-v2.xml**

5. Kopieren Sie die folgende XML-Struktur in **upgrade-actions-v2.xml**. Beachten Sie, dass der Feature-GUID-Verweis in dem Pfad auf den automatisch erstellten Ordner unter dem Ordner `sharepoint/solution/debug` verweist und basierend auf Ihrer Lösung aktualisiert werden muss. Diese GUID stimmt auch mit der GUID des Features überein, die wir in der Datei **-solution.json** definiert haben.

  ```xml
  <ApplyElementManifests>
        <ElementManifest Location="523fe887-ced5-4036-b564-8dad5c6c6e24\elements-v2.xml" />
  </ApplyElementManifests>

  ```

### <a name="to-deploy-the-new-version-to-sharepoint"></a>So stellen Sie die neue Version in SharePoint bereit

Als Nächstes müssen wir sowohl die Lösungsversion als auch die Featureversion aktualisieren, die für die Bereitstellung der Ressource verantwortlich ist.

> [!IMPORTANT]
> Die Lösungsversion gibt für SharePoint an, dass eine neue Version der SharePoint Framework-Lösung zur Verfügung steht. Durch die Featureversion wird sichergestellt, dass die Upgradeaktionen entsprechend ausgeführt werden, wenn das Lösungspaket auf den vorhandenen Websites aktualisiert wird.

1. Öffnen Sie **package-solution.json** im Ordner „config“, und aktualisieren Sie die Versionswerte sowohl für die Lösung als auch für das Feature auf „2.0.0.0“. 

2. Außerdem müssen**elements-v2.xml** im Abschnitt „elementManifest“ und das „upgradeActions“-Element in einen Zeiger auf die soeben erstelle **upgrade-actions-v2.xml**-Datei eingeschlossen werden.

  Nachfolgend sehen Sie eine vollständige **package-solution.json**-Datei mit den erforderlichen Änderungen. Beachten Sie, dass die Bezeichner für Ihre Lösung etwas anders aussehen könnten, konzentrieren Sie sich daher nur auf das Hinzufügen der fehlenden Teile.

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "2.0.0.0",
      "includeClientSideAssets": true,
      "features": [{
        "title": "asset-deployment-webpart-client-side-solution",
        "description": "asset-deployment-webpart-client-side-solution",
        "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
        "version": "2.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml",
            "elements-v2.xml"
          ],
          "elementFiles":[
            "schema.xml"
          ],
          "upgradeActions":[
            "upgrade-actions-v2.xml"
          ]
        }
      }]
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }
  ```

  > [!IMPORTANT]
  > Beachten Sie, dass auch das **elements-v2.xml**-Element unter dem Abschnitt „elementManifest“ eingeschlossen wurde. Dadurch wird sichergestellt, dass das Endergebnis bei Installation dieses Pakets auf einer bereinigten Website als Version 2.0 mit den aktualisierten Paketen übereinstimmt.

3. Geben Sie im Konsolenfenster den folgenden Befehl ein, um Ihre clientseitige Lösung, die das Webpart enthält, erneut zu verpacken, damit die grundlegende Struktur für das Verpacken vorbereitet wird:

  ```
  gulp bundle
  ```
4. Führen Sie den folgenden Befehl aus, um das Lösungspaket zu erstellen:

  ```
  gulp package-solution
  ```

  Der Befehl erstellt eine neue Version des Lösungspakets im Ordner `sharepoint/solution`. Beachten Sie, dass Sie am Ordner `sharepoint/solution/debug` leicht erkennen können, dass die aktualisierten XML-Dateien im Lösungspaket enthalten sind.

5. Als Nächstes müssen Sie die neue Version, die generiert wurde, im App-Katalog bereitstellen. Wechseln Sie zum App-Katalog des Mandanten.

6. Laden Sie das Paket „asset-deployment-webpart.sppkg“, das sich im Ordner `sharepoint/solution` befindet, in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop. Sie werden von SharePoint aufgefordert, zu bestätigen, dass die vorhandene Version überschrieben werden soll.

  ![Ersetzen der Frage aus dem App-Katalog](../../../images/tutorial-feature-solution-override-sppkg.png)

7. Klicken Sie auf **Ersetzen**, um ein Update auf die neueste Version im App-Katalog durchzuführen.

8. Klicken Sie auf **Bereitstellen**, um auch der neuesten Version *zu vertrauen*. 

  Beachten Sie, dass die Spalte „App-Version“ für die **asset-deployment-webpart-client-side-solution** nun auf „2.0.0.0“ aktualisiert wurde.

  ![Nahaufnahme der Lösungszeile im App-Katalog mit aktualisierter Versionsnummer](../../../images/tutorial-feature-solution-version-2.png)

### <a name="to-update-an-existing-instance-in-the-site"></a>So aktualisieren Sie die vorhandene Instanz auf der Website

Da das Paket nun im App-Katalog aktualisiert wurde, können wir zur tatsächlichen SharePoint-Inhaltswebsite wechseln und das Upgrade für die vorhandene Instanz durchführen.

1. Wechseln zu der Website, auf der Sie die erste Version der SharePoint Framework-Lösung bereitgestellt haben.

2. Wechseln Sie auf die Seite **Websiteinhalte**.

3. Wählen der Option **Details** aus dem Kontextmenü der Lösung **asset-deployment-webpart-client-side-solution**

  ![Kontextmenü des vorhandenen Pakets auf der Website](../../../images/tutorial-feature-solution-hover-menu.png)

  Dadurch werden die aktuellen Details zu der installierten SharePoint Framework-Lösung vorgestellt. Auf dieser Seite wird nun der Text als *Es ist eine neue Version dieser App verfügbar.* angezeigt, um anzugeben, dass eine neue Version verfügbar ist.

  ![Kontextmenü des vorhandenen Pakets auf der Website](../../../images/tutorial-feature-solution-app-details.png)

4. Klicken Sie auf die Schaltfläche **HERUNTERLADEN**, um den Updateprozess für das Paket zu starten.

  ![App-Status wurde zu Updates auf der Seite der Websiteinhalte aktualisiert](../../../images/tutorial-feature-solution-updating-app.png)

  Wenn Sie zur klassischen Umgebung wechseln, sehen Sie weitere Details zur tatsächlichen Upgrade-Aktion, die für die SharePoint-Frameworklösung angewendet wird. 

  ![App-Status wurde zu Updates auf der Seite der Websiteinhalte aktualisiert](../../../images/tutorial-feature-solution-updating-app-classic.png)

  > [!NOTE]
  > Da das SharePoint-Framework dieselbe App-Struktur wie SharePoint-Add-Ins verwendet, weist der Status für das Upgrade auf ein Update für ein Add-In oder eine App hin. 

  Das Update kann eine Weile dauern, wenn der Lösungsstatus jedoch wieder zu „normal“ wechselt, können Sie auf **F5** klicken, um die Seite mit den Websiteinhalten zu aktualisieren, um zu bestätigen, dass die  *neue Liste* erfolgreich als Teil des Updateprozesses bereitgestellt wurde.

  ![Die Seite mit den Websiteinhalten mit einer zusätzlichen neuen Liste, die erstellt wird](../../../images/tutorial-feature-solution-new-list.png)

  Wir haben jetzt diese Instanz erfolgreich auf die neueste Version aktualisiert. Diese Option des Featureframeworks für die SharePoint-Ressourcenbereitstellung ist nahezu identisch wie beim SharePoint-Add-In-Modell. Der wichtigste Unterschied besteht darin, dass die Ressourcen direkt auf der normalen SharePoint-Website bereitgestellt werden, da es das Konzept „App-/Add-In-Web“ bei SharePoint Framework-Lösungen nicht gibt.

> [!NOTE]
> Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues). Vielen Dank im Voraus für Ihr Feedback.

## <a name="see-also"></a>Weitere Artikel

- [Bereitstellen von SharePoint-Elementen mit Ihrem Lösungspaket](../../toolchain/provision-sharepoint-assets.md)
- [Beispiellösung - Bereitstellen von SharePoint-Ressourcen als Teil des SPFx-Pakets](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-feature-framework)
