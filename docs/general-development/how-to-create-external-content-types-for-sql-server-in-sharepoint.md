---
title: "Erstellen externer Inhaltstypen für SQL Server in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7fe2fbf0-546b-4a16-b02e-a0960bfb3842
ms.openlocfilehash: d27d71887195026571d440b6484fad2876acf9ea
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-external-content-types-for-sql-server-in-sharepoint"></a>Erstellen externer Inhaltstypen für SQL Server in SharePoint

In diesem Artikel erfahren Sie, wie Sie einen externen Inhaltstyp für SQL Server in SharePoint erstellen.

Das Erstellen eines externen Inhaltstyps ist eine wichtige Aufgabe, wenn Sie mit externen Daten arbeiten. Ein externer Inhaltstyp enthält wichtige Informationen zu Verbindungen, Zugriff, Betriebsarten, Spalten, Filtern und anderen Metadaten, die zum Abrufen von Daten aus der externen Datenquelle dienen.
  
    
    


## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="section1"> </a>

Das Arbeiten mit externen Daten erfordert einige vorbereitende Aufgaben zum Ermöglichen des sicheren Zugriffs auf die Daten. Die folgenden Informationen können Ihnen bei der Planung der nächsten Schritte helfen. Wenn Sie darüber hinaus Probleme bei der Arbeit mit externen Daten haben sollten, können Sie anhand dieser Informationen das Problem ausmachen. Für den Zugriff auf externe Daten müssen Sie oder ein Administrator folgendermaßen vorgehen:
  
    
    
 **Vorbereiten von SQL Server** Ein Datenbankadministrator muss Berechtigungen vergeben, um sicherzustellen, dass die richtigen Personen auf die Daten zugreifen können und die Daten nicht in falsche Hände geraten. Der Datenbankadministrator muss auch ein SQL Server-Konto mit db_owner-Berechtigung erstellen. Der Datenbankadministrator kann zudem spezielle Tabellen, Ansichten, Abfragen, Spalten-Aliase usw. erstellen, um die Ergebnisse auf die benötigten Elemente zu beschränken und die Leistung zu verbessern.
  
    
    
 **Konfigurieren von SharePoint-Services** Ein Administrator muss Business Connectivity Services (BCS) und den Secure Store Service aktivieren.
  
    
    
 **Konfigurieren des einmaligen Anmeldens** Ein Administrator muss den geeignetsten Zugriffsmodus für die externe Datenquelle bestimmen, eine Zielanwendung erstellen und die Anmeldeinformationen für die Zielanwendung festlegen.
  
    
    
 **Konfigurieren von Business Data Connectivity Services** Ein Administrator muss sicherstellen, dass der Benutzer, der den externen Inhaltstyp erstellt, über Berechtigungen für den Business Data Connectivity-Metadatenspeicher (BDC) verfügt und dass entsprechende Benutzer Zugriff auf den externen Inhaltstyp haben, auf dem die externe Liste basiert.
  
    
    
 **Sicherstellen, dass Office 2013 einsatzbereit ist** Zum Synchronisieren externer Daten mit Office 2013-Produkten müssen Sie Windows 7 oder eine höhere Version verwenden und sicherstellen, dass die Office-Installationsoption für Business Connectivity Services (BCS) aktiviert ist (Standardeinstellung). Über diese Option wird die Business Connectivity Services-Clientlaufzeit installiert, die externe Daten zwischenspeichert und synchronisiert, Geschäftsdaten externen Inhaltstypen zuweist, das Auswahltool für externe Elemente in Office-Produkten anzeigt und benutzerdefinierte Lösungen in Office-Produkten ausführt. Sie müssen außerdem auf allen Clientcomputern SQL Server Compact 4.0, .NET Framework 4 und WCF Data Services 5.0 für OData, Version 3, installieren. (Bei Bedarf werden Sie automatisch zum Herunterladen der Software aufgefordert).
  
    
    

## <a name="define-general-information"></a>Definieren allgemeiner Informationen
<a name="section2"> </a>


