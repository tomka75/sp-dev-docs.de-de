---
title: "Vereinfachen des Hinzufügens von Webparts mit vorkonfigurierten Einträgen"
description: "Erfahren Sie, wie Sie Benutzern mithilfe vorkonfigurierter Einträge in Ihrem clientseitigen SharePoint-Framework-Webpart vorkonfigurierte Versionen des Webparts bereitstellen können."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 68ba1a0501a4a9154874ea15d01859369ab05577
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="simplify-adding-web-parts-with-preconfigured-entries"></a>Vereinfachen des Hinzufügens von Webparts mit vorkonfigurierten Einträgen

Komplexere clientseitige SharePoint-Framework-Webparts haben oft zahlreiche Eigenschaften, die von den Benutzern konfiguriert werden müssen. Sie können sie dabei unterstützen, indem Sie für bestimmte Szenarien vorkonfigurierte Eigenschafteneinträge hinzufügen. Ein vorkonfigurierter Eintrag initialisiert das Webpart mit vordefinierten Werten.

> [!NOTE] 
> Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für Ihr clientseitiges SharePoint-Webpart einrichten](../../set-up-your-development-environment.md).

## <a name="web-part-preconfigured-entries"></a>Vorkonfigurierte Einträge für Webparts

Jedes clientseitige SharePoint-Framework-Webpart besteht aus zwei Komponenten: 

- Dem Manifest, das das Webpart beschreibt
- Dem Webpartcode

