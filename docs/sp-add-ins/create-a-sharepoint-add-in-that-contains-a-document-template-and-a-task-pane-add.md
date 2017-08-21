# <a name="create-a-sharepoint-add-in-that-contains-a-document-template-and-a-task-pane-add-in"></a>Erstellen eines SharePoint-Add-Ins, das eine Dokumentvorlage und ein Aufgabenbereich-Add-In enthält
Verwenden Sie Visual Studio, um ein Office-Add-In zu entwickeln, das in einem Dokument angezeigt wird, das von einem SharePoint-Add-In geöffnet wird.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Sie können ein SharePoint-Add-In erstellen, das eine Dokumentenvorlage enthält (z. B. eine Spesenabrechnung). Das Dokument kann ein Add-In für den Aufgabenbereich enthalten, das mit SharePoint-Daten interagiert. Beispielsweise können Benutzer die Felder einer Rechnung ausfüllen, indem sie Daten aus den Business Connectivity Services (BCS) verwenden, oder eine Spesenabrechnung erstellen, indem sie eine Spesenkategorie in einer SharePoint-Liste auswählen.
 

This walkthrough shows you how to create a SharePoint-Add-In that includes an Excel workbook. The Excel workbook contains a task pane add-in that uses the REST interface provided by SharePoint to populate a drop-down list box with SharePoint date in the task pane add-in.
 


## <a name="prerequisites"></a>Voraussetzungen
<a name="Prerequisites"> </a>

Installieren Sie die folgenden Komponenten, bevor Sie beginnen:
 

 

 

 

- Eine SharePoint-Entwicklungsumgebung:
    
      - To develop SharePoint-Add-Ins that target SharePoint in Office 365, see  [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/en-us/library/office/apps/fp161179%28v=office.15%29).
    
 
  - Informationen zum Entwickeln von SharePoint-Add-Ins für eine lokale SharePoint-Installation finden Sie unter [Vorgehensweise: Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/en-us/library/office/apps/fp179923%28v=office.15%29).
    
 
