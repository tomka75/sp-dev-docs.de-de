---
title: "Übersicht über das mobile SharePoint-Objektmodell"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 72319846-d02d-49e7-b830-48eb8f5715cb
ms.openlocfilehash: 4f2f38a46c0afe3b534b7e2b2ee1c5a8dbbe0300
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-the-sharepoint-mobile-object-model"></a><span data-ttu-id="6a81b-102">Übersicht über das mobile SharePoint-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="6a81b-102">Overview of the SharePoint mobile object model</span></span>
<span data-ttu-id="6a81b-103">Informationen Sie zu neuen öffentlichen Klassen im Serverobjektmodell SharePoint und Silverlight-Clientobjektmodell, die zum Entwickeln von integrierter Lösungen für SharePoint und Windows Phone 7.5 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-103">Learn about the new public classes in the SharePoint server object model and Silverlight client object model that are used to develop integrated solutions for SharePoint and Windows Phone 7.5.</span></span>
## <a name="client-object-model-for-mobile-silverlight"></a><span data-ttu-id="6a81b-104">Clientobjektmodell für mobile Silverlight</span><span class="sxs-lookup"><span data-stu-id="6a81b-104">Client object model for mobile Silverlight</span></span>
<span data-ttu-id="6a81b-105"><a name="SP15OM_ClientOM"> </a></span><span class="sxs-lookup"><span data-stu-id="6a81b-105"></span></span>

<span data-ttu-id="6a81b-p101">Alle Klassen in diesem Abschnitt werden im **Microsoft.SharePoint.Client** -Namespace. Zusätzlich zu den APIs in diesem Abschnitt können die meisten Klassen und Member im Abschnitt Serverobjektmodell für die SharePoint-Mobilität auch in das Clientobjektmodell aufgerufen werden. Für Klassen, die mit "SP" beginnen, wird der Client-Objekt Modellname der "SP" entfernt. In anderen Fällen wird der Client Modell Objektname angegeben. Elementnamen sind die gleichen in des Clientobjektmodells, es sei denn, in denen anders angegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p101">All classes in this section are in the **Microsoft.SharePoint.Client** namespace. In addition to the APIs in this section, most of the classes and members in the section Server Object Model for SharePoint Mobility are also callable in the client object model. For classes that begin with "SP", the client object model name has the "SP" removed. In other cases, the client object model name is specified. Member names are the same in the client object model except where specified otherwise.</span></span>
  
    
    

### <a name="alternateurl-class"></a><span data-ttu-id="6a81b-111">AlternateUrl-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-111">AlternateUrl class</span></span>

<span data-ttu-id="6a81b-112">Stellt eine alternative URL für eine Webanwendung und die Zone, für die sie gilt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-112">Represents an alternative URL for a web application and the zone to which it applies.</span></span>
  
    
    

```cs

public class AlternateUrl
```


#### <a name="properties"></a><span data-ttu-id="6a81b-113">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-113">Properties</span></span>

 <span data-ttu-id="6a81b-114">**Uri** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-114">**Uri** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-115">Ruft den URI der alternativen URL ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-115">Gets the URI of the alternate URL.</span></span>
  
    
    



```cs
public String Uri
```

 <span data-ttu-id="6a81b-116">**UrlZone** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-116">**UrlZone** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-117">Ruft die Zone der alternativen URL an.</span><span class="sxs-lookup"><span data-stu-id="6a81b-117">Gets the zone of the alternate URL.</span></span>
  
    
    



```
public UrlZone UrlZone
```

