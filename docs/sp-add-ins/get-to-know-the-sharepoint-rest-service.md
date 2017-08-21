# <a name="get-to-know-the-sharepoint-rest-service"></a><span data-ttu-id="ec62d-101">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="ec62d-101">Get to know the SharePoint REST service</span></span>
<span data-ttu-id="ec62d-102">Hier erhalten Sie grundlegende Informationen zum Verwenden des SharePoint REST-Diensts zum Zugreifen auf und Aktualisieren von SharePoint-Daten mithilfe der REST- und OData-Webprotokollstandards.</span><span class="sxs-lookup"><span data-stu-id="ec62d-102">Get the basics of using the SharePoint REST service to access and update SharePoint data, using the REST and OData web protocol standards.</span></span>
 

 <span data-ttu-id="ec62d-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ec62d-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="ec62d-p102">In SharePoint wurde ein REST-Dienst (Representational State Transfer) eingeführt, der mit den bestehenden SharePoint-[Clientobjektmodellen](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx) vergleichbar ist. Entwickler können nun über eine beliebige Technologie, die REST-Webanforderungen unterstützt, remote mit SharePoint-Daten interagieren. Dies bedeutet, dass Entwickler mithilfe von REST-Webtechnologien und der standardmäßigen Open Data Protocol(OData)-Syntax über SharePoint-Add-Ins, -Projektmappen und -Clientanwendungen CRUD-Vorgänge (**Erstellen**, **Lesen**, **Aktualisieren** und **Löschen**) ausführen können.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p102">SharePoint 2013 introduced a Representational State Transfer (REST) service that is comparable to the existing SharePoint  [client object models](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx). Now, developers can interact remotely with SharePoint data by using any technology that supports REST web requests. This means that developers can perform  **Create**,  **Read**,  **Update**, and  **Delete** (CRUD) operations from their SharePoint Add-ins, solutions, and client applications, using REST web technologies and standard Open Data Protocol (OData) syntax.</span></span>
 

## <a name="prerequisites"></a><span data-ttu-id="ec62d-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="ec62d-109">Prerequisites</span></span>

<span data-ttu-id="ec62d-110">In diesem Thema wird davon ausgegangen, dass Sie über grundlegende Kenntnisse in REST und im Erstellen von REST-Anfragen verfügen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-110">This topic assumes you have a basic familiarity with REST and how to construct REST requests.</span></span>
 

 

## <a name="how-the-sharepoint-rest-service-works"></a><span data-ttu-id="ec62d-111">Funktionsweise des SharePoint REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="ec62d-111">How the SharePoint REST service works</span></span>
<span data-ttu-id="ec62d-112"><a name="bk_how"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-112"></span></span>

<span data-ttu-id="ec62d-p103">SharePoint bietet Ihnen jetzt die Möglichkeit, mithilfe von REST remote mit SharePoint-Websites zu interagieren. Sie können jetzt mithilfe jeder Technologie, die standardmäßige REST-Funktionen unterstützt, direkt mit SharePoint-Objekten interagieren.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p103">SharePoint adds the ability for you to remotely interact with SharePoint sites by using REST. Now, you can interact directly with SharePoint objects by using any technology that supports standard REST capabilities.</span></span>
 

 
<span data-ttu-id="ec62d-p104">Um mithilfe von REST auf SharePoint-Ressourcen zuzugreifen, erstellen Sie mithilfe des OData-Standards (Open Data Protocol), das der gewünschten Clientobjektmodell-API entspricht, eine RESTful-HTTP-Anforderung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ec62d-p104">To access SharePoint resources using REST, construct a RESTful HTTP request, using the Open Data Protocol (OData) standard, which corresponds to the desired client object model API. For example:</span></span>
 

 
 <span data-ttu-id="ec62d-117">*Clientobjektmodell-Methode:*</span><span class="sxs-lookup"><span data-stu-id="ec62d-117">*Client object model method:*</span></span> 
 

 
<span data-ttu-id="ec62d-118">List.GetByTitle(listname)</span><span class="sxs-lookup"><span data-stu-id="ec62d-118">List.GetByTitle(listname)</span></span> 
 

 
 <span data-ttu-id="ec62d-119">*REST-Endpunkt:*</span><span class="sxs-lookup"><span data-stu-id="ec62d-119">*REST endpoint:*</span></span> 
 

 
 `http://server/site/_api/lists/getbytitle('listname')`
 

 
