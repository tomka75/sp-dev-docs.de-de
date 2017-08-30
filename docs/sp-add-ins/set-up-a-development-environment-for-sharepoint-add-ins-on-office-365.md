# <a name="set-up-a-development-environment-for-sharepoint-add-ins-on-office-365"></a><span data-ttu-id="470a2-101">Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365</span><span class="sxs-lookup"><span data-stu-id="470a2-101">Set up a development environment for SharePoint Add-ins on Office 365</span></span>
<span data-ttu-id="470a2-102">Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins auf einer Office 365-Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="470a2-102">Set up a development environment for SharePoint Add-ins on an Office 365 Developer Site.</span></span>
 

 <span data-ttu-id="470a2-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="470a2-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="470a2-p102">Lesen Sie [Tools und Umgebungen für die Entwicklung von Add-Ins für SharePoint](tools-and-environments-for-developing-sharepoint-add-ins), um Ihre Optionen zu verstehen, bevor Sie die Verfahren in diesem Artikel ausführen. Sie finden weitere Informationen unter  [SharePoint-Add-Ins](sharepoint-add-ins), wenn Sie nicht sicher sind, welche Arten von SharePoint-Add-Ins Sie erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="470a2-p102">Set up a development environment for SharePoint Add-ins on an Office 365 Developer Site. Please read  [Tools and environments for developing SharePoint Add-ins](tools-and-environments-for-developing-sharepoint-add-ins) to get an understanding of your options before you carry out any procedures in this article. See [SharePoint Add-ins](sharepoint-add-ins) if you are not sure what kinds of SharePoint Add-ins you want to create.</span></span>
 

## <a name="install-visual-studio-and-tools-on-your-computer"></a><span data-ttu-id="470a2-108">Installieren von Visual Studio und Tools auf Ihrem Computer</span><span class="sxs-lookup"><span data-stu-id="470a2-108">Install Visual Studio and tools on your computer</span></span>
<span data-ttu-id="470a2-109"><a name="devenv_vs"> </a></span><span class="sxs-lookup"><span data-stu-id="470a2-109"></span></span>


