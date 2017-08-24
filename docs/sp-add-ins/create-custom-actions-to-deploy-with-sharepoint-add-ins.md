# <a name="create-custom-actions-to-deploy-with-sharepoint-add-ins"></a><span data-ttu-id="12327-101">Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-101">Create custom actions to deploy with SharePoint Add-ins</span></span>
<span data-ttu-id="12327-102">In diesem Artikel erfahren Sie, wie Sie eine benutzerdefinierte Aktion in SharePoint erstellen, die für das Hostweb bereitgestellt wird, wenn Sie ein SharePoint-Add-In bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="12327-102">Learn how to create a custom action in SharePoint that deploys to the host web when you deploy an SharePoint Add-in.</span></span>
 

 <span data-ttu-id="12327-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="12327-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="12327-p102">Wenn Sie ein SharePoint-Add-In erstellen, ermöglichen Ihnen benutzerdefinierte Aktionen die Interaktion mit den Listen und dem Menüband im Hostweb. Eine benutzerdefinierte Aktion wird für das Hostweb bereitgestellt, wenn Endbenutzer Ihr Add-In installieren. Mithilfe benutzerdefinierter Aktionen ist es möglich, eine Remotewebseite zu öffnen und über die Abfragezeichenfolge Informationen zu übergeben. Es sind zwei Typen von benutzerdefinierten Aktionen für Add-Ins verfügbar: benutzerdefinierte Aktionen für das Menüband und für Menüelemente.</span><span class="sxs-lookup"><span data-stu-id="12327-p102">When you are creating a spappsing, custom actions let you interact with the lists and the ribbon in the host web. A custom action deploys to the host web when end users install your add-in. Custom actions can open a remote webpage and pass information through the query string. There are two types of custom actions available for add-ins: Ribbon and Menu Item custom actions.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="12327-110">Voraussetzungen für die Verwendung der Beispiele in diesem Artikel</span><span class="sxs-lookup"><span data-stu-id="12327-110">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="12327-111"><a name="SP15Createcustomactionsapps_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="12327-111"></span></span>

<span data-ttu-id="12327-112">Sie benötigen eine Entwicklungsumgebung, wie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins) erläutert.</span><span class="sxs-lookup"><span data-stu-id="12327-112">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span></span>
 

 

### <a name="core-concepts-to-help-you-understand-custom-actions"></a><span data-ttu-id="12327-113">Kernkonzepte für ein besseres Verständnis von benutzerdefinierten Aktionen</span><span class="sxs-lookup"><span data-stu-id="12327-113">Core concepts to help you understand custom actions</span></span>

<span data-ttu-id="12327-114">In der folgenden Tabelle sind hilfreiche Artikel aufgeführt, die ein besseres Verständnis der Konzepte und Schritte bei einem Szenarium mit benutzerdefinierten Aktionen ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="12327-114">The following table lists useful articles that can help you understand the concepts and steps that are involved in a custom action scenario.</span></span>
 

 

<span data-ttu-id="12327-115">**Tabelle 1. Kernkonzepte für benutzerdefinierte Aktionen**</span><span class="sxs-lookup"><span data-stu-id="12327-115">**Table 1. Core concepts for custom actions**</span></span>


|<span data-ttu-id="12327-116">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="12327-116">**Article**</span></span>|<span data-ttu-id="12327-117">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="12327-117">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="12327-118">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-118">SharePoint Add-ins</span></span>](sharepoint-add-ins)|<span data-ttu-id="12327-119">Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="12327-119">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="12327-120">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-120">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins)|<span data-ttu-id="12327-121">Hier erfahren Sie mehr über die UX-Optionen (User eXperience, Benutzerumgebung) beim Erstellen von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="12327-121">Learn about the user experience (UX) options that you have when you are building SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="12327-122">Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="12327-122">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|<span data-ttu-id="12327-p103">Hier erhalten Sie Informationen über den Unterschied zwischen einem Hostweb und einem Add-In-Web. Außerdem erfahren Sie, welche SharePoint-Komponenten in ein SharePoint-Add-In eingeschlossen werden können, welche Komponenten für das Hostweb bereitgestellt werden, welche Komponenten für das Add-In-Web bereitgestellt werden, und wie das Add-In-Web in einer isolierten Domäne bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="12327-p103">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|

