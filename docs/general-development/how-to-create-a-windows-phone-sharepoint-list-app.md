---
title: Erstellen einer Windows Phone SharePoint-Listen-App
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3e40c475-f4c1-4a4f-a3e5-1a55f814d272
ms.openlocfilehash: 6d3a9f1f13f5c84a4a4260a7a68edfba6cef1264
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-windows-phone-sharepoint-list-app"></a><span data-ttu-id="d6416-102">Erstellen einer Windows Phone SharePoint-Listen-App</span><span class="sxs-lookup"><span data-stu-id="d6416-102">How to: Create a Windows Phone SharePoint list app</span></span>
<span data-ttu-id="d6416-p101">Erstellen Sie eine Windows Phone-App in Visual Studio basierend auf der Vorlage "Windows Phone - SharePoint-Listenanwendung". Installieren von Windows Phone SharePoint SDK stellt zwei SharePoint-Anwendung für Windows Phone-Vorlagen zur Verfügung Sie in Visual Studio 2010 oder Visual Studio 2010 Express für Windows Phone. (Siehe  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)). Mit der Vorlage Windows Phone SharePoint List Application können Sie die Schritte eines Assistenten zum Erstellen einer funktionalen Windows Phone-app ausführen, die zugreifen und Bearbeiten von Daten in einer SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="d6416-p101">Create a Windows Phone app in Visual Studio based on the Windows Phone SharePoint List Application template. Installing the Windows Phone SharePoint SDK makes two Windows Phone SharePoint Application templates available to you in Visual Studio 2010 or Visual Studio 2010 Express for Windows Phone. (See  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) Using the Windows Phone SharePoint List Application template, you can follow the steps of a wizard to create a functional Windows Phone app that can access and manipulate data in a SharePoint list.</span></span>


> <span data-ttu-id="d6416-106">**Wichtig:** Wenn Sie eine App für Windows Phone 8 entwickeln, müssen Sie Visual Studio Express 2012 anstelle von Visual Studio 2010 Express verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6416-106">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="d6416-107">Mit Ausnahme der Entwicklungsumgebung gelten alle Informationen in diesem Artikel für das Erstellen von Apps sowohl auf Windows Phone 8 als auch auf Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="d6416-107">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="d6416-108">Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d6416-108">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 


## <a name="create-the-windows-phone-sharepoint-list-application"></a><span data-ttu-id="d6416-109">Erstellen der Windows Phone-SharePoint-Listenanwendung</span><span class="sxs-lookup"><span data-stu-id="d6416-109">Create the Windows Phone SharePoint list application</span></span>
<span data-ttu-id="d6416-110"><a name="BKMK_CreatingSPListApplication"> </a></span><span class="sxs-lookup"><span data-stu-id="d6416-110"><a name="BKMK_CreatingSPListApplication"> </a></span></span>

<span data-ttu-id="d6416-111">In der Windows Phone-SharePoint-Listen-app können Sie die meisten der Listen zugreifen, die in SharePoint-Add-Ins verfügbar sind. Für die Zwecke dieser Beispiel-app für Windows Phone verwenden wir SharePoint-Listen mit Beispieldaten aus einem fiktiven Unternehmen mit dem Namen Contoso, Ltd. Für die Schritte zum Erstellen der ersten Iteration der in diesem SharePoint-Listen-app verwenden wir eine SharePoint-Liste Kontakte, die Mitglieder der ein Marketingteam bei Contoso, Informationen enthält, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="d6416-111">In your Windows Phone SharePoint list app, you can access most of the lists that are available in SharePoint Add-ins. For the purposes of this sample Windows Phone app, we use SharePoint lists with sample data from a fictitious company named Contoso, Ltd. For the steps to create the first iteration of this SharePoint list app, we use a SharePoint Contacts list that contains information about members of a marketing team at Contoso, as shown in Figure 1.</span></span>
  
    
    

<span data-ttu-id="d6416-112">**Abbildung 1. Kontakteliste für Contoso-Marketingteam**</span><span class="sxs-lookup"><span data-stu-id="d6416-112">**Figure 1. Contacts list for Contoso marketing team**</span></span>

  
    
    

  
    
    
![Kontakteliste für Contoso-Marketingteam](../images/8d56d824-d96a-4f1e-9040-ce1da9a734d8.gif)
  
    
    

