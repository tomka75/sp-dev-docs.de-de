# <a name="customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering"></a>Anpassen einer Listenansicht in SharePoint-Add-Ins durch clientseitiges Rendering
Erfahren Sie, wie Sie eine Listenansicht in einem von SharePoint gehosteten Add-In mithilfe der clientseitigen Renderingtechnologie in SharePoint anpassen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

In SharePoint stellt das clientseitige Rendering eine Möglichkeit dar, wie Sie Ihre eigene Ausgabe für eine Gruppe von Steuerelementen, die in einer SharePoint-Seite gehostet werden, erzeugen können. Es ermöglicht Ihnen, weit verbreitete Technologien wie HTML und JavaScript zum Definieren der Renderinglogik von SharePoint-Listenansichten zu verwenden. Beim clientseitigen Rendering können Sie Ihre eigenen JavaScript-Ressourcen definieren und sie in den für Ihre Add-Ins verfügbaren Datenspeicheroptionen hosten, beispielsweise in einer Dokumentbibliothek. Ein von SharePoint gehostetes Add-In enthält nur SharePoint-Komponenten. Die Ressourcen eines von SharePoint gehosteten Add-Ins befinden sich auf einer isolierten Unterwebsite des Hostwebs, die als Add-In-Web bezeichnet wird.
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Voraussetzungen für die Verwendung der Beispiele in diesem Artikel
<a name="SP15CSRlistview_Prereq"> </a>

Um die Schritte in diesem Beispiel auszuführen, benötigen Sie Folgendes:
 

 

