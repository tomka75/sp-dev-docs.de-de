---
title: "Behandeln von Sicherheitstokens in vom Anbieter gehosteten wenig vertrauenswürdigen SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: eee92f719ac3747f845f4aea807f71356f982fdb
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins"></a><span data-ttu-id="05410-102">Behandeln von Sicherheitstokens in vom Anbieter gehosteten wenig vertrauenswürdigen SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="05410-102">Handle security tokens in provider-hosted low-trust SharePoint Add-ins</span></span>
<span data-ttu-id="05410-103">Erfahren Sie mehr über die Kontext-, Zugriffs- und Aktualisierungstoken, die für die Autorisierung der vom Anbieter gehosteten SharePoint-Add-Ins mit niedriger Vertrauensebene verwendet werden, und wie Sie mit diesen in Ihrem Code arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="05410-103">Learn about the context, access, and refresh tokens that are used for authorization by low-trust, provider-hosted SharePoint Add-ins, and how to work with them in your code.</span></span>
 

 <span data-ttu-id="05410-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="05410-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="05410-p102">**WICHTIG**   **In diesem Artikel geht es um die Verwendung von Sicherheitstoken im Autorisierungssystem mit niedriger Vertrauensebene, nicht um das besonders vertrauenswürdige System.** Informationen zur Verwendung von Token im besonders vertrauenswürdigen System finden Sie unter [Erstellen und Verwenden von Zugriffstoken in vom Anbieter gehostete besonders vertrauenswürdige SharePoint-Add-Ins](create-and-use-access-tokens-in-provider-hosted-high-trust-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="05410-p102">**Important**   **This article is entirely about the use of security tokens in the low-trust authorization system, not the high-trust system.** For information about the use of tokens in the high-trust system, see [Create and use access tokens in provider-hosted high-trust SharePoint Add-ins](create-and-use-access-tokens-in-provider-hosted-high-trust-sharepoint-add-ins.md).</span></span>
 


 <span data-ttu-id="05410-p103">**SharePoint-Add-Ins, die das  [Autorisierungssystem mit niedriger Vertrauensebene](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) verwenden, um Zugriff auf SharePoint-Daten zu erhalten, nehmen an einem OAuth-Ablauf teil, der die Übergabe von Sicherheitstoken (im [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/)-Format) unter SharePoint, Microsoft Azure Access Control Service (ACS), den Remotekomponenten der SharePoint-Add-In und, in einigen Fällen, dem Browser des Benutzers beinhaltet.** Je nach Design des Add-Ins gibt es verschiedene Abläufe, aber beinhalten mindestens zwei der folgenden Tokentypen:</span><span class="sxs-lookup"><span data-stu-id="05410-p103">**SharePoint Add-ins that use the  [low-trust authorization system](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) to gain access to SharePoint data participate in an OAuthflow that involves the passing of security tokens (in [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/) format) among SharePoint, Microsoft Azure Access Control Service (ACS), the remote components of the SharePoint Add-in, and, in some cases, the user's browser.** There are different flows depending on the design of the add-in, but all of them involve at least the following two types of tokens:</span></span>
 


-  <span data-ttu-id="05410-p104">**Zugriffstoken:** Enthalten in jeder CRUD-Anforderung (Erstellen, Lesen, Aktualisieren oder Löschen) von den Remotekomponenten des Add-Ins an SharePoint. SharePoint überprüft das Token und verarbeitet die Anforderung.</span><span class="sxs-lookup"><span data-stu-id="05410-p104">**Access token:** Included in each create, read, update, or delete (CRUD) request from the remote components of the add-in to SharePoint. SharePoint validates the token and serves the request.</span></span>
    
 
-  <span data-ttu-id="05410-113">**Aktualisierungstoken:** Verwendet zum Abrufen des ersten Zugriffstokens im [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) und zum Ersetzen ablaufender Zugriffstoken sowohl im Kontexttoken- als auch im [Autorisierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) des Autorisierungssystems mit niedriger Vertrauensebene.</span><span class="sxs-lookup"><span data-stu-id="05410-113">**Refresh token:** Used to obtain a first access token in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), and to replace expiring access tokens in both the Context Token flow and the  [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) of the low-trust authorization system.</span></span>
    
 
<span data-ttu-id="05410-114">Je nachdem, welchen OAuth-Ablauf das Add-In verwendet, ist eine der folgenden beiden Optionen Teil des Prozesses:</span><span class="sxs-lookup"><span data-stu-id="05410-114">Depending on which OAuth flow the add-in is using, one or the other of the following is also part of the process:</span></span>
 

-  <span data-ttu-id="05410-115">**Kontexttoken:** Im Kontexttokenablauf verwendet, um der Remotekomponente ein Aktualisierungstoken und Informationen bereitzustellen, die sie benötigt, um ein Zugriffstoken von Azure ACS anzufordern.</span><span class="sxs-lookup"><span data-stu-id="05410-115">**Context token:** Used, in the Context Token flow, to provide the remote component with a refresh token and with information that it needs to request an access token from Azure ACS.</span></span>
    
 
-  <span data-ttu-id="05410-p105">**Autorisierungscode:** Kein Token, sondern Autorisierungscode, der für jedes Benutzer- und Anwendungskombination eindeutig ist. Er wird im Autorisierungscodeablauf verwendet, um ein erstes Zugriffstoken und ein Aktualisierungstoken zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="05410-p105">**Authorizaton code:** Not a token, but an authorization code, unique to each pair of user and application. It is used in the Authorization Code flow to obtain a first access token, and a refresh token.</span></span>
    
 

## <a name="understand-the-handling-of-access-tokens"></a><span data-ttu-id="05410-118">Grundlegendes zur Verwendung von Zugriffstoken</span><span class="sxs-lookup"><span data-stu-id="05410-118">Understand the handling of access tokens</span></span>
<span data-ttu-id="05410-119"><a name="AccessTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-119"></span></span>

<span data-ttu-id="05410-p106">Im Autorisierungssystem mit niedriger Vertrauensebene werden die Zugriffstoken von Azure ACS erstellt und an die Remotekomponente Ihres SharePoint-Add-Ins gesendet. (Zum Zeitpunkt, an dem dieser Artikel geschrieben wurde, hatten von ACS ausgestellte Zugriffstoken für SharePoint eine Lebensspanne von 12 Stunden, das kann sich aber geändert haben.) Die wichtigsten **Dinge, die der Code in Ihrem SharePoint-Add-In erledigen muss**, sind die folgenden:</span><span class="sxs-lookup"><span data-stu-id="05410-p106">In the low-trust authorization system, the access tokens are created by Azure ACS and sent to the remote component of your SharePoint Add-in. (When this article was written, ACS-issued access tokens for SharePoint had a life span of 12 hours, but that could change.) The main  **things that the code in your SharePoint Add-in needs to do** are:</span></span>
 

 

