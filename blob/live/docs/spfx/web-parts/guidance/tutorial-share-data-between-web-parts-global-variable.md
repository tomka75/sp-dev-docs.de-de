---
title: Gemeinsame Verwendung von Daten zwischen Webparts mithilfe einer globalen Variable (Tutorial)
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 5ee1bf737bc3d78636e981092212e5f37d89d5bc
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/20/2017
---
# <a name="share-data-between-web-parts-using-a-global-variable-tutorial"></a><span data-ttu-id="4a1b8-102">Gemeinsame Verwendung von Daten zwischen Webparts mithilfe einer globalen Variable (Tutorial)</span><span class="sxs-lookup"><span data-stu-id="4a1b8-102">Share Data Between Web Parts Using a Global Variable (Tutorial)</span></span>

> <span data-ttu-id="4a1b8-103">Hinweis: Wir konnten noch nicht überprüfen, ob sich die Anleitung in diesem Artikel mit der allgemein verfügbaren SPFx-Version (GA-Version) umsetzen lässt. Möglicherweise treten Probleme auf, wenn Sie die neueste Version für dieses Tutorial verwenden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-103">Note: This article has not yet been verified with the SPFx GA version, so you might have challenges making this work as described using the latest release.</span></span>

<span data-ttu-id="4a1b8-p101">Wenn Sie bei der Erstellung von clientseitigen Webparts Daten nur einmal laden und anschließend in den verschiedenen Webparts jeweils wiederverwenden, verbessert das die Leistung Ihrer Seiten und reduziert die Last in Ihrem Netzwerk. In diesem Tutorial beschreiben wir Schritt für Schritt, wie Webparts Daten mithilfe einer globalen Variable gemeinsam verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p101">When building client-side web parts, loading data once and reusing it across different web parts will help improve the performance of your pages and decrease the load on your network. This tutorial illustrates step-by-step how to share data between web parts using a global variable.</span></span>

