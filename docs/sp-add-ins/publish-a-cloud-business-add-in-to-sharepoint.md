
# <a name="publish-a-cloud-business-add-in-to-sharepoint"></a><span data-ttu-id="d8199-101">Veröffentlichen eines Cloud-Business-Add-Ins in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8199-101">Publish a cloud business add-in to SharePoint</span></span>
<span data-ttu-id="d8199-p101">Sie können Ihr Cloud-Geschäfts-Add-In als vom Anbieter gehostetes SharePoint-Add-In veröffentlichen. Mit einem vom Anbieter gehosteten Add-In sind Sie hinsichtlich der Bereitstellung Ihrer Web App und Datenbank flexibel. Sie können sie lokal auf einer SharePoint-Website, in Windows Azure oder auf einer Hosting-Website eines Drittanbieters bereitstellen. Nachdem Sie Ihr Add-In veröffentlicht haben, können die Benutzer das Add-In auf ihren Computern und mobilen Geräten aus SharePoint starten.</span><span class="sxs-lookup"><span data-stu-id="d8199-p101">You can publish your cloud business add-in as a provider-hosted SharePoint add-in. A provider-hosted add-in gives you the flexibility of deploying your web app and database to an on-premise SharePoint site, to Microsoft Azure, or to a third-party hosting site. After you publish your add-in, others can run it from SharePoint on their computers and mobile devices.</span></span>
 
<span data-ttu-id="d8199-105">Sie können Ihr Add-In mit WebDeploy direkt auf einer Website veröffentlichen oder ein Paket für Ihr Add-In erstellen, das auf mehreren Servern bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="d8199-105">You can publish your add-in directly to a site using WebDeploy, or you can create a package for your add-in that can be deployed to multiple servers.</span></span>
 

 <span data-ttu-id="d8199-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d8199-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="to-publish-an-add-in"></a><span data-ttu-id="d8199-109">So veröffentlichen Sie ein Add-In</span><span class="sxs-lookup"><span data-stu-id="d8199-109">To publish an add-in</span></span>
<span data-ttu-id="d8199-110"><a name="publish"> </a></span><span class="sxs-lookup"><span data-stu-id="d8199-110"></span></span>


1. <span data-ttu-id="d8199-111">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü des Anwendungsknotens auf der obersten Ebene wie in Abbildung 1 dargestellt, und klicken Sie dann auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="d8199-111">In **Solution Explorer**, open the shortcut menu for the top-level application node as shown in Figure 1, and then choose **Publish**.</span></span>
    
    <span data-ttu-id="d8199-112">**Abbildung 1. Der Knoten auf oberster Ebene**</span><span class="sxs-lookup"><span data-stu-id="d8199-112">**Figure 1. The top-level node**</span></span>

 

  ![Der Knoten „Vorfallverwaltung“](../../images/CBA_IM_18.PNG)
 

 

 
2. <span data-ttu-id="d8199-114">Klicken Sie im Assistenten zum Veröffentlichen von LightSwitch-Anwendungen auf der Seite **SharePoint-Optionen** auf das Optionsfeld **Von Anbieter gehostet** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-114">In the LightSwitch Publish Application Wizard, on the **SharePoint Options** page, choose the **Provider-hosted** option button, and then choose **Next**.</span></span>
    
 
3. <span data-ttu-id="d8199-115">Klicken Sie auf der Seite **Anwendungsserverkonfiguration** auf das Optionsfeld **IIS-Server** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-115">On the **Application Server Configuration** page, choose the **IIS Server** option button, and then choose **Next**.</span></span>
    
     <span data-ttu-id="d8199-p103">**Hinweis** Wenn Sie über eine Datei mit Veröffentlichungseinstellungen (.publishsettings oder .pubxml) verfügen, die für ein anderes Add-In erstellt wurde, können Sie diese Datei verwenden, um die restlichen zum Veröffentlichen erforderlichen Informationen bereitzustellen. Wenn dies der Fall ist, klicken Sie im Assistenten auf die Schaltfläche **Einstellungen importieren**.</span><span class="sxs-lookup"><span data-stu-id="d8199-p103">**Note** If you have a publish settings (.publishsettings or .pubxml) file that was created for another add-in, you can use that file to provide the rest of the information that you need for publishing. If so, choose the **Import Settings** button in the wizard.</span></span>
