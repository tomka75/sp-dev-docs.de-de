
# <a name="use-the-client-chrome-control-in-sharepoint-add-ins"></a>Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins
In diesem Artikel erfahren Sie, wie Sie das Chromsteuerelement in Add-Ins in SharePoint verwenden.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Dank des Chromsteuerelements in SharePoint können Sie den Kopfzeilenstil einer bestimmten SharePoint-Website in Ihrem Add-In verwenden, ohne eine Serverbibliothek registrieren zu müssen oder eine bestimmte Technologie bzw. ein bestimmtes Tool zu verwenden. Sie müssen dazu eine SharePoint-JavaScript-Bibliothek durch ein standardmäßiges <script>-Tag registrieren. Sie können einen Platzhalter bereitstellen, indem Sie ein HTML- **div**-Element verwenden und das Steuerelement mit den verfügbaren Optionen weiter anpassen. Das Steuerelement erhält sein Aussehen durch die angegebene SharePoint-Website.  
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Voraussetzungen für die Verwendung der Beispiele in diesem Artikel
<a name="SP15Usechromecontrol_Prereq"> </a>

Um die Schritte in diesem Beispiel auszuführen, benötigen Sie Folgendes:
 

 

- Visual Studio 2015
    
 
- Eine SharePoint-Entwicklungsumgebung (Add-In-Isolierung für lokale Szenarios erforderlich)
    
 
Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Office-Entwicklung](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

 

### <a name="core-concepts-to-know-before-using-the-chrome-control"></a>Kernkonzepte, die Ihnen vor der Verwendung des Chromsteuerelements bekannt sein sollten

Die folgende Tabelle enthält eine Liste von Artikeln, die das Verständnis der Konzepte erleichtern, die in einem Szenario mit dem Chromsteuerelement relevant sind.
 

 

**Tabelle 1. Kernkonzepte der Verwendung des Chromsteuerelements**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [SharePoint-Add-Ins](sharepoint-add-ins)|Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.|
| [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)|Hier erfahren Sie mehr über die UX-Optionen (User eXperience, Benutzerumgebung) und Alternativen beim Erstellen von SharePoint-Add-Ins.|
| [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint 2013](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|Lernen Sie den Unterschied zwischen Hostwebs und App-Webs kennen. Erfahren Sie, welche SharePoint-Komponenten in eine SharePoint-Add-In eingeschlossen werden können, welche Komponenten im Hostweb und welche im App-Web bereitgestellt werden und wie das App-Web in einer isolierten Domäne bereitgestellt wird.|

## <a name="code-example-use-the-chrome-control-in-your-cloud-hosted-add-in"></a>Codebeispiel: Verwenden des Chromsteuerelements in einem in der Cloud gehosteten Add-In
<a name="SP15Usechromecontrol_Codeexample"> </a>

Ein in der Cloud gehostetes Add-In enthält mindestens eine Remotekomponente. Weitere Informationen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in). Um das Chromsteuerelement in einem in der Cloud gehosteten Add-In zu verwenden, führen Sie folgende Schritte aus:
 

 

1. Erstellen Sie die SharePoint-Add-In- und Remoteweb-Projekte.
    
 
2. Senden Sie Standardkonfigurationsinformationen in der Abfragezeichenfolge.
    
 
3. Fügen Sie dem Webprojekt eine Webseite hinzu.
    
 
In Abbildung 1 ist eine Remotewebseite mit dem Chromsteuerelement dargestellt.
 

 

**Abbildung 1. Remotewebseite mit dem Chromsteuerelement**

 

 
![Eine Remotewebseite mit dem Chromsteuerelement](../../images/ChromeControl_result.png)
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a>So erstellen Sie die SharePoint-Add-In- und Remoteweb-Projekte


1. Öffnen Sie Visual Studio 2015 als Administrator. (Klicken Sie dazu im Menü **Start** mit der rechten Maustaste auf das Symbol für Visual Studio 2015, und wählen Sie **Als Administrator ausführen** aus.)
    
 
2. Erstellen Sie ein neues Projekt unter Verwendung der Vorlage **SharePoint-Add-In**.
    
    Abbildung 2 zeigt den Speicherort der Vorlage **SharePoint-Add-In** in Visual Studio 2015 unter **Vorlagen**, **Visual C#**, **Office/SharePoint**, **Office-Add-Ins**.
    

    **Abbildung 2. Visual Studio-Vorlage für SharePoint-Add-Ins**

 

  ![Speicherort der Visual Studio-Vorlage „SharePoint-Add-In“](../../images/AppForSharePointVSTemplate.PNG)
 

 

 
3. Geben Sie die URL der SharePoint-Website an, die Sie für das Debugging verwenden möchten.
    
 
4. Wählen Sie **Von Anbieter gehostet** als Option zum Hosten Ihres Add-Ins aus. Ein Codebeispiel für ein von SharePoint gehostetes Add-In finden Sie unter [SharePoint-Add-in-JSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-BasicDataOperations).
    
    Nachdem der Assistent beendet wurde, sollte der **Projektmappen-Explorer** eine Struktur ähnlich wie in Abbildung 3 zeigen.
    

    **Abbildung 3: SharePoint-Add-In-Projekte im Projektmappen-Explorer**

 

  ![SharePoint-Add-In-Projekte im Projektmappen-Explorer](../../images/AppVSTemplateSolutionExplorer.jpg)
 

 

 

### <a name="to-send-default-configuration-options-in-the-query-string"></a>So senden Sie Standardkonfigurationsoptionen in der Abfragezeichenfolge


1. Öffnen Sie die Datei „Appmanifest.xml“ im Manifest-Editor.
    
 
2. Fügen Sie der Abfragezeichenfolge das **{StandardTokens}**-Token und einen zusätzlichen _SPHostTitle_-Parameter hinzu. Abbildung 4 zeigt den Manifest-Editor mit den konfigurierten Abfragezeichenfolgen-Parametern.
    
    **Abbildung 4. Manifest-Editor mit Abfragezeichenfolgen-Parametern für das Chromsteuerelement**

 

  ![Manifest-Editor mit Abfragezeichenfolge-Parametern](../../images/ChromeControl_manifest.PNG)
 

    Das Chromsteuerelement übernimmt automatisch die folgenden Werte aus der Abfragezeichenfolge:
    
 

      -  **SPHostUrl**
    
 
  -  **SPHostTitle**
    
 
  -  **SPAppWebUrl**
    
 
  -  **SPLanguage**
    
 

     **{StandardTokens} ** umfassen **SPHostUrl** und **SPAppWebUrl**.
    
 

### <a name="to-add-a-page-that-uses-the-chrome-control-in-the-web-project"></a>So fügen Sie dem Webprojekt eine Seite hinzu, in der das Chromsteuerelement verwendet wird


1. Klicken Sie mit der rechten Maustaste auf das Webprojekt, und fügen Sie ein neues Web Form hinzu.
    
 
2. Kopieren Sie das folgende Markup, und fügen Sie es in die ASPX-Seite ein. Das Markup führt folgende Aufgaben aus:
    
      - Laden der AJAX-Bibliothek aus dem Microsoft CDN (Content Delivery Network).
    
 
  - Laden der jQuery-Bibliothek aus dem Microsoft CDN.
    
 
  - Laden der Datei „SP.UI.Controls.js“ mit der jQuery-Funktion **getScript**.
    
 
  - Definieren einer Rückruffunktion für das **onCssLoaded**-Ereignis.
    
 
  - Vorbereiten der Optionen für das Chromsteuerelement.
    
 
  - Initialisieren des Chromsteuerelements.
    
 

```HTML
  <!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Chrome control host page</title>
    <script 
        src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
        type="text/javascript">
    </script>
    <script 
        type="text/javascript" 
        src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
    </script>      
    <script 
        type="text/javascript"
        src="ChromeLoader.js">
    </script>
<script type="text/javascript">
"use strict";

var hostweburl;

//load the SharePoint resources
$(document).ready(function () {
    //Get the URI decoded URL.
    hostweburl =
        decodeURIComponent(
            getQueryStringParameter("SPHostUrl")
    );

    // The SharePoint js files URL are in the form:
    // web_url/_layouts/15/resource
    var scriptbase = hostweburl + "/_layouts/15/";

    // Load the js file and continue to the 
    //   success handler
    $.getScript(scriptbase + "SP.UI.Controls.js", renderChrome)
});

// Callback for the onCssLoaded event defined
//  in the options object of the chrome control
function chromeLoaded() {
    // When the page has loaded the required
    //  resources for the chrome control,
    //  display the page body.
    $("body").show();
}

//Function to prepare the options and render the control
function renderChrome() {
    // The Help, Account and Contact pages receive the 
    //   same query string parameters as the main page
    var options = {
        "appIconUrl": "siteicon.png",
        "appTitle": "Chrome control add-in",
        "appHelpPageUrl": "Help.html?"
            + document.URL.split("?")[1],
        // The onCssLoaded event allows you to 
        //  specify a callback to execute when the
        //  chrome resources have been loaded.
        "onCssLoaded": "chromeLoaded()",
        "settingsLinks": [
            {
                "linkUrl": "Account.html?"
                    + document.URL.split("?")[1],
                "displayName": "Account settings"
            },
            {
                "linkUrl": "Contact.html?"
                    + document.URL.split("?")[1],
                "displayName": "Contact us"
            }
        ]
    };

    var nav = new SP.UI.Controls.Navigation(
                            "chrome_ctrl_placeholder",
                            options
                        );
    nav.setVisible(true);
}

// Function to retrieve a query string value.
// For production purposes you may want to use
//  a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
    var params =
        document.URL.split("?")[1].split("&amp;");
    var strParams = "";
    for (var i = 0; i < params.length; i = i + 1) {
        var singleParam = params[i].split("=");
        if (singleParam[0] == paramToRetrieve)
            return singleParam[1];
    }
}
</script>
</head>

<!-- The body is initally hidden. 
     The onCssLoaded callback allows you to 
     display the content after the required
     resources for the chrome control have
     been loaded.  -->
<body style="display: none">

    <!-- Chrome control placeholder -->
    <div id="chrome_ctrl_placeholder"></div>

    <!-- The chrome control also makes the SharePoint
          Website stylesheet available to your page -->
    <h1 class="ms-accentText">Main content</h1>
    <h2 class="ms-accentText">The chrome control</h2>
    <div id="MainContent">
        This is the page's main content. 
        You can use the links in the header to go to the help, 
        account or contact pages.
    </div>
</body>
</html>
```

3. Sie können das Chromsteuerelement auch in deklarativem Code verwenden. Im folgenden Codebeispiel wird das Chromsteuerelement im HTML-Markup deklariert, ohne dass JavaScript-Code zum Konfigurieren und Initialisieren des Steuerelements verwendet wird. Das nachstehende Markup führt die folgenden Aufgaben aus:
    
      - Bereitstellen eines Platzhalters für die JavaScript-Datei „SP.UI.Controls.js“.
    
 
  - Dynamisches Laden der Datei „SP.UI.Controls.js“.
    
 
  - Bereitstellen eines Platzhalters für das Chromsteuerelement und Angeben der Optionen inline im HTML-Markup.
    
 

```HTML
  <!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Chrome control host page</title>
    <script 
        src="http://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
        type="text/javascript">
    </script>
    <script 
        type="text/javascript" 
        src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
    </script>      
    <script type="text/javascript">
    var hostweburl;

    // Load the SharePoint resources.
    $(document).ready(function () {

        // Get the URI decoded add-in web URL.
        hostweburl =
            decodeURIComponent(
                getQueryStringParameter("SPHostUrl")
        );

        // The SharePoint js files URL are in the form:
        // web_url/_layouts/15/resource.js
        var scriptbase = hostweburl + "/_layouts/15/";

        // Load the js file and continue to the 
        // success handler.
        $.getScript(scriptbase + "SP.UI.Controls.js")
    });

    // Function to retrieve a query string value.
    // For production purposes you may want to use
    // a library to handle the query string.
    function getQueryStringParameter(paramToRetrieve) {
        var params =
            document.URL.split("?")[1].split("&amp;");
        var strParams = "";
        for (var i = 0; i < params.length; i = i + 1) {
            var singleParam = params[i].split("=");
            if (singleParam[0] == paramToRetrieve)
                return singleParam[1];
        }
    }
    </script>
</head>
<body>

    <!-- Chrome control placeholder 
           Options are declared inline.  -->
    <div 
        id="chrome_ctrl_container"
        data-ms-control="SP.UI.Controls.Navigation"  
        data-ms-options=
            '{  
                "appHelpPageUrl" : "Help.html",
                "appIconUrl" : "siteIcon.png",
                "appTitle" : "Chrome control add-in",
                "settingsLinks" : [
                    {
                        "linkUrl" : "Account.html",
                        "displayName" : "Account settings"
                    },
                    {
                        "linkUrl" : "Contact.html",
                        "displayName" : "Contact us"
                    }
                ]
             }'>
    </div>
    
    <!-- The chrome control also makes the SharePoint
          Website style sheet available to your page. -->
    <h1 class="ms-accentText">Main content</h1>
    <h2 class="ms-accentText">The chrome control</h2>
    <div id="MainContent">
        This is the page's main content. 
        You can use the links in the header to go to the help, 
        account or contact pages.
    </div>
</body>
</html>
```


    The SP.UI.Controls.js library automatically renders the control if it finds the  **data-ms-control="SP.UI.Controls.Navigation"** attribute in a **div** element.
    
 

### <a name="to-edit-the-startpage-element-in-the-add-in-manifest"></a>So bearbeiten Sie das StartPage-Element im Add-In-Manifest


1. Doppelklicken Sie im **Projektmappen-Explorer** auf die Datei **AppManifest.xml**.
    
 
2. Wählen Sie im Dropdownmenü **Startseite** die Webseite aus, auf der das Chromsteuerelement verwendet wird.
    
 

### <a name="to-build-and-run-the-solution"></a>So erstellen Sie die Lösung und führen sie aus


1. Stellen Sie sicher, dass das "SharePoint-Add-In"-Projekt als Startprojekt festgelegt ist.
    
 
2. Drücken Sie F5.
    
     **Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.
3. Klicken Sie auf die Schaltfläche **Vertrauen**.
    
 
4. Klicken Sie auf das Symbol des Add-Ins **ChromeControlCloudhosted**.
    
 
5. Wenn Sie das Chromsteuerelement in Webseiten verwenden, können Sie auch das SharePoint-Website-Stylesheet verwenden, das in Abbildung 4 dargestellt ist.
    
    **Abbildung 5. Auf der Seite verwendetes SharePoint-Website-Stylesheet**

 

  ![Auf einer Seite verwendetes SharePoint-Website-Stylesheet](../../images/ChromControl_stylesheet.png)
 

 

 

**Tabelle 2: Problembehandlung für die Lösung**


|**Problem**|**Lösung**|
|:-----|:-----|
|Unbehandelte Ausnahme **SP ist undefiniert**.|Stellen Sie sicher, dass Ihr Browser die Datei „SP.UI.Controls.js“ lädt.|
|Das Chromsteuerelement wird nicht ordnungsgemäß gerendert.|Das Chromsteuerelement unterstützt nur Dokumentmodi von Internet Explorer 8 und höher. Stellen Sie sicher, dass Ihr Browser Ihre Seite im Dokumentmodus von Internet Explorer 8 oder höher rendert.|
|Zertifikatfehler|Legen Sie die Eigenschaft **SSL-aktiviert** des Webprojekts auf „false“ fest. Legen Sie im SharePoint-Add-In-Projekt die Eigenschaft **Webprojekt** auf „Kein“ fest, und setzen Sie die Eigenschaft dann wieder auf den Namen des Webprojekts zurück. |

## <a name="next-steps"></a>Nächste Schritte
<a name="SP15Usechromecontrol_Nextsteps"> </a>

In diesem Artikel wird gezeigt, wie Sie das Chromsteuerelement in einem SharePoint-Add-In verwenden. Im nächsten Schritt können Sie sich über UX-Komponenten informieren, die für SharePoint-Add-Ins verfügbar sind. Nähere Einzelheiten finden Sie unter:
 

 

-  [Codebeispiel: Verwenden des Chromsteuerelements in einem in der Cloud gehosteten Add-In](http://code.msdn.microsoft.com/SharePoint-2013-Work-with-089ecc6f)
    
 
-  [Codebeispiel: Verwenden des Chromsteuerelements und der domänenübergreifenden Bibliothek (CSOM)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
    
 
-  [Codebeispiel: Verwenden des Chromsteuerelements und der domänenübergreifenden Bibliothek (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
    
 
-  [Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins)
    
 
-  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Usechromecontrol_Addresources"> </a>


-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)
    
 
-  [Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Drei Methoden für Entwurfsoptionen für SharePoint-Add-Ins](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

