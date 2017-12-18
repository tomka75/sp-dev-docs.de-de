---
title: Erstellen einer minimale Gestaltungsvorlage in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 634aa471-07e1-41d6-aa80-27f7ef7e9dc8
ms.openlocfilehash: c7554383f757c5f70b87ab7eabd8651272da6275
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-minimal-master-page-in-sharepoint"></a><span data-ttu-id="f0017-102">Erstellen einer minimale Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0017-102">How to: Create a minimal master page in SharePoint</span></span>

<span data-ttu-id="f0017-p101">Eine minimale Gestaltungsvorlage enthält nur die Seitenelemente, die zum Rendern der Seite im Browser ordnungsgemäß SharePoint erforderlich. Mit Entwurfs-Manager können Sie schnell erstellen eine minimale Gestaltungsvorlage ohne zuvor zum Entwerfen und Konvertieren einer HTML-Datei.</span><span class="sxs-lookup"><span data-stu-id="f0017-p101">A minimal master page contains only those page elements that are required by SharePoint to render the page correctly in the browser. With Design Manager, you can quickly create a minimal master page without first having to design and convert an HTML file.</span></span>

## <a name="introduction-to-the-minimal-master-page"></a><span data-ttu-id="f0017-105">Einführung in die minimale Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="f0017-105">Introduction to the minimal master page</span></span>
<span data-ttu-id="f0017-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="f0017-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="f0017-p102">Mit Entwurfs-Manager können Sie eine typische HTML-Datei in eine Gestaltungsvorlage SharePoint konvertieren. Aber, wenn Sie nicht über eine vordefinierte Modell verfügen, Sie können weiterhin schnell starten von Grund auf neu, indem Sie eine minimale Gestaltungsvorlage erstellen. Die minimale Gestaltungsvorlage enthält nur die Seitenelemente, die von SharePoint zum Rendern der Seite im Browser erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f0017-p102">With Design Manager, you can convert a typical HTML file into a SharePoint master page. But, if you don't have a prebuilt mock-up, you can still quickly start from scratch by creating a minimal master page. The minimal master page contains only those page elements required by SharePoint to render the page in the browser.</span></span>
  
    
    
