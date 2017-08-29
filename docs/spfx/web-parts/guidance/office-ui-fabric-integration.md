# <a name="using-office-ui-fabric-core-and-fabric-react-in-spfx-client-side-web-parts"></a>Verwenden von Office UI Fabric Core und Fabric React in clientseitigen SPFx-Webparts

#### **Wichtig:** Sie müssen vorhandene Projekte auf *@microsoft/sp-build-web@1.0.1* oder höher aktualisieren, um Office UI Fabric React-Komponenten verwenden zu können. Lesen Sie die Anweisungen am Ende dieses Artikels, um weitere Informationen zu erhalten.

Office UI Fabric ist das offizielle Front-End-Framework zum Erstellen von Oberflächen in Office 365 und SharePoint. SharePoint bietet eine nahtlose Integration in Fabric, sodass Microsoft eine robuste und konsistente Entwurfssprache über verschiedene SharePoint-Oberflächen hinweg bereitstellen kann, z. B. moderne Teamwebsites, moderne Seiten und moderne Listen. Darüber hinaus ist Office UI Fabric für Entwickler in SharePoint Framework zum Erstellen benutzerdefinierter SharePoint-Lösungen verfügbar.

> Die Integration und Verwendung von Office UI Fabric sind noch in Bearbeitung. Dieses Dokument soll ein Statusupdate für SPF-Entwickler bereitstellen. Es ist geplant, in Kürze einen endgültigen Plan zu veröffentlichen.

## <a name="goals"></a>Ziele

