---
title: Gemeinsame Verwendung von Daten zwischen clientseitigen Webparts
description: "Ansätze, die Sie verwenden können, um Daten freizugeben und abgerufene Daten auf mehreren Webparts in SharePoint zu speichern"
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: 0d058b7f87b29f49683c9aec62d3d569d47c0d80
ms.sourcegitcommit: 1f1044e59d987d878bb8bc403413e3090234ad44
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2018
---
# <a name="share-data-between-client-side-web-parts"></a><span data-ttu-id="c4ff9-103">Gemeinsame Verwendung von Daten zwischen clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="c4ff9-103">Share data between client-side web parts</span></span>

<span data-ttu-id="c4ff9-p101">Wenn Sie bei der Erstellung von clientseitigen Webparts Daten nur einmal laden und anschließend in den verschiedenen Webparts jeweils wiederverwenden, verbessert das die Leistung Ihrer Seiten und reduziert die Last in Ihrem Netzwerk. In diesem Artikel stellen wir Ihnen verschiedene Möglichkeiten vor, wie Webparts Daten gemeinsam verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p101">When building client-side web parts, loading data once and reusing it across different web parts will help you improve the performance of your pages and decrease the load on your network. This article describes a number of approaches that you can use to share data across multiple web parts.</span></span>

## <a name="why-share-data-between-web-parts"></a><span data-ttu-id="c4ff9-106">Warum sollten Daten zwischen Webparts geteilt werden?</span><span class="sxs-lookup"><span data-stu-id="c4ff9-106">Why Share Data Between Web Parts</span></span>

<span data-ttu-id="c4ff9-p102">Bei Webpartprojekten ist es häufig der Fall, dass auf einer einzigen Seite mehrere Webparts eingesetzt werden sollen. Wenn Sie dabei jedes Webpart als unabhängigen Teil der Seite behandeln, kann es passieren, dass einander ähnliche Datasets oder sogar ein und dasselbe Dataset mehrfach auf der Seite geladen werden. Das verlangsamt das Laden der Seite unnötig und erhöht das Datenverkehrsaufkommen in Ihrem Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p102">Often, when building web parts, a number of them will be used together on one page. If you consider each web part as a standalone part of the page, then you may end up in a situation where you are loading a similar or even the same set of data multiple times on the same page. This will unnecessarily slow down the loading of the page and increase traffic on your network.</span></span>

![Zwei Webparts auf einer einzigen Seite, die jeweils separat einander ähnliche Datensätze laden](../../../images/guidance-sharingdata-loading-data-separately.png)

<br/>

<span data-ttu-id="c4ff9-111">Ein Beispieldienst für das Laden von Daten könnte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-111">A sample service responsible for loading the data could look like the following:</span></span>

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            // [...] reach out to a remote API
            resolve(recentDocument);
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            // [...] reach out to a remote API
            resolve(recentDocuments);
        });
    }
}
```

<br/>

<span data-ttu-id="c4ff9-112">Clientseitige SharePoint Framework-Webparts würden diesen Dienst über den folgenden Code nutzen:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-112">SharePoint Framework client-side web parts would consume this service using the following code:</span></span>

```ts
import { DocumentsService, IDocument } from '../../services';