### <a name="to-create-a-windows-phone-sharepoint-list-app"></a><span data-ttu-id="d6416-114">Erstellen eine Windows Phone-SharePoint-Listen-app</span><span class="sxs-lookup"><span data-stu-id="d6416-114">To create a Windows Phone SharePoint list app</span></span>


1. <span data-ttu-id="d6416-115">Starten Sie Visual Studio 2010 mit der Option **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d6416-115">Start Visual Studio 2010 by using the **Run as Administrator** option.</span></span>
    
  
2. <span data-ttu-id="d6416-116">Klicken Sie auf **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="d6416-116">Choose **File**, **New**, **Project**.</span></span> 
    
    <span data-ttu-id="d6416-117">Das Dialogfeld **Neues Projekt** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d6416-117">The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="d6416-p103">Klicken Sie im Dialogfeld **Neues Projekt** den Knoten **Visual c#**, und wählen Sie dann den Knoten **für Fenster Phone Silverlight**. (Stellen Sie sicher, dass die Zielversion .NET Framework 4 festgelegt ist.)</span><span class="sxs-lookup"><span data-stu-id="d6416-p103">In the **New Project** dialog box, expand the **Visual C#** node, and then choose the **Silverlight for Window Phone** node. (Ensure that the target .NET Framework version is set to 4.)</span></span>
    
    > <span data-ttu-id="d6416-120">**Hinweis:** Die im Rahmen des Windows Phone SharePoint SDK installierten Vorlagen eignen sich nur für C#-Projekte.</span><span class="sxs-lookup"><span data-stu-id="d6416-120">**Note:** The templates installed by the Windows Phone SharePoint SDK work only in C# projects.</span></span> <span data-ttu-id="d6416-121">Für Visual Basic-Projekte sind die Vorlagen nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d6416-121">The templates are not available for Visual Basic projects.</span></span> 
4. <span data-ttu-id="d6416-122">Wählen Sie im Bereich **Vorlagen** die Vorlage **Windows Phone - SharePoint-Listenanwendung** aus, und geben Sie dem Projekt einen Namen, wie z. B. ContosoSPListApp.</span><span class="sxs-lookup"><span data-stu-id="d6416-122">In the **Templates** pane, choose the **Windows Phone SharePoint List Application** template and give the project a name, such asContosoSPListApp.</span></span>
    
  
5. <span data-ttu-id="d6416-p105">Beim Ausführen des **Assistenten für SharePoint Phone-Anwendung**, kann der in Abbildung 2 dargestellten Fehler auftreten. Dieser Fehler tritt auf, weil das Konto der Entwickler verwendet wird, während der Ausführung des **Assistenten für SharePoint Phone-Anwendung** über unzureichende Berechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="d6416-p105">While running the **SharePoint Phone Application Wizard**, the error shown in Figure 2 can occur. This error occurs because the account the developer is using while running the **SharePoint Phone Application Wizard** has insufficient permissions.</span></span>
    
   <span data-ttu-id="d6416-125">**Abbildung 2. SPList-Assistenten-Fehlermeldung**</span><span class="sxs-lookup"><span data-stu-id="d6416-125">**Figure 2. SPList wizard error message**</span></span>

  

  ![Fehler des SPList-Assistenten](../images/SP15Con_CreateSharePointListAppsForWindowsPhoneFig3.png)
  

    <span data-ttu-id="d6416-127">Sie können diesen Fehler beheben, indem Sie dem Konto, mit dem der Entwickler den SPList-Assistenten ausführt, ausreichende Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="d6416-127">You can resolve this error by giving sufficient privileges to the account with which the developer is running the SPList wizard.</span></span> <span data-ttu-id="d6416-128">Führen Sie den **Splist-Assistenten** erneut aus, nachdem ausreichende Berechtigungen erteilt wurden.</span><span class="sxs-lookup"><span data-stu-id="d6416-128">Rerun **Splist wizard** after sufficient rights are given.</span></span>
    
  
