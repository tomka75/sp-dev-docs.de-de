---
title: Vorgehensweise Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 236ebaf8-f92e-4192-9b51-0a9de0210885
ms.openlocfilehash: b825ec245435a9d172c8fdc8064be7d92b0de38f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="24345-102">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-102">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="24345-103">In diesem Artikel erfahren Sie, wie Sie Benutzerprofileigenschaften programmgesteuert mithilfe des .NET-Clientobjektmodells in SharePoint abrufen.</span><span class="sxs-lookup"><span data-stu-id="24345-103">Learn how to retrieve user profile properties programmatically by using the SharePoint .NET client object model.</span></span>
## <a name="what-are-user-profile-properties-in-sharepoint"></a><span data-ttu-id="24345-104">Was sind Benutzerprofileigenschaften in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="24345-104">What are user profile properties in SharePoint?</span></span>
<span data-ttu-id="24345-105"><a name="bkmk_WhatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-105"></span></span>

<span data-ttu-id="24345-p101">Benutzereigenschaften und Benutzerprofileigenschaften liefern Informationen zu SharePoint-Benutzern, wie beispielsweise Anzeigename, E-Mail-Adresse, Titel sowie weitere geschäftliche und persönliche Daten. In clientseitigen APIs greifen Sie auf diese Eigenschaften über das  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) -Objekt und seine [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) -Eigenschaft zu. Die [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) -Eigenschaft enthält alle Benutzerprofileigenschaften, aber das [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) -Objekt enthält alle normalerweise verwendeten Eigenschaften (wie beispielsweise [AccountName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx) , [DisplayName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx) und [Email](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx) ), auf die einfacher zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="24345-p101">User properties and user profile properties provide information about SharePoint users, such as display name, email, title, and other business and personal information. In client-side APIs, you access these properties from the  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object and its [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) property. The [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) property contains all user profile properties, but the [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object contains commonly used properties (such as [AccountName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx) , [DisplayName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx) , and [Email](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx) ) that are easier to access.</span></span>
  
    
    
<span data-ttu-id="24345-109">Das  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) -Objekt enthält die folgenden Methoden zum Abrufen von Benutzereigenschaften und Benutzerprofileigenschaften über das .NET-Clientobjektmodell:</span><span class="sxs-lookup"><span data-stu-id="24345-109">The  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) object includes the following methods that you can use to retrieve user properties and user profile properties by using the .NET client object model:</span></span>
  
    
    

- <span data-ttu-id="24345-110">Die  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) -Methode und die [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) -Methode geben ein [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) -Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="24345-110">The  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) method and the [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) method return a [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object.</span></span>
    
  
- <span data-ttu-id="24345-111">Die  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) -Methode und die [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) -Methode geben die von Ihnen eingegebenen Werte der Benutzerprofileigenschaften zurück.</span><span class="sxs-lookup"><span data-stu-id="24345-111">The  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) method and the [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) method return the values of the user profile properties that you specify.</span></span>
    
  
<span data-ttu-id="24345-p102">Benutzerprofileigenschaften aus Client-APIs sind schreibgeschützt (mit Ausnahme des Profilbilds, das Sie mithilfe der  [PeopleManager.SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) -Methode ändern können). Wenn Sie andere Benutzerprofileigenschaften ändern möchten, müssen Sie das Serverobjektmodell verwenden.</span><span class="sxs-lookup"><span data-stu-id="24345-p102">User profile properties from client APIs are read-only (except the profile picture, which you can change by using the  [PeopleManager.SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) method). If you want to change other user profile properties, you must use the server object model.</span></span>
  
    
    

> <span data-ttu-id="24345-114">**Hinweis:** Die Clientversion des [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx)-Objekts enthält im Gegensatz zur serverseitigen Version nicht alle Benutzereigenschaften.</span><span class="sxs-lookup"><span data-stu-id="24345-114">**Note:** The client version of the  [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) object doesn't contain all of the user properties as the server-side version.</span></span> <span data-ttu-id="24345-115">Allerdings stellt die clientseitige Version die Methoden zum Erstellen einer persönlichen Website für den aktuellen Benutzer bereit.</span><span class="sxs-lookup"><span data-stu-id="24345-115">However, the client-side version does provide the methods for creating a personal site for the current user.</span></span> <span data-ttu-id="24345-116">Zum Abrufen des clientseitigen [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx)-Objekts für den aktuellen Benutzer verwenden Sie die [ProfileLoader.GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx)-Methode.</span><span class="sxs-lookup"><span data-stu-id="24345-116">To retrieve the client-side [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) for the current user, use the [ProfileLoader.GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx) method.</span></span>
  
    
    

