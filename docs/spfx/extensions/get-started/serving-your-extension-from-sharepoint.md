
# <a name="deploy-your-extension-to-sharepoint-hello-world-part-3"></a><span data-ttu-id="00b0b-101">Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)</span><span class="sxs-lookup"><span data-stu-id="00b0b-101">Deploy your client-side web part to a SharePoint page (Hello world part 3)</span></span>

><span data-ttu-id="00b0b-p101">**Hinweis:** Die SharePoint Framework-Erweiterungen befinden sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Die Verwendung von SharePoint Framework-Erweiterungen in Produktionsumgebungen wird aktuell nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p101">**Note:** The SharePoint Framework is currently in preview and is subject to change. SharePoint Framework client-side web parts are not currently supported for use in production environments.</span></span>

<span data-ttu-id="00b0b-p102">In diesem Artikel erfahren Sie, wie Sie Ihren SharePoint-Framework-Anwendungsanpasser in SharePoint bereitstellen und prüfen können, wie er auf den modernen SharePoint-Seiten funktioniert. In diesem Artikel wird weiterhin mit der Hello World-Erweiterung gearbeitet,die Sie im vorherigen Artikel [Verwenden von Seitenplatzhaltern des Anwendungsanpassers (Hello World, Teil 2)](./using-page-placeholder-with-extensions.md) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p102">In this article, you will learn how to deploy your SharePoint Framework Application Customizer to SharePoint and see it working on modern SharePoint pages. This article continues with the hello world extension built in the previous article [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md).</span></span>

<span data-ttu-id="00b0b-106">Stellen Sie sicher, dass Sie die Verfahren in den folgenden Artikeln abgeschlossen haben, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="00b0b-106">Be sure you have completed the procedures in the following articles before you start:</span></span>

* [<span data-ttu-id="00b0b-107">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="00b0b-107">Build your first SharePoint client-side web part (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="00b0b-108">Verwenden von Seitenplatzhaltern aus dem Anwendungsanpasser (Hello World, Teil 2)</span><span class="sxs-lookup"><span data-stu-id="00b0b-108">Using page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)

## <a name="package-the-helloworld-application-customizer"></a><span data-ttu-id="00b0b-109">Packen des helloWorld-Anwendungsanpassers</span><span class="sxs-lookup"><span data-stu-id="00b0b-109">Package the helloWorld Application Customizer</span></span>
<span data-ttu-id="00b0b-110">Wechseln Sie im Konsolenfenster zum Projektverzeichnis der Erweiterung, die Sie in [Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)](./build-a-hello-world-extension.md) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="00b0b-110">In the console window, go to the web part project directory created in [Build your first SharePoint client-side web part](./build-a-hello-world-extension.md).</span></span>

```
cd app-extension
```
<span data-ttu-id="00b0b-111">Wenn gulp serve noch ausgeführt wird, beenden Sie die Ausführung, indem Sie `Ctrl+C` drücken.</span><span class="sxs-lookup"><span data-stu-id="00b0b-111">If  is still running, stop it from running by choosing </span></span>

<span data-ttu-id="00b0b-p103">Im Gegensatz zum **Debug**-Modus müssen Sie zur Verwendung einer Erweiterung auf modernen serverseitigen SharePoint-Seiten die Erweiterung bereitstellen und in SharePoint registrieren, entweder im Bereich `Site collection`, `Site` oder `List`. Der Bereich definiert, wo und wie der Anwendungsanpasser aktiv sein soll. In diesem Szenario registrieren wir den Anwendungsanpasser mit dem `Site Collection`-Bereich.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p103">Unlike in **Debug** mode, in order to use an extension on modern SharePoint server-side pages, you need to deploy and register the extension with SharePoint in either `Site collection`, `Site`, or `List` scope. The scope defines where and how the Application Customizer will be active. In this particular scenario, we'll register the Application Customizer using the `Site Collection` scope.</span></span> 

<span data-ttu-id="00b0b-p104">Bevor wir die Lösung packen, müssen wir den Code, der zur Automatisierung der Erweiterungsaktivierung auf der Website bei jeder Installation der Lösung auf der Website erforderlich ist, einbeziehen. In diesem Fall verwenden wir Feature-Frameworkelemente direkt im Lösungspaket, um diese Aktionen auszuführen. Sie könnten jedoch auch den Anwendungsanpasser mit einer SharePoint-Website anhand von REST oder CSOM als Teil der Websitebereitstellung zuordnen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p104">Before we package our solution, we want to include the code needed to automate the extension activation within the site, whenever the solution is installed on the site. In this case, we'll use feature framework elements to perform these actions directly in the solution package, but you could also associate the application customizer to a SharePoint site using REST or CSOM as part of the site provisioning, for example.</span></span>

