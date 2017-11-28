---
title: "User Profile Bilder Beispiel-add-in für SharePoint hochladen"
ms.date: 11/03/2017
ms.openlocfilehash: 0897ded60ef98f019450e73860685d014afc7834
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="upload-user-profile-pictures-sample-add-in-for-sharepoint"></a>User Profile Bilder Beispiel-add-in für SharePoint hochladen

Ein Add-in vom Anbieter gehosteten können Sie führen Sie einen Massenupload von Benutzerprofildaten von einer Dateifreigabe oder einem SharePoint Online-URL.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
[Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) -Beispiel-add-in veranschaulicht eine Massenupload von Benutzerprofildaten von einer Dateifreigabe oder einem SharePoint Online-URL, und wie Sie Benutzerprofileigenschaften zu verknüpfenden Bilder hochgeladen.
    
Verwenden Sie dieses Beispiel, erfahren, wie Sie:

- Migrieren eines Benutzers Profilbilder aus SharePoint Server 2013 lokal mit SharePoint Online.
    
- Beheben von Problemen, die auftreten, wenn das Tool Azure Active Directory-Synchronisierung (Dirsync) des Benutzers Profilbilder mit SharePoint Online synchronisiert nicht.
    
- Ersetzen Sie schlechter Qualität Benutzerprofilbilder in SharePoint Online.
    
In diesem Beispiel wird eine Konsolenanwendung verwendet, die folgenden Aufgaben ausführen:

- Lesen Sie den Benutzernamen und Bilddateipfade oder URLs aus einer Datei zur Zuordnung Benutzer.
    
- Abrufen und einen oder drei Bilder in einer Bildbibliothek auf Mein Websitehost hochladen. 
    
- Festlegen von Benutzerprofileigenschaften hochgeladene Bilder mit Profil eines Benutzers zu verknüpfen.
    
- Zusätzliche (optional) von Benutzerprofileigenschaften zu aktualisieren.
    
## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie dieses Codebeispiel ausführen:

- Speichern Sie die Benutzerbilder, die Sie mit SharePoint Online auf einem Dateiserver freigeben oder den Webdienst hochladen möchten. 
    
- Bearbeiten Sie die userlist.csv-Datei, um Folgendes umfassen:
    
    - Eine Überschriftenzeile mit dem Wert **UserPrincipalName**, **SourceURL**.
    
    - Fügen Sie für jeden Benutzer eine neue Zeile, enthält das Konto des Benutzers Organisationseinheit (oder Benutzerprinzipalname) und den Dateipfad oder die URL des Bilds hochladen. 
    
- Konfigurieren Sie zum Ausführen dieses Beispiels aus Visual Studio das Projekt **Core.ProfilePictureUploader** mit den folgenden Befehlszeilenargumente:`-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`
    
  Dabei gilt:
    
    - *Benutzername* ist Benutzername Ihre Office 365-Administrator.
    
    - *Kennwort* ist der Office 365-Administrator Kennwort.
    
    - *FilePath* ist der Pfad der Datei "Configuration.xml".
    
- So legen Sie die Befehlszeilenargumente für das Projekt Core.ProfilePictureUploader fest
    
    - Öffnen Sie im Projektmappen-Explorer das Kontextmenü (klicken Sie rechts) für das Projekt **Core.ProfilePictureUploader** > **Eigenschaften**.
    
    - Wählen Sie **Debuggen**.
    
    - Geben Sie im **Befehlszeilenargumente**die zuvor aufgeführten Befehlszeilenargumente.
    
- Bearbeiten Sie die Datei "Configuration.xml", indem Sie die folgenden Werte eingeben, um während des Uploads Ihre Bedürfnisse zugeschnitten konfigurieren:
    
    - Der Name Ihres Office 365-Mandanten im **TenantName** -Element. Zum Beispiel:`<tenantName>contoso.onmicrosoft.com</tenantName>`
    
    - Der Benutzer Zuordnung-Dateipfad im **PictureSourceCsv** -Element. Zum Beispiel:`<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`
    
    - Bild hochladen Anweisungen mithilfe des **Daumen** -Elements. Bearbeiten Sie die folgenden Attribute im Daumen-Element:
    
        -  **aupload3Thumbs** - auf **true** festgelegt, wenn Sie für jeden Benutzer drei Bilder hochladen, oder auf **false** festgelegt, wenn Sie ein Bild hochladen möchten möchten.
    
        -  **CreateSMLThumbs** - Wenn Sie drei verschiedene erstellen möchten Größe auf **true** festgelegt Bilder (kleine, mittlere und große) der Quelle ein Bild oder auf **false** festgelegt, wenn Sie drei Bildern dieselbe Größe hochladen möchten.
    
    - Festlegen zusätzlicher Eigenschaften, auf das Profil des Benutzers mithilfe des **AdditionalProfilePropties** -Elements. Der folgende XML-Code gibt beispielsweise eine zusätzliche Benutzerprofileigenschaft aufgerufen **SPS-PictureExchangeSyncState** , die beim Ausführen im Codebeispiels für das Profil des Benutzers auf NULL festgelegt werden sollte.

    ```
    <additionalProfileProperties>
         <property name="SPS-PictureExchangeSyncState" value="0"/>
    </additionalProfileProperties>
    ```

  - Pfad der Protokolldatei in der **Protokolldatei** -Element, wie im folgenden Beispiel dargestellt. `<logFile path="C:\temp\log.txt" enableLogging="true" loggingLevel="verbose" />`
    
  - Der Upload Verzögerung in Millisekunden zwischen der Upload von anderen Bilddateien mithilfe des **UploadDelay** -Elements. Die empfohlene Einstellung für **UploadDelay** beträgt 500 Millisekunden.
    
