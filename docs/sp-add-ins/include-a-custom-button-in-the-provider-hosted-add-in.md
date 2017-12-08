---
title: "Einschließen einer benutzerdefinierten Schaltfläche im vom Anbieter gehosteten Add-In"
description: "Erstellen einer benutzerdefinierten Liste auf der Hostwebsite, Hinzufügen einer benutzerdefinierten Schaltfläche, Anforderung der Leseberechtigung, Ausführen des Add-Ins und Testen der Schaltfläche."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 62dce66d9f2c0cd1a33f505659bafe065e5a9f99
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="include-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="e1f1b-103">Einschließen einer benutzerdefinierten Schaltfläche im vom Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="e1f1b-103">Include a custom button in the provider-hosted add-in</span></span>

<span data-ttu-id="e1f1b-104">Dies ist der dritte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-104">This is the third in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="e1f1b-105">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e1f1b-105">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="e1f1b-106">Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In</span><span class="sxs-lookup"><span data-stu-id="e1f1b-106">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
    
> [!NOTE]
> <span data-ttu-id="e1f1b-107">Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-107">Note  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_Provider-hosted_Add-Ins_Tutorials and open the BeforeRibbonButton.sln file.</span></span> <span data-ttu-id="e1f1b-108">Sie können auch das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeAdd-inPart.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-108">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeRibbonButton.sln file.</span></span>

<span data-ttu-id="e1f1b-109">Ein SharePoint-Add-In kann benutzerdefinierte Aktionen umfasst; dies ist die SharePoint-Bezeichnung für benutzerdefinierte Menüelemente oder Menübandschaltflächen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-109">A SharePoint Add-in can include custom actions, which is the SharePoint term for a custom menu items or ribbon buttons. In this article you'll learn how to create a custom button that synchronizes a SharePoint list with a remote database.</span></span> <span data-ttu-id="e1f1b-110">In diesem Artikel erfahren Sie, wie eine benutzerdefinierte Schaltfläche erstellt wird, die eine SharePoint-Liste mit einer Remotedatenbank synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-110">A spappsing can include custom actions, which is the SharePoint term for a custom menu items or ribbon buttons. In this article you'll learn how to create a custom button that synchronizes a SharePoint list with a remote database.</span></span>
 
## <a name="create-a-custom-list-on-the-host-website"></a><span data-ttu-id="e1f1b-111">Erstellen einer benutzerdefinierten Liste auf der Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="e1f1b-111">Create a custom list on the host website</span></span>

<span data-ttu-id="e1f1b-p103">Die benutzerdefinierte Schaltfläche wird sich auf dem Menüband einer bestimmte Liste befinden, in der die Mitarbeiter eines lokalen Geschäfts aufgezeichnet werden. In einem späteren Artikel dieser Reihe erfahren Sie, wie Sie eine benutzerdefinierte Liste programmgesteuert zu einer Hostwebsite hinzufügen, aber für den Moment werden Sie diese manuell hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-p103">The custom button is going to be on the ribbon of a specific list that records the employees of the local store. In a later article in this series, you'll learn how to programmatically add a custom list to a host website, but for now you'll add one manually.</span></span> 

1. <span data-ttu-id="e1f1b-114">Navigieren Sie auf der Startseite des Fabrikam-Stores in Hongkong zu **Websiteinhalte** > **Add-In hinzufügen** > ** Benutzerdefinierte Liste**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-114">From the home page of the Fabrikam Hong Kong Store, navigate to  Site Contents | add an add-in | Custom List.</span></span> 

2. <span data-ttu-id="e1f1b-115">Geben Sie im Dialogfeld **Benutzerdefinierte Liste** **Lokale Mitarbeiter** als Name an, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-115">In the Adding Custom List dialog, specifyLocal Employees as the name and press Create.</span></span> 

3. <span data-ttu-id="e1f1b-116">Öffnen Sie auf der Seite **Websiteinhalte** die Liste **Lokale Mitarbeiter**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-116">On the **Site Contents** page, open the **Local Employees** list.</span></span>

4. <span data-ttu-id="e1f1b-117">Klicken Sie auf dem Menüband auf der Registerkarte **Liste** auf **Listeneinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-117">On the **List** tab on the ribbon, select **List Settings**.</span></span>

5. <span data-ttu-id="e1f1b-118">Klicken Sie im Abschnitt **Spalten** der Seite **Listeneinstellungen** auf die Spalte **Titel**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-118">In the  **Columns** section of the **List Settings** page, click the **Title** column.</span></span>

6. <span data-ttu-id="e1f1b-119">Ändern Sie im Formular **Spalte bearbeiten** den **Spaltenname** von **Title** in **Name**, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-119">In the  Edit Column form, change the Column name from Title toProduct; and then click  OK.</span></span>

7. <span data-ttu-id="e1f1b-120">Klicken Sie auf der Seite **Einstellungen** auf **Spalte erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-120">On the **Settings** page, click **Create column**.</span></span>

