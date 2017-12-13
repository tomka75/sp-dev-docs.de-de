# <a name="migrating-from-jslink-to-sharepoint-framework-extensions"></a>Migrieren von JSLink zu SharePoint-Framework-Erweiterungen

Seit der Microsoft SharePoint-Version 2013 nutzen die meisten Unternehmenslösungen, die auf Office 365 und SharePoint Online aufbauen, die _JSLink_-Eigenschaft von Feldern und Listenansichten, um das Rendern von Feldern anzupassen. Heute stehen die meisten dieser Anpassungsmöglichkeiten in der „modernen“ Benutzeroberfläche von SharePoint Online jedoch nicht mehr zur Verfügung. Mit den neuen SharePoint-Framework-Erweiterungen können Sie fast die gleichen Funktionen auf der modernen Benutzeroberfläche bereitstellen. In diesem Lernprogramm erfahren Sie, wie Sie die alten, klassischen Anpassungen zu dem neuen Modell basierend auf SharePoint-Framework-Erweiterungen migrieren können.

> [!IMPORTANT]
> Das bedeutet nicht das Ende der Unterstützung für die klassische Benutzeroberfläche, es stehen weiterhin sowohl die klassische als auch die moderne Oberfläche zur Verfügung.

_**Gilt für: **SharePoint Online_

## <a name="understanding-sharepoint-framework-extensions"></a>Grundlegendes zu SharePoint-Framework-Erweiterungen
<a name="spfxExtensions"> </a> Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:

* **Application Customizer**: Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden. Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.
* **Command Set**: Benutzerdefinierte ECB-Menüelemente oder benutzerdefinierte Schaltflächen können der Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek hinzugefügt werden. Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.
* **Field Customizer**: Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.

Wie bereits aus der obigen Beschreibung hervorgeht, ist die „Field Customizer“-Erweiterung die nützlichste in diesem Kontext.

> [!NOTE]
> Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen finden Sie im Artikel [Übersicht über SharePoint-Framework-Erweiterungen](https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/overview-extensions).

## <a name="migrating-a-jslink-to-an-spfx-field-customizer"></a>Migrieren von JSLink zum Field Customizer von SPFx
<a name="FromJSLinktoFieldCustomizer"> </a> Nehmen Sie an, dass Sie sich in SharePoint Online befinden und Sie über eine benutzerdefinierte Liste mit einem angepassten Feld mit der Bezeichnung „Color“ verfügen, das den Typ _Choice_ hat und die folgenden Werte übernehmen kann: _Red_, _Green_, _Blue_, _Yellow_. Nehmen Sie dann an, dass Sie einen benutzerdefinierten Wert für die _JSLink_-Eigenschaft des Webparts haben, das die Listenansicht der benutzerdefinierten Liste rendert. Im folgenden Codeausschnitt sehen Sie den JavaScript-Code, der von der _JSLink_-Eigenschaft (_customColorRendering.js_) referenziert wird.

```JavaScript
// Define a namespace for the custom rendering code
var customJSLinkRendering = customJSLinkRendering || {}; 

// Define a function that declare the custom rendering rules for the target list view
customJSLinkRendering.CustomizeFieldRendering = function () {  

    // Define a custom object to configure the rendering template overrides
    var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = 
    { 
        // Declare the custom rendering function for the 'View' of field 'Color'
        'Color': 
        { 
            'View': customJSLinkRendering.RenderColorField 
        } 
    }; 

    // Register the custom rendering template
    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride); 
}; 

// Declare the custom rendering function for the 'View' of field 'Color'
customJSLinkRendering.RenderColorField = function (context)  
{ 
    var colorField = context.CurrentItem.Color; 

    // Declare a local variable to hold the output color
    var color = '';

    // Evaluate the values of the 'Color' field and render it accordingly
    switch (colorField)
    {
        case 'Red':
            color = 'red';
            break;
        case 'Green':
            color = 'green';
            break;
        case 'Blue':
            color = 'blue';
            break;
        case 'Yellow':
            color = 'yellow';
            break;
        default:
            color = 'white';
            break;
    }

    // Render the output for the 'Color' field
    return "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
}; 

// Invoke the custom rendering function
customJSLinkRendering.CustomizeFieldRendering();
```

Im folgenden Screenshot sehen Sie darüber hinaus, wie JSLink im Listenansicht-Webpart konfiguriert ist.

![Konfiguration der JSLink-Eigenschaft im Listenansicht-Webpart](../../../images/jslink-field-configuration.png)

