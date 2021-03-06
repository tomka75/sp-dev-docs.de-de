# <a name="create-sharepoint-add-ins-in-visual-studio"></a>Erstellen von SharePoint-Add-Ins in Visual Studio
Erfahren Sie, wie Sie SharePoint-Add-Ins mithilfe von Vorlagen für Projekte und Projektelemente in Visual Studio entwickeln.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Sie können SharePoint Add-Ins mithilfe neuer Vorlagen für Projekte und Projektelemente in **vsnv** erstellen. 
 

## <a name="project-templates"></a>Projektvorlagen
<a name="SP15Projecttemplates_templates"> </a>

Wenn Sie eine Projektvorlage in Visual Studio verwenden, erstellt diese eine Projektmappe mit den Projektelementen und -dateien, die für den Projekttyp erforderlich sind. Die folgenden Projektvorlagen werden im Dialogfeld **Neues Projekt** angezeigt, wenn Sie den Knoten **Office/SharePoint** und dann den Knoten **Add-Ins** auswählen. Informationen über die Projektvorlagen unter dem Knoten **SharePoint-Lösungen** finden Sie im Artikel über [SharePoint-Projekt- und -Projektelementvorlagen](http://go.microsoft.com/fwlink/?LinkId=255306). 
 

 

### <a name="office-add-in"></a>Office-Add-In

Erstellt eine Webseite, die in einer Office-Anwendung wie Excel oder Outlook gehostet wird. Eine Office-Add-In liefert zusätzliche Inhalte und Funktionen in einem Dokument oder Outlook-Element. Weitere Informationen finden Sie unter  [Office-Add-Ins-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).
 

 

### <a name="sharepoint-add-in"></a>SharePoint-Add-In

Erstellt ein SharePoint-Add-In basierend auf den Informationen, die Sie in einem Assistenten eingeben. Zu diesen Informationen gehören folgende Angaben.
 

 

- Der Name des Add-Ins
    
 
- Die lokale SharePoint-Website oder die SharePoint-Remotewebsite für das Debugging Ihres Add-Ins.
    
 
- Der Typ des Add-Ins, das Sie erstellen möchten: von einem Provider gehostet oder von SharePoint gehostet. 
    
 
Weitere Informationen finden Sie unter [SharePoint-Add-Ins](sharepoint-add-ins).
 

 

### <a name="cloud-business-add-in"></a>Cloud-Business-Add-In

Mithilfe der Vorlage **Cloud-Business-Add-In** in Visual Studio können Sie ein in SharePoint gehostetes Add-In erstellen, in dem mobile Benutzer an einem Remotestandort mithilfe moderner Geräte wie Smartphones und Tablet-PCs mit Toucheingabe Daten anzeigen, hinzufügen und aktualisieren können. Weitere Informationen finden Sie unter [Erstellen von Cloud-Geschäfts-Add-Ins](create-cloud-business-add-ins).
 

 

## <a name="project-item-templates"></a>Projektelementvorlagen
<a name="SP15Projecttemplates_items"> </a>

Nach Erstellung einer SharePoint-Lösung können Sie Projektelemente anhand der folgenden Vorlagen hinzufügen, die im Dialogfeld **Neues Element hinzufügen** unter dem Knoten **Office/SharePoint** angezeigt werden.
 

 

### <a name="office-add-in"></a>Office-Add-In

Fügt Ihrem SharePoint-Add-In ein Office-Add-In hinzu. Sie können ein Aufgabenbereichs-, ein Inhalts- oder ein Mail-Add-In erstellen. Weitere Informationen finden Sie unter  [Office-Add-Ins-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).
 

 

### <a name="client-web-part-host-web"></a>Clientwebpart (Hostweb)

Fügt Ihrem SharePoint-Add-In ein Clientwebpart hinzu. Durch Hinzufügen eines Clientwebparts können Sie Add-Ins auf den Seiten einer Hostwebsite anzeigen. Diese Vorlage enthält eine einzelne Datei vom Typ "Elements.xml", deren Eigenschaften die folgenden Elemente des Clientwebparts definieren:
 

 


|**Eigenschaftenname**|**Beschreibung**|
|:-----|:-----|
|ClientWebPart|Gibt den Namen, den Titel, die Beschreibung und die Dimensionen des Clientwebparts an.|
|Content|Definiert den Speicherort der Seite, die innerhalb des Clientwebparts gerendert wird. Das Element verfügt über zwei Eigenschaften: `Type` und `Src`. `Type` gibt den Typ des Webparts an, das Sie erstellen, beispielsweise HTML. `Src` definiert den Speicherort der Seite, die innerhalb des Clientwebparts gerendert wird. Die Vorlage verweist unter Verwendung des Schemas _ _Eigenschaftsname__ auf Eigenschaften in der Abfragezeichenfolge. Beispiel: `Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`Weitere Informationen finden Sie unter [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in).|

### <a name="content-type"></a>Inhaltstyp

Fügt Ihrem SharePoint-Add-In einen Inhaltstyp hinzu, ähnlich wie bei Inhaltstypen, die in früheren Version von SharePoint verwendet wurden. Ein Inhaltstyp ist ein Satz von Metadaten, Workflows und Verhaltensweisen für eine Kategorie von Elementen in einer SharePoint-Liste oder -Bibliothek. Beispielsweise ist ein Element ein Listeninhaltstyp. Andere Listeninhaltstypen sind z. B. Ankündigungen, Kontakte und Aufgaben, und sie erben vom Inhaltstyp Element. Der Inhaltstyp Kontakt enthält Spalten wie **Vorname**, **Nachname** und **Position**.
 

 
Wenn Sie Ihrem SharePoint-Add-In einen Inhaltstyp hinzufügen, geben Sie den Basisinhaltstyp an, von dem der neue Inhaltstyp erben soll. Eine Vererbung ist beispielsweise von einer Ankündigung, einem Kontakt, einem Dokument oder von einem Element möglich. Danach konfigurieren Sie mit dem **Inhaltstyp**-Designer die Spalten für den Inhaltstyp und dessen Eigenschaften (wie Name und Beschreibung). Die von Ihnen gewählten Werte werden den Elementen `ContentType` und `FieldRef` in der Datei „Elements.xml“ hinzugefügt. Weitere Informationen finden Sie unter [Baustein: Inhaltstypen](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).
 

 

### <a name="empty-element"></a>Leeres Element

Fügt Ihrer SharePoint-Add-In ein Projektelement für ein leeres Element hinzu. Dieses Projektelement enthält eine einzelne Datei (ELEMENTS.XML), in der Sie die Eigenschaften des Elements festlegen. Ein leeres Element wird in der Regel zur Definition eines Elements verwendet, für das Visual Studio keine Vorlage bereitstellt.
 

 

### <a name="list"></a>Liste

Fügt Ihrem SharePoint-Add-In zwei Projektelemente hinzu: eine Listendefinition und eine Instanz der Liste. Wenn Sie Ihrem Add-In eine Liste hinzufügen, geben Sie an, wie die Liste genannt werden soll und ob eine leere Liste oder eine auf einem bestehenden Listentyp basierende Liste erstellt werden soll. Zudem geben Sie an, ob die Liste angepasst werden kann. Danach konfigurieren Sie mit dem **Listendesigner** die Spalten und Ansichten für die Liste sowie weitere Eigenschaften, wie den Namen und die Beschreibung der Liste. Weitere Informationen über Listeneigenschaften finden Sie unter [ListTemplate-Element (Listenvorlage)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) und [ListInstance-Element (Listeninstanz)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).
 

 

### <a name="menu-item-custom-action"></a>Benutzerdefinierte Aktion für Menüelement

Fügt ein Projektelement hinzu, das die Benutzeroberfläche der entsprechenden Hostwebsite erweitert, indem einem Listenmenü eine Aktion hinzugefügt wird. Die benutzerdefinierte Menüaktion umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins).
 

 

