---
title: Entwickeln mit Duet Enterprise 2.0
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c3ef38aa-559e-4832-95c7-75e222c77624
ms.openlocfilehash: 6694ddfdd6b312f59d0449643f8743f119b506dd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="developing-with-duet-enterprise-20"></a><span data-ttu-id="d99b1-102">Entwickeln mit Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="d99b1-102">Developing with Duet Enterprise 2.0</span></span>

## <a name="overview"></a><span data-ttu-id="d99b1-103">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d99b1-103">Overview</span></span>
<span data-ttu-id="d99b1-104"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-104"><a name="Overview"> </a></span></span>

<span data-ttu-id="d99b1-p101">Duet Enterprise 2.0 ist die neueste Version einer gemeinsamen Initiative zwischen Microsoft- und SAP, SharePoint-Benutzern die Möglichkeit zum Arbeiten mit Daten aus SAP-Systemen zu ermöglichen. Komponenten von SAP sowie SharePoint und SharePoint Online kombiniert. Es ermöglicht Entwicklern die Möglichkeit zum Erstellen von Komponenten, die Benutzern ermöglichen, Daten aus SAP-Systemen in der vertrauten SharePoint-Umgebung zu bringen.</span><span class="sxs-lookup"><span data-stu-id="d99b1-p101">Duet Enterprise 2.0 is the latest version of a collaborative effort between Microsoft and SAP to give SharePoint users the ability to work with data from SAP systems.It combines components from SAP as well as SharePoint and SharePoint Online. It gives a developer the ability to create components that will allow users to bring data from SAP systems into the familiar SharePoint environment.</span></span>
  
    
    

## <a name="features-of-duet-enterprise-20"></a><span data-ttu-id="d99b1-107">Features von Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="d99b1-107">Features of Duet Enterprise 2.0</span></span>
<span data-ttu-id="d99b1-108"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-108"><a name="Overview"> </a></span></span>

<span data-ttu-id="d99b1-109">Wenn ordnungsgemäß installiert und konfiguriert ist, wird Duet Enterprise 2.0 folgende Features zu ermöglichen:</span><span class="sxs-lookup"><span data-stu-id="d99b1-109">When properly installed and configured, Duet Enterprise 2.0 will provide the following features:</span></span>
  
    
    

- <span data-ttu-id="d99b1-110">Sie können mit Daten in SAP-Systemen in SharePoint mithilfe von Geschäftsdaten-Webparts, externe Listen und benutzerdefinierten Komponenten arbeiten.</span><span class="sxs-lookup"><span data-stu-id="d99b1-110">You can work with data in SAP systems within SharePoint using Business Data Web parts, External lists and custom components.</span></span>
    
  
- <span data-ttu-id="d99b1-111">Verwenden von SAP-Daten in SharePoint ohne Code mithilfe der integrierte Komponenten.</span><span class="sxs-lookup"><span data-stu-id="d99b1-111">Use SAP data in SharePoint without code by using built-in components.</span></span>
    
  
- <span data-ttu-id="d99b1-112">Verwenden von SAP-Systeme innerhalb einer app, die Berichte.</span><span class="sxs-lookup"><span data-stu-id="d99b1-112">Use SAP reporting systems inside of an app.</span></span>
    
  
- <span data-ttu-id="d99b1-113">Verwenden Sie spezielle Webparts zum Hinzufügen von SAP-Informationen zu SharePoint-Seiten mit Duet Enterprise 2.0 installiert</span><span class="sxs-lookup"><span data-stu-id="d99b1-113">Use special web parts installed with Duet Enterprise 2.0 to add SAP information to SharePoint pages</span></span>
    
  
- <span data-ttu-id="d99b1-114">Verwenden von SAP-Workflow in einer app.</span><span class="sxs-lookup"><span data-stu-id="d99b1-114">Use SAP workflow in an app.</span></span>
    
  
- <span data-ttu-id="d99b1-115">Entwickler können mithilfe der clientseitigen JavaScript zum interagieren mit SAP externe Daten verwenden.</span><span class="sxs-lookup"><span data-stu-id="d99b1-115">Developers can use client-side JavaScript to interact with SAP external data.</span></span>
    
  
- <span data-ttu-id="d99b1-116">Sichern Sie Daten mithilfe von OAuth zur Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="d99b1-116">Secure data using OAuth for authentication.</span></span>
    
  

## <a name="setting-up-the-development-environment"></a><span data-ttu-id="d99b1-117">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="d99b1-117">Setting up the development environment</span></span>
<span data-ttu-id="d99b1-118"><a name="SettingUp"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-118"><a name="SettingUp"> </a></span></span>

