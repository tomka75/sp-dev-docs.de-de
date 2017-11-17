---
title: "Vorgehensweise Hinzufügen eines Webpart-Zonenausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7583b217-200c-4569-8f88-fe975c8ebd72
ms.openlocfilehash: 5085f1a8fa2a79e78cc8c337bab0e03fe924f65d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-add-a-web-part-zone-snippet-in-sharepoint"></a><span data-ttu-id="03edb-102">Vorgehensweise: Hinzufügen eines Webpart-Zonenausschnitts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="03edb-102">How to: Add a Web Part zone snippet in SharePoint</span></span>
<span data-ttu-id="03edb-103">Eine Webpartzone ist ein Ausschnitt, den Sie einem Seitenlayout hinzufügen können, damit Inhaltsautoren Webparts in dieser Zone hinzufügen, bearbeiten und löschen können.</span><span class="sxs-lookup"><span data-stu-id="03edb-103">A Web Part zone is a snippet that you can add to a page layout so that content authors can add, edit, or delete Web Parts in that zone.</span></span>
## <a name="introduction-to-the-web-part-zone-snippet"></a><span data-ttu-id="03edb-104">Einführung in den Codeausschnitt "Webpartzone"</span><span class="sxs-lookup"><span data-stu-id="03edb-104">Introduction to the Web Part zone snippet</span></span>
<span data-ttu-id="03edb-105"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="03edb-105"></span></span>

<span data-ttu-id="03edb-p101">Ein Webpart ist ein Serversteuerelement, das eine bestimmte SharePoint-Funktionalität bietet. Eine Webpartzone ist ein Container zum Bestimmen des Layouts, Verhaltens und anderer Eigenschaften der in dieser Zone enthaltenen Webparts. Eine Webpartzone kann beispielsweise angeben, ob die Webparts in der Zone:</span><span class="sxs-lookup"><span data-stu-id="03edb-p101">A Web Part is a server control that provides a specific piece of SharePoint functionality, and a Web Part zone is a container that determines the layout, behavior, and other properties of the Web Parts contained in that zone. For example, a Web Part zone can specify whether the Web Parts in the zone:</span></span>
  
    
    

- <span data-ttu-id="03edb-108">mit einem horizontalen oder vertikalen Layout angeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="03edb-108">Are arranged in a horizontal or vertical layout.</span></span> 
    
  
- <span data-ttu-id="03edb-109">gemeinsame Benutzeroberflächenelemente wie Titelleiste oder Rand aufweisen.</span><span class="sxs-lookup"><span data-stu-id="03edb-109">Display common user interface (UI) elements such as a title bar or border.</span></span>
    
  
- <span data-ttu-id="03edb-110">von Inhaltsautoren angepasst werden können, wenn diese eine Seite im Browser bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="03edb-110">Can be customized by content authors when they edit a page in the browser.</span></span>
    
  
- <span data-ttu-id="03edb-111">von Websitebesuchern individuell angepasst werden können, die bei der Anzeige einer Seite im Browser eine persönliche Ansicht erstellen können.</span><span class="sxs-lookup"><span data-stu-id="03edb-111">Can be personalized by site visitors who create a personal view of a Web Part when they view a page in the browser.</span></span>
    
  
<span data-ttu-id="03edb-p102">Auf einer Veröffentlichungswebsite können Inhaltsautoren mit den erforderlichen Berechtigungen Seiten erstellen oder in der Bibliothek Seiten enthaltene Seiten bearbeiten. Als Designer können Sie einem Seitenlayout eine Webpartzone hinzufügen. Wenn ein Inhaltsautor eine Seite basierend auf diesem Seitenlayout erstellt oder bearbeitet, kann er Webparts in dieser Zone hinzufügen, bearbeiten oder löschen. Sie können beispielsweise einem Seitenlayout eine Webpartzone hinzufügen, damit Inhaltsautoren folgende Aufgaben ausführen können:</span><span class="sxs-lookup"><span data-stu-id="03edb-p102">In a publishing site, content authors with the necessary permissions can create or edit pages that reside in the Pages library. As a designer, you can add a Web Part zone to a page layout. When a content author creates or edits a page based on that page layout, the author can add, edit, or delete Web Parts in that zone. For example, you may want to add a Web Part zone to a page layout so that content authors can:</span></span>
  
    
    

