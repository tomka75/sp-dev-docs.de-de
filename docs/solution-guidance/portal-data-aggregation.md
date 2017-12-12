---
title: "Bewährte Methoden für SharePoint Online-Portale - Content-Zusammenführung"
ms.date: 11/03/2017
ms.openlocfilehash: b78cad9e673d28d38f8c160020c4bd0ae33de7df
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="proven-practices-for-sharepoint-online-portals---content-aggregation"></a>Bewährte Methoden für SharePoint Online-Portale - Content-Zusammenführung

Jedes Portal Entwurf umfasst eine Reihe von Anzeigekomponenten, die dynamisch Suchen von Inhalten für die Anzeige auf Portalseiten.  Grundlegende für den Betrieb des diese Steuerelemente ist das Konzept der Inhalte Aggregation, die für die Zwecke dieses Artikels, den wir für den Prozess Suchen von dynamisch festlegen Inhalte zur Laufzeit gewünscht. Das Verfahren, das Sie zum Ausführen von Aggregation auswählen kann erhebliche Auswirkungen auf die Leistung Ihres Portals und die dazugehörigen Seiten haben.

> [!NOTE] 
> Obwohl dieser Anleitung in erster Linie SharePoint Online bezieht, die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet.

_**Gilt für:** SharePoint Online_

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a>Anti-Muster (also nicht sollten Sie folgende Aktionen)
<a name="bk_antiPatterns"> </a>

Wenn Sie Probleme mit Ihrem Portal im Allgemeinen und Ihre Datenaggregation insbesondere haben möchten, sollten Sie die folgenden Anti-Muster:

- Verwenden Sie die "in Echtzeit" Content Aggregation Technik, wann und wo möglich
- Platzieren Sie zwölf oder mehrere Content Aggregation schlecht entwickelte Steuerelemente umfangreicher Portalseite (z. B. "Homepage")
- Verwenden Sie ein Gruppenrichtlinienobjekt (GPO) So erzwingen Sie allen Browsern die problematische Portalseite standardmäßig geladen werden
- Erzwungen Sie Grenzwerte für die Ergebnisse von Aggregation Zeile nicht
- Führen Sie die Ergebnisse von Aggregation nicht zwischengespeichert
- Ziel der Vorversion listet (SOAP)-Webdienst
    - zusätzliche Probleme möglich ist übergeben sie einige schlecht entwickelte CAML-Abfragen

## <a name="content-aggregation-defined"></a>Content-Sammlung definiert
<a name="sectionSection0"> </a>

Es ist wichtig, dass eine klare Definition der Content-Sammlung für den Kontext des Artikels einrichten.

>**Aggregation der Inhalte** das Konzept der dynamisch suchen und Abrufen von Inhalten für die Anzeige auf der aktuellen Seite, wenn dieser Inhalte ausreichend Abstand zu platzieren der aktuellen Seite in einem oder mehreren Standorten innerhalb des Portals vorhanden ist
>
>- Content-Sammlung umfassen nicht innerhalb der aktuellen Seite übersetzende Inhalte
>- Content-Sammlung dient hauptsächlich für die Front-End-User-Ansicht des Portals (im Gegensatz zu den Back-End-Admin-Ansicht)

Hier sind einige gängige Beispiele in der Aggregation verwendet wird:

- Die Portal-Homepage enthält ein Neuigkeiten-Steuerelement, das eine Liste mit Links zu den jüngsten Artikeln im Portal veröffentlicht rendert
- Portalseiten enthalten ein globale Navigation-Steuerelement, das innerhalb einer benutzerdefinierten SharePoint-Liste verwaltete Navigationslinks rendert

## <a name="the-problem-with-the-real-time-content-aggregation-requirement"></a>Das Problem mit der Anforderung in Echtzeit Content-Sammlung
<a name="sectionSection1"> </a>

>**Real-Time Inhalte Aggregation** - sofort mit einer Quelle Content Aggregation vorgenommenen Änderungen werden in dieser Quelle targeting Content Aggregation-Steuerelemente

Es folgen einige Beispiele, in denen Sie dafür, dass der in Echtzeit Content Aggregation wahrscheinlich auftreten kann:

