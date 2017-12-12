---
title: "Bewährte Methoden für SharePoint Online-Portale - Leistung"
ms.date: 11/03/2017
ms.openlocfilehash: 6c0d6e5783f2de3f65553810a6408df837fd6f86
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="proven-practices-for-sharepoint-online-portals---performance"></a>Bewährte Methoden für SharePoint Online-Portale - Leistung

Jedes Portal Entwurf enthält mindestens einen Aspekt, die die Anpassung von SharePoint erforderlich sind. Die Anpassungsmodell für SharePoint Online-Portale ist der SharePoint-Add-in-Objektmodell oder die SharePoint-Framework. Diese beiden im Wesentlichen verwenden eine verteilten Anwendungsarchitektur, die umfassen eine Reihe von ausführungsumgebungen: SharePoint Online, Web Hoster(s), Dienst-Anbieter und den Clientbrowser. Diese Architektur ist auf das Konzept der Client-zu-Server-Anforderungen basiert.

Implementieren von Anpassungen für SharePoint Online, und platziert eine noch größere Schwerpunkt effektiven Entwurf und Entwicklung für Webanwendungen im Allgemeinen und Webanwendungen mithilfe der clientseitigen insbesondere, besonders wenn es darum geht, das Konzept der Anwendung Leistung.

> [!NOTE] 
> Obwohl dieser Anleitung in erster Linie SharePoint Online bezieht, die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet.

_**Gilt für:** SharePoint Online_

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a>Anti-Muster (also nicht sollten Sie folgende Aktionen)
<a name="bk_antiPatterns"> </a>

Wenn Leistungsprobleme im Zusammenhang mit SharePoint im Allgemeinen werden soll, und Ihre benutzerdefinierte Portal insbesondere, berücksichtigen Sie die folgenden Anti-Muster:

- Erstellen von benutzerdefinierten mithilfe der clientseitigen Steuerelementen, die Ausstellen von clientseitigen Daten Anforderungen für SharePoint und Hinzufügen von zwölf oder mehrere Steuerelemente auf der Seite
- Implementieren Sie die clientseitige Steuerelemente ohne zentralisierte Datenzugriff für die SharePoint-Daten, sodass zahlreiche Steuerelemente dieselben Daten auf einer Seite mehrfach anfordern
- Redundante benutzerdefinierten JavaScript und CSS-Code in der gesamten im Textkörper der Seite einbetten
- Mehrere Miniaturansichten von 10MB in der gesamten im Textkörper der Seite einbetten
- Führen Sie alle clientseitigen Daten Anforderungen zur Seitenladezeit, auch wenn die Daten nicht zunächst benötigt/angezeigt werden, auch wenn sie noch nie verwendet werden
- Fügen Sie unnötige Reihenfolge Abhängigkeiten in die Daten Sequenz anfordern und **synchronen** Anforderungen von Daten verwenden, um sicherzustellen, dass die Reihenfolge der Ausführung
- Verwenden Sie den legacy-Webdienst für SharePoint-Listen (SOAP), wie die Daten API Wahl anfordern, und geben Sie ihn schlecht formulierte CAML-Abfragen
- Vermeiden Sie das Zwischenspeichern Daten Antworten (besonders für statische Daten) auf dem Client, um sicherzustellen, dass jede Anforderung Daten bei jedem Laden der Seite erneut ausgeführt wird
- Führen Sie Hunderten von Updates auf das Modell DOM (Document Object) auf der Seite wie jeder Datenantwort abgeschlossen ist aus, auch wenn sie redundante oder miteinander in Konflikt stehende sind

## <a name="introduction"></a>Einführung
<a name="bk_introduction"> </a>

Die SharePoint Online Anpassungsmodell hat, wo benutzerdefinierter Code auf dem Server ausgeführt und führt serverseitige Daten Anforderungen in einer modernen, Client-basierte Objektmodell, wo benutzerdefinierter Code Remote ausgeführt, und führt mithilfe der clientseitigen, aus dem klassischen, Server-basierte Modell entwickelt Anforderungen für Daten.  Die natürliche Lösungsarchitektur für dieses Modell ist die verteilte mithilfe der clientseitigen Webanwendung.

Eine Folge des verteilten mithilfe der clientseitigen Web-Anwendungsmodell, abgesehen davon, dass eine Erhöhung der Sicherheitsmechanismen Komplexität der neuen benutzerdefinierten Lösung, ist eine erhebliche Steigerung Client-zu-Server des Netzwerkdatenverkehrs der neuen benutzerdefinierten Lösung und eine größere zugeordnet Abhängigkeit von der Umgebung der Client-seitigen Ausführung.

Berücksichtigen Sie den folgenden Vergleich von jedem Web-Anwendungsmodell zugeordnet Ablauf beim Laden der Seite:

### <a name="classic-server-side-web-application-sequence"></a>Klassische serverseitige Web Application Sequenz

- Besuchen Sie zuerst zur Seite
    - Problem Seitenanforderung
    - Ausstellen von Datei-ressourcenanforderungen (null oder mehr)
    - Ausführen von JavaScript