- <span data-ttu-id="03edb-p103">Anzeigen der Ergebnisse einer Suchabfrage mithilfe eines Inhaltssuche-Webparts. Autoren können die Suchabfrage aktualisieren oder ändern, wenn sich ein suchgesteuertes Webpart in einer Webpartzone befindet.</span><span class="sxs-lookup"><span data-stu-id="03edb-p103">Display the results of a search query by using a Content Search Web Part. Authors can update or modify the search query when a search-driven Web Part resides inside a Web Part zone.</span></span>
    
  
- <span data-ttu-id="03edb-118">Einbetten von Video- oder Audioclips in eine Webseite mithilfe eines Medienwebparts.</span><span class="sxs-lookup"><span data-stu-id="03edb-118">Embed video or audio clips in a webpage by using a Media Web Part.</span></span>
    
  
- <span data-ttu-id="03edb-119">Erstellen von Listen mit Hyperlinks, die mit einem Hyperlinkübersicht-Webpart mühelos bearbeitet, gruppiert oder neu angeordnet werden können.</span><span class="sxs-lookup"><span data-stu-id="03edb-119">Create lists of hyperlinks that are easily edited, grouped, or reordered by using a Summary Link Web Part.</span></span>
    
  
- <span data-ttu-id="03edb-120">Erstellen einer Siteübersicht mit allen Seiten einer Website, die automatisch aktualisiert wird, wenn eine Seite mit einem Inhaltsverzeichnis-Webpart hinzugefügt, gelöscht, umbenannt oder entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="03edb-120">Create a site map that lists all pages in a site and that is automatically updated whenever a page is added, deleted, renamed, or moved by using a Table of Contents Web Part.</span></span>
    
  

### <a name="when-to-use-web-part-zones"></a><span data-ttu-id="03edb-121">Verwendung von Webpartzonen</span><span class="sxs-lookup"><span data-stu-id="03edb-121">When to use Web Part zones</span></span>

<span data-ttu-id="03edb-p104">Wenn ein Seitenlayout eine oder mehrere Webpartzonen enthält, stehen diese auf allen Seiten zur Verfügung, die dieses Layout verwendet, sodass Autoren Webparts auf diesen Seiten einfügen können. Wenn Sie Autoren das Einfügen von Webparts auf Seiten ermöglichen, verringern sich Ihre Steuerungsmöglichkeiten der Benutzeroberfläche der Website. Ein Autor kann beispielsweise ein Inhaltsverzeichnis-Webpart einer Seite hinzufügen, das Teile Ihrer Website verfügbar macht, die Sie Benutzern auf der aktuellen Seite nicht zur Verfügung stellen möchten.</span><span class="sxs-lookup"><span data-stu-id="03edb-p104">When a page layout includes one or more Web Part zones, the Web Part zones are available on all pages that use that layout, which enables authors to insert Web Parts onto those pages. If you enable authors to insert Web Parts on pages, you reduce your control over the users' experience of the site. For example, an author could insert a Table of Contents Web Part onto a page that exposes parts of your site that you don't want visitors to navigate to from the current page.</span></span>
  
    
    
<span data-ttu-id="03edb-p105">Wenn Sie die volle Kontrolle darüber wünschen, wie ein Webpart auf Ihrer Website angezeigt wird, und es auf allen Seiten eines bestimmten Typs angezeigt werden soll, fügen Sie das Webpart direkt einem Seitenlayout hinzu. Wenn ein Webpart auf allen Seiten einer Website angezeigt werden soll, können Sie es auch direkt einer Gestaltungsvorlage hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-p105">If you want complete control over how a Web Part appears on your site, and if you want that Web Part to appear on all pages of a certain type, add the Web Part directly to a page layout. If you want a Web Part to appear on all pages in a site, you can also add a Web Part directly to a master page.</span></span>
  
    
    

