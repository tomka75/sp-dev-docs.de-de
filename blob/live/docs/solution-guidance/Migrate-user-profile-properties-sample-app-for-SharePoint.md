---
title: "Migrieren Sie Benutzerprofil Eigenschaften Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 03a7591b21531387e1cd1312be76f1f6e916c41e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="migrate-user-profile-properties-sample-add-in-for-sharepoint"></a><span data-ttu-id="60766-102">Migrieren Sie Benutzerprofil Eigenschaften Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="60766-102">Migrate user profile properties sample add-in for SharePoint</span></span>

<span data-ttu-id="60766-103">Verwenden einer vom Anbieter gehosteten-add-in zu migrieren und Importieren von Profildaten für SharePoint-Benutzer.</span><span class="sxs-lookup"><span data-stu-id="60766-103">You can use a provider-hosted add-in to migrate and import SharePoint user profile data.</span></span>

<span data-ttu-id="60766-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="60766-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="60766-105">[Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) -Beispiel-add-in zeigt, wie von Benutzerprofildaten von SharePoint Server 2010 oder SharePoint Server 2013 in SharePoint Online zu migrieren.</span><span class="sxs-lookup"><span data-stu-id="60766-105">The [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) sample add-in shows you how to migrate user profile data from SharePoint Server 2010 or SharePoint Server 2013 into SharePoint Online.</span></span>
    
<span data-ttu-id="60766-106">Dieses Beispiel enthält zwei konsolenanwendungen.</span><span class="sxs-lookup"><span data-stu-id="60766-106">This sample includes two console applications.</span></span> <span data-ttu-id="60766-107">Beide verwenden den userprofileservice.asmx-Webdienst, um ein- und mehrwertige Benutzerprofildaten in eine XML-Datei extrahieren, und importieren die extrahierten Daten in den Benutzerprofildienst in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="60766-107">Both use the userprofileservice.asmx web service to extract single and multivalued user profile data to an XML file, and to import the extracted data into the user profile service in SharePoint Online.</span></span>
<span data-ttu-id="60766-108">Wenn Sie möchten, verwenden Sie dieses Codebeispiel:</span><span class="sxs-lookup"><span data-stu-id="60766-108">Use this code sample if you want to:</span></span>

- <span data-ttu-id="60766-109">Extrahieren von Benutzerprofildaten in SharePoint Server 2010 oder SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="60766-109">Extract user profile data in SharePoint Server 2010 or SharePoint Server 2013.</span></span>
    
- <span data-ttu-id="60766-110">Importieren von Benutzerprofildaten in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="60766-110">Import user profile data into SharePoint Online.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="60766-111">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="60766-111">Before you begin</span></span>
<span data-ttu-id="60766-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="60766-112"></span></span>

