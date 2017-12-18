---
title: Erstellen von UX-Steuerelementen mithilfe von SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: a5ec35589ae00a6062be724a68910365102161c3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-ux-controls-by-using-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="71784-102">Erstellen von UX-Steuerelementen mithilfe von SharePoint gehostet durch Drittanbieter-add-ins</span><span class="sxs-lookup"><span data-stu-id="71784-102">Create UX controls by using SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="71784-103">UX-Steuerelemente in SharePoint gehostet durch Drittanbieter-add-ins, die arbeiten und Verhalten sich wie UX-Steuerelemente auf dem hostweb zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="71784-103">Create UX controls in SharePoint provider-hosted add-ins that work and behave like UX controls on the host web.</span></span> 

<span data-ttu-id="71784-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="71784-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="71784-105">Dieser Artikel beschreibt drei Beispiele, die zeigen, wie Sie UX-Steuerelemente in der vom Anbieter gehosteten-add-in zu implementieren:</span><span class="sxs-lookup"><span data-stu-id="71784-105">The article describes three samples that show you how to implement UX controls in your provider-hosted add-in:</span></span>

- <span data-ttu-id="71784-106">[Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - zeigt, wie eine personenauswahlsteuerung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="71784-106">[Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - Shows you how to add a people picker control.</span></span>
    
- <span data-ttu-id="71784-107">[Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - zeigt, wie ein Menüsteuerelement lokalisierbare Taxonomie zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="71784-107">[Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - Shows you how to implement a localizable taxonomy menu control.</span></span>
    
- <span data-ttu-id="71784-108">[Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - zeigt, wie eine Taxonomie Datumsauswahl-Steuerelement implementiert.</span><span class="sxs-lookup"><span data-stu-id="71784-108">[Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - Shows you how to implement a taxonomy picker control.</span></span>
    
<span data-ttu-id="71784-109">Diese Beispiele verwenden JavaScript und des JSOM zum Kommunizieren mit SharePoint und Verwenden der [domänenübergreifenden Bibliothek](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) , Funktionsaufrufe aus das Add-in auf die Hostdomäne Website behandeln.</span><span class="sxs-lookup"><span data-stu-id="71784-109">These samples use JavaScript and the JSOM to communicate with SharePoint and use the [cross-domain library](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) to handle function calls from the add-in to the host site domain.</span></span>

## <a name="people-picker-control"></a><span data-ttu-id="71784-110">Personenauswahlsteuerung</span><span class="sxs-lookup"><span data-stu-id="71784-110">People picker control</span></span>
<span data-ttu-id="71784-111"><a name="bmPeoplePicker"> </a></span><span class="sxs-lookup"><span data-stu-id="71784-111"></span></span>

<span data-ttu-id="71784-112">Das [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) -Beispiel zeigt, wie eine personenauswahlsteuerung in einer vom Anbieter gehosteten-add-in implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="71784-112">The [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) sample shows you how to implement a people picker control in a provider-hosted add-in.</span></span> <span data-ttu-id="71784-113">Wenn der Benutzer startet einen Namen im Textfeld input, die das Benutzerprofil speichern nach potenziellen Übereinstimmungen Steuerelement suchen eingeben und auf der Benutzeroberfläche angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="71784-113">When the user starts typing a name into the text input box, the control searches the user profile store for potential matches, and displays them in the UI.</span></span> <span data-ttu-id="71784-114">Das Add-in zeigt eine konfigurierbare und erweiterbare personenauswahlsteuerung, die auf einem remote-Host ausgeführt wird und fragt den Benutzerprofilspeicher auf der Hostwebsite Benutzereingaben übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="71784-114">The add-in displays a configurable and extensible people picker control that runs on a remote host and queries the user profile store on the host site to match user inputs.</span></span>

<span data-ttu-id="71784-115">**Abbildung 1. Personenauswahlsteuerung**</span><span class="sxs-lookup"><span data-stu-id="71784-115">**Figure 1. People picker control**</span></span>

![Personenauswahlsteuerung](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/ae6e2198-6f63-4ea1-a739-34f64ecd9117.png)
    
> [!NOTE] 
> <span data-ttu-id="71784-117">Die Visual Studio 2013-Lösung für das Beispiel enthält ein Modul mit dem Namen "Dummy", um sicherzustellen, dass das Add-in bereitgestellt wird, eine Web-Add-in erstellt.</span><span class="sxs-lookup"><span data-stu-id="71784-117">The Visual Studio 2013 solution for the sample contains a module named "Dummy" to ensure that when the add-in is deployed, it creates an add-in web.</span></span> <span data-ttu-id="71784-118">Eine Web-Add-in ist für domänenübergreifende Aufrufe erforderlich.</span><span class="sxs-lookup"><span data-stu-id="71784-118">An add-in web is required for cross-domain calls.</span></span>

<span data-ttu-id="71784-119">Der Skripts-Ordner des Projekts Core.PeoplePickerWeb enthält app.js und peoplepickercontrol.js-Dateien (zusammen mit Personen Personenauswahl Ressourcendateien für zusätzliche sprachunterstützung).</span><span class="sxs-lookup"><span data-stu-id="71784-119">The Scripts folder of the Core.PeoplePickerWeb project contains app.js and peoplepickercontrol.js files (along with people picker resource files for additional language support).</span></span> <span data-ttu-id="71784-120">Die Datei app.js holt Clientkontext mithilfe der domänenübergreifenden Bibliothek und den HTML-Code in der Datei Default.aspx in der personenauswahlsteuerung verknüpft.</span><span class="sxs-lookup"><span data-stu-id="71784-120">The app.js file fetches client context by using the cross-domain library and hooks the HTML in the Default.aspx file into the people picker control.</span></span> <span data-ttu-id="71784-121">Die Datei "default.aspx" enthält die `<div>` Tags, die das Textfeld und Personen implementieren Funktion suchen.</span><span class="sxs-lookup"><span data-stu-id="71784-121">The Default.aspx file contains the  `<div>` tags that implement both the text box and the people search capability.</span></span>

> [!NOTE] 
> <span data-ttu-id="71784-122">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="71784-122">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
<div id="divAdministrators" class="cam-peoplepicker-userlookup ms-fullWidth">
  <span id="spanAdministrators"></span>
<asp:TextBox ID="inputAdministrators" runat="server" CssClass="cam-peoplepicker-edit" Width="70"></asp:TextBox>
</div>
<div id="divAdministratorsSearch" class="cam-peoplepicker-usersearch ms-emphasisBorder"></div>
<asp:HiddenField ID="hdnAdministrators" runat="server" />

```

<span data-ttu-id="71784-123">Die Datei app.js wird dann erstellt und konfiguriert eine personenauswahlsteuerung.</span><span class="sxs-lookup"><span data-stu-id="71784-123">The app.js file then creates and configures a people picker control.</span></span>

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

<span data-ttu-id="71784-124">Die personenauswahlsteuerung fragt das **ClientPeoplePickerWebServiceInterface** -Objekt in der JSOM-Bibliothek, sucht nach Benutzern zu initiieren, deren Namen die eingegebenen Zeichenfolgen übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="71784-124">The people picker control queries the  **ClientPeoplePickerWebServiceInterface** object in the JSOM library to initiate searches for users whose names match the character strings entered.</span></span>

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

## <a name="taxonomy-menu-control"></a><span data-ttu-id="71784-125">Taxonomie Menu-Steuerelement</span><span class="sxs-lookup"><span data-stu-id="71784-125">Taxonomy menu control</span></span>
<span data-ttu-id="71784-126"><a name="bmTaxMenu"> </a></span><span class="sxs-lookup"><span data-stu-id="71784-126"></span></span>

<span data-ttu-id="71784-127">Das [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) -Beispiel zeigt, wie ein Menüsteuerelement lokalisierbare Taxonomie zu implementieren, die aus dem Terminologiespeicher in einer vom Anbieter gehosteten-add-in aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="71784-127">The [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) sample shows you how to implement a localizable taxonomy menu control that is populated from the term store in a provider-hosted add-in.</span></span> <span data-ttu-id="71784-128">Das Add-in auch richtet die erforderlichen Begriff Store Sprachen, Gruppen, Sätze und Begriffe im Menü aufgefüllt, und überprüft die bevorzugte Sprache des Benutzers aktivieren, um die Anzeigesprache festgelegt.</span><span class="sxs-lookup"><span data-stu-id="71784-128">The add-in also sets up the required term store languages, groups, sets, and terms for populating the menu, and checks the user's language preference to set the display language.</span></span>

<span data-ttu-id="71784-129">Das Add-in implementiert eine **TaxonomyHelper** -Klasse (CSOM), die den Terminologiespeicher richtet und füllt mit Ausdrücken.</span><span class="sxs-lookup"><span data-stu-id="71784-129">The add-in implements a  **TaxonomyHelper** class (CSOM) that sets up the term store and populates it with terms.</span></span> <span data-ttu-id="71784-130">Es dient zum Hochladen klicken Sie dann in den Stammordner der Website einer JavaScript-Datei, die die Navigationslinks anzeigt.</span><span class="sxs-lookup"><span data-stu-id="71784-130">It then uploads into the site's root folder a JavaScript file that displays the navigational links.</span></span>

<span data-ttu-id="71784-131">Richtet das Add-in auf der Hostwebsite Terminologiespeicher aus.</span><span class="sxs-lookup"><span data-stu-id="71784-131">The add-in sets up the term store on the host site.</span></span> <span data-ttu-id="71784-132">Es wird verwendet, CSOM-Objekte und Methoden zum Erstellen einer Begriffsgruppe und Set und füllt dann den Ausdruckssatz mit vier Begriffe.</span><span class="sxs-lookup"><span data-stu-id="71784-132">It uses CSOM objects and methods to create a term group and set, and then populates the term set with four terms.</span></span> 

<span data-ttu-id="71784-133">**Abbildung 2. Begriff Store Setupbildschirm**</span><span class="sxs-lookup"><span data-stu-id="71784-133">**Figure 2. Term store setup screen**</span></span>

![Begriff Store Setupbildschirm](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/011ba839-7bc3-4a12-819a-6436deab2e34.png)

<span data-ttu-id="71784-135">Bei der Auswahl der Schaltfläche **Terminologiespeicher Setup** das Add-in:</span><span class="sxs-lookup"><span data-stu-id="71784-135">When you choose the  **Setup term store** button, the add-in:</span></span>

- <span data-ttu-id="71784-136">Stellt sicher, dass die erforderlichen Sprachen (Englisch, Deutsch, Französisch und Schwedisch) im Terminologiespeicher aktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="71784-136">Makes sure that the required languages (English, German, French, and Swedish) are enabled in the term store.</span></span>
    
- <span data-ttu-id="71784-137">Erstellt eine Begriffsgruppe und Set Ausdruckssätze und füllt den Ausdruckssatz mit vier neue Ausdrücke.</span><span class="sxs-lookup"><span data-stu-id="71784-137">Creates a term group and term set and populates the term set with four new terms.</span></span>
    
<span data-ttu-id="71784-138">In der **TaxonomyHelper** -Klasse der folgende Code wird überprüft, dass die erforderlichen Sprachen aktiviert sind, und wenn sie nicht vertraut sind, können sie.</span><span class="sxs-lookup"><span data-stu-id="71784-138">The following code in the  **TaxonomyHelper** class verifies that the required languages are enabled, and if they're not, it enables them.</span></span>

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

<span data-ttu-id="71784-139">Der folgende Code in der gleichen **TaxonomyHelper** -Klasse erstellt dann jeder neuen Begriff, zusammen mit Bezeichnungen für die Sprachen Deutsch, Französisch und Schwedisch.</span><span class="sxs-lookup"><span data-stu-id="71784-139">Finally, the following code in the same  **TaxonomyHelper** class creates each new term, along with labels for the German, French, and Swedish languages.</span></span> <span data-ttu-id="71784-140">Es wird auch einen Wert für die **_Sys_Nav_SimpleLinkUrl** -Eigenschaft der **einfachen Link oder Header** -Eigenschaft in den Terminologiespeicher-Verwaltungstool entspricht.</span><span class="sxs-lookup"><span data-stu-id="71784-140">It also sets a value for the **_Sys_Nav_SimpleLinkUrl** property, which is equivalent to the **Simple Link or Header** property in the Term Store Management Tool.</span></span> <span data-ttu-id="71784-141">In diesem Fall zeigt die URL für jeden Ausdruck auf die Stammwebsite.</span><span class="sxs-lookup"><span data-stu-id="71784-141">In this case, the URL for each term points back to the root site.</span></span>

```
var term = termSet.CreateTerm(termName, 1033, Guid.NewGuid());
term.CreateLabel(termNameGerman, 1031, false);
term.CreateLabel(termNameFrench, 1036, false);
term.CreateLabel(termNameSwedish, 1053, false);
term.SetLocalCustomProperty("_Sys_Nav_SimpleLinkUrl", clientContext.Web.ServerRelativeUrl);
```

<span data-ttu-id="71784-142">Im nächsten Schritt fügt das Add-in die Datei topnav.js in den Stammordner der Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="71784-142">Next, the add-in inserts the topnav.js file into the root folder of the host site.</span></span> <span data-ttu-id="71784-143">Diese Datei enthält den JavaScript-Code, der die Links aus dieser Ausdruckssatz in der Navigation der Homepage der Hostwebsite einfügt.</span><span class="sxs-lookup"><span data-stu-id="71784-143">This file contains the JavaScript that inserts the links from this term set into the navigation of the host site's home page.</span></span> <span data-ttu-id="71784-144">Die Add-in-Benutzeroberfläche zeigt auch, wie die Navigationslinks auf der Hostwebsite angezeigt werden, nachdem das Add-in der JavaScript-Datei hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="71784-144">The add-in UI also shows you how the navigational links will appear on the host site after the add-in uploads the JavaScript file.</span></span>

<span data-ttu-id="71784-145">Der folgende Code in der Datei topnav.js verwendet JSOM auf bevorzugte Sprache des Benutzers überprüft.</span><span class="sxs-lookup"><span data-stu-id="71784-145">The following code in the topnav.js file uses JSOM to check for the user's preferred language.</span></span>

```
var targetUser = "i:0#.f|membership|" + _spPageContextInfo.userLoginName;
        context = new SP.ClientContext.get_current();
var peopleManager = new SP.UserProfiles.PeopleManager(context);
var userProperty = peopleManager.getUserProfilePropertyFor(targetUser, "SPS-MUILanguages");
```

<span data-ttu-id="71784-146">Das Add-in bestimmt, ob der Benutzer bevorzugte Sprache auswählen eine der aktivierten Sprachen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="71784-146">The add-in then determines whether the user's language preference matches one of the enabled languages.</span></span> <span data-ttu-id="71784-147">Wenn eine Übereinstimmung gefunden wird, ruft der folgende Code die Begriffe und die zugehörigen Beschriftungen für die bevorzugte Sprache des Benutzers ab.</span><span class="sxs-lookup"><span data-stu-id="71784-147">If it finds a match, the following code gets the terms and the associated labels for the user's preferred language.</span></span>

```
while (termEnumerator.moveNext()) {
    var currentTerm = termEnumerator.get_current();
    var label = currentTerm.getDefaultLabel(lcid);

    termItems.push(currentTerm);
    termLabels.push(label);
    context.load(currentTerm);
```

<span data-ttu-id="71784-148">Schließlich fügt der folgende Code in der Datei topnav.js Links, die die Begriffe in der oberen Navigation-Element der Hostwebsite enthalten.</span><span class="sxs-lookup"><span data-stu-id="71784-148">Finally, the following code in the topnav.js file inserts links that contain the terms into the top navigational element of the host site.</span></span>

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

## <a name="taxonomy-picker-control"></a><span data-ttu-id="71784-149">Taxonomie Datumsauswahl-Steuerelement</span><span class="sxs-lookup"><span data-stu-id="71784-149">Taxonomy picker control</span></span>
<span data-ttu-id="71784-150"><a name="bmTaxPicker"> </a></span><span class="sxs-lookup"><span data-stu-id="71784-150"></span></span>

<span data-ttu-id="71784-151">Das [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) -Beispiel zeigt, wie eine Taxonomie Datumsauswahl-Steuerelement in einer vom Anbieter gehosteten-add-in implementiert.</span><span class="sxs-lookup"><span data-stu-id="71784-151">The [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) sample shows you how to implement a taxonomy picker control in a provider-hosted add-in.</span></span> <span data-ttu-id="71784-152">Wenn der Benutzer startet einen Ausdruckssatz Eingabe im Textfeld, sucht der Steuerung Terminologiespeicher für Potenzial ermittelt und zeigt diese in einer Liste unter Eingabefeld eingeben.</span><span class="sxs-lookup"><span data-stu-id="71784-152">When the user starts typing a term into the text input box, the control searches the term store for potential matches and displays them in a list under the input box.</span></span>

<span data-ttu-id="71784-153">Die Add-in erstellt eine HTML-Seite, die die JSOM Taxonomie Personenauswahl-Anforderungen entspricht und hinzugefügt und konfiguriert das Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="71784-153">The add-in creates an HTML page that conforms to the JSOM taxonomy picker requirements, and then adds and configures the control.</span></span> <span data-ttu-id="71784-154">Es verwendet die JSOM-Bibliothek zum Abfragen der Hostwebsite Terminologiespeicher.</span><span class="sxs-lookup"><span data-stu-id="71784-154">It uses the JSOM library to query the host site's term store.</span></span> <span data-ttu-id="71784-155">Die Taxonomie Personenauswahl kommuniziert mit der verwalteten Metadatendiensts von SharePoint, die Schreibberechtigung auf Standortebene Berechtigung Taxonomie erforderlich sind, damit es von geschlossenen Ausdruckssätze lesen und Schreiben von Ausdruckssätzen öffnen kann.</span><span class="sxs-lookup"><span data-stu-id="71784-155">The taxonomy picker communicates with the SharePoint Managed Metadata Service, which requires write permission at the taxonomy permission scope so that it can read from closed term sets and write to open term sets.</span></span> <span data-ttu-id="71784-156">Stellen Sie sicher, dass die Datei AppManifest.xml die Schreibberechtigung auf den entsprechenden Bereich festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="71784-156">Make sure that the AppManifest.xml file has set the write permission at the appropriate scope.</span></span>

<span data-ttu-id="71784-157">Der Skripts-Ordner des Projekts [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) enthält app.js und taxonomypickercontrol.js-Dateien (zusammen mit einer Taxonomie Personenauswahl-Ressourcendatei für zusätzliche sprachunterstützung).</span><span class="sxs-lookup"><span data-stu-id="71784-157">The Scripts folder of the [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) project contains app.js and taxonomypickercontrol.js files (along with a taxonomy picker resource file for additional language support).</span></span> <span data-ttu-id="71784-158">Die Datei app.js holt Clientkontext mithilfe der domänenübergreifenden Bibliothek und den HTML-Code in der Datei Default.aspx in der Taxonomie Datumsauswahl-Steuerelement verknüpft.</span><span class="sxs-lookup"><span data-stu-id="71784-158">The app.js file fetches client context by using the cross-domain library and hooks the HTML in the Default.aspx file into the taxonomy picker control.</span></span> <span data-ttu-id="71784-159">Die Datei "default.aspx" enthält, die das Textfeld und die Taxonomie Personenauswahl-Funktion implementiert ausgeblendeten Felds.</span><span class="sxs-lookup"><span data-stu-id="71784-159">The Default.aspx file contains the hidden field that implements both the text box and the taxonomy picker capability.</span></span> <span data-ttu-id="71784-160">Außerdem wird eine Liste mit Aufzählungszeichen zurückgegeben, die aus dem Terminologiespeicher Vorschläge anzeigen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="71784-160">It also adds a bulleted list to display suggestions returned from the term store.</span></span>

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

<span data-ttu-id="71784-161">Die Datei app.js wird dann erstellt und konfiguriert eine Taxonomie Datumsauswahl-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="71784-161">The app.js file then creates and configures a taxonomy picker control.</span></span>

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

<span data-ttu-id="71784-162">Das Taxonomie Datumsauswahl-Steuerelement verwendet den folgenden Code eine **TaxonomySession** -Instanz in der JSOM alle Elemente aus dem Terminologiespeicher laden geöffnet.</span><span class="sxs-lookup"><span data-stu-id="71784-162">The taxonomy picker control uses the following code to open a  **TaxonomySession** instance in the JSOM to load all the terms from the term store.</span></span>

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

<span data-ttu-id="71784-163">Das Taxonomie Datumsauswahl-Steuerelement sucht nach potenziellen Übereinstimmungen geladen Ausdrücken und fügt neue Ausdrücke auf den Terminologiespeicher wie nötig.</span><span class="sxs-lookup"><span data-stu-id="71784-163">The taxonomy picker control then looks for potential matches from the loaded terms, and adds new terms to the term store as needed.</span></span>

## <a name="see-also"></a><span data-ttu-id="71784-164">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="71784-164">See also</span></span>
<span data-ttu-id="71784-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="71784-165"></span></span>

- [<span data-ttu-id="71784-166">UX-Komponenten in SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="71784-166">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="71784-167">Zugreifen auf SharePoint 2013-Daten von add-ins mithilfe der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="71784-167">Access SharePoint 2013 data from add-ins using the cross-domain library</span></span>](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx)
