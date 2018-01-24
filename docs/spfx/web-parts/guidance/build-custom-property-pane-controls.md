---
title: "Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich"
description: "Erfahren Sie, wie Sie ein benutzerdefiniertes Dropdown-Steuerelement erstellen können, das seine Daten asynchron aus einem externen Dienst lädt, ohne die Benutzeroberfläche Ihres clientseitigen SharePoint-Webparts zu blockieren."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: 0e17ad3d494ec24608ff167539018919591c9688
ms.sourcegitcommit: 1f1044e59d987d878bb8bc403413e3090234ad44
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2018
---
# <a name="build-custom-controls-for-the-property-pane"></a><span data-ttu-id="b4a4b-103">Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="b4a4b-103">Build custom controls for the property pane</span></span>

<span data-ttu-id="b4a4b-104">Das SharePoint-Framework enthält eine Reihe von Standardsteuerelementen für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-104">The SharePoint Framework contains a set of standard controls for the property pane.</span></span> <span data-ttu-id="b4a4b-105">Manchmal jedoch benötigen Sie zusätzliche Funktionen, die über die grundlegenden Steuerelemente hinausgehen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-105">But sometimes you need additional functionality beyond the basic controls.</span></span> <span data-ttu-id="b4a4b-106">Vielleicht sollen beispielsweise die Daten in einem Steuerelement oder einer bestimmten Benutzeroberfläche asynchron aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-106">You might need asynchronous updates to the data on a control or a specific user interface.</span></span> <span data-ttu-id="b4a4b-107">Dann können Sie ein benutzerdefiniertes Steuerelement für den Eigenschaftenbereich erstellen, um die benötigten Funktionen zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-107">Build a custom control for the property pane to get the functionality you need.</span></span>

<span data-ttu-id="b4a4b-108">In diesem Artikel erstellen Sie ein benutzerdefiniertes Dropdown-Steuerelement, das seine Daten asynchron aus einem externen Dienst lädt, ohne die Benutzeroberfläche des Webparts zu blockieren.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-108">In this article you will learn how to build a custom control for the property pane. You will build a custom dropdown control that loads its data asynchronously from an external service without blocking the user interface of the web part.</span></span>

![Elementdropdown, das nach der Auswahl einer Liste im Listendropdown die verfügbaren Elemente lädt](../../../images/custom-property-pane-control-cascading-loading-items.png)

<span data-ttu-id="b4a4b-110">Der Quellcode des Webparts, mit dem wir arbeiten, steht auf GitHub zur Verfügung, unter [sp-dev-fx-webparts/samples/react-custompropertypanecontrols](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span><span class="sxs-lookup"><span data-stu-id="b4a4b-110">The source of the working web part is available on GitHub at [(https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols)](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span></span>

> [!NOTE] 
> <span data-ttu-id="b4a4b-111">Bevor Sie die Anleitung in diesem Artikel umsetzen können, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint-Framework-Lösungen erstellen können.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-111">Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment.md) for building SharePoint Framework solutions.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="b4a4b-112">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="b4a4b-112">Create new project</span></span>

1. <span data-ttu-id="b4a4b-113">Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-113">Start by creating a new folder for your project</span></span>

  ```sh
  md react-custompropertypanecontrol
  ```

2. <span data-ttu-id="b4a4b-114">Wechseln Sie in den Projektordner:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-114">Go to the project folder:</span></span>

  ```sh
  cd react-custompropertypanecontrol
  ```

3. <span data-ttu-id="b4a4b-115">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-115">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="b4a4b-116">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-116">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="b4a4b-117">**react-custompropertypanecontrol** als Lösungsname</span><span class="sxs-lookup"><span data-stu-id="b4a4b-117">**react-custompropertypanecontrol** as your solution name</span></span>
  - <span data-ttu-id="b4a4b-118">**Aktuellen Ordner verwenden** als Speicherort für die Dateien</span><span class="sxs-lookup"><span data-stu-id="b4a4b-118">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="b4a4b-119">**Listenelemente** als Namen des Webparts</span><span class="sxs-lookup"><span data-stu-id="b4a4b-119">**List items** as your web part name</span></span>
  - <span data-ttu-id="b4a4b-120">**Zeigt Listenelemente aus der ausgewählten Liste an** als Beschreibung Ihres Webparts</span><span class="sxs-lookup"><span data-stu-id="b4a4b-120">**Shows list items from the selected list** as your web part description</span></span>
  - <span data-ttu-id="b4a4b-121">**React** als Eintrittspunkt für die Webpart-Erstellung</span><span class="sxs-lookup"><span data-stu-id="b4a4b-121">**React** as the starting point to build the web part</span></span>

  ![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/custom-property-pane-control-yeoman.png)

5. <span data-ttu-id="b4a4b-123">Warten Sie, bis das Gerüst erstellt wurde, und sperren Sie dann mithilfe des folgenden Befehls die Version der Projektabhängigkeiten:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-123">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="b4a4b-124">Öffnen Sie den Projektordner in einem Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-124">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="b4a4b-125">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch auch jeden beliebigen anderen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-125">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

  ![SharePoint-Framework-Projekt in Visual Studio Code](../../../images/custom-property-pane-control-visual-studio-code.png)

## <a name="define-web-part-property-for-storing-the-selected-list"></a><span data-ttu-id="b4a4b-127">Definieren der Webparteigenschaft zum Speichern der ausgewählten Liste</span><span class="sxs-lookup"><span data-stu-id="b4a4b-127">Define web part property for storing the selected list</span></span>

<span data-ttu-id="b4a4b-128">In dem Webpart, das Sie erstellen, werden Listenelemente aus der jeweils ausgewählten SharePoint-Liste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-128">The web part you are building shows list items from the selected SharePoint list.</span></span> <span data-ttu-id="b4a4b-129">Benutzer können die gewünschte Liste im Eigenschaftenbereich des Webparts auswählen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-129">Users are able to select a list in the web part properties.</span></span> <span data-ttu-id="b4a4b-130">Erstellen Sie eine neue Webparteigenschaft namens **listName**, in der die ausgewählte Liste gespeichert wird:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-130">To store the selected list, create a new web part property named **listName**.</span></span>

1. <span data-ttu-id="b4a4b-p104">Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPartManifest.json** Ersetzen Sie die Standardeigenschaft **description** durch eine neue Eigenschaft mit dem Namen `listName`.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p104">In the code editor, open the **src/webparts/listItems/ListItemsWebPartManifest.json** file. Replace the default **description** property with a new property named `listName`.</span></span>

  ![Webpartmanifest mit hervorgehobener Webparteigenschaft „listName“](../../../images/custom-property-pane-control-list-property-web-part-manifest.png)

2. <span data-ttu-id="b4a4b-134">Öffnen Sie die Datei **src/webparts/listItems/IListItemsWebPartProps.ts**, und ersetzen Sie den in ihr enthaltenen Code durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-134">Next, open the **src/webparts/listItems/IListItemsWebPartProps.ts** file and replace its contents with:</span></span>

  ```ts
  export interface IListItemsWebPartProps {
    listName: string;
  }
  ```

3. <span data-ttu-id="b4a4b-135">Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** die Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-135">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the **render** method to:</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
        listName: this.properties.listName
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

4. <span data-ttu-id="b4a4b-136">Aktualisieren Sie die Methode **getPropertyPaneConfiguration** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-136">Update the **getPropertyPaneConfiguration** method to:</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: [
                  PropertyPaneTextField('listName', {
                    label: strings.ListFieldLabel
                  })
                ]
              }
            ]
          }
        ]
      };
    }
    // ...
  }
  ```

5. <span data-ttu-id="b4a4b-137">Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die Schnittstelle **IListItemsWebPartStrings** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-137">In the **src/webparts/listItems/loc/mystrings.d.ts** file change the **IListItemsWebPartStrings** interface to:</span></span>

  ```ts
  declare interface IListItemsWebPartStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListFieldLabel: string;
  }
  ```

6. <span data-ttu-id="b4a4b-138">Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ListFieldLabel** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-138">In the **src/webparts/listItems/loc/en-us.js** file add the missing definition for the **ListFieldLabel** string.</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListFieldLabel": "List"
    }
  });
  ```

