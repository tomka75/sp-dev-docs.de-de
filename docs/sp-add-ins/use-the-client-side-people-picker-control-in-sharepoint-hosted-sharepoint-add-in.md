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
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a>Verwenden des clientseitigen Personenauswahl-Steuerelement in von SharePoint gehosteten SharePoint-Add-Ins
Erfahren Sie, wie das clientseitige Personenauswahl-Steuerelement in von SharePoint gehosteten SharePoint-Add-Ins verwendet wird.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


 **Wichtig** In diesem Thema wird davon ausgegangen, dass Sie wissen, wie ein von SharePoint gehostetes SharePoint-Add-In erstellt wird. Wenn Sie mehr über das Erstellen erfahren möchten, beginnen Sie mit [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).
 


## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a>Was ist das clientseitige Personenauswahl-Steuerelement in SharePoint?
<a name="bk_whatIs"> </a>

Mit dem clientseitigen Personenauswahl-Steuerelement können Benutzer schnell nach gültigen Benutzerkonten von Personen, Gruppen und Ansprüchen in ihrer Organisation suchen und diese auswählen. Bei der Auswahl handelt es sich um ein HTML- und JavaScript-Steuerelement mit browserübergreifender Unterstützung. Das Hinzufügen der Auswahl zu Ihrem Add-In ist einfach: Fügen Sie in Ihrem Markup ein Containerelement für das Steuerelement sowie Verweise auf das Steuerelement und seine Abhängigkeiten hinzu. Rufen Sie dann in Ihrem Skript die globale Funktion **SPClientPeoplePicker_InitStandaloneControlWrapper** auf, um die Auswahl zu rendern und zu initialisieren.
 

 
Die Auswahl wird durch das **SPClientPeoplePicker**-Objekt dargestellt, das Methoden bereitstellt, mit dem andere clientseitige Steuerelemente Informationen von der Auswahl abrufen oder andere Vorgänge durchführen können. Sie können **SPClientPeoplePicker**-Eigenschaften verwenden, um die Auswahl mit steuerelementspezifischen Einstellungen zu konfigurieren, z. B. um mehrere Benutzer zuzulassen oder Zwischenspeicheroptionen festzulegen. Die Auswahl verwendet auch Konfigurationseinstellungen für Webanwendungen wie z. B. Active Directory-Domänendienste-Parameter oder Zielgesamtstrukturen. Konfigurationseinstellungen für Webanwendungen werden automatisch ausgewählt (von der **SPWebApplication.PeoplePickerSettings**-Eigenschaft).
 

 
Die Auswahl besteht aus den folgenden Komponenten:
 

 

- Ein Textfeld zum Eingeben von Namen für Benutzer, Gruppen und Ansprüche.
    
 
- Ein Span-Steuerelement, das die Namen der aufgelösten Benutzer, Gruppen und Ansprüche zeigt.
    
 
- Ein ausgeblendetes **div**-Element, das automatisch ein Dropdownfeld mit übereinstimmenden Abfrageergebnissen ausfüllt.
    
 
- Ein AutoAusfüllen-Steuerelement.
    
 

 **Hinweis** Die Auswahl und ihre Funktionalität sind in den Skriptdateien **clientforms.js**, **clientpeoplepicker.js** und **autofill.js**definiert, die sich im Ordner „%ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS“ auf dem Server befinden.
 


## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in-2013"></a>Voraussetzungen für das Einrichten der Entwicklungsumgebung für die Verwendung des clientseitiges Personenauswahl-Steuerelements in einem SharePoint-Add-In 2013
<a name="bk_prereqs"> </a>

In diesem Artikel wird davon ausgegangen, dass Sie die SharePoint-Add-In mithilfe einer Napa- oder Office 365-Entwicklerwebsite erstellen. Wenn Sie diese Entwicklungsumgebung verwenden, sind die Voraussetzungen bereits erfüllt.
 

 

 **Hinweis** Unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) erhalten Sie Informationen zur Registrierung für eine Entwicklerwebsite und zu den ersten Schritten mit Napa.
 

Wenn Sie nicht mit Napa auf einer Entwicklerwebsite arbeiten, benötigen Sie Folgendes:
 

 

- SharePoint mit mindestens einem Zielbenutzer
    
 
- Visual Studio 2012 oder Visual Studio 2013
    
 
- Office Developer Tools für Visual Studio 2013
    
 

 **Hinweis** Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von Add-Ins für Office und SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

