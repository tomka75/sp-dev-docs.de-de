---
title: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 03f72f65-b22b-4304-be92-f44ce0619372
ms.openlocfilehash: 73895457694d250f1527b69bd558335fd573263c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint"></a><span data-ttu-id="a7aa8-102">Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a7aa8-102">How to: Resolve errors and warnings when previewing a page in SharePoint</span></span>

<span data-ttu-id="a7aa8-p101">Nach dem Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage oder nach dem Erstellen eines Seitenlayouts können Sie eine Vorschau dieser Seite im Browser anzeigen. Bevor Sie eine Gestaltungsvorlage oder ein Seitenlayout in der Vorschau anzeigen können, müssen Sie jedoch alle Probleme beheben, die verhindern, dass die Seite in der serverseitigen Vorschau gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p101">After you convert an HTML file into a SharePoint master page, or after you create a page layout, you can preview that page in the browser. But before you can preview a master page or page layout, you may have to resolve any issues that prevent the server-side preview from rendering your page.</span></span>

## <a name="introduction-to-resolving-preview-errors"></a><span data-ttu-id="a7aa8-105">Einführung in das Beheben von Fehlern der Vorschau</span><span class="sxs-lookup"><span data-stu-id="a7aa8-105">Introduction to resolving preview errors</span></span>
<span data-ttu-id="a7aa8-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="a7aa8-p102">Nach dem Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage oder nach dem Erstellen eines Seitenlayouts können Sie eine Vorschau dieser Seite im Browser anzeigen. Beim Bearbeiten und Speichern Ihrer HTML-Gestaltungsvorlage oder Ihres Seitenlayouts können Sie die Vorschau aktualisieren, um genau zu sehen, wie SharePoint die Seite rendert.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p102">After you convert an HTML file into a SharePoint master page, or after you create a page layout, you can preview that page in the browser. As you edit and save your HTML master page or page layout, you can refresh the preview to see exactly how SharePoint renders your page.</span></span>
  
    
    
<span data-ttu-id="a7aa8-p103">Die Vorschau im Entwurfs-Manager zeigt eine aktuelle serverseitige Vorschau. Somit verwenden alle Codeausschnitte oder Steuerelemente auf der Seite, wie Navigationssteuerelemente oder suchgesteuerte Webparts, Livedaten. Zudem können Sie bei der Vorschau einer Gestaltungsvorlage oder eines Seitenlayouts eine generische Vorschau dieser Datei auswählen oder ansehen, wie eine bestimmte Seite Ihrer Website mit dieser Gestaltungsvorlage oder diesem Seitenlayout gerendert wird. Die serverseitige Vorschau ist ein äußerst nützliches Tool, das die Vorschau zur Entwurfszeit in einem HTML-Editor ergänzt. Weitere Informationen finden Sie unter  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p103">The preview in Design Manager is a live server-side preview, so any snippets or controls on your page, such as a navigation control or a search-driven Web Part, use live data. Also, when you preview a master page or page layout, you can choose a generic preview of just that file, or you can choose to preview how a specific page in your site renders with that master page or page layout. The server-side preview is a highly useful tool that complements the design-time preview in an HTML editor. For more information, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
  
    
    
<span data-ttu-id="a7aa8-p104">Bevor Sie eine Gestaltungsvorlage oder ein Seitenlayout in der Vorschau anzeigen können, müssen Sie jedoch alle Probleme beheben, die das Rendern der Seite in der serverseitigen Vorschau verhindern. Wenn die serverseitige Vorschau nicht funktioniert, bedeutet dies, dass die Gestaltungsvorlage oder das Seitenlayout nach der Anwendung auf Ihre Website ebenfalls nicht funktioniert. Nach dem Konvertieren einer Gestaltungsvorlage oder nach dem Erstellen eines Seitenlayouts können Sie im Entwurfs-Manager auf den Dateinamen oder den Konvertierungsstatus klicken, um eine Vorschau der Datei anzuzeigen. Im Infobereich der Vorschauseite werden etwaige Warnungen oder Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p104">But before you can preview a master page or page layout, you may have to resolve any issues that prevent the server-side preview from rendering your page. If the server-side preview isn't working, this means that the master page or page layout also won't work after they're applied to your site. In Design Manager, after you convert a master page or create a page layout, you can click the file name or conversion status to preview that file. On the preview page, the notification area at the top of the page displays any errors or warnings.</span></span>
  
    
    
