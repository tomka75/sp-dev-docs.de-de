---
title: "Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In"
description: "Fügen Sie eine benutzerdefinierte Seite hinzu, fügen Sie eine Formatklasse zu einem Stylesheet hinzu, führen Sie das Add-In aus und testen Sie es."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 7e714fd67261500a80887e49df9b471f3534c4e7
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="0fc81-103">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0fc81-103">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="0fc81-104">Dies ist der siebte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="0fc81-104">This is the seventh in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="0fc81-105">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0fc81-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="0fc81-106">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0fc81-106">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="0fc81-107">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0fc81-107">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="0fc81-108">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0fc81-108">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="0fc81-109">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0fc81-109">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="0fc81-110">Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0fc81-110">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
> [!NOTE]
> <span data-ttu-id="0fc81-111">Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen.</span><span class="sxs-lookup"><span data-stu-id="0fc81-111">Note  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_SP-hosted_Add-Ins_Tutorials and open the BeforeClientRenderedControl.sln file.</span></span> <span data-ttu-id="0fc81-112">Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforePage.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="0fc81-112">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforePage.sln file.</span></span>

<span data-ttu-id="0fc81-113">In diesem Artikel fügen Sie dem SharePoint-Add-In „Orientierung für Mitarbeiter“ eine Hilfeseite hinzu und konfigurieren sie für die Verwendung eines benutzerdefinierten CSS-Stylesheets.</span><span class="sxs-lookup"><span data-stu-id="0fc81-113">In this article you add a help page to the Employee Orientation SharePoint Add-in and configure it to use a custom CSS stylesheet.</span></span> 

## <a name="add-a-page"></a><span data-ttu-id="0fc81-114">Hinzufügen einer Seite</span><span class="sxs-lookup"><span data-stu-id="0fc81-114">Add a page</span></span>

1. <span data-ttu-id="0fc81-115">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Seiten**, und wählen Sie **Neues Element** > **hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="0fc81-115">In  **Solution Explorer**, right-click the  **Pages** folder and choose **Add** > **New Item**. The  Add New Item dialog opens to the Office/SharePoint node.</span></span> <span data-ttu-id="0fc81-116">Das Dialogfeld **Neues Element hinzufügen** wird geöffnet, und der **Office/SharePoint**-Knoten wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0fc81-116">Right-click the new folder and choose  AddNew Item. The  **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

2. <span data-ttu-id="0fc81-117">Wählen Sie **Seite** aus, und weisen Sie den Namen **Help.aspx** zu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-117">Select **Page** and give it the name **Help.aspx**.</span></span> 

3. <span data-ttu-id="0fc81-118">Suchen Sie die beiden **asp:Content**-Elemente in der Datei, und fügen Sie das folgende **asp:Content**-Markup zwischen ihnen hinzu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-118">Find the two  **asp:Content** elements in the file, and add the following third **asp:Content** markup in between them.</span></span>
    
    ```HTML
      <asp:Content ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server">
        Help
      </asp:Content> 
    ```

4. <span data-ttu-id="0fc81-119">Suchen Sie das **asp:Content**-Element mit der ID **PlaceholderAdditionalPageHead**, und fügen Sie ihm das folgende Markup hinzu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-119">Find the  **asp:Content** element with the ID of **PlaceholderAdditionalPageHead**, and add the following markup to it.</span></span>
    
    ```HTML
      <link rel="Stylesheet" type="text/css" href="../Content/App.css" />
    ```

5. <span data-ttu-id="0fc81-120">Suchen Sie das **asp:Content**-Element mit der ID **PlaceHolderMain**, und entfernen Sie alle untergeordneten Elemente.</span><span class="sxs-lookup"><span data-stu-id="0fc81-120">Find the  **asp:Content** element with the ID of **PlaceHolderMain**, and remove any child elements in it.</span></span>

6. <span data-ttu-id="0fc81-121">Fügen Sie demselben **asp:Content**-Element Folgendes als Inhalt hinzu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-121">Add the following as content to the same  **asp:Content** element.</span></span>
    
    ```HTML
      <H3>Having a problem with the add-in?</H3>
      <p>Call the help line for Fabrikam Add-ins:</p>
      <p>1-555-555-5555</p>
    ```

