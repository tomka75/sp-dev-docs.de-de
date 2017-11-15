---
title: Add-in-bezogenen externen Inhaltstypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a34cbbba-dc38-4d3d-b796-d54b5848bdfb
ms.openlocfilehash: b551602cd4a87422e50e5523e86b6a5e5be8514b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="add-in-scoped-external-content-types-in-sharepoint"></a><span data-ttu-id="979e7-102">Add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-102">Add-in-scoped external content types in SharePoint</span></span>
<span data-ttu-id="979e7-103">Erfahren Sie mehr über externe Inhaltstypen, die installiert oder auf der Ebene-Add-Ins in SharePoint ausgelegt sind, und aktivieren Sie reichhaltige SharePoint-Add-Ins mit externen Datenquellen erstellen.</span><span class="sxs-lookup"><span data-stu-id="979e7-103">Learn about external content types that are installed or scoped at the add-in level in SharePoint and enable you to create data-rich SharePoint Add-ins using external data sources.</span></span>
## <a name="overview-of-add-in-scoped-external-content-types-in-sharepoint"></a><span data-ttu-id="979e7-104">Übersicht über die add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-104">Overview of add-in-scoped external content types in SharePoint</span></span>
<span data-ttu-id="979e7-105"><a name="Appscopedect_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-105"></span></span>

<span data-ttu-id="979e7-p101">In SharePoint 2010 können Sie installieren und Verwenden von externen Inhaltstypen nur auf Farmebene. Daraufhin wird häufig Probleme für Entwickler, da auch für einfache Applications Administrator beteiligten aufgrund der Zugriffsrechte sein, die erforderlich sind musste, um auf Farmebene zu installieren.</span><span class="sxs-lookup"><span data-stu-id="979e7-p101">In SharePoint 2010, you can install and use external content types only at the farm level. This often causes problems for developers because even for simple applications, an administrator had to be involved because of the access rights that are needed to install at the farm level.</span></span>
  
    
    
<span data-ttu-id="979e7-p102">In SharePoint sind Anwendungen im Wesentlichen in mehr autonomen Einheiten mit dem Namen -add-insisoliert. -Add-ins enthalten alle Ressourcen, die sie ausführen müssen. Dieser Ansatz ermöglicht eine aktive Anwendung auf aus anderen Anwendungen isoliert werden. Die Vorteile dieser Architektur sind wie folgt:</span><span class="sxs-lookup"><span data-stu-id="979e7-p102">In SharePoint, applications are basically isolated into more autonomous units called add-ins. Add-ins contain all the resources they need to run. This approach enables a running application to be insulated from other applications. The benefits of this architecture are as follows:</span></span>
  
    
    

- <span data-ttu-id="979e7-111">Erstellen Sie add-ins, die an das neue Anwendungsmodell des SharePoint ausgerichtet werden.</span><span class="sxs-lookup"><span data-stu-id="979e7-111">You can create add-ins that are aligned with the new application model of SharePoint.</span></span>
    
  
- <span data-ttu-id="979e7-112">Erstellen Sie add-ins, die Zugriff auf externe Daten von SAP, Netflix, und proprietäre und andere Typen von Daten ohne im Zusammenhang mit der mandantenadministrator.</span><span class="sxs-lookup"><span data-stu-id="979e7-112">You can create add-ins that access external data from SAP, Netflix, and proprietary and other types of data without involving the tenant administrator.</span></span>
    
  
- <span data-ttu-id="979e7-113">Zugriff auf externe Anwendungen wird durch Business Connectivity Services (BCS), beibehalten, die eine konsistente und einheitliche Benutzeroberfläche bereitstellt, die von anderen SharePoint-Anwendungen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="979e7-113">Access to external applications is maintained through Business Connectivity Services (BCS), which provides a consistent and uniform interface that can be used by other SharePoint applications.</span></span>
    
  
<span data-ttu-id="979e7-114">Add-in-bezogenen externe Inhaltstypen ermöglichen den Zugriff auf externe Daten in einer app.</span><span class="sxs-lookup"><span data-stu-id="979e7-114">Add-in-scoped external content types provide access to external data within an app.</span></span>
  
    
    

## <a name="prerequisites-for-working-with-add-in-scoped-external-content-types"></a><span data-ttu-id="979e7-115">Erforderliche Komponenten für die Arbeit mit der add-in-bezogenen externen Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="979e7-115">Prerequisites for working with add-in-scoped external content types</span></span>
<span data-ttu-id="979e7-116"><a name="Appscopedect_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-116"></span></span>

