---
title: SharePoint Design Manager - Bilddarstellungen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d08a74c0-5674-4f26-8646-11ea1f081c85
ms.openlocfilehash: 8ec58978836a572cc7452af4d7ad28c18e215089
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-design-manager-image-renditions"></a><span data-ttu-id="f77e6-102">SharePoint Design Manager - Bilddarstellungen</span><span class="sxs-lookup"><span data-stu-id="f77e6-102">SharePoint Design Manager image renditions</span></span>
<span data-ttu-id="f77e6-p101">Erfahren Sie, wie Sie eine Bilddarstellung erstellen, zu einer Seite hinzufügen und zuschneiden. Eine Bilddarstellung definiert die Maße, die zur Anzeige von Bildern auf SharePoint-Veröffentlichungswebsites verwendet werden. Mit Bilddarstellungen können Sie unterschiedlich große Versionen eines Bilds, die alle auf demselben Quellbild basieren, auf verschiedenen Seiten einer Veröffentlichungswebsite anzeigen. Wenn Sie eine Bilddarstellung erstellen, geben Sie die Breite und/oder die Höhe für alle Bilder an, die diese Bilddarstellung verwenden. Die Bilddarstellungen sind für jedes Bild verfügbar, das in eine Bibliothek der betreffenden Websitesammlung hochgeladen wird. Designer können beispielsweise eine Bilddarstellung zur Anzeige von Miniaturbildern und eine weitere Bilddarstellung zur Anzeige von Bannerbildern erstellen. Wenn ein Bild zu einer Seite hinzugefügt wird, kann der Autor die für das Bild zu verwendende Bilddarstellung angeben. Autoren können die Bilddarstellung außerdem zuschneiden, um den Teil des Bilds anzugeben, der in der Bilddarstellung verwendet werden soll. Beim Rendern der Seite wird die korrekte Bildgröße angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p101">Learn how to create an image rendition, how to add it to a page, and how to crop it. An image rendition defines the dimensions that are used to display images in SharePoint publishing sites. Image renditions enable you to display differently sized versions of an image on different pages in a publishing site, based on the same source image. When you create an image rendition, you specify the width and/or height for all images that use that image rendition. The image renditions are available for every image that is uploaded to a library in that site collection. For example, designers can create an image rendition to display thumbnail images and another image rendition to display banner images. When an image is added to a page, the author can specify the image rendition to use on that image. Authors can also crop the image rendition to specify the portion of the image to use in the image rendition. The correct image size is displayed when the page is rendered.</span></span>
  
    
    

<span data-ttu-id="f77e6-p102">Bilddarstellungen ermöglichen es Ihnen, ein einzelnes Bild auf unterschiedliche Weise zu rendern. Ein Bild kann in verschiedenen Größen oder mit unterschiedlichem Zuschnitt dargestellt werden. Bei der erstmaligen Anforderung eines Bilds verwendet SharePoint Server die angegebene Bilddarstellung, um das Bild zu generieren. Wenn ein Benutzer eine SharePoint-Website anzeigt, wird die korrekt dimensionierte Version des Bilds auf den Clientcomputer heruntergeladen. Dadurch wird die Größe der auf den Client heruntergeladenen Datei verringert, sodass sich die Websiteleistung verbessert.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p102">Image renditions enable you to render a single image in multiple ways. An image can be displayed in various sizes or with different cropping. The first time that an image is requested, SharePoint Server uses the specified image rendition to generate the image. When a user views a SharePoint site, the correctly sized version of the image is downloaded to the client computer. This reduces the size of the file that is downloaded to the client, which improves site performance.</span></span>
## <a name="prerequisites-for-managing-image-renditions"></a><span data-ttu-id="f77e6-117">Voraussetzungen für das Verwalten von Bilddarstellungen</span><span class="sxs-lookup"><span data-stu-id="f77e6-117">Prerequisites for managing image renditions</span></span>
<span data-ttu-id="f77e6-118"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-118"></span></span>

<span data-ttu-id="f77e6-119">Da Bilddarstellungen von anderen Features in SharePoint abhängen, müssen Sie sicherstellen, dass Sie alle in diesem Abschnitt aufgeführten Voraussetzungen erfüllen, bevor Sie die Verfahren in diesem Thema durchführen.</span><span class="sxs-lookup"><span data-stu-id="f77e6-119">Because image renditions have dependencies on other features in SharePoint Server 2013, make sure that you meet the prerequisites in this section before you perform the procedures in this topic. Prerequisites include:</span></span> <span data-ttu-id="f77e6-120">Zu den Voraussetzungen gehören folgende:</span><span class="sxs-lookup"><span data-stu-id="f77e6-120">Prerequisites include:</span></span>
  
    
    