<span data-ttu-id="ec62d-p105">Der client.svc-Webdienst in SharePoint verarbeitet die HTTP-Anforderung und liefert die entsprechende Antwort im Atom- oder JSON-Format (JavaScript Object Notation). Ihre Clientanwendung muss diese Antwort dann analysieren. Die unten stehende Abbildung zeigt eine allgemeine Übersicht über die REST-Architektur von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p105">The client.svc web service in SharePoint handles the HTTP request, and serves the appropriate response in either Atom or JSON (JavaScript Object Notation) format. Your client application must then parse that response. The figure below shows a high-level view of the SharePoint REST architecture.</span></span>
 

 

<span data-ttu-id="ec62d-123">**Architektur des SharePoint REST-Diensts**</span><span class="sxs-lookup"><span data-stu-id="ec62d-123">**SharePoint REST service architecture**</span></span>

 

 
![Architektur des SharePoint REST-Diensts](../../images/SPF15Con_REST_RESTStructure.png)
 
<span data-ttu-id="ec62d-125">Aufgrund ihrer Funktionen und Benutzerfreundlichkeit bleiben Clientobjektmodelle die erste Entwicklungsoption für die Kommunikation mit SharePoint-Websites mithilfe von verwaltetem .NET Framework-Code, Silverlight oder JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ec62d-125">Because of the functionality and ease of use that client object models provide, they remain the primary development option for communicating with SharePoint sites by using .NET Framework managed code, Silverlight, or JavaScript.</span></span>
 

 

### <a name="use-http-commands-with-the-sharepoint-rest-service"></a><span data-ttu-id="ec62d-126">Verwenden von HTTP-Befehlen im SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="ec62d-126">Use HTTP commands with the SharePoint REST service</span></span>
<span data-ttu-id="ec62d-127"><a name="bk_usingHTTP"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-127"></span></span>

<span data-ttu-id="ec62d-p106">Um die REST-Funktionen zu nutzen, die in SharePoint integriert sind, erstellen Sie mithilfe des OData-Standards, welcher der Clientobjektmodell-API entspricht, die Sie verwenden möchten, eine RESTful-HTTP-Anforderung. Der client.svc-Webdienst in SharePoint verarbeitet die HTTP-Anforderung und liefert die entsprechende Antwort im Atom- oder JSON-Format (JavaScript Object Notation). Die Clientanwendung muss diese Antwort dann analysieren.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p106">To use the REST capabilities that are built into SharePoint, you construct a RESTful HTTP request, using the OData standard, which corresponds to the client object model API you want to use. The client.svc web service handles the HTTP request and serves the appropriate response in either Atom or JavaScript Object Notation (JSON) format. The client application must then parse that response.</span></span>
 

 
<span data-ttu-id="ec62d-p107">Die Endpunkte im SharePoint REST-Dienst entsprechen den Typen und Membern in den SharePoint-Clientobjektmodellen. Mithilfe von HTTP-Anforderungen können Sie diese REST-Endpunkte verwenden, um typische CRUD-Vorgänge in SharePoint-Entitäten, z. B. Listen und Websites, auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p107">The endpoints in the SharePoint REST service correspond to the types and members in the SharePoint client object models. By using HTTP requests, you can use these REST endpoints to perform typical CRUD operations against SharePoint entities, such as lists and sites.</span></span> 
 

 
<span data-ttu-id="ec62d-133">Allgemein gilt:</span><span class="sxs-lookup"><span data-stu-id="ec62d-133">In general:</span></span>
 

 


