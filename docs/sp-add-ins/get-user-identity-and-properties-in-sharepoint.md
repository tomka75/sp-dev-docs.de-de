---
title: "Abrufen von Benutzeridentitäten und Eigenschaften in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6bfca47eb63da2fe4351d93485f533a9e1c6eedf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-user-identity-and-properties-in-sharepoint"></a><span data-ttu-id="8977c-102">Abrufen von Benutzeridentitäten und Eigenschaften in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8977c-102">Get user identity and properties in SharePoint</span></span>
<span data-ttu-id="8977c-103">Rufen Sie die Benutzeridentität und Benutzerinformationen in SharePoint ab.</span><span class="sxs-lookup"><span data-stu-id="8977c-103">Retrieve user identity and user information in SharePoint.</span></span>
 

 <span data-ttu-id="8977c-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="8977c-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="8977c-p102">Je nachdem, welche Informationen Sie abrufen möchten, können Benutzeridentität und Benutzerinformationen auf verschiedene Weise abgerufen werden. In diesem Artikel werden einige Möglichkeiten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="8977c-p102">There are different ways to retrieve user identity and information, depending on what information you want to retrieve. This article shows you some of the ways you can accomplish that.</span></span>
 

## <a name="prerequisites-for-retrieving-user-identity-and-properties"></a><span data-ttu-id="8977c-109">Voraussetzungen zum Abrufen von Benutzeridentitäten und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="8977c-109">Prerequisites for retrieving user identity and properties</span></span>
<span data-ttu-id="8977c-110"><a name="Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="8977c-110"></span></span>