> <span data-ttu-id="03edb-127"> **Hinweis:** Webpartzonen stehen für Seitenlayouts, aber nicht für Gestaltungsvorlagen zur Verfügung. Zweck der Zonen ist es, Autoren das Ändern von Webparts zu erlauben, denn Autoren bearbeiten in der Regel keine Gestaltungsvorlagen.</span><span class="sxs-lookup"><span data-stu-id="03edb-127">**Note** Web Part zones are available on page layouts but not on master pages—the purpose of zones is to allow authors to modify Web Parts, and authors typically don't edit a master page.</span></span> 
  
    
    

<span data-ttu-id="03edb-p106">Sie können einem Seitenlayout auch Webpartzonen hinzufügen, ihre Nutzung jedoch einschränken. Sie können beispielsweise Webparts einer Zone hinzufügen und anschließend eine Eigenschaft dieser Zone so festlegen, dass Inhaltsautoren die Eigenschaften vorhandener Webparts ändern, aber der Zone keine Webparts hinzufügen oder daraus entfernen können. Webpartzonen verfügen über Gruppen von Eigenschaften mit einem doppelten Zweck. Mit einer Untergruppe von Eigenschaften lassen sich das Layout und Format von Webparts auf der Seite organisieren. Mithilfe einer anderen Untergruppe können Sie eine weitere Schutzebene gegen Änderungen der Webparts innerhalb der Zone hinzufügen (sie also sperren).</span><span class="sxs-lookup"><span data-stu-id="03edb-p106">You can also add Web Part zones to a page layout but restrict their use. For example, you can add Web Parts to a zone, and then set a property of that zone so that content authors can edit the properties of existing Web Parts but not add or remove Web Parts from the zone. Web Part zones have a set of properties that serve a dual purpose. You can use one subset of properties to organize the layout and format of Web Parts on the page. You can use another subset of properties to provide an additional level of protection from modification (or "lock down") of the Web Parts within the zone.</span></span>
  
    
    
<span data-ttu-id="03edb-133">Sie haben folgende Möglichkeiten, die Darstellung von Webparts auf Ihrer Website zu steuern:</span><span class="sxs-lookup"><span data-stu-id="03edb-133">For varying levels of control over how Web Parts are presented on your site, you can:</span></span>
  
    
    

- <span data-ttu-id="03edb-p107">Webparts direkt einer Gestaltungsvorlage oder einem Seitenlayout hinzufügen. Dies bringt mit sich, dass Inhaltsautoren die Webparts nicht ändern können.</span><span class="sxs-lookup"><span data-stu-id="03edb-p107">Add Web Parts directly to a master page or page layout. This means content authors cannot modify the Web Parts.</span></span>
    
  
- <span data-ttu-id="03edb-136">Webparts zu Zonen in Seitenlayouts hinzufügen, doch diese Zonen ausschließlich auf die Standardwebparts beschränken, die Sie hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-136">Add Web Parts to zones on page layouts, but restrict those zones to only the default Web Parts that you add.</span></span>
    
  
- <span data-ttu-id="03edb-137">Webpartzonen zu Seitenlayouts hinzufügen und Inhaltsautoren die vollständige Kontrolle darüber geben, welche Webparts in diesen Zonen angezeigt und wie diese konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="03edb-137">Add Web Part zones to page layouts, and give content authors complete control over what Web Parts appear in those zones and how they are configured.</span></span>
    
  
<span data-ttu-id="03edb-138">Mit den Eigenschaften einer Webpartzone kann angegeben werden, ob Inhaltsautoren Folgendes ändern dürfen:</span><span class="sxs-lookup"><span data-stu-id="03edb-138">The properties of a Web Part zone can specify whether content authors are allowed to change:</span></span>
  
    
    

