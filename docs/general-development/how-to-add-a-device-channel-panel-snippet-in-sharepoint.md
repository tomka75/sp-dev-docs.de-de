---
title: "Hinzufügen eines Gerätekanalbereich-Codeausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 612780a8-6267-49f6-a32d-33600bb5f6b4
ms.openlocfilehash: b5a208a87ee7b8af55fa6c6c1c96a0ae11df5de8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-device-channel-panel-snippet-in-sharepoint"></a><span data-ttu-id="92849-102">Hinzufügen eines Gerätekanalbereich-Codeausschnitts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92849-102">How to: Add a Device Channel Panel snippet in SharePoint</span></span>

<span data-ttu-id="92849-p101">Ein Gerätekanalbereich ist ein Codeausschnitt, den Sie einer Gestaltungsvorlage oder einem Seitenlayout hinzufügen können, um zu steuern, welche Inhalte für jeden von Ihnen erstellten Kanal gerendert werden. Der Hauptzweck eines Gerätekanalbereichs ist die selektive Anzeige verschiedener Seitenfelder in verschiedenen Kanälen eines einzigen Seitenlayouts.</span><span class="sxs-lookup"><span data-stu-id="92849-p101">A Device Channel Panel is a snippet that you can add to a master page or page layout to control what content is rendered for each channel that you create. The primary purpose of a Device Channel Panel is to selectively display different page fields on different channels from a single page layout.</span></span>

## <a name="introduction-to-the-device-channel-panel-snippet"></a><span data-ttu-id="92849-105">Einführung in den Codeausschnitt Gerät Channel-Systemsteuerung</span><span class="sxs-lookup"><span data-stu-id="92849-105">Introduction to the Device Channel Panel snippet</span></span>
<span data-ttu-id="92849-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="92849-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="92849-p102">Ein Gerät Channel Bereich ist ein Steuerelement, das Sie zu einer Gestaltungsvorlage oder Seitenlayout zu steuern, welche Inhalte in den einzelnen Kanälen gerendert wird, die Sie erstellen hinzufügen können. Ein Gerät Channel Bereich ist ein Container, der einen oder mehrere Kanäle angibt; Wenn eine oder mehrere dieser Kanäle aktiviert sind, wenn die Seite gerendert wird, werden alle Inhalte des Bereichs Channel Gerät auch gerendert. Ein Gerät Channel-Systemsteuerung kann nahezu alle Arten von Inhalten, einschließlich einer Verknüpfung zu einer CSS-Datei oder eine JS-Datei enthalten. Es ist eine einfache Möglichkeit, bestimmte Inhalte für bestimmte Kanäle enthalten.</span><span class="sxs-lookup"><span data-stu-id="92849-p102">A Device Channel Panel is a control that you can add to a master page or page layout to control what content is rendered in each channel that you create. A Device Channel Panel is a container that specifies one or more channels; if one or more of those channels are active when the page is rendered, all of the contents of the Device Channel Panel are also rendered. A Device Channel Panel can include almost any type of content, including a link to a CSS file or a .js file. It is an easy way to include specific content for specific channels.</span></span>
  
    
    
<span data-ttu-id="92849-p103">Möglicherweise ist das am häufigsten verwendete Szenario für die Verwendung von Gerätekanalbereiche Teile der ein Seitenlayout für bestimmte Kanäle einschließen. Beispielsweise können Sie ein Seitenlayout mit separaten Textfelder für eine lange Begrüßung und eine kurze Begrüßung verfügen. Indem Sie die Seitenfelder in Gerätekanalbereiche platzieren, können Sie die kurze Begrüßung nur für Telefone und die lange Grußformel nur auf dem Desktop anzeigen. Der Inhalt eines Bereichs Channel Gerät wird nicht angezeigt, auf Kanäle nicht enthalten - tatsächlich der Inhalt wird nicht wiedergegeben, die verhindern, dass Bytes Wechsel zu über das Netzwerk. Aus diesem Grund ist mit Gerätekanalbereiche eine bessere Möglichkeit zum Anzeigen von Inhalten auf bestimmte Kanäle als eine CSS-Klasse mit  `Display:None` , da Gerätekanalbereiche Hilfe, um die Seite Gewichtung für einen bestimmten Kanal zu verringern.</span><span class="sxs-lookup"><span data-stu-id="92849-p103">Perhaps the most common scenario for using Device Channel Panels is to selectively include parts of a page layout for specific channels. For example, you may have a page layout with separate text fields for a long greeting and a short greeting. By placing the page fields inside Device Channel Panels, you can display the short greeting only to phones and the long greeting only to the desktop. The content of a Device Channel Panel is not displayed on non-included channels—in fact, the content is not rendered at all, which prevents bytes from going across the wire. For this reason, using Device Channel Panels is a better way to display content on specific channels than using a CSS class with  `Display:None` because Device Channel Panels help to reduce the page weight for a specific channel.</span></span>
  
    
    