<span data-ttu-id="d99b1-119">Die Entwicklung von SharePoint-Add-Ins mit Duet Enterprise 2.0 entspricht in den meisten Fällen der Erstellung von standardmäßigen SharePoint-Add-Ins. Sie können Visual Studio verwenden, um Ihre Apps zu erweitern und in dem stabilen Framework im Rahmen der integrierten Visual Studio-Entwicklungsumgebung zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="d99b1-119">Developing SharePoint Add-ins using Duet Enterprise 2.0, for the most part, is exactly the same as creating standard SharePoint Add-ins. You can use Visual Studio to extend your apps and work within the robust framework of the Visual Studio integrated development environment.</span></span>
  
    
    

## <a name="adding-external-content-types"></a><span data-ttu-id="d99b1-120">Hinzufügen externer Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="d99b1-120">Adding external content types</span></span>
<span data-ttu-id="d99b1-121"><a name="AddingECT"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-121"><a name="AddingECT"> </a></span></span>

<span data-ttu-id="d99b1-p102">Um die externen Daten, die diese auf dem SAP-System zugreifen zu können, müssen Sie einen externen Inhaltstyp hinzuzufügen. Da SAP-Daten über OData-Endpunkte verfügbar gemacht werden, können die automatische Generierung Tools in Visual Studio installiert auf  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) verwendet werden, die auf der Ebene der app ausgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="d99b1-p102">In order to access the external data housed on the SAP system, you will have to add an external content type. Since SAP data is exposed through OData endpoints, the auto-generation tools installed in Visual Studio can be used to  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) that is scoped at the app level.</span></span>
  
    
    
<span data-ttu-id="d99b1-124">Führen Sie die folgenden Schritte aus, um einen externen Inhaltstyp zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="d99b1-124">Follow these steps to create an external content type:</span></span>
  
    
    

### <a name="creating-an-external-content-type-from-an-sap-odata-endpoint"></a><span data-ttu-id="d99b1-125">Erstellen eines externen Inhaltstyps aus einem SAP-OData-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="d99b1-125">Creating an external content type from an SAP OData endpoint</span></span>


1. <span data-ttu-id="d99b1-126">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="d99b1-126">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="d99b1-127">Geben Sie auf der Seite **OData-Quelle anzugeben** die URL der Duet Enterprise-Workflow-Dienst.</span><span class="sxs-lookup"><span data-stu-id="d99b1-127">On the **Specify OData Source** page, enter the URL of the Duet Enterprise Workflow Service.</span></span>
    
  
3. <span data-ttu-id="d99b1-128">Wählen Sie einen Namen für die OData-Quelle.</span><span class="sxs-lookup"><span data-stu-id="d99b1-128">Choose a name for your OData source.</span></span>
    
  
4. <span data-ttu-id="d99b1-129">Wählen Sie die Entitäten, die erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="d99b1-129">Select the entities that are needed.</span></span>
    
  
5. <span data-ttu-id="d99b1-130">Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="d99b1-130">Choose **Finish**.</span></span>
    
  
<span data-ttu-id="d99b1-131">Visual Studio erstellt einen neuen Ordner mit dem Namen externer Inhaltstypen Sie das neu erstellte BDC-Modell finden.</span><span class="sxs-lookup"><span data-stu-id="d99b1-131">Visual Studio will create a new folder named External Content Types where you will find the newly created BDC model.</span></span>
  
    
    

## <a name="configuring-the-bdc-model"></a><span data-ttu-id="d99b1-132">Konfigurieren des BDC-Modells</span><span class="sxs-lookup"><span data-stu-id="d99b1-132">Configuring the BDC model</span></span>
<span data-ttu-id="d99b1-133"><a name="ConfiguringProject"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-133"><a name="ConfiguringProject"> </a></span></span>

<span data-ttu-id="d99b1-p103">Stellen Sie das Projekt für die Verwendung der wichtigste wird die **ODataExtensionProvider** -Eigenschaft des BDC-Modells hinzugefügt. Diese Eigenschaft definiert den Erweiterung-Anbieter, der BCS mit den SAP-Erweiterungen für das Erstellen von app-Code benötigt bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="d99b1-p103">The most important thing to make the project work, is to add the **ODataExtensionProvider** property to the BDC model. This property defines the extension provider that provides BCS with the SAP extensions needed for creating app code.</span></span>
  
    
    
<span data-ttu-id="d99b1-136">In diesem Beispiel werden die Eigenschaften gezeigt, das BDC-Modell hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="d99b1-136">This sample shows the properties added to the BDC model:</span></span>
  
    
    



