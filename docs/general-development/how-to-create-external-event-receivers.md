---
title: "Vorgehensweise Erstellen von externen Ereignisempfängern"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6d5f486-6247-47f9-9876-fab12f13342f
ms.openlocfilehash: 638e2df70d22bd82a1f6eb0ba710515392642702
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-external-event-receivers"></a><span data-ttu-id="41f78-102">Vorgehensweise: Erstellen von externen Ereignisempfängern</span><span class="sxs-lookup"><span data-stu-id="41f78-102">How to: Create external event receivers</span></span>
<span data-ttu-id="41f78-p101">Informationen Sie zu den Schritten zum Erstellen von externen-Ereignisempfänger für lokale Installationen von Business Connectivity Services (BCS) externer Listen. Externe Ereignisempfänger sind Klassen, mit die SharePoint-Add-Ins auf Ereignisse reagieren, die auf SharePoint-Elemente wie Listen oder Listenelemente auftreten können. Beispielsweise können Sie auf die listenereignisse, z. B. hinzufügen oder Entfernen eines Felds reagieren; Listen Sie Elementereignisse wie hinzufügen oder Entfernen eines Listenelements oder einer Anlage zu einem Listenelement auf. oder Webereignisse wie beispielsweise hinzufügen oder Löschen einer Website oder Websitesammlung. Sie können einer vorhandenen Visual Studio-Lösung einen remote-Ereignisempfänger hinzufügen, die ein SharePoint-Add-In enthält.</span><span class="sxs-lookup"><span data-stu-id="41f78-p101">Learn the steps for creating external event receivers for on-premises installations of Business Connectivity Services (BCS) external lists. External event receivers are classes that enable SharePoint Add-ins to respond to events that occur to SharePoint items, such as lists or list items. For example, you can respond to list events, such as adding or removing a field; list item events, such as adding or removing a list item or attachment to a list item; or web events, such as adding or deleting a site or site collection. You can add a remote event receiver to an existing Visual Studio solution that contains an SharePoint Add-in.</span></span>
  
    
    

<span data-ttu-id="41f78-p102">Zu diesem Artikel gehörende Codebeispiel  [SharePoint: erstellen ein remoteereignissempfängers für externe Daten](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c). Es veranschaulicht, wie alle Komponenten, die zum Konfigurieren und Verwenden von externen System ereignisbenachrichtigungen benötigt erstellen. In diesem Beispiel wird Folgendes:</span><span class="sxs-lookup"><span data-stu-id="41f78-p102">This article accompanies the code sample  [SharePoint: Create a remote event receiver for external data](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c). It shows how to create all the components needed to configure and use external system event notifications. In this example, you will do the following:</span></span>
  
    
    


1. <span data-ttu-id="41f78-110">Erstellen Sie ein externes System basierend auf der Northwind-Beispieldatenbank</span><span class="sxs-lookup"><span data-stu-id="41f78-110">Create an external system based on the Northwind sample database</span></span>
    
  
2. <span data-ttu-id="41f78-111">Verfügbar machen Sie, die über OData-Beispieldaten durch Erstellen eines Windows Communication Foundation (WCF)-Diensts.</span><span class="sxs-lookup"><span data-stu-id="41f78-111">Expose the sample data through OData by creating a Windows Communication Foundation (WCF) service.</span></span>
    
  
3. <span data-ttu-id="41f78-112">Erstellen Sie einen Abruf-Dienst, der überwacht die Änderungen in den Daten und SharePoint über diese Änderungen benachrichtigen.</span><span class="sxs-lookup"><span data-stu-id="41f78-112">Create a polling service that will monitor for changes in the data and notify SharePoint of those changes.</span></span>
    
  
4. <span data-ttu-id="41f78-113">Erstellen Sie einen externen Ereignisempfänger, der ausgeführt wird, wenn die externen Daten Elemente hinzugefügt werden und daher erstellt ein neues Listenelement in einer Benachrichtigungsliste.</span><span class="sxs-lookup"><span data-stu-id="41f78-113">Create an external event receiver that executes when items are added to the external data and, as a result, creates a new list item on a notifications list.</span></span>
    
  

## <a name="prerequisites-and-system-set-up"></a><span data-ttu-id="41f78-114">Erforderliche Komponenten und System einrichten</span><span class="sxs-lookup"><span data-stu-id="41f78-114">Prerequisites and system set up</span></span>
<span data-ttu-id="41f78-115"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-115"></span></span>

<span data-ttu-id="41f78-116">Um das Beispiel zu vervollständigen, benötigen Sie die folgenden erforderlichen Komponenten:</span><span class="sxs-lookup"><span data-stu-id="41f78-116">To complete this example, you will need the following prerequisites:</span></span>
  
    
    

- <span data-ttu-id="41f78-117">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="41f78-117">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="41f78-118">Office Developer Tools für Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="41f78-118">Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="41f78-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="41f78-119">SQL Server</span></span>
    
  
- <span data-ttu-id="41f78-120">SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-120">SharePoint</span></span>
    
  
- <span data-ttu-id="41f78-121">Internetinformationsdienste 7.0</span><span class="sxs-lookup"><span data-stu-id="41f78-121">Internet Information Services 7.0</span></span>
    
  
- <span data-ttu-id="41f78-122">Northwind-Beispieldatenbank</span><span class="sxs-lookup"><span data-stu-id="41f78-122">Northwind sample database</span></span>
    
  

## <a name="build-the-components-for-external-systems"></a><span data-ttu-id="41f78-123">Die Komponenten für externe Systeme erstellen</span><span class="sxs-lookup"><span data-stu-id="41f78-123">Build the components for external systems</span></span>
<span data-ttu-id="41f78-124"><a name="BuildingTheComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-124"></span></span>

<span data-ttu-id="41f78-p103">Der größte Teil der Konfiguration geschieht tatsächlich auf dem externen System. Damit externe Ereignisempfängern ordnungsgemäß funktioniert muss die folgenden Komponenten vorhanden ist und auf dem externen System:</span><span class="sxs-lookup"><span data-stu-id="41f78-p103">The biggest part of the configuration actually happens on the external system. For external event receivers to work correctly, the following components must be present and working on the external system:</span></span>
  
    
    

- <span data-ttu-id="41f78-127">**Abonnementspeicher:** Eine Tabelle mit Informationen zu den Abonnenten, die Änderungen an der externen Daten benachrichtigt werden möchten.</span><span class="sxs-lookup"><span data-stu-id="41f78-127">**Subscription store:** A table that contains information about the subscribers that want to be notified of changes to the external data.</span></span>
    
  
- <span data-ttu-id="41f78-p104">**Änderungen zu speichern:** Eine Tabelle, die zum Speichern der Änderungen an der Datenelemente verwendet wird. Es fungiert als temporärer Speicher, da der Dienst Abruf löscht das Element in der Tabelle aus, wenn an Abonnenten in SharePoint-Benachrichtigungen gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-p104">**Changes store:** A table that is used to store the changes to the data items. It functions as temporary storage only because the polling service deletes the item in the table when notifications are sent back to subscribers in SharePoint.</span></span>
    
  
- <span data-ttu-id="41f78-p105">**Abruf Service:** In diesem Szenario erforderlich, als Mittel zur Überprüfung, wenn Daten geändert und auf die Änderungstabelle übermittelt wurde. Der Dienst Abruf fragt die Änderungstabelle und baut ein Notification-Paket, das an den SharePoint-Empfängeradresse (REST-Endpunkt) gespeichert, in dem Abonnementspeicher gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-p105">**Polling service:** Required in this scenario as a means of checking when data has been changed and submitted to the change table. The polling service queries the change table and assembles a notification package that is sent to the SharePoint delivery address (REST endpoint) stored in the subscription store.</span></span>
    
  
- <span data-ttu-id="41f78-p106">**OData-WCF-Datendienste:** Um die Daten aus dem externen System-Datenbank verfügbar zu machen, müssen Sie einen WCF-Dienst zu erstellen. Dieser Dienst, ausgeführt auf Internet Information Services (IIS), bietet der Rest-Schnittstelle und OData-feed, der für dieses Szenario erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="41f78-p106">**OData WCF Data Service:** To expose the data from the external system's database, you have to create a WCF service. This service, running on Internet Information Services (IIS), provides the RESTful interface and OData feed that is needed for this scenario.</span></span>
    
  