7. <span data-ttu-id="b4a4b-139">Ändern Sie in der Datei **src/webparts/listItems/components/ListItems.tsx** den Code der Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-139">In the **src/webparts/listItems/components/ListItems.tsx** file, change the contents of the **render** method to:</span></span>

  ```tsx
  export default class ListItems extends React.Component<IListItemsProps, {}> {
    public render(): React.ReactElement<IListItemsProps> {
      return (
        <div className={styles.listItems}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-lg10 ms-xl8 ms-xlPush2 ms-lgPush1">
                <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
                <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
                <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
                <a href="https://aka.ms/spfx" className={styles.button}>
                  <span className={styles.label}>Learn more</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      );
    }
  }
  ```

8. <span data-ttu-id="b4a4b-140">Öffnen Sie die Datei **src/webparts/listItems/components/IListItemsProps.ts**, und ersetzen Sie den in ihr enthaltenen Code durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-140">Next, open the **src/webparts/listItems/components/IListItemsProps.ts** file and replace its contents with:</span></span>

  ```ts
  export interface IListItemsProps {
    listName: string;
  }
  ```

9. <span data-ttu-id="b4a4b-141">Führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Projekt ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-141">Run the following command to verify that the project is running:</span></span>

  ```sh
  gulp serve
  ```

10. <span data-ttu-id="b4a4b-p105">Fügen Sie im Webbrowser das **Listenelement**-Webpart zum Zeichenbereich hinzu, und öffnen Sie die Eigenschaften. Überprüfen Sie, dass der für die **List**-Eigenschaft festgelegte Wert im Webparttext angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p105">In the web browser, add the **List items** web part to the canvas and open its properties. Verify that the value set for the **List** property is displayed in the web part body.</span></span>

  ![Webpart, in dem der Wert der listName-Eigenschaft angezeigt wird](../../../images/custom-property-pane-control-web-part-first-run.png)


## <a name="create-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="b4a4b-145">Erstellen eines asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="b4a4b-145">Create asynchronous dropdown property pane control</span></span>

<span data-ttu-id="b4a4b-p106">Das SharePoint Framework bietet Ihnen ein standardmäßiges Dropdown-Steuerelement, mit dem Benutzer einen bestimmten Wert auswählen können. Das Dropdown-Steuerelement wurde so konzipiert, dass all seine Werte vorab bekannt sein müssen. Wenn die Werte dynamisch geladen werden sollen oder Sie die Werte asynchron aus einem externen Dienst laden und nicht das ganze Webpart blockieren möchten, besteht eine Möglichkeit darin, ein Dropdown-Steuerelement zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p106">The SharePoint Framework offers you a standard dropdown control that allows users to select a specific value. The dropdown control is built in a way that requires all its values to be known upfront. If you want to load the values dynamically or you're loading values asynchronously from an external service and you don't want to block the whole web part, building a custom dropdown control is a viable option.</span></span>

<span data-ttu-id="b4a4b-149">Wenn Sie ein benutzerdefiniertes Eigenschaftenbereichssteuerelement erstellen, das React im SharePoint Framework verwendet, besteht das Steuerelement aus einer Klasse, die das Steuerelement bei dem Webpart registriert, und einer React-Komponente, die das Dropdown rendert und seine Daten verwaltet.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-149">When creating a custom property pane control that uses React in the SharePoint Framework, the control consists of a class that registers the control with the web part, and a React component that renders the dropdown and manages its data.</span></span>

> [!NOTE] 
> <span data-ttu-id="b4a4b-150">Ab Drop  6 des SharePoint-Framework gibt es einen Bug in der Office UI Fabric React-Dropdownkomponente, aufgrund dessen das in diesem Artikel erstellte Steuerelement nicht korrekt funktioniert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-150">In drop 6 of the SharePoint Framework there is a bug in the Office UI Fabric React Dropdown component that causes the control built in this article to work incorrectly.</span></span> <span data-ttu-id="b4a4b-151">Eine temporäre Problemumgehung besteht darin, in der Datei **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** die Zeile **12027** zu ändern, und zwar von:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-151">A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line **12027** from:</span></span>
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="b4a4b-152">in:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-152">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

### <a name="add-asynchronous-dropdown-property-pane-control-react-component"></a><span data-ttu-id="b4a4b-153">Hinzufügen eines React-basierten asynchronen Dropdown-Steuerelements zum Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="b4a4b-153">Add asynchronous dropdown property pane control React component</span></span>

1. <span data-ttu-id="b4a4b-154">Erstellen Sie einen Ordner „components“.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-154">Create components folder</span></span> <span data-ttu-id="b4a4b-155">Erstellen Sie dazu im Ordner **src** eine Hierarchie aus drei neuen Ordnern, sodass Ihre Ordnerstruktur als **src/controls/PropertyPaneAsyncDropdown/components** angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-155">In the project **src** folder, create a hierarchy of three new folders so that your folder structure appears as **src/controls/PropertyPaneAsyncDropdown/components**.</span></span>

  ![Komponentenordner in Visual Studio Code hervorgehoben](../../../images/custom-property-pane-control-components-folder.png)

2. <span data-ttu-id="b4a4b-157">Definieren Sie die Eigenschaften der asynchronen React-basierten Dropdownkomponente.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-157">Define asynchronous dropdown React component properties</span></span> <span data-ttu-id="b4a4b-158">Erstellen Sie dazu im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **IAsyncDropdownProps.ts**, und geben Sie folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-158">In the **src/controls/PropertyPaneAsyncDropdown/components** folder create a new file named **IAsyncDropdownProps.ts** and enter the following code:</span></span>

  ```ts
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IAsyncDropdownProps {
    label: string;
    loadOptions: () => Promise<IDropdownOption[]>;
    onChanged: (option: IDropdownOption, index?: number) => void;
    selectedKey: string | number;
    disabled: boolean;
    stateKey: string;
  }
  ```

  <span data-ttu-id="b4a4b-159">Die Klasse **IAsyncDropdownProps** definiert Eigenschaften, die für die React-Komponente festgelegt werden können, die vom benutzerdefinierten Steuerelement im Eigenschaftenbereich verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-159">The **IAsyncDropdownProps** class defines properties that can be set on the React component used by the custom property pane control:</span></span> 
  - <span data-ttu-id="b4a4b-160">Die Eigenschaft **label** legt die Beschriftung des Dropdown-Steuerelements fest.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-160">The **label** property specifies the label for the dropdown control.</span></span> 
  - <span data-ttu-id="b4a4b-161">Die mit dem Delegat **loadOptions** verknüpfte Funktion wird vom Steuerelement aufgerufen, um die verfügbaren Optionen zu laden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-161">The function associated with the **loadOptions** delegate is called by the control to load the available options.</span></span> 
  - <span data-ttu-id="b4a4b-162">Die mit dem Delegat **onChanged** verknüpfte Funktion wird aufgerufen, sobald der Benutzer eine Option aus dem Dropdown auswählt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-162">The function associated with the **onChanged** delegate is called after the user selects an option in the dropdown.</span></span> 
  - <span data-ttu-id="b4a4b-163">Die Eigenschaft **selectedKey** gibt den ausgewählten Wert an. Dabei kann es sich um eine Zeichenfolge oder eine Zahl handeln.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-163">The **selectedKey** property specifies the selected value, which can be a string or a number.</span></span> 
  - <span data-ttu-id="b4a4b-164">Die Eigenschaft **disabled** gibt an, ob das Dropdown-Steuerelement deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-164">The **disabled** property specifies if the dropdown control is disabled or not.</span></span> 
  - <span data-ttu-id="b4a4b-165">Die Eigenschaft **stateKey** wird verwendet, um ein Neurendern der React-Komponente zu erzwingen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-165">The **stateKey** property is used to force the React component to re-render.</span></span>