7. <span data-ttu-id="0fc81-122">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="0fc81-122">Save and close the file.</span></span>

8. <span data-ttu-id="0fc81-123">Öffnen Sie die Datei „Default.aspx“.</span><span class="sxs-lookup"><span data-stu-id="0fc81-123">Open the Default.aspx file.</span></span>

9. <span data-ttu-id="0fc81-124">Suchen Sie das **asp:Content**-Element mit der ID **PlaceHolderMain**, und fügen Sie das folgende Markup am Ende hinzu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-124">Find the  **asp:Content** element with the ID of **PlaceHolderMain**, and then add the following markup to the end of it.</span></span> 
    
    ```HTML
      <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Pages/Help.aspx';" 
        Text="Get help for the Employee Orientation add-in" /></p>
    ```

10. <span data-ttu-id="0fc81-125">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="0fc81-125">Save and close the file.</span></span>

## <a name="add-a-style-class-to-the-stylesheet"></a><span data-ttu-id="0fc81-126">Hinzufügen einer Formatklasse zum Stylesheet</span><span class="sxs-lookup"><span data-stu-id="0fc81-126">Add a style class to the stylesheet</span></span>

1. <span data-ttu-id="0fc81-127">Öffnen Sie im **Projektmappen-Explorer** die Datei „app.css“ im Ordner **Inhalt**, und fügen Sie der Datei dann die folgende Zeile hinzu.</span><span class="sxs-lookup"><span data-stu-id="0fc81-127">In  **Solution Explorer**, open the app.css file in the  **Contents** folder, and then add the following line to the file.</span></span>
    
    ```
      p {color: green;}
    ```

2. <span data-ttu-id="0fc81-128">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="0fc81-128">Save and close the file.</span></span>

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="0fc81-129">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0fc81-129">Run and test the add-in</span></span>

1. <span data-ttu-id="0fc81-p103">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="0fc81-p103">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 

2. <span data-ttu-id="0fc81-132">Wenn die Standardseite des Add-Ins geöffnet wird, wählen Sie den Link **Hilfe für das Add-In „Orientierung für Mitarbeiter“** aus, um die Seite **Hilfe** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0fc81-132">When the add-in's default page opens, click the  **Get help for the Employee Orientation add-in** link to open the **Help** page.</span></span>
    
   <span data-ttu-id="0fc81-133">Ihre benutzerdefinierte Seite wird geöffnet, und die beiden Zeilen, die Sie in `<p>`-Tags gesetzt haben, sind grün.</span><span class="sxs-lookup"><span data-stu-id="0fc81-133">Your custom page opens and the two lines that you put in <p> tags are green.</span></span>

   <span data-ttu-id="0fc81-134">*Abbildung 1. Hilfeseite*</span><span class="sxs-lookup"><span data-stu-id="0fc81-134">*Figure 1. Help page*</span></span>

   ![Eine SharePoint-Seite mit dem Titel „Hilfe“. Sie enthält eine Kopfzeile in Schwarz, gefolgt von zwei Textzeilen in Grün.](../images/2df51ab0-5b24-4a37-8b6a-6e95dbb1aeaa.PNG)

3. <span data-ttu-id="0fc81-137">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fc81-137">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="0fc81-138">Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="0fc81-138">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

4. <span data-ttu-id="0fc81-139">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="0fc81-139">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="0fc81-140">Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="0fc81-140">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc81-141">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="0fc81-141">Next steps</span></span>
<span data-ttu-id="0fc81-142"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="0fc81-142"></span></span>

<span data-ttu-id="0fc81-143">Im nächsten Artikel dieser Reihe [fügen Sie benutzerdefiniertes clientseitiges Rendering zu einem in SharePoint gehosteten SharePoint-Add-In hinzu](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="0fc81-143">In the next article in this series, you'll add a custom client-side rendering to a list column in a SharePoint Add-in:  [Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

