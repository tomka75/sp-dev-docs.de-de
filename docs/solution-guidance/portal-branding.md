---
title: "Bewährte Methoden für SharePoint Online Webportal branding"
ms.date: 11/03/2017
ms.openlocfilehash: 9d56f027541f69f12c1d487f2a97b1dd47c61373
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="proven-practices-for-sharepoint-online-portal-branding"></a>Bewährte Methoden für SharePoint Online Webportal branding

Die Fähigkeit zum Anwenden einer benutzerdefinierten Marke in einem Portal spielt eine wichtige und dieser Artikel bietet Ihnen einen Überblick über die Optionen branding und branding bewährte Methoden.

> [!NOTE] 
> Obwohl dieser Anleitung SharePoint Online Zielgruppenadressierung ist die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet wird.


_**Gilt für:** SharePoint Online_

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a>Anti-Muster (also nicht sollten Sie folgende Aktionen)
<a name="sectionSectionAntiPatterns"></a> Unterhalb der Liste enthält die wichtigsten Punkte **nicht** zu tun, wenn es darum geht, Ihr Portal branding:
- Überschreiben von Office 365-Suite Leiste branding
- Anpassen des Brandings für persönliche Websites
- Standardmäßig implementieren Sie für Ihr benutzerdefiniertes branding mithilfe von benutzerdefinierten Gestaltungsvorlagen

## <a name="overview"></a>Übersicht
<a name="sectionSection0"></a> Organisationen in der Regel das Portal sein sollte eindeutig und noch etwas suchen möchten. Benutzerdefiniertes branding können Sie um die unternehmenseigenen und Werte zu fördern und deshalb benutzerdefinierten Brandinglösung ist entscheidend für (Enterprise) Portale. Hier sind die typischen branding Anforderungen, die wir von Kunden,, beim Erstellen von benutzerdefinierten Portalen in SharePoint hören:
- Anpassen der Darstellung:
  - Benutzerdefiniertes Farbschema implementieren
  - Benutzerdefiniertes Logo anzeigen
  - Anpassen der Darstellung der Anmeldeseite
  - Ändern der Darstellung von Navigationssteuerelementen
- Anpassen des Layouts:
  - Ändern Sie allgemeine Layout der Informationen auf Seiten
  - Stellen Sie Portal "schnell"
  - Anzeigen von benutzerdefinierten Fußzeile
- Weitere Funktionen hinzufügen:
  - Anpassen des Verhaltens der Portalnavigation
  - Hinzufügen von benutzerdefinierten Steuerelementen (Webparts) auf Seiten

In den folgenden Abschnitten besprechen wir, wie diese Anforderungen zu behandeln.

