# <a name="design-sharepoint-add-ins"></a>Entwerfen von SharePoint-Add-Ins
In diesem Artikel erhalten Sie einen Überblick über die in SharePoint-Add-Ins verfügbaren Entwurfs- und Architekturoptionen und erfahren, wie Sie die richtigen Entscheidungen treffen, um die Entwicklung Ihrer Add-Ins in SharePoint zu erleichtern.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Angenommen, Sie haben eine großartige Idee für ein Add-In. In diesem Abschnitt führen wir Sie durch die erforderlichen Entwurfsentscheidungen und stellen bewährte Methoden für die Erstellung Ihres Add-Ins bereit. Was macht zum Beispiel eine gute Benutzeroberfläche aus? Welche Add-In-"Formen" sind verfügbar? Nach welchen Kriterien sollten diese ausgewählt werden? Welche Optionen stehen für den Datenzugriff zur Verfügung? 
 

## <a name="start-designing-sharepoint-add-ins"></a>Starten des Entwurfs von SharePoint-Add-Ins
<a name="SP15Design_Startdesigning"> </a>

Da das Cloud-Add-In-Modell in SharePoint so viele Designoptionen ermöglicht, können SharePoint-Add-Ins die unterschiedlichsten Formen und Größen haben. Dieser Abschnitt liefert nützliche Tipps für einige der wichtigsten Entscheidungen, die Sie bei der Planung und beim Entwurf der Architektur und der Benutzerfreundlichkeit Ihres Add-Ins treffen müssen. Dazu zählen das Hosting Ihres Add-Ins, der effiziente und sichere Zugriff auf Daten und die Benutzung.
 

 
Eine Übersicht über die Design- und Architekturoptionen für SharePoint-Add-Ins finden Sie unter  [Drei Ansätze, um Entwurfsentscheidungen für Add-Ins für SharePoint zu treffen](three-ways-to-think-about-design-options-for-sharepoint-add-ins). Worum es sich bei den SharePoint-Add-Ins handelt, erfahren Sie unter  [SharePoint-Add-Ins](sharepoint-add-ins).
 

 

## <a name="choose-the-right-hosting-model-for-your-add-in"></a>Wählen des richtigen Hostingmodells für Ihr Add-In
<a name="SP15Design_Hostingmodel"> </a>

SharePoint-Add-Ins unterstützen mehrere Hostingoptionen. Sie können Ihren eigenen Webstapel wählen, Microsoft mit der Bereitstellung von Microsoft Azure und SQL Azure beauftragen oder das Add-In auf SharePoint hosten. In Tabelle 1 ist ein Artikel aufgeführt, der Ihnen bei der Auswahl des richtigen Hostingmodells für Ihr Add-In hilft.
 

 

**Tabelle 1. Ressourcen und Anweisungen für die Wahl des richtigen Hostingmodells für SharePoint-Add-Ins**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Auswählen von Mustern für die Entwicklung und das Hosten Ihres SharePoint-Add-Ins](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)|Lernen Sie die verschiedenen Methoden zum Hosten der Komponenten von SharePoint-Add-Ins kennen.|

## <a name="choose-the-right-data-access-technologies-for-your-add-in"></a>Wählen der richtigen Datenzugriffstechnologien für Ihr Add-In
<a name="SP15Design_Dataaccess"> </a>

Sie müssen sicherstellen, dass Ihr Add-In effizient und sicher auf Daten zugreift. Für den Zugriff auf SharePoint und die Arbeit mit Daten in Ihrem Add-In stehen verschiedene Datenzugriffstechnologien zur Verfügung. In Tabelle 2 ist ein Artikel aufgeführt, in dem Sie erfahren, welche Optionen es gibt und wie Sie die richtige für Ihr Add-In auswählen. 
 

 

**Tabelle 2. Ressourcen und Anweisungen für die Wahl der Datenzugriffstechnologien zur Verwendung in SharePoint-Add-Ins**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins)| In diesem Artikel erfahren Sie, welche Datenzugriffsoptionen Sie bei der Erstellung von SharePoint-Add-Ins haben. Erläutert werden auch die Datenkonnektivitätsoptionen für eingehende und ausgehende Daten sowie die APIs, die für den Zugriff auf SharePoint von Ihrem Add-In aus zur Verfügung stehen.|

## <a name="design-the-ux-for-your-add-in"></a>Entwerfen der Benutzeroberfläche für Ihr Add-In
<a name="SP15Design_UX"> </a>

Bei der Entwicklung eines Add-Ins sollte es Ihnen vor allem darauf ankommen, dass das Add-In so benutzerfreundlich ist, dass Benutzer die vorgesehenen Funktionen ausführen können. In Tabelle 3 ist ein Artikel aufgeführt, der erläutert, wie Sie erstklassige Add-Ins entwickeln, die bewährten Anforderungen an die Benutzerfreundlichkeit genügen und deren Gestalt und Funktionsweise sich an SharePoint anlehnt.
 

 

**Tabelle 3. Ressourcen und Anweisungen für das Entwerfen einer ansprechenden Benutzeroberfläche für SharePoint-Add-Ins**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)|Hier erfahren Sie mehr über die UX (User Experience)-Optionen, die Ihnen beim Erstellen von SharePoint-Add-Ins zur Verfügung stehen.|

## <a name="design-with-update-in-mind"></a>Berücksichtigen späterer Updates beim Entwurf
<a name="Upgrade"> </a>

Irgendwann möchten Sie ein Update Ihres Add-Ins erstellen und in den Office Store oder den Add-In-Katalog eines Unternehmens hochladen. Dies ist erheblich einfacher, wenn Sie spätere Updates des Add-Ins bereits beim Entwurf der ersten Version berücksichtigen. Daher sollten Sie die folgenden Artikel zu einem frühen Zeitpunkt in der Entwurfsphase lesen:  [Aktualisierungsverfahren für Add-Ins für SharePoint](sharepoint-add-ins-update-process) und [Aktualisieren von Add-Ins für SharePoint](update-sharepoint-add-ins). 
 

 

## <a name="next-steps-develop-and-publish-your-add-in"></a>Nächste Schritte: Entwickeln und Veröffentlichen Ihres Add-Ins
<a name="SP15Design_Next"> </a>

Haben Sie ein solides Konzept für Ihr Add-In? Dann können Sie direkt mit der Erstellung des Add-Ins und seiner Veröffentlichung loslegen. Die in Tabelle 4 aufgeführten Artikel helfen Ihnen dabei.
 

 

**Tabelle 4. Ressourcen und Anweisungen für die Entwicklung und Veröffentlichung von SharePoint-Add-Ins**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Entwickeln von SharePoint-Add-Ins](develop-sharepoint-add-ins)|Erläutert erweiterte Konzepte und Funktionen des Add-In-Modells.|
| [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins)|Beschreibt das Verfahren und die Anforderungen für die Veröffentlichung von SharePoint-Add-Ins.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Design_AddRes"> </a>


-  [Beispielpaket für SharePoint-Add-Ins](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)
    
 
-  [Reimagine SharePoint development](http://msdn.microsoft.com/en-US/office/apps/dn133840)
    
 
-  [SharePoint-Add-Ins](sharepoint-add-ins)
    
 
-  [Entwickeln von SharePoint-Add-Ins](develop-sharepoint-add-ins)
    
 
-  [Blog für Add-Ins](http://blogs.msdn.com/b/spoffapps)
    
 