- Ein Inhaltsautor einen Artikel veröffentlicht und erwartet, dass die Verknüpfung zum sofort in das Steuerelement Neuigkeiten der Portal-Homepage angezeigt
- Ein Portal Admin Fügt eine Verknüpfung zur Liste globalen Navigation und erwartet sofort in der globalen Navigations-Steuerelement angezeigt werden soll

Natürlich ist es eine Klasse von dringende Informationen, die absolute, Real-Time Verteilung ist erforderlich vorhanden. ein Veröffentlichungsportal darf jedoch nicht die Wahl für die ***anfängliche*** Verteilung solcher dringende Informationen sein. Eine Reihe von anderen Systemen (Mobilfunk, Radio, Satelliten, verbringt, Sirenen, Alarmen, Lautsprecher usw.) eignen sich besser für diese Aufgabe. Das Portal eignet sich besser für die Verteilung der Kontext, Weitere Informationen und Details; durch Ableitung muss dieser Verteilergruppe nicht in Echtzeit auftreten.

Berücksichtigen Sie mit diesen Kontext berücksichtigen diese zugegebenermaßen Provokative Anweisung:

- **Es ist kein Portal Inhalt wichtig genug ist, um die Kosten für Content-Zusammenführung in Echtzeit zu rechtfertigen**

Leider ist die Standardposition des nahezu jedes Portal Content Management-Team, sogar den am häufigsten profanen Inhalt als dringende und der Echtzeit Content Aggregation berücksichtigt werden sollten. 

Hierin liegt die Herausforderung für die Portal-Architekt: Führen Sie diesen Druck Opfer und das Risiko Portal Leistung beeinträchtigt, oder führen Sie andernfalls verleiten und bieten eine leistungsstarke Portal? Wir empfehlen Ihnen, sie andernfalls verleiten.

In gewissem Sinne strict ist absolute "in Echtzeit" Content Aggregation technisch nicht möglich, in *eine beliebige* Publishing-System. Selbst wenn Sie das Standardverhalten von der Veröffentlichungsportal entsprechen, treten Verzögerungen/Zwischenspeichern an verschiedenen Stellen in der Pipeline Aggregation/Rendering des Inhalts; einen Teil davon ist sichtbar und konfigurierbar (z. B. benutzerdefinierte mithilfe der clientseitigen Cache, serverseitige Ausgabecache, Objektcache serverseitige) und einen Teil davon ausgeblendete und unveränderlich ist (z. B. database Abfrage-Pläne, interne Anwendung Zwischenspeicher usw..).

Inhaltsautoren sind in der Regel nur Personen, die Content Aggregation Verzögerungen beachten. Der Endbenutzer hat keine Forderung in Echtzeit Content Aggregation seinen mangelnde Einblicke in den Prozess Content-Veröffentlichung.

Sobald eine akzeptiert, dass "in Echtzeit" Content Aggregation auftreten, ist nicht möglich, sind alle diese bleibt die Aushandlung:

- wie lange sind Sie bereit sind, finden in den Inhalten zu warten?
- wie viel sind Sie bereit sind, auf den Inhalt etwas schneller finden Sie unter "Zahlen"?

Content-Sammlung Verzögerungen sind in einer gut funktionierende Portal Lösung lässt. auf eine akzeptable Verzögerung gefährden und die Portal-Benutzer, vielen Dank.

> Hinweis, die, obwohl Content-Sammlung in Echtzeit in sicherlich nicht möglich Fällen, kann absolut beispielsweise benutzerdefinierte Warn-Funktion mit einem Timeout von 5 Minuten und News Aggregation mit einem Timeout von einer Stunde verfügen. Dies wäre keine Echtzeit Content Aggregation, aber würde als eine Echtzeitaggregation von den meisten die Endbenutzer fast betrachtet. 

## <a name="content-aggregation-techniques"></a>Content-Sammlung Techniken (engl.) 
<a name="sectionSection2"> </a>

In den folgenden Abschnitten werden die zwei Content Aggregation-Verfahren für SharePoint Online beschrieben.

**Es wird empfohlen, Content Aggregation CAML-basierten Content Aggregation suchbasierte vorzuziehen.**

### <a name="caml-based-content-aggregation"></a>CAML-basierte Content-Zusammenführung

