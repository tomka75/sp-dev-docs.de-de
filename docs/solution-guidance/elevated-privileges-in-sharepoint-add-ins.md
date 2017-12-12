---
title: "Erhöhten Berechtigungen in SharePoint-Add-ins"
ms.date: 11/03/2017
ms.openlocfilehash: 1408ea8317d59a9e1408a2e7ebd1b88946cf0042
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="elevated-privileges-in-sharepoint-add-ins"></a>Erhöhten Berechtigungen in SharePoint-Add-ins

Verwenden Sie die Richtlinie nur für Apps oder Dienstkonten, um Berechtigungen in SharePoint-Add-ins zu erhöhen.

_**Gilt für:** apps für SharePoint | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Verschiedene Methoden werden verwendet, um Berechtigungen in SharePoint-Add-ins und Farm Solutions erhöhen. Farmlösungen ausweiten Berechtigungen mithilfe von RunWithElevatedPrivileges(SPSecurity.CodeToRunElevated), der auf das Objektmodell für SharePoint Server-Side gehört. SharePoint-Add-ins verwenden, die nur-app Richtlinie oder Dienstkonten.

Möglicherweise möchten Sie erhöhten in Ihr Add-in verwenden, wenn:

* Aktionen werden durchgeführt Ihr Add-In für Benutzer, die die Benutzer nicht über ausreichend einzelne Berechtigungen für die Durchführung aufweisen. Administratoren können nicht Benutzern bestimmte Berechtigungen zuweisen, da die Berechtigungsstufe zu hoch ist.

   Ihre Organisation möglicherweise, beispielsweise implementieren eine benutzerdefinierten Websitesammlung Benutzerwebsite, mit denen Benutzer Websitesammlungen erstellen müssen. Ihre Organisation möglicherweise angeben, dass alle neuen Websitesammlungen bestimmte Listen, Inhaltstypen oder Felder zugeordnet sein müssen. Wenn Benutzer Websitesammlungen auf ihre eigenen erstellen, werden sie möglicherweise oder möglicherweise nicht vergessen Sie nicht, diese Objekte auf ihre neue Websitesammlung zu erstellen. In diesem Szenario Benutzer erstellen von Websitesammlungen mithilfe des Add-Ins, aber Benutzer werden nicht einzeln Berechtigungen zum Erstellen von Websitesammlungen zugewiesen.

* Ihr Add-in fungiert nicht von jedem Benutzer; beispielsweise ein Steuerung oder Management Prozess.

## <a name="app-only-policy-authorization"></a>Nur-App Richtlinie-Autorisierung

Nur-App Richtlinie verwendet OAuth, um das Add-in zu authentifizieren. Wenn das Add-in die nur-app-Richtlinie verwendet wird, überprüft SharePoint die Berechtigungen des Add-in-Prinzipals nur an. Dies sind die Berechtigungen, die das Add-in erteilt wurden. Autorisierung erfolgreich, wenn das Add-in über ausreichende Berechtigungen zum Ausführen der Aufgabe, unabhängig von den Berechtigungen, die dem aktuellen Benutzer zugeordnet ist. Wenn Autorisierung erfolgreich ist, wird ein Zugriffstoken an Ihr Add-In zurückgegeben. Das Add-In wird dieses Zugriffstoken verwenden, um keine Aktionen erforderlich sind, vom Code ausführen.