## <a name="set-up-the-external-system"></a><span data-ttu-id="41f78-134">Richten Sie das externe system</span><span class="sxs-lookup"><span data-stu-id="41f78-134">Set up the external system</span></span>
<span data-ttu-id="41f78-135"><a name="bkmk_SetUpTheExternalSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-135"></span></span>

<span data-ttu-id="41f78-136">Die erste Aufgabe besteht darin, das externe System einrichten.</span><span class="sxs-lookup"><span data-stu-id="41f78-136">The first task is to set up the external system.</span></span>
  
    
    

### <a name="attach-the-northwind-sample-database"></a><span data-ttu-id="41f78-137">Fügen Sie die Nordwind-Datenbank</span><span class="sxs-lookup"><span data-stu-id="41f78-137">Attach the Northwind sample database</span></span>

<span data-ttu-id="41f78-p107">Der erste Teil der Vorbereitung des Back-End-Systems ist so eine ausgeführte Instanz von SQL Server die Nordwind-Datenbank hinzu. Wenn Sie bereits die Nordwind-Datenbank installiert haben, können Sie die Skripts ausführen, im folgenden Abschnitt, um die zusätzlichen Objekte benötigt für externe Ereignisdienst Benachrichtigungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="41f78-p107">The first part of preparing the back-end system is to add the Northwind sample database to a running instance of SQL Server. If you already have the Northwind sample database installed, you can run the scripts in the following section to create the additional objects needed for external eventing notifications to work.</span></span>
  
    
    
