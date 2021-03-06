# <a name="create-custom-actions-to-deploy-with-sharepoint-add-ins"></a>Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins
In diesem Artikel erfahren Sie, wie Sie eine benutzerdefinierte Aktion in SharePoint erstellen, die für das Hostweb bereitgestellt wird, wenn Sie ein SharePoint-Add-In bereitstellen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Wenn Sie ein SharePoint-Add-In erstellen, ermöglichen Ihnen benutzerdefinierte Aktionen die Interaktion mit den Listen und dem Menüband im Hostweb. Eine benutzerdefinierte Aktion wird für das Hostweb bereitgestellt, wenn Endbenutzer Ihr Add-In installieren. Mithilfe benutzerdefinierter Aktionen ist es möglich, eine Remotewebseite zu öffnen und über die Abfragezeichenfolge Informationen zu übergeben. Es sind zwei Typen von benutzerdefinierten Aktionen für Add-Ins verfügbar: benutzerdefinierte Aktionen für das Menüband und für Menüelemente.
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Voraussetzungen für die Verwendung der Beispiele in diesem Artikel
<a name="SP15Createcustomactionsapps_Prereq"> </a>

Sie benötigen eine Entwicklungsumgebung, wie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins) erläutert.
 

 

### <a name="core-concepts-to-help-you-understand-custom-actions"></a>Kernkonzepte für ein besseres Verständnis von benutzerdefinierten Aktionen

In der folgenden Tabelle sind hilfreiche Artikel aufgeführt, die ein besseres Verständnis der Konzepte und Schritte bei einem Szenarium mit benutzerdefinierten Aktionen ermöglichen.
 

 

**Tabelle 1. Kernkonzepte für benutzerdefinierte Aktionen**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [SharePoint-Add-Ins](sharepoint-add-ins)|Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.|
| [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)|Hier erfahren Sie mehr über die UX-Optionen (User eXperience, Benutzerumgebung) beim Erstellen von SharePoint-Add-Ins.|
| [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|Hier erhalten Sie Informationen über den Unterschied zwischen einem Hostweb und einem Add-In-Web. Außerdem erfahren Sie, welche SharePoint-Komponenten in ein SharePoint-Add-In eingeschlossen werden können, welche Komponenten für das Hostweb bereitgestellt werden, welche Komponenten für das Add-In-Web bereitgestellt werden, und wie das Add-In-Web in einer isolierten Domäne bereitgestellt wird.|

## <a name="code-example-create-a-custom-action-in-the-host-web-document-libraries"></a>Codebeispiel: Erstellen einer benutzerdefinierten Aktion in den Hostweb-Dokumentbibliotheken
<a name="SP15Createcustomactionsapps_Codeexample"> </a>

Führen Sie diese Schritte aus, um eine benutzerdefinierte Aktion in den Hostweb-Dokumentbibliotheken zu erstellen:
 

 

1. Erstellen Sie die SharePoint-Add-In- und Remotewebprojekte.
    
 
2. Fügen Sie dem SharePoint-Add-In-Projekt ein benutzerdefiniertes Feature hinzu.
    
 
3. Fügen Sie dem Webprojekt eine Add-In-Webseite hinzu.
    
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a>So erstellen Sie die Projekte für das SharePoint-Add-In und das Remoteweb


1. Öffnen Sie Visual Studio als Administrator. (Klicken Sie dazu im Menü **Start** mit der rechten Maustaste auf das Visual Studio-Symbol, und wählen Sie **Als Administrator ausführen** aus.)
    
 
2. Erstellen Sie das vom Anbieter gehostete SharePoint-Add-In wie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins) erläutert, und nennen Sie es „itCustomActionsApp“. 
    
 

### <a name="to-add-an-add-in-webpage-for-the-custom-actions"></a>So fügen Sie eine Add-In-Webseite für die benutzerdefinierten Aktionen hinzu


