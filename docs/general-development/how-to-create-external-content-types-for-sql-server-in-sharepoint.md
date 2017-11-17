---
title: "Vorgehensweise Erstellen externer Inhaltstypen für SQL Server in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7fe2fbf0-546b-4a16-b02e-a0960bfb3842
ms.openlocfilehash: c8640567852751db426ebad7e6e2cfd0e3b93231
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-external-content-types-for-sql-server-in-sharepoint"></a><span data-ttu-id="b38c7-102">Vorgehensweise: Erstellen externer Inhaltstypen für SQL Server in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b38c7-102">How to: Create external content types for SQL Server in SharePoint</span></span>
<span data-ttu-id="b38c7-p101">Erfahren Sie, wie Sie in SharePoint für SQL Server einen externen Inhaltstyp erstellen. Das Erstellen eines externen Inhaltstyps ist eine wichtige Aufgabe, wenn Sie mit externen Daten arbeiten. Ein externer Inhaltstyp enthält wichtige Informationen zu Verbindungen, Zugriff, Betriebsarten, Spalten, Filtern und anderen Metadaten, die zum Abrufen von Daten aus der externen Datenquelle dienen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p101">Learn how to create an external content type for SQL Server in SharePoint. Creating an external content type is a pivotal task when you are working with external data. An external content type contains important information about connections, access, methods of operation, columns, filters, and other metadata that is used to retrieve the data from the external data source.</span></span>
  
    
    


## <a name="before-you-begin"></a><span data-ttu-id="b38c7-106">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="b38c7-106">Before you begin</span></span>
<span data-ttu-id="b38c7-107"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-107"></span></span>

<span data-ttu-id="b38c7-p102">Das Arbeiten mit externen Daten erfordert einige vorbereitende Aufgaben zum Ermöglichen des sicheren Zugriffs auf die Daten. Die folgenden Informationen können Ihnen bei der Planung der nächsten Schritte helfen. Wenn Sie darüber hinaus Probleme bei der Arbeit mit externen Daten haben sollten, können Sie anhand dieser Informationen das Problem ausmachen. Für den Zugriff auf externe Daten müssen Sie oder ein Administrator folgendermaßen vorgehen:</span><span class="sxs-lookup"><span data-stu-id="b38c7-p102">Working with external data requires several prerequisite tasks to enable secure access to the data. The following information can help you plan your next steps. Also, if you have problems trying to work with external data, this information can help you identify the issue. To access external data, you or an administrator must do the following:</span></span>
  
    
    
 <span data-ttu-id="b38c7-112">**Vorbereiten von SQL Server** Ein Datenbankadministrator muss Berechtigungen vergeben, um sicherzustellen, dass die richtigen Personen auf die Daten zugreifen können und die Daten nicht in falsche Hände geraten.</span><span class="sxs-lookup"><span data-stu-id="b38c7-112">**Prepare SQL Server** A database administrator needs to provide permissions to make sure that that the right people have access to the data and that the data does not end up in the wrong hands.</span></span> <span data-ttu-id="b38c7-113">Der Datenbankadministrator muss auch ein SQL Server-Konto mit db_owner-Berechtigung erstellen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-113">The database administrator must also create a SQL Server account that has db_owner permission.</span></span> <span data-ttu-id="b38c7-114">Der Datenbankadministrator kann zudem spezielle Tabellen, Ansichten, Abfragen, Spalten-Aliase usw. erstellen, um die Ergebnisse auf die benötigten Elemente zu beschränken und die Leistung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="b38c7-114">The sqlservnv2 database administrator might want to create specific tables, views, indexes, and optimized queries to limit the results to just what is needed and to help improve performance.</span></span>
  
    
    
 <span data-ttu-id="b38c7-115">**Konfigurieren von SharePoint-Services** Ein Administrator muss Business Connectivity Services (BCS) und den Secure Store Service aktivieren.</span><span class="sxs-lookup"><span data-stu-id="b38c7-115">**Configure SharePoint services** An administrator must activate Business Connectivity Services (BCS) and the Secure Store Service.</span></span>
  
    
    
 <span data-ttu-id="b38c7-116">**Konfigurieren des einmaligen Anmeldens** Ein Administrator muss den geeignetsten Zugriffsmodus für die externe Datenquelle bestimmen, eine Zielanwendung erstellen und die Anmeldeinformationen für die Zielanwendung festlegen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-116">**Configure the Secure Store service** An administrator must determine the best access mode for the external data source, create a target application, and set the credentials for the target application.</span></span>
  
    
    
 <span data-ttu-id="b38c7-117">**Konfigurieren von Business Data Connectivity Services** Ein Administrator muss sicherstellen, dass der Benutzer, der den externen Inhaltstyp erstellt, über Berechtigungen für den Business Data Connectivity-Metadatenspeicher (BDC) verfügt und dass entsprechende Benutzer Zugriff auf den externen Inhaltstyp haben, auf dem die externe Liste basiert.</span><span class="sxs-lookup"><span data-stu-id="b38c7-117">**Configure Business Data Connectivity Services** An administrator must make sure that the user who creates the external content type has permission to the Business Data Connectivity (BDC) metadata store and that appropriate users have access to the external content type on which the external list is based.</span></span>
  
    
    
 <span data-ttu-id="b38c7-p104">**Sicherstellen, dass Office 2013 einsatzbereit ist** Zum Synchronisieren externer Daten mit Office 2013-Produkten müssen Sie Windows 7 oder eine höhere Version verwenden und sicherstellen, dass die Office-Installationsoption für Business Connectivity Services (BCS) aktiviert ist (Standardeinstellung). Über diese Option wird die Business Connectivity Services-Clientlaufzeit installiert, die externe Daten zwischenspeichert und synchronisiert, Geschäftsdaten externen Inhaltstypen zuweist, das Auswahltool für externe Elemente in Office-Produkten anzeigt und benutzerdefinierte Lösungen in Office-Produkten ausführt. Sie müssen außerdem auf allen Clientcomputern SQL Server Compact 4.0, .NET Framework 4 und WCF Data Services 5.0 für OData, Version 3, installieren. (Bei Bedarf werden Sie automatisch zum Herunterladen der Software aufgefordert).</span><span class="sxs-lookup"><span data-stu-id="b38c7-p104">**Be sure Office 2013 is ready to use** To synchronize external data with Office 2013 products, you must use Windows 7 or a later version, and make sure that the Office installation option for Business Connectivity Services (BCS) is enabled (this is the default). This option installs the Business Connectivity Services Client Runtime which does the following: caches and synchronizes with external data, maps business data to external content types, displays the external item picker in Office products, and runs custom solutions inside Office products. You must also have SQL Server Compact 4.0, .NET Framework 4, and WCF Data Services 5.0 for OData V3 on each client computer (If necessary, you are automatically prompted to download the software).</span></span>
  
    
    

## <a name="define-general-information"></a><span data-ttu-id="b38c7-121">Definieren allgemeiner Informationen</span><span class="sxs-lookup"><span data-stu-id="b38c7-121">Define general information</span></span>
<span data-ttu-id="b38c7-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-122"></span></span>