1. <span data-ttu-id="00b0b-117">Installieren Sie das Lösungspaket auf der Website, auf der es installiert werden soll, damit das Erweiterungsmanifest für die Ausführung freigegeben wird.</span><span class="sxs-lookup"><span data-stu-id="00b0b-117">Install the solution package to the site where it should be installed, so that extension manifest is being white listed for execution</span></span>
2. <span data-ttu-id="00b0b-p105">Ordnen Sie den Anwendungsanpasser dem geplanten Bereich zu. Dies kann programmgesteuert erfolgen (CSOM/REST) oder durch die Verwendung des Feature-Frameworks innerhalb des SharePoint-Framework-Lösungspakets. Sie müssen die folgenden Eigenschaften im `UserCustomAction`-Objekt auf Website- oder Listenebene verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p105">Associate the Application Customizer to the planned scope. This can be performed programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package. You'll need to associate the following properties in the `UserCustomAction` object at the site collection, site or list level.</span></span>
    * <span data-ttu-id="00b0b-121">**ClientSiteComponentId:** Dies ist der Bezeichner (GUID) für den Field Customizer, der im App-Katalog installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="00b0b-121">**ClientSiteComponentId:** This is the identifier (GUID) of the Field Customizer, which has been installed in the app catalog.</span></span> 
    * <span data-ttu-id="00b0b-122">**ClientSideComponentProperties:** Dies ist ein optionaler Parameter, der zum Bereitstellen von Eigenschaften für die Field Customizer-Instanz verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="00b0b-122">**ClientSideComponentProperties:** This is an optional parameter, which can be used to provide properties for the Field Customizer instance</span></span>

> <span data-ttu-id="00b0b-p106">Beachten Sie, dass Sie Lösungspakete derzeit explizit auf den Websites installieren müssen, um sicherzustellen, dass die Erweiterung ordnungsgemäß ausgeführt wird. Künftig wird es alternative Verfahren geben, um dies ohne Bereitstellung Website für Website zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p106">Notice. Currently you'll need to install solution packages explicitly to sites to ensure the extension is being properly executed. There will be alternative ways to achieve this in the future without site-by-site deployment.</span></span> 

<span data-ttu-id="00b0b-126">In den folgenden Schritten erstellen wir eine neue `CustomAction`-Definition, die dann automatisch mit den erforderlichen Konfigurationen bereitgestellt wird, sobald das Lösungspaket auf einer Website installiert wird.</span><span class="sxs-lookup"><span data-stu-id="00b0b-126">In the following steps, we'll create a new `CustomAction` definition, which will then be automatically deployed with the needed configurations when the solution package is installed on a site.</span></span> 

<span data-ttu-id="00b0b-127">Wechseln Sie wieder zu Ihrem Lösungspaket in Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="00b0b-127">Return to your solution package in Visual Studio Code (or to your preferred editor).</span></span>

<span data-ttu-id="00b0b-128">Hier müssen Sie zunächst einen Ordner **assets** erstellen, in dem Sie alle Featureframeworkobjekte ablegen, die bei der Paketinstallation zur Bereitstellung von SharePoint-Strukturen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="00b0b-128">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when package is installed.</span></span>

* <span data-ttu-id="00b0b-129">Erstellen Sie einen Ordner mit dem Namen **sharepoint** im Stammverzeichnis der Lösung.</span><span class="sxs-lookup"><span data-stu-id="00b0b-129">Create folder called **sharepoint** to the root of the solution</span></span>
* <span data-ttu-id="00b0b-130">Erstellen Sie einen Ordner mit dem Namen **assets** als Unterordner im soeben erstellten Ordner **sharepoint**.</span><span class="sxs-lookup"><span data-stu-id="00b0b-130">Create folder called **assets** as a sub folder for the just created **sharepoint** folder</span></span>

<span data-ttu-id="00b0b-131">Die Lösungsstruktur sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="00b0b-131">Your solution structure should look similar to the following picture:</span></span>

![Ordner „assets“ in der Lösungsstruktur](../../../../images/ext-app-assets-folder.png)

### <a name="add-an-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="00b0b-133">Hinzufügen einer Datei „elements.xml“ mit SharePoint-Definitionen</span><span class="sxs-lookup"><span data-stu-id="00b0b-133">Add element.xml file for SharePoint definitions</span></span>

<span data-ttu-id="00b0b-134">Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="00b0b-134">Create a new file inside the **sharepoint\assets** folder named as **elements.xml**</span></span>

