---
title: Integrieren von Webparteigenschaften in SharePoint
description: Verwenden Sie Funktionen, die die Verwaltung von Webparteigenschaftswerten vereinfachen, und integrieren Sie diese bei der Erstellung von clientseitigen SharePoint-Framework-Webparts mit der SharePoint-Suche.
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: 17beb9335654f7f5a35209005b101e5fca287d4c
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="integrate-web-part-properties-with-sharepoint"></a>Integrieren von Webparteigenschaften in SharePoint

Wenn Sie klassische Webparts erstellen, werden Webparteigenschaften aus SharePoint isoliert und deren Werte von Endbenutzern verwaltet. SharePoint-Framework bietet neue Funktionen, die die Verwaltung von Webparteigenschaftswerten vereinfachen und diese in die SharePoint-Suche integrieren. In diesem Artikel wird erläutert, wie Sie diese Funktionen beim Erstellen von clientseitigen SharePoint-Framework-Webparts verwenden können.

> [!IMPORTANT] 
> Der folgende Leitfaden gilt nur für clientseitige SharePoint-Framework-Webparts, die auf modernen SharePoint-Seiten platziert werden. Die in diesem Artikel beschriebenen Funktionen gelten nicht für klassische Webparts oder clientseitige SharePoint-Framework-Webparts, die auf klassischen Seiten platziert werden.

## <a name="client-side-web-part-properties"></a>Eigenschaften von clientseitigen Webparts

Wenn Sie clientseitige SharePoint Framework-Webparts erstellen, können Sie Eigenschaften definieren, die von Benutzern konfiguriert werden können. Durch Verwendung von Eigenschaften anstelle von festen Werte werden Webparts flexibler und eignen sich für viele unterschiedliche Szenarios.

Im Vergleich zu klassischen Webparts gibt es einige Unterschiede hinsichtlich der Verarbeitung von Webparteigenschaften mit dem SharePoint-Framework. Das folgende Schema veranschaulicht, wie Webpart-Eigenschaftswerte die verschiedenen Ebenen von SharePoint durchlaufen.

![Schema, in dem veranschaulicht wird, wie das SharePoint-Framework Webparteigenschaften behandelt](../../../images/integrate-webpart-properties-schema.png)

<br/>

Bevor Sie Werte für Webparteigenschaften von Endbenutzern annehmen, sollten Sie diese immer [überprüfen](./validate-web-part-property-values.md). Auf diese Weise können Sie nicht nur sicherstellen, dass Ihre Webparts benutzerfreundlich sind, sondern auch verhindern, dass ungültige Daten in der Webpartkonfiguration gespeichert werden. 

Darüber hinaus sollten Sie berücksichtigen, dass das SharePoint-Framework keine Anpassung unterstützt und alle Benutzer die gleiche Konfiguration des entsprechenden Webparts sehen.

## <a name="specify-web-part-property-value-type"></a>Angeben des Typs von Webpart-Eigenschaftswerten

In klassischen SharePoint-Webparts waren Werte von Webpart-Eigenschaftswerten von SharePoint isoliert. Wenn Sie eine Webparteigenschaft mit einer URL einer Datei in SharePoint gespeichert hatten, mussten Sie manuell sicherstellen, dass diese URL gültig war und auf ein korrektes Dokument verwies, falls es verschoben oder umbenannt wurde. Wenn Benutzer Text eingeben konnten, der im Webpart angezeigt wurde, wurde dieser Text von der SharePoint-Suche auch nicht indiziert.

Wenn Sie Webparts erstellen, können Sie mit SharePoint-Framework bestimmen, welche Art von Wert die jeweilige Webparteigenschaft enthalten soll. Diese Konfiguration bestimmt, wie SharePoint den Wert verarbeitet. Abhängig von der angegebenen Konfiguration kann SharePoint den Wert der jeweiligen Eigenschaft im Suchindex enthalten, unsichere HTML-Inhalte entfernen und sogar Links zu Dokumenten in SharePoint auf dem neuesten Stand speichern, falls eine Datei verschoben oder umbenannt wird.

Um die Konfiguration für Ihre Webparteigenschaften anzugeben, setzen Sie in der Webpartklasse den **propertiesMetadata**-Getter außer Kraft:

```typescript
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  IWebPartPropertiesMetadata
} from '@microsoft/sp-webpart-base';

// ...

export default class ArticleLinkWebPart extends BaseClientSideWebPart<IArticleLinkWebPartProps> {
  // ...
  protected get propertiesMetadata(): IWebPartPropertiesMetadata {
    return {
      'title': { isSearchablePlainText: true },
      'intro': { isHtmlString: true },
      'image': { isImageSource: true },
      'url': { isLink: true }
    };
  }
  // ...
}
```