1. Klicken Sie nach dem Erstellen der Visual Studio-Lösung mit der rechten Maustaste auf das Webanwendungsprojekt (nicht das SharePoint-Add-In-Projekt), und fügen Sie ein neues Webformular hinzu, indem Sie **Hinzufügen** > **Neues Element** > **Web** > **Webformular** auswählen. Geben Sie dem Formular den Namen „CustomActionTarget.aspx“.
    
 
2. Ersetzen Sie in der Datei CustomActionTarget.aspx das gesamte **html**-Element und seine untergeordneten Elemente durch den folgenden HTML-Code. Behalten Sie das gesamte Markup oberhalb des **html**-Elements wie vorhanden bei. Der HTML-Code enthält JavaScript, das die folgenden Aufgaben durchführt:
    
      - Bereitstellung eines Platzhalters für die Parameter der Abfragezeichenfolge.
    
 
  - Extrahieren der Parameter aus der Abfragezeichenfolge.
    
 
  - Rendern der Parameter im Platzhalter.
    
 

     **Wichtig** Die Token „ItemURL“ und „ItemID“ werden nur übergeben, wenn ein Element ausgewählt ist. In einem SharePoint-Add-In mit Produktionsqualität muss Ihr Code Situationen, in denen kein Element ausgewählt ist, verarbeiten können. In diesem Beispiel warnt der Code den Benutzer, dass kein Element ausgewählt wurde. 

```HTML
  <html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Custom action target</title>
</head>
<body>
    <h2>Query string parameters passed by the custom action:</h2>

    <!-- Placeholder for query string parameters -->
    <ul id="qsparams"/>

    <!-- Main JavaScript function, renders
         the query string parameters -->
    <script lang="javascript">
        var params = document.URL.split("?")[1].split("&amp;");
        var paramsHTML = "";
      
        // Extracts the parameters from the query string.
        // Parameters are URLencoded, decode for rendering
        // in page.
        for (var i = 0; i < params.length; i = i + 1) {
            params[i] = decodeURIComponent(params[i]);
            paramsHTML += "<li>" + params[i] + "</li>";
        }

         // Alert the user when no item has been selected.
         // (The SPListItemId is the 5th parameter.)
         if (params[5] === undefined) {
            paramsHTML += "<div> <h3> No item has been selected from the list.  Please select an item. </h3> </div> ";
         }

        // Render parameters in the placeholder.
        document.getElementById("qsparams").innerHTML =
            paramsHTML;
    </script>
</body>
</html>
```


### <a name="to-add-a-menu-item-custom-action-to-the-sharepoint-add-in-project"></a>So fügen Sie dem SharePoint-Add-In-Projekt eine benutzerdefinierte Menüelementaktion hinzu


1. Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menüelementaktion** aus. 
    
 
2. Übernehmen Sie den Standardnamen, und wählen Sie **Hinzufügen** aus.
    
 
3. Der Assistent **Benutzerdefinierte Aktion für ein Menüelement erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:
    
    **Tabelle 2. Eigenschaften der benutzerdefinierten Menüelementaktion**


|**Frage zur Eigenschaft**|**Antwort**|
|:-----|:-----|
|Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?|Wählen Sie **Hostweb**.|
|Wo gilt die benutzerdefinierte Aktion?|Wählen Sie **Listenvorlage**.|
|Für welches spezielle Element gilt die benutzerdefinierte Aktion?|Wählen Sie **Dokumentbibliothek**.|
|Wie lautet der Text im Menüelement?|Geben Sie **Meine benutzerdefinierte Aktion** ein.|
|Wohin navigiert die benutzerdefinierte Aktion?|Wählen Sie die Seite **CustomActionAppWeb\CustomActionTarget.aspx** aus.|
4. Wählen Sie **Fertig stellen**.
    
    Visual Studio generiert das folgende Markup in der Datei „elements.xml“ des Features für die benutzerdefinierte Menüelementaktion:
    


```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements 
    xmlns="http://schemas.microsoft.com/sharepoint/">
    <!-- RegistrationId attribute is the list type id,
        in this case, a document library (id=101). -->
  <CustomAction 
      Id="65695319-4784-478e-8dcd-4e541cb1d682.CustomAction"
      RegistrationType="List"
      RegistrationId="101"
      Location="EditControlBlock"
      Sequence="10001"
      Title="Invoke custom action">
    <!-- 
    Update the Url below to the page you want the custom action to use.
    Start the URL with the token ~remoteAppUrl if the page is in the
    associated web project, use ~appWebUrl if page is in the add-in project.
    -->
    <UrlAction Url=
"~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}" />
  </CustomAction>
</Elements>

```