-  <span data-ttu-id="05410-p107">**Anfordern eines Zugriffstokens** von Azure ACS. Je nachdem, welcher OAuth-Ablauf verwendet wird, nutzt das Add-In entweder einen Autorisierungscode oder Informationen, die es aus einem Kontexttoken extrahiert, um die Anforderung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="05410-p107">**Request an access token** from Azure ACS. Depending on which OAuth flow is being used, the add-in uses either an authorization code or information it extracts from a context token to make the request.</span></span>
    
 
-  <span data-ttu-id="05410-p108">**Schließen Sie das Token in jede HTTP-Anforderung an SharePoint ein.** Das Token wird als ein **Authorization**-Header an die Anforderung angehängt. Der Wert des Headers ist das Wort "Bearer", gefolgt von einem Leerzeichen, gefolgt von dem Base64-codierten Zugriffstoken.</span><span class="sxs-lookup"><span data-stu-id="05410-p108">**Include the token in every HTTP request to SharePoint.** The token is added as an **Authorization** header to the request. The value of the header is the word "Bearer", followed by a space, followed by the base 64 encoded access token.</span></span>
    
 
- <span data-ttu-id="05410-127">Optional (jedoch empfohlen) können Sie **das Zugriffstoken zwischenspeichern**, damit es in nachfolgenden Anforderungen erneut verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="05410-127">Optionally (but recommended),  **cache the access token** for reuse on subsequent requests.</span></span>
    
 
- <span data-ttu-id="05410-128">Optional können Sie das Zugriffstoken an Back-End-Systeme weiterleiten, damit diese direkt auf SharePoint zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="05410-128">Optionally, forward the access token to back end systems so they can directly access SharePoint.</span></span>
    
 
<span data-ttu-id="05410-p109">Diese Aufgaben müssen mit serverseitigem Code durchgeführt werden. Wenn Sie verwalteten Code verwenden, befindet sich Beispielcode für einige dieser Aufgaben in den Dateien SharePointContext.cs (oder .vb) und TokenHelper.cs (oder .vb), die Teil von Microsoft Office-Entwicklertools für Visual Studio sind. Ein Beispiel für PHP-Code, der einige dieser Aufgaben ausführt, finden Sie unter  [Erläuterungen zur REST-Schnittstelle von SharePoint und zu ihrer Verwendung](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="05410-p109">These tasks must be done with server-side code. If you are using managed code, sample code for some of these tasks is in the SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb) files that are part of Microsoft Office Developer Tools for Visual Studio. For an example of PHP code that carries out some of these tasks, see  [Understanding and Using the SharePoint REST Interface](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span></span>
 

 

### <a name="cache-the-access-token"></a><span data-ttu-id="05410-132">Zwischenspeichern des Zugriffstokens</span><span class="sxs-lookup"><span data-stu-id="05410-132">Cache the access token</span></span>
<span data-ttu-id="05410-133"><a name="CacheAccessToken"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-133"></span></span>

<span data-ttu-id="05410-134">Je nach der Architektur Ihres SharePoint-Add-Ins und der Hosting-Plattform gibt es verschiedene **Wege zum Zwischenspeichern des Zugriffstokens** auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="05410-134">Depending on your SharePoint Add-in's architecture and the hosting platform, there are several  **ways to cache the access token** on the server.</span></span>
 

 

- <span data-ttu-id="05410-135">Im Sitzungszustand</span><span class="sxs-lookup"><span data-stu-id="05410-135">In session state</span></span>
    
 
- <span data-ttu-id="05410-136">Im Anwendungszustand</span><span class="sxs-lookup"><span data-stu-id="05410-136">In application state</span></span>
    
 
- <span data-ttu-id="05410-137">Im [Windows Server AppFabric-Cache](http://msdn.microsoft.com/library/8aef3f5d-2a77-46d9-b951-0768fedd31a1%28Office.15%29.aspx) oder seiner Entsprechung in einem anderen Betriebssystem als von Microsoft.</span><span class="sxs-lookup"><span data-stu-id="05410-137">In  [Windows Server AppFabric Caching](http://msdn.microsoft.com/library/8aef3f5d-2a77-46d9-b951-0768fedd31a1%28Office.15%29.aspx) or its equivalent in a non-Microsoft OS.</span></span>
    
 
- <span data-ttu-id="05410-138">Im [Microsoft Azure Caching Service](http://msdn.microsoft.com/library/7c679300-07cc-4ba1-b8fa-39421b570d56%28Office.15%29.aspx) oder seiner Entsprechung in einem anderen Betriebssystem als von Microsoft.</span><span class="sxs-lookup"><span data-stu-id="05410-138">In the  [Microsoft Azure Caching Service](http://msdn.microsoft.com/library/7c679300-07cc-4ba1-b8fa-39421b570d56%28Office.15%29.aspx) or its equivalent in a non-Microsoft cloud service.</span></span>
    
 
- <span data-ttu-id="05410-139">In einer Datenbank</span><span class="sxs-lookup"><span data-stu-id="05410-139">In a database</span></span>
    
 
- <span data-ttu-id="05410-140">In einem [memcached](http://www.memcached.org/)-System</span><span class="sxs-lookup"><span data-stu-id="05410-140">In a  [memcached](http://www.memcached.org/) system</span></span>
    
 

 <span data-ttu-id="05410-p110">**Hinweis** In den meisten Szenarien können Sie nicht so einfache Begriffe wie „Zugriffstoken“ als Cacheschlüssel verwenden, weil Ihr Add-In die Token für verschiedene Benutzer und SharePoint-Farmen/-Mandanten voneinander unterscheiden können muss. Wenn Ihr Add-In den [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) verwendet, wird ein spezieller **CacheKey** von SharePoint bereitgestellt, der verwendet werden kann, um zwischengespeicherte Token zu unterscheiden. In diesem Abschnitt wird erklärt, worin die Probleme liegen und was Sie tun können, wenn Ihre Anwendung nicht den Kontexttokenablauf verwendet.</span><span class="sxs-lookup"><span data-stu-id="05410-p110">**Note**  In most scenarios, you won't be able to use terms as simple as "AccessToken" as the caching key because your add-in must keep the tokens for different users and SharePoint farms/tenancies distinct. If your add-in uses the  [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), there is special  **CacheKey** provided by SharePoint that can be used to distinguish cached tokens. This section explains what the issues are and what to do when your application is not using the Context Token flow.</span></span>
 

<span data-ttu-id="05410-p111">Das Zwischenspeichern des Zugriffstokens in Sitzungszustand ist für die meisten Szenarien angemessen. Wenn die Remotewebanwendung auf andere Dienste zugreift, die OAuth (zusätzlich zu SharePoint) verwenden und sie die verschiedenen Zugriffstoken im Sitzungsstatus zwischenspeichert, müssen Sie sicherstellen, dass Sie eindeutige Cacheschlüssel für die Token verwenden. Verwenden Sie beispielsweise anstelle von "AccessToken" die Bezeichnungen "SharePoint_AccessToken", "Facebook_AccessToken", "SAP_Gateway_AccessToken" usw. (Wenn Sie keinen Sitzungsstatus oder eine andere Methode zum Zwischenspeichern verwenden, die den jeweiligen Cache aller Benutzer automatisch trennt, müssten Sie auch Ihre Schlüssel für Benutzer relativieren.)</span><span class="sxs-lookup"><span data-stu-id="05410-p111">Caching the access token in session state is fine for most scenarios. If the remote web application is accessing other services that use OAuth (in addition to SharePoint) and it is caching the various access tokens in session state, be sure to use distinct cache keys for the tokens; for example, instead of "AccessToken", use "SharePoint_AccessToken", "Facebook_AccessToken", "SAP_Gateway_AccessToken", etc. . (If you are not using session state or some other caching that automatically separates each user's cache, you would need also to relativize your keys for user.)</span></span>
 

 
<span data-ttu-id="05410-p112">Wenn die Anwendung auf mehrere SharePoint-Farmen oder -Onlinemandanten zugreift, können Sie die SharePoint-Domäne als Teil des primären Cacheschlüssels der Anwendung verwenden ("SharePoint_ *<mydomain>*  .sharepoint.com_AccessToken") oder den Bereich der Farm/des Mandanten benutzen ("SharePoint_ *<realmGUID>*  _AccessToken"), die beide vom Zugriffstoken gelesen werden können. (Ihr Code muss die Base64-Codierung des Tokens umkehren, um es lesen zu können. In verwaltetem Code verfügt die Datei TokenHelper.cs, oder .vb, über Beispielcode für diesen Zweck, der Klassen aus den Namespaces **Microsoft.IdentityModel.S2S.Tokens** und **System.IdentityModel.Tokens** verwendet.) Eine weitere Option steht zur Verfügung, wenn die Anwendung den Kontexttokenablauf wie im folgenden Absatz beschrieben verwendet.</span><span class="sxs-lookup"><span data-stu-id="05410-p112">If the application accesses more than one SharePoint farm or online tenancy, you can use the SharePoint domain as part of the application's primary caching key ("SharePoint_ *<mydomain>*  .sharepoint.com_AccessToken") or use the farm/tenancy's realm ("SharePoint_ *<realmGUID>*  _AccessToken"), both of which can be read from the access token. (Your code needs to reverse the Base 64 encoding of the token to read it. In managed code, the TokenHelper.cs, or .vb, file has sample code for this purpose that uses classes from the **Microsoft.IdentityModel.S2S.Tokens** and **System.IdentityModel.Tokens** namespaces.) There is another option available when the application is using the Context Token flow as described in the next paragraph.</span></span>
 

 
<span data-ttu-id="05410-p113">In einigen Szenarien muss Ihre Anwendung das Zugriffstoken an einem Ort zwischenspeichern, der für die Anwendung über Sitzungen hinweg oder nach Beenden einer Sitzung verfügbar ist. Die Anwendung kann beispielsweise so entworfen sein, dass sie Benutzern ermöglicht, Aktionen zu planen, die durchgeführt werden, nachdem der Benutzer die Anwendung geschlossen hat. Wenn diese Aktionen den Zugriff auf SharePoint beinhalten, muss das Add-In das Zugriffstoken abrufen. In einem solchen Szenario **muss Ihre Anwendung die Zugriffstoken verschiedener Benutzer unterscheiden können**. Wenn Sie den Kontexttokenablauf verwenden, wird für diesen Zweck eine Cacheschlüsselzeichenfolge im Kontexttoken bereitgestellt, das SharePoint an die Remotekomponente Ihrer SharePoint-Add-In übergibt, wenn das Add-In gestartet wird. Weitere Informationen zu diesem **speziellen Cacheschlüssel** und seiner Verwendung finden Sie unter [Überblick über den Cacheschlüssel](#CacheKey). Sie können diese Zeichenfolge auch für das im vorherigen Abschnitt beschriebene Szenario verwenden. Das Planungssystem verfügt über eine Methode, um die erforderlichen Konfigurationsdaten zu speichern, beispielsweise dazu, wann die geplante Aktion ausgeführt wird und was sie bewirken soll. Verwenden Sie diesen Speicher, um den Cacheschlüssel für das Zugriffstoken abzulegen.</span><span class="sxs-lookup"><span data-stu-id="05410-p113">There are some scenarios in which in which your application will need to cache the access token someplace that is available to the application across sessions or after a session ends. For example, the application may be designed to enable users to schedule actions to occur after the user has closed the application. If those actions include accessing SharePoint, then the add-in will need to retrieve the access token. In this kind of scenario,  **your application must keep the access tokens of different users distinct**. If you are using the Context Token flow, a cache key string is provided for this purpose in the context token that SharePoint passes to the remote component of your SharePoint Add-in when the add-in is launched. For more information about this **special cache key** and how to use it, see [Understand the cache key](#CacheKey). You can also use this string for the scenario described in the previous paragraph. The scheduling system will have some means of storing configuration data that it will need, such as when the scheduled work will execute and what it should do. Use this storage to hold the cache key for the access token.</span></span>
 

 
<span data-ttu-id="05410-p114">Wenn der von Ihnen verwendete sitzungsübergreifende Cache auch von mehreren Anwendungen gemeinsam verwendet wird, müssen die Cacheschlüssel für Anwendungen sowie für Benutzer und SharePoint-Bereiche relativiert werden. Der Cacheschlüssel, der im Kontexttoken bereitgestellt wird, ist für Anwendungen sowie für Benutzer und SharePoint-Bereiche eindeutig.</span><span class="sxs-lookup"><span data-stu-id="05410-p114">If the cross-session cache you use is also shared by multiple applications, then the cache keys will have to be relativized to applications as well as to users and to SharePoint realms. The cache key that is provided in the context token is unique to applications as well as users and SharePoint realm.</span></span>
 

 
 <span data-ttu-id="05410-p115">**Wenn Ihre Anwendung den Autorisierungscodeablauf verwendet**, gibt es kein Kontexttoken und damit keinen speziell erstellten Cacheschlüssel. In diesem Fall **müssen Sie ein eigenes System mit Schlüsseln für zwischengespeicherte Daten erstellen**, die je nach potenziellen Namenskonflikten in den vorgesehenen Anwendungsfällen Ihrer Anwendung für eins oder mehrere der folgenden Elemente relativiert werden: den Benutzer, den SharePoint-Bereich und die Anwendung. Sie können für diesen Zweck die Ansprüche im Zugriffstoken verwenden, zum Beispiel **nameId** und **aud** (siehe Tabellen unten). Ihr Code kann einfach die Zeichenfolgen verknüpfen oder sie als Startwert verwenden, um einen eindeutigen Hashwert zu erstellen, der als Cacheschlüssel dienen kann.</span><span class="sxs-lookup"><span data-stu-id="05410-p115">**If your application is using the Authorization Code flow**, then there is no context token and, hence, no specially made cache key. In that scenario, **you will need to create your own system of keys for cached data** that are relativized to one or more of the following depending on what potential name clashes might occur given the use cases of your application: the user, the SharePoint realm, and the application. You can use the claims inside the access token for this purpose; for example, the **nameId** and the **aud** (see the tables below). Your code can simply concatenate the strings or use them as seeds to create a unique hash that can serve as the cache key.</span></span>
 

 
<span data-ttu-id="05410-p116">Wenn Ihre Anwendung schließlich sowohl Aufrufe nur für das Add-In als auch für Benutzer und Add-In an SharePoint durchführt, hat sie zwei verschiedene Zugriffstoken. Also benötigen Sie unterschiedliche Cacheschlüssel. Wenn Sie sich für einen grundlegenden Cacheschlüssel entschieden haben, hängen Sie ihm einfach "_nurapp" oder "_app+benutzer" an.</span><span class="sxs-lookup"><span data-stu-id="05410-p116">Finally, if your application makes both add-in-only and user+add-in calls to SharePoint, then it will have two different access tokens. So, you will need distinct cache keys. Once you have decided on a basic cache key, just append "_add-in-only" or "_add-in+user" to it.</span></span>
 

 

 <span data-ttu-id="05410-p117">**VORSICHT**   **Das Speichern des Zugriffstokens in einem Cookie ist keine sichere Vorgehensweise.** Für gewöhnlich wird als eine bewährte Methode vermieden, das Zugriffstoken über den Browser zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="05410-p117">**Caution**   **It is not a secure practice to store the access token in a cookie.** It is usually a good practice to avoid having the access token pass through the browser.</span></span>
 


### <a name="forward-the-access-token-to-backend-systems"></a><span data-ttu-id="05410-169">Weiterleiten des Zugriffstokens an Back-End-Systeme</span><span class="sxs-lookup"><span data-stu-id="05410-169">Forward the access token to backend systems</span></span>
<span data-ttu-id="05410-170"><a name="ForwardTokenToBackend"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-170"></span></span>

<span data-ttu-id="05410-p118">Ein SharePoint-Add-In hat möglicherweise Back-End-Server, die nicht in derselben Domäne gehostet sind wie die Remotewebanwendung. Wenn ein Back-End-Server CRUD-Vorgänge in SharePoint durchführen muss, zeigt das Add-In eine schnellere Leistung, wenn diese Vorgänge direkt vom Back-End-System zu SharePoint gehen können. Zum Glück ist die Domäne nur wichtig, wenn Ihre Anwendung ein Zugriffstoken von ACS erhält. Wenn sie das Token hat, kann sie es an die Back-End-Dienste weiterleiten und diese können damit SharePoint aufrufen. Code in diesen Systemen muss abgelaufene Zugriffstoken verarbeiten und eine Anforderung für ein neues Token zurück an die übergeordnete Webanwendung senden, die tatsächlich bei ACS registriert ist. Weitere Informationen finden Sie unter  [Handhabung abgelaufener Zugriffstoken](#Expired). Diese Technik sollte nur für die eigenen Back-End-Server Ihrer Anwendung, nicht für externe Webdienste verwendet werden. Außerdem sollten Sie bei Verwendung dieser Technik überlegen, ob Sie die Back-End-Services so entwerfen können, dass sie möglichst immer Nur-Add-In-Aufrufe verwenden.</span><span class="sxs-lookup"><span data-stu-id="05410-p118">a SharePoint Add-in may have backend servers that are not hosted in the same domain as the remote web application. When a backend server needs to perform CRUD operations on SharePoint, the add-in performs faster if these operations can go directly from the backend system to SharePoint. Fortunately, domain is only important when your application is getting an access token from ACS. After it has the token, it can forward it to the backend services and they can call SharePoint by using it. Code in these systems will need to handle expired access tokens and send a request for a new one back to the parent web application that is actually registered with ACS. See  [Handle expired access tokens](#Expired). This technique should only be used for your application's own backend servers, not to external web services. Also, if you are using this technique, consider designing the backend services to use add-in-only calls whenever possible.</span></span>
 

 

### <a name="handle-expired-access-tokens"></a><span data-ttu-id="05410-179">Umgang mit abgelaufenen Zugriffstoken</span><span class="sxs-lookup"><span data-stu-id="05410-179">Handle expired access tokens</span></span>
<span data-ttu-id="05410-180"><a name="Expired"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-180"></span></span>

<span data-ttu-id="05410-p119">Ein Zugriffstoken läuft nach einigen Stunden ab (zwölf Stunden zu dem Zeitpunkt, an dem der Artikel geschrieben wurde, aber das kann sich geändert haben). Wenn die Anwendung immer noch auf SharePoint zugreift, nachdem das Zugriffstoken abgelaufen ist, führt die erste Anforderung an SharePoint nach dem Ablaufzeitpunkt zu einem **401 Unauthorized**-Fehler. Ihr Code muss diese Antwort verarbeiten. Alternativ kann der Code den Ablaufzeitpunkt des Zugriffstokens testen, bevor es verwendet wird. **Ihr Code verwendet das Aktualisierungstoken, um ein anderes Zugriffstoken von ACS abzurufen.** Im Kontexttokenablauf ist das Aktualisierungstoken im Kontexttoken enthalten, das Ihr Add-In zu Beginn der ersten Sitzung mit SharePoint von SharePoint erhält. Im Autorisierungscodeablauf wird es zusammen mit dem ersten Zugriffstoken an die Anwendung übergeben. Ihr Code muss es zwischenspeichern, damit es bei Bedarf verfügbar ist. Das Aktualisierungstoken ist für einige Monate gültig und kann in einem Cookie oder in serverseitigem Speicher beibehalten werden. Weitere Informationen finden Sie unter [Überblick über die Handhabung und das Zwischenspeichern von Aktualisierungstoken](#RefreshTokens).</span><span class="sxs-lookup"><span data-stu-id="05410-p119">An access token expires after a few hours (twelve hours as of the time this article was written, but that can change). If the application is still accessing SharePoint after the access token expires, then the first request to SharePoint after the expiration results in a  **401 Unauthorized** error. Your code has to handle this response. Alternatively, the code can test the expiration time of the access token before it is used. **Your code uses the refresh token to obtain another access token from ACS.** In the Context Token flow, the refresh token is included in the context token that your add-in receives from SharePoint at the start of its first session with SharePoint. In the Authorization Code flow, it is passed to the application along with the first access token. Your code must cache it so it is available when needed. The refresh token lasts a few months and can be persisted in a cookie or in server-side storage. For more information, see [Understand the handling and caching of refresh tokens](#RefreshTokens).</span></span>
 

 

### <a name="see-examples-of-access-tokens"></a><span data-ttu-id="05410-191">Siehe Beispiele für Zugriffstoken</span><span class="sxs-lookup"><span data-stu-id="05410-191">See examples of access tokens</span></span>
<span data-ttu-id="05410-192"><a name="ExampleAccessTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-192"></span></span>

<span data-ttu-id="05410-193">In diesem Abschnitt werden Zugriffstoken anhand von Beispielen beschrieben, und es wird erläutert, wie sie sich je nach der verwendeten Autorisierungsrichtlinie unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="05410-193">This section describes, with examples, access tokens and shows how they differ depending on the authorization policy that is being used.</span></span>
 

 

#### <a name="see-access-tokens-for-the-low-trust-authorization-system"></a><span data-ttu-id="05410-194">Siehe Zugriffstoken für Autorisierungssysteme mit niedriger Vertrauensebene</span><span class="sxs-lookup"><span data-stu-id="05410-194">See access tokens for the low-trust authorization system</span></span>

 <span data-ttu-id="05410-195">**Benutzer-und-Add-In-Richtlinie**</span><span class="sxs-lookup"><span data-stu-id="05410-195">**User+add-in Policy**</span></span>
 

 
<span data-ttu-id="05410-p120">Im Folgenden sehen Sie ein decodiertes **Beispiel für ein Benutzer-und-Add-In-Token, das von ACS** für Aufrufe an SharePoint unter Verwendung der [Benutzer-und-Add-In-Richtlinie](add-in-authorization-policy-types-in-sharepoint.md) erstellt wurde. Zur besseren Lesbarkeit wurden Leerzeichen eingefügt. Das Token entspricht dem [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1)-Protokoll. Das JavaScript Object Notation (JSON)-Objekt im Token wird als „Anspruchssatz“ bezeichnet. Ausführliche Informationen zu den Eigenschaften im Anspruchssatz finden Sie in Tabelle 1. Beachten Sie, dass alle Werte klein geschrieben werden müssen. (Benutzer-und-Add-In-Zugriffscodes sind im [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) und im [Autorisierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) identisch.)</span><span class="sxs-lookup"><span data-stu-id="05410-p120">The following is a decoded  **example of a user+add-in access token generated by ACS** to be used for calls to SharePoint using the [user+add-in policy](add-in-authorization-policy-types-in-sharepoint.md). White space has been added for readability. The token complies with the  [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1) protocol. The JavaScript Object Notation (JSON) object in the token is called theclaim set See table 1 for details about the properties in the claim set. Note that all the values must be lower-case. (User+add-in access tokens are the same in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) and the [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows).)</span></span>
 

 



```
{
 "aud": "00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss": "00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf": 1377549246,
 "exp": 1377592446,
 "nameid": "2303000085ff9abc",
 "actor": "964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73",
 "identityprovider": "urn:federation:microsoftonline"
}
```


<span data-ttu-id="05410-202">**Tabelle 1: Von ACS ausgestellte Benutzer-und-Add-In-Zugriffstoken-Ansprüche**</span><span class="sxs-lookup"><span data-stu-id="05410-202">**Table 1: ACS-issued user+add-in access token claims**</span></span>


|<span data-ttu-id="05410-203">**Anspruch**</span><span class="sxs-lookup"><span data-stu-id="05410-203">**Claim**</span></span>|<span data-ttu-id="05410-204">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="05410-204">**Description**</span></span>|<span data-ttu-id="05410-205">**Entsprechender Wert im Beispiel-Zugriffstoken**</span><span class="sxs-lookup"><span data-stu-id="05410-205">**Corresponding value in the sample access token**</span></span>|
|:-----|:-----|:-----|
| `aud`|<span data-ttu-id="05410-p121">Abkürzung für „audience“ (Zielgruppe), was den Prinzipal bezeichnet, für den das Token vorgesehen ist. Das Format ist _Audience-Prinzipal-ID_/ _SharePoint-Domäne_@ _SharePoint-Bereich_, wobei die _Audience-Prinzipal-ID_ eine dauerhafte Sicherheitsprinzipal-ID für SharePoint ist. (Siehe [Microsoft Product Application Principal Constants](http://msdn.microsoft.com/en-us/library/hh629982%28v=office.12%29.aspx).) Der _SharePoint-Bereich_ ist die GUID des SharePoint Online-Mandanten oder der lokalen SharePoint-Farm, auf die mit dem Zugriffstoken zugegriffen wird. Diese GUID fungiert als die ID des Bereichs für den Tokenaussteller, in diesem Fall Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="05410-p121">Short for "audience", meaning the principal for which the token is intended. The format is  _audience principal ID_/ _SharePoint domain_@ _SharePoint realm_, where  _audience principal ID_ is a permanent security principal ID for SharePoint. (See [Microsoft Product Application Principal Constants](http://msdn.microsoft.com/en-us/library/hh629982%28v=office.12%29.aspx).). _SharePoint realm_ is the GUID of the SharePoint Online tenancy, or the on-premise SharePoint farm, that the access token is used to access. This GUID functions as the realm's ID for the token issuer, in this case Azure ACS.</span></span>|<span data-ttu-id="05410-211">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-211">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `iss`|<span data-ttu-id="05410-p122">Abkürzung für „issuer“ (Aussteller). Dies ist der Prinzipal, der das Token erstellt hat. Das Format ist _Aussteller-GUID_@ _SharePoint-Bereich-GUID_. Im Autorisierungssystem mit niedriger Vertrauensebene ist der Aussteller Azure ACS, und die GUID lautet **00000001-0000-0000-c000-000000000000**.</span><span class="sxs-lookup"><span data-stu-id="05410-p122">Short for "issuer". It represents the principal that created the token. The format is  _Issuer GUID_@ _SharePoint realm GUID_.In the low-trust authorization system, the issuer is Azure ACS and it's GUID is  **00000001-0000-0000-c000-000000000000**.</span></span>|<span data-ttu-id="05410-215">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-215">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `nbf`|<span data-ttu-id="05410-p123">Abkürzung für "not before" (nicht vor). Sie steht für den Zeitpunkt in Sekunden ab dem 1. Januar 1970 um Mitternacht, ab dem das Token  *beginnt*  , gültig zu werden. Standardmäßig wird der Wert auf den Moment festgelegt, in dem das Token erstellt wird. Weitere Informationen finden Sie unter [Arbeiten mit JWT-Zeitwerten](#JWTtimes).  </span><span class="sxs-lookup"><span data-stu-id="05410-p123">Short for "not before". It represents the time at which the token  *starts*  being valid, in seconds since midnight, January 1, 1970. By default, it is set to the moment the token is created. See [Work with JWT time values](#JWTtimes) for more information.</span></span>|<span data-ttu-id="05410-220">1377549246</span><span class="sxs-lookup"><span data-stu-id="05410-220">1377549246</span></span>|
| `exp`|<span data-ttu-id="05410-p124">Abkürzung für „expiration“ (Ablauf). Dies ist der Zeitpunkt, an dem das Token abläuft. Standardmäßig ist das 12 Stunden nach dem **nbf**-Wert. Weitere Informationen finden Sie unter [Arbeiten mit JWT-Zeitwerten](#JWTtimes).</span><span class="sxs-lookup"><span data-stu-id="05410-p124">Short for "expiration". It represents the time the token expires. By default, this is 12 hours after the  **nbf** time. See [Work with JWT time values](#JWTtimes) for more information.</span></span>|<span data-ttu-id="05410-225">1377592446</span><span class="sxs-lookup"><span data-stu-id="05410-225">1377592446</span></span>|
| `nameid`|<span data-ttu-id="05410-p125">Ein eindeutiger Bezeichner für den Benutzer, für den das Token ausgestellt wurde. Das Format variiert je nach Identitätsanbieter. In diesem Beispiel ist der Anbieter Microsoft Online, wäre es jedoch Active Directory, würde die ID folgendermaßen aussehen: "s-1-5-21-2127521184-1604012920-1887927527-415149".</span><span class="sxs-lookup"><span data-stu-id="05410-p125">A unique identifier for the user for whom the token is issued. The format varies depending on the identity provider. In this example, the provider is Microsoft Online, but if it was Active Directory, the ID would look like "s-1-5-21-2127521184-1604012920-1887927527-415149".</span></span>|<span data-ttu-id="05410-229">2303000085ff9abc</span><span class="sxs-lookup"><span data-stu-id="05410-229">2303000085ff9abc</span></span>|
| `actor`|<span data-ttu-id="05410-p126">Der Prinzipal, der Zugriff auf die SharePoint-Farm oder den -Mandanten erlangen möchte. Dieser hat das Format _Client-ID der Anwendung_@ _SharePoint-Bereich_.</span><span class="sxs-lookup"><span data-stu-id="05410-p126">The principal that seeks access to the SharePoint farm or tenancy. It has the form  _Client ID of Application_@ _SharePoint realm_.</span></span>|<span data-ttu-id="05410-232">964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-232">964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `identityprovider`|<span data-ttu-id="05410-p127">Der eindeutige Name des Identitätsanbieters, wie er bei der IANA (Internet Assigned Numbers Authority) registriert ist. Bei einem Add-In, das in SharePoint Online installiert ist, ist der Wert in der Regel der gleiche wie in diesem Beispiel. Bei einem Add-In, das in einer lokalen Farm installiert ist, wäre dies normalerweise ein lokaler Identitätsanbieter, z. B. „urn:office:idp:activedirectory“.</span><span class="sxs-lookup"><span data-stu-id="05410-p127">The unique name of the identity provider as registered with the Internet Assigned Numbers Authority (IANA).For an add-in that is installed to SharePoint Online, the value is usually the same as in this example. For an add-in that is installed to an on-premise farm, it would typically be an on-premise identity provider, such as "urn:office:idp:activedirectory".</span></span>|<span data-ttu-id="05410-235">urn:federation:microsoftonline</span><span class="sxs-lookup"><span data-stu-id="05410-235">urn:federation:microsoftonline</span></span>|
 <span data-ttu-id="05410-236">**Nur-Add-In-Richtlinie**</span><span class="sxs-lookup"><span data-stu-id="05410-236">**add-in-only Policy**</span></span>
 

 
<span data-ttu-id="05410-p128">Im Folgenden sehen Sie ein decodiertes **Beispiel für ein Nur-Add-In-Zugriffstoken, das von ACS** für Aufrufe an SharePoint unter Verwendung der [Nur-Add-In-Richtlinie](add-in-authorization-policy-types-in-sharepoint.md) erstellt wurde. Zur besseren Lesbarkeit wurden Leerzeichen eingefügt. Das Token entspricht dem [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1)-Protokoll. Einzelheiten zu den Eigenschaften im Anspruchssatz finden Sie in Tabelle 2. (Die Nur-Add-In-Richtlinie ist nicht für Anwendungen verfügbar, die den [Autorisierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) verwenden, weil diese nicht über eine Add-In-Manifestdatei verfügen und deshalb keine Berechtigung für die Verwendung von Nur-Add-In-Aufrufen anfordern können.)</span><span class="sxs-lookup"><span data-stu-id="05410-p128">The following is a decoded  **example of an add-in-only access token generated by ACS** to be used for calls to SharePoint using the [add-in-only policy](add-in-authorization-policy-types-in-sharepoint.md). White space has been added for readability. The token complies with the  [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1) protocol. See table 2 for details about the properties in the claim set. (The add-in-only policy is not available for applications that use the [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), because they do not have an add-in manifest file and, thus, cannot request permission to use add-in-only calls.)</span></span>
 

 



```
{
 "aud":"00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf":1403304705,
 "exp":1403347905,
 "nameid":"c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73",
 "sub":"1d47ac31-498b-4988-8aac-85fc9bd2e1ce",
 "oid":"1d47ac31-498b-4988-8aac-85fc9bd2e1ce",
 "trustedfordelegation":"false",
 "identityprovider":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73"
}
```


<span data-ttu-id="05410-242">**Tabelle 2: Von ACS ausgestellte Nur-Add-In-Zugriffstoken-Ansprüche**</span><span class="sxs-lookup"><span data-stu-id="05410-242">**Table 2: ACS-issued add-in-only access token claims**</span></span>


|<span data-ttu-id="05410-243">**Anspruch**</span><span class="sxs-lookup"><span data-stu-id="05410-243">**Claim**</span></span>|<span data-ttu-id="05410-244">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="05410-244">**Description**</span></span>|<span data-ttu-id="05410-245">**Entsprechender Wert im Beispiel-Zugriffstoken**</span><span class="sxs-lookup"><span data-stu-id="05410-245">**Corresponding value in the sample access token**</span></span>|
|:-----|:-----|:-----|
| `aud`|<span data-ttu-id="05410-246">Identisch mit dem oben aufgeführten Benutzer-und-Add-In-Token.</span><span class="sxs-lookup"><span data-stu-id="05410-246">Same as the user+add-in token above.</span></span>|<span data-ttu-id="05410-247">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-247">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `iss`|<span data-ttu-id="05410-248">Wie bei Benutzer-und-Add-In-Token oben.</span><span class="sxs-lookup"><span data-stu-id="05410-248">Same as the user+add-in token above.</span></span>|<span data-ttu-id="05410-249">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-249">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `nbf`|<span data-ttu-id="05410-250">Wie bei Benutzer-und-Add-In-Token oben.</span><span class="sxs-lookup"><span data-stu-id="05410-250">Same as the user+add-in token above.</span></span>|<span data-ttu-id="05410-251">1403304705</span><span class="sxs-lookup"><span data-stu-id="05410-251">1403304705</span></span>|
| `exp`|<span data-ttu-id="05410-252">Wie bei Benutzer-und-Add-In-Token oben.</span><span class="sxs-lookup"><span data-stu-id="05410-252">Same as the user+add-in token above.</span></span>|<span data-ttu-id="05410-253">1403347905</span><span class="sxs-lookup"><span data-stu-id="05410-253">1403347905</span></span>|
| `nameid`|<span data-ttu-id="05410-p129">Ein eindeutiger Bezeichner für das Add-In, anstelle des Benutzers, da die Identität des Benutzers bei der Nur-Add-In-Richtlinie keine Rolle spielt. Das Format ist  _Client-ID_@ _SharePoint-Bereich_.  </span><span class="sxs-lookup"><span data-stu-id="05410-p129">A unique identifier for the add-in, instead of the user, since the user's identity doesn't matter with the add-in-only policy. The format is  _client ID_@ _SharePoint realm_.</span></span>|<span data-ttu-id="05410-256">c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-256">c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `sub`|<span data-ttu-id="05410-p130">Abkürzung für „subject“, den Betreff des Tokens, das der Prinzipal ist, der auf SharePoint zugreifen möchte, in diesem Fall die Remotewebanwendung. Als Wert wird die Objekt-ID verwendet. Siehe den **oid**-Anspruch unten.</span><span class="sxs-lookup"><span data-stu-id="05410-p130">Short for "subject". It is the subject of the token, which is the principal that is seeking access to SharePoint; in this case, the remote web application. The object ID is used for the value. See the  **oid** claim below.</span></span>|<span data-ttu-id="05410-261">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span><span class="sxs-lookup"><span data-stu-id="05410-261">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span></span>|
| `oid`|<span data-ttu-id="05410-p131">Abkürzung für "object ID", also die Objekt-ID in Azure Active Directory für die Remotewebanwendung. In einem Nur-Add-In-Zugriffstoken sind die Betreff- und Objekt-ID ein identischer Wert.</span><span class="sxs-lookup"><span data-stu-id="05410-p131">Short for "object ID". It is the object ID in Azure Active Directory for the remote web application. In an add-in-only access token, the subject and object ID are the same value.</span></span>|<span data-ttu-id="05410-265">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span><span class="sxs-lookup"><span data-stu-id="05410-265">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span></span>|
| `trustedfordelegation`|<span data-ttu-id="05410-p132">Ein boolescher Wert, der angibt, ob SharePoint der SharePoint-Add-In vertrauen sollte, dass sie den Benutzer authentifiziert und autorisiert. In Nur-Add-In-Aufrufen ist der Wert auf "false" festgelegt, da die Benutzeridentität keine Rolle spielt.</span><span class="sxs-lookup"><span data-stu-id="05410-p132">A Boolean value that specifies whether SharePoint should trust the SharePoint Add-in to authenticate and authorize the user. It is false in add-in-only calls because the user identity doesn't matter.</span></span>|<span data-ttu-id="05410-268">false</span><span class="sxs-lookup"><span data-stu-id="05410-268">false</span></span>|
| `identityprovider`|<span data-ttu-id="05410-p133">Der eindeutige Name des Identitätsanbieters. Da es sich um das Add-In und nicht um einen Benutzer handelt, deren Identität bereitgestellt wird, ist ACS der Identitätsanbieter. Das Format ist  _ACS-GUID_@ _SharePoint-Bereich_.  </span><span class="sxs-lookup"><span data-stu-id="05410-p133">The unique name of the identity provider. Since it is the add-in, rather than a user, whose identity is being provided, ACS is the identity provider. The format is  _ACS GUID_@ _SharePoint realm_.</span></span>|<span data-ttu-id="05410-272">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-272">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|

## <a name="understand-the-structure-and-handling-of-context-tokens"></a><span data-ttu-id="05410-273">Grundlegendes zur Struktur und der Handhabung von Kontexttoken</span><span class="sxs-lookup"><span data-stu-id="05410-273">Understand the structure and handling of context tokens</span></span>
<span data-ttu-id="05410-274"><a name="ContextTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-274"></span></span>

<span data-ttu-id="05410-p134">Ein Kontexttoken wird nur im  [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) des Autorisierungssystems mit niedriger Vertrauensebene verwendet. **Wenn die SharePoint-Add-In in SharePoint gestartet wird, fordert SharePoint an, dass Azure ACS ein Kontexttoken erstellt, das SharePoint dann an die Remotekomponente der SharePoint-Add-In übergibt.** Das Token wird als ausgeblendeter Parameter namens **SPAppToken** in einer Anforderung von SharePoint für die Startseite der Remotekomponente übergeben. Das Token wird mit einem geheimen Clientschlüssel signiert, der nur ACS und der SharePoint-Add-In bekannt ist. Das **Kontexttoken enthält ein Aktualisierungstoken, das das Add-In**, zusammen mit anderen Informationen aus dem Kontexttoken, **verwendet, um ein Zugriffstoken** von ACS anzufordern. (Zum Zeitpunkt, an dem dieser Artikel geschrieben wurde, hatten von ACS ausgestellte Kontexttoken für SharePoint eine Lebensspanne von 12 Stunden, das kann sich aber geändert haben.) Die **Hauptaufgaben für den Code in der SharePoint-Add-In** sind die folgenden:</span><span class="sxs-lookup"><span data-stu-id="05410-p134">A context token is used only in the  [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) of the low-trust authorization system. **When the SharePoint Add-in is launched in SharePoint, SharePoint requests that Azure ACS create a context token that SharePoint then passes on to the remote component of the SharePoint Add-in.** The token is passed as a hidden form parameter called **SPAppToken** in a request from SharePoint for the start page of the remote component. The token is signed with a client secret known only to ACS and the SharePoint Add-in. The **context token includes a refresh token that the add-in uses**, along with other information from the context token, **to request an access token** from ACS. (When this article was written, ACS-issued context tokens for SharePoint had a life span of 12 hours, but that could change.) The **main tasks for the code in the SharePoint Add-in** are the following:</span></span>
 

 

- <span data-ttu-id="05410-281">Verwenden Sie den geheimen Clientschlüssel des Add-Ins, um **das Kontexttoken zu validieren**.</span><span class="sxs-lookup"><span data-stu-id="05410-281">Use the client secret of the add-in to  **validate the context token**.</span></span>
    
 
-  <span data-ttu-id="05410-282">**Zwischenspeichern Sie das Kontexttoken**, oder extrahieren Sie das Aktualisierungstoken und andere Elemente daraus, und zwischenspeichern Sie diese separat.</span><span class="sxs-lookup"><span data-stu-id="05410-282">**Cache the context token** or extract, and separately cache, the refresh token and certain other items from inside it.</span></span>
    
 
- <span data-ttu-id="05410-283">Verwenden Sie das Aktualisierungstoken und andere Informationen, um **ein Zugriffstoken** von ACS anzufordern (das dann selbst zwischengespeichert wird).</span><span class="sxs-lookup"><span data-stu-id="05410-283">Use the refresh token and other information to  **request an access token** from ACS (which is itself then cached).</span></span>
    
 
-  <span data-ttu-id="05410-284">**Zwischenspeichern Sie den CacheKey** aus dem Kontexttoken.</span><span class="sxs-lookup"><span data-stu-id="05410-284">**Cache the CacheKey** from the context token.</span></span>
    
 

 <span data-ttu-id="05410-p135">**Wichtig** Die ersten beiden Aufgaben müssen durchgeführt werden, bevor der Benutzer zu einer anderen Seite navigiert oder die Seite aktualisiert, da sonst das Token verloren geht. Ziehen Sie beispielsweise bei einer ASP.NET-Web Forms-Anwendung in Betracht, diese Aufgaben in der **Page_Load**-Methode durchzuführen (in einem Bedingungscodeblock, der nur ausgeführt wird, wenn die Anforderung kein Postback ist). Bei einer ASP.NET-MVC-Anwendung können Sie diese Aufgaben in der Standardcontrollermethode durchführen.</span><span class="sxs-lookup"><span data-stu-id="05410-p135">**Important**  The first two tasks must occur before the user navigates to another page or refreshes the page or the token is lost. For example, in an ASP.NET web forms application, consider doing those tasks in the  **Page_Load** method (in a conditional code block that runs only when the request is not a postback). In an ASP.NET MVC application, consider doing these tasks in the default controller method.</span></span>
 

<span data-ttu-id="05410-p136">Wenn Sie verwalteten Code verwenden, befindet sich Beispielcode für einige dieser Aufgaben in den Dateien SharePointContext.cs (oder .vb) und TokenHelper.cs (oder .vb), die in Microsoft Office-Entwicklertools für Visual Studio enthalten sind. Sie müssen nur einfache Aufrufe an die Mitglieder der TokenHelper-Klasse durchführen. Ihr Code kann die erste Aufgabe beispielsweise mit der folgenden einzelnen Codezeile durchführen:</span><span class="sxs-lookup"><span data-stu-id="05410-p136">If you are using managed code, sample code for some of these tasks is in the SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb) files that are included in Microsoft Office Developer Tools for Visual Studio. You just need to make simple calls to the members of the TokenHelper class. For example, your code can do the first task with the following single line of code:</span></span>
 

 



```C#
SharePointContextToken contextToken =
    TokenHelper.ReadAndValidateContextToken(contextTokenString, 
    Request.Url.Authority);
```

<span data-ttu-id="05410-291">Ein Beispiel, wie Sie einige dieser Aufgaben mit PHP erledigen können, finden im Beispiel  [SharePoint: Durchführen von Vorgängen in der SharePoint-Dokumentbibliothek von einer PHP-Website](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef).</span><span class="sxs-lookup"><span data-stu-id="05410-291">For an example of how to do some of these tasks with PHP, see the sample  [SharePoint: Perform operations on SharePoint Document Library from PHP site](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef).</span></span>
 

 

### <a name="cache-the-context-token-or-parts-of-it"></a><span data-ttu-id="05410-292">Zwischenspeichern des Kontexttokens oder Teile davon</span><span class="sxs-lookup"><span data-stu-id="05410-292">Cache the context token or parts of it</span></span>
<span data-ttu-id="05410-293"><a name="CacheContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-293"></span></span>

<span data-ttu-id="05410-p137">Sie können ganze Kontexttoken oder nur das Aktualisierungstoken und bestimmte andere darin enthaltene Elemente, die Ihr Code verwendet, um Zugriffstoken abzurufen **zwischenspeichern**, entweder **in serverseitigem oder in clientseitigem Speicher**. Zu Zwecken der Einfachheit wird in diesem Artikel davon ausgegangen, dass Sie das Kontexttoken als Einheit zwischenspeichern.</span><span class="sxs-lookup"><span data-stu-id="05410-p137">You can  **cache** whole context token, or just the refresh token and certain other items that are inside it that your code uses to get access tokens, **in either server-side or client-side storage**. For simplicity, this article assumes that you cache the context token as a unit.</span></span>
 

 

 <span data-ttu-id="05410-p138">**Wichtig** Wir erinnern Sie noch einmal, weil es wirklich wichtig ist: Verwenden Sie keinen clientseitigen Cache für das *Zugriffstoken*. Dieser ist nur für das Kontexttoken sicher.</span><span class="sxs-lookup"><span data-stu-id="05410-p138">**Important**  We remind you one more time because it's really important: do not use client-side caching for the  *access*  token. It is safe to use it only for the context token.</span></span>
 

<span data-ttu-id="05410-p139">Sie haben dieselben  [serverseitigen Cacheoptionen](#CacheAccessToken) wie oben für das Zugriffstoken aufgeführt. Zu den clientseitigen Optionen zählen ein Cookie und ein ausgeblendetes Formularfeld auf einer HTML-Seite. Eine weitere Option besteht darin, das Kontexttoken im Sitzungscache zu speichern, aber speichern Sie dann den daraus abgerufenen **Cacheschlüssel** auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="05410-p139">You have the same  [server-side caching options](#CacheAccessToken) for as are listed above for the access token. Client-side options include a cookie and a hidden form field on an HTML page. Another option is to store the context token in the session cache, but store the **CacheKey** obtained from inside it on the client.</span></span>
 

 
<span data-ttu-id="05410-p140">Wenn Ihre Anwendung auf SharePoint zugreift, nachdem eine Sitzung beendet wurde, sind weder der Sitzungscache noch der clientseitige Cache eine Option, weil das Aktualisierungstoken für die Anwendung verfügbar sein muss, falls das Originalzugriffstoken abgelaufen ist, während die Aufgaben nach der Sitzung ausgeführt werden. In diesem Szenario benötigen Sie einen dauerhaften (sitzungsübergreifenden) Cache, der von mehreren Benutzern und/oder SharePoint-Bereichen und/oder Anwendungen gemeinsam verwendet wird. Ihr Code muss also Cacheschlüssel verwenden, die Benutzer, SharePoint-Bereich und/oder Anwendung unterscheiden, wie weiter oben unter [Zwischenspeichern des Zugriffstokens](#CacheAccessToken) beschrieben. Sie können für diesen Zweck **den speziellen Cacheschlüssel verwenden**, der sich im Kontexttoken befindet, so wie Sie ihn für das Zugriffstoken verwendet haben. (Siehe [Überblick über den Cacheschlüssel](#CacheKey) weiter unten.)</span><span class="sxs-lookup"><span data-stu-id="05410-p140">If your application accesses SharePoint after a session is ended, then neither session-caching nor client-side caching is an option, because the refresh token must be available to the application in case the original access token has expired when the post-session work executes. In this scenario, you need a durable (cross-session) cache that is shared by multiple users and/or SharePoint realms and/or applications. So, your code has to use cache keys that distinguish user, SharePoint realm, and/or application as explained above in  [Cache the access token](#CacheAccessToken). You can  **use the special cache key** that is inside the context token for this purpose just as you used it for the access token. (See [Understand the cache key](#CacheKey) below.)</span></span>
 

 

#### <a name="understand-the-cache-key"></a><span data-ttu-id="05410-306">Grundlegendes zum Cacheschlüssel</span><span class="sxs-lookup"><span data-stu-id="05410-306">Understand the cache key</span></span>
<span data-ttu-id="05410-307"><a name="CacheKey"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-307"></span></span>

 <span data-ttu-id="05410-p141">**Der Cacheschlüssel ist eine opake Zeichenfolge, die für die Kombination aus Benutzer, Benutzernamenaussteller, Add-In und SharePoint-Farm oder SharePoint Online-Mandant eindeutig ist.** Bevor er verschlüsselt wird, hat er die folgende Form, wobei _Bereich_ die GUID der lokalen SharePoint-Farm oder des SharePoint Online-Mandanten ist.</span><span class="sxs-lookup"><span data-stu-id="05410-p141">**The cache key is an opaque string that is unique to the combination of user, user name issuer, add-in, and SharePoint farm or SharePoint Online tenant.** Before it is encrypted, it has the following form, where _Realm_ is the GUID of the on-premise SharePoint farm or the SharePoint Online tenancy.</span></span>
 

 
 <span data-ttu-id="05410-310">_UserNameId_ + "," + _UserNameIdIssuer_ + "," + _ApplicationId_ + "," + _Realm_</span><span class="sxs-lookup"><span data-stu-id="05410-310">_UserNameId_ + "," + _UserNameIdIssuer_ + "," + _ApplicationId_ + "," + _Realm_</span></span>
 

 
<span data-ttu-id="05410-p142">Der Cacheschlüssel enthält keine Website-URL-Informationen. Jeder SharePoint Online-Mandant (oder jede lokale SharePoint-Farm) hat einen eindeutigen Bereich, deshalb ist der Cacheschlüssel für jede Kombination aus Benutzername, Benutzernamenaussteller, Anwendung und Farm eindeutig. Im Beispielkontexttoken unten sieht der Wert für den verschlüsselten Cacheschlüssel wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="05410-p142">The cache key does not contain site URL information. Each SharePoint Online tenant (or on-premise SharePoint farm) has a unique realm, so, the cache key is unique for each combination of user name, user name issuer, application, and farm. In the example context token below, the encrypted cache key value is:</span></span>
 

 
 `KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=`
 

 
<span data-ttu-id="05410-p143">Da Ihre Anwendung möglicherweise mehrere Elemente zwischenspeichert, zum Beispiel sowohl das Zugriffstoken als auch das Kontexttoken im selben Cache mit demselben Cacheschlüssel, sollten Sie **in Betracht ziehen, den Cacheschlüssel als Stamm zu verwenden** und dann eine bestimmte Zeichenfolge wie "AccessToken" oder "ContextToken" nach Bedarf anzuhängen oder voranzustellen, um einen vollständigen Cacheschlüssel zu bilden. **Eine weitere Option besteht darin, eine Klasse zu erstellen**, die Eigenschaften für die verschiedenen Dinge enthält, die Sie zwischenspeichern möchten, und dann ein Objekt dieses Typs zwischenzuspeichern. Eine **dritte Option**, zumindest wenn Sie **eine Datenbank als Cache verwenden**, besteht darin, eine Tabelle mit einer Spalte für den Cacheschlüssel und weiteren Spalten für die zwischengespeicherten Elemente (Zugriffstoken, Kontexttoken usw.) zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="05410-p143">Since your application may be caching multiple items, such as both the access token and the context token in the same cache with the same cache key,  **consider using the cache key as a stem** and either appending or prepending a specific string such as "AccessToken" or "ContextToken" to it as needed to form a complete cache key. **Another option is to create a class** with properties for the various things you want to cache and then cache an object of that type. A **third option**, if you are **using a database** as a cache, is to use a table with a CacheKey column and additional columns for the cached items (AccessToken, ContextToken, etc.).</span></span>
 

 
<span data-ttu-id="05410-p144">Ihre Anwendung muss natürlich nicht denselben Cache für alles verwenden, was sie zwischenspeichert. Ein typisches Muster ist, das Zugriffstoken im Sitzungscache, das Kontexttoken (oder das daraus stammende Aktualisierungstoken) in einer Datenbank und den Cacheschlüssel in einem Cookie zwischenzuspeichern.</span><span class="sxs-lookup"><span data-stu-id="05410-p144">Your application does not have to use the same cache for everything it is caching, of course. A common pattern is to cache the access token in session cache, the context token (or the refresh token from inside it) in a database, and the CacheKey in a cookie.</span></span>
 

 

### <a name="use-the-context-token-to-get-an-access-token"></a><span data-ttu-id="05410-319">Verwenden des Kontexttokens zum Abrufen eines Zugriffstokens</span><span class="sxs-lookup"><span data-stu-id="05410-319">Use the context token to get an access token</span></span>
<span data-ttu-id="05410-320"><a name="UseContextTokenToGetAccessToken"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-320"></span></span>

 <span data-ttu-id="05410-p145">**Um ein Zugriffstoken zu erhalten, sendet Ihre Anwendung eine Anforderung direkt an ACS.** Die Anforderung enthält drei Informationen, die aus dem Kontexttoken (und anderen Informationen) extrahiert werden:</span><span class="sxs-lookup"><span data-stu-id="05410-p145">**To get an access token, your application sends a request directly to ACS.** The request includes three pieces of information that are extracted from the context token (and other information):</span></span>
 

 

- <span data-ttu-id="05410-323">Das Aktualisierungstoken</span><span class="sxs-lookup"><span data-stu-id="05410-323">The refresh token</span></span>
    
 
- <span data-ttu-id="05410-324">Die Anwendungsprinzipal-GUID von SharePoint</span><span class="sxs-lookup"><span data-stu-id="05410-324">The application principal GUID of SharePoint.</span></span>
    
 
- <span data-ttu-id="05410-325">Die Bereich-GUID der SharePoint-Farm oder des SharePoint Online-Mandanten, auf die bzw. den das Add-In Zugriff erlangen möchte.</span><span class="sxs-lookup"><span data-stu-id="05410-325">The realm GUID of the SharePoint farm or SharePoint Online tenancy to which the add-in is seeking access.</span></span>
    
 
<span data-ttu-id="05410-p146">Die Datei TokenHelper.cs (oder .vb) enthält Code, der diese Anforderung erstellt. Einen Beispiel-PHP-Code für diese Aufgabe finden Sie unter  [SharePoint: Durchführen von Vorgängen in der SharePoint-Dokumentbibliothek von einer PHP-Website](http://code.msdn.microsoft.com/office/SharePoint-Perform-8a78b8ef/sourcecode?fileId=117521&amp;pathId=1932320454).</span><span class="sxs-lookup"><span data-stu-id="05410-p146">The TokenHelper.cs (or .vb) file has code that creates this request. For an example of PHP code that does this, see  [SharePoint: Perform operations on SharePoint Document Library from PHP site](http://code.msdn.microsoft.com/office/SharePoint-Perform-8a78b8ef/sourcecode?fileId=117521&amp;pathId=1932320454).</span></span>
 

 
<span data-ttu-id="05410-p147">Die Anwendung kann den Bereich des SharePoint-Mandanten oder der Farm während der Laufzeit erhalten statt ihn aus dem Kontexttoken zu analysieren. Wenn Sie verwalteten Code verwenden, gibt es eine  `TokenHelper.GetRealmFromTargetUrl`-Methode, um den Bereich abzurufen. Stellen Sie sicher, dass Sie den Wert zwischenspeichern, damit Ihr Code nicht einen weiteren Netzwerkaufruf durchführt, um ihn erneut abzurufen.</span><span class="sxs-lookup"><span data-stu-id="05410-p147">The application can get the realm of the SharePoint tenancy or farm at runtime as an alternative to parsing it from the context token. If you are using managed code, there is a  `TokenHelper.GetRealmFromTargetUrl` method to get the realm. Be sure to cache the value so that your code does not make another network call to get it again.</span></span>
 

 

### <a name="get-a-new-context-token"></a><span data-ttu-id="05410-331">Abrufen eines neuen Kontexttokens</span><span class="sxs-lookup"><span data-stu-id="05410-331">Get a new context token</span></span>
<span data-ttu-id="05410-332"><a name="GetNewContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-332"></span></span>

 <span data-ttu-id="05410-p148">**Wenn Sie ein neues Kontexttoken benötigen**, normalerweise weil das Aktualisierungstoken (das in Kontexttoken enthalten ist) abgelaufen ist **, kann Ihr Code ein neues Token abrufen, indem er den Browser auf eine spezielle Seite auf jeder SharePoint-Website** umleitet: AppRedirect.aspx. Sie müssen zwei Abfrageparameter an die URL dieser Seite anhängen:</span><span class="sxs-lookup"><span data-stu-id="05410-p148">**If you need a new context token**, typically because the refresh token (which are contained in context tokens) has expired, **your code can get a new one by redirecting the browser to a special page in every SharePoint website** -- AppRedirect.aspx. Two query parameters have to be attached to the URL of this page:</span></span>
 

 

-  <span data-ttu-id="05410-335">`client_id`: Die Client-ID Ihres SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="05410-335">`client_id`: The client ID of your SharePoint Add-in.</span></span>
    
 
-  <span data-ttu-id="05410-p149">`redirect_uri`: Der URI, an den der Browser umgeleitet werden soll, nachdem das neue Kontexttoken abgerufen wurde. SharePoint fügt das Kontexttoken in diesen URI ein. Normalerweise ist das dieselbe Seite, Contollermethode oder Webdienstmethode, die das neue Kontexttoken angefordert hat. Der Wert muss URL-codiert sein.</span><span class="sxs-lookup"><span data-stu-id="05410-p149">`redirect_uri`: The URI to which you want the browser redirected after the new context token is obtained. SharePoint will POST the context token to this URI. Typically, this is the same page, controller method, or web service method that requested the new context token. The value must be URL-encoded.</span></span>
    
 
<span data-ttu-id="05410-340">Nachfolgend ist die Struktur der URL dargestellt:</span><span class="sxs-lookup"><span data-stu-id="05410-340">The following shows the structure of the URL:</span></span>
 

 



```
https://<SharePointDomain> /_layouts/15/appredirect.aspx?client_id=<app_client_GUID> &amp;redirect_uri=<URL-encoded_redirect_URI>
```

<span data-ttu-id="05410-341">Im Folgenden finden Sie ein Beispiel für die Durchführung der Anforderung in ASP.NET, bei der die TokenHelper-Datei verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="05410-341">The following is an example of making the request in ASP.NET that uses the TokenHelper file:</span></span>
 

 



```
Response.Redirect(TokenHelper.GetAppContextTokenRequestUrl(sharePointUrl, Server.UrlEncode(Request.Url.ToString())));
```


### <a name="see-an-example-of-a-context-token"></a><span data-ttu-id="05410-342">Beispiel für ein Kontexttoken</span><span class="sxs-lookup"><span data-stu-id="05410-342">See an example of a context token</span></span>
<span data-ttu-id="05410-343"><a name="ExampleContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-343"></span></span>

<span data-ttu-id="05410-p150">Im Folgenden sehen Sie ein Beispiel für ein Kontexttoken. Das kleine JavaScript Object Notation (JSON)-Objekt im oberen Bereich enthält Metadaten zum Token. Die Eigenschaften sind dieselben wie bei Zugriffstoken (siehe oben). Der Wert der Eigenschaft **alg** ist der Name des Algorithmus, der für die Erzeugung der Signatur verwendet wird, die ACS an das Token anhängt. Details zu den Eigenschaften in der Nutzlast des Tokens finden Sie in Beispiel 3. Beachten Sie, dass alle Werte kleingeschrieben werden müssen. (Zur besseren Lesbarkeit wurden Leerzeichen eingefügt.)</span><span class="sxs-lookup"><span data-stu-id="05410-p150">The following is an example of a context token. The small JavaScript Object Notation (JSON) object at the top contains metadata about the token. These properties are the same as in access tokens (see above). The value of the  **alg** property is the name of the algorithm that is used to generate the signature that ACS appends to the token. See table 3 for details about the properties in the payload of the token. Note that all the values must be lower-case. (White space has been added for readability.)</span></span>
 

 

```
{"typ":"JWT","alg":"HS256"}
.
{
 "aud":"a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf":"1335822895",
 "exp":"1335866095",
 "appctxsender":"00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "appctx":"{
            \"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\",
            \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"
           }",
 "refreshtoken":"IAAAAC1Lv5w0OrcFAmJx0xk6aaBdhgsw3VPnPzNEDAWypTHtCYytZ2/dBBUKj+HLK8YB3IUCUfDxYpAque
NHKtgs4rYJJ5AegQpNMOJR1yYK8ngivQx0oetj7aSPuGVb+k6at6G0Kx5LZ5vhxkAq8iUSwu8p4L2cvNMzDF1mDKfMivqxgrIZkr2nbf9as0SJFL6VG5hZnDE4HKq
xJnejSW3umatKM4fsfY1MClVCxrkXb2EQ8H/TmwaJc388YW063GEVUS/3BTSgSIRBKQUmXJuJ6BZY7WTm84LaGrx3mIjnUTM/jnqPoPG55JbCC9sS/MeGNPtzPPCDg
6Vv7dVhQ1Dq5Y3fQ65e9LpJ580jCgzYYvpIFT+Wx5V+17mjY2T8wug04K2ts87Znsr+GfFCorf7NS/lj5HjoxRAQ2tva/8dwguSLwxcUwi/Q9MbpR0NNtlpwVazqi9O
hJ4Df7gVhUDdJ0Dtc6aFCPbl5ZLDDRs42xK2", 
 "isbrowserhostedapp": "true"
}
```

<span data-ttu-id="05410-p151">Die Ansprüche **aud**, **iss**, **nbf** und **exp** sind exakt die gleichen wie bei einem Zugriffstoken und sind weiter oben erläutert. Die Ansprüche **appctxsender**, **appctx**, **CacheKey**, **SecurityTokenServiceUri**, **refreshtoken** und **isbrowserhostedapp** werden in der folgenden Tabelle beschrieben.</span><span class="sxs-lookup"><span data-stu-id="05410-p151">The  **aud**, **iss**, **nbf**, and **exp** claims are exactly the same as in an access token as described above. The **appctxsender**, **appctx**, **CacheKey**, **SecurityTokenServiceUri**, **refreshtoken**, and **isbrowserhostedapp** claims are described in the following table.</span></span>
 

 

<span data-ttu-id="05410-353">**Tabelle 3: Kontexttokenansprüche und -informationen**</span><span class="sxs-lookup"><span data-stu-id="05410-353">**Table 3. Context token claims and information**</span></span>


|<span data-ttu-id="05410-354">** **Anspruch****</span><span class="sxs-lookup"><span data-stu-id="05410-354">** **Claim****</span></span>|<span data-ttu-id="05410-355">** **Beschreibung****</span><span class="sxs-lookup"><span data-stu-id="05410-355">** **Description****</span></span>|<span data-ttu-id="05410-356">**.**Entsprechender Wert im Beispielkontexttoken****</span><span class="sxs-lookup"><span data-stu-id="05410-356">** **Corresponding value in sample context token****</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="05410-357">aud</span><span class="sxs-lookup"><span data-stu-id="05410-357">aud</span></span>||<span data-ttu-id="05410-358">a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-358">a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="05410-359">iss</span><span class="sxs-lookup"><span data-stu-id="05410-359">iss</span></span>||<span data-ttu-id="05410-360">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-360">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="05410-361">nbf</span><span class="sxs-lookup"><span data-stu-id="05410-361">nbf</span></span>||<span data-ttu-id="05410-362">1335822895</span><span class="sxs-lookup"><span data-stu-id="05410-362">1335822895</span></span>|
|<span data-ttu-id="05410-363">exp</span><span class="sxs-lookup"><span data-stu-id="05410-363">exp</span></span>||<span data-ttu-id="05410-364">1335866095</span><span class="sxs-lookup"><span data-stu-id="05410-364">1335866095</span></span>|
|<span data-ttu-id="05410-365">appctxsender</span><span class="sxs-lookup"><span data-stu-id="05410-365">appctxsender</span></span>|<span data-ttu-id="05410-p152">Kurz für „application context sender“ (Absender des Anwendungskontexts). Dies stellt die Anwendung dar, die das Kontexttoken an das SharePoint-Add-In gesendet hat. Sie hat das Format _GUID des Prinzipals_@ _SharePoint-Bereich_, wobei _GUID des Prinzipals_ die konstante ID des Anwendungsprinzipals ist; entweder SharePoint, Exchange 2013, Lync 2013 oder Workflow.</span><span class="sxs-lookup"><span data-stu-id="05410-p152">Short for "application context sender". It represents the application that sent the context token to the SharePoint Add-in.It has the form  _GUID of principal_@ _SharePoint realm_, where  _GUID of principal_ is the constant ID of the application principal; either SharePoint, Exchange 2013, Lync 2013, or Workflow.</span></span>|<span data-ttu-id="05410-368">00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="05410-368">00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="05410-369">appctx</span><span class="sxs-lookup"><span data-stu-id="05410-369">appctx</span></span>|<span data-ttu-id="05410-p153">Abkürzung für „add-in context“ (Add-In-Kontext), ein JSON-Objekt, das **CacheKey** und **SecurityTokenServiceURI** enthält.</span><span class="sxs-lookup"><span data-stu-id="05410-p153">Short for "add-in context". It is a JSON object that contains the  **CacheKey** and **SecurityTokenServiceURI**.</span></span>|<span data-ttu-id="05410-372">\"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\", \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"</span><span class="sxs-lookup"><span data-stu-id="05410-372">\"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\", \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"</span></span>|
|<span data-ttu-id="05410-373">CacheKey</span><span class="sxs-lookup"><span data-stu-id="05410-373">CacheKey</span></span>|<span data-ttu-id="05410-p154">Ein eindeutiger Wert, der als Schlüssel in jedem nach Schlüssel/Wert strukturierten Cache verwendet werden kann, um das Kontexttoken zu speichern und abzurufen. Er kann auch als Wert einer Schlüsselspalte in einer Zeile einer Datenbank verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="05410-p154">A unique value that can be used as the key in any key/value structured cache to store and retrieve the context token. It could also be used as the value of a key column in a row of a database.</span></span>|<span data-ttu-id="05410-376">KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=</span><span class="sxs-lookup"><span data-stu-id="05410-376">KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=</span></span>|
|<span data-ttu-id="05410-377">SecurityTokenServiceURI</span><span class="sxs-lookup"><span data-stu-id="05410-377">SecurityTokenServiceURI</span></span>|<span data-ttu-id="05410-378">Der URI des tokenausstellenden Diensts.</span><span class="sxs-lookup"><span data-stu-id="05410-378">The URI of the token issuing service.</span></span>|<span data-ttu-id="05410-379">https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2</span><span class="sxs-lookup"><span data-stu-id="05410-379">https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2</span></span>|
|<span data-ttu-id="05410-380">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="05410-380">refreshtoken</span></span>|<span data-ttu-id="05410-381">Das Aktualisierungstoken für das Add-In.</span><span class="sxs-lookup"><span data-stu-id="05410-381">The refresh token for the add-in.</span></span>|<span data-ttu-id="05410-382">IAAAAC1Lv5w0OrcFAmJx0xk6???</span><span class="sxs-lookup"><span data-stu-id="05410-382">IAAAAC1Lv5w0OrcFAmJx0xk6???</span></span>|
|<span data-ttu-id="05410-383">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="05410-383">isbrowserhostedapp</span></span>|<span data-ttu-id="05410-384">Ein **Boolean**-Feld, in dem angegeben wird, ob die Anforderung an das Add-In, das das Kontexttoken enthält, von einem Browser (true) oder von einem Remoteereignisempfänger (false) kommt</span><span class="sxs-lookup"><span data-stu-id="05410-384">A  **Boolean** field that specifies whether the request to the add-in that contains the context token is coming from a browser (true) or from a remote event receiver (false).</span></span>|<span data-ttu-id="05410-385">true</span><span class="sxs-lookup"><span data-stu-id="05410-385">true</span></span>|

### <a name="use-the-context-token-to-limit-access-to-only-sharepoint-users"></a><span data-ttu-id="05410-386">Verwenden des Kontexttokens, um den Zugriff auf SharePoint-Benutzer zu beschränken</span><span class="sxs-lookup"><span data-stu-id="05410-386">Use the context token to limit access to only SharePoint users</span></span>
<span data-ttu-id="05410-387"><a name="UseContextTokenToLimitAccess"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-387"></span></span>

<span data-ttu-id="05410-p155">Wenn Sie den Zugriff auf Ihre Remotekomponente wie einen WCF-Dienst auf SharePoint-Benutzer einschränken möchten, kann Ihr Code einfach das Kontexttoken in der HTTP-Anforderung validieren. (Wenn Sie verwalteten Code verwenden, können Sie einfach **TokenHelper.ReadAndValidateContextToken()** aufrufen.) Ihr Code kann überprüfen, ob der Akteuranspruch mit **00000003-0000-0ff1-ce00-000000000000** beginnt, wenn Sie sicherstellen möchten, dass es sich um SharePoint handelt (und z. B. nicht um Exchange 2013, Lync 2013 oder Workflow). Wenn Sie eine zusätzliche Validierung durchführen möchten, für die ein Rückruf an SharePoint erforderlich ist, beispielsweise um den Zugriff auf Benutzer mit einer bestimmten Rolle in SharePoint einzuschränken, können Sie die Tatsache, dass Sie diese Validierung für einen bestimmten Benutzer durchgeführt haben, zwischenspeichern (indem Sie den **CacheKey** des Kontexttokens verwenden), damit Sie dies nur einmal durchführen müssen.</span><span class="sxs-lookup"><span data-stu-id="05410-p155">If you want to limit access to your remote component, such as a WCF service, to SharePoint users, your code can simply validate the context token in the HTTP Request. (If you are using managed code, you can just call  **TokenHelper.ReadAndValidateContextToken()**). Your code can verify that the actor claim of the token starts with  **00000003-0000-0ff1-ce00-000000000000**, if you want to make sure that it is SharePoint (and not, for example, Exchange 2013, Lync 2013, or Workflow). If you want to do additional validation that requires a call back to SharePoint, such as limiting access to users with a certain role in SharePoint, you can cache the fact that you have done this validation for a particular user (by using the context token's **CacheKey**) so that you have to do this only once.</span></span>
 

 

## <a name="understand-the-handling-and-caching-of-refresh-tokens"></a><span data-ttu-id="05410-392">Grundlegendes zur Handhabung und zum Zwischenspeichern Aktualisierungstoken</span><span class="sxs-lookup"><span data-stu-id="05410-392">Understand the handling and caching of refresh tokens</span></span>
<span data-ttu-id="05410-393"><a name="RefreshTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-393"></span></span>

 <span data-ttu-id="05410-p156">**Ein Aktualisierungstoken ist im Kontexttoken enthalten, das SharePoint an Ihre Webanwendung veröffentlicht, wenn sie gestartet wird.** Das Aktualisierungstoken ist ein verschlüsseltes Token, das Ihre SharePoint-Add-In nicht entschlüsseln kann. **Ihr Code verwendet es**, zusammen mit anderen Informationen, **um ein neues Zugriffstoken abzurufen, wenn das aktuelle Zugriffstoken abgelaufen ist.**. Es wird auch verwendet, um das *erste*  Zugriffstoken im [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) abzurufen. (Zum Zeitpunkt, an dem dieser Artikel geschrieben wurde, hatten von ACS ausgestellte Aktualisierungstoken für SharePoint eine Lebensspanne von 6 Monaten, das kann sich aber geändert haben.)</span><span class="sxs-lookup"><span data-stu-id="05410-p156">**A refresh token is included in the context token that SharePoint posts to your web application when it is launched.** The refresh token is an encrypted token that your SharePoint Add-in cannot unencrypt. **Your code uses it**, along with other information, **to get a new access token when the current access token expires**. It is also used to get the *first*  access token in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows). (When this article was written, ACS-issued refresh tokens for SharePoint had a life span of 6 months, but that could change.)</span></span>
 

 
<span data-ttu-id="05410-399">Da ein Zugriffstoken für Stunden gültig ist (derzeit 12) und ein Endbenutzer jedes Mal, wenn er Ihre SharePoint-Add-In von SharePoint startet, ein neues bekommt, brauchen Sie das Aktualisierungstoken nur in den folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="05410-399">Since an access token lasts hours (currently 12) and an end user gets a new one each time he launches your SharePoint Add-in from SharePoint, you only need the refresh token in one of these scenarios:</span></span>
 

 

- <span data-ttu-id="05410-400">Benutzer haben über lange Zeit laufende Sitzungen mit Ihrem Add-In, in denen das Add-In über viele Stunden (derzeit mehr als 12) nach ihrem Start Aufrufe an SharePoint durchführt.</span><span class="sxs-lookup"><span data-stu-id="05410-400">Users have long running sessions with your add-in in which the add-in makes calls to SharePoint many hours (currently more than 12) after it is launched.</span></span>
    
 
- <span data-ttu-id="05410-401">Das Design des Add-Ins ermöglicht Benutzern, den Zugriff des Add-Ins auf SharePoint für einen Zeitpunkt nach dem Beenden der Sitzung zu planen.</span><span class="sxs-lookup"><span data-stu-id="05410-401">The add-in's design enables users to schedule the add-in to access SharePoint sometime after the session ends.</span></span>
    
 
<span data-ttu-id="05410-p157">Für beide **Szenarien muss Ihr Add-In das Aktualisierungstoken zwischenspeichern**, und im zweiten Szenario ist ein serverseitiger Cache erforderlich, der über Sitzungen hinweg dauerhaft ist. Ihre Optionen zum Zwischenspeichern sind dieselben wie für das [Zugriffstoken](#CacheAccessToken), und im Kontexttokenablauf können Sie [den Cacheschlüssel im Kontexttoken verwenden](#CacheKey). (Im Kontexttokenablauf speichern Sie für gewöhnlich das Kontexttoken nur zwischen. Es enthält das Aktualisierungstoken und andere Informationen, die Sie benötigen, um ein neues Zugriffstoken zu erhalten. Im [Autorisierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) gibt es kein Kontexttoken, deshalb speichern Sie das Aktualisierungstoken selbst zwischen.)</span><span class="sxs-lookup"><span data-stu-id="05410-p157">Both  **scenarios require your add-in to cache the refresh token**, and second scenario requires a server-side cache that is durable across sessions. Your caching options are the same as those for the [access token](#CacheAccessToken) and, in the Context Token flow, you can use [the cache key in the context token](#CacheKey). (In the Context Token flow, you usually just cache the context token. It contains the refresh token and other information you need to get a new access token. In the  [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), there is no context token, so you cache the refresh token itself.)</span></span>
 

 
<span data-ttu-id="05410-p158">Wenn Sie das Aktualisierungstoken in einem Speicher zwischenspeichern, der über die Sitzungen eines bestimmten Benutzers mit Ihrem Add-In bestehen bleibt, achten Sie darauf, dass Sie es durch das neueste Aktualisierungstoken ersetzen. Sowohl im in der Cloud gehosteten als auch im Autorisierungscodeablauf erhält der Benutzer jedes Mal ein neues Aktualisierungstoken, wenn er das Add-In startet.</span><span class="sxs-lookup"><span data-stu-id="05410-p158">If you are caching the refresh token in a storage that persists across a specific user's sessions with your add-in, be sure to replace it with the newest refresh token. In both the Cloud-hosted and Authorization Code flows, the user gets a new refresh token each time he or she launches the add-in.</span></span>
 

 
<span data-ttu-id="05410-p159">Wenn das Aktualisierungstoken abgelaufen ist, führt eine Anforderung an ACS für ein neues Zugriffstoken zu einem **401 Unauthorized**-Fehler. Ihr Add-In sollte auf diesen Fehler reagieren, indem es ein neues Aktualisierungstoken abruft und es verwendet, um ein neues Zugriffstoken zu erhalten. (Da das Aktualisierungstoken verschlüsselt ist, kann ihr Code den Ablaufzeitpunkt nicht überprüfen, bevor er es verwendet.) Im Kontexttokenablauf erhält Ihr Add-In ein neues Aktualisierungstoken, indem es [ein neues Kontexttoken abruft](#GetNewContextToken). Im Autorisierungscodeablauf erhält Ihr Add-In ein neues Aktualisierungstoken, indem es den Ablauf neu startet. Ihr Code sollte spezifisch auf den Fehler reagieren, indem er den Benutzer zur SharePoint OAuthAuthorize.aspx-Seite umleitet, wie unter [Informationen zum OAuth-Ablauf für Add-Ins, die dynamisch Berechtigungen anfordern](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Flow) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="05410-p159">If the refresh token is expired, a request to ACS for a new access token will result in a  **401 Unauthorized** error. Your add-in should respond to this error by getting a new refresh token and using it to get a new access token. (Since the refresh token is encrypted, your code cannot check its expiration before using it.) In the Context Token flow, your add-in gets a new refresh token by [getting a new context token](#GetNewContextToken). In the Authorization Code flow, your add-in gets a new refresh token by restarting the flow. Specifically, your code should respond to the error by redirecting the user to the SharePoint OAuthAuthorize.aspx page as explained in  [Understand the OAuth flow for add-ins that request permissions on the fly](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Flow).</span></span>
 

 

## <a name="understanding-the-handling-authorization-codes"></a><span data-ttu-id="05410-414">Grundlegendes zum Umgang mit Autorisierungscodes</span><span class="sxs-lookup"><span data-stu-id="05410-414">Understanding the handling authorization codes</span></span>
<span data-ttu-id="05410-415"><a name="Authcodes"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-415"></span></span>

 <span data-ttu-id="05410-p160">**Im Autorisierungscodeablauf beginnt der Autorisierungsprozess mit einem Autorisierungscode, den ACS auf Anforderung von SharePoint ausstellt und den SharePoint dann** als Abfrageparameter an die Remoteanwendung übergibt. Der Autorisierungscode ist für jede Paarung aus Benutzer und Remoteanwendung eindeutig. (Zum Zeitpunkt, an dem dieser Artikel geschrieben wurde, hatten von ACS ausgestellte Autorisierungscodes für SharePoint eine Lebensspanne von 5 Minuten, das kann sich aber geändert haben.) Die Logik in **Ihrer Anwendung muss den Autorisierungscode aus dem Abfrageparameter abrufen und ihn in einer Anforderung an ACS für ein Zugriffstoken verwenden**. Wenn Sie verwalteten Code verwenden, finden Sie Beispielcode für das Erstellen des Tokens in der Datei TokenHelper.cs (und .vb). Beispielcode für das Lesen des Abfrageparameters finden Sie unter [Beispielcode für eine Seite, die auf SharePoint zugreift](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Default). ACS macht den Autorisierungscode direkt nach der Ausgabe des Zugriffscodes ungültig, damit er nur einmal verwendet werden kann. Außerdem macht es keinen Sinn, ihn zwischenzuspeichern.</span><span class="sxs-lookup"><span data-stu-id="05410-p160">**In the Authorization Code flow, the authorization process begins with an authorization code that ACS issues, at the request of SharePoint, and which SharePoint then passes to the remote application** as a query parameter. The authorization code is unique to each pair of user and remote application. (When this article was written, ACS-issued authorization codes for SharePoint had a life span of 5 minutes, but that could change.) The logic in **your application must get the authorization code from the query parameter and use it in a request to ACS for an access token**. If you are using managed code, sample code for creating the token is in the TokenHelper.cs (and .vb) file. Sample code for reading the query parameter is in [Get sample code behind for a page that accesses SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Default). ACS invalidates the authorization code immediately after issuing the access token, so it can only be used once and there is no point in caching it.</span></span>
 

 

## <a name="work-with-jwt-time-values"></a><span data-ttu-id="05410-422">Verwenden von JWT-Zeitwerten</span><span class="sxs-lookup"><span data-stu-id="05410-422">Work with JWT time values</span></span>
<span data-ttu-id="05410-423"><a name="JWTtimes"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-423"></span></span>

<span data-ttu-id="05410-p161">Die Ansprüche **nbf** und **exp** haben das durch die [JWT-Spezifikation](http://self-issued.info/docs/draft-goland-json-web-token-00l) angegebene Format. Sie werden als Anzahl der Sekunden seit dem 1. Januar 1970 dargestellt. In C# können Sie diese Werte mit dem folgenden Code übersetzen, wobei _jWTTimeStamp_ der Wert aus dem Token ist, z. B. 1335822895.</span><span class="sxs-lookup"><span data-stu-id="05410-p161">The  **nbf** and **exp** claims are in the format specified by the [JWT specification](http://self-issued.info/docs/draft-goland-json-web-token-00l). They are written as the number of seconds since Jan 1, 1970. In C#, you can translate these values with the following code, where  _jWTTimeStamp_ is the value from the token, such as 1335822895.</span></span>
 

 

```C#
DateTime exp = new DateTime(1970,1,1).AddSeconds(jWTTimeStamp);

```


## <a name="troubleshooting-token-handling"></a><span data-ttu-id="05410-427">Token-Problembehandlung</span><span class="sxs-lookup"><span data-stu-id="05410-427">Troubleshooting token handling</span></span>
<span data-ttu-id="05410-428"><a name="Troubleshooting"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-428"></span></span>

<span data-ttu-id="05410-p162">Das kostenlose  [Fiddler-Tool](http://www.telerik.com/fiddler) kann verwendet werden, um die HTTP-Anforderungen zu erfassen, die von der Remotekomponente Ihres Add-Ins SharePoint gesendet werden. Es gibt eine [kostenlose Erweiterung für das Tool](https://github.com/andrewconnell/SPOAuthFiddlerExt), die automatisch die Token in den Anforderungen dekodiert.</span><span class="sxs-lookup"><span data-stu-id="05410-p162">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the tokens in the requests.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="05410-431">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="05410-431">Additional resources</span></span>
<span data-ttu-id="05410-432"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="05410-432"></span></span>


-  [<span data-ttu-id="05410-433">Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden</span><span class="sxs-lookup"><span data-stu-id="05410-433">Creating SharePoint Add-ins that use low-trust authorization</span></span>](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)
    
 
- <span data-ttu-id="05410-434">Codebeispiele, die verwalteten Code und TokenHelper verwenden, finden Sie unter [SharePoint: Remote-Add-In „Hello World“ mit CSOM](http://code.msdn.microsoft.com/SharePoint-Hello-0fd15fbf) und [SharePoint-Add-Ins - Paket mit Beispielen](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)</span><span class="sxs-lookup"><span data-stu-id="05410-434">For code samples that use managed code and TokenHelper, see  [SharePoint: Hello World remote add-in using CSOM](http://code.msdn.microsoft.com/SharePoint-Hello-0fd15fbf) and [SharePoint Add-ins sample pack](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)</span></span>
    
 
- <span data-ttu-id="05410-435">Ein Codebeispiel, in dem REST-Aufrufe von einem PHP-Add-In verwendet werden, finden Sie unter: [SharePoint: Durchführen von Vorgängen in der SharePoint-Dokumentbibliothek von einer PHP-Website](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef)</span><span class="sxs-lookup"><span data-stu-id="05410-435">For a code sample that uses REST calls from a PHP add-in:  [SharePoint: Perform operations on SharePoint Document Library from PHP site](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef)</span></span>
    
 

