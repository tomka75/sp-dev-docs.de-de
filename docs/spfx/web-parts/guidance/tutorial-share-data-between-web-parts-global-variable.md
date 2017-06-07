# <a name="share-data-between-web-parts-using-a-global-variable-tutorial"></a>Gemeinsame Verwendung von Daten zwischen Webparts unter Verwendung einer globalen Variablen (Lernprogramm).

> Hinweis:  Dieser Artikel wurde noch nicht mit der SPFx-GA-Version überprüft, möglicherweise treten daher Probleme auf, wenn Sie versuchen, dies mit der neuesten Version durchzuführen.

Wenn Sie bei der Erstellung von clientseitigen Webparts Daten nur einmal laden und anschließend in den verschiedenen Webparts jeweils wiederverwenden, verbessert das die Leistung Ihrer Seiten und reduziert die Last in Ihrem Netzwerk. Dieses Lernprogramm veranschaulicht schrittweise, wie Daten zwischen Webparts unter Verwendung einer globalen Variablen freigegeben werden.

> **Hinweis:** Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für Ihr clientseitiges SharePoint-Webpart einrichten](../../set-up-your-development-environment).

## <a name="prepare-the-project"></a>Vorbereiten des Projekts

### <a name="create-a-new-project"></a>Erstellen eines neuen Projekts

Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.

```sh
md react-recentdocuments
```

Wechseln Sie zum Projektordner.

```sh
cd react-recentdocuments
```

Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen.

```sh
yo @microsoft/sharepoint
```

Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:

- **react-recentdocuments** als Name der Lösung.
- **Verwenden Sie den aktuellen Ordner** als Speicherort für die Dateien.
- **Zuletzt verwendete Dokumente** als Name des Webparts.
- **Zeigt kürzlich geänderte Dokumente** als Beschreibung Ihres Webparts.
- **React** als Startpunkt für die Webpart-Erstellung.

![Der SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../../images/tutorial-sharingdata-yo-sharepoint-recent-documents.png)

Öffnen Sie den Projektordner in Ihrem Code-Editor, sobald die Gerüsterstellung abgeschlossen ist. In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.

![Das SharePoint Framework-Projekt wird in Visual Studio Code geöffnet.](../../../../images/tutorial-sharingdata-vscode.png)

## <a name="show-the-recently-modified-documents"></a>Anzeigen der kürzlich geänderten Dokumente

Das Webpart „Zuletzt verwendete Dokumente“ zeigt Informationen zu den zuletzt geänderten Dokumenten an, die als Karten mithilfe von Office UI Fabric angezeigt werden.

![Das Webpart „Zuletzt verwendete Dokumente“ mit drei kleinen Dokumentkarten, die die drei zuletzt geänderten Dokumente darstellen](../../../../images/tutorial-sharingdata-recent-documents.png)

### <a name="remove-the-standard-description-property"></a>Entfernen der standardmäßigen _description_-Eigenschaft

Beginnen Sie, indem Sie die standardmäßige **description**-Eigenschaft aus der **IRecentDocumentsWebPartProps**-Schnittstelle entfernen. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts**, und fügen Sie den folgenden Code ein:

```ts
export interface IRecentDocumentsWebPartProps {
}
```

Entfernen Sie die standardmäßige **description**-Eigenschaft aus dem Webpartmanifest. Öffnen Sie die Datei ./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json, und entfernen Sie die **description**-Eigenschaft aus der **properties**-Eigenschaft:

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "7a7e3aa9-5d8a-4155-936b-0b0e06e9ca11",
  "alias": "RecentDocumentsWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "7a7e3aa9-5d8a-4155-936b-0b0e06e9ca11",
    "group": { "default": "Under Development" },
    "title": { "default": "Recent documents" },
    "description": { "default": "Shows recently modified documents" },
    "officeFabricIconFontName": "Page",
    "properties": {
    }
  }]
}
```

Entfernen Sie schließlich die standardmäßige **description**-Eigenschaft aus dem Webpart. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Ersetzen Sie die **render**-Methode durch den folgenden Code:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  // ...
  public render(): void {
    const element: React.ReactElement<IRecentDocumentsProps > = React.createElement(
      RecentDocuments,
      {
      }
    );

    ReactDom.render(element, this.domElement);
  }
  // ...
}
```