- <span data-ttu-id="03edb-139">Das Layout von Webparts in der Zone durch Hinzufügen, Löschen, Verschieben oder Verändern der Größe von Webparts.</span><span class="sxs-lookup"><span data-stu-id="03edb-139">The layout of Web Parts in the zone by adding, deleting, resizing, or moving the Web Parts.</span></span>
    
  
- <span data-ttu-id="03edb-140">Die Webparteinstellungen für alle Benutzer (die freigegebene Ansicht eines Webparts).</span><span class="sxs-lookup"><span data-stu-id="03edb-140">The Web Part settings for all users (the shared view of a Web Part).</span></span>
    
  
- <span data-ttu-id="03edb-141">Die persönlichen Webparteinstellungen (die persönliche Ansicht eines Webparts).</span><span class="sxs-lookup"><span data-stu-id="03edb-141">Their personal Web Part settings (the personal view of a Web Part).</span></span>
    
  
<span data-ttu-id="03edb-142">Tabelle 1 zeigt wichtige Eigenschaften, die beim Einschränken einer Webpartzone berücksichtigt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="03edb-142">Table 1 shows important properties to consider when you want to restrict a Web Part zone.</span></span>
  
    
    

<span data-ttu-id="03edb-143">**Tabelle 1. Eigenschaften von Webpartzonen zum Einschränken von Inhaltsautoren**</span><span class="sxs-lookup"><span data-stu-id="03edb-143">**Table 1. Web Part zone properties used to restrict content authors**</span></span>


