# <a name="enable-a-newsfeed-for-a-cloud-business-add-in"></a>Aktivieren eines Newsfeesd für ein Cloud-Business-Add-In
Mit den Features für soziale Netzwerke und die Zusammenarbeit in SharePoint für Office 365 können Benutzer Aktivitäten in einer Liste verfolgen und Kommentare hinzufügen. Sie können mühelos einen Newsfeed für Ihr Cloud-Geschäfts-Add-In erstellen, indem Sie einige Eigenschaften aktivieren.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="prerequisites"></a>Voraussetzungen

Zum Hosten des Newsfeeds benötigen Sie in Office 365 eine SharePoint-Entwicklerwebsite, die Sie unter  [Registrieren für eine Office 365-Entwicklerwebsite](http://go.microsoft.com/fwlink/?LinkId=263490) erhalten.
 

 

## <a name="procedures"></a>Verfahren


### <a name="to-enable-a-newsfeed"></a>So aktivieren Sie einen Newsfeed


1. Öffnen Sie im Projektmappen-Explorer die Entität, die die Liste repräsentiert, der Sie einen Newsfeed hinzufügen möchten, und klicken Sie dann in der Leiste **Perspektive** auf die Registerkarte **Server**.
    
 
2. Aktivieren Sie im Fenster **Eigenschaften** die Kontrollkästchen **Nach dem Erstellen posten** und/oder **Nach dem Aktualisieren posten**.
    
  ![Eigenschaften für soziales Netzwerk](../../images/CBAsocial.PNG)
 

     Durch Aktivieren von **Nach dem Erstellen posten** wird für jedes neue Listenelement ein Thread zum Newsfeed hinzugefügt. Durch Aktivieren von **Nach dem Aktualisieren posten** wird ein Thread hinzugefügt, wenn ein Wert eines Listenelements geändert wird. Postauslöser ermitteln, welche Felder in dem Element einen Posts auslösen.
    
 
3. Klicken Sie auf den Link **Auswählen von Postauslösern**.
    
    Das Dialogfeld **Auswählen von Postauslösern** wird geöffnet.
    
 
4. Aktivieren Sie im Dialogfeld **Auswählen von Postauslösern** die Kontrollkästchen aller Felder, die einen Post auslösen sollen, und klicken Sie anschließend auf die Schaltfläche **OK**.
    
    Ein einzelner Thread wird für alle Änderungen in einem Element erstellt, unabhängig davon, wie viele Felder Sie auswählen.
    
 

### <a name="to-access-a-newsfeed"></a>So greifen Sie auf einen Newsfeed zu


1. Klicken Sie auf der Menüleiste auf **Debuggen**, **Debuggen starten**, um die Anwendung auszuführen.
    
 
2. Öffnen Sie in der laufenden Anwendung den Suchbildschirm der Entität, die die Liste repräsentiert, der Sie einen Newsfeed hinzugefügt haben. Wenn Sie die Option **Nach dem Erstellen posten** aktiviert haben, müssen Sie ein neues Element hinzufügen. Wenn Sie die Option **Nach dem Aktualisieren posten** aktiviert haben, müssen Sie die Felder bearbeiten, die Sie im Dialogfeld **Auswählen von Postauslösern** ausgewählt haben.
    
 
3. Klicken Sie auf der SharePoint-Chromleiste auf den Link **Newsfeed**.
    
  ![Die SharePoint-Chromleiste](../../images/CBAnewsfeed.PNG)
 

    Die Seite **Newsfeed** wird in einem neuen Browserfenster geöffnet und zeigt die Einträge der hinzugefügten und/oder aktualisierten Elemente an. Sie können für einen Beitrag auf den Link **Gefällt mir** klicken oder auf den Link **Antworten** klicken, um einen Kommentar hinzuzufügen.
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln von Cloud-Business-Add-Ins](develop-cloud-business-add-ins)
    
 
-  [Soziale Funktionen und Zusammenarbeit in SharePoint](http://msdn.microsoft.com/de-de/library/office/jj163280.aspx)
    
 
-  [Erstellen eines Cloud-Business-Add-Ins mit einem sozialen Newsfeed](create-a-cloud-business-add-in-with-a-social-newsfeed)
    
 

