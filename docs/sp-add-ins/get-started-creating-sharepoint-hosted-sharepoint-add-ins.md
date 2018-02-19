---
title: Erste Schritte beim Erstellen von SharePoint gehosteten SharePoint-Add-Ins
description: "Hier erfahren Sie, wie Sie eine Entwicklungsumgebung einrichten und Ihr erstes SharePoint-gehostetes SharePoint-Add-In erstellen können."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 6a2ed95aa06db5d6e4c6d9364cfcbfa8dc1b9f36
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="88ba2-103">Erste Schritte zum Erstellen SharePoint-gehosteter SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="88ba2-103">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="88ba2-104">SharePoint-gehostete Add-Ins sind einer der zwei Haupttypen von SharePoint-Add-Ins. Einen Überblick über SharePoint-Add-Ins und die zwei Add-In-Typen finden Sie unter [SharePoint Add-ins](sharepoint-add-ins.md). Hier die wichtigsten Punkte zu SharePoint-gehosteten Add-Ins:</span><span class="sxs-lookup"><span data-stu-id="88ba2-104">SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see [SharePoint Add-ins](sharepoint-add-ins.md). Here's a summary of SharePoint-hosted add-ins:</span></span>

- <span data-ttu-id="88ba2-105">Sie enthalten SharePoint-Listen, Webparts, Workflows, benutzerdefinierte Seiten und andere Komponenten, die auf einer Unterwebsite mit der Bezeichnung Add-In-Web der SharePoint-Website installiert sind, wo das Add-In installiert ist.</span><span class="sxs-lookup"><span data-stu-id="88ba2-105">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>
- <span data-ttu-id="88ba2-106">Sie bestehen ausschließlich aus JavaScript-Code auf benutzerdefinierten SharePoint-Seiten.</span><span class="sxs-lookup"><span data-stu-id="88ba2-106">The only code they have is JavaScript on custom SharePoint pages.</span></span>

<span data-ttu-id="88ba2-107">In diesem Artikel führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="88ba2-107">In this article, you'll complete the following steps:</span></span>

- <span data-ttu-id="88ba2-108">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="88ba2-108">Set up your dev environment</span></span>
- <span data-ttu-id="88ba2-109">Erstellen des Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="88ba2-109">Create the add-in project</span></span>
- <span data-ttu-id="88ba2-110">Codieren Ihres Add-Ins</span><span class="sxs-lookup"><span data-stu-id="88ba2-110">Code your add-in</span></span>
- <span data-ttu-id="88ba2-111">Ausführen des Add-Ins und Testen der Liste</span><span class="sxs-lookup"><span data-stu-id="88ba2-111">Run the add-in and test the list</span></span>

<span data-ttu-id="88ba2-112"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-112"></span></span>
## <a name="set-up-your-dev-environment"></a><span data-ttu-id="88ba2-113">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="88ba2-113">Set up your dev environment</span></span>

<span data-ttu-id="88ba2-114">Es gibt zahlreiche verschiedene Möglichkeiten, eine Entwicklungsumgebung für SharePoint-Add-Ins einzurichten. In diesem Abschnitt wird die einfachste von ihnen beschrieben.</span><span class="sxs-lookup"><span data-stu-id="88ba2-114">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="88ba2-115">Installieren der Tools</span><span class="sxs-lookup"><span data-stu-id="88ba2-115">Get the tools</span></span>

