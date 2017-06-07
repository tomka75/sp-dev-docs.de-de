# <a name="call-the-microsoft-graph-api-using-oauth-from-your-web-part"></a>Aufrufen der Microsoft Graph-API aus Ihrem Webpart mittels OAuth

Durch eine Integration mit Microsoft Graph können Sie viele nützliche Funktionen zu Ihrem Webpart hinzufügen, beispielsweise eine E-Mail-Funktion, Dokumente und Kalender. Damit Sie Microsoft Graph-APIs aufrufen können, müssen Sie die Active Directory Authentication Library (ADAL) for Javascript-Bibliothek verwenden und zur Authentifizierung den OAuth-Fluss nutzen. Bevor Ihr Webpart ADAL JS nutzen und Microsoft Graph-APIs korrekt und sicher aufrufen kann, sind einige Designspezifika zu berücksichtigen und Codemodifikationen zu implementieren.

## <a name="azure-active-directory-authorization-flows"></a>Azure Active Directory-Autorisierungsflüsse

Office 365 verwendet Azure Active Directory (Azure AD) zur Absicherung seiner APIs, die über Microsoft Graph zugänglich sind. Azure AD wiederum verwendet OAuth als Autorisierungsprotokoll. Wenn eine Anwendung den OAuth-Autorisierungsfluss vollständig durchlaufen hat, erhält sie ein temporäres Zugriffstoken. Das Token ermöglicht den Zugriff auf spezifische Ressourcen im Namen des Benutzers, auf Basis der Berechtigungen, die der Benutzer der Anwendung gewährt hat.

Es gibt verschiedene Arten von OAuth-Flüssen. Welcher zum Einsatz kommt, hängt vom Typ der Anwendung ab. Webanwendungen verwenden einen OAuth-Fluss, bei dem Azure AD auf die URL umleitet, unter der die Anwendung gehostet wird. Diese Umleitung ist eine zusätzliche Sicherheitsmaßnahme zur Verifizierung der Echtheit der Anwendung.

Clientanwendungen wie Android- oder iOS-Apps haben keine URL; eine Umleitung ist daher nicht möglich. Diese Anwendungen schließen den OAuth-Fluss also ohne Umleitung ab. Sowohl Webanwendungen als auch Clientanwendungen verwenden eine öffentlich bekannte Client-ID und einen privaten geheimen Clientschlüssel, den nur Azure AD und die Anwendung kennen.

Clientseitige Webanwendungen ähneln Webanwendungen, werden jedoch mithilfe von JavaScript implementiert und im Kontext eines Browsers ausgeführt. Diese Anwendungen können geheime Clientschlüssel nicht verwenden, ohne sie den Benutzern preiszugeben. Sie nutzen daher einen als impliziten OAuth-Fluss bezeichneten Autorisierungsfluss, um auf durch Azure AD gesicherte Ressourcen zuzugreifen. In diesem Fluss wird der Vertrag zwischen der Anwendung und Azure AD auf Basis der öffentlich bekannten Client-ID und der URL ausgehandelt, unter der die Anwendung gehostet wird. Clientseitige SharePoint Framework-Webparts müssen diesen Fluss verwenden, um eine Verbindung mit Ressourcen herstellen zu können, die durch Azure AD abgesichert sind. Zur Implementierung von Azure AD-basierter Authentifizierung und Autorisierung in Ihrem Webpart können Sie die von Microsoft bereitgestellte [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) verwenden.

## <a name="difference-between-client-side-applications-and-sharepoint-framework-web-parts"></a>Unterschied zwischen clientseitigen Anwendungen und SharePoint Framework-Webparts

Eine typische clientseitige Webanwendung umfasst die gesamte Seite und ist die einzige Ressource, die unter der Anwendungs-URL verfügbar ist. Alle Elemente der Seite werden während der Entwicklung festgelegt, und die Benutzer der Anwendung können nicht dynamisch neue Elemente hinzufügen. Zwar kann eine clientseitige Webanwendung durchaus aus mehreren Ansichten bestehen, mit externen Daten arbeiten und in gewissem Umfang Konfigurationen erlauben; alle diese Aspekte berücksichtigen die Entwickler jedoch bereits bei der Programmierung der Anwendung.

