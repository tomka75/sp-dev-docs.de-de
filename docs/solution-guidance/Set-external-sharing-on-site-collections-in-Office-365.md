---
title: "Legen Sie externe Freigabe für Websitesammlungen in Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: 77dcda34649a2d4d3a19e07b161c623d8db26de3
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="set-external-sharing-on-site-collections-in-office-365"></a>Legen Sie externe Freigabe für Websitesammlungen in Office 365

Sie können steuern, externe Freigabe Einstellungen auf einer SharePoint-Websitesammlung in Office 365, externe Benutzer (Benutzer, die nicht über ein Konto Organisation in Office 365-Abonnement verfügen) ermöglicht den Zugriff auf Ihrer Websitesammlung.

_**Gilt für:** -add-ins für SharePoint | SharePoint Online | Office 365_

Das [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) Code-Beispiel zeigt, wie Ihre Einstellungen für externen Freigabe für eine SharePoint-Websitesammlung gesteuert. Mit dieser Lösung können:

- Externe Freigabe Einstellungen während Ihrer Website Bereitstellungsprozesses-Steuerelement.
    
- Bereiten Sie Ihrer Websitesammlung für die Freigabe mit externen Benutzern vor.

> [!NOTE] 
> Einstellungen für externe Freigabe sind nur verfügbar in Office 365.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="using-the-coreexternalsharing-app"></a>Verwenden der app Core.ExternalSharing
<a name="sectionSection1"> </a>

Stellen Sie sicher, dass externe Freigabe Ihres Office 365-Abonnements zulässt. Dazu:

1. Öffnen Sie Ihre **Office 365 Administrationscenter**.
    
2. Wählen Sie im linken Navigationsbereich auf **SharePoint**aus.
    
3. Wählen Sie im linken Navigationsbereich auf **Freigabe**.
    
4. **Freigabe außerhalb Ihrer Organisation**sicher, dass **auf** **einladen und mit externen Benutzern authentifizierten Freigaben durch Benutzer zulassen** befindet.
    
Prüfen Sie Ihre externe websiteeinstellungen auf Ihrer SharePoint-Websitesammlung. Dazu:

1. Öffnen Sie Ihre **Office 365 Administrationscenter**.
    
2. Wählen Sie im linken Navigationsbereich auf **SharePoint** , um Ihre **SharePoint-Verwaltungskonsole**zu öffnen.
    
3. Wählen Sie in der Liste Website-Auflistung das Kontrollkästchen neben der URL der Websitesammlung, die Sie Ihre Einstellungen für externen Freigabe auf überprüfen möchten.
    
4. Wählen Sie die **Freigabe**, klicken Sie im Menüband.
    
5. Überprüfen Sie die externen Freigabe Einstellungen im Dialogfeld **Freigabe** . Geben Sie nach dem Ausführen des Beispiels Code an im Dialogfeld **Freigabe** , um sicherzustellen, dass Ihre externen Freigabe Einstellungen geändert.
    
Wenn Sie dieses Codebeispiel ausführen, werden **Main** in Program.cs die folgenden Aufgaben ausgeführt:

- Ruft die URL der SharePoint Admin Center an.
    
- Ruft die URL der Websitesammlung so konfigurieren Sie Einstellungen für externe Freigabe auf.
    
- Dient zum Abrufen Ihrer Office 365-Administrator-Anmeldeinformationen.
    
- Ruft die **GetInputSharing**, die den Benutzer auffordert, wählen Sie eine externe Freigabe Einstellung ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) für die Websitesammlung angewendet. Externe Freigabe Einstellungen zur Auswahl stehen:
    
    -  **Deaktivierte**externe Freigabe auf der Website deaktiviert.
    
    -  **ExternalUserAndGuestSharing**, wodurch externer Benutzer und Gast Freigabe auf der Website.
    
    -  **ExternalUserSharingOnly**, wodurch externer Benutzer nur Freigabe.
    
- Ruft die **SetSiteSharing**.

> [!NOTE] 
> Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