1. <span data-ttu-id="b38c7-123">Starten Sie Microsoft SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="b38c7-123">Start Microsoft SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="b38c7-124">Klicken Sie auf **Website öffnen**, und geben Sie dann den entsprechenden Websitenamen ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-124">Click **Open Site**, and then enter the appropriate site name.</span></span>
    
  
3. <span data-ttu-id="b38c7-125">Wählen Sie im **Navigationsbereich** unter **Websiteobjekte** die Option **Externe Inhaltstypen**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-125">In the **Navigation** pane, under **Site Objects**, select **External Content Types**.</span></span>
    
    > <span data-ttu-id="b38c7-126">**Hinweis:** SharePoint Designer 2013 gruppiert externe Inhaltstypen nach dem Namespace im ersten Fenster des Designers für externe Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-126">**Note** SharePoint Designer 2013 groups external content types by the namespace in the initial window of the External Content Type Designer.</span></span> 
4. <span data-ttu-id="b38c7-127">Klicken Sie zum Öffnen des Designers für externe Inhaltstypen im Menüband auf **Externer Inhaltstyp**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-127">To open the External Content Type Designer, on the ribbon, click **External Content Type**.</span></span>
    
  
5. <span data-ttu-id="b38c7-128">Führen Sie auf der Seite **Neuer externer Inhaltstyp** die folgenden Aktionen durch:</span><span class="sxs-lookup"><span data-stu-id="b38c7-128">On the **New External Content Type** page, do the following:</span></span>
    
  - <span data-ttu-id="b38c7-129">Klicken Sie neben **Name** auf **Neuer externer Inhaltstyp**, und geben Sie einen eindeutigen Namen für den externen Inhaltstyp ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-129">Next to **Name**, click **New external content type**, and then enter a unique name for the external content type.</span></span>
    
  
  - <span data-ttu-id="b38c7-130">Geben Sie neben **Anzeigename** einen anderen Namen ein, wenn Sie einen etwas aussagekräftigeren Anzeigenamen wünschen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-130">Next to **Display Name**, enter a different name if you want a more descriptive display name.</span></span>
    
  

## <a name="define-general-and-office-behaviors"></a><span data-ttu-id="b38c7-131">Definieren des allgemeinen Verhaltens und des Office-Verhaltens</span><span class="sxs-lookup"><span data-stu-id="b38c7-131">Define general and Office behaviors</span></span>
<span data-ttu-id="b38c7-132"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-132"></span></span>


1. <span data-ttu-id="b38c7-133">Wählen Sie in der Dropdownliste **Office-Elementtyp** einen der folgenden aus:</span><span class="sxs-lookup"><span data-stu-id="b38c7-133">In the **Office Item Type** drop-down list, select one of the following:</span></span>
    
  - <span data-ttu-id="b38c7-134">**Allgemeine Liste** Diese Option eignet sich für jede Art von Liste.</span><span class="sxs-lookup"><span data-stu-id="b38c7-134">**Generic List** Select this option for any type of list.</span></span>
    
  
  - <span data-ttu-id="b38c7-p105">**Termin, Kontakt, Aufgabe oder Beitrag** Wählen Sie diese Option aus, wenn Sie eine Liste erstellen, die sich wie ein Outlook-Kontakt-, -Aufgaben-, -Termin- oder Beitragselement verhält. Der Office-Elementtyp, den Sie hier auswählen, bestimmt das gewünschte Outlook-Verhalten des externen Inhaltstyps. Ein externer Inhaltstyp wie beispielsweise "Kunde" verhält sich wie ein Kontaktelement in Outlook selbst.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p105">**Appointment, Contact, Task, or Post** Select this option if you are creating a list that behaves like an Outlook Contact, Task, Appointment, or Post item. The Office item type that you select here determines the Outlook behavior that you want to attach to the external content type. For example, a Customer external content type behaves as a native Contact Item in Outlook.</span></span>
    
  
2. <span data-ttu-id="b38c7-138">Stellen Sie sicher, dass für das Kontrollkästchen **Offlinesynchronisierung für externe Liste** die Option **Aktiviert** (Standardeinstellung) ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b38c7-138">In the **Offline Sync for External List** check box, make sure **Enabled** is selected, which is the default.</span></span>
    
    > <span data-ttu-id="b38c7-139">**Hinweis:** Wenn Sie diese Option deaktivieren, ist der Befehl **SharePoint mit Outlook verbinden** für eine externe Liste nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b38c7-139">**Note** If you disable this option, then the **SharePoint Connect to Outlook** command is not available for an external list.</span></span>

> <span data-ttu-id="b38c7-140">**Hinweis:** Das Farm- und Website-Feature **Offline-Synchronisierung für externe Listen** muss ebenfalls aktiv sein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-140">**Note** The Farm and Site feature, **Offline Synchronization for External Lists**, must also be active. This feature is active by default at the Farm level, but not active by default at the site level.</span></span> <span data-ttu-id="b38c7-141">Dieses Feature ist standardmäßig auf der Farmebene, aber nicht standardmäßig auf der Websiteebene aktiv.</span><span class="sxs-lookup"><span data-stu-id="b38c7-141">The Farm and Site feature, Offline Synchronization for External Lists, must also be active. This feature is active by default at the Farm level, but not active by default at the site level.</span></span> 
  
    
    


## <a name="create-a-connection-to-the-external-data"></a><span data-ttu-id="b38c7-142">Erstellen einer Verbindung mit den externen Daten</span><span class="sxs-lookup"><span data-stu-id="b38c7-142">Create a connection to the external data</span></span>
<span data-ttu-id="b38c7-143"><a name="section4"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-143"></span></span>


1. <span data-ttu-id="b38c7-144">Zum Angeben der SQL Server-Datenbank für den externen Inhaltstyp klicken Sie auf **Klicken Sie hier, um externe Datenquellen zur ermitteln und Vorgänge zu definieren**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-144">To specify the SQL Server database for the external content type, click **Click here to discover external data sources and define operations**.</span></span>
    
  
2. <span data-ttu-id="b38c7-145">Klicken Sie auf **Verbindung hinzufügen**, wählen Sie im Dialogfeld **Auswahl des externen Datenquellentyps** die Option **SQL Server** aus, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-145">Click **Add Connection**, select **SQL Server** in **the External Data Source Type Selection** dialog box, and then click **OK**.</span></span>
    
  
3. <span data-ttu-id="b38c7-146">Geben Sie im Dialogfeld **SQL Server-Verbindung** den Namen des Servers, den Datenbanknamen und eine optionale Beschreibung ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-146">In the **SQL Server Connection** dialog box, enter the name of the server, the database name, an optional description, and then click **OK**.</span></span>
    
  
4. <span data-ttu-id="b38c7-147">Wählen Sie zum Auswählen eines Authentifizierungsmodus eine der folgenden Optionen aus:</span><span class="sxs-lookup"><span data-stu-id="b38c7-147">To choose an authentication mode, select one of the following:</span></span>
    
  - <span data-ttu-id="b38c7-148">**Verbindung mit der Identität des Benutzers herstellen** Bei dieser Option wird der Pass-Through-Authentifizierungsmodus verwendet.</span><span class="sxs-lookup"><span data-stu-id="b38c7-148">**Connect with User's Identity** Uses the Pass-through authentication mode.</span></span>
    
  
  - <span data-ttu-id="b38c7-149">**Verbindung mit angenommener Windows-Identität herstellen** Bei dieser Option wird der Authentifizierungsmodus "WindowsCredentials" verwendet.</span><span class="sxs-lookup"><span data-stu-id="b38c7-149">**Connect with Impersonated Windows Identity** Uses the WindowsCredentials authentication mode.</span></span>
    
  
  - <span data-ttu-id="b38c7-150">**Verbindung mit angenommener benutzerdefinierter Identität herstellen** Bei dieser Option wird der Authentifizierungsmodus "RDBCredentials" verwendet.</span><span class="sxs-lookup"><span data-stu-id="b38c7-150">**Connect with Impersonated Custom Identity** Uses the RDBCredentials authentication mode.</span></span>
    
  