<span data-ttu-id="60766-113">Laden Sie Sie zuerst [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="60766-113">To get started, download the  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span> <span data-ttu-id="60766-114">Das Codebeispiel enthält zwei Projekte.</span><span class="sxs-lookup"><span data-stu-id="60766-114">The code sample contains two projects.</span></span>

<span data-ttu-id="60766-115">Für das Projekt **Contoso.ProfileProperty.Migration.Extract** :</span><span class="sxs-lookup"><span data-stu-id="60766-115">For the  **Contoso.ProfileProperty.Migration.Extract** project:</span></span>

- <span data-ttu-id="60766-116">Da in diesem Codebeispiel wird das serverseitige Objektmodell verwendet, müssen Sie unbedingt, dass Sie das Projekt auf einem Server mit SharePoint Server 2010 oder SharePoint Server 2013 installiert ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="60766-116">Because this code sample uses the server-side object model, be sure that you are running the project on a server with SharePoint Server 2010 or SharePoint Server 2013 installed.</span></span>
    
- <span data-ttu-id="60766-117">Verwenden Sie ein Konto mit Administratorberechtigungen für SharePoint-Farm.</span><span class="sxs-lookup"><span data-stu-id="60766-117">Use an account that has SharePoint farm administrator permissions.</span></span>
    
- <span data-ttu-id="60766-118">Bearbeiten Sie die Konfigurationsinformationen, die in Tabelle 1 aufgeführten mithilfe die Datei App.config.</span><span class="sxs-lookup"><span data-stu-id="60766-118">Edit the App.config file using the configuration information listed in Table 1.</span></span>
    
- <span data-ttu-id="60766-119">Für alle Benutzer stellen Sie sicher, dass die Benutzerprofileigenschaft **E-Mail** nicht leer ist.</span><span class="sxs-lookup"><span data-stu-id="60766-119">For all users, ensure that the  **Work email** user profile property is not empty.</span></span> <span data-ttu-id="60766-120">Wenn der Wert der Benutzerprofileigenschaft **Arbeit e-Mail** leer ist, werden die Extraktion vorzeitig beendet.</span><span class="sxs-lookup"><span data-stu-id="60766-120">If the value of the **Work email** user profile property is empty, the extraction process will end prematurely.</span></span>
    
- <span data-ttu-id="60766-121">In diesem Codebeispiel extrahiert Benutzerprofile von SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="60766-121">This code sample extracts user profiles from SharePoint Server 2010.</span></span> <span data-ttu-id="60766-122">Wenn Sie Benutzerprofile aus SharePoint Server 2013 extrahieren, führen Sie folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="60766-122">If you are extracting user profiles from SharePoint Server 2013, do the following:</span></span>
    
  <span data-ttu-id="60766-123">ein.</span><span class="sxs-lookup"><span data-stu-id="60766-123">a.</span></span> <span data-ttu-id="60766-124">Öffnen Sie das Kontextmenü (Rechtsklick) für **Contoso.ProfileProperty.Migration.Extract** > **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="60766-124">Open the shortcut menu (right-click) for  **Contoso.ProfileProperty.Migration.Extract** > **Properties**.</span></span>
    
  <span data-ttu-id="60766-125">b.</span><span class="sxs-lookup"><span data-stu-id="60766-125">b.</span></span> <span data-ttu-id="60766-126">Wählen Sie unter **Anwendung** **Zielframework** **.NET Framework 4**.</span><span class="sxs-lookup"><span data-stu-id="60766-126">Under  **Application**, in  **Target framework** choose **.NET Framework 4**.</span></span>
    
  <span data-ttu-id="60766-127">c.</span><span class="sxs-lookup"><span data-stu-id="60766-127">c.</span></span> <span data-ttu-id="60766-128">Wählen Sie **Ja**, klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="60766-128">Choose  **Yes**, then  **Save**.</span></span>
    
<span data-ttu-id="60766-129">**In Tabelle 1. Konfigurationen für die App**</span><span class="sxs-lookup"><span data-stu-id="60766-129">**Table 1. Configuration settings for App.Config file**</span></span>

|<span data-ttu-id="60766-130">**Name der Einstellung Konfiguration**</span><span class="sxs-lookup"><span data-stu-id="60766-130">**Configuration setting name**</span></span>|<span data-ttu-id="60766-131">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="60766-131">**Description**</span></span>|<span data-ttu-id="60766-132">Beispiel</span><span class="sxs-lookup"><span data-stu-id="60766-132">Example</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="60766-133">**MYSITEHOSTURL**</span><span class="sxs-lookup"><span data-stu-id="60766-133">**MYSITEHOSTURL**</span></span> |<span data-ttu-id="60766-134">Meine Website-URL in der quellfarm für SharePoint Server 2010 oder SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="60766-134">My Site URL on the source SharePoint Server 2010 or SharePoint Server 2013 farm.</span></span>|<span data-ttu-id="60766-135">http://My.contoso.com</span><span class="sxs-lookup"><span data-stu-id="60766-135">http://my.contoso.com</span></span> |
|<span data-ttu-id="60766-136">**PROPERTYSEPERATOR**</span><span class="sxs-lookup"><span data-stu-id="60766-136">**PROPERTYSEPERATOR**</span></span> |<span data-ttu-id="60766-137">Das Zeichen verwendet, um mehrere Werte einer mehrwertigen Benutzerprofileigenschaft zu trennen.</span><span class="sxs-lookup"><span data-stu-id="60766-137">The character used to separate multiple values in a multivalued user profile property.</span></span>| |
|<span data-ttu-id="60766-138">**USERPROFILESSTORE**</span><span class="sxs-lookup"><span data-stu-id="60766-138">**USERPROFILESSTORE**</span></span> |<span data-ttu-id="60766-139">Der XML-Dateipfad zum Schreiben der extrahierten Benutzerprofildaten.</span><span class="sxs-lookup"><span data-stu-id="60766-139">The XML file path to use to write extracted user profile data.</span></span>|<span data-ttu-id="60766-140">C:\temp\ProfileData.Xml</span><span class="sxs-lookup"><span data-stu-id="60766-140">C:\temp\ProfileData.xml</span></span>|
|<span data-ttu-id="60766-141">**LOGFILE**</span><span class="sxs-lookup"><span data-stu-id="60766-141">**LOGFILE**</span></span> |<span data-ttu-id="60766-142">Der XML-Dateipfad zum Schreiben der extrahierten Benutzerprofildaten.</span><span class="sxs-lookup"><span data-stu-id="60766-142">The XML file path to use to write extracted user profile data.</span></span>|<span data-ttu-id="60766-143">C:\temp\Extract.log</span><span class="sxs-lookup"><span data-stu-id="60766-143">C:\temp\Extract.log</span></span>|
|<span data-ttu-id="60766-144">**ENABLELOGGING**</span><span class="sxs-lookup"><span data-stu-id="60766-144">**ENABLELOGGING**</span></span> |<span data-ttu-id="60766-145">Aktivieren Sie Datenträger-Protokollierung.</span><span class="sxs-lookup"><span data-stu-id="60766-145">Enable disk logging.</span></span>|<span data-ttu-id="60766-146">"True"</span><span class="sxs-lookup"><span data-stu-id="60766-146">True</span></span>|
|<span data-ttu-id="60766-147">**TESTRUN**</span><span class="sxs-lookup"><span data-stu-id="60766-147">**TESTRUN**</span></span> |<span data-ttu-id="60766-148">Führt eine Extraktion Test, um zu bestätigen, dass Ihre Konfigurationseinstellungen in App.Config richtig sind.</span><span class="sxs-lookup"><span data-stu-id="60766-148">Performs a test extraction to confirm that your configuration settings in App.Config are correct.</span></span>|<span data-ttu-id="60766-149">Legen Sie `TESTRUN=true` Wenn Sie eine Extraktion Test durchführen.</span><span class="sxs-lookup"><span data-stu-id="60766-149">Set `TESTRUN=true` if you are performing a test extraction.</span></span> <span data-ttu-id="60766-150">Der Testlauf extrahiert nur für einen Benutzer aus der Benutzerprofildienst.</span><span class="sxs-lookup"><span data-stu-id="60766-150">The test run extracts only one user from the user profile service.</span></span><br /> <span data-ttu-id="60766-151">Legen Sie `TESTRUN=false` Wenn Sie alle Benutzer aus der Benutzerprofildienst extrahieren.</span><span class="sxs-lookup"><span data-stu-id="60766-151">Set `TESTRUN=false` if you are extracting all users from the user profile service.</span></span> |

<span data-ttu-id="60766-152">Für das Projekt **Contoso.ProfileProperty.Migration.Import**</span><span class="sxs-lookup"><span data-stu-id="60766-152">For the  **Contoso.ProfileProperty.Migration.Import** project</span></span>

- <span data-ttu-id="60766-153">Stellen Sie sicher, dass die Benutzerprofile in Office 365 vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="60766-153">Ensure that user profiles exist in Office 365.</span></span> 
    
- <span data-ttu-id="60766-154">Stellen Sie sicher, dass **E-Mail** -Adresse des Benutzers in der lokalen SharePoint Server 2013 und Office 365 Benutzerprofildienst identisch ist.</span><span class="sxs-lookup"><span data-stu-id="60766-154">Ensure that the user's  **Work email** address is the same in the SharePoint Server 2013 on-premises and Office 365 user profile service.</span></span>
    
- <span data-ttu-id="60766-155">Ändern Sie in der Datei App.config das **Value** -Element der **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** Einstellung, die einen Verweis auf den Benutzerprofildienst in Ihrer SharePoint Online-Verwaltungskonsole zählen Siehe die in der folgenden Beispiel.</span><span class="sxs-lookup"><span data-stu-id="60766-155">In the App.config file, change the  **value** element of the **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** setting to include a reference to the user profile service in your SharePoint Online admin center, as shown in the following example.</span></span>

    ```XML
    <applicationSettings>
    <Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    <setting name="Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService" serializeAs="String">
    <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
    </setting>
    </Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    </applicationSettings>
    ```

- <span data-ttu-id="60766-156">Bearbeiten Sie die in Tabelle 2 aufgelisteten Konfigurationseinstellungen mithilfe die Datei App.config.</span><span class="sxs-lookup"><span data-stu-id="60766-156">Edit the App.config file using the configuration settings listed in Table 2.</span></span>
    
<span data-ttu-id="60766-157">**In Tabelle 2. Konfigurationseinstellungen für die Datei ' App.config '**</span><span class="sxs-lookup"><span data-stu-id="60766-157">**Table 2. App.config file configuration settings**</span></span>

|<span data-ttu-id="60766-158">**Name der Einstellung Konfiguration**</span><span class="sxs-lookup"><span data-stu-id="60766-158">**Configuration setting name**</span></span>|<span data-ttu-id="60766-159">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="60766-159">**Description**</span></span>|<span data-ttu-id="60766-160">Beispiel</span><span class="sxs-lookup"><span data-stu-id="60766-160">Example</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="60766-161">**tenantName**</span><span class="sxs-lookup"><span data-stu-id="60766-161">**tenantName**</span></span> |<span data-ttu-id="60766-162">Dies ist der Name des Mandanten.</span><span class="sxs-lookup"><span data-stu-id="60766-162">This is your tenant’s name.</span></span>|<span data-ttu-id="60766-163">Wenn Ihre Mandanten URL http://contoso.onmicrosoft.com ist, geben Sie Contoso als Ihrem Mandantennamen.</span><span class="sxs-lookup"><span data-stu-id="60766-163">If your tenant URL is http://contoso.onmicrosoft.com, enter contoso as your tenant name.</span></span>|
|<span data-ttu-id="60766-164">**PROPERTYSEPERATOR**</span><span class="sxs-lookup"><span data-stu-id="60766-164">**PROPERTYSEPERATOR**</span></span> |<span data-ttu-id="60766-165">Das Zeichen verwendet, um die Werte einer mehrwertigen Benutzerprofileigenschaft zu trennen.</span><span class="sxs-lookup"><span data-stu-id="60766-165">The character used to separate values in a multivalued user profile property.</span></span>| |
|<span data-ttu-id="60766-166">**USERPROFILESSTORE**</span><span class="sxs-lookup"><span data-stu-id="60766-166">**USERPROFILESSTORE**</span></span> |<span data-ttu-id="60766-167">Die XML-Datei zum Lesen der extrahierten Benutzerprofildaten.</span><span class="sxs-lookup"><span data-stu-id="60766-167">The XML file to use to read extracted user profile data.</span></span>|<span data-ttu-id="60766-168">C:\temp\ProfileData.Xml</span><span class="sxs-lookup"><span data-stu-id="60766-168">C:\temp\ProfileData.xml</span></span>|
|<span data-ttu-id="60766-169">**LOGFILE**</span><span class="sxs-lookup"><span data-stu-id="60766-169">**LOGFILE**</span></span> |<span data-ttu-id="60766-170">Die Protokolldatei für die ereignisprotokollierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="60766-170">Log file used for event logging.</span></span>|<span data-ttu-id="60766-171">C:\temp\Extract.log</span><span class="sxs-lookup"><span data-stu-id="60766-171">C:\temp\Extract.log</span></span>|
|<span data-ttu-id="60766-172">**ENABLELOGGING**</span><span class="sxs-lookup"><span data-stu-id="60766-172">**ENABLELOGGING**</span></span> |<span data-ttu-id="60766-173">Aktivieren Sie Datenträger-Protokollierung.</span><span class="sxs-lookup"><span data-stu-id="60766-173">Enable disk logging.</span></span>|<span data-ttu-id="60766-174">"True"</span><span class="sxs-lookup"><span data-stu-id="60766-174">True</span></span>|
|<span data-ttu-id="60766-175">**SPOAdminUserName**</span><span class="sxs-lookup"><span data-stu-id="60766-175">**SPOAdminUserName**</span></span> |<span data-ttu-id="60766-176">Ein Office 365-Administrator Benutzername.</span><span class="sxs-lookup"><span data-stu-id="60766-176">An Office 365 administrator’s username.</span></span>|<span data-ttu-id="60766-177">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="60766-177">Not applicable.</span></span>|
|<span data-ttu-id="60766-178">**SPOAdminPassword**</span><span class="sxs-lookup"><span data-stu-id="60766-178">**SPOAdminPassword**</span></span> |<span data-ttu-id="60766-179">Kennwort für ein Office 365-Administrator.</span><span class="sxs-lookup"><span data-stu-id="60766-179">An Office 365 administrator’s password.</span></span>|<span data-ttu-id="60766-180">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="60766-180">Not applicable.</span></span>|

## <a name="using-the-coreprofilepropertymigration-app"></a><span data-ttu-id="60766-181">Verwenden der app Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="60766-181">Using the Core.ProfileProperty.Migration app</span></span>
<span data-ttu-id="60766-182"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="60766-182"></span></span>

<span data-ttu-id="60766-183">In diesem Codebeispiel wird als Konsolenanwendung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="60766-183">This code sample runs as a console application.</span></span> <span data-ttu-id="60766-184">Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Funktion in Program.cs die folgenden Aufgaben aus:</span><span class="sxs-lookup"><span data-stu-id="60766-184">When the code sample runs, the  **Main** function in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="60766-185">Stellt eine Verbindung zur Mein Websitehost und Verbindung mit der Benutzerprofildienst **UserProfileManager** verwendet.</span><span class="sxs-lookup"><span data-stu-id="60766-185">Connects to the My Site Host and uses  **UserProfileManager** to connect to the user profile service.</span></span> <span data-ttu-id="60766-186">**UserProfileManager** gehört die **Microsoft.Office.Server.UserProfiles.dll** -Assembly.</span><span class="sxs-lookup"><span data-stu-id="60766-186">**UserProfileManager** belongs to the **Microsoft.Office.Server.UserProfiles.dll** assembly.</span></span>
    
- <span data-ttu-id="60766-187">Erstellt eine Liste namens **pData** zum Speichern der extrahierten Benutzerprofildaten.</span><span class="sxs-lookup"><span data-stu-id="60766-187">Creates a list called  **pData** to store extracted user profile data.</span></span>
    
- <span data-ttu-id="60766-188">Für alle Benutzer in der Benutzerprofildienst passiert Folgendes:</span><span class="sxs-lookup"><span data-stu-id="60766-188">For all users in the user profile service it does the following:</span></span>
    
    - <span data-ttu-id="60766-189">Wird mit **GetSingleValuedProperty** die **WorkEmail** und Benutzerprofileigenschaften **Mich-Seite** auf ein **UserProfileData** -Objekt namens **"UserData"**kopiert.</span><span class="sxs-lookup"><span data-stu-id="60766-189">Uses  **GetSingleValuedProperty** to copy the **WorkEmail** and **AboutMe** user profile properties to a **UserProfileData** object called **userData**.</span></span>
    
    - <span data-ttu-id="60766-190">Wird mit **GetMultiValuedProperty** **SPS-Verantwortung** Benutzerprofileigenschaft zu **"UserData"**kopiert.</span><span class="sxs-lookup"><span data-stu-id="60766-190">Uses  **GetMultiValuedProperty** to copy the **SPS-Responsibility** user profile property to **userData**.</span></span>
    
- <span data-ttu-id="60766-191">**UserProfileCollection.Save** verwendet zum Serialisieren von **UserData** in eine XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="60766-191">Uses  **UserProfileCollection.Save** to serialize **userData** to an XML file.</span></span> <span data-ttu-id="60766-192">Die XML-Datei wird unter dem Dateipfad gespeichert, der in ' App.config ' angegeben.</span><span class="sxs-lookup"><span data-stu-id="60766-192">The XML file is saved at the file path you specified in App.config.</span></span>

> [!NOTE] 
> <span data-ttu-id="60766-193">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="60766-193">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
static void Main(string[] args)
        {
            int userCount = 1;

            try
            {

                if (Convert.ToBoolean(ConfigurationManager.AppSettings["TESTRUN"]))
                {
                    LogMessage(string.Format("******** RUNNING IN TEST RUN MODE **********"), LogLevel.Debug);
                }
                
                LogMessage(string.Format("Connecting to My Site Host: '{0}'...", ConfigurationManager.AppSettings["MYSITEHOSTURL"]), LogLevel.Info);
                using (SPSite mySite = new SPSite(ConfigurationManager.AppSettings["MYSITEHOSTURL"]))
                {
                    LogMessage(string.Format("Connecting to My Site Host: '{0}'...Done!", ConfigurationManager.AppSettings["MYSITEHOSTURL"]), LogLevel.Info);

                    LogMessage(string.Format("getting Service Context..."), LogLevel.Info);
                    SPServiceContext svcContext = SPServiceContext.GetContext(mySite);
                    LogMessage(string.Format("getting Service Context...Done!"), LogLevel.Info);

                    LogMessage(string.Format("Connecting to Profile Manager..."), LogLevel.Info);
                    UserProfileManager profileManager = new UserProfileManager(svcContext);
                    LogMessage(string.Format("Connecting to Profile Manager...Done!"), LogLevel.Info);

                    // Size of the List is set to the number of profiles.
                    List<UserProfileData> pData = new List<UserProfileData>(Convert.ToInt32(profileManager.Count));
                    
                    // Initialize Serialization Class.
                    UserProfileCollection ups = new UserProfileCollection();

                    foreach (UserProfile spUser in profileManager)
                    {
                        // Get Profile Information.
                        LogMessage(string.Format("processing user '{0}' of {1}...", userCount,profileManager.Count),LogLevel.Info);                       
                        UserProfileData userData = new UserProfileData();
                        
                        userData.UserName = GetSingleValuedProperty(spUser, "WorkEmail");
                        
                        if (userData.UserName != string.Empty)
                        {
                            userData.AboutMe = GetSingleValuedProperty(spUser, "AboutMe");
                            userData.AskMeAbout = GetMultiValuedProperty(spUser, "SPS-Responsibility");
                            pData.Add(userData);
                            // Add to Serialization Class List of Profiles.
                            ups.ProfileData = pData;
                        }
                        
                        LogMessage(string.Format("processing user '{0}' of {1}...Done!", userCount++, profileManager.Count), LogLevel.Info);

                        // Only process the first item if we are in test mode.
                        if (Convert.ToBoolean(ConfigurationManager.AppSettings["TESTRUN"]))
                        {
                            break;
                        }

                    }
                    
                    // Serialize profiles to disk.
                    ups.Save();

                }
            }
            catch(Exception ex)
            {
                LogMessage("Exception trying to get profile properties:\n" + ex.Message, LogLevel.Error);
            }
```

<span data-ttu-id="60766-194">Beachten Sie, dass die **GetSingleValuedProperty** -Methode userprofileservice.asmx verwendet, um ein einwertiges Benutzerprofileigenschaft abzurufen.</span><span class="sxs-lookup"><span data-stu-id="60766-194">Note that the  **GetSingleValuedProperty** method uses userprofileservice.asmx to retrieve a single-valued user profile property.</span></span> <span data-ttu-id="60766-195">**GetSingleValuedProperty** wird Folgendes, wie im nächsten Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="60766-195">**GetSingleValuedProperty** does the following, as shown in the next code example:</span></span>

- <span data-ttu-id="60766-196">Ruft das Property-Objekt zum Extrahieren von Daten aus mithilfe von **Spuser [UserProperty]**ab.</span><span class="sxs-lookup"><span data-stu-id="60766-196">Gets the property object to extract data from using  **spuser[userProperty]**.</span></span>
    
- <span data-ttu-id="60766-197">Gibt den ersten Wert in der **UserProfileValueCollection** zurück, wenn der Wert nicht **null**ist.</span><span class="sxs-lookup"><span data-stu-id="60766-197">Returns the first value in the  **UserProfileValueCollection** if the value is not **null**.</span></span> 

```C#
private static string GetSingleValuedProperty(UserProfile spUser,string userProperty)
        {
            string returnString = string.Empty;
            try
            {
                UserProfileValueCollection propCollection = spUser[userProperty];

                if (propCollection[0] != null)
                {
                    returnString = propCollection[0].ToString();
                }
                else
                {
                    LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);                       
                }
            }
            catch 
            {
                LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);                       
            }


            return returnString;
            
        }
