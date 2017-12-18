---
title: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a76ab289-3256-45de-ac63-d5112a74e3c7
ms.openlocfilehash: df93a6b57fc719e83f337b061e575b7caa97eba6
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="convert-an-html-file-into-a-master-page-in-sharepoint"></a><span data-ttu-id="6d8c6-102">Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d8c6-102">How to: Convert an HTML file into a master page in SharePoint</span></span>

<span data-ttu-id="6d8c6-p101">Mit dem Entwurfs-Manager können Sie eine HTML-Datei in eine SharePoint-Gestaltungsvorlage (MASTER-Datei) konvertieren. Nach der Konvertierung wird die HTML-Datei mit der Gestaltungsvorlage verknüpft, sodass nach dem Bearbeiten und Speichern der HTML-Datei die Änderungen mit der zugeordneten Gestaltungsvorlage synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p101">With Design Manager, you can convert an .html file into a SharePoint master page, a .master file. After the conversion, the HTML file and master page are associated, so that when you edit and save the HTML file, the changes are synced to the associated master page.</span></span>

## <a name="introduction-to-converting-a-master-page"></a><span data-ttu-id="6d8c6-105">Einführung in das Konvertieren in eine Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="6d8c6-105">Introduction to converting a master page</span></span>
<span data-ttu-id="6d8c6-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-106"><a name="Introduction"> </a></span></span>

 <span data-ttu-id="6d8c6-p102">Mit dem Entwurfs-Manager können Sie eine HTML-Datei in eine SharePoint-Gestaltungsvorlage mit der Erweiterung ".master" konvertieren. Nach der Konvertierung werden die HTML-Datei und Gestaltungsvorlage miteinander verknüpft, sodass nach Bearbeiten und Speichern der HTML-Datei die Änderungen mit der zugeordneten Gestaltungsvorlage synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p102">With Design Manager, you can convert an.html file into a SharePoint master page, a .master file. After the conversion, the HTML file and master page are associated, so that when you edit and save the HTML file, the changes are synced to the associated master page.</span></span>
  
    
    
<span data-ttu-id="6d8c6-p103">Warum sollen Sie eine HTML-Datei konvertieren, anstatt eine Gestaltungsvorlage von Grund auf neu zu erstellen? In SharePoint funktionieren Gestaltungsvorlagen exakt wie in ASP.NET. Doch SharePoint verlangt außerdem, dass bestimmte für SharePoint spezifische Elemente wie Steuerelemente und Inhaltsplatzhalter auf der Seite vorhanden sein müssen, damit SharePoint die jeweilige Gestaltungsvorlage ordnungsgemäß rendern kann. Durch das Konvertieren einer HTML-Datei in eine voll funktionsfähige SharePoint-Gestaltungsvorlage mit dem Entwurfs-Manager müssen Sie nicht mit ASP.NET- oder SharePoint-spezifischem Markup vertraut sein. Stattdessen können Sie sich auf das Entwerfen Ihrer Website in HTML, CSS und JavaScript konzentrieren.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p103">Why do you want to convert an HTML file, instead of creating a .master file from scratch? In SharePoint, master pages work exactly as they do in ASP.NET, but SharePoint also requires that certain elements, such as controls and content placeholders that are specific to SharePoint, must be present on the page for SharePoint to correctly render that master page. By using Design Manager to convert an HTML file into a fully functioning SharePoint master page, you don't have to know about ASP.NET or the SharePoint-specific markup; instead, you can focus on designing your site in HTML, CSS, and JavaScript.</span></span>
  
    
    
<span data-ttu-id="6d8c6-112">Beim Konvertieren einer HTML-Datei in eine Gestaltungsvorlage passiert Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-112">When you convert an HTML file into a master page:</span></span>
  
    
    

- <span data-ttu-id="6d8c6-113">Eine MASTER-Datei, die denselben Namen wie Ihre HTML-Datei hat, wird im Gestaltungsvorlagenkatalog erstellt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-113">A .master file with the same name as your HTML file is created in the Master Page Gallery.</span></span>
    
  
- <span data-ttu-id="6d8c6-114">Das gesamte von SharePoint verlangte Markup wird der MASTER-Datei hinzugefügt, damit die Gestaltungsvorlage ordnungsgemäß gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-114">All markup required by SharePoint is added to the .master file so that the master page renders correctly.</span></span>
    
  
- <span data-ttu-id="6d8c6-115">Markup wie Kommentare, **\<div\>**-Tags, Codeausschnitte und Inhaltsplatzhalter werden Ihrer ursprünglichen HTML-Datei hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-115">Markup such as comments, **\<div\>** tags, snippets, and content placeholders are added to your original HTML file.</span></span>
    
  
- <span data-ttu-id="6d8c6-116">Die HTML-Datei und Gestaltungsvorlage werden miteinander verknüpft, damit spätere Änderungen an der HTML-Datei mit der MASTER-Datei synchronisiert werden, sobald die HTML-Datei gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-116">The HTML file and master page are associated, so that any later edits to the HTML file are synced to the .master file when the HTML file is saved.</span></span>
    
  

