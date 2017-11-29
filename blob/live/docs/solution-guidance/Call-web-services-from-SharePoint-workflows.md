---
title: Aufrufen von Webdiensten in SharePoint-workflows
ms.date: 11/03/2017
ms.openlocfilehash: d3ee350dde2f5c9978c6d875518f57e828f35dbc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="call-web-services-from-sharepoint-workflows"></a><span data-ttu-id="95719-102">Aufrufen von Webdiensten in SharePoint-workflows</span><span class="sxs-lookup"><span data-stu-id="95719-102">Call web services from SharePoint workflows</span></span>

<span data-ttu-id="95719-103">Bereitstellen eines SharePoint 2013-Workflows mit der Hostwebsite über ein Add-In für SharePoint und Aufrufen von Webdiensten in SharePoint-Workflows.</span><span class="sxs-lookup"><span data-stu-id="95719-103">Deploy a SharePoint 2013 workflow to the host web from an add-in for SharePoint, and call web services from SharePoint workflows.</span></span>

<span data-ttu-id="95719-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="95719-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="95719-105">Die SharePoint 2013-Add-in-Objektmodell können zum Erstellen und Bereitstellen von Workflows, die auf dem Web-Add-in oder der Hostwebsite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="95719-105">You can use the SharePoint 2013 add-in model to create and deploy workflows that run on either the add-in web or the host web.</span></span> <span data-ttu-id="95719-106">Diese Workflows können mit den Remote gehosteten Teile der vom Anbieter gehosteten-add-ins interagieren. Workflows können auch remote-Webdienste aufrufen, die wichtige Unternehmensdaten in einem der folgenden beiden Methoden enthalten:</span><span class="sxs-lookup"><span data-stu-id="95719-106">These workflows can interact with the remotely hosted portions of provider-hosted add-ins. The workflows can also call remote web services that contain important business data in one of two ways:</span></span> 

- <span data-ttu-id="95719-107">Einfügen, indem Sie die Abfrage von Informationen an den Remote gehosteten Teil des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="95719-107">By passing query information to the remotely hosted portion of the add-in.</span></span> <span data-ttu-id="95719-108">Die Remotewebanwendung klicken Sie dann den Webdienst aufgerufen und übergibt die Informationen mit SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95719-108">The remote web application then calls the web service and passes the information back to SharePoint.</span></span>
    
- <span data-ttu-id="95719-109">Durch Abfragen des Webdiensts mithilfe des Webproxys SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="95719-109">By querying the web service by using the SharePoint 2013 web proxy.</span></span> <span data-ttu-id="95719-110">Der Workflow übergibt die Ergebnisse der Abfrage an den Remote gehosteten Teil das Add-in, das dann die Informationen an SharePoint übergibt.</span><span class="sxs-lookup"><span data-stu-id="95719-110">The workflow passes the results of the query to the remotely hosted portion of the add-in, which then passes the information to SharePoint.</span></span>
    
<span data-ttu-id="95719-111">Die vom Webdienst abgerufene Daten gespeichert werden kann in SharePoint-Listen.</span><span class="sxs-lookup"><span data-stu-id="95719-111">The information retrieved from the web service can be stored in SharePoint lists.</span></span> <span data-ttu-id="95719-112">In diesem Artikel werden drei Codebeispiele, die zeigen, wie Sie Aufrufen von Webdiensten aus Workflows, wie in der folgenden Tabelle aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="95719-112">This article describes three code samples that show you how to call web services from workflows, as listed in the following table.</span></span> <span data-ttu-id="95719-113">In den ersten beiden Beispielen werden die Workflows und die Listen im Web-Add-in bereitgestellt, wenn das Add-in installiert.</span><span class="sxs-lookup"><span data-stu-id="95719-113">In the first two samples, the workflows and the lists are deployed to the add-in web when the add-in installs.</span></span> <span data-ttu-id="95719-114">Das letzte Beispiel stellt die grundlegende Verwaltungsshell von einem Workflow und Anleitungen zur Verwendung in der Hostwebsite bereitzustellen, und ordnen Sie ihm eine Liste auf dem hostweb.</span><span class="sxs-lookup"><span data-stu-id="95719-114">The last sample provides the basic shell of a workflow and instructions for how to deploy it to the host web and associate it with a list on the host web.</span></span> 

<span data-ttu-id="95719-115">**Workflow-Aufgaben und zugehörige Beispiele (engl.)**</span><span class="sxs-lookup"><span data-stu-id="95719-115">**Workflow tasks and associated samples**</span></span>

|<span data-ttu-id="95719-116">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="95719-116">**Task**</span></span>|<span data-ttu-id="95719-117">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="95719-117">**Sample**</span></span>|
|:-----|:-----|
|<span data-ttu-id="95719-118">Aufrufen von benutzerdefinierten Webdiensten mithilfe eines Workflows</span><span class="sxs-lookup"><span data-stu-id="95719-118">Call custom web services from a workflow</span></span>|[<span data-ttu-id="95719-119">Workflow.CallCustomService</span><span class="sxs-lookup"><span data-stu-id="95719-119">Workflow.CallCustomService</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)|
|<span data-ttu-id="95719-120">Rufen Sie einen benutzerdefinierten Webdienst mithilfe eines Workflows und aktualisieren SharePoint mithilfe des Webproxys SharePoint</span><span class="sxs-lookup"><span data-stu-id="95719-120">Call a custom web service from a workflow and update SharePoint by using the SharePoint web proxy</span></span>|[<span data-ttu-id="95719-121">Workflow.CallServiceUpdateSPViaProxy</span><span class="sxs-lookup"><span data-stu-id="95719-121">Workflow.CallServiceUpdateSPViaProxy</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)|
|<span data-ttu-id="95719-122">Zuordnen eines Workflows mit der Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="95719-122">Associate a workflow with the host web</span></span>|[<span data-ttu-id="95719-123">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="95719-123">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)|

## <a name="call-custom-web-services-from-a-workflow"></a><span data-ttu-id="95719-124">Aufrufen von benutzerdefinierten Webdiensten mithilfe eines Workflows</span><span class="sxs-lookup"><span data-stu-id="95719-124">Call custom web services from a workflow</span></span>
<span data-ttu-id="95719-125"><a name="bk1"> </a></span><span class="sxs-lookup"><span data-stu-id="95719-125"></span></span>

<span data-ttu-id="95719-126">Das [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) -Beispiel zeigt, wie Sie einen Workflow zu erstellen, der einen benutzerdefinierten Webdienst aufruft, mit der SharePoint-Listendaten aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="95719-126">The  [Workflow.CallCustomService ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) sample shows you how to create a workflow that calls a custom web service that updates SharePoint list data.</span></span> <span data-ttu-id="95719-127">Es auch zeigt, wie ein vom Anbieter gehosteten-Add-in zu entwerfen, sodass mithilfe der Remote gehosteten Webanwendung, die bereitgestellt wird mit der Add-in einem Webdienst abgefragt.</span><span class="sxs-lookup"><span data-stu-id="95719-127">It also shows you how to design a provider-hosted add-in so that it queries a web service by using the remotely hosted web application that deploys with the add-in.</span></span> <span data-ttu-id="95719-128">In diesem Beispiel ist nützlich, wenn Sie alle Interaktionen mit dem Webdienst vom Remote gehosteten Teil des vom Anbieter gehosteten Add-in behandelt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="95719-128">This sample is useful when you want all the interactions with the web service to be handled by the remotely hosted portion of your provider-hosted add-in.</span></span>

