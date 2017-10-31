---
title: Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 78b8b7813b7d21a2a197c5975472e07f5efc7613
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-developer-site-on-an-existing-office-365-subscription"></a><span data-ttu-id="f006e-102">Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement</span><span class="sxs-lookup"><span data-stu-id="f006e-102">Create a developer site on an existing Office 365 subscription</span></span>
<span data-ttu-id="f006e-p101">Eine Office 365-Entwicklerwebsite erleichtert Ihnen die Einrichtung und den Einstieg in das Erstellen, Testen und Bereitstellen Ihrer Office- und SharePoint-Add-Ins. Viele Office 365 Business-, Enterprise-, Education- und Government-Abonnements enthalten eine Websitevorlage, die Sie zum Erstellen einer Entwicklerwebsite verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f006e-p101">An Office 365 Developer Site makes it easier to get set up and start creating, testing, and deploying your Office and SharePoint Add-ins more quickly. Many Office 365 Business, Enterprise, Education, and Government subscriptions include a site template you can use to create a Developer Site.</span></span>
 

 <span data-ttu-id="f006e-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f006e-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

 <span data-ttu-id="f006e-108">**Bevor Sie beginnen**</span><span class="sxs-lookup"><span data-stu-id="f006e-108">**Before you start**</span></span>
 

-  <span data-ttu-id="f006e-p103">**Stellen Sie sicher, dass Sie ein Office 365-Abonnement besitzen, das eine Entwicklerwebsite unterstützt.** Wenn Sie eins der folgenden Office 365 Abonnementpläne besitzen, können Sie in Ihrem vorhandenen Abonnement eine Website für Entwickler erstellen:</span><span class="sxs-lookup"><span data-stu-id="f006e-p103">**Be sure you have an Office 365 subscription that supports a Developer Site.** If you have one of the following Office 365 subscription plans, you can create a Developer Site within your existing subscription:</span></span>
    
    - <span data-ttu-id="f006e-111">Office 365 Midsize Business</span><span class="sxs-lookup"><span data-stu-id="f006e-111">Office 365 Midsize Business</span></span>
    
 
