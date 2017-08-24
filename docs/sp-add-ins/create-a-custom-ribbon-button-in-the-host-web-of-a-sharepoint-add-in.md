# <a name="create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in"></a><span data-ttu-id="15423-101">Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="15423-101">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>
<span data-ttu-id="15423-102">Erfahren Sie, wie Sie benutzerdefinierte Menübandschaltflächenbefehle zum Hostweb eines SharePoint-Add-Ins hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="15423-102">Add custom ribbon button commands to the host web of a spappsing.</span></span>
 

 <span data-ttu-id="15423-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="15423-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="15423-p102">Dies ist der neunte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="15423-p102">Add custom ribbon button commands to the host web of a SharePoint Add-in. This is the ninth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="15423-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="15423-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="15423-109">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="15423-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-110">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-111">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-112">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-113">Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-114">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="15423-115">Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint gehostetes SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="15423-115">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in)
    
 

 <span data-ttu-id="15423-p103">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeRibbon.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="15423-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeRibbon.sln file.</span></span>
 

<span data-ttu-id="15423-p104">Alle SharePoint-Add-Ins können von der Seite **Websiteinhalte** des Hostwebs ausgeführt werden, indem Sie auf die Kachel des Add-Ins klicken. Die Funktionalität eines SharePoint-Add-Ins kann auch über benutzerdefinierte Aktionen im Hostweb zur Verfügung gestellt werden, die benutzerdefinierte Menübandschaltflächen oder benutzerdefinierte Menüelemente sind. In diesem Artikel fügen Sie eine Schaltfläche zum Menüband eines Hostwebs hinzu.</span><span class="sxs-lookup"><span data-stu-id="15423-p104">All SharePoint Add-ins can be run from the **Site Contents** page of the host web by clicking the add-in's tile. The functionality of a SharePoint Add-in can also be exposed on the host web through custom actions, which are custom ribbon buttons or custom menu items. In this article you add a button to the ribbon on a host web.</span></span>
 

## <a name="prepare-the-host-web"></a><span data-ttu-id="15423-121">Vorbereiten des Hostwebs</span><span class="sxs-lookup"><span data-stu-id="15423-121">Prepare the host web</span></span>

<span data-ttu-id="15423-p105">Die Schaltfläche wird dem Menüband eines Kalenders im Hostweb hinzugefügt. Führen Sie die folgenden Schritte in der Benutzeroberfläche Ihrer SharePoint-Entwicklerwebsite aus.</span><span class="sxs-lookup"><span data-stu-id="15423-p105">You will add the button to the ribbon of a calendar on the host web. Take the following steps in the UI of your SharePoint developer site.</span></span>
 

 

