---
title: "Aufrufen der Microsoft Graph-API aus Ihrem Webpart mittels OAuth"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 0fa5d369358ace2c3e13f279d4f1fcf0f20aef90
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="call-the-microsoft-graph-api-using-oauth-from-your-web-part"></a><span data-ttu-id="163a6-102">Aufrufen der Microsoft Graph-API aus Ihrem Webpart mittels OAuth</span><span class="sxs-lookup"><span data-stu-id="163a6-102">Call the Microsoft Graph API using OAuth from your web part</span></span>

<span data-ttu-id="163a6-p101">Durch eine Integration mit Microsoft Graph können Sie viele nützliche Funktionen zu Ihrem Webpart hinzufügen, beispielsweise eine E-Mail-Funktion, Dokumente und Kalender. Damit Sie Microsoft Graph-APIs aufrufen können, müssen Sie die Active Directory Authentication Library (ADAL) for Javascript-Bibliothek verwenden und zur Authentifizierung den OAuth-Fluss nutzen. Bevor Ihr Webpart ADAL JS nutzen und Microsoft Graph-APIs korrekt und sicher aufrufen kann, sind einige Designspezifika zu berücksichtigen und Codemodifikationen zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="163a6-p101">You can add lots of great functionality such as email, documents, and calendar to your web part by integrating with the Microsoft Graph. To call APIs on Microsoft Graph you will need to use the Active Directory Authentication Library (ADAL) for JavaScript library and authenticate using the OAuth flow. There are some design considerations and code modifications to make for your web part to use ADAL JS and call Microsoft Graph APIs correctly and securely.</span></span>

## <a name="azure-active-directory-authorization-flows"></a><span data-ttu-id="163a6-106">Azure Active Directory-Autorisierungsflüsse</span><span class="sxs-lookup"><span data-stu-id="163a6-106">Azure Active Directory authorization flows</span></span>

<span data-ttu-id="163a6-p102">Office 365 verwendet Azure Active Directory (Azure AD) zur Absicherung seiner APIs, die über Microsoft Graph zugänglich sind. Azure AD wiederum verwendet OAuth als Autorisierungsprotokoll. Wenn eine Anwendung den OAuth-Autorisierungsfluss vollständig durchlaufen hat, erhält sie ein temporäres Zugriffstoken. Das Token ermöglicht den Zugriff auf spezifische Ressourcen im Namen des Benutzers, auf Basis der Berechtigungen, die der Benutzer der Anwendung gewährt hat.</span><span class="sxs-lookup"><span data-stu-id="163a6-p102">Office 365 uses Azure Active Directory (Azure AD) to secure its APIs, which are accessed through the Microsoft Graph. Azure AD uses OAuth as the authorization protocol. When an application completes the OAuth authorization flow it gets a temporary access token. The token provides access to specific resources on behalf of the user by using permissions granted to the application by that user.</span></span>

<span data-ttu-id="163a6-p103">Es gibt verschiedene Arten von OAuth-Flüssen. Welcher zum Einsatz kommt, hängt vom Typ der Anwendung ab. Webanwendungen verwenden einen OAuth-Fluss, bei dem Azure AD auf die URL umleitet, unter der die Anwendung gehostet wird. Diese Umleitung ist eine zusätzliche Sicherheitsmaßnahme zur Verifizierung der Echtheit der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="163a6-p103">There are different types of OAuth flows depending on the kind of application. Web applications use an OAuth flow where Azure AD redirects to the URL where the application is hosted. The redirect is an additional security measure to verify the authenticity of that application.</span></span>

<span data-ttu-id="163a6-p104">Clientanwendungen wie Android- oder iOS-Apps haben keine URL; eine Umleitung ist daher nicht möglich. Diese Anwendungen schließen den OAuth-Fluss also ohne Umleitung ab. Sowohl Webanwendungen als auch Clientanwendungen verwenden eine öffentlich bekannte Client-ID und einen privaten geheimen Clientschlüssel, den nur Azure AD und die Anwendung kennen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p104">Client applications, such as Android and iOS apps, do not have a URL and cannot use a redirect. So they complete the OAuth flow without the redirect. Both web applications and client applications use a publicly known client ID and a privately held client secret known only to Azure AD and the application.</span></span>