5. Fügen Sie die folgenden Abfrageparameter zum Ende des Attributs **Url** des Elements **UrlAction** hinzu:
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}`
    
    Das Element **UrlAction** sollte wie folgt aussehen:
    
     ` <UrlAction Url= "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}" />`
    
 

 **Hinweis** In diesem Beispiel wird die Remotewebseite in einem vollständigen Fenster geöffnet, wenn der Benutzer die benutzerdefinierte Aktion aus dem Menü auswählt. Benutzerdefinierte Menüaktionen können eine Remotewebseite auch in einem Dialogfeld öffnen, indem Sie das Attribut **HostWebDialog** verwenden. Weitere Informationen finden Sie unter [SharePoint-Add-In-Lokalisierung](https://github.com/OfficeDev/SharePoint-Add-in-Localization).
 


### <a name="to-add-a-ribbon-custom-action-to-the-sharepoint-add-in-project"></a>So fügen Sie dem SharePoint-Add-In-Projekt eine benutzerdefinierte Menübandaktion hinzu


1. Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** > **Office/SharePoint** > **Benutzerdefinierte Menübandaktion** aus. 
    
 
2. Übernehmen Sie den Standardnamen, und wählen Sie **Hinzufügen** aus.
    
 
3. Der Assistent **Benutzerdefinierte Aktion für das Menüband erstellen** stellt Ihnen eine Reihe von Fragen. Geben Sie die Antworten aus der folgenden Tabelle ein:
    
    **Tabelle 3. Eigenschaften der benutzerdefinierten Menübandaktion**


|**Frage zur Eigenschaft**|**Antwort**|
|:-----|:-----|
|Wo möchten Sie die benutzerdefinierte Aktion verfügbar machen?|Wählen Sie **Hostweb**.|
|Wo gilt die benutzerdefinierte Aktion?|Wählen Sie **Listenvorlage**.|
|Für welches spezielle Element gilt die benutzerdefinierte Aktion?|Wählen Sie **Dokumentbibliothek**.|
|Wo befindet sich das Steuerelement?|Wählen Sie **Ribbon.Documents.Manage**.|
|Wie lautet der Text im Menüelement?|Geben Sie **Meine benutzerdefinierte Menübandschaltfläche** ein.|
|Wohin navigiert die benutzerdefinierte Aktion?|Wählen Sie die Seite **CustomActionAppWeb\CustomActionTarget.aspx** aus.|
4. Visual Studio generiert das folgende Markup in der Datei „elements.xml“ des Features für die benutzerdefinierte Menübandaktion:
    
```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="85691508-c076-4f43-93d4-96b4d5253a09.RibbonCustomAction1"
                RegistrationType="List"
                RegistrationId="101"
                Location="CommandUI.Ribbon"
                Sequence="10001"
                Title="Invoke &amp;apos;RibbonCustomAction1&amp;apos; action">
    <CommandUIExtension>
      <!-- 
      Update the UI definitions below with the controls and the command actions
      that you want to enable for the custom action.
      -->
      <CommandUIDefinitions>
        <CommandUIDefinition Location="Ribbon.Documents.Manage.Controls._children">
          <Button Id="Ribbon.Documents.Manage.RibbonCustomAction1Button"
                  Alt="My Custom Ribbon Button"
                  Sequence="100"
                  Command="Invoke_RibbonCustomAction1ButtonRequest"
                  LabelText="My Custom Ribbon Button"
                  TemplateAlias="o1"
                  Image32by32="_layouts/15/images/placeholder32x32.png"
                  Image16by16="_layouts/15/images/placeholder16x16.png" />
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest"
                          CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}"/>
      </CommandUIHandlers>
    </CommandUIExtension >
  </CustomAction>
</Elements> 

```

5. Fügen Sie die folgenden Abfrageparameter zum Ende des Attributs **CommandAction** des Elements **CommandUIHandler** hinzu:
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}`
    
    Das Element **CommandUIHandler** sollte wie folgt aussehen:
    
     ` <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest" CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}" />`
    
     **Hinweis** Benutzerdefinierte Menübandaktionen verwenden **SelectedListId** und **SelectedItemId**. **ListId** und **ItemId** werden nur mit benutzerdefinierten Menüelementaktionen verwendet.

### <a name="set-the-add-in-start-page-to-the-host-web-home-page"></a>Festlegen der Add-In-Startseite auf die Hostweb-Startseite