5. <span data-ttu-id="b38c7-151">Geben Sie in das Feld **ID der Anwendung für einmaliges Anmelden** die in Einmaliges Anmelden erstellte Zielanwendungs-ID ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-151">In the **Secure Store Application ID** box, enter the target application ID name created in the Secure Store Service.</span></span>
    
  
6. <span data-ttu-id="b38c7-152">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-152">Click **OK**.</span></span>
    
  
<span data-ttu-id="b38c7-p107">SharePoint Designer 2013 überprüft und testet die Verbindungsinformationen. Wenn Meldungen angezeigt werden, müssen Sie die gemeldeten Probleme beheben, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p107">SharePoint Designer 2013 validates and tests the connection information. If you see messages, you must resolve them before you continue.</span></span>
  
    
    

## <a name="select-a-table-view-or-routine"></a><span data-ttu-id="b38c7-155">Auswählen einer Tabelle, Ansicht oder Routine</span><span class="sxs-lookup"><span data-stu-id="b38c7-155">Select a table, view, or routine</span></span>
<span data-ttu-id="b38c7-156"><a name="section5"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-156"></span></span>


1. <span data-ttu-id="b38c7-157">Erweitern Sie im Datenquellen-Explorer die Datenbank, um die darin enthaltenen Tabellen, Ansichten und Routinen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-157">In the Data Source Explorer, expand the database to view the tables, views, and routines that it contains.</span></span>
    
  
2. <span data-ttu-id="b38c7-158">Wählen Sie eine Tabelle, Ansicht oder Routine aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-158">Select a table, view, or routine.</span></span>
    
  

## <a name="define-operations"></a><span data-ttu-id="b38c7-159">Definieren von Vorgängen</span><span class="sxs-lookup"><span data-stu-id="b38c7-159">Define operations</span></span>
<span data-ttu-id="b38c7-160"><a name="section6"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-160"></span></span>


1. <span data-ttu-id="b38c7-161">Klicken Sie im Datenquellen-Explorer mit der rechten Maustaste auf die Tabelle, Ansicht oder Routine, und wählen Sie dann eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="b38c7-161">In the Data Source Explorer, right-click the table, view, or routine, and then select one of the following:</span></span>
    
  - <span data-ttu-id="b38c7-162">**Alle Vorgänge erstellen** Dient zum Definieren der Vorgänge "Element erstellen", "Element löschen", "Element lesen", "Liste lesen" und "Element aktualisieren".</span><span class="sxs-lookup"><span data-stu-id="b38c7-162">**Create All Operations** Defines a create item, delete item, read item, read list, and update item operation.</span></span>
    
    > <span data-ttu-id="b38c7-163">**Hinweis:**
      > **Alle Vorgänge erstellen** ist nur für Tabellen und Ansichten verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b38c7-163">Create All Operations is available only for tables and views. Routines require specific operations.</span></span> <span data-ttu-id="b38c7-164">Routinen benötigen spezifische Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="b38c7-164">Routines require specific operations.</span></span>
  - <span data-ttu-id="b38c7-165">**Neuer Elementlesevorgang** Dient zum Definieren eines Elementlesevorgangs.</span><span class="sxs-lookup"><span data-stu-id="b38c7-165">**New Read Item Operation** Defines a read item operation.</span></span>
    
  
  - <span data-ttu-id="b38c7-166">**Neuer Listenlesevorgang** Dient zum Definieren eines Listenlesevorgangs.</span><span class="sxs-lookup"><span data-stu-id="b38c7-166">**New Read List Operation** Defines a read list operation.</span></span>
    
  
  - <span data-ttu-id="b38c7-167">**Neuer Aktualisierungsvorgang** Dient zum Definieren eines Aktualisierungsvorgangs.</span><span class="sxs-lookup"><span data-stu-id="b38c7-167">**New Update Operation** Defines an update item operation.</span></span>
    
  
  - <span data-ttu-id="b38c7-168">**Neuer Löschvorgang** Dient zum Definieren eines Löschvorgangs.</span><span class="sxs-lookup"><span data-stu-id="b38c7-168">**New Delete Read** Defines a delete item operation.</span></span>
    
  
  - <span data-ttu-id="b38c7-169">**Aktualisieren** Dient zum Aktualisieren der Liste der Tabellen, Ansichten und Routinen im Datenquellen-Explorer.</span><span class="sxs-lookup"><span data-stu-id="b38c7-169">**Refresh** Refreshes the list of tables, views, and routines in the Data Source Explorer.</span></span>
    
  
2. <span data-ttu-id="b38c7-170">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-170">Click **Next**.</span></span>
    
  
 <span data-ttu-id="b38c7-171">**Hinweise**</span><span class="sxs-lookup"><span data-stu-id="b38c7-171">**Notes**</span></span>
  
    
    

- <span data-ttu-id="b38c7-p109">Stellen Sie bei Ansichten, die mehrere Tabellen umfassen, sicher, dass Schreibvorgänge unterstützt werden. Andernfalls sind die Befehle **Alle Vorgänge erstellen** oder **Neuer Aktualisierungsvorgang** nicht erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p109">On views that span multiple tables, make sure that that write operations are supported. Otherwise, **Create All Operations** or **New Update Operation** might fail.</span></span>
    
  
- <span data-ttu-id="b38c7-174">Definieren Sie stets mindestens einen **Neuen Elementlesevorgang** und **Neuen Listenlesevorgang**, da SharePoint-Features wie externe Listen von diesen Vorgängen abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="b38c7-174">Always define at least a **New Read Item Operation** and **New Read List Operation** because SharePoint features, such as external lists, rely on these operations.</span></span>
    
  
- <span data-ttu-id="b38c7-175">Entscheiden Sie sich für spezifische Vorgänge anstatt für **Alle Vorgänge erstellen**, wenn die Tabelle oder Ansicht bestimmte Vorgänge nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-175">Choose specific operations, instead of **Create All Operations**, when the table or view does not support certain operations.</span></span>
    
  

## <a name="add-columns"></a><span data-ttu-id="b38c7-176">Hinzufügen von Spalten</span><span class="sxs-lookup"><span data-stu-id="b38c7-176">Add columns</span></span>
<span data-ttu-id="b38c7-177"><a name="section7"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-177"></span></span>


