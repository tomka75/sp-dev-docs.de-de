---
title: Ermitteln von URIs von SharePoint-REST-Dienstendpunkten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: efe42ece3ee16ebff3f69d71e1e1b1fb7aabf209
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="determine-sharepoint-rest-service-endpoint-uris"></a><span data-ttu-id="32468-102">Ermitteln von URIs von SharePoint-REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="32468-102">Determine SharePoint REST service endpoint URIs</span></span>
<span data-ttu-id="32468-103">Informieren Sie sich über allgemeine Richtlinien zur Ermittlung von URIs von SharePoint-REST-Endpunkten mithilfe der Signatur der entsprechenden Clientobjektmodell-APIs.</span><span class="sxs-lookup"><span data-stu-id="32468-103">Learn general guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>
 
<span data-ttu-id="32468-104">**Bevor Sie beginnen**</span><span class="sxs-lookup"><span data-stu-id="32468-104">**Before you start**</span></span>

-  [<span data-ttu-id="32468-105">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-105">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="32468-106">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="32468-106">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
<span data-ttu-id="32468-107">**Nächste Schritte**</span><span class="sxs-lookup"><span data-stu-id="32468-107">**Next steps**</span></span>

-  [<span data-ttu-id="32468-108">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="32468-108">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)


## <a name="sharepoint-rest-endpoint-uri-structure"></a><span data-ttu-id="32468-109">Struktur der URIs von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="32468-109">SharePoint REST endpoint URI structure</span></span>
<span data-ttu-id="32468-p101">Bevor Sie mithilfe des REST-Diensts auf eine SharePoint-Ressource zugreifen können, müssen Sie zuerst den URI-Endpunkt ermitteln, der auf diese Ressource zeigt. Wann immer möglich, bildet die URI für diese REST-Endpunkte die API-Signatur der Ressource im SharePoint-Clientobjektmodell streng nach. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="32468-p101">Before you can access a SharePoint resource using the REST service, you first have to figure out the URI endpoint that points to that resource. Whenever possible, the URI for these REST endpoints closely mimics the API signature of the resource in the SharePoint client object model. For example:</span></span>
 
 <span data-ttu-id="32468-113">*Clientobjektmodell-Methode:*</span><span class="sxs-lookup"><span data-stu-id="32468-113">*Client object model method:*</span></span> 

```
List.GetByTitle(listname).GetItems()
```
 
 <span data-ttu-id="32468-114">*REST-Endpunkt:*</span><span class="sxs-lookup"><span data-stu-id="32468-114">*REST endpoint:*</span></span> 

```
 http://server/site/_api/lists/getbytitle('listname')/items
```
 
<span data-ttu-id="32468-115">In einigen Fällen unterscheidet sich die Endpunkt-URI aber von der entsprechenden Clientobjektmodell-Signatur, um REST- oder OData-Konventionen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="32468-115">In some cases, however, the endpoint URI differs from the corresponding client object model signature, in order to comply with REST or OData conventions.</span></span>
 
<span data-ttu-id="32468-116">Die folgende Abbildung zeigt die allgemeine Syntaxstruktur von SharePoint REST-URIs.</span><span class="sxs-lookup"><span data-stu-id="32468-116">The following figure shows the general syntax structure of SharePoint REST URIs.</span></span> 

<span data-ttu-id="32468-117">**Syntaxstruktur von SharePoint REST-URIs**</span><span class="sxs-lookup"><span data-stu-id="32468-117">**SharePoint REST URI syntax structure**</span></span>

![SharePoint REST-Anforderungssyntax](../../images/REST_OverallSyntax.png)
 
<span data-ttu-id="32468-119">Einige Endpunkte für SharePoint-Ressourcen weichen von dieser Syntaxstruktur ab:</span><span class="sxs-lookup"><span data-stu-id="32468-119">Some endpoints for SharePoint resources deviate from this syntax structure:</span></span>

- <span data-ttu-id="32468-120">Methoden, die komplexe Typen als Parameter erfordern.</span><span class="sxs-lookup"><span data-stu-id="32468-120">Methods that require complex types as parameters.</span></span> 
    
    <span data-ttu-id="32468-121">Wenn die entsprechende Clientobjektmodell-Methode erfordert, dass komplexe Typen als Parameter übergeben werden, kann der REST-Endpunkt wegen REST-Einschränkungen von dieser Syntaxstruktur abweichen.</span><span class="sxs-lookup"><span data-stu-id="32468-121">If the corresponding client object model method requires that complex types are passed as parameters, the REST endpoint may deviate from this syntax construction to account for REST limitations.</span></span>
    
 
- <span data-ttu-id="32468-122">Statische Methoden und Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="32468-122">Static methods and properties.</span></span> 
    
    <span data-ttu-id="32468-123">REST-Endpunkte weichen von dieser Syntaxstruktur bei URIs ab, die statische Methoden und Eigenschaften darstellen.</span><span class="sxs-lookup"><span data-stu-id="32468-123">REST endpoints deviate from this syntax structure for URIs that represent static methods and properties.</span></span>
    

## <a name="determine-sharepoint-rest-service-endpoints"></a><span data-ttu-id="32468-124">Ermitteln von SharePoint-REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="32468-124">Determine SharePoint REST service endpoints</span></span>

<span data-ttu-id="32468-125">Befolgen Sie diese Schritte, um einen REST-Endpunkt für eine SharePoint-Ressource zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="32468-125">To construct a REST endpoint for a SharePoint resource, follow these steps:</span></span> 

1. <span data-ttu-id="32468-126">Starten Sie mit der REST-Dienstreferenz:</span><span class="sxs-lookup"><span data-stu-id="32468-126">Start with the REST service reference:</span></span>
    
     `http://server/site/_api`
    
 
2. <span data-ttu-id="32468-p102">Geben Sie den entsprechenden Einstiegspunkt an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="32468-p102">Specify the appropriate entry point. For example:</span></span>
    
     `http://server/site/_api/web`
    
 
3. <span data-ttu-id="32468-p103">Navigieren Sie vom Einstiegspunkt zu den spezifischen Ressourcen, auf die Sie zugreifen möchten. Dabei müssen Sie auch Parameter für Endpunkte angeben, die Methoden im Clientobjektmodell entsprechen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="32468-p103">Navigate from the entry point to the specific resources you want to access. This includes specifying parameters for endpoints that correspond to methods in the client object model. For example:</span></span>
    
     `http://server/site/_api/web/lists/getbytitle('listname')`
    
### <a name="reference-the-sharepoint-rest-service-in-your-endpoint-uri"></a><span data-ttu-id="32468-132">Referenzieren Sie den SharePoint REST-Dienst in Ihrem Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="32468-132">Reference the SharePoint REST service in your endpoint URI</span></span>

<span data-ttu-id="32468-p104">Verwenden Sie `_api`, um den SharePoint REST-Dienst in Ihren Endpunkt-URIs zu kennzeichnen. Der REST-Dienst ist Teil des Webdiensts „client.svc“. Um die Erstellung von REST-URIs zu erleichtern und den REST URI-Basispfad zu kürzen, verwendet der REST-Dienst `_api`, wodurch der explizite Verweis auf den Webdienst „client.svc“ nicht mehr erforderlich ist. URIs, die auf den Webdienst „client.svc“ verweisen, werden vom REST-Dienst jedoch weiterhin erkannt und akzeptiert. Sie können z. B. `http://server/site/_vti_bin/client.svc/web/lists` anstelle von `http://server/site/_api/web/lists` verwenden. Allerdings ist `_api` die bevorzugte Konvention. URLs haben maximal 256 Zeichen. Mit `_api` wird der Basis-URI verkürzt und es bleiben mehr Zeichen für die Erstellung der verbleibenden URL übrig.</span><span class="sxs-lookup"><span data-stu-id="32468-p104">Use  `_api` to denote the SharePoint REST service in your endpoint URIs. The REST service is part of the client.svc web service. However, to make REST URI construction easier and to shorten the base REST URI path, the REST service uses `_api` to abstract away the need to explicitly reference the client.svc web service. The REST service still recognizes and accepts URIs that reference the client.svc web service. For example, you can use `http://server/site/_vti_bin/client.svc/web/lists` instead of `http://server/site/_api/web/lists`. However, using  `_api` is the preferred convention. URLs have a 256 character limit, so using `_api` shortens the base URI, leaving more characters for use in constructing the rest of the URL.</span></span>
 

### <a name="specify-entry-points-for-the-sharepoint-rest-service"></a><span data-ttu-id="32468-140">Angeben von Einstiegspunkten für den SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-140">Specify entry points for the SharePoint REST service</span></span>

<span data-ttu-id="32468-p105">Die wichtigsten Einstiegspunkte für den REST-Dienst sind die Websitesammlung und die Website des angegebenen Kontexts. Damit entsprechen diese Einstiegspunkte den Eigenschaften **ClientContext.Site** und **ClientContext.Web** in den Clientobjektmodellen.</span><span class="sxs-lookup"><span data-stu-id="32468-p105">The main entry points for the REST service represent the site collection and site of the specified context. In this way, these entry points correspond to the  **ClientContext.Site** property and **ClientContext.Web** property in the client object models.</span></span>
 
<span data-ttu-id="32468-143">Gehen Sie folgendermaßen vor, um auf eine bestimmte Websitesammlung zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="32468-143">To access a specific site collection, use the following construction:</span></span>
 
 `http://server/site/_api/site`
 
<span data-ttu-id="32468-144">Gehen Sie folgendermaßen vor, um auf eine bestimmte Website zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="32468-144">To access a specific site, use the following construction:</span></span>
 
 `http://server/site/_api/web`
  
<span data-ttu-id="32468-145">Wobei  *server*  den Namen des Servers darstellt und  *site*  für den Namen der oder den Pfad zur entsprechenden Website steht.</span><span class="sxs-lookup"><span data-stu-id="32468-145">Where  *server*  represents the name of the server, and *site*  represents the name of, or path to, the specific site.</span></span>
 
<span data-ttu-id="32468-p106">Zusätzlich zu  `/site` und `/web` enthält der REST-Dienst mehrere Zugriffspunkte, die Entwicklern erlauben, zu spezifischen Funktionen zu navigieren. In der folgenden Tabelle sind einige dieser Zugriffspunkte aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="32468-p106">In addition to  `/site` and `/web`, the REST service includes several other access points that enable developers to navigate to specific functionality. The table below lists some of these access points.</span></span>

|<span data-ttu-id="32468-148">**Funktionsbereich**</span><span class="sxs-lookup"><span data-stu-id="32468-148">**Feature area**</span></span>|<span data-ttu-id="32468-149">**Zugriffspunkt**</span><span class="sxs-lookup"><span data-stu-id="32468-149">**Access point**</span></span>|
|:-----|:-----|
|<span data-ttu-id="32468-150">Website</span><span class="sxs-lookup"><span data-stu-id="32468-150">Site</span></span>|<span data-ttu-id="32468-151">http:// _server/site_/_api/site</span><span class="sxs-lookup"><span data-stu-id="32468-151">http:// _server/site_/_api/site</span></span>|
|<span data-ttu-id="32468-152">Web</span><span class="sxs-lookup"><span data-stu-id="32468-152">Web</span></span>|<span data-ttu-id="32468-153">http:// _server/site_/_api/web</span><span class="sxs-lookup"><span data-stu-id="32468-153">http:// _server/site_/_api/web</span></span>|
|<span data-ttu-id="32468-154">Benutzerprofil</span><span class="sxs-lookup"><span data-stu-id="32468-154">User Profile</span></span>|<span data-ttu-id="32468-155">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span><span class="sxs-lookup"><span data-stu-id="32468-155">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span></span>|
|<span data-ttu-id="32468-156">Suche</span><span class="sxs-lookup"><span data-stu-id="32468-156">Search</span></span>|<span data-ttu-id="32468-157">http:// _server/site_/_api/search</span><span class="sxs-lookup"><span data-stu-id="32468-157">http:// _server/site_/_api/search</span></span>|

### <a name="navigate-to-the-specific-resources-you-want-to-access"></a><span data-ttu-id="32468-158">Navigieren zu den Ressourcen, auf die Sie zugreifen möchten</span><span class="sxs-lookup"><span data-stu-id="32468-158">Navigate to the specific resources you want to access</span></span>
<span data-ttu-id="32468-159">Erstellen Sie hier mithilfe des Objektmodells spezifischere REST-Endpunkte mit den Namen der APIs aus dem Clientobjektmodell, jeweils getrennt durch einen Schrägstrich (/).</span><span class="sxs-lookup"><span data-stu-id="32468-159">From here, construct more specific REST endpoints by "walking" the object model, using the names of the APIs from the client object model separated by a forward slash (/).</span></span> <span data-ttu-id="32468-160">In der Tabelle unten sehen Sie Beispiele für Clientobjektmodell-Aufrufe und die zugehörigen REST-Endpunkte.</span><span class="sxs-lookup"><span data-stu-id="32468-160">The table below shows examples of client object model calls and the equivalent REST endpoint.</span></span> 
 
|<span data-ttu-id="32468-161">**Clientobjektmodell-API**</span><span class="sxs-lookup"><span data-stu-id="32468-161">**Client object model API**</span></span>|<span data-ttu-id="32468-162">**REST-Endpunkt**</span><span class="sxs-lookup"><span data-stu-id="32468-162">**REST endpoint**</span></span>|
|:-----|:-----|
|<span data-ttu-id="32468-163">ClientContext.Web.Lists</span><span class="sxs-lookup"><span data-stu-id="32468-163">ClientContext.Web.Lists</span></span>|<span data-ttu-id="32468-164">http:// _server_/ _site_/_api/web/lists</span><span class="sxs-lookup"><span data-stu-id="32468-164">http:// _server_/ _site_/_api/web/lists</span></span>|
|<span data-ttu-id="32468-165">ClientContext.Web.Lists[guid]</span><span class="sxs-lookup"><span data-stu-id="32468-165">ClientContext.Web.Lists[guid]</span></span>|<span data-ttu-id="32468-166">http:// _server_/ _site_/_api/web/lists(' _guid_')</span><span class="sxs-lookup"><span data-stu-id="32468-166">http:// _server_/ _site_/_api/web/lists(' _guid_')</span></span>|
|<span data-ttu-id="32468-167">ClientContext.Web.Lists.GetByTitle("Title")</span><span class="sxs-lookup"><span data-stu-id="32468-167">ClientContext.Web.Lists.GetByTitle("Title")</span></span>|<span data-ttu-id="32468-168">http:// _server_/ _site_/_api/web/lists/getbytitle(' _Title_')</span><span class="sxs-lookup"><span data-stu-id="32468-168">http:// _server_/ _site_/_api/web/lists/getbytitle(' _Title_')</span></span>|
<span data-ttu-id="32468-p108">Bei Endpunkt-URIs wird die Groß- und Kleinschreibung nicht beachtet. Verwenden Sie in der vorhergehenden Tabelle z. B. `/getbytitle`, um das REST-Äquivalent der **GetByTitle()**-Methode anzugeben.</span><span class="sxs-lookup"><span data-stu-id="32468-p108">Endpoint URIs are case-insensitive. In the previous table, for example, use  `/getbytitle` to specify the REST equivalent of the **GetByTitle()** method.</span></span>
 

## <a name="specify-parameters-in-rest-endpoint-uris"></a><span data-ttu-id="32468-171">Angeben von Parametern in REST-Endpunkt-URIs</span><span class="sxs-lookup"><span data-stu-id="32468-171">Specify parameters in REST endpoint URIs</span></span>
<span data-ttu-id="32468-p109">SharePoint erweitert die OData-Spezifikation, indem Sie Ihnen die Verwendung von Parametern ermöglicht, um Methodenparameter und Indexwerte anzugeben. Dadurch werden mögliche Probleme aufgrund von Mehrdeutigkeit in URIs vermieden, die mehrere Parameter mit dem gleichen Namen enthalten. Die folgenden zwei URIs enthalten z. B. Parameter mit dem gleichen Namen:</span><span class="sxs-lookup"><span data-stu-id="32468-p109">SharePoint extends the OData specification to enable you to use parentheses to specify method parameters and index values. This prevents potential disambiguation issues in URIs that contain multiple parameters with the same name. For example, the following two URIs contain parameters that have the same name:</span></span>
 
 `http://server/site/_api/web/lists/getByTitle('Announcements')/fields/getByTitle('Description')`
 
 `http://server/site/_api/web/lists('<guid>')/fields/getById('<guid>')`
 
<span data-ttu-id="32468-p110">Um mehrere Parameter anzugeben, schließen Sie den Parameter als ein Namen-Wert-Paar ein, und trennen Sie die Parameter mit Kommas. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="32468-p110">To specify multiple parameters, include the parameter as a name-value pair, and separate the parameters with commas. For example:</span></span>
  
 `http://server/site/_api/web/getAvailableWebTemplates(lcid=1033, includeCrossLanguage=true)`
  
<span data-ttu-id="32468-177">Die folgende Abbildung veranschaulicht die SharePoint-Syntax für REST-Parameter.</span><span class="sxs-lookup"><span data-stu-id="32468-177">The following figure shows the SharePoint REST parameter syntax.</span></span>
 
<span data-ttu-id="32468-178">**SharePoint-Syntax für REST-Parameter**
![SharePoint-Syntax für die Parameter für REST-Methoden](../../images/REST_parameterSyntax.png)</span><span class="sxs-lookup"><span data-stu-id="32468-178">**SharePoint REST parameter syntax**
![SharePoint REST service method parameter syntax](../../images/REST_parameterSyntax.png)</span></span>

### <a name="complex-types-as-parameters-for-the-rest-service"></a><span data-ttu-id="32468-179">Komplexe Typen als Parameter für den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-179">Complex types as parameters for the REST service</span></span>
<span data-ttu-id="32468-p111">Einige Methoden im Clientobjektmodell erfordern eine große Nutzlast als Parameter. Damit die Funktionsparität der REST-Endpunkte mit den entsprechenden Clientobjektmodell-APIs erhalten bleibt, müssen die Endpunkte einen komplexen Typ als Parameter akzeptieren. In diesen Fällen wird das vorhandene OData-Protokoll durch den REST-Dienst erweitert. Dadurch wird ermöglicht, dass diese REST-Endpunkte einen einzigen komplexen Typ als Parameter akzeptieren. Dies gilt nur für **POST**-Vorgänge. Sie müssen den komplexen Typ entsprechend der OData-Standards im [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties)- oder [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties)-Format übergeben.</span><span class="sxs-lookup"><span data-stu-id="32468-p111">Some methods in the client object model require a large payload as a parameter. For REST endpoints to maintain functionality parity with their corresponding client object model APIs, the endpoints must accept a complex type as a parameter. In these cases, the REST service extends the existing OData protocol to enable these REST endpoints to accept a single complex type as a parameter. This applies to  **POST** operations only, and you have to pass the complex type in [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) format or [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) format, according to OData standards.</span></span>
 
<span data-ttu-id="32468-p112">So verwendet beispielsweise die Methode **ListCollection.Add** ein **Microsoft.SharePoint.Client.ListCreationInformation**-Objekt als Parameter. Um eine Liste zu einer bestimmten Website hinzuzufügen, erstellen Sie den entsprechenden REST-Endpunkt wie folgt:</span><span class="sxs-lookup"><span data-stu-id="32468-p112">For example, the  **ListCollection.Add** method takes a **Microsoft.SharePoint.Client.ListCreationInformation** object as a parameter. To add a list to a specified site, construct the appropriate REST endpoint as follows:</span></span>
 
 `http://server/site/_api/web/lists/add`
 
<span data-ttu-id="32468-186">Übergeben Sie dann den komplexen Typ im Textkörper der Anforderung im JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="32468-186">Then, pass the complex type in the request body, formatted here using JSON.</span></span>

```javascript
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
### <a name="using-parameter-aliases-in-rest-service-calls"></a><span data-ttu-id="32468-187">Verwenden von Parameter-Aliasen in REST-Dienstaufrufen</span><span class="sxs-lookup"><span data-stu-id="32468-187">Using parameter aliases in REST service calls</span></span>
<span data-ttu-id="32468-p113">Sie können die "Parameteraliasing"-Semantik in OData verwenden, um Parameter an einen SharePoint-REST-Endpunkt zu übergeben. Beim Parameteraliasing wird der Parameterwert mit einem Alias im Parameteraufruf identifiziert, und der tatsächliche Wert wird in der Abfragezeichenfolge der URI angegeben. So können Sie mehr Zeichentypen und eine einheitliche Formatierung mithilfe der Abfragezeichenfolge unterstützen.</span><span class="sxs-lookup"><span data-stu-id="32468-p113">You can use the "parameter aliasing" semantic in OData to pass parameters to a SharePoint REST endpoint. In parameter aliasing, the parameter value is identified with an alias in the parameter call, and the actual value is specified in the query string of the URI. This enables you to support more types of characters and consistent formatting by using the query string.</span></span>
 
<span data-ttu-id="32468-191">Die folgenden zwei REST-URIs sind z. B. äquivalent:</span><span class="sxs-lookup"><span data-stu-id="32468-191">For example, the following two REST URIs are equivalent:</span></span> 
 
 <span data-ttu-id="32468-192">*Geben Sie den Parameterwert direkt an:*</span><span class="sxs-lookup"><span data-stu-id="32468-192">*Specify the parameter value directly:*</span></span> 
 
 `http://server/site/_api/web/applyWebTemplate("STS#0")`
 
 <span data-ttu-id="32468-193">*Verwenden Sie einen Parameteralias, und geben Sie den tatsächlichen Parameterwert in der Abfragezeichenfolge der URI an:*</span><span class="sxs-lookup"><span data-stu-id="32468-193">*Use a parameter alias, and specify the actual parameter value in the query string of the URI:*</span></span> 
 
 `http://server/site/_api/web/applyWebTemplate(title=@template)?@template="STS#0"`
 
<span data-ttu-id="32468-p114">Das Übergeben von komplexen Typen per Parameteraliasing wird vom SharePoint-REST-Dienst allerdings nicht unterstützt. So wird z. B. die folgende URI nicht unterstützt, die einen komplexen Typ im Parameteralias enthält:</span><span class="sxs-lookup"><span data-stu-id="32468-p114">However, the SharePoint REST service does not support passing complex types via parameter aliasing. For example, the following URI, which contains a complex type in the parameter alias, is not supported:</span></span>
 
 ```
 http://server/site/_api/userProfiles/People(7)/GetWorkplace(@address)?@address={"__metadata":{"type: "ODataDemo.Address"},"Street":"NE 228th", "City":"Sammamish","State":"WA","ZipCode":"98074","Country": "USA"}
 ```
 
<span data-ttu-id="32468-196">**Syntax für das Parameteraliasing im SharePoint-REST-Dienst**
![Syntax für das Parameteraliasing im SharePoint-REST-Dienst](../../images/REST_parameterAliasSyntax.png)</span><span class="sxs-lookup"><span data-stu-id="32468-196">**SharePoint REST service parameter aliasing syntax**
![SharePoint REST service parameter aliasing syntax](../../images/REST_parameterAliasSyntax.png)</span></span>

### <a name="specifying-dictionaries-as-parameter-values"></a><span data-ttu-id="32468-197">Angeben von Schlüsselverzeichnissen als Parameterwerte</span><span class="sxs-lookup"><span data-stu-id="32468-197">Specifying dictionaries as parameter values</span></span>
<span data-ttu-id="32468-198">Bei REST-Endpunkten, die Methoden entsprechen, die `Dictionary<String, String>`-Wörterbücher als Parameter verwenden, übergeben Sie das Wörterbuch als Serie von durch Kommas getrennten Namen-Wert-Paaren in der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="32468-198">For REST endpoints that correspond to methods that take  `Dictionary<String, String>` dictionaries as parameters, pass the dictionary as a series of comma delimited name-value pairs in the query string.</span></span>

<span data-ttu-id="32468-199">**Syntax für Schlüsselverzeichnisparameter im REST-Dienst**
![Syntax für Schlüsselverzeichnisparameter im REST-Dienst](../../images/REST_parameterDictionarySyntax.png)</span><span class="sxs-lookup"><span data-stu-id="32468-199">**REST service syntax for Dictionary parameters**
![REST service syntax for Dictionary parameters](../../images/REST_parameterDictionarySyntax.png)</span></span>
 
<span data-ttu-id="32468-200">Ein Objekt des Typs `Dictionary<String, object>` wird als Mehrfachwertobjekt namens „KeyedPropertyValue“ mit den folgenden Zeichenfolgeneigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="32468-200">A  `Dictionary<String, object>` is represented as a multi-value object, named KeyedPropertyValue, with the following string properties:</span></span>

-  <span data-ttu-id="32468-201">**Key** Der Schlüssel des Mehrfachwertobjekts.</span><span class="sxs-lookup"><span data-stu-id="32468-201">**Key** The key of the multi-value object.</span></span>

-  <span data-ttu-id="32468-202">**Value** Der Wert des Objekts</span><span class="sxs-lookup"><span data-stu-id="32468-202">**Value** The value of the object</span></span>

-  <span data-ttu-id="32468-p115">**ValueType** Der Werttyp des Objekts Für einfache Werttypen, die vorhandenen Entity Data Model(EDM)-Typen zugeordnet sind, gibt der REST-Dienst die entsprechende EDM-Zeichenfolge zurück, z. B. "Edm.String." Anderenfalls gibt der REST-Dienst den von der Funktion **Type.ToString** zurückgegebenen Werttyp zurück.</span><span class="sxs-lookup"><span data-stu-id="32468-p115">**ValueType** The value type of the object. For simple value types that map to existing Entity Data Model (EDM) types, the REST service returns the appropriate EDM type string; for example, "Edm.String." If not, the REST service returns the value type returned by the **Type.ToString** function.</span></span>

### <a name="specifying-parameter-values-in-the-query-string"></a><span data-ttu-id="32468-206">Angeben von Parameterwerten in der Abfragezeichenfolge</span><span class="sxs-lookup"><span data-stu-id="32468-206">Specifying parameter values in the query string</span></span>
<span data-ttu-id="32468-p116">Wenn Ihre REST-URI in einem Methodenaufruf endet, können Sie Abfragezeichenfolgensyntax verwenden, um die Parameterwerte der Methode anzugeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="32468-p116">If your REST URI terminates in a method call, you can use query string syntax to specify the parameter values of the method. For example:</span></span>
 
 `http://<server>/<site>/_api/web/applyWebTemplate?template="STS#0"`
 
<span data-ttu-id="32468-209">Die Abbildung unten veranschaulicht die Syntax, die der REST-Dienst für Parameter in einer Abfragezeichenfolge verwendet.</span><span class="sxs-lookup"><span data-stu-id="32468-209">The figure below shows the REST service syntax for parameters in query string.</span></span> 

<span data-ttu-id="32468-210">**REST-Dienst-Syntax für Parameter in Abfragezeichenfolgen**
![](../../images/REST_parameterQuerySyntax.png)</span><span class="sxs-lookup"><span data-stu-id="32468-210">**REST service syntax for parameters in query string**
![REST service syntax for parameters in query string](../../images/REST_parameterQuerySyntax.png)</span></span>
 
## <a name="specifying-static-methods-and-properties-as-rest-service-uris"></a><span data-ttu-id="32468-211">Angeben von statischen Methoden und Eigenschaften als REST-Dienst-URIs</span><span class="sxs-lookup"><span data-stu-id="32468-211">Specifying static methods and properties as REST service URIs</span></span>
<span data-ttu-id="32468-p117">Verwenden Sie zum Erstellen von URIs, die statischen Methoden oder Eigenschaften entsprechen, den entsprechenden API-Namen aus dem Objektmodell „ECMAScript“, beginnend mit der Namespace-Deklaration und dargestellt mit Punkt. Zum Beispiel würde das REST-Äquivalent von [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/de-DE/library/ee658947.aspx) im Clientobjektmodell ECMAScript wie folgt lauten:</span><span class="sxs-lookup"><span data-stu-id="32468-p117">To construct URIs that correspond to static methods or properties, use the corresponding API name from the ECMAScript object model, starting with the namespace declaration and using dot notation. For example,  [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/de-DE/library/ee658947.aspx) in the ECMAScript client object model would have the following REST equivalent:</span></span>
 
 `http://server/site/_api/SP.Utilities.Utility.getImageUrl('imageName')`
 
<span data-ttu-id="32468-p118">Statische Methoden können allerdings nur direkt aufgerufen werden und sind als Teil einer größeren URI-Komposition nicht zulässig. Das direkte Aufrufen der Methode **SP.Utility.AssetsLibrary** in REST ist z. B. wie folgt zulässig:</span><span class="sxs-lookup"><span data-stu-id="32468-p118">However, static properties can be accessed only directly, and are not allowed as part of a larger URI composition. For example, directly accessing the  **SP.Utility.AssetsLibrary** method in REST is allowable, as follows:</span></span>
  
 `http://server/site/_api/SP.Utility.assetsLibrary/id`
 
<span data-ttu-id="32468-216">Die Verwendung des Ressourcenspeicherorts als Parameter für eine komplexere URI, wie im folgenden Beispiel gezeigt, ist allerdings nicht zulässig:</span><span class="sxs-lookup"><span data-stu-id="32468-216">However, using that resource location as a parameter for a more complex URI, as shown in the following example, is not allowed:</span></span>
  
 `http://server/site/_api/getList(~SP.Utility/assetsLibrary/id)`
 
<span data-ttu-id="32468-217">Die Abbildung unten veranschaulicht die Syntax, die der SharePoint-REST-Dienst für statische Elemente verwendet.</span><span class="sxs-lookup"><span data-stu-id="32468-217">The figure below shows the SharePoint REST service static member syntax.</span></span>

<span data-ttu-id="32468-218">**SharePoint-REST-Dienst-Syntax für statische Elemente**
![REST-Dienst-Syntax für Parameter in einer Abfragezeichenfolge](../../images/REST_parameterQuerySyntax.png)</span><span class="sxs-lookup"><span data-stu-id="32468-218">**SharePoint REST service static member syntax**
![REST service syntax for parameters in query string](../../images/REST_parameterQuerySyntax.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="32468-219">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="32468-219">Next steps</span></span>
<span data-ttu-id="32468-220">Wenn Sie die von einem Endpunkt angeforderten Daten auswählen, filtern oder sortieren möchten, unterstützt der SharePoint-REST-Dienst eine breite Palette von OData-Abfragezeichenfolgen-Operatoren.</span><span class="sxs-lookup"><span data-stu-id="32468-220">If you want to select, filter, or order the data you requested from an endpoint, the SharePoint REST service supports a wide range of OData query string operators.</span></span> 
 

## <a name="see-also"></a><span data-ttu-id="32468-221">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="32468-221">See also</span></span>
<span data-ttu-id="32468-222"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="32468-222"><a name="bk_addresources"> </a></span></span>

-  [<span data-ttu-id="32468-223">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-223">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="32468-224">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="32468-224">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="32468-225">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="32468-225">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="32468-226">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="32468-226">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="32468-227">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="32468-227">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
-  [<span data-ttu-id="32468-228">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="32468-228">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="32468-229">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="32468-229">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="32468-230">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-230">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
-  [<span data-ttu-id="32468-231">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="32468-231">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