Eine der im Webpartmanifest definierten Eigenschaften ist die Eigenschaft **preconfiguredEntries**.

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "6737645a-4443-4210-a70e-e5e2a219133a",
  "alias": "GalleryWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489", // Discover
    "group": { "default": "Under Development" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "Gallery"
    }
  }]
}
```

Die **preconfiguredEntries**-Eigenschaft enthält Informationen zu Ihrem Webpart zur Verwendung in der Webpart-Toolbox. Wenn Benutzer Webparts zu der Seite hinzufügen, werden die Informationen aus der **preconfiguredEntries**-Eigenschaft verwendet, um das Webpart in der Toolbox anzuzeigen und seine Standardeinstellungen zu definieren,wenn es zu der Seite hinzugefügt wird.

Wenn Sie bereits klassische Webparts mit voll vertrauenswürdigen Lösungen erstellt haben, können Sie sich jeden Eintrag im Array **preconfiguredEntries** wie eine Datei des Typs **.webpart** vorstellen. Ganz wie eine Datei des Typs **.webpart** ist jeder Eintrag in der Eigenschaft **preconfiguredEntries** mit dem Webpartcode verknüpft und definiert grundlegende Informationen zu dem Webpart, z. B. den Titel, die Beschreibung und Standardwerte für seine Eigenschaften.

### <a name="properties-of-a-preconfiguredentries-array-item"></a>Eigenschaften von Elementen im Array **preconfiguredEntries**

Jedes Element im **preconfiguredEntries**-Array umfasst mehrere Eigenschaften. In der folgenden Tabelle wird der Zweck jeder Eigenschaft erläutert.

|Eigenschaftsname |Werttyp |Erforderlich  |Zweck  |Beispielwert |
|:-------------|:----------|:--------:|:---------|:-------------|
|title         |ILocalizedString |ja |Der Webparttitel, der in der Toolbox angezeigt wird. |`"title": { "default": "Weather", "nl-nl": "Weerbericht" }`|
|description             |ILocalizedString|ja     |Die Webpartbeschreibung, die in den Toolbox-QuickInfos angezeigt wird.|`"description": { "default": "Shows weather in the given location", "nl-nl": "Toont weerbericht voor de opgegeven locatie" } `|
|officeFabricIconFontName|string          |nein      |Das Symbol für das Webpart, das in der Toolbox angezeigt wird. Der Wert für die Eigenschaft muss einer der [Office UI Fabric-Symbolnamen](https://dev.office.com/fabric#/styles/icons) sein. Ist für diese Eigenschaft ein Wert gesetzt, wird die Eigenschaft **iconImageUrl** ignoriert.|`"officeFabricIconFontName": "Sunny"`|
|iconImageUrl            |string          |nein      |Das Symbol für das Webpart, das in der Toolbox angezeigt wird. Es wird als Bild-URL angegeben. Das unter der URL abrufbare Bild muss genau 40 × 28 px groß sein. Für diese Eigenschaft muss ein Wert angegeben werden, wenn für die Eigenschaft **officeFabricIconName** kein Wert angegeben ist.|`"iconImageUrl": "https://cdn.contoso.com/weather.png"`|
|groupId                 |string          |Ja     |Die Gruppen-ID, die festlegt, in welcher modernen Gruppe auf einer modernen Website das Webpart enthalten sein soll. Das SharePoint-Framework reserviert Gruppen-IDs für [vordefinierte Gruppen](#predefined-modern-groups). Der Entwickler kann eine dieser Gruppen auswählen. Wenn der Entwickler eine ID angibt, die nicht zu den vordefinierten Gruppen gehört, wird automatisch die Gruppe **Sonstiges** gewählt.|`"groupId": "1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489"`|
|group                   |ILocalizedString|Nein      |Der Name der Gruppe in der Webpartauswahl einer klassischen Seite, in der das Webpart enthalten sein soll. Wird kein Wert angegeben, wird das Webpart in der Gruppe **Sonstiges** aufgeführt.|`"group": { "default": "Content", "nl-nl": "Inhoud" }`|
|dataVersion             |string          |Nein      |In diesem Feld können Sie die Datenversion der vorkonfigurierten Daten angeben, die dem Webpart bereitgestellt werden. Beachten Sie, dass sich die Datenversion vom Versionsfeld im Manifest unterscheidet. Die Manifestversion wird zum Steuern der Versionsverwaltung des Webpartcodes verwendet, die Datenversion hingegen zum Steuern der Versionsverwaltung der serialisierten Daten des Webparts. Weitere Informationen finden Sie in der Beschreibung des Felds „dataVersion“ für Webparts. Unterstütztes Format für Werte: HAUPTVERSION.NEBENVERSION.|`"dataVersion": "1.0"`|
|properties              |TProperties     |Ja     |Gibt ein Schlüssel-Wert-Paar-Objekt mit Standardwerten für Webparteigenschaften an.|`"properties": { "location": "Redmond", "numberOfDays": 3, "showIcon": true }`|

<br/>

Einige Webparteigenschaften weisen einen Wert vom Typ **ILocalizedString** auf. Dieser Typ ist ein Schlüssel-Wert-Paar-Objekt, mit dem Entwickler Zeichenfolgen für die unterschiedlichen Gebietsschemas angeben können. Ein Wert des Typs **ILocalizedString** muss mindestens den Wert **default** enthalten. 

Optional können Entwickler zusätzlich die Übersetzungen dieses Werts in die unterschiedlichen Gebietsschemas bereitstellen, die ihr Webpart unterstützt. Wenn das Webpart auf einer Seite in einem Gebietsschema platziert wird, das nicht in der lokalisierten Zeichenfolge aufgeführt ist, wird stattdessen der Standardwert verwendet.

Gültige Werte für **ILocalizedString**:

```json
"title": {
  "default": "Weather",
  "nl-nl": "Weerbericht"
}
```

```json
"title": {
  "default": "Weather"
}
```

<br/>

Ein Wert des Typs **ILocalizedString**, der ungültig ist, weil der Schlüssel **default** fehlt:

```json
"title": {
  "en-us": "Weather"
}
```

### <a name="predefined-modern-groups"></a>Vordefinierte moderne Gruppen

Wie in der Tabelle unten ersichtlich, gibt es 7 vordefinierte Gruppen. Die jeweilige Gruppen-ID wird in der Eigenschaft `groupId` angegeben.

| Name der Gruppe                      | ID                                     | Umfang der Gruppe |   
|---------------------------------|----------------------------------------|---------------|
| Text, Medien und Inhalt        | `cf066440-0614-43d6-98ae-0b31cf14c7c3` | Webparts, die Text, Multimediainhalte, Dokumente, Informationen aus dem Web und andere formatierte Inhalte anzeigen |
| Ermittlung                        | `1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489` | Webparts, die Inhalte organisieren, gruppieren und filtern, um Benutzern bei der Suche nach Informationen zu helfen                 |
| Kommunikation und Zusammenarbeit | `75e22ed5-fa14-4829-850a-c890608aca2d` | Webparts, die die Weitergabe von Informationen sowie die Teamarbeit und soziale Interaktionen vereinfachen                     |
| Planung und Durchführung            | `1bc7927e-4a5e-4520-b540-71305c79c20a` | Webparts, die Planungs- und Durchführungstools für höhere Teamproduktivität bereitstellen                   |
| Business und Intelligence       | `4aca9e90-eff5-4fa1-bac7-728f5f157b66` | Webparts für das Nachverfolgen und Analysieren von Daten sowie für die Integration von Geschäftsabläufen in Seiten               |
| Websitetools                      | `070951d7-94da-4db8-b06e-9d581f1f55b1` | Webparts mit Websiteinformationen und Tools zur Websiteverwaltung                                                         |
| Sonstiges                           | `5c03119e-3074-46fd-976b-c60198311f70` | Webparts, die in keine der anderen Gruppen passen                                                                         |

Gibt der Entwickler eine ID an, die nicht in dieser Liste aufgeführt ist, wird das Webpart automatisch der Gruppe **Sonstiges** zugeordnet.

Um anzuzeigen, wie Sie beim Erstellen von Webparts vorkonfigurierte Einträge verwenden können, erstellen Sie ein Beispiel-Katalog-Webpart. Benutzer können mithilfe mehrerer Eigenschaften dieses Webpart konfigurieren, um Elemente aus einer ausgewählten Liste auf eine bestimmte Weise anzuzeigen. Aus Platzgründen wird die eigentliche Implementierung der Webpartlogik ausgelassen, und Sie konzentrieren sich auf die Verwendung der **preconfiguredEntries**-Eigenschaft, um vorkonfigurierte Versionen des Katalog-Webparts bereitzustellen.

![Webpart-Eigenschaftenbereich mit den verschiedenen Eigenschaften, die Benutzer konfigurieren müssen, damit das Webpart funktioniert](../../../images/preconfiguredentries-needs-configuration.png)

## <a name="create-a-new-web-part-project"></a>Erstellen eines neuen Webpartprojekts

1. Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.

  ```sh
  md react-preconfiguredentries
  ```

2. Wechseln Sie zum Projektordner.

  ```sh
  cd react-preconfiguredentries
  ```

3. Führen Sie im Projektordner den SharePoint-Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint-Framework-Projekt zu erstellen:

  ```sh
  yo @microsoft/sharepoint
  ```

4. Es werden verschiedene Eingabeaufforderungen angezeigt. Geben Sie jeweils die folgenden Werte an:

  - **react-preconfiguredentries** als Lösungsname
  - **Aktuellen Ordner verwenden** als Speicherort für die Dateien
  - **Katalog** als Name des Webparts
  - **Zeigt Elemente aus der ausgewählten Liste an** als Beschreibung Ihres Webparts
  - **React** als Eintrittspunkt für die Webpart-Erstellung

  ![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/preconfiguredentries-yeoman.png)

5. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

  ```sh
  npm shrinkwrap
  ```

6. Öffnen Sie den Projektordner in einem Code-Editor. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch auch jeden beliebigen anderen Editor verwenden.

  ![SharePoint-Framework-Projekt in Visual Studio Code](../../../images/preconfiguredentries-visual-studio-code.png)

## <a name="add-web-part-properties"></a>Hinzufügen von Webparteigenschaften

Fügen Sie im Webpartmanifest Webparteigenschaften hinzu, damit Benutzer das Katalog-Webpart konfigurieren können. 

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. 

2. Ersetzen Sie den Abschnitt **properties** durch den folgenden JSON-Code:

  ```json
  {
    //...
    "preconfiguredEntries": [{
      //...
      "properties": {
        "listName": "",
        "order": "",
        "numberOfItems": 10,
        "style": ""
      }
    }]
  }
  ```

  Zu diesem Code ist Folgendes anzumerken:
  - Die Eigenschaft **listName** gibt den Namen der Liste an, deren Listenelemente angezeigt werden sollen. 
  - Die Eigenschaft **order** gibt die Reihenfolge an, in der Elemente angezeigt werden sollen, z. B. chronologisch oder umgekehrt chronologisch. 
  - Die Eigenschaft **numberOfItems** gibt an, wie viele Elemente angezeigt werden sollen. 
  - Die Eigenschaft **style** gibt an, wie die Elemente angezeigt werden sollen, ob z. B. als Miniaturansichten (geeignet zum Anzeigen von Bildern) oder als Liste (geeignet zum Anzeigen von Dokumenten).

  Im Manifest angegebene Webparteigenschaften müssen außerdem der Webparteigenschaften-Schnittstelle hinzugefügt werden. 
  
3. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/IGalleryWebPartProps.ts**. Ändern Sie deren Code in Folgendes:

  ```typescript
  export interface IGalleryWebPartProps {
    listName: string;
    order: string;
    numberOfItems: number;
    style: string;
  }
  ```

  Beim Erstellen von clientseitigen SharePoint-Framework-Webparts mithilfe von React müssen Sie nach dem Ändern der Webparteigenschaften-Schnittstelle die Methode **render** des Webparts aktualisieren. Sie verwendet diese Schnittstelle zur Erstellung einer Instanz der React-Hauptkomponente. 
  
4. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/galleryWebPart.ts**. Ändern Sie die Methode **render** des Webparts wie folgt:

  ```typescript
  export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IGalleryProps> = React.createElement(Gallery, {
        listName: this.properties.listName,
        order: this.properties.order,
        numberOfItems: this.properties.numberOfItems,
        style: this.properties.style
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

5. Aktualisieren Sie die React-Hauptkomponente so, dass die Werte der Eigenschaften angezeigt werden. Wenn das Webpart nicht konfiguriert wurde, soll der standardmäßige Webpart-Platzhalter angezeigt werden. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/components/Gallery.tsx**, und ändern Sie den in der Datei enthaltenen Code wie folgt:

  ```typescript
  import * as React from 'react';
  import styles from './Gallery.module.scss';
  import { IGalleryProps } from './IGalleryProps';

  export default class Gallery extends React.Component<IGalleryProps, void> {
    public render(): JSX.Element {
      if (this.needsConfiguration()) {
        return <div className="ms-Grid" style={{ color: "#666", backgroundColor: "#f4f4f4", padding: "80px 0", alignItems: "center", boxAlign: "center" }}>
          <div className="ms-Grid-row" style={{ color: "#333" }}>
            <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
            <div className="ms-Grid-col ms-u-sm12 ms-u-md6" style={{ height: "100%", whiteSpace: "nowrap", textAlign: "center" }}>
              <i className="ms-fontSize-su ms-Icon ms-Icon--ThumbnailView" style={{ display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}></i><span className="ms-fontWeight-light ms-fontSize-xxl" style={{ paddingLeft: "20px", display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}>Gallery</span>
            </div>
            <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
          </div>
          <div className="ms-Grid-row" style={{ width: "65%", verticalAlign: "middle", margin: "0 auto", textAlign: "center" }}>
            <span style={{ color: "#666", fontSize: "17px", display: "inline-block", margin: "24px 0", fontWeight: 100 }}>Show items from the selected list</span>
          </div>
          <div className="ms-Grid-row"></div>
        </div>;
      }
      else {
        return (
          <div className={styles.gallery}>
            <div className={styles.container}>
              <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
                <div className='ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1'>
                  <span className="ms-font-xl ms-fontColor-white">
                    Welcome to SharePoint!
                  </span>
                  <p className='ms-font-l ms-fontColor-white'>
                    Customize SharePoint experiences using Web Parts.
                  </p>
                  <p className='ms-font-l ms-fontColor-white'>
                    List: {this.props.listName}<br />
                    Order: {this.props.order}<br />
                    Number of items: {this.props.numberOfItems}<br />
                    Style: {this.props.style}
                  </p>
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

    private needsConfiguration(): boolean {
      return Gallery.isEmpty(this.props.listName) ||
        Gallery.isEmpty(this.props.order) ||
        Gallery.isEmpty(this.props.style);
    }

    private static isEmpty(value: string): boolean {
      return value === undefined ||
        value === null ||
        value.length === 0;
    }
  }
  ```

6. Aktualisieren Sie die Schnittstelle der React-Hauptkomponente so, dass sie der Webparteigenschaften-Schnittstelle entspricht. Dies ist notwendig, da sämtliche Webparteigenschaften an diese Komponente übergeben werden. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/components/IGalleryProps.ts**, und ändern Sie den in der Datei enthaltenen Code wie folgt:

  ```typescript
  import { IGalleryWebPartProps } from '../IGalleryWebPartProps';

  export interface IGalleryProps extends IGalleryWebPartProps {
  }
  ```

## <a name="render-web-part-properties-in-the-property-pane"></a>Rendern von Webparteigenschaften im Eigenschaftenbereich

Damit Benutzer die neu definierten Eigenschaft verwenden können, um das Webpart zu konfigurieren, müssen die Eigenschaften im Webparteigenschaftenbereich angezeigt werden. 

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/galleryWebPart.ts**. Ändern Sie im oberen Abschnitt der Datei die Importanweisung **@microsoft/sp-webpart-base** wie folgt:

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneDropdown,
    PropertyPaneSlider,
    PropertyPaneChoiceGroup
  } from '@microsoft/sp-webpart-base';
  ```

2. Ändern Sie **propertyPaneSettings** wie folgt:

  ```typescript
  export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
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
                    options: [{
                      key: 'Documents',
                      text: 'Documents'
                    },
                    {
                      key: 'Images',
                      text: 'Images'
                    }]
                  }),
                  PropertyPaneChoiceGroup('order', {
                    label: strings.OrderFieldLabel,
                    options: [{
                      key: 'chronological',
                      text: strings.OrderFieldChronologicalOptionLabel
                    },
                    {
                      key: 'reversed',
                      text: strings.OrderFieldReversedOptionLabel
                    }]
                  }),
                  PropertyPaneSlider('numberOfItems', {
                    label: strings.NumberOfItemsFieldLabel,
                    min: 1,
                    max: 10,
                    step: 1
                  }),
                  PropertyPaneChoiceGroup('style', {
                    label: strings.StyleFieldLabel,
                    options: [{
                      key: 'thumbnails',
                      text: strings.StyleFieldThumbnailsOptionLabel
                    },
                    {
                      key: 'list',
                      text: strings.StyleFieldListOptionLabel
                    }]
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

<br/>

In einem realen Szenario würden Sie die Liste der Listen von der aktuellen SharePoint-Website abrufen. Aus Platzgründen verwenden Sie in diesem Beispiel stattdessen eine Liste mit fixer Elementanzahl.

## <a name="add-localization-labels"></a>Hinzufügen von Lokalisierungsbezeichnungen

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/loc/mystrings.d.ts**. Ändern Sie den in der Datei enthaltenen Code wie folgt:

  ```typescript
  declare interface IGalleryStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
    OrderFieldLabel: string;
    OrderFieldChronologicalOptionLabel: string;
    OrderFieldReversedOptionLabel: string;
    NumberOfItemsFieldLabel: string;
    StyleFieldLabel: string;
    StyleFieldThumbnailsOptionLabel: string;
    StyleFieldListOptionLabel: string;
  }

  declare module 'galleryStrings' {
    const strings: IGalleryStrings;
    export = strings;
  }
  ```

2. Fügen Sie die fehlenden Ressourcenzeichenfolgen hinzu. Öffnen Sie dazu im Code-Editor die Datei **./src/webparts/gallery/loc/en-us.js**, und ändern Sie den in ihr enthaltenen Code wie folgt:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListNameFieldLabel": "List",
      "OrderFieldLabel": "Items order",
      "OrderFieldChronologicalOptionLabel": "chronological",
      "OrderFieldReversedOptionLabel": "reversed chronological",
      "NumberOfItemsFieldLabel": "Number of items to show",
      "StyleFieldLabel": "Items display style",
      "StyleFieldThumbnailsOptionLabel": "thumbnails",
      "StyleFieldListOptionLabel": "list"
    }
  });
  ```

3. Vergewissern Sie sich mithilfe des folgenden Befehls, dass das Projekt erstellt wird:

  ```sh
  gulp serve
  ```

4. Fügen Sie das Webpart im Webbrowser zur Canvas hinzu, und öffnen Sie den Eigenschaftenbereich des Webparts. Es sollten alle Eigenschaften angezeigt werden, die Benutzer konfigurieren können.

  ![Webpart-Eigenschaftenbereich mit den verschiedenen Eigenschaften, die Benutzer konfigurieren müssen, damit das Webpart funktioniert](../../../images/preconfiguredentries-needs-configuration.png)

Da Sie für das Webpart keine Standardwerte angegeben haben, müssen Benutzer das Webpart immer zuerst konfigurieren, wenn sie es der Seite hinzufügen. Sie können die Benutzererfahrung einfacher gestalten, indem Sie für die gängigsten Szenarien Standardwerte angeben.

## <a name="specify-default-values-for-the-web-part"></a>Angeben von Standardwerten für das Webpart

Nehmen wir an, Ihre Benutzer verwenden häufig das Katalog-Webpart, um die fünf zuletzt hinzugefügten Bilder anzuzeigen. Statt von den Benutzern zu verlangen, dass sie das Webpart jedes Mal manuell konfigurieren, könnten Sie ihnen eine vorkonfigurierte Version mit den korrekten Einstellungen bereitstellen.

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie den vorhandenen Eintrag in der Eigenschaft **preconfiguredEntries** wie folgt:

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    }]
  }
  ```

