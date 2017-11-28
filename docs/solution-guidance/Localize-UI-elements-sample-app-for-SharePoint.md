---
title: "Lokalisieren von UI-Elemente Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e97db9ff902347015c47cfdb6605ec74072459ed
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="localize-ui-elements-sample-add-in-for-sharepoint"></a>Lokalisieren von UI-Elemente Beispiel-add-in für SharePoint

Sie können SharePoint-UI-Elemente lokalisieren, mithilfe von JavaScript ersetzen den Textwert der ein UI-Elementwert mit einem übersetzten Text-Wert aus einer Ressource JavaScript-Datei geladen. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
[Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) -Beispiel-add-in zeigt, wie JavaScript verwenden, um der Textwert der SharePoint-UI-Element mit einem Wert übersetzten Text zu ersetzen, die aus einer Ressourcendatei JavaScript wiedergegeben wird. 

**Hinweis**  Sie sind verantwortlich für die Verwaltung der übersetzten Textwerte in der JavaScript-Ressourcendatei. 

In diesem Codebeispiel wird eine vom Anbieter gehosteten add-in, verwendet:

- Lokalisieren einer Websiteseite oder Schnellstartleiste Link Titel mit bestimmten Textwerten.
    
- Beibehalten Sie einer Websiteseite oder Schnellstartleiste Link Titel in eine primäre Sprache und Bereitstellen Sie übersetzte Versionen der Websiteseite und Schnellstartleiste Link Titel in einer anderen Sprache zur Laufzeit.
    
- Verwenden von JavaScript-Ressourcendateien für die Lokalisierung von Client Side.
    
- Verknüpfen Sie eine JavaScript-Datei mit einer SharePoint-Website mithilfe einer benutzerdefinierten Aktion.
    
- Überprüfen Sie die Benutzeroberflächenkultur der Website, und Laden Sie kulturspezifische Textwerte aus einer JavaScript-Ressourcendatei.
    
- Überschreiben Sie Websiteseite und Schnellstartleiste Link Titel mit kulturspezifische Textwerte jQuery verwenden.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Konfigurieren Sie bevor Sie dieses Codebeispiel ausführen die Language-Einstellungen auf Ihrer Website, und die Anzeigesprache auf der Profilseite des Benutzers festgelegt.

### <a name="to-configure-the-language-settings-on-your-site"></a>So konfigurieren Sie die spracheinstellungen auf Ihrer Website

1. Wählen Sie auf der Teamwebsite **Einstellungen** > **websiteeinstellungen**.
    
2. Wählen Sie in der **Die Verwaltung von** **spracheinstellungen**.
    
3. Wählen Sie auf der Seite **Spracheinstellungen** im **alternative Sprache(n)**, die alternativen Sprachen, die Ihre Website unterstützt werden soll. Wählen Sie beispielsweise **Französisch** und **Finnisch**, wie in Abbildung 1 dargestellt.
    
4. Wählen Sie  **OK** aus.

### <a name="to-set-the-display-language-on-your-users-profile-page"></a>So legen Sie die Anzeigesprache auf der Profilseite des Benutzers fest

1. Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich,** wie in Abbildung 2 dargestellt.
    
2. Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.
    
3. Wählen Sie den drei Punkten (...) für zusätzliche Optionen, und wählen Sie dann **Sprache und Region**.
    
4. **Meine Anzeigesprachen**wählen Sie eine neue Sprache in der Dropdownliste **Wählen Sie eine neue Sprache aus** , und wählen Sie dann **Hinzufügen**. Wählen Sie beispielsweise Französisch und Finnisch, wie in Abbildung 3 dargestellt. Möglicherweise müssen Sie die gewünschte Sprache nach oben oder unten verschieben, indem Sie auf den Pfeil nach oben und nach unten weisenden Pfeil.
    
5. Wählen Sie **Speichern und schließen**.

**Hinweis**  Es kann für Ihre Website, um die ausgewählten Sprache(n) Rendern ein paar Minuten dauern.