1. Starten Sie Microsoft SharePoint Designer 2013.
    
  
2. Klicken Sie auf **Website öffnen**, und geben Sie dann den entsprechenden Websitenamen ein.
    
  
3. Wählen Sie im **Navigationsbereich** unter **Websiteobjekte** die Option **Externe Inhaltstypen**.
    
    > [!NOTE]
    > SharePoint Designer 2013 gruppiert externe Inhaltstypen nach dem Namespace im ersten Fenster des Designers für externe Inhaltstypen. 

4. Klicken Sie zum Öffnen des Designers für externe Inhaltstypen im Menüband auf **Externer Inhaltstyp**.
    
  
5. Führen Sie auf der Seite **Neuer externer Inhaltstyp** die folgenden Aktionen durch:
    
  - Klicken Sie neben **Name** auf **Neuer externer Inhaltstyp**, und geben Sie einen eindeutigen Namen für den externen Inhaltstyp ein.
    
  
  - Geben Sie neben **Anzeigename** einen anderen Namen ein, wenn Sie einen etwas aussagekräftigeren Anzeigenamen wünschen.
    
  

## <a name="define-general-and-office-behaviors"></a>Definieren des allgemeinen Verhaltens und des Office-Verhaltens
<a name="section3"> </a>


1. Wählen Sie in der Dropdownliste **Office-Elementtyp** einen der folgenden aus:
    
  - **Allgemeine Liste** Diese Option eignet sich für jede Art von Liste.
    
  
  - **Termin, Kontakt, Aufgabe oder Beitrag** Wählen Sie diese Option aus, wenn Sie eine Liste erstellen, die sich wie ein Outlook-Kontakt-, -Aufgaben-, -Termin- oder Beitragselement verhält. Der Office-Elementtyp, den Sie hier auswählen, bestimmt das gewünschte Outlook-Verhalten des externen Inhaltstyps. Ein externer Inhaltstyp wie beispielsweise "Kunde" verhält sich wie ein Kontaktelement in Outlook selbst.
    
  
2. Stellen Sie sicher, dass für das Kontrollkästchen **Offlinesynchronisierung für externe Liste** die Option **Aktiviert** (Standardeinstellung) ausgewählt ist.
    
    > [!NOTE]
    > Wenn Sie diese Option deaktivieren, ist der Befehl **SharePoint mit Outlook verbinden** für eine externe Liste nicht verfügbar.

> [!NOTE]
> Das Farm- und Website-Feature **Offline-Synchronisierung für externe Listen** muss ebenfalls aktiv sein. Dieses Feature ist standardmäßig auf der Farmebene, aber nicht standardmäßig auf der Websiteebene aktiv. 
  
    
    


## <a name="create-a-connection-to-the-external-data"></a>Erstellen einer Verbindung mit den externen Daten
<a name="section4"> </a>


1. Zum Angeben der SQL Server-Datenbank für den externen Inhaltstyp klicken Sie auf **Klicken Sie hier, um externe Datenquellen zur ermitteln und Vorgänge zu definieren**.
    
  
2. Klicken Sie auf **Verbindung hinzufügen**, wählen Sie im Dialogfeld **Auswahl des externen Datenquellentyps** die Option **SQL Server** aus, und klicken Sie dann auf **OK**.
    
  
3. Geben Sie im Dialogfeld **SQL Server-Verbindung** den Namen des Servers, den Datenbanknamen und eine optionale Beschreibung ein, und klicken Sie dann auf **OK**.
    
  
4. Wählen Sie zum Auswählen eines Authentifizierungsmodus eine der folgenden Optionen aus:
    
  - **Verbindung mit der Identität des Benutzers herstellen** Bei dieser Option wird der Pass-Through-Authentifizierungsmodus verwendet.
    
  
  - **Verbindung mit angenommener Windows-Identität herstellen** Bei dieser Option wird der Authentifizierungsmodus "WindowsCredentials" verwendet.
    
  
  - **Verbindung mit angenommener benutzerdefinierter Identität herstellen** Bei dieser Option wird der Authentifizierungsmodus "RDBCredentials" verwendet.
    
  
