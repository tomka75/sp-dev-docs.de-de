---
title: "Verwenden von Office UI Fabric Core und Fabric React in SharePoint-Framework"
description: "Hier finden Sie Informationen zu den Paketen Fabric Core und Fabric React sowie zu Problemen bei der Verwendung von CSS."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 9d984b1655c07d7732edd442f48dd9e253ad2b82
ms.sourcegitcommit: 53fa577acbc93bfff82c7e521b741df51e9585fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a><span data-ttu-id="b0d13-103">Verwenden von Office UI Fabric Core und Fabric React im SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="b0d13-103">Using Office UI Fabric Core and Fabric React in SharePoint Framework</span></span>

<span data-ttu-id="b0d13-p101">Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b0d13-p101">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

<span data-ttu-id="b0d13-107">Microsoft verwendet Fabric Core und Fabric React in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b0d13-107">Microsoft uses Fabric Core and Fabric React in SharePoint.</span></span> <span data-ttu-id="b0d13-108">Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, die möglicherweise auch jeweils die Version von Fabric Core und Fabric React aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b0d13-108">Microsoft regularly pushes updates to SharePoint Online which could also update the Fabric Core and Fabric React versions as well.</span></span> <span data-ttu-id="b0d13-109">Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den entsprechenden Anpassungen führen kann.</span><span class="sxs-lookup"><span data-stu-id="b0d13-109">These updates could potentially conflict with third party customer solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations.</span></span> <span data-ttu-id="b0d13-110">Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="b0d13-110">The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries.</span></span> <span data-ttu-id="b0d13-111">Solche Konflikte müssen auf jeden Fall vermieden werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-111">Such conflicts need to be avoided at all costs.</span></span> 

