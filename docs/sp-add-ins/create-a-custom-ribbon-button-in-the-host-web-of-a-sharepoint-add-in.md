# <a name="create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in"></a>Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins
Erfahren Sie, wie Sie benutzerdefinierte Menübandschaltflächenbefehle zum Hostweb eines SharePoint-Add-Ins hinzufügen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Dies ist der neunte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:
 

-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint gehostetes SharePoint-Add-In](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in)
    
 

 **Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeRibbon.sln“ öffnen.
 

Alle SharePoint-Add-Ins können von der Seite **Websiteinhalte** des Hostwebs ausgeführt werden, indem Sie auf die Kachel des Add-Ins klicken. Die Funktionalität eines SharePoint-Add-Ins kann auch über benutzerdefinierte Aktionen im Hostweb zur Verfügung gestellt werden, die benutzerdefinierte Menübandschaltflächen oder benutzerdefinierte Menüelemente sind. In diesem Artikel fügen Sie eine Schaltfläche zum Menüband eines Hostwebs hinzu.
 

## <a name="prepare-the-host-web"></a>Vorbereiten des Hostwebs

Die Schaltfläche wird dem Menüband eines Kalenders im Hostweb hinzugefügt. Führen Sie die folgenden Schritte in der Benutzeroberfläche Ihrer SharePoint-Entwicklerwebsite aus.
 

 

1. Wählen Sie auf der Startseite der Website **Websiteinhalte** > **Add-In hinzufügen** > **Kalender** aus.
    
 
2. Geben Sie im Dialogfeld **Kalender hinzufügen** „Planung für Orientierung für Mitarbeiter“ in das Feld **Name** ein, und wählen Sie dann **Erstellen** aus.
    
 
3. Wenn der Kalender geöffnet wird, setzen Sie den Cursor auf ein beliebiges Datum, bis der Link **Hinzufügen** auf dem Datum angezeigt wird, und klicken Sie dann auf **Hinzufügen**. 
    
 
4. Geben Sie im Dialogfeld **Planung für Orientierung für Mitarbeiter - neues Element** den Text „Orientierung Cassi Hicks“ in das Feld **Titel** ein. Behalten Sie für die anderen Felder die Standardwerte bei, und klicken Sie auf **Speichern**.
    
    Der Kalender sollte ähnlich wie im folgenden Beispiel aussehen:
    

    **Benutzerdefinierter Kalender**

 

  ![Ein Kalender namens „Planung für Orientierung für Mitarbeiter“ mit dem Element „Orientierung Cassie Hicks“ am 1. Juni: ](../../images/d2066862-41c1-424d-9bfb-b6c5342bcf2c.PNG)
 

 

 

 

 

 **Wichtig** Im nächsten Verfahren muss der Kalender in der Benutzeroberfläche von Visual Studio sichtbar sein, was aber nicht der Fall sein wird, wenn Visual Studio geöffnet war, als Sie den Kalender erstellt haben. Bevor Sie fortfahren, schließen Sie Visual Studio, und melden Sie sich auch von allen Browserfenstern und PowerShell-Konsolen ab, mit denen Sie bei Ihrer Entwicklerwebsite angemeldet sind.
 


## <a name="add-a-ribbon-custom-action"></a>Hinzufügen einer benutzerdefinierten Menübandaktion


1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt **EmployeeOrientation**, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menübandaktion** aus. Nennen Sie sie „RunOrientationAdd-in“, und wählen Sie **Hinzufügen** aus.
    
 
2. Der Assistent **Benutzerdefinierte Aktion für das Menüband erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:
    

