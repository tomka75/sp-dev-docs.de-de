# <a name="migrating-from-edit-control-block-ecb-menu-item-to-sharepoint-framework-extensions"></a>Migrieren vom Edit Control Block-Menüelement (ECB) zu SharePoint-Framework-Erweiterungen

In den letzten Jahren haben die meisten Unternehmenslösungen, die auf Office 365 und SharePoint Online aufbauen, die Funktion _CustomAction_ des SharePoint-Feature-Framework genutzt, um die Benutzeroberfläche von Seiten zu erweitern. Heute stehen die meisten dieser Anpassungsmöglichkeiten in der „modernen“ Benutzeroberfläche von SharePoint Online jedoch nicht mehr zur Verfügung. Mit den neuen SharePoint-Framework-Erweiterungen können Sie jedoch fast die gleichen Funktionen auch in der modernen Benutzeroberfläche bereitstellen. In diesem Lernprogramm erfahren Sie, wie Sie von den älteren „klassischen“ Anpassungen zu dem neuen Modell migrieren, das auf SharePoint-Framework-Erweiterungen basiert.

> [!IMPORTANT]
> Das bedeutet nicht das Ende der Unterstützung für die klassische Benutzeroberfläche, es stehen weiterhin sowohl die klassische als auch die moderne Oberfläche zur Verfügung.

_**Gilt für: **SharePoint Online_

## <a name="understanding-sharepoint-framework-extensions"></a>Grundlegendes zu SharePoint-Framework-Erweiterungen
<a name="spfxExtensions"> </a> Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:

* **Application Customizer**: Erweiterung der systemeigenen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clienseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden. Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.
* **Command Set**: Benutzerdefinierte ECB-Menüelemente oder benutzerdefinierte Schaltflächen können der Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek hinzugefügt werden. Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.
* **Field Customizer**: Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.

Wie bereits aus der obigen Beschreibung hervorgeht, ist die „Command Set“-Erweiterung die nützlichste in diesem Kontext.

> [!NOTE]
> Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen finden Sie im Artikel [Übersicht über SharePoint-Framework-Erweiterungen](https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/overview-extensions).

## <a name="migrating-a-ecb-to-an-spfx-command-set"></a>Migrieren eines ECB zu einem Command Set von SPFx
<a name="FromECBtoCommandSet"> </a> Angenommen Sie verfügen über eine _CustomAction_ in SharePoint Online, damit für Dokumente in einer Bibliothek ein benutzerdefiniertes ECB-Menü verfügbar ist. Die Funktion des ECB-Menüelements besteht darin, eine benutzerdefinierte Seite zu öffnen, auf der die Listen-ID und die Listenelement-ID des aktuell ausgewählten Elements in der Abfragezeichenfolge der Zielseite bereitgestellt wird.
Im folgenden Codeausschnitt ist der XML-Code enthalten, der _CustomAction_ mithilfe des SharePoint-Feature-Frameworks definiert.

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="OpenDetailsPageWithItemReference"
                Title="Show Details"
                Description="Opens a new page with further details about the currently selected item"
                Sequence="1001"
                RegistrationType="List"
                RegistrationId="101"                
                Location="EditControlBlock">
    <UrlAction Url="ShowDetails.aspx?ID={ItemId}&amp;List={ListId}" />
  </CustomAction>
