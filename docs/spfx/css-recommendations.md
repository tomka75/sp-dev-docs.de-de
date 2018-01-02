---
title: "Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen"
ms.date: 11/18/2017
ms.prod: sharepoint
ms.openlocfilehash: 0e65926fda0ff1a788388e23d1d7df2e4b9ea32a
ms.sourcegitcommit: 0350850e0f46841a7eaadcc69d0fb90739fcd654
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2017
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a>Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen

Wenn Sie SharePoint-Framework Lösungen erstellen, können Sie CSS verwenden, um zu definieren, wie sich Ihre Anpassung verhalten und aussehen soll. In diesem Artikel wird beschrieben, wie Sie die mit dem SharePoint Framework bereitgestellten Funktionen am besten nutzen und Ihre CSS-Formatvorlagen stabil erstellen.

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a>SharePoint Framework-Anpassungen sind Teil der Seite

Wenn Sie SharePoint-Anpassungen mit dem Add-In-Modell erstellen, ist die Lösung von anderen Elementen auf der Seite isoliert. Der Code wird entweder in einem Iframe, als Add-In-Bestandteil oder als immersive Anwendung ausgeführt, die die Kontrolle übe die gesamte Seite übernimmt. In beiden Fällen wird der Code nicht von anderen Elementen und Formatvorlagen beeinträchtigt, die auf der Seite definiert sind.

SharePoint Framework-Lösungen sind Teil der Seite und können vollständig in das DOM der Seite integriert werden. Dabei wird eine Reihe von Einschränkungen entfernt, die in dem Add-In-Modell enthalten sind, wodurch Ihre Lösung einem Risiko ausgesetzt wird. Da es sich um einen Teil der Seite handelt, gelten alle auf der Seite vorhandenen CSS-Formatvorlagen dafür, sofern diese nicht isoliert sind, was möglicherweise zu einer anderen Erfahrung als der beabsichtigten führt. Um derartige Risiken zu verhindern, sollten Sie Ihre CSS-Formatvorlagen so definieren, dass sie sich nicht auf andere Elemente auf der Seite, sondern nur auf die Anpassung auswirken.

## <a name="organize-css-files-in-your-solution"></a>Organisieren von CSS-Dateien in Ihrer Lösung

Die Benutzeroberfläche Ihrer Lösung besteht häufig aus mehreren Bausteinen. In vielen JavaScript-Bibliotheken werden diese Bausteine als Komponenten bezeichnet. Eine Komponente kann einfach sein und nur die Präsentation definieren, oder sie kann komplexer sein und den Status sowie andere Komponenten umfassen. Durch Aufteilen der Lösung in mehrere Komponenten können Sie den Entwicklungsprozess vereinfachen und das Testen und Wiederverwenden in Ihrer Lösung erleichtern.

Da Komponenten über eine Präsentation verfügen, erfordern sie häufig CSS-Formatvorlagen. Im Idealfall sind Komponenten isoliert und können eigenständig verwendet werden. Angesichts dessen ist es sinnvoll, CSS-Formatvorlagen für die jeweilige Komponente mit allen anderen Ressourcendateien neben der Komponente zu speichern. Nachfolgend finden Sie eine Beispielstruktur einer React-Anwendung mit einer Reihe von Komponenten, die jeweils über ihre eigene CSS-Datei verfügen.

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a>Verwenden von Sass

