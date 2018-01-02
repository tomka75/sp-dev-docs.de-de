---
title: Festlegen von benutzerdefinierten Berechtigungen in einer Liste mithilfe der REST-Schnittstelle
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2fe15a33964aadcae0c1aa3495251a2475335c3f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-custom-permissions-on-a-list-by-using-the-rest-interface"></a><span data-ttu-id="345c2-102">Festlegen von benutzerdefinierten Berechtigungen in einer Liste mithilfe der REST-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="345c2-102">Set custom permissions on a list by using the REST interface</span></span>
<span data-ttu-id="345c2-103">Informationen zum Definieren von benutzerdefinierten abgestimmten Berechtigungen in einer SharePoint-Liste mithilfe der REST-Schnittstelle und JavaScript.</span><span class="sxs-lookup"><span data-stu-id="345c2-103">Learn how to define custom, fine-grained permissions on a SharePoint list by using the REST interface and JavaScript.</span></span>

<span data-ttu-id="345c2-p101">SharePoint-Websites, Listen und Listenelemente sind Typen von **SecurableObject**. Standardmäßig erbt ein sicherungsfähiges Objekt die übergeordneten Berechtigungen. Wenn Sie benutzerdefinierte Berechtigungen für ein Objekt festlegen möchten, müssen Sie die Vererbung der Berechtigungen unterbrechen und dann durch Hinzufügen oder Entfernen von Rollenzuweisungen neue Berechtigungen definieren.</span><span class="sxs-lookup"><span data-stu-id="345c2-p101">SharePoint sites, lists, and list items are types of  **SecurableObject**. By default, a securable object inherits the permissions of its parent. To set custom permissions for an object, you need to break its inheritance so that it stops inheriting permissions from its parent, and then define new permissions by adding or removing role assignments.</span></span>
 
