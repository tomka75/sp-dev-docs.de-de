---
title: "Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In"
description: "Fügen Sie ein Webpart zu einer Seite hinzu, führen Sie das Add-In aus und testen Sie es."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 335e68f24e7bc4ba9bd8a7777b48473542e8fc26
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="c6256-103">Hinzufügen eines Webparts zu einer Seite in einem in SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="c6256-103">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="c6256-104">Dies ist der fünfte einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps) finden.</span><span class="sxs-lookup"><span data-stu-id="c6256-104">This is the fifth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="c6256-105">Wenn Sie unsere Artikelreihe zum Thema SharePoint-gehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c6256-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="c6256-106">Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeWebPart.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="c6256-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeWebPart.sln file.</span></span>

<span data-ttu-id="c6256-107">In diesem Artikel fügen Sie der Standardseite des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ ein Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="c6256-107">In this article, you add a Web Part to the default page of the Employee Orientation SharePoint Add-in.</span></span>

## <a name="add-a-web-part-to-a-page"></a><span data-ttu-id="c6256-108">Hinzufügen eines Webparts zu einer Seite</span><span class="sxs-lookup"><span data-stu-id="c6256-108">Add a Web Part to a page</span></span>

1. <span data-ttu-id="c6256-109">Öffnen Sie im **Projektmappen-Explorer** die Datei „Default.aspx“.</span><span class="sxs-lookup"><span data-stu-id="c6256-109">In **Solution Explorer**, open the Default.aspx file.</span></span> 

2. <span data-ttu-id="c6256-110">Da wir einen Listenansicht-Webpart zu der Seite hinzufügen, das die Liste „Neue Mitarbeiter in Seattle“ berücksichtigt, benötigen wir keinen Link zu der Seite „Listenansicht“ für die Liste.</span><span class="sxs-lookup"><span data-stu-id="c6256-110">Because we'll be adding a list view Web Part to the page that surfaces the New Employees in Seattle list, we no longer need a link to the list view page for the list.</span></span> <span data-ttu-id="c6256-111">Entfernen Sie das Element **<asp: HyperLink>** aus dem Element **<asp:Content>**, dessen **ContentPlaceHolderId** `PlaceHolderMain` ist.</span><span class="sxs-lookup"><span data-stu-id="c6256-111">Remove the **<asp:HyperLink>** element from the **<asp:Content>** element whose **ContentPlaceHolderId** is `PlaceHolderMain`.</span></span> 

3. <span data-ttu-id="c6256-112">Fügen Sie innerhalb desselben **<asp:Content>**-Elements die folgende **WebPartZone** hinzu.</span><span class="sxs-lookup"><span data-stu-id="c6256-112">Inside the same **<asp:Content>** element, add the following **WebPartZone**.</span></span> 
    
    ```XML
      <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
          ID="HomePage1" Title="loc:full" />
    ```

4. <span data-ttu-id="c6256-113">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="c6256-113">Save and close the file.</span></span>

5. <span data-ttu-id="c6256-114">Öffnen Sie im **Projektmappen-Explorer** die Datei „elements.xml“ für die Seite im Knoten **Seiten**.</span><span class="sxs-lookup"><span data-stu-id="c6256-114">In **Solution Explorer**, open the elements.xml file for the page in the **Pages** node.</span></span>

6. <span data-ttu-id="c6256-115">Wenn das Element **File** selbstschließend ist, entfernen Sie das Zeichen „/“ daraus, und fügen Sie das Endetag `</File>` hinzu.</span><span class="sxs-lookup"><span data-stu-id="c6256-115">If the **File** element is self-closing, remove the "/" character from it and add the end tag `</File>`.</span></span>