3. <span data-ttu-id="b4a4b-166">Definieren Sie die Schnittstelle der asynchronen React-basierten Dropdownkomponente.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-166">Define asynchronous dropdown React component interface</span></span> <span data-ttu-id="b4a4b-167">Erstellen Sie hierzu im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **IAsyncDropdownState.ts**, und geben Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-167">In the **src/controls/PropertyPaneAsyncDropdown/components** folder create new file named **IAsyncDropdownState.ts** and enter the following code:</span></span>

  ```ts
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IAsyncDropdownState {
    loading: boolean;
    options: IDropdownOption[];
    error: string;
  }
  ```

  <span data-ttu-id="b4a4b-168">Die Schnittstelle **IAsyncDropdownState** beschreibt den Status der React-Komponente.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-168">The **IAsyncDropdownState** interface describes the state of the React component:</span></span>
  - <span data-ttu-id="b4a4b-169">Die Eigenschaft **loading** gibt an, ob die Komponente ihre Optionen gerade lädt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-169">The **loading** property determines if the component is loading its options at the given moment.</span></span> 
  - <span data-ttu-id="b4a4b-170">Die Eigenschaft **options** enthält alle verfügbaren Optionen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-170">The **options** property contains all available options.</span></span> 
  - <span data-ttu-id="b4a4b-171">Tritt ein Fehler auf, wird er der Eigenschaft **error** zugewiesen und von dort an den Benutzer kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-171">If an error occurred, it is assigned to the **error** property from where it is communicated to the user.</span></span>