6. <span data-ttu-id="d6416-p107">Wählen Sie die Schaltfläche **OK**. Der **Assistent für SharePoint Phone-Anwendung** wird angezeigt. Sie verwenden dieses Assistenten zum Auswählen einer SharePoint-Liste und Konfigurieren der Eigenschaften von dieser Liste aus, um zu bestimmen, wie es in Ihrer Windows Phone-app angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="d6416-p107">Choose the **OK** button. The **SharePoint Phone Application Wizard** appears. You use this wizard to choose a SharePoint list and configure properties of that list to determine how it appears in your Windows Phone app.</span></span>
    
  
7. <span data-ttu-id="d6416-132">Geben Sie die URL der SharePoint-Zielwebsite in Ihrem Netzwerk (d. h., eine lokale Installation von SharePoint Server ).</span><span class="sxs-lookup"><span data-stu-id="d6416-132">Specify the URL of a target SharePoint site on your network (that is, an on-premises installation of SharePoint Server).</span></span>
    
  
8. <span data-ttu-id="d6416-p108">Wählen Sie **Listen Suchen**. Wenn das Konto, unter dem Sie Visual Studio ausführen, Zugriff auf die Website für die angegebene Ziel hat, zeigt der **Assistent für SharePoint Phone-Anwendung** die Listen, die auf dieser Website verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="d6416-p108">Choose **Find Lists**. If the account under which you are running Visual Studio has access to the specified target site, the **SharePoint Phone Application Wizard** displays the lists that are available on that site.</span></span>
    
  
9. <span data-ttu-id="d6416-135">Wählen Sie eine der verfügbaren Listen, wie etwa eine Kontaktliste (mit Beispieldaten in einer angepassten Ansicht in Abbildung 1 dargestellt).</span><span class="sxs-lookup"><span data-stu-id="d6416-135">Select one of the available lists, such as a Contacts list (shown with sample data in a customized view in Figure 1).</span></span>
    
  
10. <span data-ttu-id="d6416-p109">Wählen Sie auf **Weiter**. Der Assistent zeigt die verfügbaren Ansichten der ausgewählten Liste zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="d6416-p109">Choose **Next**. The wizard displays the available views associated with the selected list.</span></span>
    
    <span data-ttu-id="d6416-p110">Die vom Assistenten angezeigten Ansichten sind diese Ansichten, die von Benutzern erstellte (oder durch SharePoint Server bereitgestellt) wurde und eine bestimmte Liste auf dem Server zugeordnet ist. Einige SharePoint-Listen haben nur eine Ansicht standardmäßig zugeordnet. Eine Kontaktliste ist standardmäßig eine Ansicht für alle Kontakte zugeordnet. Eine Ankündigungsliste ist standardmäßig eine Ansicht für alle Elemente zugeordnet. Eine Aufgabenlisten wird standardmäßig sechs Ansichten, einschließlich einer Ansicht alle Tasks und einer aktiven Vorgangsansicht zugeordnet. Für die einzelnen Ansichten, die Sie in dieser Phase im Assistenten zum auswählen ein Steuerelements **PivotItem** erstellt und mit dem **Pivot** -Steuerelement in der XAML-Code, der die Benutzeroberfläche der Windows Phone-app definiert hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d6416-p110">The views displayed by the wizard are those views that have been created by users (or provisioned by SharePoint Server) and associated with a given list on the server. Some SharePoint lists have only one view associated with them by default. A Contacts list, by default, is associated with an All Contacts view. An Announcements list, by default, is associated with an All Items view. A Tasks lists, by default, is associated with six views, including an All Tasks view and an Active Tasks view. For each view that you select at this stage in the wizard, a **PivotItem** control is created and added to the **Pivot** control in the XAML that defines the UI of the Windows Phone app.</span></span>
    
  
11. <span data-ttu-id="d6416-144">Aktivieren Sie das Kontrollkästchen der Ansichten, die in der Windows Phone-App enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="d6416-144">Select the check box next to each view you want to include in your Windows Phone app.</span></span>
    
  
12. <span data-ttu-id="d6416-p111">Wählen Sie auf **Weiter**. Der Assistent zeigt die verfügbaren Aktionen für die ausgewählte Liste in Ihrer Windows Phone-app.</span><span class="sxs-lookup"><span data-stu-id="d6416-p111">Choose **Next**. The wizard displays the available actions for the selected list in your Windows Phone app.</span></span>
    
    <span data-ttu-id="d6416-p112">Die Auswahlmöglichkeiten sind **neu**, **Anzeigen**, **Bearbeiten** und **Löschen**. Wenn Sie möchten möglicherweise bearbeiten oder Löschen von Listenelementen in Ihrer app, müssen Sie den **Display**-Vorgang in dieser Phase im Assistenten auswählen. (Die Kontrollkästchen für die Vorgänge **Bearbeiten** und **Löschen von** sind deaktiviert, wenn der Vorgang **Anzeigen** ausgewählt ist.)</span><span class="sxs-lookup"><span data-stu-id="d6416-p112">The choices are **New**, **Display**, **Edit**, and **Delete**. If you want to be able to edit or delete list items in your app, you must choose the **Display** operation at this stage in the wizard. (The check boxes for the **Edit** and **Delete** operations are disabled unless the **Display** operation is selected.)</span></span>
    
  
