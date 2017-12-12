---
title: "Migrieren Sie Benutzerprofil Eigenschaften Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 03a7591b21531387e1cd1312be76f1f6e916c41e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="migrate-user-profile-properties-sample-add-in-for-sharepoint"></a>Migrieren Sie Benutzerprofil Eigenschaften Beispiel-add-in für SharePoint

Verwenden einer vom Anbieter gehosteten-add-in zu migrieren und Importieren von Profildaten für SharePoint-Benutzer.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
[Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) -Beispiel-add-in zeigt, wie von Benutzerprofildaten von SharePoint Server 2010 oder SharePoint Server 2013 in SharePoint Online zu migrieren.
    
Dieses Beispiel enthält zwei konsolenanwendungen. Beide verwenden den userprofileservice.asmx-Webdienst, um ein- und mehrwertige Benutzerprofildaten in eine XML-Datei extrahieren, und importieren die extrahierten Daten in den Benutzerprofildienst in SharePoint Online.
Wenn Sie möchten, verwenden Sie dieses Codebeispiel:

- Extrahieren von Benutzerprofildaten in SharePoint Server 2010 oder SharePoint Server 2013.
    
- Importieren von Benutzerprofildaten in SharePoint Online.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub. Das Codebeispiel enthält zwei Projekte.

Für das Projekt **Contoso.ProfileProperty.Migration.Extract** :

- Da in diesem Codebeispiel wird das serverseitige Objektmodell verwendet, müssen Sie unbedingt, dass Sie das Projekt auf einem Server mit SharePoint Server 2010 oder SharePoint Server 2013 installiert ausgeführt werden.
    
- Verwenden Sie ein Konto mit Administratorberechtigungen für SharePoint-Farm.
    
- Bearbeiten Sie die Konfigurationsinformationen, die in Tabelle 1 aufgeführten mithilfe die Datei App.config.
    
- Für alle Benutzer stellen Sie sicher, dass die Benutzerprofileigenschaft **E-Mail** nicht leer ist. Wenn der Wert der Benutzerprofileigenschaft **Arbeit e-Mail** leer ist, werden die Extraktion vorzeitig beendet.
    
- In diesem Codebeispiel extrahiert Benutzerprofile von SharePoint Server 2010. Wenn Sie Benutzerprofile aus SharePoint Server 2013 extrahieren, führen Sie folgende Schritte aus:
    
  ein. Öffnen Sie das Kontextmenü (Rechtsklick) für **Contoso.ProfileProperty.Migration.Extract** > **Eigenschaften**.
    
  b. Wählen Sie unter **Anwendung** **Zielframework** **.NET Framework 4**.
    
  c. Wählen Sie **Ja**, klicken Sie dann auf **Speichern**.
    
**In Tabelle 1. Konfigurationen für die App**

|**Name der Einstellung Konfiguration**|**Beschreibung**|Beispiel|
|:-----|:-----|:-----|
|**MYSITEHOSTURL** |Meine Website-URL in der quellfarm für SharePoint Server 2010 oder SharePoint Server 2013.|http://My.contoso.com |
|**PROPERTYSEPERATOR** |Das Zeichen verwendet, um mehrere Werte einer mehrwertigen Benutzerprofileigenschaft zu trennen.| |
|**USERPROFILESSTORE** |Der XML-Dateipfad zum Schreiben der extrahierten Benutzerprofildaten.|C:\temp\ProfileData.Xml|
|**LOGFILE** |Der XML-Dateipfad zum Schreiben der extrahierten Benutzerprofildaten.|C:\temp\Extract.log|
|**ENABLELOGGING** |Aktivieren Sie Datenträger-Protokollierung.|"True"|
|**TESTRUN** |Führt eine Extraktion Test, um zu bestätigen, dass Ihre Konfigurationseinstellungen in App.Config richtig sind.|Legen Sie `TESTRUN=true` Wenn Sie eine Extraktion Test durchführen. Der Testlauf extrahiert nur für einen Benutzer aus der Benutzerprofildienst.<br /> Legen Sie `TESTRUN=false` Wenn Sie alle Benutzer aus der Benutzerprofildienst extrahieren. |

