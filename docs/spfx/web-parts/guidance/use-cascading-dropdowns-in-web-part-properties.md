---
title: Verwenden von kaskadierenden Dropdowns in Webparteigenschaften
description: "Erfahren Sie, wie Sie kaskadierende Dropdown-Steuerelemente im Eigenschaftenbereich von clientseitigen SharePoint-Webparts erstellen können, ohne ein benutzerdefiniertes Steuerelement für den Eigenschaftenbereich zu programmieren."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: 5c163108968bdf45b4847c3487bf275b371b1380
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="use-cascading-dropdowns-in-web-part-properties"></a><span data-ttu-id="52975-103">Verwenden von kaskadierenden Dropdowns in Webparteigenschaften</span><span class="sxs-lookup"><span data-stu-id="52975-103">Use cascading dropdowns in web part properties</span></span>

<span data-ttu-id="52975-104">Beim Entwerfen des Eigenschaftenbereichs Ihrer clientseitigen SharePoint-Webparts arbeiten Sie vielleicht mit Webparteigenschaften, deren Optionen basierend auf dem in einer anderen Eigenschaft ausgewählten Wert angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="52975-104">When designing the property pane for your SharePoint client-side web parts, you may have one web part property that displays its options based on the  value selected in another property.</span></span> <span data-ttu-id="52975-105">Dieses Szenario findet sich in der Regel bei der Implementierung von kaskadierenden Dropdown-Steuerelementen.</span><span class="sxs-lookup"><span data-stu-id="52975-105">This scenario typically occurs when implementing cascading dropdown controls.</span></span> <span data-ttu-id="52975-106">In diesem Artikel erfahren Sie, wie Sie kaskadierende Dropdown-Steuerelemente im Eigenschaftenbereich von Webparts erstellen können, ohne ein benutzerdefiniertes Steuerelement für den Eigenschaftenbereich zu programmieren.</span><span class="sxs-lookup"><span data-stu-id="52975-106">In this article, you learn how to create cascading dropdown controls in the web part property pane without developing a custom property pane control.</span></span>

![Beispiel für eine Seite mit deaktiviertem Elementdropdown und einem Webpart-Platzhalter, der die aktualisierte Liste der Elementoptionen lädt](../../../images/react-cascading-dropdowns-loading-indicator-when-loading-items.png)

