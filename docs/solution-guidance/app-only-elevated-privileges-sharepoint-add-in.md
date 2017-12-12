---
title: "Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: 9bcdbe3f5bb31e0c01fac300bb237bf0134c84a1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
<a name="app-only-and-elevated-privileges-in-the-sharepoint-add-in-model"></a><span data-ttu-id="dba4a-102">Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="dba4a-102">App-only and elevated privileges in the SharePoint add-in model</span></span>
===============================================================

<a name="summary"></a><span data-ttu-id="dba4a-103">Summary</span><span class="sxs-lookup"><span data-stu-id="dba4a-103">Summary</span></span>
-------

<span data-ttu-id="dba4a-104">Ansatz verwenden Sie zum Erhöhen von Berechtigungen in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="dba4a-104">The approach you take to elevate privileges in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="dba4a-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario der RunWithElevatedPrivileges-API über Farmlösungen bereitgestellt und mit SharePoint Server-Side-Objektmodellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dba4a-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the RunWithElevatedPrivileges API is used with the SharePoint server-side object model code and deployed via Farm Solutions.</span></span>

<span data-ttu-id="dba4a-106">In einer SharePoint-Add-in Modell Szenario, die Berechtigung AllowAppOnlyPolicy oder ein Dienstkonto wird, dass der aktuellen Benutzer zum Ausführen von Vorgängen, sie sind nicht autorisiert ausführen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-106">In an SharePoint Add-in model scenario, the AllowAppOnlyPolicy permission or a service account is used to allow the current user to execute operations they are not authorize to perform.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="dba4a-107">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="dba4a-107">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="dba4a-108">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für erhöhen von Berechtigungen im Code bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-108">As a rule of a thumb, we would like to provide the following high-level guidelines for elevating privileges in code.</span></span>

- <span data-ttu-id="dba4a-109">AllowAppOnlyPolicy funktioniert nicht mit</span><span class="sxs-lookup"><span data-stu-id="dba4a-109">AllowAppOnlyPolicy does not work with</span></span> 
    + <span data-ttu-id="dba4a-110">Suche – Wenn Ziel SharePoint lokal ist.</span><span class="sxs-lookup"><span data-stu-id="dba4a-110">Search - if target is SharePoint On-Premises.</span></span> <span data-ttu-id="dba4a-111">SharePoint Online-Unterstützung wurden ([Blogbeitrag](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)) hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="dba4a-111">SharePoint Online support for it has been added ([blog post](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))</span></span>
    + <span data-ttu-id="dba4a-112">Profil CSOM Benutzervorgänge, mit der Ausnahme, dass der Benutzerprofil Bulk Update-API mit nur-app-Berechtigungen verwendet werden können</span><span class="sxs-lookup"><span data-stu-id="dba4a-112">User Profile CSOM operations, except that the User Profile Bulk Update API can be used with app-only permissions</span></span>
    + <span data-ttu-id="dba4a-113">Aktualisieren der Taxonomie Diensteinträge (Schreiben) - Works lesen</span><span class="sxs-lookup"><span data-stu-id="dba4a-113">Updating taxonomy service entries (write) - read works</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="dba4a-114">In diesen Szenarien müssen Sie ein bestimmtes Dienstkonto verwenden.</span><span class="sxs-lookup"><span data-stu-id="dba4a-114">In these scenarios you need to use a specific service account.</span></span>

- <span data-ttu-id="dba4a-115">AllowAppOnlyPolicy ähnelt RunWithElevatedPrivileges, aber nicht genau.</span><span class="sxs-lookup"><span data-stu-id="dba4a-115">AllowAppOnlyPolicy is similar to RunWithElevatedPrivileges, but not exactly the same.</span></span>
    + <span data-ttu-id="dba4a-116">AllowAppOnlyPolicy führt Code basierend auf die Berechtigungen für das SharePoint Add-in, nicht im Auftrag einer anderen Benutzers, der die entsprechenden Berechtigungen zum Ausführen eines Vorgangs hat.</span><span class="sxs-lookup"><span data-stu-id="dba4a-116">AllowAppOnlyPolicy executes code based on the permissions granted to the SharePoint Add-in, not on behalf of another user who has the appropriate permissions to perform an operation.</span></span>