Wenn Sie die JavaScript-Datei in die Bibliothek _Site Assets_ hochgeladen haben, kann der Wert für die _JSLink_-Eigenschaft _~site/SiteAssets/customColorRendering.js_ lauten.
Hier sehen Sie, aus Gründen der Vollständigkeit, wie das benutzerdefinierte Rendern der Liste funktioniert.

![Benutzerdefiniertes Rendern des Felds „Color“ in der benutzerdefinierten Liste](../../../images/jslink-field-output.png)

Wie Sie sehen können, rendern die Felder „Color“ auf der Elementebene ein farbiges Feld mit der ausgewählten Farbe.

> [!NOTE]
> Um diese Art von Lösung für eine „klassische“ Website bereitstellen zu können, können Sie letztendlich eine PnP-Bereitstellungsvorlage verwenden, die sowohl die Liste mit dem benutzerdefinierten Feld als auch gleichzeitig die JSLink-Eigenschaft bereitstellen kann.

Um die oben aufgeführte Lösung in das SharePoint-Framework zu migrieren, müssen Sie die folgenden Schritte ausführen.

### <a name="create-a-new-sharepoint-framework-solution"></a>Erstellen einer neuen SharePoint-Framework-Lösung
<a name="CreateFieldCustomizer"> </a> Nachdem Sie die Entwicklungsumgebung für SharePoint-Framework-Lösungen entsprechend den Anweisungen im Dokument [Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts](https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/set-up-your-development-environment) eingerichtet haben, können Sie mit dem Erstellen einer SharePoint-Framework-Erweiterung beginnen.

1. Öffnen Sie ein beliebiges Befehlszeilentool (PowerShell, CMD.EXE, Cmder usw.), erstellen Sie einen neuen Ordner für die Lösung (mit dem Namen _spfx-custom-field-extension_), und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:

```
yo @microsoft/sharepoint
```

Geben Sie bei Aufforderung durch das Tool Folgendes an:
* Bestätigen Sie den Standardnamen (_spfx-custom-field-extension_) für Ihre Lösung, und drücken Sie die EINGABETASTE.
* Wählen Sie „SharePoint Online only (latest)“, und drücken Sie die EINGABETASTE.
* Wählen Sie „Use the current folder“ aus, und drücken Sie die EINGABETASTE.
* Wählen Sie „N“, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.
* Wählen Sie „Extension“ als den zu erstellenden Typ von clientseitiger Komponente aus.
* Wählen Sie _Field Customizer_ als den zu erstellenden Erweiterungstyp aus.
* Geben Sie "CustomColorField" als Namen für Ihr benutzerdefiniertes Feld an.
* Wählen Sie aus, dass kein bestimmtes JavaScript-Framework verwendet werden soll, indem Sie die Option _Kein JavaScript-Framework_ aktivieren.

![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-custom-field-extension-yeoman.png)

An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die _CustomColorField_-Erweiterung. Dies kann einige Minuten dauern.

Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:

![Gerüsterstellung abgeschlossen](../../../images/spfx-custom-field-extension-yeoman-completed.png)

2. Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:

```
npm shrinkwrap
```

3. Starten Sie jetzt Visual Studio Code (oder einen anderen Code-Editor), und beginnen Sie mit der Entwicklung der Lösung. Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.

```
code .
```

### <a name="define-the-new-field-customizer-with-javascript"></a>Definieren des neuen Field Customizer mit JavaScript
<a name="DefineFieldCustomizerWithJavaScript"> </a>Um das gleiche Verhalten beim Rendern des benutzerdefinierten _JSLink_-Felds zu reproduzieren, müssen Sie einfach die gleiche Logik mit clientseitigem Code innerhalb der neuen SharePoint-Framework-Lösung implementieren. Gehen Sie hierzu wie folgt vor:

1. Öffnen Sie zunächst die Datei _CustomColorFieldFieldCustomizer.manifest.json_ im Ordner _src/extensions/customColorField_. Kopieren Sie den Wert der Eigenschaft _id_, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.

2. Öffnen Sie jetzt die Datei _CustomColorFieldFieldCustomizer.ts_, die sich in demselben Ordner wie zuvor befindet, und bearbeiten Sie den Inhalt entsprechend dem folgenden Codeauszug.

