---
title: Add-In-Autorisierungsrichtlinientypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1a5d59656cb15f023b57b912c0cd248352931b2e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="add-in-authorization-policy-types-in-sharepoint"></a><span data-ttu-id="dd07b-102">Add-In-Autorisierungsrichtlinientypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd07b-102">Add-in authorization policy types in SharePoint</span></span>
<span data-ttu-id="dd07b-p101">Erfahren Sie mehr über die verschiedenen Autorisierungsrichtlinien für Add-Ins in SharePoint: Nur-Add-In-Richtlinie, Benutzer-und-Add-In-Richtlinie und Nur-Benutzer-Richtlinie. Außerdem werden Richtlinien für die Verwendung der Nur-Add-In-Richtlinie bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p101">Learn about the different authorization policies for add-ins in SharePoint: add-in-only policy, user+add-in policy, and user-only policy. It also provides guidelines for using add-in-only policy.</span></span>
 

 <span data-ttu-id="dd07b-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="dd07b-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="dd07b-108">Bevor Sie diesen Artikel lesen, sollten Sie sich zuerst mit den Artikeln [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md) und [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins](context-token-oauth-flow-for-sharepoint-add-ins.md) vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="dd07b-108">Before reading this article, you should first be familiar with the articles  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md) and [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md).</span></span>
 

## <a name="get-an-overview-of-add-in-authorization-policies-types"></a><span data-ttu-id="dd07b-109">Übersicht über Add-In-Autorisierungsrichtlinientypen</span><span class="sxs-lookup"><span data-stu-id="dd07b-109">Get an overview of add-in authorization policies types</span></span>
<span data-ttu-id="dd07b-110"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-110"></span></span>

<span data-ttu-id="dd07b-111">SharePoint bietet drei Arten von Autorisierungsrichtlinien:</span><span class="sxs-lookup"><span data-stu-id="dd07b-111">SharePoint provides three types of authorization policies:</span></span>
 

 

-  <span data-ttu-id="dd07b-p103">**Nur-Benutzer-Richtlinie**: Die Nur-Benutzer-Richtlinie entspricht der Autorisierungsrichtlinie, die beispielsweise auf der Startseite einer SharePoint-Website oder beim Zugriff auf SharePoint-APIs über PowerShell beim erstmaligen Öffnen angewendet wurde. Wenn die Nur-Benutzer-Richtlinie verwendet wird, wird bei den Autorisierungsprüfungen nur die Benutzeridentität berücksichtigt. Diese Richtlinie wird beispielsweise verwendet, wenn der Benutzer direkt auf Ressourcen zugreift, ohne die App zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p103">**User-only policy** — When the user-only policy is used, SharePoint checks only the permissions for the user. SharePoint uses this policy when the user is accessing resources directly without using an add-in, such as when a user first opens a SharePoint website's home page or accesses SharePoint APIs from PowerShell.</span></span>
    
    
    
 
-  <span data-ttu-id="dd07b-p104">**Benutzer-und-Add-In-Richtlinie**: Wenn die Add-In-Richtlinie verwendet wird, wird bei Autorisierungsprüfungen der Inhaltsdatenbank die Benutzer- und Add-In-Identität berücksichtigt. Insbesondere ist bei Verwendung dieser Richtlinie eine Autorisierungsprüfung nur erfolgreich, wenn der aktuelle Benutzer und das Add-In über ausreichende Berechtigungen für die fragliche Aktion verfügt.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p104">**User+add-in policy** —When the user+add-in policy is used, SharePoint checks the permissions of both the user and the add-in principal. Authorization checks succeed only if both the current user and the add-in have permissions to perform the action in question.</span></span>
    
    <span data-ttu-id="dd07b-p105">Diese Richtlinie wird beispielsweise verwendet, wenn eine SharePoint-Add-In auf die Ressourcen eines Benutzers in SharePoint zugreifen möchte. (Der Code in den Remotekomponenten der SharePoint-Add-In muss so konzipiert sein, dass Benutzer-und-Add-In-Aufrufe an SharePoint) erfolgen können.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p105">For example this policy is used when a SharePoint Add-in wants to get access to the user's resources on SharePoint. (The code in the remote components of the SharePoint Add-in have to be designed to make user+add-in calls to SharePoint.)</span></span>
    
    
    
 