<span data-ttu-id="dba4a-117">Hier ist ein Beispiel für eine nur-App-Richtlinie Token zurückgeben und dessen Verwendung zum Erstellen eines Kontextobjekts.</span><span class="sxs-lookup"><span data-stu-id="dba4a-117">Here is an example of returning an App Only Policy token and using it to create a context object.</span></span>

    Uri siteUrl = new Uri(ConfigurationManager.AppSettings["MySiteUrl"]);
    try
    {
        //Connect to the give site using App Only token
        string realm = TokenHelper.GetRealmFromTargetUrl(siteUrl);
        var token = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUrl.Authority, realm).AccessToken;

        using (var ctx = TokenHelper.GetClientContextWithAccessToken(siteUrl.ToString(), token))
        {
            // Perform operations using the app only token access. 
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error in execution: " + ex.Message);
    }

- <span data-ttu-id="dba4a-118">Wenn Sie mit der AllowAppOnlyPolicy im Hinterkopf behalten funktioniert dies nur in vom Anbieter gehosteten SharePoint-Add-ins.</span><span class="sxs-lookup"><span data-stu-id="dba4a-118">When using the AllowAppOnlyPolicy, keep in mind it only works in Provider-hosted SharePoint Add-ins.</span></span>
- <span data-ttu-id="dba4a-119">AllowAppOnlyPolicy Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.</span><span class="sxs-lookup"><span data-stu-id="dba4a-119">AllowAppOnlyPolicy does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>
- <span data-ttu-id="dba4a-120">Dienstkonten werden in SharePoint definiert.</span><span class="sxs-lookup"><span data-stu-id="dba4a-120">Service accounts are defined in SharePoint.</span></span>
    + <span data-ttu-id="dba4a-121">In einer Office 365-Instanz, je nachdem, welche Funktionalität Ihre Code-Bestimmungen unterliegen, die Dienstkonten eine Office 365-Lizenz zugewiesen werden möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="dba4a-121">In an Office 365 tenancy, depending what functionality your code requirements have, the service accounts may need an Office 365 license assigned to them.</span></span>
    + <span data-ttu-id="dba4a-122">Erstellen Sie Dienstkonten auf einer pro SharePoint-Add-in-Basis, oder verwenden Sie ein einzelnes Konto für alle SharePoint-Add-ins.</span><span class="sxs-lookup"><span data-stu-id="dba4a-122">You can create service accounts on a per SharePoint Add-in basis, or use a single account for all SharePoint Add-ins.</span></span>
    + <span data-ttu-id="dba4a-123">Erstellen Sie klare und beschreibende Namen für die Dienstkonten, damit Sie auf einfache Weise die Vorgänge überwachen können, die sie durchführen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-123">Create clear and descriptive names for the service accounts so you can easily track the operations they perform.</span></span>
    
    <span data-ttu-id="dba4a-124">Beispiel: Wenn Ihre SharePoint-Add-in Listenelemente geändert wird, zeigt die Spalte geändert von für die Listenelemente den Namen des Dienstkontos mit dem SharePoint-Add-in verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="dba4a-124">For example: If your SharePoint Add-in modifies list items, the Modified By column for the list items will display the name of the service account associated with the SharePoint Add-in.</span></span>

