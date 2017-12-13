---
title: Konfigurieren des Erweiterungssymbols
ms.date: 11/20/2017
ms.prod: sharepoint
ms.openlocfilehash: d20f2317e160fa46b0b48902cc9bc40970173470
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="configure-extension-icon"></a><span data-ttu-id="7d326-102">Konfigurieren des Erweiterungssymbols</span><span class="sxs-lookup"><span data-stu-id="7d326-102">Configure extension icon</span></span>

<span data-ttu-id="7d326-103">Die Verwendung eines Symbols, das den Zweck des benutzerdefinierten Befehls darstellt, erleichtert Benutzern die Suche nach Ihrem Befehl unter anderen Optionen, die in der Symbolleiste oder im Kontextmenü angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="7d326-103">Selecting an icon that illustrates the purpose of your custom command, makes it easier for users to find your command among other options visible in the toolbar or in the context menu.</span></span> <span data-ttu-id="7d326-104">In diesem Artikel werden die verschiedenen Optionen erläutert, die beim Konfigurieren des Symbols für Ihre Befehle zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="7d326-104">This article explains the different options available to you to configure the icon for your commands.</span></span>

## <a name="extension-types-that-support-icons"></a><span data-ttu-id="7d326-105">Erweiterungstypen, die Symbole unterstützen</span><span class="sxs-lookup"><span data-stu-id="7d326-105">Extension types that support icons</span></span>

<span data-ttu-id="7d326-106">SharePoint-Framework unterstützt die folgenden Erweiterungstypen:</span><span class="sxs-lookup"><span data-stu-id="7d326-106">SharePoint Framework supports building the following types of extensions:</span></span>

- <span data-ttu-id="7d326-107">Application Customizer</span><span class="sxs-lookup"><span data-stu-id="7d326-107">Application customizer</span></span>
- <span data-ttu-id="7d326-108">Field Customizer</span><span class="sxs-lookup"><span data-stu-id="7d326-108">Field Customizer</span></span>
- <span data-ttu-id="7d326-109">Befehlssatz</span><span class="sxs-lookup"><span data-stu-id="7d326-109">Command set</span></span>

<span data-ttu-id="7d326-110">Befehlssatz ist der einzige SharePoint-Framework-Erweiterungstyp, in dem Symbole konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="7d326-110">Command set is the only type of SharePoint Framework extension for which you can configure icons.</span></span>

## <a name="defining-command-set-locations"></a><span data-ttu-id="7d326-111">Definieren der Position des Befehlssatzes</span><span class="sxs-lookup"><span data-stu-id="7d326-111">Defining Command set locations</span></span>

<span data-ttu-id="7d326-112">Wenn Sie Befehlssätze bereitstellen, können Sie festlegen, ob die Befehle auf der Befehlsleiste (`location: ClientSideExtension.ListViewCommandSet.CommandBar`), im Kontextmenü (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`) oder sowohl auf der Befehlsleiste als auch im Kontextmenü (`location: ClientSideExtension.ListViewCommandSet`) angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7d326-112">When deploying command sets, you can choose whether their commands should be visible on the command bar (`location: ClientSideExtension.ListViewCommandSet.CommandBar`), in the context menu (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`) or both (`location: ClientSideExtension.ListViewCommandSet`).</span></span> <span data-ttu-id="7d326-113">Symbole, die für andere Befehle definiert werden, werden nur für Befehle auf der Befehlsleiste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7d326-113">Icons defined for the different commands will be displayed only for commands displayed in the command bar.</span></span>

## <a name="configuring-command-set-icons"></a><span data-ttu-id="7d326-114">Konfigurieren von Symbolen für Befehlssätze</span><span class="sxs-lookup"><span data-stu-id="7d326-114">Configuring command set icons</span></span>

<span data-ttu-id="7d326-115">SharePoint-Framework bietet zwei Möglichkeiten zum Definieren des Symbols für Ihre Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="7d326-115">SharePoint Framework offers you two ways to define the icon for your extension.</span></span>

### <a name="using-an-external-icon-image"></a><span data-ttu-id="7d326-116">Verwenden eines externen Symbolbilds</span><span class="sxs-lookup"><span data-stu-id="7d326-116">Using an external icon image</span></span>

