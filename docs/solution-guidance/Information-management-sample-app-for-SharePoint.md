---
title: "Informationen Management Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c5e81e55cff89d6bf311c3fb6c7f40e0b0c87ee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="information-management-sample-add-in-for-sharepoint"></a><span data-ttu-id="dfdb6-102">Informationen Management Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="dfdb6-102">Information management sample add-in for SharePoint</span></span>
<span data-ttu-id="dfdb6-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie abrufen oder Festlegen von Richtlinien für Website zum Verwalten des Lebenszyklus der SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-103">As part of your Enterprise Content Management (ECM) strategy, you can get or set site policies to manage the lifecycle of your SharePoint site.</span></span>
    
<span data-ttu-id="dfdb6-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="dfdb6-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="dfdb6-105">Das [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) -Beispiel zeigt, wie Sie ein ASP.NET vom Anbieter gehosteten SharePoint-add-in zum Abrufen und Festlegen von Standortrichtlinien auf einer Website.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-105">The [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) sample shows you how to use an ASP.NET provider-hosted SharePoint add-in to get and set a site policy on a site.</span></span> <span data-ttu-id="dfdb6-106">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="dfdb6-106">Use this solution if you want to:</span></span>

- <span data-ttu-id="dfdb6-107">Anwenden von Richtlinieneinstellungen während Ihrer benutzerdefinierten Site Bereitstellungsprozesses.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-107">Apply policy settings during your custom site provisioning process.</span></span> 
    
- <span data-ttu-id="dfdb6-108">Erstellen Sie eines neuen oder ändern Sie einer vorhandenen Website.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-108">Create a new or modify an existing site policy.</span></span>
    
- <span data-ttu-id="dfdb6-109">Erstellen einer benutzerdefinierten ablaufformel.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-109">Create a custom expiration formula.</span></span> 
    
## <a name="before-you-begin"></a><span data-ttu-id="dfdb6-110">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="dfdb6-110">Before you begin</span></span>
<span data-ttu-id="dfdb6-111"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdb6-111"></span></span>