<span data-ttu-id="92849-p104">Sie können auch Gerätekanalbereiche auf Gestaltungsvorlagen. Wenn Sie eine Gestaltungsvorlage, die zwei unterschiedliche Geräte (oder zwei verschiedenen Browsern) bewältigen kann mit nur minimale Änderungen verfügen, können Sie auf den Inhalt auf der Masterseite enthalten, die entweder dieser Geräte spezifisch sind beispielsweise Gerätekanalbereiche verwenden.</span><span class="sxs-lookup"><span data-stu-id="92849-p104">You can also use Device Channel Panels on master pages. For example, if you have a master page that can accommodate two different devices (or two different browsers) with only minimal changes, you can use Device Channel Panels to hold the content on the master page that is specific to either of those devices.</span></span>
  
    
    
<span data-ttu-id="92849-118">Es gibt zwei Einschränkungen der Kanal mithilfe eines Geräts:</span><span class="sxs-lookup"><span data-stu-id="92849-118">There are two limitations to using a Device Channel Panel:</span></span>
  
    
    

- <span data-ttu-id="92849-p105">**Anzeigevorlagen** Da Anzeigevorlagen auf dem Client gerendert werden und Gerätekanalbereiche auf dem Server ausgeführt werden, nicht Gerät Channel Bereichs innerhalb einer Anzeigevorlage verwendet werden. Verwenden Sie stattdessen Sie sollten zwei verschiedene Inhaltssuche-Webparts innerhalb der Gerätekanalbereiche auf das Seitenlayout, oder verwenden Sie die JavaScript-Variable auf das Verhalten auslösen innerhalb der Anzeigevorlage selbst gewünschten.</span><span class="sxs-lookup"><span data-stu-id="92849-p105">**Display templates** Because display templates are rendered on the client side and Device Channel Panels run on the server side, you cannot use a Device Channel Panel within a display template. Instead, you should use two different Content Search Web Parts within Device Channel Panels on your page layout, or use the JavaScript variable to trigger the behavior you want within the display template itself.</span></span>
    
  
- <span data-ttu-id="92849-p106">**Webpartzonen** Eine Webpartzone in einem Gerät Channel Bereich kann nicht eingefügt werden. Wenn Sie zulassen Autoren Webparts zu einer Seite hinzufügen möchten, und wenn Sie nicht die Seite Gewichtung für mobile Geräte besorgt sind, können Sie ein Seitenfeld Rich-Text-Editor zu einem Gerät Channel-Element hinzufügen, und weisen Sie Autoren Webparts hinzufügen vorhanden. Sie können Webparts direkt zu einem Gerät Channel-Element (ohne eine Webpartzone) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="92849-p106">**Web Part zones** You cannot insert a Web Part zone inside a Device Channel Panel. If you want to allow authors to add Web Parts to a page, and if you are not concerned about the page weight for mobile devices, you can add a Rich Text Editor page field to a Device Channel Panel, and then instruct authors to add Web Parts there. You can add Web Parts directly to a Device Channel Panel (without a Web Part zone).</span></span>
    
  

## <a name="inserting-a-device-channel-panel-snippet"></a><span data-ttu-id="92849-124">Einen Gerät Channel Systemsteuerung Ausschnitt einfügen</span><span class="sxs-lookup"><span data-stu-id="92849-124">Inserting a Device Channel Panel snippet</span></span>
<span data-ttu-id="92849-125"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="92849-125"><a name="InsertSnippet"> </a></span></span>