<span data-ttu-id="7d326-117">Beim Erstellen von Befehlssätzen des SharePoint-Framework können Sie für jeden Befehl ein Symbol angeben, indem Sie in der **iconImageUrl**-Eigenschaft eine absolute URL angeben, die auf das Symbolbild im Erweiterungsmanifest verweist.</span><span class="sxs-lookup"><span data-stu-id="7d326-117">When building SharePoint Framework command sets, you can specify an icon for each command by providing an absolute URL pointing to the icon image in the extension manifest, in the **iconImageUrl** property.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/command-set-extension-manifest.schema.json",

  "id": "6cdfbff6-714f-4c26-a60c-0b18afe60837",
  "alias": "WeatherCommandSet",
  "componentType": "Extension",
  "extensionType": "ListViewCommandSet",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "items": {
    "WEATHER": {
      "title": { "default": "Weather" },
      "iconImageUrl": "https://localhost:4321/temp/sun.png",
      "type": "command"
    }
  }
}
```

<span data-ttu-id="7d326-118">Das auf der Befehlsleiste angezeigte Befehlssymbol weist eine Größe von 16 x 16 Pixel auf.</span><span class="sxs-lookup"><span data-stu-id="7d326-118">The command icon displayed in the command bar is 16x16px.</span></span> <span data-ttu-id="7d326-119">Wenn das Bild größer ist, wird seine Größe proportional entsprechend dieser Größe angepasst.</span><span class="sxs-lookup"><span data-stu-id="7d326-119">If your image is bigger, it will be sized proportionally to match these dimensions.</span></span>

![Das auf der Befehlsleiste als Befehlssymbol verwendetes benutzerdefiniertes Bild](../../../images/extensionicon_commandbar_imagepng.png)

<span data-ttu-id="7d326-121">Während Sie mit benutzerdefinierten Bildern von mehr Flexibilität bei der Wahl eines Symbols für Ihren Befehl profitieren, müssen Sie diese zusammen mit anderen Erweiterungsressourcen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="7d326-121">While using custom images gives you flexibility to choose an icon for your command, it requires you to deploy them along with your other extension assets.</span></span> <span data-ttu-id="7d326-122">Darüber hinaus kann es zum Qualitätsverlust kommen, wenn das Bild mit höheren DPI-Werten oder bestimmten Barrierefreiheitseinstellungen angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7d326-122">Additionally, your image might lose quality when displayed in higher DPI or specific accessibility settings.</span></span> <span data-ttu-id="7d326-123">Um Qualitätsverlust zu vermeiden, können Sie Vektor-basierte SVG-Bilder verwenden, die auch von SharePoint-Framework unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="7d326-123">To avoid quality loss, you can use vector-based SVG images which are also supported by the SharePoint Framework.</span></span>

### <a name="using-a-base64-encoded-image"></a><span data-ttu-id="7d326-124">Verwenden eines base64-codierten Bilds</span><span class="sxs-lookup"><span data-stu-id="7d326-124">Using a base64 encoded image</span></span>

<span data-ttu-id="7d326-125">Wenn Sie ein benutzerdefiniertes Bild verwenden, statt eine absolute URL zu der mit anderen Erweiterungsressourcen gehosteten Bilddatei anzugeben, können Sie ein base64-codiertes Bild und die base64-Zeichenfolge anstelle der URL verwenden.</span><span class="sxs-lookup"><span data-stu-id="7d326-125">When using a custom image, rather than specifying an absolute URL to the image file hosted together with other extension assets, you can have your image base64 encoded and use the base64 string instead of the URL.</span></span>

> <span data-ttu-id="7d326-126">Im Internet sind zahlreiche Dienste verfügbar, die Sie für die base64-Codierung von Bildern verwenden können, zum Beispiel [https://www.base64-image.de](https://www.base64-image.de).</span><span class="sxs-lookup"><span data-stu-id="7d326-126">There are a number of services available on the Internet that you can use to base64 encode your image, such as [https://www.base64-image.de](https://www.base64-image.de).</span></span>

<span data-ttu-id="7d326-127">Kopieren Sie nach dem Codieren des Bilds die base64-Zeichenfolge, und verwenden Sie sie als Wert für die **iconImageUrl**-Eigenschaft im Manifest des Webparts.</span><span class="sxs-lookup"><span data-stu-id="7d326-127">After encoding the image, copy the base64 string and use it as the value for the **iconImageUrl** property in the web part manifest.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/command-set-extension-manifest.schema.json",

  "id": "6cdfbff6-714f-4c26-a60c-0b18afe60837",
  "alias": "WeatherCommandSet",
  "componentType": "Extension",
  "extensionType": "ListViewCommandSet",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "items": {
    "WEATHER": {
      "title": { "default": "Weather" },
      "iconImageUrl": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQAAAAEACAYAAABccqhmAAAAAXNSR0IB2cksfwAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAB/hUlEQVR42u29ebwkWVUn/j03Ipe31PZqr+ruqu7q6pXuZlcRRgUVBRnUn0rpMAJuTDeLog4u48bMiDoMtCA0MjAwOqil4oI6qCO2oIiDTQ...",
      "type": "command"
    }
  }
}
```

![Base64-codiertes Bild als Webpartsymbol in der Toolbox](../../../images/extensionicon_commandbar_base64.png)

<span data-ttu-id="7d326-129">Base64-Codierung kann sowohl für BItmapbilder, zum Beispiel PNG, sowie für Vektor-basierte SVG-Bilder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7d326-129">Base64 encoding works both for bitmap images such as PNG as well as vector SVG images.</span></span> <span data-ttu-id="7d326-130">Der große Vorteil der base64-Codierung von Bildern ist, dass Sie das Webpartsymbolbild nicht separat bereitstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="7d326-130">The big benefit of using base64 encoded images is, that you don't need to deploy the web part icon image separately.</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="7d326-131">Zusätzliche Überlegungen</span><span class="sxs-lookup"><span data-stu-id="7d326-131">Additional considerations</span></span>

<span data-ttu-id="7d326-132">Das Angeben eines Symbols für einen Befehl ist optional.</span><span class="sxs-lookup"><span data-stu-id="7d326-132">Specifying an icon for a command is optional.</span></span> <span data-ttu-id="7d326-133">Wenn Sie kein Symbol angeben, wird nur der Befehlstitel auf der Befehlsleiste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7d326-133">If you don't specify an icon, then only the command title will be displayed in the command bar.</span></span>