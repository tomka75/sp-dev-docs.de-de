---
title: "Legen Sie externe Freigabe für Websitesammlungen in Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: 77dcda34649a2d4d3a19e07b161c623d8db26de3
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="set-external-sharing-on-site-collections-in-office-365"></a><span data-ttu-id="5ceb4-102">Legen Sie externe Freigabe für Websitesammlungen in Office 365</span><span class="sxs-lookup"><span data-stu-id="5ceb4-102">Set external sharing on site collections in Office 365</span></span>

<span data-ttu-id="5ceb4-103">Sie können steuern, externe Freigabe Einstellungen auf einer SharePoint-Websitesammlung in Office 365, externe Benutzer (Benutzer, die nicht über ein Konto Organisation in Office 365-Abonnement verfügen) ermöglicht den Zugriff auf Ihrer Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-103">You can control external sharing settings on a SharePoint site collection in Office 365, allowing external users (users who don't have an organization account in your Office 365 subscription) access to your site collection.</span></span>

<span data-ttu-id="5ceb4-104">_**Gilt für:** -add-ins für SharePoint | SharePoint Online | Office 365_</span><span class="sxs-lookup"><span data-stu-id="5ceb4-104">_**Applies to:** add-ins for SharePoint | SharePoint Online | Office 365_</span></span>

<span data-ttu-id="5ceb4-105">Das [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) Code-Beispiel zeigt, wie Ihre Einstellungen für externen Freigabe für eine SharePoint-Websitesammlung gesteuert.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-105">The  [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) code sample shows you how to control your external sharing settings on a SharePoint site collection.</span></span> <span data-ttu-id="5ceb4-106">Mit dieser Lösung können:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-106">Use this solution to:</span></span>

- <span data-ttu-id="5ceb4-107">Externe Freigabe Einstellungen während Ihrer Website Bereitstellungsprozesses-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-107">Control external sharing settings during your site provisioning process.</span></span>
    
- <span data-ttu-id="5ceb4-108">Bereiten Sie Ihrer Websitesammlung für die Freigabe mit externen Benutzern vor.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-108">Prepare your site collection for sharing with external users.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ceb4-109">Einstellungen für externe Freigabe sind nur verfügbar in Office 365.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-109">External sharing settings are only available in Office 365.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ceb4-110">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-110">Before you begin</span></span>
<span data-ttu-id="5ceb4-111"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="5ceb4-111"></span></span>

