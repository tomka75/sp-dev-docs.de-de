

# <a name="use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins"></a><span data-ttu-id="af963-101">Verwenden des experimentellen Desktoplistenansicht-Widgets in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="af963-101">Use the experimental Desktop List View widget in SharePoint Add-ins</span></span>
<span data-ttu-id="af963-p101">Erfahren Sie, wie Sie das Desktoplistenansichts-Widget auf jeder Webseite verwenden, auch wenn die Seite nicht in SharePoint gehostet wird. Verwenden Sie das Listenansichts-Widget in Ihren Add-Ins, um Daten in Listen anzuzeigen, die in einer SharePoint-Website gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="af963-p101">Learn how to use the Desktop List View widget on any web page, even if the page is not hosted in SharePoint. Use the List View widget in your add-ins to display data in lists that are hosted in a SharePoint site.</span></span>
 

 <span data-ttu-id="af963-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="af963-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="af963-p103">**Hinweis** Die Office Web Widgets - Experimental werden nur zu Recherche- und Feedbackzwecken bereitgestellt. Verwenden Sie sie nicht in Produktionsszenarios. Das Verhalten von Office Web Widgets kann sich in künftigen Versionen erheblich ändern. Lesen und prüfen Sie die  [Lizenzbedingungen für Office Web Widgets - Experimental](office-web-widgets--experimental-license-terms).</span><span class="sxs-lookup"><span data-stu-id="af963-p103">**Note** The Office Web Widgets - Experimental are only provided for research and feedback purposes. Do not use in production scenarios. The Office Web Widgets behavior may change significantly in future releases. Read and review the  [Office Web Widgets - Experimental License Terms](office-web-widgets--experimental-license-terms).</span></span>
 


<span data-ttu-id="af963-111">Sie können das Listenansichts-Widget ähnlich dem herkömmlichen Listenansichts-Widget verwenden, um die Daten in einer SharePoint-Liste anzuzeigen. Der Unterschied ist, dass Sie es in Ihren Add-Ins und Websites verwenden können, die nicht unbedingt in SharePoint gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="af963-111">You can use the List View widget to display the data in a spnv list similar to the regular List View widget, but you can use it in your add-ins and websites that are not necessarily hosted in spnv.</span></span>
 


<span data-ttu-id="af963-112">**Abbildung 1: Desktoplistenansichts-Widget zeigt Daten in einer Liste an**</span><span class="sxs-lookup"><span data-stu-id="af963-112">**Figure 1. Desktop List View widget displaying data in a list**</span></span>

 

 
![Desktoplistenansicht – Experimentelles Steuerelement auf einer Seite](../../images/DesktopListView_basic.png)
 

 

 

## <a name="introduction"></a><span data-ttu-id="af963-114">Einführung</span><span class="sxs-lookup"><span data-stu-id="af963-114">Introduction</span></span>

<span data-ttu-id="af963-p104">Sie können die Ansicht in der SharePoint-Liste angeben, die Sie zum Anzeigen der Daten verwenden möchten. Das Listenansichts-Widget zeigt die Spalten und Elemente in der durch die Ansicht festgelegten Reihenfolge an.</span><span class="sxs-lookup"><span data-stu-id="af963-p104">You can specify the view in the SharePoint list that you want to use to display the data. The List View widget displays the columns and items in the order specified by the view.</span></span>
 

 
<span data-ttu-id="af963-p105">Das Listenansichts-Widget verwendet die domänenübergreifende Bibliothek, um die Listendaten abzurufen. Daher erfolgt die Kommunikation auf der Clientebene.</span><span class="sxs-lookup"><span data-stu-id="af963-p105">The List View widget uses the cross-domain library to get the list data. For this reason, communication happens at the client level.</span></span>
 

 

 <span data-ttu-id="af963-119">**Vorsicht** Das Desktoplistenansichts-Widget ermöglicht nicht alle Szenarios der nativen Listenansicht.</span><span class="sxs-lookup"><span data-stu-id="af963-119">**Caution** The Desktop List View widget doesn't enable all the scenarios of the native List View.</span></span>
 

<span data-ttu-id="af963-120">Die folgenden Szenarios wurden in der aktuellen Version des Widgets nicht aktiviert:</span><span class="sxs-lookup"><span data-stu-id="af963-120">The following scenarios have not been enabled in the current version of the widget:</span></span>
 

 

- <span data-ttu-id="af963-121">Verwenden des Widgets in Authentifizierungsschemas, die von der domänenübergreifenden Bibliothek nicht nativ unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="af963-121">Use the widget on authentication schemes that aren't natively supported by the cross-domain library.</span></span>
    
 
- <span data-ttu-id="af963-122">Verwenden des Widgets mit anderen Datenquellen als SharePoint-Listen oder -Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="af963-122">Use the widget with data sources other than SharePoint lists or libraries.</span></span>
    
 
- <span data-ttu-id="af963-123">Herstellen einer Datenbindung mit dem Widget.</span><span class="sxs-lookup"><span data-stu-id="af963-123">Data bind the widget.</span></span>
    
 
- <span data-ttu-id="af963-124">Ansichten mit Toucheingabe.</span><span class="sxs-lookup"><span data-stu-id="af963-124">User touch-friendly views.</span></span>
    
 
- <span data-ttu-id="af963-125">Inlinebearbeitung für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="af963-125">User inline-editing.</span></span>
    
 
- <span data-ttu-id="af963-126">Anzeigen von Anwesenheitsinformationen.</span><span class="sxs-lookup"><span data-stu-id="af963-126">Show presence information.</span></span>
    
 
- <span data-ttu-id="af963-127">Bereitstellen benutzerdefinierter Wiedergabevorlagen.</span><span class="sxs-lookup"><span data-stu-id="af963-127">Provide custom rendering templates.</span></span>
    
 
- <span data-ttu-id="af963-p106">Lokale Szenarios. Derzeit kann das Widget nur in SharePoint Online verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="af963-p106">On-premises scenarios. At this moment, the widget only works on SharePoint Online.</span></span>
    
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="af963-130">Voraussetzungen für die Verwendung der Beispiele in diesem Artikel</span><span class="sxs-lookup"><span data-stu-id="af963-130">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="af963-131">Um diese Beispiele auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="af963-131">To follow the examples in this article, you need the following:</span></span>
 

 

