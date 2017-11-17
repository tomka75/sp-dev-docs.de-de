---
title: "Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cb954660d47ab7cf4c3b71921843f5826c3be14d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a><span data-ttu-id="98bed-102">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="98bed-102">Complete basic operations using SharePoint REST endpoints</span></span>
<span data-ttu-id="98bed-103">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, mit der SharePoint-REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="98bed-103">Learn how to perform basic create, read, update, and delete (CRUD) operations with the SharePoint REST interface.</span></span>

## <a name="developing-with-the-sharepoint-client-apis-and-rest"></a><span data-ttu-id="98bed-104">Entwickeln mit SharePoint-Client-APIs und REST</span><span class="sxs-lookup"><span data-stu-id="98bed-104">Developing with the SharePoint client APIs and REST</span></span>
<span data-ttu-id="98bed-105"><a name="ClientAPIs"> </a> Sie können grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren und Löschen) mithilfe der Representational State Transfer (REST)-Schnittstelle ausführen, die von SharePoint bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="98bed-105"><a name="ClientAPIs"> </a> You can perform basic create, read, update, and delete (CRUD) operations by using the Representational State Transfer (REST) interface provided by SharePoint.</span></span> <span data-ttu-id="98bed-106">Die REST-Schnittstelle macht alle SharePoint-Entitäten und -Vorgänge verfügbar, die in den anderen SharePoint-Client APIs zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="98bed-106">The REST interface exposes all of the SharePoint entities and operations that are available in the other SharePoint client APIs.</span></span> <span data-ttu-id="98bed-107">Ein Vorteil der Verwendung von REST besteht darin, dass Sie keine Verweise auf SharePoint-Bibliotheken oder Clientassemblys hinzufügen müssen.</span><span class="sxs-lookup"><span data-stu-id="98bed-107">One advantage of using REST is that you don't have to add references to any SharePoint libraries or client assemblies.</span></span> <span data-ttu-id="98bed-108">Stattdessen richten Sie HTTP-Anforderungen an die entsprechenden Endpunkte, um SharePoint-Entitäten, wie z. B. Webseiten, Listen und Listenelemente, abzurufen oder zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="98bed-108">Instead, you make HTTP requests to the appropriate endpoints to retrieve or update SharePoint entities, such as webs, lists, and list items.</span></span> <span data-ttu-id="98bed-109">Unter [Einführung in den SharePoint-REST-Dienst](get-to-know-the-sharepoint-rest-service.md) erhalten Sie eine umfassende Einführung in die SharePoint-REST-Schnittstelle und ihre Architektur.</span><span class="sxs-lookup"><span data-stu-id="98bed-109">See  [Get to know the SharePoint REST service](get-to-know-the-sharepoint-rest-service.md) for a thorough introduction to the SharePoint REST interface and its architecture.</span></span>
 
<span data-ttu-id="98bed-p102">Unter  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md) und [Arbeiten mit Ordnern und Dateien mit REST](working-with-folders-and-files-with-rest.md) wird die Verwendung von SharePoint-Kernentitäten ausführlich erläutert. Unter [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md) ist ein Beispiel enthalten, das Ihnen zeigt, wie Sie viele dieser Operationen im Kontext einer in C# geschriebenen ASP.NET-Webanwendung durchführen können.</span><span class="sxs-lookup"><span data-stu-id="98bed-p102">[Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) and [Working with folders and files with REST](working-with-folders-and-files-with-rest.md) explain in greater detail how to work with core SharePoint entities. See [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md) for a sample that shows you how to do many of these operations in the context of an ASP.NET web application written in C#.</span></span>
 
