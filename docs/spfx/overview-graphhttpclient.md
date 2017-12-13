# <a name="overview-of-the-graphhttpclient-class-preview"></a><span data-ttu-id="77507-101">Übersicht über die GraphHttpClient-Klasse (Vorschau)</span><span class="sxs-lookup"><span data-stu-id="77507-101">Overview of the GraphHttpClient class (preview)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77507-102">**GraphHttpClient** befindet sich derzeit in der Preview-Phase. Änderungen sind vorbehalten.</span><span class="sxs-lookup"><span data-stu-id="77507-102">The **GraphHttpClient** is currently in preview and is subject to change.</span></span> <span data-ttu-id="77507-103">Er wird derzeit in Produktionsumgebungen nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="77507-103">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="77507-104">Sie können Microsoft Graph zum Erstellen leistungsstarker Lösungen verwenden, die auf Daten aus Office 365 und anderen Microsoft-Dienste zugreifen.</span><span class="sxs-lookup"><span data-stu-id="77507-104">You can use Microsoft Graph to build powerful solutions that access data from Office 365 and other Microsoft services.</span></span> <span data-ttu-id="77507-105">Um SharePoint-Framework-Lösungen (SPFx) mit Microsoft Graph zu verbinden, müssen Sie eine Azure Active Directory (Azure AD)-Anwendung registrieren und den Autorisierungsfluss abschließen.</span><span class="sxs-lookup"><span data-stu-id="77507-105">To connect SharePoint Framework (SPFx) solutions to Microsoft Graph, you have to register an Azure Active Directory (Azure AD) application and complete the authorization flow.</span></span> <span data-ttu-id="77507-106">Um dies zu vereinfachen, können Sie die SPFx-Klasse **GraphHttpClient** für den direkten Aufruf von Microsoft Graph verwenden, ohne dass zusätzliche Einrichtungsschritte erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="77507-106">To make this easier, you can use the SPFx **GraphHttpClient** class to call Microsoft Graph directly, without any additional setup.</span></span>

## <a name="what-is-the-graphhttpclient-class"></a><span data-ttu-id="77507-107">Was ist die GraphHttpClient-Klasse?</span><span class="sxs-lookup"><span data-stu-id="77507-107">What is the GraphHttpClient class?</span></span>

<span data-ttu-id="77507-108">Die **GraphHttpClient**-Klasse ist im SharePoint-Framework enthalten.</span><span class="sxs-lookup"><span data-stu-id="77507-108">The **GraphHttpClient** class is included as part of the SharePoint Framework.</span></span> <span data-ttu-id="77507-109">Sie funktioniert ähnlich wie das HttpClient-Element, das für die Kommunikation mit Drittanbieter APIs verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="77507-109">It works in a similar way to the HttpClient that you can use to communicate with third-party APIs.</span></span> <span data-ttu-id="77507-110">Die **GraphHttpClient**-Klasse stellt automatisch sicher, dass Ihre Anforderung an Microsoft Graph ein gültiges Bearerzugriffstoken und die erforderlichen Header aufweist.</span><span class="sxs-lookup"><span data-stu-id="77507-110">The **GraphHttpClient** class automatically ensures that your request to Microsoft Graph has a valid bearer access token and the required headers.</span></span> <span data-ttu-id="77507-111">Wenn Sie eine GET- oder POST-Anforderung ausgeben, prüft **GraphHttpClient**, ob diese ein gültiges Zugriffstoken enthält, und wenn dies nicht der Fall ist, ruft die Klasse eins aus einer internen API ab und speichert es für nachfolgende Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="77507-111">When you issue a GET or a POST request, **GraphHttpClient** verifies that it has a valid access token, and if it doesn't, it automatically retrieves one from an internal API and stores it for subsequent requests.</span></span>

<span data-ttu-id="77507-112">Das folgende Beispiel zeigt eine Anforderung an Microsoft Graph, die die **GraphHttpClient**-Klasse verwendet.</span><span class="sxs-lookup"><span data-stu-id="77507-112">The following example shows a request to Microsoft Graph that uses the **GraphHttpClient** class.</span></span>

