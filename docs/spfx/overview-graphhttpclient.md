# <a name="overview-of-the-graphhttpclient-class-preview"></a>Übersicht über die GraphHttpClient-Klasse (Vorschau)

> [!IMPORTANT]
> **GraphHttpClient** befindet sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Er wird derzeit in Produktionsumgebungen nicht unterstützt.

Sie können Microsoft Graph zum Erstellen leistungsstarker Lösungen verwenden, die auf Daten aus Office 365 und anderen Microsoft-Dienste zugreifen. Um SharePoint-Framework-Lösungen (SPFx) mit Microsoft Graph zu verbinden, müssen Sie eine Azure Active Directory (Azure AD)-Anwendung registrieren und den Autorisierungsfluss abschließen. Um dies zu vereinfachen, können Sie die SPFx-Klasse **GraphHttpClient** für den direkten Aufruf von Microsoft Graph verwenden, ohne dass zusätzliche Einrichtungsschritte erforderlich sind.

## <a name="what-is-the-graphhttpclient-class"></a>Was ist die GraphHttpClient-Klasse?

Die **GraphHttpClient**-Klasse ist im SharePoint-Framework enthalten. Sie funktioniert ähnlich wie das HttpClient-Element, das für die Kommunikation mit Drittanbieter APIs verwendet werden kann. Die **GraphHttpClient**-Klasse stellt automatisch sicher, dass Ihre Anforderung an Microsoft Graph ein gültiges Bearerzugriffstoken und die erforderlichen Header aufweist. Wenn Sie eine GET- oder POST-Anforderung ausgeben, prüft **GraphHttpClient**, ob diese ein gültiges Zugriffstoken enthält, und wenn dies nicht der Fall ist, ruft die Klasse eins aus einer internen API ab und speichert es für nachfolgende Anforderungen.

Das folgende Beispiel zeigt eine Anforderung an Microsoft Graph, die die **GraphHttpClient**-Klasse verwendet.

```ts
// ...
import { GraphHttpClient, GraphHttpClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphHttpClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

So senden Sie eine Anforderung an Microsoft Graph

- Importieren Sie die **GraphHttpClient**- und **GraphHttpClientResponse**-Module aus dem Paket **@microsoft/sp-http**.
- Verwenden Sie die Instanz von **GraphHttpClient**, die für die `this.context.graphHttpClient`-Eigenschaft zum Ausgeben einer GET- oder POST-Anforderung an Microsoft Graph zur Verfügung steht.
- Geben Sie als Parameter die Microsoft Graph-API an, die Sie aufrufen möchten (beginnen Sie mit der API-Version ohne führenden Schrägstrich `/`), gefolgt von der **GraphHttpClient**-Konfiguration.
- Optional können Sie zusätzliche Anforderungsheader angeben, die mit den von **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` und `'Content-Type': 'application/json; charset=utf-8'`) festgelegten Standardheadern zusammengeführt werden.

## <a name="considerations-for-using-the-graphhttpclient-class"></a>Überlegungen zur Verwendung der **GraphHttpClient**-Klasse

Die **GraphHttpClient**-Klasse ist eine komfortable Möglichkeit für die Kommunikation mit Microsoft Graph, da sie den Autorisierungsfluss und die Verwaltung von Zugriffstoken abstrahiert. Da **GraphHttpClient** sich derzeit in der Entwicklervorschau befindet, gibt es einige Aspekte, die Sie vor der Verwendung berücksichtigen sollten.

### <a name="use-for-microsoft-graph-access-only"></a>Verwendung ausschließlich zum Zugriff auf Microsoft Graph

Verwenden Sie die **GraphHttpClient**-Klasse ausschließlich für den Zugriff auf Microsoft Graph. Die in der Anforderung angegebene URL muss mit der Version der Microsoft Graph-API beginnen (entweder **v1.0** oder **beta**), gefolgt von dem API-Vorgang. Bei jeder anderen URL wird ein Fehler zurückgegeben.

### <a name="permissions"></a>Berechtigungen

GraphHttpClient verwendet die Azure AD-Anwendung Office 365 SharePoint Online, um im Namen des aktuellen Benutzers ein gültiges Zugriffstoken für Microsoft Graph abzurufen. Das abgerufene Zugriffstoken enthält zwei Berechtigungen:

- Alle Gruppen lesen und schreiben (Preview) (`Group.ReadWrite.All`)
- Alle Verwendungsberichte lesen(`Reports.Read.All`)

Dies sind die einzigen Berechtigungen, die bei der Verwendung von **GraphHttpClient** verfügbar sind. Wenn Sie andere Berechtigungen für Ihre Lösung benötigen, können Sie stattdessen [ADAL JS mit implizitem OAuth-Fluss](web-parts/guidance/call-microsoft-graph-from-your-web-part.md) verwenden.

### <a name="tokens-are-retrieved-using-an-internal-api"></a>Tokenabruf über eine interne API

Um ein gültiges Zugriffstoken abzurufen, gibt **GraphHttpClient** eine Webanforderung an den `/_api/SP.OAuth.Token/Acquire`-Endpunkt aus. Diese API ist nur für die interne Verwendung vorgesehen. Sie sollten in Ihren Lösungen nicht direkt mit dieser kommunizieren.

## <a name="see-also"></a>Siehe auch

- [GraphClient im Application Customizer aus dem Beispiel für eine moderne Teamwebsite](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).
- [Verwenden von GraphHttpClient zum Aufrufen von Microsoft Graph](call-microsoft-graph-using-graphhttpclient.md)
- [Microsoft Graph Dev Center](https://developer.microsoft.com/de-DE/graph/)