<span data-ttu-id="98bed-112">Weitere Informationen zu den Gruppen von APIs, die auf der SharePoint-Plattform verfügbar sind, finden Sie unter [Auswählen des richtigen API-Satzes in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="98bed-112">For more details about the sets of APIs available on the SharePoint platform, see  [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span> <span data-ttu-id="98bed-113">Informationen dazu, wie Sie andere Client-APIs verwenden, finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx), [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx) und [Erstellen von Windows Phone-Apps, die auf SharePoint 2013 zugreifen](https://msdn.microsoft.com/en-us/library/office/jj163228.aspx).</span><span class="sxs-lookup"><span data-stu-id="98bed-113">For more details about the sets of APIs available on the SharePoint 2013 platform, see  Choose the right API set in SharePoint 2013. For information about how to use the other client APIs, see  Complete basic operations using JavaScript library code in SharePoint 2013,  Complete basic operations using JavaScript library code in SharePoint 2013, and  Build Windows Phone apps that access SharePoint 2013.</span></span>
 

## <a name="http-operations-in-sharepoint-rest-services"></a><span data-ttu-id="98bed-114">HTTP-Operationen in SharePoint-REST-Diensten</span><span class="sxs-lookup"><span data-stu-id="98bed-114">HTTP operations in SharePoint REST services</span></span>
<span data-ttu-id="98bed-115"><a name="HTTPOps"> </a> Die Endpunkte im SharePoint-REST-Dienst entsprechen den Typen und Mitgliedern in den SharePoint-Clientobjektmodellen.</span><span class="sxs-lookup"><span data-stu-id="98bed-115"><a name="HTTPOps"> </a> The endpoints in the SharePoint  REST service correspond to the types and members in the SharePoint client object models.</span></span> <span data-ttu-id="98bed-116">Mithilfe von HTTP-Anfragen können Sie diese REST-Endpunkte verwenden, um typische CRUD-Vorgänge (**Erstellen**,  **Lesen**,  **Aktualisieren** und **Löschen**) in SharePoint-Entitäten, z. B. Listen und Websites, auszuführen.</span><span class="sxs-lookup"><span data-stu-id="98bed-116">The endpoints in the SharePoint REST service correspond to the types and members in the SharePoint client object models. By using HTTP requests, you can use these REST endpoints to perform typical CRUD ( **Create**,  **Read**,  **Update**, and  **Delete**) operations against SharePoint entities, such as lists and sites.</span></span> 
 
<span data-ttu-id="98bed-p105">In der Regel entsprechen Endpunkte, die **Read**-Operationen darstellen, HTTP- **GET**-Befehlen. Endpunkte, die Aktualisierungsoperationen darstellen, entsprechen HTTP- **POST**-Befehlen, und Endpunkte, die Aktualisierungs- oder Einfügeoperationen darstellen, entsprechen HTTP- **PUT**-Befehlen.</span><span class="sxs-lookup"><span data-stu-id="98bed-p105">Typically, endpoints that represent  **Read** operations map to HTTP **GET** commands. Endpoints that represent update operations map to HTTP **POST** commands, and endpoints that represent update or insert operations map to HTTP **PUT** commands.</span></span>
 
<span data-ttu-id="98bed-p106">In SharePoint verwenden Sie **POST**, um Entitäten wie Listen und Websites zu erstellen. Der SharePoint-REST-Dienst unterstützt das Senden von **POST**-Befehlen, die Objektdefinitionen enthalten, an Endpunkte, die Auflistungen darstellen. Sie können beispielsweise einen **POST**-Befehl, der eine neue Listenobjektdefinition in ATOM enthält, an die folgende URL senden, um eine SharePoint-Liste zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="98bed-p106">In SharePoint, use  **POST** to create entities such as lists and sites. The SharePoint REST service supports sending **POST** commands that include object definitions to endpoints that represent collections. For example, you could send a **POST** command that included a new list object definition in ATOM to the following URL, to create a SharePoint list:</span></span>
 
 ```
 http://<site url>/_api/web/lists
 ```

<span data-ttu-id="98bed-p107">Alle nicht erforderlichen Eigenschaften in **POST**-Operationen werden auf ihre Standardwerte festgelegt. Wenn Sie eine schreibgeschützte Eigenschaft im Rahmen einer **POST**-Operation festzulegen versuchen, gibt der Dienst eine Ausnahme zurück.</span><span class="sxs-lookup"><span data-stu-id="98bed-p107">For  **POST** operations, any properties that are not required are set to their default values. If you attempt to set a read-only property as part of a **POST** operation, the service returns an exception.</span></span>
  
<span data-ttu-id="98bed-p108">Verwenden Sie die Operationen **PUT** und **MERGE**, um vorhandene SharePoint-Objekte zu aktualisieren. Jeder Dienstendpunkt, der eine **set**-Operation für eine Objekteigenschaft darstellt, unterstützt **PUT**-Anforderungen und **MERGE**-Anforderungen. Bei **MERGE**-Anforderungen ist das Festlegen von Eigenschaften optional. Alle Eigenschaften, die Sie nicht explizit festlegen, behalten ihre aktuelle Eigenschaft. Bei **PUT**-Befehlen werden jedoch alle Eigenschaften, die Sie nicht explizit festlegen, auf ihre Standardeigenschaften festgelegt. Darüber hinaus gibt der REST-Dienst eine Ausnahme zurück, wenn Sie bei Verwendung von HTTP- **PUT**-Befehlen nicht alle erforderlichen Eigenschaften in Objektaktualisierungen angeben.</span><span class="sxs-lookup"><span data-stu-id="98bed-p108">Use  **PUT** and **MERGE** operations to update existing SharePoint objects. Any service endpoint that represents an object property **set** operation supports both **PUT** requests and **MERGE** requests. For **MERGE** requests, setting properties is optional; any properties that you do not explicitly set retain their current property. For **PUT** commands, however, any properties you do not explicitly set are set to their default properties. In addition, if you do not specify all required properties in object updates when using HTTP **PUT** commands, the REST service returns an exception.</span></span>
  
<span data-ttu-id="98bed-p109">Verwenden Sie den HTTP-Befehl **DELETE** für die spezifische Endpunkt-URL, um das durch den Endpunkt dargestellte SharePoint-Objekt zu löschen. Bei wiederverwendbaren Objekten, wie Listen, Dateien und Listenelementen, führt dies zu einer **Recycle**-Operation.</span><span class="sxs-lookup"><span data-stu-id="98bed-p109">Use the HTTP  **DELETE** command against the specific endpoint URL to delete the SharePoint object represented by that endpoint. In the case of recyclable objects, such as lists, files, and list items, this results in a **Recycle** operation.</span></span>
 
## <a name="reading-data-with-the-sharepoint-rest-interface"></a><span data-ttu-id="98bed-131">Lesen von Daten mit der SharePoint-REST-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="98bed-131">Reading data with the SharePoint REST interface</span></span>
<span data-ttu-id="98bed-132"><a name="ReadingData"> </a>  Um die in SharePoint integrierten REST-Funktionen zu verwenden, erstellen Sie mithilfe des OData-Standards eine RESTful-HTTP-Anforderung, die der Clientobjektmodell-API entspricht, die Sie verwenden möchten. </span><span class="sxs-lookup"><span data-stu-id="98bed-132"><a name="ReadingData"> </a>To use the REST capabilities that are built into SharePoint, you construct a RESTful HTTP request, using the OData standard, which corresponds to the client object model API you want to use. The client.svc web service handles the HTTP request and serves the appropriate response in either Atom or JavaScript Object Notation (JSON) format. The client application must then parse that response.</span></span> <span data-ttu-id="98bed-133">Jede SharePoint-Entität wird an einem Endpunkt auf der SharePoint-Website verfügbar gemacht, auf die Sie abzielen, und ihre Metadaten werden entweder im XML- oder im JSON-Format dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98bed-133">Each SharePoint entity is exposed at an endpoint on the SharePoint  site that you are targeting, and its metadata is represented in either XML or JSON format.</span></span> <span data-ttu-id="98bed-134">Sie können die HTTP-Anforderung in einer beliebigen Sprache erstellen, einschließlich, aber nicht beschränkt auf JavaScript und C#.</span><span class="sxs-lookup"><span data-stu-id="98bed-134">You can make the HTTP requests in any language, including but not limited to JavaScript and C#.</span></span>
 
<span data-ttu-id="98bed-p111">Um Informationen aus einem REST-Endpunkt zu lesen, müssen Sie die URL des Endpunkts und die OData-Darstellung der SharePoint-Entität kennen, die an diesem Endpunkt verfügbar gemacht wird. Um beispielsweise alle Listen in einer bestimmten SharePoint-Website abzurufen, senden Sie eine **GET**-Anforderung an `http://<site url>/_api/web/lists`. Sie können zu dieser URL in Ihrem Browser navigieren und das zurückgegebene XML anzeigen. Wenn Sie die Anforderung in Code durchführen, können Sie angeben, ob die OData-Darstellung der Listen im XML- oder JSON-Format erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="98bed-p111">To read information from a REST endpoint, you must know both the URL of the endpoint and the OData representation of the SharePoint entity that is exposed at that endpoint. For example, to retrieve all of the lists in a specific SharePoint site, you would make a  **GET** request to `http://<site url>/_api/web/lists`. You can navigate to this URL in your browser and see the XML that gets returned. When you make the request in code, you can specify whether to receive the OData representation of the lists in XML or JSON.</span></span>
 
<span data-ttu-id="98bed-p112">Der folgende C#-Code zeigt die Vorgehensweise zum Durchführen der **GET**-Anforderung, die eine JSON-Darstellung aller Listen einer Website mithilfe von JQuery zurückgibt. Dabei wird auch davon ausgegangen, dass Sie einen gültigen OAuth-Zugriffstoken installiert haben, der in der **accessToken**-Variablen gespeichert ist. Sie benötigen den Zugriffstoken nicht, wenn Sie den Aufruf, wie bei einem in SharePoint gehosteten Add-In, innerhalb einer Add-In-Website vornehmen. Beachten Sie, dass Sie den Zugriffstoken nicht aus Code abrufen können, der auf einem Browserclient ausgeführt wird. Sie müssen den Zugriffstoken aus Code abrufen, der auf einem Server ausgeführt wird. Unter  [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) und [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) wird erläutert, wie Sie einen Zugriffstoken abrufen können.</span><span class="sxs-lookup"><span data-stu-id="98bed-p112">The following C# code demonstrates how to make this  **GET** request that returns a JSON representation of all of a site's lists by using JQuery. It also assumes that you have a valid OAuth access token that is stored in the **accessToken** variable. You do not need the access token if you make this call from inside an add-in web, as you would in a SharePoint-hosted add-in. Note that you cannot obtain an access token from code that is running on a browser client. You must obtain the access token from code that is running on a server. [Context Token OAuth flow for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) and [Authorization Code OAuth flow for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) explain how you can obtain an access token.</span></span>

```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", 
  "Bearer " + accessToken);
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

<span data-ttu-id="98bed-p113">Diese Anforderung würde etwas anders aussehen, wenn Sie Ihr Add-In in JavaScript schreiben, jedoch die domänenübergreifende SharePoint-Bibliothek verwenden. In diesem Fall müssen Sie keinen Zugriffstoken zur Verfügung stellen. Der folgende Code zeigt, wie die Anforderung aussehen würde, wenn Sie die domänenübergreifende Bibliothek verwenden und die OData-Darstellung der Listen im XML-Format anstatt im JSON-Format erfolgen soll. (Da Atom das Standardantwortformat ist, müssen Sie keinen **Accept**-Header einfügen.) Weitere Informationen über die Verwendung der domänenübergreifenden Bibliothek finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx).</span><span class="sxs-lookup"><span data-stu-id="98bed-p113">This request would look a little different if you are writing your add-in in JavaScript but using the SharePoint cross-domain library. In this case, you don't need to provide an access token. The following code demonstrates how this request would look if you are using the cross-domain library and want to receive the OData representation of the lists as XML instead of JSON. (Because Atom is the default response format, you don't have to include an  **Accept** header.) See [Access SharePoint data from add-ins using the cross-domain library](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx) for more information about using the cross-domain library.</span></span>
 
```javascript
var executor = new SP.RequestExecutor(appweburl);
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/lists?@target='" +
            hostweburl + "'",
        method: "GET",
        success: successHandler,
        error: errorHandler
    }
);
```

<span data-ttu-id="98bed-p114">Der Code im folgenden Beispiel zeigt, wie Sie eine JSON-Darstellung aller Listen in einer Website anfordern, indem Sie C# verwenden. Das Beispiel geht davon aus, dass Sie über einen OAuth-Zugriffstoken verfügen, den Sie in der  `accessToken`-Variablen speichern.</span><span class="sxs-lookup"><span data-stu-id="98bed-p114">The code in the following example shows you how to request a JSON representation of all of the lists in a site by using C#. It assumes that you have an OAuth access token that you are storing in the  `accessToken` variable.</span></span>

```
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```

### <a name="getting-properties-that-arent-returned-with-the-resource"></a><span data-ttu-id="98bed-151">Abrufen von Eigenschaften, die nicht mit der Ressource zurückgegeben werden</span><span class="sxs-lookup"><span data-stu-id="98bed-151">Getting properties that aren't returned with the resource</span></span>
<span data-ttu-id="98bed-152"><a name="NavigationProperties"> </a>Viele Eigenschaftswerte werden zurückgegeben, wenn Sie eine Ressource abrufen. Bei einigen Eigenschaften müssen Sie allerdings eine **GET**-Anforderung direkt an den Eigenschaftsendpunkt senden.</span><span class="sxs-lookup"><span data-stu-id="98bed-152"><a name="NavigationProperties"> </a> Many property values are returned when you retrieve a resource, but for some properties, you have to send a  **GET** request directly to the property endpoint. This is typical of properties that represent SharePoint entities.</span></span> <span data-ttu-id="98bed-153">Dies gilt i. d. R. für Eigenschaften, die SharePoint-Entitäten darstellen.</span><span class="sxs-lookup"><span data-stu-id="98bed-153">This is typical of properties that represent SharePoint entities.</span></span>
 
<span data-ttu-id="98bed-p116">Das folgende Beispiel zeigt, wie Sie eine Eigenschaft abrufen, indem Sie den Namen der Eigenschaft an den Ressourcenendpunkt anhängen. Im Beispiel wird der Wert der Eigenschaft **Author** von einer **File**-Ressource abgerufen.</span><span class="sxs-lookup"><span data-stu-id="98bed-p116">The following example shows how to get a property by appending the property name to the resource endpoint. The example gets the value of the  **Author** property from a **File** resource.</span></span>
 
 ```
 http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author
 ```

<span data-ttu-id="98bed-156">Um die Ergebnisse im JSON-Format zu erhalten, fügen Sie einen **Accept**-Header zu `"application/json;odata=verbose"` hinzu.</span><span class="sxs-lookup"><span data-stu-id="98bed-156">To get the results in JSON format, include an  **Accept** header set to `"application/json;odata=verbose"`.</span></span>

## <a name="writing-data-by-using-the-rest-interface"></a><span data-ttu-id="98bed-157">Schreiben von Daten unter Verwendung der REST-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="98bed-157">Writing data by using the REST interface</span></span>
<span data-ttu-id="98bed-158"><a name="WritingData"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-158"></span></span>

<span data-ttu-id="98bed-p117">Sie können SharePoint-Entitäten erstellen und aktualisieren, indem Sie RESTful-HTTP-Anforderungen an die entsprechenden Endpunkte erstellen, genauso wie beim Lesen von Daten. Ein wesentlicher Unterschied dabei ist jedoch, dass Sie eine **POST**-Anforderung verwenden. Beim Aktualisieren von Entitäten übergeben Sie außerdem eine **PUT**- oder **MERGE**-HTTP-Anforderungsmethode, indem Sie einen dieser Begriffe den Headern Ihrer Anforderung als Wert des **X-HTTP-Method**-Schlüssels hinzufügen. Die **MERGE**-Methode aktualisiert nur die Eigenschaften der von Ihnen angegebenen Entität, während die **PUT**-Methode die bestehende Entität durch eine neue ersetzt, die Sie im Textkörper der **POST**-Anforderung angeben. Verwenden Sie die **DELETE**-Methode, um die Entität zu löschen. Beim Erstellen oder Aktualisieren einer Entität müssen Sie eine OData-Darstellung der Entität, die Sie erstellen oder ändern möchten, im Textkörper Ihrer HTTP-Anforderung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="98bed-p117">You can create and update SharePoint entities by constructing RESTful HTTP requests to the appropriate endpoints, just as you do when you're reading data. One key difference, however, is that you use a  **POST** request. When you're updating entities, you also pass a **PUT** or **MERGE** HTTP request method by adding one of those terms to the headers of your request as the value of the **X-HTTP-Method** key. The **MERGE** method updates only the properties of the entity that you specify, while the **PUT** method replaces the existing entity with a new one that you supply in the body of the **POST**. Use the  **DELETE** method to delete the entity. When you create or update an entity, you must provide an OData representation of the entity that you want to create or change in the body of your HTTP request.</span></span>
 
<span data-ttu-id="98bed-p118">Eine weitere wichtige Überlegung beim Erstellen, Aktualisieren und Löschen von SharePoint-Entitäten ist, dass diese Vorgänge auch den Anforderungsformular-Digestwert des Servers als Wert des **X-RequestDigest**-Headers erfordern, wenn Sie nicht OAuth verwenden, um Ihre Anforderungen zu autorisieren. Sie können diesen Wert abrufen, indem Sie eine **POST**-Anforderung mit leerem Textkörper an  `http://<site url>/_api/contextinfo` senden und den Wert des `d:FormDigestValue`-Knotens aus der XML-Datei extrahieren, das der **contextinfo**-Endpunkt zurückgibt. Das folgende Beispiel zeigt eine HTTP-Anforderung an den **contextinfo**-Endpunkt in C#.</span><span class="sxs-lookup"><span data-stu-id="98bed-p118">Another important consideration when creating, updating, and deleting SharePoint entities is that if you aren't using OAuth to authorize your requests, these operations require the server's request form digest value as the value of the  **X-RequestDigest** header. You can retrieve this value by making a **POST** request with an empty body to `http://<site url>/_api/contextinfo` and extracting the value of the `d:FormDigestValue` node in the XML that the **contextinfo** endpoint returns. The following example shows an HTTP request to the **contextinfo** endpoint in C#.</span></span>
 