4. <span data-ttu-id="b4a4b-172">Definieren Sie die asynchrone React-basierte Dropdownkomponente.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-172">Define the asynchronous dropdown React component</span></span> <span data-ttu-id="b4a4b-173">Erstellen Sie hierzu im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **AsyncDropdown.tsx**, und geben Sie folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-173">In the **src/controls/PropertyPaneAsyncDropdown/components** folder create a new file named **AsyncDropdown.tsx** and enter the following code:</span></span>

  ```tsx
  import * as React from 'react';
  import { Dropdown, IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { Spinner } from 'office-ui-fabric-react/lib/components/Spinner';
  import { IAsyncDropdownProps } from './IAsyncDropdownProps';
  import { IAsyncDropdownState } from './IAsyncDropdownState';

  export default class AsyncDropdown extends React.Component<IAsyncDropdownProps, IAsyncDropdownState> {
    private selectedKey: React.ReactText;

    constructor(props: IAsyncDropdownProps, state: IAsyncDropdownState) {
      super(props);
      this.selectedKey = props.selectedKey;

      this.state = {
        loading: false,
        options: undefined,
        error: undefined
      };
    }

    public componentDidMount(): void {
      this.loadOptions();
    }

    public componentDidUpdate(prevProps: IAsyncDropdownProps, prevState: IAsyncDropdownState): void {
      if (this.props.disabled !== prevProps.disabled ||
        this.props.stateKey !== prevProps.stateKey) {
        this.loadOptions();
      }
    }

    private loadOptions(): void {
      this.setState({
        loading: true,
        error: undefined,
        options: undefined
      });

      this.props.loadOptions()
        .then((options: IDropdownOption[]): void => {
          this.setState({
            loading: false,
            error: undefined,
            options: options
          });
        }, (error: any): void => {
          this.setState((prevState: IAsyncDropdownState, props: IAsyncDropdownProps): IAsyncDropdownState => {
            prevState.loading = false;
            prevState.error = error;
            return prevState;
          });
        });
    }

    public render(): JSX.Element {
      const loading: JSX.Element = this.state.loading ? <div><Spinner label={'Loading options...'} /></div> : <div />;
      const error: JSX.Element = this.state.error !== undefined ? <div className={'ms-TextField-errorMessage ms-u-slideDownIn20'}>Error while loading items: {this.state.error}</div> : <div />;

      return (
        <div>
          <Dropdown label={this.props.label}
            disabled={this.props.disabled || this.state.loading || this.state.error !== undefined}
            onChanged={this.onChanged.bind(this)}
            selectedKey={this.selectedKey}
            options={this.state.options} />
          {loading}
          {error}
        </div>
      );
    }

    private onChanged(option: IDropdownOption, index?: number): void {
      this.selectedKey = option.key;
      // reset previously selected options
      const options: IDropdownOption[] = this.state.options;
      options.forEach((o: IDropdownOption): void => {
        if (o.key !== option.key) {
          o.selected = false;
        }
      });
      this.setState((prevState: IAsyncDropdownState, props: IAsyncDropdownProps): IAsyncDropdownState => {
        prevState.options = options;
        return prevState;
      });
      if (this.props.onChanged) {
        this.props.onChanged(option, index);
      }
    }
  }
  ```

  <span data-ttu-id="b4a4b-174">Die Klasse **AsyncDropdown** stellt die React-Komponente dar, die verwendet wird, um das asynchrone Dropdown-Steuerelement im Eigenschaftenbereich zu rendern.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-174">The **AsyncDropdown** class represents the React component used to render the asynchronous dropdown property pane control:</span></span>

  - <span data-ttu-id="b4a4b-175">Wenn die Komponente zum ersten Mal geladen wird, ändert sich die Methode **componentDidMount**, oder es ändern sich ihre Eigenschaften **disabled** oder **stateKey**. Anschließend werden durch Aufrufen der über die Eigenschaften übergebenen Methode **loadOptions** die verfügbaren Optionen geladen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-175">When the component first loads, the **componentDidMount** method, or its **disabled** or **stateKey** properties, change, and it loads the available options by calling the **loadOptions** method passed through the properties.</span></span> 
  - <span data-ttu-id="b4a4b-176">Sobald die Optionen geladen wurden, wird der Status der Komponente aktualisiert, und die verfügbaren Optionen werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-176">After the options are loaded, the component updates its state showing the available options.</span></span> 
  - <span data-ttu-id="b4a4b-177">Das Dropdown selbst wird mithilfe der [Office UI Fabric React-Dropdownkomponente](https://developer.microsoft.com/de-DE/fabric#/components/dropdown) gerendert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-177">The dropdown itself is rendered by using the [Office UI Fabric React dropdown component](https://developer.microsoft.com/de-DE/fabric#/components/dropdown).</span></span> 
  - <span data-ttu-id="b4a4b-178">Während die Komponente die verfügbaren Optionen lädt, wird mithilfe der [Office UI Fabric React-Drehfeldkomponente](https://developer.microsoft.com/de-DE/fabric#/components/spinner) ein Drehfeld angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-178">When the component is loading the available options, it displays a spinner by using the [Office UI Fabric React spinner component](https://developer.microsoft.com/de-DE/fabric#/components/spinner).</span></span>


<span data-ttu-id="b4a4b-179">Der nächste Schritt besteht darin, das benutzerdefinierte Steuerelement für den Eigenschaftenbereich zu definieren.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-179">The next step is to define the custom property pane control.</span></span> <span data-ttu-id="b4a4b-180">Dieses Steuerelement wird im Webpart zum Definieren von Eigenschaften im Eigenschaftenbereich verwendet und mithilfe der zuvor definierten React-Komponente gerendert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-180">The next step is to define the custom property pane control. This control is used inside the web part when defining properties in the property pane and renders using the previously defined React component.</span></span>

### <a name="add-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="b4a4b-181">Hinzufügen eines asynchronen Dropdown-Steuerelements zum Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="b4a4b-181">Add asynchronous dropdown property pane control</span></span>

1. <span data-ttu-id="b4a4b-182">Definieren Sie die Eigenschaften des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-182">Define asynchronous dropdown property pane control properties</span></span> <span data-ttu-id="b4a4b-183">Ein benutzerdefiniertes Eigenschaftenbereich-Steuerelement weist zwei Eigenschaftensätze auf.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-183">A custom property pane control has two sets of properties.</span></span> 
  
  <span data-ttu-id="b4a4b-184">Der erste Satz von Eigenschaften wird öffentlich verfügbar gemacht und wird zum Definieren der Webparteigenschaft innerhalb des Webparts verwendet.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-184">The first set of properties are exposed publicly and are used to define the web part property inside the web part.</span></span> <span data-ttu-id="b4a4b-185">Diese Eigenschaften sind komponentenspezifische Eigenschaften wie beispielsweise die Bezeichnung, die neben dem Steuerelement angezeigt wird, Mindest- und Maximalwerte für ein Drehfeld oder verfügbare Optionen für ein Dropdown.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-185">These properties are component-specific properties, such as the label displayed next to the control, minimum and maximum values for a spinner, or available options for a dropdown.</span></span> <span data-ttu-id="b4a4b-186">Bei der Definition eines benutzerdefinierten Eigenschaftenbereich-Steuerelements muss der Typ, der diese Eigenschaften beschreibt, als Typ **TProperties** übergeben werden, wenn die Schnittstelle `IPropertyPaneField<TProperties>` implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-186">When defining a custom property pane control, the type describing these properties must be passed as the **TProperties** type when implementing the `IPropertyPaneField<TProperties>` interface.</span></span>

  <span data-ttu-id="b4a4b-p115">Bei dem zweiten Satz von Eigenschaften handelt es sich um private Eigenschaften, die intern innerhalb des benutzerdefinierten Eigenschaftenbereichssteuerelements verwendet werden. Diese Eigenschaften müssen den SharePoint Framework-APIs entsprechen, damit das benutzerdefinierte Steuerelement korrekt gerendert wird. Diese Eigenschaften müssen die **IPropertyPaneCustomFieldProps**-Schnittstelle aus dem **@microsoft/sp-webpart-base**-Paket implementieren.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p115">The second set of properties are private properties used internally inside the custom property pane control. These properties have to adhere to the SharePoint Framework APIs for the custom control to render correctly. These properties must implement the **IPropertyPaneCustomFieldProps** interface from the **@microsoft/sp-webpart-base** package.</span></span>

2. <span data-ttu-id="b4a4b-190">Definieren Sie die öffentlichen Eigenschaften des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-190">Define the public properties for the asynchronous dropdown property pane control</span></span> <span data-ttu-id="b4a4b-191">Erstellen Sie hierzu im Ordner **src/controls/PropertyPaneAsyncDropdown** eine neue Datei mit dem Namen **IPropertyPaneAsyncDropdownProps.ts**, und geben Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-191">In the **src/controls/PropertyPaneAsyncDropdown** folder create a new file named **IPropertyPaneAsyncDropdownProps.ts** and enter the following code:</span></span>

  ```ts
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IPropertyPaneAsyncDropdownProps {
    label: string;
    loadOptions: () => Promise<IDropdownOption[]>;
    onPropertyChange: (propertyPath: string, newValue: any) => void;
    selectedKey: string | number;
    disabled?: boolean;
  }
  ```

  <span data-ttu-id="b4a4b-192">Zur Schnittstelle **IPropertyPaneAsyncDropdownProps** ist Folgendes anzumerken:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-192">In the **IPropertyPaneAsyncDropdownProps** interface:</span></span>
  - <span data-ttu-id="b4a4b-193">Die Eigenschaft **label** definiert die Bezeichnung, die neben dem Dropdown angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-193">The **label** property defines the label displayed next to the dropdown.</span></span> 
  - <span data-ttu-id="b4a4b-194">Der Delegat **loadOptions** definiert die Methode, die zum Laden der verfügbaren Dropdownoptionen aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-194">The **loadOptions** delegate defines the method that is called to load the available dropdown options.</span></span> 
  - <span data-ttu-id="b4a4b-195">Der Delegat **onPropertyChange** definiert eine Methode, die aufgerufen wird, wenn der Benutzer einen Wert aus dem Dropdown auswählt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-195">The **onPropertyChange** delegate defines a method that is called when the user selects a value in the dropdown.</span></span> 
  - <span data-ttu-id="b4a4b-196">Die Eigenschaft **selectedKey** gibt den aus dem Dropdown ausgewählten Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-196">The **selectedKey** property returns the selected dropdown value.</span></span> 
  - <span data-ttu-id="b4a4b-197">Die Eigenschaft **disabled** gibt an, ob das Steuerelement deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-197">The **disabled** property specifies whether the control is disabled or not.</span></span>

3. <span data-ttu-id="b4a4b-198">Definieren Sie die internen Eigenschaften des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-198">Define the internal properties for the asynchronous dropdown property pane control</span></span> <span data-ttu-id="b4a4b-199">Erstellen Sie hierzu im Ordner **src/controls/PropertyPaneAsyncDropdown** eine neue Datei mit dem Namen **IPropertyPaneAsyncDropdownInternalProps.ts**, und geben Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-199">In the **src/controls/PropertyPaneAsyncDropdown** folder create a new file named **IPropertyPaneAsyncDropdownInternalProps.ts** and enter the following code:</span></span>

  ```ts
  import { IPropertyPaneCustomFieldProps } from '@microsoft/sp-webpart-base';
  import { IPropertyPaneAsyncDropdownProps } from './IPropertyPaneAsyncDropdownProps';

  export interface IPropertyPaneAsyncDropdownInternalProps extends IPropertyPaneAsyncDropdownProps, IPropertyPaneCustomFieldProps {
  }
  ```

  <span data-ttu-id="b4a4b-200">Die Schnittstelle **IPropertyPaneAsyncDropdownInternalProps** definiert zwar keine neuen Eigenschaften, kombiniert aber die Eigenschaften aus der zuvor definierten Schnittstelle **IPropertyPaneAsyncDropdownProps** und der SharePoint-Framework-Standardschnittstelle **IPropertyPaneCustomFieldProps**. Diese ist erforderlich, damit ein benutzerdefiniertes Steuerelement korrekt ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-200">While the **IPropertyPaneAsyncDropdownInternalProps** interface doesn't define any new properties, it combines the properties from the previously defined **IPropertyPaneAsyncDropdownProps** interface and the standard SharePoint Framework **IPropertyPaneCustomFieldProps** interface which is required for a custom control to run correctly.</span></span>

4. <span data-ttu-id="b4a4b-201">Definieren Sie das asynchrone Dropdown-Steuerelement für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-201">Define the asynchronous dropdown property pane control</span></span> <span data-ttu-id="b4a4b-202">Erstellen Sie hierzu im Ordner **src/controls/PropertyPaneAsyncDropdown** eine neue Datei mit dem Namen **PropertyPaneAsyncDropdown.ts**, und geben Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-202">In the **src/controls/PropertyPaneAsyncDropdown** folder create a new file named **PropertyPaneAsyncDropdown.ts** and enter the following code:</span></span>

  ```ts
  import * as React from 'react';
  import * as ReactDom from 'react-dom';
  import {
    IPropertyPaneField,
    PropertyPaneFieldType
  } from '@microsoft/sp-webpart-base';
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { IPropertyPaneAsyncDropdownProps } from './IPropertyPaneAsyncDropdownProps';
  import { IPropertyPaneAsyncDropdownInternalProps } from './IPropertyPaneAsyncDropdownInternalProps';
  import AsyncDropdown from './components/AsyncDropdown';
  import { IAsyncDropdownProps } from './components/IAsyncDropdownProps';

  export class PropertyPaneAsyncDropdown implements IPropertyPaneField<IPropertyPaneAsyncDropdownProps> {
    public type: PropertyPaneFieldType = PropertyPaneFieldType.Custom;
    public targetProperty: string;
    public properties: IPropertyPaneAsyncDropdownInternalProps;
    private elem: HTMLElement;

    constructor(targetProperty: string, properties: IPropertyPaneAsyncDropdownProps) {
      this.targetProperty = targetProperty;
      this.properties = {
        key: properties.label,
        label: properties.label,
        loadOptions: properties.loadOptions,
        onPropertyChange: properties.onPropertyChange,
        selectedKey: properties.selectedKey,
        disabled: properties.disabled,
        onRender: this.onRender.bind(this)
      };
    }

    public render(): void {
      if (!this.elem) {
        return;
      }

      this.onRender(this.elem);
    }

    private onRender(elem: HTMLElement): void {
      if (!this.elem) {
        this.elem = elem;
      }

      const element: React.ReactElement<IAsyncDropdownProps> = React.createElement(AsyncDropdown, {
        label: this.properties.label,
        loadOptions: this.properties.loadOptions,
        onChanged: this.onChanged.bind(this),
        selectedKey: this.properties.selectedKey,
        disabled: this.properties.disabled,
        // required to allow the component to be re-rendered by calling this.render() externally
        stateKey: new Date().toString()
      });
      ReactDom.render(element, elem);
    }

    private onChanged(option: IDropdownOption, index?: number): void {
      this.properties.onPropertyChange(this.targetProperty, option.key);
    }
  }
  ```

  <span data-ttu-id="b4a4b-203">Die Klasse **PropertyPaneAsyncDropdown** implementiert die SharePoint-Framework-Standardschnittstelle **IPropertyPaneField**, unter Verwendung der Schnittstelle **IPropertyPaneAsyncDropdownProps** als Vertrag für die öffentlichen Eigenschaften, die innerhalb des Webparts festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-203">The **PropertyPaneAsyncDropdown** class implements the standard SharePoint Framework **IPropertyPaneField** interface using the **IPropertyPaneAsyncDropdownProps** interface as a contract for its public properties that can be set from inside the web part. The class contains the following three public properties defined by the IPropertyPaneField interface:</span></span> <span data-ttu-id="b4a4b-204">Die Klasse enthält die folgenden drei öffentlichen Eigenschaften, die von der Schnittstelle **IPropertyPaneField** definiert werden:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-204">The class contains the following three public properties defined by the **IPropertyPaneField** interface:</span></span>

  - <span data-ttu-id="b4a4b-205">**type**: Muss bei benutzerdefinierten Eigenschaftenbereich-Steuerelementen auf **PropertyPaneFieldType.Custom** festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-205">**type**: Must be set to **PropertyPaneFieldType.Custom** for a custom property pane control.</span></span>
  - <span data-ttu-id="b4a4b-206">**targetProperty**: Wird zum Angeben des Namens der Webparteigenschaft verwendet, die mit dem Steuerelement verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-206">**targetProperty**: Used to specify the name of the web part property to be used with the control.</span></span>
  - <span data-ttu-id="b4a4b-207">**properties**: Wird zum Definieren von steuerelementspezifischen Eigenschaften verwendet.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-207">**properties**: Used to define control-specific properties.</span></span>

  <span data-ttu-id="b4a4b-208">Wie Sie sehen, ist die Eigenschaft **properties** vom internen Typ **IPropertyPaneAsyncDropdownInternalProps** und gehört nicht zur öffentlichen Schnittstelle **IPropertyPaneAsyncDropdownProps**, die von der Klasse implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-208">Notice how the **properties** property is of the internal **IPropertyPaneAsyncDropdownInternalProps** type rather than the public **IPropertyPaneAsyncDropdownProps** interface implemented by the class.</span></span> <span data-ttu-id="b4a4b-209">Dies ist gewollt, damit die Eigenschaft **properties** die Methode **onRender** definieren kann, die vom SharePoint-Framework gefordert wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-209">This is on purpose so that the **properties** property can define the **onRender** method required by the SharePoint Framework.</span></span> <span data-ttu-id="b4a4b-210">Wäre die Methode **onRender** Teil der öffentlichen Schnittstelle **IPropertyPaneAsyncDropdownProps**, müssten Sie ihr bei Verwendung des asynchronen Dropdown-Steuerelements im Webpart einen Wert zuweisen. Das ist nicht erstrebenswert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-210">Notice how the properties property is of the internal IPropertyPaneAsyncDropdownInternalProps type rather than the public IPropertyPaneAsyncDropdownProps interface implemented by the class. This is on purpose so that the properties property can define the onRender method required by the SharePoint Framework. If the onRender method was a part of the public IPropertyPaneAsyncDropdownProps interface then, when using the asynchronous dropdown control in the web part, you would be required to assign a value to it inside the web part, which isn't desirable.</span></span>

  <span data-ttu-id="b4a4b-211">Die Klasse **PropertyPaneAsyncDropdown** definiert eine öffentliche Methode **render**, die zum Aktualisieren des Steuerelements verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-211">The **PropertyPaneAsyncDropdown** class defines a public **render** method, which can be used to repaint the control.</span></span> <span data-ttu-id="b4a4b-212">Das ist beispielsweise bei kaskadierenden Dropdowns nützlich, bei denen ein in Dropdown 1 festgelegter Wert festlegt, welche Optionen in Dropdown 2 verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-212">This is useful in situations such as when you have cascading dropdowns where the value set in one determines the options available in another.</span></span> <span data-ttu-id="b4a4b-213">Durch Aufrufen der Methode **render** nach dem Auswählen eines Elements können die verfügbaren Optionen vom abhängigen Dropdown geladen werden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-213">By calling the **render** method after selecting an item, you can have the dependent dropdown load available options.</span></span> <span data-ttu-id="b4a4b-214">Hierfür muss React erkennen können, dass sich das Steuerelement geändert hat.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-214">For this to work, you have to make React detect that the control has changed.</span></span> <span data-ttu-id="b4a4b-215">Das ermöglichen Sie durch Festlegen des Werts von **stateKey** auf das jeweils aktuelle Datum.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-215">This is done by setting the value of the **stateKey** to the current date.</span></span> <span data-ttu-id="b4a4b-216">Mithilfe dieses Tricks wird bei jedem Aufruf der Methode **onRender** die Komponente nicht nur erneut gerendert, sondern es werden auch ihre verfügbaren Optionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-216">Using this trick, every time the **onRender** method is called, the component not only is re-rendered but also updates its available options.</span></span>

## <a name="use-the-asynchronous-dropdown-property-pane-control-in-the-web-part"></a><span data-ttu-id="b4a4b-217">Verwenden des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich im Webpart</span><span class="sxs-lookup"><span data-stu-id="b4a4b-217">Use the asynchronous dropdown property pane control in the web part</span></span>

<span data-ttu-id="b4a4b-218">Sobald das asynchrone Dropdown-Steuerelement für den Eigenschaftenbereich bereit ist, besteht der nächste Schritt darin, es innerhalb des Webparts zu verwenden, damit Benutzer eine Liste auswählen können.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-218">With the asynchronous dropdown property pane control ready, the next step is to use it inside the web part allowing users to select a list.</span></span>

### <a name="add-list-info-interface"></a><span data-ttu-id="b4a4b-219">Hinzufügen einer Schnittstelle des Typs „ListInfo“</span><span class="sxs-lookup"><span data-stu-id="b4a4b-219">Add list info interface</span></span>

<span data-ttu-id="b4a4b-220">Um Informationen zu verfügbaren Listen auf konsistente Art und Weise zu übergeben, definieren Sie eine Schnittstelle, die Informationen zu einer Liste darstellt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-220">To pass information about available lists around in a consistent manner, define an interface that will represent information about a list. In the src/webparts/listItems folder create a new file named IListInfo.ts and enter the following code:</span></span> <span data-ttu-id="b4a4b-221">Erstellen Sie hierzu im Ordner **src/webparts/listItems** eine neue Datei mit dem Namen **IListInfo.ts** , und geben Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-221">In the **./src/webparts/greetings/loc** folder create new file named **nl-nl.js** and enter the following code:</span></span>

```ts
export interface IListInfo {
  Id: string;
  Title: string;
}
```

### <a name="use-the-asynchronous-dropdown-property-pane-control-to-render-the-listname-web-part-property"></a><span data-ttu-id="b4a4b-222">Verwenden des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich zum Rendern der Webparteigenschaft „listName“</span><span class="sxs-lookup"><span data-stu-id="b4a4b-222">Use the asynchronous dropdown property pane control to render the listName web part property</span></span>

1. <span data-ttu-id="b4a4b-223">Referenzieren Sie die erforderlichen Typen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-223">Reference required types</span></span> <span data-ttu-id="b4a4b-224">Importieren Sie hierzu im oberen Teil der Datei **src/webparts/listItems/ListItemsWebPart.ts** die zuvor erstellte Klasse **PropertyPaneAsyncDropdown**, indem Sie folgenden Code hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-224">In the top section of the **src/webparts/listItems/ListItemsWebPart.ts** file import the previously created **PropertyPaneAsyncDropdown** class by adding:</span></span>

  ```ts
  import { PropertyPaneAsyncDropdown } from '../../controls/PropertyPaneAsyncDropdown/PropertyPaneAsyncDropdown';
  ```

2. <span data-ttu-id="b4a4b-225">Fügen Sie unter diesem Code einen Verweis auf die Schnittstelle **IDropdownOption** und zwei Hilfsfunktionen hinzu, die für die Arbeit mit Webparteigenschaften erforderlich sind:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-225">Then after that code, add a reference to the **IDropdownOption** interface and two helpers functions required to work with web part properties.</span></span>

  ```ts
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { update, get } from '@microsoft/sp-lodash-subset';
  ```

  <br/>

  ![Hervorgehobene Verweise auf die Klasse „PropertyPaneAsyncDropdown“ und die Schnittstelle „IDropdownOption“ in Visual Studio Code](../../../images/custom-property-pane-control-web-part-imports.png)

3. <span data-ttu-id="b4a4b-227">Fügen Sie eine Methode zum Laden der verfügbaren Listen hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-227">Add method to load available lists</span></span> <span data-ttu-id="b4a4b-228">Dazu fügen Sie in der Klasse **ListItemsWebPart** eine Methode zum Laden der verfügbaren Listen hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-228">In the **ListItemsWebPart** class, add a method to load available lists.</span></span> <span data-ttu-id="b4a4b-229">In diesem Artikel verwenden Sie simulierte Daten; Sie können aber auch die SharePoint-REST-API aufrufen, um die Liste der verfügbaren Listen aus dem aktuellen Web abzurufen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-229">In the ListItemsWebPart class, add a method to load available lists. In this article you will use mock data, but you could also call the SharePoint REST API to retrieve the list of available lists from the current web. To simulate loading options from an external service the method uses a two-second delay.</span></span> <span data-ttu-id="b4a4b-230">Um das Laden aus einem externen Dienst zu simulieren, implementiert die Methode eine Verzögerung von 2 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-230">To simulate loading options from an external service, the method uses a two second delay.</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private loadLists(): Promise<IDropdownOption[]> {
      return new Promise<IDropdownOption[]>((resolve: (options: IDropdownOption[]) => void, reject: (error: any) => void) => {
        setTimeout(() => {
          resolve([{
            key: 'sharedDocuments',
            text: 'Shared Documents'
          },
            {
              key: 'myDocuments',
              text: 'My Documents'
            }]);
        }, 2000);
      });
    }
  }
  ```

4. <span data-ttu-id="b4a4b-231">Fügen Sie eine Methode hinzu, die Wertänderungen im Dropdown verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-231">Add method to handle the change of the value in the dropdown</span></span> <span data-ttu-id="b4a4b-232">Fügen Sie hierzu in der Klasse **ListItemsWebPart** eine neue Methode mit dem Namen**onListChange** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-232">In the **ListItemsWebPart** class add a new method named **onListChange**.</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private onListChange(propertyPath: string, newValue: any): void {
      const oldValue: any = get(this.properties, propertyPath);
      // store new value in web part properties
      update(this.properties, propertyPath, (): any => { return newValue; });
      // refresh web part
      this.render();
    }
  }
  ```

  <span data-ttu-id="b4a4b-233">Nach dem Auswählen einer Liste aus dem Listendropdown sollte der ausgewählte Wert in Webparteigenschaften beibehalten werden, und das Webpart sollte erneut gerendert werden, damit die ausgewählte Eigenschaft übernommen wird.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-233">After selecting a list in the list dropdown, the selected value should be persisted in web part properties and the web part should be re-rendered to reflect the selected property.</span></span>

5. <span data-ttu-id="b4a4b-234">Rendern Sie die Webparteigenschaft „listName“ mithilfe des asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-234">Render the list web part property using the asynchronous dropdown property pane control</span></span> <span data-ttu-id="b4a4b-235">Ändern Sie hierzu in der Klasse **ListItemsWebPart** die Methode **getPropertyPaneConfiguration** so ab, dass sie das asynchrone Dropdown-Steuerelement für den Eigenschaftenbereich zum Rendern der Webparteigenschaft **listName** verwendet.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-235">In the **ListItemsWebPart** class change the **getPropertyPaneConfiguration** method to use the asynchronous dropdown property pane control to render the **listName** web part property.</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: [
                  new PropertyPaneAsyncDropdown('listName', {
                    label: strings.ListFieldLabel,
                    loadOptions: this.loadLists.bind(this),
                    onPropertyChange: this.onListChange.bind(this),
                    selectedKey: this.properties.listName
                  })
                ]
              }
            ]
          }
        ]
      };
    }
    // ...
  }
  ```

6. <span data-ttu-id="b4a4b-236">An diesem Punkt sollten Sie in der Lage sein, mithilfe des neu erstellten asynchronen Dropdown-Steuerelements für den Eigenschaftenbereich eine Liste auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-236">At this point you should be able to select a list using the newly created asynchronous dropdown property pane control. To verify that the control is working as expected, open the command-line and run:</span></span> <span data-ttu-id="b4a4b-237">Öffnen Sie die Befehlszeile, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Steuerelement korrekt funktioniert:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-237">To verify that everything is working as expected in the command-line run:</span></span>

  ```sh
  gulp serve
  ```

  <br/>

  ![Asynchrones Steuerelement für den Dropdown-Eigenschaftenbereich beim Laden der Optionen, ohne die Webpart-Benutzeroberfläche zu blockieren](../../../images/custom-property-pane-control-loading-options.png)

  <br/>

  ![Auswählen einer der Optionen im asynchronen Steuerelement für den Dropdown-Eigenschaftenbereich](../../../images/custom-property-pane-control-selecting-option.png)

## <a name="implement-cascading-dropdowns-using-the-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="b4a4b-240">Implementieren kaskadierender Dropdowns mithilfe des asynchronen Dropdown-Steuerelements für Eigenschaftenbereiche</span><span class="sxs-lookup"><span data-stu-id="b4a4b-240">Implement cascading dropdowns using the asynchronous dropdown property pane control</span></span>

<span data-ttu-id="b4a4b-241">Beim Erstellen von SharePoint-Framework-Webparts müssen Sie möglicherweise eine Konfiguration implementieren, bei der es von einer anderen zuvor ausgewählten Option abhängt, welche Optionen verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-241">When building SharePoint Framework web parts, you might need to implement a configuration where the available options depend on another option chosen previously.</span></span> <span data-ttu-id="b4a4b-242">Ein typisches Beispiel besteht darin, Benutzer zuerst eine Liste und dann ein Listenelement aus dieser Liste auswählen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-242">A common example is to first let users choose a list and from that list select a list item.</span></span> <span data-ttu-id="b4a4b-243">Die Liste der verfügbaren Element wäre von der ausgewählten Liste abhängig.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-243">The list of available items would depend on the selected list.</span></span> <span data-ttu-id="b4a4b-244">Nachfolgend erfahren Sie, wie ein solches Szenario mithilfe des in den vorangegangenen Abschnitten implementieren asynchronen Dropdown-Steuerelements für den Eigenschaftbereich umgesetzt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-244">Here is how to implement such a scenario by using the asynchronous dropdown property pane control implemented in previous steps.</span></span>

### <a name="add-item-web-part-property"></a><span data-ttu-id="b4a4b-245">Hinzufügen der Webparteigenschaft „item“</span><span class="sxs-lookup"><span data-stu-id="b4a4b-245">Add item web part property</span></span>

1. <span data-ttu-id="b4a4b-246">Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-246">In the code editor, open the **src/webparts/listItems/ListItemsWebPart.manifest.json** file.</span></span> <span data-ttu-id="b4a4b-247">Fügen Sie im Abschnitt **properties** eine neue Eigenschaft mit dem Namen **item** hinzu. Der Code sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-247">In the code editor open the src/webparts/listItems/ListItemsWebPart.manifest.json file. To the **properties** section add a new property named **item** so that it appears as follows:</span></span>

  ```ts
  // ...
  "properties": {
    "listName": "",
    "item": ""
  }
  // ...
  ```

  <br/>

  ![Webpartmanifest mit hervorgehobener Webparteigenschaft „item“](../../../images/custom-property-pane-control-item-property-web-part-manifest.png)

2. <span data-ttu-id="b4a4b-249">Ändern Sie den Code in der Datei **src/webparts/listItems/IListItemsWebPartProps.ts** in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-249">Change the code in the **src/webparts/listItems/IListItemsWebPartProps.ts** file to:</span></span>

  ```ts
  export interface IListItemsWebPartProps {
    listName: string;
    item: string;
  }
  ```

3. <span data-ttu-id="b4a4b-250">Ändern Sie den Inhalt der Datei **src/webparts/listItems/components/IListItemsProps.ts** in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-250">Change the contents of the **src/webparts/listItems/components/IListItemsProps.ts** file to:</span></span>

  ```ts
  export interface IListItemsProps {
    listName: string;
    item: string;
  }
  ```

4. <span data-ttu-id="b4a4b-251">Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** den Code der Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-251">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the code of the **render** method to:</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
        listName: this.properties.listName,
        item: this.properties.item
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

5. <span data-ttu-id="b4a4b-252">Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die Schnittstelle **IListItemsWebPartStrings** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-252">In the **src/webparts/listItems/loc/mystrings.d.ts** file change the **IListItemsWebPartStrings** interface to</span></span>

  ```ts
  declare interface IListItemsWebPartStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListFieldLabel: string;
    ItemFieldLabel: string;
  }
  ```

6. <span data-ttu-id="b4a4b-253">Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ItemFieldLabel** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-253">In the **src/webparts/listItems/loc/en-us.js** file add the missing definition for the **ItemFieldLabel** string.</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListFieldLabel": "List",
      "ItemFieldLabel": "Item"
    }
  });
  ```

