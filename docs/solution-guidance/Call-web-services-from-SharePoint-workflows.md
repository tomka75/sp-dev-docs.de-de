---
title: Aufrufen von Webdiensten in SharePoint-workflows
ms.date: 11/03/2017
ms.openlocfilehash: d3ee350dde2f5c9978c6d875518f57e828f35dbc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="call-web-services-from-sharepoint-workflows"></a>Aufrufen von Webdiensten in SharePoint-workflows

Bereitstellen eines SharePoint 2013-Workflows mit der Hostwebsite über ein Add-In für SharePoint und Aufrufen von Webdiensten in SharePoint-Workflows.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Die SharePoint 2013-Add-in-Objektmodell können zum Erstellen und Bereitstellen von Workflows, die auf dem Web-Add-in oder der Hostwebsite ausgeführt. Diese Workflows können mit den Remote gehosteten Teile der vom Anbieter gehosteten-add-ins interagieren. Workflows können auch remote-Webdienste aufrufen, die wichtige Unternehmensdaten in einem der folgenden beiden Methoden enthalten: 

- Einfügen, indem Sie die Abfrage von Informationen an den Remote gehosteten Teil des Add-Ins. Die Remotewebanwendung klicken Sie dann den Webdienst aufgerufen und übergibt die Informationen mit SharePoint.
    
- Durch Abfragen des Webdiensts mithilfe des Webproxys SharePoint 2013. Der Workflow übergibt die Ergebnisse der Abfrage an den Remote gehosteten Teil das Add-in, das dann die Informationen an SharePoint übergibt.
    
Die vom Webdienst abgerufene Daten gespeichert werden kann in SharePoint-Listen. In diesem Artikel werden drei Codebeispiele, die zeigen, wie Sie Aufrufen von Webdiensten aus Workflows, wie in der folgenden Tabelle aufgeführt. In den ersten beiden Beispielen werden die Workflows und die Listen im Web-Add-in bereitgestellt, wenn das Add-in installiert. Das letzte Beispiel stellt die grundlegende Verwaltungsshell von einem Workflow und Anleitungen zur Verwendung in der Hostwebsite bereitzustellen, und ordnen Sie ihm eine Liste auf dem hostweb. 

**Workflow-Aufgaben und zugehörige Beispiele (engl.)**

|**Aufgabe**|**Beispiel**|
|:-----|:-----|
|Aufrufen von benutzerdefinierten Webdiensten mithilfe eines Workflows|[Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)|
|Rufen Sie einen benutzerdefinierten Webdienst mithilfe eines Workflows und aktualisieren SharePoint mithilfe des Webproxys SharePoint|[Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)|
|Zuordnen eines Workflows mit der Hostwebsite|[Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)|

## <a name="call-custom-web-services-from-a-workflow"></a>Aufrufen von benutzerdefinierten Webdiensten mithilfe eines Workflows
<a name="bk1"> </a>

Das [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) -Beispiel zeigt, wie Sie einen Workflow zu erstellen, der einen benutzerdefinierten Webdienst aufruft, mit der SharePoint-Listendaten aktualisiert. Es auch zeigt, wie ein vom Anbieter gehosteten-Add-in zu entwerfen, sodass mithilfe der Remote gehosteten Webanwendung, die bereitgestellt wird mit der Add-in einem Webdienst abgefragt. In diesem Beispiel ist nützlich, wenn Sie alle Interaktionen mit dem Webdienst vom Remote gehosteten Teil des vom Anbieter gehosteten Add-in behandelt werden sollen.

Das Beispiel funktioniert durch Starten eines Workflows von einer remote-Webanwendung. Diesen Workflow übergibt Abfrageinformationen, die vom Benutzer an der remote-Webanwendung, der dann diese Informationen zum Erstellen einer Abfrage an den Northwind OData-Webdienst übermittelt. Die Abfrage gibt die Produktlieferanten für ein bestimmtes Land. Nachdem sie diese Informationen empfangen hat, aktualisiert die Remotewebanwendung eine Lieferanten Produktliste, die in der Web-Add-in das Add-in bereitgestellt wurde.

**Hinweis**  Die [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) -Beispielseite enthält Anweisungen für die Bereitstellung von add-Ins. Sie können auch bereitstellen und Testen mit F5 in Visual Studio debuggen, wenn Sie die Anweisungen in den Blogbeitrag [Debugging SharePoint 2013-Workflows mit Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)befolgen.

