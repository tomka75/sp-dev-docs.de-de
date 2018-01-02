---
title: "Verbinden Ihres clientseitigen Webparts mit SharePoint („Hello World“ Teil 2)"
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: 50ba50db6da70ab271d61db1c8f894fd091270c2
ms.sourcegitcommit: 1f752afb40ff133e2fae14337e09392cc5d9d181
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="connect-your-client-side-web-part-to-sharepoint-hello-world-part-2"></a><span data-ttu-id="f7b91-102">Verbinden Ihres clientseitigen Webparts mit SharePoint („Hello World“ Teil 2)</span><span class="sxs-lookup"><span data-stu-id="f7b91-102">Connect your client-side web part to SharePoint (Hello world part 2)</span></span>

<span data-ttu-id="f7b91-103">Wenn Sie Ihr Webpart mit SharePoint verbinden, haben Sie Zugriff auf SharePoint-Funktionalitäten und -Daten und können Endbenutzern eine stärker integrierte Erfahrung bieten.</span><span class="sxs-lookup"><span data-stu-id="f7b91-103">Connect your web part to SharePoint to access functionality and data in SharePoint and provide a more integrated experience for end users. This article continues building the hello world web part built in the previous article Build your first web part.</span></span> <span data-ttu-id="f7b91-104">In diesem Artikel bauen wir das HelloWorld-Webpart weiter aus, das Sie im vorherigen Artikel [Erstellen Ihres ersten Webparts](./build-a-hello-world-web-part.md) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f7b91-104">Connect your web part to SharePoint to access functionality and data in SharePoint and provide a more integrated experience for end users. This article continues building the hello world web part built in the previous article [Build your first web part](./build-a-hello-world-web-part.md).</span></span>

<span data-ttu-id="f7b91-105">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="f7b91-105">You can also follow follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3).</span></span> 

<a href="https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3">
<img src="../../../images/spfx-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="run-gulp-serve"></a><span data-ttu-id="f7b91-106">Ausführen von „gulp serve“</span><span class="sxs-lookup"><span data-stu-id="f7b91-106">Run gulp serve</span></span>

<span data-ttu-id="f7b91-107">Stellen Sie sicher, dass der Befehl `gulp serve` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f7b91-107">Make sure you have the `gulp serve` command running.</span></span> <span data-ttu-id="f7b91-108">Sollte er noch nicht ausgeführt werden, wechseln Sie ins Projektverzeichnis **helloworld-webpart**, und führen Sie die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="f7b91-108">Make sure you have the  command running. If it is not already running, go to the **helloworld-webpart** project directory and run it using the following commands.</span></span>

```
cd helloworld-webpart
gulp serve
```

## <a name="get-access-to-page-context"></a><span data-ttu-id="f7b91-109">Zugreifen auf den Seitenkontext</span><span class="sxs-lookup"><span data-stu-id="f7b91-109">Get access to page context</span></span>

<span data-ttu-id="f7b91-p103">Wird Workbench lokal gehostet, befinden Sie sich nicht im Kontext einer SharePoint-Seite. Sie haben aber auch dann viele verschiedene Möglichkeiten, Ihr Webpart zu testen. Beispielsweise können Sie sich auf die Webpart-UX konzentrieren und mithilfe simulierter Daten eine Interaktion mit SharePoint simulieren, wenn Sie sich nicht im SharePoint-Kontext bewegen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-p103">When the workbench is hosted locally, you do not have the SharePoint page context. You can still test your web part in many different ways. For example, you can concentrate on building the web part's UX and use mock data to simulate SharePoint interaction when you don't have the SharePoint context.</span></span>

<span data-ttu-id="f7b91-113">Wenn Sie Workbench jedoch in SharePoint hosten, haben Sie Zugang zum Seitenkontext, der wiederum verschiedene Schlüsseleigenschaften bereitstellt, darunter:</span><span class="sxs-lookup"><span data-stu-id="f7b91-113">However, when the workbench is hosted in SharePoint, you get access to the page context which provides various key properties, such as:</span></span>

* <span data-ttu-id="f7b91-114">Webtitel</span><span class="sxs-lookup"><span data-stu-id="f7b91-114">Web title</span></span>
* <span data-ttu-id="f7b91-115">Absolute Web-URL</span><span class="sxs-lookup"><span data-stu-id="f7b91-115">Web absolute URL</span></span>
* <span data-ttu-id="f7b91-116">Relative Webserver-URL</span><span class="sxs-lookup"><span data-stu-id="f7b91-116">Web server-relative URL</span></span>
* <span data-ttu-id="f7b91-117">Benutzeranmeldename</span><span class="sxs-lookup"><span data-stu-id="f7b91-117">User login name</span></span>

