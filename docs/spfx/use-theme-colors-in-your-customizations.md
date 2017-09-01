# <a name="use-theme-colors-in-your-sharepoint-framework-customizations"></a>Verwenden von Designfarben in Ihren SharePoint Framework-Anpassungen

Beim Erstellen von SharePoint Framework-Anpassungen sollten Sie Designfarben verwenden, damit Ihre Anpassungen wie ein Teil der Website aussehen. In diesem Artikel wird erläutert, wie Sie auf die Designfarben der Kontextwebsite in Ihrer SharePoint Framework-Lösung verweisen können.

> **Hinweis:** In diesem Artikel wird zwar ein clientseitiges SharePoint Framework-Webpart als Beispiel verwendet, die beschriebenen Techniken gelten jedoch für alle Typen von SharePoint Framework-Anpassungen.

## <a name="fixed-colors-vs-theme-colors"></a>Feste Farben im Vergleich zu Designfarben

Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird dafür eine feste Palette mit Blautönen verwendet. Wenn Sie ein solches Webpart zu einer modernen Website hinzufügen, die ein anderes Farbschema verwendet, sticht dieses hervor und sieht nicht wie ein Teil der Website aus.

![Clientseitiges SharePoint Framework-Webpart mit blauem Farbschema auf einer modernen Teamwebsite, die ein rotes Design aufweist](../../images/themed-styles-blue-web-part-red-site.png)

Wenn Sie feste Farben verwenden, entscheiden Sie vorab, welche Farben für welche Elemente verwendet werden sollen. Dies kann zu einer Situation wie oben beschrieben führen, bei der ein blaues Webpart auf einer roten Teamwebsite angezeigt wird und unnötig hervorsticht. In den meisten Fällen bietet es sich an, die Designfarben der Kontextwebsite zu verwenden, damit Ihre Lösung nicht hervorsticht, sondern wie ein Teil der Website aussieht.

In SharePoint Framework können Sie anstelle der Verwendung von festen Farben auf Designfarben der Kontextwebsite verweisen. Wenn Ihr Webpart auf einer Website mit rotem Design platziert wird, wird folglich auch die rote Palette verwendet; wenn es auf einer Website mit dem blauen Design verwendet wird, wird es automatisch an die blaue Palette angepasst. All dies erfolgt automatisch, ohne dass Änderungen am Webpartcode vorgenommen werden.

## <a name="using-theme-colors-in-the-sharepoint-framework"></a>Verwenden von Designfarben im SharePoint Framework

Wenn Sie mit festen Farben arbeiten, geben Sie diese in CSS-Eigenschaften an, z. B.:

```css
.button {
    background-color: #0078d7;
}
```

Um stattdessen eine Designfarbe zu verwenden, ersetzen Sie die feste Farbe durch ein Designtoken:

```css
.button {
    background-color: "[theme: themePrimary, default: #0078d7]";
}
```

Wenn Ihre SharePoint Framework-Anpassung auf der Seite geladen wird, sucht das Paket **@microsoft/load-themed-styles**, das Teil von SharePoint Framework ist, nach Designtoken in CSS-Dateien und versucht, diese durch die entsprechende Farbe aus dem aktuellen Design zu ersetzen. Wenn der Wert für das angegebene Token nicht verfügbar ist, verwendet SharePoint Framework stattdessen den mithilfe des **Standard**parameters angegebenen Wert, deshalb ist es so wichtig, dass Sie diesen immer einschließen.

Folgende Designtoken stehen für Sie zur Verfügung:

Token|Standardwert auf einer modernen Teamwebsite, auf der die rote Palette verwendet wird|Hinweise
-----|--------------------------------|-----------
`backgroundImageUri`|`none`|
`themeAccent`|`#ee0410`|
`themeAccentTranslucent10`|`rgba(238, 4, 16, 0.10)`|
`themeDark`|`#b3030c`|Wird für Aktionssymbole in der Befehlsleiste und als Hoverfarbe verwendet
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

> **Hinweis:** Es gibt weitere Token, die in SharePoint Framework registriert sind. Alle diese Token weisen Werte auf, die in klassischen Websites angegeben sind, nur die zuvor erwähnte Untergruppe weist Werte für moderne SharePoint-Websites auf. Die vollständige Liste verfügbarer Token finden Sie im Wert der `window.__themeState__.theme`-Eigenschaft mithilfe der Konsole in den Entwicklertools Ihres Webbrowsers.

## <a name="use-theme-colors-in-your-customizations"></a>Verwenden von Designfarben in Ihren Anpassungen

Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird standardmäßig die feste Palette für Blautöne verwendet. In den folgenden Schritten werden die Anpassungen beschrieben, die erforderlich sind, damit das Webpart stattdessen Designfarben verwendet.

> **Hinweis:** In den folgenden Schritten wird ein clientseitiges SharePoint Framework-Webpart mit dem Namen _HelloWorld_ mithilfe von React angewendet. Für Webparts, die mit anderen Bibliotheken und anderen Anpassungstypen erstellt wurden, müssen Sie die Änderungen möglicherweise entsprechend anpassen.

Öffnen Sie im Code-Editor die Datei **./src/webparts/helloWorld/components/HelloWorld.tsx**, und entfernen Sie aus dem Div mit der Klasse **ms-Raster-Row** die Klasse **ms-BgColor-ThemeDark**Klasse.

![Die Klasse „ms-bgColor-themeDark“ ausgewählt im Visual Studio-Code-Editor](../../images/themed-styles-ms-bgcolor-themedark-class.png)

Öffnen Sie als Nächstes in demselben Ordner die Datei **HelloWorld.module.scss**. Ändern Sie den `.row`-Selektor folgendermaßen:

```css
.row {
    padding: 20px;
    background-color: "[theme: themeDark, default: #005a9e]";
}
```

![Der erweiterte .row-Selektor mit Hintergrundfarbe](../../images/themed-styles-row-class.png)

Ändern Sie im `.button`-Selektor die Eigenschaften `background-color` und `border-color` folgendermaßen:

```css
.button {
    /* ... */
    background-color: "[theme: themePrimary, default: #0078d7]";
    border-color: "[theme: themePrimary, default: #0078d7]";
    /* ... */
}
```

![Der aktualisierte .button-Selektor mit Verweisen auf Designfarben](../../images/themed-styles-button-class.png)

Wenn Sie das Webpart zu einer Website hinzufügen, werden die vom Webpart verwendeten Farben automatisch an die von der aktuellen Website verwendeten Designfarben angepasst.

![Parallele Ansicht desselben Webparts, das in zwei Websites mit unterschiedlichen Farben angezeigt wird. Das Webpart folgt dem Farbschema der jeweiligen Website.](../../images/themed-styles-side-by-side.png)

## <a name="more-information"></a>Weitere Informationen

* [How to use Theme Colors in SPFX Web Parts](http://www.n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/) von Stefan Bauer (Office Development MVP)