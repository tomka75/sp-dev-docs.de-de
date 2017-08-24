
# <a name="three-ways-to-think-about-design-options-for-sharepoint-add-ins"></a>Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen
Der Artikel enthält eine Übersicht über die verfügbaren Entwurfs- und Architekturoptionen für SharePoint-Add-Ins. Zuvor sollten Sie sich mit dem Artikel  [SharePoint-Add-Ins](sharepoint-add-ins) vertraut machen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="overview-and-the-first-decision"></a>Übersicht und erste Entscheidung
<a name="Overview"> </a>

In diesem Artikel werden die architekturbezogenen Entscheidungen für SharePoint-Add-Ins unter drei Aspekten erläutert. Zunächst lernen Sie die wichtigsten Kategorien der Entwurfsentscheidungen kennen. Anschließend wird die Add-In-Architektur im Hinblick auf Anwendungsebenen betrachtet. Und schließlich werden Faktoren beleuchtet, die Sie bei Ihren Entwurfsentscheidungen berücksichtigen sollten.
 

 
Als Erstes müssen Sie entscheiden, ob Ihre SharePoint-Erweiterung eine SharePoint-Add-In oder eine klassische SharePoint-Farmlösung oder Sandkastenlösung darstellen soll. Einige Teile des SharePoint-Objektmodells, vor allem in Verbindung mit der Anpassung der SharePoint-Verwaltung und -Sicherheit, sind für Clients nicht zugänglich. Auf diese Teile kann nur von auf dem SharePoint-Server ausgeführtem benutzerdefiniertem Code zugegriffen werden. Benutzerdefinierter serverseitiger Code ist in einer SharePoint-Add-In nicht zulässig. (Über einen umfangreichen Satz von Clientobjektmodellen und einen REST/OData-Dienst können SharePoint-Add-Ins nahezu jede endbenutzerorientierte SharePoint-Erweiterung ausführen.) Weitere Informationen zur Entscheidung zwischen klassischen Lösungen und Add-Ins finden Sie unter  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx). Ebenfalls hilfreich für diese Entscheidung ist der Artikel  [Auswählen des richtigen API-Satzes in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).
 

 

## <a name="key-elements-in-the-design-of-sharepoint-add-ins"></a>Schlüsselelemente beim Entwurf von SharePoint-Add-Ins
<a name="MajorCategoriesOfChoices"> </a>

Beim Entwerfen einer SharePoint-Add-In sind im Wesentlichen drei Kategorien von Entscheidungen zu fällen. Wie immer sind beim Anwendungsentwurf bestimmte Abwägungen zu treffen. Entscheidungen in einer Kategorie können die Optionen in einer anderen beeinflussen. Nicht jede mögliche Kombination von Entscheidungen ist umsetzbar.
 

 

-  **Hosting:** SharePoint-Add-Ins können bezüglich ihrer Bereitstellung und ihres Hostings in zwei Haupttypen unterschieden werden.
    
      -  Bei **vom Anbieter gehosteten** Add-Ins werden der primäre Datenspeicher und die Geschäftslogik von Ihnen als dem Entwickler außerhalb von SharePoint auf von Ihnen bereitgestellten Servern oder in einem Cloudkonto bereitgestellt und gehostet. Sie sind zuständig für die Isolation zwischen den Konten der Kunden, die Ihr Add-In erwerben. Solche Add-Ins können auch SharePoint-Komponenten enthalten. Diese werden in der SharePoint-Farm des Kunden gehostet. Dieser Add-In-Typ bietet Ihnen in den anderen Kategorien von Entwurfsentscheidungen die meiste Flexibilität. Zudem können Sie nicht von Microsoft stammende Plattformen für die externen Daten, die Logik und die Webbenutzeroberfläche verwenden. (Innerhalb der Kategorie der vom Anbieter gehosteten Add-Ins müssen Sie unterscheiden zwischen Add-Ins, deren Remotekomponenten innerhalb derselben Unternehmensfirewall wie die SharePoint-Farm liegen, und solchen, deren Remotekomponenten außerhalb dieser Firewall liegen. Bei diesen beiden Szenarien werden unterschiedliche Autorisierungssysteme verwendet. Dies hat wiederum Auswirkungen auf die verwendbare Programmiersprache für den Zugriff auf die SharePoint-Daten.)
    
 
  -  In **SharePoint gehostete** Add-Ins bestehen ausschließlich aus SharePoint-Komponenten, wie Listen, Inhaltstypen, Workflows und Webparts. Es gibt keine externen Komponenten. Weitere Informationen zu den Arten von SharePoint-Komponenten, die in SharePoint-Add-Ins enthalten sein können, finden Sie unter [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).
    
 

    Ausführlichere Informationen zu den Hostingoptionen von SharePoint-Add-Ins finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres SharePoint-Add-Ins](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in).
    
 
