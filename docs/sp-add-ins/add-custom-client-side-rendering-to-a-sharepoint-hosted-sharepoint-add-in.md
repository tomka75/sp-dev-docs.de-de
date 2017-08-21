# <a name="add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="e62d5-101">Hinzufügen des benutzerdefinierten clientseitigen Renderings für ein von SharePoint gehostetes SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="e62d5-101">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="e62d5-102">Passen Sie das Rendering und die Prüfung von Steuerelementen in SharePoint-Add-In-Seiten an.</span><span class="sxs-lookup"><span data-stu-id="e62d5-102">Customize the rendering and validation of controls in  spappplural pages.</span></span>
 
<span data-ttu-id="e62d5-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e62d5-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 
<span data-ttu-id="e62d5-p102">Dies ist der achte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="e62d5-p102">Customize the rendering and validation of controls in SharePoint Add-ins pages. This is the eighth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 
-  [<span data-ttu-id="e62d5-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e62d5-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
-  [<span data-ttu-id="e62d5-109">Bereitstellung und Installation eines von SharePoint gehosteten Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="e62d5-110">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
-  [<span data-ttu-id="e62d5-111">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
-  [<span data-ttu-id="e62d5-112">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="e62d5-113">Hinzufügen eines Workflows zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="e62d5-114">Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e62d5-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in)

<span data-ttu-id="e62d5-p103">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeClientRenderedControl.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeClientRenderedControl.sln file.</span></span>
 
<span data-ttu-id="e62d5-p104">Sie können etwas clientseitiges JavaScript verwenden, um das Rendering von Webparts, der meisten Typen von Feldern (Spalten) und anderer Steuerelemente anzupassen, indem Sie eine JavaScript-Datei zur Eigenschaft **JSLink** des Steuerelements zuweisen, z. B. **SPField.JSLink**. Sie können auch clientseitige Prüflogik auf diese Weise hinzufügen. In diesem Artikel passen Sie das Rendering eines Felds in einer Liste des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ mithilfe von clientseitigem Rendering an.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p104">You can use a little client-side JavaScript to customize the rendering of Web Parts, most types of fields (columns), and some other controls, by assigning a JavaScript file to the **JSLink** property of the control, such as **SPField.JSLink**. You can also add client-side validation logic in this way. In this article you customize the rendering of a field in a list of the Employee Orientation SharePoint Add-in by using client-side rendering.</span></span>
 
 <span data-ttu-id="e62d5-120">**Hinweis** Wenn der Endbenutzer JavaScript in seinem Browser deaktiviert hat, greift SharePoint auf das serverseitige Rendern und Prüfen zurück.</span><span class="sxs-lookup"><span data-stu-id="e62d5-120">**Note** If the end-user has JavaScript disabled in their browser, SharePoint will fall back to server-side rendering and validation.</span></span>
 
 <span data-ttu-id="e62d5-p105">**Hinweis** Die JSLink-Eigenschaft wird nicht für Umfrage- oder Ereignislisten nicht unterstützt. Ein SharePoint-Kalender ist eine Ereignisliste.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p105">**Note** The JSLink property is not supported on Survey or Events lists. A SharePoint calendar is an Events list.</span></span>
 
## <a name="create-and-register-the-javascript"></a><span data-ttu-id="e62d5-123">Erstellen und registrieren des JavaScript-Codes</span><span class="sxs-lookup"><span data-stu-id="e62d5-123">Create and register the JavaScript</span></span>

- <span data-ttu-id="e62d5-124">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten **Skripts**, und wählen Sie **Hinzufügen** > **Neues Element** > **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="e62d5-124">In **Solution Explorer**, right-click the **Scripts** node and choose **Add** > **New Item** > **Web**.</span></span>
- <span data-ttu-id="e62d5-125">Wählen Sie **JavaScript-Datei**, und nennen Sie die Datei „OrientationStageRendering.js“.</span><span class="sxs-lookup"><span data-stu-id="e62d5-125">Choose **JavaScript File** and name itOrientationStageRendering.js.</span></span>
- <span data-ttu-id="e62d5-126">Ihr benutzerdefiniertes Rendern des Felds sollte automatisch erfolgen. Fügen Sie daher eine anonyme Methode zum JavaScript hinzu, die automatisch ausgeführt wird, wenn die Datei mit dem folgenden Code geladen wird.</span><span class="sxs-lookup"><span data-stu-id="e62d5-126">Your custom rendering of the field should happen automatically, so add an anonymous method to the JavaScript that runs automatically when the file loads with the following code.</span></span>

```
  (function () {

})();
```

- <span data-ttu-id="e62d5-127">Fügen Sie im Textkörper dieser Methode (zwischen den {}-Zeichen) den folgenden Code zum Erstellen von JSON-Objekten (Javascript Object Notation) für den Renderingüberschreibungskontext, die Vorlagen in dem Kontext und die Vorlagen für die Felder hinzu.</span><span class="sxs-lookup"><span data-stu-id="e62d5-127">In the body fo this method (between the { } characters), add the following code to create JSON (Javascript Object Notation) objects for the rendering override context, the templates in the context, and the templates for the fields.</span></span>
    
```
  var customRenderingOverride = {};
customRenderingOverride.Templates = {};
customRenderingOverride.Templates.Fields = {

}
```

- <span data-ttu-id="e62d5-p106">Fügen Sie im Textkörper des  `Fields`-Vorlagenobjekts das folgende JSON-Objekt ein. Der Name der Eigenschaft  `OrientationStage` identifiziert das Feld, mit dem das Rendering angepasst wurde. Der Wert der Eigenschaft ist ein weiteres JSON-Objekt. Die Eigenschaft `View` gibt den Seitenkontext an, in dem das benutzerdefinierte Rendering angewendet wird. In diesem Fall teilt das Objekt SharePoint mit, das benutzerdefinierte Rendering auf Listenansichten zu verwenden. (Weitere Optionen sind die Formulare zum Bearbeiten, für neue Element und zum Anzeigen.) Der Wert der Eigenschaft `renderOrientationStage` ist der Name der benutzerdefiniertes Renderingmethode, die Sie in einem späteren Schritt erstellen.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p106">In the body of the  `Fields` template object, add the following JSON. The property name `OrientationStage` identifies the field that has customized rendering. The value of the property is another JSON object. The `View` property identifies the page context in which the custom rendering is applied. In this case, the object is telling SharePoint to use the customized rendering on list views. (Other options would be for the Edit, New, and Display forms.) The value of the property, `renderOrientationStage`, is the name of the custom rendering method which you create in a later step.</span></span>
    
```
  "OrientationStage": { "View": renderOrientationStage }
```

- <span data-ttu-id="e62d5-p107">Die letzte Aktion, die die anonyme Methode durchführen muss, besteht darin, den Vorlagen-Manager von SharePoint die Renderingüberschreibung zu informieren. Fügen Sie die folgende Zeile am Ende des Hauptteils der Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p107">The last thing that the anonymous method must do is tell SharePoint's template manager about the rendering override. Add the following line to the end of the body of the method.</span></span>
    
```
  SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
```

   <span data-ttu-id="e62d5-136">Die Methode sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="e62d5-136">The method should now look like the following.</span></span>
    
```
  (function () {
    var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = {
        "OrientationStage": { "View": renderOrientationStage }
    }

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
})();
```

- <span data-ttu-id="e62d5-p108">Fügen Sie die folgende Methode zur Datei hinzu. Sie legt die Farbe des Werts in der Spalte **Orientierungsphase** auf Rot fest, wenn der Wert „Nicht gestartet“ ist, und auf Grün, wenn der Wert „Abgeschlossen“ ist. (Das `ctx`-Objekt ist ein Clientkontextobjekt, das vom standardmäßigen SharePoint-Skript deklariert wird.)</span><span class="sxs-lookup"><span data-stu-id="e62d5-p108">Add the following method to the file. It sets the color of the **Orientation Stage** column value to red when the value is "Not Started" and to green when the value is "Completed". (The `ctx` object is a client context object that is declared by in-the-box SharePoint script.)</span></span>
    
```
  function renderOrientationStage(ctx) {
    var orientationStageValue = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];
    if (orientationStageValue == "Not Started")  {
        return "<span style='color:red'>" + orientationStageValue + "</span>"
    }
    else if (orientationStageValue == "Completed") {
        return "<span style='color:green'>" + orientationStageValue + "</span>"
    }
    else {
        return orientationStageValue;
    }
}
```

- <span data-ttu-id="e62d5-140">Erweitern Sie im **Projektmappen-Explorer** **Websitespalten** und dann **OrientationStage**, und öffnen Sie dann die Datei „elements.xml“.</span><span class="sxs-lookup"><span data-stu-id="e62d5-140">In **Solution Explorer**, expand **Site Columns** and then **OrientationStage**; and then open the elements.xml file.</span></span> 
- <span data-ttu-id="e62d5-141">Um SharePoint anzuweisen, Ihren benutzerdefinierten JavaScript-Code zu verwenden, fügen Sie eine neues **JSLink**-Attribut zum **Field**-Element hinzu, und weisen dann die folgende URL als Wert zu: `~site/Scripts/OrientationStageRendering.js`.</span><span class="sxs-lookup"><span data-stu-id="e62d5-141">To tell SharePoint to use your custom JavaScript, add a new attribute, **JSLink**, to the **Field** element, and then assign the following URL as its value: `~site/Scripts/OrientationStageRendering.js`.</span></span>
    
<span data-ttu-id="e62d5-p109">**Hinweis** Die Eigenschaft **JSLink** ist immer eine Datei, keine Methode. Es gibt keine Möglichkeit, SharePoint mitzuteilen, welche Methode ausgeführt werden soll. Aus diesem Grund enthält die Datei eine Methode, die automatisch ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p109">**Note** The **JSLink** property is always a file, not a method. There's no way to tell SharePoint which method to run. That is why the file contains a method that runs automatically.</span></span>

<span data-ttu-id="e62d5-145">Das Start-Tag für das **Field**-Element sieht nun wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="e62d5-145">The start tag for the **Field** element will now look like the following.</span></span>
    
```
  <Field
       ID="{some_guid_here}"
       Name="OrientationStage"
       Title="OrientationStage"
       DisplayName="Orientation Stage"
       Description="The current orientation stage of the employee."
       Type="Choice"
       Required="TRUE"
       Group="Employee Orientation" 
       JSLink="~site/Scripts/OrientationStageRendering.js">
<!-- child elements and end tag omitted -->
```

- <span data-ttu-id="e62d5-146">Öffnen Sie die Seite „Default.aspx“, und fügen Sie den folgenden Code als letztes untergeordnetes Element des **asp:Content**-Elements hinzu, dessen **ContentPlaceHolderID** auf **PlaceHolderMain** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="e62d5-146">Open the Default.aspx page and add the following code as the last child of the **asp:Content** element that has **ContentPlaceHolderID** set to **PlaceHolderMain**.</span></span> 
    
```XML
  <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
    Text="List View Page for New Employees in Seattle" /></p>

```

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="e62d5-147">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e62d5-147">Run and test the add-in</span></span>

- <span data-ttu-id="e62d5-p110">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p110">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
 
- <span data-ttu-id="e62d5-p111">Das clientseitige Rendering, das Sie konfiguriert haben, wirkt sich nur in der Listenansichtsseite auf das Rendering des Felds aus, nicht jedoch im Listenansicht-Webpart, das wir auf der Startseite abgelegt haben. Der Grund hierfür ist, dass das Webpart standardmäßig das serverseitige Rendering verwendet. Es gibt Möglichkeiten, dies umzukehren, aber diese sind zu fortgeschritten für dieses einfache Beispiel. Um also das clientseitige Rendering in Aktion zu sehen, klicken Sie auf den Link am unteren Rand der Seite **Listenansichtsseite für neue Mitarbeiter in Seattle**.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p111">The client-side rendering that you have configured affects the rendering of the field only on the list view page, not in the list view Web Part that we put on the home page. This is because the Web Part defaults to server-side rendering. There are ways to reverse this, but they are too advanced for this simple example. So, to see the client-side rendering in action, click the link at the bottom of the page **List View Page for New Employees in Seattle**.</span></span>
 
- <span data-ttu-id="e62d5-154">Wenn die Listenansichtsseite geöffnet wird, legen Sie den Wert **Orientierungsphase** für einige Elemente auf **Nicht gestartet** und für andere auf **Abgeschlossen** fest, um das benutzerdefinierte Farbrendering anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e62d5-154">When the list view page opens, set the **Orientation Stage** value for some items to **Not Started** and set others to **Completed** to see the custom color rendering.</span></span>
    
<span data-ttu-id="e62d5-155">**Liste mit benutzerdefiniertem clientseitigem Rendering**</span><span class="sxs-lookup"><span data-stu-id="e62d5-155">**List with custom client-side rendering**</span></span>

![Liste "Neue Mitarbeiter in Seattle" mit den Orientierungsphasewerten "Nicht gestartet" in Rot und "Abgeschlossen" in Grün. Andere Werte in Schwarz.](../../images/dc8e2b7d-1747-4b65-aab4-6fc93c6867d4.PNG)
  
- <span data-ttu-id="e62d5-p113">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p113">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
- <span data-ttu-id="e62d5-p114">Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="e62d5-p114">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>

## 
<span data-ttu-id="e62d5-162"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="e62d5-162"></span></span>

<span data-ttu-id="e62d5-163">Im nächsten Artikel dieser Reihe fügen Sie ein benutzerdefiniertes Menüelement und eine benutzerdefinierte Schaltfläche zum Menüband im SharePoint-Add-In hinzu:  [Erstellen einer benutzerdefinierten Menübandschaltfläche im Hostweb eines SharePoint-Add-Ins](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="e62d5-163">In the next article in this series, you'll add a custom menu item and custom button to the ribbon in the SharePoint Add-in:  [Create a custom ribbon button in the host web of a SharePoint Add-in](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in).</span></span>
 
