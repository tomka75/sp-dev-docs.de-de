---
title: "Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen"
description: "Mit CSS können Sie das Aussehen und das Verhalten von SharePoint-Framework-Anpassungen definieren."
ms.date: 1/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 2258d163f47b5961555f9362aa87a9c1ab82ba39
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a>Empfehlungen für das Arbeiten mit CSS in SharePoint-Framework-Lösungen

Bei der Erstellung von SharePoint-Framework-Lösungen können Sie mithilfe von CSS definieren, wie Ihre Anpassungen aussehen und wie sie sich verhalten sollen. In diesem Artikel wird beschrieben, wie Sie die vom SharePoint-Framework bereitgestellten Funktionen optimal nutzen und stabile CSS-Formatvorlagen erstellen können.

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a>SharePoint-Framework-Anpassungen als Teil der Seite

Wenn Sie SharePoint-Anpassungen mithilfe des Add-In-Modells erstellen, ist Ihre Lösung von anderen Elementen auf der Seite isoliert. Ihr Code kann als Add-In-Webpart in einem iFrame ausgeführt werden oder als immersive Anwendung, von der die gesamte Seite gesteuert wird. In beiden Fällen haben andere Elemente und Formatvorlagen, die auf der Seite definiert sind, keine Auswirkungen auf den Code.

SharePoint-Framework-Lösungen sind Teil der Seite und vollständig in das DOM der Seite integriert. Dadurch fallen zwar verschiedene Einschränkungen des Add-In-Modells weg, es entstehen jedoch auch Risiken für die Lösung. Da sie Teil der Seite ist, gilt: Solange Sie die Lösung nicht explizit isolieren, werden sämtliche auf der Seite definierten CSS-Vorlagen auf sie angewendet. Das kann dazu führen, dass die Oberfläche anders aussieht als von Ihnen vorgesehen. Um das zu vermeiden, sollten Sie Ihre CSS-Formatvorlagen so definieren, dass sie sich ausschließlich auf Ihre Anpassung auswirken, nicht jedoch auf andere Seitenelemente.

## <a name="organize-css-files-in-your-solution"></a>Organisieren von CSS-Dateien in Ihrer Lösung

Oft besteht die Benutzeroberfläche einer Lösung aus mehreren Bausteinen. In vielen JavaScript-Bibliotheken werden diese Bausteine als Komponenten bezeichnet. Eine Komponente kann einfach sein und nur die Darstellungsweise definieren, oder sie kann komplexer sein und sowohl den Status als auch andere Komponenten enthalten. Wenn Sie Ihre Lösung in mehrere Komponenten unterteilen, vereinfacht das den Entwicklungsprozess und macht es leichter, die Komponenten zu testen und in Ihrer Lösung wiederzuverwenden.

Da Komponenten visuell dargestellt werden, sind für sie oftmals CSS-Formatvorlagen erforderlich. Im Idealfall sollten Komponenten isoliert werden und eigenständig nutzbar sein. Um das zu erreichen, ist es sinnvoll, die CSS-Formatvorlagen einer Komponente zusammen mit allen anderen Objektdateien der Komponente zu speichern. Unten sehen Sie eine Beispielstruktur einer React-Anwendung mit verschiedenen Komponenten, die jeweils eine eigene CSS-Datei haben.

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

Im SharePoint-Framework können Sie sowohl CSS als auch Sass verwenden. Sass ist eine CSS übergeordnete Sprache und bietet eine Reihe von Funktionen, die die Arbeit mit und die Verwaltung von CSS-Formatvorlagen langfristig einfacher machen. Zu diesen Funktionen gehören beispielsweise Variablen, Schachtelungsselektoren und Mixins. 