|<span data-ttu-id="ec62d-134">**Wenn Sie dies an einem Endpunkt ausführen möchten**</span><span class="sxs-lookup"><span data-stu-id="ec62d-134">**If you want to do this to an endpoint**</span></span>|<span data-ttu-id="ec62d-135">**Verwenden Sie diese HTTP-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="ec62d-135">**Use this HTTP request**</span></span>|<span data-ttu-id="ec62d-136">**Zu berücksichtigen**</span><span class="sxs-lookup"><span data-stu-id="ec62d-136">**Keep in mind**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="ec62d-137">Lesen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="ec62d-137">Read a resource</span></span>|<span data-ttu-id="ec62d-138">**GET**</span><span class="sxs-lookup"><span data-stu-id="ec62d-138">**GET**</span></span>||
|<span data-ttu-id="ec62d-139">Erstellen oder Aktualisieren einer Ressource</span><span class="sxs-lookup"><span data-stu-id="ec62d-139">Create or update a resource</span></span>|<span data-ttu-id="ec62d-140">**POST**</span><span class="sxs-lookup"><span data-stu-id="ec62d-140">**POST**</span></span>|<span data-ttu-id="ec62d-p108">Verwenden Sie **POST**, um Entitäten wie Listen und Websites zu erstellen. Der SharePoint REST-Dienst unterstützt das Senden von **POST**-Befehlen mit Objektdefinitionen an Endpunkte, die Sammlungen darstellen. Bei **POST**-Vorgängen werden nicht erforderliche Eigenschaften auf ihre Standardwerte festgelegt. Wenn Sie versuchen, eine schreibgeschützte Eigenschaft als Teil des **POST**-Vorgangs festzulegen, gibt der Dienst eine Ausnahme zurück.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p108">Use  **POST** to create entities such as lists and sites. The SharePoint REST service supports sending **POST** commands that include object definitions to endpoints that represent collections.For  **POST** operations, any properties that are not required are set to their default values. If you attempt to set a read-only property as part of a **POST** operation, the service returns an exception.</span></span>|
|<span data-ttu-id="ec62d-144">Aktualisieren oder Hinzufügen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="ec62d-144">Update or insert a resource</span></span> |<span data-ttu-id="ec62d-145">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ec62d-145">**PUT**</span></span>| <span data-ttu-id="ec62d-p109">Verwenden Sie **PUT**- und **MERGE**-Vorgänge, um vorhandene SharePoint-Objekte zu aktualisieren. Jeder Dienstendpunkt, der einen **set**-Vorgang einer Objekteigenschaft darstellt, unterstützt sowohl **PUT**- als auch **MERGE**-Anforderungen. Bei **MERGE**-Vorgängen ist das Festlegen von Eigenschaften optional; Eigenschaften, die Sie nicht explizit festlegen, behalten ihre aktuelle Eigenschaft. Wenn Sie bei **PUT**-Befehlen nicht alle erforderlichen Eigenschaften in Objektaktualisierungen angeben, gibt der REST-Dienst eine Ausnahme zurück. Zusätzlich werden alle nicht explizit festgelegten Eigenschaften auf ihre Standardeigenschaften festgelegt.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p109">Use **PUT** and **MERGE** operations to update existing SharePoint objects. Any service endpoint that represents an object property **set** operation supports both **PUT** requests and **MERGE** requests. For **MERGE** requests, setting properties is optional; any properties that you do not explicitly set retain their current property. For **PUT** requests, if you do not specify all required properties in object updates, the REST service returns an exception. In addition, any optional properties you do not explicitly set are set to their default properties.</span></span>|
|<span data-ttu-id="ec62d-151">Löschen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="ec62d-151">Delete a resource</span></span>|<span data-ttu-id="ec62d-152">**DELETE**</span><span class="sxs-lookup"><span data-stu-id="ec62d-152">**DELETE**</span></span>|<span data-ttu-id="ec62d-153">Verwenden Sie den HTTP-Befehl **DELETE** für die spezifische Endpunkt-URL, um das durch den Endpunkt dargestellte SharePoint-Objekt zu löschen. Bei wiederverwendbaren Objekten, wie Listen, Dateien und Listenelementen, führt dies zu einer **Recycle**-Operation.</span><span class="sxs-lookup"><span data-stu-id="ec62d-153">Use the HTTP  **DELETE** command against the specific endpoint URL to delete the SharePoint object represented by that endpoint.In the case of recyclable objects, such as lists, files, and list items, this results in a  **Recycle** operation.</span></span>|

### <a name="construct-rest-urls-to-access-sharepoint-resources"></a><span data-ttu-id="ec62d-154">Erstellen von REST-URLs für den Zugriff auf SharePoint-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ec62d-154">Construct REST URLs to access SharePoint resources</span></span>
<span data-ttu-id="ec62d-155"><a name="bk_constructURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-155"></span></span>

