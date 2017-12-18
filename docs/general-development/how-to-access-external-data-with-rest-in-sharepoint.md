---
title: Zugriff auf externe Daten mit REST in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0663cc8c-a736-434d-9858-6ce12ce7f748
ms.openlocfilehash: 3b51aeb585db992208117c2ddcc014425c87822c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="access-external-data-by-using-rest-in-sharepoint"></a><span data-ttu-id="92e6a-102">Zugriff auf externe Daten mit REST in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92e6a-102">Access external data by using REST in SharePoint</span></span>

<span data-ttu-id="92e6a-p101">Erfahren Sie, wie externe Daten mithilfe von Representational State Transfer (REST) URLs für Business Connectivity Services (BCS)SharePoint zugreifen. In diesem Artikel veranschaulicht, wie eine externe Liste einrichten, die Daten aus einer Open Data Protocol (OData) Datenquelle abruft.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p101">Learn how to access external data from SharePoint by using Representational State Transfer (REST) URLs for Business Connectivity Services (BCS). This article shows how to set up an external list that retrieves data from an Open Data protocol (OData) source.</span></span>
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-rest"></a><span data-ttu-id="92e6a-105">Erforderliche Komponenten für den Zugriff auf externe Daten mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="92e6a-105">Prerequisites for accessing external data using REST</span></span>
<span data-ttu-id="92e6a-106"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="92e6a-106"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="92e6a-107">Zugriff auf externe Daten aus SharePoint unter Verwendung von REST, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="92e6a-107">To access external data from SharePoint by using REST, you need the following:</span></span>
  
    
    

- <span data-ttu-id="92e6a-108">SharePoint</span><span class="sxs-lookup"><span data-stu-id="92e6a-108">SharePoint</span></span>
    
  
- <span data-ttu-id="92e6a-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="92e6a-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="92e6a-110">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="92e6a-110">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="92e6a-111">Eine funktionsfähige SharePoint-Add-Ins Entwicklungsumgebung: befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="92e6a-111">A functioning SharePoint Add-ins development environment: Follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="92e6a-112">Zugriff auf den öffentlichen OData.org Herstellern</span><span class="sxs-lookup"><span data-stu-id="92e6a-112">Access to the public OData.org producers</span></span>
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-rest"></a><span data-ttu-id="92e6a-113">Kernkonzepte beim Zugriff auf externe Daten mit REST</span><span class="sxs-lookup"><span data-stu-id="92e6a-113">Core concepts to know when accessing external data with REST</span></span>

<span data-ttu-id="92e6a-p102">Der REST-Dienst SharePoint bietet eine Möglichkeit Zugriff auf externe Daten mithilfe einer speziell gestalteten URL. Funktionsweise und Ihre Verwendung finden Sie unter den folgenden Artikeln.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p102">The SharePoint REST service provides a way to access external data using a specially constructed URL. To understand how it works and how to use it, see the following articles.</span></span>
  
    
    

<span data-ttu-id="92e6a-116">**In Tabelle 1. Kernkonzepte für REST in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="92e6a-116">**Table 1. Core concepts for REST in SharePoint**</span></span>


|<span data-ttu-id="92e6a-117">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="92e6a-117">**Article title**</span></span>|<span data-ttu-id="92e6a-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="92e6a-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="92e6a-119">Programmieren mit dem SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="92e6a-119">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx) <br/> |<span data-ttu-id="92e6a-120">Erfahren Sie, wie den SharePoint-REST-Dienst verwenden, der eine Programmierschnittstelle vergleichbar mit der vorhandenen SharePoint-Clientobjektmodell REST bietet.</span><span class="sxs-lookup"><span data-stu-id="92e6a-120">Learn how to use the SharePoint REST service, which provides a REST programming interface comparable to the existing client object model.</span></span>  <br/> |
| [<span data-ttu-id="92e6a-121">Erste Schritte mit den SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="92e6a-121">Get to know the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) <br/> |<span data-ttu-id="92e6a-122">Hier erhalten Sie grundlegende Informationen zum Verwenden des SharePoint REST-Diensts zum Zugreifen auf und Aktualisieren von SharePoint-Daten mithilfe der REST- und OData-Webprotokollstandards.</span><span class="sxs-lookup"><span data-stu-id="92e6a-122">Get the basics of using the SharePoint REST service to access and update SharePoint data, using the REST and OData web protocol standards.</span></span>  <br/> |
| [<span data-ttu-id="92e6a-123">Verwenden des SharePoint REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="92e6a-123">Using the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx) <br/> |<span data-ttu-id="92e6a-124">Erfahren Sie, wie die SharePoint-Datenstruktur dargestellt in der REST-Dienst zu navigieren, führen Sie allgemeine CRUD (erstellen, lesen, aktualisieren und löschen)-Vorgänge zu SharePoint-Elemente über den REST-Dienst Synchronisieren von SharePoint-Elemente anwendungsübergreifend und Element Parallelität steuern.</span><span class="sxs-lookup"><span data-stu-id="92e6a-124">Learn how to navigate the SharePoint data structure as it is represented in the REST service, perform common CRUD (create, read, update, and delete) operations on SharePoint items via the REST service, synchronize SharePoint items across applications, and control item concurrency.</span></span>  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-rest"></a><span data-ttu-id="92e6a-125">Erstellen einer SharePoint-Add-In zum Zugreifen auf externe Daten mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="92e6a-125">Create an SharePoint Add-in to access external data using REST</span></span>
<span data-ttu-id="92e6a-126"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="92e6a-126"><a name="bkmk_CreateApp"> </a></span></span>

