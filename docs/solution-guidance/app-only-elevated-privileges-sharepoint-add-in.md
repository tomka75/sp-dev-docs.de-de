---
title: "Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: 9bcdbe3f5bb31e0c01fac300bb237bf0134c84a1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
<a name="app-only-and-elevated-privileges-in-the-sharepoint-add-in-model"></a>Nur-App- und erhöhten Berechtigungen in der SharePoint-add-in-Objektmodell
===============================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Erhöhen von Berechtigungen in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario der RunWithElevatedPrivileges-API über Farmlösungen bereitgestellt und mit SharePoint Server-Side-Objektmodellcode verwendet wird.

In einer SharePoint-Add-in Modell Szenario, die Berechtigung AllowAppOnlyPolicy oder ein Dienstkonto wird, dass der aktuellen Benutzer zum Ausführen von Vorgängen, sie sind nicht autorisiert ausführen.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für erhöhen von Berechtigungen im Code bereitstellen.

- AllowAppOnlyPolicy funktioniert nicht mit 
    + Suche – Wenn Ziel SharePoint lokal ist. SharePoint Online-Unterstützung wurden ([Blogbeitrag](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)) hinzugefügt
    + Profil CSOM Benutzervorgänge, mit der Ausnahme, dass der Benutzerprofil Bulk Update-API mit nur-app-Berechtigungen verwendet werden können
    + Aktualisieren der Taxonomie Diensteinträge (Schreiben) - Works lesen
    
    > [!NOTE] 
    > In diesen Szenarien müssen Sie ein bestimmtes Dienstkonto verwenden.

- AllowAppOnlyPolicy ähnelt RunWithElevatedPrivileges, aber nicht genau.
    + AllowAppOnlyPolicy führt Code basierend auf die Berechtigungen für das SharePoint Add-in, nicht im Auftrag einer anderen Benutzers, der die entsprechenden Berechtigungen zum Ausführen eines Vorgangs hat.

Hier ist ein Beispiel für eine nur-App-Richtlinie Token zurückgeben und dessen Verwendung zum Erstellen eines Kontextobjekts.

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

- Wenn Sie mit der AllowAppOnlyPolicy im Hinterkopf behalten funktioniert dies nur in vom Anbieter gehosteten SharePoint-Add-ins.
- AllowAppOnlyPolicy Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.
- Dienstkonten werden in SharePoint definiert.
    + In einer Office 365-Instanz, je nachdem, welche Funktionalität Ihre Code-Bestimmungen unterliegen, die Dienstkonten eine Office 365-Lizenz zugewiesen werden möglicherweise.
    + Erstellen Sie Dienstkonten auf einer pro SharePoint-Add-in-Basis, oder verwenden Sie ein einzelnes Konto für alle SharePoint-Add-ins.
    + Erstellen Sie klare und beschreibende Namen für die Dienstkonten, damit Sie auf einfache Weise die Vorgänge überwachen können, die sie durchführen.
    
    Beispiel: Wenn Ihre SharePoint-Add-in Listenelemente geändert wird, zeigt die Spalte geändert von für die Listenelemente den Namen des Dienstkontos mit dem SharePoint-Add-in verknüpft ist.

- Bei der Authentifizierung mit Dienstkonten müssen Sie einen Benutzernamen und ein Kennwort für das Dienstkonto abrufen.
    + Der folgende Codeausschnitt veranschaulicht die Verwendung von einen Benutzernamen und ein Kennwort um zu authentifizieren.
    + Achten Sie zum Speichern und abrufen, den Benutzernamen und das Kennwort auf sichere Weise.

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {
    
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<a name="options-to-elevate-permissions"></a>Optionen zum Erhöhen von Berechtigungen
------------------------------

Sie haben verschiedene Optionen zum Erhöhen von Berechtigungen.

- OAuth (AllowAppOnlyPolicy)
    + S2S (sub-Option)
    + ACS (Sub Option)
- -Dienstkonto
    + Remote gehosteten Code (Beispiel: Azure WebJob)

<a name="oauth-allowapponlypolicy"></a>OAuth (AllowAppOnlyPolicy)
--------------------------
Die AllowAppOnlyPolicy ist legen Sie diese Option auf true in den AppPermissionRequests-Element und Berechtigungen in der SharePoint-Add-in-Manifest festgelegt sind. OAuth dient zum Zurückgeben Zugriffstoken zum Zulassen des SharePoint-Add-Ins Ausführen von Vorgängen, die diese Berechtigungen zum Ausführen verfügt.

**S2S Sub-option**

Die S2S sub-Option funktioniert nur, wenn in der lokalen SharePoint-Umgebungen.

Beim Authentifizieren über OAuth in einem Szenario S2S die **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** -Methode verwendet, um das Zugriffstoken für das SharePoint-Add-in zurückzugeben.  Das Zugriffstoken ermöglicht die SharePoint-Add-in für alle Vorgänge ausführen des SharePoint-Add-Ins erteilt im SharePoint-Add-in-Manifest.

Diese Option Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.

**Wenn sie geeignet ist?**

Wenn Sie Berechtigungen in einem Szenario mit SharePoint S2S erhöhen müssen ist dies eine gute Wahl, da diese Option mit S2S arbeitet und sehr einfach zu implementieren ist.

**Erste Schritte**

Im folgende Artikel veranschaulicht, wie AllowAppOnlyPolicy mit S2S.

- [SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

**ACS Sub-option**

Die Option ACS Sub Arbeit in lokalen und Office 365 SharePoint-Umgebungen.

Beim Authentifizieren über OAuth in einem Szenario mit ACS die **TokenHelper::GetAppOnlyAccessTokenmethod** verwendet, um das Zugriffstoken für das SharePoint-Add-in zurückzugeben.  Anschließend wird die **TokenHelper::GetClientContextWithAccessToken** -Methode aufgerufen, die Rückgabe Clientkontexts erforderlich sind, um alle Vorgänge ausführen, die des SharePoint-Add-Ins berechtigt ist, anhand von Berechtigungen in der SharePoint-Add-in-Manifest.

Diese Option Code im Auftrag eines Benutzers wird nicht ausgeführt, und daher möglicherweise nicht für alle Szenarien.

**Wenn sie geeignet ist?**

Wenn Sie Berechtigungen in einem Szenario mit SharePoint ACS erhöhen müssen ist dies eine gute Wahl, da diese Option mit ACS arbeitet und sehr einfach zu implementieren ist.  Diese Option ist ideal, wenn Sie eine lokale SharePoint-Umgebung verwenden, die eine Vertrauensstellung mit ACS hat.  Dies ist nur OAuth die Option, wenn Sie eine Office 365 SharePoint-Umgebung haben.

**Erste Schritte**

Im folgende Artikel veranschaulicht, wie AllowAppOnlyPolicy mit ACS.

- [SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<a name="service-account"></a>-Dienstkonto
---------------
In diesem Muster wird die SharePointOnlineCredentials-Klasse verwendet, herstellen im Kontext eines Benutzers, der Code ausgeführt wird.

**Wenn sie geeignet ist?**

Wenn Sie zum Ausführen von Code im Auftrag eines bestimmten Benutzers (Service Account müssen) ist dies eine gute Wahl, da Aktionen des Benutzers (Service Account) und die SharePoint Add-in Berechtigungen ausgeführt.

**Erste Schritte**

Im folgende Artikel veranschaulicht, wie die SharePointOnlineCredentials-Klasse verwendet wird, herstellen im Kontext eines Benutzers, der Code ausgeführt wird.

- [Erste Schritte mit der Erstellung von Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365 (Aspekte im Abschnitt Authentifizierung) - Tobias Zimmergren-Blog-Artikel Websites](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)

<a name="related-links"></a>Verwandte links
=============
- [SharePoint 2013-App nur leicht gemacht Richtlinie (Kirk Evans - MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)
- [Erste Schritte mit der Erstellung von Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365 (Aspekte im Abschnitt Authentifizierung) - Tobias Zimmergren-Blog-Artikel Websites](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)
- [SharePointOnlineCredentials-Klasse (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.sharepointonlinecredentials.aspx)
- [Verwenden von Add-in- / nur-app-Berechtigungen mit Suchabfragen in SharePoint Online - Vesa Juvonen Blog-Artikel](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.SimpleTimerJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