-  **Konnektivität:** In SharePoint werden drei Arten von sicherem Zugriff zum Erstellen/Lesen/Aktualisieren/Löschen (Create/Read/Update/Delete, CRUD) auf Daten unterstützt.
    
      - Externe Webanwendungen in einem Add-In verwenden das OAuth-Protokoll zum Zugriff auf SharePoint-Daten. Weitere Informationen finden Sie unter  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins).
    
 
  - Der Zugriff von JavaScript auf Daten in einem SharePoint-Add-In-Web und Daten auf anderen Websites innerhalb desselben Mandanten erfolgt mithilfe einer besonderen JavaScript-Bibliothek, die sicheres domänenübergreifendes Skripting ermöglicht. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).
    
 
  - Eine SharePoint-Add-In kann auch über Business Connectivity Services (BCS) oder einen Webdienstproxy auf externe Daten zugreifen. Weitere Informationen finden Sie unter  [Business Connectivity Services in SharePoint](http://msdn.microsoft.com/library/64b7d032-4b83-4e9e-bc08-f0a161af5457%28Office.15%29.aspx) and [Abfragen eines Remotediensts mithilfe des Webproxys in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint-2013).
    
 

    Weitere Informationen zu Datenspeicherung und -zugriff in SharePoint-Add-Ins finden Sie unter  [Datenspeicher in Add-Ins für SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape#Data),  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins) und [Arbeiten mit externen Daten in SharePoint](work-with-external-data-in-sharepoint-2013).
    
 
-  **Benutzeroberfläche:** Eine SharePoint-Add-In kann auf drei Arten in SharePoint dargestellt werden: Alle Add-Ins werden zumindest auf einer vollständigen Webseite dargestellt. Optional kann ein Add-In auch durch ein Add-In-Webpart und durch ein Menüelement oder eine Menübandschaltfläche dargestellt werden. Weitere Informationen finden Sie unter [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins).
    
     **Hinweis** SharePoint-Add-Ins können von den Kunden in mehreren Websitesammlungen eines Mandanten oder auf einzelnen Websites installiert werden. Erstere werden als Add-Ins mit Mandantenbereich bezeichnet. Wenn Sie den Kunden die Option des Mandantenbereichs bieten möchten, können Sie keine benutzerdefinierte Menübandschaltfläche und kein Add-In-Webpart einschließen. Weitere Informationen finden Sie unter [Mandantschaften und Bereitstellungsbereiche von SharePoint-Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins).

## <a name="architectural-tiers"></a>Architekturebenen
<a name="Tiers"> </a>

Eine andere Sicht auf die Architekturoptionen Ihres Add-Ins besteht darin, die drei logischen Ebenen des Add-Ins zu betrachten: Benutzeroberfläche, Geschäftslogik und Datenzugriff. Für jede Ebene bestehen mehrere Implementierungsoptionen. Auch hier haben Entscheidungen für eine Ebene Auswirkungen auf die Optionen anderer Ebenen. In den folgenden Tabellen sind die Optionen für die Remotekomponenten eines Add-Ins und die SharePoint-Komponenten zusammen mit ihrer Verwendung beschrieben.
 

 

**Remotekomponenten in vom Anbieter gehosteten Add-Ins: Optionen für die einzelnen Ebenen**


|**Ebene**|**Optionen**|**Vorteil**|
|:-----|:-----|:-----|
|Benutzeroberfläche|ASP.NET-Seiten in einem ASP.NET-Formular oder einer MVC-Anwendung, gehostet in einer Microsoft Azure-Webrolle.|Nutzen der Erfahrung von ASP.NET-Entwicklungsmitarbeitern.|
||HTML 5-Seite mit JavaScript.|Reichhaltige Benutzeroberfläche.|
||PHP- oder andere Webseite, gehostet in einem nicht von Microsoft bereitgestellten Clouddienst.|Integrieren von nicht von Microsoft stammenden Anwendungen in SharePoint.|
||Silverlight in einer Windows Phone-App.|Mobiler Zugriff auf SharePoint-Daten und Integration mit Geolocation-Daten und Push-Benachrichtigungen.|
|Geschäftslogik|Clientseitiges JavaScript.|Benutzeroberflächenlogik und einfache Geschäftslogik. Zugriff auf SharePoint-Daten über das JavaScript-Clientobjektmodell. |
||Eine Microsoft Azure-Workerrolle.|Prozessorintensive Funktionalität. Zugriff auf SharePoint-Daten über das .NET Framework-Clientobjektmodell.|
||Ein Remotewebdienst.|Prozessorintensive Funktionalität. Zugriff auf SharePoint-Daten über das .NET Framework-Clientobjektmodell.|
|Daten|SQL Azure.|Relationale Daten mit vollem Funktionsumfang.|
||Microsoft Azure-Tabellenspeicherung.|Anwendungseinstellungen und andere Metadaten.|
||Microsoft Azure-BLOB-Speicherung.|Speicherung großer Dateien.|
||Ein nicht von Microsoft bereitgestellter Clouddienst.|Nutzen vorhandener Datenquellen auf Basis nicht von Microsoft stammender Plattformen.|
||Eine Datenbank auf dem eigenen Server des Entwicklers.|Hosting durch den Anbieter und Kontrolle der Mandantenisolation durch den Entwickler.|

**SharePoint-Komponenten: Optionen für die einzelnen Ebenen**


|**Ebene**|**Optionen**|**Vorteil**|
|:-----|:-----|:-----|
|Benutzeroberfläche|Benutzerdefinierte Ansichten von Listen und Bibliotheken von SharePoint auf Add-In-Webseiten. |Optimale Integration in die Darstellung und das Verhalten von SharePoint.|
||Silverlight-Anwendung, gehostet in einem Webpart (oder in <object>-Tags) auf einer Add-In-Webseite.|Nutzen vorhandener Erfahrungen bei der Silverlight-Entwicklung. Umfassende Benutzeroberfläche.|
|Geschäftslogik|Ein SharePoint-Workflow.|Implementieren von Geschäftsprozessen.|
||Clientseitiges JavaScript, ergänzt durch die domänenübergreifende SharePoint-Bibliothek.|Zugriff auf SharePoint-Daten im Add-In-Web. Zugriff auf Daten auf anderen Websites des Mandanten.|
||Ein Remoteereignishandler.|Behandeln von CRUD-Ereignissen in SharePoint-Listen und Bibliotheken mit extern gehosteter Logik|
|Daten|Listen und Bibliotheken von SharePoint, die über Collaborative Application Markup Language (CAML)- oder LINQ-Abfragen mit einem der SharePoint-Clientobjektmodelle abgefragt werden.|Nutzen vorhandener Erfahrungen bei der SharePoint- und .NET Framework-Entwicklung.|
||Listen und Bibliotheken von SharePoint, die über den SharePoint REST/OData-Webdienst abgefragt werden.|Zugriff auf SharePoint-Daten von nicht von Microsoft stammenden Plattformen. Nutzen vorhandener Erfahrungen mit OData-Abfragen.|
||Ein BCS-Modell.|Darstellung externer Daten in SharePoint als SharePoint-Liste.|

## <a name="factors-to-consider-when-making-your-design-decisions"></a>Bei Entwurfsentscheidungen zu berücksichtigende Faktoren
<a name="DecisionFactors"> </a>

Das SharePoint-Add-In-Modell bietet so viele Entwurfsmöglichkeiten, dass sich keine einfache Entscheidungsstruktur dafür erstellen lässt. Im Folgenden sind einige der wichtigsten Faktoren aufgeführt, die bei der Erwägung der Architektur einer SharePoint-Add-In zu berücksichtigen sind.
 

 

- Der wichtigste Faktor ist die Funktionalität, die Sie den Kunden zur Verfügung stellen möchten, d. h. die Anwendungsfälle. Enthält Ihr Add-In beispielsweise prozessorintensive Funktionen, wie z. B. die Konvertierung von Videodateien in ein anderes Videoformat, spricht dies für ein vom Anbieter gehostetes Add-In, bei der die Verarbeitung auf einem Ihrer Server oder in einer Microsoft Azure-Workerrolle erfolgt.
    
 
- Da bei einer Art von SharePoint-Add-In (vom Anbieter gehostete Add-Ins) Sie (oder Ihr Kunde) die Nicht-SharePoint-Komponenten hosten und die Mandantenisolation erzwingen müssen, sollten Sie bedenken, ob Sie (bzw. die Zielkunden) über die entsprechende Hardware und das erforderliche IT-Personal verfügen.
    
 
- Die Kundenzielgruppe stellt ebenfalls einen wichtigen Faktor dar. Werden alle Ihre Add-Ins innerhalb des Unternehmens (d. h., Sie haben keine externen Kunden) oder von einem einzelnen Kunden verwendet werden, sind vom Anbieter gehostete Add-Ins wesentlich einfacher zu implementieren und zu warten, als wenn Sie externe Kunden bedienen oder mehrere Kunden das Add-In nutzen. Falls Sie das Add-In öffentlich vertreiben möchten, sollten Sie auch überlegen, ob Sie sie an Unternehmen mit SharePoint Online-Konten oder solche mit eigenen SharePoint-Farmen oder beides vermarkten möchten.
    
 
- Sie sollten auch Ihre vorhandenen Fachkenntnisse und Erfahrungen bzw. die Ihres Entwicklungspersonals berücksichtigen. Sind Sie beispielsweise ein erfahrener ASP.NET-Entwickler, spricht dies für das Erstellen einer Remotewebanwendung und die Darstellung von SharePoint-Listendaten in einem Rastersteuerelement auf einer ASP.NET-Seite. Sind Sie dagegen ein erfahrener SharePoint-Entwickler, ist dies ein Argument für die Verwendung einer benutzerdefinierten SharePoint-Liste und -Websiteseite mit JavaScript zur Verarbeitung.
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AdditionalResources"> </a>


-  [Entwerfen von SharePoint-Add-Ins](design-sharepoint-add-ins)
    
 
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

