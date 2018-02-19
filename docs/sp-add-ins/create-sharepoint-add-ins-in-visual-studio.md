---
title: Erstellen von SharePoint-Add-Ins in Visual Studio
description: "Entwickeln von SharePoint-Add-Ins mithilfe von Vorlagen für Projekte und Projektelemente in Visual Studio"
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 826498c45f6cb8a7cff0bd7c07a6ff3ebd339928
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-sharepoint-add-ins-in-visual-studio"></a>Erstellen von SharePoint-Add-Ins in Visual Studio

Sie können SharePoint Add-Ins mithilfe neuer Vorlagen für Projekte und Projektelemente in **vsnv** erstellen. 
 
<a name="SP15Projecttemplates_templates"> </a>
## <a name="project-templates"></a>Projektvorlagen

Wenn Sie eine Projektvorlage in Visual Studio verwenden, wird eine Lösung erstellt, die die für den Projekttyp erforderlichen Projektelemente und Dateien enthält. Folgende Projektvorlagen werden im Dialogfeld **Neues Projekt** angezeigt, wenn Sie den Knoten **Office/SharePoint** erweitern und dann den Knoten **Add-Ins** wählen. Informationen zu Projektvorlagen unter dem Knoten **SharePoint-Lösungen** finden Sie unter [Vorlagen für SharePoint-Projekte und Projektelemente](http://go.microsoft.com/fwlink/?LinkId=255306). 

### <a name="office-add-in"></a>Office-Add-In

Erstellt eine Webseite, die in einer Office-Anwendung wie Excel oder Outlook gehostet wird. Ein Office-Add-In enthält zusätzliche Inhalte und Funktionen in Dokumenten und Outlook-Elementen. 

Weitere Informationen finden Sie unter [Office-Add-In-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).

### <a name="sharepoint-add-in"></a>SharePoint-Add-In

Erstellt ein SharePoint-Add-In basierend auf den Informationen, die Sie in einem Assistenten eingeben. Zu diesen Informationen gehören folgende Angaben.

- Der Name des Add-Ins
- Die lokale SharePoint-Website oder die SharePoint-Remotewebsite für das Debugging Ihres Add-Ins.
- Der Typ des Add-Ins, das Sie erstellen möchten: von einem Provider gehostet oder von SharePoint gehostet. 

Weitere Informationen finden Sie unter [SharePoint-Add-Ins](sharepoint-add-ins.md).

<a name="SP15Projecttemplates_items"> </a>
## <a name="project-item-templates"></a>Projektelementvorlagen

Nach Erstellung einer SharePoint-Lösung können Sie Projektelemente anhand der folgenden Vorlagen hinzufügen, die im Dialogfeld **Neues Element hinzufügen** unter dem Knoten **Office/SharePoint** angezeigt werden.

### <a name="office-add-in"></a>Office-Add-In

Fügt ein Office-Add-In zu Ihrem SharePoint-Add-In. Sie können ein Aufgabenbereich-Add-In, ein Inhalts-Add-In oder ein E-Mail-Add-In hinzufügen. 

Weitere Informationen finden Sie unter [Office-Add-In-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).

### <a name="client-web-part-host-web"></a>Clientwebpart (Hostweb)

Fügt Ihrem SharePoint-Add-In ein Clientwebpart hinzu. Durch Hinzufügen eines Clientwebparts können Sie Add-Ins auf den Seiten einer Hostwebsite anzeigen. Diese Vorlage enthält eine einzelne Datei vom Typ "Elements.xml", deren Eigenschaften die folgenden Elemente des Clientwebparts definieren:

|**Eigenschaftenname**|**Beschreibung**|
|:-----|:-----|
|ClientWebPart|Gibt den Namen, den Titel, die Beschreibung und die Dimensionen des Clientwebparts an.|
|Inhalt|Definiert die Position der Seite, die im Clientwebpart gerendert wird. Dieses Element verfügt über zwei Eigenschaften: `Type` und `Src`.<br/>`Type` gibt den Typ des zu erstellenden Webparts an, z. B. HTML.<br/>`Src` definiert die Position der Seite, die im Clientwebpart gerendert wird.<br/>Die Vorlage verweist mit dem Muster __PropertyName__, z. B.`Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`, auf die Eigenschaften in der Abfragezeichenfolge.<br/><br/>Weitere Informationen finden Sie unter [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).|

### <a name="content-type"></a>Inhaltstyp

Fügt Ihrer SharePoint-Add-In einen Inhaltstyp hinzu, ähnlich wie bei Inhaltstypen, die in früheren Version von SharePoint verwendet wurden. Ein Inhaltstyp ist ein Satz Metadaten, Workflows und Verhaltensweisen für eine Kategorie von Elementen in einer SharePoint-Liste oder -Bibliothek. Beispielsweise ist ein Element ein Listeninhaltstyp. Andere Listeninhaltstypen sind z. B. Ankündigungen, Kontakte und Aufgaben, und sie erben vom Inhaltstyp Element. Der Inhaltstyp Kontakt enthält Spalten wie **Vorname**, **Nachname** und **Position**.

Wenn Sie einen Inhaltstyp im SharePoint-Add-In hinzufügen möchten, müssen Sie den grundlegenden Inhaltstyp angeben, von dem der neue Inhaltstyp erbt. Er kann zum Beispiel von einer Ankündigung, einem Kontakt, einem Dokument oder einem Inhaltstypelement erben. Sie verwenden dann den Designer für **Inhaltstypen**, um die Spalten für den Inhaltstyp und die zugehörigen Eigenschaften wie Name und Beschreibung zu konfigurieren. Die von Ihnen angegebenen Werte werden den `ContentType`- und `FieldRef`-Elemente in der Datei „Elements.xml“ hinzugefügt. 

Weitere Informationen finden Sie unter [Baustein: SharePoint 2010-Inhaltstypen](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).

### <a name="empty-element"></a>Leeres Element

Fügt Ihrer SharePoint-Add-In ein Projektelement für ein leeres Element hinzu. Dieses Projektelement enthält eine einzelne Datei (ELEMENTS.XML), in der Sie die Eigenschaften des Elements festlegen. Ein leeres Element wird in der Regel zur Definition eines Elements verwendet, für das Visual Studio keine Vorlage bereitstellt.

### <a name="list"></a>Liste

Fügt zwei Projektelemente zum SharePoint-Add-In hinzu: eine Listendefinition und eine Instanz der Liste. Wenn Sie eine Liste zu Ihrem Add-In hinzufügen, müssen Sie den Namen für die Liste sowie angeben, ob eine leere Liste oder eine Liste auf Grundlage eines vorhandenen Listentyps erstellt werden soll. Sie müssen auch angeben, ob die Liste angepasst werden kann. Anschließend verwenden Sie den **Listen-Designer** zum Konfigurieren der Spalten und Ansichten für die Liste und anderer Eigenschaften wie Name und Beschreibung der Liste. 

Weitere Informationen zu Listeneigenschaften finden Sie unter [ListTemplate-Element (Listenvorlage)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) und [ListInstance-Element (Listeninstanz)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).

### <a name="menu-item-custom-action"></a>Benutzerdefinierte Aktion für Menüelement

Fügt ein Projektelement hinzu, das die Benutzeroberfläche der Hostwebsite durch Hinzufügen einer Aktion zu einem Listenmenü erweitert. Die benutzerdefinierte Menüaktion enthält eine Datei „Elements.xml“, die Sie zum Definieren der Eigenschaften der Aktion verwenden. 

Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).

