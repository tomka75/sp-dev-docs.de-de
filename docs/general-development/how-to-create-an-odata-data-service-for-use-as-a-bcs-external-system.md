---
title: "Erstellen eines OData-Datendiensts für die Verwendung als BCS-externes System"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d7b3aa6-85b7-400d-8ea5-50bebac56a1d
ms.openlocfilehash: 71c2397d1064746db45a55b05452352dc6c8ef5c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-odata-data-service-for-use-as-a-bcs-external-system"></a><span data-ttu-id="0b41f-102">Erstellen eines OData-Datendiensts für die Verwendung als BCS-externes System</span><span class="sxs-lookup"><span data-stu-id="0b41f-102">How to: Create an OData data service for use as a BCS external system</span></span>

<span data-ttu-id="0b41f-p101">In diesem Artikel erfahren sie, wie Sie einen im Internet aufrufbaren WCF-Dienst erstellen, der OData zum Senden von Benachrichtigungen an SharePoint verwendet, wenn die zugrunde liegenden Daten geändert werden. Mithilfe dieser Benachrichtigungen werden Ereignisse ausgelöst, die mit externen Listen verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="0b41f-p101">Learn how to create an Internet-addressable WCF service that uses OData to send notifications to SharePoint when the underlying data changes. These notifications are used to trigger events that are attached to external lists.</span></span>

<span data-ttu-id="0b41f-105">In diesem Artikel wird beschrieben, wie ein  ASP.NET Windows Communication Foundation (WCF)-Datendienst erstellt wird, um die AdventureWorks 2012 LT-Beispieldatenbank verfügbar zu  machen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-105">This article describes how to create an ASP.NET Windows Communication Foundation (WCF) Data Service to expose the AdventureWorks 2012 LT sample database.</span></span> <span data-ttu-id="0b41f-106">Auf diese Weise können Sie über das Open Data-Protokoll (OData) auf die Daten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-106">This enables you to access the data through the Open Data protocol (OData).</span></span> <span data-ttu-id="0b41f-107">Wenn der Zugriff über OData hergestellt wurde, können Sie den externen Inhaltstyp „Business Connectivity Services (BCS)“ konfigurieren, der ermöglicht, dass SharePoint die Daten aus der externen Datenbank verwendet.</span><span class="sxs-lookup"><span data-stu-id="0b41f-107">When access is established through OData, you can configure a Business Connectivity Services (BCS) external content type that will enable SharePoint to consume the data from the external database.</span></span> <span data-ttu-id="0b41f-108">Zur weiteren Verbesserung dieser OData-Quelle können Sie Dienstverträge zum WCF-Dienst hinzufügen, sodass BCS Benachrichtigungen abonnieren kann, die darauf hinweisen, dass sich die externen Daten geändert haben.</span><span class="sxs-lookup"><span data-stu-id="0b41f-108">To further enhance this OData source, you can add service contracts to the WCF service that will enable BCS to subscribe to notifications that indicate that the external data has changed.</span></span>
  
    
    


## <a name="prerequisites-for-creating-the-odata-service"></a><span data-ttu-id="0b41f-109">Voraussetzungen für die Erstellung des OData-Diensts</span><span class="sxs-lookup"><span data-stu-id="0b41f-109">Prerequisites for creating the OData service</span></span>
<span data-ttu-id="0b41f-110"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="0b41f-110"></span></span>

<span data-ttu-id="0b41f-111">Folgende sind zum Erstellen des OData-Diensts in diesem Artikel erforderlich:</span><span class="sxs-lookup"><span data-stu-id="0b41f-111">The following are required to create the OData service in this article:</span></span>
  
    
    

