---
title: "Erstellen von Hybridkonnektivitäts-Apps für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 311f036e-3442-4497-b35e-442b665462d3
ms.openlocfilehash: 19c48b7f0d8da449cd1c96561b8017fb4d7514b1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-hybrid-connectivity-apps-for-sharepoint"></a><span data-ttu-id="abaa4-102">Erstellen von Hybridkonnektivitäts-Apps für SharePoint</span><span class="sxs-lookup"><span data-stu-id="abaa4-102">Create hybrid connectivity apps for SharePoint</span></span>
<span data-ttu-id="abaa4-103">Informationen Sie zu den Prozess der entwickeln und Bereitstellen von apps für SharePoint-Diensten hybridlösungen.</span><span class="sxs-lookup"><span data-stu-id="abaa4-103">Learn about the process of developing and deploying apps for SharePoint hybrid connectivity solutions.</span></span>
## <a name="hybrid-connectivity-in-sharepoint-and-sharepoint-online"></a><span data-ttu-id="abaa4-104">Hybridkonnektivität in SharePoint und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="abaa4-104">Hybrid connectivity in SharePoint and SharePoint Online</span></span>
<span data-ttu-id="abaa4-105"><a name="bk_hybridconnectivity"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-105"><a name="bk_hybridconnectivity"> </a></span></span>

<span data-ttu-id="abaa4-p101">Als Unternehmen mit SharePoint Online zu verschieben, benötigen sie eine Möglichkeit, große Mengen von proprietäre Daten sichere verfügbar zu machen. Um diese Herausforderung zu lösen, SharePoint hybridkonnektivität eingeführt.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p101">As businesses move to using SharePoint Online, they need a way to expose large amounts of proprietary data safely and securely. To help solve this challenge, SharePoint introduced hybrid connectivity.</span></span>
  
    
    
<span data-ttu-id="abaa4-p102">"Übertragen" Business Connectivity Services (BCS) Hybrid-Konnektivität kann SharePoint Nutzen von Daten, die lokal, innerhalb Unternehmensfirewalls, und verschiedene Formen der Authentifizierung gesichert. Mit hybride Connectivity Funktionen können SharePoint Online diese Daten sicher über das Internet zugreifen als wäre es im gleichen internen Netzwerk. Nachdem hybridkonnektivität konfiguriert wurde, können Benutzer mit Daten arbeiten, die innerhalb des Unternehmens-Infrastruktur gesichert wird. Sie können zugreifen und bearbeiten die Daten entsprechend den Berechtigungen, die ihnen in SharePoint gewährt wurden.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p102">The Business Connectivity Services (BCS) hybrid connectivity capability lets SharePoint consume data housed on-premises, inside corporate firewalls, and secured by various forms of authentication. With hybrid connectivity functionality, SharePoint Online can access this data securely over the web as if it was on the same internal network. Once hybrid connectivity is configured, users can work with data that is secured within the business' infrastructure. They can access and manipulate the data according to the permissions that they have been granted in SharePoint.</span></span>
  
    
    