```ts
// ...
import { GraphHttpClient, GraphHttpClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphHttpClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

<span data-ttu-id="77507-113">So senden Sie eine Anforderung an Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="77507-113">To make a request to Microsoft Graph:</span></span>

- <span data-ttu-id="77507-114">Importieren Sie die **GraphHttpClient**- und **GraphHttpClientResponse**-Module aus dem Paket **@microsoft/sp-http**.</span><span class="sxs-lookup"><span data-stu-id="77507-114">Import the **GraphHttpClient** and **GraphHttpClientResponse** modules from the **@microsoft/sp-http** package.</span></span>
- <span data-ttu-id="77507-115">Verwenden Sie die Instanz von **GraphHttpClient**, die für die `this.context.graphHttpClient`-Eigenschaft zum Ausgeben einer GET- oder POST-Anforderung an Microsoft Graph zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="77507-115">Use the instance of **GraphHttpClient** that's available on the `this.context.graphHttpClient` property to issue a GET or POST request to Microsoft Graph.</span></span>
- <span data-ttu-id="77507-116">Geben Sie als Parameter die Microsoft Graph-API an, die Sie aufrufen möchten (beginnen Sie mit der API-Version ohne führenden Schrägstrich `/`), gefolgt von der **GraphHttpClient**-Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="77507-116">As parameters, specify the Microsoft Graph API that you want to call (start with the API version without a leading `/` - slash), followed by the **GraphHttpClient** configuration.</span></span>
- <span data-ttu-id="77507-117">Optional können Sie zusätzliche Anforderungsheader angeben, die mit den von **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` und `'Content-Type': 'application/json; charset=utf-8'`) festgelegten Standardheadern zusammengeführt werden.</span><span class="sxs-lookup"><span data-stu-id="77507-117">Optionally, you can specify additional request headers that will be merged with the default headers set by **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` and `'Content-Type': 'application/json; charset=utf-8'`).</span></span>

## <a name="considerations-for-using-the-graphhttpclient-class"></a><span data-ttu-id="77507-118">Überlegungen zu der Verwendung der **GraphHttpClient**-Klasse</span><span class="sxs-lookup"><span data-stu-id="77507-118">Considerations for using the **GraphHttpClient** class</span></span>

<span data-ttu-id="77507-119">Die **GraphHttpClient**-Klasse ist eine komfortable Möglichkeit für die Kommunikation mit Microsoft Graph, da sie den Autorisierungsfluss und die Verwaltung von Zugriffstoken abstrahiert.</span><span class="sxs-lookup"><span data-stu-id="77507-119">The **GraphHttpClient** class provides a convenient way to communicate with Microsoft Graph because it abstracts the authorization flow and management of access tokens.</span></span> <span data-ttu-id="77507-120">Da **GraphHttpClient** sich derzeit in der Entwicklervorschau befindet, gibt es einige Aspekte, die Sie vor der Verwendung berücksichtigen sollten.</span><span class="sxs-lookup"><span data-stu-id="77507-120">Because **GraphHttpClient** is currently in developer preview, there are some considerations that you should take into account before using it.</span></span>

### <a name="use-for-microsoft-graph-access-only"></a><span data-ttu-id="77507-121">Verwendung ausschließlich zum Zugriff auf Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="77507-121">Use for Microsoft Graph access only</span></span>

<span data-ttu-id="77507-122">Verwenden Sie die **GraphHttpClient**-Klasse ausschließlich für den Zugriff auf Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="77507-122">Use the **GraphHttpClient** class only to access Microsoft Graph.</span></span> <span data-ttu-id="77507-123">Die in der Anforderung angegebene URL muss mit der Version der Microsoft Graph-API beginnen (entweder **v1.0** oder **beta**), gefolgt von dem API-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="77507-123">The GraphHttpClient is meant to be used only for accessing the Microsoft Graph. The URL specified in the request must begin with the version of the Microsoft Graph API (either **v1.0** or **beta**) followed by the API operation. Any other URL will be rejected with an error.</span></span> <span data-ttu-id="77507-124">Bei jeder anderen URL wird ein Fehler zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="77507-124">Any other URL will return an error.</span></span>

### <a name="permissions"></a><span data-ttu-id="77507-125">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="77507-125">Permissions</span></span>

<span data-ttu-id="77507-126">GraphHttpClient verwendet die Azure AD-Anwendung Office 365 SharePoint Online, um im Namen des aktuellen Benutzers ein gültiges Zugriffstoken für Microsoft Graph abzurufen.</span><span class="sxs-lookup"><span data-stu-id="77507-126">The GraphHttpClient uses the Office 365 SharePoint Online Azure Active Directory application to retrieve a valid access token to the Microsoft Graph on behalf of the current user. The retrieved access token contains two permissions scopes:</span></span> <span data-ttu-id="77507-127">Das abgerufene Zugriffstoken enthält zwei Berechtigungen:</span><span class="sxs-lookup"><span data-stu-id="77507-127">The retrieved access token contains two permissions:</span></span>

- <span data-ttu-id="77507-128">Alle Gruppen lesen und schreiben (Preview) (`Group.ReadWrite.All`)</span><span class="sxs-lookup"><span data-stu-id="77507-128">Read and write all groups (preview) (`Group.ReadWrite.All`)</span></span>
- <span data-ttu-id="77507-129">Alle Verwendungsberichte lesen(`Reports.Read.All`)</span><span class="sxs-lookup"><span data-stu-id="77507-129">Read all usage reports (`Reports.Read.All`)</span></span>

<span data-ttu-id="77507-130">Dies sind die einzigen Berechtigungen, die bei der Verwendung von **GraphHttpClient** verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="77507-130">These are the only permissions that are available when you use **GraphHttpClient**.</span></span> <span data-ttu-id="77507-131">Wenn Sie andere Berechtigungen für Ihre Lösung benötigen, können Sie stattdessen [ADAL JS mit implizitem OAuth-Fluss](web-parts/guidance/call-microsoft-graph-from-your-web-part.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="77507-131">If you need other permissions for your solution, you can use [ADAL JS with implicit OAuth flow](web-parts/guidance/call-microsoft-graph-from-your-web-part.md) instead.</span></span>

### <a name="tokens-are-retrieved-using-an-internal-api"></a><span data-ttu-id="77507-132">Tokenabruf über eine interne API</span><span class="sxs-lookup"><span data-stu-id="77507-132">Tokens are retrieved using an internal API</span></span>

<span data-ttu-id="77507-133">Um ein gültiges Zugriffstoken abzurufen, gibt **GraphHttpClient** eine Webanforderung an den `/_api/SP.OAuth.Token/Acquire`-Endpunkt aus.</span><span class="sxs-lookup"><span data-stu-id="77507-133">To acquire a valid access token, the GraphHttpClient issues a web request to the  endpoint. This API is intended for internal use and you should not communicate with it directly in your solutions.</span></span> <span data-ttu-id="77507-134">Diese API ist nur für die interne Verwendung vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="77507-134">This API is intended for internal use.</span></span> <span data-ttu-id="77507-135">Sie sollten in Ihren Lösungen nicht direkt mit dieser kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="77507-135">You should not communicate with it directly in your solutions.</span></span>

## <a name="see-also"></a><span data-ttu-id="77507-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="77507-136">See also</span></span>

- <span data-ttu-id="77507-137">[GraphClient im Application Customizer aus dem Beispiel für eine moderne Teamwebsite](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span><span class="sxs-lookup"><span data-stu-id="77507-137">[Application Customizer GraphClient from Modern Teamsite sample](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span></span>
- [<span data-ttu-id="77507-138">Verwenden von GraphHttpClient zum Aufrufen von Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="77507-138">Use GraphHttpClient to call Microsoft Graph</span></span>](call-microsoft-graph-using-graphhttpclient.md)
- [<span data-ttu-id="77507-139">Microsoft Graph Dev Center</span><span class="sxs-lookup"><span data-stu-id="77507-139">Microsoft Graph dev center</span></span>](https://developer.microsoft.com/de-DE/graph/)
