---
title: Verwenden des clientseitigen Personenauswahl-Steuerelement in von SharePoint gehosteten SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ab5c3d1cb7c47518a4806af2fc075f1730e53399
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="7bafd-102">Verwenden des clientseitigen Personenauswahl-Steuerelement in von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="7bafd-102">Use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins</span></span>
<span data-ttu-id="7bafd-103">Erfahren Sie, wie das clientseitige Personenauswahl-Steuerelement in von SharePoint gehosteten SharePoint-Add-Ins verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7bafd-103">Learn how to use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="7bafd-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="7bafd-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="7bafd-p102">**Wichtig** In diesem Thema wird davon ausgegangen, dass Sie wissen, wie ein von SharePoint gehostetes SharePoint-Add-In erstellt wird. Wenn Sie mehr über das Erstellen erfahren möchten, beginnen Sie mit [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="7bafd-p102">**Important**  This topic assumes that you know how to create a SharePoint-hosted SharePoint Add-in. To learn how to create one, start at  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
 


## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a><span data-ttu-id="7bafd-109">Was ist das clientseitige Personenauswahl-Steuerelement in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="7bafd-109">What is the client-side People Picker control in SharePoint?</span></span>
<span data-ttu-id="7bafd-110"><a name="bk_whatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="7bafd-110"></span></span>

<span data-ttu-id="7bafd-p103">Mit dem clientseitigen Personenauswahl-Steuerelement können Benutzer schnell nach gültigen Benutzerkonten von Personen, Gruppen und Ansprüchen in ihrer Organisation suchen und diese auswählen. Bei der Auswahl handelt es sich um ein HTML- und JavaScript-Steuerelement mit browserübergreifender Unterstützung. Das Hinzufügen der Auswahl zu Ihrem Add-In ist einfach: Fügen Sie in Ihrem Markup ein Containerelement für das Steuerelement sowie Verweise auf das Steuerelement und seine Abhängigkeiten hinzu. Rufen Sie dann in Ihrem Skript die globale Funktion **SPClientPeoplePicker_InitStandaloneControlWrapper** auf, um die Auswahl zu rendern und zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p103">The client-side People Picker control lets users quickly search for and select valid user accounts for people, groups, and claims in their organization. The picker is an HTML and JavaScript control that provides cross-browser support. Adding the picker to your add-in is easy: In your markup, add a container element for the control and references for the control and its dependencies. Then in your script, call the  **SPClientPeoplePicker_InitStandaloneControlWrapper** global function to render and initialize the picker.</span></span>
 

 
<span data-ttu-id="7bafd-p104">Die Auswahl wird durch das **SPClientPeoplePicker**-Objekt dargestellt, das Methoden bereitstellt, mit dem andere clientseitige Steuerelemente Informationen von der Auswahl abrufen oder andere Vorgänge durchführen können. Sie können **SPClientPeoplePicker**-Eigenschaften verwenden, um die Auswahl mit steuerelementspezifischen Einstellungen zu konfigurieren, z. B. um mehrere Benutzer zuzulassen oder Zwischenspeicheroptionen festzulegen. Die Auswahl verwendet auch Konfigurationseinstellungen für Webanwendungen wie z. B. Active Directory-Domänendienste-Parameter oder Zielgesamtstrukturen. Konfigurationseinstellungen für Webanwendungen werden automatisch ausgewählt (von der **SPWebApplication.PeoplePickerSettings**-Eigenschaft).</span><span class="sxs-lookup"><span data-stu-id="7bafd-p104">The picker is represented by the  **SPClientPeoplePicker** object, which provides methods that other client-side controls can use to get information from the picker or to perform other operations. You can use **SPClientPeoplePicker** properties to configure the picker with control-specific settings, such as allowing multiple users or specifying caching options. The picker also uses web application configuration settings such as Active Directory Domain Services parameters or targeted forests. Web application configuration settings are picked up automatically (from the **SPWebApplication.PeoplePickerSettings** property).</span></span>
 

 
<span data-ttu-id="7bafd-119">Die Auswahl besteht aus den folgenden Komponenten:</span><span class="sxs-lookup"><span data-stu-id="7bafd-119">The picker has the following components:</span></span>
 

 

