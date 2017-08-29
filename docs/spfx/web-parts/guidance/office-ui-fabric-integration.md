# <a name="using-office-ui-fabric-core-and-fabric-react-in-spfx-client-side-web-parts"></a><span data-ttu-id="8d256-101">Verwenden von Office UI Fabric Core und Fabric React in clientseitigen SPFx-Webparts</span><span class="sxs-lookup"><span data-stu-id="8d256-101">Using Office UI Fabric Core and Fabric React in SPFx client-side web parts</span></span>

#### <span data-ttu-id="8d256-p101">**Wichtig:** Sie müssen vorhandene Projekte auf *@microsoft/sp-build-web@1.0.1* oder höher aktualisieren, um Office UI Fabric React-Komponenten verwenden zu können. Lesen Sie die Anweisungen am Ende dieses Artikels, um weitere Informationen zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="8d256-p101">**Important:** You must upgrade existing projects to use *@microsoft/sp-build-web@1.0.1* or later in order to use the Office UI Fabric React components. See the instructions at the end of this article for additional information.</span></span>

<span data-ttu-id="8d256-p102">Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="8d256-p102">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

> <span data-ttu-id="8d256-p103">Die Integration und Verwendung von Office UI Fabric sind noch in Bearbeitung. Dieses Dokument soll ein Statusupdate für SPF-Entwickler bereitstellen. Es ist geplant, in Kürze einen endgültigen Plan zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="8d256-p103">Integration and usage of the Office UI Fabric is still a work in progress. The purpose of this document is to provide a status update to SPFx developers. Very soon we will publish a final plan.</span></span>

## <a name="goals"></a><span data-ttu-id="8d256-110">Ziele</span><span class="sxs-lookup"><span data-stu-id="8d256-110">Goals</span></span>