<span data-ttu-id="a7aa8-117">Hier finden Sie die Fehler und Warnungen, die bei der Vorschau auftreten können, und Hilfe für deren Behebung.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-117">Here are the preview errors and warnings that you might encounter, and help for how to resolve them.</span></span>
  
    
    

## <a name="html-file-cannot-contain-form-tags"></a><span data-ttu-id="a7aa8-118">HTML-Datei darf keine \<form\>-Tags enthalten</span><span class="sxs-lookup"><span data-stu-id="a7aa8-118">HTML file cannot contain \<form\> tags</span></span>
<span data-ttu-id="a7aa8-119"><a name="FormTags"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-119"><a name="FormTags"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-120">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-120">Message</span></span>

 <span data-ttu-id="a7aa8-121">**Ihre Gestaltungsvorlage verfügt über ein oder mehrere \<FORM\>-HTML-Tags. Damit Ihre Gestaltungsvorlage funktioniert, müssen die Tags entfernt werden (die Tag-Inhalte müssen Sie jedoch nicht entfernen).**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-121">**Your Master Page has one or more HTML \<FORM\> tags. For your master page to work, remove the tags (but you can leave the content in them).**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="a7aa8-122">Auflösung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-122">Resolution</span></span>

<span data-ttu-id="a7aa8-123">SharePoint-Seiten werden bereits in ein **\<form\>**-Tag eingeschlossen, damit ASP.NET Postbacks ausführen kann (insbesondere enthält eine SharePoint-Gestaltungsvorlage das **<SharePoint:SharePointForm>**-Tag, das beim Rendern einer verknüpften Inhaltsseite ein tatsächliches ** \<form\>**-Tag erstellt).</span><span class="sxs-lookup"><span data-stu-id="a7aa8-123">SharePoint pages are already wrapped in a **\<form\>** tag so that ASP.NET can do post-backs (specifically, a SharePoint.master page contains the **<SharePoint:SharePointForm>** tag that creates an actual **\<form\>** tag when an associated content page is rendered).</span></span> <span data-ttu-id="a7aa8-124">Somit bedeutet die Aufnahme eines **\<form\>**-Tags in Ihre Gestaltungsvorlage oder Ihr Seitenlayout, dass das endgültige Rendering der Seite geschachtelte **\<form\>**-Tags enthalten würde, was in HTML nicht zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-124">So, including a **\<form\>** tag on your master page or page layout means that there would be nested **\<form\>** tags on the final rendering of the page, which is not valid in HTML.</span></span> <span data-ttu-id="a7aa8-125">Löschen Sie in Ihrem HTML-Editor alle **\<form\>**-Tags, speichern Sie die Seite, und aktualisieren Sie dann die Vorschau.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-125">In your HTML editor, delete any **\<form\>** tags, save the page, and then refresh the preview.</span></span>
  
    
    
<span data-ttu-id="a7aa8-126">Soll das Seitenlayout ein **\<form\>**-HTML-Tag enthalten, sollten Sie das Formular in einen Inhaltsplatzhalter mit der ID **PlaceHolderUtilityContent** einschließen. Dazu fügen Sie Ihrem HTML-Seitenlayout folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="a7aa8-126">If you want an HTML **\<form\>** tag in the page layout, you should put the form within a content placeholder with the ID **PlaceHolderUtilityContent** by adding this code to your HTML page layout:</span></span>
  
    
    



```HTML

<!--CS: Start Create Snippets From Custom ASP.NET Markup Snippet-->
<!--SPM:<SharePoint:AjaxDelta id="DeltaPlaceHolderUtilityContent" runat="server">-->
<!--SPM:<asp:ContentPlaceHolder id="PlaceHolderUtilityContent" runat="server" />-->
<!--SPM:</SharePoint:AjaxDelta>-->
<!--CE: End Create Snippets From Custom ASP.NET Markup Snippet-->
```

