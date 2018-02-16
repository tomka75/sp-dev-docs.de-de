---
title: "Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen"
description: "Mit CSS können Sie das Aussehen und das Verhalten von SharePoint-Framework-Anpassungen definieren."
ms.date: 1/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 38d74b4a84187b16a3085354a6dda19b60e2eb56
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a><span data-ttu-id="d0e72-103">Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen</span><span class="sxs-lookup"><span data-stu-id="d0e72-103">Recommendations for working with CSS in SharePoint Framework solutions</span></span>

<span data-ttu-id="d0e72-104">Bei der Erstellung von SharePoint-Framework-Lösungen können Sie mithilfe von CSS definieren, wie Ihre Anpassungen aussehen und wie sie sich verhalten sollen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-104">When building SharePoint Framework solutions, you can use CSS to define how your customization should look and behave.</span></span> <span data-ttu-id="d0e72-105">In diesem Artikel wird beschrieben, wie Sie die vom SharePoint-Framework bereitgestellten Funktionen optimal nutzen und stabile CSS-Formatvorlagen erstellen können.</span><span class="sxs-lookup"><span data-stu-id="d0e72-105">When building SharePoint Framework solutions, you can use CSS to define how your customization should look like and behave. This article describes how you can make the best use of the capabilities provided with the SharePoint Framework and build your CSS styles in a robust way.</span></span>

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a><span data-ttu-id="d0e72-106">SharePoint-Framework-Anpassungen als Teil der Seite</span><span class="sxs-lookup"><span data-stu-id="d0e72-106">SharePoint Framework customizations are part of the page</span></span>

<span data-ttu-id="d0e72-107">Wenn Sie SharePoint-Anpassungen mithilfe des Add-In-Modells erstellen, ist Ihre Lösung von anderen Elementen auf der Seite isoliert.</span><span class="sxs-lookup"><span data-stu-id="d0e72-107">When building SharePoint customizations using the add-in model, the solution is isolated from other elements on the page.</span></span> <span data-ttu-id="d0e72-108">Ihr Code kann als Add-In-Webpart in einem iFrame ausgeführt werden oder als immersive Anwendung, von der die gesamte Seite gesteuert wird.</span><span class="sxs-lookup"><span data-stu-id="d0e72-108">Your code can be executed in an iframe as an add-in part, or as an immersive application that takes control of the whole page.</span></span> <span data-ttu-id="d0e72-109">In beiden Fällen haben andere Elemente und Formatvorlagen, die auf der Seite definiert sind, keine Auswirkungen auf den Code.</span><span class="sxs-lookup"><span data-stu-id="d0e72-109">In both cases, your code is not affected by other elements and styles defined on the page.</span></span>

<span data-ttu-id="d0e72-110">SharePoint-Framework-Lösungen sind Teil der Seite und vollständig in das DOM der Seite integriert.</span><span class="sxs-lookup"><span data-stu-id="d0e72-110">SharePoint Framework solutions are a part of the page and integrate fully with the page's DOM.</span></span> <span data-ttu-id="d0e72-111">Dadurch fallen zwar verschiedene Einschränkungen des Add-In-Modells weg, es entstehen jedoch auch Risiken für die Lösung.</span><span class="sxs-lookup"><span data-stu-id="d0e72-111">While this removes a number of restrictions that come with the add-in model, it exposes your solution to risk.</span></span> <span data-ttu-id="d0e72-112">Da sie Teil der Seite ist, gilt: Solange Sie die Lösung nicht explizit isolieren, werden sämtliche auf der Seite definierten CSS-Vorlagen auf sie angewendet. Das kann dazu führen, dass die Oberfläche anders aussieht als von Ihnen vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-112">Because it's a part of the page, unless explicitly isolated, all CSS styles present on the page apply to it, potentially resulting in an experience different from what you intended.</span></span> <span data-ttu-id="d0e72-113">Um das zu vermeiden, sollten Sie Ihre CSS-Formatvorlagen so definieren, dass sie sich ausschließlich auf Ihre Anpassung auswirken, nicht jedoch auf andere Seitenelemente.</span><span class="sxs-lookup"><span data-stu-id="d0e72-113">To avoid such risks, you should define your CSS styles in such a way so that they won't affect anything else on the page other than your customization.</span></span>