8. <span data-ttu-id="e1f1b-121">Gehen Sie im Formular **Spalte erstellen** folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-121">In the **Create Column** form, do the following:</span></span>
    
   1. <span data-ttu-id="e1f1b-122">Geben Sie **Zur Unternehmensdatenbank hinzugefügt** als **Spaltenname** ein.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-122">For **Column name**, enter **Added to Corporate DB**.</span></span>
   2. <span data-ttu-id="e1f1b-123">Legen Sie den **Typ** auf **Ja/Nein (Kontrollkästchen)** fest.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-123">Set the type to  Yes/No (check box).</span></span>
   3. <span data-ttu-id="e1f1b-124">Legen Sie den **Standardwert** auf **Nein** fest.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-124">Set the  **Default value** to **No**.</span></span>
   4. <span data-ttu-id="e1f1b-125">Klicken Sie auf **OK**. </span><span class="sxs-lookup"><span data-stu-id="e1f1b-125">Select **OK**.</span></span> <span data-ttu-id="e1f1b-126">Sie gelangen zurück zur Seite **Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-126">Press  OK. You are taken back to the  **Settings** page.</span></span>
    
9. <span data-ttu-id="e1f1b-127">Wählen Sie **Websiteinhalte** aus, um die Seite **Websiteinhalte** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-127">Select **Site Contents** to open the **Site Contents** page.</span></span> <span data-ttu-id="e1f1b-128">Dort befindet sich die Kachel für die neute Liste.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-128">Click  Site Contents to open the Site Contents page. The tile for the new list is there. Open it.</span></span> <span data-ttu-id="e1f1b-129">Öffnen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-129">Open it.</span></span>
    
10. <span data-ttu-id="e1f1b-130">Klicken Sie auf **Neues Element**, und geben Sie auf dem Formular zu Erstellen eines Elements einen Namen ein, wählen Sie jedoch *nicht* die Option **Zur Unternehmensdatenbank hinzugefügt** aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-130">Click  **new item** and on the create item form, enter a name, but do *not*  check **Added to Corporate DB**. Then click  Save. The list should look similar to the following:</span></span> <span data-ttu-id="e1f1b-131">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-131">Select **Save**.</span></span> <span data-ttu-id="e1f1b-132">Die Liste sollte ähnlich wie im folgenden Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-132">The calendar should look similar to the following:</span></span>

    <span data-ttu-id="e1f1b-133">*Abbildung 1. Die Liste der lokalen Mitarbeiter mit einem einzelnen Element*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-133">*Figure 1. Local Employees list with a single item*</span></span>

    ![Die Liste der lokalen Mitarbeiter mit einem einzelnen Element. Der Name ist Brayden Sawtell. Der Wert der Spalte „Zur Unternehmensdatenbank hinzugefügt“ ist „Nein“.](../images/a3371859-e42f-49ea-8f17-48d8a248b075.PNG)

## <a name="add-the-custom-button"></a><span data-ttu-id="e1f1b-137">Hinzufügen der benutzerdefinierten Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="e1f1b-137">Add the custom button</span></span>

<span data-ttu-id="e1f1b-138">In diesem Abschnitt schließen Sie das Markup in das Add-In ein, das eine Schaltfläche für das Menüband der Liste bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-138">In this section, you include markup in the add-in that deploys a button to the list's ribbon.</span></span> <span data-ttu-id="e1f1b-139">Wenn ein Benutzer einen Mitarbeiter in der Liste markiert und die Schaltfläche auswählt, wird der Name des Mitarbeiters zur Unternehmensdatenbank hinzugefügt, und das Feld **Zur Unternehmensdatenbank hinzugefügt** ändert sich von **Nein** zu **Ja**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-139">In this section, you include markup in the add-in that will deploy a button to the list's ribbon. When a user highlights an employee on the list and clicks the button, the employee's name will be added to the corporate database and the  Added to Corporate DB field for the employee will be switched from No to Yes.</span></span>

1.  <span data-ttu-id="e1f1b-140">Wenn Visual Studio geöffnet ist, müssen Sie es schließen und die Projektmappe „ChainStore“ erneut öffen, damit Visual Studio Ihre neue Liste erkennen kann. (Führen Sie Visual Studio als Administrator aus.)</span><span class="sxs-lookup"><span data-stu-id="e1f1b-140">If Visual Studio is open, you have to close it  and reopen the Chain Store solution so that Visual Studio can discover your new list. (Run Visual Studio as an administrator.)</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="e1f1b-141">Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach dem erneuten Öffnen wieder auf die Standardwerte eingestellt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-141">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> <span data-ttu-id="e1f1b-142">Gehen Sie nach dem erneuten Öffnen der Beispiel-Lösung in dieser Artikelreihe immer folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-142">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 

   > 1. <span data-ttu-id="e1f1b-143">Klicken Sie mit der rechten Maustaste oben im **Projektmappen-Explorer** auf den Projektmappenknoten, und wählen Sie **Startprojekte festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-143">Right-click the solution node at the top of  **Solution Explorer** and select **Set startup projects**.</span></span>  
   > 2. <span data-ttu-id="e1f1b-144">Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-144">Make sure all three projects are set to  **Start** in the **Action** column.</span></span>