Diese app-Startseite enthält ein Dropdownmenü, aus dem Sie ein Land auswählen können, für die Sie eine Produktliste Lieferanten (Abbildung 1) erstellen möchten. 

**Abbildung 1. Workflow.CallCustomService Beispiel-add-in-Startseite**

![Screenshot, der die Startseite der Beispiel-app anzeigt](media/b2def940-9c82-458b-8f57-7ea92548ea71.png)

Die Schaltfläche **Erstellen** , auf dem Bildschirm Ruft eine **Create** -Methode in der Controllers\PartSuppliersController.cs-Datei, die einen neuen Eintrag in der Liste Webpart Lieferanten im Web-Add-in erstellt. Die **Create** -Methode ruft dann die **Add** -Methode, die in der Datei Services\PartSuppliersService.cs definiert ist. Die Abfolge ist in die folgenden beiden Codebeispiele dargestellt.

**Create-Methode**

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

**"Add"-Methode**

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

Nach dem Erstellen dieser neuen Listenelements an, zeigt das Add-in eine Schaltfläche, die den Genehmigungsworkflow gestartet wird wie in Abbildung 2 dargestellt.

**Abbildung 2. Workflow-Schaltfläche "Start" in der Beispielapp**

![Screenshot, der die Seite Workflow starten in der Beispielapp anzeigt](media/1d5fc6a1-79fe-4767-b8d8-905a10354565.png)

Auswahl der Schaltfläche **Workflow starten** , löst die **StartWorkflow** -Methode, die in der Datei Controllers\PartSuppliersController.cs definiert ist. Diese Methode Pakete die Add-in-Web-URL, die Webdienst-URL (für die Remote gehosteten Webanwendung nicht für die Northwind-Webdienst) und die Kontext-token-Werte und übergibt sie an die **StartWorkflow** -Methode. Die **PartSuppliersService** -Methode wird das Kontext-Token für die Interaktion mit SharePoint benötigen.

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

Die **StartWorkflow** -Methode erstellt eine Workflowinstanz dann und übergibt die drei Werte (AppWebUrl, WebServiceUrl, ContextToken) in der Nutzlast Variablen für den Workflow gespeichert.

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

Nachdem der Workflow startet, wird eine **HTTP POST-** Anforderung an die Webanwendung Remote gehosteten erleichtert. Diese Anforderung weist die Webanwendung so aktualisieren Sie die Liste Lieferanten mit Lieferanten für das Land, die der Benutzer gerade hinzugefügt wurde. Die Controllers\DataController.cs-Datei enthält eine **POST** -Methode, die den Inhalt dieser Anforderung empfängt.

```
public void Post([FromBody]string country)
        {
            var supplierNames = GetSupplierNames(country);
            UpdateSuppliers(country, supplierNames);
        }

```

Die **GetSupplierNames** -Methode (in der Datei Controllers\DataController.cs) erstellt und führt eine LINQ-Abfrage an den Northwind OData-Webdienst für alle Lieferanten ausgewählte Land zugeordnet. Die **UpdateSuppliers** -Methode aktualisiert TheSuppliers dar, der dem neu hinzugefügten Listenelement, klicken Sie dann, wie in den folgenden beiden Codebeispiele dargestellt.

**Abfrage Nordwind (engl.)**

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

**Lieferanten Updateliste**

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

Wenn Sie die Entwurfsansicht der workflow.xaml-Datei in das Verzeichnis Lieferanten Genehmigen des app-Projekts betrachten, sehen Sie (indem Sie auf die Registerkarte **Argumente** am unteren linken Ecke des der Entwurfsansicht), dass der Workflow die drei Werte in Thepayload-Variablen gespeichert sind wird es als Workflow Argumente (Abbildung 3) übergeben.

**Abbildung 3. Argumente für den Workflow Nutzlast**

![Screenshot, der auf dem Bildschirm für die Eingabe der Nutzlast Argumente an den Workflow übergeben werden](media/4bd5cbde-d505-4d35-9fe6-50ea79f63263.png)

