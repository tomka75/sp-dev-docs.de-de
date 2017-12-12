---
title: "Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 42b3b6858626ab110aa03202819ea174c0c3fd62
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="build-custom-controls-for-the-property-pane"></a>Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich

Das SharePoint Framework enthält eine Reihe von Standardsteuerelementen für den Eigenschaftenbereich. Doch manchmal benötigen Sie zusätzliche Funktionen, die über die grundlegenden Steuerelemente hinausgehen. Möglicherweise benötigen Sie asynchrone Updates für die Daten in einem Steuerelement oder eine bestimmte Benutzeroberfläche. Erstellen Sie ein benutzerdefiniertes Steuerelement für den Eigenschaftenbereich, um die benötigten Funktionen zu erhalten.

In diesem Artikel erfahren Sie, wie Sie ein benutzerdefiniertes Steuerelement für den Eigenschaftenbereich erstellen. Sie erstellen ein benutzerdefiniertes Dropdown-Steuerelement, das seine Daten asynchron aus einem externen Dienst lädt, ohne die Benutzeroberfläche des Webparts zu blockieren.

![Element-Dropdownliste, in der verfügbare Elemente nach dem Auswählen einer Liste im Listen-Dropdown geladen werden](../../../images/custom-property-pane-control-cascading-loading-items.png)

Der Quellcode des Webparts, mit dem wir arbeiten, steht auf GitHub zur Verfügung, unter [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).

> **Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint Framework-Lösungen erstellen können.

## <a name="create-new-project"></a>Erstellen eines neuen Projekts

Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.

```sh
md react-custompropertypanecontrol
```

Wechseln Sie zum Projektordner.

```sh
cd react-custompropertypanecontrol
```

Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen.

```sh
yo @microsoft/sharepoint
```

Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:

- **react-custompropertypanecontrol** als Lösungsname
- **Aktuellen Ordner verwenden** als Speicherort für die Dateien
- **Listenelemente** als Namen des Webparts
- **Zeigt Listenelemente aus der ausgewählten Liste an** als Beschreibung Ihres Webparts
- **React** als Eintrittspunkt für die Webpart-Erstellung

![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/custom-property-pane-control-yeoman.png)

Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

```sh
npm shrinkwrap
```

Öffnen Sie dann den Projektordner im Code-Editor. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.

![SharePoint Framework-Projekt in Visual Studio Code](../../../images/custom-property-pane-control-visual-studio-code.png)

## <a name="define-web-part-property-for-storing-the-selected-list"></a>Definieren der Webparteigenschaft zum Speichern der ausgewählten Liste

In dem Webpart, das Sie erstellen, werden Listenelemente aus der ausgewählten SharePoint-Liste erstellt. Benutzer können eine Liste in den Webparteigenschaften auswählen. Erstellen Sie zum Speichern der ausgewählten Liste eine neue Webparteigenschaft namens **listName**.

Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPartManifest.json** Ersetzen Sie die standardmäßige **description**-Eigenschaft durch eine neue Eigenschaft mit dem Namen `listName`.

![Webpartmanifest, bei dem die Webparteigenschaft 'listName' markiert ist](../../../images/custom-property-pane-control-list-property-web-part-manifest.png)

Öffnen Sie als Nächstes die Datei **src/webparts/listItems/IListItemsWebPartProps.ts**, und ersetzen Sie ihren Inhalt durch Folgendes:

```ts
export interface IListItemsWebPartProps {
  listName: string;
}
```

Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** die **render**-Methode in:

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

Aktualisieren Sie die **getPropertyPaneConfiguration**-Methode in:

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

Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die **IListItemsWebPartStrings**-Schnittstelle in Folgendes:

