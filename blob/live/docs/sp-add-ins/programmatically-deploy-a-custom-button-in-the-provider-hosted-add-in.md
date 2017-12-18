---
title: "Programmgesteuertes Bereitstellen einer benutzerdefinierten Schaltfläche in anbietergehosteten Add-Ins"
description: "Hier erfahren Sie, wie Sie eine benutzerdefinierte Menübandschaltfläche bei einer benutzerdefinierten Liste in Ihrem zuvor erstellten anbietergehosteten SharePoint-Add-In registrieren können."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 0fc7f5e8d4255f103413d9f49750d7d3365a2562
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="57855-103">Programmgesteuertes Bereitstellen einer benutzerdefinierten Schaltfläche in anbietergehosteten Add-Ins</span><span class="sxs-lookup"><span data-stu-id="57855-103">Programmatically deploy a custom button in the provider-hosted add-in</span></span>

<span data-ttu-id="57855-104">Dies ist der neunte Artikel in unserer Artikelreihe über die Grundlagen der Entwicklung von anbietergehosteten SharePoint-Add-Ins. Vor der Lektüre dieses Artikels sollten Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) vertraut machen und die vorherigen Artikel der Reihe lesen:</span><span class="sxs-lookup"><span data-stu-id="57855-104">This is the ninth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="57855-105">Get started creating provider-hosted SharePoint Add-ins</span><span class="sxs-lookup"><span data-stu-id="57855-105">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="57855-106">Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-106">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
-  [<span data-ttu-id="57855-107">Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-107">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="57855-108">Schnelle Übersicht über das SharePoint-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="57855-108">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model.md)
-  [<span data-ttu-id="57855-109">Hinzufügen von SharePoint-Schreibvorgängen zum vom Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-109">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="57855-110">Einfügen eines Add-In-Webparts in das vom Anbieter gehostete Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-110">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="57855-111">Verarbeiten von Add-In-Ereignissen im vom Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-111">Handle add-in events in the provider-hosted add-in</span></span>](handle-add-in-events-in-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="57855-112">Hinzufügen der Logik für die erste Ausführung zum vom Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="57855-112">Add first-run logic to the provider-hosted add-in</span></span>](add-first-run-logic-to-the-provider-hosted-add-in.md)

> [!NOTE]
> <span data-ttu-id="57855-113">Wenn Sie unsere Artikelreihe zum Thema anbietergehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können.</span><span class="sxs-lookup"><span data-stu-id="57855-113">Note  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_Provider-hosted_Add-Ins_Tutorials and open the BeforeAdd-inPart.sln file.</span></span> <span data-ttu-id="57855-114">Alternativ können Sie das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeProgrammaticButton.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="57855-114">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeProgrammaticButton.sln file.</span></span>

<span data-ttu-id="57855-115">In diesem Artikel erfahren Sie, wie Sie eine benutzerdefinierte Menübandschaltfläche in ein SharePoint-Add-In einfügen können, wenn die Liste, deren Menüband die Schaltfläche abruft, selbst programmgesteuert in dem betreffenden Add-In bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="57855-115">In this article you will learn how to include a custom ribbon button in the a SharePoint Add-in when the list whose ribbon gets the button is itself being programmatically deployed in the very same add-in.</span></span>

## <a name="re-add-the-custom-button-to-the-project"></a><span data-ttu-id="57855-116">Erneutes Hinzufügen der benutzerdefinierten Schaltfläche zum Projekt</span><span class="sxs-lookup"><span data-stu-id="57855-116">Re-add the custom button to the project</span></span>

> [!NOTE]
> <span data-ttu-id="57855-117">Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach jedem erneuten Öffnen der Lösung wieder auf die Standardwerte zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="57855-117">NOTE The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> <span data-ttu-id="57855-118">Wann immer Sie beim Durcharbeiten dieser Artikelreihe die Beispiellösung erneut öffnen, müssen Sie umgehend die folgenden Schritte durchführen:</span><span class="sxs-lookup"><span data-stu-id="57855-118">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 
> 1. <span data-ttu-id="57855-119">Klicken Sie oben im **Projektmappen-Explorer** mit der rechten Maustaste auf den Lösungsknoten, und wählen Sie die Option **Startprojekte festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="57855-119">Right-click the solution node at the top of  **Solution Explorer** and select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="57855-120">Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="57855-120">Make sure all three projects are set to  **Start** in the **Action** column.</span></span>

<span data-ttu-id="57855-121">Im vorherigen Artikel haben Sie die benutzerdefinierte Menübandschaltfläche **AddEmployeeToCorpDB** aus dem Projekt entfernt.</span><span class="sxs-lookup"><span data-stu-id="57855-121">In the previous article you removed the custom  **AddEmployeeToCorpDB** ribbon button from the project. Add it back in with these steps below.</span></span> <span data-ttu-id="57855-122">Gehen Sie nun wie folgt vor, um sie dem Projekt wieder hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="57855-122">Add it back in with the following steps.</span></span>

1. <span data-ttu-id="57855-123">Klicken Sie auf der Symbolleiste oben im **Projektmappen-Explorer** auf die Schaltfläche **Alle Dateien anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="57855-123">On the toolbar at the top of **Solution Explorer**, select the **Show All Files** button.</span></span>

   <span data-ttu-id="57855-124">*Abbildung 1: Symbolleiste im Projektmappen-Explorer*</span><span class="sxs-lookup"><span data-stu-id="57855-124">*Figure 1. Solution Explorer toolbar*</span></span>

   ![Symbolleiste im Projektmappen-Explorer mit einem Kästchen um die Schaltfläche „Alle Dateien anzeigen“](../images/f6b035f5-1aa7-452a-8f59-9dd44b062d06.PNG)

2. <span data-ttu-id="57855-126">Klicken Sie im Projekt **ChainStore** mit der rechten Maustaste auf **AddEmployeeToCorpDB**, und wählen Sie die Option **Zu Projekt hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="57855-126">In the  **ChainStore** project, right-click **AddEmployeeToCorpDB** and select **Include in Project**.</span></span>

3. <span data-ttu-id="57855-127">Klicken Sie erneut auf die Schaltfläche **Alle Dateien anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="57855-127">Press the  **Show All Files** button again.</span></span>

4. <span data-ttu-id="57855-128">Erweitern Sie im Projekt **ChainStore** das Element **AddEmployeeToCorpDB**, und öffnen Sie die Datei „elements.xml".</span><span class="sxs-lookup"><span data-stu-id="57855-128">In the  **ChainStore** project, expand **AddEmployeeToCorpDB** and then open the elements.xml file.</span></span>

## <a name="understand-a-dilemma-and-its-solution"></a><span data-ttu-id="57855-129">Ein Problem und seine Lösung</span><span class="sxs-lookup"><span data-stu-id="57855-129">Understand a dilemma and its solution</span></span>

<span data-ttu-id="57855-p104">In der Datei „elements.xml" identifiziert das Attribut **RegistrationId** des Elements **CustomAction** die Liste, auf deren Menüband die Schaltfläche hinzugefügt wird: `{$ListId:Lists/Local Employees;}`. Das hat einwandfrei funktioniert, als die Liste bereits manuell zum Hostweb hinzugefügt wurde. Aber jetzt, da die Liste programmgesteuert in der zuerst ausgeführten Logik bereitgestellt wird, ist die Liste nicht vorhanden, wenn SharePoint das Add-In installiert und versucht, die Schaltfläche bereitzustellen. Bei der Installation des Add-Ins wird eine Ausnahme ausgelöst, und es treten Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="57855-p104">In the elements.xml file, the **RegistrationId** attribute of the **CustomAction** element identifies the list on whose ribbon the button is added: `{$ListId:Lists/Local Employees;}`. This worked fine when the list had already been added to the host web manually. But now that we are deploying the list programmatically in first-run logic, the list doesn't exist when SharePoint installs the add-in and tries to deploy the button. The installation of the add-in would throw an exception and fail.</span></span>

<span data-ttu-id="57855-134">Eine Bereitstellung der Liste im Installationsereignishandler statt in der zuerst auszuführenden Logik wird das Problem nicht lösen, da SharePoint benutzerdefinierte deskriptiv definierte Komponenten wie die benutzerdefinierte Schaltfläche (und das Add-In-Part **Bestellung aufgeben**) bereitstellt, *bevor* der benutzerdefinierte Handler ausgeführt wird. Die Liste wird also nicht vorhanden sein, wenn SharePoint versucht, die Schaltfläche bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="57855-134">Deploying the list in the installation event handler, instead of first-run logic, won't solve the dilemma because SharePoint deploys custom descriptively-defined components, such as the custom button (and the **Place Order** add-in part), *before*  it runs the custom handler, so the list won't exist when SharePoint tries to deploy the button.</span></span>

<span data-ttu-id="57855-135">Eine vollständig programmgesteuerte Erstellung von benutzerdefinierten Schaltflächen ist aus verschiedenen Gründen nicht zweckmäßig. Deren Erörterung würde jedoch den Rahmen dieses Artikels sprengen.</span><span class="sxs-lookup"><span data-stu-id="57855-135">Creating a custom button entirely programmatically is not practical for reasons that are too advanced to discuss here.</span></span> <span data-ttu-id="57855-136">Glücklicherweise ist eine solche vollständig programmgesteuerte Erstellung auch nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="57855-136">Fortunately, it is not necessary.</span></span> <span data-ttu-id="57855-137">Es gibt eine relativ unkomplizierte Methode, benutzerdefinierte Schaltflächen halb-programmgesteuert zu erstellen und einer benutzerdefinierten Liste zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="57855-137">There is a relatively painless way to semi-programmatically create a custom button and assign it to a custom list.</span></span> 

<span data-ttu-id="57855-138">Gehen Sie dazu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="57855-138">The following are the steps to take.</span></span>

1. <span data-ttu-id="57855-139">Behalten Sie die deskriptiv definierte Schaltfläche im Projekt bei, aber weisen Sie diese dem Menüband von etwas zu, das immer auf SharePoint-Websites vorhanden ist, statt einer Liste,die programmgesteuert mit demselben Add-In bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="57855-139">Keep the descriptively defined button in the project, but assign it to the ribbon of something that always exists on SharePoint sites, instead of to a list that's programmatically deployed with the same add-in.</span></span> 

2. <span data-ttu-id="57855-140">Fügen Sie in der zuerst auszuführenden Logik (First-Run-Logik) nach dem Code für die programmgesteuerte Erstellung der Liste programmgesteuert eine nicht definierte Schaltfläche zum Menüband der Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="57855-140">In the first-run logic, after the list is programmatically created, programmatically add an undefined button to the ribbon of the list.</span></span>

3. <span data-ttu-id="57855-141">Initialisieren Sie die Eigenschaften der neuen Schaltfläche mit den Werten der ursprünglichen Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="57855-141">Initialize the properties of the new button with the values of the original button.</span></span> <span data-ttu-id="57855-142">Jetzt existieren zwei identische Schaltflächen.</span><span class="sxs-lookup"><span data-stu-id="57855-142">At this point there are two identical buttons.</span></span> <span data-ttu-id="57855-143">Die zweite Schaltfläche ist dem Menüband der Liste **Lokale Mitarbeiter** zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="57855-143">The second is assigned to the ribbon of the **Local Employees** list.</span></span>

4. <span data-ttu-id="57855-144">Löschen Sie die ursprüngliche Schaltfläche programmgesteuert.</span><span class="sxs-lookup"><span data-stu-id="57855-144">Programmatically delete the original button.</span></span>

## <a name="programmatically-register-the-custom-button"></a><span data-ttu-id="57855-145">Programmgesteuertes Registrieren der benutzerdefinierten Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="57855-145">Programmatically register the custom button</span></span>

<span data-ttu-id="57855-146">Mithilfe der nachfolgenden Anleitung können Sie diese Strategie umsetzen:</span><span class="sxs-lookup"><span data-stu-id="57855-146">The following procedure shows how to implement this strategy.</span></span>

1. <span data-ttu-id="57855-147">Erweitern Sie im Projekt **ChainStore** das Element **AddEmployeeToCorpDB**, öffnen Sie die Datei „elements.xml“, und ändern Sie den Wert des Attributs **RegistrationId** des Elements **CustomAction** in „100“.</span><span class="sxs-lookup"><span data-stu-id="57855-147">In the **ChainStore** project, expand **AddEmployeeToCorpDB**, open the elements.xml file, and then change the value of the **RegistrationId** attribute of the **CustomAction** element to "100".</span></span> <span data-ttu-id="57855-148">Dies ist die ID eines Listentyps.</span><span class="sxs-lookup"><span data-stu-id="57855-148">This is the ID of a type of list.</span></span> <span data-ttu-id="57855-149">Auch wenn auf der Website keine Instanzen von Listen dieses Typs vorhanden sind, existiert der *Listentyp* dennoch auf jeder SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="57855-149">Even if there are no instances of lists of this type on the website, the list *type* is on every SharePoint website.</span></span> <span data-ttu-id="57855-150">Das Attribut sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="57855-150">The method should now look like the following.</span></span>
    
    ```XML
      RegistrationId="100"
    ```

2. <span data-ttu-id="57855-151">Fügen Sie in der Datei „SharePointComponentDeployer.cs“ die folgende Zeile zur Methode **DeployChainStoreComponentsToHostWeb** hinzu, direkt unterhalb der Zeile, die `CreateLocalEmployeesList` aufruft (diese Methode erstellen Sie im nächsten Schritt):</span><span class="sxs-lookup"><span data-stu-id="57855-151">In the file SharePointComponentDeployer.cs, add the following line to the DeployChainStoreComponentsToHostWeb method, just below the line that calls CreateLocalEmployeesList. You will create this method in the next step.</span></span>
    
    ```C#
      ChangeCustomActionRegistration();
    ```

3. <span data-ttu-id="57855-152">Fügen Sie der Klasse `SharePointComponentDeployer` die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="57855-152">Add the following method to the  `SharePointComponentDeployer` class.</span></span> 

    ```C#
      private static void ChangeCustomActionRegistration()
    {
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())
        {
         var query = from action in clientContext.Web.UserCustomActions
                 where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                 select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();

          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         // TODO8: Get a reference to the (empty) collection of custom actions 
         // that are registered with the custom list.

         // TODO9: Add a blank custom action to the list's collection.

         // TODO10: Copy property values from the descriptively deployed
         // custom action to the new custom action

        // TODO11: Delete the original custom action.         

          clientContext.ExecuteQuery();
        }
    }
    ```

   <span data-ttu-id="57855-153">Zu diesem Code ist Folgendes anzumerken:</span><span class="sxs-lookup"><span data-stu-id="57855-153">Note the following about this code:</span></span>
    
   - <span data-ttu-id="57855-154">Da die benutzerdefinierte Aktion (d. h. die benutzerdefinierte Schaltfläche) im Menüband eines *Listentyps* registriert wurde, umfasst ihr Bereich die gesamte Website. Zudem ist die Aktion Teil der Sammlung von benutzerdefinierten Aktionen dieser Website.</span><span class="sxs-lookup"><span data-stu-id="57855-154">Because the custom action; that is, the custom button; was registered with the ribbon of a list  *type*  , it is scoped to the entire website and is in the website's collection of custom actions. So the code retrieves it from that collection.</span></span> <span data-ttu-id="57855-155">Der Code ruft sie also aus dieser Sammlung ab.</span><span class="sxs-lookup"><span data-stu-id="57855-155">So the code retrieves it from that collection.</span></span>
    
   - <span data-ttu-id="57855-156">Der Wert von `action.Name` wird aus dem Attribut **ID** des Elements **CustomAction** in der Datei „elements.xml“ in **AddEmployeeToCorpDB** abgerufen.</span><span class="sxs-lookup"><span data-stu-id="57855-156">The value of the  `action.Name` comes from the **ID** attribute of the **CustomAction** element in the element.xml file in **AddEmployeeToCorpDB**.</span></span>
    
   > [!IMPORTANT]
   > <span data-ttu-id="57855-157">**Sie müssen in Ihrem Code als Wert für `action.Name` den Wert aus der Datei „elements.xml“ angeben.**</span><span class="sxs-lookup"><span data-stu-id="57855-157">**You must change the `action.Name` value in the code to match the value in your elements.xml file.**</span></span> <span data-ttu-id="57855-158">Der Name wird einen anderen GUID-Teil haben.</span><span class="sxs-lookup"><span data-stu-id="57855-158">The GUID part of the name will be different.</span></span> <span data-ttu-id="57855-159">Dabei muss zwischen der GUID und dem Rest des Namens ein Zeichen des Typs `"."` stehen.</span><span class="sxs-lookup"><span data-stu-id="57855-159">Note that there is a `"."` character between the GUID and the rest of the name.</span></span> <span data-ttu-id="57855-160">Unten sehen Sie ein Beispiel für diese Zeile:</span><span class="sxs-lookup"><span data-stu-id="57855-160">The following is an example of the markup:</span></span> 
   > 
   > `where action.Name == "4a926a42-3577-4e02-9d06-fef78586b1bc.AddEmployeeToCorpDB"`

4. <span data-ttu-id="57855-161">Ersetzen Sie `TODO8` durch den unten aufgeführten Code.</span><span class="sxs-lookup"><span data-stu-id="57855-161">Replace  `TODO8` with the following code.</span></span> <span data-ttu-id="57855-162">Bedenken Sie dabei, dass beim Zurückziehen eines Add-Ins die von diesem Add-In erstellten Komponenten nicht entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="57855-162">Note that when you retract an add-in, components created by the add-in are not removed.</span></span> <span data-ttu-id="57855-163">Nach der Ausführung der First-Run-Logik wird in der Sammlung **UserCustomActions** der Liste eine benutzerdefinierte Aktion aufgeführt, die nicht zurückgezogen wird, wenn Sie das nächste Mal die Taste F5 drücken.</span><span class="sxs-lookup"><span data-stu-id="57855-163">Note that when you retract an add-in, components created by the add-in are not removed. After your first-run logic executes, there will be a custom action in the list's  **UserCustomActions** collection, and it will not be retracted the next time you press F5. To avoid confusion, the last line in this code  empties the collection.</span></span> <span data-ttu-id="57855-164">Um Verwirrung vorzubeugen, leert die letzte Zeile in diesem Codebeispiel (`listActions.Clear();`) die Sammlung.</span><span class="sxs-lookup"><span data-stu-id="57855-164">To avoid confusion, the last line in this code `listActions.Clear();` empties the collection.</span></span>

    ```C#
    var queryForList = from list in clientContext.Web.Lists
               where list.Title == "Local Employees"
               select list;
    IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
    clientContext.ExecuteQuery();

    List employeeList = matchingLists.First();
    var listActions = employeeList.UserCustomActions;
    clientContext.Load(listActions);
    listActions.Clear();
    ```

5. <span data-ttu-id="57855-165">Ersetzen Sie `TODO9` durch die nachfolgende Zeile. Sie fügt der Liste **Lokale Mitarbeiter** eine nicht definierte benutzerdefinierte Aktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="57855-165">Replace  `TODO9` with the following line, which adds an undefined custom action to the **Local Employees** list.</span></span>
    
    ```C#
      var listScopedEmployeeAction = listActions.Add();
    ```

6. <span data-ttu-id="57855-166">Ersetzen Sie `TODO10` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="57855-166">Replace  `TODO10` with the following code.</span></span> 

    ```C#
    listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
    listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
    listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
    listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
    listScopedEmployeeAction.Update();
    ```

   <span data-ttu-id="57855-167">Zu diesem Code ist Folgendes anzumerken:</span><span class="sxs-lookup"><span data-stu-id="57855-167">Note the following about this code:</span></span>
    
   - <span data-ttu-id="57855-168">Er weist die Eigenschaftswerte der Schaltfläche für den Webbereich (die mit beschreibendem Markup bereitgestellt wurde) den entsprechenden Eigenschaften der Schaltfläche für den Listenbereich zu, damit die beiden Schaltflächen außer im Bereich identisch sind.</span><span class="sxs-lookup"><span data-stu-id="57855-168">It assigns the property values of the web-scoped button (that was deployed with descriptive markup) to the corresponding properties of the list-scoped button, so the two buttons are identical except in scope.</span></span>
    
   - <span data-ttu-id="57855-169">Die Eigenschaft **Sequence** legt die relative Reihenfolge für die Anzeige der Schaltfläche in dem Menübereich fest, in dem sie platziert werden soll.</span><span class="sxs-lookup"><span data-stu-id="57855-169">The **Sequence** property specifies the relative order that the button will appear in its area of the ribbon.</span></span> <span data-ttu-id="57855-170">In unserem Fall wird die Schaltfläche im Abschnitt **Aktionen** der Menübandregisterkarte **Elemente** platziert.</span><span class="sxs-lookup"><span data-stu-id="57855-170">In this case, the button is on the **Actions** section of the **Items** tab of the ribbon.</span></span> <span data-ttu-id="57855-171">Im deskriptiven Markup war der Wert auf „10001“ gesetzt, also hoch genug, dass die Schaltfläche nach (d. h. rechts von) den standardmäßigen Schaltflächen angezeigt wird, die SharePoint im Bereich **Aktionen** des Menübands platziert.</span><span class="sxs-lookup"><span data-stu-id="57855-171">The  Sequence property specifies the relative order that the button will appear in its area of the ribbon. In this case, the button is on the Actions section of the Items tab of the ribbon. In the descriptive markup this value was set to 10001 which is high enough to ensure that it will appear after (that is, to the right of) any in-the-box buttons that SharePoint itself puts in the **Actions** section of the ribbon.</span></span>

7. <span data-ttu-id="57855-172">Ersetzen Sie `TODO11` durch die nachfolgend aufgeführte Zeile. Sie löscht die ursprüngliche deskriptiv definierte Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="57855-172">Replace `TODO11` with the following line, which deletes the original descriptively-defined button.</span></span> <span data-ttu-id="57855-173">Ohne diese Zeile würde die benutzerdefinierte Schaltfläche auf der Website in jeder Liste angezeigt, die die Listenvorlage „100“ verwendet.</span><span class="sxs-lookup"><span data-stu-id="57855-173">If we did not have this line, every list on the website that uses list template "100" would have the custom button on it.</span></span> <span data-ttu-id="57855-174">Da die Funktionalität der Schaltfläche eng verzahnt ist mit der Liste **Lokale Mitarbeiter**, wäre es nicht sinnvoll, die Schaltfläche in andere Listen zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="57855-174">Because the button's functionality is closely tied to the **Local Employees** list, it would make no sense to have the button on any other list.</span></span> <span data-ttu-id="57855-175">Zudem würde die Schaltfläche ohne diese Zeile *doppelt* in der Liste **Lokale Mitarbeiter** angezeigt, da die Liste die Vorlage „100“ verwendet.</span><span class="sxs-lookup"><span data-stu-id="57855-175">Also, without this line, the button would appear *twice*  on the **Local Employees** list, because that list uses template "100".</span></span>
    
    ```C#
      webScopedEmployeeAction.DeleteObject();
    ```
    
8. <span data-ttu-id="57855-176">Insgesamt sollte die Methode jetzt wie unten dargestellt aussehen (mit einer GUID statt des Platzhalters):</span><span class="sxs-lookup"><span data-stu-id="57855-176">The entire method should now look like the following (except there should be a GUID in place of the placeholder).</span></span>
    
    ```C#
      private static void ChangeCustomActionRegistration()
    {
        using (var clientContext = SPContext.CreateUserClientContextForSPHost())
        {
         var query = from action in clientContext.Web.UserCustomActions
                 where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                 select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();

          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         var queryForList = from list in clientContext.Web.Lists
                    where list.Title == "Local Employees"
                    select list;
         IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
         clientContext.ExecuteQuery();

        List employeeList = matchingLists.First();
        var listActions = employeeList.UserCustomActions;
        clientContext.Load(listActions);
        listActions.Clear();

        var listScopedEmployeeAction = listActions.Add();

        listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
        listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
        listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
        listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
        listScopedEmployeeAction.Update();

        webScopedEmployeeAction.DeleteObject();         

        clientContext.ExecuteQuery();
        }
    }
    ```


## <a name="request-full-control-of-the-host-web"></a><span data-ttu-id="57855-177">Anfordern von Vollzugriff vom Hostweb</span><span class="sxs-lookup"><span data-stu-id="57855-177">Request full control of the host web</span></span>

<span data-ttu-id="57855-178">Da das Add-In jetzt auf den Bereich „Web“ bezogene benutzerdefinierte Aktionen hinzufügt und löscht, müssen Sie die vom Add-In angeforderten Berechtigungen von „Verwalten“ auf „Vollzugriff“ erweitern:</span><span class="sxs-lookup"><span data-stu-id="57855-178">Since the add-in is now adding adding and deleting web-scoped custom actions, we need to escalate the permissions that the add-in requests from Manage to Full Control. Follow these steps.</span></span>

1. <span data-ttu-id="57855-179">Öffnen Sie im **Projektmappen-Explorer** im Projekt **ChainStore** die Datei „AppManifest.xml“.</span><span class="sxs-lookup"><span data-stu-id="57855-179">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>

2. <span data-ttu-id="57855-180">Öffnen Sie die Registerkarte **Berechtigungen**. Behalten Sie für **Bereich** den Wert **Web** bei, aber wählen Sie im Feld **Berechtigung** aus der Dropdownliste die Option **Vollzugriff** aus.</span><span class="sxs-lookup"><span data-stu-id="57855-180">Open the **Permissions** tab. Leave the **Scope** value at **Web**, but in the **Permission** field, select **Full Control** from the drop down.</span></span>

3. <span data-ttu-id="57855-181">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="57855-181">Save the file.</span></span>

## <a name="run-the-add-in-and-test-the-button-deployment"></a><span data-ttu-id="57855-182">Ausführen des Add-Ins und Testen der Schaltflächenbereitstellung</span><span class="sxs-lookup"><span data-stu-id="57855-182">Run the add-in and test the button deployment</span></span>

1. <span data-ttu-id="57855-183">Öffnen Sie die Seite **Websiteinhalte** der Website des Hongkong-Stores, und entfernen Sie die Liste **Lokale Mitarbeiter**.</span><span class="sxs-lookup"><span data-stu-id="57855-183">Open the  Site Contents page of the Hong Kong store's website and remove the  Local Employees list!</span></span> 
    
   > [!NOTE]
   > <span data-ttu-id="57855-184">Wenn Sie ein Add-In in Visual Studio zurückziehen, werden die von dem betreffenden Add-In erstellten Listen nicht entfernt. Sie müssen die Liste also jedes Mal manuell löschen, wenn Sie den Code testen, der sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="57855-184">Note  Retracting an add-in in Visual Studio, does not remove lists that are created by the add-in, so you need to manually delete it any time you are testing code that creates it.</span></span>

2. <span data-ttu-id="57855-185">Drücken Sie die Taste F5, um das Add-In bereitzustellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="57855-185">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="57855-186">Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express.</span><span class="sxs-lookup"><span data-stu-id="57855-186">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="57855-187">Zudem installiert Visual Studio das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite und führt es sofort aus.</span><span class="sxs-lookup"><span data-stu-id="57855-187">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="57855-188">Bevor die Startseite des Add-Ins geöffnet wird, werden Sie aufgefordert, dem Add-In Berechtigungen zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="57855-188">You are prompted to grant permissions to the add-in before its start page opens.</span></span>

3. <span data-ttu-id="57855-189">Die Startseite des Add-Ins wird geöffnet. Klicken Sie oben im Chromsteuerelement auf **Zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="57855-189">When the add-in's start page opens, select the **Back to Site** link on the chrome control at the top.</span></span>

4. <span data-ttu-id="57855-190">Wechseln Sie auf die Seite **Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="57855-190">Go to the **Site Contents** page.</span></span> <span data-ttu-id="57855-191">Die Liste **Lokale Mitarbeiter** wird angezeigt, da sie von der First-Run-Logik hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="57855-191">Navigate to the  Site Contents page. The **Local Employees** list is present because your first-run logic added it.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="57855-192">Falls die Liste nicht angezeigt wird oder Sie Grund zu der Annahme haben, dass die First-Run-Logik nicht ausgeführt wird, kann das daran liegen, wird möglicherweise die Tabelle **Mandanten** beim Drücken von F5 nicht in den leeren Zustand zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="57855-192">If the list is not there or you have other indications that the first-run code is not executing, it may be that the **Tenants** table is not being reverted to an empty state when you select F5.</span></span> <span data-ttu-id="57855-193">Die häufigste Ursache hierfür: Das Projekt **ChainCorporateDB** ist in Visual Studio nicht mehr als Startprojekt gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="57855-193">The most common cause of this is that the **ChainCorporateDB** project is no longer set as a startup project in Visual Studio.</span></span> <span data-ttu-id="57855-194">Eine Lösung für dieses Problem finden Sie in dem [Hinweis oben in diesem Artikel](#re-add-the-custom-button-to-the-project).</span><span class="sxs-lookup"><span data-stu-id="57855-194">See the [note near the top of this article](#re-add-the-custom-button-to-the-project) for how to fix this.</span></span> <span data-ttu-id="57855-195">Vergewissern Sie sich außerdem, dass die Datenbank so konfiguriert ist, dass sie neu erstellt wird (siehe [Konfigurieren von Visual Studio zum Neuerstellen der Unternehmensdatenbank in jeder Debugsitzung](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild)).</span><span class="sxs-lookup"><span data-stu-id="57855-195">Also be sure that you've configured the database to be rebuilt as described in [Configure Visual Studio to rebuild the corporate database with each debugging session](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild).</span></span>

5. <span data-ttu-id="57855-196">Öffnen Sie die Liste, und fügen Sie ein Element hinzu.</span><span class="sxs-lookup"><span data-stu-id="57855-196">Open the list and add an item.</span></span>

6. <span data-ttu-id="57855-197">Wählen Sie das Element in der Listenansicht aus, und wechseln Sie auf dem Menüband auf die Registerkarte **Element**.</span><span class="sxs-lookup"><span data-stu-id="57855-197">In the list view, select the item and open the  **Item** tab on the ribbon. The Add to Corporate DB button is on the ribbon.</span></span> 

7. <span data-ttu-id="57855-198">Klicken Sie auf der Registerkarte **Element** auf die Schaltfläche **Zur Unternehmensdatenbank hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="57855-198">On the **Item** tab, select the **Add to Corporate DB** button.</span></span> <span data-ttu-id="57855-199">Der Mitarbeiter wird der Unternehmensdatenbank hinzugefügt, und das Feld **Zur Unternehmensdatenbank hinzugefügt** wird in **Ja** geändert.</span><span class="sxs-lookup"><span data-stu-id="57855-199">Click the button and the employee is added to the corporate database and the  **Added to Corporate DB** field is changed to **Yes**.</span></span>

8. <span data-ttu-id="57855-200">Wechseln Sie wieder auf die Seite **Websiteinhalte**, und klicken Sie dort auf **Add-In hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="57855-200">Navigate back to the  **Site Contents** page and select **add an add-in**.</span></span>

9. <span data-ttu-id="57855-201">Fügen Sie eine neue **benutzerdefinierte Liste** hinzu.</span><span class="sxs-lookup"><span data-stu-id="57855-201">Add a new **Custom List**.</span></span> <span data-ttu-id="57855-202">Als Typ wird standardmäßig „Generic“ festgelegt (d. h. der Listentyp „100“).</span><span class="sxs-lookup"><span data-stu-id="57855-202">By default it will be "Generic" type (Generic is list type 100).</span></span> <span data-ttu-id="57855-203">Öffnen Sie nach der Erstellung der Liste auf dem Menüband die Registerkarte **Element**.</span><span class="sxs-lookup"><span data-stu-id="57855-203">After the list is created, open the **Item** tab on the ribbon.</span></span> <span data-ttu-id="57855-204">Wie Sie sehen, wird die Schaltfläche **Zur Unternehmensdatenbank hinzufügen** zu diesem Zeitpunkt *nicht* auf dem Menüband angezeigt.</span><span class="sxs-lookup"><span data-stu-id="57855-204">Notice that the **Add to Corporate DB** button is *not*  on the ribbon.</span></span> <span data-ttu-id="57855-205">Das liegt daran, dass Ihr Code die Schaltfläche mit dem Bezugsbereich „Web“ gelöscht hat.</span><span class="sxs-lookup"><span data-stu-id="57855-205">This is because your code deleted the web-scoped button.</span></span>

10. <span data-ttu-id="57855-206">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57855-206">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="57855-207">Wann immer Sie F5 drücken, zieht Visual Studio die bisherige Version des Add-Ins zurück und installiert die jeweils neueste Version.</span><span class="sxs-lookup"><span data-stu-id="57855-207">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

11. <span data-ttu-id="57855-208">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung auch in anderen Artikeln arbeiten werden, empfiehlt es sich, das Add-In ein letztes Mal zurückzuziehen, sobald Sie eine Weile nicht mehr an ihm arbeiten werden.</span><span class="sxs-lookup"><span data-stu-id="57855-208">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="57855-209">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="57855-209">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57855-210">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="57855-210">Next steps</span></span>
<span data-ttu-id="57855-211"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="57855-211"></span></span>

<span data-ttu-id="57855-212">Listenereignisse und Listenelementereignisse können in SharePoint ebenfalls von benutzerdefinierten Handlern verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="57855-212">Events on lists and list items can also have custom handlers in SharePoint.</span></span> <span data-ttu-id="57855-213">Wie Sie einen solchen Handler erstellen und in der First-Run-Logik bereitstellen, erfahren Sie im Artikel [Handle list item events in the provider-hosted add-in](handle-list-item-events-in-the-provider-hosted-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="57855-213">Events on lists and list items can also have custom handlers in SharePoint. You learn how to create one and deploy it in your first-run logic in the next article: [Handle list item events in the provider-hosted add-in](handle-list-item-events-in-the-provider-hosted-add-in.md)</span></span>
 

 