1. <span data-ttu-id="15423-124">Wählen Sie auf der Startseite der Website **Websiteinhalte** > **Add-In hinzufügen** > **Kalender** aus.</span><span class="sxs-lookup"><span data-stu-id="15423-124">From the home page of the site, choose **Site Contents** > **add and add-in** > **Calendar**.</span></span>
    
 
2. <span data-ttu-id="15423-125">Geben Sie im Dialogfeld **Kalender hinzufügen** „Planung für Orientierung für Mitarbeiter“ in das Feld **Name** ein, und wählen Sie dann **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="15423-125">On the **Adding Calendar** dialog, typeEmployee Orientation Schedule for the **Name**, and then choose **Create**.</span></span>
    
 
3. <span data-ttu-id="15423-126">Wenn der Kalender geöffnet wird, setzen Sie den Cursor auf ein beliebiges Datum, bis der Link **Hinzufügen** auf dem Datum angezeigt wird, und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="15423-126">When the calendar opens, put the cursor on any date until the **Add** link appears on the date, and then click **Add**.</span></span> 
    
 
4. <span data-ttu-id="15423-p106">Geben Sie im Dialogfeld **Planung für Orientierung für Mitarbeiter - neues Element** den Text „Orientierung Cassi Hicks“ in das Feld **Titel** ein. Behalten Sie für die anderen Felder die Standardwerte bei, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="15423-p106">On the **Employee Orientation Schedule - New Item** dialog, typeOrient Cassi Hicks for the **Title**. Leave the other fields at their defaults and click **Save**.</span></span>
    
    <span data-ttu-id="15423-129">Der Kalender sollte ähnlich wie im folgenden Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="15423-129">The calendar should look similar to the following:</span></span>
    

    <span data-ttu-id="15423-130">**Benutzerdefinierter Kalender**</span><span class="sxs-lookup"><span data-stu-id="15423-130">**Custom calendar**</span></span>

 

  ![Ein Kalender namens „Planung für Orientierung für Mitarbeiter“ mit dem Element „Orientierung Cassie Hicks“ am 1. Juni: ](../../images/d2066862-41c1-424d-9bfb-b6c5342bcf2c.PNG)
 

 

 

 

 

 <span data-ttu-id="15423-p107">**Wichtig** Im nächsten Verfahren muss der Kalender in der Benutzeroberfläche von Visual Studio sichtbar sein, was aber nicht der Fall sein wird, wenn Visual Studio geöffnet war, als Sie den Kalender erstellt haben. Bevor Sie fortfahren, schließen Sie Visual Studio, und melden Sie sich auch von allen Browserfenstern und PowerShell-Konsolen ab, mit denen Sie bei Ihrer Entwicklerwebsite angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="15423-p107">**Important** The next procedure requires that the calendar be visible in the UI of Visual Studio, but it won't be if If Visual Studio was open when you created the calendar. Before you continue, close Visual Studio and also log out of any browser windows and PowerShell consoles where you are logged into your developer site.</span></span>
 


## <a name="add-a-ribbon-custom-action"></a><span data-ttu-id="15423-134">Hinzufügen einer benutzerdefinierten Menübandaktion</span><span class="sxs-lookup"><span data-stu-id="15423-134">Add a ribbon custom action</span></span>


1. <span data-ttu-id="15423-p108">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt **EmployeeOrientation**, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menübandaktion** aus. Nennen Sie sie „RunOrientationAdd-in“, und wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="15423-p108">In **Solution Explorer**, right-click the **EmployeeOrientation** project, and choose **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**. Name it RunOrientationAdd-in, and then choose **Add**.</span></span>
    
 
2. <span data-ttu-id="15423-p109">Der Assistent **Benutzerdefinierte Aktion für das Menüband erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:</span><span class="sxs-lookup"><span data-stu-id="15423-p109">The **Create Custom Action for Ribbon** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    