5. Geben Sie in das Feld **ID der Anwendung für einmaliges Anmelden** die in Einmaliges Anmelden erstellte Zielanwendungs-ID ein.
    
  
6. Klicken Sie auf **OK**.
    
  
SharePoint Designer 2013 überprüft und testet die Verbindungsinformationen. Wenn Meldungen angezeigt werden, müssen Sie die gemeldeten Probleme beheben, bevor Sie fortfahren.
  
    
    

## <a name="select-a-table-view-or-routine"></a>Auswählen einer Tabelle, Ansicht oder Routine
<a name="section5"> </a>


1. Erweitern Sie im Datenquellen-Explorer die Datenbank, um die darin enthaltenen Tabellen, Ansichten und Routinen anzuzeigen.
    
  
2. Wählen Sie eine Tabelle, Ansicht oder Routine aus.
    
  

## <a name="define-operations"></a>Definieren von Vorgängen
<a name="section6"> </a>


1. Klicken Sie im Datenquellen-Explorer mit der rechten Maustaste auf die Tabelle, Ansicht oder Routine, und wählen Sie dann eine der folgenden Optionen:
    
  - **Alle Vorgänge erstellen** Dient zum Definieren der Vorgänge "Element erstellen", "Element löschen", "Element lesen", "Liste lesen" und "Element aktualisieren".
    
    > [!NOTE]
    > **Alle Vorgänge erstellen** ist nur für Tabellen und Ansichten verfügbar. Routinen benötigen spezifische Vorgänge.

  - **Neuer Elementlesevorgang** Dient zum Definieren eines Elementlesevorgangs.
    
  
  - **Neuer Listenlesevorgang** Dient zum Definieren eines Listenlesevorgangs.
    
  
  - **Neuer Aktualisierungsvorgang** Dient zum Definieren eines Aktualisierungsvorgangs.
    
  
  - **Neuer Löschvorgang** Dient zum Definieren eines Löschvorgangs.
    
  
  - **Aktualisieren** Dient zum Aktualisieren der Liste der Tabellen, Ansichten und Routinen im Datenquellen-Explorer.
    
  
2. Klicken Sie auf **Weiter**.
    
  
> [!NOTE]
> - Stellen Sie bei Ansichten, die mehrere Tabellen umfassen, sicher, dass Schreibvorgänge unterstützt werden. Andernfalls sind die Befehle **Alle Vorgänge erstellen** oder **Neuer Aktualisierungsvorgang** nicht erfolgreich.
> - Definieren Sie stets mindestens einen **Neuen Elementlesevorgang** und **Neuen Listenlesevorgang**, da SharePoint-Features wie externe Listen von diesen Vorgängen abhängig sind.
> - Entscheiden Sie sich für spezifische Vorgänge anstatt für **Alle Vorgänge erstellen**, wenn die Tabelle oder Ansicht bestimmte Vorgänge nicht unterstützt.
    
  

## <a name="add-columns"></a>Hinzufügen von Spalten
<a name="section7"> </a>


1. Um die Spalten der Tabelle oder Ansicht anzugeben, die Sie anzeigen möchten, klicken Sie auf **Weiter**.
    
  
2. Im Dialogfeld **Parameterkonfiguration** sind standardmäßig alle Spalten (als **Datenquellenelemente** bezeichnet) ausgewählt. Zum Entfernen nicht benötigter Spalten deaktivieren Sie die entsprechenden Kontrollkästchen.
    
    > [!NOTE]
    > Im Gegensatz zu einer SharePoint-eigenen Liste kann der Spaltenname einer externen Liste nicht geändert werden. Erwägen Sie einen SQL-Spaltenalias, um einen aussagekräftigeren Namen bereitzustellen, oder verwenden Sie einen kürzeren Namen. 

3. Um ein ID-Feld auszuwählen, klicken Sie auf ein Feld und markieren Sie es (in der Regel ein Feld mit einem eindeutigen Werten). Klicken Sie dann unter **Eigenschaften** auf **Zu ID zuordnen**.
    
> [!IMPORTANT]
> Um zu verhindern, dass bestimmte Felder aktualisiert werden, z. B. eine ID oder ein Primärschlüsselfeld, deaktivieren Sie das Kontrollkästchen **Erforderlich**. Aktivieren Sie hingegen das Kontrollkästchen **Schreibgeschützt**, was zum Abrufen von Elementen nötig ist, damit Sie andere Felder aktualisieren können.
  
