


# <a name="add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in"></a>Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In
Erfahren Sie, wie Sie eine benutzerdefinierte Seite und CSS-Datei in ein SharePoint-Add-In einschließen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Dies ist der siebte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:
 

-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
    
 

 **Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforePage.sln“ öffnen.
 

In diesem Artikel fügen Sie dem SharePoint-Add-In „Orientierung für Mitarbeiter“ eine Hilfeseite hinzu und konfigurieren sie für die Verwendung eines benutzerdefinierten CSS-Stylesheets. 
 

## <a name="add-a-page"></a>Hinzufügen einer Seite


1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Seiten**, und wählen Sie **Hinzufügen** > **Neues Element**. Das Dialogfeld **Neues Element hinzufügen** wird mit dem Knoten **Office/SharePoint** geöffnet.
    
 
2. Wählen Sie **Seite**, und weisen Sie den Namen „Help.aspx“ zu. 
    
 
3. Suchen Sie die beiden **asp:Content**-Elemente in der Datei, und fügen Sie das folgende **asp:Content** Markup zwischen ihnen hinzu.
    
```HTML
  <asp:Content ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server">
    Help
</asp:Content> 
```

4. Suchen Sie das **asp:Content**-Element mit der ID **PlaceholderAdditionalPageHead**, und fügen Sie ihm das folgende Markup hinzu.
    
```HTML
  <link rel="Stylesheet" type="text/css" href="../Content/App.css" />
```

5. Suchen Sie das **asp:Content**-Element mit der ID **PlaceHolderMain**, und entfernen Sie alle untergeordneten Elemente.
    
 
6. Fügen Sie demselben **asp:Content**-Elements Folgendes als Inhalt hinzu.
    
```HTML
  <H3>Having a problem with the add-in?</H3>
<p> Call the help line for Fabrikam Add-ins:</p>
<p>1-555-555-5555</p>
```

7. Speichern und schließen Sie die Datei.
    
 
8. Öffnen Sie die Datei „Default.aspx“.
    
 
9. Suchen Sie das **asp:Content**-Element mit der ID **PlaceHolderMain**, und fügen Sie das folgende Markup am Ende hinzu. 
    
```HTML
  <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Pages/Help.aspx';" 
    Text="Get help for the Employee Orientation add-in" /></p>

```

10. Speichern und schließen Sie die Datei.
    
 

## <a name="add-a-style-class-to-the-stylesheet"></a>Hinzufügen einer Formatklasse zum Stylesheet


 

 

1. Öffnen Sie im **Projektmappen-Explorer** die Datei „app.css“ im Ordner **Inhalt**, und fügen Sie der Datei dann die folgende Zeile hinzu.
    
```
  p {color: green;}
```

2. Speichern und schließen Sie die Datei.
    
 

## <a name="run-and-test-the-add-in"></a>Ausführen und Testen des Add-Ins


 

 

1. Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. 
    
 
2. Wenn die Standardseite des Add-Ins geöffnet wird, klicken Sie auf den Link **Hilfe für das Add-In „Orientierung für Mitarbeiter“**, um die Seite **Hilfe** zu öffnen.
    
    Ihre benutzerdefinierte Seite wird geöffnet, und die beiden Zeilen, die Sie in <p> -Tags eingeschlossen haben, werden grün angezeigt.
    

    **Hilfeseite**

 

  ![Eine SharePoint-Seite mit dem Titel „Hilfe“. Sie enthält eine Kopfzeile in Schwarz, gefolgt von zwei Textzeilen in Grün.](../../images/2df51ab0-5b24-4a37-8b6a-6e95dbb1aeaa.PNG)
 

    
    
 
3. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.
    
 
4. Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.
    
 

## 
<a name="Nextsteps"> </a>

Im nächsten Artikel in dieser Reihe fügen Sie ein benutzerdefiniertes clientseitiges Rendering zu einer Listenspalte in einem SharePoint-Add-In hinzu:  [Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint-gehostetes SharePoint Add-In](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in).
 

 

