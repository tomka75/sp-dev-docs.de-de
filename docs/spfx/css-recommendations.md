---
title: "Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c55b5362b4a1426c44cc0e7c53eacfe08982de64
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a><span data-ttu-id="aded6-102">Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen</span><span class="sxs-lookup"><span data-stu-id="aded6-102">Recommendations for working with CSS in SharePoint Framework solutions</span></span>

<span data-ttu-id="aded6-p101">Wenn Sie SharePoint-Framework Lösungen erstellen, können Sie CSS verwenden, um zu definieren, wie sich Ihre Anpassung verhalten und aussehen soll. In diesem Artikel wird beschrieben, wie Sie die mit dem SharePoint Framework bereitgestellten Funktionen am besten nutzen und Ihre CSS-Formatvorlagen stabil erstellen.</span><span class="sxs-lookup"><span data-stu-id="aded6-p101">When building SharePoint Framework solutions, you can use CSS to define how your customization should look like and behave. This article describes how you can make the best use of the capabilities provided with the SharePoint Framework and build your CSS styles in a robust way.</span></span>

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a><span data-ttu-id="aded6-105">SharePoint Framework-Anpassungen sind Teil der Seite</span><span class="sxs-lookup"><span data-stu-id="aded6-105">SharePoint Framework customizations are part of the page</span></span>

<span data-ttu-id="aded6-p102">Wenn Sie SharePoint-Anpassungen mit dem Add-In-Modell erstellen, ist die Lösung von anderen Elementen auf der Seite isoliert. Der Code wird entweder in einem Iframe, als Add-In-Bestandteil oder als immersive Anwendung ausgeführt, die die Kontrolle übe die gesamte Seite übernimmt. In beiden Fällen wird der Code nicht von anderen Elementen und Formatvorlagen beeinträchtigt, die auf der Seite definiert sind.</span><span class="sxs-lookup"><span data-stu-id="aded6-p102">When building SharePoint customizations using the add-in model, the solution is isolated from other elements on the page. Your code is executed either in an iframe, as an add-in part, or as an immersive application taking control of the whole page. In both cases, your code is not affected by other elements and styles defined on the page.</span></span>

<span data-ttu-id="aded6-p103">SharePoint Framework-Lösungen sind Teil der Seite und können vollständig in das DOM der Seite integriert werden. Dabei wird eine Reihe von Einschränkungen entfernt, die in dem Add-In-Modell enthalten sind, wodurch Ihre Lösung einem Risiko ausgesetzt wird. Da es sich um einen Teil der Seite handelt, gelten alle auf der Seite vorhandenen CSS-Formatvorlagen dafür, sofern diese nicht isoliert sind, was möglicherweise zu einer anderen Erfahrung als der beabsichtigten führt. Um derartige Risiken zu verhindern, sollten Sie Ihre CSS-Formatvorlagen so definieren, dass sie sich nicht auf andere Elemente auf der Seite, sondern nur auf die Anpassung auswirken.</span><span class="sxs-lookup"><span data-stu-id="aded6-p103">SharePoint Framework solutions are a part of the page and integrate fully with the page's DOM. While this removes a number of restrictions that come with the add-in model, it exposes your solution to a risk. Because it's a part of the page, unless explicitly isolated, all CSS styles present on the page will apply to it, potentially resulting in an experience different from intended. To avoid such risks, you should define your CSS styles in such a way so that they won't affect anything else on the page other than your customization.</span></span>

## <a name="organize-css-files-in-your-solution"></a><span data-ttu-id="aded6-113">Organisieren von CSS-Dateien in Ihrer Lösung</span><span class="sxs-lookup"><span data-stu-id="aded6-113">Organize CSS files in your solution</span></span>

<span data-ttu-id="aded6-p104">Die Benutzeroberfläche Ihrer Lösung besteht häufig aus mehreren Bausteinen. In vielen JavaScript-Bibliotheken werden diese Bausteine als Komponenten bezeichnet. Eine Komponente kann einfach sein und nur die Präsentation definieren, oder sie kann komplexer sein und den Status sowie andere Komponenten umfassen. Durch Aufteilen der Lösung in mehrere Komponenten können Sie den Entwicklungsprozess vereinfachen und das Testen und Wiederverwenden in Ihrer Lösung erleichtern.</span><span class="sxs-lookup"><span data-stu-id="aded6-p104">The UI of your solutions often consists of multiple building blocks. In many JavaScript libraries these building blocks are called components. A component can be simple and define only the presentation or it can be more complex and include state and other components. Splitting your solution into multiple components allows you to simplify the development process and makes them easier to test and reuse in your solution.</span></span>