<span data-ttu-id="a7aa8-p106">Sie können Ihrer Seite auch das HTML-Formularwebpart oder das InfoPath-Formularwebpart aus dem Codeausschnittkatalog hinzufügen. Weitere Informationen finden Sie unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p106">You can also add the HTML Form Web Part or the InfoPath Form Web Part to your page from the Snippet Gallery. For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
  
    
    

## <a name="html-file-must-be-xml-compliant"></a><span data-ttu-id="a7aa8-129">HTML-Datei muss XML-konform sein</span><span class="sxs-lookup"><span data-stu-id="a7aa8-129">HTML file must be XML-compliant</span></span>
<span data-ttu-id="a7aa8-130"><a name="XMLCompliant"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-130"><a name="XMLCompliant"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-131">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-131">Message</span></span>

 <span data-ttu-id="a7aa8-132">**Für XML-Kompatibilität benötigt SharePoint HTML-Dateien. Ihre Datei ist nicht XML-kompatibel, wahrscheinlich aufgrund von Tageigenschaften ohne Anführungszeichen, fehlenden Endtags oder ungültigen Eigenschaften in den Tags. {Art des Fehlers, Ort des Fehlers}. Aufgetreten bei: {Zeit}.**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-132">**SharePoint requires HTML files to be XML-compliant. Your file isn't XML-compliant, likely because of tag properties without quotes, missing closing tags, or invalid properties in tags. {Type of error, location of error}. Occurred at: {Time}.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="a7aa8-133">Auflösung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-133">Resolution</span></span>

<span data-ttu-id="a7aa8-p107">Für die Konvertierung einer HTML-Datei in die entsprechende ASP.NET-Datei muss die HTML-Datei XML-konform sein. Dieser Fehler gibt bestimmtes Markup in der HTML-Datei an, das nicht XML-kompatibel ist. Führen Sie die HTML-Datei über eine XML-Bestätigung aus, beheben Sie etwaige Probleme mit Ihrem HTML-Editor, speichern Sie die Datei und aktualisieren Sie dann die Vorschau.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p107">For an HTML file to be converted into the corresponding ASP.NET file, the HTML file must be XML-compliant. This error identifies specific markup in your HTML file that is not XML-compliant. Run the HTML file through an XML validator, fix any issues in your HTML editor, save the file, and then refresh the preview.</span></span>
  
    
    

> <span data-ttu-id="a7aa8-137">**Hinweis:** Diese Anforderung setzt einige HTML 5-Normen außer Kraft.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-137">**Note:** This requirement overrides some HTML 5 standards.</span></span> <span data-ttu-id="a7aa8-138">Beispielsweise können Sie den Dokumenttyp (doctype) in HTML 5 in Kleinschreibung angeben, während er in XML in Großbuchstaben geschrieben sein muss.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-138">For example, in HTML 5 you can specify the doctype in lowercase, but in XML the doctype must be uppercase.</span></span> 
  
    
    


  
    
    

## <a name="html-file-contains-problematic-markup"></a><span data-ttu-id="a7aa8-139">HTML-Datei enthält problematisches Markup</span><span class="sxs-lookup"><span data-stu-id="a7aa8-139">HTML file contains problematic markup</span></span>
<span data-ttu-id="a7aa8-140"><a name="ProblematicMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-140"><a name="ProblematicMarkup"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-141">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-141">Message</span></span>

 <span data-ttu-id="a7aa8-142">**SharePoint kann diese Datei nicht analysieren, höchstwahrscheinlich aufgrund eines falsch formatierten SharePoint-Ausschnitts. Das Markup an folgender Position verursacht Probleme. Bearbeiten Sie das Markup manuell, um es zu reparieren, oder ersetzen Sie es durch einen neuen Ausschnitt aus dem Codeausschnittkatalog. {Art des Fehlers, Ort des Fehlers}. Aufgetreten bei: {Zeit}.**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-142">**SharePoint can't parse this file, most likely because of an incorrectly formatted SharePoint snippet. The markup at the following location is causing problems. Edit the markup manually to fix it, or replace it with a new snippet from the Snippet Gallery. {Type of error, location of error}. Occurred at: {Time}.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="a7aa8-143">Auflösung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-143">Resolution</span></span>

