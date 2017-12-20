---
title: Verbinden mit SharePoint mithilfe des JavaScript-Objektmodells (JSOM)
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: fdd500431679e34298abd7ac55b3aa4af519e10e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="connect-to-sharepoint-using-the-javascript-object-model-jsom"></a>Verbinden mit SharePoint mithilfe des JavaScript-Objektmodells (JSOM)

In der Vergangenheit haben Sie vielleicht beim Erstellen von SharePoint-Anpassungen, das SharePoint JavaScript-Objektmodell (JSOM) zur Kommunikation mit SharePoint verwendet. Dies wird nicht mehr empfohlen (siehe **Empfehlungen** unten), es gibt jedoch nach wie vor gültige Anwendungsfälle, z. B. die Codemigration. Dieser Artikel veranschaulicht, wie SharePoint JSOM beim Erstellen von Lösungen auf dem SharePoint Framework verwendet wird.

> [!NOTE] 
> Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für das SharePoint-Framework einrichten](../../set-up-your-development-environment.md).

## <a name="create-a-new-project"></a>Erstellen eines neuen Projekts

Erstellen Sie in der Konsole einen neuen Ordnern für Ihr Projekt:

```sh
md react-sharepointlists
```

Wechseln Sie zum Projektordner:

```sh
cd react-sharepointlists
```

Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:

```sh
yo @microsoft/sharepoint
```

Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:

- **react-sharepointlists** als Lösungsname.
- Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.
- **Verwenden Sie den aktuellen Ordner** als Speicherort für die Dateien.
- **React** als Ausgangs-Framework für die Webpart-Erstellung.
- **SharePoint-Listen** als Webpartname.
- **Zeigt die Namen von Listen auf der aktuellen Website an** als Webpartbeschreibung.

![Der SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../images/tutorial-spjsom-yo-sharepoint.png)

Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

```sh
npm shrinkwrap
```

Öffnen Sie dann den Projektordner im Code-Editor. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.

![Das SharePoint Framework-Projekt in Visual Studio-Code](../../../images/tutorial-spjsom-vscode.png)

Gehen Sie folgendermaßen vor, um das Verzeichnis in Visual Studio-Code vom Konsolentyp aus zu öffnen:
```sh
code .
```

## <a name="referencing-jsom"></a>Verweisen auf JSOM
Um SharePoint JSOM in Ihrer SharePoint Framework-Komponente verwenden zu können, müssen Sie zunächst darauf verweisen. In der Vergangenheit stand es bereits auf der Seite zu Ihrer Verfügung, um es aber in SharePoint-Framework zu verwenden, muss es explizit geladen werden.

Es gibt zwei Methoden, um in SharePoint Framework auf SharePoint JSOM zu verweisen: 
- **Deklarativ** – über die Konfiguration
- **Imperativ** – über Code

Jeder dieser Ansätze hat seine Vor- und Nachteile, die Sie unbedingt kennen sollten.

## <a name="reference-jsom-declaratively"></a>Deklaratives Referenzieren von JSOM

Der erste Schritt beim deklarativen Referenzieren von JSOM besteht darin, die SharePoint JSOM-API als externe Skripts in Ihrem SharePoint Framework-Projekt zu registrieren. Öffnen Sie im Code-Editor die Datei **./config/config.json**, und fügen Sie dem Abschnitt **externals** Folgendes hinzu:

```json
{
  // ...
  "externals": {
    "sp-init": {
      "path": "https://contoso.sharepoint.com/_layouts/15/init.js",
      "globalName": "$_global_init"
    },
    "microsoft-ajax": {
      "path": "https://contoso.sharepoint.com/_layouts/15/MicrosoftAjax.js",
      "globalName": "Sys",
      "globalDependencies": [
        "sp-init"
      ]
    },
    "sp-runtime": {
      "path": "https://contoso.sharepoint.com/_layouts/15/SP.Runtime.js",
      "globalName": "SP",
      "globalDependencies": [
        "microsoft-ajax"
      ]
    },
    "sharepoint": {
      "path": "https://contoso.sharepoint.com/_layouts/15/SP.js",
      "globalName": "SP",
      "globalDependencies": [
        "sp-runtime"
      ]
    }
  }
  // ...
}
```

