---
title: Machen Sie Ihr clientseitiges SharePoint-Webpart konfigurierbar
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 5b63efd205dc55cf741628ecf00bff44efb4c9d1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="make-your-sharepoint-client-side-web-part-configurable"></a>Machen Sie Ihr clientseitiges SharePoint-Webpart konfigurierbar

Im Eigenschaftenbereich können Endbenutzer das Webpart mit einer Reihe von Eigenschaften konfigurieren. Im Artikel [Erstellen Ihres ersten Webparts](../get-started/build-a-hello-world-web-part.md) wird beschrieben, wie der Eigenschaftenbereich in der **HelloWorldWebPart**-Klasse definiert ist. Die Eigenschaften des Eigenschaftenbereichs sind in**PropertyPaneSettings** definiert.

Die folgende Abbildung zeigt ein Beispiel für einen Eigenschaftenbereich in SharePoint.

![Beispiel für Eigenschaftenbereich](../../../images/property-pane-example.png)

Der Eigenschaftenbereich weist drei wichtige Metadaten auf:

* Seiten
* Kopfzeile
* Gruppen

Über Seiten haben Sie die Flexibilität, komplexe Interaktionen zu trennen diese auf einer oder mehreren Seiten zu platzieren. Seiten enthalten dann eine Kopfzeile und Gruppen.

Über Kopfzeilen können Sie den Titel des Eigenschaftenbereichs definieren, und über Gruppen können Sie die verschiedenen Abschnitte im Eigenschaftenbereich definieren, mit denen Sie Ihre Feldgruppen gruppieren. 

Eine Eigenschaftenbereich sollte eine Seite, einen optionalen Header und mindestens eine Gruppe enthalten.

Eigenschaftenfelder werden dann innerhalb einer Gruppe definiert. 

## <a name="using-the-property-pane"></a>Verwenden des Eigenschaftenbereichs

Im folgenden Codebeispiel wird der Eigenschaftenbereich in Ihrem Webpart initialisiert und konfiguriert. Sie setzen die Methode **getPropertyPaneConfiguration** außer Kraft und geben eine Auflistung der Eigenschaftbereichsseite(n) zurück.

```ts
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

* Schaltfläche
* Kontrollkästchen
* Auswahlgruppe
* Dropdown
* Horizontales Lineal
* Beschriftung
* Link
* Schieberegler
* Textfeld
* Mehrzeiliges Textfeld
* Umschaltfläche
* Benutzerdefiniert

Die Feldtypen sind in **sp-client-platform** als Module verfügbar. Bevor sie im Code verwendet werden können, müssen sie importiert werden:

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

Jede Feldtypmethode ist wie folgt definiert, wobei **PropertyPaneTextField** als Beispiel verwendet wird:

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

Wenn die Eigenschaften definiert sind, können Sie in Ihrem Webpart mit dem **this.properties.[Eigenschaftsname** darauf zugreifen. Details finden Sie unter [**Render**-Methode von **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part.md#web-part-render-method):

## <a name="handling-field-changes"></a>Behandeln von Feldänderungen

Der Eigenschaftenbereich besteht aus zwei Interaktionsmodi:

* Reaktiv
* Nicht reaktiv

Im reaktiven Modus wird bei jeder Änderung ein Änderungsereignis ausgelöst. Durch das reaktive Verhalten wird das Webpart automatisch mit den neuen Werten aktualisiert.

Der reaktive Modus ist zwar für viele Szenarien ausreichend, manchmal benötigen Sie aber das nicht reaktive Verhalten. Beim nicht reaktiven Verhalten wird das Webpart nicht automatisch aktualisiert, es sei denn, der Benutzer bestätigt die Änderungen. Fügen Sie Ihrem Webpart den folgenden Code hinzu, um den nicht reaktiven Modus zu aktivieren:

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a>Benutzerdefinierte Eigenschaftenbereich-Steuerelemente

SharePoint Framework enthält eine Reihe von Standardsteuerelementen für den Eigenschaftenbereich. Doch manchmal benötigen Sie zusätzliche Funktionen, die über die grundlegenden Steuerelemente hinausgehen. Mit SharePoint Framework können Sie benutzerdefinierte Steuerelemente erstellen, um die erforderliche Funktionalität bereitzustellen. Weitere Informationen finden Sie im Leitfaden zum [Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich](../guidance/build-custom-property-pane-controls.md).