```

<span data-ttu-id="60766-198">Beachten Sie, dass die **GetMultiValuedProperty** -Methode userprofileservice.asmx verwendet, um eine mehrwertige Benutzerprofileigenschaft abzurufen.</span><span class="sxs-lookup"><span data-stu-id="60766-198">Note that the  **GetMultiValuedProperty** method uses userprofileservice.asmx to retrieve a multivalued user profile property.</span></span> <span data-ttu-id="60766-199">**GetMultiValuedProperty** wird Folgendes, wie im nächsten Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="60766-199">**GetMultiValuedProperty** does the following, as shown in the next code example:</span></span>

- <span data-ttu-id="60766-200">Ruft die Benutzerprofileigenschaft-Objekts das update **Spuser [UserProperty]**.</span><span class="sxs-lookup"><span data-stu-id="60766-200">Gets the user profile property object to update using  **spuser[userProperty]**.</span></span>
    
- <span data-ttu-id="60766-201">Erstellt eine Zeichenfolge der Benutzer Profile-Eigenschaftswerte durch die in der Datei ' App.config ' angegebenen **PROPERTYSEPARATOR** getrennt.</span><span class="sxs-lookup"><span data-stu-id="60766-201">Builds a string of user profile property values separated by the  **PROPERTYSEPARATOR** specified in the App.config file.</span></span>

```C#
private static string GetMultiValuedProperty(UserProfile spUser, string userProperty)
        {
            StringBuilder sb = new StringBuilder("");
            string seperator = ConfigurationManager.AppSettings["PROPERTYSEPERATOR"];

            string returnString = string.Empty;
            try
            {

                UserProfileValueCollection propCollection = spUser[userProperty];

                if (propCollection.Count > 1)
                {
                    for (int i = 0; i < propCollection.Count; i++)
                    {
                        if (i == propCollection.Count - 1) { seperator = ""; }
                        sb.AppendFormat("{0}{1}", propCollection[i], seperator);
                    }
                }
                else if (propCollection.Count == 1)
                {
                    sb.AppendFormat("{0}", propCollection[0]);
                }

            }
            catch
            {
                LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);
            }

            return sb.ToString();

        }