Jeder Eintrag verweist auf unterschiedliche Skriptdateien, die Ihnen zusammen die Verwendung von SharePoint JSOM in Ihrer SPFx-Komponente ermöglichen. Alle diese Skripts werden als Nicht-Modul-Skripts verteilt. Daher erfordert jeder Registrierungseintrag eine URL (die mit der `path`-Eigenschaft angegeben wird) sowie einen vom Skript verwendeten Namen (der in der `globalName`-Eigenschaft angegeben ist). Um sicherzustellen, dass diese Skripts in der richtigen Reihenfolge geladen werden, werden die Abhängigkeiten zwischen diesen Skripts mit der `globalDependencies`-Eigenschaft angegeben.

In Abhängigkeit von der JSOM-Funktionalität, die Sie verwenden, müssen möglicherweise weitere Skripts hinzugefügt werden (z. B.sp.taxonomy.js).

### <a name="install-typescript-typings-for-sharepoint-jsom"></a>Installieren von TypeScript-Eingaben für SharePoint JSOM

Der nächste Schritt besteht darin, TypeScript-Eingaben für SharePoint JSOM zu installieren und zu konfigurieren. So profitieren Sie von den Sicherheitsfunktionen der TypeScript-Typen, wenn Sie mit SharePoint JSOM arbeiten.

Führen Sie den folgenden Befehl in Ihrem Projektverzeichnis von der Konsole aus:

```sh
npm install @types/microsoft-ajax @types/sharepoint --save-dev
```

Da SharePoint JSOM nicht als Modul verteilt ist und Sie es nicht direkt in Ihren Code importieren können, müssen Sie seine TypeScript-Eingaben global registrieren. Öffnen Sie im Code-Editor die Datei **./tsconfig.json**, und fügen Sie in der `types`-Eigenschaft, gleich hinter dem Eintrag **webpack-env** Verweise auf **microsoft-ajax** und **sharepoint** hinzu.

```json
{
  "compilerOptions": {
    // ...
    "types": [
      "es6-promise",
      "es6-collections",
      "webpack-env",
      "microsoft-ajax",
      "sharepoint"
    ]
  }
}
```

### <a name="reference-sharepoint-jsom-scripts-in-a-react-component"></a>Referenzieren von SharePoint JSOM-Skripts in einer React-Komponente

Um die SharePoint JSOM-Skripts in Ihrer SPFx-Komponente zu laden, müssen Sie im Code der Komponente darauf verweisen. In diesem Beispiel fügen Sie die Verweise in der React-Komponente hinzu, in der JSOM zur Kommunikation mit SharePoint verwendet wird.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Fügen nach der letzten `import`-Anweisung folgenden Code hinzu:

```ts
require('sp-init');
require('microsoft-ajax');
require('sp-runtime');
require('sharepoint');
```

Da diese Namen den zuvor hinzugefügten externen Verweisen entsprechen, wird SharePoint Framework dieses Skript unter den angegebenen URLs laden.

### <a name="show-titles-of-sharepoint-lists-in-the-current-site-using-jsom"></a>Anzeigen von Titeln von SharePoint-Listen auf der aktuellen Website mit JSOM

Zur Veranschaulichung, wie SharePoint JSOM zur Kommunikation mit SharePoint beiträgt, rufen Sie die Titel aller SharePoint-Listen ab, die sich auf der aktuellen Website befinden, und geben Sie sie wieder.

#### <a name="add-siteurl-to-the-react-components-properties"></a>Hinzufügen von _siteUrl_ zu Komponenteneigenschaften

Damit Sie sich mit SharePoint verbunden können, muss die React-Komponente die URL der aktuellen Website kennen. Die URL ist im übergeordneten Webpart verfügbar und kann über ihre Eigenschaften an die Komponente übergeben werden.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** und fügen Sie der Schnittstelle `ISharePointListsProps` die `siteUrl`-Eigenschaft hinzu:

```ts
export interface ISharePointListsProps {
  description: string;
  siteUrl: string;
}
```

Um die URL der aktuellen Website an die Komponente zu übergeben, öffnen Sie die Datei **./src/webparts/sharePointLists/SharePointListsWebPart.ts** im Code-Editor, und ändern Sie die `render`-Methode in:

```ts
export default class SharePointListsWebPart extends BaseClientSideWebPart<ISharePointListsWebPartProps> {
  public render(): void {
    const element: React.ReactElement<ISharePointListsProps > = React.createElement(
      SharePointLists,
      {
        description: this.properties.description,
        siteUrl: this.context.pageContext.web.absoluteUrl
      }
    );

    ReactDom.render(element, this.domElement);
  }

  // ...
}
```

#### <a name="define-the-react-components-state"></a>Definieren des Status der React-Komponente