<span data-ttu-id="92849-p107">Wie alle Ausschnitte fügen Sie einen Gerät Channel Systemsteuerung Ausschnitt aus Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.</span><span class="sxs-lookup"><span data-stu-id="92849-p107">Like all snippets, you add a Device Channel Panel snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-device-channel-panel-snippet"></a><span data-ttu-id="92849-128">So fügen Sie ein Gerät Channel Systemsteuerung Ausschnitt ein</span><span class="sxs-lookup"><span data-stu-id="92849-128">To insert a Device Channel Panel snippet</span></span>


1. <span data-ttu-id="92849-129">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="92849-129">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="92849-130">Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="92849-130">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="92849-131">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="92849-131">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="92849-132">Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="92849-132">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="92849-133">Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.</span><span class="sxs-lookup"><span data-stu-id="92849-133">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="92849-134">Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** **Gerät Channel Systemsteuerung** aus.</span><span class="sxs-lookup"><span data-stu-id="92849-134">On the ribbon, on the **Design** tab, choose **Device Channel Panel**.</span></span>
    
  
7. <span data-ttu-id="92849-135">Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="92849-135">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="92849-p108">Im Abschnitt mit dem Namen **Wichtig** enthält die Eigenschaften, die-Taste, um die Funktionsweise dieser bestimmten Ausschnitts sind. Für ein Gerät Channel-Bereich ist die **IncludedChannels**-Eigenschaft die wichtigste. Geben Sie für diese Eigenschaft den Alias des einzelnen Gerätekanal, die Sie den Inhalt im Kanal dieses Gerät anzeigen möchten. Wenn Sie mehr als einen Alias eingeben, trennen Sie die einzelnen durch ein Komma.</span><span class="sxs-lookup"><span data-stu-id="92849-p108">The section named **Important** contains the properties that are key to how this particular snippet works. For a Device Channel Panel, the **IncludedChannels** property is the most important. For this property, enter the alias of each Device Channel that you want to display the content contained in this Device Channel Panel. If you enter more than one alias, separate each with a comma.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="92849-140">Wenn Sie den Alias eines Kanals in der Liste „Gerätekanäle“ bearbeiten, müssen Sie den Alias manuell suchen und alle Vorkommen in Ihren Designdateien aktualisieren. Zudem müssen Sie die **IncludedChannels**-Eigenschaft für jeden Gerätekanalbereich aktualisieren, der den Alias verwendet.</span><span class="sxs-lookup"><span data-stu-id="92849-140">**Note:** If you edit the alias of a channel in the Device Channels list, you must manually find and update that alias wherever it appears in your design files, including updating the IncludedChannels property for every Device Channel Panel that uses that alias</span></span>

8. <span data-ttu-id="92849-p109">Nachdem Sie alle anderen Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Den HTML-Codeausschnitt auf der linken Seite der Seite aktualisiert, damit das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können immer auf alle Eigenschaften auf die Standardeinstellungen zurück **Zurücksetzen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="92849-p109">After you configure any other properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="92849-144">Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.</span><span class="sxs-lookup"><span data-stu-id="92849-144">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="92849-145">Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="92849-145">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
    <span data-ttu-id="92849-146">Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="92849-146">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="92849-147">Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="92849-147">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="92849-148">Wenn Sie den Codeausschnitt, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**einfügen.</span><span class="sxs-lookup"><span data-stu-id="92849-148">If you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="92849-149">Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="92849-149">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
    <span data-ttu-id="92849-150">In der Regel, wenn Sie ein Gerät Channel-Systemsteuerung einem Seitenlayout hinzufügen, ersetzen Sie die **<div>** durch Kopieren Seitenfelder innerhalb des Bereichs.</span><span class="sxs-lookup"><span data-stu-id="92849-150">Typically, if you're adding a Device Channel Panel to a page layout, you replace the **<div>** by copying page fields inside the panel.</span></span>
    
  
13. <span data-ttu-id="92849-151">Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass das Gerät Channel wird angezeigt, wie erwartet.</span><span class="sxs-lookup"><span data-stu-id="92849-151">Save the page, and then refresh the server-side preview in Design Manager to make sure the Device Channel Panel appears as expected.</span></span>
    
    <span data-ttu-id="92849-p110">Um eine Vorschau die Systemsteuerung auf unterschiedliche Kanäle anzeigen, können Sie auf die URL Abfragezeichenfolgen-Parameter hinzufügen. Beispielsweise können Sie auf die URL einer beliebigen Seite in der serverseitigen Vorschau der Abfrage Zeichenfolge variabler  `"DeviceChannel=YourChannelAlias"` anfügen.</span><span class="sxs-lookup"><span data-stu-id="92849-p110">To preview the panel on different channels, you can add query string parameters to the URL. For example, you can append the query string variable  `"DeviceChannel=YourChannelAlias"` to the URL of any page in the server-side preview.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="92849-154">Grundlegendes zum Codeausschnittmarkup</span><span class="sxs-lookup"><span data-stu-id="92849-154">Understanding the snippet markup</span></span>
