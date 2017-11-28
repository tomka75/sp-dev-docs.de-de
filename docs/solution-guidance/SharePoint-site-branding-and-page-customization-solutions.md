---
title: "SharePoint-Website branding und Seite Anpassung Lösungen"
ms.date: 11/03/2017
ms.openlocfilehash: 6d522af8f85a750656ef53b00785591bac4f93b4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sharepoint-site-branding-and-page-customization-solutions"></a>SharePoint-Website branding und Seite Anpassung Lösungen

Verwenden Sie das SharePoint-Seitenmodell und zusammengesetzten, SharePoint 2013 Designmodul und CSS zu Ihrer SharePoint-Website und Seiten mit Branding versehen.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können das Aussehen und Verhalten der SharePoint-Website auf zwei Arten anpassen:

- Mithilfe von Designmodul zum Erstellen benutzerdefinierter Designs (zusammengesetzten in SharePoint 2013 und SharePoint Online). Definieren von mindestens Designs Farben. Ein vollständiges Design definiert Farben, Schriftarten, eines Hintergrundbilds und der zugeordneten Masterseite und eine .preview-Datei, die definiert, wie die master-Seite eine Vorschau angezeigt wird. Das remote provisioning Muster können Sie Designs auf Websites angewendet.

- Erstellen Sie benutzerdefinierte cascading Stylesheets (CSS) auf SharePoint Online-Websites anwenden. Eine app für SharePoint und das remote provisioning Muster können zum Bereitstellen von SharePoint-Websites, um benutzerdefinierte CSS verwenden.

Brandingänderungen können einfach und kostengünstig, jedoch auch komplex und teuer sein. Benutzer können die Benutzeroberfläche zusammengesetzten, die ein Hintergrundbild, Farbpalette, Schriftarten, eine Gestaltungsvorlage und einer Datei zugeordneten .preview für die Gestaltungsvorlage enthalten, angewendet. Können Sie SharePoint 2013 Designmodul zusammengesetzten entwerfen und Bereitstellen von Websites, und Sie können benutzerdefinierte CSS, um das Aussehen und Verhalten der Website und seine Elemente ändern erstellen.

**Wichtige**  Obwohl es möglich, zum Erstellen von benutzerdefinierten Gestaltungsvorlagen und andere strukturellen Elemente als Teil eines benutzerdefinierten branding-Projekts ist, ist die langfristige Kosten Unterstützung für benutzerdefinierte Masterseiten und andere benutzerdefinierte Elemente strukturelle hoch. Benutzerdefiniertes branding kann machen es kostspieliger für Ihre Organisation zum Anwenden von Upgrades und die laufende Unterstützung bieten.

In diesem Abschnitt basiert auf Ihr Wissen über [SharePoint-Entwicklung und Designtools und Methoden](SharePoint-development-and-design-tools-and-practices.md), um zu zeigen, wie Sie das Aussehen und Verhalten der SharePoint-Website anpassen.

## <a name="key-terms-and-concepts-related-to-sharepoint-branding"></a>Wichtige Begriffe und Konzepte im Zusammenhang mit der SharePoint-branding
<a name="sectionSection0"> </a>

