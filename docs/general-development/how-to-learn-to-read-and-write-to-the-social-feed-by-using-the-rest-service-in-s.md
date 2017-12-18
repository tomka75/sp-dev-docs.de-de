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
# <a name="read-and-write-to-the-social-feed-by-using-the-rest-service-in-sharepoint"></a>Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des REST-Diensts in SharePoint

Erstellen Sie eine von SharePoint gehostete App, die den REST-Dienst zum Veröffentlichen eines Beitrags und zum Abrufen des persönlichen Feeds für den aktuellen Benutzer verwendet.

## <a name="prerequisites-for-creating-a-sharepoint-hosted-sharepoint-add-in-that-publishes-a-post-and-gets-the-social-feed-by-using-the-sharepoint-rest-service"></a>Voraussetzungen für das Erstellen einer SharePoint-Hosting SharePoint-Add-In, die einen Beitrag veröffentlicht und ruft den Feed für soziale Netzwerke mithilfe des REST-Diensts SharePoint
<a name="bkmk_Prereqs"> </a>

In diesem Artikel wird davon ausgegangen, dass Sie die SharePoint-Add-In mithilfe einer Napa- oder Office 365-Entwicklerwebsite erstellen. Wenn Sie diese Entwicklungsumgebung verwenden, sind die Voraussetzungen bereits erfüllt.
  
    
    

> **Hinweis:** Unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) erhalten Sie Informationen zur Registrierung für eine Entwicklerwebsite und zu den ersten Schritten mit Napa.
  
    
    

Wenn Sie nicht mit Napa auf einer Entwicklerwebsite arbeiten, benötigen Sie Folgendes:
  
    
    

- SharePoint mit Meine Website konfiguriert und mit einer persönlichen Website für den aktuellen Benutzer erstellt
    
  
- Visual Studio 2012 und Office Developer Tools für Visual Studio 2013
    
  
- Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer
    
  

> **Hinweis:** Anleitungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von Apps für Office und SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx). 
  
    
    


## <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a>Kernkonzepte zum Arbeiten mit sozialen Feeds in SharePoint
<a name="bkmk_CoreConcepts"> </a>

Die SharePoint-hosted app, die Sie in diesem Artikel erstellen verwendet JavaScript zu erstellen und Senden von HTTP-Anfragen an Endpunkten Representational State Transfer (REST). Diese Anfragen einen Beitrag veröffentlichen und Personal-feed für den aktuellen Benutzer abzurufen. Tabelle 1 enthält Links zu Artikeln, in denen allgemeine Konzepte zu, die Sie kennen sollten beschreiben, bevor Sie beginnen.
  
    
    