4. <span data-ttu-id="d8199-118">Klicken Sie auf der Seite **Ausgabe veröffentlichen** auf das Optionsfeld **Jetzt direkt auf einem Server veröffentlichen**, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-118">On the **Publish Output** page, choose the **Publish directly to a server now** option button, and then choose **Next**.</span></span>
    
 
5. <span data-ttu-id="d8199-119">Geben Sie auf der Seite **Veröffentlichungseinstellungen** in das Textfeld **Dienst-URL** die URL des Servers ein, auf dem Sie Ihr Add-In veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="d8199-119">On the **Publish Settings** page, in the **Service URL** text box, enter the URL for the server where you want to publish your add-in.</span></span>
    
    <span data-ttu-id="d8199-p104">Wenn Sie an ein Hostingunternehmen veröffentlichen, wird dieser Wert vom Unternehmen bereitgestellt. Er kann in jedem der folgenden Formate vorliegen:</span><span class="sxs-lookup"><span data-stu-id="d8199-p104">If you're publishing to a hosting company, the company provides this value. It can be in any of the following formats:</span></span>
    
      -  <span data-ttu-id="d8199-122">_HostingCompanyURL_ (z. B. `contoso.com`)</span><span class="sxs-lookup"><span data-stu-id="d8199-122">_HostingCompanyURL_ (for example, `contoso.com`)</span></span>
    
 
  -  <span data-ttu-id="d8199-123">`https://` _HostingCompanyURL_ (z. B. `https://contoso.com`)</span><span class="sxs-lookup"><span data-stu-id="d8199-123">`https://` _HostingCompanyURL_ (for example, `https://contoso.com`)</span></span>
    
 
  -  <span data-ttu-id="d8199-124">`https://` _HostingCompanyURL_ `:8172/msdeploy.axd` (z. B. `https://contoso.com:8172/msdeploy.axd`)</span><span class="sxs-lookup"><span data-stu-id="d8199-124">`https://` _HostingCompanyURL_ `:8172/msdeploy.axd` (for example, `https://contoso.com:8172/msdeploy.axd`)</span></span>
    
 

    <span data-ttu-id="d8199-125">Wenn Sie zu Testzwecken an Internetinformationsdienste (IIS) auf Ihrem eigenen Computer veröffentlichen, geben Sie `localhost` oder den Namen Ihres Computers ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-125">If you're publishing to Internet Information Services (IIS) on your own computer for testing, enter  `localhost` or the name of your computer.</span></span>
    
    <span data-ttu-id="d8199-126">Wenn Sie an einen Server in Ihrem eigenen Netzwerk veröffentlichen, geben Sie eine der folgenden URLs ein:</span><span class="sxs-lookup"><span data-stu-id="d8199-126">If you're publishing to a server on your own network, enter one of these URLs:</span></span>
    
      -  <span data-ttu-id="d8199-127">`http://` _ServerName_</span><span class="sxs-lookup"><span data-stu-id="d8199-127">`http://` _servername_</span></span>
    
 
  -  <span data-ttu-id="d8199-128">`http://` _ServerName_ `/msdeployagentservice`</span><span class="sxs-lookup"><span data-stu-id="d8199-128">`http://` _servername_ `/msdeployagentservice`</span></span>
    
 

     <span data-ttu-id="d8199-129">**Hinweis** Wenn Sie durch eine Firewall hindurch veröffentlichen, müssen Sie möglicherweise Port 8172 öffnen.</span><span class="sxs-lookup"><span data-stu-id="d8199-129">**Note** If you're publishing through a firewall, you might have to open port 8172.</span></span>
6. <span data-ttu-id="d8199-130">Geben Sie im Textfeld **Website/Anwendung** den Namen der IIS-Website und den Ihres Add-Ins ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-130">In the **Site/application** text box, enter the names of the IIS website and your add-in.</span></span>
    
    <span data-ttu-id="d8199-p105">Wenn Sie Ihr Add-In bei einem Hosting-Unternehmen veröffentlichen, stellt das Unternehmen diesen Wert bereit. In der Regel ist das ein Domänenname (z. B.  `contoso.com`) oder ein Domänenname und ein Add-In-Name (z. B.  `contoso.com/MyApp`).</span><span class="sxs-lookup"><span data-stu-id="d8199-p105">If you're publishing to a hosting company, the company provides this value. It's typically either a domain name (for example,  `contoso.com`) or a domain and add-in name (for example,  `contoso.com/MyApp`).</span></span>
    
    <span data-ttu-id="d8199-p106">Wenn Sie Ihr Add-In zu Testzwecken in IIS auf Ihrem Computer oder auf einem Server in Ihrem internen Netzwerk veröffentlichen, geben Sie den Namen der Website und des Add-Ins so ein, wie sie im IIS-Manager angezeigt werden. Wenn Sie das Add-In "MyApp" auf der Standardwebsite in IIS veröffentlichen, geben Sie Standwardwebsite/MyApp ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-p106">If you're publishing to IIS on your own computer for testing, or you're publishing to a server on your internal network, enter the site and add-in name as they appear in IIS Manager. For example, if you're publishing the add-in MyApp to the default website in IIS, enter Default Web Site/MyApp.</span></span>
    
     <span data-ttu-id="d8199-135">**Hinweis** Wenn Sie in einem vorhandenen Webordner veröffentlichen und vorhandene Inhalte entfernen möchten, müssen Sie das Kontrollkästchen **Zusätzliche Dateien auf dem Ziel entfernen** aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d8199-135">**Note** If you're publishing to an existing web folder and want to remove any existing content, select the **Remove additional files at destination** check box.</span></span>