## <a name="code-example-create-a-custom-action-in-the-host-web-document-libraries"></a><span data-ttu-id="12327-125">Codebeispiel: Erstellen einer benutzerdefinierten Aktion in den Hostweb-Dokumentbibliotheken</span><span class="sxs-lookup"><span data-stu-id="12327-125">Code example: Create a custom action in the host web document libraries</span></span>
<span data-ttu-id="12327-126"><a name="SP15Createcustomactionsapps_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="12327-126"></span></span>

<span data-ttu-id="12327-127">Führen Sie diese Schritte aus, um eine benutzerdefinierte Aktion in den Hostweb-Dokumentbibliotheken zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="12327-127">Follow these steps to create a custom action in the host web document libraries:</span></span>
 

 

1. <span data-ttu-id="12327-128">Erstellen Sie die SharePoint-Add-In- und Remotewebprojekte.</span><span class="sxs-lookup"><span data-stu-id="12327-128">Create the SharePoint Add-in and remote web projects.</span></span>
    
 
2. <span data-ttu-id="12327-129">Fügen Sie dem SharePoint-Add-In-Projekt ein benutzerdefiniertes Feature hinzu.</span><span class="sxs-lookup"><span data-stu-id="12327-129">Add a custom action feature to the SharePoint Add-in project.</span></span>
    
 
3. <span data-ttu-id="12327-130">Fügen Sie dem Webprojekt eine Add-In-Webseite hinzu.</span><span class="sxs-lookup"><span data-stu-id="12327-130">Add an add-in webpage to the web project.</span></span>
    
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a><span data-ttu-id="12327-131">So erstellen Sie die Projekte für das SharePoint-Add-In und das Remoteweb</span><span class="sxs-lookup"><span data-stu-id="12327-131">To create the SharePoint Add-in and remote web projects</span></span>


1. <span data-ttu-id="12327-p104">Öffnen Sie Visual Studio als Administrator. (Klicken Sie dazu im Menü **Start** mit der rechten Maustaste auf das Visual Studio-Symbol, und wählen Sie **Als Administrator ausführen** aus.)</span><span class="sxs-lookup"><span data-stu-id="12327-p104">Open Visual Studio as administrator. (To do this, right-click the Visual Studio icon on the **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="12327-134">Erstellen Sie das vom Anbieter gehostete SharePoint-Add-In wie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins) erläutert, und nennen Sie es „itCustomActionsApp“.</span><span class="sxs-lookup"><span data-stu-id="12327-134">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins) and name itCustomActionsApp.</span></span> 
    
 

### <a name="to-add-an-add-in-webpage-for-the-custom-actions"></a><span data-ttu-id="12327-135">So fügen Sie eine Add-In-Webseite für die benutzerdefinierten Aktionen hinzu</span><span class="sxs-lookup"><span data-stu-id="12327-135">To add an add-in webpage for the custom actions</span></span>


