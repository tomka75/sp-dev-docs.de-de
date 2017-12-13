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
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a>Verwenden von Office UI Fabric Core und Fabric React in SharePoint-Framework

Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.

## <a name="summary"></a>Zusammenfassung

Microsoft verwendet Fabric Core und Fabric React in SharePoint. Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, die möglicherweise auch die Fabric Core- und Fabric React-Versionen aktualisieren. Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den Anpassungen führen kann. Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken. Solche Konflikte müssen auf jeden Fall vermieden werden. 

> Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JSS ausführlich erläutert: [React-CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).

Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss. Grund hierfür ist, dass keine globalen Klassennamen im HTML-Markup verwendet werden und stattdessen Fabric Core-Mixins und -Variablen in der SASS-Deklarationsdatei verwendet werden. Dies umfasst den Import der Fabric Core-SASS-Deklarationen in die SASS-Datei und anschließend eine entsprechende Verarbeitung der Variablen und Mixins. 

## <a name="goals"></a>Ziele

Das Ziel von SharePoint-Framework besteht darin, Microsoft und Kunden das Erstellen vielfältiger, ansprechender und konsistenter Benutzeroberflächen über SharePoint hinaus zu ermöglichen. Im Folgenden werden die wichtigsten Entwurfsprinzipien entsprechend diesen Zielen erläutert:

* Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.
* Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.
* Kunden können die Standardformatvorlagen, Designs und Komponenten in Übereinstimmung mit den Anforderungen ihrer Lösung anpassen und überschreiben.

Es gibt zwei Teile von Office UI Fabric, die für Entwickler zur Verfügung stehen:

* [Office UI Fabric Core](http://dev.office.com/fabric)

  Hierbei handelt es sich um einen Satz von Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen grundlegenden Bausteinen der gesamten Entwurfssprache.

* [Office UI Fabric React](http://dev.office.com/fabric#/components)

  Hierbei handelt es sich um eine Reihe von React-Komponenten, die über die Fabric-Entwurfssprache hinaus für die Verwendung in React-basierten Projekten erstellt wurden.

## <a name="spfx-fabric-core-package"></a>SPFx Fabric Core-Paket

Das npm-Paket von SPFx Fabric Core – Fabric-Core - sp-office-ui-fabric-core – enthält eine Teilmenge der unterstützten Fabric Core-Formatvorlagen, die auf sichere Weise in einer SharePoint-Framework-Komponente verarbeitet werden können. 

Die folgenden grundlegenden Formatvorlagen werden in dem Paket unterstützt:
- Typografie
- Layouts
- Farben
- Designs
- Lokalisierung

Folgendes wird in dem Paket noch nicht unterstützt:
- Animationen
- Symbole

Ab Yeoman-Generator Version 1.3.4 von SharePoint-Framework sind standardmäßige Projektvorlagen (Webparts und Erweiterungen) im neuen Paket „sp-office-fabric-core“ eingerichtet, und es werden die grundlegenden Formatvorlagen aus dem Paket anstelle von globalen CSS-Formatvorlagen verwendet. 

### <a name="updating-existing-projects"></a>Aktualisieren bereits vorhandener Projekte

Um das SPFx Fabric Core-Paket in einem bereits vorhandenen Projekt zu verwenden, müssen Sie das Paket als dev-Abhängigkeit installieren:

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

Nach Abschluss der Installation können Sie die Fabric Core-SASS-Deklarationen in die SASS-Definitionsdatei importieren und die Mixins und Variablen wie im folgenden Abschnitt beschrieben verwenden. 

### <a name="using-fabric-core-styles"></a>Verwenden von Fabric Core-Formatvorlagen

Um die Fabric Core-Formatvorlagen zu verwenden, müssen Sie zunächst die SPFabricCore-Deklarationen in Ihre SASS-Datei importieren.

> Hinweis: Installieren Sie das npm-Paket „sp-office-ui-fabric-core“.

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

Sie können jetzt die grundlegenden Formatvorlagen sowie Mixins und Variablen verwenden.

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="using-office-ui-fabric-react"></a>Verwenden von Office UI Fabric React

Es wird empfohlen, das neueste Office UI Fabric React-Paket zu installieren und eine explizite Abhängigkeit für diese bestimmte Version des Pakets zu platzieren. Dies umfasst die in der SPFx-Lösung verwendeten Komponenten in Ihrem Komponentenbundle, entweder Webpart oder Erweiterung, je nachdem wo Sie die Fabric React-Komponenten verwenden. 

> Bitte beachten Sie, dass die Versionen 2.x und älter von Fabric React in SharePoint-Framework nicht unterstützt werden.

Nach der Installation des Fabric React-Pakets können Sie die erforderlichen Komponenten aus dem Fabric React-Paket importieren.

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

Das Fabric React-Paket enthält die unterstützten Fabric Core-Formatvorlagen, die in den Fabric React-Komponenten verwendet werden. Es wird empfohlen, die Fabric Core-Formatvorlagen aus dem Fabric React-Paket anstelle des Pakets „sp-office-ui-fabric-core“ zu importieren, um sicherzustellen, dass die richtigen Formatvorlagen in Ihrer Komponente verwendet werden. 

Da das Paket „sp-office-ui-fabric-core“ bereits in Ihrer Lösung vom Yeoman-Generator installiert wurde, empfiehlt es sich, das Paket zu deinstallieren, wenn Sie Fabric-Komponenten verwenden und die Größe des Komponentenbundles reduzieren möchten.

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

Anschließend können Sie die wichtigsten Formatvorlagen aus den SASS-Deklarationen importieren, die im Fabric React-Paket verfügbar sind.

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a>Grundlegendes zu diesem Ansatz und Nachteile

Fabric-Komponenten in Ihrer Lösung sind mit dieser bestimmten installierten Version von Fabric React verbunden. Sie müssen das Fabric React-Paket aktualisieren, um neue Komponenten zu verwenden, falls diese in einer neueren Paketversion zur Verfügung stehen. Da Fabric-Komponenten im Komponentenbundle enthalten sind, wird dadurch möglicherweise Ihr Komponentenbundle größer. Dies ist der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in den SharePoint-Framework-Lösungen unterstützt wird.


## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a>Weitere Informationen zu dem CSS-Problem in Office UI Fabric
Die folgenden Konzepte und Verweise liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext clientseitiger Webparts. 

**Globale CSS-Formatvorlagen** und wie diese unbedingt vermieden werden: Dies stellt ein großes Problem dar. Heute weisen sowohl Fabric Core als auch Fabric React globale Formatvorlagen auf. Aufgrund eines Mangels systemeigener Lösungen vom Browser zum Verwalten der Bereichsdefinition der Formatvorlagen ist dies ein schwerwiegendes Problem.
  
  - [Die Bereichsdefinition von CSS](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) erfolgt in den frühen Phasen der Besprechung. 
  - iFrames sind keine gute Option zum Isolieren von Formatvorlagen.
  - [Webkomponenten](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht, der sich aber noch in der Besprechungsphase befindet.
  - In [dieser](https://speakerdeck.com/vjeux/react-css-in-js) Diskussion wird das Problem gut erläutert. Es gibt zahlreiche andere Dokumentationen im Web über die Lösungen für das Problem mit dem globalen Namespace.
 
**[CSS-Genauigkeit](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity)** und wie diese auf Webbenutzeroberflächen angewendet wird. Formatvorlagen mit höherer Genauigkeit setzen die Formatvorlagen mit niedrigerer Genauigkeit außer Kraft.  Das Wichtigste ist jedoch, dass Sie verstehen, wie die Genauigkeitsregeln angewendet werden. Im Allgemeinen ist die Rangfolge von oben nach unten wie folgt:
  - Das Style-Attribut (z. B. `style="background:red;"`)
  - ID-Selektoren (z. B. `#myDiv { }`)
  - Klassenselektoren (z. B. `.myCssClass{}`), Attributselektoren (z. B. `[type="radio"]`) und Pseudoselektoren (z. B. `:hover`)
  - Typselektoren (z.B. `h1`)

***Ladereihenfolge*** – Wenn zwei Klassen auf ein Element angewendet werden und diese dieselbe Genauigkeit aufweisen, hat die Klasse Vorrang, die später geladen wird. Wie im folgenden Code dargestellt, wird die Schaltfläche rot angezeigt. Wenn die Reihenfolge der Styletags geändert wird, wird die Schaltfläche grün angezeigt. Dies ist ein wichtiges Konzept. Wenn es nicht korrekt verwendet wird, kann die Benutzerfreundlichkeit von der Ladereihenfolge abhängig sein, d.h. sie wird inkonsistent.

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

## <a name="other-approaches-considered-and-discarded"></a>Andere in Erwägung gezogene und verworfene Ansätze
Nachfolgend finden Sie weitere Informationen zu den anderen Ansätzen, die in Betracht gezogen, aber dann verworfen wurden, weil damit die wichtigsten Ziele, und zwar, dass Drittanbieterentwickler Office UI Fabric-Formatvorlagen sicher verwenden können, nicht erreicht wurden.

**Office UI Fabric Core**

Der Webpartentwickler muss nicht explizit etwas tun, damit die Bereichsdefinition funktioniert. Wir planen, dieses Problem über die CSS-Genauigkeit und einen Nachfolgerselektor zu beheben. Das Fabric Core-Team wird mehrere Kopien von Fabric Core-CSS-Dateien ausliefern, z. B. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.

Alle Formatvorlagen in den bereichsbezogenen CSS-Dateien befinden sich innerhalb eines Nachfolgerselektors, z. B. `"ms-Fabric-core--v6 ms-Icon--List"`. Zur Kompilierzeit erfassen die Tools die Version von Office UI Fabric Core, mit der das Webpart erstellt wurde. Bei dieser Version kann es sich um die Version handeln, die mit SPFx geliefert wird. Webpartentwickler können alternativ eine explizite Abhängigkeit von einer bestimmten Version von Office-UI-Fabric Core in ihrer**package.json**-Datei verwenden.

Das Webpart-Div wird diesem Bereich zugewiesen, d. h. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Das Framework lädt die spezifische Hauptversion der bereichsbezogenen Fabric Core-CSS-Datei. Wenn das Webpart mit Version 6.0.0 von Fabric Core-CSS erstellt wurde, lädt das Framework `fabric-6-scoped.css` zur Ladezeit des Webparts herunter.

Der Rest der Seite enthält nicht bereichsbezogenen Office UI Fabric Core-Formatvorlagen. Auf diese Weise erhält das bereichsbezogene CSS Vorrang innerhalb des Webpart-Div, wie in den CSS-Genauigkeitsregeln festgelegt. Das Webpart und sein Inhalt werden auf die Version von Office UI Fabric Core abgestimmt, die der Entwickler ausgewählt hat.

Das **Außerkraftsetzen** von Fabric Core-Formatvorlagen wird nicht unterstützt.  

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

Nach längerer Analyse dieser Strategie wurde festgestellt, dass der Ansatz mit dem Nachfolgerselektor zwei wesentliche Nachteile hat, aufgrund derer es nicht möglich ist, ein Webpart zu erstellen, das niemals beschädigt wird.

**Keine zuverlässige Unterstützung für Schachtelung** – Dieser Ansatz funktioniert nur, wenn die Microsoft-Benutzeroberfläche (d. h. die Seite und alle Erstanbieter-Webparts) eine nicht bereichsbezogene Version von Office UI Fabric Core verwenden (z. B. `ms-Icon--List`) und wenn die Drittanbieter-Webparts nur bereichsbezogenes Office UI Fabric Core-CSS wie oben erläutert verwenden. Der Grund hierfür ist, dass die Genauigkeit des bereichsbezogenen CSS, das auf das Webpart angewendet wird, das nicht bereichsbezogene CSS auf der Seite außer Kraft setzt. Beachten Sie: Wie oben erläutert gilt, dass, wenn die CSS-Genauigkeit von zwei Klassen gleich ist, ihre Ladereihenfolge eine Rolle für die Anwendung der CSS-Klassen spielt. Die Klasse, die später geladen wird, hat Vorrang. Die höhere Genauigkeit des bereichsbezogenen CSS ist daher wichtig, um eine konsistente Oberfläche zu erhalten.

Darüber hinaus können mehrere Erweiterungen, von denen eine jeweils in der anderen enthalten ist, nicht unterschiedliche Fabric Core-Versionen verwenden, d. h. im folgenden Beispiel wird nur `ms-Fabric-core--v6` angewendet:

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

Nachfolgend finden Sie ein einfacheres Beispiel, in dem das Problem erläutert wird:

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

**Offenlegung von nicht bereichsbezogenen Klassen** – Es gibt ein weiteres Problem mit Nachfolgerselektoren. Beachten Sie im obigen Beispiel, dass die Formatvorlagen für Höhe und Breite aus der nicht bereichsbezogenen myButton-Klasse auf alle Schaltflächen angewendet werden. Dies impliziert, dass eine Änderung in dieser Formatvorlage die HTML, die das bereichsbezogene Markup verwendet, versehentlich beschädigen könnte. Nehmen wir beispielsweise an, dass wir die Höhe auf App-Ebene auf 0px in der myButton-Klasse festlegen. Dies führt dazu, dass alle Drittanbieter-Webparts, die die myButton-Klasse verwenden, eine Höhe von 0 haben, also eine wesentliche Regression in der Benutzeroberfläche.