<span data-ttu-id="f7b91-118">Zugreifen können Sie auf den Seitenkontext durch Implementierung der folgenden Variable in der Webpart-Klasse:</span><span class="sxs-lookup"><span data-stu-id="f7b91-118">You can get access to the page context using the following variable in your web part class:</span></span>

```ts
this.context.pageContext
```

<span data-ttu-id="f7b91-119">Wechseln Sie zu Visual Studio Code (oder Ihrer bevorzugten IDE), und öffnen Sie **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-119">Switch to Visual Studio code (or your preferred IDE) and open **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span></span>

<span data-ttu-id="f7b91-120">Ersetzen Sie in der Methode **render** den Codeblock **innerHTML** durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="f7b91-120">Inside the **render** method, replace the **innerHTML** code block with the following code:</span></span>

```ts
    this.domElement.innerHTML = `
      <div class="${ styles.helloWorld }">
        <div class="${ styles.container }">
          <div class="${ styles.row }">
            <div class="${ styles.column }">
              <span class="${ styles.title }">Welcome to SharePoint!</span>
              <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
              <p class="${ styles.description }">${escape(this.properties.description)}</p>
              <p class="${ styles.description }">${escape(this.properties.test)}</p>
              <p class="${ styles.description }">Loading from ${escape(this.context.pageContext.web.title)}</p>
              <a href="https://aka.ms/spfx" class="${ styles.button }">
                <span class="${ styles.label }">Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>`;
```

<span data-ttu-id="f7b91-121">Dabei wird `${ }` verwendet, um den Variablenwert im HTML-Block auszugeben.</span><span class="sxs-lookup"><span data-stu-id="f7b91-121">Notice how `${ }` is used to output the variable's value in the HTML block.</span></span> <span data-ttu-id="f7b91-122">Ein zusätzlicher per `p` codierter HTML-Abschnitt wird zur Anzeige von `this.context.pageContext.web.title` verwendet.</span><span class="sxs-lookup"><span data-stu-id="f7b91-122">An extra HTML `p` is used to display `this.context.pageContext.web.title`.</span></span> <span data-ttu-id="f7b91-123">Da dieses Webpart aus der lokalen Umgebung geladen wird, lautet der Titel **Local Workbench**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-123">Notice how  is used to output the variable's value in the HTML block. An extra HTML  is used to display . Since this web part loads from the local environment, the title will be **Local Workbench**.</span></span>

<span data-ttu-id="f7b91-124">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-124">Save the file.</span></span> <span data-ttu-id="f7b91-125">Der noch in der Konsole laufende Befehl `gulp serve` erkennt diesen Speichervorgang und:</span><span class="sxs-lookup"><span data-stu-id="f7b91-125">Save the file. The `gulp serve` running in your console will detect this save operation and:</span></span>

* <span data-ttu-id="f7b91-126">Erstellt und bündelt den aktualisierten Code automatisch</span><span class="sxs-lookup"><span data-stu-id="f7b91-126">Build and bundle the updated code automatically.</span></span>
* <span data-ttu-id="f7b91-127">Aktualisiert die Seite in der lokalen Workbench (da der Webpart-Code neu geladen werden muss)</span><span class="sxs-lookup"><span data-stu-id="f7b91-127">Refresh your local workbench page (as the web part code needs to be reloaded).</span></span>

> [!NOTE]
> <span data-ttu-id="f7b91-128">Zeigen Sie das Konsolenfenster und VS Code nebeneinander an, um mitzuverfolgen, wie gulp beim Speichern von Änderungen in VS Code automatisch kompiliert.</span><span class="sxs-lookup"><span data-stu-id="f7b91-128">Note: Keep the console window and VS Code side by side to see gulp automatically compile as you save changes in VS Code.</span></span>

<span data-ttu-id="f7b91-129">Wechseln Sie in Ihrem Browser zur lokalen Registerkarte „SharePoint Workbench“. Wenn Sie die Registerkarte bereits geschlossen haben, lautet die URL `https://localhost:4321/temp/workbench.html`.</span><span class="sxs-lookup"><span data-stu-id="f7b91-129">In your browser, switch to the local SharePoint Workbench tab. If you have already closed the tab, the URL is `https://localhost:4321/temp/workbench.html`.</span></span>

<span data-ttu-id="f7b91-130">Im Webpart sollte jetzt Folgendes zu sehen sein:</span><span class="sxs-lookup"><span data-stu-id="f7b91-130">You should see the following in the web part:</span></span>

![SharePoint-Seitenkontext unter „localhost“](../../../images/sp-mock-localhost-wp.png)