7. <span data-ttu-id="c6256-116">Fügen Sie im **Datei**-Element ein untergeordnetes **AllUsersWebPart**-Element hinzu, und legen Sie seine **WebPartZoneID** auf die ID der Webpartzone fest, die Sie auf der Seite erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c6256-116">In the **File** element, add a child **AllUsersWebPart** element, and set its **WebPartZoneID** to the ID of the Web Part zone that you created on the page.</span></span> <span data-ttu-id="c6256-117">Die Inhalte der Datei sollten jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="c6256-117">The file's contents should now look like the following.</span></span> <span data-ttu-id="c6256-118">Dieses Markup fordert SharePoint auf, ein **AllUsersWebPart** mit dem Namen „HomePage1“ in die Webpartzone einzufügen.</span><span class="sxs-lookup"><span data-stu-id="c6256-118">This markup tells SharePoint to insert an **AllUsersWebPart** into the Web Part zone that is named "HomePage1".</span></span>
    
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

8. <span data-ttu-id="c6256-119">Fügen Sie ein **CDATA**-Element als untergeordnetes Element von **AllUsersWebPart** hinzu, und fügen Sie dann ein **webParts**-Element als untergeordnetes Element von **CDATA** hinzu, wie im folgenden Markup gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c6256-119">Add a **CDATA** element as a child of the **AllUsersWebPart**, and then add a **webParts** element as a child of the **CDATA**, as shown in the following markup.</span></span> 
    
    ```
    <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
      <![CDATA[
        <webParts>

        </webParts>
      ]]>
    </AllUsersWebPart>
    ```

9. <span data-ttu-id="c6256-120">Fügen Sie das folgende **webPart**-Markup als untergeordnetes Element des **webParts**-Elements hinzu.</span><span class="sxs-lookup"><span data-stu-id="c6256-120">Add the following **webPart** markup as a child of the **webParts** element.</span></span> <span data-ttu-id="c6256-121">Dieses Markup fügt ein **XsltListViewWebPart** hinzu und fordert das Webpart auf, die Liste **Neue Mitarbeiter in Seattle** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c6256-121">This markup adds an **XsltListViewWebPart** and tells the Web Part to show the **New Employees in Seattle** list.</span></span> <span data-ttu-id="c6256-122">Beachten Sie, dass der **ViewContentTypeId**-Eigenschaftswert nur `0x` und nicht die tatsächliche ID des **NewEmployee**-Inhaltstyps ist.</span><span class="sxs-lookup"><span data-stu-id="c6256-122">Note that the **ViewContentTypeId** property value is just `0x`, not the actual ID of the **NewEmployee** content type.</span></span>
    
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


## <a name="run-and-test-the-add-in"></a><span data-ttu-id="c6256-123">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c6256-123">Run and test the add-in</span></span>

1. <span data-ttu-id="c6256-p105">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="c6256-p105">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 

2. <span data-ttu-id="c6256-126">Wenn die Standardseite des Add-Ins geöffnet wird, enthält sie das Listenansicht-Webpart, und die Liste wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c6256-126">When the add-in's default page opens, the list view Web Part is on it and the list is displayed.</span></span> 
    
   <span data-ttu-id="c6256-127">*Abbildung 1. Standardseite mit Listenansicht-Webpart*</span><span class="sxs-lookup"><span data-stu-id="c6256-127">*Figure 1. Default page with list view Web part*</span></span>

   ![Standardseite des Add-Ins mit Anzeige der Liste „Neue Mitarbeiter in Seattle“ in einem Webpart](../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)

3. <span data-ttu-id="c6256-129">Versuchen Sie, der Liste neue Elemente hinzuzufügen und vorhandene Elemente zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c6256-129">Try adding new items to the list and editing existing items.</span></span>

4. <span data-ttu-id="c6256-p106">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="c6256-p106">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="c6256-132">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="c6256-132">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="c6256-133">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="c6256-133">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6256-134">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c6256-134">Next steps</span></span> 
<span data-ttu-id="c6256-135"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="c6256-135"></span></span>

<span data-ttu-id="c6256-136">Im nächsten Artikel dieser Reihe [fügen Sie einen Workflow zu einem von SharePoint gehosteten SharePoint-Add-In hinzu](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="c6256-136">In the next article in this series, you'll [add a workflow to a SharePoint-hosted SharePoint Add-in](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