</Elements>
```

Wie Sie sehen können, definiert die Funktionselementdatei ein Element des Typs _CustomAction_, um ein neues Element am Ort von _EditControlBlock_ (d. h. ECB) für ein beliebiges Dokument in einer beliebigen Bibliothek hinzuzufügen (_ RegistrationType_ ist _List_ und _RegistrationId_ ist _101_).

In der folgenden Abbildung sehen Sie die Ausgabe der vorherigen benutzerdefinierten Aktion in der Listenansicht einer Bibliothek.

![Die benutzerdefinierte Fußzeile auf einer klassischen Seite](../../../images/ecb-menu-classic-output.png)

Beachten Sie, dass das benutzerdefinierte ECB-Element des SharePoint-Feature-Framework auch in einer „modernen“ Liste funktioniert. Tatsächlich funktioniert eine benutzerdefinierte Listenaktion auch in „modernen“ Listen, solange Sie keinen JavaScript-Code verwenden.

Um die oben aufgeführte Lösung in das SharePoint-Framework zu migrieren, müssen Sie die folgenden Schritte ausführen.

### <a name="create-a-new-sharepoint-framework-solution"></a>Erstellen einer neuen SharePoint-Framework-Lösung
<a name="CreateCommandSet"> </a> Nachdem Sie die Entwicklungsumgebung für SharePoint-Framework-Lösungen entsprechend den Anweisungen im Dokument [Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts](https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/set-up-your-development-environment) eingerichtet haben, können Sie mit dem Erstellen einer SharePoint-Framework-Erweiterung beginnen.

1. Öffnen Sie ein beliebiges Befehlszeilentool (PowerShell, CMD.EXE, Cmder usw.), erstellen Sie einen neuen Ordner für die Lösung (mit dem Namen _spfx-ecb-extension_), und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:

```
yo @microsoft/sharepoint
```

Geben Sie bei Aufforderung durch das Tool Folgendes an:
* Bestätigen Sie den Standardnamen (_spfx-ecb-extension_) für Ihre Lösung, und drücken Sie die EINGABETASTE.
* Wählen Sie „SharePoint Online only (latest)“, und drücken Sie die EINGABETASTE.
* Wählen Sie „Use the current folder“ aus, und drücken Sie die EINGABETASTE.
* Wählen Sie „N“, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.
* Wählen Sie „Extension“ als den zu erstellenden Typ von clientseitiger Komponente aus.
* Wählen Sie _ListView Command Set_ als den zu erstellenden Typ von Erweiterung aus.
* Geben Sie „CustomECB“ als Namen für Ihr Command Set an.

![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-ecb-extension-yeoman.png)

An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die _CustomFooter_-Erweiterung. Das kann einige Minuten dauern.

Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:

![Gerüsterstellung abgeschlossen](../../../images/spfx-ecb-extension-yeoman-completed.png)

2. Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:

```
npm shrinkwrap
```

3. Starten Sie jetzt Visual Studio Code (oder einen anderen Code-Editor), und beginnen Sie mit der Entwicklung der Lösung. Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.

```
code .
```

### <a name="define-the-new-ecb-item"></a>Definieren des neuen ECB-Elements
<a name="DefineCommandSetECB"> </a> Um das gleiche Verhalten des ECB-Menüelements zu reproduzieren, das mit dem SharePoint-Feature-Framework erstellt wurde, müssen Sie einfach die gleiche Logik mit clientseitigem Code innerhalb der neuen SharePoint-Framework-Lösung implementieren. Gehen Sie hierzu wie folgt vor:

1. Öffnen Sie zunächst die Datei _CustomEcbCommandSet.manifest.json_ im Ordner _src/extensions/customEcb_. Kopieren Sie den Wert der Eigenschaft _id_, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.

2. Bearbeiten Sie in derselben Datei das Array von _items_ im unteren Bereich der Datei, um einen einzelnen Befehl für das Command Set zu definieren. Rufen Sie den Befehl _ShowDetails_ auf, und geben Sie einen Titel sowie einen Befehlstyp ein. Im folgenden Screenshot sehen Sie, wie die Manifestdatei aussehen soll.

![Die Manifestdatei für das benutzerdefinierte Command Set](../../../images/spfx-ecb-extension-manifest.png)

3. Öffnen Sie jetzt die Datei _CustomEcbCommandSet.ts_, die sich in demselben Ordner wie zuvor befindet, und bearbeiten Sie den Inhalt entsprechend dem folgenden Codeauszug.

``` TypeScript
import { Guid } from '@microsoft/sp-core-library';
import { override } from '@microsoft/decorators';
import {
  BaseListViewCommandSet,
  Command,
  IListViewCommandSetListViewUpdatedParameters,
  IListViewCommandSetExecuteEventParameters
} from '@microsoft/sp-listview-extensibility';
import { Dialog } from '@microsoft/sp-dialog';

import * as strings from 'CustomEcbCommandSetStrings';

export interface ICustomEcbCommandSetProperties {
  targetUrl: string;
}

export default class CustomEcbCommandSet extends BaseListViewCommandSet<ICustomEcbCommandSetProperties> {

  @override
  public onInit(): Promise<void> {
    return Promise.resolve();
  }

