---
title: Richten Sie Ihre Multi-Geo Beispielanwendungen
ms.date: 11/03/2017
ms.openlocfilehash: 5974998440e13f99fb7b025d1dcd70d84c2edd06
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-your-multi-geo-sample-applications"></a><span data-ttu-id="6b6c9-102">Richten Sie Ihre Multi-Geo Beispielanwendungen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-102">Set up your Multi-Geo sample applications</span></span>

> <span data-ttu-id="6b6c9-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="6b6c9-104">Bei der Entwicklung für einen Mandanten Multi-Geo ist es wichtig zu verstehen, das Sicherheitsmodell und zum Glück verwendete Modell für einen Mandanten Multi-Geo unterscheidet sich nicht aus dem Modell für einen regulären Mandanten verwendet.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-104">When developing for a Multi-Geo tenant it's important to understand the security model and luckily the used model for a Multi-Geo tenant does not differ from the model used for a regular tenant.</span></span> <span data-ttu-id="6b6c9-105">In diesem Artikel wird das Konfigurieren der Beispielanwendungen veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-105">This article shows you how to configure the sample applications.</span></span>

## <a name="my-application-needs-to-be-able-to-readupdate-profiles-for-all-users"></a><span data-ttu-id="6b6c9-106">Meine Anwendung benötigt Lese-/Profile für alle Benutzer aktualisieren können</span><span class="sxs-lookup"><span data-stu-id="6b6c9-106">My application needs to be able to read/update profiles for all users</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="6b6c9-107">Ich verwende Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-107">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="6b6c9-108">Wie im Artikel [Multi-Geo Profil Benutzererlebnis](multigeo-userprofileexperience.md) erläutert ist das bevorzugte Modell zum Lesen/Aktualisieren von Benutzerprofileigenschaften mithilfe der API: Grafik.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-108">As explained in the [Multi-geo User Profile Experience](multigeo-userprofileexperience.md) article the preferred model to read/update user profile properties is by using the Graph API.</span></span> <span data-ttu-id="6b6c9-109">In diesem Kapitel wird erläutert, welche Berechtigungen Sie so gewähren Sie der Anwendung, Mandanten breit Benutzerprofil Lesevorgänge und Updates zu erzielen müssen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-109">This chapter explains which permissions you'll need to grant to your application to realize tenant wide user profile reads and updates.</span></span> <span data-ttu-id="6b6c9-110">Es gibt [eine lange Liste von Berechtigungen](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) , dass Sie zu einer Anwendung in Azure AD definierten gewähren können, aber für die Bearbeitung von Benutzerprofilen können Sie Berechtigungen zum einschränken:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-110">There [a long list of possible permissions](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) that you can grant to an application defined in Azure AD, but for manipulating profiles you can limit permissions to:</span></span>

|<span data-ttu-id="6b6c9-111">**Berechtigung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-111">**Permission**</span></span>|<span data-ttu-id="6b6c9-112">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-112">**Type**</span></span>|<span data-ttu-id="6b6c9-113">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-113">**Description**</span></span>| <span data-ttu-id="6b6c9-114">**Admin Zustimmung erforderlich**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-114">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="6b6c9-115">**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-115">**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="6b6c9-116">Anwendung die Berechtigung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-116">Application permission</span></span> | <span data-ttu-id="6b6c9-117">Ermöglicht der App, den vollständigen Satz von Profileigenschaften, Gruppenmitgliedschaften, Berichten und Vorgesetzten von anderen Benutzern in Ihrer Organisation ohne angemeldeten Benutzer zu lesen und zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-117">Allows the app to read and write the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.</span></span>  <span data-ttu-id="6b6c9-118">Außerdem können die app zum Erstellen und Löschen von Benutzern ohne Administratorrechte.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-118">Also allows the app to create and delete non-administrative users.</span></span> <span data-ttu-id="6b6c9-119">Zurücksetzen von Benutzerkennwörtern ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-119">Does not allow reset of user passwords.</span></span> | <span data-ttu-id="6b6c9-120">Ja</span><span class="sxs-lookup"><span data-stu-id="6b6c9-120">Yes</span></span>
|<span data-ttu-id="6b6c9-121">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-121">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="6b6c9-122">Anwendung die Berechtigung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-122">Application permission</span></span> | <span data-ttu-id="6b6c9-123">Ermöglicht die app den Lese-/Schreibzugriff Dokumente und Listenelemente in allen Websitesammlungen, ohne dass ein Benutzer angemeldet.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-123">Allows the app to read/write documents and list items in all site collections without a signed in user.</span></span> <span data-ttu-id="6b6c9-124">Diese Berechtigung ist nur erforderlich, wenn die Anwendung Speicherorts für persönliche Websites des Benutzers abrufen (z. B. https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$ wählen =-MeineWebsite)</span><span class="sxs-lookup"><span data-stu-id="6b6c9-124">This permission is only needed if the application will be retrieving the user's personal site location (e.g. https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$select=mySite)</span></span> | <span data-ttu-id="6b6c9-125">Ja</span><span class="sxs-lookup"><span data-stu-id="6b6c9-125">Yes</span></span>