> [!TIP]
> Lesen Sie sich die Meldungen im Bereich **Fehler und Warnungen** immer sorgfältig durch. Sie enthalten nützliche Informationen zur Bestätigung Ihrer Aktionen oder zur Behandlung von Problemen. Klicken Sie regelmäßig in den Bereich **Fehler und Warnungen**, und stellen Sie sicher, dass keine weiteren Fehler oder Warnungen vorhanden sind.

## <a name="map-outlook-fields"></a>Outlook-Felder zuordnen
<a name="section8"> </a>

Falls Ihr externer Inhaltstyp einem Outlook-Elementtyp zugeordnet ist, müssen Sie die Felder Ihres externen Inhaltstyps Outlook-Elementfeldern zuordnen. Wenn Sie einen externen Inhaltstyp, wie z. B. "Kunde", einem Outlook-Elementtyp wie "Kontakt" zuordnen, müssen Sie die einzelnen Felder im externen Inhaltstyp, wie z. B. "Vorname des Kunden", "Nachname des Kunden", "Kundenadresse" und "Telefonnummer des Kunden" explizit den entsprechenden Outlook-Feldern des Kontakts zuordnen, z. B. "Vorname", "Nachname", "Geschäftsadresse" und "Telefon geschäftlich" zuordnen.
  
    
    

- Gehen Sie bei jedem Feld wie folgt vor:
    
1. Klicken Sie auf ein Feld, um es zu markieren.
    
  
2. Klicken Sie unter **Eigenschaften** neben **Office-Eigenschaft** auf den Abwärtspfeil, und wählen Sie dann das entsprechende übereinstimmende Feld. 
    
> [!NOTE]
> Es müssen zwar nicht alle entsprechenden Felder zugeordnet werden, die in der folgenden Tabelle aber auf jeden Fall. 

**Tabelle: Outlook-Elementfeld zugeordneter Outlook-Elementtyp**


|**Outlook-Elementtyp**|**Outlook-Elementfeld**|
|:-----|:-----|
|Kontakt  <br/> |LastName  <br/> |
|Aufgabe  <br/> |Subject  <br/> |
|Termin  <br/> |Beginnt um, Endet um und Betreff  <br/> |
|Beitrag  <br/> |Subject  <br/> |
   
Nicht zugeordnete Felder werden je nach Anzahl wie folgt als erweiterte Eigenschaften angezeigt:
  
    
    

- **Benachbart** Wird dem Formularbereich unten auf der Standardseite eines Outlook-Formulars angefügt (2 bis 5 Felder).
    
  
- **Getrennt** Wird einem Outlook-Formular als neue Seite hinzugefügt (mindestens 6 Felder).
    
  

## <a name="set-up-the-external-item-picker-control"></a>Einrichten des Steuerelements für das Auswahltool für externe Elemente
<a name="section9"> </a>

Das Steuerelement für das Auswahltool für externe Elemente ermöglicht Benutzern das Auswählen eines Felds, z. B. eines ID-Felds oder eines Felds mit eindeutigen Werten, um ein Element bequem auszuwählen. Dieses Steuerelement steht in SharePoint- und Office 2013-Produkten zur Verfügung. Beispielsweise können Benutzer dieses Steuerelement nutzen, um in einer externen Liste von Kunden ein Element auswählen. In Word 2013 kann dieses Steuerelement mit Inhaltssteuerelementen verwendet werden, die mit externen Datenspalten verknüpft sind. Es ist ratsam, bestimmte Spalten auswählen, die Sie im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, weil standardmäßig alle Spalten angezeigt werden, was in den meisten Fällen nicht erforderlich ist.
  
    
    

1. Klicken Sie auf jedes Feld, das im Steuerelement für das Auswahltool für externe Elemente angezeigt werden soll, um es zu markieren, und aktivieren Sie dann unter **Eigenschaften** das Kontrollkästchen **In Auswahl anzeigen**.
    
  
2. Klicken Sie auf **Weiter**.
    