<span data-ttu-id="92e6a-127">Die folgenden Schritte führen Sie durch eine SharePoint-Add-In einrichten und Konfigurieren von einer Webseite zum Verwenden von REST-Funktionen zum Abrufen von Daten aus einer externen Datenquelle anzufordern.</span><span class="sxs-lookup"><span data-stu-id="92e6a-127">The following procedures guide you through setting up an SharePoint Add-in and configuring a webpage to make requests using REST functions to retrieve data from an external data source.</span></span>
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a><span data-ttu-id="92e6a-128">Erstellen einer SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="92e6a-128">To create an SharePoint Add-in</span></span>


1. <span data-ttu-id="92e6a-129">Öffnen Sie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="92e6a-129">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="92e6a-130">Erstellen einer **App für SharePoint**-Projekt.</span><span class="sxs-lookup"><span data-stu-id="92e6a-130">Create an **App for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="92e6a-p103">Geben Sie die Appeinstellungen, einschließlich app-Name die URL der Website für das Debuggen der app und wie Sie die app (automatisch gehostet, vom Anbieter gehosteten, SharePoint-Hosting) hosten möchten. Weitere Informationen zu Hostingoptionen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="92e6a-p103">Specify the app settings, including app name, the site URL for debugging the app, and how you want to host the app (Autohosted, Provider-hosted, SharePoint-hosted). For more information about hosting options, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="92e6a-133">Wählen Sie auf **Fertig stellen**, um die app zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="92e6a-133">Choose **Finish** to create the app.</span></span>
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="92e6a-134">Um den externen Inhaltstyp zu generieren.</span><span class="sxs-lookup"><span data-stu-id="92e6a-134">To generate the external content type</span></span>


1. <span data-ttu-id="92e6a-135">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="92e6a-135">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content Types for External Data Source**.</span></span>
    
  
2. <span data-ttu-id="92e6a-p104">**OData-Quelle geben** Sie auf der Seite Geben Sie die URL der OData-Dienst, den, dem Sie mit verbinden möchten. In diesem Fall verwenden Sie die Northwind-OData-Quelle auf [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem)veröffentlicht. Legen Sie die URL für den OData-Dienst auf  `http://services.odata.org/Northwind/Northwind.svc/`, und geben Sie einen Namen für die Datenquelle.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p104">In the **Specify OData Source** page, enter the URL of the OData service you want to connect to. In this case, use the Northwind OData source published at [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Set the URL for the OData service to  `http://services.odata.org/Northwind/Northwind.svc/`, and provide a name for the data source.</span></span>
    
    <span data-ttu-id="92e6a-139">Wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="92e6a-139">Choose **Next**.</span></span>
    
  
3. <span data-ttu-id="92e6a-p105">Dadurch wird eine Liste aller Datenentitäten, die vom OData Service verfügbar gemacht werden. Wählen Sie die **Kunden**-Entität. Stellen Sie sicher, dass das Kontrollkästchen **für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge) Listeninstanzen erstellen** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p105">This displays a list of data entities that are being exposed by the OData Service. Select the **Customers** entity. Ensure that the **Create list instances for the selected data entities (except Service Operations)** check box is selected.</span></span>
    
  
4. <span data-ttu-id="92e6a-143">Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="92e6a-143">Choose **Finish**.</span></span>
    
  