## <a name="organize-css-files-in-your-solution"></a><span data-ttu-id="d0e72-114">Organisieren von CSS-Dateien in Ihrer Lösung</span><span class="sxs-lookup"><span data-stu-id="d0e72-114">Organize CSS files in your solution</span></span>

<span data-ttu-id="d0e72-115">Oft besteht die Benutzeroberfläche einer Lösung aus mehreren Bausteinen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-115">The UI of your solutions often consists of multiple building blocks.</span></span> <span data-ttu-id="d0e72-116">In vielen JavaScript-Bibliotheken werden diese Bausteine als Komponenten bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="d0e72-116">In many JavaScript libraries, these building blocks are called components.</span></span> <span data-ttu-id="d0e72-117">Eine Komponente kann einfach sein und nur die Darstellungsweise definieren, oder sie kann komplexer sein und sowohl den Status als auch andere Komponenten enthalten.</span><span class="sxs-lookup"><span data-stu-id="d0e72-117">A component can be simple and define only the presentation, or it can be more complex and include state and other components.</span></span> <span data-ttu-id="d0e72-118">Wenn Sie Ihre Lösung in mehrere Komponenten unterteilen, vereinfacht das den Entwicklungsprozess und macht es leichter, die Komponenten zu testen und in Ihrer Lösung wiederzuverwenden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-118">Splitting your solution into multiple components allows you to simplify the development process and makes it easier to test and reuse the components in your solution.</span></span>

<span data-ttu-id="d0e72-119">Da Komponenten visuell dargestellt werden, sind für sie oftmals CSS-Formatvorlagen erforderlich.</span><span class="sxs-lookup"><span data-stu-id="d0e72-119">Because components have presentation, they often require CSS styles.</span></span> <span data-ttu-id="d0e72-120">Im Idealfall sollten Komponenten isoliert werden und eigenständig nutzbar sein.</span><span class="sxs-lookup"><span data-stu-id="d0e72-120">Ideally, components should be isolated and be able to be used on their own.</span></span> <span data-ttu-id="d0e72-121">Um das zu erreichen, ist es sinnvoll, die CSS-Formatvorlagen einer Komponente zusammen mit allen anderen Objektdateien der Komponente zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d0e72-121">With that in mind, it makes perfect sense for you to store CSS styles for the particular component along with all other asset files next to the component.</span></span> <span data-ttu-id="d0e72-122">Unten sehen Sie eine Beispielstruktur einer React-Anwendung mit verschiedenen Komponenten, die jeweils eine eigene CSS-Datei haben.</span><span class="sxs-lookup"><span data-stu-id="d0e72-122">Following is a sample structure of a React application with a number of components, each with its own CSS file.</span></span>

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a><span data-ttu-id="d0e72-123">Verwenden von Sass</span><span class="sxs-lookup"><span data-stu-id="d0e72-123">Use Sass</span></span>

<span data-ttu-id="d0e72-124">Im SharePoint-Framework können Sie sowohl CSS als auch Sass verwenden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-124">In SharePoint Framework, you can use both CSS and Sass.</span></span> <span data-ttu-id="d0e72-125">Sass ist eine CSS übergeordnete Sprache und bietet eine Reihe von Funktionen, die die Arbeit mit und die Verwaltung von CSS-Formatvorlagen langfristig einfacher machen. Zu diesen Funktionen gehören beispielsweise Variablen, Schachtelungsselektoren und Mixins.</span><span class="sxs-lookup"><span data-stu-id="d0e72-125">Sass is a superset of CSS and offers you a number of features such as variables, nesting selectors, or mixins, all of which simplify working with and managing CSS styles over the long term.</span></span> 