<span data-ttu-id="163a6-117">Clientseitige Webanwendungen ähneln Webanwendungen, werden jedoch mithilfe von JavaScript implementiert und im Kontext eines Browsers ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="163a6-117">Client-side web applications are similar to web applications but are implemented using JavaScript and run in the context of a browser.</span></span> <span data-ttu-id="163a6-118">Diese Anwendungen können geheime Clientschlüssel nicht verwenden, ohne sie den Benutzern preiszugeben.</span><span class="sxs-lookup"><span data-stu-id="163a6-118">These applications are incapable of using a client secret without revealing it to users.</span></span> <span data-ttu-id="163a6-119">Sie nutzen daher einen als impliziten OAuth-Fluss bezeichneten Autorisierungsfluss, um auf durch Azure AD gesicherte Ressourcen zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="163a6-119">Therefore these applications use an authorization flow called OAuth implicit flow to access resources secured with Azure AD.</span></span> <span data-ttu-id="163a6-120">In diesem Fluss wird der Vertrag zwischen der Anwendung und Azure AD auf Basis der öffentlich bekannten Client-ID und der URL ausgehandelt, unter der die Anwendung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="163a6-120">In this flow the contract between the application and Azure AD is established based on the publicly-known client ID and the URL where the application is hosted.</span></span> <span data-ttu-id="163a6-121">Clientseitige SharePoint Framework-Webparts müssen diesen Fluss verwenden, um eine Verbindung mit Ressourcen herstellen zu können, die durch Azure AD abgesichert sind.</span><span class="sxs-lookup"><span data-stu-id="163a6-121">This is the flow that SharePoint Framework client-side web parts must use in order to connect to resources secured with Azure AD.</span></span> <span data-ttu-id="163a6-122">Zur Implementierung von Azure AD-basierter Authentifizierung und Autorisierung in Ihrem Webpart können Sie die von Microsoft bereitgestellte [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) verwenden.</span><span class="sxs-lookup"><span data-stu-id="163a6-122">To implement Azure AD-based authentication and authorization in your web part, you can use the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) provided by Microsoft.</span></span>

## <a name="difference-between-client-side-applications-and-sharepoint-framework-web-parts"></a><span data-ttu-id="163a6-123">Unterschied zwischen clientseitigen Anwendungen und SharePoint-Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-123">Difference between client-side applications and SharePoint Framework web parts</span></span>

<span data-ttu-id="163a6-p106">Eine typische clientseitige Webanwendung umfasst die gesamte Seite und ist die einzige Ressource, die unter der Anwendungs-URL verfügbar ist. Alle Elemente der Seite werden während der Entwicklung festgelegt, und die Benutzer der Anwendung können nicht dynamisch neue Elemente hinzufügen. Zwar kann eine clientseitige Webanwendung durchaus aus mehreren Ansichten bestehen, mit externen Daten arbeiten und in gewissem Umfang Konfigurationen erlauben; alle diese Aspekte berücksichtigen die Entwickler jedoch bereits bei der Programmierung der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="163a6-p106">A typical client-side web application owns the whole page and is the only resource available at the application's URL. All elements of the page are determined during development and users working with the application cannot dynamically add new elements. Even though a client-side web application might consist of several views, work with external data, and offer a certain degree of configuration, these aspects are considered by developers while building the application.</span></span>

<span data-ttu-id="163a6-p107">SharePoint-Benutzer können sich Seiten durch Hinzufügen und Konfigurieren von Webparts selbst zusammenstellen. Ein einziger Webpart ist dabei nur ein kleiner Teil der gesamten Seite. Entwickler eines Webparts wissen vorab weder, ob andere Webparts auf derselben Seite platziert werden, noch, welche Ressourcen eventuelle weitere Webparts verwenden werden. Anders als SharePoint-Add-Ins sind Webparts Teil der Seite. Alle Webparts können auf das DOM der Seite zugreifen, und alle Ressourcen, die ein Webpart lädt, sind auch für alle anderen Webparts verfügbar.</span><span class="sxs-lookup"><span data-stu-id="163a6-p107">When working with SharePoint, users compose pages by adding and configuring web parts. A single web part is only a small part of the whole page. Developers building a web part cannot know up front if other web parts will be placed on the same page, and if so, which resources those web parts will use. Unlike SharePoint Add-ins, web parts are a part of the page. All web parts can access the page's DOM, and resources loaded by one web part are available to other web parts.</span></span>

## <a name="limitations-when-using-adal-js-with-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="163a6-132">Einschränkungen bei der Verwendung von ADAL JS in clientseitigen SharePoint Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-132">Limitations when using ADAL JS with SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="163a6-p108">Die ADAL JS-Bibliothek vereinfacht die Implementierung des OAuth-Flusses für Azure AD in clientseitigen Webanwendungen signifikant. Bei Verwendung in clientseitigen SharePoint Framework-Webparts gibt es jedoch eine Reihe von Einschränkungen. Diese Einschränkungen ergeben sich aus der Tatsache, dass ADAL JS für clientseitige Webanwendungen entwickelt wurde, die sich über eine ganze Seite erstrecken und diese Seite nicht mit anderen Anwendungen teilen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p108">The ADAL JS library significantly simplifies implementing the OAuth flow for Azure AD in client-side web applications. But it has a number of limitations when used with SharePoint Framework client-side web parts. These limitations are due to the fact that ADAL JS is designed to be used by client-side web applications that own the whole page and do not share the page with other applications.</span></span>

### <a name="shared-storage"></a><span data-ttu-id="163a6-136">Gemeinsamer Speicher</span><span class="sxs-lookup"><span data-stu-id="163a6-136">Shared storage</span></span>