2. <span data-ttu-id="e1f1b-145">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das **ChainStore**-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-145">Right-click the **ChainStore** project in **Solution Explorer**, and then select **Add** > **New Item**.</span></span> 
    
3. <span data-ttu-id="e1f1b-146">Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **Benutzerdefinierte Menübandaktion** aus, nennen Sie sie **AddEmployeeToCorpDB**, und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-146">In the  **Add New Item** dialog, select **Ribbon Custom Action**, give it the name AddEmployeeToCorpDB, and then click  **Add**.</span></span>

4. <span data-ttu-id="e1f1b-p110">In dem Dialogfeld, das geöffnet wird, werden drei Fragen gestellt. Geben Sie die folgenden Antworten ein:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-p110">The dialog that opens asks three questions. Give the following answers:</span></span>

   |<span data-ttu-id="e1f1b-149">**Frage**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-149">**Question**</span></span>|<span data-ttu-id="e1f1b-150">**Geben Sie die folgende Antwort ein:**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-150">**Give this answer:**</span></span>|
   |:-----|:-----|
   |<span data-ttu-id="e1f1b-151">**Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-151">**Where do you want to expose the custom action?**</span></span>|<span data-ttu-id="e1f1b-152">Hostweb</span><span class="sxs-lookup"><span data-stu-id="e1f1b-152">Host Web</span></span>|
   |<span data-ttu-id="e1f1b-153">**Wo gilt die benutzerdefinierte Aktion?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-153">**Where is the custom action scoped to?**</span></span>|<span data-ttu-id="e1f1b-154">Listeninstanz</span><span class="sxs-lookup"><span data-stu-id="e1f1b-154">List Instance</span></span>|
   |<span data-ttu-id="e1f1b-155">**Für welches spezielle Element gilt die benutzerdefinierte Aktion?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-155">**Which particular item is the custom action scoped to?**</span></span>|<span data-ttu-id="e1f1b-156">Lokale Mitarbeiter</span><span class="sxs-lookup"><span data-stu-id="e1f1b-156">Local Employees</span></span>|

5. <span data-ttu-id="e1f1b-157">Klicken Sie auf **Weiter**, und Sie erhalten drei weitere Fragen:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-157">Click  **Next** and you get three more questions:</span></span>

   |<span data-ttu-id="e1f1b-158">**Frage**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-158">**Question**</span></span>|<span data-ttu-id="e1f1b-159">**Geben Sie die folgende Antwort ein:**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-159">**Give this answer:**</span></span>|
   |:-----|:-----|
   |<span data-ttu-id="e1f1b-160">**Wo befindet sich das Steuerelement?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-160">**Where is the control located?**</span></span>|<span data-ttu-id="e1f1b-161">Ribbon.ListItem.Actions</span><span class="sxs-lookup"><span data-stu-id="e1f1b-161">Ribbon.ListItem.Actions</span></span>|
   |<span data-ttu-id="e1f1b-162">**Was ist die Beschriftung für das Schaltflächen-Steuerelement?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-162">**What is the label text for the button control?**</span></span>|<span data-ttu-id="e1f1b-163">Zur Unternehmensdatenbank hinzufügen</span><span class="sxs-lookup"><span data-stu-id="e1f1b-163">Add to Corporate DB</span></span>|
   |<span data-ttu-id="e1f1b-164">**Wohin navigiert das Schaltflächen-Steuerelement?**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-164">**Where does the button control navigate to?**</span></span>|<span data-ttu-id="e1f1b-165">ChainStoreWeb\Pages\EmployeeAdder.aspx</span><span class="sxs-lookup"><span data-stu-id="e1f1b-165">ChainStoreWeb\Pages\EmployeeAdder.aspx</span></span><br/><span data-ttu-id="e1f1b-166">(Dies ist eine Seite, deren zugrunde liegender Code den Mitarbeiter zur Datenbank hinzufügt.)</span><span class="sxs-lookup"><span data-stu-id="e1f1b-166">ChainStoreWeb\Pages\EmployeeAdder.aspx (This is a page whose code behind is going to add the employee to the database.)</span></span>|

