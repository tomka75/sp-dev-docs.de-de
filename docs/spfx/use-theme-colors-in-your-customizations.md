---
title: Verwenden von Designfarben in Ihren SharePoint Framework-Anpassungen
description: "Verwenden Sie Designfarben, damit Ihre Anpassungen wie ein Teil der Website aussehen, indem Sie auf die Designfarben der Kontextwebsite in Ihrer SharePoint Framework-Lösung verweisen."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 1fa72a0304eeb3ed93328e5040f9ca1a580a3b82
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="use-theme-colors-in-your-sharepoint-framework-customizations"></a>Verwenden von Designfarben in Ihren SharePoint Framework-Anpassungen

Beim Erstellen von SharePoint Framework-Anpassungen sollten Sie Designfarben verwenden, damit Ihre Anpassungen wie ein Teil der Website aussehen. In diesem Artikel wird erläutert, wie Sie auf die Designfarben der Kontextwebsite in Ihrer SharePoint Framework-Lösung verweisen.

> [!NOTE] 
> In diesem Artikel wird zwar ein clientseitiges SharePoint-Framework-Webpart als Beispiel verwendet, die beschriebenen Techniken gelten jedoch für alle Typen von SharePoint-Framework-Anpassungen.

## <a name="fixed-colors-vs-theme-colors"></a>Feste Farben im Vergleich zu Designfarben

Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird eine feste blaue Palette verwendet. Wenn Sie ein solches Webpart mithilfe eines anderen Farbschemas zu einer modernen Website hinzufügen, sticht dieses hervor und sieht nicht wie ein Teil der Website aus.

![Clientseitiges SharePoint Framework-Webpart mit blauem Farbschema auf einer modernen Teamwebsite, die ein rotes Design aufweist](../images/themed-styles-blue-web-part-red-site.png)

Wenn Sie feste Farben verwenden, entscheiden Sie vorab, welche Farben für welche Elemente verwendet werden sollen. Dies kann zu einer Situation wie soeben beschrieben führen, bei der ein blaues Webpart auf einer roten Teamwebsite angezeigt wird und unnötig hervorsticht. In den meisten Fällen sollten Sie sich bemühen, die Designfarben der Kontextwebsite zu verwenden, damit Ihre Lösung nicht hervorsticht, sondern wie ein Teil der Website aussieht.

In SharePoint Framework können Sie auf die Designfarben der Kontextwebsite verweisen anstatt feste Farben zu verwenden. Ihr Webpart wird folglich auf einer Website mit einem roten Design platziert, es verwendet ebenfalls die rote Palette und passt sich selbst automatisch an die blaue Palette an, wenn es auf einer Website platziert wird, die das blaue Design verwendet. All dies erfolgt automatisch ohne Änderungen am Code des Webparts.

## <a name="use-theme-colors-in-the-sharepoint-framework"></a>Verwenden von Designfarben im SharePoint Framework

Wenn Sie mit festen Farben arbeiten, geben Sie diese in CSS-Eigenschaften an, z. B.:

```css
.button {
    background-color: #0078d7;
}
```

<br/>

Um stattdessen eine Designfarbe zu verwenden, ersetzen Sie die feste Farbe durch ein Designtoken:

```css
.button {
    background-color: "[theme: themePrimary, default: #0078d7]";
}
```

<br/>

Wenn Ihre SharePoint Framework-Anpassung auf der Seite geladen wird, sucht das Paket **@microsoft/load-themed-styles**, das ein Teil von SharePoint Framework ist, nach Designtoken in CSS-Dateien und versucht, diese durch die entsprechende Farbe aus dem aktuellen Design zu ersetzen. Wenn der Wert für das angegebene Token nicht verfügbar ist, verwendet SharePoint Framework stattdessen den Wert, der unter Verwendung des Parameters **Standard** angegeben wird – daher es wichtig ist, dass Sie diesen immer einschließen.

Die folgenden Designtoken stehen für Sie zur Verfügung:

Token|Standardwert auf einer modernen Teamwebsite, auf der die rote Palette verwendet wird|Bemerkungen
-----|--------------------------------|-----------
`backgroundImageUri`|`none`|
`themeAccent`|`#ee0410`|
`themeAccentTranslucent10`|`rgba(238, 4, 16, 0.10)`|
`themeDark`|`#b3030c`|Wird für Aktionssymbole in der Befehlsleiste und als Hoverfarbe verwendet.
`themeDarkAlt`|`#b3030c`|
`themeDarker`|`#770208`|
`themeLight`|`#fd969b`|
`themeLightAlt`|`#fd969b`|
`themeLighter`|`#fecacd`|
`themeLighterAlt`|`#fecacd`|
`themePrimary`|`#ee0410`|Primäre Designfarbe. Wird für Symbole und Standardschaltflächen verwendet.
`themeSecondary`|`#fc6169`|
`themeTertiary`|`#fd969b`|
`themeTertiaryAlt`|`#fd969b`|

> [!NOTE] 
> Es gibt weitere Token, die bei SharePoint Frameworks registriert sind. Für alle Token sind zwar Werte auf klassischen Websites angegeben, nur die zuvor erwähnte Teilmenge weist jedoch Werte auf modernen SharePoint-Websites auf. Die vollständige Liste verfügbarer Token finden Sie unter dem Wert der `window.__themeState__.theme`-Eigenschaft mithilfe der Konsole in den Entwicklertools Ihres Webbrowsers.

## <a name="use-theme-colors-in-your-customizations"></a>Verwenden von Designfarben in Ihren Anpassungen

Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird standardmäßig die feste blaue Palette verwendet. Die folgenden Schritte beschreiben die Anpassungen, die erforderlich sind, damit das Webpart stattdessen Designfarben verwendet.

> [!NOTE] 
> Die folgenden Schritte gelten für ein clientseitiges SharePoint Framework-Webpart mit dem Namen _HelloWorld_, das mithilfe von React erstellt wurde. Für Webparts, die mit anderen Bibliotheken und anderen Typen von Anpassungen erstellt werden, müssen Sie die Änderungen möglicherweise anpassen.

### <a name="to-use-theme-colors"></a>So verwenden Sie Designfarben

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/helloWorld/components/HelloWorld.tsx**, und entfernen Sie aus dem Div mit der Klasse **ms-Raster-Row** die Klasse **ms-BgColor-ThemeDark**.

    ![Die Klasse „ms-bgColor-themeDark“ ausgewählt im Visual Studio-Code-Editor](../images/themed-styles-ms-bgcolor-themedark-class.png)

2. Öffnen Sie in demselben Ordner die Datei **HelloWorld.module.scss**. Ändern Sie den `.row`-Selektor folgendermaßen:

    ```css
    .row {
        padding: 20px;
        background-color: "[theme: themeDark, default: #005a9e]";
    }
    ```

    <br/>

    ![Der erweiterte .row-Selektor mit Hintergrundfarbe](../images/themed-styles-row-class.png)

3. Ändern Sie im `.button`-Selektor die Eigenschaften `background-color` und `border-color` folgendermaßen:

    ```css
    .button {
        /* ... */
        background-color: "[theme: themePrimary, default: #0078d7]";
        border-color: "[theme: themePrimary, default: #0078d7]";
        /* ... */
    }
    ```

    <br/>

    ![Der aktualisierte .button-Selektor mit Verweisen auf Designfarben](../images/themed-styles-button-class.png)

4. Wenn Sie das Webpart zu einer Website hinzufügen, werden die vom Webpart verwendeten Farben automatisch an die von der aktuellen Website verwendeten Designfarben angepasst.

    ![Parallele Ansicht desselben Webparts, das in zwei Websites mit unterschiedlichen Farben angezeigt wird. Das Webpart folgt dem Farbschema der jeweiligen Website.](../images/themed-styles-side-by-side.png)

## <a name="see-also"></a>Weitere Artikel

- [Designs und Farben in SharePoint](../design/themes-colors.md)
- [How to use Theme Colors in SPFX Web Parts](https://n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/) von Stefan Bauer (Office Development MVP)