```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/contextinfo");
endpointRequest.Method = "POST";
endpointRequest.Accept = "application/json;odata=verbose";
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();
  
```

<span data-ttu-id="98bed-168">Wenn Sie den unter [Autorisierung und Authentifizierung für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142384.aspx) beschriebenen Authentifizierungs- und Autorisierungsablauf verwenden, müssen Sie den Anforderungsdigest nicht in Ihre Anforderungen einschließen.</span><span class="sxs-lookup"><span data-stu-id="98bed-168">If you're using the authentication and authorization flow described in  [Authorization and authentication of SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/fp142384.aspx), you don't need to include the request digest in your requests.</span></span>
 
<span data-ttu-id="98bed-169">Wenn Sie die domänenübergreifende JavaScript-Bibliothek verwenden, übernimmt SP.RequestExecutor das Abrufen und Senden des Formulardigestwerts für Sie.</span><span class="sxs-lookup"><span data-stu-id="98bed-169">If you're using the JavaScript cross-domain library, SP.RequestExecutor handles getting and sending the form digest value for you.</span></span>
 
<span data-ttu-id="98bed-p119">Wenn Sie eine in SharePoint gehostete SharePoint-Add-In erstellen, müssen Sie keine separate HTTP-Anforderung durchführen, um den Formulardigestwert abzurufen. Stattdessen können Sie den Wert im JavaScript-Code aus dem SharePoint einer Seite (wenn die Seite die Standard-Masterseite verwendet) abrufen, siehe folgendes Beispiel, indem die JQuery verwendet und eine Liste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="98bed-p119">If you're creating a SharePoint-hosted SharePoint Add-in, you don't have to make a separate HTTP request to retrieve the form digest value. Instead, you can retrieve the value in JavaScript code from the SharePoint a page (if the page uses the default master page), as shown in the following example, which uses JQuery and creates a list.</span></span>
 