```C#
 static void Main(string[] args)
        {
           
            /* Prompt for your Office 365 admin center URL*/
            Console.WriteLine("Enter your Tenant Admin URL for your Office 365 subscription:");
            string tenantAdminURL = GetSite();

            /* End Program if no Office 365 admin center URL is supplied*/
            if (string.IsNullOrEmpty(tenantAdminURL))
            {
                Console.WriteLine("Hmm, i tried to work on it but you didn't supply your admin tenant url:");
                return;
            }
               
            // Prompt the user for an Office365 site collection 
            Console.WriteLine("Enter your Office 365 Site Collection URL:");
            string siteUrl = GetSite();

            /* Prompt for Credentials */
            Console.WriteLine("Enter Credentials for your Office 365 Site Collection {0}:", siteUrl);

            string userName = GetUserName();
            SecureString pwd = GetPassword();

            /* End program if no credentials are entered */
            if (string.IsNullOrEmpty(userName) || (pwd == null))
            {
                Console.WriteLine("Hmm, i tried to work on it but you didn't supply your credentials:");
                return;
            }

            try 
            {
                SharingCapabilities _sharingSettingToApply = GetInputSharing(siteUrl);
                using (ClientContext cc = new ClientContext(tenantAdminURL))
                { 
                    cc.AuthenticationMode = ClientAuthenticationMode.Default;
                    cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    SetSiteSharing(cc, siteUrl, _sharingSettingToApply);
                }
            }
            catch(Exception ex)
            {
                Console.WriteLine("Oops, Mistakes can happen to anyone. An Error occured : {0}", ex.Message);
               
            }

            Console.WriteLine("Hit Enter to exit.");
            Console.Read();

        
        }
```

**SetSiteSharing** bewirkt Folgendes:

-  Mithilfe der **Tenant.GetSitePropertiesByUrl** **SiteProperties** in Ihrer Websitesammlung abgerufen.
    
- Wird **Tenant.SharingCapability** ermittelt, ob externe Freigabe für Ihre Office 365-Abonnements aktiviert ist.
    
-  Freigabe in Ihrem Office 365-Abonnement aktiviert ist, können Sie die **SiteProperties.SharingCapability** auf die Einstellungen für externen Freigabe vom Benutzer eingegebenen festgelegt.

```C#
public static void SetSiteSharing(ClientContext adminCC, string siteCollectionURl, SharingCapabilities shareSettings)
        {
            var _tenantAdmin = new Tenant(adminCC);
            SiteProperties _siteprops = _tenantAdmin.GetSitePropertiesByUrl(siteCollectionURl, true);
            adminCC.Load(_tenantAdmin);
            adminCC.Load(_siteprops);
            adminCC.ExecuteQuery();

            SharingCapabilities _tenantSharing = _tenantAdmin.SharingCapability;
            var _currentShareSettings = _siteprops.SharingCapability;
            bool _isUpdatable = false;

            if(_tenantSharing == SharingCapabilities.Disabled)
            {
                Console.WriteLine("Sharing is currently disabled in your tenant! I am unable to work on it.");
            }
            else
            {  
                if(shareSettings == SharingCapabilities.Disabled)
                { _isUpdatable = true; }
                else if(shareSettings == SharingCapabilities.ExternalUserSharingOnly)
                {
                    _isUpdatable = true;   
                }
                else if (shareSettings == SharingCapabilities.ExternalUserAndGuestSharing)
                {
                    if (_tenantSharing == SharingCapabilities.ExternalUserAndGuestSharing)
                    {
                        _isUpdatable = true;
                    }
                    else
                    {
                        Console.WriteLine("ExternalUserAndGuestSharing is currently disabled in your tenant! I am unable to work on it.");
                    }
                }
            }
            if (_currentShareSettings != shareSettings &amp;&amp; _isUpdatable)
            {
                _siteprops.SharingCapability = shareSettings;
                _siteprops.Update();
                adminCC.ExecuteQuery();
                Console.WriteLine("Set Sharing on site {0} to {1}.", siteCollectionURl, shareSettings);
            }
        }
```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Verwalten Sie externe Freigabe für Ihre SharePoint Online-Umgebung](https://support.office.com/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85)
