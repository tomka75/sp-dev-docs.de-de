---
title: Datenspeicheroptionen in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 0e9264de4cb19e4f32939e02786611580d41c82d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="data-storage-options-in-sharepoint-online"></a><span data-ttu-id="6596d-102">Datenspeicheroptionen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6596d-102">Data storage options in SharePoint Online</span></span>

<span data-ttu-id="6596d-103">Bei der Entwicklung von SharePoint Online-add-ins müssen Sie eine Reihe von verschiedenen Optionen zum Speichern von Daten.</span><span class="sxs-lookup"><span data-stu-id="6596d-103">When you develop SharePoint Online add-ins, you have a number of different options for data storage.</span></span> <span data-ttu-id="6596d-104">Sie können das in diesem Artikel beschriebene Beispiel erkunden die Unterschiede zwischen den einzelnen Optionen, und lernen Sie die Vorteile der Verwendung von remote-Datenspeicher verwenden.</span><span class="sxs-lookup"><span data-stu-id="6596d-104">You can use the sample described in this article to explore the differences between each option, and to learn about the advantages to using remote data storage.</span></span> 

<span data-ttu-id="6596d-105">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="6596d-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="6596d-106">In diesem Artikel werden die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app, die jeder der folgenden Datenspeicheroptionen und die Vorteile und Nachteile der einzelnen anzeigt:</span><span class="sxs-lookup"><span data-stu-id="6596d-106">This article describes the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app, which shows you each of the following data storage options and the advantages and disadvantages of each:</span></span>

- <span data-ttu-id="6596d-107">SharePoint-Liste auf dem hostweb</span><span class="sxs-lookup"><span data-stu-id="6596d-107">SharePoint list on the host web</span></span>
    
- <span data-ttu-id="6596d-108">SharePoint-Liste im Web app</span><span class="sxs-lookup"><span data-stu-id="6596d-108">SharePoint list on the app web</span></span>
    
- <span data-ttu-id="6596d-109">SQL Azure-Datenbank</span><span class="sxs-lookup"><span data-stu-id="6596d-109">SQL Azure database</span></span>
    
- <span data-ttu-id="6596d-110">Azure Warteschlangenspeicher</span><span class="sxs-lookup"><span data-stu-id="6596d-110">Azure queue storage</span></span>
    
- <span data-ttu-id="6596d-111">Azure-tabellenspeicherung</span><span class="sxs-lookup"><span data-stu-id="6596d-111">Azure table storage</span></span>
    
- <span data-ttu-id="6596d-112">Externen Webdienst</span><span class="sxs-lookup"><span data-stu-id="6596d-112">External web service</span></span>
    
<span data-ttu-id="6596d-113">Die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app ist eine vom Anbieter gehosteten app geschrieben in c# und JavaScript, das eine Anzahl von SharePoint-Artefakte (Listen, app-Webpart, Webpart) für das hostweb und app-Webs bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-113">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app is a provider-hosted app written in C# and JavaScript that deploys a number of SharePoint artifacts (lists, app part, web part) to both the host web and the app web.</span></span> <span data-ttu-id="6596d-114">Es interagiert mit SharePoint-Listen auf der app-Web und Host-Web und führt auch Aufrufe an eine SQL Azure-Datenbank, ein Azure Warteschlangen- und Tabelle Speicherung und ein Remotewebdienst, die OData implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="6596d-114">It interacts with SharePoint lists on the app web and host web, and also makes calls to a SQL Azure database, an Azure queue and table storage, and a remote web service that implements OData.</span></span> <span data-ttu-id="6596d-115">In diesem Beispiel wird das Muster Model-View-Controller (MVC) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6596d-115">This sample uses the Model-View-Controller (MVC) pattern.</span></span>
<span data-ttu-id="6596d-116">Die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app gilt jede Speicheroption Daten auf eine bestimmte Funktion für die die Option gut geeignet ist, wie in der folgenden Tabelle beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6596d-116">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app applies each data storage option to a specific function for which the option is well suited, as described in the following table.</span></span>

|<span data-ttu-id="6596d-117">Beispiel-app-Speicheroption</span><span class="sxs-lookup"><span data-stu-id="6596d-117">Sample app storage option</span></span>|<span data-ttu-id="6596d-118">Verwendet für</span><span class="sxs-lookup"><span data-stu-id="6596d-118">Used for</span></span>|
|:--|:--|
|<span data-ttu-id="6596d-119">SharePoint-Liste app-web</span><span class="sxs-lookup"><span data-stu-id="6596d-119">SharePoint list app web</span></span>|<span data-ttu-id="6596d-120">Kunden-Notizen</span><span class="sxs-lookup"><span data-stu-id="6596d-120">Customer notes</span></span>|
|<span data-ttu-id="6596d-121">SharePoint-Liste Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="6596d-121">SharePoint list host web</span></span>|<span data-ttu-id="6596d-122">Support-Anfragen</span><span class="sxs-lookup"><span data-stu-id="6596d-122">Support cases</span></span>|
|<span data-ttu-id="6596d-123">Northwind-OData-Dienst</span><span class="sxs-lookup"><span data-stu-id="6596d-123">Northwind OData service</span></span>|<span data-ttu-id="6596d-124">Kunden</span><span class="sxs-lookup"><span data-stu-id="6596d-124">Customers</span></span>|
|<span data-ttu-id="6596d-125">Azure-tabellenspeicherung</span><span class="sxs-lookup"><span data-stu-id="6596d-125">Azure table storage</span></span>|<span data-ttu-id="6596d-126">CSR-Bewertungen</span><span class="sxs-lookup"><span data-stu-id="6596d-126">CSR ratings</span></span>|
|<span data-ttu-id="6596d-127">Azure Warteschlangenspeicher</span><span class="sxs-lookup"><span data-stu-id="6596d-127">Azure queue storage</span></span>|<span data-ttu-id="6596d-128">Aufrufen der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="6596d-128">Call queue</span></span>|
|<span data-ttu-id="6596d-129">SQL Azure-Datenbank Northwind</span><span class="sxs-lookup"><span data-stu-id="6596d-129">SQL Azure Northwind database</span></span>|<span data-ttu-id="6596d-130">Aufträge, Bestelldetails, Produkte</span><span class="sxs-lookup"><span data-stu-id="6596d-130">Orders, order details, products</span></span>|

<span data-ttu-id="6596d-131">Die app implementiert ein Customer Service Dashboard und zugehörige Schnittstellen, die aktuellen Aufträge, Kunden repräsentative Umfrage Bewertungen, Kunden Notizen, Support-Anfragen und eine Customer Vertreter Warteschlange anzeigen.</span><span class="sxs-lookup"><span data-stu-id="6596d-131">The app implements a customer service dashboard and related interfaces that show recent orders, customer representative survey ratings, customer notes, support cases, and a customer representative call queue.</span></span> <span data-ttu-id="6596d-132">Die ersten beiden Szenarien können Sie das Abrufen von Daten mithilfe von relativ einfach, Client-Objektmodellcode oder REST-Abfragen, aber durch Liste Abfrage Schwellenwerte begrenzt werden.</span><span class="sxs-lookup"><span data-stu-id="6596d-132">The first two scenarios let you retrieve data by using relatively simply client object model code or REST queries, but are limited by list query thresholds.</span></span> <span data-ttu-id="6596d-133">Die folgenden vier Szenarien verwendet unterschiedliche Typen von Remotespeicher.</span><span class="sxs-lookup"><span data-stu-id="6596d-133">The next four scenarios uses different types of remote storage.</span></span> 

<span data-ttu-id="6596d-134">**Abbildung 1. Startseite für Data Storage Modelle fordert Sie zum Bereitstellen von SharePoint-Komponenten**</span><span class="sxs-lookup"><span data-stu-id="6596d-134">**Figure 1. Data storage models start page prompts you to deploy SharePoint components**</span></span>

![Screenshot des app-Beispiel-UI](media/bb3b58ca-b983-4ec4-b36d-18a911edb5d5.png)

## <a name="before-you-begin"></a><span data-ttu-id="6596d-136">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="6596d-136">Before you begin</span></span>
<span data-ttu-id="6596d-137"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-137"></span></span>

<span data-ttu-id="6596d-138">Bevor Sie dieses Beispiel verwenden, stellen Sie sicher, dass Sie über Folgendes verfügen:</span><span class="sxs-lookup"><span data-stu-id="6596d-138">Before you use this sample, make sure that you have the following:</span></span>

- <span data-ttu-id="6596d-139">Ein Microsoft Azure-Konto können Sie eine SQL Azure-Datenbank bereitstellen und erstellen Sie ein Konto Azure-Speicher.</span><span class="sxs-lookup"><span data-stu-id="6596d-139">A Microsoft Azure account where you can deploy a SQL Azure database and create an Azure storage account.</span></span> 
    
- <span data-ttu-id="6596d-140">SharePoint-Entwickler-Standort, damit Sie das Beispiel aus Visual Studio 2013 bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="6596d-140">A SharePoint developer site so that you can deploy the sample from Visual Studio 2013.</span></span>
    
<span data-ttu-id="6596d-141">Darüber hinaus müssen Sie die Northwind-Datenbank in Microsoft Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="6596d-141">Also, you need to deploy the Northwind database to Microsoft Azure.</span></span>

### <a name="to-deploy-the-northwind-database"></a><span data-ttu-id="6596d-142">Zum Bereitstellen der Northwind-Datenbank</span><span class="sxs-lookup"><span data-stu-id="6596d-142">To deploy the Northwind database</span></span>

