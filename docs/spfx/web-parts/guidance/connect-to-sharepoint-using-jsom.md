---
title: Verbinden mit SharePoint mithilfe des JavaScript-Objektmodells (JSOM)
description: "Verwendung von SharePoint JSOM beim Erstellen von Lösungen auf dem SharePoint Framework."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 9baa9eff13769a93239eb56bdda50139ecf391a4
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="connect-to-sharepoint-using-the-javascript-object-model-jsom"></a><span data-ttu-id="501cb-103">Verbinden mit SharePoint mithilfe des JavaScript-Objektmodells (JSOM)</span><span class="sxs-lookup"><span data-stu-id="501cb-103">Connect to SharePoint using the JavaScript Object Model (JSOM)</span></span>

<span data-ttu-id="501cb-104">In der Vergangenheit haben Sie vielleicht beim Erstellen von SharePoint-Anpassungen, das SharePoint JavaScript-Objektmodell (JSOM) zur Kommunikation mit SharePoint verwendet.</span><span class="sxs-lookup"><span data-stu-id="501cb-104">In the past, when building SharePoint customizations, you might have used the SharePoint JavaScript Object Model (JSOM) to communicate with SharePoint. This article illustrates how to use SharePoint JSOM when building solutions on the SharePoint Framework.</span></span> <span data-ttu-id="501cb-105">Dies ist nicht mehr der empfohlene Pfad (siehe [Überlegungen](#considerations) weiter unten in diesem Artikel), aber es gibt noch gültige Anwendungsfälle wie z. B. die Codemigration.</span><span class="sxs-lookup"><span data-stu-id="501cb-105">This is no longer the recommended path (see [Considerations](#considerations) later in this article), but there are still valid use cases such as code migration.</span></span> 

<span data-ttu-id="501cb-106">Um SharePoint JSOM in Ihrer SharePoint Framework-Komponente zu verwenden, müssen Sie zuerst darauf verweisen.</span><span class="sxs-lookup"><span data-stu-id="501cb-106">To use SharePoint JSOM in your SharePoint Framework component, you must first reference it.</span></span> <span data-ttu-id="501cb-107">Bisher stand es bereits auf der Seite zur Verwendung zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="501cb-107">In the past it was already available on the page for you to use.</span></span> <span data-ttu-id="501cb-108">Es muss in SharePoint Framework explizit geladen werden.</span><span class="sxs-lookup"><span data-stu-id="501cb-108">In the SharePoint Framework, it has to be explicitly loaded.</span></span>

<span data-ttu-id="501cb-109">Es gibt zwei Methoden, um in SharePoint Framework auf SharePoint JSOM zu verweisen:</span><span class="sxs-lookup"><span data-stu-id="501cb-109">There are two ways to reference SharePoint JSOM in the SharePoint Framework:</span></span> 
- <span data-ttu-id="501cb-110">**Deklarativ** – über die Konfiguration</span><span class="sxs-lookup"><span data-stu-id="501cb-110">**Declarative** - through configuration</span></span>
- <span data-ttu-id="501cb-111">**Imperativ** – über Code</span><span class="sxs-lookup"><span data-stu-id="501cb-111">**Imperative** - through code</span></span>

<span data-ttu-id="501cb-112">Jeder dieser Ansätze hat seine Vor- und Nachteile, die Sie unbedingt kennen sollten.</span><span class="sxs-lookup"><span data-stu-id="501cb-112">Each of these approaches have advantages and disadvantages and it's important for you to understand each of them.</span></span>

> [!NOTE] 
> <span data-ttu-id="501cb-113">Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für das SharePoint-Framework einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="501cb-113">Before following the steps in this article, be sure to [set up your SharePoint Framework development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="501cb-114">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="501cb-114">Create a new project</span></span>

1. <span data-ttu-id="501cb-115">Erstellen Sie in der Konsole einen neuen Ordnern für Ihr Projekt:</span><span class="sxs-lookup"><span data-stu-id="501cb-115">From the console, create a new folder for your project:</span></span>

  ```sh
  md react-sharepointlists
  ```

2. <span data-ttu-id="501cb-116">Wechseln Sie zum Projektordner:</span><span class="sxs-lookup"><span data-stu-id="501cb-116">Go to the project folder:</span></span>

  ```sh
  cd react-sharepointlists
  ```

3. <span data-ttu-id="501cb-117">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="501cb-117">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="501cb-118">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="501cb-118">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="501cb-119">**react-sharepointlists** als Lösungsname.</span><span class="sxs-lookup"><span data-stu-id="501cb-119">**react-sharepointlists** as your solution name.</span></span>
  - <span data-ttu-id="501cb-120">Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="501cb-120">Choose **Webpart** as the client-side component type to be created.</span></span>
  - <span data-ttu-id="501cb-121">**Use the currecnt folder** als Speicherort für die Dateien.</span><span class="sxs-lookup"><span data-stu-id="501cb-121">**Use the current folder** for the location to place the files.</span></span>
  - <span data-ttu-id="501cb-122">**React** als Ausgangs-Framework für die Webpart-Erstellung.</span><span class="sxs-lookup"><span data-stu-id="501cb-122">**React** as the starting framework to build the web part.</span></span>
  - <span data-ttu-id="501cb-123">**SharePoint-Listen** als Webpartname.</span><span class="sxs-lookup"><span data-stu-id="501cb-123">**SharePoint lists** as your web part name.</span></span>
  - <span data-ttu-id="501cb-124">**Zeigt die Namen von Listen auf der aktuellen Website an** als Webpartbeschreibung.</span><span class="sxs-lookup"><span data-stu-id="501cb-124">**Shows names of lists in the current site** as your web part description.</span></span>

  ![Der SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/tutorial-spjsom-yo-sharepoint.png)

5. <span data-ttu-id="501cb-126">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="501cb-126">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="501cb-127">Öffnen Sie den Projektordner im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="501cb-127">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="501cb-128">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="501cb-128">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor you prefer.</span></span>

  ![Das SharePoint-Framework-Projekt in Visual Studio-Code](../../../images/tutorial-spjsom-vscode.png)

7. <span data-ttu-id="501cb-130">Gehen Sie folgendermaßen vor, um das Verzeichnis in Visual Studio Code von der Konsole aus zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="501cb-130">To open the directory in Visual Studio Code, from the console type:</span></span>

  ```sh
  code .
  ```


## <a name="reference-jsom-declaratively"></a><span data-ttu-id="501cb-131">Deklaratives Referenzieren von JSOM</span><span class="sxs-lookup"><span data-stu-id="501cb-131">Reference JSOM declaratively</span></span>

### <a name="register-the-sharepoint-jsom-api-as-external-scripts"></a><span data-ttu-id="501cb-132">Registrieren der SharePoint JSOM-API als externe Skripts</span><span class="sxs-lookup"><span data-stu-id="501cb-132">Register SharePoint JSOM API as external scripts</span></span>

<span data-ttu-id="501cb-133">Beim deklarativen Verweisen auf JSOM besteht der erste Schritt darin, die SharePoint JSOM-API als externe Skripts innerhalb Ihres SharePoint Framework-Projekts zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="501cb-133">When referencing JSOM declaratively, the first step is to register the SharePoint JSOM API as external scripts within your SharePoint Framework project. In your code editor, open the ./config/config.json file and add the following to the externals section:</span></span>

1. <span data-ttu-id="501cb-134">Öffnen Sie im Code-Editor die Datei **./config/config.json**, und fügen Sie dem Abschnitt **externals** Folgendes hinzu:</span><span class="sxs-lookup"><span data-stu-id="501cb-134">When referencing JSOM declaratively, the first step is to register the SharePoint JSOM API as external scripts within your SharePoint Framework project. In your code editor, open the **./config/config.json** file and add the following to the **externals** section:</span></span>

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

  <br/>

  <span data-ttu-id="501cb-135">Jeder Eintrag verweist auf eine andere Skriptdatei, die Ihnen zusammen die Verwendung von SharePoint JSOM in der SPFx-Komponente ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="501cb-135">Each of the entries points to different script files that together allow you to use SharePoint JSOM in your SPFx component.</span></span> <span data-ttu-id="501cb-136">Alle diese Skripts werden als Nicht-Modul-Skripts verteilt.</span><span class="sxs-lookup"><span data-stu-id="501cb-136">All of these scripts are distributed as non-module scripts.</span></span> <span data-ttu-id="501cb-137">Deshalb erfordert jeder Registrierungseintrag eine URL (angegeben mit der `path`-Eigenschaft) und den vom Skript verwendeten Namen (bereitgestellt in der `globalName`-Eigenschaft).</span><span class="sxs-lookup"><span data-stu-id="501cb-137">This is why each registration entry requires a URL, (specified using the `path` property) and the name used by the script (provided in the `globalName` property).</span></span> <span data-ttu-id="501cb-138">Um sicherzustellen, dass diese Skripts in der richtigen Reihenfolge laden, werden die Abhängigkeiten zwischen diesen Skripts mit der `globalDependencies`-Eigenschaft angegeben.</span><span class="sxs-lookup"><span data-stu-id="501cb-138">To ensure that these scripts load in the right order, the dependencies between these scripts are specified by using the `globalDependencies` property.</span></span>

  <span data-ttu-id="501cb-139">In Abhängigkeit von der JSOM-Funktionalität, die Sie verwenden, müssen möglicherweise weitere Skripts hinzugefügt werden (z. B.sp.taxonomy.js).</span><span class="sxs-lookup"><span data-stu-id="501cb-139">Additional scripts may need to be added depending on the JSOM functionality you are using (e.g. sp.taxonomy.js).</span></span>

### <a name="install-typescript-typings-for-sharepoint-jsom"></a><span data-ttu-id="501cb-140">Installieren von TypeScript-Eingaben für SharePoint JSOM</span><span class="sxs-lookup"><span data-stu-id="501cb-140">Install TypeScript typings for SharePoint JSOM</span></span>

<span data-ttu-id="501cb-141">Der nächste Schritt besteht darin, TypeScript-Eingaben für SharePoint JSOM zu installieren und zu konfigurieren. So profitieren Sie von den Sicherheitsfunktionen der TypeScript-Typen, wenn Sie mit SharePoint JSOM arbeiten.</span><span class="sxs-lookup"><span data-stu-id="501cb-141">The next step is to install and configure TypeScript typings for SharePoint JSOM. This allows you to benefit from TypeScript's type safety features when working with SharePoint JSOM.</span></span>

1. <span data-ttu-id="501cb-142">Führen Sie den folgenden Befehl in Ihrem Projektverzeichnis von der Konsole aus:</span><span class="sxs-lookup"><span data-stu-id="501cb-142">From the console, execute the following command within your project directory:</span></span>

  ```sh
  npm install @types/microsoft-ajax @types/sharepoint --save-dev
  ```

  <span data-ttu-id="501cb-143">SharePoint JSOM wird nicht als Modul verteilt, Sie können es daher nicht direkt in Ihren Code importieren.</span><span class="sxs-lookup"><span data-stu-id="501cb-143">SharePoint JSOM is not distributed as a module, so you cannot import it directly in your code.</span></span> <span data-ttu-id="501cb-144">Stattdessen müssen Sie die TypeScript-Eingaben global registrieren.</span><span class="sxs-lookup"><span data-stu-id="501cb-144">Instead, you need to register its TypeScript typings globally.</span></span> 

2. <span data-ttu-id="501cb-145">Öffnen Sie im Code-Editor die Datei **./tsconfig.json** und fügen Sie in der `types`-Eigenschaft, gleich hinter dem Eintrag **webpack-env** Verweise auf **microsoft-ajax** and **sharepoint**: hinzu.</span><span class="sxs-lookup"><span data-stu-id="501cb-145">SharePoint JSOM is not distributed as a module and so you cannot import it directly in your code. Instead, you need to register its TypeScript typings globally. In the code editor, open the **./tsconfig.json** file, and in the `types` property, right after the **webpack-env** entry, add references to **microsoft-ajax** and **sharepoint**:</span></span>

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

### <a name="reference-sharepoint-jsom-scripts-in-a-react-component"></a><span data-ttu-id="501cb-146">Referenzieren von SharePoint JSOM-Skripts in einer React-Komponente</span><span class="sxs-lookup"><span data-stu-id="501cb-146">Reference SharePoint JSOM Scripts in a React Component</span></span>

<span data-ttu-id="501cb-147">Um die SharePoint JSOM-Skripts in die SPFx-Komponente zu laden, müssen Sie auf diese im Code der Komponente verweisen.</span><span class="sxs-lookup"><span data-stu-id="501cb-147">To load the SharePoint JSOM scripts in your SPFx component, you have to reference them in the component's code. In this example, you will add the references in a React component where JSOM will be used to communicate with SharePoint.</span></span> <span data-ttu-id="501cb-148">In diesem Beispiel fügen Sie die Verweise in der React-Komponente hinzu, in der JSOM zur Kommunikation mit SharePoint verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="501cb-148">To load the SharePoint JSOM scripts in your SPFx component, you have to reference them in the component's code. In this example, you will add the references in a React component where JSOM will be used to communicate with SharePoint.</span></span>

<span data-ttu-id="501cb-149">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**.</span><span class="sxs-lookup"><span data-stu-id="501cb-149">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing  statements add:</span></span> <span data-ttu-id="501cb-150">Fügen Sie den folgenden Code hinter der letzten `import`-Anweisung ein:</span><span class="sxs-lookup"><span data-stu-id="501cb-150">After the last `import` statement add the following code:</span></span>

```ts
  require('sp-init');
  require('microsoft-ajax');
  require('sp-runtime');
  require('sharepoint');
```

<span data-ttu-id="501cb-151">Da diese Namen den zuvor hinzugefügten externen Verweisen entsprechen, wird SharePoint Framework dieses Skript unter den angegebenen URLs laden.</span><span class="sxs-lookup"><span data-stu-id="501cb-151">These names correspond to the external references you added previously so SharePoint Framework will load these scripts from the specified URLs.</span></span>

<span data-ttu-id="501cb-152">Zur Veranschaulichung, wie SharePoint JSOM zur Kommunikation mit SharePoint beiträgt, rufen Sie die Titel aller SharePoint-Listen ab, die sich auf der aktuellen Website befinden, und geben Sie sie wieder.</span><span class="sxs-lookup"><span data-stu-id="501cb-152">To demonstrate using SharePoint JSOM for communicating with SharePoint, you will retrieve and render the titles of all SharePoint lists located in the current site.</span></span>

### <a name="add-siteurl-to-the-react-components-properties"></a><span data-ttu-id="501cb-153">Hinzufügen von _siteUrl_ zu React-Komponenteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="501cb-153">Add _siteUrl_ to the React Component's Properties</span></span>

<span data-ttu-id="501cb-154">Damit Sie sich mit SharePoint verbinden können, muss die React-Komponente die URL der aktuellen Website kennen.</span><span class="sxs-lookup"><span data-stu-id="501cb-154">To connect to SharePoint, the React component must know the URL of the current site.</span></span> <span data-ttu-id="501cb-155">Die URL ist im übergeordneten Webpart verfügbar und kann über ihre Eigenschaften an die Komponente übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="501cb-155">In order to connect to SharePoint, the React component must know the URL of the current site. That URL is available in the parent web part and can be passed into the component through its properties.</span></span>

1. <span data-ttu-id="501cb-156">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/ISharePointListsProps.ts**, und fügen Sie der Schnittstelle `ISharePointListsProps` die `siteUrl`-Eigenschaft hinzu:</span><span class="sxs-lookup"><span data-stu-id="501cb-156">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** file and to the `siteUrl` interface add the `ISharePointListsProps` property:</span></span>

  ```ts
  export interface ISharePointListsProps {
    description: string;
    siteUrl: string;
  }
  ```

2. <span data-ttu-id="501cb-157">Um die URL der aktuellen Website an die Komponente zu übergeben, öffnen Sie die Datei **./src/webparts/sharePointLists/SharePointListsWebPart.ts** im Code-Editor, und ändern Sie die `render`-Methode in:</span><span class="sxs-lookup"><span data-stu-id="501cb-157">To pass the URL of the current site into the component, open the **./src/webparts/sharePointLists/SharePointListsWebPart.ts** file in the code editor and change the `render` method to:</span></span>

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

### <a name="define-the-react-components-state"></a><span data-ttu-id="501cb-158">Definieren des Status der React-Komponente</span><span class="sxs-lookup"><span data-stu-id="501cb-158">Define the React Component's State</span></span>

<span data-ttu-id="501cb-159">Die React-Komponente lädt Daten aus SharePoint, um sie für den Benutzer wiederzugeben.</span><span class="sxs-lookup"><span data-stu-id="501cb-159">The React component loads data from SharePoint and renders it to the user.</span></span> <span data-ttu-id="501cb-160">Der aktuelle Status der React-Komponente wird mit der state-Schnittstelle modelliert, die wir hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="501cb-160">The React component will load data from SharePoint and render it to the user. The current state of the React component is modeled using a state interface we will add.</span></span>

<span data-ttu-id="501cb-161">Erstellen Sie im Code-Editor im Ordner **./src/webparts/sharePointLists/components** eine neue Daten namens **ISharePointListsState.ts**, und fügen Sie folgenden Inhalt ein:</span><span class="sxs-lookup"><span data-stu-id="501cb-161">In the code editor, in the **./src/webparts/sharePointLists/components** folder, create a new file named **ISharePointListsState.ts** and paste the following contents:</span></span>

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
}
```

### <a name="add-state-to-the-react-component"></a><span data-ttu-id="501cb-162">Hinzufügen des Status zur React-Komponente</span><span class="sxs-lookup"><span data-stu-id="501cb-162">Add state to the React component</span></span>

<span data-ttu-id="501cb-163">Nachdem Sie die Schnittstelle definiert haben, indem Sie die Form des Komponentenstatus beschrieben haben, muss die React-Komponente als Nächstes die state-Schnittstelle verwenden.</span><span class="sxs-lookup"><span data-stu-id="501cb-163">Having defined the interface describing the shape of the component's state, the next step is to have the React component use that state interface.</span></span>

1. <span data-ttu-id="501cb-164">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**.</span><span class="sxs-lookup"><span data-stu-id="501cb-164">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing  statements add:</span></span> <span data-ttu-id="501cb-165">Fügen Sie unter den vorhandenen `import` -Anweisungen Folgendes hinzu:</span><span class="sxs-lookup"><span data-stu-id="501cb-165">Under the existing `import` statements, add:</span></span>

  ```ts
  import { ISharePointListsState } from './ISharePointListsState';
  ```

2. <span data-ttu-id="501cb-166">Im nächsten Schritt ändern Sie die Signatur der `SharePointLists`-Klasse in:</span><span class="sxs-lookup"><span data-stu-id="501cb-166">Next, change the signature of the `SharePointLists` class to:</span></span>

  ```ts
  export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
    // ...
  }
  ```

3. <span data-ttu-id="501cb-167">Fügen Sie in der `SharePointLists`-Klasse einen Konstruktor mit dem Standardstatuswert hinzu:</span><span class="sxs-lookup"><span data-stu-id="501cb-167">In the `SharePointLists` class, add a constructor with the default state value:</span></span>

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

### <a name="load-information-about-sharepoint-lists-from-the-current-site-using-jsom"></a><span data-ttu-id="501cb-168">Herunterladen von Informationen zu SharePoint-Listen von der aktuellen Website mit JSOM</span><span class="sxs-lookup"><span data-stu-id="501cb-168">Load information about SharePoint lists from the current site using JSOM</span></span>

<span data-ttu-id="501cb-169">Das clientseitige Webpart, das in diesem Artikel als Beispiel verwendet wurde, lädt per Klick Informationen zu SharePoint-Listen in die aktuelle Website.</span><span class="sxs-lookup"><span data-stu-id="501cb-169">The sample client-side web part used in this article loads information about SharePoint lists in the current site after clicking a button.</span></span>

  ![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

1. <span data-ttu-id="501cb-171">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**.</span><span class="sxs-lookup"><span data-stu-id="501cb-171">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing  statements add:</span></span> <span data-ttu-id="501cb-172">Fügen Sie in der `SharePointLists`-Klasse eine neue Methode mit dem Namen`getListsTitles` hinzu.</span><span class="sxs-lookup"><span data-stu-id="501cb-172">In the `SharePointLists` class add a new method named `getListsTitles`.</span></span>

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

2. <span data-ttu-id="501cb-173">Um die richtigen Bereichsdefinition der Methode sicherzustellen, binden wir sie im Konstruktor an das Webpart.</span><span class="sxs-lookup"><span data-stu-id="501cb-173">To ensure the correct scoping of the method, we bind it to the web part in the constructor.</span></span> <span data-ttu-id="501cb-174">Verwenden Sie in der `getListsTitles`-Methode SharePoint JSOM, um die Titel der SharePoint-Listen auf die aktuelle Website zu laden:</span><span class="sxs-lookup"><span data-stu-id="501cb-174">In the `getListsTitles` method, use SharePoint JSOM to load the titles of SharePoint lists in the current site:</span></span>

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

  <br/>

<span data-ttu-id="501cb-175">Setzen Sie zunächst den Status der Komponente zurück, um dem Benutzer mitzuteilen, dass die Komponente Informationen aus SharePoint laden wird.</span><span class="sxs-lookup"><span data-stu-id="501cb-175">We start by resetting the component's state to communicate to the user that the component is loading information from SharePoint.</span></span> <span data-ttu-id="501cb-176">Verwenden Sie dann die URL der aktuellen Website, die der Komponente über ihre Eigenschaften übergeben wurde, um einen neuen SharePoint-Kontext zu instanziieren.</span><span class="sxs-lookup"><span data-stu-id="501cb-176">Using the URL of the current site passed to the component through its properties, we instantiate a new SharePoint context.</span></span> <span data-ttu-id="501cb-177">Mit SharePoint JSOM werden Listen von der aktuellen Website geladen.</span><span class="sxs-lookup"><span data-stu-id="501cb-177">Using SharePoint JSOM, we load lists from the current site.</span></span> <span data-ttu-id="501cb-178">Um die Leistung der Anforderung zu optimieren, geben wir an, dass nur die `Title`- Eigenschaft geladen werden sollte.</span><span class="sxs-lookup"><span data-stu-id="501cb-178">To optimize the request for performance, we specify that only the `Title` property should be loaded.</span></span> 

<span data-ttu-id="501cb-179">Im nächsten Schritt führen Sie die Abfrage durch Aufruf der `executeQueryAsync`-Methode und Übergabe zweier Rückruffunktionen aus.</span><span class="sxs-lookup"><span data-stu-id="501cb-179">Next, we execute the query by calling the `executeQueryAsync` method and passing two callback functions.</span></span> <span data-ttu-id="501cb-180">Nach Abschluss der Abfrage durchlaufen Sie die Sammlung der abgerufenen Listen, speichern deren Titel in einem Array und aktualisieren den Status der Komponente.</span><span class="sxs-lookup"><span data-stu-id="501cb-180">After the query is completed, we enumerate through the collection of retrieved lists, store their titles in an array, and update the component's state.</span></span>

### <a name="render-the-titles-of-sharepoint-lists-in-the-current-site"></a><span data-ttu-id="501cb-181">Wiedergeben der Titel von SharePoint-Listen auf der aktuellen Website</span><span class="sxs-lookup"><span data-stu-id="501cb-181">Render the titles of SharePoint lists in the current site</span></span>

<span data-ttu-id="501cb-182">Nachdem Sie die Titel von SharePoint-Listen auf die aktuelle Website geladen haben, müssen Sie sie nur noch in der Komponente wiedergeben.</span><span class="sxs-lookup"><span data-stu-id="501cb-182">Having loaded the titles of SharePoint lists in the current site, the final step is to render them in the component. In the code editor, open the ./src/webparts/sharePointLists/components/SharePointLists.tsx file and update the  method:</span></span> 

1. <span data-ttu-id="501cb-183">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx** und aktualisieren Sie die `render`-Methode:</span><span class="sxs-lookup"><span data-stu-id="501cb-183">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing `render` statements add:</span></span>

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

2. <span data-ttu-id="501cb-p115">Jetzt sollten Sie Ihr Webpart der Seite hinzufügen und die Titel der SharePoint-Listen auf der aktuellen Website anzeigen können. Für eine Überprüfung, dass das Projekt korrekt funktioniert, führen Sie auf der Konsole den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="501cb-p115">At this point, you should be able to add your web part to the page and see the titles of SharePoint lists in the current site. To verify that the project is working correctly, run the following command from the console:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

3. <span data-ttu-id="501cb-186">Da Sie SharePoint JSOM zur Kommunikation mit SharePoint verwenden, müssen Sie das Webpart mit der gehosteten SharePoint-Workbench-Version testen. (Deshalb wird der `--nobrowser`-Parameter angegeben, um zu verhindern, dass die lokale Workbench automatisch geladen wird).</span><span class="sxs-lookup"><span data-stu-id="501cb-186">As you are using SharePoint JSOM to communicate with SharePoint, you have to test the web part using the hosted version of the SharePoint workbench (which is why the `--nobrowser` parameter is specified to prevent the automatic loading of the local workbench).</span></span>

  ![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="501cb-188">Das deklarative Referenzieren von SharePoint JSOM-Skripts als externe Skripts ist bequem und Sie können so den Code übersichtlich halten.</span><span class="sxs-lookup"><span data-stu-id="501cb-188">Referencing SharePoint JSOM scripts declaratively as external scripts is convenient and allows you to keep your code clean.</span></span> <span data-ttu-id="501cb-189">Ein Nachteil besteht aber darin, dass Sie absolute URLs zum Speicherort angeben müssen, aus dem SharePoint JSOM-Skripts geladen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="501cb-189">One disadvantage, however, is that it requires specifying absolute URLs to the location from which SharePoint JSOM scripts should be loaded.</span></span> <span data-ttu-id="501cb-190">Wenn Sie für Entwicklung, Prüfung und Produktion separate SharePoint-Mandanten verwenden, wird zusätzliche Arbeit erforderlich, um die folgenden URLs für die verschiedenen Umgebungen entsprechend zu ändern.</span><span class="sxs-lookup"><span data-stu-id="501cb-190">If you're using separate SharePoint tenants for development, testing, and production, it requires some additional work to change these URLs for the different environments accordingly.</span></span> <span data-ttu-id="501cb-191">In solchen Fällen sollten Sie imperativ mithilfe von [SPComponentLoader](https://docs.microsoft.com/de-DE/javascript/api/sp-application-base) auf JSOM verweisen, um die Skripts im Code der SPFx-Komponenten zu laden.</span><span class="sxs-lookup"><span data-stu-id="501cb-191">In such cases, you may consider referencing JSOM imperatively by using the [SPComponentLoader](https://docs.microsoft.com/de-DE/javascript/api/sp-application-base) to load the scripts in the SPFx component's code.</span></span>

## <a name="reference-jsom-imperatively"></a><span data-ttu-id="501cb-192">Imperatives Verweisen auf JSOM</span><span class="sxs-lookup"><span data-stu-id="501cb-192">Reference JSOM imperatively</span></span>

<span data-ttu-id="501cb-193">Eine weitere Möglichkeit zum Laden von JavaScript-Bibliotheken in SharePoint Framework-Projekten besteht darin, `SPComponentLoader` zu verwenden, eine Dienstprogrammklasse, die mit dem SharePoint Framework bereitgestellt wird und Ihnen helfen soll, die Skripts und andere Ressourcen in die Komponenten zu laden.</span><span class="sxs-lookup"><span data-stu-id="501cb-193">Another way to load JavaScript libraries in SharePoint Framework projects, is by using the `SPComponentLoader`.  is a utility class provided with the SharePoint Framework designed to help you load scripts and other resources in your components. One benefit of using the  over loading scripts declaratively is that it allows you to use server-relative URLs which is more convenient when using different SharePoint tenants for the different stages of your development process.</span></span> <span data-ttu-id="501cb-194">Ein Vorteil der Verwendung von `SPComponentLoader` gegenüber dem deklarativen Laden von Skripts ist, dass Sie serverrelative URLs verwenden können, die bequemer sind, wenn Sie mehrere SharePoint-Mandanten für die verschiedenen Phasen des Entwicklungsprozesses verwenden.</span><span class="sxs-lookup"><span data-stu-id="501cb-194">Another way to load JavaScript libraries in SharePoint Framework projects, is by using the .  is a utility class provided with the SharePoint Framework designed to help you load scripts and other resources in your components. One benefit of using the `SPComponentLoader` over loading scripts declaratively is that it allows you to use server-relative URLs which is more convenient when using different SharePoint tenants for the different stages of your development process.</span></span>

<span data-ttu-id="501cb-195">Für diesen Teil des Lernprogramms passen wir den zuvor im Abschnitt zum deklarativen Verweisen erstellten Code an.</span><span class="sxs-lookup"><span data-stu-id="501cb-195">For this portion of the tutorial, we'll be adjusting the code we created previously in the Declarative section above.</span></span>

### <a name="declarative-reference-cleanup"></a><span data-ttu-id="501cb-196">Bereinigung durch deklaratives Verweisen</span><span class="sxs-lookup"><span data-stu-id="501cb-196">Declarative Reference Cleanup</span></span>

<span data-ttu-id="501cb-197">Wenn Sie die Schritte in den Abschnitten weiter oben zum deklarativen Verweisen befolgt haben, müssen Sie diese Verweise entfernen.</span><span class="sxs-lookup"><span data-stu-id="501cb-197">If you followed the steps in the declarative reference sections above, you'll need to remove those references.</span></span>

1. <span data-ttu-id="501cb-198">Entfernen Sie die vorhandenen externen Skriptverweise.</span><span class="sxs-lookup"><span data-stu-id="501cb-198">Remove the existing external script references.</span></span> <span data-ttu-id="501cb-199">Öffnen Sie dazu im Code-Editor die Datei **config/config.json**, und entfernen Sie aus der **externals**-Eigenschaft alle Einträge:</span><span class="sxs-lookup"><span data-stu-id="501cb-199">First, remove the existing external script references. In the code editor, open the **./config/config.json** file and from the **externals** property, remove all entries:</span></span>

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

  <span data-ttu-id="501cb-200">Wenn SharePoint JSOM-Skripts nicht mehr als externe Skripts registriert sind, können Sie nicht direkt im Code darauf verweisen.</span><span class="sxs-lookup"><span data-stu-id="501cb-200">With the SharePoint JSOM scripts no longer being registered as external scripts, you cannot reference them directly in your code.</span></span> 

2. <span data-ttu-id="501cb-201">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx** und entfernen Sie die `require`-Anweisungen, die auf die verschiedenen SharePoint JSOM-Skripts verweisen.</span><span class="sxs-lookup"><span data-stu-id="501cb-201">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file and remove the `require` statements pointing to the different SharePoint JSOM scripts.</span></span>

### <a name="wait-to-load-data-until-the-jsom-scripts-are-loaded"></a><span data-ttu-id="501cb-202">Warten Sie mit dem Laden der Daten, bis die JSOM-Skripts geladen sind</span><span class="sxs-lookup"><span data-stu-id="501cb-202">Wait to Load Data Until the JSOM Scripts are Loaded</span></span>

<span data-ttu-id="501cb-203">Die Hauptfunktion des clientseitigen Webparts, das wir in diesem Lernprogramm erstellen, hängt von SharePoint JSOM ab.</span><span class="sxs-lookup"><span data-stu-id="501cb-203">The primary functionality of the client-side web part that we are building in this tutorial depends on SharePoint JSOM.</span></span> <span data-ttu-id="501cb-204">In Abhängigkeit von verschiedenen Faktoren kann das Laden dieser Skripts etwas dauern.</span><span class="sxs-lookup"><span data-stu-id="501cb-204">Depending on a number of factors, loading these scripts could take a few moments.</span></span> <span data-ttu-id="501cb-205">Beim Erstellen von SPFx-Komponenten , die JSOM nutzen, sollten Sie dies berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="501cb-205">When building SPFx components that utilize JSOM, you should take that into account.</span></span> <span data-ttu-id="501cb-206">Wenn das Webpart einer Seite hinzugefügt worden ist, sollte es dem Benutzer mitteilen, dass es seine Voraussetzungen lädt, und melden, wann es einsatzbereit ist.</span><span class="sxs-lookup"><span data-stu-id="501cb-206">When added to the page, the web part should communicate to the user that it's loading its prerequisites and should make it clear when it's ready to be used.</span></span> 

<span data-ttu-id="501cb-207">Um dies zu unterstützen, erweitern Sie den Status der React-Komponente um eine zusätzliche Eigenschaft, damit Sie den Ladestatus der JSOM-Skripts verfolgen können.</span><span class="sxs-lookup"><span data-stu-id="501cb-207">To support this, extend the React component's state with an additional property to track the status of loading the JSOM scripts.</span></span>

1. <span data-ttu-id="501cb-208">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/ISharePointListsState.ts**, und fügen Sie folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="501cb-208">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsState.ts** file and paste the following code:</span></span>

  ```ts
  export interface ISharePointListsState {
      listTitles: string[];
      loadingLists: boolean;
      error: string;
      loadingScripts: boolean;
  }
  ```

2. <span data-ttu-id="501cb-209">Fügen Sie die neu hinzugefügte Eigenschaft zu den Statusdefinitionen in der React-Komponente hinzu.</span><span class="sxs-lookup"><span data-stu-id="501cb-209">Add the newly added property to the state definitions in the React component.</span></span> <span data-ttu-id="501cb-210">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**.</span><span class="sxs-lookup"><span data-stu-id="501cb-210">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing  statements add:</span></span> <span data-ttu-id="501cb-211">Aktualisieren Sie den Konstruktor auf den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="501cb-211">Update the constructor to the following code:</span></span>

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

3. <span data-ttu-id="501cb-212">Aktualisieren Sie in der gleichen Datei die `getListsTitles`-Methode auf den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="501cb-212">In the same file, update the `getListsTitles` method to the following code:</span></span>

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

4. <span data-ttu-id="501cb-213">Um dem Benutzer den Ladestatus der SharePoint JSOM-Skripts zu melden, aktualisieren Sie die `render`-Methode auf den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="501cb-213">To communicate the status of loading the SharePoint JSOM scripts to the user, update the `render` method to the following code:</span></span>

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

5. <span data-ttu-id="501cb-214">Wenn der Status der React-Komponente angibt, dass die SharePoint JSOM-Skripts geladen werden, wird ein Platzhalter angezeigt.</span><span class="sxs-lookup"><span data-stu-id="501cb-214">When the React component's state indicates that the SharePoint JSOM scripts are being loaded, it displays a placeholder.</span></span> <span data-ttu-id="501cb-215">Nachdem die Skripts geladen wurden, zeigt das Webpart den erwarteten Inhalt mit der Schaltfläche an, damit der Benutzer die Informationen zu SharePoint-Listen auf die aktuelle Website laden kann.</span><span class="sxs-lookup"><span data-stu-id="501cb-215">When the React component's state indicates that the SharePoint JSOM scripts are being loaded, it will display a placeholder. Once the scripts have been loaded, the web part will display the expected content with the button allowing users to load the information about SharePoint lists in the current site.</span></span>

### <a name="load-sharepoint-jsom-scripts-by-using-spcomponentloader"></a><span data-ttu-id="501cb-216">Laden von SharePoint JSOM-Skripts mit SPComponentLoader</span><span class="sxs-lookup"><span data-stu-id="501cb-216">Load SharePoint JSOM scripts using SPComponentLoader</span></span>

<span data-ttu-id="501cb-p122">SPFx-Komponenten sollten SharePoint JSOM-Skripts nur einmal laden. In diesem Beispiel – vorausgesetzt, das Webpart besteht aus einer einzigen React-Komponente – sollten Sie die SharePoint JSOM-Skripts am besten in der `componentDidMount`-Methode der React-Komponente laden, da diese Methode erst ausgeführt wird, wenn die Komponente instanziiert wurde.</span><span class="sxs-lookup"><span data-stu-id="501cb-p122">SPFx components should load SharePoint JSOM scripts only once. In this example, given that the web part consists of a single React component, the best place to load SharePoint JSOM scripts is inside the React component's `componentDidMount` method, which executes only once after the component has been instantiated.</span></span>

1. <span data-ttu-id="501cb-219">Öffnen Sie im Code-Editor die Datei **./src/webparts/sharePointLists/components/SharePointLists.tsx**.</span><span class="sxs-lookup"><span data-stu-id="501cb-219">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing  statements add:</span></span> <span data-ttu-id="501cb-220">Fügen Sie im oberen Bereich der Datei eine `import`-Anweisung hinzu, die auf `SPComponentLoader` verweist.</span><span class="sxs-lookup"><span data-stu-id="501cb-220">In the code editor, open the ./src/webparts/sharePointLists/components/SharePointLists.tsx file. In the top section of the file, add an  statement referencing the . Then, in the  class, add the  method:</span></span> <span data-ttu-id="501cb-221">Fügen Sie die `SharePointLists`-Klasse der `componentDidMount`-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="501cb-221">In the `SharePointLists` class, add the `componentDidMount` method:</span></span>

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

2. <span data-ttu-id="501cb-222">Unter Verwendung einer Reihe von verketteten Zusagen laden wir die verschiedenen Skripts, die zusammen die Verwendung von SharePoint JSOM in Ihrer clientseitigen SharePoint Framework-Webpart ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="501cb-222">Using a series of chained promises, we load the different scripts that together enable using SharePoint JSOM in your SharePoint Framework component.</span></span> <span data-ttu-id="501cb-223">Beachten Sie, wie Sie dank Verwendung des `SPComponentLoader` serverrelative URLs verwenden können, die Skripts aus dem aktuellen SharePoint-Mandanten laden.</span><span class="sxs-lookup"><span data-stu-id="501cb-223">Note that by using the `SPComponentLoader`, you can use server-relative URLs that load the scripts from the current SharePoint tenant.</span></span> <span data-ttu-id="501cb-224">Nachdem alle Skripts geladen wurden, aktualisieren Sie den Status der React-Komponente, indem Sie bestätigen, dass alle Voraussetzungen geladen wurden und das Webpart einsatzbereit ist.</span><span class="sxs-lookup"><span data-stu-id="501cb-224">After all scripts have been loaded, you update the React component's state confirming that all prerequisites have been loaded and the web part is ready to use.</span></span>

3. <span data-ttu-id="501cb-225">Bestätigen Sie, dass das Webpart wie erwartet funktioniert, indem Sie auf der Konsole den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="501cb-225">Confirm that the web part is working as expected by running the following command from the console:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

  <span data-ttu-id="501cb-226">Wie zuvor sollte das Webpart die Titel der SharePoint-Listen auf der aktuellen Website anzeigen.</span><span class="sxs-lookup"><span data-stu-id="501cb-226">Just as before, the web part should show the titles of SharePoint lists in the current site.</span></span>

  ![Das clientseitige SharePoint Framework-Webpart zeigt Titel von SharePoint-Listen in der aktuellen Website an](../../../images/tutorial-spjsom-web-part-list-titles.png)

  
<span data-ttu-id="501cb-228">Obwohl die Verwendung des `SPComponentLoader` einigen Aufwand erfordert, ermöglicht er Ihnen, serverrelative URLs zu verwenden, die in Szenarien nützlich sind, in denen Sie unterschiedliche Mandanten für Entwicklung, Prüfung und Produktion einsetzen.</span><span class="sxs-lookup"><span data-stu-id="501cb-228">While using the `SPComponentLoader` requires some additional effort, it allows you to use server-relative URLs which is beneficial in scenarios when you're using different tenants for development, testing, and production.</span></span>

## <a name="considerations"></a><span data-ttu-id="501cb-229">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="501cb-229">Considerations</span></span>

<span data-ttu-id="501cb-230">In der Vergangenheit haben Sie vielleicht beim Erstellen von clientseitigen Anpassungen auf SharePoint-Plattformen SharePoint JSOM zur Kommunikation mit SharePoint verwendet.</span><span class="sxs-lookup"><span data-stu-id="501cb-230">In the past, when building client-side customizations on SharePoint you might have used SharePoint JSOM to communicate with SharePoint. However, the recommended approach is to use the SharePoint REST API either directly or through the PnP JavaScript Core Library.</span></span> <span data-ttu-id="501cb-231">Jetzt ist die empfohlene Vorgehensweise aber entweder die Verwendung der SharePoint REST-API oder der [PnP JavaScript-Core-Bibliothek](https://github.com/SharePoint/PnP-JS-Core).</span><span class="sxs-lookup"><span data-stu-id="501cb-231">In the past, when building client-side customizations on SharePoint you might have used SharePoint JSOM to communicate with SharePoint. However, the recommended approach is to use the SharePoint REST API either directly or through the [PnP JavaScript Core Library](https://github.com/SharePoint/PnP-JS-Core).</span></span>

<span data-ttu-id="501cb-p126">Als SharePoint JSOM eingeführt wurde, stellte dies den ersten Schritt im Hinblick auf eine Unterstützung clientseitiger Lösungen auf SharePoint dar. Es wird jedoch nicht mehr aktiv verwaltet und bietet möglicherweise keinen Zugriff auf alle Funktionen, die über die REST-API verfügbar sind. Außerdem können Sie, unabhängig davon, ob Sie die SharePoint-REST-API direkt oder über die PnP JavaScript-Core-Bibliothek verwenden, Zusagen verwenden, die das Schreiben von asynchronem Code erheblich erleichtern (ein häufig auftretendes Problem bei der Verwendung von JSOM).</span><span class="sxs-lookup"><span data-stu-id="501cb-p126">When SharePoint JSOM was introduced, it was the first step towards supporting client-side solutions on SharePoint. However, it is no longer being actively maintained and might not offer access to all capabilities available through the REST API. Additionally, whether using the SharePoint REST API directly or through the PnP JavaScript Core Library, you can use promises which significantly simplify writing asynchronous code (a common problem when utilizing JSOM).</span></span>

<span data-ttu-id="501cb-235">Es gibt zwar immer noch Fälle, in denen SharePoint JSOM Zugriff auf Daten und Methoden bietet, die noch nicht von der SharePoint-REST-API abgedeckt sind, wenn möglich sollte aber die REST-API verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="501cb-235">Although there are still a limited number of cases where SharePoint JSOM provides access to data and methods not yet covered by the SharePoint REST API, where possible, the REST API should be preferred.</span></span>

<span data-ttu-id="501cb-p127">Wenn Sie vorhandene Anpassungen haben, die SharePoint JSOM verwenden, und in Erwägung ziehen, diese zu SharePoint Framework zu migrieren, sollte dieser Artikel Ihnen die erforderlichen Informationen zur Verwendung von SharePoint JSOM in SharePoint Framework-Lösungen liefern. Langfristig sollten Sie jedoch die Art und Weise ändern, wie Sie mit SharePoint kommunizieren, entweder unter Verwendung der SharePoint-REST-API (direkt) oder über die PnP JavaScript-Core-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="501cb-p127">If you have existing customizations using SharePoint JSOM and are considering migrating them to the SharePoint Framework, this article should provide you with the necessary information about using SharePoint JSOM in SharePoint Framework solutions. Longer term, however, you should consider changing how you communicate with SharePoint to either using the SharePoint REST API directly or through the PnP JavaScript Core Library.</span></span>