## <a name="general-principles"></a>Allgemeine Grundsätze
<a name="sectionSection1"></a> Die folgenden allgemeinen Richtlinien sollten beim branding Portalen in einer SharePoint Online-Umgebung beachtet werden:
1. Im SharePoint Online-Dienst ist ständig verbessern. Mit dem Dienst bereitgestellten Updates beeinträchtigen DOM-Struktur, von der im Feld Seiten und den Inhalt von der Feld-Dateien (z. B. Gestaltungsvorlagen). Entwickler müssen beachten Sie dies und darf nicht als nicht unterstützte anpassungsansätze (beispielsweise Position von bestimmten Element in DOM-Struktur der Seite) abhängig.
2. Vermeiden Sie das Anpassen von Gestaltungsvorlagen. Wie bereits erwähnt, kann Updates auf den Dienst, die Struktur der Nutzung der Masterseiten Feld auswirken. Wenn Sie eine benutzerdefinierte Gestaltungsvorlage Kopieren des Inhalts der außerhalb der Gestaltungsvorlage Feld implementiert haben, müssen Sie weiter überwachen, wenn dies der Gestaltungsvorlage Feld in der nicht aktualisiert wird, und diese Änderungen in Ihre benutzerdefinierte Gestaltungsvorlage erneut zu implementieren. Andernfalls kann einige Funktionen von SharePoint starten falsch, verhält, wenn Ihre benutzerdefinierte Gestaltungsvorlage verwendet wird. Aus diesem Grund Anpassen von Gestaltungsvorlagen führt zu zusätzlichen Risiken und Wartungskosten wird, und es wird empfohlen, dies möglichst vermeiden.
3. Individuelles branding persönlicher Websites (OneDrive for Business-Websites) wird **nicht** unterstützt. Es ist zulässig, benutzerdefinierte Farbschemas über Office 365-Mandanten Ebene branding-Einstellungen ([Anpassen der Office 365-Design für Ihre Organisation](https://support.office.com/en-us/article/Customize-the-Office-365-theme-for-your-organization-8275da91-7a48-4591-94ab-3123a3f79530)) anwenden
4. SharePoint Online-Portale müssen als Teil der gesamten Office 365-Ökosystem berücksichtigt werden. Deshalb jedes Portal verfügt nun über Office 365-Suite-Leiste und anpassen, es ist **nicht** unterstützte (Siehe den Abschnitt **Office 365-Suite Leiste** unten).
5. Bei der Planung von branding und die Struktur der Navigationskomponente ist es wichtig, denen Sie im [Portal Navigation Artikel](portal-navigation.md)beschriebenen Empfehlungen folgen.
6. Beim Erweitern Portal Funktionalität über benutzerdefinierte Steuerelemente (Webparts) ist es wichtig, um Empfehlungen von [Portal Leistung Artikel](portal-performance.md)folgen.
7. Es gibt wesentliche Unterschiede zwischen branding Ansätze für die "klassische" Vs "modernen" Websites und Seiten unterstützt. Ausführliche Informationen zu "modernen" Websites und Seiten, finden Sie unter: [Anpassen von "modernen" Teamwebsites](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-customize-sites) und [Anpassen von "modernen" Websiteseiten](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-customize-pages).

## <a name="customize-the-look"></a>Anpassen des Erscheinungsbilds
<a name="sectionSection2"></a> Mehrere Out der Feld Methoden zum Anpassen der Darstellung der SharePoint-Portale vorhanden sind. Erstens können Administratoren das Office 365-Design für eine gesamte Mandanten anpassen. Im nächsten Schritt kann ein benutzerdefiniertes Design auf bestimmte Website angewendet werden. Diesen Techniken können in "get" die benötigten Farben / zulassen für flexible über verschiedene Portalwebsites Farben verwendet werden. Wenn mehr Flexibilität benötigt wird, wird empfohlen, dass Kunden aus der Gestaltungsvorlage Feld (seattle.master) starten und eines benutzerdefiniertes Designs anwenden und/oder verwenden Sie die benutzerdefinierten CSS-Einstellungen (``Web.AlternateCSSUrl``) zu den erforderlichen CSS-Code Einbindung Dateien. Benutzerdefiniertes Logobilds kann festgelegt werden, mit der ``Web.SiteLogoUrl`` Eigenschaft. Diese Verfahren werden in den folgenden Artikeln und Plug & Play-Beispiele veranschaulicht:
- [Anpassen des Office 365-Designs für Ihre Organisation](https://support.office.com/en-us/article/Customize-the-Office-365-theme-for-your-organization-8275da91-7a48-4591-94ab-3123a3f79530)
- [Design Management mit CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DeployCustomThemeWeb)
- [Anwenden von branding](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
- [AlternateCSSUrl & SiteLogoUrl Eigenschaften im Web-Objekt](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
- [Nicht genügend Steuerelemente für die Navigation im Feld Branding](http://blog.sharepointexperience.com/2016/10/branding-structured-managed-navigation-sharepoint/)

Es gibt verschiedene Empfehlungen, die bei der Entwicklung von benutzerdefinierter CSS-Dateien für SharePoint befolgt werden sollten:
1. Beschränken Sie die aus dem Feld CSS-Klassen überschreiben
2. Verwendung der ``Web.AlternateCssUrl`` -Eigenschaft auf eine benutzerdefinierte CSS-Dateien enthalten
3. Setzen Sie nicht außer Kraft die Office 365-Suite Leiste branding wie, die in mangelnde Vernetzung führt, wenn das Portal Benutzer verlassen


### <a name="office-365-sign-in-page"></a>Office 365-Anmeldeseite
Kunden können Unternehmen branding zu Office 365-Anmeldeseite anwenden. Wird beschrieben, wie im folgenden Artikel: [Hinzufügen von Ihrem Unternehmen zu Office 365 anmelden Seite branding](https://support.office.com/en-us/article/Add-your-company-branding-to-Office-365-Sign-In-Page-a1229cdb-ce19-4da5-90c7-2b9b146aef0a).

### <a name="office-365-suite-bar"></a>Office 365-Suite-Leiste
Anweisungen gelten für die Leiste Suite aus der Sicht von Microsoft lautet wie folgt:
- Die Leiste Suite ist eine auf Mandantenebene-Navigationskomponente, die Benutzern für die einfache Verschiebung zwischen allen Office 365-Dienste in eine einfache und konsistente Weise ermöglicht
- Die Portal-Anwendung nicht "Besitzer" der Suite-Leiste noch sollte es davon dazu aus
- Behandeln Sie der Suite-Leiste wie die Browser-Symbolleiste insofern, dass es nicht Bestandteil der Anwendung
- Sie können Ändern/der Suite-Leiste, aber nur auf der Ebene Mandanten und nur über die O365-Admin-Seiten konfigurieren
- Verwenden Sie Code nicht ändern (verschieben, ausblenden usw.) der Suite-Leiste innerhalb der Anwendung
- Sie sollten nicht Aspekte des Balkens Suite (z. B. das Startprogramm für App-Symbol) in Ihrer Anwendung erneut verwenden
- Wenn Sie sich entschließen, werden "intelligente", Sie in den meisten Fällen werden ausgeführt unerwartete Probleme in Zukunft

## <a name="adjust-the-layout"></a>Anpassen des Layouts
<a name="sectionSection3"></a> Bei der Kommunikation über das Anpassen des Layouts von SharePoint-Portale, in der Regel die erste Option, die von Entwicklern berücksichtigt wird ist die Erstellung einer benutzerdefinierten Gestaltungsvorlage. Zwar weiterhin benutzerdefinierte Gestaltungsvorlagen unterstützt, diese Vorgehensweise wird nicht empfohlen, aufgrund von den oben genannten Gründen - benutzerdefinierte Gestaltungsvorlagen führen zu weiteren Risiken und Wartungskosten in langfristige. Deshalb Entwickler sollten alternative Ansätze, mit denen das Layout von SharePoint-Portale anpassen können. Dazu zählen folgende:
- Implementieren von benutzerdefinierten CSS
- Verwenden von benutzerdefinierten Seitenlayouts
- Implementieren allgemeine Brandingelemente (wie "Fußzeile") durch Einfügen von Client-Skripts (diese Vorgehensweise wird im nächsten Abschnitt erläutert.)

Kombinieren von diesen Methoden können Sie das gewünschte SharePoint Portal Layout ohne Entwickeln von benutzerdefinierten Masterpages zu erreichen. Die folgenden Plug & Play-Beispiele und Lösungen, führen Sie vor, wie dies erzielt werden kann:
- [SharePoint 2013/2016/Online schnell Benutzeroberfläche](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.UI.Responsive)
- [Sofort einsatzbereit Seattle Master durchführen schnell](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.InjectResponsiveCSS)
- [Beispiel für benutzerdefinierte Kopf- und Fußzeilen](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript.HeaderFooter)

## <a name="add-functionality"></a>Hinzufügen von Funktionalität
<a name="sectionSection4"></a> Einbetten von Client-Skripts in den Seiten die Darstellung und Funktionalität des Portals weiter anpassen können. Beispielsweise kann diese Vorgehensweise zum Anpassen von Navigationssteuerelementen, können Sie benutzerdefinierte Kopf- und Fußzeilen auf allen Seiten des Portals hinzufügen oder andere benutzerdefinierte UI-Blöcke implementieren verwendet werden.

Die folgenden Vorgehensweisen können JavaScript einbetten verwendet werden:
1. Hinzufügen einer benutzerdefinierten Aktion auf Website oder Websitesammlungsebene. Dies kann die Ausführung eines Teils der JavaScript auf allen Seiten in der Website oder Websitesammlung ausgelöst werden.
2. JavaScript-Datei Inhalts-Editor oder Skript-Editor-Webpart auf einer Seite mit tatsächlichen JavaScript-Code oder einen Link hinzufügen. Dies kann die Ausführung von JavaScript-Code auf einer bestimmten Seite ausgelöst werden.
3. JavaScript-Code oder einen Link zur JavaScript-Datei in Inhalt des Layouts Seitendatei einschließen. Dies kann Ausführung von JavaScript in allen Veröffentlichungsseiten ausgelöst werden, die diese Seitenlayouts-Datei verwenden.

Darauf hinzuweisen, dass benutzerdefinierte Aktion Ansatz funktioniert "klassische" Websites nur, einschließlich der aktuellen veröffentlichungsportale.

Die folgenden Plug & Play-Beispielen wird veranschaulicht, wie das Einbetten von JavaScript erzielt werden kann:
- [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [Core.EmbedJavaScriptJSOM](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScriptJSOM)
- [Anpassung über JavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)

Es ist wichtig, um hervorzuheben, dass beim Erweitern Portal Funktionalität mithilfe von JavaScript im [Portal Leistung Artikel](portal-performance.md)beschriebenen Empfehlungen folgen entscheidend ist.

## <a name="provisioning-branding-assets"></a>Bereitstellung der Branding-Objekte
<a name="sectionSection5"></a> Der letzte Schritt bei der Implementierung Brandinglösung ist die Bereitstellung von Anlagen von branding. Dazu gehören in der Regel Bilder, CSS- und JavaScript-Dateien. Es gibt verschiedene Ansätze, wie diese Dateien bereitgestellt werden können:
1. Veröffentlichen von Dateien auf Bibliotheken auf einzelne Websitesammlungen. In diesem Fall können jede Websitesammlung eine eigene Version der branding-Objekte. Zugriff auf Dateien ist mit der standardmäßigen SharePoint-Sicherheitsmechanismen gesteuert. Jedoch erfordert Aktualisieren von Dateien diese in jeder Websitesammlung erneut hochladen.
2. Veröffentlichen von Dateien in Bibliothek in einer Websitesammlung (Unternehmenszentrale). In diesem Szenario können alle Websitesammlungen die einzelne neueste Version von branding-Objekte. Aktualisierte Dateien müssen auf nur einem Speicherort hochgeladen werden. Administratoren müssen sicherstellen, dass Benutzer aller Websitesammlungen Zugriff auf die Dateien im zentralen Speicherort veröffentlicht haben.
3. Veröffentlichen von Dateien zu CDN (Web Application, Azure CDN oder Office 365 CDN). In diesem Fall können alle Websitesammlungen die einzelne neueste Version von branding-Objekte. Aktualisierte Dateien müssen auf nur einem Speicherort hochgeladen werden. Verwenden des CDN kann die Leistung verbessert, jedoch außerhalb von SharePoint der Inhalt gespeichert wird und deshalb Objekte können nicht mithilfe von standardmäßigen SharePoint-Sicherheitsmechanismen, mit Ausnahme der Office 365 der privaten CDN-Funktion die Dateien auf sichern können geschützt werden ein CDN.

[Plug & Play-Bereitstellung Engine](https://dev.office.com/blogs/introduction-to-office-365-dev-pnp-provisioning-engine) kann zum Bereitstellen von Anlagen von branding in SharePoint-Bibliotheken verwendet werden. Bei Verwendung die Office 365 CDN-Funktion werden die Dateien automatisch in dem CDN provisioning bei Verwendung alternative CDN-Lösungen, die ein benutzerdefinierter Bereitstellung Ansatz zum Veröffentlichen von Dateien zu des CDN erforderlich ist.

Weitere Informationen zu den CDN finden Sie unter:
- [Office 365 öffentliches/privates CDN-Funktion](https://dev.office.com/blogs/general-availability-of-office-365-cdn)
- [Verwenden die Inhaltsübermittlung mit SharePoint Online](https://support.office.com/en-gb/article/Using-content-delivery-networks-with-SharePoint-Online-9a64268c-0b74-4eaa-b971-fb6380b1b165)
- [CDN-Manager](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.CDNManager)

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Branding von SharePoint-Websites in der SharePoint-add-in-Objektmodell](branding-sharepoint-sites-sharepoint-add-in.md)
- [Branding von SharePoint Online](https://sharepointgurus.net/branding-sharepoint-online/)
- [92 % der SharePoint-Branding ist CSS, also Warum sind Sie leben in einer Gestaltungsvorlage?](http://blog.sharepointexperience.com/2016/12/sptechcon-sf-2016-branding-with-css-session-recap/)
- [Überprüfen der Valo: Ready für unterwegs-Intranet in Office 365 und SharePoint](https://absolute-sharepoint.com/2017/01/review-of-valo-ready-to-go-intranet-on-office-365-and-sharepoint.html)