Ersetzen Sie dann die **getPropertyPaneConfiguration**-Methode durch den folgenden Code:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
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
              groupFields: []
            }
          ]
        }
      ]
    };
  }
}
```

### <a name="create-the-idocumentactivity-interface"></a>Erstellen der IDocumentActivity-Schnittstelle

Erstellen Sie im Ordner **./src/webparts/recentDocuments** eine neue Datei namens **IDocumentActivity.ts**, und fügen Sie den folgenden Code ein:

```ts
export interface IDocumentActivity {
    title: string;
    actorName: string;
    actorImageUrl: string;
}
```

Diese Schnittstelle wird verwendet, um die Aktivitätsinformationen eines bestimmten Dokuments auf einer Karte anzuzeigen.

### <a name="create-the-idocument-interface"></a>Erstellen der IDocument-Schnittstelle

Erstellen Sie im Ordner **./src/webparts/recentDocuments** eine neue Datei namens **IDocument.ts**, und fügen Sie den folgenden Code ein:

```ts
import { IDocumentActivity } from './IDocumentActivity';

export interface IDocument {
    title: string;
    url: string;
    imageUrl: string;
    iconUrl: string;
    activity: IDocumentActivity;
}
```

Diese Schnittstelle stellt ein Dokument mit allen erforderlichen Informationen zum Anzeigen des Dokuments als Karte dar.

### <a name="show-recent-documents-in-the-recentdocuments-react-component"></a>Anzeigen zuletzt verwendeter Dokumente in der React-Komponente „RecentDocuments“ 

Fügen Sie die **documents**-Eigenschaft zu der **IRecentDocumentsProps**-Schnittstelle hinzu. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und fügen Sie den folgenden Code ein:

```ts
import { IDocument } from '../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/RecentDocuments.tsx**, und fügen Sie den folgenden Code ein:

```tsx
import * as React from 'react';
import {
  DocumentCard,
  DocumentCardType,
  DocumentCardPreview,
  DocumentCardTitle,
  DocumentCardActivity
} from 'office-ui-fabric-react';
import { IDocument } from '../IDocument';
import styles from './RecentDocuments.module.scss';
import { IRecentDocumentsProps } from './IRecentDocumentsProps';

export default class RecentDocuments extends React.Component<IRecentDocumentsProps, void> {
  public render(): React.ReactElement<IRecentDocumentsProps> {
    const documents: JSX.Element[] = this.props.documents.map((document: IDocument, index: number, array: IDocument[]): JSX.Element => {
      return (
        <DocumentCard type={DocumentCardType.compact} onClickHref={document.url} accentColor='#ce4b1f' key={index}>
          <DocumentCardPreview previewImages={[{
            name: document.title,
            url: document.url,
            previewImageSrc: document.imageUrl,
            iconSrc: document.iconUrl,
            width: 144
          }]} />
          <div className='ms-DocumentCard-details'>
            <DocumentCardTitle
              title={document.title}
              shouldTruncate={true} />
            <DocumentCardActivity
              activity={document.activity.title}
              people={
                [
                  { name: document.activity.actorName, profileImageSrc: document.activity.actorImageUrl }
                ]
              }
              />
          </div>
        </DocumentCard>
      );
    });
    return (
      <div className={styles.helloWorld}>
        {documents}
      </div>
    );
  }
}
```