-  [Visual Studio 2015 und die neuesten Microsoft Office Developer Tools ](https://www.visualstudio.com/features/office-tools-vs)
    
 
- Eine SharePoint-Entwicklungsumgebung (Add-In-Isolierung für lokale Szenarios erforderlich)
    
 
Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Office-Entwicklung](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

 

### <a name="core-concepts-to-help-you-understand-list-view-customization-with-client-side-rendering"></a>Kernkonzepte zum Verständnis der Anpassung von Listenansichten mittels clientseitigem Rendering

Die folgende Tabelle enthält eine Liste hilfreicher Artikel, die es Ihnen erleichtern können, die für die Anpassung von Listenansichten relevanten Konzepte zu verstehen.
 

 

**Tabelle 1. Kernkonzepte für die Anpassung von Listenansichten in einem Add-In**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [SharePoint-Add-Ins](sharepoint-add-ins)|In diesem Artikel erfahren Sie mehr über das neue Add-In-Modell in Microsoft SharePoint, das Sie zur Erstellung von Add-Ins verwenden können, die einfache, benutzerfreundliche Lösungen für Endbenutzer darstellen.|
| [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)|Hier erfahren Sie mehr über die UX-Optionen beim Erstellen von SharePoint-Add-Ins.|
| [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|In diesem Artikel erfahren Sie, welche Unterschiede zwischen Hostwebs und App-Webs bestehen. Sie erfahren zudem, welche SharePoint-Komponenten in eine SharePoint-Add-In aufgenommen werden können, welche Komponenten für das Hostweb und welche für das App-Web bereitgestellt werden und wie das App-Web in einer isolierten Domäne bereitgestellt wird.|

## <a name="code-example-customize-a-list-view-by-using-client-side-rendering"></a>Codebeispiel: Anpassen einer Listenansicht durch clientseitiges Rendering
<a name="SP15CSRlistview_Codeexample"> </a>

Um eine Listenansicht anzupassen, die mittels clientseitigem Rendering im Add-In-Web bereitgestellt wird, führen Sie folgende Schritte aus:
 

 

1. Erstellen Sie das SharePoint-Add-In-Projekt.
    
 
2. Erstellen Sie eine neue Listendefinition mit einer benutzerdefinierten Ansicht.
    
 
3. Stellen Sie die benutzerdefinierte Renderinglogik in einer JavaScript-Datei bereit.
    
 
Abbildung 1 zeigt eine clientseitig gerenderte Ansicht einer Liste mit Ankündigungen.
 

 

**Abbildung 1. Benutzerdefinierte Ansicht einer Liste mit Ankündigungen**

 

 
![Benutzerdefinierte Ansicht einer Liste mit Ankündigungen](../../images/CSRListView_result.png)
 

### <a name="to-create-the-sharepoint-add-in-project"></a>So erstellen Sie das SharePoint-Add-In-Projekt


1. Öffnen Sie Visual Studio 2015 als Administrator. (Klicken Sie dazu im Menü **Start** mit der rechten Maustaste auf das Symbol für **Visual Studio**, und wählen Sie **Als Administrator ausführen** aus.)
    
 
2. Erstellen Sie ein neues Projekt unter Verwendung der Vorlage **SharePoint-Add-In**.
    
    Abbildung 2 zeigt den Speicherort der Vorlage **SharePoint-Add-In** in Visual Studio 2015 unter **Vorlagen**, **Visual C#**, **Office/SharePoint**, **Office-Add-Ins**.
    

    **Abbildung 2. Visual Studio-Vorlage „SharePoint-Add-In“**

 

  ![Visual Studio-Vorlage „SharePoint-Add-In“](../../images/AppForSharePointVSTemplate.PNG)
 

 

 
3. Geben Sie die URL der SharePoint-Website an, die Sie für das Debugging verwenden möchten.
    
 
4. Wählen Sie **Von SharePoint gehostet** als Hostingoption für Ihr Add-In aus.
    
 

### <a name="to-create-a-new-list-definition"></a>So erstellen Sie eine neue Listendefinition


1. Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und fügen Sie dann ein neues Element vom Typ **Liste** hinzu. Erstellen Sie eine anpassbare Liste, die auf Ankündigungen basiert.
    
 
2. Kopieren Sie das folgende Markup, und fügen Sie es in das **Views**-Element der Datei „Schema.xml“ des Listenfeatures ein. Das Markup führt folgende Aufgaben aus:
    
      - Deklarieren einer neuen Ansicht namens „Overridable“ mit der BaseViewID 2.
    
 
  - Bereitstellen eines Werts für das **JSLink**-Element, das auf eine JavaScript-Datei zeigt, die zusammen mit dem Add-In bereitgestellt wird.
    
     **Hinweis** Die JSLink-Eigenschaft wird für Umfrage- oder Ereignislisten nicht unterstützt. Ein SharePoint-Kalender ist eine Ereignisliste.

```XML
  <View BaseViewID="2" 
      Name="8d2719f3-c3c3-415b-989d-33840d8e2ddb" 
      DisplayName="Overridable" 
      Type="HTML" 
      WebPartZoneID="Main" 
      SetupPath="pages\viewpage.aspx" 
      Url="Overridable.aspx"
      DefaultView="TRUE">
  <ViewFields>
    <FieldRef Name="Title" />
  </ViewFields>
  <Query />
  <Toolbar Type="Standard" />
  <XslLink>main.xsl</XslLink>
  <JSLink Default="TRUE">~site/Scripts/CSRListView.js</JSLink>
</View>
```


### <a name="to-provide-the-custom-rendering-logic-in-a-javascript-file"></a>So stellen Sie eine benutzerdefinierte Renderinglogik in einer JavaScript-Datei bereit


1. Klicken Sie mit der rechten Maustaste auf den Ordner **Skripts**, und fügen Sie eine neue JavaScript-Datei ein. Geben Sie der Datei den Namen „CSRListView.js“.
    
 
2. Kopieren Sie den folgenden Code, und fügen Sie ihn in die Datei „CSRListView.js“ ein. Der Code führt folgende Aufgaben aus:
    
      - Bereitstellen von Ereignishandlern für die Ereignisse **PreRender** und **PostRender**
    
 
  - Bereitstellen von Vorlagen für die Vorlagengruppen „Header“, „Footer“ und „Item“.
    
 
  - Registrieren der Vorlagen
    
 

```
  (function () {
    // Initialize the variable that stores the objects.
    var overrideCtx = {};
    overrideCtx.Templates = {};

    // Assign functions or plain html strings to the templateset objects:
    // header, footer and item.
    overrideCtx.Templates.Header = "<B><#=ctx.ListTitle#></B>" +
        "<hr><ul id='unorderedlist'>";

    // This template is assigned to the CustomItem function.
    overrideCtx.Templates.Item = customItem;
    overrideCtx.Templates.Footer = "</ul>";

    // Set the template to the:
    //  Custom list definition ID
    //  Base view ID
    overrideCtx.BaseViewID = 2;
    overrideCtx.ListTemplateType = 10057;

    // Assign a function to handle the
    // PreRender and PostRender events
    overrideCtx.OnPreRender = preRenderHandler;
    overrideCtx.OnPostRender = postRenderHandler;

    // Register the template overrides.
    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(overrideCtx);
})();

// This function builds the output for the item template.
// It uses the context object to access announcement data.
function customItem(ctx) {

    // Build a listitem entry for every announcement in the list.
    var ret = "<li>" + ctx.CurrentItem.Title + "</li>";
    return ret;
}

// The preRenderHandler attends the OnPreRender event
function preRenderHandler(ctx) {

    // Override the default title with user input.
    ctx.ListTitle = prompt("Type a title", ctx.ListTitle);
}

// The postRenderHandler attends the OnPostRender event
function postRenderHandler(ctx) {

    // You can manipulate the DOM in the postRender event
    var ulObj;
    var i, j;

    ulObj = document.getElementById("unorderedlist");
    
    // Reverse order the list.
    for (i = 1; i < ulObj.children.length; i++) {
        var x = ulObj.children[i];
        for (j = 1; j < ulObj.children.length; j++) {
            var y = ulObj.children[j];
            if(x.innerText<y.innerText){                  
                ulObj.insertBefore(y, x);
            }
        }
    }
}
```


### <a name="to-build-and-run-the-solution"></a>So erstellen Sie die Lösung und führen Sie sie aus


1. Drücken Sie F5.
    
     **Hinweis** Wenn Sie F5 drücken, erstellt Visual Studio die Lösung, stellt das Add-In bereit und öffnet die Berechtigungsseite für das Add-In.
2. Klicken Sie auf die Schaltfläche **Vertrauen**.
    
 
3. Navigieren Sie zu der benutzerdefinierten Liste, indem Sie die Adresse  _/Lists/<your_list_instance>_ relativ zum App-Verzeichnis in der App-Webdomäne (nicht der Hostwebdomäne) eingeben. Fügen Sie eine oder zwei Ankündigungen hinzu. Wählen Sie im Menüband die Ansicht **Überschreibbar** aus.
    
 

## <a name="next-steps"></a>Nächste Schritte
<a name="SP15CSRlistview_Nextsteps"> </a>

In diesem Artikel wird gezeigt, wie Sie mithilfe des clientseitigen Renderings eine Listenansicht in einer SharePoint-Add-In anpassen können. Als Nächstes können Sie sich über andere UX-Komponenten informieren, die für SharePoint-Add-Ins verfügbar sind. Nähere Einzelheiten finden Sie unter:
 

 

-  [Codebeispiel: Anpassen einer Listenansicht in einem Add-In durch clientseitiges Rendering](http://code.msdn.microsoft.com/SharePoint-2013-Customize-61761017)
    
 
-  [Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins)
    
 
-  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15CSRlistview_AddResources"> </a>


-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)
    
 
-  [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