export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {

  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    DocumentsService.getRecentDocuments(this.properties.startFrom)
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

<br/>

<span data-ttu-id="c4ff9-p103">Sie können Ihre Webparts so konfigurieren, dass sie die Daten nur ein einziges Mal laden. Das beschleunigt das Laden der Seite und reduziert den Datenverkehr in Ihrem Netzwerk. Wann immer eines der Webparts auf der Seite ein spezifisches Dataset anfordert, verwendet es wenn möglich die zuvor geladenen Daten wieder.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p103">To improve the loading time of the page and decrease the traffic on your network, you can build your web parts in such a way that they will load the data only once. Whenever one of the web parts on the page requests a specific set of data, it will reuse data loaded previously if possible.</span></span>

## <a name="store-the-retrieved-data-in-a-globally-scoped-variable"></a><span data-ttu-id="c4ff9-115">Speichern der abgerufenen Daten in einer Variablen mit globaler Bereichsdefinition</span><span class="sxs-lookup"><span data-stu-id="c4ff9-115">Store the retrieved data in a globally-scoped variable</span></span>

> [!NOTE] 
> <span data-ttu-id="c4ff9-p104">In der Regel sollten Sie keine Variablen mit globaler Bereichsdefinition verwenden. Wir verwenden Sie hier jedoch zur Veranschaulichung und aus Gründen der Einfachheit als „Democode“. Es gibt viele Muster, um dieses Problem zu umgehen, beispielsweise den Import/Export von Modulen mithilfe von TypeScript-Konzepten.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p104">Note, globally-scoped variables are generally a bad idea. However, for illustration and simplicity purposes we are using them here as "demo code". There are many patterns around this issue, including importing/exporting modules using TypeScript concepts.</span></span>

<span data-ttu-id="c4ff9-p105">Webparts, die mit SharePoint Framework erstellt werden, werden in separaten Modulen voneinander isoliert. Daher kann ein Webpart nicht direkt auf Daten und Eigenschaften zugreifen, die von einem anderen Webpart gespeichert werden. Eine Möglichkeit, diese Designstruktur zu umgehen und die von einem Webpart geladenen Daten auch für andere Webparts auf derselben Seite verfügbar zu machen: Sie können die abgerufenen Daten einer Variable mit globaler Bereichsdefinition zuweisen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p105">Web parts built using the SharePoint Framework are isolated into separate modules. This way, one web part cannot directly access data and properties stored by another web part. One way to overcome this design characteristic and make data loaded by one web part available to other web parts on the page is to assign the retrieved data to a globally-scoped variable.</span></span>

<span data-ttu-id="c4ff9-122">Der zuvor beschriebene Datenzugriffsdienst könnte dazu wie folgt angepasst werden:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-122">Using the data access service shown above, it could be changed as follows:</span></span>

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            if ((window as any).loadedData) {
                // data already loaded so reuse
                resolve((window as any).loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                (window as any).loadedData = loadedData;
                (window as any).loadingData = false;
                resolve((window as any).loadedData);
            }
        });
    }
}
```

<br/>

<span data-ttu-id="c4ff9-p106">Wie Sie sehen, wurde das Laden der Daten aus den spezifischen Methoden in die Methode `ensureRecentDocuments` verlagert. Falls die Daten bereits vorher geladen wurden, löst die Methode die Zusage auf und gibt sofort die zuvor geladenen Dokumente zurück. Werden die Daten gerade erst geladen, wartet die Methode 100 ms und versucht dann erneut, die Zusage aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p106">Notice how loading the data has been moved from the specific methods to the `ensureRecentDocuments` method. If the data has been loaded previously, the method resolves the promise immediately returning the previously loaded documents. If the data is currently being loaded, the method waits for 100ms and tries resolving the promise again.</span></span>

<span data-ttu-id="c4ff9-126">Ein Blick in das Protokoll in den Entwicklertools zeigt, dass die Remote-API jetzt nur noch ein einziges Mal aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-126">If you look at the log in the developer tools, you will notice that the remote API is now called only once.</span></span>

![Ein einziger Protokolleintrag über das Laden der Daten, für beide Webparts](../../../images/guidance-sharingdata-reusing-data-global-variable-loading-message.png)

<br/>

<span data-ttu-id="c4ff9-p107">Wenn Sie sich die Informationsmeldungen durchlesen, bemerken Sie Folgendes: Sobald das zweite Webpart versucht, die Daten zu laden, erkennt es, dass diese bereits geladen werden. Nachdem die Daten geladen wurden, verwendet es diese bereits vorhandenen Daten wieder, statt sie selbst nochmals zu laden.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p107">Looking at the informational messages, you can confirm that when the second web part tries to load the data it detects that the data is already being loaded. Once the data is loaded, it reuses the existing data rather than loading it itself.</span></span>

![Informationsmeldung aus dem Protokoll, die dokumentiert, dass das zweite Webpart gewartet hat, bis die Daten geladen wurden](../../../images/guidance-sharingdata-reusing-data-global-variable-waiting-message.png)

<br/>

<span data-ttu-id="c4ff9-p108">Eine Variable mit globaler Bereichsdefinition ist der einfachste Weg, Daten zwischen verschiedenen Webparts auf ein und derselben Seite auszutauschen. Ein Nachteil dieser Methode: Die Daten sind nicht nur für Webparts verfügbar, sondern auch für alle übrigen Elemente auf der Seite. Dadurch könnte es passieren, dass andere Elemente auf der Seite dieselbe Variable zur Datenspeicherung verwenden. Ihre Daten würden dann schlussendlich überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p108">Using a globally-scoped variable is the easiest way to exchange data between different web parts on the page. One downside of using this approach, however, is that the data is exposed not only to web parts but also to all other elements on the page. This introduces the risk of other elements on the page using the same variable as you to store their data potentially overwriting your data.</span></span>

## <a name="store-the-retrieved-data-in-a-cookie"></a><span data-ttu-id="c4ff9-134">Speichern der abgerufenen Daten in einem Cookie</span><span class="sxs-lookup"><span data-stu-id="c4ff9-134">Store the retrieved data in a cookie</span></span>

<span data-ttu-id="c4ff9-p109">Eine weitere Möglichkeit, Daten zwischen unterschiedlichen Webparts auszutauschen, besteht darin, sie in einem Cookie zu speichern. Das hat den zusätzlichen Vorteil, dass die Daten über einen längeren Zeitraum verfügbar sind. Wenn die Daten also selten geändert werden, können Sie sie ein einziges Mal laden und dann nicht nur in den verschiedenen Webparts wiederverwenden, sondern auch auf verschiedenen Seiten.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p109">Another approach to exchange data across different web parts is by storing the data in a cookie. The added benefit of using cookies is that you can persist the data for longer periods of time. So in cases where the data doesn't change often, you can load the data once and reuse it not only across different web parts but also across different pages.</span></span>

<span data-ttu-id="c4ff9-p110">Die Datenspeicherung in einem Cookie lässt sich fast genauso implementieren wie die Speicherung in einer Variable mit globaler Bereichsdefinition. Dass die eigentlichen Daten in einem Cookie gespeichert werden, ist im Grunde genommen der einzige Unterschied.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p110">The implementation using cookies is very similar to how you store data in a globally-scoped variable. The only difference is that the actual data would be stored in a cookie:</span></span>

```ts
import { IDocument } from './IDocument';
import * as Cookies from 'js-cookie';