<span data-ttu-id="abaa4-112">Eine vollständige Beschreibung zum Konfigurieren einer funktionierenden Hybrid-Lösung finden Sie unter  [Hybridlösung für SharePoint](http://technet.microsoft.com/de-DE/library/jj838715.aspx).</span><span class="sxs-lookup"><span data-stu-id="abaa4-112">For a complete description of how to configure a working hybrid solution, see  [Hybrid for SharePoint](http://technet.microsoft.com/de-DE/library/jj838715.aspx).</span></span> <span data-ttu-id="abaa4-113">Diese Artikelreihe führt Sie durch alle Anforderungen der Konfiguration von Datenquellen, Reverseproxys, Suche, Sicherheit, Netzwerken und anderen Voraussetzungen zum Einrichten des End-to-End-Szenarios.</span><span class="sxs-lookup"><span data-stu-id="abaa4-113">This series of articles walks you through all the requirements of configuring data sources, reverse proxies, search, security, networking, and everything else needed to set up the end-to-end scenario.</span></span>
  
    
    

> <span data-ttu-id="abaa4-114">**Vorsicht:** Um eine SharePoint-Hybridumgebung zu konfigurieren, benötigen Sie eine Kombination aus Experten-Know-how und erheblicher praktischer Erfahrung mit SharePoint, SharePoint Online und verwandten Produkten und Technologien.</span><span class="sxs-lookup"><span data-stu-id="abaa4-114">**Caution:** To configure a hybrid SharePoint environment, you need a combination of expert skills and significant hands-on experience with SharePoint, SharePoint Online, and related products and technologies.</span></span> <span data-ttu-id="abaa4-115">Es wird empfohlen, bei Entwurf und Bereitstellung der Hybridumgebung technische Anleitung und Unterstützung durch die Microsoft Beratungsdienste in Anspruch zu nehmen.</span><span class="sxs-lookup"><span data-stu-id="abaa4-115">We recommend that you engage Microsoft Consulting Services to provide technical guidance and support during the design and deployment of your hybrid environment.</span></span> <span data-ttu-id="abaa4-116">Weitere Informationen finden Sie unter [Microsoft Services](http://www.microsoft.com/de-DE/microsoftservices/deploy.aspx).</span><span class="sxs-lookup"><span data-stu-id="abaa4-116">> For more information, see  [Microsoft Services](http://www.microsoft.com/de-DE/microsoftservices/deploy.aspx).</span></span> 
  
    
    

<span data-ttu-id="abaa4-117">Damit Sie eine app erstellen können, die Daten aus einer internen Datenquelle über BCS und die Verbindung Hybrid nutzt, wird in diesem Artikel davon ausgegangen, dass Sie die Verfahren zum Konfigurieren der hybridumgebung bereits durchgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="abaa4-117">For you to be able to create an app that consumes data from an internal data source through BCS and the hybrid connection, this article assumes that you have already followed the procedures to configure your hybrid environment.</span></span>
  
    
    

## <a name="create-hybrid-connectivity-apps"></a><span data-ttu-id="abaa4-118">Konnektivität-Hybrid-apps erstellen</span><span class="sxs-lookup"><span data-stu-id="abaa4-118">Create hybrid connectivity apps</span></span>
<span data-ttu-id="abaa4-119"><a name="bkmk_CreatingHybridConnectivityApps"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-119"><a name="bkmk_CreatingHybridConnectivityApps"> </a></span></span>

<span data-ttu-id="abaa4-120">Erstellen einer hybriden SharePoint-Add-In ist im Wesentlichen das Erstellen eine beliebige SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="abaa4-120">Creating a hybrid SharePoint Add-in is essentially the same as creating any SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="abaa4-121">Führen Sie diese Schritte zum Erstellen einer Hybrid-app:</span><span class="sxs-lookup"><span data-stu-id="abaa4-121">Follow these steps to create a hybrid app:</span></span>
  
    
    

-  [<span data-ttu-id="abaa4-122">Vorbereiten der Datenquelle</span><span class="sxs-lookup"><span data-stu-id="abaa4-122">Prepare the data source</span></span>](#bkmk_PrepareDataSource)
    
  
-  [<span data-ttu-id="abaa4-123">Erstellen einer SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="abaa4-123">Create an SharePoint Add-in</span></span>](#bkmk_CreateAnApp)
    
  
-  [<span data-ttu-id="abaa4-124">Erstellen eines externen Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="abaa4-124">Create an external content type</span></span>](#bkmk_CreateECT)
    
  
-  [<span data-ttu-id="abaa4-125">Bereitstellen der Hybrid-app</span><span class="sxs-lookup"><span data-stu-id="abaa4-125">Deploy the hybrid app</span></span>](#bkmk_DeployHybridApp)
    
  

### <a name="prepare-the-data-source"></a><span data-ttu-id="abaa4-126">Vorbereiten der Datenquelle</span><span class="sxs-lookup"><span data-stu-id="abaa4-126">Prepare the data source</span></span>
<span data-ttu-id="abaa4-127"><a name="bkmk_PrepareDataSource"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-127"><a name="bkmk_PrepareDataSource"> </a></span></span>

<span data-ttu-id="abaa4-p105">In den meisten Fällen, die Datenquelle bereits vorhanden ist und eine beliebige Anzahl von Geschäftsanwendungen bedient. Diese Daten können jedoch nur innerhalb der Unternehmens Sicherheitsinfrastruktur zur Verfügung sein. Wenn Ihre Daten auf einem Server befindet sich innerhalb des Unternehmens-Firewall vorhanden, oder mit anderen Mitteln geschützt ist, besteht der nächste Schritt auf Daten, BCS, verfügbar machen, die auch innerhalb der Firewall gespeichert ist. Ein Netzwerkgerät ist so konfiguriert, dass um Anrufe von SharePoint Online an der internen SharePoint-Farm zu übersetzen. Dieses Gerät wird als "Reverseproxy" bezeichnet und ermöglicht die SharePoint-Add-In in der Cloud Aufruf von BCS befindet sich innerhalb der Firewall befinden. BCS behandelt die Datenkonnektivität von dort aus.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p105">Most of the time, the data source is already in place and is servicing any number of business applications. However, that data may only be available from inside the corporate security infrastructure. If your data does exist on a server located on the inside of a corporate firewall, or is secured by some other means, the next step is to expose that data to BCS, which is also housed inside the firewall. A network device is configured to translate calls from SharePoint Online to the internal SharePoint farm. This device is referred to as a "reverse proxy" and allows the SharePoint Add-in located in the cloud to call into BCS located inside the firewall. BCS handles all the data connectivity from there.</span></span>
  
    
    
<span data-ttu-id="abaa4-p106">Diese Daten zum BCS zur Verfügung zu stellen, sollten Sie es als einer OData-Quelle verfügbar machen. Zu diesem Zweck erstellen eine Website von Internetinformationsdienste (Internet Information Services, IIS), die als host für den Dienst und ermöglichen die Kommunikation mit der Datenquelle über OData und Representational State Transfer (REST) Endpunkte BCS.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p106">To make this data available to BCS, you should expose it as an OData source. You do this by creating an Internet Information Services (IIS) website that will host the service and allow BCS to talk to the data source through OData and Representational State Transfer (REST) endpoints.</span></span>
  
    
    
<span data-ttu-id="abaa4-136">Um einen OData-Endpunkt zu erstellen, müssen Sie diese Schritte für die Erstellung einer Datendienst Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="abaa4-136">To create an OData endpoint, you will need to follow these steps for creating a Windows Communication Foundation (WCF) data service.</span></span>
  
    
    

### <a name="to-create-a-wcf-data-service"></a><span data-ttu-id="abaa4-137">Erstellen ein WCF-Datendiensts</span><span class="sxs-lookup"><span data-stu-id="abaa4-137">To create a WCF data service</span></span>


1. <span data-ttu-id="abaa4-p107">Erstellen Sie eine IIS-Website mit mindestens Microsoft .NET Framework 4. Sichern Sie die Website mit der Standardauthentifizierung.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p107">Create an IIS website running at least Microsoft .NET Framework 4. Secure the site using basic authentication.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="abaa4-140">Es ist nicht erforderlich, dass SharePoint auf diesem Server installiert ist.</span><span class="sxs-lookup"><span data-stu-id="abaa4-140">Note: It's not necessary for SharePoint to be installed on this server.</span></span> <span data-ttu-id="abaa4-141">Tatsächlich ist es aus Gründen der Einfachheit und Leistung besser, wenn SharePoint nicht auf dem Server installiert ist, der den WCF-Datendienst hostet.</span><span class="sxs-lookup"><span data-stu-id="abaa4-141">In fact, for the sake of simplicity and performance, it's better if SharePoint is not installed on the server that hosts the WCF data service.</span></span> 

2. <span data-ttu-id="abaa4-142">Erstellen Sie in Visual Studio 2012 ein neues Projekt mithilfe der Vorlage **Leere ASP.NET-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-142">Create a new project in Visual Studio 2012 using the **ASP.NET Empty Web Application** template.</span></span>
    
  
3. <span data-ttu-id="abaa4-143">Fügen Sie im **Projektmappen-Explorer** ein neues **ADO.NET Entitätsdatenmodell** hinzu.</span><span class="sxs-lookup"><span data-stu-id="abaa4-143">In **Solution Explorer** add a new **ADO.NET Entity Data Model**.</span></span>
    
  
4. <span data-ttu-id="abaa4-144">Wählen Sie im **Entity Data Model Wizard** die **aus Datenbank generieren**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-144">Choose the **Generate from database** option in the **Entity Data Model Wizard**.</span></span>
    
  
5. <span data-ttu-id="abaa4-145">Wählen Sie eine vorhandene Verbindung aus, oder erstellen Sie einen neuen Anwendungspool.</span><span class="sxs-lookup"><span data-stu-id="abaa4-145">Select an existing connection, or create a new one.</span></span>
    
  
6. <span data-ttu-id="abaa4-146">Geben Sie die URL und die Verknüpfung Security-Informationen.</span><span class="sxs-lookup"><span data-stu-id="abaa4-146">Provide the URL and connection security information.</span></span>
    
  
7. <span data-ttu-id="abaa4-147">Wählen Sie die Elemente, die im Modell enthalten sein sollen, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-147">Select the items that you want to include in the model, and choose **Finish**.</span></span>
    
  
8. <span data-ttu-id="abaa4-148">Fügen Sie im **Projektmappen-Explorer** erneut einen neuen **WCF Data Service** mithilfe der Visual Studio-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="abaa4-148">Again in **Solution Explorer**, add a new **WCF Data Service** using the Visual Studio template.</span></span>
    
  
9. <span data-ttu-id="abaa4-149">Nennen Sie den Data-Dienst, und wählen Sie **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-149">Name the data service, and choose **Next**.</span></span>
    
    <span data-ttu-id="abaa4-150">Zu diesem Zeitpunkt das Entitätsmodell erstellt werden, und die resultierenden Klassen werden in Ihrem Projekt enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="abaa4-150">At this point, the entity model will be created and the resulting classes will be included in your project.</span></span>
    
  
10. <span data-ttu-id="abaa4-151">Set Sicherheitsmodell für die Personen, und Ersetzen Sie die  `/* TODO: put your data source class name here */` durch den Klassennamen der Entität erstellt Sie die soeben erstellte und Angeben der Entitäten, die Sie Berechtigungen erteilen möchten.</span><span class="sxs-lookup"><span data-stu-id="abaa4-151">Set the security to the entities created by replacing the  `/* TODO: put your data source class name here */` with the class name of the entity model you just created and specifying which entities you want to grant permissions to.</span></span>
    
  
<span data-ttu-id="abaa4-152">Ein vollständiges Lernprogramm dafür, wie Sie dies einrichten finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="abaa4-152">For a complete tutorial of how to set this up, see the following:</span></span> 
  
    
    

-  <span data-ttu-id="abaa4-153">[Erste Schritte mit OData-Teil 1: Erstellen einer OData-Dienst](http://msdn.microsoft.com/de-DE/data/gg601462)</span><span class="sxs-lookup"><span data-stu-id="abaa4-153">[Getting Started With OData Part 1: Building an OData Service](http://msdn.microsoft.com/de-DE/data/gg601462)</span></span>
    
  
-  <span data-ttu-id="abaa4-154">[Schnellstart (WCF Data Services)](http://msdn.microsoft.com/de-DE/library/cc668796.aspx)</span><span class="sxs-lookup"><span data-stu-id="abaa4-154">[Quickstart (WCF Data Services)](http://msdn.microsoft.com/de-DE/library/cc668796.aspx)</span></span>
    
  

### <a name="create-an-sharepoint-add-in"></a><span data-ttu-id="abaa4-155">Erstellen einer SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="abaa4-155">Create an SharePoint Add-in</span></span>
<span data-ttu-id="abaa4-156"><a name="bkmk_CreateAnApp"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-156"><a name="bkmk_CreateAnApp"> </a></span></span>

<span data-ttu-id="abaa4-p109">Einer der Annahmen, die wir hier machen ist, dass Sie Ihre app innerhalb der Unternehmensfirewall entwickeln. Dies stellt ein Szenario mit einem Entwickler arbeiten für ein Unternehmen einen Computer hinter den Schutz der Sicherheitsinfrastruktur, entwickeln und Testen der app, bis es bereitgestellt werden kann vor würde. Dies vereinfacht das Herstellen einer Verbindung mit der Datenquelle aus Visual Studio und Office Developer Tools für Visual Studio 2013 verwendet, um den externen Inhaltstyp im nächsten Schritt automatisch zu generieren.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p109">One of the assumptions we are making here is that you are developing your app inside the corporate firewall. This represents a scenario where a developer working for a company would have a computer located behind the protection of the security infrastructure, developing and testing the app until it is ready to be deployed. This simplifies the process of connecting to the data source from Visual Studio, and uses Office Developer Tools for Visual Studio 2013 to automatically generate the external content type in the next step.</span></span>
  
    
    

### <a name="to-create-a-new-app"></a><span data-ttu-id="abaa4-160">Zum Erstellen einer neuen app</span><span class="sxs-lookup"><span data-stu-id="abaa4-160">To create a new app</span></span>


1. <span data-ttu-id="abaa4-161">Öffnen Sie Visual Studio 2012 auf Ihrem Entwicklungscomputer, die Office Developer Tools für Visual Studio 2013 und SharePoint installiert hat.</span><span class="sxs-lookup"><span data-stu-id="abaa4-161">Open Visual Studio 2012 on your development computer that has Office Developer Tools for Visual Studio 2013 and SharePoint installed.</span></span>
    
  
2. <span data-ttu-id="abaa4-162">Erstellen Sie eine neue app für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="abaa4-162">Create a new app for SharePoint.</span></span>
    
  
3. <span data-ttu-id="abaa4-p110">Geben Sie den Namen der app, die lokale SharePoint-URL, die zum Testen Ihrer Website gehostet wird und wie Sie die app gehostet werden soll. Wählen Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p110">Specify the name of the app, the local SharePoint URL that will host your site for testing, and how you want the app to be hosted. Choose **Finish**.</span></span>
    
  

### <a name="create-an-external-content-type"></a><span data-ttu-id="abaa4-165">Erstellen eines externen Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="abaa4-165">Create an external content type</span></span>
<span data-ttu-id="abaa4-166"><a name="bkmk_CreateECT"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-166"><a name="bkmk_CreateECT"> </a></span></span>

<span data-ttu-id="abaa4-167">Um dem Projekt eine BDC-Modell oder externen Inhaltstyp hinzuzufügen, die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="abaa4-167">To add a BDC model or external content type to your project, do the following.</span></span>
  
    
    

### <a name="to-add-an-external-content-type"></a><span data-ttu-id="abaa4-168">So fügen Sie einen externen Inhaltstyp hinzu</span><span class="sxs-lookup"><span data-stu-id="abaa4-168">To add an external content type</span></span>


1. <span data-ttu-id="abaa4-169">Mit dem neuen Projekt weiterhin öffnen Sie, öffnen Sie das Kontextmenü für die Lösung, und wählen Sie **Hinzufügen** und **Inhaltstypen für eine externe Datenquelle**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-169">With your new project still open, open the shortcut menu for the solution, and choose **Add**, **Content types for an External Data source**.</span></span>
    
  
2. <span data-ttu-id="abaa4-p111">Die erste Seite des Assistenten wird verwendet, um die URL des Datendiensts anzugeben. Geben Sie die URL des OData-Diensts, die Sie mit verbinden möchten, klicken Sie auf der Seite **OData-Quelle anzugeben**. Die URL sollte etwa folgendermaßen aussehen: **http://services.odata.org/Northwind/Northwind.svc/**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p111">The first page of the wizard is used to specify the URL of the data service. On the **Specify OData Source** page, enter the URL of the OData service that you want to connect to. The URL should resemble the following: **http://services.odata.org/Northwind/Northwind.svc/**.</span></span>
    
  
3. <span data-ttu-id="abaa4-173">Wählen Sie einen Namen für die OData-Quelle und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="abaa4-173">Choose a name for your OData source, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="abaa4-p112">Es wird eine Liste der Datenentitäten, die vom OData-Dienst verfügbar gemacht werden angezeigt. Stellen Sie sicher, dass das Kontrollkästchen **Listeninstanzen für die ausgewählten Datenentitäten erstellen** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p112">A list of data entities that are being exposed by the OData service appears. Make sure that the **Create list instances for the selected data entities** check box is selected.</span></span>
    
  
5. <span data-ttu-id="abaa4-176">Wählen Sie eine oder mehrere Entitäten, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="abaa4-176">Select one or more of the entities, and choose **Finish**.</span></span>
    
  
6. <span data-ttu-id="abaa4-177">Schritte vor der Bereitstellung Letztes ist die URL in der Datei neu erstellten externen Inhaltstyp zu ändern.</span><span class="sxs-lookup"><span data-stu-id="abaa4-177">The last thing you have to do before deployment is modify the URL in your newly created external content type file.</span></span>
    
    <span data-ttu-id="abaa4-178">Öffnen Sie die .ect-Datei in einem XML-Editor.</span><span class="sxs-lookup"><span data-stu-id="abaa4-178">Open the .ect file in an XML editor.</span></span>
    
  
7. <span data-ttu-id="abaa4-179">Ändern Sie die  `ODataServiceMetadataUrl` -Eigenschaft auf die URL auf dem ermöglicht den Zugriff über den Reverseproxy geleitet.</span><span class="sxs-lookup"><span data-stu-id="abaa4-179">Modify the  `ODataServiceMetadataUrl` property to point to the URL that allows access through the reverse proxy.</span></span>
    
  
8. <span data-ttu-id="abaa4-180">Ändern Sie die  `ODataServiceUrl` -Eigenschaft mit der URL, die über den Reverseproxy Zugriff zulässt.</span><span class="sxs-lookup"><span data-stu-id="abaa4-180">Modify the  `ODataServiceUrl` property with the URL that allows access through the reverse proxy.</span></span>
    
  
<span data-ttu-id="abaa4-181">Informationen zum Hinzufügen eines OData-basierten externen Inhaltstyps finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="abaa4-181">For information about how to add an OData-based external content type, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
  
    
    

### <a name="deploy-the-hybrid-app"></a><span data-ttu-id="abaa4-182">Bereitstellen der Hybrid-app</span><span class="sxs-lookup"><span data-stu-id="abaa4-182">Deploy the hybrid app</span></span>
<span data-ttu-id="abaa4-183"><a name="bkmk_DeployHybridApp"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-183"><a name="bkmk_DeployHybridApp"> </a></span></span>

<span data-ttu-id="abaa4-p113">Wenn Ihre app bereitgestellt wird, können Sie eine Reihe von Auswahlmöglichkeiten. Sie können direkt an eines Mandanten mit F5-Bereitstellung bereitstellen oder Sie können mithilfe der Features zum Veröffentlichen von Visual Studio zum Erstellen einer Datei am Seitenrand packen. Diese Datei kann, der mandantenadministrator SharePoint Online zugewiesen und hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p113">When it is time to deploy your app, you have a couple of choices. You can deploy it directly to a tenancy using F5 deployment, or you can package it using the publishing features of Visual Studio to create an .app file. This file can then be given to the SharePoint Online tenant administrator and uploaded.</span></span>
  
    
    
<span data-ttu-id="abaa4-187">Informationen zum Bereitstellen von SharePoint-Add-Ins finden Sie unter den folgenden:</span><span class="sxs-lookup"><span data-stu-id="abaa4-187">For information about deploying SharePoint Add-ins, see the following:</span></span> 
  
    
    

-  <span data-ttu-id="abaa4-188">[Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](http://msdn.microsoft.com/library/d15a74a7-3c10-485a-9885-7ef11aaa0d90%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="abaa4-188">[Deploying and installing SharePoint Add-ins: methods and options](http://msdn.microsoft.com/library/d15a74a7-3c10-485a-9885-7ef11aaa0d90%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="abaa4-189">[Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="abaa4-189">[Publish SharePoint Add-ins by using Visual Studio](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)</span></span>
    
  
<span data-ttu-id="abaa4-p114">Außerdem können Sie die BDCM-Datei für den externen Inhaltstyp erstellt und zu extrahieren, die auf jeder Ebene oberhalb der app verwendet werden. Dies ist in  [Vorgehensweise: Konvertieren ein Add-in-bezogenen externes Inhaltstyps in mandantenbereichsbezogenen](how-to-convert-an-add-in-scoped-external-content-type-to-tenant-scoped.md)veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="abaa4-p114">You can also take the BDCM file created for the external content type and extract that to be used at any level above the app. This is demonstrated in  [How to: Convert an add-in-scoped external content type to tenant-scoped](how-to-convert-an-add-in-scoped-external-content-type-to-tenant-scoped.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="abaa4-192">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="abaa4-192">See also</span></span>
<span data-ttu-id="abaa4-193"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="abaa4-193"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="abaa4-194">[Hybridlösung für SharePoint](http://technet.microsoft.com/de-DE/library/jj838715.aspx)</span><span class="sxs-lookup"><span data-stu-id="abaa4-194">[Hybrid for SharePoint](http://technet.microsoft.com/de-DE/library/jj838715.aspx)</span></span>
    
  
-  [<span data-ttu-id="abaa4-195">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="abaa4-195">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="abaa4-196">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="abaa4-196">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  <span data-ttu-id="abaa4-197">[Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="abaa4-197">[Publish SharePoint Add-ins by using Visual Studio](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)</span></span>
    
  