Für das Projekt **Contoso.ProfileProperty.Migration.Import**

- Stellen Sie sicher, dass die Benutzerprofile in Office 365 vorhanden sein. 
    
- Stellen Sie sicher, dass **E-Mail** -Adresse des Benutzers in der lokalen SharePoint Server 2013 und Office 365 Benutzerprofildienst identisch ist.
    
- Ändern Sie in der Datei App.config das **Value** -Element der **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** Einstellung, die einen Verweis auf den Benutzerprofildienst in Ihrer SharePoint Online-Verwaltungskonsole zählen Siehe die in der folgenden Beispiel.

    ```XML
    <applicationSettings>
    <Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    <setting name="Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService" serializeAs="String">
    <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
    </setting>
    </Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    </applicationSettings>
    ```

- Bearbeiten Sie die in Tabelle 2 aufgelisteten Konfigurationseinstellungen mithilfe die Datei App.config.
    
**In Tabelle 2. Konfigurationseinstellungen für die Datei ' App.config '**

|**Name der Einstellung Konfiguration**|**Beschreibung**|Beispiel|
|:-----|:-----|:-----|
|**tenantName** |Dies ist der Name des Mandanten.|Wenn Ihre Mandanten URL http://contoso.onmicrosoft.com ist, geben Sie Contoso als Ihrem Mandantennamen.|
|**PROPERTYSEPERATOR** |Das Zeichen verwendet, um die Werte einer mehrwertigen Benutzerprofileigenschaft zu trennen.| |
|**USERPROFILESSTORE** |Die XML-Datei zum Lesen der extrahierten Benutzerprofildaten.|C:\temp\ProfileData.Xml|
|**LOGFILE** |Die Protokolldatei für die ereignisprotokollierung verwendet.|C:\temp\Extract.log|
|**ENABLELOGGING** |Aktivieren Sie Datenträger-Protokollierung.|"True"|
|**SPOAdminUserName** |Ein Office 365-Administrator Benutzername.|Nicht zutreffend|
|**SPOAdminPassword** |Kennwort für ein Office 365-Administrator.|Nicht zutreffend|

## <a name="using-the-coreprofilepropertymigration-app"></a>Verwenden der app Core.ProfileProperty.Migration
<a name="sectionSection1"> </a>

In diesem Codebeispiel wird als Konsolenanwendung ausgeführt. Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Funktion in Program.cs die folgenden Aufgaben aus:

- Stellt eine Verbindung zur Mein Websitehost und Verbindung mit der Benutzerprofildienst **UserProfileManager** verwendet. **UserProfileManager** gehört die **Microsoft.Office.Server.UserProfiles.dll** -Assembly.
    
- Erstellt eine Liste namens **pData** zum Speichern der extrahierten Benutzerprofildaten.
    
- Für alle Benutzer in der Benutzerprofildienst passiert Folgendes:
    
    - Wird mit **GetSingleValuedProperty** die **WorkEmail** und Benutzerprofileigenschaften **Mich-Seite** auf ein **UserProfileData** -Objekt namens **"UserData"**kopiert.
    
    - Wird mit **GetMultiValuedProperty** **SPS-Verantwortung** Benutzerprofileigenschaft zu **"UserData"**kopiert.
    
- **UserProfileCollection.Save** verwendet zum Serialisieren von **UserData** in eine XML-Datei. Die XML-Datei wird unter dem Dateipfad gespeichert, der in ' App.config ' angegeben.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

Beachten Sie, dass die **GetSingleValuedProperty** -Methode userprofileservice.asmx verwendet, um ein einwertiges Benutzerprofileigenschaft abzurufen. **GetSingleValuedProperty** wird Folgendes, wie im nächsten Beispiel dargestellt:

- Ruft das Property-Objekt zum Extrahieren von Daten aus mithilfe von **Spuser [UserProperty]**ab.
    