**In Tabelle 1. Zentrale Konzepte für die Arbeit mit sozialen Feeds SharePoint**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Informationen Sie zu SharePoint-Add-Ins und grundlegende Konzepte für deren Erstellung.  <br/> |
| [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie die Programmierung mit sozialen Feeds und Microblog Beiträge, folgen von Personen und Inhalten (Dokumente, Websites und tags.md), und Arbeiten mit Benutzerprofilen zu starten.  <br/> |
| [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md) <br/> |Informationen Sie zu allgemeinen Programmieraufgaben zum Arbeiten mit sozialen Feeds und die API, die Sie zum Ausführen der Aufgaben verwenden.  <br/> |
   

## <a name="create-the-sharepoint-add-in-project"></a>Erstellen Sie das SharePoint-Add-In-Projekt.
<a name="bkmk_CreateApp"> </a>


1. Klicken Sie auf Ihrer Entwicklerwebsite öffnen Sie Napa, und wählen Sie dann auf **Neues Projekt hinzufügen**.
    
  
2. Wählen Sie die Vorlage **App für SharePoint**, nennen Sie das Projekt SocialFeedREST, und wählen Sie dann auf die Schaltfläche **Erstellen**.
    
  
3. Geben Sie die Berechtigungen an, die Ihre App benötigt:
    
  a. Wählen Sie die Schaltfläche **Eigenschaften** am unteren Rand der Seite.
     
  b. Wählen Sie im Fenster **Eigenschaften****Berechtigungen**.
    
  c. Legen Sie **die Inhaltskategorie****Write** Berechtigungen für den **Mandanten** Bereich.
    
  d. Legen Sie in der Kategorie **für soziale Netzwerke****Read**-Berechtigungen für den Bereich **Von Benutzerprofilen**.
    
  e. Das Fenster **Eigenschaften** zu schließen.
    
4. Erweitern Sie den Knoten **Skripts**, wählen Sie die Datei App.js, und löschen Sie den Inhalt der Datei.
    
  

## <a name="post-to-the-social-feed-by-using-the-sharepoint-rest-service"></a>Veröffentlichen Sie den Feed für soziale Netzwerke mithilfe der SharePoint REST-Dienst
<a name="bkmk_PubPost"> </a>


1. Deklarieren Sie eine globale Variable für die URL des Endpunkts **SocialFeedManager**, in der Datei App.js.
    
```
var feedManagerEndpoint;
```

2. Fügen Sie den folgenden Code, die Ruft den **SPAppWebUrl** -Parameter aus der Abfragezeichenfolge ab und wird verwendet, um den **SocialFeedManager** -Endpunkt zu erstellen.
    
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

3. Fügen Sie den folgenden Code, in dem die **POST** HTTP-Anforderung für den Endpunkt `/my/Feed/Post` erstellt, definiert die Bereitstellungsdaten Erstellung und im Beitrag veröffentlicht.
    
    Die Anforderung sendet eine Ressource **SocialRestPostCreationData** im Textkörper Anforderung. **SocialRestPostCreationData** enthält das Ziel für die Bereitstellung (in diesem Fall `null` an einen Stammbeitrag für den aktuellen Benutzer) und **SocialPostCreationData** komplexen Typs, die im Beitrag Eigenschaften definiert.
    


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


## <a name="retrieve-the-social-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a>Abrufen von den Feed für soziale Netzwerke für den aktuellen Benutzer mithilfe des REST-Diensts SharePoint
<a name="bkmk_GetFeed"> </a>

Fügen Sie den folgenden Code, der den Typ für den aktuellen Benutzer mithilfe des  `/my/Feed` Endpunkts feed **Personal** abgerufen. Die Kopfzeile **accept** fordert an, dass der Server eine JavaScript Object Notation (JSON) Darstellung des Feeds in der Antwort zurückgeben.
  
    
    

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


## <a name="iterate-through-the-social-feed-and-read-from-it-by-using-the-sharepoint-rest-service"></a>Durchlaufen Sie die Nutzung von sozialen Netzwerken feed und daraus mithilfe des REST-Diensts SharePoint lesen
<a name="bkmk_ReadFeed"> </a>

Fügen Sie den folgenden Code, das bereitet der zurückgegebenen Daten mithilfe der **JSON.stringify** und die Funktion **JSON.parse** und dann den Feed durchläuft und dient zum Abrufen der Thread Besitzer und die Stamm-Post-Text.
  
    
    

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


## <a name="run-the-app-for-sharepoint-on-the-developer-site"></a>Ausführen der app für SharePoint auf der Entwicklerwebsite für
<a name="bkmk_ReadFeed"> </a>


1. Um die app ausgeführt werden soll, wählen Sie die Schaltfläche " **Projekt ausführen** " am unteren Rand der Seite.
    
  
2. Wählen Sie die Schaltfläche **Vertrauen sie** **Vertrauen Sie** Sie auf der Seite, die geöffnet wird. Die appseite wird geöffnet und der Name des Besitzers sowie den Text der einzelnen Stamm-Beiträge im Feed angezeigt.
    
  

  
    
    

## <a name="code-example-publish-a-post-and-get-the-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a>Codebeispiel: Veröffentlichen einer POST-Anforderung und den Feed für den aktuellen Benutzer mithilfe des REST-Diensts SharePoint abrufen
<a name="bkmk_PubPosts1"> </a>

Es folgt der vollständige Beispielcode für die Datei app.js aus. Einen Beitrag veröffentlicht, und ruft die persönlich feed für den aktuellen Benutzer, die als JSON-Objekt zurückgegeben wird. Dann durchläuft es den Feed.
  
    
    

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


## <a name="next-steps"></a>Nächste Schritte
<a name="bkmk_PubPosts1"> </a>

Finden Sie unter  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md) und [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) für weitere REST-Endpunkte, die Sie verwenden können, um Features für soziale Netzwerke zugreifen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addResources"> </a>


-  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  

