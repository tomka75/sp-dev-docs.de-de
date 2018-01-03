---
title: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 236ebaf8-f92e-4192-9b51-0a9de0210885
ms.openlocfilehash: 8ff2bf5802099c70f60cf362916659af1c657a8b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="retrieve-user-profile-properties-by-using-the-net-client-object-model-in-sharepoint"></a>Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint

In diesem Artikel erfahren Sie, wie Sie Benutzerprofileigenschaften programmgesteuert mithilfe des .NET-Clientobjektmodells in SharePoint abrufen.

## <a name="what-are-user-profile-properties-in-sharepoint"></a>Was sind Benutzerprofileigenschaften in SharePoint?
<a name="bkmk_WhatIs"> </a>

Benutzereigenschaften und Benutzerprofileigenschaften liefern Informationen zu SharePoint-Benutzern, wie beispielsweise Anzeigename, E-Mail-Adresse, Titel sowie weitere geschäftliche und persönliche Daten. In clientseitigen APIs greifen Sie auf diese Eigenschaften über das  [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) -Objekt und seine [UserProfileProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx)) -Eigenschaft zu. Die [UserProfileProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx)) -Eigenschaft enthält alle Benutzerprofileigenschaften, aber das [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) -Objekt enthält alle normalerweise verwendeten Eigenschaften (wie beispielsweise [AccountName]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx)) , [DisplayName]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx)) und [Email]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx)) ), auf die einfacher zugegriffen werden kann.
  
    
    
Das  [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx)) -Objekt enthält die folgenden Methoden zum Abrufen von Benutzereigenschaften und Benutzerprofileigenschaften über das .NET-Clientobjektmodell:
  
    
    

- Die  [GetMyProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx)) -Methode und die [GetPropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx)) -Methode geben ein [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) -Objekt zurück.
    
  
- Die  [GetUserProfilePropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx)) -Methode und die [GetUserProfilePropertyFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx)) -Methode geben die von Ihnen eingegebenen Werte der Benutzerprofileigenschaften zurück.
    
  
Benutzerprofileigenschaften aus Client-APIs sind schreibgeschützt (mit Ausnahme des Profilbilds, das Sie mithilfe der  [PeopleManager.SetMyProfilePicture]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx)) -Methode ändern können). Wenn Sie andere Benutzerprofileigenschaften ändern möchten, müssen Sie das Serverobjektmodell verwenden.
  
> [!NOTE]
> Die Clientversion des [UserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx))-Objekts enthält im Gegensatz zur serverseitigen Version nicht alle Benutzereigenschaften. Allerdings stellt die clientseitige Version die Methoden zum Erstellen einer persönlichen Website für den aktuellen Benutzer bereit. Zum Abrufen des clientseitigen [UserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx))-Objekts für den aktuellen Benutzer verwenden Sie die [ProfileLoader.GetUserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx))-Methode.
  
    
    

Weitere Informationen zum Arbeiten mit Benutzerprofilen finden Sie unter  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md).
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Voraussetzungen für die Einrichtung der Entwicklungsumgebung zum Abrufen von Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint.
<a name="bk_Prereqs"> </a>

Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Abrufen von Benutzerprofileigenschaften verwendet, benötigen Sie Folgendes:
  
    
    

- SharePoint mit Profilen, die für den aktuellen Benutzer und einen Zielbenutzer erstellt wurden
    
  
- Visual Studio 2012
    
  
- Verbindungsberechtigungen **Vollzugriff** zum Zugriff auf die Benutzerprofildienst-Anwendung für den aktuellen Benutzer.
    
> [!NOTE]
> Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.
  
    
    


## <a name="create-the-console-application-that-retrieves-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Erstellen der Konsolenanwendung, die Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint abruft
<a name="bk_RetrieveProps"> </a>


