---
title: Vorgehensweise folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2643c286-47c9-4a7a-9273-7474394477d6
ms.openlocfilehash: 56c38ff03d11fc9c66d885d92d572aa1a5bf9286
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="414f1-102">Vorgehensweise: Folgen von Personen mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-102">How to: Follow people by using the JavaScript object model in SharePoint</span></span>
<span data-ttu-id="414f1-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des JavaScript-Objektmodells in SharePoint mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="414f1-103">Learn how to work with Following People features by using the SharePoint JavaScript object model.</span></span>
## <a name="why-use-following-people-features-in-sharepoint"></a><span data-ttu-id="414f1-104">Gründe für die Verwendung von Features zum Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-104">Why use Following People features in SharePoint Server 2013?</span></span>
<span data-ttu-id="414f1-105"><a name="bk_FollowingPeopleFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-105"></span></span>

<span data-ttu-id="414f1-106">In SharePoint helfen Features zum Folgen von Personen den Benutzern, miteinander verbunden zu bleiben.</span><span class="sxs-lookup"><span data-stu-id="414f1-106">In SharePoint, Following People features help users to stay connected with each other.</span></span> <span data-ttu-id="414f1-107">Wenn beispielsweise ein Benutzer einer Person folgt, werden die Beiträge und Aktivitäten dieser Person im Newsfeed des Benutzers angezeigt.</span><span class="sxs-lookup"><span data-stu-id="414f1-107">For example, when a user follows someone, that person's posts and activities show up in the user's newsfeed.</span></span> <span data-ttu-id="414f1-108">Indem Sie Features zum Folgen von Personen nutzen, damit sich Benutzer auf die Personen konzentrieren können, die für sie wichtig sind, können Sie die Relevanz Ihrer App oder Lösung verbessern.</span><span class="sxs-lookup"><span data-stu-id="414f1-108">By using Following People features to focus on the people who users care about, you can improve the relevance of your app or solution.</span></span> <span data-ttu-id="414f1-109">Im JavaScript-Objektmodell werden Personen, denen Sie folgen, durch [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)-Objekte dargestellt.</span><span class="sxs-lookup"><span data-stu-id="414f1-109">In the JavaScript object model, people that you follow are represented by  [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) objects.</span></span> <span data-ttu-id="414f1-110">Zum Durchführen der Hauptaufgaben zum Folgen von Personen im JavaScript-Objektmodel verwenden Sie das [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)-Objekt.</span><span class="sxs-lookup"><span data-stu-id="414f1-110">To perform core Following People tasks in the JavaScript object model, you use the [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) object.</span></span> <span data-ttu-id="414f1-111">In diesem Artikel erfahren Sie, wie Sie mithilfe des JavaScript-Objektmodells mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="414f1-111">This article shows how to use the JavaScript object model to work with Following People features.</span></span>
  
    
    
> <span data-ttu-id="414f1-112">**Hinweis:**
> [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) ist die empfohlene API zum Folgen von Personen und Inhalten.</span><span class="sxs-lookup"><span data-stu-id="414f1-112">**Note:**
[SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) is the recommended API to use for following people and content.</span></span> <span data-ttu-id="414f1-113">Das [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx)-Objekt enthält jedoch zusätzliche Funktionen zum Folgen von Personen, wie die Methode [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) und Methoden, die den Folgen-Status anderer Benutzer abrufen.</span><span class="sxs-lookup"><span data-stu-id="414f1-113">NOTESocialFollowingManager is the recommended API to use for following people and content. However, the [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) object contains additional functionality for following people, such as the [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) method and methods that obtain the following status of other users.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="414f1-114">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Personen mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-114">Prerequisites for setting up your development environment to work with Following People features by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="414f1-115"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-115"></span></span>

<span data-ttu-id="414f1-116">Zum Erstellen der Farmlösung, die das JavaScript-Objektmodell verwendet, um mit Features zum Folgen von Personen zu arbeiten, benötigen Sie:</span><span class="sxs-lookup"><span data-stu-id="414f1-116">To create the farm solution that uses the JavaScript object model to work with Following People features, you'll need:</span></span>
  
    
    