<span data-ttu-id="5ceb4-112">Laden Sie Sie zuerst [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-112">To get started, download the  [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreexternalsharing-app"></a><span data-ttu-id="5ceb4-113">Verwenden der app Core.ExternalSharing</span><span class="sxs-lookup"><span data-stu-id="5ceb4-113">Using the Core.ExternalSharing app</span></span>
<span data-ttu-id="5ceb4-114"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="5ceb4-114"></span></span>

<span data-ttu-id="5ceb4-115">Stellen Sie sicher, dass externe Freigabe Ihres Office 365-Abonnements zulässt.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-115">Verify that your Office 365 subscription allows external sharing.</span></span> <span data-ttu-id="5ceb4-116">Dazu:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-116">To do this:</span></span>

1. <span data-ttu-id="5ceb4-117">Öffnen Sie Ihre **Office 365 Administrationscenter**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-117">Open your  **Office 365 admin center**.</span></span>
    
2. <span data-ttu-id="5ceb4-118">Wählen Sie im linken Navigationsbereich auf **SharePoint**aus.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-118">On the left navigation menu, choose **SharePoint**.</span></span>
    
3. <span data-ttu-id="5ceb4-119">Wählen Sie im linken Navigationsbereich auf **Freigabe**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-119">On the left navigation menu, choose  **Sharing**.</span></span>
    
4. <span data-ttu-id="5ceb4-120">**Freigabe außerhalb Ihrer Organisation**sicher, dass **auf** **einladen und mit externen Benutzern authentifizierten Freigaben durch Benutzer zulassen** befindet.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-120">In  **Sharing outside your organization**, ensure that  **Allow users to invite and share with authenticated external users** is **On**.</span></span>
    
<span data-ttu-id="5ceb4-121">Prüfen Sie Ihre externe websiteeinstellungen auf Ihrer SharePoint-Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-121">Verify your external site settings on your SharePoint site collection.</span></span> <span data-ttu-id="5ceb4-122">Dazu:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-122">To do this:</span></span>

1. <span data-ttu-id="5ceb4-123">Öffnen Sie Ihre **Office 365 Administrationscenter**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-123">Open your  **Office 365 admin center**.</span></span>
    
2. <span data-ttu-id="5ceb4-124">Wählen Sie im linken Navigationsbereich auf **SharePoint** , um Ihre **SharePoint-Verwaltungskonsole**zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-124">On the left navigation menu, choose  **SharePoint** to open your **SharePoint admin center**.</span></span>
    
3. <span data-ttu-id="5ceb4-125">Wählen Sie in der Liste Website-Auflistung das Kontrollkästchen neben der URL der Websitesammlung, die Sie Ihre Einstellungen für externen Freigabe auf überprüfen möchten.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-125">In the Site Collection List, select the check box next to the site collection URL that you want to verify your external sharing settings on.</span></span>
    
4. <span data-ttu-id="5ceb4-126">Wählen Sie die **Freigabe**, klicken Sie im Menüband.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-126">On the ribbon, choose  **Sharing**.</span></span>
    
5. <span data-ttu-id="5ceb4-127">Überprüfen Sie die externen Freigabe Einstellungen im Dialogfeld **Freigabe** .</span><span class="sxs-lookup"><span data-stu-id="5ceb4-127">Review your external sharing settings in the  **sharing** dialog.</span></span> <span data-ttu-id="5ceb4-128">Geben Sie nach dem Ausführen des Beispiels Code an im Dialogfeld **Freigabe** , um sicherzustellen, dass Ihre externen Freigabe Einstellungen geändert.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-128">After running the code sample, return to the **sharing** dialog to verify that your external sharing settings changed.</span></span>
    
<span data-ttu-id="5ceb4-129">Wenn Sie dieses Codebeispiel ausführen, werden **Main** in Program.cs die folgenden Aufgaben ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-129">When you run this code sample,  **Main** in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="5ceb4-130">Ruft die URL der SharePoint Admin Center an.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-130">Gets the SharePoint admin center URL.</span></span>
    
- <span data-ttu-id="5ceb4-131">Ruft die URL der Websitesammlung so konfigurieren Sie Einstellungen für externe Freigabe auf.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-131">Gets the site collection URL to configure external sharing settings on.</span></span>
    
- <span data-ttu-id="5ceb4-132">Dient zum Abrufen Ihrer Office 365-Administrator-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-132">Gets your Office 365 administrator credentials.</span></span>
    
- <span data-ttu-id="5ceb4-133">Ruft die **GetInputSharing**, die den Benutzer auffordert, wählen Sie eine externe Freigabe Einstellung ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) für die Websitesammlung angewendet.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-133">Calls  **GetInputSharing**, which prompts the user to choose an external sharing setting ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) to apply to the site collection.</span></span> <span data-ttu-id="5ceb4-134">Externe Freigabe Einstellungen zur Auswahl stehen:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-134">The external sharing settings choices include:</span></span>
    
    -  <span data-ttu-id="5ceb4-135">**Deaktivierte**externe Freigabe auf der Website deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-135">**Disabled**, which turns off external sharing on the site.</span></span>
    
    -  <span data-ttu-id="5ceb4-136">**ExternalUserAndGuestSharing**, wodurch externer Benutzer und Gast Freigabe auf der Website.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-136">**ExternalUserAndGuestSharing**, which enables external user and guest sharing on the site.</span></span>
    
    -  <span data-ttu-id="5ceb4-137">**ExternalUserSharingOnly**, wodurch externer Benutzer nur Freigabe.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-137">**ExternalUserSharingOnly**, which enables external user sharing only.</span></span>
    
- <span data-ttu-id="5ceb4-138">Ruft die **SetSiteSharing**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-138">Calls  **SetSiteSharing**.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ceb4-139">Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-139">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="5ceb4-140">**SetSiteSharing** bewirkt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-140">**SetSiteSharing** does the following:</span></span>

-  <span data-ttu-id="5ceb4-141">Mithilfe der **Tenant.GetSitePropertiesByUrl** **SiteProperties** in Ihrer Websitesammlung abgerufen.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-141">Uses the **Tenant.GetSitePropertiesByUrl** to retrieve **SiteProperties** on your site collection.</span></span>
    
- <span data-ttu-id="5ceb4-142">Wird **Tenant.SharingCapability** ermittelt, ob externe Freigabe für Ihre Office 365-Abonnements aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-142">Uses  **Tenant.SharingCapability** to determine whether external sharing is enabled on your Office 365 subscription.</span></span>
    
-  <span data-ttu-id="5ceb4-143">Freigabe in Ihrem Office 365-Abonnement aktiviert ist, können Sie die **SiteProperties.SharingCapability** auf die Einstellungen für externen Freigabe vom Benutzer eingegebenen festgelegt.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-143">If sharing is enabled in your Office 365 subscription, sets the **SiteProperties.SharingCapability** to the external sharing settings the user entered.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5ceb4-144">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="5ceb4-144">See also</span></span>
<span data-ttu-id="5ceb4-145"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5ceb4-145"></span></span>

-  [<span data-ttu-id="5ceb4-146">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="5ceb4-146">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="5ceb4-147">Verwalten Sie externe Freigabe für Ihre SharePoint Online-Umgebung</span><span class="sxs-lookup"><span data-stu-id="5ceb4-147">Manage external sharing for your SharePoint Online environment</span></span>](https://support.office.com/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85)