1. <span data-ttu-id="6596d-143">Melden Sie sich an dem Azure-Verwaltungsportal, und wählen Sie **SQL-Datenbanken**> **Server**.</span><span class="sxs-lookup"><span data-stu-id="6596d-143">Log on to the Azure Management Portal and choose  **SQL Databases**> **Servers**.</span></span>
    
2. <span data-ttu-id="6596d-144">Wählen Sie **einen SQL-Datenbankserver zu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="6596d-144">Choose  **Create a SQL Database Server**.</span></span>
    
3. <span data-ttu-id="6596d-145">Geben Sie Werte für **Benutzername**, **Kennwort**und **Region**, wie in Abbildung 2 dargestellt im Format **Server erstellen** .</span><span class="sxs-lookup"><span data-stu-id="6596d-145">In the  **Create Server** form, enter values for **Login Name**,  **Login Password**, and  **Region**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="6596d-146">**Abbildung 2. Servereinstellungen für SQL-Datenbank**</span><span class="sxs-lookup"><span data-stu-id="6596d-146">**Figure 2. SQL database server settings**</span></span>

    ![Zeigt die SQL-Datenbank für den server](media/7ae059fa-eecc-4446-8171-294e44acb189.png)

4. <span data-ttu-id="6596d-148">Wählen Sie die Taste mit dem Häkchen auf Fertig stellen, und erstellen Sie den Server.</span><span class="sxs-lookup"><span data-stu-id="6596d-148">Choose the checkmark button to finish and create the server.</span></span>
    
5. <span data-ttu-id="6596d-149">Nun, dass Sie die Datenbank erstellt haben, wählen Sie den Namen des Servers, den Sie erstellt haben, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-149">Now that you've created the database, choose the server name that you created, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="6596d-150">**Abbildung 3. Servernamen, klicken Sie auf der Seite Server**</span><span class="sxs-lookup"><span data-stu-id="6596d-150">**Figure 3. Server name on the Servers page**</span></span>

    ![Zeigt die Liste der SQL-Datenbanken](media/a6b097e4-5ad2-47df-9e31-ac0d699efd76.png)

6. <span data-ttu-id="6596d-152">Wählen Sie **Konfigurieren**, und wählen Sie den Pfeil in der unteren rechten Ecke, um die Konfiguration abzuschließen, und wählen Sie **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="6596d-152">Choose  **CONFIGURE**, and then choose the arrow in the lower right corner to complete the configuration, and choose  **SAVE**.</span></span>
    
7. <span data-ttu-id="6596d-153">Öffnen Sie SQL Server Management Studio auf Ihrem lokalen Entwicklungscomputer und erstellen Sie eine neue Datenbank mit dem Namen **NorthWind**.</span><span class="sxs-lookup"><span data-stu-id="6596d-153">Open SQL Server Management Studio on your local development computer and create a new database named  **NorthWind**.</span></span>
    
8. <span data-ttu-id="6596d-154">Wählen Sie aus der **Nordwind** -Datenbank im **Objekt-Explorer**, und wählen Sie dann auf **Neue Abfrage**.</span><span class="sxs-lookup"><span data-stu-id="6596d-154">In the  **Object Explorer**, select the  **Northwind** database, and then choose **New Query**.</span></span>
    
9. <span data-ttu-id="6596d-155">Öffnen Sie in einem Text-Editor Ihrer Wahl northwind.sql-SQL-Skript, das bereitgestellt wird mit dem Beispiel [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) .</span><span class="sxs-lookup"><span data-stu-id="6596d-155">In a text editor of your choice, open the northwind.sql SQL script that is provided with the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample.</span></span>
    
10. <span data-ttu-id="6596d-156">Kopieren Sie den Text in der Datei northwind.sql, und fügen Sie ihn in das **Fenster SQL-Abfrage** in der SQL Server Management Studio, und wählen Sie dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="6596d-156">Copy the text in the northwind.sql file and paste it into the  **SQL Query window** in the SQL Server Management Studio, and then choose **Execute**.</span></span>
    
11. <span data-ttu-id="6596d-157">Öffnen Sie im **Objekt-Explorer**das Kontextmenü (Rechtsklick) der **Northwind** -Datenbank, wählen Sie **Tasks**aus, und wählen Sie dann auf **Datenbank in SQL Azure bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="6596d-157">In the  **Object Explorer**, open the shortcut menu for (right-click) the  **Northwind** database, select **Tasks**, and then select  **Deploy Database to SQL Azure**.</span></span>
    
12. <span data-ttu-id="6596d-158">Wählen Sie auf dem Bildschirm **Einführung in die** **nächste**.</span><span class="sxs-lookup"><span data-stu-id="6596d-158">On the  **Introduction** screen, choose **Next**.</span></span>
    
13. <span data-ttu-id="6596d-159">Wählen Sie **verbinden...** , und geben Sie den **Servernamen** für den soeben erstellten SQL Azure-Datenbankserver.</span><span class="sxs-lookup"><span data-stu-id="6596d-159">Choose  **Connect ...** and enter the **Server name** for the SQL Azure Database Server you just created.</span></span>
    
14. <span data-ttu-id="6596d-160">Wählen Sie im Dropdownmenü für die **Authentifizierung** **SQL Server-Authentifizierung**aus.</span><span class="sxs-lookup"><span data-stu-id="6596d-160">In the  **Authentication** dropdown, select **SQL Server Authentication**.</span></span>
    
15. <span data-ttu-id="6596d-161">Geben Sie den Benutzernamen und das Kennwort, mit dem Sie den Server SQL Azure-Datenbank erstellt, und wählen Sie dann **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="6596d-161">Enter the user name and password you used when you created the SQL Azure Database server, then choose  **Connect**.</span></span>
    
16. <span data-ttu-id="6596d-162">Wählen Sie **Weiter**, und wählen Sie **Fertig stellen**, und warten Sie, bis die Datenbank erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="6596d-162">Choose  **Next**, and then choose  **Finish**, and wait until the database is created.</span></span> <span data-ttu-id="6596d-163">Nachdem er erstellt wurde, wählen Sie **Schließen** , um den Assistenten zu schließen.</span><span class="sxs-lookup"><span data-stu-id="6596d-163">After it is created, choose  **Close** to close the wizard.</span></span>
    
17. <span data-ttu-id="6596d-164">Geben Sie an der Azure-Verwaltungsportal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)), stellen Sie sicher, dass die Nordwind-Datenbank erfolgreich erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="6596d-164">Return to the Azure Management Portal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)) to verify that the Northwind database was created successfully.</span></span> <span data-ttu-id="6596d-165">Sie sollte angezeigt werden, dass es auf dem Bildschirm Sql-Datenbanken aufgeführt wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-165">You should see it listed on the sql databases screen, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="6596d-166">**Abbildung 4. Übersicht über SQL Server-Datenbanken**</span><span class="sxs-lookup"><span data-stu-id="6596d-166">**Figure 4. Listing of SQL Server databases**</span></span>

    ![Zeigt eine Liste aller SQL-Datenbanken, einschließlich Nordwind (engl.)](media/036b4252-f57b-4f39-9f60-ddaa30daf23c.png)

18. <span data-ttu-id="6596d-168">Wählen Sie aus der Nordwind-Datenbank, und wählen Sie dann auf **Ansicht SQL-Datenbank-Verbindungszeichenfolgen**.</span><span class="sxs-lookup"><span data-stu-id="6596d-168">Select the Northwind database, and then select  **View SQL Database connection strings**.</span></span>
    
19. <span data-ttu-id="6596d-169">Kopieren Sie die Verbindungszeichenfolge, und fügen Sie ihn in eine Textdatei, und speichern Sie es lokal.</span><span class="sxs-lookup"><span data-stu-id="6596d-169">Copy the connection string and paste it into a text file and save it locally.</span></span> <span data-ttu-id="6596d-170">Sie werden diese Verbindungszeichenfolge später benötigen.</span><span class="sxs-lookup"><span data-stu-id="6596d-170">You will need this connection string later.</span></span> <span data-ttu-id="6596d-171">Das Dialogfeld **Verbindungszeichenfolgen** zu schließen.</span><span class="sxs-lookup"><span data-stu-id="6596d-171">Close the  **Connection Strings** dialog box.</span></span>
    
20. <span data-ttu-id="6596d-172">Wählen Sie den Link zum **Einrichten von Windows Azure-Firewall-Regeln für diese IP-Adresse** , und fügen Sie Ihre IP-Adresse den Firewall-Regeln, die Zugriff auf die Datenbank zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="6596d-172">Choose the  **Set up Windows Azure firewall rules for this IP address** link and add your IP address to the firewall rules to allow you to access the database.</span></span>
    
21. <span data-ttu-id="6596d-173">Öffnen Sie das Core.DataStorageModels.sln-Projekt in Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6596d-173">Open the Core.DataStorageModels.sln project in Visual Studio 2013.</span></span>
    
22. <span data-ttu-id="6596d-174">Suchen Sie im Visual Studio- **Projektmappen-Explorer**die Datei "Web.config".</span><span class="sxs-lookup"><span data-stu-id="6596d-174">In the Visual Studio **Solution Explorer**, locate the Web.config file.</span></span>
    
