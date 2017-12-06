---
title: "Erstellen eines SharePoint-Add-Ins, das eine Dokumentvorlage und ein Aufgabenbereich-Add-In enthält"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 8cda409943bfb30168650d3aaf8118ce4af0faac
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-sharepoint-add-in-that-contains-a-document-template-and-a-task-pane-add-in"></a><span data-ttu-id="fc3b0-102">Erstellen eines SharePoint-Add-Ins, das eine Dokumentvorlage und ein Aufgabenbereich-Add-In enthält</span><span class="sxs-lookup"><span data-stu-id="fc3b0-102">Create a SharePoint Add-in that contains a document template and a task pane add-in</span></span>
<span data-ttu-id="fc3b0-103">Verwenden Sie Visual Studio, um ein Office-Add-In zu entwickeln, das in einem Dokument angezeigt wird, das von einem SharePoint-Add-In geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-103">Use Visual Studio to develop an Office Add-in that appears in a document that is opened from a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="fc3b0-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="fc3b0-p102">Sie können ein SharePoint-Add-In erstellen, das eine Dokumentenvorlage enthält (z. B. eine Spesenabrechnung). Das Dokument kann ein Add-In für den Aufgabenbereich enthalten, das mit SharePoint-Daten interagiert. Beispielsweise können Benutzer die Felder einer Rechnung ausfüllen, indem sie Daten aus den Business Connectivity Services (BCS) verwenden, oder eine Spesenabrechnung erstellen, indem sie eine Spesenkategorie in einer SharePoint-Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p102">You can create a SharePoint Add-in that includes a document template (for example, an expense report). The document can include a task pane add-in that interacts with SharePoint data. For example, users can populate fields of an invoice by using data from the Business Connectivity Services (BCS) or create an expense report by selecting an expense category from a SharePoint list.</span></span>
 

<span data-ttu-id="fc3b0-p103">This walkthrough shows you how to create a SharePoint-Add-In that includes an Excel workbook. The Excel workbook contains a task pane add-in that uses the REST interface provided by SharePoint to populate a drop-down list box with SharePoint date in the task pane add-in.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p103">This walkthrough shows you how to create a SharePoint Add-in that includes an Excel workbook. The Excel workbook contains a task pane add-in that uses the REST interface provided by SharePoint to populate a drop-down list box with SharePoint date in the task pane add-in.</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="fc3b0-112">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="fc3b0-112">Prerequisites</span></span>
<span data-ttu-id="fc3b0-113"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-113"></span></span>

<span data-ttu-id="fc3b0-114">Installieren Sie die folgenden Komponenten, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="fc3b0-114">Install the following components before you get started:</span></span>
 

 

 

 

