---
title: "Erhöhten Berechtigungen in SharePoint-Add-ins"
ms.date: 11/03/2017
ms.openlocfilehash: 8102a3acc77efbc492c9ef7e62649851b5388954
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="elevated-privileges-in-sharepoint-add-ins"></a><span data-ttu-id="52ccf-102">Erhöhten Berechtigungen in SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="52ccf-102">Elevated privileges in SharePoint Add-ins</span></span>

<span data-ttu-id="52ccf-103">Verwenden Sie die Richtlinie nur für Apps oder Dienstkonten, um Berechtigungen in SharePoint-Add-ins zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-103">Use the app-only policy or service accounts to elevate privileges in SharePoint Add-ins.</span></span>

<span data-ttu-id="52ccf-104">_**Gilt für:** apps für SharePoint | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="52ccf-104">_**Applies to:** apps for SharePoint | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="52ccf-105">Verschiedene Methoden werden verwendet, um Berechtigungen in SharePoint-Add-ins und Farm Solutions erhöhen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-105">Different methods are used to elevate privileges in SharePoint Add-ins and farm solutions.</span></span> <span data-ttu-id="52ccf-106">Farmlösungen ausweiten Berechtigungen mithilfe von RunWithElevatedPrivileges(SPSecurity.CodeToRunElevated), der auf das Objektmodell für SharePoint Server-Side gehört.</span><span class="sxs-lookup"><span data-stu-id="52ccf-106">Farm solutions elevate privileges by using RunWithElevatedPrivileges(SPSecurity.CodeToRunElevated), which belongs to the SharePoint server-side object model.</span></span> <span data-ttu-id="52ccf-107">SharePoint-Add-ins verwenden, die nur-app Richtlinie oder Dienstkonten.</span><span class="sxs-lookup"><span data-stu-id="52ccf-107">SharePoint Add-ins use either the app-only policy or service accounts.</span></span>

<span data-ttu-id="52ccf-108">Möglicherweise möchten Sie erhöhten in Ihr Add-in verwenden, wenn:</span><span class="sxs-lookup"><span data-stu-id="52ccf-108">You might want to use elevated privileges in your add-in when:</span></span>

* <span data-ttu-id="52ccf-109">Aktionen werden durchgeführt Ihr Add-In für Benutzer, die die Benutzer nicht über ausreichend einzelne Berechtigungen für die Durchführung aufweisen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-109">Your add-in performs actions for users that the users don't have adequate individual permissions to complete.</span></span> <span data-ttu-id="52ccf-110">Administratoren können nicht Benutzern bestimmte Berechtigungen zuweisen, da die Berechtigungsstufe zu hoch ist.</span><span class="sxs-lookup"><span data-stu-id="52ccf-110">Administrators might not assign users certain permissions because the permission level is too high.</span></span>

   <span data-ttu-id="52ccf-111">Ihre Organisation möglicherweise, beispielsweise implementieren eine benutzerdefinierten Websitesammlung Benutzerwebsite, mit denen Benutzer Websitesammlungen erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-111">Your organization might, for example, implement a custom site collection provisioning solution that users must use to create site collections.</span></span> <span data-ttu-id="52ccf-112">Ihre Organisation möglicherweise angeben, dass alle neuen Websitesammlungen bestimmte Listen, Inhaltstypen oder Felder zugeordnet sein müssen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-112">Your organization might specify that all new site collections must have certain lists, content types, or fields associated with them.</span></span> <span data-ttu-id="52ccf-113">Wenn Benutzer Websitesammlungen auf ihre eigenen erstellen, werden sie möglicherweise oder möglicherweise nicht vergessen Sie nicht, diese Objekte auf ihre neue Websitesammlung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-113">If users create site collections on their own, they might or might not remember to create these objects on their new site collection.</span></span> <span data-ttu-id="52ccf-114">In diesem Szenario Benutzer erstellen von Websitesammlungen mithilfe des Add-Ins, aber Benutzer werden nicht einzeln Berechtigungen zum Erstellen von Websitesammlungen zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-114">In this scenario, users create site collections by using the add-in, but users aren't individually assigned permissions to create site collections.</span></span>

* <span data-ttu-id="52ccf-115">Ihr Add-in fungiert nicht von jedem Benutzer; beispielsweise ein Steuerung oder Management Prozess.</span><span class="sxs-lookup"><span data-stu-id="52ccf-115">Your add-in is not acting on behalf of any user; for example, a governance or management process.</span></span>