<span data-ttu-id="95719-129">Das Beispiel funktioniert durch Starten eines Workflows von einer remote-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="95719-129">The sample works by starting a workflow from a remote web application.</span></span> <span data-ttu-id="95719-130">Diesen Workflow übergibt Abfrageinformationen, die vom Benutzer an der remote-Webanwendung, der dann diese Informationen zum Erstellen einer Abfrage an den Northwind OData-Webdienst übermittelt.</span><span class="sxs-lookup"><span data-stu-id="95719-130">This workflow passes query information submitted by the user to the remote web application, which then uses that information to construct a query to the Northwind OData web service.</span></span> <span data-ttu-id="95719-131">Die Abfrage gibt die Produktlieferanten für ein bestimmtes Land.</span><span class="sxs-lookup"><span data-stu-id="95719-131">The query returns the product suppliers for a given country.</span></span> <span data-ttu-id="95719-132">Nachdem sie diese Informationen empfangen hat, aktualisiert die Remotewebanwendung eine Lieferanten Produktliste, die in der Web-Add-in das Add-in bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="95719-132">After it receives that information, the remote web application updates a product suppliers list that the add-in has deployed to the add-in web.</span></span>

<span data-ttu-id="95719-133">**Hinweis**  Die [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) -Beispielseite enthält Anweisungen für die Bereitstellung von add-Ins.</span><span class="sxs-lookup"><span data-stu-id="95719-133">**Note**  The  [Workflow.CallCustomService ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) sample page contains instructions for deploying this add-in.</span></span> <span data-ttu-id="95719-134">Sie können auch bereitstellen und Testen mit F5 in Visual Studio debuggen, wenn Sie die Anweisungen in den Blogbeitrag [Debugging SharePoint 2013-Workflows mit Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)befolgen.</span><span class="sxs-lookup"><span data-stu-id="95719-134">You can also deploy and test with F5 debugging in Visual Studio if you follow the instructions in the blog post [Debugging SharePoint 2013 workflows using Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span></span>

<span data-ttu-id="95719-135">Diese app-Startseite enthält ein Dropdownmenü, aus dem Sie ein Land auswählen können, für die Sie eine Produktliste Lieferanten (Abbildung 1) erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="95719-135">This app's start page includes a drop-down menu from which you can select a country for which you want to create a product suppliers list (Figure 1).</span></span> 

<span data-ttu-id="95719-136">**Abbildung 1. Workflow.CallCustomService Beispiel-add-in-Startseite**</span><span class="sxs-lookup"><span data-stu-id="95719-136">**Figure 1. Workflow.CallCustomService sample add-in start page**</span></span>

![Screenshot, der die Startseite der Beispiel-app anzeigt](media/b2def940-9c82-458b-8f57-7ea92548ea71.png)

<span data-ttu-id="95719-138">Die Schaltfläche **Erstellen** , auf dem Bildschirm Ruft eine **Create** -Methode in der Controllers\PartSuppliersController.cs-Datei, die einen neuen Eintrag in der Liste Webpart Lieferanten im Web-Add-in erstellt.</span><span class="sxs-lookup"><span data-stu-id="95719-138">The  **Create** button on the screen calls a **Create** method in the Controllers\PartSuppliersController.cs file that creates a new entry in the Part Suppliers list on the add-in web.</span></span> <span data-ttu-id="95719-139">Die **Create** -Methode ruft dann die **Add** -Methode, die in der Datei Services\PartSuppliersService.cs definiert ist.</span><span class="sxs-lookup"><span data-stu-id="95719-139">The **Create** method then calls the **Add** method that is defined in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="95719-140">Die Abfolge ist in die folgenden beiden Codebeispiele dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-140">The sequence is shown in the following two code examples.</span></span>

<span data-ttu-id="95719-141">**Create-Methode**</span><span class="sxs-lookup"><span data-stu-id="95719-141">**Create method**</span></span>

```
public ActionResult Create(string country, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                var id = service.GetIdByCountry(country);
                if (id == null)
                {
                    id = service.Add(country);
                    TempData["Message"] = "Part Supplier Successfully Created!";
                }
                else
                    TempData["ErrorMessage"] = string.Format("Failed to Create The Part Supplier: There's already a Part Supplier who's country is {0}.", country);

                return RedirectToAction("Details", new { id = id.Value, SPHostUrl = spHostUrl });
            }
        }

```

<span data-ttu-id="95719-142">**"Add"-Methode**</span><span class="sxs-lookup"><span data-stu-id="95719-142">**Add method**</span></span>

```
public int Add(string country)
        {
            var item = list.AddItem(new ListItemCreationInformation());
            item["Country"] = country;
            item.Update();
            clientContext.ExecuteQuery();
            return item.Id;
        }

```

<span data-ttu-id="95719-143">Nach dem Erstellen dieser neuen Listenelements an, zeigt das Add-in eine Schaltfläche, die den Genehmigungsworkflow gestartet wird wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-143">After creating that new list item, the add-in presents a button that starts the approval workflow, as shown in Figure 2.</span></span>

<span data-ttu-id="95719-144">**Abbildung 2. Workflow-Schaltfläche "Start" in der Beispielapp**</span><span class="sxs-lookup"><span data-stu-id="95719-144">**Figure 2. Start Workflow button in the sample app**</span></span>

![Screenshot, der die Seite Workflow starten in der Beispielapp anzeigt](media/1d5fc6a1-79fe-4767-b8d8-905a10354565.png)

<span data-ttu-id="95719-146">Auswahl der Schaltfläche **Workflow starten** , löst die **StartWorkflow** -Methode, die in der Datei Controllers\PartSuppliersController.cs definiert ist.</span><span class="sxs-lookup"><span data-stu-id="95719-146">Choosing the  **Start Workflow** button triggers the **StartWorkflow** method that is defined in the Controllers\PartSuppliersController.cs file.</span></span> <span data-ttu-id="95719-147">Diese Methode Pakete die Add-in-Web-URL, die Webdienst-URL (für die Remote gehosteten Webanwendung nicht für die Northwind-Webdienst) und die Kontext-token-Werte und übergibt sie an die **StartWorkflow** -Methode.</span><span class="sxs-lookup"><span data-stu-id="95719-147">This method packages the add-in web URL, the web service URL (for your remotely hosted web application, not for the Northwind web service), and the context token values, and passes them to the **StartWorkflow** method.</span></span> <span data-ttu-id="95719-148">Die **PartSuppliersService** -Methode wird das Kontext-Token für die Interaktion mit SharePoint benötigen.</span><span class="sxs-lookup"><span data-stu-id="95719-148">The **PartSuppliersService** method will need the context token to interact with SharePoint.</span></span>

```
public ActionResult StartWorkflow(int id, Guid workflowSubscriptionId, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext) as SharePointAcsContext;

            var webServiceUrl = Url.RouteUrl("DefaultApi", new { httproute = "", controller = "Data" }, Request.Url.Scheme);
            var payload = new Dictionary<string, object>
                {
                    { "appWebUrl", spContext.SPAppWebUrl.ToString() },
                    { "webServiceUrl", webServiceUrl },
                    { "contextToken",  spContext.ContextToken }
                };

            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                service.StartWorkflow(workflowSubscriptionId, id, payload);
            }

            TempData["Message"] = "Workflow Successfully Started!";
            return RedirectToAction("Details", new { id = id, SPHostUrl = spHostUrl });
        }

```

<span data-ttu-id="95719-149">Die **StartWorkflow** -Methode erstellt eine Workflowinstanz dann und übergibt die drei Werte (AppWebUrl, WebServiceUrl, ContextToken) in der Nutzlast Variablen für den Workflow gespeichert.</span><span class="sxs-lookup"><span data-stu-id="95719-149">The  **StartWorkflow** method then creates a workflow instance and passes the three values (appWebUrl, webServiceUrl, contextToken) stored in the payload variable to the workflow.</span></span>

```
 {
            var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

            var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
            var subscription = subscriptionService.GetSubscription(subscriptionId);

            var instanceService = workflowServicesManager.GetWorkflowInstanceService();
            instanceService.StartWorkflowOnListItem(subscription, itemId, payload);
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="95719-150">Nachdem der Workflow startet, wird eine **HTTP POST-** Anforderung an die Webanwendung Remote gehosteten erleichtert.</span><span class="sxs-lookup"><span data-stu-id="95719-150">After the workflow starts, it makes a  **POST HTTP** request to the remotely hosted web application.</span></span> <span data-ttu-id="95719-151">Diese Anforderung weist die Webanwendung so aktualisieren Sie die Liste Lieferanten mit Lieferanten für das Land, die der Benutzer gerade hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="95719-151">This request tells the web application to update the suppliers list with the suppliers for the country that the user has just added.</span></span> <span data-ttu-id="95719-152">Die Controllers\DataController.cs-Datei enthält eine **POST** -Methode, die den Inhalt dieser Anforderung empfängt.</span><span class="sxs-lookup"><span data-stu-id="95719-152">The Controllers\DataController.cs file contains a **POST** method that receives the contents of this request.</span></span>

```
public void Post([FromBody]string country)
        {
            var supplierNames = GetSupplierNames(country);
            UpdateSuppliers(country, supplierNames);
        }

```

<span data-ttu-id="95719-153">Die **GetSupplierNames** -Methode (in der Datei Controllers\DataController.cs) erstellt und führt eine LINQ-Abfrage an den Northwind OData-Webdienst für alle Lieferanten ausgewählte Land zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="95719-153">The  **GetSupplierNames** method (in the Controllers\DataController.cs file) constructs and executes a LINQ query to the Northwind OData web service for all the suppliers associated with the selected country.</span></span> <span data-ttu-id="95719-154">Die **UpdateSuppliers** -Methode aktualisiert TheSuppliers dar, der dem neu hinzugefügten Listenelement, klicken Sie dann, wie in den folgenden beiden Codebeispiele dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-154">The **UpdateSuppliers** method then updates theSuppliers field of the newly added list item, as shown in the following two code examples.</span></span>

<span data-ttu-id="95719-155">**Abfrage Nordwind (engl.)**</span><span class="sxs-lookup"><span data-stu-id="95719-155">**Query Northwind**</span></span>

```
private string[] GetSupplierNames(string country)
        {
            Uri uri = new Uri("http://services.odata.org/V3/Northwind/Northwind.svc");
            var entities = new NorthwindEntities(uri);
            var names = entities.Suppliers
                .Where(s => s.Country == country)
                .AsEnumerable()
                .Select(s => s.CompanyName)
                .ToArray();
            return names;
        }

```

<span data-ttu-id="95719-156">**Lieferanten Updateliste**</span><span class="sxs-lookup"><span data-stu-id="95719-156">**Update suppliers list**</span></span>

```
private void UpdateSuppliers(string country, string[] supplierNames)
        {
            var request = HttpContext.Current.Request;
            var authority = request.Url.Authority;
            var spAppWebUrl = request.Headers["SPAppWebUrl"];
            var contextToken = request.Headers["SPContextToken"];

            using (var clientContext = TokenHelper.GetClientContextWithContextToken(
                spAppWebUrl, contextToken, authority))
            {
                var service = new PartSuppliersService(clientContext);
                service.UpdateSuppliers(country, supplierNames);
            }
        }

```

<span data-ttu-id="95719-157">Wenn Sie die Entwurfsansicht der workflow.xaml-Datei in das Verzeichnis Lieferanten Genehmigen des app-Projekts betrachten, sehen Sie (indem Sie auf die Registerkarte **Argumente** am unteren linken Ecke des der Entwurfsansicht), dass der Workflow die drei Werte in Thepayload-Variablen gespeichert sind wird es als Workflow Argumente (Abbildung 3) übergeben.</span><span class="sxs-lookup"><span data-stu-id="95719-157">If you look at the design view of the workflow.xaml file in the Approve Suppliers directory of the app project, you'll see (by choosing the  **Arguments** tab at the bottom left of the design view) that the workflow stores the three values in thepayload variable that is passed to it as workflow arguments (Figure 3).</span></span>

<span data-ttu-id="95719-158">**Abbildung 3. Argumente für den Workflow Nutzlast**</span><span class="sxs-lookup"><span data-stu-id="95719-158">**Figure 3. Payload arguments passed to the workflow**</span></span>

![Screenshot, der auf dem Bildschirm für die Eingabe der Nutzlast Argumente an den Workflow übergeben werden](media/4bd5cbde-d505-4d35-9fe6-50ea79f63263.png)

<span data-ttu-id="95719-160">Die **HttpSend** Aktivität tritt vor dem Workflow Genehmigung.</span><span class="sxs-lookup"><span data-stu-id="95719-160">The  **HttpSend** activity occurs before workflow approval.</span></span> <span data-ttu-id="95719-161">Diese Aktivität sendet die Abfrage **POST** an Ihre remote-Webanwendung, die den Anruf an den Webdienst Northwind ausgelöst wird, und klicken Sie dann das Listenelement aktualisieren (mit der Liste Lieferanten).</span><span class="sxs-lookup"><span data-stu-id="95719-161">This activity sends the **POST** query to your remote web application that triggers the call to the Northwind web service and then the list item update (with the suppliers list).</span></span> <span data-ttu-id="95719-162">Diese Aktivität ist so konfiguriert, dass sendet die Anforderung an ThewebServiceUrl-Wert, der als eine Workflow-Argument (Abbildung 4) übergeben wurde.</span><span class="sxs-lookup"><span data-stu-id="95719-162">This activity is configured to send the request to thewebServiceUrl value that was passed as a workflow argument (Figure 4).</span></span>

<span data-ttu-id="95719-163">**Abbildung 4. HttpSend Aktivität Uri-Wert**</span><span class="sxs-lookup"><span data-stu-id="95719-163">**Figure 4. HttpSend activity Uri value**</span></span>

![Screenshot, der im Textfeld zum Eingeben der Webdienst-URL senden über HTTP anzeigt](media/7f8c1f8c-b045-4b35-9435-5fcf1be12835.png)

<span data-ttu-id="95719-165">Die **POST** -Anforderung übergibt auch den Wert für das Land, das in der Listenelement gespeichert ist, der Workflow (Abbildung 5) arbeitet.</span><span class="sxs-lookup"><span data-stu-id="95719-165">The  **POST** request also passes the country value that is stored in the list item on which the workflow is operating (Figure 5).</span></span>

<span data-ttu-id="95719-166">**Abbildung 5. Eigenschaftenraster für die Aktivität HttpSend**</span><span class="sxs-lookup"><span data-stu-id="95719-166">**Figure 5. Property grid for the HttpSend activity**</span></span>

![Screenshot, der das Eigenschaftenraster für das Senden von HTTP-Aktivität anzeigt](media/7a241a29-5b3b-4c82-b86b-67159685dd02.png)

<span data-ttu-id="95719-168">Der Workflow sendet die AppWebUrl AndcontextToken-Werte für die Webanwendung über die Anforderungsheader (Abbildung 6).</span><span class="sxs-lookup"><span data-stu-id="95719-168">The workflow sends the appWebUrl andcontextToken values to the web application through the request headers (Figure 6).</span></span> <span data-ttu-id="95719-169">Der Header festlegen auch die Inhaltstypen für das Senden und Anforderungen akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="95719-169">The headers also set the content types for sending and accepting requests.</span></span>

<span data-ttu-id="95719-170">**Abbildung 6. Anforderungsheader für die Aktivität HttpSend**</span><span class="sxs-lookup"><span data-stu-id="95719-170">**Figure 6. Request headers for the HttpSend activity**</span></span>

![Screenshot, der das Raster für das Hinzufügen von HTTP senden Anforderungsheader Aktivität anzeigt](media/1c019be6-f509-4ff3-83af-e1ecb1f7fbe5.png)

<span data-ttu-id="95719-172">Wenn der Workflow genehmigt wird, wird den Wert des Felds IsApproved des Listenelements auf **true**.</span><span class="sxs-lookup"><span data-stu-id="95719-172">If the workflow is approved, it changes the value of the isApproved field of the list item to **true**.</span></span>

## <a name="call-a-custom-web-service-from-a-workflow-and-update-sharepoint-by-using-the-sharepoint-web-proxy"></a><span data-ttu-id="95719-173">Rufen Sie einen benutzerdefinierten Webdienst mithilfe eines Workflows und aktualisieren SharePoint mithilfe des Webproxys SharePoint</span><span class="sxs-lookup"><span data-stu-id="95719-173">Call a custom web service from a workflow and update SharePoint by using the SharePoint web proxy</span></span>
<span data-ttu-id="95719-174"><a name="bk2"> </a></span><span class="sxs-lookup"><span data-stu-id="95719-174"></span></span>

<span data-ttu-id="95719-175">Im Beispiel [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) zeigt, wie ein vom Anbieter gehosteten Add-in zum Abfragen von eines Webdiensts, und übergeben Sie diese Informationen auf einer SharePoint-Liste, über den Webproxy SharePoint 2013 entwerfen.</span><span class="sxs-lookup"><span data-stu-id="95719-175">The  [Workflow.CallServiceUpdateSPViaProxy ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) sample shows how to design a provider-hosted add-in to query a web service and then pass that information to a SharePoint list via the SharePoint 2013 web proxy.</span></span>

<span data-ttu-id="95719-176">Im Beispiel wird eine Aufgabe, die nützlich ist, wenn alle Interaktionen mit einem Webdienst kapseln, sodass sie direkt vom Workflow verarbeitet werden soll.</span><span class="sxs-lookup"><span data-stu-id="95719-176">The sample shows a task that is useful when you want to encapsulate all the interactions with a web service so that they are handled directly by the workflow.</span></span> <span data-ttu-id="95719-177">Mithilfe des Webproxys vereinfacht die Remotewebsite Anwendungslogik zu aktualisieren, ohne die Workflowinstanz zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="95719-177">Using the web proxy makes it easier to update the remote web application logic without having to update the workflow instance.</span></span> <span data-ttu-id="95719-178">Wenn Sie den Proxy nicht verwenden, und Sie die Logik in Ihrer Webanwendung zu aktualisieren müssen, müssen Sie zum Entfernen der vorhandenen Workflow-Instanzen und klicken Sie dann das Add-In erneut bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="95719-178">If you're not using the proxy and you have to update the logic in your web application, you'll have to remove the existing workflow instances and then redeploy the add-in.</span></span> <span data-ttu-id="95719-179">Aus diesem Grund wird empfohlen Design, wenn Sie einen remote-Webdienst aufrufen müssen.</span><span class="sxs-lookup"><span data-stu-id="95719-179">For this reason, we recommend this design when you need to call a remote web service.</span></span> 

<span data-ttu-id="95719-180">**Hinweis**  Die [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) -Beispielseite enthält Anweisungen für die Bereitstellung von add-Ins.</span><span class="sxs-lookup"><span data-stu-id="95719-180">**Note**  The  [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) sample page contains instructions for deploying this add-in.</span></span> <span data-ttu-id="95719-181">Sie können auch bereitstellen und Testen des Add-Ins mithilfe von **F5** in Visual Studio debuggen, wenn Sie die Anweisungen in den Blogbeitrag [Debugging SharePoint 2013-Workflows mit Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)befolgen.</span><span class="sxs-lookup"><span data-stu-id="95719-181">You can also deploy and test the add-in by using **F5** debugging in Visual Studio if you follow the instructions in the blog post [Debugging SharePoint 2013 workflows using Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span></span>

<span data-ttu-id="95719-182">Im Beispiel startet einen Workflow aus einer remote-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="95719-182">The sample starts a workflow from a remote web application.</span></span> <span data-ttu-id="95719-183">Diesen Workflow übergibt Abfrageinformationen, die vom Benutzer zum Northwind OData-Webdienst übermittelt.</span><span class="sxs-lookup"><span data-stu-id="95719-183">This workflow passes query information submitted by the user to the Northwind OData web service.</span></span> <span data-ttu-id="95719-184">Die Abfrage gibt die Produktlieferanten für ein bestimmtes Land.</span><span class="sxs-lookup"><span data-stu-id="95719-184">The query returns the product suppliers for a given country.</span></span> <span data-ttu-id="95719-185">Nach die Webdienstantwort Erhalt übergibt der Workflow die Informationen aus der Antwort auf die remote-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="95719-185">After it receives the web service response, the workflow passes the information from the response to the remote web application.</span></span> <span data-ttu-id="95719-186">Klicken Sie dann die Remotewebanwendung aktualisiert eine Lieferanten Produktliste, die in der Web-Add-in das Add-in bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="95719-186">The remote web application then updates a product suppliers list that the add-in has deployed to the add-in web.</span></span>

<span data-ttu-id="95719-187">Wenn Sie die app starten, enthält die Startseite ein Dropdownmenü, aus dem Sie ein Land auswählen können, für die Sie eine Produktliste Lieferanten (Abbildung 7) erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="95719-187">When you start the app, the start page includes a drop-down menu from which you can select a country for which you want to create a product suppliers list (Figure 7).</span></span>

<span data-ttu-id="95719-188">**Abbildung 7. Workflow.CallServiceUpdateSPViaProxy Beispiel-add-in-Startseite**</span><span class="sxs-lookup"><span data-stu-id="95719-188">**Figure 7. Workflow.CallServiceUpdateSPViaProxy sample add-in start page**</span></span>

![Screenshot, der die Startseite für das Beispiel-add-in mit Update für Proxy-Workflow-app anzeigt](media/29a447b3-f17d-441f-b428-dd2a34285bb6.png)

<span data-ttu-id="95719-190">Diese Schaltfläche ruft eine Methode in der Controllers\PartSuppliersController.cs-Datei, die einen neuen Eintrag in der Liste **Webpart Lieferanten** im Web-Add-in erstellt.</span><span class="sxs-lookup"><span data-stu-id="95719-190">That button calls a method in the Controllers\PartSuppliersController.cs file that creates a new entry in the  **Part Suppliers** list on the add-in web.</span></span> <span data-ttu-id="95719-191">Die **Create** -Methode in dieser Datei ruft die **Add** -Methode, die in der Datei Services\PartSuppliersService.cs definiert ist.</span><span class="sxs-lookup"><span data-stu-id="95719-191">The **Create** method in that file calls the **Add** method that is defined in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="95719-192">Beide werden in die folgenden beiden Codebeispiele aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="95719-192">Both are shown in the following two code examples.</span></span>

<span data-ttu-id="95719-193">**Create-Methode**</span><span class="sxs-lookup"><span data-stu-id="95719-193">**Create method**</span></span>

```
public ActionResult Create(string country, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                var id = service.GetIdByCountry(country);
                if (id == null)
                {
                    id = service.Add(country);
                    TempData["Message"] = "Part Supplier Successfully Created!";
                }
                else
                    TempData["ErrorMessage"] = string.Format("Failed to Create The Part Supplier: There's already a Part Supplier who's country is {0}.", country);

                return RedirectToAction("Details", new { id = id.Value, SPHostUrl = spHostUrl });
            }
        }