<span data-ttu-id="41f78-140">Jedoch, wenn Sie keine Northwind installiert haben, finden Sie unter  [Installieren der Northwind-Beispieldatenbank](http://msdn.microsoft.com/library/2f92cfc3-6310-4327-b2f2-8610f7385c86%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="41f78-140">However, if you don't have Northwind installed, see  [Installing the Northwind Sample Database](http://msdn.microsoft.com/library/2f92cfc3-6310-4327-b2f2-8610f7385c86%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="41f78-141">Die Datenbank ist auch in das Codebeispiel enthalten:  [SharePoint: erstellen ein remoteereignissempfängers für externe Daten](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span><span class="sxs-lookup"><span data-stu-id="41f78-141">The database is also included with the code sample:  [SharePoint: Create a remote event receiver for external data](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span></span>
  
    
    

### <a name="create-the-subscription-store"></a><span data-ttu-id="41f78-142">Erstellen von dem Abonnementspeicher</span><span class="sxs-lookup"><span data-stu-id="41f78-142">Create the subscription store</span></span>

<span data-ttu-id="41f78-143">Wenn die Nordwind-Datenbank installiert ist, öffnen Sie ein neues Abfragefenster, und führen Sie das folgende Skript aus.</span><span class="sxs-lookup"><span data-stu-id="41f78-143">When the Northwind database is installed, open a new query window and execute the following script.</span></span>
  
    
    

```

USE [Northwind]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EntitySubscribe](
    [SubscriptionId] [int] IDENTITY(1,1) NOT NULL,
    [EntityName] [nvarchar](250) NULL,
    [DeliveryURL] [nvarchar](250) NULL,
    [EventType] [int] NULL,
    [UserId] [nvarchar](50) NULL,
    [SubscribeTime] [timestamp] NULL,
    [SelectColumns] [nvarchar](10) NULL,
 CONSTRAINT [PK_Subscribe] PRIMARY KEY CLUSTERED 
(
    [SubscriptionId] ASC
)WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
```

<span data-ttu-id="41f78-p108">Dadurch wird eine Tabelle in der Nordwind-Datenbank mit dem Namen EntitySubscribe erstellt. Dies dient dem Abonnementspeicher weiter oben genannten.</span><span class="sxs-lookup"><span data-stu-id="41f78-p108">This creates a table in the Northwind database named EntitySubscribe. This serves as the subscription store referred to earlier.</span></span>
  
    
    

### <a name="create-the-change-store"></a><span data-ttu-id="41f78-146">Erstellen Sie den Speicher ändern</span><span class="sxs-lookup"><span data-stu-id="41f78-146">Create the change store</span></span>

<span data-ttu-id="41f78-147">Führen Sie das folgende Skript aus, um die Änderungstabelle erstellen, die Änderungen an den Daten in der Tabelle Customers aufgezeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-147">Run the following script to create the change table that will record changes to the data in the Customers table.</span></span>
  
    
    

```

USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[Customers_Updates](
    [CustomerID] [nchar](5) NOT NULL,
    [CompanyName] [nvarchar](40) NOT NULL,
    [ContactName] [nvarchar](30) NULL,
    [ContactTitle] [nvarchar](30) NULL,
    [Address] [nvarchar](60) NULL,
    [City] [nvarchar](15) NULL,
    [Region] [nvarchar](15) NULL,
    [PostalCode] [nvarchar](10) NULL,
    [Country] [nvarchar](15) NULL,
    [Phone] [nvarchar](24) NULL,
    [Fax] [nvarchar](24) NULL,
    [TimeAdded] [datetime] NULL,
    [EventType] [int] NULL,
 CONSTRAINT [PK_Customers_Updates] PRIMARY KEY CLUSTERED 
(
    [CustomerID] ASC
)WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
```

<span data-ttu-id="41f78-148">Dadurch wird eine Tabelle mit dem Namen Customers_Updates, die die Informationen zu den Datensatz speichert, das der Customers-Tabelle hinzugefügt wurde, hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="41f78-148">This adds a table named Customers_Updates that stores the information about the record that was added to the Customers table.</span></span>
  
    
    

### <a name="create-the-change-trigger"></a><span data-ttu-id="41f78-149">Erstellen Sie den Auslöser ändern</span><span class="sxs-lookup"><span data-stu-id="41f78-149">Create the change trigger</span></span>

<span data-ttu-id="41f78-p109">Der Änderung Trigger wird ausgelöst, wenn Änderungen auf die Tabelle Kunden erfolgen. Bei jedem Kunden ein Datensatz hinzugefügt wird, führt SQL Server den Auslöser, der einen neuen Datensatz in der Tabelle Customers_Updates mit Informationen zu den Datensatz einfügt.</span><span class="sxs-lookup"><span data-stu-id="41f78-p109">The change trigger is fired when changes happen to the Customers table. Whenever a record is added to Customers, SQL Server executes the trigger, which inserts a new record in the Customers_Updates table with the information about the record.</span></span>
  
    
    
<span data-ttu-id="41f78-152">Um den Trigger zu erstellen, führen Sie die folgende Abfrage aus.</span><span class="sxs-lookup"><span data-stu-id="41f78-152">To create the trigger, execute the following query.</span></span>
  
    
    



```

USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE trigger [dbo].[Customer_insupd] on [dbo].[Customers] for
INSERT
AS
DECLARE 
    @CustomerID nchar(5),
    @CompanyName nvarchar(40),
    @ContactName nvarchar(30) ,
    @ContactTitle nvarchar(30) ,
    @Address nvarchar(60) ,
    @City nvarchar(15) ,
    @Region nvarchar(15) ,
    @PostalCode nvarchar(10) ,
    @Country nvarchar(15) ,
    @Phone nvarchar(24) ,
    @Fax nvarchar(24), 
    @TimeAdded datetime,
    @EventType int
    
    Select @CustomerID = CustomerId, @CompanyName=CompanyName,
    @ContactName=ContactName, @ContactTitle=ContactTitle,
    @Address=Address, @City=City, @Region=Region,
    @PostalCode =PostalCode, @Country=Country,
    @Phone=Phone,@Fax=Fax,@EventType=1 
    from inserted
    
    insert into Customers_Updates 
    (CustomerId,CompanyName,
    ContactName, ContactTitle,
    Address, City, Region,
    PostalCode,Country,
    Phone,Fax,TimeAdded,EventType) values
    (@CustomerId,@CompanyName,
    @ContactName, @ContactTitle,
    @Address, @City, @Region,
    @PostalCode,@Country,
    @Phone,@Fax,SYSDATETIME(),@EventType)
    
GO

```


> <span data-ttu-id="41f78-153">**Hinweis:** Wenn Sie Ihre eigenen benutzerdefinierten gespeicherten Prozeduren gemäß Definition im BDC-Modell verwenden, sollten Sie auch löschen erstellen und Aktualisieren von Triggern.</span><span class="sxs-lookup"><span data-stu-id="41f78-153">**Note** If you are using your own custom stored procedures as defined in your BDC model, you might also want to create the delete and update triggers. The additional triggers are not be covered as part of this scenario.</span></span> <span data-ttu-id="41f78-154"> Zusätzliche Trigger werden nicht im Rahmen dieses Szenarios behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-154">The additional triggers are not be covered as part of this scenario.</span></span> 
  
    
    


### <a name="create-the-stored-procedures"></a><span data-ttu-id="41f78-155">Erstellen der gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="41f78-155">Create the stored procedures</span></span>

<span data-ttu-id="41f78-p111">Wenn Sie Zugriff auf die direkte Tabelle mit Business Connectivity Services dieser Verfahren nicht erforderlich verwenden. Wenn Sie Ihre eigenen Prozeduren und benutzerdefinierter Code für das externe System definieren, sollten Sie diese Option, um die Gewährung des Zugriffs auf die Tabelle von SQL Server hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="41f78-p111">If you are using direct table access with Business Connectivity Services, these procedures won't be necessary. However, if you are defining your own procedures and custom code on the external system, you might want to add these to allow access to the table from SQL Server.</span></span>
  
    
    

```

// DeleteEventRecords stored procedure
USE [Northwind]
GO
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE PROCEDURE [dbo].[proc_DeleteEventRecords]
    @CustomerID nchar(5), @EventType int
    AS
    Delete from Customers_Updates 
    WHERE  CustomerID like @CustomerID AND EventType=@EventType

GO

```

<span data-ttu-id="41f78-158">Die **SubscribeEntity** gespeicherte Prozedur erstellt einen Datensatz in dem Abonnementspeicher.</span><span class="sxs-lookup"><span data-stu-id="41f78-158">The **SubscribeEntity** stored procedure will create a record in the subscription store.</span></span>
  
    
    



```

// SubscribeEntity 
USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE PROCEDURE [dbo].[SubscribeEntity] 
    @EntityName Varchar(255),
    @EventType Integer,
    @DeliveryAddress Varchar(255),
    @SelectColumns Varchar(10)

AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;

    -- Insert statements for procedure here
    
    Insert into EntitySubscribe(EntityName,DeliveryURL,EventType,SelectColumns)
    values (@EntityName,@DeliveryAddress,@EventType,@SelectColumns)


END

GO

```


## <a name="create-the-odata-service"></a><span data-ttu-id="41f78-159">Erstellen des OData-Diensts</span><span class="sxs-lookup"><span data-stu-id="41f78-159">Create the OData Service</span></span>
<span data-ttu-id="41f78-160"><a name="bkmk_CreatingTheODataService"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-160"></span></span>

<span data-ttu-id="41f78-p112">OData-Feed wird innerhalb eines **WCF-Datendienste**gehostet. Dieser WCF-Dienst wird anschließend in einer Webanwendung von IIS gehostet.</span><span class="sxs-lookup"><span data-stu-id="41f78-p112">The OData feed is hosted inside a **WCF Data Service**. This WCF service is then hosted by IIS in a web application.</span></span>
  
    
    
<span data-ttu-id="41f78-163">Die folgenden Schritte erstellen Sie eine neue ASP.NET WCF-Datendienste.</span><span class="sxs-lookup"><span data-stu-id="41f78-163">The following steps create a new ASP.NET WCF data service.</span></span>
  
    
    

### <a name="to-create-the-wcf-data-service-application"></a><span data-ttu-id="41f78-164">So erstellen Sie die WCF Data Service-Anwendung</span><span class="sxs-lookup"><span data-stu-id="41f78-164">To create the WCF Data Service application</span></span>


1. <span data-ttu-id="41f78-165">Wählen Sie in Visual Studio 2012 klicken Sie im Menü **Datei** auf **neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="41f78-165">In Visual Studio 2012, on the **File** menu, choose **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="41f78-166">Klicken Sie im Dialogfeld **Neues Projekt** unter den Knoten Visual c# wählen Sie **die Vorlage**, und wählen Sie dann **ASP.NET-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="41f78-166">In the **New Project** dialog box, under the Visual C# node, choose the **Web** template, and then choose **ASP.NET Web Application**.</span></span>
    
  
3. <span data-ttu-id="41f78-167">Geben Sie den Namen des Projekts NorthwindService , und wählen Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f78-167">Enter NorthwindService as the name of the project, and then choose **OK**.</span></span>
    
  
<span data-ttu-id="41f78-168">Im nächsten Schritt mit dem Visual Studio-Assistenten, Sie verwenden, um ein ADO.NET Entitätsdatenmodell erstellen und ermitteln das Schema der Datenquelle.</span><span class="sxs-lookup"><span data-stu-id="41f78-168">Next, using the Visual Studio wizard, you discover the schema of the data source and use it to create an ADO.NET entity data model.</span></span>
  
    
    

### <a name="to-define-the-data-model"></a><span data-ttu-id="41f78-169">So definieren Sie das Datenmodell</span><span class="sxs-lookup"><span data-stu-id="41f78-169">To define the data model</span></span>


1. <span data-ttu-id="41f78-170">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt ASP.NET, und wählen Sie **Neues Element hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="41f78-170">In **Solution Explorer**, open the shortcut menu for the ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="41f78-171">Klicken Sie im Dialogfeld **Neues Element hinzufügen** auswählen **der Datenvorlage**, und wählen Sie dann **ADO.NET Entitätsdatenmodell**.</span><span class="sxs-lookup"><span data-stu-id="41f78-171">In the **Add New Item** dialog box, choose the **Data** template, and then choose **ADO.NET Entity Data Model**.</span></span>
    
  
3. <span data-ttu-id="41f78-172">Geben Sie den Namen des Datenmodells zu Northwind.edmx.</span><span class="sxs-lookup"><span data-stu-id="41f78-172">For the name of the data model, enter Northwind.edmx.</span></span>
    
  
4. <span data-ttu-id="41f78-173">Wählen Sie im Entity Data Model-Assistenten **aus Datenbank generieren**, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="41f78-173">In the Entity Data Model Wizard, choose **Generate from Database**, and then choose **Next**.</span></span>
    
  
5. <span data-ttu-id="41f78-174">Verbinden Sie das Datenmodell mit der Datenbank, führen Sie einen der folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="41f78-174">Connect the data model to the database by doing one of the following steps:</span></span>
    
1. <span data-ttu-id="41f78-p113">Wenn Sie keine datenbankverbindung bereits konfiguriert haben, wählen Sie **Neue Verbindung** aus, und erstellen Sie eine neue Verbindung. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen von Verbindungen mit SQL Server-Datenbanken](http://msdn.microsoft.com/library/360c340d-e5a6-4a7e-a569-e95d500be43d%28Office.15%29.aspx). Diese Instanz von SQL Server benötigen die Nordwind-Datenbank zugeordnet ist. Wählen Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="41f78-p113">If you do not have a database connection already configured, choose **New Connection** and create a new connection. For more information, see [How to: Create Connections to SQL Server Databases](http://msdn.microsoft.com/library/360c340d-e5a6-4a7e-a569-e95d500be43d%28Office.15%29.aspx). This SQL Server instance must have the Northwind sample database attached. Choose **Next**.</span></span>
    
    <span data-ttu-id="41f78-179">- oder -</span><span class="sxs-lookup"><span data-stu-id="41f78-179">-or-</span></span>
    
  
2. <span data-ttu-id="41f78-180">Wenn Sie eine Verbindung zum Verbinden mit der Nordwind-Datenbank bereits konfiguriert haben, wählen Sie diese Verbindung aus der Liste der Verbindungen, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="41f78-180">If you have a database connection already configured to connect to the Northwind database, choose that connection from the list of connections, and then choose **Next**.</span></span>
    
  
6. <span data-ttu-id="41f78-181">Wählen Sie auf der letzten Seite des Assistenten die Kontrollkästchen für alle Tabellen in der Datenbank, und deaktivieren Sie die Kontrollkästchen für die Ansichten und gespeicherte Prozeduren.</span><span class="sxs-lookup"><span data-stu-id="41f78-181">On the final page of the wizard, select the check boxes for all tables in the database, and clear the check boxes for views and stored procedures.</span></span>
    
  
7. <span data-ttu-id="41f78-182">Wählen Sie die Schaltfläche **Fertig stellen** aus, um den Assistenten zu schließen.</span><span class="sxs-lookup"><span data-stu-id="41f78-182">Choose the **Finish** button to close the wizard.</span></span>
    
  
<span data-ttu-id="41f78-183">Im nächsten Schritt erstellen Sie den eigentlichen Dienst, der von IIS gehostet wird, der die Mittel Zugriff auf externe Daten über Representational State Transfer (REST) bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="41f78-183">In the next step, you create the actual service that is hosted by IIS that will provide the means to access external data through Representational State Transfer (REST).</span></span>
  
    
    

### <a name="to-create-the-wcf-data-service"></a><span data-ttu-id="41f78-184">Zum Erstellen der WCF-Dienst</span><span class="sxs-lookup"><span data-stu-id="41f78-184">To create the WCF Data Service</span></span>


1. <span data-ttu-id="41f78-185">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für Ihr Projekt ASP.NET, und wählen Sie **Neues Element hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="41f78-185">In **Solution Explorer**, open the shortcut menu for your ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="41f78-186">Wählen Sie im Dialogfeld **Neues Element hinzufügen** **WCF Data Service**.</span><span class="sxs-lookup"><span data-stu-id="41f78-186">In the **Add New Item** dialog box, choose **WCF Data Service**.</span></span>
    
  
3. <span data-ttu-id="41f78-187">Geben Sie für den Namen des Diensts Northwind.</span><span class="sxs-lookup"><span data-stu-id="41f78-187">For the name of the service, enter Northwind.</span></span>
    
  
4. <span data-ttu-id="41f78-p114">Ersetzen Sie in den Code für die Data-Dienst, in der Definition der Klasse, die den Datendienst definiert den Kommentar  `/* TODO: put your data source class name here */` mit dem Typ, der Entitätscontainer des Datenmodells, die in diesem Fall `NorthwindEntities`ist. Die Definition der Klasse sollte wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="41f78-p114">In the code for the data service, in the definition of the class that defines the data service, replace the comment  `/* TODO: put your data source class name here */` with the type that is the entity container of the data model, which in this case is `NorthwindEntities`. The class definition should look like the following.</span></span>
    
```cs
  
public class Northwind : DataService<NorthwindEntities>

```


### <a name="to-set-the-security-on-the-service"></a><span data-ttu-id="41f78-190">Die Sicherheit für den Dienst festlegen</span><span class="sxs-lookup"><span data-stu-id="41f78-190">To set the security on the service</span></span>


- <span data-ttu-id="41f78-p115">Sie haben jetzt die Sicherheit, um die Gewährung des Zugriffs auf die Daten aus der OData-feed von externen Empfängern zu ändern. Wenn ein WCF-Dienst erstellt wird, wird standardmäßig alle Zugriff verweigert. Stellen Sie die folgenden Änderungen auf die soeben erstellte Klasse.</span><span class="sxs-lookup"><span data-stu-id="41f78-p115">You now have to modify the security to allow access to the data from the OData feed by external consumers. When a WCF service is created, all access is denied by default. Make the following changes to the class you just created.</span></span>
    
```cs
  
config.SetEntitySetAccessRule("*", EntitySetRights.All);
config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


### <a name="create-the-subscribe-service-operation-optional"></a><span data-ttu-id="41f78-194">Erstellen Sie den Vorgang Subscribe (optional)</span><span class="sxs-lookup"><span data-stu-id="41f78-194">Create the Subscribe service operation (optional)</span></span>

<span data-ttu-id="41f78-p116">WCF-Dienst kann auch eine Möglichkeit zum Behandeln der abonnieren und kündigen Anforderungen von SharePoint codiert werden. Benutzerdefinierte gespeicherte Prozeduren für die Anwendung erstellt werden soll wird jeweils durch ein Vorgang behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-p116">The WCF service can also be coded with a means to handle the Subscribe and Unsubscribe requests from SharePoint. If you choose to create custom stored procedures for your application these will each be handled by a service operation.</span></span>
  
    
    
 <span data-ttu-id="41f78-p117">**Abonnieren**: Abonnieren den Vorgang nimmt die Anforderung vom SharePoint gesendet und der Empfängeradresse den Ereignistyp und die Entität abgerufen. Es muss außerdem ein **subscriptionId** generieren und zeichnen Sie dann alle diese in der Tabelle der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="41f78-p117">**Subscribe**: The Subscribe operation takes the request sent by SharePoint and retrieves the delivery address the event type and the entity. It also has to generate a **subscriptionId** and then record all of these into the database table.</span></span>
  
    
    



```cs

/// The Subscribe service operation maps directly to the Subscribe stereotype
/// found in the BDC model

[WebGet]
public string Subscribe(string deliveryUrl, string eventType)
{
   // Generate a new Guid that will function as the subscriptionId.
            string subscriptionId = new Guid().ToString();

            // This sproc will be used to create the subscription in the database.
            string subscribeSproc = "SubscribeEntity";

            // Create connection to database.
            using (SqlConnection conn = new SqlConnection(sqlConn))
            {
                SqlCommand cmd = new SqlCommand(subscribeSproc, conn);
                cmd.Parameters.Add(new SqlParameter("SubscriptionId", subscriptionId));
                cmd.Parameters.Add(new SqlParameter("EntityName", entityName));
                cmd.Parameters.Add(new SqlParameter("EventType", eventType));
                cmd.Parameters.Add(new SqlParameter("DeliveryAddress", deliveryUrl));
                cmd.Parameters.Add(new SqlParameter("SelectColumns", selectColumns));

                try
                {
                    conn.Open();
                    cmd.ExecuteNonQuery();
                }
                catch (Exception e)
                {
                    throw e;
                }
                finally
                {
                    conn.Close();
                }

                return subscriptionId;
            }
```


> <span data-ttu-id="41f78-199">**Hinweis:** Wenn SQL Server für die Windows-Authentifizierung eingerichtet ist, versucht das Programm, die Anforderung mit der App-Pool-Identität zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="41f78-199">**Note** If SQL Server is set up for Windows authentication, it will try to authenticate the request with the App Pool identity. Make sure that the account configured in the App Pool has rights to read and write in the database.</span></span> <span data-ttu-id="41f78-200">Stellen Sie sicher, dass das im App-Pool konfigurierte Konto über Berechtigungen zum Lesen und Schreiben in der Datenbank verfügt.</span><span class="sxs-lookup"><span data-stu-id="41f78-200">Note If SQL Server is set up for Windows authentication, it will try to authenticate the request with the App Pool identity. Make sure that the account configured in the App Pool has rights to read and write in the database.</span></span> 
  
    
    


## <a name="create-the-polling-service"></a><span data-ttu-id="41f78-201">Erstellen des Umfragedienstes</span><span class="sxs-lookup"><span data-stu-id="41f78-201">Create the polling service</span></span>
<span data-ttu-id="41f78-202"><a name="bkmk_CreateThePollingService"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-202"></span></span>

<span data-ttu-id="41f78-203">Der Abruf-Dienst ist ein Windowsdienst, der für die Abfrage der Änderungstabelle und erstellen und Senden von Benachrichtigungen zu SharePoint oder SharePoint Online an der angegebenen zustellungs-Adresse zuständig ist.</span><span class="sxs-lookup"><span data-stu-id="41f78-203">The polling service is a Windows service that is responsible for querying the change table and creating and sending notifications to SharePoint or SharePoint Online at the specific delivery address.</span></span>
  
    
    
<span data-ttu-id="41f78-p119">Im nächsten Schritt erstellen Sie ein neues Windows-Dienst-Projekt, das registriert wird, auf dem Hostcomputer WCF. Nachdem das Projekt registriert ist, können Sie in der Microsoft Management Console (MMC) den ausgeführten Dienst anzeigen.</span><span class="sxs-lookup"><span data-stu-id="41f78-p119">Next, you create a new Windows Service project that will be registered on the WCF host machine. Once the project is registered, you can view the running service in the Microsoft Management Console (MMC).</span></span>
  
    
    

### <a name="to-create-a-new-project"></a><span data-ttu-id="41f78-206">So erstellen Sie ein neues Projekt</span><span class="sxs-lookup"><span data-stu-id="41f78-206">To create a new project</span></span>


1. <span data-ttu-id="41f78-207">Öffnen Sie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="41f78-207">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="41f78-208">Erstellen eines neuen Projekts mithilfe der Windows-Dienst-Vorlage, nennen Sie das Projekt PollingService, und wählen Sie die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f78-208">Create a new project using the Windows Service template, name the project PollingService, and choose the **OK** button.</span></span>
    
  
3. <span data-ttu-id="41f78-209">Wenn das Projekt erstellt wird, öffnen Sie die PollingService.cs-Datei in der Codeansicht.</span><span class="sxs-lookup"><span data-stu-id="41f78-209">When the project is created, open the PollingService.cs file in code view.</span></span>
    
  
4. <span data-ttu-id="41f78-210">Fügen Sie den folgenden Code in der neu erstellten-Klasse.</span><span class="sxs-lookup"><span data-stu-id="41f78-210">Add the following code in the newly created class.</span></span>
    
```cs
  
public partial class PollingService : ServiceBase
{
   string subscriptionStorePath = string.Empty;

   public PollingService()
   {
      InitializeComponent();
   }

   protected override void OnStart(string[] args)
   {

      // This is the timer which fires every minute.           
      System.Timers.Timer aTimer = new System.Timers.Timer();
      aTimer.Elapsed += new System.Timers.ElapsedEventHandler(SendEventNotification);
      aTimer.Interval = 60000;
      aTimer.Enabled = true;
   }
   protected override void OnStop()
   {}

   private void SendEventNotification(object sender, EventArgs e)
   {
      try
      {
         List<ItemChange> events = itemChangeLookUp();             
         triggerEventPerSubscription(events);
      }
      catch (Exception ex)
      {
         EventLog.Log = "Application";
         EventLog.Source = ServiceName;
         EventLog.WriteEntry("PollingService" + ex.Message, EventLogEntryType.Error);
      }
   }

   private void triggerEventPerSubscription(List<ItemChange> events)
   {           
      foreach (ItemChange itemChangeEvent in events)
      {                        
         SendNotification(itemChangeEvent, itemChangeEvent.DeliveryAddress);
         string message = string.Format("PollingService.TriggerEventPerSubscription: Notification sent for item {0} of eventType 
                          {1}", itemChangeEvent.CustomerId, itemChangeEvent.EventType);
         EventLog.Log = "Application";
         EventLog.Source = ServiceName;
         EventLog.WriteEntry(message);                   
      }
   }

   private List<ItemChange> itemChangeLookUp()
   {
      EventLog.Log = "Application";
      EventLog.Source = ServiceName;
      EventLog.WriteEntry("Polling for Item Change");
      List<ItemChange> itemChangeList = new List<ItemChange>();          
      string connectionString = "Data Source=.;Initial Catalog=Northwind;Integrated Security=true";

      // Provide the query string with a parameter placeholder.
      string queryString = "Proc_RetrieveEventRecords";

      // Specify the parameter value.
      int paramValue = -50;

      using (SqlConnection connection = new SqlConnection(connectionString))
      {
         SqlCommand command = new SqlCommand(queryString, connection);
         command.CommandType = CommandType.StoredProcedure;
         command.Parameters.AddWithValue("@TimeSince", paramValue);
         try
         {
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();
            while (reader.Read())
            {
               ItemChange item = new ItemChange(reader["CustomerID"].ToString(), Int32.Parse(reader["EventType"].ToString()), 
               reader[14].ToString(), reader["DeliveryUrl"].ToString(), reader["CompanyName"].ToString(), 
               reader["ContactName"].ToString(),reader["ContactTitle"].ToString(), reader["Address"].ToString(), 
               reader["City"].ToString(), reader["Region"].ToString(), reader["Country"].ToString(), reader["PostalCode"].ToString(), 
               reader["Phone"].ToString(), reader["Fax"].ToString());
               itemChangeList.Add(item);
            }
            reader.Close();
         }
         catch (Exception ex)
         {
            EventLog.Log = "Application";
            EventLog.Source = ServiceName;
            EventLog.WriteEntry("PollingService : ItemChangeLookup " + ex.Message, EventLogEntryType.Error);
         }
      } 
      string message = string.Format("{0} items changes", itemChangeList.Count);
      EventLog.Log = "Application";
      EventLog.Source = ServiceName;
      EventLog.WriteEntry(message);

      return itemChangeList;
   }

```

<span data-ttu-id="41f78-211">Im nächste Schritt wird eine ausführbare Datei erstellen, die die ausgeführten Dienste auf dem Computer OData hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="41f78-211">The next step is to build an executable file that can be added to the running services on the OData computer.</span></span>
  
    
    

### <a name="to-compile-and-deploy-the-polling-service"></a><span data-ttu-id="41f78-212">So kompilieren und stellen Sie den Dienst abrufen</span><span class="sxs-lookup"><span data-stu-id="41f78-212">To compile and deploy the polling service</span></span>


1. <span data-ttu-id="41f78-213">Drücken Sie F5, um das Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="41f78-213">Press F5 to build your project.</span></span>
    
  
2. <span data-ttu-id="41f78-214">Öffnen Sie die **Befehlszeile für VS2012**.</span><span class="sxs-lookup"><span data-stu-id="41f78-214">Open the **Command Prompt for VS2012**.</span></span>
    
  
3. <span data-ttu-id="41f78-215">Navigieren Sie dazu aufgefordert werden zu dem Speicherort der Project-Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="41f78-215">At the prompt, navigate to your project output location.</span></span>
    
  
4. <span data-ttu-id="41f78-216">Suchen Sie in das Verzeichnis Bin die PollingService.exe-Datei aus.</span><span class="sxs-lookup"><span data-stu-id="41f78-216">In the Bin directory, find the PollingService.exe file.</span></span>
    
  
5. <span data-ttu-id="41f78-217">Geben Sie Installutil PollingService.exe , und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="41f78-217">Enter installutil PollingService.exe and press Enter.</span></span>
    
  
6. <span data-ttu-id="41f78-218">Stellen Sie sicher, dass der Dienst ausgeführt durch Ausführung der Dienste-MMC.</span><span class="sxs-lookup"><span data-stu-id="41f78-218">Verify that the service is running by running the Services MMC.</span></span>
    
  

## <a name="required-sharepoint-components"></a><span data-ttu-id="41f78-219">Erforderliche Komponenten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-219">Required SharePoint components</span></span>
<span data-ttu-id="41f78-220"><a name="bkmk_SharePointComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-220"></span></span>

<span data-ttu-id="41f78-221">Um das gesamte System abgeschlossen haben, müssen die folgenden Komponenten auf dem Server, auf dem SharePoint ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-221">To complete the whole system, the following components are required on the server that is running SharePoint.</span></span>
  
    
    

- <span data-ttu-id="41f78-p120">**Externer Inhaltstyp:** Der externe Inhaltstyp ist im Wesentlichen eine XML-Definition der externen Datenquelle. Für dieses Szenario verwenden Sie die neue automatische Generierung von Tools in Visual Studio 2012 zum Ermitteln der Datenquelle und den externen Inhaltstyp automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="41f78-p120">**External content type:** The external content type is basically an XML definition of the external data source. For this scenario, you will use the new autogeneration tools in Visual Studio 2012 to discover the data source and create the external content type automatically.</span></span>
    
  
- <span data-ttu-id="41f78-p121">**Externe Ereignisempfänger:** Der Remote- oder externen Ereignisempfänger ist die Sache, die Aktionen auf externe datenänderungen in SharePoint ermöglicht. Sie können Ereignisempfänger für externe Listen und für Entitäten erstellen.</span><span class="sxs-lookup"><span data-stu-id="41f78-p121">**External event receiver:** The remote or external event receiver is the thing that makes actions on external data changes possible in SharePoint. You can create event receivers for external lists and for entities.</span></span>
    
    <span data-ttu-id="41f78-p122">Ein Ereignisempfänger, der für eine externe Liste erstellt wird, ähnelt anderen-Ereignisempfänger für SharePoint-Listen. Erstellen Sie den Code, und fügen sie Sie der Liste. Wenn eine Aktion für die Daten ausgeführt wird, die durch die Liste dargestellt wird, führt der Ereignisempfänger aus.</span><span class="sxs-lookup"><span data-stu-id="41f78-p122">An event receiver that is created for an external list is similar to other event receivers for SharePoint lists. You create the code and attach it to the list. When an action is performed on the data that is represented by the list, the event receiver executes.</span></span>
    
    <span data-ttu-id="41f78-p123">Ein Ereignisempfänger für Entitäten wird genau wie ein List-basierten Ereignisempfänger ausgeführt, jedoch nicht muss, um zu einer Liste angefügt werden soll. Er erhält Benachrichtigungen auf die gleiche Weise wie, aber sie benötigt nicht die Schnittstelle, die im Beispiel listenbasierten zugeordnet ist. Dies ist, Sie können die Benachrichtigungen programmgesteuert intercept und Erstellen von Code, um eine bestimmte Aktion ausgeführt. In diesem Szenario wird die Aktion zum Erstellen eines neuen Datensatzes in der Benachrichtigungsliste</span><span class="sxs-lookup"><span data-stu-id="41f78-p123">An event receiver for entities is executed just like a list-based event receiver, except it doesn't need to be attached to a list. It receives notifications the same way, but it doesn't need the interface that is associated with the list-based example. The benefit of this is that you can intercept the notifications programmatically and create code to perform some action. In this scenario, that action is to create a new record in the notifications list</span></span> 
    
  
- <span data-ttu-id="41f78-p124">**Benachrichtigungsliste:** Benachrichtigungsliste ist eine einfache SharePoint-Liste, die zum Aufzeichnen von Benachrichtigungen empfangen aus dem externen System verwendet wird. Für jeden neuen Datensatz, das externe System hinzugefügt wurde wird ein Datensatz in der Benachrichtigungsliste erstellt.</span><span class="sxs-lookup"><span data-stu-id="41f78-p124">**Notifications list:** The notifications list is a simple SharePoint list that is used to record notifications received from the external system. For each new record added to the external system, a record is created in the notifications list.</span></span>
    
  

## <a name="set-up-the-sharepoint-components"></a><span data-ttu-id="41f78-235">Richten Sie die SharePoint-Komponenten</span><span class="sxs-lookup"><span data-stu-id="41f78-235">Set up the SharePoint components</span></span>
<span data-ttu-id="41f78-236"><a name="bkmk_SettingUpTheSharePointComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-236"></span></span>

<span data-ttu-id="41f78-p125">Nun, da Sie das externe System eingerichtet haben, ist es Zeit zum Wechsel auf die andere Hälfte der Formel erstellen. Erstellen Sie nun die Komponenten, die in SharePoint gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-p125">Now that you have the external system set up, it's time to move on to creating the other half of the equation. You will now create the components to be hosted on SharePoint.</span></span>
  
    
    

### <a name="to-create-a-new-visual-studio-2012-project"></a><span data-ttu-id="41f78-239">Erstellen Sie ein neues Projekt von Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="41f78-239">To create a new Visual Studio 2012 project</span></span>


1. <span data-ttu-id="41f78-240">Wählen Sie im Visual Studio 2012 **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="41f78-240">In Visual Studio 2012, choose **New Project**.</span></span>
    
  
2. <span data-ttu-id="41f78-241">Wählen Sie die SharePoint-app-Projektvorlage.</span><span class="sxs-lookup"><span data-stu-id="41f78-241">Choose the SharePoint app project template.</span></span>
    
  
<span data-ttu-id="41f78-242">Office Developer Tools für Visual Studio 2013 hinzugefügt, ein automatische Generierung von-Assistent, der als entdecken Schema der Datenquelle und klicken Sie dann aus, die einen externen Inhaltstyp erstellen.</span><span class="sxs-lookup"><span data-stu-id="41f78-242">Office Developer Tools for Visual Studio 2013 added an autogeneration wizard that will discover a data source's schema and then create an external content type from that.</span></span>
  
    
    

### <a name="to-add-a-new-external-content-type"></a><span data-ttu-id="41f78-243">So fügen Sie einen neuen externen Inhaltstyp hinzu</span><span class="sxs-lookup"><span data-stu-id="41f78-243">To add a new external content type</span></span>


- <span data-ttu-id="41f78-244">Klicken Sie im **Projektmappen-Explorer** öffnen Sie das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für eine externe Datenquelle**.</span><span class="sxs-lookup"><span data-stu-id="41f78-244">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content Types for an External Data Source**.</span></span>
    
    <span data-ttu-id="41f78-245">Dies startet den **Assistenten zum Anpassen von SharePoint**, die automatisch erstellen des externen Inhaltstyps verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-245">This starts the **SharePoint Customization Wizard**, which is used to build the external content type automatically.</span></span>
    
    <span data-ttu-id="41f78-246">Weitere Informationen zum Erstellen externer Inhaltstypen finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="41f78-246">For more information about how to create external content types, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
    
  
<span data-ttu-id="41f78-p126">Ändern Sie jetzt den XML-Code, der im vorherigen Schritt zum Hinzufügen von Methoden zum Abonnieren generiert wurde. Dadurch wird BCS mit dem externen System kommunizieren, wenn jemand abonniert externe datenänderungen informiert werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-p126">You will now modify the XML that was generated in the previous step to add a method for Subscribe. This will allow BCS to communicate with the external system when someone subscribes to be notified about external data changes.</span></span>
  
    
    

### <a name="to-add-the-subscribe-method-to-the-external-content-type-xml"></a><span data-ttu-id="41f78-249">So fügen Sie die Subscribe-Methode für den externen Inhaltstyp XML hinzu</span><span class="sxs-lookup"><span data-stu-id="41f78-249">To add the Subscribe method to the external content type XML</span></span>


1. <span data-ttu-id="41f78-250">Suchen Sie im **Projektmappen-Explorer** den neuen Knoten mit dem Namen **External Content Types**.</span><span class="sxs-lookup"><span data-stu-id="41f78-250">In **Solution Explorer**, find the new node named **External Content Types**.</span></span>
    
  
2. <span data-ttu-id="41f78-251">Suchen Sie die Datei **Customers.ect**, und öffnen Sie es mit einem XML-Editor.</span><span class="sxs-lookup"><span data-stu-id="41f78-251">Find the **Customers.ect** file, and open it with an XML editor.</span></span>
    
  
3. <span data-ttu-id="41f78-252">Führen Sie einen Bildlauf nach unten zum unteren Rand der Seite, und fügen Sie die folgende Methode in den Abschnitt  `<Methods>` .</span><span class="sxs-lookup"><span data-stu-id="41f78-252">Scroll down to the bottom of the page, and paste the following method into the  `<Methods>` section.</span></span>
    
```XML
  
<Method Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe" IsStatic="true">
              <Properties>
                <Property Name="ODataEntityUrl" Type="System.String">/EntitySubscribes</Property>
                <Property Name="ODataHttpMethod" Type="System.String">POST</Property>
                <Property Name="ODataPayloadKind" Type="System.String">Entry</Property>
                <Property Name="ODataFormat" Type="System.String">application/atom+xml</Property>
                <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
              </Properties>
              <AccessControlList>
                <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                  <Right BdcRight="Edit" />
                  <Right BdcRight="Execute" />
                  <Right BdcRight="SetPermissions" />
                  <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
              </AccessControlList>
              <Parameters>
                <Parameter Direction="In" Name="@DeliveryURL">
                  <TypeDescriptor TypeName="System.String" Name="DeliveryURL" >
                    <Properties>
                      <Property Name="IsDeliveryAddress" Type="System.Boolean">true</Property>
                    </Properties>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@EventType">
                  <TypeDescriptor TypeName="System.Int32" Name="EventType" >
                    <Properties>
                      <Property Name="IsEventType" Type="System.Boolean">true</Property>
                    </Properties>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@EntityName">
                  <TypeDescriptor TypeName="System.String" Name="EntityName" >
                    <DefaultValues>
                      <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">Customers</DefaultValue>
                    </DefaultValues>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@SelectColumns">
                  <TypeDescriptor TypeName="System.String" Name="SelectColumns" >
                    <DefaultValues>
                      <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">*</DefaultValue>
                    </DefaultValues>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="Return" Name="SubscribeReturn">
                  <TypeDescriptor Name="SubscribeReturnRootTd" TypeName="Microsoft.BusinessData.Runtime.DynamicType">
                    <TypeDescriptors>
                      <TypeDescriptor Name="SubscriptionId" TypeName="System.String" >
                        <Properties>
                          <Property Name="SubscriptionIdName" Type="System.String">Default</Property>
                        </Properties>
                        <Interpretation>
                          <ConvertType LOBType="System.Int32" BDCType="System.String"/>
                        </Interpretation>
                      </TypeDescriptor>
                      <TypeDescriptor Name="DeliveryURL" TypeName="System.String" />
                      <TypeDescriptor Name="SelectColumns" TypeName="System.String" >
                      </TypeDescriptor>
                      <TypeDescriptor Name="EntityName" TypeName="System.String" />
                      <TypeDescriptor Name="EventType" TypeName="System.Int32" />
                      <TypeDescriptor Name="UserId" TypeName="System.String" />
                      <!--TypeDescriptor Name="SubscribeTime" TypeName="System." /-->
                    </TypeDescriptors>
                  </TypeDescriptor>
                </Parameter>
              </Parameters>
              <MethodInstances>
                <MethodInstance Type="EventSubscriber" ReturnParameterName="SubscribeReturn" ReturnTypeDescriptorPath="SubscribeReturnRootTd" Default="true" Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe">
                  <AccessControlList>
                    <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                      <Right BdcRight="Edit" />
                      <Right BdcRight="Execute" />
                      <Right BdcRight="SetPermissions" />
                      <Right BdcRight="SelectableInClients" />
                    </AccessControlEntry>
                  </AccessControlList>
                </MethodInstance>
              </MethodInstances>
            </Method>
```

<span data-ttu-id="41f78-253">Fügen Sie jetzt Clientcode, um der Liste, um ereignisbenachrichtigungen abonnieren zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="41f78-253">You will now add client code to allow your list to subscribe to event notifications.</span></span>
  
    
    

### <a name="to-add-code-to-the-appjs-file-to-initiate-the-subscription"></a><span data-ttu-id="41f78-254">Die Datei App.js, das Abonnement zu initiieren Code hinzu</span><span class="sxs-lookup"><span data-stu-id="41f78-254">To add code to the App.js file to initiate the subscription</span></span>


- <span data-ttu-id="41f78-p127">Öffnen Sie in den Ordner Skripts Ihres Projekts SharePoint-Add-In die Datei **App.js** aus. Fügen Sie die folgende Methode in die Datei.</span><span class="sxs-lookup"><span data-stu-id="41f78-p127">In the Scripts folder of your SharePoint Add-in project, open the **App.js** file. Paste the following method into the file.</span></span>
    
```
  
function SubscribeEntity()
{
    var notificationCallback = new SP.BusinessData.Runtime.NotificationCallback(context, "http://[MACHINE NAME]:8585");
    var url = myweb.get_url();
    notificationCallback.set_notificationContext(url);
    context.load(notificationCallback);
    var subscription = entity.subscribe(1, notificationCallback, "", "SubscribeCustomer", lobSystemInstance);
    context.load(subscription);
    context.executeQueryAsync(OnSubscribeSuccess, failmethod);
}
```

<span data-ttu-id="41f78-257">Um den Ereignisempfänger mit diesem Skript zu registrieren, müssen Sie eine Schaltfläche auf der Seite "Default.aspx" in Ihrem Projekt erstellen, und rufen Sie die **SubscribeEntity()** die **onclick()** -Methode.</span><span class="sxs-lookup"><span data-stu-id="41f78-257">To register the event receiver with this script, you have to create a button on the Default.aspx page in your project and call the **SubscribeEntity()** from the **onclick()** method.</span></span>
  
    
    

- <span data-ttu-id="41f78-258">Öffnen Sie die Seite "default.aspx", und fügen Sie den folgenden HTML-Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="41f78-258">Open the Default.aspx page, and add the following HTML.</span></span>
    
```HTML
  
<input type="button" value="Subscribe" onclick="SubscribeEntity();"/>
```

<span data-ttu-id="41f78-p128">Für Ereignisdienst funktioniert müssen Sie auch die SharePoint-Liste externe Ereignisse akzeptieren aktivieren. Dies erfolgt durch Aktivieren des Features für externe Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="41f78-p128">For eventing to work, you must also enable the SharePoint list to accept external events. This is done by turning on the External Events feature.</span></span>
  
    
    
<span data-ttu-id="41f78-261">Es folgt ein Skript, das das Feature mithilfe der Clientcode aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-261">The following is a script that will turn on the feature using client code.</span></span>
  
    
    



```cs
function EnableEventing_Clicked()
{
    var clientContext = SP.ClientContext.get_current();
    var web = clientContext.get_web();
    var features = web.get_features();

    clientContext.load(features);

    // The GUID provided here is the feature that allows external events and alerts.
    var eventingFeatureId = new SP.Guid('5B10D113-2D0D-43BD-A2FD-F8BC879F5ABD');

    var eventingFeature = features.add(eventingFeatureId, true, SP.FeatureDefinitionScope.farm);

    clientContext.load(eventingFeature);
    var onEventingFeatureActivated = function () {
        alert("eventing feature activated");
    };
    clientContext.executeQueryAsync(Function.createDelegate(this,
    onEventingFeatureActivated));
}
```

<span data-ttu-id="41f78-262">Genau wie mit **Subscribe**, fügen Sie eine Schaltfläche auf der Seite hinzu, die das Feature aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-262">Just like with **Subscribe**, you will add a button to the page that will turn on the feature.</span></span>
  
    
    
<span data-ttu-id="41f78-263">Fügen Sie den folgenden HTML-Code auf der Seite Default.aspx direkt unterhalb der Schaltfläche " **Anmelden** ".</span><span class="sxs-lookup"><span data-stu-id="41f78-263">Add the following HTML to the Default.aspx page, right below the **Subscribe** button.</span></span>
  
    
    



```HTML

<input type="button" value="EnableEventing" onclick="EnableEventing_Clicked();"" />
```

<span data-ttu-id="41f78-264">Für dieses Szenario müssen Sie als Nächstes eine Benachrichtigungsliste hinzufügen, die die Senden von Benachrichtigungen vom externen System angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="41f78-264">Next, for this scenario you must add a notifications list that will show the notifications sent by the external system.</span></span>
  
    
    

### <a name="to-add-the-notifications-list"></a><span data-ttu-id="41f78-265">So fügen Sie der Benachrichtigungsliste hinzu</span><span class="sxs-lookup"><span data-stu-id="41f78-265">To add the notifications list</span></span>


1. <span data-ttu-id="41f78-266">Klicken Sie im **Projektmappen-Explorer** öffnen Sie das Kontextmenü für den Projektnamen, und wählen Sie **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="41f78-266">In **Solution Explorer**, open the shortcut menu for the project name, and choose **Add**.</span></span>
    
  
2. <span data-ttu-id="41f78-267">Wählen Sie die Vorlage **Liste** aus, und nennen Sie die ListeNotificationList.</span><span class="sxs-lookup"><span data-stu-id="41f78-267">Choose the **List** template, and name the listNotificationList.</span></span>
    
  
<span data-ttu-id="41f78-p129">Um einen Ereignisempfänger imitieren, der mit SharePoint im globalen Assemblycache registriert ist, enthält das Beispiel eine Konsolenanwendung, die überwacht werden, damit die Änderungen gestartet wird. Wenn sie eine Benachrichtigung erhält, werden die **NotificationList**ein Listenelements hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="41f78-p129">To mimic an event receiver that is registered with SharePoint in the global assembly cache, the sample provides a console application that will start listening for changes. When it receives a notification, it adds a list item to the **NotificationList**.</span></span>
  
    
    

### <a name="to-start-the-command-line-event-receiver"></a><span data-ttu-id="41f78-270">Starten Sie den Command-Line-Ereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="41f78-270">To start the command-line event receiver</span></span>


1. <span data-ttu-id="41f78-271">Öffnen Sie die **RemoteEventReceiverConsoleApp**.</span><span class="sxs-lookup"><span data-stu-id="41f78-271">Open the **RemoteEventReceiverConsoleApp**.</span></span>
    
  
2. <span data-ttu-id="41f78-272">Öffnen Sie die Datei **Program.cs**, und ändern Sie den Namen von Ihrem lokalen Computer (oder dem Computer, auf dem der Ereignisempfänger ausgeführt wird).</span><span class="sxs-lookup"><span data-stu-id="41f78-272">Open the **Program.cs** file, and change the name of your local computer (or the computer where the event receiver will be running).</span></span>
    
  
3. <span data-ttu-id="41f78-273">Klicken Sie auf die Schaltfläche **Start** in Visual Studio die Konsolenanwendung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="41f78-273">Click the **Start** button in Visual Studio to run the console application.</span></span>
    
    <span data-ttu-id="41f78-p130">Ein Befehlsfenster wird geöffnet, die angibt, dass die Anwendung ordnungsgemäß kompiliert wurde, und es für Benachrichtigungen aus dem externen System ändern hört. Lassen Sie dieses Fenster geöffnet, während des Tests.</span><span class="sxs-lookup"><span data-stu-id="41f78-p130">A command window opens, which indicates that the application has compiled correctly, and it is listening for change notifications from the external system. Leave this window open during this test.</span></span>
    
  

### <a name="to-deploy-the-app-to-sharepoint"></a><span data-ttu-id="41f78-276">Zum Bereitstellen der app für SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-276">To deploy the app to SharePoint</span></span>


- <span data-ttu-id="41f78-277">Drücken Sie F5 mit Visual Studio zum Erstellen und Bereitstellen der app öffnen.</span><span class="sxs-lookup"><span data-stu-id="41f78-277">Press F5 with Visual Studio open to build and deploy the app.</span></span>
    
  

## <a name="test-the-app"></a><span data-ttu-id="41f78-278">Testen der App</span><span class="sxs-lookup"><span data-stu-id="41f78-278">Test the app</span></span>
<span data-ttu-id="41f78-279"><a name="bkmk_testApp"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-279"></span></span>

<span data-ttu-id="41f78-280">Nun können Sie die app in Aktion angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="41f78-280">Now you can see the app in action.</span></span>
  
    
    

1. <span data-ttu-id="41f78-281">Durchsuchen Sie, um die app aus, um die verschiedenen Listen anzuzeigen, die Daten im externen System darstellen.</span><span class="sxs-lookup"><span data-stu-id="41f78-281">Browse around the app to see the different lists that represent the data in the external system.</span></span>
    
  
2. <span data-ttu-id="41f78-282">Klicken Sie auf die Liste der **Kunden**.</span><span class="sxs-lookup"><span data-stu-id="41f78-282">Click the **Customers** list.</span></span>
    
  
3. <span data-ttu-id="41f78-283">Hinzufügen eines neuen Kundens.</span><span class="sxs-lookup"><span data-stu-id="41f78-283">Add a new customer.</span></span>
    
  
4. <span data-ttu-id="41f78-284">Zeigen Sie das neue Listenelement, den, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="41f78-284">View the new list item you just created.</span></span>
    
  
5. <span data-ttu-id="41f78-285">Wechseln Sie zu der Benachrichtigungsliste zu sehen, dass das externe System SharePoint von einer Änderung der Customers-Tabelle benachrichtigt hat.</span><span class="sxs-lookup"><span data-stu-id="41f78-285">Go to the notifications list to see that the external system has notified SharePoint of a change to the Customers table.</span></span>
    
    <span data-ttu-id="41f78-p131">Behalten Sie im Hinterkopf, die der Timer zum Senden von Benachrichtigungen einer Minute festgelegt ist. Beim Testen, müssen Sie möglicherweise für eine kurze Zeit, bevor Sie die Benachrichtigungen gebucht finden Sie unter warten.</span><span class="sxs-lookup"><span data-stu-id="41f78-p131">Keep in mind that the timer is set to send notifications every one minute. While testing, you might have to wait for a short period before you see the notifications posted.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="41f78-288">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="41f78-288">Additional resources</span></span>
<span data-ttu-id="41f78-289"><a name="bkmk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="41f78-289"></span></span>


-  [<span data-ttu-id="41f78-290">Externe Ereignisse und Warnungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-290">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="41f78-291">Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-291">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="41f78-292">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-292">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="41f78-293">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-293">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="41f78-294">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-294">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="41f78-295">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="41f78-295">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