1. <span data-ttu-id="b38c7-178">Um die Spalten der Tabelle oder Ansicht anzugeben, die Sie anzeigen möchten, klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-178">To specify the columns that you want to display from the table or view, click **Next**.</span></span>
    
  
2. <span data-ttu-id="b38c7-p110">Im Dialogfeld **Parameterkonfiguration** sind standardmäßig alle Spalten (als **Datenquellenelemente** bezeichnet) ausgewählt. Zum Entfernen nicht benötigter Spalten deaktivieren Sie die entsprechenden Kontrollkästchen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p110">In the **Parameters Configuration** dialog box, by default all columns (known as **Data Source Elements**) are selected. To remove unnecessary columns, clear the corresponding check boxes.</span></span>
    
    > <span data-ttu-id="b38c7-181">**Hinweis:** Anders als bei einer systemeigenen SharePoint-Liste können Sie den Namen der Spalte einer externen Liste nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="b38c7-181">**Note** Unlike a native SharePoint list, you cannot change the column name of an external list. Consider using an SQL column alias to provide a more meaningful name or a shorter name.</span></span> <span data-ttu-id="b38c7-182">Erwägen Sie die Verwendung eines SQL-Spalten-Alias, um einen aussagekräftigeren oder kürzeren Namen anzugeben.</span><span class="sxs-lookup"><span data-stu-id="b38c7-182">Unlike a native SharePoint list, you cannot change the column name of an external list. Consider using an SQL column alias to provide a more meaningful name or a shorter name.</span></span> 
3. <span data-ttu-id="b38c7-183">Um ein ID-Feld auszuwählen, klicken Sie auf ein Feld und markieren Sie es (in der Regel ein Feld mit einem eindeutigen Werten). Klicken Sie dann unter **Eigenschaften** auf **Zu ID zuordnen**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-183">To select an identifier field, click and highlight a field (typically a unique-valued field), and then under **Properties**, click **Map to Identifier**.</span></span>
    
  

> <span data-ttu-id="b38c7-184">**Wichtig:** Um zu verhindern, dass bestimmte Felder aktualisiert werden, z. B. eine ID oder ein Primärschlüsselfeld, deaktivieren Sie das Kontrollkästchen **Erforderlich**. Aktivieren Sie hingegen das Kontrollkästchen **Schreibgeschützt**, was zum Abrufen von Elementen nötig ist, damit Sie andere Felder aktualisieren können.</span><span class="sxs-lookup"><span data-stu-id="b38c7-184">**Important** To prevent specific fields from being updated, such as an ID or primary key field, clear the **Required** check box, but select the **Read-Only** check box, which is needed to retrieve items so you can update other fields.</span></span>
  
    
    

  
    
    


> <span data-ttu-id="b38c7-185">**Tipp:** Lesen Sie sich die Meldungen im Bereich **Fehler und Warnungen** immer sorgfältig durch.</span><span class="sxs-lookup"><span data-stu-id="b38c7-185">**Tip:** Always carefully read the messages in the **Errors and Warnings** pane.</span></span> <span data-ttu-id="b38c7-186">Sie enthalten nützliche Informationen zur Bestätigung Ihrer Aktionen oder zur Behandlung von Problemen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-186">They provide useful information to confirm your actions or troubleshoot any issues.</span></span> <span data-ttu-id="b38c7-187">Klicken Sie regelmäßig in den Bereich **Fehler und Warnungen**, und stellen Sie sicher, dass keine weiteren Fehler oder Warnungen vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="b38c7-187">Always carefully read the messages in the **Errors and Warnings** pane. They provide useful information to confirm your actions or troubleshoot any issues. Periodically click the Errors and Warnings pane and make sure that there are no more errors or warnings.</span></span>
  
    
    


## <a name="map-outlook-fields"></a><span data-ttu-id="b38c7-188">Outlook-Felder zuordnen</span><span class="sxs-lookup"><span data-stu-id="b38c7-188">Map Outlook fields</span></span>
<span data-ttu-id="b38c7-189"><a name="section8"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-189"></span></span>

<span data-ttu-id="b38c7-p113">Falls Ihr externer Inhaltstyp einem Outlook-Elementtyp zugeordnet ist, müssen Sie die Felder Ihres externen Inhaltstyps Outlook-Elementfeldern zuordnen. Wenn Sie einen externen Inhaltstyp, wie z. B. "Kunde", einem Outlook-Elementtyp wie "Kontakt" zuordnen, müssen Sie die einzelnen Felder im externen Inhaltstyp, wie z. B. "Vorname des Kunden", "Nachname des Kunden", "Kundenadresse" und "Telefonnummer des Kunden" explizit den entsprechenden Outlook-Feldern des Kontakts zuordnen, z. B. "Vorname", "Nachname", "Geschäftsadresse" und "Telefon geschäftlich" zuordnen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p113">If your external content type maps to an Outlook item type, you must map one or more fields from your external content type to the Outlook item fields. When you map an external content type, such as a Customer, to an Outlook item type, such as a Contact, you must explicitly map the individual fields in the external content type, such as Customer First Name, Customer Last Name, Customer Address, and Customer Phone, to their respective Outlook item type fields, such as a contact's FirstName, LastName, BusinessAddress, and BusinessPhone.</span></span>
  
    
    

- <span data-ttu-id="b38c7-192">Gehen Sie bei jedem Feld wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="b38c7-192">For the each field, do the following:</span></span>
    
1. <span data-ttu-id="b38c7-193">Klicken Sie auf ein Feld, um es zu markieren.</span><span class="sxs-lookup"><span data-stu-id="b38c7-193">Click and highlight the field.</span></span>
    
  
2. <span data-ttu-id="b38c7-p114">Klicken Sie unter **Eigenschaften** neben **Office-Eigenschaft** auf den Abwärtspfeil, und wählen Sie dann das entsprechende übereinstimmende Feld.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p114">Under **Properties**, next to **Office property**, click the down arrow. and then select the appropriate matching field.</span></span> 
    
  

> <span data-ttu-id="b38c7-196">**Hinweis:** Sie müssen nicht alle entsprechenden Feldern zuordnen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-196">**Note** You do not need to map all the corresponding fields. However, the fields shown in the following table must be mapped.</span></span> <span data-ttu-id="b38c7-197">Die Felder aus der folgenden Tabelle müssen jedoch zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="b38c7-197">You do not need to map all the corresponding fields. However, the fields shown in the following table must be mapped.</span></span> 
  
    
    


<span data-ttu-id="b38c7-198">**Tabelle: Outlook-Elementfeld zugeordneter Outlook-Elementtyp**</span><span class="sxs-lookup"><span data-stu-id="b38c7-198">**Table: Outlook item type mapped to Outlook item field**</span></span>