|<span data-ttu-id="03edb-144">**Eigenschaftenname**</span><span class="sxs-lookup"><span data-stu-id="03edb-144">**Property Name**</span></span>|<span data-ttu-id="03edb-145">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="03edb-145">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="03edb-146">**AllowLayoutChange**</span><span class="sxs-lookup"><span data-stu-id="03edb-146">**AllowLayoutChange**</span></span> <br/> |<span data-ttu-id="03edb-147">Gibt an, ob Webparts innerhalb der Zone geschlossen, minimiert, gelöscht oder wiederhergestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="03edb-147">Specifies whether Web Parts within the zone can be closed, minimized, deleted, or restored.</span></span>  <br/> <span data-ttu-id="03edb-p108">Bei Festlegung auf **False** können Benutzer Webparts in der Zone nicht schließen, minimieren, löschen oder wiederherstellen, nicht in eine andere Zone ziehen und nicht neu anordnen oder innerhalb der Zone verschieben. Benutzer können außerdem keine Webparts aus dem Webpartkatalog hinzufügen. Zudem sind mehrere Eigenschaften deaktiviert, die sich auf die Benutzeroberfläche von Webparts in der Zone auswirken. Diese Eigenschaft wirkt sich nicht auf die Fähigkeit aus, das Layout programmgesteuert zu ändern.</span><span class="sxs-lookup"><span data-stu-id="03edb-p108">If set to **False**, users cannot close, minimize, delete, or restore Web Parts in the zone, drag Web Parts to a different zone, or rearrange or move Web Parts within the zone. Users also cannot add Web Parts from the Web Part catalog, and several properties that affect the UI of Web Parts in the zone are disabled. This property does not affect the ability to change the layout programmatically.  </span></span><br/> <span data-ttu-id="03edb-151">Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen diese Aktionen ausführen.</span><span class="sxs-lookup"><span data-stu-id="03edb-151">If set to **True**, users with appropriate permissions can perform these actions.</span></span>  <br/> |
|<span data-ttu-id="03edb-152">**LockLayout**</span><span class="sxs-lookup"><span data-stu-id="03edb-152">**LockLayout**</span></span> <br/> |<span data-ttu-id="03edb-p109">Gibt an, ob Webparts innerhalb der Zone hinzugefügt, gelöscht oder verschoben werden können bzw. ob ihre Größe geändert werden kann. Diese Eigenschaft funktioniert unabhängig davon gleich, ob die Webpartseite in der persönlichen oder freigegebenen Ansicht angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="03edb-p109">Specifies whether Web Parts within the zone can be added, deleted, resized, or moved. This property works the same whether the Web Part Page is in personal view or shared view.  </span></span><br/> <span data-ttu-id="03edb-p110"> Bei Festlegung auf **True** sind die folgenden spezifischen Webparteigenschaften für jedes Webpart in der Zone betroffen: **Zone (ZoneID)**, **Reihenfolge der Teile (PartOrder)**, **Auf Seite sichtbar (IsVisible)**, **Höhe (Height)**, **Breite (Width)**, **Schließen zulassen (AllowRemove)** und **IsIncluded** (der Befehl **Schließen** im Menü **Webpart**). Andere Webparteigenschaften sind nicht betroffen.  </span><span class="sxs-lookup"><span data-stu-id="03edb-p110">If set to **True**, the specific Web Part properties for each Web Part in the zone that are affected are: **Zone (ZoneID)**, **Part Order (PartOrder)**, **Visible on Page (IsVisible)**, **Height (Height)**, **Width (Width)**, **Allow Close (AllowRemove)**, and **IsIncluded** (the **Close** command on the **Web Part** menu). Other Web Part properties are not affected. </span></span><br/> <span data-ttu-id="03edb-157">Bei Festlegung auf **False** bestimmen die Webparteigenschaften (gemeinsam mit den entsprechenden Websiteberechtigungen), ob Änderungen erfolgen dürfen.</span><span class="sxs-lookup"><span data-stu-id="03edb-157">If set to **False**, the Web Part properties determine whether modifications can be made (together with the appropriate site permissions).</span></span>  <br/> |
|<span data-ttu-id="03edb-158">**AllowCustomization**</span><span class="sxs-lookup"><span data-stu-id="03edb-158">**AllowCustomization**</span></span> <br/> |<span data-ttu-id="03edb-159">Gibt an, ob freigegebene Eigenschaftenwerte von Webparts innerhalb der Zone geändert werden können.</span><span class="sxs-lookup"><span data-stu-id="03edb-159">Specifies whether shared property values of Web Parts within the zone can be modified.</span></span>  <br/> <span data-ttu-id="03edb-160">Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen Änderungen an der Webparts in der Zone für alle Benutzer vornehmen.</span><span class="sxs-lookup"><span data-stu-id="03edb-160">If set to **True**, users with appropriate permissions can make changes to the Web Parts in the zone for all users.</span></span>  <br/> <span data-ttu-id="03edb-161">Bei Festlegung auf **False** können Benutzer auf der Benutzeroberfläche der freigegebenen Ansicht keine Änderungen an den Webparts in der Zone vornehmen.</span><span class="sxs-lookup"><span data-stu-id="03edb-161">If set to **False**, users cannot make changes to the Web Parts in the zone in the UI in shared view. But, changes can still be made programmatically and by using the Web Part Maintenance page.</span></span> <span data-ttu-id="03edb-162">Änderungen können jedoch weiter programmgesteuert und über die Seite Webpartwartung erfolgen.</span><span class="sxs-lookup"><span data-stu-id="03edb-162">If set to False, users cannot make changes to the Web Parts in the zone in the UI in shared view. But, changes can still be made programmatically and by using the Web Part Maintenance page.</span></span>  <br/> |
|<span data-ttu-id="03edb-163">**AllowPersonalization**</span><span class="sxs-lookup"><span data-stu-id="03edb-163">**AllowPersonalization**</span></span> <br/> |<span data-ttu-id="03edb-164">Gibt an, ob persönliche Eigenschaftenwerte von Webparts innerhalb der Zone geändert werden können.</span><span class="sxs-lookup"><span data-stu-id="03edb-164">Specifies whether personal property values of Web Parts within the zone can be modified.</span></span>  <br/> <span data-ttu-id="03edb-165">Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen persönliche Änderungen an den Webparts in der Zone vornehmen.</span><span class="sxs-lookup"><span data-stu-id="03edb-165">If set to **True**, users with appropriate permissions can make personal changes to the Web Parts in the zone.</span></span>  <br/> <span data-ttu-id="03edb-166">Bei Festlegung auf **False** können Benutzer auf der Benutzeroberfläche keine persönlichen Änderungen vornehmen, es sei denn, das Webpart ist privat und sie verfügen über die benötigten Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="03edb-166">If set to **False**, users cannot make personal changes to the Web Parts through the UI, unless the Web Part is a private Web Part and they have appropriate permissions.</span></span>  <br/> |
   

