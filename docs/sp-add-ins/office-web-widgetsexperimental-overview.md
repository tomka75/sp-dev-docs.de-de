---
title: "Office Web Widgets – Experimentelle Übersicht"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 40770129baa7606b7e3ebf6fb7d99cefabf51df7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="office-web-widgets---experimental-overview"></a><span data-ttu-id="7b7b1-102">Office Web Widgets – Experimentelle Übersicht</span><span class="sxs-lookup"><span data-stu-id="7b7b1-102">Office Web Widgets - Experimental overview</span></span>
<span data-ttu-id="7b7b1-103">Erfahren Sie mehr über die Office Web Widgets - Experimental, die Sie in Office-Add-Ins, SharePoint-Add-Ins und auf Websites verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-103">Learn about the Office Web Widgets - Experimental that you can use in Office Add-ins, SharePoint Add-ins, and websites.</span></span>
 

 <span data-ttu-id="7b7b1-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="7b7b1-p102">**Vorsicht** Die Office Web Widgets - Experimental werden nur zu Recherche- und Feedbackzwecken bereitgestellt. Verwenden Sie sie nicht in Produktionsszenarios. Das Verhalten von Office Web Widgets kann sich in künftigen Versionen erheblich ändern. Lesen und prüfen Sie die  [Lizenzbedingungen für Office Web Widgets - Experimental](office-web-widgetsexperimental-license-terms.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p102">**Caution**  The Office Web Widgets - Experimental are only provided for research and feedback purposes. Do not use in production scenarios. The Office Web Widgets behavior may change significantly in future releases. Read and review the  [Office Web Widgets - Experimental License Terms](office-web-widgetsexperimental-license-terms.md).</span></span>
 


<span data-ttu-id="7b7b1-111">Clientsteuerelemente wie die Office Web Widgets - Experimental können den Arbeitsaufwand zur Erstellung von Add-Ins deutlich reduzieren und gleichzeitig die Qualität der Add-Ins steigern. Damit dies zutrifft, müssen die Widgets bestimmte Kriterien erfüllen:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-111">Client controls, such as the Office Web Widgets - Experimental, can greatly reduce the amount of time required to build add-ins, and at the same time, increase the quality of the add-ins. For this to be true, we have to be sure the widgets meet certain criteria:</span></span>
 


- <span data-ttu-id="7b7b1-112">Widgets müssen auf die Verwendung in jeder Webseite ausgelegt sein, auch wenn die Seite nicht auf SharePoint gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-112">Widgets must be designed to be used in any webpage, even if the page is not hosted on SharePoint.</span></span>
    
 
- <span data-ttu-id="7b7b1-p103">Widgets funktionieren innerhalb der Office-Steuerelementelaufzeit. Dadurch können Sie einen allgemeinen Satz von Anforderungen und eine einheitliche Syntax zur Verwendung der Widgets bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p103">Widgets work within the Office controls runtime. This lets us to provide a common set of requirements and a consistent syntax to use the widgets.</span></span>
    
 
- <span data-ttu-id="7b7b1-p104">Widgets, die mit SharePoint kommunizieren, verwenden die domänenübergreifende Bibliothek. Die Widgets weisen keine Abhängigkeiten von einer bestimmten serverseitigen Plattform oder Technologie auf. Sie können die Widgets unabhängig von der von Ihnen gewählten Servertechnologie verwenden.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p104">Widgets that communicate back to SharePoint use the cross-domain library. The widgets don't have a dependency on a particular server-side platform or technology. You can use the widgets regardless of your choice of server technology.</span></span>
    
 
- <span data-ttu-id="7b7b1-p105">Widgets müssen mit anderen Elementen in der Seite zusammen verwendet werden können. Der Einschluss des Widgets in einer Seite sollte darin befindliche Elemente nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p105">Widgets must coexist with other elements in the page. The inclusion of the widget to a page should not modify other elements in it.</span></span>
    
 
- <span data-ttu-id="7b7b1-p106">Gehen Sie umsichtig mit vorhandenen Frameworks um. Wir möchten sichergehen, dass Sie die Tools und Technologien, die Sie gewöhnt sind, auch weiterhin nutzen können.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p106">Play nice with existing frameworks. We want to be sure you can still use the tools and technologies that you are used to.</span></span>
    
 