## <a name="app-only-policy-authorization"></a><span data-ttu-id="52ccf-116">Nur-App Richtlinie-Autorisierung</span><span class="sxs-lookup"><span data-stu-id="52ccf-116">App-only policy authorization</span></span>

<span data-ttu-id="52ccf-117">Nur-App Richtlinie verwendet OAuth, um das Add-in zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="52ccf-117">App-only policy uses OAuth to authenticate your add-in.</span></span> <span data-ttu-id="52ccf-118">Wenn das Add-in die nur-app-Richtlinie verwendet wird, überprüft SharePoint die Berechtigungen des Add-in-Prinzipals nur an.</span><span class="sxs-lookup"><span data-stu-id="52ccf-118">When your add-in uses the app-only policy, SharePoint checks the permissions of the add-in principal only.</span></span> <span data-ttu-id="52ccf-119">Dies sind die Berechtigungen, die das Add-in erteilt wurden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-119">These are the permissions that were granted to the add-in.</span></span> <span data-ttu-id="52ccf-120">Autorisierung erfolgreich, wenn das Add-in über ausreichende Berechtigungen zum Ausführen der Aufgabe, unabhängig von den Berechtigungen, die dem aktuellen Benutzer zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="52ccf-120">Authorization succeeds if the add-in has sufficient permissions to perform the task, regardless of the permissions associated with the current user.</span></span> <span data-ttu-id="52ccf-121">Wenn Autorisierung erfolgreich ist, wird ein Zugriffstoken an Ihr Add-In zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="52ccf-121">When authorization succeeds, an access token is returned to your add-in.</span></span> <span data-ttu-id="52ccf-122">Das Add-In wird dieses Zugriffstoken verwenden, um keine Aktionen erforderlich sind, vom Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-122">Your add-in will use this access token to perform any operations required by your code.</span></span>