### <a name="render-the-value-of-the-item-web-part-property"></a><span data-ttu-id="b4a4b-254">Rendern des Werts der Webparteigenschaft „item“</span><span class="sxs-lookup"><span data-stu-id="b4a4b-254">Render the value of the item web part property</span></span>

<span data-ttu-id="b4a4b-255">Ändern Sie in der Datei **src/webparts/listItems/components/ListItems.tsx** die Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-255">In the **src/webparts/listItems/components/ListItems.tsx** file, change the **render** method to:</span></span>

```tsx
export default class ListItems extends React.Component<IListItemsProps, {}> {
  public render(): React.ReactElement<IListItemsProps> {
    return (
      <div className={styles.listItems}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-lg10 ms-xl8 ms-xlPush2 ms-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.item)}</p>
              <a href="https://aka.ms/spfx" className={styles.button}>
                <span className={styles.label}>Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

### <a name="add-method-to-load-list-items"></a><span data-ttu-id="b4a4b-256">Hinzufügen einer Methode zum Laden von Listenelementen</span><span class="sxs-lookup"><span data-stu-id="b4a4b-256">Add method to load list items</span></span>

<span data-ttu-id="b4a4b-257">Fügen Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** in der Klasse **ListItemsWebPart** eine neue Methode zum Laden der verfügbaren Listenelemente aus der ausgewählten Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-257">In the **src/webparts/listItems/ListItemsWebPart.ts** file, in the **ListItemsWebPart** class add a new method to load available list items from the selected list. Like the method for loading available lists, you will use mock data.</span></span> <span data-ttu-id="b4a4b-258">Wie auch bei der Methode zum Laden der verfügbaren Listen verwenden Sie hier simulierte Daten.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-258">Like the method for loading available lists, you use mock data.</span></span> <span data-ttu-id="b4a4b-259">In Abhängigkeit von der zuvor ausgewählten Liste gibt die Methode **loadItems** simulierte Listenelemente zurück.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-259">Depending on the previously selected list, the **loadItems** method returns mock list items. When no list has been selected, the method resolves the promise without any data.</span></span> <span data-ttu-id="b4a4b-260">Wenn keine Liste ausgewählt wurde, löst die Methode die Zusage ohne Daten.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-260">The loadItems method returns mock list items for the previously selected list. When no list has been selected, the method resolves the promise without any data.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private loadItems(): Promise<IDropdownOption[]> {
    if (!this.properties.listName) {
      // resolve to empty options since no list has been selected
      return Promise.resolve();
    }

    const wp: ListItemsWebPart = this;

    return new Promise<IDropdownOption[]>((resolve: (options: IDropdownOption[]) => void, reject: (error: any) => void) => {
      setTimeout(() => {
        const items = {
          sharedDocuments: [
            {
              key: 'spfx_presentation.pptx',
              text: 'SPFx for the masses'
            },
            {
              key: 'hello-world.spapp',
              text: 'hello-world.spapp'
            }
          ],
          myDocuments: [
            {
              key: 'isaiah_cv.docx',
              text: 'Isaiah CV'
            },
            {
              key: 'isaiah_expenses.xlsx',
              text: 'Isaiah Expenses'
            }
          ]
        };
        resolve(items[wp.properties.listName]);
      }, 2000);
    });
  }
}
```