2. Starten Sie das Debuggen des Projekts, indem Sie den folgenden Befehl ausführen:

  ```sh
  gulp serve
  ```

  > [!NOTE] 
  > Falls das Debuggen bereits läuft: Stoppen Sie den Prozess, und starten Sie ihn erneut. Änderungen am Webpartmanifest werden beim Debuggen nicht automatisch in die Workbench übernommen. Sie müssen das Projekt neu erstellen, um sie sehen zu können.

3. Sobald Sie die Webpart-Toolbox öffnen, um das Webpart zur Canvas hinzuzufügen, werden Sie sehen, dass sich Name und Symbol geändert haben. Sie entsprechen nun den vorkonfigurierten Einstellungen.

  ![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-recent-images-toolbox.png)

4. Sobald das Webpart zur Seite hinzugefügt wird, funktioniert es unmittelbar und verwendet die vorkonfigurierten Einstellungen.

  ![Vorkonfiguriertes Webpart, das sofort funktioniert, wenn es der Seite hinzugefügt wird](../../../images/preconfiguredentries-recent-images-canvas.png)

## <a name="specify-multiple-preconfigured-web-part-entries"></a>Eingeben mehrerer vorkonfigurierter Webparteinträge

Stellen Sie sich vor, dass eine andere Gruppe von Benutzern häufig Ihr Katalog-Webpart verwendet, um Dokumente anzuzeigen, die kürzlich ihrer Website hinzugefügt wurden. Damit diese Ihr Webpart verwenden können, können Sie einen weiteren Satz von Voreinstellungen hinzufügen, die deren Konfigurationsanforderungen entsprechen.

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie die Eigenschaft **preconfiguredEntries** wie folgt:

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent documents" },
      "description": { "default": "Shows 10 most recent documents" },
      "officeFabricIconFontName": "Documentation",
      "properties": {
        "listName": "Documents",
        "order": "reversed",
        "numberOfItems": 10,
        "style": "list"
      }
    }]
  }
  ```

2. Wie Sie sehen, behalten Sie den bisherigen vorkonfigurierten Eintrag bei und fügen einen weiteren hinzu, mit anderen Werten für die Eigenschaften.

3. Starten Sie mit dem folgenden Befehl das Debuggen des Projekts, um das Ergebnis zu sehen:

  ```sh
  gulp serve
  ```

4. Sobald Sie die Webpart-Toolbox öffnen, um das Webpart der Canvas hinzuzufügen, werden zwei Webparts zur Auswahl angezeigt.

  ![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-multiple-web-parts-toolbox.png)

5. Das Webpart **Zuletzt verwendete Dokumente** funktioniert sofort, wenn es der Seite hinzugefügt wird, und arbeitet dabei mit den festgelegten vorkonfigurierten Einstellungen.

  ![Vorkonfiguriertes Webpart „Zuletzt verwendete Dokumente“, das sofort funktioniert, wenn es der Seite hinzugefügt wird](../../../images/preconfiguredentries-recent-documents-canvas.png)

## <a name="specify-an-unconfigured-instance-of-the-web-part"></a>Angeben einer nicht konfigurierten Instanz des Webparts

Beim Erstellen von Webparts gibt es häufig spezielle Szenarien, die das Webpart unterstützen soll. Das Bereitstellen vorkonfigurierter Einträge für diese Szenarien erleichtert Benutzern die Arbeit mit dem Webpart.

Je nachdem, wie Sie das Webpart erstellen, könnte es möglicherweise auch andere Szenarien unterstützen, die Sie nicht vorab eingeplant haben. Wenn Sie nur ganz bestimmte vorkonfigurierte Einträge bereitstellen, ist für Benutzer möglicherweise nicht klar, dass sie Ihr Webpart für ein anderes Szenario verwenden können. Es empfiehlt sich daher, auch eine allgemeine, nicht konfigurierte Variante des Webparts bereitzustellen.

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie die Eigenschaft **preconfiguredEntries** wie folgt:

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent documents" },
      "description": { "default": "Shows 10 most recent documents" },
      "officeFabricIconFontName": "Documentation",
      "properties": {
        "listName": "Documents",
        "order": "reversed",
        "numberOfItems": 10,
        "style": "list"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Gallery" },
      "description": { "default": "Shows items from the selected list" },
      "officeFabricIconFontName": "CustomList",
      "properties": {
        "listName": "",
        "order": "",
        "numberOfItems": 5,
        "style": ""
      }
    }]
  }
  ```

2. Wie Sie sehen, wird die allgemeine, nicht konfigurierte Version des Webparts zusätzlich zu den Konfigurationen hinzugefügt, die auf bestimmte Szenarien abzielen. Entspricht keine der vorab definierten Konfigurationen den Anforderungen der Benutzer, können sie jederzeit die allgemeine Version verwenden und entsprechend ihren Bedürfnissen konfigurieren.

3. Starten Sie mit dem folgenden Befehl das Debuggen des Projekts, um das Ergebnis zu sehen:

  ```sh
  gulp serve
  ```

4. Sobald Sie die Webpart-Toolbox öffnen, um das Webpart der Canvas hinzuzufügen, werden drei Webparts angezeigt, aus denen die Benutzer wählen können.

  ![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-three-configurations-toolbox.png)