SharePoint-Benutzer können sich Seiten durch Hinzufügen und Konfigurieren von Webparts selbst zusammenstellen. Ein einziger Webpart ist dabei nur ein kleiner Teil der gesamten Seite. Entwickler eines Webparts wissen vorab weder, ob andere Webparts auf derselben Seite platziert werden, noch, welche Ressourcen eventuelle weitere Webparts verwenden werden. Anders als SharePoint-Add-Ins sind Webparts Teil der Seite. Alle Webparts können auf das DOM der Seite zugreifen, und alle Ressourcen, die ein Webpart lädt, sind auch für alle anderen Webparts verfügbar.

## <a name="limitations-when-using-adal-js-with-sharepoint-framework-client-side-web-parts"></a>Einschränkungen bei der Verwendung von ADAL JS in clientseitigen SharePoint Framework-Webparts

Die ADAL JS-Bibliothek vereinfacht die Implementierung des OAuth-Flusses für Azure AD in clientseitigen Webanwendungen signifikant. Bei Verwendung in clientseitigen SharePoint Framework-Webparts gibt es jedoch eine Reihe von Einschränkungen. Diese Einschränkungen ergeben sich aus der Tatsache, dass ADAL JS für clientseitige Webanwendungen entwickelt wurde, die sich über eine ganze Seite erstrecken und diese Seite nicht mit anderen Anwendungen teilen.

### <a name="shared-storage"></a>Gemeinsamer Speicher

Je nachdem, wie Sie die ADAL JS-Bibliothek in Ihrem Projekt konfigurieren, speichert sie ihre Daten entweder im lokalen Speicher des Browsers oder im Sitzungsspeicher. Ganz gleich jedoch, wo ADAL JS die Informationen speichert: Jede Komponente, die sich auf derselben Seite befindet, kann auf sie zugreifen. Wenn beispielsweise ein Webpart ein Zugriffstoken für Microsoft Graph abruft, kann jedes andere Webpart, das sich auf derselben Seite befindet, dieses Token wiederverwenden und ebenfalls Microsoft Graph aufrufen.

### <a name="adal-js-as-a-singleton"></a>ADAL JS als Singleton

ADAL JS ist als Singleton-Dienst konzipiert, der im globalen Bereich der Seite registriert ist. Bei der Verarbeitung von OAuth-Fluss-Rückrufen in iFrames nutzt ADAL JS-Code die registrierte Singleton-Referenz aus dem Hauptfenster, um den Tokenfluss aufzulösen. Da jedes Webpart in einer anderen Azure AD-Anwendung registriert ist, führt eine Wiederverwendung ein und derselben ADAL JS-Instanz zu unerwünschten Ergebnissen: Jedes Webpart verwendet dann die Konfiguration, die das zuerst auf der Seite geladene Webpart registriert hat.

### <a name="resource-based-storage"></a>Ressourcenbasierter Speicherung

Standardmäßig speichert die ADAL JS-Bibliothek Informationen wie das aktuelle Zugriffstoken oder dessen Ablaufzeit in einem Satz Schlüssel, der der betreffenden Ressource zugeordnet ist, zum Beispiel Microsoft Graph oder SharePoint. Wenn auf ein und derselben Seite mehrere Komponenten mit unterschiedlichen Berechtigungen auf dieselbe Ressource zugreifen, liefert ADAL JS das zuerst abgerufene Token an alle Komponenten aus. Müssen unterschiedliche Komponenten auf dieselbe Ressource zugreifen, kann der Zugriff fehlschlagen. Veranschaulichen wir uns diese Einschränkung anhand eines Beispiels.

Nehmen wir an, es gibt auf einer Seite zwei Webparts: eines, das bevorstehende Besprechungen auflistet, und eines, das neue Besprechungen erstellt. Um die anstehenden Besprechungen abzurufen, nutzt das entsprechende Webpart ein Microsoft Graph-Zugriffstoken mit Berechtigungen zum Lesen der Benutzerkalender. Das Webpart zur Erstellung neuer Besprechungen erfordert jedoch ein Microsoft Graph-Zugriffstoken mit Berechtigungen zum Schreiben in die Benutzerkalender. Wenn das Webpart zum Abrufen bevorstehender Besprechungen zuerst geladen wird, ruft ADAL JS dessen Token ab, das nur die Leseberechtigung hat. Anschließend liefert ADAL JS eben dieses Token an das Webpart zur Erstellung neuer Besprechungen aus. Die logische Konsequenz: Wenn dieses Webpart nun versucht, eine neue Besprechung zu erstellen, schlägt dies mit einem Fehler des Typs „Zugriff verweigert“ fehl. Da eine ressourcenbasierte Speicherung zum Einsatz kommt, würde ADAL JS in einem solchen Szenario erst nach Ablauf des zuvor abgerufenen Tokens ein neues Token für Microsoft Graph abrufen.