Die Komponente durchläuft zunächst die Dokumente, die unter Verwendung der **documents**-Eigenschaft übergeben wurden. Für jedes Dokument wird eine [Office UI Fabric-Dokumentkarte](https://dev.office.com/fabric#/components/documentcard) erstellt, mit der die Eigenschaften mit den relevanten Informationen zu dem jeweiligen Dokument gefüllt werden. Wenn Karten für alle Dokumente erstellt wurden, fügt die Komponente diese schließlich zu ihrem Text hinzu und gibt das gesamte Markup zurück.

### <a name="load-the-information-about-the-recent-documents"></a>Laden der Informationen zu den zuletzt verwendeten Dokumenten

In diesem Beispiel werden die Informationen zu den zuletzt geänderten Dokumenten aus einem statischen Dataset geladen. Sie könnten diese Implementierung jedoch ganz einfach ändern, um die Daten stattdessen aus einer SharePoint-Dokumentbibliothek zu laden.

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Fügen Sie den import-Anweisungen im oberen Abschnitt der Datei einen Verweis auf die **IDocument**-Schnittstelle mithilfe des folgenden Codes hinzu:

```ts
import { IDocument } from './IDocument';
```

Fügen Sie in der **RecentDocumentsWebPart**-Klasse eine neue private Variable mit dem Namen **Dokumente** mithilfe des folgenden Codes hinzu:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    private static documents: IDocument[] = [
        {
            title: 'Proposal for Jacksonville Expansion Ad Campaign',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 25 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Customer Feedback for ZT1000',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Asia Q3 Marketing Overview',
            url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Trey Research Business Development Plan',
            url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 15 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'XT1000 Marketing Analysis',
            url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, December 15 2016',
                actorName: 'Henrietta Mueller',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
            }
        }
    ];

    // ...
}
```

Ändern Sie die **render**-Methode so, dass die Informationen zu den zuletzt geänderten Dokumenten geladen und gerendert werden:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  // ...
  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    window.setTimeout((): void => {
      const element: React.ReactElement<IRecentDocumentsProps> = React.createElement(
        RecentDocuments,
        {
          documents: RecentDocumentsWebPart.documents.slice(0, 3)
        }
      );

      this.context.statusRenderer.clearLoadingIndicator(this.domElement);
      ReactDom.render(element, this.domElement);
    }, 300);
  }
  // ...
}
```

Überprüfen Sie, dass das Webpart korrekt funktioniert und Informationen zu den drei zuletzt geänderten Dokumenten anzeigt, indem Sie den folgenden Befehl ausführen:

```sh
gulp serve
```

Fügen Sie in der SharePoint Workbench das Webpart „Zuletzt verwendete Dokumente“ dem Zeichenbereich hinzu.

![Das Webpart „Zuletzt verwendete Dokumente“, das die drei zuletzt geänderten Dokumente als Dokumentkarten anzeigt](../../../../images/tutorial-sharingdata-recent-documents.png)

## <a name="show-the-most-recently-modified-document"></a>Anzeigen des kürzlich geänderten Dokuments

Das Webpart „Zuletzt verwendetes Dokument“ zeigt Informationen zu dem zuletzt geänderten Dokument an.

![Das Webpart „Zuletzt verwendetes Dokument“ zeigt eine große Dokumentkarte mit Informationen zu dem zuletzt geänderten Dokument an]()

### <a name="add-the-second-web-part"></a>Hinzufügen des zweiten Webpart

Um die Freigabe von Daten zwischen Webparts zu veranschaulichen, fügen Sie dem Projekt ein zweites Webpart hinzu.

Führen Sie im Projektordner den Yeoman-Generator von SharePoint Framework aus.

```sh
yo @microsoft/sharepoint
```

Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:

- **Zuletzt verwendetes Dokument** als Name des Webparts.
- **Zeigt Informationen zu dem zuletzt geänderten Dokumentinformation** als Beschreibung des Webparts.

![Der Yeoman-Generator von SharePoint Framework mit Informationen zum Erstellen eines Gerüsts für das zweite Webpart.](../../../../images/tutorial-sharingdata-yo-sharepoint-recent-document.png)

### <a name="remove-the-standard-description-property"></a>Entfernen der standardmäßigen _description_-Eigenschaft