- <span data-ttu-id="414f1-117">SharePoint mit konfigurierter „Meine Website“ und mit Benutzerprofilen und persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer</span><span class="sxs-lookup"><span data-stu-id="414f1-117">SharePoint Server 2013 with My Site configured, and with user profiles and personal sites created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="414f1-118">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="414f1-118">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="414f1-119">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="414f1-119">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="414f1-120">**Vollzugriff auf die Benutzerprofildienst-Anwendung für den angemeldeten Benutzer**</span><span class="sxs-lookup"><span data-stu-id="414f1-120">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  
- <span data-ttu-id="414f1-121">Lokale Administratorberechtigungen für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="414f1-121">Local administrator permissions for the logged-on user</span></span>
    
  

## <a name="create-a-farm-solution-and-application-page-in-visual-studio-2012"></a><span data-ttu-id="414f1-122">Erstellen einer Farm Solution und Anwendung Seite in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="414f1-122">Create a farm solution and application page in Visual Studio 2012</span></span>
<span data-ttu-id="414f1-123"><a name="bk_CreateSolution"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-123"></span></span>


1. <span data-ttu-id="414f1-124">Führen Sie Visual Studio als Administrator aus, und wählen Sie **Datei**, **neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="414f1-124">Run Visual Studio as administrator, and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="414f1-125">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="414f1-125">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="414f1-126">In **der Vorlagenliste** erweitern Sie **Office/SharePoint**, wählen Sie **SharePoint-Lösungen**, und wählen Sie dann die Vorlage **SharePoint - leeres Projekt**.</span><span class="sxs-lookup"><span data-stu-id="414f1-126">In the **Templates** list, expand **Office/SharePoint**, choose **SharePoint Solutions**, and then choose the **SharePoint - Empty Project** template.</span></span>
    
  
4. <span data-ttu-id="414f1-127">Nennen Sie das Projekt FollowPeopleJSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="414f1-127">Name the project FollowPeopleJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="414f1-128">Wählen Sie in das Dialogfeld des **Assistenten zum Anpassen von SharePoint** **als farmlösung bereitstellen**, und wählen Sie dann auf die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="414f1-128">In the **SharePoint Customization Wizard** dialog box, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="414f1-129">Im **Projektmappen-Explorer** das Kontextmenü für das Projekt **FollowPeopleJSOM** öffnen, und fügen Sie eine SharePoint "Layouts" Ordner zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="414f1-129">In **Solution Explorer**, open the shortcut menu for the **FollowPeopleJSOM** project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="414f1-130">Öffnen Sie im Ordner **Layouts** das Kontextmenü für den Ordner **FollowPeopleJSOM**, und fügen Sie anschließend eine neue SharePoint-Anwendungsseite namens „FollowPeople.aspx“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="414f1-130">In the **Layouts** folder, open the shortcut menu for the **FollowPeopleJSOM** folder, and then add a new SharePoint application page namedFollowPeople.aspx.</span></span>
    
   > <span data-ttu-id="414f1-131">**Hinweis:** Die Codebeispiele in diesem Artikel legen benutzerdefinierten Code im Seitenmarkup fest, verwenden jedoch nicht die Code-Behind-Klasse, die Visual Studio für die Seite erstellt.</span><span class="sxs-lookup"><span data-stu-id="414f1-131">**Note** The code examples in this article define custom code in the page markup but do not use the code-behind class that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="414f1-132">Öffnen Sie das Kontextmenü für die Seite „FollowPeople.aspx“, und wählen Sie dann **Als Startelement festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="414f1-132">Open the shortcut menu for the FollowPeople.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="414f1-p103">Fügen Sie im Markup der Datei „FollowPeople.aspx“ den folgenden Code zwischen den **asp:Content**-Haupttags hinzu. Dieser Code definiert Steuerelemente und Skriptverweise.</span><span class="sxs-lookup"><span data-stu-id="414f1-p103">In the markup of the FollowPeople.aspx file, paste the following code between the "Main" **asp:Content** tags. This code defines controls and script references.</span></span>
    
```HTML
<span id="followResults"></span><br/><br />
<button id="sendRequest" type="button"></button><br/>
<span id="message" style="color: #FF0000;"></span>
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js" type="text/javascript"></script>
<SharePoint:ScriptLink name="SP.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink name="SP.UserProfiles.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:FormDigest id="FormDigest" runat="server"/>
<script type="text/javascript">
    // Replace this comment with the code for your scenario. 
</script>
```

   > <span data-ttu-id="414f1-135">**Hinweis:** Im Beispiel „Abrufen von Followern und gefolgten Personen“ wird das Schaltflächen-Steuerelement oder das Formulardigest-Steuerelement nicht verwendet, da es nur für Vorgänge erforderlich ist, die Serverinhalte aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="414f1-135">**Note** The "Get followers and followed people" example doesn't use the button control or the form digest control, which is only required for operations that update server content. A form digest generates a message digest used for security validation.</span></span> <span data-ttu-id="414f1-136">Ein Formulardigest generiert einen Nachrichtenhash zur Sicherheitsprüfung. </span><span class="sxs-lookup"><span data-stu-id="414f1-136">A form digest generates a message digest used for security validation.</span></span> 