- <span data-ttu-id="470a2-p103">Wenn Sie **Visual Studio** 2013 oder höher noch nicht installiert haben, installieren Sie es mithilfe der Anweisungen unter [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Wir empfehlen die Verwendung der [aktuellsten Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="470a2-p103">If you don't already have **Visual Studio** 2013 or later installed, install it with the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="470a2-p104">Visual Studio umfasst **Microsoft Office Developer Tools für Visual Studio**, es gibt jedoch auch Fälle, in denen eine Version der Tools zwischen den Updates von Visual Studio veröffentlicht wird. Um sicherzustellen, dass Sie die aktuellste Version der Tools verwenden, führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus.</span><span class="sxs-lookup"><span data-stu-id="470a2-p104">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**, but sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools use run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 
    
 

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="470a2-114">Ausführliche Protokollierung in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="470a2-114">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="470a2-115">Führen Sie die folgenden Schritte aus, wenn Sie die ausführliche Protokollierung aktivieren möchten:</span><span class="sxs-lookup"><span data-stu-id="470a2-115">Follow these steps if you want to turn on verbose logging:</span></span>
 

 

1. <span data-ttu-id="470a2-116">Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, wobei _nn.n_ die Version von Visual Studio ist, z. B. 12.0 oder 14.0.</span><span class="sxs-lookup"><span data-stu-id="470a2-116">Open the registry, and navigate to HKEY_CURRENT_USERSoftwareMicrosoft**VisualStudio_nn.n_SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>
    
 
2. <span data-ttu-id="470a2-117">Fügen Sie einen DWORD-Schlüssel mit dem Namen **EnableDiagnostics** hinzu.</span><span class="sxs-lookup"><span data-stu-id="470a2-117">Add a DWORD key named **EnableDiagnostics**.</span></span>
    
 
3. <span data-ttu-id="470a2-118">Geben Sie dem Schlüssel den Wert **1**.</span><span class="sxs-lookup"><span data-stu-id="470a2-118">Give the key the value **1**.</span></span>
    
 
<span data-ttu-id="470a2-119">Der Registrierungspfad wird sich in kommenden Versionen von Visual Studio ändern.</span><span class="sxs-lookup"><span data-stu-id="470a2-119">The registry path will change in future versions of Visual Studio.</span></span>
 

 

## <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="470a2-120">Registrieren für eine Office 365-Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="470a2-120">Sign up for an Office 365 Developer Site</span></span>
<span data-ttu-id="470a2-121"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="470a2-121"></span></span>


 <span data-ttu-id="470a2-p105">**Hinweis** Sie haben möglicherweise bereits Zugriff auf eine Office 365-Entwicklerwebsite: **Sind Sie MSDN-Abonnent?** Visual Studio Enterprise mit MSDN-Abonnenten erhalten ein Office 365-Entwicklerabonnement als Vorteil. [Lösen Sie Ihren Vorteil noch heute ein. ](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Haben Sie einen der folgenden Office 365-Abonnementpläne?** **Wenn ja, kann ein Administrator des Office 365-Abonnements eine Entwicklerwebsite erstellen**, und zwar im [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx). Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="470a2-p105">**Note**   You might already have access to an Office 365 Developer Site: **Are you an MSDN subscriber?** Visual Studio Enterprise with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more information, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription).</span></span> 
 

<span data-ttu-id="470a2-128">Es gibt drei Wege, um einen Office 365-Plan zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="470a2-128">Three ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="470a2-p106">Registrieren Sie sich über das Office 365-Entwicklerprogramm für ein kostenloses einjähriges Office 365-Entwicklerkonto.  [Informieren Sie sich ausführlicher](http://dev.office.com/devprogram), oder wechseln Sie direkt zum  [Registrierungsformular](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). Nach der Registrierung für das Entwicklerprogramm erhalten Sie eine E-Mail mit einem Link, über den Sie sich für das Entwicklerkonto registrieren können. Beachten Sie die nachstehenden Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="470a2-p106">Sign up for a free, one year Office 365 developer account through the Office 365 Developer Program.  [Get more information](http://dev.office.com/devprogram), or go straight to  [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). You'll get an e-mail after you sign up for the developer program with a link to sign up for the developer account. Use the instructions below.</span></span>
    
 
- <span data-ttu-id="470a2-133">Beginnen Sie mit einer [kostenlosen 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) mit einer Benutzerlizenz.</span><span class="sxs-lookup"><span data-stu-id="470a2-133">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="470a2-134">Erwerben Sie ein [Office 365 Developer-Abonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="470a2-134">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="470a2-135">**Tipp** Öffnen Sie diese Links in einem anderen Fenster oder einer anderen Registerkarte, damit die nachfolgenden Anweisungen übersichtlich bleiben.</span><span class="sxs-lookup"><span data-stu-id="470a2-135">**TIP** Open these links in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="470a2-136">**Abb. 1. Domänenname der Office 365-Entwicklerwebsite**</span><span class="sxs-lookup"><span data-stu-id="470a2-136">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Seite 2 des Registrierungsformulars für das Office 365-Konto](../../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="470a2-p107">Die erste Seite (nicht abgebildet) des Registrierungsformulars ist selbsterklärend. Geben Sie einfach die erforderlichen Informationen zu Ihrer Person an, und wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="470a2-p107">The first page (not shown) of the signup form is self-explanatory. Just supply the information about yourself that is requested and choose **Next**.</span></span>
    
 
2. <span data-ttu-id="470a2-140">Geben Sie auf der zweiten Seite, die in Abbildung 1 gezeigt ist, eine Benutzer-ID für den Administrator des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="470a2-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="470a2-141">Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="470a2-141">Create a subdomain of **.onmicrosoft.com**.</span></span> 
    
    <span data-ttu-id="470a2-p108">Nach der Registrierung müssen Sie die resultierenden Anmeldeinformationen (im Format _UserID_@ _IhreDomäne_.onmicrosoft.com) benutzen, um sich auf Ihrer Office 365-Portalwebsite anzumelden, auf der Sie Ihr Konto verwalten. Ihre SharePoint Online-Entwicklerwebsite wird unter Ihrer neuen Domäne **http:// _IhreDomäne_.sharepoint.com** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="470a2-p108">After signup, you have to use the resulting credentials (in the format  _UserID_@ _yourdomain_.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is provisioned at your new domain: **http:// _yourdomain_.sharepoint.com**.</span></span>
    
 
4. <span data-ttu-id="470a2-p109">Wählen Sie **Weiter** aus, und füllen Sie die letzte Seite des Formulars aus. Wenn Sie eine Telefonnummer bereitstellen, um Ihren Bestätigungscode zu erhalten, können Sie eine Mobil- oder Festnetznummer, aber *keine* VoIP-Nummer (Voice over Internet Protocol) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="470a2-p109">Choose **Next** and fill out the final page of the form. If you choose to provide a telephone number to obtain a confirmation code, you can provide a mobile or land line telephone number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="470a2-p110">**Hinweis** Wenn Sie beim Versuch, sich bei einem Entwicklerkonto anzumelden, bei einem anderen Microsoft-Konto angemeldet sind, wird möglicherweise die folgende Nachricht angezeigt: „Die eingegebene Benutzer-ID hat leider nicht funktioniert. Sie ist anscheinend nicht gültig. Geben Sie die Benutzer-ID ein, die Ihnen von Ihrem Unternehmen zugewiesen wurde. Ihre Benutzer-ID hat in der Regel das Format *someone@example.com* oder *someone@example.onmicrosoft.com*.“ Wenn diese Meldung angezeigt wird, melden Sie sich von dem Microsoft-Konto ab, das Sie verwendet haben, und versuchen Sie es erneut. Wenn Sie weiterhin die Meldung erhalten, löschen Sie den Browsercache, oder wechseln Sie zu **InPrivate-Browsen**, und füllen Sie dann das Formular aus.</span><span class="sxs-lookup"><span data-stu-id="470a2-p110">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might get this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="470a2-p111">Nachdem Sie die Registrierung abgeschlossen haben, wird in Ihrem Browser die Office 365-Installationsseite geöffnet. Wählen Sie das Admin-Symbol aus, um die Admin Center-Seite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="470a2-p111">After you finish the signup process, your browser will opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="470a2-153">**Abb. 2. Office 365 Admin Center-Seite**</span><span class="sxs-lookup"><span data-stu-id="470a2-153">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Screenshot mit dem Office 365 Admin Center](../../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="470a2-p112">Warten Sie, bis der Bereitstellungsprozess für Ihre Entwicklerwebsite abgeschlossen ist. Nach Abschluss der Bereitstellung aktualisieren Sie die Admin Center-Seite im Browser.</span><span class="sxs-lookup"><span data-stu-id="470a2-p112">You'll have to wait for your Developer Site to finish provisioning. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="470a2-p113">Wählen Sie dann links oben den Link **Add-Ins erstellen** aus, um Ihre Website für Entwickler zu öffnen. Sie sollten eine Website wie in Abbildung 3 dargestellt sehen. Auf der Seite wird die Liste **Add-Ins im Test** angezeigt. Damit wird bestätigt, dass die Website mit der Entwicklerwebsitevorlage von SharePoint erstellt wurde. Wird stattdessen eine Teamwebsite angezeigt, warten Sie einige Minuten und starten dann Ihre Website erneut.</span><span class="sxs-lookup"><span data-stu-id="470a2-p113">Then, choose the **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. There is an **Add-ins in Testing** list on the page. This confirms that the website was made with SharePoint's Developer Site template. If you see a regular team site instead, wait a few minutes and launch your site again.</span></span>
    
 
3. <span data-ttu-id="470a2-p114">Notieren Sie die URL der Website. Diese wird verwendet, wenn Sie SharePoint-Add-Ins-Projekte in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="470a2-p114">Make a note of the URL of the site. It is used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="470a2-164">**Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test**</span><span class="sxs-lookup"><span data-stu-id="470a2-164">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Screenshot, auf dem die Entwicklerwebsite-Startseite angezeigt ist](../../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="470a2-166">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="470a2-166">Additional resources</span></span>
<span data-ttu-id="470a2-167"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="470a2-167"></span></span>


-  [<span data-ttu-id="470a2-168">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="470a2-168">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="470a2-169">Erste Schritte beim Erstellen von Anbieter-gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="470a2-169">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="470a2-170">Erste Schritte beim Erstellen von SharePoint-gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="470a2-170">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

 

 