> <span data-ttu-id="03edb-167">**Hinweis:** Sie können keine Webpartzone in einen Gerätekanalbereich einfügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-167">**Note:** You cannot insert a Web Part zone inside a Device Channel Panel.</span></span> <span data-ttu-id="03edb-168">Wenn Sie zulassen möchten, dass Autoren Webparts zu einer Seite hinzufügen können, und wenn Sie sich keine Sorgen über die Seitengewichtung für mobile Geräte machen, können Sie ein Rich-Text-Editor-Seitenfeld in einen Gerätekanalbereich einfügen und dann die Autoren anweisen, Webparts dort hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-168">Web Part zones You cannot insert a Web Part zone inside a Device Channel Panel. If you want to allow authors to add Web Parts to a page, and if you are not concerned about the page weight for mobile devices, you can add a Rich Text Editor page field to a Device Channel Panel, and then instruct authors to add Web Parts there. You can add Web Parts directly to a Device Channel Panel (without a Web Part zone).</span></span> <span data-ttu-id="03edb-169">Sie können Webparts direkt zu einem Gerätekanalbereich (ohne eine Webpartzone) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-169">You can add Web Parts directly to a Device Channel Panel (without a Web Part zone).</span></span> <span data-ttu-id="03edb-170">Weitere Informationen finden Sie unter [Vorgehensweise: Hinzufügen eines Gerätekanalbereich-Ausschnitts in SharePoint](how-to-add-a-device-channel-panel-snippet-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-170">[How to: Add a Device Channel Panel snippet in SharePoint](how-to-add-a-device-channel-panel-snippet-in-sharepoint.md)</span></span> 
  
    
    


## <a name="inserting-a-web-part-zone-snippet"></a><span data-ttu-id="03edb-171">Einfügen eines Webpartzone-Ausschnitts</span><span class="sxs-lookup"><span data-stu-id="03edb-171">Inserting a Web Part zone snippet</span></span>
<span data-ttu-id="03edb-172"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="03edb-172"></span></span>

<span data-ttu-id="03edb-p113">Wie alle Codeausschnitte können Sie diesen Codeausschnitt aus dem Codeausschnittkatalog hinzufügen. Sie müssen zunächst ein zu bearbeitendes Seitenlayout auswählen, um zum Codeausschnittkatalog zu gelangen. Sie können Webpartzonen zwar Seitenlayouts, aber nicht Gestaltungsvorlagen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-p113">Like all snippets, you add this snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a page layout to edit. Web Part zones can be added to page layouts but cannot be added to master pages.</span></span>
  
    
    

### <a name="to-insert-a-web-part-zone-snippet"></a><span data-ttu-id="03edb-176">So fügen Sie den Codeausschnitt "Webpartzone" ein</span><span class="sxs-lookup"><span data-stu-id="03edb-176">To insert a Web Part zone snippet</span></span>