|<span data-ttu-id="b38c7-199">**Outlook-Elementtyp**</span><span class="sxs-lookup"><span data-stu-id="b38c7-199">**Outlook item type**</span></span>|<span data-ttu-id="b38c7-200">**Outlook-Elementfeld**</span><span class="sxs-lookup"><span data-stu-id="b38c7-200">**Outlook item field**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b38c7-201">Kontakt</span><span class="sxs-lookup"><span data-stu-id="b38c7-201">Contact</span></span>  <br/> |<span data-ttu-id="b38c7-202">LastName</span><span class="sxs-lookup"><span data-stu-id="b38c7-202">LastName</span></span>  <br/> |
|<span data-ttu-id="b38c7-203">Aufgabe</span><span class="sxs-lookup"><span data-stu-id="b38c7-203">Task</span></span>  <br/> |<span data-ttu-id="b38c7-204">Subject</span><span class="sxs-lookup"><span data-stu-id="b38c7-204">Subject</span></span>  <br/> |
|<span data-ttu-id="b38c7-205">Termin</span><span class="sxs-lookup"><span data-stu-id="b38c7-205">Appointment</span></span>  <br/> |<span data-ttu-id="b38c7-206">Beginnt um, Endet um und Betreff</span><span class="sxs-lookup"><span data-stu-id="b38c7-206">Start, End, and Subject</span></span>  <br/> |
|<span data-ttu-id="b38c7-207">Beitrag</span><span class="sxs-lookup"><span data-stu-id="b38c7-207">Post</span></span>  <br/> |<span data-ttu-id="b38c7-208">Subject</span><span class="sxs-lookup"><span data-stu-id="b38c7-208">Subject</span></span>  <br/> |
   
<span data-ttu-id="b38c7-209">Nicht zugeordnete Felder werden je nach Anzahl wie folgt als erweiterte Eigenschaften angezeigt:</span><span class="sxs-lookup"><span data-stu-id="b38c7-209">Unmapped fields, depending on the number, are displayed as extended properties as follows:</span></span>
  
    
    

- <span data-ttu-id="b38c7-210">**Benachbart** Wird dem Formularbereich unten auf der Standardseite eines Outlook-Formulars angefügt (2 bis 5 Felder).</span><span class="sxs-lookup"><span data-stu-id="b38c7-210">**Adjoining** Appended to the form region at the bottom of an Outlook form's default page (two to five fields).</span></span>
    
  
- <span data-ttu-id="b38c7-211">**Getrennt** Wird einem Outlook-Formular als neue Seite hinzugefügt (mindestens 6 Felder).</span><span class="sxs-lookup"><span data-stu-id="b38c7-211">**Separate** Added as a new page to an Outlook form (six or more fields).</span></span>
    
  

## <a name="set-up-the-external-item-picker-control"></a><span data-ttu-id="b38c7-212">Einrichten des Steuerelements für das Auswahltool für externe Elemente</span><span class="sxs-lookup"><span data-stu-id="b38c7-212">Set up the external item picker control</span></span>
<span data-ttu-id="b38c7-213"><a name="section9"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-213"></span></span>

<span data-ttu-id="b38c7-p116">Das Steuerelement für das Auswahltool für externe Elemente ermöglicht Benutzern das Auswählen eines Felds, z. B. eines ID-Felds oder eines Felds mit eindeutigen Werten, um ein Element bequem auszuwählen. Dieses Steuerelement steht in SharePoint- und Office 2013-Produkten zur Verfügung. Beispielsweise können Benutzer dieses Steuerelement nutzen, um in einer externen Liste von Kunden ein Element auswählen. In Word 2013 kann dieses Steuerelement mit Inhaltssteuerelementen verwendet werden, die mit externen Datenspalten verknüpft sind. Es ist ratsam, bestimmte Spalten auswählen, die Sie im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, weil standardmäßig alle Spalten angezeigt werden, was in den meisten Fällen nicht erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p116">The external item picker control allows users to select a field, such as an ID field or a field that has unique values, to conveniently choose an item. This control is available in SharePoint and Office 2013 products. For example, users can use this control to choose an item from an external list of customers and Word 2013 enables this control for use with content controls that are linked to external data columns.It's a good idea to select the specific columns you want to display in the external item picker control because the default operation is to show all the columns, which in most cases, is not necessary.</span></span>
  
    
    

1. <span data-ttu-id="b38c7-217">Klicken Sie auf jedes Feld, das im Steuerelement für das Auswahltool für externe Elemente angezeigt werden soll, um es zu markieren, und aktivieren Sie dann unter **Eigenschaften** das Kontrollkästchen **In Auswahl anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-217">For each field that you want displayed in the external content item picker, click and highlight the field, and then under **Properties**, click the **Show in Picker** check box.</span></span>
    
  
2. <span data-ttu-id="b38c7-218">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-218">Click **Next**.</span></span>
    
  

> <span data-ttu-id="b38c7-219">**Hinweis:** Alle Filter, die Sie definieren, werden im Steuerelement für das Auswahltool für externe Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-219">**Note:** All filters that you define are displayed in the external item picker control.</span></span> <span data-ttu-id="b38c7-220">Obwohl sich bestimmte Filter nicht aus dem Steuerelement für das Auswahltool für externe Elemente entfernen lassen, können Sie einen Standardfilter definieren, indem Sie im Dialogfeld **Filterkonfiguration** auf **Ist Standard** klicken, wenn Sie den Filter erstellen oder ändern.</span><span class="sxs-lookup"><span data-stu-id="b38c7-220">Note All filters that you define are displayed in the external item picker control. Although you cannot remove specific filters from the external item picker control, you can define a default filter by clicking **Is Default** in the **Filter configuration** dialog box when you are creating or modifying the filter.</span></span>
  
    
    


## <a name="define-filters"></a><span data-ttu-id="b38c7-221">Definieren von Filtern</span><span class="sxs-lookup"><span data-stu-id="b38c7-221">Define filters</span></span>
<span data-ttu-id="b38c7-222"><a name="section10"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-222"></span></span>

<span data-ttu-id="b38c7-p118">Wenn Sie keine Filter definieren, gibt eine externe Liste alle Daten bis zum Business Connectivity Services (BCS)-Grenzwert (standardmäßig 2.000 Elemente) bzw. alle Daten zurück, die im externen Inhaltstyp definiert sind, wenn die Menge unter dem aktuellen Grenzwert liegt. Darüber hinaus erfolgt die gesamte Verarbeitung der Ergebnisse innerhalb des SharePoint-Produkts. Es ist ratsam, mindestens einen Filter zu definieren. Im Allgemeinen gibt es zwei Arten von Filtern, die Sie kennen sollten:</span><span class="sxs-lookup"><span data-stu-id="b38c7-p118">If you do not define a filter, an external list returns all of the data up to the Business Connectivity Services (BCS) throttle limit (by default, 2,000 items) or all the data that is defined in the external content type, if less than the current throttle limit. In addition, the entire processing of the results occurs within the SharePoint product. It's a good idea to define at least one filter. In general, there are two types of filters that you need to be aware:</span></span>
  
    
    