-  <span data-ttu-id="dd07b-p106">**Nur-Add-In-Richtlinie**: Wenn die Nur-Add-In-Richtlinie verwendet wird, wird bei der Autorisierungsprüfung nur die Add-In-Identität berücksichtigt. Insbesondere sind bei Verwendung dieser Richtlinie Autorisierungsprüfungen nur erfolgreich, wenn das aktuelle Add-In über ausreichende Berechtigungen verfügen, um die fragliche Aktion auszuführen (unabhängig von den Berechtigungen des aktuellen Benutzers).</span><span class="sxs-lookup"><span data-stu-id="dd07b-p106">**Add-in-only policy** —When the add-in-only policy is used, SharePoint checks only the permissions of the add-in principal. Authorization checks succeed only if the current add-in has sufficient permissions to perform the action in question, regardless of the permissions of the current user (if any).</span></span>
    
    <span data-ttu-id="dd07b-p107">Ein Ausgabengenehmigungs-Add-In ist ein Beispiel eines Add-Ins, das für die Verwendung dieser Richtlinie konzipiert werden kann. Durch dieses Add-In können Benutzer, die ansonsten keine Ausgaben genehmigen können, Ausgaben unter einem bestimmten Betrag genehmigen. In dem Szenario unten finden Sie dazu weitere Details.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p107">An expense approval add-in is an example of an add-in that could be designed to use this policy. The add-in allows users who wouldn't otherwise be able to approve expenses to approve expenses below a certain amount. See the scenario below for details.</span></span> 
    
    
    
     <span data-ttu-id="dd07b-p108">**Hinweis** Bestimmte APIs erfordern einen Benutzerkontext und können nicht mit einer Nur-Add-In-Richtlinie ausgeführt werden. Hierzu gehören viele APIs für die Interaktion mit Project Server 2013 und für Suchabfragen.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p108">**Note**  Certain APIs require a user context and can't be executed with an add-in-only policy. These include many APIs for interacting with Project Server 2013 and for performing search queries.</span></span>

### <a name="see-an-example-scenario-of-an-add-in-that-uses-the-add-in-only-policy"></a><span data-ttu-id="dd07b-125">Hier finden Sie ein Beispielszenario für ein Add-In, das die Nur-Add-In-Richtlinie verwendet:</span><span class="sxs-lookup"><span data-stu-id="dd07b-125">See an example scenario of an add-in that uses the add-in-only policy</span></span>
<span data-ttu-id="dd07b-126"><a name="Scenario"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-126"></span></span>

