# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a>Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint Framework-Erweiterungen

Benutzerdefinierte Dialogfelder können im Kontext von SharePoint Framework-Erweiterungen oder im Kontext von clientseitigen Webparts verwendet werden. Sie sind über das Paket **@microsoft/sp-dialog** verfügbar. 

In diesem Artikel wird beschrieben, wie Sie ein benutzerdefiniertes Dialogfeld erstellen und im Kontext einer Erweiterung des Typs „ListView Command Set“ verwenden können.

>**Hinweis:** Das Feature zur Erstellung benutzerdefinierter Dialogfelder befindet sich derzeit in der Preview-Phase. Wir würden uns vor der Freigabe über Ihr Feedback freuen. Wenn Sie uns Feedback senden möchten, können Sie [ein Ticket in unserem GitHub-Repository erstellen](https://github.com/SharePoint/sp-dev-docs/issues).

> Beachten Sie, dass das Debuggen von benutzerdefinierten Erweiterungen des Typs „ListView Command Set“ in SharePoint Online derzeit nur über die moderne Listenoberfläche auf klassischen Teamwebsites möglich ist, die in einem **Entwicklermandanten** gehostet werden.


Den Beispielcode, auf den in diesem Artikel Bezug genommen wird, finden Sie in unserem [Repository](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).

## <a name="set-up-your-development-environment"></a>Einrichten der Entwicklungsumgebung

Zur Erstellung eines benutzerdefinierten Dialogfelds müssen Sie zunächst die Schritt-für-Schritt-Anleitung im Artikel zum Thema [Einrichten Ihrer Entwicklungsumgebung](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) befolgen. Stellen Sie sicher, dass Sie die neuesten SharePoint Framework-Yeoman-Vorlagen verwenden. 

Aktualisieren können Sie Ihre SharePoint Framework-Yeoman-Vorlagen mit dem folgenden Befehl:

```sh
npm install -g @microsoft/generator-sharepoint`
```

## <a name="create-a-new-project"></a>Erstellen eines neuen Projekts

Erstellen Sie über eine Konsole Ihrer Wahl einen neuen Ordner für das Projekt:

```sh
md dialog-cmd
```

Wechseln Sie nun in diesen Ordner:

```sh
cd dialog-cmd
```

Führen Sie den Yeoman-Generator für SharePoint Framework aus:

```sh
yo @microsoft/sharepoint
```

Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

* Übernehmen Sie den Standardwert **dialog-cmd** als Namen der Lösung, und drücken Sie die **EINGABETASTE**.
* Wählen Sie **Extension (Preview)** als den zu erstellenden Typ von clientseitiger Komponente aus. 
* Wählen Sie **ListView Command Set (Preview)** als den zu erstellenden Typ von Erweiterung aus.

Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:

* Übernehmen Sie den Wert **DialogDemo** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.
* Übernehmen Sie den Standardwert **DialogDemo description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.

![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../../images/ext-com-dialog-yeoman-prompts.png)

An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die *DialogDemo*-Erweiterung. Das kann einige Minuten dauern. 

Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-com-dialog-yeoman-complete.png)

>**Hinweis:** Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../basics/known-issues).

Öffnen Sie nach dem Abschluss der Gerüsterstellung den Projektordner in Ihrem Code-Editor. Für die Anleitung in diesem Artikel haben wir Visual Studio Code verwendet; auch die Screenshots entstammen diesem Editor. Sie können jedoch auch jeden beliebigen anderen Editor verwenden. Führen Sie den folgenden Befehl in der Konsole aus, um den Ordner in Visual Studio Code zu öffnen:

```sh
code .
```

![Anfängliche Visual Studio Code-Struktur nach der Gerüsterstellung](../../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a>Ändern des Erweiterungsmanifests

Konfigurieren Sie die Erweiterung im Erweiterungsmanifest so, dass sie nur eine Schaltfläche hat. Öffnen Sie dazu im Code-Editor die Datei **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**, und ersetzen Sie den Befehlsabschnitt durch den folgenden JSON-Code:

```json
{
  //...
  "commands": {
    "COMMAND_1": {
      "title": "Open Custom Dialog",
      "iconImageUrl": "icons/request.png"
    }
  }
}
```

## <a name="add-the-sp-dialog-package-to-the-solution"></a>Hinzufügen des Pakets „sp-dialog“ zur Lösung

Wechseln Sie wieder zur Konsole, und führen Sie den folgenden Befehl aus, um die Dialogfeld-API in die Lösung einzuschließen:

```sh
npm install @microsoft/sp-dialog --save
```

Da Sie die Option `--save` verwenden, wird diese Abhängigkeit der Datei **package.json** hinzugefügt. Dadurch wird sichergestellt, dass sie automatisch installiert wird, sobald der Befehl `npm install` ausgeführt wird. (Das ist wichtig, wenn Sie das Projekt an einen anderen Speicherort wiederherstellen oder klonen möchten.)

Wechseln Sie wieder zu Visual Studio Code (oder Ihrem bevorzugten Editor).

## <a name="create-a-custom-dialog-box"></a>Erstellen eines benutzerdefinierten Dialogfelds

Erstellen Sie eine neue Datei mit dem Namen **ColorPickerDialog.tsx** im Ordner **./src/extensions/dialogDemo/**.

Fügen Sie die folgenden Importanweisungen am Anfang der neu erstellten Datei ein. Da Sie das benutzerdefinierte Dialogfeld mithilfe von [Office UI Fabric React-Komponenten](https://dev.office.com/fabric#/components) erstellen, nutzen Sie React zur Implementierung. 

> **Hinweis:** Die Komponente `DialogContent` wird derzeit über `@microsoft/sp-dialog` bereitgestellt, sie wird jedoch in Kürze in die Office UI Fabric React-Komponenten aufgenommen. 

```ts
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { BaseDialog, IDialogConfiguration } from '@microsoft/sp-dialog';
import {
  autobind,
  ColorPicker,
  PrimaryButton,
  Button,
  DialogFooter
  // DialogContent <- This should be imported here for third parties
} from 'office-ui-fabric-react';
// Note: DialogContent is available in v2.32.0 of office-ui-fabric-react
// As a workaround we're importing it from sp-dialog until the next version bump
import { DialogContent } from '@microsoft/sp-dialog';
```

Fügen Sie die nachfolgende Schnittstellendefinition direkt unterhalb der Importanweisungen ein. Sie regelt die Übergabe von Informationen und Funktionen zwischen Ihrer Erweiterung des Typs „ListView Command Set“ und Ihrem benutzerdefinierten Dialogfeld.

```ts
interface IColorPickerDialogContentProps {
  message: string;
  close: () => void;
  submit: (color: string) => void;
  defaultColor?: string;
}
```

Fügen Sie die nachfolgende Klasse direkt unterhalb der Schnittstellendefinition ein. Diese React-Klasse ist für das Rendern der Benutzeroberfläche im benutzerdefinierten Dialogfeld zuständig. Wie Sie sehen, werden zum eigentlichen Rendern die Office UI Fabric React-Komponenten verwendet. Die erforderlichen Eigenschaften werden lediglich übergeben.  

```ts
class ColorPickerDialogContent extends React.Component<IColorPickerDialogContentProps, {}> {
  private _pickedColor: string;

  constructor(props) {
    super(props);
    // Default Color
    this._pickedColor = props.defaultColor || '#FFFFFF';
  }

  public render(): JSX.Element {
    return <DialogContent
      title='Color Picker'
      subText={this.props.message}
      onDismiss={this.props.close}
      showCloseButton={true}
    >
      <ColorPicker color={this._pickedColor} onColorChanged={this._onColorChange} />
      <DialogFooter>
        <Button text='Cancel' title='Cancel' onClick={this.props.close} />
        <PrimaryButton text='OK' title='OK' onClick={() => { this.props.submit(this._pickedColor); }} />
      </DialogFooter>
    </DialogContent>;
  }

  @autobind
  private _onColorChange(color: string): void {
    this._pickedColor = color;
  }
}
```
Fügen Sie die nachfolgende Klassendefinition für das benutzerdefinierte Dialogfeld direkt unterhalb der Klasse `ColorPickerDialogContent` ein, die Sie soeben hinzugefügt haben. Hierbei handelt es sich um das eigentliche benutzerdefinierte Dialogfeld, das über einen Klick auf die durch die Erweiterung des Typs „ListView Command Set“ implementierte Schaltfläche aufgerufen wird und von `BaseDialog` vererbt wird.

```ts
export default class ColorPickerDialog extends BaseDialog {
  public message: string;
  public colorCode: string;

  public render(): void {
    ReactDOM.render(<ColorPickerDialogContent
      close={ this.close }
      message={ this.message }
      defaultColor={ this.colorCode }
      submit={ this._submit }
    />, this.domElement);
  }

  public getConfig(): IDialogConfiguration {
    return {
      isBlocking: false
    };
  }

  @autobind
  private _submit(color: string): void {
    this.colorCode = color;
    this.close();
  }
}
```

## <a name="associate-the-custom-dialog-box-with-the-listview-command-set-button-click"></a>Verknüpfen des benutzerdefinierten Dialogfelds mit dem Klickereignis für die per „ListView Command Set“ implementierte Schaltfläche
Zur Verknüpfung des benutzerdefinierten Dialogfelds mit Ihrer benutzerdefinierten Erweiterung des Typs „ListView Command Set“ fügen Sie nun den zur Initiierung des Dialogfelds erforderlichen Code in die Klickoperation der Schaltfläche ein.

Öffnen Sie im Code-Editor die Datei **DialogDemoCommandSet.ts** im Ordner **./src/extensions/dialogDemo/**.

Fügen Sie die nachfolgenden Importanweisungen unter der bereits vorhandenen **strings**-Importanweisung hinzu. Über die neuen Importanweisungen kann das benutzerdefinierte Dialogfeld im Kontext der Erweiterung des Typs „ListView Command Set“ verwendet werden. 

```ts
import { Dialog } from '@microsoft/sp-dialog';
import ColorPickerDialog from './ColorPickerDialog';
```

Fügen Sie die nachfolgende Variablendefinition `_colorCode` oberhalb der Funktion `onInit` in die Klasse `DialogDemoCommandSet` ein. Sie speichert den Rückgabewert aus dem Farbauswahl-Dialogfeld.

```ts
  private _colorCode: string;
```

Aktualisieren Sie die Funktion `onExecute` wie unten dargestellt. Dieser Code führt folgende Aktionen durch:

* Er initiiert das benutzerdefinierte Dialogfeld.
* Er übergibt eine Nachricht an das Dialogfeld, die als Titel verwendet wird.
* Er übergibt einen Farbcode an das Dialogfeld (den Standardwert, falls nicht anders festgelegt).
* Er rendert das benutzerdefinierte Dialogfeld.
* Er empfängt und speichert den Rückgabewert des Dialogfelds.
* Er zeigt den empfangenen Wert mithilfe der Funktion `Dialog.alert()` in einem Standarddialogfeld an.

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
      case 'COMMAND_1':
        const dialog: ColorPickerDialog = new ColorPickerDialog();
        dialog.message = 'Pick a color:';
        // Use 'EEEEEE' as the default color for first usage
        dialog.colorCode = this._colorCode || '#EEEEEE';
        dialog.show().then(() => {
          this._colorCode = dialog.colorCode;
          Dialog.alert(`Picked color: ${dialog.colorCode}`);
        });
        break;
      default:
        throw new Error('Unknown command');
    }
  }
```

## <a name="test-the-custom-dialog-box-in-your-tenant"></a>Testen des benutzerdefinierten Dialogfelds im Mandanten

Öffnen Sie die Datei **DialogDemoCommandSet.manifest.json** im Ordner **./src/extensions/dialogDemo/**, und kopieren Sie den **id**-Wert. Ihn müssen Sie im Abfrageparameter für das Debuggen angeben.

Wechseln Sie zurück zur Konsole, und führen Sie den folgenden Befehl aus:

```sh
gulp serve --nobrowser
```

Wie Sie sehen, verwenden Sie die Option `--nobrowser`. Ein Aufrufen der lokalen Workbench ist nicht nötig, da Erweiterungen derzeit nicht lokal debuggt werden können.

Nun wird die Bündelung der Lösung angestoßen, und das resultierende Manifest wird von der `localhost`-Adresse ausgeliefert.

![Anfängliche Visual Studio Code-Struktur nach der Gerüsterstellung](../../../../images/ext-com-dialog-gulp-serve.png)

Navigieren Sie nun zu einer Website in Ihrem SharePoint Online-Entwicklermandanten, um Ihre Erweiterung zu testen.

Rufen Sie auf der Website eine bereits vorhandene benutzerdefinierte Liste mit Elementen auf. Sie können auch eine neue Liste erstellen und ihr zu Testzwecken einige Elemente hinzufügen. 

Fügen Sie die nachfolgenden Abfragezeichenfolgenparameter an die URL an. Beachten Sie, dass Sie den **id**-Wert mit dem Bezeichner Ihrer Erweiterung aus der Datei **DialogDemoCommandSet.manifest.json** aktualisieren müssen:

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

Klicken Sie bei Aufforderung auf **Load debug scripts**, um das Laden der Debugmanifeste zu akzeptieren.

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-debug-scripts.png)

Sie sehen: Die neue Schaltfläche wird jetzt auf der Symbolleiste der Liste angezeigt, mit dem Text *Open Custom Dialog*.

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-button-in-toolbar.png)

Klicken Sie auf die Schaltfläche *Open Custom Dialog*. Ihr benutzerdefiniertes Dialogfeld wird nun in der Listenansicht gerendert. 

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-visible-dialog.png)

Wählen Sie in der *Farbauswahl* eine Farbe aus, und klicken Sie auf **OK**, um zu testen, wie der Code den ausgewählten Wert an den Aufrufer zurückgibt. Die Auswahl wird anschließend in einem Standarddialogfeld „Alert“ angezeigt.

![Standarddialogfeld „Alert“](../../../../images/ext-com-dialog-oob-alert-dialog.png)