<span data-ttu-id="ec62d-p110">Wann immer möglich, bildet die URI für diese REST-Endpunkte die API-Signatur der Ressource im SharePoint-Clientobjektmodell streng nach. Die zentralen Einstiegspunkte für den REST-Service stellen die Websitesammlung und die Website des angegebenen Kontexts dar.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p110">Whenever possible, the URI for these REST endpoints closely mimics the API signature of the resource in the SharePoint client object model. The main entry points for the REST service represent the site collection and site of the specified context.</span></span> 
 

 
<span data-ttu-id="ec62d-158">Gehen Sie folgendermaßen vor, um auf eine bestimmte Websitesammlung zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="ec62d-158">To access a specific site collection, use the following construction:</span></span>
 

 
 `http://server/site/_api/site`
 

 
<span data-ttu-id="ec62d-159">Gehen Sie folgendermaßen vor, um auf eine bestimmte Website zuzugreifen:</span><span class="sxs-lookup"><span data-stu-id="ec62d-159">To access a specific site, use the following construction:</span></span>
 

 
 `http://server/site/_api/web`
 

 
<span data-ttu-id="ec62d-160">Dabei steht *server* für den Namen des Servers und *site* für den Namen der oder den Pfad zur entsprechenden Website.</span><span class="sxs-lookup"><span data-stu-id="ec62d-160">In each case,  *server*  represents the name of the server, and *site*  represents the name of, or path to, the specific site.</span></span>
 

 
<span data-ttu-id="ec62d-161">Ausgehend davon können Sie dann spezifischere REST-URIs erstellen, indem Sie das Objektmodell mithilfe der durch Schrägstrich (/) getrennten Namen der APIs aus dem Clientobjektmodell durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-161">From this starting point, you can then construct more specific REST URIs by ''walking" the object model, using the names of the APIs from the client object model separated by a forward slash (/).</span></span>
 

 
<span data-ttu-id="ec62d-p111">Diese Syntax kann nicht für die SocialFeedManager- oder die SocialFollowingManager-REST-API verwendet werden. Weitere Informationen finden Sie in  [REST-API-Referenz für sozialen Feed für SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) und [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec62d-p111">This syntax doesn't apply to the SocialFeedManager or SocialFollowingManager REST APIs. See  [Social feed REST API reference for SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) and [Following people and content REST API reference for SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx) for more information.</span></span>
 

 
<span data-ttu-id="ec62d-164">Weitere Richtlinien zur Ermittlung von URIs von SharePoint-REST-Endpunkten aus der Signatur der entsprechenden Clientobjektmodell-APIs finden Sie in  [Ermitteln von URIs von SharePoint-REST-Dienstendpunkten](determine-sharepoint-rest-service-endpoint-uris).</span><span class="sxs-lookup"><span data-stu-id="ec62d-164">See  [Determine SharePoint REST service endpoint URIs](determine-sharepoint-rest-service-endpoint-uris) for more guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>
 

 

## <a name="sharepoint-rest-endpoint-examples"></a><span data-ttu-id="ec62d-165">Beispiele für SharePoint REST-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="ec62d-165">SharePoint REST endpoint examples</span></span>
<span data-ttu-id="ec62d-166"><a name="bk_URLexamples"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-166"></span></span>

<span data-ttu-id="ec62d-p112">Die folgende Tabelle enthält Beispiele für typische REST-Endpunkt-URLs, um Ihnen den Einstieg in die Arbeit mit SharePoint-Daten zu erleichtern. Stellen Sie den in der Tabelle gezeigten URL-Fragmenten `http://server/site/_api/` voran, um eine vollständig qualifizierte REST-URL zu konstruieren. Wenn für **POST**-Befehle erforderlich, enthält die Tabelle Beispieldaten, die Sie im Hauptteil der HTTP-Anforderung übergeben müssen, um das angegebene SharePoint-Element zu erstellen. Elemente in Kursivschrift stellen Variablen dar, die Sie durch Ihre Werte ersetzen müssen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-p112">The following table contains typical REST endpoint URL examples to get you started working with SharePoint data. Prepend  `http://server/site/_api/` to the URL fragments shown in the table to construct a fully qualified REST URL. Where necessary for **POST** commands, the table contains sample data you must pass in the HTTP request body to create the specified SharePoint item. Items in italics represent variables that you must replace with your values.</span></span>
 

 


|<span data-ttu-id="ec62d-171">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ec62d-171">**Description**</span></span>|<span data-ttu-id="ec62d-172">**URL-Endpunkt**</span><span class="sxs-lookup"><span data-stu-id="ec62d-172">**URL endpoint**</span></span>|<span data-ttu-id="ec62d-173">**HTTP-Methode**</span><span class="sxs-lookup"><span data-stu-id="ec62d-173">**HTTP method**</span></span>|<span data-ttu-id="ec62d-174">**Textkörper**</span><span class="sxs-lookup"><span data-stu-id="ec62d-174">**Body content**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="ec62d-175">Ruft den Titel einer Liste ab</span><span class="sxs-lookup"><span data-stu-id="ec62d-175">Retrieves the title of a list</span></span>| `web/title`|<span data-ttu-id="ec62d-176">GET</span><span class="sxs-lookup"><span data-stu-id="ec62d-176">GET</span></span>|<span data-ttu-id="ec62d-177">–</span><span class="sxs-lookup"><span data-stu-id="ec62d-177">Not applicable</span></span>|
|<span data-ttu-id="ec62d-178">Ruft alle Listen auf einer Website</span><span class="sxs-lookup"><span data-stu-id="ec62d-178">Retrieves all lists on a site</span></span>| `lists`|<span data-ttu-id="ec62d-179">GET</span><span class="sxs-lookup"><span data-stu-id="ec62d-179">GET</span></span>|<span data-ttu-id="ec62d-180">–</span><span class="sxs-lookup"><span data-stu-id="ec62d-180">Not applicable</span></span>|
|<span data-ttu-id="ec62d-181">Ruft die Metadaten einer einzelnen Liste ab</span><span class="sxs-lookup"><span data-stu-id="ec62d-181">Retrieves a single 'list's metadata</span></span>| `lists/getbytitle('listname')`|<span data-ttu-id="ec62d-182">GET</span><span class="sxs-lookup"><span data-stu-id="ec62d-182">GET</span></span>|<span data-ttu-id="ec62d-183">–</span><span class="sxs-lookup"><span data-stu-id="ec62d-183">Not applicable</span></span>|
|<span data-ttu-id="ec62d-184">Ruft Elemente in einer Liste ab</span><span class="sxs-lookup"><span data-stu-id="ec62d-184">Retrieves items within a list</span></span>| `lists/getbytitle('listname')/items`|<span data-ttu-id="ec62d-185">GET</span><span class="sxs-lookup"><span data-stu-id="ec62d-185">GET</span></span>|<span data-ttu-id="ec62d-186">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="ec62d-186">Not applicable</span></span>|
|<span data-ttu-id="ec62d-p113">Ruft eine bestimmte Eigenschaft eines Dokuments ab. (In diesem Fall den Titel des Dokuments.)</span><span class="sxs-lookup"><span data-stu-id="ec62d-p113">Retrieves a specific property of a document. (In this case, the document title.)</span></span>| `lists/getbytitle('listname')?select=Title`|<span data-ttu-id="ec62d-189">GET</span><span class="sxs-lookup"><span data-stu-id="ec62d-189">GET</span></span>|<span data-ttu-id="ec62d-190">–</span><span class="sxs-lookup"><span data-stu-id="ec62d-190">Not applicable</span></span>|
|<span data-ttu-id="ec62d-191">Erstellt eine Liste</span><span class="sxs-lookup"><span data-stu-id="ec62d-191">Creates a list</span></span>| `lists`|<span data-ttu-id="ec62d-192">POST</span><span class="sxs-lookup"><span data-stu-id="ec62d-192">POST</span></span>|
```
{
  '__metadata':{'type':SP.List},
  'AllowContentTypes': true,
  'BaseTemplate': 104 ,
  'ContentTypesEnabled': true,
  'Description': 'My list description ',
  'Title': 'RestTest '
}
```

<span data-ttu-id="ec62d-193">|Fügt ein Element zu einer Liste hinzu| `lists/getbytitle('listname')/items`|POST|</span><span class="sxs-lookup"><span data-stu-id="ec62d-193">|Adds an item to a list| `lists/getbytitle('listname')/items`|POST|</span></span>
```
{
  '__metadata':{'type': SP.Data.'listname'.ListItem},
  'Title': 'MyItem'
}

```

|

## <a name="batch-job-support"></a><span data-ttu-id="ec62d-194">Unterstützung für Batchaufträge</span><span class="sxs-lookup"><span data-stu-id="ec62d-194">Batch job support</span></span>
<span data-ttu-id="ec62d-195"><a name="batch"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-195"></span></span>

<span data-ttu-id="ec62d-p114">Der SharePoint Online-REST-Dienst unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption  `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter  [Erstellen von Batchanforderungen mit den REST-APIs](make-batch-requests-with-the-rest-apis).</span><span class="sxs-lookup"><span data-stu-id="ec62d-p114">The SharePoint Online (and on-premise SharePoint 2016 or later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis). .</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="ec62d-199">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ec62d-199">Additional Resources</span></span>
<span data-ttu-id="ec62d-200"><a name="bk_learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-200"></span></span>

<span data-ttu-id="ec62d-201">Verwenden Sie die unten aufgeführten Ressourcen, um weitere Informationen zum Verwenden des SharePoint REST-Diensts zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="ec62d-201">Use the resources listed below to learn more about using the SharePoint REST service.</span></span>
 

 

|<span data-ttu-id="ec62d-202">**Titel**</span><span class="sxs-lookup"><span data-stu-id="ec62d-202">**Title**</span></span>|<span data-ttu-id="ec62d-203">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ec62d-203">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="ec62d-204">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="ec62d-204">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)|<span data-ttu-id="ec62d-205">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, mit der SharePoint REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-205">Learn how to perform basic create, read, update, and delete (CRUD) operations with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="ec62d-206">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="ec62d-206">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)|<span data-ttu-id="ec62d-207">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Listen und Listenelemente mit der SharePoint REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-207">Learn how to perform basic create, read, update, and delete (CRUD) operations on lists and list items with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="ec62d-208">Arbeiten mit Ordnern und Dateien mit REST</span><span class="sxs-lookup"><span data-stu-id="ec62d-208">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)|<span data-ttu-id="ec62d-209">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Ordner und Dateien mit der SharePoint REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-209">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="ec62d-210">Navigieren durch die im REST-Dienst dargestellte SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="ec62d-210">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)|<span data-ttu-id="ec62d-211">Informationen zum Starten von einem REST-Endpunkt für einen gegebenen SharePoint-Element und Navigieren zu und Zugreifen auf dazugehörige Elemente, z. B. übergeordnete Standorte oder die Bibliotheksstruktur, in der sich das jeweilige Element befindet.</span><span class="sxs-lookup"><span data-stu-id="ec62d-211">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span>|
| [<span data-ttu-id="ec62d-212">Ermitteln von URIs von SharePoint-REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="ec62d-212">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)|<span data-ttu-id="ec62d-213">Informieren Sie sich über allgemeine Richtlinien zur Ermittlung von URIs von SharePoint-REST-Endpunkten mithilfe der Signatur der entsprechenden Clientobjektmodell-APIs.</span><span class="sxs-lookup"><span data-stu-id="ec62d-213">Learn general guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>|
| [<span data-ttu-id="ec62d-214">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="ec62d-214">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)|<span data-ttu-id="ec62d-215">Hier erfahren Sie, wie Sie eine Reihe von OData-Abfragezeichenfolgeoperatoren verwenden, um die vom SharePoint REST-Dienst angeforderten Daten auszuwählen, zu filtern und zu ordnen.</span><span class="sxs-lookup"><span data-stu-id="ec62d-215">Learn how to use a wide range of OData query string operators to select, filter, and order the data you request from the SharePoint REST service.</span></span>|
| [<span data-ttu-id="ec62d-216">SharePoint - REST-API, Endpunkte und Beispiele</span><span class="sxs-lookup"><span data-stu-id="ec62d-216">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)|<span data-ttu-id="ec62d-217">Diese Seite enthält Links zu allen REST-Ressourcen, die auf MSDN für SharePoint-Entwickler verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="ec62d-217">This page contains links to all of the REST resources that are available for SharePoint developers on MSDN.</span></span>|
| [<span data-ttu-id="ec62d-218">Übersicht über die REST-API der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="ec62d-218">SharePoint Search REST API overview</span></span>](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx)|<span data-ttu-id="ec62d-219">Fügen Sie Suchfunktionen zu Client- und mobilen Anwendungen hinzu, mit dem Search-REST-Dienst in SharePoint Server 2013 und jeder Technologie, die REST-Webanforderungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ec62d-219">Add search functionality to client and mobile applications using the Search REST service in SharePoint Server 2013 and any technology that supports REST web requests.</span></span>|
| [<span data-ttu-id="ec62d-220">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ec62d-220">Social feed REST API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx)|<span data-ttu-id="ec62d-221">Informieren Sie sich über SharePoint-REST-Endpunkte für feedbezogene Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="ec62d-221">Learn about SharePoint REST endpoints for feed-related tasks.</span></span>|
| [<span data-ttu-id="ec62d-222">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ec62d-222">Following people and content REST API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx)|<span data-ttu-id="ec62d-223">Informieren Sie sich über SharePoint-REST-Endpunkte zum Folgen von Personen und Inhalten.</span><span class="sxs-lookup"><span data-stu-id="ec62d-223">Learn about SharePoint REST endpoints for following people and content.</span></span>|
| [<span data-ttu-id="ec62d-224">Erstellen von Batchanforderungen mit den REST-APIs</span><span class="sxs-lookup"><span data-stu-id="ec62d-224">Make batch requests with the REST APIs</span></span>](make-batch-requests-with-the-rest-apis)|<span data-ttu-id="ec62d-225">Erfahren Sie, wie Sie mehrere Anforderungen zu einem einzigen Aufruf an den REST-Dienst kombinieren.</span><span class="sxs-lookup"><span data-stu-id="ec62d-225">Learn how to combine multiple requests into a single call to the REST service.</span></span>|
| [<span data-ttu-id="ec62d-226">Synchronisieren von SharePoint-Elementen mithilfe des REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="ec62d-226">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)|<span data-ttu-id="ec62d-227">Erfahren Sie, wie Sie mit der Ressource **GetListItemChangesSinceToken**, die Teil des SharePoint REST-Diensts ist, Elemente zwischen SharePoint und Ihren Add-ins oder Diensten synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="ec62d-227">Learn how to synchronize items between SharePoint and your add-ins or services by using the  **GetListItemChangesSinceToken** resource, part of the SharePoint REST service.</span></span>|
| [<span data-ttu-id="ec62d-228">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="ec62d-228">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)|<span data-ttu-id="ec62d-229">Erfahren Sie, wie Sie HTML ETags mit dem SharePoint REST-Dienst für die Gleichzeitigkeitssteuerung von SharePoint-Listen und -Listenelementen verwenden.</span><span class="sxs-lookup"><span data-stu-id="ec62d-229">Learn how to use HTML ETags with the SharePoint REST service for concurrency control of SharePoint lists and list items.</span></span>|

## <a name="odata-resources"></a><span data-ttu-id="ec62d-230">OData-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ec62d-230">OData resources</span></span>
<span data-ttu-id="ec62d-231"><a name="SP15startREST_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ec62d-231"></span></span>


 

 

-  [<span data-ttu-id="ec62d-232">Einführung OData</span><span class="sxs-lookup"><span data-stu-id="ec62d-232">Introducing OData</span></span>](http://msdn.microsoft.com/en-us/data/hh237663)
    
 
-  [<span data-ttu-id="ec62d-233">Open Data Protocol – Beispiel</span><span class="sxs-lookup"><span data-stu-id="ec62d-233">Open Data Protocol by Example</span></span>](http://msdn.microsoft.com/en-us/library/ff478141.aspx)
    
 
-  [<span data-ttu-id="ec62d-234">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="ec62d-234">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="ec62d-235">OData-Protokoll – URI-Konventionen</span><span class="sxs-lookup"><span data-stu-id="ec62d-235">OData Protocol URI Conventions</span></span>](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
    
 
-  [<span data-ttu-id="ec62d-236">Adressieren von Dienstvorgängen</span><span class="sxs-lookup"><span data-stu-id="ec62d-236">Addressing Service Operations</span></span>](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#AddressingServiceOperations)
    
 
-  [<span data-ttu-id="ec62d-237">OData-Protokoll – Vorgänge</span><span class="sxs-lookup"><span data-stu-id="ec62d-237">OData Protocol Operations</span></span>](http://www.odata.org/documentation/odata-version-2-0/operations/)
    
 
-  [<span data-ttu-id="ec62d-238">Fehlerbedingungen</span><span class="sxs-lookup"><span data-stu-id="ec62d-238">Error Conditions</span></span>](http://www.odata.org/documentation/odata-version-2-0/operations#ErrorConditions)
    
 