<span data-ttu-id="979e7-117">Im folgenden sind die Anforderungen für die Entwicklung von externen Inhaltstypen, die auf der Ebene der Add-in-Bereich haben:</span><span class="sxs-lookup"><span data-stu-id="979e7-117">The following are the requirements for developing external content types that are scoped at the add-in level:</span></span>
  
    
    

- <span data-ttu-id="979e7-118">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="979e7-118">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="979e7-119">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="979e7-119">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="979e7-120">SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-120">SharePoint</span></span>
    
  
<span data-ttu-id="979e7-121">Informationen dazu, wie Sie Ihre SharePoint-Entwicklungsumgebung einrichten, finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="979e7-121">For information about setting up your SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="add-in-scoped-external-content-type-essentials"></a><span data-ttu-id="979e7-122">Add-in-bezogenen externen Inhaltstyp essentials</span><span class="sxs-lookup"><span data-stu-id="979e7-122">Add-in-scoped external content type essentials</span></span>

<span data-ttu-id="979e7-123">Tabelle 1 enthält einige wichtige Konzepte, denen Sie mit vertraut beim Arbeiten mit der add-in-bezogenen externen Inhaltstypen sein sollten.</span><span class="sxs-lookup"><span data-stu-id="979e7-123">Table 1 contains some core concepts that you should be familiar with when working with add-in-scoped external content types.</span></span>
  
    
    

<span data-ttu-id="979e7-124">**In Tabelle 1. Kernkonzepte für das Verständnis von add-in-bezogenen externer Inhaltstypen**</span><span class="sxs-lookup"><span data-stu-id="979e7-124">**Table 1. Core concepts for understanding add-in-scoped external content types**</span></span>


