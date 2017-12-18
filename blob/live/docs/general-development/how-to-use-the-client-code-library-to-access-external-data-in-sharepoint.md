---
title: "Verwenden der Code-Clientbibliothek für den Zugriff auf externe Daten in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c280ae92-c52b-4658-b0f3-805fb215ef8e
ms.openlocfilehash: bee624e58e0b7b85adbbdbc6097e04961001422f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-the-client-code-library-to-access-external-data-in-sharepoint"></a><span data-ttu-id="2ad7d-102">Verwenden der Code-Clientbibliothek für den Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-102">How to: Use the client code library to access external data in SharePoint</span></span>

<span data-ttu-id="2ad7d-103">In diesem Artikel erfahren Sie, wie Sie das Clientobjektmodell in SharePoint verwenden, um mit Business Connectivity Services (BCS)-Objekten in SharePoint mithilfe von browserbasierten Skripts zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-103">Learn how to use the SharePoint client object model to work with BCS objects in SharePoint using browser-based scripting.</span></span>

<span data-ttu-id="2ad7d-104">In diesem Artikel wird gezeigt, wie eine externe Liste eingerichtet wird, die Daten von einer Open Data-Protokollquelle (OData) mithilfe des Clientobjektmodells in SharePoint abruft.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-104">Learn how to use the SharePoint client object model to work with Business Connectivity Services (BCS) objects in SharePoint using browser-based scripting. This article demonstrates how to set up an external list that retrieves data from an Open Data protocol (OData) source using the client object model in SharePoint.</span></span>
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-the-sharepoint-client-object-model"></a><span data-ttu-id="2ad7d-105">Erforderliche Komponenten für den Zugriff auf externe Daten mithilfe des Clientobjektmodells SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-105">Prerequisites for accessing external data using the SharePoint client object model</span></span>
<span data-ttu-id="2ad7d-106"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="2ad7d-106"></span></span>

<span data-ttu-id="2ad7d-107">Im folgenden sind die Anforderungen für die Entwicklung von apps mithilfe des SharePoint-Clientobjektmodells:</span><span class="sxs-lookup"><span data-stu-id="2ad7d-107">The following are requirements for being able to develop apps using the SharePoint client object model:</span></span>
  
    
    

- <span data-ttu-id="2ad7d-108">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-108">SharePoint</span></span>
    
  
- <span data-ttu-id="2ad7d-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2ad7d-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="2ad7d-110">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2ad7d-110">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="2ad7d-111">Eine funktionsfähige SharePoint-Add-Ins Entwicklungsumgebung: befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="2ad7d-111">A functioning SharePoint Add-ins development environment: Follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="2ad7d-112">Zugriff auf den öffentlichen OData.org Herstellern</span><span class="sxs-lookup"><span data-stu-id="2ad7d-112">Access to the public OData.org producers</span></span>
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-the-sharepoint-client-object-model"></a><span data-ttu-id="2ad7d-113">Kernkonzepte beim Zugriff auf externe Daten mit dem SharePoint-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="2ad7d-113">Core concepts to know when accessing external data with the SharePoint client object model</span></span>

<span data-ttu-id="2ad7d-p101">Das Clientobjektmodell SharePoint bietet eine Möglichkeit zum Zugriff auf externe Daten mit clientseitigen aufrufen, die die serverseitige APIs imitieren. Funktionsweise und Verwendungsweise, finden Sie in die Artikeln in Tabelle 1.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p101">The SharePoint client object model provides a way to access external data using client-side calls that mimic the server-side APIs. To understand how it works and how to use it, see the articles in Table 1.</span></span>
  
    
    

<span data-ttu-id="2ad7d-116">**In Tabelle 1. Kernkonzepte für die Verwendung des Clientobjektmodells**</span><span class="sxs-lookup"><span data-stu-id="2ad7d-116">**Table 1. Core concepts for using the client object model**</span></span>


|<span data-ttu-id="2ad7d-117">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="2ad7d-117">**Article**</span></span>|<span data-ttu-id="2ad7d-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2ad7d-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2ad7d-119">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="2ad7d-119">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |<span data-ttu-id="2ad7d-120">Erfahren Sie, wie Sie Code führen grundlegende Vorgänge mit dem SharePoint .NET Framework-Client-Objektmodell (CSOM) schreiben.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-120">Learn how to write code to peform basic operations with the SharePoint .NET Framework client object model (CSOM).</span></span>  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-the-client-object-model"></a><span data-ttu-id="2ad7d-121">Erstellen einer SharePoint-Add-In Zugriff auf externe Daten mithilfe des Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="2ad7d-121">Create an SharePoint Add-in to access external data using the client object model</span></span>
<span data-ttu-id="2ad7d-122"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="2ad7d-122"></span></span>