<span data-ttu-id="00b0b-p107">Kopieren Sie die nachfolgende XML-Struktur in die Datei **elements.xml**. Vergessen Sie dabei nicht, für die Eigenschaft **ClientSideComponentId** die eindeutige ID Ihres Anwendungsanpassers aus der Datei **HelloWorldApplicationCustomizer.manifest.json** im Ordner **src\extensions\helloWorld** anzugeben.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p107">Copy the following xml structure into **elements.xml**. Be sure to update the **ClientSideComponentId** property to the unique Id of your Application Customizer available in the **HelloWorldApplicationCustomizer.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="00b0b-p108">Wir legen darüber hinaus die **ClientSideComponentProperties** fest und übergeben JSON-Eigenschaften für diese Erweiterungsinstanz. Beachten Sie, dass JSON hier auskommentiert ist, damit wir es ordnungsgemäß in einem XML-Attribut festlegen können.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p108">We also set the **ClientSideComponentProperties** and pass JSON properties for this extension instance. Notice how the JSON is escaped so that we can set it properly within an XML attribute.</span></span> 

<span data-ttu-id="00b0b-p109">Beachten Sie auch, dass wir den spezifischen Speicherort von `ClientSideExtension.ApplicationCustomizer` verwenden, um zu definieren, dass es sich um einen Anwendungsanpasser handelt. Da dieses **elements.xml** standardmäßig mit einem *Web*-Bereichsfeature verknüpft ist, wird diese `CustomAction` automatisch zur `Web.UserCustomAction`-Websitesammlung auf der Website hinzugefügt, auf der die Lösung installiert wird.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p109">Notice also that we use the specific location of `ClientSideExtension.ApplicationCustomizer` to define that this is an Application Customizer. Since by default this **elements.xml** will be associated to a *Web* scoped feature, this `CustomAction` will be automatically added to the `Web.UserCustomAction` collection in the site where the solution is being installed.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxApplicationCustomizer"
        Location="ClientSideExtension.ApplicationCustomizer"
        ClientSideComponentId="46606aa6-5dd8-4792-b017-1555ec0a43a4"
        ClientSideComponentProperties="{&quot;Header&quot;:&quot;Header area of the page&quot;,&quot;Footer&quot;:&quot;Footer area in the page&quot;}">

    </CustomAction>

</Elements>
```

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="00b0b-141">Gewährleisten der Berücksichtigung von Definitionen in der Buildpipeline</span><span class="sxs-lookup"><span data-stu-id="00b0b-141">Ensure that definitions are taken into use in build pipeline</span></span>

<span data-ttu-id="00b0b-p110">Öffnen Sie die Datei **package-solution.json** im Ordner **config**. Die Datei **package-solution.json** enthält die Paketmetadaten, definiert wie folgt:</span><span class="sxs-lookup"><span data-stu-id="00b0b-p110">Open **package-solution.json** from the config folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "02d35a3e-5896-4664-874f-9fe9fdfe8408",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}

```

<span data-ttu-id="00b0b-p111">Um sicherzustellen, dass die neu hinzugefügte Datei **element.xml** beim Verpacken der Lösung berücksichtigt wird, müssen wir eine Featureframework-Featuredefinition für das Lösungspaket einschließen. Dazu integrieren wir wie nachfolgend demonstriert eine JSON-Definition des benötigten Features in die Lösungsstruktur.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p111">To ensure that our newly added Feature Framework files are taken into account while solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for needed feature inside of the solution structure as demonstrated in below code.</span></span>

```json
{
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "02d35a3e-5896-4664-874f-9fe9fdfe8408",
    "version": "1.0.0.0",
    "features": [{
      "title": "Application Extension - Deployment of custom action.",
      "description": "Deploys a custom action with ClientSideComponentId association",
      "id": "456da147-ced2-3036-b564-8dad5c1c2e34",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}

```

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="00b0b-146">Bereitstellen der Erweiterung in SharePoint Online und Hosten des JavaScript-Codes über Localhost</span><span class="sxs-lookup"><span data-stu-id="00b0b-146">Deploy the extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="00b0b-147">Nun können Sie die Lösung auf einer SharePoint-Website bereitstellen und das Objekt `CustomAction` automatisch auf Website-Ebene verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-147">Now you are ready to deploy the solution to a SharePoint site and to have the `CustomAction` automatically associated on the site level.</span></span>

<span data-ttu-id="00b0b-148">Geben Sie im Konsolenfenster den folgenden Befehl ein, um die clientseitige Lösung, die die Erweiterung enthält, zu verpacken und so die Grundstruktur für die Paketierung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="00b0b-148">In the console window, enter the following command to package your client-side solution that contains the web part, so that we get the basic structure ready for packaging:</span></span>

```
gulp bundle
```

<span data-ttu-id="00b0b-149">Führen Sie als Nächstes den folgenden Befehl aus, um das Lösungspaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="00b0b-149">Next execute following command, so that the solution package is created:</span></span>