- <span data-ttu-id="88ba2-116">Falls Sie **Visual Studio 2013** oder höher noch nicht installiert haben: Installieren Sie es mithilfe der Anweisungen unter [Installieren von Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="88ba2-116">If you don't already have **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="88ba2-117">Wir empfehlen die Verwendung der [aktuellen Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="88ba2-117">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>

- <span data-ttu-id="88ba2-118">Visual Studio umfasst die **Microsoft Office Developer Tools für Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-118">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="88ba2-119">Gelegentlich wird jedoch zwischen zwei Updates von Visual Studio eine neue Version der Tools veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="88ba2-119">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="88ba2-120">Führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus, um sicherzustellen, dass Sie die aktuelle Version der Tools haben.</span><span class="sxs-lookup"><span data-stu-id="88ba2-120">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>

<span data-ttu-id="88ba2-121">Als Referenz dienen [frühere Versionen von Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) oder andere [Visual Studio-Dokumentation](https://docs.microsoft.com/de-DE/visualstudio/).</span><span class="sxs-lookup"><span data-stu-id="88ba2-121">Reference [earlier versions of Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) or other [Visual Studio documentation](https://docs.microsoft.com/de-DE/visualstudio/).</span></span>

<span data-ttu-id="88ba2-122"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-122"></span></span>
### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="88ba2-123">Registrieren für eine Office 365-Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="88ba2-123">Sign up for an Office 365 Developer Site</span></span>

> [!NOTE]
> <span data-ttu-id="88ba2-124">Möglicherweise haben Sie bereits Zugriff auf eine Office 365-Entwicklerwebsite:</span><span class="sxs-lookup"><span data-stu-id="88ba2-124">You might already have access to an Office 365 Developer Site:</span></span>
> - <span data-ttu-id="88ba2-p103">**Sind Sie MSDN-Abonnent?** Visual Studio Ultimate und Visual Studio Premium mit MSDN-Abonnenten erhalten als Bonus ein einjähriges Office 365 Developer-Abonnement. [Lösen Sie Ihren Bonus heute ein.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="88ba2-p103">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="88ba2-128">**Besitzen Sie einen der folgenden Office 365-Abonnementpläne?**</span><span class="sxs-lookup"><span data-stu-id="88ba2-128">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="88ba2-129">Wenn ja, kann ein Administrator des jeweiligen Office 365-Abonnements über das [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx) eine Entwicklerwebsite für Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-129">If so, an administrator of the Office 365 subscription can create a Developer Site by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx).</span></span> <span data-ttu-id="88ba2-130">Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="88ba2-130">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="88ba2-131">Sie haben drei Möglichkeiten, einen Office 365-Plan zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="88ba2-131">There are three ways to get an Office 365 plan:</span></span> 

- <span data-ttu-id="88ba2-132">Sie können die [kostenlose 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) nutzen, die eine einzige Benutzerlizenz enthält.</span><span class="sxs-lookup"><span data-stu-id="88ba2-132">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>

- <span data-ttu-id="88ba2-133">Sie können ein [Office 365-Entwicklerabonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK) erwerben.</span><span class="sxs-lookup"><span data-stu-id="88ba2-133">Buy an [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 

- <span data-ttu-id="88ba2-134">Sie können sich über das Office 365-Entwicklerprogramm für ein kostenloses Office 365-Entwicklerkonto mit einem Jahr Laufzeit registrieren.</span><span class="sxs-lookup"><span data-stu-id="88ba2-134">Sign up for a free, one-year Office 365 developer account through the Office 365 Developer Program.</span></span> <span data-ttu-id="88ba2-135">Weitere Informationen finden Sie [hier](http://dev.office.com/devprogram). Alternativ können Sie direkt das [Registrierungsformular](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170) ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-135">[Get more information](http://dev.office.com/devprogram), or go straight to [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span></span> <span data-ttu-id="88ba2-136">Nach der Registrierung für das Entwicklerprogramm erhalten Sie eine E-Mail mit einem Link, unter dem Sie sich für ein Entwicklerkonto registrieren können.</span><span class="sxs-lookup"><span data-stu-id="88ba2-136">You'll get an email after you sign up for the developer program with a link to sign up for the developer account.</span></span> <span data-ttu-id="88ba2-137">Nachfolgend finden Sie eine Anleitung.</span><span class="sxs-lookup"><span data-stu-id="88ba2-137">Use the following instructions.</span></span>

> [!TIP]
> <span data-ttu-id="88ba2-138">Öffnen Sie diese Links in einem anderen Fenster oder auf einer anderen Registerkarte, damit Sie die Anleitung jederzeit einsehen können.</span><span class="sxs-lookup"><span data-stu-id="88ba2-138">Open these links in another window or tab to keep the following instructions handy.</span></span>

1. <span data-ttu-id="88ba2-139">Die erste Seite des Registrierungsformulars ist selbsterklärend. Geben Sie die geforderten Informationen ein, und klicken Sie anschließend auf **Next**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-139">The first page of the sign-up form is self-explanatory; supply the requested information, and then select **Next**.</span></span>

2. <span data-ttu-id="88ba2-140">Geben Sie auf der zweiten Seite, die in Abbildung 1 gezeigt ist, eine Benutzer-ID für den Administrator des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="88ba2-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
   
   <span data-ttu-id="88ba2-141">*Abbildung 1: Domänenname der Office 365-Entwicklerwebsite*</span><span class="sxs-lookup"><span data-stu-id="88ba2-141">*Figure 1. Office 365 Developer Site domain name*</span></span>

   ![Seite 2 des Registrierungsformulars für ein Office 365-Konto](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
   
3. <span data-ttu-id="88ba2-143">Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**, zum Beispiel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="88ba2-143">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
   <span data-ttu-id="88ba2-144">Sobald die Registrierung abgeschlossen ist, können Sie sich mit den daraus resultierenden Anmeldeinformationen (im Format *Benutzer-ID@ihredomäne.onmicrosoft.com*) bei Ihrer Office 365-Portalwebsite anmelden und dort Ihr Konto verwalten.</span><span class="sxs-lookup"><span data-stu-id="88ba2-144">After you sign up, you use the resulting credentials (in the format *UserID@yourdomain.onmicrosoft.com*) to sign in to your Office 365 portal site where you administer your account.</span></span> <span data-ttu-id="88ba2-145">Ihre SharePoint Online-Entwicklerwebsite wird in Ihrer neuen Domäne eingerichtet: `http://yourdomain.sharepoint.com`.</span><span class="sxs-lookup"><span data-stu-id="88ba2-145">Your SharePoint Online Developer Site is set up at your new domain: `http://yourdomain.sharepoint.com`.</span></span>
    
4. <span data-ttu-id="88ba2-146">Klicken Sie auf **Next**, und füllen Sie die letzte Seite des Formulars aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-146">Select **Next** and fill out the final page of the form.</span></span> <span data-ttu-id="88ba2-147">Wenn Sie sich telefonisch einen Bestätigungscode durchgeben lassen möchten, können Sie wahlweise eine Mobiltelefonnummer oder eine Festnetznummer angeben. VoIP-Nummern (Voice over Internet Protocol) werden jedoch *nicht* unterstützt.</span><span class="sxs-lookup"><span data-stu-id="88ba2-147">If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not* a VoIP (Voice over Internet Protocol) number.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="88ba2-148">Falls Sie zum Zeitpunkt Ihrer Registrierung für ein Entwicklerkonto noch bei einem anderen Microsoft-Konto angemeldet sind, wird unter Umständen die folgende Meldung angezeigt: „Sorry, that user ID you entered didn‘t work.</span><span class="sxs-lookup"><span data-stu-id="88ba2-148">If you're signed in to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work.</span></span> <span data-ttu-id="88ba2-149">It looks like it's not valid.</span><span class="sxs-lookup"><span data-stu-id="88ba2-149">It looks like it's not valid.</span></span> <span data-ttu-id="88ba2-150">Be sure you enter the user ID that your organization assigned to you.</span><span class="sxs-lookup"><span data-stu-id="88ba2-150">Be sure you enter the user ID that your organization assigned to you.</span></span> <span data-ttu-id="88ba2-151">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*.“</span><span class="sxs-lookup"><span data-stu-id="88ba2-151">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*."</span></span> 

   > <span data-ttu-id="88ba2-152">Sollte diese Meldung angezeigt werden, müssen Sie sich von dem betreffenden Microsoft-Konto abmelden und die Registrierung erneut versuchen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-152">If you see that message, sign out of the Microsoft account you were using and try again.</span></span> <span data-ttu-id="88ba2-153">Wird Ihnen die Meldung weiterhin angezeigt: Leeren Sie den Cache Ihres Browsers, oder schalten Sie um auf **InPrivate-Browsen**, und füllen Sie das Formular erneut aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-153">If you still get the message, clear your browser cache or switch to **InPrivate Browsing** and then fill out the form.</span></span>

   <span data-ttu-id="88ba2-154">Sobald der Registrierungsprozess abgeschlossen ist, wird in Ihrem Browser die Office 365-Installationsseite geöffnet.</span><span class="sxs-lookup"><span data-stu-id="88ba2-154">After you finish the sign-up process, your browser opens the Office 365 installation page.</span></span> <span data-ttu-id="88ba2-155">Klicken Sie auf das Symbol „Admin“, um das Admin Center zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-155">Select the Admin icon to open the admin center page.</span></span>

   <span data-ttu-id="88ba2-156">*Abbildung 2: Office 365 Admin Center-Seite*</span><span class="sxs-lookup"><span data-stu-id="88ba2-156">*Figure 2. Office 365 admin center page*</span></span>

   ![Screenshot mit dem Office 365 Admin Center](../images/SP15_Office365AdminInset_border.png)
 
5. <span data-ttu-id="88ba2-p111">Warten Sie, bis der Einrichtungsprozess für Ihre Entwicklerwebsite abgeschlossen ist. Nach Abschluss der Bereitstellung aktualisieren Sie die Admin Center-Seite im Browser.</span><span class="sxs-lookup"><span data-stu-id="88ba2-p111">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>

6. <span data-ttu-id="88ba2-160">Klicken Sie oben links auf der Seite auf **Build Add-ins**, um Ihre Entwicklerwebsite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-160">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="88ba2-161">Nun sollten Sie eine Website sehen, die wie Abbildung 3 aussieht.</span><span class="sxs-lookup"><span data-stu-id="88ba2-161">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="88ba2-162">Dass die Liste **Add-ins in Testing** auf der Seite angezeigt wird, ist der Beleg dafür, dass die Website auf Basis der Vorlage für SharePoint-Entwicklerwebsites erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="88ba2-162">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="88ba2-163">Falls stattdessen eine normale Teamwebsite angezeigt wird: Warten Sie einige Minuten, und starten Sie dann die Website neu.</span><span class="sxs-lookup"><span data-stu-id="88ba2-163">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>

7. <span data-ttu-id="88ba2-164">Notieren Sie die URL der Website. Diese wird verwendet, wenn Sie SharePoint-Add-Ins-Projekte in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-164">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>

   <span data-ttu-id="88ba2-165">*Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test*</span><span class="sxs-lookup"><span data-stu-id="88ba2-165">*Figure 3. Your Developer Site home page with the Add-ins in Testing list*</span></span>

   ![Screenshot, auf dem die Entwicklerwebsite-Startseite angezeigt ist](../images/SP15_DeveloperSiteHome_border.png)

<span data-ttu-id="88ba2-167"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-167"></span></span>
## <a name="create-the-add-in-project"></a><span data-ttu-id="88ba2-168">Erstellen des Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="88ba2-168">Create the add-in project</span></span>

1. <span data-ttu-id="88ba2-169">Starten Sie Visual Studio mit der Option **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-169">Start Visual Studio by using the **Run as administrator** option.</span></span>

2. <span data-ttu-id="88ba2-170">Klicken Sie in Visual Studio auf **Datei** > **Neu** > **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-170">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
 
3. <span data-ttu-id="88ba2-171">Erweitern Sie im Dialogfeld **Neues Projekt** zunächst den Knoten **Visual C#** und dann den Knoten **Office/SharePoint**. Klicken Sie nun auf **Add-Ins** > **Add-in for SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-171">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then select **Add-ins** > **Add-in for SharePoint**.</span></span>

4. <span data-ttu-id="88ba2-172">Geben Sie dem Projekt den Namen **EmployeeOrientation**, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-172">Name the project **EmployeeOrientation**, and then select **OK**.</span></span>

5. <span data-ttu-id="88ba2-173">Geben Sie im Dialogfeld **Specify the Add-in for SharePoint Settings** die vollständige URL der SharePoint-Website ein, die Sie zum Debuggen Ihres Add-Ins verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="88ba2-173">In the **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in.</span></span> <span data-ttu-id="88ba2-174">Gemeint ist die URL der Entwicklerwebsite.</span><span class="sxs-lookup"><span data-stu-id="88ba2-174">This is the URL of the Developer Site.</span></span> <span data-ttu-id="88ba2-175">(Verwenden Sie HTTPS in der URL, nicht HTTP.) Wählen Sie unter **Wie soll Ihr SharePoint-Add-In gehostet werden?** die Option **Von SharePoint gehostet** aus, und klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-175">(Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, select  **SharePoint-hosted**, and then select **Finish**.</span></span>

6. <span data-ttu-id="88ba2-176">Möglicherweise werden Sie aufgefordert, sich bei Ihrer Entwicklerwebsite anzumelden.</span><span class="sxs-lookup"><span data-stu-id="88ba2-176">You may be prompted to sign in to your Developer Site.</span></span> <span data-ttu-id="88ba2-177">Verwenden Sie in diesem Fall die Anmeldeinformationen des Abonnementadministrators.</span><span class="sxs-lookup"><span data-stu-id="88ba2-177">If so, use your subscription administrator's credentials.</span></span>

7. <span data-ttu-id="88ba2-178">Das Projekt wird erstellt. Öffnen Sie im Stammverzeichnis des Projekts die Datei **/Pages/Default.aspx**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-178">After the project is created, open the file **/Pages/Default.aspx** from the root of the project.</span></span> <span data-ttu-id="88ba2-179">Unter anderem lädt diese generierte Datei eines oder beide der zwei Skripts, die in SharePoint gehostet werden: „sp.runtime.js“ und „sp.js“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-179">Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js.</span></span> <span data-ttu-id="88ba2-180">Das Markup zum Laden dieser Dateien befindet sich im Steuerelement des Typs **Content** mit der ID **PlaceHolderAdditionalPageHead** am Anfang der Datei.</span><span class="sxs-lookup"><span data-stu-id="88ba2-180">The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**.</span></span> <span data-ttu-id="88ba2-181">Dieses Markup unterscheidet sich je nach der verwendeten Version von **Microsoft Office Developer Tools für Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-181">The markup varies depending on the version of **Microsoft Office Developer Tools for Visual Studio** that you are using.</span></span> <span data-ttu-id="88ba2-182">Für diese Tutorialreihe müssen beide Dateien geladen werden. Zudem müssen die Dateien mit herkömmlichen HTML-Tags des Typs **\<script\>** geladen werden statt mit Tags des Typs **\<SharePoint:ScriptLink\>**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-182">This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags.</span></span> 

    <span data-ttu-id="88ba2-183">Stellen Sie sicher, dass das Steuerelement **PlaceHolderAdditionalPageHead** die nachfolgenden Zeilen enthält, und zwar *direkt oberhalb* der Zeile `<meta name="WebPartPageExpansion" content="full" />`:</span><span class="sxs-lookup"><span data-stu-id="88ba2-183">Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above*  the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>
    
    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

8. <span data-ttu-id="88ba2-184">Suchen Sie in der Datei nach anderem Markup, das ebenfalls eine dieser Dateien lädt, und entfernen Sie dieses redundante Markup.</span><span class="sxs-lookup"><span data-stu-id="88ba2-184">Search the file for any other markup that also loads one or the other of these files and remove the redundant markup.</span></span> <span data-ttu-id="88ba2-185">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="88ba2-185">Save and close the file.</span></span>

<span data-ttu-id="88ba2-186"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-186"></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="88ba2-187">Programmieren des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="88ba2-187">Code your add-in</span></span>

<span data-ttu-id="88ba2-188">In Ihr erstes SharePoint-gehostetes SharePoint-Add-In integrieren wir die klassische SharePoint-Erweiterung: eine benutzerdefinierte Liste und eine Instanz dieser Liste.</span><span class="sxs-lookup"><span data-stu-id="88ba2-188">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>

1. <span data-ttu-id="88ba2-189">Öffnen Sie im **Projektmappen-Explorer** die Datei „AppManifest.xml".</span><span class="sxs-lookup"><span data-stu-id="88ba2-189">In **Solution Explorer**, open the AppManifest.xml file.</span></span>

2. <span data-ttu-id="88ba2-190">Der Manifest-Designer wird geöffnet. Ändern Sie die Zeichenfolge im Feld **Titel** in **Orientierung für Mitarbeiter**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-190">When the manifest designer opens, add a space between the words in the **Title** field so that it reads **Employee Orientation**.</span></span> <span data-ttu-id="88ba2-191">(Ändern Sie *keinesfalls* das Feld **Name**.)</span><span class="sxs-lookup"><span data-stu-id="88ba2-191">(Do  *not* change the **Name** field.)</span></span>

3. <span data-ttu-id="88ba2-192">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="88ba2-192">Save and close the file.</span></span>

4. <span data-ttu-id="88ba2-193">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Hinzufügen** > **Neuer Ordner** aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-193">Right-click the project in **Solution Explorer** and select **Add** > **New Folder**.</span></span> <span data-ttu-id="88ba2-194">Geben Sie dem Ordner den Namen „Listen“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-194">Name the folder Lists.</span></span>

5. <span data-ttu-id="88ba2-195">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie die Option **Hinzufügen** > **Neues Element** aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-195">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="88ba2-196">Das Dialogfeld **Neues Element hinzufügen** wird geöffnet, und der Knoten **Office/SharePoint** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="88ba2-196">The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

6. <span data-ttu-id="88ba2-197">Klicken Sie auf **Liste**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-197">Select **List**.</span></span> <span data-ttu-id="88ba2-198">Geben Sie der Liste den Namen **NewEmployeeOrientation**, und klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-198">Give it the name **NewEmployeeOrientation**, and then select **Add**.</span></span> 
 
7. <span data-ttu-id="88ba2-199">Übernehmen Sie im Assistent zum Anpassen von SharePoint auf der Seite **Listeneinstellungen auswählen** den Standardwert **NewEmployeeOrientation** als Anzeigename der Liste, und aktivieren Sie das Optionsfeld **Anpassbare Listenvorlage und eine Listeninstanz davon erstellen**. Wählen Sie dann aus der Dropdownliste die Option **Standard (benutzerdefinierte Liste)** aus, und klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-199">On the **Choose List Settings** page of the SharePoint Customization Wizard, leave the list display name at the default **NewEmployeeOrientation**, select the **Create a customizable list template and a list instance of it** option button, select **Default (Custom List)** on the drop-down list, and then select **Finish**.</span></span>

8. <span data-ttu-id="88ba2-p121">Der Assistent erstellt eine **NewEmployeeOrientation**-Listenvorlage mit einer untergeordneten Listeninstanz mit der Bezeichnung **NewEmployeeOrientationInstance**. Möglicherweise wird ein Listen-Designer geöffnet. Dieser wird in einem späteren Schritt verwendet.</span><span class="sxs-lookup"><span data-stu-id="88ba2-p121">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>

9. <span data-ttu-id="88ba2-203">Erweitern Sie den Knoten **NewEmployeeOrientationInstance** im **Projektmappen-Explorer**, sofern dies noch nicht geschehen ist, damit Sie die Datei „elements.xml“, die ein untergeordnetes Element der Liste *Instanz* ist, klar von der Datei „elements.xml“ unterscheiden können, die ein untergeordnetes Element der Liste *Vorlage* ist.</span><span class="sxs-lookup"><span data-stu-id="88ba2-203">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list *instance* from the elements.xml file that is a child of the list *template*.</span></span>
    
    <span data-ttu-id="88ba2-204">*Abbildung 4: Knoten „Listen“ im Projektmappen-Explorer*</span><span class="sxs-lookup"><span data-stu-id="88ba2-204">*Figure 4. Lists node in Solution Explorer*</span></span>

    ![Listenordner mit der untergeordneten Vorlage "NewEmployeeOrientation", die wiederum über drei untergeordnete Elemente verfügt: eine NewEmployeeOrientationInstance, die Datei "elements.xml" und die Datei "schema.xml". Die Instanz selbst ist ein untergeordnetes Element mit dem Namen "elements.xml".](../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)

10. <span data-ttu-id="88ba2-207">Öffnen Sie das untergeordnete Element „elements.xml“ der Listenvorlage **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-207">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>

11. <span data-ttu-id="88ba2-208">Fügen Sie in das Attribut **DisplayName** (nicht in das Attribut **Name**) Leerzeichen ein, damit es besser lesbar ist: „New Employee Orientation“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-208">Add spaces to the **DisplayName** attribute (not the **Name** attribute) to make it friendlier: "New Employee Orientation."</span></span>

12. <span data-ttu-id="88ba2-209">Tragen Sie als Wert für das Attribut **Description** die Zeichenfolge „Orientation information about new employees“ ein.</span><span class="sxs-lookup"><span data-stu-id="88ba2-209">Set the **Description** attribute to "Orientation information about new employees."</span></span>

13. <span data-ttu-id="88ba2-210">Übernehmen Sie für alle anderen Attribute jeweils den Standardwert, speichern Sie die Datei, und schließen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="88ba2-210">Leave all other attributes at their default, save the file, and close it.</span></span>

14. <span data-ttu-id="88ba2-211">Falls der Listen-Designer noch nicht geöffnet ist: Klicken Sie im **Projektmappen-Explorer** auf den Knoten **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-211">If the list designer is not open, select the **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>

15. <span data-ttu-id="88ba2-212">Öffnen Sie im Designer die Registerkarte **Liste**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-212">Open the **List** tab of the designer.</span></span> <span data-ttu-id="88ba2-213">Auf dieser Registerkarte werden bestimmte Werte der *Listeninstanz* festgelegt, nicht der *Listenvorlage*. Einige Standardwerte werden jedoch von der Vorlage vererbt.</span><span class="sxs-lookup"><span data-stu-id="88ba2-213">This tab is used to set certain values for the list *instance*, not the list *template*, but it has some default values that it inherited from the template.</span></span>

16. <span data-ttu-id="88ba2-214">Ändern Sie die Werte auf der Registerkarte **Liste** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="88ba2-214">Change the values on the **List** tab to the following:</span></span>
    
    -  <span data-ttu-id="88ba2-215">**Titel:** Neue Mitarbeiter in Seattle</span><span class="sxs-lookup"><span data-stu-id="88ba2-215">**Title**: New Employees in Seattle</span></span>
    -  <span data-ttu-id="88ba2-216">**Listen-URL:** Listen/NewEmployeesInSeattle</span><span class="sxs-lookup"><span data-stu-id="88ba2-216">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    -  <span data-ttu-id="88ba2-217">**Beschreibung:** Die neuen Mitarbeiter in Seattle</span><span class="sxs-lookup"><span data-stu-id="88ba2-217">**Description**: The new employees in Seattle</span></span>

17. <span data-ttu-id="88ba2-218">Übernehmen Sie den Standardstatus der Kontrollkästchen, speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="88ba2-218">Leave the check boxes at their default status, save the file, and then close the designer.</span></span>

18. <span data-ttu-id="88ba2-219">Im **Projektmappen-Explorer** wird möglicherweise noch der alte Name der Listeninstanz angezeigt.</span><span class="sxs-lookup"><span data-stu-id="88ba2-219">The list instance may have its old name in **Solution Explorer**.</span></span> <span data-ttu-id="88ba2-220">Sollte das der Fall sein: Öffnen Sie das Kontextmenü von **NewEmployeeOrientationInstance**, klicken Sie auf **Umbenennen**, und ändern Sie den Namen in **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-220">If so, open the shortcut menu for **NewEmployeeOrientationInstance**, select **Rename**, and change the name to **NewEmployeesInSeattle**.</span></span>

19. <span data-ttu-id="88ba2-221">Öffnen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-221">Open the schema.xml file.</span></span>

20. <span data-ttu-id="88ba2-222">Ersetzen Sie im Element des Typs **View** mit „0“ als Wert für **BaseViewID** das vorhandene Element des Typs **ViewFields** durch das unten aufgeführte Markup. (Verwenden Sie exakt diese GUID für das Element **FieldRef** mit dem Namen `Title`.)</span><span class="sxs-lookup"><span data-stu-id="88ba2-222">In the **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `Title`).</span></span> <span data-ttu-id="88ba2-223">Zeilenumbrüche können in der automatisch generierten Datei „schema.xml“ an ungewöhnlichen Stellen gesetzt sein.</span><span class="sxs-lookup"><span data-stu-id="88ba2-223">Line breaks may come at odd places in this autogenerated schema.xml file.</span></span> <span data-ttu-id="88ba2-224">Vergewissern Sie sich, dass Sie wirklich das Starttag und das Endtag des Elements **ViewFields** gefunden haben.</span><span class="sxs-lookup"><span data-stu-id="88ba2-224">Be sure you have found the matching begin and end tags for the **ViewFields** element.</span></span> <span data-ttu-id="88ba2-225">Fügen Sie Zeilenumbrüche ein, um den Code besser lesbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-225">Add line breaks to improve readability.</span></span> 

    ```
      <ViewFields>
         <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
      </ViewFields>
    ```

21. <span data-ttu-id="88ba2-226">Ersetzen Sie in der Datei „schema.xml“ im Element des Typs **View** mit „1“ als Wert für **BaseViewID** das vorhandene Element des Typs **ViewFields** durch das folgende Markup. (Verwenden Sie exakt diese GUID für das Element **FieldRef** mit dem Namen `LinkTitle`.)</span><span class="sxs-lookup"><span data-stu-id="88ba2-226">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `LinkTitle`).</span></span>
    
    ```
      <ViewFields>
         <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      </ViewFields>
    ```

22. <span data-ttu-id="88ba2-227">Speichern und schließen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-227">Save and close the schema.xml file.</span></span>

23. <span data-ttu-id="88ba2-228">Öffnen sie die Datei „elements.xml“, die ein untergeordnetes Element der *Listeninstanz* **NewEmployeesInSeattle** ist (nicht die Datei „elements.xml“, die ein untergeordnetes Element der *Listenvorlage* **NewEmployeeOrientation** ist).</span><span class="sxs-lookup"><span data-stu-id="88ba2-228">Open the elements.xml file that is a child of the list *instance* **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template* **NewEmployeeOrientation**).</span></span>

24. <span data-ttu-id="88ba2-p126">Füllen Sie in dieser Datei die Liste mit einigen Ausgangsdaten. Hierzu fügen Sie folgendes **Data**-Elementmarkup als untergeordnetes Element des **ListInstance**-Elements hinzu.</span><span class="sxs-lookup"><span data-stu-id="88ba2-p126">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
    ```
      <Data>
      <Rows>
        <Row>
          <Field Name="Title">Tom Higginbotham</Field>
        </Row>
        <Row>
          <Field Name="Title">Satomi Hayakawa</Field>
        </Row>
        <Row>
          <Field Name="Title">Cassi Hicks</Field>
        </Row>
        <Row>
          <Field Name="Title">Lertchai Treetawatchaiwong</Field>
        </Row>
      </Rows>
    </Data>
    ```

25. <span data-ttu-id="88ba2-231">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="88ba2-231">Save and close the file.</span></span>

26. <span data-ttu-id="88ba2-232">Doppelklicken Sie im **Projektmappen-Explorer** auf **Feature1**, um den Feature-Designer zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-232">In **Solution Explorer**, double-click **Feature1** to open the Feature designer.</span></span> <span data-ttu-id="88ba2-233">Legen Sie im Designer als **Titel** die Zeichenfolge **Orientierungskomponenten für neue Mitarbeiter** fest und als **Beschreibung** die Zeichenfolge **Listen und andere Komponenten, die zur Orientierung neuer Mitarbeiter im Unternehmen dienen**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-233">In the designer, set the **Title** to **New Employee Orientation Components** and set the **Description** to **Lists and other components for getting employees oriented to the company**.</span></span> <span data-ttu-id="88ba2-234">Speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="88ba2-234">Save the file, and then close the designer.</span></span>

27. <span data-ttu-id="88ba2-235">Falls **Feature1** im **Projektmappen-Explorer** nicht automatisch umbenannt wurde: Öffnen Sie das Kontextmenü des Elements, klicken Sie auf **Umbenennen**, und geben Sie ihm den Namen **NewEmployeeOrientationComponents**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-235">If the **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, select **Rename**, and rename it to **NewEmployeeOrientationComponents**.</span></span>

28. <span data-ttu-id="88ba2-236">Öffnen Sie die Datei „Default.aspx“.</span><span class="sxs-lookup"><span data-stu-id="88ba2-236">Open the Default.aspx file.</span></span>

29. <span data-ttu-id="88ba2-237">Suchen Sie das ASP.NET-Element des Typs **Content** mit der ID **PlaceHolderPageTitleInTitleArea**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-237">Find the ASP.NET **Content** element with the ID **PlaceHolderPageTitleInTitleArea**.</span></span> <span data-ttu-id="88ba2-238">Ersetzen Sie die Standardzeichenfolge **Page Title** durch **Neue Mitarbeiter nach Standort**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-238">Replace the default string **Page Title** with **New Employees by Location**.</span></span>

30. <span data-ttu-id="88ba2-239">Suchen Sie das ASP.NET-Element des Typs **Content** mit der ID **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="88ba2-239">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.</span></span> <span data-ttu-id="88ba2-240">*Ersetzen* Sie dessen Inhalt durch das unten aufgeführte Markup.</span><span class="sxs-lookup"><span data-stu-id="88ba2-240">*Replace* its contents with the following markup.</span></span> <span data-ttu-id="88ba2-241">`_spPageContextInfo` ist ein JavaScript-Objekt, das von SharePoint automatisch in die Seite integriert wird.</span><span class="sxs-lookup"><span data-stu-id="88ba2-241">The `_spPageContextInfo` is a JavaScript object that SharePoint automatically includes on the page.</span></span> <span data-ttu-id="88ba2-242">Die Eigenschaft `webAbsoluteUrl` dieses Objekts gibt die URL des Add-In-Webs zurück.</span><span class="sxs-lookup"><span data-stu-id="88ba2-242">It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
    ```XML
        <p><asp:HyperLink runat="server" 
        NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="New Employees in Seattle" /></p>
    ```

<span data-ttu-id="88ba2-243"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-243"></span></span>
## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="88ba2-244">Ausführen des Add-Ins und Testen der Liste</span><span class="sxs-lookup"><span data-stu-id="88ba2-244">Run the add-in and test the list</span></span>

1. <span data-ttu-id="88ba2-245">Drücken Sie die Taste F5, um das Add-In bereitzustellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-245">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="88ba2-246">Visual Studio installiert das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-246">Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="88ba2-247">(Weitere Informationen dazu, wie Endbenutzer ein installiertes SharePoint-Add-In ausführen können, finden Sie unter [Nächste Schritte](#Nextsteps)).</span><span class="sxs-lookup"><span data-stu-id="88ba2-247">(To find out how end users run an installed SharePoint Add-in, see [Next Steps](#Nextsteps).)</span></span>

2. <span data-ttu-id="88ba2-248">Die Standardseite des Add-Ins wird geöffnet. Klicken Sie auf **Neue Mitarbeiter in Seattle**, um die Instanz der benutzerdefinierten Liste zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="88ba2-248">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>
    
    <span data-ttu-id="88ba2-249">*Abbildung 5: Standardseite und die Seite mit der Listenansicht*</span><span class="sxs-lookup"><span data-stu-id="88ba2-249">*Figure 5. Default page and list view page*</span></span>

    ![Die Standardseite des Add-Ins mit dem Titel "Neue Mitarbeiter nach Standort" wird angezeigt. Es gibt einen Link mit der Bezeichnung "Neue Mitarbeiter in Seattle". Ein Pfeil von diesem Link zeigt auf die Listenansichtsseite für die Liste. Diese hat den Titel "Neue Mitarbeiter in Seattle" und weist die folgende Liste auf.](../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)

3. <span data-ttu-id="88ba2-254">Fügen Sie der Liste Elemente hinzu, und löschen Sie Elemente aus der Liste.</span><span class="sxs-lookup"><span data-stu-id="88ba2-254">Add and delete items from the list.</span></span>

4. <span data-ttu-id="88ba2-p132">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="88ba2-p132">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="88ba2-257">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung auch in anderen Artikeln arbeiten werden, empfiehlt es sich, das Add-In ein letztes Mal zurückzuziehen, sobald Sie eine Weile nicht mehr an ihm arbeiten werden.</span><span class="sxs-lookup"><span data-stu-id="88ba2-257">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are finished working with it for a while.</span></span> <span data-ttu-id="88ba2-258">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="88ba2-258">Right-click the project in **Solution Explorer**, and select **Retract**.</span></span>

<span data-ttu-id="88ba2-259"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="88ba2-259"></span></span>
## <a name="next-steps"></a><span data-ttu-id="88ba2-260">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="88ba2-260">Next steps</span></span>

<span data-ttu-id="88ba2-261">Um Ihre Add-Ins zu erstellen, führen Sie die folgenden Schritte in der folgenden Reihenfolge aus:</span><span class="sxs-lookup"><span data-stu-id="88ba2-261">To create your add-ins, walk through the following steps in this order:</span></span>

1.  [<span data-ttu-id="88ba2-262">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="88ba2-262">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
2.  [<span data-ttu-id="88ba2-263">Hinzufügen von Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="88ba2-263">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
3.  [<span data-ttu-id="88ba2-264">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="88ba2-264">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
4.  [<span data-ttu-id="88ba2-265">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="88ba2-265">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
5.  [<span data-ttu-id="88ba2-266">Hinzufügen eines Workflows zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="88ba2-266">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
6.  [<span data-ttu-id="88ba2-267">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="88ba2-267">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
7.  [<span data-ttu-id="88ba2-268">Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint-gehostetes SharePoint Add-In</span><span class="sxs-lookup"><span data-stu-id="88ba2-268">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
8.  [<span data-ttu-id="88ba2-269">Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="88ba2-269">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
9.  [<span data-ttu-id="88ba2-270">Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten</span><span class="sxs-lookup"><span data-stu-id="88ba2-270">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md)
10. [<span data-ttu-id="88ba2-271">Arbeiten mit Hostwebdaten aus JavaScript im Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="88ba2-271">Work with host web data from JavaScript in the add-in web</span></span>](work-with-host-web-data-from-javascript-in-the-add-in-web.md)


