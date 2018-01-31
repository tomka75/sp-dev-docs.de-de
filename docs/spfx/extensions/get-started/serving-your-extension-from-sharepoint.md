---
title: Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)
description: "Bereitstellen Ihres SharePoint-Framework Application Customizer in SharePoint und Erläuterung seiner Funktionsweise auf modernen SharePoint-Seiten."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 47dbc2baa9503a2e9f7793411a794c0bf948a739
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="deploy-your-extension-to-sharepoint-hello-world-part-3"></a><span data-ttu-id="72ac6-103">Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)</span><span class="sxs-lookup"><span data-stu-id="72ac6-103">Deploy your extension to SharePoint (Hello World part 3)</span></span>

<span data-ttu-id="72ac6-104">In diesem Artikel wird die Bereitstellung des Application Customizers von SharePoint-Framework in SharePoint und seine Funktionsweise auf modernen SharePoint-Seiten erläutert.</span><span class="sxs-lookup"><span data-stu-id="72ac6-104">This article describes how to deploy your SharePoint Framework Application Customizer to SharePoint and see it working on modern SharePoint pages.</span></span> 

<span data-ttu-id="72ac6-105">Stellen Sie sicher, dass Sie die Verfahren in den folgenden Artikeln abgeschlossen haben, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="72ac6-105">Be sure you have completed the procedures in the following articles before you begin:</span></span>

* [<span data-ttu-id="72ac6-106">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="72ac6-106">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="72ac6-107">Verwenden von Seitenplatzhaltern aus dem Application Customizer (Hello World, Teil 2)</span><span class="sxs-lookup"><span data-stu-id="72ac6-107">Use page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)

<span data-ttu-id="72ac6-108">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=P_yWI0WVQIg&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="72ac6-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=P_yWI0WVQIg&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=DzHdVxLA3Pc">
<img src="../../../images/spfx-ext-youtube-tutorial3.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="package-the-hello-world-application-customizer"></a><span data-ttu-id="72ac6-109">Packen des Hello World Application Customizers</span><span class="sxs-lookup"><span data-stu-id="72ac6-109">Package the Hello World Application Customizer</span></span>

1. <span data-ttu-id="72ac6-110">Wechseln Sie im Konsolenfenster zum Projektverzeichnis der Erweiterung, die Sie unter [Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)](./build-a-hello-world-extension.md) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="72ac6-110">In the console window, go to the extension project directory created in [Build your first SharePoint Framework Extension (Hello World part 1)](./build-a-hello-world-extension.md).</span></span>

  ```
  cd app-extension
  ```

2. <span data-ttu-id="72ac6-111">Wenn gulp serve noch ausgeführt wird, beenden Sie die Ausführung, indem Sie STRG + C drücken.</span><span class="sxs-lookup"><span data-stu-id="72ac6-111">If gulp serve is still running, stop it from running by selecting Ctrl+C.</span></span>

  <span data-ttu-id="72ac6-112">Im Gegensatz zum **Debug**-Modus müssen Sie für die Verwendung einer Erweiterung auf modernen serverseitigen SharePoint-Seiten die Erweiterung bei SharePoint im Bereich `Site collection`, `Site` oder `List` bereitstellen und registrieren.</span><span class="sxs-lookup"><span data-stu-id="72ac6-112">Unlike in **Debug** mode, to use an extension on modern SharePoint server-side pages, you need to deploy and register the extension with SharePoint in `Site collection`, `Site`, or `List` scope.</span></span> <span data-ttu-id="72ac6-113">Der Bereich definiert, wo und wie der Application Customizer aktiv ist.</span><span class="sxs-lookup"><span data-stu-id="72ac6-113">The scope defines where and how the Application Customizer will be active.</span></span> <span data-ttu-id="72ac6-114">In diesem Szenario wird der Application Customizer unter Verwendung des Bereichs `Site collection` registriert.</span><span class="sxs-lookup"><span data-stu-id="72ac6-114">In this particular scenario, we'll register the Application Customizer by using the `Site collection` scope.</span></span> 

  <span data-ttu-id="72ac6-115">Vor dem Packen der Lösung wird der Code hinzugefügt, mit dem die Erweiterungsaktivierung auf der Website automatisiert wird, sobald die Lösung auf der Website installiert ist.</span><span class="sxs-lookup"><span data-stu-id="72ac6-115">Before we package our solution, we want to include the code needed to automate the extension activation within the site whenever the solution is installed on the site.</span></span> <span data-ttu-id="72ac6-116">In diesem Fall verwenden wir Feature-Framework-Elemente für die direkte Ausführung dieser Aktionen in dem Lösungspaket, Sie können jedoch auch den Application Customizer einer SharePoint-Website zuordnen, indem Sie REST oder CSOM im Rahmen der Websitebereitstellung verwenden.</span><span class="sxs-lookup"><span data-stu-id="72ac6-116">In this case, we'll use feature framework elements to perform these actions directly in the solution package, but you could also associate the application customizer to a SharePoint site by using REST or CSOM as part of the site provisioning, for example.</span></span>

