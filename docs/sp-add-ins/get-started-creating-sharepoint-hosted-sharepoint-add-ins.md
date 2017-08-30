# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="996fc-101">Erste Schritte beim Erstellen von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="996fc-101">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>
<span data-ttu-id="996fc-102">Einrichten einer Entwicklungsumgebung und Erstellen Ihres ersten von SharePoint gehosteten SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="996fc-102">Set up a development environment and create your first SharePoint-hosted spappsing.</span></span>
 

 <span data-ttu-id="996fc-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="996fc-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="996fc-p102">Von SharePoint gehostete Add-Ins sind eine der zwei Haupttypen von SharePoint-Add-Ins. Einen schnellen Überblick über SharePoint-Add-Ins und die zwei verschiedenen Typen finden Sie unter [SharePoint Add-Ins](sharepoint-add-ins). Hier ist eine Zusammenfassung zu von SharePoint gehosteten Add-Ins:</span><span class="sxs-lookup"><span data-stu-id="996fc-p102">Set up a development environment and create your first SharePoint-hosted SharePoint Add-in. SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see  [SharePoint Add-ins](sharepoint-add-ins). Here's a summary of SharePoint-hosted add-ins:</span></span>
 

- <span data-ttu-id="996fc-109">Sie enthalten SharePoint-Listen, Webparts, Workflows, benutzerdefinierte Seiten und andere Komponenten, die auf einer Unterwebsite mit der Bezeichnung Add-In-Web der SharePoint-Website installiert sind, wo das Add-In installiert ist.</span><span class="sxs-lookup"><span data-stu-id="996fc-109">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>
    
 
- <span data-ttu-id="996fc-110">Der einzige verfügbare Code ist JavaScript auf benutzerdefinierten SharePoint-Seiten.</span><span class="sxs-lookup"><span data-stu-id="996fc-110">The only code they have is JavaScript on custom SharePoint pages.</span></span>
    
 
- [<span data-ttu-id="996fc-111">Schritt 1: Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="996fc-111">Step 1 Set up your dev environment</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Setup) 

- [<span data-ttu-id="996fc-112">Schritt 2: Erstellen des App-Projekts</span><span class="sxs-lookup"><span data-stu-id="996fc-112">Step 2 Create the app project</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Create) 

- [<span data-ttu-id="996fc-113">Schritt 3: Codieren Ihrer App</span><span class="sxs-lookup"><span data-stu-id="996fc-113">Step 3 Code your app</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Code)
 

## <a name="set-up-your-dev-environment"></a><span data-ttu-id="996fc-114">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="996fc-114">Set up your dev environment</span></span>
<span data-ttu-id="996fc-115"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-115"></span></span>