<span data-ttu-id="f7b91-132">Navigieren Sie nun zu der in SharePoint gehosteten SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="f7b91-132">Now, navigate to the SharePoint Workbench hosted in SharePoint. The full URL is .</span></span> <span data-ttu-id="f7b91-133">Die vollständige URL lautet `https://your-sharepoint-site-url/_layouts/workbench.aspx`.</span><span class="sxs-lookup"><span data-stu-id="f7b91-133">The full URL is `https://your-sharepoint-site-url/_layouts/workbench.aspx`.</span></span> <span data-ttu-id="f7b91-134">Beachten Sie, dass Sie auf der SharePoint Online-Seite die Seiten aktualisieren müssen, um die Änderungen zu sehen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-134">Now, navigate to the SharePoint Workbench hosted in SharePoint. The full URL is . Notice that in the SharePoint Online side, you'll need to refresh the page to see the changes.</span></span>

> [!NOTE]
> <span data-ttu-id="f7b91-135">Wenn Sie das SPFx-Entwicklerzertifikat noch nicht installiert haben, meldet Workbench, dass das Laden von Skripts von „localhost“ nicht konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="f7b91-135">Note: If you do not have the SPFx developer certificate installed, Workbench will notify you that it is not configured to load scripts from localhost.</span></span> <span data-ttu-id="f7b91-136">Führen Sie im Projektverzeichnis den Befehl `gulp trust-dev-cert` in der Konsole aus, um das Entwicklerzertifikat zu installieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-136">Execute `gulp trust-dev-cert` command in your project directory console to install the developer certificate.</span></span>

<span data-ttu-id="f7b91-137">Der Seitenkontext ist jetzt für das Webpart verfügbar, und der Seitentitel Ihrer SharePoint-Website sollte im Webpart zu sehen sein.</span><span class="sxs-lookup"><span data-stu-id="f7b91-137">You should now see your SharePoint site title in the web part now that page context is available to the web part.</span></span>

![SharePoint-Seitenkontext auf der SharePoint-Website](../../../images/sp-lists-spsiteurl-wp.png)

## <a name="define-list-model"></a><span data-ttu-id="f7b91-139">Definieren eines Listenmodells</span><span class="sxs-lookup"><span data-stu-id="f7b91-139">Define list model</span></span>
<span data-ttu-id="f7b91-p108">Wenn Sie mit SharePoint-Listendaten arbeiten möchten, benötigen Sie ein Listenmodell. Zum Abrufen von Listen sind zwei Modelle erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f7b91-p108">You need a list model to start working with SharePoint list data. To retrieve the lists, you need two models.</span></span> 

<span data-ttu-id="f7b91-142">Wechseln Sie zu Visual Studio Code, und öffnen Sie **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-142">Switch to Visual Studio Code and go to **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span></span>

<span data-ttu-id="f7b91-143">Definieren Sie die folgenden Modelle des Typs `interface` direkt oberhalb der Klasse **HelloWorldWebPart**:</span><span class="sxs-lookup"><span data-stu-id="f7b91-143">Define the following `interface` models just above the **HelloWorldWebPart** class:</span></span>

```ts
export interface ISPLists {
    value: ISPList[];
}

export interface ISPList {
    Title: string;
    Id: string;
}
```

<span data-ttu-id="f7b91-144">Die Schnittstelle **ISPList** enthält die SharePoint-Listeninformationen, die Sie einbinden möchten.</span><span class="sxs-lookup"><span data-stu-id="f7b91-144">The **ISPList** interface holds the SharePoint list information we are connecting to.</span></span> 

## <a name="retrieve-lists-from-mock-store"></a><span data-ttu-id="f7b91-145">Abrufen von Listen aus einem simulierten Speicher</span><span class="sxs-lookup"><span data-stu-id="f7b91-145">Retrieve lists from mock store</span></span>

<span data-ttu-id="f7b91-146">Für die Tests in der lokalen Workbench benötigen Sie einen simulierten Speicher, der simulierte Daten zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="f7b91-146">To test in the local workbench you will need a mock store that returns mock data.</span></span>

<span data-ttu-id="f7b91-147">Erstellen Sie im Ordner **src\webparts\helloWorld** eine neue Datei mit dem Namen **MockHttpClient.ts**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-147">Create a new file inside the **src\webparts\helloWorld** folder named **MockHttpClient.ts**.</span></span>

<span data-ttu-id="f7b91-148">Kopieren Sie den folgenden Code in die Datei **MockHttpClient.ts**:</span><span class="sxs-lookup"><span data-stu-id="f7b91-148">Copy the following code into **MockHttpClient.ts**:</span></span>