3. <span data-ttu-id="72ac6-117">Installieren Sie das Lösungspaket auf der Website, auf der es installiert sein soll, damit das Erweiterungsmanifest für die Ausführung freigegeben wird.</span><span class="sxs-lookup"><span data-stu-id="72ac6-117">Install the solution package to the site where it should be installed so that the extension manifest is being white listed for execution.</span></span>

4. <span data-ttu-id="72ac6-118">Ordnen Sie den Application Customizer dem geplanten Bereich zu.</span><span class="sxs-lookup"><span data-stu-id="72ac6-118">Associate the Application Customizer to the planned scope.</span></span> <span data-ttu-id="72ac6-119">Dies kann programmgesteuert (CSOM/REST) oder mit dem Feature-Framework innerhalb des SharePoint-Framework-Lösungspakets erfolgen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-119">This can be performed programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package.</span></span> <span data-ttu-id="72ac6-120">Sie müssen die folgenden Eigenschaften im `UserCustomAction`-Objekt auf der Websitesammlungs-, Website- oder Listenebene zuweisen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-120">You'll need to associate the following properties in the `UserCustomAction` object at the site collection, site, or list level.</span></span>
  
  * <span data-ttu-id="72ac6-121">**ClientSideComponentId**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-121">**ClientSideComponentId**.</span></span> <span data-ttu-id="72ac6-122">Dies ist der Bezeichner (GUID) für den Field Customizer, der im App-Katalog installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="72ac6-122">ClientSiteComponentId is the identifier (GUID) of the Field Customizer, which has been installed in the App Catalog.</span></span> 
  * <span data-ttu-id="72ac6-123">**ClientSideComponentProperties**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-123">**ClientSideComponentProperties**.</span></span> <span data-ttu-id="72ac6-124">Dies ist ein optionaler Parameter, der verwendet werden kann, um Eigenschaften für die Field Customizer-Instanz bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-124">ClientSideComponentProperties: This is an optional parameter, which can be used to provide properties for the Field Customizer instance.</span></span>
   
  <span data-ttu-id="72ac6-125">Beachten Sie, dass Sie die Anforderung zum Hinzufügen einer Lösung mit Ihrer Erweiterung zu der Website mithilfe der `skipFeatureDeployment`-Einstellung in **package-solution.json** steuern können.</span><span class="sxs-lookup"><span data-stu-id="72ac6-125">Note that you can control the requirement to add a solution containing your extension to the site by using the `skipFeatureDeployment` setting in **package-solution.json**.</span></span> <span data-ttu-id="72ac6-126">Auch wenn Sie die Installation der Lösung auf der Website nicht voraussetzen, müssen Sie **ClientSideComponentId** bestimmten Objekten zuweisen, damit die Erweiterung angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="72ac6-126">Even though you would not require the solution to be installed on the site, you'd need to associate **ClientSideComponentId** to specific objects for the extension to be visible.</span></span> 
   
  <span data-ttu-id="72ac6-127">In den folgenden Schritten wird die `CustomAction`-Definition geprüft, die automatisch für die Lösung als Teil der Gerüsterstellung erstellt wurde, damit die Lösung auf einer Website aktiviert wird, sobald sie installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="72ac6-127">In the following steps, we'll review the `CustomAction` definition, which was automatically created for the solution as part of the scaffolding for enabling the solution on a site when it's being installed.</span></span> 
   
