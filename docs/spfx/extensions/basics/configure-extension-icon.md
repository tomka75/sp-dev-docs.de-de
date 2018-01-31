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
# <a name="configure-extension-icon"></a>Konfigurieren des Erweiterungssymbols

Die Verwendung eines Symbols, das den Zweck des benutzerdefinierten Befehls darstellt, in SharePoint-Framework erleichtert Benutzern die Suche nach Ihrem Befehl unter anderen Optionen, die in der Symbolleiste oder im Kontextmenü angezeigt werden. Das Angeben eines Symbols für einen Befehl ist optional. Wenn Sie kein Symbol angeben, wird nur der Befehlstitel in der Befehlsleiste angezeigt.

SharePoint-Framework unterstützt die folgenden Erweiterungstypen:

- Application Customizer
- Field Customizer
- Befehlssatz

Der Befehlssatz ist der einzige SharePoint-Framework-Erweiterungstyp, in dem Symbole konfiguriert werden können.

Wenn Sie Befehlssätze bereitstellen, können Sie festlegen, wo die Befehle angezeigt werden sollen:

- Auf der Befehlsleiste (`location: ClientSideExtension.ListViewCommandSet.CommandBar`)

- Im Kontextmenü (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`)

- Oder beides (`location: ClientSideExtension.ListViewCommandSet`)

Symbole, die für andere Befehle definiert werden, werden nur für Befehle auf der Befehlsleiste angezeigt.

SharePoint-Framework bietet zwei Möglichkeiten zum Definieren des Symbols für Ihre Erweiterung:

- Verwenden eines externen Symbolbilds
- Verwenden eines base64-codierten Bilds

## <a name="use-an-external-icon-image"></a>Verwenden eines externen Symbolbilds

Beim Erstellen von Befehlssätzen des SharePoint-Framework können Sie für jeden Befehl ein Symbol angeben, indem Sie in der **iconImageUrl**-Eigenschaft eine absolute URL angeben, die auf das Symbolbild im Erweiterungsmanifest verweist.

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

Das auf der Befehlsleiste angezeigte Befehlssymbol weist eine Größe von 16 x 16 Pixel auf. Wenn das Bild größer ist, wird seine Größe proportional entsprechend dieser Größe angepasst.

![Auf der Befehlsleiste als Befehlssymbol verwendetes benutzerdefiniertes Bild](../../../images/extensionicon_commandbar_imagepng.png)

<br/>

Während Sie mit benutzerdefinierten Bildern von mehr Flexibilität bei der Wahl eines Symbols für Ihren Befehl profitieren, müssen Sie diese zusammen mit anderen Erweiterungsressourcen bereitzustellen. Darüber hinaus kann es zum Qualitätsverlust kommen, wenn das Bild mit höheren DPI-Werten oder bestimmten Barrierefreiheitseinstellungen angezeigt wird. Um Qualitätsverlust zu vermeiden, können Sie Vektor-basierte SVG-Bilder verwenden, die auch von SharePoint-Framework unterstützt werden.

## <a name="use-a-base64-encoded-image"></a>Verwenden eines base64-codierten Bilds

Wenn Sie ein benutzerdefiniertes Bild verwenden, statt eine absolute URL zu der mit anderen Erweiterungsressourcen gehosteten Bilddatei anzugeben, können Sie ein base64-codiertes Bild und die base64-Zeichenfolge anstelle der URL verwenden.

Online steht eine Reihe von Diensten zur Verfügung, die Sie zum Codieren Ihres Bilds mit base64 verwenden können, zum Beispiel [Konvertieren Ihrer Bilder mit Base64](https://www.base64-image.de).

Kopieren Sie nach dem Codieren des Bilds die base64-Zeichenfolge, und verwenden Sie sie als Wert für die **iconImageUrl**-Eigenschaft im Manifest des Webparts.

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

Base64-Codierung kann sowohl für Bitmapbilder, zum Beispiel PNG, als auch für Vektor-basierte SVG-Bilder verwendet werden. Der große Vorteil der base64-Codierung von Bildern ist, dass Sie das Webpart-Symbolbild nicht separat bereitstellen müssen.

![Base64-codiertes Bild als Webpartsymbol in der Toolbox](../../../images/extensionicon_commandbar_base64.png)

## <a name="see-also"></a>Siehe auch

- [Übersicht über SharePoint-Framework-Erweiterungen](../overview-extensions.md)