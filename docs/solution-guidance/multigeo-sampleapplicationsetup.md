---
title: Richten Sie Ihre Multi-Geo Beispielanwendungen
ms.date: 11/03/2017
ms.openlocfilehash: 5974998440e13f99fb7b025d1dcd70d84c2edd06
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-your-multi-geo-sample-applications"></a>Richten Sie Ihre Multi-Geo Beispielanwendungen

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Bei der Entwicklung für einen Mandanten Multi-Geo ist es wichtig zu verstehen, das Sicherheitsmodell und zum Glück verwendete Modell für einen Mandanten Multi-Geo unterscheidet sich nicht aus dem Modell für einen regulären Mandanten verwendet. In diesem Artikel wird das Konfigurieren der Beispielanwendungen veranschaulicht.

## <a name="my-application-needs-to-be-able-to-readupdate-profiles-for-all-users"></a>Meine Anwendung benötigt Lese-/Profile für alle Benutzer aktualisieren können
### <a name="im-using-the-microsoft-graph-api"></a>Ich verwende Microsoft Graph-API
Wie im Artikel [Multi-Geo Profil Benutzererlebnis](multigeo-userprofileexperience.md) erläutert ist das bevorzugte Modell zum Lesen/Aktualisieren von Benutzerprofileigenschaften mithilfe der API: Grafik. In diesem Kapitel wird erläutert, welche Berechtigungen Sie so gewähren Sie der Anwendung, Mandanten breit Benutzerprofil Lesevorgänge und Updates zu erzielen müssen. Es gibt [eine lange Liste von Berechtigungen](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) , dass Sie zu einer Anwendung in Azure AD definierten gewähren können, aber für die Bearbeitung von Benutzerprofilen können Sie Berechtigungen zum einschränken:

|**Berechtigung**|**Typ**|**Beschreibung**| **Admin Zustimmung erforderlich**
|:-----|:-----|:-----|:-----|
|**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Anwendung die Berechtigung | Ermöglicht der App, den vollständigen Satz von Profileigenschaften, Gruppenmitgliedschaften, Berichten und Vorgesetzten von anderen Benutzern in Ihrer Organisation ohne angemeldeten Benutzer zu lesen und zu schreiben.  Außerdem können die app zum Erstellen und Löschen von Benutzern ohne Administratorrechte. Zurücksetzen von Benutzerkennwörtern ist nicht zulässig. | Ja
|**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Anwendung die Berechtigung | Ermöglicht die app den Lese-/Schreibzugriff Dokumente und Listenelemente in allen Websitesammlungen, ohne dass ein Benutzer angemeldet. Diese Berechtigung ist nur erforderlich, wenn die Anwendung Speicherorts für persönliche Websites des Benutzers abrufen (z. B. https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$ wählen =-MeineWebsite) | Ja

Das Microsoft Graph basierend Multi-Geo-Beispiele für die Verbindung mit der Microsoft Graph für den Endpunkt v2 Microsoft Authentifizierung Library (MSAL) verwenden. Im Vergleich zu ADAL, der eine Verbindung herstellt, unter Verwendung des Endpunktes v1, MSAL ermöglicht eine Verbindung zu den Microsoft Graph mit Microsoft Accounts, Azure AD und Azure AD B2C. Unten Anweisungen helfen Ihnen beim setup von der Anwendung für den Endpunkt v2, aber Sie können auch den "älteren" Ansatz basierend auf den v1-Endpunkten verwenden.

#### <a name="register-your-application"></a>Registrieren Sie Ihre Anwendung
Berechtigungen für die Microsoft Graph verwenden Sie zuerst die Anwendung zu registrieren müssen. Dabei wird unter https://apps.dev.microsoft.com. Nach der Anmeldung in Klick fügen Sie eine neue Zusammengef-Anwendung, indem Sie auf app hinzufügen

![Registrieren Sie die Anwendung in Azure AD](media/multigeo/multigeopermissions_registerapp1.png)

Geben Sie der Anwendung einen Namen ein, und drücken Sie Anwendung erstellen.

Konfigurieren Sie im Konfigurationsbildschirm Anwendung Folgendes:
- Generieren Sie ein Kennwort, und notieren Sie es zusammen mit der Id der Anwendung
- Klicken Sie auf 'Plattform hinzufügen', und wählen Sie "Systemeigene Anwendung" als Zielplattform, wie die Anwendung ein Zielseite nicht vorhanden ist
- Fügen Sie die erforderliche Berechtigung für die Anwendung hinzu. In diesem Beispiel-app haben wir die User.ReadWrite.All und Sites.ReadWrite.All Berechtigungen hinzugefügt.
- Stellen Sie sicher, 'Live SDK Unterstützung' deaktivieren
- Speichern Ihrer Änderungen einmal konfiguriert.

![Konfigurieren von Anwendung in Azure AD-Teil 1](media/multigeo/multigeopermissions_registerapp2.png)

