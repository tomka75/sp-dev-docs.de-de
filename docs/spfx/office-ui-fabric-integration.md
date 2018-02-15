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
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a>Verwenden von Office UI Fabric Core und Fabric React im SharePoint-Framework

Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.

Microsoft verwendet Fabric Core und Fabric React in SharePoint. Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, die möglicherweise auch jeweils die Version von Fabric Core und Fabric React aktualisieren. Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den entsprechenden Anpassungen führen kann. Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken. Solche Konflikte müssen auf jeden Fall vermieden werden. 

Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JavaScript erläutert: [React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).

Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss. Hierzu sind statt globaler Klassennamen im HTML-Markup Fabric Core-Mixins und -Variablen in der SASS-Deklarationsdatei zu verwenden. Dies umfasst den Import der Fabric Core-Sass-Deklarationen in die Sass-Datei und anschließend eine entsprechende Verarbeitung der Variablen und Mixins. 

## <a name="goals"></a>Ziele

Das Ziel des SharePoint-Frameworks besteht darin, Microsoft und Kunden das Erstellen funktionsreicher, ansprechender und konsistenter Benutzeroberflächen auf SharePoint-Basis zu ermöglichen. 

Im Folgenden werden die wichtigsten Entwurfsprinzipien für die Umsetzung dieses Ziels erläutert:

* Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.
* Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.
* Kunden können die Standardformatvorlagen, -designs und -komponenten gemäß den Anforderungen ihrer Lösung anpassen und überschreiben.

Es gibt zwei Teile von Office UI Fabric, die Entwicklern zur Verfügung stehen:

* [Office UI Fabric Core](https://developer.microsoft.com/de-DE/fabric): Hierbei handelt es sich um einen Satz von grundlegenden Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen Basisbausteinen der gesamten Entwurfssprache.

* [Office UI Fabric React](https://developer.microsoft.com/de-DE/fabric#/components): Hierbei handelt es sich um eine Reihe von React-Komponenten, die auf der Fabric-Entwurfssprache aufbauen und in React-basierten Projekten verwendet werden können.

## <a name="office-ui-fabric-core-package"></a>Office UI Fabric Core-Paket

Das Fabric Core-npm-Paket für das SharePoint-Framework (sp-office-ui-fabric-core) enthält eine Teilmenge der unterstützten Fabric Core-Formatvorlagen, die ohne Sicherheitsrisiko in SharePoint-Framework-Komponenten verwendet werden können. 

Die folgenden grundlegenden Formatvorlagen werden in dem Paket unterstützt:
- Typografie
- Layouts
- Farben
- Designs
- Lokalisierung

Folgendes wird in dem Paket noch nicht unterstützt:
- Animationen
- Symbole

Ab Version 1.3.4 des SharePoint-Framework-Yeoman-Generators enthalten die Standardprojektvorlagen (Webparts und Erweiterungen) das neue Paket „sp-office-ui-fabric-core“ und nutzen statt globaler CSS-Formatvorlagen grundlegende Formatvorlagen aus diesem Paket. 

### <a name="update-existing-projects"></a>Aktualisieren bereits vorhandener Projekte

Um das Fabric Core-Paket in einem vorhandenen Projekt verwenden zu können, müssen Sie das Paket als Entwicklerabhängigkeit installieren:

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

Nach Abschluss der Installation können Sie die Fabric Core-Sass-Deklarationen in die Sass-Definitionsdatei importieren und die Mixins und Variablen wie im folgenden Abschnitt beschrieben verwenden. 

### <a name="use-fabric-core-styles"></a>Verwenden von Fabric Core-Formatvorlagen

Um die Fabric Core-Formatvorlagen verwenden zu können, müssen Sie die SPFabricCore-Deklarationen in Ihre Sass-Datei importieren.

> [!NOTE] 
> Vergewissern Sie sich, dass das npm-Paket „sp-office-ui-fabric-core“ installiert ist.

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

<br/>

Jetzt können Sie die grundlegenden Formatvorlagen als Mixins und Variablen verwenden.

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="office-ui-fabric-react"></a>Office UI Fabric React

Wir empfehlen, das neueste Office UI Fabric React-Paket zu installieren und eine explizite Abhängigkeit von dieser spezifischen Version des Pakets zu setzen. Dies umfasst die in der SharePoint-Framework-Lösung verwendeten Komponenten in Ihrem Komponentenbundle, entweder Webpart oder Erweiterung, je nachdem wo Sie die Fabric React-Komponenten verwenden. 

> [!NOTE] 
> Die Version 2.x von Fabric React sowie ältere Versionen werden im SharePoint-Framework nicht unterstützt.

Nach der Installation des Fabric React-Pakets können Sie die erforderlichen Komponenten aus dem Fabric React-Paket importieren.

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

Das Fabric React-Paket enthält die unterstützten Fabric Core-Formatvorlagen, die in den Fabric React-Komponenten verwendet werden. Wir empfehlen, die Fabric Core-Formatvorlagen aus dem Fabric React-Paket zu importieren, nicht aus dem Paket „sp-office-ui-fabric-core“. So ist sichergestellt, dass in Ihrer Komponente die korrekten Formatvorlagen verwendet werden. 

Da das Paket „sp-office-ui-fabric-core“ bereits vom Yeoman-Generator in Ihrer Lösung installiert wurde, empfehlen wir, dieses Paket zu deinstallieren, wenn Sie Fabric-Komponenten verwenden und die Größe des Komponentenbundles reduzieren möchten.

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

Anschließend können Sie die grundlegenden Formatvorlagen aus den Sass-Deklarationen importieren, die im Fabric React-Paket enthalten sind.

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a>Grundlegendes zu diesem Ansatz und seinen Nachteilen

Fabric-Komponenten in Ihrer Lösung sind an die spezifische Fabric React-Version gebunden, die Sie installiert haben. Wenn Sie neue Komponenten aus einer neueren Version des Pakets verwenden möchten, müssen Sie das Fabric React-Paket aktualisieren. Da die Fabric-Komponenten im Komponentenbundle enthalten sind, wird Ihr Komponentenbundle dadurch möglicherweise größer. Dies ist jedoch der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in SharePoint-Framework-Lösungen unterstützt wird.


## <a name="the-css-challenge-with-office-ui-fabric"></a>Das CSS-Problem in Office UI Fabric

Die folgenden Konzepte und Ressourcen liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext von clientseitigen Webparts. 

### <a name="global-css-styles"></a>Globale CSS-Formatvorlagen

Es ist sehr schwierig, den Einsatz globaler CSS-Formatvorlagen komplett zu vermeiden. Aktuell nutzen sowohl Fabric Core als auch Fabric React globale Formatvorlagen. Da Browser keine nativen Lösungen für die Verwaltung der Bereichsdefinitionen von Formatvorlagen mitbringen, ist das ein schwerwiegendes Problem.
  
  - Die Diskussion um [CSS-Bereiche](https://developer.mozilla.org/de-DE/docs/Web/CSS/:scope) steht noch ganz am Anfang.
  - iFrames sind keine gute Option zur Isolierung von Formatvorlagen.
  - [Webkomponenten](https://developer.mozilla.org/de-DE/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht. Auch hier befindet man sich jedoch noch ganz am Anfang der Diskussion.
  - Die Präsentation [React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js) erläutert das Problem anschaulich. 
  
Es gibt zahlreiche weitere Dokumentationen im Web, die sich Lösungen für das Problem globaler Namespace gewidmet haben.

### <a name="css-specificity"></a>CSS-Spezifität

In [diesem Artikel zum Thema CSS-Spezifität](https://developer.mozilla.org/de-DE/docs/Web/CSS/Specificity) erfahren Sie, wie das Konzept auf Webbenutzeroberflächen angewendet wird. Formatvorlagen mit höherer Spezifität überschreiben Formatvorlagen mit niedrigerer Spezifität. Am wichtigsten ist es jedoch, dass Sie verstehen, wie die Spezifitätsregeln angewendet werden. Im Allgemeinen lautet die Rangfolge von der höchsten zur niedrigsten Formatvorlage wie folgt:
  - Attribut „style“ (zum Beispiel `style="background:red;"`)
  - ID-Selektoren (`#myDiv { }`)
  - Klassenselektoren (`.myCssClass{}`), Attributselektoren (`[type="radio"]`) und Pseudoklassen (`:hover`)
  - Typselektoren (`h1`)

**Ladereihenfolge:** Wenn zwei Klassen auf ein Element angewendet werden und diese Klassen dieselbe Spezifität aufweisen, hat die Klasse Vorrang, die später geladen wird. Wie im nachfolgenden Code ersichtlich, wird die Schaltfläche rot angezeigt. Wenn die Reihenfolge der „style“-Tags geändert wird, wird die Schaltfläche grün angezeigt. Dies ist ein wichtiges Konzept. Wenn es nicht korrekt angewendet wird, kann die Benutzeroberfläche abhängig von der Ladereihenfolge werden (d. h., sie wird inkonsistent).

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

Nachfolgend finden Sie weitere Informationen zu den anderen Ansätzen, die in Betracht gezogen, aber dann verworfen wurden, weil mit ihnen das wichtigste Ziele nicht erreicht werden konnte: Drittanbietern die risikofreie Verwendung der Office UI Fabric-Formatvorlagen zu ermöglichen.

### <a name="office-ui-fabric-core"></a>Office UI Fabric Core

Webpartentwickler müssen nicht explizit etwas tun, damit Bereichsdefinitionen funktionieren. Wir wollten dieses Problem mithilfe von CSS-Spezifität und Nachfolgerselektoren lösen. Dazu stellte das Fabric Core-Team mehrere Versionen von Fabric Core-CSS-Dateien bereit (zum Beispiel `fabric-6.css`, `fabric-6-scoped.css`,`fabric-6.0.0.css` und `fabric-6.0.0-scoped.css`).

Alle Formatvorlagen in den bereichsbezogenen CSS-Dateien befanden sich innerhalb eines Nachfolgerselektors, zum Beispiel `"ms-Fabric-core--v6 ms-Icon--List"`. Zur Kompilierzeit erfassten die Tools die Version von Office UI Fabric Core, mit der das Webpart erstellt wurde. Bei dieser Version konnte es sich um die mit dem SharePoint-Framework bereitgestellte Version handeln. Alternativ konnten Webpartentwickler eine explizite Abhängigkeit von einer bestimmten Office UI Fabric Core-Version in ihrer Datei **package.json** setzen.

Dem Webpart-Div wurde dann der entsprechende Bereich zugewiesen, also `<div data-sp-webpart class="ms-Fabric-core--v6">`. Das Framework lud die spezifische Hauptversion der Fabric Core-bezogenen CSS-Datei. Wurde das Webpart mit Version 6.0.0 des Fabric Core-CSS-Codes erstellt, lud das Framework die Datei `fabric-6-scoped.css` herunter, sobald das Webpart geladen wurde.

Der Rest der Seite enthielt nicht bereichsbezogene Office UI Fabric Core-Formatvorlagen. Auf diese Weise erhielt der bereichsbezogene CSS-Code gemäß den CSS-Spezifitätsregeln Vorrang innerhalb des Webpart-DIV. Das Webpart und sein Inhalt wurden an die Office UI Fabric Core-Version angepasst, die der Entwickler ausgewählt hatte.

Eine *Überschreibung* von Fabric Core-Formatvorlagen wurde nicht unterstützt.  

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

### <a name="shortcomings-of-this-strategy"></a>Nachteile dieser Strategie

Nach längerer Analyse dieser Strategie stellten wir fest, dass die Verwendung von Nachfolgerselektoren zwei wesentliche Nachteile hat, aufgrund derer es nicht möglich ist, ein gegen Fehler immunes Webpart zu erstellen.

#### <a name="lack-of-reliable-nesting-support"></a>Keine zuverlässige Unterstützung für Schachtelung

Dieser Ansatz funktioniert nur, wenn die Microsoft-Benutzeroberfläche (d. h. die Seite und alle Erstanbieter-Webparts) eine nicht bereichsbezogene Version von Office UI Fabric Core verwenden (z. B. `ms-Icon--List`) und wenn die Drittanbieter-Webparts nur bereichsbezogenen Office UI Fabric Core-CSS-Code verwenden (siehe oben). 

Der Grund hierfür ist, dass die Spezifität des bereichsbezogenen CSS-Codes, der auf das Webpart angewendet wird, den nicht bereichsbezogenen CSS-Code auf der Seite überschreibt. Wie weiter oben erläutert: Wenn die CSS-Spezifität von zwei CSS-Klassen identisch ist, entscheidet die Ladereihenfolge der Klassen darüber, wie sie angewendet werden. Die Klasse, die später geladen wird, hat Vorrang. Die höhere Spezifität des bereichsbezogenen CSS-Codes ist daher wichtig, um eine konsistente Oberfläche zu erhalten.

Darüber hinaus können mehrere ineinander geschachtelte Erweiterungen nicht jeweils eine andere Version von Fabric Core verwenden. Im folgenden Beispiel würde ausschließlich `ms-Fabric-core--v6` angewendet werden:

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<br/>

Unten sehen Sie ein einfacheres Beispiel zur Veranschaulichung des Problems:

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

#### <a name="leakage-from-unscoped-classes"></a>Übersprung aus nicht bereichsbezogenen Klassen

Nachfolgerselektoren bergen ein weiteres Problem. Wie Sie im vorangegangenen Beispiel sehen, werden die Formatvorlagen „height“ und „width“ aus der nicht bereichsbezogenen Klasse „myButton“ auf alle Schaltflächen angewendet. Das bedeutet: Würde diese Formatvorlage dahingehend verändert, dass bereichsbezogenes Markup verwendet wird, könnte dadurch versehentlich der HTML-Code beschädigt werden. 

Nehmen wir beispielsweise an, wir würden aus Gründen auf App-Ebene das Attribut „height“ in der Klasse „myButton“ auf „0 px“ setzen. Dann würde in allen Drittanbieter-Webparts, die die Klasse „myButton“ verwenden, ein „height“-Wert von 0 px gelten. (Es würde also zu einer schwerwiegenden Regression auf der Benutzeroberfläche kommen.)

## <a name="see-also"></a>Weitere Artikel

- [Übersicht über das SharePoint-Framework](sharepoint-framework-overview.md)




