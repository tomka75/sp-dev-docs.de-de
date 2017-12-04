---
title: Verwenden von Designfarben in Ihren SharePoint Framework-Anpassungen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f7f8c24bb2483064504e75e71a19caf1914874f4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="use-theme-colors-in-your-sharepoint-framework-customizations"></a><span data-ttu-id="6972c-102">Verwenden von Designfarben in Ihren SharePoint Framework-Anpassungen</span><span class="sxs-lookup"><span data-stu-id="6972c-102">Use theme colors in your SharePoint Framework customizations</span></span>

<span data-ttu-id="6972c-p101">Beim Erstellen von SharePoint Framework-Anpassungen sollten Sie Designfarben verwenden, damit Ihre Anpassungen wie ein Teil der Website aussehen. In diesem Artikel wird erläutert, wie Sie auf die Designfarben der Kontextwebsite in Ihrer SharePoint Framework-Lösung verweisen können.</span><span class="sxs-lookup"><span data-stu-id="6972c-p101">When building SharePoint Framework customizations you should use theme colors, so that your customizations looks like a part of the site. This article explains how can you refer to the theme colors of the context site in your SharePoint Framework solution.</span></span>

> <span data-ttu-id="6972c-105">**Hinweis:** In diesem Artikel wird zwar ein clientseitiges SharePoint Framework-Webpart als Beispiel verwendet, die beschriebenen Techniken gelten jedoch für alle Typen von SharePoint Framework-Anpassungen.</span><span class="sxs-lookup"><span data-stu-id="6972c-105">**Note:** although this article uses SharePoint Framework client-side web part as example, the described techniques apply to all types of SharePoint Framework customizations.</span></span>

## <a name="fixed-colors-vs-theme-colors"></a><span data-ttu-id="6972c-106">Feste Farben im Vergleich zu Designfarben</span><span class="sxs-lookup"><span data-stu-id="6972c-106">Fixed colors vs. theme colors</span></span>

<span data-ttu-id="6972c-p102">Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird dafür eine feste Palette mit Blautönen verwendet. Wenn Sie ein solches Webpart zu einer modernen Website hinzufügen, die ein anderes Farbschema verwendet, sticht dieses hervor und sieht nicht wie ein Teil der Website aus.</span><span class="sxs-lookup"><span data-stu-id="6972c-p102">When you scaffold a new SharePoint Framework client-side web part, it uses a fixed blue palette. When you add such web part on a modern site, using a different color scheme, it stands out and doesn't look like a part of the site.</span></span>

![Clientseitiges SharePoint Framework-Webpart mit blauem Farbschema auf einer modernen Teamwebsite, die ein rotes Design aufweist](../images/themed-styles-blue-web-part-red-site.png)

<span data-ttu-id="6972c-p103">Wenn Sie feste Farben verwenden, entscheiden Sie vorab, welche Farben für welche Elemente verwendet werden sollen. Dies kann zu einer Situation wie oben beschrieben führen, bei der ein blaues Webpart auf einer roten Teamwebsite angezeigt wird und unnötig hervorsticht. In den meisten Fällen bietet es sich an, die Designfarben der Kontextwebsite zu verwenden, damit Ihre Lösung nicht hervorsticht, sondern wie ein Teil der Website aussieht.</span><span class="sxs-lookup"><span data-stu-id="6972c-p103">When using fixed colors, you decide upfront which colors you want to use for which elements. This can lead to a situation like the one just illustrated, where a blue web part is displayed on a red team site, standing out unnecessarily. In most cases, you should strive to leverage the theme colors of the context site, so that your solution doesn't stand out but looks like a part of the site.</span></span>

<span data-ttu-id="6972c-p104">In SharePoint Framework können Sie anstelle der Verwendung von festen Farben auf Designfarben der Kontextwebsite verweisen. Wenn Ihr Webpart auf einer Website mit rotem Design platziert wird, wird folglich auch die rote Palette verwendet; wenn es auf einer Website mit dem blauen Design verwendet wird, wird es automatisch an die blaue Palette angepasst. All dies erfolgt automatisch, ohne dass Änderungen am Webpartcode vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="6972c-p104">Instead of using fixed colors, SharePoint Framework allows you to refer to theme colors of the context site. As a result, if your web part is placed on a site using red theme, it will use the red palette as well, and if it's placed on a site using the blue theme, it will automatically adjust itself to use the blue palette. All of this is done automatically without any changes to the web part code in between.</span></span>