23. <span data-ttu-id="6596d-175">Suchen Sie in der Datei Web.config hinzufügen `name="NorthWindEntities"` Element, und ersetzen den vorhandenen ConnectionString-Wert mit der Verbindungszeichenfolge, die Sie in Schritt 19 lokal gespeichert.</span><span class="sxs-lookup"><span data-stu-id="6596d-175">In the Web.config file, locate the add  `name="NorthWindEntities"` element and replace the existing connectionString value with the connection string information that you saved locally in step 19.</span></span> 
    
    ```XML
      <add name="NorthWindEntities" connectionString="metadata=res://*/Northwind.csdl|res://*/Northwind.ssdl|res://*/Northwind.msl;provider=System.Data.SqlClient;provider connection string=&amp;quot;data source=<Your Server Here>.database.windows.net;initial catalog=NorthWind;user id=<Your Username Here>@<Your Server Here>;password=<Your Password Here>;MultipleActiveResultSets=True;App=EntityFramework&amp;quot;" providerName="System.Data.EntityClient" />
    ```
24. <span data-ttu-id="6596d-176">Speichern Sie die Datei "Web.config".</span><span class="sxs-lookup"><span data-stu-id="6596d-176">Save the Web.config file.</span></span>

## <a name="sharepoint-list-on-the-app-web-notes-scenario"></a><span data-ttu-id="6596d-177">SharePoint-Liste im Web app (Notes Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-177">SharePoint list on the app web (Notes scenario)</span></span>
<span data-ttu-id="6596d-178"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-178"></span></span>

<span data-ttu-id="6596d-179">Das Notes Liste Szenario, das in einer SharePoint-Liste für eine app-Website verwendet wird, zeigt, wie Listen in einer SharePoint-app-Web ausführen.</span><span class="sxs-lookup"><span data-stu-id="6596d-179">The Notes list scenario, which uses a SharePoint list on an app web, shows how lists perform in a SharePoint app web.</span></span> <span data-ttu-id="6596d-180">In der app-Website mit einem Feld Titel und Beschreibung wird die Liste Notizen erstellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-180">The Notes list is created in the app web with a title and description field.</span></span> <span data-ttu-id="6596d-181">Die SharePoint-REST-API führt eine Abfrage die Liste Notizen und gibt alle Notizen basierend auf eine Kunden-ID</span><span class="sxs-lookup"><span data-stu-id="6596d-181">The SharePoint REST API queries the Notes list and returns all the notes based on a customer ID.</span></span>

<span data-ttu-id="6596d-182">Von Listen im Web app hat eine wichtige Vorteil gegenüber der anderen Speicher Lösungen: Sie können einfache SharePoint REST-API-Aufrufe zum Abfragen von Daten verwenden.</span><span class="sxs-lookup"><span data-stu-id="6596d-182">Using lists in the app web has one important advantage over other storage solutions: you can use simple SharePoint REST API calls to query data.</span></span> <span data-ttu-id="6596d-183">Es gibt jedoch auch einige Nachteile:</span><span class="sxs-lookup"><span data-stu-id="6596d-183">However, there are some disadvantages:</span></span>

- <span data-ttu-id="6596d-184">Um listenmetadaten zu aktualisieren, müssen Sie aktualisieren und erneut bereitstellen die app.</span><span class="sxs-lookup"><span data-stu-id="6596d-184">To update list metadata, you must update and redeploy the app.</span></span>
    
- <span data-ttu-id="6596d-185">Um die Datenstruktur zu aktualisieren, müssen Sie die Logik für das Speichern und Aktualisieren von Daten umschreiben.</span><span class="sxs-lookup"><span data-stu-id="6596d-185">To update the data structure, you must rewrite application logic for storing and updating data.</span></span>
    
- <span data-ttu-id="6596d-186">In der Liste gespeicherten Informationen kann nicht mit anderen add-ins auf einfache Weise gemeinsam genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="6596d-186">Information stored in the list cannot be shared easily with other add-ins.</span></span>
    
- <span data-ttu-id="6596d-187">Sie können keine Daten in SharePoint suchen.</span><span class="sxs-lookup"><span data-stu-id="6596d-187">You cannot search for data in SharePoint.</span></span>
    
- <span data-ttu-id="6596d-188">Die Menge der Daten, die in Listen gespeichert werden können und die Größe des Abfrageresultsets sind beschränkt.</span><span class="sxs-lookup"><span data-stu-id="6596d-188">The amount of data that you can store in lists and the size of query result sets are limited.</span></span>
    
<span data-ttu-id="6596d-189">Der Code, der im Abschnitt "Hinweise" des Kunden Dashboards zugrunde liegt verwendet REST-Abfragen zum Abrufen von Daten aus einer Liste, die in der app-Web bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="6596d-189">The code that underlies the Notes section of the customer dashboard uses REST queries to retrieve data from a list that is deployed to the app web.</span></span> <span data-ttu-id="6596d-190">Diese Liste enthält die Felder für Titel, Autoren, Kunden-IDs und Beschreibungen.</span><span class="sxs-lookup"><span data-stu-id="6596d-190">This list contains fields for titles, authors, customer IDs, and descriptions.</span></span> <span data-ttu-id="6596d-191">Sie können die app-Schnittstelle zum Hinzufügen und Abrufen von Notizen für einen angegebenen Kunden, verwenden, wie in Abbildung 5 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-191">You can use the app's interface to add and retrieve notes for a specified customer, as shown in Figure 5.</span></span>

<span data-ttu-id="6596d-192">**Abbildung 5. Benutzeroberfläche für die Notes-app**</span><span class="sxs-lookup"><span data-stu-id="6596d-192">**Figure 5. User interface for the Notes app**</span></span>

![Ein Screenshot der Benutzeroberfläche für das Datenmodell Speicher Notizen](media/d98ce2cf-5022-4f2b-ad3e-da4eea52dfb2.png)

<span data-ttu-id="6596d-194">Der **Notizen der Ansichtsliste in App-Web** -Link bietet eine Ansicht "sofort einsatzbereit" den Listendaten.</span><span class="sxs-lookup"><span data-stu-id="6596d-194">The  **View Notes List in App Web** link provides an "out of the box" view of the list data.</span></span>

<span data-ttu-id="6596d-195">Diese app mithilfe des Model-View-Controller (MVC).</span><span class="sxs-lookup"><span data-stu-id="6596d-195">This app uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="6596d-196">Sie können den Code für das Szenario Notizen in der Datei Views/CustomerDashboard/Notes.cshtml sehen.</span><span class="sxs-lookup"><span data-stu-id="6596d-196">You can see the code for the notes scenario in the Views/CustomerDashboard/Notes.cshtml file.</span></span> <span data-ttu-id="6596d-197">Einfache REST-Aufrufen verwendet zum Hinzufügen und Abrufen von Daten.</span><span class="sxs-lookup"><span data-stu-id="6596d-197">It uses simple REST calls to add and retrieve data.</span></span> <span data-ttu-id="6596d-198">Der folgende Code ruft Notes aus der Liste Notizen für einen angegebenen Kunden.</span><span class="sxs-lookup"><span data-stu-id="6596d-198">The following code retrieves notes from the Notes list for a specified customer.</span></span>

```C#
function getNotesAndShow() {
    var executor = new SP.RequestExecutor(appWebUrl);
    executor.executeAsync(
       {
           url: appWebUrl + "/_api/web/lists/getByTitle('Notes')/items/" +
                "?$select=FTCAM_Description,Modified,Title,Author/ID,Author/Title" +
                "&amp;$expand=Author/ID,Author/Title" +
                "&amp;$filter=(Title eq '" + customerID + "')",
           type: "GET",
           dataType: 'json',
           headers: { "accept": "application/json;odata=verbose" },
           success: function (data) {
               var value = JSON.parse(data.body);
               showNotes(value.d.results);
           },
           error: function (error) { console.log(JSON.stringify(error)) }
       }

    );
}
```

<span data-ttu-id="6596d-199">Der folgende Code Fügt einen Hinweis für einen bestimmten Kunden zur Notizenliste.</span><span class="sxs-lookup"><span data-stu-id="6596d-199">The following code adds a note for a given customer to the notes list.</span></span>

```C#
function addNoteToList(note, customerID) {
    var executor = new SP.RequestExecutor(appWebUrl);
    var bodyProps = {
        '__metadata': { 'type': 'SP.Data.NotesListItem' },
        'Title': customerID,
        'FTCAM_Description': note
    };
    executor.executeAsync({
        url: appWebUrl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('Notes')/items?@target='" + appWebUrl + "'",
        contentType: "application/json;odata=verbose",
        method: "POST",
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        body: JSON.stringify(bodyProps),
        success: getNotesAndShow,
        error: addNoteFailed
    });
}
```

