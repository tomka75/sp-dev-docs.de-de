# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a><span data-ttu-id="e3df3-101">Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="e3df3-101">Use custom dialog boxes with SharePoint Framework Extensions</span></span>

<span data-ttu-id="e3df3-102">Benutzerdefinierte Dialogfelder können im Kontext von SharePoint Framework-Erweiterungen oder im Kontext von clientseitigen Webparts verwendet werden. Sie sind über das Paket **@microsoft/sp-dialog** verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e3df3-102">You can use custom dialog boxes, available from the **@microsoft/sp-dialog** package, within the context of SharePoint Framework Extensions or client-side web parts.</span></span> 

<span data-ttu-id="e3df3-103">In diesem Artikel wird beschrieben, wie Sie ein benutzerdefiniertes Dialogfeld erstellen und im Kontext einer Erweiterung des Typs „ListView Command Set“ verwenden können.</span><span class="sxs-lookup"><span data-stu-id="e3df3-103">This article describes how to create a custom dialog box and use it within the context of a ListView Command Set extension.</span></span>

><span data-ttu-id="e3df3-p101">**Hinweis:** Das Feature zur Erstellung benutzerdefinierter Dialogfelder befindet sich derzeit in der Preview-Phase. Wir würden uns vor der Freigabe über Ihr Feedback freuen. Wenn Sie uns Feedback senden möchten, können Sie [ein Ticket in unserem GitHub-Repository erstellen](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="e3df3-p101">**Note:** The custom dialog box feature is currently in preview. We are looking for your feedback before we release. To provide feedback, [file an issue in our GitHub repo](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

> <span data-ttu-id="e3df3-107">Beachten Sie, dass das Debuggen von benutzerdefinierten Erweiterungen des Typs „ListView Command Set“ in SharePoint Online derzeit nur über die moderne Listenoberfläche auf klassischen Teamwebsites möglich ist, die in einem **Entwicklermandanten** gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="e3df3-107">Please note that debugging Custom ListView Command Sets in SharePoint Online is currently only available from the modern list experience within classic team sites hosted in a **developer tenant**.</span></span>


<span data-ttu-id="e3df3-108">Den Beispielcode, auf den in diesem Artikel Bezug genommen wird, finden Sie in unserem [Repository](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).</span><span class="sxs-lookup"><span data-stu-id="e3df3-108">You can access the sample code that this article is based on in the [](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog) repo.</span></span>

## <a name="set-up-your-development-environment"></a><span data-ttu-id="e3df3-109">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="e3df3-109">Set up your development environment</span></span>

<span data-ttu-id="e3df3-p102">Zur Erstellung eines benutzerdefinierten Dialogfelds müssen Sie zunächst die Schritt-für-Schritt-Anleitung im Artikel zum Thema [Einrichten Ihrer Entwicklungsumgebung](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) befolgen. Stellen Sie sicher, dass Sie die neuesten SharePoint Framework-Yeoman-Vorlagen verwenden.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p102">To create a custom dialog box, you'll need to follow the steps in the [Set up your development environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment). Make sure that you're using the latest SharePoint Framework Yeoman templates.</span></span> 

<span data-ttu-id="e3df3-112">Aktualisieren können Sie Ihre SharePoint Framework-Yeoman-Vorlagen mit dem folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="e3df3-112">To update your SharePoint Framework Yeoman templates, run the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint`
```

## <a name="create-a-new-project"></a><span data-ttu-id="e3df3-113">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="e3df3-113">Create a new project</span></span>

<span data-ttu-id="e3df3-114">Erstellen Sie über eine Konsole Ihrer Wahl einen neuen Ordner für das Projekt:</span><span class="sxs-lookup"><span data-stu-id="e3df3-114">Start by creating a new folder for the project using your console of choice:</span></span>

```sh
md dialog-cmd
```

<span data-ttu-id="e3df3-115">Wechseln Sie nun in diesen Ordner:</span><span class="sxs-lookup"><span data-stu-id="e3df3-115">And enter that folder</span></span>

```sh
cd dialog-cmd
```

<span data-ttu-id="e3df3-116">Führen Sie den Yeoman-Generator für SharePoint Framework aus:</span><span class="sxs-lookup"><span data-stu-id="e3df3-116">Run the Yeoman generator for the SharePoint Framework:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="e3df3-117">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="e3df3-117">When prompted:</span></span>

* <span data-ttu-id="e3df3-118">Übernehmen Sie den Standardwert **dialog-cmd** als Namen der Lösung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e3df3-118">Accept the default value of **command-extension** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="e3df3-119">Wählen Sie **Extension (Preview)** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="e3df3-119">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="e3df3-120">Wählen Sie **ListView Command Set (Preview)** als den zu erstellenden Typ von Erweiterung aus.</span><span class="sxs-lookup"><span data-stu-id="e3df3-120">Choose **ListView Command Set (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="e3df3-121">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:</span><span class="sxs-lookup"><span data-stu-id="e3df3-121">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="e3df3-122">Übernehmen Sie den Wert **DialogDemo** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e3df3-122">Accept the default value of **HelloWorld** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="e3df3-123">Übernehmen Sie den Standardwert **DialogDemo description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e3df3-123">Accept the default value of **HelloWorld description** as your extension description and press **Enter**.</span></span>

![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../../images/ext-com-dialog-yeoman-prompts.png)

<span data-ttu-id="e3df3-p103">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die *DialogDemo*-Erweiterung. Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the *HelloWorld* extension. This might take a few minutes.</span></span> 

<span data-ttu-id="e3df3-127">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="e3df3-127">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-com-dialog-yeoman-complete.png)

><span data-ttu-id="e3df3-129">**Hinweis:** Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="e3df3-129">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

<span data-ttu-id="e3df3-p104">Öffnen Sie nach dem Abschluss der Gerüsterstellung den Projektordner in Ihrem Code-Editor. Für die Anleitung in diesem Artikel haben wir Visual Studio Code verwendet; auch die Screenshots entstammen diesem Editor. Sie können jedoch auch jeden beliebigen anderen Editor verwenden. Führen Sie den folgenden Befehl in der Konsole aus, um den Ordner in Visual Studio Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="e3df3-p104">When the scaffolding is complete, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots, but you can use any editor you prefer. To open the folder in Visual Studio Code, use the following command in the console:</span></span>

```sh
code .
```

![Anfängliche Visual Studio Code-Struktur nach der Gerüsterstellung](../../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a><span data-ttu-id="e3df3-134">Ändern des Erweiterungsmanifests</span><span class="sxs-lookup"><span data-stu-id="e3df3-134">Modify the extension manifest</span></span>

<span data-ttu-id="e3df3-p105">Konfigurieren Sie die Erweiterung im Erweiterungsmanifest so, dass sie nur eine Schaltfläche hat. Öffnen Sie dazu im Code-Editor die Datei **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**, und ersetzen Sie den Befehlsabschnitt durch den folgenden JSON-Code:</span><span class="sxs-lookup"><span data-stu-id="e3df3-p105">In the extension manifest, configure the extension to have only one button. In the code editor, open the **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json** file. Replace the commands section with the following JSON:</span></span>

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

## <a name="add-the-sp-dialog-package-to-the-solution"></a><span data-ttu-id="e3df3-138">Hinzufügen des Pakets „sp-dialog“ zur Lösung</span><span class="sxs-lookup"><span data-stu-id="e3df3-138">Add the sp-dialog package to the solution</span></span>

<span data-ttu-id="e3df3-139">Wechseln Sie wieder zur Konsole, und führen Sie den folgenden Befehl aus, um die Dialogfeld-API in die Lösung einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="e3df3-139">Return to the console and execute the following command to include the dialog API in our solution.</span></span>

```sh
npm install @microsoft/sp-dialog --save
```

<span data-ttu-id="e3df3-p106">Da Sie die Option `--save` verwenden, wird diese Abhängigkeit der Datei **package.json** hinzugefügt. Dadurch wird sichergestellt, dass sie automatisch installiert wird, sobald der Befehl `npm install` ausgeführt wird. (Das ist wichtig, wenn Sie das Projekt an einen anderen Speicherort wiederherstellen oder klonen möchten.)</span><span class="sxs-lookup"><span data-stu-id="e3df3-p106">Because you're using the `--save` option, this dependency will be added to the **package.json** file. This ensures that it will be installed automatically when the `npm install` command runs (this is important when you restore or clone your project elsewhere).</span></span>

<span data-ttu-id="e3df3-142">Wechseln Sie wieder zu Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="e3df3-142">Return to Visual Studio Code (or your preferred editor).</span></span>

## <a name="create-a-custom-dialog-box"></a><span data-ttu-id="e3df3-143">Erstellen eines benutzerdefinierten Dialogfelds</span><span class="sxs-lookup"><span data-stu-id="e3df3-143">Create a custom dialog box</span></span>

<span data-ttu-id="e3df3-144">Erstellen Sie eine neue Datei mit dem Namen **ColorPickerDialog.tsx** im Ordner **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="e3df3-144">Create a new file called **ColorPickerDialog.tsx** in the **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="e3df3-p107">Fügen Sie die folgenden Importanweisungen am Anfang der neu erstellten Datei ein. Da Sie das benutzerdefinierte Dialogfeld mithilfe von [Office UI Fabric React-Komponenten](https://dev.office.com/fabric#/components) erstellen, nutzen Sie React zur Implementierung.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p107">Add the following import statements at the top of the newly created file. You're creating your custom dialog box using the [Office UI Fabric React components](https://dev.office.com/fabric#/components), so the implementation will be in React.</span></span> 

> <span data-ttu-id="e3df3-147">**Hinweis:** Die Komponente `DialogContent` wird derzeit über `@microsoft/sp-dialog` bereitgestellt, sie wird jedoch in Kürze in die Office UI Fabric React-Komponenten aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="e3df3-147">**Note:** Currently the `DialogContent` component is coming from `@microsoft/sp-dialog`, but it will be included as part of the Office UI Fabric React components soon.</span></span> 

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

<span data-ttu-id="e3df3-p108">Fügen Sie die nachfolgende Schnittstellendefinition direkt unterhalb der Importanweisungen ein. Sie regelt die Übergabe von Informationen und Funktionen zwischen Ihrer Erweiterung des Typs „ListView Command Set“ und Ihrem benutzerdefinierten Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p108">Add the following interface definition just below the import statements. This will be used to pass information and functions between your ListView Command Set extension and your custom dialog box.</span></span>

```ts
interface IColorPickerDialogContentProps {
  message: string;
  close: () => void;
  submit: (color: string) => void;
  defaultColor?: string;
}
```

<span data-ttu-id="e3df3-p109">Fügen Sie die nachfolgende Klasse direkt unterhalb der Schnittstellendefinition ein. Diese React-Klasse ist für das Rendern der Benutzeroberfläche im benutzerdefinierten Dialogfeld zuständig. Wie Sie sehen, werden zum eigentlichen Rendern die Office UI Fabric React-Komponenten verwendet. Die erforderlichen Eigenschaften werden lediglich übergeben.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p109">Add the following class just below the interface definition. This React class is responsible for rendering the UI experiences inside the custom dialog box. Notice that you use the Office UI Fabric React components for actual rendering and just pass the needed properties.</span></span>  

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
<span data-ttu-id="e3df3-p110">Fügen Sie die nachfolgende Klassendefinition für das benutzerdefinierte Dialogfeld direkt unterhalb der Klasse `ColorPickerDialogContent` ein, die Sie soeben hinzugefügt haben. Hierbei handelt es sich um das eigentliche benutzerdefinierte Dialogfeld, das über einen Klick auf die durch die Erweiterung des Typs „ListView Command Set“ implementierte Schaltfläche aufgerufen wird und von `BaseDialog` vererbt wird.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p110">Add the following class definition for your custom dialog box under the `ColorPickerDialogContent` class that you just added. This is the actual custom dialog box that will be called from the ListView Command Set button click and is inherited from the `BaseDialog`.</span></span>

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

## <a name="associate-the-custom-dialog-box-with-the-listview-command-set-button-click"></a><span data-ttu-id="e3df3-155">Verknüpfen des benutzerdefinierten Dialogfelds mit dem Klickereignis für die per „ListView Command Set“ implementierte Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="e3df3-155">Associate the custom dialog box with the ListView Command Set button click</span></span>
<span data-ttu-id="e3df3-156">Zur Verknüpfung des benutzerdefinierten Dialogfelds mit Ihrer benutzerdefinierten Erweiterung des Typs „ListView Command Set“ fügen Sie nun den zur Initiierung des Dialogfelds erforderlichen Code in die Klickoperation der Schaltfläche ein.</span><span class="sxs-lookup"><span data-stu-id="e3df3-156">To associate the custom dialog box with your custom ListView Command Set, add the code to initiate the dialog box within the button click operation.</span></span>

<span data-ttu-id="e3df3-157">Öffnen Sie im Code-Editor die Datei **DialogDemoCommandSet.ts** im Ordner **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="e3df3-157">In the code editor, open the **DialogDemoCommandSet.ts** file from the **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="e3df3-p111">Fügen Sie die nachfolgenden Importanweisungen unter der bereits vorhandenen **strings**-Importanweisung hinzu. Über die neuen Importanweisungen kann das benutzerdefinierte Dialogfeld im Kontext der Erweiterung des Typs „ListView Command Set“ verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p111">Add the following import statements under the existing **strings** import. These are for using the custom dialog box in the context of your ListView Command Set.</span></span> 

```ts
import { Dialog } from '@microsoft/sp-dialog';
import ColorPickerDialog from './ColorPickerDialog';
```

<span data-ttu-id="e3df3-p112">Fügen Sie die nachfolgende Variablendefinition `_colorCode` oberhalb der Funktion `onInit` in die Klasse `DialogDemoCommandSet` ein. Sie speichert den Rückgabewert aus dem Farbauswahl-Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p112">Add the following `_colorCode` variable definition above the `onInit` function in the `DialogDemoCommandSet` class. This is used to store the color picker dialog box result.</span></span>

```ts
  private _colorCode: string;
```

<span data-ttu-id="e3df3-p113">Aktualisieren Sie die Funktion `onExecute` wie unten dargestellt. Dieser Code führt folgende Aktionen durch:</span><span class="sxs-lookup"><span data-stu-id="e3df3-p113">Update the `onExecute` function as follows. This code does the following:</span></span>

* <span data-ttu-id="e3df3-164">Er initiiert das benutzerdefinierte Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="e3df3-164">Initiates the custom dialog box.</span></span>
* <span data-ttu-id="e3df3-165">Er übergibt eine Nachricht an das Dialogfeld, die als Titel verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e3df3-165">Passes a message for the dialog box, which is used for the title.</span></span>
* <span data-ttu-id="e3df3-166">Er übergibt einen Farbcode an das Dialogfeld (den Standardwert, falls nicht anders festgelegt).</span><span class="sxs-lookup"><span data-stu-id="e3df3-166">Passed a color code for the dialog box with a default value, if not yet set.</span></span>
* <span data-ttu-id="e3df3-167">Er rendert das benutzerdefinierte Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="e3df3-167">Shows the custom dialog box.</span></span>
* <span data-ttu-id="e3df3-168">Er empfängt und speichert den Rückgabewert des Dialogfelds.</span><span class="sxs-lookup"><span data-stu-id="e3df3-168">Receives and stores the return value from the dialog box.</span></span>
* <span data-ttu-id="e3df3-169">Er zeigt den empfangenen Wert mithilfe der Funktion `Dialog.alert()` in einem Standarddialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="e3df3-169">Shows the received value in a default dialog box using the `Dialog.alert()` function.</span></span>

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

## <a name="test-the-custom-dialog-box-in-your-tenant"></a><span data-ttu-id="e3df3-170">Testen des benutzerdefinierten Dialogfelds im Mandanten</span><span class="sxs-lookup"><span data-stu-id="e3df3-170">Test the custom dialog box in your tenant</span></span>

<span data-ttu-id="e3df3-171">Öffnen Sie die Datei **DialogDemoCommandSet.manifest.json** im Ordner **./src/extensions/dialogDemo/**, und kopieren Sie den **id**-Wert. Ihn müssen Sie im Abfrageparameter für das Debuggen angeben.</span><span class="sxs-lookup"><span data-stu-id="e3df3-171">Open the **DialogDemoCommandSet.manifest.json** file in the **./src/extensions/dialogDemo/** folder and copy the **id** value, which will be used in the debug query parameter.</span></span>

<span data-ttu-id="e3df3-172">Wechseln Sie zurück zur Konsole, und führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="e3df3-172">Return to the console and run the following command:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="e3df3-p114">Wie Sie sehen, verwenden Sie die Option `--nobrowser`. Ein Aufrufen der lokalen Workbench ist nicht nötig, da Erweiterungen derzeit nicht lokal debuggt werden können.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p114">Notice that you use the `--nobrowser` option. You don't need to launch the local workbench because you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="e3df3-175">Nun wird die Bündelung der Lösung angestoßen, und das resultierende Manifest wird von der `localhost`-Adresse ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="e3df3-175">This will start the bundling of your solution and will serve the resulting manifest from the `localhost` address.</span></span>

![Anfängliche Visual Studio Code-Struktur nach der Gerüsterstellung](../../../../images/ext-com-dialog-gulp-serve.png)

<span data-ttu-id="e3df3-177">Navigieren Sie nun zu einer Website in Ihrem SharePoint Online-Entwicklermandanten, um Ihre Erweiterung zu testen.</span><span class="sxs-lookup"><span data-stu-id="e3df3-177">To test your extension, navigate to a site in your SharePoint Online tenant.</span></span>

<span data-ttu-id="e3df3-178">Rufen Sie auf der Website eine bereits vorhandene benutzerdefinierte Liste mit Elementen auf. Sie können auch eine neue Liste erstellen und ihr zu Testzwecken einige Elemente hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="e3df3-178">Go to an existing custom list within the site that contains some items, or create a new list and add a few items to it for testing purposes.</span></span> 

<span data-ttu-id="e3df3-p115">Fügen Sie die nachfolgenden Abfragezeichenfolgenparameter an die URL an. Beachten Sie, dass Sie den **id**-Wert mit dem Bezeichner Ihrer Erweiterung aus der Datei **DialogDemoCommandSet.manifest.json** aktualisieren müssen:</span><span class="sxs-lookup"><span data-stu-id="e3df3-p115">Append the following query string parameters to the URL. Notice that you will need to update the id to match your own extension identifier available from the **HelloWorldFieldCustomizer.manifest.json** file:</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="e3df3-181">Klicken Sie bei Aufforderung auf **Load debug scripts**, um das Laden der Debugmanifeste zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="e3df3-181">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-debug-scripts.png)

<span data-ttu-id="e3df3-183">Sie sehen: Die neue Schaltfläche wird jetzt auf der Symbolleiste der Liste angezeigt, mit dem Text *Open Custom Dialog*.</span><span class="sxs-lookup"><span data-stu-id="e3df3-183">Notice that the new button is visible in the toolbar of the list with the text *Open Custom Dialog box*.</span></span>

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-button-in-toolbar.png)

<span data-ttu-id="e3df3-185">Klicken Sie auf die Schaltfläche *Open Custom Dialog*. Ihr benutzerdefiniertes Dialogfeld wird nun in der Listenansicht gerendert.</span><span class="sxs-lookup"><span data-stu-id="e3df3-185">Choose the *Open Custom Dialog box* button to see your custom dialog box rendered within the list view.</span></span> 

![Warnung zum Zulassen von Debugskripts](../../../../images/ext-com-dialog-visible-dialog.png)

<span data-ttu-id="e3df3-p116">Wählen Sie in der *Farbauswahl* eine Farbe aus, und klicken Sie auf **OK**, um zu testen, wie der Code den ausgewählten Wert an den Aufrufer zurückgibt. Die Auswahl wird anschließend in einem Standarddialogfeld „Alert“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e3df3-p116">Choose a color in the *Color Picker* and choose **OK** to test how the code is returning the selected value back to the caller. The selection is then shown using the default alert dialog box.</span></span>

![Standarddialogfeld „Alert“](../../../../images/ext-com-dialog-oob-alert-dialog.png)
