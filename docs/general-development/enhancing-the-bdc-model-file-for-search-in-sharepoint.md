---
title: "Optimieren der BDC-Modelldatei für die Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c67b1cf-5fca-4805-a1b5-c9ac1ff8aede
ms.openlocfilehash: 7ec597c113aec7f5a017dbe233e6a89ef416ec07
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="enhancing-the-bdc-model-file-for-search-in-sharepoint"></a>Optimieren der BDC-Modelldatei für die Suche in SharePoint
Informationen Sie zu den Eigenschaften im BDC-Metadatenmodell, die die BCS-indizierungskonnektoren betreffen die Suche in SharePoint zum Durchforsten der externer Daten zu ermöglichen.
## <a name="search-properties-for-bdc-model-files"></a>Sucheigenschaften für BDC-Modelldateien
<a name="SearchBDCModelProperties_SearchProperties"> </a>

Das konnektorframework in Suche können Sie zum Durchforsten der externer Daten, die in den Suchergebnissen über BCS-indizierungskonnektoren verfügbar zu machen. BCS-Indizierungsconnector wird vom Crawler verwendet, mit der externen Datenquelle kommunizieren. Bei der Durchforstung ruft der Crawler den BCS-Indizierungsconnector zum Abrufen der Daten aus dem externen System, und geben Sie ihn an dem Crawler. 
  
    
    
BCS-Indizierungsconnectors bestehen aus Folgendem:
  
    
    


  
    
    
> **BDC-Modelldatei** Die Datei, die Verbindungsinformationen für das externe System und die Struktur der Daten bereitstellt.
    
  

  
    
    
> **Connector** Die Komponente mit dem Code, der eine Verbindung mit dem externen System und analysiert das Access-URLs und BCS-IDs.
    
  
Das BDC-Metadatenmodell enthält verschiedene Eigenschaften, die gelten für Suche, von die viele zur Unterstützung von BCS-Indizierungsconnector Durchforstung erforderlich sind. 
  
    
    
In der folgenden Tabelle wird beschrieben, die BDC-Modell-Eigenschaften, die auf Suche angewendet werden.
  
    
    

**Tabelle 1. Suchdiensteigenschaften für BDC-Modelldateien**