## <a name="code-example-add-scripts-and-html-to-the-homeaspx-page"></a><span data-ttu-id="92e6a-144">Codebeispiel: Hinzufügen von Skripts und HTML auf der Seite Home.aspx</span><span class="sxs-lookup"><span data-stu-id="92e6a-144">Code example: Add scripts and HTML to the Home.aspx page</span></span>
<span data-ttu-id="92e6a-145"><a name="bkmk_AddUIelements"> </a></span><span class="sxs-lookup"><span data-stu-id="92e6a-145"><a name="bkmk_AddUIelements"> </a></span></span>

<span data-ttu-id="92e6a-146">Zu diesem Zeitpunkt haben Sie einen externen Inhaltstyp und eine externe Liste, in der die Daten aus der Northwind OData-Quelle angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="92e6a-146">At this point, you have an external content type and an external list that will display the data from the Northwind OData source.</span></span> 
  
    
    
<span data-ttu-id="92e6a-p106">Nächste Ziel ist es, die Seite "default.aspx" zu ändern, die erstellt wurde, wenn Sie Ihre app erstellt haben. Fügen Sie einen Container zum Speichern der Ergebnisse der Abfrage, die mit Laden der Seite ausgeführt wird. Durch Ausführen des Skripts auf der Seite Load-Ereignis, stellen Sie sicher, dass das Skript ausgeführt wird, jedes Mal wird die Seite durchsucht, und die resultierenden REST-Aufrufe auf die Northwind OData-Quelle erfolgen Datensätze auf der Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p106">The next objective is to modify the default.aspx page that was created when you created your app. You will add a container to hold the results of the query that is executed with the page loads. By executing the scripts on the page load event, you ensure that the script is executed every time the page is browsed, and the resulting REST calls are made to the Northwind OData source to add records to the page.</span></span>
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a><span data-ttu-id="92e6a-150">So fügen Sie dem Container zur Seite Default.aspx hinzu</span><span class="sxs-lookup"><span data-stu-id="92e6a-150">To add the container to the Default.aspx page</span></span>


1. <span data-ttu-id="92e6a-151">Öffnen Sie im **Projektmappen-Explorer** die Seite "Default.aspx" im Modul **Seiten**.</span><span class="sxs-lookup"><span data-stu-id="92e6a-151">In **Solution Explorer**, open the Default.aspx page in the **Pages** module.</span></span>
    
  
2. <span data-ttu-id="92e6a-152">Fügen Sie das folgende **div** Element auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="92e6a-152">Add the following **div** element to the page.</span></span>
    
```HTML
  
<div id="displayDiv"></div>
```

3. <span data-ttu-id="92e6a-153">Speichern Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="92e6a-153">Save the page.</span></span>
    
  
<span data-ttu-id="92e6a-154">Zum Schluss fügen Sie Code auf die Datei App.js, die beim Laden der Seite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="92e6a-154">Finally, you add code to the App.js file that executes when the page loads.</span></span>
  
    
    

### <a name="to-modify-the-appjs-file-to-make-rest-calls"></a><span data-ttu-id="92e6a-155">So ändern Sie die Datei App.js REST-Anrufe</span><span class="sxs-lookup"><span data-stu-id="92e6a-155">To modify the App.js file to make REST calls</span></span>


1. <span data-ttu-id="92e6a-156">Öffnen Sie die Datei App.js in das Modul Skripts Ihrer SharePoint-Projekts.</span><span class="sxs-lookup"><span data-stu-id="92e6a-156">Open the App.js file in the Scripts module of your SharePoint project.</span></span>
    
  
2. <span data-ttu-id="92e6a-157">Fügen Sie den folgenden Code am Ende der Datei.</span><span class="sxs-lookup"><span data-stu-id="92e6a-157">Paste the following code at the end of the file.</span></span>
    
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

<span data-ttu-id="92e6a-p107">Drücken Sie F5, um die app in SharePoint bereitstellen. Wechseln Sie zur Seite Default.aspx in der app, und eine Liste der Kunden wird auf der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="92e6a-p107">Press F5 to deploy the app to SharePoint. Browse to the Default.aspx page in the app, and a list of customers appears on the page.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="92e6a-160">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="92e6a-160">Additional resources</span></span>
<span data-ttu-id="92e6a-161"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="92e6a-161"><a name="bkmk_Addres"> </a></span></span>


-  [<span data-ttu-id="92e6a-162">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92e6a-162">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="92e6a-163">Erste Schritte mit den SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="92e6a-163">Get to know the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="92e6a-164">Verwenden des SharePoint REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="92e6a-164">Using the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [<span data-ttu-id="92e6a-165">Add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92e6a-165">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="92e6a-166">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92e6a-166">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