<span data-ttu-id="aded6-p105">Da Komponenten über eine Präsentation verfügen, erfordern sie häufig CSS-Formatvorlagen. Im Idealfall sind Komponenten isoliert und können eigenständig verwendet werden. Angesichts dessen ist es sinnvoll, CSS-Formatvorlagen für die jeweilige Komponente mit allen anderen Ressourcendateien neben der Komponente zu speichern. Nachfolgend finden Sie eine Beispielstruktur einer React-Anwendung mit einer Reihe von Komponenten, die jeweils über ihre eigene CSS-Datei verfügen.</span><span class="sxs-lookup"><span data-stu-id="aded6-p105">Because components have presentation, they often require CSS styles. Ideally, components should be isolated and be able to be used on their own. With that in mind, it makes perfect sense for you to store CSS styles for the particular component along with all other asset files next to the component. Following, is a sample structure of a React application with a number of components each with its own CSS file.</span></span>

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a><span data-ttu-id="aded6-122">Verwenden von Sass</span><span class="sxs-lookup"><span data-stu-id="aded6-122">Use Sass</span></span>

<span data-ttu-id="aded6-p106">Im SharePoint-Framework können Sie sowohl CSS und Sass verwenden. Sass ist eine Obermenge von CSS und bietet Ihnen eine Reihe von Funktionen, z. B. das Verwenden von Variablen, das Verschachteln von Selektoren oder die Verwendung von Mixins, die alle das Arbeiten mit und das Verwalten von CSS-Formatvorlagen langfristig vereinfachen. Eine vollständigen Satz von Funktionen finden Sie auf der [Sass-Website](http://sass-lang.com). Gültige CSS ist ebenfalls gültige Sass, was sehr hilfreich ist, wenn Sie noch nicht mit Sass gearbeitet haben und sich an die Funktionen herantasten möchten.</span><span class="sxs-lookup"><span data-stu-id="aded6-p106">In the SharePoint Framework you can use both CSS and Sass. Sass is a superset of CSS and offers you a number of features such as using variables, nesting selectors or using mixins - all of which simplify working with and managing CSS styles over long term. For a complete set of features see the [Sass website](http://sass-lang.com). All valid CSS is also valid Sass which is very helpful if you haven't worked with Sass before and want to gradually learn its capabilities.</span></span>

## <a name="avoid-using-ids-in-markup"></a><span data-ttu-id="aded6-127">Vermeiden der Verwendung von IDs in Markup</span><span class="sxs-lookup"><span data-stu-id="aded6-127">Avoid using ID's in markup</span></span>

<span data-ttu-id="aded6-p107">Mithilfe von SharePoint Framework erstellen Sie Anpassungen, die Endbenutzer zu SharePoint hinzufügen. Es kann vorab festgestellt werden, ob die jeweilige Anpassung nur einmal auf einer Seite verwendet wird oder ob es mehrere Instanzen davon gibt. Um Probleme zu verhindern, sollten Sie immer davon ausgehen, dass es mehrere Instanzen Ihrer Anpassung auf derselben Seite gibt. Angesichts dieser Tatsache sollten Sie keine IDs in Ihrem Markup verwenden. IDs sollen auf einer Seite eindeutig sein, und wenn ein Benutzer Ihr Webpart der Seite zweimal hinzugefügt hat, würde dies einen Verstoß gegen diese Voraussetzung bedeuten, was zu Fehlern führen kann.</span><span class="sxs-lookup"><span data-stu-id="aded6-p107">Using the SharePoint Framework you build customizations that end-users add to SharePoint. It's impossible to tell upfront if the particular customization will be used only once on a page or if there will be multiple instances of it. To avoid issues, you should always assume that there are multiple instances of your customization on the same page. With that in mind, you should avoid using any ID's in your markup. ID's are meant to be unique on a page and if a user added your web part to the page twice, it would violate this premise possibly leading to errors.</span></span>

<span data-ttu-id="aded6-133">**Nicht zu empfehlen:**</span><span class="sxs-lookup"><span data-stu-id="aded6-133">**Bad practice:**</span></span>

```ts
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

<span data-ttu-id="aded6-134">**Zu empfehlen:**</span><span class="sxs-lookup"><span data-stu-id="aded6-134">**Good practice:**</span></span>

```ts
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

## <a name="use-css-modules-to-avoid-styling-conflicts"></a><span data-ttu-id="aded6-135">Verwenden von CSS-Modulen zur Vermeidung von Formatkonflikten</span><span class="sxs-lookup"><span data-stu-id="aded6-135">Use CSS modules to avoid styling conflicts</span></span>

<span data-ttu-id="aded6-p108">SharePoint Framework-Lösungen sind Teil der Seite. Um sicherzustellen, dass CSS-Formatvorlagen für eine Komponente keine Auswirkungen auf andere Elemente auf der Seite haben, sollten Sie Ihre CSS-Selektoren so verwenden, dass sie nur für das DOM Ihrer Lösung gelten. Bei manueller Ausführung ist dies mühsam und fehleranfällig, in SharePoint Framework kann dies jedoch automatisch ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="aded6-p108">SharePoint Framework solutions are a part of the page. To ensure that CSS styles for one component don't affect other elements on the page, you should define your CSS selectors in such a way that they apply only to the DOM of your solution. It's tedious and error-prone to do this manually, but SharePoint Framework can do this automatically for you.</span></span>

<span data-ttu-id="aded6-p109">Um Formatkonflikte zu vermeiden, verwendet SharePoint Framework [CSS-Module](https://github.com/css-modules/css-modules). Beim Erstellen des Projekts verarbeitet die SharePoint Framework-Toolkette alle Dateien mit der Erweiterung **. module.scss**. Alle Klassenselektoren werden für jede Datei gelesen und diesen wird ein eindeutiger Hashwert angefügt. Nach Abschluss werden die aktualisierten Selektoren in Zwischen-CSS-Dateien geschrieben, die im generierten Webpartpaket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="aded6-p109">To help you avoid stylings conflicts, SharePoint Framework uses [CSS modules](https://github.com/css-modules/css-modules). When building the project, the SharePoint Framework toolchain processes all files with the **.module.scss** extension. For each file, it reads all class selectors and appends a unique hash value to them. Once finished, it writes the updated selectors to intermediate CSS files that are included in the generated web part bundle.</span></span>

<span data-ttu-id="aded6-143">Gehen Sie gemäß dem obigen Beispiel davon aus, dass Sie über die beiden folgenden Sass-Dateien verfügen:</span><span class="sxs-lookup"><span data-stu-id="aded6-143">Following the example above, assume you had the following two Sass files:</span></span>

<span data-ttu-id="aded6-144">**todoList.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="aded6-144">**todoList.module.scss:**</span></span>

```scss
.todoList {
  margin: 1em 0;

  .text {
    font-weight: bold;
    font-size: 1.5em;
  }
}
```

<span data-ttu-id="aded6-145">**todoItem.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="aded6-145">**todoItem.module.scss:**</span></span>

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<span data-ttu-id="aded6-146">Nach dem Erstellen des Projekts würden Sie im Ordner **lib** die folgenden beiden generierten CSS-Dateien sehen (Zeilenumbrüche und Einzüge wurden zur besseren Lesbarkeit hinzugefügt):</span><span class="sxs-lookup"><span data-stu-id="aded6-146">After building the project, in the **lib** folder you would see the following two CSS files generated (line breaks and indenting added for readability):</span></span>

<span data-ttu-id="aded6-147">**todoList.module.css:**</span><span class="sxs-lookup"><span data-stu-id="aded6-147">**todoList.module.css:**</span></span>

```css
.todoList_3e9d35f0 {
  margin:1em 0
}

.todoList_3e9d35f0 .text_3e9d35f0 {
  font-weight:700;
  font-size:1.5em
}
```

<span data-ttu-id="aded6-148">**todoItem.module.css:**</span><span class="sxs-lookup"><span data-stu-id="aded6-148">**todoItem.module.css:**</span></span>

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<span data-ttu-id="aded6-149">Obwohl eine **.text**-Klasse in beiden Sass-Dateien definiert wurde, werden Sie feststellen, dass in den generierten CSS-Dateien zwei Hashes angefügt wurden, sodass ein eindeutiger Klassenname entsteht, der für jede Komponente spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="aded6-149">Even though there was a **.text** class defined in both Sass files, notice how in the generated CSS files it has two different hashes appended to it, becoming a unique class name specific to each component.</span></span>

<span data-ttu-id="aded6-p110">Die CSS-Klassennamen in CSS-Modulen werden dynamisch generiert, sodass Sie nicht direkt im Code auf diese verweisen können. Stattdessen generiert die SharePoint Framework-Toolkette beim Verarbeiten von CSS-Modulen eine JavaScript-Datei mit Verweisen auf die generierten Klassennamen.</span><span class="sxs-lookup"><span data-stu-id="aded6-p110">The CSS class names in CSS modules are generated dynamically, which makes it impossible for you to refer to them in your code directly. Instead, when processing CSS modules, the SharePoint Framework toolchain generates a JavaScript file with references to the generated class names.</span></span>

<span data-ttu-id="aded6-152">**todoList.module.scss.js:**</span><span class="sxs-lookup"><span data-stu-id="aded6-152">**todoList.module.scss.js:**</span></span>

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

<span data-ttu-id="aded6-153">Um die generierten Klassennamen in Ihrem Code zu verwenden, importieren Sie zunächst die Formatvorlagen Ihrer Komponente, und verwenden Sie dann die Eigenschaft, die auf die jeweilige Klasse zeigt:</span><span class="sxs-lookup"><span data-stu-id="aded6-153">To use the generated class names in your code, you first import the styles of your component and then use the property pointing to the particular class:</span></span>

```ts
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

<span data-ttu-id="aded6-154">Damit die CSS-Module ordnungsgemäß funktionieren, müssen Sie die folgenden Bedingungen erfüllen:</span><span class="sxs-lookup"><span data-stu-id="aded6-154">For the CSS modules to work correctly you have to meet the following conditions:</span></span>

* <span data-ttu-id="aded6-p111">Die Sass-Dateien müssen die Erweiterung **.module.scss** aufweisen. Wenn Sie die Erweiterung **.scss** ohne **.module** verwenden, wird beim Erstellungsprozess eine Warnung angezeigt. Die Sass-Datei wird in eine Zwischen-CSS-Datei übertragen, die Klassennamen **werden aber nicht eindeutig gemacht**. Dies kann in Fällen, in denen Sie CSS-Formatvorlagen von Drittanbietern außer Kraft setzen müssen, beabsichtigt sein.</span><span class="sxs-lookup"><span data-stu-id="aded6-p111">your Sass files must have the **.module.scss** extension. If you use the **.scss** extension without **.module**, you will see a warning in the build process. The Sass file will be transpiled to an intermediate CSS file but the class names **will not be made unique**. In cases, when you need to override 3rd party CSS styles, this might be intended</span></span>
* <span data-ttu-id="aded6-159">Die CSS-Klassennamen müssen gültige JavaScript-Variablennamen sein, sie dürfen also zum Beispiel keine Bindestriche enthalten: `todoList` ist richtig, `todo-list` jedoch nicht.</span><span class="sxs-lookup"><span data-stu-id="aded6-159">your CSS class names must be valid JavaScript variable names, so for example they cannot contain hyphens: `todoList` is correct but `todo-list` isn't</span></span>
* <span data-ttu-id="aded6-160">camelCase-Benennung für Klassen wird empfohlen, wird aber nicht erzwungen</span><span class="sxs-lookup"><span data-stu-id="aded6-160">camelCase naming for classes is recommended, but it's not enforced</span></span>

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a><span data-ttu-id="aded6-161">Verpacken Sie Ihre CSS-Formatvorlagen in einer Klasse, die nach der Komponente benannt ist</span><span class="sxs-lookup"><span data-stu-id="aded6-161">Wrap your CSS styles in a class named after the component</span></span>

<span data-ttu-id="aded6-162">Durch Kombinieren von CSS-Modulen mit der Unterstützung von Sass zum Verschachteln von Regelsätzen können Sie Ihre CSS-Formatvorlagen vereinfachen und sicherstellen, dass diese keine Auswirkungen auf andere Elemente auf der Seite haben.</span><span class="sxs-lookup"><span data-stu-id="aded6-162">By combining CSS modules with Sass' support for nesting rule sets you can simplify your CSS styles and ensure that they won't affect other elements on the page.</span></span>

<span data-ttu-id="aded6-p112">Verpacken Sie beim Erstellen von CSS-Formatvorlagen für eine Komponente diese in einer Klasse, die nach der Komponente benannt ist. Weisen Sie diese Klassen dann in der Komponente dem Stammelement der Komponente zu.</span><span class="sxs-lookup"><span data-stu-id="aded6-p112">When building CSS styles for a component, wrap them in a class named after the component. Then, in the component, assign that class to the component's root element.</span></span>

<span data-ttu-id="aded6-165">**todoList.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="aded6-165">**todoList.module.scss:**</span></span>

```scss
.todoList {
  a {
    display: block;
  }
}
```

<span data-ttu-id="aded6-166">**TodoList.tsx:**</span><span class="sxs-lookup"><span data-stu-id="aded6-166">**TodoList.tsx:**</span></span>

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

<span data-ttu-id="aded6-167">Nach der Übertragung sieht die generierte CSS-Datei in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="aded6-167">After transpilation, the generated CSS file will look similar to:</span></span>

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

<span data-ttu-id="aded6-168">Da der Selektor mit dem eindeutigen Klassennamen beginnt, der spezifisch für die Komponente ist, gilt die alternative Präsentation nur für Hyperlinks innerhalb der Komponenten.</span><span class="sxs-lookup"><span data-stu-id="aded6-168">Because the selector begins with the unique class name, specific to your component, the alternative presentation will apply only to hyperlinks inside your component.</span></span>

## <a name="integrate-office-ui-fabric"></a><span data-ttu-id="aded6-169">Integration von Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="aded6-169">Integrate Office UI Fabric</span></span>

<span data-ttu-id="aded6-170">Wenn Sie die Darstellung und das Verhalten Ihrer Anpassungen so nah wie möglich an den Standardfunktionen von SharePoint und Office 365 halten, wird dies den Endbenutzern das Arbeiten mit diesen erleichtern.</span><span class="sxs-lookup"><span data-stu-id="aded6-170">By making your customizations look and behave like the standard functionality of SharePoint and Office 365 you will make it easier for the end-users to work with them.</span></span> <span data-ttu-id="aded6-171">Office-UI-Fabric bietet eine Reihe von Steuerelementen und Formatvorlagen für die Verwendung in Ihren Anpassungen, die sich nahtlos in die vorhandene Benutzeroberfläche integrieren.</span><span class="sxs-lookup"><span data-stu-id="aded6-171">Office UI Fabric offers you a set of controls and styles for use in your customizations to seamlessly integrate with the existing user experience.</span></span> <span data-ttu-id="aded6-172">Weitere Informationen zur Verwendung von Office-UI-Fabric in SharePoint-Framework finden Sie im [Integrationshandbuch für Office-UI-Fabric](office-ui-fabric-integration.md).</span><span class="sxs-lookup"><span data-stu-id="aded6-172">For more information about using Office UI Fabric in the SharePoint Framework, read the [Office UI Fabric integration guide](office-ui-fabric-integration.md).</span></span>

## <a name="use-theme-colors"></a><span data-ttu-id="aded6-173">Verwenden von Designfarben</span><span class="sxs-lookup"><span data-stu-id="aded6-173">Use theme colors</span></span>

<span data-ttu-id="aded6-p114">In SharePoint können Benutzer die Designfarbe für Ihre Websites auswählen. In Ihren SharePoint Framework-Anpassungen sollten Sie dasselbe Design verwenden, das von den Benutzern ausgewählt wurde, damit Ihre Anpassung wie ein fester Bestandteil der Website aussieht und nicht unnötig hervorsticht. Da das Design von Benutzern auf deren Website festgelegt wird, können Sie nicht vorab festlegen, welche Farben Ihre Anpassung verwenden sollte, in SharePoint Framework kann das derzeit aktive Farbschema jedoch dynamisch und automatisch für Sie geladen werden. Weitere Informationen zu dieser Funktion finden Sie im [Leitfaden zur Verwendung von Designfarben](./use-theme-colors-in-your-customizations.md).</span><span class="sxs-lookup"><span data-stu-id="aded6-p114">SharePoint allows users to choose the theme color for their sites. In your SharePoint Framework customizations you should follow the theme selected by the users to make your customization look like an integral part of the site rather than unnecessarily stand out. Because the theme is set by users in their site, you cannot tell upfront which colors your customization should use, but SharePoint Framework can dynamically load the currently active color scheme automatically for you. For more information about this capability read the [guide on using theme colors](./use-theme-colors-in-your-customizations.md).</span></span>