- <span data-ttu-id="0b41f-112">Ein Server mit Internet Information Services (IIS)</span><span class="sxs-lookup"><span data-stu-id="0b41f-112">A server hosting Internet Information Services (IIS)</span></span>
    
  
- <span data-ttu-id="0b41f-113">.NET Framework 3.5 oder höher</span><span class="sxs-lookup"><span data-stu-id="0b41f-113">.NET Framework 3.5 or later</span></span>
    
  
- <span data-ttu-id="0b41f-114">SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-114">SharePoint</span></span>
    
  
-  [<span data-ttu-id="0b41f-115">AdventureWorks 20012 LT-Skript</span><span class="sxs-lookup"><span data-stu-id="0b41f-115">AdventureWorks 20012 LT script</span></span>](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
-  [<span data-ttu-id="0b41f-116">AdventureWorks 2012 LT Daten</span><span class="sxs-lookup"><span data-stu-id="0b41f-116">AdventureWorks 2012 LT Data</span></span>](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
- <span data-ttu-id="0b41f-117">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="0b41f-117">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="0b41f-118">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="0b41f-118">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="0b41f-119">Informationen zum Einrichten Ihrer Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0b41f-119">For information about setting up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="core-concepts-for-creating-an-odata-service"></a><span data-ttu-id="0b41f-120">Kernkonzepte für das Erstellen eines OData-Diensts</span><span class="sxs-lookup"><span data-stu-id="0b41f-120">Core concepts for creating an OData service</span></span>

<span data-ttu-id="0b41f-121">In Tabelle 1 sind Artikel aufgeführt, Ihnen das Verständnis der Kernkonzepte der Erstellung von einem WCF-Dienst mithilfe von OData und externen Inhalt werden.</span><span class="sxs-lookup"><span data-stu-id="0b41f-121">Table 1 lists articles that will help you understand the core concepts of building a WCF service using OData and external content.</span></span>
  
    
    

<span data-ttu-id="0b41f-122">**In Tabelle 1. Kernkonzepte für das Erstellen eines OData-Diensts**</span><span class="sxs-lookup"><span data-stu-id="0b41f-122">**Table 1. Core concepts for creating an OData service**</span></span>


|<span data-ttu-id="0b41f-123">**Resource**</span><span class="sxs-lookup"><span data-stu-id="0b41f-123">**Resource**</span></span>|<span data-ttu-id="0b41f-124">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="0b41f-124">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="0b41f-125">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-125">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="0b41f-126">Enthält Informationen, die Sie mit dem Erstellen von externer Inhaltstypen basierend auf OData-Quellen und Verwenden der Daten in SharePoint oder Office 2013-Komponenten unterstützen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-126">Provides information to help you start creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>  <br/> |
| [<span data-ttu-id="0b41f-127">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-127">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="0b41f-128">Erfahren Sie, wie Visual Studio 2012 verwenden, um eine veröffentlichte OData-Quelle ermitteln und erstellen Sie einen wiederverwendbaren externen Inhaltstyp im BCS in SharePoint verwenden.</span><span class="sxs-lookup"><span data-stu-id="0b41f-128">Learn how to use Visual Studio 2012 to discover a published OData source and create a reusable external content type to use in BCS in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="0b41f-129">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="0b41f-129">Open Data Protocol</span></span>](http://www.odata.org) <br/> |<span data-ttu-id="0b41f-130">Enthält Informationen zu den Open Data Protocol, einschließlich Definitionen des Protokolls, architektonische Informationen und Beispiele für die Verwendung.</span><span class="sxs-lookup"><span data-stu-id="0b41f-130">Provides information about the Open Data protocol, including protocol definitions, architectural information and usage examples.</span></span>  <br/> |
| [<span data-ttu-id="0b41f-131">WCF Data Services (Übersicht)</span><span class="sxs-lookup"><span data-stu-id="0b41f-131">WCF Data Services Overview</span></span>](http://msdn.microsoft.com/de-DE/library/cc668794.aspx) <br/> |<span data-ttu-id="0b41f-p103">WCF Data Services ermöglicht die Erstellung und Verwendung von Data Services für das Internet oder Intranet mithilfe von OData. OData können Sie Ihre Daten als Ressourcen verfügbar machen, adressierbar über URIs sind.</span><span class="sxs-lookup"><span data-stu-id="0b41f-p103">WCF Data Services enables creation and consumption of data services for the web or an intranet by using OData. OData enables you to expose your data as resources that are addressable by URIs.</span></span>  <br/> |
| [<span data-ttu-id="0b41f-134">Entwickeln und Bereitstellen von WCF Data Services</span><span class="sxs-lookup"><span data-stu-id="0b41f-134">Developing and Deploying WCF Data Services</span></span>](http://msdn.microsoft.com/de-DE/library/gg258442) <br/> |<span data-ttu-id="0b41f-135">Enthält Informationen zu entwickeln und Bereitstellen von WCF Data Services.</span><span class="sxs-lookup"><span data-stu-id="0b41f-135">Provides information about developing and deploying WCF Data Services.</span></span>  <br/> |
   

### <a name="steps-involved-in-creating-the-external-system"></a><span data-ttu-id="0b41f-136">Schritte zum Erstellen des externen Systems</span><span class="sxs-lookup"><span data-stu-id="0b41f-136">Steps involved in creating the external system</span></span>

<span data-ttu-id="0b41f-137">Die folgenden Schritte ausgeführt werden müssen</span><span class="sxs-lookup"><span data-stu-id="0b41f-137">The following steps will need to be completed</span></span> 
  
    
    

- <span data-ttu-id="0b41f-138">Installieren der AdventureWorks 2012 LT-Beispieldatenbank</span><span class="sxs-lookup"><span data-stu-id="0b41f-138">Install the AdventureWorks 2012 LT sample database</span></span>
    
  
- <span data-ttu-id="0b41f-139">Erstellen des OData-Diensts</span><span class="sxs-lookup"><span data-stu-id="0b41f-139">Create the OData Service</span></span>
    
  
- <span data-ttu-id="0b41f-140">Festlegen von Zugriffsberechtigungen</span><span class="sxs-lookup"><span data-stu-id="0b41f-140">Set access permissions</span></span>
    
  
- <span data-ttu-id="0b41f-141">Testen Sie den Dienst</span><span class="sxs-lookup"><span data-stu-id="0b41f-141">Test the service</span></span>
    
  
- <span data-ttu-id="0b41f-142">Hinzufügen von Funktionen für zusätzliche BCS-Funktionen</span><span class="sxs-lookup"><span data-stu-id="0b41f-142">Add capabilities for additional BCS functionality</span></span>
    
  

## <a name="installing-the-sample-database"></a><span data-ttu-id="0b41f-143">Installieren der Beispieldatenbank</span><span class="sxs-lookup"><span data-stu-id="0b41f-143">Installing the sample database</span></span>
<span data-ttu-id="0b41f-144"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="0b41f-144"></span></span>

<span data-ttu-id="0b41f-145">Ein externes System ist in der Regel eine Datenbank, und aus diesem Grund in diesem Beispiel wird veranschaulicht, wie die 2012-LT AdventureWorks-Beispieldatenbank verwenden, um eine proprietäre Datenquelle darstellen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-145">An external system is usually a database and for that reason, this example shows how to use the AdventureWorks 2012 LT sample database to represent a proprietary datasource.</span></span>
  
    
    
<span data-ttu-id="0b41f-146">Die folgenden Schritte wird</span><span class="sxs-lookup"><span data-stu-id="0b41f-146">The following steps will</span></span> 
  
    
    

## <a name="how-to-create-the-wcf-odata-service"></a><span data-ttu-id="0b41f-147">Zum Erstellen der WCF OData-Dienst</span><span class="sxs-lookup"><span data-stu-id="0b41f-147">How to create the WCF OData service</span></span>
<span data-ttu-id="0b41f-148"><a name="bkmk_CreatingTheService"> </a></span><span class="sxs-lookup"><span data-stu-id="0b41f-148"></span></span>

<span data-ttu-id="0b41f-p104">Erstellen einen Windows Communication Foundation (WCF)-Dienst, der über den OData-Protokoll zugegriffen werden kann, ist relativ einfach. Visual Studio 2012 bietet verschiedene Tools zum automatisch erkennen und die Daten aus verschiedenen Datenquellen modellieren. Dadurch können Sie zum Erstellen von Verbindungen und Schnittstellen mit Daten in SQL Server-Datenbanken und anderen Arten von Datenspeichern, die bei der Verwendung von eines umfangreiches Objektmodells programmgesteuert bearbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="0b41f-p104">Creating a Windows Communication Foundation (WCF) service that can be accessed through the OData protocol is relatively straightforward. Visual Studio 2012 provides several tools for automatically discovering and modeling the data from various data sources. This allows you to create connections and interfaces to data in SQL Server databases and other types of data stores that can then be worked with programmatically using an extensive object model.</span></span>
  
    
    
<span data-ttu-id="0b41f-152">SharePoint aktivieren BCS Benachrichtigungen von remote-Systemen ausgegeben, wenn die zugrunde liegenden Daten geändert haben, müssen Sie jedoch den WCF-Dienst, um auf diese Änderungen reagieren ändern.</span><span class="sxs-lookup"><span data-stu-id="0b41f-152">However, for SharePoint to enable BCS to receive notifications from remote systems when the underlying data has changed, you must modify the WCF service to respond to those changes.</span></span>
  
    
    

### <a name="to-create-a-new-wcf-project"></a><span data-ttu-id="0b41f-153">So erstellen Sie ein neues WCF-Projekt</span><span class="sxs-lookup"><span data-stu-id="0b41f-153">To create a new WCF project</span></span>


1. <span data-ttu-id="0b41f-154">Wählen Sie im Visual Studio, klicken Sie im Menü **Datei** auf **neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-154">In Visual Studio, on the **File** menu, choose **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="0b41f-155">Klicken Sie im Dialogfeld **Neues Projekt** wählen Sie **die Vorlage** aus, und wählen Sie dann **ASP.NET-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-155">In the **New Project** dialog box, choose the **Web** template, and then choose **ASP.NET Web Application**.</span></span>
    
  
3. <span data-ttu-id="0b41f-156">Geben Sie **AdventureWorksService** für den Projektnamen, und wählen Sie **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-156">Enter **AdventureWorksService** for the project name, and choose **OK**.</span></span>
    
  
4. <span data-ttu-id="0b41f-157">Klicken Sie im **Projektmappen-Explorer** öffnen Sie das Kontextmenü für das ASP.NET-Projekt, das Sie gerade erstellt haben, und wählen Sie **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-157">In **Solution Explorer**, open the shortcut menu for the ASP.NET project that you just created, and choose **Properties**.</span></span>
    
  
5. <span data-ttu-id="0b41f-158">Wählen Sie die Registerkarte **Web**, und legen Sie den Wert des Textfelds **bestimmte Ports** auf8008.</span><span class="sxs-lookup"><span data-stu-id="0b41f-158">Select the **Web** tab, and set the value of the **Specific port** text box to8008.</span></span>
    
  

### <a name="to-define-the-data-model"></a><span data-ttu-id="0b41f-159">So definieren Sie das Datenmodell</span><span class="sxs-lookup"><span data-stu-id="0b41f-159">To define the data model</span></span>


1. <span data-ttu-id="0b41f-160">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt ASP.NET, und wählen Sie **Neues Element hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-160">In **Solution Explorer**, open the shortcut menu for the ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="0b41f-161">Klicken Sie im Dialogfeld **Neues Element hinzufügen** Auswählen der Datenvorlage, und wählen Sie dann **ADO.NET Entitätsdatenmodell**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-161">In the **Add New Item** dialog box, choose the Data template, and then choose **ADO.NET Entity Data Model**.</span></span>
    
  
3. <span data-ttu-id="0b41f-162">Geben Sie den Namen des Datenmodells zu **AdventureWorks.edmx**aus.</span><span class="sxs-lookup"><span data-stu-id="0b41f-162">For the name of the data model, enter **AdventureWorks.edmx**.</span></span>
    
  
4. <span data-ttu-id="0b41f-163">Im **Entity Data Model Wizard** wählen Sie **aus Datenbank generieren**, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-163">In the **Entity Data Model Wizard**, choose **Generate from Database**, and then choose **Next**.</span></span>
    
  
5. <span data-ttu-id="0b41f-164">Verbinden Sie das Datenmodell mit der Datenbank führen Sie einen der folgenden Schritte aus, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-164">Connect the data model to the database by doing one of the following steps, and then choose **Next**.</span></span>
    
  - <span data-ttu-id="0b41f-165">Wenn Sie keine datenbankverbindung bereits konfiguriert haben, wählen Sie **Neue Verbindung** aus, und erstellen Sie eine neue Verbindung.</span><span class="sxs-lookup"><span data-stu-id="0b41f-165">If you do not have a database connection already configured, choose **New Connection**, and create a new connection.</span></span>
    
  
  - <span data-ttu-id="0b41f-166">Wenn Sie eine Verbindung zum Verbinden mit der Nordwind-Datenbank bereits konfiguriert haben, wählen Sie diese Verbindung in der Liste der Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-166">If you have a database connection already configured to connect to the Northwind database, choose that connection in the list of connections.</span></span>
    
  
  - <span data-ttu-id="0b41f-167">Wählen Sie auf der letzten Seite des Assistenten die Kontrollkästchen für alle Tabellen in der Datenbank, und deaktivieren Sie die Kontrollkästchen für die Ansichten und gespeicherte Prozeduren.</span><span class="sxs-lookup"><span data-stu-id="0b41f-167">On the final page of the wizard, select the check boxes for all tables in the database, and clear the check boxes for views and stored procedures.</span></span>
    
  
6. <span data-ttu-id="0b41f-168">Wählen Sie auf **Fertig stellen**, um den Assistenten zu schließen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-168">Choose **Finish** to close the wizard.</span></span>
    
  

### <a name="to-create-the-data-service"></a><span data-ttu-id="0b41f-169">So erstellen Sie den Datendienst</span><span class="sxs-lookup"><span data-stu-id="0b41f-169">To create the data service</span></span>


1. <span data-ttu-id="0b41f-170">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für Ihr Projekt ASP.NET, und wählen Sie dann auf **Neues Element hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-170">In **Solution Explorer**, open the shortcut menu for your ASP.NET project, and then choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="0b41f-171">Wählen Sie im Dialogfeld **Neues Element hinzufügen** **WCF Data Service**.</span><span class="sxs-lookup"><span data-stu-id="0b41f-171">In the **Add New Item** dialog box, choose **WCF Data Service**.</span></span>
    
  
3. <span data-ttu-id="0b41f-172">Geben Sie für den Namen des Diensts **AdventureWorks**ein.</span><span class="sxs-lookup"><span data-stu-id="0b41f-172">For the name of the service, enter **AdventureWorks**.</span></span>
    
    <span data-ttu-id="0b41f-p105">Visual Studio wird die XML-Markup und Code-Dateien für den neuen Dienst erstellt. In der Standardeinstellung öffnet das Code-Editor-Fenster. Klicken Sie im **Projektmappen-Explorer**, der Dienst hat den Namen **AdventureWorks**, mit der Erweiterung. svc.cs oder. svc.vb.</span><span class="sxs-lookup"><span data-stu-id="0b41f-p105">Visual Studio creates the XML markup and code files for the new service. By default, the code-editor window opens. In **Solution Explorer**, the service will have the name, **AdventureWorks**, with the extension .svc.cs or .svc.vb.</span></span>
    
  
4. <span data-ttu-id="0b41f-p106">Ersetzen Sie den Kommentar  `/* TODO: put your data source class name here */` in der Definition der Klasse, die den Datendienst mit dem Typ definiert, die Entitäten-Container des Datenmodells, die in diesem Fall **AdventureWorksEntities** ist. Die Definition der Klasse sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="0b41f-p106">Replace the comment  `/* TODO: put your data source class name here */` in the definition of the class that defines the data service with the type that is the entity container of the data model, which in this case is **AdventureWorksEntities**. The class definition should look like the following:</span></span>
    
```cs
  
public class AdventureWorks : DataService<AdventureWorksEntities>
```

<span data-ttu-id="0b41f-p107">Standardmäßig beim Dienst WCF erstellt wurde, kann es aufgrund der Sicherheitskonfiguration zugegriffen werden. Im nächsten Schritt können, die Sie angeben, die darauf zugreifen können und welche Berechtigungen, besitzen.</span><span class="sxs-lookup"><span data-stu-id="0b41f-p107">By default, when a WCF service is created, it cannot be accessed due to its security configuration. The next step lets you specify who can access it, and what rights they have.</span></span>
  
    
    

### <a name="to-enable-access-to-data-service-resources"></a><span data-ttu-id="0b41f-180">Zugriff auf Daten Dienstressourcen unterstützt</span><span class="sxs-lookup"><span data-stu-id="0b41f-180">To enable access to data service resources</span></span>


- <span data-ttu-id="0b41f-181">Ersetzen Sie den Platzhalter-Code in der **InitializeService** -Funktion im Code für den Datendienst durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="0b41f-181">In the code for the data service, replace the placeholder code in the **InitializeService** function with the following.</span></span>
    
```cs
  
      config.SetEntitySetAccessRule("*", EntitySetRights.All);
      config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


    This enables authorized clients to have read and write access to resources for the specified entity sets.
    
    > **Note:**
      > Any client that can access the ASP.NET application can also access the resources that are exposed by the data service. In a production data service, to prevent unauthorized access to resources, you should also secure the application itself. For more information, see  [Securing WCF Data Services](http://msdn.microsoft.com/en-us/library/dd728284.aspx). 
<span data-ttu-id="0b41f-182">Für BCS zum Empfangen von Benachrichtigungen, muss es einen Mechanismus für die Back-End-Datenquelle, die eine Anforderung an hinzugefügt und entfernt aus der Benachrichtigungsabonnements werden akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="0b41f-182">For BCS to receive notifications, there must be a mechanism on the back-end data source that will accept a request to be added and removed from notification subscriptions.</span></span> 
  
    
    
<span data-ttu-id="0b41f-183">Der letzte Schritt beim Erstellen des Diensts ist für die **Subscribe** und **Unsubscribe** Stereotype Vorgänge des Diensts hinzufügen, die im BDC-Modell definiert sind.</span><span class="sxs-lookup"><span data-stu-id="0b41f-183">The last step in creating the service is to add service operations for the **Subscribe** and **Unsubscribe** stereotypes that are defined in the BDC model.</span></span>
  
    
    

### <a name="to-add-service-operations-for-subscribe-and-unsubscribe-stereotypes"></a><span data-ttu-id="0b41f-184">Hinzufügen von Dienstvorgänge zum Abonnieren und Kündigen des Abonnements Stereotype</span><span class="sxs-lookup"><span data-stu-id="0b41f-184">To add service operations for Subscribe and Unsubscribe stereotypes</span></span>


- <span data-ttu-id="0b41f-185">Fügen Sie auf der Seite AdventureWorks.cs die folgende Zeichenfolge Variablendeklaration hinzu.</span><span class="sxs-lookup"><span data-stu-id="0b41f-185">In the AdventureWorks.cs page, add the following string variable declaration.</span></span>
    
```cs
  
public string subscriptionStorePath = @"\\\\[SHARE_NAME]\\SubscriptionStore\\SubscriptionStore.xml";
```


    > **Note:**
      > This file is an XML file that is updated with the new subscriptions. Access to this file will be made by the server process, so make sure you have granted sufficient rights for this file access. > You might also want to create a database solution for storing subscription information. 

    Then add the following two **WebGet** methods to handle the subscriptions.
    


```cs
  [WebGet]
        public string Subscribe(string deliveryUrl, string eventType)
        {
            string subscriptionId = Guid.NewGuid().ToString();
            
            XmlDocument subscriptionStore = new XmlDocument();
            
            subscriptionStore.Load(subscriptionStorePath);

            // Add a new subscription element.
            XmlNode newSubNode = subscriptionStore.CreateElement("Subscription");

            // Add subscription ID element to the subscription element.
            XmlNode subscriptionIdStart = subscriptionStore.CreateElement("SubscriptionID");
            subscriptionIdStart.InnerText = subscriptionId;
            newSubNode.AppendChild(subscriptionIdStart);

            // Add delivery URL element to the subscription element.
            XmlNode deliveryAddressStart = subscriptionStore.CreateElement("DeliveryAddress");
            deliveryAddressStart.InnerText = deliveryUrl;
            newSubNode.AppendChild(deliveryAddressStart);

            // Add event type element to the subscription element.
            XmlNode eventTypeStart = subscriptionStore.CreateElement("EventType");
            eventTypeStart.InnerText = eventType;
            newSubNode.AppendChild(eventTypeStart);

            // Add the subscription element to the root element. 
            subscriptionStore.AppendChild(newSubNode);

            
            subscriptionStore.Save(subscriptionStorePath);

            return subscriptionId;
        }

        [WebGet]
        public void Unsubscribe(string subscriptionId)
        {
            XmlDocument subscriptionStore = new XmlDocument();
            subscriptionStore.Load(subscriptionStorePath);

            XmlNodeList subscriptions = subscriptionStore.DocumentElement.ChildNodes;
            foreach (XmlNode subscription in subscriptions)
            {
                XmlNodeList subscriptionList = subscription.ChildNodes;
                if (subscriptionList.Item(0).InnerText == subscriptionId)
                {
                    subscriptionStore.DocumentElement.RemoveChild(subscription);
                    break;
                }
            }

            subscriptionStore.Save(subscriptionStorePath);
        }

```


## <a name="next-steps"></a><span data-ttu-id="0b41f-186">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="0b41f-186">Next steps</span></span>
<span data-ttu-id="0b41f-187"><a name="bkmk_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="0b41f-187"></span></span>

<span data-ttu-id="0b41f-188">Um SharePoint zu benachrichtigen, dass Änderungen vorgenommen wurden, müssen Sie auch einen Dienst zu erstellen, der die Datenquelle für Änderungen abgefragt und sendet dann Benachrichtigungen an alle Benachrichtigungen abonniert.</span><span class="sxs-lookup"><span data-stu-id="0b41f-188">To notify SharePoint that changes have been made, you also need to create a service that queries the data source for changes, and then sends notifications to all those subscribed to notifications.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="0b41f-189">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0b41f-189">Additional resources</span></span>
<span data-ttu-id="0b41f-190"><a name="bkmk_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0b41f-190"></span></span>


-  [<span data-ttu-id="0b41f-191">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-191">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0b41f-192">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-192">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0b41f-193">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-193">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0b41f-194">Externe Ereignisse und Warnungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-194">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0b41f-195">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-195">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0b41f-196">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="0b41f-196">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

