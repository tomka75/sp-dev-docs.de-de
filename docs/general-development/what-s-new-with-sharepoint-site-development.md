---
title: Neuigkeiten in der SharePoint-Websiteentwicklung
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ac1e9891-5ce9-4707-84e5-6e2fc02fda6b
ms.openlocfilehash: aa697345fd77c86159a94de4f5c91b79ead99e73
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-with-sharepoint-site-development"></a>Neuigkeiten in der SharePoint-Websiteentwicklung
Informationen über das neue Erstellungs -und Veröffentlichungsmodell in SharePoint zur Veröffentlichung von Websites.
## <a name="introduction-to-site-publishing-for-designers-and-developers-in-sharepoint"></a>Einführung in die Websiteveröffentlichung für Designer und Entwickler in SharePoint
<a name="SP15_WhatsNewSiteDevelopment_IntroductionToSitePublishing"> </a>

SharePoint führt die folgenden Features neu ein. Sie unterstützen den Workflow einer ECM-Websiteerstellung (Enterprise Content Management) für Veröffentlichungssites.
  
    
    

### <a name="client-programming-models-for-publishing-site-development"></a>Clientprogrammierungsmodelle für die Entwicklung von Veröffentlichungssites

In SharePoint können Sie das .NET-Clientobjektmodell (CSOM), Silverlight und die JavaScript-Programmierungsmodelle zum Entwickeln von benutzerdefinierten Websites, Sitekomponenten, Branding-Elementen und Verhalten verwenden. Viele der für die .NET-Serverprogrammierung verfügbaren APIs finden Sie im entsprechenden .NET-Client (CSOM), in Silverlight und in JavaScript-Assemblys. In einigen Fällen sind die entsprechenden APIs auch in Windows Phone-Bibliotheken verfügbar.
  
    
    