```ts
declare interface IListItemsWebPartStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListFieldLabel: string;
}
```

Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ListFieldLabel** hinzu.

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ListFieldLabel": "List"
  }
});
```

Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** den Inhalt der **render**-Methode in:

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

Öffnen Sie als Nächstes die Datei  **src/webparts/listItems/components/IListItemsProps.ts**, und ersetzen Sie ihren Inhalt durch Folgendes:

```ts
export interface IListItemsProps {
  listName: string;
}
```

Führen Sie den folgenden Befehl aus, um sicherzustellen, dass das Projekt ausgeführt wird:

```sh
gulp serve
```

Fügen Sie im Webbrowser das **Listenelement**-Webpart zum Zeichenbereich hinzu, und öffnen Sie die Eigenschaften. Überprüfen Sie, dass der für die **List**-Eigenschaft festgelegte Wert im Webparttext angezeigt wird.

![Webpart, in dem der Wert der listName-Eigenschaft angezeigt wird](../../../images/custom-property-pane-control-web-part-first-run.png)

## <a name="create-asynchronous-dropdown-property-pane-control"></a>Erstellen eines asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich

Das SharePoint Framework bietet Ihnen ein standardmäßiges Dropdown-Steuerelement, mit dem Benutzer einen bestimmten Wert auswählen können. Das Dropdown-Steuerelement wurde so konzipiert, dass all seine Werte vorab bekannt sein müssen. Wenn die Werte dynamisch geladen werden sollen oder Sie die Werte asynchron aus einem externen Dienst laden und nicht das ganze Webpart blockieren möchten, besteht eine Möglichkeit darin, ein Dropdown-Steuerelement zu erstellen.

Wenn Sie ein benutzerdefiniertes Eigenschaftenbereichssteuerelement erstellen, das React im SharePoint Framework verwendet, besteht das Steuerelement aus einer Klasse, die das Steuerelement bei dem Webpart registriert, und einer React-Komponente, die das Dropdown rendert und seine Daten verwaltet.

> **Hinweis:** Ab Drop 6 des SharePoint Frameworks gibt es einen Fehler in der React-Dropdownkomponente der Office UI Fabric, der dazu führt, dass das in diesem Artikel erstellte Steuerelement nicht ordnungsgemäß funktioniert. Eine temporäre Problemumgehung besteht darin, die Datei **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** zu bearbeiten und die Zeile **12027** von:
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> in:
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

### <a name="add-asynchronous-dropdown-property-pane-control-react-component"></a>Hinzufügen eines asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich einer React-Komponente

#### <a name="create-components-folder"></a>Erstellen eines Komponentenordners

Erstellen Sie im Ordner **src** eine Hierarchie aus drei neuen Ordnern, damit Ihre Ordnerstruktur als **src/controls/PropertyPaneAsyncDropdown/components** angezeigt wird.

![Komponentenordner in Visual Studio Code hervorgehoben](../../../images/custom-property-pane-control-components-folder.png)

#### <a name="define-asynchronous-dropdown-react-component-properties"></a>Definieren von Eigenschaften asynchroner Dropdown-React-Komponenten

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **IAsyncDropdownProps.ts**, und geben Sie den folgenden Code ein:

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

Die **IAsyncDropdownProps**-Klasse definiert Eigenschaften, die für die React-Komponente festgelegt werden können, die vom benutzerdefinierten Eigenschaftenbereichssteuerelement verwendet werden. Die **label**-Eigenschaft gibt die Bezeichnung für das Dropdown-Steuerelement an. Die der **loadOptions**-Stellvertretung zugeordnete Funktion wird vom Steuerelement aufgerufen, um die verfügbaren Optionen zu laden. Die der **onChanged**-Stellvertretung zugeordnete Funktion wird aufgerufen, nachdem der Benutzer eine Option in der Dropdownliste ausgewählt hat. Die **selectedKey**-Eigenschaft gibt den ausgewählten Wert an, der eine Zeichenfolge oder eine Zahl sein kann. Die **disabled**-Eigenschaft gibt an, ob das Dropdown-Steuerelement deaktiviert ist oder nicht. Die **stateKey**-Eigenschaft wird verwendet, um zu erzwingen, dass die React-Komponente erneut gerendert wird.

#### <a name="define-asynchronous-dropdown-react-component-interface"></a>Definieren der asynchronen Dropdown-React-Komponentenschnittstelle

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **IAsyncDropdownState.ts**, und geben Sie den folgenden Code ein:

```ts
import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