```ts
import { ISPList } from './HelloWorldWebPart';

export default class MockHttpClient  {

    private static _items: ISPList[] = [{ Title: 'Mock List', Id: '1' },
                                        { Title: 'Mock List 2', Id: '2' },
                                        { Title: 'Mock List 3', Id: '3' }];
    
    public static get(): Promise<ISPList[]> {
    return new Promise<ISPList[]>((resolve) => {
            resolve(MockHttpClient._items);
        });
    }
}
```

<span data-ttu-id="f7b91-149">Wichtige Hinweise zum Code:</span><span class="sxs-lookup"><span data-stu-id="f7b91-149">Things to note about the code:</span></span>

* <span data-ttu-id="f7b91-150">Da es in **HelloWorldWebPart.ts** mehrere Exporte gibt, wird per `{ }` festgelegt, welcher zu importieren ist.</span><span class="sxs-lookup"><span data-stu-id="f7b91-150">Because there are multiple exports in HelloWorldWebPart.ts the specific one to import is specified using . In this case, only the data model  is required.</span></span> <span data-ttu-id="f7b91-151">In diesem Fall ist nur das Datenmodell `ISPList` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f7b91-151">In this case, only the data model `ISPList` is required.</span></span>
* <span data-ttu-id="f7b91-152">Die Eingabe der Dateierweiterung ist bei Importen aus dem Standardmodul nicht nötig. In unserem Beispiel ist das Standardmodul **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-152">You do not need to type the file extension when importing from the default module which in this case is **HelloWorldWebPart**.</span></span> 
* <span data-ttu-id="f7b91-153">Der Code exportiert die Klasse **MockHttpClient** als Standardmodul, das sich anschließend in andere Dateien importieren lässt.</span><span class="sxs-lookup"><span data-stu-id="f7b91-153">It exports the **MockHttpClient** class as a default module so that it can be imported in other files.</span></span>
* <span data-ttu-id="f7b91-154">Der Code erstellt das anfängliche simulierte Array `ISPList` und die simulierten Rückgaben.</span><span class="sxs-lookup"><span data-stu-id="f7b91-154">It builds the initial `ISPList` mock array and returns.</span></span>

<span data-ttu-id="f7b91-155">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-155">Save the file.</span></span>

<span data-ttu-id="f7b91-156">Jetzt können Sie die Klasse **MockHttpClient** in der Klasse **HelloWorldWebPart** verwenden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-156">You can now use the **MockHttpClient** class in the **HelloWorldWebPart** class. You first need to import the MockHttpClient module.</span></span> <span data-ttu-id="f7b91-157">Zunächst müssen Sie das Modul **MockHttpClient** importieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-157">You can now use the MockHttpClient class in the HelloWorldWebPart class. You first need to import the **MockHttpClient** module.</span></span>

<span data-ttu-id="f7b91-158">Öffnen Sie die Datei **HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-158">Open the **HelloWorldWebPart.ts** file.</span></span>

<span data-ttu-id="f7b91-159">Kopieren Sie den folgenden Code, und fügen Sie ihn direkt unter `import * as strings from 'HelloWorldWebPartStrings';` ein.</span><span class="sxs-lookup"><span data-stu-id="f7b91-159">Copy and paste the following code just below `import * as strings from 'HelloWorldWebPartStrings';` :</span></span>

```ts
import MockHttpClient from './MockHttpClient';
```
 
<span data-ttu-id="f7b91-160">Fügen Sie die folgende private Methode in der Klasse **HelloWorldWebPart** hinzu, um den Listenabruf zu simulieren:</span><span class="sxs-lookup"><span data-stu-id="f7b91-160">Add the following private method that mocks the list retrieval inside the **HelloWorldWebPart** class.</span></span>

```ts
  private _getMockListData(): Promise<ISPLists> {
    return MockHttpClient.get()
      .then((data: ISPList[]) => {
        var listData: ISPLists = { value: data };
        return listData;
      }) as Promise<ISPLists>;
  }
```

<span data-ttu-id="f7b91-161">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-161">Save the file.</span></span>

## <a name="retrieve-lists-from-sharepoint-site"></a><span data-ttu-id="f7b91-162">Abrufen von Listen von einer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="f7b91-162">Retrieve lists from SharePoint site</span></span>

<span data-ttu-id="f7b91-p111">Als Nächstes müssen Sie Listen von der aktuellen Website abrufen. Zum Abrufen der Listen von der Website verwenden Sie die SharePoint-REST-APIs, die unter „https://yourtenantprefix.sharepoint.com/_api/web/lists“ liegen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-p111">Next you need to retrieve lists from the current site. You will use SharePoint REST APIs to retrieve the lists from the site, which are located at https://yourtenantprefix.sharepoint.com/_api/web/lists.</span></span>