<span data-ttu-id="52975-108">Der Quellcode des Webparts, mit dem wir arbeiten, steht auf GitHub zur Verfügung, unter [sp-dev-fx-webparts/samples/react-custompropertypanecontrols](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span><span class="sxs-lookup"><span data-stu-id="52975-108">The source of the working web part is available on GitHub at [sp-dev-fx-webparts/samples/react-custompropertypanecontrols/](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span></span>

> [!NOTE] 
> <span data-ttu-id="52975-109">Bevor Sie die Anleitung in diesem Artikel umsetzen können, müssen Sie [die Entwicklungsumgebung für Ihr clientseitiges SharePoint-Webpart einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="52975-109">Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-new-project"></a><span data-ttu-id="52975-110">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="52975-110">Create new project</span></span>

1. <span data-ttu-id="52975-111">Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt:</span><span class="sxs-lookup"><span data-stu-id="52975-111">Start by creating a new folder for your project:</span></span>

  ```sh
  md react-cascadingdropdowns
  ```

2. <span data-ttu-id="52975-112">Wechseln Sie in den Projektordner:</span><span class="sxs-lookup"><span data-stu-id="52975-112">Go to the project folder:</span></span>

  ```sh
  cd react-cascadingdropdowns
  ```

3. <span data-ttu-id="52975-113">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="52975-113">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="52975-114">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="52975-114">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="52975-115">**react-cascadingdropdowns** als Lösungsname</span><span class="sxs-lookup"><span data-stu-id="52975-115">**react-cascadingdropdowns** as your solution name</span></span>
  - <span data-ttu-id="52975-116">**Aktuellen Ordner verwenden** als Speicherort für die Dateien</span><span class="sxs-lookup"><span data-stu-id="52975-116">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="52975-117">**React** als Eintrittspunkt für die Webpart-Erstellung</span><span class="sxs-lookup"><span data-stu-id="52975-117">**React** as the starting point to build the web part</span></span>
  - <span data-ttu-id="52975-118">**Listenelemente** als Namen des Webparts</span><span class="sxs-lookup"><span data-stu-id="52975-118">**List items** as your web part name</span></span>
  - <span data-ttu-id="52975-119">**Zeigt Listenelemente aus der ausgewählten Liste an** als Beschreibung Ihres Webparts</span><span class="sxs-lookup"><span data-stu-id="52975-119">**Shows list items from the selected list** as your web part description</span></span>

  ![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/react-cascading-dropdowns-yo-sharepoint.png)

5. <span data-ttu-id="52975-121">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="52975-121">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="52975-122">Öffnen Sie den Projektordner in einem Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="52975-122">Open your project folder in your code editor.</span></span> <span data-ttu-id="52975-123">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch auch jeden beliebigen anderen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="52975-123">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

  ![SharePoint-Framework-Projekt in Visual Studio Code](../../../images/react-cascading-dropdowns-visual-studio-code.png)

## <a name="define-a-web-part-property-to-store-the-selected-list"></a><span data-ttu-id="52975-125">Definieren einer Webparteigenschaft zum Speichern der ausgewählten Liste</span><span class="sxs-lookup"><span data-stu-id="52975-125">Define a web part property to store the selected list</span></span>

<span data-ttu-id="52975-126">In diesem Tutorial erstellen Sie ein Webpart, in dem Listenelemente aus einer ausgewählten SharePoint-Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="52975-126">You will build a web part that displays list items from a selected SharePoint list.</span></span> <span data-ttu-id="52975-127">Benutzer können die gewünschte Liste im Eigenschaftenbereich des Webparts auswählen.</span><span class="sxs-lookup"><span data-stu-id="52975-127">Users are able to select a list in the web part property pane.</span></span> <span data-ttu-id="52975-128">Erstellen Sie eine neue Webparteigenschaft namens **listName**, in der die ausgewählte Liste gespeichert wird:</span><span class="sxs-lookup"><span data-stu-id="52975-128">To store the selected list, create a new web part property named **listName**.</span></span>

1. <span data-ttu-id="52975-p104">Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPartManifest.json**. Ersetzen Sie die Standardeigenschaft **description** durch eine neue Eigenschaft mit dem Namen `listName`.</span><span class="sxs-lookup"><span data-stu-id="52975-p104">In the code editor, open the **src/webparts/listItems/ListItemsWebPartManifest.json** file. Replace the default **description** property with a new property named `listName`.</span></span>

  ![Webpartmanifest mit hervorgehobener Webparteigenschaft „listName“](../../../images/react-cascading-dropdowns-listname-property-web-part-manifest.png)

2. <span data-ttu-id="52975-132">Öffnen Sie die Datei **src/webparts/listItems/IListItemsWebPartProps.ts**, und ersetzen Sie den in ihr enthaltenen Code durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="52975-132">Open the **src/webparts/listItems/IListItemsWebPartProps.ts** file, and replace its contents with:</span></span>

  ```typescript
  export interface IListItemsWebPartProps {
    listName: string;
  }
  ```

3. <span data-ttu-id="52975-133">Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** die Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="52975-133">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the **render** method to:</span></span>

  ```typescript
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

4. <span data-ttu-id="52975-134">Aktualisieren Sie **propertyPaneSettings** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="52975-134">Update **propertyPaneSettings** to:</span></span>

  ```typescript
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
                    label: strings.ListNameFieldLabel
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

5. <span data-ttu-id="52975-135">Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die Schnittstelle **IListItemsStrings** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="52975-135">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsStrings** interface to:</span></span>

  ```typescript
  declare interface IListItemsStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
  }
  ```

6. <span data-ttu-id="52975-136">Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ListNameFieldLabel** hinzu:</span><span class="sxs-lookup"><span data-stu-id="52975-136">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ListNameFieldLabel** string:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListNameFieldLabel": "List"
    }
  });
  ```

7. <span data-ttu-id="52975-137">Ändern Sie in der Datei **src/webparts/listItems/components/ListItems.tsx** den Code der Methode **render** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="52975-137">In the **src/webparts/listItems/components/ListItems.tsx** file, change the contents of the **render** method to:</span></span>

  ```tsx
  export default class ListItems extends React.Component<IListItemsProps, {}> {
  public render(): JSX.Element {
      return (
          <div className={styles.listItems}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
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

8. <span data-ttu-id="52975-138">Ändern Sie in der Datei **src/webparts/listItems/components/IListItemsProps.ts** die **IListItemsProps**-Oberfläche in:</span><span class="sxs-lookup"><span data-stu-id="52975-138">In the **src/webparts/listItems/components/IListItemsProps.ts** file, change the **IListItemsProps** interface to:</span></span>

  ```typescript
  export interface IListItemsProps {
    listName: string;
  }
  ```

9. <span data-ttu-id="52975-139">Führen Sie den folgenden Befehl aus, um sicherzustellen, dass das Projekt ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="52975-139">Run the following command to verify that the project is running:</span></span>

  ```sh
  gulp serve
  ```

10. <span data-ttu-id="52975-p105">Fügen Sie im Webbrowser das **Listenelement**-Webpart zum Zeichenbereich hinzu, und öffnen Sie die Eigenschaften. Überprüfen Sie, dass der für die **List**-Eigenschaft festgelegte Wert im Webparttext angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="52975-p105">In the web browser, add the **List items** web part to the canvas and open its properties. Verify that the value set for the **List** property is displayed in the web part body.</span></span>

  ![Webpart, in dem der Wert der listName-Eigenschaft angezeigt wird](../../../images/react-cascading-dropdowns-web-part-first-run.png)



## <a name="populate-the-dropdown-with-sharepoint-lists-to-choose-from"></a><span data-ttu-id="52975-143">Ausfüllen des Dropdowns mit SharePoint-Listen, aus denen eine Auswahl getroffen werden kann</span><span class="sxs-lookup"><span data-stu-id="52975-143">Populate the dropdown with SharePoint lists to choose from</span></span>

<span data-ttu-id="52975-144">An diesem Punkt gibt der Benutzer an, welche Liste das Webpart verwenden soll. Hierzu gibt er manuell den Namen der entsprechenden Liste ein.</span><span class="sxs-lookup"><span data-stu-id="52975-144">At this point, a user specifies which list the web part should use by manually entering the list name.</span></span> <span data-ttu-id="52975-145">Diese Vorgehensweise ist fehleranfällig, und im Idealfall sollten Benutzer eine der Listen auswählen, die auf der aktuellen SharePoint-Website vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="52975-145">This is error-prone, and ideally you want users to choose one of the lists existing in the current SharePoint site.</span></span>

### <a name="use-dropdown-control-to-render-the-listname-property"></a><span data-ttu-id="52975-146">Verwenden des Dropdown-Steuerelements zum Rendern der Eigenschaft „listName“</span><span class="sxs-lookup"><span data-stu-id="52975-146">Use dropdown control to render the listName property</span></span>

1. <span data-ttu-id="52975-147">Fügen Sie in der Klasse **ListItemsWebPart** einen Verweis auf die Klasse **PropertyPaneDropdown** im oberen Bereich des Webparts hinzu.</span><span class="sxs-lookup"><span data-stu-id="52975-147">In the **ListItemsWebPart** class, add a reference to the **PropertyPaneDropdown** class in the top section of the web part.</span></span> <span data-ttu-id="52975-148">Ersetzen Sie die Importklausel, von der die Klasse **PropertyPaneTextField** geladen wird, durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="52975-148">Replace the import clause that loads the **PropertyPaneTextField** class with:</span></span>

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneTextField,
    PropertyPaneDropdown,
    IPropertyPaneDropdownOption
  } from '@microsoft/sp-webpart-base';
  ```

2. <span data-ttu-id="52975-149">Fügen Sie in der Klasse **ListItemsWebPart** eine neue Variable mit dem Namen **lists** hinzu, in der Informationen über alle auf der aktuellen Website verfügbaren Liste gespeichert werden:</span><span class="sxs-lookup"><span data-stu-id="52975-149">In the **ListItemsWebPart** class, add a new variable named **lists** to store information about all available lists in the current site:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    private lists: IPropertyPaneDropdownOption[];
    // ...
  }
  ```

3. <span data-ttu-id="52975-150">Fügen Sie eine neue Klassenvariable mit dem Namen **listsDropdownDisabled** hinzu.</span><span class="sxs-lookup"><span data-stu-id="52975-150">Add a new class variable named **listsDropdownDisabled**.</span></span> <span data-ttu-id="52975-151">Diese Variable legt fest, ob das Listendropdown aktiviert ist oder nicht.</span><span class="sxs-lookup"><span data-stu-id="52975-151">This variable determines whether the list dropdown is enabled or not.</span></span> <span data-ttu-id="52975-152">Das Dropdown sollte solange deaktiviert sein, bis das Webpart die Informationen zu den auf der aktuellen Website verfügbaren Listen abgerufen hat.</span><span class="sxs-lookup"><span data-stu-id="52975-152">Until the web part retrieves the information about the lists available in the current site, the dropdown should be disabled.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private listsDropdownDisabled: boolean = true;
    // ...
  }
  ```

4. <span data-ttu-id="52975-153">Ändern Sie den Getter **propertyPaneSettings** so, dass er zum Rendern der Eigenschaft **listName** das Dropdown-Steuerelement verwendet:</span><span class="sxs-lookup"><span data-stu-id="52975-153">Change the **propertyPaneSettings** getter to use the dropdown control to render the **listName** property:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected get propertyPaneSettings(): IPropertyPaneSettings {
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
                  PropertyPaneDropdown('listName', {
                    label: strings.ListNameFieldLabel,
                    options: this.lists,
                    disabled: this.listsDropdownDisabled
                  })
                ]
              }
            ]
          }
        ]
      };
    }
  }
  ```

5. <span data-ttu-id="52975-154">Führen Sie den folgenden Befehl aus, um zu überprüfen, ob alles wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="52975-154">Run the following command to verify that it's working as expected:</span></span>

  ```sh
  gulp serve
  ```

  ![Die im Webpart-Eigenschaftenbereich mithilfe eines Dropdownsteuerelements gerenderte listName-Eigenschaft](../../../images/react-cascading-dropdowns-listname-property-pane-dropdown.png)


### <a name="show-available-lists-in-the-list-dropdown"></a><span data-ttu-id="52975-156">Anzeigen verfügbarer Listen im Listendropdown</span><span class="sxs-lookup"><span data-stu-id="52975-156">Show available lists in the list dropdown</span></span>

<span data-ttu-id="52975-157">Im vorangegangenen Schritt haben Sie das Dropdown-Steuerelement der Eigenschaft **listName** mit der Klasseneigenschaft **lists** verknüpft.</span><span class="sxs-lookup"><span data-stu-id="52975-157">Previously, you associated the dropdown control of the **listName** property with the **lists** class property.</span></span> <span data-ttu-id="52975-158">Da Sie noch keine Werte in das Element geladen haben, bleibt das Dropdown **List** im Eigenschaftenbereich des Webparts deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="52975-158">Because you haven't loaded any values into it yet, the **List** dropdown in the web part property pane remains disabled.</span></span> <span data-ttu-id="52975-159">In diesem Abschnitt erweitern Sie das Webpart so, dass es Informationen zu den verfügbaren Listen lädt.</span><span class="sxs-lookup"><span data-stu-id="52975-159">In this section, you will extend the web part to load the information about available lists.</span></span>

1. <span data-ttu-id="52975-p110">Fügen Sie in der Klasse **ListItemsWebPart** eine Methode zum Laden aller verfügbaren Listen hinzu. Hier verwenden Sie simulierte Daten; Sie können aber auch die SharePoint-REST-API aufrufen, um die Liste aller im aktuellen Web verfügbaren Listen abzurufen. Um das Laden aus einem externen Dienst zu simulieren, implementiert die Methode eine Verzögerung von 2 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="52975-p110">In the **ListItemsWebPart** class, add a method to load available lists. You will use mock data, but you could also call the SharePoint REST API to retrieve the list of available lists from the current web. To simulate loading options from an external service, the method uses a two-second delay.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private loadLists(): Promise<IPropertyPaneDropdownOption[]> {
      return new Promise<IPropertyPaneDropdownOption[]>((resolve: (options: IPropertyPaneDropdownOption[]) => void, reject: (error: any) => void) => {
        setTimeout((): void => {
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

2. <span data-ttu-id="52975-163">Laden Sie Informationen zu den verfügbaren Listen in das Listendropdown.</span><span class="sxs-lookup"><span data-stu-id="52975-163">Load information about available lists into the list dropdown.</span></span> <span data-ttu-id="52975-164">Überschreiben Sie dazu in der Klasse **ListItemsWebPart**die Methode **onPropertyPaneConfigurationStart** mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="52975-164">In the **ListItemsWebPart** class, override the **onPropertyPaneConfigurationStart** method by using the following code:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected onPropertyPaneConfigurationStart(): void {
      this.listsDropdownDisabled = !this.lists;

      if (this.lists) {
        return;
      }

      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'lists');

      this.loadLists()
        .then((listOptions: IPropertyPaneDropdownOption[]): void => {
          this.lists = listOptions;
          this.listsDropdownDisabled = false;
          this.context.propertyPane.refresh();
          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          this.render();
        });
    }
    // ...
  }
  ```

  <span data-ttu-id="52975-165">Die Methode **onPropertyPaneConfigurationStart** wird vom SharePoint-Framework aufgerufen, sobald der Eigenschaftenbereich des Webparts geöffnet wurde.</span><span class="sxs-lookup"><span data-stu-id="52975-165">The **onPropertyPaneConfigurationStart** method is called by the SharePoint Framework after the web part property pane for the web part has been opened.</span></span> 
  - <span data-ttu-id="52975-166">Die Methode prüft zuerst, ob die Informationen zu den auf der aktuellen Website verfügbaren Listen geladen wurden.</span><span class="sxs-lookup"><span data-stu-id="52975-166">First, the method checks if the information about the lists available in the current site has been loaded.</span></span> 
  - <span data-ttu-id="52975-167">Wurden die Listeninformationen geladen, wird das Listendropdown aktiviert.</span><span class="sxs-lookup"><span data-stu-id="52975-167">If the list information is loaded, the list dropdown is enabled.</span></span> 
  - <span data-ttu-id="52975-168">Wurden die Informationen zu den Listen noch nicht geladen, wird die Ladeanzeige angezeigt. Sie informiert den Benutzer darüber, dass das Webpart gerade Informationen zu Listen abruft.</span><span class="sxs-lookup"><span data-stu-id="52975-168">If the list information about lists has not been loaded yet, the loading indicator is displayed, which informs the user that the web part is loading information about lists.</span></span>

  ![Die während des Ladens von Informationen zu verfügbaren Listen angezeigte Ladeanzeige im Webpart](../../../images/react-cascading-dropdowns-loading-indicator-when-loading-list-info.png)

  <span data-ttu-id="52975-170">Sobald die Informationen zu den verfügbaren Listen geladen wurden, weist die Methode die abgerufenen Daten der Klassenvariablen **lists** zu, aus der sie vom Listendropdown referenziert werden können.</span><span class="sxs-lookup"><span data-stu-id="52975-170">After the information about available lists has been loaded, the method assigns the retrieved data to the **lists** class variable, from which it can be used by the list dropdown.</span></span> 
  
  <span data-ttu-id="52975-171">Als Nächstes wird das Dropdown aktiviert, sodass der Benutzer eine Liste auswählen kann.</span><span class="sxs-lookup"><span data-stu-id="52975-171">Next, the dropdown is enabled allowing the user to select a list.</span></span> <span data-ttu-id="52975-172">Durch Aufrufen von **this.context.propertyPane.refresh()** wird der Webpart-Eigenschaftenbereich aktualisiert und übernimmt die neuesten Änderungen am Listendropdown.</span><span class="sxs-lookup"><span data-stu-id="52975-172">By calling **this.context.propertyPane.refresh()**, the web part property pane is refreshed and it reflects the latest changes to the list dropdown.</span></span> 
  
  <span data-ttu-id="52975-173">Sobald Listeninformationen geladen wurden, wird die Ladeanzeige über einen Aufruf der Methode **clearLoadingIndicator** entfernt.</span><span class="sxs-lookup"><span data-stu-id="52975-173">After list information is loaded, the loading indicator is removed by a call to the **clearLoadingIndicator** method.</span></span> <span data-ttu-id="52975-174">Da durch das Aufrufen dieser Methode die Webpart-Benutzeroberfläche gelöscht wird, wird die Methode **render** aufgerufen, um ein Neurendern des Webparts zu erzwingen.</span><span class="sxs-lookup"><span data-stu-id="52975-174">Because calling this method clears the web part user interface, the **render** method is called to force the web part to re-render.</span></span>

3. <span data-ttu-id="52975-175">Überprüfen Sie mit dem folgenden Befehl, ob alles wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="52975-175">Run the following command to confirm that everything is working as expected:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="52975-176">Wenn Sie dem Zeichenbereich ein Webpart hinzufügen und seinen Eigenschaftenbereich öffnen, sollten Sie das Listendropdown mit den verfügbaren Listen sehen, aus denen der Benutzer eine Auswahl treffen kann.</span><span class="sxs-lookup"><span data-stu-id="52975-176">When you add a web part to the canvas and open its property pane, you should see the lists dropdown filled with available lists for the user to choose from.</span></span>

  ![Listendropdown im Webpart-Eigenschaftenbereich, in dem die verfügbaren Listen angezeigt werden](../../../images/react-cascading-dropdowns-list-dropdown-available-lists.png)



## <a name="allow-users-to-select-an-item-from-the-selected-list"></a><span data-ttu-id="52975-178">Ermöglichen, dass Benutzer ein Element aus der ausgewählten Listen auswählen können</span><span class="sxs-lookup"><span data-stu-id="52975-178">Allow users to select an item from the selected list</span></span>

<span data-ttu-id="52975-179">Beim Erstellen von Webparts müssen Sie es Benutzern häufig ermöglichen, eine Option aus einer Reihe von Werten auszuwählen, die von einem zuvor ausgewählten Wert festgelegt werden. Beispiele wären die Auswahl eines Landes oder einer Region auf Basis des zuvor ausgewählten Kontinents oder die Auswahl eines Listenelements aus einer zuvor ausgewählten Liste.</span><span class="sxs-lookup"><span data-stu-id="52975-179">When building web parts, you often need to allow users to choose an option from a set of values determined by a previously selected value, such as choosing a country/region based on the selected continent, or choosing a list item from a selected list.</span></span> <span data-ttu-id="52975-180">Eine solche Gestaltung der Benutzeroberfläche wird häufig als kaskadierende Dropdowns bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="52975-180">This user experience is often referred to as cascading dropdowns.</span></span> <span data-ttu-id="52975-181">Mithilfe der standardmäßigen Funktionen von clientseitigen SharePoint-Framework-Webparts können Sie kaskadierende Dropdowns im Webpart-Eigenschaftenbereich erstellen.</span><span class="sxs-lookup"><span data-stu-id="52975-181">Using the standard SharePoint Framework client-side web parts capabilities, you can build cascading dropdowns in the web part property pane.</span></span> <span data-ttu-id="52975-182">Hierzu erweitern Sie das zuvor erstellte Webpart um eine Funktion zur Auswahl eines Listenelements aus einer zuvor ausgewählten Liste.</span><span class="sxs-lookup"><span data-stu-id="52975-182">To do this, you extend the previously built web part with the ability to choose a list item based on the previously selected list.</span></span>

![Geöffnetes Listenelement-Dropdown im Webpart-Eigenschaftenbereich](../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)

### <a name="add-item-web-part-property"></a><span data-ttu-id="52975-184">Hinzufügen der Webparteigenschaft „itemName“</span><span class="sxs-lookup"><span data-stu-id="52975-184">Add item web part property</span></span>

1. <span data-ttu-id="52975-185">Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="52975-185">In the code editor, open the **src/webparts/listItems/ListItemsWebPart.manifest.json** file.</span></span> <span data-ttu-id="52975-186">Fügen Sie im Abschnitt **properties** eine neue Eigenschaft mit dem Namen **itemName** hinzu. Der Code sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="52975-186">To the **properties** section, add a new property named **itemName** so that it appears as follows:</span></span>

  ```json
  {
    // ...
    "properties": {
      "listName": "",
      "itemName": ""
    }
    // ...
  }
  ```

  <br/>

  ![Webpartmanifest mit hervorgehobener Webparteigenschaft „itemName“](../../../images/react-cascading-dropdowns-itemname-property-web-part-manifest.png)

2. <span data-ttu-id="52975-188">Ändern Sie den Code in der Datei **src/webparts/listItems/IListItemsWebPartProps.ts** in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="52975-188">Change the code in the **src/webparts/listItems/IListItemsWebPartProps.ts** file to:</span></span>

  ```typescript
  export interface IListItemsWebPartProps {
    listName: string;
    itemName: string;
  }
  ```

3. <span data-ttu-id="52975-189">Ändern Sie den Code in der Datei **src/webparts/listItems/components/IListItemsProps.ts** in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="52975-189">Change the code in the **src/webparts/listItems/components/IListItemsProps.ts** file to:</span></span>

  ```typescript
  export interface IListItemsProps {
    listName: string;
    itemName: string;
  }
  ```

4. <span data-ttu-id="52975-190">Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** den Code der **render**-Methode in:</span><span class="sxs-lookup"><span data-stu-id="52975-190">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the code of the **render** method to:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
        listName: this.properties.listName,
        itemName: this.properties.itemName
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

5. <span data-ttu-id="52975-191">Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die **IListItemsStrings**-Schnittstelle in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="52975-191">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsStrings** interface to:</span></span>

  ```typescript
  declare interface IListItemsStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
    ItemNameFieldLabel: string;
  }
  ```

6. <span data-ttu-id="52975-192">Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ItemNameFieldLabel** hinzu.</span><span class="sxs-lookup"><span data-stu-id="52975-192">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ItemNameFieldLabel** string.</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListNameFieldLabel": "List",
      "ItemNameFieldLabel": "Item"
    }
  });
  ```

### <a name="render-the-value-of-the-item-web-part-property"></a><span data-ttu-id="52975-193">Rendern des Werts der item-Webparteigenschaft</span><span class="sxs-lookup"><span data-stu-id="52975-193">Render the value of the item web part property</span></span>

<span data-ttu-id="52975-194">Ändern Sie in der Datei **src/webparts/listItems/components/ListItems.tsx** die **render**-Methode in:</span><span class="sxs-lookup"><span data-stu-id="52975-194">In the **src/webparts/listItems/components/ListItems.tsx** file, change the **render** method to:</span></span>

```tsx
export default class ListItems extends React.Component<IListItemsProps, {}> {
  public render(): JSX.Element {
    return (
        <div className={styles.listItems}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.itemName)}</p>
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

### <a name="allow-users-to-choose-the-item-from-a-list"></a><span data-ttu-id="52975-195">Ermöglichen, dass Benutzer das Element aus einer Liste auswählen können</span><span class="sxs-lookup"><span data-stu-id="52975-195">Allow users to choose the item from a list</span></span>

<span data-ttu-id="52975-196">Ähnlich wie die Benutzer eine Liste aus einem Dropdown auswählen können, sollten sie auch das Element aus der Liste der verfügbaren Elemente auswählen können.</span><span class="sxs-lookup"><span data-stu-id="52975-196">Similar to how users can select a list by using a dropdown, they should be able to select the item from the list of available items.</span></span>

1. <span data-ttu-id="52975-197">Fügen Sie in der Klasse **ListItemsWebPart** eine neue Variable mit dem Namen **items** hinzu, in der die Informationen zu allen in der aktuell ausgewählten Liste verfügbaren Elementen gespeichert werden:</span><span class="sxs-lookup"><span data-stu-id="52975-197">In the **ListItemsWebPart** class, add a new variable named **items**, which you use to store information about all available items in the currently selected list.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private items: IPropertyPaneDropdownOption[];
    // ...
  }
  ```

2. <span data-ttu-id="52975-198">Fügen Sie eine neue Klassenvariable mit dem Namen **itemsDropdownDisabled** hinzu.</span><span class="sxs-lookup"><span data-stu-id="52975-198">Add a new class variable named **itemsDropdownDisabled**.</span></span> <span data-ttu-id="52975-199">Diese Variable legt fest, ob das Elementdropdown aktiviert ist oder nicht.</span><span class="sxs-lookup"><span data-stu-id="52975-199">This variable determines whether the items dropdown should be enabled or not.</span></span> <span data-ttu-id="52975-200">Benutzer sollten erst dann ein Element auswählen können, nachdem sie eine Liste ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="52975-200">Users should be able to select an item only after they selected a list.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private itemsDropdownDisabled: boolean = true;
    // ...
  }
  ```

3. <span data-ttu-id="52975-201">Ändern Sie den **propertyPaneSettings**-Getter im Dropdown-Steuerelement, um die **itemName**-Eigenschaft zu rendern.</span><span class="sxs-lookup"><span data-stu-id="52975-201">Change the **propertyPaneSettings** getter to use the dropdown control to render the **itemName** property.</span></span>

  ```typescript
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
                  PropertyPaneDropdown('listName', {
                    label: strings.ListNameFieldLabel,
                    options: this.lists,
                    disabled: this.listsDropdownDisabled
                  }),
                  PropertyPaneDropdown('itemName', {
                    label: strings.ItemNameFieldLabel,
                    options: this.items,
                    disabled: this.itemsDropdownDisabled
                  })
                ]
              }
            ]
          }
        ]
      };
    }
  }
  ```

4. <span data-ttu-id="52975-202">Führen Sie den folgenden Befehl aus, um sicherzustellen, dass er wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="52975-202">Run the following command to verify that it's working as expected:</span></span>

  ```sh
  gulp serve
  ```

  ![Die im Webpart-Eigenschaftenbereich mithilfe eines Dropdown-Steuerelements gerenderte itemName-Eigenschaft](../../../images/react-cascading-dropdowns-itemname-property-pane-dropdown.png)



### <a name="show-items-available-in-the-selected-list-in-the-item-dropdown"></a><span data-ttu-id="52975-204">Anzeigen von verfügbaren Elementen in der ausgewählten Liste im Elementdropdown</span><span class="sxs-lookup"><span data-stu-id="52975-204">Show items available in the selected list in the item dropdown</span></span>

<span data-ttu-id="52975-205">Im vorangegangenen Abschnitt haben Sie ein Dropdown-Steuerelement definiert, dass die Eigenschaft **itemName** im Eigenschaftenbereich des Webparts rendert.</span><span class="sxs-lookup"><span data-stu-id="52975-205">Previously, you defined a dropdown control to render the **itemName** property in the web part property pane.</span></span> <span data-ttu-id="52975-206">Als Nächstes erweitern Sie das Webpart so, dass die Informationen zu den in der ausgewählten Liste verfügbaren Elementen geladen und die Elemente im Elementdropdown angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="52975-206">Next, you extend the web part to load the information about items available in the selected list, and show the items in the item dropdown.</span></span>

1. <span data-ttu-id="52975-207">Fügen Sie eine Methode zum Laden der Listenelemente hinzu.</span><span class="sxs-lookup"><span data-stu-id="52975-207">Add method to load list items.</span></span> <span data-ttu-id="52975-208">Fügen Sie hierzu in der Datei **src/webparts/listItems/ListItemsWebPart.ts** in der Klasse **ListItemsWebPart** eine neue Methode zum Laden der verfügbaren Listenelemente aus der ausgewählten Liste hinzu</span><span class="sxs-lookup"><span data-stu-id="52975-208">In the **src/webparts/listItems/ListItemsWebPart.ts** file, in the **ListItemsWebPart** class, add a new method to load available list items from the selected list.</span></span> <span data-ttu-id="52975-209">(wie auch bei der Methode zum Laden der verfügbaren Listen verwenden Sie hier simulierte Daten):</span><span class="sxs-lookup"><span data-stu-id="52975-209">(Like the method for loading available lists, you use mock data.)</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private loadItems(): Promise<IPropertyPaneDropdownOption[]> {
      if (!this.properties.listName) {
        // resolve to empty options since no list has been selected
        return Promise.resolve();
      }

      const wp: ListItemsWebPart = this;

      return new Promise<IPropertyPaneDropdownOption[]>((resolve: (options: IPropertyPaneDropdownOption[]) => void, reject: (error: any) => void) => {
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

  <span data-ttu-id="52975-p119">Die **loadItems**-Methode gibt simulierte Listenelemente für die zuvor ausgewählte Liste zurück. Wenn keine Liste ausgewählt wurde, löst die Methode die Zusage ohne Daten.</span><span class="sxs-lookup"><span data-stu-id="52975-p119">The **loadItems** method returns mock list items for the previously selected list. When no list has been selected, the method resolves the promise without any data.</span></span>

2. <span data-ttu-id="52975-212">Laden Sie die Informationen zu den verfügbaren Elementen in das Elementdropdown.</span><span class="sxs-lookup"><span data-stu-id="52975-212">Load information about available items into the item dropdown.</span></span> <span data-ttu-id="52975-213">Erweitern Sie hierzu in der Klasse **ListItemsWebPart** die Methode **onPropertyPaneConfigurationStart** so, dass sie Elemente aus der ausgewählten Liste lädt:</span><span class="sxs-lookup"><span data-stu-id="52975-213">In the **ListItemsWebPart** class, extend the **onPropertyPaneConfigurationStart** method to load items for the selected list:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected onPropertyPaneConfigurationStart(): void {
      this.listsDropdownDisabled = !this.lists;
      this.itemsDropdownDisabled = !this.properties.listName || !this.items;

      if (this.lists) {
        return;
      }

      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'options');

      this.loadLists()
        .then((listOptions: IPropertyPaneDropdownOption[]): Promise<IPropertyPaneDropdownOption[]> => {
          this.lists = listOptions;
          this.listsDropdownDisabled = false;
          this.context.propertyPane.refresh();
          return this.loadItems();
        })
        .then((itemOptions: IPropertyPaneDropdownOption[]): void => {
          this.items = itemOptions;
          this.itemsDropdownDisabled = !this.properties.listName;
          this.context.propertyPane.refresh();
          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          this.render();
        });
    }
    // ...
  }
  ```

  <span data-ttu-id="52975-214">Bei der Initialisierung ermittelt das Webpart zuerst, ob das Elementdropdown aktiviert werden soll oder nicht.</span><span class="sxs-lookup"><span data-stu-id="52975-214">When initializing, the web part first determines if the items dropdown should be enabled or not.</span></span> <span data-ttu-id="52975-215">Hat der Benutzer zuvor eine Liste ausgewählt, kann er nun ein Element aus dieser Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="52975-215">If the user previously selected a list, they can select an item from that list.</span></span> <span data-ttu-id="52975-216">Wurde keine Liste ausgewählt, ist das Elementdropdown deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="52975-216">If no list was selected, the item dropdown is disabled.</span></span>

  <span data-ttu-id="52975-p122">Sie haben den zuvor definierten Code erweitert, der die Informationen zu verfügbaren Listen lädt, um die Informationen zu verfügbaren Elementen in der ausgewählten Liste zu laden. Der Code weist dann die abgerufenen Informationen der **items**-Klassenvariablen zur Verwendung vom Elementdropdown zu Schließlich löscht der Code die Ladeanzeige, und der Benutzer kann beginnen, mit dem Webpart zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="52975-p122">You extended the previously defined code, which loads the information about available lists, to load the information about items available in the selected list. The code then assigns the retrieved information to the **items** class variable for use by the item dropdown. Finally, the code clears the loading indicator and allows the user to start working with the web part.</span></span>