export interface IAsyncDropdownState {
  loading: boolean;
  options: IDropdownOption[];
  error: string;
}
```

Die **IAsyncDropdownState**-Schnittstelle beschreibt den Status der React-Komponente. Die **loading**-Eigenschaft bestimmt, ob die Komponente ihre Optionen in dem bestimmten Moment lädt. Die **options**-Eigenschaft enthält alle verfügbare Optionen. Wenn ein Fehler aufgetreten ist, wird dieser der **error**-Eigenschaft zugewiesen, von wo aus er dem Benutzer mitgeteilt wird.

#### <a name="define-the-asynchronous-dropdown-react-component"></a>Definieren der asynchronen Dropdown-React-Komponente

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **AsyncDropdown.tsx**, und geben Sie den folgenden Code ein:

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

Die **AsyncDropdown**-Klasse stellt die React-Komponente dar, die zum Rendern des asynchronen Dropdown-Eigenschaftenbereichssteuerelements verwendet wird. Wenn die Komponente das erste Mal geladen wird, ändert sich die **componentDidMount**-Methode bzw. ihre  **disabled**- oder **stateKey**-Eigenschaft, und die verfügbaren Optionen werden durch Aufrufen der **loadOptions**-Methode geladen, die über die Eigenschaften übergeben wird. Nachdem die Optionen geladen wurden, wird der Status der Komponente aktualisiert, und die verfügbaren Optionen werden angezeigt. Die Dropdownliste selbst wird mithilfe der [React-Dropdownkomponente der Office UI Fabric](http://dev.office.com/fabric#/components/dropdown) gerendert. Wenn die Komponente die verfügbaren Optionen lädt, wird ein Drehfeld mithilfe der [React-Drehfeldkomponente der Office UI Fabric](http://dev.office.com/fabric#/components/spinner) angezeigt.

### <a name="add-asynchronous-dropdown-property-pane-control"></a>Hinzufügen eines asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich

Der nächste Schritt besteht darin, das benutzerdefinierte Eigenschaftenbereichssteuerelement zu definieren. Dieses Steuerelement wird beim Definieren von Eigenschaften im Eigenschaftenbereich innerhalb des Webparts verwendet und wird mithilfe der zuvor definierten React-Komponente gerendert.

#### <a name="define-asynchronous-dropdown-property-pane-control-properties"></a>Definieren der Eigenschaften eines asynchronen Eigenschaftenbereichsteuerelements

Ein benutzerdefiniertes Eigenschaftenbereichsteuerelement weist zwei Eigenschaftssätze auf. Der erste Satz von Eigenschaften wird öffentlich verfügbar gemacht und wird zum Definieren der Webparteigenschaft innerhalb des Webparts verwendet. Diese Eigenschaften sind komponentenspezifische Eigenschaften, z. B. die Bezeichnung, die neben dem Steuerelement angezeigt wird, minimale und maximale Werte für ein Drehfeld oder verfügbare Optionen für eine Dropdownliste. Wenn Sie ein benutzerdefiniertes Eigenschaftenbereichssteuerelement definieren, muss der Typ, der diese Eigenschaften beschreibt, als **TProperties**-Typ übergeben werden, wenn die **IPropertyPaneField<TProperties> **-Schnittstelle implementiert wird.

Bei dem zweiten Satz von Eigenschaften handelt es sich um private Eigenschaften, die intern innerhalb des benutzerdefinierten Eigenschaftenbereichssteuerelements verwendet werden. Diese Eigenschaften müssen den SharePoint Framework-APIs entsprechen, damit das benutzerdefinierte Steuerelement korrekt gerendert wird. Diese Eigenschaften müssen die **IPropertyPaneCustomFieldProps**-Schnittstelle aus dem **@microsoft/sp-webpart-base**-Paket implementieren.

##### <a name="define-the-public-properties-for-the-asynchronous-dropdown-property-pane-control"></a>Definieren der öffentlichen Eigenschaften für das asynchrone Dropdown-Eigenschaftenbereichsteuerelement 

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown/components** eine neue Datei mit dem Namen **IPropertyPaneAsyncDropdownProps.ts**, und geben Sie den folgenden Code ein:

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

Die **label**-Eigenschaft definiert die Bezeichnung, die neben der Dropdownliste angezeigt wird. Die **loadOptions**-Stellvertretung definiert die Methode, die zum Laden der verfügbaren Dropdownoptionen aufgerufen wird. Die **onPropertyChange**-Stellvertretung definiert eine Methode, die aufgerufen wird, wenn der Benutzer einen Wert in der Dropdownliste auswählt. Die **selectedKey**-Eigenschaft gibt den ausgewählten Dropdownwert zurück. Die **disabled**-Eigenschaft gibt an, ob das Steuerelement deaktiviert ist oder nicht.

##### <a name="define-the-internal-properties-for-the-asynchronous-dropdown-property-pane-control"></a>Definieren der internen Eigenschaften für das asynchrone Dropdown-Eigenschaftenbereichsteuerelement 

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown** eine neue Datei mit dem Namen **IPropertyPaneAsyncDropdownInternalProps.ts**, und geben Sie den folgenden Code ein:

```ts
import { IPropertyPaneCustomFieldProps } from '@microsoft/sp-webpart-base';
import { IPropertyPaneAsyncDropdownProps } from './IPropertyPaneAsyncDropdownProps';