### <a name="processing-authorization-callbacks"></a>Verarbeiten von Autorisierungsrückrufen

Der implizierte OAuth-Fluss basiert auf Umleitungen zwischen Azure AD und der Anwendung, die am Fluss teilnimmt. Zu Beginn des Authentifizierungsprozesses leitet die Anwendung Sie auf die Azure AD-Anmeldeseite um. Nach Abschluss der Authentifizierung leitet Azure AD Sie zurück zur Anwendung und schickt das Identitätstoken in einem URL-Hash an die Anwendung zurück, die dieses dann verarbeitet. Aus der Perspektive eines Webparts auf einer SharePoint-Seite hat dieses Verhalten zwei Nachteile.

Obwohl Sie bei SharePoint angemeldet sind, müssen Sie sich separat bei Azure AD authentifizieren, damit Ihr Webpart auf die durch Azure AD abgesicherten Ressourcen zugreifen kann. Das Webpart ist nur ein kleiner Teil der Gesamtseite, doch um den Authentifizierungsprozess abzuschließen, müssten Sie die ganze Seite verlassen. Das wäre nicht sehr benutzerfreundlich.

Nach Abschluss der Authentifizierung leitet Azure AD Sie zurück zur Anwendung. Dabei fügt es in den URL-Hash das Identitätstoken ein, das die Anwendung verarbeiten muss. Da das Identitätstoken jedoch unglücklicherweise keine Informationen zu seiner Herkunft enthält, würden auf einer Seite mit mehreren Webparts alle Webparts versuchen, dieses Identitätstoken aus der URL zu verarbeiten.

## <a name="use-adal-js-with-sharepoint-framework-client-side-web-parts"></a>Verwendung von ADAL JS in clientseitigen SharePoint Framework-Webparts

Es gibt Möglichkeiten, die Einschränkungen von ADAL JS zu umgehen und OAuth erfolgreich in einem clientseitigen SharePoint Framework-Webpart zu implementieren.

> **Wichtig:** Die folgende Anleitung basiert auf ADAL JS v1.0.12. Stellen Sie beim Hinzufügen von ADAL JS zu Ihren SharePoint Framework-Projekten sicher, dass Sie ADAL JS v1.0.12 installieren, da sonst die in diesem Artikel genannte Anleitung nicht wie erwartet funktioniert.

### <a name="load-adal-js-in-your-web-part"></a>Laden von ADAL JS in Ihrem Webpart

Webparts werden mithilfe von TypeScript erstellt und als AMD-Module verteilt. Dank dieser modularen Architektur können Sie die verschiedenen Ressourcen, die das Webpart verwendet, isolieren. Designbedingt registriert sich ADAL JS selbstständig im globalen Bereich, Sie können die Bibliothek aber mit dem folgenden Code in einem Webpart laden:

```ts
import * as AuthenticationContext from 'adal-angular';
```

Diese Anweisung importiert die Klasse `AuthenticationContext`, die die ADAL JS-Funktionalität für die Verwendung in Webparts verfügbar macht. Anders als der Name des Moduls vermuten lässt, funktioniert die Klasse `AuthenticationContext` mit jeder JavaScript-Bibliothek.

### <a name="make-adal-js-suitable-for-use-with-sharepoint-framework-web-parts"></a>Vorbereiten von ADAL JS für die Verwendung in SharePoint Framework-Webparts

Die aktuelle ADAL JS-Funktionalität ist nicht für die Verwendung in Webparts geeignet. Sie müssen daher den nachfolgenden Patch verwenden, damit ADAL JS in Ihrem Webpart funktioniert.