> [!NOTE]
> Alle Filter, die Sie definieren, werden im Steuerelement für das Auswahltool für externe Elemente angezeigt. Obwohl sich bestimmte Filter nicht aus dem Steuerelement für das Auswahltool für externe Elemente entfernen lassen, können Sie einen Standardfilter definieren, indem Sie im Dialogfeld **Filterkonfiguration** auf **Ist Standard** klicken, wenn Sie den Filter erstellen oder ändern.
  
    
    


## <a name="define-filters"></a>Definieren von Filtern
<a name="section10"> </a>

Wenn Sie keine Filter definieren, gibt eine externe Liste alle Daten bis zum Business Connectivity Services (BCS)-Grenzwert (standardmäßig 2.000 Elemente) bzw. alle Daten zurück, die im externen Inhaltstyp definiert sind, wenn die Menge unter dem aktuellen Grenzwert liegt. Darüber hinaus erfolgt die gesamte Verarbeitung der Ergebnisse innerhalb des SharePoint-Produkts. Es ist ratsam, mindestens einen Filter zu definieren. Im Allgemeinen gibt es zwei Arten von Filtern, die Sie kennen sollten:
  
    
    

- **Datenquellenfilter** Wenn Sie einen Filter für externe Inhaltstypen erstellen, der als Datenquellenfilter bezeichnet wird, erfolgt der Filtervorgang innerhalb der SQL Server-Datenbank. Dies ist wichtig, wenn Sie mit großen Datenmengen arbeiten, da Sie die Verarbeitung aus den SharePoint-Produkten in die externe Datenbank auslagern und sich Leistungsverbesserungen verschaffen können. Nachdem Sie die externe Liste erstellt haben, können Sie den Datenquellenfilter durch Erstellen einer Ansicht nutzen, die verschiedene Filterwerte im Abschnitt **Datenquellenfilter** der Einstellungsseite **Listenansicht** angibt.
    
  
- **SharePoint-Filter** Benutzer können Daten weiterhin mithilfe eines SharePoint-Filters filtern, entweder mit dem Spaltenüberschriftsfilter oder mithilfe des Abschnitts **Filter** auf der Einstellungsseite **Listenansicht**. In diesem Fall erfolgt der Filtervorgang im SharePoint-Produkt und nicht innerhalb der SQL Server-Datenbank.
    
  
Eine zu erwägende ratsame Strategie ist das Erstellen einer Gruppe externer Listenansichten basierend auf bestimmten Datenquellenfiltern, die sicherstellen, dass größere Datenmengen zuerst in der externen Datenquelle gefiltert werden. Anschließend können Benutzer weiter filtern und die Ergebnisse mithilfe von SharePoint-Filter optimieren.
  
    
    
Sie können verschiedene Arten von Filtern erstellen. Führen Sie für jeden Filter, den Sie erstellen, folgende Schritte aus:
  
    
    

1. Wählen Sie unter **Eigenschaften** neben **Datenquellenelement** ein Feld aus.
    
  
2. Klicken Sie unter **Eigenschaften** neben **Filter** auf **Zum Hinzufügen klicken**, um das Dialogfeld **Filterkonfiguration** anzuzeigen.
    
  
3. Klicken Sie auf **Filterparameter hinzufügen**.
    
  
4. Geben Sie im Feld **Neuer Filter** einen Namen für den Filter ein.
    
  
5. Wählen Sie im Feld **Filtertyp** einen Filtertyp aus:
    
    
  
    
    
 **Vergleiche**
  
    
    

    
    Ein Vergleichsfilter beschränkt, welche Elemente basierend auf einer Bedingung zurückgegeben werden (z. B. Bundesland = "Hessen") und wird in eine SQL-WHERE-Klausel umgewandelt.
    