export interface IPropertyPaneAsyncDropdownInternalProps extends IPropertyPaneAsyncDropdownProps, IPropertyPaneCustomFieldProps {
}
```

Die **IPropertyPaneAsyncDropdownInternalProps**-Schnittstelle definiert zwar keine neuen Eigenschaften, sie kombiniert aber die Eigenschaften aus der zuvor definierten **IPropertyPaneAsyncDropdownProps**-Schnittstelle und der standardmäßigen **IPropertyPaneCustomFieldProps**-Schnittstelle von SharePoint Framework, die erforderlich ist, damit ein benutzerdefiniertes Steuerelement korrekt ausgeführt wird.

#### <a name="define-the-asynchronous-dropdown-property-pane-control"></a>Definieren des asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich

Erstellen Sie im Ordner **src/controls/PropertyPaneAsyncDropdown** eine neue Datei mit dem Namen **PropertyPaneAsyncDropdown.ts**, und geben Sie den folgenden Code ein:

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

Die **PropertyPaneAsyncDropdown**-Klasse implementiert die standardmäßige **IPropertyPaneField**-Schnittstelle von SharePoint Framework mithilfe der **IPropertyPaneAsyncDropdownProps**-Schnittstelle als Vertrag für die öffentlichen Eigenschaften, die innerhalb des Webparts festgelegt werden können. Die Klasse enthält die folgenden drei öffentlichen Eigenschaften, die von der **IPropertyPaneField**-Schnittstelle definiert werden:

- **type**: Muss auf **PropertyPaneFieldType.Custom** für ein benutzerdefiniertes Eigenschaftenbereichssteuerelement festgelegt sein.
- **targetProperty**: Wird zum Angeben des Namens der Webparteigenschaft verwendet, die mit dem Steuerelement verwendet werden soll.
- **properties**: Wird zum Definieren von steuerelementspezifischen Eigenschaften verwendet.

Beachten Sie, dass die **properties**-Eigenschaften den internen Typ **IPropertyPaneAsyncDropdownInternalProps** und nicht die öffentliche **IPropertyPaneAsyncDropdownProps**-Schnittstelle aufweist, die von der Klasse implementiert wird. Dies ist Absicht, damit die **properties**-Eigenschaft die **onRender**-Methode definieren kann, die für das SharePoint Framework erforderlich ist. Wenn die **onRender**-Methode Teil der öffentlichen **IPropertyPaneAsyncDropdownProps**-Schnittstelle war, müssten Sie bei Verwendung des asynchronen Dropdownsteuerelement im Webpart war, müssten Sie dieser einen Wert innerhalb des Webparts zuweisen, was nicht erstrebenswert ist.

Die **PropertyPaneAsyncDropdown**-Klasse definiert eine öffentliche **render**-Methode, die zum Aktualisieren des Steuerelements verwendet werden kann. Dies ist in Situationen hilfreich, wenn Sie zum Beispiel über verkettete Dropdowns verfügen, in denen der in einem Dropdown festgelegte Wert die im anderen Dropdown verfügbaren Optionen bestimmt. Durch Aufrufen der **render**-Methode nach dem Auswählen eines Elements können die verfügbaren Optionen vom abhängigen Dropdown geladen werden. Hierfür muss React erkennen, dass sich das Steuerelement geändert hat. Dies erfolgt durch Festlegen des Werts von **stateKey** auf das aktuelle Datum. Mithilfe dieses Tricks wird bei jedem Aufruf der **onRender**-Methode die Komponente nicht nur erneut gerendert, sondern es werden auch ihre verfügbaren Optionen aktualisiert.

## <a name="use-the-asynchronous-dropdown-property-pane-control-in-the-web-part"></a>Verwenden des asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich im Webpart

Wenn das asynchrone Dropdown-Eigenschaftenbereichssteuerelement bereit ist, besteht der nächste Schritt darin, dieses innerhalb des Webparts zu verwenden, damit Benutzer eine Liste auswählen können.

### <a name="add-list-info-interface"></a>Hinzufügen einer listinfo-Schnittstelle

Um Informationen zu verfügbaren Listen auf konsistente Art und Weise zu übergeben, definieren Sie eine Schnittstelle, die Informationen zu einer Liste darstellt. Erstellen Sie im Ordner **src/Webparts/ListItems** eine neue Datei mit dem Namen **IListInfo.ts** , und geben Sie den folgenden Code ein:

```ts
export interface IListInfo {
  Id: string;
  Title: string;
}
```

### <a name="use-the-asynchronous-dropdown-property-pane-control-to-render-the-listname-web-part-property"></a>Verwenden des asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich zum Rendern der listName-Webparteigenschaft

#### <a name="reference-required-types"></a>Erforderliche Verweistypen

Importieren Sie oberen Teil der **src/webparts/listItems/ListItemsWebPart.ts**-Datei die zuvor erstellte **PropertyPaneAsyncDropdown**-Klasse, indem Sie Folgendes hinzufügen:

```ts
import { PropertyPaneAsyncDropdown } from '../../controls/PropertyPaneAsyncDropdown/PropertyPaneAsyncDropdown';
```

Fügen Sie dann nach dem Code einen Verweis auf die **IDropdownOption**-Schnittstelle und zwei Hilfsfunktionen hinzu, die für die Arbeit mit Webparteigenschaften erforderlich sind.

```ts
import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
import { update, get } from '@microsoft/sp-lodash-subset';
```

![Verweise auf die hervorgehobene Klasse 'PropertyPaneAsyncDropdown' und die Schnittstelle 'IDropdownOption in Visual Studio Code](../../../images/custom-property-pane-control-web-part-imports.png)

#### <a name="add-method-to-load-available-lists"></a>Hinzufügen einer Methode zum Laden von verfügbaren Listen

Fügen Sie in der **ListItemsWebPart**-Klasse eine Methode zum Laden der verfügbaren Listen hinzu. In diesem Artikel verwenden Sie simulierte Daten, Sie können aber auch die SharePoint-REST-API aufrufen, um die Liste verfügbarer Listen aus dem aktuellen Web abzurufen. Um Ladeoptionen aus einem externen Dienst zu simulieren, verwendet die Methode eine Verzögerung von zwei Sekunden.

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

#### <a name="add-method-to-handle-the-change-of-the-value-in-the-dropdown"></a>Hinzufügen einer Methode zum Behandeln der Änderung der Werts in der Dropdownliste

Fügen Sie in der **ListItemsWebPart**-Klasse eine neue Methode mit dem Namen**onListChange** hinzu.

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

Nach dem Auswählen einer Liste im Listendropdown sollte der ausgewählte Wert in Webparteigenschaften beibehalten werden, und das Webpart sollte erneut gerendert werden, um die ausgewählte Eigenschaft widerzuspiegeln.

#### <a name="render-the-list-web-part-property-using-the-asynchronous-dropdown-property-pane-control"></a>Rendern der list-Webparteigenschaft mithilfe des asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich

Ändern Sie in der **ListItemsWebPart**-Klasse die **getPropertyPaneConfiguration**-Methode, um das asynchrone Steuerelement für den Dropdown-Eigenschaftenbereich zum Rendern der **listName**-Webparteigenschaft zu verwenden.

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

An diesem Punkt sollten Sie in der Lage sein, eine Liste mithilfe des neu erstellten asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich auszuwählen. Um zu bestätigen, dass das Steuerelement wie erwartet funktioniert, öffnen Sie die Befehlszeile und führen Folgendes aus:

```sh
gulp serve
```

![Asynchrones Steuerelement für den Dropdown-Eigenschaftenbereich beim Laden der Optionen, ohne die Webpart-Benutzeroberfläche zu blockieren](../../../images/custom-property-pane-control-loading-options.png)

![Auswählen einer der Optionen im asynchronen Steuerelement für den Dropdown-Eigenschaftenbereich](../../../images/custom-property-pane-control-selecting-option.png)

## <a name="implement-cascading-dropdowns-using-the-asynchronous-dropdown-property-pane-control"></a>Implementieren verketteter Dropdownmenüs mithilfe des asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich

Beim Erstellen von SharePoint Framework-Webparts müssen Sie möglicherweise eine Konfiguration implementieren, bei der verfügbare Optionen von einer anderen zuvor ausgewählten Option abhängig sind. Ein typisches Beispiel besteht darin, Benutzer zuerst eine Liste und dann ein Listenelement aus dieser Liste auswählen zu lassen. Die Liste der verfügbaren Element wäre von der ausgewählten Liste abhängig. Hier erfahren Sie, wie ein solches Szenario mithilfe des in vorherigen Schritten implementierten asynchronen Steuerelements für den Dropdown-Eigenschaftenbereich implementiert wird.

### <a name="add-item-web-part-property"></a>Hinzufügen der item-Webparteigenschaft

Öffnen Sie im Code-Editor die Datei **src/webparts/listItems/ListItemsWebPart.manifest.json**. Fügen Sie im Abschnitt **properties** eine neue Eigenschaft mit dem Namen **item** hinzu, damit diese wie folgt angezeigt wird:

```ts
// ...
"properties": {
   "listName": "",
   "item": ""
}
// ...
```

![Webpartmanifest, bei dem die Webparteigenschaft 'item' markiert ist](../../../images/custom-property-pane-control-item-property-web-part-manifest.png)

Ändern Sie den Code in der Datei **src/webparts/listItems/IListItemsWebPartProps.ts** in Folgendes:

```ts
export interface IListItemsWebPartProps {
  listName: string;
  item: string;
}
```

Ändern Sie den Inhalt der Datei **src/webparts/listItems/components/IListItemsProps.ts** in Folgendes:

```ts
export interface IListItemsProps {
  listName: string;
  item: string;
}
```

Ändern Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** den Code der **render**-Methode in:

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

Ändern Sie in der Datei **src/webparts/listItems/loc/mystrings.d.ts** die **IListItemsWebPartStrings**-Schnittstelle in Folgendes:

```ts
declare interface IListItemsWebPartStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListFieldLabel: string;
  ItemFieldLabel: string;
}
```

Fügen Sie in der Datei **src/webparts/listItems/loc/en-us.js** die fehlende Definition für die Zeichenfolge **ItemFieldLabel** hinzu.

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

### <a name="render-the-value-of-the-item-web-part-property"></a>Rendern des Werts der item-Webparteigenschaft

Ändern Sie in der Datei **src/webparts/listItems/components/ListItems.tsx** die **render**-Methode in:

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

### <a name="add-method-to-load-list-items"></a>Hinzufügen einer Methode zum Laden von Listenelementen

Fügen Sie in der Datei **src/webparts/listItems/ListItemsWebPart.ts** in der **ListItemsWebPart**-Klasse eine neue Methode zum Laden der verfügbaren Listenelemente aus der ausgewählten Liste hinzu. Wie auch bei der Methode zum Laden der verfügbaren Listen verwenden Sie auch hier simulierte Daten.

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

In Abhängigkeit von der zuvor ausgewählten Liste gibt die **loadItems**-Methode simulierte Listenelemente zurück. Wenn keine Liste ausgewählt wurde, löst die Methode die Zusage ohne Daten.

### <a name="add-method-to-handle-the-selection-of-an-item"></a>Hinzufügen einer Methode zum Behandeln der Auswahl eines Elements

Fügen Sie in der **ListItemsWebPart**-Klasse eine neue Methode mit dem Namen**onListItemChange** hinzu.

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

Nach Auswahl eines Elements in der Element-Dropdownliste sollte das Webpart den neuen Wert in den Webparteigenschaften speichern und das Webpart erneut rendern, um die Änderungen in der Benutzeroberfläche widerzuspiegeln.

### <a name="render-the-item-web-part-property-in-the-property-pane"></a>Rendern der item-Webparteigenschaft im Eigenschaftenbereich

Fügen Sie in der **ListItemsWebPart**-Klasse eine neue Klasseneigenschaft mit dem Namen **itemsDropdown** hinzu.

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  private itemsDropDown: PropertyPaneAsyncDropdown;
  // ...
}
```