13. <span data-ttu-id="d6416-150">Aktivieren Sie das Kontrollkästchen neben jedem gewünschte Aktion haben verfügbar für die ausgewählte Liste in Ihrer Windows Phone-app.</span><span class="sxs-lookup"><span data-stu-id="d6416-150">Select the check box next to each action you want to have available for the selected list in your Windows Phone app.</span></span>
    
  
14. <span data-ttu-id="d6416-p113">Wählen Sie **Weiter**. Der Assistent zeigt die Felder an, die mit der ausgewählten Liste auf der SharePoint-Website verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="d6416-p113">Choose **Next**. The wizard displays the fields associated with the selected list on the SharePoint site.</span></span>
    
    > <span data-ttu-id="d6416-153">**Hinweis:** Benutzerdefinierte Felder können im Assistenten für SharePoint-Listen für mobile Geräte nicht ausgewählt werden.</span><span class="sxs-lookup"><span data-stu-id="d6416-153">**Note:** A custom field will not be available to select from the SharePoint List wizard for mobile devices.</span></span> <span data-ttu-id="d6416-154">Sie können jedoch benutzerdefinierten Code zum Zugriff auf jedes beliebige benutzerdefinierte Feld schreiben.</span><span class="sxs-lookup"><span data-stu-id="d6416-154">However, you can write custom code to access any custom field.</span></span> <span data-ttu-id="d6416-155">Ein Feld kann nicht mit seinem Inhaltstyp verknüpft werden.</span><span class="sxs-lookup"><span data-stu-id="d6416-155">A field cannot be associated with its content type.</span></span> <span data-ttu-id="d6416-156">Aber wenn für die Liste mehrere Inhaltstypen aktiviert sind, können alle Felder von Entwicklern in ihren Phone-Apps verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d6416-156">However if multiple content types are enabled for the list, all the fields will be available for developers to consume in their phone apps.</span></span> 
15. <span data-ttu-id="d6416-157">Aktivieren Sie das Kontrollkästchen neben jedem Feld, das in der Liste enthalten sein, wie es in Ihrer Windows Phone-app angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d6416-157">Select the check box next to each field you want to include in the list as it will appear in your Windows Phone app.</span></span>
    
    > <span data-ttu-id="d6416-158">**Hinweis:** Listenfelder, die in SharePoint Server als Informationen erfordernd vorgesehen sind, sind bereits ausgewählt. Sie können nicht im Assistenten gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="d6416-158">**Note:** List fields that are designated in SharePoint Server as requiring information are selected already; they can't be cleared in the wizard.</span></span> 
16. <span data-ttu-id="d6416-p115">Wählen Sie **Weiter**. Der Assistent bietet Ihnen die Möglichkeit, die Reihenfolge der Felder anzugeben, die Sie im vorherigen Schritt ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="d6416-p115">Choose **Next**. The wizard gives you the opportunity to order the fields you selected in the previous step.</span></span>
    
  
17. <span data-ttu-id="d6416-161">Sortieren Sie die Felder gemäß Ihren Anforderungen. Wählen Sie hierzu ein Feld aus, und verschieben Sie es mithilfe des Aufwärts- oder Abwärtspfeils nach oben bzw. nach unten.</span><span class="sxs-lookup"><span data-stu-id="d6416-161">Order the fields according to your needs by selecting individual fields and moving them higher or lower in the order by choosing the up or down arrows.</span></span>
    
  
18. <span data-ttu-id="d6416-p116">Klicken Sie auf **Fertig stellen**. Von Visual Studio werden die erforderlichen Dateien für das Projekt erstellt, und die Datei "List.xaml" wird zur Bearbeitung geöffnet.</span><span class="sxs-lookup"><span data-stu-id="d6416-p116">Choose **Finish**. Visual Studio creates the necessary files for the project and opens the List.xaml file for editing.</span></span>
    
  

