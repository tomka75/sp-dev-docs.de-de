---
title: "Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des REST-Diensts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1da8d484-3666-42c3-8a8f-8b3ef93e96e9
ms.openlocfilehash: 2fafda13f6d5c6e62f7519bd9896c91a87dcc5f3
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-rest-service-in-sharepoint"></a><span data-ttu-id="a9010-102">Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-102">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>

<span data-ttu-id="a9010-103">Erstellen Sie eine von SharePoint gehostete App, die den REST-Dienst zum Veröffentlichen eines Beitrags und zum Abrufen des persönlichen Feeds für den aktuellen Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="a9010-103">Create a SharePoint-hosted app that uses the REST service to publish a post and get the personal feed for the current user.</span></span>

## <a name="prerequisites-for-creating-a-sharepoint-hosted-sharepoint-add-in-that-publishes-a-post-and-gets-the-social-feed-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="a9010-104">Voraussetzungen für das Erstellen einer SharePoint-Hosting SharePoint-Add-In, die einen Beitrag veröffentlicht und ruft den Feed für soziale Netzwerke mithilfe des REST-Diensts SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-104">Prerequisites for creating a SharePoint-hosted SharePoint Add-in that publishes a post and gets the social feed by using the SharePoint REST service</span></span>
<span data-ttu-id="a9010-105"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-105"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="a9010-p101">In diesem Artikel wird davon ausgegangen, dass Sie die SharePoint-Add-In mithilfe einer Napa- oder Office 365-Entwicklerwebsite erstellen. Wenn Sie diese Entwicklungsumgebung verwenden, sind die Voraussetzungen bereits erfüllt.</span><span class="sxs-lookup"><span data-stu-id="a9010-p101">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
  
    
    

> <span data-ttu-id="a9010-108">**Hinweis:** Unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) erhalten Sie Informationen zur Registrierung für eine Entwicklerwebsite und zu den ersten Schritten mit Napa.</span><span class="sxs-lookup"><span data-stu-id="a9010-108">**Note:** Go to  [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) to find out how to sign up for a Developer Site and start using Napa.</span></span>
  
    
    