Die **HttpSend** Aktivität tritt vor dem Workflow Genehmigung. Diese Aktivität sendet die Abfrage **POST** an Ihre remote-Webanwendung, die den Anruf an den Webdienst Northwind ausgelöst wird, und klicken Sie dann das Listenelement aktualisieren (mit der Liste Lieferanten). Diese Aktivität ist so konfiguriert, dass sendet die Anforderung an ThewebServiceUrl-Wert, der als eine Workflow-Argument (Abbildung 4) übergeben wurde.

**Abbildung 4. HttpSend Aktivität Uri-Wert**

![Screenshot, der im Textfeld zum Eingeben der Webdienst-URL senden über HTTP anzeigt](media/7f8c1f8c-b045-4b35-9435-5fcf1be12835.png)

Die **POST** -Anforderung übergibt auch den Wert für das Land, das in der Listenelement gespeichert ist, der Workflow (Abbildung 5) arbeitet.

**Abbildung 5. Eigenschaftenraster für die Aktivität HttpSend**

![Screenshot, der das Eigenschaftenraster für das Senden von HTTP-Aktivität anzeigt](media/7a241a29-5b3b-4c82-b86b-67159685dd02.png)

Der Workflow sendet die AppWebUrl AndcontextToken-Werte für die Webanwendung über die Anforderungsheader (Abbildung 6). Der Header festlegen auch die Inhaltstypen für das Senden und Anforderungen akzeptiert.

**Abbildung 6. Anforderungsheader für die Aktivität HttpSend**

![Screenshot, der das Raster für das Hinzufügen von HTTP senden Anforderungsheader Aktivität anzeigt](media/1c019be6-f509-4ff3-83af-e1ecb1f7fbe5.png)

Wenn der Workflow genehmigt wird, wird den Wert des Felds IsApproved des Listenelements auf **true**.

## <a name="call-a-custom-web-service-from-a-workflow-and-update-sharepoint-by-using-the-sharepoint-web-proxy"></a>Rufen Sie einen benutzerdefinierten Webdienst mithilfe eines Workflows und aktualisieren SharePoint mithilfe des Webproxys SharePoint
<a name="bk2"> </a>

Im Beispiel [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) zeigt, wie ein vom Anbieter gehosteten Add-in zum Abfragen von eines Webdiensts, und übergeben Sie diese Informationen auf einer SharePoint-Liste, über den Webproxy SharePoint 2013 entwerfen.

Im Beispiel wird eine Aufgabe, die nützlich ist, wenn alle Interaktionen mit einem Webdienst kapseln, sodass sie direkt vom Workflow verarbeitet werden soll. Mithilfe des Webproxys vereinfacht die Remotewebsite Anwendungslogik zu aktualisieren, ohne die Workflowinstanz zu aktualisieren. Wenn Sie den Proxy nicht verwenden, und Sie die Logik in Ihrer Webanwendung zu aktualisieren müssen, müssen Sie zum Entfernen der vorhandenen Workflow-Instanzen und klicken Sie dann das Add-In erneut bereitstellen. Aus diesem Grund wird empfohlen Design, wenn Sie einen remote-Webdienst aufrufen müssen. 

**Hinweis**  Die [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) -Beispielseite enthält Anweisungen für die Bereitstellung von add-Ins. Sie können auch bereitstellen und Testen des Add-Ins mithilfe von **F5** in Visual Studio debuggen, wenn Sie die Anweisungen in den Blogbeitrag [Debugging SharePoint 2013-Workflows mit Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)befolgen.

Im Beispiel startet einen Workflow aus einer remote-Webanwendung. Diesen Workflow übergibt Abfrageinformationen, die vom Benutzer zum Northwind OData-Webdienst übermittelt. Die Abfrage gibt die Produktlieferanten für ein bestimmtes Land. Nach die Webdienstantwort Erhalt übergibt der Workflow die Informationen aus der Antwort auf die remote-Webanwendung. Klicken Sie dann die Remotewebanwendung aktualisiert eine Lieferanten Produktliste, die in der Web-Add-in das Add-in bereitgestellt wurde.

Wenn Sie die app starten, enthält die Startseite ein Dropdownmenü, aus dem Sie ein Land auswählen können, für die Sie eine Produktliste Lieferanten (Abbildung 7) erstellen möchten.

**Abbildung 7. Workflow.CallServiceUpdateSPViaProxy Beispiel-add-in-Startseite**