Beginnen Sie, indem Sie die **description**-Eigenschaft aus der **IRecentDocumentsWebPartProps**-Schnittstelle entfernen. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts**, und fügen Sie den folgenden Code ein:

```ts
export interface IRecentDocumentWebPartProps {
}
```

Entfernen Sie die standardmäßige **description**-Eigenschaft aus dem Webpartmanifest. Öffnen Sie die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json**, und entfernen Sie die **description**-Eigenschaft aus der **properties**-Eigenschaft:

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "71a6f643-1ac1-47ee-a9f1-502ef52f26d4",
  "alias": "RecentDocumentWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "71a6f643-1ac1-47ee-a9f1-502ef52f26d4",
    "group": { "default": "Under Development" },
    "title": { "default": "Recent document" },
    "description": { "default": "Shows information about the most recently modified document" },
    "officeFabricIconFontName": "Page",
    "properties": {
    }
  }]
}
```

Entfernen Sie schließlich die standardmäßige **description**-Eigenschaft aus dem Eigenschaftenbereich des Webparts. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Ersetzen Sie die **render**-Methode durch den folgenden Code:

```ts
export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
  // ...
  public render(): void {
    const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
      RecentDocument,
      {
      }
    );

    ReactDom.render(element, this.domElement);
  }
  // ...
}
```

Ersetzen Sie dann die **getPropertyPaneConfiguration**-Methode durch den folgenden Code:

```ts
export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
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
              groupFields: []
            }
          ]
        }
      ]
    };
  }
}
```

### <a name="reuse-the-idocument-and-idocumentactivity-interfaces"></a>Wiederverwenden der _IDocument_- und _IDocumentActivity_-Schnittstellen

Das Webpart „Zuletzt verwendetes Dokument“ zeigt Informationen zu dem zuletzt geänderten Dokument anders als das Webpart „Zuletzt verwendete Dokumente“ an, beide Webparts verwenden aber dieselbe Datenstruktur, die ein Dokument darstellt. Anstatt die Schnittstellen **IDocument** und **IDocumentActivity** zu duplizieren, können Sie sie in beiden Webparts wiederverwenden.

Aktivieren Sie in Visual Studio Code das Explorer-Fenster aus dem Ordner **./src/webparts/recentDocuments**, und verschieben Sie die Dateien **IDocument.ts** und **IDocumentActivity.ts** eine Ebene nach oben zum Ordner **./src/webparts**.

![Explorer-Fenster in Visual Studio Code, in dem die Dateien „IDocument.ts“ und „ IDocumentActivity.ts“ hervorgehoben sind](../../../../images/tutorial-sharingdata-interfaces.png)

#### <a name="update-references-to-the-moved-files"></a>Aktualisieren der Verweise auf die verschobenen Dateien

Da Sie die Dateien an einen anderen Ort in Ihrem Projekt verschoben haben, müssen Sie die Pfade in ihren Verweisen aktualisieren.

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und ändern Sie ihren Code folgendermaßen:

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

Öffnen Sie als Nächstes die **./src/webparts/recentDocuments/components/RecentDocuments.tsx**-Datei, und aktualisieren Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../../IDocument';
```

Öffnen Sie schließlich die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**, und aktualisieren Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../IDocument';
```

### <a name="show-the-most-recent-document-in-the-recentdocument-react-component"></a>Anzeigen des zuletzt verwendeten Dokuments in der React-Komponente „RecentDocuments“

Fügen Sie die **document**-Eigenschaft zu der **IRecentDocumentProps**-Schnittstelle hinzu. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/components/IRecentDocumentprops.ts**, und fügen Sie den folgenden Code ein:

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/components/RecentDocument.tsx**, und fügen Sie den folgenden Code ein:

```tsx
import * as React from 'react';
import {
  DocumentCard,
  DocumentCardPreview,
  DocumentCardTitle,
  DocumentCardActivity,
  ImageFit
} from 'office-ui-fabric-react';
import { IDocument } from '../../IDocument';
import styles from './RecentDocument.module.scss';
import { IRecentDocumentProps } from './IRecentDocumentProps';