export class DocumentsService {
    private static cookieName: string = 'recentDocuments';

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            let loadedData: IDocument[] = Cookies.getJSON(DocumentsService.cookieName);
            if (loadedData) {
                // data already loaded so reuse
                resolve(loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                Cookies.set(DocumentsService.cookieName, loadedData, {
                    expires: 1,
                    path: '/'
                });
                (window as any).loadingData = false;
                resolve(loadedData);
            }
        });
    }
}
```

<br/>

<span data-ttu-id="c4ff9-p111">Im vorherigen Beispiel wird das Paket [js-cookie](https://www.npmjs.com/package/js-cookie) verwendet, um das Arbeiten mit Cookies zu vereinfachen. Mithilfe der an die Methode `Cookies.set()` übergebenen Parameter können Sie festlegen, für welche Seiten die abgerufenen Daten verfügbar sein sollen und wie lange sie verfügbar sein sollen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p111">In the example above the [js-cookie](https://www.npmjs.com/package/js-cookie) package is used to simplify working with cookies. Using the parameters passed into the `Cookies.set()` method you can specify to which pages and for how long the retrieved data should be available.</span></span>

<span data-ttu-id="c4ff9-142">Wenn Sie die Seite das erste Mal in Microsoft Edge laden, werden die Daten ein einziges Mal abgerufen und dann von beiden Webparts wiederverwendet.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-142">When you load the page in Microsoft Edge the first time, you will see that the data is retrieved once and reused by both web parts.</span></span>

![Protokollnachrichten, die dokumentieren, dass die Daten ein einziges Mal geladen wurden und dass das jeweils andere Webpart gewartet hat, bis die Daten von der ersten Anforderung in Microsoft Edge geladen wurden](../../../images/guidance-sharingdata-cookie-edge-first-request.png)

<br/>

<span data-ttu-id="c4ff9-144">Bei nachfolgenden Anforderungen können Webparts die zuvor geladenen Daten direkt wiederverwenden, ohne zuerst die Remote-API aufrufen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-144">On subsequent requests, a web part can directly reuse the previously loaded data without calling the remote API.</span></span>

![Protokollnachricht, die dokumentiert, dass die Daten bei nachfolgenden Anforderungen in Microsoft Edge direkt geladen wurden, ohne vorherigen Aufruf der Remote-API](../../../images/guidance-sharingdata-cookie-edge-subsequent-request.png)

<br/>

<span data-ttu-id="c4ff9-146">Wenn Sie die Seite in Google Chrome laden, könnte es sein, dass die Daten zweimal über die Remote-API geladen werden und überhaupt nicht zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-146">When loading the page in Google Chrome, you would see that the data is loaded twice from the remote API and is not being cached at all.</span></span>

![Protokollnachricht, die dokumentiert, dass die Daten zweimal über die Remote-API geladen wurden, obwohl Cookies verwendet wurden](../../../images/guidance-sharingdata-cookie-chrome.png)

<br/>

<span data-ttu-id="c4ff9-p112">Die verschiedenen Webbrowser haben jeweils unterschiedliche Limits bezüglich der Datenmenge, die in einem Cookie gespeichert werden darf. In diesem Beispiel überschreiten die abgerufenen Daten die maximale Datenlänge, die Google Chrome in einem Cookie akzeptiert. Als Konsequenz wird kein Cookie gesetzt, und die Daten werden zweimal geladen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p112">Different web browsers have different limits regarding how much data can be stored in a cookie. In this example, the retrieved data exceeds the maximum length of what can be stored in a cookie in Google Chrome. As a result, no cookie is being set and the data is loaded twice.</span></span>

<span data-ttu-id="c4ff9-p113">Nun wissen Sie, dass Sie Cookies verwenden können, um Daten zwischen verschiedenen Webparts auszutauschen, vorausgesetzt, die betreffende Datenmenge ist nicht zu groß. Diese Methode hat jedoch auch Nachteile. Ähnlich wie Variablen mit globaler Bereichsdefinition sind auch Cookies für alle Elemente auf einer Seite oder sogar im gesamten Portal verfügbar und könnten von ihnen überschrieben werden. Darüber hinaus senden Webbrowser Cookies zusammen mit ausgehenden Anforderungen und rufen sie zusammen mit eingehenden Antworten ab, was beim Laden von Informationen im Portal zu mehr Overhead führt. Ein weiterer wichtiger Aspekt: Cookies werden dauerhaft im Webbrowser aufbewahrt. Daher sollten Sie in einem Cookie niemals vertrauliche Informationen speichern.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p113">While you could use cookies to share data between web parts, assuming the data that you want to share is not too large, there are some downsides to using cookies. Similar to globally-scoped variables, cookies are available to all elements on the page, or even across the whole portal and could be overwritten by them. Additionally, web browsers send cookies with outgoing requests and retrieve them with incoming responses which adds overhead to loading information in the portal. Another important thing that you should consider is that cookies are persisted in the web browser and you should never store any confidential information in them.</span></span>

## <a name="store-the-retrieved-data-in-session-or-local-storage"></a><span data-ttu-id="c4ff9-155">Speichern der abgerufenen Daten im Sitzungsspeicher oder im lokalen Speicher</span><span class="sxs-lookup"><span data-stu-id="c4ff9-155">Store the Retrieved Data in Session or Local Storage</span></span>

<span data-ttu-id="c4ff9-p114">Als Alternative zu Cookies können Sie Daten im Sitzungsspeicher oder im lokalen Speicher speichern. Ähnlich wie beim Einsatz von Cookies können Sie auch bei Verwendung des Browserspeichers die Daten dauerhaft für nachfolgende Anforderungen sowie seitenübergreifend verfügbar machen. Gegenüber Cookies hat der Browserspeicher den Vorteil, dass die dort gespeicherten Daten nicht zusammen mit ausgehenden Anforderungen gesendet werden. Außerdem können Sie im Browserspeicher mehr Daten speichern als in einem Cookie. Anders als Cookies können Sie im Browserspeicher jedoch nur Zeichenfolgenwerte speichern. Müssen komplexere Objekte gespeichert werden, müssen Sie diese also zuerst serialisieren, beispielsweise mit der nativen Methode `JSON.stringify()`.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p114">An alternative to using cookies is storing data in session or local storage. Similar to cookies, browser storage allows you to persist data not just for subsequent requests but also across pages. The benefits of using browser storage over using cookies are that data stored in browser storage is not sent with outgoing requests and you can store more data than in a cookie. Comparable to cookies, browser storage is capable of storing only string values. So if you need to store more complex objects, you will need to serialize them first using, for example, the native `JSON.stringify()` method.</span></span>

<span data-ttu-id="c4ff9-p115">Sollen die Daten nur für die Dauer der aktuellen Sitzung gespeichert werden, sollten Sie den Sitzungsspeicher verwenden. Sollen die Daten für einen längeren Zeitraum verfügbar sein, ist der lokale Speicher das Mittel der Wahl. Im lokalen Speicher gespeicherte Daten laufen nicht ab. Sie müssen sie selbst löschen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p115">If you want data to be stored only during the current session, you should use session storage. If the data should be persisted for a longer period of time you should use local storage instead. Data stored in local storage doesn't expire and it's up to you to clear it.</span></span>

<span data-ttu-id="c4ff9-164">Der oben implementierte Datenzugriffsdienst auf Basis von Cookies lässt sich ganz einfach so anpassen, dass stattdessen der lokale Speicher verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-164">The previously used implementation of the data access service based on cookies can easily be adapted to use local storage instead:</span></span>

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    private static storageKey: string = 'recentDocuments';

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            let loadedData: IDocument[] = localStorage ? JSON.parse(localStorage.getItem(DocumentsService.storageKey)) : undefined;
            if (loadedData) {
                // data already loaded so reuse
                resolve(loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                if (localStorage) {
                    localStorage.setItem(DocumentsService.storageKey, JSON.stringify(loadedData));
                }
                (window as any).loadingData = false;
                resolve(loadedData);
            }
        });
    }
}
```

