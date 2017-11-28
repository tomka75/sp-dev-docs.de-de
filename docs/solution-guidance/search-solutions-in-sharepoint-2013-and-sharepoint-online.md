---
title: "Suchlösungen in SharePoint 2013 und SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 549e899fb3f4994442040b0699ce1367bbdf787a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="search-solutions-in-sharepoint-2013-and-sharepoint-online"></a>Suchlösungen in SharePoint 2013 und SharePoint Online

Mehr über die SharePoint-Sucharchitektur, Such-APIs und Suche-Add-Ins erfahren.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Suche in SharePoint 2013 kombiniert einfache Konfiguration und Bereitstellung mit der Skalierbarkeit und Erweiterbarkeit von FAST Search-Server auf einer einzelnen Enterprise Search-Plattform.

SharePoint 2013 enthält gängiger Muster in der Suche-Plattform, die Sie Anpassen der Suche für die verschiedenen Szenarien unterstützen. Beispiel:

- Video-Suche, und suchen Sie Unterhaltung sind als Out-of-Box- [Suche Optionen](https://technet.microsoft.com/en-us/library/dn794227.aspx)enthalten.
    
- Thema Seiten und Inhalte von der Suche Web Content Management-Funktionen und Szenarien wie etwa Websites suchbasierte und Knowledge Management-Websites zu verbessern.
    
- Meine Aufgaben bündelt Projektvorgängen, damit Benutzer an mehreren Standorten an einem zentralen Speicherort, ihre OneDrive for Business-Site zugewiesene Aufgaben nachverfolgen können.

## <a name="sharepoint-2013-search-architecture"></a>SharePoint 2013-Sucharchitektur

Die Sucharchitektur in SharePoint 2013 enthält Komponenten und Datenbanken, die zusammenarbeiten. 

**Suchkomponenten in SharePoint 2013**

|**Komponente**|**Beschreibung**|
|:-----|:-----|
|Durchforsten |Durchforstet Inhaltsquellen, um Eigenschaften und Metadaten zu sammeln und sendet diese Informationen an die inhaltsverarbeitungskomponente.|
|Inhaltsverarbeitung |Überträgt die durchforsteten Elemente und sendet sie an die Indexkomponente. Diese Komponente ordnet auch gecrawlte Eigenschaften verwalteten Eigenschaften.|
|Verarbeitung der Verwendungsanalyse |Führt Such-und Verwendungsanalysen.|
|Index |Empfängt die verarbeiteten Elemente von der inhaltsverarbeitungskomponente und schreibt sie in den Suchindex. Diese Komponente auch eingehende Abfragen verarbeitet, ruft die Informationen aus dem Suchindex und sendet das Resultset auf abfrageverarbeitungskomponente.|
|Abfrageverarbeitung |Analysiert eingehende Abfragen. Dadurch wird die Genauigkeit, Rückruf und Relevanz zu optimieren. Die Abfragen werden an die Indexkomponente gesendet, die eine Gruppe von Suchergebnissen für die Abfrage zurückgibt.|
|Verwalten der Suche |Führt die Systemprozesse für die Suche aus, fügt neue Instanzen von Suchkomponenten hinzu und initialisiert diese anschließend.|

**Suchdatenbanken in SharePoint 2013**

|**Datenbank**|**Beschreibung**|
|:-----|:-----|
|Durchforsten |Speichert Informationen und Verlaufsinformationen zu durchforsteten Elemente wie Dokumente und URLs nachverfolgen. Sie speichert auch Informationen wie dem Zeitpunkt der letzten Durchforstung, die letzte Crawl-ID und den Typ der Aktualisierung (hinzufügen, aktualisieren und löschen) während der letzten Durchforstung.|
|Link |Speichert nicht verarbeitete Informationen, die von der inhaltsverarbeitungskomponente Komponente und Informationen zur Suche extrahiert wird klickt. Die analyseverarbeitungskomponente analysiert diese Informationen.|
|Analyseberichtsdatenbank |Speichert die Ergebnisse der Verwendungsanalyse.|
|Verwalten der Suche |Speichert die Suchkonfigurationsdaten.|

### <a name="crawl-and-content-processing"></a>Durchforstung und inhaltsverarbeitung

Der Crawlvorgang beginnt mit den unterschiedlichen Inhaltsquellen (beispielsweise HTTP, Dateifreigaben und SharePoint). Für Inhalt, den Index hinzugefügt werden soll verwendet der Crawler Connectors, die dem Crawler mit, wie Sie eine Verbindung mit der Inhaltsquelle und Zugreifen auf die Inhaltselemente innerhalb der Quellwebsitesammlung. Wenn der Crawler die Inhaltselemente gefunden hat, verwendet eine entsprechende formathandler, um den Inhalt zu analysieren.

Nach dem Abrufen des Inhalts, durchforstet der Durchforstung Komponente übergibt Elemente an die inhaltsverarbeitung-Komponente, die verarbeitet die Elemente und sendet sie an die Indexkomponente. Dazu gehören Dokumentanalyse Zuordnen von durchforsteten Eigenschaften auf die zugeordnete verwaltete Eigenschaften und linguistikverarbeitung, wie etwa Sprache Erkennung und Entität Extraction. Die inhaltsverarbeitungskomponente schreibt auch Informationen zu URLs und Links auf den linkdatenbank.

### <a name="query-processing"></a>Abfrageverarbeitung

Analysiert die abfrageverarbeitungskomponente, und Prozesse Suchabfragen um Genauigkeit, Rückruf und Relevanz, einschließlich der Durchführung der linguistischen Verarbeitung wie Word knacken und wortstammerkennung zu optimieren. Die verarbeitete Abfrage dann weitergeleitet an die Indexkomponente, die ein Resultset basierend auf der verarbeiteten Abfrage an die abfrageverarbeitungskomponente zurückgibt, die aktivieren in Prozesse, die Set führen.

### <a name="search-analytics"></a>Suchanalyse

SharePoint analysiert sowohl den Inhalt, sich selbst (suchanalyse) und auch die Möglichkeit, die Interaktion von Benutzern mit (Verwendungsanalyse) und verwendet diese Informationen, um die Suche zu verbessern.

Suchanalyse ist zum Extrahieren von Informationen, wie Links, die Anzahl der, wie oft, die ein Element geklickt wird, die Ankertext, Daten im Zusammenhang mit Personen und Metadaten, aus der linkdatenbank. Suchanalyse bildet die Grundlage der Bestimmung der Relevanz. Verwendungsanalysen, ist andererseits, zum Analysieren von Informationen zur Verwendung von melden Sie sich von den Front-End-über den Ereignisspeicher empfangen wurden. Verwendungsanalyse bildet die Grundlage für Statistiken zu Nutzung und Berichte.

Die Ergebnisse von Analysen werden die Elemente im Suchindex hinzugefügt. Darüber hinaus werden Ergebnisse aus der Verwendungsanalyse in der analyseberichtsdatenbank gespeichert.

## <a name="building-blocks-for-customizing-the-search-experience"></a>Bausteine für das Anpassen des Suchvorgangs

Suche in SharePoint 2013 und SharePoint Online enthält neue Funktionen und Verbesserungen, die Sie zum Anpassen des Suchvorgangs zulassen. Viele der Verbesserungen erfordern keinen Code schreiben. SharePoint-Suche enthält CSOM und REST-APIs, mit deren Hilfe Sie müssen dem Schreiben von Code für Ihre Anpassung oder wenn Sie Add-Ins Zugriff auf SharePoint-Suchergebnisse außerhalb von SharePoint erstellen möchten.

### <a name="search-center-site"></a>Suchcenter-Website

Das Suchcenter ist eine SharePoint-Website für die Suche einrichten. Es ist ein Portal, in dem Sie die Suche nach Inhalten im Intranet Ihrer Organisation können, und bietet eine zentralisierte und anpassbare Benutzeroberfläche. Dieser Artikel beschreibt die Suchcenter-Seiten und Webparts, zusammen mit der suchkonfigurationseinstellungen, die Sie ändern können, um benutzerdefinierte Suche Erfahrungen erstellen, ohne zu viel Code schreiben, oder erstellen Sie benutzerdefinierte suchanwendungen.

Wenn Sie eine Suchcenter-Website erstellen, erstellt SharePoint eine Standardhomepage für die Suche und eine Standardseite für Suchergebnisse angezeigt. Darüber hinaus sind auch bekannte als Suche Optionen mehrere Seiten erstellt. Suche Optionen werden Suchergebnisseiten, die angepasst werden, um bestimmte Inhaltstypen, z. B. Personen und Videos, suchen und diese Suchergebnisse an, die für einen bestimmten Inhaltstyp oder einer Klasse formatiert und gefiltert.

Die folgenden Seiten werden in einer Websitesammlung Suchcenter in der Bibliothek für Seiten erstellt:

- **default.aspx** – die Startseite des Suchcenters und die Seite, in dem Endbenutzer ihre Abfragen eingeben.
    
- **results.aspx** - die standardmäßige Suche Ergebnisseite für das Suchcenter. Es ist außerdem die Suchergebnisseite der **Alles** suchsparte.
    
- **peopleresults.aspx** - Suche Ergebnisseite für die suchsparte **Personen** .
    
- **conversationresults.aspx** - Suche Ergebnisseite für die suchsparte **Unterhaltungen** .
    
- **videoresults.aspx** - Suche Ergebnisseite für die suchsparte **Videos** .
    
- **advanced.aspx** - Suchseite, in dem Endbenutzer Einschränkungen auf ihre Suchausdrücke anwenden können beschränken die Suche auf einen exakten Ausdruck.
    
Alle suchspartenseiten enthalten im Suchergebnisse-Webpart, obwohl das Webpart für jede suchsparte unterschiedlich konfiguriert ist. Für jede wird die Abfrage im Suchergebnisse-Webpart auf einer bestimmten ergebnisquelle gelten, vertikale Suche weitergeleitet. Beispielsweise ist die Abfrage im Suchergebnisse-Webpart auf der Seite peopleresults.aspx auf die ergebnisquelle lokale Personenergebnisse beschränkt. Verstehen, wie die standardsuchsparten in SharePoint 2013 konfiguriert werden kann Ihnen Erstellen Ihrer eigenen Suche vertikale oder Suchcenter anpassen.

Im folgenden sind zusätzliche Ressourcen zur Unterstützung des Suchcenters entwickelt:

- [Richten Sie ein Suchcenter in SharePoint 2013](http://technet.microsoft.com/en-us/library/dn794206%28v=office.15%29.aspx)
    
- [Zum Erstellen einer Websitesammlung für Search Center und ermöglichen Sie die Durchforstung des Inhalts in SharePoint 2013](http://technet.microsoft.com/en-us/library/dn794245%28v=office.15%29.aspx)
    
- [Erstellen einer Suchcenterwebsite in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/hh582314%28v=office.15%29.aspx)
    
- [Verwalten des Suchcenters](http://technet.microsoft.com/en-us/library/jj851144%28v=office.15%29.aspx)
    
- [Verwalten der Suchcenter in SharePoint Online](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/manage-the-search-center-in-sharepoint-online-HA103994122.aspx)

### <a name="search-center-web-parts"></a>Suchcenter-Webparts

Suchcenter Seiten enthalten vier Typen von Webparts: Suchfeld, Suchergebnisse, Suchnavigation und Einschränkung. 

#### <a name="search-box-web-part"></a>Suchen Sie im Feld-Webpart

Das Suchfeld-Webpart zeigt ein Textfeld, in dem Benutzer Text für die Suche eingeben. Standardmäßig verwendet, das Suchfeld-Webpart wird auf der Suchcenter-Homepage (default.aspx) sowie auf allen Standard-Suchergebnissen Seiten (results.aspx, peopleresults.aspx, conversationresults.aspx und videoresults.aspx).

Sie können das Suchfeld-Webpart durch Bearbeiten der Eigenschaften in der Webpart-Toolbereich anpassen. Hiermit können Sie folgende Aktionen ausführen:

- Ändern Sie, in die Suchergebnissen angezeigt werden. Beispielsweise können Sie die Ergebnisse in einem benutzerdefinierten Search Results Web teilweise oder auf eine benutzerdefinierte Suchergebnisseite Seite anzeigen.
    
- Deaktivieren von abfragevorschlägen und Personen Vorschläge.
    
- Anzeigen von Links zu einer sucheinstellungsseite und einer erweiterten Suchseite.
    
- Ändern der Anzeigevorlage für das Webpart an.
    
Weitere Informationen finden Sie unter [Konfigurieren von Eigenschaften für das Suchfeld-Webparts in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/gg576963%28v=office.15%29.aspx) und [wie Sie den Text zu ändern, der in das Suchfeld-Webparts in SharePoint Server 2013 angezeigt wird](http://technet.microsoft.com/en-us/library/dn794238%28v=office.15%29.aspx).

#### <a name="search-results-web-part"></a>Suchen Sie Suchergebnisse-Webpart

Das Suchergebnisse-Webpart zeigt die Ergebnisse einer Suchabfrage. Standardmäßig wird das Suchergebnisse-Webpart auf allen Standard suchspartenseiten (results.aspx, peopleresults.aspx, conversationresults.aspx und videoresults.aspx) verwendet. Das Suchergebnisse-Webpart sendet auch die Suchergebnisse an das einschränkungswebpart und das Suchnavigation-Webpart, damit es muss ein Suchergebnisse-Webpart auf einer Suchergebnisseite für die anderen Such-Webparts zu.

Sie können die Suchergebnisse Webpart-Eigenschaften in der Webpart-Toolbereich sowie die Suchabfrage zu ändern, um das Verhalten und die Darstellung der Ergebnisse auf der Suchergebnisseite alter bearbeiten. Durch Ändern der Eigenschaftswerte, können Sie Folgendes ein:

- Ändern Sie die ergebnisquelle aus, um anzugeben, welche Inhalte durchsucht werden sollen.
    
- Hinzufügen von Abfragevariablen oder Eigenschaftenfiltern zum Anpassen von Suchergebnissen für unterschiedliche Benutzer oder Benutzergruppen.
    
- Herauf- oder Herabstufen von Elementen oder Seiten innerhalb der Suchergebnisse.
    
- Ändern der Sortierung der Suchergebnisse.
    
- Ändern der Anzeigevorlage.
    
Weitere Informationen zu den Suchergebnisse-Webparts finden Sie unter [Konfigurieren von Eigenschaften des the Search Results Web Part in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/gg549987.aspx) und [zum Konfigurieren der Suchergebnisse-Webpart, um eine neue ergebnisquelle in SharePoint 2013 verwenden](http://technet.microsoft.com/en-us/library/dn794200%28v=office.15%29.aspx).

#### <a name="search-navigation-web-part"></a>Suchen Sie Suchnavigations-Webpart

Das Suchnavigation-Webpart zeigt Links, mit die Benutzer schnell zwischen den verschiedenen Suche-Optionen (alles, Personen, Gespräche und Videos) verschieben können. Das Suchnavigation-Webpart verwendet Suchergebnisse aus dem Suchergebnisse-Webpart, sodass Wenn Benutzer einen vertikale Suchlink auswählen, werden die Suchergebnisse gefiltert und angezeigt, wie die suchsparte eingerichtet ist. Durch die Suchnavigation Webpart-Eigenschaften in der Webpart-Toolbereich bearbeiten, können Sie das Webpart wie folgt anpassen:

- Angeben eines anderen Webparts aus der die Ergebnisse abgerufen.
    
- Ändern Sie die Anzahl der anzuzeigenden suchspartenlinks.
    
- Ändern der Darstellung und das Layout des Webparts.
    
Wählen Sie darüber hinaus auf dem Menüband **Websiteeinstellungen** > **Für die Suche** , um die folgenden Änderungen vornehmen:

- Ändern Sie die Anzeigenamen der Verknüpfung.
    
- Ändern der Verknüpfungsreihenfolge.

#### <a name="refinement-web-part"></a>Einschränkungsbereich-Webpart

Die Einschränkung Webpart Filter Suchergebnisse in Kategorien Einschränkungen aufgerufen. Benutzer können diese Einschränkungen auf die Suchergebnisse einzuschränken. Einschränkungen sind verwaltete Eigenschaften, die als _EINSCHRÄNKBAR_ als auch _Abfragbar_gekennzeichnet sind. Informationen zu diesen Einstellungen finden Sie unter [verwaltete Eigenschaften im Überblick Einstellung in der Übersicht über das Suchschema in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj219669%28v=office.15%29.aspx). Bearbeiten Sie die Einschränkung von Webpart-Eigenschaften in der Webpart-Toolbereich Folgendes an:

- Welche Suchergebnisse-Webpart zum Filtern Suche ergibt sich aus.
    
- Die Einschränkungen im Einschränkungsbereich-Webpart verwenden.
    
- Die Anzeigevorlage, die auf jede Einschränkung angewendet wird.
    
- Darstellung, Layout und Verhalten des Einschränkungsbereich-WebParts.
    
Standardmäßig zeigt die Anzahl der Ergebnisse für jeden Einschränkungswert nicht das Einschränkungsbereich-Webpart an. Sie können von einschränkungsanzahlen durch Ändern der Anzeigevorlage für die Einschränkung hinzufügen. Weitere Informationen zu diesem Feature finden Sie unter [Hinzufügen von einschränkungszählern, mit dem Einschränkungsbereich-Webpart in Konfigurieren von Eigenschaften des Einschränkungsbereich-Webparts in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/gg549985%28v=office.15%29.aspx).

Weitere Informationen zu den Einschränkungsbereich-Webpart und Einschränkungen finden Sie unter [Einschränkungen auf einer Suchergebnisseite in SharePoint 2013 verwenden möchten](http://technet.microsoft.com/en-us/library/dn794223%28v=office.15%29.aspx) , und [zum Hinzufügen von Einschränkungen zu Seite mit den Suchergebnissen in SharePoint 2013](http://technet.microsoft.com/en-us/library/dn794243%28v=office.15%29.aspx).

### <a name="result-sources"></a>Ergebnisquellen

Ergebnisquellen die Suche auf bestimmte Inhalte oder auf eine Teilmenge der Suchergebnisse einschränken. Sie können eine ergebnisquelle definieren, indem Sie Folgendes angeben:

- Eine Suchergebnisse vom Anbieter oder eine Quelle URL zum Abruf; beispielsweise Suchindex des lokalen SharePoint-Suchdiensts.
    
- Ein Protokoll zum Abrufen von Suchergebnissen verwendet; beispielsweise zum [OpenSearch](http://www.opensearch.org/Home) -Protokoll.
    
- Eine Abfragetransformation, die Ergebnisse aus der angegebenen Suchanbieter oder die URL auf eine bestimmte Teilmenge der Ergebnisse einschränken kann; Beispielsweise verfügt, um eine Gruppe von Ergebnissen ein bestimmtes Inhaltstyps.
    
SharePoint 2013 sechzehn vorkonfigurierte ergebnisquellen bietet, verwandte dem aktuellen Benutzer einschließlich lokale SharePoint-Ergebnisse, Gespräche und Elemente. Informationen zu ergebnisquellen auf der Seite **Ergebnisquellen verwalten** können Sie Details anzeigen. (**Websiteeinstellungen** > **Suche** > **Ergebnisquellen**). Klicken Sie auf der Seite **Ergebnisquellen verwalten** Sie neue ergebnisquellen in einem der beiden folgenden Methoden erstellen können:

- Wählen Sie **Neue Ergebnisquelle** , und wählen Sie das gewünschte Ergebnis Datenquelle aus. (Weitere Informationen finden Sie unter [Konfigurieren von ergebnisquellen für die Suche in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj683115%28v=office.15%29.aspx)).
    
- Zeigen Sie auf den Pfeil neben einer vorhandenen ergebnisquelle, wählen Sie **Kopieren**, ändern Sie die Kopie nach Bedarf, und speichern Sie sie unter einem neuen Namen.
    
Eine ergebnisquelle gibt eine von vier Protokollen Suchergebnisse abgerufen. Wenn die ergebnisquelle ein anderes Protokoll als **SharePoint lokal**verwendet wird, muss die ergebnisquelle auch eine URL aus dem Suchergebnisse abgerufen angeben.

**Ergebnisquellenprotokolle und ihre Anbieter**

|**Ergebnis-Quelle-Protokoll**|**Anbieter**|**URL**|
|:-----|:-----|:-----|
|SharePoint lokal|Der Suchindex des lokalen Suchdiensts.|Nicht zutreffend|
|Remote-SharePoint|Der Suchindex eines in einer anderen Farm gehosteten Suchdiensts.|Die Adresse der Stammwebsitesammlung der remote-SharePoint-Farm. |
|OpenSearch 1.0/1.1|Eine externe Suchanbieter (wie eine remote Suchmaschine oder Feed), die das OpenSearch-Protokoll verwendet, um die Suchergebnisse zu liefern.|Die URL des RSS-Feeds eines Suchanbieters, der das OpenSearch-Protokoll verwendet.|
|Exchange|Exchange-Webdienste (EWS).|EWS-URL.|

Hier finden Sie weitere Informationen:

- [Grundlegendes zu ergebnisquellen für die Suche in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn186229%28v=office.15%29.aspx)
    
- [Informationen zu ergebnisquellen und Verbund](http://technet.microsoft.com/en-us/library/jj219577%28v=office.15%29.aspx#Section12)
    
- [Grundlegendes zu ergebnisquellen](http://office.microsoft.com/en-us/sharepoint-server-help/understanding-result-sources-HA102848849.aspx?CTT=1)
    
- [Verwalten von ergebnisquellen](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/manage-result-sources-HA103639370.aspx)

### <a name="query-rules"></a>Abfrageregeln

Verwenden von Abfrageregeln zum Anpassen des Suchvorgangs für Abfragen, die für Ihre Benutzer besonders wichtig sind. In einer Abfrageregel Geben Sie den Kontext, Bedingungen und korrelierte Aktionen. Klicken Sie dann im angegebenen Kontext, und wenn eine Abfrage die angegebenen Bedingungen erfüllt, führt Suche korrelierten Aktionen zur Verbesserung der Relevanz der Suchergebnisse.

Im Hinblick auf Kontext können Sie die Abfrage Regel Abfragen einschränken, die sind: 

- Für eine angegebene ergebnisquelle ausgeführt.
    
- Aus einer angegebenen Thema Kategorie.
    
- Durch einen Benutzer mit einem angegebenen Benutzer-Segment ausgeführt.
    
Die folgende Tabelle enthält die Bedingungen, die Sie angeben können, dass die, die dazu führen, dass eine Abfrageregel ausführen.

**Abfrageregelbedingungen**

|**Condition**|**Beschreibung**|
|:-----|:-----|
|Abfrage stimmt exakt Schlüsselwort überein|Die Abfrageregel soll angewendet, wenn die Abfrage genau stimmt ein Wort oder Ausdruck, die Sie angeben.|
|Abfrage enthält Aktionsausdruck|Die Abfrageregel soll angewendet, wenn die Abfrage einen Begriff in Form von ein einzelnes Wort oder Ausdruck, der angibt enthält, dass der Benutzer versucht, etwas zu tun. Der Begriff muss der Anfang oder das Ende der Abfrage und möglicherweise ein Verb, einen Befehl oder einen Filter.|
|Abfrage stimmt exakt Wörterbuch überein|Die Abfrageregel soll angewendet, wenn die Abfrage exakt mit einem Wörterbucheintrag übereinstimmt. Dieser Eintrag kann einen Ausdruckssatz im Terminologiespeicher oder einen Eintrag im Wörterbuch Namen Personen sein. |
|Abfrage häufiger in Quelle|Die Abfrageregel soll angewendet, wenn die Abfrage des Benutzers als den aktuellen häufiger für eine andere ergebnisquelle durchgeführt wird. Diese Bedingung verwendet einer Analyse der Abfragen, die Benutzer in den verschiedenen ergebnisquellen eingegeben.|
|Häufig geklickter Ergebnistyp|Die Abfrageregel soll angewendet, wenn die Abfrage häufig Benutzer auswählen die Ergebnisse für einen bestimmten Ergebnistyp endet. Wenn Sie einen neuen Ergebnistyp erstellen, können Sie angeben, dass diese Auswahl aufgezeichnet werden soll, um in Abfrageregeln verwendet werden.|
|Erweiterte abfragetextübereinstimmung|Die Abfrageregel soll angewendet, wenn die Abfrage mit einem regulären Ausdruck übereinstimmt. Darüber hinaus können Sie die Verwendung von Variationen der Schlüsselwort, Aktionsausdruck und Wörterbuch-Bedingungen vorher noch stärkere Kontrolle erläutert.|

Eine Abfrageregel kann drei Arten von Aktionen angeben:

- Fügen Sie **Ergebnisse heraufgestuft** (früher als " **Beste Suchergebnisse**" bezeichnet), die über bewertete Ergebnisse angezeigt werden. Beispielsweise könnten die Abfrageregel für die Abfrage "Krankheit", ein bestimmtes heraufgestuft Ergebnis, wie eine Verknüpfung zu einer Website angeben, die eine Unternehmensrichtlinie bezüglich nicht bei der Arbeit-Anweisung besteht.
    
- Hinzufügen einer oder mehrerer Gruppen von Ergebnissen, ergebnisblöcke aufgerufen. Ein Ergebnisblock enthält eine kleine Gruppe von Ergebnissen, die auf eine bestimmte Weise zu einer Abfrage verknüpft sind. Wie einzelne Ergebnisse können Sie einen Ergebnisblock herauf- oder ordnen es mit anderen Suchergebnissen. 
    
- Ändern Sie die Rangfolge der Ergebnisse durch Ändern der Abfrage. Beispielsweise für eine Abfrage, die "Toolbox herunterladen" enthält, konnte eine Abfrageregel das Wort "herunterladen" als ein Aktionsausdruck erkennen und Boost von Suchergebnissen, zeigen Sie auf einen bestimmten Download-Website in Ihrem Intranet.
    
Weitere Informationen zu Abfrageregeln finden Sie unter [Verwalten von Abfrageregeln in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj871676.aspx).

### <a name="query-transforms"></a>Transformationen Abfrage

Um die Suchergebnisse zu liefern, die für eine Benutzerabfrage geeignet sind, muss manchmal die Abfrage geändert werden soll. Hierzu abfragetransformationen. SharePoint 2013 wie Videos, Personen und Unterhaltungen enthaltener standardsuchsparten, enthalten alle vordefinierten abfragetransformationen zur Optimierung des Suchvorgangs für diese vertikal.

Abfragetransformationen können an drei Orten konfiguriert werden:

- In einem Webpart wie einem Suchergebnisse-Webpart. 
    
- In einer Abfrageregel gibt an, welche bestimmte Aktionen werden durchgeführt, nur, wenn bestimmte Bedingungen erfüllt werden. 
    
- In der ergebnisquelle, die die Abfrage verwendet, um Suchergebnisse abzurufen.
    
Eine Abfrage des Benutzers wird vom Webpart und dann nach jeder Abfrageregeln, die anwenden möchten, zuerst transformiert und schließlich auf durch die ergebnisquelle aus. Beim Konfigurieren eine Transformation auf eine ergebnisquelle, wissen Sie, dass die Transformation Änderungen nicht verworfen oder überschreiben, da die ergebnisquelle aus die Abfrage zuletzt transformiert. Sie können eine Quelle Abfragetransformation ein Ergebnis in Webparts oder ergebnisblöcke wiederverwenden, und Sie Erstellen von Abfrageregeln oder Ergebnistypen, die nur Ergebnisse aus bestimmten ergebnisquellen angewendet werden können.

Sie können den Abfrage-Generator, damit Sie schreiben und Testen von abfragetransformationen verwenden. Sie können die Abfrage von innerhalb des Abfrage-Generators durch Festlegen von Werten für die Abfragevariablen temporäre Test testen die Abfrage ausführen und Anzeigen einer Vorschau der Suchergebnisse. Weitere Informationen zu abfragetransformationen finden Sie unter [Planen der transform Queries and Order Results in SharePoint 2013](http://technet.microsoft.com/en-us/library/60a1110d-27dc-45d0-86e2-cddc72d072b2%28v=office.15%29).

### <a name="result-types-and-display-templates"></a>Ergebnistypen und Anzeigevorlagen

SharePoint 2013-Suche umfasst ein neues Ergebnisse-Framework, das erleichtert die Art und Weise anpassen der Suchergebnisse angezeigt werden. Nun können Sie anstelle von Schreiben von benutzerdefiniertem XSLT zum Ändern der Anzeige von Suchergebnissen aus, die Darstellung der wichtige Typen von Ergebnissen mithilfe von Anzeigevorlagen und Ergebnistypen anpassen.

#### <a name="result-types"></a>Ergebnistypen

Um die Anzeige von Suchergebnissen anders, haben Suchergebnisse in verschiedenen Ergebnistypen sortiert werden sollen. Ein Ergebnistyp ist eine Aufstellung ein Suchergebnis an, die ein Suchergebnis von einem anderen unterscheidet. Es besteht eine Auflistung der folgenden:

- **Regeln** – mindestens eine Merkmale oder Bedingungen zum Vergleichen von eigenständigen jedes Suchergebnis vor, wie die ergebnisquelle oder den Inhaltstyp, der das Suchergebnis. Regelbedingungen können mithilfe von Gleichheit, Vergleichsoperatoren und logischen Operatoren verknüpft werden.
    
- **Eigenschaften** - die Liste der verwalteten Eigenschaften für das Suchergebnis. Sie müssen der Eigenschaftenliste verwaltete Eigenschaften hinzufügen, bevor Sie eine Anzeigevorlage die verwaltete Eigenschaft zuordnen.
    
- **Anzeigevorlagen** - steuert die Art der in der alle Ergebnisse, die die Kriterien erfüllen, angezeigt werden, und Verhalten auf einer Suchergebnisseite.
    
SharePoint-Suche umfasst mehrere standardergebnistypen. Um diese anzuzeigen, wechseln Sie zu **Websiteeinstellungen** > **Websitesammlungsverwaltung** > **Suchergebnistypen**. Den standardmäßigen Ergebnistypen kann nicht bearbeitet werden. Sie können neue Ergebnistypen durch vorhandene kopieren und ändern sie erstellen. Weitere Informationen zu den standardmäßigen Ergebnistypen SharePoint 2013 enthaltener finden Sie unter [Ergebnistypen und Anzeigevorlagen, die Anzeige von Suchergebnissen in SharePoint Server 2013 verwendet werden](http://technet.microsoft.com/en-us/library/dn386874%28v=office.15%29.aspx).

#### <a name="display-templates"></a>Anzeigevorlagen

Anzeigevorlagen definieren die visuelle Layout und das Verhalten von Suchergebnissen. Sie steuern, welche verwalteten Eigenschaften in den Suchergebnissen angezeigt werden und wie diese angezeigt werden. SharePoint speichert Anzeigevorlagen in die Suche Unterordner des Ordners Anzeigevorlagen im Gestaltungsvorlagenkatalog. Jede Anzeigevorlage besteht aus zwei Dateien: 

- Eine HTML-Version der Anzeigevorlage an, der Sie in Ihre HTML-Editor bearbeiten können.
    
- Eine JS-Datei, die von SharePoint verwendet wird. 
    
Beim Arbeiten mit Anzeigevorlagen, ändern Sie die HTML-Datei. Die JS-Datei erstellt und geändert von SharePoint. Sie diese Datei überhaupt nicht bearbeiten.

Es gibt grundsätzlich zwei Arten von Anzeigevorlagen:

- **Steuerelement Anzeigevorlagen** - bestimmen die allgemeine Struktur wie die Ergebnisse dargestellt werden.
    
- **Element Anzeigevorlagen** - bestimmen, wie jedes Ergebnis in der Gruppe angezeigt wird.
    
Die Steuerelement-Anzeigevorlage bietet HTML, um die Struktur des allgemeinen Layouts für, wie Sie die Suchergebnisse zu präsentieren möchten. Beispielsweise können Sie die Steuerelement-Anzeigevorlage für eine Überschrift und Anfang und Ende einer Liste den HTML-Code bereitstellen. Die Steuerelement-Anzeigevorlage wird nur einmal im Webpart gerendert.

Die Elementanzeigevorlage stellt HTML bereit, das die Anzeige jedes Elements im Ergebnissatz bestimmt. So stellt die Elementanzeigevorlage möglicherweise das HTML für ein Listenelement bereit, das ein Bild und drei Zeilen Text enthält, die unterschiedlichen verwalteten Eigenschaften zugeordnet sind, die mit dem Element verknüpft sind. Die Elementanzeigevorlage wird für jedes Element im Ergebnissatz einmal gerendert. Wenn der Ergebnissatz zehn Elemente enthält, erstellt die Anzeigevorlage daher ihren HMTL-Abschnitt zehnmal.

Details Anzeigevorlagen und deren Struktur finden Sie unter [SharePoint 2013 Design Manager display Templates](http://msdn.microsoft.com/en-us/library/jj945138.aspx) und [suchgesteuerte Webparts und Anzeigevorlagen](http://msdn.microsoft.com/en-us/library/jj191506.aspx) in [Übersicht über das Modell von SharePoint 2013](http://msdn.microsoft.com/en-us/library/jj191506.aspx).

Weitere Informationen zu Anzeigevorlagen in SharePoint 2013 verfügbar sind finden Sie unter [Anzeigen der vorlagenreferenz in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj944947.aspx).

#### <a name="customize-display-templates"></a>Konfigurieren von Anzeigevorlagen

Wenn Sie Anzeigevorlagen in SharePoint enthaltene anpassen möchten, erstellen Sie eine neue Anzeigevorlage durch Kopieren des Inhalts aus, die Sie ändern möchten, und passen Sie anschließend die neue Version. Eine Kopie einer vorhandenen Anzeigevorlage beginnend ist auch die einfachste Möglichkeit, eine neue erstellen, wie es wird sichergestellt, dass alle erforderlichen Elemente verwendet wird.

Ein weiterer Tipp beim Arbeiten mit Anzeigevorlagen ist zum Zuordnen eines Netzlaufwerks zum Gestaltungsvorlagenkatalog. Weitere Informationen hierzu finden Sie unter [wie: Zuordnen eines Netzlaufwerks zum SharePoint 2013 Master Page Gallery](https://msdn.microsoft.com/en-us/library/office/jj733519.aspx).

Die HTML-Datei, die für eine Anzeigevorlage verwendet wird einen vollständigen HTML-Dokument mit `head` und `body` Elemente. Innerhalb der `head` -Element ist ein `title` -Element, das den Anzeigenamen für die Anzeigevorlage angibt. Der Text in diesem Tag wird, was angezeigt wird, wenn Sie Konfigurationen in der SharePoint-UI, beispielsweise tun, wenn Sie einen Ergebnistyp konfigurieren.

Nach der `title` -Element ist ein benutzerdefinierter Eigenschaften Dokumentelement `mso:CustomDocumentProperties`. In elementanzeigevorlagen, dieses Element enthält ein `mso:ManagedPropertyMapping` -Element, das ist, wobei die verwalteten Eigenschaften von SharePoint-Suche verwendet, von der Anzeigevorlage verwendeten Werte zugeordnet werden. Im folgenden werden die Syntax für diese: `<display template reference name>:<managed property name>`, wie im folgenden Beispiel gezeigt.

```HTML
<mso:ManagedPropertyMapping msdt:dt="string">'Title':'Title','Path':'Path','Description':'Description'
```

Innerhalb der `body` -Element vorhanden ist ein `script` Element, in dem Sie externe Ressourcen wie CSS-Dateien oder JavaScript-Dateien außerhalb der Anzeigevorlage einfügen können. Finden Sie im Abschnitt "Skriptblock" in [SharePoint 2013 Design Manager display Templates](http://msdn.microsoft.com/en-us/library/jj945138.aspx) Beispiele dazu, wie Sie externe Ressourcen in das Script-Element enthalten.

Das nächste Element ist ein `div` Element. Dies ist, platzieren Sie alle HTML oder Skripts, das als Teil der Vorlage angezeigt werden soll. Eine gute Möglichkeit, sich mit anzeigevorlagenstruktur vertraut werden Kopien der Standardvorlagen für Suchergebnisse anzeigen, Control_SearchResults.html, die Steuerelement-Anzeigevorlage und Item_Default.html elementanzeigevorlage herunterladen.

#### <a name="additional-resources-for-result-types-and-display-templates"></a>Zusätzliche Ressourcen für Ergebnistypen und Anzeigevorlagen

Im folgenden sind einige zusätzlichen Ressourcen für Anzeigevorlagen und Ergebnistypen:

- [Anpassen von Suchergebnistypen in SharePoint 2013](http://technet.microsoft.com/en-us/library/dn135239%28v=office.15%29.aspx)
    
- [Gewusst wie: Ändern der Suchergebnisse in SharePoint Server 2013 angezeigt werden](http://technet.microsoft.com/en-us/library/dn794204%28v=office.15%29.aspx)
    
- [Grundlegendes zur Anzeige der Suchergebnisse in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794212%28v=office.15%29.aspx)
    
- [Grundlegendes zu anzeigen wie Vorlagen und treffermarkierungen in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794249%28v=office.15%29.aspx)
    
- [Gewusst wie: erstellen ein neuen Ergebnistyps in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794234%28v=office.15%29.aspx)
    
- [Von Werten von benutzerdefinierten verwalteten Eigenschaften in Suchergebnissen – Option 1 in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794209%28v=office.15%29.aspx)
    
- [Von Werten von benutzerdefinierten verwalteten Eigenschaften in Suchergebnissen – Option 2 in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794240%28v=office.15%29.aspx)
    
- [Gewusst wie: Anzeigen von Werten von benutzerdefinierten verwalteten Eigenschaften im daraufzeigebereich in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn794247%28v=office.15%29.aspx)

## <a name="query-apis-and-search-add-ins"></a>Abfragen von APIs und Durchsuchen-add-ins

SharePoint 2013-Suche umfasst .NET und JavaScript-clientobjektmodellen und ein REST-Dienst, der Zugriff auf online für Suchergebnisse, lokalen und Mobilgeräte-Entwicklung ermöglicht. 

**Suchabfrage-APIs**

|**API**|**Class Library oder Schema Pfad**|**Beispiel**|
|:-----|:-----|:-----|
|.NET CSOM|Microsoft.SharePoint.Client.Search.dll[Client Components SDK für SharePoint Server 2013 herunterladen](http://www.microsoft.com/en-us/download/details.aspx?id=35585)%ProgramFiles%\Common Files\Microsoft Shared\web Server extensions\15\ISAPI[SharePoint Online-Clientkomponenten – SDK herunterladen](http://www.microsoft.com/en-us/download/details.aspx?id=42038)% ProgramFiles%\Common Dateien\Microsoft Shared\web Server extensions\16\ISAPI|[SharePoint 2013: Suche mit der verwaltete Client Abfragen](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1) [Objektmodell (Code Gallery)](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1)|
|JavaScript-CSOM|SP.search.js%ProgramFiles%\SharePoint Client Components\Scripts|[Abfragen von Suche mit der JavaScript-Clientobjektmodell](http://code.msdn.microsoft.com/SharePoint-2013-Querying-a629b53b) (Code Gallery)|
|REST-Dienst|Http://Server/_API/Search/queryhttp://Server/_API/Search/ postqueryhttp://server/_api/search/suggest|[SharePoint 2013: Verwenden des REST-Suchdiensts aus einer SharePoint-Add-in-service](http://code.msdn.microsoft.com/sharepoint/SharePoint-2013-Perform-a-1bf3e87d) (Code Gallery)|

### <a name="search-query-net-csom"></a>Suchabfrage .NET CSOM

Um die Abfrage .NET CSOM verwenden möchten, erstellen Sie eine neue Instanz der [t: Microsoft.SharePoint.Client.ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) -Klasse, die in der [Microsoft.SharePoint.Client](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.aspx) -Namespace in der Microsoft.SharePoint.Client.dll befindet. Verwenden Sie das abfrageobjektmodell klicken Sie dann im [Microsoft.SharePoint.Search.Client.Query](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.search.query.aspx) -Namespace. Es folgt ein einfaches Beispiel.

```C#
using Microsoft.SharePoint.Client; 
using Microsoft.SharePoint.Client.Search.Query;
â€¦
using (ClientContext clientContext = new ClientContext("http://intranet.contoso.com"))
{
    KeywordQuery keywordQuery = new KeywordQuery(clientContext);
    keywordQuery.QueryText = "Argument";
    SearchExecutor searchExecutor = new SearchExecutor(clientContext);
    ClientResult<ResultTableCollection> results = searchExecutor.ExecuteQuery(keywordQuery);
    clientContext.ExecuteQuery();
}
 
```

Sie können nun die Suchergebnisse durchlaufen. Im folgenden Beispiel wird der Titel jedes Ergebnisses geschrieben.

```C#
foreach (var row in results.Value[0].ResultRows) 
{ 
    Console.WriteLine(row["Title"]); 
}
```

### <a name="search-query-rest-service"></a>Suchabfrage-REST-Dienst

Die Suchabfrage REST-Dienst unterstützt sowohl HTTP **POST** und **GET** -Anforderungen. Wenn Sie einen Anruf mit dem Search-REST-Dienst vornehmen, geben Sie die Abfrageparameter mit der Anforderung, und suchen Sie diese Abfrageparameter verwendet, um die Suchabfrage zu erstellen. Mit **GET** -Anforderung Geben Sie die Parameter für die Abfrage in der URL. **POST** -Anforderungen übergeben Sie Parameter für die Abfrage in den Hauptteil in JavaScript Object Notation (JSON)-Format.

**JSON GET und POST-Anforderungen**

|Verb|URI|
|:---|:---|
| **GET** -Anfragen| `http://server/_api/search/query`|
| **POST** -Anforderungen| `http://server/_api/search/postquery`|

**GET-beispielanfragen für Search-REST-Dienst**

|**Anforderungstyp**|**Anforderungs-URL**|
|:-----|:-----|
|Schlüsselwörter|http://Server/Site/_API/Search/Query?QueryText= '{KQL-Abfrage}'|
|Eigenschaften auswählen|http://Server/Site/_API/Search/query?querytext= 'Test'&amp;Selectproperties = 'Titel, Rang'|
|Die Sortierung|http://Server/Site/_API/Search/query?querytext= 'Test'&amp;Sortlist =' ZuletztGeändertUm: absteigender 'http://server/site/_api/search/query?querytext=' Test'&amp;Sortlist =' ZuletztGeändertUm: absteigender Rangfolge: Aufsteigend '|

Eine vollständige Liste der verfügbaren Parameter für die Abfrage und deren Verwendung finden Sie unter [SharePoint Search-REST-API (Übersicht)](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx). Beispielcode finden Sie unter [SharePoint 2013: Verwenden des REST-Suchdiensts aus einer SharePoint-Add-in-service](https://code.msdn.microsoft.com/sharepoint/SharePoint-2013-Perform-a-1bf3e87d).

### <a name="search-add-ins"></a>Search-add-ins

SharePoint-Add-ins (vormals apps für SharePoint) sind eigenständig der Funktionalität, die der Leistungsumfang von einer SharePoint-Website. Search-add-ins (vormals Search-apps) sind SharePoint-Add-ins, die Suchfunktion verwenden. In ein Search-add-ins können Sie die Suchabfrage APIs verwenden, um Suchergebnisse abzurufen. Darüber hinaus können Sie auch verwenden zum Verteilen von Suchkonfigurationen aus einer SharePoint-Installation in eine andere.

Informationen zum Einrichten einer Entwicklungsumgebung zum Erstellen Suchen Sie-add-ins zu, finden Sie unter [Einrichten von einer lokalen Entwicklungsumgebung für SharePoint-Add-ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx) oder [einer Entwicklungsumgebung für SharePoint-Add-ins in Office 365 einrichten](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx).

#### <a name="permissions"></a>Berechtigungen

Search-add-ins sind nur auf Benutzerebene Berechtigungen, wobei der Wert des Attributs _QueryAsUserIgnoreAppPrincipal_ist erforderlich. Mit dieser Berechtigung können Sie die Abfragen der Suche Add-Ins basierend auf den Berechtigungen des Benutzers. Dies bedeutet, dass ACLs des Benutzers, dass die Suche, die Ergebnisse zurückgegeben werden, basiert. So gewähren Sie Berechtigungen für die Add-ins für auf Suche verwenden:

1. Öffnen Sie im **Projektmappen-Explorer** **AppManifest.xml**aus.
    
2. Wählen Sie **Suchen nach Bereich** aus, und wählen Sie **QueryAsUserIgnoreAppPrincipal**, klicken Sie auf der Registerkarte **Berechtigungen** .
    
Weitere Informationen finden Sie unter [Add-in-Berechtigungen in SharePoint 2013](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx).

#### <a name="query-apis"></a>Abfrage-APIs

Sie können die .NET CSOM, JavaScript CSOM oder Search-REST-Dienst Abrufen von Suchergebnissen in einer Search-add-ins verwenden. Im folgenden Beispiel wird veranschaulicht, wie die Abfrage .NET CSOM Abrufen von Suchergebnissen in einer Search-add-ins verwenden.

```C#
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    KeywordQuery keywordQuery = new KeywordQuery(clientContext);
    keywordQuery.QueryText = "Argument";
    SearchExecutor searchExecutor = new SearchExecutor(clientContext);
    ClientResult<ResultTableCollection> results = searchExecutor.ExecuteQuery(keywordQuery);
    clientContext.ExecuteQuery();
}

```

## <a name="in-this-section"></a>Inhalt dieses Abschnitts

- [Durchsuchen von Anpassungen für SharePoint](search-customizations-for-sharepoint.md)

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
- [Search-add-ins in SharePoint 2013](http://msdn.microsoft.com/library/21682e45-dd78-4f3c-8f1e-cdd48de3bde2%28Office.15%29.aspx)
    
- [Hinzufügen von Suchfunktionen zu SharePoint-Add-ins](http://blogs.msdn.com/b/officeapps/archive/2013/05/30/add-search-capabilities-to-your-apps-for-sharepoint.aspx)