```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists",
        type: "POST",
        data:  JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true,
 'BaseTemplate': 100, 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: doSuccess,
        error: doError
});
```

<span data-ttu-id="98bed-p120">Das folgende Beispiel zeigt, wie Sie die im vorherigen Beispiel erstellte Liste aktualisieren. In dem Beispiel wird der Titel der Liste geändert, JQuery wird verwendet, und es wird davon ausgegangen, dass Sie diese Operation in einem in SharePoint gehosteten Add-In durchführen.</span><span class="sxs-lookup"><span data-stu-id="98bed-p120">The following example shows how to update the list that is created in the previous example. The example changes the title of the list, uses JQuery, and assumes that you are doing this operation in a SharePoint-hosted add-in.</span></span>

```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists/GetByTitle('Test')",
        type: "POST",
        data: JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }),
        headers: { 
            "X-HTTP-Method":"MERGE",
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val(),
            "IF-MATCH": "*"
        },
        success: doSuccess,
        error: doError
});

```

<span data-ttu-id="98bed-p121">Geben Sie im Wert des **IF-MATCH**-Schlüssels in den Anforderungs-Headern den **etag**-Wert einer Liste oder eines Listenelements an. Dieser bestimmte Wert gilt nur für Listen und Listenelemente und soll Ihnen nicht helfen, Parallelitätsprobleme beim Aktualisieren dieser Entitäten zu vermeiden. Im vorherigen Beispiel wird ein Sternchen (*) für diesen Wert verwendet. Sie können den Wert immer verwenden, wenn Sie sicher sind, dass keine Parallelitätsprobleme bestehen. Andernfalls sollten Sie den **etag**-Wert bzw. eine Liste oder ein Listenelement abrufen, indem Sie eine **GET**-Anforderung durchführen, die die Entität abruft. Die Antwortheader der resultierenden HTTP-Antwort übergeben das ETag als Wert des **ETag**-Schlüssels. Dieser Wert ist auch in den Entitätsmetadaten enthalten. Das folgende Beispiel zeigt das öffnende Tag  `<entry>` für den XML-Knoten, der die Listeninformationen enthält. Die Eigenschaft **m:etag** enthält den **etag**-Wert.</span><span class="sxs-lookup"><span data-stu-id="98bed-p121">The value of the  **IF-MATCH** key in the request headers is where you specify the **etag** value of a list or list item. This particular value applies only to lists and list items, and it is intended to help you avoid concurrency problems when you update those entities. The previous example uses an asterisk (*) for this value, and you can use that value whenever you don't have any reason to worry about concurrency issues. Otherwise, you should obtain the **etag** value or a list or list item by performing a **GET** request that retrieves the entity. The response headers of the resulting HTTP response will pass the etag as the value of the **ETag** key. This value is also included in the entity metadata. The following example shows the opening `<entry>` tag for the XML node that contains the list information. The **m:etag** property contains the **etag** value.</span></span>

```XML
<entry xml:base="http://site url/_api/" xmlns=http://www.w3.org/2005/Atom 
xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" 
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:etag=""1"">
```

## <a name="creating-a-site-with-rest"></a><span data-ttu-id="98bed-182">Erstellen einer Website mit REST</span><span class="sxs-lookup"><span data-stu-id="98bed-182">Creating a site with REST</span></span>
<span data-ttu-id="98bed-183"><a name="bk_CreateSite"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-183"></span></span>

<span data-ttu-id="98bed-184">Das folgende Beispiel zeigt, wie Sie eine Website in JavaScript erstellen können.</span><span class="sxs-lookup"><span data-stu-id="98bed-184">The following example shows how to create a site in JavaScript.</span></span>

```javascript
jQuery.ajax({
    url: "http://<site url>/_api/web/webinfos/add",
    type: "POST",
    data: JSON.stringify(
        {'parameters': {
            '__metadata':  {'type': 'SP.WebInfoCreationInformation' },
            'Url': 'RestSubWeb',
            'Title': 'RestSubWeb',
            'Description': 'REST created web',
            'Language':1033,
            'WebTemplate':'sts',
            'UseUniquePermissions':false}
        }
    ),
    headers: { 
        "accept": "application/json; odata=verbose", 
        "content-type":"application/json;odata=verbose",
        "content-length": <length of post body>,
        "X-RequestDigest": $("#__REQUESTDIGEST").val() 
    },
    success: doSuccess,
    error: doError
});
```

## <a name="how-rest-requests-differ-by-environment"></a><span data-ttu-id="98bed-185">So unterscheiden sich REST-Anforderungen je nach Umgebung</span><span class="sxs-lookup"><span data-stu-id="98bed-185">How REST requests differ by environment</span></span>
<span data-ttu-id="98bed-186"><a name="bk_HowRequestsDiffer"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-186"></span></span>

