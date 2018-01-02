---
title: Bereitstellen Ihres clientseitigen SharePoint-Webparts in einem CDN
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: 5999958169ec6d94d5e8eca29a4d8458a6a77dea
ms.sourcegitcommit: 1f752afb40ff133e2fae14337e09392cc5d9d181
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="deploy-your-sharepoint-client-side-web-part-to-azure-cdn"></a><span data-ttu-id="e25b4-102">Bereitstellen Ihres clientseitigen SharePoint-Webparts im Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e25b4-102">Deploy your SharePoint client-side web part to a CDN</span></span>

<span data-ttu-id="e25b4-103">Dieser Artikel enthält Informationen zum Erstellen eines neuen Beispielwebparts und zum Bereitstellen der zugehörigen Objekte in einem Azure CDN als Hostinglösung, anstelle des standardmäßigen Office 365 CDN.</span><span class="sxs-lookup"><span data-stu-id="e25b4-103">In this article, you will create a new sample web part and deploy it's assets to a Azure CDN instead of using the default Office 365 CDN as the hosting solution.</span></span> <span data-ttu-id="e25b4-104">Sie verwenden ein Azure-Speicherkonto, das in ein CDN integriert ist, um Ihre Ressourcen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-104">You'll use an Azure Storage account integrated with a CDN to deploy your assets.</span></span> <span data-ttu-id="e25b4-105">Die Buildtools von SharePoint Framework bieten eine sofort nutzbare Unterstützung für die Bereitstellung auf einem Azure-Speicherkonto. Sie können die Dateien jedoch auch manuell an einen CDN-Anbieter Ihrer Wahl oder nach SharePoint hochladen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-105">In this article, you will deploy the HelloWorld assets to a remote CDN instead of using the local environment. You'll use an Azure Storage account integrated with a CDN to deploy your assets. SharePoint Framework build tools provide out-of-the-box support for deploying to an Azure Storage account; however, you can also manually upload the files to your favorite CDN provider or to SharePoint.</span></span>

> [!NOTE]
> <span data-ttu-id="e25b4-106">Es gibt mehrere unterschiedliche Hostingoptionen für Webpart-Objekte.</span><span class="sxs-lookup"><span data-stu-id="e25b4-106">There are multiple different hosting options for your web part assets.</span></span> <span data-ttu-id="e25b4-107">In diesem Lernprogramm steht die Option „Azure CDN“ im Vordergrund, Sie können jedoch auch das [Office 365 CDN](./hosting-webpart-from-office-365-cdn.md) verwenden oder einfach Ihre Objekt aus der SharePoint-Bibliothek aus dem Mandanten hosten.</span><span class="sxs-lookup"><span data-stu-id="e25b4-107">This tutorial concentrates on showing the Azure CDN option, but you could also use the [Office 365 CDN](./hosting-webpart-from-office-365-cdn.md) or simply host your assets from SharePoint library from your tenant.</span></span> <span data-ttu-id="e25b4-108">Im letzteren Fall würden Sie nicht von den CDN-Leistungssteigerungen profitieren, im Hinblick auf die Funktionalität wäre dies jedoch möglich.</span><span class="sxs-lookup"><span data-stu-id="e25b4-108">In the latter case, you would not benefit from the CDN performance improvements, but that would also work from the functionality perspective.</span></span> <span data-ttu-id="e25b4-109">Technisch gesehen wäre jeder Ort zum Hosten der Objekte für Endbenutzer denkbar, auf den Endbenutzer über HTTP zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="e25b4-109">Any location which end users can access using HTTP would be technically suitable for hosting the assets for end users.</span></span>

## <a name="configure-azure-storage-account"></a><span data-ttu-id="e25b4-110">Konfigurieren eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="e25b4-110">Configure Azure storage account</span></span>

<span data-ttu-id="e25b4-111">Konfigurieren Sie ein Azure-Speicherkonto, und integrieren Sie es in das CDN.</span><span class="sxs-lookup"><span data-stu-id="e25b4-111">Configure an Azure storage account and integrate it with the CDN.</span></span>