7. <span data-ttu-id="d8199-136">Geben Sie in den Textfeldern **Benutzername** und **Kennwort** die Anmeldeinformationen eines Kontos ein, das über ausreichende Bereichtigungen verfügt, um Bereitstellungsaufgaben auf dem Zielwebserver auszuführen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-136">In the **User Name** and **Password** text boxes, enter credentials for an account that has sufficient authority to perform deployment tasks on the destination web server, and then choose **Next**.</span></span>
    
    <span data-ttu-id="d8199-137">Wenn Sie an ein Hostingunternehmen veröffentlichen, werden diese Werte vom Unternehmen bereitgestellt</span><span class="sxs-lookup"><span data-stu-id="d8199-137">If you're publishing to a hosting company, the company provides these values.</span></span>
    
 
8. <span data-ttu-id="d8199-138">Klicken Sie auf der Seite **Sicherheitseinstellungen** auf das Optionsfeld **Ja, Benutzer müssen eine Verbindung mithilfe von HTTPS herstellen** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-138">On the **Security Settings** page, choose the **Yes, users must connect using HTTPS** option button, and then choose **Next**.</span></span>
    
 
9. <span data-ttu-id="d8199-139">Geben Sie auf der Seite **Datenverbindungen** auf der Registerkarte **Datenbankverbindungen** die Administrator- und Benutzerverbindungszeichenfolgen des Datenbankservers ein, auf dem Sie die Datenbank Ihres Add-Ins veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="d8199-139">On the **Data connections** page, on the **Database Connections** tab, enter the administrator and user connection strings for the database server where you want to publish your add-in's database.</span></span>
    
     <span data-ttu-id="d8199-140">**Hinweis** Die Datenbank muss nicht auf dem Server gespeichert sein, auf dem Sie das Add-In veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="d8199-140">**Note** The database doesn't have to be located on the server where you are publishing the add-in.</span></span>
10. <span data-ttu-id="d8199-141">Aktualisieren Sie bei Bedarf auf der Registerkarte **Angefügte Datenquellen** die Verbindungszeichenfolgen von zusätzlichen Verbindungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-141">On the **Attached Data Sources** tab, update the connection strings for any additional connections as needed, and then choose **Next**.</span></span>
    
 
11. <span data-ttu-id="d8199-142">Geben Sie auf der Seite **Anbieter-Hosting** im Textfeld **Wo wird Ihre LightSwitch-Anwendung gehostet** die vollständige URL Ihres Add-Ins ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-142">On the **Provider Hosting** page, in the **Where is your LightSwitch application hosted** text box, enter the full URL for your add-in.</span></span>
    
    <span data-ttu-id="d8199-143">In den meisten Fällen stimmt diese URL mit den von Ihnen zuvor eingegebenen Werten unter **Dienst-URL** und **Website/Anwendung** überein (z. B. `https://contoso.com/MyApplication`).</span><span class="sxs-lookup"><span data-stu-id="d8199-143">In most cases this URL will be the same as the **Service URL** and **Site/application** values that you entered earlier (for example `https://contoso.com/MyApplication`).</span></span>
    
 