<span data-ttu-id="8d256-111">Es gibt zwei Teile von Office UI Fabric, die für Entwickler zur Verfügung stehen:</span><span class="sxs-lookup"><span data-stu-id="8d256-111">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

  1. <span data-ttu-id="8d256-p104">[Office UI Fabric Core](http://dev.office.com/fabric), auch bezeichnet als Fabric Core – Hierbei handelt es sich um einen Satz von Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen grundlegenden Bausteinen der gesamten Entwurfssprache.</span><span class="sxs-lookup"><span data-stu-id="8d256-p104">[Office UI Fabric Core](http://dev.office.com/fabric) a.k.a. Fabric Core - this is a set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

  2. <span data-ttu-id="8d256-p105">[Office UI Fabric React](http://dev.office.com/fabric#/components), auch bezeichnet als Fabric React – Dieses Paket enthält eine Reihe von React-Komponenten, die über die Fabric-Entwurfssprache hinaus erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="8d256-p105">[Office UI Fabric React](http://dev.office.com/fabric#/components) a.k.a. Fabric React - this package contains a set of React components built on top of the Fabric design language.</span></span>
  
<span data-ttu-id="8d256-p106">Einige der Ziele von SharePoint Framework bestehen darin, Microsoft und Kunden das Erstellen vielfältiger, ansprechender und konsistenter Lösungen über SharePoint hinaus zu ermöglichen. In Übereinstimmung mit diesen Zielen finden Sie nachfolgend unsere Entwurfsgrundsätze:</span><span class="sxs-lookup"><span data-stu-id="8d256-p106">Some of the goals of the SharePoint Framework are to allow both Microsoft and customers to build rich, beautiful, and consistent solutions on top of SharePoint. In accordance with these goals, here are our design principles:</span></span>

* <span data-ttu-id="8d256-118">Alle Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.</span><span class="sxs-lookup"><span data-stu-id="8d256-118">All customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="8d256-119">Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.</span><span class="sxs-lookup"><span data-stu-id="8d256-119">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="8d256-120">Kunden können die Formatvorlagen, Designs und Komponenten in Übereinstimmung mit den Anforderungen ihrer Lösung anpassen und überschreiben.</span><span class="sxs-lookup"><span data-stu-id="8d256-120">Customers can customize and override the styles, designs, and components to tailor to their solution's needs.</span></span>
* <span data-ttu-id="8d256-121">Kunden sollten in der Lage sein, Lösungen mit Frameworks zu erstellen, die nicht auf React basieren.</span><span class="sxs-lookup"><span data-stu-id="8d256-121">Customers should be able to build solutions with non-React based frameworks.</span></span>

## <a name="summary"></a><span data-ttu-id="8d256-122">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="8d256-122">Summary</span></span>

<span data-ttu-id="8d256-p107">Microsoft verwendet Fabric Core und Fabric React in SharePoint. Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, und die SharePoint-Oberflächen werden mit großer Wahrscheinlichkeit die jeweils verwendete Version von Fabric Core und Fabric React weiterhin aktualisieren. Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den Anpassungen führen kann. Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken. Solche Konflikte müssen auf jeden Fall vermieden werden.</span><span class="sxs-lookup"><span data-stu-id="8d256-p107">Microsoft uses Fabric Core and Fabric React in SharePoint. Microsoft regularly pushes updates to SharePoint Online and SharePoint experiences are likely to continue updating the version of Fabric Core and Fabric React used. These updates could potentially conflict with third party solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations. The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries. Such conflicts need to be avoided at all costs.</span></span> 

<span data-ttu-id="8d256-p108">Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss. Sowohl Fabric Core als auch „fabric.component.css“ verwenden derzeit globale Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="8d256-p108">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**. Currently, both Fabric Core and fabric.component.css use global styles.</span></span>

<span data-ttu-id="8d256-p109">Aus diesen Gründen können Kundenlösungen derzeit Teile von Office-UI-Fabric noch nicht sicher verwenden. Natürlich sind wir uns bewusst, dass Entwickler Fabric Core und Fabric React zum Erstellen ihrer Lösungen benötigen. Wir arbeiten daran, dies so schnell wie möglich zu beheben.</span><span class="sxs-lookup"><span data-stu-id="8d256-p109">For these reasons, currently, customer solutions cannot yet safely use portions of the Office UI Fabric. However, we understand that developers need Fabric Core and Fabric React to build their solutions. We are working to resolve this as quickly as possible.</span></span>

<span data-ttu-id="8d256-133">Nachfolgend finden Sie eine Zusammenfassung derzeit unterstützter Optionen zur Verwendung von Office-UI-Fabric mit SharePoint Framework-Lösungen basierend auf dem ausgewählten JavaScript-Framework.</span><span class="sxs-lookup"><span data-stu-id="8d256-133">Here's a summary of currently supported options for using the Office UI Fabric within SharePoint Framework solutions based on the JavaScript framework selected:</span></span>

- <span data-ttu-id="8d256-134">React – Office-UI-Fabric kann nur über die **statische Verknüpfung** mit den Fabric React-Komponenten sicher verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8d256-134">React - You can only use the Office UI Fabric safely by **statically linking** to the Fabric React components</span></span>
- <span data-ttu-id="8d256-135">Andere JS-Bibliotheken – Die Verwendung von Office-UI-Fabric innerhalb einer SharePoint Framework-Lösung wird **nicht** unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8d256-135">Other JS libraries - Usage of the Office UI Fabric within a SharePoint Framework solution is **not** supported</span></span>

> <span data-ttu-id="8d256-p110">Ein Beispiel für das aktuelle Problem mit der Versionsverwaltung: Ein Webpart verwendet die Klasse `ms-Icon--List`, wenn das Webpart erstellt wird. Später entscheidet Fabric, dass die Definition dieser Klasse geändert werden soll. Das Webpart, das eine Annahme zu der vorherigen Implementierung gestellt hatte, wird möglicherweise beschädigt. Gleichermaßen nehmen wir beispielsweise an, dass das Webpart die Klasse `ms-Button` aus Fabric React verwendet. Zu einem späteren Zeitpunkt ändert das Fabric React-Team die Implementierung der Schaltfläche zusammen mit den Formatvorlagen in der `ms-Button`-Klasse wesentlich. Dadurch würde das Webpart aller Wahrscheinlichkeit nach beschädigt werden.</span><span class="sxs-lookup"><span data-stu-id="8d256-p110">An example of the current versioning challenge: A web part consumes the class `ms-Icon--List` when they build their web part. At a later date, Fabric decides to change the definition of this class. The web part that had made an assumption regarding the previous implementation can break. Similarly, let's say, the web part uses the class `ms-Button` from Fabric React. Then the Fabric React team later changes the implementation of the Button in a big way along with the styles in the `ms-Button` class. That would likely break the web part.</span></span>

> <span data-ttu-id="8d256-142">Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JSS ausführlich erläutert: [React-CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="8d256-142">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

## <a name="how-to-use-the-office-ui-fabric-react-in-a-safe-way-in-your-solution"></a><span data-ttu-id="8d256-143">Sicheres Verwenden von Office UI Fabric React in Ihrer Lösung</span><span class="sxs-lookup"><span data-stu-id="8d256-143">How to use the Office UI Fabric React in a Safe Way in Your Solution</span></span>

<span data-ttu-id="8d256-144">Nachfolgend finden Sie Empfehlungen zur sicheren und zuverlässigen Verwendung von Fabric in auf React basierenden Webparts.</span><span class="sxs-lookup"><span data-stu-id="8d256-144">Here are the recommendations for using Fabric in React based web parts in a safe and reliable way:</span></span>

- <span data-ttu-id="8d256-p111">Webpartentwickler müssen eine explizite Abhängigkeit von einer bestimmten Version von Fabric React, Version 2.0, in der **package.json**-Datei `"office-ui-fabric-react":"2.34.2"` verwenden. Beachten Sie, dass ältere Versionen von Fabric React als Version 2.x nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="8d256-p111">Web part developers should place an explicit dependency on the specific version of Fabric React version 2.0 in their **package.json** file `"office-ui-fabric-react":"2.34.2"`. Please note, Fabric React versions older than 2.x are not supported.</span></span>
- <span data-ttu-id="8d256-p112">Der Webpartentwickler muss eine **statische Verknüpfung** zu den Fabric React-Komponenten herstellen. Dazu gehören die Fabric React-Komponenten in Ihrem Webpartpaket. Würde sich die Implementierung der Schaltfläche auf Seitenebene ändern, hätte dies keine nachteiligen Auswirkungen auf Ihr Webpart.</span><span class="sxs-lookup"><span data-stu-id="8d256-p112">Web part developers need to **statically link** to the Fabric React components. This includes the Fabric React component in your web part bundle. This will ensure that if the page level implementation of the Button were to change, it will not affect your web part adversely.</span></span>
- <span data-ttu-id="8d256-p113">Das **Außerkraftsetzen** von Formatvorlagen für Fabric React-Komponenten sollte nur selten und innerhalb eines lokalen Bereichs verwendet werden. Die Außerkraftsetzungen können von einem Entwickler unter Verwendung von benutzerdefinierten CSS-Klassen mit `!important` und Styletags vorgenommen werden. Beides hat eine höhere Genauigkeit als die Komponentenklassen. Wenn Sie eine Außerkraftsetzung unter Verwendung einer einfachen Klasse vornehmen, beachten Sie, dass dann möglicherweise Probleme mit der Ladereihenfolge auftreten können. Wenn `ms-Button` nach Ihrer Klasse geladen wird, hat diese Vorrang, da ihre Genauigkeit dieselbe ist.</span><span class="sxs-lookup"><span data-stu-id="8d256-p113">**Overriding** Fabric React component styles should be done only sparingly and within a local scope. A developer can override using custom CSS classes with `!important` and style tags. Both will have higher specificity than the component classes. Please note, if you override using a simple class, then you may run into load order issues. i.e. If `ms-Button` loads after your class, it will take precedence because their specificity is the same.</span></span>
- <span data-ttu-id="8d256-p114">**Designs** sollten standardmäßig funktionieren. Seitens des Entwicklers sind keine weiteren Aktionen erforderlich.</span><span class="sxs-lookup"><span data-stu-id="8d256-p114">**Theming** should just work as is. No extra work is required on the part of the developer.</span></span>

<span data-ttu-id="8d256-157">Der folgende Codeausschnitt zeigt, wie die statische und dynamische Verknüpfung von Bibliotheken funktioniert.</span><span class="sxs-lookup"><span data-stu-id="8d256-157">The following code snippet shows how to perform static and dynamic linking of libraries:</span></span>

```Javascript
  // This sample demonstrates how static linking should be done for Fabric React components.
  // Remember to explicitly add a dependency on a specific version of 
  // office-ui-fabric-react in your package.json file.

  // correct - static linking.
  import { Button } from 'office-ui-fabric-react/lib/Button';

  // incorrect - dynamic linking.
  import { Button } from '@microsoft/office-ui-fabric-react';

  render() {
    ...
    <div>
      <Button>click me</Button>
    </div>
    ...
  }
```

<span data-ttu-id="8d256-158">***Grundlegendes zu diesem Ansatz und Nachteile***</span><span class="sxs-lookup"><span data-stu-id="8d256-158">***Understanding this approach and its shortcomings:***</span></span>

- <span data-ttu-id="8d256-p115">Komponenten im Webpart sind auf die Version von Fabric React beschränkt, die Sie beim Erstellen des Webparts verwendet haben. Diese werden nicht automatisch mit der umgebenden Seite weiterentwickelt. Sie müssen Ihr Webpart manuell aktualisieren, um eine Anpassung an neuere Versionen von Fabric React vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="8d256-p115">Components in your web part are locked to the version of Fabric React you used when you built the web part. They will not automatically evolve with the surrounding page. You will need to manually update your web part to adapt to newer versions of Fabric React.</span></span>
- <span data-ttu-id="8d256-162">Die Seite reagiert möglicherweise langsamer, da unter Umständen mehr CSS geladen wird, funktioniert aber zuverlässig.</span><span class="sxs-lookup"><span data-stu-id="8d256-162">The page may be less performant as it may load more CSS, but it will be reliable.</span></span>
- <span data-ttu-id="8d256-p116">Die statische Verknüpfung bläht Ihr Webpartpaket auf, die dynamische Verknüpfung ist jedoch angesichts künftiger Updates, die in SharePoint Online eingeführt werden, nicht stabil genug. Die statische Verknüpfung ist der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in den SharePoint Framework-Lösungen unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="8d256-p116">Static linking bloats up your web part bundle, but dynamic linking is too fragile considering future updates to be introduced in SharePoint Online. Static linking is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>

### <a name="currently-unsupported-features"></a><span data-ttu-id="8d256-165">Derzeit nicht unterstützte Features</span><span class="sxs-lookup"><span data-stu-id="8d256-165">Currently unsupported features</span></span>

- <span data-ttu-id="8d256-p117">**Office UI Fabric Core**: Die Fabric Core-Implementierung verwendet derzeit globale Formatvorlagen, z. B. `.ms-Icon--List`, und Fabric Core kann daher nicht sicher in Ihrem Webpart ohne mögliche Probleme in der Zukunft verwendet werden. Es wird daran gearbeitet, dieses Problem zu lösen. Weitere Informationen werden veröffentlicht, wenn sich die Situation ändert.</span><span class="sxs-lookup"><span data-stu-id="8d256-p117">**Office UI Fabric Core**: The Fabric Core implementation currently uses global styles e.g. `.ms-Icon--List` and hence there is no safe way to use Fabric core in your web part without potential challenges in the future. Work is being done to address this challenge and more details will be shared when the situation changes.</span></span>

- <span data-ttu-id="8d256-p118">**fabric.components.css**: Diese Datei enthält globale Klassen, die mit Fabric React in Konflikt stehen, `.ms-Button` in „fabric.component.css“ setzt beispielsweise die Button-Formatvorlagen in der Button-Komponente von Fabric React außer Kraft. Das Einbinden von „fabric.component.css“ führt dazu, dass die umgebende Seite oder andere Webparts auf der Seite beschädigt werden. Wir arbeiten an einer Lösung und werden in Kürze ein Update veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="8d256-p118">**fabric.components.css**: This file contains global classes that conflict with Fabric React. e.g. `.ms-Button` in fabric.component.css will override the Button styles in a Fabric React Button component. Including fabric.component.css in a web part is bound to break the surrounding page or other web parts on the page. We are working on a solution and will release an update shortly.</span></span>


## <a name="using-the-office-ui-fabric-with-non-react-based-web-parts"></a><span data-ttu-id="8d256-172">Verwenden von Office UI Fabric mit Webparts, die nicht auf React basieren</span><span class="sxs-lookup"><span data-stu-id="8d256-172">Using the Office UI Fabric with Non-React Based Web Parts</span></span>

<span data-ttu-id="8d256-p119">Die Verwendung von  Office UI Fabric mit Webparts, die nicht auf React basieren, wird derzeit nicht unterstützt, und mögliche Implementierungen können unerwartete Probleme verursachen, wenn eine neuere Version von Office UI Fabric veröffentlicht wird. Wir arbeiten derzeit an einer zuverlässigen Integration von **Office UI Fabric Core**, **fabric.component.css** und **nicht auf React basierenden Webparts**.</span><span class="sxs-lookup"><span data-stu-id="8d256-p119">Using the Office UI Fabric with non-React based web parts is currently not supported and implementations could experience unexpected issues when newer versions of the Office UI Fabric are released. We are working on creating a reliable integration story for **Office UI Fabric Core**, **fabric.component.css**, and **Non-React based web parts**.</span></span> 

## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="8d256-175">Weitere Informationen zu dem CSS-Problem in Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="8d256-175">Additional Details on the CSS Challenge with Office UI Fabric</span></span>
<span data-ttu-id="8d256-176">Die folgenden Konzepte und Verweise liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext clientseitiger Webparts.</span><span class="sxs-lookup"><span data-stu-id="8d256-176">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

<span data-ttu-id="8d256-p120">**Globale CSS-Formatvorlagen** und wie diese unbedingt vermieden werden: Dies stellt ein großes Problem dar. Heute weisen sowohl Fabric Core als auch Fabric React globale Formatvorlagen auf. Aufgrund eines Mangels systemeigener Lösungen vom Browser zum Verwalten der Bereichsdefinition der Formatvorlagen ist dies ein schwerwiegendes Problem.</span><span class="sxs-lookup"><span data-stu-id="8d256-p120">**Global CSS styles** and how to avoid them at all cost: this is a big problem. Today, both Fabric Core and Fabric React have global styles. Lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="8d256-180">[Die Bereichsdefinition von CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope) erfolgt in den frühen Phasen der Besprechung.</span><span class="sxs-lookup"><span data-stu-id="8d256-180">[Scope CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope) is in early stages of discussion.</span></span> 
  - <span data-ttu-id="8d256-181">iFrames sind keine gute Option zum Isolieren von Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="8d256-181">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="8d256-182">[Webkomponenten](https://developer.mozilla.org/en-US/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht, der sich aber noch in der Besprechungsphase befindet.</span><span class="sxs-lookup"><span data-stu-id="8d256-182">[Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
          
    <span data-ttu-id="8d256-p121">In [dieser](https://speakerdeck.com/vjeux/react-css-in-js) Diskussion wird das Problem gut erläutert. Es gibt zahlreiche andere Dokumentationen im Web über die Lösungen für das Problem mit dem globalen Namespace.</span><span class="sxs-lookup"><span data-stu-id="8d256-p121">[This](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>
 
<span data-ttu-id="8d256-p122">**[CSS-Genauigkeit](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)** und wie diese auf Webbenutzeroberflächen angewendet wird. Formatvorlagen mit höherer Genauigkeit setzen die Formatvorlagen mit niedrigerer Genauigkeit außer Kraft.  Das Wichtigste ist jedoch, dass Sie verstehen, wie die Genauigkeitsregeln angewendet werden. Im Allgemeinen ist die Rangfolge von oben nach unten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="8d256-p122">**[CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)** and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="8d256-188">Das Style-Attribut (z. B. `style="background:red;"`)</span><span class="sxs-lookup"><span data-stu-id="8d256-188">The style attribute (e.g. `style="background:red;"`)</span></span>
  - <span data-ttu-id="8d256-189">ID-Selektoren (z. B. `#myDiv { }`)</span><span class="sxs-lookup"><span data-stu-id="8d256-189">Id selectors (e.g. `#myDiv { }`)</span></span>
  - <span data-ttu-id="8d256-190">Klassenselektoren (z. B. `.myCssClass{}`), Attributselektoren (z. B. `[type="radio"]`) und Pseudoselektoren (z. B. `:hover`)</span><span class="sxs-lookup"><span data-stu-id="8d256-190">Class selectors (e.g. `.myCssClass{}`), attributre selectors (e.g. `[type="radio"]`), and pseudo-classes (e.g. `:hover`)</span></span>
  - <span data-ttu-id="8d256-191">Typselektoren (z.B. `h1`)</span><span class="sxs-lookup"><span data-stu-id="8d256-191">Type selectors (e.g. `h1`)</span></span>

<span data-ttu-id="8d256-p123">***Ladereihenfolge*** – Wenn zwei Klassen auf ein Element angewendet werden und diese dieselbe Genauigkeit aufweisen, hat die Klasse Vorrang, die später geladen wird. Wie im folgenden Code dargestellt, wird die Schaltfläche rot angezeigt. Wenn die Reihenfolge der Styletags geändert wird, wird die Schaltfläche grün angezeigt. Dies ist ein wichtiges Konzept. Wenn es nicht korrekt verwendet wird, kann die Benutzerfreundlichkeit von der Ladereihenfolge abhängig sein, d.h. sie wird inkonsistent.</span><span class="sxs-lookup"><span data-stu-id="8d256-p123">***Loading order*** - If two classes are applied on an element and they have the same specificity, the class that is loaded later takes precedence. As shown in the code below, the button will appear red. If the order of the style tags is changed, the button will appear green. This is an important concept, and if not used correctly, the user experience can become load order dependent (i.e. inconsistent).</span></span>

```HTML
<style>
  .greenButton { color: green; }
</style>
<style>
  .redButton { color: red; }
</style>
<body>
  <button class="greenButton redButton"></button>
</body>
```

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="8d256-196">Andere in Erwägung gezogene und verworfene Ansätze</span><span class="sxs-lookup"><span data-stu-id="8d256-196">Other Approaches Considered and Discarded</span></span>
<span data-ttu-id="8d256-197">Nachfolgend finden Sie weitere Informationen zu den anderen Ansätzen, die in Betracht gezogen, aber dann verworfen wurden, weil damit die wichtigsten Ziele, und zwar, dass Drittanbieterentwickler Office UI Fabric-Formatvorlagen sicher verwenden können, nicht erreicht wurden.</span><span class="sxs-lookup"><span data-stu-id="8d256-197">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

<span data-ttu-id="8d256-198">**Office UI Fabric Core**</span><span class="sxs-lookup"><span data-stu-id="8d256-198">**Office UI Fabric Core**</span></span>

<span data-ttu-id="8d256-p124">Der Webpartentwickler muss nicht explizit etwas tun, damit die Bereichsdefinition funktioniert. Wir planen, dieses Problem über die CSS-Genauigkeit und einen Nachfolgerselektor zu beheben. Das Fabric Core-Team wird mehrere Kopien von Fabric Core-CSS-Dateien ausliefern, z. B. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span><span class="sxs-lookup"><span data-stu-id="8d256-p124">The web part developer would not be required to do anything explicitly to get the scoping to work. We planned to solve this problem through CSS specificity and descendant selectors. The Fabric Core team would ship multiple copies of Fabric Core css. e.g. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span></span>

<span data-ttu-id="8d256-p125">Alle Formatvorlagen in den bereichsbezogenen CSS-Dateien befinden sich innerhalb eines Nachfolgerselektors, z. B. `"ms-Fabric-core--v6 ms-Icon--List"`. Zur Kompilierzeit erfassen die Tools die Version von Office UI Fabric Core, mit der das Webpart erstellt wurde. Bei dieser Version kann es sich um die Version handeln, die mit SPFx geliefert wird. Webpartentwickler können alternativ eine explizite Abhängigkeit von einer bestimmten Version von Office-UI-Fabric Core in ihrer**package.json**-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="8d256-p125">All the styles in the scoped CSS files would be inside a descendant selector e.g. `"ms-Fabric-core--v6 ms-Icon--List"`. At compile time, the tooling would collect the version of the Office UI Fabric Core the web part was built with. This version could be the one that comes with SPFx. Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="8d256-p126">Das Webpart-Div wird diesem Bereich zugewiesen, d. h. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Das Framework lädt die spezifische Hauptversion der bereichsbezogenen Fabric Core-CSS-Datei. Wenn das Webpart mit Version 6.0.0 von Fabric Core-CSS erstellt wurde, lädt das Framework `fabric-6-scoped.css` zur Ladezeit des Webparts herunter.</span><span class="sxs-lookup"><span data-stu-id="8d256-p126">The web part div would be assigned this scope i.e. `<div data-sp-webpart class="ms-Fabric-core--v6">`. The framework would load the specific major version of the Fabric core scoped CSS file. If the web part was built with version 6.0.0 of Fabric core CSS, the framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="8d256-p127">Der Rest der Seite enthält nicht bereichsbezogenen Office UI Fabric Core-Formatvorlagen. Auf diese Weise erhält das bereichsbezogene CSS Vorrang innerhalb des Webpart-Div, wie in den CSS-Genauigkeitsregeln festgelegt. Das Webpart und sein Inhalt werden auf die Version von Office UI Fabric Core abgestimmt, die der Entwickler ausgewählt hat.</span><span class="sxs-lookup"><span data-stu-id="8d256-p127">The rest of the page would contain unscoped Office UI Fabric Core styles. This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div. The web part and its contents would align to the specific version of the Office UI Fabric Core the developer had chosen.</span></span>

<span data-ttu-id="8d256-212">Das **Außerkraftsetzen** von Fabric Core-Formatvorlagen wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8d256-212">**Overriding** Fabric Core styles would not be supported.</span></span>  

```Javascript
// Sample of how the scoping would work.
import { SPComponentLoader } from '@microsoft/sp-loader';

export default class MyWebPart {
    constructor() {
        super();

        SPComponentLoader.loadCss('https://static2.sharepointonline.com/files/fabric/office-ui-fabric-core/6.0.0/css/fabric-6.0.0.scoped.css');
    }
}

protected render(): void {
  <div className={css('ms-Fabric-core--v6')}>
    { // Rest of the web part UI }
  </div>
}
```

<span data-ttu-id="8d256-213">Nach längerer Analyse dieser Strategie wurde festgestellt, dass der Ansatz mit dem Nachfolgerselektor zwei wesentliche Nachteile hat, aufgrund derer es nicht möglich ist, ein Webpart zu erstellen, das niemals beschädigt wird.</span><span class="sxs-lookup"><span data-stu-id="8d256-213">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

<span data-ttu-id="8d256-p128">**Keine zuverlässige Unterstützung für Schachtelung** – Dieser Ansatz funktioniert nur, wenn die Microsoft-Benutzeroberfläche (d. h. die Seite und alle Erstanbieter-Webparts) eine nicht bereichsbezogene Version von Office UI Fabric Core verwenden (z. B. `ms-Icon--List`) und wenn die Drittanbieter-Webparts nur bereichsbezogenes Office UI Fabric Core-CSS wie oben erläutert verwenden. Der Grund hierfür ist, dass die Genauigkeit des bereichsbezogenen CSS, das auf das Webpart angewendet wird, das nicht bereichsbezogene CSS auf der Seite außer Kraft setzt. Beachten Sie: Wie oben erläutert gilt, dass, wenn die CSS-Genauigkeit von zwei Klassen gleich ist, ihre Ladereihenfolge eine Rolle für die Anwendung der CSS-Klassen spielt. Die Klasse, die später geladen wird, hat Vorrang. Die höhere Genauigkeit des bereichsbezogenen CSS ist daher wichtig, um eine konsistente Oberfläche zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="8d256-p128">**Lack of reliable nesting support** - This approach only works if the Microsoft user experience (i.e. page and first party web parts) use an unscoped version of the Office UI Fabric Core. i.e. `ms-Icon--List` while the third party web parts only use scoped Office UI Fabric Core css as explained above. The reason being that the specificity of the scoped CSS applied on the web part overrides unscoped CSS on the page. Keep in mind, as explained above, if CSS specificity of two classes is the same, then their loading order plays a role in how the CSS classes will be applied. The class that loads later will take precedence. Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="8d256-p129">Darüber hinaus können mehrere Erweiterungen, von denen eine jeweils in der anderen enthalten ist, nicht unterschiedliche Fabric Core-Versionen verwenden, d. h. im folgenden Beispiel wird nur `ms-Fabric-core--v6` angewendet:</span><span class="sxs-lookup"><span data-stu-id="8d256-p129">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<span data-ttu-id="8d256-222">Nachfolgend finden Sie ein einfacheres Beispiel, in dem das Problem erläutert wird:</span><span class="sxs-lookup"><span data-stu-id="8d256-222">Here's a more simplistic sample demonstrating the challenge:</span></span>

```HTML
<html>
<head>
  <title>CSS specifity test</title>
  <style>
  .myButton {
      background-color: brown;
      color: brown;
      height: 20px;
      width: 40px;
  }
  </style>
  <style>
  .scope2 .myButton {
      background-color: green;
      color: green;
  }
  </style>
  <style>
  .scope3 .myButton {
      background-color: yellow;
      color: yellow;
  }
  </style>
  <style>
  .scope1 .myButton {
      background-color: red;
      color: red;
  }
  </style>
</head>
<body>
  <div>
    <span>These tests demonstrate descendant selectors, nesting and load order problems.</span>

    <div>
      <br/>
      <span>This test depicts that a descendant selector with the same specificity does not allow nesting.
      All buttons below do not take the innermost scope (i.e. they should be different colors), but they are all red.
      Further, if you change the ordering of the style tags, the colors will change. (i.e. the UI is load order dependant.)</span> 
      <div class='scope1'>
        <button class='myButton'</button>
        <div class='scope2'>
          <button class='myButton'></button>
          <div class='scope3'>
            <button class='myButton'></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

<span data-ttu-id="8d256-p130">**Offenlegung von nicht bereichsbezogenen Klassen** – Es gibt ein weiteres Problem mit Nachfolgerselektoren. Beachten Sie im obigen Beispiel, dass die Formatvorlagen für Höhe und Breite aus der nicht bereichsbezogenen myButton-Klasse auf alle Schaltflächen angewendet werden. Dies impliziert, dass eine Änderung in dieser Formatvorlage die HTML, die das bereichsbezogene Markup verwendet, versehentlich beschädigen könnte. Nehmen wir beispielsweise an, dass wir die Höhe auf App-Ebene auf 0px in der myButton-Klasse festlegen. Dies führt dazu, dass alle Drittanbieter-Webparts, die die myButton-Klasse verwenden, eine Höhe von 0 haben, also eine wesentliche Regression in der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8d256-p130">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0px (i.e. a serious regression in the user experience).</span></span>

## <a name="updating-an-existing-project"></a><span data-ttu-id="8d256-228">Aktualisieren bereits vorhandener Projekte</span><span class="sxs-lookup"><span data-stu-id="8d256-228">Updating an existing project</span></span>

<span data-ttu-id="8d256-229">Aktualisieren Sie in der Datei `package.json` Ihres Projekts die Abhängigkeit `@microsoft/sp-build-web` mindestens auf Version 1.0.1, löschen Sie das Verzeichnis `node_modules` Ihres Projekts, und führen Sie den Befehl `npm install` aus.</span><span class="sxs-lookup"><span data-stu-id="8d256-229">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>