Die React-Komponente lädt Daten aus SharePoint, um sie für den Benutzer wiederzugeben. Der aktuelle Status der React-Komponente wird mit einer state-Schnittstelle modelliert, die wir hinzufügen.

Erstellen Sie im Code-Editor im Ordner **./src/webparts/sharePointLists/components** eine neue Daten namens **ISharePointListsState.ts**, und fügen Sie folgenden Inhalt ein:

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
}
```

#### <a name="add-state-to-the-react-component"></a>Hinzufügen des Status zur React-Komponente

Nachdem Sie die Schnittstelle definiert haben, indem Sie die Form des Komponentenstatus beschrieben haben, muss die React-Komponente als Nächstes die state-Schnittstelle verwenden.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Fügen Sie unter den vorhandenen `import`-Anweisungen Folgendes hinzu:

```ts
import { ISharePointListsState } from './ISharePointListsState';
```

Im nächsten Schritt ändern Sie die Signatur der `SharePointLists`-Klasse in:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
}
```

Fügen Sie in der `SharePointLists`-Klasse einen Konstruktor mit dem Standardstatuswert hinzu:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null
    };
  }

  // ...
}
```

#### <a name="load-information-about-sharepoint-lists-from-the-current-site-using-jsom"></a>Laden von Informationen zu SharePoint-Listen von der aktuellen Website mit JSOM

Das clientseitige Webpart, das in diesem Artikel als Beispiel verwendet wurde, lädt per Klick Informationen zu SharePoint-Listen in die aktuelle Website.

![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Fügen Sie in der `SharePointLists`-Klasse eine neue Methode namens `getListsTitles` hinzu:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null
    };

    this.getListsTitles = this.getListsTitles.bind(this);
  }

  // ...

  private getListsTitles(): void {
  }
}
```

Um die richtigen Bereichsdefinition der Methode sicherzustellen, binden wir sie im Konstruktor an das Webpart.