<span data-ttu-id="98bed-p122">Der Vorgang zum Erstellen und Senden einer HTTP-Anforderung kann je nach Sprache, Bibliothek und Add-In-Typ variieren, sodass Sie häufig mindestens eine Anforderungskomponente ändern müssen, wenn Sie eine Anforderung aus einer Umgebung in eine andere übertragen. jQuery AJAX-Anforderungen verwenden beispielsweise **data**- und **type**-Parameter, um den Anforderungstext und -typ anzugeben, während domänenübergreifende Bibliotheksanforderungen **body**- und **method**-Parameter zum Angeben dieser Werte verwenden.</span><span class="sxs-lookup"><span data-stu-id="98bed-p122">Building and sending an HTTP request may vary according to language, library, and add-in type, so you often need to change one or more request components when you're translating a request from one environment to another. For example, jQuery AJAX requests use  **data** and **type** parameters to specify the request body and type, but cross-domain library requests use **body** and **method** parameters to specify those values.</span></span>
 
<span data-ttu-id="98bed-189">In den folgenden Abschnitten werden weitere allgemeine Unterschiede zwischen Umgebungen beschrieben.</span><span class="sxs-lookup"><span data-stu-id="98bed-189">The following sections describe other common differences across environments.</span></span>

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a><span data-ttu-id="98bed-190">Wie Sie den Formulardigestwert abrufen und senden, hängt von dem Add-In ab</span><span class="sxs-lookup"><span data-stu-id="98bed-190">The way you get and send the form digest value depends on the add-in</span></span>
<span data-ttu-id="98bed-191"><a name="FormDigest"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-191"><a name="FormDigest"> </a></span></span>

<span data-ttu-id="98bed-p123">Wenn Sie eine POST-Anforderung senden, muss die Anforderung im **X-RequestDigest**-Header den Formulardigestwert enthalten. Wie Sie den Wert abrufen und senden, ist jedoch je nach Add-In unterschiedlich:</span><span class="sxs-lookup"><span data-stu-id="98bed-p123">When you send a POST request, the request must include the form digest value in the  **X-RequestDigest** header. However, the way you get and send the value differs by add-in:</span></span>
 
- <span data-ttu-id="98bed-194">In in SharePoint gehosteten Add-Ins können Sie einfach den folgenden Header übergeben:</span><span class="sxs-lookup"><span data-stu-id="98bed-194">In SharePoint-hosted add-ins, you can just pass the following header:</span></span> 
 
 `X-RequestDigest": $("#__REQUESTDIGEST").val()`
    
- <span data-ttu-id="98bed-195">Rufen Sie in Cloud-gehosteten Add-Ins, die OAuth verwenden, zuerst den Formulardigestwert ab, indem sie eine Anforderung an den **contextinfo**-Endpunkt senden, und dann der Anforderung den Wert hinzufügen, wie unter [Schreiben von Daten unter Verwendung der REST-Schnittstelle](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData) gezeigt.</span><span class="sxs-lookup"><span data-stu-id="98bed-195">In cloud-hosted add-ins that use OAuth, first retrieve the form digest value by sending a request to the  **contextinfo** endpoint, and then add it to requests, as shown in [Writing data by using the REST interface](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).</span></span>
    
- <span data-ttu-id="98bed-p124">In Cloud-gehosteten Add-Ins, welche die domänenübergreifende JavaScript-Bibliothek verwenden, müssen Sie den Formulardigestwert nicht angeben. SP.RequestExecutor gibt diesen automatisch für Sie an (ebenso wie den Inhalt-Länge-Wert).</span><span class="sxs-lookup"><span data-stu-id="98bed-p124">In cloud-hosted add-ins that use the JavaScript cross-domain library, you don't need to specify the form digest value. By default, SP.RequestExecutor automatically handles this for you. (It also handles the content-length value.)</span></span>

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a><span data-ttu-id="98bed-199">Add-Ins, die OAuth verwenden, müssen Zugriffstoken in Anforderungen übergeben</span><span class="sxs-lookup"><span data-stu-id="98bed-199">Add-ins that use OAuth must pass access tokens in requests</span></span>
<span data-ttu-id="98bed-200"><a name="OAuthTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-200"></span></span>

<span data-ttu-id="98bed-p125">In der Cloud gehostete Add-Ins autorisieren den Zugriff auf SharePoint-Daten entweder mit OAuth oder mit der domänenübergreifenden Bibliothek. Add-In-Komponenten mit auf einem Remotewebserver ausgeführtem Code müssen OAuth verwenden, um den Zugriff auf SharePoint-Daten zu autorisieren. In diesem Fall müssen Sie einen **Authorization**-Header zum Senden des Zugriffstokens einbeziehen. Unter [Lesen von Daten mit der SharePoint REST-Schnittstelle](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData) finden Sie ein Beispiel, in dem einem **HTTPWebRequest**-Objekt ein Autorisierungsheader hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="98bed-p125">Cloud-hosted add-ins use either OAuth or the cross-domain library to authorize access to SharePoint data. Add-in components with code that runs on a remote web server must use OAuth to authorize access to SharePoint data. In this case, you need to include an  **Authorization** header to send the access token. See [Reading data with the SharePoint REST interface](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData) for an example that adds an authorization header to an **HTTPWebRequest** object.</span></span>
 
 <span data-ttu-id="98bed-p126">**Hinweis** In der Cloud gehostete Add-In-Komponenten, die in JavaScript geschrieben wurden, müssen zum Zugreifen auf SharePoint-Daten das **SP.RequestExecutor**-Objekt in der domänenübergreifenden Bibliothek verwenden. Domänenübergreifende Bibliotheksanforderungen müssen kein Zugriffstoken enthalten.</span><span class="sxs-lookup"><span data-stu-id="98bed-p126">**Note**  Cloud-hosted add-in components that are written in JavaScript must use the  **SP.RequestExecutor** object in the cross-domain library to access to SharePoint data. Cross-domain library requests don't need to include an access token.</span></span>
 
<span data-ttu-id="98bed-207">Weitere Informationen zu OAuth-Zugriffstoken und wie diese abgerufen werden, finden Sie unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) und [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).</span><span class="sxs-lookup"><span data-stu-id="98bed-207">To learn more about OAuth access tokens and how to get them, see  [Context Token OAuth flow for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) and [Authorization Code OAuth flow for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).</span></span>
 
### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a><span data-ttu-id="98bed-208">Endpunkt-URIs in domänenübergreifenden Bibliotheksanforderungen verwenden "SP.AppContextSite", um den Kontext zu ändern</span><span class="sxs-lookup"><span data-stu-id="98bed-208">Endpoint URIs in cross-domain requests use SP.AppContextSite to change the context</span></span>
<span data-ttu-id="98bed-209"><a name="AppContextSite"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-209"></span></span>

<span data-ttu-id="98bed-p127">Die Anforderungen werden an den in der **url**-Eigenschaft der Anforderung angegebenen Ressourcenendpunkt gesendet. Endpunkt-URIs verwenden das folgende Format:</span><span class="sxs-lookup"><span data-stu-id="98bed-p127">Requests are sent to the resource endpoint that's specified in the  **url** property of the request. Endpoint URIs use the following format:</span></span>
 
 `_<site url>_/_api/ _<context>_/ _<resource>_ (example, https://contoso.com/_api/web/lists)`
 