<span data-ttu-id="a7aa8-p109">Dieser Fehler wird angezeigt, wenn ein Problem mit einem SharePoint-Ausschnitt in Ihrer HTML-Datei auftritt. Zur Behebung des Fehlers machen Sie die Änderung rückgängig, die den Fehler verursacht hat, oder ersetzen Sie den problematischen Codeausschnitt durch einen neuen, entweder aus dem Codeausschnittkatalog oder aus einer anderen Gestaltungsvorlage oder Seitenlayoutdatei, die eine funktionierende Version des Ausschnitts enthält. Nach dem Reparieren oder Ersetzen des Codeausschnitts speichern Sie die Seite in Ihrem HTML-Editor, und aktualisieren Sie dann die Vorschau.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p109">You see this error when there is a problem with a SharePoint snippet in your HTML file. To fix this error, undo whatever change caused the error, or replace the problematic snippet with a new one, either from the Snippet Gallery or from a different master page or page layout file that has a working version of the snippet. In your HTML editor, after you fix or replace the snippet, save the page, and then refresh the preview.</span></span>
  
    
    

## <a name="master-page-for-a-page-layout-has-changed"></a><span data-ttu-id="a7aa8-147">Gestaltungsvorlage für ein Seitenlayout wurde geändert</span><span class="sxs-lookup"><span data-stu-id="a7aa8-147">Master page for a page layout has changed</span></span>
<span data-ttu-id="a7aa8-148"><a name="PageLayoutChanged"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-148"><a name="PageLayoutChanged"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-149">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-149">Message</span></span>

 <span data-ttu-id="a7aa8-150">**Diese Gestaltungsvorlage des Seitenlayouts hat sich geändert, was auf Ihrer Website zu Inkonsistenzen führt. Klicken Sie hier, um die Bereiche Ihres Seitenlayouts zu ändern, die Bereiche der Gestaltungsvorlage repräsentieren.**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-150">**This page layout's master page has changed, which will cause inconsistencies across your site. Click here to update the sections of your page layout that represent master page regions.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="a7aa8-151">Auflösung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-151">Resolution</span></span>

<span data-ttu-id="a7aa8-p110">Damit ein Seitenlayout mit einer bestimmten Gestaltungsvorlage funktioniert, müssen beide den gleichen Satz von Inhaltsplatzhaltern enthalten. Wenn Sie ein Seitenlayout basierend auf einer bestimmten Gestaltungsvorlage erstellen und dann diese HTML-Gestaltungsvorlage bearbeiten, wird diese Meldung angezeigt. Auch wenn Sie wissen, dass durch Änderungen an der Gestaltungsvorlage keine Inhaltsplatzhalter hinzugefügt oder entfernt wurden, sollten Sie die Inhaltsbereiche des Seitenlayouts aktualisieren, um eine Vorschau aller Änderungen der Gestaltungsvorlage anzuzeigen, die sich auf das Seitenlayout auswirken.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p110">For a page layout to work with a given master page, the two must have the same set of content placeholders. If you create a page layout based on a particular master page, and then edit that HTML master page, you'll see this message. Even if you know that changes to the master page didn't add or remove content placeholders, you should update the content regions of your page layout anyway, so that you can preview any changes from the master page that might affect your page layout.</span></span>
  
    
    

## <a name="reset-the-preview"></a><span data-ttu-id="a7aa8-155">Zurücksetzen der Vorschau</span><span class="sxs-lookup"><span data-stu-id="a7aa8-155">Reset the preview</span></span>
<span data-ttu-id="a7aa8-156"><a name="ResetPreview"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-156"><a name="ResetPreview"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-157">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-157">Message</span></span>

 <span data-ttu-id="a7aa8-158">**Bei Ihrer Gestaltungsvorlage (Ihrem Seitenlayout) sind keine Warnungen oder Fehler vorhanden. Setzen Sie die Vorschau auf den ursprünglichen Zustand zurück.**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-158">**Your master page (page layout) doesn't have any warnings or errors. Reset the preview to its original state.**</span></span>
  
    
    