``` TypeScript
import { Log } from '@microsoft/sp-core-library';
import { override } from '@microsoft/decorators';
import {
  BaseFieldCustomizer,
  IFieldCustomizerCellEventParameters
} from '@microsoft/sp-listview-extensibility';

import * as strings from 'CustomColorFieldFieldCustomizerStrings';
import styles from './CustomColorFieldFieldCustomizer.module.scss';

/**
 * If your field customizer uses the ClientSideComponentProperties JSON input,
 * it will be deserialized into the BaseExtension.properties object.
 * You can define an interface to describe it.
 */
export interface ICustomColorFieldFieldCustomizerProperties {
  // This is an example; replace with your own property
  sampleText?: string;
}

const LOG_SOURCE: string = 'CustomColorFieldFieldCustomizer';

export default class CustomColorFieldFieldCustomizer
  extends BaseFieldCustomizer<ICustomColorFieldFieldCustomizerProperties> {

  @override
  public onInit(): Promise<void> {
    // Add your custom initialization to this method.  The framework will wait
    // for the returned promise to resolve before firing any BaseFieldCustomizer events.
    Log.info(LOG_SOURCE, 'Activated CustomColorFieldFieldCustomizer with properties:');
    Log.info(LOG_SOURCE, JSON.stringify(this.properties, undefined, 2));
    Log.info(LOG_SOURCE, `The following string should be equal: "CustomColorFieldFieldCustomizer" and "${strings.Title}"`);
    return Promise.resolve();
  }

  @override
  public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

    var colorField = event.fieldValue; 
    
    // Declare a local variable to hold the output color
    var color = '';

    // Evaluate the values of the 'Color' field and render it accordingly
    switch (colorField)
    {
        case 'Red':
            color = 'red';
            break;
        case 'Green':
            color = 'green';
            break;
        case 'Blue':
            color = 'blue';
            break;
        case 'Yellow':
            color = 'yellow';
            break;
        default:
            color = 'white';
            break;
    }
    
    // Render the output for the 'Color' field
    event.domElement.innerHTML = "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
  }

  @override
  public onDisposeCell(event: IFieldCustomizerCellEventParameters): void {
    // This method should be used to free any resources that were allocated during rendering.
    // For example, if your onRenderCell() called ReactDOM.render(), then you should
    // call ReactDOM.unmountComponentAtNode() here.
    super.onDisposeCell(event);
  }
}
```

Wie Sie sehen können, ist der Inhalt der Methode _onRenderCell_ fast identisch mit der vorherigen _RenderColorField_-Methode in der _JSLink_-Implementierung.
Die einzigen Unterschiede sind:
- Um den aktuellen Feldwert abzurufen, müssen Sie die _event.fieldValue_-Eigenschaft des Eingabearguments der _onRenderCell_-Methode lesen.
- Um den benutzerdefinierten HTML-Code zum Rendern des Felds zurückzugeben, müssen Sie der _innerHTML_-Eigenschaft des _event.domElement_-Objekts einen Wert zuweisen, der den Ausgabe-HTML-Container des Feldrenderings darstellt.

Abgesehen von diesen geringfügigen Änderungen können Sie fast den gesamten JavaScript-Code wie zuvor verwenden.

Die folgende Abbildung zeigt die resultierende Ausgabe.

![Der in einer modernen Liste gerenderte Field Customizer](../../../images/spfx-custom-field-extension-output.png)

### <a name="test-the-solution-in-debug-mode"></a>Testen der Lösung im Debugmodus
<a name="DebugFieldCustomizer"> </a> Sie können die Lösung jetzt im Debugmodus testen. 

1. Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus:

```
gulp serve --nobrowser
```

Der oben angegebene Befehl erstellt die Lösung und führt den lokalen Node.js-Server aus, um sie zu hosten.

