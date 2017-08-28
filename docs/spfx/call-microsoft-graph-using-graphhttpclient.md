# <a name="call-microsoft-graph-using-the-sharepoint-framework-graphhttpclient"></a>Aufrufen von Microsoft Graph mit SharePoint Framework GraphHttpClient

Mit Microsoft Graph können Sie leistungsfähige Lösungen erstellen, die Daten aus den anderen Office 365-Diensten verwenden. Bisher war es nicht ganz einfach, SharePoint Framework-Lösungen mit Microsoft Graph zu verbinden: Es war nötig, eine Azure Active Directory-Anwendung zu registrieren und den Autorisierungsfluss zu durchlaufen. Mit SharePoint Framework GraphHttpClient können Sie Microsoft Graph direkt aufrufen, ohne zusätzliche Einrichtungsschritte.

> **Wichtig:** GraphHttpClient befindet sich derzeit in der Developer Preview-Phase und sollte nicht in Produktionsumgebungen eingesetzt werden.

## <a name="what-is-graphhttpclient"></a>Was ist GraphHttpClient?

GraphHttpClient ist ein spezialisierter HTTP-Client, der als Teil von SharePoint Framework bereitgestellt wird. Er arbeitet ähnlich wie der Client HttpClient, der zur Kommunikation mit Drittanbieter-APIs eingesetzt werden kann. Zusätzlich zum Funktionsumfang von HttpClient stellt GraphHttpClient automatisch sicher, dass Ihre Anforderungen an Microsoft Graph ein gültiges Bearerzugriffstoken und alle erforderlichen Header enthalten. Bei jeder GET- oder POST-Anforderung überprüft GraphHttpClient, ob ein gültiges Zugriffstoken vorhanden ist. Ist kein solches Token vorhanden, ruft der Client automatisch eines von einer internen API ab und speichert es für zukünftige Anforderungen.

Unten sehen Sie eine Beispielanforderung an Microsoft Graph über GraphHttpClient:

```ts
// ...
import { GraphHttpClient, GraphClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

Zunächst importieren Sie die Module **GraphHttpClient** und **GraphClientResponse** aus dem Paket **@microsoft/sp-http**. Anschließend senden Sie über die GraphHttpClient-Instanz in der Eigenschaft `this.context.graphHttpClient` eine GET- oder eine POST-Anforderung an Microsoft Graph. Als Parameter geben Sie die Microsoft Graph-API an, die Sie aufrufen möchten (beginnend mit der API-Version ohne führenden Schrägstrich [`/`]), gefolgt von der GraphHttpClient-Konfiguration. Optional können Sie weitere Anforderungsheader angeben, die dann mit den von GraphHttpClient gesetzten Standardheadern (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` und `'Content-Type': 'application/json; charset=utf-8'`) zusammengeführt werden.

## <a name="graphhttpclient-considerations"></a>Wichtige Aspekte bei der Arbeit mit GraphHttpClient

Der Einsatz von GraphHttpClient ist eine sehr praktische Methode zur Kommunikation mit Microsoft Graph, da der Autorisierungsfluss und die Verwaltung der Zugriffstoken abstrahiert werden. Da sich GraphHttpClient jedoch aktuell noch in der Developer Preview-Phase befindet, gibt es bei der Arbeit mit dem Client einige Aspekte zu bedenken.

### <a name="use-for-microsoft-graph-access-only"></a>Verwendung ausschließlich zum Zugriff auf Microsoft Graph

GraphHttpClient ist ausschließlich als Zugriffsclient für Microsoft Graph gedacht. Die in der Anforderung angegebene URL muss mit der Version der Microsoft Graph-API beginnen (entweder **v1.0** oder **beta**), gefolgt vom betreffenden API-Vorgang. Andere URLs werden mit einer Fehlermeldung abgelehnt.

### <a name="available-permission-scopes"></a>Verfügbare Berechtigungsbereiche

GraphHttpClient verwendet die Azure Active Directory-Anwendung **Office 365 SharePoint Online**, um im Namen des aktuellen Benutzers ein gültiges Zugriffstoken für Microsoft Graph abzurufen. Das abgerufene Zugriffstoken enthält zwei Berechtigungsbereiche: 

* **Alle Gruppen lesen und schreiben (Preview)** (`Group.ReadWrite.All`) 
* **Alle Nutzungsberichte lesen** (`Reports.Read.All`) 

Aktuell sind für GraphHttpClient nur diese beiden Berechtigungen verfügbar. Falls Sie für Ihre Lösung andere Berechtigungsbereiche benötigen, müssen Sie stattdessen [ADAL JS mit implizitem OAuth-Fluss](web-parts/guidance/call-microsoft-graph-from-your-web-part) verwenden.

### <a name="tokens-are-retrieved-using-an-internal-api"></a>Tokenabruf über eine interne API

Zum Abrufen eines gültigen Zugriffstokens sendet GraphHttpClient eine Webanforderung an den Endpunkt `/_api/SP.OAuth.Token/Acquire`. Diese API ist nur zur internen Verwendung gedacht. Ihre Lösungen sollten daher nicht direkt mit ihr kommunizieren.

## <a name="more-information"></a>Weitere Informationen

Als Praxisbeispiel für die Verwendung von GraphHttpClient finden Sie eine Beispiellösung auf GitHub, unter [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).

Weitere Informationen zu Microsoft Graph finden Sie unter [https://developer.microsoft.com/en-us/graph/](https://developer.microsoft.com/en-us/graph/).