![Konfigurieren von Anwendung in Azure AD-Teil 2](media/multigeo/multigeopermissions_registerapp3.png)


#### <a name="consent-to-the-application"></a>Einverständnis, dass die Anwendung
In diesem Beispiel die User.ReadWrite.All und erfordern Sites.ReadWrite.All Anwendungsberechtigungen Admin Zustimmung in einem Mandanten bevor verwendet werden können. Erstellen Sie eine Zustimmung URL wie folgt:

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<clientid>&state=<something>
```

Verwenden die Client-Id aus der app registriert und damit einverstanden, die app aus Meine Mandanten contoso.onmicrosoft.com, sieht die URL folgendermaßen aus:

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

Durchsuchen, um das erstellte URL und melden Sie sich als Administrator und Zustimmung an die Anwendung. Sie können den Zustimmung Bildschirm zeigen Sie den Namen der Anwendung als auch die von Ihnen konfigurierten berechtigungsbereiche sehen.

![Mandanten Zustimmung für Azure AD-Anwendung](media/multigeo/multigeopermissions_registerapp4.png)

### <a name="im-using-the-csom-user-profile-api"></a>Verwende ich die CSOM Benutzerprofil-API
Beim Verwenden der CSOM-API zum Bearbeiten von Benutzerprofileigenschaften, die Sie nur dann tun, werden für die erstellten benutzerdefinierten Eigenschaften seit Out-of-Box-Eigenschaften besser sind über die Microsoft Graph-API... behandelt finden Sie im Artikel [Multi-Geo Benutzererlebnis Profil](multigeo-userprofileexperience.md) nach weiteren Details. Aus Sicht einer Berechtigung gibt es zwei Modi:

#### <a name="using-user-credentials"></a>Verwenden von Benutzeranmeldeinformationen
Dies erfordert das Einrichten einer `ClientContext` -Objekts verwenden die Mandanten-Admin-Url und Verwenden von SharePoint Online-Admin-Anmeldeinformationen. Da es ist nur eine einzige Azure AD-Instanz, die gedrückt halten, Benutzer bedeutet dies auch, dass ein SharePoint Online Admin Admin für alle Speicherorte Geo ist.

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

#### <a name="using-an-app-only-principal"></a>Mithilfe eines nur-app-Prinzipals
Bei Verwendung der nur-app-müssen Sie das erstellte app principal **Vollzugriff** für den Bereich der [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) Berechtigung erteilen. Unten Anweisungen zeigen Sie zum Registrieren eines app-Prinzipals und stimmen sie die Verwendung von "appregnew.aspx" und "appinv.aspx an".

##### <a name="create-the-principal"></a>Erstellen des Prinzipals
Navigieren Sie zu einer Website in Ihrem Mandanten (z. B. https://contoso.sharepoint.com), und rufen Sie dann auf der Seite "appregnew.aspx" (z. B. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx). In dieser Seite klicken Sie auf die Schaltfläche generieren, um eine Client-Id und den geheimen Clientschlüssel generieren und füllen Sie die verbleibende Informationen wie in der Screenshot-unten angezeigt.

![Registrieren von app-Prinzipal ACS](media/multigeo/multigeopermissions_registerprincipal1.png)

> **Wichtige** Speichern Sie die abgerufene Informationen (Client-Id und den geheimen Clientschlüssel), da Sie dies im nächsten Schritt benötigen!

##### <a name="grant-permissions-to-the-created-principal"></a>Erteilen von Berechtigungen für den erstellten Prinzipal
Nächsten Schritt wird das Erteilen von Berechtigungen für die neu erstellte Prinzipal. Da wir Mandanten bezogenen Berechtigungen gewähren kann dieses Verfahren nur über die Seite "appinv.aspx" auf die Mandantenverwaltungs-Website ausgeführt werden. Sie können diese Website über https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx erreichen. Nach dem Laden der Seite fügen Sie Ihrer Client-Id hinzu und den erstellten Prinzipal nachschlagen:

![Erteilen von Berechtigungen für app-Prinzipal](media/multigeo/multigeopermissions_registerprincipal2.png)

Um Berechtigungen zu erteilen, müssen Sie die Berechtigung XML bereitstellen, auf denen die erforderlichen Berechtigungen beschrieben. Seit die Benutzeroberfläche auftreten Scanner muss auf allen Websites zugreifen + verwendet auch mit nur-app-Suche ist es unten aufgeführten Berechtigungen erforderlich:

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="FullControl" />
</AppPermissionRequests>
```

Wenn Sie auf Create wird eine Berechtigung Zustimmungsdialogfeld angezeigt. Drücken Sie vertrauen, die Berechtigungen erteilen:

![Zustimmung der app-Prinzipal](media/multigeo/multigeopermissions_registerprincipal3.png)


##### <a name="use-the-principal-in-your-code"></a>Verwenden Sie den Prinzipal in Ihrem code
Sobald der Prinzipal erstellt und zugestimmt ist können des Prinzipals-Id und geheimen Schlüssel Sie eine Access anfordern. Die `TokenHelper.cs` Klasse wird die Id und geheimen Clientschlüssel aus der Anwendungskonfigurationsdatei Code.

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