2. Öffnen Sie nun Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Liste, die über ein benutzerdefiniertes Feld mit dem Namen _Color_ verfügt, und geben Sie _Choice_ mit den gleichen Werten wie zuvor ein (Red, Green, Blue, Yellow). Sie können letztendlich die Liste verwenden, die Sie in der „klassischen“ Website erstellt haben, und sie einfach in der „modernen“ Benutzerumgebung anzeigen. Hängen Sie jetzt die folgenden Abfragezeichenfolgeparameter an die _AllItems.aspx_-Seiten-URL an.

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Color":{"id":"c3070978-d85e-4298-8758-70b5b5933076"}}
```

In der oben aufgeführten Abfragezeichenfolge müssen Sie die GUID durch den _id_-Wert aus der Datei _CustomColorFieldFieldCustomizer.manifest.json_ ersetzen, den Sie zuvor gespeichert oder notiert haben. Der _Color_-Objektname bezieht sich auf das anzupassende Feld. Wenn Sie möchten, können Sie auch ein benutzerdefiniertes Konfigurationsobjekt, das im JSON-Format serialisiert ist, als einen zusätzlichen Parameter für die Field Customizer-Konstruktion bereitstellen.

Beachten Sie, dass beim Ausführen der Seitenanforderung ein Warnmeldungsfeld „Debugskripts zulassen?“ angezeigt wird, in dem Sie aus Sicherheitsgründen nach der Zustimmung für die Ausführung des Codes von Localhost gefragt werden. Wenn Sie lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.

### <a name="define-the-new-field-customizer-with-typescript"></a>Definieren des neuen Field Customizer mit TypeScript
<a name="DefineFieldCustomizerWithTypeScript"> </a> Sie können nun den JavaScript-Code durch TypeScript ersetzen, um die Vorteile von TypeScript optimal nutzen zu können.

1. Öffnen Sie die Datei _CustomColorFieldFieldCustomizer.module.scss_ im Ordner _src/extensions/customColorField_. Diese Datei, eine Sassy CSS, stellt den Stil der Benutzeroberfläche für den Field Customizer dar. Ersetzen Sie den Inhalt der SCSS-Datei durch den folgenden:

``` SCSS
.CustomColorField {
  .cell {
    float: left;
    width: 20px; 
    height: 20px; 
    margin: 5px; 
    border: 1px solid rgba(0,0,0,.2);
  }

  .cellRed {
    background: red;
  }

  .cellGreen {
    background: green;
  }

  .cellBlue {
    background: blue;
  }

  .cellYellow {
    background: yellow;
  }

  .cellWhite {
    background: white;
  }
}
```

2. Ersetzen Sie die Implementierung der _onRenderCell_-Methode durch den folgenden Codeausschnitt.

``` TypeScript
@override
public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

// Read the current field value
let colorField: String = event.fieldValue; 

// Add the main style to the field container element
event.domElement.classList.add(styles.CustomColorField);

// Get a reference to the output HTML
let fieldHtml: HTMLDivElement = event.domElement.firstChild as HTMLDivElement;

// Add the standard style
fieldHtml.classList.add(styles.cell);

// Add the colored style
switch(colorField)
{
    case "Red":
    fieldHtml.classList.add(styles.cellRed);
    break;
    case "Green":
    fieldHtml.classList.add(styles.cellGreen);
    break;
    case "Blue":
    fieldHtml.classList.add(styles.cellBlue);
    break;
    case "Yellow":
    fieldHtml.classList.add(styles.cellYellow);
    break;
    default:
    fieldHtml.classList.add(styles.cellWhite);
    break;
}
}
```

Beachten Sie, dass die neue Methodenimplementierung einen vollständig typisierten Ansatz verwendet und die CSS-Klasse _cell_ dem untergeordneten _DIV_-Element des aktuellen Feldelements zusammen mit einer anderen CSS-Klasse zuweist, um die Zielfarbe von _DIV_ basierend auf dem derzeit ausgewählten Feldwert zu definieren.

3. Führen Sie den Field Customizer noch einmal im Debugmodus aus, und sehen Sie sich das Ergebnis an.

### <a name="package-and-host-the-solution"></a>Packen und Hosten der Lösung
<a name="PackageAndHostCommandSet"> </a> Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.
Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature Frameworkdatei deklarieren, um die Erweiterung bereitzustellen.

#### <a name="review-feature-framework-elements"></a>Überprüfen von Feature-Framework-Elementen
Öffnen Sie im Code-Editor den Unterordner _/sharepoint/assets_ der Lösung, und bearbeiten Sie die Datei _elements.xml_.
Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{40475661-efaf-447a-a220-c992b20ec1c3}"
            Name="SPFxColor"
            DisplayName="Color"
            Title="Color"
            Type="Choice"
            Required="FALSE"
            Group="SPFx Columns"
            ClientSideComponentId="c3070978-d85e-4298-8758-70b5b5933076">
    </Field>
</Elements>
```

Wie Sie sehen, ähnelt sie der SharePoint-Feature-Framework-Datei. Sie definiert ein benutzerdefiniertes _Field_-Element mit dem Feldtyp _Choice_, der das _ClientSideComponentId_-Attribut zum Veweisen auf die _id_ des Field Customizer verwendet. Es könnte auch ein _ClientSideComponentProperties_-Attribut vorhanden sein, um die für die Erweiterung erforderlichen benutzerdefinierten Konfigurationseigenschaften zu konfigurieren.

Öffnen Sie jetzt die Datei _package-solution.json_ im Lösungsordner _/config_. In der Datei können Sie sehen, dass ein Verweis auf die _elements.xml_ im Abschnitt _assets_ vorhanden ist.

