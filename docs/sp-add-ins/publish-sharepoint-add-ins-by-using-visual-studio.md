
# <a name="publish-sharepoint-add-ins-by-using-visual-studio"></a><span data-ttu-id="45136-101">Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45136-101">Publish SharePoint Add-ins by using Visual Studio</span></span>
<span data-ttu-id="45136-p101">Erfahren Sie, wie Sie Ihre SharePoint-Add-In mithilfe von Microsoft Visual Studio 2013 oder Visual Studio 2012 veröffentlichen. Wenn mit dem Add-In eine Webanwendung verknüpft ist, stellen Sie diese zuerst bereit. Wie bei allen SharePoint-Add-Ins packen Sie dann die SharePoint-Add-In und veröffentlichen sie anschließend. Sie können Ihr Add-In auch optional zur Aufnahme in den Office Store übermitteln.</span><span class="sxs-lookup"><span data-stu-id="45136-p101">Learn how to publish your SharePoint Add-in by using Microsoft Visual Studio 2013 or Visual Studio 2012. If the add-in has an associated web application, you deploy it first. Then, as for all SharePoint Add-ins, you package the SharePoint Add-in and then publish it. You can also optionally choose to submit your add-in for inclusion on the Office Store.</span></span>
 

 <span data-ttu-id="45136-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="45136-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="45136-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="45136-109">Prerequisites</span></span>
<span data-ttu-id="45136-110"><a name="Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="45136-110"></span></span>


 

 