|**Frage zur Eigenschaft**|**Antwort**|
|:-----|:-----|
|Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?|Wählen Sie **Hostweb**.|
|Wo gilt die benutzerdefinierte Aktion?|Wählen Sie **Listeninstanz** ( *nicht* Listenvorlage) aus.|
|Für welches spezielle Element gilt die benutzerdefinierte Aktion?|Wählen Sie **Planung für Orientierung für Mitarbeiter** aus.|
|Wo befindet sich das Steuerelement?|Verwenden Sie nicht die Dropdownauswahl. Geben Sie stattdessen **Ribbon.Calendar.Events.Actions.Controls._children** ein. (Der dritte Teil, **Events**, identifiziert die Registerkarte des Menübands, und der vierte Teil, **Actions**, die Schaltflächengruppe.) |
|Wie lautet der Text im Menüelement?|Geben Sie **Orientierung für Mitarbeiter** ein.|
|Wohin navigiert die benutzerdefinierte Aktion?|Verwenden Sie nicht die Dropdownauswahlen. Geben Sie stattdessen **~appWebUrl/Lists/NewEmployeesInSeattle** ein. Dies ist die Seite mit der Listenansicht für die Liste, die sich im Add-In-Web befindet, damit die Menübandschaltfläche im Hostweb eine Seite im Add-In-Web öffnet.|
3. Wählen Sie **Fertig stellen**. 
    
 

## <a name="inspect-the-add-in-web-feature"></a>Überprüfen des Add-In-Web-Features

Erweitern Sie im **Projektmappen-Explorer** den Ordner **Features**, und wählen Sie das Feature **NewEmployeeOrientationComponents** aus. Der Feature-Designer wird geöffnet.
 

 
Beachten Sie, dass die benutzerdefinierte Aktion, die Sie erstellt haben, **RunOrientationAdd-in**, in **Elemente in der Lösung**, jedoch nicht in **Elemente im Feature** aufgelistet wird. Der Grund dafür ist, dass das Feature an das Add-In-Web, Ihre benutzerdefinierte Aktion aber an das Hostweb bereitgestellt wird. Wenn Sie das Add-In in Visual Studio zur Bereitstellung für die Produktion packen oder F5 in Visual Studio drücken, erstellen die Office Developer Tools für Visual Studio ein spezielles Hostwebfeature, fügen die benutzerdefinierte Aktion hinzu und stellen sie an das Hostweb bereit. Sie sollten das Hostwebfeature niemals bearbeiten. Darum wird es erst zum Zeitpunkt des Packens erstellt.
 

 

**Feature-Designer**

 

 
![Der Feature-Designer mit Spalten namens "Elemente in der Lösung" und "Elemente in der Funktion". Das Element "Orientierungs-Add-In ausführen" befindet sich in der ersten, nicht in der zweiten.](../../images/49ea0bf0-2cfa-4070-aa65-24b4a9c5e874.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a>Ausführen und Testen des Add-Ins


 

 

1. Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. 
    
 
2. Die Standardseite des SharePoint-Add-Ins wird geöffnet. Navigieren Sie zur Startseite Ihrer Entwicklerwebsite (die das Hostweb ist). In der linken oberen Ecke der Seite finden Sie einen Breadcrumblink dahin.
    
 
3. Wählen Sie auf der Startseite des Hostwebs **Websiteinhalte**, und klicken Sie auf der Seite **Websiteinhalte** auf den Kalender **Planung für Orientierung für Mitarbeiter**(nicht das Add-In **Orientierung für Mitarbeiter**).
    
 
4. Wenn der Kalender geöffnet wird, klicken Sie auf das Ereignis **Orientierung Cassie Hicks**. Wenn die Registerkarte **Ereignisse** im Menüband nicht automatisch geöffnet wird, öffnen Sie sie manuell. Sie sollte etwa wie folgt aussehen:
    
    **Menüband-Registerkarte „Ereignisse“ mit benutzerdefinierter Schaltfläche **

 

  ![Das Menüband „Ereignisse“ mit einer benutzerdefinierten Schaltfläche namens „Orientierung für Mitarbeiter“](../../images/916ecbba-11ff-45b6-a8e9-ba717ae6fe0b.png)
 

 

 
5. Klicken Sie in der Gruppe **Aktionen** im Menüband auf **Orientierung für Mitarbeiter**. Die Seite mit der Listenansicht für **Neue Mitarbeiter in Seattle** wird geöffnet.
    
 
6. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.
    
 
7. Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.
    
 

## 
<a name="Nextsteps"> </a>

Im nächsten Artikel dieser Reihe fügen Sie JavaScript zum SharePoint-Add-In hinzu und greifen auf SharePoint-Daten mit dem JavaScript-Objektmodell von SharePoint zu:  [Verwenden von SharePoint-JavaScript-APIs zum Arbeiten mit SharePoint-Daten](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data).
 

 