3. <span data-ttu-id="52975-220">Überprüfen Sie mit dem folgenden Befehl, ob alles wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="52975-220">Run the following command to confirm that everything is working as expected:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="52975-p123">Das Elementdropdown ist, wie erforderlich, anfänglich deaktiviert, sodass Benutzer zuerst eine Liste auswählen müssen. Doch an diesem Punkt bleibt das Elementdropdown auch nach dem Auswählen einer Liste deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="52975-p123">As required, initially the item dropdown is disabled, requiring users to select a list first. But at this point, even after a list has been selected, the item dropdown remains disabled.</span></span>

  ![Auch nach dem Auswählen einer Liste deaktiviertes Elementdropdown](../../../images/react-cascading-dropdowns-list-selected-item-disabled.png)

4. <span data-ttu-id="52975-224">Sobald eine Liste ausgewählt wird, sollte der Eigenschaftenbereich des Webparts aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="52975-224">Update web part property pane after selecting a list.</span></span> <span data-ttu-id="52975-225">Wenn ein Benutzer eine Liste im Eigenschaftenbereich auswählt, sollte das Webpart entsprechend aktualisiert werden, sodass das Elementdropdown aktiviert wird und die Liste von verfügbaren Elementen in der ausgewählten Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="52975-225">When a user selects a list in the property pane, the web part should update, enabling the item dropdown and showing the list of items available in the selected list.</span></span>

  <span data-ttu-id="52975-226">Überschreiben Sie in der Datei **ListItemsWebPart.ts** in der Klasse **ListItemsWebPart** die Methode **onPropertyPaneFieldChanged** mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="52975-226">In the **ListItemsWebPart.ts** file, in the **ListItemsWebPart** class, override the **onPropertyPaneFieldChanged** method with the following code:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void {
      if (propertyPath === 'listName' &&
          newValue) {
        // push new list value
        super.onPropertyPaneFieldChanged(propertyPath, oldValue, newValue);
        // get previously selected item
        const previousItem: string = this.properties.itemName;
        // reset selected item
        this.properties.itemName = undefined;
        // push new item value
        this.onPropertyPaneFieldChanged('itemName', previousItem, this.properties.itemName);
        // disable item selector until new items are loaded
        this.itemsDropdownDisabled = true;
        // refresh the item selector control by repainting the property pane
        this.context.propertyPane.refresh();
        // communicate loading items
        this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'items');

        this.loadItems()
          .then((itemOptions: IPropertyPaneDropdownOption[]): void => {
            // store items
            this.items = itemOptions;
            // enable item selector
            this.itemsDropdownDisabled = false;
            // clear status indicator
            this.context.statusRenderer.clearLoadingIndicator(this.domElement);
            // re-render the web part as clearing the loading indicator removes the web part body
            this.render();
            // refresh the item selector control by repainting the property pane
            this.context.propertyPane.refresh();
          });
      }
      else {
        super.onPropertyPaneFieldChanged(propertyPath, oldValue, newValue);
      }
    }
    // ...
  }
  ```

  <span data-ttu-id="52975-p125">Nachdem der Benutzer eine Liste ausgewählt hat, wird der neu ausgewählte Wert im Webpart gespeichert. Da sich die ausgewählte Liste geändert hat, wird das zuvor ausgewählte Listenelement zurückgesetzt. Da nun eine Liste ausgewählt ist, werden im Webpart-Eigenschaftenbereich Listenelemente für diese spezielle Liste geladen. Beim Laden von Elementen sollte der Benutzer kein Element auswählen können.</span><span class="sxs-lookup"><span data-stu-id="52975-p125">After the user selected a list, the web part persists the newly selected value. Because the selected list changed, the web part resets the previously selected list item. Now that a list is selected, the web part property pane loads list items for that particular list. While loading items, the user shouldn't be able to select an item.</span></span>

  <span data-ttu-id="52975-231">Sobald die Elemente der ausgewählten Liste geladen wurden, werden sie der Klassenvariablen **items** zugewiesen, von wo sie vom Elementdropdown referenziert werden können.</span><span class="sxs-lookup"><span data-stu-id="52975-231">After the items for the selected list are loaded, they are assigned to the **items** class variable from where they can be referenced by the item dropdown.</span></span> <span data-ttu-id="52975-232">Da die Informationen zu verfügbaren Listenelementen jetzt verfügbar sind, wird das Elementdropdown aktiviert, und die Benutzer können ein Element auswählen.</span><span class="sxs-lookup"><span data-stu-id="52975-232">Now that the information about available list items is available, the item dropdown is enabled allowing users to choose an item.</span></span> <span data-ttu-id="52975-233">Die Ladeanzeige wird entfernt. Dadurch wird die Webpartoberfläche gelöscht, weswegen das Webpart neu gerendert werden muss.</span><span class="sxs-lookup"><span data-stu-id="52975-233">The loading indicator is removed, which clears the web part body which is why the web part should re-render.</span></span> <span data-ttu-id="52975-234">Im letzten Schritt wird der Eigenschaftenbereich des Webparts aktualisiert und übernimmt die neuesten Änderungen.</span><span class="sxs-lookup"><span data-stu-id="52975-234">Finally, the web part property pane refreshes to reflect the latest changes.</span></span>

  > [!NOTE] 
  > <span data-ttu-id="52975-235">Ab Drop 6 des SharePoint Frameworks gibt es einen Fehler in der React-Dropdownkomponente der Office UI Fabric, der dazu führt, dass das Dropdownsteuerelement nicht ordnungsgemäß funktioniert.</span><span class="sxs-lookup"><span data-stu-id="52975-235">In drop 6 of the SharePoint Framework there is a bug in the Office UI Fabric React Dropdown component that causes the dropdown control to work incorrectly.</span></span> <span data-ttu-id="52975-236">Eine temporäre Problemumgehung besteht darin, die Datei **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** zu bearbeiten und die Zeile **12027** zu ändern, und zwar von:</span><span class="sxs-lookup"><span data-stu-id="52975-236">A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line **12027** from:</span></span>
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="52975-237">in:</span><span class="sxs-lookup"><span data-stu-id="52975-237">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

<br/>

![Elementdropdown im Webpart-Eigenschaftenbereich mit den verfügbaren Listenelementen der ausgewählten Liste](../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)


## <a name="see-also"></a><span data-ttu-id="52975-239">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="52975-239">See also</span></span>

- [<span data-ttu-id="52975-240">Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="52975-240">Build custom controls for the property pane</span></span>](./build-custom-property-pane-controls.md)