- Rückgabe Zugriff auf Seite
    - Problem Seitenanforderung
    - Ausführen von JavaScript

### <a name="modern-client-side-web-application-sequence"></a>Moderne mithilfe der clientseitigen Web Application Sequenz

- Besuchen Sie zuerst zur Seite
    - Problem Seitenanforderung
    - Ausstellen von Datei-ressourcenanforderungen (null oder mehr)
    - Ausführen von JavaScript
    - Problem Datenanfragen (null oder mehr)
    - Führen Sie mehr JavaScript
- Rückgabe Zugriff auf Seite
    - Problem Seitenanforderung
    - Ausführen von JavaScript
    - Problem Datenanfragen (null oder mehr)
    - Führen Sie mehr JavaScript

Eine Netzwerkmonitor zeigt an, dass moderne Webseite auf einfache Weise einen Anstieg der Reihenfolge der Größe des Netzwerkdatenverkehrs im Vergleich zu einer klassischen Webseite, führen kann. Ein browserbasierte Ausführung Profiler auch zeigt an, dass moderne Webseite größere eine Abhängigkeit für die Ausführung von Client-seitigen JavaScript hat.  Erteilt, diese erhöht werden, eine Funktion des Entwurfs und der Implementierung der neuen Lösung, jedoch ist die Wahrscheinlichkeit, dass eine erhebliche Steigerung hoch.

## <a name="general-performance-guidelines-for-client-side-web-applications"></a>Allgemeine Leistungsrichtlinien für clientseitige Web Applications
<a name="bk_performanceGuidelines"> </a>

Bestätigen Sie einmal zum Erstellen einer benutzerdefinierten mithilfe der clientseitigen Webanwendung:

- Bestätigen Sie, dass Sie nun für die Client-seitigen Leistung dieser Anwendung zuständig sind
- Bestätigen Sie, dass die Vorteile von Server-Side rendering und Zwischenspeichern nicht mehr für Ihre benutzerdefinierten Steuerelemente verfügbar sind
- Beachten Sie, dass die Anwendung nun gut funktionierende, mithilfe der clientseitigen Entsprechungen bereitstellen müssen

>**Im Hinblick auf Leistung**: das Ziel mit modernen Webanwendungen in Allgemein und mithilfe der clientseitigen Webanwendungen ist insbesondere zum Implementieren der clientseitige Logik, die erforderlich sind, um die minimale Netzwerk Datenverkehr Muster für *beobachteten Rückgabe imitieren *Zugriffe auf klassische Webseiten.

Die folgenden Abschnitte enthalten Leitfaden zur Leistung für dieses Ziel zu erreichen.

### <a name="telemetry"></a>Telemetrie
<a name="bk_Telemetry"> </a>

Leistung wird häufig von Endbenutzern im subjektive Begriffe angezeigt. Es ist jedoch Herausforderung um definitiv Probleme zu beheben, z. B."das Portal langsame".  Um die wahrgenommene Leistungsprobleme quantifiziert, ist es wichtig, objektive Metriken für die Webanwendung mithilfe der clientseitigen zu erhalten.

Entwurf und Entwicklung Ihrer Webanwendung mithilfe der clientseitigen sollte Telemetrie zum Einrichten einer Leistungsbasislinie und permanente Überwachung von der Laufzeit-Leistung der Anwendung enthalten.

Erfassen Sie wichtige Informationen Anwendung Metriken wie:

- Anwendung Initialisierung timing
- Die Seite geladen Anzeigedauer (im Allgemeinen und für bestimmte Seiten)
- Mithilfe der clientseitigen Timing (im Allgemeinen und für bestimmte Aktionen)
- Externe Anforderung und Antwort Timing (z. B. SharePoint REST-aufrufen, Drittanbieter-Services usw..)
- Suche zeitliche Steuerung der Ausführung
- Seitenereignisse
- Ebene (d. h., Benutzer) Aktionen
- Ausnahmen auftritt (z. B. Fehler bei der Anforderung von Daten, die Anforderung gedrosselt Daten usw.)

Einrichten Sie einer Leistungsbasislinie objektive für Ihre Webanwendung mithilfe der clientseitigen, und mit dieser Baseline Tune überprüfen Sie Ihre Entscheidungen Erstentwurfs.  Wenn die Anwendung bereitgestellt wurde, überwachen Sie der Leistung von laufenden und verwenden Sie die Metriken zu identifizieren und Beheben von Problemen, die auftreten können.