1. <span data-ttu-id="12327-p105">Klicken Sie nach dem Erstellen der Visual Studio-Lösung mit der rechten Maustaste auf das Webanwendungsprojekt (nicht das SharePoint-Add-In-Projekt), und fügen Sie ein neues Webformular hinzu, indem Sie **Hinzufügen** > **Neues Element** > **Web** > **Webformular** auswählen. Geben Sie dem Formular den Namen „CustomActionTarget.aspx“.</span><span class="sxs-lookup"><span data-stu-id="12327-p105">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing **Add** > **New Item** > **Web** > **Web Form**. Name the form CustomActionTarget.aspx.</span></span>
    
 
2. <span data-ttu-id="12327-p106">Ersetzen Sie in der Datei CustomActionTarget.aspx das gesamte **html**-Element und seine untergeordneten Elemente durch den folgenden HTML-Code. Behalten Sie das gesamte Markup oberhalb des **html**-Elements wie vorhanden bei. Der HTML-Code enthält JavaScript, das die folgenden Aufgaben durchführt:</span><span class="sxs-lookup"><span data-stu-id="12327-p106">In the CustomActionTarget.aspx file, replace the entire **html** element and it's children with the following HTML code. Leave all the markup above the **html** element as it is. The HTML code contains JavaScript that performs the following tasks:</span></span>
    
      - <span data-ttu-id="12327-141">Bereitstellung eines Platzhalters für die Parameter der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="12327-141">Provides a placeholder for the query string parameters.</span></span>
    
 
  - <span data-ttu-id="12327-142">Extrahieren der Parameter aus der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="12327-142">Extracts the parameters from the query string.</span></span>
    
 
  - <span data-ttu-id="12327-143">Rendern der Parameter im Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="12327-143">Renders the parameters in the placeholder.</span></span>
    
 

     <span data-ttu-id="12327-p107">**Wichtig** Die Token „ItemURL“ und „ItemID“ werden nur übergeben, wenn ein Element ausgewählt ist. In einem SharePoint-Add-In mit Produktionsqualität muss Ihr Code Situationen, in denen kein Element ausgewählt ist, verarbeiten können. In diesem Beispiel warnt der Code den Benutzer, dass kein Element ausgewählt wurde.</span><span class="sxs-lookup"><span data-stu-id="12327-p107">**Important** The ItemURL and ItemID tokens only get passed when there is an item selected. In a production quality SharePoint Add-in, your code needs to handle situations where no item is selected. In this example the code alerts the user that no item has been selected.</span></span> 

```HTML
  <html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Custom action target</title>
</head>
<body>
    <h2>Query string parameters passed by the custom action:</h2>

    <!-- Placeholder for query string parameters -->
    <ul id="qsparams"/>

    <!-- Main JavaScript function, renders
         the query string parameters -->
    <script lang="javascript">
        var params = document.URL.split("?")[1].split("&amp;");
        var paramsHTML = "";
      
        // Extracts the parameters from the query string.
        // Parameters are URLencoded, decode for rendering
        // in page.
        for (var i = 0; i < params.length; i = i + 1) {
            params[i] = decodeURIComponent(params[i]);
            paramsHTML += "<li>" + params[i] + "</li>";
        }

         // Alert the user when no item has been selected.
         // (The SPListItemId is the 5th parameter.)
         if (params[5] === undefined) {
            paramsHTML += "<div> <h3> No item has been selected from the list.  Please select an item. </h3> </div> ";
         }

        // Render parameters in the placeholder.
        document.getElementById("qsparams").innerHTML =
            paramsHTML;
    </script>
</body>
</html>
```


### <a name="to-add-a-menu-item-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="12327-147">So fügen Sie dem SharePoint-Add-In-Projekt eine benutzerdefinierte Menüelementaktion hinzu</span><span class="sxs-lookup"><span data-stu-id="12327-147">To add a menu item custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="12327-148">Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menüelementaktion** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-148">Right-click the SharePoint Add-in project, and choose **Add** > **New Item** > **Office/SharePoint** > **Menu Item Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="12327-149">Übernehmen Sie den Standardnamen, und wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-149">Keep the default name and choose **Add**.</span></span>
    
 
3. <span data-ttu-id="12327-p108">Der Assistent **Benutzerdefinierte Aktion für ein Menüelement erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:</span><span class="sxs-lookup"><span data-stu-id="12327-p108">The **Create Custom Action for Menu Item** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="12327-152">**Tabelle 2. Eigenschaften der benutzerdefinierten Menüelementaktion**</span><span class="sxs-lookup"><span data-stu-id="12327-152">**Table 2. Menu Item custom action properties**</span></span>


|<span data-ttu-id="12327-153">**Frage zur Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="12327-153">**Property question**</span></span>|<span data-ttu-id="12327-154">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="12327-154">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="12327-155">Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?</span><span class="sxs-lookup"><span data-stu-id="12327-155">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="12327-156">Wählen Sie **Hostweb**.</span><span class="sxs-lookup"><span data-stu-id="12327-156">Choose **Host Web**.</span></span>|
|<span data-ttu-id="12327-157">Wo gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-157">Where is the custom action scoped to?</span></span>|<span data-ttu-id="12327-158">Wählen Sie **Listenvorlage**.</span><span class="sxs-lookup"><span data-stu-id="12327-158">Choose **List Template**.</span></span>|
|<span data-ttu-id="12327-159">Für welches spezielle Element gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-159">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="12327-160">Wählen Sie **Dokumentbibliothek**.</span><span class="sxs-lookup"><span data-stu-id="12327-160">Choose **Document Library**.</span></span>|
|<span data-ttu-id="12327-161">Wie lautet der Text im Menüelement?</span><span class="sxs-lookup"><span data-stu-id="12327-161">What is the text on the menu item?</span></span>|<span data-ttu-id="12327-162">Geben Sie **Meine benutzerdefinierte Aktion** ein.</span><span class="sxs-lookup"><span data-stu-id="12327-162">Type **My Custom Action**.</span></span>|
|<span data-ttu-id="12327-163">Wohin navigiert die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-163">Where does the custom action navigate to?</span></span>|<span data-ttu-id="12327-164">Wählen Sie die Seite **CustomActionAppWeb\CustomActionTarget.aspx** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-164">Choose the CustomActionAppWeb**CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="12327-165">Wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="12327-165">Choose **Finish**.</span></span>
    
    <span data-ttu-id="12327-166">Visual Studio generiert das folgende Markup in der Datei „elements.xml“ des Features für die benutzerdefinierte Menüelementaktion:</span><span class="sxs-lookup"><span data-stu-id="12327-166">Visual Studio generates the following markup in the elements.xml file of the menu item custom action feature:</span></span>
    


```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements 
    xmlns="http://schemas.microsoft.com/sharepoint/">
    <!-- RegistrationId attribute is the list type id,
        in this case, a document library (id=101). -->
  <CustomAction 
      Id="65695319-4784-478e-8dcd-4e541cb1d682.CustomAction"
      RegistrationType="List"
      RegistrationId="101"
      Location="EditControlBlock"
      Sequence="10001"
      Title="Invoke custom action">
    <!-- 
    Update the Url below to the page you want the custom action to use.
    Start the URL with the token ~remoteAppUrl if the page is in the
    associated web project, use ~appWebUrl if page is in the add-in project.
    -->
    <UrlAction Url=
"~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}" />
  </CustomAction>
</Elements>

```

5. <span data-ttu-id="12327-167">Fügen Sie die folgenden Abfrageparameter zum Ende des Attributs **Url** des Elements **UrlAction** hinzu:</span><span class="sxs-lookup"><span data-stu-id="12327-167">Add the following query parameters to the end of the **Url** attribute of the **UrlAction** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}`
    
    <span data-ttu-id="12327-168">Das Element **UrlAction** sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="12327-168">The **UrlAction** element should look like the following:</span></span>
    
     ` <UrlAction Url= "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}" />`
    
 

 <span data-ttu-id="12327-p109">**Hinweis** In diesem Beispiel wird die Remotewebseite in einem vollständigen Fenster geöffnet, wenn der Benutzer die benutzerdefinierte Aktion aus dem Menü auswählt. Benutzerdefinierte Menüaktionen können eine Remotewebseite auch in einem Dialogfeld öffnen, indem Sie das Attribut **HostWebDialog** verwenden. Weitere Informationen finden Sie unter [SharePoint-Add-In-Lokalisierung](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span><span class="sxs-lookup"><span data-stu-id="12327-p109">**Note** In this example, the remote web page opens in a full window when the user selects the custom action from the menu. Custom menu actions can also open a remote webpage in a dialog box by using the **HostWebDialog** attribute. For more information, see [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span></span>
 


### <a name="to-add-a-ribbon-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="12327-172">So fügen Sie dem SharePoint-Add-In-Projekt eine benutzerdefinierte Menübandaktion hinzu</span><span class="sxs-lookup"><span data-stu-id="12327-172">To add a Ribbon custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="12327-173">Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menübandaktion** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-173">Right-click the SharePoint Add-in project, and choose **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="12327-174">Übernehmen Sie den Standardnamen, und wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-174">Keep the default name and choose **Add**.</span></span>
    
 
3. <span data-ttu-id="12327-p110">Der Assistent **Benutzerdefinierte Aktion für das Menüband erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:</span><span class="sxs-lookup"><span data-stu-id="12327-p110">The **Create Custom Action for Ribbon** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="12327-177">**Tabelle 3. Eigenschaften der benutzerdefinierten Menübandaktion**</span><span class="sxs-lookup"><span data-stu-id="12327-177">**Table 3. Ribbon custom action properties**</span></span>


|<span data-ttu-id="12327-178">**Frage zur Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="12327-178">**Property question**</span></span>|<span data-ttu-id="12327-179">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="12327-179">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="12327-180">Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?</span><span class="sxs-lookup"><span data-stu-id="12327-180">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="12327-181">Wählen Sie **Hostweb**.</span><span class="sxs-lookup"><span data-stu-id="12327-181">Choose **Host Web**.</span></span>|
|<span data-ttu-id="12327-182">Wo gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-182">Where is the custom action scoped to?</span></span>|<span data-ttu-id="12327-183">Wählen Sie **Listenvorlage**.</span><span class="sxs-lookup"><span data-stu-id="12327-183">Choose **List Template**.</span></span>|
|<span data-ttu-id="12327-184">Für welches spezielle Element gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-184">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="12327-185">Wählen Sie **Dokumentbibliothek**.</span><span class="sxs-lookup"><span data-stu-id="12327-185">Choose **Document Library**.</span></span>|
|<span data-ttu-id="12327-186">Wo befindet sich das Steuerelement?</span><span class="sxs-lookup"><span data-stu-id="12327-186">Where is the control located?</span></span>|<span data-ttu-id="12327-187">Wählen Sie **Ribbon.Documents.Manage**.</span><span class="sxs-lookup"><span data-stu-id="12327-187">Choose **Ribbon.Documents.Manage**.</span></span>|
|<span data-ttu-id="12327-188">Wie lautet der Text im Menüelement?</span><span class="sxs-lookup"><span data-stu-id="12327-188">What is the text on the menu item?</span></span>|<span data-ttu-id="12327-189">Geben Sie **Meine benutzerdefinierte Menübandschaltfläche** ein.</span><span class="sxs-lookup"><span data-stu-id="12327-189">Type **My Custom Ribbon Button**.</span></span>|
|<span data-ttu-id="12327-190">Wohin navigiert die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="12327-190">Where does the custom action navigate to?</span></span>|<span data-ttu-id="12327-191">Wählen Sie die Seite **CustomActionAppWeb\CustomActionTarget.aspx** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-191">Choose the CustomActionAppWeb**CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="12327-192">Visual Studio generiert das folgende Markup in der Datei „elements.xml“ des Features für die benutzerdefinierte Menübandaktion:</span><span class="sxs-lookup"><span data-stu-id="12327-192">Visual Studio generates the following markup in the elements.xml file of the Ribbon custom action feature:</span></span>
    
```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="85691508-c076-4f43-93d4-96b4d5253a09.RibbonCustomAction1"
                RegistrationType="List"
                RegistrationId="101"
                Location="CommandUI.Ribbon"
                Sequence="10001"
                Title="Invoke &amp;apos;RibbonCustomAction1&amp;apos; action">
    <CommandUIExtension>
      <!-- 
      Update the UI definitions below with the controls and the command actions
      that you want to enable for the custom action.
      -->
      <CommandUIDefinitions>
        <CommandUIDefinition Location="Ribbon.Documents.Manage.Controls._children">
          <Button Id="Ribbon.Documents.Manage.RibbonCustomAction1Button"
                  Alt="My Custom Ribbon Button"
                  Sequence="100"
                  Command="Invoke_RibbonCustomAction1ButtonRequest"
                  LabelText="My Custom Ribbon Button"
                  TemplateAlias="o1"
                  Image32by32="_layouts/15/images/placeholder32x32.png"
                  Image16by16="_layouts/15/images/placeholder16x16.png" />
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest"
                          CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}"/>
      </CommandUIHandlers>
    </CommandUIExtension >
  </CustomAction>
</Elements> 

```

5. <span data-ttu-id="12327-193">Fügen Sie die folgenden Abfrageparameter zum Ende des Attributs **CommandAction** des Elements **CommandUIHandler** hinzu:</span><span class="sxs-lookup"><span data-stu-id="12327-193">Add the following query parameters to the end of the **CommandAction** attribute of the **CommandUIHandler** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}`
    
    <span data-ttu-id="12327-194">Das Element **CommandUIHandler** sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="12327-194">The **CommandUIHandler** element should look like the following:</span></span>
    
     ` <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest" CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}" />`
    
     <span data-ttu-id="12327-p111">**Hinweis** Benutzerdefinierte Menübandaktionen verwenden **SelectedListId** und **SelectedItemId**. **ListId** und **ItemId** werden nur mit benutzerdefinierten Menüelementaktionen verwendet.</span><span class="sxs-lookup"><span data-stu-id="12327-p111">**Note** Ribbon custom actions use **SelectedListId** and **SelectedItemId**. **ListId** and **ItemId** work only with menu item custom actions.</span></span>

### <a name="set-the-add-in-start-page-to-the-host-web-home-page"></a><span data-ttu-id="12327-197">Festlegen der Add-In-Startseite auf die Hostweb-Startseite</span><span class="sxs-lookup"><span data-stu-id="12327-197">Set the add-in start page to the host web home page</span></span>


1. <span data-ttu-id="12327-p112">Das fortlaufende Beispiel-SharePoint-Add-In verfügt nicht über ein Add-In-Web, und die Remotewebanwendung ist nur für das Hosten des Formulars vorhanden. Deshalb sollte die Startseite des Add-Ins auf die Startseite des Hostwebs festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="12327-p112">The continuing sample SharePoint Add-in doesn't have any add-in web and its remote web application exists only to host the form. So the start page of the add-in should be set to the home page of the host web.</span></span> 
    
    <span data-ttu-id="12327-200">Wählen Sie zunächst das SharePoint-Add-In-Projekt (nicht das Webanwendungsprojekt) im **Projektmappen-Explorer** aus, und kopieren Sie den Wert der Eigenschaft **Website-URL**, einschließlich des Protokolls (z. B. **https://contoso.sharepoint.com**), in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="12327-200">To begin, select the SharePoint Add-in project (not the web application project) in **Solution Explorer** and copy the value of the **Site URL** property, including the protocol (for example **https://contoso.sharepoint.com**) into the clipboard.</span></span> 
    
 
2. <span data-ttu-id="12327-201">Öffnen Sie das Add-In-Manifest, und fügen Sie die URL in das Feld **Startseite** ein.</span><span class="sxs-lookup"><span data-stu-id="12327-201">Open the add-in manifest, and then paste the URL into the **Start Page** box.</span></span>
    
 
3. <span data-ttu-id="12327-202">Optional können Sie die Seite „Default.aspx“ aus dem Webanwendungsprojekt löschen, da sie nicht im SharePoint-Add-In verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="12327-202">Optionally, you can delete the Default.aspx page from the web application project, because it is not used in the SharePoint Add-in.</span></span>
    
 

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="12327-203">So erstellen Sie die Lösung und führen sie aus</span><span class="sxs-lookup"><span data-stu-id="12327-203">To build and run the solution</span></span>


1. <span data-ttu-id="12327-204">Drücken Sie F5.</span><span class="sxs-lookup"><span data-stu-id="12327-204">Press the F5 key.</span></span>
    
     <span data-ttu-id="12327-205">**Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.</span><span class="sxs-lookup"><span data-stu-id="12327-205">**Note** When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="12327-p113">Klicken Sie auf die Schaltfläche **Vertrauen**. Die Standardseite Ihrer Entwicklerwebsite wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="12327-p113">Choose the **Trust It** button. The default page of your developer site opens.</span></span>
    
 
3. <span data-ttu-id="12327-208">Navigieren Sie zu einer beliebigen Dokumentbibliothek im Hostweb.</span><span class="sxs-lookup"><span data-stu-id="12327-208">Navigate to any document library in the host web.</span></span>
    
    <span data-ttu-id="12327-209">**Starten einer benutzerdefinierten Menüaktion**</span><span class="sxs-lookup"><span data-stu-id="12327-209">**Launching a custom menu action**</span></span>

 

  ![Dokumentbibliothek mit geöffneter Legende für ein Dokument, das durch die Popupschaltfläche in der Legende geöffnete Menü und das geöffnete Menü "Erweitert".](../../images/477cecf5-03ff-46ff-9c25-a5f9a86d43f4.png)
 

 

 
4. <span data-ttu-id="12327-p114">Klicken Sie auf die Popupschaltfläche ( **...**) für ein beliebiges Dokument. Das Popup wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="12327-p114">Choose the callout button ( **...**) for any document. The callout opens.</span></span>
    
 
5. <span data-ttu-id="12327-213">5.Klicken Sie auf die Popupschaltfläche ( **...**) im Popup.</span><span class="sxs-lookup"><span data-stu-id="12327-213">Choose the callout button ( **...**) on the callout.</span></span> 
    
 
6. <span data-ttu-id="12327-214">Wählen Sie **Erweitert** aus.</span><span class="sxs-lookup"><span data-stu-id="12327-214">Choose **Advanced**.</span></span>
    
 
7. <span data-ttu-id="12327-p115">Wählen Sie im Kontextmenü die Option **Meine benutzerdefinierte Menüaktion** aus. Auf der sich öffnenden Remotewebseite sollte etwas wie Folgendes angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="12327-p115">Choose **My Custom Menu Action** in the context menu. You should see something like the following on the remote webpage that opens:</span></span>
    
    <span data-ttu-id="12327-217">**Remotewebseite mit Parametern der benutzerdefinierten Aktion**</span><span class="sxs-lookup"><span data-stu-id="12327-217">**Remote webpage with parameters from the custom action**</span></span>

 

  ![Webseite mit Parametern aus einer benutzerdefinierten Aktion](../../images/CustomActions_target.png)
 

 

 
8. <span data-ttu-id="12327-219">Klicken Sie auf die Schaltfläche **Zurück** in Ihrem Browser, um zur Bibliothek zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="12327-219">Click the **Back** button on your browser to return to the library.</span></span>
    
    <span data-ttu-id="12327-220">**Starten einer benutzerdefinierten Menübandaktion**</span><span class="sxs-lookup"><span data-stu-id="12327-220">**Launching a custom ribbon action**</span></span>

 

  ![Eine Dokumentbibliothek mit einem ausgewählten Dokument, der geöffneten Registerkarte „Datei“ im Menüband und der benutzerdefinierten Schaltfläche im Menüband.](../../images/b315cb68-ff6a-4770-a1dc-738696ab71d2.png)
 

 

 
9. <span data-ttu-id="12327-222">Wählen Sie ein beliebiges Dokument aus.</span><span class="sxs-lookup"><span data-stu-id="12327-222">Select any document.</span></span>
    
 
10. <span data-ttu-id="12327-223">Öffnen Sie die Registerkarte **Datei** im Menüband.</span><span class="sxs-lookup"><span data-stu-id="12327-223">Open the **File** tab on the ribbon.</span></span>
    
 
11. <span data-ttu-id="12327-p116">Wählen Sie **Meine benutzerdefinierte Menübandschaltfläche** aus. Dieselbe Remotewebseite wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="12327-p116">Choose **My Custom Ribbon Button**. You see the same remote web page.</span></span>
    
 

<span data-ttu-id="12327-226">**Tabelle 4: Problembehandlung für die Lösung**</span><span class="sxs-lookup"><span data-stu-id="12327-226">**Table 4. Troubleshooting the solution**</span></span>


|<span data-ttu-id="12327-227">**Problem**</span><span class="sxs-lookup"><span data-stu-id="12327-227">**Problem**</span></span>|<span data-ttu-id="12327-228">**Lösung**</span><span class="sxs-lookup"><span data-stu-id="12327-228">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="12327-229">Der Browser wird nicht geöffnet, nachdem Sie F5 gedrückt haben.</span><span class="sxs-lookup"><span data-stu-id="12327-229">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="12327-230">Legen Sie das SharePoint-Add-In-Projekt als Startprojekt fest.</span><span class="sxs-lookup"><span data-stu-id="12327-230">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="12327-231">Die Token in der URL werden nicht aufgelöst, nachdem Sie in Visual Studio F5 gedrückt haben.</span><span class="sxs-lookup"><span data-stu-id="12327-231">The tokens in the URL are not resolved after you press the F5 key in Visual Studio.</span></span>|<span data-ttu-id="12327-232">Wechseln Sie zur Seite **Websiteinhalt** im Hostweb, und klicken Sie auf das Symbol für Ihr Add-In.</span><span class="sxs-lookup"><span data-stu-id="12327-232">Go to the **Site Contents** page in the host web, and click the icon for your add-in.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="12327-233">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="12327-233">Next steps</span></span>
<span data-ttu-id="12327-234"><a name="SP15Createcustomactionsapps_Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="12327-234"></span></span>

<span data-ttu-id="12327-p117">In diesem Artikel wurde die Vorgehensweise zum Erstellen einer benutzerdefinierten Aktion in einem SharePoint-Add-In beschrieben. Als nächsten Schritt können Sie sich über andere UX-Komponenten informieren, die für SharePoint-Add-Ins verfügbar sind. Weitere Informationen hierzu finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="12327-p117">This article demonstrated how to create a custom action in a SharePoint Add-in. As a next step, you can learn about other UX components that are available for SharePoint Add-ins. To learn more, see the following:</span></span>
 

 

-  [<span data-ttu-id="12327-238">Codebeispiel: Öffnen einer Remote-Add-In-Webseite mit einer benutzerdefinierten ECB-Aktion</span><span class="sxs-lookup"><span data-stu-id="12327-238">Code sample: Open a remote add-in webpage using an ECB custom action</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-e0ca1826)
    
 
-  [<span data-ttu-id="12327-239">SharePoint-Add-in-Localization</span><span class="sxs-lookup"><span data-stu-id="12327-239">SharePoint-Add-in-Localization</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-Localization)
    
 
-  [<span data-ttu-id="12327-240">Codebeispiel: Verwenden von benutzerdefinierten Aktionen und der domänenübergreifenden Bibliothek zum Bestellen von Büchern</span><span class="sxs-lookup"><span data-stu-id="12327-240">Code sample: Use custom actions and the cross-domain library to order books</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [<span data-ttu-id="12327-241">Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-241">Use a SharePoint website's style sheet in SharePoint Add-ins</span></span>](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="12327-242">Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-242">Use the client chrome control in SharePoint Add-ins</span></span>](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="12327-243">Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="12327-243">Create add-in parts to install with your SharePoint Add-in</span></span>](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a><span data-ttu-id="12327-244">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="12327-244">Additional resources</span></span>
<span data-ttu-id="12327-245"><a name="SP15Createcustomactionsapps_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="12327-245"></span></span>


-  [<span data-ttu-id="12327-246">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-246">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="12327-247">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-247">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="12327-248">Designrichtlinien für die Benutzerfreundlichkeit von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-248">SharePoint Add-ins UX design guidelines</span></span>](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [<span data-ttu-id="12327-249">Erstellen von UX-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="12327-249">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="12327-250">Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen</span><span class="sxs-lookup"><span data-stu-id="12327-250">Three ways to think about design options for SharePoint Add-ins</span></span>](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="12327-251">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="12327-251">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