5. <span data-ttu-id="72ac6-128">Wechseln Sie wieder zu Ihrem Lösungspaket in Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="72ac6-128">Return to your solution package in Visual Studio Code (or to your preferred editor).</span></span>

6. <span data-ttu-id="72ac6-129">Erweitern Sie im Stammverzeichnis der Lösung den Ordner **sharepoint** und den Unterordner **assets**, um die vorhandene Datei **elements.xml** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-129">Extend the **sharepoint** folder and **assets** subfolder in the root of the solution to see the existing **elements.xml** file.</span></span> 

   ![Ordner „assets“ in der Lösungsstruktur](../../../images/ext-app-assets-folder.png)

<br/>

### <a name="review-the-existing-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="72ac6-131">Überprüfen der vorhandenen Datei „elements.xml“ auf SharePoint-Definitionen</span><span class="sxs-lookup"><span data-stu-id="72ac6-131">Review the existing elements.xml file for SharePoint definitions</span></span>

<span data-ttu-id="72ac6-132">Überprüfen Sie die vorhandene XML-Struktur in der Datei **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-132">Review the existing xml structure in the **elements.xml** file.</span></span> <span data-ttu-id="72ac6-133">Beachten Sie, dass die Eigenschaft **ClientSideComponentId** anhand der eindeutigen ID des Application Customizer aus der Datei **HelloWorldFieldCustomizer.manifest.json** im Ordner **src\extensions\helloWorld** automatisch aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="72ac6-133">Note that the **ClientSideComponentId** property has been automatically updated based on the unique ID of your Application Customizer available in the **HelloWorldApplicationCustomizer.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="72ac6-134">**ClientSideComponentProperties** wurde auch mithilfe der standardmäßigen Struktur und JSON-Eigenschaften für diese Instanz der Erweiterung automatisch festgelegt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-134">**ClientSideComponentProperties** has also been automatically set with the default structure and JSON properties for this extension instance.</span></span> <span data-ttu-id="72ac6-135">Beachten Sie auch die Escapezeichen im JSON mit, damit es ordnungsgemäß in einem XML-Attribut festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="72ac6-135">Note how the JSON is escaped so that we can set it properly within an XML attribute.</span></span> 

<span data-ttu-id="72ac6-136">Die Konfiguration verwendet die Position von `ClientSideExtension.ApplicationCustomizer`, um zu definieren, dass es sich dabei um einen Application Customizer handelt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-136">The configuration uses the specific location of `ClientSideExtension.ApplicationCustomizer` to define that this is an Application Customizer.</span></span> <span data-ttu-id="72ac6-137">Da diese Datei standardmäßig **elements.xml** einem Feature mit dem Bereich *Web* zugeordnet wird, wird diese `CustomAction` automatisch der `Web.UserCustomAction`-Sammlung auf der Website hinzugefügt, auf der die Lösung installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="72ac6-137">Because this **elements.xml** is associated to a *Web* scoped feature by default, this `CustomAction` is automatically added to the `Web.UserCustomAction` collection in the site where the solution is being installed.</span></span>

<span data-ttu-id="72ac6-138">Um sicherzustellen, dass die Konfiguration mit den Aktualisierungen im Application Customizer übereinstimmt, aktualisieren Sie **ClientSideComponentProperties** wie in der folgenden XML-Struktur dargestellt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-138">To ensure that the configuration matches updates performed in the Application Customizer, update the **ClientSideComponentProperties** as in the following xml structure.</span></span> <span data-ttu-id="72ac6-139">Sie sollten nicht die gesamte Struktur kopieren, da es sonst zu einer Nichtübereinstimmung mit Ihrer **ClientSideComponentId** kommt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-139">Note that you should not copy the whole structure because it would cause a mismatch with your **ClientSideComponentId**.</span></span>


```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxApplicationCustomizer"
        Location="ClientSideExtension.ApplicationCustomizer"
        ClientSideComponentId="46606aa6-5dd8-4792-b017-1555ec0a43a4"
        ClientSideComponentProperties="{&quot;Top&quot;:&quot;Top area of the page&quot;,&quot;Bottom&quot;:&quot;Bottom area in the page&quot;}">

    </CustomAction>

</Elements>
```