<span data-ttu-id="f7b91-165">SharePoint-Framework umfasst die Hilfsklasse **spHttpClient**, um REST-API-Anforderungen in SharePoint auszuführen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-165">SharePoint Framework includes a helper class **spHttpClient** to execute REST API requests against SharePoint.</span></span> <span data-ttu-id="f7b91-166">Es fügt Standardkopfzeilen hinzu, verwaltet den für Schreibvorgänge erforderlichen Digest und sammelt Telemetrie, die dem Dienst hilft, die Leistung einer Anwendung zu überwachen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-166">SharePoint Framework includes a helper class spHttpClient to execute REST API requests against SharePoint. It adds default headers, manages the digest needed for writes, and collects telemetry that helps the service to monitor the performance of an application.</span></span>

<span data-ttu-id="f7b91-167">Um diese Hilfsklasse zu verwenden, müssen Sie diese zuerst aus dem **@microsoft/sp-http**-Modul importieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-167">To use this helper class, you will first need to import them from the **@microsoft/sp-http** module.</span></span>

<span data-ttu-id="f7b91-168">Führen Sie einen Bildlauf an den Anfang der Datei **HelloWorldWebPart.ts** aus.</span><span class="sxs-lookup"><span data-stu-id="f7b91-168">Scroll to the top of the **HelloWorldWebPart.ts** file.</span></span> 

<span data-ttu-id="f7b91-169">Kopieren Sie den folgenden Code, und fügen Sie ihn direkt unter `import MockHttpClient from './MockHttpClient';` ein.</span><span class="sxs-lookup"><span data-stu-id="f7b91-169">Copy and paste the following code just below `import MockHttpClient from './MockHttpClient';` :</span></span>

```ts
import {
  SPHttpClient,
  SPHttpClientResponse   
} from '@microsoft/sp-http';
```

<span data-ttu-id="f7b91-170">Fügen Sie die folgende private Methode in der Klasse **HelloWorldWebPart** hinzu, um Listen von SharePoint abzurufen:</span><span class="sxs-lookup"><span data-stu-id="f7b91-170">Add the following private method to retrieve lists from SharePoint inside the **HelloWorldWebPart** class.</span></span>

```ts
private _getListData(): Promise<ISPLists> {
  return this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + `/_api/web/lists?$filter=Hidden eq false`, SPHttpClient.configurations.v1)
    .then((response: SPHttpClientResponse) => {
      return response.json();
    });
}
```

<span data-ttu-id="f7b91-171">Die Methode verwendet die Hilfsklasse **spHttpClient** und gibt eine `get`-Anforderung aus.</span><span class="sxs-lookup"><span data-stu-id="f7b91-171">The method uses the **spHttpClient** helper class and issues a `get` request. It uses the ISPLists model and also applies a filter to not retrieve hidden lists.</span></span> <span data-ttu-id="f7b91-172">Sie verwendet das Modell **ISPLists** und implementiert einen Filter, der den Abruf versteckter Listen verhindert.</span><span class="sxs-lookup"><span data-stu-id="f7b91-172">The method uses the spHttpClient helper class and issues a  request. It uses the **ISPLists** model and also applies a filter to not retrieve hidden lists.</span></span>

<span data-ttu-id="f7b91-173">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-173">Save the file.</span></span> 

<span data-ttu-id="f7b91-p114">Wechseln Sie in das Konsolenfenster, in dem `gulp serve` ausgeführt wird, und schauen Sie nach, ob Fehler gemeldet wurden. gulp meldet alle Fehler in der Konsole. Sie müssen sie dann zuerst beheben, bevor Sie fortfahren können.</span><span class="sxs-lookup"><span data-stu-id="f7b91-p114">Switch to the console window that is running `gulp serve` and check if there are any errors. If there are errors, gulp reports them in the console and you will need to fix them before proceeding.</span></span>

## <a name="add-new-styles"></a><span data-ttu-id="f7b91-176">Hinzufügen neuer Stile</span><span class="sxs-lookup"><span data-stu-id="f7b91-176">Add new styles</span></span>