```JSON
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "spfx-custom-field-extension-client-side-solution",
    "id": "ab0fbbf8-01ba-4633-8498-46cfd5652619",
    "version": "1.0.0.0",
    "features": [
      {
        "title": "Application Extension - Deployment of custom action.",
        "description": "Deploys a custom action with ClientSideComponentId association",
        "id": "090dc976-878d-44fe-8f8e-ac603d094aa1",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ]
        }
      }
    ]
  },
  "paths": {
    "zippedPackage": "solution/spfx-custom-field-extension.sppkg"
  }
}
```

#### <a name="enable-the-cdn-in-your-office-365-tenant"></a>Aktivieren des CDN im Office 365-Mandanten
Sie müssen die Erweiterung nun in einer Hostingumgebung hosten. Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.

1. Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.

2. Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:
    
    ```
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen: 
    
    ```
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. Aktivieren Sie öffentliche CDNs im Mandanten:
    
    ```
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen. Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.

5. Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.

6. Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens _CDN_, und fügen Sie ihr einen Ordner namens _customcolorfield_ hinzu.
    
7. Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu. In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen _cdn_ als ein CDN-Ursprung.
    
    ```
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:
    
    ```
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist. Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie mit dem Bereitstellen der Erweiterung fortfahren, die anschließend im Ursprung gehostet wird. 

![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden. Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin. 

#### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a>Aktualisieren der Lösungseinstellungen und Veröffentlichen im CDN
Sie müssen die Lösung jetzt aktualisieren, damit Sie das gerade erstellte CDN als Hostingumgebung verwenden können. Sie müssen das Lösungsbundle im CDN veröffentlichen. Gehen Sie hierzu wie nachfolgend beschrieben vor.

1. Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderliche URL-Updates auszuführen.
    
2. Aktualisieren Sie die Datei _write-manifests.json_ (im Ordner _config_) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist. Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten. Die CDN-URL hat folgendes Format:
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-custom-field-extension-manifest.png)

3. Speichern Sie Ihre Änderungen.

4. Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken. Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei _write-manifests.json_ angegebenen CDN-URL. Die Ausgabe dieses Befehls finden Sie im Ordner _./temp/deploy_. Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert. 
    
    ```
    gulp bundle --ship
    ```
    
5. Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen. Dieser Befehl erstellt ein Paket namens _spfx-custom-field-extension.sppkg_ im Ordner _sharepoint/solution_ und bereitet außerdem die Ressourcen im Ordner _temp/deploy_ für die Bereitstellung im CDN vor.
    
    ```
    gulp package-solution --ship
    ```
    
6. Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche _Bereitstellen_.

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-custom-field-extension-address.png)

7. Laden Sie die Dateien im Ordner _temp/deploy_ in den Ordner _CDN/customcolorfield_ hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.

### <a name="install-and-run-the-solution"></a>Installieren und Ausführen der Lösung
<a name="InstallFieldCustomizer"> </a> Sie können die Lösung jetzt auf jeder modernen Zielwebsite installieren.

1. Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.

2. Navigieren Sie zur Seite _Websiteinhalte_, und wählen Sie _App_, um eine neue App hinzuzufügen.

3. Wählen Sie zum Installieren einer neuen App _Aus Ihrer Organisation_, um die im _AppCatalog_ verfügbaren Lösungen zu durchsuchen.

4. Wählen Sie die Lösung mit dem Namen _spfx-custom-field-extension-client-side-solution_, und installieren Sie sie auf der Zielwebsite.

    ![Hinzufügen einer App-Benutzeroberfläche, um die Lösung einer Website hinzuzufügen](../../../images/spfx-custom-field-extension-add-app.png)

5. Sobald die Anwendung installiert wurde, erstellen Sie eine neue benutzerdefinierte Liste, bearbeiten Sie die Listeneinstellungen, und fügen Sie eine neue Spalte aus den bereits vorhandenen Websitespalten hinzu. Wählen Sie die Spaltengruppe _SPFx Columns_, und fügen Sie das Feld _Color_ hinzu.

![Der Field Customizer in Aktion](../../../images/spfx-custom-field-extension-add-field.png)

6. Bearbeiten Sie das gerade hinzugefügte Feld, und konfigurieren Sie einige Farbwerte (z. B. Red, Green, Blue, Yellow). Speichern Sie die Feldeinstellungen anschließend.

7. Fügen Sie der Liste einige Elemente hinzu, und sehen Sie sich die Ausgabe in der Listenansicht an. Sie sollte in etwa wie im folgenden Screenshot aussehen.

![Der Field Customizer in Aktion](../../../images/spfx-custom-field-extension-final-output.png)

Sie können nun den Field Customizer nutzen, den Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.
