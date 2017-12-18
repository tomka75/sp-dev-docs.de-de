---
title: Folgen von Dokumenten, Websites und Kategorien mithilfe des REST-Diensts in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 989a5873-49f9-49e4-8d0f-439dde891cc2
ms.openlocfilehash: 73796b89f04291d86072234833953c97881cdff8
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint"></a><span data-ttu-id="9433c-102">Folgen von Dokumenten, Websites und Kategorien mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9433c-102">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>

<span data-ttu-id="9433c-103">Erstellen Sie von SharePoint gehostete Apps, die den REST-Dienst verwenden, um Inhalten (Dokumente, Websites und Tags) zu folgen und gefolgte Inhalte zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="9433c-103">Create SharePoint-hosted apps that use the REST service to follow content (documents, sites, and tags) and to get followed content.</span></span>

## <a name="how-do-i-use-the-sharepoint-rest-service-to-follow-content"></a><span data-ttu-id="9433c-104">Wie verwende ich den REST-Dienst von SharePoint, um Inhalten zu folgen?</span><span class="sxs-lookup"><span data-stu-id="9433c-104">How do I use the SharePoint REST service to follow content?</span></span>
<span data-ttu-id="9433c-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="9433c-106">SharePoint-Benutzer können Dokumenten, Websites und Tags folgen, um Updates zu den Elementen in ihren Newsfeeds abzurufen und gefolgte Dokumente und Websites schnell zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="9433c-106">SharePoint users can follow documents, sites, and tags to get updates about the items in their newsfeeds and to quickly open followed documents and sites.</span></span> <span data-ttu-id="9433c-107">Sie können die REST-API von SharePoint verwenden, um mit dem Folgen von Inhalten zu beginnen, das Folgen von Inhalten zu beenden und gefolgte Inhalte im Auftrag des aktuellen Benutzers abzurufen.</span><span class="sxs-lookup"><span data-stu-id="9433c-107">You can use the SharePoint REST API in your app or solution to start following content, stop following content, and get followed content on behalf of the current user.</span></span>
  
    
    
<span data-ttu-id="9433c-108">Die folgenden RESET-Ressourcen sind die primären APIs für Aufgaben zum Folgen von Inhalten:</span><span class="sxs-lookup"><span data-stu-id="9433c-108">The following REST resources are the primary API for Following Content tasks:</span></span>
  
    
    

- <span data-ttu-id="9433c-109">**SocialRestFollowingManager** bietet Methoden zum Verwalten eines Benutzers Liste besuchter Akteure.</span><span class="sxs-lookup"><span data-stu-id="9433c-109">**SocialRestFollowingManager** provides methods for managing a user's list of followed actors.</span></span>
    
  
- <span data-ttu-id="9433c-110">**SocialActor** stellt ein Dokument, Website oder Tag, der der Server als Antwort auf eine Anforderung mithilfe der clientseitigen zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="9433c-110">**SocialActor** represents a document, site, or tag that the server returns in response to a client-side request.</span></span>
    
  
- <span data-ttu-id="9433c-111">**SocialActorInfo** gibt ein Dokument, Website oder Tag in clientseitige Anforderungen an den Server.</span><span class="sxs-lookup"><span data-stu-id="9433c-111">**SocialActorInfo** specifies a document, site, or tag in client-side requests to the server.</span></span>
    
  
- <span data-ttu-id="9433c-112">**SocialActorType** und **SocialActorTypes** angeben von Inhaltstypen in clientseitige Anforderungen an den Server.</span><span class="sxs-lookup"><span data-stu-id="9433c-112">**SocialActorType** and **SocialActorTypes** specify content types in client-side requests to the server.</span></span>
    
  
<span data-ttu-id="9433c-p102">Inhalt in der folgenden Aufgaben mithilfe der REST-API, senden Sie HTTP **GET** und HTTP- **POST** Anfragen an den REST-Dienst. REST Endpoint URIs Aufgaben zum folgenden Inhalt mit der Ressource **SocialRestFollowingManager** ( `<siteUri>/_api/social.following`) beginnen und enden mit einer der folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="9433c-p102">To perform Following Content tasks by using the REST API, you send HTTP **GET** and HTTP **POST** requests to the REST service. REST endpoint URIs for Following Content tasks begin with the **SocialRestFollowingManager** resource ( `<siteUri>/_api/social.following`) and end with one of the following resources:</span></span>
  
    
    