<span data-ttu-id="e25b4-112">Sie können die Anweisungen im Artikel [Integrieren eines Speicherkontos in CDN](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/) zusammen mit den detaillierten Schritten in diesem Artikel verwenden, um ein Azure -Speicherkonto zu erstellen und dieses in das CDN zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="e25b4-112">You can follow the instructions in the article [Integrate a Storage Account with CDN](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/) along with the detailed steps in this article to create an Azure storage account and integrate it with the CDN. You will need the following information.</span></span> <span data-ttu-id="e25b4-113">Sie benötigen die folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-113">You will need the following information.</span></span>

### <a name="storage-account-name"></a><span data-ttu-id="e25b4-114">Speicherkontoname</span><span class="sxs-lookup"><span data-stu-id="e25b4-114">Storage account name</span></span>

<span data-ttu-id="e25b4-115">Dies ist der Name, den Sie zum Erstellen des Speicherkontos verwendet haben, wie in [Schritt 1: Erstellen eines Speicherkontos](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-1-create-a-storage-account) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="e25b4-115">This is the name you used to create your storage account, as described in [Step 1: Create a storage account](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-1-create-a-storage-account).</span></span>

<span data-ttu-id="e25b4-116">Im folgenden Screenshot ist **spfxsamples** der Name des Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="e25b4-116">For example, in the following screenshot, **spfxsamples** is the storage account name.</span></span>

![Screenshots, auf dem die Seite „Erstellen eines neues Speicherkontos“ dargestellt ist](../../../images/deploy-create-storage-account.png)

<span data-ttu-id="e25b4-118">Auf diese Weise wird der neue Speicherkontoendpunkt **spfxsamples.blob.core.windows.net** erstellt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-118">This will create a new storage account endpoint **spfxsamples.blob.core.windows.net**.</span></span> 

> [!NOTE]
> <span data-ttu-id="e25b4-119">Sie müssen einen eindeutigen Speicherkontonamen für Ihre eigenen SharePoint-Framework-Projekte erstellen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-119">Note: You will need to create a unique storage name for your SharePoint Framework project.</span></span>

### <a name="blob-container-name"></a><span data-ttu-id="e25b4-120">Name des BLOB-Containers</span><span class="sxs-lookup"><span data-stu-id="e25b4-120">BLOB container name</span></span>

<span data-ttu-id="e25b4-p104">Erstellen Sie einen neuen Blob-Dienstcontainer. Dieser ist im Dashboard des Speicherkontos verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e25b4-p104">Create a new Blob service container. This will be available in your storage account dashboard.</span></span>

<span data-ttu-id="e25b4-123">Wählen Sie **+ Container** aus, und erstellen Sie einen neuen Container mit den folgenden Angaben:</span><span class="sxs-lookup"><span data-stu-id="e25b4-123">Select the **+ Container** and create a new container with the following:</span></span>

* <span data-ttu-id="e25b4-124">Name: **azurehosted-webpart**</span><span class="sxs-lookup"><span data-stu-id="e25b4-124">Name: **azurehosted-webpart**</span></span>
* <span data-ttu-id="e25b4-125">Zugriffstyp: Container</span><span class="sxs-lookup"><span data-stu-id="e25b4-125">Access type: Container</span></span>

![Bild, das die Option zum Erstellen von Blob-Containern zeigt](../../../images/deploy-option-blob-container.png)

### <a name="storage-account-access-key"></a><span data-ttu-id="e25b4-127">Tastenkombination für Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="e25b4-127">Storage account access key</span></span>

<span data-ttu-id="e25b4-128">Wählen Sie im Dashboard des Speicherkontos die Option **Tastenkombination** im Dashboard aus, und kopieren Sie eine der Tastenkombinationen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-128">In the storage account dashboard, choose **Access Key** in the dashboard and copy one of the access keys.</span></span>

![Bild, das die Tastenkombination für das Speicherkonto zeigt](../../../images/deploy-storage-account-accesskey.png)

### <a name="cdn-profile-and-endpoint"></a><span data-ttu-id="e25b4-130">CDN-Profil und Endpunkt</span><span class="sxs-lookup"><span data-stu-id="e25b4-130">CDN profile and endpoint</span></span>