<span data-ttu-id="f7b91-177">Das SharePoint Framework verwendet [Sass](http://sass-lang.com/) als CSS-Präprozessor und arbeitet insbesondere mit der [SCSS-Syntax](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html), die vollständig konform mit der normalen CSS-Syntax ist.</span><span class="sxs-lookup"><span data-stu-id="f7b91-177">The SharePoint Framework uses [Sass](http://sass-lang.com/) as the CSS pre-processor and specifically uses the [SCSS syntax](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html) which is fully complaint with normal CSS syntax.</span></span> <span data-ttu-id="f7b91-178">Sass erweitert die CSS-Sprache und ermöglicht den Einsatz von Features wie Variablen, geschachtelten Regeln und Inline-Importen zur Organisation und Erstellung effizienter Stylesheets für Webparts.</span><span class="sxs-lookup"><span data-stu-id="f7b91-178">Sass extends the CSS language and allows you to use features like variables, nested rules, and inline imports to organize and create efficient style sheets for your web parts.</span></span> <span data-ttu-id="f7b91-179">In das SharePoint Framework ist bereits ein SCSS-Compiler integriert, der Sass-Dateien in normale CSS-Dateien konvertiert und eine typisierte Version bereitstellt, die Sie während der Entwicklung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f7b91-179">The SharePoint Framework already comes with a SCSS compiler that converts your Sass files to normal CSS files and also provides a typed version to use it in during development.</span></span>

<span data-ttu-id="f7b91-180">Öffnen Sie zum Hinzufügen neuer Stile zunächst **HelloWorld.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-180">To add new styles, open HelloWorld.module.scss. This is the SCSS file where you will define your styles.</span></span> <span data-ttu-id="f7b91-181">Dies ist die SCSS-Datei, in der Sie Ihre Stile definieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-181">To add new styles, open HelloWorld.module.scss. This is the SCSS file where you will define your styles.</span></span>

<span data-ttu-id="f7b91-182">Standardmäßig sind die Stile auf das Webpart beschränkt.</span><span class="sxs-lookup"><span data-stu-id="f7b91-182">By default, the styles are scoped to your web part. You can see that as the styles are defined under .helloWorld.</span></span> <span data-ttu-id="f7b91-183">Das können Sie daran erkennen, dass die Stile unter **.helloWorld** definiert werden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-183">By default, the styles are scoped to your web part. You can see that as the styles are defined under **.helloWorld**.</span></span>

<span data-ttu-id="f7b91-184">Fügen Sie die folgenden Formate nach dem `.button`-Stil, aber immer noch innerhalb des Bereichs des `.helloWorld`-Hauptstils hinzu.</span><span class="sxs-lookup"><span data-stu-id="f7b91-184">Add the following styles after the `.button` style, but still inside of the main `.helloWorld` style section:</span></span>

```css
.list {
    color: #333333;
    font-family: 'Segoe UI Regular WestEuropean', 'Segoe UI', Tahoma, Arial, sans-serif;
    font-size: 14px;
    font-weight: normal;
    box-sizing: border-box;
    margin: 10;
    padding: 10;
    line-height: 50px;
    list-style-type: none;
    box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

.listItem {
    color: #333333;
    vertical-align: center;
    font-family: 'Segoe UI Regular WestEuropean', 'Segoe UI', Tahoma, Arial, sans-serif;
    font-size: 14px;
    font-weight: normal;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    box-shadow: none;
    *zoom: 1;
    padding: 9px 28px 3px;
    position: relative;
}
``` 

<span data-ttu-id="f7b91-185">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-185">Save the file.</span></span>

<span data-ttu-id="f7b91-186">gulp erstellt den Code in der Konsole neu, sobald Sie die Datei speichern.</span><span class="sxs-lookup"><span data-stu-id="f7b91-186">gulp rebuilds the code in the console as soon as you save the file.</span></span> <span data-ttu-id="f7b91-187">Dadurch werden die entsprechenden Typisierungen in der Datei **HelloWorld.module.scss.ts** generiert.</span><span class="sxs-lookup"><span data-stu-id="f7b91-187">This will generate the corresponding typings in the **HelloWorld.module.scss.ts** file.</span></span> <span data-ttu-id="f7b91-188">Nach der Kompilierung in TypeScript können Sie diese Stile importieren und in Ihrem Webpart-Code referenzieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-188">Once compiled to typescript, you can then import and reference these styles in your web part code.</span></span>

<span data-ttu-id="f7b91-189">Ein Beispiel dafür sehen Sie in der Methode **render** des Webparts:</span><span class="sxs-lookup"><span data-stu-id="f7b91-189">You can see that in the **render** method of the web part:</span></span>

```html
<div class="${styles.row}">
```

## <a name="method-to-render-lists-information"></a><span data-ttu-id="f7b91-190">Methode zum Rendern von Listeninformationen</span><span class="sxs-lookup"><span data-stu-id="f7b91-190">Method to render lists information</span></span>

<span data-ttu-id="f7b91-191">Öffnen Sie die Klasse **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-191">Open the **HelloWorldWebPart** class.</span></span>

<span data-ttu-id="f7b91-192">SharePoint Workbench bietet Ihnen die Möglichkeit, Webparts entweder in Ihrer lokalen Umgebung oder auf einer SharePoint-Website zu testen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-192">SharePoint Workbench gives you the flexibility to test web parts in your local environment and from a SharePoint site. SharePoint Framework aids this capability by helping you understand which environment your web part is running from by using the EnvironmentType module.</span></span> <span data-ttu-id="f7b91-193">SharePoint-Framework unterstützt diese Funktion mit dem Modul **EnvironmentType**, das anzeigt, in welcher Umgebung das Webpart gerade ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f7b91-193">SharePoint Workbench gives you the flexibility to test web parts in your local environment and from a SharePoint site. SharePoint Framework aids this capability by helping you understand which environment your web part is running from by using the **EnvironmentType** module.</span></span> 

<span data-ttu-id="f7b91-194">Damit Sie das Modul verwenden können, müssen Sie zuerst die Module **Environment** und ***EnvironmentType** aus dem Bundle **@microsoft/sp-core-library** importieren.</span><span class="sxs-lookup"><span data-stu-id="f7b91-194">To use the module, you first need to import the **Environment** and the ***EnvironmentType** modules from the **@microsoft/sp-core-library** bundle. Add it to the import section at the top as shown in the following code:</span></span> <span data-ttu-id="f7b91-195">Fügen Sie es zum Abschnitt **import** oben auf der Seite hinzu, wie im folgenden Code illustriert:</span><span class="sxs-lookup"><span data-stu-id="f7b91-195">To use the module, you first need to import EnvironmentType module from the @microsoft/sp-client-base bundle. Add it to the **import** section at the top as shown in the following code:</span></span>

```ts
import {
  Environment,
  EnvironmentType
} from '@microsoft/sp-core-library';
```

<span data-ttu-id="f7b91-196">Fügen Sie die folgende private Methode in der Klasse **HelloWorldWebPart** hinzu, um die entsprechenden Methoden zum Abrufen der Listendaten aufzurufen:</span><span class="sxs-lookup"><span data-stu-id="f7b91-196">Add the following private method inside the **HelloWorldWebPart** class to call the respective methods to retrieve list data:</span></span>

```ts
  private _renderListAsync(): void {
    // Local environment
    if (Environment.type === EnvironmentType.Local) {
      this._getMockListData().then((response) => {
        this._renderList(response.value);
      });
    }
    else if (Environment.type == EnvironmentType.SharePoint || 
              Environment.type == EnvironmentType.ClassicSharePoint) {
      this._getListData()
        .then((response) => {
          this._renderList(response.value);
        });
    }
  }
```

<span data-ttu-id="f7b91-197">Wichtige Hinweise zu „hostType“ in der Methode **_renderListAsync**:</span><span class="sxs-lookup"><span data-stu-id="f7b91-197">Things to note about hostType in the **_renderListAsync** method:</span></span>

* <span data-ttu-id="f7b91-198">Die Eigenschaft `Environment.type` hilft Ihnen, zu überprüfen, ob Sie in einer lokalen Umgebung arbeiten oder in einer SharePoint-Umgebung.</span><span class="sxs-lookup"><span data-stu-id="f7b91-198">The `Environment.type` property will help you check if you are in a local or SharePoint environment.</span></span>
* <span data-ttu-id="f7b91-199">Je nachdem, wo Workbench gehostet wird, wird die jeweils korrekte Methode aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-199">The correct method is called depending on where your workbench is hosted.</span></span>

<span data-ttu-id="f7b91-200">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-200">Save the file.</span></span>

<span data-ttu-id="f7b91-201">Jetzt müssen Sie die Listendaten mit dem Wert rendern, der aus der REST-API abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="f7b91-201">Now you need to render the list data with the value fetched from the REST API.</span></span>

<span data-ttu-id="f7b91-202">Fügen Sie die folgende private Methode in der Klasse **HelloWorldWebPart** hinzu:</span><span class="sxs-lookup"><span data-stu-id="f7b91-202">Add the following private method inside the **HelloWorldWebPart** class:</span></span>

```ts
  private _renderList(items: ISPList[]): void {
    let html: string = '';
    items.forEach((item: ISPList) => {
      html += `
        <ul class="${styles.list}">
            <li class="${styles.listItem}">
                <span class="ms-font-l">${item.Title}</span>
            </li>
        </ul>`;
    });

    const listContainer: Element = this.domElement.querySelector('#spListContainer');
    listContainer.innerHTML = html;
  }
```

<span data-ttu-id="f7b91-203">Die oben beschriebene Methode referenziert die zuvor hinzugefügten neuen CSS-Stile über die Variable **styles**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-203">The previous method references the new CSS styles added earlier by using the **styles** variable.</span></span> 

<span data-ttu-id="f7b91-204">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-204">Save the file.</span></span>

## <a name="retrieve-list-data"></a><span data-ttu-id="f7b91-205">Abrufen von Listendaten</span><span class="sxs-lookup"><span data-stu-id="f7b91-205">Retrieve list data</span></span>

<span data-ttu-id="f7b91-206">Navigieren Sie zur Methode **render**, und ersetzen Sie den Code in der Methode durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="f7b91-206">Navigate to the **render** method and replace the code inside the method with the following code:</span></span>

```ts
    this.domElement.innerHTML = `
      <div class="${ styles.helloWorld }">
        <div class="${ styles.container }">
          <div class="${ styles.row }">
            <div class="${ styles.column }">
              <span class="${ styles.title }">Welcome to SharePoint!</span>
              <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
              <p class="${ styles.description }">${escape(this.properties.description)}</p>
              <p class="${ styles.description }">${escape(this.properties.test)}</p>
              <p class="${ styles.description }">Loading from ${escape(this.context.pageContext.web.title)}</p>
              <a href="https://aka.ms/spfx" class="${ styles.button }">
                <span class="${ styles.label }">Learn more</span>
              </a>
            </div>
          </div>
          <div id="spListContainer" />
        </div>
      </div>`;

      this._renderListAsync();
```

<span data-ttu-id="f7b91-207">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="f7b91-207">Save the file.</span></span>

<span data-ttu-id="f7b91-208">Im Konsolenfenster, in dem `gulp serve` ausgeführt wird, wird der Code neu erstellt.</span><span class="sxs-lookup"><span data-stu-id="f7b91-208">Notice in the `gulp serve` console window that it rebuilds the code. Make sure you don't see any errors.</span></span> <span data-ttu-id="f7b91-209">Vergewissern Sie sich, dass keine Fehler gemeldet wurden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-209">Make sure you don't see any errors.</span></span>

<span data-ttu-id="f7b91-210">Wechseln Sie zur lokalen Workbench, und fügen Sie das HelloWorld-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="f7b91-210">Switch to your local workbench and add the HelloWorld web part.</span></span>

<span data-ttu-id="f7b91-211">Nun sollten die simulierten Daten zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-211">You should see the mock data returned.</span></span>

![Rendern von Listendaten von „localhost“](../../../images/sp-lists-render-localhost.png)

<span data-ttu-id="f7b91-p122">Wechseln Sie zur in SharePoint gehosteten Workbench. Aktualisieren Sie die Seite, und fügen Sie das HelloWorld-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="f7b91-p122">Switch to the workbench hosted in SharePoint. Refresh the page and add the HelloWorld web part.</span></span>

<span data-ttu-id="f7b91-215">Es sollten nun Listen von der aktuellen Website zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-215">You should see lists returned from the current site.</span></span>

![Rendern von Listendaten aus SharePoint](../../../images/sp-lists-render-spsite.png)

<span data-ttu-id="f7b91-217">Jetzt können Sie den Server stoppen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-217">Now you can stop the server from running.</span></span> <span data-ttu-id="f7b91-218">Wechseln Sie zur Konsole, und stoppen Sie `gulp serve`.</span><span class="sxs-lookup"><span data-stu-id="f7b91-218">Switch to the console and execute the following  task:</span></span> <span data-ttu-id="f7b91-219">Drücken Sie `Ctrl+C`, um den gulp-Task zu beenden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-219">Choose `Ctrl+C` to terminate the gulp task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7b91-220">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="f7b91-220">Next steps</span></span>

<span data-ttu-id="f7b91-221">Sehr gut! Sie haben Ihren Webpart jetzt an die SharePoint-Listendaten angebunden.</span><span class="sxs-lookup"><span data-stu-id="f7b91-221">Congratulations on connecting your web part to SharePoint list data!</span></span> <span data-ttu-id="f7b91-222">Im nächsten Artikel, [Bereitstellen Ihres Webparts auf einer SharePoint-Seite](./serve-your-web-part-in-a-sharepoint-page.md), können Sie Ihren HelloWorld-Webpart weiter ausbauen.</span><span class="sxs-lookup"><span data-stu-id="f7b91-222">Congratulations on connecting your web part to SharePoint list data! You can continue building out your Hello World web part in the next topic Deploy your web part to a SharePoint page. You will learn how to deploy and preview the Hello World web part in a classic SharePoint server-side page.</span></span> <span data-ttu-id="f7b91-223">Dort erfahren Sie, wie Sie den HelloWorld-Webpart auf einer SharePoint-Seite bereitstellen und eine Vorschau anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="f7b91-223">You will learn how to deploy and preview the Hello World web part in a SharePoint page.</span></span>

> [!NOTE]
> <span data-ttu-id="f7b91-224">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="f7b91-224">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="f7b91-225">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="f7b91-225">Thanks for your input advance.</span></span>