Ändern Sie als Nächstes den Code der Methode  **getPropertyPaneConfiguration** in:

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

Das Dropdownmenü für die item-Eigenschaft wird ähnlich wie die Dropdownliste für die listName-Eigenschaft initialisiert. Der einzige Unterschied besteht darin, dass eine Instanz des Steuerelements einer Klassenvariablen zugewiesen werden muss, da nach dem Auswählen einer Liste die Element-Dropdownliste aktualisiert werden muss.

### <a name="load-items-for-the-selected-list"></a>Laden von Elementen für die ausgewählte Liste

Wenn zu Beginn keine Liste ausgewählt ist, ist die Element-Dropdownliste deaktiviert und wird aktiviert, wenn der Benutzer eine Liste auswählt. Nachdem eine Liste ausgewählt wurde, werden aus dieser Liste auch Elemente geladen. Um diese Logik zu implementieren, erweitern Sie die zuvor definierte **onListChange**-Methode folgendermaßen:

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

Nach dem Auswählen einer Liste wird das ausgewählte Element zurückgesetzt, in den Webparteigenschaften beibehalten und in der Element-Dropdownliste zurückgesetzt. Die Dropdownliste zum Auswählen eines Elements wird aktiviert, und die Dropdownliste wird aktiviert, um ihre Optionen zu laden.