<span data-ttu-id="52ccf-123">Weitere Informationen finden Sie unter [App-autorisierungsrichtlinientypen in SharePoint 2013](https://msdn.microsoft.com/library/office/fp179892.aspx).</span><span class="sxs-lookup"><span data-stu-id="52ccf-123">For more information, see [App authorization policy types in SharePoint 2013](https://msdn.microsoft.com/library/office/fp179892.aspx).</span></span>

<span data-ttu-id="52ccf-124">**Hinweis:** Die nur-app-Richtlinie ist nur für SharePoint-Hosting-add-ins, dass die Host-Web Access werden, die Benutzer + app-Richtlinie verwendet muss vom Anbieter gehosteten add-Ins verfügbar.</span><span class="sxs-lookup"><span data-stu-id="52ccf-124">**Note:** The app-only policy is available only for provider-hosted add-ins. SharePoint-hosted add-ins that access the host web must use the user+app policy.</span></span>

<span data-ttu-id="52ccf-125">Vorteile der Verwendung der nur-app-Richtlinie in der Include-add-in:</span><span class="sxs-lookup"><span data-stu-id="52ccf-125">Benefits of using the app-only policy in your add-in include:</span></span>

* <span data-ttu-id="52ccf-126">Sie müssen nicht keine separate Benutzerlizenz zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-126">You do not need to grant a separate user license.</span></span> <span data-ttu-id="52ccf-127">Dienstkonten erfordern keine separate Benutzerlizenz.</span><span class="sxs-lookup"><span data-stu-id="52ccf-127">Service accounts require a separate user license.</span></span>

* <span data-ttu-id="52ccf-128">Sie erhalten eine genauere Kontrolle über Berechtigungen als mit Dienstkonten zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="52ccf-128">You get more granular control over permissions than is available with service accounts.</span></span> <span data-ttu-id="52ccf-129">Sie können beispielsweise Vollzugriff-Berechtigungen auf dem Webserver anwenden, die nicht möglich, wenn Sie Dienstkonten verwenden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-129">For example, you can apply FullControl permissions on your web, which isn't possible when you use service accounts.</span></span>

<span data-ttu-id="52ccf-130">Sie können nicht nur-app-Richtlinie mit die folgenden APIs verwenden:</span><span class="sxs-lookup"><span data-stu-id="52ccf-130">You can't use the app-only policy with the following APIs:</span></span>

* <span data-ttu-id="52ccf-131">Benutzerprofil</span><span class="sxs-lookup"><span data-stu-id="52ccf-131">User Profile</span></span>

* <span data-ttu-id="52ccf-132">Suche</span><span class="sxs-lookup"><span data-stu-id="52ccf-132">Search</span></span>

* <span data-ttu-id="52ccf-133">Taxonomie (gilt nur für Szenarien, die in den verwalteten Metadatendienst schreiben)</span><span class="sxs-lookup"><span data-stu-id="52ccf-133">Taxonomy (this only applies to scenarios that write to the managed metadata service)</span></span>

<span data-ttu-id="52ccf-134">Um die nur-app-Richtlinie zu verwenden, müssen Sie zunächst die Berechtigungen für das Add-in erteilen, mithilfe von "appinv.aspx".</span><span class="sxs-lookup"><span data-stu-id="52ccf-134">To use the app-only policy, you first must grant permissions to the add-in by using appinv.aspx.</span></span> <span data-ttu-id="52ccf-135">Der folgende Code aus der Datei AppManifest.XML veranschaulicht, wie der nur-app-Richtlinie und die Berechtigungen für das add-in fest.</span><span class="sxs-lookup"><span data-stu-id="52ccf-135">The following code from AppManifest.xml file shows how to set the app-only policy and the permissions for your add-in.</span></span>

```xml
 <AppPermissionRequests AllowAppOnlyPolicy="true">
   <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="FullControl" />
 </AppPermissionRequests>
```

<span data-ttu-id="52ccf-136">Mit der nur-app-Richtlinie erfordert, dass Ihr Add-in niedriger oder hoher Vertrauenswürdigkeit Autorisierung verwenden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-136">Using the app-only policy requires that your add-in use either low-trust or high-trust authorization.</span></span> <span data-ttu-id="52ccf-137">Die Richtlinie ist nicht mit der SharePoint Cross-Domain-JavaScript-Bibliothek, die ist eine dritte Möglichkeit zum Abrufen von autorisierten Zugriffs auf SharePoint-Ressourcen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="52ccf-137">The policy is not available with the SharePoint cross-domain JavaScript library, which is a third way of getting authorized access to SharePoint resources.</span></span>

### <a name="low-trust-authorization"></a><span data-ttu-id="52ccf-138">Autorisierung mit niedriger Vertrauenswürdigkeit</span><span class="sxs-lookup"><span data-stu-id="52ccf-138">Low-trust authorization</span></span>

<span data-ttu-id="52ccf-139">Ihr Add-In kann beim Microsoft Azure Access Control Service (ACS) zum Einrichten der Vertrauensstellung zwischen Ihrer vom Anbieter gehosteten-add-in und Ihre Office 365-Website oder Ihre lokale SharePoint-Farm mit niedriger Vertrauenswürdigkeit Autorisierung verwenden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-139">Your add-in can use low-trust authorization when using the Microsoft Azure Access Control Service (ACS) to establish trust between your provider-hosted add-in and either your Office 365 site or your on-premises SharePoint farm.</span></span> <span data-ttu-id="52ccf-140">Sie können unter [drei Autorisierung Systeme für SharePoint-Add-ins 2013](https://msdn.microsoft.com/en-us/library/office/dn790706.aspx)informieren.</span><span class="sxs-lookup"><span data-stu-id="52ccf-140">You can learn more at [Three authorization systems for SharePoint Add-ins 2013](https://msdn.microsoft.com/en-us/library/office/dn790706.aspx).</span></span> <span data-ttu-id="52ccf-141">Wenn Sie einen Verweis auf das [ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) -Objekt erhalten möchten, sollte Ihr Add-in:</span><span class="sxs-lookup"><span data-stu-id="52ccf-141">To get a reference to the [ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) object, your add-in should:</span></span>

1. <span data-ttu-id="52ccf-142">Rufen Sie den Zugriff mithilfe der TokenHelper.GetAppOnlyAccessToken token ab.</span><span class="sxs-lookup"><span data-stu-id="52ccf-142">Get the access token by using TokenHelper.GetAppOnlyAccessToken.</span></span>

2. <span data-ttu-id="52ccf-143">Verwenden Sie TokenHelper.GetClientContextWithAccessToken, um das ClientContext-Objekt abzurufen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-143">Use TokenHelper.GetClientContextWithAccessToken to get the ClientContext object.</span></span>

<span data-ttu-id="52ccf-144">**Hinweis:** Die Datei TokenHelper wird Quellcode, die von der Microsoft Office Developer Tools für Visual Studio generiert wird.</span><span class="sxs-lookup"><span data-stu-id="52ccf-144">**Note:** The TokenHelper file is source code that is generated by the Microsoft Office Developer Tools for Visual Studio.</span></span> <span data-ttu-id="52ccf-145">Es ist keine Referenzdokumentation dafür, aber es sind umfassende Kommentare in die TokenHelper-Klasse.</span><span class="sxs-lookup"><span data-stu-id="52ccf-145">There is no reference documentation for it, but there are extensive comments in the TokenHelper class.</span></span> <span data-ttu-id="52ccf-146">Um die Codekommentare angezeigt wird, erstellen Sie eine vom Anbieter gehosteten-add-in in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52ccf-146">To see the code comments, create a provider-hosted add-in in Visual Studio.</span></span>

<span data-ttu-id="52ccf-147">**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="52ccf-147">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```cs
Uri siteUrl = new Uri(ConfigurationManager.AppSettings["MySiteUrl"]);
try
{
    // Connect to a site using an app-only token.
    string realm = TokenHelper.GetRealmFromTargetUrl(siteUrl);
    var token = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUrl.Authority, realm).AccessToken;

    using (var ctx = TokenHelper.GetClientContextWithAccessToken(siteUrl.ToString(), token))
    {
        // Perform operations on the ClientContext object, which uses the app-only token. 
    }
}
catch (Exception ex)
{
    Console.WriteLine("Error in execution: " + ex.Message);
}
```

### <a name="high-trust-authorization"></a><span data-ttu-id="52ccf-148">Besonders</span><span class="sxs-lookup"><span data-stu-id="52ccf-148">High-trust authorization</span></span>

<span data-ttu-id="52ccf-149">Wenn Ihr Add-in des besonders vertrauenswürdigen autorisierungssystems (auch bekannt als S2S Protocol) verwendet wird, ruft es eine andere Methode **TokenHelper** : **TokenHelper.GetS2SAccessTokenWithWindowsIdentity**.</span><span class="sxs-lookup"><span data-stu-id="52ccf-149">If your add-in uses the high-trust authorization system (also known as S2S protocol), it calls a different **TokenHelper** method: **TokenHelper.GetS2SAccessTokenWithWindowsIdentity**.</span></span>

<span data-ttu-id="52ccf-150">**Wichtig:** Die **TokenHelper.GetS2SAccessTokenWithWindowsIdentity** für beide nur-app-verwendet wird, und Benutzer + app aufruft.</span><span class="sxs-lookup"><span data-stu-id="52ccf-150">**Important:** The **TokenHelper.GetS2SAccessTokenWithWindowsIdentity** is used for both app-only and user+app calls.</span></span> <span data-ttu-id="52ccf-151">Der zweite Parameter der Methode, die die Identität des Benutzers enthält, bestimmt, welche Richtlinie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="52ccf-151">The second parameter of the method, which holds the user identity, determines which policy is used.</span></span> <span data-ttu-id="52ccf-152">Übergeben Sie **null** , um die nur-app-Richtlinie verwenden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-152">Pass **null** to use the app-only policy.</span></span>

## <a name="service-accounts"></a><span data-ttu-id="52ccf-153">Dienstkonten</span><span class="sxs-lookup"><span data-stu-id="52ccf-153">Service accounts</span></span>

<span data-ttu-id="52ccf-154">Verwenden Sie Dienstkonten, um Berechtigungen für das add-in zu erhöhen, nur, wenn die Richtlinie nur für Apps nicht über ausreichende Berechtigungen zum Ausführen der Aufgabe bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="52ccf-154">Use service accounts to elevate privileges for your add-in only when the app-only policy does not provide sufficient permissions to complete your task.</span></span> <span data-ttu-id="52ccf-155">Darüber hinaus ist ein Benutzerkonto in bestimmten Szenarien erforderlich.</span><span class="sxs-lookup"><span data-stu-id="52ccf-155">Also, in certain scenarios a user account is required.</span></span> <span data-ttu-id="52ccf-156">Beispielsweise müssen Sie Dienstkonten verwenden, wenn Ihr Code mit einem der folgenden SharePoint-dienstanwendungen funktioniert:</span><span class="sxs-lookup"><span data-stu-id="52ccf-156">For example, you need to use service accounts when your code works with any of the following SharePoint service applications:</span></span>

* <span data-ttu-id="52ccf-157">Benutzerprofildienst mit dem clientseitigen Objektmodell (CSOM)</span><span class="sxs-lookup"><span data-stu-id="52ccf-157">User Profile service using the client-side object model (CSOM)</span></span>

* <span data-ttu-id="52ccf-158">Verwalteter Metadatendienst</span><span class="sxs-lookup"><span data-stu-id="52ccf-158">Managed metadata service</span></span>

* <span data-ttu-id="52ccf-159">Suche</span><span class="sxs-lookup"><span data-stu-id="52ccf-159">Search</span></span>

<span data-ttu-id="52ccf-160">Bei der Planung von Dienstkonten in Ihr Add-in verwenden, beachten Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="52ccf-160">When planning to use service accounts in your add-in, consider the following:</span></span>

* <span data-ttu-id="52ccf-161">Dienstkonten erfordern keine separate Benutzerlizenz.</span><span class="sxs-lookup"><span data-stu-id="52ccf-161">Service accounts require a separate user license.</span></span>

* <span data-ttu-id="52ccf-162">Erstellen Sie entweder ein Dienstkonto pro-add-in, oder verwenden Sie ein Dienstkonto für alle Add-Ins in Ihrer SharePoint-Umgebung.</span><span class="sxs-lookup"><span data-stu-id="52ccf-162">Create either one service account per add-in, or use one service account for all add-ins in your SharePoint environment.</span></span>

* <span data-ttu-id="52ccf-163">Sie müssen den Benutzernamen und das Kennwort während der Autorisierung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="52ccf-163">You must supply the user name and password during authorization.</span></span> <span data-ttu-id="52ccf-164">Stellen Sie sicher, Anmeldeinformationen für das Dienstkonto gespeichert oder abgerufen sicher.</span><span class="sxs-lookup"><span data-stu-id="52ccf-164">Ensure service account credentials are stored or retrieved securely.</span></span>

* <span data-ttu-id="52ccf-165">Bevor das Add-in eine Aktion auf einer Website ausführen kann, müssen Dienstkonten zunächst über die Berechtigung zum Zugriff auf die Website erteilt werden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-165">Before your add-in can perform an action on a site, service accounts first must be granted permission to access the site.</span></span>

<span data-ttu-id="52ccf-166">**Hinweis:** Add-ins aus dem Office Store erworben haben, kann nicht Dienstkonten verwenden.</span><span class="sxs-lookup"><span data-stu-id="52ccf-166">**Note:** Add-ins purchased from the Office Store cannot use service accounts.</span></span>

<span data-ttu-id="52ccf-167">Der folgende Code zeigt, wie Sie mithilfe von [SharePointOnlineCredentials](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.sharepointonlinecredentials.aspx) mit einem Dienstkonto zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="52ccf-167">The following code shows how to authenticate by using [SharePointOnlineCredentials](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.sharepointonlinecredentials.aspx) with a service account.</span></span>

```cs
using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
{

    // Use default authentication mode.
    context.AuthenticationMode = ClientAuthenticationMode.Default;  

    // Specify the credentials for the service account.
    context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
}
```

## <a name="additional-resources"></a><span data-ttu-id="52ccf-168">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="52ccf-168">Additional resources</span></span>

<span data-ttu-id="52ccf-169">[Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="52ccf-169">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>

<span data-ttu-id="52ccf-170">[Add-in - autorisierungsrichtlinientypen in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179892.aspx).</span><span class="sxs-lookup"><span data-stu-id="52ccf-170">[Add-in authorization policy types in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179892.aspx).</span></span>

<span data-ttu-id="52ccf-171">[Office 365 SharePoint-Website zum Autorisieren von vom Anbieter gehosteten-add-ins auf einer lokalen SharePoint-Website verwenden](https://msdn.microsoft.com/en-us/library/office/dn155905.aspx).</span><span class="sxs-lookup"><span data-stu-id="52ccf-171">[Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site](https://msdn.microsoft.com/en-us/library/office/dn155905.aspx).</span></span>