- <span data-ttu-id="af963-132">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="af963-132">Visual Studio 2013</span></span>
    
 
- <span data-ttu-id="af963-p107">NuGet-Paket-Manager. Weitere Informationen finden Sie unter [Installieren von NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span><span class="sxs-lookup"><span data-stu-id="af963-p107">NuGet Package Manager. For more information, see  [Installing NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span></span>
    
 
- <span data-ttu-id="af963-135">Eine SharePoint-Entwicklungsumgebung (für lokale Szenarios App-Isolierung erforderlich).</span><span class="sxs-lookup"><span data-stu-id="af963-135">A SharePoint development environment (app isolation required for on-premises scenarios).</span></span> 
    
 
- <span data-ttu-id="af963-p108">Office Web Widgets - Experimental - NuGet-Paket. Weitere Informationen dazu, wie Sie ein NuGet-Paket installieren, finden Sie unter  [Verwalten von NuGet-Paketen mithilfe des Dialogfelds](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). Sie können auch die  [NuGet-Galerieseite](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/) durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="af963-p108">Office Web Widgets - Experimental NuGet package. For more information about how to install a NuGet package, see  [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). You can also browse the  [NuGet gallery page](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
    
 

## <a name="use-the-desktop-list-view-widget-in-a-provider-hosted-sharepoint-add-in"></a><span data-ttu-id="af963-139">Verwenden des Desktoplistenansichts-Widgets in einem vom Anbieter gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="af963-139">Use the Desktop List View widget in a provider-hosted SharePoint Add-in</span></span>

<span data-ttu-id="af963-140">Dieses Beispiel enthält eine einfache Seite, die außerhalb von SharePoint gehostet wird und ein Desktoplistenansichts-Widget deklariert.</span><span class="sxs-lookup"><span data-stu-id="af963-140">In this example, there is a simple page hosted outside of SharePoint that declares a Desktop List View widget.</span></span>
 

 
<span data-ttu-id="af963-141">Sie müssen Folgendes tun, um das Listenansichts-Widget zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="af963-141">To use the List View widget, you must do the following:</span></span>
 

 

- <span data-ttu-id="af963-142">Erstellen Sie SharePoint-Add-In- und Webprojekte.</span><span class="sxs-lookup"><span data-stu-id="af963-142">Create SharePoint Add-in and web projects.</span></span>
    
 
- <span data-ttu-id="af963-p109">Erstellen Sie im Add-In-Web eine Liste. Mit diesem Schritt wird außerdem sichergestellt, dass ein Add-In-Web erstellt wird, wenn Benutzer das Add-In bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="af963-p109">Create a list on the add-in web. This step also ensures that an add-in web is created when users deploy the add-in.</span></span>
    
     <span data-ttu-id="af963-p110">**Hinweis** Für die domänenübergreifende Bibliothek muss ein Add-Ins-Web vorhanden sein. Das Listenansichts-Widget kommuniziert mit SharePoint mithilfe der domänenübergreifenden Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="af963-p110">**Note** The cross-domain library requires the existence of an add-in web. The List View widget communicates with SharePoint by using the cross-domain library.</span></span>
- <span data-ttu-id="af963-147">Erstellen Sie eine Add-In-Seite, die mithilfe von HTML-Markup eine Listenansichts-Widget-Instanz deklariert.</span><span class="sxs-lookup"><span data-stu-id="af963-147">Create an add-in page that declares a List View widget instance using HTML markup.</span></span>
    
 

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="af963-148">So erstellen Sie ein SharePoint-Add-In und Webprojekte</span><span class="sxs-lookup"><span data-stu-id="af963-148">To create a SharePoint Add-in and web projects</span></span>


1. <span data-ttu-id="af963-p111">Öffnen Sie Visual Studio 2013 als Administrator. (Wählen Sie dazu im Menü **Start** das Symbol für Visual Studio 2013 aus, und wählen Sie **Als Administrator ausführen** aus.)</span><span class="sxs-lookup"><span data-stu-id="af963-p111">Open Visual Studio 2013 as administrator. (To do this, choose the Visual Studio 2013 icon on the **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="af963-p112">Erstellen Sie mithilfe der SharePoint-Add-In 2013-Vorlage ein neues Projekt. Die **SharePoint-Add-In 2013**-Vorlage befindet sich unter **Vorlagen**> **Visual C#**, **Office/SharePoint**> **Add-Ins**.</span><span class="sxs-lookup"><span data-stu-id="af963-p112">Create a new project using the **SharePoint Add-in 2013** template. The SharePoint Add-in 2013 template is located under **Templates**> **Visual C#**, **Office/SharePoint**> **Add-ins**.</span></span>
    
 
3. <span data-ttu-id="af963-153">Geben Sie die URL der SharePoint-Website an, die Sie für das Debugging verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="af963-153">Provide the SharePoint website URL that you want to use for debugging.</span></span>
    
 
4. <span data-ttu-id="af963-154">Wählen Sie als Hostingoption für Ihr Add-In **Von Anbieter gehostet** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-154">Select **Provider-hosted** as the hosting option for your add-in.</span></span>
    
     <span data-ttu-id="af963-155">**Hinweis** Sie können das Desktoplistenansichts-Widget auch mit anderen Hostingoptionen oder sogar mit Add-Ins für Office oder Ihrer eigenen Website verwenden.</span><span class="sxs-lookup"><span data-stu-id="af963-155">**Note** You can also use the Desktop List View widget with other hosting options or even with Office Add-ins or your own website.</span></span>
5. <span data-ttu-id="af963-156">Wählen Sie als Typ des Webanwendungsprojekts **ASP.NET Webformular-Anwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-156">Select **ASP.NET Web Forms Application** as the type of web application project.</span></span>
    
 
6. <span data-ttu-id="af963-157">Wählen Sie als Authentifizierungsoption **Windows Azure-Zugriffssteuerungsdienst** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-157">Select **Windows Azure Access Control Service** as the authentication option.</span></span>
    
 

### <a name="to-create-a-list-on-the-add-in-web"></a><span data-ttu-id="af963-158">So erstellen Sie eine Liste im Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="af963-158">To create a list on the add-in web</span></span>


1. <span data-ttu-id="af963-p113">Wählen Sie das SharePoint-Add-In-Projekt im **Projektmappen-Explorer** aus. Wählen Sie **Hinzufügen**> **Neues Element** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-p113">Choose the SharePoint Add-in project in **Solution Explorer**. Choose **Add**> **New Item…**</span></span>
    
 
2. <span data-ttu-id="af963-p114">Wählen Sie **Visual C#-Elemente**> **Office/SharePoint**> **Liste** aus. Geben Sie im Textfeld **Name****Ankündigungen** ein. Wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-p114">Choose **Visual C# Items**> **Office/SharePoint**> **List**. Type **Announcements** in the **Name** textbox. Choose **Add**.</span></span>
    
 
3. <span data-ttu-id="af963-p115">Wählen Sie **Listeninstanz basierend auf einer bestehenden Listenvorlage erstellen** aus. Wählen Sie die Vorlage **Ankündigungen** aus. Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-p115">Choose **Create a list instance based on an existing list template**.Choose the **Announcements** template. Choose **Finish**.</span></span>
    
 

### <a name="to-add-a-new-page-that-uses-the-desktop-list-view-widget"></a><span data-ttu-id="af963-166">So fügen Sie eine neue Seite hinzu, die das Desktoplistenansichts-Widget verwendet</span><span class="sxs-lookup"><span data-stu-id="af963-166">To add a new page that uses the Desktop List View widget</span></span>


1. <span data-ttu-id="af963-167">Wählen Sie im **Projektmappen-Explorer** im Webprojekt den Ordner **Seiten** aus.</span><span class="sxs-lookup"><span data-stu-id="af963-167">Choose the **Pages** folder in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="af963-p116">Kopieren Sie den folgenden Code, und fügen Sie ihn in eine **ASPX** -Datei im Projekt ein. Der Code führt die folgenden Aufgaben durch:</span><span class="sxs-lookup"><span data-stu-id="af963-p116">Copy the following code and paste it in an **ASPX** file in the project. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="af963-170">Fügt Referenzen zu den erforderlichen Office-Bibliotheken und -Ressourcen hinzu.</span><span class="sxs-lookup"><span data-stu-id="af963-170">Adds references to the required Office libraries and resources.</span></span>
    
 
  - <span data-ttu-id="af963-171">Stellt einen Platzhalter für das Listenansichts-Widget bereit.</span><span class="sxs-lookup"><span data-stu-id="af963-171">Provides a placeholder for the List View widget.</span></span>
    
 
  - <span data-ttu-id="af963-172">Initialisiert die Steuerelementelaufzeit.</span><span class="sxs-lookup"><span data-stu-id="af963-172">Initializes the controls runtime.</span></span>
    
 
  - <span data-ttu-id="af963-173">Führt die Methode **renderAll** der Office-Steuerelementelaufzeit aus.</span><span class="sxs-lookup"><span data-stu-id="af963-173">Runs the **renderAll** method of the Office Controls runtime.</span></span>
    
 

```
  <!DOCTYPE html>
<html>
<head>
    <!-- IE9 or superior -->
    <meta http-equiv="x-ua-compatible" content="IE=10">
    <title>Desktop List View HTML Markup</title>

    <!-- Controls Specific CSS File -->
    <link rel="stylesheet" type="text/css" href="/Scripts/Office.Controls.css" />

    <!-- Ajax, jQuery, and utils -->
    <script 
        src=" https://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js.js">
    </script>
    <script 
        src=" https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js">
    </script>
    <script type="text/javascript">

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

    <!-- Cross-Domain Library and Office controls runtime -->
    <script type="text/javascript">
        //Register namespace and variables used through the sample
        Type.registerNamespace("Office.Samples.ListViewBasic");
        //Retrieve context tokens from the querystring
        Office.Samples.ListViewBasic.appWebUrl =
            decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
        Office.Samples.ListViewBasic.hostWebUrl =
            decodeURIComponent(getQueryStringParameter("SPHostUrl"));
        Office.Samples.ListViewBasic.ctag =
            decodeURIComponent(getQueryStringParameter("SPClientTag"));

        //Pattern to dynamically load JSOM and the cross-domain library
        var scriptbase =
            Office.Samples.ListViewBasic.hostWebUrl + "/_layouts/15/";

        //Get the cross-domain library
        $.getScript(scriptbase + "SP.RequestExecutor.js", 
            //Get the Office controls runtime and 
            //  continue to the createControl function
            function () {
                $.getScript("../Scripts/Office.Controls.js", createControl);
            }
        );
    </script>

    <!-- List View -->
    <script 
        src="../Scripts/Office.Controls.ListView.debug.js" 
        type="text/javascript">
    </script>

    <!-- SharePoint CSS -->
    <script type="text/javascript">
        document.addEventListener("DOMContentLoaded", function () {
            // The resource files are in a URL in the form:
            // web_url/_layouts/15/Resource.ashx
            var scriptbase =
                Office.Samples.ListViewBasic.appWebUrl + "/_layouts/15/";

            // Dynamically create the invisible iframe.
            var blankiframe;
            var blankurl;
            var body;
            blankurl =
                Office.Samples.ListViewBasic.appWebUrl + "/Pages/blank.html";
            blankiframe = document.createElement("iframe");
            blankiframe.setAttribute("src", blankurl);
            blankiframe.setAttribute("style", "display: none");
            body = document.getElementsByTagName("body");
            body[0].appendChild(blankiframe);

            // Dynamically create the link element.
            var dclink;
            var head;
            dclink = document.createElement("link");
            dclink.setAttribute("rel", "stylesheet");
            dclink.setAttribute("href",
                                scriptbase +
                                "defaultcss.ashx?ctag=" +
                                Office.Samples.ListViewBasic.ctag
                                );
            head = document.getElementsByTagName("head");
            head[0].appendChild(dclink);
        }, false);
    </script>
</head>
<body>
    Basic List View sample (HTML markup declaration):
    <div id="ListViewDiv"
         data-office-control="Office.Controls.ListView"
         data-office-options='{"listUrl" : getListUrl()}'>
    </div>

    <script type="text/javascript">
        function createControl() {
            //Initialize Controls Runtime
            Office.Controls.Runtime.initialize({
                sharePointHostUrl: Office.Samples.ListViewBasic.hostWebUrl,
                appWebUrl: Office.Samples.ListViewBasic.appWebUrl
            });

            //Render the widget, this must be executed after the
            //placeholder DOM is loaded
            Office.Controls.Runtime.renderAll();
        }

        function getListUrl() {
            return Office.Samples.ListViewBasic.appWebUrl +
                    "/_api/web/lists/getbytitle('Announcements')";
        }
    </script>
</body>
</html>
```


 <span data-ttu-id="af963-p117">**Hinweis** Das obige Codebeispiel gibt die URLs des Hostwebs und des Add-In-Webs explizit an, um die Office-Steuerelementelaufzeit zu initialisieren. Wenn die URLs des Hostwebs und des Add-In-Webs allerdings im Abfragezeichenfolgenparameter **SPAppWebUrl** bzw. **SPHostUrl** angegeben werden, können Sie ein leeres Objekt übergeben. Der Code wird dann versuchen, die Parameter automatisch abzurufen. Die Parameter **SPAppWebUrl** und **SPHostUrl** sind in der Abfragezeichenfolge enthalten, wenn Sie das Token **{StandardTokens}** verwenden.</span><span class="sxs-lookup"><span data-stu-id="af963-p117">**Note** The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime. However, if the add-in web and host web URLs are specified in the **SPAppWebUrl** and **SPHostUrl** query string parameters, respectively; you can pass an empty object and the code will attempt to get the parameters automatically. The **SPAppWebUrl** and **SPHostUrl** parameters are included in the query string when you use the **{StandardTokens}** token.</span></span>
 

<span data-ttu-id="af963-177">Das folgende Beispiel zeigt, wie Sie ein leeres Objekt übergeben, um die Methode zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="af963-177">The following example shows you how to pass an empty object to the initialize method:</span></span>
 

 



```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="af963-178">So erstellen Sie die Lösung und führen sie aus</span><span class="sxs-lookup"><span data-stu-id="af963-178">To build and run the solution</span></span>


1. <span data-ttu-id="af963-179">Drücken Sie F5.</span><span class="sxs-lookup"><span data-stu-id="af963-179">Press the F5 key.</span></span>
    
     <span data-ttu-id="af963-180">**Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.</span><span class="sxs-lookup"><span data-stu-id="af963-180">**Note** When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="af963-181">Klicken Sie auf die Schaltfläche **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="af963-181">Choose the **Trust It** button.</span></span>
    
 
3. <span data-ttu-id="af963-182">Wählen Sie auf der Seite **Websiteinhalte** das Add-In-Symbol.</span><span class="sxs-lookup"><span data-stu-id="af963-182">Choose the add-in icon on the **Site Contents** page.</span></span>
    
 
<span data-ttu-id="af963-183">Sie können dieses Beispiel auch in der Codegalerie herunterladen: siehe [Codebeispiel Verwenden des experimentellen Desktoplistenansichts-Widgets in einem Add-In](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="af963-183">You can also download this sample from code gallery, see the  [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076) code sample.</span></span>
 

 

## 

<span data-ttu-id="af963-p118">In diesem Artikel wird gezeigt, wie Sie das Desktoplistenansichts-Widget in Ihrem Add-In mithilfe von HTML verwenden. Sie können sich auch mit den folgenden Szenarios und Details zum Widget vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="af963-p118">This article shows how to use the Desktop List View widget in your add-in by using HTML. You can also explore the following scenarios and details about the widget.</span></span>
 

 

### <a name="use-javascript-to-declare-the-desktop-list-view-widget"></a><span data-ttu-id="af963-186">Verwenden von JavaScript zum Deklarieren des Desktoplistenansichts-Widgets</span><span class="sxs-lookup"><span data-stu-id="af963-186">Use JavaScript to declare the Desktop List View widget</span></span>

<span data-ttu-id="af963-p119">Möglicherweise verwenden Sie zum Deklarieren des Widgets anstatt HTML lieber das JavaScript. Ist dies der Fall, können Sie das folgende Markup als Platzhalter für das Widget verwenden.</span><span class="sxs-lookup"><span data-stu-id="af963-p119">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span>
 

 

```HTML
<div id="ListViewDiv"></div>
```

<span data-ttu-id="af963-189">Verwenden Sie den folgenden JavaScript-Code, um die Listenansicht zu instanziieren.</span><span class="sxs-lookup"><span data-stu-id="af963-189">Use the following JavaScript code to instantiate the List View.</span></span>
 

 



```
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: Office.Samples.ListViewBasic.appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
    });
```

<span data-ttu-id="af963-190">Ein Beispiel dafür, wie die Aufgaben durchgeführt werden, finden Sie auf der Seite **JSSimple.html** im Codebeispiel [Verwenden des experimentellen Desktoplistenansichts-Widgets in einem Add-In](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="af963-190">For an example that shows how to perform the tasks, see the **JSSimple.html** page in the [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076) code sample.</span></span>
 

 

### <a name="specify-a-view-to-display-the-data"></a><span data-ttu-id="af963-191">Festlegen einer Ansicht zur Anzeige der Daten</span><span class="sxs-lookup"><span data-stu-id="af963-191">Specify a view to display the data</span></span>

<span data-ttu-id="af963-192">Sie können in Ihrer SharePoint-Liste eine vorhandene Ansicht festlegen, die das Listenansichts-Widget dann zur Anzeige der Daten verwendet.</span><span class="sxs-lookup"><span data-stu-id="af963-192">You can specify an existent view in your SharePoint list, the List View widget displays the data using the view specification.</span></span>
 

 
<span data-ttu-id="af963-193">Wenn Sie zum Deklarieren des Widgets HTML-Markup verwenden, können Sie zum Festlegen einer Ansicht die folgende Syntax verwenden.</span><span class="sxs-lookup"><span data-stu-id="af963-193">If you're using HTML markup to declare the widget, you can use the following syntax to specify a view.</span></span>
 

 



```
<div id="ListViewDiv"
        data-office-control="Office.Controls.ListView"
        data-office-options="{listUrl: 'list URL',
                            viewID: 'GUID'
                            }">
</div> 

```

<span data-ttu-id="af963-194">Wenn Sie das Widget mit JavaScript deklarieren, verwenden Sie zum Festlegen einer Ansicht die folgende Syntax.</span><span class="sxs-lookup"><span data-stu-id="af963-194">If you're declaring the widget using JavaScript, use the following syntax to specify a view.</span></span>
 

 



```
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: "list URL",
        viewID: "GUID"
    });
