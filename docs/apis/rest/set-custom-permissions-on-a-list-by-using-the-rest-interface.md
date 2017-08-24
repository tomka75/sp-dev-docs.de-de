# <a name="set-custom-permissions-on-a-list-by-using-the-rest-interface"></a>Festlegen von benutzerdefinierten Berechtigungen in einer Liste mithilfe der REST-Schnittstelle
Informationen zum Definieren von benutzerdefinierten abgestimmten Berechtigungen in einer SharePoint-Liste mithilfe der REST-Schnittstelle und JavaScript.

SharePoint-Websites, Listen und Listenelemente sind Typen von **SecurableObject**. Standardmäßig erbt ein sicherungsfähiges Objekt die übergeordneten Berechtigungen. Wenn Sie benutzerdefinierte Berechtigungen für ein Objekt festlegen möchten, müssen Sie die Vererbung der Berechtigungen unterbrechen und dann durch Hinzufügen oder Entfernen von Rollenzuweisungen neue Berechtigungen definieren.
 
 **Hinweis**  Links zu Artikeln zum Festlegen abgestimmter Berechtigungen finden Sie unter [zusätzliche Ressourcen](set-custom-permissions-on-a-list-by-using-the-rest-interface.md#bk_addresources).
 
In dem Codebeispiel in diesem Artikel werden benutzerdefinierte Berechtigungen in einer Liste zugewiesen, anschließend werden die Gruppenberechtigungen für die Liste geändert. In dem Beispiel wird die REST-Schnittstelle für folgende Vorgänge verwendet:
 

- Zum Abrufen der ID der Zielgruppe. In dem Beispiel wird die Gruppen-ID verwendet, um die aktuellen Rollenbindungen für die Gruppe in der Liste abzurufen, und um der Liste die neue Rolle hinzuzufügen.

- Zum Abrufen der ID der Rollendefinition, die die neuen Berechtigungen für die Gruppe definiert. Die ID wird verwendet, um der Liste die neue Rolle hinzuzufügen. In diesem Beispiel wird die vorhandene Rollendefinition für die neue Rolle verwendet, Sie können optional jedoch auch eine neue Rollendefinition erstellen.
 
- Unterbrechen Sie die Vererbung von Rollen in der Liste mithilfe der Methode `BreakRoleInheritance`. Im Beispiel wird die Rollenvererbung unterbrochen, der aktuelle Rollensatz jedoch beibehalten. (Alternativ können Sie darauf verzichten, Rollenzuweisungen zu kopieren und den aktuellen Benutzer zur Stufe der Berechtigungsverwaltung hinzuzufügen.)
 
- Entfernen Sie die aktuelle Rollenzuweisung der Gruppe in der Liste, indem Sie eine DELETE-Anforderung an den Rollenzuweisungsendpunkt senden. (Wenn Sie vorsehen, keine Rollenzuweisungen zu kopieren, können Sie diesen Schritt überspringen).
 
- Fügen Sie eine Rollenzuweisung für die Gruppe mithilfe der Methode `AddRoleAssignment` hinzu, die die Gruppe an die Rollendefinition bindet und die Rolle zu der Liste hinzufügt.
    
## <a name="prerequisites-for-using-the-example-in-this-article"></a>Voraussetzungen für die Verwendung des Beispiels in diesem Artikel
<a name="SP15Accessdatafromremoteapp_Prereq"> </a> Um das Beispiel in diesem Artikel verwenden zu können, benötigen Sie:

- Eine SharePoint-Entwicklungsumgebung (App-Isolierung für lokale Szenarien erforderlich)
- Visual Studio 2013 oder höher mit Office Developer Tools
    
Außerdem müssen Sie Add-in-Berechtigungen mit **Vollzugriff** für den **Web**-Bereich festlegen. Nur Benutzer, die über ausreichende Berechtigungen zum Ändern von Listenberechtigungen verfügen (z. B. Websitebesitzer), können dieses Add-in ausführen.

## <a name="example-set-custom-permissions-on-a-list-by-using-the-rest-interface"></a>Beispiel: Festlegen von benutzerdefinierten Berechtigungen in einer Liste mithilfe der REST-Schnittstelle
<a name="bk_example1"> </a>

In den folgenden Beispielen ist der Inhalt der Datei „App.js“ in einem auf SharePoint gehosteten Add-in dargestellt. Im ersten Beispiel wird die domainübergreifende JavaScript-Bibliothek zu Erstellen und Senden der HTTP-Anfragen verwendet. Im zweiten Beispiel werden jQuery AJAX-Anfragen verwendet.
 
Bevor Sie den Code ausführen, ersetzen Sie die Platzhalterwerte mit tatsächlichen Werten. Wenn Sie eine andere Sprache oder Umgebung verwenden, müssen Sie einige Komponenten der Anforderung hinzufügen oder ändern. Weitere Informationen finden Sie unter [How REST requests differ by environment](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer) (So unterscheiden sich REST-Anforderungen je nach Umgebung).
 
 **Beispiel 1: Domänenübergreifende Bibliotheksanforderungen**
 
```javascript
'use strict';

// Change placeholder values before you run this code.
var listTitle = 'List 1';
var groupName = 'Group A';
var targetRoleDefinitionName = 'Contribute';
var appweburl;
var hostweburl;
var executor;
var groupId;
var targetRoleDefinitionId;

$(document).ready( function() {

    //Get the URI decoded URLs.
    hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
    appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

    // Load the cross-domain library file and continue to the custom code.
    var scriptbase = hostweburl + "/_layouts/15/";
    $.getScript(scriptbase + "SP.RequestExecutor.js", getTargetGroupId);
});

// Get the ID of the target group.
function getTargetGroupId() {
    executor = new SP.RequestExecutor(appweburl);
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/sitegroups/getbyname('";
    endpointUri += groupName + "')/id" + "?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            var jsonObject = JSON.parse(responseData.body);
            groupId = jsonObject.d.Id;
            getTargetRoleDefinitionId();
        },
        error: errorHandler
   });
}

// Get the ID of the role definition that defines the permissions
// you want to assign to the group.
function getTargetRoleDefinitionId() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/roledefinitions/getbyname('";
    endpointUri += targetRoleDefinitionName + "')/id" + "?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            var jsonObject = JSON.parse(responseData.body)
            targetRoleDefinitionId = jsonObject.d.Id;
            breakRoleInheritanceOfList();
        },
        error: errorHandler
    });
}

// Break role inheritance on the list.
function breakRoleInheritanceOfList() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/breakroleinheritance(true)?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: deleteCurrentRoleForGroup,
        error: errorHandler
    });
}

// Remove the current role assignment for the group on the list.
function deleteCurrentRoleForGroup() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/roleassignments/getbyprincipalid('" + groupId + "')?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 
            'X-RequestDigest':$('#__REQUESTDIGEST').val(),
            'X-HTTP-Method':'DELETE'
        },
        success: setNewPermissionsForGroup,
        error: errorHandler
    });
}

// Add the new role assignment for the group on the list.
function setNewPermissionsForGroup() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/roleassignments/addroleassignment(principalid=" + groupId;
    endpointUri += ",roledefid=" + targetRoleDefinitionId + ")?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: successHandler,
        error: errorHandler
    });
}

// Get parameters from the query string.
// For production purposes you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var singleParam = params[i].split("=");
        if (singleParam[0] == paramToRetrieve) return singleParam[1];
    }
}

function successHandler() {
    alert('Request succeeded.');
} 

function errorHandler(xhr, ajaxOptions, thrownError) {
    alert('Request failed: ' + xhr.status + '\n' + thrownError + '\n' + xhr.responseText);
}
```

 **Beispiel 2: jQuery AJAX-Anforderungen**
 
```javascript
// Change placeholder values before you run this code.
var siteUrl = 'http://server/site';
var listTitle = 'List 1';
var groupName = 'Group A';
var targetRoleDefinitionName = 'Contribute';
var groupId;
var targetRoleDefinitionId;

$(document).ready( function() {
    getTargetGroupId();
});

// Get the ID of the target group.
function getTargetGroupId() {
    $.ajax({
        url: siteUrl + '/_api/web/sitegroups/getbyname(\'' + groupName + '\')/id',
        type: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            groupId = responseData.d.Id;
            getTargetRoleDefinitionId();
        },
        error: errorHandler
   });
}

// Get the ID of the role definition that defines the permissions
// you want to assign to the group.
function getTargetRoleDefinitionId() {
    $.ajax({
        url: siteUrl + '/_api/web/roledefinitions/getbyname(\''
            + targetRoleDefinitionName + '\')/id',
        type: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            targetRoleDefinitionId = responseData.d.Id;
            breakRoleInheritanceOfList();
        },
        error: errorHandler
    });
}

// Break role inheritance on the list.
function breakRoleInheritanceOfList() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/breakroleinheritance(true)',
        type: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: deleteCurrentRoleForGroup,
        error: errorHandler
    });
}

// Remove the current role assignment for the group on the list.
function deleteCurrentRoleForGroup() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/roleassignments/getbyprincipalid(' + groupId + ')',
        type: 'POST',
        headers: { 
            'X-RequestDigest':$('#__REQUESTDIGEST').val(),
            'X-HTTP-Method':'DELETE'
        },
        success: setNewPermissionsForGroup,
        error: errorHandler
    });
}

// Add the new role assignment for the group on the list.
function setNewPermissionsForGroup() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/roleassignments/addroleassignment(principalid='
            + groupId + ',roledefid=' + targetRoleDefinitionId + ')',
        type: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: successHandler,
        error: errorHandler
    });
}

function successHandler() {
    alert('Request succeeded.');
} 

function errorHandler(xhr, ajaxOptions, thrownError) {
    alert('Request failed: ' + xhr.status + '\n' + thrownError + '\n' + xhr.responseText);
}
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-rest-service.md) 
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)

- REST-Ressourcen:
     - [Ressource GroupCollection](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_GroupCollection)
     - [Ressource Group](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_Group) 
     - [Ressource RoleAssignmentCollection](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignmentCollection)
     - [Ressource RoleAssignment](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignment)
     - [Ressource RoleDefinitionCollection](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinitionCollection)
     - [Ressource RoleDefinition](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinition)
    
 
- TechNet-Artikel:
     - [Referenz zu abgestimmten Berechtigungen für SharePoint Server 2013](http://technet.microsoft.com/de-de/library/dn169567.aspx)
     - [Bewährte Methoden für die Verwendung abgestimmter Berechtigungen in SharePoint Server 2013](http://technet.microsoft.com/de-de/library/gg128955.aspx)
     - [Benutzerberechtigungen und Berechtigungsstufen in SharePoint 2013](http://technet.microsoft.com/de-de/library/cc721640.aspx)
    
 