> [!Note]
> <span data-ttu-id="345c2-107">Links zu Artikeln zum Festlegen abgestimmter Berechtigungen finden Sie unter [zusätzliche Ressourcen](set-custom-permissions-on-a-list-by-using-the-rest-interface.md#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="345c2-107">See [Additional resources](set-custom-permissions-on-a-list-by-using-the-rest-interface.md#bk_addresources) for links to articles about setting fine-grained permissions.</span></span>
 
<span data-ttu-id="345c2-p102">In dem Codebeispiel in diesem Artikel werden benutzerdefinierte Berechtigungen in einer Liste zugewiesen, anschließend werden die Gruppenberechtigungen für die Liste geändert. In dem Beispiel wird die REST-Schnittstelle für folgende Vorgänge verwendet:</span><span class="sxs-lookup"><span data-stu-id="345c2-p102">The code example in this article sets custom permissions on a list, and then changes a group's permissions to it. The example uses the REST interface to:</span></span>
 

- <span data-ttu-id="345c2-p103">Zum Abrufen der ID der Zielgruppe. In dem Beispiel wird die Gruppen-ID verwendet, um die aktuellen Rollenbindungen für die Gruppe in der Liste abzurufen, und um der Liste die neue Rolle hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="345c2-p103">Get the ID of the target group. The example uses the group ID to get the current role bindings for the group on the list and to add the new role to the list.</span></span>

- <span data-ttu-id="345c2-p104">Zum Abrufen der ID der Rollendefinition, die die neuen Berechtigungen für die Gruppe definiert. Die ID wird verwendet, um der Liste die neue Rolle hinzuzufügen. In diesem Beispiel wird die vorhandene Rollendefinition für die neue Rolle verwendet, Sie können optional jedoch auch eine neue Rollendefinition erstellen.</span><span class="sxs-lookup"><span data-stu-id="345c2-p104">Get the ID of the role definition that defines the new permissions for the group. The ID is used to add the new role to the list. This example uses an existing role definition for the new role, but you can optionally create a new role definition.</span></span>
 
- <span data-ttu-id="345c2-p105">Unterbrechen Sie die Vererbung von Rollen in der Liste mithilfe der Methode `BreakRoleInheritance`. Im Beispiel wird die Rollenvererbung unterbrochen, der aktuelle Rollensatz jedoch beibehalten. (Alternativ können Sie darauf verzichten, Rollenzuweisungen zu kopieren und den aktuellen Benutzer zur Stufe der Berechtigungsverwaltung hinzuzufügen.)</span><span class="sxs-lookup"><span data-stu-id="345c2-p105">Break role inheritance on the list by using the  `BreakRoleInheritance` method. The example breaks role inheritance but keeps the current set of roles. (Alternatively, you can choose not to copy any role assignments and to add the current user to the Manage permission level.)</span></span>
 
- <span data-ttu-id="345c2-p106">Entfernen Sie die aktuelle Rollenzuweisung der Gruppe in der Liste, indem Sie eine DELETE-Anforderung an den Rollenzuweisungsendpunkt senden. (Wenn Sie vorsehen, keine Rollenzuweisungen zu kopieren, können Sie diesen Schritt überspringen).</span><span class="sxs-lookup"><span data-stu-id="345c2-p106">Remove the group's current role assignment on the list by sending a DELETE request to the role assignment endpoint. (If you choose not to copy any role assignments, you would skip this step.)</span></span>
 
- <span data-ttu-id="345c2-120">Fügen Sie eine Rollenzuweisung für die Gruppe mithilfe der Methode `AddRoleAssignment` hinzu, die die Gruppe an die Rollendefinition bindet und die Rolle zu der Liste hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="345c2-120">Add a role assignment for the group to the list by using the  `AddRoleAssignment` method, which binds the group to the role definition and adds the role to the list.</span></span>
    
## <a name="prerequisites-for-using-the-example-in-this-article"></a><span data-ttu-id="345c2-121">Voraussetzungen für die Verwendung des Beispiels in diesem Artikel</span><span class="sxs-lookup"><span data-stu-id="345c2-121">Prerequisites for using the example in this article</span></span>
<span data-ttu-id="345c2-122"><a name="SP15Accessdatafromremoteapp_Prereq"> </a> Um das Beispiel in diesem Artikel verwenden zu können, benötigen Sie:</span><span class="sxs-lookup"><span data-stu-id="345c2-122"><a name="SP15Accessdatafromremoteapp_Prereq"> </a> To use the example in this article, you'll need:</span></span>

- <span data-ttu-id="345c2-123">Eine SharePoint-Entwicklungsumgebung (App-Isolierung für lokale Szenarien erforderlich)</span><span class="sxs-lookup"><span data-stu-id="345c2-123">A SharePoint development environment (app isolation required for on-premises scenarios)</span></span>
- <span data-ttu-id="345c2-124">Visual Studio 2013 oder höher mit Office Developer Tools</span><span class="sxs-lookup"><span data-stu-id="345c2-124">Visual Studio 2013 with Office Developer Tools or newer</span></span>
    
<span data-ttu-id="345c2-p107">Außerdem müssen Sie Add-in-Berechtigungen mit **Vollzugriff** für den **Web**-Bereich festlegen. Nur Benutzer, die über ausreichende Berechtigungen zum Ändern von Listenberechtigungen verfügen (z. B. Websitebesitzer), können dieses Add-in ausführen.</span><span class="sxs-lookup"><span data-stu-id="345c2-p107">You'll also need to set  **Full Control** add-in permissions at the **Web** scope. Only users who have sufficient permissions to change list permissions (such as site owners) can run this add-in.</span></span>

## <a name="example-set-custom-permissions-on-a-list-by-using-the-rest-interface"></a><span data-ttu-id="345c2-127">Beispiel: Festlegen von benutzerdefinierten Berechtigungen in einer Liste mithilfe der REST-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="345c2-127">Example: Set custom permissions on a list by using the REST interface</span></span>
<span data-ttu-id="345c2-128"><a name="bk_example1"> </a></span><span class="sxs-lookup"><span data-stu-id="345c2-128"></span></span>

<span data-ttu-id="345c2-p108">In den folgenden Beispielen ist der Inhalt der Datei „App.js“ in einem auf SharePoint gehosteten Add-in dargestellt. Im ersten Beispiel wird die domainübergreifende JavaScript-Bibliothek zu Erstellen und Senden der HTTP-Anfragen verwendet. Im zweiten Beispiel werden jQuery AJAX-Anfragen verwendet.</span><span class="sxs-lookup"><span data-stu-id="345c2-p108">The following examples represent the contents of the App.js file in a SharePoint-hosted add-in. The first example uses the JavaScript cross-domain library to build and send HTTP requests. The second example uses jQuery AJAX requests.</span></span>
 
<span data-ttu-id="345c2-p109">Bevor Sie den Code ausführen, ersetzen Sie die Platzhalterwerte mit tatsächlichen Werten. Wenn Sie eine andere Sprache oder Umgebung verwenden, müssen Sie einige Komponenten der Anforderung hinzufügen oder ändern. Weitere Informationen finden Sie unter [How REST requests differ by environment](complete-basic-operations-using-sharepoint-rest-endpoints.md#bk_HowRequestsDiffer) (So unterscheiden sich REST-Anforderungen je nach Umgebung).</span><span class="sxs-lookup"><span data-stu-id="345c2-p109">Before you run the code, replace the placeholder values with actual values. If you're using a different language or environment, you'll need to add or change some request components. See  [How REST requests differ by environment](complete-basic-operations-using-sharepoint-rest-endpoints.md#bk_HowRequestsDiffer) for more information.</span></span>
 
 <span data-ttu-id="345c2-135">**Beispiel 1: Domänenübergreifende Bibliotheksanforderungen**</span><span class="sxs-lookup"><span data-stu-id="345c2-135">**Example 1: Cross-domain library requests**</span></span>
 
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

 <span data-ttu-id="345c2-136">**Beispiel 2: jQuery AJAX-Anforderungen**</span><span class="sxs-lookup"><span data-stu-id="345c2-136">**Example 2: jQuery AJAX requests**</span></span>
 
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


## <a name="see-also"></a><span data-ttu-id="345c2-137">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="345c2-137">See also</span></span>
<span data-ttu-id="345c2-138"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="345c2-138"></span></span>

-  [<span data-ttu-id="345c2-139">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="345c2-139">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md) 
-  [<span data-ttu-id="345c2-140">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="345c2-140">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="345c2-141">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="345c2-141">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)

- <span data-ttu-id="345c2-142">REST-Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="345c2-142">REST resources:</span></span>
     - [<span data-ttu-id="345c2-143">Ressource GroupCollection</span><span class="sxs-lookup"><span data-stu-id="345c2-143">GroupCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_GroupCollection)
     - [<span data-ttu-id="345c2-144">Ressource Group</span><span class="sxs-lookup"><span data-stu-id="345c2-144">Group resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_Group) 
     - [<span data-ttu-id="345c2-145">Ressource RoleAssignmentCollection</span><span class="sxs-lookup"><span data-stu-id="345c2-145">RoleAssignmentCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignmentCollection)
     - [<span data-ttu-id="345c2-146">Ressource RoleAssignment</span><span class="sxs-lookup"><span data-stu-id="345c2-146">RoleAssignment resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignment)
     - [<span data-ttu-id="345c2-147">Ressource RoleDefinitionCollection</span><span class="sxs-lookup"><span data-stu-id="345c2-147">RoleDefinitionCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinitionCollection)
     - [<span data-ttu-id="345c2-148">Ressource RoleDefinition</span><span class="sxs-lookup"><span data-stu-id="345c2-148">RoleDefinition resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinition)
    
 
- <span data-ttu-id="345c2-149">TechNet-Artikel:</span><span class="sxs-lookup"><span data-stu-id="345c2-149">TechNet articles:</span></span>
     - [<span data-ttu-id="345c2-150">Referenz zu abgestimmten Berechtigungen für SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="345c2-150">Fine-grained permission reference for SharePoint Server 2013</span></span>](http://technet.microsoft.com/de-DE/library/dn169567.aspx)
     - [<span data-ttu-id="345c2-151">Bewährte Methoden für die Verwendung abgestimmter Berechtigungen in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="345c2-151">Best practices for using fine-grained permissions in SharePoint Server 2013</span></span>](http://technet.microsoft.com/de-DE/library/gg128955.aspx)
     - [<span data-ttu-id="345c2-152">Benutzerberechtigungen und Berechtigungsstufen in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="345c2-152">User permissions and permission levels in SharePoint 2013</span></span>](http://technet.microsoft.com/de-DE/library/cc721640.aspx)
    
 