Diese Vorgehensweise CAML-basierten Content Aggregation basiert auf die Verwendung von Collaborative Application Markup Language (CAML) Abfragen. 

Eine kann CAML-Abfragen erstellen und verwenden sie zum Ausführen von Aggregation Operations in SharePoint. Die Abfragen werden für die SharePoint-Inhaltsdatenbanken ausgeführt. CAML-Abfragen sind in der Implementierung der serverseitige Steuerelemente, wie zum Beispiel das Out-of-Box (OOB) Inhalt-nach-Abfrage-Webpart integrierten. CAML-Abfragen können auch direkt für die verschiedenen Content-Erkennung für benutzerdefinierte clientseitige JavaScript-Steuerelemente verfügbaren-APIs verwendet werden.

Der Hauptvorteil der CAML besteht darin, dass es nahe kommen ermöglicht wie möglich, um "in Echtzeit" Content Aggregation erreichen. Der primäre Nachteil CAML ist, dass sie Kenntnisse und Fertigkeiten zum Entwerfen von gut funktionierende CAML-Abfragen benötigt. eine scheinbar harmlose Änderung kann dazu führen, in einer schlechter CAML-Abfrage und/oder eine Endlosschleife Reihe von Cachefehlern, die Auswirkungen von denen nicht ersichtlich ist, bis das Portal bei starker ist.

Durch die Bereitstellung von benutzerdefiniertem Code untersagt, SharePoint Online wurde ausgeschlossen, was in der Vergangenheit der einzelnen schlechtesten Kategorie des SharePoint-Leistungskiller hat: benutzerdefinierte serverseitige Steuerelemente und Webparts, die schlecht entwickelte CAML-Abfragen zu nutzen. Es ist jedoch weiterhin die Möglichkeit, Missbrauch CAML sowohl über die OOB Inhalt-nach-Abfrage-Webparts als auch über benutzerdefinierte clientseitige JavaScript-Steuerelemente. Beachtet werden: 

- Jeder Anforderung mithilfe der clientseitigen CAML führt zu einer direkten Datenbankabfrage
    - Mithilfe der clientseitigen CAML Ergebnisse sind nicht auf dem Server zwischengespeichert.
    - CAML-Anforderungen mithilfe der clientseitigen Treffer den Datenbankserver für die Ausführung (einem Cachefehler tritt immer)
- Jeder Server-Side CAML-Anforderung ist gefährdet der sind somit eine direkte Datenbankabfrage
    - Serverseitige CAML Ergebnisse werden auf dem Server, basierend auf ähnliche Benutzer Berechtigungssätze zwischengespeichert.
    - Abfragen, die Personalisierung Felder enthalten, werden nie zwischengespeichert.
    - Serverseitige CAML-Anforderungen Treffer den Datenbankserver für die Ausführung tritt einem Cachefehler
    - Einem Cachefehler ist einer in der Nähe-Sicherheit in Farmen mit einer großen Anzahl von Web-Front-ends

**Es wird empfohlen, dass Sie vermeiden, dass die CAML-basierten Content Aggregation, wenn möglich.**

Wenn Sie Inhalte Aggregation CAML-basierte verwenden müssen, beachten Sie die folgenden Richtlinien:

- Vermeiden Sie die Verwendung für große Seiten
- Beschränken Sie die Verwendung einer bestimmten Klasse von Inhalten (z. B. Benachrichtigungen)
- Definieren Sie die einfachste und die meisten-effiziente CAML-Abfrage möglichen und überprüfen Sie die Leistung
- Implementieren Sie indizierte Spalten für die Ziellisten
- Grenzwerte für die Abfrage Zeile enthalten
- Sicherstellen Sie, dass benutzerdefinierte clientseitige JavaScript-Steuerelemente geben Sie eine **Weitere** Verknüpfung zum Umleiten von Benutzern zu einer Seite der geringem Volumen alles anzeigen 
- Stellen Sie sicher, dass benutzerdefinierte clientseitige JavaScript-Steuerelemente Client-Side Data Access Layer Framework zum Zwischenspeichern der Content Antwort nutzen
    - "Keine Ergebnisse" ist eine gültige Antwort und sollten auch zwischengespeichert werden
- Erzwingen einer clientseitigen Cache Ablauf nicht weniger als 5 Minuten