- <span data-ttu-id="7bafd-120">Ein Textfeld zum Eingeben von Namen für Benutzer, Gruppen und Ansprüche.</span><span class="sxs-lookup"><span data-stu-id="7bafd-120">An input text box to enter names for users, groups, and claims.</span></span>
    
 
- <span data-ttu-id="7bafd-121">Ein Span-Steuerelement, das die Namen der aufgelösten Benutzer, Gruppen und Ansprüche zeigt.</span><span class="sxs-lookup"><span data-stu-id="7bafd-121">A span control that shows the names of resolved users, groups, and claims.</span></span>
    
 
- <span data-ttu-id="7bafd-122">Ein ausgeblendetes **div**-Element, das automatisch ein Dropdownfeld mit übereinstimmenden Abfrageergebnissen ausfüllt.</span><span class="sxs-lookup"><span data-stu-id="7bafd-122">A hidden  **div** element that autofills a drop-down box with matching query results.</span></span>
    
 
- <span data-ttu-id="7bafd-123">Ein AutoAusfüllen-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="7bafd-123">An autofill control.</span></span>
    
 

 <span data-ttu-id="7bafd-124">**Hinweis** Die Auswahl und ihre Funktionalität sind in den Skriptdateien **clientforms.js**, **clientpeoplepicker.js** und **autofill.js**definiert, die sich im Ordner „%ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS“ auf dem Server befinden.</span><span class="sxs-lookup"><span data-stu-id="7bafd-124">**Note**  The picker and its functionality are defined in the  **clientforms.js**,  **clientpeoplepicker.js**, and  **autofill.js** script files, which are located in the %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS folder on the server.</span></span>
 


## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in-2013"></a><span data-ttu-id="7bafd-125">Voraussetzungen für das Einrichten der Entwicklungsumgebung für die Verwendung des clientseitiges Personenauswahl-Steuerelements in einem SharePoint-Add-In 2013</span><span class="sxs-lookup"><span data-stu-id="7bafd-125">Prerequisites for setting up your development environment to use the client-side People Picker control in a SharePoint Add-in 2013</span></span>
<span data-ttu-id="7bafd-126"><a name="bk_prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="7bafd-126"></span></span>

<span data-ttu-id="7bafd-p105">In diesem Artikel wird davon ausgegangen, dass Sie die SharePoint-Add-In mithilfe einer Napa- oder Office 365-Entwicklerwebsite erstellen. Wenn Sie diese Entwicklungsumgebung verwenden, sind die Voraussetzungen bereits erfüllt.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p105">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
 

 

 <span data-ttu-id="7bafd-129">**Hinweis** Unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) erhalten Sie Informationen zur Registrierung für eine Entwicklerwebsite und zu den ersten Schritten mit Napa.</span><span class="sxs-lookup"><span data-stu-id="7bafd-129">**Note**  Go to  [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) to find out how to sign up for a Developer Site and start using Napa.</span></span>
 

<span data-ttu-id="7bafd-130">Wenn Sie nicht mit Napa auf einer Entwicklerwebsite arbeiten, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="7bafd-130">If you're not using Napa on a Developer Site, you'll need the following:</span></span>
 

 

