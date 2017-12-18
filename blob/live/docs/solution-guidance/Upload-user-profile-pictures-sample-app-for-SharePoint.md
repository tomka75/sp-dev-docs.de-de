---
title: "User Profile Bilder Beispiel-add-in für SharePoint hochladen"
ms.date: 11/03/2017
ms.openlocfilehash: ac6787f528d3f611d9eaecb415e8f48d7b392f53
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="upload-user-profile-pictures-sample-add-in-for-sharepoint"></a><span data-ttu-id="d6db4-102">User Profile Bilder Beispiel-add-in für SharePoint hochladen</span><span class="sxs-lookup"><span data-stu-id="d6db4-102">Upload user profile pictures sample add-in for SharePoint</span></span>

<span data-ttu-id="d6db4-103">Ein Add-in vom Anbieter gehosteten können Sie führen Sie einen Massenupload von Benutzerprofildaten von einer Dateifreigabe oder einem SharePoint Online-URL.</span><span class="sxs-lookup"><span data-stu-id="d6db4-103">You can use a provider-hosted add-in to do a bulk upload of user profile data from either a file share or SharePoint Online URL.</span></span>
    
<span data-ttu-id="d6db4-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="d6db4-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="d6db4-105">[Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) -Beispiel-add-in veranschaulicht eine Massenupload von Benutzerprofildaten von einer Dateifreigabe oder einem SharePoint Online-URL, und wie Sie Benutzerprofileigenschaften zu verknüpfenden Bilder hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-105">The [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) sample add-in shows how to do a bulk upload of user profile data from either a file share or SharePoint Online URL, and how to link user profile properties to uploaded images.</span></span>
    
<span data-ttu-id="d6db4-106">Verwenden Sie dieses Beispiel, erfahren, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="d6db4-106">Use this sample to learn how to:</span></span>

- <span data-ttu-id="d6db4-107">Migrieren eines Benutzers Profilbilder aus SharePoint Server 2013 lokal mit SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d6db4-107">Migrate a user's profile pictures from SharePoint Server 2013 on-premises to SharePoint Online.</span></span>
    
- <span data-ttu-id="d6db4-108">Beheben von Problemen, die auftreten, wenn das Tool Azure Active Directory-Synchronisierung (Dirsync) des Benutzers Profilbilder mit SharePoint Online synchronisiert nicht.</span><span class="sxs-lookup"><span data-stu-id="d6db4-108">Fix issues that occur when the Azure Active Directory Sync tool (dirsync) fails to synchronize user's profile pictures to SharePoint Online.</span></span>
    
- <span data-ttu-id="d6db4-109">Ersetzen Sie schlechter Qualität Benutzerprofilbilder in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d6db4-109">Replace poor quality user profile pictures in SharePoint Online.</span></span>
    
<span data-ttu-id="d6db4-110">In diesem Beispiel wird eine Konsolenanwendung verwendet, die folgenden Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="d6db4-110">This sample uses a console application to do the following:</span></span>

- <span data-ttu-id="d6db4-111">Lesen Sie den Benutzernamen und Bilddateipfade oder URLs aus einer Datei zur Zuordnung Benutzer.</span><span class="sxs-lookup"><span data-stu-id="d6db4-111">Read the user names and image file paths or URLs from a user mapping file.</span></span>
    
- <span data-ttu-id="d6db4-112">Abrufen und einen oder drei Bilder in einer Bildbibliothek auf Mein Websitehost hochladen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-112">Fetch and upload one or three images to a picture library on the My Site host.</span></span> 
    
- <span data-ttu-id="d6db4-113">Festlegen von Benutzerprofileigenschaften hochgeladene Bilder mit Profil eines Benutzers zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-113">Set user profile properties to link the uploaded images to a user's profile.</span></span>
    
- <span data-ttu-id="d6db4-114">Zusätzliche (optional) von Benutzerprofileigenschaften zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="d6db4-114">Update additional (optional) user profile properties.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="d6db4-115">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="d6db4-115">Before you begin</span></span>
<span data-ttu-id="d6db4-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="d6db4-116"></span></span>

<span data-ttu-id="d6db4-117">Laden Sie Sie zuerst [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6db4-117">To get started, download the  [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="d6db4-118">Bevor Sie dieses Codebeispiel ausführen:</span><span class="sxs-lookup"><span data-stu-id="d6db4-118">Before you run this code sample:</span></span>

- <span data-ttu-id="d6db4-119">Speichern Sie die Benutzerbilder, die Sie mit SharePoint Online auf einem Dateiserver freigeben oder den Webdienst hochladen möchten.</span><span class="sxs-lookup"><span data-stu-id="d6db4-119">Store your user images that you intend to upload to SharePoint Online on a file share or web server.</span></span> 
    
- <span data-ttu-id="d6db4-120">Bearbeiten Sie die userlist.csv-Datei, um Folgendes umfassen:</span><span class="sxs-lookup"><span data-stu-id="d6db4-120">Edit the userlist.csv file to include the following:</span></span>
    
    - <span data-ttu-id="d6db4-121">Eine Überschriftenzeile mit dem Wert **UserPrincipalName**, **SourceURL**.</span><span class="sxs-lookup"><span data-stu-id="d6db4-121">A header row containing the value  **UserPrincipalName**,  **SourceURL**.</span></span>
    
    - <span data-ttu-id="d6db4-122">Fügen Sie für jeden Benutzer eine neue Zeile, enthält das Konto des Benutzers Organisationseinheit (oder Benutzerprinzipalname) und den Dateipfad oder die URL des Bilds hochladen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-122">For each user, add a new row containing the user's organizational account (or user principal name) and the file path or URL of the image to upload.</span></span> 
    
- <span data-ttu-id="d6db4-123">Konfigurieren Sie zum Ausführen dieses Beispiels aus Visual Studio das Projekt **Core.ProfilePictureUploader** mit den folgenden Befehlszeilenargumente:`-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`</span><span class="sxs-lookup"><span data-stu-id="d6db4-123">To run this sample from Visual Studio, configure the  **Core.ProfilePictureUploader** project with the following command-line arguments: `-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`</span></span>
    
  <span data-ttu-id="d6db4-124">Dabei gilt:</span><span class="sxs-lookup"><span data-stu-id="d6db4-124">Where:</span></span>
    
    - <span data-ttu-id="d6db4-125">*Benutzername* ist Benutzername Ihre Office 365-Administrator.</span><span class="sxs-lookup"><span data-stu-id="d6db4-125">*Username* is your Office 365 administrator's username.</span></span>
    
    - <span data-ttu-id="d6db4-126">*Kennwort* ist der Office 365-Administrator Kennwort.</span><span class="sxs-lookup"><span data-stu-id="d6db4-126">*Password* is your Office 365 administrator's password.</span></span>
    
    - <span data-ttu-id="d6db4-127">*FilePath* ist der Pfad der Datei "Configuration.xml".</span><span class="sxs-lookup"><span data-stu-id="d6db4-127">*Filepath* is the file path of the configuration.xml file.</span></span>
    
- <span data-ttu-id="d6db4-128">So legen Sie die Befehlszeilenargumente für das Projekt Core.ProfilePictureUploader fest</span><span class="sxs-lookup"><span data-stu-id="d6db4-128">To set the command-line arguments on the Core.ProfilePictureUploader project:</span></span>
    
    - <span data-ttu-id="d6db4-129">Öffnen Sie im Projektmappen-Explorer das Kontextmenü (klicken Sie rechts) für das Projekt **Core.ProfilePictureUploader** > **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="d6db4-129">In Solution Explorer, open the shortcut menu (right click) for the  **Core.ProfilePictureUploader** project > **Properties**.</span></span>
    
    - <span data-ttu-id="d6db4-130">Wählen Sie **Debuggen**.</span><span class="sxs-lookup"><span data-stu-id="d6db4-130">Choose  **Debug**.</span></span>
    
    - <span data-ttu-id="d6db4-131">Geben Sie im **Befehlszeilenargumente**die zuvor aufgeführten Befehlszeilenargumente.</span><span class="sxs-lookup"><span data-stu-id="d6db4-131">In  **Command line arguments**, enter the command-line arguments listed earlier.</span></span>
    
- <span data-ttu-id="d6db4-132">Bearbeiten Sie die Datei "Configuration.xml", indem Sie die folgenden Werte eingeben, um während des Uploads Ihre Bedürfnisse zugeschnitten konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="d6db4-132">To configure the upload process to meet your requirements, edit the configuration.xml file by entering the following values:</span></span>
    
    - <span data-ttu-id="d6db4-133">Der Name Ihres Office 365-Mandanten im **TenantName** -Element.</span><span class="sxs-lookup"><span data-stu-id="d6db4-133">The name of your Office 365 tenant in the  **tenantName** element.</span></span> <span data-ttu-id="d6db4-134">Zum Beispiel:`<tenantName>contoso.onmicrosoft.com</tenantName>`</span><span class="sxs-lookup"><span data-stu-id="d6db4-134">For example: `<tenantName>contoso.onmicrosoft.com</tenantName>`</span></span>
    
    - <span data-ttu-id="d6db4-135">Der Benutzer Zuordnung-Dateipfad im **PictureSourceCsv** -Element.</span><span class="sxs-lookup"><span data-stu-id="d6db4-135">The user mapping file path in the  **pictureSourceCsv** element.</span></span> <span data-ttu-id="d6db4-136">Zum Beispiel:`<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`</span><span class="sxs-lookup"><span data-stu-id="d6db4-136">For example: `<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`</span></span>
    
    - <span data-ttu-id="d6db4-137">Bild hochladen Anweisungen mithilfe des **Daumen** -Elements.</span><span class="sxs-lookup"><span data-stu-id="d6db4-137">Image upload instructions using the  **thumbs** element.</span></span> <span data-ttu-id="d6db4-138">Bearbeiten Sie die folgenden Attribute im Daumen-Element:</span><span class="sxs-lookup"><span data-stu-id="d6db4-138">Edit the following attributes in the thumbs element:</span></span>
    
        -  <span data-ttu-id="d6db4-139">**aupload3Thumbs** - auf **true** festgelegt, wenn Sie für jeden Benutzer drei Bilder hochladen, oder auf **false** festgelegt, wenn Sie ein Bild hochladen möchten möchten.</span><span class="sxs-lookup"><span data-stu-id="d6db4-139">**aupload3Thumbs** - Set to **true** if you want to upload three images for each user, or set to **false** if you only want to upload one image.</span></span>
    
        -  <span data-ttu-id="d6db4-140">**CreateSMLThumbs** - Wenn Sie drei verschiedene erstellen möchten Größe auf **true** festgelegt Bilder (kleine, mittlere und große) der Quelle ein Bild oder auf **false** festgelegt, wenn Sie drei Bildern dieselbe Größe hochladen möchten.</span><span class="sxs-lookup"><span data-stu-id="d6db4-140">**createSMLThumbs** - Set to **true** if you want to create three different sized images (small, medium, and large) of the source image, or set to **false** if you want to upload three images of the same size.</span></span>
    
    - <span data-ttu-id="d6db4-141">Festlegen zusätzlicher Eigenschaften, auf das Profil des Benutzers mithilfe des **AdditionalProfilePropties** -Elements.</span><span class="sxs-lookup"><span data-stu-id="d6db4-141">Additional properties to set on the user's profile using the  **additionalProfilePropties** element.</span></span> <span data-ttu-id="d6db4-142">Der folgende XML-Code gibt beispielsweise eine zusätzliche Benutzerprofileigenschaft aufgerufen **SPS-PictureExchangeSyncState** , die beim Ausführen im Codebeispiels für das Profil des Benutzers auf NULL festgelegt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="d6db4-142">For example, the following XML specifies an additional user profile property called **SPS-PictureExchangeSyncState** that should be set to zero on the user's profile when the code sample runs.</span></span>

    ```
    <additionalProfileProperties>
         <property name="SPS-PictureExchangeSyncState" value="0"/>
    </additionalProfileProperties>
    ```

  - <span data-ttu-id="d6db4-143">Pfad der Protokolldatei in der **Protokolldatei** -Element, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="d6db4-143">The log file path in the  **logfile** element, as shown in the following example.</span></span> `<logFile path="C:\temp\log.txt" enableLogging="true" loggingLevel="verbose" />`
    
  - <span data-ttu-id="d6db4-144">Der Upload Verzögerung in Millisekunden zwischen der Upload von anderen Bilddateien mithilfe des **UploadDelay** -Elements.</span><span class="sxs-lookup"><span data-stu-id="d6db4-144">The upload delay in milliseconds between the upload of different image files using the  **uploadDelay** element.</span></span> <span data-ttu-id="d6db4-145">Die empfohlene Einstellung für **UploadDelay** beträgt 500 Millisekunden.</span><span class="sxs-lookup"><span data-stu-id="d6db4-145">The recommended setting for **uploadDelay** is 500 milliseconds.</span></span>
    
- <span data-ttu-id="d6db4-146">Ändern Sie in der Datei App.config das **Value** -Element der **ProfilePictureUploader_UPSvc_UserProfileService** Einstellung, die einen Verweis auf den Benutzerprofildienst in Ihrer SharePoint Online-Verwaltungskonsole enthalten.</span><span class="sxs-lookup"><span data-stu-id="d6db4-146">In the App.config file, change the  **value** element of the **ProfilePictureUploader_UPSvc_UserProfileService** setting to include a reference to the user profile service in your SharePoint Online admin center.</span></span> <span data-ttu-id="d6db4-147">wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="d6db4-147">as shown in the following example.</span></span>

```XML  
<Contoso.Core.ProfilePictureUploader.Properties.Settings>
      <setting name="ProfilePictureUploader_UPSvc_UserProfileService"
            serializeAs="String">
            <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
      </setting>
 </Contoso.Core.ProfilePictureUploader.Properties.Settings>
```

<span data-ttu-id="d6db4-148">**Wichtige**  Herstellen einer Verbindung mit dem userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole können Sie die Benutzerprofileigenschaften von anderen Benutzern zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="d6db4-148">**Important**  Connecting to the userprofileservice.asmx web service on the SharePoint Online admin center allows you to update the user profile properties of other users.</span></span> <span data-ttu-id="d6db4-149">Wenn Sie dieses Codebeispiel ausführen, verwenden Sie ein Office 365-Administratorkonto, das über Berechtigungen zum Verwalten von Benutzerprofilen verfügt.</span><span class="sxs-lookup"><span data-stu-id="d6db4-149">When you run this code sample, use an Office 365 administrator account that has permissions to manage user profiles.</span></span> 

## <a name="using-the-coreprofilepictureuploader-app"></a><span data-ttu-id="d6db4-150">Verwenden der app Core.ProfilePictureUploader</span><span class="sxs-lookup"><span data-stu-id="d6db4-150">Using the Core.ProfilePictureUploader app</span></span>
<span data-ttu-id="d6db4-151"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="d6db4-151"></span></span>

<span data-ttu-id="d6db4-152">In diesem Codebeispiel wird als Konsolenanwendung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d6db4-152">This code sample runs as a console application.</span></span> <span data-ttu-id="d6db4-153">Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Methode in Program.cs Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="d6db4-153">When the code sample runs, the  **Main** method in Program.cs does the following:</span></span>

- <span data-ttu-id="d6db4-154">Initialisiert die Konsolenanwendung **SetupArguments** und **InitializeConfiguration**verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6db4-154">Initializes the console application using  **SetupArguments** and **InitializeConfiguration**.</span></span> 
    
- <span data-ttu-id="d6db4-155">Ruft **InitializeWebService** Verbindung mit dem Benutzerprofildienst in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d6db4-155">Calls  **InitializeWebService** to connect to the user profile service in SharePoint Online.</span></span>
    
- <span data-ttu-id="d6db4-156">Durchlaufen und die Datei userlist.csv den Benutzerprinzipalnamen (UPN) für den Benutzer und den Speicherort der Bilddatei des Benutzers zu lesen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-156">Iterates through the userlist.csv file to read the user principal name (UPN) for the user and the location of the user's image file.</span></span> 
    
- <span data-ttu-id="d6db4-157">Ruft **WebRequest** und **WebResponse** -Objekte in **GetImagefromHTTPUrl**mithilfe eines Benutzers Bild ab.</span><span class="sxs-lookup"><span data-stu-id="d6db4-157">Fetches a user's image using  **WebRequest** and **WebResponse** objects in **GetImagefromHTTPUrl**.</span></span>
    
- <span data-ttu-id="d6db4-158">Ruft die **UploadImageToSpo** , um das Bild des Benutzers in SharePoint Online hoch.</span><span class="sxs-lookup"><span data-stu-id="d6db4-158">Calls  **UploadImageToSpo** to upload the user's image to SharePoint Online.</span></span>
    
- <span data-ttu-id="d6db4-159">Ruft die **SetMultipleProfileProperties** , um den **Bild-URL** und **SPS-PicturePlaceholderState** Benutzer Profileigenschaften für den Benutzer festzulegen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-159">Calls  **SetMultipleProfileProperties** to set the **PictureURL** and **SPS-PicturePlaceholderState** user profile properties for the user.</span></span>
    
- <span data-ttu-id="d6db4-160">Ruft die **SetAdditionalProfileProperties** , um zusätzliche Eigenschaften im Benutzerprofil festzulegen, nachdem die Datei hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="d6db4-160">Calls  **SetAdditionalProfileProperties** to set additional properties on the user profile after the image file is uploaded.</span></span>

> [!NOTE] 
> <span data-ttu-id="d6db4-161">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="d6db4-161">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
static void Main(string[] args)
        {
            int count = 0;

            if (SetupArguments(args)) // Checks if args passed are valid 
            {

                if (InitializeConfiguration()) // Check that the configuration file is valid
                {
                    if (InitializeWebService()) // Initialize the web service end point for the SharePoint Online user profile service.
                    {
                        
                        using (StreamReader readFile = new StreamReader(_appConfig.PictureSourceCsv))
                        {
                            string line;
                            string[] row;
                            string sPoUserProfileName;
                            string sourcePictureUrl;

                            while ((line = readFile.ReadLine()) != null)
                            {
                                if (count > 0)
                                {
                                    row = line.Split(',');
                                    sPoUserProfileName = row[0]; 
                                    sourcePictureUrl = row[1]; 

                                    LogMessage("Begin processing for user " + sPoUserProfileName, LogLevel.Warning);

                                    // Get source picture from source image path.
                                    using (MemoryStream picturefromExchange = GetImagefromHTTPUrl(sourcePictureUrl))
                                    {
                                        if (picturefromExchange != null) // if we got image, upload to SharePoint Online
                                        {
                                            // Create SharePoint naming convention for image file.
                                            string newImageNamePrefix = sPoUserProfileName.Replace("@", "_").Replace(".", "_");
                                            // Upload source image to SharePoint Online.
                                            string spoImageUrl = UploadImageToSpo(newImageNamePrefix, picturefromExchange);
                                            if (spoImageUrl.Length > 0)// If upload worked.
                                            {
                                                string[] profilePropertyNamesToSet = new string[] { "PictureURL", "SPS-PicturePlaceholderState" };
                                                string[] profilePropertyValuesToSet = new string[] { spoImageUrl, "0" };
                                                // Set these two required user profile properties - path to uploaded image, and pictureplaceholder state.
                                                SetMultipleProfileProperties(_sPOProfilePrefix + sPoUserProfileName, profilePropertyNamesToSet, profilePropertyValuesToSet);
                                                // Set additional user profile properties based on your requirements.
                                                SetAdditionalProfileProperties(_sPOProfilePrefix + sPoUserProfileName);
                                            }
                                        }
                                    }

                                    LogMessage("End processing for user " + sPoUserProfileName, LogLevel.Warning);

                                    int sleepTime = _appConfig.UploadDelay;
                                    System.Threading.Thread.Sleep(sleepTime); // A pause between uploads is recommended. 
                                }
                                count++;
                            }
                        }
                    }
                }
            }


            LogMessage("Processing finished for " + count + " user profiles", LogLevel.Information);
         } 

```

<span data-ttu-id="d6db4-162">**InitializeWebService** stellt eine Verbindung mit SharePoint Online, und einen Verweis auf den Benutzerprofildienst auf eine Instanzvariable festgelegt.</span><span class="sxs-lookup"><span data-stu-id="d6db4-162">**InitializeWebService** connects to SharePoint Online, and sets a reference of the user profile service to an instance variable.</span></span> <span data-ttu-id="d6db4-163">Andere Methoden in diesem Codebeispiel verwenden Sie diese Instanzvariable zum Anwenden von Updates auf Benutzerprofileigenschaften.</span><span class="sxs-lookup"><span data-stu-id="d6db4-163">Other methods in this code sample use this instance variable to apply updates to user profile properties.</span></span> <span data-ttu-id="d6db4-164">Um das Benutzerprofil zu verwalten, verwendet dieses Codebeispiel den userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole.</span><span class="sxs-lookup"><span data-stu-id="d6db4-164">To administer the user profile, this code sample uses the userprofileservice.asmx web service in the SharePoint Online admin center.</span></span>

```
static bool InitializeWebService()
        {
            try
            {
                string webServiceExt = "_vti_bin/userprofileservice.asmx";
                string adminWebServiceUrl = string.Empty;

                // Append the web service (ASMX) URL onto the admin website URL.
                if (_profileSiteUrl.EndsWith("/"))
                    adminWebServiceUrl = _profileSiteUrl + webServiceExt;
                else
                    adminWebServiceUrl = _profileSiteUrl + "/" + webServiceExt;

                LogMessage("Initializing SPO web service " + adminWebServiceUrl, LogLevel.Information);

                // Get secure password from clear text password.
                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);

                // Set credentials from SharePoint Client API, used later to extract authentication cookie, so can replay to web services.
                SharePointOnlineCredentials onlineCred = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);

                // Get the authentication cookie by passing the URL of the admin website. 
                string authCookie = onlineCred.GetAuthenticationCookie(new Uri(_profileSiteUrl));

                // Create a CookieContainer to authenticate against the web service. 
                CookieContainer authContainer = new CookieContainer();

                // Put the authenticationCookie string in the container. 
                authContainer.SetCookies(new Uri(_profileSiteUrl), authCookie);

                // Setting up the user profile web service. 
                _userProfileService = new UPSvc.UserProfileService();

                // Assign the correct URL to the admin profile web service. 
                _userProfileService.Url = adminWebServiceUrl;

                // Assign previously created authentication container to admin profile web service. 
                _userProfileService.CookieContainer = authContainer;
               // LogMessage("Finished creating service object for SharePoint Online Web Service " + adminWebServiceUrl, LogLevel.Information);
                return true;
            }
            catch (Exception ex)
            {
                LogMessage("Error initiating connection to profile web service in SPO " + ex.Message, LogLevel.Error);
                return false;

            }

            
        }