Verwenden Sie in der `getListsTitles`-Methode SharePoint JSOM, um die Titel der SharePoint-Listen auf die aktuelle Website zu laden:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  private getListsTitles(): void {
    this.setState({
      loadingLists: true,
      listTitles: [],
      error: null
    });

    const context: SP.ClientContext = new SP.ClientContext(this.props.siteUrl);
    const lists: SP.ListCollection = context.get_web().get_lists();
    context.load(lists, 'Include(Title)');
    context.executeQueryAsync((sender: any, args: SP.ClientRequestSucceededEventArgs): void => {
      const listEnumerator: IEnumerator<SP.List> = lists.getEnumerator();

      const titles: string[] = [];
      while (listEnumerator.moveNext()) {
        const list: SP.List = listEnumerator.get_current();
        titles.push(list.get_title());
      }

      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.listTitles = titles;
        prevState.loadingLists = false;
        return prevState;
      });
    }, (sender: any, args: SP.ClientRequestFailedEventArgs): void => {
      this.setState({
        loadingLists: false,
        listTitles: [],
        error: args.get_message()
      });
    });
  }
}
```

Setzen Sie zunächst den Status der Komponente zurück, um dem Benutzer mitzuteilen, dass die Komponente Informationen aus SharePoint laden wird. Verwenden Sie dann die URL der aktuellen Website, die der Komponente über ihre Eigenschaften übergeben wurde, um einen neuen SharePoint-Kontext zu instanziieren. Laden Sie Listen von der aktuellen Website mit SharePoint JSOM, und um die Leistungsanforderung zu optimieren, geben Sie an, dass nur die `Title`-Eigenschaft geladen werden soll. Im nächsten Schritt führen Sie die Abfrage durch Aufruf der `executeQueryAsync`-Methode und Übergabe zweier Rückruffunktionen aus. Nach Abschluss der Abfrage durchlaufen Sie die Sammlung der abgerufenen Listen, speichern deren Titel in einem Array und aktualisieren den Status der Komponente.

#### <a name="render-the-titles-of-sharepoint-lists-in-the-current-site"></a>Wiedergeben der Titel von SharePoint-Listen auf der aktuellen Website

Nachdem Sie die Titel von SharePoint-Listen in der aktuellen Website geladen haben, müssen Sie sie nur noch in der Komponente wiedergeben. Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**, und aktualisieren Sie die `render`-Methode:

```tsx
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.sharePointLists}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
              <a className={styles.button} onClick={this.getListsTitles} role="button">
                <span className={styles.label}>Get lists titles</span>
              </a><br />
              {this.state.loadingLists &&
                <span>Loading lists...</span>}
              {this.state.error &&
                <span>An error has occurred while loading lists: {this.state.error}</span>}
              {this.state.error === null && titles &&
                <ul>
                  {titles}
                </ul>}
            </div>
          </div>
        </div>
      </div>
    );
  }
  // ...
}
```

Jetzt sollten Sie Ihr Webpart der Seite hinzufügen und die Titel der SharePoint-Listen auf der aktuellen Website anzeigen können. Für eine Überprüfung, dass das Projekt korrekt funktioniert, führen Sie auf der Konsole den folgenden Befehl aus:

```sh
gulp serve --nobrowser
```

Da Sie SharePoint JSOM zur Kommunikation mit SharePoint verwenden, müssen Sie das Webpart mit der gehosteten SharePoint-Workbench-Version testen. (Deshalb wird der `--nobrowser`-Parameter angegeben, um zu verhindern, dass die lokale Workbench automatisch geladen wird).

![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

Das deklarative Referenzieren von SharePoint JSOM-Skripts als externe Skripts ist bequem, und Sie können so den Code übersichtlich halten. Ein Nachteil besteht aber darin, dass Sie absolute URLs zum Speicherort angeben müssen, aus dem SharePoint JSOM-Skripts geladen werden sollen. Wenn Sie für Entwicklung, Prüfung und Produktion separate SharePoint-Mandanten verwenden, wird zusätzliche Arbeit erforderlich, um die folgenden URLs für die verschiedenen Umgebungen entsprechend zu ändern. In solchen Fällen könnten Sie auch erwägen, mithilfe von [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader) imperativ auf JSOM zu verweisen, um die Skripts im Code der SPFx-Komponenten zu laden.

## <a name="reference-jsom-imperatively"></a>Imperatives Referenzieren von JSOM

Eine andere Möglichkeit zum Laden von JavaScript-Bibliotheken in SharePoint Framework-Projekt besteht darin, den `SPComponentLoader` zu verwenden. `SPComponentLoader` ist eine Dienstprogrammklasse, die mit dem SharePoint Framework bereitgestellt wird und Ihnen helfen soll, die Skripts und andere Ressourcen in die Komponenten zu laden. Ein Vorteil der Verwendung des `SPComponentLoader` gegenüber dem deklarativen Laden von Skripts ist, dass Sie serverrelative URLs verwenden können, die bequemer sind, wenn Sie mehrere SharePoint-Mandanten für die verschiedenen Phasen des Entwicklungsprozesses verwenden.

> Für diesen Teil des Lernprogramms passen wir den zuvor im Abschnitt zum deklarativen Referenzieren weiter oben erstellten Code an.

### <a name="declarative-reference-cleanup"></a>Bereinigung durch deklaratives Verweisen

Wenn Sie die Schritte in den Abschnitten weiter oben zum deklarativen Verweisen befolgt haben, müssen Sie diese Verweise entfernen.

Entfernen Sie zuerst vorhandene externe Skriptverweise. Öffnen Sie dazu im Code-Editor die Datei **config/config.json**, und entfernen Sie aus der **externals**-Eigenschaft alle Einträge:

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/config.2.0.schema.json",
  "version": "2.0",
  "bundles": {
    "share-point-lists-web-part": {
      "components": [
        {
          "entrypoint": "./lib/webparts/sharePointLists/SharePointListsWebPart.js",
          "manifest": "./src/webparts/sharePointLists/SharePointListsWebPart.manifest.json"
        }
      ]
    }
  },
  "externals": {},
  "localizedResources": {
    "SharePointListsWebPartStrings": "lib/webparts/sharePointLists/loc/{locale}.js"
  }
}
```

Wenn SharePoint JSOM-Skripts nicht mehr als externe Skripts registriert sind, können Sie nicht direkt im Code darauf verweisen.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx** und entfernen Sie die `require`-Anweisungen, die auf die verschiedenen SharePoint JSOM-Skripts verweisen.

### <a name="wait-to-load-data-until-the-jsom-scripts-are-loaded"></a>Warten Sie mit den Laden der Daten, bis die JSOM-Skripts geladen sind