- <span data-ttu-id="7bafd-131">SharePoint mit mindestens einem Zielbenutzer</span><span class="sxs-lookup"><span data-stu-id="7bafd-131">SharePoint with at least one target user</span></span>
    
 
- <span data-ttu-id="7bafd-132">Visual Studio 2012 oder Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7bafd-132">Visual Studio 2012 or Visual Studio 2013</span></span>
    
 
- <span data-ttu-id="7bafd-133">Office Developer Tools für Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7bafd-133">Office Developer Tools for Visual Studio 2013</span></span>
    
 

 <span data-ttu-id="7bafd-134">**Hinweis** Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von Add-Ins für Office und SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span><span class="sxs-lookup"><span data-stu-id="7bafd-134">**Note**  For guidance about how to set up a development environment that fits your needs, see  [Start building Office and SharePoint Add-ins](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span>
 

<span data-ttu-id="7bafd-p106">Es folgen die allgemeinen Schritte zum Hinzufügen der Auswahl zu Ihrer App und zum Abrufen von Benutzerinformationen von einem anderen clientseitigen Steuerelement. Den entsprechenden Code finden Sie im  [ Codebeispiel: Verwendung der clientseitigen Personenauswahl](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example).</span><span class="sxs-lookup"><span data-stu-id="7bafd-p106">The following steps describe the high-level steps for adding the picker to your add-in and then getting its user information from another client-side control. See  [Code example: Using the client-side People Picker](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example) for the corresponding code.</span></span>
 

 
<span data-ttu-id="7bafd-137">Sie können das clientseitige Steuerelement "Personenauswahl" in SharePoint-gehosteten, jedoch nicht in anbietergehosteten SharePoint-Add-Ins verwenden. Laden Sie die  [Office App-Modellbeispiele](http://officeams.codeplex.com) herunter, um ein Beispiel dafür zu sehen, wie ein Personenauswahl-Steuerelement in einer anbietergehosteten App implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="7bafd-137">You can use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins, but not in provider-hosted add-ins. For a sample that shows how to implement a people-picker control in a provider-hosted add-in, download the  [Office Add-in Model Samples](http://officeams.codeplex.com).</span></span>
 

 

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="7bafd-138">Verwenden des clientseitigen Personenauswahl-Steuerelements in von SharePoint gehosteten Add-Ins</span><span class="sxs-lookup"><span data-stu-id="7bafd-138">Use the client-side People Picker control in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="7bafd-139"><a name="bk_steps"> </a></span><span class="sxs-lookup"><span data-stu-id="7bafd-139"></span></span>


### <a name="in-your-page-markup"></a><span data-ttu-id="7bafd-140">In Ihrem Seitenmarkup</span><span class="sxs-lookup"><span data-stu-id="7bafd-140">In your page markup</span></span>


1. <span data-ttu-id="7bafd-141">Fügen Sie Verweise auf die Skriptabhängigkeiten des clientseitigen Personenauswahl-Steuerelements hinzu.</span><span class="sxs-lookup"><span data-stu-id="7bafd-141">Add references to the client-side People Picker control's script dependencies.</span></span>
    
 
2. <span data-ttu-id="7bafd-p107">Fügen Sie die HTML-Tags für die Benutzeroberfläche der Seite hinzu. Das Add-In in diesem Beispiel definiert zwei **div**-Elemente: eines, in dem die Auswahl gerendert wird, und eines für die Benutzeroberfläche: eine Schaltfläche zum Aufrufen des Skripts für die Abfrage der Auswahl und der Elemente, die Benutzerinformationen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p107">Add the HTML tags for the page UI. The add-in in this example defines two  **div** elements: one for the picker to render in and one for the UI: a button that invokes script to query the picker and the elements that display user information.</span></span>
    
 

### <a name="in-your-script"></a><span data-ttu-id="7bafd-144">In Ihrem Skript</span><span class="sxs-lookup"><span data-stu-id="7bafd-144">In your script</span></span>


1. <span data-ttu-id="7bafd-145">Erstellen Sie ein JSON-Wörterbuch, das als Schema zum Speichern von auswahlspezifischen Eigenschaften wie z. B. **AllowMultipleValues** und **MaximumEntitySuggestions** verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7bafd-145">Create a JSON dictionary to use as a schema that stores picker-specific properties, such as  **AllowMultipleValues** and **MaximumEntitySuggestions**.</span></span>
    
 
2. <span data-ttu-id="7bafd-146">Rufen Sie die globale Funktion **SPClientPeoplePicker_InitStandaloneControlWrapper** auf.</span><span class="sxs-lookup"><span data-stu-id="7bafd-146">Call the  **SPClientPeoplePicker_InitStandaloneControlWrapper** global function.</span></span>
    
 
3. <span data-ttu-id="7bafd-147">Rufen Sie das Auswahlobjekt von der Seite ab.</span><span class="sxs-lookup"><span data-stu-id="7bafd-147">Get the picker object from the page.</span></span>
    
 
4. <span data-ttu-id="7bafd-p108">Fragen Sie die Auswahl ab. Das Add-In in diesem Beispiel ruft die Methode **GetAllUserInfo** auf, um alle Benutzerinformationen für die aufgelösten Benutzer abzurufen, und die Methode **GetAllUserKeys**, um nur die Schlüssel für die aufgelösten Benutzer abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p108">Query the picker. The add-in in this example calls the  **GetAllUserInfo** method to get all user information for the resolved users and the **GetAllUserKeys** method to just get the keys for the resolved users.</span></span>
    
 
5. <span data-ttu-id="7bafd-p109">Rufen Sie die Benutzer-ID mit dem JavaScript-Objektmodell ab. Die Benutzer-ID ist in den Informationen, die von der Auswahl zurückgegeben werden, nicht enthalten, deshalb ruft das Add-In die **SP.Web.ensureUser**-Methode auf und die ID aus dem zurückgegebenen **SP.User**-Objekt ab.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p109">Get the user ID by using the JavaScript object model. The user ID isn't included in the information that's returned by the picker, so the add-in calls the  **SP.Web.ensureUser** method and gets the ID from the returned **SP.User** object.</span></span>
    
 
<span data-ttu-id="7bafd-152">Rendering, Initialisierung und andere Funktionen der Auswahl werden vom Server bearbeitet, darunter das Durchsuchen und Auflösen von Benutzereingaben für die SharePoint-Authentifizierungsanbieter.</span><span class="sxs-lookup"><span data-stu-id="7bafd-152">Rendering, initializing, and other functionality for the picker are handled by the server, including searching and resolving user input against the SharePoint authentication providers.</span></span>
 

 

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="7bafd-153">Codebeispiel: Verwenden des clientseitigen Personenauswahl-Steuerelements in von SharePoint gehosteten Add-Ins</span><span class="sxs-lookup"><span data-stu-id="7bafd-153">Code example: Using the client-side People Picker in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="7bafd-154"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="7bafd-154"></span></span>

<span data-ttu-id="7bafd-155">Die folgenden HTML- und JavaScript-Codebeispiele fügen ein clientseitiges Personenauswahl-Steuerelement zu einem von SharePoint gehosteten Add-In hinzu.</span><span class="sxs-lookup"><span data-stu-id="7bafd-155">The following HTML and JavaScript code examples add a client-side People Picker control to a SharePoint-hosted add-in.</span></span>
 

 
<span data-ttu-id="7bafd-p110">Das erste Beispiel zeigt das Seitenmarkup für die **PlaceHolderMain-****asp:Content**-Tags auf der Seite „Default.aspx“. Dieser Code verweist auf die Skriptabhängigkeiten der Auswahl, gibt eine eindeutige ID für das DOM-Element an, in dem die Auswahl gerendert wird, und definiert die Benutzeroberfläche des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p110">The first example shows the page markup for the  **PlaceHolderMain** **asp:Content** tags in the Default.aspx page. This code references the picker's script dependencies, gives a unique ID to the DOM element where the picker will render, and defines the add-in's UI.</span></span>
 

 



```HTML
<asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
    <SharePoint:ScriptLink name="clienttemplates.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="clientforms.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="clientpeoplepicker.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="autofill.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.runtime.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.core.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <div id="peoplePickerDiv"></div>
    <div>
        <br/>
        <input type="button" value="Get User Info" onclick="getUserInfo()"></input>
        <br/>
        <h1>User info:</h1>
        <p id="resolvedUsers"></p>
        <h1>User keys:</h1>
        <p id="userKeys"></p> 
        <h1>User ID:</h1>
        <p id="userId"></p>
    </div>
</asp:Content>
```


 <span data-ttu-id="7bafd-158">**Hinweis** Abhängig von Ihrer Umgebung müssen Sie möglicherweise nicht explizit auf all diese Abhängigkeiten verweisen.</span><span class="sxs-lookup"><span data-stu-id="7bafd-158">**Note**  Depending on your environment, you might not have to explicitly reference all of these dependencies.</span></span>
 

<span data-ttu-id="7bafd-p111">Das folgende Beispiel zeigt das Skript aus der Datei "App.js". Dieses Skript initialisiert und rendert die Auswahl und fragt anschließend Benutzerinformationen davon ab. Außerdem ruft es mithilfe des JavaScript-Objektmodells die Benutzer-ID ab.</span><span class="sxs-lookup"><span data-stu-id="7bafd-p111">The following example shows the script from the App.js file. This script initializes and renders the picker, queries it for user information, and then gets the user ID by using the JavaScript object model.</span></span>
 

 



```
// Run your custom code when the DOM is ready.
$(document).ready(function () {

    // Specify the unique ID of the DOM element where the
    // picker will render.
    initializePeoplePicker('peoplePickerDiv');
});

// Render and initialize the client-side People Picker.
function initializePeoplePicker(peoplePickerElementId) {

    // Create a schema to store picker properties, and set the properties.
    var schema = {};
    schema['PrincipalAccountType'] = 'User,DL,SecGroup,SPGroup';
    schema['SearchPrincipalSource'] = 15;
    schema['ResolvePrincipalSource'] = 15;
    schema['AllowMultipleValues'] = true;
    schema['MaximumEntitySuggestions'] = 50;
    schema['Width'] = '280px';

    // Render and initialize the picker. 
    // Pass the ID of the DOM element that contains the picker, an array of initial
    // PickerEntity objects to set the picker value, and a schema that defines
    // picker properties.
    this.SPClientPeoplePicker_InitStandaloneControlWrapper(peoplePickerElementId, null, schema);
}

// Query the picker for user information.
function getUserInfo() {

    // Get the people picker object from the page.
    var peoplePicker = this.SPClientPeoplePicker.SPClientPeoplePickerDict.peoplePickerDiv_TopSpan;

    // Get information about all users.
    var users = peoplePicker.GetAllUserInfo();
    var userInfo = '';
    for (var i = 0; i < users.length; i++) {
        var user = users[i];
        for (var userProperty in user) { 
            userInfo += userProperty + ':  ' + user[userProperty] + '<br>';
        }
    }
    $('#resolvedUsers').html(userInfo);

    // Get user keys.
    var keys = peoplePicker.GetAllUserKeys();
    $('#userKeys').html(keys);

    // Get the first user's ID by using the login name.
    getUserId(users[0].Key);
}

// Get the user ID.
function getUserId(loginName) {
    var context = new SP.ClientContext.get_current();
    this.user = context.get_web().ensureUser(loginName);
    context.load(this.user);
    context.executeQueryAsync(
         Function.createDelegate(null, ensureUserSuccess), 
         Function.createDelegate(null, onFail)
    );
}

function ensureUserSuccess() {
    $('#userId').html(this.user.get_id());
}

function onFail(sender, args) {
    alert('Query failed. Error: ' + args.get_message());
}
```


## <a name="additional-resources"></a><span data-ttu-id="7bafd-161">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7bafd-161">Additional resources</span></span>
<span data-ttu-id="7bafd-162"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7bafd-162"></span></span>


-  [<span data-ttu-id="7bafd-163">Erstellen von UX-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7bafd-163">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="7bafd-164">Überblick über die Personenauswahl und Anspruchsanbieter (SharePoint)</span><span class="sxs-lookup"><span data-stu-id="7bafd-164">People Picker and claims providers overview (SharePoint)</span></span>](http://technet.microsoft.com/library/gg602078.aspx)
    
 
-  [<span data-ttu-id="7bafd-165">Konfigurieren der Personenauswahl in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7bafd-165">Configure People Picker in SharePoint</span></span>](http://technet.microsoft.com/library/gg602075.aspx)
    
 