<span data-ttu-id="163a6-p109">Je nachdem, wie Sie die ADAL JS-Bibliothek in Ihrem Projekt konfigurieren, speichert sie ihre Daten entweder im lokalen Speicher des Browsers oder im Sitzungsspeicher. Ganz gleich jedoch, wo ADAL JS die Informationen speichert: Jede Komponente, die sich auf derselben Seite befindet, kann auf sie zugreifen. Wenn beispielsweise ein Webpart ein Zugriffstoken für Microsoft Graph abruft, kann jedes andere Webpart, das sich auf derselben Seite befindet, dieses Token wiederverwenden und ebenfalls Microsoft Graph aufrufen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p109">Depending on how you configured the ADAL JS library in your project, it will store its data either in the browser's local storage or in the session storage. Either way, the information stored by ADAL JS is accessible to any component on the same page. For example, if one web part retrieves an access token for Microsoft Graph, then any other web part on the same page can reuse that token and call the Microsoft Graph.</span></span>

### <a name="adal-js-as-a-singleton"></a><span data-ttu-id="163a6-140">ADAL JS als Singleton</span><span class="sxs-lookup"><span data-stu-id="163a6-140">ADAL JS as a singleton</span></span>

<span data-ttu-id="163a6-p110">ADAL JS ist als Singleton-Dienst konzipiert, der im globalen Bereich der Seite registriert ist. Bei der Verarbeitung von OAuth-Fluss-Rückrufen in iFrames nutzt ADAL JS-Code die registrierte Singleton-Referenz aus dem Hauptfenster, um den Tokenfluss aufzulösen. Da jedes Webpart in einer anderen Azure AD-Anwendung registriert ist, führt eine Wiederverwendung ein und derselben ADAL JS-Instanz zu unerwünschten Ergebnissen: Jedes Webpart verwendet dann die Konfiguration, die das zuerst auf der Seite geladene Webpart registriert hat.</span><span class="sxs-lookup"><span data-stu-id="163a6-p110">ADAL JS is designed to work as a singleton service registered in the global scope of the page. When processing OAuth flow callbacks in IFrames, ADAL JS code uses the registered singleton reference from the main window to resolve the token flow. Since each web part is registered with a different Azure AD application, reusing the same instance of ADAL JS leads to undesirable results where every web part uses the same configuration as the one registered by the first web part loaded on the page.</span></span>

### <a name="resource-based-storage"></a><span data-ttu-id="163a6-144">Ressourcenbasierter Speicherung</span><span class="sxs-lookup"><span data-stu-id="163a6-144">Resource-based storage</span></span>

<span data-ttu-id="163a6-p111">Standardmäßig speichert die ADAL JS-Bibliothek Informationen wie das aktuelle Zugriffstoken oder dessen Ablaufzeit in einem Satz Schlüssel, der der betreffenden Ressource zugeordnet ist, zum Beispiel Microsoft Graph oder SharePoint. Wenn auf ein und derselben Seite mehrere Komponenten mit unterschiedlichen Berechtigungen auf dieselbe Ressource zugreifen, liefert ADAL JS das zuerst abgerufene Token an alle Komponenten aus. Müssen unterschiedliche Komponenten auf dieselbe Ressource zugreifen, kann der Zugriff fehlschlagen. Veranschaulichen wir uns diese Einschränkung anhand eines Beispiels.</span><span class="sxs-lookup"><span data-stu-id="163a6-p111">By default, the ADAL JS library stores information such as the current access token or its expiration time in a set of keys associated with the particular resource, for example Microsoft Graph or SharePoint. If there are multiple components on one page accessing the same resource with different permissions, then the first retrieved token will be served by ADAL JS to all components. If different components require access to the same resource, then they might fail. To illustrate this limitation, consider the following example.</span></span>

<span data-ttu-id="163a6-p112">Nehmen wir an, es gibt auf einer Seite zwei Webparts: eines, das bevorstehende Besprechungen auflistet, und eines, das neue Besprechungen erstellt. Um die anstehenden Besprechungen abzurufen, nutzt das entsprechende Webpart ein Microsoft Graph-Zugriffstoken mit Berechtigungen zum Lesen der Benutzerkalender. Das Webpart zur Erstellung neuer Besprechungen erfordert jedoch ein Microsoft Graph-Zugriffstoken mit Berechtigungen zum Schreiben in die Benutzerkalender. Wenn das Webpart zum Abrufen bevorstehender Besprechungen zuerst geladen wird, ruft ADAL JS dessen Token ab, das nur die Leseberechtigung hat. Anschließend liefert ADAL JS eben dieses Token an das Webpart zur Erstellung neuer Besprechungen aus. Die logische Konsequenz: Wenn dieses Webpart nun versucht, eine neue Besprechung zu erstellen, schlägt dies mit einem Fehler des Typs „Zugriff verweigert“ fehl. Da eine ressourcenbasierte Speicherung zum Einsatz kommt, würde ADAL JS in einem solchen Szenario erst nach Ablauf des zuvor abgerufenen Tokens ein neues Token für Microsoft Graph abrufen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p112">Imagine that there are two web parts on the page: one that lists upcoming meetings, and one that creates a new meeting. To get upcoming meetings, the upcoming meetings web part uses a Microsoft Graph access token with permissions to read user's calendars. The web part that creates new meetings on the other hand, requires a Microsoft Graph access token with permissions to write to user's calendars. If the upcoming meetings web part loads first then ADAL JS retrieves its token with only the read permission. The same token is then served by ADAL JS to the web part creating new meetings. As you can see, when the web part attempts to create a new meeting the web part will fail with an access denied error. Because of the resource-based storage, ADAL JS wouldn't retrieve a new token for Microsoft Graph until the previously retrieved token expired.</span></span>

