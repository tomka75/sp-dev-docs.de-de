---
title: Erste Schritte beim Erstellen von einem Anbieter gehosteten SharePoint-Add-Ins
description: Richten Sie eine Entwicklungsumgebung ein und erstellen Sie Ihr erstes, von einem Anbieter gehostetes SharePoint-Add-In.
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 8dfd0b77765d9dd6305fc6bb282c52bb5fb1dd02
ms.sourcegitcommit: 074f3a7983a7b253f56f8c670a0290c27bb7734b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="get-started-creating-provider-hosted-sharepoint-add-ins"></a><span data-ttu-id="bfe93-103">Erste Schritte beim Erstellen eines von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="bfe93-103">Get started creating provider-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="bfe93-104">Vom Anbieter gehostete Add-Ins sind eine der zwei Haupttypen von SharePoint-Add-Ins. Einen schnellen Überblick über SharePoint-Add-Ins und die zwei verschiedenen Typen finden Sie unter [SharePoint Add-Ins](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="bfe93-104">Provider-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see  [SharePoint Add-ins](sharepoint-add-ins.md). Here's a summary of provider-hosted add-ins:</span></span> 

<span data-ttu-id="bfe93-105">Es folgt eine Zusammenfassung zu vom Anbieter gehosteten Add-Ins:</span><span class="sxs-lookup"><span data-stu-id="bfe93-105">Here's a summary of provider-hosted add-ins:</span></span>

- <span data-ttu-id="bfe93-106">Sie enthalten Webanwendungen, Dienste oder Datenbanken, die extern über eine SharePoint-Farm oder ein SharePoint Online-Abonnement gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="bfe93-106">They include a web application, or service, or database that is hosted externally from the SharePoint farm or SharePoint Online subscription. They may also include SharePoint components. You can host the external components on any web-hosting stack, including the LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span> <span data-ttu-id="bfe93-107">Sie können auch SharePoint-Komponenten enthalten.</span><span class="sxs-lookup"><span data-stu-id="bfe93-107">They may also include SharePoint components.</span></span> <span data-ttu-id="bfe93-108">Sie können die externen Komponenten in einem beliebigen Webhostingstapel, einschließlich des LAMP-Stapels (Linux, Apache, MySQL und PHP) hosten.</span><span class="sxs-lookup"><span data-stu-id="bfe93-108">They include a web application, or service, or database that is hosted externally from the SharePoint farm or sposhort subscription. They may also include SharePoint components. You can host the external components on any web-hosting stack, including the LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

- <span data-ttu-id="bfe93-109">Die benutzerdefinierte Geschäftslogik im Add-In muss entweder in den externen Komponenten oder in JavaScript auf benutzerdefinierten SharePoint-Seiten ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfe93-109">The custom business logic in the add-in has to run on either the external components or in JavaScript on custom SharePoint pages.</span></span>
    
- <span data-ttu-id="bfe93-110">Schritt 1: Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="bfe93-110">Step 1 - Set up your dev environment</span></span>

- <span data-ttu-id="bfe93-111">Schritt 2: Erstellen des App-Projekts</span><span class="sxs-lookup"><span data-stu-id="bfe93-111">Step 2 - Create the app project</span></span>

- <span data-ttu-id="bfe93-112">Schritt 3: Programmieren der App</span><span class="sxs-lookup"><span data-stu-id="bfe93-112">Step 3 - Code your app</span></span>

<span data-ttu-id="bfe93-113"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-113"></span></span>
## <a name="set-up-your-dev-environment"></a><span data-ttu-id="bfe93-114">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="bfe93-114">Set up your dev environment</span></span>

<span data-ttu-id="bfe93-p102">Es gibt verschiedene Möglichkeiten zum Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins. In diesem Abschnitt wird die einfachste Möglichkeit erläutert. Alternativen finden Sie unter  [Zusätzliche Ressourcen](#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="bfe93-p102">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way. For alternatives, see  [Additional resources](#bk_addresources).</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="bfe93-117">Abrufen der Tools</span><span class="sxs-lookup"><span data-stu-id="bfe93-117">Get the tools</span></span>

- <span data-ttu-id="bfe93-118">Falls Sie **Visual Studio 2013** oder höher noch nicht installiert haben: Installieren Sie es mithilfe der Anweisungen unter [Installieren von Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="bfe93-118">If you don't already have  **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio). We recommend using the  latest version from the Microsoft Download Center.</span></span> <span data-ttu-id="bfe93-119">Wir empfehlen die Verwendung der [aktuellen Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="bfe93-119">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
 
- <span data-ttu-id="bfe93-120">Visual Studio umfasst die **Microsoft Office Developer Tools für Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-120">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="bfe93-121">Gelegentlich wird jedoch zwischen zwei Updates von Visual Studio eine neue Version der Tools veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="bfe93-121">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="bfe93-122">Führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus, um sicherzustellen, dass Sie die aktuelle Version der Tools haben.</span><span class="sxs-lookup"><span data-stu-id="bfe93-122">Visual Studio includes the  Microsoft Office Developer Tools for Visual Studio. Sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 

<span data-ttu-id="bfe93-123"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-123"></span></span>
### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="bfe93-124">Registrieren für eine Office 365-Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="bfe93-124">Sign up for an Office 365 Developer Site</span></span>

> [!NOTE]
> <span data-ttu-id="bfe93-125">Möglicherweise haben Sie bereits Zugriff auf eine Office 365-Entwicklerwebsite:</span><span class="sxs-lookup"><span data-stu-id="bfe93-125">Note You might already have access to an Office 365 Developer Site:</span></span> 
> - <span data-ttu-id="bfe93-p105">**Sind Sie MSDN-Abonnent?** Visual Studio Ultimate und Visual Studio Premium mit MSDN-Abonnenten erhalten als Bonus ein einjähriges Office 365 Developer-Abonnement. [Lösen Sie Ihren Bonus heute ein.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="bfe93-p105">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="bfe93-129">**Besitzen Sie einen der folgenden Office 365-Abonnementpläne?**</span><span class="sxs-lookup"><span data-stu-id="bfe93-129">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="bfe93-130">Wenn ja, kann ein Administrator des jeweiligen Office 365-Abonnements über das [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx) eine Entwicklerwebsite für Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-130">If so, an administrator of the Office 365 subscription can create a Developer Site by using the [Office 365 admin center. For more information, see  Create a developer site on an existing Office 365 subscription](https://portal.microsoftonline.com/admin/default.aspx).</span></span> <span data-ttu-id="bfe93-131">Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="bfe93-131">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="bfe93-132">Sie haben drei Möglichkeiten, einen Office 365-Plan zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="bfe93-132">There are three ways to get an Office 365 plan.</span></span> 

- <span data-ttu-id="bfe93-133">Sie können die [kostenlose 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) nutzen, die eine einzige Benutzerlizenz enthält.</span><span class="sxs-lookup"><span data-stu-id="bfe93-133">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>

- <span data-ttu-id="bfe93-134">Sie können ein [Office 365-Entwicklerabonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK) erwerben.</span><span class="sxs-lookup"><span data-stu-id="bfe93-134">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 

- <span data-ttu-id="bfe93-135">Sie können sich über das Office 365-Entwicklerprogramm für ein kostenloses Office 365-Entwicklerkonto mit einem Jahr Laufzeit registrieren.</span><span class="sxs-lookup"><span data-stu-id="bfe93-135">Sign up for a free, one-year Office 365 developer account through the Office 365 Developer Program.</span></span> <span data-ttu-id="bfe93-136">Weitere Informationen finden Sie [hier](http://dev.office.com/devprogram). Alternativ können Sie direkt das [Registrierungsformular](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170) ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-136">[Get more information](http://dev.office.com/devprogram), or go straight to [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span></span> <span data-ttu-id="bfe93-137">Nach der Registrierung für das Entwicklerprogramm erhalten Sie eine E-Mail mit einem Link, unter dem Sie sich für ein Entwicklerkonto registrieren können.</span><span class="sxs-lookup"><span data-stu-id="bfe93-137">You'll get an email after you sign up for the developer program with a link to sign up for the developer account.</span></span> <span data-ttu-id="bfe93-138">Nachfolgend finden Sie eine Anleitung.</span><span class="sxs-lookup"><span data-stu-id="bfe93-138">Use the following instructions.</span></span>

> [!TIP]
> <span data-ttu-id="bfe93-139">Öffnen Sie diese Links in einem anderen Fenster oder auf einer anderen Registerkarte, damit Sie die Anleitung jederzeit einsehen können.</span><span class="sxs-lookup"><span data-stu-id="bfe93-139">Open these links in another window or tab in order to keep the following instructions handy.</span></span>

1. <span data-ttu-id="bfe93-140">Die erste Seite des Registrierungsformulars ist selbsterklärend. Geben Sie die geforderten Informationen ein, und klicken Sie anschließend auf **Next**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-140">The first page (not shown) of the signup form is self-explanatory; supply the requested information and then choose  **Next**.</span></span>
    
2. <span data-ttu-id="bfe93-141">Geben Sie auf der zweiten Seite, die in Abbildung 1 gezeigt ist, eine Benutzer-ID für den Administrator des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="bfe93-141">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
   <span data-ttu-id="bfe93-142">*Abbildung 1: Domänenname der Office 365-Entwicklerwebsite*</span><span class="sxs-lookup"><span data-stu-id="bfe93-142">*Figure 1. Office 365 Developer Site domain name*</span></span>

   ![Seite 2 des Registrierungsformulars für ein Office 365-Konto](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)

3. <span data-ttu-id="bfe93-144">Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**, zum Beispiel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="bfe93-144">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
   <span data-ttu-id="bfe93-145">Sobald die Registrierung abgeschlossen ist, können Sie sich mit den daraus resultierenden Anmeldeinformationen (im Format *Benutzer-ID@ihredomäne.onmicrosoft.com*) bei Ihrer Office 365-Portalwebsite anmelden und dort Ihr Konto verwalten.</span><span class="sxs-lookup"><span data-stu-id="bfe93-145">After signup, you use the resulting credentials (in the format  *UserID*yourdomain.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is set up at your new domain: http:// yourdomain.sharepoint.com.</span></span> <span data-ttu-id="bfe93-146">Ihre SharePoint Online-Entwicklerwebsite wird in Ihrer neuen Domäne eingerichtet: `http://yourdomain.sharepoint.com`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-146">Your SharePoint Online Developer Site is set up at your new domain: `http://yourdomain.sharepoint.com`.</span></span>
    
4. <span data-ttu-id="bfe93-147">Klicken Sie auf **Next**, und füllen Sie die letzte Seite des Formulars aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-147">Select **Next** and fill out the final page of the form.</span></span> <span data-ttu-id="bfe93-148">Wenn Sie sich telefonisch einen Bestätigungscode durchgeben lassen möchten, können Sie wahlweise eine Mobiltelefonnummer oder eine Festnetznummer angeben. VoIP-Nummern (Voice over Internet Protocol) werden jedoch *nicht* unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bfe93-148">Choose  Next and fill out the final page of the form. If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="bfe93-149">Falls Sie zum Zeitpunkt Ihrer Registrierung für ein Entwicklerkonto noch bei einem anderen Microsoft-Konto angemeldet sind, wird unter Umständen die folgende Meldung angezeigt: „Sorry, that user ID you entered didn‘t work.</span><span class="sxs-lookup"><span data-stu-id="bfe93-149">If you're signed in to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work.</span></span> <span data-ttu-id="bfe93-150">It looks like it's not valid.</span><span class="sxs-lookup"><span data-stu-id="bfe93-150">It looks like it's not valid.</span></span> <span data-ttu-id="bfe93-151">Be sure you enter the user ID that your organization assigned to you.</span><span class="sxs-lookup"><span data-stu-id="bfe93-151">Be sure you enter the user ID that your organization assigned to you.</span></span> <span data-ttu-id="bfe93-152">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*.“</span><span class="sxs-lookup"><span data-stu-id="bfe93-152">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*."</span></span> 
   
   > <span data-ttu-id="bfe93-153">Sollte diese Meldung angezeigt werden, müssen Sie sich von dem betreffenden Microsoft-Konto abmelden und die Registrierung erneut versuchen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-153">If you see that message, sign out of the Microsoft account you were using and try again.</span></span> <span data-ttu-id="bfe93-154">Wird Ihnen die Meldung weiterhin angezeigt: Leeren Sie den Cache Ihres Browsers, oder schalten Sie um auf **InPrivate-Browsen**, und füllen Sie das Formular erneut aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-154">If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to **InPrivate Browsing** and then fill out the form.</span></span>

   <span data-ttu-id="bfe93-155">Sobald der Registrierungsprozess abgeschlossen ist, wird in Ihrem Browser die Office 365-Installationsseite geöffnet.</span><span class="sxs-lookup"><span data-stu-id="bfe93-155">After you finish the signup process, your browser opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span> <span data-ttu-id="bfe93-156">Klicken Sie auf das Symbol „Admin“, um das Admin Center zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-156">Select the Admin icon to open the admin center page.</span></span>
 
   <span data-ttu-id="bfe93-157">*Abbildung 2: Office 365 Admin Center-Seite*</span><span class="sxs-lookup"><span data-stu-id="bfe93-157">*Figure 2. Office 365 admin center page*</span></span>

   ![Screenshot mit dem Office 365 Admin Center](../images/SP15_Office365AdminInset_border.png)

5. <span data-ttu-id="bfe93-p113">Warten Sie, bis der Einrichtungsprozess für Ihre Entwicklerwebsite abgeschlossen ist. Nach Abschluss der Bereitstellung aktualisieren Sie die Admin Center-Seite im Browser.</span><span class="sxs-lookup"><span data-stu-id="bfe93-p113">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>
     
6. <span data-ttu-id="bfe93-161">Klicken Sie oben links auf der Seite auf **Build Add-ins**, um Ihre Entwicklerwebsite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-161">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="bfe93-162">Nun sollten Sie eine Website sehen, die wie Abbildung 3 aussieht.</span><span class="sxs-lookup"><span data-stu-id="bfe93-162">Then, choose the Build Apps link in the upper left corner of the page to open your off365devsiteshort. You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="bfe93-163">Dass die Liste **Add-ins in Testing** auf der Seite angezeigt wird, ist der Beleg dafür, dass die Website auf Basis der Vorlage für SharePoint-Entwicklerwebsites erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="bfe93-163">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="bfe93-164">Falls stattdessen eine normale Teamwebsite angezeigt wird: Warten Sie einige Minuten, und starten Sie dann die Website neu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-164">If you see a regular team site instead, wait a few minutes and launch your site again.</span></span>
    
7. <span data-ttu-id="bfe93-165">Notieren Sie die URL der Website. Diese wird verwendet, wenn Sie SharePoint-Add-Ins-Projekte in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-165">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
   <span data-ttu-id="bfe93-166">*Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test*</span><span class="sxs-lookup"><span data-stu-id="bfe93-166">*Figure 3. Your Developer Site home page with the Add-ins in Testing list*</span></span>

   ![Screenshot, auf dem die Entwicklerwebsite-Startseite angezeigt ist](../images/SP15_DeveloperSiteHome_border.png)
 
<span data-ttu-id="bfe93-168"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-168"></span></span>
## <a name="create-the-add-in-project"></a><span data-ttu-id="bfe93-169">Erstellen des Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="bfe93-169">Create the add-in project</span></span>

1. <span data-ttu-id="bfe93-170">Starten Sie Visual Studio mit der Option **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-170">Start Visual Studio using the **Run as administrator** option.</span></span>
    
2. <span data-ttu-id="bfe93-171">Klicken Sie in Visual Studio auf **Datei** > **Neu** > **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-171">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
    
3. <span data-ttu-id="bfe93-172">Erweitern Sie im Dialogfeld **Neues Projekt** den Knoten **Visual C#**, dann den Knoten **Office/SharePoint**, und wählen Sie den Knoten **Add-Ins** > **SharePoint-Add-In** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-172">In the  **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose **Add-ins** > **SharePoint Add-in**.</span></span>
    
4. <span data-ttu-id="bfe93-173">Geben Sie dem Projekt den Namen **SampleAddIn**, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-173">Name the project SampleAddIn, and then choose  OK.</span></span>
   
5. <span data-ttu-id="bfe93-174">Gehen Sie im Dialogfeld **Einstellungen für das SharePoint-Add-In angeben** folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="bfe93-174">In the first  **Specify the SharePoint Add-in Settings** dialog box, do the following:</span></span>
    
   - <span data-ttu-id="bfe93-175">Geben Sie die komplette URL der SharePoint-Website an, die Sie für das Debugging Ihres Add-Ins verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="bfe93-175">Provide the full URL of the SharePoint site that you want to use to debug your add-in.</span></span> <span data-ttu-id="bfe93-176">Gemeint ist die URL der Entwicklerwebsite.</span><span class="sxs-lookup"><span data-stu-id="bfe93-176">This is the URL of the Developer Site.</span></span> <span data-ttu-id="bfe93-177">Verwenden Sie HTTPS und nicht HTTP in der URL.</span><span class="sxs-lookup"><span data-stu-id="bfe93-177">Use HTTPS, not HTTP in the URL.</span></span> <span data-ttu-id="bfe93-178">An einem bestimmten Punkt während dieses Vorgangs oder kurz nachdem dieser Vorgang abgeschlossen wurde, werden Sie aufgefordert, sich bei dieser Website anzumelden.</span><span class="sxs-lookup"><span data-stu-id="bfe93-178">At some point during this procedure, or shortly after it completes, you will be prompted to sign in to this site.</span></span> <span data-ttu-id="bfe93-179">Der Zeitpunkt der Aufforderung ist unterschiedlich.</span><span class="sxs-lookup"><span data-stu-id="bfe93-179">The timing of the prompt varies.</span></span> <span data-ttu-id="bfe93-180">Verwenden Sie die Administratoranmeldeinformationen (in der Domäne \*.onmicrosoft.com), die Sie bei der Anmeldung bei Ihrer Entwicklerseite erstellt haben, z. B. MyName@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="bfe93-180">Use the administrator credentials (in the \*.onmicrosoft.com domain) that you created when you signed up for your Developer Site; for example MyName@contoso.onmicrosoft.com.</span></span>    

   - <span data-ttu-id="bfe93-181">Wählen Sie unter **Wie soll Ihr Add-In für SharePoint gehostet werden** die Option **Von Anbieter gehostet** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-181">Under  **How do you want to host your SharePoint Add-in**, choose  **Provider-hosted**.</span></span>

   - <span data-ttu-id="bfe93-182">Wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-182">Select **Next**.</span></span>  
 
6. <span data-ttu-id="bfe93-183">Wählen Sie auf der Seite **Ziel-SharePoint-Version angeben** die Option **SharePoint Online** und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-183">On the  **Specify the target SharePoint version** page, choose **SharePoint Online**, and then choose  **Next**.</span></span>

7. <span data-ttu-id="bfe93-184">Wählen Sie unter **Welchen Webanwendungsprojekttyp möchten Sie erstellen?**** ASP.NET Webformular-Anwendung**. Wählen Sie dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-184">Under  **Which type of web application project do you want to create?**, choose  **ASP.NET Web Forms Application**. Choose  **Next**.</span></span>

8. <span data-ttu-id="bfe93-185">Wählen Sie unter **Wie soll Ihr Add-In authentifiziert werden?**** Microsoft Azure-Zugriffssteuerungsdienst verwenden** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-185">Under  **How do you want your add-in to authenticate?**, choose  **Use Windows Azure Access Control Service**.</span></span>

9. <span data-ttu-id="bfe93-186">Wählen Sie im Assistenten **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="bfe93-186">In the wizard, choose  **Finish**.</span></span>
    
   <span data-ttu-id="bfe93-187">Ein Großteil der Konfiguration wird beim Öffnen der Lösung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bfe93-187">Much of the configuration is done when the solution opens.</span></span> <span data-ttu-id="bfe93-188">In der Visual Studio-Projektmappe werden zwei Projekte erstellt, eines für die SharePoint-Add-In und das andere für die ASP.NET-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="bfe93-188">Much of the configuration is done when the solution opens. Two projects are created in the Visual Studio solution - one for the SharePoint Add-in and the other for the ASP.NET web application.</span></span>

<span data-ttu-id="bfe93-189"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-189"></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="bfe93-190">Codieren Ihres Add-Ins</span><span class="sxs-lookup"><span data-stu-id="bfe93-190">Code your add-in</span></span>

1. <span data-ttu-id="bfe93-p117">Öffnen Sie die Datei AppManifest.xml. Geben Sie auf der Registerkarte **Berechtigungen** den Bereich der **Websitesammlung** und die **Lese**berechtigungsstufe an.</span><span class="sxs-lookup"><span data-stu-id="bfe93-p117">Open the AppManifest.xml file. On the **Permissions** tab, specify the **Site Collection** scope and the **Read** permission level.</span></span>

2. <span data-ttu-id="bfe93-193">Löschen Sie alle Markups innerhalb des `<body>`-Tags der Datei „Pages/Default.aspx“ Ihrer Webanwendung, und fügen Sie dann die folgenden HTML- und ASP.NET-Steuerelemente in `<body>` ein.</span><span class="sxs-lookup"><span data-stu-id="bfe93-193">Delete any markup inside the    tag of the Pages/Default.aspx file of your web application, and then add the following HTML and ASP.NET controls inside the   . This sample uses the  UpdatePanel control to enable partial page rendering.</span></span> <span data-ttu-id="bfe93-194">In diesem Beispiel wird das [UpdatePanel](http://msdn2.microsoft.com/de-DE/library/bb359258)-Steuerelement verwendet, um ein teilweises Seitenrendering zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="bfe93-194">This sample uses the [UpdatePanel](http://msdn2.microsoft.com/de-DE/library/bb359258) control to enable partial page rendering.</span></span>
    
    ```HTML
     <form id="form1" runat="server">
       <div>
         <asp:ScriptManager ID="ScriptManager1" runat="server"
                 EnablePartialRendering="true" />
         <asp:UpdatePanel ID="PopulateData" runat="server" UpdateMode="Conditional">
           <ContentTemplate>      
             <table border="1" cellpadding="10">
              <tr><th><asp:LinkButton ID="CSOM" runat="server" Text="Populate Data" 
                                    OnClick="CSOM_Click" /></th></tr>
              <tr><td>

             <h2>SharePoint Site</h2>
             <asp:Label runat="server" ID="WebTitleLabel"/>

             <h2>Current User:</h2>
             <asp:Label runat="server" ID="CurrentUserLabel" />

             <h2>Site Users</h2>
             <asp:ListView ID="UserList" runat="server">     
                 <ItemTemplate >
                   <asp:Label ID="UserItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                   </asp:Label><br />
                </ItemTemplate>
             </asp:ListView>

             <h2>Site Lists</h2>
                    <asp:ListView ID="ListList" runat="server">
                        <ItemTemplate >
                          <asp:Label ID="ListItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                         </asp:Label><br />
                       </ItemTemplate>
                   </asp:ListView>
                 </td>              
               </tr>
              </table>
            </ContentTemplate>
          </asp:UpdatePanel>
       </div>
     </form>
    ```

3. <span data-ttu-id="bfe93-195">Fügen Sie in der Datei „Default.aspx.cs“ der Webanwendung folgende Deklarationen hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-195">Add the following declarations to the Default.aspx.cs file of your web application.</span></span>
    
    ```C#
       using Microsoft.SharePoint.Client;
       using Microsoft.IdentityModel.S2S.Tokens;
       using System.Net;
       using System.IO;
       using System.Xml;
    ```

4. <span data-ttu-id="bfe93-196">Fügen Sie in der Datei „Default.aspx.cs“ der Webanwendung folgende Variablen in der [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1)-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-196">In the Default.aspx.cs file of your web application, add these variables inside the  [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1) class.</span></span>
    
   ```C#
     SharePointContextToken contextToken;
     string accessToken;
     Uri sharepointUrl;
     string siteName;
     string currentUser;
     List<string> listOfUsers = new List<string>();
     List<string> listOfLists = new List<string>();
   ```

5. <span data-ttu-id="bfe93-197">Fügen Sie die `RetrieveWithCSOM`-Methode in der [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1)-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-197">Add the `RetrieveWithCSOM` method inside the [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1) class.</span></span> <span data-ttu-id="bfe93-198">In dieser Methode wird SharePoint CSOM verwendet, um Informationen zu Ihrer Website abzurufen und auf der Seite anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-198">Add the   method inside the Page class. This method uses the SharePoint CSOM to retrieve information about your site and display it on the page.</span></span>
    
    ```C#
        // This method retrieves information about the host web by using the CSOM.
      private void RetrieveWithCSOM(string accessToken)
      {

          if (IsPostBack)
          {
              sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
          }            

          ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

          // Load the properties for the web object.
          Web web = clientContext.Web;
          clientContext.Load(web);
          clientContext.ExecuteQuery();

          // Get the site name.
          siteName = web.Title;

          // Get the current user.
          clientContext.Load(web.CurrentUser);
          clientContext.ExecuteQuery();
          currentUser = clientContext.Web.CurrentUser.LoginName;

          // Load the lists from the Web object.
          ListCollection lists = web.Lists;
          clientContext.Load<ListCollection>(lists);
          clientContext.ExecuteQuery();

          // Load the current users from the Web object.
          UserCollection users = web.SiteUsers;
          clientContext.Load<UserCollection>(users);
          clientContext.ExecuteQuery();

          foreach (User siteUser in users)
          {
              listOfUsers.Add(siteUser.LoginName);
          }

          foreach (List list in lists)
          {
              listOfLists.Add(list.Title);
          }
      }
    ```

6. <span data-ttu-id="bfe93-199">Fügen Sie die `CSOM_Click`-Methode in der [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1)-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-199">Add the `CSOM_Click` method inside the [Page](http://msdn2.microsoft.com/de-DE/library/dfbt9et1) class.</span></span> <span data-ttu-id="bfe93-200">Diese Methode löst das Ereignis aus, das auftritt, wenn der Benutzer auf den Link **Daten auffüllen** klickt.</span><span class="sxs-lookup"><span data-stu-id="bfe93-200">Add the   method inside the Page class. This method triggers the event that occurs when the user clicks the **Populate Data** link.</span></span>
    
    ```C#
      protected void CSOM_Click(object sender, EventArgs e)
    {
        string commandAccessToken = ((LinkButton)sender).CommandArgument;
        RetrieveWithCSOM(commandAccessToken);
        WebTitleLabel.Text = siteName;
        CurrentUserLabel.Text = currentUser;
        UserList.DataSource = listOfUsers;
        UserList.DataBind();
        ListList.DataSource = listOfLists;
        ListList.DataBind();    
     }
    ```

7. <span data-ttu-id="bfe93-201">Ersetzen Sie zunächst die vorhandene `Page_Load`-Methode durch diese.</span><span class="sxs-lookup"><span data-stu-id="bfe93-201">Replace the existing `Page_Load` method with this one.</span></span> <span data-ttu-id="bfe93-202">Die `Page_Load`-Methode verwendet Methoden in der Datei „TokenHelper.cs", um den Kontext aus dem `Request`-Objekt abzurufen und ein Zugriffstoken von Microsoft Azure Access Control Service (ACS) anzufordern.</span><span class="sxs-lookup"><span data-stu-id="bfe93-202">Replace the existing   method with this one. The `Page_Load` method uses methods in the TokenHelper.cs file to retrieve the context from the `Request` object and get an access token from Microsoft Azure Access Control Service (ACS).</span></span>
    
    ```C#
      // The Page_load method fetches the context token and the access token. 
    // The access token is used by all of the data retrieval methods.
    protected void Page_Load(object sender, EventArgs e)
    {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

        if (contextTokenString != null)
        {
            contextToken =
                TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

            sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
            accessToken =
                        TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                        .AccessToken;

             // For simplicity, this sample assigns the access token to the button's CommandArgument property. 
             // In a production add-in, this would not be secure. The access token should be cached on the server-side.
            CSOM.CommandArgument = accessToken;
        }
        else if (!IsPostBack)
        {
            Response.Write("Could not find a context token.");
            return;
        }
    }
    ```

8. <span data-ttu-id="bfe93-203">Die Datei „Default.aspx.cs“ sollte wie folgt aussehen, wenn Sie fertig sind.</span><span class="sxs-lookup"><span data-stu-id="bfe93-203">The Default.aspx.cs file should look like this when you're done.</span></span>
    
    ```C#
      using System;
      using System.Collections.Generic;
      using System.Linq;
      using System.Web;
      using System.Web.UI;
      using System.Web.UI.WebControls;

      using Microsoft.SharePoint.Client;
      using Microsoft.IdentityModel.S2S.Tokens;
      using System.Net;
      using System.IO;
      using System.Xml;

      namespace SampleAddInWeb
      {
          public partial class Default : System.Web.UI.Page
          {
              SharePointContextToken contextToken;
              string accessToken;
              Uri sharepointUrl;
              string siteName;
              string currentUser;
              List<string> listOfUsers = new List<string>();
              List<string> listOfLists = new List<string>();

              protected void Page_PreInit(object sender, EventArgs e)
              {
                  Uri redirectUrl;
                  switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
                  {
                      case RedirectionStatus.Ok:
                          return;
                      case RedirectionStatus.ShouldRedirect:
                          Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                          break;
                      case RedirectionStatus.CanNotRedirect:
                          Response.Write("An error occurred while processing your request.");
                          Response.End();
                          break;
                  }
              }

              protected void CSOM_Click(object sender, EventArgs e)
              {
                  string commandAccessToken = ((LinkButton)sender).CommandArgument;
                  RetrieveWithCSOM(commandAccessToken);
                  WebTitleLabel.Text = siteName;
                  CurrentUserLabel.Text = currentUser;
                  UserList.DataSource = listOfUsers;
                  UserList.DataBind();
                  ListList.DataSource = listOfLists;
                  ListList.DataBind();
              }

              // This method retrieves information about the host web by using the CSOM.
              private void RetrieveWithCSOM(string accessToken)
              {

                  if (IsPostBack)
                  {
                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                  }

                  ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

                  // Load the properties for the web object.
                  Web web = clientContext.Web;
                  clientContext.Load(web);
                  clientContext.ExecuteQuery();

                  // Get the site name.
                  siteName = web.Title;

                  // Get the current user.
                  clientContext.Load(web.CurrentUser);
                  clientContext.ExecuteQuery();
                  currentUser = clientContext.Web.CurrentUser.LoginName;

                  // Load the lists from the Web object.
                  ListCollection lists = web.Lists;
                  clientContext.Load<ListCollection>(lists);
                  clientContext.ExecuteQuery();

                  // Load the current users from the Web object.
                  UserCollection users = web.SiteUsers;
                  clientContext.Load<UserCollection>(users);
                  clientContext.ExecuteQuery();

                  foreach (User siteUser in users)
                  {
                      listOfUsers.Add(siteUser.LoginName);
                  }

                  foreach (List list in lists)
                  {
                      listOfLists.Add(list.Title);
                  }
              }

              protected void Page_Load(object sender, EventArgs e)
              {
                  string contextTokenString = 
                       TokenHelper.GetContextTokenFromRequest(Request);

                  if (contextTokenString != null)
                  {
                      contextToken =
                          TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                      accessToken =
                          TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                     .AccessToken;
                      CSOM.CommandArgument = accessToken;
                  }
                  else if (!IsPostBack)
                  {
                      Response.Write("Could not find a context token.");
                      return;
                  }
              }
          }
      }
     
    ```

9. <span data-ttu-id="bfe93-204">Drücken Sie auf die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-204">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="bfe93-205">Wenn ein Dialogfeld **Sicherheitshinweis** angezeigt wird, das Sie danach fragt, ob Sie dem selbstsignierten Localhost-Zertifikat vertrauen, klicken Sie auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-205">Use the F5 key to deploy and run your add-in. If you see a  **Security Alert** window that asks you to trust the self-signed Localhost certificate, choose **Yes**.</span></span>
    
10. <span data-ttu-id="bfe93-206">Wählen Sie **Vertrauen** auf der Zustimmungsseite, um die Berechtigungen für das Add-In zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="bfe93-206">Select **Trust It** on the consent page to grant permissions to the add-in.</span></span> <span data-ttu-id="bfe93-207">Visual Studio installiert die Webanwendung in IIS Express, installiert dann das Add-In in Ihrer Test-SharePoint-Website und startet diese.</span><span class="sxs-lookup"><span data-stu-id="bfe93-207">Visual Studio will install the web application to IIS Express and then install the add-in to your test SharePoint site and launch it.</span></span> <span data-ttu-id="bfe93-208">Es wird eine Seite mit der im folgenden Screenshot gezeigten Tabelle angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bfe93-208">You'll see a page that has the table shown in the following screen shot.</span></span> <span data-ttu-id="bfe93-209">Wenn Sie zusammenfassende Informationen zu Ihrer SharePoint-Website anzeigen möchten, wählen Sie **Daten auffüllen**.</span><span class="sxs-lookup"><span data-stu-id="bfe93-209">To see summary information about your SharePoint site, select **Populate Data**.</span></span>

   <span data-ttu-id="bfe93-210">*Abbildung 4. Startseite des grundlegenden vom Anbieter gehosteten Beispiel-Add-Ins*</span><span class="sxs-lookup"><span data-stu-id="bfe93-210">*Launch page of the basic provider-hosted add-in sample*</span></span>

   ![Startseite der selbst gehosteten Basis-App](../images/SP15_basicself-hostedapp.gif)
 
## <a name="additional-resources"></a><span data-ttu-id="bfe93-212">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bfe93-212">Additional resources</span></span>
<span data-ttu-id="bfe93-213"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-213"></span></span>

- <span data-ttu-id="bfe93-214">Andere Möglichkeiten zum Einrichten einer Entwicklungsumgebung, beispielsweise einer „rein lokalen“ Umgebung, finden Sie im Abschnitt [Tools](tools-and-environments-for-developing-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="bfe93-214">For other ways of setting up a development environment, such as an "all on-premise" environment, see the Tools section in the spappplural table of contents.</span></span>
- [<span data-ttu-id="bfe93-215">Installieren älterer Versionen von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfe93-215">Install earlier versions of Visual Studio</span></span>](https://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx)
- [<span data-ttu-id="bfe93-216">Visual Studio-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="bfe93-216">Visual Studio documentation</span></span>](https://docs.microsoft.com/de-DE/visualstudio/)
    
## <a name="next-steps"></a><span data-ttu-id="bfe93-217">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="bfe93-217">Next steps</span></span>
<span data-ttu-id="bfe93-218"><a name="SP15createprovider_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe93-218"></span></span>

<span data-ttu-id="bfe93-219">Um zu erfahren, wie Sie ein Add-In in das Benutzeroberflächenschema von SharePoint integrieren, lesen Sie bitte [Erteilen des Aussehens und Verhaltens von SharePoint für Ihr von einem Anbieter gehostetes Add-In](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md).</span><span class="sxs-lookup"><span data-stu-id="bfe93-219">To learn how to integrate an add-in into SharePoint's UI scheme, see [Give your provider-hosted add-in the SharePoint look-and-feel](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md).</span></span>