- <span data-ttu-id="9433c-115">**follow** starten nach einem Dokument, Website oder tag</span><span class="sxs-lookup"><span data-stu-id="9433c-115">**follow** to start following a document, site, or tag</span></span>
    
  
- <span data-ttu-id="9433c-116">**stopfollowing** zu einem Dokument, Website oder tag</span><span class="sxs-lookup"><span data-stu-id="9433c-116">**stopfollowing** to stop following a document, site, or tag</span></span>
    
  
- <span data-ttu-id="9433c-117">**isfollowed**, um herauszufinden, ob der Benutzer ein bestimmtes Dokument, eine Website oder ein Tag folgt</span><span class="sxs-lookup"><span data-stu-id="9433c-117">**isfollowed** to find out whether the user is following a specific document, site, or tag</span></span>
    
  
- <span data-ttu-id="9433c-118">**my/followed** abzurufenden beobachteter Dokumente, Websites und tags</span><span class="sxs-lookup"><span data-stu-id="9433c-118">**my/followed** to get followed documents, sites, and tags</span></span>
    
  
- <span data-ttu-id="9433c-119">**my/followedcount** Anzahl der gefolgten Dokumente, Websites und Tags abrufen</span><span class="sxs-lookup"><span data-stu-id="9433c-119">**my/followedcount** to get the count of followed documents, sites, and tags</span></span>
    
  