Die Hauptfunktion des clientseitigen Webparts, das wir in diesem Lernprogramm erstellen, hängt von SharePoint JSOM ab. Je nach Anzahl der Faktoren kann das Laden der Skripts einige Zeit dauern, und wenn Sie SPFx-Komponenten erstellen, die JSOM verwenden, sollten Sie diese Verzögerung berücksichtigen. Wenn das Webpart einer Seite hinzugefügt worden ist, sollte es dem Benutzer mitteilen, dass es seine Voraussetzungen lädt, und melden, wann es einsatzbereit ist. Um dies zu unterstützen, erweitern Sie den Status der React-Komponente um eine zusätzliche Eigenschaft, damit Sie den Ladestatus der JSOM-Skripts verfolgen können.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/ISharePointListsState.ts**, und fügen Sie folgenden Code ein:

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
    loadingScripts: boolean;
}
```

Fügen Sie anschließend die neu hinzugefügte Eigenschaft zu den Statusdefinitionen in der React-Komponente hinzu. Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Aktualisieren Sie den Konstruktor auf den folgenden Code:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null,
      loadingScripts: true
    };

    this.getListsTitles = this.getListsTitles.bind(this);
  }
  // ...
}
```

Aktualisieren Sie in der gleichen Datei die `getListsTitles`-Methode auf den folgenden Code:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  private getListsTitles(): void {
    this.setState({
      loadingLists: true,
      listTitles: [],
      error: null,
      loadingScripts: false
    });

    const context: SP.ClientContext = new SP.ClientContext(this.props.siteUrl);
    const lists: SP.ListCollection = context.get_web().get_lists();
    context.load(lists, 'Include(Title)');
    context.executeQueryAsync((sender: any, args: SP.ClientRequestSucceededEventArgs): void => {
      const listEnumerator: IEnumerator<SP.List> = lists.getEnumerator();

      const titles: string[] = [];
      while (listEnumerator.moveNext()) {
        const list: SP.List = listEnumerator.get_current();
        titles.push(list.get_title());
      }

      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.listTitles = titles;
        prevState.loadingLists = false;
        return prevState;
      });
    }, (sender: any, args: SP.ClientRequestFailedEventArgs): void => {
      this.setState({
        loadingLists: false,
        listTitles: [],
        error: args.get_message(),
        loadingScripts: false
      });
    });
  }
}
```

Um dem Benutzer den Ladestatus der SharePoint JSOM-Skripts zu melden, aktualisieren Sie die `render`-Methode auf den folgenden Code:

```tsx
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.sharePointLists}>
        <div className={styles.container}>
          {this.state.loadingScripts &&
            <div className="ms-Grid" style={{ color: "#666", backgroundColor: "#f4f4f4", padding: "80px 0", alignItems: "center", boxAlign: "center" }}>
              <div className="ms-Grid-row" style={{ color: "#333" }}>
                <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
                <div className="ms-Grid-col ms-u-sm12 ms-u-md6" style={{ height: "100%", whiteSpace: "nowrap", textAlign: "center" }}>
                  <i className="ms-fontSize-su ms-Icon ms-Icon--CustomList" style={{ display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}></i><span className="ms-fontWeight-light ms-fontSize-xxl" style={{ paddingLeft: "20px", display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}>SharePoint lists</span>
                </div>
                <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
              </div>
              <div className="ms-Grid-row" style={{ width: "65%", verticalAlign: "middle", margin: "0 auto", textAlign: "center" }}>
                <span style={{ color: "#666", fontSize: "17px", display: "inline-block", margin: "24px 0", fontWeight: 100 }}>Loading SharePoint JSOM scripts...</span>
              </div>
              <div className="ms-Grid-row"></div>
            </div>}
          {this.state.loadingScripts === false &&
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
                <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
                <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
                <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
                <a className={styles.button} onClick={this.getListsTitles} role="button">
                  <span className={styles.label}>Get lists titles</span>
                </a><br />
                {this.state.loadingLists &&
                  <span>Loading lists...</span>}
                {this.state.error &&
                  <span>An error has occurred while loading lists: {this.state.error}</span>}
                {this.state.error === null && titles &&
                  <ul>
                    {titles}
                  </ul>}
              </div>
            </div>
          }
        </div>
      </div>
    );
  }
  // ...
}
```

Wenn die React-Komponente meldet, dass die SharePoint JSOM-Skripts geladen werden, zeigt sie einen Platzhalter an. Nachdem die Skripts geladen wurden, wird das Webpart den erwarteten Inhalt mit der Schaltfläche anzeigen, damit der Benutzer die Informationen zu SharePoint-Listen auf die aktuelle Website laden kann.

### <a name="load-sharepoint-jsom-scripts-using-spcomponentloader"></a>Laden von SharePoint JSOM-Skripts mit SPComponentLoader

SPFx-Komponenten sollten SharePoint JSOM-Skripts nur einmal laden. In diesem Beispiel – vorausgesetzt, das Webpart besteht aus einer einzigen React-Komponente – sollten Sie die SharePoint JSOM-Skripts am besten in der `componentDidMount`-Methode der React-Komponente laden, da diese Methode erst ausgeführt wird, wenn die Komponente instanziiert wurde.

Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Fügen Sie im oberen Bereich der Datei eine `import`-Anweisung hinzu, die auf `SPComponentLoader` verweist. Fügen Sie dann in der `SharePointLists`-Klasse die `componentDidMount`-Methode hinzu:

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';

export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public componentDidMount(): void {
    SPComponentLoader.loadScript('/_layouts/15/init.js', {
      globalExportsName: '$_global_init'
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/MicrosoftAjax.js', {
        globalExportsName: 'Sys'
      });
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/SP.Runtime.js', {
        globalExportsName: 'SP'
      });
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/SP.js', {
        globalExportsName: 'SP'
      });
    })
    .then((): void => {
      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.loadingScripts = false;
        return prevState;
      });
    });
  }
  // ...
}
```