- Ändern Sie in der Datei App.config das **Value** -Element der **ProfilePictureUploader_UPSvc_UserProfileService** Einstellung, die einen Verweis auf den Benutzerprofildienst in Ihrer SharePoint Online-Verwaltungskonsole enthalten. wie im folgenden Beispiel dargestellt.

```XML  
<Contoso.Core.ProfilePictureUploader.Properties.Settings>
      <setting name="ProfilePictureUploader_UPSvc_UserProfileService"
            serializeAs="String">
            <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
      </setting>
 </Contoso.Core.ProfilePictureUploader.Properties.Settings>
```

**Wichtige**  Herstellen einer Verbindung mit dem userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole können Sie die Benutzerprofileigenschaften von anderen Benutzern zu aktualisieren. Wenn Sie dieses Codebeispiel ausführen, verwenden Sie ein Office 365-Administratorkonto, das über Berechtigungen zum Verwalten von Benutzerprofilen verfügt. 

## <a name="using-the-coreprofilepictureuploader-app"></a>Verwenden der app Core.ProfilePictureUploader
<a name="sectionSection1"> </a>

In diesem Codebeispiel wird als Konsolenanwendung ausgeführt. Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Methode in Program.cs Folgendes aus:

- Initialisiert die Konsolenanwendung **SetupArguments** und **InitializeConfiguration**verwenden. 
    
- Ruft **InitializeWebService** Verbindung mit dem Benutzerprofildienst in SharePoint Online.
    
- Durchlaufen und die Datei userlist.csv den Benutzerprinzipalnamen (UPN) für den Benutzer und den Speicherort der Bilddatei des Benutzers zu lesen. 
    
- Ruft **WebRequest** und **WebResponse** -Objekte in **GetImagefromHTTPUrl**mithilfe eines Benutzers Bild ab.
    
- Ruft die **UploadImageToSpo** , um das Bild des Benutzers in SharePoint Online hoch.
    
- Ruft die **SetMultipleProfileProperties** , um den **Bild-URL** und **SPS-PicturePlaceholderState** Benutzer Profileigenschaften für den Benutzer festzulegen.
    
- Ruft die **SetAdditionalProfileProperties** , um zusätzliche Eigenschaften im Benutzerprofil festzulegen, nachdem die Datei hochgeladen wurde.

**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

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

**InitializeWebService** stellt eine Verbindung mit SharePoint Online, und einen Verweis auf den Benutzerprofildienst auf eine Instanzvariable festgelegt. Andere Methoden in diesem Codebeispiel verwenden Sie diese Instanzvariable zum Anwenden von Updates auf Benutzerprofileigenschaften. Um das Benutzerprofil zu verwalten, verwendet dieses Codebeispiel den userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole.

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

Die **Main** -Methode in Program.cs ruft **UploadImageToSpo** , um die benutzerprofilbilds in SharePoint Online hoch. Profilbilder für alle Benutzer werden in einer Bildbibliothek auf Mein Websitehost gespeichert. **UploadImageToSpo** führt die folgenden Aufgaben:

- Verbindet mit SharePoint Online.
    
- Bestimmt die Anzahl der Bilder für jeden Benutzer hochladen. 
    
    - Wenn Sie die Anwendung zum Hochladen einer Grafik pro Benutzer konfiguriert haben, wird das Bild in die Bildbibliothek hochgeladen. 
    
    - Wenn Sie die Anwendung zum Hochladen von drei Bilder pro Benutzer konfiguriert haben, überprüft die Anwendung den Wert des **CreateSMLThumbs** in der Konfigurationsdatei, um festzustellen, ob die drei verschiedene Größe Bilder erforderlich sind. Drei verschiedene Größe Bilder erforderlich sind, verwendet die Anwendung **ResizeImageSmall** und **ResizeImageLarge** auf um drei verschiedene Größe Bilder aus diesem Quellabbild zu erstellen. Die Anwendung dann hochgeladen dessen Größe angepasst wurde Bilder in die Bildbibliothek. Wenn Sie drei verschiedene Größe Bilder nicht erforderlich sind, hochgeladen die Anwendung drei Bildern dieselbe Größe die Bildbibliothek.

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

**SetMultipleProfileProperties** festgelegt mehrere Benutzer Profileigenschaften in einem einzelnen Methodenaufruf. In diesem Codebeispiel legt **SetMultipleProfileProperties** die folgenden Benutzerprofileigenschaften für einen Benutzer fest:

-  **Bild-URL** - legen Sie auf die URL des Bilds hochgeladenen mittlerer Größe in die Bildbibliothek auf Mein Websitehost.
    
-  **SPS-PicturePlaceholderState** - auf NULL gesetzt, um anzugeben, dass SharePoint Online das hochgeladene Bild für den Benutzer angezeigt werden soll.

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

**SetAdditionalProfileProperties** wird zusätzliche Profileigenschaften, den, die Sie nach dem Hochladen der Bilddateien aktualisieren möchten. Sie können zusätzliche Eigenschaften so aktualisieren Sie in der Datei "Configuration.xml" angeben.

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

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [User Profile Lösungen für SharePoint 2013 und SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Core.ProfilePictureUploader-app](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