1. Öffnen Sie auf dem Entwicklungscomputer Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt** aus.
    
  
2. Wählen Sie im Dialogfeld **Neues Projekt** in der Dropdownliste oben im Dialogfeld **.NET Framework 4.5** aus.
    
  
3. Wählen Sie in den Projektvorlage **Windows** und anschließend **Konsolenanwendung** aus.
    
  
4. Geben Sie für das Projekt den Namen UserProfilesCSOM an, und klicken Sie dann auf **OK**.
    
  
5. Fügen Sie Verweise auf die folgenden Assemblys hinzu:
    
  - **Microsoft.SharePoint.Client**
  - **Microsoft.SharePoint.ClientRuntime**  
  - **Microsoft.SharePoint.Client.UserProfiles**
    
  
6. Definieren Sie in der **Main**-Methode Variablen für die Server-URL und den Benutzernamen, wie im folgenden Code dargestellt.
    
```cs
const string serverUrl = "http://serverName/";
const string targetUser = "domainName\\\\userName";
```

   > Hinweis: Ersetzen Sie unbedingt die Platzhalterwerte  `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.

7. Initialisieren Sie den SharePoint-Clientkontext, wie im folgenden Code dargestellt.
    
```cs
ClientContext clientContext = new ClientContext(serverUrl);
```

8. Rufen Sie die Eigenschaften des Zielbenutzers aus dem **PeopleManager**-Objekt ab, wie im folgenden Code gezeigt.
    
```cs
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);
```

   Das **personProperties**-Objekt ist ein Clientobjekt. Einige Clientobjekte enthalten erst Daten, nachdem sie initialisiert wurden. Beispielweise können Sie auf die Eigenschaftswerte des **personProperties**-Objekts zugreifen, nachdem dieses initialisiert wurde. Wenn Sie versuchen, auf eine Eigenschaft zuzugreifen, bevor sie initialisiert wurde, erhalten Sie eine **PropertyOrFieldNotInitializedException**-Ausnahme.
    
  
9. Zum Initialisieren des **personProperties**-Objekts registrieren Sie die Anforderung, die Sie ausführen möchten, und führen Sie die Anforderung dann auf dem Server aus, wie im folgenden Code gezeigt.
    
```cs
clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
clientContext.ExecuteQuery();
```

   Wenn Sie die **Load**-Methode (oder die **LoadQuery**-Methode) aufrufen, übergeben Sie das Objekt, das Sie abrufen oder ändern möchten. In diesem Beispiel werden durch den Aufruf der **Load**-Methode optionale Parameter zum Filtern der Anforderung übergeben. Bei den Parametern handelt es sich um lambda-Ausdrücke, die nur die **AccountName**-Eigenschaft und die **UserProfileProperties**-Eigenschaft des **personProperties**-Objekts anfordern.
    
   >Tipp: Fordern Sie beim Aufruf der **Load**-Methode nur die Eigenschaften an, die Sie verwenden möchten, um den Netzwerkverkehr zu reduzieren. Wenn Sie mit mehreren Objekten arbeiten, gruppieren Sie mehrere Aufrufe der **Load**-Methode nach Möglichkeit vor dem Aufrufen der **ExecuteQuery**-Methode.

10. Durchlaufen Sie die Benutzerprofileigenschaften, und lesen Sie den Namen und den Wert jeder Eigenschaft, wie im folgenden Code dargestellt.
    
```cs
foreach (var property in personProperties.UserProfileProperties)
{
    Console.WriteLine(string.Format("{0}: {1}", 
        property.Key.ToString(), property.Value.ToString()));
}
```


## <a name="code-example-retrieving-all-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen sämtlicher Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint
<a name="SP15UserProf_codeexample1"> </a>

Das folgende Codebeispiel zeigt, wie alle Benutzerprofileigenschaften eines Zielbenutzers abgerufen und durchlaufen werden, wie im  [vorherigen Verfahren](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps) beschrieben.
  
> [!NOTE]
> Ersetzen Sie die Platzhalterwerte `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace UserProfilesCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target SharePoint site and
            // target user.
            const string serverUrl = "http://serverName/";  
            const string targetUser = "domainName\\\\userName";  

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the PeopleManager object and then get the target user's properties.
            PeopleManager peopleManager = new PeopleManager(clientContext);
            PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);

            // Load the request and run it on the server.
            // This example requests only the AccountName and UserProfileProperties
            // properties of the personProperties object.
            clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
            clientContext.ExecuteQuery();

            foreach (var property in personProperties.UserProfileProperties)
            {
                Console.WriteLine(string.Format("{0}: {1}", 
                    property.Key.ToString(), property.Value.ToString()));
            }
            Console.ReadKey(false);

            // TODO: Add error handling and input validation.
        }
    }
}
```


## <a name="code-example-retrieving-user-profile-properties-of-people-who-are-following-me-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen von Benutzerprofileigenschaften von Personen, die mir folgen, mit dem SharePoint .NET-Clientobjektmodell
<a name="SP15UserProfilescodeInApp"> </a>

Im folgenden Codebeispiel wird gezeigt, wie die Benutzerprofileigenschaften von Personen in einer SharePoint-Add-In abgerufen werden können, die Ihnen folgen.
  
    
    

```cs