```

## <a name="using-contosoprofilepropertymigrationimport"></a><span data-ttu-id="60766-202">Verwenden von Contoso.ProfileProperty.Migration.Import</span><span class="sxs-lookup"><span data-stu-id="60766-202">Using Contoso.ProfileProperty.Migration.Import</span></span>
<span data-ttu-id="60766-203"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="60766-203"></span></span>

<span data-ttu-id="60766-204">In diesem Codebeispiel wird als Konsolenanwendung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="60766-204">This code sample runs as a console application.</span></span> <span data-ttu-id="60766-205">Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Methode in Program.cs Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="60766-205">When the code sample runs, the  **Main** method in Program.cs does the following:</span></span>

- <span data-ttu-id="60766-206">Initialisiert die Konsolenanwendung **InitializeConfiguration** und **InitializeWebService**verwenden.</span><span class="sxs-lookup"><span data-stu-id="60766-206">Initializes the console application using  **InitializeConfiguration** and **InitializeWebService**.</span></span> 
    
- <span data-ttu-id="60766-207">Deserialisiert die XML-Datei, die die extrahierten Benutzerprofildaten enthält.</span><span class="sxs-lookup"><span data-stu-id="60766-207">Deserializes the XML file containing the extracted user profile data.</span></span>
    
- <span data-ttu-id="60766-208">Für alle Benutzer in der XML-Datei geschieht Folgendes:</span><span class="sxs-lookup"><span data-stu-id="60766-208">For all users in the XML file it does the following:</span></span>
    
    - <span data-ttu-id="60766-209">Extrahiert die **UserName** -Eigenschaft aus der XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="60766-209">Extracts the  **UserName** property from the XML file.</span></span>
    
    - <span data-ttu-id="60766-210">Mithilfe von **SetSingleMVProfileProperty** **SPS-Verantwortung** auf das Profil des Benutzers festgelegt.</span><span class="sxs-lookup"><span data-stu-id="60766-210">Uses  **SetSingleMVProfileProperty** to set **SPS-Responsibility** on the user's profile.</span></span>
    
    - <span data-ttu-id="60766-211">Mithilfe von **SetSingleMVProfileProperty** **Mich-Seite** auf das Profil des Benutzers festgelegt.</span><span class="sxs-lookup"><span data-stu-id="60766-211">Uses  **SetSingleMVProfileProperty** to set **AboutMe** on the user's profile.</span></span>
    
<span data-ttu-id="60766-212">**InitializeWebService** stellt eine Verbindung mit SharePoint Online, und einen Verweis auf den Benutzerprofildienst auf eine Instanzvariable festgelegt.</span><span class="sxs-lookup"><span data-stu-id="60766-212">**InitializeWebService** connects to SharePoint Online, and sets a reference of the user profile service to an instance variable.</span></span> <span data-ttu-id="60766-213">Andere Methoden in diesem Codebeispiel verwenden Sie diese Instanzvariable zum Schreiben von Werten in Benutzerprofileigenschaften.</span><span class="sxs-lookup"><span data-stu-id="60766-213">Other methods in this code sample use this instance variable to write values to user profile properties.</span></span> <span data-ttu-id="60766-214">Zum Verwalten von Benutzerprofil verwendet dieses Codebeispiel den userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole.</span><span class="sxs-lookup"><span data-stu-id="60766-214">To administer the user profile, this code sample uses the userprofileservice.asmx web service on the SharePoint Online admin center.</span></span>

```C#
static bool InitializeWebService()
        {
            try
            {
                string webServiceExt = "_vti_bin/userprofileservice.asmx";
                string adminWebServiceUrl = string.Empty;
                
                if (_profileSiteUrl.EndsWith("/"))
                    adminWebServiceUrl = _profileSiteUrl + webServiceExt;
                else
                    adminWebServiceUrl = _profileSiteUrl + "/" + webServiceExt;

                LogMessage("Initializing SPO web service " + adminWebServiceUrl, LogLevel.Information);

                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);
                SharePointOnlineCredentials onlineCred = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);

                string authCookie = onlineCred.GetAuthenticationCookie(new Uri(_profileSiteUrl));

                CookieContainer authContainer = new CookieContainer();
                authContainer.SetCookies(new Uri(_profileSiteUrl), authCookie);

                // Setting up the user profile web service.
                _userProfileService = new UPSvc.UserProfileService();
                _userProfileService.Url = adminWebServiceUrl;

                // Assign previously created auth container to admin profile web service. 
                _userProfileService.CookieContainer = authContainer;
                return true;
            }
            catch (Exception ex)
            {
                LogMessage("Error initiating connection to profile web service in SPO " + ex.Message, LogLevel.Error);
                return false;

            }
            
        }
