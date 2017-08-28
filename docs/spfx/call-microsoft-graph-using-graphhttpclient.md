# <a name="call-microsoft-graph-using-the-sharepoint-framework-graphhttpclient"></a><span data-ttu-id="8d993-101">Aufrufen von Microsoft Graph mit SharePoint Framework GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="8d993-101">Call Microsoft Graph using the SharePoint Framework GraphHttpClient</span></span>

<span data-ttu-id="8d993-p101">Mit Microsoft Graph können Sie leistungsfähige Lösungen erstellen, die Daten aus den anderen Office 365-Diensten verwenden. Bisher war es nicht ganz einfach, SharePoint Framework-Lösungen mit Microsoft Graph zu verbinden: Es war nötig, eine Azure Active Directory-Anwendung zu registrieren und den Autorisierungsfluss zu durchlaufen. Mit SharePoint Framework GraphHttpClient können Sie Microsoft Graph direkt aufrufen, ohne zusätzliche Einrichtungsschritte.</span><span class="sxs-lookup"><span data-stu-id="8d993-p101">Using the Microsoft Graph you can build powerful solutions that use data from the different services that are a part of Office 365. In the past, connecting SharePoint Framework solutions to the Microsoft Graph was challenging, as it required you to register an Azure Active Directory application and complete the authorization flow. With the SharePoint Framework GraphHttpClient you can directly call the Microsoft Graph, without any additional setup.</span></span>

> <span data-ttu-id="8d993-105">**Wichtig:** GraphHttpClient befindet sich derzeit in der Developer Preview-Phase und sollte nicht in Produktionsumgebungen eingesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="8d993-105">**Important:** The GraphHttpClient is currently in developer preview and should not be used in production.</span></span>

## <a name="what-is-graphhttpclient"></a><span data-ttu-id="8d993-106">Was ist GraphHttpClient?</span><span class="sxs-lookup"><span data-stu-id="8d993-106">What is GraphHttpClient</span></span>

<span data-ttu-id="8d993-p102">GraphHttpClient ist ein spezialisierter HTTP-Client, der als Teil von SharePoint Framework bereitgestellt wird. Er arbeitet ähnlich wie der Client HttpClient, der zur Kommunikation mit Drittanbieter-APIs eingesetzt werden kann. Zusätzlich zum Funktionsumfang von HttpClient stellt GraphHttpClient automatisch sicher, dass Ihre Anforderungen an Microsoft Graph ein gültiges Bearerzugriffstoken und alle erforderlichen Header enthalten. Bei jeder GET- oder POST-Anforderung überprüft GraphHttpClient, ob ein gültiges Zugriffstoken vorhanden ist. Ist kein solches Token vorhanden, ruft der Client automatisch eines von einer internen API ab und speichert es für zukünftige Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="8d993-p102">GraphHttpClient is a specialized HTTP client provided as a part of the SharePoint Framework. It works similarly to the HttpClient that you can use to communicate with third party APIs. On top of the HttpClient, the GraphHttpClient automatically ensures that your request to the Microsoft Graph has a valid bearer access token and required headers. Whenever you issue a GET or a POST request, the GraphHttpClient verifies that it has a valid access token, and if it doesn't, it automatically retrieves one from an internal API and stores it for subsequent requests.</span></span>

<span data-ttu-id="8d993-111">Unten sehen Sie eine Beispielanforderung an Microsoft Graph über GraphHttpClient:</span><span class="sxs-lookup"><span data-stu-id="8d993-111">A sample request to the Microsoft Graph using the GraphHttpClient looks as follows:</span></span>

```ts
// ...
import { GraphHttpClient, GraphClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

<span data-ttu-id="8d993-p103">Zunächst importieren Sie die Module **GraphHttpClient** und **GraphClientResponse** aus dem Paket **@microsoft/sp-http**. Anschließend senden Sie über die GraphHttpClient-Instanz in der Eigenschaft `this.context.graphHttpClient` eine GET- oder eine POST-Anforderung an Microsoft Graph. Als Parameter geben Sie die Microsoft Graph-API an, die Sie aufrufen möchten (beginnend mit der API-Version ohne führenden Schrägstrich [`/`]), gefolgt von der GraphHttpClient-Konfiguration. Optional können Sie weitere Anforderungsheader angeben, die dann mit den von GraphHttpClient gesetzten Standardheadern (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` und `'Content-Type': 'application/json; charset=utf-8'`) zusammengeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8d993-p103">You start with importing the **GraphHttpClient** and **GraphClientResponse** modules from the **@microsoft/sp-http** package. Next, using the instance of the GraphHttpClient available on the `this.context.graphHttpClient` property, you issue a GET or a POST request to the Microsoft Graph. As the parameters, you specify the Microsoft Graph API that you want to call (starting with the API version without a leading `/` - slash), followed by the GraphHttpClient configuration. Optionally, you can specify additional request headers that will be merged with the default headers set by the GraphHttpClient (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` and `'Content-Type': 'application/json; charset=utf-8'`).</span></span>

## <a name="graphhttpclient-considerations"></a><span data-ttu-id="8d993-116">Wichtige Aspekte bei der Arbeit mit GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="8d993-116">GraphHttpClient considerations</span></span>