Finden Sie im [Artikel Portal Leistung](portal-performance.md) für Weitere Informationen zu den clientseitigen Datenzugriffsschicht.

### <a name="search-based-content-aggregation"></a>Suchbasierte Inhalte Aggregation

Diese Vorgehensweise suchbasierte Inhalte Aggregation basiert auf die Verwendung von SharePoint Search Keyword Query Language (KQL) Abfragen. 

Eine kann Suche KQL-Abfragen erstellen und verwenden sie zum Ausführen von Aggregation Operations in SharePoint. Die Abfragen werden für die SharePoint-Suchindex ausgeführt. Suche KQL-Abfragen sind in der Implementierung der serverseitige Steuerelemente, wie zum Beispiel Out-of-Box (OOB) Inhalt-nach-Suchwebparts integrierten. KQL-Abfragen können auch direkt für die benutzerdefinierte clientseitige JavaScript-Steuerelemente zur Such-APIs verwendet werden.

Der Hauptvorteil der suchbasierte Inhalte Aggregation ist, dass sie den SharePoint-Suchdienst nutzt die außergewöhnliche Leistung in einer großen Skalierung bei starker anzugebende integriert ist. Der primäre Nachteil der suchbasierte Inhalte Aggregation ist die Abhängigkeit der Suchindex, was, dass es wird eine kurze Verzögerung sein bedeutet, bevor Änderungen Inhalte im Suchindex angezeigt werden.

Beachtet werden: 

- Portalinhalt muss gecrawlt und dem Suchindex hinzugefügt, um Daten suchbasierten Aggregation verfügbar gemacht werden 
- SharePoint crawlt kontinuierlich Portal-Inhalt, um eine auf dem neuesten Stand Suchindex zu gewährleisten.
    - Es werden jedoch eine kurze Verzögerung bevor inhaltlichen Änderungen im Index angezeigt werden.
- Das Suchschema muss konfiguriert werden die gewünschten Inhalten Eigenschaften über Suche gefunden werden

**Es wird empfohlen, dass Sie suchbasierte Inhalte Aggregation bevorzugen.**

Wenn Sie suchbasierte Inhalte Aggregation verwenden, beachten Sie die folgenden Richtlinien:

- Stellen Sie sicher, dass Ihre Content Management-Teams, dass Inhalte verstehen müssen gecrawlt werden, bevor es aggregiert werden kann
    - Einrichten der erwarteten die Verzögerung Content-Sammlung 
- Konfigurieren der erforderlichen Suchschema
    - Wählen Sie einen passenden Bereich (Mandant, Websitesammlung oder Web)
    - Trigger die automatische Generierung von durchforsteten und verwalteten Eigenschaften
    - Nutzen der Out-of-Box-Platzhalter für verwaltete Eigenschaften (z. B. RefinableInt01) Wenn Sortieren/verfeinern benötigt wird
- Entwerfen der entsprechenden Ergebnisquellen und Abfragen
    - Ziel: einzelne Listen, Webs oder Websites nach Bedarf
    - Ziel-einzelne Inhaltstypen
    - Ziel-bestimmte verwaltete Eigenschaften (d. h., Websitespalten)
- Wählen Sie die gewünschte Anzeigesteuerelemente:
    - OOB-Steuerelemente: 
        - Verwenden Sie die Inhalte von Search Webparts
        - Zurückgeben der minimale Zeilen und Spalten, die benötigt
        - Entwickeln Sie die erforderlichen Anzeigevorlagen
        - Aktivieren Sie bei Bedarf asynchrones clientseitiges rendering
    - Benutzerdefinierte Steuerelemente:
        - Benutzerdefiniertes, clientseitiges JavaScript Anzeige-Steuerelemente verwenden, die die Such-REST API verwenden
        - Zurückgeben der minimale Zeilen und Spalten, die benötigt
        - Achten Sie darauf, Client-Side Data Access Layer Framework zum Zwischenspeichern der Antworten zu nutzen.

Finden Sie im [Artikel Portal Leistung](portal-performance.md) für Weitere Informationen zu den clientseitigen Datenzugriffsschicht.

## <a name="see-also"></a>Siehe auch
<a name="bk_additionalResources"> </a>

- [Leitfaden zur Portal Leistung](portal-performance.md)