<br/>

<span data-ttu-id="c4ff9-p116">Die Implementierung eines solchen Diensts ähnelt der Implementierung der auf Cookies basierenden Variante sehr. Beachten Sie jedoch Folgendes: Der Browserspeicher kann vom Benutzer deaktiviert werden. Sie sollten also immer prüfen, ob er auch verfügbar ist, bevor Sie Vorgänge auf ihn anwenden. Ebenso wie Cookies wird auch der lokale Speicher dauerhaft im Webbrowser aufbewahrt und sollte nicht für vertrauliche Informationen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p116">The implementation of this service is very similar to when using cookies. One thing that you should keep in mind, however, is that browser storage can be disabled by the user and you should always check for its availability before performing operations on it. Just as with cookies, local storage is persisted in the web browser and you should never use it to store any confidential information.</span></span>

## <a name="share-data-through-a-sharepoint-framework-service"></a><span data-ttu-id="c4ff9-168">Gemeinsam Verwendung von Daten über einen SharePoint Framework-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4ff9-168">Share data through a SharePoint Framework service</span></span>

<span data-ttu-id="c4ff9-p117">Als weitere Variante für die gemeinsame Verwendung von Daten zwischen Webparts können Sie einen SharePoint Framework-Dienst erstellen, der Daten zentral lädt und verwaltet. SharePoint Framework-Dienste sind eigenständige Komponenten, die separat von Webparts erstellt werden und als separate Node-Pakete verteilt werden. SharePoint Framework-Webparts können Dienste referenzieren und sie verwenden, um bestimmte von diesen Diensten unterstützte Vorgänge auszuführen, beispielsweise das Laden von Daten.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p117">Another approach to sharing data between web parts, is by building a SharePoint Framework service and using it to centrally load and manage data. SharePoint Framework services are standalone components built separately from web parts and distributed as separate Node packages. SharePoint Framework web parts can reference services and use them to perform specific operations supported by these services, such as loading data.</span></span>

