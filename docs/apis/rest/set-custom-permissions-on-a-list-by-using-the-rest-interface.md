<span data-ttu-id="905c6-p109">Bevor Sie den Code ausführen, ersetzen Sie die Platzhalterwerte mit tatsächlichen Werten. Wenn Sie eine andere Sprache oder Umgebung verwenden, müssen Sie einige Komponenten der Anforderung hinzufügen oder ändern. Weitere Informationen finden Sie unter [How REST requests differ by environment](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer) (So unterscheiden sich REST-Anforderungen je nach Umgebung).</span><span class="sxs-lookup"><span data-stu-id="905c6-p109">Before you run the code, replace the placeholder values with actual values. If you're using a different language or environment, you'll need to add or change some request components. See  [How REST requests differ by environment](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer) for more information.</span></span>
 
Bevor Sie den Code ausführen, ersetzen Sie die Platzhalterwerte mit tatsächlichen Werten. Wenn Sie eine andere Sprache oder Umgebung verwenden, müssen Sie einige Komponenten der Anforderung hinzufügen oder ändern. Weitere Informationen finden Sie unter [How REST requests differ by environment](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer) (So unterscheiden sich REST-Anforderungen je nach Umgebung).
 
 <span data-ttu-id="905c6-134">**Beispiel 1: Domänenübergreifende Bibliotheksanforderungen**</span><span class="sxs-lookup"><span data-stu-id="905c6-134">**Example 1: Cross-domain library requests**</span></span>
 
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

 <span data-ttu-id="905c6-135">**Beispiel 2: jQuery AJAX-Anforderungen**</span><span class="sxs-lookup"><span data-stu-id="905c6-135">**Example 2: jQuery AJAX requests**</span></span>
 
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


## <a name="additional-resources"></a><span data-ttu-id="905c6-136">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="905c6-136">Additional resources</span></span>
<span data-ttu-id="905c6-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="905c6-137"></span></span>

-  [<span data-ttu-id="905c6-138">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="905c6-138">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md) 
-  [<span data-ttu-id="905c6-139">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="905c6-139">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="905c6-140">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="905c6-140">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)

- <span data-ttu-id="905c6-141">REST-Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="905c6-141">REST resources:</span></span>
     - [<span data-ttu-id="905c6-142">Ressource GroupCollection</span><span class="sxs-lookup"><span data-stu-id="905c6-142">GroupCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_GroupCollection)
     - [<span data-ttu-id="905c6-143">Ressource Group</span><span class="sxs-lookup"><span data-stu-id="905c6-143">Group resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_Group) 
     - [<span data-ttu-id="905c6-144">Ressource RoleAssignmentCollection</span><span class="sxs-lookup"><span data-stu-id="905c6-144">RoleAssignmentCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignmentCollection)
     - [<span data-ttu-id="905c6-145">Ressource RoleAssignment</span><span class="sxs-lookup"><span data-stu-id="905c6-145">RoleAssignment resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignment)
     - [<span data-ttu-id="905c6-146">Ressource RoleDefinitionCollection</span><span class="sxs-lookup"><span data-stu-id="905c6-146">RoleDefinitionCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinitionCollection)
     - [<span data-ttu-id="905c6-147">Ressource RoleDefinition</span><span class="sxs-lookup"><span data-stu-id="905c6-147">RoleDefinition resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinition)
    
 
- <span data-ttu-id="905c6-148">TechNet-Artikel:</span><span class="sxs-lookup"><span data-stu-id="905c6-148">TechNet articles:</span></span>
     - [<span data-ttu-id="905c6-149">Referenz zu abgestimmten Berechtigungen für SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="905c6-149">Fine-grained permission reference for SharePoint Server 2013</span></span>](http://technet.microsoft.com/en-us/library/dn169567.aspx)
     - [<span data-ttu-id="905c6-150">Bewährte Methoden für die Verwendung abgestimmter Berechtigungen in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="905c6-150">Best practices for using fine-grained permissions in SharePoint Server 2013</span></span>](http://technet.microsoft.com/en-us/library/gg128955.aspx)
     - [<span data-ttu-id="905c6-151">Benutzerberechtigungen und Berechtigungsstufen in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="905c6-151">User permissions and permission levels in SharePoint 2013</span></span>](http://technet.microsoft.com/en-us/library/cc721640.aspx)
    
 

