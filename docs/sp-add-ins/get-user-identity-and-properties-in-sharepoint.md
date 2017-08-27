# <a name="get-user-identity-and-properties-in-sharepoint"></a>Abrufen von Benutzeridentitäten und Eigenschaften in SharePoint
Rufen Sie die Benutzeridentität und Benutzerinformationen in SharePoint ab.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Je nachdem, welche Informationen Sie abrufen möchten, können Benutzeridentität und Benutzerinformationen auf verschiedene Weise abgerufen werden. In diesem Artikel werden einige Möglichkeiten gezeigt.
 

## <a name="prerequisites-for-retrieving-user-identity-and-properties"></a>Voraussetzungen zum Abrufen von Benutzeridentitäten und Eigenschaften
<a name="Prereq"> </a>


- Bereiten Sie Ihre Add-In-Entwicklungsumgebung wie in [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins) beschrieben vor.
    
 
- Installieren Sie Visual Studio.
    
 
- Installieren Sie die aktuelle Version von [Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder [Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).
    
 

 **Hinweis** Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins).
 


### <a name="core-concepts-to-know-for-retrieving-user-identity-and-properties"></a>Kernkonzepte, die Ihnen beim Abrufen von Benutzeridentitäten und Eigenschaften bekannt sein sollten

In der folgenden Tabelle werden einige hilfreiche Artikel aufgelistet, in denen die relevanten Konzepte für das Erstellen von SharePoint-Add-Ins erläutert werden.
 

 


|** Artikel **|**Beschreibung**|
|:-----|:-----|
| [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint-2013)|Dieser Artikel enthält Informationen zu Add-In-Berechtigungen in SharePoint, zu Typen von Add-In-Berechtigungen, Berechtigungsanforderungsbereichen und der Verwaltung von Berechtigungen. Zudem werden in diesem Artikel die Unterschiede zwischen Add-In-Berechtigungsrechten und Benutzerrechten besprochen.|
| [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In](context-token-oauth-flow-for-sharepoint-add-ins)|In diesem Artikel wird der OAuth-Authentifizierungs- und -Autorisierungsablauf für in der Cloud gehostete Add-Ins erläutert.|
| [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins)|In diesem Artikel erfahren Sie, wie Sie eine grundlegende von einem Anbieter gehostete SharePoint-Add-In mit Office Developer Tools für Visual Studio 2012 erstellen, wie Sie unter Verwendung des SharePoint-CSOM mit Microsoft SharePoint-Sites interagieren und wie Sie OAuth in einer SharePoint-Add-In implementieren.|

## <a name="retrieving-current-website-user-identity"></a>Abrufen der Identität des aktuellen Websitebenutzers
<a name="WebsiteUserID"> </a>

Die einfachste Möglichkeit, die Identität des aktuellen Benutzers einer Website abzurufen, bietet das **Web**-Objekt. Wenn Ihr Projekt die Datei „TokenHelper.cs“ enthält, können Sie mithilfe des folgenden Codeausschnitts die Identität des aktuellen Websitebenutzers abrufen.
 

 

```C#
ClientContext clientContext =
                    TokenHelper.GetClientContextWithAccessToken(
                        sharepointUrl.ToString(), accessToken);
 
 
            //Load the properties for the Web object.
            Web web = clientContext.Web;
            clientContext.Load(web);
            clientContext.ExecuteQuery();
 
            //Get the site name.
            siteName = web.Title;
 
            //Get the current user.
            clientContext.Load(web.CurrentUser);
            clientContext.ExecuteQuery();
            currentUser = clientContext.Web.CurrentUser.LoginName;

```


- Wenn Sie Office 365 verwenden, erhalten Sie einen Anmeldename ähnlich `i:0#.f|membership|adam@contoso.com`.
    
 
- Wenn Sie Microsoft SharePoint lokal einsetzen und sich der Benutzer über NTLM als normaler Benutzer angemeldet hat, dann erhalten Sie einen Anmeldenamen wie  `i:0#.w|contoso\adam`.
    
 
- Wenn Sie SharePoint lokal verwenden und der Benutzer mit einem Farmkonto angemeldet ist, erhalten Sie einen Anmeldenamen wie `SHAREPOINT\System`.
    
 