<span data-ttu-id="6b6c9-126">Das Microsoft Graph basierend Multi-Geo-Beispiele für die Verbindung mit der Microsoft Graph für den Endpunkt v2 Microsoft Authentifizierung Library (MSAL) verwenden.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-126">The Microsoft Graph based Multi-Geo samples are using the Microsoft Authentication Library (MSAL) to connect with the Microsoft Graph on the v2 endpoint.</span></span> <span data-ttu-id="6b6c9-127">Im Vergleich zu ADAL, der eine Verbindung herstellt, unter Verwendung des Endpunktes v1, MSAL ermöglicht eine Verbindung zu den Microsoft Graph mit Microsoft Accounts, Azure AD und Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-127">Compared to ADAL which connects using the v1 endpoint, MSAL allows connection to the Microsoft Graph with Microsoft Accounts, Azure AD and Azure AD B2C.</span></span> <span data-ttu-id="6b6c9-128">Unten Anweisungen helfen Ihnen beim setup von der Anwendung für den Endpunkt v2, aber Sie können auch den "älteren" Ansatz basierend auf den v1-Endpunkten verwenden.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-128">Below instructions will help you setup your application for the v2 endpoint, but you can also use the "older" approach based on the v1 endpoints.</span></span>

#### <a name="register-your-application"></a><span data-ttu-id="6b6c9-129">Registrieren Sie Ihre Anwendung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-129">Register your application</span></span>
<span data-ttu-id="6b6c9-130">Berechtigungen für die Microsoft Graph verwenden Sie zuerst die Anwendung zu registrieren müssen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-130">To use application permissions against the Microsoft Graph you first have to register your application.</span></span> <span data-ttu-id="6b6c9-131">Dabei wird unter https://apps.dev.microsoft.com. Nach der Anmeldung in Klick fügen Sie eine neue Zusammengef-Anwendung, indem Sie auf app hinzufügen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-131">You do this at https://apps.dev.microsoft.com. Once logged in click add a new Converged application, by clicking Add an app</span></span>

![Registrieren Sie die Anwendung in Azure AD](media/multigeo/multigeopermissions_registerapp1.png)

<span data-ttu-id="6b6c9-133">Geben Sie der Anwendung einen Namen ein, und drücken Sie Anwendung erstellen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-133">Give your application a name and hit Create application.</span></span>

<span data-ttu-id="6b6c9-134">Konfigurieren Sie im Konfigurationsbildschirm Anwendung Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-134">In the application configuration screen configure the following:</span></span>
- <span data-ttu-id="6b6c9-135">Generieren Sie ein Kennwort, und notieren Sie es zusammen mit der Id der Anwendung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-135">Generate a password and make a note of it together with the application id</span></span>
- <span data-ttu-id="6b6c9-136">Klicken Sie auf 'Plattform hinzufügen', und wählen Sie "Systemeigene Anwendung" als Zielplattform, wie die Anwendung ein Zielseite nicht vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="6b6c9-136">Click 'Add Platform' and select "Native application" as the platform target as the application does not have a landing page</span></span>
- <span data-ttu-id="6b6c9-137">Fügen Sie die erforderliche Berechtigung für die Anwendung hinzu.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-137">Add the necessary Application Permission.</span></span> <span data-ttu-id="6b6c9-138">In diesem Beispiel-app haben wir die User.ReadWrite.All und Sites.ReadWrite.All Berechtigungen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-138">In this sample app we have added the User.ReadWrite.All and Sites.ReadWrite.All application permissions.</span></span>
- <span data-ttu-id="6b6c9-139">Stellen Sie sicher, 'Live SDK Unterstützung' deaktivieren</span><span class="sxs-lookup"><span data-stu-id="6b6c9-139">Make sure to uncheck 'Live SDK support'</span></span>
- <span data-ttu-id="6b6c9-140">Speichern Ihrer Änderungen einmal konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-140">Once configured save your changes.</span></span>

