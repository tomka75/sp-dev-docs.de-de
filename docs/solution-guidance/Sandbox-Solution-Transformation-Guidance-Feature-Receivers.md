---
title: "Sandkasten-Transformation ausgesprochen - Featureempfänger"
ms.date: 11/03/2017
ms.openlocfilehash: 4072e7d7b920bcb2347d40d1f1ff25cd2935b3c4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---feature-receivers"></a>Sandkasten-Transformation ausgesprochen - Featureempfänger 
Transformieren oder Konvertieren von codebasierte sandkastenlösungen in der SharePoint-add-in-Objektmodell. Hier erfahren Sie, über die Optionen und Strategien für die vorhandenen Funktionalität in SharePoint-add-in-Modell oder alternative Lösungen zu konvertieren.

_**Gilt für:** Add-ins für SharePoint | SharePoint 2013 | SharePoint-2016 | SharePoint Online_


## <a name="summary"></a>Summary
Featureempfänger werden in der Regel verwendet, andere Art Konfigurationen oder Einstellungen auf SharePoint-Websites anwenden, wenn Feature aktiviert wird oder Site (wenn Feature zugeordnet, um die Vorlage Website / Webvorlagen) erstellt wird. Featureempfänger bereitgestellt von sandkastenlösungen in SharePoint Online, aber seit codebasierte Anpassungen keine Logner können nicht verwendet werden, alternative Entwurf muss ausgeführt werden soll. 

Ansatz verwenden Sie zum Verarbeiten von featureempfängern in SharePoint unterscheidet sich etwas in der SharePoint-add-in-Objektmodell mit vollständigen vertrauen Code oder in der codierten sandkastenlösungen war. Sie müssen die Lösung in Abwesend überarbeiten Sie, dass Sie remote-APIs (CSOM/REST) die erforderlichen Konfigurationen auf Ihren Websites anwenden, das zuvor in der Funktion Receiver(s) verwenden. 


## <a name="options-for-replacing-feature-receivers"></a>Optionen für den Austausch von Featureempfängern
<a name="sectionSection2"> </a>