> <span data-ttu-id="6d8c6-117">**Hinweis:** Die Synchronisierung erfolgt nur in eine Richtung.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-117">**Note:** The syncing goes in one direction only.</span></span> <span data-ttu-id="6d8c6-118">Änderungen an der HTML-Gestaltungsvorlage werden mit der zugehörigen .master-Datei synchronisiert, aber wenn Sie die .master-Datei direkt bearbeiten, werden diese Änderungen nicht mit der HTML-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-118">Changes to the HTML master page are synced to the associated .master file, but if you choose to edit the .master file directly the changes are not synced to the HTML file.</span></span> <span data-ttu-id="6d8c6-119">Jede HTML-Gestaltungsvorlage (und jedes HTML-Seitenlayout) verfügt über eine Eigenschaft mit dem Namen **Zugeordnete Datei**, die standardmäßig auf **True** festgelegt ist und mit deren Hilfe die Zuordnung und die Synchronisierung zwischen Dateien eingerichtet wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-119">Every HTML master page (and every HTML page layout) has a property named **Associated File** that is set to **True** by default, which creates the association and syncing between files.</span></span>
  
    
    

<span data-ttu-id="6d8c6-p105">Wenn Sie über ein Paar miteinander verknüpfter Dateien (HTML und MASTER) verfügen und Sie die MASTER-Datei bearbeiten, ohne die Verknüpfung zu unterbrechen, werden die Änderungen an der MASTER-Datei gespeichert. Doch Sie können die MASTER-Datei weder einchecken noch veröffentlichen, weshalb die Änderungen nicht auf sinnvolle Weise gespeichert werden. Bei Änderungen an der HTML-Datei wird die MASTER-Datei überschrieben. Wenn Sie die HTML-Datei einchecken oder veröffentlichen, überschreiben die Änderungen an der HTML-Datei alle Änderungen, die an der MASTER-Datei erfolgt sind. Die Änderungen an der MASTER-Datei gehen daraufhin verloren.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p105">If you have a pair of associated files (HTML and .master) and you edit the .master file without breaking the association, the changes to the .master file will be saved, but you can't check in or publish the .master file, so those changes are not saved in a meaningful way. Any changes to the HTML file override the .master file. If you check in or publish the HTML file, the HTML file changes override any changes that were made to the .master file. The changes to the .master file are lost.</span></span>
  
    
    
<span data-ttu-id="6d8c6-p106">Als Entwickler, der mit ASP.NET vertraut ist, können Sie nach Wunsch nur mit der MASTER-Datei arbeiten und die Verknüpfung zwischen den Dateien aufheben. Dazu wählen Sie im Entwurfs-Manager den Befehl **Eigenschaften bearbeiten** für die HTML-Datei aus und deaktivieren das Kontrollkästchen **Zugeordnete Datei**. Sie können später die Verknüpfung zwischen den Datei wieder aktivieren, indem Sie die Eigenschaften bearbeiten und dieses Kontrollkästchen aktivieren. In diesem Fall wird die MASTER-Datei erneut von der HTML-Datei überschrieben, und an der MASTER-Datei erfolgte Änderungen gehen verloren.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p106">If you're a developer comfortable working with ASP.NET, you can choose to work only with the .master file by breaking the association between the files. To break the association between the HTML file and the .master file, in Design Manager, choose **Edit Properties** for the HTML file, and then clear the **Associated File** check box. You can later re-associate the files by editing the properties and selecting this check box, in which case the HTML file will again overwrite the .master file, and changes made to the .master file will be lost.</span></span>
  
    
    

## <a name="prepare-the-html-file-for-conversion"></a><span data-ttu-id="6d8c6-127">Vorbereiten der HTML-Datei auf die Konvertierung</span><span class="sxs-lookup"><span data-stu-id="6d8c6-127">Prepare the HTML file for conversion</span></span>
<span data-ttu-id="6d8c6-128"><a name="Prepare"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-128"><a name="Prepare"> </a></span></span>

<span data-ttu-id="6d8c6-129">Vor der Konvertierung Ihrer HTML-Datei sollten Sie einige bewährte Methoden und Tipps befolgen:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-129">Before you convert your HTML file, here are some best practices and guidance to consider:</span></span>
  
    
    