<span data-ttu-id="b0d13-112">Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JavaScript erläutert: [React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="b0d13-112">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

<span data-ttu-id="b0d13-113">Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss.</span><span class="sxs-lookup"><span data-stu-id="b0d13-113">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**.</span></span> <span data-ttu-id="b0d13-114">Hierzu sind statt globaler Klassennamen im HTML-Markup Fabric Core-Mixins und -Variablen in der SASS-Deklarationsdatei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-114">This accounts to not using global class names in the HTML markup and instead using Fabric Core mixins and variables in the SASS declaration file.</span></span> <span data-ttu-id="b0d13-115">Dies umfasst den Import der Fabric Core-Sass-Deklarationen in die Sass-Datei und anschließend eine entsprechende Verarbeitung der Variablen und Mixins.</span><span class="sxs-lookup"><span data-stu-id="b0d13-115">This involves importing the Fabric Core's SASS declarations in your SASS file and then consuming the variables and mixins appropriately.</span></span> 

## <a name="goals"></a><span data-ttu-id="b0d13-116">Ziele</span><span class="sxs-lookup"><span data-stu-id="b0d13-116">Goals</span></span>

<span data-ttu-id="b0d13-117">Das Ziel des SharePoint-Frameworks besteht darin, Microsoft und Kunden das Erstellen funktionsreicher, ansprechender und konsistenter Benutzeroberflächen auf SharePoint-Basis zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-117">The goal of the SharePoint Framework is to allow both Microsoft and customers build rich, beautiful, and consistent user experiences on top of SharePoint.</span></span> 

<span data-ttu-id="b0d13-118">Im Folgenden werden die wichtigsten Entwurfsprinzipien für die Umsetzung dieses Ziels erläutert:</span><span class="sxs-lookup"><span data-stu-id="b0d13-118">In accordance with these goals, below are the key design  principles:</span></span>

* <span data-ttu-id="b0d13-119">Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.</span><span class="sxs-lookup"><span data-stu-id="b0d13-119">Customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="b0d13-120">Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-120">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="b0d13-121">Kunden können die Standardformatvorlagen, -designs und -komponenten gemäß den Anforderungen ihrer Lösung anpassen und überschreiben.</span><span class="sxs-lookup"><span data-stu-id="b0d13-121">Customers can customize and override the default styles, designs, and components to tailor the solution's needs.</span></span>

<span data-ttu-id="b0d13-122">Es gibt zwei Teile von Office UI Fabric, die Entwicklern zur Verfügung stehen:</span><span class="sxs-lookup"><span data-stu-id="b0d13-122">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

* <span data-ttu-id="b0d13-123">[Office UI Fabric Core](https://developer.microsoft.com/de-DE/fabric):</span><span class="sxs-lookup"><span data-stu-id="b0d13-123">[Office UI Fabric Core](https://developer.microsoft.com/de-DE/fabric)</span></span> <span data-ttu-id="b0d13-124">Hierbei handelt es sich um einen Satz von grundlegenden Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen Basisbausteinen der gesamten Entwurfssprache.</span><span class="sxs-lookup"><span data-stu-id="b0d13-124">A set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

* <span data-ttu-id="b0d13-125">[Office UI Fabric React](https://developer.microsoft.com/de-DE/fabric#/components):</span><span class="sxs-lookup"><span data-stu-id="b0d13-125">[Office UI Fabric React](https://developer.microsoft.com/de-DE/fabric#/components)</span></span> <span data-ttu-id="b0d13-126">Hierbei handelt es sich um eine Reihe von React-Komponenten, die auf der Fabric-Entwurfssprache aufbauen und in React-basierten Projekten verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="b0d13-126">A set of React components built on top of the Fabric design language for use in React-based projects.</span></span>

## <a name="office-ui-fabric-core-package"></a><span data-ttu-id="b0d13-127">Office UI Fabric Core-Paket</span><span class="sxs-lookup"><span data-stu-id="b0d13-127">Office UI Fabric Core</span></span>

<span data-ttu-id="b0d13-128">Das Fabric Core-npm-Paket für das SharePoint-Framework (sp-office-ui-fabric-core) enthält eine Teilmenge der unterstützten Fabric Core-Formatvorlagen, die ohne Sicherheitsrisiko in SharePoint-Framework-Komponenten verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="b0d13-128">The SPFx Fabric Core npm package - sp-office-ui-fabric-core - contains a subset of supported Fabric Core styles that can be safely consumed within a SharePoint Framework component.</span></span> 

<span data-ttu-id="b0d13-129">Die folgenden grundlegenden Formatvorlagen werden in dem Paket unterstützt:</span><span class="sxs-lookup"><span data-stu-id="b0d13-129">The following core styles are supported in the package:</span></span>
- <span data-ttu-id="b0d13-130">Typografie</span><span class="sxs-lookup"><span data-stu-id="b0d13-130">Typography</span></span>
- <span data-ttu-id="b0d13-131">Layouts</span><span class="sxs-lookup"><span data-stu-id="b0d13-131">Layouts</span></span>
- <span data-ttu-id="b0d13-132">Farben</span><span class="sxs-lookup"><span data-stu-id="b0d13-132">Colors</span></span>
- <span data-ttu-id="b0d13-133">Designs</span><span class="sxs-lookup"><span data-stu-id="b0d13-133">Themes</span></span>
- <span data-ttu-id="b0d13-134">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="b0d13-134">Localization</span></span>

<span data-ttu-id="b0d13-135">Folgendes wird in dem Paket noch nicht unterstützt:</span><span class="sxs-lookup"><span data-stu-id="b0d13-135">The following are not yet supported in the package:</span></span>
- <span data-ttu-id="b0d13-136">Animationen</span><span class="sxs-lookup"><span data-stu-id="b0d13-136">Animations</span></span>
- <span data-ttu-id="b0d13-137">Symbole</span><span class="sxs-lookup"><span data-stu-id="b0d13-137">Icons</span></span>

<span data-ttu-id="b0d13-138">Ab Version 1.3.4 des SharePoint-Framework-Yeoman-Generators enthalten die Standardprojektvorlagen (Webparts und Erweiterungen) das neue Paket „sp-office-ui-fabric-core“ und nutzen statt globaler CSS-Formatvorlagen grundlegende Formatvorlagen aus diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="b0d13-138">Starting with the SharePoint Framework yeoman generator version 1.3.4, the default project (web parts and extensions) templates will come setup with the new sp-office-ui-fabric-core package and consume core styles from the package instead of using global CSS styles.</span></span> 

### <a name="update-existing-projects"></a><span data-ttu-id="b0d13-139">Aktualisieren bereits vorhandener Projekte</span><span class="sxs-lookup"><span data-stu-id="b0d13-139">Update existing projects</span></span>

<span data-ttu-id="b0d13-140">Um das Fabric Core-Paket in einem vorhandenen Projekt verwenden zu können, müssen Sie das Paket als Entwicklerabhängigkeit installieren:</span><span class="sxs-lookup"><span data-stu-id="b0d13-140">To use the SPFx Fabric Core package in your existing project, install the package as dev dependency:</span></span>

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="b0d13-141">Nach Abschluss der Installation können Sie die Fabric Core-Sass-Deklarationen in die Sass-Definitionsdatei importieren und die Mixins und Variablen wie im folgenden Abschnitt beschrieben verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-141">Once installed, you can then import the Fabric Core SASS declarations in your SASS defintion file and use the mixins and variables as decribed in the section below.</span></span> 

### <a name="use-fabric-core-styles"></a><span data-ttu-id="b0d13-142">Verwenden von Fabric Core-Formatvorlagen</span><span class="sxs-lookup"><span data-stu-id="b0d13-142">Using Fabric Core styles</span></span>

<span data-ttu-id="b0d13-143">Um die Fabric Core-Formatvorlagen verwenden zu können, müssen Sie die SPFabricCore-Deklarationen in Ihre Sass-Datei importieren.</span><span class="sxs-lookup"><span data-stu-id="b0d13-143">In order to use the Fabric Core styles first you will need to import the SPFabricCore declarations in your SASS file.</span></span>

> [!NOTE] 
> <span data-ttu-id="b0d13-144">Vergewissern Sie sich, dass das npm-Paket „sp-office-ui-fabric-core“ installiert ist.</span><span class="sxs-lookup"><span data-stu-id="b0d13-144">Note: Make sure you have the sp-office-ui-fabric-core npm package installed.</span></span>

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

<br/>

<span data-ttu-id="b0d13-145">Jetzt können Sie die grundlegenden Formatvorlagen als Mixins und Variablen verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-145">Now, you can use the core styles as mixins and variables.</span></span>

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="office-ui-fabric-react"></a><span data-ttu-id="b0d13-146">Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="b0d13-146">Office UI Fabric React</span></span>

<span data-ttu-id="b0d13-147">Wir empfehlen, das neueste Office UI Fabric React-Paket zu installieren und eine explizite Abhängigkeit von dieser spezifischen Version des Pakets zu setzen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-147">It is recommended to install the latest Office UI Fabric React package and place an explicit dependency on that specific version of the package.</span></span> <span data-ttu-id="b0d13-148">Dies umfasst die in der SharePoint-Framework-Lösung verwendeten Komponenten in Ihrem Komponentenbundle, entweder Webpart oder Erweiterung, je nachdem wo Sie die Fabric React-Komponenten verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-148">This will include the components used in your SPFx solution in your component bundle, either the web part or extension depending on where you use the Fabric React components.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b0d13-149">Die Version 2.x von Fabric React sowie ältere Versionen werden im SharePoint-Framework nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b0d13-149">Please note that Fabric React versions 2.x or older are not supported in SharePoint Framework.</span></span>

<span data-ttu-id="b0d13-150">Nach der Installation des Fabric React-Pakets können Sie die erforderlichen Komponenten aus dem Fabric React-Paket importieren.</span><span class="sxs-lookup"><span data-stu-id="b0d13-150">Once the Fabric React package is installed, you can import the required components from the Fabric React bundle.</span></span>

```js
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

<span data-ttu-id="b0d13-151">Das Fabric React-Paket enthält die unterstützten Fabric Core-Formatvorlagen, die in den Fabric React-Komponenten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-151">Fabric React package includes the supported Fabric Core styles used in the Fabric React components.</span></span> <span data-ttu-id="b0d13-152">Wir empfehlen, die Fabric Core-Formatvorlagen aus dem Fabric React-Paket zu importieren, nicht aus dem Paket „sp-office-ui-fabric-core“. So ist sichergestellt, dass in Ihrer Komponente die korrekten Formatvorlagen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-152">It is recommended to import the Fabric Core styles from the Fabric React package instead of the sp-office-ui-fabric-core package to ensure the right styles are used in your component.</span></span> 

<span data-ttu-id="b0d13-153">Da das Paket „sp-office-ui-fabric-core“ bereits vom Yeoman-Generator in Ihrer Lösung installiert wurde, empfehlen wir, dieses Paket zu deinstallieren, wenn Sie Fabric-Komponenten verwenden und die Größe des Komponentenbundles reduzieren möchten.</span><span class="sxs-lookup"><span data-stu-id="b0d13-153">Since the sp-office-ui-fabric-core package is already installed in your solution by the yeoman generator, it is recommended to uninstall that package if you decide to use Fabric Components and reduce your component bundle size.</span></span>

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="b0d13-154">Anschließend können Sie die grundlegenden Formatvorlagen aus den Sass-Deklarationen importieren, die im Fabric React-Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="b0d13-154">Then you can import the core styles from the SASS declarations available in the Fabric React package .</span></span>

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a><span data-ttu-id="b0d13-155">Grundlegendes zu diesem Ansatz und seinen Nachteilen</span><span class="sxs-lookup"><span data-stu-id="b0d13-155">Understanding this approach and its shortcomings</span></span>

<span data-ttu-id="b0d13-156">Fabric-Komponenten in Ihrer Lösung sind an die spezifische Fabric React-Version gebunden, die Sie installiert haben.</span><span class="sxs-lookup"><span data-stu-id="b0d13-156">Fabric Components in your solution are locked to that specific version of Fabric React you installed.</span></span> <span data-ttu-id="b0d13-157">Wenn Sie neue Komponenten aus einer neueren Version des Pakets verwenden möchten, müssen Sie das Fabric React-Paket aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b0d13-157">You will need to update the Fabric React package to get any new components if they are available in a newer package version.</span></span> <span data-ttu-id="b0d13-158">Da die Fabric-Komponenten im Komponentenbundle enthalten sind, wird Ihr Komponentenbundle dadurch möglicherweise größer.</span><span class="sxs-lookup"><span data-stu-id="b0d13-158">Since the Fabric Components are included in the component bundle, it may increase the size of your component bundle.</span></span> <span data-ttu-id="b0d13-159">Dies ist jedoch der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in SharePoint-Framework-Lösungen unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="b0d13-159">However, this approach is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>


## <a name="the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="b0d13-160">Das CSS-Problem in Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="b0d13-160">Additional details on the CSS challenge with Office UI Fabric</span></span>

<span data-ttu-id="b0d13-161">Die folgenden Konzepte und Ressourcen liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext von clientseitigen Webparts.</span><span class="sxs-lookup"><span data-stu-id="b0d13-161">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

### <a name="global-css-styles"></a><span data-ttu-id="b0d13-162">Globale CSS-Formatvorlagen</span><span class="sxs-lookup"><span data-stu-id="b0d13-162">Global CSS styles</span></span>

<span data-ttu-id="b0d13-163">Es ist sehr schwierig, den Einsatz globaler CSS-Formatvorlagen komplett zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-163">How to avoid Global CSS styles at all costs is a big problem.</span></span> <span data-ttu-id="b0d13-164">Aktuell nutzen sowohl Fabric Core als auch Fabric React globale Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-164">Today, both Fabric Core and Fabric React have global styles.</span></span> <span data-ttu-id="b0d13-165">Da Browser keine nativen Lösungen für die Verwaltung der Bereichsdefinitionen von Formatvorlagen mitbringen, ist das ein schwerwiegendes Problem.</span><span class="sxs-lookup"><span data-stu-id="b0d13-165">A lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="b0d13-166">Die Diskussion um [CSS-Bereiche](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) steht noch ganz am Anfang.</span><span class="sxs-lookup"><span data-stu-id="b0d13-166">[Scope CSS](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) is in early stages of discussion.</span></span>
  - <span data-ttu-id="b0d13-167">iFrames sind keine gute Option zur Isolierung von Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-167">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="b0d13-168">[Webkomponenten](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht. Auch hier befindet man sich jedoch noch ganz am Anfang der Diskussion.</span><span class="sxs-lookup"><span data-stu-id="b0d13-168">[Web Components](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
  - <span data-ttu-id="b0d13-169">Die Präsentation [React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js) erläutert das Problem anschaulich.</span><span class="sxs-lookup"><span data-stu-id="b0d13-169">[The React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well.</span></span> 
  
<span data-ttu-id="b0d13-170">Es gibt zahlreiche weitere Dokumentationen im Web, die sich Lösungen für das Problem globaler Namespace gewidmet haben.</span><span class="sxs-lookup"><span data-stu-id="b0d13-170">This discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>

### <a name="css-specificity"></a><span data-ttu-id="b0d13-171">CSS-Spezifität</span><span class="sxs-lookup"><span data-stu-id="b0d13-171">CSS specificity</span></span>

<span data-ttu-id="b0d13-172">In [diesem Artikel zum Thema CSS-Spezifität](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity) erfahren Sie, wie das Konzept auf Webbenutzeroberflächen angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="b0d13-172">How [CSS specificity](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity) applies to web UI.</span></span> <span data-ttu-id="b0d13-173">Formatvorlagen mit höherer Spezifität überschreiben Formatvorlagen mit niedrigerer Spezifität. Am wichtigsten ist es jedoch, dass Sie verstehen, wie die Spezifitätsregeln angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-173">CSS Specificity and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span> <span data-ttu-id="b0d13-174">Im Allgemeinen lautet die Rangfolge von der höchsten zur niedrigsten Formatvorlage wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b0d13-174">In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="b0d13-175">Attribut „style“ (zum Beispiel `style="background:red;"`)</span><span class="sxs-lookup"><span data-stu-id="b0d13-175">The style attribute (for example, `style="background:red;"`)</span></span>
  - <span data-ttu-id="b0d13-176">ID-Selektoren (`#myDiv { }`)</span><span class="sxs-lookup"><span data-stu-id="b0d13-176">ID selectors (`#myDiv { }`)</span></span>
  - <span data-ttu-id="b0d13-177">Klassenselektoren (`.myCssClass{}`), Attributselektoren (`[type="radio"]`) und Pseudoklassen (`:hover`)</span><span class="sxs-lookup"><span data-stu-id="b0d13-177">Class selectors (`.myCssClass{}`), attribute selectors (`[type="radio"]`), and pseudo-classes (`:hover`)</span></span>
  - <span data-ttu-id="b0d13-178">Typselektoren (`h1`)</span><span class="sxs-lookup"><span data-stu-id="b0d13-178">Type selectors (`h1`)</span></span>

<span data-ttu-id="b0d13-179">**Ladereihenfolge:**</span><span class="sxs-lookup"><span data-stu-id="b0d13-179">**Loading order**.</span></span> <span data-ttu-id="b0d13-180">Wenn zwei Klassen auf ein Element angewendet werden und diese Klassen dieselbe Spezifität aufweisen, hat die Klasse Vorrang, die später geladen wird.</span><span class="sxs-lookup"><span data-stu-id="b0d13-180">If two classes are applied on an element and have the same specificity, the class that is loaded later takes precedence.</span></span> <span data-ttu-id="b0d13-181">Wie im nachfolgenden Code ersichtlich, wird die Schaltfläche rot angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0d13-181">As shown in the following code, the button appears red.</span></span> <span data-ttu-id="b0d13-182">Wenn die Reihenfolge der „style“-Tags geändert wird, wird die Schaltfläche grün angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0d13-182">If the order of the style tags is changed, the button appears green.</span></span> <span data-ttu-id="b0d13-183">Dies ist ein wichtiges Konzept. Wenn es nicht korrekt angewendet wird, kann die Benutzeroberfläche abhängig von der Ladereihenfolge werden (d. h., sie wird inkonsistent).</span><span class="sxs-lookup"><span data-stu-id="b0d13-183">This is an important concept, and if not used correctly, the user experience can become load order-dependent (that is, inconsistent).</span></span>

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

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="b0d13-184">Andere in Erwägung gezogene und verworfene Ansätze</span><span class="sxs-lookup"><span data-stu-id="b0d13-184">Other approaches considered and discarded</span></span>

<span data-ttu-id="b0d13-185">Nachfolgend finden Sie weitere Informationen zu den anderen Ansätzen, die in Betracht gezogen, aber dann verworfen wurden, weil mit ihnen das wichtigste Ziele nicht erreicht werden konnte: Drittanbietern die risikofreie Verwendung der Office UI Fabric-Formatvorlagen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-185">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

### <a name="office-ui-fabric-core"></a><span data-ttu-id="b0d13-186">Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="b0d13-186">Office UI Fabric Core</span></span>

<span data-ttu-id="b0d13-187">Webpartentwickler müssen nicht explizit etwas tun, damit Bereichsdefinitionen funktionieren.</span><span class="sxs-lookup"><span data-stu-id="b0d13-187">The web part developer would not be required to do anything explicitly to get the scoping to work.</span></span> <span data-ttu-id="b0d13-188">Wir wollten dieses Problem mithilfe von CSS-Spezifität und Nachfolgerselektoren lösen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-188">We planned to solve this problem through CSS specificity and descendant selectors.</span></span> <span data-ttu-id="b0d13-189">Dazu stellte das Fabric Core-Team mehrere Versionen von Fabric Core-CSS-Dateien bereit (zum Beispiel `fabric-6.css`, `fabric-6-scoped.css`,`fabric-6.0.0.css` und `fabric-6.0.0-scoped.css`).</span><span class="sxs-lookup"><span data-stu-id="b0d13-189">The Fabric Core team would ship multiple copies of Fabric Core css (for example, `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`).</span></span>

<span data-ttu-id="b0d13-190">Alle Formatvorlagen in den bereichsbezogenen CSS-Dateien befanden sich innerhalb eines Nachfolgerselektors, zum Beispiel `"ms-Fabric-core--v6 ms-Icon--List"`.</span><span class="sxs-lookup"><span data-stu-id="b0d13-190">All the styles in the scoped CSS files would be inside a descendant selector, for example `"ms-Fabric-core--v6 ms-Icon--List"`.</span></span> <span data-ttu-id="b0d13-191">Zur Kompilierzeit erfassten die Tools die Version von Office UI Fabric Core, mit der das Webpart erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="b0d13-191">At compile time, the tooling would collect the version of the Office UI Fabric Core that the web part was built with.</span></span> <span data-ttu-id="b0d13-192">Bei dieser Version konnte es sich um die mit dem SharePoint-Framework bereitgestellte Version handeln.</span><span class="sxs-lookup"><span data-stu-id="b0d13-192">This version could be the one that comes with SharePoint Framework.</span></span> <span data-ttu-id="b0d13-193">Alternativ konnten Webpartentwickler eine explizite Abhängigkeit von einer bestimmten Office UI Fabric Core-Version in ihrer Datei **package.json** setzen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-193">Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="b0d13-194">Dem Webpart-Div wurde dann der entsprechende Bereich zugewiesen, also `<div data-sp-webpart class="ms-Fabric-core--v6">`.</span><span class="sxs-lookup"><span data-stu-id="b0d13-194">The web part div would be assigned this scope, that is `<div data-sp-webpart class="ms-Fabric-core--v6">`.</span></span> <span data-ttu-id="b0d13-195">Das Framework lud die spezifische Hauptversion der Fabric Core-bezogenen CSS-Datei.</span><span class="sxs-lookup"><span data-stu-id="b0d13-195">The Framework would load the specific major version of the Fabric Core-scoped CSS file.</span></span> <span data-ttu-id="b0d13-196">Wurde das Webpart mit Version 6.0.0 des Fabric Core-CSS-Codes erstellt, lud das Framework die Datei `fabric-6-scoped.css` herunter, sobald das Webpart geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="b0d13-196">If the web part was built with version 6.0.0 of the Fabric Core CSS, the Framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="b0d13-197">Der Rest der Seite enthielt nicht bereichsbezogene Office UI Fabric Core-Formatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-197">The rest of the page would contain unscoped Office UI Fabric Core styles.</span></span> <span data-ttu-id="b0d13-198">Auf diese Weise erhielt der bereichsbezogene CSS-Code gemäß den CSS-Spezifitätsregeln Vorrang innerhalb des Webpart-DIV.</span><span class="sxs-lookup"><span data-stu-id="b0d13-198">This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div.</span></span> <span data-ttu-id="b0d13-199">Das Webpart und sein Inhalt wurden an die Office UI Fabric Core-Version angepasst, die der Entwickler ausgewählt hatte.</span><span class="sxs-lookup"><span data-stu-id="b0d13-199">The web part and its contents would align to the specific version of the Office UI Fabric Core that the developer had chosen.</span></span>

<span data-ttu-id="b0d13-200">Eine *Überschreibung* von Fabric Core-Formatvorlagen wurde nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b0d13-200">*Overriding* Fabric Core styles would not be supported.</span></span>  

```js
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

### <a name="shortcomings-of-this-strategy"></a><span data-ttu-id="b0d13-201">Nachteile dieser Strategie</span><span class="sxs-lookup"><span data-stu-id="b0d13-201">Shortcomings of this strategy</span></span>

<span data-ttu-id="b0d13-202">Nach längerer Analyse dieser Strategie stellten wir fest, dass die Verwendung von Nachfolgerselektoren zwei wesentliche Nachteile hat, aufgrund derer es nicht möglich ist, ein gegen Fehler immunes Webpart zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-202">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

#### <a name="lack-of-reliable-nesting-support"></a><span data-ttu-id="b0d13-203">Keine zuverlässige Unterstützung für Schachtelung</span><span class="sxs-lookup"><span data-stu-id="b0d13-203">Lack of reliable nesting support</span></span>

<span data-ttu-id="b0d13-204">Dieser Ansatz funktioniert nur, wenn die Microsoft-Benutzeroberfläche (d. h. die Seite und alle Erstanbieter-Webparts) eine nicht bereichsbezogene Version von Office UI Fabric Core verwenden (z. B. `ms-Icon--List`) und wenn die Drittanbieter-Webparts nur bereichsbezogenen Office UI Fabric Core-CSS-Code verwenden (siehe oben).</span><span class="sxs-lookup"><span data-stu-id="b0d13-204">This approach only works if the Microsoft user experience (that is, page and first-party web parts) use an unscoped version of the Office UI Fabric Core such as `ms-Icon--List`, while the third-party web parts only use scoped Office UI Fabric Core CSS as explained earlier.</span></span> 

<span data-ttu-id="b0d13-205">Der Grund hierfür ist, dass die Spezifität des bereichsbezogenen CSS-Codes, der auf das Webpart angewendet wird, den nicht bereichsbezogenen CSS-Code auf der Seite überschreibt.</span><span class="sxs-lookup"><span data-stu-id="b0d13-205">The reason being that the specificity of the scoped CSS applied on the web part overrides the unscoped CSS on the page.</span></span> <span data-ttu-id="b0d13-206">Wie weiter oben erläutert: Wenn die CSS-Spezifität von zwei CSS-Klassen identisch ist, entscheidet die Ladereihenfolge der Klassen darüber, wie sie angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-206">Keep in mind, as explained earlier, that if CSS specificity of the two classes is the same, their loading order plays a role in how the CSS classes are applied.</span></span> <span data-ttu-id="b0d13-207">Die Klasse, die später geladen wird, hat Vorrang.</span><span class="sxs-lookup"><span data-stu-id="b0d13-207">The class that loads later takes precedence.</span></span> <span data-ttu-id="b0d13-208">Die höhere Spezifität des bereichsbezogenen CSS-Codes ist daher wichtig, um eine konsistente Oberfläche zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b0d13-208">Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="b0d13-209">Darüber hinaus können mehrere ineinander geschachtelte Erweiterungen nicht jeweils eine andere Version von Fabric Core verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-209">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only  would get applied:</span></span> <span data-ttu-id="b0d13-210">Im folgenden Beispiel würde ausschließlich `ms-Fabric-core--v6` angewendet werden:</span><span class="sxs-lookup"><span data-stu-id="b0d13-210">In the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<br/>

<span data-ttu-id="b0d13-211">Unten sehen Sie ein einfacheres Beispiel zur Veranschaulichung des Problems:</span><span class="sxs-lookup"><span data-stu-id="b0d13-211">Here's a more simplistic sample demonstrating the challenge:</span></span>

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

#### <a name="leakage-from-unscoped-classes"></a><span data-ttu-id="b0d13-212">Übersprung aus nicht bereichsbezogenen Klassen</span><span class="sxs-lookup"><span data-stu-id="b0d13-212">Leakage from unscoped classes</span></span>

<span data-ttu-id="b0d13-213">Nachfolgerselektoren bergen ein weiteres Problem.</span><span class="sxs-lookup"><span data-stu-id="b0d13-213">There is another problem with descendant selectors.</span></span> <span data-ttu-id="b0d13-214">Wie Sie im vorangegangenen Beispiel sehen, werden die Formatvorlagen „height“ und „width“ aus der nicht bereichsbezogenen Klasse „myButton“ auf alle Schaltflächen angewendet.</span><span class="sxs-lookup"><span data-stu-id="b0d13-214">Note in the previous example that the height and the width styles from the unscoped myButton class are applied to all the buttons.</span></span> <span data-ttu-id="b0d13-215">Das bedeutet: Würde diese Formatvorlage dahingehend verändert, dass bereichsbezogenes Markup verwendet wird, könnte dadurch versehentlich der HTML-Code beschädigt werden.</span><span class="sxs-lookup"><span data-stu-id="b0d13-215">This implies that a change in that style could inadvertently break HTML by using scoped markup.</span></span> 

<span data-ttu-id="b0d13-216">Nehmen wir beispielsweise an, wir würden aus Gründen auf App-Ebene das Attribut „height“ in der Klasse „myButton“ auf „0 px“ setzen.</span><span class="sxs-lookup"><span data-stu-id="b0d13-216">Say for example, for some reason at the app level we decide to make height 0 px on the myButton class.</span></span> <span data-ttu-id="b0d13-217">Dann würde in allen Drittanbieter-Webparts, die die Klasse „myButton“ verwenden, ein „height“-Wert von 0 px gelten. (Es würde also zu einer schwerwiegenden Regression auf der Benutzeroberfläche kommen.)</span><span class="sxs-lookup"><span data-stu-id="b0d13-217">That results in all third-party web parts that use the myButton class to have a height of 0 px (that is, a serious regression in the user experience).</span></span>

## <a name="see-also"></a><span data-ttu-id="b0d13-218">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="b0d13-218">See also</span></span>

- [<span data-ttu-id="b0d13-219">Übersicht über das SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="b0d13-219">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)




