# <a name="use-sp-pnp-js-with-sharepoint-framework-web-parts"></a><span data-ttu-id="6f088-101">Verwenden von sp-pnp-js mit SharePoint Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="6f088-101">Use sp-pnp-js with SharePoint Framework Web Parts</span></span>

<span data-ttu-id="6f088-p101">Sie können wählen, ob Sie die [sp-pnp-js](https://www.npmjs.com/package/sp-pnp-js)-Bibliothek beim Erstellen Ihrer SharePoint Framework-Webparts (SPFx) verwenden möchten. Diese Bibliothek bietet eine Fluent-API, um die Erstellung Ihrer REST-Abfragen intuitiv zu gestalten und die Batchverarbeitung und die Zwischenspeicherung zu unterstützen. Erfahren Sie mehr auf der [Projekt-Homepage](https://github.com/SharePoint/PnP-JS-Core), die Links zu Dokumentation, Beispielen und weiteren Ressourcen bieten, die Ihnen die ersten Schritte erleichtern.</span><span class="sxs-lookup"><span data-stu-id="6f088-p101">You may opt to use the [sp-pnp-js](https://www.npmjs.com/package/sp-pnp-js) library when building your SharePoint Framework web parts. This library provides a fluent API to make building your REST queries intuitive and supports batching and caching. You can learn more on the [project's homepage](https://github.com/SharePoint/PnP-JS-Core) which has links to documentation, samples, and other resources to help you get started.</span></span>

<span data-ttu-id="6f088-105">Sie können die [vollständige Quelle](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js) für diesen Artikel von der Beispielwebsite herunterladen.</span><span class="sxs-lookup"><span data-stu-id="6f088-105">You can download the [full source](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js) for this article from the samples site.</span></span>

## <a name="setup-your-environment"></a><span data-ttu-id="6f088-106">Einrichten der Umgebung</span><span class="sxs-lookup"><span data-stu-id="6f088-106">Setup your Environment</span></span>

<span data-ttu-id="6f088-107">Bevor Sie diesen Leitfaden abschließen können, müssen Sie sicherzustellen, dass Sie [die Umgebung](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) für die Entwicklung mit SharePoint Framework eingerichtet haben.</span><span class="sxs-lookup"><span data-stu-id="6f088-107">Before you can complete this guide you will need to ensure you have [setup your environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) for development using SharePoint Framework.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="6f088-108">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="6f088-108">Create a New Project</span></span>

<span data-ttu-id="6f088-109">Erstellen Sie zunächst einen neuen Ordners für das Projekt über eine Konsole Ihrer Wahl:</span><span class="sxs-lookup"><span data-stu-id="6f088-109">Start by creating a new folder for the project using your console of choice:</span></span>

```sh
md spfx-sp-pnp-js-example
```

<span data-ttu-id="6f088-110">Geben Sie diesen Ordner ein:</span><span class="sxs-lookup"><span data-stu-id="6f088-110">And enter that folder</span></span>

```sh
cd spfx-sp-pnp-js-example
```

<span data-ttu-id="6f088-111">Führen Sie dann den Yeoman-Generator für SPFx aus:</span><span class="sxs-lookup"><span data-stu-id="6f088-111">The run the Yeoman generator for SPFx</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="6f088-112">Geben Sie die folgenden Werte ein, sobald Sie während der Einrichtung des neuen Projekts dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="6f088-112">Enter the following values when prompted during the setup of your new project:</span></span>

- <span data-ttu-id="6f088-113">**spfx-sp-pnp-js-example** als Lösungsname (Standardwert beibehalten)</span><span class="sxs-lookup"><span data-stu-id="6f088-113">**spfx-sp-pnp-js-example** as solution name (keep default)</span></span>
- <span data-ttu-id="6f088-114">**Aktueller Ordner** als Speicherort der Lösung</span><span class="sxs-lookup"><span data-stu-id="6f088-114">**Current Folder** as the solution location</span></span>
- <span data-ttu-id="6f088-115">**Kockout** als Framework</span><span class="sxs-lookup"><span data-stu-id="6f088-115">**Kockout** as the framework</span></span>
- <span data-ttu-id="6f088-116">**SPPnPJSExample** als Name des Webparts</span><span class="sxs-lookup"><span data-stu-id="6f088-116">**SPPnPJSExample** as the name of the web part</span></span>
- <span data-ttu-id="6f088-117">**Beispiel zur Verwendung von sp-pnp-js in SPFx** als Beschreibung</span><span class="sxs-lookup"><span data-stu-id="6f088-117">**Example of using sp-pnp-js within SPFx** as the description</span></span>

![Erstellung des Projektgerüsts abgeschlossen](../../../../images/sp-pnp-js-guide-completed-setup.png)


<span data-ttu-id="6f088-p102">Nachdem der Bau des Gerüsts abgeschlossen wurde, öffnen Sie das Projekt im Code-Editor Ihrer Wahl. Die hier dargestellten Screenshots verwenden [Visual Studio Code](https://code.visualstudio.com/). Um das Verzeichnis in Visual Studio Code zu öffnen, geben Sie an der Konsole Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="6f088-p102">Once the scaffolding completes, open the project in the code editor of your choosing. The screenshots shown here demonstrate [Visual Studio Code](https://code.visualstudio.com/). To open the directory within Visual Studio Code, enter the following in the console:</span></span>

```sh
code .
```

![Projekt in Visual Studio Code geöffnet](../../../../images/sp-pnp-js-guide-first-open.png)

## <a name="install-and-setup-sp-pnp-js"></a><span data-ttu-id="6f088-123">Installieren und Einrichten von sp-pnp-js</span><span class="sxs-lookup"><span data-stu-id="6f088-123">Install And Setup sp-pnp-js</span></span>

<span data-ttu-id="6f088-p103">Nachdem Sie das Projekt erstellt haben, müssen Sie sp-pnp-js, beginnend mit der Installation des Pakets, installieren und einrichten. Diese Schritte gelten für alle Projekttypen (React usw.).</span><span class="sxs-lookup"><span data-stu-id="6f088-p103">Once your project is created you will need to install and setup sp-pnp-js, starting with installing the package. This section is common for any project type (React, etc).</span></span>

```sh
npm install sp-pnp-js --save
```

<span data-ttu-id="6f088-p104">Da die sp-pnp-js-Bibliothek REST-Anforderungen erstellt, muss sie die URL kennen, um diese Anforderung senden zu können. Bei der Arbeit mit herkömmlichen Websites und Webseiten kann die globale `_spPageContextInfo`-Variable verwendet werden. In SPFx ist diese nicht verfügbar bzw. ist möglicherweise nicht richtig. Daher wird das vom Framework bereitgestellte [context](https://dev.office.com/sharepoint/reference/spfx/sp-webpart-base/iwebpartcontext)-Objekt verwendet. Es gibt [zwei Möglichkeiten](https://github.com/SharePoint/PnP-JS-Core/wiki/Using-sp-pnp-js-in-SharePoint-Framework#establish-context), um sicherzustellen, dass Sie Ihre Anforderungen korrekt eingerichtet haben. In diesem Beispiel verwenden wir die `onInit`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6f088-p104">Because the sp-pnp-js library constructs REST requests it needs to know the URL to send these requests. When operating within classic sites and pages we can make use of the global _spPageContextInfo variable. Within SPFx this is not available, or if it is may not be correct. So we need to rely on the context object supplied by the framework. There are two ways to ensure you have correctly setup your requests, we'll use the onInit method in this example.</span></span>

### <a name="update-oninit-in-sppnpjsexamplewebpartts"></a><span data-ttu-id="6f088-131">Aktualisieren von onInit in SpPnPjsExampleWebPart.ts</span><span class="sxs-lookup"><span data-stu-id="6f088-131">Update onInit in SpPnPjsExampleWebPart.ts</span></span>

<span data-ttu-id="6f088-132">Öffnen Sie die Datei **src\webparts\spPnPjsExample\SpPnPjsExampleWebPart.ts**, und fügen Sie eine Importanweisung für das pnp-Stammobjekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="6f088-132">Open the src\webparts\spPnPjsExample\SpPnPjsExampleWebPart.ts file and add the import for the pnp root object.</span></span>

```TypeScript
import pnp from "sp-pnp-js";
```

<span data-ttu-id="6f088-p105">Aktualisieren Sie den Code in der `onInit`-Methode wie unten dargestellt. Der Block wird nach dem `super.onInit()`-Aufruf hinzugefügt. Dies geschieht nach `super.onInit`, um sicherzustellen, dass das Framework alles Erforderliche initialisieren kann, und dass die Bibliothek nach diesen Schritten eingerichtet werden kann.</span><span class="sxs-lookup"><span data-stu-id="6f088-p105">In the onInit method update the code to appear as below. We are adding the block after the super.onInit() call. We do this after the super.onInit to ensure that the framework has a chance to initialize anything required and that we are setting up the library after those steps are complete.</span></span>

```TypeScript
/**
 * Initialize the web part.
 */
protected onInit(): Promise<void> {
  this._id = _instance++;

  const tagName: string = `ComponentElement-${this._id}`;
  this._componentElement = this._createComponentElement(tagName);
  this._registerComponent(tagName);

  // When the web part description is changed, notify the view model to update.
  this._koDescription.subscribe((newValue: string) => {
    this._shouter.notifySubscribers(newValue, 'description');
  });

  const bindings: ISpPnPjsExampleBindingContext = {
    description: this.properties.description,
    shouter: this._shouter
  };

  ko.applyBindings(bindings, this._componentElement);

  return super.onInit().then(_ => {
    pnp.setup({
      spfxContext: this.context
    });
  });
}
```

## <a name="update-the-viewmodel"></a><span data-ttu-id="6f088-136">Aktualisieren von ViewModel</span><span class="sxs-lookup"><span data-stu-id="6f088-136">Update the ViewModel</span></span>

<span data-ttu-id="6f088-p106">Als Nächstes ersetzen Sie den Inhalt der Datei **SpPnPjsExampleViewModel.ts** durch den unten aufgeführten Code. Wir fügen eine Importanweisung für die pnp-Elemente, eine Schnittstelle zum Definieren der Elementfelder, einige Objekte des Typs „Observable“ zum Verfolgen der Elementliste und der neuen Elementform sowie schließlich Methoden, die das Abrufen, Hinzufügen und Löschen von Elementen unterstützen, hinzu. Wir haben außerdem eine `ensureList`-Methode hinzugefügt, die die sp-pnp-js `lists.ensure`-Methode verwendet, um stets sicherzustellen, dass wir die Liste haben (oder sie bei Bedarf zu erstellen). Es gibt viele Möglichkeiten, Ressourcen bereitzustellen; diese Methode wurde jedoch ausgewählt, um zu zeigen, wie eine Liste, ein Feld und Elemente mithilfe der Batchverarbeitung in einer einzigen Methode erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="6f088-p106">Next you will want to replace the contents of the SpPnPjsExampleViewModel.ts file with the below. We are adding an import for the pnp items, an interface to define our list item's fields, some observables to track both our list of items and new item form, and methods to support getting, adding, & deleting items. We also added an ensureList method which uses the sp-pnp-js lists.ensure method to always make sure we have the list. There are many ways to provision resources but this was done to demonstrate both creating a list, field, and items using batching in a single method.</span></span>

<span data-ttu-id="6f088-141">Festzuhalten ist, dass durch die Verwendung von sp-pnp-js weniger Code zur Verarbeitung der Anforderungen zu schreiben ist und mehr Zeit für die Geschäftslogik bleibt.</span><span class="sxs-lookup"><span data-stu-id="6f088-141">The takeaway is that using sp-pnp-js we write much less code to handle the requests and can focus on our business logic.</span></span>

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './ISpPnPjsExampleWebPartProps';
import pnp, { List, ListEnsureResult, ItemAddResult } from "sp-pnp-js";

export interface ISpPnPjsExampleBindingContext extends ISpPnPjsExampleWebPartProps {
  shouter: KnockoutSubscribable<{}>;
}

/**
 * Interface which defines the fields in our list items
 */
export interface OrderListItem {
  Id: number;
  Title: string;
  OrderNumber: string;
}

export default class SpPnPjsExampleViewModel {

  public description: KnockoutObservable<string> = ko.observable('');
  public newItemTitle: KnockoutObservable<string> = ko.observable('');
  public newItemNumber: KnockoutObservable<string> = ko.observable('');
  public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

  public labelClass: string = styles.label;
  public helloWorldClass: string = styles.helloWorld;
  public containerClass: string = styles.container;
  public rowClass: string = `ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`;
  public buttonClass: string = `ms-Button ${styles.button}`;

  constructor(bindings: ISpPnPjsExampleBindingContext) {
    this.description(bindings.description);

    // When the web part description is updated, change this view model's description.
    bindings.shouter.subscribe((value: string) => {
      this.description(value);
    }, this, 'description');

    // Load the items
    this.getItems().then(items => {

      this.items(items);
    });
  }

  /**
   * Gets the items from the list
   */
  private getItems(): Promise<OrderListItem[]> {

    return this.ensureList().then(list => {

      // Here we are using the getAs operator so that our returned value will be typed
      return list.items.select("Id", "Title", "OrderNumber").getAs<OrderListItem[]>();
    });
  }

  /**
   * Adds an item to the list
   */
  public addItem(): void {

    if (this.newItemTitle() !== "" && this.newItemNumber() !== "") {

      this.ensureList().then(list => {

        // Add the new item to the SharePoint list
        list.items.add({
          Title: this.newItemTitle(),
          OrderNumber: this.newItemNumber(),
        }).then((iar: ItemAddResult) => {

          // Add the new item to the display
          this.items.push({
            Id: iar.data.Id,
            OrderNumber: iar.data.OrderNumber,
            Title: iar.data.Title,
          });

          // Clear the form
          this.newItemTitle("");
          this.newItemNumber("");
        });
      });
    }
  }

  /**
   * Deletes an item from the list
   */
  public deleteItem(data): void {

    if (confirm("Are you sure you want to delete this item?")) {
      this.ensureList().then(list => {
        list.items.getById(data.Id).delete().then(_ => {
          this.items.remove(data);
        });
      }).catch((e: Error) => {
        alert(`There was an error deleting the item: ${e.message}`);
      });
    }
  }

  /**
   * Ensures the list exists. If not, it creates it and adds some default example data
   */
  private ensureList(): Promise<List> {

    return new Promise<List>((resolve, reject) => {

      // Use lists.ensure to always have the list available
      pnp.sp.web.lists.ensure("SPPnPJSExampleList").then((ler: ListEnsureResult) => {

        if (ler.created) {

          // We created the list on this call, so let's add a column
          ler.list.fields.addText("OrderNumber").then(_ => {

            // And we will also add a few items so we can see some example data
            // Here we use batching

            // Create a batch
            let batch = pnp.sp.web.createBatch();

            ler.list.getListItemEntityTypeFullName().then(typeName => {

              ler.list.items.inBatch(batch).add({
                Title: "Title 1",
                OrderNumber: "4826492"
              }, typeName);

              ler.list.items.inBatch(batch).add({
                Title: "Title 2",
                OrderNumber: "828475"
              }, typeName);

              ler.list.items.inBatch(batch).add({
                Title: "Title 3",
                OrderNumber: "75638923"
              }, typeName);

              // Excute the batched operations
              batch.execute().then(_ => {
                // All of the items have been added within the batch

                resolve(ler.list);

              }).catch(e => reject(e));

            }).catch(e => reject(e));

          }).catch(e => reject(e));

        } else {

          resolve(ler.list);
        }

      }).catch(e => reject(e));
    });
  }
}
```
## <a name="update-the-template"></a><span data-ttu-id="6f088-142">Aktualisieren der Vorlage</span><span class="sxs-lookup"><span data-stu-id="6f088-142">Update the Template</span></span>

<span data-ttu-id="6f088-p107">Schließlich müssen wir die Vorlage aktualisieren, um sie der Funktionalität anzupassen, die wir dem ViewModel hinzugefügt haben. Kopieren Sie den unten aufgeführten Code die Datei **SpPnPjsExample.template.html**. Wir haben eine Titelzeile sowie einen ForEach-Repeater für die Elementauflistung und ein Formular hinzugefügt, mit dem Sie neue Elemente zur Liste hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="6f088-p107">Finally we need to update the template to match the functionality we have added into the ViewModel. Copy the below code into the SpPnPjsExample.template.html file. We have added a title row, a foreach repeater for the items collection, and a form allowing you to add new items to the list.</span></span>

```html
<div data-bind="attr: {class:helloWorldClass}">
  <div data-bind="attr: {class:containerClass}">

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col ms-u-sm12">
        <span class="ms-font-xl ms-fontColor-white ms-fontWeight-semibold" data-bind="text: description"></span>
      </div>
    </div>

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Title</span>
      </div>
      <div class="ms-Grid-col  ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Order Number</span>
      </div>
    </div>

    <!-- ko foreach: items -->
    <div data-bind="attr: {class:$parent.rowClass}">
      <div class="ms-Grid-col ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white" data-bind="text: Title"></span>
      </div>
      <div class="ms-Grid-col  ms-u-sm5">
        <span class="ms-font-l ms-fontColor-white" data-bind="text: OrderNumber"></span>
      </div>
      <div class="ms-Grid-col  ms-u-sm1">
        <i class="ms-Icon ms-Icon--Delete" aria-hidden="true" data-bind="click: $parent.deleteItem.bind($parent, $data)"></i>
      </div>
    </div>
    <!-- /ko -->

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col  ms-u-sm12">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Add New</span>
      </div>
    </div>

    <div data-bind="attr: {class:rowClass}">
      <form data-bind="submit: addItem">
        <div class="ms-Grid-col ms-u-sm5">
          <input class="ms-TextField-field" placeholder="Title" data-bind='value: newItemTitle, valueUpdate: "afterkeydown"' />
        </div>
        <div class="ms-Grid-col ms-u-sm5">
          <input class="ms-TextField-field" placeholder="Order Number" data-bind='value: newItemNumber, valueUpdate: "afterkeydown"'
          />
        </div>
        <div class="ms-Grid-col ms-u-sm2">
          <button class="ms-Button--default ms-Button" type="submit" data-bind="enable: newItemTitle().length > 0 && newItemNumber().length > 0"><span class="ms-Button-label">Add</span></button>
        </div>
      </form>
    </div>

  </div>
</div>
```
## <a name="run-the-example"></a><span data-ttu-id="6f088-146">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="6f088-146">Run the Example</span></span>

<span data-ttu-id="6f088-147">Starten Sie das Beispiel, und fügen Sie das Webpart zu Ihrer in SharePoint gehosteten Workbench (/_layouts/workbench.aspx) hinzu, um es in Aktion sehen zu können.</span><span class="sxs-lookup"><span data-stu-id="6f088-147">Start the sample and add the web part to your SharePoint hosted workbench (/_layouts/workbench.aspx) to can see it in action.</span></span>

```sh
gulp serve --nobrowser
```

![Projekt bei der ersten Ausführung](../../../../images/sp-pnp-js-guide-first-run.png)

<span data-ttu-id="6f088-149">Sie können vorhandene Elemente löschen, indem Sie auf das Papierkorbsymbol klicken, oder neue Elemente hinzufügen, indem Sie Werte in beide Felder eingeben und auf die Schaltfläche „Hinzufügen“ klicken.</span><span class="sxs-lookup"><span data-stu-id="6f088-149">You can delete existing items by clicking on the trashcan icon, or add items by putting values in both fields and clicking the add button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f088-150">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6f088-150">Next Steps</span></span>

<span data-ttu-id="6f088-p108">Die sp-pnp-js-Bibliothek enthält eine große Palette an Funktionen und Erweiterungsoptionen. Im [Leitfaden für Entwickler](https://github.com/SharePoint/PnP-JS-Core/wiki/Developer-Guide) finden Sie Beispiele, Anleitungen und Tipps zur Verwendung und Konfiguration der Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="6f088-p108">The sp-pnp-js library contains a great range of functionality and extensibility. Please check out the [developer guide](https://github.com/SharePoint/PnP-JS-Core/wiki/Developer-Guide) for samples, guidance, and hints on using and configuring the library.</span></span>

## <a name="production-deployment"></a><span data-ttu-id="6f088-153">Bereitstellung in der Produktion</span><span class="sxs-lookup"><span data-stu-id="6f088-153">Production Deployment</span></span>

<span data-ttu-id="6f088-p109">Wenn Sie Ihre Lösung bereitstellen und mithilfe der Kennzeichnung `--ship` erstellen möchten, müssen Sie sp-pnp-js als externe Bibliothek in der Konfiguration markieren. Dies geschieht durch Aktualisierung der SPFx-Datei **config/config.js**, um diese Zeile in den Extern-Abschnitt einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="6f088-p109">When you are ready to deploy your solution and want to build using the --ship flag you need to mark sp-pnp-js as an external in the configuration. This is done by updating the SPFx config/config.js to include this line in the externals section:</span></span>

```
"sp-pnp-js": "https://cdnjs.cloudflare.com/ajax/libs/sp-pnp-js/2.0.1/pnp.min.js"
```

<span data-ttu-id="6f088-p110">In der oben aufgeführten Konfiguration verwenden wir das öffentliche CDN. Die URL kann jedoch auch ein interner Pfad oder ein anderer Speicherort sein, den Sie verwenden möchten. Achten Sie jedoch darauf, dass Sie die Versionsnummer in der URL so aktualisieren, dass sie mit der Zielversion übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="6f088-p110">Here we are using the public CDN but the URL can be internal or any location you would like to use. Be sure to update the version number in the url to match the version you want.</span></span>

## <a name="improving-the-example---mock-data"></a><span data-ttu-id="6f088-158">Verbessern des Beispiels - simulierte Daten</span><span class="sxs-lookup"><span data-stu-id="6f088-158">Improving the Example - Mock Data</span></span>

<span data-ttu-id="6f088-p111">Idealerweise funktioniert das Beispiel sowohl in der lokalen als auch in der von SharePoint gehosteten Workbench. Zur Aktivierung müssen wir das ViewModel simulieren und den Webpartcode, wie unten dargestellt, aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6f088-p111">Ideally the sample will work in both the local workbench as well as the SharePoint hosted. To enable this we need to mock our ViewModel and make an update to the web part code as outlined below.</span></span>

### <a name="mock-viewmodel"></a><span data-ttu-id="6f088-161">Simuliertes ViewModel</span><span class="sxs-lookup"><span data-stu-id="6f088-161">Mock ViewModel</span></span>

<span data-ttu-id="6f088-p112">Fügen Sie eine neue Datei mit dem Namen **MockSpPnPjsExampleViewModel.ts** zusammen mit den anderen Webpartdateien hinzu. Aktualisieren Sie dann den Inhalt dieser Datei mit dem unten aufgeführten Code. Damit erhalten Sie den gleichen Satz an Funktionen, ohne dass SharePoint verfügbar sein muss, und es funktioniert in der lokalen Umgebung.</span><span class="sxs-lookup"><span data-stu-id="6f088-p112">Add a new file named MockSpPnPjsExampleViewModel.ts along side the other web part files, then update the content to match the below. This will provide the same set of functionality but does not rely on SharePoint being available and will work in the local environment.</span></span>

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './ISpPnPjsExampleWebPartProps';
import pnp, { List, ListEnsureResult, ItemAddResult } from "sp-pnp-js";
import { ISpPnPjsExampleBindingContext, OrderListItem } from './SpPnPjsExampleViewModel';

export default class MockSpPnPjsExampleViewModel {

    public description: KnockoutObservable<string> = ko.observable('');
    public newItemTitle: KnockoutObservable<string> = ko.observable('');
    public newItemNumber: KnockoutObservable<string> = ko.observable('');
    public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

    public labelClass: string = styles.label;
    public helloWorldClass: string = styles.helloWorld;
    public containerClass: string = styles.container;
    public rowClass: string = `ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`;
    public buttonClass: string = `ms-Button ${styles.button}`;

    constructor(bindings: ISpPnPjsExampleBindingContext) {
        this.description(bindings.description);

        // When the web part description is updated, change this view model's description.
        bindings.shouter.subscribe((value: string) => {
            this.description(value);
        }, this, 'description');

        // Load the items
        this.getItems().then(items => {

            this.items(items);
        });
    }

    /**
     * Simulates getting the items from the list
     */
    private getItems(): Promise<OrderListItem[]> {
        return Promise.resolve([{
            Id: 1,
            Title: "Mock Item 1",
            OrderNumber: "12345"
        },
        {
            Id: 2,
            Title: "Mock Item 2",
            OrderNumber: "12345"
        },
        {
            Id: 3,
            Title: "Mock Item 3",
            OrderNumber: "12345"
        }]);
    }

    /**
     * Simulates adding an item to the list
     */
    public addItem(): void {

        if (this.newItemTitle() !== "" && this.newItemNumber() !== "") {

            // Add the new item to the display
            this.items.push({
                Id: this.items.length,
                OrderNumber: this.newItemNumber(),
                Title: this.newItemTitle(),
            });

            // Clear the form
            this.newItemTitle("");
            this.newItemNumber("");
        }
    }

    /**
     * Simulates deleting an item from the list
     */
    public deleteItem(data): void {

        if (confirm("Are you sure you want to delete this item?")) {
            this.items.remove(data);
        }
    }
}
```
### <a name="update-webpart"></a><span data-ttu-id="6f088-165">Aktualisieren des Webparts</span><span class="sxs-lookup"><span data-stu-id="6f088-165">Update Webpart</span></span>

<span data-ttu-id="6f088-p113">Abschließend muss das Webpart aktualisiert werden, um die simulierten Daten bei Bedarf verwenden zu können. Öffnen Sie die Datei **SpPnPjsExampleWebPart.ts**. Importieren Sie dann das simulierte ViewModell-Web, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6f088-p113">Finally we need to update the webpart to use the mock data when appropriate, to do so start by opening the SpPnPjsExampleWebPart.ts file. Start by importing the mock ViewModel web just created.</span></span>

```TypeScript
import MockSpPnPjsExampleViewModel from './MockSpPnPjsExampleViewModel';
```
<span data-ttu-id="6f088-169">Suchen Sie anschließend die `_registerComponent`-Methode, und aktualisieren Sie diese wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="6f088-169">Then locate the _registerComponent method and update it as shown below.</span></span>

```TypeScript
private _registerComponent(tagName: string): void {

  if (Environment.type === EnvironmentType.Local) {
    console.log("here I am.")
    ko.components.register(
      tagName,
      {
        viewModel: MockSpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  } else {
    ko.components.register(
      tagName,
      {
        viewModel: SpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  }
}
```
<span data-ttu-id="6f088-p114">Geben Sie dann `gulp serve` in der Konsole ein, um die lokale Workbench aufzurufen, die jetzt die simulierten Daten verwendet. (Falls der Server bereits ausgeführt wird, halten Sie ihn mit STRG+C an, und starten Sie ihn dann erneut.)</span><span class="sxs-lookup"><span data-stu-id="6f088-p114">Finally type gulp serve in the console to bring up the local workbench, which now will work with the mock data. (If you already have the server running stop it using Ctrl+C and then restart it)</span></span>

```sh
gulp serve
```

![Angezeigtes Projekt, das in der lokalen Workbench mit simulierten Daten ausgeführt wird](../../../../images/sp-pnp-js-guide-with-mock-data.png)


## <a name="download-full-example-code"></a><span data-ttu-id="6f088-173">Herunterladen des vollständigen Beispielcodes</span><span class="sxs-lookup"><span data-stu-id="6f088-173">Download Full Example Code</span></span>

<span data-ttu-id="6f088-174">Zur Erinnerung: Sie finden Sie das vollständige Beispiel [hier](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span><span class="sxs-lookup"><span data-stu-id="6f088-174">Remember you can find the full sample [here](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span></span>

## <a name="provide-feedback--report-issues"></a><span data-ttu-id="6f088-175">Geben Sie Feedback/Melden Sie Probleme</span><span class="sxs-lookup"><span data-stu-id="6f088-175">Provide Feedback / Report Issues</span></span>

<span data-ttu-id="6f088-176">Wenn Sie uns Ihr Feedback senden oder ein Problem mit sp-pnp-js melden möchten, verwenden Sie die [Problemliste](https://github.com/SharePoint/PnP-JS-Core/issues) in diesem Bericht.</span><span class="sxs-lookup"><span data-stu-id="6f088-176">If you have any feedback or need to report as issue with sp-pnp-js please use the [issues list](https://github.com/SharePoint/PnP-JS-Core/issues) in that repo.</span></span>