<span data-ttu-id="98bed-p128">Domänenübergreifende Bibliotheksanforderungen verwenden dieses Format für den Zugriff auf Daten im Add-In-Web. Dies ist der Standardkontext für domänenübergreifende Bibliotheksanforderungen. Um jedoch auf Daten im Hostweb oder in einer anderen Websitesammlung zugreifen zu können, müssen die Anforderungen das Hostweb oder die andere Websitesammlung als Kontext initialisieren. Hierzu wird wie in Tabelle 1 gezeigt der **SP.AppContextSite**-Endpunkt im URI verwendet. Die in Tabelle 1 aufgeführten Beispiel-URIs verwenden den **@target**-Alias zum Senden der Ziel-URL in der Abfragezeichenfolge, weil die URL ein Sonderzeichen (':') enthält.</span><span class="sxs-lookup"><span data-stu-id="98bed-p128">Cross-domain library requests use this format when they access data on the add-in web, which is the default context for cross-domain library requests. But to access data on the host web or on another site collection, the requests need to initialize the host web or other site collection as the context. To do this, they use the  **SP.AppContextSite** endpoint in the URI, as shown in Table 1. The example URIs in Table 1 use the **@target** alias to send the target URL in the query string because the URL contains a special character (':').</span></span>

 <span data-ttu-id="98bed-216">**Hinweis** Damit ein in der Cloud gehostetes Add-In beim Verwenden der domänenübergreifenden Bibliothek auf SharePoint-Daten zugreifen kann, ist eine Add-In-Webinstanz erforderlich.</span><span class="sxs-lookup"><span data-stu-id="98bed-216">**Note**  An add-in web instance is required for a cloud-hosted add-in to access SharePoint data when using the cross-domain library.</span></span>

<span data-ttu-id="98bed-217">**Tabelle 1: Verwenden des „SP.AppContextSite“-Endpunkts zum Ändern des Kontexts der Anforderung**</span><span class="sxs-lookup"><span data-stu-id="98bed-217">**Table 1. Using the SP.AppContextSite endpoint to change the context of the request**</span></span>


|<span data-ttu-id="98bed-218">**Add-In-Typ**</span><span class="sxs-lookup"><span data-stu-id="98bed-218">**Add-in type**</span></span>|<span data-ttu-id="98bed-219">**Szenario für den domänenübergreifenden Datenzugriff**</span><span class="sxs-lookup"><span data-stu-id="98bed-219">**Cross-domain data access scenario**</span></span>|<span data-ttu-id="98bed-220">**Beispiel-Endpunkt-URI**</span><span class="sxs-lookup"><span data-stu-id="98bed-220">**Example endpoint URI**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="98bed-221">In der Cloud gehostet</span><span class="sxs-lookup"><span data-stu-id="98bed-221">Cloud-hosted</span></span>|<span data-ttu-id="98bed-222">JavaScript-Add-In-Komponente, die mithilfe der domänenübergreifenden Bibliothek auf Hostwebdaten zugreift</span><span class="sxs-lookup"><span data-stu-id="98bed-222">JavaScript add-in component accessing host web data by using the cross-domain library</span></span>| <span data-ttu-id="98bed-223">_<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'</span><span class="sxs-lookup"><span data-stu-id="98bed-223">_<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'</span></span>|
|<span data-ttu-id="98bed-224">In der Cloud gehostet</span><span class="sxs-lookup"><span data-stu-id="98bed-224">Cloud-hosted</span></span>|<span data-ttu-id="98bed-225">JavaScript-Add-In-Komponente, die mithilfe der domänenübergreifenden Bibliothek auf Daten zugreift, die sich in einer anderen Websitesammlung als dem Hostweb befinden (gilt nur für Add-Ins mit Mandantenbereich)</span><span class="sxs-lookup"><span data-stu-id="98bed-225">JavaScript add-in component accessing data in a site collection other than the host web by using the cross-domain library (tenant-scoped add-ins only)</span></span>| <span data-ttu-id="98bed-226">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span><span class="sxs-lookup"><span data-stu-id="98bed-226">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span></span>|
|<span data-ttu-id="98bed-227">Auf SharePoint gehostet</span><span class="sxs-lookup"><span data-stu-id="98bed-227">SharePoint-hosted</span></span>|<span data-ttu-id="98bed-228">Add-In-Webkomponente, die auf Daten einer anderen Websitesammlung zugreift (gilt nur für Add-Ins mit Mandantenbereich)</span><span class="sxs-lookup"><span data-stu-id="98bed-228">Add-in web component accessing data in another site collection (tenant-scoped add-ins only)</span></span>| <span data-ttu-id="98bed-229">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span><span class="sxs-lookup"><span data-stu-id="98bed-229">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span></span>|

 <span data-ttu-id="98bed-p129">
  **Hinweis** In Szenarien für den domänenübergreifenden Datenzugriff sind auch die entsprechenden Add-In-Berechtigungen erforderlich. Weitere Informationen finden Sie unter  [Zugreifen auf Daten in einem Hostweb](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_Hostweb) und [Zugreifen auf Daten in allen Websitesammlungen](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_TenantScope).</span><span class="sxs-lookup"><span data-stu-id="98bed-p129">**Note**  Cross-domain data access scenarios also require appropriate add-in permissions. For more information, see  [Access data from the host web](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_Hostweb) and [Access data across site collections](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_TenantScope).</span></span>

<span data-ttu-id="98bed-p130">SharePoint-Add-Ins können die Add-In-Web-URL und die Hostweb-URL aus der Abfragezeichenfolge der Add-In-Seite abrufen. Dies wird im folgenden Codebeispiel gezeigt. Aus dem Beispiel geht außerdem hervor, wie auf die domänenübergreifende Bibliothek verwiesen wird, die im Hostweb in der Datei "SP.RequestExecutor.js" definiert ist. In dem Beispiel wird davon ausgegangen, dass Ihr Add-In über SharePoint gestartet wird. Unter  [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) finden Sie Anleitungen, wie Sie Ihren SharePoint-Kontext richtig festlegen, wenn das Add-In nicht über SharePoint gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="98bed-p130">SharePoint Add-ins can get the add-in web URL and host web URL from the query string of the add-in page, as shown in the following code example. The example also shows how to reference the cross-domain library, which is defined in the SP.RequestExecutor.js file on the host web. The example assumes that your add-in launches from SharePoint. See  [Authorization Code OAuth flow for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) for guidance on setting your SharePoint context correctly when your add-in does not launch from SharePoint.</span></span>

```javascript
var hostweburl;
var appweburl;

// Get the URLs for the add-in web the host web URL from the query string.
$(document).ready(function () {
  //Get the URI decoded URLs.
  hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
  appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

  // Load the SP.RequestExecutor.js file.
  $.getScript(hostweburl + "/_layouts/15/SP.RequestExecutor.js", runCrossDomainRequest);
});

// Build and send the HTTP request.
function runCrossDomainRequest() {
  var executor = new SP.RequestExecutor(appweburl); 
  executor.executeAsync({
      url: appweburl + "/_api/SP.AppContextSite(@target)/web/lists?@target='" + hostweburl + "'",
      method: "GET", 
      headers: { "Accept": "application/json; odata=verbose" }, 
      success: successHandler, 
      error: errorHandler 
  });
}

// Get a query string value.
// For production add-ins, you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("?")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve) return singleParam[1];
  }
}
… // success and error callback functions
```