6. <span data-ttu-id="e1f1b-167">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-167">Click  **Finish**.</span></span>
    
   <span data-ttu-id="e1f1b-168">Eine Datei „elements.xml“, die die benutzerdefinierte Aktion definiert, wird dem Projekt hinzugefügt und geöffnet.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-168">An elements.xml file that defines the add-in part is added to the project and opened.</span></span> <span data-ttu-id="e1f1b-169">In den meisten Fällen können Sie diese Datei als Blackbox betrachten; Sie werden erst in einem späteren Artikel in dieser Reihe Änderungen daran vornehmen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-169">An elements.xml file that defines the custom action is added to the project and opened. For the most part, you can treat this file as a black box, and you won't need to make any changes in it untill a later article in this series. For now, note only the following:</span></span> <span data-ttu-id="e1f1b-170">Beachten Sie für den Moment Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-170">For now, note only the following:</span></span>

   - <span data-ttu-id="e1f1b-171">Das **Location**-Attribut des **CommandUIDefinition**-Elements hat den Wert `Ribbon.ListItem.Actions.Controls_children`.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-171">The  **Location** attribute of the **CommandUIDefinition** element has the value `Ribbon.ListItem.Actions.Controls_children`.</span></span> <span data-ttu-id="e1f1b-172">Der zweite Teil davon, `ListItem`, identifiziert die *Registerkarte* auf dem Menüband, auf der die Schaltfläche platziert wird (dies ist aber möglicherweise nicht genau der Anzeigename der Registerkarte).</span><span class="sxs-lookup"><span data-stu-id="e1f1b-172">The  Location attribute of the *CommandUIDefinition* element has the value . The second part of this,  `ListItem`, identifies the tab on the ribbon where the button will be placed (but that may not be the exact display name of the tab) and the third part,  , is the name of the section of the ribbon where the button will be placed.</span></span> <span data-ttu-id="e1f1b-173">Der dritte Teil, `Actions`, ist der Name des *Abschnitts* des Menübands, in dem die Schaltfläche platziert wird.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-173">The third part, `Actions`, is the name of the *section* of the ribbon where the button will be placed.</span></span>

   - <span data-ttu-id="e1f1b-p113">Das Attribut **CommandAction** des Elements **CommandUIHandler** beginnt mit dem Platzhalter `~remoteAppUrl`. Dieser wird bei der Bereitstellung der Schaltfläche ersetzt durch die URL der Remotewebanwendung.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-p113">The  **CommandAction** attribute of the **CommandUIHandler** element begins with the placeholder `~remoteAppUrl`. This will be replaced with the URL of the remote web application when the button is deployed.</span></span>

   - <span data-ttu-id="e1f1b-176">Dem Wert **CommandAction** wurden einige Abfrageparameter mit Platzhalterwerte in Klammern „{ }“ hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-176">A few query parameters have been added to the **CommandAction** value with placeholder values in braces "{ }".</span></span> <span data-ttu-id="e1f1b-177">Diese Platzhalter werden zur Laufzeit aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-177">These placeholders are resolved at runtime.</span></span> <span data-ttu-id="e1f1b-178">Beachten Sie, dass einer der Platzhalter die ID des Listenelements ist, das vom Benutzer ausgewählt wurde, bevor die benutzerdefinierte Schaltfläche auf dem Menüband ausgewählt wurde.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-178">A few query parameters have been added to the  CommandAction value with placeholder values in braces "{ }". These placeholders are resolved at runtime. Note that one of them is the ID of the list item that is selected by the user before she presses the custom button on the ribbon.</span></span>

7. <span data-ttu-id="e1f1b-179">Öffnen Sie im Projekt **ChainStoreWeb** die Datei **Pages/EmployeeAdder.aspx**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-179">In the **ChainStoreWeb** project, open the **Pages/EmployeeAdder.aspx** file.</span></span> <span data-ttu-id="e1f1b-180">Beachten Sie, dass diese keine Benutzeroberfläche aufweist.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-180">Notice that it doesn't have any UI.</span></span> <span data-ttu-id="e1f1b-181">Dass Add-In verwendet diese Seite als eine Art Webdienst.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-181">The add-in is going to use this page as a kind of web service.</span></span> <span data-ttu-id="e1f1b-182">Dies ist möglich, da die **System.Web.UI.Page**-Klasse von ASP.NET **System.Web.IHttpHandler** implementiert und da das **Page\_Load**-Ereignis automatisch ausgeführt wird, wenn die Seite angefordert wird.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-182">In the  ChainStoreWeb project, open the Pages/EmployeeAdder.aspx file. Notice that it doesn't have any UI. The add-in is going to use this page as a kind of web service. This is possible because the ASP.NET **System.Web.UI.Page** class implements **System.Web.IHttpHandler** and because the **Page\_Load** event runs automatically when the page is requested.</span></span>  
 
8. <span data-ttu-id="e1f1b-183">Öffnen Sie die Code-Behind-Datei **Pages/EmployeeAdder.aspx.cs**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-183">Open the code-behind file **Pages/EmployeeAdder.aspx.cs**.</span></span> <span data-ttu-id="e1f1b-184">Die Methode, die den Mitarbieter zu der Remotedatenbank hinzufügt (`AddLocalEmployeeToCorpDB`) ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-184">The method that adds the employee to the remote database, `AddLocalEmployeeToCorpDB`, is already present.</span></span> <span data-ttu-id="e1f1b-185">Sie verwendet das **SharePointContext**-Objekt, um die URL des Hostwebs abzurufen, die das Add-In als Mandantendiskriminator verwendet.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-185">It uses the **SharePointContext** object to get the host web's URL, which the add-in uses as its tenant discriminator.</span></span> <span data-ttu-id="e1f1b-186">Das erste, was die **Page_Load**-Methode tun muss, ist die Initialisierung des Objekts.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-186">The first thing the **Page_Load** method needs to do is initialize this object.</span></span> <span data-ttu-id="e1f1b-187">Das Objekt wird erstellt und in der Sitzung zwischengespeichert, wenn die Startseite des Add-Ins geladen wird, fügen Sie den folgenden Code daher zur **Page_Load**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-187">The object is created and cached in the Session when the add-in's start page loads, so add the following code to the **Page_Load** method.</span></span> <span data-ttu-id="e1f1b-188">(Das **SharePointContext**-Objekt wird in der Datei „SharePointContext.cs“ definiert, die von den Office-Entwicklertools für Visual Studio generiert wird, wenn die Add-In-Lösung erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-188">(The **SharePointContext** object is defined in the SharePointContext.cs file that the Office Developer Tools for Visual Studio generates when the add-in solution is created.)</span></span>
    
    ```C#
      spContext = Session["SPContext"] as SharePointContext;
    ```

9. <span data-ttu-id="e1f1b-189">Da die `AddLocalEmployeeToCorpDB`-Methode den Namen des Mitarbeiters als Parameter akzeptiert, fügen Sie die folgende Zeile zur **Page_Load**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-189">The  `AddLocalEmployeeToCorpDB` method takes the employee's name as a parameter, so add the following line to the **Page_Load** method. You'll create the  method in a later step.</span></span> <span data-ttu-id="e1f1b-190">Sie erstellen die `GetLocalEmployeeName`-Methode in einem späteren Schritt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-190">You will create the  `GetLocalEmployeeName` object and  method in a later step.</span></span>
    
    ```C#
      // Read from SharePoint 
    string employeeName = GetLocalEmployeeName();
    ```

10. <span data-ttu-id="e1f1b-191">Fügen Sie unterhalb dieser Zeile den Aufruf der `AddLocalEmployeeToCorpDB`-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-191">Below this line, add the call to the  `AddLocalEmployeeToCorpDB` method.</span></span>
    
    ```C#
      // Write to remote database 
    AddLocalEmployeeToCorpDB(employeeName);
    ```

11. <span data-ttu-id="e1f1b-p118">Fügen Sie eine **using**-Anweisung zur Datei für den Namespace  `Microsoft.SharePoint.Client` hinzu. (Die Office-Entwicklertools für Visual Studio enthielten die Microsoft.SharePoint.Client-Assembly im **ChainStoreWeb**-Projekt, als dieses erstellt wurde.)</span><span class="sxs-lookup"><span data-stu-id="e1f1b-p118">Add a **using** statement to file for the namespace `Microsoft.SharePoint.Client`. (The Office Developer Tools for Visual Studio included the Microsoft.SharePoint.Client assembly in the **ChainStoreWeb** project when it was created.)</span></span>
    
12. <span data-ttu-id="e1f1b-194">Fügen Sie der `EmployeeAdder`-Klasse jetzt die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-194">Add the following method to the  `EmployeeAdder` class.</span></span> <span data-ttu-id="e1f1b-195">Das clientseitige SharePoint .NET-Objektmodell (CSOM) wird an einer anderen Stelle in MSDN ausführlich beschrieben, und es wird empfohlen, dass Sie sich dieses genauer ansehen, wenn Sie mit dieser Artikelreihe fertig sind.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-195">The SharePoint .NET Client-side Object Model (CSOM) is documented in detail elsewhere on MSDN, and we encourage you to explore it when you are finished with this series of articles.</span></span> <span data-ttu-id="e1f1b-196">Beachten Sie, dass in diesem Artikel die **ListItem**-Klasse ein Element in einer SharePoint-Liste darstellt und dass auf einen Wert eines Felds in dem Element mit der „indexer“-Syntax verwiesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-196">For this article, note that the **ListItem** class represents an item in a SharePoint list, and that the value of a field in the item can be referenced with "indexer" syntax.</span></span> <span data-ttu-id="e1f1b-197">Beachten Sie außerdem, dass der Code das Feld als **Titel** bezeichnet, obwohl Sie den Feldnamen in **Name** geändert haben.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-197">Also notice that the code refers to the field as **Title** even though you changed the field name to **Name**.</span></span> <span data-ttu-id="e1f1b-198">Dies liegt daran, dass Felder im Code immer mit ihrem *internen* Namen und nicht mit ihrem Anzeigenamen bezeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-198">This is because fields are always referred to in code by their *internal* name, not their display name.</span></span> <span data-ttu-id="e1f1b-199">Der interne Name eines Felds wird festgelegt, wenn das Feld erstellt wird, und kann nie geändert werden.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-199">The internal name of a field is set when the field is created and can never change.</span></span> <span data-ttu-id="e1f1b-200">Sie schließen den `TODO1` in einem späteren Schritt ab.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-200">You will create the  `TODO1` object and  method in a later step.</span></span>
    
    ```C#
      private string GetLocalEmployeeName()
    {
        ListItem localEmployee;

        // TODO1: Initialize the localEmployee object by getting  
        // the item from SharePoint.

        return localEmployee["Title"].ToString();
    }
    ```

