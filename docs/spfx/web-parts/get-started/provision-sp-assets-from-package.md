---
title: Bereitstellen von SharePoint-Ressourcen aus Ihrem clientseitigen SharePoint-Webpart
description: "SharePoint-Objekte können im Rahmen der SharePoint Framework-Lösung bereitgestellt werden und werden auf SharePoint-Websites bereitgestellt, wenn die Lösung darauf installiert wird."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 48a5262c322c74028abc10054b321bff104a3b24
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="provision-sharepoint-assets-from-your-sharepoint-client-side-web-part"></a><span data-ttu-id="5e307-103">Bereitstellen von SharePoint-Ressourcen aus Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="5e307-103">Provisioning SharePoint assets from your SharePoint client-side web part</span></span>

<span data-ttu-id="5e307-104">SharePoint-Objekte können im Rahmen der SharePoint Framework-Lösung bereitgestellt werden und werden auf SharePoint-Websites bereitgestellt, wenn die Lösung darauf installiert wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-104">SharePoint assets can be provisioned as part of the SharePoint Framework solution, and are deployed to SharePoint sites when the solution is installed on it.</span></span> 

<span data-ttu-id="5e307-105">Bevor Sie beginnen, führen Sie die Schritte in den folgenden Artikeln aus, um sicherzustellen, dass Sie den grundlegenden Fluss des Erstellens eines benutzerdefinierten, clientseitigen Webparts verstehen:</span><span class="sxs-lookup"><span data-stu-id="5e307-105">Before you start, complete the procedures in the following articles to ensure that you understand the basic flow of creating a custom client-side web part:</span></span>

* [<span data-ttu-id="5e307-106">Erstellen des ersten Webparts</span><span class="sxs-lookup"><span data-stu-id="5e307-106">Build your first web part</span></span>](build-a-hello-world-web-part.md)
* [<span data-ttu-id="5e307-107">Verbinden des Webparts mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="5e307-107">Connect your client-side web part to SharePoint</span></span>](connect-to-sharepoint.md) 

<span data-ttu-id="5e307-108">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=qAqNk_X82QM&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=8) nachvollziehen.</span><span class="sxs-lookup"><span data-stu-id="5e307-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=qAqNk_X82QM&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=8).</span></span> 

<a href="https://www.youtube.com/watch?v=qAqNk_X82QM&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=8">
<img src="../../../images/spfx-youtube-tutorial7.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a><span data-ttu-id="5e307-109">Erstellen eines neuen Webpart-Projekts</span><span class="sxs-lookup"><span data-stu-id="5e307-109">Create a new web part project</span></span>

1. <span data-ttu-id="5e307-110">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="5e307-110">Create a new project directory in your favorite location:</span></span>

  ```
  md asset-deployment-webpart
  ```

2. <span data-ttu-id="5e307-111">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="5e307-111">Go to the project directory:</span></span>

  ```
  cd asset-deployment-webpart
  ```
    