## <a name="properties-used-in-rest-requests"></a><span data-ttu-id="98bed-236">In REST-Anforderungen verwendete Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="98bed-236">Properties used in REST requests</span></span>
<span data-ttu-id="98bed-237"><a name="bk_requestElements"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-237"></span></span>

<span data-ttu-id="98bed-238">In Tabelle 2 sind häufig in HTTP-Anforderungen für den SharePoint-REST-Dienst verwendete Eigenschaften aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="98bed-238">Table 2 shows properties that are commonly used in HTTP requests for the SharePoint REST service.</span></span>
 
<span data-ttu-id="98bed-239">**Tabelle 2: Verwendung von REST-Anforderungseigenschaften in HTTP-Anforderungen**</span><span class="sxs-lookup"><span data-stu-id="98bed-239">**Table 2. When to use REST request properties in HTTP requests**</span></span>

|<span data-ttu-id="98bed-240">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="98bed-240">**Properties**</span></span>|<span data-ttu-id="98bed-241">**Wann erforderlich**</span><span class="sxs-lookup"><span data-stu-id="98bed-241">**When required**</span></span>|<span data-ttu-id="98bed-242">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="98bed-242">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="98bed-243">**url**</span><span class="sxs-lookup"><span data-stu-id="98bed-243">**url**</span></span>|<span data-ttu-id="98bed-244">Alle Anforderungen</span><span class="sxs-lookup"><span data-stu-id="98bed-244">All requests</span></span>|<span data-ttu-id="98bed-p131">Die URL eines REST-Ressourcenendpunkts. Beispiel:  `http://<site url>/_api/web/lists`</span><span class="sxs-lookup"><span data-stu-id="98bed-p131">The URL of the REST resource endpoint. Example:  `http://<site url>/_api/web/lists`</span></span>|
|<span data-ttu-id="98bed-247">**method** (oder **type**)</span><span class="sxs-lookup"><span data-stu-id="98bed-247">**method** (or **type**)</span></span>|<span data-ttu-id="98bed-248">Alle Anforderungen</span><span class="sxs-lookup"><span data-stu-id="98bed-248">All requests</span></span>|<span data-ttu-id="98bed-p132">Die HTTP-Anforderungsmethode: **GET** für Lesevorgänge und **POST** für Schreibvorgänge. **POST**-Anforderungen können Aktualisierungs- oder Löschvorgänge durchführen, wenn das Verb **DELETE**, **MERGE** oder **PUT** im **X-HTTP-Method**-Header angegeben wird.  </span><span class="sxs-lookup"><span data-stu-id="98bed-p132">The HTTP request method:  **GET** for read operations and **POST** for write operations. **POST** requests can perform update or delete operations by specifying a **DELETE**,  **MERGE**, or  **PUT** verb in the **X-HTTP-Method** header.</span></span>|
|<span data-ttu-id="98bed-251">**body** (oder **data**)</span><span class="sxs-lookup"><span data-stu-id="98bed-251">**body** (or **data**)</span></span>|<span data-ttu-id="98bed-252">**POST**-Anforderungen, die Daten im Anforderungstextkörper senden</span><span class="sxs-lookup"><span data-stu-id="98bed-252">**POST** requests that send data in the request body</span></span>|<span data-ttu-id="98bed-p133">Der Textkörper der POST-Anforderung. Sendet Daten (z. B. komplexe Typen), die nicht in einer Endpunkt-URI gesendet werden können. Wird mit dem **content-length**-Header verwendet.</span><span class="sxs-lookup"><span data-stu-id="98bed-p133">The body of the POST request. Sends data (such as complex types) that can't be sent in the endpoint URI. Used with the  **content-length** header.</span></span>|
|<span data-ttu-id="98bed-256">**Authentication**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-256">**Authentication** header</span></span>|<span data-ttu-id="98bed-p134">Remote-Add-Ins verwenden OAuth, um Benutzer zu authentifizieren. Dies gilt nicht bei der Verwendung von JavaScript oder der domänenübergreifenden Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="98bed-p134">Remote add-ins that are using OAuth to authenticate users. Does not apply when using JavaScript or the cross domain library.</span></span>|<span data-ttu-id="98bed-p135">Sendet den OAuth-Zugriffstoken (erhalten von einem sicheren Token-Server von Microsoft Access Control Service (ACS)), der zur Authentifizierung der Anforderung des Nutzers verwendet wird. Beispiel:  `"Authorization": "Bearer " + accessToken`, wobei  `accessToken` für die Variable steht, die den Token enthält. Token müssen mittels serverseitigem Code abgerufen werden. </span><span class="sxs-lookup"><span data-stu-id="98bed-p135">Sends the OAuth access token (obtained from a Microsoft Access Control Service (ACS) secure token server) that's used to authenticate the user for the request. Example:  `"Authorization": "Bearer " + accessToken`, where  `accessToken` represents the variable that stores the token. Tokens must be retrieved by using server-side code.</span></span>|
|<span data-ttu-id="98bed-262">**X-RequestDigest**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-262">**X-RequestDigest** header</span></span>|<span data-ttu-id="98bed-263">**POST**-Anforderungen (außer SP.RequestExecutor-Anforderungen)</span><span class="sxs-lookup"><span data-stu-id="98bed-263">**POST** requests (except SP.RequestExecutor requests)</span></span>|<span data-ttu-id="98bed-p136">Remote-Add-Ins, die OAuth verwenden, können den Formulardigestwert vom Endpunkt  `http://<site url>/_api/contextinfo` abrufen. In SharePoint gehostete Add-Ins können den Wert über das **#__REQUESTDIGEST**-Seitensteuerelement abrufen, wenn es auf der SharePoint-Seite verfügbar ist. Weitere Informationen finden Sie unter  [Schreiben von Daten unter Verwendung der REST-Schnittstelle](#WritingData).  </span><span class="sxs-lookup"><span data-stu-id="98bed-p136">Remote add-ins that use OAuth can get the form digest value from the  `http://<site url>/_api/contextinfo` endpoint. SharePoint-hosted add-ins can get the value from the **#__REQUESTDIGEST** page control if it's available on the SharePoint page. See [Writing data by using the REST interface](#WritingData).</span></span>|
|<span data-ttu-id="98bed-267">**accept**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-267">**accept** header</span></span>|<span data-ttu-id="98bed-268">Anforderungen, die SharePoint-Metadaten zurückgeben</span><span class="sxs-lookup"><span data-stu-id="98bed-268">Requests that return SharePoint metadata</span></span>|<span data-ttu-id="98bed-p137">Gibt das Format für Antwortdaten vom Server an. Das Standardformat ist  `application/atom+xml`. Beispiel:  `"accept":"application/json;odata=verbose"`</span><span class="sxs-lookup"><span data-stu-id="98bed-p137">Specifies the format for response data from the server. The default format is  `application/atom+xml`. Example:  `"accept":"application/json;odata=verbose"`</span></span>|
|<span data-ttu-id="98bed-272">**content-type**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-272">**content-type** header</span></span>|<span data-ttu-id="98bed-273">**POST**-Anforderungen, die Daten im Anforderungstextkörper senden</span><span class="sxs-lookup"><span data-stu-id="98bed-273">**POST** requests that send data in the request body</span></span>|<span data-ttu-id="98bed-p138">Gibt das Format der Daten an, die der Client an den Server sendet. Das Standardformat ist  `application/atom+xml`. Beispiel:  `"content-type":"application/json;odata=verbose"`</span><span class="sxs-lookup"><span data-stu-id="98bed-p138">Specifies the format of the data that the client is sending to the server. The default format is  `application/atom+xml`. Example:  `"content-type":"application/json;odata=verbose"`</span></span>|
|<span data-ttu-id="98bed-277">**content-length**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-277">**content-length** header</span></span>|<span data-ttu-id="98bed-278">**POST**-Anforderungen, die Daten im Anforderungstextkörper senden (außer SP.RequestExecutor-Anforderungen)</span><span class="sxs-lookup"><span data-stu-id="98bed-278">**POST** requests that send data in the request body (except SP.RequestExecutor requests)</span></span>|<span data-ttu-id="98bed-p139">Gibt die Länge des Inhalts an. Beispiel:  `"content-length":requestBody.length`</span><span class="sxs-lookup"><span data-stu-id="98bed-p139">Specifies the length of the content. Example:  `"content-length":requestBody.length`</span></span>|
|<span data-ttu-id="98bed-281">**IF-MATCH**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-281">**IF-MATCH** header</span></span>|<span data-ttu-id="98bed-282">**POST**-Anforderungen für **DELETE**-, **MERGE**- oder **PUT**-Vorgänge, in erster Linie, um Listen und Bibliotheken zu ändern.</span><span class="sxs-lookup"><span data-stu-id="98bed-282">**POST** requests for **DELETE**,  **MERGE**, or  **PUT** operations, primarily for changing lists and libraries.</span></span>|<span data-ttu-id="98bed-p140">Bietet eine Möglichkeit, zu überprüfen, dass das Objekt, das geändert wird, seit seinem letzten Abruf nicht geändert wurde. Sie können aber auch festlegen, dass alle Änderungen überschrieben werden, wie im folgenden Beispiel zu sehen:  `"IF-MATCH":"*"`</span><span class="sxs-lookup"><span data-stu-id="98bed-p140">Provides a way to verify that the object being changed has not been changed since it was last retrieved. Or, lets you specify to overwrite any changes, as shown in the following example:  `"IF-MATCH":"*"`</span></span>|
|<span data-ttu-id="98bed-285">**X-HTTP-Method**-Header</span><span class="sxs-lookup"><span data-stu-id="98bed-285">**X-HTTP-Method** header</span></span>|<span data-ttu-id="98bed-286">**POST**-Anforderungen für **DELETE**-, **MERGE**- oder **PUT**-Vorgänge</span><span class="sxs-lookup"><span data-stu-id="98bed-286">**POST** requests for **DELETE**,  **MERGE**, or  **PUT** operations</span></span>|<span data-ttu-id="98bed-p141">Wird verwendet, um festzulegen, dass die Anforderung einen Aktualisierungs- oder Löschvorgang durchführt. Beispiel: `"X-HTTP-Method":"PUT"`</span><span class="sxs-lookup"><span data-stu-id="98bed-p141">Used to specify that the request performs an update or delete operation. Example:  `"X-HTTP-Method":"PUT"`</span></span>|
|<span data-ttu-id="98bed-289">**binaryStringRequestBody**</span><span class="sxs-lookup"><span data-stu-id="98bed-289">**binaryStringRequestBody**</span></span>|<span data-ttu-id="98bed-290">SP.RequestExecutor-**POST**-Anforderungen, die binäre Daten im Anforderungstextkörper senden</span><span class="sxs-lookup"><span data-stu-id="98bed-290">SP.RequestExecutor  **POST** requests that send binary data in the body</span></span>|<span data-ttu-id="98bed-p142">Gibt an, ob der Anforderungstextkörper eine binäre Zeichenfolge ist. **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="98bed-p142">Specifies whether the request body is a binary string.  **Boolean**.</span></span>|
|<span data-ttu-id="98bed-293">**binaryStringResponseBody**</span><span class="sxs-lookup"><span data-stu-id="98bed-293">**binaryStringResponseBody**</span></span>|<span data-ttu-id="98bed-294">SP.RequestExecutor-Anforderungen, die binäre Daten zurückgeben</span><span class="sxs-lookup"><span data-stu-id="98bed-294">SP.RequestExecutor requests that return binary data</span></span>|<span data-ttu-id="98bed-p143">Gibt an, ob die Antwort eine binäre Zeichenfolge ist. **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="98bed-p143">Specifies whether the response is a binary string.  **Boolean**.</span></span>|