## <a name="retrieving-user-identity-using-the-resolveprincipal-method"></a>Abrufen der Benutzeridentitäten mithilfe der ResolvePrincipal-Methode
<a name="ResolvePrincipal"> </a>

Nachfolgend wird eine andere Möglichkeit zum Abrufen des Anmeldenamens des Benutzers beschrieben. Wenn Sie die E-Mail-Adresse oder den Anzeigenamen des Benutzers kennen, können Sie mit der  **ResolvePrincipal** -Methode den Anmeldenamen des Benutzers abrufen.
 

 

 **Hinweis** Die APIs befinden sich im Namespace „Microsoft.SharePoint.Client.Utilities“ in der Assembly [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx).
 

Nachfolgend finden Sie einen Beispielcode, anhand dessen erläutert wird, wie Sie die Anmeldeinformationen des Benutzers abrufen.
 

 



```C#
ClientResult<Microsoft.SharePoint.Client.Utilities.PrincipalInfo> persons = Microsoft.SharePoint.Client.Utilities.Utility.ResolvePrincipal(clientContext, clientContext.Web, <email>, Microsoft.SharePoint.Client.Utilities.PrincipalType.User, Microsoft.SharePoint.Client.Utilities.PrincipalSource.All, null, true);
                    clientContext.ExecuteQuery();
                    Microsoft.SharePoint.Client.Utilities.PrincipalInfo person = persons.Value;

```

Der Wert **Person.LoginName** enthält die Anmeldeinformationen
 

 

## <a name="retrieving-user-identity-and-profile-properties"></a>Abrufen von Benutzeridentität und Profileigenschaften
<a name="Profile"> </a>

Wenn Sie die Identität und die Eigenschaften des Benutzers abrufen möchten, können Sie das OAuth-Token und APIs für soziale Funktionen verwenden. Rufen Sie zuerst das OAuth-Token ab, und legen Sie es auf den Clientkontext fest. Im folgenden Beispielcode wird gezeigt, wie Benutzerprofileigenschaften abgerufen werden.
 

 

```C#

ClientContext clientContext = new ClientContext(<sharepointurl>);
clientContext.AuthenticationMode = ClientAuthenticationMode.Anonymous;
clientContext.FormDigestHandlingEnabled = false;
clientContext.ExecutingWebRequest +=
delegate(object oSender, WebRequestEventArgs webRequestEventArgs)
{                      
    webRequestEventArgs.WebRequestExecutor.RequestHeaders["Authorization"] =
        "Bearer " + accessToken;
};

```

Verwenden Sie dann die API **UserProfilesPeopleManager**, um die Eigenschaften des Benutzers abzurufen, der das Add-In verwendet.
 

 



```C#

PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personDetails = peopleManager.GetMyProperties();
clientContext.Load(personDetails, personsD => personsD.AccountName, personsD => personsD.Email,  personsD => personsD.DisplayName);
                clientContext.ExecuteQuery();

```

Damit der Code funktioniert, müssen folgende Voraussetzungen erfüllt sein:
 

 

- Der gemeinsame Benutzerprofildienst muss in SharePoint für die Benutzer konfiguriert und synchronisiert werden.
    
 
- Sie müssen dem Add-In-Manifest den folgenden Berechtigungsbereich für soziale Funktionen hinzufügen:
    
```XML
  <AppPermissionRequest Right="Read" Scope="http://sharepoint/social/tenant" />

```

Die APIs befinden sich in „Microsoft.SharePoint.Client.UserProfiles.dll“.
 

 
Es folgt ein weiterer Codeausschnitt, der zeigt, wie auf den Benutzerprofilspeicher zugegriffen wird.
 

 



```C#

ClientContext clientContext; //Create this like you normally would.               
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties myProperties = peopleManager.GetMyProperties();
clientContext.Load(myProperties);
clientContext.ExecuteQuery();

```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AdditionalResources"> </a>


-  [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint-2013)
    
 
-  [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [SharePoint-Add-Ins](sharepoint-add-ins)
    
 
-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 