export default class RecentDocument extends React.Component<IRecentDocumentProps, void> {
  public render(): React.ReactElement<IRecentDocumentProps> {
    const document: IDocument = this.props.document;

    return (
      <div className={styles.helloWorld}>
        <DocumentCard onClickHref={document.url}>
          <DocumentCardPreview previewImages={[{
            name: document.title,
            url: document.url,
            previewImageSrc: document.imageUrl,
            iconSrc: document.iconUrl,
            imageFit: ImageFit.cover,
            width: 318,
            height: 196,
            accentColor: '#ce4b1f'
          }]} />
          <DocumentCardTitle
            title={document.title}
            shouldTruncate={true} />
          <DocumentCardActivity
            activity={document.activity.title}
            people={
              [
                { name: document.activity.actorName, profileImageSrc: document.activity.actorImageUrl }
              ]
            }
            />
        </DocumentCard>
      </div>
    );
  }
}
```

Die React-Komponente **RecentDocument** verwendet die Informationen zu dem zuletzt geänderten Dokument, das an die **document**-Eigenschaft übergeben wurde, und verwendet dieses zum Rendern einer Office UI Fabric-Dokumentkarte.

### <a name="load-the-information-about-the-recent-document"></a>Laden der Informationen zu dem zuletzt verwendeten Dokument

In diesem Beispiel werden die Informationen zu dem zuletzt geänderten Dokument aus einem statischen Dataset geladen. Sie könnten diese Implementierung jedoch ganz einfach ändern, um die Daten stattdessen aus einer SharePoint-Dokumentbibliothek zu laden.

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Fügen Sie den import-Anweisungen im oberen Abschnitt der Datei einen Verweis auf die **IDocument**-Schnittstelle mithilfe des folgenden Codes hinzu:

```ts
import { IDocument } from '../IDocument';
```

Fügen Sie in der **RecentDocumentWebPart**-Klasse eine neue private Variable mit dem Namen **Dokument** mithilfe des folgenden Codes hinzu:

```ts
export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
    private static document: IDocument = {
        title: 'Proposal for Jacksonville Expansion Ad Campaign',
        url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
        imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
        iconUrl: '',
        activity: {
            title: 'Modified, January 25 2017',
            actorName: 'Miriam Graham',
            actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
        }
    };

    // ...
}
```

Ändern Sie die **render**-Methode so, dass die Informationen zu dem zuletzt geänderten Dokument geladen und gerendert werden:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  // ...
  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    window.setTimeout((): void => {
      const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
        RecentDocument,
        {
          document: RecentDocumentWebPart.document
        }
      );

      this.context.statusRenderer.clearLoadingIndicator(this.domElement);
      ReactDom.render(element, this.domElement);
    }, 300);
  }
  // ...
}
```

Überprüfen Sie, dass das Webpart korrekt funktioniert und Informationen zu dem zuletzt geänderten Dokument anzeigt, indem Sie den folgenden Befehl ausführen:

```sh
gulp serve
```

Fügen Sie in der SharePoint Workbench das Webpart „Zuletzt verwendetes Dokument“ dem Zeichenbereich hinzu.

![Das Webpart „Zuletzt verwendetes Dokument“ zeigt eine Dokumentkarte mit Informationen zu dem zuletzt geänderten Dokument an](../../../../images/tutorial-sharingdata-recent-document.png)

Die aktuelle Implementierung ist ein typisches Beispiel für zwei Webparts, die unabhängig voneinander entwickelt werden. Wenn sie beide auf derselben Seite platziert und Daten aus SharePoint laden würden, würden sie zwei separate Anforderungen zum Abrufen ähnlicher Informationen ausführen. Wenn Sie zu einem bestimmten Zeitpunkt den Ort ändern müssten, von dem die Informationen zu den zuletzt geänderten Dokumente ändern müssten, müssten Sie beide Webparts aktualisieren. Um die Leistung beim Laden der Seite zu verbessern und die Verwaltung des Webpartcodes zu vereinfachen, können Sie die Logik des Abrufens von Daten zentralisieren und die einmal abgerufenen Daten für beide Webparts verfügbar machen.