> <span data-ttu-id="4a1b8-106">**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen können, müssen Sie [Ihre Entwicklungsumgebung für die Erstellung clientseitiger SharePoint-Webparts einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="4a1b8-106">**Note:** Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="prepare-the-project"></a><span data-ttu-id="4a1b8-107">Vorbereiten des Projekts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-107">Prepare the Project</span></span>

### <a name="create-a-new-project"></a><span data-ttu-id="4a1b8-108">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-108">Create a New Project</span></span>

<span data-ttu-id="4a1b8-109">Erstellen Sie über eine Eingabeaufforderung einen Ordner für Ihr Projekt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-109">Using a command prompt, create a new folder for your project:</span></span>

```sh
md react-recentdocuments
```

<span data-ttu-id="4a1b8-110">Wechseln Sie in den Projektordner:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-110">Go into the project folder:</span></span>

```sh
cd react-recentdocuments
```

<span data-ttu-id="4a1b8-111">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-111">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="4a1b8-112">Es werden verschiedene Eingabeaufforderungen angezeigt. Geben Sie jeweils die folgenden Werte an:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-112">When prompted, use the following values:</span></span>

- <span data-ttu-id="4a1b8-113">**WebPart** als den Typ von zu erstellender clientseitiger Komponente</span><span class="sxs-lookup"><span data-stu-id="4a1b8-113">**WebPart** as the type of client-side component to create.</span></span>
- <span data-ttu-id="4a1b8-114">**react-recentdocuments** als Namen der Lösung</span><span class="sxs-lookup"><span data-stu-id="4a1b8-114">**react-recentdocuments** as your solution name.</span></span>
- <span data-ttu-id="4a1b8-115">**Verwenden Sie den aktuellen Ordner** als Speicherort für die Dateien.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-115">**Use the current folder** for the location to place the files.</span></span>
- <span data-ttu-id="4a1b8-116">**Zuletzt verwendete Dokumente** als Name des Webparts.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-116">**Recent documents** as your web part name.</span></span>
- <span data-ttu-id="4a1b8-117">**Shows recently modified documents** als Beschreibung Ihres Webparts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-117">**Shows recently modified documents** as your web part description.</span></span>
- <span data-ttu-id="4a1b8-118">**React** als das zu verwendende Framework</span><span class="sxs-lookup"><span data-stu-id="4a1b8-118">**React** as the framework to use.</span></span>

![Der SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../images/tutorial-sharingdata-yo-sharepoint-recent-documents.png)

<span data-ttu-id="4a1b8-120">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-120">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="4a1b8-121">Öffnen Sie dann den Projektordner im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-121">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="4a1b8-122">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-122">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Das SharePoint Framework-Projekt in Visual Studio-Code](../../../images/tutorial-sharingdata-vscode.png)

## <a name="show-the-recently-modified-documents"></a><span data-ttu-id="4a1b8-124">Anzeigen der kürzlich geänderten Dokumente</span><span class="sxs-lookup"><span data-stu-id="4a1b8-124">Show the Recently Modified Documents</span></span>

<span data-ttu-id="4a1b8-125">Das Webpart „Zuletzt verwendete Dokumente“ zeigt Informationen zu den zuletzt geänderten Dokumenten an, die jeweils als Office UI Fabric-Karte dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-125">The Recent documents web part shows information about the most recently modified documents displayed as cards using the Office UI Fabric.</span></span>

![Webpart „Zuletzt verwendete Dokumente“ mit drei kleinen Dokumentkarten für die drei zuletzt geänderten Dokumente](../../../images/tutorial-sharingdata-recent-documents.png)

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="4a1b8-127">Entfernen der Standardeigenschaft _description_</span><span class="sxs-lookup"><span data-stu-id="4a1b8-127">Remove the Standard _description_ Property</span></span>

<span data-ttu-id="4a1b8-p103">Im ersten Schritt entfernen Sie die Standardeigenschaft `description` aus der Schnittstelle `IRecentDocumentsWebPartProps`. Öffnen Sie hierzu im Code-Editor die Datei **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p103">Start by removing the standard `description` property from the `IRecentDocumentsWebPartProps` interface. In the code editor, open the **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts** file and paste the following code:</span></span>

```ts
export interface IRecentDocumentsWebPartProps {
}
```

<span data-ttu-id="4a1b8-p104">Entfernen Sie nun die Standardeigenschaft `description` aus dem Webpartmanifest. Öffnen Sie hierzu die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json**, und entfernen Sie aus der Eigenschaft `properties` die Eigenschaft `description`:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p104">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

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

<span data-ttu-id="4a1b8-p105">Entfernen Sie anschließend die Standardeigenschaft `description` aus dem Webpart. Öffnen Sie dazu im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**, und ersetzen Sie die Methode `render` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p105">Finally, remove the standard `description` property from the web part. In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Replace its `render` method with the following code:</span></span>

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

<span data-ttu-id="4a1b8-135">Ersetzen Sie nun die Methode `getPropertyPaneConfiguration` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-135">Then, replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

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

### <a name="create-the-idocumentactivity-interface"></a><span data-ttu-id="4a1b8-136">Erstellen der Schnittstelle „IDocumentActivity“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-136">Create the IDocumentActivity Interface</span></span>

<span data-ttu-id="4a1b8-137">Erstellen Sie im Ordner **./src/webparts/recentDocuments** eine neue Datei mit dem Namen **IDocumentActivity.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-137">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocumentActivity.ts** and paste the following code:</span></span>

```ts
export interface IDocumentActivity {
    title: string;
    actorName: string;
    actorImageUrl: string;
}
```

<span data-ttu-id="4a1b8-138">Diese Schnittstelle wird verwendet, um die Aktivitätsinformationen eines gegebenen Dokuments auf einer Karte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-138">This interface is used to display the activity information of a particular document on a card.</span></span>

### <a name="create-the-idocument-interface"></a><span data-ttu-id="4a1b8-139">Erstellen der Schnittstelle „IDocument“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-139">Create the IDocument Interface</span></span>

<span data-ttu-id="4a1b8-140">Erstellen Sie im Ordner **./src/webparts/recentDocuments** eine neue Datei mit dem Namen **IDocument.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-140">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocument.ts** and paste the following code:</span></span>

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

<span data-ttu-id="4a1b8-141">Diese Schnittstelle repräsentiert ein Dokument samt allen Informationen, die erforderlich sind, um es als Karte anzeigen zu können.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-141">This interface represents a document with all information necessary to display the document as a card.</span></span>

### <a name="show-recent-documents-in-the-recentdocuments-react-component"></a><span data-ttu-id="4a1b8-142">Anzeigen zuletzt verwendeter Dokumente in der React-Komponente „RecentDocuments“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-142">Show Recent Documents in the RecentDocuments React Component</span></span>

<span data-ttu-id="4a1b8-p106">Fügen Sie die **documents**-Eigenschaft zu der **IRecentDocumentsProps**-Schnittstelle hinzu. Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p106">Add the **documents** property to the **IRecentDocumentsProps** interface. In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file, and paste the following code:</span></span>

```ts
import { IDocument } from '../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="4a1b8-145">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/RecentDocuments.tsx**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-145">In the code editor, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and paste the following code:</span></span>

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

<span data-ttu-id="4a1b8-p107">Die Komponente durchläuft zunächst die Dokumente, die in der Komponenteneigenschaft `documents` übergeben wurden. Dabei erstellt sie für jedes Dokument eine [Office UI Fabric-Dokumentkarte](https://dev.office.com/fabric#/components/documentcard) und trägt als deren Eigenschaften die entsprechenden Informationen zu dem jeweiligen Dokument ein. Sobald für jedes Dokument eine Karte erstellt wurde, fügt die Komponente diese Karten ihrem Textkörper hinzu und gibt das vollständige Markup zurück.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p107">First, the component iterates through the documents passed using its `documents` property. For each document, it builds an [Office UI Fabric Document Card](https://dev.office.com/fabric#/components/documentcard) filling its properties with the relevant information about that particular document. Finally, when cards for all documents have been built, the component adds them to its body and returns the complete markup.</span></span>

### <a name="load-the-information-about-the-recent-documents"></a><span data-ttu-id="4a1b8-149">Laden der Informationen zu den zuletzt verwendeten Dokumenten</span><span class="sxs-lookup"><span data-stu-id="4a1b8-149">Load the Information About the Recent Documents</span></span>

<span data-ttu-id="4a1b8-p108">In diesem Beispiel werden die Informationen zu den zuletzt geänderten Dokumenten aus einem statischen Dataset geladen. Sie können die Implementierung jedoch auch mühelos so abändern, dass die Daten stattdessen aus einer SharePoint-Dokumentbibliothek geladen werden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p108">In this example, the information about the recently modified documents is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

<span data-ttu-id="4a1b8-p109">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Fügen Sie eine Importanweisung für die Schnittstelle `IDocument` unterhalb der anderen Importanweisungen am Anfang der Datei ein. Verwenden Sie hierzu den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p109">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Add an import statement for the `IDocument` interface under the other import statements at the top of the file using the following code:</span></span>

```ts
import { IDocument } from './IDocument';
```

<span data-ttu-id="4a1b8-154">Fügen Sie in der Klasse `RecentDocumentsWebPart` eine neue private Variable mit dem Namen `documents` ein. Verwenden Sie hierzu den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-154">In the `RecentDocumentsWebPart` class, add a new private variable named `documents` using the following code:</span></span>

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

<span data-ttu-id="4a1b8-155">Ändern Sie die Methode `render` so, dass die Informationen zu den zuletzt geänderten Dokumenten geladen und gerendert werden:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-155">Change the `render` method to load and render the information about the recently modified documents:</span></span>

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

<span data-ttu-id="4a1b8-156">Überprüfen Sie nun, ob das Webpart korrekt funktioniert und Informationen zu den drei zuletzt geänderten Dokumenten anzeigt. Führen Sie dazu den folgenden Befehl über eine Eingabeaufforderung in Ihrem Projektverzeichnis aus:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-156">Verify that the web part is working correctly and shows information about the three most recently modified documents by running the following command from a command prompt in your project directory:</span></span>

```sh
gulp serve
```

<span data-ttu-id="4a1b8-157">Fügen Sie in SharePoint Workbench das Webpart „Zuletzt verwendete Dokumente“ zur Canvas hinzu.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-157">In the SharePoint workbench add the Recent Documents web part to the canvas.</span></span>

![Webpart „Zuletzt verwendete Dokumente“ mit Dokumentkarten für die drei zuletzt geänderten Dokumente](../../../images/tutorial-sharingdata-recent-documents.png)

## <a name="show-the-most-recently-modified-document"></a><span data-ttu-id="4a1b8-159">Anzeigen des zuletzt geänderten Dokuments</span><span class="sxs-lookup"><span data-stu-id="4a1b8-159">Show the Most Recently Modified Document</span></span>

<span data-ttu-id="4a1b8-160">Das Webpart „Recent document“ zeigt Informationen zu dem zuletzt geänderten Dokument an.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-160">The Recent document web part shows information about the most recently modified document.</span></span>

![Webpart „Recent document“ mit einer großen Dokumentkarte mit Informationen zu dem zuletzt geänderten Dokument](../../../images/tutorial-sharingdata-recent-document.png)

### <a name="add-the-second-web-part"></a><span data-ttu-id="4a1b8-162">Hinzufügen des zweiten Webparts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-162">Add the Second Web Part</span></span>

<span data-ttu-id="4a1b8-163">Nun fügen wir dem Projekt ein zweites Webpart hinzu, um zu veranschaulichen, wie Webparts Daten gemeinsam verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-163">To illustrate sharing data between web parts, add a second web part to the project.</span></span>

<span data-ttu-id="4a1b8-164">Führen Sie über eine Eingabeaufforderung im Projektordner den SharePoint Framework-Yeoman-Generator aus.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-164">Using a command prompt in the project folder, run the SharePoint Framework Yeoman generator.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="4a1b8-165">Es werden verschiedene Eingabeaufforderungen angezeigt. Geben Sie jeweils die folgenden Werte an:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-165">When prompted, enter the following values:</span></span>


- <span data-ttu-id="4a1b8-166">**WebPart** als den Typ von zu erstellender clientseitiger Komponente</span><span class="sxs-lookup"><span data-stu-id="4a1b8-166">**WebPart** as the type of client-side component to create.</span></span>
- <span data-ttu-id="4a1b8-167">**Recent document** als Namen des Webparts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-167">**Recent document** as your web part name.</span></span>
- <span data-ttu-id="4a1b8-168">**Zeigt Informationen zu dem zuletzt geänderten Dokumentinformation** als Beschreibung des Webparts.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-168">**Shows information about the most recently modified document** as your web part description.</span></span>

![SharePoint Framework-Yeoman-Generator mit Informationen zum Erstellen eines Gerüsts für das zweite Webpart](../../../images/tutorial-sharingdata-yo-sharepoint-recent-document.png)

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="4a1b8-170">Entfernen der Standardeigenschaft _description_</span><span class="sxs-lookup"><span data-stu-id="4a1b8-170">Remove the Standard _description_ Property</span></span>

<span data-ttu-id="4a1b8-p110">Im ersten Schritt entfernen Sie die Eigenschaft `description` aus der Schnittstelle `IRecentDocumentWebPartProps`. Öffnen Sie hierzu im Code-Editor die Datei **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p110">Start by removing the `description` property from the `IRecentDocumentWebPartProps` interface. In the code editor, open the **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts** file and paste the following code:</span></span>

```ts
export interface IRecentDocumentWebPartProps {
}
```

<span data-ttu-id="4a1b8-p111">Entfernen Sie die Standardeigenschaft `description` aus dem Webpartmanifest. Öffnen Sie hierzu die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json**, und entfernen Sie aus der Eigenschaft `properties` die Eigenschaft `description`:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p111">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

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

<span data-ttu-id="4a1b8-p112">Entfernen Sie nun die Standardeigenschaft `description` aus dem Eigenschaftenbereich des Webparts. Öffnen Sie hierzu im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**, und ersetzen Sie die Methode `render` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p112">Finally, remove the standard `description` property from the web part property pane. In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Replace its `render` method with the following code:</span></span>

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

<span data-ttu-id="4a1b8-178">Im nächsten Schritt ersetzen Sie die Methode `getPropertyPaneConfiguration` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-178">Next, replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

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

### <a name="reuse-the-idocument-and-idocumentactivity-interfaces"></a><span data-ttu-id="4a1b8-179">Wiederverwenden der Schnittstellen _IDocument_ und _IDocumentActivity_</span><span class="sxs-lookup"><span data-stu-id="4a1b8-179">Reuse the _IDocument_ and _IDocumentActivity_ Interfaces</span></span>

<span data-ttu-id="4a1b8-p113">Das Webpart „Recent document“ zeigt Informationen zu dem zuletzt geänderten Dokument an, tut das jedoch anders als das Webpart „Zuletzt verwendete Dokumente“. Die Datenstruktur, die die Dokumente repräsentiert, ist bei beiden Webparts jedoch dieselbe. Statt die Schnittstellen `IDocument` und `IDocumentActivity` zu duplizieren, können Sie sie einmal implementieren und im zweiten Webpart wiederverwenden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p113">The Recent document web part displays information about the most recently modified document in a different way than the Recent documents web part, but both web parts use the same data structure representing a document. Instead of duplicating the `IDocument` and `IDocumentActivity` interfaces, you can reuse them across both web parts.</span></span>

<span data-ttu-id="4a1b8-182">Aktivieren Sie in Visual Studio Code das Explorer-Fenster aus dem Ordner **./src/webparts/recentDocuments**, und verschieben Sie die Dateien **IDocument.ts** und **IDocumentActivity.ts** eine Ebene nach oben zum Ordner **./src/webparts**.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-182">In Visual Studio Code, activate the Explorer pane, and from the **./src/webparts/recentDocuments** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files one level up, to the **./src/webparts** folder.</span></span>

![Explorer-Fenster in Visual Studio Code mit den Dateien „IDocument.ts“ und „IDocumentActivity.ts“ (hervorgehoben)](../../../images/tutorial-sharingdata-interfaces.png)

#### <a name="update-references-to-the-moved-files"></a><span data-ttu-id="4a1b8-184">Aktualisieren der Verweise auf die verschobenen Dateien</span><span class="sxs-lookup"><span data-stu-id="4a1b8-184">Update References to the Moved Files</span></span>

<span data-ttu-id="4a1b8-185">Da Sie die Dateien an einen anderen Speicherort innerhalb Ihres Projekts verschoben haben, müssen Sie überall dort, wo die Dateien referenziert werden, den Pfad entsprechend aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-185">Having moved the files to another location in your project, you need to update the paths where they're referenced.</span></span>

<span data-ttu-id="4a1b8-186">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-186">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="4a1b8-187">Öffnen Sie nun die Datei **./src/webparts/recentDocuments/components/RecentDocuments.tsx**, und aktualisieren Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-187">Next, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and update the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../IDocument';
```

<span data-ttu-id="4a1b8-188">Öffnen Sie anschließend die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**, und aktualisieren Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-188">Finally, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file and update the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../IDocument';
```

### <a name="show-the-most-recent-document-in-the-recentdocument-react-component"></a><span data-ttu-id="4a1b8-189">Anzeigen des zuletzt verwendeten Dokuments in der React-Komponente „RecentDocument“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-189">Show the Most Recent Document in the RecentDocument React Component</span></span>

<span data-ttu-id="4a1b8-p114">Fügen Sie die Eigenschaft `document` der Schnittstelle `IRecentDocumentProps` hinzu. Öffnen Sie hierzu im Code-Editor die Datei **./src/webparts/recentDocument/components/IRecentDocumentProps.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p114">Add the `document` property to the `IRecentDocumentProps` interface. In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file, and paste the following code:</span></span>

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

<span data-ttu-id="4a1b8-192">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/components/RecentDocument.tsx**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-192">In the code editor, open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file and paste the following code:</span></span>

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

<span data-ttu-id="4a1b8-193">Die React-Komponente `RecentDocument` verwendet die Informationen zu dem in der Eigenschaft `document` übergebenen zuletzt geänderten Dokument zum Rendern einer Office UI Fabric-Dokumentkarte.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-193">The `RecentDocument` React component uses the information about the most recently modified document passed in the `document` property and uses it to render an Office UI Fabric Document Card.</span></span>

### <a name="load-the-information-about-the-recent-document"></a><span data-ttu-id="4a1b8-194">Laden der Informationen zu dem zuletzt verwendeten Dokument</span><span class="sxs-lookup"><span data-stu-id="4a1b8-194">Load the Information About the Recent Document</span></span>

<span data-ttu-id="4a1b8-p115">In diesem Beispiel werden die Informationen zu dem zuletzt geänderten Dokument aus einem statischen Dataset geladen.  Sie können die Implementierung jedoch auch mühelos so abändern, dass die Daten stattdessen aus einer SharePoint-Dokumentbibliothek geladen werden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p115">In this example, the information about the most recently modified document is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

<span data-ttu-id="4a1b8-p116">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Fügen Sie eine Importanweisung für die Schnittstelle `IDocument` unterhalb der anderen Importanweisungen am Anfang der Datei ein. Verwenden Sie hierzu den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p116">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Add an import statement for the `IDocument` interface under the other import statements at the top of the file using the following code:</span></span>

```ts
import { IDocument } from '../IDocument';
```

<span data-ttu-id="4a1b8-199">Fügen Sie in der Klasse `RecentDocumentWebPart` eine neue private Variable mit dem Namen `document` ein. Verwenden Sie hierzu den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-199">In the `RecentDocumentWebPart` class, add a new private variable named `document` using the following code:</span></span>

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

<span data-ttu-id="4a1b8-200">Ändern Sie die Methode `render` so, dass die Informationen zu dem zuletzt geänderten Dokument geladen und gerendert werden:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-200">Change the `render` method to load and render the information about the most recently modified document:</span></span>

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

<span data-ttu-id="4a1b8-201">Überprüfen Sie nun, ob das Webpart korrekt funktioniert und Informationen zu dem zuletzt geänderten Dokument anzeigt. Führen Sie dazu den folgenden Befehl über eine Eingabeaufforderung in Ihrem Projektordner aus:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-201">Verify that the web part is working correctly and shows information about the most recently modified document, by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

<span data-ttu-id="4a1b8-202">Fügen Sie in SharePoint Workbench das Webpart „Recent document“ zur Canvas hinzu.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-202">In the SharePoint workbench add the Recent document web part to the canvas.</span></span>

![Webpart „Recent document“ mit einer Dokumentkarte mit Informationen zu dem zuletzt geänderten Dokument](../../../images/tutorial-sharingdata-recent-document.png)

<span data-ttu-id="4a1b8-p117">Diese Implementierung ist ein typisches Beispiel für zwei Webparts, die unabhängig voneinander entwickelt werden. Würden beide Webparts auf derselben Seite platziert und würden beide Webparts Daten aus SharePoint laden, würden sie zwei separate Anforderungen ausführen, um einander ähnliche Informationen abzurufen. Angenommen, Sie müssten zu einem späteren Zeitpunkt die Quelle für die Informationen zu den zuletzt geänderten Dokumenten ändern. Dann müssten Sie beide Webparts aktualisieren. Damit die Seite schneller lädt und der Webpartcode einfacher zu pflegen ist, können Sie die zum Abrufen der Daten genutzte Logik zentralisieren und einmal abgerufene Daten für beide Webparts verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p117">The current implementation is a typical example of two web parts being developed independently. If they were both placed on the same page and were loading data from SharePoint, they would execute two separate requests to retrieve similar information. If, at some point, you had to change where the information about the recently modified documents is loaded from, you would have to update both web parts. To improve the performance of loading the page and simplify maintaining the web part code, you can centralize the logic of retrieving the data and make the once retrieved data available to both web parts.</span></span>

## <a name="centralize-loading-data"></a><span data-ttu-id="4a1b8-208">Zentralisieren des Ladens von Daten</span><span class="sxs-lookup"><span data-stu-id="4a1b8-208">Centralize Loading Data</span></span>

<span data-ttu-id="4a1b8-209">Zur Zentralisierung des Ladens der Informationen zu den zuletzt geänderten Dokumenten erstellen Sie einen Dienst, der von beiden Webparts referenziert wird.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-209">To centralize loading the information about recently modified documents, build a service that will be referenced by both web parts.</span></span>

### <a name="move-the-data-model-interfaces"></a><span data-ttu-id="4a1b8-210">Verschieben der Datenmodellschnittstellen</span><span class="sxs-lookup"><span data-stu-id="4a1b8-210">Move the Data Model Interfaces</span></span>

<span data-ttu-id="4a1b8-p118">Erstellen Sie im Projektordner den Ordnerpfad **./src/services/documentsService**. Verschieben Sie die Dateien **IDocument.ts** und **IDocumentActivity.ts** aus dem Ordner **./src/webparts** in den Ordner **./src/services/documentsService**.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p118">In the project folder create the **./src/services/documentsService** folder path. From the **./src/webparts** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files to the **./src/services/documentsService** folder.</span></span>

![Dateien „IDocument.ts“ und „IDocumentActivity.ts“ im Explorer-Fenster in Visual Studio Code](../../../images/tutorial-sharingdata-interfaces-documentsservice.png)

### <a name="build-the-data-access-service"></a><span data-ttu-id="4a1b8-214">Erstellen des Datenzugriffsdiensts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-214">Build the Data Access Service</span></span>

<span data-ttu-id="4a1b8-215">Erstellen Sie im Ordner **./src/services/documentsService** eine neue Datei namens **DocumentsService.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-215">In the **./src/services/documentsService** folder, create a new file named **DocumentsService.ts** and paste the following code:</span></span>

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

<span data-ttu-id="4a1b8-p119">Die Klasse `DocumentsService` ist ein Beispieldienst, der Informationen zu den zuletzt verwendeten Dokumenten lädt. In diesem Beispiel wird ein statisches Dataset verwendet. Sie können die Implementierung jedoch mühelos so abändern, dass die Daten aus einer SharePoint-Dokumentbibliothek geladen werden. Zu diesem Zeitpunkt stellt die Klasse `DocumentsService` eine zentrale Schnittstelle bereit, über die alle Webparts auf ihre Daten zugreifen können. Sie speichert die zuvor geladenen Daten jedoch nicht. Diese Funktion wird im weiteren Verlauf dieses Tutorials implementiert.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p119">The `DocumentsService` class is a sample service that loads information about recent documents. In this example, it uses a static data set, but you could easily change its implementation to load its data from a SharePoint document library. At this stage, the `DocumentsService` class offers a centralized point for all web parts to access their data, but it doesn't store the previously loaded data. You will implement that later in this tutorial.</span></span>

### <a name="create-a-barrel-for-the-service-files"></a><span data-ttu-id="4a1b8-220">Erstellen eines Barrels für die Dienstdateien</span><span class="sxs-lookup"><span data-stu-id="4a1b8-220">Create a Barrel for the Service Files</span></span>

<span data-ttu-id="4a1b8-p120">Wenn Sie Dateien in einem Projekt referenzieren, verweisen Sie auf ihren relativen Pfad. Jedes Mal, wenn sich dieser Pfad ändert, müssen Sie alle Verweise auf die betreffende Datei aktualisieren. Gerade am Anfang eines Projekts werden solche Änderungen wahrscheinlich sehr häufig notwendig sein, da Sie kontinuierlich neue Elemente hinzufügen und die endgültige Projektstruktur noch nicht feststeht. Um häufige Änderungen an den Dateiverweisen innerhalb eines Projekts zu vermeiden, können Sie Barrels nutzen.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p120">When referencing files in a project you point to their relative path. Whenever that path changes, you have to update all references to the particular file. Such changes are very likely at the beginning of the project when the different elements are being added and the final project structure is unclear. To avoid frequent changes to file references in a project you can use barrels.</span></span>

<span data-ttu-id="4a1b8-p121">Bei einem Barrel handelt es sich um einen Container, der mehrere exportierte Objekte kombiniert. Mithilfe von Barrels können Sie den genauen Speicherort der Dateien eines Projektes und die Projektelemente, die die Dateien verwenden, voneinander abstrahieren.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p121">A barrel is a container that combines a number of exported objects. By using barrels you can abstract away the exact location of files from other elements in the project using them.</span></span>

<span data-ttu-id="4a1b8-227">Erstellen Sie im Ordner **./src/services/documentsService** eine neue Datei mit dem Namen **index.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-227">In the **./src/services/documentsService** folder create a new file named **index.ts** and paste the following code:</span></span>

```ts
export { IDocument } from './IDocument';
export { IDocumentActivity } from './IDocumentActivity';
export { DocumentsService } from './DocumentsService';
```

<span data-ttu-id="4a1b8-p122">Sobald Sie dieses Barrel definiert haben, können andere Elemente in Ihrem Projekt alle exportierten Typen über den relativen Pfad zum Ordner **./src/services/documentsService** referenzieren statt über den exakten Pfad zu den einzelnen Dateien. Die Schnittstelle `IDocument` kann dann beispielsweise wie folgt referenziert werden:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p122">With this barrel defined, other elements in the project can reference any of the exported types using the relative path to the **./src/services/documentsService** folder instead of the exact path to the individual files. For example the `IDocument` interface can be referenced like this:</span></span>

```ts
import { IDocument } from '../services/documentsService';
```

<span data-ttu-id="4a1b8-230">Ein Verweis wie der unten gezeigte ist nicht mehr nötig:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-230">instead of:</span></span>

```ts
import { IDocument } from '../services/documentsService/IDocument.ts';
```

<span data-ttu-id="4a1b8-p123">Sollten Sie sich zu einem späteren Zeitpunkt dazu entscheiden, die Datei **IDocument.ts** in einen Unterordner zu verschieben oder verschiedene Dateien zusammenzuführen, müssten Sie lediglich den Pfad in der Barreldefinition (**./src/services/documentsService/index.ts**) ändern. Alle Elemente in Ihrem Projekt hingegen könnten weiterhin denselben relativen Pfad zum Ordner **documentsService** verwenden, um die Schnittstelle `IDocument` zu referenzieren.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p123">If at some point you decided that it's better to move the **IDocument.ts** file to a subfolder or merge a few files together, the only thing that you would change is the path in the barrel definition (**./src/services/documentsService/index.ts**). All elements in the project could still use the exact same relative path to the **documentsService** folder to reference the `IDocument` interface.</span></span>

### <a name="update-references-to-the-moved-files-to-use-the-barrel"></a><span data-ttu-id="4a1b8-233">Aktualisieren der Verweise auf die verschobenen Dateien zur Verwendung das Barrels</span><span class="sxs-lookup"><span data-stu-id="4a1b8-233">Update References to the Moved Files to Use the Barrel</span></span>

<span data-ttu-id="4a1b8-p124">Da Sie die Dateien **IDocument.ts** und **IDocumentActivity.ts** an einen anderen Speicherort verschoben haben, müssen Sie alle Verweise auf diese Dateien aktualisieren. Dank des Barrels ist das nur noch dieses eine Mal notwendig.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p124">As you have moved the **IDocument.ts** and **IDocumentActivity.ts** files to another location, you have to update their references. Thanks to the barrel, this will be the last time that you will have to do this.</span></span>

#### <a name="update-references-in-the-recent-documents-web-part"></a><span data-ttu-id="4a1b8-236">Aktualisieren der Verweise im Webpart „Zuletzt verwendete Dokumente“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-236">Update References in the Recent Documents Web Part</span></span>

<span data-ttu-id="4a1b8-237">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts**, und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-237">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="4a1b8-238">Öffnen Sie nun die Datei **./src/webparts/recentDocuments/components/RecentDocuments.tsx**, und aktualisieren Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-238">Next, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';
```

<span data-ttu-id="4a1b8-239">Öffnen Sie anschließend die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**, und aktualisieren Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-239">Then, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../services/documentsService';
```

#### <a name="update-references-in-the-recent-document-web-part"></a><span data-ttu-id="4a1b8-240">Aktualisieren der Verweise im Webpart „Recent document“</span><span class="sxs-lookup"><span data-stu-id="4a1b8-240">Update References in the Recent Document Web Part</span></span>

<span data-ttu-id="4a1b8-241">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/components/IRecentDocumentProps.ts**, und ändern Sie den Code wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-241">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

<span data-ttu-id="4a1b8-242">Öffnen Sie nun die Datei **./src/webparts/recentDocument/components/RecentDocument.tsx**, und ändern Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-242">Next, open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';
```

<span data-ttu-id="4a1b8-243">Öffnen Sie anschließend die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.t**, und ändern Sie die `import`-Anweisung der Schnittstelle `IDocument` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-243">Then, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../services/documentsService';
```

<span data-ttu-id="4a1b8-244">Führen Sie den folgenden Befehl über eine Eingabeaufforderung in Ihrem Projektordner aus, um zu überprüfen, ob Ihre Änderungen wie erwartet funktionieren:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-244">Verify that your changes work as expected, by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Webparts „Recent document“ und „Zuletzt verwendete Dokumente“ mit Informationen zu den zuletzt geänderten Dokumenten](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="load-web-part-data-using-the-data-service"></a><span data-ttu-id="4a1b8-246">Laden von Webpartdaten mithilfe des Datendiensts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-246">Load Web Part Data Using the Data Service</span></span>

<span data-ttu-id="4a1b8-247">Der Datendienst ist nun einsatzbereit. Jetzt gestalten Sie beide Webparts so um, dass sie ihre Daten über den Datendienst laden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-247">With the data service ready, the next step is to refactor both web parts to use the data service to load their data.</span></span>

#### <a name="load-information-about-the-recently-modified-documents"></a><span data-ttu-id="4a1b8-248">Laden der Informationen zu den zuletzt geänderten Dokumenten</span><span class="sxs-lookup"><span data-stu-id="4a1b8-248">Load Information About the Recently Modified Documents</span></span>

<span data-ttu-id="4a1b8-p125">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Ergänzen Sie die `import`-Anweisung, die die Schnittstelle `IDocument` referenziert, wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p125">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

<span data-ttu-id="4a1b8-251">Aktualisieren Sie anschließend die Methode `render` mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-251">Next, update the `render` method using the following code:</span></span>

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

#### <a name="load-information-about-the-most-recently-modified-document"></a><span data-ttu-id="4a1b8-252">Laden der Informationen zu dem zuletzt geänderten Dokument</span><span class="sxs-lookup"><span data-stu-id="4a1b8-252">Load Information About the Most Recently Modified Document</span></span>

<span data-ttu-id="4a1b8-p126">Öffnen Sie im Code-Editor die Datei **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Ergänzen Sie die `import`-Anweisung, die die Schnittstelle `IDocument` referenziert, wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p126">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

<span data-ttu-id="4a1b8-255">Aktualisieren Sie anschließend die Methode `render` mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-255">Next, update the `render` method using the following code:</span></span>

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

<span data-ttu-id="4a1b8-256">Führen Sie über eine Eingabeaufforderung im Projektordner den folgenden Befehl aus, um sich zu vergewissern, dass beide Webparts korrekt funktionieren:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-256">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Webparts „Recent document“ und „Zuletzt verwendete Dokumente“ mit Informationen zu den zuletzt geänderten Dokumenten](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="share-data-between-web-parts"></a><span data-ttu-id="4a1b8-258">Gemeinsame Verwendung von Daten zwischen Webparts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-258">Share Data Between Web Parts</span></span>

<span data-ttu-id="4a1b8-259">Da nun beide Webparts den Datendienst zum Laden der Daten verwenden, besteht der nächste Schritt darin, den Datendienst so zu erweitern, dass dieser die Daten nur einmal lädt und diese für beide Webparts wiederverwendet.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-259">Now that both web parts use the data service to load their data, the next step is to extend the data service so that it loads the data only once and reuses it for both web parts.</span></span>

<span data-ttu-id="4a1b8-260">Öffnen Sie im Code-Editor die Datei **./src/services/documentsService/DocumentsService.ts**, und fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-260">In the code editor, open the **./src/services/documentsService/DocumentsService.ts** file and paste the following code:</span></span>

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

<span data-ttu-id="4a1b8-p127">Sobald ein Webpart erstmals den Datendienst aufruft, um Daten zu laden, setzt der Dienst die globale Variable `loadingData` auf `true`. So wird angezeigt, dass aktuell Daten geladen werden. Das ist erforderlich, damit Daten nicht mehrfach geladen werden, beispielsweise wenn ein anderes Webpart seine Daten laden möchte, bevor die ursprüngliche Anforderung zum Laden der Daten abgeschlossen wurde. In unserem Beispiel werden die Daten aus einem statischen Dataset geladen. Sie können die Implementierung jedoch mühelos so abändern, dass die Daten aus einer SharePoint-Dokumentbibliothek geladen werden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p127">The first time a web part calls the data service to load its data, the service will set the `loadingData` global variable to `true`. This indicates that data is currently being loaded. This is required to prevent data from being loaded multiple times should, for instance, another web part request loading its data while the initial request to load data has not yet completed. In this example, the data is loaded from a static data set, but you could easily change the implementation to load the data from a SharePoint document library.</span></span>

<span data-ttu-id="4a1b8-p128">Nachdem die Daten geladen wurden, werden sie in der globalen Variable `loadedData` gespeichert. Der Wert der Variable `loadingData` wird auf `false` festgelegt, und die Zusage wird mit den abgerufenen Daten aufgelöst. Bei der nächsten Datenanforderung durch ein Webpart gibt der Datendienst die zuvor bereits geladenen Daten zurück. Alle zusätzlichen Anforderungen an die Remote-APIs fallen dadurch weg.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-p128">Once the data is loaded, it is stored in the `loadedData` global variable. The value of the `loadingData` variable is set to `false` and the promise is resolved with the retrieved data. The next time a web part requests its data, the data service will return the data loaded previously eliminating any additional requests to the remote APIs.</span></span>

<span data-ttu-id="4a1b8-268">Führen Sie über eine Eingabeaufforderung im Projektordner den folgenden Befehl aus, um sich zu vergewissern, dass beide Webparts korrekt funktionieren:</span><span class="sxs-lookup"><span data-stu-id="4a1b8-268">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Webparts „Recent document“ und „Zuletzt verwendete Dokumente“ mit Informationen zu den zuletzt geänderten Dokumenten](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

<span data-ttu-id="4a1b8-270">Wenn Sie den verschiedenen Abschnitten der Methode `DocumentsService.ensureRecentDocuments` Protokollierungsanweisungen hinzufügen, können Sie nachverfolgen, wie die Daten einmalig geladen und anschließend für das zweite Webpart wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="4a1b8-270">If you were to add logging statements in the different parts of the `DocumentsService.ensureRecentDocuments` method, you would see that the data is loaded once and reused for the second web part!</span></span>

![Entwicklerkonsole mit verschiedenen Protokollierungsmeldungen in Microsoft Edge](../../../images/tutorial-sharingdata-console-log.png)

## <a name="see-also"></a><span data-ttu-id="4a1b8-272">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="4a1b8-272">See Also</span></span>

- [<span data-ttu-id="4a1b8-273">Gemeinsame Verwendung von Daten zwischen clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="4a1b8-273">Share Data Between Client-Side Web Parts</span></span>](./share-data-between-web-parts.md)