12. <span data-ttu-id="d8199-144">Geben Sie die Werte **Client-ID** und **Clientgeheimnis** für Ihr Add-In ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-144">Enter the **Client ID** and **Client Secret** values for your add-in.</span></span>
    
    <span data-ttu-id="d8199-p107">Sie können diese Werte von der Seite **appregnew** Ihrer SharePoint-Website oder aus dem Verkäuferdashboard abrufen. Weitere Informationen dazu finden Sie unter [Richtlinien für das Registrieren von SharePoint-Add-Ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8199-p107">You can get these values from the **appregnew** page of your SharePoint site or from the Seller dashboard. See [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span></span>
    
 
13. <span data-ttu-id="d8199-147">Klicken Sie auf **Veröffentlichen**, um Ihr Add-In zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="d8199-147">Choose **Publish** to publish your add-in.</span></span>
    
    <span data-ttu-id="d8199-148">Nachdem Ihr Add-In veröffentlicht wurde, wird der **Datei-Explorer** geöffnet. Er zeigt das Verzeichnis **Veröffentlichen** Ihres Projekts an.</span><span class="sxs-lookup"><span data-stu-id="d8199-148">When your add-in is published, **File Explorer** opens and displays the **Publish** directory for your project.</span></span>
    
 

## <a name="to-package-an-add-in"></a><span data-ttu-id="d8199-149">So packen Sie ein Add-In</span><span class="sxs-lookup"><span data-stu-id="d8199-149">To package an add-in</span></span>
<span data-ttu-id="d8199-150"><a name="package"> </a></span><span class="sxs-lookup"><span data-stu-id="d8199-150"></span></span>


1. <span data-ttu-id="d8199-151">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü des Anwendungsknotens auf der obersten Ebene wie in Abbildung 1 dargestellt, und klicken Sie dann auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="d8199-151">In **Solution Explorer**, open the shortcut menu for the top-level application node as shown in Figure 1, and then choose **Publish**.</span></span>
    
    <span data-ttu-id="d8199-152">**Abbildung 1. Der Knoten auf oberster Ebene**</span><span class="sxs-lookup"><span data-stu-id="d8199-152">**Figure 1. The top-level node**</span></span>

 

  ![Der Knoten „Vorfallverwaltung“](../../images/CBA_IM_18.PNG)
 

    
    
 
2. <span data-ttu-id="d8199-154">Klicken Sie im Assistenten zum Veröffentlichen von LightSwitch-Anwendungen auf der Seite **SharePoint-Optionen** auf das Optionsfeld **Von Anbieter gehostet** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-154">In the LightSwitch Publish Application Wizard, on the **SharePoint Options** page, choose the **Provider-hosted** option button, and then choose **Next**.</span></span>
    
 
3. <span data-ttu-id="d8199-155">Klicken Sie auf der Seite **Anwendungsserverkonfiguration** auf das Optionsfeld **IIS-Server** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-155">On the **Application Server Configuration** page, choose the **IIS Server** option button, and then choose **Next**.</span></span>
    
     <span data-ttu-id="d8199-p108">**Hinweis** Wenn Sie über eine Datei mit Veröffentlichungseinstellungen (.publishsettings oder .pubxml) verfügen, die für ein anderes Add-In erstellt wurde, können Sie diese Datei verwenden, um die restlichen zum Veröffentlichen erforderlichen Informationen bereitzustellen. Wenn dies der Fall ist, klicken Sie im Assistenten auf die Schaltfläche **Einstellungen importieren**.</span><span class="sxs-lookup"><span data-stu-id="d8199-p108">**Note** If you have a publish settings (.publishsettings or .pubxml) file that was created for another add-in, you can use that file to provide the rest of the information that you need for publishing. If so, choose the **Import Settings** button in the wizard.</span></span>
4. <span data-ttu-id="d8199-158">Klicken Sie auf der Seite **Ausgabe veröffentlichen** auf das Optionsfeld **Paket auf Datenträger erstellen** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-158">On the **Publish Output** page, choose the **Create a package on disk** option button, and then choose **Next**.</span></span>
    
 
5. <span data-ttu-id="d8199-159">Geben Sie auf der Seite **Veröffentlichungseinstellungen** im Textfeld **Wie soll der Name der Website lauten?** den Namen für Ihre Website ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-159">On the **Publish Settings** page, in the **What should the website be named?** text box, enter a name for the website.</span></span>
    
    <span data-ttu-id="d8199-160">Der Standardname ist der Name des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="d8199-160">The default name is the add-in name.</span></span>
    
 
6. <span data-ttu-id="d8199-161">Geben Sie im Textfeld **Wo soll das Paket erstellt werden?** den Pfad des Speicherorts ein, an dem die Ausgabe veröffentlicht werden soll, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-161">In the **Where should the package be created?** text box, enter the path for the location where you want the output to be published, and then choose **Next**.</span></span>
    
    <span data-ttu-id="d8199-162">Der Standardspeicherort ist das Unterverzeichnis „Veröffentlichen“ Ihres Projektordners.</span><span class="sxs-lookup"><span data-stu-id="d8199-162">The default location is the Publish subdirectory under your project directory.</span></span>
    
 
7. <span data-ttu-id="d8199-163">Klicken Sie auf der Seite **Sicherheitseinstellungen** auf das Optionsfeld **Ja, Benutzer müssen eine Verbindung mithilfe von HTTPS herstellen** und dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-163">On the **Security Settings** page, choose the **Yes, users must connect using HTTPS** option button, and then choose **Next**.</span></span>
    
 
8. <span data-ttu-id="d8199-164">Klicken Sie auf der Seite **Datenbankkonfiguration** auf das Optionsfeld **Neue Datenbank mit folgendem Namen erstellen**, und geben Sie den Namen Ihres Add-Ins als Datenbanknamen ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-164">On the **Database Configuration** page, choose the **Generate a new database called** option button and enter your add-in's name as the database name.</span></span>
    
 
9. <span data-ttu-id="d8199-165">Klicken Sie auf die Registerkarte **Angefügte Datenquellen**, aktualisieren Sie bei Bedarf die Verbindungszeichenfolgen von zusätzlichen Verbindungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="d8199-165">Choose the **Attached Data Sources** tab and update the connection strings for any additional connections as needed, and then choose **Next**.</span></span>
    
 
10. <span data-ttu-id="d8199-166">Geben Sie auf der Seite **Anbieter-Hosting** im Textfeld **Wo wird Ihre LightSwitch-Anwendung gehostet** die vollständige URL Ihres Add-Ins ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-166">On the **Provider Hosting** page, in the **Where is your LightSwitch application hosted** text box, enter the full URL for your add-in.</span></span>
    
    <span data-ttu-id="d8199-167">In den meisten Fällen stimmt diese URL mit den von Ihnen zuvor eingegebenen Werten unter **Dienst-URL** und **Website/Anwendung** überein (z. B. `https://contoso.com/MyApplication`).</span><span class="sxs-lookup"><span data-stu-id="d8199-167">In most cases this URL will be the same as the **Service URL** and **Site/application** values that you entered earlier (for example `https://contoso.com/MyApplication`).</span></span>
    
 
11. <span data-ttu-id="d8199-168">Geben Sie die Werte **Client-ID** und **Clientgeheimnis** für Ihr Add-In ein.</span><span class="sxs-lookup"><span data-stu-id="d8199-168">Enter the **Client ID** and **Client Secret** for your add-in.</span></span>
    
    <span data-ttu-id="d8199-p109">Sie können diese Werte von der Seite **appregnew** Ihrer SharePoint-Website oder aus dem Verkäuferdashboard abrufen. Weitere Informationen dazu finden Sie unter [Richtlinien für das Registrieren von SharePoint-Add-Ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8199-p109">You can get these values from the **appregnew** page of your SharePoint site or from the Seller dashboard. See [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span></span>
    
 
12. <span data-ttu-id="d8199-171">Klicken Sie auf **Veröffentlichen**, um Ihr Add-In zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="d8199-171">Choose **Publish** to publish your add-in.</span></span>
    
    <span data-ttu-id="d8199-p110">Nachdem Ihr Add-In veröffentlicht wurde, wird eine ZIP-Datei, die das Paket enthält, in das Verzeichnis kopiert, das Sie in Schritt 4 angegeben haben. Nachdem dieses Paket erstellt wurde, kann ein Administrator das MSDeploy-Tool verwenden, um Ihr Add-In auf Servern bereitzustellen, die IIS und SQL Server ausführen.</span><span class="sxs-lookup"><span data-stu-id="d8199-p110">When your add-in is published, a .zip file that contains the package is placed in the directory that you specified in step 4. After this package has been created, a server administrator can use the MSDeploy tool to deploy your add-in to servers that are running IIS and SQL Server.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="d8199-174">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d8199-174">Additional resources</span></span>
<span data-ttu-id="d8199-175"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d8199-175"></span></span>


-  [<span data-ttu-id="d8199-176">Registrieren von SharePoint-Add-Ins 2013</span><span class="sxs-lookup"><span data-stu-id="d8199-176">Register SharePoint Add-ins 2013</span></span>](register-sharepoint-add-ins-2013)
    
 
-  [<span data-ttu-id="d8199-177">Veröffentlichen von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d8199-177">Publish cloud business add-ins</span></span>](publish-cloud-business-add-ins)
    
 