Führen Sie in der Befehlszeile Folgendes aus, um zu überprüfen, dass alles wie erwartet funktioniert:

```sh
gulp serve
```

Nachdem Sie das Webpart das erste Mal zu der Seite hinzugefügt und seinen Eigenschaftenbereich geöffnet haben, sollten Sie beide Dropdownlisten deaktiviert und beim Laden ihrer Optionen sehen.

![Dropdownmenüs im Webpart-Eigenschaftbereich beim Laden der Daten](../../../images/custom-property-pane-control-cascading-loading-lists.png)

Nachdem die Optionen geladen wurden, wird die Dropdownliste aktiviert. Da noch keine Liste ausgewählt wurde, bleibt die Dropdownliste deaktiviert.

![Aktivierte Dropdownliste im Webpart-Eigenschaftenbereich. Deaktivierte Element-Dropdownliste](../../../images/custom-property-pane-control-cascading-lists-loaded-items-disabled.png)

Nach dem Auswählen einer Liste in der Dropdownliste werden die in dieser Liste verfügbaren Elemente geladen.

![Element-Dropdownliste, in der verfügbare Elemente nach dem Auswählen einer Liste im Listen-Dropdown geladen werden](../../../images/custom-property-pane-control-cascading-loading-items.png)

Nachdem die verfügbaren Elemente geladen wurden, wird die Element-Dropdownliste aktiviert.

![Auswählen eines Listenelements aus der Element-Dropdownliste im Webpart-Eigenschaftenbereich](../../../images/custom-property-pane-control-cascading-items-loaded-enabled.png)

Nach dem Auswählen eines Elements in der Element-Dropdownliste wird das Webpart aktualisiert und zeigt das ausgewählte Element im Text an.

![Ausgewählte Liste und gerendertes Element im Webpart](../../../images/custom-property-pane-control-cascading-selected-list-item.png)