|<span data-ttu-id="15423-139">**Frage zur Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="15423-139">**Property question**</span></span>|<span data-ttu-id="15423-140">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="15423-140">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="15423-141">Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?</span><span class="sxs-lookup"><span data-stu-id="15423-141">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="15423-142">Wählen Sie **Hostweb**.</span><span class="sxs-lookup"><span data-stu-id="15423-142">Choose **Host Web**.</span></span>|
|<span data-ttu-id="15423-143">Wo gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="15423-143">Where is the custom action scoped to?</span></span>|<span data-ttu-id="15423-144">Wählen Sie **Listeninstanz** ( *nicht* Listenvorlage) aus.</span><span class="sxs-lookup"><span data-stu-id="15423-144">Choose **List Instance** ( *not*  List Template).</span></span>|
|<span data-ttu-id="15423-145">Für welches spezielle Element gilt die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="15423-145">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="15423-146">Wählen Sie **Planung für Orientierung für Mitarbeiter** aus.</span><span class="sxs-lookup"><span data-stu-id="15423-146">Choose **Employee Orientation Schedule**.</span></span>|
|<span data-ttu-id="15423-147">Wo befindet sich das Steuerelement?</span><span class="sxs-lookup"><span data-stu-id="15423-147">Where is the control located?</span></span>|<span data-ttu-id="15423-p110">Verwenden Sie nicht die Dropdownauswahl. Geben Sie stattdessen **Ribbon.Calendar.Events.Actions.Controls._children** ein. (Der dritte Teil, **Events**, identifiziert die Registerkarte des Menübands, und der vierte Teil, **Actions**, die Schaltflächengruppe.) </span><span class="sxs-lookup"><span data-stu-id="15423-p110">Do not use the drop down selections. Instead, type **Ribbon.Calendar.Events.Actions.Controls._children**. (The third part, **Events**, identifies the tab of the ribbon, and the fourth part, **Actions**, identifies the button group.)</span></span>|
|<span data-ttu-id="15423-151">Wie lautet der Text im Menüelement?</span><span class="sxs-lookup"><span data-stu-id="15423-151">What is the text on the menu item?</span></span>|<span data-ttu-id="15423-152">Geben Sie **Orientierung für Mitarbeiter** ein.</span><span class="sxs-lookup"><span data-stu-id="15423-152">Type **Employee Orientation**.</span></span>|
|<span data-ttu-id="15423-153">Wohin navigiert die benutzerdefinierte Aktion?</span><span class="sxs-lookup"><span data-stu-id="15423-153">Where does the custom action navigate to?</span></span>|<span data-ttu-id="15423-p111">Verwenden Sie nicht die Dropdownauswahlen. Geben Sie stattdessen **~appWebUrl/Lists/NewEmployeesInSeattle** ein. Dies ist die Seite mit der Listenansicht für die Liste, die sich im Add-In-Web befindet, damit die Menübandschaltfläche im Hostweb eine Seite im Add-In-Web öffnet.</span><span class="sxs-lookup"><span data-stu-id="15423-p111">Do not use the drop down selections. Instead, type **~appWebUrl/Lists/NewEmployeesInSeattle**. This is the list view page for the list, which is on the add-in web, so the ribbon button on the host web opens a page on the add-in web.</span></span>|
3. <span data-ttu-id="15423-157">Wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="15423-157">Choose **Finish**.</span></span> 
    
 

## <a name="inspect-the-add-in-web-feature"></a><span data-ttu-id="15423-158">Überprüfen des Add-In-Web-Features</span><span class="sxs-lookup"><span data-stu-id="15423-158">Inspect the add-in web Feature</span></span>

<span data-ttu-id="15423-p112">Erweitern Sie im **Projektmappen-Explorer** den Ordner **Features**, und wählen Sie das Feature **NewEmployeeOrientationComponents** aus. Der Feature-Designer wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="15423-p112">In **Solution Explorer**, expand the **Features** folder and choose the **NewEmployeeOrientationComponents** feature. The Feature designer opens.</span></span>
 

 
<span data-ttu-id="15423-p113">Beachten Sie, dass die benutzerdefinierte Aktion, die Sie erstellt haben, **RunOrientationAdd-in**, in **Elemente in der Lösung**, jedoch nicht in **Elemente im Feature** aufgelistet wird. Der Grund dafür ist, dass das Feature an das Add-In-Web, Ihre benutzerdefinierte Aktion aber an das Hostweb bereitgestellt wird. Wenn Sie das Add-In in Visual Studio zur Bereitstellung für die Produktion packen oder F5 in Visual Studio drücken, erstellen die Office Developer Tools für Visual Studio ein spezielles Hostwebfeature, fügen die benutzerdefinierte Aktion hinzu und stellen sie an das Hostweb bereit. Sie sollten das Hostwebfeature niemals bearbeiten. Darum wird es erst zum Zeitpunkt des Packens erstellt.</span><span class="sxs-lookup"><span data-stu-id="15423-p113">Notice that the custom action that you created, **RunOrientationAdd-in**, is listed in **Items in the solution**, but not in **Items in the feature**. This is because the Feature is deployed to the add-in web, but your custom action is deployed to the host web. When you package the add-in in Visual Studio for deployment to production, or when you press F5 in Visual Studio, the Office Developer Tools for Visual Studio creates a special host web Feature, adds the custom action to it, and deploys it to the host web. You should never edit the host web Feature. That is why it is not created until packaging-time.</span></span>
 

 