<span data-ttu-id="d0e72-126">Eine umfassende Übersicht über alle Funktionen finden Sie auf der [Sass-Website](http://sass-lang.com).</span><span class="sxs-lookup"><span data-stu-id="d0e72-126">For a complete set of features, see the [Sass website](http://sass-lang.com).</span></span> <span data-ttu-id="d0e72-127">Jeder gültige CSS-Code ist auch gültiger Sass-Code. Das ist sehr nützlich, falls Sie bisher noch nicht mit Sass gearbeitet haben und sich Schritt für Schritt mit den Funktionen der Sprache vertraut machen möchten.</span><span class="sxs-lookup"><span data-stu-id="d0e72-127">All valid CSS is also valid Sass, which is very helpful if you haven't worked with Sass before and want to gradually learn its capabilities.</span></span>

## <a name="avoid-using-ids-in-markup"></a><span data-ttu-id="d0e72-128">Vermeiden der Verwendung von IDs im Markup</span><span class="sxs-lookup"><span data-stu-id="d0e72-128">Avoid using ID's in markup</span></span>

<span data-ttu-id="d0e72-129">Wenn Sie mit dem SharePoint-Framework arbeiten, erstellen Sie Anpassungen, die Endbenutzer SharePoint hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-129">Using SharePoint Framework, you build customizations that end-users add to SharePoint.</span></span> <span data-ttu-id="d0e72-130">Vorab lässt sich unmöglich voraussehen, ob auf einer Seite nur eine einzige Instanz einer Anpassung implementiert wird oder ob mehrere Instanzen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-130">It's impossible to tell upfront if the particular customization is used only once on a page or if there are multiple instances of it.</span></span> 

<span data-ttu-id="d0e72-131">Um Probleme zu vermeiden, sollten Sie immer davon ausgehen, dass auf einer Seite mehrere Instanzen Ihrer Anpassung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-131">To avoid issues, you should always assume that there are multiple instances of your customization on the same page.</span></span> <span data-ttu-id="d0e72-132">Daher sollten Sie keine IDs in Ihrem Markup verwenden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-132">With that in mind, you should avoid using any IDs in your markup.</span></span> <span data-ttu-id="d0e72-133">IDs müssen auf einer Seite immer eindeutig sein; fügt ein Benutzer zwei Instanzen Ihres Webparts zu einer Seite hinzu, wird damit gegen diese Vorgabe verstoßen, und es kann zu Fehlern kommen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-133">IDs are meant to be unique on a page, and if a user adds your web part to the page twice, it violates this premise, possibly leading to errors.</span></span>

#### <a name="bad-practice"></a><span data-ttu-id="d0e72-134">Nicht zu empfehlen:</span><span class="sxs-lookup"><span data-stu-id="d0e72-134">Bad practice:</span></span>

```typescript
// ...

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {

  public render(): void {
    this.domElement.innerHTML = `
      <div id="helloWorld">
        Hello world
      </div>`;
  }

  // ...
}
```

<br/>

#### <a name="good-practice"></a><span data-ttu-id="d0e72-135">Zu empfehlen:</span><span class="sxs-lookup"><span data-stu-id="d0e72-135">Good practice:</span></span>

```typescript
// ...

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {

  public render(): void {
    this.domElement.innerHTML = `
      <div class="${styles.helloWorld}">
        Hello world
      </div>`;
  }

  // ...
}
```

## <a name="use-css-modules-to-avoid-styling-conflicts"></a><span data-ttu-id="d0e72-136">Verwenden von CSS-Modulen zur Vermeidung von Formatkonflikten</span><span class="sxs-lookup"><span data-stu-id="d0e72-136">Use CSS modules to avoid styling conflicts</span></span>

<span data-ttu-id="d0e72-p110">SharePoint Framework-Lösungen sind Teil der Seite. Um sicherzustellen, dass CSS-Formatvorlagen für eine Komponente keine Auswirkungen auf andere Elemente auf der Seite haben, sollten Sie Ihre CSS-Selektoren so verwenden, dass sie nur für das DOM Ihrer Lösung gelten. Bei manueller Ausführung ist dies mühsam und fehleranfällig, in SharePoint Framework kann dies jedoch automatisch ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-p110">SharePoint Framework solutions are a part of the page. To ensure that CSS styles for one component don't affect other elements on the page, you should define your CSS selectors in such a way that they apply only to the DOM of your solution. It's tedious and error-prone to do this manually, but SharePoint Framework can do this automatically for you.</span></span>

<span data-ttu-id="d0e72-140">Das SharePoint-Framework verwendet [CSS-Module](https://github.com/css-modules/css-modules), um Formatkonflikte zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-140">To help you avoid styling conflicts, SharePoint Framework uses [CSS modules](https://github.com/css-modules/css-modules).</span></span> <span data-ttu-id="d0e72-141">Wenn Sie ein Projekt erstellen, verarbeitet die SharePoint-Framework-Toolkette alle Dateien mit der Dateiendung **.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="d0e72-141">When building the project, the SharePoint Framework toolchain processes all files with the **.module.scss** extension.</span></span> <span data-ttu-id="d0e72-142">Sie liest die Klassenselektoren jeder Datei und fügt ihnen jeweils einen eindeutigen Hashwert an.</span><span class="sxs-lookup"><span data-stu-id="d0e72-142">For each file, it reads all class selectors and appends a unique hash value to them.</span></span> <span data-ttu-id="d0e72-143">Anschließend werden die aktualisierten Selektoren in CSS-Zwischendateien geschrieben, die in das generierte Webpartpaket gepackt werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-143">After it's finished, it writes the updated selectors to intermediate CSS files that are included in the generated web part bundle.</span></span>

<span data-ttu-id="d0e72-144">Nehmen wir das oben angeführte Beispiel, und gehen wir davon aus, wir arbeiten mit den folgenden beiden Sass-Dateien:</span><span class="sxs-lookup"><span data-stu-id="d0e72-144">Following the example above, assume you had the following two Sass files:</span></span>

#### <a name="todolistmodulescss"></a><span data-ttu-id="d0e72-145">todoList.module.scss</span><span class="sxs-lookup"><span data-stu-id="d0e72-145">todoList.module.scss:</span></span>

```scss
.todoList {
  margin: 1em 0;

  .text {
    font-weight: bold;
    font-size: 1.5em;
  }
}
```

<br/>

#### <a name="todoitemmodulescss"></a><span data-ttu-id="d0e72-146">todoItem.module.scss</span><span class="sxs-lookup"><span data-stu-id="d0e72-146">todoItem.module.scss:</span></span>

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<br/>

<span data-ttu-id="d0e72-147">Nach dem Erstellen des Projekts würden Sie im Ordner **lib** die folgenden beiden generierten CSS-Dateien sehen (Zeilenumbrüche und Einzüge wurden zur besseren Lesbarkeit hinzugefügt):</span><span class="sxs-lookup"><span data-stu-id="d0e72-147">After building the project, in the **lib** folder you would see the following two CSS files generated (line breaks and indenting added for readability):</span></span>

#### <a name="todolistmodulecss"></a><span data-ttu-id="d0e72-148">todoList.module.css</span><span class="sxs-lookup"><span data-stu-id="d0e72-148">todoList.module.css:</span></span>

```css
.todoList_3e9d35f0 {
  margin:1em 0
}

.todoList_3e9d35f0 .text_3e9d35f0 {
  font-weight:700;
  font-size:1.5em
}
```

<br/>

#### <a name="todoitemmodulecss"></a><span data-ttu-id="d0e72-149">todoItem.module.css</span><span class="sxs-lookup"><span data-stu-id="d0e72-149">todoItem.module.css:</span></span>

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<br/>

<span data-ttu-id="d0e72-150">Obwohl eine **.text**-Klasse in beiden Sass-Dateien definiert wurde, werden Sie feststellen, dass in den generierten CSS-Dateien zwei Hashes angefügt wurden, sodass ein eindeutiger Klassenname entsteht, der für jede Komponente spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="d0e72-150">Even though there was a **.text** class defined in both Sass files, notice how in the generated CSS files it has two different hashes appended to it, becoming a unique class name specific to each component.</span></span>

<span data-ttu-id="d0e72-p112">Die CSS-Klassennamen in CSS-Modulen werden dynamisch generiert, sodass Sie nicht direkt im Code auf diese verweisen können. Stattdessen generiert die SharePoint Framework-Toolkette beim Verarbeiten von CSS-Modulen eine JavaScript-Datei mit Verweisen auf die generierten Klassennamen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-p112">The CSS class names in CSS modules are generated dynamically, which makes it impossible for you to refer to them in your code directly. Instead, when processing CSS modules, the SharePoint Framework toolchain generates a JavaScript file with references to the generated class names.</span></span>

#### <a name="todolistmodulescssjs"></a><span data-ttu-id="d0e72-153">todoList.module.scss.js</span><span class="sxs-lookup"><span data-stu-id="d0e72-153">todoList.module.scss.js:</span></span>

```js
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
/* tslint:disable */
require('./todoList.module.css');
var styles = {
    todoList: 'todoList_3e9d35f0',
    text: 'text_3e9d35f0',
};
exports.default = styles;
/* tslint:enable */

//# sourceMappingURL=todoList.module.scss.js.map
```

<br/>

<span data-ttu-id="d0e72-154">Um die generierten Klassennamen in Ihrem Code verwenden zu können, müssen Sie zunächst die Formatvorlagen Ihrer Komponente importieren. Anschließend verwenden Sie die Eigenschaft, die auf die betreffende Klasse zeigt:</span><span class="sxs-lookup"><span data-stu-id="d0e72-154">To use the generated class names in your code, you first import the styles of your component and then use the property pointing to the particular class:</span></span>

```typescript
import styles from './todoList.module.scss';
// ...

export default class TodoList extends React.Component<ITodoListProps, void> {
  public render(): React.ReactElement<ITodoListProps> {
    return (
      <div className={styles.todoList}>
        <div className={styles.text}>Hello world</div>
      </div>
    );
  }
}
```

<br/>

<span data-ttu-id="d0e72-155">Damit die CSS-Module korrekt funktionieren, müssen die folgenden Bedingungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="d0e72-155">For the CSS modules to work correctly you have to meet the following conditions:</span></span>

* <span data-ttu-id="d0e72-156">Ihre Sass-Dateien müssen die Dateiendung **.module.scss** haben.</span><span class="sxs-lookup"><span data-stu-id="d0e72-156">Your Sass files must have the **.module.scss** extension.</span></span> <span data-ttu-id="d0e72-157">Wenn Sie die Dateiendung **.scss** ohne **.module** verwenden, wird während des Erstellungsprozesses eine Warnmeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d0e72-157">If you use the **.scss** extension without **.module**, you see a warning in the build process.</span></span> <span data-ttu-id="d0e72-158">Die Sass-Datei wird in eine CSS-Zwischendatei transpiliert, wobei die Klassennamen jedoch *nicht eindeutig gemacht werden*.</span><span class="sxs-lookup"><span data-stu-id="d0e72-158">The Sass file is transpiled to an intermediate CSS file, but the class names *will not be made unique*.</span></span> <span data-ttu-id="d0e72-159">Falls Sie CSS-Formatvorlagen von Drittanbietern überschreiben müssen, ist dies möglicherweise gewollt.</span><span class="sxs-lookup"><span data-stu-id="d0e72-159">In cases when you need to override third-party CSS styles, this might be intended.</span></span>

* <span data-ttu-id="d0e72-160">Alle CSS-Klassennamen müssen gültige JavaScript-Variablennamen sein.</span><span class="sxs-lookup"><span data-stu-id="d0e72-160">Your CSS class names must be valid JavaScript variable names.</span></span> <span data-ttu-id="d0e72-161">Sie dürfen beispielsweise keine Bindestriche enthalten: `todoList` ist korrekt, `todo-list` jedoch nicht.</span><span class="sxs-lookup"><span data-stu-id="d0e72-161">For example, they cannot contain hyphens: `todoList` is correct, but `todo-list` isn't.</span></span>

* <span data-ttu-id="d0e72-162">Wir empfehlen die CamelCase-Notation für die Benennung von Klassen. Obligatorisch ist die Verwendung dieser Notation jedoch nicht.</span><span class="sxs-lookup"><span data-stu-id="d0e72-162">camelCase naming for classes is recommended, but it's not enforced</span></span>

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a><span data-ttu-id="d0e72-163">Einbetten von CSS-Formatvorlagen in eine nach der Komponente benannten Klasse</span><span class="sxs-lookup"><span data-stu-id="d0e72-163">Wrap your CSS styles in a class named after the component</span></span>

<span data-ttu-id="d0e72-164">Wenn Sie CSS-Module und die Sass-Unterstützung für die Schachtelung von Regelsätzen miteinander kombinieren, können Sie Ihre CSS-Formatvorlagen vereinfachen und sicherstellen, dass sie keine Auswirkungen auf andere Seitenelemente haben.</span><span class="sxs-lookup"><span data-stu-id="d0e72-164">By combining CSS modules with Sass' support for nesting rule sets you can simplify your CSS styles and ensure that they won't affect other elements on the page.</span></span>

<span data-ttu-id="d0e72-165">Betten Sie dazu die CSS-Formatvorlagen Ihrer Komponente bei der Erstellung in eine Klasse ein, die nach der Komponente benannt ist.</span><span class="sxs-lookup"><span data-stu-id="d0e72-165">When building CSS styles for a component, wrap them in a class named after the component. Then, in the component, assign that class to the component's root element.</span></span> <span data-ttu-id="d0e72-166">In der Komponente selbst muss die Klasse dem Stammelement der Komponente zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-166">In the component, assign that class to the component's root element.</span></span>

#### <a name="todolistmodulescss"></a><span data-ttu-id="d0e72-167">todoList.module.scss</span><span class="sxs-lookup"><span data-stu-id="d0e72-167">todoList.module.scss:</span></span>

```scss
.todoList {
  a {
    display: block;
  }
}
```

<br/>

#### <a name="todolisttsx"></a><span data-ttu-id="d0e72-168">TodoList.tsx</span><span class="sxs-lookup"><span data-stu-id="d0e72-168">TodoList.tsx:</span></span>

```tsx
// ...

export default class TodoList extends React.Component<ITodoListProps, void> {
  public render(): React.ReactElement<ITodoListProps> {
    return (
      <div className={styles.todoList}>
        ...
      </div>
    );
  }
}
```

<br/>

<span data-ttu-id="d0e72-169">Nach der Transpilierung sieht die generierte CSS-Datei in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="d0e72-169">After transpilation, the generated CSS file will look similar to:</span></span>

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

<span data-ttu-id="d0e72-170">Da der Selektor mit dem eindeutigen Klassennamen beginnt, der spezifisch für die Komponente ist, gilt die alternative Darstellung nur für Links innerhalb der Komponente.</span><span class="sxs-lookup"><span data-stu-id="d0e72-170">Because the selector begins with the unique class name, specific to your component, the alternative presentation will apply only to hyperlinks inside your component.</span></span>

## <a name="handling-of-css-vendor-prefix"></a><span data-ttu-id="d0e72-171">Verarbeiten von CSS-Anbieterpräfixen</span><span class="sxs-lookup"><span data-stu-id="d0e72-171">Handling of CSS vendor prefix</span></span>

<span data-ttu-id="d0e72-172">Im SharePoint-Framework müssen in den Sass- oder CSS-Dateien von Projekten nicht zwingend Formateigenschaften mit Anbieterpräfix verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-172">In SPFx no vendor prefixed style properties are required in the SASS or CSS files of a project.</span></span> <span data-ttu-id="d0e72-173">Für den Fall, dass einige der vom SharePoint-Framework unterstützten Browser Präfixe fordern, werden diese automatisch nach der Kompilierung von Sass zu CSS hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0e72-173">If some of the SPFx supported browsers require prefixes they were added after the SASS to CSS compilation automatically.</span></span> <span data-ttu-id="d0e72-174">Diese Methode wird auch als automatische Voranstellung von Präfixen (Prefixing) bezeichnet und ist grundlegender Bestandteil der CSS-Buildkette im SharePoint-Framework.</span><span class="sxs-lookup"><span data-stu-id="d0e72-174">This method is also known as auto-prefixing and is a fundamental part of the CSS build chain in SPFx.</span></span>

<span data-ttu-id="d0e72-175">Falls Ihr Webpart das neue Flex-Box-Modell verwendet (definiert durch die Deklaration `display: flex`), erfordern einige ältere WebKit-basierte Browser und Internet Explorer-Versionen einen bestimmten Anbieterpräfix im CSS-Code.</span><span class="sxs-lookup"><span data-stu-id="d0e72-175">In case a web part should use the new flex box model defined by the `display: flex` declaration, some older WebKit-based and Internet Explorer versions require a particular vendor prefix defined in the CSS.</span></span>

```css
.container{
  display: flex;
}
```

<br/>

<span data-ttu-id="d0e72-176">Der Sass-Code des SharePoint-Framework-Artefakts muss keine Anbieterpräfixes enthalten.</span><span class="sxs-lookup"><span data-stu-id="d0e72-176">In the SASS code of the SPFx artefact does not need to have vendor prefixes included.</span></span> <span data-ttu-id="d0e72-177">Nach der Kompilierung von Sass zu CSS werden diese automatisch hinzugefügt, sodass die CSS-Deklaration wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="d0e72-177">After the SASS-to-CSS compilation, those were added automatically resulting in the following CSS declaration.</span></span>

```css
.container_7e976ae1 {
  display: -webkit-box; // older Safari on MacOS and iOS
  display: -ms-flexbox; // IE 10 - 11
  display: flex;
}
```

<br/>

<span data-ttu-id="d0e72-178">Durch das Entfernen bereits angewendeter Präfixe wird der Artefaktcode nicht nur übersichtlicher, sondern auch einfacher lesbar und zukunftssicherer.</span><span class="sxs-lookup"><span data-stu-id="d0e72-178">Removing already applied prefixes does not only make the code of the artefact cleaner, it also makes it easier to read and future-ready.</span></span> <span data-ttu-id="d0e72-179">Darüber hinaus ist dieser Prozess so konfiguriert, dass nur vom SharePoint-Framework unterstützte Browser unterstützt werden. Das sichert effektiver gegen Fehler ab.</span><span class="sxs-lookup"><span data-stu-id="d0e72-179">This process is also configured to support only SharePoint Framework-supported browsers and makes it more error-safe.</span></span>

<span data-ttu-id="d0e72-180">Falls die Sass-Dateien eines Webparts bereits Anbieterpräfixe enthalten, die nicht mehr benötigt werden, werden diese Deklarationen über denselben Prozess automatisch entfernt.</span><span class="sxs-lookup"><span data-stu-id="d0e72-180">In case a web part already has vendor prefixes included in the SASS files that are not needed anymore the same process removes those declarations automatically.</span></span>

<span data-ttu-id="d0e72-181">Im nachfolgenden Beispiel wird die Eigenschaft `border-radius` verwendet, die keine Anbieterpräfixe auf den unterstützten Systemen erfordert.</span><span class="sxs-lookup"><span data-stu-id="d0e72-181">The following example makes use of the `border-radius` property, which does not require vendor prefixes on the supported systems.</span></span>

```css
.container {
  /* Safari 3-4, iOS 1-3.2, Android 1.6- */
  -webkit-border-radius: 7px;
  /* Firefox 1-3.6 */
  -moz-border-radius: 7px;
  /* Opera 10.5, IE 9, Safari 5, Chrome, Firefox 4, iOS 4, Android 2.1+ */
  border-radius: 7px;
}
```

<br/>

<span data-ttu-id="d0e72-182">Der resultierende CSS-Code im Paket wird in den folgenden Code umgewandelt:</span><span class="sxs-lookup"><span data-stu-id="d0e72-182">The resulting CSS in the package will be converted to the following code.</span></span>

```css
.container_9e54c0b0 {
  border-radius: 7px
}
```

<span data-ttu-id="d0e72-183">Weitere Informationen zum automatischen Prefixing finden Sie im GitHub-Repository [autoprefixer](https://github.com/postcss/autoprefixer).</span><span class="sxs-lookup"><span data-stu-id="d0e72-183">For more information about auto-prefixing, see the [autoprefixer](https://github.com/postcss/autoprefixer) GitHub repository.</span></span> <span data-ttu-id="d0e72-184">Die Datenbank für diesen Prozess ist auf [Can I use__?](https://caniuse.com) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d0e72-184">The database for this process is available on [Can I use__?](https://caniuse.com).</span></span>

## <a name="integrate-office-ui-fabric"></a><span data-ttu-id="d0e72-185">Integrieren von Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="d0e72-185">Integrate Office UI Fabric</span></span>

<span data-ttu-id="d0e72-186">Wenn Sie Ihre Anpassung so gestalten, dass sie in puncto Aussehen und Verhalten den Standardfunktionen von SharePoint und Office 365 entspricht, machen Sie es Endbenutzern einfacher, mit ihr zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="d0e72-186">By making your customizations look and behave like the standard functionality of SharePoint and Office 365 you will make it easier for the end-users to work with them.</span></span> <span data-ttu-id="d0e72-187">Office UI Fabric bietet eine Reihe von Steuerelementen und Formatvorlagen für Anpassungen, mit denen eine nahtlose Integration in die vorhandene Benutzeroberfläche möglich ist.</span><span class="sxs-lookup"><span data-stu-id="d0e72-187">Office UI Fabric offers you a set of controls and styles for use in your customizations to seamlessly integrate with the existing user experience.</span></span> 

<span data-ttu-id="d0e72-188">Weitere Informationen zur Verwendung von Office UI Fabric im SharePoint-Framework finden Sie unter [Verwenden von Office UI Fabric Core und Fabric React im SharePoint-Framework](./office-ui-fabric-integration.md).</span><span class="sxs-lookup"><span data-stu-id="d0e72-188">For more information about using Office UI Fabric in SharePoint Framework, see [Using Office UI Fabric Core and Fabric React in SharePoint Framework](./office-ui-fabric-integration.md).</span></span>

## <a name="use-theme-colors"></a><span data-ttu-id="d0e72-189">Verwenden von Farbdesigns</span><span class="sxs-lookup"><span data-stu-id="d0e72-189">Use theme colors</span></span>

<span data-ttu-id="d0e72-190">SharePoint ermöglicht es Benutzern, ein Farbdesign für ihre Website auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="d0e72-190">SharePoint allows users to choose the theme color for their sites.</span></span> <span data-ttu-id="d0e72-191">Damit Ihre SharePoint-Framework-Anpassung wie ein integraler Bestandteil der Website aussieht und nicht unnötig heraussticht, sollte sie jeweils das vom Benutzer ausgewählte Design verwenden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-191">In your SharePoint Framework customizations, you should follow the theme selected by the users to make your customization look like an integral part of the site rather than unnecessarily stand out.</span></span> 

<span data-ttu-id="d0e72-192">Da die Benutzer selbst das Design für eine Website festlegen, wissen Sie vorab nicht, welche Farben Ihre Anpassung verwenden sollte. Das SharePoint-Framework kann das aktuell aktive Farbdesign jedoch automatisch dynamisch für Sie laden.</span><span class="sxs-lookup"><span data-stu-id="d0e72-192">Because the theme is set by users on their site, you cannot tell upfront which colors your customization should use, but SharePoint Framework can dynamically load the currently active color scheme automatically for you.</span></span> 

<span data-ttu-id="d0e72-193">Weitere Informationen zu dieser Funktion finden Sie unter [Verwenden von Designfarben in Ihren SharePoint-Framework-Anpassungen](./use-theme-colors-in-your-customizations.md).</span><span class="sxs-lookup"><span data-stu-id="d0e72-193">For more information about this capability, see [Use theme colors in your SharePoint Framework customizations](./use-theme-colors-in-your-customizations.md).</span></span>