Eine umfassende Übersicht über alle Funktionen finden Sie auf der [Sass-Website](http://sass-lang.com). Jeder gültige CSS-Code ist auch gültiger Sass-Code. Das ist sehr nützlich, falls Sie bisher noch nicht mit Sass gearbeitet haben und sich Schritt für Schritt mit den Funktionen der Sprache vertraut machen möchten.

## <a name="avoid-using-ids-in-markup"></a>Vermeiden der Verwendung von IDs im Markup

Wenn Sie mit dem SharePoint-Framework arbeiten, erstellen Sie Anpassungen, die Endbenutzer SharePoint hinzufügen. Vorab lässt sich unmöglich voraussehen, ob auf einer Seite nur eine einzige Instanz einer Anpassung implementiert wird oder ob mehrere Instanzen verwendet werden. 

Um Probleme zu vermeiden, sollten Sie immer davon ausgehen, dass auf einer Seite mehrere Instanzen Ihrer Anpassung verwendet werden. Daher sollten Sie keine IDs in Ihrem Markup verwenden. IDs müssen auf einer Seite immer eindeutig sein; fügt ein Benutzer zwei Instanzen Ihres Webparts zu einer Seite hinzu, wird damit gegen diese Vorgabe verstoßen, und es kann zu Fehlern kommen.

#### <a name="bad-practice"></a>Nicht zu empfehlen:

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

<br/>

#### <a name="good-practice"></a>Zu empfehlen:

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

Das SharePoint-Framework verwendet [CSS-Module](https://github.com/css-modules/css-modules), um Formatkonflikte zu vermeiden. Wenn Sie ein Projekt erstellen, verarbeitet die SharePoint-Framework-Toolkette alle Dateien mit der Dateiendung **.module.scss**. Sie liest die Klassenselektoren jeder Datei und fügt ihnen jeweils einen eindeutigen Hashwert an. Anschließend werden die aktualisierten Selektoren in CSS-Zwischendateien geschrieben, die in das generierte Webpartpaket gepackt werden.

Nehmen wir das oben angeführte Beispiel, und gehen wir davon aus, wir arbeiten mit den folgenden beiden Sass-Dateien:

#### <a name="todolistmodulescss"></a>todoList.module.scss

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

#### <a name="todoitemmodulescss"></a>todoItem.module.scss

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<br/>

Nach dem Erstellen des Projekts würden Sie im Ordner **lib** die folgenden beiden generierten CSS-Dateien sehen (Zeilenumbrüche und Einzüge wurden zur besseren Lesbarkeit hinzugefügt):

#### <a name="todolistmodulecss"></a>todoList.module.css

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

#### <a name="todoitemmodulecss"></a>todoItem.module.css

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<br/>

Obwohl eine **.text**-Klasse in beiden Sass-Dateien definiert wurde, werden Sie feststellen, dass in den generierten CSS-Dateien zwei Hashes angefügt wurden, sodass ein eindeutiger Klassenname entsteht, der für jede Komponente spezifisch ist.

Die CSS-Klassennamen in CSS-Modulen werden dynamisch generiert, sodass Sie nicht direkt im Code auf diese verweisen können. Stattdessen generiert die SharePoint Framework-Toolkette beim Verarbeiten von CSS-Modulen eine JavaScript-Datei mit Verweisen auf die generierten Klassennamen.

#### <a name="todolistmodulescssjs"></a>todoList.module.scss.js

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

Um die generierten Klassennamen in Ihrem Code verwenden zu können, müssen Sie zunächst die Formatvorlagen Ihrer Komponente importieren. Anschließend verwenden Sie die Eigenschaft, die auf die betreffende Klasse zeigt:

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

<br/>

Damit die CSS-Module korrekt funktionieren, müssen die folgenden Bedingungen erfüllt sein:

* Ihre Sass-Dateien müssen die Dateiendung **.module.scss** haben. Wenn Sie die Dateiendung **.scss** ohne **.module** verwenden, wird während des Erstellungsprozesses eine Warnmeldung angezeigt. Die Sass-Datei wird in eine CSS-Zwischendatei transpiliert, wobei die Klassennamen jedoch *nicht eindeutig gemacht werden*. Falls Sie CSS-Formatvorlagen von Drittanbietern überschreiben müssen, ist dies möglicherweise gewollt.

* Alle CSS-Klassennamen müssen gültige JavaScript-Variablennamen sein. Sie dürfen beispielsweise keine Bindestriche enthalten: `todoList` ist korrekt, `todo-list` jedoch nicht.

* Wir empfehlen die CamelCase-Notation für die Benennung von Klassen. Obligatorisch ist die Verwendung dieser Notation jedoch nicht.

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a>Einbetten von CSS-Formatvorlagen in eine nach der Komponente benannten Klasse

Wenn Sie CSS-Module und die Sass-Unterstützung für die Schachtelung von Regelsätzen miteinander kombinieren, können Sie Ihre CSS-Formatvorlagen vereinfachen und sicherstellen, dass sie keine Auswirkungen auf andere Seitenelemente haben.

Betten Sie dazu die CSS-Formatvorlagen Ihrer Komponente bei der Erstellung in eine Klasse ein, die nach der Komponente benannt ist. In der Komponente selbst muss die Klasse dem Stammelement der Komponente zugewiesen werden.

#### <a name="todolistmodulescss"></a>todoList.module.scss

```scss
.todoList {
  a {
    display: block;
  }
}
```

<br/>

#### <a name="todolisttsx"></a>TodoList.tsx

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

Nach der Transpilierung sieht die generierte CSS-Datei in etwa wie folgt aus:

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

Da der Selektor mit dem eindeutigen Klassennamen beginnt, der spezifisch für die Komponente ist, gilt die alternative Darstellung nur für Links innerhalb der Komponente.

## <a name="handling-of-css-vendor-prefix"></a>Verarbeiten von CSS-Anbieterpräfixen

Im SharePoint-Framework müssen in den Sass- oder CSS-Dateien von Projekten nicht zwingend Formateigenschaften mit Anbieterpräfix verwendet werden. Für den Fall, dass einige der vom SharePoint-Framework unterstützten Browser Präfixe fordern, werden diese automatisch nach der Kompilierung von Sass zu CSS hinzugefügt. Diese Methode wird auch als automatische Voranstellung von Präfixen (Prefixing) bezeichnet und ist grundlegender Bestandteil der CSS-Buildkette im SharePoint-Framework.

Falls Ihr Webpart das neue Flex-Box-Modell verwendet (definiert durch die Deklaration `display: flex`), erfordern einige ältere WebKit-basierte Browser und Internet Explorer-Versionen einen bestimmten Anbieterpräfix im CSS-Code.

```css
.container{
  display: flex;
}
```

<br/>

Der Sass-Code des SharePoint-Framework-Artefakts muss keine Anbieterpräfixes enthalten. Nach der Kompilierung von Sass zu CSS werden diese automatisch hinzugefügt, sodass die CSS-Deklaration wie folgt aussieht:

```css
.container_7e976ae1 {
  display: -webkit-box; // older Safari on MacOS and iOS
  display: -ms-flexbox; // IE 10 - 11
  display: flex;
}
```

<br/>

Durch das Entfernen bereits angewendeter Präfixe wird der Artefaktcode nicht nur übersichtlicher, sondern auch einfacher lesbar und zukunftssicherer. Darüber hinaus ist dieser Prozess so konfiguriert, dass nur vom SharePoint-Framework unterstützte Browser unterstützt werden. Das sichert effektiver gegen Fehler ab.

Falls die Sass-Dateien eines Webparts bereits Anbieterpräfixe enthalten, die nicht mehr benötigt werden, werden diese Deklarationen über denselben Prozess automatisch entfernt.

Im nachfolgenden Beispiel wird die Eigenschaft `border-radius` verwendet, die keine Anbieterpräfixe auf den unterstützten Systemen erfordert.

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

Der resultierende CSS-Code im Paket wird in den folgenden Code umgewandelt:

```css
.container_9e54c0b0 {
  border-radius: 7px
}
```

Weitere Informationen zum automatischen Prefixing finden Sie im GitHub-Repository [autoprefixer](https://github.com/postcss/autoprefixer). Die Datenbank für diesen Prozess ist auf [Can I use__?](https://caniuse.com) verfügbar.

## <a name="integrate-office-ui-fabric"></a>Integrieren von Office UI Fabric

Wenn Sie Ihre Anpassung so gestalten, dass sie in puncto Aussehen und Verhalten den Standardfunktionen von SharePoint und Office 365 entspricht, machen Sie es Endbenutzern einfacher, mit ihr zu arbeiten. Office UI Fabric bietet eine Reihe von Steuerelementen und Formatvorlagen für Anpassungen, mit denen eine nahtlose Integration in die vorhandene Benutzeroberfläche möglich ist. 

Weitere Informationen zur Verwendung von Office UI Fabric im SharePoint-Framework finden Sie unter [Verwenden von Office UI Fabric Core und Fabric React im SharePoint-Framework](./office-ui-fabric-integration.md).

## <a name="use-theme-colors"></a>Verwenden von Farbdesigns

SharePoint ermöglicht es Benutzern, ein Farbdesign für ihre Website auszuwählen. Damit Ihre SharePoint-Framework-Anpassung wie ein integraler Bestandteil der Website aussieht und nicht unnötig heraussticht, sollte sie jeweils das vom Benutzer ausgewählte Design verwenden. 

Da die Benutzer selbst das Design für eine Website festlegen, wissen Sie vorab nicht, welche Farben Ihre Anpassung verwenden sollte. Das SharePoint-Framework kann das aktuell aktive Farbdesign jedoch automatisch dynamisch für Sie laden. 

Weitere Informationen zu dieser Funktion finden Sie unter [Verwenden von Designfarben in Ihren SharePoint-Framework-Anpassungen](./use-theme-colors-in-your-customizations.md).