- <span data-ttu-id="b38c7-p119">**Datenquellenfilter** Wenn Sie einen Filter für externe Inhaltstypen erstellen, der als Datenquellenfilter bezeichnet wird, erfolgt der Filtervorgang innerhalb der SQL Server-Datenbank. Dies ist wichtig, wenn Sie mit großen Datenmengen arbeiten, da Sie die Verarbeitung aus den SharePoint-Produkten in die externe Datenbank auslagern und sich Leistungsverbesserungen verschaffen können. Nachdem Sie die externe Liste erstellt haben, können Sie den Datenquellenfilter durch Erstellen einer Ansicht nutzen, die verschiedene Filterwerte im Abschnitt **Datenquellenfilter** der Einstellungsseite **Listenansicht** angibt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p119">**Data Source Filter** When you create an external content type filter, which is known as a Data Source Filter, the filter operation occurs within the SQL Server database. This is important when you are working with lots of data because you can offload processing from SharePoint products to the external database and gain performance improvements. After you create the external list, you can use the Data Source Filter by creating a view that specifies different filter values in the **Data Source Filter** section of the **List View** settings page.</span></span>
    
  
- <span data-ttu-id="b38c7-p120">**SharePoint-Filter** Benutzer können Daten weiterhin mithilfe eines SharePoint-Filters filtern, entweder mit dem Spaltenüberschriftsfilter oder mithilfe des Abschnitts **Filter** auf der Einstellungsseite **Listenansicht**. In diesem Fall erfolgt der Filtervorgang im SharePoint-Produkt und nicht innerhalb der SQL Server-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p120">**SharePoint filter** Users can still filter the data by using a SharePoint filter, either the column header filter or by using the **Filters** section in the **List View** settings page. In this case, the filter operation occurs within the SharePoint product, not within the SQL Server database.</span></span>
    
  
<span data-ttu-id="b38c7-232">Eine zu erwägende ratsame Strategie ist das Erstellen einer Gruppe externer Listenansichten basierend auf bestimmten Datenquellenfiltern, die sicherstellen, dass größere Datenmengen zuerst in der externen Datenquelle gefiltert werden. Anschließend können Benutzer weiter filtern und die Ergebnisse mithilfe von SharePoint-Filter optimieren.</span><span class="sxs-lookup"><span data-stu-id="b38c7-232">A good strategy to consider is to create a set of external list views based on specific Data Source Filters that make sure that larger amounts of data are filtered first in the external data source, and then users can further filter and refine the results by using SharePoint filters.</span></span>
  
    
    
<span data-ttu-id="b38c7-p121">Sie können verschiedene Arten von Filtern erstellen. Führen Sie für jeden Filter, den Sie erstellen, folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="b38c7-p121">You can create several different types of filters. For each filter that you create, do the following:</span></span>
  
    
    

1. <span data-ttu-id="b38c7-235">Wählen Sie unter **Eigenschaften** neben **Datenquellenelement** ein Feld aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-235">Under **Properties**, next to **Data Source Element**, select a field.</span></span>
    
  
2. <span data-ttu-id="b38c7-236">Klicken Sie unter **Eigenschaften** neben **Filter** auf **Zum Hinzufügen klicken**, um das Dialogfeld **Filterkonfiguration** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b38c7-236">Under **Properties**, next to **Filter**, click **Click to Add** to display the **Filter Configuration** dialog box.</span></span>
    
  
3. <span data-ttu-id="b38c7-237">Klicken Sie auf **Filterparameter hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-237">Click **Add Filter Parameter**.</span></span>
    
  
4. <span data-ttu-id="b38c7-238">Geben Sie im Feld **Neuer Filter** einen Namen für den Filter ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-238">In the **New Filter** box, enter a filter name.</span></span>
    
  
5. <span data-ttu-id="b38c7-239">Wählen Sie im Feld **Filtertyp** einen Filtertyp aus:</span><span class="sxs-lookup"><span data-stu-id="b38c7-239">In the **Filter Type** box, select a filter type:</span></span>
    
    
  
    
    
 <span data-ttu-id="b38c7-240">**Vergleiche**</span><span class="sxs-lookup"><span data-stu-id="b38c7-240">**Comparisons**</span></span>
  
    
    

    
    <span data-ttu-id="b38c7-241">Ein Vergleichsfilter beschränkt, welche Elemente basierend auf einer Bedingung zurückgegeben werden (z. B. Bundesland = "Hessen") und wird in eine SQL-WHERE-Klausel umgewandelt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-241">A Comparison filter limits what items are returned based on a condition (such as State = "New Jersey") and is converted to an SQL WHERE clause.</span></span>
    
1. <span data-ttu-id="b38c7-242">Wählen Sie im Feld **Filtertyp** die Option **Vergleich** aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-242">In the **Filter Type** box, select **Comparison**.</span></span>
    
  
2. <span data-ttu-id="b38c7-243">Wählen Sie im Feld **Operator** einen Vorgang aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-243">In the **Operator** box, select an operation.</span></span>
    
  
3. <span data-ttu-id="b38c7-244">Stellen Sie im Feld **Filterfeld** sicher, dass das Feld, das Sie vergleichen möchten, ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b38c7-244">In the **Filter Field** box, make sure that the field that you want to compare is selected.</span></span>
    
  
4. <span data-ttu-id="b38c7-245">Wenn die vom Benutzer eingegebenen Werte hinsichtlich der Groß- und Kleinschreibung übereinstimmen sollen, wählen Sie **Groß-und Kleinschreibung**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-245">If you want values entered by the user to match by case, click **Case Sensitive**.</span></span>
    
  
5. <span data-ttu-id="b38c7-246">Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-246">If you want to display a list of possible matches ¡n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
6. <span data-ttu-id="b38c7-247">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-247">Click **OK**.</span></span>
    
  
7.  <span data-ttu-id="b38c7-p122">Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p122">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span>
    
  

    
  
    
    
 <span data-ttu-id="b38c7-250">**Platzhalter**</span><span class="sxs-lookup"><span data-stu-id="b38c7-250">**Wildcards**</span></span>
  
    
    

    
    <span data-ttu-id="b38c7-251">Ein Platzhalterfilter beschränkt, welche Elemente basierend auf einem vom Benutzer angegebenen Zeichenfolgenwert (z. B. Zustand enthält "Neu") zurückgegeben werden, und wird in eine SQL-ähnliche Klausel konvertiert.</span><span class="sxs-lookup"><span data-stu-id="b38c7-251">A Wildcard filter limits what items are returned based on a user-entered string value (such as State Contains "New") and is converted to an SQL LIKE clause. Valid sqlservnv2 wildcard characters are * (asterisk) which means match any number of characters and _ (underscore) which means match one and only one character. </span></span> <span data-ttu-id="b38c7-252">Gültige SQL Server-Platzhalterzeichen sind \* (Sternchen), was bedeutet, dass eine beliebige Anzahl von Zeichen übereinstimmen muss, und \_ (Unterstrich), was bedeutet, dass nur ein einziges Zeichen übereinstimmen muss.</span><span class="sxs-lookup"><span data-stu-id="b38c7-252">A Wildcard filter limits what items are returned based on a user-entered string value (such as State Contains "New") and is converted to an SQL LIKE clause. Valid SQL Server wildcard characters are * (asterisk) which means match any number of characters and _ (underscore) which means match one and only one character.</span></span> 
  
    
    

    