## <a name="using-theme-colors-in-the-sharepoint-framework"></a><span data-ttu-id="6972c-116">Verwenden von Designfarben im SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="6972c-116">Using theme colors in the SharePoint Framework</span></span>

<span data-ttu-id="6972c-117">Wenn Sie mit festen Farben arbeiten, geben Sie diese in CSS-Eigenschaften an, z. B.:</span><span class="sxs-lookup"><span data-stu-id="6972c-117">When working with fixed colors, you specify them in CSS properties, for example:</span></span>

```css
.button {
    background-color: #0078d7;
}
```

<span data-ttu-id="6972c-118">Um stattdessen eine Designfarbe zu verwenden, ersetzen Sie die feste Farbe durch ein Designtoken:</span><span class="sxs-lookup"><span data-stu-id="6972c-118">To use a theme color instead, replace the fixed color with a theme token:</span></span>

```css
.button {
    background-color: "[theme: themePrimary, default: #0078d7]";
}
```

<span data-ttu-id="6972c-p105">Wenn Ihre SharePoint Framework-Anpassung auf der Seite geladen wird, sucht das Paket **@microsoft/load-themed-styles**, das Teil von SharePoint Framework ist, nach Designtoken in CSS-Dateien und versucht, diese durch die entsprechende Farbe aus dem aktuellen Design zu ersetzen. Wenn der Wert für das angegebene Token nicht verfügbar ist, verwendet SharePoint Framework stattdessen den mithilfe des **Standard**parameters angegebenen Wert, deshalb ist es so wichtig, dass Sie diesen immer einschließen.</span><span class="sxs-lookup"><span data-stu-id="6972c-p105">When your SharePoint Framework customization is loading on the page, the **@microsoft/load-themed-styles** package, which is a part of the SharePoint Framework, will look for theme tokens in CSS files and try to replace them with the corresponding color from the current theme. If the value for the specified token is not available, SharePoint Framework will use the value specified using the **default** parameter instead, which is why it's important that you always include it.</span></span>

<span data-ttu-id="6972c-121">Folgende Designtoken stehen für Sie zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="6972c-121">Following theme tokens are available for you to use:</span></span>

<span data-ttu-id="6972c-122">Token</span><span class="sxs-lookup"><span data-stu-id="6972c-122">Token</span></span>|<span data-ttu-id="6972c-123">Standardwert auf einer modernen Teamwebsite, auf der die rote Palette verwendet wird</span><span class="sxs-lookup"><span data-stu-id="6972c-123">Default value on a modern team site using the red palette</span></span>|<span data-ttu-id="6972c-124">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6972c-124">Remarks</span></span>
-----|--------------------------------|-----------
`backgroundImageUri`|`none`|
`themeAccent`|`#ee0410`|
`themeAccentTranslucent10`|`rgba(238, 4, 16, 0.10)`|
`themeDark`|`#b3030c`|<span data-ttu-id="6972c-125">Wird für Aktionssymbole in der Befehlsleiste und als Hoverfarbe verwendet</span><span class="sxs-lookup"><span data-stu-id="6972c-125">Used for action icons in the command bar and as hover color</span></span>
`themeDarkAlt`|`#b3030c`|
`themeDarker`|`#770208`|
`themeLight`|`#fd969b`|
`themeLightAlt`|`#fd969b`|
`themeLighter`|`#fecacd`|
`themeLighterAlt`|`#fecacd`|
`themePrimary`|`#ee0410`|<span data-ttu-id="6972c-p106">Primäre Designfarbe. Wird für Symbole und Standardschaltflächen verwendet.</span><span class="sxs-lookup"><span data-stu-id="6972c-p106">Primary theme color. Used for icons and default buttons</span></span>
`themeSecondary`|`#fc6169`|
`themeTertiary`|`#fd969b`|
`themeTertiaryAlt`|`#fd969b`|

> <span data-ttu-id="6972c-p107">**Hinweis:** Es gibt weitere Token, die in SharePoint Framework registriert sind. Alle diese Token weisen Werte auf, die in klassischen Websites angegeben sind, nur die zuvor erwähnte Untergruppe weist Werte für moderne SharePoint-Websites auf. Die vollständige Liste verfügbarer Token finden Sie im Wert der `window.__themeState__.theme`-Eigenschaft mithilfe der Konsole in den Entwicklertools Ihres Webbrowsers.</span><span class="sxs-lookup"><span data-stu-id="6972c-p107">**Note:** there are more tokens registered with the SharePoint Framework. While all of them have values specified on classic sites, only the subset mentioned earlier has values on modern SharePoint sites. For the complete list of available tokens, see the value of the `window.__themeState__.theme` property using the console in your web browser's developer tools.</span></span>