### <a name="processing-authorization-callbacks"></a><span data-ttu-id="163a6-156">Verarbeiten von Autorisierungsrückrufen</span><span class="sxs-lookup"><span data-stu-id="163a6-156">Processing authorization callbacks</span></span>

<span data-ttu-id="163a6-p113">Der implizierte OAuth-Fluss basiert auf Umleitungen zwischen Azure AD und der Anwendung, die am Fluss teilnimmt. Zu Beginn des Authentifizierungsprozesses leitet die Anwendung Sie auf die Azure AD-Anmeldeseite um. Nach Abschluss der Authentifizierung leitet Azure AD Sie zurück zur Anwendung und schickt das Identitätstoken in einem URL-Hash an die Anwendung zurück, die dieses dann verarbeitet. Aus der Perspektive eines Webparts auf einer SharePoint-Seite hat dieses Verhalten zwei Nachteile.</span><span class="sxs-lookup"><span data-stu-id="163a6-p113">OAuth implicit flow is based on redirects between Azure AD and the application participating in the flow. When the authentication process starts, the application redirects you to the Azure AD sign-in page. Once the authentication completes, Azure AD redirects you back to the application, and sends the identity token in the URL hash for the application to process. From the perspective of a web part placed on a SharePoint page this behavior has two drawbacks.</span></span>

<span data-ttu-id="163a6-p114">Obwohl Sie bei SharePoint angemeldet sind, müssen Sie sich separat bei Azure AD authentifizieren, damit Ihr Webpart auf die durch Azure AD abgesicherten Ressourcen zugreifen kann. Das Webpart ist nur ein kleiner Teil der Gesamtseite, doch um den Authentifizierungsprozess abzuschließen, müssten Sie die ganze Seite verlassen. Das wäre nicht sehr benutzerfreundlich.</span><span class="sxs-lookup"><span data-stu-id="163a6-p114">Even though you are signed in to SharePoint, you need to separately authenticate with Azure AD in order for your web part to be able to access resources secured with Azure AD. The web part is a small part of the overall page, but in order to complete the authentication process, you would need to leave the whole page which is a poor user experience.</span></span>

<span data-ttu-id="163a6-p115">Nach Abschluss der Authentifizierung leitet Azure AD Sie zurück zur Anwendung. Dabei fügt es in den URL-Hash das Identitätstoken ein, das die Anwendung verarbeiten muss. Da das Identitätstoken jedoch unglücklicherweise keine Informationen zu seiner Herkunft enthält, würden auf einer Seite mit mehreren Webparts alle Webparts versuchen, dieses Identitätstoken aus der URL zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="163a6-p115">After the authentication completes, Azure AD redirects you back to your application. In the URL hash it includes the identity token that your application needs to process. Unfortunately, as the identity token doesn't contain any information about its origin, if you had multiple web parts on one page, all of them would try to process the identity token from the URL.</span></span>

## <a name="use-adal-js-with-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="163a6-166">Verwendung von ADAL JS in clientseitigen SharePoint Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-166">Use ADAL JS with SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="163a6-167">Es gibt Möglichkeiten, die Einschränkungen von ADAL JS zu umgehen und OAuth erfolgreich in einem clientseitigen SharePoint-Framework-Webpart zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="163a6-167">You can overcome the limitations in ADAL JS to implement OAuth successfully in your SharePoint Framework client-side web part.</span></span>

> <span data-ttu-id="163a6-168">**Wichtig:** Die folgende Anleitung basiert auf ADAL JS v1.0.12.</span><span class="sxs-lookup"><span data-stu-id="163a6-168">**Important:** The following guidance is based on ADAL JS v1.0.12.</span></span> <span data-ttu-id="163a6-169">Stellen Sie beim Hinzufügen von ADAL JS zu Ihren SharePoint-Framework-Projekten sicher, dass Sie ADAL JS v1.0.12 installieren, da sonst die in diesem Artikel genannte Anleitung nicht wie erwartet funktioniert.</span><span class="sxs-lookup"><span data-stu-id="163a6-169">Important: The following guidance is based on ADAL JS v1.0.12. When adding ADAL JS to your SharePoint Framework projects, ensure that you're installing ADAL JS v1.0.12 or the guidance mentioned in this article will not work as expected.</span></span>