1. <span data-ttu-id="b38c7-253">Wählen Sie im Kontrollkästchen **Filtertyp** die Option **Platzhalter**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-253">In the **Filter Type** box, select **Wildcard**.</span></span>
    
  
2. <span data-ttu-id="b38c7-254">Wählen Sie im Feld **Filterfeld** ein Feld aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-254">In the **Filter Field** box, select a field.</span></span>
    
  
3. <span data-ttu-id="b38c7-255">Wenn die vom Benutzer eingegebenen Werte hinsichtlich der Groß- und Kleinschreibung übereinstimmen sollen, wählen Sie **Groß-und Kleinschreibung**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-255">If you want values entered by the user to match by case, click **Case Sensitive**.</span></span>
    
  
4. <span data-ttu-id="b38c7-256">Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-256">If you want to display a list of possible matches ¡n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
5. <span data-ttu-id="b38c7-257">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-257">Click **OK**.</span></span>
    
  
6.  <span data-ttu-id="b38c7-258">Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-258">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span> <span data-ttu-id="b38c7-259">Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-259">If you do not enter a value, the external list does not display any items.</span></span> <span data-ttu-id="b38c7-260">Es ist ratsam, ein \* (Sternchen) als Standard einzugeben.</span><span class="sxs-lookup"><span data-stu-id="b38c7-260">It's a good idea to enter an \* (asterisk) as the default.</span></span>
    
  

    
  
    
    
 <span data-ttu-id="b38c7-261">**Grenze**</span><span class="sxs-lookup"><span data-stu-id="b38c7-261">**Limit**</span></span>
  
    
    

    
    <span data-ttu-id="b38c7-p125">In den meisten Fällen müssen Sie einen Limit-Filter für Lese- und Listenlesevorgänge definieren. Wenn Sie kein **Standardlimit** festlegen, werden aus der externen Datenquelle keine Daten abgerufen. Stellen Sie sicher, dass der Standardwert, den Sie für den Limit-Filter angeben, kleiner als 2.000 ist, da der Business Connectivity Services (BCS)-Standardgrenzwert 2.000 Elemente ist. Sie können diesen Grenzwert erhöhen, sollte dies erforderlich sein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p125">In most cases, you must define a Limit Filter for Read and Read List operations. If you do not define a **Default Limit** value, no data is retrieved from the external data source. Ensure that the default value that you enter for the limit filter is less than 2,000, because the default Business Connectivity Services (BCS) throttle is 2,000 items. You can increase this limit if it is necessary.</span></span>
    
1. <span data-ttu-id="b38c7-266">Wählen Sie im Feld **Filtertyp** die Option **Limit** aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-266">In the **Filter Type** box, select **Limit**.</span></span> 
    
  
2. <span data-ttu-id="b38c7-267">Geben Sie in das Kästchen **Anzahl** eine Zahl ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-267">In the **Number** box, enter a number.</span></span>
    
  
3. <span data-ttu-id="b38c7-268">Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-268">If you want to display a list of possible matches ¡n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
4. <span data-ttu-id="b38c7-p126">Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p126">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span>
    
  
5. <span data-ttu-id="b38c7-271">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-271">Click **OK**.</span></span> 
  
    
    

    
  

    > <span data-ttu-id="b38c7-272">**Hinweis:** Der SQL Server-Administrator kann zudem spezielle Tabellen, Ansichten, Indizes und optimierte Abfragen erstellen, um die Ergebnisse auf die benötigten Elemente zu beschränken und die Leistung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="b38c7-272">**Note** The SQL Server database administrator might want to create specific tables, views, indexes, and optimized queries to limit the results to just what is needed and to help improve performance.</span></span> 

    
  
    
    
 <span data-ttu-id="b38c7-273">**Seitenzahl**</span><span class="sxs-lookup"><span data-stu-id="b38c7-273">**Page Number**</span></span>
  
    
    

    
    <span data-ttu-id="b38c7-274">Verwenden Sie den externen Inhaltstyp Seitenzahl, um den SharePoint-Seitengrenzwert zu ersetzen, der auf der Seite **Listenansicht** der externen Liste festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="b38c7-274">Use the external content type Page Number to supersede the SharePoint page limit defined in the **List View** page of the external list. Here’s the difference:</span></span> <span data-ttu-id="b38c7-275">Dies sind die Unterschiede:</span><span class="sxs-lookup"><span data-stu-id="b38c7-275">Here's the difference:</span></span>
    
  - <span data-ttu-id="b38c7-276">Beim externen Inhaltstyp Seitenzahl werden zuerst die Ergebnisse innerhalb der SQL Server-Datenbank verarbeitet. Dann nur wird die Anzahl der Zeilen zurückgegeben und angezeigt, die vom Wert Seitengröße bestimmt wird.</span><span class="sxs-lookup"><span data-stu-id="b38c7-276">The external content type Page Number first processes the results within the sqlservnv2 database, and then returns and displays only the number of rows determined by the Page Size value.</span></span>
    
  
  - <span data-ttu-id="b38c7-277">Beim SharePoint-Seitengrenzwert werden alle Zeilen bis zur Größe von Standardwert aus der SQL Server-Datenbank zurückgegeben. Anschließend wird die Anzahl der Zeilen angezeigt, die vom SharePoint-Seitengrenzwert auf der Einstellungsseite **Listenansicht** bestimmt wird.</span><span class="sxs-lookup"><span data-stu-id="b38c7-277">The SharePoint page limit returns all the rows up to the Default Value size from the sqlservnv2 database, and then displays the number of rows determined by the SharePoint page limit value in the List View settings page.</span></span>
    
  

    <span data-ttu-id="b38c7-278">Die Verwendung der externen Inhaltstyp-Seitenzahl ist im Allgemeinen effizienter.</span><span class="sxs-lookup"><span data-stu-id="b38c7-278">Using the external content type Page Number is generally more efficient.</span></span> <span data-ttu-id="b38c7-279">Darüber hinaus hilft der Wert der **Reihenfolge** sicherzustellen, dass eine genaue Anzeige der Ergebnisse zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b38c7-279">Using the external content type Page Number is generally more efficient. In addition, the **Order** value helps make sure that an accurate display of the results returned.</span></span>
    
1. <span data-ttu-id="b38c7-280">Wählen Sie im Kontrollkästchen **Filtertyp** die Option **Seitenzahl**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-280">In the **Filter Type** box, select **Page Number**.</span></span> 
    
  
2. <span data-ttu-id="b38c7-281">Geben Sie in das Feld **Seitenzahl** eine Zahl ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-281">In the **Page Size** box, enter a number.</span></span>
    
  
3. <span data-ttu-id="b38c7-282">Wählen Sie im Feld **Reihenfolge** eine Sortierrichtung aus.</span><span class="sxs-lookup"><span data-stu-id="b38c7-282">In the **Order** box, select a sort direction.</span></span>
    
  
4. <span data-ttu-id="b38c7-283">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-283">Click **OK**.</span></span> 
    
  
5. <span data-ttu-id="b38c7-p129">Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p129">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span> 
  
    
    

    
  
