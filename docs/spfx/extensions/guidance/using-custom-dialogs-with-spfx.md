---
title: 'Lernprogramm: Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint-Framework-Erweiterungen'
description: "Erstellen eines benutzerdefinierten Dialogfelds und Verwenden im Kontext einer Erweiterung des Typs „ListView Command Set“."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: da4680145b34cff093057f98f8c53d8c2a24b5ea
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a>Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint-Framework-Erweiterungen

Benutzerdefinierte Dialogfelder können im Kontext von SharePoint Framework-Erweiterungen oder im Kontext von clientseitigen Webparts verwendet werden. Sie sind über das Paket **@microsoft/sp-dialog** verfügbar. 

In diesem Artikel wird beschrieben, wie Sie ein benutzerdefiniertes Dialogfeld erstellen und im Kontext einer Erweiterung des Typs „ListView Command Set“ verwenden können.

Den Beispielcode, auf den in diesem Artikel Bezug genommen wird, finden Sie in unserem [sp-dev-fx-extensions](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog)-Repository.

## <a name="set-up-your-development-environment"></a>Einrichten der Entwicklungsumgebung

Um ein benutzerdefiniertes Dialogfeld zu erstellen, müssen Sie die Schritte in [Einrichten der Entwicklungsumgebung](../../set-up-your-development-environment.md) ausführen. Stellen Sie sicher, dass Sie die neuesten Yeoman-Vorlagen von SharePoint Framework verwenden.

## <a name="create-a-new-project"></a>Erstellen eines neuen Projekts

1. Erstellen Sie über eine Konsole Ihrer Wahl einen neuen Ordner für das Projekt:

  ```sh
  md dialog-cmd
  ```

2. Geben Sie diesen Ordner ein:

  ```sh
  cd dialog-cmd
  ```

3. Führen Sie den Yeoman-Generator für SharePoint Framework aus:

  ```sh
  yo @microsoft/sharepoint
  ```

4. Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

  * Übernehmen Sie den Standardwert **dialog-cmd** als Namen der Lösung, und drücken Sie die EINGABETASTE.
  * Wählen Sie **SharePoint Online only (latest)** aus, und drücken Sie die EINGABETASTE.
  * Wählen Sie **Use the current folder** aus, und drücken Sie die EINGABETASTE.
  * Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.
  * Wählen Sie **Extension** als den zu erstellenden Typ von clientseitiger Komponente aus. 
  * Wählen Sie **ListView Command Set** als den zu erstellenden Typ von Erweiterung aus.

5. Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:

  * Übernehmen Sie den Wert **DialogDemo** als Namen für Ihre Erweiterung, und drücken Sie die EINGABETASTE.
  * Übernehmen Sie den Standardwert **DialogDemo description** als Beschreibung Ihrer Erweiterung, und drücken Sie die EINGABETASTE.

  ![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../images/ext-com-dialog-yeoman-prompts.png)

  An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die **DialogDemo**-Erweiterung. Das kann einige Minuten dauern.

  Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:

  ![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../images/ext-com-dialog-yeoman-complete.png)

6. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

  ```sh
  npm shrinkwrap
  ```