<span data-ttu-id="a9010-109">Wenn Sie nicht mit Napa auf einer Entwicklerwebsite arbeiten, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a9010-109">If you're not using Napa on a Developer Site, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="a9010-110">SharePoint mit Meine Website konfiguriert und mit einer persönlichen Website für den aktuellen Benutzer erstellt</span><span class="sxs-lookup"><span data-stu-id="a9010-110">SharePoint with My Site configured, and with a personal site created for the current user</span></span>
    
  
- <span data-ttu-id="a9010-111">Visual Studio 2012 und Office Developer Tools für Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a9010-111">Visual Studio 2012 and Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="a9010-112">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="a9010-112">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="a9010-113">**Hinweis:** Anleitungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von Apps für Office und SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9010-113">**Note:** For guidance about how to set up a development environment that fits your needs, see  [Start building apps for Office and SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span> 
  
    
    


## <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a><span data-ttu-id="a9010-114">Kernkonzepte zum Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-114">Core concepts to know about working with SharePoint social feeds</span></span>
<span data-ttu-id="a9010-115"><a name="bkmk_CoreConcepts"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-115"><a name="bkmk_CoreConcepts"> </a></span></span>

<span data-ttu-id="a9010-p102">Die SharePoint-hosted app, die Sie in diesem Artikel erstellen verwendet JavaScript zu erstellen und Senden von HTTP-Anfragen an Endpunkten Representational State Transfer (REST). Diese Anfragen einen Beitrag veröffentlichen und Personal-feed für den aktuellen Benutzer abzurufen. Tabelle 1 enthält Links zu Artikeln, in denen allgemeine Konzepte zu, die Sie kennen sollten beschreiben, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="a9010-p102">The SharePoint-hosted app that you create in this article uses JavaScript to build and send HTTP requests to Representational State Transfer (REST) endpoints. These requests publish a post and get the personal feed for the current user. Table 1 contains links to articles that describe general concepts you should understand before you get started.</span></span>
  
    
    

<span data-ttu-id="a9010-119">**In Tabelle 1. Zentrale Konzepte für die Arbeit mit sozialen Feeds SharePoint**</span><span class="sxs-lookup"><span data-stu-id="a9010-119">**Table 1. Core concepts for working with SharePoint social feeds**</span></span>


|<span data-ttu-id="a9010-120">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="a9010-120">**Article title**</span></span>|<span data-ttu-id="a9010-121">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a9010-121">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="a9010-122">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="a9010-122">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="a9010-123">Informationen Sie zu SharePoint-Add-Ins und grundlegende Konzepte für deren Erstellung.</span><span class="sxs-lookup"><span data-stu-id="a9010-123">Learn about SharePoint Add-ins and fundamental concepts for building them.</span></span>  <br/> |
| [<span data-ttu-id="a9010-124">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-124">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md) <br/> |<span data-ttu-id="a9010-125">Erfahren Sie, wie Sie die Programmierung mit sozialen Feeds und Microblog Beiträge, folgen von Personen und Inhalten (Dokumente, Websites und tags.md), und Arbeiten mit Benutzerprofilen zu starten.</span><span class="sxs-lookup"><span data-stu-id="a9010-125">Find out how to start programming with social feeds and microblog posts, following people and content (documents, sites, and tags.md), and working with user profiles.</span></span>  <br/> |
| [<span data-ttu-id="a9010-126">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-126">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md) <br/> |<span data-ttu-id="a9010-127">Informationen Sie zu allgemeinen Programmieraufgaben zum Arbeiten mit sozialen Feeds und die API, die Sie zum Ausführen der Aufgaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="a9010-127">Learn about common programming tasks for working with social feeds and the API that you use to perform the tasks.</span></span>  <br/> |
   

## <a name="create-the-sharepoint-add-in-project"></a><span data-ttu-id="a9010-128">Erstellen Sie das SharePoint-Add-In-Projekt.</span><span class="sxs-lookup"><span data-stu-id="a9010-128">Create the SharePoint Add-in project</span></span>
<span data-ttu-id="a9010-129"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-129"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="a9010-130">Klicken Sie auf Ihrer Entwicklerwebsite öffnen Sie Napa, und wählen Sie dann auf **Neues Projekt hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="a9010-130">On your Developer Site, open Napa, and then choose **Add New Project**.</span></span>
    
  
2. <span data-ttu-id="a9010-131">Wählen Sie die Vorlage **App für SharePoint**, nennen Sie das Projekt SocialFeedREST, und wählen Sie dann auf die Schaltfläche **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="a9010-131">Choose the **App for SharePoint** template, name the projectSocialFeedREST, and then choose the **Create** button.</span></span>
    
  
3. <span data-ttu-id="a9010-132">Geben Sie die Berechtigungen an, die Ihre App benötigt:</span><span class="sxs-lookup"><span data-stu-id="a9010-132">Specify the permissions that your app needs:</span></span>
    
  <span data-ttu-id="a9010-133">a.</span><span class="sxs-lookup"><span data-stu-id="a9010-133">a.</span></span> <span data-ttu-id="a9010-134">Wählen Sie die Schaltfläche **Eigenschaften** am unteren Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="a9010-134">Choose the **Properties** button at the bottom of the page.</span></span>
     
  <span data-ttu-id="a9010-135">b.</span><span class="sxs-lookup"><span data-stu-id="a9010-135">b.</span></span> <span data-ttu-id="a9010-136">Wählen Sie im Fenster **Eigenschaften****Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="a9010-136">In the **Properties** window, choose **Permissions**.</span></span>
    
  <span data-ttu-id="a9010-137">c.</span><span class="sxs-lookup"><span data-stu-id="a9010-137">c.</span></span> <span data-ttu-id="a9010-138">Legen Sie **die Inhaltskategorie****Write** Berechtigungen für den **Mandanten** Bereich.</span><span class="sxs-lookup"><span data-stu-id="a9010-138">In the **Content** category, set **Write** permissions for the **Tenant** scope.</span></span>
    
  <span data-ttu-id="a9010-139">d.</span><span class="sxs-lookup"><span data-stu-id="a9010-139">d.</span></span> <span data-ttu-id="a9010-140">Legen Sie in der Kategorie **für soziale Netzwerke****Read**-Berechtigungen für den Bereich **Von Benutzerprofilen**.</span><span class="sxs-lookup"><span data-stu-id="a9010-140">In the **Social** category, set **Read** permissions for the **User Profiles** scope.</span></span>
    
  <span data-ttu-id="a9010-141">e.</span><span class="sxs-lookup"><span data-stu-id="a9010-141">e.</span></span> <span data-ttu-id="a9010-142">Das Fenster **Eigenschaften** zu schließen.</span><span class="sxs-lookup"><span data-stu-id="a9010-142">Close the **Properties** window.</span></span>
    
4. <span data-ttu-id="a9010-143">Erweitern Sie den Knoten **Skripts**, wählen Sie die Datei App.js, und löschen Sie den Inhalt der Datei.</span><span class="sxs-lookup"><span data-stu-id="a9010-143">Expand the **Scripts** node, choose the App.js file, and delete the contents of the file.</span></span>
    
  

## <a name="post-to-the-social-feed-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="a9010-144">Veröffentlichen Sie den Feed für soziale Netzwerke mithilfe der SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="a9010-144">Post to the social feed by using the SharePoint REST service</span></span>
<span data-ttu-id="a9010-145"><a name="bkmk_PubPost"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-145"><a name="bkmk_PubPost"> </a></span></span>


1. <span data-ttu-id="a9010-146">Deklarieren Sie eine globale Variable für die URL des Endpunkts **SocialFeedManager**, in der Datei App.js.</span><span class="sxs-lookup"><span data-stu-id="a9010-146">In the App.js file, declare a global variable for the URL of the **SocialFeedManager** endpoint.</span></span>
    
```
var feedManagerEndpoint;
```

2. <span data-ttu-id="a9010-147">Fügen Sie den folgenden Code, die Ruft den **SPAppWebUrl** -Parameter aus der Abfragezeichenfolge ab und wird verwendet, um den **SocialFeedManager** -Endpunkt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a9010-147">Add the following code, which gets the **SPAppWebUrl** parameter from the query string and uses it to build the **SocialFeedManager** endpoint.</span></span>
    
```
  $(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    feedManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.feed";
    postToMyFeed();
});
```

3. <span data-ttu-id="a9010-148">Fügen Sie den folgenden Code, in dem die **POST** HTTP-Anforderung für den Endpunkt `/my/Feed/Post` erstellt, definiert die Bereitstellungsdaten Erstellung und im Beitrag veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="a9010-148">Add the following code, which builds the HTTP **POST** request for the `/my/Feed/Post` endpoint, defines the post's creation data, and publishes the post.</span></span>
    
    <span data-ttu-id="a9010-p108">Die Anforderung sendet eine Ressource **SocialRestPostCreationData** im Textkörper Anforderung. **SocialRestPostCreationData** enthält das Ziel für die Bereitstellung (in diesem Fall `null` an einen Stammbeitrag für den aktuellen Benutzer) und **SocialPostCreationData** komplexen Typs, die im Beitrag Eigenschaften definiert.</span><span class="sxs-lookup"><span data-stu-id="a9010-p108">The request sends a **SocialRestPostCreationData** resource in the request body. **SocialRestPostCreationData** contains the target for the post (in this case, `null` to specify a root post for the current user) and a **SocialPostCreationData** complex type that defines the post's properties.</span></span>
    


```
  
function postToMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed/Post",
        type: "POST",
        data: JSON.stringify( { 
            'restCreationData':{
                '__metadata':{ 
                    'type':'SP.Social.SocialRestPostCreationData'
                },
                'ID':null, 
                'creationData':{ 
                    '__metadata':{ 
                        'type':'SP.Social.SocialPostCreationData'
                    },
                'ContentText':'This post was published using REST.',
                'UpdateStatusText':false
                } 
            } 
        }),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: getMyFeed,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("POST error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });
}

```


## <a name="retrieve-the-social-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="a9010-151">Abrufen von den Feed für soziale Netzwerke für den aktuellen Benutzer mithilfe des REST-Diensts SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-151">Retrieve the social feed for the current user by using the SharePoint REST service</span></span>
<span data-ttu-id="a9010-152"><a name="bkmk_GetFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-152"><a name="bkmk_GetFeed"> </a></span></span>

<span data-ttu-id="a9010-p109">Fügen Sie den folgenden Code, der den Typ für den aktuellen Benutzer mithilfe des  `/my/Feed` Endpunkts feed **Personal** abgerufen. Die Kopfzeile **accept** fordert an, dass der Server eine JavaScript Object Notation (JSON) Darstellung des Feeds in der Antwort zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="a9010-p109">Add the following code, which gets the **Personal** feed type for the current user by using the `/my/Feed` endpoint. The **accept** header requests that the server return a JavaScript Object Notation (JSON) representation of the feed in its response.</span></span>
  
    
    

```

function getMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: feedRetrieved,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("GET error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });    
}

```


## <a name="iterate-through-the-social-feed-and-read-from-it-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="a9010-155">Durchlaufen Sie die Nutzung von sozialen Netzwerken feed und daraus mithilfe des REST-Diensts SharePoint lesen</span><span class="sxs-lookup"><span data-stu-id="a9010-155">Iterate through the social feed and read from it by using the SharePoint REST service</span></span>
<span data-ttu-id="a9010-156"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-156"><a name="bkmk_ReadFeed"> </a></span></span>

<span data-ttu-id="a9010-157">Fügen Sie den folgenden Code, das bereitet der zurückgegebenen Daten mithilfe der **JSON.stringify** und die Funktion **JSON.parse** und dann den Feed durchläuft und dient zum Abrufen der Thread Besitzer und die Stamm-Post-Text.</span><span class="sxs-lookup"><span data-stu-id="a9010-157">Add the following code, which prepares the returned data by using the **JSON.stringify** function and the **JSON.parse** function, and then iterates through the feed and gets the thread's owner and the root post's text.</span></span>
  
    
    

```

function feedRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
 
    var feed = jsonObject.d.SocialFeed.Threads; 
    var threads = feed.results;
    var feedContent = "";
    for (var i = 0; i < threads.length; i++) {
        var thread = threads[i];
        var participants = thread.Actors;
        var owner = participants.results[thread.OwnerIndex].Name;
        feedContent += '<p>' + owner + 
            ' said "' + thread.RootPost.Text + '"</p>';
    }  
    $("#message").html(feedContent); 
}
```


## <a name="run-the-app-for-sharepoint-on-the-developer-site"></a><span data-ttu-id="a9010-158">Ausführen der app für SharePoint auf der Entwicklerwebsite für</span><span class="sxs-lookup"><span data-stu-id="a9010-158">Run the app for SharePoint on the Developer Site</span></span>
<span data-ttu-id="a9010-159"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-159"><a name="bkmk_ReadFeed"> </a></span></span>


1. <span data-ttu-id="a9010-160">Um die app ausgeführt werden soll, wählen Sie die Schaltfläche " **Projekt ausführen** " am unteren Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="a9010-160">To run the app, choose the **Run Project** button at the bottom of the page.</span></span>
    
  
2. <span data-ttu-id="a9010-p110">Wählen Sie die Schaltfläche **Vertrauen sie** **Vertrauen Sie** Sie auf der Seite, die geöffnet wird. Die appseite wird geöffnet und der Name des Besitzers sowie den Text der einzelnen Stamm-Beiträge im Feed angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a9010-p110">In the **Do you trust** page that opens, choose the **Trust It** button. The app page opens and displays the owner's name and the text of each root post in the feed.</span></span>
    
  

  
    
    

## <a name="code-example-publish-a-post-and-get-the-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="a9010-163">Codebeispiel: Veröffentlichen einer POST-Anforderung und den Feed für den aktuellen Benutzer mithilfe des REST-Diensts SharePoint abrufen</span><span class="sxs-lookup"><span data-stu-id="a9010-163">Code example: Publish a post and get the feed for the current user by using the SharePoint REST service</span></span>
<span data-ttu-id="a9010-164"><a name="bkmk_PubPosts1"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-164"><a name="bkmk_PubPosts1"> </a></span></span>

<span data-ttu-id="a9010-p111">Es folgt der vollständige Beispielcode für die Datei app.js aus. Einen Beitrag veröffentlicht, und ruft die persönlich feed für den aktuellen Benutzer, die als JSON-Objekt zurückgegeben wird. Dann durchläuft es den Feed.</span><span class="sxs-lookup"><span data-stu-id="a9010-p111">The following is the complete code example for the App.js file. It publishes a post and gets the personal feed for the current user, which is returned as a JSON object. Then it iterates through the feed.</span></span>
  
    
    

```

var feedManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the feed manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    feedManagerEndpoint = decodeURIComponent(appweburl)+ "/_api/social.feed";
    postToMyFeed();
});

// Publish a post to the current user's feed by using the 
// "<app web URL>/_api/social.feed/my/Feed/Post" endpoint.
function postToMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed/Post",
        type: "POST",
        data: JSON.stringify( { 
            'restCreationData':{
                '__metadata':{ 
                    'type':'SP.Social.SocialRestPostCreationData'
                },
                'ID':null, 
                'creationData':{ 
                    '__metadata':{ 
                        'type':'SP.Social.SocialPostCreationData'
                    },
                'ContentText':'This post was published using REST.',
                'UpdateStatusText':false
                } 
            } 
        }),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: getMyFeed,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("POST error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });
}

// Get the current user's feed by using the 
// "<app web URL>/_api/social.feed/my/Feed" endpoint.
function getMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: feedRetrieved,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("GET error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });    
}

// Parse the JSON data and iterate through the feed.
function feedRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
 
    var feed = jsonObject.d.SocialFeed.Threads; 
    var threads = feed.results;
    var feedContent = "";
    for (var i = 0; i < threads.length; i++) {
        var thread = threads[i];
        var participants = thread.Actors;
        var owner = participants.results[thread.OwnerIndex].Name;
        feedContent += '<p>' + owner + 
            ' said "' + thread.RootPost.Text + '"</p>';
    }  
    $("#message").html(feedContent); 
}
```


## <a name="next-steps"></a><span data-ttu-id="a9010-168">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="a9010-168">Next steps</span></span>
<span data-ttu-id="a9010-169"><a name="bkmk_PubPosts1"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-169"><a name="bkmk_PubPosts1"> </a></span></span>

<span data-ttu-id="a9010-170">Finden Sie unter  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md) und [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) für weitere REST-Endpunkte, die Sie verwenden können, um Features für soziale Netzwerke zugreifen.</span><span class="sxs-lookup"><span data-stu-id="a9010-170">See  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md) and [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) for other REST endpoints that you can use to access social features.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a9010-171">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a9010-171">Additional resources</span></span>
<span data-ttu-id="a9010-172"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a9010-172"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="a9010-173">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-173">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a9010-174">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-174">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a9010-175">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9010-175">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  