<span data-ttu-id="dd07b-p109">Angenommen, ein Vertriebsmanager bei Contoso, Adam, kauft eine Kostenvorlage-App, die die Nur-Add-In-Richtlinie verwendet. Beim Kauf des Add-Ins wird Adam aufgefordert, dem Add-In zu erlauben, Benutzerberechtigungen zu erhöhen. Adam erteilt dem Add-In die angeforderte Berechtigung. Anschließend kauft er genügend Lizenzen für alle Contoso-Vertriebsmitarbeiter und installiert das Add-In auf der SharePoint-Website des Vertriebsteams.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p109">Let's says a sales manager at Contoso, Adam, buys an expense submission add-in that uses the add-in-only policy. When Adam chooses to buy the add-in, Adam is prompted to allow the add-in to elevate user permissions; that is, to allow the add-in to make add-in-only calls to SharePoint. Adam grants the add-in the requested permissions. He then purchases enough licenses of the add-in for all of the Contoso sales people, and he installs the add-in in the sales team's SharePoint website.</span></span>
 

 
<span data-ttu-id="dd07b-p110">Bald reichen die Vertriebsmitarbeiter Kostenberichte mit dem neuen Kostenvorlage-Tool (des von Adam erworbenen Kostenvorlage-Add-Ins) ein. Das Add-In verhindert, dass Vertriebsmitarbeiter ihre eigenen Kostenberichte genehmigen. Das Add-In kann sie jedoch genehmigen, da Adam ihr die Berechtigung zum Erhöhen von Benutzerberechtigungen erteilt hat. Adam richtet das Add-In so ein, dass Kostenvorlagen unter 50 € automatisch genehmigt werden und ihm bei Berichten über 50 € automatisch eine Aufgabe zugewiesen wird, diese zu genehmigen. Dies kann implementiert werden, indem das SharePoint-Add-In eine Schreibberechtigung für eine SharePoint-Liste mit genehmigten Ausgaben erhält. Aber unter den Benutzern haben nur Manager der Personalabteilung Schreibberechtigungen für die Liste. Der Code im Add-In wurde so entwickelt, dass ein Nur-Add-In-Aufruf an SharePoint erfolgt, wenn die Ausgabe unter 45 Euro liegt, damit sie der Liste hinzugefügt wird. Da die Berechtigungen des Benutzers nicht überprüft werden, werden alle Benutzerübertragungen unter 45 Euro automatisch zur Liste genehmigter Ausgaben hinzugefügt, selbst wenn der Benutzer nicht über eine Schreibberechtigung für die Liste verfügt.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p110">Soon, the salespeople are submitting expense reports using the new expense submission add-in. Salespeople usually cannot approve their own expense reports, but they can do this when using the add-in because Adam granted it the ability to do this for expense submissions below $50 because he set the add-in to automatically approve reports below $50. The add-in automatically assigns him a task to approve reports of $50 or more. This could be implemented by giving the SharePoint Add-in Write permission to a SharePoint list of approved expenses. But, among users, only human resources managers have Write permission to the list. The code in the add-in is designed to add the expense to the list by making an add-in-only call to SharePoint whenever the expense is less than $50. Since the user's permissions aren't checked, any user's submissions below $50 are automatically added to the approved expenses list, even if the user doesn't have Write permission to the list.</span></span>
 

 

 

 

### <a name="learn-how-add-ins-get-permission-to-use-the-add-in-only-policy"></a><span data-ttu-id="dd07b-138">Informationen über das Anfordern der Berechtigung zur Verwendung der Nur-Add-In-Richtlinie für Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dd07b-138">Learn how add-ins get permission to use the add-in-only policy</span></span>
<span data-ttu-id="dd07b-139"><a name="Approve"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-139"></span></span>

<span data-ttu-id="dd07b-p111">Um Nur-Add-In-Aufrufe an SharePoint ausführen zu können, muss Ihr Add-In die Berechtigung zur Verwendung der Nur-Add-In-Richtlinie anfordern. Diese Anforderung erfolgt im Add-In-Manifest. Fügen Sie dazu das **AllowAppOnlyPolicy**-Attribut zum **AppPermissionRequests**-Element hinzu, und legen Sie es auf **true** fest, wie im folgenden Markup dargestellt:</span><span class="sxs-lookup"><span data-stu-id="dd07b-p111">To be able to make add-in-only calls to SharePoint, your add-in must request permission to use the add-in-only policy. This request is made in the add-in manifest. You do this by adding the  **AllowAppOnlyPolicy** attribute to the **AppPermissionRequests** element and setting it to **true** as shown in the following markup:</span></span>
 

 

