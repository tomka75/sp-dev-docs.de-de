---
title: Konfigurieren des Erweiterungssymbols in SharePoint-Framework (SPFx)-Erweiterungen
description: "Optionen zum Konfigurieren des Symbols für die Befehle in SharePoint-Framework (SPFx)-Erweiterungen."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 1dcbef078f8985de00614f8ebfbf3dd1030439d6
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="configure-extension-icon"></a><span data-ttu-id="786e6-103">Konfigurieren des Erweiterungssymbols</span><span class="sxs-lookup"><span data-stu-id="786e6-103">Configure extension icon</span></span>

<span data-ttu-id="786e6-104">Die Verwendung eines Symbols, das den Zweck des benutzerdefinierten Befehls darstellt, in SharePoint-Framework erleichtert Benutzern die Suche nach Ihrem Befehl unter anderen Optionen, die in der Symbolleiste oder im Kontextmenü angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="786e6-104">Selecting an icon that illustrates the purpose of your custom command, makes it easier for users to find your command among other options visible in the toolbar or in the context menu.</span></span> <span data-ttu-id="786e6-105">Das Angeben eines Symbols für einen Befehl ist optional.</span><span class="sxs-lookup"><span data-stu-id="786e6-105">Specifying an icon for a command is optional.</span></span> <span data-ttu-id="786e6-106">Wenn Sie kein Symbol angeben, wird nur der Befehlstitel in der Befehlsleiste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="786e6-106">If you don't specify an icon, then only the command title will be displayed in the command bar.</span></span>

<span data-ttu-id="786e6-107">SharePoint-Framework unterstützt die folgenden Erweiterungstypen:</span><span class="sxs-lookup"><span data-stu-id="786e6-107">SharePoint Framework supports building the following types of extensions:</span></span>

- <span data-ttu-id="786e6-108">Application Customizer</span><span class="sxs-lookup"><span data-stu-id="786e6-108">Application customizer</span></span>
- <span data-ttu-id="786e6-109">Field Customizer</span><span class="sxs-lookup"><span data-stu-id="786e6-109">Field Customizer</span></span>
- <span data-ttu-id="786e6-110">Befehlssatz</span><span class="sxs-lookup"><span data-stu-id="786e6-110">Command set</span></span>

<span data-ttu-id="786e6-111">Der Befehlssatz ist der einzige SharePoint-Framework-Erweiterungstyp, in dem Symbole konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="786e6-111">Command set is the only type of SharePoint Framework extension for which you can configure icons.</span></span>

<span data-ttu-id="786e6-112">Wenn Sie Befehlssätze bereitstellen, können Sie festlegen, wo die Befehle angezeigt werden sollen:</span><span class="sxs-lookup"><span data-stu-id="786e6-112">When deploying Command Sets, you can choose whether their commands should be visible on:</span></span>

- <span data-ttu-id="786e6-113">Auf der Befehlsleiste (`location: ClientSideExtension.ListViewCommandSet.CommandBar`)</span><span class="sxs-lookup"><span data-stu-id="786e6-113">The command bar (`location: ClientSideExtension.ListViewCommandSet.CommandBar`)</span></span>

- <span data-ttu-id="786e6-114">Im Kontextmenü (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`)</span><span class="sxs-lookup"><span data-stu-id="786e6-114">The context menu (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`)</span></span>

- <span data-ttu-id="786e6-115">Oder beides (`location: ClientSideExtension.ListViewCommandSet`)</span><span class="sxs-lookup"><span data-stu-id="786e6-115">Both (`location: ClientSideExtension.ListViewCommandSet`)</span></span>

<span data-ttu-id="786e6-116">Symbole, die für andere Befehle definiert werden, werden nur für Befehle auf der Befehlsleiste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="786e6-116">Icons defined for the different commands will be displayed only for commands displayed in the command bar.</span></span>

<span data-ttu-id="786e6-117">SharePoint-Framework bietet zwei Möglichkeiten zum Definieren des Symbols für Ihre Erweiterung:</span><span class="sxs-lookup"><span data-stu-id="786e6-117">SharePoint Framework offers you two ways to define the icon for your extension.</span></span>

- <span data-ttu-id="786e6-118">Verwenden eines externen Symbolbilds</span><span class="sxs-lookup"><span data-stu-id="786e6-118">Using an external icon image</span></span>
- <span data-ttu-id="786e6-119">Verwenden eines base64-codierten Bilds</span><span class="sxs-lookup"><span data-stu-id="786e6-119">Use a base64-encoded image</span></span>

## <a name="use-an-external-icon-image"></a><span data-ttu-id="786e6-120">Verwenden eines externen Symbolbilds</span><span class="sxs-lookup"><span data-stu-id="786e6-120">Using an external icon image</span></span>