-  [<span data-ttu-id="45136-111">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="45136-111">Microsoft Visual Studio 2013</span></span>](http://go.microsoft.com/fwlink/?LinkId=517284  )
    
    <span data-ttu-id="45136-112">- oder -</span><span class="sxs-lookup"><span data-stu-id="45136-112">-or-</span></span>
    
     <span data-ttu-id="45136-p103">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) und Office-Entwicklertools für Visual Studio. Informationen zum Herunterladen dieser Tools finden Sie auf der [Downloadseite](http://go.microsoft.com/fwlink/?LinkId=234393) im Abschnitt „Tools". (Der neue Publish Manager ist in Visual Studio 2012 oder früheren Versionen nicht verfügbar).</span><span class="sxs-lookup"><span data-stu-id="45136-p103">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) and the Office Developer Tools for Visual Studio. To download the tools, see "Tools" on the [Download page](http://go.microsoft.com/fwlink/?LinkId=234393). (The new Publish Manager is not available in Visual Studio 2012 or earlier versions.)</span></span>
    
 
- <span data-ttu-id="45136-116">Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="45136-116">Microsoft SharePoint</span></span>
    
 

## <a name="publish-by-using-visual-studio-2013"></a><span data-ttu-id="45136-117">Veröffentlichen mit Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="45136-117">Publish by using Visual Studio 2013</span></span>
<span data-ttu-id="45136-118"><a name="VS2013"> </a></span><span class="sxs-lookup"><span data-stu-id="45136-118"></span></span>

<span data-ttu-id="45136-p104">Wenn Ihre von einem Anbieter gehostete SharePoint-Add-In über eine Webanwendung verfügt, stellen Sie zuerst die Dateien für diese bereit. Wie bei allen SharePoint-Add-Ins packen Sie dann die SharePoint-Add-In und veröffentlichen sie anschließend.</span><span class="sxs-lookup"><span data-stu-id="45136-p104">If your provider-hosted SharePoint Add-in has a web application, deploy the files for it first. You then, as for all SharePoint Add-ins, package the SharePoint Add-in and publish it.</span></span>
 

 

 <span data-ttu-id="45136-p105">**Wichtig** Um sicherzustellen, dass Ihre SharePoint-Client-ID und Ihr geheimer Clientschlüssel mit Ihrem Webprojekt veröffentlicht werden, sodass Ihre Webinhalte auf SharePoint-Daten zugreifen können, veröffentlichen Sie Ihr SharePoint-Add-In-Projekt von der Seite **Add-In veröffentlichen**. Sie können diese Seite aufrufen, indem Sie das Kontextmenü der SharePoint-Add-In - nicht das Kontextmenü der Webapp - aufrufen, und dann den Befehl **Veröffentlichen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="45136-p105">**Important** To ensure that your SharePoint Client ID and Client Secret values get published with your web project, which allows your web content to access SharePoint data, publish your SharePoint Add-in project from the **Publish your add-in** page. You access this page by opening the shortcut menu for the SharePoint Add-in, not the shortcut menu for the web app, and then choosing the **Publish** command.</span></span>
 


### <a name="step-1-deploy-the-web-application"></a><span data-ttu-id="45136-123">Schritt 1: Stellen Sie die Webanwendung bereit</span><span class="sxs-lookup"><span data-stu-id="45136-123">Step 1: Deploy the web application</span></span>

<span data-ttu-id="45136-p106">Ihre SharePoint-Add-In ist in der Regel mit einer Hostwebanwendung verknüpft, die Sie auf einem Webserver bereitstellen müssen. Weitere Informationen zur Verwendung des Assistenten zur Veröffentlichung von Webinhalten finden Sie unter  [Vorgehensweise: Bereitstellen eines Webanwendungsprojekts mit der One-Click-Veröffentlichung in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="45136-p106">Your SharePoint Add-in typically has an associated host web application that you need to deploy to a web server. For more information about how to use the Publish Web wizard, see  [How to: Deploy a Web Project using On-Click Publishing in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span></span>
 

 

### <a name="to-open-the-publish-your-add-in-page"></a><span data-ttu-id="45136-126">So öffnen Sie die Seite „Add-In veröffentlichen“</span><span class="sxs-lookup"><span data-stu-id="45136-126">To open the Publish your add-in page</span></span>


- <span data-ttu-id="45136-127">Öffnen Sie im  **Projektmappen-Explorer** das Kontextmenü für das SharePoint-Add-In-Projekt, und wählen Sie dann **Veröffentlichen** aus.</span><span class="sxs-lookup"><span data-stu-id="45136-127">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="45136-128">Die Seite **Add-In veröffentlichen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="45136-128">The  **Publish your add-in** page appears.</span></span>
    
 

### <a name="to-select-or-create-a-profile"></a><span data-ttu-id="45136-129">So wählen oder erstellen Sie ein Profil</span><span class="sxs-lookup"><span data-stu-id="45136-129">To select or create a profile</span></span>


- <span data-ttu-id="45136-130">Wählen Sie in der Liste **Aktuelles Profil** ein Profil aus, das importiert werden soll, oder wählen Sie **<Neu …>** aus, um ein Profil zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="45136-130">In the **Current profile** list, choose a profile to import, or choose **<New …>** to create a profile.</span></span>
    
    <span data-ttu-id="45136-p107">Ein Veröffentlichungsprofil gibt den Server an, auf dem die Web App bereitgestellt wird, sowie die Anmeldedaten, die zur Anmeldung am Server erforderlich sind, die Datenbank, die bereitgestellt werden soll, (falls zutreffend) und weitere Bereitstellungsoptionen. Sie können entsprechend Ihren Anforderungen unterschiedliche Veröffentlichungsprofile erstellen. Sie können z. B. ein Profil zum Testen und ein weiteres Profil zum Veröffentlichen erstellen.</span><span class="sxs-lookup"><span data-stu-id="45136-p107">A publish profile specifies the server to which you're deploying the web app, the credentials that are needed to log on to the server, the databases to deploy (if applicable), and other deployment options. You can create different publish profiles to fit your needs. For example, you might create one profile for testing and another profile for publishing.</span></span>
    
    <span data-ttu-id="45136-p108">Wenn Sie **<Neu …>** auswählen, wird der Assistent **Veröffentlichungsprofil erstellen** angezeigt. Sie können diesen Assistenten verwenden, um ein Veröffentlichungsprofil von einem Webhosting-Anbieter wie Azure zu importieren, oder um ein Profil zu erstellen, und dann manuell den Servernamen, die Anmeldedaten und andere Einstellungen hinzuzufügen. Wenn Sie kein vorhandenes Profil importiert, sondern ein neues Profil erstellt haben, müssen Sie die Werte für die Client-ID und den geheimen Clientschlüssel angeben, wie in [Richtlinien für das Registrieren von Add-Ins für SharePoint 2013](http://msdn.microsoft.com/library/jj687469.aspx) und [Gewusst wie: Erstellen von Client-IDs und geheimen Clientschlüsseln im Microsoft Seller Dashboard](http://msdn.microsoft.com/library/office/jj220036.aspx) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="45136-p108">If you choose **<New …>**, the **Create publishing profile** wizard appears. You can use this wizard to import a publishing profile from a website hosting provider, such as Azure, or to create a profile and then manually add your server name, credentials, and other settings. If you created a new profile rather than imported an existing profile, you'll need to supply client Id and client secret values, as outlined in [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/library/jj687469.aspx) and [How to: Create Client IDs and secrets in the Microsoft Seller Dashboard](http://msdn.microsoft.com/library/office/jj220036.aspx).</span></span>
    
    <span data-ttu-id="45136-p109">Wenn Sie Ihre SharePoint-Add-In an den Office Store übermitteln möchten, müssen Sie für die Client-ID und den geheimen Clientschlüssel Werte verwenden, die im Verkäuferdashboard erstellt werden. Sie können für Client-IDs und geheime Clientschlüssel Werte verwenden, die Sie in der Entwicklungsphase mithilfe der Seite "appregnew.aspx" erstellt haben. Add-Ins, die Sie an den Office Store übermitteln, müssen allerdings Client-IDs und geheime Clientschlüssel verwenden, die Sie vom Verkäuferdashboard erhalten. Außerdem sollten Sie das Veröffentlichungsprofil auf Ihrer Azure-Website erstellen und es dann in Visual Studio importieren, anstatt ein Profil im Assistenten **Veröffentlichungsprofil erstellen** zu erstellen. Wenn Sie ein Profil in Azure erstellen, werden alle Einstellungen auf der Registerkarte **Verbindung**für Sie in Visual Studio bereitgestellt. Weitere Informationen zum Importieren oder Erstellen eines Veröffentlichungsprofils finden Sie unter  [Erstellen eines Veröffentlichungsprofils](http://msdn.microsoft.com/library/dd465337.aspx#creating_a_profile).</span><span class="sxs-lookup"><span data-stu-id="45136-p109">If you plan to submit your SharePoint Add-in to the Office Store, be sure to use client ID and client secret values that are created in the Seller Dashboard. You can use client IDs and client secret values that you generate by using the appregnew.aspx page during the development phase, but add-ins that you submit to the Office Store must use client IDs and client secrets that you get from the Seller Dashboard. Also, you should create the publishing profile on your Azure site and then import it into Visual Studio, rather than creating a profile in the **Create publishing profile** wizard. When you create a profile in Azure, all of the settings on the **Connection** tab are provided for you in Visual Studio. For more information about how to import or create a publishing profile, see [Creating a Publish Profile](http://msdn.microsoft.com/library/dd465337.aspx#creating_a_profile).</span></span>
    
     <span data-ttu-id="45136-p110">**Tipp** Wenn Sie Webinhalte nicht direkt veröffentlichen können, können Sie ein Webbereitstellungspaket erstellen, das ein Administrator für Sie im Web bereitstellen kann. Um ein Webbereitstellungspaket zu erstellen, erstellen Sie ein neues Profil, wählen Sie die Registerkarte **Verbindung** und dann in der Liste **Veröffentlichungsmethode** die Option **Webbereitstellungspaket** aus.</span><span class="sxs-lookup"><span data-stu-id="45136-p110">**TIP** If you can't publish web content directly, you can create a web deploy package that an administrator can deploy to the web for you. To create a web deploy package, create a new profile, choose the **Connection** tab, and then choose **Web Deploy Package** in the **Publish method** list.</span></span>

### <a name="to-deploy-your-web-app-project"></a><span data-ttu-id="45136-144">So stellen Sie Ihr Web-App-Projekt bereit</span><span class="sxs-lookup"><span data-stu-id="45136-144">To deploy your web app project</span></span>


1. <span data-ttu-id="45136-145">Wählen Sie auf der Seite **Add-In veröffentlichen** die Schaltfläche **Webprojekt bereitstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="45136-145">On the **Publish your add-in** page, choose the **Deploy your web project** button.</span></span>
    
    <span data-ttu-id="45136-146">Das Dialogfeld **Webinhalte veröffentlichen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="45136-146">The  **Publish Web** dialog box appears.</span></span>
    
 
2. <span data-ttu-id="45136-147">Geben Sie auf den Registerkarten **Verbindung** und **Einstellungen** alle fehlenden Werte ein.</span><span class="sxs-lookup"><span data-stu-id="45136-147">On the **Connection** and **Settings** tabs, fill in any missing values.</span></span>
    
    <span data-ttu-id="45136-p111">Wenn Sie ändern möchten, wie die Dateien für Ihre SharePoint-Add-In veröffentlicht werden, oder ob das Add-In eine externe Datenbank verwendet, wählen Sie die Registerkarte **Einstellungen** aus. Siehe hierzu den Abschnitt "Configuring the Settings Tab" in [How to: Deploy a Web Project using On-Click Publishing in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="45136-p111">To change how the files for your SharePoint Add-in are published or if the add-in uses an external database, choose the **Settings** tab. See the section "Configuring the Settings Tab" in [How to: Deploy a Web Project using On-Click Publishing in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span></span>
    
 
3. <span data-ttu-id="45136-150">Um zu prüfen, welche Elemente geändert werden, wenn die Web App veröffentlicht wird, wählen Sie auf der Registerkarte **Vorschau** die Schaltfläche **Vorschau starten** aus.</span><span class="sxs-lookup"><span data-stu-id="45136-150">To review what items will change when the web app is deployed, choose the **Start Preview** button on the **Preview** tab.</span></span>
    
 
4. <span data-ttu-id="45136-151">Wählen Sie die Schaltfläche **Veröffentlichen** aus, um das Web-App-Projekt bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="45136-151">Choose the **Publish** button to deploy the web app project.</span></span>
    
 

### <a name="step-2-package-the-add-in"></a><span data-ttu-id="45136-152">Schritt 2: Packen Sie das Add-In</span><span class="sxs-lookup"><span data-stu-id="45136-152">Step 2: Package the Add-in</span></span>


1. <span data-ttu-id="45136-153">Wählen Sie auf der Seite **Add-In veröffentlichen** die Schaltfläche **Package the add-in** (Add-In packen) aus.</span><span class="sxs-lookup"><span data-stu-id="45136-153">On the **Publish your add-in** page, choose the **Package the add-in** button.</span></span>
    
    <span data-ttu-id="45136-154">Der Assistent **Add-Ins für Office und SharePoint veröffentlichen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="45136-154">The  **Publish Office and SharePoint Add-ins** wizard appears.</span></span>
    
 
2. <span data-ttu-id="45136-155">Geben Sie im Textfeld **Wo wird Ihre Website gehostet?** die URL der Website ein, welche die Inhaltsdateien Ihrer SharePoint-Add-In hosten wird.</span><span class="sxs-lookup"><span data-stu-id="45136-155">In the **Where is your website hosted?** text box, enter the URL of the website that will host the content files of your SharePoint Add-in.</span></span>
    
    <span data-ttu-id="45136-p112">Sie müssen eine Adresse angeben, die mit dem Präfix „https“ beginnt. Siehe hierzu [Warum müssen meine Add-Ins SSL-gesichert sein?](http://msdn.microsoft.com/library/jj591603#bk_q7).</span><span class="sxs-lookup"><span data-stu-id="45136-p112">You must specify an address that starts with the "https" prefix. See  [Why do my add-ins have to be SSL-secured?](http://msdn.microsoft.com/library/jj591603#bk_q7).</span></span>
    
     <span data-ttu-id="45136-p113">**Hinweis** Azure-Websites bieten automatisch einen https-Endpunkt. Wenn Sie Ihr Add-In auf einer Office Store-Website oder im Office Store veröffentlichen, muss die Adresse mit einem https-Präfix beginnen. Wenn Sie das Add-In allerdings auf einer lokalen Website veröffentlichen, können Sie ein http-Präfix verwenden.</span><span class="sxs-lookup"><span data-stu-id="45136-p113">**Note** Azure web sites automatically provide an https endpoint. If you publish your add-in on an Office Store site or to the Office Store, the address must start with an https prefix. However, if you publish the add-in to an on-premises site, you can use an http prefix.</span></span>

    <span data-ttu-id="45136-161">Im Textfeld **Wie lautet die Client-ID des Add-Ins?** sollte bereits die Client-ID angezeigt werden, die Sie im Veröffentlichungsprofil eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="45136-161">In the **What is the add-in's client ID?** text box, the client ID that you entered in the publishing profile should already appear.</span></span>
    
    <span data-ttu-id="45136-p114">Wenn Sie für diese Client-ID bisher einen Platzhalterwert verwendet haben, müssen Sie nun eine richtige Client-ID hinzufügen. Diese Informationen werden in das .app-Paket eingebettet und ermöglichen die Kommunikation zwischen Ihren Webinhalten und SharePoint auf der Live-Website.</span><span class="sxs-lookup"><span data-stu-id="45136-p114">If you've used a placeholder value for the client ID until this point, you must add an actual client ID now. This information is embedded in the .app package and enables your web content to communicate with SharePoint on the live site.</span></span>
    
 
3. <span data-ttu-id="45136-164">Klicken Sie auf die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="45136-164">Choose the **Finish** button.</span></span>
    
    <span data-ttu-id="45136-p115">Visual Studio generiert die erforderlichen Dateien, um Ihre SharePoint-Add-In zu veröffentlichen, und öffnet dann den Ordner mit der Veröffentlichungsausgabe. Weitere Informationen zur Installation des Add-Ins finden Sie unter  [Installieren und Verwalten von Add-Ins für SharePoint](http://technet.microsoft.com/library/fp161232.aspx).</span><span class="sxs-lookup"><span data-stu-id="45136-p115">Visual Studio generates the files that are needed to publish your SharePoint Add-in and then opens the publish output folder. For information about how to install the add-in, see  [Install and manage SharePoint Add-ins 2013](http://technet.microsoft.com/library/fp161232.aspx).</span></span>
    
 

### <a name="step-3-publish-your-sharepoint-add-in-on-the-office-store"></a><span data-ttu-id="45136-167">Schritt 3: Veröffentlichen Sie Ihr SharePoint-Add-In im Office Store</span><span class="sxs-lookup"><span data-stu-id="45136-167">Step 3: Publish your SharePoint Add-in on the Office Store</span></span>

<span data-ttu-id="45136-168">Führen Sie die folgenden Schritte aus, wenn Sie Ihr SharePoint-Add-In im Office Store veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="45136-168">Perform the following procedure if you want to submit your SharePoint Add-in to the Office Store.</span></span>
 

 

1. <span data-ttu-id="45136-169">Wählen Sie auf der Seite **Add-In veröffentlichen** die Schaltfläche **Verkäuferdashboard besuchen** aus, und melden Sie sich dann bei Ihrem Microsoft-Verkäuferdashboard an.</span><span class="sxs-lookup"><span data-stu-id="45136-169">On the **Publish your add-in** page, choose the **Visit the Seller Dashboard** button, and then sign in to your Microsoft Seller Dashboard account.</span></span>
    
    <span data-ttu-id="45136-170">Siehe [Veröffentlichen von Office- und SharePoint-Add-Ins und Office 365 Web Apps im Office Store](http://msdn.microsoft.com/library/submit-office-and-sharepoint-add-ins-and-office-365-web-apps-to-the-office-store%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="45136-170">See  [Submit Office and SharePoint Add-ins and Office 365 web apps to the Office Store](http://msdn.microsoft.com/library/submit-office-and-sharepoint-add-ins-and-office-365-web-apps-to-the-office-store%28Office.15%29.aspx).</span></span>
    
 
2. <span data-ttu-id="45136-p116">Wählen Sie **Neue App hinzufügen** aus, tragen Sie die Informationen ein, und senden Sie das Add-In dann an den Office Store. Weitere Informationen finden Sie unter [Verwenden des Verkäuferdashboards zum Übermitteln von Office- und SharePoint-Add-Ins und Office 365-Apps an den Office Store](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="45136-p116">Choose **add a new app**, fill out the information, and then submit the add-in to the Office Store. For details, see  [Use the Seller Dashboard to submit Office and SharePoint Add-ins and Office 365 apps to the Office Store](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx).</span></span>
    
 

## <a name="publish-by-using-visual-studio-2012"></a><span data-ttu-id="45136-173">Veröffentlichen mit Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="45136-173">Publish by using Visual Studio 2012</span></span>
<span data-ttu-id="45136-174"><a name="VS2012"> </a></span><span class="sxs-lookup"><span data-stu-id="45136-174"></span></span>

<span data-ttu-id="45136-175">Wenn Sie soweit sind, dass Sie die SharePoint-Add-In als Paket veröffentlichen können, öffnen Sie den Assistenten zum **Veröffentlichen von Office-Add-Ins**, der die Dateien in Ihrer SharePoint-Add-In für die Veröffentlichung vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="45136-175">When you're ready to package your SharePoint Add-in, open the **Publish Office Add-ins** wizard, which prepares the files in your SharePoint Add-in for publishing.</span></span>
 

 

### <a name="step-1-package-the-sharepoint-add-in"></a><span data-ttu-id="45136-176">Schritt 1: Packen des SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="45136-176">Step 1: Package the SharePoint Add-in</span></span>


1. <span data-ttu-id="45136-177">Öffnen Sie im  **Projektmappen-Explorer** das Kontextmenü für das SharePoint-Add-In-Projekt, und wählen Sie dann **Veröffentlichen** aus.</span><span class="sxs-lookup"><span data-stu-id="45136-177">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="45136-p117">Der Assistent zum **Veröffentlichen von Office-Add-Ins** wird angezeigt. Welche Seiten im Assistenten angezeigt werden, hängt vom Typ der als Paket zu veröffentlichenden SharePoint-Add-In ab. Wenn das Add-In in SharePoint gehostet wird, wird nur die Seite **Zusammenfassung** angezeigt. Soll das Add-In von einem Provider gehostet werden, dann werden auch die Seiten **Profil** und **Hosting** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="45136-p117">The **Publish Office Add-ins** wizard appears. The type of SharePoint Add-in that you're packaging determines the pages that appear in the wizard. If your add-in will be SharePoint-hosted, only the **Summary** page appears. If your add-in will be provider-hosted, the **Profile** and **Hosting** pages also appear.</span></span>
    
 
2. <span data-ttu-id="45136-182">Wenn Ihre SharePoint-Add-In von einem Anbieter gehostet wird, geben Sie in der Liste zur **Angabe des zu veröffentlichenden Profils** den Namen eines Veröffentlichungsprofils an, und wählen Sie dann die Schaltfläche **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="45136-182">If your SharePoint Add-in is provider-hosted, specify a publishing profile name in the **Which profile do you wish to publish?** list, and then choose the **Next** button.</span></span>
    
    <span data-ttu-id="45136-183">Im Veröffentlichungsprofil werden die Informationen gespeichert, die Sie auf der Seite **Hosting** eingeben.</span><span class="sxs-lookup"><span data-stu-id="45136-183">The publishing profile saves the information that you enter in the **Hosting** page.</span></span>
    
 
3. <span data-ttu-id="45136-184">Geben Sie in der Liste zur **Angabe des Websitehosts** die URL der Webanwendung an, die als Host der SharePoint-Add-In fungieren wird.</span><span class="sxs-lookup"><span data-stu-id="45136-184">In the **Where is your website hosted?** list, specify the URL for the web application that will host your SharePoint Add-in.</span></span>
    
 
4. <span data-ttu-id="45136-185">Geben Sie in den Feldern zur **Angabe der Identität des Add-Ins** die Client-ID und das Clientgeheimnis des Add-Ins ein, und wählen Sie dann die Schaltfläche **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="45136-185">In the boxes under **What is the identity of your add-in?**, specify the client ID and client secret for your add-in, and then choose the **Next** button.</span></span>
    
    <span data-ttu-id="45136-186">Siehe [Autorisierung und Authentifizierung von SharePoint-Add-Ins](authorization-and-authentication-of-sharepoint-add-ins)</span><span class="sxs-lookup"><span data-stu-id="45136-186">See  [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins).</span></span>
    
 
5. <span data-ttu-id="45136-187">Aktivieren Sie für alle Typen von SharePoint-Add-Ins das Kontrollkästchen **Ausgabeordner nach dem Verpacken öffnen**, sofern es nicht bereits aktiviert ist, und wählen Sie dann die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="45136-187">For all types of SharePoint Add-ins, select the **Open output folder after successful packaging** check box, if it isn't already selected, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="45136-p118">Visual Studio generiert alle Dateien, die zum Veröffentlichen der SharePoint-Add-In erforderlich sind. Sie finden diese Dateien im Ordner  `app.Publish` im Projektausgabeordner (beispielsweise `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`). Dieser Ordner enthält eine APP-Datei für die SharePoint-Add-In und mehrere Dateien für die Webanwendung (wenn die SharePoint-Add-In cloudbasiert ist). Alle SharePoint-Add-Ins verfügen über eine APP-Datei, die das Add-In-Manifest zum Veröffentlichen der SharePoint-Add-In enthält. Vom Anbieter gehostete SharePoint-Add-Ins enthalten auch Dateien zum Veröffentlichen der Hostwebanwendung.</span><span class="sxs-lookup"><span data-stu-id="45136-p118">Visual Studio generates all of the files that you need to publish your SharePoint Add-in. You can find these files in the  `app.Publish` folder of your project output folder (for example, `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`). That folder will contain a .app file for your SharePoint Add-in and multiple files for the web application (if your SharePoint Add-in is cloud-based). All SharePoint Add-ins include a .app file, which is the add-in manifest to publish the SharePoint Add-in. Provider-hosted SharePoint Add-ins also include files for publishing the host web application.</span></span>
    
 

### <a name="step-2-publish-the-web-application"></a><span data-ttu-id="45136-193">Schritt 2: Veröffentlichen Sie die Webanwendung</span><span class="sxs-lookup"><span data-stu-id="45136-193">Step 2: Publish the web application</span></span>

<span data-ttu-id="45136-p119">Wenn die SharePoint-Add-In von einem Anbieter gehostet wird, müssen Sie die verknüpfte Webanwendung auf einem Webserver veröffentlichen. Visual Studio erzeugt ein Bereitstellungspaket und ein Skript, das Ihnen die Ausführung dieser Aufgabe erleichtern soll.</span><span class="sxs-lookup"><span data-stu-id="45136-p119">If your SharePoint Add-in is provider-hosted, you'll typically have an associated host web application that you need to publish to a web server. Visual Studio generates a deployment package and a script to help you perform this task.</span></span>
 

 
<span data-ttu-id="45136-p120">Das Bereitstellungspaket des Webanwendungsprojekts befindet sich in einer komprimierten Datei (.ZIP) im Ordner  `app.publish`. Neben dieser ZIP-Datei enthält der Ordner  `app.publish` folgende Dateien:</span><span class="sxs-lookup"><span data-stu-id="45136-p120">The deployment package of the web application project is contained in a compressed (.zip) file in the  `app.publish` folder. In addition to the .zip file, the `app.publish` folder contains the following files:</span></span>
 

 


|<span data-ttu-id="45136-198">**Datei**</span><span class="sxs-lookup"><span data-stu-id="45136-198">**File**</span></span>|<span data-ttu-id="45136-199">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="45136-199">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="45136-200">_Projektname_.deploy.cmd</span><span class="sxs-lookup"><span data-stu-id="45136-200">_ProjectName_.deploy.cmd</span></span>|<span data-ttu-id="45136-201">Dies ist eine Befehlszeilen-Batchdatei, die Web Deploy aufruft, um die Installation des Pakets über die Befehlszeile zu erleichtern.</span><span class="sxs-lookup"><span data-stu-id="45136-201">This file is a command-line batch file that invokes Web Deploy so that you can more easily install the package at a command prompt.</span></span>|
| <span data-ttu-id="45136-202">_Projektname_.SetParameters.xml</span><span class="sxs-lookup"><span data-stu-id="45136-202">_ProjectName_.SetParameters.xml</span></span>|<span data-ttu-id="45136-p121">Diese Datei enthält Parameter, die Web Deploy übergeben werden, wenn Sie die App mithilfe der Datei "deploy.cmd" installieren. Die Paketeinstellungen von Visual Studio bestimmen die Standardwerte für die einzelnen Parameter. Sie können diese Werte beispielsweise ändern, wenn Sie die Webanwendung auf mehreren Servern bereitstellen und für jeden Server andere Einstellungen verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="45136-p121">This file contains parameters that are passed to Web Deploy when you use the deploy.cmd file to install the package. The Visual Studio package settings determine the default value that's specified for each parameter. You can change these values if, for example, you want to install the web application to multiple servers and use different settings for each server.</span></span>|
| <span data-ttu-id="45136-206">_Projektname_.SourceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="45136-206">_ProjectName_.SourceManifest.xml</span></span>|<span data-ttu-id="45136-p122">Diese Datei enthält Einstellungen, die Visual Studio an Web Deploy übergibt und die von Web Deploy zum Erstellen des Webpakets verwendet werden. Web Deploy benötigt diese Datei nur zum Erstellen des Pakets. Diese Datei wird nicht zur Installation des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="45136-p122">This file contains settings that Visual Studio passes to Web Deploy and that Web Deploy uses to create the web package. Web Deploy requires this file only to create the package. This file isn't used when the package is installed.</span></span>|
<span data-ttu-id="45136-210">Eine Schritt-für-Schritt-Anleitung finden Sie unter [Gewusst wie: Installieren eines Bereitstellungspakets mit der von Visual Studio erstellten Datei „deploy.cmd“](http://go.microsoft.com/fwlink/?LinkID=254954)</span><span class="sxs-lookup"><span data-stu-id="45136-210">For step-by-step guidance, see  [How to: Install a Deployment Package Using the deploy.cmd File Created by Using Visual Studio](http://go.microsoft.com/fwlink/?LinkID=254954)</span></span>
 

 

### <a name="step-3-publish-your-sharepoint-add-in"></a><span data-ttu-id="45136-211">Schritt 3: Veröffentlichen Sie Ihr SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="45136-211">Step 3: Publish your SharePoint Add-in</span></span>
<span data-ttu-id="45136-212"><a name="Publish"> </a></span><span class="sxs-lookup"><span data-stu-id="45136-212"></span></span>

<span data-ttu-id="45136-p123">Zum Veröffentlichen der SharePoint-Add-In laden Sie die Add-In-Manifestdatei (.APP) des Add-Ins in den Office Store, den Katalog für Add-Ins für Office, SharePoint, eine Dateifreigabe oder einen Exchange-Katalog hoch. Das Add-In-Manifest Ihres Add-Ins befindet sich im Ordner  `app.publish`, z. B.  `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`. Weitere Informationen zum Veröffentlichen Ihrer SharePoint-Add-In finden Sie unter  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="45136-p123">To publish your SharePoint Add-in, upload the add-in manifest file (.app) of your add-in to the Office Store, the Office Add-ins catalog, SharePoint, a file share, or the Exchange catalog. The add-in manifest for your add-in is located in the  `app.publish` folder, such as `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`. For more information about how to publish your SharePoint Add-in, see  [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="45136-216">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="45136-216">Additional resources</span></span>
<span data-ttu-id="45136-217"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="45136-217"></span></span>


-  [<span data-ttu-id="45136-218">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="45136-218">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="45136-219">Veröffentlichen Ihres Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="45136-219">Publish your Office Add-in</span></span>](http://msdn.microsoft.com/library/7f3ae6a0-06e9-438c-8899-bd9f605e6d9e%28Office.15%29.aspx)
    
 