```

<span data-ttu-id="95719-194">**"Add"-Methode**</span><span class="sxs-lookup"><span data-stu-id="95719-194">**Add method**</span></span>

```
public int Add(string country)
        {
            var item = list.AddItem(new ListItemCreationInformation());
            item["Country"] = country;
            item.Update();
            clientContext.ExecuteQuery();
            return item.Id;
        }

```

<span data-ttu-id="95719-195">Nachdem sie diese neuen Listenelements erstellt hat, wird das Add-in eine Schaltfläche, die den Genehmigungsworkflow (Abbildung 8) beginnt.</span><span class="sxs-lookup"><span data-stu-id="95719-195">After it creates that new list item, the add-in presents a button that starts the approval workflow (Figure 8).</span></span>

<span data-ttu-id="95719-196">**Abbildung 8. Schaltfläche Workflow starten**</span><span class="sxs-lookup"><span data-stu-id="95719-196">**Figure 8. Start Workflow button**</span></span>

![Screenshot, der die Seite Workflow starten in benutzerdefinierten Webdienstes anzeigt](media/69576609-f4c1-4160-9f82-3099e0a07d58.png)

<span data-ttu-id="95719-198">Auswahl der Schaltfläche **Workflow starten** , löst die Methode **StartWorkflow** in der Datei Controllers\PartSuppliersController.cs.</span><span class="sxs-lookup"><span data-stu-id="95719-198">Choosing the  **Start Workflow** button triggers the **StartWorkflow** method in the Controllers\PartSuppliersController.cs file.</span></span> <span data-ttu-id="95719-199">Diese Methode Pakete die Add-in-Web-URL und den Webdienst-URL (für die Remote gehosteten Webanwendung nicht für die Northwind-Webdienst) und übergibt sie an die **StartWorkflow** -Methode in der Datei Services\PartSuppliersService.cs.</span><span class="sxs-lookup"><span data-stu-id="95719-199">This method packages the add-in web URL and the web service URL (for your remotely hosted web application, not for the Northwind web service) and passes them to the **StartWorkflow** method in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="95719-200">Der Workflow wird mit der remote-Webanwendung über den Webproxy kommunizieren, und des Webproxys wird das Zugriffstoken eines Anforderungsheaders hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="95719-200">The workflow is going to communicate with the remote web application via the web proxy, and the web proxy will add the access token in a request header.</span></span> <span data-ttu-id="95719-201">Deshalb wird der Workflow eine Kontext-Token an die **StartWorkflow** -Methode in diesem Beispiel übergeben nicht.</span><span class="sxs-lookup"><span data-stu-id="95719-201">This is why the workflow doesn't pass a context token to the **StartWorkflow** method in this sample.</span></span> <span data-ttu-id="95719-202">Im folgenden Beispiel wird der Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="95719-202">The code is shown in the following example.</span></span>

```
public ActionResult StartWorkflow(int id, Guid workflowSubscriptionId, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);

            var webServiceUrl = Url.RouteUrl("DefaultApi", new { httproute = "", controller = "Data" }, Request.Url.Scheme);
            var payload = new Dictionary<string, object>
                {
                    { "appWebUrl", spContext.SPAppWebUrl.ToString() },
                    { "webServiceUrl", webServiceUrl }
                };

            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                service.StartWorkflow(workflowSubscriptionId, id, payload);
            }

            TempData["Message"] = "Workflow Successfully Started!";
            return RedirectToAction("Details", new { id = id, SPHostUrl = spHostUrl });
        }