7. Öffnen Sie den Projektordner in einem Code-Editor. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden. Um den Ordner in Visual Studio Code zu öffnen, verwenden Sie den folgenden Befehl in der Konsole:

  ```sh
  code .
  ```

  <br/>

  ![Anfängliche Visual Studio Code-Struktur nach der Gerüsterstellung](../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a>Ändern des Erweiterungsmanifests

Konfigurieren Sie die Erweiterung im Erweiterungsmanifest so, dass sie nur eine Schaltfläche hat. Öffnen Sie dazu im Code-Editor die Datei **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**, und ersetzen Sie den Befehlsabschnitt durch den folgenden JSON-Code:

```json
{
  //...
  "items": {
    "COMMAND_1": {
      "title": { "default": "Open Custom Dialog" },
      "iconImageUrl": "icons/request.png",
      "type": "command"
    }
  }
}
```

## <a name="create-a-custom-dialog-box"></a>Erstellen eines benutzerdefinierten Dialogfelds

1. Erstellen Sie eine neue Datei mit dem Namen **ColorPickerDialog.tsx** im Ordner **./src/extensions/dialogDemo/**.

2. Fügen Sie die folgenden Importanweisungen oben in der neu erstellten Datei hinzu: Sie erstellen Ihr benutzerdefiniertes Dialogfeld mithilfe der [React-Komponenten der Office UI Fabric](https://developer.microsoft.com/de-DE/fabric#/components), die Implementierung erfolgt daher in React. 

  ```ts
  import * as React from 'react';
  import * as ReactDOM from 'react-dom';
  import { BaseDialog, IDialogConfiguration } from '@microsoft/sp-dialog';
  import {
    autobind,
    ColorPicker,
    PrimaryButton,
    Button,
    DialogFooter,
    DialogContent
  } from 'office-ui-fabric-react';

  ```

3. Fügen Sie die folgende Schnittstellendefinition direkt unterhalb den Importanweisungen hinzu: Diese wird verwendet, um Informationen und Funktionen zwischen den Erweiterung des Typs „ListView Command Set“ und Ihrem benutzerdefinierten Dialogfeld zu übergeben.

  ```ts
  interface IColorPickerDialogContentProps {
    message: string;
    close: () => void;
    submit: (color: string) => void;
    defaultColor?: string;
  }
  ```

4. Fügen Sie die folgende Klasse direkt unterhalb der Schnittstellendefinition hinzu: Diese React-Klasse ist für das Rendern der Benutzeroberflächen innerhalb des benutzerdefinierten Dialogfelds verantwortlich. Beachten Sie, dass die React-Komponenten der Office UI Fabric für das tatsächliche Rendern verwendet wird und die erforderlichen Eigenschaften nur übergeben werden.  

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

5. Fügen Sie die folgende Klassendefinition für Ihr benutzerdefiniertes Dialogfeld unter der `ColorPickerDialogContent` -Klasse hinzu, die Sie soeben hinzugefügt haben. Dies ist das tatsächliche benutzerdefinierte Dialogfeld, das durch Klicken auf die Schaltfläche „ListView Command Set“ aufgerufen und von `BaseDialog` geerbt wird.

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

## <a name="associate-the-dialog-box-with-the-listview-command-set-button-click"></a>Verknüpfen des Dialogfelds mit dem Klickereignis für die per „ListView Command Set“ implementierte Schaltfläche

Zur Verknüpfung des benutzerdefinierten Dialogfelds mit Ihrer benutzerdefinierten Erweiterung des Typs „ListView Command Set“ fügen Sie nun den zur Initiierung des Dialogfelds erforderlichen Code in die Klickoperation der Schaltfläche ein.

1. Öffnen Sie im Code-Editor die Datei **DialogDemoCommandSet.ts** im Ordner **./src/extensions/dialogDemo/**.

2. Fügen Sie die nachfolgenden Importanweisungen unter der bereits vorhandenen **strings**-Importanweisung hinzu. Über die neuen Importanweisungen kann das benutzerdefinierte Dialogfeld im Kontext der Erweiterung des Typs „ListView Command Set“ verwendet werden. 

  ```ts
  import ColorPickerDialog from './ColorPickerDialog';
  ```

3. Fügen Sie die nachfolgende Variablendefinition `_colorCode` oberhalb der Funktion `onInit` in die Klasse `DialogDemoCommandSet` ein. Sie speichert den Rückgabewert aus dem Farbauswahl-Dialogfeld.

  ```ts
    private _colorCode: string;
  ```

4. Aktualisieren Sie die Funktion `onExecute` wie unten dargestellt. Dieser Code führt folgende Aktionen durch:

  * Er initiiert das benutzerdefinierte Dialogfeld.
  * Er übergibt eine Nachricht an das Dialogfeld, die als Titel verwendet wird.
  * Er übergibt einen Farbcode an das Dialogfeld (den Standardwert, falls nicht anders festgelegt).
  * Er rendert das benutzerdefinierte Dialogfeld.
  * Er empfängt und speichert den Rückgabewert des Dialogfelds.
  * Er zeigt den empfangenen Wert mithilfe der Funktion `Dialog.alert()` in einem Standarddialogfeld an.

  ```ts
    @override
    public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
      switch (event.itemId) {
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

## <a name="test-the-dialog-box-in-your-tenant"></a>Testen des benutzerdefinierten Dialogfelds im Mandanten

1. Öffnen Sie die Datei **serve.json** in dem Ordner **./config/**, und aktualisieren Sie die aktuellen Einstellungen in der Datei. Diese Datei ermöglicht ein einfacheres Debuggen von SharePoint-Framework-Erweiterungen. Sie können den Dateiinhalt an die entsprechenden Mandanten- und Websitedetails anpassen, die zum Testen der Erweiterung verwendet werden sollen. Ein wichtiger Wert, der in der JSON-Definition an den entsprechenden Mandanten angepasst werden muss, ist die `pageUrl`-Eigenschaft.

2. `pageUrl` muss auf eine Listen-URL verweisen, wo die Dialogfeldfunktionalität getestet werden soll.

  ```sh
    "serveConfigurations": {
      "default": {
        "pageUrl": "https://sppnp.sharepoint.com/sites/team/Shared%20Documents/Forms/AllItems.aspx",
        "customActions": {
          "9b98b919-fe5e-4758-ac91-6d62e582c4fe": {
            "location": "ClientSideExtension.ListViewCommandSet.CommandBar",
            "properties": {
              "sampleTextOne": "One item is selected in the list",
              "sampleTextTwo": "This command is always visible."
            }
          }
        }
      },
  ```

  > [!NOTE]
  > Der eindeutige Bezeichner der Erweiterung wird während der anfänglichen Gerüsterstellung automatisch auf diese Datei aktualisiert. Wenn Sie die Eigenschaften ändern, die Ihre Erweiterung verwendet, sollten Sie die Datei **serve.json** vor dem Debuggen entsprechend aktualisieren.

3. Wechseln Sie zurück zur Konsole, und führen Sie den folgenden Befehl aus:

  ```sh
  gulp serve
  ```

  Nun wird die Bündelung der Lösung angestoßen, und das resultierende Manifest wird von der `localhost`-Adresse ausgeliefert. Aufgrund der Konfiguration in der Datei **serve.json** wird auch ein Browser in der angegebenen URL geöffnet, bei dem die Abfrageparameter automatisch auf Grundlage der Lösungskonfiguration festgelegt sind.

4. Klicken Sie bei Aufforderung auf **Debugskripts laden**, um das Laden der Debugmanifeste zu akzeptieren.

  ![Warnung zum Zulassen von Debugskripts](../../../images/ext-com-dialog-debug-scripts.png)

  Beachten Sie, dass die neue Schaltfläche *nicht* standardmäßig in der Symbolleiste angezeigt wird, da Sie für die Standardlösung ein Element aus der Liste auswählen müssen. Wenn keine Elemente in der Liste oder Bibliothek angezeigt werden, erstellen Sie ein Element, oder laden Sie ein Dokument hoch. 

5. Wählen Sie ein Element aus der Liste oder der Bibliothek aus. Die Schaltfläche wird nun in der Symbolleiste mit dem Text **Open Custom Dialog** angezeigt.

  ![Die Schaltfläche „Open Cusotm Dialog“ wird auf der Symbolleiste angezeigt](../../../images/ext-com-dialog-button-in-toolbar.png)

6. Klicken Sie auf die Schaltfläche **Open Custom Dialog**. Ihr benutzerdefiniertes Dialogfeld wird nun in der Listenansicht gerendert. 

  ![Im Dialogmodus gerenderte Farbauswahl](../../../images/ext-com-dialog-visible-dialog.png)

7. Wählen Sie eine Farbe in der **Farbauswahl** aus, und klicken Sie dann auf **OK**, um zu testen, wie der Code den ausgewählten Wert zurück an den Aufrufer zurückgibt. Die Auswahl wird dann mithilfe des standardmäßigen Warndialogfelds angezeigt.

  ![Dialogfeld mit Details zur ausgewählten Farbe](../../../images/ext-com-dialog-oob-alert-dialog.png)

> [!NOTE]
> Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues). Vielen Dank im Voraus für Ihr Feedback.

## <a name="see-also"></a>Siehe auch

- [Übersicht über SharePoint-Framework-Erweiterungen](../overview-extensions.md)