## <a name="centralize-loading-data"></a>Zentralisieren des Ladens von Daten

Um das Laden der Informationen zu den zuletzt geänderten Dokumenten zu zentralisieren, erstellen Sie einen Dienst, auf den von beiden Webparts verwiesen wird.

### <a name="move-data-model-interfaces"></a>Verschieben von Datenmodellschnittstellen

Erstellen Sie im Projektordner den Ordnerpfad **./src/services/documentsService**. Verschieben Sie die Dateien IDocument.ts und IDocumentActivity.ts aus dem Ordner**./src/webparts** in den Ordner ./src/services/documentsService Ordner.

![Die Dateien „IDocument.ts“ und „IDocumentActivity.ts“ sind im Explorer-Fenster in Visual Studio Code hervorgehoben](../../../../images/tutorial-sharingdata-interfaces-documentsservice.png)

### <a name="build-the-data-access-service"></a>Erstellen des Datenzugriffsdiensts

Erstellen Sie im Ordner **./src/services/documentsService** eine neue Datei namens **DocumentsService.ts**, und fügen Sie den folgenden Code ein:

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    private static documents: IDocument[] = [
        {
            title: 'Proposal for Jacksonville Expansion Ad Campaign',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 25 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Customer Feedback for ZT1000',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Asia Q3 Marketing Overview',
            url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Trey Research Business Development Plan',
            url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 15 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'XT1000 Marketing Analysis',
            url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, December 15 2016',
                actorName: 'Henrietta Mueller',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
            }
        }
    ];

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            window.setTimeout((): void => {
                resolve(DocumentsService.documents[0]);
            }, 300);
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            window.setTimeout((): void => {
                resolve(DocumentsService.documents.slice(startFrom, startFrom + 3));
            }, 300);
        });
    }
}
```

Die DocumentsService-Klasse ist ein Beispieldienst, der Informationen zu den zuletzt verwendeten Dokumenten lädt. In diesem Beispiel wird ein statisches Dataset verwendet, Sie können aber dessen Implementierung einfach ändern, um die Daten aus einer SharePoint-Dokumentbibliothek zu laden. In dieser Phase bietet die DocumentsService-Klasse einen zentralen Punkt für alle Webparts zum Zugriff auf ihre Daten, die zuvor geladenen Daten werden jedoch nicht gespeichert. Dies wird später in diesem Lernprogramm implementiert.

### <a name="create-barrel-for-the-service-files"></a>Erstellen eines Barrels für die Dienstdateien

Wenn Sie in einem Projekt auf Dateien verweisen, zeigen Sie auf ihren relativen Pfad. Jedes Mal, wenn sich der Pfad ändert, müssen Sie alle Verweise auf diese bestimmte Datei aktualisieren. Solche Änderungen sind zu Beginn des Projekts sehr wahrscheinlich, wenn die unterschiedlichen Elemente hinzugefügt werden und die finale Projektstruktur noch unklar ist. Zur Vermeidung häufiger Änderungen an Dateiverweisen in einem Projekt können Sie Barrels verwenden. 

Bei einem Barrel handelt es sich um einen Container, der mehrere exportierte Objekte kombiniert. Mithilfe von Barrels können Sie die genaue Position von Dateien von anderen Elementen im Projekt, die diese verwenden, abstrahieren.

Erstellen Sie im Ordner **./src/services/documentsService** eine neue Datei mti dem Name **index.ts**, und fügen Sie den folgenden Code ein:

```ts
export { IDocument } from './IDocument';
export { IDocumentActivity } from './IDocumentActivity';
export { DocumentsService } from './DocumentsService';
```

Wenn Sie ein solches Barrel definiert haben, können andere Elemente in dem Projekt auf einen der exportierten Typen anhand des relativen Pfads zum Ordner **./src/services/documentsService** anstelle des genauen Pfads zur Datei **IDocument.ts** verweisen. Zum Beispiel:

```ts
import { IDocument } from '../services/documentsService';
```

anstelle von:

```ts
import { IDocument } from '../services/documentsService/IDocument.ts';
```

Wenn Sie sich irgendwann einmal entscheiden, dass es besser wäre, die Datei **IDocument.ts** in einen Unterordner zu verschieben oder einige Dateien zusammenzuführen, müssten Sie nur den Pfad in der Barrel-Definition (**./src/services/documentsService/index.ts**) ändern. Alle Elemente im Projekt könnten weiterhin denselben relativen Pfad zum Ordner **documentsService** verwenden, um auf die **IDocument**-Schnittstelle zu verweisen.

### <a name="update-references-to-the-moved-files-using-the-barrel"></a>Aktualisieren der Verweise auf die verschobenen Dateien mithilfe des Barrels

Da Sie die Dateien **IDocument.ts** und **IDocumentActivity.ts** an einen anderen Ort verschoben haben, müssen Sie ihre Verweise aktualisieren. Dank des Barrels ist dies das letzte Mal, das Sie das tun müssen.

#### <a name="update-references-in-the-recent-documents-web-part"></a>Aktualisieren der Verweise im Webpart „Zuletzt verwendete Dokumente“

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und ändern Sie ihren Code folgendermaßen:

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

Öffnen Sie als Nächstes die **./src/webparts/recentDocuments/components/RecentDocuments.tsx**-Datei, und ändern Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../../../services/documentsService';
```