```

<span data-ttu-id="d6db4-165">Die **Main** -Methode in Program.cs ruft **UploadImageToSpo** , um die benutzerprofilbilds in SharePoint Online hoch.</span><span class="sxs-lookup"><span data-stu-id="d6db4-165">The  **Main** method in Program.cs calls **UploadImageToSpo** to upload the user's profile picture to SharePoint Online.</span></span> <span data-ttu-id="d6db4-166">Profilbilder für alle Benutzer werden in einer Bildbibliothek auf Mein Websitehost gespeichert.</span><span class="sxs-lookup"><span data-stu-id="d6db4-166">All users' profile pictures are stored in a picture library on the My Site Host.</span></span> <span data-ttu-id="d6db4-167">**UploadImageToSpo** führt die folgenden Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="d6db4-167">**UploadImageToSpo** performs the following tasks:</span></span>

- <span data-ttu-id="d6db4-168">Verbindet mit SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d6db4-168">Connects to SharePoint Online.</span></span>
    
- <span data-ttu-id="d6db4-169">Bestimmt die Anzahl der Bilder für jeden Benutzer hochladen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-169">Determines the number of images to upload for each user.</span></span> 
    
    - <span data-ttu-id="d6db4-170">Wenn Sie die Anwendung zum Hochladen einer Grafik pro Benutzer konfiguriert haben, wird das Bild in die Bildbibliothek hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-170">If you configured the application to upload one image per user, the image is uploaded to the picture library.</span></span> 
    
    - <span data-ttu-id="d6db4-171">Wenn Sie die Anwendung zum Hochladen von drei Bilder pro Benutzer konfiguriert haben, überprüft die Anwendung den Wert des **CreateSMLThumbs** in der Konfigurationsdatei, um festzustellen, ob die drei verschiedene Größe Bilder erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="d6db4-171">If you configured the application to upload three images per user, the application checks the value of  **createSMLThumbs** in the configuration file to determine whether three different sized images are required.</span></span> <span data-ttu-id="d6db4-172">Drei verschiedene Größe Bilder erforderlich sind, verwendet die Anwendung **ResizeImageSmall** und **ResizeImageLarge** auf um drei verschiedene Größe Bilder aus diesem Quellabbild zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6db4-172">If three different sized images are required, the application uses **ResizeImageSmall** and **ResizeImageLarge** to create three different sized images from the source image.</span></span> <span data-ttu-id="d6db4-173">Die Anwendung dann hochgeladen dessen Größe angepasst wurde Bilder in die Bildbibliothek.</span><span class="sxs-lookup"><span data-stu-id="d6db4-173">The application then uploads the resized images to the picture library.</span></span> <span data-ttu-id="d6db4-174">Wenn Sie drei verschiedene Größe Bilder nicht erforderlich sind, hochgeladen die Anwendung drei Bildern dieselbe Größe die Bildbibliothek.</span><span class="sxs-lookup"><span data-stu-id="d6db4-174">If three different sized images are not required, the application uploads three images of the same size to the picture library.</span></span>

```C#
static string UploadImageToSpo(string PictureName, Stream ProfilePicture)
        {
            try
            {

                string spPhotoPathTempate = "/User Photos/Profile Pictures/{0}_{1}Thumb.jpg"; // Path template to picture library on the My Site Host.
                string spImageUrl = string.Empty;

                // Create SharePoint Online Client context to My Site Host.
                ClientContext mySiteclientContext = new ClientContext(_mySiteUrl);
                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);
                // Provide authentication credentials using Office 365 authentication.
                mySiteclientContext.Credentials = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);
                                
                if (!_appConfig.Thumbs.Upload3Thumbs) // Upload a single input image only to picture library, no resizing necessary.
                {
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                    LogMessage("Uploading single image, no resize, to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);
                }
                else if (_appConfig.Thumbs.Upload3Thumbs &amp;&amp; !_appConfig.Thumbs.CreateSMLThumbs)// Upload three images of the same size. 
                {
                    // The following code is not optimal. Upload the same source image three times with different names.
                    // No resizing of images necessary.
                    LogMessage("Uploading threes image to SPO, no resize", LogLevel.Information);

                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                    LogMessage("Uploading medium image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);

                    ProfilePicture.Seek(0, SeekOrigin.Begin);
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "L");
                    LogMessage("Uploading large image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);
                    
                    ProfilePicture.Seek(0, SeekOrigin.Begin);
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "S");
                    LogMessage("Uploading small image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);

                    
                }
                else if (_appConfig.Thumbs.Upload3Thumbs &amp;&amp; _appConfig.Thumbs.CreateSMLThumbs) //generate 3 different sized images
                {
                    LogMessage("Uploading threes image to SPO, with resizing", LogLevel.Information);
                    // Create three images based on recommended sizes for SharePoint Online.
                    // Create small-sized image.
                    using (Stream smallThumb = ResizeImageSmall(ProfilePicture, _smallThumbWidth))
                    {
                        if (smallThumb != null)
                        {
                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "S");
                            LogMessage("Uploading small image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, smallThumb, true);                            
                        }
                    }

                    // Create medium-sized image.
                    using (Stream mediumThumb = ResizeImageSmall(ProfilePicture, _mediumThumbWidth))
                    {
                        if (mediumThumb != null)
                        {
                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                            LogMessage("Uploading medium image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, mediumThumb, true);
                           
                        }
                    }

                    // Create large-sized image. This image is shown when you open the user's OneDrive for Business. 
                    using (Stream largeThumb = ResizeImageLarge(ProfilePicture, _largeThumbWidth))
                    {
                        if (largeThumb != null)
                        {

                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "L");
                            LogMessage("Uploading large image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, largeThumb, true);
                            
                        }
                    }
                  
                   
                }
                // Return URL of the medium-sized image to set properties on the user profile.
                return _mySiteUrl + string.Format(spPhotoPathTempate, PictureName, "M");                
                
            }
            catch (Exception ex)
            {
                LogMessage("User Error: Failed to upload thumbnail picture to SPO for " + PictureName + " " + ex.Message, LogLevel.Error);
                return string.Empty;
            }

        }

```

<span data-ttu-id="d6db4-175">**SetMultipleProfileProperties** festgelegt mehrere Benutzer Profileigenschaften in einem einzelnen Methodenaufruf.</span><span class="sxs-lookup"><span data-stu-id="d6db4-175">**SetMultipleProfileProperties** sets multiple user profile properties in a single method call.</span></span> <span data-ttu-id="d6db4-176">In diesem Codebeispiel legt **SetMultipleProfileProperties** die folgenden Benutzerprofileigenschaften für einen Benutzer fest:</span><span class="sxs-lookup"><span data-stu-id="d6db4-176">In this code sample, **SetMultipleProfileProperties** sets the following user profile properties for a user:</span></span>

-  <span data-ttu-id="d6db4-177">**Bild-URL** - legen Sie auf die URL des Bilds hochgeladenen mittlerer Größe in die Bildbibliothek auf Mein Websitehost.</span><span class="sxs-lookup"><span data-stu-id="d6db4-177">**PictureURL** - Set to the URL of the medium-sized uploaded image in the picture library on the My Site Host.</span></span>
    
-  <span data-ttu-id="d6db4-178">**SPS-PicturePlaceholderState** - auf NULL gesetzt, um anzugeben, dass SharePoint Online das hochgeladene Bild für den Benutzer angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d6db4-178">**SPS-PicturePlaceholderState** - Set to zero to indicate that SharePoint Online should show the uploaded picture for the user.</span></span>

```C#
static void SetMultipleProfileProperties(string UserName, string[] PropertyName, string[] PropertyValue)
        {

            LogMessage("Setting multiple SPO user profile properties for " + UserName, LogLevel.Information);

            try
            {
                int arrayCount = PropertyName.Count();

                UPSvc.PropertyData[] data = new UPSvc.PropertyData[arrayCount];
                for (int x = 0; x < arrayCount; x++)
                {
                    data[x] = new UPSvc.PropertyData();
                    data[x].Name = PropertyName[x];
                    data[x].IsValueChanged = true;
                    data[x].Values = new UPSvc.ValueData[1];
                    data[x].Values[0] = new UPSvc.ValueData();
                    data[x].Values[0].Value = PropertyValue[x];
                }

                _userProfileService.ModifyUserPropertyByAccountName(UserName, data);
                // LogMessage("Finished setting multiple SharePoint Online user profile properties for " + UserName, LogLevel.Information);

            }
            catch (Exception ex)
            {
                LogMessage("User Error: Exception trying to update profile properties for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }
        }

```

<span data-ttu-id="d6db4-179">**SetAdditionalProfileProperties** wird zusätzliche Profileigenschaften, den, die Sie nach dem Hochladen der Bilddateien aktualisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="d6db4-179">**SetAdditionalProfileProperties** sets any additional user profile properties you want to update after uploading the image files.</span></span> <span data-ttu-id="d6db4-180">Sie können zusätzliche Eigenschaften so aktualisieren Sie in der Datei "Configuration.xml" angeben.</span><span class="sxs-lookup"><span data-stu-id="d6db4-180">You can specify additional properties to update in the configuration.xml file.</span></span>

```C#
static void SetAdditionalProfileProperties(string UserName)
        {
            if (_appConfig.AdditionalProfileProperties.Properties == null) // If there are no additional properties to update. 
                return;

            int propsCount = _appConfig.AdditionalProfileProperties.Properties.Count();
            if (propsCount > 0)
            {
                string[] profilePropertyNamesToSet = new string[propsCount];
                string[] profilePropertyValuesToSet = new string[propsCount];
                // Loop through each property in configuration file.
                for (int i = 0; i < propsCount; i++)
                {
                    profilePropertyNamesToSet[i] = _appConfig.AdditionalProfileProperties.Properties[i].Name;
                    profilePropertyValuesToSet[i] = _appConfig.AdditionalProfileProperties.Properties[i].Value;
                }

                // Set all properties in a single call.
                SetMultipleProfileProperties(UserName, profilePropertyNamesToSet, profilePropertyValuesToSet);

            }
        }

```

## <a name="see-also"></a><span data-ttu-id="d6db4-181">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d6db4-181">See also</span></span>
<span data-ttu-id="d6db4-182"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d6db4-182"></span></span>

-  [<span data-ttu-id="d6db4-183">User Profile Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="d6db4-183">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="d6db4-184">Core.ProfilePictureUploader-app</span><span class="sxs-lookup"><span data-stu-id="d6db4-184">Core.ProfilePictureUploader app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [<span data-ttu-id="d6db4-185">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="d6db4-185">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="d6db4-186">Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="d6db4-186">Core.ProfileProperty.Migration</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
    
-  [<span data-ttu-id="d6db4-187">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="d6db4-187">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