- <span data-ttu-id="dba4a-125">Bei der Authentifizierung mit Dienstkonten müssen Sie einen Benutzernamen und ein Kennwort für das Dienstkonto abrufen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-125">When authenticating with service accounts, you must retrieve a user name and password for the service account.</span></span>
    + <span data-ttu-id="dba4a-126">Der folgende Codeausschnitt veranschaulicht die Verwendung von einen Benutzernamen und ein Kennwort um zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="dba4a-126">The code snippet below illustrates using a user name and password to authenticate.</span></span>
    + <span data-ttu-id="dba4a-127">Achten Sie zum Speichern und abrufen, den Benutzernamen und das Kennwort auf sichere Weise.</span><span class="sxs-lookup"><span data-stu-id="dba4a-127">Take care to store and retrieve the user name and password in a secure fashion.</span></span>

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {
    
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<a name="options-to-elevate-permissions"></a><span data-ttu-id="dba4a-128">Optionen zum Erhöhen von Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="dba4a-128">Options to elevate permissions</span></span>
------------------------------

<span data-ttu-id="dba4a-129">Sie haben verschiedene Optionen zum Erhöhen von Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-129">You have a couple of options to elevate permissions.</span></span>

- <span data-ttu-id="dba4a-130">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="dba4a-130">OAuth (AllowAppOnlyPolicy)</span></span>
    + <span data-ttu-id="dba4a-131">S2S (sub-Option)</span><span class="sxs-lookup"><span data-stu-id="dba4a-131">S2S (sub option)</span></span>
    + <span data-ttu-id="dba4a-132">ACS (Sub Option)</span><span class="sxs-lookup"><span data-stu-id="dba4a-132">ACS (sub option)</span></span>
- <span data-ttu-id="dba4a-133">-Dienstkonto</span><span class="sxs-lookup"><span data-stu-id="dba4a-133">Service Account</span></span>
    + <span data-ttu-id="dba4a-134">Remote gehosteten Code (Beispiel: Azure WebJob)</span><span class="sxs-lookup"><span data-stu-id="dba4a-134">Remotely hosted code (Example: Azure WebJob)</span></span>

<a name="oauth-allowapponlypolicy"></a><span data-ttu-id="dba4a-135">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="dba4a-135">OAuth (AllowAppOnlyPolicy)</span></span>
--------------------------
<span data-ttu-id="dba4a-136">Die AllowAppOnlyPolicy ist legen Sie diese Option auf true in den AppPermissionRequests-Element und Berechtigungen in der SharePoint-Add-in-Manifest festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="dba4a-136">In this option the AllowAppOnlyPolicy is set to true in the AppPermissionRequests element and permissions are set in the SharePoint Add-in manifest.</span></span> <span data-ttu-id="dba4a-137">OAuth dient zum Zurückgeben Zugriffstoken zum Zulassen des SharePoint-Add-Ins Ausführen von Vorgängen, die diese Berechtigungen zum Ausführen verfügt.</span><span class="sxs-lookup"><span data-stu-id="dba4a-137">OAuth is used to return access tokens to allow the SharePoint Add-in to execute operations it has permissions to perform.</span></span>

<span data-ttu-id="dba4a-138">**S2S Sub-option**</span><span class="sxs-lookup"><span data-stu-id="dba4a-138">**S2S sub option**</span></span>

<span data-ttu-id="dba4a-139">Die S2S sub-Option funktioniert nur, wenn in der lokalen SharePoint-Umgebungen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-139">The S2S sub option only works in on-premises SharePoint environments.</span></span>

<span data-ttu-id="dba4a-140">Beim Authentifizieren über OAuth in einem Szenario S2S die **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** -Methode verwendet, um das Zugriffstoken für das SharePoint-Add-in zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="dba4a-140">When authenticating via OAuth in an S2S scenario the **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** method is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="dba4a-141">Das Zugriffstoken ermöglicht die SharePoint-Add-in für alle Vorgänge ausführen des SharePoint-Add-Ins erteilt im SharePoint-Add-in-Manifest.</span><span class="sxs-lookup"><span data-stu-id="dba4a-141">The access token allows the SharePoint Add-in to perform any operations the SharePoint Add-in is granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="dba4a-142">Diese Option Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.</span><span class="sxs-lookup"><span data-stu-id="dba4a-142">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="dba4a-143">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="dba4a-143">**When is it a good fit?**</span></span>

<span data-ttu-id="dba4a-144">Wenn Sie Berechtigungen in einem Szenario mit SharePoint S2S erhöhen müssen ist dies eine gute Wahl, da diese Option mit S2S arbeitet und sehr einfach zu implementieren ist.</span><span class="sxs-lookup"><span data-stu-id="dba4a-144">When you need to elevate privileges in a SharePoint S2S scenario this is a good option because this option works with S2S and is very easy to implement.</span></span>

<span data-ttu-id="dba4a-145">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="dba4a-145">**Getting Started**</span></span>

<span data-ttu-id="dba4a-146">Im folgende Artikel veranschaulicht, wie AllowAppOnlyPolicy mit S2S.</span><span class="sxs-lookup"><span data-stu-id="dba4a-146">The following article demonstrates how to use AllowAppOnlyPolicy with S2S.</span></span>

- [<span data-ttu-id="dba4a-147">SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)</span><span class="sxs-lookup"><span data-stu-id="dba4a-147">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<span data-ttu-id="dba4a-148">**ACS Sub-option**</span><span class="sxs-lookup"><span data-stu-id="dba4a-148">**ACS sub option**</span></span>

<span data-ttu-id="dba4a-149">Die Option ACS Sub Arbeit in lokalen und Office 365 SharePoint-Umgebungen.</span><span class="sxs-lookup"><span data-stu-id="dba4a-149">The ACS sub option work in on-premises and Office 365 SharePoint environments.</span></span>

<span data-ttu-id="dba4a-150">Beim Authentifizieren über OAuth in einem Szenario mit ACS die **TokenHelper::GetAppOnlyAccessTokenmethod** verwendet, um das Zugriffstoken für das SharePoint-Add-in zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="dba4a-150">When authenticating via OAuth in an ACS scenario the **TokenHelper::GetAppOnlyAccessTokenmethod** is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="dba4a-151">Anschließend wird die **TokenHelper::GetClientContextWithAccessToken** -Methode aufgerufen, die Rückgabe Clientkontexts erforderlich sind, um alle Vorgänge ausführen, die des SharePoint-Add-Ins berechtigt ist, anhand von Berechtigungen in der SharePoint-Add-in-Manifest.</span><span class="sxs-lookup"><span data-stu-id="dba4a-151">Then, the **TokenHelper::GetClientContextWithAccessToken** method is invoked to return the client context necessary to perform any operations the SharePoint Add-in has permission to do based on the permissions granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="dba4a-152">Diese Option Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.</span><span class="sxs-lookup"><span data-stu-id="dba4a-152">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="dba4a-153">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="dba4a-153">**When is it a good fit?**</span></span>

<span data-ttu-id="dba4a-154">Wenn Sie Berechtigungen in einem Szenario mit SharePoint ACS erhöhen müssen ist dies eine gute Wahl, da diese Option mit ACS arbeitet und sehr einfach zu implementieren ist.</span><span class="sxs-lookup"><span data-stu-id="dba4a-154">When you need to elevate privileges in a SharePoint ACS scenario this is a good option because this option works with ACS and is very easy to implement.</span></span>  <span data-ttu-id="dba4a-155">Diese Option ist ideal, wenn Sie eine lokale SharePoint-Umgebung verwenden, die eine Vertrauensstellung mit ACS hat.</span><span class="sxs-lookup"><span data-stu-id="dba4a-155">This option is a good fit when you have an on-premises SharePoint environment that has an established trust with ACS.</span></span>  <span data-ttu-id="dba4a-156">Dies ist nur OAuth die Option, wenn Sie eine Office 365 SharePoint-Umgebung haben.</span><span class="sxs-lookup"><span data-stu-id="dba4a-156">This is your only OAuth option when you have a Office 365 SharePoint environment.</span></span>

<span data-ttu-id="dba4a-157">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="dba4a-157">**Getting Started**</span></span>

<span data-ttu-id="dba4a-158">Im folgende Artikel veranschaulicht, wie AllowAppOnlyPolicy mit ACS.</span><span class="sxs-lookup"><span data-stu-id="dba4a-158">The following article demonstrates how to use AllowAppOnlyPolicy with ACS.</span></span>

- [<span data-ttu-id="dba4a-159">SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)</span><span class="sxs-lookup"><span data-stu-id="dba4a-159">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<a name="service-account"></a><span data-ttu-id="dba4a-160">-Dienstkonto</span><span class="sxs-lookup"><span data-stu-id="dba4a-160">Service Account</span></span>
---------------
<span data-ttu-id="dba4a-161">In diesem Muster wird die SharePointOnlineCredentials-Klasse verwendet, herstellen im Kontext eines Benutzers, der Code ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dba4a-161">In this pattern, the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

<span data-ttu-id="dba4a-162">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="dba4a-162">**When is it a good fit?**</span></span>

<span data-ttu-id="dba4a-163">Wenn Sie zum Ausführen von Code im Auftrag eines bestimmten Benutzers (Service Account müssen) ist dies eine gute Wahl, da Aktionen des Benutzers (Service Account) und die SharePoint Add-in Berechtigungen ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="dba4a-163">When you need to execute code on behalf of a specific user (service account) this is a good option because it performs actions on the user's (service account) and the SharePoint Add-in's permissions.</span></span>

<span data-ttu-id="dba4a-164">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="dba4a-164">**Getting Started**</span></span>

<span data-ttu-id="dba4a-165">Im folgende Artikel veranschaulicht, wie die SharePointOnlineCredentials-Klasse verwendet wird, herstellen im Kontext eines Benutzers, der Code ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dba4a-165">The following article demonstrates how the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

- [<span data-ttu-id="dba4a-166">Erste Schritte mit der Erstellung von Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365 (Aspekte im Abschnitt Authentifizierung) - Tobias Zimmergren-Blog-Artikel Websites</span><span class="sxs-lookup"><span data-stu-id="dba4a-166">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)

<a name="related-links"></a><span data-ttu-id="dba4a-167">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="dba4a-167">Related links</span></span>
=============
- [<span data-ttu-id="dba4a-168">SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)</span><span class="sxs-lookup"><span data-stu-id="dba4a-168">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)
- [<span data-ttu-id="dba4a-169">Erste Schritte mit der Erstellung von Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365 (Aspekte im Abschnitt Authentifizierung) - Tobias Zimmergren-Blog-Artikel Websites</span><span class="sxs-lookup"><span data-stu-id="dba4a-169">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)
- [<span data-ttu-id="dba4a-170">SharePointOnlineCredentials-Klasse (MSDN-API-Dokumentation)</span><span class="sxs-lookup"><span data-stu-id="dba4a-170">SharePointOnlineCredentials class (MSDN API Documentation)</span></span>](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.sharepointonlinecredentials.aspx)
- [<span data-ttu-id="dba4a-171">Verwenden von Add-in- / nur-app-Berechtigungen mit Suchabfragen in SharePoint Online - Vesa Juvonen Blog-Artikel</span><span class="sxs-lookup"><span data-stu-id="dba4a-171">Using add-in only / app-only permissions with search queries in SharePoint Online - Vesa Juvonen Blog Article</span></span>](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)
- <span data-ttu-id="dba4a-172">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="dba4a-172">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="dba4a-173">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="dba4a-173">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="dba4a-174">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="dba4a-174">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="dba4a-175">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="dba4a-175">Related PnP samples</span></span>
===================

- [<span data-ttu-id="dba4a-176">Core.SimpleTimerJob (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="dba4a-176">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- <span data-ttu-id="dba4a-177">Beispiele und Inhalte am https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="dba4a-177">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="dba4a-178">Gilt für</span><span class="sxs-lookup"><span data-stu-id="dba4a-178">Applies to</span></span>
==========
- <span data-ttu-id="dba4a-179">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="dba4a-179">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="dba4a-180">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="dba4a-180">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="dba4a-181">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="dba4a-181">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="dba4a-182">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="dba4a-182">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