- <span data-ttu-id="f77e6-p104">
  **Eine Veröffentlichungswebsitesammlung** - Die Websitesammlung, der Sie Bilddarstellungen hinzufügen, muss mithilfe des Veröffentlichungsportals oder der Websitesammlungsvorlage des Produktkatalogs erstellt worden sein. Alternativ müssen Veröffentlichungsfeatures in der Websitesammlung aktiviert sein, in der Sie Bilddarstellungen verwenden möchten. Weitere Informationen finden Sie unter [Übersicht über die Veröffentlichung auf Internet-, Intranet und Extranet-Websites](http://technet.microsoft.com/en-us/library/jj635881%28office.15%29.aspx) in der TechNet-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p104">**A publishing site collection** The site collection where you are adding image renditions must have been created by using the Publishing Portal or the Product Catalog site collection template. Or, publishing features must be enabled on the site collection where you want to use image renditions. For more information, see [Overview of publishing to Internet, intranet, and extranet sites](http://technet.microsoft.com/en-us/library/jj635881%28office.15%29.aspx) in the TechNet Library.</span></span>
    
  
- <span data-ttu-id="f77e6-p105">
  **Ein konfigurierter BLOB-Cache** - Der datenträgerbasierte BLOB-Cache steuert das Zwischenspeichern für Binary Large Objects (BLOBs), wie z. B. häufig verwendete Bild-, Audio- und Videodateien, sowie andere Dateien, die zum Anzeigen von Webseiten verwendet werden, wie z. B. CSS- und JS-Dateien. Der BLOB-Cache muss auf jedem Front-End-Webserver aktiviert werden, auf dem Sie Bilddarstellungen verwenden möchten. Wenn der BLOB-Cache nicht aktiviert ist, wird immer das ursprüngliche Bild verwendet. Weitere Informationen finden Sie unter [Konfigurieren von Cacheeinstellungen für eine Webanwendung](http://technet.microsoft.com/en-us/library/cc770229.aspx) in der TechNet-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p105">**A configured BLOB cache** The disk-based BLOB cache controls the caching for binary large objects (BLOBs), such as frequently used image, audio, and video files, and other files that are used to display webpages, such as .css files and .js files. The BLOB cache must be enabled on each front-end web server where you want to use image renditions. If the BLOB cache is not enabled, the original image is always used. For more information, see [Configure cache settings for a Web application](http://technet.microsoft.com/en-us/library/cc770229.aspx) in the TechNet Library.</span></span>
    
  
- <span data-ttu-id="f77e6-p106">**Eine Objektbibliothek (empfohlen)** - Sie können die Objektbibliotheksvorlage verwenden, um eine Bibliothek einzurichten, mit der Sie bequem umfangreiche Medienobjekte wie z. B. Bild-, Audio- oder Videodateien speichern, organisieren und suchen können. Weitere Informationen finden Sie unter [Einrichten einer Objektbibliothek zum Speichern von Bild-, Audio- oder Videodateien](http://office.microsoft.com/en-us/sharepoint-server-help/set-up-an-asset-library-to-store-image-audio-or-video-files-HA102785730.aspx) auf Office.com.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p106">**An asset library (recommended)** You can use the Asset Library template to set up a library that makes it easy to store, organize, and find rich media assets, such as image, audio, or video files. For more information, see [Set up an Asset Library to store image, audio, or video files](http://office.microsoft.com/en-us/sharepoint-server-help/set-up-an-asset-library-to-store-image-audio-or-video-files-HA102785730.aspx) on Office.com.</span></span>
    
  

## <a name="create-an-image-rendition"></a><span data-ttu-id="f77e6-130">Erstellen einer Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-130">Create an image rendition</span></span>
<span data-ttu-id="f77e6-131"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-131"></span></span>

<span data-ttu-id="f77e6-132">Wenn eine Bildwiedergabe erstellt wurde, erstellt SharePoint eine eindeutige ID, die diese Bildwiedergabe identifiziert.</span><span class="sxs-lookup"><span data-stu-id="f77e6-132">When an image rendition is created, SharePoint Server 2013 creates a unique ID that identifies that image rendition. An image is generated when SharePoint Server first receives a request for the image rendition.</span></span> <span data-ttu-id="f77e6-133">Ein Bild wird generiert, wenn SharePoint Server eine Anforderung für die Bildwiedergabe erhält.</span><span class="sxs-lookup"><span data-stu-id="f77e6-133">When an image rendition is created, SharePoint Server 2013 creates a unique ID that identifies that image rendition. An image is generated when SharePoint Server first receives a request for the image rendition.</span></span>
  
    
    

### <a name="to-create-an-image-rendition"></a><span data-ttu-id="f77e6-134">Erstellen einer Bildwiedergabe</span><span class="sxs-lookup"><span data-stu-id="f77e6-134">To create an image rendition</span></span>


1. <span data-ttu-id="f77e6-135">Stellen Sie sicher, dass das Benutzerkonto, mit dem dieses Verfahren ausgeführt wird, mindestens über Entwurfsberechtigungen für die Website auf oberster Ebene der Websitesammlung verfügt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-135">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="f77e6-136">Wechseln Sie in einem Browser zur Website der obersten Ebene der Veröffentlichungswebsitesammlung.</span><span class="sxs-lookup"><span data-stu-id="f77e6-136">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="f77e6-p108">Wählen Sie das Symbol **Einstellungen**. Wählen Sie auf der Seite **Webseiteeinstellungen** des Abschnitts **Aussehen und Verhalten** **Bildwiedergaben**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p108">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > <span data-ttu-id="f77e6-139">**Hinweis:** Die Seite Bildwiedergaben kann auch über die standardmäßige Homepage der Veröffentlichungswebsite geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-139">**Note** The Image Renditions page can also be opened from the default home page of the publishing site. In the I'm the Visual Designer section, choose Configure image renditions.</span></span> <span data-ttu-id="f77e6-140">Wählen Sie im Abschnitt **Ich bin der Visual Designer** **Bildwiedergaben konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-140">In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 
4. <span data-ttu-id="f77e6-141">Wählen Sie auf der Seite **Bildwiedergaben** die Option **Neues Element hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-141">On the **Image Renditions** page, choose **Add new item**.</span></span>
    
  
5. <span data-ttu-id="f77e6-p110">Geben Sie auf der Seite **Neue Bildwiedergabe** in das Feld **Name** einen Namen für die Darstellung ein, z. B.Thumbnail_Small.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p110">On the **New Image Rendition** page, in the **Name** box, enter a name for the rendition. For example, enterThumbnail_Small.</span></span>
    
  
6. <span data-ttu-id="f77e6-144">Geben Sie in die Textfelder **Breite** und **Höhe** die Breite und Höhe der Darstellung in Pixel ein, und klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-144">In the **Width** and **Height** text boxes, enter the width and height, in pixels, of the rendition, and then choose **Save**.</span></span>
    
  

## <a name="edit-an-image-rendition"></a><span data-ttu-id="f77e6-145">Bearbeiten einer Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-145">Edit an image rendition</span></span>
<span data-ttu-id="f77e6-146"><a name="Edit"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-146"></span></span>

<span data-ttu-id="f77e6-p111">Wenn eine Bilddarstellung bearbeitet wird, werden die neuen Maße bei der nächsten Anforderung des Bilds wirksam. Wenn es ein Bild gibt, das zuvor aus der Bilddarstellung generiert wurde, wird das Bild bei der nächsten Anforderung mit den neuen Maßen erneut generiert.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p111">When an image rendition is edited, the new dimensions take effect the next time that the image is requested. If there is an image that was generated previously from the image rendition, the image is regenerated with the new dimensions the next time that the image is requested.</span></span>
  
    
    

### <a name="to-edit-an-image-rendition"></a><span data-ttu-id="f77e6-149">So bearbeiten Sie eine Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-149">To edit an image rendition</span></span>


1. <span data-ttu-id="f77e6-150">Stellen Sie sicher, dass das Benutzerkonto, mit dem dieses Verfahren ausgeführt wird, mindestens über Entwurfsberechtigungen für die Website auf oberster Ebene der Websitesammlung verfügt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-150">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="f77e6-151">Wechseln Sie in einem Browser zur Website der obersten Ebene der Veröffentlichungswebsitesammlung.</span><span class="sxs-lookup"><span data-stu-id="f77e6-151">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="f77e6-p112">Wählen Sie das Symbol **Einstellungen**. Wählen Sie auf der Seite **Webseiteeinstellungen** des Abschnitts **Aussehen und Verhalten** **Bildwiedergaben**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p112">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > <span data-ttu-id="f77e6-154">**Hinweis:** Die Seite **Bildwiedergaben** kann auch über die standardmäßige Homepage der Veröffentlichungswebsite geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-154">**Note** The **Image Renditions** page can also be opened from the default home page of the publishing site. In the I'm the Visual Designer section, choose Configure image renditions.</span></span> <span data-ttu-id="f77e6-155">Wählen Sie im Abschnitt **Ich bin der Visual Designer** **Bildwiedergaben konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-155">In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 
4. <span data-ttu-id="f77e6-156">Wählen Sie auf der Seite **Bildwiedergaben** die Bildwiedergabe, die Sie bearbeiten möchten.</span><span class="sxs-lookup"><span data-stu-id="f77e6-156">On the **Image Renditions** page, choose the image rendition that you want to edit.</span></span>
    
  
5. <span data-ttu-id="f77e6-157">Ändern Sie auf der Seite **Bildwiedergabe bearbeiten** den Namen, die Breite oder Höhe der Bilddarstellung.</span><span class="sxs-lookup"><span data-stu-id="f77e6-157">On the **Edit Image Rendition** page, modify the name, width, or height of the image rendition.</span></span>
    
  

## <a name="add-an-image-rendition"></a><span data-ttu-id="f77e6-158">Hinzufügen einer Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-158">Add an image rendition</span></span>
<span data-ttu-id="f77e6-159"><a name="Add"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-159"></span></span>

<span data-ttu-id="f77e6-p114">Wenn Sie ein Bild zu einer Seite einer SharePoint-Veröffentlichungswebsite hinzufügen, können Sie die für dieses Bild zu verwendende Bilddarstellung angeben. Wenn die Seite in einem Browser gerendert wird, wird die korrekte Bildgröße angezeigt. Sie können die Bilddarstellung im Rich-Text-Editor, in einem Bildfeldsteuerelement oder in der Bild-URL angeben.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p114">When you add an image to a page in a SharePoint publishing site, you can specify the image rendition to use for that image. When the page is rendered in a browser, the correct image size is displayed. You can specify the image rendition in the Rich Text Editor, in an image field control, or in the image URL.</span></span>
  
    
    

### <a name="specify-the-image-rendition-by-using-the-rich-text-editor"></a><span data-ttu-id="f77e6-163">Angeben der Bilddarstellung mithilfe des Rich-Text-Editors</span><span class="sxs-lookup"><span data-stu-id="f77e6-163">Specify the image rendition by using the Rich Text Editor</span></span>

<span data-ttu-id="f77e6-p115">Wenn ein Bild auf einer Seite eingefügt wird, können Sie die zu verwendende Bilddarstellung angeben, damit die korrekte Bildgröße angezeigt wird, nachdem die Seite gerendert wurde. Die Angabe der Bilddarstellung im Rich-Text-Editor ist nur für Bilder möglich, die in derselben Websitesammlung gespeichert sind, in der sich auch die bearbeitete Seite befindet.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p115">When an image is inserted in a page, you can specify the image rendition to use so that the correct image size is displayed when the page is rendered. You can specify the image rendition in the Rich Text Editor only for images that are stored in the same site collection as the page that is being edited.</span></span>
  
    
    

### <a name="to-specify-an-image-rendition-by-using-the-rich-text-editor"></a><span data-ttu-id="f77e6-166">So geben Sie eine Bilddarstellung mithilfe des Rich-Text-Editors an</span><span class="sxs-lookup"><span data-stu-id="f77e6-166">To specify an image rendition by using the Rich Text Editor</span></span>


1. <span data-ttu-id="f77e6-167">Klicken Sie auf der Registerkarte **Seite** auf **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-167">On the **Page** tab, choose **Edit**.</span></span>
    
  
2. <span data-ttu-id="f77e6-168">Klicken Sie auf das Symbol **Einstellungen** und dann auf **Seite hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-168">Choose the **Settings** icon, and then choose **Add a page**.</span></span>
    
  
3. <span data-ttu-id="f77e6-169">Geben Sie im Fenster **Seite hinzufügen** einen Namen für die Seite ein, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-169">In the **Add a page** window, enter a name for the page, and then choose **Create**.</span></span>
    
  
4. <span data-ttu-id="f77e6-170">Positionieren Sie den Mauszeiger im Feld **Seiteninhalt**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-170">Place the pointer in the **Page Content** field.</span></span>
    
  
5. <span data-ttu-id="f77e6-171">Klicken Sie auf der Registerkarte **Einfügen** auf **Bild** und dann auf **Von SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-171">On the **Insert** tab, choose **Picture**, and then choose **From SharePoint**.</span></span>
    
  
6. <span data-ttu-id="f77e6-p116">Suchen Sie das Bild, das Sie zur Seite hinzufügen möchten, wählen Sie es aus, und klicken Sie dann auf **Einfügen**. Das Bild wird in voller Größe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p116">Locate the image that you want to add to the page, select the image, and then choose **Insert**. The image will be displayed at full size.</span></span>
    
  
7. <span data-ttu-id="f77e6-p117">Klicken Sie auf der Registerkarte **Design** in der Gruppe **Auswählen** auf **Formatvariante auswählen**, und wählen Sie dann eine Bilddarstellung aus. Das Bild wird entsprechend der für die Bilddarstellung angegebenen Größe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p117">On the **Design** tab, in the **Select** group, choose **Pick Rendition**, and then select an image rendition. The image will display according to the size specified for the image rendition.</span></span>
    
    > <span data-ttu-id="f77e6-176">**Hinweis:** Der Befehl **Formatvariante auswählen** ist nur für Bilder verfügbar, die in derselben Websitesammlung gespeichert sind wie die aktuell bearbeitete Seite.</span><span class="sxs-lookup"><span data-stu-id="f77e6-176">**Note** The **Pick Rendition** command is available only for images that are stored in the same site collection as the page that is being edited.</span></span>
8. <span data-ttu-id="f77e6-177">Wenn Sie die Bildwiedergabe zuschneiden möchten, wählen Sie **Formatvariante auswählen** und dann **Bildwiedergaben bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-177">If you want to crop the image rendition, choose **Pick Rendition**, and then choose **Edit Renditions**.</span></span>
    
    <span data-ttu-id="f77e6-178">Weitere Informationen zum Zuschneiden von Bilddarstellungen finden Sie im Abschnitt  [Zuschneiden einer Bilddarstellung](#Crop) dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="f77e6-178">For more information about cropping image renditions, see the  [Crop an image rendition](#Crop) section of this article.</span></span>
    
  

### <a name="specify-the-image-rendition-in-the-image-url"></a><span data-ttu-id="f77e6-179">Angeben der Bilddarstellung in der Bild-URL</span><span class="sxs-lookup"><span data-stu-id="f77e6-179">Specify the image rendition in the image URL</span></span>

<span data-ttu-id="f77e6-180">Sie können die Bilddarstellung angeben, indem Sie die Parameter "RenditionID", "Width" oder "Height" zur Bild-URL hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f77e6-180">You can specify the image rendition by adding the RenditionID, Width, or Height parameters to the image URL.</span></span>
  
    
    
 <span data-ttu-id="f77e6-181">**RenditionID** - Mit dem Parameter "RenditionID" können Sie die ID der zu verwendenden Bilddarstellung angeben.</span><span class="sxs-lookup"><span data-stu-id="f77e6-181">**RenditionID** Use the RenditionID parameter to specify the ID of the image rendition to use.</span></span>
  
    
    
 <span data-ttu-id="f77e6-p118">**Width** - Mit dem Parameter "Width" können Sie die Breite der Bilddarstellung in Pixeln angeben. SharePoint Server versucht, eine Bilddarstellung mit der angegebenen Breite zu finden. Als Nächstes versucht SharePoint Server eine Bilddarstellung zu finden, die breiter als die angegebene Breite ist. Wenn mehrere Bilddarstellungen vorhanden sind, die mit diesem Kriterium übereinstimmen, verwendet SharePoint Server die Bilddarstellung, deren Breite der angegebenen am nächsten kommt. Wenn keine Bilddarstellung mit einer Breite vorhanden ist, die größer oder gleich der angegebenen Breite ist, wird das ursprüngliche Bild verwendet.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p118">**Width** Use the Width parameter to specify the width, in pixels, of the image rendition. SharePoint Server tries to find an image rendition with the specified width. Next, SharePoint Server tries to find an image rendition that has a width that is larger than the specified width. If there are multiple image renditions that match this criterion, SharePoint Server uses the image rendition with the closest width to what was specified. If there is no image rendition with a width that is equal to or larger than the specified width the original image is used.</span></span>
  
    
    
 <span data-ttu-id="f77e6-p119">**Height** - Mit dem Parameter "Height" können Sie die Höhe der Bilddarstellung in Pixeln angeben. SharePoint Server versucht, eine Bilddarstellung mit der angegebenen Höhe zu finden. Als Nächstes versucht SharePoint Server eine Bilddarstellung zu finden, die höher als die angegebene Höhe ist. Wenn mehrere Bilddarstellungen vorhanden sind, die mit diesem Kriterium übereinstimmen, verwendet SharePoint Server die Bilddarstellung, deren Höhe der angegebenen am nächsten kommt. Wenn keine Bilddarstellung mit einer Höhe vorhanden ist, die größer oder gleich der angegebenen Höhe ist, wird das ursprüngliche Bild verwendet.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p119">**Height** Use the Height parameter to specify the height, in pixels, of the image rendition. SharePoint Server tries to find an image rendition with the specified height. Next, SharePoint Server tries to find an image rendition that has a height that is larger than the specified height. If there are multiple image renditions that match this criterion, SharePoint Server uses the image rendition with the closest height to what was specified. If there is no image rendition with a height that is equal to or larger than the specified height the original image is used.</span></span>
  
    
    
 <span data-ttu-id="f77e6-p120">**Width und Height** - Bei Angabe der Parameter "Width" und "Height" versucht SharePoint Server, eine Bilddarstellung mit der angegebenen Breite und Höhe zu finden. Als Nächstes versucht SharePoint Server eine Bilddarstellung zu finden, die dem angegebenen Breiten-/Höhen-Verhältnis am nächsten kommt. Wenn es mehrere Übereinstimmungen gibt, wird die Bilddarstellung mit dem nächstgrößeren Breiten-/Höhen-Verhältnis im Vergleich zur angeforderten Größe ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p120">**Width and Height** If both the Width parameter and the Height parameter are specified, SharePoint Server tries to find an image rendition with the specified width and height. Next, SharePoint Server tries to find a rendition that is closest to the width/height ratio specified. If there are multiple matches, the image rendition that has the closest larger width/height ratio to the requested size is chosen.</span></span>
  
    
    

> <span data-ttu-id="f77e6-195"> **Hinweis:** Wenn die Bild-URL die Parameter "RenditionID", "Width" und "Height" enthält, werden die Parameter "Width" und "Height" ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f77e6-195">**Note** If the image URL includes the RenditionID parameter and Width and Height parameters, the Width and Height parameters are ignored.</span></span> 
  
    
    

<span data-ttu-id="f77e6-196">Im folgenden Beispiel wird gezeigt, wie der RenditionID-Parameter verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f77e6-196">The following example shows how to use the RenditionID parameter:</span></span>
  
    
    



```HTML

<img src="/sites/pub/Assets/Lighthouse.jpg?RenditionID=2" />
```

<span data-ttu-id="f77e6-197">Das folgende Beispiel zeigt die Verwendung der Parameter "Width" und "Height":</span><span class="sxs-lookup"><span data-stu-id="f77e6-197">The following example shows how to use the Width and Height parameters:</span></span>
  
    
    



```HTML
<img src="/sites/pub/Assets/Lighthouse.jpg?Width=400&amp;Height=200" />
```


### <a name="specify-the-image-rendition-in-the-image-field-control"></a><span data-ttu-id="f77e6-198">Angeben der Bilddarstellung im Bildfeldsteuerelement</span><span class="sxs-lookup"><span data-stu-id="f77e6-198">Specify the image rendition in the image field control</span></span>

<span data-ttu-id="f77e6-p121">Ein Entwickler kann die Bilddarstellung angeben, die im Bildfeldsteuerelement verwendet werden soll. Verwenden Sie die **RenditionId**-Eigenschaft, um die ID der Bilddarstellung festzulegen. Weitere Informationen finden Sie unter **RenditionId**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p121">A developer can specify the image rendition to use in the image field control. Use the **RenditionId** property to set the ID of the image rendition. For more information, see **RenditionId**.</span></span>
  
    
    

## <a name="crop-an-image-rendition"></a><span data-ttu-id="f77e6-202">Zuschneiden einer Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-202">Crop an image rendition</span></span>
<span data-ttu-id="f77e6-203"><a name="Crop"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-203"></span></span>

<span data-ttu-id="f77e6-p122">Standardmäßig wird eine Bilddarstellung aus der Mitte des Bilds generiert. Sie können die Bilddarstellung für einzelne Bilder anpassen, indem Sie den Teil des Bilds zuschneiden, den Sie verwenden möchten. Wenn ein Foto beispielsweise ein Leuchtturmmotiv zeigt, die Bilddarstellung jedoch nicht den ganzen Leuchtturm enthält (siehe Abbildung 1), können Sie den ausgewählten Bildbereich so ändern, dass der ganze Leuchtturm angezeigt wird (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="f77e6-p122">By default, an image rendition is generated from the center of the image. You can adjust the image rendition for individual images by cropping the portion of the image that you want to use. For example, if a photo shows a lighthouse scene but the image rendition does not show the whole lighthouse (see Figure 1), you can change the selected image area so that the whole lighthouse is displayed (see Figure 2).</span></span> 
  
    
    

<span data-ttu-id="f77e6-207">**Abbildung 1: Ursprüngliche Bilddarstellung**</span><span class="sxs-lookup"><span data-stu-id="f77e6-207">**Figure 1. Original image rendition**</span></span>

  
    
    

  
    
    
![Wiedergabe des Originalbildes](../images/ImgRendition_orig.PNG)
  
    
    

<span data-ttu-id="f77e6-209">**Abbildung 2: Zugeschnittene Bilddarstellung**</span><span class="sxs-lookup"><span data-stu-id="f77e6-209">**Figure 2. Cropped image rendition**</span></span>

  
    
    

  
    
    
![Wiedergabe eines beschnittenen Bildes](../images/ImgRendition_crop.PNG)
  
    
    
<span data-ttu-id="f77e6-211">Eine Bilddarstellung kann in der Objektbibliothek oder auf einer Seite zugeschnitten werden, ohne das ursprüngliche Bild zu ändern.</span><span class="sxs-lookup"><span data-stu-id="f77e6-211">An image rendition can be cropped in the asset library or on a page, without changing the original image.</span></span> 
  
    
    
<span data-ttu-id="f77e6-212">Bilddarstellungen können folgendermaßen zugeschnitten werden:</span><span class="sxs-lookup"><span data-stu-id="f77e6-212">Image renditions can be cropped in the following ways:</span></span>
  
    
    

- <span data-ttu-id="f77e6-p123">Designer können eine Bilddarstellung in der Objektbibliothek zuschneiden. Ein Designer möchte beispielsweise angeben, wie ein Bild in der Miniaturbilddarstellung angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p123">Designers can crop an image rendition in the asset library. For example, a designer may want to specify how an image appears in the thumbnail image rendition.</span></span>
    
  
- <span data-ttu-id="f77e6-p124">Autoren können eine Bilddarstellung zuschneiden, wenn sie ein Bild in eine Seite einfügen. Dadurch können sie das Erscheinungsbild der Seite anpassen. Wenn ein Autor eine Bilddarstellung zuschneidet, wird auch die Bilddarstellung für das Bild geändert. Jedem Benutzer der Bilddarstellung wird das zugeschnittene Bild angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p124">Authors can crop an image rendition when they insert an image into a page. This enables them to customize the look of their page. When an author crops an image rendition, this also changes the image rendition for that image. Anyone who uses that image rendition sees the cropped image.</span></span>
    
    > <span data-ttu-id="f77e6-219">**Hinweis:** Ein Autor kann eine Bildwiedergabe nur zuschneiden, wenn das Originalbild in einer Bibliothek gespeichert ist, die sich in der gleichen Websitesammlung wie die Seite befindet, die gerade bearbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="f77e6-219">**Note** An author can crop an image rendition only when the original image is stored in a library that is in the same site collection as the page that is being edited. For example, in cross-site publishing scenarios, an author can crop the image rendition only if the image is stored in the same site collection as the catalog content. Otherwise, the image rendition must be cropped in the asset library.</span></span> <span data-ttu-id="f77e6-220">In Szenarien für die websiteübergreifende Veröffentlichung, kann ein Autor die Bildwiedergabe beispielsweise nur zuschneiden, wenn das Bild in der gleichen Websitesammlung wie der Kataloginhalt gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="f77e6-220">For example, in cross-site publishing scenarios, an author can crop the image rendition only if the image is stored in the same site collection as the catalog content.</span></span> <span data-ttu-id="f77e6-221">Andernfalls muss die Bildwiedergabe in der Objektbibliothek zugeschnitten werden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-221">Otherwise, the image rendition must be cropped in the asset library.</span></span> 

### <a name="crop-an-image-rendition-in-the-asset-library"></a><span data-ttu-id="f77e6-222">Zuschneiden ein Bildwiedergabe in der Objektbibliothek</span><span class="sxs-lookup"><span data-stu-id="f77e6-222">Crop an image rendition in the asset library</span></span>

<span data-ttu-id="f77e6-223">Designer können eine Bilddarstellung in der Objektbibliothek zuschneiden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-223">Designers can crop an image rendition in the asset library.</span></span>
  
    
    

### <a name="to-crop-an-image-rendition-in-the-asset-library"></a><span data-ttu-id="f77e6-224">So schneiden Sie eine Bilddarstellung in der Objektbibliothek zu</span><span class="sxs-lookup"><span data-stu-id="f77e6-224">To crop an image rendition in the asset library</span></span>


1. <span data-ttu-id="f77e6-225">Vergewissern Sie sich, dass das Benutzerkonto, mit dem dieses Verfahren durchgeführt wird, über Schreibberechtigungen für die Objektbibliothek verfügt, in der sich das Bild befindet.</span><span class="sxs-lookup"><span data-stu-id="f77e6-225">Verify that the user account that is performing this procedure has Write permissions to the asset library where the image is located.</span></span>
    
  
2. <span data-ttu-id="f77e6-226">Wechseln Sie in einem Browser zur Objektbibliothek.</span><span class="sxs-lookup"><span data-stu-id="f77e6-226">In a browser, go to the asset library.</span></span>
    
  
3. <span data-ttu-id="f77e6-227">Positionieren Sie den Mauszeiger in der unteren rechten Ecke des Bilds, dessen Darstellung Sie ändern möchten, wählen Sie die angezeigten Ellipsen ( **...**) aus, und klicken Sie dann auf **BEARBEITEN VON FORMATVARIANTEN**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-227">Position the pointer in the lower-right corner of the image whose rendition you want to change, select the ellipses ( **...**) that appears, and then choose **EDIT RENDITIONS**.</span></span>
    
    > <span data-ttu-id="f77e6-228">**Hinweis:** Sie können die Seite **Bearbeiten von Formatvarianten** auch öffnen, indem Sie den Mauszeiger über dem Vorschaubild in der Objektbibliothek positionieren und dann das Kontrollkästchen aktivieren, das unter dem Vorschaubild angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="f77e6-228">**Note** You can also open the **Edit Renditions** page by placing the pointer over the preview image in the asset library, and then selecting the check box that appears at the bottom of the preview image. Then, on the Design tab, choose Edit Renditions.</span></span> <span data-ttu-id="f77e6-229">Klicken Sie auf die Registerkarte **Entwurf** und wählen Sie **Bearbeiten von Formatvarianten**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-229">Then, on the **Design** tab, choose **Edit Renditions**.</span></span> 

    <span data-ttu-id="f77e6-230">Auf der Seite Bearbeiten von Formatvarianten wird ein Vorschaubild für jede Bildwiedergabe angezeigt, die in der Websitesammlung definiert ist.</span><span class="sxs-lookup"><span data-stu-id="f77e6-230">The Edit Renditions page displays a preview image for each image rendition that is defined in the site collection.</span></span>
    
  
4. <span data-ttu-id="f77e6-231">Suchen Sie nach der Bilddarstellung, die Sie ändern möchten, und klicken Sie dann auf **Zu ändernde Formatierung**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-231">Locate the image rendition that you want to change, and then choose **Click to change**.</span></span>
    
  
5. <span data-ttu-id="f77e6-232">Verwenden Sie im Fenster **Darstellung zuschneiden** das Bildtool, um den Teil des Bilds auszuwählen, den Sie in der Bilddarstellung verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f77e6-232">In the **Crop Rendition** window, use the image tool to select the portion of the image that you want to use in the image rendition.</span></span>
    
  
6. <span data-ttu-id="f77e6-233">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="f77e6-233">Choose **Save**.</span></span>
    
  
<span data-ttu-id="f77e6-234">Wenn sich das Bild und die aktuell bearbeitete Seite in derselben Websitesammlung befinden, können Sie eine Bilddarstellung auch mithilfe des Rich-Text-Editors zuschneiden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-234">If the image and the page that is being edited are in the same site collection, you also can crop an image rendition by using the Rich Text Editor.</span></span>
  
    
    

### <a name="crop-an-image-rendition-on-a-page"></a><span data-ttu-id="f77e6-235">Zuschneiden einer Bilddarstellung auf einer Seite</span><span class="sxs-lookup"><span data-stu-id="f77e6-235">Crop an image rendition on a page</span></span>

<span data-ttu-id="f77e6-p127">Autoren können eine Bilddarstellung zuschneiden, wenn sie ein Bild in eine Seite einfügen. Dadurch können sie das Erscheinungsbild der Seite anpassen. Wenn ein Autor eine Bilddarstellung zuschneidet, wird auch die Bilddarstellung für das Bild geändert. Jedem Benutzer der Bilddarstellung wird das zugeschnittene Bild angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p127">Authors can crop an image rendition when they insert an image into a page. This enables them to customize the look of their page. When an author crops an image rendition, this also changes the image rendition for that image. Anyone who uses that image rendition sees the cropped image.</span></span>
  
    
    

### <a name="to-crop-an-image-rendition-on-a-page"></a><span data-ttu-id="f77e6-240">So schneiden Sie eine Bilddarstellung auf einer Seite zu</span><span class="sxs-lookup"><span data-stu-id="f77e6-240">To crop an image rendition on a page</span></span>


1. <span data-ttu-id="f77e6-241">Vergewissern Sie sich, dass das Benutzerkonto, mit dem dieses Verfahren durchgeführt wird, über Schreibberechtigungen für die Objektbibliothek verfügt, in der sich das Bild befindet.</span><span class="sxs-lookup"><span data-stu-id="f77e6-241">Verify that the user account that is performing this procedure has Write permissions to the asset library where the image is located.</span></span>
    
  
2. <span data-ttu-id="f77e6-242">Wechseln Sie in einem Browser zu der SharePoint-Website, die das Bild enthält.</span><span class="sxs-lookup"><span data-stu-id="f77e6-242">In a browser, go to the SharePoint site that contains the image.</span></span>
    
  
3. <span data-ttu-id="f77e6-243">Klicken Sie auf der Registerkarte **Seite** auf **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-243">On the **Page** tab, choose **Edit**.</span></span>
    
  
4. <span data-ttu-id="f77e6-244">Wählen Sie das Bild aus, das Sie zuschneiden möchten.</span><span class="sxs-lookup"><span data-stu-id="f77e6-244">Select the image that you want to crop.</span></span>
    
  
5. <span data-ttu-id="f77e6-245">Klicken Sie auf der Registerkarte **Bild** des Menübands in der Gruppe **Auswählen** auf **Formatvariante auswählen**, und wählen Sie dann **Bearbeiten von Formatvarianten**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-245">On the **Image** tab of the ribbon, in the **Select** group, choose **Pick Rendition**, and then choose **Edit Renditions**.</span></span>
    
    <span data-ttu-id="f77e6-246">Auf der Seite **Bearbeiten von Formatvarianten** wird ein Vorschaubild für jede Bildwiedergabe angezeigt, die in der Websitesammlung definiert ist.</span><span class="sxs-lookup"><span data-stu-id="f77e6-246">The **Edit Renditions** page displays a preview image for each image rendition that is defined in the site collection.</span></span>
    
    > <span data-ttu-id="f77e6-247">**Hinweis:** Der Befehl **Formatvariante auswählen** ist nur für Bilder verfügbar, die in derselben Websitesammlung gespeichert sind wie die aktuell bearbeitete Seite.</span><span class="sxs-lookup"><span data-stu-id="f77e6-247">**Note** The **Pick Rendition** command is available only for images that are stored in the same site collection as the page that is being edited.</span></span>
6. <span data-ttu-id="f77e6-248">Suchen Sie die Bildwiedergabe, die Sie ändern möchten, und wählen Sie dann **Zum Ändern klicken**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-248">Locate the image rendition that you want to change, and then choose **Click to change**.</span></span>
    
  
7. <span data-ttu-id="f77e6-249">Verwenden Sie im Fenster **Darstellung zuschneiden** das Bildtool, um den Teil des Bilds auszuwählen, der in der Bilddarstellung verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="f77e6-249">In the **Crop Rendition** window, use the image tool to select the portion of the image to use in the image rendition.</span></span>
    
  
8. <span data-ttu-id="f77e6-250">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="f77e6-250">Choose **Save**.</span></span>
    
  

## <a name="delete-an-image-rendition"></a><span data-ttu-id="f77e6-251">Löschen einer Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-251">Delete an image rendition</span></span>
<span data-ttu-id="f77e6-252"><a name="Delete"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-252"></span></span>

<span data-ttu-id="f77e6-p128">Wenn eine Bilddarstellung gelöscht wird, wird sie nicht mehr für Bilder generiert. Wenn eine Website die gelöschte Bilddarstellung anfordert, wird das ursprüngliche Bild zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p128">When an image rendition is deleted, that image rendition is no longer generated for images. If a site requests the deleted image rendition, the original image is returned.</span></span>
  
    
    

### <a name="to-delete-an-image-rendition"></a><span data-ttu-id="f77e6-255">So löschen Sie eine Bilddarstellung</span><span class="sxs-lookup"><span data-stu-id="f77e6-255">To delete an image rendition</span></span>


1. <span data-ttu-id="f77e6-256">Stellen Sie sicher, dass das Benutzerkonto, mit dem dieses Verfahren ausgeführt wird, mindestens über Entwurfsberechtigungen für die Website auf oberster Ebene der Websitesammlung verfügt.</span><span class="sxs-lookup"><span data-stu-id="f77e6-256">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="f77e6-257">Wechseln Sie in einem Browser zur Website der obersten Ebene der Veröffentlichungswebsitesammlung.</span><span class="sxs-lookup"><span data-stu-id="f77e6-257">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="f77e6-p129">Wählen Sie das Symbol **Einstellungen**. Wählen Sie auf der Seite **Webseiteeinstellungen** des Abschnitts **Aussehen und Verhalten** **Bildwiedergaben**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-p129">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > <span data-ttu-id="f77e6-260">**Hinweis:** Die Seite **Bildwiedergaben** kann auch über die standardmäßige Homepage der Veröffentlichungswebsite geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="f77e6-260">**Note** The **Image Renditions** page can also be opened from the default home page of the publishing site. In the I'm the Visual Designer section, choose Configure image renditions.</span></span> <span data-ttu-id="f77e6-261">Wählen Sie im Abschnitt **Ich bin der Visual Designer** **Bildwiedergaben konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-261">In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 
4. <span data-ttu-id="f77e6-262">Suchen Sie auf der Seite **Bildwiedergaben** die Bildwiedergabe, die Sie löschen möchten, und wählen Sie dann **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="f77e6-262">On the **Image Renditions** page, locate the image rendition that you want to delete, and then choose **Delete**.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="f77e6-263">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f77e6-263">Additional resources</span></span>
<span data-ttu-id="f77e6-264"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="f77e6-264"></span></span>


-  [<span data-ttu-id="f77e6-265">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f77e6-265">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f77e6-266">SharePoint Design Manager - Branding- und Designfunktionen</span><span class="sxs-lookup"><span data-stu-id="f77e6-266">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  
-  [<span data-ttu-id="f77e6-267">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f77e6-267">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