### <a name="load-adal-js-in-your-web-part"></a><span data-ttu-id="163a6-170">Laden von ADAL JS in Ihrem Webpart</span><span class="sxs-lookup"><span data-stu-id="163a6-170">Load ADAL JS in your web part</span></span>

<span data-ttu-id="163a6-p117">Webparts werden mithilfe von TypeScript erstellt und als AMD-Module verteilt. Dank dieser modularen Architektur können Sie die verschiedenen Ressourcen, die das Webpart verwendet, isolieren. Designbedingt registriert sich ADAL JS selbstständig im globalen Bereich, Sie können die Bibliothek aber mit dem folgenden Code in einem Webpart laden:</span><span class="sxs-lookup"><span data-stu-id="163a6-p117">Web parts are built using TypeScript and distributed as AMD modules. Their modular architecture allows you to isolate the different resources used by the web part. ADAL JS is designed to register itself in the global scope, but you can load it in a web part by using the following code:</span></span>

```ts
import * as AuthenticationContext from 'adal-angular';
```

<span data-ttu-id="163a6-174">Diese Anweisung importiert die Klasse `AuthenticationContext`, die die ADAL JS-Funktionalität für die Verwendung in Webparts verfügbar macht.</span><span class="sxs-lookup"><span data-stu-id="163a6-174">This statement imports the `AuthenticationContext` class that exposes the ADAL JS functionality for use in web parts. Despite the name of the module, the  class works with every JavaScript library.</span></span> <span data-ttu-id="163a6-175">Anders als der Name des Moduls vermuten lässt, funktioniert die Klasse `AuthenticationContext` mit jeder JavaScript-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="163a6-175">This statement imports the  class that exposes the ADAL JS functionality for use in web parts. Despite the name of the module, the `AuthenticationContext` class works with every JavaScript library.</span></span>

### <a name="make-adal-js-suitable-for-use-with-sharepoint-framework-web-parts"></a><span data-ttu-id="163a6-176">Vorbereiten von ADAL JS für die Verwendung in SharePoint-Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-176">Make ADAL JS suitable for use with SharePoint Framework web parts</span></span>

<span data-ttu-id="163a6-p119">Die aktuelle ADAL JS-Funktionalität ist nicht für die Verwendung in Webparts geeignet. Sie müssen daher den nachfolgenden Patch verwenden, damit ADAL JS in Ihrem Webpart funktioniert.</span><span class="sxs-lookup"><span data-stu-id="163a6-p119">The current ADAL JS functionality is unsuitable for use in web parts. Use the following patch to make ADAL JS work in your web part.</span></span>

<span data-ttu-id="163a6-179">**WebPartAuthenticationContext.js:**</span><span class="sxs-lookup"><span data-stu-id="163a6-179">**WebPartAuthenticationContext.js:**</span></span>
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
    _renewStates = _renewStates.split(',');
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

<span data-ttu-id="163a6-180">Der Patch implementiert die folgenden Änderungen in ADAL JS:</span><span class="sxs-lookup"><span data-stu-id="163a6-180">The patch applies the following changes to of ADAL JS:</span></span>
- <span data-ttu-id="163a6-181">Alle Informationen werden in einem Webpart-spezifischen Schlüssel gespeichert (durch die Außerkraftsetzung der Funktionen `_getItem` und `_saveItem`).</span><span class="sxs-lookup"><span data-stu-id="163a6-181">All information is stored in key specific to the web part (see the override of the `_getItem` and `_saveItem` functions)</span></span>
- <span data-ttu-id="163a6-182">Rückrufe werden nur von den Webparts verarbeitet, die sie initiiert haben (durch die Außerkraftsetzung der Funktion `handleWindowCallback`).</span><span class="sxs-lookup"><span data-stu-id="163a6-182">Callbacks are processed only by web parts that initiated them (see the override of the `handleWindowCallback` function)</span></span>
- <span data-ttu-id="163a6-183">Bei der Verifizierung von Rückrufdaten wird die Instanz der Klasse `AuthenticationContext` des spezifischen Webparts verwendet, nicht das global registrierte Singleton (durch `_renewToken`, `getRequestInfo` und die leere Registrierung der Funktion `window.AuthenticationContext`).</span><span class="sxs-lookup"><span data-stu-id="163a6-183">When verifying data from callbacks, the instance of the `AuthenticationContext` class of the specific web part is used instead of the globally registered singleton (see `_renewToken`, `getRequestInfo` and the empty registration of the `window.AuthenticationContext` function)</span></span>

### <a name="use-the-adal-js-patch-in-sharepoint-framework-web-parts"></a><span data-ttu-id="163a6-184">Verwenden des ADAL JS-Patches in SharePoint Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-184">Use the ADAL JS patch in SharePoint Framework web parts</span></span>