<span data-ttu-id="92849-155"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="92849-155"><a name="UnderstandMarkup"> </a></span></span>

<span data-ttu-id="92849-p111">Die beiden wichtigsten Teile eines Ausschnitts Gerät Channel Systemsteuerung sind die **IncludedChannels** -Eigenschaft und die **<div>**, in dem `class="DefaultContentBlock"`. Standardmäßig ist die **IncludedChannels** -Eigenschaft leer. Geben Sie im Abschnitt **wichtige** des Eigenschaftenrasters Aliase, durch Kommas getrennt, der die Gerätekanäle, die Sie den Inhalt in diesem Bereich anzeigen möchten.</span><span class="sxs-lookup"><span data-stu-id="92849-p111">The two most important parts of a Device Channel Panel snippet are the **IncludedChannels** property and the **<div>** where `class="DefaultContentBlock"`. By default, the **IncludedChannels** property is empty. In the **Important** section of the property grid, you should enter the aliases, separated by commas, of the device channels that you want to display the content in this panel.</span></span>
  
> [!NOTE]
> <span data-ttu-id="92849-159">Wenn Sie einen Alias in der Liste „Gerätekanäle“ ändern, müssen Sie alle Vorkommen des Alias im Markup ändern, einschließlich in der **IncludedChannels**-Eigenschaft für jeden Gerätekanalbereich, der den Alias verwendet.</span><span class="sxs-lookup"><span data-stu-id="92849-159">**Note:** If you change an alias in the Device Channels list, you must also change that alias wherever it appears in your markup, including in the IncludedChannels property for every Device Channel Panel that uses that alias.</span></span>
  
    
    

<span data-ttu-id="92849-p112">Die **<div>**, in dem `class="DefaultContentBlock"` ersetzt werden soll, mit dem jeweils spezifischen Inhalt, anzuzeigende für Kanäle enthalten. Ein Gerät Channel-Systemsteuerung kann nahezu alle Arten von Inhalten, einschließlich einer Verknüpfung zu einer CSS-Datei oder eine JS-Datei enthalten. Das häufigste Szenario für die Verwendung von Gerätekanalbereiche ist bestimmte Seitenfelder in einem Seitenlayout für bestimmte Kanäle eingeschlossen. In diesem Fall kopieren Sie das Position der **<div>** innerhalb des Bereichs des Geräts Channel Feld Seitenmarkup.</span><span class="sxs-lookup"><span data-stu-id="92849-p112">The **<div>** where `class="DefaultContentBlock"` should be replaced with whatever specific content you want to display for the included channels. A Device Channel Panel can include almost any type of content, including a link to a CSS file or a .js file. The most common scenario for using Device Channel Panels is to include specific page fields from a page layout for specific channels. In this case, you copy the page field markup where the **<div>** is positioned inside the Device Channel Panel.</span></span>
  
    
    



```HTML

<div data-name="DeviceChannelPanel">
    <!--CS: Start Device Channel Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:DeviceChannelPanel runat="server" IncludedChannels="MyPhoneChannel, MyTabletChannel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
       <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Device Channel Panel Properties.    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:DeviceChannelPanel>-->
    <!--CE: End Device Channel Panel Snippet-->
</div>

```


## <a name="see-also"></a><span data-ttu-id="92849-164">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="92849-164">See also</span></span>
<span data-ttu-id="92849-165"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="92849-165"><a name="AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="92849-166">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="92849-166">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="92849-167">SharePoint-Design-Manager-Gerätekanäle</span><span class="sxs-lookup"><span data-stu-id="92849-167">SharePoint Design Manager device channels</span></span>](sharepoint-design-manager-device-channels.md)
    
  
-  [<span data-ttu-id="92849-168">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="92849-168">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="92849-169">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="92849-169">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

