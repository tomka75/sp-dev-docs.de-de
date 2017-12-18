---
title: Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins
description: "Erstellen Sie einen Add-In-Katalog, packen Sie das Add-In, laden Sie es in den Katalog hoch, installieren Sie es und löschen Sie es."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: c11fb37232d433d41866d42d18322431902257ae
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="deploy-and-install-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="18e22-103">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="18e22-103">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="18e22-104">Dies ist der zweite in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="18e22-104">This is the second in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with the topic  [SharePoint Add-ins](sharepoint-add-ins.md) and the preceding topics in the series:</span></span>

-  [<span data-ttu-id="18e22-105">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="18e22-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
> [!NOTE]
> <span data-ttu-id="18e22-106">Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen.</span><span class="sxs-lookup"><span data-stu-id="18e22-106">Note  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_SP-hosted_Add-Ins_Tutorials and open the BeforeClientRenderedControl.sln file.</span></span> <span data-ttu-id="18e22-107">Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeColumns.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="18e22-107">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>

<span data-ttu-id="18e22-108">Sie werden feststellen, dass die Entwicklung von SharePoint gehosteter SharePoint-Add-Ins viel einfacher ist, wenn Sie wissen, wie Benutzer bereitgestellt und Ihre Add-Ins installiert werden. Deshalb unterbrechen wir in diesem Artikel kurz die Codierung, um einen Add-In-Katalog zu erstellen und zu verwenden, und installieren dann das Add-In, an dem Sie gearbeitet haben.</span><span class="sxs-lookup"><span data-stu-id="18e22-108">You'll find it a lot easier to develop SharePoint-hosted SharePoint Add-ins if you are familiar with how users deploy and install your add-ins. So, in this article, we'll take a brief break from coding to create and use an add-in catalog, and then install the add-in you've been working on.</span></span>

## <a name="create-an-add-in-catalog"></a><span data-ttu-id="18e22-109">Erstellen eines Add-In-Katalogs</span><span class="sxs-lookup"><span data-stu-id="18e22-109">Create an add-in catalog</span></span>

1. <span data-ttu-id="18e22-110">Melden Sie sich bei Ihrem Office 365-Abonnement als Administrator an.</span><span class="sxs-lookup"><span data-stu-id="18e22-110">Sign in to your Office 365 subscription as an administrator.</span></span> <span data-ttu-id="18e22-111">Wählen Sie das Symbol für das  Add-In-Startprogramm, und wählen Sie dann das **Admin**-Add-In.</span><span class="sxs-lookup"><span data-stu-id="18e22-111">Select the add-in launcher icon, and then select the **Admin** add-in.</span></span>
    
   <span data-ttu-id="18e22-112">*Abbildung 1. Add-In-Startprogramm für Office 365*</span><span class="sxs-lookup"><span data-stu-id="18e22-112">*Figure 1. Office 365 add-in launcher*</span></span>

   ![App-Startprogramm für Office 365](../images/ec60797c-d329-4922-a811-70c64598f4d5.PNG)
 
2. <span data-ttu-id="18e22-114">Erweitern Sie im **Admin Center** den Knoten **Admin** im Aufgabenbereich, und wählen Sie dann **SharePoint** aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-114">In the  **Admin Center**, expand the  **Admin** node in the task pane and then choose **SharePoint**.</span></span>
     
3. <span data-ttu-id="18e22-115">Wählen Sie im **SharePoint Admin Center** die Option **Add-Ins** im Aufgabenbereich aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-115">In the  **SharePoint Admin Center**, choose  **add-ins** in the task pane.</span></span>
     
4. <span data-ttu-id="18e22-116">Wählen Sie auf der Seite  **Add-Ins** die Option **Add-In-Katalog** aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-116">On the **add-ins** page, select **Add-in Catalog**.</span></span> <span data-ttu-id="18e22-117">(Wenn bereits eine Add-In-Katalog-Websitesammlung im Abonnement vorhanden ist, wird diese geöffnet, und Sie sind fertig.</span><span class="sxs-lookup"><span data-stu-id="18e22-117">(If there is already an add-in catalog site collection in the subscription, it opens and you are finished.</span></span> <span data-ttu-id="18e22-118">Sie können nur jeweils einen Add-In-Katalog pro Abonnement erstellen.)</span><span class="sxs-lookup"><span data-stu-id="18e22-118">You cannot create more than one add-in catalog in a subscription.)</span></span>    
 
5. <span data-ttu-id="18e22-119">Wählen Sie auf der Seite  **Add-In-Katalogwebsite** **OK** aus, um die Standardoption zu akzeptieren und eine neue Add-In-Katalogwebsite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="18e22-119">On the  **Add-in Catalog Site** page, choose **OK** to accept the default option and create a new add-in catalog site.</span></span>    
 
6. <span data-ttu-id="18e22-120">Geben Sie im Dialog  **Add-In-Katalog-Websitesammlung erstellen** den Titel und die Webadresse Ihrer Add-In-Katalogwebsite an.</span><span class="sxs-lookup"><span data-stu-id="18e22-120">In the **Create Add-in Catalog Site Collection** dialog, specify the title and website address of your add-in catalog site.</span></span> <span data-ttu-id="18e22-121">Wir empfehlen, den Begriff „Katalog“ im Titel und der URL zu verwenden, damit er einprägsamer ist und im **SharePoint Admin Center** besser unterschieden werden kann.</span><span class="sxs-lookup"><span data-stu-id="18e22-121">On the  Create Add-in Catalog Site Collection dialog, specify the title and web site address of your add-in catalog site. We recommend that you include "catalog" in the title and URL to make it memorable and distinguishable in the **SharePoint Admin Center**.</span></span>   
 
7. <span data-ttu-id="18e22-122">Geben Sie eine **Zeitzone** an, und legen Sie sich selbst als **Administrator** fest.</span><span class="sxs-lookup"><span data-stu-id="18e22-122">Specify a  **Time Zone** and set yourself as the **Administrator**.</span></span>
    
8. <span data-ttu-id="18e22-123">Legen Sie das **Speicherkontingent** auf den niedrigsten möglichen Wert fest (derzeit 110, das kann sich jedoch ändern), da die Add-In-Pakete, die Sie an diese Websitesammlung hochladen, sehr klein sind.</span><span class="sxs-lookup"><span data-stu-id="18e22-123">Set the  **Storage Quota** to the lowest possible value (currently 110, but that can change), because the add-in packages you upload to this site collection are very small.</span></span>
    
9. <span data-ttu-id="18e22-124">Legen Sie das **Serverressourcenkontingent** auf 0 (null) fest, und wählen Sie dann **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-124">Set the **Server Resource Quota** to 0 (zero), and then select **OK**.</span></span> <span data-ttu-id="18e22-125">(Das Serverressourcenkontingent hat Auswirkungen auf die Einschränkung leistungsschwacher Sandkastenlösungen; Sie müssen jedoch keine Sandkastenlösungen auf der Add-In-Katalogwebsite installieren.)</span><span class="sxs-lookup"><span data-stu-id="18e22-125">Set the  Server Resource Quota to 0 (zero). (The server resource quota is related to throttling poorly performing sandboxed solutions, but you won't be installing any sandboxed solutions on your add-in catalog site.)</span></span> 
 
<span data-ttu-id="18e22-126">Während die Websitesammlung erstellt wird, gelangen Sie zurück zum **SharePoint Admin Center**.</span><span class="sxs-lookup"><span data-stu-id="18e22-126">As the site collection is being created, SharePoint takes you back to the  **SharePoint Admin Center**. After a few minutes, you'll see that the collection has been created.</span></span> <span data-ttu-id="18e22-127">Nach ein paar Minuten sehen Sie, dass die Sammlung erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="18e22-127">As the site collection is being created, SharePoint takes you back to the  SharePoint Admin Center. After a few minutes, you'll see that the collection has been created.</span></span>

## <a name="package-the-add-in-and-upload-it-to-the-catalog"></a><span data-ttu-id="18e22-128">Packen des Add-Ins und Hochladen in den Katalog</span><span class="sxs-lookup"><span data-stu-id="18e22-128">Package the add-in and upload it to the catalog</span></span>

1. <span data-ttu-id="18e22-129">Öffnen Sie die Visual Studio-Projektmappe, klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektknoten, und wählen Sie dann **Veröffentlichen** aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-129">Open the Visual Studio solution, and then right-click the project node in  **Solution Explorer**. Choose  **Publish**.</span></span>
     
2. <span data-ttu-id="18e22-130">Wählen Sie im Bereich **Veröffentlichen** die Option **Add-In verpacken** aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-130">In the **Publish** pane, select **Package the add-in**.</span></span> <span data-ttu-id="18e22-131">Das Add-In wird gepackt und als `*.app`-Datei im Ordner „\bin\debug\web.publish\1.0.0.0“ der Projektmappe gespeichert.</span><span class="sxs-lookup"><span data-stu-id="18e22-131">In the  Publish pane, choose Package the add-in. The add-in is packaged and saved as an *.app file in the solution's \bin\debug\web.publish\1.0.0.0 folder.</span></span>  
 
3. <span data-ttu-id="18e22-132">Öffnen Sie die Add-In-Katalogwebsite in einem Browser, und wählen Sie dann **SharePoint-Add-Ins** in der Navigationsleiste aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-132">Open your add-in catalog site in a browser and choose  **SharePoint Add-ins** in the navigation bar.</span></span>

4. <span data-ttu-id="18e22-133">Der **SharePoint-Add-Ins**-Katalog ist eine standardmäßige SharePoint-Objektbibliothek.</span><span class="sxs-lookup"><span data-stu-id="18e22-133">The **SharePoint Add-ins** catalog is a standard SharePoint asset library.</span></span> <span data-ttu-id="18e22-134">Laden Sie das Add-In-Paket mithilfe einer der Methoden zum Hochladen von Dateien in SharePoint-Bibliotheken in den Katalog hoch.</span><span class="sxs-lookup"><span data-stu-id="18e22-134">The spapppluralcap catalog is a standard SharePoint asset library. Upload the add-in package to it using any of the methods of uploading files to SharePoint libraries.</span></span>

## <a name="install-the-add-in-as-end-users-do"></a><span data-ttu-id="18e22-135">Installieren des Add-Ins als Endbenutzer</span><span class="sxs-lookup"><span data-stu-id="18e22-135">Install the add-in as end users do</span></span>

1. <span data-ttu-id="18e22-136">Navigieren Sie zu einer beliebigen Website im SharePoint Online-Abonnement, und öffnen Sie die Seite **Websiteinhalt**.</span><span class="sxs-lookup"><span data-stu-id="18e22-136">Navigate to any website in the SharePoint Online subscription and open the  **Site Contents** page.</span></span>

2. <span data-ttu-id="18e22-137">Wählen Sie **Add-In hinzufügen** aus, um die Seite **Ihre Add-Ins** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="18e22-137">Choose  **add an add-in** to open the **Your Add-ins** page.</span></span>

3. <span data-ttu-id="18e22-138">Suchen Sie das Add-In **Orientierung für Mitarbeiter** im Abschnitt **Add-Ins, die Sie hinzufügen können**, und wählen Sie die zugehörige Kachel aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-138">Find the  **Employee Orientation** add-in in the **Add-ins you can add** section and click its tile.</span></span>

4. <span data-ttu-id="18e22-139">Wählen Sie **Vertrauen** im Zustimmungsdialogfeld aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-139">Select **Trust It** in the consent dialog.</span></span> <span data-ttu-id="18e22-140">Die Seite **Websiteinhalte** wird automatisch geöffnet, und das Add-In wird mit einer Anmerkung, dass es gerade installiert wird, angezeigt.</span><span class="sxs-lookup"><span data-stu-id="18e22-140">Choose  Trust It on the consent dialog. The **Site Contents** page automatically opens and the add-in appears with a notation that it is installing. After it installs, users can choose the tile to run the add-in.</span></span> <span data-ttu-id="18e22-141">Nach der Installation können Benutzer die Kachel auswählen, um das Add-In auszuführen.</span><span class="sxs-lookup"><span data-stu-id="18e22-141">After it installs, users can select the tile to run the add-in.</span></span>

## <a name="remove-the-add-in"></a><span data-ttu-id="18e22-142">Entfernen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="18e22-142">Remove the add-in</span></span>

<span data-ttu-id="18e22-143">Um das gleiche SharePoint-Add-In in Visual Studio noch weiter zu verbessern (siehe [nächste Schritte](#Nextsteps)), entfernen Sie das Add-In mit den folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="18e22-143">In order to continue enhancing the same SharePoint Add-in in Visual Studio (see  [Next steps](#Nextsteps)), remove the add-in with these steps:</span></span>

1. <span data-ttu-id="18e22-144">Bewegen Sie den Cursor auf der Seite **Websiteinhalte** über das Add-In, sodass die Popupschaltfläche **...** angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="18e22-144">In the  **Site Contents** page, move the cursor over the add-in so that the callout button **...** appears.</span></span>

2. <span data-ttu-id="18e22-145">Wählen Sie die Popupschaltfläche aus, und wählen Sie dann **ENTFERNEN** im Popup aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-145">Choose the callout button and then choose  **REMOVE** on the callout.</span></span>

3. <span data-ttu-id="18e22-146">Navigieren Sie zurück zur Add-In-Katalogwebsite, und wählen Sie **SharePoint-Add-Ins** in der Navigationsleiste aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-146">Navigate back to your add-in catalog site and choose  **SharePoint Add-ins** in the navigation bar.</span></span>

4. <span data-ttu-id="18e22-147">Markieren Sie das Add-In, wählen Sie **Verwalten** auf der Taskleiste direkt oberhalb der Liste aus, und wählen Sie dann **Löschen** im Verwaltungsmenü aus.</span><span class="sxs-lookup"><span data-stu-id="18e22-147">Highlight the add-in and choose  **manage** on the task bar just above the list, and then choose **Delete** on the manage menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18e22-148">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="18e22-148">Next steps</span></span>
<a name="Nextsteps"></a>

<span data-ttu-id="18e22-149">Es wird dringend empfohlen, dass Sie mit dieser Reihe zu von SharePoint gehosteten Add-Ins fortfahren, bevor Sie mit den fortgeschrittenen Themen beginnen.</span><span class="sxs-lookup"><span data-stu-id="18e22-149">We strongly recommend that you continue with this series about SharePoint-hosted add-ins before you go on to the more advanced topics. Next we get back to coding in  Add custom columns to a SharePoint-hostedSharePoint Add-in.</span></span> <span data-ttu-id="18e22-150">In [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md) befassen wir uns wieder mit der Programmierung.</span><span class="sxs-lookup"><span data-stu-id="18e22-150">We strongly recommend that you continue with this series about SharePoint-hosted add-ins before you go on to the more advanced topics. Next we get back to coding in [Add custom columns to a SharePoint-hosted SharePoint Add-in](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

