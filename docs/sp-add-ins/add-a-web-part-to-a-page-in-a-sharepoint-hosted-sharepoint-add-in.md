# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="84a3a-101">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="84a3a-101">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="84a3a-102">Erfahren Sie, wie Sie Webparts auf einer Seite in einem SharePoint-Add-In einfügen.</span><span class="sxs-lookup"><span data-stu-id="84a3a-102">Learn how to include Web Parts in a page in an spappplural.</span></span>
 

 <span data-ttu-id="84a3a-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="84a3a-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="84a3a-p102">Dies ist der fünfte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-In. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="84a3a-p102">This is the fifth in a series of articles about the basics of developing SharePoint-hosted spappplural. You should first be familiar with SharePoint Add-ins and the earlier articles in this series:</span></span>
 

-  [<span data-ttu-id="84a3a-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="84a3a-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="84a3a-109">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="84a3a-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="84a3a-110">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="84a3a-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="84a3a-111">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="84a3a-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 

 <span data-ttu-id="84a3a-p103">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeWebPart.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeWebPart.sln file.</span></span>
 

<span data-ttu-id="84a3a-114">In diesem Artikel fügen Sie der Standardseite des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ ein Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="84a3a-114">In this article you add a Web Part to the default page of the Employee Orientation SharePoint Add-in.</span></span>
 

## <a name="add-a-web-part-to-a-page"></a><span data-ttu-id="84a3a-115">Hinzufügen eines Webparts zu einer Seite</span><span class="sxs-lookup"><span data-stu-id="84a3a-115">Add a Web Part to a page</span></span>


 

 

1. <span data-ttu-id="84a3a-116">Öffnen Sie im **Projektmappen-Explorer** die Datei „Default.aspx“.</span><span class="sxs-lookup"><span data-stu-id="84a3a-116">In  **Solution Explorer**, open the Default.aspx file.</span></span> 
    
 
2. <span data-ttu-id="84a3a-p104">Wir fügen ein Listenansicht-Webpart zu der Seite hinzu, auf der die Liste Neue Mitarbeiter in Seattle angezeigt wird, damit kein Link zur Listenansichtsseite für die Liste mehr erforderlich ist. Entfernen Sie das Element **<asp:HyperLink>** aus dem Element **<asp:Content>**, dessen **ContentPlaceHolderId** `PlaceHolderMain` lautet.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p104">We'll be adding a list view Web Part to the page that surfaces the New Employees in Seattle list, so there's no longer a need to have a link to the list view page for the list. Remove the **<asp:HyperLink>** element from the **<asp:Content>** element whose **ContentPlaceHolderId** is `PlaceHolderMain`.</span></span> 
    
 
3. <span data-ttu-id="84a3a-119">Fügen Sie innerhalb desselben **<asp:Content>**-Elements die folgende **WebPartZone** hinzu.</span><span class="sxs-lookup"><span data-stu-id="84a3a-119">Inside the same  **<asp:Content>** element, add the following **WebPartZone**.</span></span> 
    
```XML
  <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
      ID="HomePage1" Title="loc:full" />

```

4. <span data-ttu-id="84a3a-120">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="84a3a-120">Save and close the file.</span></span>
    
 
5. <span data-ttu-id="84a3a-121">Öffnen Sie im **Projektmappen-Explorer** die Datei „elements.xml“ für die Seite im Knoten **Seiten**.</span><span class="sxs-lookup"><span data-stu-id="84a3a-121">In  **Solution Explorer**, open the elements.xml file for the page in the  **Pages** node.</span></span>
    
 
6. <span data-ttu-id="84a3a-122">Wenn das Element **File** selbstschließend ist, entfernen Sie das Zeichen „/“ daraus, und fügen Sie das Endetag `</File>` hinzu.</span><span class="sxs-lookup"><span data-stu-id="84a3a-122">If the  **File** element is self-closing, remove the "/" character from it and add the end tag `</File>`.</span></span>
    
 
7. <span data-ttu-id="84a3a-p105">Fügen Sie im Element **File** ein untergeordnetes **AllUsersWebPart**-Element hinzu, und legen Sie dessen **WebPartZoneID** auf die ID der Webpartzone fest, die Sie auf der Seite erstellt haben. Der Inhalt der Datei sollte nun wie folgt aussehen. Dieses Markup weist SharePoint an, ein **AllUsersWebPart** in der Webpartzone namens „HomePage1" einzufügen.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p105">In the  **File** element, add a child **AllUsersWebPart** element and set its **WebPartZoneID** to the ID of the Web Part zone that you created on the page. The file's contents should now look like the following. This markup tells SharePoint to insert an **AllUsersWebPart** into the Web Part zone that is named "HomePage1".</span></span>
    
```
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <Module Name="Pages">
    <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
      <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

      </AllUsersWebPart>
    </File>
  </Module>
</Elements>

```

8. <span data-ttu-id="84a3a-126">Fügen Sie ein **CDATA**-Element als untergeordnetes Element von **AllUsersWebPart** hinzu, und fügen Sie dann ein **webParts**-Element als untergeordnetes Element von **CDATA** hinzu, wie im folgenden Markup gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84a3a-126">Add a  **CDATA** element as a child of the **AllUsersWebPart**, then add a  **webParts** element as a child of the **CDATA**, as shown in the following markup.</span></span> 
    
```
  <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
  <![CDATA[
    <webParts>

    </webParts>
  ]]>
</AllUsersWebPart>
```

9. <span data-ttu-id="84a3a-p106">Fügen Sie das folgende **webPart**-Markup als untergeordnetes Element des Elements **webParts** hinzu. Dieses Markup fügt ein **XsltListViewWebPart** hinzu und weist das Webpart an, die ListeNeue Mitarbeiter in Seattle anzuzeigen. Beachten Sie, dass der Eigenschaftswert **ViewContentTypeId** nur „0x" und nicht die tatsächliche ID des InhaltstypsNewEmployee ist.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p106">Add the following  **webPart** markup as a child of the **webParts** element. This markup adds an **XsltListViewWebPart** and tells the Web Part to show theNew Employees in Seattle list. Note that the **ViewContentTypeId** property value is just "0x", not the actual ID of theNewEmployee content type.</span></span>
    
```
  
  <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
    <metaData>
      <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                   Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                   PublicKeyToken=71e9bce111e9429c" />
    </metaData>
    <data>
      <properties>
        <property name="ListUrl">Lists/NewEmployeesInSeattle</property>
        <property name="IsIncluded">True</property>
        <property name="NoDefaultStyle">True</property>
        <property name="Title">New Employees in Seattle</property>
        <property name="PageType">PAGE_NORMALVIEW</property>
        <property name="Default">False</property>
        <property name="ViewContentTypeId">0x</property>
      </properties>
    </data>
  </webPart>
```


## <a name="run-and-test-the-add-in"></a><span data-ttu-id="84a3a-130">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="84a3a-130">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="84a3a-p107">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p107">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
2. <span data-ttu-id="84a3a-133">Wenn die Standardseite des Add-Ins geöffnet wird, enthält sie das Listenansicht-Webpart, und die Liste wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="84a3a-133">When the add-in's default page opens, the list view Web Part is on it and the list is displayed.</span></span> 
    
    <span data-ttu-id="84a3a-134">**Standardseite mit Listenansicht-Webpart**</span><span class="sxs-lookup"><span data-stu-id="84a3a-134">**Default page with list view Web part**</span></span>

 

     ![Standardseite des Add-Ins mit Anzeige der Liste „Neue Mitarbeiter in Seattle“ in einem Webpart](../../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)
 

    
    
 
3. <span data-ttu-id="84a3a-136">Versuchen Sie, der Liste neue Elemente hinzuzufügen und vorhandene Elemente zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="84a3a-136">Try adding new items to the list and editing existing items.</span></span>
    
 
4. <span data-ttu-id="84a3a-p108">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p108">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="84a3a-p109">Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="84a3a-p109">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="84a3a-141"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="84a3a-141"></span></span>

<span data-ttu-id="84a3a-142">Im nächsten Artikel dieser Reihe fügen Sie dem SharePoint-Add-In einen Workflow hinzu: [Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="84a3a-142">In the next article in this series, you'll add a workflow to the SharePoint Add-in:  [Add a workflow to a SharePoint-hosted SharePoint Add-in](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in).</span></span>
 

 