Erwägen Sie [Einblicke in Azure-Anwendung](https://azure.microsoft.com/en-us/blog/understand-your-sharepoint-usage-with-application-insights-2/), die ein JavaScript-Modul bereitstellt, die Telemetrie jede mithilfe der clientseitigen Web-Anwendung hinzufügen erleichtert. Sie können auch einen eigenen Telemetrie Back-End-Dienst erstellen, aber Sie wissen, speichern die Telemetrie, die Daten in SharePoint überhaupt nicht empfohlen werden, wie, die sich negativ auf die Leistung Ihres Portals auswirkt.

### <a name="client-browser"></a>Clientbrowser
<a name="bk_clientBrowser"> </a>

Der Clientbrowser kann eine erhebliche Auswirkungen auf die Leistung der Webanwendung mithilfe der clientseitigen im Hinblick auf die tatsächliche Leistung und verfügbare Funktionalität haben.

Im Allgemeinen sollten Sie die aktuelle Version modernen Browser Ziel, die mit dem desktop Betriebssystem kompatibel sind. 

Es wird eine große Unternehmen mindestens einen webbasierten Line-of-Business (LOB)-Anwendung sein, die die Verwendung eines legacy-Browsers weiterhin erforderlich sind. Diese Einschränkung sollten jedoch nicht den Fortschritt von neuen Webanwendungen beeinträchtigen. Entwerfen Sie neue Client-Side-Webanwendungen zu nutzen, der die verbesserte Leistung und und Funktionalität der modernen Browser.  Beim Umgang mit einer Einschränkung legacy Browser:

- Behandeln Sie legacy Browseranforderungen als Ausnahmen; Analysieren Sie die Gesamtkosten der Bearbeitung der Ausnahme
- Verzögert/Deaktivieren der modernen Funktionen der neuen Anwendung bei ein älterer Browser zur Laufzeit erkannt wird
- Erwägen Sie älteren Browser, nur für die eingeschränkte LOB-Anwendung; Verwenden Sie für alle anderen, einschließlich der neuen mithilfe der clientseitigen Webanwendung(en) einen modernen browser

Finden Sie im Artikel [Browserunterstützung für Office 365](https://support.office.com/en-us/article/Office-Online-browser-support-AD1303E0-A318-47AA-B409-D3A5EB44E452) für die neuesten Browseranforderungen für Office 365.

### <a name="client-environment-and-network-topology"></a>Client-Umgebung und Netzwerktopologie
<a name="bk_clientEnvironment"> </a>

Der Clientumgebung und der Netzwerktopologie des Clients mit dem Server verbinden können eine erhebliche Auswirkungen auf die Leistung von Webanwendungen mithilfe der clientseitigen aufweisen.

Im Idealfall die Clientumgebung besteht aus modernen Browser auf dem neuesten Stand Clientcomputern und über ein Netzwerk mit ausreichend Bandbreite mit geringer Latenz mit dem Server verbunden ist. In der Praxis Sie System mit einem weniger als idealen Szenario einzurichten und Ihre Webanwendung möglicherweise nicht die politische Währung erforderlich sind, um die sofortige Änderung Laufwerk verfügbar. Als solche zum Anpassen des anfänglichen Entwurfs der Webanwendung mithilfe der clientseitigen vorhanden Nebenbedingungen mit einen Plan für die Client-Umgebung Verbesserungen bei Bereitstellung nutzen entsprechen. In diesem Fall werden möglicherweise eine Kombination von Client auftreten, den Computer so sicher, dass Ihre Webanwendung mithilfe der clientseitigen kann Clientfunktionen zur Laufzeit erkennen und ihr Verhalten entsprechend anpassen.

Finden Sie im Artikel [Office 365 Netzwerkplanung and Performance Tuning](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848) Anleitung für die Planung der Netzwerk Leistung.

### <a name="data-request-patterns"></a>Daten Anforderung Muster
<a name="bk_dataRequestPatterns"> </a>

Eine ordnungsgemäße Verwaltung des Datenverkehrs mithilfe der clientseitigen Anforderung ist entscheidend für die Leistung einer benutzerdefinierten mithilfe der clientseitigen Webanwendung fest.  In diesem Zusammenhang sollte Ihre Vorrangiges Ziel darstellen, zu minimieren und zur Optimierung der Client-zu-Server-Anforderungen, die die Anwendung erforderlich ist.

Verwenden Sie eine intelligente Datenladevorgänge-Muster, um Ihre Anforderungen für Daten (aus dem Server oder einer anderen Back-End-Datenquelle) steuern:

- Defer die Anforderung Daten so lange wie möglich (d. h., verzögerte Laden)
- Anfordern der Daten nur, wenn, und wenn sie tatsächlich benötigt wird. beispielsweise wie in der Antwort auf ein Browser-Ereignis oder Benutzeraktion
    - d. h., keine Daten für ein Steuerelement reduziert/ausgeblendet anfordern; Warten Sie, bis das Steuerelement erweitert/gerendert wird.

Verwenden Sie einen mithilfe der clientseitigen Cache, um alle Daten Anforderungen erfüllen:
 
- Wenden Sie sich an den lokalen Datencache vor dem Ausstellen der Anforderung von Daten an den server
- Return zwischengespeicherten Daten, sofern es vorhanden ist und noch nicht abgelaufen (z. B. beim Cachetreffer)

Rufen Sie den Server (oder anderen Back-End-Datenquelle) nur auftritt, wenn ein Cache verpassen:

- Rufen Sie die aktuellen Daten über einen asynchronen AJAX-Aufruf (nie verwenden einen synchronen AJAX-Aufruf)
- Zurückgeben Sie veraltet (oder Standarddomäne) Daten, wenn eine Anforderung für neue Daten fehlschlägt
- Berücksichtigen Sie die Präsentation einer Statusanzeige während ein Anrufs hoher Latenz Flug wird

Die Datenantwort zu analysieren: 

- Entfernt alle Anforderung-spezifisches Packen Ebenen aus der Antwort
- Extrahieren Sie die Ergebnisse der **Kern** -Daten und Konvertieren in eine minimale Anforderung unabhängigen JSON Darstellung:
    - Eine minimale Darstellung erfordert weniger Speicherplatz im Cache mithilfe der clientseitigen (begrenzt)
    - Eine Darstellung der Anforderung unabhängigen trennt die Daten aus ihrer Daten Quell- und Anforderung Semantik
        - auf diese Weise können Datenquelle auf einfache Weise geändert werden muss (statische, simulierten, live) wie die Lösung entwickelt wurde 
    - JSON ermöglicht die Verwendung von JavaScript-Objekten, die an die benutzerdefinierte clientseitige Anzeigesteuerelemente auf einfache Weise gebunden werden können
        - Dies dient auch den arbeiten Datenvertrag zwischen Teams UX und Daten der definieren

Die Datenantwort in den clientseitigen Cache zu speichern: 

- Speichern Sie die JSON-Darstellung der Datenantwort im lokalen Zwischenspeicher (z. B. Web Storage)
    - Verwenden Sie einen öffentlichen (d. h., lokalen Speicher) Cache für freigegebene Daten (z. B. globale Menü)
    - Verwenden Sie einen privaten (d. h., Sitzung Storage) Cache für persönliche Daten (z. B. Meine Aktien)
- Ablauf der Komponente-spezifischen Werte verwenden, die die Nichtflüchtigkeit des zugehörigen Daten ausgerichtet
    - z. B. globale Menü Daten (30 Minuten), Stock tickerdaten (5 Minuten), etc.
- "Keine Ergebnisse" ist eine Antwort gültigen Daten. Achten Sie darauf, dass Sie es auch speichern
- Stellen Sie sicher, dass die zwischengespeicherte Daten in allen Seiten und Komponenten der Webanwendung mithilfe der clientseitigen verfügbar ist

Nutzen Sie die Client-Side Data Access Layer Framework (weiter unten in diesem Artikel beschrieben), die oben beschriebenen Muster implementiert. Der Datenzugriffsschicht als eine Hauptkomponente von Ihrer insgesamt mithilfe der clientseitigen Framework behandeln, und stellen Sie sicher, dass er für Konsistenz und Leistung von alle mithilfe der clientseitigen Webanwendungen verwendet wird.

### <a name="data-request-apis"></a>Daten Anforderung-APIs
<a name="bk_dataRequestApis"> </a>

Beachten Sie, dass einige Anforderungen mithilfe der clientseitigen Daten in schwerwiegende sich negativ auf den SharePoint-Server auswirken können.

- Vermeiden der Verwendung von Client-seitigen CAML-Abfragen, insbesondere solche, die den Vorversion listet (SOAP) Webdienst abzielen würde 
- Mithilfe der clientseitigen CAML-Abfragen im Allgemeinen umgehen alle serverseitigen Cache-Mechanismen, wodurch negative Server-Leistung bei hoher Auslastung.

Wenn Sie die CAML-Abfragen verwenden müssen, beachten Sie die folgenden Richtlinien:

- Vermeiden Sie ihre Verwendung für große Seiten (z. B. Homepage des Portals)
- Definieren Sie die einfachste und die meisten-effiziente CAML-Abfrage möglichen und überprüfen Sie die Leistung
- Nutzen Sie die Client-Side Data Access Layer Framework (weiter unten in diesem Artikel beschrieben) zum Zwischenspeichern der Datenantwort

Verwenden Sie im Allgemeinen SharePoint-REST-APIs für Anforderungen mithilfe der clientseitigen Daten. Wenn Sie Dateninhalte/Aggregation ausführen, verwenden Sie SharePoint Search-REST-APIs. Optimieren Sie Ihre Suchabfragen um Ausführungszeit und Antwort Größen zu minimieren:

- Beschränken Sie die Verwendung von Platzhaltern
- Zurückgeben nur die Felder, die erforderlich sind (d. h., vermeiden von Select *)
- Grenzwert für die Anzahl der Ergebnisse (d. h., Zeile Grenzen)
- Ziel: mögliche engsten Bereich
- Die Anzahl der Suchabfragen so gering wie möglich zu halten
- Durchführen Sie normale Abfrage Überwachungen redundante/ähnliche konsolidieren fragt, abzielen dieselben Daten

REST-Anforderungen zu SharePoint Online mithilfe der clientseitigen unterliegen jetzt anforderungsdrosselung und sogar Anforderung blockiert. Achten Sie auf die HTTP-Antwort Codes/Warnungen Ihrer Daten Anfragen und ändern Sie Ihre Daten Anforderungsverhalten entsprechend, um Ausfällen in Ihre Webanwendungen mithilfe der clientseitigen Daten zu vermeiden. Finden Sie im Artikel [SharePoint Online-Anforderungsdrosselung](https://msdn.microsoft.com/en-us/library/office/dn889829.aspx) ausführliche Informationen zur Vermeidung gedrosselt oder blockiert werden.

REST-Anforderung Datenverkehr können jetzt über OData Batchverarbeitung optimiert werden.  Finden Sie unter das [OData Batch anfordern Lernprogramm](http://www.odata.org/getting-started/advanced-tutorial/#batch) als auch die [OData Batch anfordern Protokoll Spec](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752313) ausführliche Informationen. Alternativ sollten Sie die Office-Entwicklung Muster und Methoden - [JavaScript (PnP-JS-Core)](https://github.com/SharePoint/PnP-JS-Core) Hauptkomponente, die auch ein [Wrapper](https://github.com/SharePoint/PnP-JS-Core/wiki/Batching) zum Kapseln Batch anfordern Funktionalität bereitstellt.

### <a name="take-advantage-of-free-shipping"></a>Nutzen Sie "Frachtkosten"
<a name="bk_freeShipping"> </a>

Stellen Sie Verwendung der integrierten Funktionen, die automatisch Daten an die Webanwendung mithilfe der clientseitigen, ohne die Notwendigkeit für eine Anforderung für expliziten Daten übermittelt werden kann:

- Verwenden Sie die globale JavaScript-Variable mit dem Namen **SpPageContextInfo**, sofern verfügbar
    - Es ist im globalen JavaScript Namespace von jedem ***klassische*** SharePoint Page enthalten.
    - Es enthält allgemeine Kontextinformationen von der Umgebung mithilfe der clientseitigen beim Laden der Seite 
    - Besteht keine Notwendigkeit zum Tätigen eines Anrufs in SharePoint zum Abrufen dieser Daten beim Laden der Seite
- Verwenden Sie vorinstallierte Informationen aus SharePoint-Framework, wenn Sie mithilfe von modernen Seiten und implementieren eine Anpassung mit SharePoint-Framework
- Verwenden von JavaScript-Dateien zum Speichern von Konfigurationseinstellungen, die von der Webanwendung mithilfe der clientseitigen verwendet
    - Platzieren Sie diese Dateien in Ihre Dateispeicherort der Ressource (z. B. SharePoint Style Library)
    - Verweisen auf diese Dateien als Ressourcendatei in Ihrer Webanwendung mithilfe der clientseitigen JavaScript
    - Browser bieten diese Dateien automatisch in die Clientumgebung, beim Laden der Seite
        - Darüber hinaus wird jeder gespeichert/bedient aus dem lokalen Cache der Internet-Dateien werden 
    - Besteht keine Notwendigkeit zum Tätigen eines Anrufs in SharePoint zum Abrufen dieser Daten beim Laden der Seite

### <a name="resource-files"></a>Ressourcendateien
<a name="bk_resourceFiles"> </a>

Verwenden Sie Ressourcendateien effektiv zur Verbesserung der Leistung Ihrer Client-Side-Webanwendung.

- Verwendet JavaScript/CSS-Dateien allgemeine Skript/CSS übermitteln Inhalt über freigegebenen Seiten und Komponenten. Sie erhalten die gleichen Vorteile für JavaScript-basiertes Konfigurationsdateien oben beschriebenen plus:
    - Entspricht der Precept "Eine Regel, einer Stelle"
    - Vermeidet redundante, eingebettete Skript/CSS-Inhalt
    - Minimiert Seiteninhalt
- Paket (d. h., "minify") zur Reduzierung von deren Größe verbessern die Ressourcendateien Zeiten herunterladen
- Nutzen Sie dynamische Datei Anforderungen an Load zurückstellen optional JavaScript-Dateien, die nur bei Bedarf (d. h., verzögerte Laden)
- Stellen Sie sicher, dass die JavaScript-Dateien in der richtigen Reihenfolge angefordert werden
    - Implementieren Sie Logik, um sicherzustellen, dass die erforderlichen Funktionen vorhanden ist 
- Nutzen Sie Sprites Bild, um die Anzahl der Bilddateien zu reduzieren, die heruntergeladen werden müssen
- Nutzen von Bilddarstellungen in SharePoint für die optimale Bild Einschränkungen für allgemeine Bild definieren verwenden Sie Groß-/Kleinschreibung Szenarien (z. B. Miniaturansicht, Textlinks, Rollup usw.) 

### <a name="content-delivery-network-cdn"></a>Content Delivery Network (CDN)
<a name="bk_cdn"> </a>

Content Delivery Network (CDN) ist ein geografisch verteilte-Netzwerk, mit dem einen Endbenutzer eine bestimmte Ressource-Datei aus dem engsten CDN-Speicherort abrufen kann.  Verwendung von ein CDN bessere Downloadzeiten erzeugt und trägt zu einer verbesserten Wahrnehmung der Seite Leistungseinbußen.

- Nutzen der vorhandenen Content Delivery Networks Übermitteln von Drittanbieter-Client-Side-Frameworks (z. B. jQuery, Bootstrap, Knockout, AJAX, usw..)
- Berücksichtigen Sie eine Content Delivery Network (CDN) Ihre benutzerdefinierten Ressourcendateien übermitteln
    - [Azure CDN](https://azure.microsoft.com/en-us/services/cdn/)
    - [Office 365 öffentliches/privates CDN](https://dev.office.com/blogs/general-availability-of-office-365-cdn)
    - SharePoint Portal Style Library - Standardoption, wenn ein CDN nicht verwendet wird

> [!NOTE] 
> Die [Office 365 private CDN-Funktion](https://dev.office.com/blogs/general-availability-of-office-365-cdn) verfügt über eine Veröffentlichung Feature automatische Umschreiben von URLs zu Urls CDN. Also nach der Aktivierung von privaten CDN wird SharePoint Ihrer Veröffentlichungsseiten mit Links zu Ihrem privaten CDN Standort ohne Sie als Entwickler müssen dies erstellt zeigen zurückgegeben. Dies gilt für Veröffentlichungsseiten, aber auch für Daten, die von den Inhalt von Such-Webparts, die Bibliothek Bildschirmpräsentation mit Bildern, Bildfelder in SPList-REST-Abfragen und SharePoint-bilddarstellungen zurückgegeben. Ihre Veröffentlichungsportal kann auch privaten und öffentlichen CDN im gleichen Portal kombinieren.

### <a name="ajax"></a>AJAX
<a name="bk_ajax"> </a>

Asynchrone JavaScript und Xml (AJAX) können eine Webanwendung mithilfe der clientseitigen, Hintergrund Daten Anforderungen in einer Weise auszuführen, die keine ganze Seite Last erforderlich sind.
 
Zur Hervorhebung steht "**A**" in AJAX für "**asynchrone**"; Es wird empfohlen, um sie auf diese Weise zu machen. Es ist, zwar möglich, synchrone Aufrufe im AJAX ausgeführt werden ist es selten sollten Sie dies tun. 

- Nie führen Sie synchrone AJAX-Aufrufe aus; der Browser wird blockiert, bis der Anruf abgeschlossen ist, wodurch benutzerfreundlich

Die Notwendigkeit für einen synchronen Aufruf entsteht in der Regel aufgrund einer Abhängigkeit in den Ablauf der Daten an. Analysieren des Datenfluss der Anforderung zur Entwurfszeit und eliminieren (oder mindestens reduzieren) die Reihenfolge Abhängigkeit. Abwehren von den Auswirkungen von Abhängigkeiten, die durch Verketten der Erfolg-Ereignishandler der asynchronen Daten Anforderungen verbleiben. 

### <a name="javascript"></a>JavaScript
<a name="bk_javaScript"> </a>

Der Ausführungsphase JavaScript ist den letzten Teil der gesamten Seite Load Sequenz.  Während dieser Phase führt alle JavaScript erforderlich sind, um alles verknüpfen, und stellen Sie die endgültige gerenderte Seite für dem Benutzer im Browser aus.

Schlecht implementiert JavaScript kann weiterhin, auch wenn Ihre Webanwendung mithilfe der clientseitigen folgt aller der Anleitung zum Anfordern der Webseite ihrer Ressourcendateien und Ausführen aller Datenanfragen benutzerfreundlich, führen.

Umfassende Leistungsrichtlinien für JavaScript sind außerhalb des Bereichs des in diesem Artikel. Wir zusammenfassen jedoch einige der wichtigsten Konzepte:

- Beschränken von Updates auf das Modell DOM (Document Object)
- Effizientes Verwenden von Schleifenstrukturen
- Beschränken Sie die Verwendung von Try/Catch in Segmente critical-code
- Verwenden Sie die korrekten Bereichs für Variablen

Finden Sie in den folgenden Artikeln fundierte Richtlinien auf die JavaScript-Leistung: 

- [JavaScript-Muster und Leistung](https://msdn.microsoft.com/en-us/pnp_articles/javascript-patterns-and-performance)
- [Office Dev Plug & Play-veranstaltet – JavaScript Leistungsaspekte mit SharePoint](https://dev.office.com/blogs/javascript-performance-considerations-with-sharepoint)

### <a name="high-volume-pages"></a>Große Seiten
<a name="bk_highVolumePages"> </a>

Achten Sie besonders für den Entwurf und Implementierung umfangreicher Seiten innerhalb der Webanwendung mithilfe der clientseitigen.

Eine typische umfangreicher Seite ist die Homepage des Portals.  Erwägen Sie das Szenario die Corporate IT-Abteilung von einem großen Unternehmen (50.000 Benutzer) beschließt, ein Gruppenrichtlinienobjekt (GPO) implementieren, die zum Öffnen der Homepage des Portals standardmäßig alle Desktopbrowser erzwingt. Die Leistung der Homepage des Portals entscheidend geworden.  Wenn Ihre Erstentwurfs nicht dieser Umfang des Datenverkehrs bedenken, konnte das Portal einer deutlichen Beeinträchtigung der Systemleistung auftreten.

- Vermeiden der Verwendung von Inhaltsabfragen-Webparts auf der Seite; bevorzugen Sie Inhalt-nach-Such-Webparts stattdessen
- Begrenzen Sie und Optimieren Sie, die Anzahl der clientseitigen Datenanfragen einstufen der Seite
- Sicherstellen Sie, dass ordnungsgemäße mithilfe der clientseitigen Zwischenspeichern wiedergeben für Anforderungen mithilfe der clientseitigen Daten
- Die Seite "aufteilen"
    - Limit-Startseite nur die obere Hälfte Verarbeitung (d. h., der erste Abschnitt) auf der Seite
    - Scroll-Ereignisse verwenden die Verarbeitung der zusätzliche Abschnitte der Seite wie des Benutzers ausgelöst wird nach unten verschoben.
- Beschränken Sie die Menge der Daten in den benutzerdefinierten Steuerelementen Hervorhebung (z. B. Fallstudie) und Rollups (z. B. Top 3 News Verknüpfungen) gerendert 
    - Geben Sie "**Weitere...**" Links zu redirect Users to geringem Volumen Projektdetailseiten, in dem erweiterten Inhalt mit weniger allgemeine Auswirkungen auf das Portal angezeigt werden kann,

## <a name="client-side-data-access-layer-dal-framework"></a>Client-Side Data Access Layer (DAL) Framework
<a name="bk_dal"> </a>

Das Client-Side Data Access Layer (DAL) Framework ist eine benutzerdefinierte clientseitige JavaScript-Frameworks, die Sie implementieren und alle benutzerdefinierten clientseitigen Anzeigesteuerelemente Ihrer Client-seitigen Webanwendungen zur Verfügung stellen.  Es unterstützt intelligent Datenladevorgänge-Muster, abstrahiert die Details der Client-zu-Server-Anforderungen, bietet Funktionen für die Client-zu-Server-Datenverkehr zu minimieren das Zwischenspeichern von Daten und deutliche Verbesserung der Seite wahrgenommenen Leistung.

Es gibt eine Reihe von Client-seitigen JavaScript-Frameworks und Bibliotheken, die Sie zum Implementieren der DAL nutzen können. Wählen Sie eine, mit denen Sie am besten vertraut sind und die folgenden Grundsätze entsprechen.  Verwenden Sie die logische Architektur, die als Vorlage für die Implementierung der nachstehend vorgeschlagenen.

Die **Client-Side Data Access Layer (DAL) Beispiel** stellt eine funktionsfähige Verweis Implementierung von Client-Side Data Access Layer (DAL) Framework bereit. Sie können das Beispiel auf GitHub zuzugreifen:

- [Client-Side Data Access Layer (DAL) Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer)

### <a name="architectural-tenets"></a>Architektonische Grundsätze
<a name="bk_dalTenets"> </a>

- Leistung ist Feature #1
- Hauptkomponente von insgesamt mithilfe der clientseitigen framework
    - Um alle benutzerdefinierten mithilfe der clientseitigen Webanwendungen und Komponenten für Konsistenz und Leistung genutzt werden
- Erfüllen von Datenanfragen über Datencache mithilfe der clientseitigen; Wenn einem Cachefehler auftritt, Ausführen der Fetch-Client-zu-Server-Daten
- Rufen Sie die Serverdaten über einen asynchronen Aufruf für Client-zu-Server-AJAX (nie verwenden einen synchronen Aufruf)
- Reduzieren Sie Fehler beim Aufrufen eines cascading, indem Sie veraltete Daten wiederverwenden, falls eine Anforderung Daten fehlschlägt
- Anforderungssteuerung Antworten berücksichtigt und Verhalten entsprechend anpassen
- Speichern Sie die Antwort vom Server Daten im mithilfe der clientseitigen Cache über eine minimale, Anforderung unabhängigen JSON-Darstellung
- Vorübergehende und zuverlässige Supportoptionen
- Verwenden von temporärer Speicher für persönliche Daten und dauerhaften Speicher für freigegebene Daten
- Unterstützung der absoluten und gleitenden Ablaufrichtlinien
- Ermöglichen Sie jeden Speicher-Eintrag so konfigurieren Sie eine eigene Speicheroptionen für Speicher (vorübergehende/dauerhaft), Ablaufrichtlinie (Absolute/sliding) und Ablauftimeout (in Minuten)
- Permanente Überwachung von Leistung über die Protokollierung und Telemetrie zur Laufzeit 
- Überprüfen Sie kontinuierlich Data Flow Szenarien/Sequences, um sicherzustellen, dass jedes optimierte für allgemeine Seite Leistung und Reaktionsfähigkeit bleiben

Das folgende Diagramm veranschaulicht die logische Architektur von Client-Side Data Access Layer (DAL) Framework:

![Data Access Layer logische Architektur](./media/logicalDataAccessLayer.png)

### <a name="major-components"></a>Hauptkomponenten
<a name="bk_dalComponents"> </a>

Die logische Architektur von der Datenzugriffsschicht (Data Access Layer, DAL) Framework umfasst die folgenden Komponenten:

- JavaScript-basierten Komponenten
    - Diese Steuerelemente nutzen intelligent Data Access Muster (z. B. verzögerte Laden) und Modell DOM (Document Object) Ereignisse, um sicherzustellen, dass Daten Anforderungen sind so lange zurückgestellt und initiiert nur bei Bedarf (z. B., warten Sie, bis eine reduzierte Menüs erweitert ist)
    - Anzeigesteuerelemente können Statusindikatoren präsentieren, während des Flugs Datenanfragen werden
- Ereignisbasierte Datenanfragen
    - Diese Ereignishandler an Ereignisse Steuerelements oder der Seite gebunden sind und Aufrufen Datenzugriffsmethoden ausgelöst
- Business Data Manager
    - Bietet Business Data Objects (BDOs) für die Verwendung durch die Anzeige-Komponenten
    - Logische Datenzugriffsmethoden, die die zugrunde liegenden Datenquellen abstrakten enthält
    - Böffnen Daten können ein Mock, einen mithilfe der clientseitigen Cache oder der tatsächlichen Datenquelle stammen.
- Externe Dienste
    - Zugriff auf serverseitige APIs bieten (d. h., Back-End) Daten
    - Enthält SharePoint Online, Drittanbieter-Datendienste, benutzerdefinierten Datenquellen und Anwendungen (engl.)
- Storage-Manager
    - Bietet mithilfe der clientseitigen Datencache Semantik, Dauerhaftigkeit (vorübergehende oder dauerhafte), Dauer (Timeout für Ablauf) und Gruppenrichtlinien (absoluten oder gleitenden)
    - Webspeicher ermöglicht die Clientumgebung zum Speichern von temporäre Daten (Sitzung Storage) und langfristige Daten (lokaler Speicher)
        - Sitzungsinformationen unterstützt das Zwischenspeichern von vertraulichen Daten
        - Lokaler Speicher unterstützt das Zwischenspeichern von freigegebenen Daten
    - Unterstützung von Cookies kann hinzugefügt werden, zu einer anderen mithilfe der clientseitigen Speicheroption bereitzustellen, wenn benötigt
    - Bereitstellung von Daten aus einem clientseitigen Cache verringert die Anforderungen an die aktuelle Datenquelle und verbessert die Leistung der Seite

### <a name="typical-call-sequence"></a>Typische Aufrufsequenz
<a name="bk_dalCallSequence"> </a>

1. Ein Ereignis (implizit oder explizit) auftritt in den Clientbrowser
2. Die Anzeige Komponente bestimmt, dass zum Rendern von Daten angefordert werden muss
3. Die Anzeige Komponente fordert seine zugeordneten Business Data Object (Böffnen) aus dem Business Data-Manager 
    - Optional können Sie zeigt eine Statusanzeige die Anzeige-Komponente, während die Anforderung ausgeführt wird
4. Die Business Data Manager berechnet den Speicherschlüssel und bestimmt die Speicheroptionen für die Böffnen
5. Die Business Data Manager fordert die Böffnen pro Speicheroptionen aus dem Speicher-Manager
    - Wenn die Böffnen vorhanden und aktuell ist, ein Cachetreffer tritt auf, und der Speicher-Manager gibt den Böffnen (Weiter mit Schritt 10)
    - Ist die Böffnen abwesend oder veraltete, einem Cachefehler tritt auf, und der Storage Manager gibt keine Böffnen (Weiter mit Schritt 6)
6. Die Business Data Manager sendet eine (asynchrone) Anforderung an den externen Dienst für die aktuelle Daten
    - Wenn die Anforderung ein Fehler auftritt, der Business Data Manager **erneut verwendet** veraltete Böffnen *falls vorhanden* (Weiter mit Schritt 9)
    - Wenn die Anforderung erfolgreich ist, verarbeitet die Business Data Manager die aktuelle Daten-Antwort (Weiter mit Schritt 7)
7. Die Business Data Manager erstellt die Business Data Object (Böffnen)
8. Die Business Data Manager füllt die Böffnen mit neuen Daten
9. Die Business Data Manager fragt Storage-Manager zum Speichern der Böffnen pro Speicheroptionen 
10. Die Business Data Manager gibt die Böffnen für die Anzeige-Komponente
11. Die Komponente für die Anzeige bindet an den Böffnen und rendert die Daten

## <a name="see-also"></a>Siehe auch
<a name="bk_additionalResources"> </a>

- [Client-Side Data Access Layer (DAL) Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer)
- [Einführung in die Leistungsoptimierung für SharePoint Online](https://support.office.com/en-US/article/Introduction-to-performance-tuning-for-SharePoint-Online-81c4be5f-327e-435d-a568-526d68cffef0)
- [Optimieren der Leistung von SharePoint Online](https://support.office.com/en-us/article/Tune-SharePoint-Online-performance-f0522d4a-fbf4-41f9-854e-c9b59555091d)
- [Office-Entwicklungsmustern und Methoden (Plug & Play-) JavaScript-Core](https://github.com/SharePoint/PnP-JS-Core)
- [Informationen Sie zum Erstellen einer schnellen, schnell SharePoint Portal in SharePoint Online](https://channel9.msdn.com/Events/Ignite/2016/BRK3026)
- [Client-Side Data Access Layer (DAL) Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer)