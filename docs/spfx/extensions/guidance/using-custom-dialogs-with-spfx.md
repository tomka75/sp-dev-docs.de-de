# <a name="using-custom-dialogs-with-sharepoint-framework-extensions"></a><span data-ttu-id="29229-101">Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint Framework Extensions</span><span class="sxs-lookup"><span data-stu-id="29229-101">Using Custom Dialogs with SharePoint Framework Extensions</span></span>

<span data-ttu-id="29229-102">Im Paket `@microsoft/sp-dialog` stehen benutzerdefinierte Dialogfelder zur Verfügung, die im Kontext von SharePoint Framework Extensions oder clientseitigen Webparts verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="29229-102">Custom dialogs are available from `@microsoft/sp-dialog`package and can be used within the context of SharePoint Framework Extensions or client-side web parts.</span></span> 

<span data-ttu-id="29229-103">Dieses Lernprogramm demonstriert die Erstellung eines benutzerdefinierten Dialogfelds und dessen Verwendung im Kontext der ListView-Befehlssatzerweiterung.</span><span class="sxs-lookup"><span data-stu-id="29229-103">This tutorial demonstrates creation of a custom dialog and using that in the context of ListView Command Set extension.</span></span>

> <span data-ttu-id="29229-p101">Beachten Sie, dass sich das SharePoint Framework-Dialogfeld derzeit in der Vorschauphase befindet und wir Feedback sammeln, bevor es offiziell veröffentlicht wird. Übermitteln Sie uns Ihr Feedback anhand der [sp-dev-docs-Repository-Problemliste](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="29229-p101">Notice that the SharePoint Framework dialog is currently in preview status and we are looking to collect feedback before it's officially released. Please provide us feedback by using the [sp-dev-docs repository Issue list](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

> <span data-ttu-id="29229-106">Beachten Sie, dass das Debuggen von benutzerdefinierten ListView-Sätzen in SharePoint Online derzeit nur in der modernen Listenoberfläche auf klassischen Teamwebsites verfügbar ist, die auf einem Entwicklungsmandanten gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="29229-106">Notice that debugging Custom ListView Sets in the SharePoint Online is currently only available from modern list experience in classic team sites hosted on dev tenant.</span></span> 

> <span data-ttu-id="29229-107">Das Endergebnis dieses Lernprogramms ist ebenfalls als Quellcode unter https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog verfügbar.</span><span class="sxs-lookup"><span data-stu-id="29229-107">End result of this tutorial is also available as source code at https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog.</span></span>  

## <a name="setup-your-environment"></a><span data-ttu-id="29229-108">Einrichten der Umgebung</span><span class="sxs-lookup"><span data-stu-id="29229-108">Setup your Environment</span></span>

<span data-ttu-id="29229-109">Bevor Sie diesen Leitfaden durcharbeiten können, müssen Sie sicherstellen, dass Sie [Ihre Umgebung](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) für die Entwicklung mithilfe von SharePoint-Framework eingerichtet haben und dass Sie die aktuellen Yeoman-Vorlagen für das SharePoint-Framework verwenden.</span><span class="sxs-lookup"><span data-stu-id="29229-109">Before you can complete this guide you will need to ensure you have [setup your environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) for development using SharePoint Framework and that you are using latest SharePoint Framework Yeoman templates.</span></span> 

> <span data-ttu-id="29229-110">Sie können Ihre SharePoint-Framework-Yeoman-Vorlagen aktualisieren, indem Sie den folgenden Befehl ausführen: `npm install -g @microsoft/generator-sharepoint`.</span><span class="sxs-lookup"><span data-stu-id="29229-110">You can update your SharePoint Framework Yeoman templates by running following command `npm install -g @microsoft/generator-sharepoint`.</span></span> 

## <a name="create-a-new-project"></a><span data-ttu-id="29229-111">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="29229-111">Create a New Project</span></span>

<span data-ttu-id="29229-112">Erstellen Sie zunächst einen neuen Ordners für das Projekt über eine Konsole Ihrer Wahl:</span><span class="sxs-lookup"><span data-stu-id="29229-112">Start by creating a new folder for the project using your console of choice:</span></span>

```sh
md dialog-cmd
```

<span data-ttu-id="29229-113">Geben Sie diesen Ordner ein</span><span class="sxs-lookup"><span data-stu-id="29229-113">And enter that folder</span></span>

```sh
cd dialog-cmd
```

<span data-ttu-id="29229-114">Führen Sie dann den Yeoman-Generator für das SharePoint-Framework aus.</span><span class="sxs-lookup"><span data-stu-id="29229-114">The run the Yeoman generator for SPFx</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="29229-115">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="29229-115">When prompted:</span></span>

* <span data-ttu-id="29229-116">Übernehmen Sie den Standardwert **dialog-cmd** als Namen der Lösung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="29229-116">Accept the default value of **dialog-cmd** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="29229-117">Wählen Sie **Extension (Preview)** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="29229-117">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="29229-118">Wählen Sie **ListView Command Set (Preview)** als den zu erstellenden Typ von Erweiterung aus.</span><span class="sxs-lookup"><span data-stu-id="29229-118">Choose **ListView Command Set (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="29229-119">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:</span><span class="sxs-lookup"><span data-stu-id="29229-119">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="29229-120">Übernehmen Sie den Standardwert **DialogDemo** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="29229-120">Accept the default value of **DialogDemo** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="29229-121">Übernehmen Sie den Standardwert **DialogDemo description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="29229-121">Accept the default value of **DialogDemo description** as your extension description and press **Enter**.</span></span>

![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../../images/ext-com-dialog-yeoman-prompts.png)

<span data-ttu-id="29229-p102">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die *HelloWorld*-Erweiterung. Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="29229-p102">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the *HelloWorld* web part. This might take a few minutes.</span></span> 

<span data-ttu-id="29229-125">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="29229-125">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-com-dialog-yeoman-complete.png)

<span data-ttu-id="29229-127">Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="29229-127">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

<span data-ttu-id="29229-p103">Öffnen Sie den Projektordner in Ihrem Code-Editor, sobald die Gerüsterstellung abgeschlossen ist. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="29229-p103">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

```
code .
```

![Anfängliche Visual Studio Code-Struktur nach dem Bau des Gerüsts](../../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-extension-manifest-based-on-requirements"></a><span data-ttu-id="29229-131">Ändern des Erweiterungsmanifests basierend auf Anforderungen</span><span class="sxs-lookup"><span data-stu-id="29229-131">Modify extension manifest based on requirements</span></span> 

<span data-ttu-id="29229-p104">Konfigurieren Sie im Erweiterungsmanifest die Erweiterung so, dass sie nur eine Schaltfläche hat. Öffnen Sie im Code-Editor die Datei **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**. Ersetzen Sie den Befehlsabschnitt mit dem folgenden JSON-Code:</span><span class="sxs-lookup"><span data-stu-id="29229-p104">In the extension manifest, configure extension to have only one button. In the code editor, open the **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json** file. Replace the commands section with the following JSON:</span></span>

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

## <a name="adding-sp-dialog-package-to-solution"></a><span data-ttu-id="29229-135">Hinzufügen des sp-dialog-Pakets zur Lösung</span><span class="sxs-lookup"><span data-stu-id="29229-135">Adding sp-dialog package to solution</span></span>
<span data-ttu-id="29229-136">Wechseln Sie wieder zur Konsole, und führen Sie den folgenden Befehl aus, um die Dialogfeld-API in die Lösung einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="29229-136">Return to the console and execute the following command to include the dialog API in our solution.</span></span> 

```
npm install @microsoft/sp-dialog --save
```

<span data-ttu-id="29229-137">Da wir die Option `--save` verwenden, wird diese Abhängigkeit zur Datei *package.json* hinzugefügt und automatisch installiert, wenn der Befehl `npm install` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="29229-137">Since we are using the `--save` option, this dependency will be added to *package.json* file and would be automatically installed when `npm install` command is executed.</span></span>

<span data-ttu-id="29229-138">Wechseln Sie wieder zu Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="29229-138">Return to Visual Studio Code (or your preferred editor).</span></span>

## <a name="creating-your-custom-dialog"></a><span data-ttu-id="29229-139">Erstellen des benutzerdefinierten Dialogfelds</span><span class="sxs-lookup"><span data-stu-id="29229-139">Creating your custom dialog</span></span>
<span data-ttu-id="29229-140">Erstellen Sie eine neue Datei mit dem Namen **ColorPickerDialog.tsx** im Ordner **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="29229-140">Create a new file called **ColorPickerDialog.tsx** to **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="29229-p105">Fügen Sie die folgenden Importanweisungen am Anfang der neu erstellten Datei hinzu. Wir erstellen unser benutzerdefiniertes Dialogfeld mit Office UI Fabric React-Komponenten, sodass die Implementierung in React erfolgt.</span><span class="sxs-lookup"><span data-stu-id="29229-p105">Add following import statements on the start of the newly created file. We are creating our custom dialog using Office UI Fabric React components, so the implementation will be in React.</span></span> 

> <span data-ttu-id="29229-143">Beachten Sie, dass die DialogContent-Komponente derzeit aus `@microsoft/sp-dialog` stammt. Sie wird jedoch in Kürze in die Office UI Fabric React Komponenten aufgenommen, wie bereits in den Codekommentaren erwähnt.</span><span class="sxs-lookup"><span data-stu-id="29229-143">Notice that currently DialogContent component is coming from `@microsoft/sp-dialog`, but will be included in Office UI Fabric React components soon, like mentioned in the code comments.</span></span> 

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

<span data-ttu-id="29229-p106">Fügen Sie die folgende Schnittstellendefinition direkt unterhalb der Importanweisungen ein. Dies wird verwendet, um benötigte Informationen und Funktionen zwischen der ListView-Befehlssatzerweiterung und dem benutzerdefinierten Dialogfeld zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="29229-p106">Add following interface definition just below the import statements. This wil be used to bypass needed information and functions between the ListView Command Set extension and custom dialog.</span></span>

```ts
interface IColorPickerDialogContentProps {
  message: string;
  close: () => void;
  submit: (color: string) => void;
  defaultColor?: string;
}
```

<span data-ttu-id="29229-p107">Fügen Sie die folgende Klasse direkt unter der Schnittstellendefinition ein. Diese React-Klasse ist für das Rendern der Benutzeroberfläche im benutzerdefinierten Dialogfeld zuständig. Beachten Sie, dass wir die Office UI Fabric React-Komponenten für das eigentliche Rendern verwenden und die erforderlichen Eigenschaften umgehen.</span><span class="sxs-lookup"><span data-stu-id="29229-p107">Add following class just below the interface definition. This React class is responsible for rendering the UI experiences inside of the custom dialog. Notice that we use the Office UI Fabric React components for actual rendering and just bypass the needed properties.</span></span>  

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
<span data-ttu-id="29229-p108">Fügen Sie die folgende Klassendefinition für das benutzerdefinierte Dialogfeld direkt unter dem soeben hinzugefügten Klassencode hinzu. Dies ist das eigentliche benutzerdefinierte Dialogfeld, das durch Klicken auf die Schaltfläche aufgerufen wird und das von **BaseDialog** geerbt wird.</span><span class="sxs-lookup"><span data-stu-id="29229-p108">Add following class definition for our custom dialog under the just added class code. This one is the actual custom dialog, which will be called from the button click and which is inherited from the **BaseDialog**.</span></span>

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

## <a name="associating-custom-dialog-to-button-click"></a><span data-ttu-id="29229-151">Zuordnen des benutzerdefinierten Dialogfelds zur Schaltflächen-Klickaktion</span><span class="sxs-lookup"><span data-stu-id="29229-151">Associating custom dialog to button click</span></span>
<span data-ttu-id="29229-152">Um das benutzerdefinierte Dialogfeld dem benutzerdefinierten ListView-Befehlssatz zuzuordnen, muss der Code zum Initiieren des Dialogfelds für die Schaltflächen-Klickaktion hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="29229-152">To associate the custom dialog button to custom ListView Command Set, the code to initiate the dialog has to be added for the button click operation.</span></span>

<span data-ttu-id="29229-153">Öffnen Sie im Code-Editor die Datei **DialogDemoCommandSet.ts** aus dem Ordner **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="29229-153">In the code editor, open the  **DialogDemoCommandSet.ts** file from **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="29229-p109">Fügen Sie die folgenden Importanweisungen unter dem vorhandenen **strings**-Import hinzu. Diese dienen zur Verwendung des gerade erstellten benutzerdefinierten Dialogfelds im Kontext des ListView-Befehlssatzes.</span><span class="sxs-lookup"><span data-stu-id="29229-p109">Add following import statements under the existing **strings** import. These are for using the just created custom dialog in the context of ListView Command Set.</span></span> 

```ts
import { Dialog } from '@microsoft/sp-dialog';
import ColorPickerDialog from './ColorPickerDialog';
```

<span data-ttu-id="29229-p110">Fügen Sei die folgende **_colorCode**-Variablendefinition oberhalb der **onInit**-Funktion in der **DialogDemoCommandSet**-Klasse hinzu. Dies wird zum Speichern des Ergebnisses für das Farbauswahl-Dialogfeld verwendet.</span><span class="sxs-lookup"><span data-stu-id="29229-p110">Add following **_colorCode** variable definition above **onInit** function in the **DialogDemoCommandSet** class. This is used to store teh color picker dialog result.</span></span>

```ts
  private _colorCode: string;
```

<span data-ttu-id="29229-p111">Aktualisieren Sie die **OnExecute**-Funktion wie folgt. In diesem Code führen wir die folgenden Schritte durch.</span><span class="sxs-lookup"><span data-stu-id="29229-p111">Update the **onExecute** function as follows. In this code we are doing following steps</span></span>

* <span data-ttu-id="29229-160">Initiieren des benutzerdefinierten Dialogfelds</span><span class="sxs-lookup"><span data-stu-id="29229-160">Initiate custom dialog</span></span>
* <span data-ttu-id="29229-161">Umgehen der Meldung für das Dialogfeld, die als Titel verwendet wird</span><span class="sxs-lookup"><span data-stu-id="29229-161">Bypass message for the dialog, which will be used as title</span></span>
* <span data-ttu-id="29229-162">Umgehen des Farbcodes für das Dialogfeld mit dem Standardwert, wenn noch nicht festgelegt</span><span class="sxs-lookup"><span data-stu-id="29229-162">Bypass color code for the dialog with default value, if not yet set</span></span>
* <span data-ttu-id="29229-163">Anzeigen des benutzerdefinierten Dialogfelds</span><span class="sxs-lookup"><span data-stu-id="29229-163">Show the dialog box</span></span>
* <span data-ttu-id="29229-164">Empfangen und Speichern des vom Dialogfeld zurückgegebenen Werts</span><span class="sxs-lookup"><span data-stu-id="29229-164">Receive and store return value from the dialog</span></span>
* <span data-ttu-id="29229-165">Anzeigen des erhaltenen Werts im vordefinierten Dialogfeld mit der `Dialog.alert()`-Funktion</span><span class="sxs-lookup"><span data-stu-id="29229-165">Show received value in out-of-the-box dialog using `Dialog.alert()` function</span></span>

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

## <a name="testing-custom-dialog-in-your-tenant"></a><span data-ttu-id="29229-166">Testen des benutzerdefinierten Dialogfelds im Mandanten</span><span class="sxs-lookup"><span data-stu-id="29229-166">Testing custom dialog in your tenant</span></span>
<span data-ttu-id="29229-167">Gehen Sie zur Datei **DialogDemoCommandSet.manifest.json** im Ordner **./src/extensions/dialogDemo/**, und kopieren Sie den **id**-Wert, der im Debugging-Abfrageparameter verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="29229-167">Move to **DialogDemoCommandSet.manifest.json** file in **./src/extensions/dialogDemo/** folder and copy **id** value, which will be used in the debug query parameter.</span></span>

<span data-ttu-id="29229-p112">Wechseln Sie zur Konsole, und führen Sie den folgenden Befehl aus. Wir verwenden die Option `--nobrowser`, da die lokale Workbench derzeit nicht für das Debuggen verwendet werden kann. Daher ist es nicht notwendig, sie zu starten.</span><span class="sxs-lookup"><span data-stu-id="29229-p112">Move to console side and execute following command. We use `--nobrowser` option, since local workbench cannot be currently used for debugging, so there's no reason to start that.</span></span> 

```sh
gulp serve --nobrowser
```

<span data-ttu-id="29229-170">Hierdurch wird die Bündelung gestartet, und es dient als das sich aus der `localhost`-Adresse ergebende Manifest.</span><span class="sxs-lookup"><span data-stu-id="29229-170">This will start bundling and will serve the resulting manifest from `localhost` address.</span></span>

![Anfängliche Visual Studio Code-Struktur nach dem Bau des Gerüsts](../../../../images/ext-com-dialog-gulp-serve.png)

<span data-ttu-id="29229-172">Um die Erweiterung zu testen, navigieren Sie zu einer Website in Ihrem SharePoint Online-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="29229-172">To test your extension, navigate to a site in your SharePoint Online tenant.</span></span>

<span data-ttu-id="29229-173">Gehen Sie zu einer vorhandenen benutzerdefinierten Liste auf der Website, die einige Elemente enthält, oder erstellen Sie eine neue Liste, und fügen Sie ihr einige Elemente zu Testzwecken hinzu.</span><span class="sxs-lookup"><span data-stu-id="29229-173">Move to an existing custom list in the site with some items or create a new list and add few items to it for testing purposes.</span></span> 

<span data-ttu-id="29229-p113">Fügen Sie die folgende Abfragezeichenfolgenparameter an die URL an. Beachten Sie, dass Sie die **ID** aktualisieren müssen, damit diese Ihrer Erweiterungs-ID entspricht, die in der Datei **DialogDemoCommandSet.manifest.json** verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="29229-p113">Append the following query string parameters to the URL. Notice that you will need to update the **id** to match your own extension identifier available from the **DialogDemoCommandSet.manifest.json** file:</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="29229-176">Klicken Sie bei Aufforderung auf **Load debug scripts**, um das Laden der Debugmanifeste zu akzeptieren:</span><span class="sxs-lookup"><span data-stu-id="29229-176">Accept the loading of Debug Manifests by clicking **Load debug scripts** when prompted:</span></span>

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-debug-scripts.png)

<span data-ttu-id="29229-178">Beachten Sie, dass die neue Schaltfläche in der Symbolleiste der Liste mit dem *Open Custom Dialog* zu Testzwecken angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="29229-178">Notice new button being visible in the toolbar of the list with test *Open Custom Dialog*.</span></span>

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-button-in-toolbar.png)

<span data-ttu-id="29229-180">Klicken Sie auf die Schaltfläche *Open Custom Dialog*, um das in der Listenansicht gerenderte benutzerdefinierte Dialogfeld anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="29229-180">Click *Open Custom Dialog* button to see custom dialog rendered in the list view.</span></span> 

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-visible-dialog.png)

<span data-ttu-id="29229-182">Wählen Sie in der *Farbauswahl* eine Farbe, und klicken Sie auf **OK**, um zu testen, wie der Code den ausgewählten Wert an den Aufrufer zurückgibt, der dann im vordefinierten Warnungsdialogfeld angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="29229-182">Choose a color in the *Color Picker* and click **OK** to test how the code is returning selected value back to caller, which is then shown using out-of-the-box alert dialog.</span></span>

![Vordefiniertes Warnungsdialogfeld](../../../../images/ext-com-dialog-oob-alert-dialog.png)