<span data-ttu-id="163a6-185">Es ist eine spezielle Konfiguration nötig, damit ADAL JS in SharePoint Framework-Webparts korrekt arbeitet.</span><span class="sxs-lookup"><span data-stu-id="163a6-185">For ADAL JS to work correctly in SharePoint Framework web parts, you have to configure it in a specific way. To do that, you first need to define a custom interface that extends the standard ADAL JS  interface to expose additional properties on the configuration object.</span></span> <span data-ttu-id="163a6-186">Zunächst müssen Sie eine benutzerdefinierte Schnittstelle definieren, die die ADAL JS-Standardschnittstelle `Config` erweitert und zusätzliche Eigenschaften für das Konfigurationsobjekt verfügbar macht.</span><span class="sxs-lookup"><span data-stu-id="163a6-186">For ADAL JS to work correctly in SharePoint Framework web parts, you have to configure it in a specific way. To do that, you first need to define a custom interface that extends the standard ADAL JS `Config` interface to expose additional properties on the configuration object.</span></span>

```ts
export interface IAdalConfig extends adal.Config {
  popUp?: boolean;
  callback?: (error: any, token: string) => void;
  webPartId?: string;
}
```

<span data-ttu-id="163a6-187">Die Eigenschaft `popUp` und die Funktion `callback` sind beide bereits in ADAL JS implementiert, sind jedoch in den TypeScript-Typisierungen der Config-Standardschnittstelle noch nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="163a6-187">The `popUp` property and the `callback` function are both already implemented in ADAL JS but are not exposed in the TypeScript typings of the standard Config interface. You need them in order to allow users to sign in to your web parts using a pop-up window instead of redirecting to the Azure AD sign-in page.</span></span> <span data-ttu-id="163a6-188">Sie werden benötigt, damit Benutzer sich über ein Popupfenster bei Ihrem Webpart anmelden können und nicht auf die Azure AD-Anmeldeseite umgeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="163a6-188">The  property and the  function are both already implemented in ADAL JS but are not exposed in the TypeScript typings of the standard Config interface. You need them in order to allow users to sign in to your web parts using a pop-up window instead of redirecting to the Azure AD sign-in page.</span></span>

<span data-ttu-id="163a6-189">Als Nächstes laden Sie den ADAL JS-Patch, die benutzerdefinierte Konfigurationsschnittstelle und Ihr Konfigurationsobjekt in die Hauptkomponente Ihres Webparts.</span><span class="sxs-lookup"><span data-stu-id="163a6-189">Next load the ADAL JS patch, the custom configuration interface, and your configuration object into the main component of your web part.</span></span>

```tsx
import * as AuthenticationContext from 'adal-angular';
import adalConfig from '../AdalConfig';
import { IAdalConfig } from '../../IAdalConfig';
import '../../WebPartAuthenticationContext';
```

<span data-ttu-id="163a6-190">Im Konstruktor Ihrer Komponente erweitern Sie die ADAL JS-Konfiguration um zusätzliche Eigenschaften und verwenden sie anschließend zur Erstellung einer neuen Instanz der Klasse `AuthenticationContext`.</span><span class="sxs-lookup"><span data-stu-id="163a6-190">In the constructor of your component, extend the ADAL JS configuration with additional properties and use it to create a new instance of the `AuthenticationContext` class.</span></span>

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

<span data-ttu-id="163a6-191">Der Code ruft zunächst das ADAL JS-Standardkonfigurationsobjekt ab und überträgt es an die Typisierung der neu definierten Konfigurationsschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="163a6-191">The code first retrieves the standard ADAL JS configuration object and casts it to the type of the newly defined configuration interface.</span></span> <span data-ttu-id="163a6-192">Anschließend übergibt er die ID der Webpart-Instanz, damit sichergestellt ist, dass alle ADAL JS-Werte so gespeichert werden können, dass es nicht zu Konflikten mit anderen Webparts auf der Seite kommt.</span><span class="sxs-lookup"><span data-stu-id="163a6-192">Then it passes the ID of the web part instance so that all ADAL JS values can be stored in a way that they won't collide with other web parts on the page.</span></span> <span data-ttu-id="163a6-193">Als Nächstes aktiviert der Code die popupbasierte Authentifizierung und definiert eine Rückruffunktion, die bei Abschluss der Authentifizierung ausgeführt wird und die Komponente aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="163a6-193">Next it enables the pop-up-based authentication and defines a callback function that runs when authentication completes to update the component.</span></span> <span data-ttu-id="163a6-194">Zuletzt wird eine neue Instanz der Klasse `AuthenticationContext` erstellt, und die `_singletonInstance`, die im Konstruktor der Klasse `AuthenticationContext` definiert ist, wird zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="163a6-194">Finally it creates a new instance of the `AuthenticationContext` class and resets the `_singletonInstance`  set in the constructor of the `AuthenticationContext` class.</span></span> <span data-ttu-id="163a6-195">Dies ist erforderlich, damit jedes Webpart eine eigene Version des ADAL JS-Authentifizierungskontexts verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="163a6-195">This is required in order to allow every web part to use its own version of the ADAL JS authentication context.</span></span>