<span data-ttu-id="6a81b-p102">Die UrlZone-Klasse ist die Client-Objektmodellversion der SPUrlZone-Klasse im Serverobjektmodell. Weitere Informationen hierzu finden Sie unter der  [SharePoint 2010 Software Development Kit (SDK)](http://msdn.microsoft.com/de-DE/library/ee557253.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a81b-p102">The UrlZone class is the client object model version of the SPUrlZone class in the server object model. For more information about it, see the  [SharePoint 2010 Software Development Kit (SDK)](http://msdn.microsoft.com/de-DE/library/ee557253.aspx).</span></span>
  
    
    

### <a name="authenticationcompletedeventargs-class"></a><span data-ttu-id="6a81b-120">AuthenticationCompletedEventArgs-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-120">AuthenticationCompletedEventArgs class</span></span>

<span data-ttu-id="6a81b-121">Stellt Daten über ein **AuthenticationCompleted** -Ereignis bereit.</span><span class="sxs-lookup"><span data-stu-id="6a81b-121">Provides data about an **AuthenticationCompleted** event.</span></span>
  
    
    

```cs
public sealed class AuthenticationCompletedEventArgs : AsyncCompletedEventArgs

```


#### <a name="constructors"></a><span data-ttu-id="6a81b-122">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-122">Constructors</span></span>

<span data-ttu-id="6a81b-123">Initialisiert eine neue Instanz der AuthenticationCompletedEventArgs-Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-123">Initializes a new instance of the AuthenticationCompletedEventArgs class.</span></span>
  
    
    

```cs

public AuthenticationCompletedEventArgs(Exception error, bool canceled, HttpStatusCode userState)
```

 <span data-ttu-id="6a81b-124">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-124">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-125">_error_ ist das Exception-Objekt, wenn es eine Ausnahme ausgelöst wird, in der Authentifizierungsversuch wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-125">_error_ is the Exception object if there was an exception thrown in the authentication attempt.</span></span>
    
  
-  <span data-ttu-id="6a81b-126">_canceled_ ist True, wenn der Authentifizierungsversuch abgebrochen wurde, bevor es erfolgreich oder fehlgeschlagen konnte.</span><span class="sxs-lookup"><span data-stu-id="6a81b-126">_canceled_ is true if the authentication attempt was canceled before it could succeed or fail.</span></span>
    
  
-  <span data-ttu-id="6a81b-127">_userState_ ist die HttpStatusCode vom Server zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-127">_userState_ is the HttpStatusCode returned by the server.</span></span>
    
  

#### <a name="properties"></a><span data-ttu-id="6a81b-128">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-128">Properties</span></span>

 <span data-ttu-id="6a81b-129">**HttpStatusCode** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-129">**HttpStatusCode** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-130">Ruft den Status, die vom Server nach einen Authentifizierungsversuch zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-130">Gets the status returned by the server after an authentication attempt.</span></span>
  
    
    



```cs
public HttpStatusCode HttpStatusCode
```


### <a name="authenticationstatus-enum"></a><span data-ttu-id="6a81b-131">AuthenticationStatus-Enumeration</span><span class="sxs-lookup"><span data-stu-id="6a81b-131">AuthenticationStatus enum</span></span>

<span data-ttu-id="6a81b-132">Gibt den aktuellen Status des einen Authentifizierungsversuch.</span><span class="sxs-lookup"><span data-stu-id="6a81b-132">Specifies the current state of an authentication attempt.</span></span>
  
    
    

- <span data-ttu-id="6a81b-133">**NotStarted**</span><span class="sxs-lookup"><span data-stu-id="6a81b-133">**NotStarted**</span></span>
    
  
- <span data-ttu-id="6a81b-134">**InProgress**</span><span class="sxs-lookup"><span data-stu-id="6a81b-134">**InProgress**</span></span>
    
  
- <span data-ttu-id="6a81b-135">**CompletedSuccess**</span><span class="sxs-lookup"><span data-stu-id="6a81b-135">**CompletedSuccess**</span></span>
    
  
- <span data-ttu-id="6a81b-136">**CompletedException**</span><span class="sxs-lookup"><span data-stu-id="6a81b-136">**CompletedException**</span></span>
    
  

### <a name="authenticator-class"></a><span data-ttu-id="6a81b-137">Authentifizierungsserver-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-137">Authenticator class</span></span>

<span data-ttu-id="6a81b-138">Stellt Methoden zum Authentifizieren eines Benutzers auf einer SharePoint-Website bereit.</span><span class="sxs-lookup"><span data-stu-id="6a81b-138">Provides methods for authenticating a user on a SharePoint website.</span></span>
  
    
    

```
public class Authenticator : ICredentials
```


#### <a name="constructors"></a><span data-ttu-id="6a81b-139">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-139">Constructors</span></span>

<span data-ttu-id="6a81b-140">Initialisiert eine neue Instanz der Klasse an.</span><span class="sxs-lookup"><span data-stu-id="6a81b-140">Initializes a new instance of the class.</span></span>
  
    
    

```cs
public Authenticator()

public Authenticator(Uri uagServerUrl)
```

 <span data-ttu-id="6a81b-141">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-141">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-142">_uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6a81b-142">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    



```cs

public Authenticator(string userName, string password)
```

 <span data-ttu-id="6a81b-143">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-143">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-144">_userName_ ist der Name für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-144">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-145">_password_ ist das Kennwort für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-145">_password_ is the password for the credentials.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, string domain)
```

 <span data-ttu-id="6a81b-146">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-146">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-147">_userName_ ist der Name für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-147">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-148">_password_ ist das Kennwort für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-148">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-149">_domain_ ist der Name der Domäne oder des Computers, auf dem die Anmeldeinformationen überprüft werden, in der Regel die Domäne des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6a81b-149">_domain_ is the name of the domain or computer where the credentials are verified, typically the domain of the current user.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, Uri uagServerUrl)
```

 <span data-ttu-id="6a81b-150">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-150">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-151">_userName_ ist der Name für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-151">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-152">_password_ ist das Kennwort für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-152">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-153">_uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6a81b-153">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, string domain, Uri uagServerUrl)
```

 <span data-ttu-id="6a81b-154">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-154">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-155">_userName_ ist der Name für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-155">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-156">_password_ ist das Kennwort für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-156">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6a81b-157">_domain_ ist der Name der Domäne oder des Computers, auf dem die Anmeldeinformationen überprüft werden, in der Regel die Domäne des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6a81b-157">_domain_ is the name of the domain or computer where the credentials are verified, typically the domain of the current user.</span></span>
  
    
    
 <span data-ttu-id="6a81b-158">_uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6a81b-158">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6a81b-159">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-159">Methods</span></span>

 <span data-ttu-id="6a81b-160">**ClearAllApplicationSettings**</span><span class="sxs-lookup"><span data-stu-id="6a81b-160">**ClearAllApplicationSettings**</span></span>
  
    
    
<span data-ttu-id="6a81b-161">Löscht alle Cookies, Anmeldeinformationen und UAG-Einstellungen aus dem Cache.</span><span class="sxs-lookup"><span data-stu-id="6a81b-161">Clears all cookies, credentials, and UAG settings from the cache.</span></span>
  
    
    



```cs
public static void ClearAllApplicationSettings
```

 <span data-ttu-id="6a81b-162">**ClearAllCookies**</span><span class="sxs-lookup"><span data-stu-id="6a81b-162">**ClearAllCookies**</span></span>
  
    
    
<span data-ttu-id="6a81b-163">Löscht alle gespeicherten Cookies, und die **Status** -Eigenschaft aller **Authenticator** -Objekte auf **NotStarted**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-163">Clears all stored cookies and sets the **Status** property of all **Authenticator** objects to **NotStarted**.</span></span>
  
    
    



```cs
public static void ClearAllCookies()
```

 <span data-ttu-id="6a81b-164">**ClearAllCredentials**</span><span class="sxs-lookup"><span data-stu-id="6a81b-164">**ClearAllCredentials**</span></span>
  
    
    
<span data-ttu-id="6a81b-165">Löscht alle Anmeldeinformationen aus dem Cache und die **Status** -Eigenschaft aller **Authenticator** -Objekte auf **NotStarted**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-165">Clears all credentials from the cache and sets the **Status** property of all **Authenticator** objects to **NotStarted**.</span></span>
  
    
    



```cs
public static void ClearAllCredentials()
```

 <span data-ttu-id="6a81b-166">**GetCredential**</span><span class="sxs-lookup"><span data-stu-id="6a81b-166">**GetCredential**</span></span>
  
    
    
<span data-ttu-id="6a81b-167">Ruft ein Objekt mit Anmeldeinformationen für den angegebenen Uri und Authentifizierungstyp.</span><span class="sxs-lookup"><span data-stu-id="6a81b-167">Gets a credential object for the specified uri and authentication type.</span></span>
  
    
    



```
public NetworkCredential GetCredential(Uri uri, string authType)
```

 <span data-ttu-id="6a81b-168">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-168">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-169">_uri_ ist der URI, einschließlich der Port, für die der Client die Authentifizierung bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-169">_uri_ is the URI, including port, for which the client is providing authentication.</span></span>
    
  
-  <span data-ttu-id="6a81b-170">_authType_ ist die Art der Authentifizierung angefordert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-170">_authType_ is the type of authentication requested.</span></span>
    
  
<span data-ttu-id="6a81b-p103">Diese Methode ist nur für die anonyme Authentifizierung verwendet. Wenn  _authType_ nicht "Basic" ist, wird ein leeres Objekt zurückgegeben. Weitere Informationen über die **NetworkCredential** -Klasse finden Sie unter [NetworkCredential-Klasse](http://msdn.microsoft.com/de-DE/library/system.net.networkcredential.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a81b-p103">This method is only used for anonymous authentication. If  _authType_ is not "Basic", an empty object is returned. For more information about the **NetworkCredential** class, see [NetworkCredential Class](http://msdn.microsoft.com/de-DE/library/system.net.networkcredential.aspx).</span></span>
  
    
    
 <span data-ttu-id="6a81b-174">**IsRequestUnauthorized**</span><span class="sxs-lookup"><span data-stu-id="6a81b-174">**IsRequestUnauthorized**</span></span>
  
    
    
<span data-ttu-id="6a81b-175">Gibt true zurück, wenn die Autorisierung Anforderung aufgrund einer ungültigen Cookie oder Anmeldeinformationen ist fehlgeschlagen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-175">Returns true if the authorization request failed because of an invalid cookie or credentials.</span></span>
  
    
    



```cs
public static bool IsRequestUnauthorized(ClientRequestFailedEventArgs failedEventArgs)
```


#### <a name="properties"></a><span data-ttu-id="6a81b-176">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-176">Properties</span></span>

 <span data-ttu-id="6a81b-177">**AllowSmartRouting**</span><span class="sxs-lookup"><span data-stu-id="6a81b-177">**AllowSmartRouting**</span></span>
  
    
    
<span data-ttu-id="6a81b-178">Ruft ab oder legt diesen fest einen Indikator, ob der smart-routing aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="6a81b-178">Gets or sets an indicator of whether smart routing is enabled.</span></span>
  
    
    



```
public bool AllowSmartRouting
```

<span data-ttu-id="6a81b-p104">Beim smart routing aktiviert ist, versucht das **Authenticator** -Objekt mit dem Server herstellen, die SharePoint- und dem UAG-Server ausgeführt wird und verwendet, je nachdem, was zuerst als Kommunikationskanal antwortet. Wenn kein UAG-Server vorhanden ist, wird diese Eigenschaft ignoriert. Der Standardwert ist **true**. Wenn **false**, dem UAG-Server immer verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p104">When smart routing is enabled, the **Authenticator** object tries to connect to the server that is running SharePoint and the UAG server and uses whichever responds first as its communication channel. If there is no UAG server, this property is ignored. The default is **true**. If set to **false**, the UAG server is always used.</span></span>
  
    
    
 <span data-ttu-id="6a81b-183">**AuthenticatorMode**</span><span class="sxs-lookup"><span data-stu-id="6a81b-183">**AuthenticatorMode**</span></span>
  
    
    
<span data-ttu-id="6a81b-184">Ruft ab oder legt den Authentifizierungsmodus fest.</span><span class="sxs-lookup"><span data-stu-id="6a81b-184">Gets or sets the authentication mode.</span></span>
  
    
    



```cs
public ClientAuthenticationMode AuthenticationMode
```

<span data-ttu-id="6a81b-185">Weitere Informationen zu den **ClientAuthenticationMode** -Enumeration finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-185">For more information about the **ClientAuthenticationMode** enum, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-186">**CookieCachingEnabled**</span><span class="sxs-lookup"><span data-stu-id="6a81b-186">**CookieCachingEnabled**</span></span>
  
    
    
<span data-ttu-id="6a81b-187">Ruft ab oder legt diesen fest einen Indikator gibt an, ob Cookies zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-187">Gets or sets an indicator of whether cookies are cached.</span></span>
  
    
    



```
public bool CookieCachingEnabled
```

<span data-ttu-id="6a81b-p105">Wenn Sie das Zwischenspeichern von Cookies aktivieren, sollten Sie Sie, dass die Cookies zu einem bestimmten Zeitpunkt ablaufen. Wenn diese abgelaufen sind, wenn **ExecuteQueryAsync** aufgerufen wird, klicken Sie dann der Aufruf fehlschlägt, und der Rückruf für Fehler ausgeführt wird. Entsprechend, wenn Sie diese Eigenschaft auf True festlegen, müssen Sie Code für den Rückruf für Fehler hinzufügen, die den Cache gelöscht, in diesem Fall. Hier ist ein Beispiel, wobei `execQueryArgs` der den Typ **ClientRequestFailedEventArgs** in der Failure-Rückruf **ExecuteQueryAsync**übergeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p105">If you enable caching of cookies, consider that the cookies expire at some point. If they are expired when **ExecuteQueryAsync** is called, then it fails and the callback for failure runs. Accordingly, if you set this property to true, you must add code to the callback for failure that clears the cache if this happens. Here is an example, where `execQueryArgs` is of the type **ClientRequestFailedEventArgs** passed in the failure callback of **ExecuteQueryAsync**.</span></span>
  
    
    



```cs
if (Authenticator.IsRequestUnauthorized(execQueryArgs))
{
    (sender as Authenticator).ClearCookies();
}
```

 <span data-ttu-id="6a81b-192">**CredentialCachingEnabled**</span><span class="sxs-lookup"><span data-stu-id="6a81b-192">**CredentialCachingEnabled**</span></span>
  
    
    
<span data-ttu-id="6a81b-193">Ruft ab oder legt diesen fest einen Indikator gibt an, ob die Anmeldeinformationen zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-193">Gets or sets an indicator of whether credentials are cached.</span></span>
  
    
    



```cs

public bool CredentialCachingEnabled
```

 <span data-ttu-id="6a81b-194">**Domain**</span><span class="sxs-lookup"><span data-stu-id="6a81b-194">**Domain**</span></span>
  
    
    
<span data-ttu-id="6a81b-195">Ruft ab oder legt diesen fest, Domäne oder des Computers für die Anmeldeinformationen in der Regel ist dies die Domäne des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6a81b-195">Gets or sets the domain or computer for the credential, usually this is the domain of the current user.</span></span>
  
    
    



```cs
public string Domain
```

<span data-ttu-id="6a81b-196">Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf nicht gestartet festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-196">When this property is set to a new value, the **Status** property is set to NotStarted.</span></span>
  
    
    
 <span data-ttu-id="6a81b-197">**NavigateBackAfterAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6a81b-197">**NavigateBackAfterAuthentication**</span></span>
  
    
    
<span data-ttu-id="6a81b-198">Dient zum Abrufen oder festlegen einen Indikator gibt an, ob der Benutzer wieder auf die vorherige Seite auf der Anmeldeseite von dem navigiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="6a81b-198">Gets or sets a indicator of whether the user should be navigated back to the previous page from the login page.</span></span>
  
    
    



```cs
public bool NavigateBackAfterAuthentication
```

 <span data-ttu-id="6a81b-199">**Password**</span><span class="sxs-lookup"><span data-stu-id="6a81b-199">**Password**</span></span>
  
    
    
<span data-ttu-id="6a81b-200">Ruft ab oder legt das Kennwort für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-200">Gets or sets the password for the credential.</span></span>
  
    
    



```cs
public string Password
```

<span data-ttu-id="6a81b-201">Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf **NotStarted**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-201">When this property is set to a new value, the **Status** property is set to **NotStarted**.</span></span>
  
    
    
 <span data-ttu-id="6a81b-202">**PromptOnFailure**</span><span class="sxs-lookup"><span data-stu-id="6a81b-202">**PromptOnFailure**</span></span>
  
    
    
<span data-ttu-id="6a81b-203">Ruft ab oder legt diesen fest einen Indikator gibt an, ob der Benutzer aufgefordert werden soll, einen Namen und ein Kennwort eingeben, wenn die erste Authentifizierung ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-203">Gets or sets an indicator of whether the user should be prompted to enter a name and password if initial authentication fails.</span></span>
  
    
    



```cs
public bool PromptOnFailure
```

 <span data-ttu-id="6a81b-204">**Status** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-204">**Status** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-205">Ruft den Status des Programms zur Authentifizierung ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-205">Gets the status of the attempt to authenticate.</span></span>
  
    
    



```cs
public AuthenticationStatus Status
```

<span data-ttu-id="6a81b-206">Finden Sie weiter oben in diesem Dokument, um Informationen über die **AuthenticationStatus** -Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-206">See earlier in this document for information about the **AuthenticationStatus** class.</span></span>
  
    
    
 <span data-ttu-id="6a81b-207">**UagServerUrl**</span><span class="sxs-lookup"><span data-stu-id="6a81b-207">**UagServerUrl**</span></span>
  
    
    
<span data-ttu-id="6a81b-208">Dient zum Abrufen oder Festlegen der URL des UAG-Server.</span><span class="sxs-lookup"><span data-stu-id="6a81b-208">Gets or sets the URL of the UAG server.</span></span>
  
    
    



```cs
public Uri UagServerUrl
```

 <span data-ttu-id="6a81b-209">**UserName**</span><span class="sxs-lookup"><span data-stu-id="6a81b-209">**userName**</span></span>
  
    
    
<span data-ttu-id="6a81b-210">Ruft ab oder legt den Benutzernamen für die Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-210">Gets or sets the user name for the credential.</span></span>
  
    
    



```cs
public string UserName
```

<span data-ttu-id="6a81b-211">Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf **NotStarted**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-211">When this property is set to a new value, the **Status** property is set to **NotStarted**.</span></span>
  
    
    

#### <a name="events"></a><span data-ttu-id="6a81b-212">Veranstaltungen</span><span class="sxs-lookup"><span data-stu-id="6a81b-212">Events</span></span>

 <span data-ttu-id="6a81b-213">**AuthenticationCompleted**</span><span class="sxs-lookup"><span data-stu-id="6a81b-213">**AuthenticationCompleted**</span></span>
  
    
    
<span data-ttu-id="6a81b-214">Wird ausgelöst, wenn der Authentifizierungsversuch unabhängig davon, ob es erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-214">Raised when the authentication attempt is completed, regardless of whether it succeeded.</span></span>
  
    
    



```cs
public event EventHandler<AuthenticationCompletedEventArgs> AuthenticationCompleted;
```


### <a name="clientauthenticationmode-enum"></a><span data-ttu-id="6a81b-215">ClientAuthenticationMode-Enumeration</span><span class="sxs-lookup"><span data-stu-id="6a81b-215">ClientAuthenticationMode enum</span></span>

<span data-ttu-id="6a81b-p106">Gibt einen Authentifizierungsmodus für ein **Authenticator** -Objekt an. Hierbei handelt es sich um eine vorhandene Enumeration an die, einen neuen Wert **BrowserBasedAuthentication** hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p106">Specifies an authentication mode for an **Authenticator** object. This is an existing enum to which a new value, **BrowserBasedAuthentication** has been added.</span></span>
  
    
    


|<span data-ttu-id="6a81b-218">**Standard**</span><span class="sxs-lookup"><span data-stu-id="6a81b-218">**Default**</span></span>||
|:-----|:-----|
|<span data-ttu-id="6a81b-219">**FormsAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6a81b-219">**FormsAuthentication**</span></span> <br/> |<span data-ttu-id="6a81b-220">Stellt die formularbasierte Authentifizierung-Modus</span><span class="sxs-lookup"><span data-stu-id="6a81b-220">Represents forms-based authentication mode</span></span>  <br/> |
|<span data-ttu-id="6a81b-221">**Anonymous**</span><span class="sxs-lookup"><span data-stu-id="6a81b-221">**Anonymous**</span></span> <br/> |<span data-ttu-id="6a81b-222">Anonymen Zugriffsmodus darstellt</span><span class="sxs-lookup"><span data-stu-id="6a81b-222">Represents anonymous access mode</span></span>  <br/> |
|<span data-ttu-id="6a81b-223">**BrowserBasedAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6a81b-223">**BrowserBasedAuthentication**</span></span> <br/> |<span data-ttu-id="6a81b-224">Microsoft Office Forms basierte Authentifizierung (MSOFBA) Modus darstellt</span><span class="sxs-lookup"><span data-stu-id="6a81b-224">Represents Microsoft Office Forms Based Authentication (MSOFBA) mode</span></span>  <br/> |
   

### <a name="odataauthenticator-class"></a><span data-ttu-id="6a81b-225">ODataAuthenticator-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-225">ODataAuthenticator class</span></span>

<span data-ttu-id="6a81b-226">Stellt Methoden zum Authentifizieren eines Benutzers auf einer SharePoint-Website bereit.</span><span class="sxs-lookup"><span data-stu-id="6a81b-226">Provides methods for authenticating a user on a SharePoint website.</span></span>
  
    
    

```cs
public class ODataAuthenticator : Authenticator
```


#### <a name="constructors"></a><span data-ttu-id="6a81b-227">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-227">Constructors</span></span>

<span data-ttu-id="6a81b-p107">Die Konstruktoren sind identisch mit der übergeordneten Klassenkonstruktoren. Weitere Informationen finden Sie weiter oben in diesem Dokument Authentifizierungsserver-Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p107">The constructors are identical to the parent class constructors. For more information, see Authenticator Class earlier in this document.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6a81b-230">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-230">Methods</span></span>

 <span data-ttu-id="6a81b-231">**Authenticate**</span><span class="sxs-lookup"><span data-stu-id="6a81b-231">**Authenticate**</span></span>
  
    
    
<span data-ttu-id="6a81b-232">Authentifiziert einen Benutzer mit der angegebenen Website.</span><span class="sxs-lookup"><span data-stu-id="6a81b-232">Authenticates a user to the specified website.</span></span>
  
    
    



```cs
public new void Authenticate(Uri serverUrl)
```

<span data-ttu-id="6a81b-233">Das Schlüsselwort  `new` wird verwendet, da die übergeordnete Klasse eine interne Methode mit demselben Namen verfügt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-233">The  `new` keyword is used because the parent class has an internal method of the same name.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6a81b-234">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-234">Properties</span></span>

 <span data-ttu-id="6a81b-235">**CookieContainer** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-235">**CookieContainer** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-236">Ruft einen Container mit Cookies für Anfragen auf der Website ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-236">Gets a container with the cookies for requests to the website.</span></span>
  
    
    



```cs
public new CookieContainer CookieContainer
```

<span data-ttu-id="6a81b-237">Das Schlüsselwort  `new` wird verwendet, da die übergeordnete Klasse eine interne Methode mit demselben Namen verfügt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-237">The  `new` keyword is used because the parent class has an internal method of the same name.</span></span>
  
    
    
 <span data-ttu-id="6a81b-238">**ResolvedUrl** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-238">**ResolvedUrl** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-p108">Ruft die URL, die für die Kommunikation mit dem Server verwendet wird, auf dem SharePoint ausgeführt wird, wenn ein **ODataAuthenticator** verwendet wird. Dies ist möglicherweise die URL auf dem UAG-Server veröffentlicht oder, wenn die **AllowSmartRouting** -Eigenschaft auf true festgelegt ist, kann dies die URL der SharePoint-Intranet sein, wenn zuerst erreicht wird die **Authenticate** -Methode aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p108">Gets the URL that is used for communication to the server that is running SharePoint when an **ODataAuthenticator** is being used. This may be the URL published on the UAG server or, if the **AllowSmartRouting** property is true, this may be the SharePoint intranet URL if it is reached first when the **Authenticate** method is called.</span></span>
  
    
    



```cs
public Uri ResolvedUrl
```


### <a name="serversettings-class"></a><span data-ttu-id="6a81b-241">ServerSettings-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-241">ServerSettings class</span></span>

<span data-ttu-id="6a81b-242">Stellt eine Methode zum Abrufen von alternativen URLs der Webanwendung, die eine Website enthält.</span><span class="sxs-lookup"><span data-stu-id="6a81b-242">Provides a method for getting the Alternate URLs of the web application that contains a website.</span></span>
  
    
    

```cs
public static class ServerSettings
```


#### <a name="methods"></a><span data-ttu-id="6a81b-243">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-243">Methods</span></span>

 <span data-ttu-id="6a81b-244">**GetAlternateUrls**</span><span class="sxs-lookup"><span data-stu-id="6a81b-244">**GetAlternateUrls**</span></span>
  
    
    
<span data-ttu-id="6a81b-245">Ruft die alternativen URLs der angegebenen Website ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-245">Gets the alternate URLs of the specified website.</span></span>
  
    
    



```cs
public static ClientObjectList<AlternateUrl> GetAlternateUrls(ClientRuntimeContext context)
```

 <span data-ttu-id="6a81b-246">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-246">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-247">_context_ ist die ein Objekt, das den aktuellen Clientkontext darstellt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-247">_context_ is the an object that represents the current client context.</span></span>
  
    
    
<span data-ttu-id="6a81b-248">Finden Sie weiter oben in diesem Dokument, um Informationen über die **AlternateUrl** -Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-248">See earlier in this document for information about the **AlternateUrl** class.</span></span>
  
    
    

## <a name="server-object-model-for-sharepoint-mobility"></a><span data-ttu-id="6a81b-249">Objektmodell für Mobilität mit SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="6a81b-249">Server object model for SharePoint mobility</span></span>
<span data-ttu-id="6a81b-250"><a name="SP15OM_ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="6a81b-250"></span></span>

<span data-ttu-id="6a81b-p109">Alle Klassen in diesem Abschnitt werden im **Microsoft.SharePoint** -Namespace. Es sei denn, in denen angegeben werden sind diese ebenfalls in das Clientobjektmodell verfügbar. Für Klassen, die mit "SP" beginnen, wird der Client-Objekt Modellname der "SP" entfernt. In anderen Fällen wird der Client Modell Objektname angegeben. Elementnamen sind die gleichen in des Clientobjektmodells, es sei denn, in denen anders angegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p109">All classes in this section are in the **Microsoft.SharePoint** namespace. Except where specified, these are all available also in the client object model. For classes that begin with "SP", the client object model name has the "SP" removed. In other cases, the client object model name is specified. Member names are the same in the client object model except where specified otherwise.</span></span>
  
    
    

### <a name="geolocationfieldcontrol-class"></a><span data-ttu-id="6a81b-256">GeolocationFieldControl-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-256">GeolocationFieldControl class</span></span>

<span data-ttu-id="6a81b-257">(Nicht verfügbar im Client Object Model).</span><span class="sxs-lookup"><span data-stu-id="6a81b-257">(Not available in client object model.)</span></span> 
  
    
    
<span data-ttu-id="6a81b-p110">Steuert das Rendern von Feldern **SPFieldGeolocation**. Ein Objekt dieses Typs wird als der Wert der **FieldRenderingControl** -Eigenschaft eines **SPFieldGeolocation** -Objekts verwendet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p110">Governs the rendering of **SPFieldGeolocation** fields. An object of this type is used as the value of the **FieldRenderingControl** property of a **SPFieldGeolocation** object.</span></span>
  
    
    



```cs
public class GeolocationFieldControl : BaseFieldControl
```

<span data-ttu-id="6a81b-p111">Im Zusammenhang mit dieser Klasse Beachten Sie außerdem, dass es zwei renderingvorlagen, eines für den Anzeigemodus und einen für New- und Edit-Modus gibt. Sie sind in der Datei % SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx definiert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p111">In connection with this class, note also that there are two rendering templates, one for Display mode and one for New and Edit mode. They are defined in the file %SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx.</span></span>
  
    
    

#### <a name="fields"></a><span data-ttu-id="6a81b-262">Felder</span><span class="sxs-lookup"><span data-stu-id="6a81b-262">Fields</span></span>

<span data-ttu-id="6a81b-263">Die folgenden dienen zum Rendern des Felds in der neuen und bearbeiteten Modi verwendet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-263">The following are used to render the field in the New and Edit modes.</span></span>
  
    
    

```cs
protected TextBox m_latitudeBox;
protected TextBox m_longitudeBox;
protected Label m_longitudeLabel;
protected Label m_latitudeLabel;
```


#### <a name="methods"></a><span data-ttu-id="6a81b-264">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-264">Methods</span></span>

<span data-ttu-id="6a81b-p112">Mit dieser Klasse sind keine nicht abgeleitete öffentlichen Eigenschaften eingeführt. Standard Außerkraftsetzungen von einigen abgeleiteten Methoden sind vorhanden, wie in der folgenden Tabelle angegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p112">No non-derived public properties are introduced with this class. There are standard overrides of some derived methods as indicated in the following table.</span></span>
  
    
    


|<span data-ttu-id="6a81b-267">**Method**</span><span class="sxs-lookup"><span data-stu-id="6a81b-267">**Method**</span></span>|<span data-ttu-id="6a81b-268">**This override???**</span><span class="sxs-lookup"><span data-stu-id="6a81b-268">**This override…**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a81b-269">CreateChildControls</span><span class="sxs-lookup"><span data-stu-id="6a81b-269">CreateChildControls</span></span>  <br/> |<span data-ttu-id="6a81b-270">Erstellt die untergeordneten Steuerelemente einschließlich ein JavaScript Map-Steuerelement für den Anzeigemodus.</span><span class="sxs-lookup"><span data-stu-id="6a81b-270">Creates the child controls including a JavaScript map control for Display mode.</span></span>  <br/> |
|<span data-ttu-id="6a81b-271">Konferenzzustandsobjekt</span><span class="sxs-lookup"><span data-stu-id="6a81b-271">Focus</span></span>  <br/> |<span data-ttu-id="6a81b-272">Verschiebt den Fokus auf das Längengrad Textbox untergeordnete Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="6a81b-272">Gives focus to the longitude textbox child control.</span></span>  <br/> |
|<span data-ttu-id="6a81b-273">OnPreRender</span><span class="sxs-lookup"><span data-stu-id="6a81b-273">OnPreRender</span></span>  <br/> |<span data-ttu-id="6a81b-274">Die base-Methode aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-274">Calls the base method.</span></span>  <br/> |
|<span data-ttu-id="6a81b-275">Validieren</span><span class="sxs-lookup"><span data-stu-id="6a81b-275">Validate</span></span>  <br/> |<span data-ttu-id="6a81b-p113">Überprüft die Breiten- und Längengrad Werte, die in der Benutzeroberfläche (UI) angezeigt werden. Dies wird nicht die Eigenschaften **Longitude** und **Latitude** des zugrunde liegenden **SPFieldGeolocatonValue** -Objekts validiert die abweichen wird, wenn der Benutzer eine oder mehrere der folgenden Werte in der Benutzeroberfläche geändert und die Änderungen noch nicht gespeichert wurde. </span><span class="sxs-lookup"><span data-stu-id="6a81b-p113">Validates the latitude and longitude values that appear in the user interface (UI). This does not validate the **Longitude** and **Latitude** properties of the underlying **SPFieldGeolocatonValue** object, which will differ if the user has changed one or more of these values in the UI and not yet saved the changes. </span></span><br/> |
   

#### <a name="properties"></a><span data-ttu-id="6a81b-278">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-278">Properties</span></span>

<span data-ttu-id="6a81b-p114">Mit dieser Klasse sind keine nicht abgeleitete öffentlichen Eigenschaften eingeführt. Standard Außerkraftsetzungen von einige abgeleiteten Eigenschaften sind vorhanden, wie in der folgenden Tabelle angegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p114">No non-derived public properties are introduced with this class. There are standard overrides of some derived properties as indicated in the following table.</span></span>
  
    
    


|<span data-ttu-id="6a81b-281">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="6a81b-281">**Property**</span></span>|<span data-ttu-id="6a81b-282">**Diese Außerkraftsetzung...**</span><span class="sxs-lookup"><span data-stu-id="6a81b-282">**This override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a81b-283">CssClass</span><span class="sxs-lookup"><span data-stu-id="6a81b-283">CssClass</span></span>  <br/> |<span data-ttu-id="6a81b-284">Verhält sich wie die übergeordnete Implementierung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-284">Behaves just like the parent implementation.</span></span>  <br/> |
|<span data-ttu-id="6a81b-285">DefaultTemplateName</span><span class="sxs-lookup"><span data-stu-id="6a81b-285">DefaultTemplateName</span></span>  <br/> |<span data-ttu-id="6a81b-286">Gibt "GeolocationField"</span><span class="sxs-lookup"><span data-stu-id="6a81b-286">Returns "GeolocationField"</span></span>  <br/> |
|<span data-ttu-id="6a81b-287">DisplayTemplateName</span><span class="sxs-lookup"><span data-stu-id="6a81b-287">DisplayTemplateName</span></span>  <br/> |<span data-ttu-id="6a81b-288">Gibt "GeolocationDisplayField"</span><span class="sxs-lookup"><span data-stu-id="6a81b-288">Returns "GeolocationDisplayField"</span></span>  <br/> |
|<span data-ttu-id="6a81b-289">Wert</span><span class="sxs-lookup"><span data-stu-id="6a81b-289">Value</span></span>  <br/> |<span data-ttu-id="6a81b-290">Dient zum Abrufen oder Festlegen des Werts, der mithilfe eines Objekts **SPFieldGeolocationValue** gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-290">Gets or sets the value that is rendered by using a **SPFieldGeolocationValue** object.</span></span> <br/> |
   

### <a name="spfieldgeolocation-class"></a><span data-ttu-id="6a81b-291">SPFieldGeolocation-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-291">SPFieldGeolocation class</span></span>

<span data-ttu-id="6a81b-292">Stellt ein Feld (Spalte), das ein Verzeichnis auf der ganzen Welt von Längengrad, Breiten- und möglicherweise Höhe definierten enthält.</span><span class="sxs-lookup"><span data-stu-id="6a81b-292">Represents a field (column) that holds a location on the globe defined by longitude, latitude, and possibly altitude.</span></span>
  
    
    

```cs

public class SPFieldGeolocation : SPField
```

<span data-ttu-id="6a81b-293">Im Zusammenhang mit dieser Klasse wird der Feldtyp **Geolocation** in % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml definiert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-293">In connection with this class, the **Geolocation** field type is defined in % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml.</span></span>
  
    
    

#### <a name="constructors-overloaded"></a><span data-ttu-id="6a81b-294">Konstruktoren (überladen)</span><span class="sxs-lookup"><span data-stu-id="6a81b-294">Constructors (overloaded)</span></span>

<span data-ttu-id="6a81b-295">Initialisiert eine neue Instanz der **SPFieldGeolocation** -Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-295">Initializes a new instance of the **SPFieldGeolocation** class.</span></span>
  
    
    

```cs
public SPFieldGeolocation(SPFieldCollection fields, string fieldName)
public SPFieldGeolocation(SPFieldCollection fields, string fieldName, string displayName)
```

 <span data-ttu-id="6a81b-296">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-296">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-297">_fields_ ist die Auflistung der Feldtypen dar, die das neue Feld Typ-Objekt hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-297">_fields_ is the collection of field types to which the new field type object is added.</span></span>
    
  
-  <span data-ttu-id="6a81b-298">_fieldName_ ist ein interner Name des neuen Feldtyps.</span><span class="sxs-lookup"><span data-stu-id="6a81b-298">_fieldName_ is an internal name of the new field type.</span></span>
    
  
-  <span data-ttu-id="6a81b-299">_displayName_ ist ein Anzeigename des neuen Feldtyps.</span><span class="sxs-lookup"><span data-stu-id="6a81b-299">_displayName_ is a friendly name of the new field type.</span></span>
    
  

#### <a name="methods"></a><span data-ttu-id="6a81b-300">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-300">Methods</span></span>

 <span data-ttu-id="6a81b-301">**GetFieldValueForClientRender**</span><span class="sxs-lookup"><span data-stu-id="6a81b-301">**GetFieldValueForClientRender**</span></span>
  
    
    
<span data-ttu-id="6a81b-302">Ruft den Wert des Felds, sodass es auf dem Client gerendert werden kann.</span><span class="sxs-lookup"><span data-stu-id="6a81b-302">Gets the value of the field so that it can be rendered on the client.</span></span>
  
    
    



```cs

public override object GetFieldValueForClientRender(SPItem item, SPControlMode mode)
```

<span data-ttu-id="6a81b-303">Parameter</span><span class="sxs-lookup"><span data-stu-id="6a81b-303">Parameters</span></span>
  
    
    

-  <span data-ttu-id="6a81b-304">_item_ ist das aktuelle Listenelement.</span><span class="sxs-lookup"><span data-stu-id="6a81b-304">_item_ is the current list item.</span></span>
    
  
-  <span data-ttu-id="6a81b-305">_mode_ ist die aktuelle Rendermodus wie neu, bearbeiten oder anzeigen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-305">_mode_ is the current rendering mode such as New, Edit, or Display.</span></span>
    
  
 <span data-ttu-id="6a81b-306">**GetJsonClientFormFieldSchema**</span><span class="sxs-lookup"><span data-stu-id="6a81b-306">**GetJsonClientFormFieldSchema**</span></span>
  
    
    
<span data-ttu-id="6a81b-307">Ruft das Feldschema als JavaScript Object Notation (JSON) ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-307">Gets the field schema as JavaScript Object Notation (JSON).</span></span>
  
    
    



```cs
public override Dictionary<string, object> GetJsonClientFormFieldSchema(SPControlMode mode)
```

 <span data-ttu-id="6a81b-308">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-308">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-309">_mode_ ist die aktuelle Rendermodus wie neu, bearbeiten oder anzeigen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-309">_mode_ is the current rendering mode such as New, Edit, or Display.</span></span>
  
    
    
 <span data-ttu-id="6a81b-310">**ValidateAndParseValue**</span><span class="sxs-lookup"><span data-stu-id="6a81b-310">**ValidateAndParseValue**</span></span>
  
    
    
<span data-ttu-id="6a81b-311">Überprüft, ob das angegebene Listenelement nicht null ist, und klicken Sie dann überprüft, ob die Zeichenfolge ist Übereinstimmung Open geografische Consortium (OGC) Standards strukturiert und gibt ihn als ein Objekt, das in der **SPFieldGeolocationValue** -Typ ist.</span><span class="sxs-lookup"><span data-stu-id="6a81b-311">Verifies that the specified list item is not null and then verifies that the string is structured in compliance with Open Geospatial Consortium (OGC) standards and returns it as an object that is castable to the **SPFieldGeolocationValue** type.</span></span>
  
    
    



```cs
public override object ValidateAndParseValue(SPListItem item, string value)
```

 <span data-ttu-id="6a81b-312">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-312">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-313">_item_ ist ein Listenelement, das mit dem Wert aktualisiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="6a81b-313">_item_ is a list item that is to be updated with the value.</span></span>
    
  
-  <span data-ttu-id="6a81b-314">_value_ ist eine Zeichenfolgendarstellung eines Geolocation-Werts.</span><span class="sxs-lookup"><span data-stu-id="6a81b-314">_value_ is a string representation of a geolocation value.</span></span>
    
  
<span data-ttu-id="6a81b-p115">Die folgenden Methoden sind standard Außerkraftsetzungen von geerbten Methoden, die in SharePoint 2010 waren. Die spezifische Informationen für diese Klasse ist in der folgenden Tabelle.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p115">The following methods are standard overrides of inherited methods that were in SharePoint 2010. The specific information for this class is in the following table.</span></span>
  
    
    


|<span data-ttu-id="6a81b-317">**Methode**</span><span class="sxs-lookup"><span data-stu-id="6a81b-317">**Method**</span></span>|<span data-ttu-id="6a81b-318">**Diese Außerkraftsetzung...**</span><span class="sxs-lookup"><span data-stu-id="6a81b-318">**This override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a81b-319">GetFieldValue (String s)</span><span class="sxs-lookup"><span data-stu-id="6a81b-319">GetFieldValue(String s)</span></span>  <br/> |<span data-ttu-id="6a81b-320">Gibt den angegebenen Wert als ein Objekt, das in SPFieldGeolocationValue ist.</span><span class="sxs-lookup"><span data-stu-id="6a81b-320">Returns the specified value as an Object that is castable to SPFieldGeolocationValue.</span></span>  <br/> |
|<span data-ttu-id="6a81b-321">GetFieldValueAsText (Object o)</span><span class="sxs-lookup"><span data-stu-id="6a81b-321">GetFieldValueAsText(Object o)</span></span>  <br/> |<span data-ttu-id="6a81b-322">GetValidatedString bindet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-322">Wraps GetValidatedString.</span></span>  <br/> |
|<span data-ttu-id="6a81b-323">GetValidatedString (Object o)</span><span class="sxs-lookup"><span data-stu-id="6a81b-323">GetValidatedString(Object o)</span></span>  <br/> |<span data-ttu-id="6a81b-324">Überprüft, ob der angegebene Wert ist mit Open geografische Consortium (OGC) Standards strukturiert und wird als Zeichenfolge zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="6a81b-324">Verifies that the specified value is structured in compliance with Open Geospatial Consortium (OGC) standards and returns it as a string.</span></span>  <br/> |
   

#### <a name="properties"></a><span data-ttu-id="6a81b-325">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-325">Properties</span></span>

 <span data-ttu-id="6a81b-326">**JSLink**</span><span class="sxs-lookup"><span data-stu-id="6a81b-326">**JSLink**</span></span>
  
    
    
<span data-ttu-id="6a81b-327">Ruft den Namen der JavaScript-Datei ab, die die Felder des **SPFieldGeolocation**-Typs rendert, oder legt den Namen fest.</span><span class="sxs-lookup"><span data-stu-id="6a81b-327">Gets or sets the name of the JavaScript file that renders the fields of the **SPFieldGeolocation** type.</span></span>
  
    
    

> <span data-ttu-id="6a81b-328">**Hinweis:** Die JSLink-Eigenschaft wird für Umfrage- oder Ereignislisten nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-328">**Note** The JSLink property is not supported on Survey or Events lists. A SharePoint calendar is an Events list.</span></span> <span data-ttu-id="6a81b-329">Ein SharePoint-Kalender ist eine Ereignisliste.</span><span class="sxs-lookup"><span data-stu-id="6a81b-329">A SharePoint calendar is an Events list.</span></span> 
  
    
    




```cs
public override string JSLink
```

<span data-ttu-id="6a81b-330">Der Standardwert ist "clienttemplates.js| Geolocationfieldtemplate.js|SP.Map.js".</span><span class="sxs-lookup"><span data-stu-id="6a81b-330">The default value is "clienttemplates.js|Geolocationfieldtemplate.js|sp.map.js".</span></span>
  
    
    
 <span data-ttu-id="6a81b-331">**FieldRenderingMobileWebControl**</span><span class="sxs-lookup"><span data-stu-id="6a81b-331">**FieldRenderingMobileWebControl**</span></span>
  
    
    
<span data-ttu-id="6a81b-332">Ruft das **SPMobileGeolocationField** -Objekt, das das Feld gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-332">Gets the **SPMobileGeolocationField** object that renders the field.</span></span>
  
    
    



```cs
public override SPMobileBaseFieldControl FieldRenderingMobileControl
```

<span data-ttu-id="6a81b-333">Diese Eigenschaft ersetzt die veraltete **FieldRenderingMobileControl**.</span><span class="sxs-lookup"><span data-stu-id="6a81b-333">This property replaces the obsolete **FieldRenderingMobileControl**.</span></span>
  
    
    
<span data-ttu-id="6a81b-p117">Die anderen Eigenschaften sind standard Außerkraftsetzungen von geerbten Eigenschaften, die in SharePoint 2010 waren. Die spezifische Informationen für diese Klasse ist in der folgenden Tabelle.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p117">The other properties are standard overrides of inherited properties that were in SharePoint 2010. The specific information for this class is in the following table.</span></span>
  
    
    


|<span data-ttu-id="6a81b-336">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="6a81b-336">**Property**</span></span>|<span data-ttu-id="6a81b-337">**Die Überschreibung...**</span><span class="sxs-lookup"><span data-stu-id="6a81b-337">**The override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a81b-338">FieldValueType</span><span class="sxs-lookup"><span data-stu-id="6a81b-338">FieldValueType</span></span>  <br/> |<span data-ttu-id="6a81b-339">Gibt **typeof(SPFieldGeolocationValue)**zurück.</span><span class="sxs-lookup"><span data-stu-id="6a81b-339">Returns **typeof(SPFieldGeolocationValue)**.</span></span>  <br/> |
|<span data-ttu-id="6a81b-340">FieldRenderingControl</span><span class="sxs-lookup"><span data-stu-id="6a81b-340">FieldRenderingControl</span></span>  <br/> |<span data-ttu-id="6a81b-341">Gibt ein **GeolocationFieldControl** -Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="6a81b-341">Returns a **GeolocationFieldControl** object.</span></span> <br/> |
|<span data-ttu-id="6a81b-342">Filterbar</span><span class="sxs-lookup"><span data-stu-id="6a81b-342">Filterable</span></span>  <br/> |<span data-ttu-id="6a81b-343">Gibt **false**zurück.</span><span class="sxs-lookup"><span data-stu-id="6a81b-343">Returns **false**.</span></span>  <br/> |
|<span data-ttu-id="6a81b-344">Sortierbar</span><span class="sxs-lookup"><span data-stu-id="6a81b-344">Sortable</span></span>  <br/> |<span data-ttu-id="6a81b-345">Gibt **false**zurück.</span><span class="sxs-lookup"><span data-stu-id="6a81b-345">Returns **false**.</span></span>  <br/> |
|<span data-ttu-id="6a81b-346">Veraltet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-346">[Obsolete]</span></span>  <br/> <span data-ttu-id="6a81b-347">FieldRenderingMobileControl</span><span class="sxs-lookup"><span data-stu-id="6a81b-347">FieldRenderingMobileControl</span></span>  <br/> |<span data-ttu-id="6a81b-348">Gibt ein **SPMobileGeolocationField** -Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="6a81b-348">Returns a **SPMobileGeolocationField** object.</span></span> <br/> |
   

### <a name="spfieldgeolocationvalue-class"></a><span data-ttu-id="6a81b-349">SPFieldGeolocationValue-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-349">SPFieldGeolocationValue class</span></span>

<span data-ttu-id="6a81b-350">Stellt ein Verzeichnis auf der ganzen Welt zu durch Längengrad, Breiten- und möglicherweise Höhe definiert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-350">Represents a location on the globe defined by longitude, latitude, and possibly altitude too.</span></span>
  
    
    

```cs
public class SPFieldGeolocationValue : SPFieldGeographyValue
```


#### <a name="constructors-overloaded"></a><span data-ttu-id="6a81b-351">Konstruktoren (überladen)</span><span class="sxs-lookup"><span data-stu-id="6a81b-351">Constructors (overloaded)</span></span>

<span data-ttu-id="6a81b-352">Initialisiert eine neue Instanz der **SPFieldGeolocationValue** -Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-352">Initializes a new instance of the **SPFieldGeolocationValue** class.</span></span>
  
    
    

```cs
public SPFieldGeolocationValue()
public SPFieldGeolocationValue(string fieldValue)
public SPFieldGeolocationValue(double latitude, double longitude)
public SPFieldGeolocationValue(double latitude, double longitude, double altitude, double measure)

```

 <span data-ttu-id="6a81b-353">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-353">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-354">_fieldValue_ ist eine Zeichenfolge in einem der folgenden Formate Well-Known Text (WKT):</span><span class="sxs-lookup"><span data-stu-id="6a81b-354">_fieldValue_ is a string in one of the following Well-Known Text (WKT) formats:</span></span>
    
  - <span data-ttu-id="6a81b-355">"Point ( _longitude_ _latitude_)", wobei  _longitude_ und _latitude_ Zeichenfolgen aus einer oder mehreren Ziffern, optional einschließlich pro Periode sind (der als Dezimaltrennzeichen interpretiert wird) und optional beginnend mit einem Bindestrich (der als ein negatives interpretiert wird).</span><span class="sxs-lookup"><span data-stu-id="6a81b-355">"Point( _longitude_ _latitude_)", where  _longitude_ and _latitude_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
  - <span data-ttu-id="6a81b-356">"Punkt (_longitude_ _latitude_ _altitude_ _measure_), wobei _longitude_, _latitude_, _altitude_ und _measure_ Zeichenfolgen aus einer oder mehreren Ziffern sind, die optional einen Punkt enthalten (der als Dezimaltrennzeichen interpretiert wird) und optional mit einem Bindestrich beginnen (der als negatives Zeichen interpretiert wird).</span><span class="sxs-lookup"><span data-stu-id="6a81b-356">"Point( longitude latitude)", where  longitude and latitude are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
-  <span data-ttu-id="6a81b-357">_latitude_ ist die Breite und muss zwischen 90,0 und 90,0.</span><span class="sxs-lookup"><span data-stu-id="6a81b-357">_latitude_ is the latitude and must be between -90.0 and 90.0.</span></span>
    
  
-  <span data-ttu-id="6a81b-358">_longitude_ ist die Längengrad und muss zwischen 180,0 und 180,0.</span><span class="sxs-lookup"><span data-stu-id="6a81b-358">_longitude_ is the longitude and must be between -180.0 and 180.0.</span></span>
    
  
-  <span data-ttu-id="6a81b-359">_altitude_ ist die Höhe an.</span><span class="sxs-lookup"><span data-stu-id="6a81b-359">_altitude_ is the altitude.</span></span>
    
  
-  <span data-ttu-id="6a81b-p118">_measure_ ist eine alternative Bezeichnung des Punkts. Siehe **Measure** -Eigenschaft weiter unten in diesem Abschnitt Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p118">_measure_ is an alternate designation of the point. See the **Measure** property later in this section for more information.</span></span>
    
  

#### <a name="methods"></a><span data-ttu-id="6a81b-362">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-362">Methods</span></span>

 <span data-ttu-id="6a81b-363">**ToString**</span><span class="sxs-lookup"><span data-stu-id="6a81b-363">**toString()**</span></span>
  
    
    
<span data-ttu-id="6a81b-364">Diese Außerkraftsetzung gibt eine der folgenden, je nachdem, ob der **Altitude** oder **Measure** -Eigenschaft einen Wert ungleich Null zugewiesen wurden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-364">This override returns one of the following, depending on whether the **Altitude** or **Measure** properties have been assigned a non-null value.</span></span>
  
    
    

- <span data-ttu-id="6a81b-365">Wenn weder Höhe noch Measure einen Null-Wert zugewiesen wurde:</span><span class="sxs-lookup"><span data-stu-id="6a81b-365">If neither Altitude nor Measure have been assigned a non-null value:</span></span>
    
    <span data-ttu-id="6a81b-366">"Point ( _longitude_ _latitude_)", wobei  _longitude_ und _latitude_ Zeichenfolgen aus einer oder mehreren Ziffern, optional einschließlich pro Periode sind (der als Dezimaltrennzeichen interpretiert wird) und optional beginnend mit einem Bindestrich (der als ein negatives interpretiert wird).</span><span class="sxs-lookup"><span data-stu-id="6a81b-366">"Point( _longitude_ _latitude_)", where  _longitude_ and _latitude_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
- <span data-ttu-id="6a81b-367">Andernfalls (mindestens einer der beiden Eigenschaften **Altitude** oder **Measure** wurde ein anderer Wert als Null zugewiesen):</span><span class="sxs-lookup"><span data-stu-id="6a81b-367">Otherwise (at least one of **Altitude** or **Measure** have been assigned a non-null value):</span></span>
    
    <span data-ttu-id="6a81b-368">"Punkt (longitude latitude altitude measure), wobei _longitude_,  _latitude_, _altitude_ und _measure_ Zeichenfolgen aus einer oder mehreren Ziffern sind, die optional einen Punkt enthalten (der als Dezimaltrennzeichen interpretiert wird) und optional mit einem Bindestrich beginnen (der als negatives Zeichen interpretiert wird).</span><span class="sxs-lookup"><span data-stu-id="6a81b-368">"Point( _longitude_ _latitude_)", where  _longitude_ and _latitude_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span> <span data-ttu-id="6a81b-369">Wenn **Altitude** oder **Measure** kein anderer Wert als Null zugewiesen wurde, wird der Wert der Eigenschaft **WellKnownText** als 0 gemeldet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-369">If either **Altitude** or **Measure** has not been assigned a non-null value, it is reported as "0" in the value of the **WellKnownText** property.</span></span> <span data-ttu-id="6a81b-370">Wenn **Altitude** oder **Measure** als 0 gemeldet werden, kann dies daran liegen, dass den Eigenschaften nie ein anderer Wert als Null zugewiesen wurde, aber es kann auch daran liegen, dass eine 0 zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-370">The converse does not hold: if either **Altitude** or **Measure** is reported as 0, that might be because it was never assigned a non-null value, but it might be because it was assigned 0.</span></span>
    
  



```cs

public override string ToString()
```

 <span data-ttu-id="6a81b-371">**ToWellKnownText**</span><span class="sxs-lookup"><span data-stu-id="6a81b-371">**ToWellKnownText**</span></span>
  
    
    
<span data-ttu-id="6a81b-372">**ToString**bindet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-372">Wraps **ToString**.</span></span>
  
    
    



```cs
public string ToWellKnownText()
```


#### <a name="properties"></a><span data-ttu-id="6a81b-373">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-373">Properties</span></span>

 <span data-ttu-id="6a81b-374">**Altitude**</span><span class="sxs-lookup"><span data-stu-id="6a81b-374">**Altitude**</span></span>
  
    
    
<span data-ttu-id="6a81b-p120">Dient zum Abrufen oder festlegen die Höhe des Speicherorts. Die Verwendung dieser Eigenschaft ist optional und die angenommenen--Einheit (beispielsweise Meter) und Nullpunkt (beispielsweise gefährliche Ebene oder Center der Erde) ist benutzerdefiniert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p120">Gets or sets the altitude of the location. Use of this property is optional and the assumed unit-of-measure (for example, meters) and zero-point (for example, sea level or center-of-the-earth) is user-defined.</span></span>
  
    
    



```cs
public double Altitude
```

 <span data-ttu-id="6a81b-377">**Latitude**</span><span class="sxs-lookup"><span data-stu-id="6a81b-377">**Latitude**</span></span>
  
    
    
<span data-ttu-id="6a81b-378">Dient zum Abrufen oder Festlegen der Breite des Speicherorts.</span><span class="sxs-lookup"><span data-stu-id="6a81b-378">Gets or sets the latitude of the location.</span></span>
  
    
    



```cs
public double Latitude
```

<span data-ttu-id="6a81b-379">Der Wert muss zwischen 90,0 und 90,0.</span><span class="sxs-lookup"><span data-stu-id="6a81b-379">The value must be between -90.0 and 90.0.</span></span>
  
    
    
 <span data-ttu-id="6a81b-380">**Longitude**</span><span class="sxs-lookup"><span data-stu-id="6a81b-380">**Longitude**</span></span>
  
    
    
<span data-ttu-id="6a81b-381">Dient zum Abrufen oder festlegen die Länge des Speicherorts.</span><span class="sxs-lookup"><span data-stu-id="6a81b-381">Gets or sets the longitude of the location.</span></span>
  
    
    



```cs
public double Longitude
```

<span data-ttu-id="6a81b-382">Der Wert muss zwischen 180,0 und 180,0.</span><span class="sxs-lookup"><span data-stu-id="6a81b-382">The value must be between -180.0 and 180.0..</span></span>
  
    
    
 <span data-ttu-id="6a81b-383">**Measure**</span><span class="sxs-lookup"><span data-stu-id="6a81b-383">**Measure**</span></span>
  
    
    
<span data-ttu-id="6a81b-p121">Ruft ab oder legt eine alternative Bezeichnung des Punkts Speicherort. Wenn der Punkt entlang einer fahren mit Datenpunkten Meilenstein ist, konnte beispielsweise diese Eigenschaft verwendet werden, die die Nummer des Meilensteins enthalten soll, die am nächsten liegt der Punkt ist. Wenn der Punkt in einem öffentlichen camping Bereich mit nummerierten Zeltplätze ist, konnte diese Eigenschaft verwendet werden, die die Anzahl der der nächste Campsite enthalten soll. Die Semantik der-Eigenschaft ist vollständig benutzergesteuerten und deren Verwendung ist optional.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p121">Gets or sets a user-defined alternate designation of the location point. For example, if the point is along a highway with milestone markers, this property could be used to hold the number of the milestone that is nearest to the point. If the point is in a public camping area with numbered campsites, this property could be used to hold the number of the nearest campsite. The semantics of the property are entirely user-determined and its use is optional.</span></span>
  
    
    



```cs
public double Measure
```


### <a name="spfieldtype-enum"></a><span data-ttu-id="6a81b-388">SPFieldType-Enumeration</span><span class="sxs-lookup"><span data-stu-id="6a81b-388">SPFieldType enum</span></span>

<span data-ttu-id="6a81b-389">Diese Enumeration verfügt über ein neuer Wert hinzugefügt wurde:</span><span class="sxs-lookup"><span data-stu-id="6a81b-389">A new value has been added to this enum:</span></span>
  
    
    

```cs
Geolocation
```


### <a name="spphonenotificationcontent-class"></a><span data-ttu-id="6a81b-390">SPPhoneNotificationContent-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-390">SPPhoneNotificationContent class</span></span>

<span data-ttu-id="6a81b-p122">Eine Basisklasse für Klassen, die den Inhalt einer Benachrichtigung Telefon darstellen. Abgeleitete Klassen müssen deklarieren Sie eine oder mehrere Felder oder Eigenschaften, die den Inhalt enthalten und müssen die **PreparePayload** -Methode, um den Inhalt in ein Bytearray transformieren implementieren.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p122">A base class for classes that represent the content of a phone notification. Derived classes must declare one or more fields or properties to hold the content and must implement the **PreparePayload** method to transform the content into a byte array.</span></span>
  
    
    

```cs
public abstract class SPPhoneNotificationContent
```


#### <a name="methods"></a><span data-ttu-id="6a81b-393">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-393">Methods</span></span>

 <span data-ttu-id="6a81b-394">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6a81b-394">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6a81b-p123">Wenn in einer abgeleiteten Klasse implementiert wird, überträgt den Inhalt in ein Bytearray, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird. Es ist keine Standard-Implementierung, damit diese Methode eine abgeleitete Klasse implementiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p123">When implemented in a derived class, transforms the content into a Byte array that is sent over the wire to the notification service. There is no default implementation so a derived class must implement this method.</span></span>
  
    
    



```cs
protected internal abstract byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6a81b-397">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-397">Properties</span></span>

 <span data-ttu-id="6a81b-398">**NotificationType** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-398">**NotificationType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-399">Ruft den Typ der Benachrichtigung (beispielsweise Kacheln oder Toast) für die Inhalte konzipiert ist.</span><span class="sxs-lookup"><span data-stu-id="6a81b-399">Gets the type of notification (for example, tile or toast) for which the content is intended.</span></span>
  
    
    



```cs
public SPPhoneNotificationType NotificationType

```

<span data-ttu-id="6a81b-400">Informationen zu den **SPPhoneNotificationType**finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-400">For information about the **SPPhoneNotificationType**, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-401">**SubscriberType** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-401">**SubscriberType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-402">Ruft den Typ des Abonnenten beispielsweise eine Windows Phone-Gerät ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-402">Gets the type of the subscriber's device, for example, a Windows Phone.</span></span>
  
    
    



```cs

public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6a81b-403">Informationen zu den **SPPhoneNotificationSubscriberType**finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-403">For information about the **SPPhoneNotificationSubscriberType**, see later in this document.</span></span>
  
    
    

### <a name="spphonenotificationresponse-class"></a><span data-ttu-id="6a81b-404">SPPhoneNotificationResponse-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-404">SPPhoneNotificationResponse class</span></span>

<span data-ttu-id="6a81b-405">Stellt das Ergebnis der Versuch, eine Benachrichtigung zu senden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-405">Represents the outcome of an attempt to send a notification.</span></span>
  
    
    

```cs
public class SPPhoneNotificationResponse
```


#### <a name="methods"></a><span data-ttu-id="6a81b-406">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-406">Methods</span></span>

 <span data-ttu-id="6a81b-407">**Create**</span><span class="sxs-lookup"><span data-stu-id="6a81b-407">**Create**</span></span>
  
    
    
<span data-ttu-id="6a81b-408">Erstellt ein **SPPhoneNotificationResponse** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-408">Creates an **SPPhoneNotificationResponse** object.</span></span>
  
    
    



```cs
public static SPPhoneNotificationResponse
Create(SPPhoneNotificationSubscriberType subscriberType, 
SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 <span data-ttu-id="6a81b-409">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-409">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-410">_subscriberType_ ist das Gerät, wie beispielsweise Windows Phone 7.5.</span><span class="sxs-lookup"><span data-stu-id="6a81b-410">_subscriberType_ is the device, such as Windows Phone 7.5.</span></span>
    
  
-  <span data-ttu-id="6a81b-411">_notificationType_ ist der Typ der Benachrichtigung, wie Toast oder Kachel.</span><span class="sxs-lookup"><span data-stu-id="6a81b-411">_notificationType_ is the type of notification, such as toast or tile.</span></span>
    
  
-  <span data-ttu-id="6a81b-412">_response_ ist die HTTP-Antwortobjekt, das vom Server generiert wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-412">_response_ is the HTTP response object that was generated by the server.</span></span>
    
  
<span data-ttu-id="6a81b-413">Weitere Informationen zu **SPPhoneNotificationSubscriberType** und **SPPhoneNotificationType**finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-413">For more information about **SPPhoneNotificationSubscriberType** and **SPPhoneNotificationType**, see later in this document.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6a81b-414">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-414">Properties</span></span>

 <span data-ttu-id="6a81b-415">**NotificationType** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-415">**NotificationType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-416">Ruft den Typ der Benachrichtigung (beispielsweise Toast oder nebeneinander).</span><span class="sxs-lookup"><span data-stu-id="6a81b-416">Gets the type of notification (for example, toast or tile).</span></span>
  
    
    



```cs

public SPPhoneNotificationType NotificationType
```

<span data-ttu-id="6a81b-417">Informationen zu den SPPhoneNotificationType finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-417">For information about the SPPhoneNotificationType, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-418">**ServiceToken** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-418">**ServiceToken** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-419">Ruft das Token des Notification Service, der in der Benachrichtigung verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-419">Gets the token of the notification service that was used in the notification.</span></span>
  
    
    



```cs
public string ServiceToken
```

 <span data-ttu-id="6a81b-420">**StatusCode** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-420">**StatusCode** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-p124">Ruft den HTTP-Statuscode ab. Eine Zeichenfolgenversion einen **HttpStatusCode** -Wert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p124">Gets the HTTP status code. A string version of a **HttpStatusCode** value.</span></span>
  
    
    



```cs
public string StatusCode
```

 <span data-ttu-id="6a81b-423">**SubscriberType**</span><span class="sxs-lookup"><span data-stu-id="6a81b-423">**SubscriberType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-424">Ruft ab oder legt den Typ des Geräts an die die Benachrichtigung gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-424">Gets or sets the type of device to which the notification was sent.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6a81b-425">Informationen zu den **SPPhoneNotificationSubscriberType**finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-425">For information about the **SPPhoneNotificationSubscriberType**, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-426">**TimeStamp** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-426">**TimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-427">Die UTC-Zeit der Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-427">The UTC time of the notification.</span></span>
  
    
    



```cs
public DateTime Timestamp
```


### <a name="spphonenotificationsubscriber-class"></a><span data-ttu-id="6a81b-428">SPPhoneNotificationSubscriber-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-428">SPPhoneNotificationSubscriber class</span></span>

<span data-ttu-id="6a81b-429">Eine Basisklasse für Klassen, die ein-Abonnent auf einer SharePoint-Anwendung serverseitige einstufen Benachrichtigungen darstellen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-429">A base class for classes that represent a subscriber to notifications issued by a server-side SharePoint application.</span></span>
  
    
    

```cs
public abstract class SPPhoneNotificationSubscriber
```


#### <a name="methods"></a><span data-ttu-id="6a81b-430">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-430">Methods</span></span>

<span data-ttu-id="6a81b-431">Benachrichtigen</span><span class="sxs-lookup"><span data-stu-id="6a81b-431">Notify</span></span>
  
    
    
<span data-ttu-id="6a81b-432">Sendet den Inhalt der angegebenen Benachrichtigung an den Abonnenten mit Fehler überprüfen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-432">Sends the specified notification content to the subscriber with error checking.</span></span>
  
    
    



```cs
public SPPhoneNotificationResponse Notify(SPPhoneNotificationContent notificationContent)
```

 <span data-ttu-id="6a81b-433">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-433">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-434">_notificationContent_ werden Informationen über das Ereignis, das die Benachrichtigung auslöste.</span><span class="sxs-lookup"><span data-stu-id="6a81b-434">_notificationContent_ is information about the event that triggered the notification.</span></span>
  
    
    
<span data-ttu-id="6a81b-p125">Diese Methode kann nicht überschrieben werden. Umschließt die abstrakte **NotifyInternal** -Methode, und stellt sicher, dass bestimmte fehlerüberprüfung durchgeführt wird, wenn **NotifyInternal** aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p125">This method cannot be overridden. It wraps the abstract **NotifyInternal** method and ensures that certain error checking is done when **NotifyInternal** is called.</span></span>
  
    
    
<span data-ttu-id="6a81b-437">Weitere Informationen zu den Klassen **SPPhoneNotificationContent** und **SPPhoneNotificationResponse** finden Sie weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-437">For more information about the **SPPhoneNotificationContent** and **SPPhoneNotificationResponse** classes, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-438">**NotifyInternal**</span><span class="sxs-lookup"><span data-stu-id="6a81b-438">**NotifyInternal**</span></span>
  
    
    
<span data-ttu-id="6a81b-439">Wenn Sie in einer abgeleiteten Klasse überschrieben wird, sendet den Inhalt der angegebenen Benachrichtigung an den Abonnenten.</span><span class="sxs-lookup"><span data-stu-id="6a81b-439">When overridden in a derived class, sends the specified notification content to the subscriber.</span></span>
  
    
    



```cs
protected abstract SPPhoneNotificationResponse NotifyInternal(SPPhoneNotificationContent notificationContent);
```

 <span data-ttu-id="6a81b-440">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-440">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-441">_notificationContent_ werden Informationen über das Ereignis, das die Benachrichtigung auslöste.</span><span class="sxs-lookup"><span data-stu-id="6a81b-441">_notificationContent_ is information about the event that triggered the notification.</span></span>
  
    
    
<span data-ttu-id="6a81b-442">Weitere Informationen zu den Klassen **SPPhoneNotificationContent** und **SPPhoneNotificationResponse** finden Sie weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-442">For more information about the **SPPhoneNotificationContent** and **SPPhoneNotificationResponse** classes, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-443">**ToString**</span><span class="sxs-lookup"><span data-stu-id="6a81b-443">**toString()**</span></span>
  
    
    
<span data-ttu-id="6a81b-444">Gibt die ausgewählten Eigenschaften des Objekts als Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="6a81b-444">Returns selected properties of the object as a string.</span></span>
  
    
    



```cs
public override string ToString()
```

<span data-ttu-id="6a81b-445">Die standardmäßige Implementierung enthält die Eigenschaften **ParentWeb**, **ApplicationTag**und **DeviceAppInstanceId**.</span><span class="sxs-lookup"><span data-stu-id="6a81b-445">The default implementation includes the **ParentWeb**, **ApplicationTag**, and **DeviceAppInstanceId** properties.</span></span>
  
    
    
<span data-ttu-id="6a81b-446">Aktualisieren</span><span class="sxs-lookup"><span data-stu-id="6a81b-446">Update</span></span>
  
    
    
<span data-ttu-id="6a81b-447">Speichert ein (möglicherweise geänderten) **SPPhoneNotificationSubscriber** -Objekt an der Website Abonnenten Store.</span><span class="sxs-lookup"><span data-stu-id="6a81b-447">Saves a (possibly changed) **SPPhoneNotificationSubscriber** object to the website's Subscriber Store.</span></span>
  
    
    



```cs
public void Update()
```

 <span data-ttu-id="6a81b-448">**ValidateSubscriberProperties**</span><span class="sxs-lookup"><span data-stu-id="6a81b-448">**ValidateSubscriberProperties**</span></span>
  
    
    
<span data-ttu-id="6a81b-449">Wenn in einer abgeleiteten Klasse implementiert wird, überprüft die ausgewählte Eigenschaften des Objekts.</span><span class="sxs-lookup"><span data-stu-id="6a81b-449">When implemented in a derived class, validates selected properties of the object.</span></span>
  
    
    



```cs
protected abstract void ValidateSubscriberProperties();
```


#### <a name="properties"></a><span data-ttu-id="6a81b-450">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-450">Properties</span></span>

 <span data-ttu-id="6a81b-451">**CustomArgs**</span><span class="sxs-lookup"><span data-stu-id="6a81b-451">**CustomArgs**</span></span>
  
    
    
<span data-ttu-id="6a81b-p126">Dient zum Abrufen oder Festlegen einer benutzerdefinierten Argumente-Zeichenfolge, die den Status des Abonnements Benachrichtigungen darstellt. Diese Zeichenfolge konnte von der Anwendungslogik zur Unterscheidung zwischen seine Benachrichtigung Abonnenten für verschiedene Arten von Benachrichtigungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p126">Gets or sets a custom arguments string which represents the state of the notifications subscription. This string could be used by the application logic to differentiate between its notification subscribers for different kinds of notifications.</span></span>
  
    
    



```cs
public string CustomArgs
```

 <span data-ttu-id="6a81b-454">**DeviceAppInstanceId** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-454">**DeviceAppInstanceId** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-455">Ruft eine ID für die spezifische Instanz der Anwendung auf das Telefon oder anderen mobilen Gerät.</span><span class="sxs-lookup"><span data-stu-id="6a81b-455">Gets an ID for the specific instance of the application on the phone or other mobile device.</span></span>
  
    
    



```cs
public Guid DeviceAppInstanceId
```

 <span data-ttu-id="6a81b-456">**LastModifiedTimeStamp** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-456">**LastModifiedTimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-457">Ruft Datum und Uhrzeit der letzten des Abonnenten Änderung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-457">Gets the date and time when the subscriber was last modified.</span></span>
  
    
    



```cs
public DateTime LastModifiedTimeStamp
```

 <span data-ttu-id="6a81b-458">**RegistrationTimeStamp** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-458">**RegistrationTimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-459">Ruft Datum und Uhrzeit des Abonnenten Wenn registriert für Benachrichtigungen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-459">Gets the date and time when the subscriber registered for notifications.</span></span>
  
    
    



```cs
public DateTime RegistrationTimeStamp
```

 <span data-ttu-id="6a81b-460">**ServiceToken**</span><span class="sxs-lookup"><span data-stu-id="6a81b-460">**ServiceToken** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-461">Ruft ab oder legt diesen fest Channel Übermittlungsinformationen, die von einem Benachrichtigungsdienst, wie etwa Channel-URI benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-461">Gets or sets delivery channel information that is needed by a notification service, such as channel URI.</span></span>
  
    
    



```cs
public string ServiceToken
```

 <span data-ttu-id="6a81b-462">**SubscriberType** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-462">**SubscriberType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-463">Ruft den Typ des Geräts, wie Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6a81b-463">Gets the type of the device, such as Windows Phone 7.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6a81b-464">Informationen über die **SPPhoneNotificationSubscriberType** -Klasse finden Sie weiter unten in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-464">For information about the **SPPhoneNotificationSubscriberType** class, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-465">**User** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-465">**User** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-466">Dient zum Abrufen des registrierten Benutzers für Benachrichtigungen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-466">Gets the user who registered for notifications.</span></span>
  
    
    



```cs
public SPUser User
```


### <a name="spphonenotificationsubscribercollection-class"></a><span data-ttu-id="6a81b-467">SPPhoneNotificationSubscriberCollection-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-467">SPPhoneNotificationSubscriberCollection class</span></span>

<span data-ttu-id="6a81b-p127">Eine Auflistung von pushbenachrichtigungsabonnenten. Das Auflistungsobjekt dauert **Int32** Indexer.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p127">A collection of notification subscribers. The collection object takes **Int32** indexers.</span></span>
  
    
    

```cs
public sealed class SPPhoneNotificationSubscriberCollection : SPBaseCollection
```


#### <a name="properties"></a><span data-ttu-id="6a81b-470">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-470">Properties</span></span>

 <span data-ttu-id="6a81b-471">**Count**</span><span class="sxs-lookup"><span data-stu-id="6a81b-471">**Count**</span></span>
  
    
    
<span data-ttu-id="6a81b-472">Ruft die Anzahl der Elemente in der Auflistung ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-472">Gets the number of items in the collection.</span></span>
  
    
    



```cs
public override int Count
```


### <a name="spphonenotificationsubscribertype-enum"></a><span data-ttu-id="6a81b-473">SPPhoneNotificationSubscriberType-Enumeration</span><span class="sxs-lookup"><span data-stu-id="6a81b-473">SPPhoneNotificationSubscriberType enum</span></span>

<span data-ttu-id="6a81b-474">Gibt einen Typ des Geräts, die Benachrichtigungen erhalten kann.</span><span class="sxs-lookup"><span data-stu-id="6a81b-474">Specifies a type of device that can receive notifications.</span></span>
  
    
    


|<span data-ttu-id="6a81b-475">**Benachrichtigung**</span><span class="sxs-lookup"><span data-stu-id="6a81b-475">**Notification**</span></span>|<span data-ttu-id="6a81b-476">**Gerät**</span><span class="sxs-lookup"><span data-stu-id="6a81b-476">**Device**</span></span>|
|:-----|:-----|
|||
|<span data-ttu-id="6a81b-477">**WP7**</span><span class="sxs-lookup"><span data-stu-id="6a81b-477">**WP7**</span></span> <br/> |<span data-ttu-id="6a81b-478">Windows Phone 7.5</span><span class="sxs-lookup"><span data-stu-id="6a81b-478">Windows Phone 7.5</span></span>  <br/> |
|<span data-ttu-id="6a81b-479">**Custom**</span><span class="sxs-lookup"><span data-stu-id="6a81b-479">**Custom**</span></span> <br/> |<span data-ttu-id="6a81b-480">Nur von Windows Phone 7.5</span><span class="sxs-lookup"><span data-stu-id="6a81b-480">Any device other than Windows Phone 7.5</span></span>  <br/> |
   

### <a name="spphonenotificationtype-enum"></a><span data-ttu-id="6a81b-481">SPPhoneNotificationType-Enumeration</span><span class="sxs-lookup"><span data-stu-id="6a81b-481">SPPhoneNotificationType enum</span></span>

<span data-ttu-id="6a81b-482">Gibt den Typ der Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-482">Specifies the type of notification.</span></span>
  
    
    


|||
|:-----|:-----|
|<span data-ttu-id="6a81b-483">**None**</span><span class="sxs-lookup"><span data-stu-id="6a81b-483">**None**</span></span> <br/> ||
|<span data-ttu-id="6a81b-484">**Tile**</span><span class="sxs-lookup"><span data-stu-id="6a81b-484">**Tile**</span></span> <br/> ||
|<span data-ttu-id="6a81b-485">**Toast**</span><span class="sxs-lookup"><span data-stu-id="6a81b-485">**Toast**</span></span> <br/> ||
|<span data-ttu-id="6a81b-486">**Raw**</span><span class="sxs-lookup"><span data-stu-id="6a81b-486">**Raw**</span></span> <br/> ||
   

### <a name="spweb-class"></a><span data-ttu-id="6a81b-487">SPWeb-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-487">SPWeb class</span></span>

<span data-ttu-id="6a81b-488">Diese Klasse wurden die folgenden Elemente hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6a81b-488">The following members have been added to this class.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6a81b-489">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-489">Methods</span></span>

 <span data-ttu-id="6a81b-490">**DoesPhoneNotificationSubscriberExist**</span><span class="sxs-lookup"><span data-stu-id="6a81b-490">**DoesPhoneNotificationSubscriberExist**</span></span>
  
    
    
<span data-ttu-id="6a81b-491">Ruft einen Wert, der angibt, ob der aktuelle Benutzer ein-Abonnent für die angegebene Instanz der angegebenen app ist.</span><span class="sxs-lookup"><span data-stu-id="6a81b-491">Gets a value that indicates whether the current user is a subscriber for the specified instance of the specified app.</span></span>
  
    
    



```cs
public bool DoesPhoneNotificationSubscriberExist(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6a81b-492">**GetPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6a81b-492">**GetPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6a81b-493">Ruft ein-Abonnent Benachrichtigung mit der angegebenen Anwendung und Telefon IDs aus der Website Abonnementspeicher Benachrichtigungsliste ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-493">Gets a notification subscriber with the specified application and phone IDs from the website's notification Subscription Store list.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriber GetPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6a81b-494">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-494">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-495">_deviceAppInstanceId_ ist die ID für die Instanz der Anwendung auf einem bestimmten Telefon oder Gerät.</span><span class="sxs-lookup"><span data-stu-id="6a81b-495">_deviceAppInstanceId_ is an ID for the instance of the application on a specific phone or device.</span></span>
  
    
    
<span data-ttu-id="6a81b-496">Weitere Informationen über die **SPPhoneNotificationSubscriber** -Klasse finden Sie unter weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-496">For information about the **SPPhoneNotificationSubscriber** class see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-497">**GetPhoneNotificationSubscribers** (überladen)</span><span class="sxs-lookup"><span data-stu-id="6a81b-497">**GetPhoneNotificationSubscribers** (overloaded)</span></span>
  
    
    
<span data-ttu-id="6a81b-498">Ruft eine Auflistung von pushbenachrichtigungsabonnenten aus der Website Abonnementspeicher Benachrichtigungsliste, optional Filterung anhand der IDs der Phone-Anwendungen und möglicherweise auch auf eine der folgenden: der Benutzer oder einige benutzerdefinierte Argumente.</span><span class="sxs-lookup"><span data-stu-id="6a81b-498">Gets a collection of notification subscribers from the website's notification Subscription Store list, optionally filtering on the ID of the phone applications and possibly also on one of the following: the user or some custom arguments.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string customArgs)
```


> <span data-ttu-id="6a81b-499">**Hinweis:** Der Client-Objekt-Modellname lautet **GetPhoneNotificationSubscribersByArgs**.</span><span class="sxs-lookup"><span data-stu-id="6a81b-499">**Note** Client object model name is **GetPhoneNotificationSubscribersByArgs**.</span></span> 
  
    
    




```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string user)

```


> <span data-ttu-id="6a81b-500">**Hinweis:** Der Client-Objekt-Modellname lautet **GetPhoneNotificationSubscribersByUser**.</span><span class="sxs-lookup"><span data-stu-id="6a81b-500">**Note** Client object model name is **GetPhoneNotificationSubscribersByUser**.</span></span> 
  
    
    

 <span data-ttu-id="6a81b-501">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-501">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-502">_customArgs_ sind zusätzliche benutzerdefinierte Informationen, die möglicherweise einige Benachrichtigung-aktivierte Anwendungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-502">_customArgs_ are additional custom information that some notification-enabled applications may use.</span></span>
    
  
-  <span data-ttu-id="6a81b-503">_user_ ist der Benutzer, die für die Benachrichtigungen registriert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-503">_user_ is the user who registered for the notifications.</span></span>
    
  
<span data-ttu-id="6a81b-504">Weitere Informationen über die **SPPhoneNotificationSubscriberCollection** -Klasse finden Sie unter weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-504">For information about the **SPPhoneNotificationSubscriberCollection** class see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-505">**RegisterPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6a81b-505">**RegisterPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6a81b-506">Phone-app auf einem Telefon zum Empfangen von Benachrichtigungen registriert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-506">Registers a phone app on a phone to receive notifications.</span></span>
  
    
    



```cs

public SPPhoneNotificationSubscriber RegisterPhoneNotificationSubscriber(SPPhoneNotificationSubscriberType subscriberType, Guid deviceAppInstanceId, string serviceToken)
```

 <span data-ttu-id="6a81b-507">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-507">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-508">_subscriberType_ ist der Typ des Geräts, wie Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6a81b-508">_subscriberType_ is the device type, such as Windows Phone 7.</span></span>
    
  
-  <span data-ttu-id="6a81b-509">_deviceAppInstanceId_ ist die ID für die Instanz der app auf einem bestimmten Telefon oder Gerät.</span><span class="sxs-lookup"><span data-stu-id="6a81b-509">_deviceAppInstanceId_ is an ID for the instance of the app on a specific phone or device.</span></span>
    
  
-  <span data-ttu-id="6a81b-510">_serviceToken_ ist das Token, das vom Benachrichtigungsdienst verwendet wird, die an den Abonnenten Benachrichtigung sendet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-510">_serviceToken_ is the token that is used by the notification service that sends notifications to the subscriber.</span></span>
    
  
<span data-ttu-id="6a81b-511">Informationen zu **SPPhoneNotificationSubscriberType**finden Sie weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-511">For information about **SPPhoneNotificationSubscriberType**, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6a81b-512">**UnregisterPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6a81b-512">**UnregisterPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6a81b-513">Hebt die Registrierung einer Phone-app auf einem Telefon aus den Empfang von Benachrichtigungen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-513">Unregisters a phone app on a phone from receiving notifications.</span></span>
  
    
    



```cs
public void UnregisterPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6a81b-514">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-514">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6a81b-515">_deviceAppInstanceId_ ist die ID für die Instanz der app auf einem bestimmten Telefon oder Gerät.</span><span class="sxs-lookup"><span data-stu-id="6a81b-515">_deviceAppInstanceId_ is an ID for the instance of the app on a specific phone or device.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6a81b-516">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-516">Properties</span></span>

 <span data-ttu-id="6a81b-517">**PhoneNotificationSubscribers** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-517">**PhoneNotificationSubscribers** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-518">Ruft eine Auflistung aller das Telefon pushbenachrichtigungsabonnenten anmelden Abonnenten der Website ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-518">Gets a collection of all the phone notification subscribers in the website's Subscriber Store.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection PhoneNotificationSubscribers
```

<span data-ttu-id="6a81b-519">Informationen über die **SPPhoneNotificationSubscriberCollection** -Klasse finden Sie weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-519">For information about the **SPPhoneNotificationSubscriberCollection** class, see earlier in this document.</span></span>
  
    
    

### <a name="wp7notificationtilecontent-class"></a><span data-ttu-id="6a81b-520">WP7NotificationTileContent-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-520">WP7NotificationTileContent class</span></span>

<span data-ttu-id="6a81b-521">Stellt den Inhalt der Benachrichtigung über eine Kachel dar.</span><span class="sxs-lookup"><span data-stu-id="6a81b-521">Represents the content of a tile notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationTileContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6a81b-522">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-522">Constructors</span></span>

<span data-ttu-id="6a81b-523">Initialisiert eine neue Instanz der WP7NotificationTileContent-Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-523">Initializes a new instance of the WP7NotificationTileContent class.</span></span>
  
    
    

```cs
public WP7NotificationTileContent()
```


#### <a name="methods"></a><span data-ttu-id="6a81b-524">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-524">Methods</span></span>

 <span data-ttu-id="6a81b-525">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6a81b-525">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6a81b-526">Überträgt den Inhalt in ein Array von **Byte**, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-526">Transforms the content into a **Byte** array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6a81b-527">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-527">Properties</span></span>

 <span data-ttu-id="6a81b-528">**Count**</span><span class="sxs-lookup"><span data-stu-id="6a81b-528">**Count**</span></span>
  
    
    
<span data-ttu-id="6a81b-p128">Dient zum Abrufen oder festlegen die Anzahl der Benachrichtigung. Muss zwischen-1 bis 99 inklusive sein.</span><span class="sxs-lookup"><span data-stu-id="6a81b-p128">Gets or sets the count of the notification. Must be from -1 to 99 inclusive.</span></span>
  
    
    



```cs
public int Count
```

<span data-ttu-id="6a81b-531">Das Festlegen von-1 wird die Anzahl die nicht über die Kachel geändert.</span><span class="sxs-lookup"><span data-stu-id="6a81b-531">Setting the property to -1 will not change the count over the tile.</span></span>
  
    
    
 <span data-ttu-id="6a81b-532">**Title**</span><span class="sxs-lookup"><span data-stu-id="6a81b-532">**Title**</span></span>
  
    
    
<span data-ttu-id="6a81b-533">Dient zum Abrufen oder Festlegen des Titels der Kachel-Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-533">Gets or sets the title of the tile notification.</span></span>
  
    
    



```cs
public string Title
```

 <span data-ttu-id="6a81b-534">**BackgroundImagePath**</span><span class="sxs-lookup"><span data-stu-id="6a81b-534">**BackgroundImagePath**</span></span>
  
    
    
<span data-ttu-id="6a81b-535">Ruft ab oder legt den Pfad auf die Kachel Hintergrundbild.</span><span class="sxs-lookup"><span data-stu-id="6a81b-535">Gets or sets the path to the tile's background image.</span></span>
  
    
    



```cs
public string BackgroundImagePath
```

 <span data-ttu-id="6a81b-536">**BackBackgroundImagePath**</span><span class="sxs-lookup"><span data-stu-id="6a81b-536">**BackBackgroundImagePath**</span></span>
  
    
    
<span data-ttu-id="6a81b-537">Ruft ab oder legt diesen fest das Hintergrundbild des der Rückseite des eine Invertierung Kachel.</span><span class="sxs-lookup"><span data-stu-id="6a81b-537">Gets or sets the background image of the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackBackgroundImagePath
```

 <span data-ttu-id="6a81b-538">**BackContent**</span><span class="sxs-lookup"><span data-stu-id="6a81b-538">**BackContent**</span></span>
  
    
    
<span data-ttu-id="6a81b-539">Ruft ab oder legt den Inhalt der Rückseite des eine Invertierung Kachel.</span><span class="sxs-lookup"><span data-stu-id="6a81b-539">Gets or sets the content of the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackContent
```

 <span data-ttu-id="6a81b-540">**BackTitle**</span><span class="sxs-lookup"><span data-stu-id="6a81b-540">**BackTitle**</span></span>
  
    
    
<span data-ttu-id="6a81b-541">Ruft ab oder legt des Titels, die auf der Rückseite des eine Invertierung Kachel angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-541">Gets or sets of the title that appears on the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackTitle
```

 <span data-ttu-id="6a81b-542">**TileId**</span><span class="sxs-lookup"><span data-stu-id="6a81b-542">**TileId**</span></span>
  
    
    
<span data-ttu-id="6a81b-543">Dient zum Abrufen oder Festlegen der ID der Kachel.</span><span class="sxs-lookup"><span data-stu-id="6a81b-543">Gets or sets the ID of the tile.</span></span>
  
    
    



```cs
public string TileId
```


### <a name="wp7notificationtoastcontent-class"></a><span data-ttu-id="6a81b-544">WP7NotificationToastContent-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-544">WP7NotificationToastContent class</span></span>

<span data-ttu-id="6a81b-545">Stellt den Inhalt der ein Toast-Benachrichtigung an.</span><span class="sxs-lookup"><span data-stu-id="6a81b-545">Represents the content of a toast notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationToastContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6a81b-546">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-546">Constructors</span></span>

<span data-ttu-id="6a81b-547">Initialisiert eine neue Instanz der WP7NotificationToastContent-Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-547">Initializes a new instance of the WP7NotificationToastContent class.</span></span>
  
    
    

```cs
public WP7NotificationToastContent()
```


#### <a name="methods"></a><span data-ttu-id="6a81b-548">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-548">Methods</span></span>

 <span data-ttu-id="6a81b-549">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6a81b-549">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6a81b-550">Überträgt den Inhalt in ein Array von **Byte**, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-550">Transforms the content into a **Byte** array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6a81b-551">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-551">Properties</span></span>

 <span data-ttu-id="6a81b-552">**Meldung**</span><span class="sxs-lookup"><span data-stu-id="6a81b-552">**Message**</span></span>
  
    
    
<span data-ttu-id="6a81b-553">Dient zum Abrufen oder Festlegen der Meldung von Toast-Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-553">Gets or sets the message of the toast notification.</span></span>
  
    
    



```cs
public string Message
```

 <span data-ttu-id="6a81b-554">**Title**</span><span class="sxs-lookup"><span data-stu-id="6a81b-554">**Title**</span></span>
  
    
    
<span data-ttu-id="6a81b-555">Dient zum Abrufen oder Festlegen des Titels der Toast-Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-555">Gets or sets the title of the toast notification.</span></span>
  
    
    



```cs
public string Title
```

 <span data-ttu-id="6a81b-556">**Param**</span><span class="sxs-lookup"><span data-stu-id="6a81b-556">**Param**</span></span>
  
    
    
<span data-ttu-id="6a81b-557">Ruft ab oder legt diesen fest benutzerdefinierte Einstellungsdaten, die an die empfangende Anwendung übergeben wird, wenn der Benutzer auf die Toast-Benachrichtigung antwortet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-557">Gets or sets custom settings data that is passed to the receiving application if the user responds to the toast notification.</span></span>
  
    
    



```cs
public string Param
```

<span data-ttu-id="6a81b-558">Diese Eigenschaft kann zum Übergeben von Informationen an die empfangende Anwendung wie eine URL oder eine Reihe von Name / Wert-Paare verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6a81b-558">This property can be used to pass information to the receiving application such as a URL or a set of name-value pairs.</span></span>
  
    
    

### <a name="wp7notificationrawcontent-class"></a><span data-ttu-id="6a81b-559">WP7NotificationRawContent-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-559">WP7NotificationRawContent class</span></span>

<span data-ttu-id="6a81b-560">Stellt den Inhalt einer unformatierte Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-560">Represents the content of a raw notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationRawContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6a81b-561">Konstruktoren</span><span class="sxs-lookup"><span data-stu-id="6a81b-561">Constructors</span></span>

<span data-ttu-id="6a81b-562">Initialisiert eine neue Instanz der WP7NotificationRawContent-Klasse.</span><span class="sxs-lookup"><span data-stu-id="6a81b-562">Initializes a new instance of the WP7NotificationRawContent class.</span></span>
  
    
    

```cs
public WP7NotificationRawContent()
```


#### <a name="methods"></a><span data-ttu-id="6a81b-563">Methoden</span><span class="sxs-lookup"><span data-stu-id="6a81b-563">Methods</span></span>

 <span data-ttu-id="6a81b-564">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6a81b-564">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6a81b-565">Überträgt den Inhalt in ein Bytearray, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="6a81b-565">Transforms the content into a Byte array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6a81b-566">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-566">Properties</span></span>

 <span data-ttu-id="6a81b-567">**Meldung**</span><span class="sxs-lookup"><span data-stu-id="6a81b-567">**Message**</span></span>
  
    
    
<span data-ttu-id="6a81b-568">Dient zum Abrufen oder festlegen die Meldung, die der unformatierte Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-568">Gets or sets the message of the raw notification.</span></span>
  
    
    



```cs
public string Message
```


### <a name="wp7phonenotificationresponse-class"></a><span data-ttu-id="6a81b-569">WP7PhoneNotificationResponse-Klasse</span><span class="sxs-lookup"><span data-stu-id="6a81b-569">WP7PhoneNotificationResponse class</span></span>

<span data-ttu-id="6a81b-570">Stellt das Ergebnis der Versuch, eine Benachrichtigung an eine Windows Phone 7-Abonnenten gesendet.</span><span class="sxs-lookup"><span data-stu-id="6a81b-570">Represents the outcome of an attempt to send a notification to a Windows Phone 7 subscriber.</span></span>
  
    
    

```cs
public WP7PhoneNotificationResponse(SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 <span data-ttu-id="6a81b-571">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a81b-571">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6a81b-572">_notificationType_ ist der Typ der Benachrichtigung, wie Toast oder Kachel.</span><span class="sxs-lookup"><span data-stu-id="6a81b-572">_notificationType_ is the type of notification, such as toast or tile.</span></span>
    
  
-  <span data-ttu-id="6a81b-573">_response_ ist die HTTP-Antwortobjekt, das vom Server generiert wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-573">_response_ is the HTTP response object that was generated by the server.</span></span>
    
  
<span data-ttu-id="6a81b-574">Weitere Informationen zu **SPPhoneNotificationType**finden Sie unter weiter oben in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6a81b-574">For more information about **SPPhoneNotificationType**, see earlier in this document.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6a81b-575">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a81b-575">Properties</span></span>

 <span data-ttu-id="6a81b-576">**NotificationStatus** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-576">**NotificationStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-577">Ruft den Status der Benachrichtigung, beispielsweise Erfolg oder das fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="6a81b-577">Gets the notification status, for example, success or failure.</span></span>
  
    
    



```cs
public string NotificationStatus
```

 <span data-ttu-id="6a81b-578">**DeviceConnectionStatus** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-578">**DeviceConnectionStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-579">Ruft den Status des Geräts zum Zeitpunkt der Benachrichtigung ab.</span><span class="sxs-lookup"><span data-stu-id="6a81b-579">Gets the status of the device at the time of the notification.</span></span>
  
    
    



```cs
public string DeviceConnectionStatus
```

 <span data-ttu-id="6a81b-580">**SubscriptionStatus** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-580">**SubscriptionStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-581">Der Abonnementstatus des Geräts zum Zeitpunkt der Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="6a81b-581">The subscription status of the device at the time of the notification.</span></span>
  
    
    



```cs
public string SubscriptionStatus
```

 <span data-ttu-id="6a81b-582">**MessageId** (schreibgeschützt)</span><span class="sxs-lookup"><span data-stu-id="6a81b-582">**MessageId** (read-only)</span></span>
  
    
    
<span data-ttu-id="6a81b-583">Ruft die ID der Nachricht, die in der Benachrichtigung gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="6a81b-583">Gets the ID of the message that was sent in the notification.</span></span>
  
    
    



```
public string MessageId
```


## <a name="additional-resources"></a><span data-ttu-id="6a81b-584">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6a81b-584">Additional resources</span></span>
<span data-ttu-id="6a81b-585"><a name="SP15MobileOM_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6a81b-585"></span></span>


-  [<span data-ttu-id="6a81b-586">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="6a81b-586">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="6a81b-587">Vorgehensweise: Konfigurieren und Verwenden von Pushbenachrichtigungen in SharePoint-apps für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="6a81b-587">How to: Configure and use push notifications in SharePoint apps for Windows Phone</span></span>](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [<span data-ttu-id="6a81b-588">Integrieren von Standort- und Kartenfunktionen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a81b-588">Integrating location and map functionality in SharePoint</span></span>](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6a81b-589">Übersicht über das SharePoint-Objektmodell für die mobile Clientauthentifizierung</span><span class="sxs-lookup"><span data-stu-id="6a81b-589">Overview of the SharePoint mobile client authentication object model</span></span>](overview-of-the-sharepoint-mobile-client-authentication-object-model.md)
    
  