- <span data-ttu-id="fc3b0-115">Eine SharePoint-Entwicklungsumgebung:</span><span class="sxs-lookup"><span data-stu-id="fc3b0-115">A SharePoint development environment:</span></span>
    
      - <span data-ttu-id="fc3b0-116">To develop SharePoint-Add-Ins that target SharePoint in Office 365, see  [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/de-DE/library/office/apps/fp161179%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-116">To develop SharePoint Add-ins that target SharePoint in Office 365, see  [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/de-DE/library/office/apps/fp161179%28v=office.15%29).</span></span>
    
 
  - <span data-ttu-id="fc3b0-117">Informationen zum Entwickeln von SharePoint-Add-Ins für eine lokale SharePoint-Installation finden Sie unter [Vorgehensweise: Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/de-DE/library/office/apps/fp179923%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-117">To develop SharePoint Add-ins that target an on-premises installation of SharePoint, see  [How to: Set up an on-premises development environment for SharePoint Add-ins](http://msdn.microsoft.com/de-DE/library/office/apps/fp179923%28v=office.15%29).</span></span>
    
 
-  [<span data-ttu-id="fc3b0-118">Visual Studio 2015 und die Microsoft Office Developer Tools</span><span class="sxs-lookup"><span data-stu-id="fc3b0-118">Visual Studio 2015 and the Microsoft Office Developer Tools</span></span>](https://www.visualstudio.com/features/office-tools-vs)
    
 
- <span data-ttu-id="fc3b0-119">Excel 2013 oder ein Office 365-Konto.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-119">Excel 2013 or an Office 365 account.</span></span>
    
 

## <a name="create-a-sharepoint-add-in-project-in-visual-studio"></a><span data-ttu-id="fc3b0-120">Erstellen eines SharePoint-Add-In-Projekts in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc3b0-120">Create a SharePoint Add-in project in Visual Studio</span></span>
<span data-ttu-id="fc3b0-121"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-121"></span></span>


1. <span data-ttu-id="fc3b0-122">Starten Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-122">Start Visual Studio.</span></span>
    
 
2. <span data-ttu-id="fc3b0-123">Wählen Sie auf der Menüleiste die Optionen  **Datei**,  **Neu**,  **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-123">On the menu bar, choose  **File**,  **New**,  **Project**.</span></span>
    
    <span data-ttu-id="fc3b0-124">Das Dialogfeld **Neues Projekt** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-124">The  **New Project** dialog box opens.</span></span>
    
 
3. <span data-ttu-id="fc3b0-125">Erweitern Sie im Vorlagenbereich unter dem Knoten für die gewünschte Sprache  **Office/ SharePoint**, und wählen Sie dann  **Office-Add-Ins** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-125">In the templates pane, under the node for the language you want to use, expand  **Office/SharePoint**, and then choose  **Office Add-ins**.</span></span>
    
 
4. <span data-ttu-id="fc3b0-126">Wählen Sie in der Liste der Projekttypen die Option  **SharePoint-Add-In** aus, benennen Sie das ProjektOfficeEnabledAddin, und wählen Sie dann die Schaltfläche  **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-126">In the list of project types, choose  **SharePoint Add-in**, name the project OfficeEnabledAddin, and then choose the  **OK** button.</span></span>
    
    <span data-ttu-id="fc3b0-127">Das Dialogfeld **Neues SharePoint-Add-In** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-127">The  **New SharePoint Add-in** dialog box appears.</span></span>
    
 
5. <span data-ttu-id="fc3b0-128">Wählen Sie in der Dropdownliste  **Welche SharePoint-Website soll für das Debugging Ihres Add-Ins verwendet werden?** die URL einer SharePoint-Website aus, oder geben Sie eine ein.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-128">In the  **What SharePoint site do you want to use for debugging your add-in?** drop-down list, choose or enter the URL of a SharePoint site.</span></span>
    
 
6. <span data-ttu-id="fc3b0-129">Wählen Sie in der Dropdownliste  **Wie soll Ihr SharePoint-Add-In gehostet werden?** die Option **SharePoint-Hosting** und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-129">In the  **How do you want to host your SharePoint Add-in?** drop-down list, choose **SharePoint-hosted** and then choose **Next**.</span></span>
    
     <span data-ttu-id="fc3b0-130">**Hinweis**Dieses Szenario funktioniert nur mit den Optionen „Von SharePoint gehostet“ und „Von Anbieter gehostet“ in der Dropdownliste **Wie soll Ihr SharePoint-Add-In gehostet werden?**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-130">**Note**  This scenario works only with the SharePoint-hosted and provider-hosted options presented in the  **How do you want to host your SharePoint Add-in?** drop-down list.</span></span>
7. <span data-ttu-id="fc3b0-131">Wählen Sie auf der nächsten Seite **SharePoint** aus, und klicken Sie dann auf die Schaltfläche **Fertig stellen**, um das Dialogfeld zu schließen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-131">On the next page, select  **SharePoint** and then choose the **Finish** button to close the dialog box.</span></span>
    
 

## <a name="add-a-task-pane-add-in-item"></a><span data-ttu-id="fc3b0-132">Hinzufügen eines Elements für ein Aufgabenbereich-Add-In</span><span class="sxs-lookup"><span data-stu-id="fc3b0-132">Add a task pane add-in item</span></span>
<span data-ttu-id="fc3b0-133"><a name="Add"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-133"></span></span>

<span data-ttu-id="fc3b0-p104">Fügen Sie dem Projekt als Nächstes ein Office-Add-In hinzu. Sie können ein beliebiges Add-In hinzufügen. In dieser exemplarischen Vorgehensweise haben wir uns für ein Add-In für den Aufgabenbereich entschieden.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p104">Next, add an Office Add-in to the project. You can add any type of add-in that you want. For this walkthrough, we will add a task pane add-in.</span></span>
 

 

1. <span data-ttu-id="fc3b0-137">Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-137">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
2. <span data-ttu-id="fc3b0-138">Wählen Sie im Menü  **Projekt** die Option **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-138">On the  **Project** menu, choose **Add New Item**.</span></span>
    
 
3. <span data-ttu-id="fc3b0-139">Wählen Sie im Menü  **Neues Element hinzufügen** die Option **Office/SharePoint** und dann **Office-Add-In** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-139">In the  **Add New Item** dialog box, select **Office/SharePoint** and then choose **Office Add-in**.</span></span>
    
 
4. <span data-ttu-id="fc3b0-140">Nennen Sie das Add-In für den Aufgabenbereich MyTaskPaneAddin, und wählen Sie dann die Schaltfläche  **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-140">Name the task pane add-in MyTaskPaneAddin, and then choose the  **Add** button.</span></span>
    
    <span data-ttu-id="fc3b0-141">Das Dialogfeld **Add-In für Office erstellen** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-141">The  **Create Add-in for Office** dialog box opens.</span></span>
    
 
5. <span data-ttu-id="fc3b0-p105">Wählen Sie im Dialogfeld  **Add-In für Office erstellen** die Option **Aufgabenbereich** und dann **Weiter**. Deaktivieren Sie auf der nächsten Seite die Kontrollkästchen  **Word** und **PowerPoint**, und wählen Sie dann  **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p105">In the  **Create Add-in for Office** dialog box, select **Task pane** and then choose **Next**. On the next page, clear the  **Word** and **PowerPoint** check boxes, and then choose **Next**.</span></span>
    
 
6. <span data-ttu-id="fc3b0-144">Wählen Sie auf der Seite  **Soll Ihr Office-Add-In in einem neuen Dokument oder in einem vorhandenen Dokument angezeigt werden?** die Option **Neues Dokument erstellen und Add-In einfügen** und dann die Schaltfläche **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-144">In the  **Would you like your Office Add-in to appear in a new document or in an existing document?** page, choose **Create a new document and insert my add-in**, and then choose  **Finish**.</span></span>
    
    <span data-ttu-id="fc3b0-p106">Visual Studio fügt eine Dokumentbibliothek und eine Arbeitsmappenvorlage für die Bibliothek hinzu.  Die Arbeitsmappe beinhaltet ein Add-In für den Aufgabenbereich.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p106">Visual Studio adds a document library and a workbook template for the library. The workbook contains a task pane add-in.</span></span>
    
 

## <a name="add-a-document-library"></a><span data-ttu-id="fc3b0-147">Hinzufügen einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="fc3b0-147">Add a document library</span></span>
<span data-ttu-id="fc3b0-148"><a name="Library"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-148"></span></span>

<span data-ttu-id="fc3b0-149">In diesem Verfahren erstellen Sie eine Dokumentbibliothek und legen die Arbeitsmappe als Standardvorlage für die Dokumentbibliothek fest.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-149">In this procedure, you will add a document library and make the workbook the default template of the document library.</span></span>
 

 

1. <span data-ttu-id="fc3b0-150">Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-150">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
2. <span data-ttu-id="fc3b0-151">Wählen Sie im Menü  **Projekt** die Option **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-151">On the  **Project** menu, choose **Add New Item**.</span></span>
    
 
3. <span data-ttu-id="fc3b0-152">Wählen Sie im Dialogfeld  **Neues Element hinzufügen** die Option **Office/SharePoint** und dann **Liste** aus, nennen Sie die ListeMyDocumentLibrary, und wählen Sie dann die Schaltfläche  **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-152">In the  **Add New Item** dialog box, select **Office/SharePoint**, then choose  **List**, name the list MyDocumentLibrary, and then choose the  **Add** button.</span></span>
    
 
4. <span data-ttu-id="fc3b0-153">Wählen Sie im  **Assistenten zum Anpassen von SharePoint** die Option **Anpassbare Listenvorlage und Listeninstanz erstellen:** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-153">In  **SharePoint Customization Wizard**, select the  **Create a customizable list template and list instance of it** option.</span></span>
    
 
5. <span data-ttu-id="fc3b0-154">Wählen Sie in der Dropdownliste unter dieser Option  **Dokumentbibliothek** aus und klicken Sie anschließend auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-154">In the drop-down list beneath this option, select  **Document Library**, and then choose the  **Next** button.</span></span>
    
 
6. <span data-ttu-id="fc3b0-155">Wählen Sie unter  **Wählen Sie eine Vorlage für diese Dokumentbibliothek aus. Dokumente, die von Benutzern in dieser Bibliothek erstellt werden, basieren auf dieser Vorlageseite.** die Option **Das folgende Dokument als Vorlage für diese Bibliothek verwenden** und dann die Schaltfläche **Durchsuchen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-155">In the  **Choose a template for this document library. Documents that users create in this library will be based on that template** page, choose **Use the following document as the template for this library**, and then choose the  **Browse** button.</span></span>
    
 
7. <span data-ttu-id="fc3b0-156">Öffnen Sie im Dialogfeld  **Öffnen** den Ordner **OfficeDocuments**, und wählen Sie die Datei  **MyTaskPaneApp.xlsx** aus. Wählen Sie anschließend die Schaltfläche **Öffnen** und dann die Schaltfläche **Fertig stellen** aus, und schließen Sie den Listen-Designer.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-156">In the  **Open** dialog box, open the **OfficeDocuments** folder, select the **MyTaskPaneApp.xlsx** file, choose the **Open** button, choose the **Finish** button, and then close the list designer.</span></span>
    
 
8. <span data-ttu-id="fc3b0-157">Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-157">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
9. <span data-ttu-id="fc3b0-158">Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-158">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
10. <span data-ttu-id="fc3b0-159">Wählen Sie im  **Projektmappen-Explorer** die Datei **AppManifest.xml** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-159">In  **Solution Explorer**, choose the  **AppManifest.xml** file.</span></span>
    
 
11. <span data-ttu-id="fc3b0-160">Wählen Sie  **Ansicht** und **Designer** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-160">Choose  **View**,  **Designer**.</span></span>
    
 
12. <span data-ttu-id="fc3b0-p107">Legen Sie im Manifest-Designer den Wert für **Startseite** auf „~appWebUrl/Lists/MyDocumentLibrary“ fest. Dieser wird in den Wert „OfficeEnabledAddin/Lists/MyDocumentLibrary“ konvertiert.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p107">In the manifest designer, set the value of the  **Start page** value to~appWebUrl/Lists/MyDocumentLibrary. This converts to a value of OfficeEnabledAddin/Lists/MyDocumentLibrary.</span></span>
    
     <span data-ttu-id="fc3b0-p108">**Hinweis** Diese URL verweist auf die Dokumentbibliothek. Sie müssen das ~appWebUrl-Token am Anfang von allen URLs in Ihrem Office-Add-In-Manifest verwenden, die auf Elemente innerhalb der Add-In-Website verweist. Weitere Informationen zu URL-Token in einem SharePoint-Add-In Projekt finden Sie unter [URL-Zeichenfolgen und Token in SharePoint-Add-Ins](url-strings-and-tokens-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p108">**Note**  This URL refers to the document library. You must use the ~appWebUrl token at the beginning of any URL in your Office Add-in manifest that refers to items within the add-in web. For more information about URL tokens in a SharePoint Add-in project, see  [URL strings and tokens in SharePoint Add-ins](url-strings-and-tokens-in-sharepoint-add-ins.md).</span></span>
13. <span data-ttu-id="fc3b0-166">Schließen Sie den Manifest-Designer, um die Änderung zu speichern.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-166">Close the manifest designer to save the change.</span></span>
    
 

## <a name="consume-sharepoint-data-in-the-task-pane"></a><span data-ttu-id="fc3b0-167">Verwenden von SharePoint-Daten im Aufgabenbereich</span><span class="sxs-lookup"><span data-stu-id="fc3b0-167">Consume SharePoint data in the task pane</span></span>
<span data-ttu-id="fc3b0-168"><a name="Consume"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-168"></span></span>

<span data-ttu-id="fc3b0-169">In diesem Verfahren zeigen Sie mithilfe der von SharePoint bereitgestellten REST-Schnittstelle eine Liste von Websitebenutzern an.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-169">In this procedure, you'll show a list of site users by using the REST interface provided by SharePoint.</span></span>
 

 
<span data-ttu-id="fc3b0-p109">In diesem Beispiel werden die SharePoint-Listendaten nur angezeigt, aber Sie können diese Art von Daten als Teil eines Dokumentgenehmigungs-Add-ins verwenden. Wenn ein Benutzer einen Namen aus der Liste auswählt, legt Ihr Code den Wert der „Prüfer“-Spalte in einer Dokumentnachverfolgungsliste fest. Ein mit dieser Liste verknüpfter Workflow kann eine Prüfbenachrichtigung an den Benutzer senden. Alternativ können Sie den ausgewählten Namen in den Dokumenteinstellungen speichern. Wenn dann ein Benutzer das Dokument öffnet, können Sie die Steuerelemente ausschließlich im Aufgabenbereich-Add-in anzeigen, wenn der aktuelle Benutzer mit dem in den Dokumenteinstellungen gespeicherten Benutzer übereinstimmt. Weitere Informationen finden Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p109">In this example, the SharePoint list data is only displayed, but you might use this sort of data as part of a document approval add-in. When a user chooses a name from that list, your code sets the value of the reviewer column in a document tracking list. A workflow associated with that list could send a review notification to that user. Alternatively, you might save the selected name to the document settings. Then, when a user opens the document, you could show controls in the task pane add-in only if the current user and the user stored to the document settings are the same. See the following topics for more information:</span></span>
 

 

-  [<span data-ttu-id="fc3b0-176">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="fc3b0-176">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="fc3b0-177">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="fc3b0-177">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
    
 
-  [<span data-ttu-id="fc3b0-178">Beibehalten des Zustands und der Einstellungen von Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-178">Persisting add-in state and settings</span></span>](http://msdn.microsoft.com/library/407df6e8-c237-4d6a-b357-3000fe3de9ff%28Office.15%29.aspx)
    
 

1. <span data-ttu-id="fc3b0-179">Erweitern Sie im  **Projektmappen-Explorer** den Ordner **MyTaskPaneAddin**, erweitern Sie den Ordner  **Home** und wählen Sie dann die Datei „**Home.html** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-179">In  **Solution Explorer**, expand the  **MyTaskPaneAddin** folder, expand the **Home** folder, and then choose the **Home.html** file.</span></span>
    
    <span data-ttu-id="fc3b0-180">Die Datei "Home.html" wird im Code-Editor geöffnet.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-180">The Home.html file opens in the code editor.</span></span>
    
 
2. <span data-ttu-id="fc3b0-181">Fügen Sie den folgenden HTML-Code unter der Schaltfläche  `get-data-from-selection` hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-181">Add the following HTML beneath the  `get-data-from-selection` button.</span></span>
    
```HTML
  <p>Select Reviewer:</p> <select class="select" id="select-reviewer" name="D1"> </select>
```

3. <span data-ttu-id="fc3b0-182">Wählen Sie die Datei  **Home.js**, um Sie im Code-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-182">Choose the  **Home.js** file to open the Home.js file in the code editor.</span></span>
    
 
4. <span data-ttu-id="fc3b0-183">Fügen Sie der Datei Home.js oben die folgenden Deklarationen hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-183">Add the following declarations to the top of the Home.js file.</span></span>
    
```
  var appWebURL; var web;
```

5. <span data-ttu-id="fc3b0-184">Ersetzen Sie die  `Initialize`-Funktion durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-184">Replace the  `Initialize` function with the following code.</span></span>
    
    <span data-ttu-id="fc3b0-185">Dieser Code führt die folgenden Aufgaben aus:</span><span class="sxs-lookup"><span data-stu-id="fc3b0-185">This code performs the following tasks:</span></span>
    
      - <span data-ttu-id="fc3b0-p110">Die Dateien "SP.Runtime.js" und "SP.js" werden mithilfe der  `getScript`-Funktion in jQuery geladen. Nachdem die Dateien geladen wurden, hat das Programm Zugriff auf das JavaScript-Objektmodell für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p110">Loads the SP.Runtime.js and SP.js files by using the  `getScript` function in jQuery. After loading the files, your program has access to the JavaScript object model for SharePoint.</span></span>
    
 
  - <span data-ttu-id="fc3b0-188">Lädt das aktuelle Websiteobjekt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-188">Loads the current website object.</span></span>
    
 
  - <span data-ttu-id="fc3b0-p111">Ruft eine Funktion auf, die alle Benutzer der Website abruft. Sie fügen den Code für diese Funktion im nächsten Schritt hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p111">Calls a function that gets all of the users of the site. You will add the code for that function in the next step.</span></span>
    
 



```JS
   // The initialize function must be run each time a new page is loaded 
   Office.initialize = function (reason) { $(document).ready(function () { app.initialize(); var scriptbase = "/_layouts/15/"; $.getScript(scriptbase + "SP.Runtime.js", function () { $.getScript(scriptbase + "SP.js", function () { getAppWeb(function () { getSPUsers(populateUsersDropDown); }); }); }); function getAppWeb(functionToExecuteOnReady) { var context = SP.ClientContext.get_current(); web = context.get_web(); context.load(web); context.executeQueryAsync(onSuccess, onFailure); function onSuccess() { appWebURL = web.get_url(); functionToExecuteOnReady(); } function onFailure(sender, args) { app.initialize(); app.showNotification("Failed to connect to SharePoint. Error: " + args.get_message()); } } $('#get-data-from-selection').click(getDataFromSelection); }); };
```

6. <span data-ttu-id="fc3b0-191">Fügen Sie der Datei Home.js unten den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-191">Add the following code to the bottom of the Home.js file.</span></span>
    
    <span data-ttu-id="fc3b0-p112">This code obtains a list of website users by using the REST interface provided by SharePoint. Then, this code populates a drop-down list with the name and ID of each user.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p112">This code obtains a list of website users by using the REST interface provided by SharePoint. Then, this code populates a drop-down list with the name and ID of each user.</span></span>
    


```JS
  function getSPUsers(functionToExecuteOnReady) { var url = appWebURL + "/../_api/web/siteUsers"; jQuery.ajax({ url: url, type: "GET", headers: { "ACCEPT": "application/json;odata=verbose" }, success: onSuccess, error: onFailure }); function onSuccess(data) { var results = data.d.results; functionToExecuteOnReady(results); } function onFailure(jaXHR, textStatus, errorThrown) { var error = textStatus + " " + errorThrown; app.showNotification(error); } } function populateUsersDropDown(results) { for (var i = 0; i < results.length; i++) { var IDTemp = results[i].Id; $('#select-reviewer').append("<option value='" + IDTemp + "'>" + results[i].Title + "</option>"); } }
```

7. <span data-ttu-id="fc3b0-194">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü der Datei **AppManifest.xml**, und wählen Sie **Designer anzeigen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-194">In  **Solution Explorer**, open the shortcut menu for the  **AppManifest.xml** file, and then choose **View Designer**.</span></span>
    
 
8. <span data-ttu-id="fc3b0-195">Wählen Sie im Designer die Seite  **Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-195">On the designer, choose the  **Permissions** page.</span></span>
    
 
9. <span data-ttu-id="fc3b0-196">Wählen Sie der Dropdownliste der Spalte  **Bereich** das Element **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-196">From the drop-down list under the  **Scope** column, choose the **Web** item.</span></span>
    
 
10. <span data-ttu-id="fc3b0-197">Wählen Sie in der Dropdownliste der Spalte  **Berechtigung** das Element **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-197">From the drop-down list under the  **Permission** column, choose the **Read** item.</span></span>
    
 

## <a name="debug-the-task-pane-add-in"></a><span data-ttu-id="fc3b0-198">Debuggen des Aufgabenbereich-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-198">Debug the task pane add-in</span></span>
<span data-ttu-id="fc3b0-199"><a name="debug"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-199"></span></span>

<span data-ttu-id="fc3b0-200">Sie können Ihr Aufgabenbereich-Add-in debuggen, indem Sie das Dokument starten oder das SharePoint-Add-In starten und dann ein Dokument aus der Dokumentbibliothek öffnen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-200">You can debug your task pane add-in by starting the document or by starting the SharePoint Add-in, and then opening a document from the document library.</span></span>
 

 

### <a name="debugging-your-task-pane-add-in-by-starting-the-document"></a><span data-ttu-id="fc3b0-201">Debuggen des Aufgabenbereich-Add-ins durch Starten eines Dokuments</span><span class="sxs-lookup"><span data-stu-id="fc3b0-201">Debugging your task pane add-in by starting the document</span></span>


 

 

 <span data-ttu-id="fc3b0-p113">**Hinweis**  Da dieser Vorgang Excel öffnet, funktioniert er nur, wenn Office auf dem System installiert ist. Andernfalls erhalten Sie den Fehler, dass die mit diesem Projekttyp verknüpfte Anwendung nicht auf diesem Rechner installiert ist.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p113">**Note**  Because this procedure opens Excel, it works only when Office is installed on the system. Otherwise, you get an error that the "application associated with this project type isn't installed on this computer."</span></span>
 


1. <span data-ttu-id="fc3b0-204">Öffnen Sie die Datei "Home.js" im Code-Editor und setzen Sie neben der  `getDataFromSelection`-Methode einen Haltepunkt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-204">Open the Home.js file in the code editor, and then set a breakpoint next to the  `getDataFromSelection` method.</span></span>
    
 
2. <span data-ttu-id="fc3b0-205">Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledApp** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-205">In  **Solution Explorer**, choose the  **OfficeEnabledApp** project node.</span></span>
    
 
3. <span data-ttu-id="fc3b0-206">Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-206">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
4. <span data-ttu-id="fc3b0-p114">Wählen Sie im Fenster "Eigenschaften" aus der Dropdownliste  **Startaktion** das Element **Office Desktop Client**. Daraufhin wird eine neue Eigenschaft,  **Startdokument** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p114">In the Properties windows, from the  **Start Action** drop-down list, choose the **Office Desktop Client** item. When you do this, a new property appears, **Start Document**.</span></span>
    
 
5. <span data-ttu-id="fc3b0-209">Wählen Sie in der Dropdownliste  **Startdokument** das Element **OfficeDocuments\TaskPaneApp.xlsx** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-209">From the  **Start Document** drop-down list, choose the **OfficeDocuments\TaskPaneApp.xlsx** item.</span></span>
    
 
6. <span data-ttu-id="fc3b0-210">Wählen Sie im Menü  **Debuggen** die Option **Debuggen starten**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-210">On the  **Debug** menu, choose **Start Debugging**.</span></span>
    
    <span data-ttu-id="fc3b0-p115">Diese Einstellung zeigt die Arbeitsmappe im Aufgabenbereich-Add-in an, wenn das Add-in ausgeführt wird. Die Arbeitsmappe wird geöffnet und das Add-in für den Aufgabenbereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p115">This setting makes the workbook in the task pane add-in appear when the add-in runs. The workbook opens and the task pane add-in appears.</span></span>
    
 
7. <span data-ttu-id="fc3b0-213">Wählen Sie im Aufgabenbereich-Add-in die Dropdownliste  **Prüfer auswählen** aus, um eine Liste der SharePoint-Benutzer anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-213">In the task pane add-in, choose the  **Select Reviewer** drop down list to view a list of SharePoint users.</span></span>
    
 
8. <span data-ttu-id="fc3b0-214">Wählen Sie in der Excel-Arbeitsmappe eine beliebige Zelle aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-214">In the Excel workbook, select any cell.</span></span>
    
 
9. <span data-ttu-id="fc3b0-215">Wählen Sie im Add-in für den Aufgabenbereich die Schaltfläche  **Daten von Auswahl abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-215">In the task pane add-in, choose the  **Get data from selection** button.</span></span>
    
    <span data-ttu-id="fc3b0-216">Die Ausführung wird an dem Haltepunkt unterbrochen, den Sie neben der `getDataFromSelection`-Methode gesetzt haben.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-216">Execution stops at the breakpoint that you set next to the  `getDataFromSelection` method.</span></span>
    
 

### <a name="debugging-your-task-pane-add-in-by-starting-sharepoint"></a><span data-ttu-id="fc3b0-217">Debuggen des Aufgabenbereich-Add-Ins durch Starten von SharePoint</span><span class="sxs-lookup"><span data-stu-id="fc3b0-217">Debugging your task pane add-in by starting SharePoint</span></span>


 

 

 <span data-ttu-id="fc3b0-p116">**Hinweis** Dieser Vorgang öffnet Excel Online. Dies funktioniert nur mit einem Office 365-Konto. Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/de-DE/library/office/apps/fp161179%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p116">**Note**  This procedure opens the Excel Online. It works only when you have an Office 365 account. See  [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/de-DE/library/office/apps/fp161179%28v=office.15%29).</span></span>
 


1. <span data-ttu-id="fc3b0-221">Öffnen Sie die Datei „Home.js“ im Code-Editor, und setzen Sie neben der `getDataFromSelection`-Methode einen Haltepunkt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-221">Open the Home.js file in the code editor, and then set a breakpoint next to the  `getDataFromSelection` method.</span></span>
    
 
2. <span data-ttu-id="fc3b0-222">Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledApp** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-222">In  **Solution Explorer**, choose the  **OfficeEnabledApp** project node.</span></span>
    
 
3. <span data-ttu-id="fc3b0-223">Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-223">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
4. <span data-ttu-id="fc3b0-224">Wählen Sie im Fenster "Eigenschaften" aus der Dropdownliste  **Startaktion** das Element **Internet Explorer** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-224">In the Properties windows, from the  **Start Action** drop-down list, choose the **Internet Explorer** item.</span></span>
    
 
5. <span data-ttu-id="fc3b0-225">Wählen Sie im Menü  **Debuggen** die Option **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-225">On the  **Debug** menu, **Start Debugging**.</span></span>
    
    <span data-ttu-id="fc3b0-226">Visual Studio öffnet SharePoint und zeigt die Bibliothek **MyDocumentLibrary** an.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-226">Visual Studio opens SharePoint and shows the  **MyDocumentLibrary** library.</span></span>
    
 
6. <span data-ttu-id="fc3b0-227">Wählen Sie in SharePoint auf der Registerkarte  **Dateien** die Option **Neues Dokument** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-227">In SharePoint, on the  **Files** tab, choose **New Document**.</span></span> 
    
 
7. <span data-ttu-id="fc3b0-228">Gehen Sie in der Arbeitsmappe zu Ihrem Projekt, MyTaskPaneApp.xlsx.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-228">Navigate to the workbook in your project, MyTaskPaneApp.xlsx.</span></span>
    
    <span data-ttu-id="fc3b0-229">Die Arbeitsmappe wird geöffnet, und das Add-in für den Aufgabenbereich wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-229">The workbook opens and the task pane add-in appears.</span></span>
    
 
8. <span data-ttu-id="fc3b0-p117">Stellen Sie sicher, dass im Browser das Skriptdebugging aktiviert ist. Im Internet Explorer können Sie das Skriptdebugging aktivieren, indem Sie das Dialogfeld  **Internetoptionen** öffnen und auf der Registerkarte **Erweitert** und die Kontrollkästchen **Skriptdebugging deaktivieren (Internet Explorer)** und **Skriptdebugging deaktivieren (Andere)** deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p117">Ensure that script debugging is enabled in your browser. In Internet Explorer, you can enable script debugging by opening the  **Internet Options** dialog box, choosing the **Advanced** tab, and then clearing the **Disable Script Debugging (Internet Explorer)** and **Disable Script Debugging (Other)** check boxes.</span></span>
    
 
9. <span data-ttu-id="fc3b0-232">Wählen Sie in Visual Studio im Menü  **Debuggen** die Option **An den Prozess anhängen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-232">In Visual Studio, on the  **Debug** menu, choose **Attach to Process**.</span></span>
    
 
10. <span data-ttu-id="fc3b0-233">Wählen Sie im Dialogfeld **An den Prozess anhängen** alle verfügbaren **iexplore.exe**-Prozesse und dann die Schaltfläche zum Anhängen**** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-233">In the  **Attach to Process** dialog box, choose all of the available **iexplore.exe** processes, and then choose the **Attach** button.</span></span>
    
 
11. <span data-ttu-id="fc3b0-234">Wählen Sie im Aufgabenbereich-Add-in die Dropdownliste  **Prüfer auswählen** aus, um eine Liste der SharePoint-Benutzer anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-234">In the task pane add-in, choose the  **Select Reviewer** drop-down list to view a list of SharePoint users.</span></span>
    
    <span data-ttu-id="fc3b0-235">Die Daten der Liste werden aus SharePoint mithilfe eines REST-Aufrufs abgerufen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-235">The data in the list is retrieved from SharePoint by using a REST call.</span></span>
    
 
12. <span data-ttu-id="fc3b0-236">Wählen Sie in der Excel-Arbeitsmappe eine beliebige Zelle aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-236">In the Excel workbook, choose any cell.</span></span>
    
 
13. <span data-ttu-id="fc3b0-237">Wählen Sie im Add-in für den Aufgabenbereich die Schaltfläche  **Daten von Auswahl abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-237">In the task pane add-in, choose the  **Get data from selection** button.</span></span>
    
    <span data-ttu-id="fc3b0-238">Die Ausführung wird an dem Haltepunkt unterbrochen, den Sie neben der `getDataFromSelection`-Methode gesetzt haben.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-238">Execution stops at the breakpoint that you set next to the  `getDataFromSelection` method.</span></span>
    
     <span data-ttu-id="fc3b0-239">**Hinweis** Falls die Arbeitsmappe keine Daten enthält, fügen Sie welche hinzu, indem Sie **Arbeitsmappe bearbeiten**, **In Excel Online bearbeiten** in der Symbolleiste wählen.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-239">**Note**  If the workbook doesn't contain any data, you can add some by choosing  **EDIT WORBOOK**,  **Edit in Excel Online** on the toolbar in the workbook.</span></span>

## <a name="package-and-publish-the-add-in"></a><span data-ttu-id="fc3b0-240">Packen und Veröffentlichen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-240">Package and publish the add-in</span></span>
<span data-ttu-id="fc3b0-241"><a name="Package"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-241"></span></span>

<span data-ttu-id="fc3b0-242">Wenn Sie zum Packen des Add-Ins für die Veröffentlichung bereit sind, öffnen Sie den Assistenten **Veröffentlichen von Office- und SharePoint-Add-Ins**.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-242">When you are ready to package your add-in for publishing, open the  **Publish Office and SharePoint Add-ins** wizard.</span></span>
 

 

- <span data-ttu-id="fc3b0-243">Öffnen Sie im  **Projektmappen-Explorer** das Kontextmenü für das SharePoint-Add-In-Projekt, und wählen Sie dann **Veröffentlichen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc3b0-243">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="fc3b0-p118">Der Assistent **Add-Ins für Office und SharePoint veröffentlichen** wird angezeigt. Weitere Informationen finden Sie unter [Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="fc3b0-p118">The  **Publish Office and SharePoint Add-ins** wizard appears. For more information, see [Publish SharePoint Add-ins by using Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="fc3b0-246">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fc3b0-246">Additional resources</span></span>
<span data-ttu-id="fc3b0-247"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="fc3b0-247"></span></span>


-  [<span data-ttu-id="fc3b0-248">Aufgabenbereich- und Inhalts-Add-Ins für Office 2013</span><span class="sxs-lookup"><span data-stu-id="fc3b0-248">Task pane and content add-ins for Office 2013</span></span>](http://msdn.microsoft.com/library/baf73b23-4429-4b7f-bcb9-a99a9618ae38%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-249">Entwurfsrichtlinien für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-249">Design guidelines for Office Add-ins</span></span>](http://msdn.microsoft.com/library/d5b2ab2e-dfc8-47c8-919c-e9c23358d70c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-250">Entwicklungslebenszyklus von Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-250">Office Add-ins development lifecycle</span></span>](http://msdn.microsoft.com/library/c35b4b2b-7869-4501-9f10-888c8e74c98c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-251">Veröffentlichen Ihres Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-251">Publish your Office Add-in</span></span>](http://msdn.microsoft.com/library/7f3ae6a0-06e9-438c-8899-bd9f605e6d9e%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-252">Grundlegendes zur JavaScript-API für Office</span><span class="sxs-lookup"><span data-stu-id="fc3b0-252">Understanding the JavaScript API for Office</span></span>](http://msdn.microsoft.com/library/01180dae-ca45-40c8-b3dd-fd2a85651c0c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-253">XML-Manifest für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-253">Office Add-ins XML manifest</span></span>](http://msdn.microsoft.com/library/4139ff24-afac-472a-af7d-9d069587ac9b%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fc3b0-254">API und Schemaverweise für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="fc3b0-254">Office Add-ins API and schema references</span></span>](http://msdn.microsoft.com/library/afcc2908-1e1b-4297-b554-11e6eb404804%28Office.15%29.aspx)
    
 