<span data-ttu-id="c4ff9-172">Der in den oben beschriebenen Beispielen demonstrierte Dienst lässt sich mit nur wenigen Modifizierungen in einen SharePoint Framework-Dienst umwandeln.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-172">The existing service, demonstrated in previous examples, with just a few modifications can be transformed into a SharePoint Framework service.</span></span>

<span data-ttu-id="c4ff9-173">Zunächst muss der Dienst eine Schnittstelle implementieren, die die von ihm unterstützten Vorgänge und Eigenschaften darstellt:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-173">First, it needs to implement an interface that represents the operations and properties it supports:</span></span>

```ts
export interface IDocumentsService {
    getRecentDocument(): Promise<IDocument>;
    getRecentDocuments(startFrom: number): Promise<IDocument[]>;
}

export class DocumentsService implements IDocumentsService {
    // ...
}
```

<br/>

<span data-ttu-id="c4ff9-174">Anschließend muss der Dienst einen [Dienstschlüssel](https://docs.microsoft.com/de-DE/javascript/api/sp-core-library/servicekey) festlegen, über den er in SharePoint Framework registriert und von Webparts genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-174">Next, it needs to specify a [service key](https://docs.microsoft.com/de-DE/javascript/api/sp-core-library/servicekey) used to register the service with the SharePoint Framework and consume it from within web parts:</span></span>

```ts
import { ServiceScope, ServiceKey } from '@microsoft/sp-core-library';

export class DocumentsService implements IDocumentsService {
    public static readonly serviceKey: ServiceKey<IDocumentsService> = ServiceKey.create<IDocumentsService>('contoso:DocumentsService', DocumentsService);
    // ...

    constructor(serviceScope: ServiceScope) {
    }

    // ...
}
```

<br/>

<span data-ttu-id="c4ff9-175">Zudem muss jeder SharePoint Framework-Dienst einen Konstruktor haben, der eine Instanz der Klasse [ServiceScope](https://docs.microsoft.com/de-DE/javascript/api/sp-core-library/servicescope) als Parameter akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-175">Each SharePoint Framework service must also have a constructor that accepts an instance of the [ServiceScope](https://docs.microsoft.com/de-DE/javascript/api/sp-core-library/servicescope) class as a parameter.</span></span>

<span data-ttu-id="c4ff9-p118">SharePoint Framework-Dienste können mithilfe desselben Projekt-Buildsystems erstellt werden wie clientseitige SharePoint Framework-Webparts. Ganz wie ein clientseitiges Webpart hat auch ein SharePoint Framework-Dienst ein Manifest. Der Hauptunterschied zu einem Webpartmanifest besteht darin, dass die Eigenschaft `componentType` auf `Library` gesetzt ist:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-p118">SharePoint Framework services can be built using the same project build system as SharePoint Framework client-side web parts. Similar to a client-side web part, a SharePoint Framework service has a manifest. The main difference with the web part manifest is that the `componentType` property is set to `Library`:</span></span>

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "69b1aacd-68f2-4147-8433-8efb08eae331",
  "alias": "DocumentsService",
  "componentType": "Library",
  "version": "0.0.1",
  "manifestVersion": 2
}
```

<br/>

<span data-ttu-id="c4ff9-179">Wenn der SharePoint Framework-Dienst bereit ist, können Sie ihn über ein Webpart nutzen, indem Sie sein Paket referenzieren und ihn dann über seinen Schlüssel abrufen.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-179">Once ready, you can consume the SharePoint Framework service from a web part by referencing its package and retrieving the service using its key.</span></span>

```ts
// ...
import { DocumentsService, IDocumentsService, IDocument } from 'react-recentdocuments-service';
import { ServiceScope } from '@microsoft/sp-core-library';

export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  private documentsService: IDocumentsService;

  protected onInit(): Promise<void> {
    return new Promise<void>((resolve: () => void, reject: (error: any) => void): void => {
      const serviceScope: ServiceScope = this.context.serviceScope.getParent();
      serviceScope.whenFinished((): void => {
        this.documentsService = serviceScope.consume(DocumentsService.serviceKey as any) as IDocumentsService;
        resolve();
      });
    });
  }

  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    this.documentsService.getRecentDocuments(this.properties.startFrom)
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

<br/>

<span data-ttu-id="c4ff9-180">Selbst wenn mehrere Webparts auf der Seite den Dienst referenzieren, wird das Dienstpaket nur ein einziges Mal heruntergeladen, und SharePoint Framework erstellt nur eine einzige Instanz des Dienstes auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-180">Even if there are multiple web parts on the page referencing the same service, its bundle is downloaded only once, and the SharePoint Framework creates only one instance of the service on the page.</span></span> <span data-ttu-id="c4ff9-181">Damit haben Sie einen komfortablen Mechanismus für die zentrale Verarbeitung und Speicherung von Daten auf einer Seite zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-181">This offers you a convenient mechanism for centralizing processing and storing data on a page.</span></span> 

<span data-ttu-id="c4ff9-182">Zwar ist der Einsatz von SharePoint Framework-Diensten komplexer als die zuvor in diesem Artikel beschriebenen Methoden; ein großer Vorteil ist jedoch, dass Sie die Daten von anderen Komponenten auf der Seite isolieren können und damit die Datenintegrität besser gewährleisten können.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-182">While working with SharePoint Framework services is more complex than the previously described approaches, it offers you the great benefits of isolating the data from other components on the page and better handling of its integrity.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4ff9-183">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c4ff9-183">See also</span></span>

- [<span data-ttu-id="c4ff9-184">Tutorial: Gemeinsame Verwendung von Daten zwischen Webparts mithilfe einer globalen Variable</span><span class="sxs-lookup"><span data-stu-id="c4ff9-184">Share data between web parts using a global variable (tutorial)</span></span>](./tutorial-share-data-between-web-parts-global-variable.md)