1. Wählen Sie im Feld **Filtertyp** die Option **Vergleich** aus.
    
  
2. Wählen Sie im Feld **Operator** einen Vorgang aus.
    
  
3. Stellen Sie im Feld **Filterfeld** sicher, dass das Feld, das Sie vergleichen möchten, ausgewählt ist.
    
  
4. Wenn die vom Benutzer eingegebenen Werte hinsichtlich der Groß- und Kleinschreibung übereinstimmen sollen, wählen Sie **Groß-und Kleinschreibung**.
    
  
5. Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.
    
  
6. Klicken Sie auf **OK**.
    
  
7.  Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.
    
  

    
  
    
    
 **Platzhalter**
  
    
    

    
    Ein Platzhalterfilter beschränkt, welche Elemente basierend auf einem vom Benutzer angegebenen Zeichenfolgenwert (z. B. Zustand enthält "Neu") zurückgegeben werden, und wird in eine SQL-ähnliche Klausel konvertiert. Gültige SQL Server-Platzhalterzeichen sind \* (Sternchen), was bedeutet, dass eine beliebige Anzahl von Zeichen übereinstimmen muss, und \_ (Unterstrich), was bedeutet, dass nur ein einziges Zeichen übereinstimmen muss. 
  
    
    

    
1. Wählen Sie im Kontrollkästchen **Filtertyp** die Option **Platzhalter**.
    
  
2. Wählen Sie im Feld **Filterfeld** ein Feld aus.
    
  
3. Wenn die vom Benutzer eingegebenen Werte hinsichtlich der Groß- und Kleinschreibung übereinstimmen sollen, wählen Sie **Groß-und Kleinschreibung**.
    
  
4. Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.
    
  
5. Klicken Sie auf **OK**.
    
  
6.  Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt. Es ist ratsam, ein \* (Sternchen) als Standard einzugeben.
    
  

    
  
    
    
 **Grenze**
  
    
    

    
    In den meisten Fällen müssen Sie einen Limit-Filter für Lese- und Listenlesevorgänge definieren. Wenn Sie kein **Standardlimit** festlegen, werden aus der externen Datenquelle keine Daten abgerufen. Stellen Sie sicher, dass der Standardwert, den Sie für den Limit-Filter angeben, kleiner als 2.000 ist, da der Business Connectivity Services (BCS)-Standardgrenzwert 2.000 Elemente ist. Sie können diesen Grenzwert erhöhen, sollte dies erforderlich sein.
    
1. Wählen Sie im Feld **Filtertyp** die Option **Limit** aus. 
    
  
2. Geben Sie in das Kästchen **Anzahl** eine Zahl ein.
    
  
3. Wenn Sie eine Liste möglicher Übereinstimmungen im Steuerelement für das Auswahltool für externe Elemente anzeigen möchten, wenn mehr als ein übereinstimmendes Element vorhanden ist, aktivieren Sie **Zur Erstellung einer Übereinstimmungsliste im Auswahltool für externe Elemente verwenden**.
    
  
4. Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt.
    
  
5. Klicken Sie auf **OK**. 
  
    > [!NOTE]
    > Der SQL Server-Administrator kann zudem spezielle Tabellen, Ansichten, Indizes und optimierte Abfragen erstellen, um die Ergebnisse auf die benötigten Elemente zu beschränken und die Leistung zu verbessern. 

    
 **Seitenzahl**
  
    
    

    
    Verwenden Sie den externen Inhaltstyp Seitenzahl, um den SharePoint-Seitengrenzwert zu ersetzen, der auf der Seite **Listenansicht** der externen Liste festgelegt ist. Dies sind die Unterschiede:
    
  - Beim externen Inhaltstyp Seitenzahl werden zuerst die Ergebnisse innerhalb der SQL Server-Datenbank verarbeitet. Dann nur wird die Anzahl der Zeilen zurückgegeben und angezeigt, die vom Wert Seitengröße bestimmt wird.
    
  
  - Beim SharePoint-Seitengrenzwert werden alle Zeilen bis zur Größe von Standardwert aus der SQL Server-Datenbank zurückgegeben. Anschließend wird die Anzahl der Zeilen angezeigt, die vom SharePoint-Seitengrenzwert auf der Einstellungsseite **Listenansicht** bestimmt wird.
    
  

    Die Verwendung der externen Inhaltstyp-Seitenzahl ist im Allgemeinen effizienter. Darüber hinaus hilft der Wert der **Reihenfolge** sicherzustellen, dass eine genaue Anzeige der Ergebnisse zurückgegeben wird.
    