-  [Visual Studio 2015 und die Microsoft Office Developer Tools](https://www.visualstudio.com/features/office-tools-vs)
    
 
- Excel 2013 oder ein Office 365-Konto.
    
 

## <a name="create-a-sharepoint-add-in-project-in-visual-studio"></a>Erstellen eines SharePoint-Add-In-Projekts in Visual Studio
<a name="Create"> </a>


1. Starten Sie Visual Studio.
    
 
2. Wählen Sie auf der Menüleiste die Optionen  **Datei**,  **Neu**,  **Projekt**.
    
    Das Dialogfeld **Neues Projekt** wird geöffnet.
    
 
3. Erweitern Sie im Vorlagenbereich unter dem Knoten für die gewünschte Sprache  **Office/ SharePoint**, und wählen Sie dann  **Office-Add-Ins** aus.
    
 
4. Wählen Sie in der Liste der Projekttypen die Option  **SharePoint-Add-In** aus, benennen Sie das ProjektOfficeEnabledAddin, und wählen Sie dann die Schaltfläche  **OK** aus.
    
    Das Dialogfeld **Neues SharePoint-Add-In** wird angezeigt.
    
 
5. Wählen Sie in der Dropdownliste  **Welche SharePoint-Website soll für das Debugging Ihres Add-Ins verwendet werden?** die URL einer SharePoint-Website aus, oder geben Sie eine ein.
    
 
6. Wählen Sie in der Dropdownliste  **Wie soll Ihr SharePoint-Add-In gehostet werden?** die Option **SharePoint-Hosting** und dann **Weiter** aus.
    
     **Hinweis**Dieses Szenario funktioniert nur mit den Optionen „Von SharePoint gehostet“ und „Von Anbieter gehostet“ in der Dropdownliste **Wie soll Ihr SharePoint-Add-In gehostet werden?**.
7. Wählen Sie auf der nächsten Seite **SharePoint** aus, und klicken Sie dann auf die Schaltfläche **Fertig stellen**, um das Dialogfeld zu schließen.
    
 

## <a name="add-a-task-pane-add-in-item"></a>Hinzufügen eines Elements für ein Aufgabenbereich-Add-In
<a name="Add"> </a>

Fügen Sie dem Projekt als Nächstes ein Office-Add-In hinzu. Sie können ein beliebiges Add-In hinzufügen. In dieser exemplarischen Vorgehensweise haben wir uns für ein Add-In für den Aufgabenbereich entschieden.
 

 

1. Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.
    
 
2. Wählen Sie im Menü  **Projekt** die Option **Neues Element hinzufügen** aus.
    
 
3. Wählen Sie im Menü  **Neues Element hinzufügen** die Option **Office/SharePoint** und dann **Office-Add-In** aus.
    
 
4. Nennen Sie das Add-In für den Aufgabenbereich MyTaskPaneAddin, und wählen Sie dann die Schaltfläche  **Hinzufügen** aus.
    
    Das Dialogfeld **Add-In für Office erstellen** wird geöffnet.
    
 
5. Wählen Sie im Dialogfeld  **Add-In für Office erstellen** die Option **Aufgabenbereich** und dann **Weiter**. Deaktivieren Sie auf der nächsten Seite die Kontrollkästchen  **Word** und **PowerPoint**, und wählen Sie dann  **Weiter** aus.
    
 
6. Wählen Sie auf der Seite  **Soll Ihr Office-Add-In in einem neuen Dokument oder in einem vorhandenen Dokument angezeigt werden?** die Option **Neues Dokument erstellen und Add-In einfügen** und dann die Schaltfläche **Fertig stellen** aus.
    
    Visual Studio fügt eine Dokumentbibliothek und eine Arbeitsmappenvorlage für die Bibliothek hinzu.  Die Arbeitsmappe beinhaltet ein Add-In für den Aufgabenbereich.
    
 

## <a name="add-a-document-library"></a>Hinzufügen einer Dokumentbibliothek
<a name="Library"> </a>

In diesem Verfahren erstellen Sie eine Dokumentbibliothek und legen die Arbeitsmappe als Standardvorlage für die Dokumentbibliothek fest.
 

 

1. Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.
    
 
2. Wählen Sie im Menü  **Projekt** die Option **Neues Element hinzufügen** aus.
    
 
3. Wählen Sie im Dialogfeld  **Neues Element hinzufügen** die Option **Office/SharePoint** und dann **Liste** aus, nennen Sie die ListeMyDocumentLibrary, und wählen Sie dann die Schaltfläche  **Hinzufügen** aus.
    
 
4. Wählen Sie im  **Assistenten zum Anpassen von SharePoint** die Option **Anpassbare Listenvorlage und Listeninstanz erstellen:** aus.
    
 
5. Wählen Sie in der Dropdownliste unter dieser Option  **Dokumentbibliothek** aus und klicken Sie anschließend auf **Weiter**.
    
 
6. Wählen Sie unter  **Wählen Sie eine Vorlage für diese Dokumentbibliothek aus. Dokumente, die von Benutzern in dieser Bibliothek erstellt werden, basieren auf dieser Vorlageseite.** die Option **Das folgende Dokument als Vorlage für diese Bibliothek verwenden** und dann die Schaltfläche **Durchsuchen** aus.
    
 
7. Öffnen Sie im Dialogfeld  **Öffnen** den Ordner **OfficeDocuments**, und wählen Sie die Datei  **MyTaskPaneApp.xlsx** aus. Wählen Sie anschließend die Schaltfläche **Öffnen** und dann die Schaltfläche **Fertig stellen** aus, und schließen Sie den Listen-Designer.
    
 
8. Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledAddin** aus.
    
 
9. Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.
    
 
10. Wählen Sie im  **Projektmappen-Explorer** die Datei **AppManifest.xml** aus.
    
 
11. Wählen Sie  **Ansicht** und **Designer** aus.
    
 
12. Legen Sie im Manifest-Designer den Wert für **Startseite** auf „~appWebUrl/Lists/MyDocumentLibrary“ fest. Dieser wird in den Wert „OfficeEnabledAddin/Lists/MyDocumentLibrary“ konvertiert.
    
     **Hinweis** Diese URL verweist auf die Dokumentbibliothek. Sie müssen das ~appWebUrl-Token am Anfang von allen URLs in Ihrem Office-Add-In-Manifest verwenden, die auf Elemente innerhalb der Add-In-Website verweist. Weitere Informationen zu URL-Token in einem SharePoint-Add-In Projekt finden Sie unter [URL-Zeichenfolgen und Token in SharePoint-Add-Ins](url-strings-and-tokens-in-sharepoint-add-ins).
13. Schließen Sie den Manifest-Designer, um die Änderung zu speichern.
    
 

## <a name="consume-sharepoint-data-in-the-task-pane"></a>Verwenden von SharePoint-Daten im Aufgabenbereich
<a name="Consume"> </a>

In diesem Verfahren zeigen Sie mithilfe der von SharePoint bereitgestellten REST-Schnittstelle eine Liste von Websitebenutzern an.
 

 
In diesem Beispiel werden die SharePoint-Listendaten nur angezeigt, aber Sie können diese Art von Daten als Teil eines Dokumentgenehmigungs-Add-ins verwenden. Wenn ein Benutzer einen Namen aus der Liste auswählt, legt Ihr Code den Wert der „Prüfer“-Spalte in einer Dokumentnachverfolgungsliste fest. Ein mit dieser Liste verknüpfter Workflow kann eine Prüfbenachrichtigung an den Benutzer senden. Alternativ können Sie den ausgewählten Namen in den Dokumenteinstellungen speichern. Wenn dann ein Benutzer das Dokument öffnet, können Sie die Steuerelemente ausschließlich im Aufgabenbereich-Add-in anzeigen, wenn der aktuelle Benutzer mit dem in den Dokumenteinstellungen gespeicherten Benutzer übereinstimmt. Weitere Informationen finden Sie unter den folgenden Themen:
 

 

-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [Beibehalten des Zustands und der Einstellungen von Add-Ins](http://msdn.microsoft.com/library/407df6e8-c237-4d6a-b357-3000fe3de9ff%28Office.15%29.aspx)
    
 

1. Erweitern Sie im  **Projektmappen-Explorer** den Ordner **MyTaskPaneAddin**, erweitern Sie den Ordner  **Home** und wählen Sie dann die Datei „**Home.html** aus.
    
    Die Datei "Home.html" wird im Code-Editor geöffnet.
    
 
2. Fügen Sie den folgenden HTML-Code unter der Schaltfläche  `get-data-from-selection` hinzu.
    
```HTML
  <p>Select Reviewer:</p> <select class="select" id="select-reviewer" name="D1"> </select>
```

3. Wählen Sie die Datei  **Home.js**, um Sie im Code-Editor zu öffnen.
    
 
4. Fügen Sie der Datei Home.js oben die folgenden Deklarationen hinzu.
    
```
  var appWebURL; var web;
```

5. Ersetzen Sie die  `Initialize`-Funktion durch den folgenden Code.
    
    Dieser Code führt die folgenden Aufgaben aus:
    
      - Die Dateien "SP.Runtime.js" und "SP.js" werden mithilfe der  `getScript`-Funktion in jQuery geladen. Nachdem die Dateien geladen wurden, hat das Programm Zugriff auf das JavaScript-Objektmodell für SharePoint.
    
 
  - Lädt das aktuelle Websiteobjekt.
    
 
  - Ruft eine Funktion auf, die alle Benutzer der Website abruft. Sie fügen den Code für diese Funktion im nächsten Schritt hinzu.
    
 



```JS
   // The initialize function must be run each time a new page is loaded 
   Office.initialize = function (reason) { $(document).ready(function () { app.initialize(); var scriptbase = "/_layouts/15/"; $.getScript(scriptbase + "SP.Runtime.js", function () { $.getScript(scriptbase + "SP.js", function () { getAppWeb(function () { getSPUsers(populateUsersDropDown); }); }); }); function getAppWeb(functionToExecuteOnReady) { var context = SP.ClientContext.get_current(); web = context.get_web(); context.load(web); context.executeQueryAsync(onSuccess, onFailure); function onSuccess() { appWebURL = web.get_url(); functionToExecuteOnReady(); } function onFailure(sender, args) { app.initialize(); app.showNotification("Failed to connect to SharePoint. Error: " + args.get_message()); } } $('#get-data-from-selection').click(getDataFromSelection); }); };
```

6. Fügen Sie der Datei Home.js unten den folgenden Code hinzu.
    
    This code obtains a list of website users by using the REST interface provided by SharePoint. Then, this code populates a drop-down list with the name and ID of each user.
    


```JS
  function getSPUsers(functionToExecuteOnReady) { var url = appWebURL + "/../_api/web/siteUsers"; jQuery.ajax({ url: url, type: "GET", headers: { "ACCEPT": "application/json;odata=verbose" }, success: onSuccess, error: onFailure }); function onSuccess(data) { var results = data.d.results; functionToExecuteOnReady(results); } function onFailure(jaXHR, textStatus, errorThrown) { var error = textStatus + " " + errorThrown; app.showNotification(error); } } function populateUsersDropDown(results) { for (var i = 0; i < results.length; i++) { var IDTemp = results[i].Id; $('#select-reviewer').append("<option value='" + IDTemp + "'>" + results[i].Title + "</option>"); } }
```

7. Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü der Datei **AppManifest.xml**, und wählen Sie **Designer anzeigen** aus.
    
 
8. Wählen Sie im Designer die Seite  **Berechtigungen**.
    
 
9. Wählen Sie der Dropdownliste der Spalte  **Bereich** das Element **Web** aus.
    
 
10. Wählen Sie in der Dropdownliste der Spalte  **Berechtigung** das Element **Web** aus.
    
 

## <a name="debug-the-task-pane-add-in"></a>Debuggen des Aufgabenbereich-Add-Ins
<a name="debug"> </a>

Sie können Ihr Aufgabenbereich-Add-in debuggen, indem Sie das Dokument starten oder das SharePoint-Add-In starten und dann ein Dokument aus der Dokumentbibliothek öffnen.
 

 

### <a name="debugging-your-task-pane-add-in-by-starting-the-document"></a>Debuggen des Aufgabenbereich-Add-ins durch Starten eines Dokuments


 

 

 **Hinweis**  Da dieser Vorgang Excel öffnet, funktioniert er nur, wenn Office auf dem System installiert ist. Andernfalls erhalten Sie den Fehler, dass die mit diesem Projekttyp verknüpfte Anwendung nicht auf diesem Rechner installiert ist.
 


1. Öffnen Sie die Datei "Home.js" im Code-Editor und setzen Sie neben der  `getDataFromSelection`-Methode einen Haltepunkt.
    
 
2. Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledApp** aus.
    
 
3. Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.
    
 
4. Wählen Sie im Fenster "Eigenschaften" aus der Dropdownliste  **Startaktion** das Element **Office Desktop Client**. Daraufhin wird eine neue Eigenschaft,  **Startdokument** angezeigt.
    
 
5. Wählen Sie in der Dropdownliste  **Startdokument** das Element **OfficeDocuments\TaskPaneApp.xlsx** aus.
    
 
6. Wählen Sie im Menü  **Debuggen** die Option **Debuggen starten**.
    
    Diese Einstellung zeigt die Arbeitsmappe im Aufgabenbereich-Add-in an, wenn das Add-in ausgeführt wird. Die Arbeitsmappe wird geöffnet und das Add-in für den Aufgabenbereich angezeigt.
    
 
7. Wählen Sie im Aufgabenbereich-Add-in die Dropdownliste  **Prüfer auswählen** aus, um eine Liste der SharePoint-Benutzer anzuzeigen.
    
 
8. Wählen Sie in der Excel-Arbeitsmappe eine beliebige Zelle aus.
    
 
9. Wählen Sie im Add-in für den Aufgabenbereich die Schaltfläche  **Daten von Auswahl abrufen** aus.
    
    Die Ausführung wird an dem Haltepunkt unterbrochen, den Sie neben der `getDataFromSelection`-Methode gesetzt haben.
    
 

### <a name="debugging-your-task-pane-add-in-by-starting-sharepoint"></a>Debuggen des Aufgabenbereich-Add-Ins durch Starten von SharePoint


 

 

 **Hinweis** Dieser Vorgang öffnet Excel Online. Dies funktioniert nur mit einem Office 365-Konto. Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/en-us/library/office/apps/fp161179%28v=office.15%29).
 


1. Öffnen Sie die Datei „Home.js“ im Code-Editor, und setzen Sie neben der `getDataFromSelection`-Methode einen Haltepunkt.
    
 
2. Wählen Sie im  **Projektmappen-Explorer** den Projektknoten **OfficeEnabledApp** aus.
    
 
3. Wählen Sie im Menü  **Ansicht** die Option **Eigenschaftenfenster** aus.
    
 
4. Wählen Sie im Fenster "Eigenschaften" aus der Dropdownliste  **Startaktion** das Element **Internet Explorer** aus.
    
 
5. Wählen Sie im Menü  **Debuggen** die Option **Debuggen starten** aus.
    
    Visual Studio öffnet SharePoint und zeigt die Bibliothek **MyDocumentLibrary** an.
    
 
6. Wählen Sie in SharePoint auf der Registerkarte  **Dateien** die Option **Neues Dokument** aus. 
    
 
7. Gehen Sie in der Arbeitsmappe zu Ihrem Projekt, MyTaskPaneApp.xlsx.
    
    Die Arbeitsmappe wird geöffnet, und das Add-in für den Aufgabenbereich wird angezeigt.
    
 
8. Stellen Sie sicher, dass im Browser das Skriptdebugging aktiviert ist. Im Internet Explorer können Sie das Skriptdebugging aktivieren, indem Sie das Dialogfeld  **Internetoptionen** öffnen und auf der Registerkarte **Erweitert** und die Kontrollkästchen **Skriptdebugging deaktivieren (Internet Explorer)** und **Skriptdebugging deaktivieren (Andere)** deaktivieren.
    
 
9. Wählen Sie in Visual Studio im Menü  **Debuggen** die Option **An den Prozess anhängen** aus.
    
 
10. Wählen Sie im Dialogfeld **An den Prozess anhängen** alle verfügbaren **iexplore.exe**-Prozesse und dann die Schaltfläche zum Anhängen**** aus.
    
 
11. Wählen Sie im Aufgabenbereich-Add-in die Dropdownliste  **Prüfer auswählen** aus, um eine Liste der SharePoint-Benutzer anzuzeigen.
    
    Die Daten der Liste werden aus SharePoint mithilfe eines REST-Aufrufs abgerufen.
    
 
12. Wählen Sie in der Excel-Arbeitsmappe eine beliebige Zelle aus.
    
 
13. Wählen Sie im Add-in für den Aufgabenbereich die Schaltfläche  **Daten von Auswahl abrufen** aus.
    
    Die Ausführung wird an dem Haltepunkt unterbrochen, den Sie neben der `getDataFromSelection`-Methode gesetzt haben.
    
     **Hinweis** Falls die Arbeitsmappe keine Daten enthält, fügen Sie welche hinzu, indem Sie **Arbeitsmappe bearbeiten**, **In Excel Online bearbeiten** in der Symbolleiste wählen.

## <a name="package-and-publish-the-add-in"></a>Packen und Veröffentlichen des Add-Ins
<a name="Package"> </a>

Wenn Sie zum Packen des Add-Ins für die Veröffentlichung bereit sind, öffnen Sie den Assistenten **Veröffentlichen von Office- und SharePoint-Add-Ins**.
 

 

- Öffnen Sie im  **Projektmappen-Explorer** das Kontextmenü für das SharePoint-Add-In-Projekt, und wählen Sie dann **Veröffentlichen** aus.
    
    Der Assistent **Add-Ins für Office und SharePoint veröffentlichen** wird angezeigt. Weitere Informationen finden Sie unter [Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio).
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AdditionalResources"> </a>


-  [Aufgabenbereich- und Inhalts-Add-Ins für Office 2013](http://msdn.microsoft.com/library/baf73b23-4429-4b7f-bcb9-a99a9618ae38%28Office.15%29.aspx)
    
 
-  [Entwurfsrichtlinien für Office-Add-Ins](http://msdn.microsoft.com/library/d5b2ab2e-dfc8-47c8-919c-e9c23358d70c%28Office.15%29.aspx)
    
 
-  [Entwicklungslebenszyklus von Office-Add-Ins](http://msdn.microsoft.com/library/c35b4b2b-7869-4501-9f10-888c8e74c98c%28Office.15%29.aspx)
    
 
-  [Veröffentlichen Ihres Office-Add-Ins](http://msdn.microsoft.com/library/7f3ae6a0-06e9-438c-8899-bd9f605e6d9e%28Office.15%29.aspx)
    
 
-  [Grundlegendes zur JavaScript-API für Office](http://msdn.microsoft.com/library/01180dae-ca45-40c8-b3dd-fd2a85651c0c%28Office.15%29.aspx)
    
 
-  [XML-Manifest für Office-Add-Ins](http://msdn.microsoft.com/library/4139ff24-afac-472a-af7d-9d069587ac9b%28Office.15%29.aspx)
    
 
-  [API und Schemaverweise für Office-Add-Ins](http://msdn.microsoft.com/library/afcc2908-1e1b-4297-b554-11e6eb404804%28Office.15%29.aspx)
    
 