### <a name="module"></a>Modul

Fügt Ihrer SharePoint-Add-In ein Modul-Projektelement hinzu. Module sind einfach ausgedrückt Behälter, mit denen Sie bei der Bereitstellung Ihrer SharePoint-Add-In weitere Dateien einschließen können. Um eine Datei hinzuzufügen, kopieren Sie sie unter dem Modul im **Projektmappen-Explorer** in das Projekt. Ein Verweis auf die Datei wird der Datei ELEMENTS. XML für das Modul automatisch hinzugefügt. Der Verweis enthält den Pfad und die URL der neuen Datei. Die Datei SAMPLE.TXT für das Modul können Sie löschen, da sie lediglich als Beispiel dient.

### <a name="remote-event-receiver"></a>Remoteereignisempfänger

Fügt Ihrem SharePoint-Add-In ein Projektelement für einen Remoteereignisempfänger und Ihrer Lösung ein Webanwendungsprojekt hinzu, wenn ein solches Projekt noch nicht vorhanden ist. Die Webanwendung enthält einen Webdienst, der dem Remoteereignisempfänger in dem SharePoint-Add-In zugeordnet ist. Der Webdienst enthält eine Visual Basic- oder Visual C#-Codedatei, deren Code ausgeführt wird, wenn eine Liste, ein Listenelement oder ein Webelementereignis im SharePoint-Add-In vorkommt. Wenn eine Webanwendung vorhanden ist, wird sie dem SharePoint-Add-In zugeordnet, und der Webdienst wird der Anwendung hinzugefügt. 