<span data-ttu-id="15423-166">**Feature-Designer**</span><span class="sxs-lookup"><span data-stu-id="15423-166">**Feature designer**</span></span>

 

 
![Der Feature-Designer mit Spalten namens "Elemente in der Lösung" und "Elemente in der Funktion". Das Element "Orientierungs-Add-In ausführen" befindet sich in der ersten, nicht in der zweiten.](../../images/49ea0bf0-2cfa-4070-aa65-24b4a9c5e874.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="15423-169">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="15423-169">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="15423-p115">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="15423-p115">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
2. <span data-ttu-id="15423-p116">Die Standardseite des SharePoint-Add-Ins wird geöffnet. Navigieren Sie zur Startseite Ihrer Entwicklerwebsite (die das Hostweb ist). In der linken oberen Ecke der Seite finden Sie einen Breadcrumblink dahin.</span><span class="sxs-lookup"><span data-stu-id="15423-p116">The default page of the SharePoint Add-in opens. Navigate to the home page of your developer site (which is the host web). There is a breadcrumb link to it in the upper left of the page.</span></span>
    
 
3. <span data-ttu-id="15423-175">Wählen Sie auf der Startseite des Hostwebs **Websiteinhalte**, und klicken Sie auf der Seite **Websiteinhalte** auf den Kalender **Planung für Orientierung für Mitarbeiter**(nicht das Add-In **Orientierung für Mitarbeiter**).</span><span class="sxs-lookup"><span data-stu-id="15423-175">On the host web's home page, choose **Site Contents**, and on the **Site Contents** page, click the **Employee Orientation Schedule** calendar (not the **Employee Orientation** add-in).</span></span>
    
 
4. <span data-ttu-id="15423-p117">Wenn der Kalender geöffnet wird, klicken Sie auf das Ereignis **Orientierung Cassie Hicks**. Wenn die Registerkarte **Ereignisse** im Menüband nicht automatisch geöffnet wird, öffnen Sie sie manuell. Sie sollte etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="15423-p117">When the calendar opens, click the event **Orient Cassie Hicks**. If the **Events** tab on the ribbon doesn't open automatically, open it. It should look similar to the following:</span></span>
    
    <span data-ttu-id="15423-179">**Menüband-Registerkarte „Ereignisse“ mit benutzerdefinierter Schaltfläche **</span><span class="sxs-lookup"><span data-stu-id="15423-179">**Events ribbon tab with custom button**</span></span>

 

  ![Das Menüband „Ereignisse“ mit einer benutzerdefinierten Schaltfläche namens „Orientierung für Mitarbeiter“](../../images/916ecbba-11ff-45b6-a8e9-ba717ae6fe0b.png)
 

 

 
5. <span data-ttu-id="15423-p118">Klicken Sie in der Gruppe **Aktionen** im Menüband auf **Orientierung für Mitarbeiter**. Die Seite mit der Listenansicht für **Neue Mitarbeiter in Seattle** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="15423-p118">In the **Actions** group on the ribbon, click **Employee Orientation**. The list view page for **New Employees in Seattle** opens.</span></span>
    
 
6. <span data-ttu-id="15423-p119">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="15423-p119">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="15423-p120">Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="15423-p120">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="15423-187"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="15423-187"></span></span>

<span data-ttu-id="15423-188">Im nächsten Artikel dieser Reihe fügen Sie JavaScript zum SharePoint-Add-In hinzu und greifen auf SharePoint-Daten mit dem JavaScript-Objektmodell von SharePoint zu:  [Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data).</span><span class="sxs-lookup"><span data-stu-id="15423-188">In the next article in this series, you'll add JavaScript to the SharePoint Add-in and access SharePoint data with SharePoint's JavaScript object model:  [Use the SharePoint JavaScript APIs to work with SharePoint data](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data).</span></span>
 

 