<br/>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="72ac6-140">Gewährleisten der Berücksichtigung von Definitionen in der Buildpipeline</span><span class="sxs-lookup"><span data-stu-id="72ac6-140">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="72ac6-141">Öffnen Sie **package-solution.json** im Ordner **config**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-141">Open **package-solution.json** from the **config** folder.</span></span> <span data-ttu-id="72ac6-142">Die Datei **package-solution.json** definiert die Paketmetadaten, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-142">The **package-solution.json** file defines the package metadata as shown in the following code:</span></span> <span data-ttu-id="72ac6-143">Um sicherzustellen, dass die Datei **element.xml** beim Packen der Lösung berücksichtigt wird, fügt das Standardgerüst die benötigte Konfiguration hinzu, um eine Framework-Featuredefinition für das Lösungspaket zu definieren.</span><span class="sxs-lookup"><span data-stu-id="72ac6-143">To ensure that the **element.xml** file is taken into account while the solution is being packaged, default scaffolding adds needed configuration to define a feature framework feature definition for the solution package.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "98a9fe4f-175c-48c1-adee-63fb927faa70",
    "version": "1.0.0.0",
    "features": [
      {
        "title": "Application Extension - Deployment of custom action.",
        "description": "Deploys a custom action with ClientSideComponentId association",
        "id": "4678966b-de68-445f-a74e-e553a7b937ab",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ]
        }
      }
    ]
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}