Weitere Informationen finden Sie in den Referenzhomepages zu Websites und Inhalten für  [.NET-Server](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx),  [.NET-Client](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx) und [JavaScript](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx). Sie können auch mit der  [-Referenzhomepage](http://msdn.microsoft.com/library/7940ba4e-f6f0-4bc0-b995-ceb2d358ca0d%28Office.15%29.aspx) beginnen, falls Sie ganz oben beginnen möchten und dann die Inhalte der einzelnen Programmierungsmodelle kennen lernen wollen.
  
    
    

### <a name="using-publishing-and-taxonomy-apis-with-the-new-sharepoint-app-model"></a>Verwenden von Veröffentlichungs- und Taxonomie-APIs im neuen SharePoint-App-Modell

Sie können benutzerdefinierten Client- und Servercode in SharePoint-Add-Ins schreiben und damit die SharePoint-Veröffentlichungs- und Taxonomiefunktionalität erweiterten. Diese steht den Benutzern auf der Benutzeroberfläche (UI) bereit. 
  
    
    
Einige Punkte bei der Entwicklung von Apps, die eine Websiteveröffentlichung verbessern, sind Umfragen, Kontoverwaltungs-Apps, eCommerce-Support, Apps, die soziale Funktionen und externe Daten in Veröffentlichungssites beinhalten, ausgelagerte zusätzliche Inhalte sowie mobile Begleit-Apps.
  
    
    

## <a name="authoring-design-and-branding-features"></a>Erstellungs-, Entwurfs- und Branding-Features
<a name="SP15_WhatsNewSiteDevelopment_AuthoringAndBranding"> </a>

SharePoint enthält Features und APIs für das Erstellen, Entwerfen, Branding und Erweitern Ihrer Website, des Websitedesigns, der Branding-Elemente und des Websiteverhaltens. 
  
    
    

### <a name="design-manager"></a>Design Manager

In früheren SharePoint-Versionen benötigte das Branding einer Website spezielle technische Kenntnisse beispielsweise zu Inhaltsplatzhaltern auf der Masterseite oder wie eine Masterseite bestimmte Steuerelementformatklassen bereitstellt. SharePoint führt den  [Entwurfs-Manager](overview-of-design-manager-in-sharepoint.md) ein, die neue Schnittstelle und zentraler Hub für die Verwaltung aller Branding-Aspekte auf Ihrer SharePoint-Website. Sie finden den Entwurfs-Manager auf der obersten Website Ihrer Websitesammlung. Er ist Teil der Websitesammlungsvorlage "Veröffentlichungsportal" in SharePoint.
  
    
    
Der Entwurfs-Manager ermöglicht eine schrittweise Herangehensweise für das Erstellen von Designobjekten, die Sie für das Branding von Websites verwenden können. Laden Sie zunächst die Designobjekte (Bilder, HTML, CSS usw.) hoch, und erstellen Sie dann Ihre Gestaltungsvorlagen und Seitenlayouts. Während des Entwurfs können Sie in einer Vorschau anzeigen, wie das Design in einem clientseitigen Codeeditor oder auf dem Server aussieht. Sie können benutzerdefinierte SharePoint-Komponenten und Menübandelemente mithilfe der Entwurfs-Manager-Benutzeroberfläche hinzufügen. Der Entwurfs-Manager generiert HTML-[Codeausschnitte](sharepoint-design-manager-snippets.md), die mit jedem Webdesigntool verwendet werden können. Er rendert HTML- und ignoriert ASP.NET- und SharePoint-Markup (während SharePoint nur ASP.NET- und SharePoint-Markup rendert und HTML.md ignoriert).
  
    
    
Sie können Ihre Kenntnisse in HTML, CSS und JavaScript zum Entwerfen von Gestaltungsvorlagen in HTML nutzen und HTML-Seitenlayouts im HTML-Editor Ihrer Wahl entwerfen. Um Ihr bevorzugtes Erstellungs- und Designtool mit Ihrer SharePoint-Website zu verbinden, [ordnen Sie ein Netzlaufwerk zu](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md), und bearbeiten Sie dann die SharePoint-Datei, als wäre sie eine lokale Datei. Wenn Ihr Websitedesign fertig ist, laden Sie den HTML-Code und die unterstützenden Dateien hoch, und verwenden Sie den Entwurfs-Manager, um die [HTML-Datei in eine ASP.NET-Gestaltungsvorlage (.master.md-Datei) zu konvertieren](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md). Jetzt [wenden Sie die Gestaltungsvorlage](how-to-apply-a-master-page-to-a-site-in-sharepoint.md) auf Ihre SharePoint-Website an. Verwenden Sie den Entwurfs-Manager zum [Erstellen eines neuen Seitenlayouts](how-to-create-a-page-layout-in-sharepoint.md); die HTML-Version wird automatisch der entsprechenden ASP.NET-Seite (.aspx Datei.md) zugeordnet, die SharePoint interpretiert. 
  
    
    
Nachdem Sie Ihre HTML-Dateien konvertiert haben, verfeinern Sie Ihren Entwurf im HTML-Editor, zeigen Ihre Dateien in einer Vorschau an und speichern sie. Immer wenn Sie HTML-Versionen der Masterseite oder der Seitenlayoutdateien speichern, aktualisiert SharePoint automatisch die damit verbundene SharePoint-Masterseite und die Seitenlayouts, um den Änderungen Rechnung zu tragen. 
  
    
    
Mit dem Entwurfs-Manager müssen Sie nur die HTML-Dateien bearbeiten. Sie können weiterhin benutzerdefinierte Masterseite und Seitenlayouts mit Ihren ASP.NET- und SharePoint-Entwicklungskenntnissen erstellen. Der Entwurfs-Manager befähigt Sie auch ohne große SharePoint-Entwicklerkenntnisse, großartige Websites zu entwerfen.
  
    
    
SharePoint beinhaltet auch HTML-Versionen mehrerer Masterseiten und Seitenlayouts, die Sie als Startvorlagen nutzen können. Wenn Sie mit diesen Dateien beginnen möchten, erstellen Sie eine Kopie der HTML-Seite (die verknüpfte ASP.NET-Datei wird automatisch verarbeitet), und bearbeiten Sie dann die HTML-Datei in der üblichen Weise. Sie können auch mit einer Basisvorlage beginnen, indem Sie die Option **Masterseite aus Minimalvorlage** verwenden, die dann selbsttätig die damit verbundene .master-Datei erstellt.
  
    
    

### <a name="snippet-gallery"></a>Codeausschnittkatalog

SharePoint enthält viele einsatzbereite Komponenten, wie Webparts und Steuerelemente, die Sie Ihren Webseiten hinzufügen können. Beispiel: Sie fügen eine SharePoint-Komponente, wie ein Suchfeld oder ein Navigationssteuerelement, in die HTML-Masterseite ein, um somit schnell und einfach viel Funktionalität in Ihre Seiten einzubauen.
  
    
    
In der Gruppe **Codeausschnittkatalog** des Menübands können Sie eine Komponente auswählen, ihre Eigenschaften konfigurieren und den Codeausschnitt aktualisieren, den generierten HTML-Codeausschnitt kopieren und diesen HTML-Codeausschnitt in Ihre HTML-Datei einfügen. Der HTML-Codeausschnitt bietet Ihnen eine äußerste präzise Vorschau der Komponente, sowohl in der serverseitigen Vorschau als auch im HTML-Editor Ihrer Wahl. Nachdem Sie Ihren HTML-Dateien SharePoint-Komponenten hinzugefügt haben, können Sie CSS für das vollständige Branding verwenden. Ebenso wie bei jeder Aktualisierung der HTML-Datei werden die Änderungen nach dem Hinzufügen von SharePoint-Komponenten und ihrem Branding automatisch mit der zugeordneten Gestaltungsvorlage bzw. dem Seitenlayout synchronisiert. Die HTML-Codeausschnitte werden automatisch in SharePoint-Komponenten konvertiert.
  
    
    
 Unabhängig davon, ob die HTML-Datei eine Masterseite oder ein Seitenlayout ist, zeigt der Codeausschnittkatalog die benötigten Komponenten an. Falls Sie nicht den benötigten Codeausschnitt entdecken, können Sie immer noch einen HTML-Codeausschnitt des ASP.NET-Markup erstellen und diesem zur HTML-Masterseite bzw. zum Seitenlayout hinzufügen.
  
    
    
Der Entwurfs-Manager generiert HTML-Codeausschnitte, die mit jedem Webentwurfstool verwendet werden können. Er rendert einfach nur HTML- und ignoriert ASP.NET- und SharePoint-Markup. SharePoint rendert nur ASP.NET- und SharePoint-Markup, ignoriert aber HTML.
  
    
    

### <a name="device-channels"></a>Gerätekanäle

Im Entwurfs-Manager erstellen Sie  [Gerätekanäle](sharepoint-design-manager-device-channels.md) und ordnet diese dann mobilen Geräten oder Browsern mithilfe von Teilzeichenfolgen der einzelnen auf dem Gerät eingehenden Zeichenfolge des Benutzer-Agenten zu. Ein Gerät kann zu mehreren Kanälen gehören, und die Kanäle können somit eine Rangordnung haben. Beispiel: Wenn Sie Gerätekanäle für "Smartphones" und "Windows Phone 8" erstellen, können Sie die Kanäle ordnen, so dass die Geräte, mit Windows Phone 8 ausgeführt werden, einen speziell für sie reservierten Kanal bekommen, während andere Smartphones zum "Smartphones"-Kanal zugeordnet werden.
  
    
    
Nachdem Sie die Kanäle festgelegt haben, ordnen Sie dem Kanal eine Masterseite zu. Diese Masterseite verweist auf eine andere CSS-Datei als die Masterseite für den Standardkanal. Alle von Ihnen erstellten Seitenlayouts arbeiten mit alle von Ihnen erstellten Kanälen zusammen. Wenn Sie die Seitenlayoutentwürfe bei den Kanälen unterschiedlich entwerfen möchten, verwenden Sie das Steuerelement **Gerätekanalbereich**.
  
    
    
Veröffentlichungssites in SharePoint sind für eine mobile Entwicklung optimiert. Sie können mit dem Gerätekanalfeature Kanäle für mindestens ein Gerät definieren, um Ihnen eine Kontrolle darüber zu geben, wie Mobilgerätbenutzer die Benutzerfreundlichkeit Ihrer Website erfahren. Für eine bessere Optik, können Sie den einzelnen Kanälen eine alternative Masterseite zuweisen. Wählen Sie, ob Sie Teile eines Seitenlayouts in einen Kanal mit ein- oder ausschließen möchten, und sehen Sie in der Vorschau, wie der mobile Kanalentwurf während der Entwicklung fortschreitet. Gerätekanäle werden vor dem Hintergrund einer Suchmaschinenoptimierung (SEO) geplant. Passen Sie damit Look and Feel der vorhandenen Seiten an, um mobile Szenarien zu unterstützen.
  
    
    
Sie können Kanäle dafür einsetzen, dass bestimmte Renderings auf bestimmten Geräten erschienen; dies wird Kanäle erzwingen genannt. Dies ist bei mobilen Szenarien nützlich, wenn Sie ein Rendering geplant haben, das für ein bestimmtes mobiles Gerät optimiert ist.
  
    
    

### <a name="device-channel-panel-control"></a>Steuerelement "Gerätekanalbereich"

"Gerätekanalbereich" ist ein neues Steuerelement, das Sie in das Seitenlayout mit aufnehmen können, um zu steuern, welche Inhalte in welchem Kanal gerendert werden sollen. Der Gerätekanalbereich ist ein Container, der einem oder mehreren Kanälen zugeordnet ist: Wenn mindestens einer dieser Kanäle während des Renderings der Seite aktiv ist, werden alle Inhalte des Gerätekanalbereichs gerendert. Über "Gerätekanalbereich" können Sie festlegen, wann ein bestimmter Inhalt für bestimmte Kanäle mit eingeschlossen werden soll.
  
    
    

### <a name="display-templates"></a>Anzeigevorlagen
<a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a>

Sie möchten möglicherweise Format und Darstellung der Suchergebnisse auf Ihrer Website steuern können. Verwenden Sie dazu Anzeigevorlagen, die die verfügbaren Optionen einer Anpassung der Suchergebnisse über die Benutzeroberfläche über die Zuordnung der anzuzeigenden vordefinierten Felder hinaus erweitern.
  
    
    
Es gibt drei Kontexte, wenn Sie Anzeigevorlagen mit Suchergebnissen verwenden möchten: eine Darstellungszuordnung der Gesamtstruktur der Suchergebnisse, eine Darstellung von gruppierten Ergebnissen und eine Darstellung der einzelnen Ergebnisse oder Elemente im Resultset. Diese Darstellungsarten werden "Steuerelementvorlage", "Gruppenvorlage" und "Elementvorlage" genannt.
  
    
    
Weitere Informationen zu Anzeigevorlagen finden Sie unter  [Anzeigevorlagen im SharePoint-Entwurfs-Manager](sharepoint-design-manager-display-templates.md).
  
    
    

### <a name="image-renditions"></a>Bilddarstellungen
<a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a>

Mit  [Bildwiedergaben](sharepoint-design-manager-image-renditions.md) können Sie hochgeladene Bilder in vordefinierten Größen, Breiten und Beschnitten anzeigen. Sie können mehrere Wiedergaben ein und derselben Quellbilddatei erstellen. Das heißt, Sie können die Anzeigemerkmale einmal festlegen und sie dann auf eine beliebige Anzahl Bilder anwenden. Beispiel: Eine Bildwiedergabe namens **Article_image** zeigt ein Bild in Vollbildgröße in einem Artikel an, während die Wiedergabe namens **Thumbnail_small** eine kleinere Version des Bildes in einem von Ihnen definierten Kontext anzeigt.
  
    
    
Bevor Sie Bildwiedergaben verwenden können, stellen Sie sicher, dass der BLOB-Cache auf dem Server aktiviert ist. Dies erfolgt über in den Internetinformationsdiensten (IIS) mit den Verwaltungstools. Suchen Sie dort nach der **web.config**-Datei, und aktivieren Sie den BLOB-Cache. Aktualisieren Sie die Seite, damit die Bildwiedergaben verfügbar sind.
  
    
    

## <a name="managed-metadata-and-navigation-in-sharepoint"></a>Verwaltete Metadaten und Navigation in SharePoint
<a name="SP15_WhatsNewSiteDevelopment_MetadataAndNavigation"> </a>

Die in eingeführten Enterprise-Managed-Metadaten-Funktionen (EMM) wurden in SharePoint für mehr Leistung, leichteren Zugriff über die Benutzeroberfläche und taxonomiegesteuerte Navigation, die so genannte verwaltete Navigation, verbessert und erweitert.
  
    
    

### <a name="managed-navigation"></a>Verwaltete Navigation

Verwaltete Navigation ist die taxonomiegesteuerte Alternative zur herkömmlichen SharePoint-Navigationsfunktion, der strukturierten Navigation, die auf den SharePoint-Strukturen basiert. Die Funktion der  [verwalteten Navigation](managed-navigation-in-sharepoint.md) ermöglicht Ihnen den Entwurf einer Websitenavigation, die über verwaltete Metadaten gesteuert wird. Verwalte Navigation erstellt SEO-optimierte URLs, die aus der verwalteten Navigationsstruktur abgeleitet werden. Da die verwaltete Navigation taxonomisch gesteuert wird, können Sie diese für den Entwurf der Websitenavigation in wichtigen Geschäftskonzepten verwenden, ohne die Struktur Ihrer Website oder Websitekomponenten ändern zu müssen.
  
    
    

### <a name="content-search-web-part"></a>Webpart für Inhaltssuche
<a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a>

Mit dem  [Inhaltssuche-Webpart (CSWP)](content-search-web-part-in-sharepoint.md) können Sie Suchdaten auf Ihren Seiten anzeigen. Der Webpart hat eine ähnliche Funktion wie die des Webparts für Inhaltsabfragen, aber seine Websitedesignziele sind andere. CSWP-Formatvorlagen können leichter angepasst werden als CQWP-Formatvorlagen. CSWP gibt clientseitige Ergebnisse im JSON-Format zurück. Sie können auf dem Server Ergebnisse mithilfe von Anzeigevorlagen anpassen.
  
    
    

### <a name="other-managed-metadata-improvements-for-sites"></a>Weitere verwaltete Metadatenverbesserungen für Websites
<a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a>

SharePoint führt mehrere Verbesserungen bei verwalteten Metadaten-Benutzeroberflächen und Funktionen ein. Weitere Informationen finden Sie unter  [Verwaltete Metadaten und Navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md).
  
    
    

## <a name="publishing-content-in-sharepoint"></a>Veröffentlichung von Inhalten in SharePoint
<a name="SP15_WhatsNewSiteDevelopment_Publishing"> </a>

SharePoint bietet neue Features für das Veröffentlichen von Inhalten, mit denen Sie Veröffentlichungssites entwerfen können, die wiederum neue, flexiblere und komplexere Topologien und Szenarien unterstützen. 
  
    
    

### <a name="design-packages"></a>Designpakete

Wenn Sie ein erfahrener Webdesigner sind, möchten Sie vielleicht einen Entwurf in Ihrer eigenen Umgebung oder Websitesammlung erstellen und testen, bevor er in anderen Websitesammlungen installiert wird. Sollten Sie die websiteübergreifende Veröffentlichung zum Teilen von Inhalten in allen Websitesammlungen verwenden, können Sie denselben Entwurf als Paket auf jeder Website installieren.
  
    
    
In früheren SharePoint-Versionen mussten Sie, wenn Sie einen Entwurf erneut verwenden wollten, Visual Studio installiert haben, um ein SharePoint-Lösungspaket (.wsp-Datei) zu erstellen. Auf der Zielwebsite mussten Sie dann das Paket in den Lösungskatalog hochladen und dort ausführen. In SharePoint können Sie jetzt, nachdem Sie den Entwurf Ihrer Website abgeschlossen haben, im Entwurfs-Manager **Paket exportieren** wählen, um eine einzige .wsp-Datei, das so genannte [Designpaket](sharepoint-design-manager-design-packages.md) zu exportieren. Beim Export eines Designpakets erstellt SharePoint automatisch ein Designpaket des gesamten Inhalts, den Sie im Masterseitenkatalog, in der Formatbibliothek, in der Designgalerie, in der Gerätkanalliste und in den Seiteninhaltstypen hinzugefügt oder geändert haben. 
  
    
    

> **Hinweis:** Ein Designpaket enthält keine Seiten, Navigationseinstellungen oder den Terminologiespeicher. 
  
    
    

Designpakete überschreiben bei öffentlichen Office 365-Websites keine vorhandenen Dateien Bei der Installation eines Designpakets wird ein neuer Ordner im Masterseitenkatalog, in der Formatbibliothek und in der Designgalerie erstellt, in der die Designelemente isoliert sind. 
  
    
    
Wenn Sie ein Designpaket importieren, überschreiben die Designelemente des Pakets vorhandene Dateien. Die Designelement werden dann auf das aktuelle Design der Website angewendet. Die Standard- und Systemmasterseite der Website, das Design und die alternative CSS-Datei sind alle in den Dateien im Designpaket festgelegt. Ein Entwurf, der in einer Umgebung erstellt wurde, kann mit Designpaketen problemlos auf andere, separate Umgebungen angewendet werden.
  
    
    

### <a name="catalogs"></a>Kataloge

Websiteveröffentlichung in SharePoint führt Kataloge ein, mit deren Hilfe Sie Listen in Veröffentlichungssites einbinden können. Mit Katalogen können Inhalte in allen Websitesammlungen veröffentlicht werden. Die Funktionen der websiteübergreifenden Veröffentlichung hängen vom jeweiligen Katalog ab. Sie können Kataloge für eine Wiederverwendung von Inhalten auf allen Ihren Websites und grenzüberschreitend auf allen Ihren Intranetwebsites, Internetwebsites und Extranetwebsites verwenden. Kataloge sind bei vordefinierten Suchabfragen in der Suche gekennzeichnet. Sie können Inhalte in Katalogen in allen Websitesammlungen darstellen, wenn Sie dazu den [Inhaltssuche-Webpart (CSWP)](content-search-web-part-in-sharepoint.md) verwenden. Außerdem können Sie benutzerdefinierten Code schreiben, um Kataloge zu befüllen, einen Produktkatalog mit einer Seite verknüpfen und individuelle Seiten mit benutzerdefiniertem Seitenlayout, Webparts und HTML-Inhalten, die ausschließlich im festgelegten Kontext erscheinen, verbessern.
  
    
    

### <a name="client-side-rendering-controls"></a>Clientseitige Rendering-Steuerelemente

Alle neuen Steuerelemente in SharePoint werden clientseitig wiedergegeben. Als Designer oder Entwickler können Sie steuern, wie Inhalte auf der Seite wiedergegeben werden sollen. Sie können außerdem zahlreiche Designtechniken verwenden, um das gewünschte Erscheinungsbild und Verhalten auf den veröffentlichten Seiten zu erzielen, indem Sie Features wie Inhaltssuche-Webparts und Anzeigevorlagen mit einschließen. Daten werden in einem clientseitigen JSON-Array in die Steuerelemente geschrieben. Inhalte zeigen Sie über JavaScript, CSS und Vorlagen an. 
  
    
    

### <a name="cross-site-publishing"></a>Websiteübergreifende Veröffentlichung

Microsoft SharePoint führt ein websiteübergreifendes Veröffentlichungsfeature ein, mit dem Sie Inhalte in mehreren Websitesammlungen wiederverwenden können. Es verwendet integrierte Suchfunktionen, um Szenarien und Architekturen veröffentlichen zu können. Zum ersten Mal können Sie jetzt Websites farmübergreifend in SharePoint erstellen. Damit überbrücken Ihre Websites die Kluft zwischen Intranet und Internet. 
  
    
    
Verwenden Sie die Themenseitenfunktion, um die Benutzerfreundlichkeit der Startseite an Inhalte anzupassen, die websiteübergreifend veröffentlich werden. Verwenden Sie auch SEO-freundliche URLs für das Verwalten und eine leichtere Aufrechterhaltung der Websitestruktur in einer breiten Palette an Szenarien, einschließlich komplexer mehrsprachiger Websitetopologien.
  
    
    
Weitere Informationen zur websiteübergreifenden Veröffentlichung finden Sie unter [Szenario: Erstellen von SharePoint-Websites mit websiteübergreifender Veröffentlichung in SharePoint](http://technet.microsoft.com/en-us/sharepoint/jj872721). Weitere Informationen über Entwicklungsoptionen für die websiteübergreifende Veröffentlichung finden Sie unter [Websiteübergreifende Veröffentlichung in SharePoint](cross-site-publishing-in-sharepoint.md).
  
    
    

### <a name="seo-enhancements"></a>SEO-Verbesserungen

Viele Benutzer von Geschäftswebsites werden von großen Suchmaschinen wie Bing und seine Konkurrenten zu Geschäftswebsites im Internet umgeleitet. SharePoint umfasst Features, wie benutzerfreundliche URLs, Homepageumleitung, XML-Sitemaps, benutzerdefinierte SEO-Eigenschaften, mit denen Sie flexibel Browsertitel, **<Meta>**-Tagbeschreibungen, Schlüsselwörter und leichtverständliche URLs für mehrsprachige Websitevarianten festlegen können.
  
    
    
In Office 365 generiert die Websiteinfrastruktur innerhalb von 24 Stunden nach einer Websiteänderung eine aktualisierte XML-Sitemap. Dank der lokalen Installation können Sie die Aktualität Ihrer Sitemaps anpassen und festlegen, welche Suchmaschinen Microsoft für Sie pingen soll, wenn die Sitemap aktualisiert wird.
  
    
    
Das, was Ihre Freunde auf Facebook mögen, beeinflusst das, was Sie in den von Bing und anderen Suchmaschinen zurückgegebenen Suchergebnissen sehen. Sie können APIs in SharePoint-Programmierungsmodellen verwenden, um eine Suchoptimierung für Ihre Website anzupassen.
  
    
    

### <a name="analytics-and-recommendations"></a>Analyse und Empfehlungen

Sie können nachverfolgen, wie Personen Veröffentlichungswebsites und deren Komponenten unter Zuhilfenahme des SharePoint Analytics-Features nutzen, das tief in die Suchmaschine integriert ist. Analytics befördert die Empfehlungsmöglichkeiten bei Inhalten und führt Berechnungen als verwaltete Eigenschaften in den Suchindex ein. Die Empfehlungen von Suchanalysen, wie Seitenaufrufe und eindeutige Elemente pro Tag, beeinflussen die Relevanz von Suchergebnissen.
  
    
    
Analytics anonymisiert Daten und macht alle 2 Wochen ein Rollup. Analytics löscht erst alle 2 Wochen, dann nach 3 Jahren jeden Monat, Ereignisse. Lebensdaueransichten bleiben immer erhalten. Der zuletzt angezeigte Inhalt wird zunächst geglättet, bevor Analytics Aggregatdaten in eine Berichtsdatenbank verschiebt. Für den Export von Daten aus der Berichtsdatenbank in Excel, für das Anpassen der Gewichtung von **View**-Ereignissen und für das Erstellen von benutzerdefinierten Ereignissen, einschließlich jener, die von JavaScript bereitgestellt werden, können Sie benutzerdefinierten Code verwenden.
  
    
    

### <a name="variations-and-multilingual-sites"></a>Variationen und mehrsprachige Websites

Sie können das Variationsfeature in SharePoint verwenden, um mehrsprachige Websites oder andere Websites zu erstellen, auf denen Sie die Präsentation Ihrer Inhalte variieren möchten. Das Variationsfeature ist auf eine Websitesammlung beschränkt. Das heißt, Sie können für eine Quellsprache/ein Quellgebietsschema mehrere Zielsprachen-/-gebietsschema-Varianten als aktuelle Websites innerhalb der gleichen SharePoint-Websitesammlung erstellen. Variationen unterstützen benutzerfreundliche URLs sowie die Möglichkeit zum Exportieren oder Importieren von Inhalten für die Übersetzung durch einen Drittanbieter im [XLIFF-Dateiformat](the-xliff-interchange-file-format-in-sharepoint.md). Sie können Bezeichnungen, eine Seite für Übersetzung und Replikation, eine Vielzahl von Listenelementen (z. B. Dokumentbibliotheken.md) und Navigation in die Exportpakete einbeziehen. 
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_WhatsNewSiteDevelopment_AdditionalResources"> </a>


-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [Vorgehenweise: Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md)
    
  
-  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md)
    
  
-  [Übersicht über Designs für SharePoint](themes-overview-for-sharepoint.md)
    
  
-  [Verwaltete Metadaten und Navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [What's new in SharePoint-Suche für Entwickler](what-s-new-in-sharepoint-search-for-developers.md)
    
  

