# <a name="determine-sharepoint-rest-service-endpoint-uris"></a><span data-ttu-id="c4d7b-101">Ermitteln von URIs von SharePoint-REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="c4d7b-101">Determine SharePoint REST service endpoint URIs</span></span>
<span data-ttu-id="c4d7b-102">Informieren Sie sich über allgemeine Richtlinien zur Ermittlung von URIs von SharePoint REST-Endpunkten mithilfe der Signatur der entsprechenden Clientobjektmodell-APIs.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-102">Learn general guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>
 

 <span data-ttu-id="c4d7b-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

 <span data-ttu-id="c4d7b-106">**Bevor Sie beginnen**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-106">**Before you start**</span></span>
 

-  [<span data-ttu-id="c4d7b-107">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-107">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="c4d7b-108">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="c4d7b-108">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
<span data-ttu-id="c4d7b-109">**Nächste Schritte**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-109">**Next steps**</span></span>
 

-  [<span data-ttu-id="c4d7b-110">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="c4d7b-110">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 

## <a name="sharepoint-rest-endpoint-uri-structure"></a><span data-ttu-id="c4d7b-111">Struktur der URIs von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="c4d7b-111">SharePoint REST endpoint URI structure</span></span>

<span data-ttu-id="c4d7b-p102">Bevor Sie mithilfe des REST-Diensts auf eine SharePoint-Ressource zugreifen können, müssen Sie zuerst den URI-Endpunkt ermitteln, der auf diese Ressource zeigt. Wann immer möglich, bildet die URI für diese REST-Endpunkte die API-Signatur der Ressource im SharePoint-Clientobjektmodell streng nach. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p102">Before you can access a SharePoint resource using the REST service, you first have to figure out the URI endpoint that points to that resource. Whenever possible, the URI for these REST endpoints closely mimics the API signature of the resource in the SharePoint client object model. For example:</span></span>
 

 
 <span data-ttu-id="c4d7b-115">*Clientobjektmodell-Methode:*</span><span class="sxs-lookup"><span data-stu-id="c4d7b-115">*Client object model method:*</span></span> 
 

 
<span data-ttu-id="c4d7b-116">List.GetByTitle(listname).GetItems()</span><span class="sxs-lookup"><span data-stu-id="c4d7b-116">List.GetByTitle(listname).GetItems()</span></span>
 

 
 <span data-ttu-id="c4d7b-117">*REST-Endpunkt:*</span><span class="sxs-lookup"><span data-stu-id="c4d7b-117">*REST endpoint:*</span></span> 
 

 
 `http://server/site/_api/lists/getbytitle('listname')/items`
 

 
<span data-ttu-id="c4d7b-118">In einigen Fällen unterscheidet sich die Endpunkt-URI aber von der entsprechenden Clientobjektmodell-Signatur, um REST- oder OData-Konventionen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-118">In some cases, however, the endpoint URI differs from the corresponding client object model signature, in order to comply with REST or OData conventions.</span></span>
 

 
<span data-ttu-id="c4d7b-119">Die folgende Abbildung zeigt die allgemeine Syntaxstruktur von SharePoint REST-URIs.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-119">The following figure shows the general syntax structure of SharePoint REST URIs.</span></span> 
 

 

<span data-ttu-id="c4d7b-120">**Syntaxstruktur von SharePoint REST-URIs**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-120">**SharePoint REST URI syntax structure**</span></span>

 

 
![SharePoint REST-Anforderungssyntax](../../images/SPF15Con_REST_OverallSyntax.png)
 
<span data-ttu-id="c4d7b-122">Einige Endpunkte für SharePoint-Ressourcen weichen von dieser Syntaxstruktur ab:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-122">Some endpoints for SharePoint resources deviate from this syntax structure:</span></span>
 

 

 

- <span data-ttu-id="c4d7b-123">Methoden, die komplexe Typen als Parameter erfordern.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-123">Methods that require complex types as parameters.</span></span> 
    
    <span data-ttu-id="c4d7b-124">Wenn die entsprechende Clientobjektmodell-Methode erfordert, dass komplexe Typen als Parameter übergeben werden, kann der REST-Endpunkt wegen REST-Einschränkungen von dieser Syntaxstruktur abweichen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-124">If the corresponding client object model method requires that complex types are passed as parameters, the REST endpoint may deviate from this syntax construction to account for REST limitations.</span></span>
    
 
- <span data-ttu-id="c4d7b-125">Statische Methoden und Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-125">Static methods and properties.</span></span> 
    
    <span data-ttu-id="c4d7b-126">REST-Endpunkte weichen von dieser Syntaxstruktur bei URIs ab, die statische Methoden und Eigenschaften darstellen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-126">REST endpoints deviate from this syntax structure for URIs that represent static methods and properties.</span></span>
    
 

## <a name="determine-sharepoint-rest-service-endpoints"></a><span data-ttu-id="c4d7b-127">Ermitteln von SharePoint-REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="c4d7b-127">Determine SharePoint REST service endpoints</span></span>

<span data-ttu-id="c4d7b-128">Befolgen Sie diese Schritte, um einen REST-Endpunkt für eine SharePoint-Ressource zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-128">To construct a REST endpoint for a SharePoint resource, follow these steps:</span></span>
 

 

1. <span data-ttu-id="c4d7b-129">Starten Sie mit der REST-Dienstreferenz:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-129">Start with the REST service reference:</span></span>
    
     `http://server/site/_api`
    
 
2. <span data-ttu-id="c4d7b-p103">Geben Sie den entsprechenden Einstiegspunkt an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p103">Specify the appropriate entry point. For example:</span></span>
    
     `http://server/site/_api/web`
    
 
3. <span data-ttu-id="c4d7b-p104">Navigieren Sie vom Einstiegspunkt zu den spezifischen Ressourcen, auf die Sie zugreifen möchten. Dabei müssen Sie auch Parameter für Endpunkte angeben, die Methoden im Clientobjektmodell entsprechen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p104">Navigate from the entry point to the specific resources you want to access. This includes specifying parameters for endpoints that correspond to methods in the client object model. For example:</span></span>
    
     `http://server/site/_api/web/lists/getbytitle('listname')`
    
 

### <a name="reference-the-sharepoint-rest-service-in-your-endpoint-uri"></a><span data-ttu-id="c4d7b-135">Referenzieren Sie den SharePoint REST-Dienst in Ihrem Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="c4d7b-135">Reference the SharePoint REST service in your endpoint URI</span></span>

<span data-ttu-id="c4d7b-p105">Verwenden Sie `_api`, um den SharePoint REST-Dienst in Ihren Endpunkt-URIs zu kennzeichnen. Der REST-Dienst ist Teil des Webdiensts „client.svc“. Um die Erstellung von REST-URIs zu erleichtern und den REST URI-Basispfad zu kürzen, verwendet der REST-Dienst `_api`, wodurch der explizite Verweis auf den Webdienst „client.svc“ nicht mehr erforderlich ist. URIs, die auf den Webdienst „client.svc“ verweisen, werden vom REST-Dienst jedoch weiterhin erkannt und akzeptiert. Sie können z. B. `http://server/site/_vti_bin/client.svc/web/lists` anstelle von `http://server/site/_api/web/lists` verwenden. Allerdings ist `_api` die bevorzugte Konvention. URLs haben maximal 256 Zeichen. Mit `_api` wird der Basis-URI verkürzt und es bleiben mehr Zeichen für die Erstellung der verbleibenden URL übrig.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p105">Use  `_api` to denote the SharePoint REST service in your endpoint URIs. The REST service is part of the client.svc web service. However, to make REST URI construction easier and to shorten the base REST URI path, the REST service uses `_api` to abstract away the need to explicitly reference the client.svc web service. The REST service still recognizes and accepts URIs that reference the client.svc web service. For example, you can use `http://server/site/_vti_bin/client.svc/web/lists` instead of `http://server/site/_api/web/lists`. However, using  `_api` is the preferred convention. URLs have a 256 character limit, so using `_api` shortens the base URI, leaving more characters for use in constructing the rest of the URL.</span></span>
 

 

### <a name="specify-entry-points-for-the-sharepoint-rest-service"></a><span data-ttu-id="c4d7b-143">Angeben von Einstiegspunkten für den SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-143">Specify entry points for the SharePoint REST service</span></span>

<span data-ttu-id="c4d7b-p106">Die wichtigsten Einstiegspunkte für den REST-Dienst sind die Websitesammlung und die Website des angegebenen Kontexts. Damit entsprechen diese Einstiegspunkte den Eigenschaften **ClientContext.Site** und **ClientContext.Web** in den Clientobjektmodellen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p106">The main entry points for the REST service represent the site collection and site of the specified context. In this way, these entry points correspond to the  **ClientContext.Site** property and **ClientContext.Web** property in the client object models.</span></span>
 

 
<span data-ttu-id="c4d7b-146">Gehen Sie folgendermaßen vor, um auf eine bestimmte Websitesammlung zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-146">To access a specific site collection, use the following construction:</span></span>
 

 
 `http://server/site/_api/site`
 

 
<span data-ttu-id="c4d7b-147">Gehen Sie folgendermaßen vor, um auf eine bestimmte Website zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-147">To access a specific site, use the following construction:</span></span>
 

 
 `http://server/site/_api/web`
 

 
<span data-ttu-id="c4d7b-148">Wobei  *server*  den Namen des Servers darstellt und  *site*  für den Namen der oder den Pfad zur entsprechenden Website steht.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-148">Where  *server*  represents the name of the server, and *site*  represents the name of, or path to, the specific site.</span></span>
 

 
<span data-ttu-id="c4d7b-p107">Zusätzlich zu  `/site` und `/web` enthält der REST-Dienst mehrere Zugriffspunkte, die Entwicklern erlauben, zu spezifischen Funktionen zu navigieren. In der folgenden Tabelle sind einige dieser Zugriffspunkte aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p107">In addition to  `/site` and `/web`, the REST service includes several other access points that enable developers to navigate to specific functionality. The table below lists some of these access points.</span></span>
 

 


|<span data-ttu-id="c4d7b-151">**Funktionsbereich**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-151">**Feature area**</span></span>|<span data-ttu-id="c4d7b-152">**Zugriffspunkt**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-152">**Access point**</span></span>|
|:-----|:-----|
|<span data-ttu-id="c4d7b-153">Website</span><span class="sxs-lookup"><span data-stu-id="c4d7b-153">Site</span></span>|<span data-ttu-id="c4d7b-154">http:// _server/site_/_api/site</span><span class="sxs-lookup"><span data-stu-id="c4d7b-154">http:// _server/site_/_api/site</span></span>|
|<span data-ttu-id="c4d7b-155">Web</span><span class="sxs-lookup"><span data-stu-id="c4d7b-155">Web</span></span>|<span data-ttu-id="c4d7b-156">http:// _server/site_/_api/web</span><span class="sxs-lookup"><span data-stu-id="c4d7b-156">http:// _server/site_/_api/web</span></span>|
|<span data-ttu-id="c4d7b-157">Benutzerprofil</span><span class="sxs-lookup"><span data-stu-id="c4d7b-157">User Profile</span></span>|<span data-ttu-id="c4d7b-158">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span><span class="sxs-lookup"><span data-stu-id="c4d7b-158">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span></span>|
|<span data-ttu-id="c4d7b-159">Suche</span><span class="sxs-lookup"><span data-stu-id="c4d7b-159">Search</span></span>|<span data-ttu-id="c4d7b-160">http:// _server/site_/_api/search</span><span class="sxs-lookup"><span data-stu-id="c4d7b-160">http:// _server/site_/_api/search</span></span>|

### <a name="navigate-to-the-specific-resources-you-want-to-access"></a><span data-ttu-id="c4d7b-161">Navigieren Sie zu den entsprechenden Ressourcen, auf die Sie zugreifen möchten</span><span class="sxs-lookup"><span data-stu-id="c4d7b-161">Navigate to the specific resources you want to access</span></span>

<span data-ttu-id="c4d7b-p108">Erstellen Sie von hier aus spezifischere REST-Endpunkte, indem Sie das Objektmodell durchlaufen. Verwenden Sie dazu die Namen der APIs aus dem Clientobjektmodell, getrennt durch einen Schrägstrich (/). Die nachfolgende Tabelle zeigt Beispiele für Clientobjektmodell-Aufrufe und den entsprechenden REST-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p108">From here, construct more specific REST endpoints by ''walking" the object model, using the names of the APIs from the client object model separated by a forward slash (/). The table below shows examples of client object model calls and the equivalent REST endpoint.</span></span> 
 

 


|<span data-ttu-id="c4d7b-164">** Clientobjektmodell-API **</span><span class="sxs-lookup"><span data-stu-id="c4d7b-164">**Client object model API **</span></span>|<span data-ttu-id="c4d7b-165">**REST-Endpunkt**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-165">**REST endpoint**</span></span>|
|:-----|:-----|
|<span data-ttu-id="c4d7b-166">ClientContext.Web.Lists</span><span class="sxs-lookup"><span data-stu-id="c4d7b-166">ClientContext.Web.Lists</span></span>|<span data-ttu-id="c4d7b-167">http:// _server_/ _site_/_api/web/lists</span><span class="sxs-lookup"><span data-stu-id="c4d7b-167">http:// _server_/ _site_/_api/web/lists</span></span>|
|<span data-ttu-id="c4d7b-168">ClientContext.Web.Lists[guid]</span><span class="sxs-lookup"><span data-stu-id="c4d7b-168">ClientContext.Web.Lists[guid]</span></span>|<span data-ttu-id="c4d7b-169">http:// _server_/ _site_/_api/web/lists(' _guid_')</span><span class="sxs-lookup"><span data-stu-id="c4d7b-169">http:// _server_/ _site_/_api/web/lists(' _guid_')</span></span>|
|<span data-ttu-id="c4d7b-170">ClientContext.Web.Lists.GetByTitle("Title")</span><span class="sxs-lookup"><span data-stu-id="c4d7b-170">ClientContext.Web.Lists.GetByTitle("Title")</span></span>|<span data-ttu-id="c4d7b-171">http:// _server_/ _site_/_api/web/lists/getbytitle(' _Title_')</span><span class="sxs-lookup"><span data-stu-id="c4d7b-171">http:// _server_/ _site_/_api/web/lists/getbytitle(' _Title_')</span></span>|
<span data-ttu-id="c4d7b-p109">Bei Endpunkt-URIs wird die Groß- und Kleinschreibung nicht beachtet. Verwenden Sie in der vorhergehenden Tabelle z. B. `/getbytitle`, um das REST-Äquivalent der **GetByTitle()**-Methode anzugeben.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p109">Endpoint URIs are case-insensitive. In the previous table, for example, use  `/getbytitle` to specify the REST equivalent of the **GetByTitle()** method.</span></span>
 

 

## <a name="specify-parameters-in-rest-endpoint-uris"></a><span data-ttu-id="c4d7b-174">Angeben von Parametern in REST-Endpunkt-URIs</span><span class="sxs-lookup"><span data-stu-id="c4d7b-174">Specify parameters in REST endpoint URIs</span></span>

<span data-ttu-id="c4d7b-p110">SharePoint erweitert die OData-Spezifikation, indem Sie Ihnen die Verwendung von Parametern ermöglicht, um Methodenparameter und Indexwerte anzugeben. Dadurch werden mögliche Probleme aufgrund von Mehrdeutigkeit in URIs vermieden, die mehrere Parameter mit dem gleichen Namen enthalten. Die folgenden zwei URIs enthalten z. B. Parameter mit dem gleichen Namen:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p110">SharePoint extends the OData specification to enable you to use parentheses to specify method parameters and index values. This prevents potential disambiguation issues in URIs that contain multiple parameters with the same name. For example, the following two URIs contain parameters that have the same name:</span></span>
 

 
 `http://server/site/_api/web/lists/getByTitle('Announcements')/fields/getByTitle('Description')`
 

 
 `http://server/site/_api/web/lists('<guid>')/fields/getById('<guid>')`
 

 
<span data-ttu-id="c4d7b-p111">Um mehrere Parameter anzugeben, schließen Sie den Parameter als ein Namen-Wert-Paar ein, und trennen Sie die Parameter mit Kommas. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p111">To specify multiple parameters, include the parameter as a name-value pair, and separate the parameters with commas. For example:</span></span>
 

 
 `http://server/site/_api/web/getAvailableWebTemplates(lcid=1033, includeCrossLanguage=true)`
 

 
<span data-ttu-id="c4d7b-180">Die folgende Abbildung zeigt die Syntax von SharePoint REST-Parametern.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-180">The following figure shows the SharePoint REST parameter syntax.</span></span>
 

 

<span data-ttu-id="c4d7b-181">**Syntax von SharePoint REST-Parametern**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-181">**SharePoint REST parameter syntax**</span></span>

 

 
![Syntax von Methodenparametern des SharePoint REST-Diensts](../../images/SPF15Con_REST_parameterSyntax.png)
 

### <a name="complex-types-as-parameters-for-the-rest-service"></a><span data-ttu-id="c4d7b-183">Komplexe Typen als Parameter für den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-183">Complex types as parameters for the REST service</span></span>

<span data-ttu-id="c4d7b-p112">Einige Methoden im Clientobjektmodell erfordern eine große Nutzlast als Parameter. Damit die Funktionsparität der REST-Endpunkte mit den entsprechenden Clientobjektmodell-APIs erhalten bleibt, müssen die Endpunkte einen komplexen Typ als Parameter akzeptieren. In diesen Fällen wird das vorhandene OData-Protokoll durch den REST-Dienst erweitert. Dadurch wird ermöglicht, dass diese REST-Endpunkte einen einzigen komplexen Typ als Parameter akzeptieren. Dies gilt nur für **POST**-Vorgänge. Sie müssen den komplexen Typ entsprechend der OData-Standards im [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties)- oder [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties)-Format übergeben.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p112">Some methods in the client object model require a large payload as a parameter. For REST endpoints to maintain functionality parity with their corresponding client object model APIs, the endpoints must accept a complex type as a parameter. In these cases, the REST service extends the existing OData protocol to enable these REST endpoints to accept a single complex type as a parameter. This applies to  **POST** operations only, and you have to pass the complex type in [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) format or [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) format, according to OData standards.</span></span>
 

 
<span data-ttu-id="c4d7b-p113">So verwendet beispielsweise die Methode **ListCollection.Add** ein **Microsoft.SharePoint.Client.ListCreationInformation**-Objekt als Parameter. Um eine Liste zu einer bestimmten Website hinzuzufügen, erstellen Sie den entsprechenden REST-Endpunkt wie folgt:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p113">For example, the  **ListCollection.Add** method takes a **Microsoft.SharePoint.Client.ListCreationInformation** object as a parameter. To add a list to a specified site, construct the appropriate REST endpoint as follows:</span></span>
 

 
 `http://server/site/_api/web/lists/add`
 

 
<span data-ttu-id="c4d7b-190">Übergeben Sie dann den komplexen Typ im Textkörper der Anforderung im JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-190">Then, pass the complex type in the request body, formatted here using JSON.</span></span>
 

 



```
{ "d" : {
   "results": {
     "__metadata": {
       "type": "SP.ListCreationInformation"
     }, 
     "CustomSchemaXml": "…large payload…/", 
     "Description": "desc", 
     "DocumentTemplateType": "1", 
     "TemplateType": "101", 
     "Title": "Announcements"
   }
} 
}

```


### <a name="using-parameter-aliases-in-rest-service-calls"></a><span data-ttu-id="c4d7b-191">Verwenden von Parameter-Aliasen in REST-Dienstaufrufen</span><span class="sxs-lookup"><span data-stu-id="c4d7b-191">Using parameter aliases in REST service calls</span></span>

<span data-ttu-id="c4d7b-p114">Sie können die "Parameteraliasing"-Semantik in OData verwenden, um Parameter an einen SharePoint-REST-Endpunkt zu übergeben. Beim Parameteraliasing wird der Parameterwert mit einem Alias im Parameteraufruf identifiziert, und der tatsächliche Wert wird in der Abfragezeichenfolge der URI angegeben. So können Sie mehr Zeichentypen und eine einheitliche Formatierung mithilfe der Abfragezeichenfolge unterstützen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p114">You can use the "parameter aliasing" semantic in OData to pass parameters to a SharePoint REST endpoint. In parameter aliasing, the parameter value is identified with an alias in the parameter call, and the actual value is specified in the query string of the URI. This enables you to support more types of characters and consistent formatting by using the query string.</span></span>
 

 
<span data-ttu-id="c4d7b-195">Die folgenden zwei REST-URIs sind z. B. äquivalent:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-195">For example, the following two REST URIs are equivalent:</span></span> 
 

 
 <span data-ttu-id="c4d7b-196">*Geben Sie den Parameterwert direkt an:*</span><span class="sxs-lookup"><span data-stu-id="c4d7b-196">*Specify the parameter value directly:*</span></span> 
 

 
 `http://server/site/_api/web/applyWebTemplate("STS#0")`
 

 
 <span data-ttu-id="c4d7b-197">*Verwenden Sie einen Parameteralias, und geben Sie den tatsächlichen Parameterwert in der Abfragezeichenfolge der URI an:*</span><span class="sxs-lookup"><span data-stu-id="c4d7b-197">*Use a parameter alias, and specify the actual parameter value in the query string of the URI:*</span></span> 
 

 
 `http://server/site/_api/web/applyWebTemplate(title=@template)?@template="STS#0"`
 

 
<span data-ttu-id="c4d7b-p115">Das Übergeben von komplexen Typen per Parameteraliasing wird vom SharePoint-REST-Dienst allerdings nicht unterstützt. So wird z. B. die folgende URI nicht unterstützt, die einen komplexen Typ im Parameteralias enthält:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p115">However, the SharePoint REST service does not support passing complex types via parameter aliasing. For example, the following URI, which contains a complex type in the parameter alias, is not supported:</span></span>
 

 
 `http://server/site/_api/userProfiles/People(7)/GetWorkplace(@address)?@address={"__metadata":{"type: "ODataDemo.Address"},"Street":"NE 228th", "City":"Sammamish","State":"WA","ZipCode":"98074","Country": "USA"}`
 

 

<span data-ttu-id="c4d7b-200">**Parameter-Aliasing-Syntax des SharePoint REST-Diensts**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-200">**SharePoint REST service parameter aliasing syntax**</span></span>

 

 
![Parameter-Aliasing-Syntax des SharePoint REST-Diensts](../../images/SPF15Con_REST_parameterAliasSyntax.png)
 

 

 

### <a name="specifying-dictionaries-as-parameter-values"></a><span data-ttu-id="c4d7b-202">Angeben von Wörterbüchern als Parameterwerte</span><span class="sxs-lookup"><span data-stu-id="c4d7b-202">Specifying dictionaries as parameter values</span></span>

<span data-ttu-id="c4d7b-203">Bei REST-Endpunkten, die Methoden entsprechen, die `Dictionary<String, String>`-Wörterbücher als Parameter verwenden, übergeben Sie das Wörterbuch als Serie von durch Kommas getrennten Namen-Wert-Paaren in der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-203">For REST endpoints that correspond to methods that take  `Dictionary<String, String>` dictionaries as parameters, pass the dictionary as a series of comma delimited name-value pairs in the query string.</span></span>
 

 

<span data-ttu-id="c4d7b-204">**REST-Dienstsyntax für Wörterbuchparameter**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-204">**REST service syntax for Dictionary parameters**</span></span>

 

 
![REST-Dienstsyntax für Wörterbuchparameter](../../images/SPF15Con_REST_parameterDictionarySyntax.png)
 
<span data-ttu-id="c4d7b-206">Ein `Dictionary<String, object>` wird als Mehrfachwertobjekt namens „KeyedPropertyValue“ mit den folgenden Zeichenfolgeneigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-206">A  `Dictionary<String, object>` is represented as a multi-value object, named KeyedPropertyValue, with the following string properties:</span></span>
 

 

 

-  <span data-ttu-id="c4d7b-207">**Key** Der Schlüssel des Mehrfachwertobjekts.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-207">**Key** The key of the multi-value object.</span></span>
    
 
-  <span data-ttu-id="c4d7b-208">**Value** Der Wert des Objekts</span><span class="sxs-lookup"><span data-stu-id="c4d7b-208">**Value** The value of the object</span></span>
    
 
-  <span data-ttu-id="c4d7b-p116">**ValueType** Der Werttyp des Objekts Für einfache Werttypen, die vorhandenen Entity Data Model(EDM)-Typen zugeordnet sind, gibt der REST-Dienst die entsprechende EDM-Zeichenfolge zurück, z. B. "Edm.String." Anderenfalls gibt der REST-Dienst den von der Funktion **Type.ToString** zurückgegebenen Werttyp zurück.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p116">**ValueType** The value type of the object. For simple value types that map to existing Entity Data Model (EDM) types, the REST service returns the appropriate EDM type string; for example, "Edm.String." If not, the REST service returns the value type returned by the **Type.ToString** function.</span></span>
    
 

### <a name="specifying-parameter-values-in-the-query-string"></a><span data-ttu-id="c4d7b-212">Angeben von Parameterwerten in der Abfragezeichenfolge</span><span class="sxs-lookup"><span data-stu-id="c4d7b-212">Specifying parameter values in the query string</span></span>

<span data-ttu-id="c4d7b-p117">Wenn Ihre REST-URI in einem Methodenaufruf endet, können Sie Abfragezeichenfolgensyntax verwenden, um die Parameterwerte der Methode anzugeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p117">If your REST URI terminates in a method call, you can use query string syntax to specify the parameter values of the method. For example:</span></span>
 

 
 `http://<server>/<site>/_api/web/applyWebTemplate?template="STS#0"`
 

 
<span data-ttu-id="c4d7b-215">Die unten stehende Abbildung zeigt die REST-Dienstsyntax für Parameter in Abfragezeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-215">the figure below shows the REST service syntax for parameters in query string.</span></span>
 

 

<span data-ttu-id="c4d7b-216">**REST-Dienstsyntax für Parameter in Abfragezeichenfolgen**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-216">**REST service syntax for parameters in query string**</span></span>

 

 
![REST-Dienstsyntax für Parameter in Abfragezeichenfolgen](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="specifying-static-methods-and-properties-as-rest-service-uris"></a><span data-ttu-id="c4d7b-218">Angeben von statischen Methoden und Eigenschaften als REST-Dienst-URIs</span><span class="sxs-lookup"><span data-stu-id="c4d7b-218">Specifying static methods and properties as REST service URIs</span></span>

<span data-ttu-id="c4d7b-p118">Verwenden Sie zum Erstellen von URIs, die statischen Methoden oder Eigenschaften entsprechen, den entsprechenden API-Namen aus dem Objektmodell „ECMAScript“, beginnend mit der Namespace-Deklaration und dargestellt mit Punkt. Zum Beispiel würde das REST-Äquivalent von [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/en-us/library/ee658947.aspx) im Clientobjektmodell ECMAScript wie folgt lauten:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p118">To construct URIs that correspond to static methods or properties, use the corresponding API name from the ECMAScript object model, starting with the namespace declaration and using dot notation. For example,  [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/en-us/library/ee658947.aspx) in the ECMAScript client object model would have the following REST equivalent:</span></span>
 

 
 `http://server/site/_api/SP.Utilities.Utility.getImageUrl('imageName')`
 

 
<span data-ttu-id="c4d7b-p119">Statische Methoden können allerdings nur direkt aufgerufen werden und sind als Teil einer größeren URI-Komposition nicht zulässig. Das direkte Aufrufen der Methode **SP.Utility.AssetsLibrary** in REST ist z. B. wie folgt zulässig:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-p119">However, static properties can be accessed only directly, and are not allowed as part of a larger URI composition. For example, directly accessing the  **SP.Utility.AssetsLibrary** method in REST is allowable, as follows:</span></span>
 

 
 `http://server/site/_api/SP.Utility.assetsLibrary/id`
 

 
<span data-ttu-id="c4d7b-223">Die Verwendung des Ressourcenspeicherorts als Parameter für eine komplexere URI, wie im folgenden Beispiel gezeigt, ist allerdings nicht zulässig:</span><span class="sxs-lookup"><span data-stu-id="c4d7b-223">However, using that resource location as a parameter for a more complex URI, as shown in the following example, is not allowed:</span></span>
 

 
 `http://server/site/_api/getList(~SP.Utility/assetsLibrary/id)`
 

 
<span data-ttu-id="c4d7b-224">Die unten stehende Abbildung zeigt die Syntax von statischen Membern des SharePoint REST-Diensts.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-224">The figure below shows the SharePoint REST service static member syntax.</span></span>
 

 

<span data-ttu-id="c4d7b-225">**Syntax von statischen Membern des SharePoint REST-Diensts**</span><span class="sxs-lookup"><span data-stu-id="c4d7b-225">**SharePoint REST service static member syntax**</span></span>

 

 
![REST-Dienstsyntax für Parameter in Abfragezeichenfolgen](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="next-steps"></a><span data-ttu-id="c4d7b-227">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c4d7b-227">Next steps</span></span>

<span data-ttu-id="c4d7b-228">Wenn Sie die von einem Endpunkt angeforderten Daten auswählen, filtern oder sortieren möchten, unterstützt der SharePoint-REST-Dienst eine breite Palette von OData-Abfragezeichenfolgen-Operatoren.</span><span class="sxs-lookup"><span data-stu-id="c4d7b-228">If you want to select, filter, or order the data you requested from an endpoint, the SharePoint REST service supports a wide range of OData query string operators.</span></span> 
 

 

## <a name="additional-resources"></a><span data-ttu-id="c4d7b-229">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c4d7b-229">Additional resources</span></span>
<span data-ttu-id="c4d7b-230"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4d7b-230"></span></span>


-  [<span data-ttu-id="c4d7b-231">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-231">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="c4d7b-232">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="c4d7b-232">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="c4d7b-233">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="c4d7b-233">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="c4d7b-234">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="c4d7b-234">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="c4d7b-235">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="c4d7b-235">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [<span data-ttu-id="c4d7b-236">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="c4d7b-236">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [<span data-ttu-id="c4d7b-237">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="c4d7b-237">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="c4d7b-238">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-238">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)
    
 
-  [<span data-ttu-id="c4d7b-239">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="c4d7b-239">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