## <a name="use-theme-colors-in-your-customizations"></a><span data-ttu-id="6972c-131">Verwenden von Designfarben in Ihren Anpassungen</span><span class="sxs-lookup"><span data-stu-id="6972c-131">Use theme colors in your customizations</span></span>

<span data-ttu-id="6972c-p108">Wenn Sie ein Gerüst für ein neues clientseitiges SharePoint Framework-Webpart erstellen, wird standardmäßig die feste Palette für Blautöne verwendet. In den folgenden Schritten werden die Anpassungen beschrieben, die erforderlich sind, damit das Webpart stattdessen Designfarben verwendet.</span><span class="sxs-lookup"><span data-stu-id="6972c-p108">When you scaffold a new SharePoint Framework client-side web part, by default, it uses the fixed blue palette. Following steps describe the necessary adjustments to have the web part use theme colors instead.</span></span>

> <span data-ttu-id="6972c-p109">**Hinweis:** In den folgenden Schritten wird ein clientseitiges SharePoint Framework-Webpart mit dem Namen _HelloWorld_ mithilfe von React angewendet. Für Webparts, die mit anderen Bibliotheken und anderen Anpassungstypen erstellt wurden, müssen Sie die Änderungen möglicherweise entsprechend anpassen.</span><span class="sxs-lookup"><span data-stu-id="6972c-p109">**Note:** the following steps apply to a SharePoint Framework client-side web part named _HelloWorld_ built using React. For web parts built using different libraries and other types of customizations, you might need to adjust the modifications accordingly.</span></span>

<span data-ttu-id="6972c-136">Öffnen Sie im Code-Editor die Datei **./src/webparts/helloWorld/components/HelloWorld.tsx**, und entfernen Sie aus dem Div mit der Klasse **ms-Raster-Row** die Klasse **ms-BgColor-ThemeDark**Klasse.</span><span class="sxs-lookup"><span data-stu-id="6972c-136">In the code editor open the **./src/webparts/helloWorld/components/HelloWorld.tsx** file and from the div with class **ms-Grid-row** remove the **ms-bgColor-themeDark** class.</span></span>

![Die Klasse „ms-bgColor-themeDark“ ausgewählt im Visual Studio-Code-Editor](../images/themed-styles-ms-bgcolor-themedark-class.png)

<span data-ttu-id="6972c-p110">Öffnen Sie als Nächstes in demselben Ordner die Datei **HelloWorld.module.scss**. Ändern Sie den `.row`-Selektor folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="6972c-p110">Next, in the same folder, open the **HelloWorld.module.scss** file. Change the `.row` selector to:</span></span>

```css
.row {
    padding: 20px;
    background-color: "[theme: themeDark, default: #005a9e]";
}
```

![Der erweiterte .row-Selektor mit Hintergrundfarbe](../images/themed-styles-row-class.png)

<span data-ttu-id="6972c-141">Ändern Sie im `.button`-Selektor die Eigenschaften `background-color` und `border-color` folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="6972c-141">In the `.button` selector, change the `background-color` and `border-color` properties to:</span></span>

```css
.button {
    /* ... */
    background-color: "[theme: themePrimary, default: #0078d7]";
    border-color: "[theme: themePrimary, default: #0078d7]";
    /* ... */
}
```

![Der aktualisierte .button-Selektor mit Verweisen auf Designfarben](../images/themed-styles-button-class.png)

<span data-ttu-id="6972c-143">Wenn Sie das Webpart zu einer Website hinzufügen, werden die vom Webpart verwendeten Farben automatisch an die von der aktuellen Website verwendeten Designfarben angepasst.</span><span class="sxs-lookup"><span data-stu-id="6972c-143">When you add the web part to a site, the colors used by the web part will automatically adapt to the theme colors used by the current site.</span></span>

![Parallele Ansicht desselben Webparts, das in zwei Websites mit unterschiedlichen Farben angezeigt wird. Das Webpart folgt dem Farbschema der jeweiligen Website.](../images/themed-styles-side-by-side.png)

## <a name="more-information"></a><span data-ttu-id="6972c-146">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="6972c-146">More information</span></span>

* <span data-ttu-id="6972c-147">[How to use Theme Colors in SPFX Web Parts](http://www.n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/) von Stefan Bauer (Office Development MVP)</span><span class="sxs-lookup"><span data-stu-id="6972c-147">[How to use Theme Colors in SPFX Web Parts](http://www.n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/) by Stefan Bauer (Office Development MVP)</span></span>