```

<span data-ttu-id="60766-215">Die **SetSingleMVProfileProperty** -Methode wird eine mehrwertige Benutzerprofileigenschaft wie **SPS-Verantwortung**, die folgenden Schritte durch:</span><span class="sxs-lookup"><span data-stu-id="60766-215">The  **SetSingleMVProfileProperty** method sets a multivalued user profile property, such as **SPS-Responsibility**, by doing the following:</span></span>

- <span data-ttu-id="60766-216">Aufteilen von **PropertyValue** in ein Zeichenfolgenarray aufgerufen **Arrs** um User Profile-Eigenschaftswerte zu speichern.</span><span class="sxs-lookup"><span data-stu-id="60766-216">Splitting  **PropertyValue** into a string array called **arrs** to store user profile property values.</span></span> <span data-ttu-id="60766-217">Die Zeichenfolge wird bei Verwendung in ' App.config ' angegebenen Einstellung für die **PROPERTYSEPERATOR** geteilt.</span><span class="sxs-lookup"><span data-stu-id="60766-217">The string is split using the **PROPERTYSEPERATOR** configuration setting specified in App.Config.</span></span>
    
- <span data-ttu-id="60766-218">Zuweisen der Werte von **Arrs** in ein Array **ValueData** auf den Benutzerprofildienst.</span><span class="sxs-lookup"><span data-stu-id="60766-218">Assigning the values of  **arrs** to a **ValueData** array on the user profile service.</span></span>
    
- <span data-ttu-id="60766-219">Erstellen ein Array **PropertyData** auf den Benutzerprofildienst.</span><span class="sxs-lookup"><span data-stu-id="60766-219">Creating a  **PropertyData** array on the user profile service.</span></span> <span data-ttu-id="60766-220">Der Name der Benutzerprofileigenschaft und das Array **ValueData** werden Eigenschaften für das Objekt **PropertyData** übergeben.</span><span class="sxs-lookup"><span data-stu-id="60766-220">The name of the user profile property and the **ValueData** array are passed to properties on the **PropertyData** object.</span></span> <span data-ttu-id="60766-221">Dieses Array hat ein Element, da nur eine mehrwertige Benutzerprofileigenschaft importiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="60766-221">This array has one element only because only one multivalued user profile property will be imported.</span></span>
    
<span data-ttu-id="60766-222">Die Daten werden in der Verwendung von **ModifyUserPropertyByAccountName** auf dem **userprofileservice.asmx** -Webdienst in der SharePoint Online-Verwaltungskonsole Benutzerprofildienst geschrieben.</span><span class="sxs-lookup"><span data-stu-id="60766-222">The data is written to the user profile service using  **ModifyUserPropertyByAccountName** on the **userprofileservice.asmx** web service on the SharePoint Online admin center.</span></span> <span data-ttu-id="60766-223">Der Benutzer ein, der in diesem Codebeispiel muss ein Office 365-Administrator sein.</span><span class="sxs-lookup"><span data-stu-id="60766-223">The user running this code sample must be an Office 365 administrator.</span></span>

```C#
static void SetSingleMVProfileProperty(string UserName, string PropertyName, string PropertyValue)
        {

            try
            {
                string[] arrs = PropertyValue.Split(ConfigurationManager.AppSettings["PROPERTYSEPERATOR"][0]);
                
               UPSvc.ValueData[] vd = new UPSvc.ValueData[arrs.Count()];
               
               for (int i=0;i<=arrs.Count()-1;i++)
               {
                    vd[i] = new UPSvc.ValueData();
                    vd[i].Value = arrs[i];
                }
               
                UPSvc.PropertyData[] data = new UPSvc.PropertyData[1];
                data[0] = new UPSvc.PropertyData();
                data[0].Name = PropertyName;
                data[0].IsValueChanged = true;
                data[0].Values = vd;
                               
                _userProfileService.ModifyUserPropertyByAccountName(string.Format(@"i:0#.f|membership|{0}", UserName), data);

            }
            catch (Exception ex)
            {
                LogMessage("Exception trying to update profile property " + PropertyName + " for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }

        }

```

<span data-ttu-id="60766-224">Die **SetSingleValuedProperty** -Methode wird ein einwertiges Benutzerprofileigenschaften, wie **Mich-Seite**.</span><span class="sxs-lookup"><span data-stu-id="60766-224">The  **SetSingleValuedProperty** method sets single-valued user profile properties, such as **AboutMe**.</span></span>  <span data-ttu-id="60766-225">**SetSingleValuedProperty** das gleiche Verfahren als **SetSingleMVProfileProperty**implementiert, verwendet jedoch ein Array **ValueData** mit nur einem Element.</span><span class="sxs-lookup"><span data-stu-id="60766-225">**SetSingleValuedProperty** implements the same technique as **SetSingleMVProfileProperty**, but uses a  **ValueData** array with one element only.</span></span>

```C#
static void SetSingleProfileProperty(string UserName, string PropertyName, string PropertyValue)
        {

            try
            {
                UPSvc.PropertyData[] data = new UPSvc.PropertyData[1];
                data[0] = new UPSvc.PropertyData();
                data[0].Name = PropertyName;
                data[0].IsValueChanged = true;
                data[0].Values = new UPSvc.ValueData[1];
                data[0].Values[0] = new UPSvc.ValueData();
                data[0].Values[0].Value = PropertyValue;
                _userProfileService.ModifyUserPropertyByAccountName(UserName, data);
            }
            catch (Exception ex)
            {
                LogMessage("Exception trying to update profile property " + PropertyName + " for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }

        }

```

## <a name="see-also"></a><span data-ttu-id="60766-226">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="60766-226">See also</span></span>
<span data-ttu-id="60766-227"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="60766-227"></span></span>

-  [<span data-ttu-id="60766-228">User Profile Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="60766-228">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="60766-229">Core.ProfilePictureUploader</span><span class="sxs-lookup"><span data-stu-id="60766-229">Core.ProfilePictureUploader</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [<span data-ttu-id="60766-230">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="60766-230">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="60766-231">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="60766-231">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
