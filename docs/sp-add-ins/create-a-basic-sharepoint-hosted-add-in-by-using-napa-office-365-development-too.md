---
title: Erstellen eines einfachen von SharePoint gehosteten Add-Ins mithilfe von Napa Office 365-Entwicklungstools
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1551c0a7d5cb453a5093563298c9afb9225f7997
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools"></a><span data-ttu-id="3a9e5-102">Erstellen eines einfachen von SharePoint gehosteten Add-Ins mithilfe von Napa Office 365-Entwicklungstools</span><span class="sxs-lookup"><span data-stu-id="3a9e5-102">Create a basic SharePoint-hosted add-in by using Napa Office 365 Development Tools</span></span>
<span data-ttu-id="3a9e5-103">Erfahren Sie, wie Sie ein einfaches von SharePoint gehostetes SharePoint-Add-In mithilfe von Napa Office 365-Entwicklungstools erstellen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-103">Learn how to create a basic SharePoint-hosted SharePoint Add-in by using Napa Office 365 Development Tools.</span></span>
 

 
![Schaltfläche „Ausführen“](../images/Apps_NAPA_Run_Button.png)
 
 [<span data-ttu-id="3a9e5-105">Führen Sie jetzt dieses Beispiel aus!</span><span class="sxs-lookup"><span data-stu-id="3a9e5-105">Run this sample now!</span></span>](http://go.microsoft.com/fwlink/?LinkId=313212)
 

 <span data-ttu-id="3a9e5-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="3a9e5-p102">Napa ist ein Tool, mit dem Sie von SharePoint gehostete SharePoint-Add-Ins erstellen können. Napa selbst wird als ein (vom Anbieter gehostetes) SharePoint-Add-In implementiert, das auf SharePoint Online-Websites installiert werden kann, die mit der Vorlage **Entwicklerwebsite** erstellt werden. SharePoint-Entwicklerwebsites verfügen über eine Bibliothek namens **Add-Ins im Test** auf der Startseite. Anweisungen zum Erstellen einer Entwicklerwebsite und Installieren von Napa finden Sie weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p102">Napa is a tool that you can use to create SharePoint-hosted SharePoint Add-ins. Napa is itself implemented as a (provider-hosted) SharePoint Add-in that can be installed on SharePoint Online websites that are created with the  **Developer Site** template. SharePoint developer sites have a library called **Add-ins in Testing** on the home page. Instructions for creating a developer site and installing Napa are later in this article.</span></span>
 

 <span data-ttu-id="3a9e5-112">**Hinweis** Die Installation von Napa wird nicht für lokale SharePoint-Bereitstellungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-112">**Note**  We do not support installing Napa to on-premises SharePoint.</span></span>
 

<span data-ttu-id="3a9e5-p103">Durch die Verwendung von Napa können Sie Ihr SharePoint-Add-Ins im Browser statt in Visual Studio erstellen. Sie können das Projekt bei komplexeren Szenarios jederzeit herunterladen und in Visual Studio öffnen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p103">By using Napa, you can create your SharePoint Add-ins inside your browser instead of in Visual Studio. At any time, you can download your project and open it in Visual Studio for more advanced scenarios.</span></span>
 
<span data-ttu-id="3a9e5-p104">Durch Befolgen der Schritte in diesem Artikel erfahren Sie, wie Sie ein einfaches in SharePoint gehostetes SharePoint-Add-In mithilfe von Napa erstellen. Das von Ihnen erstellte Add-In enhält Steuerelemente und Code für das Verwalten von Listen und Listenelementen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p104">By following this article, you can learn how to create a simple SharePoint-hosted SharePoint Add-in by using Napa. The add-in that you'll create includes controls and code for managing lists and list items.</span></span> 
 

 <span data-ttu-id="3a9e5-p105">**Hinweis** Sie können mit Napa nur von SharePoint gehostete SharePoint-Add-Ins erstellen, keine vom Anbieter gehosteten. Informationen zu den Unterschieden finden Sie unter [SharePoint-Add-Ins](sharepoint-add-ins.md). Sie können in Napa nicht die Aktualisierungssemantik für SharePoint-Add-Ins verwenden, die in [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md) beschrieben wird. Wenn Sie also ein in Napa erstelltes Add-In aktualisieren müssen, müssen Sie es zuerst in Visual Studio exportieren. Anweisungen hierzu finden Sie weiter unten in diesem Artikel. Sie können auch mit Visual Studio ein SharePoint-Add-In erstellen. Weitere Informationen finden Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p105">**Note**  You can create only SharePoint-hosted SharePoint Add-ins with Napa, not provider-hosted. For information on the differences, see  [SharePoint Add-ins](sharepoint-add-ins.md).You cannot use SharePoint's add-in updating semantics, which is described in  [Update add-in web components in SharePoint](update-add-in-web-components-in-sharepoint.md), in Napa. So if you need to update an add-in created in Napa, you first have to export it to Visual Studio. Instructions for doing so are later in this article.You can also create a SharePoint Add-in by using Visual Studio. For more information, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>
 


## <a name="optionally-get-an-office-365-developer-site"></a><span data-ttu-id="3a9e5-122">Optional eine Office 365-Entwicklerwebsite erwerben</span><span class="sxs-lookup"><span data-stu-id="3a9e5-122">Optionally, get an Office 365 Developer Site</span></span>
<span data-ttu-id="3a9e5-123"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-123"></span></span>

<span data-ttu-id="3a9e5-p106">Wenn Sie noch kein SharePoint Online-Abonnement haben, das Sie für die Entwickung verwenden können, erwerben Sie eins mithilfe der Informationen in diesem Abschnitt. Fahren Sie andernfalls mit  [Installieren von Napa](#Overview) fort.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p106">If you don't already have a SharePoint Online subscription that you can use for development, use this section to get one. Otherwise, skip to  [Install Napa](#Overview).</span></span>
 

 

 <span data-ttu-id="3a9e5-p107">**Hinweis** Sie haben möglicherweise bereits Zugriff auf eine Office 365-Entwicklerwebsite: **Sind Sie MSDN-Abonnent?** Visual Studio Ultimate und Visual Studio Premium mit MSDN-Abonnenten erhalten ein Office 365-Entwicklerabonnement als Vorteil. [Lösen Sie Ihren Vorteil noch heute ein. ](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Haben Sie einen der folgenden Office 365-Abonnementpläne?** **Wenn ja, kann ein Administrator des Office 365-Abonnements eine Entwicklerwebsite erstellen**, und zwar im [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx). Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p107">**Note**   You might already have access to an Office 365 Developer Site: **Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more information, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 
 

<span data-ttu-id="3a9e5-132">Es gibt zwei Wege zu einem Office 365-Plan.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-132">Two ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="3a9e5-133">Beginnen Sie mit einer [kostenlosen 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) mit einer Benutzerlizenz.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-133">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="3a9e5-134">Erwerben Sie ein [Office 365 Developer-Abonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-134">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="3a9e5-135">**Tipp** Jeder dieser Links wird in einem anderen Fenster oder einer anderen Registerkarte geöffnet, damit die nachfolgenden Anweisungen übersichtlich bleiben.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-135">**Tip**  Each of these links will open in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="3a9e5-136">**Abb. 1. Domänenname der Office 365-Entwicklerwebsite**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-136">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Seite 2 des Registrierungsformulars für das Office 365-Konto](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="3a9e5-p108">Die erste Seite (nicht abgebildet) des Registrierungsformulars ist selbsterklärend. Geben Sie einfach die erforderlichen Informationen zu Ihrer Person an, und wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p108">The first page (not shown) of the signup form is self-explanatory. Just supply the information about yourself that is requested and choose  **Next**.</span></span>
    
 
2. <span data-ttu-id="3a9e5-140">Geben Sie auf der zweiten Seite, die in Abbildung 1 gezeigt ist, eine Benutzer-ID für den Administrator des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="3a9e5-141">Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-141">Create a subdomain of  **.onmicrosoft.com**.</span></span> 
    
    <span data-ttu-id="3a9e5-p109">Nach der Registrierung müssen Sie die resultierenden Anmeldeinformationen (im Format _UserID_@ _IhreDomäne_.onmicrosoft.com) benutzen, um sich auf Ihrer Office 365-Portalwebsite anzumelden, auf der Sie Ihr Konto verwalten. Ihre SharePoint Online-Entwicklerwebsite wird unter Ihrer neuen Domäne **http:// _IhreDomäne_.sharepoint.com** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p109">After signup, you have to use the resulting credentials (in the format  _UserID_@ _yourdomain_.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is provisioned at your new domain:  **http:// _yourdomain_.sharepoint.com**.</span></span>
    
 
4. <span data-ttu-id="3a9e5-p110">Wählen Sie **Weiter** aus, und füllen Sie die letzte Seite des Formulars aus. Wenn Sie eine Telefonnummer bereitstellen, um Ihren Bestätigungscode zu erhalten, können Sie eine Mobil- oder Festnetznummer, aber *keine* VoIP-Nummer (Voice over Internet Protocol) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p110">Choose  **Next** and fill out the final page of the form. If you choose to provide a telephone number to obtain a confirmation code, you can provide a mobile or land line telephone number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="3a9e5-p111">**Hinweis** Wenn Sie beim Versuch, sich bei einem Entwicklerkonto anzumelden, bei einem anderen Microsoft-Konto angemeldet sind, wird möglicherweise die folgende Nachricht angezeigt: „Die eingegebene Benutzer-ID hat leider nicht funktioniert. Sie ist anscheinend nicht gültig. Geben Sie die Benutzer-ID ein, die Ihnen von Ihrem Unternehmen zugewiesen wurde. Ihre Benutzer-ID hat in der Regel das Format *someone@example.com* oder *someone@example.onmicrosoft.com*.“ Wenn diese Meldung angezeigt wird, melden Sie sich von dem Microsoft-Konto ab, das Sie verwendet haben, und versuchen Sie es erneut. Wenn Sie weiterhin die Meldung erhalten, löschen Sie den Browsercache, oder wechseln Sie zu **InPrivate-Browsen**, und füllen Sie dann das Formular aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p111">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might get this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="3a9e5-p112">Nachdem Sie die Registrierung abgeschlossen haben, wird in Ihrem Browser die Office 365-Installationsseite geöffnet. Wählen Sie das Admin-Symbol aus, um die Admin Center-Seite zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p112">After you finish the signup process, your browser will opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="3a9e5-153">**Abb. 2. Office 365 Admin Center-Seite**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-153">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Screenshot mit dem Office 365 Admin Center](../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="3a9e5-p113">Warten Sie, bis der Bereitstellungsprozess für Ihre Entwicklerwebsite abgeschlossen ist. Nach Abschluss der Bereitstellung aktualisieren Sie die Admin Center-Seite im Browser.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p113">You'll have to wait for your Developer Site to finish provisioning. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="3a9e5-p114">Wählen Sie dann links oben den Link **Add-Ins erstellen** aus, um Ihre Website für Entwickler zu öffnen. Sie sollten eine Website wie in Abbildung 3 dargestellt sehen. Auf der Seite wird die Liste **Add-Ins im Test** angezeigt. Damit wird bestätigt, dass die Website mit der Entwicklerwebsitevorlage von SharePoint erstellt wurde. Wird stattdessen eine Teamwebsite angezeigt, warten Sie einige Minuten und starten dann Ihre Website erneut.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p114">Then, choose the  **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. There is an **Add-ins in Testing** list on the page. This confirms that the website was made with SharePoint's Developer Site template. If you see a regular team site instead, wait a few minutes and launch your site again.</span></span>
    
 
3. <span data-ttu-id="3a9e5-p115">Notieren Sie die URL der Website. Diese wird verwendet, wenn Sie SharePoint-Add-Ins-Projekte in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p115">Make a note of the URL of the site. It is used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="3a9e5-164">**Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-164">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Screenshot, auf dem die Entwicklerwebsite-Startseite angezeigt ist](../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="install-napa"></a><span data-ttu-id="3a9e5-166">Installieren von Napa</span><span class="sxs-lookup"><span data-stu-id="3a9e5-166">Install Napa</span></span>
<span data-ttu-id="3a9e5-167"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-167"></span></span>

<span data-ttu-id="3a9e5-p116">Wenn Ihr -Abonnement ursprünglich nicht als eine Website für Office 365-Entwickler erstellt wurde, müssen Sie in der Verwaltungsbenutzeroberfläche des -Abonnements eine Entwicklerwebsite erstellen und dann Napa darin installieren. Anweisungen für das Erstellen der Website finden Sie unter  [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p116">If your subscription was not originally created as a Office 365 Developer Site, then you have to create a Developer Site in the Administration UI of the subscription and then install Napa in it. Instructions for creating the site are in  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
 

 
<span data-ttu-id="3a9e5-p117">Öffnen Sie zum Installieren von Napa Ihre Entwicklerwebsite, und wählen Sie **Websiteinhalte** > **Add-In hinzufügen** > **SharePoint Store** aus. Suchen Sie im Store nachNapa, und installieren Sie das Add-In. (Wenn Sie eine Website für Office 365-Entwickler haben, wurde Napa möglicherweise bereits bei der Erstellung der Website installiert und wird auf der Seite **Websiteinhalte** angezeigt.)</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p117">To install Napa, open your Developer Site and choose  **Site Contents** > **add an add-in** > **SharePoint Store**. In the store, search for Napa and install it. (If you have a Office 365 Developer Site, Napa may have already been installed when the site was created and you will see it on the **Site Contents** page.)</span></span>
 

 

## <a name="create-a-sharepoint-add-in-project"></a><span data-ttu-id="3a9e5-173">Erstellen eines SharePoint-Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="3a9e5-173">Create a SharePoint Add-in project</span></span>
<span data-ttu-id="3a9e5-174"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-174"></span></span>


1. <span data-ttu-id="3a9e5-175">Öffnen Sie das Napa-Add-In auf der Office 365-Seite.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-175">Open the Napa add-in on the Office 365 page.</span></span>
    
 
2. <span data-ttu-id="3a9e5-176">Wählen Sie die Kachel **Neues Projekt hinzufügen** und dann die Kachel **SharePoint-Add-In** aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-176">Choose the  **Add New Project** tile, and then choose the **Add-in for SharePoint** tile.</span></span>
    
 
3. <span data-ttu-id="3a9e5-177">Nennen Sie das Projekt „SharePoint-Add-In-Test“, und klicken Sie dann auf die Schaltfläche **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-177">Name the project Test SharePoint Add-in, and then choose the  **Create** button.</span></span>
    
    <span data-ttu-id="3a9e5-178">Der Code-Editor wird mit der Standardwebsite geöffnet, die bereits etwas Beispielcode enthält, den Sie ohne weiteres Zutun ausführen können.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-178">The code editor opens and shows the default webpage, which already contains some sample code that you can run without doing anything else.</span></span>
    
 

## <a name="add-controls-to-the-home-page"></a><span data-ttu-id="3a9e5-179">Hinzufügen von Steuerelementen zur Homepage</span><span class="sxs-lookup"><span data-stu-id="3a9e5-179">Add controls to the home page</span></span>
<span data-ttu-id="3a9e5-180"><a name="AddControls1"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-180"></span></span>

<span data-ttu-id="3a9e5-p118">Fügen Sie der standardmäßigen Homepage im SharePoint-Add-In Steuerelemente zum Erstellen und Löschen einer generischen SharePoint-Liste und zum Abrufen der aktuellen Anzahl von Listen im Web des SharePoint-Add-Ins hinzu. Den Code für die Steuerelemente fügen Sie später hinzu.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p118">In the SharePoint Add-in, add controls to the default home page for creating and deleting a generic SharePoint list and getting the current number of lists in the web of the SharePoint Add-in. You'll add code for the controls later.</span></span>
 

 

### <a name="to-add-controls-to-the-home-page"></a><span data-ttu-id="3a9e5-183">So fügen Sie der Homepage Steuerelemente hinzu</span><span class="sxs-lookup"><span data-stu-id="3a9e5-183">To add controls to the home page</span></span>


1. <span data-ttu-id="3a9e5-184">Wählen Sie links auf der Seite unter dem Ordner **Seiten** die Seite **Default.aspx** aus, falls diese nicht bereits ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-184">On the left side of the page under the  **Pages** folder, choose the **Default.aspx** page if it isn't already selected.</span></span>
    
    <span data-ttu-id="3a9e5-185">Die Webseite „Default.aspx“ wird im Code-Editor angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-185">The Default.aspx webpage appears in the code editor.</span></span> 
    
 
2. <span data-ttu-id="3a9e5-186">Fügen Sie im Abschnitt `PlaceHolderMain` den folgenden Code unter dem vorhandenen HTML-Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="3a9e5-186">In the  `PlaceHolderMain` section, add this code under the existing HTML</span></span>
    
```HTML
  <br />
<div>
    <button id="getListCount">Get count of lists in web</button>
</div>
<br />
<div id="starter">
    <input type="text" value="List name here" id="createlistbox"/><button id="createlistbutton">Create List</button>
    <p>
    Lists
    <br />
    <select id="selectlistbox" ></select><button id="deletelistbutton">Delete Selected List</button>
    </p>
</div>
```


    The HTML creates these controls.
    
      - A button that gets the number of lists in the web of the SharePoint Add-in.
    
 
  - <span data-ttu-id="3a9e5-187">Eine Schaltfläche zum Erstellen einer generischen SharePoint-Liste und eine weitere Schaltfläche zum Löschen der Liste.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-187">A button for creating a generic SharePoint list and another button for deleting the list.</span></span>
    
 
  - <span data-ttu-id="3a9e5-188">Eine Liste mit den Listen, die in dem Add-In verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-188">A list of lists that are available within the add-in.</span></span>
    
 

## <a name="add-code-for-creating-and-deleting-lists"></a><span data-ttu-id="3a9e5-189">Hinzufügen von Code zum Erstellen und Löschen von Listen</span><span class="sxs-lookup"><span data-stu-id="3a9e5-189">Add code for creating and deleting lists</span></span>
<span data-ttu-id="3a9e5-190"><a name="AddCode1"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-190"></span></span>

<span data-ttu-id="3a9e5-191">In diesem Verfahren fügen Sie JavaScript-Code hinzu, damit Benutzer Listen im SharePoint Add-In erstellen und löschen können.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-191">In this procedure, you'll add some JavaScript code so that users can create and delete lists in the SharePoint Add-in.</span></span>
 

 

### <a name="to-add-code-for-creating-and-deleting-lists"></a><span data-ttu-id="3a9e5-192">So fügen Sie Code zum Erstellen und Löschen von Listen hinzu</span><span class="sxs-lookup"><span data-stu-id="3a9e5-192">To add code for creating and deleting lists</span></span>


1. <span data-ttu-id="3a9e5-193">Wählen Sie den Ordner **Skripts** aus, und klicken Sie dann auf den Link **App.js**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-193">Choose the  **Scripts** folder, and then choose the **App.js** link.</span></span>
    
    <span data-ttu-id="3a9e5-p119">Die standardmäßige JavaScript-Codedatei der Projektvorlage wird für die Bearbeitung geöffnet. Diese Datei enthält den Code, der in Ihrem SharePoint-Add-In verwendet wird. Sie können auch eine andere JS-Datei hinzufügen, in die Sie Code (anstatt in die vorhandene Datei) einfügen. Fügen Sie den Code in diesem Beispiel jedoch in die bereitgestellte Datei **App.js** ein.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p119">The default JavaScript code file from the project template opens for editing. This file contains the code that's used in your SharePoint Add-in. You could add another .js file and add code to it instead of to the existing file. But, for this example, add it to the  **App.js** file that's provided.</span></span>
    
    <span data-ttu-id="3a9e5-198">Im nächsten Schritt definieren Sie die Funktionen für die Steuerelemente, die Sie im vorherigen Verfahren erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-198">In the next step, you'll define the functions for the controls that you created in the previous procedure.</span></span>
    

|<span data-ttu-id="3a9e5-199">**Funktionsname**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-199">**Function Name**</span></span>|<span data-ttu-id="3a9e5-200">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-200">**Description**</span></span>|
|:-----|:-----|
| `getWebProperties()`|<span data-ttu-id="3a9e5-201">Verbunden mit dem **getListCount**-Steuerelement - ruft die Anzahl von Listen im Web ab.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-201">Connected to the  **getListCount** control???retrieves the number of lists in the web.</span></span>|
| `createlist()`|<span data-ttu-id="3a9e5-202">Verbunden mit dem **createListButton**-Steuerelement - erstellt eine generische SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-202">Connected to the  **createListButton** control???creates a generic SharePoint list.</span></span>|
| `deletelist()`|<span data-ttu-id="3a9e5-203">Verbunden mit dem **deletelistbutton**-Steuerelement - löscht die Liste, die Benutzer aus der Liste mit den verfügbaren Listen ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-203">Connected to the  **deletelistbutton** control???deletes the list that the user chose from the list of available lists.</span></span>|

    You'll also call the  `welcome()` and `displayLists()` functions, which this walkthrough will describe later.
    
 
2. <span data-ttu-id="3a9e5-204">Fügen Sie in der Datei **App.js** die Variablen `web`, `lists` und `listItemcollection` zu den beiden Standardvariablen hinzu, und ändern Sie den Code in der Funktion `$(document).ready()` in das folgende Beispiel.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-204">In the  **App.js** file, add the `web`,  `lists`, and  `listItemcollection` variables to the two default variables, and change the code in the `$(document).ready()` function to the following example.</span></span>
    
     <span data-ttu-id="3a9e5-p120">**Hinweis** Im Code werden gewellte Unterstreichungen angezeigt. Diese werden im Laufe der nächsten Schritte ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p120">**Note**  Error squiggles will appear in this code. They'll disappear in later steps.</span></span>

```
  'use strict';

var context = SP.ClientContext.get_current();
var user = context.get_web().get_currentUser();
var web = context.get_web();
var lists = web.get_lists();
var listItemCollection;  // This variable is used later when you add list items.

(function () {

// This code runs when the DOM is ready and creates a context object which is 
// needed to use the SharePoint object model.
$(document).ready(function () {
    getUserName();
    $("#getListCount").click(function (event) {
        getWebProperties();
        event.preventDefault();
    });

    $("#createlistbutton").click(function (event) {
        createlist();
        event.preventDefault();
    });

    $("#deletelistbutton").click(function (event) {
        deletelist();
        event.preventDefault();
    });
        displayLists();
    });

```


    In the next step, you'll add JavaScript functions for the definitions. Each function in the code is executed by calling  `executeQueryAsync()`, which executes the current pending request asynchronously on the server by using the client-side object model (CSOM) for SharePoint. When a function executes asynchronously, your script continues to run without waiting for the server to respond. Each  `executeQueryAsync()` call includes two event handlers. One handler responds if the function runs successfully, and the other handler responds if the function fails. This table describes the main functions.
    

|<span data-ttu-id="3a9e5-207">**Funktionsname**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-207">**Function name**</span></span>|<span data-ttu-id="3a9e5-208">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-208">**Description**</span></span>|
|:-----|:-----|
| `welcome()`|<span data-ttu-id="3a9e5-209">Ruft den aktuellen Webkontextverweis ab und verwendet diesen dann, um die aktuellen Benutzerinformationen in den Kontext einzubinden.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-209">Gets the current web context reference, and then uses it to set the current user information into the context.</span></span>|
| `getWebProperties()`|<span data-ttu-id="3a9e5-210">Ruft die Listensammlung im aktuellen Web ab und gibt dann die Anzahl der Listen zurück.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-210">Gets the collection of lists in the current web and then returns the number of lists.</span></span>|
| `displaylists()`|<span data-ttu-id="3a9e5-p121">Ruft die aktuelle Listensammlung in diesem Web ab. Ist dies erfolgreich, wird mit dieser Funktion der Name der einzelnen Listen in der Sammlung der Liste mit den verfügbaren Listen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p121">Gets the current collection of lists in this web. If successful, this function adds the name of each list in the collection to the list of available lists.</span></span>|
| `createlist()`|<span data-ttu-id="3a9e5-p122">Erstellt eine generische SharePoint-Liste (Listenvorlagentyp **genericList**) und benennt diese mit dem Namen, den Benutzer im **createlistbox**-Steuerelement angeben. Sie können auch andere Arten von Listen erstellen. Weitere Informationen zu den Arten von Listen finden Sie unter [SPListTemplateType Enumeration](http://go.microsoft.com/fwlink/?LinkId=256687).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p122">Creates a generic SharePoint list (list template type  **genericList**) and gives it the name that the user specifies in the  **createlistbox** control. You can create other types of lists. For more information about list types, see [SPListTemplateType Enumeration](http://go.microsoft.com/fwlink/?LinkId=256687).</span></span>|
| `deletelist()`|<span data-ttu-id="3a9e5-216">Löscht die Liste, die Benutzer aus der Liste mit den verfügbaren Listen ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-216">Deletes the list that the user chose from the list of available lists.</span></span>|
3. <span data-ttu-id="3a9e5-217">Fügen Sie den folgenden Code nach der Funktion `onGetUserNameFail()` in **App.js** ein.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-217">Add the following code after the  `onGetUserNameFail()` function in **App.js**.</span></span>
    
```
  function getWebProperties() {
        // Get the number of lists in the current web.
        context.load(lists);
        context.executeQueryAsync(onWebPropsSuccess, onWebPropsFail);
    }

    function onWebPropsSuccess(sender, args) {
        alert('Number of lists in web: ' + lists.get_count());
    }

    function onWebPropsFail(sender, args) {
        alert('Failed to get list. Error: ' + args.get_message());
    }

    function displayLists() {
        // Get the available SharePoint lists, and then set them into 
        // the context.
        lists = web.get_lists();
        context.load(lists);
        context.executeQueryAsync(onGetListsSuccess, onGetListsFail);
    }

    function onGetListsSuccess(sender, args) {
        // Success getting the lists. Set references to the list 
        // elements and the list of available lists.
        var listEnumerator = lists.getEnumerator();
        var selectListBox = document.getElementById("selectlistbox");
        if (selectListBox.hasChildNodes()) {
            while (selectListBox.childNodes.length >= 1) {
                selectListBox.removeChild(selectListBox.firstChild);
            }
        }
        // Traverse the elements of the collection, and load the name of    
        // each list into the dropdown list box.
        while (listEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listEnumerator.get_current().get_title();
            selectOption.innerHTML = listEnumerator.get_current().get_title();
            selectListBox.appendChild(selectOption);
        }
    }

    function onGetListsFail(sender, args) {
        // Lists couldn't be loaded - display error.
        alert('Failed to get list. Error: ' + args.get_message());
    }

function createlist() {
        // Create a generic SharePoint list with the name that the user specifies.
        var listCreationInfo = new SP.ListCreationInformation();
        var listTitle = document.getElementById("createlistbox").value;
        listCreationInfo.set_title(listTitle);
        listCreationInfo.set_templateType(SP.ListTemplateType.genericList);
        lists = web.get_lists();
        var newList = lists.add(listCreationInfo);
        context.load(newList);
        context.executeQueryAsync(onListCreationSuccess, onListCreationFail);
    }

    function onListCreationSuccess() {
        displayLists();
    }

    function onListCreationFail(sender, args) {
        alert('Failed to create the list. ' + args.get_message());
    }

    function deletelist() {
        // Delete the list that the user specifies.
        var selectListBox = document.getElementById("selectlistbox");
        var selectedListTitle = selectListBox.value;
        var selectedList = web.get_lists().getByTitle(selectedListTitle);
        selectedList.deleteObject();
        context.executeQueryAsync(onDeleteListSuccess, onDeleteListFail);
    }

    function onDeleteListSuccess() {
        displayLists();
    }

    function onDeleteListFail(sender, args) {
        alert('Failed to delete the list. ' + args.get_message());
    }
```


## <a name="run-it"></a><span data-ttu-id="3a9e5-218">Führen Sie die App aus!</span><span class="sxs-lookup"><span data-stu-id="3a9e5-218">Run it!</span></span>
<span data-ttu-id="3a9e5-219"><a name="Run1"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-219"></span></span>

<span data-ttu-id="3a9e5-220">Der erste Teil der Benutzeroberfläche und des Codes ist jetzt fertig. Sie sollten das Add-In also ausführen, um zu überprüfen, ob es funktioniert.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-220">The first part of the UI and code is in place, so go ahead and run the add-in to verify whether it works.</span></span>
 

 

### <a name="to-run-the-add-in"></a><span data-ttu-id="3a9e5-221">So führen Sie das Add-In aus</span><span class="sxs-lookup"><span data-stu-id="3a9e5-221">To run the add-in</span></span>


1. <span data-ttu-id="3a9e5-222">Wählen Sie unten auf der Seite die Ausführungsschaltfläche (</span><span class="sxs-lookup"><span data-stu-id="3a9e5-222">At the bottom of the page, choose the run (</span></span>
 
![Schaltfläche "Ausführen"](../images/Apps_NAPA_Run_Button.png)
 
<span data-ttu-id="3a9e5-224">Ausführen).</span><span class="sxs-lookup"><span data-stu-id="3a9e5-224">) button.</span></span>
    
    The add-in is packaged, deployed, and installed on your Office 365 Developer Site.
    
    After installation, the SharePoint Add-in starts. If the add-in doesn't start automatically because, for example, a popup blocker is enabled, choose the add-in link to start the add-in.
    
 
2. <span data-ttu-id="3a9e5-225">Klicken Sie auf den Link **Click here to launch your add-in in a new window**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-225">Choose the  **Click here to launch your add-in in a new window** link.</span></span>
    
    <span data-ttu-id="3a9e5-226">Der Bildschirm für das SharePoint-Add-In wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-226">The screen for the SharePoint Add-in appears.</span></span>
    
 
3. <span data-ttu-id="3a9e5-227">Klicken Sie auf die Schaltfläche **Get count of lists in web**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-227">Choose the  **Get count of lists in web** button.</span></span>
    
    <span data-ttu-id="3a9e5-p123">In einem Dialogfeld wird angegeben, dass das Web für das aktuelle SharePoint-Add-In zwei Listen enthält. (Standardmäßig sind im Web die Listen „Design Gallery" und „Gestaltungsvorlagenkatalog" enthalten.)</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p123">A dialog box specifies that the web for the current SharePoint Add-in contains two lists. (The web contains the Design Gallery and Master Page Gallery lists by default.)</span></span>
    
 
4. <span data-ttu-id="3a9e5-230">Geben Sie im Feld **List name here** den Text „Testliste“ ein, und klicken Sie auf die Schaltfläche **Create List**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-230">In the  **List name here** box, enterTest List, and then choose the  **Create List** button.</span></span>
    
 
5. <span data-ttu-id="3a9e5-231">Öffnen Sie die Liste **Lists**, um zu überprüfen, ob die neue Liste darin enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-231">Open the  **Lists** list to verify that the new list appears in it.</span></span>
    
 
6. <span data-ttu-id="3a9e5-232">Klicken Sie erneut auf die Schaltfläche **Get count of lists in web**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-232">Choose the  **Get count of lists in web** button again.</span></span>
    
    <span data-ttu-id="3a9e5-233">Das Web enthält mit der eben erstellten Liste jetzt drei Listen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-233">The web now contains three lists, including the list that you just created.</span></span>
    
 
7. <span data-ttu-id="3a9e5-234">Wählen Sie in der Liste **Lists** den Eintrag **Testliste** aus, und klicken Sie auf die Schaltfläche **Delete Selected List**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-234">In the  **Lists** list, choose **Test List**, and then choose the  **Delete Selected List** button.</span></span>
    
     <span data-ttu-id="3a9e5-235">Der Eintrag **Testliste** wird aus der Liste mit den verfügbaren Listen entfernt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-235">**Test List** disappears from the list of available lists.</span></span>
    
 
8. <span data-ttu-id="3a9e5-236">Schließen Sie nach Abschluss Ihrer Änderungen das Browserfenster, und klicken Sie dann im Fenster **Launch Add-in** auf die Schaltfläche **Close**, um zum in Bearbeitung befindlichen Projekt zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-236">When you finish, close the browser window, and then choose the  **Close** button in **Launch Add-in** window to return to the project that you were editing.</span></span>
    
 

## <a name="add-code-and-controls-for-adding-and-deleting-list-items"></a><span data-ttu-id="3a9e5-237">Hinzufügen von Code und Steuerelementen zum Hinzufügen und Löschen von Listenelementen</span><span class="sxs-lookup"><span data-stu-id="3a9e5-237">Add code and controls for adding and deleting list items</span></span>
<span data-ttu-id="3a9e5-238"><a name="AddControls2"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-238"></span></span>

<span data-ttu-id="3a9e5-239">Da Benutzer jetzt Listen erstellen und löschen können, können Sie die folgenden Schritte ausführen, um Benutzern das Hinzufügen und Löschen von Listenelementen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-239">Now that users can create and delete lists, you can perform the following steps to enable them to add and delete list items.</span></span>
 

 

### <a name="to-add-code-and-controls-for-adding-and-deleting-list-items"></a><span data-ttu-id="3a9e5-240">So fügen Sie Code und Steuerelemente zum Hinzufügen und Löschen von Listenelementen hinzu</span><span class="sxs-lookup"><span data-stu-id="3a9e5-240">To add code and controls for adding and deleting list items</span></span>


1. <span data-ttu-id="3a9e5-241">Wählen Sie die Datei „Default.aspx“ zur Bearbeitung aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-241">Choose the Default.aspx file to edit it.</span></span>
    
 
2. <span data-ttu-id="3a9e5-242">Fügen Sie unter dem `selectlistbox`-Element den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-242">Under the  `selectlistbox` element, add this code.</span></span>
    
```XML
      <p>
    Items
    <br />
    <input type="text" value="item name here" id="createitembox"/><button id="createitembutton">Create Item</button>
    </p>
    <p>
    <select id="selectitembox"></select> <button id="deleteitembutton">Delete Selected Item</button>
    </p>
```


    This code adds an input box where users can specify the name of an item, a button to add the item to the list, and a button to delete the item from the list.
    
 
3. <span data-ttu-id="3a9e5-243">Wählen Sie die Datei **App.js** zur Bearbeitung aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-243">Choose the  **App.js** file to edit it.</span></span>
    
 
4. <span data-ttu-id="3a9e5-p124">Fügen Sie in der  `$(document).ready()`-Funktion Definitionen für Funktionen hinzu, die aufgerufen werden, wenn Benutzer auf die Schaltflächen **Element erstellen** und **Ausgewähltes Element löschen** klicken. Fügen Sie außerdem einen jQuery-Ereignishandler für das Listenfeld **Listen** hinzu, um sicherzustellen, dass die Listenelemente aktualisiert werden, wenn Sie eine neue Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p124">In the  `$(document).ready()` function, add definitions for functions that are called when the user chooses the **Create Item** and **Delete Selected Item** buttons. Also, add a jQuery event handler for the **Lists** list box to ensure the list items get updated when you select a new list.</span></span>
    
```
  $("#createitembutton").click(function (event) {
            createitem();
            event.preventDefault();
        });

        $("#deleteitembutton").click(function (event) {
            deleteitem();
            event.preventDefault();
        });
    
        // Update the list items dropdown when a new list
        // is selected in the Lists dropdown.
        $("#selectlistbox").change(function (event) {
            getitems();
            event.preventDefault();
        });
```


     **Note**  If the list items aren't displaying when you run the add-in, be sure that the  `displayLists();` statement comes after the previous code.

    In the next step, you'll add JavaScript functions for the new definitions and a support function ( `getItems()`). This table describes what the main functions do.
    

|<span data-ttu-id="3a9e5-246">**Funktionsname**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-246">**Function name**</span></span>|<span data-ttu-id="3a9e5-247">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-247">**Description**</span></span>|
|:-----|:-----|
| `createItem()`|<span data-ttu-id="3a9e5-248">Fügt der vom Benutzer ausgewählten Liste ein Element hinzu und benennt dieses Element mit dem Namen, den der Benutzer im Feld **Items** angibt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-248">Adds an item to the list that the user chooses, and gives that item the name that the user specifies in the  **Items** box.</span></span>|
| `deleteItem()`|<span data-ttu-id="3a9e5-249">Löscht das vom Benutzer ausgewählte Element aus der Liste.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-249">Deletes the item that the user chooses from the list.</span></span>|
| `getItems()`|<span data-ttu-id="3a9e5-250">Ruft die Listensammlung (und die untergeordneten Elemente) der Liste ab, die vom Benutzer ausgewählt wurde.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-250">Retrieves the collection of items (and its children) in the list that the user chooses.</span></span>|
5. <span data-ttu-id="3a9e5-251">Fügen Sie diesen Code am Ende der Datei **App.js** nach der Funktion `onDeleteListFail()` hinzu.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-251">Add this code to bottom of  **App.js**, after the  `onDeleteListFail()` function.</span></span>
    
```
  function createitem() {
    // Retrieve the list that the user chose, and add an item to it.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);

    var listItemCreationInfo = new SP.ListItemCreationInformation();
    var newItem = selectedList.addItem(listItemCreationInfo);
    var listItemTitle = document.getElementById("createitembox").value;
    newItem.set_item('Title', listItemTitle);
    newItem.update();
    context.load(newItem);
    context.executeQueryAsync(onItemCreationSuccess, onItemCreationFail);
}

function onItemCreationSuccess() {
    // Refresh the list of items.
    getitems();
}

function onItemCreationFail(sender, args) {
    // The item couldn't be created - display an error message.
    alert('Failed to create the item. ' + args.get_message());
}

function deleteitem() {
    // Delete the item that the user chose.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);
    var selectItemBox = document.getElementById("selectitembox");
    var selectedItemID = selectItemBox.value;
    var selectedItem = selectedList.getItemById(selectedItemID);
    selectedItem.deleteObject();
    selectedList.update();
    context.load(selectedList);
    context.executeQueryAsync(onDeleteItemSuccess, onDeleteItemFail);
}

function onDeleteItemSuccess() {
    // Refresh the list of items.
    getitems();
}

function onDeleteItemFail(sender, args) {
    // The item couldn't be deleted - display an error message.
    alert('Failed to delete the item. ' + args.get_message());
}

function getitems() {
    // Using a CAML query, get the items in the list that the user chose, and 
    // set the context to the collection of list items.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedList = selectListBox.value;
    var selectedListTitle = web.get_lists().getByTitle(selectedList);  
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml("<View><ViewFields>" +
        "<FieldRef Name='ID' />" +
        "<FieldRef Name='Title' />" +
        "</ViewFields></View>')");
    listItemCollection = selectedListTitle.getItems(camlQuery);
    context.load(listItemCollection, "Include(Title, ID)");
    context.executeQueryAsync(onGetItemsSuccess, onGetItemsFail);
}

function onGetItemsSuccess(sender, args) {
    // The list items were retrieved.
    // Show all child nodes.
    var listItemEnumerator = listItemCollection.getEnumerator();
    var selectItemBox = document.getElementById("selectitembox");
    if (selectItemBox.hasChildNodes()) {
        while (selectItemBox.childNodes.length >= 1) {
     selectItemBox.removeChild(selectItemBox.firstChild);
        }
    }
        while (listItemEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listItemEnumerator.get_current().get_item('ID');
            selectOption.innerHTML = listItemEnumerator.get_current().get_item('Title');
            selectItemBox.appendChild(selectOption);
        }
}

function onGetItemsFail(sender, args) {
    // The list items couldn't be retrieved - display an error message.
    alert('Failed to get items. Error: ' + args.get_message());
}
```


## <a name="run-the-revised-sharepoint-add-in"></a><span data-ttu-id="3a9e5-252">Führen Sie das überarbeitete SharePoint-Add-In aus!</span><span class="sxs-lookup"><span data-stu-id="3a9e5-252">Run the revised SharePoint Add-in!</span></span>
<span data-ttu-id="3a9e5-253"><a name="Run2"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-253"></span></span>

<span data-ttu-id="3a9e5-254">Die gesamte Benutzeroberfläche und der gesamte Code ist jetzt fertig. Sie sollten das Add-In also ausführen, um zu überprüfen, ob es funktioniert.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-254">All of the UI and code is in place, so go ahead and run the add-in to be sure it works.</span></span>
 

 

### <a name="to-run-the-revised-sharepoint-add-in"></a><span data-ttu-id="3a9e5-255">So führen Sie das überarbeitete SharePoint-Add-In aus</span><span class="sxs-lookup"><span data-stu-id="3a9e5-255">To run the revised SharePoint Add-in</span></span>


1. <span data-ttu-id="3a9e5-256">Wählen Sie unten auf der Seite erneut die Schaltfläche **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-256">At the bottom of the page, choose the  **Run** button again.</span></span>
    
 
2. <span data-ttu-id="3a9e5-257">Geben Sie im Feld **List name here** den Text „New Test List“ ein, und klicken Sie auf die Schaltfläche **Create List**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-257">In the  **List name here** box, enterNew Test List, and then choose the  **Create List** button.</span></span>
    
    <span data-ttu-id="3a9e5-258">Die neue Liste wird der Liste **Lists** hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-258">The new list is added to the  **Lists** list.</span></span>
    
 
3. <span data-ttu-id="3a9e5-259">Wählen Sie in der Liste **Lists** die Option **New Test List** aus.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-259">In the  **Lists** list, choose **New Test List**.</span></span>
    
 
4. <span data-ttu-id="3a9e5-260">Geben Sie im Feld **Item name here** den Text „Item 1“ ein, und klicken Sie auf die Schaltfläche **Create Item**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-260">In the  **Item name here** box, enterItem 1, and then choose the  **Create Item** button.</span></span>
    
    <span data-ttu-id="3a9e5-261">Das neue Listenelement wird in der Liste **Items** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-261">The new list item appears in the  **Items** list.</span></span>
    
 
5. <span data-ttu-id="3a9e5-262">Wiederholen Sie den vorherigen Schritt, um „Item 2“ und „Item 3“ hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-262">Repeat the previous step to add Item 2 andItem 3.</span></span>
    
 
6. <span data-ttu-id="3a9e5-263">Wählen Sie in der Liste mit den Elementen die Option **Item 2** aus, und klicken Sie auf die Schaltfläche **Delete Selected Item**.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-263">In the list of items, choose  **Item 2**, and then choose the  **Delete Selected Item** button.</span></span>
    
     <span data-ttu-id="3a9e5-264">**Item 2** wird aus der Liste mit den Elementen entfernt.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-264">**Item 2** disappears from the list of items.</span></span>
    
 
7. <span data-ttu-id="3a9e5-265">Schließen Sie das Browserfenster, wenn Sie fertig sind.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-265">When you finish, close the browser window.</span></span>
    
 

## <a name="export-the-project-to-visual-studio"></a><span data-ttu-id="3a9e5-266">Exportieren des Projekts in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a9e5-266">Export the project to Visual Studio</span></span>
<span data-ttu-id="3a9e5-267"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-267"></span></span>

<span data-ttu-id="3a9e5-p125">Öffnen Sie das Projekt in Visual Studio, indem Sie die Schaltfläche **In Visual Studio öffnen** auswählen, wie in Abbildung 3 dargestellt. Napa installiert automatisch die erforderlichen Tools und öffnet Ihr Projekt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a9e5-p125">Open your project in Visual Studio by choosing the  **Open in Visual Studio** button, as shown in Figure 3. Napa automatically installs the necessary tools and opens your project in Visual Studio.</span></span>
 

 

<span data-ttu-id="3a9e5-270">**Abbildung 3: Schaltfläche „In Visual Studio öffnen“**</span><span class="sxs-lookup"><span data-stu-id="3a9e5-270">**Figure 3. The Open in Visual Studio button**</span></span>

 

 
![Schaltfläche „In Visual Studio öffnen“](../images/Apps_Napa_OpenInVS.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="3a9e5-272">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3a9e5-272">Additional resources</span></span>
<span data-ttu-id="3a9e5-273"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="3a9e5-273"></span></span>


-  [<span data-ttu-id="3a9e5-274">Übersicht über die SharePoint-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="3a9e5-274">SharePoint development overview</span></span>](http://msdn.microsoft.com/library/f86e2695-4d7a-4fc5-bc23-689de96c4b06%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="3a9e5-275">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="3a9e5-275">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 