**WebPartAuthenticationContext.js:**
```js
const AuthenticationContext = require('adal-angular');

AuthenticationContext.prototype._getItemSuper = AuthenticationContext.prototype._getItem;
AuthenticationContext.prototype._saveItemSuper = AuthenticationContext.prototype._saveItem;
AuthenticationContext.prototype.handleWindowCallbackSuper = AuthenticationContext.prototype.handleWindowCallback;
AuthenticationContext.prototype._renewTokenSuper = AuthenticationContext.prototype._renewToken;
AuthenticationContext.prototype.getRequestInfoSuper = AuthenticationContext.prototype.getRequestInfo;
AuthenticationContext.prototype._addAdalFrameSuper = AuthenticationContext.prototype._addAdalFrame;

AuthenticationContext.prototype._getItem = function (key) {
  if (this.config.webPartId) {
    key = this.config.webPartId + '_' + key;
  }

  return this._getItemSuper(key);
};

AuthenticationContext.prototype._saveItem = function (key, object) {
  if (this.config.webPartId) {
    key = this.config.webPartId + '_' + key;
  }

  return this._saveItemSuper(key, object);
};

AuthenticationContext.prototype.handleWindowCallback = function (hash) {
  if (hash == null) {
    hash = window.location.hash;
  }

  if (!this.isCallback(hash)) {
    return;
  }

  var requestInfo = this.getRequestInfo(hash);
  if (requestInfo.requestType === this.REQUEST_TYPE.LOGIN) {
    return this.handleWindowCallbackSuper(hash);
  }

  var resource = this._getResourceFromState(requestInfo.stateResponse);
  if (!resource || resource.length === 0) {
    return;
  }

  if (this._getItem(this.CONSTANTS.STORAGE.RENEW_STATUS + resource) === this.CONSTANTS.TOKEN_RENEW_STATUS_IN_PROGRESS) {
    return this.handleWindowCallbackSuper(hash);
  }
}

AuthenticationContext.prototype._renewToken = function (resource, callback) {
  this._renewTokenSuper(resource, callback);
  var _renewStates = this._getItem('renewStates');
  if (_renewStates) {
    _renewStates = _renewStates.split(';');
  }
  else {
    _renewStates = [];
  }
  _renewStates.push(this.config.state);
  this._saveItem('renewStates', _renewStates);
}

AuthenticationContext.prototype.getRequestInfo = function (hash) {
  var requestInfo = this.getRequestInfoSuper(hash);
  var _renewStates = this._getItem('renewStates');
  if (!_renewStates) {
    return requestInfo;
  }

  _renewStates = _renewStates.split(';');
  for (var i = 0; i < _renewStates.length; i++) {
    if (_renewStates[i] === requestInfo.stateResponse) {
      requestInfo.requestType = this.REQUEST_TYPE.RENEW_TOKEN;
      requestInfo.stateMatch = true;
      break;
    }
  }

  return requestInfo;
}

AuthenticationContext.prototype._addAdalFrame = function (iframeId) {
  var adalFrame = this._addAdalFrameSuper(iframeId);
  adalFrame.style.width = adalFrame.style.height = '106px';
  return adalFrame;
}

window.AuthenticationContext = function() {
  return undefined;
}
```

Der Patch implementiert die folgenden Änderungen in ADAL JS:
- Alle Informationen werden in einem Webpart-spezifischen Schlüssel gespeichert (durch die Außerkraftsetzung der Funktionen `_getItem` und `_saveItem`).
- Rückrufe werden nur von den Webparts verarbeitet, die sie initiiert haben (durch die Außerkraftsetzung der Funktion `handleWindowCallback`).
- Bei der Verifizierung von Rückrufdaten wird die Instanz der Klasse `AuthenticationContext` des spezifischen Webparts verwendet, nicht das global registrierte Singleton (durch `_renewToken`, `getRequestInfo` und die leere Registrierung der Funktion `window.AuthenticationContext`).

### <a name="use-the-adal-js-patch-in-sharepoint-framework-web-parts"></a>Verwenden des ADAL JS-Patches in SharePoint Framework-Webparts

Es ist eine spezielle Konfiguration nötig, damit ADAL JS in SharePoint Framework-Webparts korrekt arbeitet. Zunächst müssen Sie eine benutzerdefinierte Schnittstelle definieren, die die ADAL JS-Standardschnittstelle `Config` erweitert und zusätzliche Eigenschaften für das Konfigurationsobjekt verfügbar macht.

```ts
export interface IAdalConfig extends adal.Config {
  popUp?: boolean;
  callback?: (error: any, token: string) => void;
  webPartId?: string;
}
```