13. <span data-ttu-id="e1f1b-201">Unser Code benötigt die ID des Listenelements, bevor dieser aus SharePoint abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-201">Our code will need the list item's ID before it can retrieve it from SharePoint. Add the following declaration to the   class just below the declaration for the  object.</span></span> <span data-ttu-id="e1f1b-202">Fügen Sie die folgende Deklaration der `EmployeeAdder`-Klasse direkt unter der Deklaration für das `spContext`-Objekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-202">Add the following declaration to the `EmployeeAdder` class just under the declaration for the `spContext` object.</span></span>
    
    ```C#
      private int listItemID;
    ```

14. <span data-ttu-id="e1f1b-203">Fügen Sie jetzt die folgende Methode der `EmployeeAdder`-Klasse hinzu, um die ID dieses Listenelements aus dem Abfrageparameter abzurufen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-203">Now add the following method to the  `EmployeeAdder` class to get the list item's ID from the query parameter.</span></span>
    
    ```C#
      private int GetListItemIDFromQueryParameter()
    {
        int result;
        Int32.TryParse(Request.QueryString["SPListItemId"], out result);
        return result;
    }
    ```

15. <span data-ttu-id="e1f1b-204">Um die `listItemID`-Variable zu initialisieren, fügen Sie der **Page_Load**-Methode die folgende Zeile unter der Zeile hinzu, die die `spContext`-Variable initialisiert.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-204">To initialize the  `listItemID` variable, add the following line to the **Page_Load** method just below the line that initializes the `spContext` variable.</span></span>
    
    ```C#
      listItemID = GetListItemIDFromQueryParameter();
    ```

16. <span data-ttu-id="e1f1b-205">Ersetzen Sie in `GetLocalEmployeeName` die Zeile `TODO1` durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-205">In the TasksCalendarWebPart class replace the displayTasks and updateTask methods with the following code:</span></span> <span data-ttu-id="e1f1b-206">Behandeln Sie diesen Code vorerst wie eine Blackbox, solange wir uns auf das darauf konzentrieren, die benutzerdefinierte Schaltfläche zum Laufen zu bringen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-206">For the time being, just treat this code as a black box while we concentrate on getting the custom button working.</span></span> <span data-ttu-id="e1f1b-207">Im nächsten Artikel in dieser Reihe, in der es um das clientseitige SharePoint-Objektmodell geht, erfahren Sie mehr über diesen Code.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-207">In the  , replace the   with the following code. For the time being, just treat this code as a black box while we concentrate on getting the custom button working. We'll learn more about this code in the next article in this series, which is all about the SharePoint client-side object model.</span></span>
    
    ```C#
      using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        localEmployee = localEmployeesList.GetItemById(listItemID);
        clientContext.Load(localEmployee);
        clientContext.ExecuteQuery();
    }

    ```

   <span data-ttu-id="e1f1b-208">Die gesamte Methode sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-208">The entire method should now look like the following.</span></span>

    ```C#
      private string GetLocalEmployeeName()
     {
         ListItem localEmployee;

         using (var clientContext = spContext.CreateUserClientContextForSPHost())
         {
             List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
             selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
             clientContext.Load(selectedLocalEmployee);
             clientContext.ExecuteQuery();
         }
         return localEmployee["Title"].ToString();
     }
     ```

17. <span data-ttu-id="e1f1b-209">Die Seite „EmployeeAdder“ sollte tatsächlich nicht gerendert werden, fügen Sie Folgendes als letzte Zeile in der **Page_Load**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-209">The EmployeeAdder page should not actually render, so add the following as the last line in the  **Page_Load** method. This will redirect the browser back to the list view page for the Local Employees list.</span></span> <span data-ttu-id="e1f1b-210">Dadurch wird der Browser zurück zur Listenansichtsseite für die **Local Employees**-Liste geleitet.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-210">This redirects the browser back to the list view page for the **Local Employees** list.</span></span>
    
    ```C#
      // Go back to the Local Employees page
    Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);

    ```

   <span data-ttu-id="e1f1b-211">Die gesamte **Page_Load**-Methode sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-211">The entire method should now look like the following.</span></span>

    ```C#
          protected void Page_Load(object sender, EventArgs e)
        {
            spContext = Session["SPContext"] as SharePointContext;
            listItemID = GetListItemIDFromQueryParameter();

            // Read from SharePoint
            string employeeName = GetLocalEmployeeName();

            // Write to remote database
            AddLocalEmployeeToCorpDB(employeeName);

            // Go back to the preceding page
            Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);
        }
    ```


## <a name="request-permission-to-read-the-host-web-list"></a><span data-ttu-id="e1f1b-212">Anfordern der Berechtigung zum Lesen der Hostwebliste</span><span class="sxs-lookup"><span data-stu-id="e1f1b-212">Request permission to read the host web list</span></span>