> <span data-ttu-id="9433c-120">**Hinweis:** Sie verwenden diese Endpunkte auch für Aufgaben zum Folgen von Personen, allerdings unterstützen die Ressourcen **followers** und **suggestions**, die über **SocialRestFollowingManager** verfügbar sind, nur das Folgen von Personen, nicht von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="9433c-120">**Note:** You also use these endpoints for Following People tasks, but the **followers** and **suggestions** resources available from **SocialRestFollowingManager** only support following people, not content.</span></span> <span data-ttu-id="9433c-121">Weitere Informationen zur Verwendung von **SocialRestFollowingManager** finden Sie unter [Folgen von Inhalten in SharePoint](follow-content-in-sharepoint.md) und [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="9433c-121">For more information about how you can use **SocialRestFollowingManager**, see  [Follow content in SharePoint](follow-content-in-sharepoint.md) and [Follow people in SharePoint](follow-people-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-creating-a-sharepoint-hosted-app-that-manages-followed-content-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="9433c-122">Voraussetzungen für die Erstellung einer von SharePoint gehosteten App, die gefolgte Inhalte mit dem REST-Dienst von SharePoint verwaltet</span><span class="sxs-lookup"><span data-stu-id="9433c-122">Prerequisites for creating a SharePoint-hosted app that manages followed content by using the SharePoint REST service</span></span>
<span data-ttu-id="9433c-123"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-123"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="9433c-p104">In diesem Artikel wird davon ausgegangen, dass Sie die SharePoint-Add-In mithilfe einer Napa- oder Office 365-Entwicklerwebsite erstellen. Wenn Sie diese Entwicklungsumgebung verwenden, sind die Voraussetzungen bereits erfüllt.</span><span class="sxs-lookup"><span data-stu-id="9433c-p104">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
  
    
    

> <span data-ttu-id="9433c-126">**Hinweis:** Wechseln Sie zur [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx), um sich für eine Entwicklerwebsite anzumelden und mit der Verwendung von Napa zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="9433c-126">**Note:** Go to  [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) to sign up for a Developer Site and start using Napa.</span></span>
  
    
    

<span data-ttu-id="9433c-127">Wenn Sie nicht auf eine Office 365 Developer Site Napa verwenden, benötigen Sie die folgenden Anforderungen erfüllen, bevor Sie die SharePoint-Add-In bereitstellen können:</span><span class="sxs-lookup"><span data-stu-id="9433c-127">If you're not using Napa on an Office 365 Developer Site, you'll need to meet the following prerequisites before you can deploy the SharePoint Add-in:</span></span>
  
    
    

- <span data-ttu-id="9433c-p105">Eine SharePoint-Entwicklungsumgebung, die für die Anwendungsisolation konfiguriert ist. Wenn Sie Remote-Entwicklung, muss der Server Sideloading Apps Unterstützung oder müssen Sie die app auf einer Entwicklerwebsite installieren.</span><span class="sxs-lookup"><span data-stu-id="9433c-p105">A SharePoint development environment that is configured for app isolation. If you're developing remotely, the server must support sideloading of apps or you must install the app on a Developer Site.</span></span>
    
  
- <span data-ttu-id="9433c-130">Der Meine Website-Host konfiguriert ist, mit einer persönlichen Website für den aktuellen Benutzer erstellt.</span><span class="sxs-lookup"><span data-stu-id="9433c-130">The My Site host configured, with a personal site created for the current user.</span></span>
    
  
- <span data-ttu-id="9433c-131">Visual Studio 2012 oder Visual Studio 2013 mit Office Developer Tools für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9433c-131">Visual Studio 2012 or Visual Studio 2013 with Office Developer Tools for Visual Studio 2013.</span></span>
    
  
- <span data-ttu-id="9433c-132">Über ausreichende Berechtigungen für den angemeldeten Benutzer:</span><span class="sxs-lookup"><span data-stu-id="9433c-132">Sufficient permissions for the logged-on user:</span></span>
    
  - <span data-ttu-id="9433c-133">Lokale Administratorberechtigungen auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="9433c-133">Local administrator permissions on the development computer.</span></span>
    
  
  - <span data-ttu-id="9433c-p106">Verwalten von Website und Erstellen von Unterwebsites von Benutzerberechtigungen für die SharePoint-Website, in dem Sie die app installieren möchten. Standardmäßig sind diese Berechtigungen nur für Benutzer über die Berechtigungsstufe Vollzugriff verfügen oder Personen in der Gruppe Websitebesitzer sind verfügbar.</span><span class="sxs-lookup"><span data-stu-id="9433c-p106">Manage Web Site and Create Subsites user permissions to the SharePoint site where you're installing the app. By default, these permissions are available only to users who have the Full Control permission level or who are in the site Owners group.</span></span>
    
  
  - <span data-ttu-id="9433c-p107">Sie müssen sich mit einem anderen Konto als dem Systemkonto anmelden, da das Systemkonto nicht über die Berechtigung zur Installation der App verfügt.</span><span class="sxs-lookup"><span data-stu-id="9433c-p107">You must be logged on as someone other than the system account. The system account does not have permission to install the app.</span></span>
    
  

> <span data-ttu-id="9433c-138">**Hinweis:** Informationen zum lokalen Setup (einschließlich der eventuell erforderlichen Deaktivierung der Loopbacküberprüfung) finden Sie unter [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9433c-138">**Note:** See  [Set up an on-premises development environment for SharePoint Add-ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx) for guidance about on-premises setup (including how to disable the loopback check, if necessary).</span></span>
  
    
    


  
    
    

## <a name="create-the-sharepoint-add-in-project"></a><span data-ttu-id="9433c-139">Erstellen des SharePoint-Add-In-Projekts</span><span class="sxs-lookup"><span data-stu-id="9433c-139">Create the SharePoint Add-in project</span></span>
<span data-ttu-id="9433c-140"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-140"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="9433c-141">Klicken Sie auf Ihrer Entwicklerwebsite öffnen Sie Napa, und wählen Sie dann auf **Neues Projekt hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="9433c-141">On your Developer Site, open Napa, and then choose **Add New Project**.</span></span>
    
  
2. <span data-ttu-id="9433c-142">Wählen Sie die Vorlage **App für SharePoint**, nennen Sie das Projekt, und wählen Sie dann auf die Schaltfläche **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="9433c-142">Choose the **App for SharePoint** template, name the project, and then choose the **Create** button.</span></span>
    
  
3. <span data-ttu-id="9433c-143">Legen Sie die Berechtigungen für Ihre app:</span><span class="sxs-lookup"><span data-stu-id="9433c-143">Set the permissions for your app:</span></span>
    
   1. <span data-ttu-id="9433c-144">Wählen Sie die Schaltfläche " **Eigenschaften** " am unteren Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="9433c-144">Choose the **Properties** button at the bottom of the page.</span></span>
    
  
   2. <span data-ttu-id="9433c-145">Wählen Sie im Fenster **Eigenschaften****Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="9433c-145">In the **Properties** window, choose **Permissions**.</span></span>
    
  
   3. <span data-ttu-id="9433c-146">Legen Sie **die Inhaltskategorie****Write** Berechtigungen für den **Mandanten** Bereich.</span><span class="sxs-lookup"><span data-stu-id="9433c-146">In the **Content** category, set **Write** permissions for the **Tenant** scope.</span></span>
    
  
   4. <span data-ttu-id="9433c-147">Legen Sie in der Kategorie **für soziale Netzwerke****Read** -Berechtigungen für den Bereich **Von Benutzerprofilen**.</span><span class="sxs-lookup"><span data-stu-id="9433c-147">In the **Social** category, set **Read** permissions for the **User Profiles** scope.</span></span>
    
  
   5. <span data-ttu-id="9433c-148">Das Fenster **Eigenschaften** zu schließen.</span><span class="sxs-lookup"><span data-stu-id="9433c-148">Close the **Properties** window.</span></span>
    
  
4. <span data-ttu-id="9433c-149">Erweitern Sie den Knoten **Skripts**, wählen Sie die Datei App.js, und Ersetzen Sie den Inhalt durch den Code aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="9433c-149">Expand the **Scripts** node, choose the App.js file and replace its contents with the code from one of the following scenarios:</span></span>
    
   -  [<span data-ttu-id="9433c-150">Starten Sie nach und nicht mehr Folgen eines Dokuments</span><span class="sxs-lookup"><span data-stu-id="9433c-150">Start following and stop following a document</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowDocs)
   -  [<span data-ttu-id="9433c-151">Starten Sie nach und nicht mehr folgen einer Website</span><span class="sxs-lookup"><span data-stu-id="9433c-151">Start following and stop following a site</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowSites)
   -  [<span data-ttu-id="9433c-152">Nach Starten Sie und beenden Sie einer Kategorie folgen</span><span class="sxs-lookup"><span data-stu-id="9433c-152">Start following and stop following a tag</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowTags)
   -  [<span data-ttu-id="9433c-153">Abrufen von verfolgten Inhalt</span><span class="sxs-lookup"><span data-stu-id="9433c-153">Get followed content</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_GetFollowed)
  
5. <span data-ttu-id="9433c-154">Um die app ausgeführt werden soll, wählen Sie die Schaltfläche " **Projekt ausführen** " am unteren Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="9433c-154">To run the app, choose the **Run Project** button at the bottom of the page.</span></span>
    
  
6. <span data-ttu-id="9433c-p108">Wählen Sie die Schaltfläche **Vertrauen sie** **Vertrauen Sie** Sie auf der Seite, die geöffnet wird. Die appseite wird geöffnet, und es wird der Code ausgeführt. Debuggen Sie die Seite, wählen die **F12**-Taste, und wählen Sie dann auf der Registerkarte **Skript** App.js aus.</span><span class="sxs-lookup"><span data-stu-id="9433c-p108">In the **Do you trust** page that opens, choose the **Trust It** button. The app page opens and runs the code. To debug the page, choose the **F12** key and then choose App.js on the **Script** tab.</span></span>
    
  

## <a name="code-example-start-following-and-stop-following-a-document-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="9433c-158">Codebeispiel: Starten Sie nach und nach einem Dokument mithilfe des REST-Diensts SharePoint beenden</span><span class="sxs-lookup"><span data-stu-id="9433c-158">Code example: Start following and stop following a document by using the SharePoint REST service</span></span>
<span data-ttu-id="9433c-159"><a name="bkmk_FollowDocs"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-159"><a name="bkmk_FollowDocs"> </a></span></span>

<span data-ttu-id="9433c-160">Das folgende Codebeispiel stellt den Inhalt der App.js-Datei und zeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="9433c-160">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="9433c-161">Möchten Sie app-Webs URI aus der Abfragezeichenfolge erhalten, und erstellen Sie den  `<siteUri>/_api/social.following` Endpunkt-URI.</span><span class="sxs-lookup"><span data-stu-id="9433c-161">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="9433c-162">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `isfollowed` , um herauszufinden, ob der aktuelle Benutzer bereits ein angegebenes Dokument folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-162">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified document.</span></span>
    
  
- <span data-ttu-id="9433c-163">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `follow` , um nach dem Dokument zu starten.</span><span class="sxs-lookup"><span data-stu-id="9433c-163">Build and send a **POST** request to the `follow` endpoint to start following the document.</span></span>
    
  
- <span data-ttu-id="9433c-164">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `stopfollowing` So beenden Sie nach dem Dokument.</span><span class="sxs-lookup"><span data-stu-id="9433c-164">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the document.</span></span>
    
  
- <span data-ttu-id="9433c-p109">Lesen Sie die JSON-Antwort von der Anforderung  `isfollowed` und die Anforderung `follow` zurückgegeben. (Die Anforderung `stopfollowing` nicht nichts in der Antwort zurück.) Siehe [Beispiel JSON Antworten](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="9433c-p109">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) See [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="9433c-167">Bevor Sie den Code ausführen müssen Sie zum Hochladen eines Dokuments und ändern den Platzhalterwert für die Variable **documentUrl** an die URL des Dokuments.</span><span class="sxs-lookup"><span data-stu-id="9433c-167">Before you run the code, you'll need to upload a document and change the placeholder value for the **documentUrl** variable to the document's URL.</span></span>
  
    
    



```

// Replace the documentUrl placeholder value before you run the code.
var documentUrl = "https://domain.sharepoint.com/Shared%20Documents/fileName.docx";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the document.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the document.');
                stopFollowDocument();
            }
            else {
                alert('The user is currently NOT following the document.');
                followDocument();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a document.
// The request body includes a SocialActorInfo object that represents
// the document to follow.
// The success function reads the response from the REST service.
function followDocument() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the document. ',
                1 : 'The user is already following the document. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a document.
// The request body includes a SocialActorInfo object that represents
// the document to stop following.
function stopFollowDocument() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the document.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-start-following-and-stop-following-a-site-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="9433c-168">Codebeispiel: Starten Sie nach und nach einer Website mithilfe des REST-Diensts SharePoint beenden</span><span class="sxs-lookup"><span data-stu-id="9433c-168">Code example: Start following and stop following a site by using the SharePoint REST service</span></span>
<span data-ttu-id="9433c-169"><a name="bkmk_FollowSites"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-169"><a name="bkmk_FollowSites"> </a></span></span>

<span data-ttu-id="9433c-170">Das folgende Codebeispiel stellt den Inhalt der App.js-Datei und zeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="9433c-170">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="9433c-171">Möchten Sie app-Webs URI aus der Abfragezeichenfolge erhalten, und erstellen Sie den  `<siteUri>/_api/social.following` Endpunkt-URI.</span><span class="sxs-lookup"><span data-stu-id="9433c-171">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="9433c-172">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `isfollowed` , um herauszufinden, ob der aktuelle Benutzer eine angegebene Website bereits folgen.</span><span class="sxs-lookup"><span data-stu-id="9433c-172">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified site.</span></span>
    
  
- <span data-ttu-id="9433c-173">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `follow` , um nach der Website zu starten.</span><span class="sxs-lookup"><span data-stu-id="9433c-173">Build and send a **POST** request to the `follow` endpoint to start following the site.</span></span>
    
  
- <span data-ttu-id="9433c-174">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `stopfollowing` So beenden Sie nach der Website.</span><span class="sxs-lookup"><span data-stu-id="9433c-174">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the site.</span></span>
    
  
- <span data-ttu-id="9433c-p110">Lesen Sie die JSON-Antwort von der Anforderung  `isfollowed` und die Anforderung `follow` zurückgegeben. (Die Anforderung `stopfollowing` nicht nichts in der Antwort zurück.) Siehe [Beispiel JSON Antworten](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="9433c-p110">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) See [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="9433c-p111">Bevor Sie den Code ausführen ändern Sie den Platzhalterwert für die Variable **siteUrl** entsprechend die Website, die Sie folgen möchten. Verwenden Sie das Format **http://server/siteCollection/site** für eine Website in einer Websitesammlung. Führen Sie eine Website über eine beliebige Seite oder eine Bibliothek an diesem Standort. Wenn die Website eine Vorlage verwendet wird, die nicht unterstützt erhalten (wie meine Website-Host oder einer persönlichen Website) folgen einen **UnsupportedSite** -Fehler (Fehlercode 10) Sie.</span><span class="sxs-lookup"><span data-stu-id="9433c-p111">Before you run the code, change the placeholder value for the **siteUrl** variable to match the site that you want to follow. Use the format **http://server/siteCollection/site** for a site in a site collection. You can follow a site from any page or library in that site. If the site uses a template that doesn't support following (like the My Site host or a personal site), you'll get an **UnsupportedSite** error (error code 10).</span></span>
  
    
    



```

// Replace the siteUrl placeholder value before you run the code.
var siteUrl = "https://domain.sharepoint.com";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the site.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the site.');
                stopFollowSite();
            }
            else {
                alert('The user is currently NOT following the site.');
                followSite();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a site.
// The request body includes a SocialActorInfo object that represents
// the site to follow.
// The success function reads the response from the REST service.
function followSite() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the site. ',
                1 : 'The user is already following the site. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a site.
// The request body includes a SocialActorInfo object that represents
// the site to stop following.
function stopFollowSite() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the site.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-start-following-and-stop-following-a-tag-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="9433c-181">Codebeispiel: nach starten und Beenden einer Kategorie mithilfe des REST-Diensts SharePoint folgen</span><span class="sxs-lookup"><span data-stu-id="9433c-181">Code example: Start following and stop following a tag by using the SharePoint REST service</span></span>
<span data-ttu-id="9433c-182"><a name="bkmk_FollowTags"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-182"><a name="bkmk_FollowTags"> </a></span></span>

<span data-ttu-id="9433c-183">Das folgende Codebeispiel stellt den Inhalt der App.js-Datei und zeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="9433c-183">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="9433c-184">Möchten Sie app-Webs URI aus der Abfragezeichenfolge erhalten, und erstellen Sie den  `<siteUri>/_api/social.following` Endpunkt-URI.</span><span class="sxs-lookup"><span data-stu-id="9433c-184">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="9433c-185">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `isfollowed` , um herauszufinden, ob der aktuelle Benutzer ein angegebenes Tag bereits folgen.</span><span class="sxs-lookup"><span data-stu-id="9433c-185">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified tag.</span></span>
    
  
- <span data-ttu-id="9433c-186">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `follow` , um die Kategorie folgen zu starten.</span><span class="sxs-lookup"><span data-stu-id="9433c-186">Build and send a **POST** request to the `follow` endpoint to start following the tag.</span></span>
    
  
- <span data-ttu-id="9433c-187">Erstellen Sie und senden Sie eine **POST** -Anforderung an den Endpunkt `stopfollowing` So beenden Sie die Kategorie folgen.</span><span class="sxs-lookup"><span data-stu-id="9433c-187">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the tag.</span></span>
    
  
- <span data-ttu-id="9433c-p112">Lesen Sie die JSON-Antwort von der Anforderung  `isfollowed` und die Anforderung `follow` zurückgegeben. (Die Anforderung `stopfollowing` nicht nichts in der Antwort zurück.) Weitere Informationen finden Sie unter [Beispiel JSON Antworten](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="9433c-p112">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) For more information, see [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="9433c-p113">Ändern Sie den Platzhalterwert für die Variable **tagGuid** vor dem Ausführen des Codes die GUID der vorhandene Tags. Die Taxonomie-API, die Sie verwenden, um ein Tag aus der **HashTagsTermSet** abzurufen keine REST-Schnittstelle, daher Sie in das Clientobjektmodell .NET oder das JavaScript-Objektmodell verwenden müssen. Ein Beispiel finden Sie unter [So rufen Sie die GUID eines Tags auf der Basis des Namens des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid) .</span><span class="sxs-lookup"><span data-stu-id="9433c-p113">Before you run the code, change the placeholder value for the **tagGuid** variable to the GUID of an existing tag. The taxonomy API that you use to retrieve a tag from the **HashTagsTermSet** doesn't have a REST interface, so you have to use the .NET client object model or the JavaScript object model. See [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid) for an example.</span></span>
  
    
    



```

// Replace the tagGuid placeholder value before you run the code.
var tagGuid = "19a4a484-c1dc-4bc5-8c93-bb96245ce928";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the tag.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the tag.');
                stopFollowTag();
            }
            else {
                alert('The user is currently NOT following the tag.');
                followTag();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a tag.
// The request body includes a SocialActorInfo object that represents
// the tag to follow.
// The success function reads the response from the REST service.
function followTag() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the tag. ',
                1 : 'The user is already following the tag. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a tag.
// The request body includes a SocialActorInfo object that represents
// the tag to stop following.
function stopFollowTag() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the tag.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-get-followed-content-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="9433c-193">Codebeispiel: Gefolgte Inhalte mit dem REST-Dienst von SharePoint erhalten</span><span class="sxs-lookup"><span data-stu-id="9433c-193">Code example: Get followed content by using the SharePoint REST service</span></span>
<span data-ttu-id="9433c-194"><a name="bkmk_GetFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-194"><a name="bkmk_GetFollowed"> </a></span></span>

<span data-ttu-id="9433c-195">Das folgende Codebeispiel stellt den Inhalt der App.js-Datei und zeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="9433c-195">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="9433c-196">Möchten Sie app-Webs URI aus der Abfragezeichenfolge erhalten, und erstellen Sie den  `<siteUri>/_api/social.following` Endpunkt-URI.</span><span class="sxs-lookup"><span data-stu-id="9433c-196">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="9433c-197">Erstellen Sie und senden Sie eine **GET** -Anforderung an den Endpunkt `my/followedcount` , um die Anzahl der Inhalte abzurufen, die der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-197">Build and send a **GET** request to the `my/followedcount` endpoint to get the count of content that the current user is following.</span></span>
    
  
- <span data-ttu-id="9433c-198">Erstellen Sie und senden Sie eine **GET** -Anforderung an den Endpunkt `my/followed` , um den Inhalt abzurufen, den der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-198">Build and send a **GET** request to the `my/followed` endpoint to get the content that the current user is following.</span></span>
    
  
- <span data-ttu-id="9433c-p114">Lesen Sie die JSON-Antwort von der Anforderungen zurückgegeben. Siehe  [Beispiel JSON Antworten](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="9433c-p114">Read the JSON response returned by the requests. See  [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  

```

var followingManagerEndpoint;
var followedCount;

// Get the SPAppWebUrl parameter from the query string and build
// the following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl)+ "/_api/social.following";
    getMyFollowedCount();
} );

// Get the count of content that the current user is following.
// The "types=14" parameter specifies all content types
// (documents = 2 + sites = 4 + tags = 8).
function getMyFollowedCount() {
    $.ajax( {
        url: followingManagerEndpoint + "/my/followedcount(types=14)",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: function (data) { 
            followedCount = data.d.FollowedCount;
            getMyFollowedContent();
        },
        error: requestFailed
    } );
}

// Get the content that the current user is following.
// The "types=14" parameter specifies all content types
// (documents = 2 + sites = 4 + tags = 8).
function getMyFollowedContent() {
    $.ajax( {
        url: followingManagerEndpoint + "/my/followed(types=14)",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: followedContentRetrieved,
        error: requestFailed
    });
}

// Parse the JSON data and iterate through the collection.
function followedContentRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
    var types = {
        1: "document",
        2: "site",
        3: "tag" 
    };
 
    var followedActors = jsonObject.d.Followed.results; 
    var followedList = "You're following " + followedCount + " items:";
    for (var i = 0; i < followedActors.length; i++) {
        var actor = followedActors[i];
        followedList += "<p>The " + types[actor.ActorType] + ": \\"" +
        actor.Name + "\\"</p>";
    } 
    $("#message").html(followedList); 
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="example-json-responses-for-following-content-requests"></a><span data-ttu-id="9433c-201">Beispiel von JSON Antworten für folgende inhaltsanforderungen</span><span class="sxs-lookup"><span data-stu-id="9433c-201">Example JSON responses for Following Content requests</span></span>
<span data-ttu-id="9433c-202"><a name="bk_exampleResponses"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-202"><a name="bk_exampleResponses"> </a></span></span>

<span data-ttu-id="9433c-p115">Standardmäßig gibt des REST-Diensts Antworten, die mithilfe des Atom-Protokolls formatiert sind, aber Sie können das JSON-Format mithilfe von HTTP-Headers **Accept** anfordern (zum Beispiel: `"accept":"application/json;odata=verbose"`). Die Antwortdaten werden als Zeichenfolge zurückgegeben, und können die **JSON.stringify** und **JSON.parse** konvertiert die Zeichenfolge in ein Objekt, wie in den vorherigen Codebeispielen dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9433c-p115">By default, the REST service returns responses that are formatted by using the Atom protocol, but you can request the JSON format by using an HTTP **Accept** header (for example: `"accept":"application/json;odata=verbose"`). The response data is returned as a string, and you can use the **JSON.stringify** function and **JSON.parse** function to convert the string into an object, as shown in the previous code examples.</span></span>
  
    
    
<span data-ttu-id="9433c-p116">Betrachten Sie um einen von der REST-Dienst im Debugmodus zurückgegebenen Fehler beheben die **responseText** -Eigenschaft, wie die **requestFailed** Rückruffunktionen in den vorherigen Beispielen gezeigt aus. Sie können auch die Korrelations-ID für die Server-ULS-Protokoll aus einem Netzwerksniffer oder HTTP-Debugger, wie beispielsweise Fiddler abrufen. Die Korrelations-ID ist die gleiche wie die-ID in der HTTP-Antwort.</span><span class="sxs-lookup"><span data-stu-id="9433c-p116">To troubleshoot an error returned by the REST service, in debug mode, look at the **responseText** property, as shown in the **requestFailed** callback functions in the previous examples. You can also get the correlation ID for the ULS server log from a network sniffer or HTTP debugger, such as Fiddler. The correlation ID is the same as the request ID in the HTTP response.</span></span>
  
    
    

### <a name="example-response-for-the-follow-endpoint"></a><span data-ttu-id="9433c-208">Beispielantwort für den Endpunkt folgen</span><span class="sxs-lookup"><span data-stu-id="9433c-208">Example response for the Follow endpoint</span></span>

<span data-ttu-id="9433c-209">Als Reaktion auf Anfragen an den Endpunkt  `follow` mithilfe der clientseitigen gibt der REST-Dienst einen **SocialFollowResult** -Wert, der angibt, ob die Anforderung **Follow** erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="9433c-209">In response to client-side requests to the  `follow` endpoint, the REST service returns a **SocialFollowResult** value that represents whether the **Follow** request succeeded.</span></span>
  
    
    
<span data-ttu-id="9433c-210">Die folgende Antwort stellt den Status **AlreadyFollowing** dar.</span><span class="sxs-lookup"><span data-stu-id="9433c-210">The following response represents the **AlreadyFollowing** status.</span></span>
  
    
    



```

{"d":{"Follow":1}}
```

<span data-ttu-id="9433c-211">Tabelle 1 zeigt **SocialFollowResult** Statuscodes und deren Werte an.</span><span class="sxs-lookup"><span data-stu-id="9433c-211">Table 1 shows **SocialFollowResult** status codes and their values.</span></span>
  
    
    

<span data-ttu-id="9433c-212">**Tabelle 1: SocialFollowResult-Codes und -Werte**</span><span class="sxs-lookup"><span data-stu-id="9433c-212">**Table 1. SocialFollowResult codes and values**</span></span>

|<span data-ttu-id="9433c-213">**Statuscode**</span><span class="sxs-lookup"><span data-stu-id="9433c-213">**Status code**</span></span>|<span data-ttu-id="9433c-214">**Wert**</span><span class="sxs-lookup"><span data-stu-id="9433c-214">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9433c-215">0</span><span class="sxs-lookup"><span data-stu-id="9433c-215">0</span></span>|<span data-ttu-id="9433c-p117">**OK**. Der aktuelle Benutzer ist nun den Akteur folgen.</span><span class="sxs-lookup"><span data-stu-id="9433c-p117">**OK**. The current user is now following the actor.</span></span>|
|<span data-ttu-id="9433c-218">1</span><span class="sxs-lookup"><span data-stu-id="9433c-218">1</span></span>|<span data-ttu-id="9433c-p118">**AlreadyFollowing**. Der aktuelle Benutzer ist den Akteur bereits folgen.</span><span class="sxs-lookup"><span data-stu-id="9433c-p118">**AlreadyFollowing**. The current user is already following the actor.</span></span>|
|<span data-ttu-id="9433c-221">2</span><span class="sxs-lookup"><span data-stu-id="9433c-221">2</span></span>|<span data-ttu-id="9433c-p119">**LimitReached**. Fehler bei der Anforderung, da ein internes Limit erreicht wurde.</span><span class="sxs-lookup"><span data-stu-id="9433c-p119">**LimitReached**. The request failed because an internal limit was reached.</span></span>|
|<span data-ttu-id="9433c-224">3</span><span class="sxs-lookup"><span data-stu-id="9433c-224">3</span></span>|<span data-ttu-id="9433c-p120">**InternalError**. Die Anforderung ist aufgrund eines internen Fehlers fehlgeschlagen.</span><span class="sxs-lookup"><span data-stu-id="9433c-p120">**InternalError**. The request failed due to an internal error.</span></span>|
   

> <span data-ttu-id="9433c-227">**Hinweis:** Der REST-Dienst gibt keine Antwort für die Anforderung **StopFollowing** zurück.</span><span class="sxs-lookup"><span data-stu-id="9433c-227">**Note:** The REST service doesn't return a response for the **StopFollowing** request.</span></span> <span data-ttu-id="9433c-228">Er gibt `{"d":{"StopFollowing":null}}` zurück.</span><span class="sxs-lookup"><span data-stu-id="9433c-228">It returns `{"d":{"StopFollowing":null}}`.</span></span> 
  
    
    


### <a name="example-response-for-the-isfollowed-endpoint"></a><span data-ttu-id="9433c-229">Beispielantwort für den Endpunkt IsFollowed</span><span class="sxs-lookup"><span data-stu-id="9433c-229">Example response for the IsFollowed endpoint</span></span>

<span data-ttu-id="9433c-230">Als Reaktion auf Anfragen an den Endpunkt  `isfollowed` mithilfe der clientseitigen gibt der REST-Dienst einen **bool** -Wert, der angibt, ob der aktuelle Benutzer den angegebenen Akteur folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-230">In response to client-side requests to the  `isfollowed` endpoint, the REST service returns a **bool** value that represents whether the current user is following the specified actor.</span></span>
  
    
    
<span data-ttu-id="9433c-231">Die folgende Antwort gibt an, dass der aktuelle Benutzer nicht das angegebene Dokument, eine Website oder ein Tag folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-231">The following response indicates that the current user is not following the specified document, site, or tag.</span></span>
  
    
    



```
{"d":{"IsFollowed":false}}
```


### <a name="example-response-for-the-myfollowed-endpoint"></a><span data-ttu-id="9433c-232">Beispielantwort für den Endpunkt Meine/besuchter</span><span class="sxs-lookup"><span data-stu-id="9433c-232">Example response for the My/Followed endpoint</span></span>

<span data-ttu-id="9433c-233">Als Reaktion auf Anfragen an den Endpunkt  `my/followed` mithilfe der clientseitigen gibt der REST-Dienst ein Array von **SP.Social.SocialActor** -Objekten, die Dokumenten, Websites und Tags, die der aktuelle Benutzer folgt darstellen.</span><span class="sxs-lookup"><span data-stu-id="9433c-233">In response to client-side requests to the  `my/followed` endpoint, the REST service returns an array of **SP.Social.SocialActor** objects that represent documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="9433c-p122">Die folgende Antwort stellt eine besuchter Dokument, Website und Tag. Die Anforderung gibt die Arten von Inhalt enthalten.</span><span class="sxs-lookup"><span data-stu-id="9433c-p122">The following response represents a followed document, site, and tag. The request specifies the types of content to include.</span></span>
  
    
    



```
{"d":{"Followed":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":1
    "CanFollow":true
    "ContentUri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"2.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.
      51bbb5d8e214457ba794669345d23040.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"snippets.txt"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"00000000-0000-0000-0000-000000000000"
    "Title":null
    "Uri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
  }
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":2
    "CanFollow":true
    "ContentUri":"https://domain.sharepoint.com:443/"
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"8.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.
      089f4944a6374a64b52b7af5ba140392.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"Developer Site"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"00000000-0000-0000-0000-000000000000"
    "Title":null
    "Uri":"https://domain.sharepoint.com:443/"
  }
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":3
    "CanFollow":true
    "ContentUri":null
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"16.00000000000000000000000000000000.00000000000000000000000000000000.
      19a4a484c1dc4bc58c93bb96245ce928.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"#someTag"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928"
    "Title":null
    "Uri":"https://domain-my.sharepoint.com:443/_layouts/15/HashTagProfile.aspx?
      TermID=19a4a484-c1dc-4bc5-8c93-bb96245ce928"
  }
]}}}
```


### <a name="example-response-for-the-myfollowedcount-endpoint"></a><span data-ttu-id="9433c-236">Beispielantwort für den Endpunkt Meine/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="9433c-236">Example response for the My/FollowedCount endpoint</span></span>

<span data-ttu-id="9433c-237">Als Reaktion auf Anfragen an den Endpunkt  `my/followedcount` mithilfe der clientseitigen gibt der REST-Dienst einen **Int32** -Wert, der die Gesamtzahl der angegebenen Actor Typen darstellt, die der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="9433c-237">In response to client-side requests to the  `my/followedcount` endpoint, the REST service returns an **Int32** value that represents the total count of specified actor types that the current user is following.</span></span>
  
    
    
<span data-ttu-id="9433c-p123">Die folgende Antwort stellt eine Anzahl von drei beobachteter Dokumente, Websites und/oder Tags dar. Die Anforderung gibt die Arten von Inhalt enthalten.</span><span class="sxs-lookup"><span data-stu-id="9433c-p123">The following response represents a count of three followed documents, sites, and/or tags. The request specifies the types of content to include.</span></span>
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="additional-resources"></a><span data-ttu-id="9433c-240">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9433c-240">Additional resources</span></span>
<span data-ttu-id="9433c-241"><a name="bkmk_AddtionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="9433c-241"><a name="bkmk_AddtionalResources"> </a></span></span>


-  [<span data-ttu-id="9433c-242">Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9433c-242">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9433c-243">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9433c-243">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="9433c-244">Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9433c-244">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