Es gibt zwei Teile von Office UI Fabric, die für Entwickler zur Verfügung stehen:

  1. [Office UI Fabric Core](http://dev.office.com/fabric), auch bezeichnet als Fabric Core – Hierbei handelt es sich um einen Satz von Formatvorlagen, Typografien, dynamischen Rastern, Animationen, Symbolen und anderen grundlegenden Bausteinen der gesamten Entwurfssprache.

  2. [Office UI Fabric React](http://dev.office.com/fabric#/components), auch bezeichnet als Fabric React – Dieses Paket enthält eine Reihe von React-Komponenten, die über die Fabric-Entwurfssprache hinaus erstellt wurden.
  
Einige der Ziele von SharePoint Framework bestehen darin, Microsoft und Kunden das Erstellen vielfältiger, ansprechender und konsistenter Lösungen über SharePoint hinaus zu ermöglichen. In Übereinstimmung mit diesen Zielen finden Sie nachfolgend unsere Entwurfsgrundsätze:

* Alle Kunden sollen Fabric Core und Fabric React nahtlos und zuverlässig in ihren Lösungen nutzen können.
* Microsoft veröffentlicht aktualisierte Oberflächen, die aktualisierte Versionen von Fabric Core und Fabric React verwenden, in SharePoint, ohne dass Konflikte mit den Lösungen von Kunden entstehen.
* Kunden können die Formatvorlagen, Designs und Komponenten in Übereinstimmung mit den Anforderungen ihrer Lösung anpassen und überschreiben.
* Kunden sollten in der Lage sein, Lösungen mit Frameworks zu erstellen, die nicht auf React basieren.

## <a name="summary"></a>Zusammenfassung

Microsoft verwendet Fabric Core und Fabric React in SharePoint. Microsoft veröffentlicht regelmäßig Updates für SharePoint Online, und die SharePoint-Oberflächen werden mit großer Wahrscheinlichkeit die jeweils verwendete Version von Fabric Core und Fabric React weiterhin aktualisieren. Diese Updates können möglicherweise in Konflikt mit Drittanbieterlösungen stehen, die mit früheren Versionen von Fabric Core und Fabric React erstellt wurden, was zu Ausnahmen in den Anpassungen führen kann. Der Hauptgrund für diese Konflikte ist die Verwendung **globaler CSS-Formatvorlagen** in beiden Fabric-Bibliotheken. Solche Konflikte müssen auf jeden Fall vermieden werden. 

Um Zuverlässigkeit zu erreichen, ist das Problem der **globalen CSS-Formatvorlagen** das wichtigste Problem, das gelöst werden muss. Sowohl Fabric Core als auch „fabric.component.css“ verwenden derzeit globale Formatvorlagen.

Aus diesen Gründen können Kundenlösungen derzeit Teile von Office-UI-Fabric noch nicht sicher verwenden. Natürlich sind wir uns bewusst, dass Entwickler Fabric Core und Fabric React zum Erstellen ihrer Lösungen benötigen. Wir arbeiten daran, dies so schnell wie möglich zu beheben.

Nachfolgend finden Sie eine Zusammenfassung derzeit unterstützter Optionen zur Verwendung von Office-UI-Fabric mit SharePoint Framework-Lösungen basierend auf dem ausgewählten JavaScript-Framework.

- React – Office-UI-Fabric kann nur über die **statische Verknüpfung** mit den Fabric React-Komponenten sicher verwendet werden.
- Andere JS-Bibliotheken – Die Verwendung von Office-UI-Fabric innerhalb einer SharePoint Framework-Lösung wird **nicht** unterstützt.

> Ein Beispiel für das aktuelle Problem mit der Versionsverwaltung: Ein Webpart verwendet die Klasse `ms-Icon--List`, wenn das Webpart erstellt wird. Später entscheidet Fabric, dass die Definition dieser Klasse geändert werden soll. Das Webpart, das eine Annahme zu der vorherigen Implementierung gestellt hatte, wird möglicherweise beschädigt. Gleichermaßen nehmen wir beispielsweise an, dass das Webpart die Klasse `ms-Button` aus Fabric React verwendet. Zu einem späteren Zeitpunkt ändert das Fabric React-Team die Implementierung der Schaltfläche zusammen mit den Formatvorlagen in der `ms-Button`-Klasse wesentlich. Dadurch würde das Webpart aller Wahrscheinlichkeit nach beschädigt werden.

> Das Problem mit globalen CSS-Formatvorlagen wird in der folgenden Präsentation im Kontext von React und JSS ausführlich erläutert: [React-CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).

## <a name="how-to-use-the-office-ui-fabric-react-in-a-safe-way-in-your-solution"></a>Sicheres Verwenden von Office UI Fabric React in Ihrer Lösung

Nachfolgend finden Sie Empfehlungen zur sicheren und zuverlässigen Verwendung von Fabric in auf React basierenden Webparts.

- Webpartentwickler müssen eine explizite Abhängigkeit von einer bestimmten Version von Fabric React, Version 2.0, in der **package.json**-Datei `"office-ui-fabric-react":"2.34.2"` verwenden. Beachten Sie, dass ältere Versionen von Fabric React als Version 2.x nicht unterstützt werden.
- Der Webpartentwickler muss eine **statische Verknüpfung** zu den Fabric React-Komponenten herstellen. Dazu gehören die Fabric React-Komponenten in Ihrem Webpartpaket. Würde sich die Implementierung der Schaltfläche auf Seitenebene ändern, hätte dies keine nachteiligen Auswirkungen auf Ihr Webpart.
- Das **Außerkraftsetzen** von Formatvorlagen für Fabric React-Komponenten sollte nur selten und innerhalb eines lokalen Bereichs verwendet werden. Die Außerkraftsetzungen können von einem Entwickler unter Verwendung von benutzerdefinierten CSS-Klassen mit `!important` und Styletags vorgenommen werden. Beides hat eine höhere Genauigkeit als die Komponentenklassen. Wenn Sie eine Außerkraftsetzung unter Verwendung einer einfachen Klasse vornehmen, beachten Sie, dass dann möglicherweise Probleme mit der Ladereihenfolge auftreten können. Wenn `ms-Button` nach Ihrer Klasse geladen wird, hat diese Vorrang, da ihre Genauigkeit dieselbe ist.
- **Designs** sollten standardmäßig funktionieren. Seitens des Entwicklers sind keine weiteren Aktionen erforderlich.

Der folgende Codeausschnitt zeigt, wie die statische und dynamische Verknüpfung von Bibliotheken funktioniert.

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

***Grundlegendes zu diesem Ansatz und Nachteile***

- Komponenten im Webpart sind auf die Version von Fabric React beschränkt, die Sie beim Erstellen des Webparts verwendet haben. Diese werden nicht automatisch mit der umgebenden Seite weiterentwickelt. Sie müssen Ihr Webpart manuell aktualisieren, um eine Anpassung an neuere Versionen von Fabric React vorzunehmen.
- Die Seite reagiert möglicherweise langsamer, da unter Umständen mehr CSS geladen wird, funktioniert aber zuverlässig.
- Die statische Verknüpfung bläht Ihr Webpartpaket auf, die dynamische Verknüpfung ist jedoch angesichts künftiger Updates, die in SharePoint Online eingeführt werden, nicht stabil genug. Die statische Verknüpfung ist der einzige Ansatz, der offiziell bei der Verwendung von Office UI Fabric React in den SharePoint Framework-Lösungen unterstützt wird.

### <a name="currently-unsupported-features"></a>Derzeit nicht unterstützte Features

- **Office UI Fabric Core**: Die Fabric Core-Implementierung verwendet derzeit globale Formatvorlagen, z. B. `.ms-Icon--List`, und Fabric Core kann daher nicht sicher in Ihrem Webpart ohne mögliche Probleme in der Zukunft verwendet werden. Es wird daran gearbeitet, dieses Problem zu lösen. Weitere Informationen werden veröffentlicht, wenn sich die Situation ändert.

- **fabric.components.css**: Diese Datei enthält globale Klassen, die mit Fabric React in Konflikt stehen, `.ms-Button` in „fabric.component.css“ setzt beispielsweise die Button-Formatvorlagen in der Button-Komponente von Fabric React außer Kraft. Das Einbinden von „fabric.component.css“ führt dazu, dass die umgebende Seite oder andere Webparts auf der Seite beschädigt werden. Wir arbeiten an einer Lösung und werden in Kürze ein Update veröffentlichen.


## <a name="using-the-office-ui-fabric-with-non-react-based-web-parts"></a>Verwenden von Office UI Fabric mit Webparts, die nicht auf React basieren

Die Verwendung von  Office UI Fabric mit Webparts, die nicht auf React basieren, wird derzeit nicht unterstützt, und mögliche Implementierungen können unerwartete Probleme verursachen, wenn eine neuere Version von Office UI Fabric veröffentlicht wird. Wir arbeiten derzeit an einer zuverlässigen Integration von **Office UI Fabric Core**, **fabric.component.css** und **nicht auf React basierenden Webparts**. 

## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a>Weitere Informationen zu dem CSS-Problem in Office UI Fabric
Die folgenden Konzepte und Verweise liefern Einblicke in das Problem bei der Verwendung von Office UI Fabric im Kontext clientseitiger Webparts. 

**Globale CSS-Formatvorlagen** und wie diese unbedingt vermieden werden: Dies stellt ein großes Problem dar. Heute weisen sowohl Fabric Core als auch Fabric React globale Formatvorlagen auf. Aufgrund eines Mangels systemeigener Lösungen vom Browser zum Verwalten der Bereichsdefinition der Formatvorlagen ist dies ein schwerwiegendes Problem.
  
  - [Die Bereichsdefinition von CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope) erfolgt in den frühen Phasen der Besprechung. 
  - iFrames sind keine gute Option zum Isolieren von Formatvorlagen.
  - [Webkomponenten](https://developer.mozilla.org/en-US/docs/Web/Web_Components) sind ein weiterer Standard, bei dem es um bereichsbezogene Formatvorlagen geht, der sich aber noch in der Besprechungsphase befindet.
          
    In [dieser](https://speakerdeck.com/vjeux/react-css-in-js) Diskussion wird das Problem gut erläutert. Es gibt zahlreiche andere Dokumentationen im Web über die Lösungen für das Problem mit dem globalen Namespace.
 
**[CSS-Genauigkeit](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)** und wie diese auf Webbenutzeroberflächen angewendet wird. Formatvorlagen mit höherer Genauigkeit setzen die Formatvorlagen mit niedrigerer Genauigkeit außer Kraft.  Das Wichtigste ist jedoch, dass Sie verstehen, wie die Genauigkeitsregeln angewendet werden. Im Allgemeinen ist die Rangfolge von oben nach unten wie folgt:
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

## <a name="updating-an-existing-project"></a>Aktualisieren bereits vorhandener Projekte

Aktualisieren Sie in der Datei `package.json` Ihres Projekts die Abhängigkeit `@microsoft/sp-build-web` mindestens auf Version 1.0.1, löschen Sie das Verzeichnis `node_modules` Ihres Projekts, und führen Sie den Befehl `npm install` aus.