### <a name="add-method-to-handle-the-selection-of-an-item"></a><span data-ttu-id="b4a4b-261">Hinzufügen einer Methode zum Verarbeiten der Auswahl eines Elements</span><span class="sxs-lookup"><span data-stu-id="b4a4b-261">Add method to handle the selection of an item</span></span>

<span data-ttu-id="b4a4b-262">Fügen Sie in der Klasse **ListItemsWebPart** eine neue Methode mit dem Namen**onListItemChange** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-262">In the **ListItemsWebPart** class add a new method named **onListItemChange**.</span></span> <span data-ttu-id="b4a4b-263">Nach Auswahl eines Elements in der Element-Dropdownliste sollte das Webpart den neuen Wert in den Webparteigenschaften speichern und das Webpart erneut rendern, um die Änderungen in der Benutzeroberfläche widerzuspiegeln.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-263">After selecting an item in the items dropdown, the web part should store the new value in web part properties and re-render the web part to reflect the changes in the user interface.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private onListItemChange(propertyPath: string, newValue: any): void {
    const oldValue: any = get(this.properties, propertyPath);
    // store new value in web part properties
    update(this.properties, propertyPath, (): any => { return newValue; });
    // refresh web part
    this.render();
  }
}
```


### <a name="render-the-item-web-part-property-in-the-property-pane"></a><span data-ttu-id="b4a4b-264">Rendern der Webparteigenschaft „item“ im Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="b4a4b-264">Render the item web part property in the property pane</span></span>

1. <span data-ttu-id="b4a4b-265">Fügen Sie in der Klasse **ListItemsWebPart** eine neue Klasseneigenschaft mit dem Namen **itemsDropdown** hinzu:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-265">In the **ListItemsWebPart** class, add a new class property named **itemsDropdown**.</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    private itemsDropDown: PropertyPaneAsyncDropdown;
    // ...
  }
  ```