![Screenshot, der die Startseite für das Beispiel-add-in mit Update für Proxy-Workflow-app anzeigt](media/29a447b3-f17d-441f-b428-dd2a34285bb6.png)

Diese Schaltfläche ruft eine Methode in der Controllers\PartSuppliersController.cs-Datei, die einen neuen Eintrag in der Liste **Webpart Lieferanten** im Web-Add-in erstellt. Die **Create** -Methode in dieser Datei ruft die **Add** -Methode, die in der Datei Services\PartSuppliersService.cs definiert ist. Beide werden in die folgenden beiden Codebeispiele aufgeführt.

**Create-Methode**

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

**"Add"-Methode**

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

Nachdem sie diese neuen Listenelements erstellt hat, wird das Add-in eine Schaltfläche, die den Genehmigungsworkflow (Abbildung 8) beginnt.

**Abbildung 8. Schaltfläche Workflow starten**

![Screenshot, der die Seite Workflow starten in benutzerdefinierten Webdienstes anzeigt](media/69576609-f4c1-4160-9f82-3099e0a07d58.png)

Auswahl der Schaltfläche **Workflow starten** , löst die Methode **StartWorkflow** in der Datei Controllers\PartSuppliersController.cs. Diese Methode Pakete die Add-in-Web-URL und den Webdienst-URL (für die Remote gehosteten Webanwendung nicht für die Northwind-Webdienst) und übergibt sie an die **StartWorkflow** -Methode in der Datei Services\PartSuppliersService.cs. Der Workflow wird mit der remote-Webanwendung über den Webproxy kommunizieren, und des Webproxys wird das Zugriffstoken eines Anforderungsheaders hinzufügen. Deshalb wird der Workflow eine Kontext-Token an die **StartWorkflow** -Methode in diesem Beispiel übergeben nicht. Im folgenden Beispiel wird der Code gezeigt.

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

Die **StartWorkflow** -Methode erstellt eine Workflowinstanz und übergibt die zwei Werte (AppWebUrl AndwebServiceUrl), die in der Nutzlast Variablen für den Workflow gespeichert.

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