10. <span data-ttu-id="414f1-137">Ersetzen Sie den Kommentar zwischen den **script**-Tags durch den Beispielcode aus einem der folgenden Szenarios:</span><span class="sxs-lookup"><span data-stu-id="414f1-137">Replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="414f1-138">Starten oder Beenden von Personen folgen</span><span class="sxs-lookup"><span data-stu-id="414f1-138">Start or stop following people</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_FollowPeople)  
  -  [<span data-ttu-id="414f1-139">Nachfolgende Aktivitäten und beobachteter Personen heranziehen.</span><span class="sxs-lookup"><span data-stu-id="414f1-139">Get followers and followed people</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_GetFollowers)
    
11. <span data-ttu-id="414f1-140">Wählen Sie zum Testen der Lösung auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="414f1-140">To test the solution, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="414f1-141">Codebeispiel: Starten oder beenden nach Personen, für die mithilfe der SharePoint JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="414f1-141">Code example: Start or stop following people by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="414f1-142"><a name="bk_FollowPeople"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-142"></span></span>

<span data-ttu-id="414f1-p105">Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder einen Zielbenutzer nach Beenden. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="414f1-p105">The following code example makes the current user start following or stop following a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="414f1-145">Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="414f1-145">Check whether the current user is following a target user by using the  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="414f1-146">Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="414f1-146">Get the count of people who the current user is following by using the  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="414f1-147">Starten Sie den Zielbenutzer mithilfe der Methode  [Führen Sie die](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) folgenden.</span><span class="sxs-lookup"><span data-stu-id="414f1-147">Start following the target user by using the  [follow](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="414f1-148">Beenden Sie das Folgen des Zielbenutzers mithilfe der [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="414f1-148">Stop following the target user by using the  [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx) method.</span></span>
    
  

> <span data-ttu-id="414f1-149">**Hinweis:** Fügen Sie den folgenden Code zwischen den **script**-Tags ein, die Sie im Verfahren [Erstellen einer Farmlösung und Anwendungsseite](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="414f1-149">**Note** Paste the following code between the **script** tags that you added in the [Create a farm solution and application page](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) procedure.</span></span> <span data-ttu-id="414f1-150">Ändern Sie dann den Platzhalterwert für die Variable **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="414f1-150">Note Change the placeholder value for the serverUrl variable before you run the code.</span></span>
  
    
    


```

// Replace the placeholder value with the account name of the target user.
var targetUser = 'domain\\userName';

var clientContext;
var followingManager;
var actorInfo;
var isFollowed;
var followedCount;

// Ensure that the SP.UserProfiles.js file is loaded before running your code.
$(document).ready(function () {
    SP.SOD.executeOrDelayUntilScriptLoaded(getFollowingStatus, 'SP.UserProfiles.js');
});

// Get the Following status of the current user.
function getFollowingStatus() {

    // Get the current client context.
    clientContext = SP.ClientContext.get_current();

    // Get the SocialFeedManager instance.
    followingManager = new SP.Social.SocialFollowingManager(clientContext);

    // Create a SocialActorInfo object to represent the target user.
    actorInfo = new SP.Social.SocialActorInfo();
    actorInfo.set_accountName(targetUser);

    // Find out whether the current user is following the target user.
    isFollowed = followingManager.isFollowed(actorInfo);
    followedCount = followingManager.getFollowedCount(1);

    // Get the information from the server.
    clientContext.executeQueryAsync(showFollowingStatus, requestFailed)
}

// Show the Following status of the current user.
function showFollowingStatus() {
    var results = '';
    results += 'Is the current user following the target user? ' + isFollowed.get_value();
    results += '<br/>Total count of followed people: ' + followedCount.get_value();
    $('#followResults').html(results);

    // Initialize the button for this example.
    $('#sendRequest').click(
        function () {
            $('#message').empty();
            toggleFollowingStatus();
        });
    $('#sendRequest').text('Toggle following status');
}

// Follow or stop following the target user.
function toggleFollowingStatus() {
    if (isFollowed.get_value() === false) {
        followingManager.follow(actorInfo);
    }
    else if (isFollowed.get_value() === true) {
        followingManager.stopFollowing(actorInfo);
    }
    clientContext.executeQueryAsync(getFollowingStatus, requestFailed);
}

// Failure callback.
function requestFailed(sender, args) {
    $('#message').html('Error: ' + args.get_message());
}
```


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="414f1-151">Codebeispiel: Abrufen von Followern und gefolgten Personen mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-151">Code example: Get followers and followed people by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="414f1-152"><a name="bk_GetFollowers"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-152"></span></span>

<span data-ttu-id="414f1-p107">Das folgende Codebeispiel ruft die Personen, die der aktuelle Benutzer folgt und ruft die Personen, die vom aktuellen Benutzer eingehalten werden. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="414f1-p107">The following code example gets the people who the current user is following and gets the people who are followed by the current user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="414f1-155">Rufen Sie die Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="414f1-155">Get the people who the current user is following by using the  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="414f1-156">Rufen Sie die Personen, die den aktuellen Benutzer folgen, indem Sie mithilfe der Methode  [GetFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) und übergeben **1** **User** Actor Typen dargestellt.</span><span class="sxs-lookup"><span data-stu-id="414f1-156">Get the people who are following the current user by using the  [getFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) method and passing **1** to represent **User** actor types.</span></span>
    
  
- <span data-ttu-id="414f1-157">Iterieren Sie durch die Gruppen von Personen, und rufen Sie den Anzeigenamen, den persönlichen Website-URI und den Bild-URI jeder Person ab.</span><span class="sxs-lookup"><span data-stu-id="414f1-157">Iterate through the groups of people and get each person's display name, personal site URI, and picture URI.</span></span>
    
  

> <span data-ttu-id="414f1-158">**Hinweis:** Fügen Sie den folgenden Code zwischen den **script**-Tags ein, die Sie im Verfahren [Erstellen einer Farmlösung und Anwendungsseite](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="414f1-158">**Note** Paste the following code between the **script** tags that you added in the [Create a farm solution and application page](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) procedure.</span></span>
  
    
    


```

var followed;
var followers;

// Ensure that the SP.UserProfiles.js file is loaded before running your code.
$(document).ready(function () {
    SP.SOD.executeOrDelayUntilScriptLoaded(getFollowedAndFollowers, 'SP.UserProfiles.js');

    // Hide the button for this example.
    $('#sendRequest').hide();
});

// Get the Following status of the current user.
function getFollowedAndFollowers() {

    // Get the current client context.
    var clientContext = SP.ClientContext.get_current();

    // Get the SocialFeedManager instance.
    var followingManager = new SP.Social.SocialFollowingManager(clientContext);

    // Get followed people and followers.
    followers = followingManager.getFollowers();
    followed = followingManager.getFollowed(1);

    // Send the request to the server.
    clientContext.executeQueryAsync(showFollowedAndFollowers, requestFailed)
}

// Show the Following status of the current user.
function showFollowedAndFollowers() {
    var results = 'The current user is following ' + followed.length + ' people: <br/>';

    for (var i = 0; i < followed.length; i++) {
        var user = followed[i];
        var name = user.get_name();
        var personalSiteUri = user.get_personalSiteUri();
        var pictureUri = user.get_imageUri();

        results += '<br/>' + name + '<br/>' + personalSiteUri + '<br/>' + pictureUri + '<br/>';
    }

    results += '<br/>The current user is followed by ' + followers.length + ' people: <br/>';

    for (var i = 0; i < followers.length; i++) {
        var user = followers[i];
        var name = user.get_name();
        var personalSiteUri = user.get_personalSiteUri();
        var pictureUri = user.get_imageUri();

        results += '<br/>' + name + '<br/>' + personalSiteUri + '<br/>' + pictureUri + '<br/>';
    }
    $('#followResults').html(results);
}

// Failure callback.
function requestFailed(sender, args) {
    $('#message').html('Error: ' + args.get_message());
}
```


## <a name="additional-resources"></a><span data-ttu-id="414f1-159">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="414f1-159">Additional resources</span></span>
<span data-ttu-id="414f1-160"><a name="bk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="414f1-160"></span></span>


-  [<span data-ttu-id="414f1-161">Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-161">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="414f1-162">Vorgehensweise: führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint</span><span class="sxs-lookup"><span data-stu-id="414f1-162">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

