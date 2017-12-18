---
title: "Verwenden von Office UI Fabric Core und Fabric React in SharePoint-Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e1e9ac646257d8875de4097b65b19e680e1f9f25
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a><span data-ttu-id="9ef37-102">Verwenden von Office UI Fabric Core und Fabric React in SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="9ef37-102">Using Office UI Fabric Core and Fabric React in SPFx client-side web parts</span></span>

<span data-ttu-id="9ef37-p101">Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p101">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

## <a name="summary"></a><span data-ttu-id="9ef37-106">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9ef37-106">Summary</span></span>

<span data-ttu-id="9ef37-107">Microsoft verwendet Fabric Core und Fabric React in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9ef37-107">Microsoft uses Fabric Core and Fabric React in SharePoint.</span></span> <span data-ttu-id="9ef37-108">Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, die möglicherweise auch die Fabric Core- und Fabric React-Versionen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9ef37-108">Microsoft regularly pushes updates to SharePoint Online which could also update the Fabric Core and Fabric React versions as well.</span></span> <span data-ttu-id="9ef37-109">Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den Anpassungen führen kann.</span><span class="sxs-lookup"><span data-stu-id="9ef37-109">These updates could potentially conflict with third party customer solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations.</span></span> <span data-ttu-id="9ef37-110">Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="9ef37-110">The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries.</span></span> <span data-ttu-id="9ef37-111">Solche Konflikte müssen auf jeden Fall vermieden werden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-111">Such conflicts need to be avoided at all costs.</span></span> 