6. <span data-ttu-id="b38c7-286">Wenn Sie ein Feld anzeigen, aber nicht ändern möchten, klicken Sie auf das Feld, um es zu markieren, und klicken Sie dann unter **Eigenschaften** auf **Schreibgeschützt**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-286">If you want to display but not modify a field, click and highlight the field, and then under **Properties**, select **Read-Only**.</span></span>
    
  
7. <span data-ttu-id="b38c7-287">Falls Sie sicherstellen möchten, dass ein Feld immer einen Wert enthält, wenn es erstellt oder geändert wird, klicken Sie auf das Feld, um es zu markieren, und klicken Sie dann unter **Eigenschaften** auf **Erforderlich**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-287">If you want to make sure that a field always has a value when it's created or modified, click and highlight the field, and then under **Properties**, select **Required**.</span></span>
    
  
8. <span data-ttu-id="b38c7-288">Wenn Sie im Steuerelement für das Auswahltool für externe Elemente für den Namen in **Datenquellenelement**, der vom SQL Server-Spaltennamen abgeleitet ist, einen beschreibenden Namen angeben möchten, klicken Sie auf das Feld, um es zu markieren, und geben Sie dann unter **Eigenschaften** in das Feld **Anzeigename** einen Namen ein.</span><span class="sxs-lookup"><span data-stu-id="b38c7-288">To provide a descriptive name in the external item picker control of the **Data Source Element** name, which is derived from the SQL Server column name, click and highlight the field, and then under **Properties**, in the **Display Name** box, enter a name.</span></span>
    
  
9. <span data-ttu-id="b38c7-p130">Zum Definieren eines Standardwerts für den Filter (der auch im Abschnitt **Datenquellenfilter** auf der Einstellungsseite **Listenansicht** angezeigt wird) klicken Sie unter **Filterparameter** auf den Filter, um ihn zu markieren. Geben Sie dann in das Feld **Standardwert** den gewünschten Wert ein. Wenn Sie keinen Wert eingeben, werden beim ersten Verwenden dieses Filters keine Elemente angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p130">To define a default value for the filter (which also displays in the **Data Source Filter** section of the **List View** settings page), under **Filter Parameters**, click and highlight the filter, and then in the **Default Value** box, enter an appropriate value. If you do not enter a value, then when that filter is used for the first time, no items are displayed.</span></span>
    
  

## <a name="set-the-title-field-for-an-external-list"></a><span data-ttu-id="b38c7-291">Festlegen des Felds "Titel" für eine externe Liste</span><span class="sxs-lookup"><span data-stu-id="b38c7-291">Set the Title field for an external list</span></span>
<span data-ttu-id="b38c7-292"><a name="section11"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-292"></span></span>


1. <span data-ttu-id="b38c7-293">Klicken Sie auf dem Menüband auf **Zusammenfassungsansicht**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-293">On the ribbon, click **Summary View**.</span></span>
    
  
2. <span data-ttu-id="b38c7-294">Wählen Sie im Abschnitt **Felder** unter **Feldname** ein Feld.</span><span class="sxs-lookup"><span data-stu-id="b38c7-294">In the **Fields** section, under **Field Name**, select a field.</span></span>
    
    > <span data-ttu-id="b38c7-295">**Wichtig:** Im Allgemeinen ist es ratsam, dass der Titel aus einem Feld mit einem eindeutigen Wert besteht.</span><span class="sxs-lookup"><span data-stu-id="b38c7-295">**Important:** In general, it's a good idea to make the Title a field that has a unique value.</span></span> <span data-ttu-id="b38c7-296">Das Titelfeld wird zum Anzeigen der Liste oder InfoPath-Formulare verwendet.</span><span class="sxs-lookup"><span data-stu-id="b38c7-296">The Title field is used to display list or InfoPath forms.</span></span> <span data-ttu-id="b38c7-297">Nachdem Sie das Titelfeld festgelegt haben, können Sie es nicht mehr ändern.</span><span class="sxs-lookup"><span data-stu-id="b38c7-297">Once you set the Title field, you cannot change it.</span></span> 
3. <span data-ttu-id="b38c7-298">Klicken Sie auf dem Menüband auf **Als Titel festlegen**.</span><span class="sxs-lookup"><span data-stu-id="b38c7-298">On the ribbon, click **Set as Title**.</span></span>
    
  

## <a name="complete-the-external-content-type"></a><span data-ttu-id="b38c7-299">Vervollständigen des externen Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="b38c7-299">Complete the external content type</span></span>
<span data-ttu-id="b38c7-300"><a name="section12"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-300"></span></span>


- <span data-ttu-id="b38c7-p132">Klicken Sie auf der Symbolleiste für den Schnellzugriff auf **Speichern**. Dadurch wird die Definition des externen Inhaltstyps im Business Data Connectivity-Metadatenspeicher gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b38c7-p132">On the Quick Access Toolbar, click **Save**. This stores the external content type definition in the Business Data Connectivity metadata store.</span></span>
    
  

> <span data-ttu-id="b38c7-303">**Hinweis:** Um eine bessere Leistung zu erzielen, speichert Business Data Connectivity alle Objekte im Metadatenspeicher zwischen und aktualisiert Änderungen mit einem Zeitgeberauftrag, der jede Minute ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b38c7-303">**Note** To provide better performance, Business Data Connectivity caches all the objects in the metadata store and updates changes by using a timer job that runs every minute. It might take up to one minute for changes to propagate to all the servers in the farm, but changes are immediate on the server where you make the change.</span></span> <span data-ttu-id="b38c7-304">Es kann bis zu einer Minute dauern, bis die Änderungen an alle Server in der Farm weitergegeben wurden, aber die Änderungen auf dem Server, auf dem Sie die Änderung vorgenommen haben, treten sofort in Kraft.</span><span class="sxs-lookup"><span data-stu-id="b38c7-304">Note To provide better performance, Business Data Connectivity caches all the objects in the metadata store and updates changes by using a timer job that runs every minute. It might take up to one minute for changes to propagate to all the servers in the farm, but changes are immediate on the server where you make the change.</span></span> 
  
    
    

<span data-ttu-id="b38c7-305">Den hinzugefügten Benutzern steht jetzt der externe Inhaltstyp für die Verwendung in SharePoint- und Office 2013-Produkten zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b38c7-305">The external content type is now available for use in SharePoint and Office 2013 products.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="b38c7-306">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b38c7-306">Additional resources</span></span>
<span data-ttu-id="b38c7-307"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="b38c7-307"></span></span>


-  [<span data-ttu-id="b38c7-308">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b38c7-308">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b38c7-309">Deploy a Business Connectivity Services on-premises solution in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b38c7-309">Deploy a Business Connectivity Services on-premises solution in SharePoint</span></span>](http://msdn.microsoft.com/library/4692ebba-90eb-4d72-ac12-e90c4d4ee7ae.aspx)
    
  
-  [<span data-ttu-id="b38c7-310">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b38c7-310">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b38c7-311">Configure the Secure Store Service in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b38c7-311">Configure the Secure Store Service in SharePoint</span></span>](http://msdn.microsoft.com/library/29C0BC76-D835-401B-A2FB-ABB069E84125.aspx)
    
  