<span data-ttu-id="24345-117">Weitere Informationen zum Arbeiten mit Benutzerprofilen finden Sie unter  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="24345-117">For more information about working with profiles, see  [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="24345-118">Voraussetzungen für die Einrichtung der Entwicklungsumgebung zum Abrufen von Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="24345-118">Prerequisites for setting up your development environment to retrieve user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="24345-119"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-119"></span></span>

<span data-ttu-id="24345-120">Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Abrufen von Benutzerprofileigenschaften verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="24345-120">To create a console application that uses the .NET client object model to retrieve user profile properties, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="24345-121">SharePoint mit Profilen, die für den aktuellen Benutzer und einen Zielbenutzer erstellt wurden</span><span class="sxs-lookup"><span data-stu-id="24345-121">SharePoint Server 2013 with profiles created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="24345-122">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="24345-122">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="24345-123">Verbindungsberechtigungen **Vollzugriff** zum Zugriff auf die Benutzerprofildienst-Anwendung für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="24345-123">**Full Control** connection permissions to access the User Profile service application for the current user.</span></span>
    
  

> <span data-ttu-id="24345-124">**Hinweis:** Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die  [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="24345-124">**Note** If you're not developing on the computer that is running SharePoint Server 2013, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-the-console-application-that-retrieves-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="24345-125">Erstellen der Konsolenanwendung, die Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint abruft</span><span class="sxs-lookup"><span data-stu-id="24345-125">Create the console application that retrieves user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="24345-126"><a name="bk_RetrieveProps"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-126"></span></span>


1. <span data-ttu-id="24345-127">Öffnen Sie auf dem Entwicklungscomputer Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt** aus.</span><span class="sxs-lookup"><span data-stu-id="24345-127">On your development computer, open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="24345-128">Wählen Sie im Dialogfeld **Neues Projekt** in der Dropdownliste oben im Dialogfeld **.NET Framework 4.5** aus.</span><span class="sxs-lookup"><span data-stu-id="24345-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="24345-129">Wählen Sie in den Projektvorlage **Windows** und anschließend **Konsolenanwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="24345-129">From the project templates, choose **Windows**, and then choose **Console Application**.</span></span>
    
  
4. <span data-ttu-id="24345-130">Geben Sie für das Projekt den Namen UserProfilesCSOM an, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="24345-130">Name the project UserProfilesCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="24345-131">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="24345-131">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="24345-132">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="24345-132">**Microsoft.SharePoint.Client**</span></span>
  - <span data-ttu-id="24345-133">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="24345-133">**Microsoft.SharePoint.ClientRuntime**</span></span>  
  - <span data-ttu-id="24345-134">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="24345-134">Primary namespace:            **Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
  
6. <span data-ttu-id="24345-135">Definieren Sie in der **Main**-Methode Variablen für die Server-URL und den Benutzernamen, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="24345-135">In the **Main** method, define variables for the server URL and the target user name, as shown in the following code.</span></span>
    
```cs
const string serverUrl = "http://serverName/";
const string targetUser = "domainName\\\\userName";
```

   > <span data-ttu-id="24345-136">Hinweis: Ersetzen Sie unbedingt die Platzhalterwerte  `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="24345-136">Note Remember to replace the   and  placeholder values before you run the code.</span></span>

7. <span data-ttu-id="24345-137">Initialisieren Sie den SharePoint-Clientkontext, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="24345-137">Initialize the SharePoint client context, as shown in the following code.</span></span>
    
```cs
ClientContext clientContext = new ClientContext(serverUrl);
```

8. <span data-ttu-id="24345-138">Rufen Sie die Eigenschaften des Zielbenutzers aus dem **PeopleManager**-Objekt ab, wie im folgenden Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="24345-138">Get the target user's properties from the **PeopleManager** object, as shown in the following code.</span></span>
    
```cs
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);
```

   <span data-ttu-id="24345-p104">Das **personProperties**-Objekt ist ein Clientobjekt. Einige Clientobjekte enthalten erst Daten, nachdem sie initialisiert wurden. Beispielweise können Sie auf die Eigenschaftswerte des **personProperties**-Objekts zugreifen, nachdem dieses initialisiert wurde. Wenn Sie versuchen, auf eine Eigenschaft zuzugreifen, bevor sie initialisiert wurde, erhalten Sie eine **PropertyOrFieldNotInitializedException**-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="24345-p104">The **personProperties** object is a client object. Some client objects contain no data until they are initialized. For example, you cannot access the property values of the **personProperties** object until you initialize it. If you try to access a property before it is initialized, you receive a **PropertyOrFieldNotInitializedException** exception.</span></span>
    
  
9. <span data-ttu-id="24345-143">Zum Initialisieren des **personProperties**-Objekts registrieren Sie die Anforderung, die Sie ausführen möchten, und führen Sie die Anforderung dann auf dem Server aus, wie im folgenden Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="24345-143">To initialize the **personProperties** object, register the request that you want to run, and then run the request on the server, as shown in the following code.</span></span>
    
```cs
clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
clientContext.ExecuteQuery();
```

   <span data-ttu-id="24345-p105">Wenn Sie die **Load**-Methode (oder die **LoadQuery**-Methode) aufrufen, übergeben Sie das Objekt, das Sie abrufen oder ändern möchten. In diesem Beispiel werden durch den Aufruf der **Load**-Methode optionale Parameter zum Filtern der Anforderung übergeben. Bei den Parametern handelt es sich um lambda-Ausdrücke, die nur die **AccountName**-Eigenschaft und die **UserProfileProperties**-Eigenschaft des **personProperties**-Objekts anfordern.</span><span class="sxs-lookup"><span data-stu-id="24345-p105">When you call the **Load** method (or the **LoadQuery** method), you pass in the object that you want to retrieve or change. In this example, the call to the **Load** method passes in optional parameters to filter the request. The parameters are lambda expressions that request only the **AccountName** property and **UserProfileProperties** property of the **personProperties** object.</span></span>
    
   ><span data-ttu-id="24345-147">Tipp: Fordern Sie beim Aufruf der **Load**-Methode nur die Eigenschaften an, die Sie verwenden möchten, um den Netzwerkverkehr zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="24345-147">To reduce network traffic, request only the properties that you want to work with when you call the **Load** method. In addition, if you’re working with multiple objects, group multiple calls to the Load method when possible before you call the ExecuteQuery method.</span></span> <span data-ttu-id="24345-148">Wenn Sie mit mehreren Objekten arbeiten, gruppieren Sie mehrere Aufrufe der **Load**-Methode nach Möglichkeit vor dem Aufrufen der **ExecuteQuery**-Methode.</span><span class="sxs-lookup"><span data-stu-id="24345-148">TIP To reduce network traffic, request only the properties that you want to work with when you call the Load method. In addition, if you're working with multiple objects, group multiple calls to the **Load** method when possible before you call the **ExecuteQuery** method.</span></span>

10. <span data-ttu-id="24345-149">Durchlaufen Sie die Benutzerprofileigenschaften, und lesen Sie den Namen und den Wert jeder Eigenschaft, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="24345-149">Iterate through the user profile properties and read the name and value of each property, as shown in the following code.</span></span>
    
```cs
foreach (var property in personProperties.UserProfileProperties)
{
    Console.WriteLine(string.Format("{0}: {1}", 
        property.Key.ToString(), property.Value.ToString()));
}
```


## <a name="code-example-retrieving-all-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="24345-150">Codebeispiel: Abrufen sämtlicher Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-150">Code example: Retrieving all user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="24345-151"><a name="SP15UserProf_codeexample1"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-151"></span></span>

<span data-ttu-id="24345-152">Das folgende Codebeispiel zeigt, wie alle Benutzerprofileigenschaften eines Zielbenutzers abgerufen und durchlaufen werden, wie im  [vorherigen Verfahren](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="24345-152">The following code example shows how to retrieve and iterate through all the user profile properties of a target user, as described in the  [previous procedure](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps).</span></span>
  
    
    

> <span data-ttu-id="24345-153">**Hinweis:** Ersetzen Sie die Platzhalterwerte  `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="24345-153">**Note** Replace the  `http://serverName/` and `domainName\\\\userName` placeholder values before you run the code.</span></span>
  
    
    


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


## <a name="code-example-retrieving-user-profile-properties-of-people-who-are-following-me-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="24345-154">Codebeispiel: Abrufen von Benutzerprofileigenschaften von Personen, die mir folgen, mit dem SharePoint .NET-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="24345-154">Code example: Retrieving user profile properties of people who are following me by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="24345-155"><a name="SP15UserProfilescodeInApp"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-155"></span></span>

<span data-ttu-id="24345-156">Im folgenden Codebeispiel wird gezeigt, wie die Benutzerprofileigenschaften von Personen in einer SharePoint-Add-In abgerufen werden können, die Ihnen folgen.</span><span class="sxs-lookup"><span data-stu-id="24345-156">The following code example shows how to get, in a SharePoint Add-in, the user profile properties of people who are following you.</span></span>
  
    
    

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


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="24345-157">Codebeispiel: Abrufen einer Gruppe von Benutzerprofileigenschaften über das .NET-Clientobjektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-157">Code example: Retrieving a set of user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="24345-158"><a name="SP15UserProfilescode2"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-158"></span></span>

<span data-ttu-id="24345-159">Das folgende Codebeispiel zeigt, wie eine bestimmte Gruppe von Benutzerprofileigenschaften für einen Zielbenutzer abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="24345-159">The following code example shows how to retrieve a specific set of user profile properties for a target user.</span></span>
  
    
    

> <span data-ttu-id="24345-160">**Hinweis:** Um nur den Wert für eine einzige Benutzerprofileigenschaft abzurufen, verwenden Sie die  [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx)-Methode.</span><span class="sxs-lookup"><span data-stu-id="24345-160">**Note** To retrieve the value for only one user profile property, use the  [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) method.</span></span>
  
    
    

<span data-ttu-id="24345-p107">Anders als in dem vorherigen Codebeispiel, bei dem ein  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) -Objekt für den Zielbenutzer abgerufen wird, wird mit diesem Beispiel die [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) -Methode aufgerufen und ein [UserProfilePropertiesForUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx) -Objekt übergeben, das den Zielbenutzer und die Benutzerprofileigenschaften angibt, die abgerufen werden sollen. [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) gibt eine **IEnumerable<string>**-Auflistung zurück, die die Werte der von Ihnen angegebenen Eigenschaften enthält.</span><span class="sxs-lookup"><span data-stu-id="24345-p107">Unlike the previous code example that retrieves a  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object for the target user, this example calls the [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) method and passes in a [UserProfilePropertiesForUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx) object that specifies the target user and the user profile properties to retrieve. [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) returns an **IEnumerable<string>** collection that contains the values of the properties that you specify.</span></span>
  
    
    

> <span data-ttu-id="24345-163">**Hinweis:** Ersetzen Sie die Platzhalterwerte  `http://serverName/` und `domainName\\\\userName`, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="24345-163">**Note** Replace the  `http://serverName/` and `domainName\\\\userName` placeholder values before you run the code.</span></span>
  
    
    




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


## <a name="additional-resources"></a><span data-ttu-id="24345-164">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="24345-164">Additional resources</span></span>
<span data-ttu-id="24345-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="24345-165"></span></span>


-  [<span data-ttu-id="24345-166">Arbeiten mit Benutzerprofilen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-166">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="24345-167">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-167">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [<span data-ttu-id="24345-168">Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24345-168">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  <span data-ttu-id="24345-169">[Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)</span><span class="sxs-lookup"><span data-stu-id="24345-169">Primary namespace:            [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)</span></span>
    
  