Weitere Informationen finden Sie unter [App-autorisierungsrichtlinientypen in SharePoint 2013](https://msdn.microsoft.com/library/office/fp179892.aspx).

> [!NOTE] 
> Die nur-app-Richtlinie ist nur für SharePoint-Hosting-add-ins, dass die Host-Web Access werden, die Benutzer + app-Richtlinie verwendet muss vom Anbieter gehosteten add-Ins verfügbar.

Vorteile der Verwendung der nur-app-Richtlinie in der Include-add-in:

* Sie müssen nicht keine separate Benutzerlizenz zu erteilen. Dienstkonten erfordern keine separate Benutzerlizenz.

* Sie erhalten eine genauere Kontrolle über Berechtigungen als mit Dienstkonten zur Verfügung steht. Sie können beispielsweise Vollzugriff-Berechtigungen auf dem Webserver anwenden, die nicht möglich, wenn Sie Dienstkonten verwenden.

Sie können nicht nur-app-Richtlinie mit die folgenden APIs verwenden:

* Benutzerprofil

* Suche

* Taxonomie (gilt nur für Szenarien, die in den verwalteten Metadatendienst schreiben)

Um die nur-app-Richtlinie zu verwenden, müssen Sie zunächst die Berechtigungen für das Add-in erteilen, mithilfe von "appinv.aspx". Der folgende Code aus der Datei AppManifest.XML veranschaulicht, wie der nur-app-Richtlinie und die Berechtigungen für das add-in fest.

```xml
 <AppPermissionRequests AllowAppOnlyPolicy="true">
   <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="FullControl" />
 </AppPermissionRequests>
```

Mit der nur-app-Richtlinie erfordert, dass Ihr Add-in niedriger oder hoher Vertrauenswürdigkeit Autorisierung verwenden. Die Richtlinie ist nicht mit der SharePoint Cross-Domain-JavaScript-Bibliothek, die ist eine dritte Möglichkeit zum Abrufen von autorisierten Zugriffs auf SharePoint-Ressourcen verfügbar.

### <a name="low-trust-authorization"></a>Autorisierung mit niedriger Vertrauenswürdigkeit

Ihr Add-In kann beim Microsoft Azure Access Control Service (ACS) zum Einrichten der Vertrauensstellung zwischen Ihrer vom Anbieter gehosteten-add-in und Ihre Office 365-Website oder Ihre lokale SharePoint-Farm mit niedriger Vertrauenswürdigkeit Autorisierung verwenden. Sie können unter [drei Autorisierung Systeme für SharePoint-Add-ins 2013](https://msdn.microsoft.com/en-us/library/office/dn790706.aspx)informieren. Wenn Sie einen Verweis auf das [ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) -Objekt erhalten möchten, sollte Ihr Add-in:

1. Rufen Sie den Zugriff mithilfe der TokenHelper.GetAppOnlyAccessToken token ab.

2. Verwenden Sie TokenHelper.GetClientContextWithAccessToken, um das ClientContext-Objekt abzurufen.

> [!NOTE] 
> Die Datei TokenHelper wird Quellcode, die von der Microsoft Office Developer Tools für Visual Studio generiert wird. Es ist keine Referenzdokumentation dafür, aber es sind umfassende Kommentare in die TokenHelper-Klasse. Um die Codekommentare angezeigt wird, erstellen Sie eine vom Anbieter gehosteten-add-in in Visual Studio.

> [!NOTE] 
> IE-Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

### <a name="high-trust-authorization"></a>Besonders

Wenn Ihr Add-in des besonders vertrauenswürdigen autorisierungssystems (auch bekannt als S2S Protocol) verwendet wird, ruft es eine andere Methode **TokenHelper** : **TokenHelper.GetS2SAccessTokenWithWindowsIdentity**.

**Wichtig:** Die **TokenHelper.GetS2SAccessTokenWithWindowsIdentity** für beide nur-app-verwendet wird, und Benutzer + app aufruft. Der zweite Parameter der Methode, die die Identität des Benutzers enthält, bestimmt, welche Richtlinie verwendet wird. Übergeben Sie **null** , um die nur-app-Richtlinie verwenden.

## <a name="service-accounts"></a>Dienstkonten

Verwenden Sie Dienstkonten, um Berechtigungen für das add-in zu erhöhen, nur, wenn die Richtlinie nur für Apps nicht über ausreichende Berechtigungen zum Ausführen der Aufgabe bereitstellt. Darüber hinaus ist ein Benutzerkonto in bestimmten Szenarien erforderlich. Beispielsweise müssen Sie Dienstkonten verwenden, wenn Ihr Code mit einem der folgenden SharePoint-dienstanwendungen funktioniert:

* Benutzerprofildienst mit dem clientseitigen Objektmodell (CSOM)

* Verwalteter Metadatendienst

* Suche

Bei der Planung von Dienstkonten in Ihr Add-in verwenden, beachten Sie Folgendes:

* Dienstkonten erfordern keine separate Benutzerlizenz.

* Erstellen Sie entweder ein Dienstkonto pro-add-in, oder verwenden Sie ein Dienstkonto für alle Add-Ins in Ihrer SharePoint-Umgebung.

* Sie müssen den Benutzernamen und das Kennwort während der Autorisierung bereitstellen. Stellen Sie sicher, Anmeldeinformationen für das Dienstkonto gespeichert oder abgerufen sicher.

* Bevor das Add-in eine Aktion auf einer Website ausführen kann, müssen Dienstkonten zunächst über die Berechtigung zum Zugriff auf die Website erteilt werden.

> [!NOTE] 
> Add-ins aus dem Office Store erworben haben, kann nicht Dienstkonten verwenden.

Der folgende Code zeigt, wie Sie mithilfe von [SharePointOnlineCredentials](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.sharepointonlinecredentials.aspx) mit einem Dienstkonto zu authentifizieren.

```cs
using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
{

    // Use default authentication mode.
    context.AuthenticationMode = ClientAuthenticationMode.Default;  

    // Specify the credentials for the service account.
    context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
}
```

## <a name="see-also"></a>Siehe auch

- [Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).
- [Add-in - autorisierungsrichtlinientypen in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179892.aspx).
- [Office 365 SharePoint-Website zum Autorisieren von vom Anbieter gehosteten-add-ins auf einer lokalen SharePoint-Website verwenden](https://msdn.microsoft.com/en-us/library/office/dn155905.aspx).
