---
title: Vorgehensweise Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6e1ca38-134f-428a-8d21-b8b2615b161b
ms.openlocfilehash: a308df72d1aa24e853b38a5dacf4b7f8d1a21e3b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in-sharepoint"></a>Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint
Informationen zum programmtechnischen Abrufen von Benutzereigenschaften und Benutzerprofileigenschaften über das SharePoint JavaScript-Objektmodell.
## <a name="what-are-user-properties-and-user-profile-properties-in-sharepoint"></a>Was sind Benutzereigenschaften und Benutzerprofileigenschaften in SharePoint?
<a name="bkmk_WhatIs"> </a>

Benutzereigenschaften und Benutzerprofileigenschaften liefern Informationen über SharePoint-Benutzer, wie Anzeigename, E-Mail, Titel und andere geschäftliche oder persönliche Daten. In clientseitigen APIs greifen Sie auf diese Eigenschaften über das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt und seine  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft zu. Die  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft enthält alle Benutzerprofileigenschaften, aber das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt beinhaltet die normalerweise verwendeten Eigenschaften (wie  [accountName](http://msdn.microsoft.com/library/ad1551bf-dad8-d54e-880a-8a4388fad44e%28Office.15%29.aspx),  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx) und [email](http://msdn.microsoft.com/library/74302f73-aaf6-920b-0605-812b0dbf4568%28Office.15%29.aspx)), auf die leichter zugegriffen werden kann.
  
    
    
Das  [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx)-Objekt enthält die folgenden Methoden zum Abrufen von Benutzereigenschaften und Benutzerprofileigenschaften über das JavaScript-Objektmodell:
  
    
    

- Die  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx)-Methode und die  [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx)-Methode geben ein  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt zurück.
    
  
- Die  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode und die  [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx)-Methode geben die von Ihnen angegebenen Werte der Benutzerprofileigenschaften zurück.
    
  
Benutzerprofileigenschaften von Client-APIs sind schreibgeschützt (mit Ausnahme des Profilbilds, das Sie mithilfe der  [PeopleManager.setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx)-Methode ändern können). Wenn Sie weitere Benutzerprofileigenschaften ändern möchten, verwenden Sie das Serverobjektmodell. Weitere Informationen zum Arbeiten mit Benutzerprofilen finden Sie unter  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md).
  
    
    

> **Hinweis:** Das clientseitige [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx)-Objekt enthält im Gegensatz zur serverseitigen Version nicht alle Benutzereigenschaften. Allerdings stellt die clientseitige Version die Methoden zum Erstellen einer persönlichen Website für den aktuellen Benutzer bereit. Verwenden Sie zum Abrufen die [ProfileLoader.getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx)-Methode.
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-properties-by-using-the-sharepoint-javascript-object-model"></a>Voraussetzungen für das Einrichten der Entwicklungsumgebung zum Abrufen von Benutzereigenschaften über das SharePoint JavaScript-Objektmodell
<a name="bk_Prereqs"> </a>

Um eine Anwendungsseite zu erstellen, die das JavaScript-Objektmodell zum Abrufen von Benutzereigenschafen verwendet, benötigen Sie Folgendes:
  
    
    

- SharePoint mit Profilen, die für den aktuellen Benutzer und einen Zielbenutzer erstellt wurden
    
  
- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2013
    
  
- Verbindungsberechtigungen für den **Vollzugriff**, um auf die Benutzerprofildienst-Anwendung für den aktuellen Benutzer zugreifen zu können
    
  

## <a name="create-the-application-page-in-visual-studio-2012"></a>Erstellen der Anwendungsseite in Visual Studio 2012
<a name="bk_CreateAppPage"> </a>