<span data-ttu-id="e25b4-131">Erstellen Sie ein neues CDN-Profil, und weisen Sie den CDN-Endpunkt diesem BLOB-Container zu.</span><span class="sxs-lookup"><span data-stu-id="e25b4-131">Create a new CDN profile and associate the CDN endpoint with this BLOB container.</span></span>

<span data-ttu-id="e25b4-132">Erstellen Sie ein neues CDN-Profil, wie unter [Schritt 2: Erstellen eines neuen CDN-Profils](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-2-create-a-new-cdn-profile) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="e25b4-132">Create a new CDN profile as described in [Step 2: Create a new CDN profile](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-2-create-a-new-cdn-profile).</span></span>

<span data-ttu-id="e25b4-133">Im folgenden Screenshot ist **spfxwebparts** der Name des CDN-Profils.</span><span class="sxs-lookup"><span data-stu-id="e25b4-133">For example, in the following screenshot, **spfxwebparts** is the CDN profile name.</span></span>

![Screenshot zur Erstellung eines neuen CDN-Profils](../../../images/deploy-create-cdn-profile.png)

<span data-ttu-id="e25b4-135">Erstellen Sie einen CND-Endpunkt, wie unter [Schritt 3: Erstellen eines neuen CDN-Endpunkts](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-3-create-a-new-cdn-endpoint) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="e25b4-135">Create a CDN endpoint as described in [Step 3: Create a new CDN endpoint](https://azure.microsoft.com/de-DE/documentation/articles/cdn-create-a-storage-account-with-cdn/#step-3-create-a-new-cdn-endpoint).</span></span>

<span data-ttu-id="e25b4-136">Im folgenden Screenshot ist **spfxsamples** beispielsweise der Endpunktname **Speicher** ist der Ursprungstyp, und **spfxsamples.blob.core.windows.net** ist das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="e25b4-136">For example, in the following screenshot, **spfxsamples** is the endpoint name, **Storage** is the origin type, and **spfxsamples.blob.core.windows.net** is the storage account.</span></span>

![Screenshot zum Erstellen eines CDN-Endpunkts](../../../images/deploy-create-cdn-endpoint.png)

<span data-ttu-id="e25b4-138">Der CDN-Endpunkt wird mit folgender URL erstellt: http://spfxsamples.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="e25b4-138">The CDN endpoint will be created with the following URL: http://spfxsamples.azureedge.net</span></span>

<span data-ttu-id="e25b4-139">Da Sie den CDN-Endpunkt dem Speicherkonto zugewiesen haben, können Sie auch unter der folgenden URL auf den BLOB-Container zugreifen: http://spfxsamples.azureedge.net/azurehosted-webpart/</span><span class="sxs-lookup"><span data-stu-id="e25b4-139">Because you associated the CDN endpoint with your storage account, you can also access the BLOB container at the following URL:http://spfxsamples.azureedge.net/helloworld-webpart/</span></span>

<span data-ttu-id="e25b4-140">Beachten Sie jedoch, dass Sie die Dateien noch nicht bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="e25b4-140">Note, however that you have not yet deployed the files.</span></span>

## <a name="creating-a-new-web-part-project"></a><span data-ttu-id="e25b4-141">Erstellen eines neuen Webpartprojekts</span><span class="sxs-lookup"><span data-stu-id="e25b4-141">Creating a new Web Part project</span></span>

<span data-ttu-id="e25b4-142">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="e25b4-142">Create a new project directory in your preferred location:</span></span>

```
md azurehosted-webpart
```

<span data-ttu-id="e25b4-143">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="e25b4-143">Go to the project directory:</span></span>

```
cd azurehosted-webpart
```

<span data-ttu-id="e25b4-144">Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue SharePoint Framework-Lösung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-144">Create a new SharePoint Framework solution by running Yeoman SharePoint Generator:</span></span>

```
yo @microsoft/sharepoint
```
    
<span data-ttu-id="e25b4-145">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="e25b4-145">When prompted:</span></span>

* <span data-ttu-id="e25b4-146">Akzeptieren Sie den Standardnamen **azurehosted-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-146">Accept the default **jquery-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="e25b4-147">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-147">Choose **SharePoint Online only (latest)**, and press **Enter**.</span></span>
* <span data-ttu-id="e25b4-148">Wählen Sie als Speicherort für die Dateien die Option **Use the current folder** aus.</span><span class="sxs-lookup"><span data-stu-id="e25b4-148">Select **Use the current folder** for where to place the files.</span></span>
* <span data-ttu-id="e25b4-149">Wählen Sie **y**, um die mandatenweite Bereitstellung zu verwenden, mit der das Webpart auf allen Websites zur Verfügung steht, sobald es bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="e25b4-149">Choose **y** to use the tenant-scoped deployment option, which makes web part available across sites immediately when it's deployed.</span></span> 
* <span data-ttu-id="e25b4-150">Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="e25b4-150">Choose **Webpart** as the client-side component type to be created.</span></span> 

<span data-ttu-id="e25b4-151">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="e25b4-151">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="e25b4-152">Verwenden Sie **AzureCDN** als Namen des Webparts, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-152">Use **DocumentCardExample** for your web part name and choose **Enter**.</span></span>
* <span data-ttu-id="e25b4-153">Akzeptieren Sie die Standardbeschreibung **AzureCDN description** als Beschreibung für Ihr Webpart, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-153">Accept the default **HelloWorld description** as your web part description and choose **Enter**.</span></span>
* <span data-ttu-id="e25b4-154">Akzeptieren Sie die Standardeinstellung **No javaScript web framework** als das zu verwendende Framework, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-154">Accept the default **No javascript web framework** as the framework you would like to use and choose **Enter**.</span></span>

![Yeoman-Generator-Fragen für das neu erstellte Webpart](../../../images/cdn-azure-create-webpart-yo.png)

<span data-ttu-id="e25b4-p105">An diesem Punkt erstellt Yeoman ein Gerüst für die Lösungsdateien und installiert die erforderlichen Abhängigkeiten. Das kann einige Minuten dauern. Yeoman nimmt auch Ihr benutzerdefiniertes Webpart in das Projektgerüst auf.</span><span class="sxs-lookup"><span data-stu-id="e25b4-p105">At this point, Yeoman will scaffold the solution files and install the required dependencies. This might take a few minutes. Yeoman will scaffold the project to include your custom web part as well.</span></span>

<span data-ttu-id="e25b4-159">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-159">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="e25b4-160">Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-160">Next, type the following to open the web part project in Visual Studio Code:</span></span>

```
code .
```

## <a name="configure-solution-not-to-use-default-settings"></a><span data-ttu-id="e25b4-161">Konfigurieren der Lösung für die Nichtverwendung der Standardeinstellungen</span><span class="sxs-lookup"><span data-stu-id="e25b4-161">Configure solution not to use default settings</span></span>

<span data-ttu-id="e25b4-162">Öffnen Sie **deploy-azure-storage.json** im Ordner **config**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-162">Open **deploy-azure-storage.json** in the **config** folder.</span></span>

<span data-ttu-id="e25b4-163">Hier werden die Lösungspakete gesteuert.</span><span class="sxs-lookup"><span data-stu-id="e25b4-163">This is where we control the solution packaging.</span></span>

<span data-ttu-id="e25b4-164">Ändern Sie den `includeClientSideAssets`-Wert zu **false**, damit clientseitige Objekte nicht in die .sppkg-Datei gepackt werden, was dem Standardverhalten entspricht.</span><span class="sxs-lookup"><span data-stu-id="e25b4-164">Update `includeClientSideAssets` value as **false** so that client-side assets are NOT packaged inside of the sppkg file, which is the default behavior.</span></span> <span data-ttu-id="e25b4-165">Da Objekte aus dem externen CDN gehostet werden, sollen sie nicht im dem Lösungspaket enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="e25b4-165">Since we are hosting assets from external CDN, we do not want them to be included in the solution package.</span></span> <span data-ttu-id="e25b4-166">Die Konfiguration könnte wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-166">Your configuration should look somewhat following.</span></span>

``` json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "azurehosted-webpart-client-side-solution",
    "id": "a4e95ed1-d096-4573-8a57-d0cc3b52da6a",
    "version": "1.0.0.0",
    "includeClientSideAssets": false,
    "skipFeatureDeployment": true
  },
  "paths": {
    "zippedPackage": "solution/azurehosted-webpart.sppkg"
  }
}
```

> [!NOTE]
> <span data-ttu-id="e25b4-167">`skipFeatureDeployment`-Einstellung lautet **true**, da die Antwort für die mandantenweite Bereitstellung in dem Yeoman-Ablauf „y“ lautete.</span><span class="sxs-lookup"><span data-stu-id="e25b4-167">`skipFeatureDeployment` setting is here **true** since answer for the tenant-scope deployment option was said to be 'y' in the Yeoman flow.</span></span> <span data-ttu-id="e25b4-168">Dies bedeutet, dass Sie die Lösung erst auf der Website installieren müssen, wenn das Webpart verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="e25b4-168">This means that you do NOT need to explicitly install solution to the site before web part is available.</span></span> <span data-ttu-id="e25b4-169">Die Bereitstellung und Genehmigung des Lösungspakets in dem App-Katalog des Mandanten reicht aus, damit das Webpart auf allen Websites in dem jeweiligen Mandanten zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="e25b4-169">Deploying and approving solution package in tenant app catalog is sufficient to make web part available cross all the sites in the given tenant.</span></span>


## <a name="configure-azure-storage-account-details"></a><span data-ttu-id="e25b4-170">Konfigurieren der Details eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="e25b4-170">Configure Azure Storage account details</span></span>

<span data-ttu-id="e25b4-171">Öffnen Sie **deploy-azure-storage.json** im Ordner **config**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-171">Open **deploy-azure-storage.json** in the **config** folder.</span></span>

<span data-ttu-id="e25b4-172">Das ist die Datei, die die Details zu Ihrem Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="e25b4-172">This is the file that contains your Azure Storage account details.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/deploy-azure-storage.schema.json",
  "workingDir": "./temp/deploy/",
  "account": "<!-- STORAGE ACCOUNT NAME -->",
  "container": "azurehosted-webpart",
  "accessKey": "<!-- ACCESS KEY -->"
}
```

<span data-ttu-id="e25b4-173">Ersetzen Sie **Konto**, **Container** und **accessKey** jeweils mit dem Speicherkontonamen, dem BLOB-Container und der Tastenkombination für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="e25b4-173">Replace the **account**, **container**, **accessKey** with your storage account name, BLOB container and storage account access key respectively.</span></span>

<span data-ttu-id="e25b4-174">**workingDir** ist das Verzeichnis, in dem sich die Webpartressourcen befinden.</span><span class="sxs-lookup"><span data-stu-id="e25b4-174">**workingDir** is the directory where the web part assets will be located.</span></span>

<span data-ttu-id="e25b4-175">In diesem Beispiel sieht diese Datei mit dem zuvor erstellten Speicherkonto wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="e25b4-175">In this example, with the storage account created earlier, this file will look like:</span></span>

```json
{
  "workingDir": "./temp/deploy/",
  "account": "spfxsamples",
  "container": "azurehosted-webpart",
  "accessKey": "q1UsGWocj+CnlLuv9ZpriOCj46ikgBbDBCaQ0FfE8+qKVbDTVSbRGj41avlG73rynbvKizZpIKK9XpnpA=="
}
```

<span data-ttu-id="e25b4-176">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="e25b4-176">Save the file.</span></span>

## <a name="configuring-web-part-to-load-from-cdn"></a><span data-ttu-id="e25b4-177">Konfigurieren von Webparts, die aus dem CDN geladen werden</span><span class="sxs-lookup"><span data-stu-id="e25b4-177">Configuring web part to load from CDN</span></span>

<span data-ttu-id="e25b4-178">Damit das Webpart aus Ihrem CDN geladen wird, müssen Sie ihm den CDN-Pfad mitteilen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-178">In order for the web part to load from your CDN, you will need to tell it your CDN path.</span></span>

<span data-ttu-id="e25b4-179">Wechseln Sie zu Visual Studio Code, und öffnen Sie **write-manifests.json** aus dem Ordner **config**.</span><span class="sxs-lookup"><span data-stu-id="e25b4-179">Switch to Visual Studio Code and open the **write-manifests.json** from the **config** folder.</span></span>

<span data-ttu-id="e25b4-180">Geben Sie den Pfad der CDN-Basis für die **cdnBasePath**-Eigenschaft ein.</span><span class="sxs-lookup"><span data-stu-id="e25b4-180">Enter your CDN base path for the **cdnBasePath** property.</span></span>

```json
{
  "cdnBasePath": "<!-- PATH TO CDN -->"
}
```

<span data-ttu-id="e25b4-181">In diesem Beispiel sieht diese Datei mit dem zuvor erstellten CDN-Profil wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="e25b4-181">In this example, with the CDN profile created earlier, this file will look like:</span></span>

```json
{
  "cdnBasePath": "https://spfxsamples.azureedge.net/azurehosted-webpart/"
}
```

> [!NOTE]
> <span data-ttu-id="e25b4-182">Der CDN-Basispfad ist der CDN-Endpunkt mit dem BLOB-Container.</span><span class="sxs-lookup"><span data-stu-id="e25b4-182">Note: The CDN base path is the CDN endpoint with the BLOB container.</span></span>

<span data-ttu-id="e25b4-183">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="e25b4-183">Save the file.</span></span>


## <a name="prepare-web-part-assets-to-deploy"></a><span data-ttu-id="e25b4-184">Vorbereiten der bereitzustellenden Webpartressourcen</span><span class="sxs-lookup"><span data-stu-id="e25b4-184">Prepare web part assets to deploy</span></span>

<span data-ttu-id="e25b4-185">Bevor Sie die Ressourcen in das CDN hochladen, müssen Sie sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-185">Before uploading the assets to CDN, you need to build them.</span></span>

<span data-ttu-id="e25b4-186">Wechseln Sie zur Konsole, und führen Sie die folgenden `gulp`-Aufgabe aus:</span><span class="sxs-lookup"><span data-stu-id="e25b4-186">Switch to the console and execute the following `gulp` task:</span></span>

```
gulp bundle --ship
```

<span data-ttu-id="e25b4-187">Dadurch werden die minimierten Ressourcen erstellt, die zum Hochladen an den CDN-Anbieter erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="e25b4-187">This will build the minified assets required to upload to the CDN provider.</span></span> <span data-ttu-id="e25b4-188">In `--ship` ist das Buildtool zum Erstellen für die Verteilung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-188">The `--ship` indicates the build tool to build for distribution.</span></span> <span data-ttu-id="e25b4-189">Beachten Sie außerdem die Ausgabe der Buildtools, die angibt, dass das Build-Ziel SHIP ist.</span><span class="sxs-lookup"><span data-stu-id="e25b4-189">This will build the minified assets required to upload to the CDN provider. The  indicates the build tool to build for distribution. You should also notice the output of the build tools indicate the Build Target is SHIP.</span></span>

```
Build target: SHIP
[21:23:01] Using gulpfile ~/apps/azurehosted-webpart/gulpfile.js
[21:23:01] Starting gulp
[21:23:01] Starting 'default'...
```

<span data-ttu-id="e25b4-190">Die minimierten Ressourcen befinden sich im `temp\deploy`-Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="e25b4-190">The minified assets can be found under the `temp\deploy` directory.</span></span>

## <a name="deploy-assets-to-azure-storage"></a><span data-ttu-id="e25b4-191">Bereitstellen von Ressourcen für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e25b4-191">Deploy assets to Azure Storage</span></span>

<span data-ttu-id="e25b4-192">Wechseln Sie zur Konsole des **azurehosted-webpart**-Projektverzeichnisses.</span><span class="sxs-lookup"><span data-stu-id="e25b4-192">Switch to the console of the **HelloWorld** project directory.</span></span>

<span data-ttu-id="e25b4-193">Geben Sie die gulp-Aufgabe an, um die Ressourcen in Ihrem Speicherkonto bereitzustellen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-193">Enter the gulp task to deploy the assets to your storage account:</span></span>

```
gulp deploy-azure-storage
```

<span data-ttu-id="e25b4-194">Dadurch wird das Webpartbundle zusammen mit anderen Ressourcen wie JavaScript- und CSS-Dateien im CDN bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-194">This will deploy the web part bundle along with other assets like JavaScript and CSS files to the CDN.</span></span>

## <a name="deploy-the-updated-package"></a><span data-ttu-id="e25b4-195">Bereitstellen des aktualisierten Pakets</span><span class="sxs-lookup"><span data-stu-id="e25b4-195">Deploy the updated package</span></span>

### <a name="package-the-solution"></a><span data-ttu-id="e25b4-196">Verpacken der Lösung</span><span class="sxs-lookup"><span data-stu-id="e25b4-196">Package the solution</span></span>

<span data-ttu-id="e25b4-197">Da Sie das Webpartbundle geändert haben, müssen Sie das Paket erneut im App-Katalog bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-197">Because you changed the web part bundle, you will need to re-deploy the package to the App Catalog. You used --ship to generate minified assets for distribution.</span></span> <span data-ttu-id="e25b4-198">Sie haben **--ship** verwendet, um minimierte Ressourcen für die Verteilung zu generieren.</span><span class="sxs-lookup"><span data-stu-id="e25b4-198">You used **--ship** to generate minified assets for distribution.</span></span>

<span data-ttu-id="e25b4-199">Wechseln Sie zur Konsole des **azurehosted-webpart**-Projektverzeichnisses.</span><span class="sxs-lookup"><span data-stu-id="e25b4-199">Switch to the console of the **HelloWorld** project directory.</span></span>

<span data-ttu-id="e25b4-200">Geben Sie die gulp-Aufgabe zum Verpacken der clientseitigen Lösung an, dieses Mal mit gesetztem `--ship`-Flag.</span><span class="sxs-lookup"><span data-stu-id="e25b4-200">Enter the gulp task to package the client-side solution, this time with the `--ship` flag set. This forces the task to pick up the CDN base path configured in the previous step:</span></span> <span data-ttu-id="e25b4-201">Dadurch wird die Aufgabe gezwungen, den im vorherigen Schritt konfigurierten CDN-Basispfad aufzugreifen:</span><span class="sxs-lookup"><span data-stu-id="e25b4-201">Enter the gulp task to package the client-side solution, this time with the  flag set. This forces the task to pick up the CDN base path configured in the previous step:</span></span>

```
gulp package-solution --ship
```

<span data-ttu-id="e25b4-202">Dadurch wird das aktualisierte clientseitige Lösungspaket im Ordner **sharepoint\solution** erstellt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-202">This will create the updated client-side solution package in the **sharepoint\solution** folder.</span></span>

### <a name="upload-to-your-app-catalog"></a><span data-ttu-id="e25b4-203">Hochladen in den App-Katalog</span><span class="sxs-lookup"><span data-stu-id="e25b4-203">Upload to your App Catalog</span></span>

<span data-ttu-id="e25b4-204">Laden Sie das clientseitige Lösungspaket in den App-Catalog hoch, oder verwenden Sie Drag & Drop.</span><span class="sxs-lookup"><span data-stu-id="e25b4-204">Upload or drag & drop the client-side solution package to the App Catalog.</span></span> <span data-ttu-id="e25b4-205">Beachten Sie, dass die URL auf die in den vorherigen Schritten konfigurierte URL des Azure CDN verweist.</span><span class="sxs-lookup"><span data-stu-id="e25b4-205">Notice how the URL is pointing to the Azure CDN URL configured in the previous steps.</span></span> 

<span data-ttu-id="e25b4-206">**Aktivieren Sie das Kontrollkästchen**, das angibt, dass die Lösung automatisch auf allen Websites in der Organisation bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e25b4-206">**Click checkbox** on indicating that solution can be deployed automatically available cross all sites in the organization.</span></span>

![Screenshot der Aufforderung für die Vertrauensstellung zum clientseitigen Lösungspaket](../../../images/cdn-azure-trust-hosted-app-catalog.png)

<span data-ttu-id="e25b4-208">Wählen Sie **Bereitstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="e25b4-208">Choose **Deploy**</span></span>

<span data-ttu-id="e25b4-209">Der App-Katalog verfügt nun über das clientseitige Lösungspaket, in das das Webpartbundle aus dem CDN geladen wird.</span><span class="sxs-lookup"><span data-stu-id="e25b4-209">The App Catalog will now have the latest client-side solution package where the web part bundle is loaded from the CDN.</span></span>

## <a name="test-the-helloworld-web-part"></a><span data-ttu-id="e25b4-210">Testen des HelloWorld-Webparts</span><span class="sxs-lookup"><span data-stu-id="e25b4-210">Test the HelloWorld web part</span></span>

<span data-ttu-id="e25b4-211">Wechseln Sie zu einer beliebigen SharePoint-Website in Ihrem Mandanten, und wählen Sie **Seite hinzufügen** in dem Menü mit dem *Zahnrad*.</span><span class="sxs-lookup"><span data-stu-id="e25b4-211">Go to any SharePoint site in your tenant and choose **Add a page** from the *gears* menu.</span></span>

<span data-ttu-id="e25b4-212">**Bearbeiten** Sie die Seite, und wählen Sie das **AzureCDN**-Webpart in der Webpartauswahl, um zu bestätigen, dass die Bereitstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="e25b4-212">**Edit** the page and select **AzureCDN** web part from the web part picker to confirm that your deployment has been successful.</span></span>

![Screenshot der Aufforderung für die Vertrauensstellung zum clientseitigen Lösungspaket](../../../images/cdn-azure-picker-selection-page.png)

<span data-ttu-id="e25b4-214">Beachten Sie, dass **gulp serve** nicht ausgeführt wird und dass deshalb nichts von **localhost** kommt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-214">Notice that you are no longer running **gulp serve**, and therefore nothing is served from **localhost**.</span></span> <span data-ttu-id="e25b4-215">Inhalt wird vom Azure CDN bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e25b4-215">Content is served from the Azure CDN.</span></span> <span data-ttu-id="e25b4-216">Sie können dies auch prüfen, indem Sie in Ihrem Browser F12 drücken und sicherstellen, dass das Azure CDN als Quelle für die Seitenobjekte angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="e25b4-216">You can also double check this by pressing F12 in your browser and confirm that you can see the Azure CDN as one of the sources for the page assets.</span></span>

![Quellen mit der URL des Azure CDN](../../../images/cdn-azure-sources-browser-dev-tools.png)

## <a name="deploying-to-other-cdns"></a><span data-ttu-id="e25b4-218">Bereitstellen auf anderen CDNs</span><span class="sxs-lookup"><span data-stu-id="e25b4-218">Deploying to other CDNs</span></span>

<span data-ttu-id="e25b4-219">Um die Ressourcen auf Ihrem bevorzugten CDN-Anbieter bereitzustellen, können Sie die Dateien aus dem Ordner **tmp\deploy** kopieren.</span><span class="sxs-lookup"><span data-stu-id="e25b4-219">In order to deploy the assets to your favorite CDN provider, you can copy the files from **temp\deploy** folder. To generate assets for distribution you will run the following gulp command as we did before with the --ship parameter:</span></span> <span data-ttu-id="e25b4-220">Zum Generieren der Ressourcen für die Verteilung führen Sie den folgenden gulp-Befehl so aus wie zuvor den **--ship**-Parameter:</span><span class="sxs-lookup"><span data-stu-id="e25b4-220">In order to deploy the assets to your favorite CDN provider, you can copy the files from temp\deploy folder. To generate assets for distribution you will run the following gulp command as we did before with the **--ship** parameter:</span></span>

```
gulp bundle --ship
```

<span data-ttu-id="e25b4-221">Solange Sie die **cdnBasePath**-Eigenschaft entsprechend aktualisieren, werden Ihre Dateien ordnungsgemäß geladen.</span><span class="sxs-lookup"><span data-stu-id="e25b4-221">As long as you are updating the **cdnBasePath** accordingly, your files are being properly loaded.</span></span>

> [!NOTE]
> <span data-ttu-id="e25b4-222">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="e25b4-222">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="e25b4-223">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="e25b4-223">Thanks for your input advance.</span></span>