- <span data-ttu-id="8977c-111">Bereiten Sie Ihre Add-In-Entwicklungsumgebung wie in [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md) beschrieben vor.</span><span class="sxs-lookup"><span data-stu-id="8977c-111">Prepare your add-in development environment as described in  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).</span></span>
    
 
- <span data-ttu-id="8977c-112">Installieren Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8977c-112">Install Visual Studio.</span></span>
    
 
- <span data-ttu-id="8977c-113">Installieren Sie die aktuelle Version von [Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder [Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="8977c-113">Install the most recent version of  [Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) or [Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 

 <span data-ttu-id="8977c-114">**Hinweis** Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="8977c-114">**Note**  For guidance on how to setup a development environment that fits your needs, see  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
 


### <a name="core-concepts-to-know-for-retrieving-user-identity-and-properties"></a><span data-ttu-id="8977c-115">Kernkonzepte, die Ihnen beim Abrufen von Benutzeridentitäten und Eigenschaften bekannt sein sollten</span><span class="sxs-lookup"><span data-stu-id="8977c-115">Core concepts to know for retrieving user identity and properties</span></span>

<span data-ttu-id="8977c-116">In der folgenden Tabelle werden einige hilfreiche Artikel aufgelistet, in denen die relevanten Konzepte für das Erstellen von SharePoint-Add-Ins erläutert werden.</span><span class="sxs-lookup"><span data-stu-id="8977c-116">The following table lists some useful articles that can help you to understand the concepts involved in creating SharePoint Add-ins.</span></span>
 

 


|<span data-ttu-id="8977c-117">** Artikel **</span><span class="sxs-lookup"><span data-stu-id="8977c-117">**Article **</span></span>|<span data-ttu-id="8977c-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="8977c-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="8977c-119">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8977c-119">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)|<span data-ttu-id="8977c-p103">Dieser Artikel enthält Informationen zu Add-In-Berechtigungen in SharePoint, zu Typen von Add-In-Berechtigungen, Berechtigungsanforderungsbereichen und der Verwaltung von Berechtigungen. Zudem werden in diesem Artikel die Unterschiede zwischen Add-In-Berechtigungsrechten und Benutzerrechten besprochen.</span><span class="sxs-lookup"><span data-stu-id="8977c-p103">Learn about SharePoint add-in permissions for working with SharePoint, including types of add-in permissions, permission request scopes, and managing permissions. This article also discusses the differences in add-in permission rights, and user rights.</span></span>|
| [<span data-ttu-id="8977c-122">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8977c-122">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)|<span data-ttu-id="8977c-123">In diesem Artikel wird der OAuth-Authentifizierungs- und -Autorisierungsablauf für in der Cloud gehostete Add-Ins erläutert.</span><span class="sxs-lookup"><span data-stu-id="8977c-123">Learn about the OAuth authentication and authorization flow for cloud-hosted add-ins.</span></span>|
| [<span data-ttu-id="8977c-124">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8977c-124">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)|<span data-ttu-id="8977c-125">In diesem Artikel erfahren Sie, wie Sie eine grundlegende von einem Anbieter gehostete SharePoint-Add-In mit Office Developer Tools für Visual Studio 2012 erstellen, wie Sie unter Verwendung des SharePoint-CSOM mit Microsoft SharePoint-Sites interagieren und wie Sie OAuth in einer SharePoint-Add-In implementieren.</span><span class="sxs-lookup"><span data-stu-id="8977c-125">Learn how to create a basic provider-hosted SharePoint Add-in with the Office Developer Tools for Visual Studio 2012, how to interact with Microsoft SharePoint sites by using the SharePoint CSOM, and how to implement OAuth in a SharePoint Add-in.</span></span>|

## <a name="retrieving-current-website-user-identity"></a><span data-ttu-id="8977c-126">Abrufen der Identität des aktuellen Websitebenutzers</span><span class="sxs-lookup"><span data-stu-id="8977c-126">Retrieving current website user identity</span></span>
<span data-ttu-id="8977c-127"><a name="WebsiteUserID"> </a></span><span class="sxs-lookup"><span data-stu-id="8977c-127"></span></span>

<span data-ttu-id="8977c-p104">Die einfachste Möglichkeit, die Identität des aktuellen Benutzers einer Website abzurufen, bietet das **Web**-Objekt. Wenn Ihr Projekt die Datei „TokenHelper.cs“ enthält, können Sie mithilfe des folgenden Codeausschnitts die Identität des aktuellen Websitebenutzers abrufen.</span><span class="sxs-lookup"><span data-stu-id="8977c-p104">The easiest way to retrieve the identity of the current user of the website is via the  **Web** object. With the TokenHelper.cs file in your project, you can get the current website user identity using the following code snippet.</span></span>
 

 

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


- <span data-ttu-id="8977c-130">Wenn Sie Office 365 verwenden, erhalten Sie einen Anmeldename ähnlich `i:0#.f|membership|adam@contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8977c-130">If you are using Office 365, the login name you get is similar to  `i:0#.f|membership|adam@contoso.com`.</span></span>
    
 
- <span data-ttu-id="8977c-131">Wenn Sie Microsoft SharePoint lokal einsetzen und sich der Benutzer über NTLM als normaler Benutzer angemeldet hat, dann erhalten Sie einen Anmeldenamen wie  `i:0#.w|contoso\adam`.</span><span class="sxs-lookup"><span data-stu-id="8977c-131">If you are using Microsoft SharePoint on-premises and the user is logged in as a normal user using NTLM, the login name you get is similar to  `i:0#.w|contoso\adam`.</span></span>
    
 
- <span data-ttu-id="8977c-132">Wenn Sie SharePoint lokal verwenden und der Benutzer mit einem Farmkonto angemeldet ist, erhalten Sie einen Anmeldenamen wie `SHAREPOINT\System`.</span><span class="sxs-lookup"><span data-stu-id="8977c-132">If you are using SharePoint on-premises and the user is logged in using a farm account, the login name you get is  `SHAREPOINT\System`.</span></span>
    
 

## <a name="retrieving-user-identity-using-the-resolveprincipal-method"></a><span data-ttu-id="8977c-133">Abrufen der Benutzeridentitäten mithilfe der ResolvePrincipal-Methode</span><span class="sxs-lookup"><span data-stu-id="8977c-133">Retrieving user identity using the ResolvePrincipal method</span></span>
<span data-ttu-id="8977c-134"><a name="ResolvePrincipal"> </a></span><span class="sxs-lookup"><span data-stu-id="8977c-134"></span></span>

<span data-ttu-id="8977c-p105">Nachfolgend wird eine andere Möglichkeit zum Abrufen des Anmeldenamens des Benutzers beschrieben. Wenn Sie die E-Mail-Adresse oder den Anzeigenamen des Benutzers kennen, können Sie mit der  **ResolvePrincipal** -Methode den Anmeldenamen des Benutzers abrufen.</span><span class="sxs-lookup"><span data-stu-id="8977c-p105">The following is another way to retrieve user's login name. If you have the user's email address or display name, you can use the  **ResolvePrincipal** method to get the user's login name.</span></span>
 

 

 <span data-ttu-id="8977c-137">**Hinweis** Die APIs befinden sich im Namespace „Microsoft.SharePoint.Client.Utilities“ in der Assembly [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx).</span><span class="sxs-lookup"><span data-stu-id="8977c-137">**Note**  The APIs are in the Microsoft.SharePoint.Client.Utilities namespace in the  [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx) assembly.</span></span>
 

<span data-ttu-id="8977c-138">Nachfolgend finden Sie einen Beispielcode, anhand dessen erläutert wird, wie Sie die Anmeldeinformationen des Benutzers abrufen.</span><span class="sxs-lookup"><span data-stu-id="8977c-138">The following is sample code to show how to get the user login information.</span></span>
 

 



```C#
ClientResult<Microsoft.SharePoint.Client.Utilities.PrincipalInfo> persons = Microsoft.SharePoint.Client.Utilities.Utility.ResolvePrincipal(clientContext, clientContext.Web, <email>, Microsoft.SharePoint.Client.Utilities.PrincipalType.User, Microsoft.SharePoint.Client.Utilities.PrincipalSource.All, null, true);
                    clientContext.ExecuteQuery();
                    Microsoft.SharePoint.Client.Utilities.PrincipalInfo person = persons.Value;

```

<span data-ttu-id="8977c-139">Der Wert **Person.LoginName** enthält die Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="8977c-139">The  **Person.LoginName** value gives the login information.</span></span>
 

 

## <a name="retrieving-user-identity-and-profile-properties"></a><span data-ttu-id="8977c-140">Abrufen von Benutzeridentität und Profileigenschaften</span><span class="sxs-lookup"><span data-stu-id="8977c-140">Retrieving user identity and profile properties</span></span>
<span data-ttu-id="8977c-141"><a name="Profile"> </a></span><span class="sxs-lookup"><span data-stu-id="8977c-141"></span></span>

<span data-ttu-id="8977c-p106">Wenn Sie die Identität und die Eigenschaften des Benutzers abrufen möchten, können Sie das OAuth-Token und APIs für soziale Funktionen verwenden. Rufen Sie zuerst das OAuth-Token ab, und legen Sie es auf den Clientkontext fest. Im folgenden Beispielcode wird gezeigt, wie Benutzerprofileigenschaften abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="8977c-p106">If you want to retrieve the user's identity and properties, you can use the OAuth token and the social features APIs. First get the OAuth token and then set it to the client context. The following sample code shows how to get the user profile properties.</span></span>
 

 

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

<span data-ttu-id="8977c-145">Verwenden Sie dann die API **UserProfilesPeopleManager**, um die Eigenschaften des Benutzers abzurufen, der das Add-In verwendet.</span><span class="sxs-lookup"><span data-stu-id="8977c-145">Then, use the  **UserProfilesPeopleManager** API to get the properties of the user who is using the add-in.</span></span>
 

 



```C#

PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personDetails = peopleManager.GetMyProperties();
clientContext.Load(personDetails, personsD => personsD.AccountName, personsD => personsD.Email,  personsD => personsD.DisplayName);
                clientContext.ExecuteQuery();

```

<span data-ttu-id="8977c-146">Damit der Code funktioniert, müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="8977c-146">For the code to work:</span></span>
 

 

- <span data-ttu-id="8977c-147">Der gemeinsame Benutzerprofildienst muss in SharePoint für die Benutzer konfiguriert und synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="8977c-147">The user profile shared service should be configured and synced on SharePoint for the users.</span></span>
    
 
- <span data-ttu-id="8977c-148">Sie müssen dem Add-In-Manifest den folgenden Berechtigungsbereich für soziale Funktionen hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="8977c-148">You must add the following permission scope for social features in the add-in manifest:</span></span>
    
```XML
  <AppPermissionRequest Right="Read" Scope="http://sharepoint/social/tenant" />

```

<span data-ttu-id="8977c-149">Die APIs befinden sich in „Microsoft.SharePoint.Client.UserProfiles.dll“.</span><span class="sxs-lookup"><span data-stu-id="8977c-149">The APIs are in Microsoft.SharePoint.Client.UserProfiles.dll.</span></span>
 

 
<span data-ttu-id="8977c-150">Es folgt ein weiterer Codeausschnitt, der zeigt, wie auf den Benutzerprofilspeicher zugegriffen wird.</span><span class="sxs-lookup"><span data-stu-id="8977c-150">The following is another sample code snippet that shows how to access the user profile store.</span></span>
 

 



```C#

ClientContext clientContext; //Create this like you normally would.               
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties myProperties = peopleManager.GetMyProperties();
clientContext.Load(myProperties);
clientContext.ExecuteQuery();

```


## <a name="additional-resources"></a><span data-ttu-id="8977c-151">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8977c-151">Additional resources</span></span>
<span data-ttu-id="8977c-152"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="8977c-152"></span></span>


-  [<span data-ttu-id="8977c-153">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8977c-153">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)
    
 
-  [<span data-ttu-id="8977c-154">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="8977c-154">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="8977c-155">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8977c-155">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="8977c-156">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8977c-156">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="8977c-157">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8977c-157">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 