```XML

<LobSystem Type="OData" Name="LOB_SYSTEM_NAME">
                     <Properties>
                          <Property Name="ODataServiceMetadataUrl" Type="System.String">
                               https://<DUET_METADATA_URL>:443/sap/opu/odata/sap/ 
                               ZANDY_PO_HEADER_SRV/$metadata</Property>
                          <Property Name="ODataServicesVersion" Type="System.String">2.0</Property>
                          <Property Name="ODataExtensionProvider" Type="System.String"> 
                               OBA.Server.Canary.ObaOdataServerExtensionProvider, 
                               OBA.Server.SSOProvider, 
                               Version=15.0.0.0, 
                               Culture=neutral, 
                               PublicKeyToken=71e9bce111e9429c</Property>
                          <Property Name="TraceHeader" Type="System.String">SAP-PASSPORT</Property>
                     </Properties>

```


## <a name="using-duet-starter-services-to-develop-custom-apps"></a><span data-ttu-id="d99b1-137">Entwickeln von benutzerdefinierten apps mithilfe von Duet Starter services</span><span class="sxs-lookup"><span data-stu-id="d99b1-137">Using Duet starter services to develop custom apps</span></span>
<span data-ttu-id="d99b1-138"><a name="UsingDuetStarterServices"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-138"><a name="UsingDuetStarterServices"> </a></span></span>

<span data-ttu-id="d99b1-139">Duet Enterprise 2.0 installiert mehrere Starterdienste im Dateisystem auf dem SharePoint-Server.</span><span class="sxs-lookup"><span data-stu-id="d99b1-139">Duet Enterprise 2.0 installs several starter services to the file system on the SharePoint server.</span></span> <span data-ttu-id="d99b1-140">In einer Standardinstallation befinden sich die Dateien im Verzeichnis C:\\Programme\\Duet Enterprise\\2.0\\Solutions\\Starter Services.</span><span class="sxs-lookup"><span data-stu-id="d99b1-140">In a default installation, the files are found at C:\\Program Files\\Duet Enterprise\\2.0\\Solutions\\Starter Services.</span></span> <span data-ttu-id="d99b1-141">Dies sind:</span><span class="sxs-lookup"><span data-stu-id="d99b1-141">Among these are:</span></span> 
  
    
    

- <span data-ttu-id="d99b1-142">OBACustomerWorkspace</span><span class="sxs-lookup"><span data-stu-id="d99b1-142">OBACustomerWorkspace</span></span>
    
  
- <span data-ttu-id="d99b1-143">OBAOrderToCash</span><span class="sxs-lookup"><span data-stu-id="d99b1-143">OBAOrderToCash</span></span>
    
  
- <span data-ttu-id="d99b1-144">OBAPortal</span><span class="sxs-lookup"><span data-stu-id="d99b1-144">OBAPortal</span></span>
    
  
- <span data-ttu-id="d99b1-145">OBAProductCenter</span><span class="sxs-lookup"><span data-stu-id="d99b1-145">OBAProductCenter</span></span>
    
  
<span data-ttu-id="d99b1-146">Jede dieser Lösungen enthält WSP-Dateien, Lösung und andere unterstützenden Dateien benötigt, sie zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="d99b1-146">Each of these solutions contains WSP files, solution and other supporting files needed to implement them.</span></span>
  
    
    
<span data-ttu-id="d99b1-147">Diese Lösungen werden kann, finden Sie unter Was mit Duet Enterprise 2.0 ausgeführt werden können und was die Entwicklung Muster sind, aber nicht für die Verwendung in SharePoint-Add-Ins unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="d99b1-147">These solutions can be used to see what can be done with Duet Enterprise 2.0 and what the development patterns are, but they are not supported for use in SharePoint Add-ins.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="d99b1-148">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d99b1-148">See also</span></span>
<span data-ttu-id="d99b1-149"><a name="ConNavExample_resources"> </a></span><span class="sxs-lookup"><span data-stu-id="d99b1-149"><a name="ConNavExample_resources"> </a></span></span>


-  [<span data-ttu-id="d99b1-150">Duet Enterprise für Microsoft SharePoint und SAP Server 2.0</span><span class="sxs-lookup"><span data-stu-id="d99b1-150">Duet Enterprise for Microsoft SharePoint and SAP Server 2.0</span></span>](http://technet.microsoft.com/de-DE/library/ff972436.aspx)
    
  
-  [<span data-ttu-id="d99b1-151">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d99b1-151">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d99b1-152">Visual Studio Developer Center</span><span class="sxs-lookup"><span data-stu-id="d99b1-152">Visual Studio Developer Center</span></span>](http://msdn.microsoft.com/de-DE/vstudio/default)
    
  
-  [<span data-ttu-id="d99b1-153">Office-Entwicklung mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d99b1-153">Office Development with Visual Studio</span></span>](http://msdn.microsoft.com/de-DE/office/hh133430)
    
  