Die Eigenschaft `popUp` und die Funktion `callback` sind beide bereits in ADAL JS implementiert, sind jedoch in den TypeScript-Typisierungen der Config-Standardschnittstelle noch nicht verfügbar. Sie werden benötigt, damit Benutzer sich über ein Popupfenster bei Ihrem Webpart anmelden können und nicht auf die Azure AD-Anmeldeseite umgeleitet werden.

Als Nächstes laden Sie den ADAL JS-Patch, die benutzerdefinierte Konfigurationsschnittstelle und Ihr Konfigurationsobjekt in die Hauptkomponente Ihres Webparts.

```tsx
import * as AuthenticationContext from 'adal-angular';
import adalConfig from '../AdalConfig';
import { IAdalConfig } from '../../IAdalConfig';
import '../../WebPartAuthenticationContext';
```

Im Konstruktor Ihrer Komponente erweitern Sie die ADAL JS-Konfiguration um zusätzliche Eigenschaften und verwenden sie anschließend zur Erstellung einer neuen Instanz der Klasse `AuthenticationContext`.

```tsx
export default class UpcomingMeetings extends React.Component<IUpcomingMeetingsProps, IUpcomingMeetingsState> {
  private authCtx: adal.AuthenticationContext;

  constructor(props: IUpcomingMeetingsProps, state: IUpcomingMeetingsState) {
    super(props);

    this.state = {
      loading: false,
      error: null,
      upcomingMeetings: [],
      signedIn: false
    };

    const config: IAdalConfig = adalConfig;
    config.webPartId = this.props.webPartId;
    config.popUp = true;
    config.callback = (error: any, token: string): void => {
      this.setState((previousState: IUpcomingMeetingsState, currentProps: IUpcomingMeetingsProps): IUpcomingMeetingsState => {
        previousState.error = error;
        previousState.signedIn = !(!this.authCtx.getCachedUser());
        return previousState;
      });
    };

    this.authCtx = new AuthenticationContext(config);
    AuthenticationContext.prototype._singletonInstance = undefined;
  }
}
```

Der Code ruft zunächst das ADAL JS-Standardkonfigurationsobjekt ab und überträgt es an die Typisierung der neu definierten Konfigurationsschnittstelle. Anschließend übergibt er die ID der Webpart-Instanz, damit sichergestellt ist, dass alle ADAL JS-Werte so gespeichert werden können, dass es nicht zu Konflikten mit anderen Webparts auf der Seite kommt. Als Nächstes aktiviert der Code die popupbasierte Authentifizierung und definiert eine Rückruffunktion, die bei Abschluss der Authentifizierung ausgeführt wird und die Komponente aktualisiert. Zuletzt wird eine neue Instanz der Klasse `AuthenticationContext` erstellt, und die `_singletonInstance`, die im Konstruktor der Klasse `AuthenticationContext` definiert ist, wird zurückgesetzt. Dies ist erforderlich, damit jedes Webpart eine eigene Version des ADAL JS-Authentifizierungskontexts verwenden kann.

## <a name="considerations-when-using-oauth-implicit-flow-in-sharepoint-framework-client-side-web-parts"></a>Wichtige Aspekte bei der Verwendung des impliziten OAuth-Flusses in clientseitigen SharePoint Framework-Webparts

Bevor Sie clientseitige SharePoint Framework-Webparts erstellen, die mit durch Azure AD abgesicherten Ressourcen kommunizieren, sollten Sie einige Einschränkungen bedenken. Anhand der nachfolgenden Informationen können Sie entscheiden, ob die Verwendung von OAuth-Autorisierung in Webparts für Ihre Lösung und Ihre Organisation das Richtige ist.

### <a name="sharepoint-framework-web-parts-are-highly-trusted"></a>SharePoint Framework-Webparts haben eine umfassende Vertrauensstellung.

Anders als SharePoint-Add-Ins werden Webparts mit denselben Berechtigungen ausgeführt, die auch der aktuelle Benutzer hat. Alles, was der Benutzer tun darf, darf auch das Webpart tun. Deshalb dürfen Webparts nur von Mandantenadministratoren installiert und bereitgestellt werden. Mandantenadministratoren sollten verifizieren, dass alle bereitzustellenden Webparts von einer vertrauenswürdigen Quelle stammen und für die Verwendung im jeweiligen Mandanten freigegeben sind.