## <a name="run-the-windows-phone-app-generated-by-the-sharepoint-phone-application-wizard"></a><span data-ttu-id="d6416-164">Führen Sie mithilfe des Assistenten für SharePoint Phone-Anwendung generierte Windows Phone-app</span><span class="sxs-lookup"><span data-stu-id="d6416-164">Run the Windows Phone app generated by the SharePoint Phone Application Wizard</span></span>
<span data-ttu-id="d6416-165"><a name="BKMK_RunningApp"> </a></span><span class="sxs-lookup"><span data-stu-id="d6416-165"><a name="BKMK_RunningApp"> </a></span></span>

<span data-ttu-id="d6416-p117">Das Projekt mit dem **Assistenten für SharePoint Phone-Anwendung** generiert kann erstellt werden, wie es ist, erstellen eine einfache, aber funktionale Windows Phone SharePoint-Listen-app. Wir können ändern und Entwickeln der app weiter, aber, jetzt ein Benutzer können Tippen Sie auf (oder, klicken Sie in der Windows Phone-Emulator auf) ein bestimmtes Listenelement und die app zeigt alle Felder zugeordnet, dass das Element (diese Felder, die Sie im Assistenten zum Einschließen in die app ausgewählt haben). Ein Benutzer kann auch neue Listenelemente hinzufügen, Löschen von Listenelementen und die Feldwerte für Listenelemente bearbeiten. Mehrere Benutzer anmelden in einer einzelnen app wird nicht unterstützt. Entwickler kann jedoch Code schreiben, die den aktuellen Benutzer abmeldet, wenn ein anderer Benutzer, zur Anmeldung bei der gleichen mobile app versucht.</span><span class="sxs-lookup"><span data-stu-id="d6416-p117">The project generated by the **SharePoint Phone Application Wizard** can be built as it is to create a simple but functional Windows Phone SharePoint list app. We can modify and develop the app further, but, for now, a user can tap (or, in the Windows Phone Emulator, click) a given list item and the app displays all the fields associated with that item (those fields that you selected in the wizard to include in the app). A user can also add new list items, delete list items, and edit the field values for list items. Multiple-user logon in a single app is not supported. However, a developer can write code that logs off the current user when another user tries to log on to the same mobile app.</span></span>
  
    
    
<span data-ttu-id="d6416-p118">Das Deployment-Ziel für die Lösung wird standardmäßig auf Windows Phone-Emulator festgelegt. Sie können das Projekt in Visual Studio ausführen, unverändert (durch Drücken von F5, um das Projekt im Zusammenhang mit den Debugger starten oder durch Drücken von STRG + F5, um das Projekt ohne Debuggen starten). Die Windows Phone-Emulator neu gestartet wird, das Betriebssystem Windows Phone wird geladen und Ihre app für den Emulator bereitgestellt und gestartet wird. Wenn Sie mit dem Code starten, während sie vom Assistenten erstellt werden, wenn Ihre SharePoint-Listen-app im Emulator ausgeführt wird, werden Sie für die Anmeldeinformationen für die angegebene SharePoint-Liste auf die Zielwebsite gefragt. Geben Sie die Anmeldeinformationen für ein Konto, das über ausreichende Berechtigungen zum Zugriff auf die Liste, und wählen Sie **Anmelden** im Emulator hat. Die Hauptseite der Windows Phone-app (definiert durch die List.xaml-Datei in das Projekt) wird im Emulator angezeigt. Je nach den Feldern, die Sie ausgewählt haben und den Auftrag, den Sie für diese Felder in den vorherigen Schritten angegeben, sollte die Elemente aus der angegebenen Liste angezeigt werden. Basierend auf den Daten in der Liste, die durch die in Abbildung 1 dargestellt, wird eine Liste von Elementen im Emulator wie in Abbildung 3 dargestellt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="d6416-p118">The deployment target for the solution is set to Windows Phone Emulator by default. You can run the project in Visual Studio as it is (either by pressing F5 to start the project in the context of the debugger or by pressing CTRL+F5 to start the project without debugging). The Windows Phone Emulator is launched, the Windows Phone operating system is loaded, and your app is deployed to the emulator and started. If you start with the code as it is generated by the wizard, when your SharePoint list app runs in the emulator, you're asked for credentials for the specified SharePoint list on the target site. Provide the credentials for an account that has sufficient permissions to access the list and choose **Log On** in the emulator. The main page of the Windows Phone app (defined by the List.xaml file in the project) is displayed in the emulator. Depending on the fields you chose and the order you specified for those fields in the previous steps, you should see items from the specified list. Based on the data in the list represented by Figure 1, you would see a list of items in the emulator as shown in Figure 3.</span></span>
  
    
    