|**Ansatz**|**Weitere Informationen**|
|:-----|:-----|
|PowerShell-basierte Anpassungen|<p>Sie PowerShell-Skripts verwenden, um neue Websitesammlungen bereitstellen (und potenziell sub-Websites), in denen erforderliche Anpassungen mithilfe von remote-APIs angewendet werden. In der Regel mithilfe von CSOM/REST direkt in die PowerShell-Skripts oder mithilfe von Plug & Play-PowerShell-Befehle, erfolgt dies dem bietet einfache Möglichkeit, Websites und Inhalte Remote zu ändern.</p><p><lu><li>[Plug & Play-Modul für die Bereitstellung](https://github.com/SharePoint/PnP-PowerShell)</li><li>[Plug & Play-PowerShell – erste Schritte mit den neuesten updates](http://dev.office.com/blogs/pnp-powershell-getting-started-with-latest-updates)</li></lu></p>|
|Code basierend Anpassungen|<p>Sie können die erforderlichen Anpassungen auch mithilfe von verwaltetem Code mit remote-APIs anwenden. Dies bedeutet, dass Sie entweder sie als Teil der administrativen Vorgang beim Anwenden von Anpassungen auf SharePoint, die eingebunden wird im Code die Elemente der Benutzeroberfläche angewendet werden, wie durch die Sub Site Creation Logik Overiding angehören, oder die Website beim , sodass Anpassungen als Teil der Bereitstellung Logik zugeordnet werden kann.</p><p><lu><li>[Remote provisioning Muster für Sub Site creation](https://channel9.msdn.com/blogs/OfficeDevPnP/Using-remote-provisioning-pattern-for-sub-site-creation)</li><li>[Hauptkomponente Plug & Play-CSOM](https://github.com/SharePoint/PnP-sites-core)</li></lu></p>|

## <a name="design-considerations"></a>Entwurfsaspekte
### <a name="powershell-based-provisioning"></a>PowerShell basierte Bereitstellung
Dieses Modell funktioniert hervorragend, wenn Ihre Bereitstellung Modell Website administrativen Aktionen basiert.
- Skript ausgeführt werden erfordert die erforderliche Anpassungen für erstellte Websites verwendet wird
- Kann zum websiteerstellungsprozesses, kombiniert werden, wenn vom als administrative Vorgang ausgeführt
- Erfordert keinen Hostinginfrastruktur ab
- Keine Möglichkeit, die automatisch als Teil des Erstellungsprozesses Sub Website kombinieren

### <a name="code-based-provisioning"></a>Codebasierten Bereitstellung
- Kann sperrt Hostinginfrastruktur ab, wenn mit der End-Benutzeroperationen kombiniert
- Sie können verwalteten Code verwenden, die an einer beliebigen Stelle mit CSOM/REST-APIs für die erforderlichen Vorgänge ausgeführt wird
- Kann verwendet werden, um auf SharePoint integrieren, indem Sub Site Creation Link überschreiben
- Sie können Websitesammlung automatisieren und Unterwebsite bereitstellen mithilfe von remote-APIs

> Wenn schafft automatische Möglichkeit zum Anwenden Remotecode als Teil der Sub Site Creation Logik benötigt werden soll, müssen Sie die Sub-Standortlinks mit benutzerdefinierten Benutzeraktionen außer Kraft setzen. Diese Option ist nur entwerteten in Websites, die im klassischen Modus um Bibliotheken und Listen verwenden. 


## <a name="reference-approaches"></a>Verweis Ansätze
### <a name="applying-needed-customizations-to-sites-using-powershell"></a>Anwenden von Anpassungen von Websites mithilfe von PowerShell erforderlich
Hier ist ein einfaches Skript, das Plug & Play-PowerShell verwendet eine Designfarbe hochzuladenden Datei vom Computer mit SharePoint Online und aktiviert, die in der SharePoint-Website. 

> In diesem Beispiel wird [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell)verwendet, das mehr als 150 zielorientierten zusätzlichen PowerShell-Cmdlets für die Standortkonfiguration und Asset Management bereitstellt. 

```postscript 

Connect-SPOnline –Url https://yoursite.sharepoint.com/ –Credentials (Get-Credential)
Add-SPOFile -Path c:\temp\company.spcolor -Folder /_catalogs/theme/15/
Set-SPOTheme -ColorPaletteUrl /_catalogs/theme/15/company.spcolor

```

### <a name="applying-needed-customizations-to-sites-using-code"></a>Anwenden von Anpassungen von Websites mithilfe von Code erforderlich
Hier ist eine einfache Code die SharePoint Online-CSOM zum benutzerdefinierten Designs zu aktivieren, indem Sie zuerst die Anlagen auf SharePoint-Website hochladen und das anschließende Aktivieren benutzerdefiniertes Design verwendet. 

> In diesem Beispiel wird [Plug & Play-CSOM Hauptkomponente](https://github.com/SharePoint/PnP-sites-core), mithilfe der systemeigenen aus dem Feld Vorgängen durch die Einführung von zusätzlichen Satz von Erweiterungsmethoden für allgemeine Vorgänge erweitert. Sie können ähnliche Vorgänge auch mithilfe von systemeigenen CSOM ausführen, aber Code wäre wesentlich komplexer.

```csharp

// Upload assets to theme folder
clientContext.Site.RootWeb.UploadThemeFile(
        HostingEnvironment.MapPath(string.Format("~/{0}", "Resources/Themes/SPC/SPCTheme.spcolor")));
clientContext.Site.RootWeb.UploadThemeFile(
        HostingEnvironment.MapPath(string.Format("~/{0}", "Resources/Themes/SPC/SPCbg.jpg")));

Web web = clientContext.Web;
// loading RootWeb.ServerRelativeUrl property;
clientContext.Load(clientContext.Site, w => w.RootWeb.ServerRelativeUrl); 
clientContext.ExecuteQuery();
// Let's first upload the contoso theme to host web, if it does not exist there
web.CreateComposedLookByUrl("Contoso",
                clientContext.Site.RootWeb.ServerRelativeUrl + "/_catalogs/theme/15/SPCTheme.spcolor",
                null,
                clientContext.Site.RootWeb.ServerRelativeUrl + "/_catalogs/theme/15/SPCbg.jpg",
                string.Empty);

// Setting the Contoos theme to host web
web.SetComposedLookByUrl("Green");

```

Wenn Sie Code basierend Ansätze verwenden, empfehlen wir [Plug & Play-Provisioning-Modul](http://dev.office.com/blogs/sharepoint-pnp-remote-provisioning-engine-august-2016) für die vorlagenverwaltung, die der Entwicklungsaufwand erheblich vereinfachen wird. 

## <a name="removing-sandbox-solution-containing-feature-receiver-code-from-your-site"></a>Sandkasten-Lösung, die mit Feature Receiver Code von Ihrer Website entfernen
<a name="sectionSection3"></a> Wenn die Sandkasten-Lösung Feature Ereignisempfänger Logik für die Deaktivierung des Features enthält, und es wichtig ist, dass diese ausgeführt werden bevor codebasierte Unterstützung vollständig entfernt wird, sollten Sie sicherstellen, dass diese Art von Features werden vor deaktiviert aus SharePoint Online ist die Unterstützung codebasierte deaktiviert. Sie können sandkastenlösungen aus SharePoint Online deinstallieren, nachdem die Unterstützung codebasierte ist deaktiviert, aber Feature Receiver Code würde nicht ausgeführt werden, obwohl die Features von der Website verschoben werden. 

Wenn Sie Ihre vorhandenen Sandkasten-Lösung aus Ihrer Websites, die alle Elemente oder Dateien bereitgestellt, mit deklarativer Optionen werden jedoch nicht entfernt deaktivieren wird automatisch das Feature deaktiviert werden. Ausführung des Codes in den Featureempfänger ist abhängig von der Zeitpunkt, wenn die Lösung Sandkasten deaktiviert wird. 


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>
-  [Entfernen codebasierte Sandkastenlösungen in SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Hilfestellung zur Transformation von Sandkastenlösungen](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/blob/master/README.md) - Skript wie Anpassungen
-  [Schulung Plug & Play-CSOM-Kern](https://blogs.msdn.microsoft.com/vesku/2016/04/12/office-dev-pnp-core-componenttraining-package/) - basierte für Code Optionen