```


## <a name="conclusion"></a><span data-ttu-id="af963-195">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="af963-195">Conclusion</span></span>

<span data-ttu-id="af963-p120">Sie können das experimentelle Desktoplistenansichts-Widget zum Anzeigen von Daten in SharePoint-Listen verwenden. Das Widget zeigt Daten im schreibgeschützten Modus an. Wir freuen uns über Ihre Ideen und Kommentare auf der  [Office Developer Platform UserVoice-Website](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="af963-p120">You can use the experimental Desktop List View widget to display data in SharePoint lists. The widget displays data in read-only mode. Please provide ideas and comments in the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="af963-199">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="af963-199">Additional resources</span></span>
<span data-ttu-id="af963-200"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="af963-200"></span></span>


-  [<span data-ttu-id="af963-201">Übersicht über Office Web Widgets – Experimental</span><span class="sxs-lookup"><span data-stu-id="af963-201">Office Web Widgets - Experimental overview</span></span>](office-web-widgets--experimental-overview)
    
 
-  [<span data-ttu-id="af963-202">Lizenzbedingungen für Office Web Widgets - Experimental</span><span class="sxs-lookup"><span data-stu-id="af963-202">Office Web Widgets - Experimental License Terms</span></span>](office-web-widgets--experimental-license-terms)
    
 
-  [<span data-ttu-id="af963-203">Office Web Widgets - Experimental – NuGet-Galerieseite</span><span class="sxs-lookup"><span data-stu-id="af963-203">Office Web Widgets - Experimental NuGet gallery page</span></span>](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/)
    
 
-  [<span data-ttu-id="af963-204">Codebeispiel: Verwenden des experimentellen Desktoplistenansichts-Widgets in einem Add-In</span><span class="sxs-lookup"><span data-stu-id="af963-204">Code sample: Use the Desktop List View experimental widget in an add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076)
    
 
-  <span data-ttu-id="af963-205">[Verwenden des experimentellen Desktoplistenansichts-Widgets in SharePoint-Add-Ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins)</span><span class="sxs-lookup"><span data-stu-id="af963-205">[Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins).</span></span>
    
 