### <a name="module"></a>Modul

Fügt Ihrem SharePoint-Add-In ein Modul-Projektelement hinzu. Module sind einfach ausgedrückt Behälter, mit denen Sie bei der Bereitstellung Ihres SharePoint-Add-Ins weitere Dateien einschließen können. Um eine Datei hinzuzufügen, kopieren Sie sie unter dem Modul im **Projektmappen-Explorer** in das Projekt. Ein Verweis auf die Datei wird der Datei ELEMENTS. XML für das Modul automatisch hinzugefügt. Der Verweis enthält den Pfad und die URL der neuen Datei. Die Datei SAMPLE.TXT für das Modul können Sie löschen, da sie lediglich als Beispiel dient.
 

 

### <a name="remote-event-receiver"></a>Remoteereignisempfänger

Fügt Ihrer SharePoint-Add-In ein Projektelement für einen Remoteereignisempfänger und Ihrer Lösung ein Webanwendungsprojekt hinzu, sofern noch kein solches Projekt vorhanden ist. Die Webanwendung enthält einen Webdienst, der dem Remoteereignisempfänger in Ihrer SharePoint-Add-In zugeordnet ist. Der Webdienst enthält eine Visual Basic- oder Visual C#-Codedatei, deren Code ausgeführt wird, wenn in der SharePoint-Add-In ein Listen-, ein Listenelement- oder ein Webelementereignis auftritt. Wenn eine Webanwendung vorhanden ist, wird sie der SharePoint-Add-In zugeordnet, und der Webdienst wird der Anwendung hinzugefügt. Weitere Informationen finden Sie unter  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins).
 

 

### <a name="ribbon-custom-action"></a>Benutzerdefinierte Menübandaktion

Fügt ein Projektelement hinzu, das die Benutzeroberfläche der entsprechenden Hostwebsite erweitert, indem einem Menüband eine Aktion hinzugefügt wird. Die benutzerdefinierte Menübandaktion umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins).
 

 

### <a name="search-configuration"></a>Suchkonfiguration

Fügt ein Projektelement hinzu, das Ihnen das Importieren benutzerdefinierter Suchkonfigurationseinstellungen ermöglicht, die von einer SharePoint-Website exportiert wurden.
 

 

### <a name="site-column"></a>Websitespalte

