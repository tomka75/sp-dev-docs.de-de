---
title: "Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e7b5afc5617df0998f34dc2d6e353ffd8a4d4998
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="access-sharepoint-data-from-add-ins-using-the-cross-domain-library"></a><span data-ttu-id="f9443-102">Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="f9443-102">Access SharePoint data from add-ins using the cross-domain library</span></span>
<span data-ttu-id="f9443-103">In diesem Artikel erfahren Sie, wie Sie von Ihrem Add-In aus mithilfe der domänenübergreifenden Bibliothek in SharePoint auf Daten einer SharePoint-Website zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="f9443-103">Learn how to access data in a SharePoint website from your add-in by using the cross domain library in SharePoint.</span></span>
 

 <span data-ttu-id="f9443-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f9443-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="f9443-p102">Beim Erstellen von SharePoint Add-Ins müssen Sie in der Regel Daten aus verschiedenen Quellen einbinden. Aus [Sicherheitsgründen](http://msdn.microsoft.com/library/cc709423.aspx) gibt es jedoch Blockierungsmechanismen, die die Kommunikation mit mehr als einer Domäne zur gleichen Zeit verhindern. Diese Sicherheitsmechanismen sind in den meisten Browsern implementiert und unterbinden clientseitige domänenübergreifende Aufrufe nahezu.</span><span class="sxs-lookup"><span data-stu-id="f9443-p102">When you build SharePoint Add-ins, you usually have to incorporate data from various sources. But for  [security reasons](http://msdn.microsoft.com/library/cc709423.aspx), there are blocking mechanisms that prevent communication with more than one domain at a time. These security mechanisms are implemented in most browsers, making difficult or impossible to accomplish client-side calls across domains.</span></span>
 

<span data-ttu-id="f9443-110">Abbildung 1 zeigt eine blockierte domänenübergreifende Anforderung.</span><span class="sxs-lookup"><span data-stu-id="f9443-110">Figure 1 shows a blocked request across domains.</span></span>
 


<span data-ttu-id="f9443-111">**Abbildung 1. Blockierte domänenübergreifende Anforderung**</span><span class="sxs-lookup"><span data-stu-id="f9443-111">**Figure 1. Blocked request across domains**</span></span>

 
<span data-ttu-id="f9443-p103">Wenn ein Benutzer eine Webseite aus Ihrer Add-In-Domäne (1) anfordert, ist die clientseitige Kommunikation nur an diese Domäne gebunden. Ihr Add-In kann clientseitige Aufrufe von der Webseite nur zu anderen Ressourcen in derselben Domäne machen. Add-Ins fordern normalerweise aber Ressourcen von anderen Domänen an, wie der SharePoint-Domäne, um ihre Szenarien zu erfüllen. Im Code auf Ihrer Webseite können Sie versuchsweise eine Anforderung an die SharePoint-Domäne (2) senden, die vom Browser blockiert wird. Normalerweise sehen Sie die Fehlermeldung **Zugriff verweigert**. Der Fehler impliziert aber nicht, dass Sie keine Berechtigungen für die angeforderten Ressourcen haben, sondern Sie können in der Regel nur keine Anforderung an die genannten Ressourcen senden.</span><span class="sxs-lookup"><span data-stu-id="f9443-p103">When a user requests a page from your add-in domain (1), the client-side communication is bound only to that domain. Your add-in can issue client-side calls from the page only to other resources in the same domain. However, add-ins usually require resources from other domains, such as the SharePoint domain, to fulfill their scenarios. In the code in your page, you may try to issue a request to the SharePoint domain (2), which is blocked by the browser. You usually see an  **Access is denied** error. The error doesn't imply that you don't have permissions to the requested resources but, most likely, you can't even issue a request to the mentioned resources.</span></span>
 
<span data-ttu-id="f9443-p104">Wenn Sie die domänenübergreifende Bibliothek verwenden, können die Webseiten in Ihrem Add-In auf Daten in der Add-In-Domäne und in der SharePoint-Domäne zugreifen. Die domänenübergreifende Bibliothek ist eine clientseitige Alternative in Form einer auf der SharePoint-Website gehosteten JavaScript-Datei (SP.RequestExecutor.js), auf die Sie in Ihrem Remote-Add-In verweisen können. Die domänenübergreifende Bibliothek ermöglicht Ihnen, über einen Proxy auf der Remote-Add-In-Seite mit mehreren Domänen zu interagieren. Diese Option ist geeignet, wenn Sie den Add-In-Code auf dem Client statt auf dem Server ausführen möchten oder wenn Konnektivitätsbarrieren, z. B. Firewalls, zwischen SharePoint und der Remoteinfrastruktur bestehen. Sie können auf Daten im Hostweb zugreifen – beispielsweise können Sie auf Listen zugreifen, mit denen Endbenutzer unabhängig von Ihrem Add-In interagieren. Oder Sie können auf Daten im Add-In zugreifen, wie Listen, die speziell für Ihr Add-In bereitgestellt wurden. Add-Ins mit Mandantenbereich können zudem auf andere Websitesammlungen und Websites zugreifen, sofern das Add-In über die erforderlichen Berechtigungen verfügt und als Batchinstallation mittels des Add-In-Katalogs bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="f9443-p104">When you use the cross-domain library, the webpages in your add-in can access data in your add-in domain and the SharePoint domain. The cross-domain library is a client-side alternative in the form of a JavaScript file (SP.RequestExecutor.js) that is hosted in the SharePoint website that you can reference in your remote add-in. The cross-domain library lets you interact with more than one domain in your remote add-in page through a proxy. It is a good option if you like your add-in code to run on the client instead of on the server, and if there are connectivity barriers, such as firewalls, between SharePoint and your remote infrastructure. You can access data in the host web—for example, you can access lists that end users interact with regardless of your add-in. Or you can access data in the add-in web, such as lists specifically provisioned for your add-in. Add-ins can also access other site collections and websites as long as the add-in has tenant-scoped permissions and it has been deployed as a batch installation using the add-in catalog.</span></span>
 

 <span data-ttu-id="f9443-p105">**Hinweis** In diesem Thema bezieht sich **Add-In-Domäne** auf die Domäne, die die Add-In-Seiten hostet. Dies kann die Domäne einer Remote-Webanwendung in einem Add-In, die vom Anbieter gehostet wird, sein, oder Add-In-Seiten können sich auch in SharePoint im Add-In-Web befinden und Aufrufe an die Hostwebdomäne machen. In diesem Fall ist die Add-In-Domäne die Domäne des Add-In-Webs.</span><span class="sxs-lookup"><span data-stu-id="f9443-p105">**Note**  In this topic,  **add-in domain** refers to the domain that hosts the add-in pages. This can be the domain of a remote web application in a provider-hosted, but add-in pages can also be on SharePoint in the add-in web and make calls to the host web domain. In the latter scenario, the add-in domain is the domain of the add-in web.</span></span>
 