|**Name**|**Metadatenobjekt**|**Beschreibung**|
|:-----|:-----|:-----|
|ShowInSearchUI  <br/> |Model  <br/> |Gibt an, dass ein **LobSystemInstance**-Element in der Modelldatei in der Benutzeroberfläche des Suchdiensts angezeigt werden soll. Dieser Wert wird für benutzerdefinierte Konnektoren ignoriert.<br/> |
|InputUriProcessor  <br/> |LobSystem  <br/> |Gibt den Namen der Klasse, die die eingegebene URL vor der Übergabe an den Connector verarbeitet. Gilt für .NET und benutzerdefinierten BCS Indizierung Connectors. Weitere Informationen finden Sie unter  [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).<br/> |
|OutputUriProcessor  <br/> |LobSystem  <br/> |Gibt den Namen der Klasse, die die URL für die Ausgabe vor der Übergabe an das Suchsystem aus den Connector verarbeitet. Gilt für .NET und benutzerdefinierten BCS Indizierung Connectors. Weitere Informationen finden Sie unter  [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).<br/> |
|SystemUtilityTypeName  <br/> |LobSystem  <br/> |Gibt den Namen der Klasse, die die **StructuredRepositorySystemUtility** -Klasse implementiert. Gilt für benutzerdefinierte BCS Indizierung Connectors. Weitere Informationen finden Sie unter [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx). <br/> |
|Title  <br/> |Entität  <br/> |Gibt den Titel des externen Inhaltstyps an, der in Suchergebnissen angezeigt werden soll.  <br/> |
|DefaultLocale  <br/> |Entität  <br/> |Gibt die Gebietsschema-Zeichenfolge an. Diesen Wert können Sie mit der **LCIDField**-Eigenschaft oder der **CultureField**-Eigenschaft überschreiben. <br/> |
|RootFinder  <br/> |Methode  <br/> |Gibt die **Finder**-Methode an, die zum Aufzählen der zu durchforstenden Elemente verwendet werden soll. Beispielsweise könnte dies beim Herstellen einer Verbindung mit einer Datenbank die **SELECT**-Anweisung oder die Liste der zu durchforstenden Tabellen sein. <br/> |
|DirectoryLink  <br/> |Methode  <br/> |Gibt an, dass BCS Zuordnungen navigieren soll. Erforderlich für das hierarchische crawlen.  <br/> |
|DeletedCountField  <br/> |Methode  <br/> |Gibt den Wert für die Anzahl gelöschter Elemente an. Diese Eigenschaft wird ignoriert, außer sie enthält eine ganze Zahl, die größer als Null ist.  <br/> |
|WindowsSecurityDescriptorField  <br/> |Methode  <br/> |Gibt die Windows-Sicherheitsbeschreibung für das Element an. Wenn diese Eigenschaft nicht angegeben ist, wird die **GetSecurityDescriptor**-Methode aufgerufen. Wenn **GetSecurityDescriptor** nicht definiert ist, werden alle externen Elemente der Zugriffssteuerungsliste (Access Control List, ACL) "Jeder" zugewiesen. <br/> |
|AuthorField  <br/> |Methode  <br/> |Gibt den Namen des Autors an, der in Suchergebnissen angezeigt werden soll.  <br/> |
|DisplayUriField  <br/> |Methode  <br/> |Gibt die URL in den Suchergebnissen angezeigt. Wenn angegeben, überschreibt diese Eigenschaft die URL für die Profile von BCS bereitgestellt. Wenn nicht angegeben wird, beginnt die URL in den Suchergebnissen angezeigt mit **bdc3: / /**, und wird nicht vom Browser verstanden.<br/> |
|LastModifiedTimeStampField  <br/> |Methode  <br/> |Gibt den Zeitstempel des externen Elements an, der in Suchergebnissen angezeigt werden soll. Dieser Wert wird auch für die inkrementelle Durchforstung verwendet.  <br/> |
|DescriptionField  <br/> |Methode  <br/> |Gibt die Beschreibung an, die in Suchergebnissen angezeigt werden soll.  <br/> |
|LCIDField  <br/> |Methode  <br/> |Gibt die Gebietsschema-ID (LCID) für **DescriptionField** an. Wenn diese Eigenschaft nicht angegeben ist, wird die standardmäßige Wörtertrennung verwendet.<br/> |
|CultureField  <br/> |Methode  <br/> |Gibt die Kultur für **DescriptionField** an.  <br/> |
|Extension  <br/> |Methode  <br/> |Gibt die Dateinamenerweiterung für den Datenstrom an, der durchforstet werden kann. Wenn diese Eigenschaft nicht angegeben ist, lautet die Standarderweiterung **.txt**.<br/> |
|MimeType  <br/> |Methode  <br/> |Gibt den MIME-Typ für den Datenstrom an, der durchforstet werden kann. Wenn diese Eigenschaft nicht angegeben ist, lautet die Standarderweiterung **.txt**. Wenn die Felder **Extension** und **MimeType** beide angegeben sind, wird der im Feld angegebene **MimeType** Wert verwendet. <br/> |
|UseClientCachingForSearch  <br/> |Methode  <br/> |Gibt an, ob der Crawler den Inhalt während Enumeration zwischengespeichert. Wenn der Inhalt zwischengespeichert wird, werden der Crawler keine gestellt einer anderen Reise zur Inhaltsquelle beim Crawlen einzelne Elemente.  <br/> |
|EnumerateIdsOnly  <br/> |FilterDescriptor  <br/> |Gibt an, ob in **IDEnumerator** nur IDs zurückgegeben werden sollen.  <br/> |
|CrawlStartTime  <br/> |FilterDescriptor  <br/> |Enthält die Startzeit der letzten Durchforstung.  <br/> |
|SynchronizationCookie  <br/> |FilterDescriptor  <br/> |Gibt an, dass die externe Inhaltsquelle nach einer Durchforstung ein Cookie zurückgibt, das anschließend vom Indizierungskonnektor während des nächsten Aufzählungsaufrufs erneut gesendet wird. Die externe Inhaltsquelle nutzt das Cookie, um zu bestimmen, was sich seit der letzten Durchforstung geändert hat. Diese Eigenschaft wird mit Instanzen der Methoden **ChangedIDEnumerator** und **DeletedIDEnumerator** verwendet. <br/> |
|Property  <br/> |TypeDescriptor  <br/> | Gibt das **struct**-Array an, das bei der Suche nach Eigenschaften verwendet wird und aus Folgendem besteht:<br/> <ul><li>**PropertyName**</li><li>**PropertyValue**</li><li>**PropertyCulture**</li></ul> |
|Text  <br/> |TypeDescriptor  <br/> | Gibt das **struct**-Array an, das von der Suche für Anlagen verwendet wird. Dies besteht aus Folgendem:<br/> <ul><li>**TextExtension**</li><li>**TextContentType**</li><li>**TextValue**</li></ul> <br/> |
   

## <a name="bdc-model-file-changes-to-improve-performance-when-crawling-external-data"></a>BDC-Modell Datei Änderungen zum Verbessern der Leistung beim Crawlen von externer Daten
<a name="SearchBDCModelProperties_Performance"> </a>

Wenn Sie möchten eine BDC-Modelldatei für ein externes System zu erstellen, die Sie für die Suche aktivieren möchten, können Sie die Modelldatei zum Optimieren der Leistung beim Durchforsten externer Systeme verbessern. In diesem Abschnitt werden Verfahren zum Ändern der BDC-Modelldatei zum Verbessern der Leistung.
  
    
    

### <a name="use-inline-property-io-when-retrieving-large-scale-data"></a>Verwenden der eingebetteten Eigenschafts-E/A beim Abrufen großer Datenmengen

Wenn für ein einzelnes Element große Datenmengen zurückgegeben werden, sollten Sie für die Rückgabe generell nicht die **SpecificFinder**-Methode, sondern eine der folgenden Spezialmethoden zum Abrufen der Daten verwenden:
  
    
    

- Verwenden Sie die **BinarySecurityDescriptorAccessor**-Methode, wenn eine Sicherheits-Zugriffssteuerungsliste (Security Access Control List, SACL) anstelle der **WindowsSecurityDescriptor**-Eigenschaft übergeben wird.
    
  
- Verwenden Sie zum Übergeben von Datenströmen die **StreamAccessor**-Methode.
    
  
Außer bei einer langen Netzwerkwartezeit ist die Leistung meist besser als bei einem zusätzlichen Abrufvorgang des externen Systems.
  
    
    

### <a name="enumeration-optimization-when-crawling-external-systems"></a>Aufzählungsoptimierung beim Durchforsten externer Systeme

Zählen Sie pro Aufruf an das externe System nicht mehr als 100.000 Elemente auf. Lang andauernde Aufzählungen können zwischenzeitliche Unterbrechungen verursachen und den Abschluss einer Durchforstung verhindern. Es wird empfohlen, dass Ihr BDC-Modell die Daten in logischen Ordnern strukturiert, die einzeln aufgezählt werden können (siehe das folgende Beispiel). 
  
    
    
Dieses Beispiel veranschaulicht das Aufzählen für eine Datenbanktabelle mit einer Million Zeilen, aber mit einer festen Gruppe von Werten in der Spalte "ColumnA". In diesem Szenario können Sie "ColumnA" als den externen Inhaltstyp betrachten und mithilfe der folgenden SQL-Anweisung einen Enumerator für diese Wertegruppe schreiben. 
  
    
    



```sql

SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table
```

Definieren Sie nun mit der folgenden SQL-Anweisung den spezifischen Finder. 
  
    
    



```sql
SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table where ColumnA = @Value
```

Schließlich müssen Sie den Zuordnungsnavigationsvorgang wie folgt definieren. 
  
    
    



```sql
Select * from table where ColumnA=@value
```

Eine Methode muss binnen zwei Minuten mit der Rückgabe von Ergebnissen beginnen. Andernfalls bricht der Crawler den Aufruf ab. Die Ausführung einer komplexen SQL-Anweisung mit der **LIKE**-Klausel kann beispielsweise länger als zwei Minuten dauern, was den Crawler zum Abbrechen des Aufrufs veranlassen würde.
  
    
    

### <a name="improving-crawl-speed-with-the-useclientcachingforsearch-property"></a>Erhöhen der Durchforstungsgeschwindigkeit mithilfe der "UseClientCachingForSearch"-Eigenschaft

Die **UseClientCachingForSearch**-Eigenschaft beschleunigt vollständige Durchforstungen, indem das Element während der Aufzählung zwischengespeichert wird. Diese Eigenschaft wird auch empfohlen, wenn inkrementelle auf Änderungsprotokollen basierende Durchforstungen implementiert werden, da dadurch inkrementelle Durchforstungen beschleunigt.
  
    
    

> **Wichtig:** Wenn Elemente durchschnittlich größer als 30 KB sind, legen Sie diese Eigenschaft nicht fest, da sie eine beträchtliche Anzahl von Cachefehlern verursacht und Leistungsvorteile zunichte macht. 
  
    
    


## <a name="security-in-bdc-model-files"></a>Sicherheit in BDC-Modelldateien
<a name="SearchBDCModelProperties_Security"> </a>

Wenn das Repository die NTLM-Authentifizierung verwendet, wird empfohlen, für Durchforstungen die PassThrough-Authentifizierung zu aktivieren.
  
    
    
Profilseiten können erfordern, dass Sie den Dienst für Einmaliges Anmelden aufgrund des Delegierungsproblems bei Mehrfachhops auf dem Front-End-Webserver verwenden müssen. Bei Auftreten dieses Problems können Sie die Durchforstung optimieren und gleichzeitig das Erstellen von Profilseiten zulassen, indem Sie zwei ähnliche **LobSystemInstance**-Instanzen erstellen. Die erste Instanz muss Anmeldeinformationen aus der Authentifizierung für Einmaliges Anmelden verwenden. Diese Instanz darf nicht die **ShowInSearchUI**-Eigenschaft enthalten. Die zweite Instanz muss die PassThrough-Authentifizierung verwenden und die **ShowInSearchUI**-Eigenschaft enthalten. Profilseiten verwenden die erste **LobSystemInstance**-Instanz, der Crawler die zweite Instanz.
  
    
    

> **Hinweis:** Dies erfordert, dass Sie die **ShowInSearchUI**-Eigenschaft auf **LobSystemInstance**-Ebene anstatt auf **LobSystem**-Ebene festlegen.
  
    
    


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15enhanceBDC_addlresources"> </a>


-  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Infrastruktur des BDC-Modells](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)
    
  
-  [Erstellen von BDC-Modellen](http://msdn.microsoft.com/library/170d1cfd-cf19-4162-b79f-ba6d3b4ad23b%28Office.15%29.aspx)
    
  
-  [Einrichten einer Entwicklungsumgebung für BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen einer BDC-Modelldatei für einen benutzerdefinierten Konnektor in SharePoint Designer](http://msdn.microsoft.com/library/8f239482-0c82-4b60-817d-b0c4392e7e2e%28Office.15%29.aspx)
    
  