|<span data-ttu-id="979e7-125">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="979e7-125">**Article**</span></span>|<span data-ttu-id="979e7-126">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="979e7-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="979e7-127">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-127">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="979e7-128">Erfahren Sie, wie BCS externen Inhaltstypen erstellen.</span><span class="sxs-lookup"><span data-stu-id="979e7-128">Learn how to create BCS external content types.</span></span>  <br/> |
| [<span data-ttu-id="979e7-129">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="979e7-129">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="979e7-130">Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="979e7-130">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>  <br/> |
| [<span data-ttu-id="979e7-131">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="979e7-131">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx) <br/> |<span data-ttu-id="979e7-132">Informationen Sie zur Erstellung eines einfachen SharePoint-Hosting add-Ins mithilfe der Office Developer Tools für Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="979e7-132">Learn how to create a basic SharePoint-hosted add-in by using the Office Developer Tools for Visual Studio 2012.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-add-in-scoped-external-content-types"></a><span data-ttu-id="979e7-133">Was können Sie mit der add-in-bezogenen externen Inhaltstypen?</span><span class="sxs-lookup"><span data-stu-id="979e7-133">What can you do with add-in-scoped external content types?</span></span>
<span data-ttu-id="979e7-134"><a name="Appscopedect_Tasks"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-134"></span></span>

<span data-ttu-id="979e7-p103">Der Hauptgrund für das Hinzufügen eines Add-in-bezogenen externen Inhaltstyps ist für den Zugriff auf externe Daten aus einer einzelnen-Add-in. Hiermit können Sie folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="979e7-p103">The primary reason for adding an add-in-scoped external content type is to provide access to external data from an individual add-in. This allows you to do the following:</span></span> 
  
    
    

- <span data-ttu-id="979e7-137">Einschränken des Zugriffs auf externe Inhaltstypen zu einer bestimmten app.</span><span class="sxs-lookup"><span data-stu-id="979e7-137">Limit access to external content types to a particular app.</span></span>
    
  
- <span data-ttu-id="979e7-138">Bereitstellen von externen Inhaltstypen in einer app.</span><span class="sxs-lookup"><span data-stu-id="979e7-138">Deploy external content types within an app.</span></span>
    
  

### <a name="create-add-in-scoped-external-content-types"></a><span data-ttu-id="979e7-139">Erstellen von add-in-bezogenen externen Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="979e7-139">Create add-in-scoped external content types</span></span>
<span data-ttu-id="979e7-140"><a name="Appscopedect_createect"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-140"></span></span>

<span data-ttu-id="979e7-p104">Das Konzept eines Katalogs dateibasierten Metadaten wurde in SharePoint 2010 eingeführt. Es können Sie angeben, dass eine Datei mit dem XML benötigt, um externe Inhaltstypen zu definieren. Diese Datei in eine WSP-Paket bereitgestellt werden kann und bezieht sich nur auf die Anwendung, der sie für ausgelegt ist. Mithilfe dieser Metadatendatei können externe Inhaltstypen auf die-Add-in-Ebene beschränkt.</span><span class="sxs-lookup"><span data-stu-id="979e7-p104">The concept of a file-based metadata catalog was introduced in SharePoint 2010. It enables you to specify a file that contains the XML needed to define external content types. This file can be deployed within a WSP package and pertains only to the application that it is scoped for. By using this metadata file, external content types can be restricted to the add-in level.</span></span>
  
    
    
<span data-ttu-id="979e7-145">In SharePoint wurde **SPListDataSource** geändert, um eine Eigenschaft hinzuzufügen, die den Bereich der Anwendung angibt.</span><span class="sxs-lookup"><span data-stu-id="979e7-145">In SharePoint, **SPListDataSource** has been modified to add a property that indicates the scope of the application.</span></span>
  
    
    
<span data-ttu-id="979e7-p105">Diese Klasse dient als die Brücke zwischen **SPList** und einer externen Liste. Verwenden Sie die zugeordneten **SPList** Entitätsfelder und Daten abgerufen. Eine Instanz des **SPListDataSource** aus der **HasExternalDataSource** -Eigenschaft abrufen. Wenn **HasExternalDataSource** nicht null ist, ist das **SPList** -Objekt Daten außerhalb SharePoint.</span><span class="sxs-lookup"><span data-stu-id="979e7-p105">This class serves as the bridge between **SPList** and an external list. Use the associated **SPList** to retrieve entity fields and data. Retrieve an instance of **SPListDataSource** from the **HasExternalDataSource** property. When **HasExternalDataSource** is not null, the **SPList** object's data is external to SharePoint.</span></span>
  
    
    
<span data-ttu-id="979e7-150">Wenn Sie einen Add-in-bezogenen externen Inhaltstyp hinzufügen möchten, ist diese Eigenschaft auf **Add-in**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="979e7-150">When you want to add an add-in-scoped external content type, this property is set to **Add-in**.</span></span>
  
    
    
<span data-ttu-id="979e7-p106">Die **MetadataCatalogFileName** -Eigenschaft wird verwendet, um die BDC-Modelldatei zu definieren, die die Definition des externen Inhaltstyps enthält. Diese Eigenschaft kann deklarativ oder programmgesteuert definiert werden, aber nicht in der SharePoint-Benutzeroberfläche (UI).</span><span class="sxs-lookup"><span data-stu-id="979e7-p106">The **MetadataCatalogFileName** property is used to define the BDC model file that contains the external content type definition. This property can be defined declaratively or programmatically, but not in the SharePoint user interface (UI).</span></span>
  
    
    
<span data-ttu-id="979e7-153">Im folgenden Beispiel wird gezeigt, wie Sie die **MetadataCatalogFileName**-Eigenschaft deklarativ festlegen können.</span><span class="sxs-lookup"><span data-stu-id="979e7-153">The following example shows how to set the **MetadataCatalogFileName** property declaratively.</span></span>
  
    
    



```XML

<DataSource>
  <Property Name="Entity" Value="Customer" />
  <Property Name="EntityNamespace" Value="SAP" />
  <Property Name="LobSystemInstanceName" Value="SAPClient1" />
  <Property Name="SpecificFinder" Value="ReadCustomer" />
  <Property Name=" MetadataCatalogFileName" Value="BDCMetadata.bdcm" />
</DataSource>
```


> <span data-ttu-id="979e7-154">**Hinweis:** Websiteadministratoren können Add-Ins installieren, die App-bezogene externe Inhaltstypen verwenden, nur SiteCollection-Administratoren können jedoch Apps Berechtigungen zum Verwenden von BCS-Verbindungen gewähren.</span><span class="sxs-lookup"><span data-stu-id="979e7-154">**Note** Site administrators can install add-ins that use App-Scoped-ECTs, but only SiteCollection administrators can grant permissions for Apps to Use BCS Connections.</span></span> 
  
    
    


### <a name="deploy-an-add-in-scoped-external-content-type-in-a-custom-feature-in-a-wsp-file"></a><span data-ttu-id="979e7-155">Bereitstellen eines Add-In-bezogenen externen Inhaltstyps in einer benutzerdefinierten Funktion in einer WSP-Datei</span><span class="sxs-lookup"><span data-stu-id="979e7-155">Deploy an add-in-scoped external content type in a custom Feature in a WSP file</span></span>
<span data-ttu-id="979e7-156"><a name="Appscopedect_deployect"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-156"></span></span>

<span data-ttu-id="979e7-p107">Sie können ein BDC-Modell in eine WSP-Datei für die Bereitstellung einschließen. Im folgenden Beispiel wird veranschaulicht, wie ein BDC-Modell in der app werden soll.</span><span class="sxs-lookup"><span data-stu-id="979e7-p107">You can include a BDC model in a WSP file for deployment. The following example shows how to include a BDC model in the app.</span></span>
  
    
    

```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
  </BdcModel>
</Elements>

```


> <span data-ttu-id="979e7-159">**Wichtig:** Es kann nur eine BDC-Modelldatei pro Add-In verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="979e7-159">**Important:** Only one BDC model file can be included per add-in.</span></span> <span data-ttu-id="979e7-160">In diesem Beispiel lautet der Dateiname BDCMetadata.bdcm, der Modelldateiname kann beliebig sein, solange dieser dem Dateinamen im **Path**-Attribut der BDC-Modelldatei entspricht.</span><span class="sxs-lookup"><span data-stu-id="979e7-160">Important Only one BDC model file can be included per add-in. While the file name in this example is BDCMetadata.bdcm, the model file can actually be any name you choose as long as the file name matches that is in the **Path** attribute of the BDC model file.</span></span>
  
    
    


> <span data-ttu-id="979e7-161">**Hinweis:** Nur Open Data Protocol (OData)-Verbindungen sind für Add-In-bezogene externe Inhaltstypen zulässig.</span><span class="sxs-lookup"><span data-stu-id="979e7-161">**Note** Only Open Data protocol (OData) connections are allowed for add-in-scoped external content types.</span></span> 
  
    
    


### <a name="set-security-credentials-for-an-external-system"></a><span data-ttu-id="979e7-162">Festlegen von Sicherheitsanmeldeinformationen für ein externes System</span><span class="sxs-lookup"><span data-stu-id="979e7-162">Set security credentials for an external system</span></span>
<span data-ttu-id="979e7-163"><a name="Appscopedect_deployect"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-163"></span></span>

<span data-ttu-id="979e7-164">Um Daten für eine sichere externe System zugreifen zu können, müssen Sie das BDC-Modell mit den entsprechenden Anmeldeinformationen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="979e7-164">In order to access data on a secured external system, you must configure the BDC model with the appropriate credentials.</span></span>
  
    
    
<span data-ttu-id="979e7-165">Im folgenden Beispiel wird gezeigt, wie durch Bearbeiten der Datei "Elements.xml" der app Sicherheitsanmeldeinformationen für ein externes System add-in-bezogenen externen Inhaltstypen festgelegt.</span><span class="sxs-lookup"><span data-stu-id="979e7-165">The following example shows how to set security credentials for an external system in add-in-scoped external content types by modifying the Elements.xml file of the app.</span></span>
  
    
    



```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
    <LobSystem Name="SAP">
       <LobSystemInstance Name="SAPInst" RequireCredentials="true" CredentialsDescription="Credentials to connect to SAP"/>
    </LobSystem>
    <LobSystem Name="SQL">
       <LobSystemInstance Name="App Database" DataSource="SQL-Azure" RequireCredentials="true" />
    </LobSystem>
  </BdcModel>
</Elements>

```


## <a name="in-this-section"></a><span data-ttu-id="979e7-166">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="979e7-166">In this section</span></span>
<span data-ttu-id="979e7-167"><a name="Appscopedect_inthissection"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-167"></span></span>


-  [<span data-ttu-id="979e7-168">Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-168">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-169">Vorgehensweise: Zugriff auf externe Daten mit REST in der SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-169">How to: Access external data with REST in SharePoint</span></span>](how-to-access-external-data-with-rest-in-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="979e7-170">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="979e7-170">Additional resources</span></span>
<span data-ttu-id="979e7-171"><a name="Appscopedect_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="979e7-171"></span></span>


-  [<span data-ttu-id="979e7-172">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-172">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-173">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-173">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-174">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="979e7-174">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="979e7-175">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-175">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-176">Externe Ereignisse und Warnungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-176">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-177">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-177">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="979e7-178">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="979e7-178">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