- Gibt den ersten Wert in der **UserProfileValueCollection** zurück, wenn der Wert nicht **null**ist. 

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

Beachten Sie, dass die **GetMultiValuedProperty** -Methode userprofileservice.asmx verwendet, um eine mehrwertige Benutzerprofileigenschaft abzurufen. **GetMultiValuedProperty** wird Folgendes, wie im nächsten Beispiel dargestellt:

- Ruft die Benutzerprofileigenschaft-Objekts das update **Spuser [UserProperty]**.
    
- Erstellt eine Zeichenfolge der Benutzer Profile-Eigenschaftswerte durch die in der Datei ' App.config ' angegebenen **PROPERTYSEPARATOR** getrennt.

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

## <a name="using-contosoprofilepropertymigrationimport"></a>Verwenden von Contoso.ProfileProperty.Migration.Import
<a name="sectionSection2"> </a>

In diesem Codebeispiel wird als Konsolenanwendung ausgeführt. Wenn das Codebeispiel ausgeführt wird, führt die **Main** -Methode in Program.cs Folgendes aus:

- Initialisiert die Konsolenanwendung **InitializeConfiguration** und **InitializeWebService**verwenden. 
    
- Deserialisiert die XML-Datei, die die extrahierten Benutzerprofildaten enthält.
    
- Für alle Benutzer in der XML-Datei geschieht Folgendes:
    
    - Extrahiert die **UserName** -Eigenschaft aus der XML-Datei.
    
    - Mithilfe von **SetSingleMVProfileProperty** **SPS-Verantwortung** auf das Profil des Benutzers festgelegt.
    
    - Mithilfe von **SetSingleMVProfileProperty** **Mich-Seite** auf das Profil des Benutzers festgelegt.
    
**InitializeWebService** stellt eine Verbindung mit SharePoint Online, und einen Verweis auf den Benutzerprofildienst auf eine Instanzvariable festgelegt. Andere Methoden in diesem Codebeispiel verwenden Sie diese Instanzvariable zum Schreiben von Werten in Benutzerprofileigenschaften. Zum Verwalten von Benutzerprofil verwendet dieses Codebeispiel den userprofileservice.asmx-Webdienst in der SharePoint Online-Verwaltungskonsole.

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

Die **SetSingleMVProfileProperty** -Methode wird eine mehrwertige Benutzerprofileigenschaft wie **SPS-Verantwortung**, die folgenden Schritte durch:

- Aufteilen von **PropertyValue** in ein Zeichenfolgenarray aufgerufen **Arrs** um User Profile-Eigenschaftswerte zu speichern. Die Zeichenfolge wird bei Verwendung in ' App.config ' angegebenen Einstellung für die **PROPERTYSEPERATOR** geteilt.
    
- Zuweisen der Werte von **Arrs** in ein Array **ValueData** auf den Benutzerprofildienst.
    
- Erstellen ein Array **PropertyData** auf den Benutzerprofildienst. Der Name der Benutzerprofileigenschaft und das Array **ValueData** werden Eigenschaften für das Objekt **PropertyData** übergeben. Dieses Array hat ein Element, da nur eine mehrwertige Benutzerprofileigenschaft importiert werden sollen.
    
Die Daten werden in der Verwendung von **ModifyUserPropertyByAccountName** auf dem **userprofileservice.asmx** -Webdienst in der SharePoint Online-Verwaltungskonsole Benutzerprofildienst geschrieben. Der Benutzer ein, der in diesem Codebeispiel muss ein Office 365-Administrator sein.

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

Die **SetSingleValuedProperty** -Methode wird ein einwertiges Benutzerprofileigenschaften, wie **Mich-Seite**.  **SetSingleValuedProperty** das gleiche Verfahren als **SetSingleMVProfileProperty**implementiert, verwendet jedoch ein Array **ValueData** mit nur einem Element.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [User Profile Lösungen für SharePoint 2013 und SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
