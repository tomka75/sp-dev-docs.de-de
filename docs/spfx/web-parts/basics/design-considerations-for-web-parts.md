---
title: "Entwurfsüberlegungen für clientseitige SharePoint-Webparts"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 98a0662e893ea5f5729e6f77d01a51dcc5f57fb0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="design-considerations-for-sharepoint-client-side-web-parts"></a><span data-ttu-id="6304e-102">Entwurfsüberlegungen für clientseitige SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="6304e-102">Design considerations for SharePoint client-side web parts</span></span>

<span data-ttu-id="6304e-p101">Um mit der Entwicklung von Webparts zu beginnen, sollten Sie sich mit [Office UI Fabric](http://dev.office.com/fabric) vertraut machen. Alle Formatvorlagen aus [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) – einschließlich Symbolen, Typografie, Farben, Animationen und des dynamischen Rasters – werden standardmäßig geladen und stehen dem Webpart zur Verfügung. Importieren Sie keine Kopie der Fabric für Ihr Webpart, das dies einen Konflikt mit der globalen Kopie verursachen könnte. Diese Klassen bieten eine Grundlage für die Darstellung Ihres Webparts, die Sie jederzeit ändern können, wenn für die Marke Ihres Unternehmens andere Ausführungen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="6304e-p101">To get started designing web parts, you will want to be familiar with [Office UI Fabric](http://dev.office.com/fabric). All of the styles from [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) – including icons, typography, color usage, animation, and the responsive grid – are loaded by default and available to your web part. Do not import a copy of Fabric for your web part, as this may conflict with the global copy. These classes provide a foundation to your web part's styling, which you can always depart from if you require different visuals to match your company's brand.</span></span>

## <a name="office-ui-fabric-react-components"></a><span data-ttu-id="6304e-107">React-Komponenten der Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="6304e-107">Office UI Fabric React Components</span></span>

<span data-ttu-id="6304e-p102">Neben der Office UI Fabric können Sie React-Komponenten der Office UI Fabric verwenden, um Webparts zu erstellen. Bei Fabric React handelt es sich um eine dynamische Sammlung von Mobilitätskomponenten, die Ihnen das Erstellen von Weboberflächen mithilfe der Office-Entwurfssprache erleichtern.</span><span class="sxs-lookup"><span data-stu-id="6304e-p102">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts. Fabric React is a responsive, mobile-first collection of  components designed to make it quick and simple for you to create web experiences using the Office Design Language.</span></span>

<span data-ttu-id="6304e-110">Im folgenden Aufgabenlistenbeispiel werden Fabric-Komponenten im Eigenschaftenbereich verwendet, mit dem der Seitenautor ein Webpart konfigurieren kann.</span><span class="sxs-lookup"><span data-stu-id="6304e-110">The following To Do list example uses Fabric components in the property pane that lets the page author configure a web part.</span></span>

![Beispiel für ein Aufgaben-Webpart, das Fabric verwendet](../../../images/design-wp-todo-example.png)

<span data-ttu-id="6304e-112">Eine vollständige Liste der Office UI Fabric-Stile, -Typografie, -Farben, -Symbole und Animationen finden Sie unter [Office UI Fabric-Formatvorlagen](http://dev.office.com/fabric/styles).</span><span class="sxs-lookup"><span data-stu-id="6304e-112">You can find a complete list of the Office UI Fabric styles, typography, color, icons, and animations at [Office UI Fabric styles](http://dev.office.com/fabric/styles).</span></span>


## <a name="responsive-behavior"></a><span data-ttu-id="6304e-113">Dynamisches Verhalten</span><span class="sxs-lookup"><span data-stu-id="6304e-113">Responsive behavior</span></span>

<span data-ttu-id="6304e-114">Seiten in der neuen SharePoint-Erstellungsumgebung verwenden das dynamische Raster von Office UI Fabric, um sicherzustellen, dass jede Seite ansprechend aussieht.</span><span class="sxs-lookup"><span data-stu-id="6304e-114">Pages in the new SharePoint authoring experience use the Office UI Fabric responsive grid to help ensure that each page will look great.</span></span> 

### <a name="max-width"></a><span data-ttu-id="6304e-115">Maximale Breite</span><span class="sxs-lookup"><span data-stu-id="6304e-115">Max width</span></span>

<span data-ttu-id="6304e-p103">Es wird empfohlen, dass alle Webparts eine maximale Breite von 100 %, verwenden um sicherzustellen, dass sie auf jeder Seite dynamisch umbrechen und ordnungsgemäß funktionieren. Die Seiten- und Spaltenbreite wird von der Seitenvorlage definiert, kann aber vom Autor geändert werden. Wenn im Webpart ein maximaler Pixelwert festgelegt wird, könnte es unerwartete Ergebnisse sowohl im Hinblick auf die Funktionalität als auch auf das Layout geben, wenn die Seite mit unterschiedlichen Breiten angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6304e-p103">We recommend that all web parts use a 100% maximum width to ensure that they will re-flow and function properly on any page. The page and column widths are defined by the page template but can be modified by the author. If a max pixel value is set in the web part, there could be unexpected results in both functionality and layout when the page is seen at different widths.</span></span>

![Dynamisches Verhalten von Webparts mit maximaler Breite](../../../images/design-wp-responsive-max-width.png)

### <a name="min-width"></a><span data-ttu-id="6304e-120">Minimale Breite</span><span class="sxs-lookup"><span data-stu-id="6304e-120">Min width</span></span>

<span data-ttu-id="6304e-121">Alle Webparts sollten so gestaltet werden, dass sie dynamisch umbrechen, wenn die Seiten-/Spaltenbreite bis zu einer minimalen Breite von 320 px abnimmt.</span><span class="sxs-lookup"><span data-stu-id="6304e-121">All web parts should be designed to reflow as the page/column width gets smaller down to a min width of 320 px.</span></span>

![Dynamisches Verhalten von Webparts mit minimaler Breite](../../../images/design-wp-responsive-min-width.png)

## <a name="web-part-published-mode-vs-edit-mode"></a><span data-ttu-id="6304e-123">Webparts im Modus „Veröffentlicht“ und Webparts im Bearbeitungsmodus - Vergleich</span><span class="sxs-lookup"><span data-stu-id="6304e-123">Web part published mode vs edit mode</span></span>

<span data-ttu-id="6304e-124">Die neue SharePoint-Erstellungsumgebung weist zwei Modi auf:</span><span class="sxs-lookup"><span data-stu-id="6304e-124">The new SharePoint page authoring experience has two modes:</span></span>

* <span data-ttu-id="6304e-125">**Modus „Veröffentlicht“** In diesem Modus kann Ihr Team oder Ihre Zielgruppe den Inhalt anzeigen und mit Webparts interagieren.</span><span class="sxs-lookup"><span data-stu-id="6304e-125">**Published mode** which allows your team or audience to view content and interact with web parts.</span></span>
* <span data-ttu-id="6304e-126">**Bearbeitungsmodus** In diesem Modus können Seitenautoren Webparts hinzufügen und konfigurieren, um einer Seite Inhalte hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6304e-126">**Edit mode** which allows page author(s) to add and configure web parts to add content to a page.</span></span>

### <a name="edit-mode"></a><span data-ttu-id="6304e-127">Bearbeitungsmodus</span><span class="sxs-lookup"><span data-stu-id="6304e-127">Edit mode</span></span>

#### <a name="add-hint-and-toolbox"></a><span data-ttu-id="6304e-128">Hinweis zum Hinzufügen und Toolbox</span><span class="sxs-lookup"><span data-stu-id="6304e-128">Add hint and Toolbox</span></span>

<span data-ttu-id="6304e-p104">Der Hinweis zum Hinzufügen besteht aus einer horizontalen Linie mit einem Pluszeichen, die angezeigt wird, wenn ein Webpart ausgewählt wird, und wenn darauf gezeigt wird, um anzugeben, wo Seitenautoren neue Webparts zu ihrer Seite hinzufügen können. Die Toolbox wird geöffnet, wenn ein Benutzer auf das Pluszeichen tippt/klickt. Die Toolbox enthält alle Webparts, die einer Seite hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="6304e-p104">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page. The toolbox opens when a user clicks/taps the plus icon. The toolbox contains all the web parts that can be added to a page.</span></span>

![Hinweis zum Hinzufügen eines Webparts und Toolbox](../../../images/design-wp-toolbox.png)

#### <a name="toolbar"></a><span data-ttu-id="6304e-133">Symbolleiste</span><span class="sxs-lookup"><span data-stu-id="6304e-133">Toolbar</span></span>

<span data-ttu-id="6304e-p105">Eine vertikale Symbolleiste und das umgebende Feld sind Teil des Frameworks für jedes Webpart und werden von der Seite bereitgestellt. Jedes Webpart weist in der Symbolleiste eine Bearbeitungs- und Löschaktion auf.</span><span class="sxs-lookup"><span data-stu-id="6304e-p105">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span>

![Vertikale Webpart-Symbolleiste](../../../images/design-wp-toolbar.png)

#### <a name="contextual-edits"></a><span data-ttu-id="6304e-137">Kontextbezogene Bearbeitungen</span><span class="sxs-lookup"><span data-stu-id="6304e-137">Contextual edits</span></span>

<span data-ttu-id="6304e-p106">Für Webparts sollte eine WYSIWYG-Oberfläche entwickelt werden, damit Informationen eingetragen oder Inhalte hinzugefügt werden können, die dem Benutzer bei der Veröffentlichung angezeigt werden. Die Eingabe dieses Inhalts sollte auf der Seite erfolgen, damit der Benutzer versteht, wie der Inhalt für den Betrachter angezeigt wird. Titel und Beschreibungen sollten beispielsweise dort ausgefüllt werden, wo der Text angezeigt wird, oder neue Aufgaben sollten im Kontext der Seite hinzugefügt und geändert werden.</span><span class="sxs-lookup"><span data-stu-id="6304e-p106">A WYSIWYG experience should be designed for web parts to fill in information or add content that will be displayed to the user when published. Entering this content should be done in page so the user understands how the viewer will see the content. For example, titles and descriptions should be filled out where the text displays or new tasks should be added and modified in context of the page.</span></span>

![Kontextbezogene Bearbeitungen des Webparts](../../../images/design-wp-contexual-edits.png)

#### <a name="item-level-edits"></a><span data-ttu-id="6304e-142">Bearbeitungen auf Elementebene</span><span class="sxs-lookup"><span data-stu-id="6304e-142">Item-level edits</span></span>

<span data-ttu-id="6304e-143">Die Benutzeroberfläche kann sich innerhalb des Webparts ändern. Text wird zum Beispiel in ein Textfeld umgewandelt, damit Links eingetragen werden können, oder beim Anzeigen von UI zur Neuanordnung von Elementen oder zum Überprüfen von Aufgaben in einem Webpart.</span><span class="sxs-lookup"><span data-stu-id="6304e-143">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span>

![Webpart-Bearbeitungen auf Elementebene](../../../images/design-wp-item-level-edits.png)

## <a name="property-panes"></a><span data-ttu-id="6304e-145">Eigenschaftenbereiche</span><span class="sxs-lookup"><span data-stu-id="6304e-145">Property panes</span></span>

<span data-ttu-id="6304e-p107">Eigenschaftenbereiche werden über das Aktionssymbol zum Bearbeiten auf der Symbolleiste aufgerufen. Bereiche sollten in erster Linie Konfigurationseinstellungen enthalten, die Features aktivieren/deaktivieren, die entweder auf der Seite angezeigt werden oder die einen Aufruf eines Diensts vornehmen, um Inhalte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6304e-p107">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span>

![Design des Webpart-Eigenschaftenbereichs](../../../images/design-wp-pp.png)

<span data-ttu-id="6304e-149">Es gibt drei Arten von Eigenschaftenbereichen, mit denen Sie Webparts entwerfen und entwickeln können, die den Anforderungen Ihres Unternehmens oder Ihrer Kunden entsprechen.</span><span class="sxs-lookup"><span data-stu-id="6304e-149">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

### <a name="single-pane"></a><span data-ttu-id="6304e-150">Einzelner Bereich</span><span class="sxs-lookup"><span data-stu-id="6304e-150">Single pane</span></span>

<span data-ttu-id="6304e-151">Ein einzelner Bereich wird für einfache Webparts verwendet, bei denen nur eine kleine Anzahl von Eigenschaften konfiguriert werden kann.</span><span class="sxs-lookup"><span data-stu-id="6304e-151">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>

![Design des einzelnen Eigenschaftenbereichs des Webparts](../../../images/design-wp-pp-single.png)

### <a name="accordion-pane"></a><span data-ttu-id="6304e-153">Accordion-Bereich</span><span class="sxs-lookup"><span data-stu-id="6304e-153">Accordion pane</span></span>

<span data-ttu-id="6304e-p108">Ein Accordion-Bereich wird für eine Gruppe bzw. Gruppen von Eigenschaften mit vielen Optionen verwendet und dann, wenn die Gruppen zu einer langen Bildlaufleiste mit Optionen führen würden. Angenommen, Sie haben drei Gruppen mit dem Namen „Eigenschaften“, „Darstellung“ und „Layout“, von denen jede über zehn Komponenten verfügt.</span><span class="sxs-lookup"><span data-stu-id="6304e-p108">A accordion pane is used for containing a group or groups of properties with many options and where the groups would result in a long scrolling list of options. For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

#### <a name="accordion---one-group-open"></a><span data-ttu-id="6304e-156">Accordion - Eine geöffnete Gruppe</span><span class="sxs-lookup"><span data-stu-id="6304e-156">Accordion - One group open</span></span>

![Accordion-Eigenschaftenbereich eines Webparts mit einer geöffneten Gruppe](../../../images/design-wp-pp-accordion.png)

#### <a name="accordion--two-groups-open-and-scrolled"></a><span data-ttu-id="6304e-158">Accordion - Zwei geöffnete Gruppen mit Bildlauf</span><span class="sxs-lookup"><span data-stu-id="6304e-158">Accordion- Two groups open and scrolled</span></span>

![Accordion-Eigenschaftenbereich eines Webparts mit zwei geöffneten Gruppen und Bildlauf](../../../images/design-wp-pp-accordion-groups.png)


### <a name="property-pane-stepspages"></a><span data-ttu-id="6304e-160">Schritte/Seiten von Eigenschaftenbereichen</span><span class="sxs-lookup"><span data-stu-id="6304e-160">Property pane steps/pages</span></span>

<span data-ttu-id="6304e-161">Der Bereich „Schritte“ wird zum Gruppieren von Eigenschaften in mehreren Schritten oder Seiten verwendet, wenn das Webpart in einer linearen Reihenfolge konfiguriert werden muss oder wenn die beim ersten Schritt getroffene Auswahl Auswirkungen auf Optionen hat, die im zweiten Schritt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6304e-161">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span>

<span data-ttu-id="6304e-162">**Schritt 1 von 3**
![Eigenschaftenbereich mit Schrittedesign 1 von 3](../../../images/design-wp-pp-pages-step1.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-162">**Step 1 of 3**
![Property pane with steps design 1 of 3](../../../images/design-wp-pp-pages-step1.png)</span></span>

<span data-ttu-id="6304e-163">**Schritt 2 von 3**
![Eigenschaftenbereich mit Schrittedesign 2 von 3](../../../images/design-wp-pp-pages-step2.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-163">**Step 2 of 3**
![Property pane with steps design 2 of 3](../../../images/design-wp-pp-pages-step2.png)</span></span>

<span data-ttu-id="6304e-164">**Schritt 3 von 3**
![Eigenschaftenbereich mit Schrittedesign 3 von 3](../../../images/design-wp-pp-pages-step3.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-164">**Step 3 of 3**
![Property pane with steps design 3 of 3](../../../images/design-wp-pp-pages-step3.png)</span></span>


## <a name="reactive-vs-non-reactive-web-parts"></a><span data-ttu-id="6304e-165">Dynamisch Webparts und nicht dynamische Webparts - Vergleich</span><span class="sxs-lookup"><span data-stu-id="6304e-165">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="6304e-p109">Dynamische Webparts werden so entwickelt, dass sie vollständig clientseitige Webparts sind. Das bedeutet, dass jede Komponente, die im Eigenschaftenbereich konfiguriert wird, die Änderung, die innerhalb des Webparts auf der Seite vorgenommen wird, widerspiegelt. Wenn Sie im Aufgabenlisten-Webparts die Option „Abgeschlossene Aufgaben“ deaktivieren, wird diese Ansicht im Webpart ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="6304e-p109">Reactive web parts are designed to be full client-side web parts, which mean that each component that is configured in the properties pane will reflect as the change is made within the web part on the page. For the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Dynamisches Webpartdesign](../../../images/design-wp-pp-reactive.png)

<span data-ttu-id="6304e-p110">Nicht dynamische Webparts sind nicht vollständig clientseitig, und in der Regel muss mindestens eine Eigenschaft einen Aufruf ausführen, um Daten auf einem Server festzulegen/abzurufen oder zu speichern. In diesem Fall sollten Sie die Schaltflächen „Übernehmen“ und „Abbrechen“ am unteren Rand des Eigenschaftenbereich aktivieren.</span><span class="sxs-lookup"><span data-stu-id="6304e-p110">Non-reactive web parts are not fully client side and generally one or more properties need to make a call to set/pull or store data on a server. In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span>

![Nicht dynamisches Webpartdesign](../../../images/design-wp-pp-non-reactive.png)

## <a name="constructing-the-to-do-list-property-pane"></a><span data-ttu-id="6304e-172">Erstellen des Aufgabenlisten-Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="6304e-172">Constructing the To-Do List property pane</span></span>

<span data-ttu-id="6304e-p111">Das Beispiel der Aufgabenliste verwendet den einzelnen Eigenschaftenbereich, und es handelt sich um ein dynamisches Webpart. Nachfolgend ist eine React-Komponente von Fabric und das daraus resultierende Design dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6304e-p111">The To-Do List example uses the single pane and is a reactive web part. The following shows each Fabric React component and the resulting design.</span></span>

<span data-ttu-id="6304e-175">Hinzufügen einer Beschreibung für die Aufgabenliste![Hinzufügen einer Beschreibung für die Aufgabenliste](../../../images/design-wp-todo-pp-description.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-175">Adding a description for To-Do List ![Adding a description for To-Do List](../../../images/design-wp-todo-pp-description.png)</span></span>

<span data-ttu-id="6304e-176">Dropdown – Zum Auswählen von Aufgaben aus einer vorhandenen Liste ![Dropdown zum Auswählen von Aufgaben aus einer vorhandenen Liste](../../../images/design-wp-todo-pp-dropdown.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-176">Drop down – to select tasks from an existing list ![Drop down to select tasks from an existing list](../../../images/design-wp-todo-pp-dropdown.png)</span></span>

<span data-ttu-id="6304e-177">Kontrollkästchen – Ermöglicht Autoren das Ein-oder Ausblenden von verschiedenen Ansichten ![Kontrollkästchen, um Autoren das Ein-oder Ausblenden von verschiedenen Ansichten zu ermöglichen](../../../images/design-wp-todo-pp-checkbox.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-177">Checkbox– to allow authors to show or hide different views ![Checkbox to allow authors to show or hide different views](../../../images/design-wp-todo-pp-checkbox.png)</span></span>

<span data-ttu-id="6304e-178">Schieberegler – Zum Festlegen der Anzahl sichtbarer Aufgaben![Zum Festlegen der Anzahl sichtbarer Aufgaben](../../../images/design-wp-todo-pp-slider.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-178">Slider – to set the number of tasks visible ![Slider to set the number of tasks visible](../../../images/design-wp-todo-pp-slider.png)</span></span>

<span data-ttu-id="6304e-179">Nach dem Auswählen einer Liste aus dem Dropdown wird das Webpart angezeigt und gibt die Anzahl von Elementen an, die auf der Seite geladen werden ![Webpart, das die Ladeanzeige zum Laden von Elementen](../../../images/design-wp-todo-loading-indicator.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-179">After selecting a list from the drop down the web part shows and indicator of items loading onto the page ![Web part showing loading indicator to load items](../../../images/design-wp-todo-loading-indicator.png)</span></span>

<span data-ttu-id="6304e-180">Wenn die neuen Aufgaben geladen werden, werden Sie mithilfe von Animationsstilen aus Office UI Fabric eingeblendet ![Webpart mit Fabric-Animationen](../../../images/design-wp-todo-fabric-animations.png)</span><span class="sxs-lookup"><span data-stu-id="6304e-180">When the new tasks are loaded the fade into view using animation styles from Office UI Fabric ![Web part with fabric animations](../../../images/design-wp-todo-fabric-animations.png)</span></span>