Nachdem der Workflow gestartet wurde und bevor es genehmigt wird, macht der Workflow eine Abfrage an den Northwind-Webdienst, um der Liste Lieferanten für das Land abzurufen, die Sie ausgewählt haben. Dies geschieht mithilfe einer **HTTPSend** -Aktivitätsfeeds, die eine OData-Abfrage an diesen Endpunkt sendet: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`. Die Aktivität **HttpSend** sollte als eine **GET** -Anforderung mit einem **Accept** -Header, der angibt, JSON ohne Metadaten konfiguriert werden: ` application/json;odata=nometadata` (Abbildung 9 und 10).

**Abbildung 9. HttpSend Aktivitätskonfiguration**

![Screenshot, der das Senden von HTTP-Aktivität Raster konfiguriert als eine GET-Anforderung zeigt](media/8f6c5d61-4d09-4a68-9745-3548d7353d73.png)

**Abbildung 10. HttpSend Aktivität Anforderungsheader**

![Screenshot, der das Raster anfordern Kopfzeilen für die HTTP-Send-Aktivität anzeigt](media/5cac4a52-cb8e-432a-bf72-6d0fa100f3fd.png)

Wenn der Benutzer für das neue Listenelement Lieferanten Kanada ausgewählt haben, wird beispielsweise die Antwort JSON-Format sein, wie im folgenden Beispiel dargestellt.

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

Nachdem der Workflow startet, erleichtert eine **HTTP POST** -Anforderung, die die Liste Lieferanten über den Proxy der Remote gehosteten Web-Anwendung enthält. Dies geschieht über eine **HttpSend** -Aktivität, die fragt die Webproxy-URL: `appWebUrl + "/_api/SP.WebProxy.invoke"`. Anschließend übergibt der Workflow die Lieferanten-Liste, die sie aus der Northwind-Dienst durch Erstellen und übergeben eine benutzerdefinierten Dienst Nutzlast erhalten hat. Die **Erstellen benutzerdefinierter Dienst Nutzlast** Aktivitätseigenschaften enthalten die Liste Lieferanten und die ID für das Land Lieferanten, wie in Abbildung 11 dargestellt.

**Abbildung 11. Erstellen Sie benutzerdefinierte Service Nutzlast Aktivität**

![Screenshot, der Eigenschaft und Wert Raster für eine benutzerdefinierte Web Service Nutzlast Aktivität anzeigt](media/7a155105-e6d5-456a-8985-eab03d6dfad9.png)

Die ** erstellen WebProxy Nutzlast ** Aktivität erstellt eine Nutzlast, die den Inhalt dieser Nutzlast an der Webproxy-URL (Abbildung 12) übergibt.

**Abbildung 12. WebProxy Nutzlast Konfiguration erstellen**

![Screenshot, der im Dialogfeld der WebProxy-Nutzlast erstellen Aktivität anzeigt](media/0f016d2c-8e90-4d23-aea3-095ad6bf288a.png)

Die Eigenschaften für diese Aktivität angeben, die Add-in-Web-URL, die Länge des Inhalts POST-Anforderung und Typ und die Akzeptanz Anforderungstyp über Anforderungsheader (Abbildung 13).

**Abbildung 13. Eigenschaftenraster WebProxy Nutzlast Aktivität**

![Screenshot, der im Eigenschaftenraster für die WebProxy-Nutzlast Aktivität anzeigt](media/0b335b2d-7bb3-43ec-ab96-019b493533a3.png)

Nachdem der Workflow Nutzlast und die Anforderung erstellt wurde, übergibt die Anforderung an dem Webproxy mithilfe einer **HttpSend** -Aktivitätsfeeds, die als eine POST-Anforderung an den Webproxy-URL konfiguriert ist. Die Anforderungsheader angeben OData JSON-Format in die **Content-Type** und **Accept** -Header (Abbildung 14).

**Abbildung 14. Eigenschaften für die Aktivität HttpSend**

![Screenshot, der im Dialogfeld anfordern Kopfzeilen für die HTTP-Send-Aktivität anzeigt](media/01ce82fb-4690-4226-874a-c4734a17d9a4.png)

Die **Post** -Methode in der Datei Controllers\DataController.cs akzeptiert den Inhalt der Anforderung, die der Workflow über den Webproxy sendet. Im vorherigen Beispiel die **Post** -Methode aufgerufen eine Methode zum Abrufen der Liste Lieferanten aus Northwind sowie eine für das Aktualisieren der entsprechenden SharePoint-Anbieter-Liste. Da Workflows in diesem Beispiel den Northwind-Dienst bereits abgefragt hat, muss diese Version der Methode nur die SharePoint-Liste aktualisieren. Anschließend übergibt auch die Add-ins Web-URL und das Zugriffstoken (die mithilfe des Webproxys übergeben wird) an die **UpdateSuppliers** -Methode in der Datei Services\PartSuppliersService.cs wie im folgenden Codebeispiel dargestellt.

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

Die **UpdateSuppliers** -Methode in der Datei PartSuppliers.cs aktualisiert TheSuppliers Feld des neu erstellten Listenelements.

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

Wenn der Workflow genehmigt wird, wird den Wert des Felds IsApproved des Listenelements auf "true".

## <a name="associate-a-workflow-with-the-host-web"></a>Zuordnen eines Workflows mit der Hostwebsite
<a name="bk3"> </a>

Das [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) -Beispiel zeigt, wie Sie einen Workflow mit der Hostwebsite bereitstellen und verknüpfen ihn mit einer Liste auf dem hostweb mithilfe der Tools in Visual Studio 2013. Die Anweisungen in diesem Beispiel dargestellt, wie Sie zum Erstellen eines Workflows in Visual Studio, stellen sie mit der Hostwebsite und verknüpfen ihn mit einer Liste auf dem hostweb.

Das Beispiel enthält einen einfachen Workflow, der alle Listen zugeordnet werden kann. Die Anweisungen für die Bereitstellung von diesen Workflow wird gezeigt, wie die aktuellen Einschränkungen der Visual Studio-Workflow-Tools umgehen, indem Sie die app packen, öffnen sie und eine Konfigurationsdatei bearbeiten und dann neu zu verpacken, manuell vor der Bereitstellung an den host Web.

Wenn Sie dieses Projekt in Visual Studio öffnen, sehen Sie sich, dass es sich um eine einfache, allgemeine Workflow handelt, der entwickelt für Funktion wird mit einer beliebigen SharePoint-Liste. Als die Workflowaufgabenliste bereitstellen nicht es eine beliebige Liste, mit der es verknüpft werden kann.

**Hinweis**  Die Aufgabe aus, wie in diesem Beispiel mithilfe von Visual Studio 2013 nicht möglich. Dieses Beispiel stellt eine nützliche dieses Problem zu umgehen. Wenn der Visual Studio-Tools in der Zukunft aktualisiert werden, müssen Sie möglicherweise nicht um diese Methode verwenden.

### <a name="deploy-a-workflow-to-the-host-web"></a>Bereitstellen eines Workflows mit der Hostwebsite

1. Öffnen Sie im Projekt-Explorer das Kontextmenü (Rechtsklick) für die [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) -add-in-Projekt, und wählen Sie **Veröffentlichen**aus. Sie sehen ein Fenster, das eine Schaltfläche **Packen der app** enthält, wie in Abbildung 15 dargestellt.
    
    **Abbildung 15. Veröffentlichen des Bildschirms-add-in**
    
    ![Screenshot, der dem Veröffentlichen Ihrer appseite für die Veröffentlichung der Beispiel-app anzeigt](media/b003cc8b-90dc-4d49-8cb7-8b563f25f056.png)

2. Wenn Sie **die app Paket**auswählen, erstellt Visual Studio eine Workflow.AssociateToHostWeb.app-Datei in die `bin\Debug\app.publish\1.0.0.0` Verzeichnis Ihrer Lösung. Diese Datei am Seitenrand ist ein Zip-Datei.
    
3. Extrahieren Sie den Inhalt der Datei durch ändern die Erweiterung ersten ZIP ändern. 
    
4. Klicken Sie in das Verzeichnis, das Sie extrahiert haben, suchen Sie und öffnen Sie die XML-Datei mit dem Namen WorkflowManifest.xml. Die Datei ist leer.
    
5. Fügen Sie das folgende XML-Fragment in die Datei, und speichern Sie die Datei.
    
    ```XML
      <SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
        <IntegratedApp>true</IntegratedApp>
      </SPIntegratedWorkflow>
    ```

6. Wählen Sie alle Dateien im Ordner "extrahierten" und öffnen Sie das Kontextmenü (Rechtsklick) für die Dateien, und wählen Sie **Senden an** > **komprimierte ZIP-Ordner**.
    
7. Klicken Sie auf die Zip-Datei, die Sie gerade erstellt haben, ändern Sie die Erweiterung der Datei in. app. Sie sollten nun ein neues Paket Workflow.AssociateToHostWeb.app verfügen, das die aktualisierte WorkflowManifest.xml-Datei enthält.
    
8. Fügen Sie das Add-in Ihrer app-Katalog.
    
9. Installieren Sie das Add-in auf der Hostwebsite.
    
10. Rufen Sie eine Liste der Host-Website, und wählen Sie aus der **Liste** Bearbeitungsoption am oberen Rand der Seite von links. Sie sehen, dass ein **Workflow Settings** Dropdown-Menü (Abbildung 16).
    
    **Abbildung 16. Workfloweinstellungen für eine Liste**
    
    ![Screenshot, der workfloweinstellungen für eine Liste anzeigt](media/195d2d5b-091e-46aa-aefd-e1b883b1c33e.png)

11. Wählen Sie ** Workflow ** aus dem Dropdown Menü hinzufügen.
    
12. Eine Auswahl aus ähnlich wie in Abbildung 17 werden nun angezeigt. Wählen Sie die **Workflow.AssociateToHostWeb** app aus der Liste der verfügbaren Optionen.
    
    **Abbildung 17. Hinzufügen einer workfloweinstellungen**
    
    ![Screenshot, der zeigt, hinzufügen eine Workflow-Einstellungsseite](media/08317057-4546-4ad9-b8c5-d5b33bc4350d.png)

Sie haben nun den Workflow mit der Hostwebsite bereitgestellt und eine Liste auf dem hostweb zugeordnet. Sie können einen Workflow manuell auslösen, oder Sie können den Workflow in Visual Studio aktualisieren, sodass auf andere Weise ausgelöst wird.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Debuggen von SharePoint 2013-Workflows mit Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)
    
-  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
    
-  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