1. Wählen Sie im Kontrollkästchen **Filtertyp** die Option **Seitenzahl**. 
    
  
2. Geben Sie in das Feld **Seitenzahl** eine Zahl ein.
    
  
3. Wählen Sie im Feld **Reihenfolge** eine Sortierrichtung aus.
    
  
4. Klicken Sie auf **OK**. 
    
  
5. Geben Sie unter **Eigenschaften** neben **Standardwert** den ersten Wert ein, nach dem gefiltert werden soll, wenn der Benutzer keinen Wert eingibt. Wenn Sie keinen Wert eingeben, werden von der externen Liste keine Elemente angezeigt. 
  
    
    

    
  
6. Wenn Sie ein Feld anzeigen, aber nicht ändern möchten, klicken Sie auf das Feld, um es zu markieren, und klicken Sie dann unter **Eigenschaften** auf **Schreibgeschützt**.
    
  
7. Falls Sie sicherstellen möchten, dass ein Feld immer einen Wert enthält, wenn es erstellt oder geändert wird, klicken Sie auf das Feld, um es zu markieren, und klicken Sie dann unter **Eigenschaften** auf **Erforderlich**.
    
  
8. Wenn Sie im Steuerelement für das Auswahltool für externe Elemente für den Namen in **Datenquellenelement**, der vom SQL Server-Spaltennamen abgeleitet ist, einen beschreibenden Namen angeben möchten, klicken Sie auf das Feld, um es zu markieren, und geben Sie dann unter **Eigenschaften** in das Feld **Anzeigename** einen Namen ein.
    
  
9. Zum Definieren eines Standardwerts für den Filter (der auch im Abschnitt **Datenquellenfilter** auf der Einstellungsseite **Listenansicht** angezeigt wird) klicken Sie unter **Filterparameter** auf den Filter, um ihn zu markieren. Geben Sie dann in das Feld **Standardwert** den gewünschten Wert ein. Wenn Sie keinen Wert eingeben, werden beim ersten Verwenden dieses Filters keine Elemente angezeigt.
    
  

## <a name="set-the-title-field-for-an-external-list"></a>Festlegen des Felds "Titel" für eine externe Liste
<a name="section11"> </a>


1. Klicken Sie auf dem Menüband auf **Zusammenfassungsansicht**.
    
  
2. Wählen Sie im Abschnitt **Felder** unter **Feldname** ein Feld.
    
    > **Wichtig:** Im Allgemeinen ist es ratsam, dass der Titel aus einem Feld mit einem eindeutigen Wert besteht. Das Titelfeld wird zum Anzeigen der Liste oder InfoPath-Formulare verwendet. Nachdem Sie das Titelfeld festgelegt haben, können Sie es nicht mehr ändern. 
3. Klicken Sie auf dem Menüband auf **Als Titel festlegen**.
    
  

## <a name="complete-the-external-content-type"></a>Vervollständigen des externen Inhaltstyps
<a name="section12"> </a>


- Klicken Sie auf der Symbolleiste für den Schnellzugriff auf **Speichern**. Dadurch wird die Definition des externen Inhaltstyps im Business Data Connectivity-Metadatenspeicher gespeichert.
    
> [!NOTE]
> Um eine bessere Leistung zu bieten, speichert Business Data Connectivity alle Objekte im Metadatenspeicher zwischen und nimmt Änderungen mithilfe eines Zeitgeberauftrags vor, der minütlich ausgeführt wird. Es kann bis zu einer Minute dauern, bis Änderungen von allen Servern in der Farm übernommen wurden, erfolgen aber auf dem Server unmittelbar, auf dem Sie die Änderungen vornehmen. 
  
    
    

Den hinzugefügten Benutzern steht jetzt der externe Inhaltstyp für die Verwendung in SharePoint- und Office 2013-Produkten zur Verfügung.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="AR"> </a>


-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Deploy a Business Connectivity Services on-premises solution in SharePoint](http://msdn.microsoft.com/library/4692ebba-90eb-4d72-ac12-e90c4d4ee7ae.aspx)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Configure the Secure Store Service in SharePoint](http://msdn.microsoft.com/library/29C0BC76-D835-401B-A2FB-ABB069E84125.aspx)
    
  

