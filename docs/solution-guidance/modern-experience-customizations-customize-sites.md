---
title: Anpassen von "modernen" Teamwebsites
description: Anwenden eines benutzerdefinierten Designs zu einer "modernen" Teamsite in SharePoint Online.
ms.date: 11/08/2017
ms.openlocfilehash: 4341876f6ee07018325c5cc089cc28728538ab10
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="customizing-modern-team-sites"></a>Anpassen von "modernen" Teamwebsites

Im 2016 veröffentlicht das SharePoint Online-Team Websites "modernen" für die Zusammenarbeit. Diese "modernen" Teamwebsites in Office 365 Gruppen integriert werden und eine erheblich verbesserte Endbenutzers bringen. "Modernen" Teamwebsites sind entwurfsbedingt schnell und viel schneller erstellen und aus Sicht der Endbenutzer verwenden. Es folgen einige der wichtigsten Vorteile der "modernen" Teamwebsites:

- Entwickelt für die horizontale Skalierung für jedes Gerät systemintern ohne Anpassungen für eine vollständig Reaktionsfähigkeit bereitzustellen.
- Enthalten Sie systemeigene News, Quicklinks und Aktivität Funktionen. 
- Integration mit Office 365-Gruppen. 
- Wesentlich schneller websiteerstellung im Vergleich zu Teamwebsites "klassische".
- Einschließen Sie "modernen" Listen und Bibliotheken mit Support für Microsoft Flow und PowerApps.
- Enthalten Sie "modernen" Seite Bearbeitungsfunktionen.
- Enthalten Sie eine Seite mit zusätzlichen Insights auf der Websiteverwendung aktualisierte Websiteinhalte.

In diesem Artikel konzentriert sich auf die der verfügbaren Erweiterbarkeitsoptionen "modernen" Teamwebsites:

- [Neue Funktionen in SharePoint Online, einschließlich der Integration mit Office 365 Gruppen Teamwebsites](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups)
- [Erstellen von verbundenen SharePoint Online Teamwebsites in Sekunden](https://blogs.office.com/2016/11/08/create-connected-sharepoint-online-team-sites-in-seconds)
- [Ermöglichen oder verhindern, dass benutzerdefinierte Skripts](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US)

> [!IMPORTANT]
> Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.

<a name="supportedcustomizations"> </a>
## <a name="supported-customizations-on-modern-team-sites"></a>Unterstützte Anpassungen von "modernen" Teamwebsites

"Modernen" Websites haben eine andere Ebene Anpassungsoptionen im Vergleich zu Teamwebsites "klassische". Über einen Zeitraum wird eine Einführung Weitere Anpassungsoptionen hauptsächlich Konzentration auf Erweiterbarkeit und branding. Die folgende Liste enthält einen schnellen Überblick über die unterstützten Funktionen für "modernen" Teamwebsites. Sie haben folgenden Möglichkeiten:

- Anwenden eines benutzerdefinierten Designs, oder ändern Sie das Logo.
- Ein Out-of-Box-Design anwenden.
- Erstellen Sie benutzerdefinierte Websitespalten (Felder) und Inhaltstypen.
- Erstellen von Listen und Bibliotheken.
- Konfigurieren von Einstellungen der Website, wie beispielsweise regionale Einstellungen, Sprachen und Überwachungsrichtlinien.

> [!NOTE]
> Standardmäßig weist eine Teamwebsite "modernen" AppleScript deaktiviert. Sie können ein benutzerdefiniertes Design trotzdem anwenden, jedoch können nicht führen Sie ein benutzerdefiniertes Design in den Designkatalog als Option für Endbenutzer. Wenn Sie ein Design in den Designkatalog hinzufügen möchten, müssen Sie auf der Website [Skripts aktivieren möchten](https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f) .

<a name="notsupported"> </a>
### <a name="whats-not-supported-on-modern-team-sites"></a>Was ist auf "modernen" Teamwebsites nicht unterstützt

Zahlreiche Bereiche auf den "modernen" Teamwebsites sind die typischen Anpassungen zurzeit nicht verfügbar. Weiterer Unterstützung werden für einige dieser Themen verfügbar sein, wenn sie bereit sind, freigegeben werden muss. Es folgt eine Liste der derzeit nicht unterstützte Anpassungen von "modernen" Teamwebsites:

- Benutzerdefinierte Masterseiten; eine ausführlichere branding wird später mit alternative Optionen unterstützt werden.
- Ändern der "modernen" Website "klassische" seattle.master oder oslo.master verwenden.
- Benutzerdefinierten Seitenlayouts; Wir suchen nach wegen, um die Unterstützung für mehrere explizite in der Zukunft haben.
- Aktivieren der Website oder Websitesammlung begrenzt Veröffentlichungsfeatures. Technisch gesehen Features derzeit aktiviert werden können, aber dies wird nicht unterstützt.
- Benutzerdefinierte Benutzeraktionen / benutzerdefiniertes JavaScript; mehr kontrolliert JavaScript auf den Seiten über die SharePoint-Framework-Erweiterungen (derzeit in Developer Preview) eingebettet werden.
- "Modernen" Unterwebsites; Unterwebsites auf "modernen" Teamwebsites erstellten verwenden der "klassischen" wünschen, aber Sie können die Benutzeroberfläche "modernen" Websites ähnlich sein, um ändern.
- Die Möglichkeit, verfügbaren Unterwebsite Vorlagenoptionen steuern.
- "Klassische" Veröffentlichen von Features (WCM).
- Aktivierung von Communityfeature oder der Community Unterwebsites unter "modernen" Teamwebsite Creation.

Da "modernen" Teamwebsites auch haben AppleScript deaktiviert (es ist eine so genannte NoScript-Website), zahlreiche Bereiche können nicht angepasst werden. Die Auswirkung NoScript ist für "modernen" oder "klassische" Sites identisch. "Modernen" Websites haben NoScript standardmäßig aktiviert, was bedeutet, dass Skriptfunktionen nicht verfügbar sind. Es ist jedoch möglich und unterstützte NoScript Einstellungen in "modernen" und "klassische" Websites, um weitere einige Funktionen aktivieren deaktivieren. 

Berücksichtigen Sie beim Entwerfen von Lösungen diese Bereiche im Zusammenhang mit der Einstellung NoScript:

- Sandkastenlösungen werden nicht unterstützt.
- Benutzerdefiniertes JavaScript kann nicht auf den Websites mithilfe von "klassische" Erweiterbarkeitsoptionen (beispielsweise über benutzerdefinierte Benutzeraktionen) aktiviert werden.
- Sie können nicht mithilfe von SharePoint Designer Websites zugreifen.
- Einige Webparts sind nicht verfügbar für Endbenutzer.
- Die Möglichkeit, Access oder Update-Website-Eigenschaft Eigenschaftensammlung Einträge.

> [!NOTE]
> Sie können die vollständige Liste der betroffene Funktionen aus dem Microsoft Support-Artikel suchen [Zulassen oder verhindern, dass benutzerdefinierte Skripts](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US) klicken Sie im Abschnitt "Features betroffen, wenn benutzerdefinierte Skripts blockiert wird".

<a name="pnpprovisioningengine"> </a>
### <a name="using-pnp-provisioning-engine-with-modern-team-sites"></a>Verwenden von Plug & Play-Bereitstellung Engine mit "modernen" Teamwebsites

Sie können die [Plug & Play-Bereitstellung Engine](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) mit "modernen" Teamwebsites verwenden. Das Plug & Play-Bereitstellung Modul erkennt automatisch auf, wenn eine Website eine "modernen" Teamwebsite ist und passt dieses Verhalten basierend auf den unterstützten Funktionen an. Der Prozess entspricht genau der Verwendung der Plug & Play-Bereitstellung Engine mit "klassische" Websites, bei denen die Skriptfunktionen nicht deaktiviert werden.

Die folgenden Elemente werden ignoriert, wenn eine remote-Vorlage auf einer Teamwebsite "modernen" oder einer Website, die NoScript aktiviert hat angewendet wird:

- Standortkonfiguration Auflistung **AuditLogTrimmingRetention** in der Überwachungsrichtlinien
- Anwenden eines benutzerdefinierten Designs aus der Vorlage; aktuelle Implementierung hat eine Abhängigkeit zum Speichern von ein benutzerdefiniertes Design auf den Katalog, die nicht unterstützt wird
- Formular Einstellungen für Inhaltstypen
- Hinzufügen von benutzerdefinierten Aktionen zu Websites, Web oder Listenebene
- Hinzufügen von Dateien mit Dateitypen der "asmx", "aspx", "aspx", ".htc", "JAR-", "Master", "SWF", "XAP", "xsf"
- Hinzufügen von Dateien zu Bibliotheken mit den folgenden Urls `"_catalogs/theme"`, `"style library"`, `"_catalogs/lt"`,`"_catalogs/wp"`
- Hinzufügen von Webparts zu Seiten der Website
- Speichern von Vorlage Bereitstellungsinformationen der Eigenschaftensammlung der bereitgestellten Website
- Hinzufügen oder Aktualisieren der Eigenschaftensammlung der Website-Eigenschaftensammlung
- "Klassische" Veröffentlichen von Einstellungen und Objekte
- Website keine Einstellungen für die Durchforstung
- Einstellungen für die Website-Gestaltungsvorlage

## <a name="apply-a-custom-theme-to-a-modern-team-site"></a>Anwenden eines benutzerdefinierten Designs auf einer Teamwebsite "modern"

"Modernen" Teamwebsites unterstützen benutzerdefinierte Designs, auch wenn Sie einen neuen Katalog-Eintrag für Endbenutzer Hochladen ist nicht möglich. Dies kann durch Hochladen der benötigten Objekte in der Website, und klicken Sie dann ausführen **ApplyTheme** -Methode erreicht werden. Das folgende PowerShell-Skript zeigt, wie dies für eine Teamwebsite "modernen" ausführen.

```PowerShell

# Connect to a previously created Modern Site
$cred = Get-Credential
Connect-PnPOnline https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Apply a custom theme to a Modern Site

# First, upload the theme assets
Add-PnPFile -Path .\sppnp.spcolor -Folder SiteAssets
Add-PnPFile -Path .\sppnp-bg.png -Folder SiteAssets

# Second, apply the theme assets to the site
$web = Get-PnPWeb
$palette = $web.ServerRelativeUrl + "/SiteAssets/sppnp.spcolor"
$background = $web.ServerRelativeUrl + "/SiteAssets/sppnp-bg.png"

# We use OOTB CSOM operation for this
$web.ApplyTheme($palette, [NullString]::Value, $background, $true)
$web.Update()
# Set timeout as high as possible and execute
$web.Context.RequestTimeout = [System.Threading.Timeout]::Infinite
$web.Context.ExecuteQuery()

```

<br/>

*Abbildung 1. "Modernen" Teamwebsite mit benutzerdefinierten Designs*

!["Modernen" Teamwebsite mit benutzerdefinierten Designs](media/modern-experiences/modern-site-with-custom-theme.png)

> [!NOTE]
> - Sie können das [Tool für SharePoint Farbe Palette](https://www.microsoft.com/en-us/download/details.aspx?id=38182) zum Erstellen einer benutzerdefinierten Designs-Datei (.spcolor) mit der Definition von benutzerdefinierten Farbe verwenden. Versuchen Sie im Allgemeinen "modernen" Teamwebsites, das Verhalten des Designs durch die Umwandlung der "klassischen" Designoberfläche Websiteelemente automatisch auf der Seite "modernen" beibehalten. Beibehaltene Bereichen sind Hintergrundbild und die folgenden Design Steckplätze: ContentAccent1 PageBackground und BackgroundOverlay.
> - Sie können das Logo der Teamwebsite "modernen" ändern, indem die Gruppen Diagramm-API wie von der SharePoint- [Plug & Play-UpdateUnifiedGroup-Methode](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs#L350).
> - Anwenden eines benutzerdefinierten Designs auf einer Teamwebsite "modernen" kann zu Timeouts führen. Die Lösung für dieses besteht darin, alle verfügbaren [Benutzeroberflächensprachen](https://support.office.com/en-us/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) für die Website vor dem Anwenden des Designs deaktivieren und anschließend wieder aktivieren.

## <a name="determine-if-a-site-is-a-modern-team-site"></a>Bestimmen Sie, ob eine Website einer Teamwebsite "moderne" ist

Sie können erkennen, dass eine Website einer Teamwebsite "modernen" wird durch den Wert "Web.WebTemplate" der Website überprüfen. "Modernen" Teamwebsites verwenden Sie die Vorlage "GROUP". Da die unterstützten Funktionen für eine "klassische" Teamwebsite identisch, sind Wenn das scripting deaktiviert ist, Sie sollten beide Einstellungen im Code zu bestimmen, das rechte-Verhalten überprüfen oder Funktionen unterstützt.

Da keine direkte Eigenschaft zu überprüfen, ob die scripting oder nicht aktiviert ist vorhanden ist, können Sie Berechtigungen verwenden, um den aktuellen Status zu ermitteln. Wenn scripting aktiviert ist, ist gibt es keine AddAndCustomizePages Berechtigung in die Basisberechtigungen der Website.

```C#
/// <summary>
/// Can be used to check if site has noscript enabled.
/// </summary>
/// <param name="web">site object to inspect</param>
/// <returns>True if no scripting is enabled, False if it's not</returns>
public static bool IsNoScriptSite(Web web)
{
    // Ensure that we have the needed properties - Notice that these are 
    // PnP CSOM extension capabilities
    web.EnsureProperties(w => w.WebTemplate, w => w.EffectiveBasePermissions);

    // Definition of no-script is not having the AddAndCustomizePages permission
    if (!web.EffectiveBasePermissions.Has(PermissionKind.AddAndCustomizePages))
    {
        return true;
    }

    // It's a site without noscript enabled
    return false;
}
```

## <a name="additional-considerations"></a>Zusätzliche Überlegungen

Wir werden schrittweise weitere Anpassungsoptionen für "modernen" Teamwebsites einzuführen, die mit der Veröffentlichung von SharePoint-Framework Zusatzfunktionen ausgerichtet wird. Derzeit ist kein genauen Zeitplan verfügbar, aber wir werden in den Artikeln "modernen" Erfahrung aktualisieren, sobald neue Funktionen freigegeben werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online](modern-experience-customizations.md)
- [Plug & Play-Remote-Bereitstellung](https://msdn.microsoft.com/en-us/pnp_articles/pnp-remote-provisioning)