![Konfigurieren von Anwendung in Azure AD-Teil 1](media/multigeo/multigeopermissions_registerapp2.png)

![Konfigurieren von Anwendung in Azure AD-Teil 2](media/multigeo/multigeopermissions_registerapp3.png)


#### <a name="consent-to-the-application"></a><span data-ttu-id="6b6c9-143">Einverständnis, dass die Anwendung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-143">Consent to the application</span></span>
<span data-ttu-id="6b6c9-144">In diesem Beispiel die User.ReadWrite.All und erfordern Sites.ReadWrite.All Anwendungsberechtigungen Admin Zustimmung in einem Mandanten bevor verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-144">In this sample the User.ReadWrite.All and Sites.ReadWrite.All application permissions require admin consent in a tenant before it can be used.</span></span> <span data-ttu-id="6b6c9-145">Erstellen Sie eine Zustimmung URL wie folgt:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-145">Create a consent URL like the following:</span></span>

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<clientid>&state=<something>
```

<span data-ttu-id="6b6c9-146">Verwenden die Client-Id aus der app registriert und damit einverstanden, die app aus Meine Mandanten contoso.onmicrosoft.com, sieht die URL folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-146">Using the client id from the app registered and consenting to the app from my tenant contoso.onmicrosoft.com, the URL looks like this:</span></span>

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

<span data-ttu-id="6b6c9-147">Durchsuchen, um das erstellte URL und melden Sie sich als Administrator und Zustimmung an die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-147">Browsing to the created URL and log in as a tenant admin, and consent to the application.</span></span> <span data-ttu-id="6b6c9-148">Sie können den Zustimmung Bildschirm zeigen Sie den Namen der Anwendung als auch die von Ihnen konfigurierten berechtigungsbereiche sehen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-148">You can see the consent screen show the name of your application as well as the permission scopes you configured.</span></span>

![Mandanten Zustimmung für Azure AD-Anwendung](media/multigeo/multigeopermissions_registerapp4.png)

### <a name="im-using-the-csom-user-profile-api"></a><span data-ttu-id="6b6c9-150">Verwende ich die CSOM Benutzerprofil-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-150">I'm using the CSOM User Profile API</span></span>
<span data-ttu-id="6b6c9-151">Beim Verwenden der CSOM-API zum Bearbeiten von Benutzerprofileigenschaften, die Sie nur dann tun, werden für die erstellten benutzerdefinierten Eigenschaften seit Out-of-Box-Eigenschaften besser sind über die Microsoft Graph-API... behandelt finden Sie im Artikel [Multi-Geo Benutzererlebnis Profil](multigeo-userprofileexperience.md) nach weiteren Details.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-151">When using the CSOM API to manipulate profile properties you'll only do this for the custom created properties since out-of-the-box properties are better handled via the Microsoft Graph API...see the [Multi-geo User Profile Experience](multigeo-userprofileexperience.md) article for more details.</span></span> <span data-ttu-id="6b6c9-152">Aus Sicht einer Berechtigung gibt es zwei Modi:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-152">From a permission point of view there's two modes:</span></span>

#### <a name="using-user-credentials"></a><span data-ttu-id="6b6c9-153">Verwenden von Benutzeranmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-153">Using user credentials</span></span>
<span data-ttu-id="6b6c9-154">Dies erfordert das Einrichten einer `ClientContext` -Objekts verwenden die Mandanten-Admin-Url und Verwenden von SharePoint Online-Admin-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-154">This requires setting up a `ClientContext` object using the tenant admin url and using SharePoint Online admin credentials.</span></span> <span data-ttu-id="6b6c9-155">Da es ist nur eine einzige Azure AD-Instanz, die gedrückt halten, Benutzer bedeutet dies auch, dass ein SharePoint Online Admin Admin für alle Speicherorte Geo ist.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-155">Since there's only one Azure AD instance holding users this also implies that a SharePoint Online admin is admin for all the geo locations.</span></span>

```C#
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";

using (ClientContext cc = new ClientContext(tenantAdminSiteForMyGeoLocation))
{
    SecureString securePassword = GetSecurePassword("password");
    cc.Credentials = new SharePointOnlineCredentials("admin@contoso.onmicrosoft.com", securePassword);
    
    // user profile logic
}

static SecureString GetSecurePassword(string Password)
{
    SecureString sPassword = new SecureString();
    foreach (char c in Password.ToCharArray()) sPassword.AppendChar(c);
    return sPassword;
}
```

#### <a name="using-an-app-only-principal"></a><span data-ttu-id="6b6c9-156">Mithilfe eines nur-app-Prinzipals</span><span class="sxs-lookup"><span data-stu-id="6b6c9-156">Using an app-only principal</span></span>
<span data-ttu-id="6b6c9-157">Bei Verwendung der nur-app-müssen Sie das erstellte app principal **Vollzugriff** für den Bereich der [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) Berechtigung erteilen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-157">When using app-only you'll need to grant the created app principal **full control** for the [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) permission scope.</span></span> <span data-ttu-id="6b6c9-158">Unten Anweisungen zeigen Sie zum Registrieren eines app-Prinzipals und stimmen sie die Verwendung von "appregnew.aspx" und "appinv.aspx an".</span><span class="sxs-lookup"><span data-stu-id="6b6c9-158">Below instructions show you to use appregnew.aspx and appinv.aspx to register an app principal and consent it.</span></span>

##### <a name="create-the-principal"></a><span data-ttu-id="6b6c9-159">Erstellen des Prinzipals</span><span class="sxs-lookup"><span data-stu-id="6b6c9-159">Create the principal</span></span>
<span data-ttu-id="6b6c9-160">Navigieren Sie zu einer Website in Ihrem Mandanten (z. B. https://contoso.sharepoint.com), und rufen Sie dann auf der Seite "appregnew.aspx" (z. B. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b6c9-160">Navigate to a site in your tenant (e.g. https://contoso.sharepoint.com) and then call the appregnew.aspx page (e.g. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span></span> <span data-ttu-id="6b6c9-161">In dieser Seite klicken Sie auf die Schaltfläche generieren, um eine Client-Id und den geheimen Clientschlüssel generieren und füllen Sie die verbleibende Informationen wie in der Screenshot-unten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-161">In this page click on the Generate button to generate a client id and client secret and fill the remaining information like shown in the screen-shot below.</span></span>

![Registrieren von app-Prinzipal ACS](media/multigeo/multigeopermissions_registerprincipal1.png)

> <span data-ttu-id="6b6c9-163">**Wichtige** Speichern Sie die abgerufene Informationen (Client-Id und den geheimen Clientschlüssel), da Sie dies im nächsten Schritt benötigen!</span><span class="sxs-lookup"><span data-stu-id="6b6c9-163">**Important** Store the retrieved information (client id and client secret) since you'll need this in the next step!</span></span>

##### <a name="grant-permissions-to-the-created-principal"></a><span data-ttu-id="6b6c9-164">Erteilen von Berechtigungen für den erstellten Prinzipal</span><span class="sxs-lookup"><span data-stu-id="6b6c9-164">Grant permissions to the created principal</span></span>
<span data-ttu-id="6b6c9-165">Nächsten Schritt wird das Erteilen von Berechtigungen für die neu erstellte Prinzipal.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-165">Next step is granting permissions to the newly created principal.</span></span> <span data-ttu-id="6b6c9-166">Da wir Mandanten bezogenen Berechtigungen gewähren kann dieses Verfahren nur über die Seite "appinv.aspx" auf die Mandantenverwaltungs-Website ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-166">Since we're granting tenant scoped permissions this granting can only be done via the appinv.aspx page on the tenant administration site.</span></span> <span data-ttu-id="6b6c9-167">Sie können diese Website über https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx erreichen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-167">You can reach this site via https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx.</span></span> <span data-ttu-id="6b6c9-168">Nach dem Laden der Seite fügen Sie Ihrer Client-Id hinzu und den erstellten Prinzipal nachschlagen:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-168">Once the page is loaded add your client id and look up the created principal:</span></span>

![Erteilen von Berechtigungen für app-Prinzipal](media/multigeo/multigeopermissions_registerprincipal2.png)

<span data-ttu-id="6b6c9-170">Um Berechtigungen zu erteilen, müssen Sie die Berechtigung XML bereitstellen, auf denen die erforderlichen Berechtigungen beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-170">In order to grant permissions you'll need to provide the permission XML that describes the needed permissions.</span></span> <span data-ttu-id="6b6c9-171">Seit die Benutzeroberfläche auftreten Scanner muss auf allen Websites zugreifen + verwendet auch mit nur-app-Suche ist es unten aufgeführten Berechtigungen erforderlich:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-171">Since the UI experience scanner needs to be able to access all sites + also uses search with app-only it requires below permissions:</span></span>

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="FullControl" />
</AppPermissionRequests>
```

<span data-ttu-id="6b6c9-172">Wenn Sie auf Create wird eine Berechtigung Zustimmungsdialogfeld angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-172">When you click on Create you'll be presented with a permission consent dialog.</span></span> <span data-ttu-id="6b6c9-173">Drücken Sie vertrauen, die Berechtigungen erteilen:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-173">Press Trust It to grant the permissions:</span></span>

![Zustimmung der app-Prinzipal](media/multigeo/multigeopermissions_registerprincipal3.png)


##### <a name="use-the-principal-in-your-code"></a><span data-ttu-id="6b6c9-175">Verwenden Sie den Prinzipal in Ihrem code</span><span class="sxs-lookup"><span data-stu-id="6b6c9-175">Use the principal in your code</span></span>
<span data-ttu-id="6b6c9-176">Sobald der Prinzipal erstellt und zugestimmt ist können des Prinzipals-Id und geheimen Schlüssel Sie eine Access anfordern.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-176">Once the principal is created and consented you can use the principal's id and secret to request an access.</span></span> <span data-ttu-id="6b6c9-177">Die `TokenHelper.cs` Klasse wird die Id und geheimen Clientschlüssel aus der Anwendungskonfigurationsdatei Code.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-177">The `TokenHelper.cs` class will grab the id and secret from the application's configuration file.</span></span>

```C#
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";

//Get the realm for the URL
string realm = TokenHelper.GetRealmFromTargetUrl(siteUri);

//Get the access token for the URL.  
string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUri.Authority, realm).AccessToken;

//Create a client context object based on the retrieved access token
using (ClientContext cc = TokenHelper.GetClientContextWithAccessToken(tenantAdminSiteForMyGeoLocation, accessToken))
{
    // user profile logic
}
```

<span data-ttu-id="6b6c9-178">Ein Beispiel app.config sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-178">A sample app.config looks like this:</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <!-- Use AppRegNew.aspx and AppInv.aspx to register client id with proper secret -->
    <add key="ClientId" value="[Your Client ID]" />
    <add key="ClientSecret" value="[Your Client Secret]" />
  </appSettings>
</configuration>
```


> [!NOTE] 
> <span data-ttu-id="6b6c9-179">Sie können auf einfache Weise einfügen der `TokenHelper.cs` -Klasse in Ihrem Projekt, indem Sie die **AppForSharePointOnlineWebToolkit** Nuget-Paket für Ihre Lösung.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-179">You can easily insert the `TokenHelper.cs` class in your project by adding the **AppForSharePointOnlineWebToolkit** nuget package to your solution.</span></span>

## <a name="my-application-needs-to-be-able-to-be-able-to-discover-the-multi-geo-configuration"></a><span data-ttu-id="6b6c9-180">Meine Anwendung muss die Konfiguration mit mehreren geografisch ermitteln können können</span><span class="sxs-lookup"><span data-stu-id="6b6c9-180">My application needs to be able to be able to discover the Multi-Geo configuration</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="6b6c9-181">Ich verwende Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-181">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="6b6c9-182">Die einzige unterstützte API entdecken Sie die Geo Speicherorte in einem Multi-Geo-Mandanten mithilfe der API: Grafik ist.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-182">The only supported API discover the geo locations in a Multi-Geo tenant is by using the Graph API.</span></span> <span data-ttu-id="6b6c9-183">In diesem Kapitel wird erläutert, welche Berechtigungen Sie so gewähren Sie die Anwendung zum Ermitteln von Multi-Geo-Informationen müssen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-183">This chapter explains which permissions you'll need to grant to your application to discover Multi-Geo information.</span></span> <span data-ttu-id="6b6c9-184">Es gibt [eine lange Liste von Berechtigungen](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) , dass Sie zu einer Anwendung in Azure AD definierten gewähren können, aber für das Lesen von Multi-Geo Mandanten Konfigurationsinformationen können Sie Berechtigungen zum einschränken:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-184">There [a long list of possible permissions](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) that you can grant to an application defined in Azure AD, but for reading Multi-Geo tenant configuration information you can limit permissions to:</span></span>

|<span data-ttu-id="6b6c9-185">**Berechtigung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-185">**Permission**</span></span>|<span data-ttu-id="6b6c9-186">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-186">**Type**</span></span>|<span data-ttu-id="6b6c9-187">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-187">**Description**</span></span>| <span data-ttu-id="6b6c9-188">**Admin Zustimmung erforderlich**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-188">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="6b6c9-189">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-189">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="6b6c9-190">Anwendung die Berechtigung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-190">Application permission</span></span> | <span data-ttu-id="6b6c9-191">Ermöglicht die app den Lese-/Schreibzugriff Dokumente und Listenelemente in allen Websitesammlungen, ohne dass ein Benutzer angemeldet.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-191">Allows the app to read/write documents and list items in all site collections without a signed in user.</span></span> | <span data-ttu-id="6b6c9-192">Ja</span><span class="sxs-lookup"><span data-stu-id="6b6c9-192">Yes</span></span>

<span data-ttu-id="6b6c9-193">Verwenden Sie die Schritten zur Erstellung des Azure AD-Anwendung, wie im Kapitel "Meine Anwendung muss Read/Update Profile für alle Benutzer können" beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-193">Use the Azure AD application creation steps as described in the "My application needs to be able to read/update profiles for all users" chapter.</span></span>

## <a name="my-application-needs-to-be-able-to-createdelete-sites-collections-or-set-tenant-site-collection-properties"></a><span data-ttu-id="6b6c9-194">Meine Anwendung muss können Websitesammlungen erstellen/löschen oder Festlegen der Eigenschaften der Websitesammlung Mandanten</span><span class="sxs-lookup"><span data-stu-id="6b6c9-194">My application needs to be able to create/delete sites collections or set tenant site collection properties</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="6b6c9-195">Ich verwende Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-195">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="6b6c9-196">Die [Multi-Geo Websites](multigeo-sites.md) enthält weitere Details zum (auch bekannt als Gruppe Websites erstellen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-196">The [Multi-Geo Sites](multigeo-sites.md) provides more details on how to create group sites (a.k.a.</span></span> <span data-ttu-id="6b6c9-197">"modernen" Teamwebsites) mit der Microsoft Graph-API in diesem Abschnitt wir sind nur reagieren auf Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-197">"modern" team sites) using the Microsoft Graph API, in this section we're only addressing the permissions.</span></span> <span data-ttu-id="6b6c9-198">Unter Tabelle enthält die erforderlichen Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-198">Below table lists the needed permissions</span></span>

|<span data-ttu-id="6b6c9-199">**Berechtigung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-199">**Permission**</span></span>|<span data-ttu-id="6b6c9-200">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-200">**Type**</span></span>|<span data-ttu-id="6b6c9-201">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-201">**Description**</span></span>| <span data-ttu-id="6b6c9-202">**Admin Zustimmung erforderlich**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-202">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="6b6c9-203">**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)**</span><span class="sxs-lookup"><span data-stu-id="6b6c9-203">**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)**</span></span> | <span data-ttu-id="6b6c9-204">Anwendung die Berechtigung</span><span class="sxs-lookup"><span data-stu-id="6b6c9-204">Application permission</span></span> | <span data-ttu-id="6b6c9-205">Ermöglicht die app Gruppen erstellen, lesen und Gruppenmitgliedschaften aktualisieren und Löschen von Gruppen.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-205">Allows the app to create groups, read and update group memberships, and delete groups.</span></span> <span data-ttu-id="6b6c9-206">Alle Vorgänge können von der app, ohne dass ein angemeldeten Benutzer ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-206">All of these operations can be performed by the app without a signed-in user.</span></span> <span data-ttu-id="6b6c9-207">Beachten Sie, dass nicht alle API unterstützt den Zugriff mit nur-app-Berechtigungen zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-207">Note that not all group API supports access using app-only permissions.</span></span> | <span data-ttu-id="6b6c9-208">Ja</span><span class="sxs-lookup"><span data-stu-id="6b6c9-208">Yes</span></span>

<span data-ttu-id="6b6c9-209">Das Microsoft Graph basierend Multi-Geo-Beispiele für die Verbindung mit der Microsoft Graph für den Endpunkt v2 Microsoft Authentifizierung Library (MSAL) verwenden.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-209">The Microsoft Graph based Multi-Geo samples are using the Microsoft Authentication Library (MSAL) to connect with the Microsoft Graph on the v2 endpoint.</span></span> <span data-ttu-id="6b6c9-210">Im Vergleich zu ADAL, der eine Verbindung herstellt, unter Verwendung des Endpunktes v1, MSAL ermöglicht eine Verbindung zu den Microsoft Graph mit Microsoft Accounts, Azure AD und Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-210">Compared to ADAL which connects using the v1 endpoint, MSAL allows connection to the Microsoft Graph with Microsoft Accounts, Azure AD and Azure AD B2C.</span></span> <span data-ttu-id="6b6c9-211">Verwenden Sie die Schritten zur Erstellung des Azure AD-Anwendung, wie im Kapitel "Meine Anwendung muss Read/Update Profile für alle Benutzer können" beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-211">Use the Azure AD application creation steps as described in the "My application needs to be able to read/update profiles for all users" chapter.</span></span>

### <a name="im-using-the-csom-tenant-api"></a><span data-ttu-id="6b6c9-212">Verwende ich die CSOM-Mandanten-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-212">I'm using the CSOM Tenant API</span></span>
<span data-ttu-id="6b6c9-213">Mithilfe der CSOM-Mandanten-API ist ähnlich wie die zuvor beschriebenen CSOM-Anweisungen, in eigentlich der Anleitung für die Verwendung von Benutzeranmeldeinformationen identisch.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-213">Using the CSOM Tenant API is very similar to the previously described CSOM guidance, in a matter of fact the guidance for using user credentials is identical.</span></span> <span data-ttu-id="6b6c9-214">Die Anweisungen für die Verwendung eines nur-app-Prinzipals sind identisch, doch müssen Sie unterschiedliche Berechtigungen (Mandant, Vollzugriff) erteilen:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-214">For using an app-only principal the instructions are the same but you'll need to grant different permissions (tenant, full control):</span></span>

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

## <a name="resources"></a><span data-ttu-id="6b6c9-215">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6b6c9-215">Resources</span></span>
<span data-ttu-id="6b6c9-216">Unterhalb der Liste der Ressourcen sind hilfreich, wenn Sie mehr über die Microsoft Graph-API und die CSOM-API vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="6b6c9-216">Below list of resources are useful when you're learning more about the Microsoft Graph API and CSOM API's:</span></span>
- [<span data-ttu-id="6b6c9-217">Developercenter für Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="6b6c9-217">Microsoft Graph developer center</span></span>](https://developer.microsoft.com/en-us/graph)
- [<span data-ttu-id="6b6c9-218">Abrufen von Zugriffstoken aufrufen, das Diagramm-API</span><span class="sxs-lookup"><span data-stu-id="6b6c9-218">Get access tokens to call the Graph API</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/auth_overview)
- [<span data-ttu-id="6b6c9-219">Microsoft Graph-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="6b6c9-219">Microsoft Graph documentation</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [<span data-ttu-id="6b6c9-220">Diagramm-Explorer</span><span class="sxs-lookup"><span data-stu-id="6b6c9-220">Graph Explorer</span></span>](https://developer.microsoft.com/en-us/graph/graph-explorer)
- [<span data-ttu-id="6b6c9-221">Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="6b6c9-221">App-only and elevated privileges in the SharePoint add-in model</span></span>](app-only-elevated-privileges-sharepoint-add-in.md)