string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

if (contextTokenString != null)
{
    Uri sharepointUrl = new Uri(Request.QueryString["SP.Url"]);

    ClientContext clientContext = TokenHelper.GetClientContextWithContextToken(sharepointUrl.ToString(), contextTokenString, Request.Url.Authority);

    PeopleManager peopleManager = new PeopleManager(clientContext);
    ClientObjectList<PersonProperties> peopleFollowedBy = peopleManager.GetMyFollowers();
    clientContext.Load(peopleFollowedBy, people => people.Include(person => person.PictureUrl, person => person.DisplayName));
    clientContext.ExecuteQuery();

    foreach (PersonProperties personFollowedBy in peopleFollowedBy)
    {
        if (!string.IsNullOrEmpty(personFollowedBy.PictureUrl))
        {
        Response.Write("<img src=\\"" + personFollowedBy.PictureUrl + "\\" alt=\\"" + personFollowedBy.DisplayName + "\\"/>");
        }
    }
    clientContext.Dispose();
}
```


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen einer Gruppe von Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint
<a name="SP15UserProfilescode2"> </a>

Das folgende Codebeispiel zeigt, wie eine bestimmte Gruppe von Benutzerprofileigenschaften für einen Zielbenutzer abgerufen wird.
  
> [!NOTE]
> Um nur den Wert für eine einzige Benutzerprofileigenschaft abzurufen, verwenden Sie die [GetUserProfilePropertyFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx))-Methode.
  
    
    

Anders als in dem vorherigen Codebeispiel, bei dem ein  [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) -Objekt für den Zielbenutzer abgerufen wird, wird mit diesem Beispiel die [PeopleManager.GetUserProfilePropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx)) -Methode aufgerufen und ein [UserProfilePropertiesForUser]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx)) -Objekt übergeben, das den Zielbenutzer und die Benutzerprofileigenschaften angibt, die abgerufen werden sollen. [GetUserProfilePropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx)) gibt eine **IEnumerable<string>**-Auflistung zurück, die die Werte der von Ihnen angegebenen Eigenschaften enthält.
  
> [!NOTE]
> Ersetzen Sie die Platzhalterwerte `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace UserProfilesCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target SharePoint site and the
            // target user.
            const string serverUrl = "http://serverName/";  
            const string targetUser = "domainName\\\\userName";  

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the PeopleManager object.
            PeopleManager peopleManager = new PeopleManager(clientContext);

            // Retrieve specific properties by using the GetUserProfilePropertiesFor method. 
            // The returned collection contains only property values.
            string[] profilePropertyNames = new string[] { "PreferredName", "Department", "Title" };
            UserProfilePropertiesForUser profilePropertiesForUser = new UserProfilePropertiesForUser(
                clientContext, targetUser, profilePropertyNames);
            IEnumerable<string> profilePropertyValues = peopleManager.GetUserProfilePropertiesFor(profilePropertiesForUser);

            // Load the request and run it on the server.
            clientContext.Load(profilePropertiesForUser);
            clientContext.ExecuteQuery();

            // Iterate through the property values.
            foreach (var value in profilePropertyValues)
            {
                Console.Write(value + "\\n");
            }
            Console.ReadKey(false);

            // TO DO: Add error handling and input validation.
        }
    }
}

```


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  
-  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [Microsoft.SharePoint.Client.UserProfiles]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx))
    
  