  @override
  public onListViewUpdated(event: IListViewCommandSetListViewUpdatedParameters): void {
    const compareOneCommand: Command = this.tryGetCommand('ShowDetails');
    if (compareOneCommand) {
      // This command should be hidden unless exactly one row is selected.
      compareOneCommand.visible = event.selectedRows.length === 1;
    }
  }

  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.itemId) {
      case 'ShowDetails':

        const itemId: number = event.selectedRows[0].getValueByName("ID");
        const listId: Guid = this.context.pageContext.list.id;

        window.location.replace(`${this.properties.targetUrl}?ID=${itemId}&List=${listId}`);

        break;
      default:
        throw new Error('Unknown command');
    }
  }
}
```

Beachten Sie die _import_-Anweisung ganz am Anfang der Datei, die den _Guid_-Typ referenziert und die ID der aktuellen Liste beinhaltet. Darüber hinaus deklariert die Schnittstelle _ICustomEcbCommandSetProperties_ eine einzelne Eigenschaft mit der Bezeichnung _targetUrl_, die verwendet werden kann, um die URL der Zielseite anzugeben, die beim Klicken auf das ECB-Menüelement geöffnet werden soll.
Darüber hinaus behandelt die Überschreibung der _onExecute_-Methode die Ausführung der benutzerdefinierten Aktion. Beachten Sie den Codeauszug, der die ID des aktuell ausgewählten Elements aus dem _event_-Argument sowie die ID der Quellliste aus dem _PageContext_-Objekt abruft.
Beachten Sie schließlich auch die Überschreiben der _OnListViewUpdated_-Methode, die standardmäßig den Befehl _ShowDetails_ nur dann aktivierte, wenn ein einzelnes Element ausgewählt wird.

Die Umleitung an die Ziel-URL erfolgt durch die Verwendung von klassischem JavaScript-Code und der Funktion _window.location.replace_. Sie können natürlich jede Art von TypeScript-Code in die _OnExecute_-Methode schreiben. Um hier nur ein Beispiel zu nennen, können Sie das Dialog-Framework des SharePoint-Frameworks verwenden, um ein neues Dialogfeld zu öffnen und mit den Endbenutzern zu interagieren.

> [!NOTE]
> Weitere Informationen zum Dialog-Framework von SharePoint-Framework finden Sie im Dokument [Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint Framework Extensions](https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/guidance/using-custom-dialogs-with-spfx).

Die folgende Abbildung zeigt die resultierende Ausgabe.

![Das Command Set von ECB, gerendert in einer „modernen“ Liste](../../../images/spfx-ecb-extension-output.png)

### <a name="test-the-solution-in-debug-mode"></a>Testen der Lösung im Debugmodus
<a name="DebugCommandSet"> </a> Sie können die Lösung jetzt im Debugmodus testen. 

1. Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus:

```
gulp serve --nobrowser
```

Der oben angegebene Befehl erstellt die Lösung und führt den lokalen Node.js-Server aus, um sie zu hosten.

2. Öffnen Sie jetzt Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Bibliothek einer beliebigen „modernen“ Teamwebsite. Hängen Sie jetzt die folgenden Abfragezeichenfolgeparameter an die _AllItems.aspx_-Seiten-URL an.

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6c5b8ee9-43ba-4cdf-a106-04857c8307be":{"location":"ClientSideExtension.ListViewCommandSet.ContextMenu","properties":{"targetUrl":"ShowDetail.aspx"}}}
```

In der oben aufgeführten Abfragezeichenfolge müssen Sie die GUID durch den _id_-Wert aus der Datei _CustomEcbCommandSet.manifest.json_ ersetzen, den Sie gespeichert und aufbewahrt haben. Es ist außerdem eine _location_-Eigenschaft vorhanden, die den Wert von _ClientSideExtension.ListViewCommandSet.ContextMenu_ annimmt. Dieser weist SPFx an, das Command Set als ein ECB-Menüelement zu rendern. Nachfolgend sind alle für die _location_-Eigenschaft verfügbaren Optionen aufgeführt:
* **ClientSideExtension.ListViewCommandSet.ContextMenu:** im Kontextmenü der Elemente
* **ClientSideExtension.ListViewCommandSet.CommandBar:** im oberen Befehlssatzmenü in einer Liste oder Bibliothek
* **ClientSideExtension.ListViewCommandSet:** sowohl im Kontextmenü als auch auf der Befehlsleiste (entspricht SPUserCustomAction.Location="CommandUI.Ribbon")

Schließlich befindet sich in der Abfragezeichenfolge auch noch die Eigenschaft _properties_, die die JSON-Serialisierung eines Objekts vom Typ _ICustomEcbCommandSetProperties_ darstellt. Dies ist der Typ der benutzerdefinierten Eigenschaften, die das benutzerdefinierte Command Set zum Rendern anfordert.