Unter Verwendung einer Reihe von verketteten Zusagen laden Sie die verschiedenen Skripts, die zusammen die Verwendung von SharePoint JSOM in Ihrer SharePoint Framework-Komponente ermöglichen. Beachten Sie, wie Sie dank Verwendung des `SPComponentLoader` serverrelative URLs verwenden können, die Skripts aus dem aktuellen SharePoint-Mandanten laden. Nachdem alle Skripts geladen wurden, aktualisieren Sie den Status der React-Komponente, indem Sie bestätigen, dass alle Voraussetzungen geladen wurden und das Webpart einsatzbereit ist.

Bestätigen Sie, dass das Webpart wie erwartet funktioniert, indem Sie auf der Konsole den folgenden Befehl ausführen:

```sh
gulp serve --nobrowser
```

Wie zuvor sollte das Webpart die Titel der SharePoint-Listen auf der aktuellen Website anzeigen.

![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

Obwohl die Verwendung des `SPComponentLoader` einigen Aufwand erfordert, ermöglicht er Ihnen, serverrelative URLs zu verwenden, die in Szenarien nützlich sind, in denen Sie unterschiedliche Mandanten für Entwicklung, Prüfung und Produktion einsetzen.

## <a name="considerations"></a>Überlegungen

In der Vergangenheit haben Sie vielleicht beim Erstellen von clientseitigen Anpassungen auf SharePoint SharePoint JSOM zur Kommunikation mit SharePoint verwendet. Jetzt ist die empfohlene Vorgehensweise jedoch entweder die Verwendung der SharePoint REST-API (direkt oder über die [PnP JavaScript-Core-Bibliothek](https://github.com/SharePoint/PnP-JS-Core)).

Als SharePoint JSOM eingeführt wurde, stellte dies den ersten Schritt im Hinblick auf eine Unterstützung clientseitiger Lösungen auf SharePoint dar. Es wird jedoch nicht mehr aktiv verwaltet und bietet möglicherweise keinen Zugriff auf alle Funktionen, die über die REST-API verfügbar sind. Außerdem können Sie, unabhängig davon, ob Sie die SharePoint-REST-API direkt oder über die PnP JavaScript-Core-Bibliothek verwenden, Zusagen verwenden, die das Schreiben von asynchronem Code erheblich erleichtern (ein häufig auftretendes Problem bei der Verwendung von JSOM).

Es gibt zwar immer noch Fälle, in denen SharePoint JSOM Zugriff auf Daten und Methoden bietet, die noch nicht von der SharePoint-REST-API abgedeckt sind, wenn möglich sollte aber die REST-API verwendet werden.

Wenn Sie vorhandene Anpassungen haben, die SharePoint JSOM verwenden, und in Erwägung ziehen, diese zu SharePoint Framework zu migrieren, sollte dieser Artikel Ihnen die erforderlichen Informationen zur Verwendung von SharePoint JSOM in SharePoint Framework-Lösungen liefern. Langfristig sollten Sie jedoch die Art und Weise ändern, wie Sie mit SharePoint kommunizieren, entweder unter Verwendung der SharePoint-REST-API (direkt) oder über die PnP JavaScript-Core-Bibliothek.