<span data-ttu-id="d6416-179">**Abbildung 3. SharePoint-Listenelemente in einer Windows Phone-app**</span><span class="sxs-lookup"><span data-stu-id="d6416-179">**Figure 3. SharePoint list items in a Windows Phone app**</span></span>

  
    
    

  
    
    
![SharePoint-Listenelemente in einer Windows Phone-App](../images/9159345c-ce12-41a6-8994-fc2e9aa26fd6.gif)
  
    
    
<span data-ttu-id="d6416-p119">Während der Ausführung einer Windows Phone-app, kann der in Abbildung 4 dargestellte Authentifizierungsfehler auftreten. In diesem Fall, da die mobile SharePoint-app **Standardauthentifizierung Formular** benötigt; Dies ist nicht standardmäßig aktiviert.</span><span class="sxs-lookup"><span data-stu-id="d6416-p119">While running a Windows Phone app, the authentication error shown in Figure 4 can occur. This happens because the SharePoint mobile app requires **Basic Form Authentication**; this isn't enabled by default.</span></span>
  
    
    

<span data-ttu-id="d6416-183">**Abbildung 4. Authentifizierungsfehler für Windows Phone-app**</span><span class="sxs-lookup"><span data-stu-id="d6416-183">**Figure 4. Windows Phone app authentication error**</span></span>

  
    
    

  
    
    
![Fehler der mobilen App](../images/SP15Con_CreateSharePointListAppsForWindowsPhoneFig4.png)
  
    
    
<span data-ttu-id="d6416-185">Sie können diesen Fehler beheben, indem-Zentraladministration **grundlegende Formularauthentifizierung** auswählen.</span><span class="sxs-lookup"><span data-stu-id="d6416-185">You can resolve this error by choosing **Basic form authentication** from Central Administration.</span></span>
  
    
    

### <a name="to-enable-basic-form-authentication"></a><span data-ttu-id="d6416-186">So aktivieren Sie grundlegende Formularauthentifizierung</span><span class="sxs-lookup"><span data-stu-id="d6416-186">To enable Basic form authentication</span></span>


1. <span data-ttu-id="d6416-187">Navigieren Sie zur **Zentraladministration**; Stellen Sie sicher, dass Sie Administratorrechte auf dem Server verfügen.</span><span class="sxs-lookup"><span data-stu-id="d6416-187">Navigate to **Central Administration**; ensure you have admin rights on server.</span></span>
    
  
2. <span data-ttu-id="d6416-188">Wählen Sie unter **Verwaltung von** **Webanwendungen verwalten**.</span><span class="sxs-lookup"><span data-stu-id="d6416-188">Choose **Manage Web Applications** under **Application Management**.</span></span>
    
  
3. <span data-ttu-id="d6416-189">Wählen Sie die Webanwendung (auf dem der SharePoint-Website, die Sie von der mobilen Anwendung zugreifen müssen).</span><span class="sxs-lookup"><span data-stu-id="d6416-189">Choose your web application (on which you have your SharePoint site, which you are accessing from your mobile app).</span></span>
    
  
4. <span data-ttu-id="d6416-190">Wählen Sie im Menüband **Authentifizierungsanbieter**.</span><span class="sxs-lookup"><span data-stu-id="d6416-190">Choose **Authentication Providers** from the ribbon.</span></span>
    
  
5. <span data-ttu-id="d6416-191">Wählen Sie im Menüband **Authentifizierungsanbieter**.</span><span class="sxs-lookup"><span data-stu-id="d6416-191">Choose **Authentication Providers** from the ribbon.</span></span>
    
  
6. <span data-ttu-id="d6416-192">Wählen Sie im Dialogfeld **Authentifizierungsanbieter** **Standard** Authentifizierung bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="d6416-192">In the **Authentication Provider** dialog box, choose **Default** to Edit Authentication.</span></span>
    
  
7. <span data-ttu-id="d6416-193">Klicken Sie im Modell **Authentifizierung bearbeiten** wählen Sie unter **Claims Authentication** Typen **Standardauthentifizierung**.</span><span class="sxs-lookup"><span data-stu-id="d6416-193">In the **Edit Authentication** model window, choose **Basic Authentication** under **Claims Authentication** types.</span></span>
    
  
<span data-ttu-id="d6416-p120">Wenn Sie Ihre Windows Phone-app auf den Daten aus der Kontaktliste basierend, wie in Abbildung 1 dargestellt, können Sie ein bestimmtes Listenelement auswählen und die app stellt eine Seite mit einer Ansicht des Elements (durch DisplayForm.xaml im Projekt definiert) alle für das Element verfügbaren Felder in der app, wie in Abbildung 5 angezeigt. (In diesem Beispiel alle Felder, die mit einer SharePoint-Liste Kontakte verknüpft sind im Application-Assistent für SharePoint-Telefon ausgewählt wurden und wurde die Standardreihenfolge dieser Felder beibehalten.)</span><span class="sxs-lookup"><span data-stu-id="d6416-p120">If you based your Windows Phone app on the data from a Contacts list, as shown in Figure 1, you can choose a particular list item and the app presents a page with a view of the item (defined by DisplayForm.xaml in the project) showing all the fields available for the item in the app, as in Figure 5. (For this example, all the fields associated with a SharePoint Contacts list were selected in the SharePoint Phone Application Wizard and the default order of those fields was retained.)</span></span>
  
    
    