Es folgen die allgemeinen Schritte zum Hinzufügen der Auswahl zu Ihrer App und zum Abrufen von Benutzerinformationen von einem anderen clientseitigen Steuerelement. Den entsprechenden Code finden Sie im  [ Codebeispiel: Verwendung der clientseitigen Personenauswahl](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example).
 

 
Sie können das clientseitige Steuerelement "Personenauswahl" in SharePoint-gehosteten, jedoch nicht in anbietergehosteten SharePoint-Add-Ins verwenden. Laden Sie die  [Office App-Modellbeispiele](http://officeams.codeplex.com) herunter, um ein Beispiel dafür zu sehen, wie ein Personenauswahl-Steuerelement in einer anbietergehosteten App implementiert wird.
 

 

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a>Verwenden des clientseitigen Personenauswahl-Steuerelements in von SharePoint gehosteten Add-Ins
<a name="bk_steps"> </a>


### <a name="in-your-page-markup"></a>In Ihrem Seitenmarkup


1. Fügen Sie Verweise auf die Skriptabhängigkeiten des clientseitigen Personenauswahl-Steuerelements hinzu.
    
 
2. Fügen Sie die HTML-Tags für die Benutzeroberfläche der Seite hinzu. Das Add-In in diesem Beispiel definiert zwei **div**-Elemente: eines, in dem die Auswahl gerendert wird, und eines für die Benutzeroberfläche: eine Schaltfläche zum Aufrufen des Skripts für die Abfrage der Auswahl und der Elemente, die Benutzerinformationen anzeigen.
    
 

### <a name="in-your-script"></a>In Ihrem Skript


1. Erstellen Sie ein JSON-Wörterbuch, das als Schema zum Speichern von auswahlspezifischen Eigenschaften wie z. B. **AllowMultipleValues** und **MaximumEntitySuggestions** verwendet wird.
    
 
2. Rufen Sie die globale Funktion **SPClientPeoplePicker_InitStandaloneControlWrapper** auf.
    
 
3. Rufen Sie das Auswahlobjekt von der Seite ab.
    
 
4. Fragen Sie die Auswahl ab. Das Add-In in diesem Beispiel ruft die Methode **GetAllUserInfo** auf, um alle Benutzerinformationen für die aufgelösten Benutzer abzurufen, und die Methode **GetAllUserKeys**, um nur die Schlüssel für die aufgelösten Benutzer abzurufen.
    
 
5. Rufen Sie die Benutzer-ID mit dem JavaScript-Objektmodell ab. Die Benutzer-ID ist in den Informationen, die von der Auswahl zurückgegeben werden, nicht enthalten, deshalb ruft das Add-In die **SP.Web.ensureUser**-Methode auf und die ID aus dem zurückgegebenen **SP.User**-Objekt ab.
    
 
Rendering, Initialisierung und andere Funktionen der Auswahl werden vom Server bearbeitet, darunter das Durchsuchen und Auflösen von Benutzereingaben für die SharePoint-Authentifizierungsanbieter.
 

 

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a>Codebeispiel: Verwenden des clientseitigen Personenauswahl-Steuerelements in von SharePoint gehosteten Add-Ins
<a name="bk_example"> </a>

Die folgenden HTML- und JavaScript-Codebeispiele fügen ein clientseitiges Personenauswahl-Steuerelement zu einem von SharePoint gehosteten Add-In hinzu.
 

 
Das erste Beispiel zeigt das Seitenmarkup für die **PlaceHolderMain-****asp:Content**-Tags auf der Seite „Default.aspx“. Dieser Code verweist auf die Skriptabhängigkeiten der Auswahl, gibt eine eindeutige ID für das DOM-Element an, in dem die Auswahl gerendert wird, und definiert die Benutzeroberfläche des Add-Ins.
 

 



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


 **Hinweis** Abhängig von Ihrer Umgebung müssen Sie möglicherweise nicht explizit auf all diese Abhängigkeiten verweisen.
 

Das folgende Beispiel zeigt das Skript aus der Datei "App.js". Dieses Skript initialisiert und rendert die Auswahl und fragt anschließend Benutzerinformationen davon ab. Außerdem ruft es mithilfe des JavaScript-Objektmodells die Benutzer-ID ab.
 

 



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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint.md)
    
 
-  [Überblick über die Personenauswahl und Anspruchsanbieter (SharePoint)](http://technet.microsoft.com/library/gg602078.aspx)
    
 
-  [Konfigurieren der Personenauswahl in SharePoint](http://technet.microsoft.com/library/gg602075.aspx)
    
 