<span data-ttu-id="f9443-p106">Das Hauptbeispiel in diesem Artikel zeigt Ihnen, wie Sie ein Add-In erstellen können, die Daten im Add-In-Web liest und diese in einer Webseite anzeigt. Der Abschnitt  [Nächste Schritte](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Next) zeigt weitere Szenarien an, die auf dem Hauptbeispiel aufbauen.</span><span class="sxs-lookup"><span data-stu-id="f9443-p106">The main example in this article shows how to build an add-in that reads data on the add-in web and displays it in a webpage. The  [Next steps](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Next) section shows more scenarios that build on top of the main example.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="f9443-130">Voraussetzungen für die Verwendung der Beispiele in diesem Artikel</span><span class="sxs-lookup"><span data-stu-id="f9443-130">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="f9443-131"><a name="SP15Accessdatafromremoteapp_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-131"><a name="SP15Accessdatafromremoteapp_Prereq"> </a></span></span>

<span data-ttu-id="f9443-132">Um diese Beispiele auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f9443-132">To follow the examples in this article, you need the following:</span></span>
 

 

-  [<span data-ttu-id="f9443-133">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f9443-133">Visual Studio 2012</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=30682)
    
 
-  [<span data-ttu-id="f9443-134">Microsoft Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f9443-134">Microsoft Office Developer Tools for Visual Studio 2012</span></span>](https://msdn.microsoft.com/en-us/office/aa905340.aspx)
    
 
- <span data-ttu-id="f9443-135">Eine SharePoint-Entwicklungsumgebung (App-Isolierung für lokale Szenarien erforderlich)</span><span class="sxs-lookup"><span data-stu-id="f9443-135">A SharePoint development environment (app isolation required for on-premises scenarios)</span></span>
    
 

## <a name="read-data-on-the-add-in-web-using-the-cross-domain-library"></a><span data-ttu-id="f9443-136">Lesen von Daten im Add-In-Web unter Verwendung der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="f9443-136">Read data on the add-in web using the cross-domain library</span></span>
<span data-ttu-id="f9443-137"><a name="SP15Accessdatafromremoteapp_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-137"><a name="SP15Accessdatafromremoteapp_Codeexample"> </a></span></span>

<span data-ttu-id="f9443-p107">In diesem Beispiel wurde eine einfache Webseite außerhalb von SharePoint gehostet, die einen Representational State Transfer- (REST-)Endpunkt benötigt, um Daten einer SharePoint-Website (Add-In-Web) zu lesen. Da die domänenübergreifende Bibliothek ein Add-In-Web erfordert, sollten Sie mit diesem Szenario beginnen.</span><span class="sxs-lookup"><span data-stu-id="f9443-p107">In this example, there is a simple page hosted outside of SharePoint that uses a Representational State Transfer (REST) endpoint to read data in a SharePoint website (the add-in web). Since the cross-domain library requires an add-in web, it makes sense to start with this scenario.</span></span>
 

 
<span data-ttu-id="f9443-140">Gehen Sie wie folgt vor, um Daten im Add-In-Web zu lesen:</span><span class="sxs-lookup"><span data-stu-id="f9443-140">To read data from the add-in web, you must do the following:</span></span>
 

 

1. <span data-ttu-id="f9443-141">Erstellen Sie ein SharePoint-Add-In-Projekt und Webprojekte.</span><span class="sxs-lookup"><span data-stu-id="f9443-141">Create a SharePoint Add-in and web projects.</span></span>
    
 
2. <span data-ttu-id="f9443-p108">Erstellen Sie Listenelemente im Add-In-Web. Mit diesem Schritt stellen Sie auch sicher, dass ein Add-In-Web erstellt wird, wenn Benutzer das Add-In bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="f9443-p108">Create list items in the add-in web. This step also ensures that an add-in web is created when users deploy the add-in.</span></span>
    
 
3. <span data-ttu-id="f9443-144">Erstellen Sie eine Add-In-Seite, die mithilfe der domänenübergreifenden Bibliothek die Listenelemente liest.</span><span class="sxs-lookup"><span data-stu-id="f9443-144">Create an add-in page that uses the cross-domain library to read the list items.</span></span>
    
 
<span data-ttu-id="f9443-145">Abbildung 2 zeigt eine Webseite, die Daten im Add-In-Web anzeigt.</span><span class="sxs-lookup"><span data-stu-id="f9443-145">Figure 2 shows a webpage that displays the data on the add-in web.</span></span>
 

 

<span data-ttu-id="f9443-146">**Abbildung 2. Webseite, die Daten im Add-In-Web anzeigt**</span><span class="sxs-lookup"><span data-stu-id="f9443-146">**Figure 2. Webpage that displays the data on the add-in web**</span></span>

 

 
![Beispielergebnisbildschirm für domänenübergreifende Leseelemente](../images/CrossDomainReadItemsResult.png)
 

### <a name="create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="f9443-148">Erstellen eines SharePoint-Add-In- und Web-Projekts</span><span class="sxs-lookup"><span data-stu-id="f9443-148">Create a SharePoint Add-in and web projects</span></span>


1. <span data-ttu-id="f9443-p109">Öffnen Sie Visual Studio 2012 als Administrator. (Klicken Sie dazu im Menü **Start** mit der rechten Maustaste auf das Symbol für Visual Studio 2012, und wählen Sie **Als Administrator ausführen** aus.)</span><span class="sxs-lookup"><span data-stu-id="f9443-p109">Open Visual Studio 2012 as administrator. (To do this, right-click the Visual Studio 2012 icon on the  **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="f9443-151">Erstellen Sie ein neues Projekt unter Verwendung der Vorlage **SharePoint-Add-In**.</span><span class="sxs-lookup"><span data-stu-id="f9443-151">Create a new project using the  **Add-in for SharePoint** template.</span></span>
    
    <span data-ttu-id="f9443-152">Die Vorlage **SharePoint-Add-In** in Visual Studio 2012 befindet sich unter **Vorlagen** **>** **Visual C#**, **Office SharePoint** **>** **Add-Ins**.</span><span class="sxs-lookup"><span data-stu-id="f9443-152">The  **Add-in for SharePoint** template in Visual Studio 2012 is located under **Templates** **>** **Visual C#**,  **Office SharePoint** **>** **Add-ins**.</span></span>
    
 
3. <span data-ttu-id="f9443-153">Geben Sie die URL der SharePoint-Website an, die Sie für das Debugging verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f9443-153">Provide the SharePoint website URL that you want to use for debugging.</span></span>
    
 
4. <span data-ttu-id="f9443-154">Wählen Sie als Hostingoption für Ihr Add-In **Von Anbieter gehostet** aus.</span><span class="sxs-lookup"><span data-stu-id="f9443-154">Select  **Provider-hosted** as the hosting option for your add-in.</span></span>
    
     <span data-ttu-id="f9443-p110">**Hinweis** Sie können die domänenübergreifende Bibliothek auch in einem von SharePoint gehosteten Add-In verwenden. In einem von SharePoint gehosteten Add-In befindet sich die Add-In-Seite jedoch bereits im Add-In-Web. In diesem Fall benötigt sie nicht die domänenübergreifende Bibliothek zum Lesen von Listenelementen. Ein Beispiel zu einem von SharePoint gehosteten Add-In, das Daten im Hostweb lesen kann, finden Sie unter [Verwenden der domänenübergreifenden Bibliothek in einem von SharePoint gehosteten Add-In (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814) oder unter [Zugreifen auf Daten in einem Hostweb](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) später in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="f9443-p110">**Note**  You can also use the cross-domain library in a SharePoint-hosted add-in. However, in a SharePoint-hosted add-in the add-in page is already in the add-in web, in which case it wouldn't need the cross-domain library to read the list items. For a SharePoint-hosted add-in sample that reads data in the host web, see  [Use the cross-domain library in a SharePoint-hosted add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814) or see [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) later in this article.</span></span>

### <a name="create-list-items-on-the-add-in-web"></a><span data-ttu-id="f9443-158">Erstellen von Listenelementen im Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="f9443-158">Create list items on the add-in web</span></span>


1. <span data-ttu-id="f9443-p111">Klicken Sie im **Projektmappen-Explorer** auf das SharePoint-Add-In-Projekt. Wählen Sie **Hinzufügen** **>** **Neues Element…**.</span><span class="sxs-lookup"><span data-stu-id="f9443-p111">Right-click the SharePoint Add-in project in  **Solution Explorer**. Choose  **Add** **>** **New Item…**</span></span>
    
 
2. <span data-ttu-id="f9443-p112">Wählen Sie **Visual C#-Elemente** **>** **Office/SharePoint** **>** **Liste**. Geben Sie Ihrer Liste den Namen **Ankündigungen**.</span><span class="sxs-lookup"><span data-stu-id="f9443-p112">Choose  **Visual C# Items** **>** **Office/SharePoint** **>** **List**. Set the name of your list to  **Announcements**.</span></span>
    
 
3. <span data-ttu-id="f9443-p113">Doppelklicken Sie auf **Ankündigungen** **>** **Elements.xml**. Fügen Sie die folgenden XML-Knoten als untergeordnete Objekte des **ListInstance**-Elements ein.</span><span class="sxs-lookup"><span data-stu-id="f9443-p113">Double click  **Announcements** **>** **Elements.xml**. Paste the following XML nodes as children of the  **ListInstance** element.</span></span>
    
```
  <Data>
    <Rows>
        <Row>
            <Field Name="Title">Lorem ipsum 1</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
        <Row>
            <Field Name="Title">Lorem ipsum 2</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
    </Rows>
</Data>
```


### <a name="to-add-a-new-page-that-uses-the-cross-domain-library"></a><span data-ttu-id="f9443-165">So fügen Sie eine neue Seite hinzu, die die domänenübergreifende Bibliothek verwendet</span><span class="sxs-lookup"><span data-stu-id="f9443-165">To add a new page that uses the cross-domain library</span></span>


1. <span data-ttu-id="f9443-166">Doppelklicken Sie im **Projektmappen-Explorer** auf die Datei **Default.aspx**.</span><span class="sxs-lookup"><span data-stu-id="f9443-166">Double-click  **Default.aspx** in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="f9443-p114">Kopieren Sie den folgenden Code, und fügen Sie ihn in die Datei „Default.aspx“ ein. Der Code führt die folgenden Aufgaben aus:</span><span class="sxs-lookup"><span data-stu-id="f9443-p114">Copy the following code and paste it in the Default.aspx file. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="f9443-169">Laden der jQuery-Bibliothek aus dem Microsoft CDN.</span><span class="sxs-lookup"><span data-stu-id="f9443-169">Loads the jQuery library from the Microsoft CDN.</span></span>
    
 
  - <span data-ttu-id="f9443-170">Stellt einen Platzhalter für das Ergebnis bereit.</span><span class="sxs-lookup"><span data-stu-id="f9443-170">Provides a placeholder for the result.</span></span>
    
 
  - <span data-ttu-id="f9443-171">Extrahiert die Add-In-Web-URL aus der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="f9443-171">Extracts the add-in web URL from the query string.</span></span>
    
 
  - <span data-ttu-id="f9443-172">Lädt das JavaScript für die domänenübergreifende Bibliothek mithilfe der **getScript**-Funktion in jQuery.</span><span class="sxs-lookup"><span data-stu-id="f9443-172">Loads the cross-domain library JavaScript using the  **getScript** function in jQuery.</span></span>
    
    <span data-ttu-id="f9443-173">Die Funktion lädt die erforderlichen Ressourcen und geht dann zur angegebenen Funktion über. Sie stellt sicher, dass die domänenübergreifende Bibliothek geladen und verfügbar für den nachfolgenden Code ist.</span><span class="sxs-lookup"><span data-stu-id="f9443-173">The function loads the required resources and then continues to the specified function, ensuring that the cross-domain library is loaded and available to use by the subsequent code.</span></span>
    
 
  - <span data-ttu-id="f9443-p115">Instantiiert das **RequestExecutor**-Objekt. Standardmäßig verwendet RequestExecutor das Add-In-Web als Kontextwebsite.</span><span class="sxs-lookup"><span data-stu-id="f9443-p115">Instantiates the  **RequestExecutor** object. By default, RequestExecutor uses the add-in web as the context site.</span></span>
    
     <span data-ttu-id="f9443-p116">**Hinweis** Sie können die Kontextwebsite durch andere Websites, die sich vom Add-In-Web unterscheiden, mithilfe des **AppContextSite**-Endpunkts (REST) oder -Objekts (JSOM) ersetzen. Weitere Informationen zu AppContextSite finden Sie unter [Zugreifen auf Daten in einem Hostweb](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="f9443-p116">**Note**  You can change the context site to other sites different than the add-in web by using the  **AppContextSite** endpoint (REST) or object (JSOM). To learn more about AppContextSite, see [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) later in this article.</span></span>
  - <span data-ttu-id="f9443-178">Gibt einen REST-Aufruf an den Listenelementendpunkt aus.</span><span class="sxs-lookup"><span data-stu-id="f9443-178">Issues a REST call to the list items endpoint.</span></span>
    
 
  - <span data-ttu-id="f9443-179">Sorgt für einen erfolgreichen Abschluss und zeigt die Listenelemente auf der Webseite an.</span><span class="sxs-lookup"><span data-stu-id="f9443-179">Handles successful completion, displaying the list items on the webpage.</span></span>
    
 
  - <span data-ttu-id="f9443-180">Behandelt Fehler und zeigt die Fehlermeldung auf der Webseite an.</span><span class="sxs-lookup"><span data-stu-id="f9443-180">Handles errors, displaying the error message on the webpage.</span></span>
    
 

```
  
<html>
    <head>
        <title>Cross-domain sample</title>
    </head>
    <body>
        <!-- This is the placeholder for the announcements -->
        <div id="renderAnnouncements"></div>
        <script 
            type="text/javascript" 
            src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
        </script>
        <script type="text/javascript">
          var hostweburl;
          var appweburl;

          // Load the required SharePoint libraries
          $(document).ready(function () {
            //Get the URI decoded URLs.
            hostweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPHostUrl")
            );
            appweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPAppWebUrl")
            );

            // resources are in URLs in the form:
            // web_url/_layouts/15/resource
            var scriptbase = hostweburl + "/_layouts/15/";

            // Load the js files and continue to the successHandler
            $.getScript(scriptbase + "SP.RequestExecutor.js", execCrossDomainRequest);
          });

          // Function to prepare and issue the request to get
          //  SharePoint data
          function execCrossDomainRequest() {
            // executor: The RequestExecutor object
            // Initialize the RequestExecutor with the add-in web URL.
            var executor = new SP.RequestExecutor(appweburl);

            // Issue the call against the add-in web.
            // To get the title using REST we can hit the endpoint:
            //      appweburl/_api/web/lists/getbytitle('listname')/items
            // The response formats the data in the JSON format.
            // The functions successHandler and errorHandler attend the
            //      sucess and error events respectively.
            executor.executeAsync(
                {
                  url:
                      appweburl +
                      "/_api/web/lists/getbytitle('Announcements')/items",
                  method: "GET",
                  headers: { "Accept": "application/json; odata=verbose" },
                  success: successHandler,
                  error: errorHandler
                }
            );
          }

          // Function to handle the success event.
          // Prints the data to the page.
          function successHandler(data) {
            var jsonObject = JSON.parse(data.body);
            var announcementsHTML = "";

            var results = jsonObject.d.results;
            for (var i = 0; i < results.length; i++) {
              announcementsHTML = announcementsHTML +
                  "<p><h1>" + results[i].Title +
                  "</h1>" + results[i].Body +
                  "</p><hr>";
            }

            document.getElementById("renderAnnouncements").innerHTML =
                announcementsHTML;
          }

          // Function to handle the error event.
          // Prints the error message to the page.
          function errorHandler(data, errorCode, errorMessage) {
            document.getElementById("renderAnnouncements").innerText =
                "Could not complete cross-domain call: " + errorMessage;
          }

          // Function to retrieve a query string value.
          // For production purposes you may want to use
          //  a library to handle the query string.
          function getQueryStringParameter(paramToRetrieve) {
            var params =
                document.URL.split("?")[1].split("&amp;");
            var strParams = "";
            for (var i = 0; i < params.length; i = i + 1) {
              var singleParam = params[i].split("=");
              if (singleParam[0] == paramToRetrieve)
                return singleParam[1];
            }
          }
        </script>
    </body>
</html>
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="f9443-181">So erstellen Sie die Lösung und führen sie aus</span><span class="sxs-lookup"><span data-stu-id="f9443-181">To build and run the solution</span></span>


1. <span data-ttu-id="f9443-182">Drücken Sie F5.</span><span class="sxs-lookup"><span data-stu-id="f9443-182">Press the F5 key.</span></span>
    
     <span data-ttu-id="f9443-183">**Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.</span><span class="sxs-lookup"><span data-stu-id="f9443-183">**Note**  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="f9443-184">Klicken Sie auf die Schaltfläche **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="f9443-184">Choose the  **Trust It** button.</span></span>
    
 
3. <span data-ttu-id="f9443-185">Wählen Sie auf der Seite **Websiteinhalte** das Add-In-Symbol.</span><span class="sxs-lookup"><span data-stu-id="f9443-185">Choose the add-in icon on the  **Site Contents** page.</span></span>
    
 
<span data-ttu-id="f9443-p117">Falls Sie herunterladbare Codebeispiele bevorzugen, rufen Sie diese aus der Code Gallery ab. **Codebeispiel: Abrufen von Listenelementen mithilfe der domänenübergreifenden Bibliothek** mit [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain) oder [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).</span><span class="sxs-lookup"><span data-stu-id="f9443-p117">If you prefer downloadable code samples, you can get this one from code gallery.  **Code sample: Get list items by using the cross-domain library** using [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain) or [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).</span></span>
 

 

<span data-ttu-id="f9443-188">**Tabelle 2: Problembehandlung für die Lösung**</span><span class="sxs-lookup"><span data-stu-id="f9443-188">**Table 2. Troubleshooting the solution**</span></span>


|<span data-ttu-id="f9443-189">**Wird diese Fehlermeldung angezeigt...**</span><span class="sxs-lookup"><span data-stu-id="f9443-189">**If you see…**</span></span>|<span data-ttu-id="f9443-190">**Versuchen Sie Folgendes...**</span><span class="sxs-lookup"><span data-stu-id="f9443-190">**Then try…**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f9443-191">Fehlermeldung: Zugriff auf Ihre Website nicht möglich. Es gibt zwar eine Schaltfläche zur Fehlerbehebung, aber sie löst nicht das Problem.</span><span class="sxs-lookup"><span data-stu-id="f9443-191">Error message: Sorry, we had some trouble accessing your site.There is also a button to fix the error, but it doesn't correct the problem.</span></span>|<span data-ttu-id="f9443-192">Möglicherweise haben Sie ein bekanntes Problem mit Sicherheitszonen in Internet Explorer. Weitere Informationen dazu finden Sie unter  [Arbeiten mit der domänenübergreifenden Bibliothek in verschiedenen Internet Explorer-Sicherheitszonen in Add-Ins für SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span><span class="sxs-lookup"><span data-stu-id="f9443-192">You may have hit a known problem with security zones in Internet Explorer, see  [Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span></span>|
|<span data-ttu-id="f9443-p118">Fehlermeldung: Die erforderlichen Funktionen werden von Ihrem Browser nicht unterstützt. Stellen Sie bitte sicher, dass Sie IE8 oder höher bzw. einen anderen modernen Browser verwenden. Stellen Sie bitte ferner sicher, dass das Metatag "X-UA-Compatible" auf "IE = 8" oder höher festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="f9443-p118">Error message: The required functionalities are not supported by your browser. Please make sure you are using IE 8 or above, or other modern browser. Please make sure the 'X-UA-Compatible' meta tag is set to be 'IE=8' or above.</span></span>|<span data-ttu-id="f9443-p119">Die domänenübergreifende Bibliothek erfordert den Dokumentmodus **IE8** oder höher. In einigen Fällen ist der Dokumentmodus standardmäßig auf **IE7** festgelegt. Sie können die Internet Explorer-Entwicklertools verwenden, um den Dokumentmodus der Seite zu ermitteln bzw. zu ändern. Weitere Informationen finden Sie unter [Definieren der Dokumentkompatibilität](http://msdn.microsoft.com/library/cc288325.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9443-p119">The cross-domain library requires a document mode of  **IE8** or above. In some scenarios, the document mode is set to **IE7** by default. You can use the Internet Explorer developer tools to determine and change the document mode of your page. For more information, see [Defining Document Compatibility](http://msdn.microsoft.com/library/cc288325.aspx).</span></span>|
|<span data-ttu-id="f9443-200">Fehlermeldung: „Typ“ wurde nicht definiert. Ihr Add-In verwendet auch das JavaScript-Objektmodell (JSOM).</span><span class="sxs-lookup"><span data-stu-id="f9443-200">Error message: 'Type' is undefined.Additionally, your add-in uses the JavaScript Object Model (JSOM).</span></span>|<span data-ttu-id="f9443-p120">Das JSOM verwendet die **Type.registerNamespace**-Methode in der Microsoft Ajax-Bibliothek, um den **SP**-Namespace zu registrieren. Verwenden Sie den folgenden Code, um einen Verweis von Ihrer Webseite auf die Microsoft Ajax-Bibliothek zu erstellen:```HTML<script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```</span><span class="sxs-lookup"><span data-stu-id="f9443-p120">The JSOM uses the  **Type.registerNamespace** method in the Microsoft Ajax library to register the **SP** namespace. Use the following code to add a reference to the Microsoft Ajax library from your page:```HTML<script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f9443-203">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="f9443-203">Next steps</span></span>
<span data-ttu-id="f9443-204"><a name="SP15Accessdatafromremoteapp_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-204"><a name="SP15Accessdatafromremoteapp_Next"> </a></span></span>

<span data-ttu-id="f9443-p121">Dieser Artikel zeigt, wie Sie eine Anforderungen an einen REST-Endpunkten senden, um Daten im Add-In-Web über eine Add-In-Seite zu lesen, die nicht auf SharePoint gehostet ist. Sie können auch die folgenden Szenarien untersuchen und Details zur domänenübergreifenden Bibliothek anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f9443-p121">This article shows how to query a REST endpoint to read data from the add-in web by using an add-in page that is not hosted on SharePoint. You can also explore the following scenarios and details about the cross-domain library.</span></span>
 

 

### <a name="use-the-jsom-to-read-data-from-the-add-in-web"></a><span data-ttu-id="f9443-207">Verwenden des JSOM zum Lesen von Daten im Add-In-Web:</span><span class="sxs-lookup"><span data-stu-id="f9443-207">Use the JSOM to read data from the add-in web</span></span>
<span data-ttu-id="f9443-208"><a name="SP15Accessdatafromremoteapp_JSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-208"><a name="SP15Accessdatafromremoteapp_JSOM"> </a></span></span>

<span data-ttu-id="f9443-p122">Sie möchten vielleicht lieber das JSOM anstelle von REST verwenden, um Daten aus dem Add-In-Web anzufordern. Sie müssen zusätzliche Tasks ausführen, um die domänenübergreifende Bibliothek zusammen mit JSOM verwenden zu können:</span><span class="sxs-lookup"><span data-stu-id="f9443-p122">Depending on your preference, you might want to use the JSOM instead of REST to query data from the add-in web. You must complete additional tasks to use the cross-domain library with JSOM:</span></span>
 

 

- <span data-ttu-id="f9443-211">Verweisen Sie auf SharePoint JSOM auf Ihrer Add-In-Seite.</span><span class="sxs-lookup"><span data-stu-id="f9443-211">Reference the SharePoint JSOM in your add-in page.</span></span>
    
 
- <span data-ttu-id="f9443-212">Initialisieren Sie das **ProxyWebRequestExecutorFactory**-Objekt, und legen Sie es als die Factory des Kontextobjekts fest.</span><span class="sxs-lookup"><span data-stu-id="f9443-212">Initialize the  **ProxyWebRequestExecutorFactory** object and set it as the factory of the context object.</span></span>
    
 
- <span data-ttu-id="f9443-213">Greifen Sie auf die SharePoint-Objekte zu, um Daten in der Liste zu lesen.</span><span class="sxs-lookup"><span data-stu-id="f9443-213">Access the SharePoint objects to read the data from the list.</span></span>
    
 
- <span data-ttu-id="f9443-214">Laden Sie die Objekte in den Kontext, und führen Sie die Abfrage aus.</span><span class="sxs-lookup"><span data-stu-id="f9443-214">Load the objects in the context and execute the query.</span></span>
    
 
<span data-ttu-id="f9443-p123">Ein Codebeispiel, das zeigt, wie Sie die Tasks ausführen, finden Sie in  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain) Weitere Informationen zur Verwendung von JSOM finden Sie in [Verwenden des JavaScript-Objektmodells (JSOM) in Add-Ins für SharePoint](http://blogs.msdn.com/b/officeapps/archive/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9443-p123">For a code sample that shows how to perform the tasks, see  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain). For more information on how to use the JSOM, see  [Using the JavaScript object model (JSOM) in SharePoint Add-ins](http://blogs.msdn.com/b/officeapps/archive/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint.aspx).</span></span>
 

 

### <a name="access-data-from-the-host-web"></a><span data-ttu-id="f9443-217">Zugreifen auf Daten in einem Hostweb</span><span class="sxs-lookup"><span data-stu-id="f9443-217">Access data from the host web</span></span>
<span data-ttu-id="f9443-218"><a name="SP15Accessdatafromremoteapp_Hostweb"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-218"><a name="SP15Accessdatafromremoteapp_Hostweb"> </a></span></span>

<span data-ttu-id="f9443-p124">Das Beispiel auf dieser Seite zeigt, wie Daten im Add-In-Web gelesen werden. Dieses Beispiel ist ein guter Einstieg, da die domänenübergreifende Bibliothek anfangs das Add-In als Kontextwebsite verwendet. Aber es mag viele andere Szenarien geben, in denen Sie auf Daten im Hostweb zugreifen möchten. Dafür sind einige zusätzliche Tasks erforderlich:</span><span class="sxs-lookup"><span data-stu-id="f9443-p124">The example in this page shows how to read data from the add-in web. This works fine as the starting example because the cross-domain library initially uses the add-in as the context site. However, there are many scenarios where you want to access data on the host web. There are a few tasks required to access data on the host web:</span></span> 
 

 

- <span data-ttu-id="f9443-223">Legen Sie das Hostweb als Kontextwebsite für die domänenübergreifende Bibliothek fest.</span><span class="sxs-lookup"><span data-stu-id="f9443-223">Set the host web as the context site for the cross-domain library.</span></span>
    
 
- <span data-ttu-id="f9443-224">Stellen Sie ausreichende Berechtigungen für das Add-In bereit.</span><span class="sxs-lookup"><span data-stu-id="f9443-224">Provide appropriate permissions to the add-in.</span></span>
    
 
<span data-ttu-id="f9443-p125">Sie können die Kontextwebsite über den **AppContextSite**-Endpunkt (REST) oder das Objekt (JSOM) ändern. Das folgende Beispiel zeigen Ihnen, wie Sie die Kontextwebsite mithilfe des REST-Endpunkts ändern:</span><span class="sxs-lookup"><span data-stu-id="f9443-p125">You can change the context site by using the  **AppContextSite** endpoint (REST) or object (JSOM). The following example shows how to change the context site using the REST endpoint:</span></span>
 

 



```
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/title?@target='" +
            hostweburl + "'",
        method: "GET",
        headers: { "Accept": "application/json; odata=verbose" },
        success: successHandler,
        error: errorHandler
    }
);
```

<span data-ttu-id="f9443-227">Das folgende Codebeispiel zeigt, wie die Kontextwebsite mit JSOM geändert wird:</span><span class="sxs-lookup"><span data-stu-id="f9443-227">The following code example shows how to change the context site using JSOM:</span></span>
 

 



```
context = new SP.ClientContext(appweburl);
factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
context.set_webRequestExecutorFactory(factory);
appContextSite = new SP.AppContextSite(context, hostweburl);

this.web = appContextSite.get_web();
context.load(this.web);
```

<span data-ttu-id="f9443-p126">Ihr Add-In hat standardmäßig Berechtigungen für das Add-In-Web, aber nicht für das Hostweb. Das folgende Beispiel zeigt einen Manifestabschnitt, der eine Berechtigungsanforderung zum Lesen von Daten aus dem Hostweb deklariert:</span><span class="sxs-lookup"><span data-stu-id="f9443-p126">By default, your add-in has permissions to the add-in web, but not to the host web. The following example shows a manifest section that declares a permission request to read data from the host web:</span></span>
 

 



```XML
<AppPermissionRequests>
    <AppPermissionRequest 
        Scope="http://sharepoint/content/sitecollection/web" 
        Right="Read" />
</AppPermissionRequests>
```

<span data-ttu-id="f9443-230">Stellen Sie sicher, dass Sie eine Ressource im Add-In-Web erstellen (beispielsweise eine leere Seite oder Liste), um die Bereitstellung des Add-In-Webs zu erzwingen, die für eine Verwendung der domänenübergreifenden Bibliothek erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="f9443-230">Make sure that you create a resource on the add-in web (like an empty page or list) to force the provisioning of the add-in web, which is required to use the cross-domain library.</span></span>
 

 

### <a name="access-data-across-site-collections"></a><span data-ttu-id="f9443-231">Zugreifen auf Daten in allen Websitesammlungen</span><span class="sxs-lookup"><span data-stu-id="f9443-231">Access data across site collections</span></span>
<span data-ttu-id="f9443-232"><a name="SP15Accessdatafromremoteapp_TenantScope"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-232"><a name="SP15Accessdatafromremoteapp_TenantScope"> </a></span></span>

<span data-ttu-id="f9443-p127">Dank der domänenübergreifenden Bibliothek können Sie auf Daten in allen Websitesammlungen desselben Mandanten zugreifen. Sie müssen aber einige Tasks ausführen, um websitesammlungsübergreifende auf Daten zugreifen zu können:</span><span class="sxs-lookup"><span data-stu-id="f9443-p127">With the cross-domain library, you can access data across site collections in the same tenant. There are some tasks that you need to complete to access data across site collections:</span></span>
 

 

- <span data-ttu-id="f9443-235">Fügen Sie eine Berechtigungsanforderung hinzu, um auf Daten im Mandanten zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="f9443-235">Add a permission request to access data in the tenant.</span></span>
    
 
- <span data-ttu-id="f9443-236">Wechseln Sie in Ihrem Code von der Kontextwebsite zu den Websitesammlungen, die Sie abfragen möchten.</span><span class="sxs-lookup"><span data-stu-id="f9443-236">In your code, switch the context site to the site collections that you want to query.</span></span>
    
 
- <span data-ttu-id="f9443-237">Fügen Sie das Add-In zum Add-In-Katalog hinzu.</span><span class="sxs-lookup"><span data-stu-id="f9443-237">Add the add-in to the add-in catalog.</span></span>
    
 
- <span data-ttu-id="f9443-p128">Stellen Sie das Add-In als mandantenbereichsbezogenes Add-In auf einer Website bereit. Ein Beispiel, wie Sie ein mandantenbereichsbezogenes Add-In bereitstellen, finden Sie in der Beschreibung des Codebeispiels  [Verwenden der domänenübergreifenden Bibliothek in einem mandantenbereichsbezogenen Add-In (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span><span class="sxs-lookup"><span data-stu-id="f9443-p128">Deploy the add-in as a tenant-scoped add-in to a website. For an example on how to deploy as a tenant-scoped add-in, see the description of the  [Use the cross-domain library in a tenant-scoped add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e) code sample.</span></span>
    
 
<span data-ttu-id="f9443-p129">Ihr Add-In benötigt auch Zugriffsberechtigungen für Daten aus dem Mandanten. Das folgende Beispiel zeigt einen Manifestabschnitt, der eine Berechtigungsanforderung zum Lesen von Daten aus dem Mandanten deklariert:</span><span class="sxs-lookup"><span data-stu-id="f9443-p129">Your add-in also needs permission to access data from the tenant. The following example shows a manifest section that declares a permission request to read data from the tenant:</span></span>
 

 



```XML
<AppPermissionRequests>
  <AppPermissionRequest 
    Scope="http://sharepoint/content/tenant" 
    Right="Read" />
</AppPermissionRequests>
```

<span data-ttu-id="f9443-p130">Wenn Sie die Kontextwebsite in Ihrem Code wechseln möchten, verwenden Sie den **AppContextSite**-Endpunkt (REST) oder das Objekt (JSOM), genau so wie im Abschnitt [Zugreifen auf Daten in einem Hostweb](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) beschrieben. Hier finden Sie zur Erinnerung Informationen zum REST-Endpunkt: /_api/SP.AppContextSite(@target)/web/title?@target='weburl' und ein Beispiel zum Instanziieren des Objekts in JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.</span><span class="sxs-lookup"><span data-stu-id="f9443-p130">To switch the context site in your code, use the  **AppContextSite** endpoint (REST) or object (JSOM), just like in the [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) section. Here is a reminder of the REST endpoint: /_api/SP.AppContextSite(@target)/web/title?@target='weburl', and an example on how to instantiate the object in JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.</span></span>
 

 
<span data-ttu-id="f9443-p131">Als Entwickler können Sie nur mandantenbereichsbezogene Add-Ins aus dem Add-In-Katalog bereitstellen. Den Add-In-Katalog können Sie lokal oder in SharePoint Online-Umgebungen bereitstellen. Das Hochladen Ihres Add-Ins in den Add-In-Katalog ist so einfach wie das Hochladen einer Datei in einer Dokumentbibliothek. Weitere Anweisungen finden Sie unter  [Hinzufügen von benutzerdefinierten Add-Ins zur Add-In-Katalogwebsite](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9443-p131">As a developer, you can only deploy tenant-scoped add-ins from the add-in catalog. You can provision an add-in catalog to your on-premises or SharePoint Online environments. Uploading your add-in to the add-in catalog is as simple as uploading a file to a document library. See  [Add custom add-ins to the Add-in Catalog site](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx) for detailed instructions.</span></span>
 

 
<span data-ttu-id="f9443-p132">Aus dem Add-In-Katalog können Sie das Add-In auf einer oder mehreren Websites im Mandanten bereitstellen. Da Ihr Add-In über Berechtigungen zum Zugriff auf Daten im Mandanten verfügt, müssen Sie es nur auf einer Website bereitstellen, um Datenzugriff im gesamten Mandanten zu haben. Weitere Anweisungen, wie Sie ein Add-In aus dem Add-In-Katalog bereitstellen, finden Sie unter  [Bereitstellen von benutzerdefinierten Add-Ins](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9443-p132">From the add-in catalog you can deploy the add-in to one or more websites in the tenant. Since your add-in has permissions to access data in the tenant, you only have to deploy to one website to access data on the whole tenant. See  [Deploy a custom add-in](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx) for instructions on how to deploy an add-in from the add-in catalog.</span></span>
 

 
<span data-ttu-id="f9443-251">Wenn Sie einen Beispielcode herunterladen möchten, der den Zugriff auf Daten in allen Websitesammlungen zeigt, navigieren Sie zu  [Verwenden der domänenübergreifenden Bibliothek in einem mandantenbereichsbezogenen Add-In (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span><span class="sxs-lookup"><span data-stu-id="f9443-251">To download a code sample that shows how to access data across site collections, see  [Use the cross-domain library in a tenant-scoped add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span></span>
 

 

### <a name="issuing-calls-across-different-security-zones"></a><span data-ttu-id="f9443-252">Senden von Aufrufen in unterschiedlichen Sicherheitszonen</span><span class="sxs-lookup"><span data-stu-id="f9443-252">Issuing calls across different security zones</span></span>
<span data-ttu-id="f9443-253"><a name="SP15Accessdatafromremoteapp_IEZones"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-253"><a name="SP15Accessdatafromremoteapp_IEZones"> </a></span></span>

<span data-ttu-id="f9443-p133">Die domänenübergreifende Bibliothek verwendet eine Proxyseite, die auf einem **IFrame** auf der Add-In-Seite gehostet ist, um Kommunikation zu ermöglichen. Wenn sich die Add-In-Seite und die SharePoint-Website in verschiedenen Sicherheitszonen befinden, können keine Autorisierungscookies gesendet werden. Wenn keine Autorisierungscookies vorhanden sind und IFrame die Proxyseite zu laden versucht, wird dieser zur SharePoint-Anmeldeseite weitergeleitet. Aus Sicherheitsgründen kann die SharePoint-Anmeldeseite nicht in einem IFrame enthalten sein. In diesen Szenarien kann die Bibliothek die Proxyseite nicht laden, und es ist keine Kommunikation mit SharePoint möglich.</span><span class="sxs-lookup"><span data-stu-id="f9443-p133">The cross-domain library uses a proxy page that is hosted in an  **IFrame** on the add-in page to enable communication. When the add-in page and SharePoint website are in different security zones, authorization cookies can't be sent. If there are no authorization cookies, and the IFrame tries to load the proxy page, it will be redirected to the SharePoint sign-in page. The SharePoint sign-in page can't be contained in an IFrame for security reasons. In these scenarios, the library cannot load the proxy page, and communication with SharePoint is not possible.</span></span>
 

 
<span data-ttu-id="f9443-p134">Es gibt aber eine Lösung für diesen Fall. Die Lösung ist das **apphost-Muster**, das darin besteht, die Add-In-Seiten in einer Seite zu verpacken, die im Add-In-Web gehostet ist. Das apphost-Muster eignet sich gut in Add-Ins, die die domänenübergreifende Bibliothek verwenden, selbst wenn keine offensichtlichen Sicherheitsgrenzen vorhanden sind. Weitere Informationen finden Sie unter [Arbeiten mit der domänenübergreifenden Bibliothek in verschiedenen Internet Explorer-Sicherheitszonen in SharePoint-Add-Ins](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span><span class="sxs-lookup"><span data-stu-id="f9443-p134">However, there is a solution for these scenarios. The solution is the  **apphost pattern**, which consists in wrapping the add-in pages in a page hosted in the add-in web. It's a good idea to use the apphost pattern in add-ins that use the cross-domain library, even if there are no evident security boundaries. For more information, see [Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span></span>
 

 

### <a name="access-data-from-an-additional-remote-host-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="f9443-263">Zugreifen auf Daten über einen zusätzlichen Remotehost in einem von SharePoint gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="f9443-263">Access data from an additional remote host in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="f9443-264"><a name="SP15Accessdatafromremoteapp_SPhosted"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-264"><a name="SP15Accessdatafromremoteapp_SPhosted"> </a></span></span>

<span data-ttu-id="f9443-p135">Standardmäßig ist es zulässig, dass ein von SharePoint gehostetes Add-In domänenübergreifende Aufrufe an das Hostweb sendet, vorausgesetzt es verfügt über die entsprechenden Berechtigungen. Ein von SharePoint gehostetes Add-In kann aber auch einen Remotehost im **AllowedRemoteHostUrl**-Attribut seines **AppPrincipal** angeben. Damit können Sie domänenübergreifende Aufrufe aus dem Add-In-Web und von beliebigen anderen Hosts senden.</span><span class="sxs-lookup"><span data-stu-id="f9443-p135">By default, a SharePoint-hosted add-in is allowed to issue cross-domain calls to the host web, provided that it has proper permissions. However, a SharePoint-hosted add-in can also specify a remote host in the  **AllowedRemoteHostUrl** attribute of its **AppPrincipal**. This effectively lets you issue cross-domain calls from the add-in web and from another host elsewhere.</span></span>
 

 
<span data-ttu-id="f9443-268">Wenn Sie ein Codebeispiel eines Von SharePoint gehostetes Add-In herunterladen möchten, das die domänenübergreifende Bibliothek verwendet, navigieren Sie zu  [Codebeispiel: Verwenden der domänenübergreifenden Bibliothek in einem von SharePoint gehosteten Add-In (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).</span><span class="sxs-lookup"><span data-stu-id="f9443-268">To download a sample of a SharePoint-hosted add-in that uses the cross-domain library, see  [Code sample: Use the cross-domain library in a SharePoint-hosted add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="f9443-269">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f9443-269">Additional resources</span></span>
<span data-ttu-id="f9443-270"><a name="SP15Accessdatafromremoteapp_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f9443-270"><a name="SP15Accessdatafromremoteapp_Addresources"> </a></span></span>


-  [<span data-ttu-id="f9443-271">SharePoint-Add-in-REST-OData-CrossDomain</span><span class="sxs-lookup"><span data-stu-id="f9443-271">SharePoint-Add-in-REST-OData-CrossDomain</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain)
    
 
-  [<span data-ttu-id="f9443-272">SharePoint-Add-in-JSOM-CrossDomain</span><span class="sxs-lookup"><span data-stu-id="f9443-272">SharePoint-Add-in-JSOM-CrossDomain</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain)
    
 
-  [<span data-ttu-id="f9443-273">Codebeispiel: Abrufen des Hostwebtitels mithilfe der domänenübergreifenden Bibliothek (REST)</span><span class="sxs-lookup"><span data-stu-id="f9443-273">Code sample: Get the host web title using the cross-domain library (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Get-the-0ec36bb6)
    
 
-  [<span data-ttu-id="f9443-274">Codebeispiel: Abrufen des Hostwebtitels mithilfe der domänenübergreifenden Bibliothek (JSOM)</span><span class="sxs-lookup"><span data-stu-id="f9443-274">Code sample: Get the host web title using the cross-domain library (JSOM)</span></span>](http://code.msdn.microsoft.com/office/SharePoint-2013-Get-the-563f2a3d)
    
 
-  [<span data-ttu-id="f9443-275">Codebeispiel: Verwenden der domänenübergreifenden Bibliothek in einem von SharePoint gehosteten Add-In (REST)</span><span class="sxs-lookup"><span data-stu-id="f9443-275">Code sample: Use the cross-domain library in a SharePoint-hosted add-in (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814)
    
 
-  [<span data-ttu-id="f9443-276">Codebeispiel: Verwenden der domänenübergreifenden Bibliothek in einem mandantenbereichsbezogenen Add-In (REST)</span><span class="sxs-lookup"><span data-stu-id="f9443-276">Code sample: Use the cross-domain library in a tenant-scoped add-in (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e)
    
 
-  [<span data-ttu-id="f9443-277">Codebeispiel: Verwenden des Chromsteuerelements und der domänenübergreifenden Bibliothek (REST)</span><span class="sxs-lookup"><span data-stu-id="f9443-277">Code sample: Use the chrome control and the cross-domain library (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
    
 
-  [<span data-ttu-id="f9443-278">Codebeispiel: Verwenden des Chromsteuerelements und der domänenübergreifenden Bibliothek (JSOM)</span><span class="sxs-lookup"><span data-stu-id="f9443-278">Code sample: Use the chrome control and the cross-domain library (JSOM)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
    
 
-  [<span data-ttu-id="f9443-279">Codebeispiel: Verwenden von benutzerdefinierten Aktionen und der domänenübergreifenden Bibliothek zum Bestellen von Büchern</span><span class="sxs-lookup"><span data-stu-id="f9443-279">Code sample: Use custom actions and the cross-domain library to order books</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [<span data-ttu-id="f9443-280">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f9443-280">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f9443-281">Arbeiten mit der domänenübergreifenden Bibliothek in verschiedenen Internet Explorer-Sicherheitszonen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f9443-281">Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins</span></span>](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md)
    
 
-  [<span data-ttu-id="f9443-282">Erstellen einer benutzerdefinierten Proxyseite für die domänenübergreifende Bibliothek in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9443-282">Create a custom proxy page for the cross-domain library in SharePoint</span></span>](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f9443-283">Abfragen eines Remotediensts mithilfe des Webproxys in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9443-283">Query a remote service using the web proxy in SharePoint</span></span>](query-a-remote-service-using-the-web-proxy-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f9443-284">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f9443-284">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
    
 