3. <span data-ttu-id="5e307-112">Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue clientseitige Webpartlösung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="5e307-112">Create a new client-side web part solution by running the Yeoman SharePoint Generator:</span></span>

  ```
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="5e307-113">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="5e307-113">When prompted:</span></span>

  * <span data-ttu-id="5e307-114">Akzeptieren Sie den Standardnamen **asset-deployment-webpart** als Lösungsnamen, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="5e307-114">Accept the default asset-deployment-webpart as your solution name and choose Enter.</span></span>
  * <span data-ttu-id="5e307-115">Wählen Sie **SharePoint Online only (latest)** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="5e307-115">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
  * <span data-ttu-id="5e307-116">Wählen Sie die Option **Use the current folder** als Speicherort für die Dateien aus.</span><span class="sxs-lookup"><span data-stu-id="5e307-116">Select **Use the current folder** as the location for the files.</span></span>
  * <span data-ttu-id="5e307-117">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-117">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
  * <span data-ttu-id="5e307-118">Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="5e307-118">Select **Extension** as the client-side component type to be created.</span></span> 

5. <span data-ttu-id="5e307-119">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="5e307-119">The next set of prompts will ask for specific information about your web part:</span></span>

  * <span data-ttu-id="5e307-120">Geben Sie **AssetDeployment** als Namen des Webparts ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="5e307-120">Type AssetDeployment for the web part name and choose Enter.</span></span>
  * <span data-ttu-id="5e307-121">Geben Sie **AssetDeployment-Webpart** als Beschreibung des Webparts ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="5e307-121">Enter AssetDeployment Web Part as the description of the web part and choose Enter.</span></span> 
  * <span data-ttu-id="5e307-122">Akzeptieren Sie die Standardeinstellung **No javascript web framework** als Framework, und drücken Sie dann die EINGABETASTE, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="5e307-122">Accept the default No JavaScipt web framework option for the framework and choose Enter to continue.</span></span>

  ![Yeoman-Eingabeaufforderungen](../../../images/asset-deployment-yeoman.png)

  <span data-ttu-id="5e307-124">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien.</span><span class="sxs-lookup"><span data-stu-id="5e307-124">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the HelloWorld extension.</span></span> <span data-ttu-id="5e307-125">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="5e307-125">This might take a few minutes.</span></span> <span data-ttu-id="5e307-126">Yeoman erstellt ein Gerüst für das Projekt, um auch das **AssetDeployment**-Webpart einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="5e307-126">Yeoman scaffolds the project to include your **AssetDeployment** web part as well.</span></span>

6. <span data-ttu-id="5e307-127">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="5e307-127">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

7. <span data-ttu-id="5e307-128">Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="5e307-128">Next, type the following to open the web part project in Visual Studio Code:</span></span>

  ```
  code .
  ```

## <a name="create-folder-structure-for-your-sharepoint-assets"></a><span data-ttu-id="5e307-129">Erstellen der Ordnerstruktur für Ihre SharePoint-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5e307-129">Create folder structure for your SharePoint assets</span></span>

<span data-ttu-id="5e307-130">Wir müssen zuerst einen **Ressourcen**ordner erstellen, in dem die gesamten Featureframeworkressourcen platziert werden, die zum Bereitstellen von SharePoint-Strukturen verwendet werden, wenn das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-130">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when package is installed.</span></span>

1. <span data-ttu-id="5e307-131">Erstellen Sie einen Ordner mit dem Namen **Sharepoint** auf der Stammebene der Lösung.</span><span class="sxs-lookup"><span data-stu-id="5e307-131">Create folder called **sharepoint** to the root of the solution</span></span>

2. <span data-ttu-id="5e307-132">Erstellen Sie einen Ordner mit dem Namen **Ressourcen** als Unterordner für den soeben erstellten **Sharepoint**-Ordner</span><span class="sxs-lookup"><span data-stu-id="5e307-132">Create folder called **assets** as a sub folder for the just created **sharepoint** folder</span></span>

  <span data-ttu-id="5e307-133">Die Lösungsstruktur sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="5e307-133">Your solution structure should look similar to the following picture:</span></span>

  ![Screenshot, in dem der Ressourcenordner unter dem SharePoint-Ordner in der Lösungsstruktur angezeigt wird](../../../images/tutorial-feature-solution-initial-structure.png)


## <a name="create-feature-framework-files-for-initial-deployment"></a><span data-ttu-id="5e307-135">Erstellen von Featureframeworkdateien für die anfängliche Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="5e307-135">Create feature framework files for initial deployment</span></span>

<span data-ttu-id="5e307-136">Um SharePoint-Ressourcen auf Websites mit Featureframeworkelementen bereitstellen zu können, müssen wir die erforderlichen XML-Dateien für den Ressourcenordner erstellen.</span><span class="sxs-lookup"><span data-stu-id="5e307-136">To be able to provision SharePoint assets to sites with feature framework elements, we'll need to create needed xml files to the asset folder. Supported elements for the SharePoint Framework solution packages are following:</span></span> <span data-ttu-id="5e307-137">Unterstützte Elemente für die SharePoint Framework-Lösungspakete sind wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5e307-137">Supported elements for the SharePoint Framework solution packages are following:</span></span>

* <span data-ttu-id="5e307-138">Felder/Websitespalten</span><span class="sxs-lookup"><span data-stu-id="5e307-138">Fields / Site columns</span></span>
* <span data-ttu-id="5e307-139">Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="5e307-139">Content types</span></span>
* <span data-ttu-id="5e307-140">Listeninstanzen</span><span class="sxs-lookup"><span data-stu-id="5e307-140">List instances</span></span>
* <span data-ttu-id="5e307-141">Listeninstanzen mit benutzerdefiniertem Schema</span><span class="sxs-lookup"><span data-stu-id="5e307-141">List instances with custom schema</span></span>

<span data-ttu-id="5e307-142">In den folgenden Schritten wird die erforderliche Struktur definiert, die bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="5e307-142">In following steps, we'll define the needed structure to be provisioned.</span></span>

### <a name="to-add-an-elementxml-file-for-sharepoint-definitions"></a><span data-ttu-id="5e307-143">So fügen Sie die Datei „elements.xml“ für SharePoint-Definitionen hinzu</span><span class="sxs-lookup"><span data-stu-id="5e307-143">To add an element.xml file for SharePoint definitions</span></span>

1. <span data-ttu-id="5e307-144">Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-144">Create a new file inside the **sharepoint\assets** folder named **elements.xml**</span></span>

2. <span data-ttu-id="5e307-145">Kopieren Sie die folgende XML-Struktur in **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-145">Copy the following xml structure into **elements.xml**.</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">

      <Field ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}"
              Name="SPFxAmount"
              DisplayName="Amount"
              Type="Currency"
              Decimals="2"
              Min="0"
              Required="FALSE"
              Group="SPFx Columns" />

      <Field ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}"
              Name="SPFxCostCenter"
              DisplayName="Cost Center"
              Type="Choice"
              Required="FALSE"
              Group="SPFx Columns">
          <CHOICES>
          <CHOICE>Administration</CHOICE>
          <CHOICE>Information</CHOICE>
          <CHOICE>Facilities</CHOICE>
          <CHOICE>Operations</CHOICE>
          <CHOICE>Sales</CHOICE>
          <CHOICE>Marketing</CHOICE>
          </CHOICES>
      </Field>

      <ContentType ID="0x010042D0C1C200A14B6887742B6344675C8B" 
              Name="Cost Center" 
              Group="SPFx Content Types" 
              Description="Sample content types from web part solution">
          <FieldRefs>
              <FieldRef ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}" /> 
              <FieldRef ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}" />
          </FieldRefs>
      </ContentType> 

      <ListInstance 
              CustomSchema="schema.xml"
              FeatureId="00bfea71-de22-43b2-a848-c05709900100"
              Title="SPFx List" 
              Description="SPFx List"
              TemplateType="100"
              Url="Lists/SPFxList">
      </ListInstance>

  </Elements>
  ```

  <span data-ttu-id="5e307-146">Beachten Sie zu der eingefügten XML-Struktur Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5e307-146">Note the following about the pasted XML structure:</span></span>
  * <span data-ttu-id="5e307-147">Wir stellen zwei Felder, den Inhaltstyp und eine Listeninstanz mit benutzerdefiniertem Schema auf der Website bereit.</span><span class="sxs-lookup"><span data-stu-id="5e307-147">We are provisioning two fields, content type and a list instance with custom schema to the site</span></span>
  * <span data-ttu-id="5e307-148">Definitionen verwenden das Standardschema für das Featureframework, das SharePoint-Entwickler gut kennen.</span><span class="sxs-lookup"><span data-stu-id="5e307-148">Definitions are using standard Feature Framework schema, which is well known for SharePoint developers</span></span>
  * <span data-ttu-id="5e307-149">Auf benutzerdefinierte Felder wird in dem eingeführten Inhaltstyp verwiesen.</span><span class="sxs-lookup"><span data-stu-id="5e307-149">Custom fields are being referenced in the introduced content type</span></span>
  * <span data-ttu-id="5e307-150">Wir verwenden das **CustomSchema**-Attribut im **ListInstance**-Element, um die Bereitstellungszeit der schema.xml-Datei für die Liste zu definieren.</span><span class="sxs-lookup"><span data-stu-id="5e307-150">We use the **CustomSchema** attribute in the **ListInstance** element to define a provisioning time schema.xml file for the list.</span></span> <span data-ttu-id="5e307-151">Auf diese Weise basiert die Liste immer noch auf der einsatzbereiten Listenvorlage (die normale benutzerdefinierte Liste „100“ in diesem Fall), es kann jedoch während der anfänglichen Bereitstellung eine alternative Bereitstellungsdefinition definiert werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-151">We use CustomSchema attribute in the ListInstance element to define provisioning time schema.xml file for the list. This way list is still based on out-of-the-box list template (Normal custom list '100' in this case), but we can define alternative provisioning definition during initial provisioning.</span></span>

  <span data-ttu-id="5e307-152">Weitere Informationen zu den verwendeten Schemastrukturen finden Sie unter [Verwenden von Funktionen in SharePoint Foundation](https://msdn.microsoft.com/en-us/library/office/ms460318(v=office.14).aspx) auf MSDN.</span><span class="sxs-lookup"><span data-stu-id="5e307-152">More details about the used schema structures can be found at [FUsing Features in SharePoint Foundation](https://msdn.microsoft.com/en-us/library/office/ms460318(v=office.14).aspx) on MSDN.</span></span>

### <a name="to-add-a-schemaxml-file-for-defining-list-structure"></a><span data-ttu-id="5e307-153">So fügen Sie die Datei „schema.xml“ zum Definieren der Listenstruktur hinzu</span><span class="sxs-lookup"><span data-stu-id="5e307-153">To add a schema.xml file for defining list structure</span></span>

<span data-ttu-id="5e307-154">Im vorherigen Schritt haben wir auf die Datei **schema.xml** im **CustomSchema**-Attribut des **ListInstance**-Elements verwiesen, dies muss also in das Paket eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-154">In previous step, we referenced **schema.xml** file in the **CustomSchema** attribute of the **ListInstance** element, so we'll need to include that in our package.</span></span> 

1. <span data-ttu-id="5e307-155">Erstellen Sie eine neue Datei innerhalb des Ordners **SharePoint\Ressourcen** mit dem Namen **schema.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-155">Create a new file inside the **sharepoint\assets** folder named as **schema.xml**</span></span>

2. <span data-ttu-id="5e307-156">Kopieren Sie die folgende XML-Struktur in **schema.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-156">Copy the following xml structure into **schema.xml**.</span></span>

  ```xml
  <List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE" Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
    <MetaData>
      <ContentTypes>
        <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
      </ContentTypes>
      <Fields></Fields>
      <Views>
        <View BaseViewID="1" Type="HTML" WebPartZoneID="Main" DisplayName="$Resources:core,objectiv_schema_mwsidcamlidC24;" DefaultView="TRUE" MobileView="TRUE" MobileDefaultView="TRUE" SetupPath="pages\viewpage.aspx" ImageUrl="/_layouts/images/generic.png" Url="AllItems.aspx">
          <XslLink Default="TRUE">main.xsl</XslLink>
          <JSLink>clienttemplates.js</JSLink>
          <RowLimit Paged="TRUE">30</RowLimit>
          <Toolbar Type="Standard" />
          <ViewFields>
            <FieldRef Name="LinkTitle"></FieldRef>
            <FieldRef Name="SPFxAmount"></FieldRef>
            <FieldRef Name="SPFxCostCenter"></FieldRef>
          </ViewFields>
          <Query>
            <OrderBy>
              <FieldRef Name="ID" />
            </OrderBy>
          </Query>
        </View>
      </Views>
      <Forms>
        <Form Type="DisplayForm" Url="DispForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
        <Form Type="EditForm" Url="EditForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
        <Form Type="NewForm" Url="NewForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      </Forms>
    </MetaData>
  </List>
  ```

<span data-ttu-id="5e307-157">Beachten Sie zu der eingefügten XML-Struktur Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5e307-157">Note the following about the included XML structure:</span></span>
* <span data-ttu-id="5e307-158">Auf den benutzerdefinierten Inhaltstyp, der unter Verwendung der Datei **elements.xml** bereitgestellt wird, wird im **ContentTypeRef**-Element verwiesen.</span><span class="sxs-lookup"><span data-stu-id="5e307-158">Custom content type deployed using **elements.xml** file is referenced in the **ContentTypeRef** element</span></span>
* <span data-ttu-id="5e307-159">Auf benutzerdefinierte Felder mit dem Namen **SPFxAmount** und **SPFxCostCenter** wird im **FieldRef**-Element verwiesen.</span><span class="sxs-lookup"><span data-stu-id="5e307-159">Custom fields called **SPFxAmount** and **SPFxCostCenter** are being referenced in the **FieldRef** element</span></span>

<span data-ttu-id="5e307-160">Weitere Einzelheiten zu den verwendeten Schemastrukturen finden Sie im Artikel [Grundlegendes zu Schema.xml-Dateien](https://msdn.microsoft.com/en-us/library/office/ms459356(v=office.14).aspx) auf MSDN.</span><span class="sxs-lookup"><span data-stu-id="5e307-160">More details on the used schema structures can be found from [Understanding Schema.xml Files](https://msdn.microsoft.com/en-us/library/office/ms459356(v=office.14).aspx) article at MSDN.</span></span>

## <a name="ensure-that-definitions-are-taken-into-use-in-build-pipeline"></a><span data-ttu-id="5e307-161">Sicherstellen, dass Definitionen in der Buildpipeline verwendet werden</span><span class="sxs-lookup"><span data-stu-id="5e307-161">Ensure that definitions are taken into use in build pipeline</span></span>

<span data-ttu-id="5e307-162">Nun haben wir die erforderlichen Strukturen für das Bereitstellen von SharePoint-Ressourcen automatisch aus der Lösung erstellt, wenn diese bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-162">Now we have created the needed structures for provisioning SharePoint assets automatically from the solution when it's deployed. Next step is to ensure that we package these xml files as part of the solution file.</span></span> <span data-ttu-id="5e307-163">Der nächste Schritt besteht darin, sicherzustellen, dass diese XML-Dateien als Teil der Lösungsdatei verpackt werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-163">The next step is to ensure that we package these XML files as part of the solution file.</span></span>

1. <span data-ttu-id="5e307-164">Öffnen Sie **package-solution.json** im Ordner „config“.</span><span class="sxs-lookup"><span data-stu-id="5e307-164">Open **package-solution.json** from the config folder.</span></span>

  <span data-ttu-id="5e307-165">Die Datei **package-solution.json** definiert die Paketmetadaten, wie im folgenden Code dargestellt:</span><span class="sxs-lookup"><span data-stu-id="5e307-165">The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "1.0.0.0",
      "includeClientSideAssets": true
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }

  ```

2. <span data-ttu-id="5e307-166">Um sicherzustellen, dass unsere neu hinzugefügten Featureframeworkdateien beim Verpacken der Lösung berücksichtigt werden, müssen wir eine Featureframework-Featuredefinition für das Lösungspaket einschließen.</span><span class="sxs-lookup"><span data-stu-id="5e307-166">To ensure that our newly added Feature Framework files are taken into account while solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for needed feature inside of the solution structure as demonstrated in below code.</span></span> <span data-ttu-id="5e307-167">Wir werden eine JSON-Definition für erforderliche Features innerhalb der Lösungsstruktur einschließen, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5e307-167">Let's include a JSON definition for the needed feature inside of the solution structure as demonstrated in the following code.</span></span>

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "1.0.0.0",
      "includeClientSideAssets": true,
      "features": [{
        "title": "asset-deployment-webpart-client-side-solution",
        "description": "asset-deployment-webpart-client-side-solution",
        "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ],
          "elementFiles":[
            "schema.xml"
          ]
        }
      }]
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }
  ```

<span data-ttu-id="5e307-168">Beachten Sie Folgendes zu den hinzugefügten JSON-Definitionen:</span><span class="sxs-lookup"><span data-stu-id="5e307-168">Note the following about the added json definitions:</span></span>

* <span data-ttu-id="5e307-169">Technisch gesehen können mehrere Features in dem Paket vorhanden sein, da es sich bei **Features** um eine Sammlung handelt. Dies wird aber nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="5e307-169">You can technically have multiple features in the package since **features** is a collection, which is not however recommended</span></span>

* <span data-ttu-id="5e307-170">Auf **elements.xml** wird unter „elementManifests“ verwiesen, sodass es für die tatsächliche Feature-XML-Struktur ordnungsgemäß als Elementmanifestdatei verpackt wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-170">**elements.xml** is referenced under elementManifests, so that it's packaged properly for the actual feature xml structure as element manifest file</span></span>

* <span data-ttu-id="5e307-171">In der Definition können mehrere element.xml-Dateien vorhanden sein, und diese würden in der Reihenfolge ausgeführt, in der sie in der JSON-Definition erwähnt werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-171">You can have multiple element.xml files in the definition and they would be executed in the order they are mentioned in the JSON definition. Typically, you should avoid usage of multiple element.xml since it adds unnecessary complexity. You can define all needed assets in single element.xml file</span></span> <span data-ttu-id="5e307-172">Im Allgemeinen sollten Sie die Verwendung mehrerer „element.xml“-Dateien vermeiden, da dadurch eine unnötige Komplexität entsteht.</span><span class="sxs-lookup"><span data-stu-id="5e307-172">Typically, you should avoid using multiple element.xml files because this adds unnecessary complexity.</span></span> <span data-ttu-id="5e307-173">Sie können alle erforderlichen Ressourcen in einer einzigen „element.xml“-Datei definieren.</span><span class="sxs-lookup"><span data-stu-id="5e307-173">You can define all needed assets in a single element.xml file.</span></span>

## <a name="deploy-and-test-asset-provisioning"></a><span data-ttu-id="5e307-174">Bereitstellen und Testen der Bereitstellung von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5e307-174">Deploy and test asset provisioning</span></span>

<span data-ttu-id="5e307-175">Jetzt sind Sie bereit, die Lösung in SharePoint bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="5e307-175">Now you are ready to deploy the solution to a SharePoint site and to have the  automatically associated on the site level.</span></span> <span data-ttu-id="5e307-176">Da wir Ressourcen direkt auf SharePoint-Websites bereitstellen, wenn die Lösung installiert wird, können Sie die Funktion in der lokalen oder Online-Workbench nicht testen.</span><span class="sxs-lookup"><span data-stu-id="5e307-176">Now you are ready to deploy the solution to SharePoint. Since in this case we are provisioning assets directly to the SharePoint sites when the solution is installed, you cannot test the capability in local or in online workbench.</span></span>

1. <span data-ttu-id="5e307-177">Geben Sie im Konsolenfenster den folgenden Befehl ein, um Ihre clientseitige Lösung, die das Webpart enthält, zu verpacken, damit die grundlegende Struktur für das Verpacken vorbereitet wird:</span><span class="sxs-lookup"><span data-stu-id="5e307-177">In the console window, enter the following command to package your client-side solution that contains the web part, so that we get the basic structure ready for packaging:</span></span>

  ```
  gulp bundle
  ```

2. <span data-ttu-id="5e307-178">Führen Sie den folgenden Befehl aus, um das Lösungspaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="5e307-178">Execute the following command to create the solution package:</span></span>

  ```
  gulp package-solution
  ```

  <span data-ttu-id="5e307-179">Der Befehl erstellt das Paket im `sharepoint/solution`-Ordner:</span><span class="sxs-lookup"><span data-stu-id="5e307-179">The command creates the package in the `sharepoint/solution` folder:</span></span>

  ```
  asset-deployment-webpart.sppkg
  ```

3. <span data-ttu-id="5e307-180">Vor dem Testen des Pakets in SharePoint sehen wir uns schnell die Standardstrukturen an, die für das Paket um die definierten Featureframeworkelemente herum erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="5e307-180">Before testing the package in the SharePoint, let's quickly have a look on the default structures created for the package around the defined feature framework elements. Move back to Visual Studio Code side and expand  folder, which contains the raw xml structures to be included in the actual sppkg package.</span></span> <span data-ttu-id="5e307-181">Wechseln Sie zurück zur Seite von Visual Studio Code, und erweitern Sie den Ordner `sharepoint/solution/debug`, der die raw.xml-Strukturen enthält, die in das tatsächliche **sppkg**-Paket eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="5e307-181">Before testing the package in the SharePoint, let's quickly have a look on the default structures created for the package around the defined feature framework elements. Move back to Visual Studio Code side and expand `sharepoint/solution/debug` folder, which contains the raw xml structures to be included in the actual **sppkg** package.</span></span>

  ![Screenshot, in dem der Debugordner unter dem SharePoint-Ordner in der Lösungsstruktur angezeigt wird](../../../images/tutorial-feature-solution-debug-folder.png)

4. <span data-ttu-id="5e307-183">Stellen Sie das Paket, das generiert wurde, im App-Katalog bereit.</span><span class="sxs-lookup"><span data-stu-id="5e307-183">Next you need to deploy the package that was generated to the App Catalog.</span></span> <span data-ttu-id="5e307-184">Wechseln Sie zum App-Katalog des Mandanten.</span><span class="sxs-lookup"><span data-stu-id="5e307-184">Go to your tenant's App Catalog.</span></span>

5. <span data-ttu-id="5e307-185">Laden Sie das Paket „asset-deployment-webpart.sppkg“, das sich im Ordner `sharepoint/solution` befindet, in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop.</span><span class="sxs-lookup"><span data-stu-id="5e307-185">Upload or drag and drop the asset-deployment-webpart.sppkg located in the `sharepoint/solution` folder to the App Catalog.</span></span> <span data-ttu-id="5e307-186">In SharePoint wird ein Dialogfeld angezeigt, und Sie werden aufgefordert, der clientseitigen Lösung, die bereitgestellt werden soll, zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="5e307-186">SharePoint displays a dialog and asks you to trust the client-side solution.</span></span>

  ![Dialogfeld für die Vertrauensstellung für die Bereitstellung des Lösungspakets](../../../images/tutorial-feature-solution-trust-app-catalog.png)

  > [!NOTE]
  > <span data-ttu-id="5e307-188">SharePoint überprüft das veröffentlichte Paket, wenn es bereitgestellt wird, und Sie sehen nur das Dialogfeld für die Vertrauensstellung, wenn das Paket bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="5e307-188">SharePoint validates the published package when it's deployed and you only see the trust dialog, if package is valid for deployment.</span></span> <span data-ttu-id="5e307-189">Sie können auch den Status dieser Überprüfung in der Spalte „Gültiges App-Paket“ im App-Katalog anzeigen.</span><span class="sxs-lookup"><span data-stu-id="5e307-189">You can also see the status around this validation from the 'Valid App Package' column in the app catalog.</span></span>

6. <span data-ttu-id="5e307-190">Wechseln Sie zu der Website, auf der Sie die Bereitstellung der SharePoint-Ressource testen möchten.</span><span class="sxs-lookup"><span data-stu-id="5e307-190">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span> <span data-ttu-id="5e307-191">Dies könnte eine Websitesammlung im Mandanten sein, auf dem Sie dieses Lösungspaket bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="5e307-191">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

7. <span data-ttu-id="5e307-192">Klicken Sie auf der oberen Navigationsleiste rechts auf das Zahnradsymbol und anschließend auf **App hinzufügen**, um Ihre Apps-Seite aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="5e307-192">Select the gears icon on the top navigation bar on the right, and then select **Add an app** to go to your Apps page.</span></span>

8. <span data-ttu-id="5e307-193">Geben Sie in das **Suchfeld** die Zeichenfolge **deployment** ein, und drücken Sie die EINGABETASTE, um Ihre Apps zu filtern.</span><span class="sxs-lookup"><span data-stu-id="5e307-193">In the **Search** box, enter **extension**, and then select Enter to filter your apps.</span></span>

  ![Suchen nach der App auf der Website](../../../images/tutorial-feature-solution-add-app.png)

9. <span data-ttu-id="5e307-195">Wählen Sie die App **asset-deployment-webpart-client-side-solution** aus, um die App auf der Website zu installieren.</span><span class="sxs-lookup"><span data-stu-id="5e307-195">Select the **app-extension-client-side-solution** app to install the solution on the site.</span></span> <span data-ttu-id="5e307-196">Wenn die Installation abgeschlossen ist, aktualisieren Sie die Seite, indem Sie **F5** drücken.</span><span class="sxs-lookup"><span data-stu-id="5e307-196">When the installation is completed, refresh the page by selecting **F5**.</span></span> <span data-ttu-id="5e307-197">Beachten Sie, dass die benutzerdefinierte **SPFx-Liste** auf der Website als Teil der Lösungspaketbereitstellung bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="5e307-197">Notice how the custom **SPFx List** has been also provisioned to site as part of the solution package deployment.</span></span>

  ![Neue SPFx-Liste und App, die auf der Websiteinhaltsseite sichtbar sind, nachdem die Lösung bereitgestellt wurde](../../../images/tutorial-feature-solution-provision-app.png)


10. <span data-ttu-id="5e307-199">Klicken Sie auf **SPFx-Liste**, um zu der Liste zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="5e307-199">Click **SPFx List** to move to the list</span></span> <span data-ttu-id="5e307-200">Beachten Sie, dass die benutzerdefinierten Felder **Betrag** und **Kostenstelle** automatisch in der Standardansicht der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-200">Notice how the custom fields **Amount** and **Cost Center** are visible automatically in the default view of the list.</span></span> 

  ![Standardmäßige Listenansicht für eine benutzerdefinierte Liste, in der standardmäßig zusätzliche Felder angezeigt werden](../../../images/tutorial-feature-solution-list-view.png)


## <a name="define-upgrade-actions-for-new-version"></a><span data-ttu-id="5e307-202">Definieren von Upgradeaktionen für die neue Version</span><span class="sxs-lookup"><span data-stu-id="5e307-202">Define upgrade actions for new version</span></span>

<span data-ttu-id="5e307-p115">Immer dann, wenn Sie eine neue Version Ihrer SharePoint Framework-Lösung erstellen, gibt es möglicherweise erforderliche Änderungen an den bereitgestellten SharePoint-Ressourcen. Sie können die Unterstützung der Upgradeaktion für das Featureframework nutzen, wenn eine neue Version des Pakets bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-p115">Whenever you build a new version of your SharePoint Framework solution, you might have some required changes on the provisioned SharePoint assets. You can take advantage of the Feature Framework upgrade action support when a new version of the package is being deployed.</span></span> 

<span data-ttu-id="5e307-205">SharePoint Framework-Lösungen unterstützen die folgenden Upgradeaktionsdefinitionen für das Featureframework:</span><span class="sxs-lookup"><span data-stu-id="5e307-205">SharePoint Framework solutions do support following Feature Framework upgrade action definitions</span></span>

* <span data-ttu-id="5e307-206">ApplyElementManifest</span><span class="sxs-lookup"><span data-stu-id="5e307-206">ApplyElementManifest</span></span>
* <span data-ttu-id="5e307-207">AddContentTypeField</span><span class="sxs-lookup"><span data-stu-id="5e307-207">AddContentTypeField</span></span>

> [!TIP]
> <span data-ttu-id="5e307-208">Weitere Informationen zu den Upgradeaktionsdefinitionen für das Featureframework finden Sie im Artikel [Aktualisierungsverfahren für Add-Ins für SharePoint](../../../sp-add-ins/sharepoint-add-ins-update-process.md).</span><span class="sxs-lookup"><span data-stu-id="5e307-208">You can read more details around the Feature Framework upgrade action definitions from [SharePoint add-ins update process](../../../sp-add-ins/sharepoint-add-ins-update-process.md) article at MSDN.</span></span>

### <a name="to-add-a-new-elementxml-file-for-the-new-version"></a><span data-ttu-id="5e307-209">So fügen Sie eine neue „element.xml“-Datei für die neue Version hinzu</span><span class="sxs-lookup"><span data-stu-id="5e307-209">Add new element.xml file for the new version</span></span>

1. <span data-ttu-id="5e307-210">Wechseln Sie zurück zu Ihrer Lösung in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5e307-210">Move back to your solution in the Visual Studio code.</span></span>

2. <span data-ttu-id="5e307-211">Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements-v2.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-211">Create a new file inside the **sharepoint\assets** folder named as **elements-v2.xml**</span></span>

3. <span data-ttu-id="5e307-212">Kopieren Sie die folgende XML-Struktur in die Datei **elements-v2.xml**, in der eine neue SharePoint-Liste definiert wird, die mit dem Titel **Neue Liste** bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="5e307-212">Copy the following xml structure into **elements-v2.xml**, which defines a new SharePoint list to be provisioned with a title of **New List**.</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">

      <ListInstance 
              FeatureId="00bfea71-de22-43b2-a848-c05709900100"
              Title="New List" 
              Description="New list provisioned from v2"
              TemplateType="100"
              Url="Lists/NewList">
      </ListInstance>

  </Elements>
  ```

4. <span data-ttu-id="5e307-213">Außerdem wird eine Definition für die tatsächlichen Upgradeaktionen für das Featureframework benötigten, erstellen Sie daher eine neue Datei innerhalb des Ordners **Sharepoint\Ressourcen** mit dem Namen **upgrade-actions-v2.xml**</span><span class="sxs-lookup"><span data-stu-id="5e307-213">We also need a definition for actual Feature Framework upgrade actions, so create a new file inside the **sharepoint\assets** folder named as **upgrade-actions-v2.xml**</span></span>

5. <span data-ttu-id="5e307-214">Kopieren Sie die folgende XML-Struktur in **upgrade-actions-v2.xml**.</span><span class="sxs-lookup"><span data-stu-id="5e307-214">Copy the following xml structure into **schema.xml**.</span></span> <span data-ttu-id="5e307-215">Beachten Sie, dass der Feature-GUID-Verweis in dem Pfad auf den automatisch erstellten Ordner unter dem Ordner `sharepoint/solution/debug` verweist und basierend auf Ihrer Lösung aktualisiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="5e307-215">Copy the following xml structure into upgrade-actions-v2.xml. Notice that the feature guid reference in the path refers to the automatically created folder under   folder and has to be updated based on your solution. This guid is also matching on the guid of the feature, which we defined in the package-solution.json file.</span></span> <span data-ttu-id="5e307-216">Diese GUID stimmt auch mit der GUID des Features überein, die wir in der Datei **-solution.json** definiert haben.</span><span class="sxs-lookup"><span data-stu-id="5e307-216">This GUID also matches the GUID of the feature, which we defined in the **package-solution.json** file.</span></span>

  ```xml
  <ApplyElementManifests>
        <ElementManifest Location="523fe887-ced5-4036-b564-8dad5c6c6e24\elements-v2.xml" />
  </ApplyElementManifests>

  ```

### <a name="to-deploy-the-new-version-to-sharepoint"></a><span data-ttu-id="5e307-217">So stellen Sie die neue Version in SharePoint bereit</span><span class="sxs-lookup"><span data-stu-id="5e307-217">To deploy the new version to SharePoint</span></span>

<span data-ttu-id="5e307-218">Als Nächstes müssen wir sowohl die Lösungsversion als auch die Featureversion aktualisieren, die für die Bereitstellung der Ressource verantwortlich ist.</span><span class="sxs-lookup"><span data-stu-id="5e307-218">Next we'll need to update both solution version and the feature version responsible of the asset provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e307-219">Die Lösungsversion gibt für SharePoint an, dass eine neue Version der SharePoint Framework-Lösung zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="5e307-219">The solution version indicates for SharePoint that there's a new version of the SharePoint Framework solution available.</span></span> <span data-ttu-id="5e307-220">Durch die Featureversion wird sichergestellt, dass die Upgradeaktionen entsprechend ausgeführt werden, wenn das Lösungspaket auf den vorhandenen Websites aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-220">The feature version ensures that the upgrade actions are executed accordingly when the solution package is upgraded in the existing site(s).</span></span>

1. <span data-ttu-id="5e307-221">Öffnen Sie **package-solution.json** im Ordner „config“, und aktualisieren Sie die Versionswerte sowohl für die Lösung als auch für das Feature auf „2.0.0.0“.</span><span class="sxs-lookup"><span data-stu-id="5e307-221">Open **package-solution.json** from the config folder and update the version values for both the solution and the feature to "2.0.0.0".</span></span> 

2. <span data-ttu-id="5e307-222">Außerdem müssen**elements-v2.xml** im Abschnitt „elementManifest“ und das „upgradeActions“-Element in einen Zeiger auf die soeben erstelle **upgrade-actions-v2.xml**-Datei eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="5e307-222">Open package-solution.json from the config folder and update version values for both solution and feature to "2.0.0.0". We will also need to include **elements-v2.xml** under the elementManifest section and also to include upgradeActions element with a pointer to just created **upgrade-actions-v2.xml** file.</span></span>

  <span data-ttu-id="5e307-p118">Nachfolgend sehen Sie eine vollständige **package-solution.json**-Datei mit den erforderlichen Änderungen. Beachten Sie, dass die Bezeichner für Ihre Lösung etwas anders aussehen könnten, konzentrieren Sie sich daher nur auf das Hinzufügen der fehlenden Teile.</span><span class="sxs-lookup"><span data-stu-id="5e307-p118">Here's a complete **package-solution.json** file with needed changes. Notice that identifiers for your solution could be slightly different, so concentrate on adding only the missing pieces.</span></span>

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "asset-deployment-webpart-client-side-solution",
      "id": "6690f11b-012f-4268-bc33-3086eb2dd287",
      "version": "2.0.0.0",
      "includeClientSideAssets": true,
      "features": [{
        "title": "asset-deployment-webpart-client-side-solution",
        "description": "asset-deployment-webpart-client-side-solution",
        "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
        "version": "2.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml",
            "elements-v2.xml"
          ],
          "elementFiles":[
            "schema.xml"
          ],
          "upgradeActions":[
            "upgrade-actions-v2.xml"
          ]
        }
      }]
    },
    "paths": {
      "zippedPackage": "solution/asset-deployment-webpart.sppkg"
    }
  }
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="5e307-225">Beachten Sie, dass auch das **elements-v2.xml**-Element unter dem Abschnitt „elementManifest“ eingeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="5e307-225">Notice that we also included the **elements-v2.xml** under the elementManifest section.</span></span> <span data-ttu-id="5e307-226">Dadurch wird sichergestellt, dass das Endergebnis bei Installation dieses Pakets auf einer bereinigten Website als Version 2.0 mit den aktualisierten Paketen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="5e307-226">Notice that we also included the elements-v2.xml under the elementManifest section. This will ensure that when you install this package to a clean site as a version 2.0, end result will match with the upgraded packages.</span></span>

3. <span data-ttu-id="5e307-227">Geben Sie im Konsolenfenster den folgenden Befehl ein, um Ihre clientseitige Lösung, die das Webpart enthält, erneut zu verpacken, damit die grundlegende Struktur für das Verpacken vorbereitet wird:</span><span class="sxs-lookup"><span data-stu-id="5e307-227">In the console window, enter the following command to re-package your client-side solution that contains the web part, so that we get the basic structure ready for packaging:</span></span>

  ```
  gulp bundle
  ```
4. <span data-ttu-id="5e307-228">Führen Sie den folgenden Befehl aus, um das Lösungspaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="5e307-228">Execute the following command to create the solution package:</span></span>

  ```
  gulp package-solution
  ```

  <span data-ttu-id="5e307-229">Der Befehl erstellt eine neue Version des Lösungspakets im Ordner `sharepoint/solution`.</span><span class="sxs-lookup"><span data-stu-id="5e307-229">The command creates a new version of the solution package in the `sharepoint/solution` folder.</span></span> <span data-ttu-id="5e307-230">Beachten Sie, dass Sie am Ordner `sharepoint/solution/debug` leicht erkennen können, dass die aktualisierten XML-Dateien im Lösungspaket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="5e307-230">The command will create new version of the solution package to the  folder. Notice that you can easily confirm from  folder that updated xml files are included in the solution package</span></span>

5. <span data-ttu-id="5e307-231">Als Nächstes müssen Sie die neue Version, die generiert wurde, im App-Katalog bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="5e307-231">Next you need to deploy the new version that was generated to the App Catalog.</span></span> <span data-ttu-id="5e307-232">Wechseln Sie zum App-Katalog des Mandanten.</span><span class="sxs-lookup"><span data-stu-id="5e307-232">Go to your tenant's App Catalog.</span></span>

6. <span data-ttu-id="5e307-233">Laden Sie das Paket „asset-deployment-webpart.sppkg“, das sich im Ordner `sharepoint/solution` befindet, in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop.</span><span class="sxs-lookup"><span data-stu-id="5e307-233">Upload or drag and drop the asset-deployment-webpart.sppkg located in the `sharepoint/solution` folder to the App Catalog.</span></span> <span data-ttu-id="5e307-234">Sie werden von SharePoint aufgefordert, zu bestätigen, dass die vorhandene Version überschrieben werden soll.</span><span class="sxs-lookup"><span data-stu-id="5e307-234">SharePoint requests that you confirm overriding the existing version.</span></span>

  ![Ersetzen der Frage aus dem App-Katalog](../../../images/tutorial-feature-solution-override-sppkg.png)

7. <span data-ttu-id="5e307-236">Klicken Sie auf **Ersetzen**, um ein Update auf die neueste Version im App-Katalog durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="5e307-236">Select **Replace It** to update the latest version to the App Catalog.</span></span>

8. <span data-ttu-id="5e307-237">Klicken Sie auf **Bereitstellen**, um auch der neuesten Version *zu vertrauen*. </span><span class="sxs-lookup"><span data-stu-id="5e307-237">Select **Deploy** to *trust* the latest version.</span></span>

  <span data-ttu-id="5e307-238">Beachten Sie, dass die Spalte „App-Version“ für die **asset-deployment-webpart-client-side-solution** nun auf „2.0.0.0“ aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="5e307-238">Notice that the App Version column for the **asset-deployment-webpart-client-side-solution** is now updated to be "2.0.0.0".</span></span>

  ![Nahaufnahme der Lösungszeile im App-Katalog mit aktualisierter Versionsnummer](../../../images/tutorial-feature-solution-version-2.png)

### <a name="to-update-an-existing-instance-in-the-site"></a><span data-ttu-id="5e307-240">So aktualisieren Sie die vorhandene Instanz auf der Website</span><span class="sxs-lookup"><span data-stu-id="5e307-240">To update an existing instance in the site</span></span>

<span data-ttu-id="5e307-241">Da das Paket nun im App-Katalog aktualisiert wurde, können wir zur tatsächlichen SharePoint-Inhaltswebsite wechseln und das Upgrade für die vorhandene Instanz durchführen.</span><span class="sxs-lookup"><span data-stu-id="5e307-241">Now that the package has been updated in the App Catalog, we can move to the actual SharePoint content site and perform the upgrade for the existing instance.</span></span>

1. <span data-ttu-id="5e307-242">Wechseln zu der Website, auf der Sie die erste Version der SharePoint Framework-Lösung bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="5e307-242">Move to site where you deployed first version of the SharePoint Framework solution</span></span>

2. <span data-ttu-id="5e307-243">Wechseln Sie auf die Seite **Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="5e307-243">Go to the **Site Contents** page.</span></span>

3. <span data-ttu-id="5e307-244">Wählen der Option **Details** aus dem Kontextmenü der Lösung **asset-deployment-webpart-client-side-solution**</span><span class="sxs-lookup"><span data-stu-id="5e307-244">Chose **Details** from the context menu of the **asset-deployment-webpart-client-side-solution** solution</span></span>

  ![Kontextmenü des vorhandenen Pakets auf der Website](../../../images/tutorial-feature-solution-hover-menu.png)

  <span data-ttu-id="5e307-246">Dadurch werden die aktuellen Details zu der installierten SharePoint Framework-Lösung vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="5e307-246">This presents the current details around the installed SharePoint Framework solution.</span></span> <span data-ttu-id="5e307-247">Auf dieser Seite wird nun der Text als *Es ist eine neue Version dieser App verfügbar.* angezeigt, um anzugeben, dass eine neue Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="5e307-247">This will present the current details around installed SharePoint Framework solution. This page also now shows a text as '*There is a new version of this app. Get it now*' to indicate that there's a new version available.</span></span>

  ![Kontextmenü des vorhandenen Pakets auf der Website](../../../images/tutorial-feature-solution-app-details.png)

4. <span data-ttu-id="5e307-249">Klicken Sie auf die Schaltfläche **HERUNTERLADEN**, um den Updateprozess für das Paket zu starten.</span><span class="sxs-lookup"><span data-stu-id="5e307-249">Click **GET IT** button to start update process for the package.</span></span>

  ![App-Status wurde zu Updates auf der Seite der Websiteinhalte aktualisiert](../../../images/tutorial-feature-solution-updating-app.png)

  <span data-ttu-id="5e307-251">Wenn Sie zur klassischen Umgebung wechseln, sehen Sie weitere Details zur tatsächlichen Upgrade-Aktion, die für die SharePoint-Frameworklösung angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="5e307-251">If you move to classic experience, you can see more details on the actual upgrade action being applied for the SharePoint Framework solution.</span></span> 

  ![App-Status wurde zu Updates auf der Seite der Websiteinhalte aktualisiert](../../../images/tutorial-feature-solution-updating-app-classic.png)

  > [!NOTE]
  > <span data-ttu-id="5e307-253">Da das SharePoint-Framework dieselbe App-Struktur wie SharePoint-Add-Ins verwendet, weist der Status für das Upgrade auf ein Update für ein Add-In oder eine App hin.</span><span class="sxs-lookup"><span data-stu-id="5e307-253">Because the SharePoint Framework uses the same app infrastructure as SharePoint Add-ins, the status for the upgrade indicates that the update can happen for an add-in or an app.</span></span> 

  <span data-ttu-id="5e307-254">Das Update kann eine Weile dauern, wenn der Lösungsstatus jedoch wieder zu „normal“ wechselt, können Sie auf **F5** klicken, um die Seite mit den Websiteinhalten zu aktualisieren, um zu bestätigen, dass die  *neue Liste* erfolgreich als Teil des Updateprozesses bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="5e307-254">Update can take a while, but when the solution status is moved to normal again, you can click F5 to refresh the site contents page to confirm that new list  called    has been successfully provisioned as part of the update process.</span></span>

  ![Die Seite mit den Websiteinhalten mit einer zusätzlichen neuen Liste, die erstellt wird](../../../images/tutorial-feature-solution-new-list.png)

  <span data-ttu-id="5e307-256">Wir haben jetzt diese Instanz erfolgreich auf die neueste Version aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="5e307-256">Now we have successfully upgraded this instance to the latest version.</span></span> <span data-ttu-id="5e307-257">Diese Option des Featureframeworks für die SharePoint-Ressourcenbereitstellung ist nahezu identisch wie beim SharePoint-Add-In-Modell.</span><span class="sxs-lookup"><span data-stu-id="5e307-257">This Feature Framework option for SharePoint asset provisioning is pretty much the same as it is for the SharePoint Add-in model.</span></span> <span data-ttu-id="5e307-258">Der wichtigste Unterschied besteht darin, dass die Ressourcen direkt auf der normalen SharePoint-Website bereitgestellt werden, da es das Konzept „App-/Add-In-Web“ bei SharePoint Framework-Lösungen nicht gibt.</span><span class="sxs-lookup"><span data-stu-id="5e307-258">The key difference is that the assets are being provisioned directly to a normal SharePoint site, because there's no concept called app or add-in web with SharePoint Framework solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="5e307-259">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="5e307-259">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="5e307-260">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="5e307-260">Thanks for your input advance.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e307-261">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="5e307-261">See also</span></span>

- [<span data-ttu-id="5e307-262">Bereitstellen von SharePoint-Elementen mit Ihrem Lösungspaket</span><span class="sxs-lookup"><span data-stu-id="5e307-262">Provision SharePoint assets with your solution package</span></span>](../../toolchain/provision-sharepoint-assets.md)
- [<span data-ttu-id="5e307-263">Beispiellösung - Bereitstellen von SharePoint-Ressourcen als Teil des SPFx-Pakets</span><span class="sxs-lookup"><span data-stu-id="5e307-263">Sample solution - Deployment of SharePoint assets as part of SPFx package</span></span>](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-feature-framework)