1. <span data-ttu-id="03edb-177">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="03edb-177">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="03edb-178">Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="03edb-178">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="03edb-179">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Seitenlayouts bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="03edb-179">In Design Manager, in the left navigation pane, choose **Edit Page Layouts**.</span></span>
    
  
4. <span data-ttu-id="03edb-180">Wählen Sie den Namen des Seitenlayouts aus, dem Sie den Codeausschnitt hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="03edb-180">Select the name of the page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="03edb-181">Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.</span><span class="sxs-lookup"><span data-stu-id="03edb-181">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="03edb-182">Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** die Option **Webpartzone** aus.</span><span class="sxs-lookup"><span data-stu-id="03edb-182">On the ribbon, on the **Design** tab, choose **Web Part zone**.</span></span>
    
  
7. <span data-ttu-id="03edb-183">Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="03edb-183">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="03edb-p114">Der Abschnitt **Wichtig** enthält die Eigenschaften, die bekannt sein müssen, um die Funktionsweise dieses bestimmten Codeausschnitts zu kennen. Für eine Webpartzone hat der Codeausschnitt eine eindeutige ID. Nachdem Sie den Codeausschnitt in Ihr Seitenlayout kopiert haben, dürfen Sie diese ID nicht wiederverwenden. Wenn Sie einen weiteren Codeausschnitt "Webpartzone" hinzufügen möchten, wählen Sie **Aktualisieren**, um eine neue ID für den nächsten Codeausschnitt zu generieren.</span><span class="sxs-lookup"><span data-stu-id="03edb-p114">The section named **Important** contains the properties that are key to how this particular snippet works. For a Web Part zone, the snippet has a unique ID. After you copy the snippet into your page layout, you should not reuse this ID. If you want to add another Web Part zone snippet, choose **Refresh** to generate a new ID for the next snippet.</span></span>
    
    <span data-ttu-id="03edb-188">Eine Beschreibung der Eigenschaften, die erforderlich sind, um eine Webpartzone einzuschränken (**LockLayout**, **AllowCustomization** und **AllowPersonalization**) finden Sie in Tabelle 1.</span><span class="sxs-lookup"><span data-stu-id="03edb-188">For descriptions of properties that are necessary for restricting a Web Part zone ( **LockLayout**, **AllowCustomization**, and **AllowPersonalization**), see Table 1.</span></span>
    
    > <span data-ttu-id="03edb-189">**Hinweis:** Sie werden möglicherweise feststellen, dass einige Eigenschaftennamen im Eigenschaftenraster des Codeausschnittkatalogs fett formatiert sind.</span><span class="sxs-lookup"><span data-stu-id="03edb-189">**Note:** You may notice that some property names are bold in the property grid of the Snippet Gallery.</span></span> <span data-ttu-id="03edb-190">Diese Eigenschaften besitzen Werte, die von der Standardeinstellung für diese Komponente geändert wurden, diese Eigenschaften sind jedoch für ein Designer-Szenario nicht zwingend relevant.</span><span class="sxs-lookup"><span data-stu-id="03edb-190">You may notice that some property names are bold in the property grid of the Snippet Gallery. These properties have values that have been changed from the default setting for this component, but these properties are not necessarily relevant to a designer scenario. In other words, a property may be bold but not necessarily important for your scenario.</span></span> <span data-ttu-id="03edb-191">In anderen Worten: Eine Eigenschaft ist möglicherweise fett formatiert, aber nicht notwendigerweise wichtig für Ihr Szenario.</span><span class="sxs-lookup"><span data-stu-id="03edb-191">In other words, a property may be bold but not necessarily important for your scenario.</span></span> 
8. <span data-ttu-id="03edb-p116">Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="03edb-p116">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="03edb-195">Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.</span><span class="sxs-lookup"><span data-stu-id="03edb-195">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="03edb-196">Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-196">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
    <span data-ttu-id="03edb-197">Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-197">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="03edb-198">Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="03edb-198">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="03edb-199">Wenn Sie den Codeausschnitt dem Seitenlayout hinzufügen, vergewissern Sie sich, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**-Tags einfügen.</span><span class="sxs-lookup"><span data-stu-id="03edb-199">When you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="03edb-200">Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="03edb-200">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
  
13. <span data-ttu-id="03edb-201">Wenn Sie die Zone vorab mit Webparts auffüllen möchten, um z. B. festzulegen, dass Inhaltsautoren nur vorhandene Webparts ändern, aber keine neuen hinzufügen dürfen, fügen Sie Webpart-Codeausschnitte dort ein, wo das **<!--DC … -->**-Tag angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="03edb-201">If you want to prepopulate the zone with Web Parts—for example, if the zone will restrict content authors to modifying only existing Web Parts and not adding new ones—insert Web Part snippets where the **<!--DC … -->** tag appears.</span></span>
    
  
14. <span data-ttu-id="03edb-202">Speichern Sie die Seite, und aktualisieren Sie anschließend im Entwurfs-Manager die serverseitige Vorschau, um sicherzustellen, dass die Seite wie gewünscht angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="03edb-202">Save the page, and then refresh the server-side preview in Design Manager to make sure the page appears as expected.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="03edb-203">Grundlegendes zum Codeausschnittmarkup</span><span class="sxs-lookup"><span data-stu-id="03edb-203">Understanding the snippet markup</span></span>
<span data-ttu-id="03edb-204"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="03edb-204"></span></span>