### <a name="explanation"></a><span data-ttu-id="a7aa8-159">Erklärung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-159">Explanation</span></span>

<span data-ttu-id="a7aa8-p111">Diese Meldung bestätigt, dass keine Fehler oder Probleme beim Konvertierungsprozess aufgetreten sind. Allerdings können Sie bei der Vorschau einer Seite von dieser bestimmten Seite weg navigieren oder die Vorschau auf andere Weise ändern. In diesem Fall können Sie im Meldungsbereich immer **Vorschau zurücksetzen** auswählen. Dadurch wird die Vorschau aktualisiert, sodass die gerade bearbeitete Gestaltungsvorlage bzw. das bearbeitete Seitenlayout und die in der Option **Vorschau-Seite ändern** in der oberen linken Ecke ausgewählte Seite verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p111">This message simply confirms that the conversion process worked with no errors or issues. However, when you preview a page, you may navigate away from that specific page or change the preview in some other way. If this happens, you can always choose **Reset the preview** in the message area. Doing so refreshes the preview so that it uses the specific master page or page layout that you're working on, and whatever page you've selected in the **Change Preview Page** option in the upper-left corner.</span></span>
  
    
    

## <a name="change-the-preview-page"></a><span data-ttu-id="a7aa8-164">Ändern der Vorschauseite</span><span class="sxs-lookup"><span data-stu-id="a7aa8-164">Change the preview page</span></span>
<span data-ttu-id="a7aa8-165"><a name="ChangePreviewPage"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-165"><a name="ChangePreviewPage"> </a></span></span>


### <a name="message"></a><span data-ttu-id="a7aa8-166">Nachricht</span><span class="sxs-lookup"><span data-stu-id="a7aa8-166">Message</span></span>

 <span data-ttu-id="a7aa8-167">**In der Vorschau wird derzeit die Gestaltungsvorlage (das Seitenlayout) ohne Inhalt angezeigt. Über das Menü oben können Sie die Seite in der Vorschau ändern.**</span><span class="sxs-lookup"><span data-stu-id="a7aa8-167">**You're currently previewing your master page (page layout) without any content. You can change the page you're previewing from the menu above.**</span></span>
  
    
    

### <a name="explanation"></a><span data-ttu-id="a7aa8-168">Erklärung</span><span class="sxs-lookup"><span data-stu-id="a7aa8-168">Explanation</span></span>

<span data-ttu-id="a7aa8-p112">Diese Meldung wird angezeigt, wenn Sie keine SharePoint-Liveseite verwenden, um eine Vorschau der Gestaltungsvorlage oder des Seitenlayouts anzuzeigen. Wenn Sie z. B. ein Seitenlayout in der Vorschau anzeigen, können Sie in der linken oberen Ecke auf **Vorschau-Seite ändern** klicken und dann eine bestimmte Inhaltsseite für die Vorschau mit dem Seitenlayout auswählen. So können Sie das Seitenlayout mit tatsächlichem Seiteninhalt in den Seitenfeldern anzeigen. Wenn die Vorschau nur die Positionen von **ContentPlaceHolderMain** oder Seitenfeldern anzeigen soll, können Sie mit **Vorschau-Seite ändern** jederzeit wieder in eine generische Vorschau wechseln.</span><span class="sxs-lookup"><span data-stu-id="a7aa8-p112">You see this message when you aren't using a live SharePoint page with which to preview your master page or page layout. For example, if you're previewing a page layout, you can choose **Change Preview Page** in the upper-left corner, and then select a specific content page to preview with your page layout. This way, you can preview the page layout with actual page content in the page fields. If you want the preview to show just the positions of **ContentPlaceHolderMain** or page fields, you can always use **Change Preview Page** to switch back to a generic preview.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a7aa8-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a7aa8-173">Additional resources</span></span>
<span data-ttu-id="a7aa8-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a7aa8-174"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="a7aa8-175">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a7aa8-175">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a7aa8-176">Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager</span><span class="sxs-lookup"><span data-stu-id="a7aa8-176">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="a7aa8-177">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="a7aa8-177">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