Die **PropertiesMetadata**-Methode gibt ein Objekt zurück, in dem die Eigenschaft eine Zeichenfolge ist, und gibt den Namen der Webparteigenschaft an, und der Wert ist ein Objekt, das angibt, wie SharePoint die jeweilige Eigenschaft behandeln soll. 

Wenn Sie die **PropertiesMetadata**-Methode überschreiben, müssen Sie nicht alle Webparteigenschaften auflisten. Standardmäßig werden die Werte der Webparteigenschaften nicht von SharePoint verarbeitet, und Sie sollten nur diejenigen Eigenschaften einschließen, die verarbeitet werden sollen.

Nachfolgend finden Sie eine Liste möglicher Werte, die in den Metadaten der Eigenschaften festgelegt werden können, sowie deren Auswirkungen darauf, wie der Wert der Webparteigenschaft von SharePoint verarbeitet wird.

<br/>

Metadatenwert|Durchsuchbar|Linkkorrektur|Unsichere HTM entfernen
--------------|:--------:|:--------:|:----------------:
Keine (Standard)|nein|nein|nein
`isSearchablePlainText`|ja|nein|nein
`isHtmlString`|ja|ja|ja
`isImageSource`|ja|ja|nein
`isLink`|ja|ja|nein

<br/>

> [!IMPORTANT] 
> Wenn Sie die Konfiguration für Ihre Webparteigenschaften definieren, sollten Sie jeweils nur eine der in der Tabelle aufgeführten Eigenschaften für jede Webparteigenschaft verwenden. Das Festlegen mehrerer Eigenschaften wird wahrscheinlich zu unerwünschten Ergebnissen führen und sollte daher vermieden werden.

Standardmäßig wird der Wert einer Webparteigenschaft nicht von der SharePoint-Suche indiziert und in keiner Weise von SharePoint verarbeitet. Er wird genau so an das Webpart übergeben, wie er vom Benutzer eingegeben wurde, der das Webpart konfiguriert.

Wenn Sie die Webparteigenschaft als `isSearchablePlainText` angeben, wird sie in den Index für die Volltextsuche integriert. Wenn Benutzer nach beliebigen, im Wert dieser Eigenschaft inbegriffenen Schlüsselwörtern suchen, gibt die SharePoint-Suche die Seite mit dem Webpart in den Suchergebnissen zurück. Wenn der Wert einen Link zu einem in SharePoint gespeicherten Dokument enthält, wird dieser Link nicht aktualisiert, wenn das Dokument, auf das verwiesen wird, verschoben oder umbenannt wird. Darüber hinaus bleibt jeglicher vom Benutzer eingegebener HTML-Code erhalten. Wenn Sie mit dem Wert einer solchen Eigenschaft arbeiten, sollten Sie diesen als Nur-Text- und escape-HTML-Code behandeln, der vor dem Rendern auf der Seite von Benutzern eingegeben werden kann, um Skripteinschleusung zu vermeiden.

Wenn eine Webparteigenschaft als `isHtmlString` definiert ist, entfernt SharePoint zuerst alle unsicheren HTML-Elemente, wie z. B. `script`-Tags, aus dem Eigenschaftswert. Der verbleibende HTML-Code kann für das Rendering auf einer Seite als sicher eingestuft werden. Wenn der Wert URLs enthält, die auf in SharePoint gespeicherte Dateien hinweisen, aktualisiert SharePoint automatisch die in die Eigenschaft des Webparts gespeicherte URL, sobald eine der Dateien umbenannt oder verschoben wird. Dies erleichtert das Verwalten von URLs für alle Webparts und Seiten in Ihrem Mandanten erheblich. HTML-Webparteigenschaften können auch durchsucht werden, sodass Benutzer nach allen im Eigenschaftswert enthaltenen Schlüsselwörtern suchen können.

Die Eigenschaftswerttypen `isImageSource` und `isLink` sind für die Verwendung mit Webparteigenschaften gedacht, die nur einen Link zu einem Bild oder einer in SharePoint gespeicherten Datei enthalten. In beiden Fällen schließt die SharePoint-Suche den Inhalt in den Volltext-Index ein und hält die angegebene URL auf dem neuesten Stand, falls die Datei, auf die verwiesen wird, umbenannt oder verschoben wird. Darüber hinaus durchlaufen Bildquellen möglicherweise eine zusätzliche Verarbeitung, damit Bilder schneller herunterladen werden können. Wenn eine Seite ein Titelbild enthält und dieses Bild zu den ersten fünf Bildern der Seite gehört oder sich in den ersten beiden Zeilen auf der Seite befindet, wird das Bild vorab geladen.