Öffnen Sie dann die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**, und ändern Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../../services/documentsService';
```

#### <a name="update-references-in-the-recent-document-web-part"></a>Aktualisieren der Verweise im Webpart „Zuletzt verwendetes Dokument“

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/components/IRecentDocumentProps.ts**, und ändern Sie ihren Code folgendermaßen:

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

Öffnen Sie als Nächstes die **./src/webparts/recentDocument/components/RecentDocument.tsx**-Datei, und ändern Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../../../services/documentsService';
```

Öffnen Sie dann die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**, und ändern Sie die **import**-Anweisung der **IDocument**-Schnittstelle folgendermaßen:

```ts
import { IDocument } from '../../services/documentsService';
```

Überprüfen Sie, ob Ihre Änderungen wie erwartet funktionieren, indem Sie den folgenden Befehl ausführen:

```sh
gulp serve
```

![Die Webparts „Zuletzt verwendetes Dokument“ und „Zuletzt verwendete Dokumente“ zeigen Informationen zu den zuletzt geänderten Dokumenten an](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="load-web-part-data-using-the-data-service"></a>Laden von Webpartdaten mithilfe des Datendiensts

Wenn der Datendienst bereit ist, besteht der nächste Schritt darin, beide Webparts so umzugestalten, dass der Datendienst zum Laden ihrer Daten verwendet wird.

#### <a name="load-information-about-the-recently-modified-documents"></a>Laden der Informationen zu den zuletzt geänderten Dokumenten

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Ändern Sie die **import**-Anweisung, die auf die **IDocument**-Schnittstelle verweist, folgendermaßen:

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

Aktualisieren Sie als Nächstes die **render**-Methode mit dem folgenden Code:

```ts
export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  // ...
  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    DocumentsService.getRecentDocuments()
      .then((documents: IDocument[]): void => {
        const element: React.ReactElement<IRecentDocumentsProps> = React.createElement(
          RecentDocuments,
          {
            documents: documents
          }
        );

        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        ReactDom.render(element, this.domElement);
      });
  }
  // ...
}
```

#### <a name="load-information-about-the-most-recently-modified-document"></a>Laden der Informationen zu dem zuletzt geänderten Dokument

Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Ändern Sie die **import**-Anweisung, die auf die **IDocument**-Schnittstelle verweist, folgendermaßen:

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

Aktualisieren Sie als Nächstes die **render**-Methode mit dem folgenden Code:

```ts
export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
  // ...
  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'document');

    DocumentsService.getRecentDocument()
      .then((document: IDocument): void => {
        const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
          RecentDocument,
          {
            document: document
          }
        );

        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        ReactDom.render(element, this.domElement);
      });
  }
  // ...
}
```

Bestätigen Sie, dass beide Webparts ordnungsgemäß arbeiten, indem Sie den folgenden Befehl ausführen:

```sh
gulp serve
```

![Die Webparts „Zuletzt verwendetes Dokument“ und „Zuletzt verwendete Dokumente“ zeigen Informationen zu den zuletzt geänderten Dokumenten an](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="share-the-data-between-web-parts"></a>Freigeben der Daten zwischen Webparts

Da nun beide Webparts den Datendienst zum Laden der Daten verwenden, besteht der nächste Schritt darin, den Datendienst so zu erweitern, dass dieser die Daten nur einmal lädt und diese für beide Webparts wiederverwendet.

Öffnen Sie im Code-Editor die Datei **./src/services/documentsService/DocumentsService.ts**, und fügen Sie den folgenden Code ein:

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    private static documents: IDocument[] = [
        {
            title: 'Proposal for Jacksonville Expansion Ad Campaign',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 25 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Customer Feedback for ZT1000',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Asia Q3 Marketing Overview',
            url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Trey Research Business Development Plan',
            url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 15 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'XT1000 Marketing Analysis',
            url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, December 15 2016',
                actorName: 'Henrietta Mueller',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
            }
        }
    ];

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            DocumentsService.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            DocumentsService.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            if ((window as any).loadedData) {
                // data already loaded. reuse
                resolve((window as any).loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded. wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                window.setTimeout((): void => {
                    // store the data for subsequent requests and resolve the Promise
                    (window as any).loadedData = DocumentsService.documents;
                    (window as any).loadingData = false;
                    resolve((window as any).loadedData);
                }, 300);
            }
        });
    }
}
```

Wenn ein Webpart den Datendienst zum Laden der Daten das erste Mal aufruft, legt der Dienst die globale Variable **loadingData** auf **true** fest. Dies deutet darauf hin, dass derzeit Daten geladen werden. Dies ist erforderlich, um zu verhindern, dass die Daten mehrmals geladen werden, falls ein anderes Webpart auch das Laden seiner Daten anfordern sollte, während die anfängliche Anforderung zum Laden der Daten noch nicht abgeschlossen wurde. In diesem Beispiel werden die Daten aus einem statischen Dataset geladen, Sie können aber die Implementierung einfach ändern, um die Daten aus einer SharePoint-Dokumentbibliothek zu laden.

Nachdem die Daten geladen wurden, werden sie in der globalen Variable **loadedData** gespeichert. Der Wert der Variablen **loadingData** wird auf **false** festgelegt, und das Versprechen wird mit den abgerufenen Daten aufgelöst. Das nächste Mal, wenn ein Webpart seine Daten anfordert, gibt der Datendienst die zuvor geladenen Daten zurück, wodurch alle Anforderungen an die Remote-APIs gelöscht werden.

Bestätigen Sie, dass beide Webparts ordnungsgemäß arbeiten, indem Sie den folgenden Befehl ausführen:

```sh
gulp serve
```

![Die Webparts „Zuletzt verwendetes Dokument“ und „Zuletzt verwendete Dokumente“ zeigen Informationen zu den zuletzt geänderten Dokumenten an](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

Wenn Sie in den verschiedenen Bereichen der **DocumentsService.ensureRecentDocuments**-Methode Protokollierungsanweisungen hinzugefügt haben, würden Sie sehen, dass die Daten einmal geladen und für das zweite Webpart wiederverwendet werden.

![Entwicklerkonsole, in der unterschiedliche Protokollierungsanweisungen in Microsoft Edge angezeigt werden](../../../../images/tutorial-sharingdata-console-log.png)

## <a name="see-also"></a>Siehe auch

- [Gemeinsame Verwendung von Daten zwischen clientseitigen Webparts](./share-data-between-web-parts)