**Wichtige**  Das CSOM ist mit neuen Features in regelmäßigen Abständen aktualisiert. Wenn das CSOM neue Features zum Aktualisieren der Websiteseite oder Schnellstartleiste Link Titel bereitstellt, wird empfohlen, dass Sie die neuen Features in der CSOM nicht die hier beschriebenen Optionen verwenden.

**Abbildung 1. Festlegen der Sprache für eine Website**

![Screenshot der Seite Spracheinstellungen der Websiteeinstellungen](media/0265dd57-cf25-4879-a6df-68072ffa5270.png)

**Abbildung 2. Navigieren zu Profilseite des Benutzers über mich auswählen**

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben](media/e3971203-7011-40ad-ab1b-341af2df28fc.png)

**Abbildung 3. Ändern eines Benutzers anzeigen Sprachoptionen auf der Profilseite des Benutzers**

![Screenshot der Seite Details bearbeiten im Abschnitt Sprache und Region](media/ff41b24e-42eb-48ca-83cd-00d88ef753bd.png)

Bevor Sie dieses Codebeispiel [Szenario 2](#bk_Scenario2) ausführen, führen Sie die folgenden Aufgaben aus.

### <a name="to-create-a-quick-launch-link"></a>Erstellen Sie eine Verknüpfung zur Schnellstartleiste

1. Wählen Sie auf der Hostwebsite **LINKS bearbeiten**.
    
2. Wählen Sie die **Verknüpfung**, wie in Abbildung 4 dargestellt.
    
3. Geben Sie in **den anzuzeigenden Text** **Meine Websitedesign Eintrag**aus.
    
4. Geben Sie im Feld **Adresse**die URL einer Website ein.
    
5. Wählen Sie **OK** > **Speichern**.

**Abbildung 4. Hinzufügen eines Links zur Schnellstartleiste**

![Screenshot der Seite Hyperlinks bearbeiten mit Link hervorgehoben](media/fcb28647-1576-4e86-8ca7-15f3ce8d85fb.png)

### <a name="to-create-a-site-page"></a>Erstellen Sie eine Websiteseite

1. Wählen Sie auf der Hostwebsite **Websiteinhalte** > **Websiteseiten** > **neue**.
    
2. Geben Sie in **Name der neuen Seite** **Hello SharePoint**aus.
    
3. Wählen Sie **Erstellen**.
    
4. Enter  **Test page** in the body of the page.
    
5. Wählen Sie **Speichern**aus.

## <a name="using-the-corejavascriptcustomization-sample-app"></a>Using the Core.JavaScriptCustomization sample app
<a name="sectionSection1"> </a>

Wenn Sie dieses Codebeispiel ausführen, wird eine vom Anbieter gehostete Anwendung angezeigt, wie in Abbildung 5 dargestellt. Dieser Artikel beschreibt Szenario 1 und 2 Szenario, da Sie die Techniken, die in Szenario 1 und 2 Szenario verwenden könnten, um lokalisierte Versionen der Websiteseite und Schnellstartleiste Link Titel bereitzustellen. 

**Abbildung 5. Startseite der app Core.JavaScriptCustomization**

![Screenshot, der zeigt der Startseite der app Core.JavaScriptCustomization](media/133a6c15-7b96-4418-b795-a7bdab63ead4.png)
### <a name="scenario-1"></a>Szenario 1

Szenario 1 zeigt, wie Sie einen Verweis auf eine JavaScript-Datei in einer SharePoint-Website mithilfe einer benutzerdefinierten Aktion hinzufügen. Auswahl der Schaltfläche **einlegen Anpassung** Ruft die **BtnSubmit_Click** -Methode im scenario1.aspx.cs. Die **BtnSubmit_Click** -Methode ruft **AddJsLink** um JavaScript-Dateien mit einer benutzerdefinierten Aktion auf dem hostweb Verweise hinzuzufügen.

Abbildung 6 zeigt die Startseite für Szenario 1.

**Abbildung 6. Szenario 1-Startseite**

![Screenshot der Startseite für Szenario 1](media/16972165-5f94-497f-b58c-0e1075d9616a.png)

Die **AddJSLink** -Methode ist Teil der Datei JavaScriptExtensions.cs in **OfficeDevPnP.Core**.  **AddJSLink** erfordert, dass eine Zeichenfolge zur Darstellung des Bezeichners der benutzerdefinierten Aktion zugewiesen bereit, und eine Zeichenfolge mit einer durch Semikolons getrennte Liste der URLs auf die JavaScript-Dateien, die Sie mit der Hostwebsite hinzufügen möchten. Beachten Sie, dass dieses Codebeispiel einen Verweis auf Scripts\scenario1.js, fügt die eine Meldung in der Statusleiste mit der Hostwebsite hinzufügt.
    
**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

```
protected void btnSubmit_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var cc = spContext.CreateUserClientContextForSPHost())
            {
                cc.Web.AddJsLink(Utilities.Scenario1Key, Utilities.BuildScenarioJavaScriptUrl(Utilities.Scenario1Key, this.Request));
            }
        }
```
   
**Hinweis**  SharePoint 2013 verwendet minimale Downloadstrategie, um die Datenmenge zu reduzieren Browser heruntergeladen wird, wenn Benutzer zwischen den Seiten auf einer SharePoint-Website navigieren. Weitere Informationen finden Sie unter [Übersicht über die minimale Downloadstrategie](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx). In scenario1.js stellt der folgende Code, und zwar unabhängig davon, ob minimale Downloadstrategie auf Ihrer SharePoint-Website verwendet wird, die **RemoteManager_Inject** -Methode immer aufgerufen wird, um den JavaScript-Code zum Hinzufügen von Meldung in der Statuszeile mit der Hostwebsite ausführen.

```
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible.
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS scenario
} else {
    RemoteManager_Inject();
}
```

**Hinweis**  Einige JavaScript-Dateien möglicherweise hängen von anderen JavaScript-Dateien geladen zuerst sein, bevor sie ausgeführt und erfolgreich abgeschlossen werden können. The following code construct from  **RemoteManager_Inject** uses the **loadScript** function in scenario1.js to first load jQuery, then continue running the remaining JavaScript code.

```
var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery first, then continue running the rest of the code.
    loadScript(jQuery, function () {
     // Add additional JavaScript code here to complete your task. 
});
```

Wählen Sie **zurück zur Website**. Wie in Abbildung 7 dargestellt, die Hostwebsite jetzt eine Meldung angezeigt, Status Leiste, die von scenario1.js hinzugefügt wurde.

**Abbildung 7. Meldung in der Statusleiste für eine Teamwebsite mithilfe von JavaScript hinzugefügt**

![Screenshot der Meldung in der Statuszeile mithilfe von JavaScript zu einer Teamwebsite hinzugefügt](media/c5d6fb6d-f05f-49aa-a3c5-af1240ee9135.png)

### <a name="scenario-2"></a>Szenario 2
<a name="bk_Scenario2"> </a>

Szenario 2 mithilfe das in Szenario 1 beschriebenen Verfahren Benutzeroberflächentext mit übersetzten Text aus einer Ressourcendatei JavaScript lesen ersetzt. Szenario 2 ersetzt die Schnellstartleiste Link Titel ( **Meine Websitedesign Eintrag**) und Website Seite Titel ( **Hello SharePoint**), die Sie zuvor erstellt haben. Szenario 2 Fügt eine JavaScript-Datei, welche Lesevorgänge Textwerte von Variablen in kulturspezifische JavaScript-Ressourcendateien übersetzt. Szenario 2 aktualisiert anschließend die Benutzeroberfläche. Abbildung 8 zeigt die Startseite für Szenario 2 an.

**Abbildung 8. Szenario 2-Startseite**

![Screenshot der Startseite für Szenario 2](media/c706060b-e77d-4ae6-99c4-43dee80ff7d3.png)

As shown in Figure 8, choosing  **Inject customization** applies the following changes to the site:

- The Quick Launch link title  **My quicklaunch entry** is changed to **Contoso link**.
    
- Den Titel der Seite **Hello SharePoint** -Website wird zur **Seite "Contoso"**geändert.

**Abbildung 9. Szenario 2 Anpassungen**

![Scenario 2 customizations](media/47e8ec40-d291-496f-8677-01eb46441df2.png)
    
**Hinweis**  Wenn Ihre Werte für die Schnellstartleiste Link Titel und Titel der Website Seite unterscheidet sich von in Abbildung 8 dargestellt die Variablen **quickLauch_Scenario2** und **PageTitle_HelloSharePoint** in Bearbeiten Dateien die JavaScript-Ressource scenario2.en us.js oder scenario2.nl-nl.js. Führen Sie das Codebeispiel erneut aus. The scenario2.en-us.js file stores English (US) culture-specific resources. Die Datei scenario2.nl nl.js speichert niederländische kulturspezifische Ressourcen. Wenn Sie dieses Codebeispiel mit einer anderen Sprache testen, sollten Sie eine andere Ressourcendatei für JavaScript in der gleichen Namenskonvention erstellen.

Szenario 1, Ähnlichkeit mit **BtnSubmit_Click** in scenario2.aspx.cs **AddJsLink** , um einen Verweis auf die Datei Scripts\scenario2.js hinzuzufügen. In scenario2.js, the **RemoteManager_Inject** function calls the **TranslateQuickLaunch** function, which performs the following tasks:

- **_SpPageContextInfo.currentUICultureName**mithilfe der Website Kultur bestimmt.
    
- Loads the JavaScript resource file containing culture specific resources that match the UI culture of the site. For example, if the site's culture was English (United States), the scenario2.en-us.js file is loaded.
    
- Replaces  **my quicklaunch entry** with the value of the **quickLauch_Scenario2** variable read from the JavaScript resource file.

```
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";
    
    loadScript(jQuery, function () {
        SP.SOD.executeOrDelayUntilScriptLoaded(function () { TranslateQuickLaunch(); }, 'sp.js');
    });
}

function TranslateQuickLaunch() {
    // Load jQuery and if complete, load the JS resource file.
    var scriptUrl = "";
    var scriptRevision = "";
    // iterate over the scripts loaded on the page to find the scenario2 script. Then use the script URL to dynamically build the URL for the resource file to be loaded.
    $('script').each(function (i, el) {
        if (el.src.toLowerCase().indexOf('scenario2.js') > -1) {
            scriptUrl = el.src;
            scriptRevision = scriptUrl.substring(scriptUrl.indexOf('.js') + 3);
            scriptUrl = scriptUrl.substring(0, scriptUrl.indexOf('.js'));
        }
    })

    var resourcesFile = scriptUrl + "." + _spPageContextInfo.currentUICultureName.toLowerCase() + ".js" + scriptRevision;
    // Load the JS resource file based on the user's language settings.
    loadScript(resourcesFile, function () {

        // General changes that apply to all loaded pages.
        // ----------------------------------------------

        // Update the Quick Launch labels.
        // Note that you can use the jQuery  function to iterate over all elements that match your jQuery selector.
        $("span.ms-navedit-flyoutArrow").each(function () {
            if (this.innerText.toLowerCase().indexOf('my quicklaunch entry') > -1) {
                // Update the label.
                $(this).find('.menu-item-text').text(quickLauch_Scenario2);
                // Update the tooltip.
                $(this).parent().attr("title", quickLauch_Scenario2);
            }
        });

        // Page specific changes require an IsOnPage call.
        // ----------------------------------------------------------

        // Change the title of the "Hello SharePoint" page.
        if (IsOnPage("Hello%20SharePoint.aspx")) {
            $("#DeltaPlaceHolderPageTitleInTitleArea").find("A").each(function () {
                if ($(this).text().toLowerCase().indexOf("hello sharepoint") > -1) {
                    // Update the label.
                    $(this).text(pageTitle_HelloSharePoint);
                    // Update the tooltip.
                    $(this).attr("title", pageTitle_HelloSharePoint);
                }
            });
        }

    });
}
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Localization solutions for SharePoint 2013 and SharePoint Online](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
