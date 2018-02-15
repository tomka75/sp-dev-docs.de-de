---
title: "Entwurfsüberlegungen für clientseitige SharePoint-Webparts"
description: Verwenden Sie React-Komponenten der Office UI Fabric zum Erstellen und Formatieren Ihrer Webparts.
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: d19d5593f6093ed44d993f9f61a37f56dcaa3883
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="design-considerations-for-sharepoint-client-side-web-parts"></a><span data-ttu-id="5a0f1-103">Entwurfsüberlegungen für clientseitige SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="5a0f1-103">Design considerations for SharePoint client-side web parts</span></span>

<span data-ttu-id="5a0f1-104">Um mit der Entwicklung von Webparts zu beginnen, sollten Sie sich mit [Office-UI-Fabric](https://developer.microsoft.com/de-DE/fabric) vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-104">To get started designing web parts, you need to be familiar with [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric).</span></span> <span data-ttu-id="5a0f1-105">Alle Formatvorlagen aus [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) – einschließlich Symbolen, Typografie, Farben, Animationen und des dynamischen Rasters – werden standardmäßig geladen und stehen dem Webpart zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-105">All of the styles from [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core), including icons, typography, color usage, animation, and the responsive grid, are loaded by default and available to your web part.</span></span> 

<span data-ttu-id="5a0f1-106">Importieren Sie keine Kopie der Fabric für Ihr Webpart, das dies einen Konflikt mit der globalen Kopie verursachen könnte.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-106">Do not import a copy of Fabric for your web part because this may conflict with the global copy.</span></span> <span data-ttu-id="5a0f1-107">Diese Klassen bieten eine Grundlage für die Darstellung Ihres Webparts, die Sie jederzeit ändern können, wenn für die Marke Ihres Unternehmens andere Ausführungen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-107">These classes provide a foundation to your web part's styling, which you can always depart from if you require different visuals to match your company's brand.</span></span>

## <a name="office-ui-fabric-react-components"></a><span data-ttu-id="5a0f1-108">React-Komponenten der Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="5a0f1-108">Office UI Fabric React Components</span></span>

<span data-ttu-id="5a0f1-109">Neben der Office-UI-Fabric können Sie React-Komponenten der Office-UI-Fabric verwenden, um Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-109">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts.</span></span> <span data-ttu-id="5a0f1-110">Bei Fabric React handelt es sich um eine dynamische Sammlung von Mobilitätskomponenten, die Ihnen das Erstellen von Weboberflächen mithilfe der Office-Entwurfssprache erleichtern.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-110">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts. Fabric React is a responsive, mobile-first collection of  components designed to make it quick and simple for you to create web experiences using the Office Design Language.</span></span>

<span data-ttu-id="5a0f1-111">Im folgenden Aufgabenlistenbeispiel werden Fabric-Komponenten im Eigenschaftenbereich verwendet, mit dem der Seitenautor ein Webpart konfigurieren kann.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-111">The following To Do list example uses Fabric components in the property pane that lets the page author configure a web part.</span></span>

![Beispiel für ein Aufgaben-Webpart, das Fabric verwendet](../../../images/design-wp-todo-example.png)

<span data-ttu-id="5a0f1-113">Eine vollständige Liste der Office UI Fabric-Stile, -Typografie, -Farben, -Symbole und Animationen finden Sie unter [Office UI Fabric-Formatvorlagen](https://developer.microsoft.com/de-DE/fabric#/styles).</span><span class="sxs-lookup"><span data-stu-id="5a0f1-113">You can find a complete list of the Office UI Fabric styles, typography, color, icons, and animations at [Office UI Fabric styles](https://developer.microsoft.com/de-DE/fabric#/styles).</span></span>


## <a name="responsive-behavior"></a><span data-ttu-id="5a0f1-114">Dynamisches Verhalten</span><span class="sxs-lookup"><span data-stu-id="5a0f1-114">Responsive behavior</span></span>

<span data-ttu-id="5a0f1-115">Seiten in der neuen SharePoint-Erstellungsumgebung verwenden das dynamische Raster von Office UI Fabric, um sicherzustellen, dass jede Seite ansprechend aussieht.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-115">Pages in the new SharePoint authoring experience use the Office UI Fabric responsive grid to help ensure that each page will look great.</span></span> 

### <a name="maximum-width"></a><span data-ttu-id="5a0f1-116">Maximale Breite</span><span class="sxs-lookup"><span data-stu-id="5a0f1-116">Maximum width</span></span>

<span data-ttu-id="5a0f1-117">Es wird empfohlen, dass alle Webparts eine maximale Breite von 100 %, verwenden um sicherzustellen, dass sie auf jeder Seite dynamisch umbrechen und ordnungsgemäß funktionieren.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-117">We recommend that all web parts use a 100% maximum width to ensure that they re-flow and function properly on any page.</span></span> <span data-ttu-id="5a0f1-118">Die Seiten- und Spaltenbreite wird von der Seitenvorlage definiert, kann aber vom Autor geändert werden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-118">The page and column widths are defined by the page template but can be modified by the author.</span></span> <span data-ttu-id="5a0f1-119">Wenn im Webpart ein maximaler Pixelwert festgelegt wird, könnte es unerwartete Ergebnisse sowohl im Hinblick auf die Funktionalität als auch auf das Layout geben, wenn die Seite mit unterschiedlichen Breiten angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-119">If a maximum pixel value is set in the web part, there could be unexpected results in both functionality and layout when the page is seen at different widths.</span></span>

![Dynamisches Verhalten von Webparts mit maximaler Breite](../../../images/design-wp-responsive-max-width.png)

### <a name="minimum-width"></a><span data-ttu-id="5a0f1-121">Minimale Breite</span><span class="sxs-lookup"><span data-stu-id="5a0f1-121">Minimum width</span></span>

<span data-ttu-id="5a0f1-122">Alle Webparts sollten so gestaltet werden, dass sie dynamisch umbrechen, wenn die Seiten-/Spaltenbreite bis zu einer minimalen Breite von 320 px abnimmt.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-122">All web parts should be designed to reflow as the page/column width gets smaller down to a min width of 320 px.</span></span>

![Dynamisches Verhalten von Webparts mit minimaler Breite](../../../images/design-wp-responsive-min-width.png)

<br/>

## <a name="web-part-edit-mode"></a><span data-ttu-id="5a0f1-124">Webpart-Bearbeitungsmodus</span><span class="sxs-lookup"><span data-stu-id="5a0f1-124">Web part Edit mode</span></span>

<span data-ttu-id="5a0f1-125">Die neue SharePoint-Erstellungsumgebung weist zwei Modi auf:</span><span class="sxs-lookup"><span data-stu-id="5a0f1-125">The new SharePoint page authoring experience has two modes:</span></span>

* <span data-ttu-id="5a0f1-126">**Modus „Veröffentlicht“** In diesem Modus kann Ihr Team oder Ihre Zielgruppe den Inhalt anzeigen und mit Webparts interagieren.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-126">**Published mode** which allows your team or audience to view content and interact with web parts.</span></span>
* <span data-ttu-id="5a0f1-127">**Bearbeitungsmodus** In diesem Modus können Seitenautoren Webparts hinzufügen und konfigurieren, um einer Seite Inhalte hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-127">**Edit mode** which allows page author(s) to add and configure web parts to add content to a page.</span></span>

<span data-ttu-id="5a0f1-128">In den folgenden Abschnitten wird der Bearbeitungsmodus beschrieben.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-128">The following sections describe Edit mode.</span></span>

### <a name="add-hint-and-toolbox"></a><span data-ttu-id="5a0f1-129">Hinweis zum Hinzufügen und Toolbox</span><span class="sxs-lookup"><span data-stu-id="5a0f1-129">Add hint and Toolbox</span></span>

<span data-ttu-id="5a0f1-130">Der Hinweis zum Hinzufügen besteht aus einer horizontalen Linie mit einem Pluszeichen, die angezeigt wird, wenn ein Webpart ausgewählt wird oder wenn auf ein Webpart gezeigt wird. Er markiert, wo Autoren neue Webparts zu ihrer Seite hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-130">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page.</span></span> <span data-ttu-id="5a0f1-131">Die Toolbox wird geöffnet, wenn ein Benutzer auf das Pluszeichen klickt.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-131">The Toolbox opens when a user chooses the plus icon.</span></span> <span data-ttu-id="5a0f1-132">Die Toolbox enthält alle Webparts, die einer Seite hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-132">The Toolbox contains all the web parts that can be added to a page.</span></span>

![Hinweis zum Hinzufügen eines Webparts und Toolbox](../../../images/design-wp-toolbox.png)

### <a name="toolbar"></a><span data-ttu-id="5a0f1-134">Symbolleiste</span><span class="sxs-lookup"><span data-stu-id="5a0f1-134">Toolbar</span></span>

<span data-ttu-id="5a0f1-p106">Eine vertikale Symbolleiste und das umgebende Feld sind Teil des Frameworks für jedes Webpart und werden von der Seite bereitgestellt. Jedes Webpart weist in der Symbolleiste eine Bearbeitungs- und Löschaktion auf.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-p106">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span>

![Vertikale Webpart-Symbolleiste](../../../images/design-wp-toolbar.png)

### <a name="contextual-edits"></a><span data-ttu-id="5a0f1-138">Kontextbezogene Bearbeitungen</span><span class="sxs-lookup"><span data-stu-id="5a0f1-138">Contextual edits</span></span>

<span data-ttu-id="5a0f1-139">Für Webparts sollte eine WYSIWYG-Oberfläche entwickelt werden, damit Informationen eingetragen oder Inhalte hinzugefügt werden können, die dem Benutzer bei der Veröffentlichung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-139">A WYSIWYG experience should be designed for web parts to fill in information or add content that is displayed to the user when published.</span></span> <span data-ttu-id="5a0f1-140">Die Eingabe dieses Inhalts sollte auf der Seite erfolgen, damit der Benutzer versteht, wie der Inhalt für den Betrachter angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-140">Entering this content should be done on the page so that the user understands how the viewer sees the content.</span></span> <span data-ttu-id="5a0f1-141">Titel und Beschreibungen sollten beispielsweise dort ausgefüllt werden, wo der Text angezeigt wird, oder neue Aufgaben sollten im Kontext der Seite hinzugefügt und geändert werden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-141">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Kontextbezogene Bearbeitungen des Webparts](../../../images/design-wp-contexual-edits.png)

### <a name="item-level-edits"></a><span data-ttu-id="5a0f1-143">Bearbeitungen auf Elementebene</span><span class="sxs-lookup"><span data-stu-id="5a0f1-143">Item-level edits</span></span>

<span data-ttu-id="5a0f1-144">Die Benutzeroberfläche kann sich innerhalb des Webparts ändern. Text wird zum Beispiel in ein Textfeld umgewandelt, damit Links eingetragen werden können, oder beim Anzeigen von UI zur Neuanordnung von Elementen oder zum Überprüfen von Aufgaben in einem Webpart.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-144">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span>

![Webpart-Bearbeitungen auf Elementebene](../../../images/design-wp-item-level-edits.png)

## <a name="property-panes"></a><span data-ttu-id="5a0f1-146">Eigenschaftenbereiche</span><span class="sxs-lookup"><span data-stu-id="5a0f1-146">Property panes</span></span>

<span data-ttu-id="5a0f1-147">Eigenschaftenbereiche werden über das Aktionssymbol zum Bearbeiten auf der Symbolleiste aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-147">Property panes are invoked via the Edit icon on the toolbar.</span></span> <span data-ttu-id="5a0f1-148">Bereiche sollten in erster Linie Konfigurationseinstellungen enthalten, die Features aktivieren/deaktivieren, die entweder auf der Seite angezeigt werden oder die einen Aufruf eines Diensts vornehmen, um Inhalte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-148">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span>

![Design des Webpart-Eigenschaftenbereichs](../../../images/design-wp-pp.png)

<span data-ttu-id="5a0f1-150">Es gibt drei Arten von Eigenschaftenbereichen, mit denen Sie Webparts entwerfen und entwickeln können, die den Anforderungen Ihres Unternehmens oder Ihrer Kunden entsprechen.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-150">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

### <a name="single-pane"></a><span data-ttu-id="5a0f1-151">Einzelner Bereich</span><span class="sxs-lookup"><span data-stu-id="5a0f1-151">Single pane</span></span>

<span data-ttu-id="5a0f1-152">Ein einzelner Bereich wird für einfache Webparts verwendet, bei denen nur eine kleine Anzahl von Eigenschaften konfiguriert werden kann.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-152">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>

![Design des einzelnen Eigenschaftenbereichs des Webparts](../../../images/design-wp-pp-single.png)

### <a name="accordion-pane"></a><span data-ttu-id="5a0f1-154">Accordion-Bereich</span><span class="sxs-lookup"><span data-stu-id="5a0f1-154">Accordion pane</span></span>

<span data-ttu-id="5a0f1-155">Ein Accordion-Bereich wird für eine Gruppe bzw. Gruppen von Eigenschaften mit vielen Optionen verwendet und dann, wenn die Gruppen zu einer langen Bildlaufleiste mit Optionen führen würden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-155">A accordion pane is used for containing a group or groups of properties with many options and where the groups would result in a long scrolling list of options. For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span> <span data-ttu-id="5a0f1-156">Ein Anwendungsbeispiel wäre ein Bereich mit drei Gruppen namens „Properties“, „Appearance“ und „Layout“, von denen jede über zehn Komponenten verfügt.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-156">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

#### <a name="accordion---one-group-open"></a><span data-ttu-id="5a0f1-157">Accordion - Eine geöffnete Gruppe</span><span class="sxs-lookup"><span data-stu-id="5a0f1-157">Accordion - One group open</span></span>

![Accordion-Eigenschaftenbereich eines Webparts mit einer geöffneten Gruppe](../../../images/design-wp-pp-accordion.png)

#### <a name="accordion---two-groups-open-and-scrolled"></a><span data-ttu-id="5a0f1-159">Accordion - Zwei geöffnete Gruppen mit Bildlauf</span><span class="sxs-lookup"><span data-stu-id="5a0f1-159">Accordion- Two groups open and scrolled</span></span>

![Accordion-Eigenschaftenbereich eines Webparts mit zwei geöffneten Gruppen und Bildlauf](../../../images/design-wp-pp-accordion-groups.png)


### <a name="property-pane-stepspages"></a><span data-ttu-id="5a0f1-161">Schritte/Seiten von Eigenschaftenbereichen</span><span class="sxs-lookup"><span data-stu-id="5a0f1-161">Property pane steps/pages</span></span>

<span data-ttu-id="5a0f1-162">Der Bereich „Schritte“ wird zum Gruppieren von Eigenschaften in mehreren Schritten oder Seiten verwendet, wenn das Webpart in einer linearen Reihenfolge konfiguriert werden muss oder wenn die beim ersten Schritt getroffene Auswahl Auswirkungen auf Optionen hat, die im zweiten Schritt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-162">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span>

#### <a name="step-1-of-3"></a><span data-ttu-id="5a0f1-163">Schritt 1 von 3</span><span class="sxs-lookup"><span data-stu-id="5a0f1-163">Step 1 of 3</span></span>

![Eigenschaftenbereich mit Schrittedesign 1 von 3](../../../images/design-wp-pp-pages-step1.png)

#### <a name="step-2-of-3"></a><span data-ttu-id="5a0f1-165">Schritt 2 von 3</span><span class="sxs-lookup"><span data-stu-id="5a0f1-165">Step 2 of 3</span></span>

![Eigenschaftenbereich mit Schrittedesign 2 von 3](../../../images/design-wp-pp-pages-step2.png)

#### <a name="step-3-of-3"></a><span data-ttu-id="5a0f1-167">Schritt 3 von 3</span><span class="sxs-lookup"><span data-stu-id="5a0f1-167">Step 3 of 3</span></span>

![Eigenschaftenbereich mit Schrittedesign 3 von 3](../../../images/design-wp-pp-pages-step3.png)


## <a name="reactive-vs-non-reactive-web-parts"></a><span data-ttu-id="5a0f1-169">Dynamische Webparts und nicht dynamische Webparts - Vergleich</span><span class="sxs-lookup"><span data-stu-id="5a0f1-169">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="5a0f1-170">**Dynamische Webparts** werden so entwickelt, dass sie vollständig clientseitige Webparts sind. Das bedeutet, dass jede Komponente, die im Eigenschaftenbereich konfiguriert wird, die Änderung, die innerhalb des Webparts auf der Seite vorgenommen wird, widerspiegelt.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-170">Reactive web parts are designed to be full client-side web parts, which mean that each component that is configured in the properties pane will reflect as the change is made within the web part on the page. For the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span> <span data-ttu-id="5a0f1-171">Deaktiviert der Benutzer im Aufgabenlisten-Webpart die Option „Completed Tasks“, wird die zugehörige Ansicht im Webpart ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-171">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Dynamisches Webpartdesign](../../../images/design-wp-pp-reactive.png)

<span data-ttu-id="5a0f1-173">**Nicht dynamische Webparts** sind nicht vollständig clientseitig, und in der Regel muss mindestens eine Eigenschaft einen Aufruf ausführen, um Daten auf einem Server festzulegen/abzurufen oder zu speichern.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-173">Nonreactive web parts are not fully client-side; generally, one or more properties need to make a call to set/pull or store data on a server.</span></span> <span data-ttu-id="5a0f1-174">In diesem Fall sollten Sie die Schaltflächen „Übernehmen“ und „Abbrechen“ am unteren Rand des Eigenschaftenbereich aktivieren.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-174">In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span>

![Nicht dynamisches Webpartdesign](../../../images/design-wp-pp-non-reactive.png)

## <a name="constructing-the-to-do-list-property-pane"></a><span data-ttu-id="5a0f1-176">Erstellen des Aufgabenlisten-Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="5a0f1-176">Constructing the To-Do List property pane</span></span>

<span data-ttu-id="5a0f1-177">Das Beispiel der Aufgabenliste verwendet den einzelnen Eigenschaftenbereich, und es handelt sich um ein dynamisches Webpart.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-177">The To-Do List example uses the single pane and is a reactive web part. The following shows each Fabric React component and the resulting design.</span></span> <span data-ttu-id="5a0f1-178">In den folgenden Diagrammen ist eine React-Komponente von Fabric und das daraus resultierende Design dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-178">The following diagrams show each Fabric React component and the resulting design.</span></span>

#### <a name="adding-a-description-for-to-do-list"></a><span data-ttu-id="5a0f1-179">Hinzufügen einer Beschreibung für die Aufgabenliste</span><span class="sxs-lookup"><span data-stu-id="5a0f1-179">Adding a description for To-Do List Adding a description for To-Do List</span></span>

![Hinzufügen einer Beschreibung für die Aufgabenliste](../../../images/design-wp-todo-pp-description.png)

#### <a name="dropdown--to-select-tasks-from-an-existing-list"></a><span data-ttu-id="5a0f1-181">Dropdown – Zum Auswählen von Aufgaben aus einer vorhandenen Liste</span><span class="sxs-lookup"><span data-stu-id="5a0f1-181">Dropdown – to select tasks from an existing list</span></span>

![Dropdown zum Auswählen von Aufgaben aus einer vorhandenen Liste](../../../images/design-wp-todo-pp-dropdown.png)

#### <a name="check-box--to-allow-authors-to-show-or-hide-different-views"></a><span data-ttu-id="5a0f1-183">Kontrollkästchen – Ermöglicht Autoren, unterschiedliche Ansichten anzuzeigen oder auszublenden</span><span class="sxs-lookup"><span data-stu-id="5a0f1-183">Check box – to allow authors to show or hide different views</span></span>

![Kontrollkästchen, um Autoren zu ermöglichen, unterschiedliche Ansichten anzuzeigen oder auszublenden](../../../images/design-wp-todo-pp-checkbox.png)

#### <a name="slider--to-set-the-number-of-tasks-visible"></a><span data-ttu-id="5a0f1-185">Schieberegler – Zum Festlegen der Anzahl sichtbarer Aufgaben</span><span class="sxs-lookup"><span data-stu-id="5a0f1-185">Slider – to set the number of tasks visible Slider to set the number of tasks visible</span></span>

![Schieberegler zum Anzeigen der Anzahl sichtbarer Aufgaben](../../../images/design-wp-todo-pp-slider.png)

#### <a name="after-selecting-a-list-from-the-dropdown-the-web-part-shows-an-indicator-of-items-loading-onto-the-page"></a><span data-ttu-id="5a0f1-187">Nach dem Auswählen einer Liste aus dem Dropdown zeigt das Webpart einen Indikator für Elemente an, die auf der Seite geladen werden.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-187">After selecting a list from the drop down the web part shows and indicator of items loading onto the page Web part showing loading indicator to load items</span></span>

![Webpart, das einen Indikator für Elemente anzeigt, die geladen werden](../../../images/design-wp-todo-loading-indicator.png)

#### <a name="when-the-new-tasks-are-loaded-they-fade-into-view-by-using-animation-styles-from-office-ui-fabric"></a><span data-ttu-id="5a0f1-189">Sobald die neuen Aufgaben geladen wurden, werden sie mithilfe von Animationsstilen aus Office UI Fabric eingeblendet.</span><span class="sxs-lookup"><span data-stu-id="5a0f1-189">When the new tasks are loaded, they fade into view using animation components from Office UI Fabric.</span></span>

![Webpart mit Fabric-Animationen](../../../images/design-wp-todo-fabric-animations.png)

## <a name="see-also"></a><span data-ttu-id="5a0f1-191">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="5a0f1-191">See also</span></span>

- [<span data-ttu-id="5a0f1-192">Entwerfen eines SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="5a0f1-192">Designing a SharePoint web part</span></span>](../../../design/design-a-web-part.md)
- [<span data-ttu-id="5a0f1-193">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="5a0f1-193">Designing great SharePoint experiences</span></span>](../../../design/design-guidance-overview.md)