- <span data-ttu-id="6d8c6-p107">Berücksichtigen Sie das SharePoint-Seitenmodell. Weitere Informationen finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md). Wenn Sie die HTML-Modelle Ihrer Website entwerfen, verfügen Sie wahrscheinlich über mehrere HTML-Dateien für verschiedene Seitentypen, so z. B. über eine Artikel- oder Kategorieseite, die Webparts enthält, mit denen eine Kategorie von Elementen in einem Katalog angezeigt wird. Doch nur eine HTML-Datei wird in eine Gestaltungsvorlage konvertiert. Eine HTML-Datei kann in eine Gestaltungsvorlage konvertiert werden, doch eine HTML-Datei kann nicht direkt in ein Seitenlayout umgewandelt werden, da für ein Seitenlayout Seitenfelder erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p107">Consider the SharePoint page model. For more information, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md). As you design the HTML mockups of your site, you'll probably have several HTML files for different types of pages, such as an article page or a category page that contains Web Parts that display a category of items from a catalog. But, only one HTML file will be converted into the master page. An HTML file can be converted into a master page, but an HTML file can't be converted directly into a page layout because a page layout requires page fields.</span></span>
    
  
- <span data-ttu-id="6d8c6-135">Stellen Sie sicher, dass Ihre HTML-Datei XML-kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-135">Make sure your HTML file is XML-compliant.</span></span> <span data-ttu-id="6d8c6-136">Damit die Umwandlung funktioniert, muss die HTML-Datei XML-kompatibel sein.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-136">For the conversion to work, the HTML file must be XML-compliant.</span></span> <span data-ttu-id="6d8c6-137">Leider setzt diese Anforderung einige HTML 5-Normen außer Kraft. Beispielsweise können Sie den **Dokumenttyp** **(doctype)** in HTML 5 in Kleinschreibung angeben, während er in XML in Großbuchstaben geschrieben sein muss.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-137">Unfortunately, this requirement overrides some HTML 5 standards—for example, in HTML 5 you can specify the **doctype** in lowercase, but in XML the **doctype** must be uppercase.</span></span> <span data-ttu-id="6d8c6-138">Darüber hinaus sollten Sie alle ** \<form\>**-Tags aus der HTML-Datei entfernen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-138">Also, you should remove any **\<form\>** tags from your HTML file.</span></span> <span data-ttu-id="6d8c6-139">Ziehen Sie in Betracht, Ihre HTML-Datei einer externen XML-Datenprüfung zu unterziehen, um XML-Fehler vor der Konvertierung zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-139">Consider running your HTML file through an external XML validator to identify XML errors before conversion.</span></span>
    
  
- <span data-ttu-id="6d8c6-140">Berücksichtigen Sie diese wichtigen Leitlinien für Ihre CSS-Verweise:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-140">Consider these important guidelines for your CSS references:</span></span>
    
  - <span data-ttu-id="6d8c6-141">Platzieren Sie keine **\<Formatvorlagen\>**-Bausteine im ** \<head\> **-Tag.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-141">Don't put **\<style\>** blocks in the **\<head\>** tag.</span></span> <span data-ttu-id="6d8c6-142">Dieses Formate werden während der Konvertierung entfernt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-142">These styles are removed during conversion.</span></span> <span data-ttu-id="6d8c6-143">Stellen Sie stattdessen eine Verknüpfung von Ihrer HTML-Datei zu einer externen CSS-Datei her.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-143">Instead, link from your HTML file to an external CSS file.</span></span>
    
  
  - <span data-ttu-id="6d8c6-144">Fügen Sie `ms-design-css-conversion="no"` zum **\<CSS-Link\>**-Tag hinzu, wenn Sie eine Webschriftart verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-144">Add  `ms-design-css-conversion="no"` to the **\<CSS link\>** tag if you're using a web font.</span></span>
    
  
  - <span data-ttu-id="6d8c6-145">Seien Sie vorsichtig, wenn Sie Formatvorlagen auf allgemeine HTML-Tags wie **\<body\>**, **\<div\>** und **\<img\>** anwenden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-145">Be cautious about applying styles to general HTML tags like **\<body\>**, **\<div\>**, and **\<img\>**.</span></span> <span data-ttu-id="6d8c6-146">Alles, was sich in Ihrem SharePoint-Entwurf befindet, einschließlich des Menübands, befindet sich im **\<body\>**-Tag.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-146">Everything within your SharePoint design, including the ribbon, is within the **\<body\>** tag.</span></span> <span data-ttu-id="6d8c6-147">Formatvorlagen, die Sie in der Regel dem ** \<body\>**-Tag zuweisen, sollten Sie stattdessen **\<div id="s4-bodyContainer"\>** zuweisen, da SharePoint diesen Tag für den Hauptteil der Seite verwendet.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-147">For styles that you would usually apply to the **\<body\>** tag, consider applying them instead to **\<div id="s4-bodyContainer"\>**, which is a tag that SharePoint uses for the main body of the page.</span></span> <span data-ttu-id="6d8c6-148">Darüber hinaus verwendet SharePoint viele Bilder, die von allen Formatvorlagen, die Sie auf das **\<img\>**-Tag anwenden, beeinflusst werden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-148">Also, SharePoint uses many images that are affected by whatever styles you apply to the **\<img\>** tag.</span></span>
    
  
  - <span data-ttu-id="6d8c6-149">Viele Designer gestalten die Navigation durch Anwenden von Klassen auf **\<ul\>**- und **\<li\>**-Elemente.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-149">Many designers style the navigation by applying classes to **\<ul\>** and **\<li\>** elements.</span></span> <span data-ttu-id="6d8c6-150">SharePoint verwendet jedoch dynamische Navigationssteuerelemente, die Sie über Ihre Gestaltungsvorlage aus dem Codeausschnittkatalog hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-150">But, SharePoint uses a dynamic navigation control, which you can add to your master page from the Snippet Gallery.</span></span> <span data-ttu-id="6d8c6-151">SharePoint-Navigationssteuerelemente werden standardmäßig Formatvorlagen zugeordnet, die Sie überschreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-151">SharePoint navigation controls have styles applied by default that you have to override.</span></span>
    
  
- <span data-ttu-id="6d8c6-152">Berücksichtigen Sie diese potenziellen Probleme beim Benennen von Dateien:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-152">Consider these potential issues about file naming:</span></span>
    
  - <span data-ttu-id="6d8c6-153">Wenn Sie über Index.html und Index.htm verfügen, haben diese Dateien dieselbe MASTER-Datei.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-153">If you have Index.html and Index.htm, those files will have the same .master file.</span></span>
    
  
  - <span data-ttu-id="6d8c6-p112">Wenn Sie über Design/Index.html und Design/SubDesign/Index.html verfügen, können diese Dateien in eigene, getrennte MASTER-Dateien konvertiert werden. Sie werden jedoch im Entwurfs-Manager in der Gestaltungsvorlagenliste als Index.html angezeigt. Um sie eindeutig zu machen, klicken Sie für jede Datei auf die Schaltfläche mit den Auslassungszeichen, um den vollständigen Pfad anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p112">If you have Design/Index.html and Design/SubDesign/Index.html, both of those files are available for conversion into their own, separate .master files, but they'll both show up as Index.html in the master page list in Design Manager. To disambiguate them, click or select the ellipsis button for each file to see the full path.</span></span>
    
  