<span data-ttu-id="786e6-121">Beim Erstellen von Befehlssätzen des SharePoint-Framework können Sie für jeden Befehl ein Symbol angeben, indem Sie in der **iconImageUrl**-Eigenschaft eine absolute URL angeben, die auf das Symbolbild im Erweiterungsmanifest verweist.</span><span class="sxs-lookup"><span data-stu-id="786e6-121">When building SharePoint Framework command sets, you can specify an icon for each command by providing an absolute URL pointing to the icon image in the extension manifest, in the **iconImageUrl** property.</span></span>

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

<br/>

<span data-ttu-id="786e6-122">Das auf der Befehlsleiste angezeigte Befehlssymbol weist eine Größe von 16 x 16 Pixel auf.</span><span class="sxs-lookup"><span data-stu-id="786e6-122">The command icon displayed in the command bar is 16x16px.</span></span> <span data-ttu-id="786e6-123">Wenn das Bild größer ist, wird seine Größe proportional entsprechend dieser Größe angepasst.</span><span class="sxs-lookup"><span data-stu-id="786e6-123">If your image is bigger, it will be sized proportionally to match these dimensions.</span></span>

![Auf der Befehlsleiste als Befehlssymbol verwendetes benutzerdefiniertes Bild](../../../images/extensionicon_commandbar_imagepng.png)

<br/>

<span data-ttu-id="786e6-125">Während Sie mit benutzerdefinierten Bildern von mehr Flexibilität bei der Wahl eines Symbols für Ihren Befehl profitieren, müssen Sie diese zusammen mit anderen Erweiterungsressourcen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="786e6-125">While using custom images gives you flexibility to choose an icon for your command, it requires you to deploy them along with your other extension assets.</span></span> <span data-ttu-id="786e6-126">Darüber hinaus kann es zum Qualitätsverlust kommen, wenn das Bild mit höheren DPI-Werten oder bestimmten Barrierefreiheitseinstellungen angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="786e6-126">Additionally, your image might lose quality when displayed in higher DPI or specific accessibility settings.</span></span> <span data-ttu-id="786e6-127">Um Qualitätsverlust zu vermeiden, können Sie Vektor-basierte SVG-Bilder verwenden, die auch von SharePoint-Framework unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="786e6-127">To avoid quality loss, you can use vector-based SVG images which are also supported by the SharePoint Framework.</span></span>

## <a name="use-a-base64-encoded-image"></a><span data-ttu-id="786e6-128">Verwenden eines base64-codierten Bilds</span><span class="sxs-lookup"><span data-stu-id="786e6-128">Use a base64-encoded image</span></span>

<span data-ttu-id="786e6-129">Wenn Sie ein benutzerdefiniertes Bild verwenden, statt eine absolute URL zu der mit anderen Erweiterungsressourcen gehosteten Bilddatei anzugeben, können Sie ein base64-codiertes Bild und die base64-Zeichenfolge anstelle der URL verwenden.</span><span class="sxs-lookup"><span data-stu-id="786e6-129">When using a custom image, rather than specifying an absolute URL to the image file hosted together with other extension assets, you can have your image base64 encoded and use the base64 string instead of the URL.</span></span>

<span data-ttu-id="786e6-130">Online steht eine Reihe von Diensten zur Verfügung, die Sie zum Codieren Ihres Bilds mit base64 verwenden können, zum Beispiel [Konvertieren Ihrer Bilder mit Base64](https://www.base64-image.de).</span><span class="sxs-lookup"><span data-stu-id="786e6-130">A number of services are available online that you can use to base64-encode your image, such as [Convert your images to Base64](https://www.base64-image.de).</span></span>

<span data-ttu-id="786e6-131">Kopieren Sie nach dem Codieren des Bilds die base64-Zeichenfolge, und verwenden Sie sie als Wert für die **iconImageUrl**-Eigenschaft im Manifest des Webparts.</span><span class="sxs-lookup"><span data-stu-id="786e6-131">After encoding the image, copy the base64 string and use it as the value for the **iconImageUrl** property in the web part manifest.</span></span>

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

<br/>

<span data-ttu-id="786e6-132">Base64-Codierung kann sowohl für Bitmapbilder, zum Beispiel PNG, als auch für Vektor-basierte SVG-Bilder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="786e6-132">Base64 encoding works both for bitmap images such as PNG as well as vector SVG images.</span></span> <span data-ttu-id="786e6-133">Der große Vorteil der base64-Codierung von Bildern ist, dass Sie das Webpart-Symbolbild nicht separat bereitstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="786e6-133">The big benefit of using base64 encoded images is, that you don't need to deploy the web part icon image separately.</span></span>

![Base64-codiertes Bild als Webpartsymbol in der Toolbox](../../../images/extensionicon_commandbar_base64.png)

## <a name="see-also"></a><span data-ttu-id="786e6-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="786e6-135">See also</span></span>

- [<span data-ttu-id="786e6-136">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="786e6-136">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)