Weitere Informationen finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md).

### <a name="ribbon-custom-action"></a>Benutzerdefinierte Menübandaktion

Fügt ein Projektelement hinzu, das die Benutzeroberfläche der Hostwebsite durch Hinzufügen einer Aktion zu einem Menüband erweitert. Die benutzerdefinierte Menübandaktion enthält eine Datei „Elements.xml“, die die Eigenschaften der Aktion definiert. 

Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).

### <a name="search-configuration"></a>Suchkonfiguration

Fügt ein Projektelement hinzu, das Ihnen das Importieren benutzerdefinierter Suchkonfigurationseinstellungen ermöglicht, die von einer SharePoint-Website exportiert wurden.

### <a name="site-column"></a>Websitespalte

Fügt dem SharePoint-Add-In ein Projektelement für eine Websitespalte hinzu. Die Websitespalte enthält eine Datei „Elements.xml“, die die **Field**-Eigenschaften der Websitespalte definiert, einschließlich der folgenden Daten.

|**Eigenschaftenname**|**Beschreibung**|
|:-----|:-----|
|ID|Ein eindeutiger GUID-Wert für die Websitespalte.|
|Name|Ein eindeutiger Name, der als Verweis auf die Websitespalte dient.|
|DisplayName|Ein auf der Benutzeroberfläche angezeigter Anzeigename.|
|Typ|Der Datentyp der Websitespalte, der auf **SPFieldType** basiert, z. B. Boolesch, Nachschlagedaten oder Text.|
|Erforderlich|Wenn die Spalte erforderlich ist, wird die Eigenschaft auf **True** festgelegt; anderenfalls wird die Eigenschaft auf **False** festgelegt.|
|Gruppe|Gibt den Namen der Gruppe an, der die Websitespalte zugeordnet ist. Der Standardwert für diese Eigenschaft lautet **Spalten benutzerdef. Website**.|

Weitere Informationen finden Sie unter [Baustein: Spalten und Feldtypen](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).

### <a name="workflow"></a>Workflow

Fügt dem SharePoint-Add-In ein Projektelement für einen Microsoft Azure-Workflow hinzu. Weitere Informationen finden Sie unter [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). 

Wenn Sie diesen Typ von Element hinzufügen möchten, geben Sie einen Namen für den Workflow sowie an, ob es sich dabei um einen Listen- oder Websiteworkflow handelt. Wie aus den Namen bereits hervorgeht, funktioniert ein Listenworkflow nur mit einer Liste und ein Websiteworkflow nur mit der SharePoint-Website. Wenn Sie den Workflow erstellen, müssen Sie angeben, ob der Workflow automatisch Listen und Bibliotheken zugeordnet werden soll, und wenn ja, welchen. Für jede Zuordnung, die Sie hinzufügen, wird dem Workflowprojekt eine Datei hinzugefügt. Ein Workflow beinhaltet folgende Dateien.

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

Fügt dem SharePoint-Add-In ein Projektelement für eine benutzerdefinierte Workflowaktivität hinzu. Beim Hinzufügen einer benutzerdefinierten Workflowaktivität können Sie zusätzliche Workflowaktionen erstellen, die Sie dann als benutzerdefinierte Aktionen im SharePoint-Designer importieren können. Die benutzerdefinierte Workflowaktivität enthält eine Datei „Elements.xml“, die die Eigenschaften der Aktion definiert, und eine XAML-Datei für den Workflow-Designer. 

Weitere Informationen finden Sie unter [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).

## <a name="see-also"></a>Weitere Artikel
<a name="SP15Projecttemplates_addlresources"> </a>

- [Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins](tools-and-environments-for-developing-sharepoint-add-ins.md)
    
 