```XML
<AppPermissionRequests AllowAppOnlyPolicy="true">
    ...
</AppPermissionRequests>
```


 <span data-ttu-id="dd07b-p112">**Hinweis** SharePoint-Add-Ins hießen ursprünglich „Apps für SharePoint“. Damit eine Abwärtskompatibilität gewährleistet werden kann, wurde das App-Manifestschema nicht geändert, sodass möglicherweise die Zeichenfolge „App“ in Elementen und Attributnamen angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p112">**Note**  SharePoint Add-ins used to be called "apps for SharePoint". To maintain backward compatibility, the app manifest schema was not changed, so the string "app" appears in may element and attribute names.</span></span>
 

<span data-ttu-id="dd07b-p113">Ein Benutzer wird bei der Installation des Add-Ins dazu aufgefordert, diese Anforderung zu genehmigen. Wenn das Add-In nach den Mandanten-Berechtigungen fragt, kann nur ein Mandanten-Administrator die Verwendung der Nur-Add-In-Richtlinie genehmigen, also kann nur ein Mandanten-Administrator das Add-In installieren. Wenn das Add-In keine höheren Berechtigungen erfordert als die auf der Ebene der Websitesammlung fragt das Add-In nach keinen Berechtigungen dafür, anschließend kann ein Website-Administrator das Add-In installieren. Weitere Informationen zu Berechtigungsbereichen finden Sie unter  [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="dd07b-p113">A user installing the add-in will be prompted to approve this request. If the add-in asks for tenant-scoped permissions, then only a tenant administrator can grant use of the add-in-only policy, so only a tenant administrator can install the add-in. If the add-in does not ask for any permissions scoped higher than site collection, then a site collection administrator can install the add-in. For more information about permission scopes, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 

 

### <a name="learn-how-add-ins-make-add-in-only-calls"></a><span data-ttu-id="dd07b-149">Informationen zum Durchführen von Nur-Add-In-Aufrufen mit Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dd07b-149">Learn how add-ins make add-in-only calls</span></span>
<span data-ttu-id="dd07b-150"><a name="AppOnlyCalls"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-150"></span></span>

<span data-ttu-id="dd07b-p114">Der Unterschied zwischen einem Nur-Add-In-Aufruf an SharePoint und einem Benutzer-und-Add-In-Aufruf ist der Typ des Zugriffstokens, das im Aufruf enthalten ist. Im folgenden Code sind die Benutzer-und-Add-In- und Nur-Add-In-Zugriffstokens im verwalteten Code dargestellt. Die detaillierte Programmierung erfolgt in der Datei TokenHelper.cs (oder .vb), das die Office-Entwicklertools für Visual Studio automatisch zum -Projekt in Visual Studio hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p114">The difference between an add-in-only call to SharePoint and a user+add-in call is the type of access token that is included in the call. The following code shows how to obtain user+add-in and add-in-only access tokens in managed code. The detailed coding is done for you in the TokenHelper.cs (or .vb) file that the Office Developer Tools for Visual Studio automatically add to the project in Visual Studio.</span></span>
 

 

```C#
string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);
if (contextTokenString != null)
{
     //Get context token.
     SharePointContextToken contextToken =
          TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);
     Uri sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);

     //Get user+add-in access token.
     string accessToken =
          TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority).AccessToken;

      ClientContext clientContext =
           TokenHelper.GetClientContextWithAccessToken(sharepointUrl.ToString(), accessToken);

      //Do something. 
       ...
    
      //Get add-in-only access token.
       string addinOnlyAccessToken = 
            TokenHelper.GetAppOnlyAccessToken(contextToken.TargetPrincipalName, 
                              sharepointUrl.Authority, contextToken.Realm).AccessToken;
         //Do something.
         ...
}
```


 <span data-ttu-id="dd07b-p115">**Hinweis** Add-Ins, die keine mit OAuth authentifizierten Aufrufe ausgeben (z. B. Add-Ins, die nur aus im Add-In-Web ausgeführtem JavaScript bestehen) können die Nur-Add-In-Richtlinie nicht verwenden. Sie können die Berechtigung anfordern, können sie jedoch nicht nutzen, da hierfür die Übergabe eines Nur-Add-In-OAuth-Tokens erforderlich wäre. Nur Add-Ins mit außerhalb von SharePoint ausgeführten Webanwendungen können Nur-Add-In-Token erstellen und übergeben.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p115">**Note**  Add-ins that do not make OAuth authenticated calls (for example, add-ins that are only JavaScript running in the add-in web) cannot use the add-in-only policy. They can request the permission, but they will not be able to take advantage of it because doing so requires passing an add-in-only OAuth token. Only add-ins with web applications running outside of SharePoint can create and pass add-in-only tokens.</span></span>
 

<span data-ttu-id="dd07b-p116">Im Allgemeinen muss ein aktueller Benutzer vorhanden sein, damit ein Aufruf möglich ist. Bei der Nur-Add-In-Richtlinie wird ein Benutzer SHAREPOINT\APP, ähnlich dem vorhandenen Benutzer SHAREPOINT\SYSTEM erstellt. Alle Nur-Add-In-Anforderungen erfolgen über SHAREPOINT\APP. Es gibt keine Möglichkeit der Authentifizierung als SHAREPOINT\APP über benutzerbasierte Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="dd07b-p116">In general, a current user is required to be present for a call to be made. In the case of add-in-only policy, SharePoint creates a SHAREPOINT\APP, similar to the existing SHAREPOINT\SYSTEM user. All add-in-only requests are made by SHAREPOINT\APP. There is no way to authenticate as SHAREPOINT\APP through user-based authentication.</span></span>
 

 

### <a name="get-guidelines-for-using-the-add-in-only-policy"></a><span data-ttu-id="dd07b-161">Anweisungen für die Verwendung der Nur-Add-In-Richtlinie</span><span class="sxs-lookup"><span data-stu-id="dd07b-161">Get guidelines for using the add-in-only policy</span></span>
<span data-ttu-id="dd07b-162"><a name="GuidelinesFor"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-162"></span></span>

<span data-ttu-id="dd07b-p117">Da durch Nur-Add-In-Aufrufe die Benutzerrechte erhöht werden, sollten Sie hinsichtlich des Erstellens von Add-Ins, die Berechtigungen erfordern, eher zurückhaltend agieren. Aufrufe sollten die Nur-Add-In-Richtlinie nur in folgenden Fällen verwenden:</span><span class="sxs-lookup"><span data-stu-id="dd07b-p117">Since add-in-only calls effectively elevate user privileges, you should be conservative in creating add-ins that ask for permission to make them. Calls should use the add-in-only policy only if:</span></span>
 

 

- <span data-ttu-id="dd07b-165">Die App muss ihre Berechtigungen für einen bestimmten Aufruf über die Berechtigungen des Benutzers hinaus erhöhen (z. B., um einen Kostenbericht unter von der App ausgewerteten Bedingungen zu genehmigen).</span><span class="sxs-lookup"><span data-stu-id="dd07b-165">The add-in needs to elevate its permissions above the user for a specific call; for example, to approve an expense report under conditions evaluated by the add-in.</span></span>
    
 
- <span data-ttu-id="dd07b-166">The add-in is not acting on behalf of any user; for example, an add-in that performs nightly maintenance tasks on a SharePoint document library.</span><span class="sxs-lookup"><span data-stu-id="dd07b-166">The add-in is not acting on behalf of any user; for example, an add-in that performs nightly maintenance tasks on a SharePoint document library.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="dd07b-167">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dd07b-167">Additional resources</span></span>
<span data-ttu-id="dd07b-168"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="dd07b-168"></span></span>


-  [<span data-ttu-id="dd07b-169">Autorisierung und Authentifizierung für Add-Ins in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd07b-169">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="dd07b-170">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd07b-170">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)
    
 
-  [<span data-ttu-id="dd07b-171">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="dd07b-171">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="dd07b-172">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dd07b-172">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="dd07b-173">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dd07b-173">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 