|**Begriff oder Konzept**|**Definition**|**Weitere Informationen**|
|:-----|:-----|:-----|
|Alternative CSS|Eine CSS-Datei als die Standardstärke, die Sie auf das Aussehen und Verhalten der Website anwenden können.|Verwenden Sie alternative CSS benutzerdefinierte CSS auf einer Website und aller Unterwebsites anwenden. |
|CSS|Eine Sprache, die einem Browser wie ein HTML- oder XML-Dokument Formatvorlagen gerendert wird. CSS trennt Dokumentinhalt (HTML oder XML) aus, wie die Inhalte präsentiert werden.||
|Zusammengesetztes Design|Eine Kombination von Schriftarten, eine Farbpalette, ein Hintergrundbild und eine Masterseite zugeordnet ist, die auf der Website angewendet werden. Schriftart Schema und Farbe Bilder sind optional. Im folgenden finden Sie den standardmäßigen Dateispeicherort für zusammengesetzten: Design Gallery\15 Ordner|<p>Zusammengesetzten sind eine bequeme Möglichkeit, das Aussehen und Verhalten von Websites zu ändern, ohne Änderungen vorzunehmen, um die Struktur einer Website.</p><p>SharePoint 2013 wird standardmäßig mehrere zusammengesetzten geliefert. Wenn ein Benutzer ein zusammengesetztes Design angewendet wird, gilt SharePoint die zugeordneten Designelemente der zusammengesetztes Design auf eine Website.</p>|
|Inhaltssuche-Webpart (CSWP)|Inhalte aus den Suchergebnissen auf der Grundlage einer angegebenen Abfrage rendert.| <p>[Inhaltssuche-Webpart in SharePoint 2013](http://social.technet.microsoft.com/wiki/contents/articles/15843.content-search-web-part-in-sharepoint-2013.aspx) (TechNet) </p><p>[Inhaltssuche-Webpart in SharePoint 2013](http://msdn.microsoft.com/library/6fb4bf41-0846-4dca-ad9e-906afdfd3d2b.aspx) (MSDN)</p>|
|corev15.CSS|Die CSS-Datei, die meisten wichtigsten Funktionen für SharePoint enthält. Es folgt der Datei Speicherort: _layouts\15 Standardordner||
|CSSRegistration|Ein Verweis in eine Gestaltungsvorlage, wie etwa seattle.master, das meisten CSS geladen wird, die für die meisten der Standardbenutzeroberfläche angewendet wird.|Verwenden Sie das **CSSRegistration** -Steuerelement in einer Gestaltungsvorlage standardmäßig CSS außer Kraft gesetzt.|
|Benutzerdefinierte Aktion|Aktionen können Sie anpassen und interagieren mit Listen und auf dem Menüband auf der Hostwebsite.| [Vorgehensweise: Erstellen benutzerdefinierter Aktionen zum Bereitstellen von mit SharePoint-Add-ins](http://msdn.microsoft.com/library/bbd11f94-1798-453e-bbb0-e5eb0df8dc75.aspx)|
|Gerätekanäle|Rendern einer einzelnen SharePoint-Veröffentlichungswebsite in mehrere Möglichkeiten mit eindeutigen Kanäle Ziel Rendering des Inhalts auf bestimmten Geräten.| [SharePoint 2013 Design Manager Gerätekanäle](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951.aspx)|
|Anzeigevorlagen|Such-Webparts zum Anzeigen der Ergebnisse einer Abfrage, die mit dem Suchindex verwendeten Vorlagen.| [SharePoint 2013 Design Manager Anzeigevorlagen](http://msdn.microsoft.com/library/1a782bac-48ee-4baf-8751-0f943a306e0f.aspx)|
|Wiedergabe eines beschnittenen Bildes|Zeigen Sie Größe Versionen eines Bildes auf einer Veröffentlichungswebsite basierend auf der gleichen Quelle ein Bild an.| [SharePoint 2013 Design Manager bilddarstellungen](http://msdn.microsoft.com/library/d08a74c0-5674-4f26-8646-11ea1f081c85.aspx)|
|Verwaltete Metadaten| Funktionen in SharePoint, die zum Definieren von Ausdrücken ermöglichen, Ausdruckssatz, Gruppen und Etiketten für Ausdrücke. Manchmal bezeichnet als Taxonomie. In SharePoint 2013 ist das System für verwaltete Metadaten die Grundlage für die verwaltete Navigation.| [Verwaltete Metadaten und Navigation in SharePoint 2013](http://msdn.microsoft.com/library/b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e.aspx)|
|Verwaltete Navigation|Navigation für Veröffentlichungswebsites, die erstellt wird basierend auf verwaltete Metadaten. Navigation wird aus einem angegebenen Ausdruckssatz im Terminologiespeicher erstellt. | [Verwaltete Navigation in SharePoint 2013](http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02.aspx)|
|Gestaltungsvorlage|Eine Seite, die das Verhalten und die Darstellung der im linken Navigationsbereich und oberen Navigationsbereich einer SharePoint-Seite standardisiert.| [Master Pages, the Master Page Gallery und Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)|
|Gestaltungsvorlagenkatalog|Eine spezielle Dokumentbibliothek in SharePoint 2013, in dem alle branding-Elemente-Masterseiten, Seitenlayouts, JavaScript-Dateien, CSS und Bilder sind standardmäßig gespeichert. Jede Website besitzt eine eigene Master Seite Gallery.When Sie benutzerdefinierte erstellen Brandingelemente, es wird empfohlen, dass Sie benutzerdefinierte Objekte in der Standardeinstellung Master Page Gallery-Dateistruktur speichern.| [Master Pages, the Master Page Gallery und Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)|
|Oslo.Master|Eine Gestaltungsvorlage in SharePoint 2013.|Verschiebt die aktuelle Navigation in derselben Position wie der Bereich der oberen Navigationsleiste. |
|Seite Inhaltssteuerelement|Ein Steuerelement auf einer Veröffentlichungswebsite, die ein Webpart hinzugefügt werden kann.||
|Seitenlayout|Eine Vorlage für eine SharePoint-Veröffentlichung Websiteseite, die Benutzer kann das Informationen auf der Seite einheitlich Layout.||
|Schnellstart|Verwaltet die Navigationselemente auf der linken Seite der Seite einer Website für die Zusammenarbeit.|Sie können Navigationselemente Gruppe Überschrift Links hinzufügen.|
|REST|Eine statusfreie architektonische Formatvorlage, die Architekturelemente abstrahiert und HTTP-Verben zum Lesen und Schreiben von Daten von Webseiten, die XML-Dateien enthalten verwendet.| [Erste Schritte mit dem SharePoint 2013 REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590.aspx)|
|Stammwebsite|Die erste Webseite in einer Websitesammlung.|Das Stammweb wird manchmal auch als the Web Application Root bezeichnet. |
|Seattle.Master|Die Standardseite des Master für SharePoint 2013 Teamwebsites und Veröffentlichung von Websites.||
|Layout der Website|Finden Sie unter Gestaltungsvorlage.|Das Layout der Website kombiniert die master-Seite eines Designs mit der entsprechenden .preview-Datei.|
|Strukturierte navigation|Eine Navigationsstruktur für die Veröffentlichung von Websites, die die Websitehierarchie von der Veröffentlichungswebsite basiert. Sie können die Kopf- und Links zu manuell ersetzen oder Anpassen der strukturierte Navigation, die automatisch SharePoint generiert hinzufügen.| [Vorgehensweise: Anpassen der Navigation in SharePoint Server 2010 (ECM)](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx)|
|Design|Eine einfache Möglichkeit, hell branding bis hin zu einer SharePoint-Website anwenden. Der Standardspeicherort für die Datei für Designs ist der Ordner _themes der Website.|<p>Designs sind eine einfache Möglichkeit zum Anwenden von benutzerdefiniertem branding auf SharePoint-Websites.</p><p>[Designs (Übersicht) für SharePoint 2013](http://msdn.microsoft.com/library/ae585dd3-82fe-46bb-ac93-065edc0a16f4.aspx)</p><p> [Vorgehensweise: Bereitstellen eines benutzerdefiniertes Designs in SharePoint 2013](http://msdn.microsoft.com/library/f703df24-8e56-4e6a-bc37-95acbb3c83e8.aspx)</p>|
|Designmodul|Eine Reihe von Dateien und Funktionen, die das Aussehen, Verhalten, Verhalten und Zuordnungen der Datei definieren durchkomponierten Looks.||
|Zeichenfolge des Benutzer-Agent|Informationen, die ein Browser zu einer Website übergibt, die die Software identifiziert, die vom Server die Anforderung stellt.| [SharePoint 2013 Design Manager Gerätekanäle](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951.aspx)|
|Benutzerdefinierte Aktion des Benutzers|Eine CSOM-Eigenschaft, die die Auflistung von benutzerdefinierten Aktionen für eine Website, Liste oder Websitesammlung zurückgibt. Der Standardspeicherort ist Folgendes: 15\TEMPLATE\FEATURES<p>Beispiel:</p><p>&lt;HideCustomAction GroupId = "Kataloge"<br />&nbsp;&nbsp;&nbsp;HideActionId = "Designs"<br />&nbsp;&nbsp;&nbsp;Location="Microsoft.SharePoint.SiteSettings"&gt;</p>|<p>[UserCustomAction-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx)</p><p>[Vorgehensweise: Erstellen benutzerdefinierter Aktionen zum Bereitstellen von mit SharePoint-Add-ins](http://msdn.microsoft.com/library/bbd11f94-1798-453e-bbb0-e5eb0df8dc75.aspx)</p><p>[Vorgehensweise: Arbeiten mit benutzerdefinierten Benutzeraktionen](https://msdn.microsoft.com/en-us/library/office/ee538686%28v=office.14%29.aspx) [Benutzerdefinierte Standardaktionsspeicherorte und IDs](http://msdn.microsoft.com/library/6889686e-f6e6-4da0-bfd4-099878614980.aspx)</p>|

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="sectionSection1"> </a>

|**Artikel**|**Zeigt, wie Sie auf...**|
|:-----|:-----|
| [Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites](Use-composed-looks-to-brand-SharePoint-sites.md)|Anwenden von zusammengesetzten, einschließlich Farben, Schriftarten und eines Hintergrundbilds, um Ihre SharePoint 2013 und SharePoint Online-Websites.|
| [Verwenden Sie remote-Bereitstellung zu Marke SharePoint-Seiten](Use-remote-provisioning-to-brand-SharePoint-pages.md)|Verwenden Sie remote-Bereitstellung zur Interaktion mit Designs in SharePoint.|
| [Mit der Marke SharePoint-Seiten CSS](Use-CSS-to-brand-pages.md)|Verwenden Sie remote-Bereitstellung zur Interaktion mit Designs in SharePoint.|
| [Anpassen einer SharePoint-Seite mithilfe von remote-Bereitstellung und CSS](Customize-a-SharePoint-page-by-using-remote-provisioning-and-CSS.md)|Verwenden Sie zum Anpassen von SharePoint-rich-Text-Felder und Webpartzonen CSS.|
| [Aktualisieren Sie das branding der vorhandenen SharePoint-Websites und Bereiche der Seite](update-the-branding-of-existing-sharepoint-sites-and-page-regions.md) | Passen Sie an und aktualisieren Sie das branding von vorhandenen SharePoint-Websites und Regionen von SharePoint-Seiten, einschließlich des Menübands, der Websitenavigation, im Menü Einstellungen, die Strukturansicht und dem Seiteninhalt.
|[Anpassen der OneDrive für Unternehmen Websitebranding](Customization-Options-For-OD4B-Sites.md)| Anpassen der OneDrive für Websites mit Geschäftsdaten in Office 365 oder über das Add-In Modell je nach den Anforderungen der Organisation.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)

-  [SharePoint-Seiten und das Seitenmodell](SharePoint-pages-and-the-page-model.md)

-  [SharePoint-Entwicklungs- und -Designtools und -Methoden](SharePoint-development-and-design-tools-and-practices.md)