2. <span data-ttu-id="b4a4b-266">Ändern Sie den Code der Methode **getPropertyPaneConfiguration** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-266">Next change the code of the **getPropertyPaneConfiguration** method to:</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      // reference to item dropdown needed later after selecting a list
      this.itemsDropDown = new PropertyPaneAsyncDropdown('item', {
        label: strings.ItemFieldLabel,
        loadOptions: this.loadItems.bind(this),
        onPropertyChange: this.onListItemChange.bind(this),
        selectedKey: this.properties.item,
        // should be disabled if no list has been selected
        disabled: !this.properties.listName
      });

      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: [
                  new PropertyPaneAsyncDropdown('listName', {
                    label: strings.ListFieldLabel,
                    loadOptions: this.loadLists.bind(this),
                    onPropertyChange: this.onListChange.bind(this),
                    selectedKey: this.properties.listName
                  }),
                  this.itemsDropDown
                ]
              }
            ]
          }
        ]
      };
    }
    // ...
  }
  ```

  <span data-ttu-id="b4a4b-267">Das Dropdown für die Eigenschaft „item“ wird ähnlich wie das Dropdown für die Eigenschaft „listName“ initialisiert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-267">The dropdown for the item property is initialized similarly to the dropdown for the listName property.</span></span> <span data-ttu-id="b4a4b-268">Der einzige Unterschied besteht darin, dass eine Instanz des Steuerelements der Klassenvariablen zugewiesen werden muss, da nach dem Auswählen einer Liste das Elementdropdown aktualisiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-268">The dropdown for the item property is initialized similarly to the dropdown for the listName property. The only difference is that because after selecting a list the items dropdown has to be refreshed, an instance of the control has to be assigned to the class variable.</span></span>

### <a name="load-items-for-the-selected-list"></a><span data-ttu-id="b4a4b-269">Laden von Elementen aus der ausgewählten Liste</span><span class="sxs-lookup"><span data-stu-id="b4a4b-269">Load items for the selected list</span></span>

<span data-ttu-id="b4a4b-270">Zu Beginn, wenn keine Liste ausgewählt ist, ist das Elementdropdown deaktiviert; es wird aktiviert, sobald der Benutzer eine Liste auswählt.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-270">Initially when no list is selected, the items dropdown is disabled and becomes enabled after the user selects a list. After selecting a list the items dropdown also loads list items from that list. To implement this logic extend the previously defined onListChange method to:</span></span> <span data-ttu-id="b4a4b-271">Nachdem eine Liste ausgewählt wurde, lädt das Elementdropdown auch die Listenelemente dieser Liste.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-271">After selecting a list, the items dropdown also loads list items from that list.</span></span> 

1. <span data-ttu-id="b4a4b-272">Um diese Logik zu implementieren, erweitern Sie die zuvor definierte Methode **onListChange** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-272">To implement this logic, extend the previously defined **onListChange** method to:</span></span>

  ```ts
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private onListChange(propertyPath: string, newValue: any): void {
      const oldValue: any = get(this.properties, propertyPath);
      // store new value in web part properties
      update(this.properties, propertyPath, (): any => { return newValue; });
      // reset selected item
      this.properties.item = undefined;
      // store new value in web part properties
      update(this.properties, 'item', (): any => { return this.properties.item; });
      // refresh web part
      this.render();
      // reset selected values in item dropdown
      this.itemsDropDown.properties.selectedKey = this.properties.item;
      // allow to load items
      this.itemsDropDown.properties.disabled = false;
      // load items and re-render items dropdown
      this.itemsDropDown.render();
    }
    // ...
  }
  ```

  <span data-ttu-id="b4a4b-p134">Nach dem Auswählen einer Liste wird das ausgewählte Element zurückgesetzt, in den Webparteigenschaften beibehalten und in der Element-Dropdownliste zurückgesetzt. Die Dropdownliste zum Auswählen eines Elements wird aktiviert, und die Dropdownliste wird aktiviert, um ihre Optionen zu laden.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p134">After selecting a list, the selected item is reset, persisted in web part properties, and reset in the items dropdown. The dropdown for selecting an item becomes enabled, and the dropdown is refreshed in order to load its options.</span></span>

2. <span data-ttu-id="b4a4b-275">Führen Sie über die Befehlszeile folgenden Befehl aus, um zu überprüfen, ob alles wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="b4a4b-275">To verify that everything is working as expected in the command-line run:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="b4a4b-276">Nachdem Sie das Webpart das erste Mal zu der Seite hinzugefügt und seinen Eigenschaftenbereich geöffnet haben, sollten Sie beide Dropdownlisten deaktiviert und beim Laden ihrer Optionen sehen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-276">After adding the web part to the page for the first time and opening its property pane, you should see both dropdowns disabled and loading their options.</span></span>

  ![Dropdownmenüs im Webpart-Eigenschaftbereich beim Laden der Daten](../../../images/custom-property-pane-control-cascading-loading-lists.png)

  <br/>

  <span data-ttu-id="b4a4b-p135">Nachdem die Optionen geladen wurden, wird die Dropdownliste aktiviert. Da noch keine Liste ausgewählt wurde, bleibt die Dropdownliste deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-p135">After the options have been loaded, the list dropdown becomes enabled. Because no list has been selected yet, the item dropdown remains disabled.</span></span>

  ![Aktivierte Dropdownliste im Webpart-Eigenschaftenbereich. Deaktivierte Element-Dropdownliste](../../../images/custom-property-pane-control-cascading-lists-loaded-items-disabled.png)

   <br/>

  <span data-ttu-id="b4a4b-282">Nach dem Auswählen einer Liste in der Dropdownliste werden die in dieser Liste verfügbaren Elemente geladen.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-282">After selecting a list in the list dropdown the item dropdown will load items available in that list.</span></span>

  ![Element-Dropdownliste, in der verfügbare Elemente nach dem Auswählen einer Liste im Listen-Dropdown geladen werden](../../../images/custom-property-pane-control-cascading-loading-items.png)

   <br/>

  <span data-ttu-id="b4a4b-284">Nachdem die verfügbaren Elemente geladen wurden, wird die Element-Dropdownliste aktiviert.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-284">After the available items have been loaded, the item dropdown becomes enabled.</span></span>

  ![Auswählen eines Listenelements aus der Element-Dropdownliste im Webpart-Eigenschaftenbereich](../../../images/custom-property-pane-control-cascading-items-loaded-enabled.png)

   <br/>

  <span data-ttu-id="b4a4b-286">Nach dem Auswählen eines Elements in der Element-Dropdownliste wird das Webpart aktualisiert und zeigt das ausgewählte Element im Text an.</span><span class="sxs-lookup"><span data-stu-id="b4a4b-286">After selecting an item in the item dropdown the web part is refreshed showing the selected item in its body.</span></span>

  ![Ausgewählte Liste und Element, gerendert im Webpart](../../../images/custom-property-pane-control-cascading-selected-list-item.png)

## <a name="see-also"></a><span data-ttu-id="b4a4b-288">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="b4a4b-288">See also</span></span>

- [<span data-ttu-id="b4a4b-289">Verwenden von kaskadierenden Dropdowns in Webparteigenschaften</span><span class="sxs-lookup"><span data-stu-id="b4a4b-289">Use cascading dropdowns in web part properties</span></span>](./use-cascading-dropdowns-in-web-part-properties.md)