- <span data-ttu-id="6d8c6-156">Wenn Sie ein JavaScript-Widget hinzufügen, vergewissern Sie sich, dass sich das Starttag **\<script\>** in einer eigenen Zeile befindet.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-156">If you're adding a JavaScript widget, make sure the **\<script\>** start tag is on its own line.</span></span>
    
```
  
<script>
(function( …

```

<span data-ttu-id="6d8c6-157">Geben Sie die Tags nicht in der gleichen Zeile ein (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-157">Do not put them on the same line, like this.</span></span>
    


```
  
<Script> (function( …
```

- <span data-ttu-id="6d8c6-158">Ein Verweis auf die JQuery-Bibliothek (ein externer Verweis) muss sich vor dem **\</head\>**-Tag befinden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-158">A reference to the JQuery library (an external reference) should go before the **\</head\>** tag.</span></span>
    
  

## <a name="convert-the-html-file-into-a-master-page"></a><span data-ttu-id="6d8c6-159">Konvertieren der HTML-Datei in eine Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="6d8c6-159">Convert the HTML file into a master page</span></span>
<span data-ttu-id="6d8c6-160"><a name="Convert"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-160"><a name="Convert"> </a></span></span>

<span data-ttu-id="6d8c6-p113">Bevor Sie eine HTML-Datei konvertieren, müssen Sie zunächst alle Ihre Entwurfsdateien samt Ihrer HTML-Datei hochladen. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p113">Before you convert an HTML file, you first have to upload all of your design files, including your HTML file. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    

### <a name="to-convert-the-html-file-into-a-master-file"></a><span data-ttu-id="6d8c6-163">So konvertieren Sie die HTML-Datei in eine Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="6d8c6-163">To convert the HTML file into a .master file</span></span>


1. <span data-ttu-id="6d8c6-164">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-164">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="6d8c6-165">Wählen Sie in der rechten oberen Ecke der Seite **Einstellungen** und dann **Entwurfs-Manager**.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-165">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="6d8c6-166">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-166">In Design Manager, in the left navigation pane, choose **Edit Master Pages**.</span></span>
    
  
4. <span data-ttu-id="6d8c6-167">Wählen Sie **Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage**.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-167">Choose **Convert an HTML file to a SharePoint master page**.</span></span>
    
  
5. <span data-ttu-id="6d8c6-168">Wählen Sie im Dialogfeld **Ein Objekt auswählen** die HTML-Datei aus, die Sie konvertieren möchten.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-168">In the **Select an Asset** dialog box, browse to and select the HTML file that you want to convert.</span></span>
    
    > <span data-ttu-id="6d8c6-169">**Hinweis:** Wenn Sie Ihre Entwurfsdateien hochladen, sollten Sie alle Dateien, die sich auf einen einzelnen Entwurf beziehen, in einem eigenen Ordner im Gestaltungsvorlagenkatalog aufbewahren.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-169">**Note:** When you upload your design files, you should keep all files that are related to a single design in their own folder in the Master Page Gallery.</span></span> <span data-ttu-id="6d8c6-170">Wenn Sie Ihren Entwurfordner auf das zugeordnete Netzlaufwerk kopieren, behält der Gestaltungsvorlagenkatalog die erstellte Ordnerstruktur bei.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-170">When you copy your design folder into the mapped network drive, the Master Page Gallery retains whatever folder structure you created.</span></span> 
6. <span data-ttu-id="6d8c6-171">Wählen Sie **Einfügen**.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-171">Choose **Insert**.</span></span>
    
    <span data-ttu-id="6d8c6-172">An dieser Stelle konvertiert SharePoint Ihre HTML-Datei in eine MASTER-Datei mit demselben Namen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-172">At this point, SharePoint converts your HTML file into a .master file with the same name.</span></span>
    
    <span data-ttu-id="6d8c6-173">Im Entwurfs-Manager wird Ihre HTML-Datei nun mit der Spalte Status mit einem von zwei möglichen Status angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-173">In Design Manager, your HTML file now appears with a Status column that shows one of two possible statuses:</span></span>
    
  - <span data-ttu-id="6d8c6-174">Fehler</span><span class="sxs-lookup"><span data-stu-id="6d8c6-174">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="6d8c6-175">**Konvertierung erfolgreich**</span><span class="sxs-lookup"><span data-stu-id="6d8c6-175">**Conversion successful**</span></span>
    
  
7. <span data-ttu-id="6d8c6-176">Öffnen Sie den Link in der Spalte Status, um eine Vorschau der Datei und etwaige Fehler oder Warnungen zur Gestaltungsvorlage anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-176">Follow the link in the Status column to preview the file and to view any errors or warnings about the master page.</span></span>
    
    <span data-ttu-id="6d8c6-p115">Die Vorschauseite zeigt eine aktuelle Vorschau auf Serverseite Ihrer Gestaltungsvorlage. Oben in der Vorschau werden etwaige Warnungen oder Fehler angezeigt, die Sie ggf. durch Bearbeiten der HTML-Datei in einem HTML-Editor beheben müssen. Fehler müssen korrigiert werden, damit die Gestaltungsvorlage in der Vorschau ordnungsgemäß angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p115">The preview page is a live server-side preview of your master page. The top of the preview displays any warnings or errors that you may have to resolve by editing the HTML file in an HTML editor. Errors must be fixed before the preview will display the master page correctly.</span></span>
    
    <span data-ttu-id="6d8c6-180">Weitere Informationen zum Beheben von Fehlern und Warnungen finden Sie unter  [Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-180">For more information about resolving errors and warnings, see  [How to: Resolve errors and warnings when previewing a page in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).</span></span>
    
    <span data-ttu-id="6d8c6-181">Weitere Informationen zur Vorschau der Gestaltungsvorlage mit unterschiedlichen Seiten finden Sie unter  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-181">For more information about previewing the master page with different pages, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
    
    <span data-ttu-id="6d8c6-182">Die Vorschauseite enthält außerdem einen Ausschnitte-Link in der oberen rechten Ecke.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-182">The preview page also contains a Snippets link in the upper-right corner.</span></span> <span data-ttu-id="6d8c6-183">Über diesen Link können Sie den Codeausschnittkatalog öffnen, mit dem Sie statische oder Modellsteuerelemente in Ihrem Entwurf durch dynamische SharePoint-Steuerelemente ersetzt können.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-183">This link opens the Snippet Gallery, where you can begin replacing static or mockup controls in your design with dynamic SharePoint controls.</span></span> <span data-ttu-id="6d8c6-184">Weitere Informationen finden Sie unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-184">For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
8. <span data-ttu-id="6d8c6-p117">Bearbeiten zum Korrigieren von Fehlern die HTML-Datei, die sich direkt auf dem Server befindet, mithilfe eines HTML-Editors, mit dem Sie die HTML-Datei auf dem zugeordneten Laufwerk öffnen und bearbeiten können. Bei jeder Speicherung der HTML-Datei werden Änderungen mit der zugeordneten MASTER-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p117">To fix any errors, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time you save the HTML file, any changes are synced to the associated .master file.</span></span>
    
  
9. <span data-ttu-id="6d8c6-187">Nachdem eine Vorschau der Gestaltungsvorlage angezeigt wurde, wird ein **\<div\>**-Tag Ihrer HTML-Datei hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-187">After your master page previews successfully, you will see a **\<div\>** tag that gets added to your HTML file.</span></span> <span data-ttu-id="6d8c6-188">Sie müssen möglicherweise bis zum Ende der Seite scrollen, um das **\<div\>**-Tag zu sehen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-188">You may have to scroll to the bottom of the page to see the **\<div\>** tag.</span></span>
    
    <span data-ttu-id="6d8c6-189">Dieses **\<div\>**-Tag ist im Hauptinhaltsblock vorhanden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-189">This **\<div\>** is the main content block.</span></span> <span data-ttu-id="6d8c6-190">Es befindet sich in einem Inhaltsplatzhalter **ContentPlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-190">It resides inside a content placeholder named **ContentPlaceHolderMain**.</span></span> <span data-ttu-id="6d8c6-191">Wenn ein Besucher zur Laufzeit Ihre Website durchsucht und eine Seite anfordert, wird dieser Platzhalter mit Inhalt aus einem Seitenlayout gefüllt, der die Inhalte in einem passenden Inhaltsbereich enthält.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-191">At run time, when a visitor browses your site and requests a page, this content placeholder gets filled with content from a page layout that contains content in a matching content region.</span></span> <span data-ttu-id="6d8c6-192">Sie sollten das **\<div\>**-Tag dort positionieren, wo Ihre Seitenlayouts in der Gestaltungsvorlage angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-192">You should position this **\<div\>** where you want your page layouts to appear on the master page.</span></span>
    
    <span data-ttu-id="6d8c6-p120">Wenn Ihre HTML-Datei statische oder Modellinhalte im Textkörper der Seite enthält, leiten Sie nun das Entfernen dieser statischen Inhalte aus der HTML-Gestaltungsvorlage ein, und Sie wenden diese Formate auf andere Elemente des SharePoint-Seitenmodells an, z. B. Seitenlayouts, Seitenfeld-Steuerelemente, Codeausschnitte und Anzeigevorlagen. Ein Beispiel finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p120">If your HTML file contains static or mockup content in the body of the page, now you begin the process of removing that static content from the HTML master page and applying those styles to other elements of the SharePoint page model, such as page layouts, page field controls, snippets, and display templates. For an example, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  

## <a name="understanding-the-html-file-after-conversion"></a><span data-ttu-id="6d8c6-195">Grundlegendes zur HTML-Datei nach der Konvertierung</span><span class="sxs-lookup"><span data-stu-id="6d8c6-195">Understanding the HTML file after conversion</span></span>
<span data-ttu-id="6d8c6-196"><a name="Understand"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-196"><a name="Understand"> </a></span></span>

<span data-ttu-id="6d8c6-p121">Wenn Sie eine HTML-Datei in eine Gestaltungsvorlage konvertieren, werden der HTML-Datei viele Markupzeilen hinzugefügt. Sie können einen Großteil dieses Markups getrost ignorieren, denn das meiste davon wird nicht im endgültigen Markup Ihrer Website enthalten sein, wenn Sie den Quellcode im Browser anzeigen. Doch dieses Markup ist wichtig für das Konvertieren Ihrer HTML-Datei in die MASTER-Datei, die SharePoint tatsächlich verwendet. Jedes Mal, wenn sie eine Änderung an Ihrer HTML-Datei speichern, ermöglicht dieses SharePoint-Markup, dass dieselbe Änderung im Hintergrund an der zugeordneten MASTER-Datei erfolgt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p121">When you convert an HTML file into a master page, many lines of markup get added to your HTML file. You can safely ignore most of this markup, and most of it will not appear in the final markup of your site when you view source in the browser, but this markup is critical for converting your HTML file into the .master file that SharePoint actually uses. Each time you save a change to your HTML file, this SharePoint markup makes it possible for that same change to be made to the associated .master file in the background.</span></span>
  
    
    
<span data-ttu-id="6d8c6-200">Das Markup, das hinzugefügt wird, enthält Tags vor und im **\<head\>**-Tag, Ausschnitte und Inhaltsplatzhalter.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-200">The markup that gets added includes tags before and in the **\<head\>** tag, snippets, and content placeholders.</span></span> <span data-ttu-id="6d8c6-201">Das meiste Markup befindet sich innerhalb von Kommentartags. Immer wenn Sie eine Änderung an der HTML-Datei speichern, entfernt der Konvertierungsprozess die Kommentare, um das enthaltene ASP.NET-Markup zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-201">Most of the markup is enclosed within comment tags: Whenever you save a change to the HTML file, the conversion process strips out the comments to use the ASP.NET markup within.</span></span>
  
    
    

### <a name="types-of-markup"></a><span data-ttu-id="6d8c6-202">Arten von Markup</span><span class="sxs-lookup"><span data-stu-id="6d8c6-202">Types of markup</span></span>

<span data-ttu-id="6d8c6-203">Es folgt eine Übersicht der Arten von Markup, die der HTML-Datei hinzugefügt werden:</span><span class="sxs-lookup"><span data-stu-id="6d8c6-203">The following is a breakdown of the types of markup that are added to the HTML file:</span></span>
  
    
    

- <span data-ttu-id="6d8c6-204">**Dokumenteigenschaften** Das **\<mso\>**-Tag enthält SharePoint-Metadaten, einschließlich Informationen zur Datei selbst und einiger Eigenschaften, die für die erfolgreiche Konvertierung in die MASTER-Datei benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-204">**Document properties** The **\<mso\>** tag contains SharePoint metadata, including information about the file itself and some properties needed for the successful conversion to the .master file.</span></span>
    
```HTML
  
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
```

- <span data-ttu-id="6d8c6-205">**Registrierung eines SharePoint-Namespace** Das **\<SPM\>**-Tag ("SharePoint-Markup") bietet eine Zeile zur Registrierung eines SharePoint-Namespace.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-205">**SharePoint namespace registration** The **\<SPM\>** tag ("SharePoint markup") provides a line registering a SharePoint namespace.</span></span>
    
```HTML
  
<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

- <span data-ttu-id="6d8c6-206">**Kommentare** Die Tags **\<CS\>** und **\<CE\>** ("Kommentaranfang" und "Kommentarende") werden während des Konvertierungsprozesses ignoriert.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-206">**Comments** The **\<CS\>** and **\<CE\>** ("Comment start" and "comment end") tags are ignored during the conversion process.</span></span> <span data-ttu-id="6d8c6-207">Diese Tags dienen zur Analyse der Markupzeilen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-207">These tags are to help you parse the lines of markup.</span></span>
    
```HTML
  
<!--CS: Start Page Head Contents Snippet-->
…
<!--CE: End Page Head Contents Snippet-->

  <!--CS: Start Ribbon Snippet-->
…
<!--CE: End Ribbon Snippet-->

<!--CS: Start PlaceHolderMain Snippet-->
…
<!--CE: End PlaceHolderMain Snippet-->
```

- <span data-ttu-id="6d8c6-208">**Ausschnitte** Die **\<MS\>**- und **\<ME\>**-Tags ("Markup-Anfang" und "Markup-Ende") kennzeichnen den Anfang und das Ende eines SharePoint-Steuerelements oder -Ausschnitts.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-208">**Snippets** The **\<MS\>** and **\<ME\>** ("markup start" and "markup end") tags denote the beginning and end of a SharePoint control or a snippet.</span></span> <span data-ttu-id="6d8c6-209">Ein Ausschnitt ist ein SharePoint-Steuerelement, mit dem Sie SharePoint-Funktionalität zu Ihrer Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-209">A snippet is a SharePoint control that adds SharePoint functionality to your page.</span></span> <span data-ttu-id="6d8c6-210">Mit dem Codeausschnittkatalog können Sie selbst Codeausschnitte hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-210">You can add snippets yourself by using the Snippet Gallery.</span></span> <span data-ttu-id="6d8c6-211">Weitere Informationen finden Sie unter [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c6-211">For more information, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
```HTML
  
<!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
```

- <span data-ttu-id="6d8c6-212">**Anzeigen einer Blockvorschau** Die **\<PS\>**- und **\<PE\>**-Tags ("Vorschau-Anfang" und "Vorschau-Ende") umgeben den Bereich eines HTML-Codes, den Sie nicht bearbeiten sollten, da sich dieser Abschnitt nur auf die Entwurfszeit-Vorschau auswirkt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-212">**Preview blocks** The **\<PS\>** and **\<PE\>** ("Preview start" and "preview end") tags surround a section of HTML code that you shouldn't edit because this section affects only the design-time preview.</span></span> <span data-ttu-id="6d8c6-213">Diese Vorschaubereiche sind eine Momentaufnahme der SharePoint-Steuerelemente, die der Abschnitt einfügt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-213">These preview sections are a snapshot in time of the SharePoint control that snippet is inserting.</span></span> <span data-ttu-id="6d8c6-214">Eine Vorschau ermöglicht es Ihnen, in einem clientseitigen HTML-Editor effektiver an der HTML-Datei zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-214">A preview makes it possible for you to work more meaningfully on the HTML file in a client-side HTML editor.</span></span> <span data-ttu-id="6d8c6-215">Wenn Sie jedoch den Inhalt oder das Format in dieser Vorschau ändern, hat dies keine dauerhaften Auswirkung auf die .master-Datei, die SharePoint letztendlich verwendet.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-215">But, changing the content or styling within that preview has no lasting effect on the .master file, which is what SharePoint is ultimately using.</span></span> <span data-ttu-id="6d8c6-216">Um einen Ausschnitt zu formatieren, müssen Sie die SharePoint-Formatvorlagen ermitteln und mit Ihren eigenen benutzerdefinierten CSS-Formatvorlagen überschreiben.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-216">To style a snippet, you have to identify and override the SharePoint styles with your own custom CSS.</span></span>
    
```HTML
  
<!--PS: Start of READ-ONLY PREVIEW (do not modify) -->
<div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div>
<!--PE: End of READ-ONLY PREVIEW -->
```

- <span data-ttu-id="6d8c6-p126">**SharePoint-IDs** Zwei der Codeausschnitte, die Ihrer HTML-Datei während der Konvertierung hinzugefügt werden (der Codeausschnitt "Seitenkopfinhalte" und das SharePoint-Menüband), haben eine zugeordnete SharePoint-ID bzw. SID (00 bzw. 02). Diese IDs ermöglichen das Kürzen der Codeausschnitte und vereinfachen das Lesen des HTML-Codes auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p126">**SharePoint IDs** Two of the snippets added to your HTML file during the conversion (the Page Head Contents snippet and the SharePoint Ribbon) have an associated SharePoint ID, or SID (00 and 02, respectively). These IDs make it possible to shorten the snippets and make the HTML in the page easier to read.</span></span>
    
```HTML
  
<!--SID:00 -->

<!--SID:02 {Ribbon}-->
```


### <a name="added-snippets"></a><span data-ttu-id="6d8c6-219">Hinzugefügte Codeausschnitte</span><span class="sxs-lookup"><span data-stu-id="6d8c6-219">Added snippets</span></span>

<span data-ttu-id="6d8c6-p127">Wichtig ist es, die beiden Codeausschnitte zu kennen, die Ihrer HTML-Datei hinzugefügt werden. Diese Codeausschnitte werden während der Konvertierung automatisch hinzugefügt. Sie stehen jedoch nicht zum Hinzufügen über den Codeausschnittkatalog zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-p127">It's important to know about two of the snippets that are added to your HTML file. These snippets are added automatically during the conversion, but they're not available for you to add from the Snippet Gallery.</span></span>
  
    
    

- <span data-ttu-id="6d8c6-222">**Das Menüband** Damit Inhaltsautoren Seiten und Inhalte auf Ihrer SharePoint-Website erstellen können, benötigt Ihre Gestaltungsvorlage ein Menüband und das neue "Suite Navigationssteuerelement" von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-222">**The Ribbon** For content authors to be able to create pages and author content on your SharePoint site, your master page needs the ribbon and the "suite navigation" that is new to SharePoint.</span></span> <span data-ttu-id="6d8c6-223">Das Menüband ist in einem Codeausschnitt mit Einschränkung aus Sicherheitsgründen enthalten, sodass, wenn ein Benutzer Ihre Website durchstöbert, das Menüband nur authentifizierten Benutzern und nicht anonymen Benutzern angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-223">The ribbon is contained in a security-trimming snippet, so that when a visitor browses your site, the ribbon is displayed only to authenticated users, not anonymous users.</span></span> <span data-ttu-id="6d8c6-224">Sie können das Menüband an eine andere Position auf der Seite verschieben oder es durch Überschreiben der CSS-Standardklassen formatieren. Jedoch wird das Verschieben oder Neuanordnen der Komponenten (z. B. des Menüs Websiteaktionen), die sich auf dem Menüband befinden, nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-224">You can move the ribbon to a different position on the page or style it by overriding the default CSS classes, but we do not recommend moving or reordering the components (such as the Site Actions menu) that are contained inside the ribbon.</span></span>
    
```HTML
  
<!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
<!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
<!--ME:</wssucw:Welcome>-->
<!--ME:</SharePoint:SPSecurityTrimmedControl>-->
```

- <span data-ttu-id="6d8c6-225">**ContentPlaceHolderMain** Unter dem **\<div id="s4-bodyContainer"\>**-Tag und vor dem schließenden **\</body\>**-Tag fügt der Konvertierungsprozess einen Inhaltsplatzhalter mit dem Namen **PlaceHolderMain** ein.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-225">**ContentPlaceHolderMain** At the bottom of the **\<div id="s4-bodyContainer"\>** tag, before the closing **\</body\>** tag, the conversion process inserts a content placeholder named **PlaceHolderMain**.</span></span> <span data-ttu-id="6d8c6-226">In diesem Codeausschnitt befindet sich das schwarz umrandete, gelbe **\<div\>**, das in der Entwurfsansicht des HTML-Editors oder in der serverseitigen Vorschau im Entwurfs-Manager angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-226">Inside this snippet is the black-bordered, yellow **\<div\>** that appears in the design view of your HTML editor, or in the server-side preview in Design Manager.</span></span>
    
    <span data-ttu-id="6d8c6-227">Dieses **\<div\>** steht für den Bereich, in den der von Ihrem Seitenlayout und Ihren Seiten definierte Inhalt gelangt.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-227">This **\<div\>** represents the area where the content specified by your page layouts and pages will go.</span></span> <span data-ttu-id="6d8c6-228">Sie müssen den Codeausschnitt **PlaceHolderMain** an die Stellen in Ihrer Gestaltungsvorlage verschieben, die durch Ihre Seitenlayouts gefüllt werden, d. h. in den Bereich Ihres Websiteentwurfs, der auf allen Seiten Ihrer Website nicht identisch ist.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-228">You should move the **PlaceHolderMain** snippet to the place within your master page that will be filled by your page layouts—the area of your site design that isn't the same across all pages of your site.</span></span>
    


```HTML
  
<!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
```


## <a name="reference-examples-of-sharepoint-markup-added-to-the-html-file"></a><span data-ttu-id="6d8c6-229">Referenz: Beispiele von zur HTML-Datei hinzugefügtem SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="6d8c6-229">Reference: Examples of SharePoint markup added to the HTML file</span></span>
<span data-ttu-id="6d8c6-230"><a name="Reference"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-230"><a name="Reference"> </a></span></span>

<span data-ttu-id="6d8c6-231">Es folgt ein Beispiel des Markups, das einer HTML-Datei hinzugefügt wird, nachdem sie in eine Gestaltungsvorlage konvertiert wurde.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-231">The following is an example of markup added to an HTML file after it is converted to a master page.</span></span>
  
    
    

### <a name="markup-added-to-the-head-tag"></a><span data-ttu-id="6d8c6-232">Dem \<head\>-Tag hinzugefügtes Markup</span><span class="sxs-lookup"><span data-stu-id="6d8c6-232">Markup added to the \<head\> tag</span></span>


```HTML

<head>
        <meta http-equiv="X-UA-Compatible" content="IE=10" />
        <!--CS: Start Page Head Contents Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SID:00 -->
        <meta name="GENERATOR" content="Microsoft SharePoint" />
        <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
        <meta http-equiv="Expires" content="0" />
        <!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--CE: End Page Head Contents Snippet-->
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <!--DC:Business Solutions-->
        <link rel="stylesheet" href="css/style.css" type="text/css" charset="utf-8" />
        <!--[if lte IE 7]>
  <link rel="stylesheet" href="css/ie.css" type="text/css" charset="utf-8"/> 
 <![endif]-->
        <!--[if gte mso 9]><xml>
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
</xml><![endif]-->
    </head>

```


### <a name="markup-added-after-the-start-body-tag"></a><span data-ttu-id="6d8c6-233">Hinter dem \<body\>-Anfangstag hinzugefügtes Markup</span><span class="sxs-lookup"><span data-stu-id="6d8c6-233">Markup added after the start \<body\> tag</span></span>


#### <a name="ribbon-snippet"></a><span data-ttu-id="6d8c6-234">Codeausschnitt des Menübands</span><span class="sxs-lookup"><span data-stu-id="6d8c6-234">Ribbon snippet</span></span>


```HTML

<!--CS: Start Ribbon Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="wssucw" TagName="Welcome" Src="~/_controltemplates/15/Welcome.ascx"%>-->
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" HideFromSearchCrawler="true" EmitDiv="true">-->
            <div id="TurnOnAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOnAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(true);UpdateAccessibilityUI();document.getElementById('linkTurnOffAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnonaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
            <div id="TurnOffAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOffAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(false);UpdateAccessibilityUI();document.getElementById('linkTurnOnAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnoffaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <div id="ms-designer-ribbon">
            <!--SID:02 {Ribbon}-->
            <!--PS: Start of READ-ONLY PREVIEW (do not modify) --><div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div><!--PE: End of READ-ONLY PREVIEW -->
        </div>
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
            <!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
            <!--ME:</wssucw:Welcome>-->
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <!--CE: End Ribbon Snippet-->

```


#### <a name="two-sharepoint-div-tags"></a><span data-ttu-id="6d8c6-235">Zwei SharePoint \<div\>-Tags</span><span class="sxs-lookup"><span data-stu-id="6d8c6-235">Two SharePoint \<div\> tags</span></span>


```HTML

<div id="s4-workspace">
            <div id="s4-bodyContainer">

```


### <a name="markup-added-before-the-closing-body-tag-and-two-closing-div-tags"></a><span data-ttu-id="6d8c6-236">Vor dem schließenden \</body\>-Tag und zwei schließenden \</div\>-Tags hinzugefügtes Markup</span><span class="sxs-lookup"><span data-stu-id="6d8c6-236">Markup added before the closing \</body\> tag and two closing \</div\> tags</span></span>


```HTML

<div data-name="ContentPlaceHolderMain">
                    <!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
                </div>

```


## <a name="additional-resources"></a><span data-ttu-id="6d8c6-237">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6d8c6-237">Additional resources</span></span>
<span data-ttu-id="6d8c6-238"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="6d8c6-238"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="6d8c6-239">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d8c6-239">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d8c6-240">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d8c6-240">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d8c6-241">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="6d8c6-241">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