<span data-ttu-id="03edb-p117">Die beiden wichtigsten Teile eines Webpartzonen-Codeausschnitts sind die Eigenschaft **ID** und der Kommentar **<!--DC … -->**. Jede Zone muss eine eindeutige ID haben. Wenn Sie Ihrem Seitenlayout mehr als eine Webpartzone hinzufügen möchten, wählen Sie im Codeausschnittkatalog **Aktualisieren** aus, bevor Sie die einzelnen Codeausschnitte kopieren, damit eine neue ID generiert wird. Der Kommentar **<!--DC … -->** muss durch Webparts ersetzt werden, die standardmäßig in der Zone angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="03edb-p117">The two most important parts of a Web Part zone snippet are the **ID** property and the **<!--DC … -->** comment. Each zone should have a unique ID. If you want to add more than one Web Part zone to your page layout, make sure to choose **Refresh** in the Snippet Gallery before copying each snippet so that a new ID is generated. The **<!--DC … -->** comment should be replaced with any Web Parts that you want to appear in the zone by default.</span></span>
  
    
    
<span data-ttu-id="03edb-209">Der folgende Code enthält weitere Eigenschaft zum Einschränken, wie Inhaltsautoren Zonen verwenden können ( **AllowCustomization**, **AllowPersonalization** und **LockLayout**).</span><span class="sxs-lookup"><span data-stu-id="03edb-209">Additional properties that can be used to restrict how content authors can use zones ( **AllowCustomization**, **AllowPersonalization**, and **LockLayout**) are shown in the following code.</span></span>
  
    
    

> <span data-ttu-id="03edb-210"> **Hinweis:** Die Eigenschaften **AllowCustomization**, **AllowPersonalization** und **LockLayout** werden nur dann im Markup angezeigt, wenn Sie ihre Standardwerte im Eigenschaftenraster ändern.</span><span class="sxs-lookup"><span data-stu-id="03edb-210">**Note** The **AllowCustomization**, **AllowPersonalization**, and **LockLayout** properties appear in the markup only if you change their default values in the property grid.</span></span>
  
    
    




```HTML

<div data-name="WebPartZone">
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <div xmlns:ie="ie">
        <!--MS:<WebPartPages:WebPartZone runat="server" ID="x0e5f5212505f48a9aac43df13eeae4f9" AllowCustomization="True" AllowPersonalization="False" FrameType="TitleBarOnly" LockLayout="True" Orientation="Vertical">-->
            <!--MS:<ZoneTemplate>-->
               <!--DC: Replace this comment with default web parts for new pages. -->
            <!--ME:</ZoneTemplate>-->
        <!--ME:</WebPartPages:WebPartZone>-->
    </div>
    <!--CE: End Web Part Zone Snippet-->
</div>

```


## <a name="additional-resources"></a><span data-ttu-id="03edb-211">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="03edb-211">Additional resources</span></span>
<span data-ttu-id="03edb-212"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="03edb-212"></span></span>


-  [<span data-ttu-id="03edb-213">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="03edb-213">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  <span data-ttu-id="03edb-214">
  [WebPartZone-Klasse](http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.webparts.webpartzone.aspx)</span><span class="sxs-lookup"><span data-stu-id="03edb-214">[WebPartZone class](http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.webparts.webpartzone.aspx)</span></span>
    
  
-  <span data-ttu-id="03edb-215">
  [WebPartZoneBase-Eigenschaften](http://msdn.microsoft.com/en-us/library/335sw9k3.aspx)</span><span class="sxs-lookup"><span data-stu-id="03edb-215">[WebPartZoneBase properties](http://msdn.microsoft.com/en-us/library/335sw9k3.aspx)</span></span>
    
  
-  [<span data-ttu-id="03edb-216">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="03edb-216">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="03edb-217">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="03edb-217">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