```
gulp package-solution
```

<span data-ttu-id="00b0b-150">Der Befehl erstellt das Paket im Ordner **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="00b0b-150">The command will create the package in the  folder:</span></span>

```
app-extension.sppkg
```

<span data-ttu-id="00b0b-151">Als Nächstes müssen Sie das Paket, das generiert wurde, im App-Katalog bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-151">Next you need to deploy the package that was generated to the App Catalog.</span></span>

<span data-ttu-id="00b0b-152">Wechseln Sie zum **App-Katalog** Ihres Mandanten, und öffnen Sie die Bibliothek **Apps für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="00b0b-152">Go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

<span data-ttu-id="00b0b-p112">Laden Sie das Paket `app-extension.sppkg` aus dem Ordner **sharepoint/solution** in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop. SharePoint fordert Sie in einem Dialogfeld auf, der clientseitigen Lösung zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p112">Upload or drag and drop the asset-deployment-webpart.sppkg located in the  folder  to the App Catalog. SharePoint will display a dialog and ask you to trust the client-side solution to deploy.</span></span>

<span data-ttu-id="00b0b-p113">Da wir die Host-URLs der Lösung für diese Bereitstellung nicht aktualisiert haben, verweist die URL immer noch auf `https://localhost:4321`. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p113">Notice that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`. Click the **Deploy** button.</span></span>

![Bestätigen des Vertrauens beim Upload in den App-Katalog](../../../../images/ext-app-sppkg-deploy-trust.png)

<span data-ttu-id="00b0b-p114">Wechseln Sie wieder zur Konsole, und vergewissern Sie sich, dass die Lösung ausgeführt wird. Sollte Sie nicht ausgeführt werden, führen Sie den folgenden Befehl im Lösungsordner aus:</span><span class="sxs-lookup"><span data-stu-id="00b0b-p114">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="00b0b-p115">Wechseln Sie zu der Website, auf der Sie die Bereitstellung der SharePoint-Ressource testen möchten. Dies könnte eine Websitesammlung im Mandanten sein, auf dem Sie dieses Lösungspaket bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p115">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

<span data-ttu-id="00b0b-162">Klicken Sie auf der oberen Navigationsleiste rechts auf das Zahnradsymbol und anschließend auf **App hinzufügen**, um Ihre Apps-Seite aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="00b0b-162">Choose the gears icon on the top nav bar on the right and choose **Add an app** to go to your Apps page.</span></span>

<span data-ttu-id="00b0b-163">Geben Sie in das **Suchfeld** die Zeichenfolge **app** ein, und drücken Sie die *EINGABETASTE*, um Ihre Apps zu filtern.</span><span class="sxs-lookup"><span data-stu-id="00b0b-163">In the **Search** box, enter **helloworld** and choose *Enter* to filter your apps.</span></span>

![Installieren von Field Customizer auf der Website](../../../../images/ext-app-install-solution-to-site.png)

<span data-ttu-id="00b0b-p116">Wählen Sie die App **app-extension-client-side-solutionn** aus, um die Lösung auf der Website zu installieren. Aktualisieren Sie die Seite nach Abschluss der Installation mithilfe der Taste **F5**.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p116">Choose the **asset-deployment-webpart-client-side-solution** app to install the app on the site. When installation is completed, refresh the page by pressing **F5**.</span></span>

<span data-ttu-id="00b0b-167">Wenn die Anwendung erfolgreich installiert wurde, werden die Kopf- und Fußzeile genau so gerendert wie mit den Debugging-Abfrageparametern.</span><span class="sxs-lookup"><span data-stu-id="00b0b-167">When the application has been successfully installed, you can see the header and footer being rendered just like with the debug query parameters.</span></span>

![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="00b0b-169">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="00b0b-169">Next steps</span></span>

<span data-ttu-id="00b0b-p117">Herzlichen Glückwunsch! Sie haben eine Erweiterung für eine moderne SharePoint-Seite aus dem App-Katalog bereitgestellt! Sie können mit der Entwicklung der Hello World-Erweiterung im nächsten Thema , [Hostingerweiterung aus Office 365 CDN (Hello World, Teil 4)](./hosting-extension-from-office365-cdn.md) fortfahren, in dem Sie erfahren, wie Sie die Erweiterungsobjekte aus einem CDN anstelle von Localhost bereitstellen und laden.</span><span class="sxs-lookup"><span data-stu-id="00b0b-p117">Congratulations, you have deployed an extension to a modern SharePoint page from the app catalog! You can continue building out your Hello World extension in the next topic, [Hosting extension from Office 365 CDN (Hello world part 4)](./hosting-extension-from-office365-cdn.md), where you will learn how to deploy and load the extension assets from a CDN instead of localhost.</span></span>