<span data-ttu-id="2ad7d-123">Die folgenden Verfahren wird gezeigt, wie ein SharePoint-Add-In einrichten und Konfigurieren einer Webseite, sodass Anforderungen mithilfe der Methoden Client und Objekte zum Abrufen von Daten aus einer externen Datenquelle.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-123">The following procedures show how to set up an SharePoint Add-in and configure a webpage to make requests using client object model methods and objects to retrieve data from an external data source.</span></span>
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a><span data-ttu-id="2ad7d-124">Erstellen einer SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="2ad7d-124">To create an SharePoint Add-in</span></span>


1. <span data-ttu-id="2ad7d-125">Öffnen Sie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-125">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="2ad7d-126">Erstellen einer **App für SharePoint**-Projekt.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-126">Create an **App for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="2ad7d-p102">Geben Sie die Appeinstellungen, einschließlich app-Name die URL der Website für das Debuggen der app und wie Sie die app (automatisch gehostet, vom Anbieter gehosteten, SharePoint-Hosting) hosten möchten. Weitere Informationen zu Hostingoptionen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p102">Specify the app settings, including app name, the site URL for debugging the app, and how you want to host the app (Autohosted, Provider-hosted, SharePoint-hosted). For more information about hosting options, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="2ad7d-129">Klicken Sie auf **Fertig stellen**, um die app zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-129">Click **Finish** to create the app.</span></span>
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="2ad7d-130">Um den externen Inhaltstyp zu generieren.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-130">To generate the external content type</span></span>


1. <span data-ttu-id="2ad7d-131">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-131">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="2ad7d-p103">Geben Sie im Assistenten **OData-Quelle angeben** die URL des OData-Diensts, die Sie mit verbinden möchten. In diesem Fall verwenden Sie die Northwind-OData-Quelle auf [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem)veröffentlicht. Legen Sie die URL für den OData-Dienst auf  `http://services.odata.org/Northwind/Northwind.svc/`</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p103">In the **Specify OData Source** wizard, enter the URL of the OData service that you want to connect to. In this case, you will use the Northwind OData source published at [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Set the URL for the OData service to  `http://services.odata.org/Northwind/Northwind.svc/`</span></span>
    
    <span data-ttu-id="2ad7d-135">Geben Sie einen Namen für die Datenquelle, und klicken auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-135">Specify a name for the data source, and choose **Next**.</span></span>
    
  
3. <span data-ttu-id="2ad7d-p104">Es wird eine Liste der Entitäten, die vom OData Service verfügbar gemacht werden angezeigt. Wählen Sie die **Kunden**-Entität. Stellen Sie sicher, dass das Kontrollkästchen **für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge) Listeninstanzen erstellen** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p104">A list of entities that are exposed by the OData Service will appear. Choose the **Customers** entity. Ensure that the **Create list instances for the selected data entities (except Service Operations)** check box is selected.</span></span>
    
  
4. <span data-ttu-id="2ad7d-139">Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-139">Choose **Finish**.</span></span>
    
  

## <a name="code-example-add-scripts-and-html-to-the-defaultaspx-page"></a><span data-ttu-id="2ad7d-140">Codebeispiel: Hinzufügen von Skripts und HTML auf der Seite "default.aspx"</span><span class="sxs-lookup"><span data-stu-id="2ad7d-140">Code example: Add scripts and HTML to the Default.aspx page</span></span>
<span data-ttu-id="2ad7d-141"><a name="bkmk_AddUIelements"> </a></span><span class="sxs-lookup"><span data-stu-id="2ad7d-141"></span></span>

<span data-ttu-id="2ad7d-142">Zu diesem Zeitpunkt müssen Sie den externen Inhaltstyp und einer externen Liste, die die Daten aus der Netflix OData-Quelle angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-142">At this point, you have the external content type and an external list that displays the data from the Netflix OData source.</span></span> 
  
    
    
<span data-ttu-id="2ad7d-p105">Nächste Ziel ist es, die Seite "default.aspx" zu ändern, die Sie erstellt haben, wenn Sie Ihre app erstellt haben. Sie fügen einen Container, der die Ergebnisse der Abfrage enthalten soll, die mit Laden der Seite ausgeführt wird. Durch Ausführen des Skripts auf der Seite Load-Ereignis, stellen Sie sicher, dass das Skript ausgeführt wird, jedes Mal, wenn die Seite wird durchsucht und die resultierende Client Objektmodellaufrufe werden versucht, den Netflix-OData-Quelle Datensätze auf der Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p105">The next objective is to modify the default.aspx page that you created when you created your app. You add a container that will hold the results of the query that is executed with the page loads. By executing the scripts on the page load event, you ensure that the script will be executed every time the page is browsed, and the resulting client object model calls will be made to the Netflix OData source to add records to the page.</span></span> 
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a><span data-ttu-id="2ad7d-146">So fügen Sie dem Container zur Seite Default.aspx hinzu</span><span class="sxs-lookup"><span data-stu-id="2ad7d-146">To add the container to the Default.aspx page</span></span>


