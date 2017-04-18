# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a>Verwenden von React-Komponenten der Office UI Fabric in Ihrem clientseitigen SharePoint-Webpart

Dieser Artikel beschreibt, wie ein einfaches Webpart erstellt wird, das die DocumentCard-Komponente der [Office UI Fabric](https://github.com/OfficeDev/office-ui-fabric-react) verwendet. Office UI Fabric React ist das Front-End-Framework zum Erstellen von Oberflächen für Office und Office 365. Fabric React umfasst eine robuste Sammlung dynamischer Mobilitätskomponenten, die Ihnen das Erstellen von Weboberflächen mithilfe der Office-Entwurfssprache erleichtern.

Die folgende Abbildung zeigt eine DocumentCard-Komponente, die mit Office UI Fabric React erstellt wurde.

![Abbildung der Fabric-Komponente „DocumentCard“ in einer SharePoint Workbench](../../../../images/fabric-components-doc-card-view-ex.png)

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen: 

<a href="https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a>Erstellen eines neuen Webpart-Projekts

Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:

```
md documentcardexample-webpart
```
    
Wechseln Sie in das Projektverzeichnis:

```
cd documentcardexample-webpart
```

Führen Sie den Yeoman-SharePoint-Generator aus, um ein neues Webpart zu erstellen:

```
yo @microsoft/sharepoint
```
    
Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

* Akzeptieren Sie den Standardnamen **documentcardexample-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.
* Wählen Sie **Aktuellen Ordner verwenden** als Speicherort für die Dateien aus.
* Wählen Sie **React** als Framework aus, und drücken Sie die**EINGABETASTE**.
* Verwenden Sie **DocumentCardExample** als Namen des Webparts, und drücken Sie die **EINGABETASTE**.
* Akzeptieren Sie den Standardnamen **DocumentCardExample - Beschreibung**, und drücken Sie die **EINGABETASTE**.

An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien. Das kann einige Minuten dauern. Yeoman erstellt ein Gerüst für das Projekt, um auch das DocumentCardExample-Webpart einzuschließen.
    
Wenn das Gerüst abgeschlossen ist, geben Sie in der Konsole Folgendes ein, um das Webpartprojekt in Visual Studio-Code zu öffnen:

```
code .
```
    
Sie haben nun ein Webpartprojekt mit dem React-Framework erstellt.

Öffnen Sie **DocumentCardExampleWebPart.ts** im Ordner **src\webparts\documentCardExample**. 

Wie Sie sehen können, erstellt die`render`-Methode ein React-Element und rendert es im Webpart-DOM.

```ts
  public render(): void {
    const element: React.ReactElement<IDocumentCardExampleProps > = React.createElement(
      DocumentCardExample,
      {
        description: this.properties.description
      }
    );
```
    
Öffnen Sie **DocumentCardExample.tsx** im Ordner **src\webparts\documentCardExample\components**. 
    
Dies ist die wichtigste React-Komponente, die Yeoman zu Ihrem Projekt hinzugefügt hat, das im Webpart-DOM gerendert wird.

```ts
export default class DocumentCardExample extends React.Component<IDocumentCardExampleProps, void> {
  public render(): React.ReactElement<IDocumentCardExampleProps> {
    return (
      <div className={styles.helloWorld}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
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

## <a name="add-an-office-ui-fabric-component"></a>Hinzufügen einer Office UI Fabric-Komponente

Die *neuen modernen Benutzeroberflächen* in SharePoint verwenden die Office UI Fabric sowie Office UI Fabric React als standardmäßiges Front-End-Framework zur Erstellung neuer Benutzeroberflächen. SharePoint Framework enthält daher bei Auslieferung eine Standardversion der Office UI Fabric sowie eine Standardversion von Fabric React, die jeweils der in SharePoint verfügbaren Version entsprechen. Dadurch wird sichergestellt, dass das Webpart, das Sie erstellen, bei der Bereitstellung in SharePoint die richtige Version der Fabric-Formatvorlagen und -Komponenten verwendet. 

Da wir bei der Erstellung der Lösung React als Framework ausgewählt haben, hat der Generator auch die richtige Version von Office UI Fabric React installiert. Sie können die Fabric-Komponenten ohne weiteren Aufwand direkt in Ihre React-Komponenten importieren. 

>**Hinweis:** Bei der Erstveröffentlichung von SharePoint Framework empfehlen wir, jeweils die Office UI Fabric- und Fabric React-Version zu verwenden, die mit dem Generator ausgeliefert wird. Von einer separaten Aktualisierung der Office UI Fabric- und Fabric React-Pakete raten wir ab. Sie könnte zu Konflikten mit der jeweils bereits in SharePoint verfügbaren Version führen. In einem solchen Fall würde Ihr Webpart möglicherweise nicht wie erwartet arbeiten. Nach GA werden Updates für diesen Bereich veröffentlicht.

Öffnen Sie **DocumentCardExample.tsx** im Ordner **src\webparts\documentCardExample\components**. 

Fügen Sie die folgende `import`-Anweisung am Anfang der Datei hinzu, um React-Komponenten der Fabric zu importieren, die verwendet werden sollen.

```ts
import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    IDocumentCardPreviewProps
} from 'office-ui-fabric-react/lib/DocumentCard';
```

Löschen Sie die aktuelle `render`-Methode, und fügen Sie die folgende aktualisierte `render`-Methode hinzu:

```ts
public render(): JSX.Element {
    const previewProps: IDocumentCardPreviewProps = {
        previewImages: [
        {
            previewImageSrc: String(require('document-preview.png')),
            iconSrc: String(require('icon-ppt.png')),
            width: 318,
            height: 196,
            accentColor: '#ce4b1f'
        }
        ],
    };

    return (
        <DocumentCard onClickHref='http://bing.com'>
        <DocumentCardPreview { ...previewProps } />
        <DocumentCardTitle title='Revenue stream proposal fiscal year 2016 version02.pptx' />
        <DocumentCardActivity
            activity='Created Feb 23, 2016'
            people={
            [
                { name: 'Kat Larrson', profileImageSrc: String(require('avatar-kat.png')) }
            ]
            }
            />
        </DocumentCard>
    );
}
```
Speichern Sie die Datei.

In diesem Code enthält die DocumentCard-Komponente einige zusätzliche Abschnitte:

* DocumentCardPreview
* DocumentCardTitle
* DocumentCardActivity

Die `previewProps`-Eigenschaft enthält einige Eigenschaften der DocumentCardPreview.

Beachten Sie die Verwendung des relativen Pfads mit einer `require`-Anweisung, um Bilder zu laden. Derzeit müssen Sie das Plug-In für den öffentlichen Pfad von webpack verwenden und den relativen Pfad der Datei aus der Quelldatei oder aus dem Quellordner in den `lib`-Ordner eingeben. Dies sollte derselbe Speicherort wie die aktuelle Arbeitsquelle sein.
    
Öffnen Sie **DocumentCardExampleWebPart.ts** im Ordner **src\webparts\documentCardExample**. 
    
Fügen Sie den folgenden Code am Anfang der Datei hinzu, um das Plug-In für den öffentlichen Pfad von webpack anzufordern.
    
```ts
require('set-webpack-public-path!');
```
    
Speichern Sie die Datei.

## <a name="copy-the-image-assets"></a>Kopieren der Bildanlagen

Kopieren Sie die folgenden Bilder in den Ordner **src\webparts\documentCardExample**:

* [avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)
* [icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)
* [document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)

## <a name="preview-the-web-part-in-workbench"></a>Anzeigen der Webpart-Vorschau in der Workbench

Geben Sie in der Konsole Folgendes ein, um das Webpart in der Workbench der Vorschau anzuzeigen:
    
```
gulp serve
```
    
Wählen Sie in der Toolbox Ihr `DocumentCardExample`-Webpart aus, das hinzugefügt werden soll:
    
![Abbildung der Fabric-Komponente „DocumentCard“ in einer SharePoint Workbench](../../../../images/fabric-components-doc-card-view-ex.png)

