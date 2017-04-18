# <a name="integrate-your-sharepoint-client-side-web-part-with-the-property-pane"></a>Integrieren Ihres clientseitigen SharePoint-Webparts in den Eigenschaftenbereich

Im Eigenschaftenbereich können Endbenutzer das Webpart mit einer Reihe von Eigenschaften konfigurieren. Im Artikel [Erstellen Ihres ersten Webparts](../get-started/build-a-hello-world-web-part) wird beschrieben, wie der Eigenschaftenbereich in der **HelloWorldWebPart**-Klasse definiert ist. Die Eigenschaften des Eigenschaftenbereichs sind in**PropertyPaneSettings** definiert.

Die folgende Abbildung zeigt ein Beispiel für einen Eigenschaftenbereich in SharePoint.

![Beispiel für Eigenschaftenbereich](../../../../images/property-pane-example.png)

Der Eigenschaftenbereich weist drei wichtige Metadaten auf:

* Seiten
* Kopfzeile
* Gruppen

Über Seiten haben Sie die Flexibilität, komplexe Interaktionen zu trennen diese auf einer oder mehreren Seiten zu platzieren. Seiten enthalten dann eine Kopfzeile und Gruppen.

Über Kopfzeilen können Sie den Titel des Eigenschaftenbereichs definieren, und über Gruppen können Sie die verschiedenen Abschnitte im Eigenschaftenbereich definieren, mit denen Sie Ihre Feldgruppen gruppieren. 

Eine Eigenschaftenbereich sollte eine Seite, einen optionalen Header und mindestens eine Gruppe enthalten.

Eigenschaftenfelder werden dann innerhalb einer Gruppe definiert. 

## <a name="using-the-property-pane"></a>Verwenden der Eigenschaftenbereichs

Im folgenden Codebeispiel wird der Eigenschaftenbereich in Ihrem Webpart initialisiert und konfiguriert. Sie erstellen eine Methode des Typs **IPropertyPaneSettings** und geben eine Auflistung der Eigenschaftbereichsseite(n) zurück.

```ts
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
              PropertyPaneTextField('description', {
                label: strings.DescriptionFieldLabel
              })
            ]
          }
        ]
      }
    ]
  };
}
```

### <a name="property-pane-fields"></a>Felder des Eigenschaftenbereichs

Die folgenden Feldtypen werden unterstützt:

* Beschriftung
* Textfeld
* Mehrzeiliges Textfeld
* Kontrollkästchen
* Dropdown
* Link
* Schieberegler
* Umschaltfläche
* Benutzerdefiniert

Die Feldtypen sind in der **sp-clent-Plattform** als Module verfügbar. Bevor sie im Code verwendet werden können, müssen sie importiert werden:

```ts
import {
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneLabel,
  PropertyPaneLink,
  PropertyPaneSlider,
  PropertyPaneToggle,
  PropertyPaneDropdown
} from '@microsoft/sp-client-preview';
```

Jeder Feldtypkonstruktor ist wie folgt definiert, wobei **PropertyPaneTextField** als Beispiel verwendet wird:

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

**targetProperty** definiert das zugeordnete Objekt für diesen Feldtyp und ist auch in der Eigenschaftenschnittstelle Ihres Webparts definiert.

Um diesen Eigenschaften Typen zuzuordnen, definieren Sie eine Schnittstelle in Ihrer Webpartklasse, die eine oder mehrere Zieleigenschaften umfasst.

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

Diese steht dann in Ihrem Webpart über die **this.properties.targetProperty** zur Verfügung.

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

Wenn die Eigenschaften definiert sind, können Sie in Ihrem Webpart mit dem **this.properties.<Eigenschaftswert>** darauf zugreifen. Details finden Sie unter [**Render**-Methode von **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part#web-part-render-method):

## <a name="handling-field-changes"></a>Behandeln von Feldänderungen

Der Eigenschaftenbereich besteht aus zwei Interaktionsmodi:

* Reaktiv
* Nicht reaktiv

Im reaktiven Modus wird bei jeder Änderung ein change-Ereignis ausgelöst. Durch das reaktive Verhalten wird das Webpart automatisch mit den neuen Werten aktualisiert.

Der reaktive Modus ist zwar für viele Szenarios ausreichend, manchmal benötigen Sie aber das nicht reaktive Verhalten. Beim nicht reaktiven Verhalten wird das Webpart nicht automatisch aktualisiert, es sei denn, der Benutzer bestätigt die Änderungen.

## <a name="custom-field-example"></a>Beispiele für das benutzerdefinierte Feld

Fügen Sie die folgende Felddefinition zu einem **groupFields**-Array hinzu.

```ts
{
  type: IPropertyPaneFieldType.Custom,
  targetProperty: 'custom',
  properties: {
    onRender: this._customFieldRender.bind(this),
    value: undefined,
    context: undefined
  }
}
```

Fügen Sie die folgenden Typen zu den **@microsoft/sp-client-platform**-Importen hinzu.

```ts
IPropertyPaneFieldType,
IOnCustomPropertyFieldChanged
```

Fügen Sie die folgende private Methode zum Rendern des benutzerdefinierten Felds hinzu.

```ts
private _customFieldRender(elem: HTMLElement, context: any, onChanged?: IOnCustomPropertyFieldChanged): void {
    elem.innerHTML = '<input id="password" type="password" name="password" class="ms-TextField-field">';
}
```