<span data-ttu-id="7b7b1-122">**Abbildung 1: Ein Add-In, das Office Web Widgets - Experimental verwendet**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-122">**Figure 1. An add-in using Office Web Widgets - Experimental**</span></span>

 

 
![Demo zu Office Web Widgets - Experimental](../images/OfficeWebWidgetsOverview_demo.png)
 
<span data-ttu-id="7b7b1-p107">Sie können die Widgets verwenden, indem Sie das **Office Web Widgets – Experimental**-NuGet-Paket von Visual Studio installieren. Weitere Informationen finden Sie unter [Verwalten von NuGet-Paketen mithilfe des Dialogfelds](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). Sie können auch die [NuGet-Galerieseite](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/) durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p107">You can use the widgets by installing the  **Office Web Widgets - Experimental** NuGet package from Visual Studio For more information, see [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). You can also browse the  [NuGet gallery page](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
 
<span data-ttu-id="7b7b1-p108">Ihr Feedback und Ihre Kommentare haben uns bei der Auswahl bereitgestellter Widgets geholfen. Wie Sie in Abbildung 1 sehen können, können Sie jetzt das (1) Personenauswahl- und das (2) Desktoplistenansichts-Widget ausprobieren und damit experimentieren. Bitte geben Sie auf der [Office Developer Platform UserVoice](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p108">Your feedback and comments helped us decide what widgets to provide. As you can see in Figure 1, the (1) People Picker and (2) Desktop List View widgets are ready for you to try and experiment. Please keep the feedback coming at the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/)</span></span>
 
<span data-ttu-id="7b7b1-129">Sie können außerdem im Codebeispiel [Demo zu Office Web Widgets - Experimental](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e) sehen, wie die Widgets eingesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-129">You can also see the widgets in action in the  [Office Web Widgets - Experimental Demo](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e) code sample.</span></span>
 

## <a name="people-picker-widget"></a><span data-ttu-id="7b7b1-130">Personenauswahl-Widget</span><span class="sxs-lookup"><span data-stu-id="7b7b1-130">People Picker widget</span></span>

<span data-ttu-id="7b7b1-p109">Sie können das experimentelle Personenauswahl-Widget in Add-Ins verwenden, um Ihren Benutzern zu helfen, Personen und Gruppen in einem Mandanten zu suchen und auszuwählen. Benutzer können beginnen, etwas in das Textfeld einzugeben, und das Widget ruft die Personen ab, deren Name oder E-Mail-Adresse mit dem Text übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p109">You can use the experimental People Picker widget in add-ins to help your users find and select people and groups in a tenant. Users can start typing in the text box and the widget retrieves the people whose name or e-mail matches the text.</span></span>
 

 

<span data-ttu-id="7b7b1-133">**Abbildung 2: Personenauswahl-Widget beim Auflösen einer Abfrage**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-133">**Figure 2. People Picker widget solving a query**</span></span>

 

 
![Personenauswahl – Experimentelles Steuerelement auf einer Seite](../images/PeoplePicker_basic.png)
 
<span data-ttu-id="7b7b1-p110">Sie können das Widget im HTML-Markup oder programmgesteuert mithilfe von JavaScript deklarieren. In beiden Fällen können Sie ein **div**-Element als Platzhalter für das Widget verwenden. Sie können auch Eigenschaften und Ereignishandler für das Personenauswahl-Widget festlegen. Die folgende Tabelle zeigt die im Personenauswahl-Widget verfügbaren Eigenschaften und Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p110">You can declare the widget in the HTML markup or programmatically using JavaScript. In either case, you use a  **div** element as a placeholder for the widget. You can also set properties and event handlers for the People Picker widget. The following table shows the available properties and events in the People Picker widget.</span></span>
 

 


|<span data-ttu-id="7b7b1-139">**Eigenschaft/Ereignis**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-139">**Property/Event**</span></span>|<span data-ttu-id="7b7b1-140">**Typ**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-140">**Type**</span></span>|<span data-ttu-id="7b7b1-141">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-141">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7b7b1-142">**objectType**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-142">**objectType**</span></span>|<span data-ttu-id="7b7b1-143">JSON-Objekt (Liste mit Zeichenfolgen)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-143">JSON Object (list of strings)</span></span>| <span data-ttu-id="7b7b1-p111">Art von Elementen, die das Widget auflöst. Optionen: Benutzer, Gruppe, Standardeinstellung: nur Benutzer.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p111">Type of items the widget will resolve. Options: User Group Default to user only.</span></span>|
|<span data-ttu-id="7b7b1-146">**allowMultipleSelections**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-146">**allowMultipleSelections**</span></span>|<span data-ttu-id="7b7b1-147">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="7b7b1-147">Boolean</span></span>|<span data-ttu-id="7b7b1-p112">Wahr/Falsch. Wenn falsch, sollte das Widget die Auswahl von jeweils nur einem Element zulassen. Standard=Falsch.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p112">True/False. If False, the widget should allow selecting only one item at the time.  Default=False.</span></span>|
|<span data-ttu-id="7b7b1-151">**rootGroupName**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-151">**rootGroupName**</span></span>|<span data-ttu-id="7b7b1-152">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="7b7b1-152">string</span></span>|<span data-ttu-id="7b7b1-p113">Wenn angegeben, beschränkt das Widget die Auswahl auf Elemente in dieser Gruppe. Wenn nicht angegeben, fragt das Widget Objekte aus dem gesamten Mandanten ab.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p113">If provided, the widget will limit the selection to items in this group.  If not provided, the widget will query objects from the whole tenancy.</span></span>|
|<span data-ttu-id="7b7b1-155">**selectedItems**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-155">**selectedItems**</span></span>|<span data-ttu-id="7b7b1-156">JSON-Array</span><span class="sxs-lookup"><span data-stu-id="7b7b1-156">JSON array</span></span>|<span data-ttu-id="7b7b1-p114">Liste ausgewählter Elemente. Jedes Element gibt ein Objekt zurück, das einen Benutzer oder eine Gruppe darstellt.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p114">List of items selected. Each item will return an object representing a user or group.</span></span>|
|<span data-ttu-id="7b7b1-159">**onAdded**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-159">**onAdded**</span></span>|<span data-ttu-id="7b7b1-160">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-160">Function</span></span>|<span data-ttu-id="7b7b1-p115">Ereignis, das ausgelöst wird, wenn der Auswahl ein neues Objekt hinzugefügt wird. Die Handlerfunktion hat das hinzugefügte Objekt erhalten.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p115">Event that fires when a new object is added to the selection. The handler function received the object added.</span></span>|
|<span data-ttu-id="7b7b1-163">**onRemoved**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-163">**onRemoved**</span></span>|<span data-ttu-id="7b7b1-164">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-164">Function</span></span>|<span data-ttu-id="7b7b1-p116">Ereignis, das ausgelöst wird, wenn aus der Auswahl ein neues Objekt entfernt wird. Die Handlerfunktion hat das entfernte Objekt erhalten.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p116">Event that fires when a new object is removed from the selection. The handler function received the object removed.</span></span>|
|<span data-ttu-id="7b7b1-167">**onChange**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-167">**onChange**</span></span>|<span data-ttu-id="7b7b1-168">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-168">Function</span></span>|<span data-ttu-id="7b7b1-p117">Das Hinzufügen oder Entfernen von Objekten löst dieses Ereignis aus. An die Handlerfunktion werden keine Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p117">Either adding or removing objects triggers this event. No parameters are passed to the handler function.</span></span>|
|<span data-ttu-id="7b7b1-171">**validationErrors**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-171">**validationErrors**</span></span>|<span data-ttu-id="7b7b1-172">Bereich</span><span class="sxs-lookup"><span data-stu-id="7b7b1-172">Array</span></span>| <span data-ttu-id="7b7b1-173">Bereich möglicher Validierungsfehler: leer, uresolvedItem, tooManyItems</span><span class="sxs-lookup"><span data-stu-id="7b7b1-173">Array of possible validation errors: empty unresolvedItem tooManyItems</span></span>|
|<span data-ttu-id="7b7b1-174">**autoShowValidationMessage**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-174">**autoShowValidationMessage**</span></span>|<span data-ttu-id="7b7b1-175">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="7b7b1-175">Boolean</span></span>|<span data-ttu-id="7b7b1-176">Wahr=Anzeigen Falsch=Nicht anzeigen</span><span class="sxs-lookup"><span data-stu-id="7b7b1-176">True=Show False=Don't show</span></span>|
|<span data-ttu-id="7b7b1-177">**hasErrors**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-177">**hasErrors**</span></span>|<span data-ttu-id="7b7b1-178">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="7b7b1-178">Boolean</span></span>|<span data-ttu-id="7b7b1-179">Wahr= Es liegen 1 oder mehrere Validierungsfehler vor Falsch=Es liegen keine Validierungsfehler vor</span><span class="sxs-lookup"><span data-stu-id="7b7b1-179">True= There are 1 or more validation errors False=There are no validation errors</span></span>|
|<span data-ttu-id="7b7b1-180">**errors**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-180">**errors**</span></span>|<span data-ttu-id="7b7b1-181">Bereich</span><span class="sxs-lookup"><span data-stu-id="7b7b1-181">Array</span></span>| <span data-ttu-id="7b7b1-182">Bereich möglicher Validierungsfehler: leer, uresolvedItem, tooManyItems</span><span class="sxs-lookup"><span data-stu-id="7b7b1-182">Array of possible validation errors: empty unresolvedItem tooManyItems</span></span>|
|<span data-ttu-id="7b7b1-183">**displayErrors**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-183">**displayErrors**</span></span>|<span data-ttu-id="7b7b1-184">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="7b7b1-184">Boolean</span></span>|<span data-ttu-id="7b7b1-185">Wahr=Fehler anzeigen Falsch=Fehler nicht anzeigen</span><span class="sxs-lookup"><span data-stu-id="7b7b1-185">True=Display the errors False=Don't display the errors</span></span>|
<span data-ttu-id="7b7b1-p118">Die CSS-Klassen für das Personenauswahl-Widget sind im Stylesheet **Office.Controls.css** definiert. Sie können die Klassen überschreiben und das Widget für Ihr Add-In anpassen.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p118">The CSS classes for the People Picker widget are defined in the  **Office.Controls.css** style sheet. You can override the classes and style the widget for your add-in.</span></span>
 

 
<span data-ttu-id="7b7b1-188">Weitere Informationen finden Sie unter  [Verwenden des experimentellen Personenauswahl-Widgets in SharePoint-Add-Ins](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md) und im Codebeispiel [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-188">For more information, see  [Use the experimental People Picker widget in SharePoint Add-ins](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md) and [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85.md) code sample.</span></span>
 

 

## <a name="desktop-list-view-widget"></a><span data-ttu-id="7b7b1-189">Desktoplistenansichts-Widget</span><span class="sxs-lookup"><span data-stu-id="7b7b1-189">Desktop List View widget</span></span>

<span data-ttu-id="7b7b1-190">Ihre Benutzer können vom Desktoplistenansichts-Widget profitieren und die Daten wie mit dem regulären Listenansichts-Widget in einer Liste anzeigen. Sie können es aber in Add-Ins verwenden, die nicht unbedingt in SharePoint gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-190">Your users can benefit from the List View widget and display the data in a list just like the regular List View widget, but you can use it in your add-ins that are not necessarily hosted in SharePoint.</span></span>
 

 

<span data-ttu-id="7b7b1-191">**Abbildung 3: Desktoplistenansichts-Widget zeigt Daten in einer Liste an**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-191">**Figure 3. Desktop List View widget displaying the data in a list**</span></span>

 

 
![Desktoplistenansicht – Experimentelles Steuerelement auf einer Seite](../images/DesktopListView_basic.png)
 
<span data-ttu-id="7b7b1-193">Sie können eine vorhandene Ansicht für die Liste festlegen. Das Widget gibt die Felder in der Reihenfolge wieder, in der sie in der Ansicht angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-193">You can specify an existing view on the list, the widget renders the fields in the order that they appear in the view.</span></span>
 

 

    
 <span data-ttu-id="7b7b1-p119">**Hinweis** Aktuell zeigt das Desktoplistenansichts-Widget nur die Daten an. Es bietet keine Funktionen zur Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p119">**Note**  At this moment, the Desktop List View widget only displays the data. It doesn't offer editing capabilities.</span></span>
 

<span data-ttu-id="7b7b1-p120">Sie können mit einem **div**-Element einen Platzhalter für das Widget angeben. Sie können das Widget programmgesteuert oder deklarativ verwenden.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p120">You can provide a placeholder for the widget using a  **div** element. You can programmatically or declaratively use the widget.</span></span>
 

 
<span data-ttu-id="7b7b1-p121">Sie können außerdem Eigenschaften oder Ereignishandler für das Desktoplistenansichts-Widget festlegen. Die folgende Tabelle zeigt die im Desktoplistenansichts-Widget verfügbaren Eigenschaften und Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p121">You also can set properties or event handlers for the Desktop List View widget. The following table shows the available properties and events in the Desktop List View widget.</span></span>
 

 


|<span data-ttu-id="7b7b1-200">**Eigenschaft/Ereignis**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-200">**Property/Event**</span></span>|<span data-ttu-id="7b7b1-201">**Typ**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-201">**Type**</span></span>|<span data-ttu-id="7b7b1-202">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-202">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7b7b1-203">**listUrl**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-203">**listUrl**</span></span>|<span data-ttu-id="7b7b1-204">URL</span><span class="sxs-lookup"><span data-stu-id="7b7b1-204">URL</span></span>|<span data-ttu-id="7b7b1-p122">URL der Listenansicht, aus der Elemente abgerufen werden. Es kann sich um eine relative URL handeln, wobei dann davon ausgegangen wird, dass sie sich im Add-In-Web selbst oder unter einer absoluten URL befindet.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p122">URL of the list view to draw items from. It can be a relative URL in which case it will be assumed to be located on the add-in web itself or an absolute URL.</span></span>|
|<span data-ttu-id="7b7b1-207">**viewName**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-207">**viewName**</span></span>|<span data-ttu-id="7b7b1-208">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="7b7b1-208">string</span></span>|<span data-ttu-id="7b7b1-p123">Name der angezeigten Ansicht. Dies ist der Programmname der Ansicht (nicht der Anzeigename).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p123">Name of the view to show. This is the programmatic name of the view (not its display name).</span></span>|
|<span data-ttu-id="7b7b1-211">**onItemSelected**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-211">**onItemSelected**</span></span>|<span data-ttu-id="7b7b1-212">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-212">Function</span></span>|<span data-ttu-id="7b7b1-213">Ereignis, das ausgelöst wird, wenn ein Element in der Liste ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-213">Event that fires when an item is selected on the list.</span></span>|
|<span data-ttu-id="7b7b1-214">**onItemAdded**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-214">**onItemAdded**</span></span>|<span data-ttu-id="7b7b1-215">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-215">Function</span></span>|<span data-ttu-id="7b7b1-216">Ereignis, das ausgelöst wird, wenn der Liste ein neues Objekt hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-216">Event that fires when a new item is added to the list.</span></span>|
|<span data-ttu-id="7b7b1-217">**onItemRemoved**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-217">**onItemRemoved**</span></span>|<span data-ttu-id="7b7b1-218">Funktion</span><span class="sxs-lookup"><span data-stu-id="7b7b1-218">Function</span></span>|<span data-ttu-id="7b7b1-219">Ereignis, das ausgelöst wird, wenn ein Element aus der Liste entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-219">Event that fires when an item is removed from the list.</span></span>|
|<span data-ttu-id="7b7b1-220">**selectedItems**</span><span class="sxs-lookup"><span data-stu-id="7b7b1-220">**selectedItems**</span></span>|<span data-ttu-id="7b7b1-221">Bereich</span><span class="sxs-lookup"><span data-stu-id="7b7b1-221">Array</span></span>|<span data-ttu-id="7b7b1-222">Liste ausgewählter Elemente im JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-222">List of Selected items in JSON format.</span></span>|
<span data-ttu-id="7b7b1-p124">Das Widget erfordert das SharePoint-Website-Stylesheet. Sie können direkt auf das SharePoint-Stylesheet verweisen oder das Chrome-Widget verwenden. Weitere Informationen zum Stylesheet finden Sie unter  [Verwenden des Stylesheets einer SharePoint-Website in Add-Ins für SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) und [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p124">The widget requires the SharePoint website style sheet. You can reference the SharePoint style sheet directly or use the chrome widget. For more information about the style sheet, see  [Use a SharePoint website's style sheet in SharePoint Add-ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) and [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span> 
 

 
<span data-ttu-id="7b7b1-p125">Erfahren Sie im Codebeispiel  [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076), wie das Listenansichts-Widget eingesetzt wird. Lesen Sie außerdem  [Verwenden des experimentellen Desktoplistenansichts-Widgets in Add-Ins für SharePoint](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-p125">To see the List View widget in action, see the  [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076) code sample. Also see [Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="conclusion"></a><span data-ttu-id="7b7b1-228">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="7b7b1-228">Conclusion</span></span>

<span data-ttu-id="7b7b1-229">Widgets können Ihnen helfen, den Entwicklungsprozess zu beschleunigen, die Kosten zu reduzieren und die Markteinführung Ihrer Add-Ins zu verkürzen. Office Web Widgets - Experimental bietet Widgets, die Sie in Nicht-Produktions-Add-Ins verwenden können. Wir freuen uns auf Ihr Feedback und Ihre Kommentare auf der  [Office Developer Platform UserVoice-Website](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-229">Widgets can help to speed up the development process and reduce the cost and time-to-market of your add-ins. Office Web Widgets - Experimental provide widgets that you can use in your non-production add-ins. Your feedback and comments are welcome in the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="7b7b1-230">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7b7b1-230">Additional resources</span></span>
<span data-ttu-id="7b7b1-231"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7b7b1-231"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="7b7b1-232">Lizenzbedingungen für Office Web Widgets - Experimental</span><span class="sxs-lookup"><span data-stu-id="7b7b1-232">Office Web Widgets - Experimental License Terms</span></span>](office-web-widgetsexperimental-license-terms.md)
    
 
-  [<span data-ttu-id="7b7b1-233">Office Web Widgets - Experimental – NuGet-Galerieseite</span><span class="sxs-lookup"><span data-stu-id="7b7b1-233">Office Web Widgets - Experimental NuGet gallery page</span></span>](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/)
    
 
-  [<span data-ttu-id="7b7b1-234">Verwenden des experimentellen Personenauswahl-Widgets in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="7b7b1-234">Use the experimental People Picker widget in SharePoint Add-ins</span></span>](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="7b7b1-235">Codebeispiel: Office Web Widgets - Experimentelle Demo</span><span class="sxs-lookup"><span data-stu-id="7b7b1-235">Code sample: Office Web Widgets - Experimental Demo</span></span>](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e)
    
 
-  [<span data-ttu-id="7b7b1-236">Verwenden des experimentellen Desktoplistenansichts-Widgets in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="7b7b1-236">Use the experimental Desktop List View widget in SharePoint Add-ins</span></span>](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="7b7b1-237">Codebeispiel: Verwenden des experimentellen Personenauswahl-Widgets in einem Add-In</span><span class="sxs-lookup"><span data-stu-id="7b7b1-237">Code sample: Use the People Picker experimental widget in an add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85)
    
 
-  [<span data-ttu-id="7b7b1-238">Codebeispiel: Verwenden des experimentellen Desktoplistenansichts-Widgets in einem Add-In</span><span class="sxs-lookup"><span data-stu-id="7b7b1-238">Code sample: Use the Desktop List View experimental widget in an add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076)
    
 