```

<span data-ttu-id="95719-203">Die **StartWorkflow** -Methode erstellt eine Workflowinstanz und übergibt die zwei Werte (AppWebUrl AndwebServiceUrl), die in der Nutzlast Variablen für den Workflow gespeichert.</span><span class="sxs-lookup"><span data-stu-id="95719-203">The  **StartWorkflow** method creates a workflow instance and passes the two values (appWebUrl andwebServiceUrl) stored in the payload variable to the workflow.</span></span>

```
public void StartWorkflow(Guid subscriptionId, int itemId, Dictionary<string, object> payload)
        {
            var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

            var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
            var subscription = subscriptionService.GetSubscription(subscriptionId);

            var instanceService = workflowServicesManager.GetWorkflowInstanceService();
            instanceService.StartWorkflowOnListItem(subscription, itemId, payload);
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="95719-204">Nachdem der Workflow gestartet wurde und bevor es genehmigt wird, macht der Workflow eine Abfrage an den Northwind-Webdienst, um der Liste Lieferanten für das Land abzurufen, die Sie ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="95719-204">After the workflow starts, and before it is approved, the workflow makes a query to the Northwind web service to retrieve the suppliers list for the country that you selected.</span></span> <span data-ttu-id="95719-205">Dies geschieht mithilfe einer **HTTPSend** -Aktivitätsfeeds, die eine OData-Abfrage an diesen Endpunkt sendet: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`.</span><span class="sxs-lookup"><span data-stu-id="95719-205">It does this by using an  **HTTPSend** activity that sends an OData query to this endpoint: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`.</span></span> <span data-ttu-id="95719-206">Die Aktivität **HttpSend** sollte als eine **GET** -Anforderung mit einem **Accept** -Header, der angibt, JSON ohne Metadaten konfiguriert werden: ` application/json;odata=nometadata` (Abbildung 9 und 10).</span><span class="sxs-lookup"><span data-stu-id="95719-206">The  **HttpSend** activity should be configured as a **GET** request with an **Accept** header that specifies JSON with no metadata: ` application/json;odata=nometadata` (Figures 9 and 10).</span></span>

<span data-ttu-id="95719-207">**Abbildung 9. HttpSend Aktivitätskonfiguration**</span><span class="sxs-lookup"><span data-stu-id="95719-207">**Figure 9. HttpSend activity configuration**</span></span>

![Screenshot, der das Senden von HTTP-Aktivität Raster konfiguriert als eine GET-Anforderung zeigt](media/8f6c5d61-4d09-4a68-9745-3548d7353d73.png)

<span data-ttu-id="95719-209">**Abbildung 10. HttpSend Aktivität Anforderungsheader**</span><span class="sxs-lookup"><span data-stu-id="95719-209">**Figure 10. HttpSend activity request headers**</span></span>

![Screenshot, der das Raster anfordern Kopfzeilen für die HTTP-Send-Aktivität anzeigt](media/5cac4a52-cb8e-432a-bf72-6d0fa100f3fd.png)

<span data-ttu-id="95719-211">Wenn der Benutzer für das neue Listenelement Lieferanten Kanada ausgewählt haben, wird beispielsweise die Antwort JSON-Format sein, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-211">If the user selected Canada for the new supplier list item, for example, the JSON-formatted response will be as shown in the following example.</span></span>

```
{
    value: [
        {
            CompanyName: "Ma Maison"
        },
        {
            CompanyName: "Forêts d'érables"
        }
    ]
}

```

<span data-ttu-id="95719-212">Nachdem der Workflow startet, erleichtert eine **HTTP POST** -Anforderung, die die Liste Lieferanten über den Proxy der Remote gehosteten Web-Anwendung enthält.</span><span class="sxs-lookup"><span data-stu-id="95719-212">After the workflow starts, it makes a  **POST HTTP** request that contains the suppliers list to the remotely hosted web application via the proxy.</span></span> <span data-ttu-id="95719-213">Dies geschieht über eine **HttpSend** -Aktivität, die fragt die Webproxy-URL: `appWebUrl + "/_api/SP.WebProxy.invoke"`.</span><span class="sxs-lookup"><span data-stu-id="95719-213">It does this via an **HttpSend** activity that queries the web proxy URL: `appWebUrl + "/_api/SP.WebProxy.invoke"`.</span></span> <span data-ttu-id="95719-214">Anschließend übergibt der Workflow die Lieferanten-Liste, die sie aus der Northwind-Dienst durch Erstellen und übergeben eine benutzerdefinierten Dienst Nutzlast erhalten hat.</span><span class="sxs-lookup"><span data-stu-id="95719-214">The workflow then passes the supplier list that it has received from the Northwind service by building and passing a custom service payload.</span></span> <span data-ttu-id="95719-215">Die **Erstellen benutzerdefinierter Dienst Nutzlast** Aktivitätseigenschaften enthalten die Liste Lieferanten und die ID für das Land Lieferanten, wie in Abbildung 11 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-215">The  **Create Custom Service Payload** activity properties contain the supplier list and the ID for the supplier country, as shown in Figure 11.</span></span>

<span data-ttu-id="95719-216">**Abbildung 11. Erstellen Sie benutzerdefinierte Service Nutzlast Aktivität**</span><span class="sxs-lookup"><span data-stu-id="95719-216">**Figure 11. Create Custom Service Payload activity**</span></span>

![Screenshot, der Eigenschaft und Wert Raster für eine benutzerdefinierte Web Service Nutzlast Aktivität anzeigt](media/7a155105-e6d5-456a-8985-eab03d6dfad9.png)

<span data-ttu-id="95719-218">Die ** erstellen WebProxy Nutzlast ** Aktivität erstellt eine Nutzlast, die den Inhalt dieser Nutzlast an der Webproxy-URL (Abbildung 12) übergibt.</span><span class="sxs-lookup"><span data-stu-id="95719-218">The ** Create WebProxy Payload** activity constructs a payload that passes the contents of this payload to the web proxy URL (Figure 12).</span></span>

<span data-ttu-id="95719-219">**Abbildung 12. WebProxy Nutzlast Konfiguration erstellen**</span><span class="sxs-lookup"><span data-stu-id="95719-219">**Figure 12. Create WebProxy Payload configuration**</span></span>

![Screenshot, der im Dialogfeld der WebProxy-Nutzlast erstellen Aktivität anzeigt](media/0f016d2c-8e90-4d23-aea3-095ad6bf288a.png)

<span data-ttu-id="95719-221">Die Eigenschaften für diese Aktivität angeben, die Add-in-Web-URL, die Länge des Inhalts POST-Anforderung und Typ und die Akzeptanz Anforderungstyp über Anforderungsheader (Abbildung 13).</span><span class="sxs-lookup"><span data-stu-id="95719-221">The properties for this activity specify the add-in web URL, the POST request content length and type, and the request acceptance type via request headers (Figure 13).</span></span>

<span data-ttu-id="95719-222">**Abbildung 13. Eigenschaftenraster WebProxy Nutzlast Aktivität**</span><span class="sxs-lookup"><span data-stu-id="95719-222">**Figure 13. WebProxy Payload activity properties grid**</span></span>

![Screenshot, der im Eigenschaftenraster für die WebProxy-Nutzlast Aktivität anzeigt](media/0b335b2d-7bb3-43ec-ab96-019b493533a3.png)

<span data-ttu-id="95719-224">Nachdem der Workflow Nutzlast und die Anforderung erstellt wurde, übergibt die Anforderung an dem Webproxy mithilfe einer **HttpSend** -Aktivitätsfeeds, die als eine POST-Anforderung an den Webproxy-URL konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="95719-224">After the workflow has constructed the payload and the request, it passes the request to the web proxy by using an  **HttpSend** activity that's configured as a POST request to the web proxy URL.</span></span> <span data-ttu-id="95719-225">Die Anforderungsheader angeben OData JSON-Format in die **Content-Type** und **Accept** -Header (Abbildung 14).</span><span class="sxs-lookup"><span data-stu-id="95719-225">The request headers specify JSON-formatted OData in the **Content-Type** and **Accept** headers (Figure 14).</span></span>

<span data-ttu-id="95719-226">**Abbildung 14. Eigenschaften für die Aktivität HttpSend**</span><span class="sxs-lookup"><span data-stu-id="95719-226">**Figure 14. Properties for the HttpSend activity**</span></span>

![Screenshot, der im Dialogfeld anfordern Kopfzeilen für die HTTP-Send-Aktivität anzeigt](media/01ce82fb-4690-4226-874a-c4734a17d9a4.png)

<span data-ttu-id="95719-228">Die **Post** -Methode in der Datei Controllers\DataController.cs akzeptiert den Inhalt der Anforderung, die der Workflow über den Webproxy sendet.</span><span class="sxs-lookup"><span data-stu-id="95719-228">The  **Post** method inside the Controllers\DataController.cs file accepts the contents of the request that the workflow sends through the web proxy.</span></span> <span data-ttu-id="95719-229">Im vorherigen Beispiel die **Post** -Methode aufgerufen eine Methode zum Abrufen der Liste Lieferanten aus Northwind sowie eine für das Aktualisieren der entsprechenden SharePoint-Anbieter-Liste.</span><span class="sxs-lookup"><span data-stu-id="95719-229">The **Post** method in the previous sample called a method for retrieving the supplier list from Northwind as well as one for updating the corresponding SharePoint supplier list.</span></span> <span data-ttu-id="95719-230">Da Workflows in diesem Beispiel den Northwind-Dienst bereits abgefragt hat, muss diese Version der Methode nur die SharePoint-Liste aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="95719-230">Since the workflow in this sample has already queried the Northwind service, this version of the method needs only to update the SharePoint list.</span></span> <span data-ttu-id="95719-231">Anschließend übergibt auch die Add-ins Web-URL und das Zugriffstoken (die mithilfe des Webproxys übergeben wird) an die **UpdateSuppliers** -Methode in der Datei Services\PartSuppliersService.cs wie im folgenden Codebeispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-231">It also passes the add-in web URL and the access token (which is passed by the web proxy) to the **UpdateSuppliers** method in the Services\PartSuppliersService.cs file, as shown in the following code example.</span></span>

```
public void Post(UpdatePartSupplierModel model)
        {
            var request = HttpContext.Current.Request;
            var authority = request.Url.Authority;
            var spAppWebUrl = request.Headers["SPAppWebUrl"];
            var accessToken = request.Headers["X-SP-AccessToken"];

            using (var clientContext = TokenHelper.GetClientContextWithContextToken(spAppWebUrl, accessToken, authority))
            {
                var service = new PartSuppliersService(clientContext);
                service.UpdateSuppliers(model.Id, model.Suppliers.Select(s => s.CompanyName));
            }
        }

```

<span data-ttu-id="95719-232">Die **UpdateSuppliers** -Methode in der Datei PartSuppliers.cs aktualisiert TheSuppliers Feld des neu erstellten Listenelements.</span><span class="sxs-lookup"><span data-stu-id="95719-232">The  **UpdateSuppliers** method in the PartSuppliers.cs file updates theSuppliers field of the newly created list item.</span></span>

```
public void UpdateSuppliers(int id, IEnumerable<string> supplierNames)
        {
            var item = list.GetItemById(id);
            clientContext.Load(item);
            clientContext.ExecuteQuery();

            string commaSeparatedList = String.Join(",", supplierNames);
            item["Suppliers"] = commaSeparatedList;
            item.Update();
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="95719-233">Wenn der Workflow genehmigt wird, wird den Wert des Felds IsApproved des Listenelements auf "true".</span><span class="sxs-lookup"><span data-stu-id="95719-233">If the workflow is approved, it changes the value of the isApproved field of the list item to true.</span></span>

## <a name="associate-a-workflow-with-the-host-web"></a><span data-ttu-id="95719-234">Zuordnen eines Workflows mit der Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="95719-234">Associate a workflow with the host web</span></span>
<span data-ttu-id="95719-235"><a name="bk3"> </a></span><span class="sxs-lookup"><span data-stu-id="95719-235"></span></span>

<span data-ttu-id="95719-236">Das [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) -Beispiel zeigt, wie Sie einen Workflow mit der Hostwebsite bereitstellen und verknüpfen ihn mit einer Liste auf dem hostweb mithilfe der Tools in Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="95719-236">The  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) sample shows you how to deploy a workflow to the host web and associate it with a list on the host web by using tools in Visual Studio 2013.</span></span> <span data-ttu-id="95719-237">Die Anweisungen in diesem Beispiel dargestellt, wie Sie zum Erstellen eines Workflows in Visual Studio, stellen sie mit der Hostwebsite und verknüpfen ihn mit einer Liste auf dem hostweb.</span><span class="sxs-lookup"><span data-stu-id="95719-237">The instructions for this sample show you how to create a workflow in Visual Studio, deploy it to the host web, and associate it with a list on the host web.</span></span>

<span data-ttu-id="95719-238">Das Beispiel enthält einen einfachen Workflow, der alle Listen zugeordnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="95719-238">The sample contains a simple workflow that can be associated with any list.</span></span> <span data-ttu-id="95719-239">Die Anweisungen für die Bereitstellung von diesen Workflow wird gezeigt, wie die aktuellen Einschränkungen der Visual Studio-Workflow-Tools umgehen, indem Sie die app packen, öffnen sie und eine Konfigurationsdatei bearbeiten und dann neu zu verpacken, manuell vor der Bereitstellung an den host Web.</span><span class="sxs-lookup"><span data-stu-id="95719-239">The instructions for deploying this workflow show you how to work around the current limitations of the Visual Studio workflow tools by packaging the app, opening it up and editing a configuration file, and then repackaging it manually before deploying it to the host web.</span></span>

<span data-ttu-id="95719-240">Wenn Sie dieses Projekt in Visual Studio öffnen, sehen Sie sich, dass es sich um eine einfache, allgemeine Workflow handelt, der entwickelt für Funktion wird mit einer beliebigen SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="95719-240">When you open this project in Visual Studio, you'll see that it is a simple, generic workflow that is designed to work with any SharePoint list.</span></span> <span data-ttu-id="95719-241">Als die Workflowaufgabenliste bereitstellen nicht es eine beliebige Liste, mit der es verknüpft werden kann.</span><span class="sxs-lookup"><span data-stu-id="95719-241">Other than the workflow task list, it doesn't deploy any list with which it can be associated.</span></span>

<span data-ttu-id="95719-242">**Hinweis**  Die Aufgabe aus, wie in diesem Beispiel mithilfe von Visual Studio 2013 nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="95719-242">**Note**  You cannot perform the task shown in this sample by using Visual Studio 2013.</span></span> <span data-ttu-id="95719-243">Dieses Beispiel stellt eine nützliche dieses Problem zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="95719-243">This sample provides a useful workaround.</span></span> <span data-ttu-id="95719-244">Wenn der Visual Studio-Tools in der Zukunft aktualisiert werden, müssen Sie möglicherweise nicht um diese Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="95719-244">If the Visual Studio tools are updated in the future, you might not need to use this workaround.</span></span>

### <a name="deploy-a-workflow-to-the-host-web"></a><span data-ttu-id="95719-245">Bereitstellen eines Workflows mit der Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="95719-245">Deploy a workflow to the host web</span></span>

1. <span data-ttu-id="95719-246">Öffnen Sie im Projekt-Explorer das Kontextmenü (Rechtsklick) für die [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) -add-in-Projekt, und wählen Sie **Veröffentlichen**aus.</span><span class="sxs-lookup"><span data-stu-id="95719-246">Open the shortcut menu (right-click) for the  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) add-in project in the project explorer, and select **Publish**.</span></span> <span data-ttu-id="95719-247">Sie sehen ein Fenster, das eine Schaltfläche **Packen der app** enthält, wie in Abbildung 15 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="95719-247">You'll see a window that contains a  **Package the app** button, as shown in Figure 15.</span></span>
    
    <span data-ttu-id="95719-248">**Abbildung 15. Veröffentlichen des Bildschirms-add-in**</span><span class="sxs-lookup"><span data-stu-id="95719-248">**Figure 15. Publish your add-in screen**</span></span>
    
    ![Screenshot, der dem Veröffentlichen Ihrer appseite für die Veröffentlichung der Beispiel-app anzeigt](media/b003cc8b-90dc-4d49-8cb7-8b563f25f056.png)

2. <span data-ttu-id="95719-250">Wenn Sie **die app Paket**auswählen, erstellt Visual Studio eine Workflow.AssociateToHostWeb.app-Datei in die `bin\Debug\app.publish\1.0.0.0` Verzeichnis Ihrer Lösung.</span><span class="sxs-lookup"><span data-stu-id="95719-250">When you choose  **Package the app**, Visual Studio creates a Workflow.AssociateToHostWeb.app file in the  `bin\Debug\app.publish\1.0.0.0` directory of your solution.</span></span> <span data-ttu-id="95719-251">Diese Datei am Seitenrand ist ein Zip-Datei.</span><span class="sxs-lookup"><span data-stu-id="95719-251">This .app file is a type of zip file.</span></span>
    
3. <span data-ttu-id="95719-252">Extrahieren Sie den Inhalt der Datei durch ändern die Erweiterung ersten ZIP ändern.</span><span class="sxs-lookup"><span data-stu-id="95719-252">Extract the contents of the file by first changing the file extension to .zip.</span></span> 
    
4. <span data-ttu-id="95719-253">Klicken Sie in das Verzeichnis, das Sie extrahiert haben, suchen Sie und öffnen Sie die XML-Datei mit dem Namen WorkflowManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="95719-253">In the directory that you've extracted, locate and open the XML file named WorkflowManifest.xml.</span></span> <span data-ttu-id="95719-254">Die Datei ist leer.</span><span class="sxs-lookup"><span data-stu-id="95719-254">The file is empty.</span></span>
    
5. <span data-ttu-id="95719-255">Fügen Sie das folgende XML-Fragment in die Datei, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="95719-255">Add the following XML fragment to the file and then save the file.</span></span>
    
    ```XML
      <SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
        <IntegratedApp>true</IntegratedApp>
      </SPIntegratedWorkflow>
    ```

6. <span data-ttu-id="95719-256">Wählen Sie alle Dateien im Ordner "extrahierten" und öffnen Sie das Kontextmenü (Rechtsklick) für die Dateien, und wählen Sie **Senden an** > **komprimierte ZIP-Ordner**.</span><span class="sxs-lookup"><span data-stu-id="95719-256">Select all the files in the extracted folder, and then open the shortcut menu (right-click) for the files and select  **Send to** > **Compressed (zipped) folder**.</span></span>
    
7. <span data-ttu-id="95719-257">Klicken Sie auf die Zip-Datei, die Sie gerade erstellt haben, ändern Sie die Erweiterung der Datei in. app.</span><span class="sxs-lookup"><span data-stu-id="95719-257">On the zip file you just created, change the file extension to .app.</span></span> <span data-ttu-id="95719-258">Sie sollten nun ein neues Paket Workflow.AssociateToHostWeb.app verfügen, das die aktualisierte WorkflowManifest.xml-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="95719-258">You should now have a new Workflow.AssociateToHostWeb.app package that contains the updated WorkflowManifest.xml file.</span></span>
    
8. <span data-ttu-id="95719-259">Fügen Sie das Add-in Ihrer app-Katalog.</span><span class="sxs-lookup"><span data-stu-id="95719-259">Add the add-in to your app catalog.</span></span>
    
9. <span data-ttu-id="95719-260">Installieren Sie das Add-in auf der Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="95719-260">Install the add-in to your host site.</span></span>
    
10. <span data-ttu-id="95719-261">Rufen Sie eine Liste der Host-Website, und wählen Sie aus der **Liste** Bearbeitungsoption am oberen Rand der Seite von links.</span><span class="sxs-lookup"><span data-stu-id="95719-261">Go to a list on your host site and select the  **List** editing option at the top left of the page.</span></span> <span data-ttu-id="95719-262">Sie sehen, dass ein **Workflow Settings** Dropdown-Menü (Abbildung 16).</span><span class="sxs-lookup"><span data-stu-id="95719-262">You'll see a **Workflow Settings** drop-down menu (Figure 16).</span></span>
    
    <span data-ttu-id="95719-263">**Abbildung 16. Workfloweinstellungen für eine Liste**</span><span class="sxs-lookup"><span data-stu-id="95719-263">**Figure 16. Workflow settings for a list**</span></span>
    
    ![Screenshot, der workfloweinstellungen für eine Liste anzeigt](media/195d2d5b-091e-46aa-aefd-e1b883b1c33e.png)

11. <span data-ttu-id="95719-265">Wählen Sie ** Workflow ** aus dem Dropdown Menü hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="95719-265">Select ** Add a Workflow** from the drop-down menu.</span></span>
    
12. <span data-ttu-id="95719-266">Eine Auswahl aus ähnlich wie in Abbildung 17 werden nun angezeigt.</span><span class="sxs-lookup"><span data-stu-id="95719-266">You will now see a selection option similar to the image in Figure 17.</span></span> <span data-ttu-id="95719-267">Wählen Sie die **Workflow.AssociateToHostWeb** app aus der Liste der verfügbaren Optionen.</span><span class="sxs-lookup"><span data-stu-id="95719-267">Select the  **Workflow.AssociateToHostWeb** app from the list of available options.</span></span>
    
    <span data-ttu-id="95719-268">**Abbildung 17. Hinzufügen einer workfloweinstellungen**</span><span class="sxs-lookup"><span data-stu-id="95719-268">**Figure 17. Add a workflow settings**</span></span>
    
    ![Screenshot, der zeigt, hinzufügen eine Workflow-Einstellungsseite](media/08317057-4546-4ad9-b8c5-d5b33bc4350d.png)

<span data-ttu-id="95719-270">Sie haben nun den Workflow mit der Hostwebsite bereitgestellt und eine Liste auf dem hostweb zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="95719-270">You have now deployed the workflow to the host web and associated it with a list on the host web.</span></span> <span data-ttu-id="95719-271">Sie können einen Workflow manuell auslösen, oder Sie können den Workflow in Visual Studio aktualisieren, sodass auf andere Weise ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="95719-271">You can trigger a workflow manually, or you can update the workflow in Visual Studio so that it is triggered in other ways.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95719-272">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="95719-272">Additional resources</span></span>
<span data-ttu-id="95719-273"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="95719-273"></span></span>

-  [<span data-ttu-id="95719-274">Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="95719-274">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="95719-275">Debuggen von SharePoint 2013-Workflows mit Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="95719-275">Debugging SharePoint 2013 workflows using Visual Studio 2013</span></span>](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)
    
-  [<span data-ttu-id="95719-276">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="95719-276">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [<span data-ttu-id="95719-277">Workflow.CallServiceUpdateSPViaProxy</span><span class="sxs-lookup"><span data-stu-id="95719-277">Workflow.CallServiceUpdateSPViaProxy</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
    
-  [<span data-ttu-id="95719-278">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="95719-278">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [<span data-ttu-id="95719-279">Workflow.CallCustomService</span><span class="sxs-lookup"><span data-stu-id="95719-279">Workflow.CallCustomService</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