## <a name="considerations-when-using-oauth-implicit-flow-in-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="163a6-196">Wichtige Aspekte bei der Verwendung des impliziten OAuth-Flusses in clientseitigen SharePoint-Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="163a6-196">Considerations when using OAuth implicit flow in SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="163a6-p123">Bevor Sie clientseitige SharePoint Framework-Webparts erstellen, die mit durch Azure AD abgesicherten Ressourcen kommunizieren, sollten Sie einige Einschränkungen bedenken. Anhand der nachfolgenden Informationen können Sie entscheiden, ob die Verwendung von OAuth-Autorisierung in Webparts für Ihre Lösung und Ihre Organisation das Richtige ist.</span><span class="sxs-lookup"><span data-stu-id="163a6-p123">Before you build SharePoint Framework client-side web parts that communicate with resources secured by Azure AD, there are some constraints that you should consider. The following information will help you determine when OAuth authorization in web parts is the right choice for your solution and organization.</span></span>

### <a name="sharepoint-framework-web-parts-are-highly-trusted"></a><span data-ttu-id="163a6-199">SharePoint Framework-Webparts haben eine umfassende Vertrauensstellung.</span><span class="sxs-lookup"><span data-stu-id="163a6-199">SharePoint Framework web parts are highly trusted</span></span>

<span data-ttu-id="163a6-p124">Anders als SharePoint-Add-Ins werden Webparts mit denselben Berechtigungen ausgeführt, die auch der aktuelle Benutzer hat. Alles, was der Benutzer tun darf, darf auch das Webpart tun. Deshalb dürfen Webparts nur von Mandantenadministratoren installiert und bereitgestellt werden. Mandantenadministratoren sollten verifizieren, dass alle bereitzustellenden Webparts von einer vertrauenswürdigen Quelle stammen und für die Verwendung im jeweiligen Mandanten freigegeben sind.</span><span class="sxs-lookup"><span data-stu-id="163a6-p124">Unlike SharePoint Add-ins, web parts run with the same permissions as the current user. Whatever the user can do, the web part can do as well. This is why web parts can be installed and deployed only by tenant administrators The tenant administrator should verify that web parts they are deploying come from a trusted source, and were approved for use in the tenant.</span></span>

<span data-ttu-id="163a6-p125">Webparts sind Bestandteil der Seite und teilen sich anders als SharePoint-Add-Ins sowohl das DOM als auch alle Ressourcen mit den anderen Elementen auf der Seite. Zugriffstoken, die Zugriff auf durch Azure AD abgesicherte Ressourcen gewähren, werden über einen Rückruf zu derselben Seite abgerufen, auf der sich das Webpart befindet. Dieser Rückruf kann von jedem beliebigen Element auf der Seite verarbeitet werden. Sobald die Zugriffstoken aus Rückrufen verarbeitet wurden, werden sie zudem im lokalen Speicher des Browsers oder im Sitzungsspeicher gespeichert, aus dem sie von jeder Komponente auf der Seite abgerufen werden können. Ein schädliches Webpart könnte das Token lesen und es oder die mit dem Token abgerufenen Daten für einen externen Dienst verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p125">Web parts are a part of the page and, unlike SharePoint Add-ins, share DOM and resources with other elements on the page. Access tokens that grant access to resources secured with Azure AD, are retrieved through a callback to the same page where the web part is located. That callback can be processed by any element on the page. Also, once access tokens are processed from callbacks, they are stored in the browser's local storage or session storage from where they can be retrieved by any component on the page. A malicious web part could read the token and either expose the token or the data it retrieved using that token to an external service.</span></span>

### <a name="url-is-a-part-of-the-oauth-implicit-flow-contract"></a><span data-ttu-id="163a6-208">Die URL ist ein Teil des Vertrags beim impliziten OAuth-Fluss.</span><span class="sxs-lookup"><span data-stu-id="163a6-208">URL is a part of the OAuth implicit flow contract</span></span>

<span data-ttu-id="163a6-p126">Clientseitige Anwendungen können geheime Clientschlüssel nicht speichern, ohne sie den Benutzern preiszugeben. Um die Echtheit einer bestimmten Anwendung zu verifizieren, wird die URL, unter der die Anwendung gehostet wird, als Teil des Vertrauensvertrags zwischen Azure AD und der Anwendung verwendet. Das bedeutet: Sie müssen die URL jeder Seite in Azure AD registrieren, auf der sich Webparts befinden, die den impliziten OAuth-Fluss verwenden. Wenn eine Seite nicht registriert ist, schlägt der OAuth-Fluss fehl, und dem Webpart wird der Zugriff auf die abgesicherte Ressource verweigert.</span><span class="sxs-lookup"><span data-stu-id="163a6-p126">Client-side applications are incapable of storing a client secret without revealing it to users. In order to verify the authenticity of the particular application, the URL where the application is hosted, is used as a part of the trust contract between Azure AD and the application. The consequences of this are that the URL of every page with web parts using OAuth implicit flow must be registered with Azure AD. If a page is not registered, the OAuth flow will fail and the web part will be denied access to the secured resource.</span></span>