<span data-ttu-id="6596d-200">Sie können 5000 Elemente hinzufügen, um der Liste angezeigt wird, dass die Liste Abfragen, die ein Ergebnis Generieren von 5000 oder mehr Elemente erreicht den Schwellenwert für die Abfrage werden und ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="6596d-200">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="6596d-201">Sie können auch große Menge an Daten hinzufügen, Ihrer Liste der app-Web, dass den Speichergrenzwert für Ihre Websitesammlung überschritten (hängt wie viel Speicher Sie darauf zugewiesen haben).</span><span class="sxs-lookup"><span data-stu-id="6596d-201">You can also add so much data to your list on the app web that you exceed the storage limit for your site collection (which depends on how much storage space you've allocated to it).</span></span> <span data-ttu-id="6596d-202">Diese Szenarien zeigen zwei die wichtigsten Nachteile dieses Ansatzes: Abfrage größenbeschränkungen für Nachrichten und Speicherplatz Speichergrenzwerte aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="6596d-202">These scenarios show two of the most important limitations of this approach: list query size limits and storage space limits.</span></span> <span data-ttu-id="6596d-203">Wenn Ihr Unternehmen Ihnen das Arbeiten mit großen Datenmengen und Abfrageresultsets notwendig ist, funktioniert diese Vorgehensweise nicht.</span><span class="sxs-lookup"><span data-stu-id="6596d-203">If your business needs require you to work with large data sets and query result sets, this approach won't work.</span></span>

### <a name="list-query-threshold"></a><span data-ttu-id="6596d-204">Schwellenwert für die Liste Abfrage</span><span class="sxs-lookup"><span data-stu-id="6596d-204">List query threshold</span></span>
<span data-ttu-id="6596d-205"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-205"></span></span>

<span data-ttu-id="6596d-206">So laden Sie genügend Daten, um die Liste Abfrage Schwellenwert überschritten:</span><span class="sxs-lookup"><span data-stu-id="6596d-206">To load enough data to exceed the list query threshold limit:</span></span>


1. <span data-ttu-id="6596d-207">Wählen Sie im linken Menü **Beispiel-Homepage**.</span><span class="sxs-lookup"><span data-stu-id="6596d-207">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="6596d-208">Wählen Sie im Abschnitt **Liste Abfrage Schwellenwerte** **Hinzufügen Listenelemente in der Liste Notizen im App-Web**.</span><span class="sxs-lookup"><span data-stu-id="6596d-208">In the  **List Query Thresholds** section, choose **Add list items to the Notes list in the App Web**.</span></span>
    
3. <span data-ttu-id="6596d-209">Pro die Anweisungen, die über der Schaltfläche angezeigt werden, führen Sie diesen Vorgang 10-Mal.</span><span class="sxs-lookup"><span data-stu-id="6596d-209">Per the instructions that appear above the button, perform this operation 10 times.</span></span>
    
    <span data-ttu-id="6596d-210">Bei der Aktualisierung der Liste Notizen am oberen Rand der Seite, die angibt, wie viele Listenelemente (Notes) Sie hinzugefügt haben, wird eine Meldung angezeigt, und wie viele sind Links, um Sie hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6596d-210">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    <span data-ttu-id="6596d-211">**Hinweis**  Der Vorgang dauert ungefähr einer Minute jedes Mal ausgeführt werden, den Sie die Schaltfläche auswählen.</span><span class="sxs-lookup"><span data-stu-id="6596d-211">**Note**  The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="6596d-212">Ausführen des Vorgangs: 10-Mal Ergebnis wird in Abbildung 6 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-212">The end result of running the operation 10 times is shown in Figure 6.</span></span>
4. <span data-ttu-id="6596d-213">Nachdem Sie die Liste 5,001 Elemente hinzugefügt haben, wählen Sie im linken Menü Notizen.</span><span class="sxs-lookup"><span data-stu-id="6596d-213">After you've added 5,001 items to the list, choose Notes in the left menu.</span></span> <span data-ttu-id="6596d-214">Beim Laden der Seite sehen Sie die Fehlermeldung, die in Abbildung 6, die anhand der SharePoint-REST-API wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-214">When the page loads, you will see the error message shown in Figure 6, which comes from the SharePoint REST API.</span></span>
    
    <span data-ttu-id="6596d-215">**Abbildung 6. Liste Abfrage Thresold Fehlermeldung überschritten**</span><span class="sxs-lookup"><span data-stu-id="6596d-215">**Figure 6. List query thresold exceeded error message**</span></span>

    ![Ein Screenshot, der eine Fehlermeldung, die besagt anzeigt, dass der Vorgang der Liste Ansicht Threshol überschritten.](media/90202b64-4b14-4764-9a4c-8fb236f8d10b.png)

5. <span data-ttu-id="6596d-217">Wählen Sie **Ansicht Notizenliste im App-Web** und Seite durch die Liste zu sehen, dass sie 500 Zeilen enthält.</span><span class="sxs-lookup"><span data-stu-id="6596d-217">Choose  **View Notes List in App Web** and page through the list to see that it includes 500 rows.</span></span> <span data-ttu-id="6596d-218">Beachten Sie, dass zwar SharePoint-Listenansichten Durchsuchen dieses viele Einträge aufnehmen können, die REST-API aufgrund der Drosselung Schwellenwert Listenabfrage fällt aus.</span><span class="sxs-lookup"><span data-stu-id="6596d-218">Note that although SharePoint list views can accommodate browsing of this many entries, the REST API fails due to the list query throttling threshold.</span></span>
    
### <a name="data-storage-limit"></a><span data-ttu-id="6596d-219">Speichergrenzwert Daten</span><span class="sxs-lookup"><span data-stu-id="6596d-219">Data storage limit</span></span>
<span data-ttu-id="6596d-220"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-220"></span></span>

<span data-ttu-id="6596d-221">So laden Sie genügend Daten, um die Speichergrenzwerte für Daten überschritten:</span><span class="sxs-lookup"><span data-stu-id="6596d-221">To load enough data to exceed the data storage limit:</span></span>

1. <span data-ttu-id="6596d-222">Wählen Sie im linken Menü **Beispiel-Homepage**.</span><span class="sxs-lookup"><span data-stu-id="6596d-222">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="6596d-223">Wählen Sie der Schwellenwert für die Daten im Abschnitt **die Liste App-Web-Notizen mit 1 GB Daten zu füllen**.</span><span class="sxs-lookup"><span data-stu-id="6596d-223">In the Data Threshold section, choose  **Fill the App Web Notes list with 1GB of data**.</span></span>
    
3. <span data-ttu-id="6596d-224">Pro die Anweisungen, die über der Schaltfläche zum **Auffüllen der Liste App-Web-Notizen mit 1 GB Daten** angezeigt werden, führen Sie diesen Vorgang 11 Mal.</span><span class="sxs-lookup"><span data-stu-id="6596d-224">Per the instructions that appear above the  **Fill the App Web Notes list with 1GB of data** button, perform this operation 11 times.</span></span>
    
    <span data-ttu-id="6596d-225">Bei der Aktualisierung der Liste Notizen am oberen Rand der Seite, die angibt, wie viele Listenelemente (Notes) Sie hinzugefügt haben, wird eine Meldung angezeigt, und wie viele sind Links, um Sie hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6596d-225">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    <span data-ttu-id="6596d-226">**Hinweis**  Der Vorgang dauert ungefähr einer Minute jedes Mal ausgeführt werden, den Sie die Schaltfläche auswählen.</span><span class="sxs-lookup"><span data-stu-id="6596d-226">**Note**  The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="6596d-227">Ausführen des Vorgangs 11 Mal Ergebnis wird in Abbildung 7 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-227">The end result of running the operation 11 times is shown in Figure 7.</span></span>
4. <span data-ttu-id="6596d-228">Nach dem Ausführen dieses Vorgangs 11 Mal eine Fehlermeldung tritt auf, wenn Sie die Schaltfläche auswählen wie in Abbildung 7 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-228">After you perform the operation 11 times, an error message will occur when you choose the button, as shown in Figure 7.</span></span>
    
    <span data-ttu-id="6596d-229">**Abbildung 7. Data Storage Schwellenwert überschritten-Fehlermeldung**</span><span class="sxs-lookup"><span data-stu-id="6596d-229">**Figure 7. Data storage threshold exceeded error message**</span></span>

    ![Ein Screenshot, der die Fehlermeldung angezeigt, die tritt auf, wenn die Daten überschritten wird](media/0bc55483-0ee1-487a-ba34-e827ec47aadd.png)

5. <span data-ttu-id="6596d-231">Nachdem Sie den Speichergrenzwert Daten überschreiten, wählen Sie im Webbrowser die zurück-Schaltfläche, und wählen Sie dann den **Notizen** Link im linken Menü.</span><span class="sxs-lookup"><span data-stu-id="6596d-231">After you exceed the data storage limit, choose the back button in the web browser, and then choose the  **Notes** link in the left menu.</span></span>
    
6. <span data-ttu-id="6596d-232">Wählen Sie **Ansicht Notizenliste im App-Web**.</span><span class="sxs-lookup"><span data-stu-id="6596d-232">Choose  **View Notes List in App Web**.</span></span>
    
    <span data-ttu-id="6596d-233">Beim Laden der Seite wird am oberen Rand der Seite, die angibt, dass die Website nicht genügend freier Speicherplatz ist eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-233">When the page loads, an error message appears at the top of the page that indicates that the site is out of storage space.</span></span>

## <a name="sharepoint-list-on-the-host-web-support-cases-scenario"></a><span data-ttu-id="6596d-234">SharePoint-Liste auf dem hostweb (Support-Anfragen Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-234">SharePoint list on the host web (Support Cases scenario)</span></span>
<span data-ttu-id="6596d-235"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-235"></span></span>

<span data-ttu-id="6596d-236">Das Support-Anfragen Szenario zeigt Daten, die in einer SharePoint-Liste im hostweb gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="6596d-236">The Support Cases scenario displays data that is stored in a SharePoint list in the host web.</span></span> <span data-ttu-id="6596d-237">In diesem Szenario werden zwei unterschiedliche Muster und interagieren mit den Daten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="6596d-237">This scenario uses two different patterns to access and interact with the data.</span></span> <span data-ttu-id="6596d-238">Das erste Muster enthält den SharePoint-Suchdienst, und die vom Inhaltssuche mit einer benutzerdefinierten Anzeigevorlage angewendet.</span><span class="sxs-lookup"><span data-stu-id="6596d-238">The first pattern includes the SharePoint Search Service and the Content By Search Web Part with a custom Display Template applied.</span></span> <span data-ttu-id="6596d-239">Das zweite Muster enthält ein App-Webpart (Clientwebpart), die eine MVC-Ansicht angezeigt wird, die die **SP verwendet wird RequestExecutor** -Klasse, um die SharePoint-REST-API-aufrufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-239">The second pattern includes an App Part (Client Web Part) that displays an MVC view, which uses the  **SP.RequestExecutor** class to call the SharePoint REST API.</span></span>

<span data-ttu-id="6596d-240">Es gibt mehrere Vorteile der Verwendung von diesem Ansatz:</span><span class="sxs-lookup"><span data-stu-id="6596d-240">There are several advantages to using this approach:</span></span>

- <span data-ttu-id="6596d-241">Sie können Daten auf einfache Weise mit einfachen REST-Abfragen oder Client-Objektmodellcode Abfragen.</span><span class="sxs-lookup"><span data-stu-id="6596d-241">You can query data easily using simple REST queries or client object model code.</span></span>
    
- <span data-ttu-id="6596d-242">Sie können nach Daten in SharePoint suchen.</span><span class="sxs-lookup"><span data-stu-id="6596d-242">You can search for data in SharePoint.</span></span>
    
- <span data-ttu-id="6596d-243">Sie können aktualisieren Sie die listenmetadaten und neue Ansichten für eine Liste erstellen, ohne zu aktualisieren und erneutes Bereitstellen der app.</span><span class="sxs-lookup"><span data-stu-id="6596d-243">You can update the list metadata and create new views for a list without updating and redeploying the app.</span></span> <span data-ttu-id="6596d-244">Diese Änderungen werden nicht beeinflusst das Verhalten Ihrer App.</span><span class="sxs-lookup"><span data-stu-id="6596d-244">These changes won't affect the behavior of your app.</span></span>
    
- <span data-ttu-id="6596d-245">Listen auf der Hostwebsite werden nicht gelöscht, wenn Sie Ihre app zu deinstallieren, wenn die app das **AppUninstalled** -Ereignis verwendet, um der Liste entfernen und/oder Löschen der Daten.</span><span class="sxs-lookup"><span data-stu-id="6596d-245">Lists on the host web are not deleted when you uninstall your app, unless the app uses the  **AppUninstalled** event to remove the list and/or delete the data.</span></span>
    
<span data-ttu-id="6596d-246">Versetzen diese Vorteile sind die folgenden Nachteile:</span><span class="sxs-lookup"><span data-stu-id="6596d-246">Offsetting these advantages are the following disadvantages:</span></span>

- <span data-ttu-id="6596d-247">Die Hostwebsite beschränkt die Datenmenge, die in Listen gespeichert werden können, und die Größe der Ergebnisse der Abfrage.</span><span class="sxs-lookup"><span data-stu-id="6596d-247">The host web limits both the amount of data you can store in lists and the size of the query results.</span></span> <span data-ttu-id="6596d-248">Wenn Ihr Unternehmen benötigt gespeichert und/oder Abfragen großen Datasets, ist dies kein empfohlener Ansatz.</span><span class="sxs-lookup"><span data-stu-id="6596d-248">If your business needs require storing and/or querying large data sets, this is not a recommended approach.</span></span>
    
- <span data-ttu-id="6596d-249">Für komplexe Abfragen führen Listen sowie Datenbanken nicht aus.</span><span class="sxs-lookup"><span data-stu-id="6596d-249">For complex queries, lists do not perform as well as databases.</span></span>
    
- <span data-ttu-id="6596d-250">Zum Sichern und Wiederherstellen von Daten, führen Sie Listen sowie Datenbanken nicht aus.</span><span class="sxs-lookup"><span data-stu-id="6596d-250">For backing up and restoring data, lists do not perform as well as databases.</span></span>
    
<span data-ttu-id="6596d-251">Die Daten für dieses Szenario werden in einer SharePoint-Liste bereitgestellt, mit der Hostwebsite gespeichert.</span><span class="sxs-lookup"><span data-stu-id="6596d-251">The data for this scenario is stored in a SharePoint list deployed to the host web.</span></span> <span data-ttu-id="6596d-252">Daten abgerufen und mithilfe der folgenden angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6596d-252">Data is retrieved and displayed by means of the following:</span></span> 

- <span data-ttu-id="6596d-253">Ein [Inhaltssuche-Webpart](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6596d-253">A  [Content Search Web Part](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span></span>
    
- <span data-ttu-id="6596d-254">Ein app-Webpart, das als Model-View-Controller Ansicht implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="6596d-254">An app part that's implemented as a model-view-controller view.</span></span> 
    
<span data-ttu-id="6596d-255">Der Code in dieser Ansicht verwendet REST-Abfragen zum Abrufen von Informationen aus der Liste, während das Inhaltssuche-Webpart den SharePoint-Suchdienst verwendet, um die Daten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-255">The code in this view uses REST queries to retrieve information from the list, while the content search web part uses the SharePoint search service to retrieve the data.</span></span> <span data-ttu-id="6596d-256">Die zwei Ansätze veranschaulichen den bedeutenden Vorteil dieser Option: Sie können den Suchdienst und den REST/CSOM-APIs verwenden, um Informationen aus einer Liste auf dem hostweb abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-256">The two approaches demonstrate the significant advantage of this option: you can use both the search service and the REST/CSOM APIs to retrieve information from a list on the host web.</span></span>

<span data-ttu-id="6596d-257">Wenn Sie einen Kunden aus der Unterstützung von Fällen Dropdown-Liste auswählen, sehen Sie die Groß-/Kleinschreibung Support-Daten für dieses Kunden anzeigen in das Webpart und das app-Webpart (Abbildung 8) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-257">When you select a customer from the support cases drop-down, you'll see the support case data for that customer displayed in both the web part and the app part (Figure 8).</span></span> <span data-ttu-id="6596d-258">Das Webpart möglicherweise nicht sofort, Inhalte zurück, da bis zu 24 Stunden für den SharePoint-Suchdienst dauert, die Daten zu indizieren.</span><span class="sxs-lookup"><span data-stu-id="6596d-258">The web part might not return content right away, because it can take up to 24 hours for the SharePoint search service to index the data.</span></span> <span data-ttu-id="6596d-259">Sie können auch den Link **Ansicht Support Fällen Liste im Hostweb** um eine herkömmliche Ansicht der Listendaten anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6596d-259">You can also choose the  **View Support Cases List in Host Web** link to see a conventional view of the list data.</span></span>

<span data-ttu-id="6596d-260">**Abbildung 8. Benutzeroberfläche für den Support-Fall**</span><span class="sxs-lookup"><span data-stu-id="6596d-260">**Figure 8. User interface for the support case scenario**</span></span>

![Ein Screenshot der Benutzeroberfläche für die Interaktion mit den Support-Fall](media/eac41f5c-90b7-4fe3-b47e-0d65b79cbf1c.png)

<span data-ttu-id="6596d-262">Das Inhaltssuche-Webpart bereitgestellt, die diese App verwendet eine benutzerdefinierte Anzeige-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="6596d-262">The content search web part deployed by this app uses a custom display template.</span></span> <span data-ttu-id="6596d-263">Abbildung 9 zeigt im Verzeichnis **Anlagen** des Webprojekts finden Sie auf das Webpart und die zugeordnete Vorlage.</span><span class="sxs-lookup"><span data-stu-id="6596d-263">Figure 9 shows where in the  **Assets** directory of the web project you can find the web part and the associated template.</span></span>

<span data-ttu-id="6596d-264">**Abbildung 9. Inhalt des Verzeichnisses Anlagen des Webprojekts**</span><span class="sxs-lookup"><span data-stu-id="6596d-264">**Figure 9. Contents of the Assets directory of the web project**</span></span>

![Screenshot des Verzeichnisses Objekte](media/95db9118-9e56-4e39-84b1-271e54447792.png)

<span data-ttu-id="6596d-266">Der folgende JavaScript-Code, den finden Sie in der Datei Views/SupportCaseAppPart\Index.cshtml mithilfe die domänenübergreifenden Bibliothek eine REST-Abfrage für die SharePoint-Liste auf dem hostweb aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-266">The following JavaScript code that you'll find in the Views/SupportCaseAppPart\Index.cshtml file uses the cross-domain library to invoke a REST query on the SharePoint list on the host web.</span></span> 

```C#
function execCrossDomainRequest() {
var executor = new SP.RequestExecutor(appWebUrl);

executor.executeAsync(
   {
        url: appWebUrl + "/_api/SP.AppContextSite(@@target)" +
                "/web/lists/getbytitle('Support Cases')/items" +
              "?$filter=(FTCAM_CustomerID eq '" + customerID + "')" +
            "&amp;$top=30" +
                    "&amp;$select=Id,Title,FTCAM_Status,FTCAM_CSR" +
                    "&amp;@@target='" + hostWebUrl + "'",
method: "GET",
              headers: { "Accept": "application/json; odata=verbose" },
              success: successHandler,
              error: errorHandler
   }
);
}
```

<span data-ttu-id="6596d-267">Sie können 5000 Elemente hinzufügen, um der Liste angezeigt wird, dass die Liste Abfragen, die ein Ergebnis Generieren von 5000 oder mehr Elemente erreicht den Schwellenwert für die Abfrage werden und ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="6596d-267">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="6596d-268">In diesem Szenario wird ein wichtigste Nachteil dieser Vorgehensweise: Auflisten der Abfrage größenbeschränkungen für Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="6596d-268">This scenario shows one of the most important limitations of this approach: list query size limits.</span></span> <span data-ttu-id="6596d-269">Wenn Ihr Unternehmen Ihnen das Arbeiten mit großen Datenmengen und Abfrageresultsets notwendig ist, funktioniert diese Vorgehensweise nicht.</span><span class="sxs-lookup"><span data-stu-id="6596d-269">If your business needs require you to work with large data and query result sets, this approach won't work.</span></span> <span data-ttu-id="6596d-270">Weitere Informationen finden Sie unter [Liste Abfrage Schwellenwert](#bk_listquerythreshold) weiter oben in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="6596d-270">For more information, see  [List query threshold](#bk_listquerythreshold) earlier in this article.</span></span>

## <a name="northwind-odata-web-service-customer-dashboard-scenario"></a><span data-ttu-id="6596d-271">Northwind-OData-Webdienst (Kunden-Dashboard Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-271">Northwind OData web service (Customer Dashboard scenario)</span></span>
<span data-ttu-id="6596d-272"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-272"></span></span>

<span data-ttu-id="6596d-273">Das Kunden-Dashboard-Szenario wird JQuery AJAX zum Aufrufen des NorthWind OData-Diensts zum Zurückgeben von Kundeninformationen verwendet.</span><span class="sxs-lookup"><span data-stu-id="6596d-273">The Customer Dashboard scenario uses JQuery AJAX to invoke the NorthWind OData service to return customer information.</span></span> <span data-ttu-id="6596d-274">Die app speichert seine Daten in einem Webdienst, und klicken Sie dann [OData](http://www.odata.org/) verwendet, um es abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-274">The app stores its data in a web service, then uses  [OData](http://www.odata.org/) to retrieve it.</span></span>

<span data-ttu-id="6596d-275">Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:</span><span class="sxs-lookup"><span data-stu-id="6596d-275">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="6596d-276">Ein bestimmten Webdienst kann mehrere Add-Ins unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6596d-276">A given web service can support multiple add-ins.</span></span>
    
- <span data-ttu-id="6596d-277">Sie können den Webdienst aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.</span><span class="sxs-lookup"><span data-stu-id="6596d-277">You can update your web service without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="6596d-278">Ihre SharePoint und Web-Service-Installationen wirken sich nicht voneinander.</span><span class="sxs-lookup"><span data-stu-id="6596d-278">Your SharePoint and web service installations do not affect one another.</span></span>
    
- <span data-ttu-id="6596d-279">Hosten Dienste, wie Microsoft Azure ermöglichen es Ihnen, die Webdienste zu skalieren.</span><span class="sxs-lookup"><span data-stu-id="6596d-279">Hosting services such as Microsoft Azure enable you to scale your web services.</span></span>
    
- <span data-ttu-id="6596d-280">Sie können sichern und Wiederherstellen von Informationen auf Ihre Webdienste separat aus Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="6596d-280">You can back up and restore information on your web services separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="6596d-281">Sie verloren nicht Daten, wenn Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.</span><span class="sxs-lookup"><span data-stu-id="6596d-281">You don't lose data when uninstalling your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="6596d-282">Dashboard Kundenszenarien speichert seine Daten in einem Webdienst, der zum Abrufen der Daten des OData-Standards implementiert.</span><span class="sxs-lookup"><span data-stu-id="6596d-282">The customer dashboard scenario stores its data in a web service that implements the OData standard to retrieve data.</span></span> <span data-ttu-id="6596d-283">In der Benutzeroberfläche des Kunden-Dashboard wählen Sie einen Kunden aus einem Dropdown-Menü und Informationen Kundenanzeige im Bereich **Kundeninformationen** .</span><span class="sxs-lookup"><span data-stu-id="6596d-283">In the customer dashboard interface, you select a customer from a drop-down menu, and customer information displays in the  **Customer Info** pane.</span></span>

<span data-ttu-id="6596d-284">Auf dieser Seite Benutzeroberfläche ist eine Model-View-Controller-Ansicht.</span><span class="sxs-lookup"><span data-stu-id="6596d-284">This UI page is a Model-View-Controller view.</span></span> <span data-ttu-id="6596d-285">Die Anzeige wird in der Datei Views/CustomerDashboard\Home.cshtml definiert.</span><span class="sxs-lookup"><span data-stu-id="6596d-285">The display is defined in the Views/CustomerDashboard\Home.cshtml file.</span></span> <span data-ttu-id="6596d-286">Der zugrunde liegende Code ist in der Datei Scripts/CustomerDashboard.js.</span><span class="sxs-lookup"><span data-stu-id="6596d-286">The underlying code is in the Scripts/CustomerDashboard.js file.</span></span> <span data-ttu-id="6596d-287">Der JavaScript-Code verwendet AJAX, um die Northwind-Webdienst abzufragen.</span><span class="sxs-lookup"><span data-stu-id="6596d-287">The JavaScript code uses AJAX to query the Northwind web service.</span></span> <span data-ttu-id="6596d-288">Da dies ein OData-Dienst ist, besteht aus den Webdienstabfrage Abfragezeichenfolgenargumente, eine URL für einen Webdienst-Endpunkt zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="6596d-288">Because this is an OData service, the web service query consists of query string arguments attached to a URL that points to a web service endpoint.</span></span> <span data-ttu-id="6596d-289">Der Dienst gibt Kundeninformationen im JSON-Format zurück.</span><span class="sxs-lookup"><span data-stu-id="6596d-289">The service returns customer information in JSON format.</span></span>

<span data-ttu-id="6596d-290">Mit dem folgende Code wird ausgeführt, wenn Sie den Link **Kunden-Dashboard** auswählen.</span><span class="sxs-lookup"><span data-stu-id="6596d-290">The following code runs when you choose the  **Customer Dashboard** link.</span></span> <span data-ttu-id="6596d-291">Die Namen der Kunden und IDs, um das Dropdown-Menü Auffüllen abgerufen.</span><span class="sxs-lookup"><span data-stu-id="6596d-291">It retrieves all the customer names and IDs in order to populate the drop-down menu.</span></span>

```C#
var getCustomerIDsUrl = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json&amp;$select=CustomerID";
    $.get(getCustomerIDsUrl).done(getCustomerIDsDone)
        .error(function (jqXHR, textStatus, errorThrown) {
            $('#topErrorMessage').text('Can\'t get customers. An error occurred: ' + jqXHR.statusText);
        });
```

<span data-ttu-id="6596d-292">Mit dem folgende Code wird ausgeführt, wenn Sie einen Kundennamen aus dem Dropdown-Menü auswählen.</span><span class="sxs-lookup"><span data-stu-id="6596d-292">The following code runs when you select a customer name from the drop-down menu.</span></span> <span data-ttu-id="6596d-293">Das OData **$filter** -Argument verwendet, um die Kunden-ID und andere Abfragezeichenfolgenargumente zum Abrufen von Informationen im Zusammenhang mit diesen Kunden angeben.</span><span class="sxs-lookup"><span data-stu-id="6596d-293">It uses the OData  **$filter** argument to specify the customer ID and other query string arguments to retrieve information related to this customer.</span></span>

```C#
var url = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json" +  "&amp;$select=CustomerID,CompanyName,ContactName,ContactTitle,Address,City,Country,Phone,Fax" + "&amp;$filter=CustomerID eq '" + customerID + "'";

$.get(url).done(getCustomersDone)
   .error(function (jqXHR, textStatus, errorThrown) {
          alert('Can\'t get customer ' + customerID + '. An error occurred: ' + 
                 jqXHR.statusText);
});
```

## <a name="azure-table-storage-customer-service-survey-scenario"></a><span data-ttu-id="6596d-294">Azure-tabellenspeicherung (Customer Service Umfrage Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-294">Azure table storage (Customer Service Survey scenario)</span></span>
<span data-ttu-id="6596d-295"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-295"></span></span>

<span data-ttu-id="6596d-296">Das Dienst Umfrage Szenario ermöglicht dem Kunden Mitarbeiter zu ihrer Bewertung basierend auf Kundenumfragen finden Sie unter und Azure-tabellenspeicherung und der Microsoft.WindowsAzure.Storage.Table.CloudTable-API zum Speichern und interagieren mit den Daten verwendet.</span><span class="sxs-lookup"><span data-stu-id="6596d-296">The Customer Service Survey scenario allows a customer service representative to see their rating based on customer surveys and uses Azure table storage and the Microsoft.WindowsAzure.Storage.Table.CloudTable API to store and interact with the data.</span></span>

<span data-ttu-id="6596d-297">Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:</span><span class="sxs-lookup"><span data-stu-id="6596d-297">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="6596d-298">Azure-Speichertabellen unterstützen mehr als eine app.</span><span class="sxs-lookup"><span data-stu-id="6596d-298">Azure storage tables support more than one app.</span></span>
    
- <span data-ttu-id="6596d-299">Sie können die Azure-Speichertabellen aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.</span><span class="sxs-lookup"><span data-stu-id="6596d-299">You can update Azure storage tables without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="6596d-300">Ihre SharePoint-Installation und Azure-Speichertabellen haben keine Auswirkung auf die Leistung des jeweils anderen.</span><span class="sxs-lookup"><span data-stu-id="6596d-300">Your SharePoint installation and Azure storage tables have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="6596d-301">Azure-Speicher Tabellen horizontal ganz einfach.</span><span class="sxs-lookup"><span data-stu-id="6596d-301">Azure storage tables scale easily.</span></span>
    
- <span data-ttu-id="6596d-302">Sie können sichern und Wiederherstellen die Azure-Speichertabellen separat von Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="6596d-302">You can back up and restore your Azure storage tables separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="6596d-303">Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.</span><span class="sxs-lookup"><span data-stu-id="6596d-303">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="6596d-304">Die app-Schnittstelle des aktuellen Benutzers Umfrage Bewertung in der Center-Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-304">The app's interface displays the current user's survey rating in the center page.</span></span> <span data-ttu-id="6596d-305">Wenn die Azure-Speicher-Tabelle leer ist, wird die app einige Informationen zur Tabelle hinzufügen, bevor es angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-305">If that Azure storage table is empty, the app will add some information to the table before it displays it.</span></span>

<span data-ttu-id="6596d-306">Der folgende Code aus der CSRInfoController.cs definiert die **Start** -Methode, die der Benutzer **NameId**abruft.</span><span class="sxs-lookup"><span data-stu-id="6596d-306">The following code from the CSRInfoController.cs defines the  **Home** method that retrieves the user's **nameId**.</span></span>

```C#
[SharePointContextFilter]
public ActionResult Home()
{
    var context = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);
    var sharePointService = new SharePointService(context);
    var currentUser = sharePointService.GetCurrentUser();
    ViewBag.UserName = currentUser.Title;

    var surveyRatingsService = new SurveyRatingsService();
    ViewBag.Score = surveyRatingsService.GetUserScore(currentUser.UserId.NameId);

    return View();
}
```

<span data-ttu-id="6596d-307">Der folgende Code aus der Datei SurveyRatingService.cs definiert den **SurveyRatingsService** -Konstruktor Einrichten der Verbindung mit dem Azure-Speicher-Konto festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6596d-307">The following code from the SurveyRatingService.cs file defines the  **SurveyRatingsService** constructor, which sets up the connection to the Azure storage account.</span></span>

```C#
public SurveyRatingsService(string storageConnectionStringConfigName = 
        "StorageConnectionString")
{
    var connectionString = Util.GetConfigSetting("StorageConnectionString");
    var storageAccount = CloudStorageAccount.Parse(connectionString);

    this.tableClient = storageAccount.CreateCloudTableClient();
    this.surveyRatingsTable = this.tableClient.GetTableReference("SurveyRatings");
    this.surveyRatingsTable.CreateIfNotExists();
}
```

<span data-ttu-id="6596d-308">Der folgende Code aus der gleichen Datei definiert die **GetUserScore** -Methode, die aus der Tabelle Azure-Speicher des Benutzers Umfrage Score abruft.</span><span class="sxs-lookup"><span data-stu-id="6596d-308">The following code from the same file defines the  **GetUserScore** method, which retrieves the user's survey score from the Azure storage table.</span></span>

```C#
public float GetUserScore(string userName)
{
    var query = new TableQuery<Models.Customer>()
    .Select(new List<string> { "Score" })
    .Where(TableQuery.GenerateFilterCondition("Name", 
    QueryComparisons.Equal, userName));

    var items = surveyRatingsTable
         .ExecuteQuery(query)
             .ToArray();

    if (items.Length == 0)           
    return AddSurveyRatings(userName);

    return (float)items.Average(c => c.Score);
}
```

<span data-ttu-id="6596d-309">Wenn die Tabelle keine Umfragedaten im Zusammenhang mit den aktuellen Benutzer enthält, weist die **AddSurveyRating** -Methode nach dem Zufallsprinzip eine Bewertung für den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="6596d-309">If the table doesn't contain any survey data related to the current user, the  **AddSurveyRating** method randomly assigns a score for the user.</span></span>

```C#
private float AddSurveyRatings(string userName)
{
    float sum = 0;
    int count = 4;
    var random = new Random();

    for (int i = 0; i < count; i++)
    {
    var score = random.Next(80, 100);
    var customer = new Models.Customer(Guid.NewGuid(), userName, score);

    var insertOperation = TableOperation.Insert(customer);
    surveyRatingsTable.Execute(insertOperation);

    sum += score;
    }
    return sum / count;
}
```

## <a name="azure-queue-storage-customer-call-queue-scenario"></a><span data-ttu-id="6596d-310">Azure Warteschlangenspeicher (Customer aufrufen Warteschlange Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-310">Azure queue storage (Customer Call Queue scenario)</span></span>
<span data-ttu-id="6596d-311"><a name="sectionSection5"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-311"></span></span>

<span data-ttu-id="6596d-312">Das Szenario Customer aufrufen Warteschlange aufgelistet Anrufer in der Warteschlange Support und simuliert Nachrichtenempfang Anrufe.</span><span class="sxs-lookup"><span data-stu-id="6596d-312">The Customer Call Queue scenario lists callers in the support queue and simulates taking calls.</span></span> <span data-ttu-id="6596d-313">Das Szenario wird Warteschlangen Azure-Speicher zum Speichern von Daten und die **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API mit Model-View-Controller verwendet.</span><span class="sxs-lookup"><span data-stu-id="6596d-313">The scenario uses Azure storage queues to store data and the  **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API with Model-View-Controller.</span></span>

<span data-ttu-id="6596d-314">Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:</span><span class="sxs-lookup"><span data-stu-id="6596d-314">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="6596d-315">Azure-Speicher Warteschlangen unterstützen mehr als eine app.</span><span class="sxs-lookup"><span data-stu-id="6596d-315">Azure storage queues support more than one app.</span></span>
    
- <span data-ttu-id="6596d-316">Sie können die Warteschlangen Azure-Speicher aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.</span><span class="sxs-lookup"><span data-stu-id="6596d-316">You can update Azure storage queues without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="6596d-317">Ihre SharePoint-Installation und Azure-Speicher Warteschlangen haben keine Auswirkung auf die Leistung des jeweils anderen.</span><span class="sxs-lookup"><span data-stu-id="6596d-317">Your SharePoint installation and Azure storage queues have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="6596d-318">Azure-Speicher Warteschlangen skalieren einfach.</span><span class="sxs-lookup"><span data-stu-id="6596d-318">Azure storage queues scale easily.</span></span>
    
- <span data-ttu-id="6596d-319">Sie können sichern und Wiederherstellen die Azure-Speicher Warteschlangen separat von Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="6596d-319">You can back up and restore your Azure storage queues separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="6596d-320">Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.</span><span class="sxs-lookup"><span data-stu-id="6596d-320">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="6596d-321">Die app-Schnittstelle angezeigt ein Anruf Supportgruppe im mittleren Bereich, wenn Sie den Link **Aufrufen Warteschlange** auswählen.</span><span class="sxs-lookup"><span data-stu-id="6596d-321">The app's interface displays a support call queue in the center pane when you choose the  **Call Queue** link.</span></span> <span data-ttu-id="6596d-322">Simulieren Sie den Empfang von Anrufen (Hinzufügen eines Anrufs an die Warteschlange), indem **Simulieren Anrufe**auswählen, und nutzen den ältesten Anruf (entfernen einen Anruf aus der Warteschlange) können Sie durch Auswählen der **Anruf annehmen** Aktion in Verbindung mit einem bestimmten Anruf simulieren.</span><span class="sxs-lookup"><span data-stu-id="6596d-322">You can simulate receiving calls (adding a call to the queue) by choosing **Simulate Calls**, and you can simulate taking the oldest call (removing a call from the queue) by choosing the  **Take Call** action associated with a given call.</span></span>

<span data-ttu-id="6596d-323">Diese Seite ist eine Model-View-Controller-Ansicht, die in der Datei Views\CallQueue\Home.cshmtl definiert ist.</span><span class="sxs-lookup"><span data-stu-id="6596d-323">This page is a Model-View-Controller view that is defined in the Views\CallQueue\Home.cshmtl file.</span></span> <span data-ttu-id="6596d-324">Die Datei Controllers\CallQueueController.cs definiert die **CallQueueController** -Klasse, die Methoden zum Abrufen aller Anrufe in die Warteschlange enthält, einen Anruf an die Warteschlange (simulieren eines Anrufs) hinzufügen und Entfernen von einen Anruf aus der Warteschlange (einen Anruf nutzen).</span><span class="sxs-lookup"><span data-stu-id="6596d-324">The Controllers\CallQueueController.cs file defines the  **CallQueueController** class, which contains methods for retrieving all calls in the queue, adding a call to the queue (simulating a call), and removing a call from the queue (taking a call).</span></span> <span data-ttu-id="6596d-325">Jeder der folgenden Methoden ruft Methoden in der Datei Services\CallQueueService.cs, die die Azure-Speicher-Warteschlange API verwendet, um die zugrunde liegenden Informationen in der Speicherwarteschlange abrufen definiert.</span><span class="sxs-lookup"><span data-stu-id="6596d-325">Each of these methods calls methods defined in the Services\CallQueueService.cs file, which uses the Azure storage queue API to retrieve the underlying information in the storage queue.</span></span>

```C#
public class CallQueueController : Controller
{
    public CallQueueService CallQueueService { get; private set; }

    public CallQueueController()
    {
        CallQueueService = new CallQueueService();
    }

    // GET: CallQueue
    public ActionResult Home(UInt16 displayCount = 10)
    {
        var calls = CallQueueService.PeekCalls(displayCount);
        ViewBag.DisplayCount = displayCount;
        ViewBag.TotalCallCount = CallQueueService.GetCallCount();
        return View(calls);
    }

    [HttpPost]
    public ActionResult SimulateCalls(string spHostUrl)
    {
        int count = CallQueueService.SimulateCalls();
        TempData["Message"] = string.Format("Successfully simulated {0} calls and added them to the call queue.", count);
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }

    [HttpPost]
    public ActionResult TakeCall(string spHostUrl)
    {
        CallQueueService.DequeueCall();
        TempData["Message"] = "Call taken successfully and removed from the call queue!";
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }
}
```

<span data-ttu-id="6596d-326">Die CallQueueService.cs-Datei definiert die **CallQueueService** -Klasse, die an die Warteschlange Azure-Speicher die Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="6596d-326">The CallQueueService.cs file defines the  **CallQueueService** class, which establishes the connection to the Azure storage queue.</span></span> <span data-ttu-id="6596d-327">Diese Klasse enthält auch die Methoden zum Hinzufügen, entfernen (entfernen) und der Aufrufe aus der Warteschlange abruft.</span><span class="sxs-lookup"><span data-stu-id="6596d-327">That class also contains the methods for adding, removing (dequeuing), and retrieving the calls from the queue.</span></span>

```C#
public class CallQueueService
{
    private CloudQueueClient queueClient;

    private CloudQueue queue;

    public CallQueueService(string storageConnectionStringConfigName = "StorageConnectionString")
    {
        var connectionString = CloudConfigurationManager.GetSetting(storageConnectionStringConfigName);
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        this.queueClient = storageAccount.CreateCloudQueueClient();
        this.queue = queueClient.GetQueueReference("calls");
        this.queue.CreateIfNotExists();
        }

        public int? GetCallCount()
        {
        queue.FetchAttributes();
        return queue.ApproximateMessageCount;
    }

    public IEnumerable<Call> PeekCalls(UInt16 count)
    {
        var messages = queue.PeekMessages(count);

        var serializer = new JavaScriptSerializer();
        foreach (var message in messages)
        {
        Call call = null;
        try
        {
        call = serializer.Deserialize<Call>(message.AsString);
        }
        catch { }

        if (call != null) yield return call;
        }
    }

    public void AddCall(Call call)
    {
        var serializer = new JavaScriptSerializer();
        var content = serializer.Serialize(call);
        var message = new CloudQueueMessage(content);
        queue.AddMessage(message);
    }

    public void DequeueCall()
    {
        var message = queue.GetMessage();
        queue.DeleteMessage(message);
    }

    public int SimulateCalls()
    {
        Random random = new Random();
        int count = random.Next(1, 6);
        for (int i = 0; i < count; i++)
        {
        int phoneNumber = random.Next();
        var call = new Call
        {
        ReceivedDate = DateTime.Now,
        PhoneNumber = phoneNumber.ToString("+1-000-000-0000")
        };
        AddCall(call);

        return count;
    }
}
```

## <a name="sql-azure-database-recent-orders-scenario"></a><span data-ttu-id="6596d-328">SQL Azure-Datenbank (aktuellen Aufträge Szenario)</span><span class="sxs-lookup"><span data-stu-id="6596d-328">SQL Azure database (Recent Orders scenario)</span></span>
<span data-ttu-id="6596d-329"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-329"></span></span>

<span data-ttu-id="6596d-330">Das aktuellen Aufträge Szenario verwendet einen direkten Aufruf der Northwind SQL Azure-Datenbank, um alle Aufträge für einen bestimmten Kunden zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="6596d-330">The Recent Orders scenario uses a direct call to the Northwind SQL Azure database to return all the orders for a given customer.</span></span>

<span data-ttu-id="6596d-331">Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:</span><span class="sxs-lookup"><span data-stu-id="6596d-331">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="6596d-332">Eine Datenbank kann mehrere app unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6596d-332">A database can support more than one app.</span></span>
    
- <span data-ttu-id="6596d-333">Sie können das Datenbankschema aktualisieren, ohne dass aktualisieren und erneut bereitstellen Ihrer app, solange die Schemaversion Abfragen in Ihrer app keine Auswirkung auf.</span><span class="sxs-lookup"><span data-stu-id="6596d-333">You can update your database schema without having to update and redeploy your app, as long as the schema changes don't affect the queries in your app.</span></span>
    
- <span data-ttu-id="6596d-334">Eine relationale Datenbank kann n: n-Beziehungen unterstützt und daher die komplexere Geschäftsszenarien unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6596d-334">A relational database can support many-to-many relationships and thus support more complex business scenarios.</span></span>
    
- <span data-ttu-id="6596d-335">Datenbank-Designtools können Sie um den Entwurf Ihrer Datenbank zu optimieren.</span><span class="sxs-lookup"><span data-stu-id="6596d-335">You can use database design tools to optimize the design of your database.</span></span>
    
- <span data-ttu-id="6596d-336">Relationale Datenbanken bieten eine bessere Leistung als die anderen Optionen, wenn Sie komplexe Vorgänge in Abfragen, wie etwa Berechnungen und Joins ausführen müssen.</span><span class="sxs-lookup"><span data-stu-id="6596d-336">Relational databases provide better performance than the other options when you need to execute complex operations in your queries, such as calculations and joins.</span></span>
    
- <span data-ttu-id="6596d-337">Eine SQL Azure-Datenbank können Sie zum Importieren und Exportieren von Daten auf einfache Weise, daher es einfacher ist zu verwalten und Ihre Daten zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="6596d-337">A SQL Azure database allows you to import and export data easily, so it's easier to manage and move your data.</span></span>
    
- <span data-ttu-id="6596d-338">Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, wenn die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.</span><span class="sxs-lookup"><span data-stu-id="6596d-338">You don't lose any data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="6596d-339">Die letzte Orders Schnittstelle funktioniert ähnlich wie die Kunden-Dashboard-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="6596d-339">The recent orders interface works much like the customer dashboard interface.</span></span> <span data-ttu-id="6596d-340">Sie wählen Sie auf den Link **Aktuellen Aufträge** in der linken Spalte aus, und wählen Sie dann im Dropdown-Menü am oberen Rand der mittleren Bereich ein Kunden.</span><span class="sxs-lookup"><span data-stu-id="6596d-340">You choose on the  **Recent Orders** link in the left column, and then choose a customer from the drop-down menu at the top of the center pane.</span></span> <span data-ttu-id="6596d-341">Eine Liste der Aufträge dieses Kunden anzeigen wird im mittleren Bereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6596d-341">A list of orders from that customer will appear in the center pane.</span></span>

<span data-ttu-id="6596d-342">Diese Seite ist eine Model-View-Controller-Ansicht in der Datei Views\CustomerDashboard\Orders.cshtml definiert.</span><span class="sxs-lookup"><span data-stu-id="6596d-342">This page is a Model-View-Controller view defined in the Views\CustomerDashboard\Orders.cshtml file.</span></span> <span data-ttu-id="6596d-343">Code in der Datei Controllers\CustomerDashboardController.cs verwendet das [Entity Framework](https://msdn.microsoft.com/en-us/data/ef.aspx) zum Abfragen der **Orders** -Tabelle in SQL Azure-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="6596d-343">Code in the Controllers\CustomerDashboardController.cs file uses the  [Entity Framework ](https://msdn.microsoft.com/en-us/data/ef.aspx) to query the **Orders** table in your SQL Azure database.</span></span> <span data-ttu-id="6596d-344">Die Kunden-ID wird mithilfe der in der URL, die übergeben wird, wenn der Benutzer einen Kunden aus dem Dropdown-Menü auswählt einen Abfragezeichenfolgen-Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="6596d-344">The customer ID is passed by using a query string parameter in the URL that is passed when the user selects a customer from the drop-down menu.</span></span> <span data-ttu-id="6596d-345">Die Abfrage erstellt eine Verknüpfung für die Tabellen **Kunden**, **Lieferanten** und **Mitarbeiter**.</span><span class="sxs-lookup"><span data-stu-id="6596d-345">The query creates a join on the **Customer**,  **Employee**, and  **Shipper** tables.</span></span> <span data-ttu-id="6596d-346">Das Abfrageergebnis wird dann an die Model-View-Controller-Ansicht übergeben, die die Ergebnisse angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6596d-346">The query result is then passed to the Model-View-Controller view that displays the results.</span></span>

<span data-ttu-id="6596d-347">Der folgende Code aus der Datei CustomerDashboardController.cs Datenbankabfrage ausführt und gibt die Daten zur Ansicht zurück.</span><span class="sxs-lookup"><span data-stu-id="6596d-347">The following code from the CustomerDashboardController.cs file performs the database query and returns the data to the view.</span></span>

```C#
public ActionResult Orders(string customerId)
{            
    Order[] orders;
    using (var db = new NorthWindEntities())
    {
            orders = db.Orders
                  .Include(o => o.Customer)
                  .Include(o => o.Employee)
                  .Include(o => o.Shipper)
                  .Where(c => c.CustomerID == customerId)
                  .ToArray();
    }

    ViewBag.SharePointContext = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    return View(orders);
}
```

## <a name="additional-resources"></a><span data-ttu-id="6596d-348">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6596d-348">Additional resources</span></span>
<span data-ttu-id="6596d-349"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6596d-349"></span></span>

-  [<span data-ttu-id="6596d-350">Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6596d-350">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="6596d-351">Office 365-Entwicklungsmuster und -übungen auf GitHub</span><span class="sxs-lookup"><span data-stu-id="6596d-351">Office 365 Development Patterns and Practices on GitHub</span></span>](https://github.com/SharePoint/PnP)
