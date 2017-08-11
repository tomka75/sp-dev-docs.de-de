# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a>Verwenden von Office UI Fabric React-Komponenten in clientseitigen SharePoint-Webparts

> **Wichtig:** Um Office UI Fabric React verwenden zu können, müssen Sie vorhandene Projekte auf @microsoft/sp-build-web@1.0.1 oder höher aktualisieren. Am einfachsten gelingt das, wenn Sie vor dem Durchspielen dieser Anleitung `npm install -g @microsoft/generator-sharepoint` in der Konsole ausführen, um sicherzustellen, dass Sie das neueste Paket haben. 

In diesem Artikel wird die Erstellung eines einfachen Webparts beschrieben, das die DocumentCard-Komponente von [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react) verwendet. Office UI Fabric React ist das Front-End-Framework zur Erstellung von Oberflächen für Office und Office 365. Fabric React umfasst eine Sammlung stabiler, dynamischer und für die Darstellung auf Mobilgeräten optimierter Komponenten zur unkomplizierten Erstellung von Weboberflächen mithilfe der Office-Entwurfssprache.

Die folgende Abbildung zeigt eine DocumentCard-Komponente, die mit Office UI Fabric React erstellt wurde:

![Abbildung der Fabric-Komponente „DocumentCard“ in einer SharePoint Workbench](../../../../images/fabric-components-doc-card-view-ex.png)

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen: 

<a href="https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="creating-a-new-web-part-project"></a>Erstellen eines neuen Webpartprojekts

Stellen Sie sicher, dass Sie die aktuelle Version von X verwenden. Führen Sie `yo` aus, und befolgen Sie die Anweisungen, um ein Projektgerüst zu erstellen.

Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:

```
md documentcardexample-webpart
```
    
Wechseln Sie in das Projektverzeichnis:

```
cd documentcardexample-webpart
```

Stellen Sie sicher, dass die aktuelle Version von `@microsoft/generator-sharepoint` installiert ist, und führen Sie den Yeoman-SharePoint-Generator aus, um ein neues Webpart zu erstellen:

```
yo @microsoft/sharepoint
```
    
Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

* Übernehmen Sie den Standardnamen **documentcardexample-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.
* Wählen Sie als Typ von clientseitiger Komponente **WebPart** aus, und drücken Sie die **EINGABETASTE**.
* Verwenden Sie **DocumentCardExample** als Namen des Webparts, und drücken Sie die **EINGABETASTE**.
* Akzeptieren Sie den Standardnamen **DocumentCardExample - Beschreibung**, und drücken Sie die **EINGABETASTE**.
* Wählen Sie **React** als Framework aus, und drücken Sie die**EINGABETASTE**.

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

### <a name="add-an-office-ui-fabric-component"></a>Hinzufügen einer Office UI Fabric-Komponente

Die *neuen modernen Benutzeroberflächen* in SharePoint verwenden die Office UI Fabric sowie Office UI Fabric React als standardmäßiges Front-End-Framework zur Erstellung neuer Benutzeroberflächen. SharePoint Framework enthält daher bei Auslieferung eine Standardversion der Office UI Fabric sowie eine Standardversion von Fabric React, die jeweils der in SharePoint verfügbaren Version entsprechen. Dadurch wird sichergestellt, dass das Webpart, das Sie erstellen, bei der Bereitstellung in SharePoint die richtige Version der Fabric-Formatvorlagen und -Komponenten verwendet. 

Da wir bei der Erstellung der Lösung React als Framework ausgewählt haben, hat der Generator auch die richtige Version von Office UI Fabric React installiert. Sie können die Fabric-Komponenten ohne weiteren Aufwand direkt in Ihre React-Komponenten importieren. 

>**Hinweis:** Wir empfehlen, mit der Erstversion von SharePoint Framework jeweils die Version von Office UI Fabric und Fabric React zu verwenden, die mit dem Generator ausgeliefert wird. Von einer separaten Aktualisierung der Pakete von Office UI Fabric und Fabric React raten wir ab. Sie könnte zu Konflikten mit der jeweils bereits in SharePoint verfügbaren Version führen. In einem solchen Fall würde Ihr Webpart möglicherweise nicht wie erwartet arbeiten.

Öffnen Sie die Datei **DocumentCardExample.tsx** im Ordner **src\webparts\documentCardExample\components**. 

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
          previewImageSrc: String(require('./document-preview.png')),
          iconSrc: String(require('./icon-ppt.png')),
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
              { name: 'Kat Larrson', profileImageSrc: String(require('./avatar-kat.png')) }
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

Die Eigenschaft `previewProps` enthält einige Eigenschaften von DocumentCardPreview.

Wie Sie sehen, wird hier ein relativer Pfad mit einer Anweisung des Typs `require` verwendet, um Bilder zu laden. Derzeit sind einige kleinere Konfigurationsanpassungen in der Datei „gulpfile.js“ nötig, damit diese Bilder korrekt von webpack verarbeitet werden.
    
Öffnen Sie die Datei **gulpfile.js** im Ordner **root**. 
    
Fügen Sie den folgenden Code direkt über der Codezeile `build.initialize(gulp);` ein:
    
```js
build.configureWebpack.mergeConfig({  
    additionalConfiguration: (generatedConfiguration) => {
        if (build.getConfig().production) {
            var basePath = build.writeManifests.taskConfig.cdnBasePath;
            if (!basePath.endsWith('/')) {
                basePath += '/';
            }
            generatedConfiguration.output.publicPath = basePath;
        }
        else {
            generatedConfiguration.output.publicPath = "/dist/";
        }
        return generatedConfiguration;
    }
});
```
    
Speichern Sie die Datei.

Die vollständige Datei **gulpfile.js** sollte wie folgt aussehen:

```js
'use strict';

const gulp = require('gulp');
const build = require('@microsoft/sp-build-web');

build.configureWebpack.mergeConfig({  
    additionalConfiguration: (generatedConfiguration) => {
        if (build.getConfig().production) {
            var basePath = build.writeManifests.taskConfig.cdnBasePath;
            if (!basePath.endsWith('/')) {
                basePath += '/';
            }
            generatedConfiguration.output.publicPath = basePath;
        }
        else {
            generatedConfiguration.output.publicPath = "/dist/";
        }
        return generatedConfiguration;
    }
});

build.initialize(gulp);

```

### <a name="copy-the-image-assets"></a>Kopieren der Bildobjekte

Kopieren Sie die folgenden Bilder in den Ordner **src\webparts\documentCardExample\components**:

* [avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)
* [icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)
* [document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)

### <a name="preview-the-web-part-in-workbench"></a>Anzeigen der Webpart-Vorschau in der Workbench

Geben Sie in der Konsole Folgendes ein, um das Webpart in der Workbench der Vorschau anzuzeigen:
    
```
gulp serve
```
    
Wählen Sie in der Toolbox Ihr `DocumentCardExample`-Webpart aus, das hinzugefügt werden soll:
    
![Abbildung der Fabric-Komponente „DocumentCard“ in einer SharePoint Workbench](../../../../images/fabric-components-doc-card-view-ex.png)