<span data-ttu-id="f0017-p103">Wenn Sie eine minimale Gestaltungsvorlage erstellen, erstellt Entwurfs-Manager die Master-Datei und eine verknüpfte HTML-Datei, damit Sie weiterhin mit der HTML-Datei arbeiten können, falls gewünscht. Arbeiten mit einer minimale Gestaltungsvorlage ist genau die gleiche wie das Arbeiten mit einer Gestaltungsvorlage, die Sie von einer HTML-Datei konvertieren. Die HTML-Datei und Gestaltungsvorlage sind verknüpft, sodass diese Änderungen an der zugeordneten Masterseite, wenn Sie bearbeiten und speichern Sie die HTML-Datei synchronisiert werden. Und die HTML-Datei enthält spezielle Arten von Markup, die Synchronisierung mit der möglichen Master-Datei vornehmen. Weitere Informationen über diese Zuordnung und diese Arten von Markup finden Sie unter  [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f0017-p103">When you create a minimal master page, Design Manager creates both the .master file and an associated HTML file, so that you can still work with only the HTML file if you prefer. Working with a minimal master page is exactly the same as working with a master page that you convert from an HTML file. The HTML file and master page are associated, so that whenever you edit and save the HTML file, those changes are synced to the associated master page. And the HTML file contains special types of markup that make syncing with the .master file possible. For more information about this association and these types of markup, see  [How to: Convert an HTML file into a master page in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="f0017-115">Beginnend mit eine minimale Gestaltungsvorlage ist hilfreich, wenn:</span><span class="sxs-lookup"><span data-stu-id="f0017-115">Starting with a minimal master page is useful when:</span></span>
  
    
    

- <span data-ttu-id="f0017-116">Sie möchten schnell neu starten, und klicken Sie dann erstellen, den Entwurf der HTML-Datei, die die minimale Gestaltungsvorlage anstelle von beginnend mit einem Modell HTML-Datei zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="f0017-116">You want to start quickly from scratch, and then build out your design in the HTML file that's associated with the minimal master page, instead of starting with a mock-up HTML file.</span></span>
    
  
- <span data-ttu-id="f0017-p104">Sie schnell testen möchten oder Prototyp Designelement, die eine funktionsfähige SharePoint-Gestaltungsvorlage erforderlich sind. Erstellen eine minimale Gestaltungsvorlage erfordern beispielsweise nicht Vorbereiten einer HTML-Datei für die Konvertierung oder Auflösen von Fehlern Preview, die aus Markup, das der HTML-Datei nicht gültig ist. Dies bedeutet, dass Sie sofort mit der serverseitigen Vorschau oder Codeausschnittkatalog arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="f0017-p104">You want to rapidly test or prototype a design element that requires a working SharePoint master page. For example, creating a minimal master page does not require preparing an HTML file for conversion or resolving any preview errors that result from markup that is not valid in the HTML file. This means you can immediately work with the server-side preview or the Snippet Gallery.</span></span>
    
  
- <span data-ttu-id="f0017-p105">Die Master-Datei direkt entwickelt werden soll. Wenn Sie ein ASP.NET-Entwickler oder SharePoint-Entwickler sind, können Sie eine minimale Gestaltungsvorlage erstellen, entfernen Sie die Zuordnung zwischen der HTML-Datei und die Master-Datei durch Deaktivieren des Kontrollkästchens **Verknüpfte Datei** in den Eigenschaften der HTML-Datei und dann arbeiten direkt mit der Master-Datei.</span><span class="sxs-lookup"><span data-stu-id="f0017-p105">You want to work directly with the .master file. If you're an ASP.NET developer or a SharePoint developer, you can create a minimal master page, remove the association between the HTML file and the .master file by clearing the **Associated File** check box in the properties of the HTML file, and then work directly with the .master file.</span></span>
    
  

## <a name="create-a-minimal-master-page"></a><span data-ttu-id="f0017-122">Erstellen einer minimalen Masterseite</span><span class="sxs-lookup"><span data-stu-id="f0017-122">Create a minimal master page</span></span>
<span data-ttu-id="f0017-123"><a name="CreateMinimalMaster"> </a></span><span class="sxs-lookup"><span data-stu-id="f0017-123"><a name="CreateMinimalMaster"> </a></span></span>


  
    
    

### <a name="to-create-a-minimal-master-page"></a><span data-ttu-id="f0017-124">Erstellen Sie eine minimale Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="f0017-124">To create a minimal master page</span></span>


1. <span data-ttu-id="f0017-125">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="f0017-125">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="f0017-126">Wählen Sie in der rechten oberen Ecke der Seite **Einstellungen** und dann **Entwurfs-Manager**.</span><span class="sxs-lookup"><span data-stu-id="f0017-126">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="f0017-127">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="f0017-127">In Design Manager, in the left navigation pane, choose **Edit Master Pages**.</span></span>
    
  
4. <span data-ttu-id="f0017-128">Wählen Sie **erstellen eine minimale Gestaltungsvorlage** aus.</span><span class="sxs-lookup"><span data-stu-id="f0017-128">Choose **Create a minimal master page**.</span></span>
    
  
5. <span data-ttu-id="f0017-129">Klicken Sie im Dialogfeld **Erstellen einer Gestaltungsvorlage** Geben Sie einen Namen für die Gestaltungsvorlage, und wählen Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0017-129">In the **Create a Master Page** dialog box, enter a name for the master page, and then choose **OK**.</span></span>
    
    <span data-ttu-id="f0017-130">Zu diesem Zeitpunkt erstellt SharePoint eine Master-Datei und eine zugeordnete HTML-Datei mit dem gleichen Namen in der Master Page Gallery.</span><span class="sxs-lookup"><span data-stu-id="f0017-130">At this point, SharePoint creates both a .master file and an associated HTML file with the same name in the Master Page Gallery.</span></span>
    
    <span data-ttu-id="f0017-131">Im Entwurfs-Manager wird Ihre HTML-Datei nun mit der **Konvertierung erfolgreich** angezeigt, in der Spalte Status angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f0017-131">In Design Manager, your HTML file now appears with **Conversion successful** displayed in the Status column.</span></span>
    
  
6. <span data-ttu-id="f0017-132">Führen Sie den Link in der Spalte Status eine Vorschau die Datei.</span><span class="sxs-lookup"><span data-stu-id="f0017-132">Follow the link in the Status column to preview the file.</span></span>
    
    <span data-ttu-id="f0017-133">Die Preview-Seite ist eine serverseitige Livevorschau der Masterseite.</span><span class="sxs-lookup"><span data-stu-id="f0017-133">The preview page is a live server-side preview of your master page.</span></span>
    
    <span data-ttu-id="f0017-134">Weitere Informationen zur Vorschau der Gestaltungsvorlage mit unterschiedlichen Seiten finden Sie unter  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f0017-134">For more information about previewing the master page with different pages, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
    
    <span data-ttu-id="f0017-p106">Die Vorschauseite enthält außerdem einen Link **Ausschnitten** in der oberen rechten Ecke. Dieser Link öffnet im Codeausschnittkatalog, wo Sie beginnen können statisch oder Modell Steuerelemente in Ihrem Entwurf mit dynamischen SharePoint-Steuerelemente ersetzen. Weitere Informationen finden Sie unter [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="f0017-p106">The preview page also contains a **Snippets** link in the upper-right corner. This link opens the Snippet Gallery, where you can begin replacing static or mock-up controls in your design with dynamic SharePoint controls. For more information, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
    <span data-ttu-id="f0017-138">Nachdem eine Vorschau der Gestaltungsvorlage angezeigt wurde, wird ein ** \<div\> **-Tag Ihrer HTML-Datei hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f0017-138">After your master page previews successfully, you will see a **\<div\>** tag that gets added to your HTML file.</span></span> <span data-ttu-id="f0017-139">Sie müssen möglicherweise bis zum Ende der Seite scrollen, um das **\<div\>**-Tag zu sehen.</span><span class="sxs-lookup"><span data-stu-id="f0017-139">You may have to scroll to the bottom of the page to see the **\<div\>** tag.</span></span>
    
    <span data-ttu-id="f0017-140">Dieses **\<div\>**-Tag ist im Hauptinhaltsblock vorhanden.</span><span class="sxs-lookup"><span data-stu-id="f0017-140">This **\<div\>** is the main content block.</span></span> <span data-ttu-id="f0017-141">Es befindet sich in einem Inhaltsplatzhalter **ContentPlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="f0017-141">It resides inside a content placeholder named **ContentPlaceHolderMain**.</span></span> <span data-ttu-id="f0017-142">Wenn ein Besucher zur Laufzeit Ihre Website durchsucht und eine Seite anfordert, wird dieser Platzhalter mit Inhalt aus einem Seitenlayout gefüllt, der die Inhalte in einem passenden Inhaltsbereich enthält.</span><span class="sxs-lookup"><span data-stu-id="f0017-142">At run time, when a visitor browses your site and requests a page, this content placeholder gets filled with content from a page layout that contains content in a matching content region.</span></span> <span data-ttu-id="f0017-143">Sie sollten das ** \<div\> **-Tag dort positionieren, wo Ihre Seitenlayouts in der Gestaltungsvorlage angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f0017-143">You should position this **\<div\>** where you want your page layouts to appear on the master page.</span></span>
    
  
7. <span data-ttu-id="f0017-p109">Sie können die HTML-Datei bearbeiten, die sich direkt auf dem Server mit einem HTML-Editor zu öffnen und Bearbeiten von HTML-Datei in ein zugeordnetes Laufwerk befindet. Jedes Mal, wenn Sie die HTML-Datei speichern, werden alle Änderungen mit der zugehörigen Master-Datei synchronisiert. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="f0017-p109">You can edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in a mapped drive. Each time you save the HTML file, any changes are synced to the associated .master file. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
8. <span data-ttu-id="f0017-p110">Nur bei der Master-Datei und nicht die HTML-Datei verwendet wird, müssen Sie die Zuordnung zwischen den beiden Dateien aufteilen. Wählen Sie im Entwurfs-Manager auf der Seite Gestaltungsvorlagen bearbeiten die HTML-Datei, öffnen Sie das Menü **Eigenschaften**, und wählen Sie dann auf **Eigenschaften bearbeiten**. Klicken Sie auf die Registerkarte **Bearbeiten** deaktivieren Sie das Kontrollkästchen **Datei verknüpft ist**, und wählen Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="f0017-p110">To work only with the .master file and not the HTML file, you must break the association between the two files. In Design Manager, on the Edit Master Pages page, select the HTML file, open the **Properties** menu, and then choose **Edit Properties**. On the **Edit** tab, clear the **Associated File** check box, and then choose **Save**.</span></span>
    
    <span data-ttu-id="f0017-p111">Informationen zum Unterteilen der Zuordnung können Sie direkt mit der Master-Datei arbeiten und die Änderungen zu speichern, ohne dass sie durch die HTML-Datei vorgenommenen Änderungen überschrieben. Sie können diese Zuordnung zu einem beliebigen Zeitpunkt wiederherstellen. Wenn Sie die Zuordnung wiederherstellen, wird die verknüpfte HTML-Datei mit der Master-Datei synchronisieren und überschreiben.</span><span class="sxs-lookup"><span data-stu-id="f0017-p111">Breaking the association enables you to work directly with the .master file and save changes without having them overwritten by any changes made to the HTML file. You can restore this association at any time. If you restore the association, the associated HTML file will sync to the .master file and overwrite it.</span></span>
    
  

## <a name="understand-the-associated-html-file"></a><span data-ttu-id="f0017-153">Verstehen der verknüpften HTML-Datei</span><span class="sxs-lookup"><span data-stu-id="f0017-153">Understand the associated HTML file</span></span>
<span data-ttu-id="f0017-154"><a name="UnderstandHTML"> </a></span><span class="sxs-lookup"><span data-stu-id="f0017-154"><a name="UnderstandHTML"> </a></span></span>

<span data-ttu-id="f0017-p112">Wenn Sie eine minimale Gestaltungsvorlage erstellen, eine HTML-Datei wird erstellt, das die Master-Datei zugeordnet ist, und diese HTML-Datei enthält viele Zeilen von Markup, die für die Funktionsweise von SharePoint spezifisch sind. Sie können die meisten dieses Markup ignorieren, und die meisten davon wird nicht angezeigt im endgültigen Markup Ihrer Website Wenn Sie die Datenquelle im Browser anzeigen, aber dieses Markup ist ein entscheidender Faktor, zum Synchronisieren von Änderungen aus der HTML-Datei an die Master-Datei, SharePoint tatsächlich verwendet. Jedes Mal, wenn Sie eine Änderung in Ihre HTML-Datei speichern ermöglicht diese SharePoint-Markup für dieselbe Änderung an der Datei zugeordneten Master im Hintergrund vorgenommen werden sollen. Weitere Informationen finden Sie in die Beispielen Markup in  [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f0017-p112">When you create a minimal master page, an HTML file is created that's associated with the .master file, and this HTML file contains many lines of markup that are specific to how SharePoint works. You can safely ignore most of this markup, and most of it does not appear in the final markup of your site when you view source in the browser, but this markup is critical for syncing changes from the HTML file to the .master file that SharePoint actually uses. Each time you save a change to your HTML file, this SharePoint markup makes it possible for that same change to be made to the associated .master file in the background. For more information, see the markup samples in  [How to: Convert an HTML file into a master page in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="f0017-159">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f0017-159">See also</span></span>
<span data-ttu-id="f0017-160"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="f0017-160"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="f0017-161">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0017-161">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f0017-162">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0017-162">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f0017-163">Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0017-163">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f0017-164">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="f0017-164">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

