---
title: Konfigurieren des Webpartsymbols
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 672f0cc67a47ff42756638798448f03085f36a9d
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="configure-web-part-icon"></a>Konfigurieren des Webpartsymbols

Die Verwendung eines Symbols, das den Zweck Ihres Webparts darstellt, erleichtert Benutzern die Suche nach Ihrem Webpart unter allen in der Toolbox verfügbaren Webparts. In diesem Artikel werden die verschiedenen Optionen erläutert, die beim Konfigurieren des Symbols für Ihre Webparts zur Verfügung stehen.

## <a name="preconfiguring-web-parts"></a>Vorkonfigurieren von Webparts

Das Webpartsymbol wird in dem Webpartmanifest im Rahmen der vorkonfigurierten Einträge definiert. Wenn Sie über ein Mehrfunktionswebpart verfügen, dass für verschiedene Anforderungen konfiguriert werden kann, kann jede Konfiguration ein anderes Symbol aufweisen, das den Zweck angibt. Ein repräsentatives Symbol erleichtert Benutzern die Suche nach dem gewünschten Webpart. Weitere Informationen zum Vorkonfigurieren von Webparts finden Sie in dem [Leitfaden zum Vorkonfigurieren von Webparts](../guidance/simplify-adding-web-parts-with-preconfigured-entries.md).

## <a name="configuring-web-part-icon"></a>Konfigurieren des Webpartsymbols

SharePoint-Framework bietet eine Reihe von Möglichkeiten zum Definieren des Symbols für das Webpart.

### <a name="using-office-ui-fabric-icon-font"></a>Verwenden von Office UI Fabric-Symbolschriftarten

Eine Möglichkeit, das Symbol für das Webpart zu definieren, ist die **officeFabricIconFontName**-Eigenschaft. Mit dieser Eigenschaft können Sie eines der im Rahmen von Office UI Fabric verfügbaren Symbole auswählen.

> Eine Liste der verfügbaren Symbole in Office UI Fabric finden Sie unter [https://developer.microsoft.com/de-de/fabric#/styles/icons](https://developer.microsoft.com/de-DE/fabric#/styles/icons).

Um ein bestimmtes Symbol zu verwenden, müssen Sie auf der Übersichtsseite mit Office UI Fabric-Symbolen seinen Namen kopieren und diesen als Wert in die **officeFabricIconFontName**-Eigenschaft im Manifest des Webparts einfügen.

![Pfeil, der auf den Symbolnamen auf der Übersichtsseite mit Office UI Fabric-Symbolen und auf den Manifestcode des Webparts zeigt](../../../images/webparticon_officeuifabricicon.png)

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "officeFabricIconFontName": "Sunny",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

Beim Hinzufügen des Webparts zur Seite wird das ausgewählte Symbol in der Toolbox angezeigt.

![Ausgewähltes Office UI Fabric-Symbol, das in der Toolbox für das Webpart angezeigt wird](../../../images/webparticon_toolbox_officeuifabricicon.png)

Der große Vorteil dieses Ansatzes ist, dass Sie keine Symbolbilddatei mit den Webpartressourcen bereitstellen müssen. Darüber hinaus wird das Symbol auf Computern mit anderen DPI- und Barrierefreiheitseinstellungen ohne Qualitätsverlust automatisch angepasst.

### <a name="using-an-external-icon-image"></a>Verwenden eines externen Symbolbilds

Obwohl Office UI Fabric zahlreiche Bilder bietet, möchten Sie möglicherweise beim Erstellen von Webparts ein für Ihre Organisation spezifisches Symbol verwenden, um Ihre Webparts deutlich von anderen, in der Toolbox verfügbaren Webparts von Erst- und Drittanbietern abzugrenzen.

Neben Office UI Fabric-Symbolen können im SharePoint-Framework auch Bilder verwendet werden. Um ein Bild als Webpartsymbol zu verwenden, müssen Sie die zugehörige eine absolute URL in der **iconImageUrl**-Eigenschaft im Manifest des Webparts angeben.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "iconImageUrl": "https://assets.contoso.com/weather.png",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

Das in der Toolbox angezeigte Webpartsymbolbild verfügt über eine Größe von 40x28 Pixel. Wenn das Bild größer ist, wird seine Größe proportional entsprechend dieser Größe angepasst.

![Ein in der Toolbox als Webpartsymbol verwendetes benutzerdefiniertes Bild](../../../images/webparticon_toolbox_imagepng.png)

Während Sie mit benutzerdefinierten Bildern von mehr Flexibilität bei der Wahl eines Symbols für Ihr Webpart profitieren, müssen Sie diese zusammen mit anderen Webpartressourcen bereitzustellen. Darüber hinaus kann es zum Qualitätsverlust kommen, wenn das Bild mit höheren DPI-Werten oder bestimmten Barrierefreiheitseinstellungen angezeigt wird. Um Qualitätsverlust zu vermeiden, können Sie Vektor-basierte SVG-Bilder verwenden, die auch von SharePoint-Framework unterstützt werden.

### <a name="using-a-base64-encoded-image"></a>Verwenden eines base64-codierten Bilds

Wenn Sie ein benutzerdefiniertes Bild verwenden, statt eine absolute URL zu der mit anderen Webpartressourcen gehosteten Bilddatei anzugeben, können Sie ein base64-codiertes Bild und die base64-Zeichenfolge anstelle der URL verwenden.

> Im Internet sind zahlreiche Dienste verfügbar, die Sie für die base64-Codierung von Bildern verwenden können, zum Beispiel [https://www.base64-image.de](https://www.base64-image.de).

Kopieren Sie nach dem Codieren des Bilds die base64-Zeichenfolge, und verwenden Sie sie als Wert für die **iconImageUrl**-Eigenschaft im Manifest des Webparts.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "iconImageUrl": "data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTAyMiIgaGVpZ2h0PSI5NzgiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiA8Zz4KICA8dGl0bGU+TGF5ZXIgMTwvdGl...",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

![Base64-codiertes Bild als Webpartsymbol in der Toolbox](../../../images/webparticon_toolbox_base64.png)

Base64-Codierung kann sowohl für BItmapbilder, zum Beispiel PNG, sowie für Vektor-basierte SVG-Bilder verwendet werden. Der große Vorteil der base64-Codierung von Bildern ist, dass Sie das Webpartsymbolbild nicht separat bereitstellen müssen.

## <a name="additional-considerations"></a>Zusätzliche Überlegungen

Jedes Webpart muss über ein Symbol verfügen. Wenn Sie das Webpartsymbol mit beiden **officeFabricIconFontName**- und den **iconImageUrl**-Eigenschaften angeben, wird das in der **officeFabricIconFontName**-Eigenschaft angegebene Symbol verwendet. Wenn Sie kein Office UI Fabric-Symbol verwenden möchten, müssen Sie eine URL in der **iconImageUrl**-Eigenschaft angeben.