Ein Beispiel app.config sieht folgendermaßen aus:

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
> Sie können auf einfache Weise einfügen der `TokenHelper.cs` -Klasse in Ihrem Projekt, indem Sie die **AppForSharePointOnlineWebToolkit** Nuget-Paket für Ihre Lösung.

## <a name="my-application-needs-to-be-able-to-be-able-to-discover-the-multi-geo-configuration"></a>Meine Anwendung muss die Konfiguration mit mehreren geografisch ermitteln können können
### <a name="im-using-the-microsoft-graph-api"></a>Ich verwende Microsoft Graph-API
Die einzige unterstützte API entdecken Sie die Geo Speicherorte in einem Multi-Geo-Mandanten mithilfe der API: Grafik ist. In diesem Kapitel wird erläutert, welche Berechtigungen Sie so gewähren Sie die Anwendung zum Ermitteln von Multi-Geo-Informationen müssen. Es gibt [eine lange Liste von Berechtigungen](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) , dass Sie zu einer Anwendung in Azure AD definierten gewähren können, aber für das Lesen von Multi-Geo Mandanten Konfigurationsinformationen können Sie Berechtigungen zum einschränken:

|**Berechtigung**|**Typ**|**Beschreibung**| **Admin Zustimmung erforderlich**
|:-----|:-----|:-----|:-----|
|**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Anwendung die Berechtigung | Ermöglicht die app den Lese-/Schreibzugriff Dokumente und Listenelemente in allen Websitesammlungen, ohne dass ein Benutzer angemeldet. | Ja

Verwenden Sie die Schritten zur Erstellung des Azure AD-Anwendung, wie im Kapitel "Meine Anwendung muss Read/Update Profile für alle Benutzer können" beschrieben.

## <a name="my-application-needs-to-be-able-to-createdelete-sites-collections-or-set-tenant-site-collection-properties"></a>Meine Anwendung muss können Websitesammlungen erstellen/löschen oder Festlegen der Eigenschaften der Websitesammlung Mandanten
### <a name="im-using-the-microsoft-graph-api"></a>Ich verwende Microsoft Graph-API
Die [Multi-Geo Websites](multigeo-sites.md) enthält weitere Details zum (auch bekannt als Gruppe Websites erstellen "modernen" Teamwebsites) mit der Microsoft Graph-API in diesem Abschnitt wir sind nur reagieren auf Berechtigungen. Unter Tabelle enthält die erforderlichen Berechtigungen

|**Berechtigung**|**Typ**|**Beschreibung**| **Admin Zustimmung erforderlich**
|:-----|:-----|:-----|:-----|
|**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)** | Anwendung die Berechtigung | Ermöglicht die app Gruppen erstellen, lesen und Gruppenmitgliedschaften aktualisieren und Löschen von Gruppen. Alle Vorgänge können von der app, ohne dass ein angemeldeten Benutzer ausgeführt werden. Beachten Sie, dass nicht alle API unterstützt den Zugriff mit nur-app-Berechtigungen zu gruppieren. | Ja

Das Microsoft Graph basierend Multi-Geo-Beispiele für die Verbindung mit der Microsoft Graph für den Endpunkt v2 Microsoft Authentifizierung Library (MSAL) verwenden. Im Vergleich zu ADAL, der eine Verbindung herstellt, unter Verwendung des Endpunktes v1, MSAL ermöglicht eine Verbindung zu den Microsoft Graph mit Microsoft Accounts, Azure AD und Azure AD B2C. Verwenden Sie die Schritten zur Erstellung des Azure AD-Anwendung, wie im Kapitel "Meine Anwendung muss Read/Update Profile für alle Benutzer können" beschrieben.

### <a name="im-using-the-csom-tenant-api"></a>Verwende ich die CSOM-Mandanten-API
Mithilfe der CSOM-Mandanten-API ist ähnlich wie die zuvor beschriebenen CSOM-Anweisungen, in eigentlich der Anleitung für die Verwendung von Benutzeranmeldeinformationen identisch. Die Anweisungen für die Verwendung eines nur-app-Prinzipals sind identisch, doch müssen Sie unterschiedliche Berechtigungen (Mandant, Vollzugriff) erteilen:

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

## <a name="resources"></a>Ressourcen
Unterhalb der Liste der Ressourcen sind hilfreich, wenn Sie mehr über die Microsoft Graph-API und die CSOM-API vertraut machen:
- [Developercenter für Microsoft Graph](https://developer.microsoft.com/en-us/graph)
- [Abrufen von Zugriffstoken aufrufen, das Diagramm-API](https://developer.microsoft.com/en-us/graph/docs/concepts/auth_overview)
- [Microsoft Graph-Dokumentation](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [Diagramm-Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
- [Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell](app-only-elevated-privileges-sharepoint-add-in.md)