<span data-ttu-id="8d993-p104">Der Einsatz von GraphHttpClient ist eine sehr praktische Methode zur Kommunikation mit Microsoft Graph, da der Autorisierungsfluss und die Verwaltung der Zugriffstoken abstrahiert werden. Da sich GraphHttpClient jedoch aktuell noch in der Developer Preview-Phase befindet, gibt es bei der Arbeit mit dem Client einige Aspekte zu bedenken.</span><span class="sxs-lookup"><span data-stu-id="8d993-p104">Using the GraphHttpClient is a very convenient way of communicating with the Microsoft Graph as it abstracts away the authorization flow and management of access tokens. The GraphHttpClient is currently in developer preview and there are some considerations that you should take into account before using it.</span></span>

### <a name="use-for-microsoft-graph-access-only"></a><span data-ttu-id="8d993-119">Verwendung ausschließlich zum Zugriff auf Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="8d993-119">Use for Microsoft Graph access only</span></span>

<span data-ttu-id="8d993-p105">GraphHttpClient ist ausschließlich als Zugriffsclient für Microsoft Graph gedacht. Die in der Anforderung angegebene URL muss mit der Version der Microsoft Graph-API beginnen (entweder **v1.0** oder **beta**), gefolgt vom betreffenden API-Vorgang. Andere URLs werden mit einer Fehlermeldung abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="8d993-p105">The GraphHttpClient is meant to be used only for accessing the Microsoft Graph. The URL specified in the request must begin with the version of the Microsoft Graph API (either **v1.0** or **beta**) followed by the API operation. Any other URL will be rejected with an error.</span></span>

### <a name="available-permission-scopes"></a><span data-ttu-id="8d993-123">Verfügbare Berechtigungsbereiche</span><span class="sxs-lookup"><span data-stu-id="8d993-123">Available permission scopes</span></span>

<span data-ttu-id="8d993-p106">GraphHttpClient verwendet die Azure Active Directory-Anwendung **Office 365 SharePoint Online**, um im Namen des aktuellen Benutzers ein gültiges Zugriffstoken für Microsoft Graph abzurufen. Das abgerufene Zugriffstoken enthält zwei Berechtigungsbereiche:</span><span class="sxs-lookup"><span data-stu-id="8d993-p106">The GraphHttpClient uses the **Office 365 SharePoint Online** Azure Active Directory application to retrieve a valid access token to the Microsoft Graph on behalf of the current user. The retrieved access token contains two permissions scopes:</span></span> 

* <span data-ttu-id="8d993-126">**Alle Gruppen lesen und schreiben (Preview)** (`Group.ReadWrite.All`)</span><span class="sxs-lookup"><span data-stu-id="8d993-126">Read and write all groups</span></span> 
* <span data-ttu-id="8d993-127">**Alle Nutzungsberichte lesen** (`Reports.Read.All`)</span><span class="sxs-lookup"><span data-stu-id="8d993-127">Read all usage reports</span></span> 

<span data-ttu-id="8d993-p107">Aktuell sind für GraphHttpClient nur diese beiden Berechtigungen verfügbar. Falls Sie für Ihre Lösung andere Berechtigungsbereiche benötigen, müssen Sie stattdessen [ADAL JS mit implizitem OAuth-Fluss](web-parts/guidance/call-microsoft-graph-from-your-web-part) verwenden.</span><span class="sxs-lookup"><span data-stu-id="8d993-p107">At this moment these are the only two permissions available when using the GraphHttpClient. If you need other permission scopes in your solution, you have to use [ADAL JS with implicit OAuth flow](web-parts/guidance/call-microsoft-graph-from-your-web-part) instead.</span></span>

### <a name="tokens-are-retrieved-using-an-internal-api"></a><span data-ttu-id="8d993-130">Tokenabruf über eine interne API</span><span class="sxs-lookup"><span data-stu-id="8d993-130">Tokens are retrieved using an internal API</span></span>

<span data-ttu-id="8d993-p108">Zum Abrufen eines gültigen Zugriffstokens sendet GraphHttpClient eine Webanforderung an den Endpunkt `/_api/SP.OAuth.Token/Acquire`. Diese API ist nur zur internen Verwendung gedacht. Ihre Lösungen sollten daher nicht direkt mit ihr kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="8d993-p108">To acquire a valid access token, the GraphHttpClient issues a web request to the `/_api/SP.OAuth.Token/Acquire` endpoint. This API is intended for internal use and you should not communicate with it directly in your solutions.</span></span>

## <a name="more-information"></a><span data-ttu-id="8d993-133">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="8d993-133">More information</span></span>

<span data-ttu-id="8d993-134">Als Praxisbeispiel für die Verwendung von GraphHttpClient finden Sie eine Beispiellösung auf GitHub, unter [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span><span class="sxs-lookup"><span data-stu-id="8d993-134">To see how the GraphHttpClient can be used in practice, see a sample solution on GitHub at [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span></span>

<span data-ttu-id="8d993-135">Weitere Informationen zu Microsoft Graph finden Sie unter [https://developer.microsoft.com/en-us/graph/](https://developer.microsoft.com/en-us/graph/).</span><span class="sxs-lookup"><span data-stu-id="8d993-135">For more information about the Microsoft Graph visit [https://developer.microsoft.com/en-us/graph/](https://developer.microsoft.com/en-us/graph/).</span></span>