1. Öffnen Sie auf dem Server, auf dem SharePoint ausgeführt wird, Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.
    
  
2. Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.
    
  
3. Erweitern Sie in der Liste **Vorlagen** das Element **Office/SharePoint**, wählen Sie die Kategorie **SharePoint-Lösungen** und dann die Vorlage **SharePoint-Projekt**.
    
  
4. Benennen Sie das Projekt mit UserProfilesJSOM, und klicken Sie dann auf **OK**.
    
  
5. Geben Sie im Dialogfeld **Assistent zum Anpassen von SharePoint** die URL zu Ihrer Ziel-SharePoint-Website, wählen Sie **Als Farmlösung bereitstellen**, und klicken Sie dann auf **Fertig stellen**.
    
  
6. Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für dasUserProfilesJSOM-Projekt, und fügen Sie dann einen zugeordneten SharePoint-Ordner "Layouts" hinzu.
    
  
7. Öffnen Sie im Ordner **Layouts** das Kontextmenü für den Ordner „UserProfilesJSOM“, und fügen Sie anschließend eine neue SharePoint-Anwendungsseite mit dem Namen „UserProfiles.aspx“ hinzu.
    
   > Hinweis: Die Codebeispiele in diesem Artikel legen benutzerdefinierten Code im Seitenmarkup fest, verwenden aber nicht die Code-Behind Class-Datei, die Visual Studio für die Seite erstellt. 

8. Öffnen Sie das Kontextmenü für die Seite „UserProfiles.aspx“, und wählen Sie dann **Als Startelement festlegen** aus.
    
  
9. Fügen Sie in das Markup der Seite "UserProfiles.aspx" den folgenden Code zwischen die Haupt- **asp:Content**-Tags ein. Dieser Code fügt ein **span**-Steuerelement, das die Abfrageergebnisse anzeigt, **SharePoint:ScriptLink**-Steuerelemente, die SharePoint JavaScript Class-Bibliotheksdateien und **script**-Tags einfügt, die Ihre benutzerdefinierte Logik enthalten.
    
```HTML
<span id="results"></span><br />
<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server"
    ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server"
    ondemand="false" localizable="false" loadafterui="true" />
<script type="text/javascript">
    // Replace this comment with the code for your scenario.
</script>
```

10. Um Logik für das Abrufen von Benutzerprofileigenschaften hinzuzufügen, ersetzen Sie den Kommentar zwischen den **script**-Tags durch das Codebeispiel für eines der folgenden Szenarien:
    
  -  [Abrufen von Benutzerprofileigenschaften aus dem "PersonProperties"-Objekt und der "userProfileProperties"-Eigenschaft](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_examplePersonPropsObj)  
  -  [Abrufen einer Gruppe von Benutzerprofileigenschaften mithilfe der "getUserProfilePropertiesFor"-Methode](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_exampleGetUPMethod)
    
  
11. Um die Anwendungsseite zu testen, wählen Sie in der Menüleiste die Optionen **Debuggen**, **Debuggen starten**. Wenn Sie aufgefordert werden, die Datei "web.config" zu ändern, klicken Sie auf **OK**.
    
  

## <a name="code-example-retrieving-user-profile-properties-from-the-personproperties-object-and-its-userprofileproperties-property-in-the-sharepoint-javascript-object-model"></a>Codebeispiel: Abrufen von Benutzerprofileigenschaften aus dem "PersonProperties"-Objekt und der "userProfileProperties-Eigenschaft im SharePoint JavaScript-Objektmodell
<a name="bk_examplePersonPropsObj"> </a>

Das folgende Codebeispiel erklärt, wie Sie Benutzerprofileigenschaften für einen Zielbenutzer abrufen, indem Sie das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt und seine  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft anfordern. Es zeigt die Vorgehensweise:
  
    
    