<span data-ttu-id="dfdb6-112">Laden Sie Sie zuerst [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-112">To get started, download the  [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="dfdb6-113">Es wird empfohlen, dass Sie mindestens eine Standortrichtlinie zu erstellen, und weisen Sie es zu Ihrer Website, bevor Sie dieses Add-in ausführen.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-113">We recommend that you create at least one site policy, and assign it to your site before you run this add-in.</span></span> <span data-ttu-id="dfdb6-114">Andernfalls wird das Add-In gestartet ohne Beispieldaten.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-114">Otherwise, the add-in will start without displaying sample data.</span></span> <span data-ttu-id="dfdb6-115">Weitere Informationen finden Sie unter [Übersicht über websiterichtlinien in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfdb6-115">For more information, see  [Overview of site policies in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span></span>

## <a name="using-the-coreinformationmanagement-sample-app"></a><span data-ttu-id="dfdb6-116">Verwenden die Core.InformationManagement Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="dfdb6-116">Using the Core.InformationManagement sample app</span></span>
<span data-ttu-id="dfdb6-117"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdb6-117"></span></span>

<span data-ttu-id="dfdb6-118">Wenn Sie die app starten, wird die Startseite die folgende Informationen angezeigt, wie in Abbildung 1 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="dfdb6-118">When you start the app, the start page displays the following information, as shown in Figure 1:</span></span>

- <span data-ttu-id="dfdb6-119">Die Website schließen und Ablauf Datumsangaben.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-119">The site's closure and expiration dates.</span></span> <span data-ttu-id="dfdb6-120">Diese Daten sind spezifisch für eine Website und basieren auf die Konfigurationseinstellungen der Website-Richtlinie, die angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-120">These dates are specific to a site and are based on the configuration settings of the site policy that is applied.</span></span>
    
- <span data-ttu-id="dfdb6-121">Alle websiterichtlinien, die auf der Website angewendet werden können.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-121">All site policies that can be applied to the site.</span></span>
    
- <span data-ttu-id="dfdb6-122">Die Website-Richtlinie, die momentan angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-122">The site policy that is currently applied.</span></span>
    
- <span data-ttu-id="dfdb6-123">Die Option Feld auswählen und Zuweisen einer neuen Standortrichtlinie für die Website.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-123">The option box to select and apply a new site policy to the site.</span></span>

<span data-ttu-id="dfdb6-124">**Abbildung 1. Informationen Management Add-in-Startseite**</span><span class="sxs-lookup"><span data-stu-id="dfdb6-124">**Figure 1. Information Management add-in start page**</span></span>

![Screenshot der Startseite-Add-in mit Website-Richtlinie zum Abschluss und Ablauf Werte, verfügbar und angewendeten Standortrichtlinien und andere Richtlinien hervorgehobenen anwenden.](media/8c5f39f7-700d-4300-bcc4-9ed9edf0e155.png)

<span data-ttu-id="dfdb6-126">Aus der SharePoint-Website können Sie Gehe zu der Anwendung, der auf dem Remotehost ausgeführt wird, indem Sie auf **zuletzt verwendet** > **Core.InformationManagement**.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-126">From your SharePoint site, you can go to the app, which runs on the remote host, by choosing  **Recent** > **Core.InformationManagement**.</span></span> <span data-ttu-id="dfdb6-127">Um zu Ihrer SharePoint-Website zurückzukehren, wählen Sie **zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-127">To return to your SharePoint site, choose  **Back to Site**.</span></span>

<span data-ttu-id="dfdb6-128">Die Datei Pages\Default.aspx.cs im Projekt Core.InformationManagementWeb enthält den Code für die Seite, die in Abbildung 1 angezeigt.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-128">The Pages\Default.aspx.cs file in the Core.InformationManagementWeb project contains the code for the page displayed in Figure 1.</span></span> 

<span data-ttu-id="dfdb6-129">Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" abruft und die Daten zum Abschluss und Ablauf der Website, basierend auf der Website angewendete Richtlinie angezeigt.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-129">The following code in the  **Page_Load** method of the Default.aspx.cs page fetches and displays the closure and expiration dates of the site, based on the applied site policy.</span></span> <span data-ttu-id="dfdb6-130">Dieser Code Ruft die Erweiterungsmethoden **GetSiteExpirationDate** und **GetSiteCloseDate** des Projekts OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-130">This code calls the **GetSiteExpirationDate** and **GetSiteCloseDate** extension methods of the OfficeDevPnP.Core project.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="dfdb6-131">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-131">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
// Get site expiration and closure dates.
if (cc.Web.HasSitePolicyApplied())
{
        lblSiteExpiration.Text = String.Format("The expiration date for the site is {0}", cc.Web.GetSiteExpirationDate());
        lblSiteClosure.Text = String.Format("The closure date for the site is {0}", cc.Web.GetSiteCloseDate());
}

```

<span data-ttu-id="dfdb6-132">Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" zeigt die Namen aller Website-Richtlinien, die auf der Website (einschließlich der derzeit angewendete Standortrichtlinie) angewendet werden können.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-132">The following code in the  **Page_Load** method of the Default.aspx.cs page displays the names of all site policies that can be applied to the site (including the currently applied site policy).</span></span> <span data-ttu-id="dfdb6-133">Dieser Code Ruft die Erweiterungsmethode **GetSitePolicies** des Projekts OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-133">This code calls the **GetSitePolicies** extension method of the OfficeDevPnP.Core project.</span></span>

```C#
// List the defined policies.
List<SitePolicyEntity> policies = cc.Web.GetSitePolicies();
string policiesString = "";
foreach (var policy in policies)
                    {
                        policiesString += String.Format("{0} ({1}) <BR />", policy.Name, policy.Description);
                    }
lblSitePolicies.Text = policiesString;
            };

```

<span data-ttu-id="dfdb6-134">Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" zeigt den Namen der Website-Richtlinie, die derzeit auf der Website angewendet.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-134">The following code in the  **Page_Load** method of the Default.aspx.cs page displays the name of the site policy currently applied to the site.</span></span> <span data-ttu-id="dfdb6-135">Dadurch wird die **GetAppliedSitePolicy** -Erweiterungsmethode des Projekts OfficeDevPnP.Core aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-135">This calls the **GetAppliedSitePolicy** extension method of the OfficeDevPnP.Core project.</span></span>

```C#
// Show the assigned policy.
SitePolicyEntity appliedPolicy = cc.Web.GetAppliedSitePolicy();
if (appliedPolicy != null)
            {
            lblAppliedPolicy.Text = String.Format("{0} ({1})", appliedPolicy.Name, appliedPolicy.Description);
            }
else
            {
            lblAppliedPolicy.Text = "No policy has been applied";
            }

```

<span data-ttu-id="dfdb6-136">Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" füllt die Dropdown-Liste mit den websiterichtlinien, die mit Ausnahme der Standortrichtlinie verfügbar sind, die der Website zugewiesen ist.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-136">The following code in the  **Page_Load** method of the Default.aspx.cs page populates the drop-down list with the site policies that are available, except for the site policy that is currently assigned to the site.</span></span>

```C#
// Fill the policies combo.
foreach (var policy in policies)
{
if (appliedPolicy == null || !policy.Name.Equals(appliedPolicy.Name, StringComparison.InvariantCultureIgnoreCase))
{
                            drlPolicies.Items.Add(policy.Name);
           }
}
btnApplyPolicy.Enabled = drlPolicies.Items.Count > 0;

```

<span data-ttu-id="dfdb6-137">Der folgende Code in der Seite "default.aspx.cs" gilt die ausgewählte Standortrichtlinie für die Website.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-137">The following code in the Default.aspx.cs page applies the selected site policy to the site.</span></span> <span data-ttu-id="dfdb6-138">Die ursprüngliche Website Richtlinie wird durch die neue Standortrichtlinie ersetzt.</span><span class="sxs-lookup"><span data-stu-id="dfdb6-138">The original site policy is replaced by the new site policy.</span></span> 

```C#
protected void btnApplyPolicy_Click(object sender, EventArgs e)
{
if (drlPolicies.SelectedItem != null)
            {
                cc.Web.ApplySitePolicy(drlPolicies.SelectedItem.Text);
                Page.Response.Redirect(Page.Request.Url.ToString(), true);
            }
}

```

## <a name="see-also"></a><span data-ttu-id="dfdb6-139">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="dfdb6-139">See also</span></span>
<span data-ttu-id="dfdb6-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdb6-140"></span></span>

-  [<span data-ttu-id="dfdb6-141">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="dfdb6-141">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="dfdb6-142">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="dfdb6-142">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
-  [<span data-ttu-id="dfdb6-143">Core.SiteClassification-Beispiel</span><span class="sxs-lookup"><span data-stu-id="dfdb6-143">Core.SiteClassification sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SiteClassification)
    
-  [<span data-ttu-id="dfdb6-144">ECM. AutoTagging Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="dfdb6-144">ECM.AutoTagging sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
    
-  [<span data-ttu-id="dfdb6-145">ECM. DocumentLibraries Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="dfdb6-145">ECM.DocumentLibraries sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
    
-  [<span data-ttu-id="dfdb6-146">ECM. RecordsManagement Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="dfdb6-146">ECM.RecordsManagement sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement)