> <span data-ttu-id="9ef37-112">Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JSS ausführlich erläutert: [React-CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="9ef37-112">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

<span data-ttu-id="9ef37-113">Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss.</span><span class="sxs-lookup"><span data-stu-id="9ef37-113">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**. Currently, both Fabric Core and fabric.component.css use global styles.</span></span> <span data-ttu-id="9ef37-114">Grund hierfür ist, dass keine globalen Klassennamen im HTML-Markup verwendet werden und stattdessen Fabric Core-Mixins und -Variablen in der SASS-Deklarationsdatei verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-114">This accounts to not using global class names in the HTML markup and instead using Fabric Core mixins and variables in the SASS declaration file.</span></span> <span data-ttu-id="9ef37-115">Dies umfasst den Import der Fabric Core-SASS-Deklarationen in die SASS-Datei und anschließend eine entsprechende Verarbeitung der Variablen und Mixins.</span><span class="sxs-lookup"><span data-stu-id="9ef37-115">This involves importing the Fabric Core's SASS declarations in your SASS file and then consuming the variables and mixins appropriately.</span></span> 

## <a name="goals"></a><span data-ttu-id="9ef37-116">Ziele</span><span class="sxs-lookup"><span data-stu-id="9ef37-116">Goals</span></span>

<span data-ttu-id="9ef37-117">Das Ziel von SharePoint-Framework besteht darin, Microsoft und Kunden das Erstellen vielfältiger, ansprechender und konsistenter Benutzeroberflächen über SharePoint hinaus zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="9ef37-117">One of the goals of SharePoint Framework is to allow both Microsoft and customers to build rich, beautiful and consistent solutions on top of SharePoint. Based on that, here are our design principles:</span></span> <span data-ttu-id="9ef37-118">Im Folgenden werden die wichtigsten Entwurfsprinzipien entsprechend diesen Zielen erläutert:</span><span class="sxs-lookup"><span data-stu-id="9ef37-118">In accordance with these goals, below are the key design  principles:</span></span>

* <span data-ttu-id="9ef37-119">Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.</span><span class="sxs-lookup"><span data-stu-id="9ef37-119">All customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="9ef37-120">Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.</span><span class="sxs-lookup"><span data-stu-id="9ef37-120">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="9ef37-121">Kunden können die Standardformatvorlagen, Designs und Komponenten in Übereinstimmung mit den Anforderungen ihrer Lösung anpassen und überschreiben.</span><span class="sxs-lookup"><span data-stu-id="9ef37-121">Customers can customize and override the styles, designs, and components to tailor to their solution's needs.</span></span>

<span data-ttu-id="9ef37-122">Es gibt zwei Teile von Office UI Fabric, die für Entwickler zur Verfügung stehen:</span><span class="sxs-lookup"><span data-stu-id="9ef37-122">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

* [<span data-ttu-id="9ef37-123">Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="9ef37-123">Office UI Fabric Core</span></span>](http://dev.office.com/fabric)

  <span data-ttu-id="9ef37-124">Hierbei handelt es sich um einen Satz von Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen grundlegenden Bausteinen der gesamten Entwurfssprache.</span><span class="sxs-lookup"><span data-stu-id="9ef37-124">Office UI Fabric Core a.k.a. Fabric Core - this is a set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

* [<span data-ttu-id="9ef37-125">Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="9ef37-125">Office UI Fabric React</span></span>](http://dev.office.com/fabric#/components)

  <span data-ttu-id="9ef37-126">Hierbei handelt es sich um eine Reihe von React-Komponenten, die über die Fabric-Entwurfssprache hinaus für die Verwendung in React-basierten Projekten erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-126">A set of React components built on top of the Fabric design language for use in React-based projects.</span></span>

## <a name="spfx-fabric-core-package"></a><span data-ttu-id="9ef37-127">SPFx Fabric Core-Paket</span><span class="sxs-lookup"><span data-stu-id="9ef37-127">SPFx Fabric Core Package</span></span>

<span data-ttu-id="9ef37-128">Das npm-Paket von SPFx Fabric Core – Fabric-Core - sp-office-ui-fabric-core – enthält eine Teilmenge der unterstützten Fabric Core-Formatvorlagen, die auf sichere Weise in einer SharePoint-Framework-Komponente verarbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="9ef37-128">The SPFx Fabric Core npm package - sp-office-ui-fabric-core - contains a subset of supported Fabric Core styles that can be safely consumed within a SharePoint Framework component.</span></span> 

<span data-ttu-id="9ef37-129">Die folgenden grundlegenden Formatvorlagen werden in dem Paket unterstützt:</span><span class="sxs-lookup"><span data-stu-id="9ef37-129">The following core styles are supported in the package:</span></span>
- <span data-ttu-id="9ef37-130">Typografie</span><span class="sxs-lookup"><span data-stu-id="9ef37-130">Typography</span></span>
- <span data-ttu-id="9ef37-131">Layouts</span><span class="sxs-lookup"><span data-stu-id="9ef37-131">Layouts</span></span>
- <span data-ttu-id="9ef37-132">Farben</span><span class="sxs-lookup"><span data-stu-id="9ef37-132">Colors</span></span>
- <span data-ttu-id="9ef37-133">Designs</span><span class="sxs-lookup"><span data-stu-id="9ef37-133">Themes</span></span>
- <span data-ttu-id="9ef37-134">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="9ef37-134">Localization</span></span>

<span data-ttu-id="9ef37-135">Folgendes wird in dem Paket noch nicht unterstützt:</span><span class="sxs-lookup"><span data-stu-id="9ef37-135">The following are not yet supported in the package:</span></span>
- <span data-ttu-id="9ef37-136">Animationen</span><span class="sxs-lookup"><span data-stu-id="9ef37-136">Animations</span></span>
- <span data-ttu-id="9ef37-137">Symbole</span><span class="sxs-lookup"><span data-stu-id="9ef37-137">Icons</span></span>

<span data-ttu-id="9ef37-138">Ab Yeoman-Generator Version 1.3.4 von SharePoint-Framework sind standardmäßige Projektvorlagen (Webparts und Erweiterungen) im neuen Paket „sp-office-fabric-core“ eingerichtet, und es werden die grundlegenden Formatvorlagen aus dem Paket anstelle von globalen CSS-Formatvorlagen verwendet.</span><span class="sxs-lookup"><span data-stu-id="9ef37-138">Starting with the SharePoint Framework yeoman generator version 1.3.4, the default project (web parts and extensions) templates will come setup with the new sp-office-ui-fabric-core package and consume core styles from the package instead of using global CSS styles.</span></span> 

### <a name="updating-existing-projects"></a><span data-ttu-id="9ef37-139">Aktualisieren bereits vorhandener Projekte</span><span class="sxs-lookup"><span data-stu-id="9ef37-139">Updating existing projects</span></span>

<span data-ttu-id="9ef37-140">Um das SPFx Fabric Core-Paket in einem bereits vorhandenen Projekt zu verwenden, müssen Sie das Paket als dev-Abhängigkeit installieren:</span><span class="sxs-lookup"><span data-stu-id="9ef37-140">To use the SPFx Fabric Core package in your existing project, install the package as dev dependency:</span></span>

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="9ef37-141">Nach Abschluss der Installation können Sie die Fabric Core-SASS-Deklarationen in die SASS-Definitionsdatei importieren und die Mixins und Variablen wie im folgenden Abschnitt beschrieben verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-141">Once installed, you can then import the Fabric Core SASS declarations in your SASS defintion file and use the mixins and variables as decribed in the section below.</span></span> 

### <a name="using-fabric-core-styles"></a><span data-ttu-id="9ef37-142">Verwenden von Fabric Core-Formatvorlagen</span><span class="sxs-lookup"><span data-stu-id="9ef37-142">Using Fabric Core styles</span></span>

<span data-ttu-id="9ef37-143">Um die Fabric Core-Formatvorlagen zu verwenden, müssen Sie zunächst die SPFabricCore-Deklarationen in Ihre SASS-Datei importieren.</span><span class="sxs-lookup"><span data-stu-id="9ef37-143">In order to use the Fabric Core styles first you will need to import the SPFabricCore declarations in your SASS file.</span></span>

> <span data-ttu-id="9ef37-144">Hinweis: Installieren Sie das npm-Paket „sp-office-ui-fabric-core“.</span><span class="sxs-lookup"><span data-stu-id="9ef37-144">Note: Make sure you have the sp-office-ui-fabric-core npm package installed.</span></span>

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

<span data-ttu-id="9ef37-145">Sie können jetzt die grundlegenden Formatvorlagen sowie Mixins und Variablen verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-145">Now, you can use the core styles as mixins and variables.</span></span>

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="using-office-ui-fabric-react"></a><span data-ttu-id="9ef37-146">Verwenden von Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="9ef37-146">Office UI Fabric React Components</span></span>

<span data-ttu-id="9ef37-147">Es wird empfohlen, das neueste Office UI Fabric React-Paket zu installieren und eine explizite Abhängigkeit für diese bestimmte Version des Pakets zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="9ef37-147">It is recommended to install the latest Office UI Fabric React package and place an explicit dependency on that specific version of the package.</span></span> <span data-ttu-id="9ef37-148">Dies umfasst die in der SPFx-Lösung verwendeten Komponenten in Ihrem Komponentenbundle, entweder Webpart oder Erweiterung, je nachdem wo Sie die Fabric React-Komponenten verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-148">This will include the components used in your SPFx solution in your component bundle, either the web part or extension depending on where you use the Fabric React components.</span></span> 

> <span data-ttu-id="9ef37-149">Bitte beachten Sie, dass die Versionen 2.x und älter von Fabric React in SharePoint-Framework nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-149">Please note that Fabric React versions 2.x or older are not supported in SharePoint Framework.</span></span>

<span data-ttu-id="9ef37-150">Nach der Installation des Fabric React-Pakets können Sie die erforderlichen Komponenten aus dem Fabric React-Paket importieren.</span><span class="sxs-lookup"><span data-stu-id="9ef37-150">Once the Fabric React package is installed, you can import the required components from the Fabric React bundle.</span></span>

```Javascript
//import Button component from Fabric React Button bundle
import { Button } from 'office-ui-fabric-react/lib/Button';

//use it in your component
render() {
  ...
  <div>
    <Button>click me</Button>
  </div>
  ...
}
```

<span data-ttu-id="9ef37-151">Das Fabric React-Paket enthält die unterstützten Fabric Core-Formatvorlagen, die in den Fabric React-Komponenten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-151">Fabric React package includes the supported Fabric Core styles used in the Fabric React components.</span></span> <span data-ttu-id="9ef37-152">Es wird empfohlen, die Fabric Core-Formatvorlagen aus dem Fabric React-Paket anstelle des Pakets „sp-office-ui-fabric-core“ zu importieren, um sicherzustellen, dass die richtigen Formatvorlagen in Ihrer Komponente verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-152">It is recommended to import the Fabric Core styles from the Fabric React package instead of the sp-office-ui-fabric-core package to ensure the right styles are used in your component.</span></span> 

<span data-ttu-id="9ef37-153">Da das Paket „sp-office-ui-fabric-core“ bereits in Ihrer Lösung vom Yeoman-Generator installiert wurde, empfiehlt es sich, das Paket zu deinstallieren, wenn Sie Fabric-Komponenten verwenden und die Größe des Komponentenbundles reduzieren möchten.</span><span class="sxs-lookup"><span data-stu-id="9ef37-153">Since the sp-office-ui-fabric-core package is already installed in your solution by the yeoman generator, it is recommended to uninstall that package if you decide to use Fabric Components and reduce your component bundle size.</span></span>

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="9ef37-154">Anschließend können Sie die wichtigsten Formatvorlagen aus den SASS-Deklarationen importieren, die im Fabric React-Paket verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="9ef37-154">Then you can import the core styles from the SASS declarations available in the Fabric React packge.</span></span>

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a><span data-ttu-id="9ef37-155">Grundlegendes zu diesem Ansatz und Nachteile</span><span class="sxs-lookup"><span data-stu-id="9ef37-155">Understanding this approach and its shortcomings:</span></span>

<span data-ttu-id="9ef37-156">Fabric-Komponenten in Ihrer Lösung sind mit dieser bestimmten installierten Version von Fabric React verbunden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-156">Fabric Components in your solution are locked to that specific version of Fabric React you installed.</span></span> <span data-ttu-id="9ef37-157">Sie müssen das Fabric React-Paket aktualisieren, um neue Komponenten zu verwenden, falls diese in einer neueren Paketversion zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="9ef37-157">You will need to update the Fabric React package to get any new components if they are available in a newer package version.</span></span> <span data-ttu-id="9ef37-158">Da Fabric-Komponenten im Komponentenbundle enthalten sind, wird dadurch möglicherweise Ihr Komponentenbundle größer.</span><span class="sxs-lookup"><span data-stu-id="9ef37-158">Since the Fabric Components are included in the component bundle, it may increase the size of your component bundle.</span></span> <span data-ttu-id="9ef37-159">Dies ist der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in den SharePoint-Framework-Lösungen unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="9ef37-159">However, this approach is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>


## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="9ef37-160">Weitere Informationen zu dem CSS-Problem in Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="9ef37-160">Additional Details on the CSS Challenge with Office UI Fabric</span></span>
<span data-ttu-id="9ef37-161">Die folgenden Konzepte und Verweise liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext clientseitiger Webparts.</span><span class="sxs-lookup"><span data-stu-id="9ef37-161">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

<span data-ttu-id="9ef37-p108">**Globale CSS-Formatvorlagen** und wie diese unbedingt vermieden werden: Dies stellt ein großes Problem dar. Heute weisen sowohl Fabric Core als auch Fabric React globale Formatvorlagen auf. Aufgrund eines Mangels systemeigener Lösungen vom Browser zum Verwalten der Bereichsdefinition der Formatvorlagen ist dies ein schwerwiegendes Problem.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p108">**Global CSS styles** and how to avoid them at all cost: this is a big problem. Today, both Fabric Core and Fabric React have global styles. Lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="9ef37-165">[Die Bereichsdefinition von CSS](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) erfolgt in den frühen Phasen der Besprechung.</span><span class="sxs-lookup"><span data-stu-id="9ef37-165">[Scope CSS](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) is in early stages of discussion.</span></span> 
  - <span data-ttu-id="9ef37-166">iFrames sind keine gute Option zum Isolieren von Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="9ef37-166">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="9ef37-167">[Webkomponenten](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht, der sich aber noch in der Besprechungsphase befindet.</span><span class="sxs-lookup"><span data-stu-id="9ef37-167">[Web Components](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
  - <span data-ttu-id="9ef37-p109">In [dieser](https://speakerdeck.com/vjeux/react-css-in-js) Diskussion wird das Problem gut erläutert. Es gibt zahlreiche andere Dokumentationen im Web über die Lösungen für das Problem mit dem globalen Namespace.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p109">[This](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>
 
<span data-ttu-id="9ef37-p110">**[CSS-Genauigkeit](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity)** und wie diese auf Webbenutzeroberflächen angewendet wird. Formatvorlagen mit höherer Genauigkeit setzen die Formatvorlagen mit niedrigerer Genauigkeit außer Kraft.  Das Wichtigste ist jedoch, dass Sie verstehen, wie die Genauigkeitsregeln angewendet werden. Im Allgemeinen ist die Rangfolge von oben nach unten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="9ef37-p110">**[CSS Specificity](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity)** and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="9ef37-173">Das Style-Attribut (z. B. `style="background:red;"`)</span><span class="sxs-lookup"><span data-stu-id="9ef37-173">The style attribute (e.g. `style="background:red;"`)</span></span>
  - <span data-ttu-id="9ef37-174">ID-Selektoren (z. B. `#myDiv { }`)</span><span class="sxs-lookup"><span data-stu-id="9ef37-174">Id selectors (e.g. `#myDiv { }`)</span></span>
  - <span data-ttu-id="9ef37-175">Klassenselektoren (z. B. `.myCssClass{}`), Attributselektoren (z. B. `[type="radio"]`) und Pseudoselektoren (z. B. `:hover`)</span><span class="sxs-lookup"><span data-stu-id="9ef37-175">Class selectors (e.g. `.myCssClass{}`), attributre selectors (e.g. `[type="radio"]`), and pseudo-classes (e.g. `:hover`)</span></span>
  - <span data-ttu-id="9ef37-176">Typselektoren (z.B. `h1`)</span><span class="sxs-lookup"><span data-stu-id="9ef37-176">Type selectors (e.g. `h1`)</span></span>

<span data-ttu-id="9ef37-p111">***Ladereihenfolge*** – Wenn zwei Klassen auf ein Element angewendet werden und diese dieselbe Genauigkeit aufweisen, hat die Klasse Vorrang, die später geladen wird. Wie im folgenden Code dargestellt, wird die Schaltfläche rot angezeigt. Wenn die Reihenfolge der Styletags geändert wird, wird die Schaltfläche grün angezeigt. Dies ist ein wichtiges Konzept. Wenn es nicht korrekt verwendet wird, kann die Benutzerfreundlichkeit von der Ladereihenfolge abhängig sein, d.h. sie wird inkonsistent.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p111">***Loading order*** - If two classes are applied on an element and they have the same specificity, the class that is loaded later takes precedence. As shown in the code below, the button will appear red. If the order of the style tags is changed, the button will appear green. This is an important concept, and if not used correctly, the user experience can become load order dependent (i.e. inconsistent).</span></span>

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

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="9ef37-181">Andere in Erwägung gezogene und verworfene Ansätze</span><span class="sxs-lookup"><span data-stu-id="9ef37-181">Other Approaches Considered and Discarded</span></span>
<span data-ttu-id="9ef37-182">Nachfolgend finden Sie weitere Informationen zu den anderen Ansätzen, die in Betracht gezogen, aber dann verworfen wurden, weil damit die wichtigsten Ziele, und zwar, dass Drittanbieterentwickler Office UI Fabric-Formatvorlagen sicher verwenden können, nicht erreicht wurden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-182">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

<span data-ttu-id="9ef37-183">**Office UI Fabric Core**</span><span class="sxs-lookup"><span data-stu-id="9ef37-183">**Office UI Fabric Core**</span></span>

<span data-ttu-id="9ef37-p112">Der Webpartentwickler muss nicht explizit etwas tun, damit die Bereichsdefinition funktioniert. Wir planen, dieses Problem über die CSS-Genauigkeit und einen Nachfolgerselektor zu beheben. Das Fabric Core-Team wird mehrere Kopien von Fabric Core-CSS-Dateien ausliefern, z. B. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p112">The web part developer would not be required to do anything explicitly to get the scoping to work. We planned to solve this problem through CSS specificity and descendant selectors. The Fabric Core team would ship multiple copies of Fabric Core css. e.g. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span></span>

<span data-ttu-id="9ef37-p113">Alle Formatvorlagen in den bereichsbezogenen CSS-Dateien befinden sich innerhalb eines Nachfolgerselektors, z. B. `"ms-Fabric-core--v6 ms-Icon--List"`. Zur Kompilierzeit erfassen die Tools die Version von Office UI Fabric Core, mit der das Webpart erstellt wurde. Bei dieser Version kann es sich um die Version handeln, die mit SPFx geliefert wird. Webpartentwickler können alternativ eine explizite Abhängigkeit von einer bestimmten Version von Office-UI-Fabric Core in ihrer**package.json**-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p113">All the styles in the scoped CSS files would be inside a descendant selector e.g. `"ms-Fabric-core--v6 ms-Icon--List"`. At compile time, the tooling would collect the version of the Office UI Fabric Core the web part was built with. This version could be the one that comes with SPFx. Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="9ef37-p114">Das Webpart-Div wird diesem Bereich zugewiesen, d. h. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Das Framework lädt die spezifische Hauptversion der bereichsbezogenen Fabric Core-CSS-Datei. Wenn das Webpart mit Version 6.0.0 von Fabric Core-CSS erstellt wurde, lädt das Framework `fabric-6-scoped.css` zur Ladezeit des Webparts herunter.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p114">The web part div would be assigned this scope i.e. `<div data-sp-webpart class="ms-Fabric-core--v6">`. The framework would load the specific major version of the Fabric core scoped CSS file. If the web part was built with version 6.0.0 of Fabric core CSS, the framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="9ef37-p115">Der Rest der Seite enthält nicht bereichsbezogenen Office UI Fabric Core-Formatvorlagen. Auf diese Weise erhält das bereichsbezogene CSS Vorrang innerhalb des Webpart-Div, wie in den CSS-Genauigkeitsregeln festgelegt. Das Webpart und sein Inhalt werden auf die Version von Office UI Fabric Core abgestimmt, die der Entwickler ausgewählt hat.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p115">The rest of the page would contain unscoped Office UI Fabric Core styles. This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div. The web part and its contents would align to the specific version of the Office UI Fabric Core the developer had chosen.</span></span>

<span data-ttu-id="9ef37-197">Das **Außerkraftsetzen** von Fabric Core-Formatvorlagen wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9ef37-197">**Overriding** Fabric Core styles would not be supported.</span></span>  

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

<span data-ttu-id="9ef37-198">Nach längerer Analyse dieser Strategie wurde festgestellt, dass der Ansatz mit dem Nachfolgerselektor zwei wesentliche Nachteile hat, aufgrund derer es nicht möglich ist, ein Webpart zu erstellen, das niemals beschädigt wird.</span><span class="sxs-lookup"><span data-stu-id="9ef37-198">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

<span data-ttu-id="9ef37-p116">**Keine zuverlässige Unterstützung für Schachtelung** – Dieser Ansatz funktioniert nur, wenn die Microsoft-Benutzeroberfläche (d. h. die Seite und alle Erstanbieter-Webparts) eine nicht bereichsbezogene Version von Office UI Fabric Core verwenden (z. B. `ms-Icon--List`) und wenn die Drittanbieter-Webparts nur bereichsbezogenes Office UI Fabric Core-CSS wie oben erläutert verwenden. Der Grund hierfür ist, dass die Genauigkeit des bereichsbezogenen CSS, das auf das Webpart angewendet wird, das nicht bereichsbezogene CSS auf der Seite außer Kraft setzt. Beachten Sie: Wie oben erläutert gilt, dass, wenn die CSS-Genauigkeit von zwei Klassen gleich ist, ihre Ladereihenfolge eine Rolle für die Anwendung der CSS-Klassen spielt. Die Klasse, die später geladen wird, hat Vorrang. Die höhere Genauigkeit des bereichsbezogenen CSS ist daher wichtig, um eine konsistente Oberfläche zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p116">**Lack of reliable nesting support** - This approach only works if the Microsoft user experience (i.e. page and first party web parts) use an unscoped version of the Office UI Fabric Core. i.e. `ms-Icon--List` while the third party web parts only use scoped Office UI Fabric Core css as explained above. The reason being that the specificity of the scoped CSS applied on the web part overrides unscoped CSS on the page. Keep in mind, as explained above, if CSS specificity of two classes is the same, then their loading order plays a role in how the CSS classes will be applied. The class that loads later will take precedence. Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="9ef37-p117">Darüber hinaus können mehrere Erweiterungen, von denen eine jeweils in der anderen enthalten ist, nicht unterschiedliche Fabric Core-Versionen verwenden, d. h. im folgenden Beispiel wird nur `ms-Fabric-core--v6` angewendet:</span><span class="sxs-lookup"><span data-stu-id="9ef37-p117">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<span data-ttu-id="9ef37-207">Nachfolgend finden Sie ein einfacheres Beispiel, in dem das Problem erläutert wird:</span><span class="sxs-lookup"><span data-stu-id="9ef37-207">Here's a more simplistic sample demonstrating the challenge:</span></span>

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

<span data-ttu-id="9ef37-p118">**Offenlegung von nicht bereichsbezogenen Klassen** – Es gibt ein weiteres Problem mit Nachfolgerselektoren. Beachten Sie im obigen Beispiel, dass die Formatvorlagen für Höhe und Breite aus der nicht bereichsbezogenen myButton-Klasse auf alle Schaltflächen angewendet werden. Dies impliziert, dass eine Änderung in dieser Formatvorlage die HTML, die das bereichsbezogene Markup verwendet, versehentlich beschädigen könnte. Nehmen wir beispielsweise an, dass wir die Höhe auf App-Ebene auf 0px in der myButton-Klasse festlegen. Dies führt dazu, dass alle Drittanbieter-Webparts, die die myButton-Klasse verwenden, eine Höhe von 0 haben, also eine wesentliche Regression in der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="9ef37-p118">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0px (i.e. a serious regression in the user experience).</span></span>


