# <a name="integrate-web-part-properties-with-sharepoint"></a>Integrieren von Webparteigenschaften in SharePoint

Beim Erstellen von klassischen Webparts waren Webparteigenschaften von SharePoint isoliert und ihre Werte wurden von Endbenutzern verwaltet. SharePoint Framework bietet Ihnen einen neuen Satz von Funktionen, die die Verwaltung der Werte von Webparteigenschaften vereinfachen und diese in die SharePoint-Suche integrieren. In diesem Artikel wird erläutert, wie Sie diese Funktionen beim Erstellen von clientseitigen SharePoint Framework-Webparts verwenden können.

> **Wichtig:** Der folgende Leitfaden gilt nur für clientseitige SharePoint Framework-Webparts, die auf modernen SharePoint-Seiten platziert werden. In diesem Artikel beschriebene Funktionen gelten nicht für klassische Webparts oder clientseitige SharePoint Framework-Webparts auf klassischen Seiten.

## <a name="client-side-web-part-properties"></a>Eigenschaften von clientseitigen Webparts

Wenn Sie clientseitige SharePoint Framework-Webparts erstellen, können Sie Eigenschaften definieren, die von Benutzern konfiguriert werden können. Durch Verwendung von Eigenschaften anstelle von festen Werte werden Webparts flexibler und eignen sich für viele unterschiedliche Szenarios.

Im Vergleich zu klassischen Webparts gibt es einige Unterschiede dahingehend, wie das SharePoint Framework Webparteigenschaften behandelt. Im folgenden Schema wird veranschaulicht, wie Werte von Webparteigenschaften durch die unterschiedlichen Ebenen von SharePoint fließen.

![Schema, in dem veranschaulicht wird, wie das SharePoint Framework Webparteigenschaften behandelt](../../../../images/integrate-webpart-properties-schema.png)

Bevor Werte für Webparteigenschaften von Endbenutzern akzeptiert werden, sollten Sie diese immer [überprüfen](./validate-web-part-property-values). Auf diese Weise können Sie nicht nur sicherstellen, dass Ihre Webparts benutzerfreundlich sind, Sie können auch verhindern, dass ungültige Daten in der Webpartkonfiguration gespeichert werden. Außerdem sollten Sie berücksichtigen, dass das SharePoint Framework keine Personalisierung unterstützt und alle Benutzer dieselbe Konfiguration des jeweiligen Webparts sehen.

## <a name="specify-web-part-property-value-type"></a>Angeben des Typs von Webpart-Eigenschaftswerten

In klassischen SharePoint-Webparts waren Werte von Webpart-Eigenschaftswerten von SharePoint isoliert. Wenn Sie eine Webparteigenschaft mit einer URL einer Datei in SharePoint gespeichert hatten, mussten Sie manuell sicherstellen, dass diese URL gültig war und auf ein korrektes Dokument verwies, falls es verschoben oder umbenannt wurde. Wenn Benutzer Text eingeben konnten, der im Webpart angezeigt wurde, wurde dieser Text von der SharePoint-Suche auch nicht indiziert.

Beim Erstellen von Webparts können Sie in SharePoint Framework angeben, welche Art von Wert die jeweilige Webparteigenschaft verwendet. Diese Konfiguration bestimmt, wie SharePoint den Wert behandelt. In Abhängigkeit von der angegebenen Dokumentation kann SharePoint den Wert der jeweiligen Eigenschaft in den Suchindex aufnehmen, unsichere HTML entfernen und Links zu in SharePoint gespeicherten Dokumente auf dem aktuellen Stand halten, falls eine Datei verschoben oder umbenannt wird.

Um die Konfiguration für Ihre Webparteigenschaften anzugeben, setzen Sie in der Webpartklasse den **propertiesMetadata**-Getter außer Kraft:

```ts
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

Die **propertiesMetadata**-Methode gibt ein Objekt zurück, wobei die Eigenschaft eine Zeichenfolge ist und den Namen der Webparteigenschaft angibt, und der Wert ein Objekt ist, das angibt, wie SharePoint diese spezielle Eigenschaft behandeln soll. Beim Außerkraftsetzen der **propertiesMetadata**-Methode müssen Sie nicht alle Webparteigenschaften auflisten. Standardmäßig werden Werte von Webparteigenschaften nicht von SharePoint verarbeitet, und Sie sollten nur die Eigenschaften einschließen, die verarbeitet werden sollen.

Nachfolgend finden Sie eine Liste möglicher Werte, die in den Metadaten der Eigenschaften festgelegt werden können, sowie deren Auswirkungen darauf, wie der Wert der Webparteigenschaft von SharePoint verarbeitet wird.

Metadatenwert|Durchsuchbar|Linkkorrektur|Unsichere HTM entfernen
--------------|:--------:|:--------:|:----------------:
Keine (Standard)|nein|nein|nein
`isSearchablePlainText`|ja|nein|nein
`isHtmlString`|ja|ja|ja
`isImageSource`|ja|ja|nein
`isLink`|ja|ja|nein

> **Wichtig:** Wenn Sie die Konfiguration für die Webparteigenschaften definieren, sollten Sie nur eine der oben genannten Eigenschaften für jede Webparteigenschaft verwenden. Das Festlegen mehrerer Eigenschaften führt mit großer Wahrscheinlichkeit zu unerwünschten Ergebnissen und sollte vermieden werden.

Standardmäßig wird der Wert einer Webparteigenschaft nicht von der SharePoint-Suche indiziert und in keiner Weise von SharePoint verarbeitet. Er wird genau so an das Webpart übergeben, wie er vom Benutzer eingegeben wurde, der das Webpart konfiguriert.

Wenn Sie die Webparteigenschaft als `isSearchablePlainText` angeben, wird diese in den Index für die Volltextsuche eingeschlossen. Immer dann, wenn Benutzer nach Schlüsselwörtern suchen, die in dem Wert dieser Eigenschaft enthalten sind, gibt die SharePoint-Suche die Seite mit dem Webpart in den Suchergebnissen zurück. Wenn der Wert einen Link zu einem in SharePoint gespeicherten Dokument enthält, wird dieser Link nicht aktualisiert, wenn das Dokument, auf das verwiesen wird, verschoben oder umbenannt wird. Außerdem wird HTML, die von Benutzern eingegeben wird, intakt gehalten. Wenn Sie mit dem Wert einer solchen Eigenschaft arbeiten, sollten Sie diese als Nur-Text behandeln und HTML, die möglicherweise von Benutzern eingegeben wird, mit Escapezeichen versehen, bevor diese auf der Seite gerendert wird, um eine Skript-Einfügung zu verhindern.

Wenn eine Webparteigenschaft als `isHtmlString` definiert ist, entfernt SharePoint zunächst unsichere HTML, z. B. `script`-Tags, aus dem Eigenschaftswert. Der verbleibende HTML-Code kann sicher auf einer Seite gerendert werden. Wenn der Wert URLs enthält, die auf in SharePoint gespeicherte Dateien zeigen, aktualisiert SharePoint die in der Webparteigenschaft gespeicherte URL sofort, wenn eine dieser Dateien umbenannt oder verschoben wird. Dadurch wird das Verwalten von URLs über alle Webparts und Seiten in Ihrem Mandanten hinweg wesentlich erleichtert. HTML-Webparteigenschaften können auch durchsucht werden, sodass Benutzer nach Schlüsselwörtern suchen können, die im Eigenschaftswert enthalten sind.

Die Typen `isImageSource` und `isLink` von Eigenschaftswerten sind für die Verwendung für Webparteigenschaften gedacht, die nur einen Link zu einem Bild oder zu einer in SharePoint gespeicherten Datei enthalten. In beiden Fällen schließt die SharePoint-Suche den Inhalt in den Index der Volltextsuche ein und hält die angegebene URL auf dem aktuellen Stand, falls die Datei, auf die verwiesen wird, umbenannt oder verschoben wird. Außerdem werden Bildquellen möglicherweise weiter verarbeitet, damit Bilder schneller heruntergeladen werden können. Wenn die Seite über ein Titelbild verfügt, und das Bild befindet sich unter den ersten fünf Bildern auf der Seite oder in der ersten oder zweiten Zeile der Seite, so wird das Bild vorab geladen.