Fügt Ihrer SharePoint-Add-In ein Projektelement für eine Websitespalte hinzu. Die Websitespalte enthält eine Datei ELEMENTS.XML, die die  `Field`-Eigenschaften der Websitespalte definiert, einschließlich der folgenden Daten.
 

 


|**Eigenschaftenname**|**Beschreibung**|
|:-----|:-----|
|ID|Ein eindeutiger GUID-Wert für die Websitespalte.|
|Name|Ein eindeutiger Name, der als Verweis auf die Websitespalte dient.|
|DisplayName|Ein auf der Benutzeroberfläche angezeigter Anzeigename.|
|Type|Der Datentyp der Websitespalte, der auf **SPFieldType** basiert, z. B. Boolesch, Nachschlagedaten oder Text.|
|Required|Wenn die Spalte erforderlich ist, wird die Eigenschaft auf **True** festgelegt; anderenfalls wird die Eigenschaft auf **False** festgelegt.|
|Group|Gibt den Namen der Gruppe an, der die Websitespalte zugeordnet ist. Der Standardwert für diese Eigenschaft lautet **Spalten benutzerdef. Website**.|
Weitere Informationen finden Sie unter [Baustein: Spalten und Feldtypen](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).
 

 

### <a name="workflow"></a>Workflow

Fügt Ihrer SharePoint-Add-In ein Projektelement für einen Microsoft Azure-Workflow hinzu. Weitere Informationen finden Sie unter  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). Wenn Sie diese Art von Element hinzufügen, geben Sie einen Namen für den Workflow an und definieren ihn als Listen- oder Website-Workflow. Ein Listenworkflow funktioniert nur mit einer Liste und ein Website-Workflow nur mit der SharePoint-Website. Bei der Erstellung des Workflows legen Sie zudem fest, ob dem Workflow automatisch Listen und Bibliotheken zugeordnet werden sollen, und wenn ja, welche. Für jede Zuordnung, die Sie hinzufügen, wird dem Workflowprojekt eine Datei hinzugefügt. Ein Workflow enthält die folgenden Dateien.
 

 


|**Dateiname**|**Beschreibung**|
|:-----|:-----|
|Elements.xml|Gibt die Konfiguration des Workflows und die darin enthaltenen Dateien an, wie die Datei WORKFLOW.XAML und Zuordnungsdateien, sowie die Eigenschaften jeder Datei, wie URL, Typ und Pfad. Für jede Datei, die dem Workflowprojekt hinzugefügt wird, wird in der Datei ELEMENTS.XML für den Workflow ein entsprechender Bereich erstellt. Zuordnungsdateien in Listenworkflows erfordern eine Liste, damit sie über einen Verweis auf das Listentoken verfügen. In einem Website-Workflow wird eine GUID für die Website hinzugefügt. **Vorsicht** Da Visual Studio die Elemente in der Datei ELEMENTS.XML beibehält, raten wir von einer Änderung der Datei ab, es sei denn, Sie kennen die Auswirkungen der Änderungen genau. |
|Workflow.xaml|Der Designer für den Workflow. In dieser Datei können Sie dem Workflow Aktionen hinzufügen und deren Code und Eigenschaften festlegen.|
|WorkflowStartAssociation|Startet den Workflow manuell in SharePoint. Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Benutzer startet den Workflow manuell** im Workflow-Assistenten aktivieren.|
|ItemAddedAssociation|Startet den Workflow manuell, sofern einer vorhanden ist, wenn ein Benutzer ein Element auf der Website oder in der Liste erstellt (je nach Workflowtyp). Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Der Workflow wird automatisch gestartet, wenn ein Element hinzugefügt wird** im Workflow-Assistenten aktivieren.|
|ItemUpdatedAssociation|Startet den Workflow automatisch, sofern einer vorhanden ist, wenn ein Benutzer ein Element auf der Website oder in der Liste ändert (je nach Workflowtyp). Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Der Workflow wird automatisch gestartet, wenn ein Element geändert wird** im Workflow-Assistenten aktivieren.|
|WorkflowHistoryList|Die Datei, die dem Workflowprojekt hinzugefügt wird, wenn eine Verlaufsliste für den Workflow im Workflow-Assistenten erstellt werden soll.|
|WorkflowTaskList|Die Datei, die dem Workflowprojekt hinzugefügt wird, wenn eine Aufgabenliste für den Workflow im Workflow-Assistenten erstellt werden soll.|

### <a name="workflow-custom-activity"></a>Benutzerdefinierte Workflowaktivität

Fügt Ihrer SharePoint-Add-In ein Projektelement für eine benutzerdefinierte Workflowaktivität hinzu. Durch Hinzufügen einer benutzerdefinierten Workflowaktivität können Sie zusätzliche Workflowaktionen erstellen, die dann als benutzerdefinierte Aktionen in SharePoint Designer 2013 importiert werden können. Die benutzerdefinierte Workflowaktivität umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden, sowie eine XAML-Datei für den Workflow-Designer. Weitere Informationen finden Sie unter  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).
 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Projecttemplates_addlresources"> </a>


-  [Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins](tools-and-environments-for-developing-sharepoint-add-ins)
    
 