<span data-ttu-id="996fc-p103">Es gibt verschiedene Möglichkeiten zum Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins. In diesem Abschnitt wird die einfachste Möglichkeit erläutert. Alternativen finden Sie unter  [Zusätzliche Ressourcen](#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="996fc-p103">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way. For alternatives, see  [Additional Resources](#bk_addresources).</span></span>
 

 

### <a name="get-the-tools"></a><span data-ttu-id="996fc-119">Abrufen der Tools</span><span class="sxs-lookup"><span data-stu-id="996fc-119">Get the tools</span></span>


- <span data-ttu-id="996fc-p104">Wenn Sie **Visual Studio** 2013 oder höher noch nicht installiert haben, installieren Sie es mit den Anweisungen unter [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Wir empfehlen die Verwendung der  [neuesten Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="996fc-p104">If you don't already have **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="996fc-p105">Visual Studio enthält die **Microsoft Office-Entwicklertools für Visual Studio**, aber manchmal wird eine Version der Tools zwischen Updates von Visual Studio veröffentlicht. Um sicherzustellen, dass Sie die neueste Version der Tools verwenden, führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-p105">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**. Sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 
    
 

### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="996fc-125">Registrieren für eine Office 365-Entwicklerwebsite</span><span class="sxs-lookup"><span data-stu-id="996fc-125">Sign up for an Office 365 Developer Site</span></span>
<span data-ttu-id="996fc-126"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-126"></span></span>


 <span data-ttu-id="996fc-p106">**Hinweis** Sie haben möglicherweise bereits Zugriff auf eine Office 365-Entwicklerwebsite: **Sind Sie MSDN-Abonnent?** Visual Studio Ultimate und Visual Studio Premium mit MSDN-Abonnenten erhalten ein Office 365-Entwicklerabonnement als Vorteil. [Lösen Sie Ihren Vorteil noch heute ein. ](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Haben Sie einen der folgenden Office 365-Abonnementpläne?** **Wenn ja, kann ein Administrator des Office 365-Abonnements eine Entwicklerwebsite erstellen**, und zwar im [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx). Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="996fc-p106">**Note**   You might already have access to an Office 365 Developer Site. **Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more info, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription).</span></span> 
 

<span data-ttu-id="996fc-134">Es gibt drei Wege, um einen Office 365-Plan zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="996fc-134">There are three ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="996fc-p107">Registrieren Sie sich über das Office 365-Entwicklerprogramm für ein kostenloses einjähriges Office 365-Entwicklerkonto.  [Informieren Sie sich ausführlicher](http://dev.office.com/devprogram), oder wechseln Sie direkt zum  [Registrierungsformular](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). Nach der Registrierung für das Entwicklerprogramm erhalten Sie eine E-Mail mit einem Link, über den Sie sich für das Entwicklerkonto registrieren können. Beachten Sie die nachstehenden Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="996fc-p107">Sign up for a free, one year Office 365 developer account through the Office 365 Developer Program.  [Get more information](http://dev.office.com/devprogram), or go straight to  [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). You'll get an e-mail after you sign up for the developer program with a link to sign up for the developer account. Use the instructions below.</span></span>
    
 
- <span data-ttu-id="996fc-139">Beginnen Sie mit einer [kostenlosen 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) mit einer Benutzerlizenz.</span><span class="sxs-lookup"><span data-stu-id="996fc-139">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="996fc-140">Erwerben Sie ein [Office 365 Developer-Abonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="996fc-140">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="996fc-141">**Tipp** Öffnen Sie diese Links in einem anderen Fenster oder einer anderen Registerkarte, damit die nachfolgenden Anweisungen übersichtlich bleiben.</span><span class="sxs-lookup"><span data-stu-id="996fc-141">**TIP** Open these links in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="996fc-142">**Abb. 1. Domänenname der Office 365-Entwicklerwebsite**</span><span class="sxs-lookup"><span data-stu-id="996fc-142">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Seite 2 des Registrierungsformulars für das Office 365-Konto](../../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="996fc-144">Die erste Seite (nicht abgebildet) des Registrierungsformulars ist selbsterklärend. Geben Sie einfach die erforderlichen Informationen zu Ihrer Person an, und wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-144">The first page (not shown) of the signup form is self-explanatory; supply the requested information and then choose **Next**.</span></span>
    
 
2. <span data-ttu-id="996fc-145">Geben Sie auf der zweiten Seite, die in Abbildung 1 gezeigt ist, eine Benutzer-ID für den Administrator des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="996fc-145">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="996fc-146">Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**, zum Beispiel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="996fc-146">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
    <span data-ttu-id="996fc-p108">Nach der Registrierung müssen Sie die resultierenden Anmeldeinformationen (im Format  _UserID_@ _IhreDomäne_.onmicrosoft.com) benutzen, um sich auf Ihrer Office 365-Portalwebsite anzumelden, auf der Sie Ihr Konto verwalten. Ihre SharePoint Online-Entwicklerwebsite wird unter Ihrer neuen Domäne **http:// _IhreDomäne_.sharepoint.com** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="996fc-p108">After signup, you use the resulting credentials (in the format  _UserID_@ _yourdomain_.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is set up at your new domain: **http:// _yourdomain_.sharepoint.com**.</span></span>
    
 
4. <span data-ttu-id="996fc-p109">Wählen Sie **Weiter** aus, und füllen Sie die letzte Seite des Formulars aus. Wenn Sie eine Telefonnummer bereitstellen, um Ihren Bestätigungscode zu erhalten, können Sie eine Mobil- oder Festnetznummer, aber *keine*  VoIP-Nummer (Voice over Internet Protocol) benutzen.</span><span class="sxs-lookup"><span data-stu-id="996fc-p109">Choose **Next** and fill out the final page of the form. If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="996fc-p110">**Hinweis** Wenn Sie beim Versuch, sich bei einem Entwicklerkonto anzumelden, bei einem anderen Microsoft-Konto angemeldet sind, wird möglicherweise die folgende Nachricht angezeigt: „Die eingegebene Benutzer-ID hat leider nicht funktioniert. Sie ist anscheinend nicht gültig. Geben Sie die Benutzer-ID ein, die Ihnen von Ihrem Unternehmen zugewiesen wurde. Ihre Benutzer-ID hat in der Regel das Format *someone@example.com* oder *someone@example.onmicrosoft.com*.“ Wenn diese Meldung angezeigt wird, melden Sie sich von dem Microsoft-Konto ab, das Sie verwendet haben, und versuchen Sie es erneut. Wenn Sie weiterhin die Meldung erhalten, löschen Sie den Browsercache, oder wechseln Sie zu **InPrivate-Browsen**, und füllen Sie dann das Formular aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-p110">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see that message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="996fc-p111">Nachdem Sie die Registrierung abgeschlossen haben, wird in Ihrem Browser die Office 365-Installationsseite geöffnet. Wählen Sie das Admin-Symbol aus, um die Admin Center-Seite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="996fc-p111">After you finish the signup process, your browser opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="996fc-158">**Abb. 2. Office 365 Admin Center-Seite**</span><span class="sxs-lookup"><span data-stu-id="996fc-158">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Screenshot mit dem Office 365 Admin Center](../../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="996fc-p112">Warten Sie, bis der Einrichtungsprozess für Ihre Entwicklerwebsite abgeschlossen ist. Nach Abschluss der Bereitstellung aktualisieren Sie die Admin Center-Seite im Browser.</span><span class="sxs-lookup"><span data-stu-id="996fc-p112">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="996fc-p113">Wählen Sie dann links oben den Link **Add-Ins erstellen** aus, um Ihre Website für Entwickler zu öffnen. Sie sollten eine Website wie in Abbildung 3 dargestellt sehen. Mit der Liste **Add-Ins im Test** auf der Seite wird bestätigt, dass die Website mit der Entwicklerwebsitevorlage von SharePoint erstellt wurde. Wird stattdessen eine Teamwebsite angezeigt, warten Sie einige Minuten und starten dann Ihre Website erneut.</span><span class="sxs-lookup"><span data-stu-id="996fc-p113">Then, choose the **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template. If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>
    
 
3. <span data-ttu-id="996fc-166">Notieren Sie die URL der Website. Diese wird verwendet, wenn Sie SharePoint-Add-Ins-Projekte in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="996fc-166">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="996fc-167">**Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test**</span><span class="sxs-lookup"><span data-stu-id="996fc-167">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Screenshot, auf dem die Entwicklerwebsite-Startseite angezeigt ist](../../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="create-the-add-in-project"></a><span data-ttu-id="996fc-169">Erstellen des Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="996fc-169">Create the add-in project</span></span>
<span data-ttu-id="996fc-170"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-170"></span></span>


1. <span data-ttu-id="996fc-171">Starten Sie Visual Studio mit der Option **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="996fc-171">Start Visual Studio using the **Run as administrator** option.</span></span>
    
 
2. <span data-ttu-id="996fc-172">Wählen Sie **Datei** > **Neu** > **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="996fc-172">Choose **File** > **New** > **New Project**.</span></span>
    
 
3. <span data-ttu-id="996fc-173">Erweitern Sie im Dialogfeld **Neues Projekt** den Knoten **Visual C#**, dann den Knoten **Office/SharePoint**, und wählen Sie den Knoten **Add-Ins** > **Add-In für SharePoint** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-173">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose **Add-ins** > **Add-in for SharePoint**.</span></span>
    
 
4. <span data-ttu-id="996fc-174">Nennen Sie das Projekt EmployeeOrientation, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="996fc-174">Name the project EmployeeOrientation, and then choose **OK**.</span></span>
    
 
5. <span data-ttu-id="996fc-p114">Stellen Sie im ersten Dialogfeld **Add-In für SharePoint-Einstellungen angeben** die vollständige URL der SharePoint-Website bereit, die Sie verwenden möchten, um das Add-In zu debuggen. Dabei handelt es sich um die URL der Website für Entwickler. (Verwenden Sie HTTPS und nicht HTTP in der URL). Wählen Sie unter **Wie soll Ihr Add-In für SharePoint gehostet werden** die Option **Von SharePoint gehostet** aus. Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-p114">In the first **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in. This is the URL of the Developer Site. (Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, choose **SharePoint-hosted**. Choose **Finish**.</span></span>
    
 
6. <span data-ttu-id="996fc-p115">Sie werden möglicherweise aufgefordert, sich bei Ihrer Entwicklerwebsite anzumelden. Wenn dies der Fall ist, verwenden Sie die Administratoranmeldeinformationen des entsprechenden Abonnements.</span><span class="sxs-lookup"><span data-stu-id="996fc-p115">You may be prompted to login to your Developer Site. If so, use your subscription administrator's credentials.</span></span>
    
 
7. <span data-ttu-id="996fc-p116">Nachdem das Projekt erstellt wurde, öffnen Sie die Datei **/Pages/Default.aspx** aus dem Stammverzeichnis des Projekts. Unter anderem lädt diese generierte Datei eines oder beide der zwei Skripts, die auf SharePoint: sp.runtime.js und sp.js gehostet werden. Das Markup zum Laden dieser Dateien befindet sich im **Content**-Steuerelement im oberen Bereich der Datei mit der ID **PlaceHolderAdditionalPageHead**. Das Markup variiert in Abhängigkeit von der **Microsoft Office-Entwicklertools für Visual Studio -Version**, die Sie verwenden. Diese Reihe von Lernprogrammen erfordert, dass beide Dateien geladen werden und sie mit normalen HTML**\<Script\>**-Tags und nicht mit **\<SharePoint:ScriptLink\>**-Tags geladen werden. Stellen Sie sicher, dass die folgenden Zeilen im **PlaceHolderAdditionalPageHead**-Steuerelement * über * der Zeile `<meta name="WebPartPageExpansion" content="full" />` enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="996fc-p116">After the project is created, open the file /Pages/Default.aspx from the root of the project. Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js. The markup for loading these files is in the Content control near the top of the file that has the ID PlaceHolderAdditionalPageHead. The markup varies depending on the version of Microsoft Office Developer Tools for Visual Studio that you are using. This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML    tags, not <SharePoint:ScriptLink> tags. Ensure that the following lines are in the PlaceHolderAdditionalPageHead control, just above  the line :</span></span>
    
```
  <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
  <script type="text/javascript" src="/_layouts/15/sp.js"></script> 

```


<span data-ttu-id="996fc-p117">Durchsuchen Sie anschließend die Datei nach einem anderen Markup, das auch eine oder die andere dieser Dateien lädt, und entfernen Sie das redundante Markup. Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="996fc-p117">Then search the file for any other markup that also loads one or the other of these files and remove the redundant markup. Save and close the file.</span></span>
    
 

## <a name="code-your-add-in"></a><span data-ttu-id="996fc-189">Codieren Ihres Add-Ins</span><span class="sxs-lookup"><span data-stu-id="996fc-189">Code your add-in</span></span>
<span data-ttu-id="996fc-190"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-190"></span></span>

<span data-ttu-id="996fc-191">Für das erste von SharePoint gehostete SharePoint-Add-In ist die klassische SharePoint-Erweiterung enthalten: eine benutzerdefinierte Liste und Listeninstanz.</span><span class="sxs-lookup"><span data-stu-id="996fc-191">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>
 

 

1. <span data-ttu-id="996fc-192">Öffnen Sie im **Projektmappen-Explorer** die Datei „AppManifest.xml".</span><span class="sxs-lookup"><span data-stu-id="996fc-192">In **Solution Explorer**, open the AppManifest.xml file.</span></span>
    
 
2. <span data-ttu-id="996fc-p118">Fügen Sie beim Öffnen des Manifest-Designers ein Leerzeichen zwischen den Wörtern im Feld **Title** hinzu, sodass dortEmployee Orientation steht. (Ändern Sie das Feld **Name***nicht*  .)</span><span class="sxs-lookup"><span data-stu-id="996fc-p118">When the manifest designer opens, add a space between the words in the **Title** field so that it readsEmployee Orientation. (Do  *not*  change the **Name** field.)</span></span>
    
 
3. <span data-ttu-id="996fc-195">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="996fc-195">Save and close the file.</span></span>
    
 
4. <span data-ttu-id="996fc-p119">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** > **Neuer Ordner** aus. Nennen Sie den OrdnerListen.</span><span class="sxs-lookup"><span data-stu-id="996fc-p119">Right-click the project in **Solution Explorer** and choose **Add** > **New Folder**. Name the folder Lists.</span></span>
    
 
5. <span data-ttu-id="996fc-p120">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Hinzufügen** > **Neues Element** aus. Das Dialogfeld **Neues Element hinzufügen** wird mit dem Knoten **Office/SharePoint** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="996fc-p120">Right-click the new folder and choose **Add** > **New Item**. The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
6. <span data-ttu-id="996fc-p121">Wählen Sie **Liste** aus. Geben Sie ihr den NamenNewEmployeeOrientation, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-p121">Choose **List**. Give it the name NewEmployeeOrientation, and then choose **Add**.</span></span> 
    
 
7. <span data-ttu-id="996fc-p122">Lassen Sie auf der Seite **Listeneinstellungen auswählen** im **Assistenten zum Anpassen von SharePoint** den Listenanzeigenamen auf dem Standardwert **NewEmployeeOrientation**, wählen Sie das Optionsfeld **Anpassbare Listenvorlage und Listeninstanz erstellen** und anschließend **Standard (benutzerdefinierte Liste)** in der Dropdownliste aus. Klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="996fc-p122">On the **Choose List Settings** page of the **SharePoint Customization Wizard**, leave the list display name at the default **NewEmployeeOrientation**, choose the **Create a customizable list template and a list instance of it** option button, and choose **Default (Custom List)** on the drop-down list. Then choose **Finish**.</span></span>
    
 
8. <span data-ttu-id="996fc-p123">Der Assistent erstellt eine **NewEmployeeOrientation**-Listenvorlage mit einer untergeordneten Listeninstanz mit der Bezeichnung **NewEmployeeOrientationInstance**. Möglicherweise wird ein Listen-Designer geöffnet. Dieser wird in einem späteren Schritt verwendet.</span><span class="sxs-lookup"><span data-stu-id="996fc-p123">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>
    
 
9. <span data-ttu-id="996fc-207">Erweitern Sie den Knoten **NewEmployeeOrientationInstance** im **Projektmappen-Explorer**, sofern dies noch nicht geschehen ist, damit Sie die Datei „elements.xml", die ein untergeordnetes Element der Liste  *Instanz*  ist, klar von der Datei „elements.xml" unterscheiden können, die ein untergeordnetes Element der Liste *Vorlage*  ist.</span><span class="sxs-lookup"><span data-stu-id="996fc-207">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list  *instance*  from the elements.xml file that is a child of the list *template*  .</span></span>
    
    <span data-ttu-id="996fc-208">**Listenknoten im Projektmappen-Explorer**</span><span class="sxs-lookup"><span data-stu-id="996fc-208">**Lists node in Solution Explorer**</span></span>

 

  ![Listenordner mit der untergeordneten Vorlage "NewEmployeeOrientation", die wiederum über drei untergeordnete Elemente verfügt: eine NewEmployeeOrientationInstance, die Datei "elements.xml" und die Datei "schema.xml". Die Instanz selbst ist ein untergeordnetes Element mit dem Namen "elements.xml".](../../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)
 

    
    
 
10. <span data-ttu-id="996fc-211">Öffnen Sie das untergeordnete Element „elements.xml" der Listenvorlage **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="996fc-211">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>
    
 
11. <span data-ttu-id="996fc-212">Fügen Sie dem Attribut **DisplayName** (nicht dem Attribut **Name**) Leerzeichen hinzu, damit es besser aussieht: „New Employee Orientation".</span><span class="sxs-lookup"><span data-stu-id="996fc-212">Add spaces to the **DisplayName** attribute (not the **Name** attribute) to make it friendlier:"New Employee Orientation".</span></span>
    
 
12. <span data-ttu-id="996fc-213">Legen Sie das Attribut **Description** auf„Orientation information about new employees." fest.</span><span class="sxs-lookup"><span data-stu-id="996fc-213">Set the **Description** attribute to"Orientation information about new employees."</span></span>
    
 
13. <span data-ttu-id="996fc-214">Lassen Sie alle anderen Attribute auf dem Standardwert, speichern Sie die Datei und schließen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="996fc-214">Leave all other attributes at their default, save the file and close it.</span></span>
    
 
14. <span data-ttu-id="996fc-215">Wenn der Listen-Designer nicht geöffnet wurde, wählen Sie den Knoten **NewEmployeeOrientation** im **Projektmappen-Explorer** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-215">If the list designer is not open, choose the **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>
    
 
15. <span data-ttu-id="996fc-p125">Öffnen Sie die Registerkarte **Liste** des Designers. Diese Registerkarte wird verwendet, um bestimmte Werte für die Liste *Instanz*  und nicht für die Liste *Vorlage*  festzulegen, aber sie enthält einige Standardwerte, die sie aus der Vorlage übernommen hat.</span><span class="sxs-lookup"><span data-stu-id="996fc-p125">Open the **List** tab of the designer. This tab is used to set certain values for the list *instance*  , not the list *template*  , but it has some default values that it inherited from the template.</span></span>
    
 
16. <span data-ttu-id="996fc-218">Ändern Sie die Werte auf dieser Registerkarte wie folgt:</span><span class="sxs-lookup"><span data-stu-id="996fc-218">Change the values on this tab to the following:</span></span>
    
      -  <span data-ttu-id="996fc-219">**Titel: **Neue Mitarbeiter in Seattle</span><span class="sxs-lookup"><span data-stu-id="996fc-219">**Title**: New Employees in Seattle</span></span>
    
 
  -  <span data-ttu-id="996fc-220">**Listen-URL: **Listen/NewEmployeesInSeattle</span><span class="sxs-lookup"><span data-stu-id="996fc-220">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    
 
  -  <span data-ttu-id="996fc-221">**Beschreibung: **Die neuen Mitarbeiter in Seattle.</span><span class="sxs-lookup"><span data-stu-id="996fc-221">**Description**: The new employees in Seattle.</span></span>
    
 

     <span data-ttu-id="996fc-222">Lassen Sie die Kontrollkästchen auf ihrer Standardeinstellung, speichern Sie die Datei und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="996fc-222">Leave the check boxes at their default status, save the file, and close the designer.</span></span>
    
 
17. <span data-ttu-id="996fc-p126">Die Listeninstanz hat möglicherweise ihren alten Namen im **Projektmappen-Explorer** beibehalten. Wenn dies der Fall ist, öffnen Sie das Kontextmenü für **NewEmployeeOrientationInstance**, wählen **Umbenennen** aus und ändern den Namen in „NewEmployeesInSeattle“.</span><span class="sxs-lookup"><span data-stu-id="996fc-p126">The list instance may have its old name in **Solution Explorer**. If so, open the shortcut menu for **NewEmployeeOrientationInstance**, choose **Rename**, and change the name to NewEmployeesInSeattle.</span></span>
    
 
18. <span data-ttu-id="996fc-225">Öffnen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="996fc-225">Open the schema.xml file.</span></span>
    
 
19. <span data-ttu-id="996fc-p127">Ersetzen Sie im Element **View**, dessen **BaseViewID**-Wert „0" ist, das vorhandene Element **ViewFields** durch das folgende Markup. (Verwenden Sie genau diese GUID für das **FieldRef**-Element mit dem Namen  `Title`.)</span><span class="sxs-lookup"><span data-stu-id="996fc-p127">In the **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `Title`.)</span></span>
    
     <span data-ttu-id="996fc-228">*Zeilenumbrüche können an ungeraden Stellen in dieser automatisch generierten schema.xml-Datei vorkommen. Stellen Sie sicher, dass Sie die übereinstimmenden Start- und Endtags für das **ViewFields**-Element gefunden haben. Fügen Sie Zeilenumbrüche hinzu, um die Lesbarkeit zu verbessern.*</span><span class="sxs-lookup"><span data-stu-id="996fc-228">*Line breaks may come at odd places in this autogenerated schema.xml file. Be sure you have found the matching begin and end tags for the **ViewFields** element. Add line breaks to improve readability.*</span></span> 
    


```
  <ViewFields>
  <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
  </ViewFields>
```

20. <span data-ttu-id="996fc-p128">Ersetzen Sie dann in der Datei „schema.xml“ im Element **View**, dessen **BaseViewID**-Wert „1“ ist, das vorhandene **ViewFields**-Element durch das folgende Markup. (Verwenden Sie genau diese GUID für das **FieldRef**-Element mit dem Namen `LinkTitle`.)</span><span class="sxs-lookup"><span data-stu-id="996fc-p128">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
  </ViewFields>
```

21. <span data-ttu-id="996fc-231">Speichern und schließen Sie die Datei schema.xml.</span><span class="sxs-lookup"><span data-stu-id="996fc-231">Save and close the schema.xml file.</span></span>
    
 
22. <span data-ttu-id="996fc-232">Öffnen Sie die Datei „elements.xml", die ein untergeordnetes Element der Liste  *Instanz*  **NewEmployeesInSeattle** ist (nicht die Datei „elements.xml", die ein untergeordnetes Element der Liste *Vorlage*  **NewEmployeeOrientation**) ist.</span><span class="sxs-lookup"><span data-stu-id="996fc-232">Open the elements.xml file that is a child of the list  *instance*  **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template*  **NewEmployeeOrientation**).</span></span>
    
 
23. <span data-ttu-id="996fc-p129">Füllen Sie in dieser Datei die Liste mit einigen Ausgangsdaten. Hierzu fügen Sie folgendes **Data**-Elementmarkup als untergeordnetes Element des **ListInstance**-Elements hinzu.</span><span class="sxs-lookup"><span data-stu-id="996fc-p129">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
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

24. <span data-ttu-id="996fc-235">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="996fc-235">Save and close the file.</span></span>
    
 
25. <span data-ttu-id="996fc-p130">Doppelklicken Sie im **Projektmappen-Explorer** auf **Feature1**, um den Feature-Designer zu öffnen. Legen Sie im Designer den **Titel** auf Orientierungskomponenten für neue Mitarbeiter und die **Beschreibung** aufListen und andere Komponenten, die zur Orientierung neuer Mitarbeiter im Unternehmen dienen fest. Speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="996fc-p130">In **Solution Explorer**, double-click **Feature1** to open the Feature designer. In the designer, set the **Title** toNew Employee Orientation Components and set the **Description** toLists and other components for getting employees oriented to the company. Save the file, and close the designer.</span></span>
    
 
26. <span data-ttu-id="996fc-239">Wenn **Feature1** im **Projektmappen-Explorer** nicht automatisch umbenannt wurde, öffnen Sie das zugehörige Kontextmenü, wählen **Umbenennen** aus und benennen die Option in „NewEmployeeOrientationComponents“ um.</span><span class="sxs-lookup"><span data-stu-id="996fc-239">If the **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, choose **Rename**, and rename it NewEmployeeOrientationComponents.</span></span>
    
 
27. <span data-ttu-id="996fc-240">Öffnen Sie die Datei „Default.aspx“.</span><span class="sxs-lookup"><span data-stu-id="996fc-240">Open the Default.aspx file.</span></span>
    
 
28. <span data-ttu-id="996fc-p131">Suchen Sie das ASP.NET **Content**-Element mit der ID **PlaceHolderPageTitleInTitleArea**. Ersetzen Sie die standardmäßige Zeichenfolge „Seitentitel“ durch „Neue Mitarbeiter nach Standort“.</span><span class="sxs-lookup"><span data-stu-id="996fc-p131">Find the ASP.NET **Content** element with the ID **PlaceHolderPageTitleInTitleArea**. Replace the default string "Page Title" with "New Employees by Location".</span></span>
    
 
29. <span data-ttu-id="996fc-p132">Suchen Sie das ASP.NET **Content**-Element mit der ID **PlaceHolderMain**.  *Ersetzen*  Sie seinen Inhalt mit dem folgenden Markup. ` _spPageContextInfo` ist ein JavaScript-Objekt, das SharePoint automatisch auf der Seite enthält. Die entsprechende `webAbsoluteUrl`-Eigenschaft gibt die URL des Add-In-Web zurück.</span><span class="sxs-lookup"><span data-stu-id="996fc-p132">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.  *Replace*  its contents with the following markup. The ` _spPageContextInfo` is a JavaScript object that SharePoint automatically includes in the page. It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
```XML
    <p><asp:HyperLink runat="server" 
    NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
    Text="New Employees in Seattle" /></p>
```


## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="996fc-247">Ausführen des Add-Ins und Testen der Liste</span><span class="sxs-lookup"><span data-stu-id="996fc-247">Run the add-in and test the list</span></span>
<span data-ttu-id="996fc-248"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-248"></span></span>


 

 

1. <span data-ttu-id="996fc-p133">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. (Weitere Informationen dazu, wie Endbenutzer ein installiertes SharePoint-Add-In ausführen, finden Sie unter  [Nächste Schritte](#Nextsteps).)</span><span class="sxs-lookup"><span data-stu-id="996fc-p133">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. (To find out how end users run an installed SharePoint Add-in, see  [Next Steps](#Nextsteps).)</span></span>
    
 
2. <span data-ttu-id="996fc-252">Wenn die Standardseite des Add-Ins geöffnet wird, wählen Sie den Link für **Neue Mitarbeiter in Seattle** aus, um die benutzerdefinierte Listeninstanz zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="996fc-252">When the add-in's default page opens, choose the **New Employees in Seattle** link to open the custom list instance.</span></span>
    
    <span data-ttu-id="996fc-253">**Standardseite und die Seite mit der Listenansicht**</span><span class="sxs-lookup"><span data-stu-id="996fc-253">**Default page and list view page**</span></span>

 

  ![Die Standardseite des Add-Ins mit dem Titel "Neue Mitarbeiter nach Standort" wird angezeigt. Es gibt einen Link mit der Bezeichnung "Neue Mitarbeiter in Seattle". Ein Pfeil von diesem Link zeigt auf die Listenansichtsseite für die Liste. Diese hat den Titel "Neue Mitarbeiter in Seattle" und weist die folgende Liste auf.](../../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)
 

    
    
 
3. <span data-ttu-id="996fc-258">Fügen Sie der Liste Elemente hinzu, und löschen Sie Elemente aus der Liste.</span><span class="sxs-lookup"><span data-stu-id="996fc-258">Add and delete items from the list.</span></span>
    
 
4. <span data-ttu-id="996fc-p135">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="996fc-p135">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="996fc-p136">Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="996fc-p136">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="996fc-263"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="996fc-263"></span></span>

<span data-ttu-id="996fc-p137">Bisher gibt es nur wenige Informationen zur Orientierung in der Liste. Wir werden in späteren Artikeln dieser Reihe einige Informationen hinzufügen. Legen wir aber zunächst eine kurze Pause bezüglich der Codierung ein, um etwas über die Bereitstellung von SharePoint-Add-Ins in  [Bereitstellung und Installation eines von SharePoint gehosteten Add-Ins für SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in) zu erfahren.</span><span class="sxs-lookup"><span data-stu-id="996fc-p137">So far, there isn't much orientation information in the list. We'll add some in later articles in this series. But first, take a brief break from coding to learn about deploying SharePoint Add-ins in  [Deploy and install a SharePoint-hosted SharePoint Add-in](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in).</span></span>
 

 