<span data-ttu-id="d6416-196">**Abbildung 5. DisplayForm-Ansicht eines kontaktlistenelements**</span><span class="sxs-lookup"><span data-stu-id="d6416-196">**Figure 5. DisplayForm view of a Contacts list item**</span></span>

  
    
    

  
    
    
![DisplayForm-Ansicht eines Kontakte-Listenelements](../images/e2cf6848-bd29-416b-b397-a1d670bd2910.gif)
  
    
    
<span data-ttu-id="d6416-p121">Beachten Sie die **Bearbeiten** und **Löschen von** Schaltflächen auf der Anwendungsleiste auf dieser Seite der app. Diese Vorgänge sind für Sie von Methoden in Microsoft.SharePoint.Phone.Application.dll implementiert (die eine der Bibliotheken, die von Windows Phone SharePoint SDK installiert ist). Wenn Sie die Schaltfläche **Bearbeiten** geklickt haben, wird ein Windows Phone- **Page** -Steuerelement (d. h., ein Objekt aus einer Klasse, die von der **Microsoft.Phone.Controls.PhoneApplicationPage** -Klasse erbt instanziiert) angezeigt. Die zugrunde liegende **UpdateItem** -Methode der **EditItemViewModelBase** -Klasse wird ausgeführt, wenn Sie die Felder bearbeiten, und wählen Sie die Schaltfläche **Absenden** auf dieser Seite in der app, (, die schließlich führt die **Update** -Methode eines **ListItem** -Objekts aus der SharePoint Silverlight-Clientobjektmodell) Ihre Änderungen an der SharePoint-Liste gespeichert.</span><span class="sxs-lookup"><span data-stu-id="d6416-p121">Notice the **Edit** and **Delete** buttons on the Application Bar in this page of the app. These operations are implemented for you by methods in Microsoft.SharePoint.Phone.Application.dll (which is one of the libraries installed by the Windows Phone SharePoint SDK). If you choose the **Edit** button, a Windows Phone **Page** control (that is, an object instantiated from a class that inherits from the **Microsoft.Phone.Controls.PhoneApplicationPage** class) is displayed. If you edit any of the fields and choose the **Submit** button on that page in the app, the underlying **UpdateItem** method of the **EditItemViewModelBase** class is executed (which, ultimately, executes the **Update** method of a **ListItem** object from the SharePoint Silverlight client object model) to save your changes to the SharePoint list.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="d6416-202">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d6416-202">Additional resources</span></span>
<span data-ttu-id="d6416-203"><a name="SP15Createwinphoneapp_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d6416-203"><a name="SP15Createwinphoneapp_addlresources"> </a></span></span>


-  [<span data-ttu-id="d6416-204">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="d6416-204">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="d6416-205">Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6416-205">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d6416-206">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="d6416-206">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="d6416-207">Microsoft SharePoint SDK für Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="d6416-207">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="d6416-208">Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="d6416-208">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="d6416-209">Microsoft SharePoint SDK für Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="d6416-209">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