Im SharePoint-Framework können Sie sowohl CSS und Sass verwenden. Sass ist eine Obermenge von CSS und bietet Ihnen eine Reihe von Funktionen, z. B. das Verwenden von Variablen, das Verschachteln von Selektoren oder die Verwendung von Mixins, die alle das Arbeiten mit und das Verwalten von CSS-Formatvorlagen langfristig vereinfachen. Eine vollständigen Satz von Funktionen finden Sie auf der [Sass-Website](http://sass-lang.com). Gültige CSS ist ebenfalls gültige Sass, was sehr hilfreich ist, wenn Sie noch nicht mit Sass gearbeitet haben und sich an die Funktionen herantasten möchten.

## <a name="avoid-using-ids-in-markup"></a>Vermeiden der Verwendung von IDs in Markup

Mithilfe von SharePoint Framework erstellen Sie Anpassungen, die Endbenutzer zu SharePoint hinzufügen. Es kann vorab festgestellt werden, ob die jeweilige Anpassung nur einmal auf einer Seite verwendet wird oder ob es mehrere Instanzen davon gibt. Um Probleme zu verhindern, sollten Sie immer davon ausgehen, dass es mehrere Instanzen Ihrer Anpassung auf derselben Seite gibt. Angesichts dieser Tatsache sollten Sie keine IDs in Ihrem Markup verwenden. IDs sollen auf einer Seite eindeutig sein, und wenn ein Benutzer Ihr Webpart der Seite zweimal hinzugefügt hat, würde dies einen Verstoß gegen diese Voraussetzung bedeuten, was zu Fehlern führen kann.

**Nicht zu empfehlen:**

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

**Zu empfehlen:**

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

## <a name="use-css-modules-to-avoid-styling-conflicts"></a>Verwenden von CSS-Modulen zur Vermeidung von Formatkonflikten

SharePoint Framework-Lösungen sind Teil der Seite. Um sicherzustellen, dass CSS-Formatvorlagen für eine Komponente keine Auswirkungen auf andere Elemente auf der Seite haben, sollten Sie Ihre CSS-Selektoren so verwenden, dass sie nur für das DOM Ihrer Lösung gelten. Bei manueller Ausführung ist dies mühsam und fehleranfällig, in SharePoint Framework kann dies jedoch automatisch ausgeführt werden.

Um Formatkonflikte zu vermeiden, verwendet SharePoint Framework [CSS-Module](https://github.com/css-modules/css-modules). Beim Erstellen des Projekts verarbeitet die SharePoint Framework-Toolkette alle Dateien mit der Erweiterung **. module.scss**. Alle Klassenselektoren werden für jede Datei gelesen und diesen wird ein eindeutiger Hashwert angefügt. Nach Abschluss werden die aktualisierten Selektoren in Zwischen-CSS-Dateien geschrieben, die im generierten Webpartpaket enthalten sind.

Gehen Sie gemäß dem obigen Beispiel davon aus, dass Sie über die beiden folgenden Sass-Dateien verfügen:

**todoList.module.scss:**

```scss
.todoList {
  margin: 1em 0;

  .text {
    font-weight: bold;
    font-size: 1.5em;
  }
}
```

**todoItem.module.scss:**

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

Nach dem Erstellen des Projekts würden Sie im Ordner **lib** die folgenden beiden generierten CSS-Dateien sehen (Zeilenumbrüche und Einzüge wurden zur besseren Lesbarkeit hinzugefügt):

**todoList.module.css:**

```css
.todoList_3e9d35f0 {
  margin:1em 0
}

.todoList_3e9d35f0 .text_3e9d35f0 {
  font-weight:700;
  font-size:1.5em
}
```

**todoItem.module.css:**

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

Obwohl eine **.text**-Klasse in beiden Sass-Dateien definiert wurde, werden Sie feststellen, dass in den generierten CSS-Dateien zwei Hashes angefügt wurden, sodass ein eindeutiger Klassenname entsteht, der für jede Komponente spezifisch ist.

Die CSS-Klassennamen in CSS-Modulen werden dynamisch generiert, sodass Sie nicht direkt im Code auf diese verweisen können. Stattdessen generiert die SharePoint Framework-Toolkette beim Verarbeiten von CSS-Modulen eine JavaScript-Datei mit Verweisen auf die generierten Klassennamen.

**todoList.module.scss.js:**

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

Um die generierten Klassennamen in Ihrem Code zu verwenden, importieren Sie zunächst die Formatvorlagen Ihrer Komponente, und verwenden Sie dann die Eigenschaft, die auf die jeweilige Klasse zeigt:

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

Damit die CSS-Module ordnungsgemäß funktionieren, müssen Sie die folgenden Bedingungen erfüllen:

* Die Sass-Dateien müssen die Erweiterung **.module.scss** aufweisen. Wenn Sie die Erweiterung **.scss** ohne **.module** verwenden, wird beim Erstellungsprozess eine Warnung angezeigt. Die Sass-Datei wird in eine Zwischen-CSS-Datei übertragen, die Klassennamen **werden aber nicht eindeutig gemacht**. Dies kann in Fällen, in denen Sie CSS-Formatvorlagen von Drittanbietern außer Kraft setzen müssen, beabsichtigt sein.
* Die CSS-Klassennamen müssen gültige JavaScript-Variablennamen sein, sie dürfen also zum Beispiel keine Bindestriche enthalten: `todoList` ist richtig, `todo-list` jedoch nicht.
* camelCase-Benennung für Klassen wird empfohlen, wird aber nicht erzwungen

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a>Verpacken Sie Ihre CSS-Formatvorlagen in einer Klasse, die nach der Komponente benannt ist

Durch Kombinieren von CSS-Modulen mit der Unterstützung von Sass zum Verschachteln von Regelsätzen können Sie Ihre CSS-Formatvorlagen vereinfachen und sicherstellen, dass diese keine Auswirkungen auf andere Elemente auf der Seite haben.

Verpacken Sie beim Erstellen von CSS-Formatvorlagen für eine Komponente diese in einer Klasse, die nach der Komponente benannt ist. Weisen Sie diese Klassen dann in der Komponente dem Stammelement der Komponente zu.

**todoList.module.scss:**

```scss
.todoList {
  a {
    display: block;
  }
}
```

**TodoList.tsx:**

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

Nach der Übertragung sieht die generierte CSS-Datei in etwa wie folgt aus:

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

Da der Selektor mit dem eindeutigen Klassennamen beginnt, der spezifisch für die Komponente ist, gilt die alternative Präsentation nur für Hyperlinks innerhalb der Komponenten.

## <a name="handling-of-css-vendor-prefix"></a>Verwenden von CSS-Anbieterpräfixen
In SPFx sind keine Formatvorlagen mit Anbieterpräfix in SASS- oder CSS-Dateien eines Projekts erforderlich. Wenn für einige Browser mit SPFx-Unterstützung Präfixe erforderlich sind, wurden diese automatisch nach der Kompilierung von SASS zu CSS hinzugefügt. Diese Methode wird auch als automatisches Voranstellen von Präfixen bezeichnet und ist grundlegender Bestandteil der CSS-Buildkette in SPFx.

Falls ein Webpart das neue Flexboxmodell verwenden sollte, das von der `display: flex`-Deklaration definiert wird. Für einige ältere WebKit-basierte und Internet Explorer-Versionen muss ein bestimmtes Anbieterpräfix in der CSS-Datei definiert sein.

```css
.container{
  display: flex;
}
```

Im SASS-Code des SPFx-Artefakts müssen keine Anbieterpräfixe enthalten sein. Nach der Kompilierung von SASS zu CSS wurden diese automatisch hinzugefügt, sodass die CSS-Deklaration wie folgt aussieht.

```css
.container_7e976ae1 {
  display: -webkit-box; // older Safari on MacOS and iOS
  display: -ms-flexbox; // IE 10 - 11
  display: flex;
}
```

Durch das Entfernen bereits angewendeter Präfixe wird der Code des Artefakts nicht nur übersichtlicher. Er wird auch lesbarer und zukunftsorientiert. Dieser Vorgang wird auch konfiguriert, um nur Browser mit SPFx-Unterstützung zu unterstützen, und sorgt für weniger Fehler.
Falls ein Webpart bereits Anbieterpräfixe in den SASS-Dateien enthält, die nicht mehr benötigt werden, werden diese Deklarationen mit demselben Vorgang automatisch entfernt.

Im folgenden Beispiel wird die `border-radius`-Eigenschaft verwendet. Eine Eigenschaft, für die keine Anbieterpräfixe auf den unterstützten Systemen erforderlich sind.

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

Die resultierende CSS-Datei in dem Paket wird in den folgenden Code konvertiert.

```css
.container_9e54c0b0 {
  border-radius: 7px
}
```

Weitere Informationen zum automatischen Voranstellen von Präfixen finden Sie in der Dokumentation im GitHub-Repository unter „[autoprefix](https://github.com/postcss/autoprefixer)“. Die Datenbank während des gesamten Prozesses ist unter [caniuse.com](https://caniuse.com) verfügbar.

## <a name="integrate-office-ui-fabric"></a>Integration von Office UI Fabric

Indem Sie dafür sorgen, dass Ihre Anpassungen wie die Standardfunktionen von SharePoint und Office 365 aussehen und sich so verhalten, können Sie Endbenutzern das Arbeiten damit erleichtern. Office UI Fabric bietet Ihnen eine Reihe von Steuerelementen und Formatvorlagen, die Sie in Ihren Anpassungen verwenden können, um eine nahtlose Integration in die vorhandene Benutzeroberfläche zu gewährleisten. Weitere Informationen zur Verwendung von Office UI Fabric im SharePoint Framework finden Sie im [Office UI Fabric-Integrationsleitfaden](./office-ui-fabric-integration.md).

## <a name="use-theme-colors"></a>Verwenden von Designfarben

In SharePoint können Benutzer die Designfarbe für Ihre Websites auswählen. In Ihren SharePoint Framework-Anpassungen sollten Sie dasselbe Design verwenden, das von den Benutzern ausgewählt wurde, damit Ihre Anpassung wie ein fester Bestandteil der Website aussieht und nicht unnötig hervorsticht. Da das Design von Benutzern auf deren Website festgelegt wird, können Sie nicht vorab festlegen, welche Farben Ihre Anpassung verwenden sollte, in SharePoint Framework kann das derzeit aktive Farbschema jedoch dynamisch und automatisch für Sie geladen werden. Weitere Informationen zu dieser Funktion finden Sie im [Leitfaden zur Verwendung von Designfarben](./use-theme-colors-in-your-customizations.md).