Webparts sind Bestandteil der Seite und teilen sich anders als SharePoint-Add-Ins sowohl das DOM als auch alle Ressourcen mit den anderen Elementen auf der Seite. Zugriffstoken, die Zugriff auf durch Azure AD abgesicherte Ressourcen gewähren, werden über einen Rückruf zu derselben Seite abgerufen, auf der sich das Webpart befindet. Dieser Rückruf kann von jedem beliebigen Element auf der Seite verarbeitet werden. Sobald die Zugriffstoken aus Rückrufen verarbeitet wurden, werden sie zudem im lokalen Speicher des Browsers oder im Sitzungsspeicher gespeichert, aus dem sie von jeder Komponente auf der Seite abgerufen werden können. Ein schädliches Webpart könnte das Token lesen und es oder die mit dem Token abgerufenen Daten für einen externen Dienst verfügbar machen.

### <a name="url-is-a-part-of-the-oauth-implicit-flow-contract"></a>Die URL ist ein Teil des Vertrags beim impliziten OAuth-Fluss.

Clientseitige Anwendungen können geheime Clientschlüssel nicht speichern, ohne sie den Benutzern preiszugeben. Um die Echtheit einer bestimmten Anwendung zu verifizieren, wird die URL, unter der die Anwendung gehostet wird, als Teil des Vertrauensvertrags zwischen Azure AD und der Anwendung verwendet. Das bedeutet: Sie müssen die URL jeder Seite in Azure AD registrieren, auf der sich Webparts befinden, die den impliziten OAuth-Fluss verwenden. Wenn eine Seite nicht registriert ist, schlägt der OAuth-Fluss fehl, und dem Webpart wird der Zugriff auf die abgesicherte Ressource verweigert.

Diese notwendige Sicherheitsmaßnahme ist eine signifikante Einschränkung für Organisationen, die es ihren Benutzern erlauben, Webparts zu Seiten hinzuzufügen. Wir empfehlen, nur an wenigen Stellen Webparts einzusetzen, die den impliziten OAuth-Fluss verwenden. Beschränken Sie sich auf einige gängige Stellen wie die Startseite oder spezifische Zielseiten, und registrieren Sie diese Seiten in Azure AD.

### <a name="internet-explorer-security-zones"></a>Internet Explorer-Sicherheitszonen

Internet Explorer verwendet Sicherheitszonen, um Sicherheitsrichtlinien auf besuchte Websites anzuwenden. Websites, die unterschiedlichen Sicherheitszonen zugeordnet sind, werden isoliert voneinander ausgeführt und können nicht interagieren. Wenn Sie den impliziten OAuth-Fluss in clientseitigen SharePoint Framework-Webparts verwenden, müssen die Seite mit den OAuth-basierten Webparts und die Azure AD-Anmeldeseite (unter „https://login.microsoftonline.com“) derselben Sicherheitszone zugeordnet sein. Bei abweichender Konfiguration schlägt der Authentifizierungsprozess fehl, und das Webpart kann nicht mit den durch Azure AD abgesicherten Ressourcen kommunizieren.

### <a name="user-must-sign-in-frequently"></a>Benutzer müssen sich häufig anmelden.

Bei Einsatz des regulären OAuth-Flusses erhalten Webanwendungen und Clientanwendungen ein kurzlebiges Zugriffstoken und ein Aktualisierungstoken, das länger gültig ist. Sobald das Zugriffstoken abgelaufen ist, wird mithilfe des Aktualisierungstokens ein neues Zugriffstoken abgerufen. Dieser Ansatz sorgt dafür, dass Benutzer sich seltener bei Azure AD anmelden müssen.

Da clientseitige Anwendungen geheime Schlüssel nicht sicher speichern können und die Offenlegung eines Aktualisierungstokens ein hohes Sicherheitsrisiko ist, erhalten sie im Rahmen des impliziten OAuth-Flusses lediglich das Zugriffstoken. Sobald dieses Token abgelaufen ist, muss die Anwendung einen neuen OAuth-Fluss starten. Der Benutzer muss sich dann möglicherweise erneut anmelden.

## <a name="more-information"></a>Weitere Informationen

- [Authentifizierungsszenarien für Azure AD](https://Azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/)