- Rufen Sie das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt ab, das für den Zielbenutzer steht, indem Sie die  [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx)-Methode anwenden. (Zum Abrufen des  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekts für den aktuellen Benutzer verwenden Sie die  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx)-Methode.)
    
  
- Rufen Sie eine Eigenschaft direkt aus dem  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt ab. In diesem Beispiel wird die  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx)-Eigenschaft abgerufen.
    
  
- Erhalten Sie eine Eigenschaft von der [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft des [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekts. In diesem Beispiel wird die **Department**-Eigenschaft abgerufen.
    
  

> **Hinweis:** Fügen Sie den folgenden Code zwischen den **script**-Tags ein, den Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) zur UserProfiles.aspx-Seite hinzugefügt haben. Ersetzen Sie den `domainName\\userName`-Platzhalterwert, bevor Sie den Code ausführen. (In diesem Codebeispiel wird die Code-Behind Class-Datei nicht verwenden.)
  
    
    


```

var personProperties;

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js');

function getUserProperties() {

    // Replace the placeholder value with the target user's credentials.
    var targetUser = "domainName\\userName";

    // Get the current client context and PeopleManager instance.
    var clientContext = new SP.ClientContext.get_current();
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    // Get user properties for the target user.
    // To get the PersonProperties object for the current user, use the
    // getMyProperties method.
    personProperties = peopleManager.getPropertiesFor(targetUser);

    // Load the PersonProperties object and send the request.
    clientContext.load(personProperties);
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail);
}

// This function runs if the executeQueryAsync call succeeds.
function onRequestSuccess() {

    // Get a property directly from the PersonProperties object.
    var messageText = " \\"DisplayName\\" property is "
        + personProperties.get_displayName();

    // Get a property from the UserProfileProperties property.
    messageText += "<br />\\"Department\\" property is "
        + personProperties.get_userProfileProperties()['Department'];
    $get("results").innerHTML = messageText;
}

// This function runs if the executeQueryAsync call fails.
function onRequestFail(sender, args) {
    $get("results").innerHTML = "Error: " + args.get_message();
}
```


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-getuserprofilepropertiesfor-method-in-the-sharepoint-javascript-object-model"></a>Codebeispiel: Abrufen einer Gruppe von Benutzerprofileigenschaften mithilfe der „getUserProfilePropertiesFor“-Methode im SharePoint JavaScript-Objektmodell
<a name="bk_exampleGetUPMethod"> </a>

Im folgenden Codebeispiel werden die Werte einer bestimmten Gruppe von Benutzerprofileigenschaften für einen Zielbenutzer mithilfe der  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode abgerufen. Es zeigt die Vorgehensweise:
  
    
    

- Erstellen Sie ein  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx)-Objekt, das den Zielbenutzer und die abzurufenden Benutzerprofileigenschaften angibt. In diesem Beispiel werden die **PreferredName**-Eigenschaft und die **Department**-Eigenschaft abgerufen.
    
  
- Rufen Sie die Werte der angegebenen Eigenschaft mithilfe der  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode ab, und übergeben Sie die Werte an das  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx)-Objekt. (Zum Abrufen des Werts von nur einer Benutzerprofileigenschaft verwenden Sie die  [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx)-Methode.)
    
  
- Rufen Sie die Werte aus dem zurückgegebenen Array von Eigenschaftswerten ab.
    
  

> **Hinweis:** Fügen Sie den folgenden Code zwischen den **script**-Tags ein, den Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) zur UserProfiles.aspx-Seite hinzugefügt haben. Ersetzen Sie den `domainName\\\\userName`-Platzhalterwert, bevor Sie den Code ausführen. (In diesem Codebeispiel wird die Code-Behind Class-Datei nicht verwenden.)
  
    
    


```

var userProfileProperties;

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js');

function getUserProperties() {

    // Replace the placeholder value with the target user's credentials.
    var targetUser = "domainName\\\\userName";

    // Get the current client context and PeopleManager instance.
    var clientContext = new SP.ClientContext.get_current();
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    // Specify the properties to retrieve and target user for the 
    // UserProfilePropertiesForUser object.
    var profilePropertyNames = ["PreferredName", "Department"];
    var userProfilePropertiesForUser = 
        new SP.UserProfiles.UserProfilePropertiesForUser(
            clientContext,
            targetUser,
            profilePropertyNames);

    // Get user profile properties for the target user.
    // To get the value for only one user profile property, use the
    // getUserProfilePropertyFor method.
    userProfileProperties = peopleManager.getUserProfilePropertiesFor(
        userProfilePropertiesForUser);

    // Load the UserProfilePropertiesForUser object and send the request.
    clientContext.load(userProfilePropertiesForUser);
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail);
}

// This function runs if the executeQueryAsync call succeeds.
function onRequestSuccess() {
    var messageText = "\\"PreferredName\\" property is " 
        + userProfileProperties[0];
    messageText += "<br />\\"Department\\" property is " 
        + userProfileProperties[1];
    $get("results").innerHTML = messageText;
}

// This function runs if the executeQueryAsync call fails.
function onRequestFail(sender, args) {
    $get("results").innerHTML = "Error: " + args.get_message();
}
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  
-  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [SP.UserProfiles-Namespace (sp.userprofiles)](http://msdn.microsoft.com/library/8c1fcceb-cd9a-b25c-32f4-1cfb0578278c%28Office.15%29.aspx)
    
  