<span data-ttu-id="e1f1b-213">Wie Sie bereits gesehen haben, werden Sie in SharePoint aufgefordert, die Add-In-Berechtigungen zum Hostweb hinzuzufügen, wenn es installiert wird.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-213">As you have seen, SharePoint prompts you to grant the add-in permissions to the host web when it is installed.</span></span> <span data-ttu-id="e1f1b-214">Jedes Mal, wenn Sie F5 drücken, haben Sie das Add-In erneut installiert.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-214">You have been re-installing the add-in every time you select F5.</span></span> <span data-ttu-id="e1f1b-215">Bisher benötigte das Add-In nur minimale Berechtigungen, die `GetLocalEmployeeName`-Methode benötigt jedoch die Berechtigung zum Lesen der Listen der Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-215">So far, the add-in has only needed minimal permissions, but the `GetLocalEmployeeName` method requires permission to read the lists of the host website.</span></span> <span data-ttu-id="e1f1b-216">Das Add-In verwendet sein Add-In-Manifest, um SharePoint mitzuteilen, welche Berechtigungen es benötigt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-216">The add-in uses its add-in manifest to tell SharePoint what permissions it needs.</span></span> <span data-ttu-id="e1f1b-217">Führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-217">Follow these steps.</span></span>

1. <span data-ttu-id="e1f1b-218">Öffnen Sie im **Projektmappen-Explorer** die Datei AppManifest.xml im **ChainStore**-Projekt. (Die Datei heißt AppManifest, da Add-Ins früher als „Apps" bezeichnet wurden.)</span><span class="sxs-lookup"><span data-stu-id="e1f1b-218">In  **Solution Explorer**, open the AppManifest.xml file in the  **ChainStore** project. (The file is called AppManifest because add-ins used to be called "apps".) The manifest designer opens.</span></span> <span data-ttu-id="e1f1b-219">Der Manifest-Designer wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-219">The application designer opens.</span></span>

2. <span data-ttu-id="e1f1b-220">Öffnen Sie die Registerkarte **Berechtigungen**, wählen Sie die leere Zelle unter der Spalte **Bereich** aus, und wählen Sie dann **Liste** aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-220">Open the  **Permissions** tab and click the empty cell under the **Scope** column; and then select **List** from the drop down.</span></span>

3. <span data-ttu-id="e1f1b-221">Wählen Sie im Feld **Berechtigung** die Option **Lesen** aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-221">In the  **Permission** field, select **Read** from the drop down.</span></span>

4. <span data-ttu-id="e1f1b-222">Lassen Sie das Feld **Eigenschaften** leer, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-222">Leave the  **Properties** field empty and save the file. The Permission tab should look similar to the following:</span></span> <span data-ttu-id="e1f1b-223">Die Registerkarte **Berechtigungen** sollte etwa wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-223">Choose  OK. The  **Permissions** tab should now look similar to the following:</span></span>

   <span data-ttu-id="e1f1b-224">*Abbildung 2. Die Registerkarte „Berechtigungen“*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-224">*Figure 2. Permissions tab*</span></span>

   ![Die Registerkarte „Berechtigungen“ im Add-In-Manifest-Designer zeigt den Bereich „Liste“ und die Berechtigung „Lesen“.](../images/8dd2a25f-103a-42af-aa88-c8ec796315db.PNG)


## <a name="run-the-add-in-and-test-the-button"></a><span data-ttu-id="e1f1b-226">Ausführen des Add-Ins und Testen der Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="e1f1b-226">Run the add-in and test the button</span></span>

1. <span data-ttu-id="e1f1b-227">Verwenden Sie die F5-Taste, um Ihr Add-In bereitzustellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-227">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="e1f1b-228">Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-228">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="e1f1b-229">Visual Studio führt zudem eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-229">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="e1f1b-230">Sie werden aufgefordert, Berechtigungen für das Add-In zu erteilen, bevor die Startseite geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-230">You are prompted to grant permissions to the add-in before its start page opens.</span></span> <span data-ttu-id="e1f1b-231">Dieses Mal weist die Aufforderung ein Dropdownmenü auf, in dem Sie die Liste auswählen, die die App zum Lesen benötigt, wie im folgenden Screenshot dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-231">This time the prompt has a drop-down where you select the list that the app needs to read as seen in the following screenshot.</span></span> 
  
   <span data-ttu-id="e1f1b-232">*Abbildung 3. SharePoint-Add-In-Berechtigungsaufforderung*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-232">*Figure 3. SharePoint add-in permission prompt*</span></span>

   ![Die SharePoint-Add-In-Berechtigungsaufforderung; die Liste „Lokale Mitarbeiter“ ist in der Dropdownliste „Darf Elemente in der Liste lesen“ ausgewählt.](../images/84e8b42c-4800-4947-acbd-21c6f096f4ea.PNG)

2. <span data-ttu-id="e1f1b-234">Wählen Sie **Lokale Mitarbeiter** aus der Liste aus, und klicken Sie dann auf **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-234">Choose  **Local Employees** from the list and then click **Trust it**.</span></span>

3. <span data-ttu-id="e1f1b-235">Wenn die Add-In-Startseite geöffnet wird, klicken Sie auf **Zurück zur Website** im Chromesteuerelement im oberen Bereich.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-235">When the add-in's start page opens, select the  **Back to Site** link on the chrome control at the top.</span></span>

4. <span data-ttu-id="e1f1b-236">Gehen Sie auf der Startseite der Website zu **Websiteinhalte** > **Lokale Mitarbeiter**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-236">From the website's home page, go to **Site Contents** > **Local Employees**.</span></span> <span data-ttu-id="e1f1b-237">Die Listenansichtsseite wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-237">The list view page opens.</span></span>

5. <span data-ttu-id="e1f1b-238">Fügen Sie der Liste ein paar Mitarbeiter hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-238">Add a few employees to the list.  Do not check the  Added to Corporate DB checkbox.</span></span> <span data-ttu-id="e1f1b-239">*Aktivieren Sie das Kontrollkästchen __Zur Unternehmensdatenbank hinzugefügt__ nicht.*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-239">*Do not select the __Added to Corporate DB__ check box.*</span></span> 

6. <span data-ttu-id="e1f1b-240">Öffnen Sie auf dem Menüband die Registerkarte **Elemente**. Im Abschnitt **Aktionen** der Registerkarte wird die benutzerdefinierte Schaltfläche **Zur Unternehmensdatenbank hinzufügen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-240">On the ribbon, open the  **Items** tab. In the **Actions** section of the tab, is the custom button **Add to Corporate DB**.</span></span>

7. <span data-ttu-id="e1f1b-241">Wählen Sie ein Element in der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-241">Select an item from the list box.</span></span> <span data-ttu-id="e1f1b-242">Die Seite und das Menüband sollten in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-242">Select an item on the list. The page and ribbon should look similar to the following:</span></span>

   <span data-ttu-id="e1f1b-243">*Abbildung 4. Die Liste „Lokale Mitarbeiter“*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-243">*Figure 4. Local Employees list*</span></span>  

   ![Die Lister der lokalen Mitarbeiter.](../images/797a5ceb-7291-4b62-8075-2bb6a1b8e8a1.PNG)

8. <span data-ttu-id="e1f1b-247">Klicken Sie nach dem Auswählen eines Elements in der Liste auf **Zur Unternehmensdatenbank hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-247">After selecting an item in the list, select **Add to Corporate DB**.</span></span> 

9. <span data-ttu-id="e1f1b-248">Die Seite scheint neu geladen zu werden, da die **Page_Load**-Methode der Seite „EmployeeAdder“ eine direkte Umleitung aufweist.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-248">The page will seem to reload because the  **Page_Load** method of the EmployeeAdder page redirects back to it.</span></span>

10. <span data-ttu-id="e1f1b-249">Klicken Sie im Browser zweimal auf die Schaltfläche „Zurück“, um zurück zur Startseite für das Add-In zu navigieren.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-249">Use the browser's back button twice to go back to the add-in's start page.</span></span> 

11. <span data-ttu-id="e1f1b-250">Klicken Sie auf **Mitarbeiter anzeigen**, und die Liste der Mitarbeiter wird mit dem Mitarbeiter, den Sie hinzugefügt haben, aufgefüllt.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-250">Click  **Show Employees** and the list of employees will be populated with the employee that you added. It should look similar to the following:</span></span> <span data-ttu-id="e1f1b-251">Sie sollte etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-251">The calendar should look similar to the following:</span></span>

   <span data-ttu-id="e1f1b-252">*Abbidlung 5. Die Liste der Unternehmensmitarbeiter auf der Startseite des Add-Ins*</span><span class="sxs-lookup"><span data-stu-id="e1f1b-252">*Figure 5. Corporate employees list on the add-in start page*</span></span> 

   ![Die Liste der Unternehmensmitarbeiter auf der Startseite des Add-Ins mit Anzeige des Mitarbeiters, der in einem früheren Schritt ausgewählt wurde.](../images/4a300a4e-f479-4f63-b536-6315c5d9ba4d.PNG)

12. <span data-ttu-id="e1f1b-254">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-254">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="e1f1b-255">Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-255">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

13. <span data-ttu-id="e1f1b-256">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-256">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="e1f1b-257">Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-257">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f1b-258">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e1f1b-258">Next steps</span></span>
<span data-ttu-id="e1f1b-259"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="e1f1b-259"></span></span>

<span data-ttu-id="e1f1b-260">In diesem Artikel legen Sie eine kurze Pause vom Codieren ein, um einen [schnellen Überblick über das SharePoint-Clientobjektmodell (CSOM) zu erhalten](get-a-quick-overview-of-the-sharepoint-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1f1b-260">In the next article, we'll take a brief break from coding for an overview of the SharePoint client-side object model: [Get a quick overview of the SharePoint object model](get-a-quick-overview-of-the-sharepoint-object-model.md).</span></span>
 

 