1. <span data-ttu-id="2ad7d-147">Öffnen Sie im **Projektmappen-Explorer** die Seite Default.aspx in der **Pages**-Modul abgelegte.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-147">In **Solution Explorer**, open the Default.aspx page located in the **Pages** module.</span></span>
    
  
2. <span data-ttu-id="2ad7d-148">Fügen Sie das folgende **div** -Element auf der Seite hinzu:</span><span class="sxs-lookup"><span data-stu-id="2ad7d-148">Add the following **div** element to the page:</span></span>
    
```HTML
  
<div id="displayDiv"></div>
```

3. <span data-ttu-id="2ad7d-149">Speichern Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-149">Save the page.</span></span>
    
  
<span data-ttu-id="2ad7d-150">Zum Schluss fügen Sie Code auf die Datei App.js, die beim Laden der Seite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-150">Finally, you add code to the App.js file that executes when the page loads.</span></span>
  
    
    

### <a name="to-modify-the-appjs-file-to-make-client-object-model-calls"></a><span data-ttu-id="2ad7d-151">So ändern Sie die Datei App.js, sodass Client ruft-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="2ad7d-151">To modify the App.js file to make client object model calls</span></span>


1. <span data-ttu-id="2ad7d-152">Öffnen Sie die Datei App.js in das Modul Skripts Ihrer SharePoint-Projekts.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-152">Open the App.js file in the Scripts module of your SharePoint project.</span></span>
    
  
2. <span data-ttu-id="2ad7d-153">Fügen Sie den folgenden Code am Ende der Datei.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-153">Paste the following code at the end of the file.</span></span>
    
```
  $(document).ready(function () {

    // Namespace
    window.AppLevelECT = window.AppLevelECT || {};

    // Constructor
    AppLevelECT.Grid = function (hostElement, surlWeb) {
        this.hostElement = hostElement;
        if (surlWeb.length > 0 &amp;&amp; surlWeb.substring(surlWeb.length - 1, surlWeb.length) != "/")
            surlWeb += "/";
        this.surlWeb = surlWeb;
    }

    // Prototype
    AppLevelECT.Grid.prototype = {

        init: function () {

            $.ajax({
                url: this.surlWeb + "_api/lists/getbytitle('Customer')/items?$select=BdcIdentity,CustomerID,ContactName",
                headers: {
                    "accept": "application/json",
                    "X-RequestDigest": $("#__REQUESTDIGEST").val()
                },
                success: this.showItems
            });
        },

        showItems: function (data) {
            var items = [];

            items.push("<table>");
            items.push('<tr><td>Customer ID</td><td>Customer Name</td></tr>');

            $.each(data.d.results, function (key, val) {
                items.push('<tr id="' + val.BdcIdentity + '"><td>' +
                    val.CustomerID + '</td><td>' +
                    val.ContactName + '</td></tr>');
            });

            items.push("</table>");

            $("#displayDiv").html(items.join(''));
        }
    }

    ExecuteOrDelayUntilScriptLoaded(getCustomers, "sp.js");
});

function getCustomers() {
    var grid = new AppLevelECT.Grid($("#displayDiv"), _spPageContextInfo.webServerRelativeUrl);
    grid.init();
}
```

<span data-ttu-id="2ad7d-p106">Drücken Sie F5, um die app in SharePoint bereitstellen. Wechseln Sie zur Seite Default.aspx in der app, und eine Liste der Kunden wird auf der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2ad7d-p106">Press F5 to deploy the app to SharePoint. Browse to the Default.aspx page in the app, and a list of customers appears on the page.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="2ad7d-156">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2ad7d-156">See also</span></span>
<span data-ttu-id="2ad7d-157"><a name="bkmk_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2ad7d-157"></span></span>


-  [<span data-ttu-id="2ad7d-158">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-158">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ad7d-159">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-159">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ad7d-160">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="2ad7d-160">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="2ad7d-161">Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-161">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="2ad7d-162">BCS-Client-Objektmodellreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-162">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="2ad7d-163">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ad7d-163">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2ad7d-164">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="2ad7d-164">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  

