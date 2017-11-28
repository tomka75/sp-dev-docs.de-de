---
title: Erstellen von UX-Steuerelementen mithilfe von SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 568c01ab1d335e45b95c57ddb92ab0d1023fb238
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="create-ux-controls-by-using-sharepoint-provider-hosted-add-ins"></a>Erstellen von UX-Steuerelementen mithilfe von SharePoint gehostet durch Drittanbieter-add-ins

UX-Steuerelemente in SharePoint gehostet durch Drittanbieter-add-ins, die arbeiten und Verhalten sich wie UX-Steuerelemente auf dem hostweb zu erstellen. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Dieser Artikel beschreibt drei Beispiele, die zeigen, wie Sie UX-Steuerelemente in der vom Anbieter gehosteten-add-in zu implementieren:

- [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - zeigt, wie eine personenauswahlsteuerung hinzufügen.
    
- [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - zeigt, wie ein Menüsteuerelement lokalisierbare Taxonomie zu implementieren.
    
- [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - zeigt, wie eine Taxonomie Datumsauswahl-Steuerelement implementiert.
    
Diese Beispiele verwenden JavaScript und des JSOM zum Kommunizieren mit SharePoint und Verwenden der [domänenübergreifenden Bibliothek](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) , Funktionsaufrufe aus das Add-in auf die Hostdomäne Website behandeln.

## <a name="people-picker-control"></a>Personenauswahlsteuerung
<a name="bmPeoplePicker"> </a>

Das [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) -Beispiel zeigt, wie eine personenauswahlsteuerung in einer vom Anbieter gehosteten-add-in implementiert wird. Wenn der Benutzer startet einen Namen im Textfeld input, die das Benutzerprofil speichern nach potenziellen Übereinstimmungen Steuerelement suchen eingeben und auf der Benutzeroberfläche angezeigt werden. Das Add-in zeigt eine konfigurierbare und erweiterbare personenauswahlsteuerung, die auf einem remote-Host ausgeführt wird und fragt den Benutzerprofilspeicher auf der Hostwebsite Benutzereingaben übereinstimmen.

**Abbildung 1. Personenauswahlsteuerung**

![Personenauswahlsteuerung](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/ae6e2198-6f63-4ea1-a739-34f64ecd9117.png)
    
**Hinweis:**  Die Visual Studio 2013-Lösung für das Beispiel enthält ein Modul mit dem Namen "Dummy", um sicherzustellen, dass das Add-in bereitgestellt wird, eine Web-Add-in erstellt. Eine Web-Add-in ist für domänenübergreifende Aufrufe erforderlich.

Der Skripts-Ordner des Projekts Core.PeoplePickerWeb enthält app.js und peoplepickercontrol.js-Dateien (zusammen mit Personen Personenauswahl Ressourcendateien für zusätzliche sprachunterstützung). Die Datei app.js holt Clientkontext mithilfe der domänenübergreifenden Bibliothek und den HTML-Code in der Datei Default.aspx in der personenauswahlsteuerung verknüpft. Die Datei "default.aspx" enthält die `<div>` Tags, die das Textfeld und Personen implementieren Funktion suchen.

**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```
<div id="divAdministrators" class="cam-peoplepicker-userlookup ms-fullWidth">
  <span id="spanAdministrators"></span>
<asp:TextBox ID="inputAdministrators" runat="server" CssClass="cam-peoplepicker-edit" Width="70"></asp:TextBox>
</div>
<div id="divAdministratorsSearch" class="cam-peoplepicker-usersearch ms-emphasisBorder"></div>
<asp:HiddenField ID="hdnAdministrators" runat="server" />

```

Die Datei app.js wird dann erstellt und konfiguriert eine personenauswahlsteuerung.

```
//Make a people picker control.
//1. context = SharePoint Client Context object
//2. $('#spanAdministrators') = SPAN that will 'host' the people picker control
//3. $('#inputAdministrators') = INPUT that will be used to capture user input
//4. $('#divAdministratorsSearch') = DIV that will show the 'drop-down' of the picker
//5. $('#hdnAdministrators') = INPUT hidden control that will host a resolved users
peoplePicker = new CAMControl.PeoplePicker(context, $('#spanAdministrators'), $('#inputAdministrators'), $('#divAdministratorsSearch'), $('#hdnAdministrators'));
// required to pass the variable name here!
peoplePicker.InstanceName = "peoplePicker";
// Hookup everything.
peoplePicker.Initialize();

```

Die personenauswahlsteuerung fragt das **ClientPeoplePickerWebServiceInterface** -Objekt in der JSOM-Bibliothek, sucht nach Benutzern zu initiieren, deren Namen die eingegebenen Zeichenfolgen übereinstimmen.

```
if (searchText.length >= parent.GetMinimalCharactersBeforeSearching()) {
                            resultDisplay = 'Searching...';
                            if (typeof resultsSearching != 'undefined') {
                                resultDisplay = resultsSearching;
                            }

                  var searchbusy = parent.Format('<div class=\'ms-emphasisBorder\' style=\'width: 400px; padding: 4px; border-left: none; border-bottom: none; border-right: none; cursor: default;\'>{0}</div>', resultDisplay);
                            parent.PeoplePickerDisplay.html(searchbusy);
                            // Display the suggestion box.
                            parent.ShowSelectionBox();

                   var query = new SP.UI.ApplicationPages.ClientPeoplePickerQueryParameters();
                            query.set_allowMultipleEntities(false);
                            query.set_maximumEntitySuggestions(2000);
                            query.set_principalType(parent.GetPrincipalType());
                            query.set_principalSource(15);
                            query.set_queryString(searchText);
                            var searchResult = SP.UI.ApplicationPages.ClientPeoplePickerWebServiceInterface.clientPeoplePickerSearchUser(parent.SharePointContext, query);

                  // Update the global queryID variable so that you can correlate incoming delegate calls.
                            parent._queryID = parent._queryID + 1;
                            var queryIDToPass = parent._queryID;
                            parent._lastQueryID = queryIDToPass;

                  // Make the SharePoint request.
                            parent.SharePointContext.executeQueryAsync(Function.createDelegate(this, function () { parent.QuerySuccess(queryIDToPass, searchResult); }),
                                                Function.createDelegate(this, function () { parent.QueryFailure(queryIDToPass); }));

```

## <a name="taxonomy-menu-control"></a>Taxonomie Menu-Steuerelement
<a name="bmTaxMenu"> </a>

Das [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) -Beispiel zeigt, wie ein Menüsteuerelement lokalisierbare Taxonomie zu implementieren, die aus dem Terminologiespeicher in einer vom Anbieter gehosteten-add-in aufgefüllt wird. Das Add-in auch richtet die erforderlichen Begriff Store Sprachen, Gruppen, Sätze und Begriffe im Menü aufgefüllt, und überprüft die bevorzugte Sprache des Benutzers aktivieren, um die Anzeigesprache festgelegt.

Das Add-in implementiert eine **TaxonomyHelper** -Klasse (CSOM), die den Terminologiespeicher richtet und füllt mit Ausdrücken. Es dient zum Hochladen klicken Sie dann in den Stammordner der Website einer JavaScript-Datei, die die Navigationslinks anzeigt.

Richtet das Add-in auf der Hostwebsite Terminologiespeicher aus. Es wird verwendet, CSOM-Objekte und Methoden zum Erstellen einer Begriffsgruppe und Set und füllt dann den Ausdruckssatz mit vier Begriffe. 

**Abbildung 2. Begriff Store Setupbildschirm**

![Begriff Store Setupbildschirm](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/011ba839-7bc3-4a12-819a-6436deab2e34.png)

Bei der Auswahl der Schaltfläche **Terminologiespeicher Setup** das Add-in:

- Stellt sicher, dass die erforderlichen Sprachen (Englisch, Deutsch, Französisch und Schwedisch) im Terminologiespeicher aktiviert sind.
    
- Erstellt eine Begriffsgruppe und Set Ausdruckssätze und füllt den Ausdruckssatz mit vier neue Ausdrücke.
    
In der **TaxonomyHelper** -Klasse der folgende Code wird überprüft, dass die erforderlichen Sprachen aktiviert sind, und wenn sie nicht vertraut sind, können sie.

```
var languages = new int[] { 1031, 1033, 1036, 1053 };
            Array.ForEach(languages, l => { 
                if (!termStore.Languages.Contains(l)) 
                    termStore.AddLanguage(l); 
            });

            termStore.CommitAll();
            clientContext.ExecuteQuery();

// Create the term group.
termGroup = termStore.CreateGroup("Taxonomy Navigation", groupId);
                clientContext.Load(termGroup);
                clientContext.ExecuteQuery();
```

Der folgende Code in der gleichen **TaxonomyHelper** -Klasse erstellt dann jeder neuen Begriff, zusammen mit Bezeichnungen für die Sprachen Deutsch, Französisch und Schwedisch. Es wird auch einen Wert für die **_Sys_Nav_SimpleLinkUrl** -Eigenschaft der **einfachen Link oder Header** -Eigenschaft in den Terminologiespeicher-Verwaltungstool entspricht. In diesem Fall zeigt die URL für jeden Ausdruck auf die Stammwebsite.

```
var term = termSet.CreateTerm(termName, 1033, Guid.NewGuid());
term.CreateLabel(termNameGerman, 1031, false);
term.CreateLabel(termNameFrench, 1036, false);
term.CreateLabel(termNameSwedish, 1053, false);
term.SetLocalCustomProperty("_Sys_Nav_SimpleLinkUrl", clientContext.Web.ServerRelativeUrl);
```

Im nächsten Schritt fügt das Add-in die Datei topnav.js in den Stammordner der Hostwebsite. Diese Datei enthält den JavaScript-Code, der die Links aus dieser Ausdruckssatz in der Navigation der Homepage der Hostwebsite einfügt. Die Add-in-Benutzeroberfläche zeigt auch, wie die Navigationslinks auf der Hostwebsite angezeigt werden, nachdem das Add-in der JavaScript-Datei hochgeladen.

Der folgende Code in der Datei topnav.js verwendet JSOM auf bevorzugte Sprache des Benutzers überprüft.

```
var targetUser = "i:0#.f|membership|" + _spPageContextInfo.userLoginName;
        context = new SP.ClientContext.get_current();
var peopleManager = new SP.UserProfiles.PeopleManager(context);
var userProperty = peopleManager.getUserProfilePropertyFor(targetUser, "SPS-MUILanguages");
```

Das Add-in bestimmt, ob der Benutzer bevorzugte Sprache auswählen eine der aktivierten Sprachen übereinstimmt. Wenn eine Übereinstimmung gefunden wird, ruft der folgende Code die Begriffe und die zugehörigen Beschriftungen für die bevorzugte Sprache des Benutzers ab.

```
while (termEnumerator.moveNext()) {
    var currentTerm = termEnumerator.get_current();
    var label = currentTerm.getDefaultLabel(lcid);

    termItems.push(currentTerm);
    termLabels.push(label);
    context.load(currentTerm);
```

Schließlich fügt der folgende Code in der Datei topnav.js Links, die die Begriffe in der oberen Navigation-Element der Hostwebsite enthalten.

```
html += "<ul style='margin-top: 0px; margin-bottom: 0px;'>"
        for (var i in termItems) {
            var term = termItems[i];
            var termLabel = termLabels[i];
            var linkName = termLabel.get_value() != 0 ? termLabel.get_value() : term.get_name();
            var linkUrl = term.get_localCustomProperties()['_Sys_Nav_SimpleLinkUrl'];

            html += "<li style='display: inline;list-style-type: none; padding-right: 20px;'><a href='" + linkUrl + "'>" + linkName + "</a></li>";
        }
        html += "</ul>";

        $('#DeltaTopNavigation').html(html);
        SP.UI.Notify.removeNotification(nid);
```

## <a name="taxonomy-picker-control"></a>Taxonomie Datumsauswahl-Steuerelement
<a name="bmTaxPicker"> </a>

Das [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) -Beispiel zeigt, wie eine Taxonomie Datumsauswahl-Steuerelement in einer vom Anbieter gehosteten-add-in implementiert. Wenn der Benutzer startet einen Ausdruckssatz Eingabe im Textfeld, sucht der Steuerung Terminologiespeicher für Potenzial ermittelt und zeigt diese in einer Liste unter Eingabefeld eingeben.

Die Add-in erstellt eine HTML-Seite, die die JSOM Taxonomie Personenauswahl-Anforderungen entspricht und hinzugefügt und konfiguriert das Steuerelement. Es verwendet die JSOM-Bibliothek zum Abfragen der Hostwebsite Terminologiespeicher. Die Taxonomie Personenauswahl kommuniziert mit der verwalteten Metadatendiensts von SharePoint, die Schreibberechtigung auf Standortebene Berechtigung Taxonomie erforderlich sind, damit es von geschlossenen Ausdruckssätze lesen und Schreiben von Ausdruckssätzen öffnen kann. Stellen Sie sicher, dass die Datei AppManifest.xml die Schreibberechtigung auf den entsprechenden Bereich festgelegt wurde.

Der Skripts-Ordner des Projekts [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) enthält app.js und taxonomypickercontrol.js-Dateien (zusammen mit einer Taxonomie Personenauswahl-Ressourcendatei für zusätzliche sprachunterstützung). Die Datei app.js holt Clientkontext mithilfe der domänenübergreifenden Bibliothek und den HTML-Code in der Datei Default.aspx in der Taxonomie Datumsauswahl-Steuerelement verknüpft. Die Datei "default.aspx" enthält, die das Textfeld und die Taxonomie Personenauswahl-Funktion implementiert ausgeblendeten Felds. Außerdem wird eine Liste mit Aufzählungszeichen zurückgegeben, die aus dem Terminologiespeicher Vorschläge anzeigen hinzugefügt.

```
<div style="left: 50%; width: 600px; margin-left: -300px; position: absolute;">
            <table>
                <tr>
                    <td class="ms-formlabel" valign="top"><h3 class="ms-standardheader">Keywords Termset:</h3></td>
                    <td class="ms-formbody" valign="top">
                        <div class="ms-core-form-line" style="margin-bottom: 0px;">
                            <asp:HiddenField runat="server" id="taxPickerKeywords" />
                        </div>
                    </td>
                </tr>
            </table>

            <asp:Button runat="server" OnClick="SubmitButton_Click" Text="Submit" />

            <asp:BulletedList runat="server" ID="SelectedValues" DataTextField="Label" />
</div>
```

Die Datei app.js wird dann erstellt und konfiguriert eine Taxonomie Datumsauswahl-Steuerelement.

```
// Load scripts for calling taxonomy APIs.
                    $.getScript(layoutsRoot + 'init.js',
                        function () {
                            $.getScript(layoutsRoot + 'sp.taxonomy.js',
                                function () {
                                    // Bind the taxonomy picker to the default keywords term set.
                                    $('#taxPickerKeywords').taxpicker({ isMulti: true, allowFillIn: true, useKeywords: true }, context);
                                });
                        });

```

Das Taxonomie Datumsauswahl-Steuerelement verwendet den folgenden Code eine **TaxonomySession** -Instanz in der JSOM alle Elemente aus dem Terminologiespeicher laden geöffnet.

```
// Get the taxonomy session by using CSOM.
            var taxSession = SP.Taxonomy.TaxonomySession.getTaxonomySession(spContext);
            //Use the default term store...this could be extended here to support additional term stores.
            var termStore = taxSession.getDefaultSiteCollectionTermStore();

            // Get the term set based on the properties of the term set.
            if (this.Id != null)
                this.RawTermSet = termStore.getTermSet(this.Id); // Get term set by ID.
            else if (this.UseHashtags)
                this.RawTermSet = termStore.get_hashTagsTermSet(); // Get the hashtags term set.
            else if (this.UseKeywords)
                this.RawTermSet = termStore.get_keywordsTermSet(); // Get the keywords term set.

            // Get all terms for the term set and organize them in the async callback.
            this.RawTerms = this.RawTermSet.getAllTerms();
            spContext.load(this.RawTermSet);
            spContext.load(this.RawTerms);
            spContext.executeQueryAsync(Function.createDelegate(this, this.termsLoadedSuccess), Function.createDelegate(this, this.termsLoadedFailed));

```

Das Taxonomie Datumsauswahl-Steuerelement sucht nach potenziellen Übereinstimmungen geladen Ausdrücken und fügt neue Ausdrücke auf den Terminologiespeicher wie nötig.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [UX-Komponenten in SharePoint 2013 und SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Zugreifen auf SharePoint 2013-Daten von add-ins mithilfe der domänenübergreifenden Bibliothek](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx)