Beachten Sie, dass beim Ausführen der Seitenanforderung eine Warnmeldung angezeigt wird, ob Sie Debugskripts zulassen möchten. Sie müssen aus Sicherheitsgründen bestätigen, dass Code von localhost ausgeführt werden darf. Wenn Sie lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.

### <a name="package-and-host-the-solution"></a>Packen und Hosten der Lösung
<a name="PackageAndHostCommandSet"> </a> Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.
Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature Frameworkdatei deklarieren, um die Erweiterung bereitzustellen.

#### <a name="review-feature-framework-elements"></a>Überprüfen von Feature-Framework-Elementen
Öffnen Sie im Code-Editor den Unterordner _/sharepoint/assets_ der Lösung, und bearbeiten Sie die Datei _elements.xml_.
Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <CustomAction
        Title="CustomEcb"
        RegistrationId="101"
        RegistrationType="List"
        Location="ClientSideExtension.ListViewCommandSet.ContextMenu"
        ClientSideComponentId="6c5b8ee9-43ba-4cdf-a106-04857c8307be"
        ClientSideComponentProperties="{&quot;targetUrl&quot;:&quot;ShowDetails.aspx&quot;}">
    </CustomAction>
</Elements>
```

Wie Sie sehen, ähnelt sie der SharePoint-Feature-Framework-Datei des „klassischen“ Modells. Sie verwendet jedoch das Attribut _ClientSideComponentId_, um die _id_ der benutzerdefinierten Erweiterung zu referenzieren, sowie das Attribut _ClientSideComponentProperties_, um die benutzerdefinierten Konfigurationseigenschaften zu konfigurieren, die für die Erweiterung erforderlich sind.

Öffnen Sie nun die Datei _package-solution.json_ im Ordner _/config_ der Lösung. Sie können sehen, dass sich in der Datei ein Verweis auf die _elements.xml_-Datei befindet, und zwar im Abschnitt _assets_.

```JSON
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "spfx-ecb-extension-client-side-solution",
    "id": "b8ff6fdf-16e9-4434-9fdb-eac6c5f948ee",
    "version": "1.0.2.0",
    "features": [
      {
        "title": "Custom ECB Menu Item.",
        "description": "Deploys a custom ECB menu item sample extension",
        "id": "f30a744c-6f30-4ccc-a428-125a290b5233",
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
    "zippedPackage": "solution/spfx-ecb-extension.sppkg"
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

6. Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens _CDN_, und fügen Sie ihr einen Ordner namens _customecb_ hinzu.
    
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
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-write-manifest.png)

3. Speichern Sie Ihre Änderungen.

4. Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken. Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei _write-manifests.json_ angegebenen CDN-URL. Die Ausgabe dieses Befehls finden Sie im Ordner _./temp/deploy_. Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert. 
    
    ```
    gulp bundle --ship
    ```
    
5. Führen Sie die folgende Aufgabe aus, um Ihre Lösung zu packen. Dieser Befehl erstellt ein Paket namens _spfx-ecb-extension.sppkg_ im Ordner _sharepoint/solution_ und bereitet außerdem die Ressourcen im Ordner _temp/deploy_ für die Bereitstellung im CDN vor.
    
    ```
    gulp package-solution --ship
    ```
    
6. Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche _Bereitstellen_.

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-cdn-address.png)

7. Laden Sie die Dateien im Ordner _temp/deploy_ in den Ordner _CDN/customfooter_ hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.

### <a name="install-and-run-the-solution"></a>Installieren und Ausführen der Lösung
<a name="InstallCommandSet"> </a> Sie können die Lösung jetzt auf jeder modernen Zielwebsite installieren.

1. Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.

2. Navigieren Sie zur Seite _Websiteinhalte_, und wählen Sie _App_, um eine neue App hinzuzufügen.

3. Wählen Sie zum Installieren einer neuen App _Aus Ihrer Organisation_, um die im _AppCatalog_ verfügbaren Lösungen zu durchsuchen.

4. Wählen Sie die Lösung mit dem Namen _spfx-ecb-extension-client-side-solution_, und installieren Sie sie auf der Zielwebsite.

    ![Hinzufügen einer App-Benutzeroberfläche, um die Lösung einer Website hinzuzufügen](../../../images/spfx-ecb-extension-add-app.png)

5. Nachdem die Installation der Anwendung abgeschlossen ist, öffnen Sie die _Documents_-Bibliothek der Website, und sehen Sie sich das funktionsfähige ECB-Menüelement an, indem Sie ein einzelnes Dokument auswählen.

Sie können nun Ihr neues benutzerdefiniertes ECB-Menüelement nutzen, das Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.