## <a name="batch-job-support"></a><span data-ttu-id="98bed-297">Unterstützung für Batchaufträge</span><span class="sxs-lookup"><span data-stu-id="98bed-297">Batch job support</span></span>
<span data-ttu-id="98bed-298"><a name="batch"> </a> Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`.</span><span class="sxs-lookup"><span data-stu-id="98bed-298">The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  <a name="batch"></a> query option. For details and links to code samples, see `$batch`.</span></span> <span data-ttu-id="98bed-299">Einzelheiten und Links zu Codebeispielen finden Sie unter [Erstellen von Batchanforderungen mit den REST-APIs](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="98bed-299">For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98bed-300">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="98bed-300">Additional resources</span></span>
<span data-ttu-id="98bed-301"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="98bed-301"></span></span>

-  [<span data-ttu-id="98bed-302">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="98bed-302">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="98bed-303">Arbeiten mit Ordner und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="98bed-303">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md) 
-  [<span data-ttu-id="98bed-304">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="98bed-304">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="98bed-305">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="98bed-305">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [<span data-ttu-id="98bed-306">SharePoint 2013: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="98bed-306">SharePoint 2013: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  <span data-ttu-id="98bed-307">
  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx)</span><span class="sxs-lookup"><span data-stu-id="98bed-307">[Complete basic operations using SharePoint 2013 client library code](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx)</span></span>
-  <span data-ttu-id="98bed-308">
  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx)</span><span class="sxs-lookup"><span data-stu-id="98bed-308">[Complete basic operations using JavaScript library code in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx)</span></span>
-  <span data-ttu-id="98bed-309">
  [Entwickeln von SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj163794.aspx)</span><span class="sxs-lookup"><span data-stu-id="98bed-309">[Develop SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/jj163794.aspx)</span></span>
-  <span data-ttu-id="98bed-310">
  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/fp179897.aspx)</span><span class="sxs-lookup"><span data-stu-id="98bed-310">[Secure data access and client object models for SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/office/fp179897.aspx)</span></span>
-  <span data-ttu-id="98bed-311">
  [Arbeiten mit externen Daten in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179893.aspx)</span><span class="sxs-lookup"><span data-stu-id="98bed-311">[Work with external data in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179893.aspx)</span></span>
-  [<span data-ttu-id="98bed-312">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="98bed-312">Open Data Protocol</span></span>](http://www.odata.org/)
-  [<span data-ttu-id="98bed-313">OData: JSON(JavaScript Object Notation)-Format</span><span class="sxs-lookup"><span data-stu-id="98bed-313">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
-  [<span data-ttu-id="98bed-314">Festlegen von benutzerdefinierten Berechtigungen in einer Liste mit der REST-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="98bed-314">Set custom permissions on a list by using the REST interface</span></span>](set-custom-permissions-on-a-list-by-using-the-rest-interface.md)