1. Das fortlaufende Beispiel-SharePoint-Add-In verfügt nicht über ein Add-In-Web, und die Remotewebanwendung ist nur für das Hosten des Formulars vorhanden. Deshalb sollte die Startseite des Add-Ins auf die Startseite des Hostwebs festgelegt werden. 
    
    Wählen Sie zunächst das SharePoint-Add-In-Projekt (nicht das Webanwendungsprojekt) im **Projektmappen-Explorer** aus, und kopieren Sie den Wert der Eigenschaft **Website-URL**, einschließlich des Protokolls (z. B. **https://contoso.sharepoint.com**), in die Zwischenablage. 
    
 
2. Öffnen Sie das Add-In-Manifest, und fügen Sie die URL in das Feld **Startseite** ein.
    
 
3. Optional können Sie die Seite „Default.aspx“ aus dem Webanwendungsprojekt löschen, da sie nicht im SharePoint-Add-In verwendet wird.
    
 

### <a name="to-build-and-run-the-solution"></a>So erstellen Sie die Lösung und führen sie aus


1. Drücken Sie F5.
    
     **Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.
2. Klicken Sie auf die Schaltfläche **Vertrauen**. Die Standardseite Ihrer Entwicklerwebsite wird geöffnet.
    
 
3. Navigieren Sie zu einer beliebigen Dokumentbibliothek im Hostweb.
    
    **Starten einer benutzerdefinierten Menüaktion**

 

  ![Dokumentbibliothek mit geöffneter Legende für ein Dokument, das durch die Popupschaltfläche in der Legende geöffnete Menü und das geöffnete Menü "Erweitert".](../../images/477cecf5-03ff-46ff-9c25-a5f9a86d43f4.png)
 

 

 
4. Klicken Sie auf die Popupschaltfläche ( **...**) für ein beliebiges Dokument. Das Popup wird geöffnet.
    
 
5. 5.Klicken Sie auf die Popupschaltfläche ( **...**) im Popup. 
    
 
6. Wählen Sie **Erweitert** aus.
    
 
7. Wählen Sie im Kontextmenü die Option **Meine benutzerdefinierte Menüaktion** aus. Auf der sich öffnenden Remotewebseite sollte etwas wie Folgendes angezeigt werden:
    
    **Remotewebseite mit Parametern der benutzerdefinierten Aktion**

 

  ![Webseite mit Parametern aus einer benutzerdefinierten Aktion](../../images/CustomActions_target.png)
 

 

 
8. Klicken Sie auf die Schaltfläche **Zurück** in Ihrem Browser, um zur Bibliothek zurückzukehren.
    
    **Starten einer benutzerdefinierten Menübandaktion**

 

  ![Eine Dokumentbibliothek mit einem ausgewählten Dokument, der geöffneten Registerkarte „Datei“ im Menüband und der benutzerdefinierten Schaltfläche im Menüband.](../../images/b315cb68-ff6a-4770-a1dc-738696ab71d2.png)
 

 

 
9. Wählen Sie ein beliebiges Dokument aus.
    
 
10. Öffnen Sie die Registerkarte **Datei** im Menüband.
    
 
11. Wählen Sie **Meine benutzerdefinierte Menübandschaltfläche** aus. Dieselbe Remotewebseite wird angezeigt.
    
 

**Tabelle 4: Problembehandlung für die Lösung**


|**Problem**|**Lösung**|
|:-----|:-----|
|Der Browser wird nicht geöffnet, nachdem Sie F5 gedrückt haben.|Legen Sie das SharePoint-Add-In-Projekt als Startprojekt fest.|
|Die Token in der URL werden nicht aufgelöst, nachdem Sie in Visual Studio F5 gedrückt haben.|Wechseln Sie zur Seite **Websiteinhalt** im Hostweb, und klicken Sie auf das Symbol für Ihr Add-In.|

## <a name="next-steps"></a>Nächste Schritte
<a name="SP15Createcustomactionsapps_Nextsteps"> </a>

In diesem Artikel wurde die Vorgehensweise zum Erstellen einer benutzerdefinierten Aktion in einem SharePoint-Add-In beschrieben. Als nächsten Schritt können Sie sich über andere UX-Komponenten informieren, die für SharePoint-Add-Ins verfügbar sind. Weitere Informationen hierzu finden Sie unter:
 

 

-  [Codebeispiel: Öffnen einer Remote-Add-In-Webseite mit einer benutzerdefinierten ECB-Aktion](http://code.msdn.microsoft.com/SharePoint-2013-Open-e0ca1826)
    
 
-  [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization)
    
 
-  [Codebeispiel: Verwenden von benutzerdefinierten Aktionen und der domänenübergreifenden Bibliothek zum Bestellen von Büchern](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Createcustomactionsapps_AddResources"> </a>


-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)
    
 
-  [Designrichtlinien für die Benutzerfreundlichkeit von SharePoint-Add-Ins](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