<span data-ttu-id="163a6-p127">Diese notwendige Sicherheitsmaßnahme ist eine signifikante Einschränkung für Organisationen, die es ihren Benutzern erlauben, Webparts zu Seiten hinzuzufügen. Wir empfehlen, nur an wenigen Stellen Webparts einzusetzen, die den impliziten OAuth-Fluss verwenden. Beschränken Sie sich auf einige gängige Stellen wie die Startseite oder spezifische Zielseiten, und registrieren Sie diese Seiten in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="163a6-p127">This necessary security measure is a significant limitation for organizations that allow users to add web parts to pages. We recommend that you limit the number of locations where web parts using OAuth implicit flow are used. Use a few well known locations such as the home page or specific landing pages and have these locations registered with Azure AD.</span></span>

### <a name="internet-explorer-security-zones"></a><span data-ttu-id="163a6-216">Internet Explorer-Sicherheitszonen</span><span class="sxs-lookup"><span data-stu-id="163a6-216">Internet Explorer security zones</span></span>

<span data-ttu-id="163a6-p128">Internet Explorer verwendet Sicherheitszonen, um Sicherheitsrichtlinien auf besuchte Websites anzuwenden. Websites, die unterschiedlichen Sicherheitszonen zugeordnet sind, werden isoliert voneinander ausgeführt und können nicht interagieren. Wenn Sie den impliziten OAuth-Fluss in clientseitigen SharePoint Framework-Webparts verwenden, müssen die Seite mit den OAuth-basierten Webparts und die Azure AD-Anmeldeseite (unter „https://login.microsoftonline.com“) derselben Sicherheitszone zugeordnet sein. Bei abweichender Konfiguration schlägt der Authentifizierungsprozess fehl, und das Webpart kann nicht mit den durch Azure AD abgesicherten Ressourcen kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="163a6-p128">Internet Explorer uses security zones to apply security policies to websites you visit. Websites assigned to different security zones run isolated and cannot cooperate. When using OAuth implicit flow in SharePoint Framework client-side web parts, the page with web parts using OAuth and the Azure AD login page (located at https://login.microsoftonline.com) must be in the same security zone. Without such configuration the authentication process will fail and web part won't be able to communicate with Azure AD-secured resources.</span></span>

### <a name="user-must-sign-in-frequently"></a><span data-ttu-id="163a6-221">Benutzer müssen sich häufig anmelden.</span><span class="sxs-lookup"><span data-stu-id="163a6-221">User must sign in frequently</span></span>

<span data-ttu-id="163a6-p129">Bei Einsatz des regulären OAuth-Flusses erhalten Webanwendungen und Clientanwendungen ein kurzlebiges Zugriffstoken und ein Aktualisierungstoken, das länger gültig ist. Sobald das Zugriffstoken abgelaufen ist, wird mithilfe des Aktualisierungstokens ein neues Zugriffstoken abgerufen. Dieser Ansatz sorgt dafür, dass Benutzer sich seltener bei Azure AD anmelden müssen.</span><span class="sxs-lookup"><span data-stu-id="163a6-p129">When using regular OAuth flow web applications and client applications get a short-lived access token and a refresh token which is valid for a longer period of time. When the access token expires, the refresh token is used to get a new access token. This approach reduces how often users need to sign in to Azure AD.</span></span>

<span data-ttu-id="163a6-p130">Da clientseitige Anwendungen geheime Schlüssel nicht sicher speichern können und die Offenlegung eines Aktualisierungstokens ein hohes Sicherheitsrisiko ist, erhalten sie im Rahmen des impliziten OAuth-Flusses lediglich das Zugriffstoken. Sobald dieses Token abgelaufen ist, muss die Anwendung einen neuen OAuth-Fluss starten. Der Benutzer muss sich dann möglicherweise erneut anmelden.</span><span class="sxs-lookup"><span data-stu-id="163a6-p130">Because client-side applications are incapable of securely storing secrets, and disclosing a refresh token is a serious security threat, they only receive the access token as part of the OAuth implicit flow. Once that token expires, the application must start a new OAuth flow which could require the user to sign in again.</span></span>

## <a name="more-information"></a><span data-ttu-id="163a6-227">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="163a6-227">More information</span></span>

- [<span data-ttu-id="163a6-228">Authentifizierungsszenarien für Azure AD</span><span class="sxs-lookup"><span data-stu-id="163a6-228">Authentication Scenarios for Azure AD</span></span>](https://Azure.microsoft.com/de-DE/documentation/articles/active-directory-authentication-scenarios/)