- <span data-ttu-id="f006e-112">Office 365 Enterprise E1, E3, E4, E5 oder K1</span><span class="sxs-lookup"><span data-stu-id="f006e-112">Office 365 Enterprise E1, E3, E4, E5, or K1</span></span>
    
 
- <span data-ttu-id="f006e-113">Office 365 Education A2, A3 oder A4</span><span class="sxs-lookup"><span data-stu-id="f006e-113">Office 365 Education A2, A3, or A4</span></span>
    
 
- <span data-ttu-id="f006e-114">Office 365 Government G1, G3, G4 oder K1</span><span class="sxs-lookup"><span data-stu-id="f006e-114">Office 365 Government G1, G3, G4, or K1</span></span>
    
 
-  <span data-ttu-id="f006e-p104">**Wenn Sie ein Office 365 Small Business-Abonnement besitzen,** unterstützt es nur eine einzelne Websitesammlung, sie können damit also keine Entwickler-Websitesammlung erstellen. Weitere Informationen über Office 365-Pläne für Ihr Unternehmen finden Sie unter [SharePoint Online: Softwarelimits und -beschränkungen](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/sharepoint-online-software-boundaries-and-limits-HA102694293.aspx).</span><span class="sxs-lookup"><span data-stu-id="f006e-p104">**If you have an Office 365 Small Business subscription,** it supports only a single site collection, and so you can't create a Developer Site collection. If you would like to learn more about Office 365 plans for your business, see [SharePoint Online: software boundaries and limits](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/sharepoint-online-software-boundaries-and-limits-HA102694293.aspx).</span></span>
    
 
- <span data-ttu-id="f006e-117">Weitere Informationen zu den Office 365 Enterprise-Angeboten finden Sie unter [Pläne &amp; Preise](http://products.office.com/en-us/business/office-365-enterprise-e1-business-software ).</span><span class="sxs-lookup"><span data-stu-id="f006e-117">For more information about the Office 365 Enterprise offerings, see  [Plans &amp; Pricing](http://products.office.com/en-us/business/office-365-enterprise-e1-business-software ).</span></span>
    
 

## <a name="create-a-developer-site"></a><span data-ttu-id="f006e-118">Erstellen einer Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="f006e-118">Create a Developer Site</span></span>
<span data-ttu-id="f006e-119"><a name="bk_createdevsite"> </a></span><span class="sxs-lookup"><span data-stu-id="f006e-119"><a name="bk_createdevsite"> </a></span></span>


1. <span data-ttu-id="f006e-120">Melden Sie sich bei Office 365 als globaler oder SharePoint Online-Administrator an.</span><span class="sxs-lookup"><span data-stu-id="f006e-120">Sign in to Office 365 as a Global or SharePoint Online admin.</span></span>
    
     <span data-ttu-id="f006e-p105">**Sie müssen als globaler oder SharePoint Online-Administrator angemeldet sein, um neue Websitesammlungen** wie z. B. eine Website für Entwickler zu erstellen. Nur Administratoren werden nach dem Anmelden an Office 365 Administratoroptionen angezeigt. Wenn Sie kein Administrator sind, müssen Sie einen Administrator in Ihrem Unternehmen kontaktieren, der für Sie eine der folgenden Aufgaben ausführen muss:</span><span class="sxs-lookup"><span data-stu-id="f006e-p105">**You must sign in as a Global or SharePoint Online admin to create new site collections,** such as a Developer Site. Only admins can see Admin options when signing into Office 365. If you're not an admin, contact an admin in your company and have them do one of the following:</span></span>
    
      - <span data-ttu-id="f006e-124">Ihnen Administratorrechte gewähren, damit Sie die Entwicklerwebsite selbst erstellen können.</span><span class="sxs-lookup"><span data-stu-id="f006e-124">Grant you admin rights, so you can create the Developer Site yourself.</span></span>
    
 
  - <span data-ttu-id="f006e-125">Die Website für Entwickler für Sie erstellen und Sie als Administrator für die Websitesammlung angeben.</span><span class="sxs-lookup"><span data-stu-id="f006e-125">Create the Developer Site for you, and specify you as an admin for the site collection.</span></span>
    
 
2. <span data-ttu-id="f006e-126">Klicken Sie auf die Schaltfläche „App-Startfeld“ ganz links auf der Navigationsleiste am oberen Bildschirmrand.</span><span class="sxs-lookup"><span data-stu-id="f006e-126">Click the App Launcher button on the far left of the navigation bar at top.</span></span>
    
 
3. <span data-ttu-id="f006e-127">Klicken Sie auf die Kachel **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f006e-127">Click the  **Admin** tile.</span></span>
    
 
4. <span data-ttu-id="f006e-128">Erweitern Sie in der Navigationsstruktur links den Eintrag **Admin**, und wählen Sie **SharePoint** aus.</span><span class="sxs-lookup"><span data-stu-id="f006e-128">In the navigation tree on the left, expand  **Admin**, and select  **SharePoint**.</span></span>
    
 
5. <span data-ttu-id="f006e-129">Klicken Sie im **SharePoint Admin Center** auf der Registerkarte **Websitesammlungen** auf **Neu > Private Websitesammlung**.</span><span class="sxs-lookup"><span data-stu-id="f006e-129">In the  **SharePoint admin center**, on the **Site Collections** tab, click **New > Private Site Collection**.</span></span>
    
  ![Option für neue Websitesammlung im SharePoint Admin Center](../images/SPAdminCenter_newSiteCollection.png)
 

 

 
6. <span data-ttu-id="f006e-131">Geben Sie im Dialogfeld **Neue Websitesammlung** Informationen zu Ihrer Entwicklerwebsite an.</span><span class="sxs-lookup"><span data-stu-id="f006e-131">In the  **New Site Collection** dialog box, provide information about your Developer Site.</span></span>
    
|<span data-ttu-id="f006e-132">**Feld**</span><span class="sxs-lookup"><span data-stu-id="f006e-132">**Field**</span></span>|<span data-ttu-id="f006e-133">**Wert**</span><span class="sxs-lookup"><span data-stu-id="f006e-133">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f006e-134">**Titel**</span><span class="sxs-lookup"><span data-stu-id="f006e-134">**Title**</span></span>|<span data-ttu-id="f006e-135">Der Name, den Sie Ihrer Entwicklerwebsite geben möchten.</span><span class="sxs-lookup"><span data-stu-id="f006e-135">The name you want to give your Developer Site.</span></span>|
|<span data-ttu-id="f006e-136">Liste **Öffentliche Websiteadresse**</span><span class="sxs-lookup"><span data-stu-id="f006e-136">**Public Website Address** list</span></span>|<span data-ttu-id="f006e-137">Ein Domänenname und ein URL-Pfad – entweder **/sites/** oder **/teams/**; geben Sie dann einen URL-Namen für die Websitesammlung ein.</span><span class="sxs-lookup"><span data-stu-id="f006e-137">A domain name and a URL path—either  **/sites/** or **/teams/**—and then type a URL name for the site collection.</span></span>|
|<span data-ttu-id="f006e-138">Liste **Sprache auswählen** im Abschnitt **Vorlagenauswahl**</span><span class="sxs-lookup"><span data-stu-id="f006e-138">**Select a language** list in the **Template Selection** section</span></span>|<span data-ttu-id="f006e-p106">Eine Primärsprache für Ihre Entwicklerwebsite. **Stellen Sie sicher, dass Sie die gewünschte Sprache für die Websitesammlung „Entwicklerwebsite“ auswählen, da diese nach der Auswahl nicht mehr geändert werden kann. **Das Auswählen einer Sprache für Ihre Entwicklerwebsite hat keine Auswirkungen auf die Sprachen, die Sie in Ihren Office- und SharePoint- Add-Ins verfügbar machen können. Sie können für Ihre Websites die mehrsprachige SharePoint-Oberfläche aktivieren, doch die Primärsprache der Websitesammlung wählen Sie hier aus.</span><span class="sxs-lookup"><span data-stu-id="f006e-p106">A primary language to use for your Developer Site. **Be sure to select the appropriate language for the Developer Site site collection, because once you choose it, it can't be changed.**Selecting a language for your Developer Site does not affect the languages you can make available in your Office and SharePoint Add-ins.You can enable the SharePoint multiple language interface on your sites, but the primary language for the site collection is the one you choose here.</span></span>|
|<span data-ttu-id="f006e-141">Abschnitt **Vorlagenauswahl** auf der Registerkarte **Zusammenarbeit** unter **Vorlage auswählen**</span><span class="sxs-lookup"><span data-stu-id="f006e-141">**Template Selection** section, on the **Collaboration** tab under **Select a template**</span></span>|<span data-ttu-id="f006e-142">Klicken Sie auf **Entwicklerwebsite**.</span><span class="sxs-lookup"><span data-stu-id="f006e-142">Choose  **Developer Site.**</span></span>|
|<span data-ttu-id="f006e-143">**Zeitzone**</span><span class="sxs-lookup"><span data-stu-id="f006e-143">**Time Zone**</span></span>|<span data-ttu-id="f006e-144">Die zum Gebietsschema Ihrer Enwicklerwebsite gehörige Zeitzone.</span><span class="sxs-lookup"><span data-stu-id="f006e-144">Time zone that's appropriate for the locale of your Developer Site.</span></span>|
|<span data-ttu-id="f006e-145">**Administrator**</span><span class="sxs-lookup"><span data-stu-id="f006e-145">**Administrator**</span></span>|<span data-ttu-id="f006e-146">Der Benutzername des Websitesammlungsadministrators.</span><span class="sxs-lookup"><span data-stu-id="f006e-146">The user name of your site collection administrator.</span></span>|
|<span data-ttu-id="f006e-147">**Speicherkontingent**</span><span class="sxs-lookup"><span data-stu-id="f006e-147">**Storage Quota**</span></span>|<span data-ttu-id="f006e-148">Die Anzahl der Megabytes (MB), die Sie dieser Websitesammlung zuordnen möchten.</span><span class="sxs-lookup"><span data-stu-id="f006e-148">Number of megabytes (MB) you want to allocate to this Developer Site site collection.</span></span>|
|<span data-ttu-id="f006e-149">**Serverressourcenkontingent**</span><span class="sxs-lookup"><span data-stu-id="f006e-149">**Server Resource Quota**</span></span>|<span data-ttu-id="f006e-p107">Die Menge an Ressourcen, die Sie der Websitesammlung zuordnen möchten. Dieser Wert ist eine Kombination von Leistungsmetriken (wie Prozessorzeit und unbehandelten Ausnahmen), die zu Code in Sandkastenlösungen gehören. Wenn der Wert ein Tageskontingent überschreitet, wird der Sandkasten für diese Websitesammlung deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="f006e-p107">The amount of resources to allocate to the site collection. This number is a combination of performance metrics (such as processor time and unhandled exceptions) that pertain to code in sandboxed solutions. When the level exceeds a daily quota, the sandbox is turned off for this site collection.</span></span>|
7. <span data-ttu-id="f006e-153">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="f006e-153">Click  **OK**.</span></span>
    
    <span data-ttu-id="f006e-p108">Die URL der neuen Entwicklerwebsite wird in der Liste **Websitesammlungen** angezeigt. Wenn die Erstellung der Website abgeschlossen ist, können Sie zur URL navigieren, um Ihre Entwicklerwebsite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="f006e-p108">You'll see the new developer site URL in the  **Site Collections** list. When the site creation is finished, you can navigate to the URL to open your Developer Site.</span></span>
    
  ![Bereitstellung der neuen Websitesammlung](../images/SPAdminCenter_newSiteCollection_provisioning.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="f006e-157">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f006e-157">Additional resources</span></span>
<span data-ttu-id="f006e-158"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f006e-158"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="f006e-159">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f006e-159">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f006e-160">Erstellen oder Löschen einer Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="f006e-160">Create or delete a site collection</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/create-or-delete-a-site-collection-HA102772354.aspx?CTT=1)
    
 