```

<br/>

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="72ac6-144">Bereitstellen der Erweiterung in SharePoint Online und Hosten des JavaScript-Codes über Localhost</span><span class="sxs-lookup"><span data-stu-id="72ac6-144">Deploy the extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="72ac6-145">Nun können Sie die Lösung auf einer SharePoint-Website bereitstellen und das Objekt `CustomAction` automatisch auf Website-Ebene verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-145">Now you are ready to deploy the solution to a SharePoint site and have the `CustomAction` automatically associated on the site level.</span></span>

1. <span data-ttu-id="72ac6-146">Geben Sie im Konsolenfenster den folgenden Befehl ein, um die clientseitige Lösung, die die Erweiterung enthält, zu verpacken und so die Grundstruktur für die Paketerstellung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="72ac6-146">In the console window, enter the following command to package your client-side solution that contains the extension so that we get the basic structure ready for packaging:</span></span>

   ```
   gulp bundle
   ```

2. <span data-ttu-id="72ac6-147">Führen Sie den folgenden Befehl aus, um das Lösungspaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="72ac6-147">Execute the following command so that the solution package is created:</span></span>

   ```
   gulp package-solution
   ```

   <span data-ttu-id="72ac6-148">Der Befehl erstellt das Paket im Ordner **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="72ac6-148">The command creates the package in the **sharepoint/solution** folder:</span></span>

   ```
   app-extension.sppkg
   ```

3. <span data-ttu-id="72ac6-149">Als Nächstes müssen Sie das Paket, das generiert wurde, im App-Katalog bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-149">You now need to deploy the package that was generated to the App Catalog.</span></span> <span data-ttu-id="72ac6-150">Wechseln Sie dazu zum **App-Katalog** Ihres Mandanten, und öffnen Sie die Bibliothek **Apps für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-150">To do this, go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

4. <span data-ttu-id="72ac6-151">Laden Sie das Paket `app-extension.sppkg`, das sich im Ordner **sharepoint/solution** befindet, in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop.</span><span class="sxs-lookup"><span data-stu-id="72ac6-151">Upload or drag and drop the `app-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog.</span></span> <span data-ttu-id="72ac6-152">In SharePoint wird ein Dialogfeld angezeigt, und Sie werden aufgefordert, der clientseitigen Lösung zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-152">SharePoint displays a dialog and asks you to trust the client-side solution.</span></span>

   <span data-ttu-id="72ac6-153">Da wir die Host-URLs der Lösung für diese Bereitstellung nicht aktualisiert haben, verweist die URL immer noch auf `https://localhost:4321`.</span><span class="sxs-lookup"><span data-stu-id="72ac6-153">Note that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`.</span></span> 
   
5. <span data-ttu-id="72ac6-154">Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="72ac6-154">Select the **Deploy** button.</span></span>

   ![Bestätigen des Vertrauens beim Upload in den App-Katalog](../../../images/ext-app-sppkg-deploy-trust.png)

6. <span data-ttu-id="72ac6-p114">Wechseln Sie wieder zur Konsole, und vergewissern Sie sich, dass die Lösung ausgeführt wird. Sollte Sie nicht ausgeführt werden, führen Sie den folgenden Befehl im Lösungsordner aus:</span><span class="sxs-lookup"><span data-stu-id="72ac6-p114">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>
   
   ```
   gulp serve --nobrowser
   ```
   
7. <span data-ttu-id="72ac6-p115">Wechseln Sie zu der Website, auf der Sie die Bereitstellung der SharePoint-Ressource testen möchten. Dies könnte eine Websitesammlung im Mandanten sein, auf dem Sie dieses Lösungspaket bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="72ac6-p115">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

8. <span data-ttu-id="72ac6-160">Klicken Sie auf der oberen Navigationsleiste rechts auf das Zahnradsymbol und anschließend auf **App hinzufügen**, um Ihre Seite „Apps“ aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="72ac6-160">Select the gear icon on the top navigation bar on the right, and then select **Add an app** to go to your Apps page.</span></span>

9. <span data-ttu-id="72ac6-161">Geben Sie in das **Suchfeld** die Zeichenfolge **app** ein, und drücken Sie die EINGABETASTE, um Ihre Apps zu filtern.</span><span class="sxs-lookup"><span data-stu-id="72ac6-161">In the **Search** box, enter **app**, and then select Enter to filter your apps.</span></span>

   ![Installieren von Field Customizer auf der Website](../../../images/ext-app-install-solution-to-site.png)

10. <span data-ttu-id="72ac6-163">Wählen Sie die App **app-extension-client-side-solution**, um die Lösung auf der Website zu installieren.</span><span class="sxs-lookup"><span data-stu-id="72ac6-163">Select the **app-extension-client-side-solution** app to install the solution on the site.</span></span> <span data-ttu-id="72ac6-164">Wenn die Installation abgeschlossen ist, aktualisieren Sie die Seite, indem Sie F5 drücken.</span><span class="sxs-lookup"><span data-stu-id="72ac6-164">When the installation is completed, refresh the page by selecting F5.</span></span>

  <span data-ttu-id="72ac6-165">Wenn die Anwendung erfolgreich installiert wurde, werden die Kopf- und Fußzeile genau so gerendert wie mit den Debugging-Abfrageparametern.</span><span class="sxs-lookup"><span data-stu-id="72ac6-165">When the application has been successfully installed, you can see the header and footer being rendered just like with the debug query parameters.</span></span>

  ![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="72ac6-167">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="72ac6-167">Next steps</span></span>

<span data-ttu-id="72ac6-168">Glückwunsch! Sie haben eine Erweiterung für eine moderne SharePoint-Seite aus dem App-Katalog bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="72ac6-168">Congratulations, you have deployed an extension to a modern SharePoint page from the app catalog!</span></span> 

<span data-ttu-id="72ac6-169">Sie können mit der Entwicklung der Hello World-Erweiterung im nächsten Thema [Hostingerweiterung aus Office 365 CDN (Hello World, Teil 4)](./hosting-extension-from-office365-cdn.md) fortfahren, in dem Sie erfahren, wie Sie die Erweiterungsobjekte aus einem CDN anstelle von Localhost bereitstellen und laden.</span><span class="sxs-lookup"><span data-stu-id="72ac6-169">You can continue building out your Hello World extension in the next topic, [Host extension from Office 365 CDN (Hello World part 4)](./hosting-extension-from-office365-cdn.md), where you will learn how to deploy and load the extension assets from a CDN instead of from localhost.</span></span>

> [!NOTE]
> <span data-ttu-id="72ac6-170">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="72ac6-170">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="72ac6-171">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="72ac6-171">Thanks for your input advance.</span></span>
