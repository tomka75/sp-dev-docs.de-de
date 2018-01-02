---
title: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6e1ca38-134f-428a-8d21-b8b2615b161b
ms.openlocfilehash: 23aead2b760bf039faae271ad26ca138e9770244
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="retrieve-user-profile-properties-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="caa54-102">Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="caa54-102">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>

<span data-ttu-id="caa54-103">In diesem Artikel erfahren Sie, wie Sie Benutzereigenschaften und Benutzerprofileigenschaften programmgesteuert mithilfe des JavaScript-Objektmodells in SharePoint abrufen.</span><span class="sxs-lookup"><span data-stu-id="caa54-103">Learn how to retrieve user properties and user profile properties programmatically by using the SharePoint JavaScript object model.</span></span>

## <a name="what-are-user-properties-and-user-profile-properties-in-sharepoint"></a><span data-ttu-id="caa54-104">Was sind Benutzereigenschaften und Benutzerprofileigenschaften in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="caa54-104">What are user properties and user profile properties in SharePoint?</span></span>
<span data-ttu-id="caa54-105"><a name="bkmk_WhatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-105"><a name="bkmk_WhatIs"> </a></span></span>

<span data-ttu-id="caa54-p101">Benutzereigenschaften und Benutzerprofileigenschaften liefern Informationen über SharePoint-Benutzer, wie Anzeigename, E-Mail, Titel und andere geschäftliche oder persönliche Daten. In clientseitigen APIs greifen Sie auf diese Eigenschaften über das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt und seine  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft zu. Die  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft enthält alle Benutzerprofileigenschaften, aber das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt beinhaltet die normalerweise verwendeten Eigenschaften (wie  [accountName](http://msdn.microsoft.com/library/ad1551bf-dad8-d54e-880a-8a4388fad44e%28Office.15%29.aspx),  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx) und [email](http://msdn.microsoft.com/library/74302f73-aaf6-920b-0605-812b0dbf4568%28Office.15%29.aspx)), auf die leichter zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="caa54-p101">User properties and user profile properties provide information about SharePoint users, such as display name, email, title, and other business and personal information. In client-side APIs, you access these properties from the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object and its [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property. The [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property contains all user profile properties, but the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object contains commonly used properties (such as [accountName](http://msdn.microsoft.com/library/ad1551bf-dad8-d54e-880a-8a4388fad44e%28Office.15%29.aspx),  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx), and  [email](http://msdn.microsoft.com/library/74302f73-aaf6-920b-0605-812b0dbf4568%28Office.15%29.aspx)) that are easier to access.</span></span>
  
    
    
<span data-ttu-id="caa54-109">Das  [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx)-Objekt enthält die folgenden Methoden zum Abrufen von Benutzereigenschaften und Benutzerprofileigenschaften über das JavaScript-Objektmodell:</span><span class="sxs-lookup"><span data-stu-id="caa54-109">The  [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) object includes the following methods that you can use to retrieve user properties and user profile properties by using the JavaScript object model:</span></span>
  
    
    

- <span data-ttu-id="caa54-110">Die  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx)-Methode und die  [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx)-Methode geben ein  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="caa54-110">The  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) method and the [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) method return a [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object.</span></span>
    
  
- <span data-ttu-id="caa54-111">Die  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode und die  [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx)-Methode geben die von Ihnen angegebenen Werte der Benutzerprofileigenschaften zurück.</span><span class="sxs-lookup"><span data-stu-id="caa54-111">The  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method and the [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) method return the values of the user profile properties that you specify.</span></span>
    
  
<span data-ttu-id="caa54-p102">Benutzerprofileigenschaften von Client-APIs sind schreibgeschützt (mit Ausnahme des Profilbilds, das Sie mithilfe der  [PeopleManager.setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx)-Methode ändern können). Wenn Sie weitere Benutzerprofileigenschaften ändern möchten, verwenden Sie das Serverobjektmodell. Weitere Informationen zum Arbeiten mit Benutzerprofilen finden Sie unter  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="caa54-p102">User profile properties from client APIs are read-only (except the profile picture, which you can change by using the  [PeopleManager.setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx) method). If you want to change other user profile properties, you must use the server object model. For more information about working with user profiles, see [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="caa54-115">Das clientseitige [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx)-Objekt enthält im Gegensatz zur serverseitigen Version nicht alle Benutzereigenschaften.</span><span class="sxs-lookup"><span data-stu-id="caa54-115">Note: The client-side  [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx) object doesn't contain all of the user properties as the server-side version.</span></span> <span data-ttu-id="caa54-116">Allerdings stellt die clientseitige Version die Methoden zum Erstellen einer persönlichen Website für den aktuellen Benutzer bereit.</span><span class="sxs-lookup"><span data-stu-id="caa54-116">However, the client-side version does provide the methods for creating a personal site for the current user.</span></span> <span data-ttu-id="caa54-117">Verwenden Sie zum Abrufen die [ProfileLoader.getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx)-Methode.</span><span class="sxs-lookup"><span data-stu-id="caa54-117">To retrieve it, use the [ProfileLoader.getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx) method.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-properties-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="caa54-118">Voraussetzungen für das Einrichten der Entwicklungsumgebung zum Abrufen von Benutzereigenschaften über das SharePoint JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="caa54-118">Prerequisites for setting up your development environment to retrieve user properties by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="caa54-119"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-119"><a name="bk_Prereqs"> </a></span></span>

<span data-ttu-id="caa54-120">Um eine Anwendungsseite zu erstellen, die das JavaScript-Objektmodell zum Abrufen von Benutzereigenschafen verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="caa54-120">To create an application page that uses the JavaScript object model to retrieve user properties, you'll need:</span></span>
  
    
    

- <span data-ttu-id="caa54-121">SharePoint mit Profilen, die für den aktuellen Benutzer und einen Zielbenutzer erstellt wurden</span><span class="sxs-lookup"><span data-stu-id="caa54-121">SharePoint with profiles created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="caa54-122">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="caa54-122">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="caa54-123">Office Developer Tools für Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="caa54-123">Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="caa54-124">Verbindungsberechtigungen für den **Vollzugriff**, um auf die Benutzerprofildienst-Anwendung für den aktuellen Benutzer zugreifen zu können</span><span class="sxs-lookup"><span data-stu-id="caa54-124">**Full Control** connection permissions to access the User Profile service application for the current user</span></span>
    
  

## <a name="create-the-application-page-in-visual-studio-2012"></a><span data-ttu-id="caa54-125">Erstellen der Anwendungsseite in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="caa54-125">Create the application page in Visual Studio 2012</span></span>
<span data-ttu-id="caa54-126"><a name="bk_CreateAppPage"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-126"><a name="bk_CreateAppPage"> </a></span></span>


1. <span data-ttu-id="caa54-127">Öffnen Sie auf dem Server, auf dem SharePoint ausgeführt wird, Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="caa54-127">On the server running SharePoint, open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="caa54-128">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="caa54-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="caa54-129">Erweitern Sie in der Liste **Vorlagen** das Element **Office/SharePoint**, wählen Sie die Kategorie **SharePoint-Lösungen** und dann die Vorlage **SharePoint-Projekt**.</span><span class="sxs-lookup"><span data-stu-id="caa54-129">In the **Templates** list, expand **Office/SharePoint**, choose the **SharePoint Solutions** category, and then choose the **SharePoint Project** template.</span></span>
    
  
4. <span data-ttu-id="caa54-130">Benennen Sie das Projekt mit UserProfilesJSOM, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="caa54-130">Name the project UserProfilesJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="caa54-131">Geben Sie im Dialogfeld **Assistent zum Anpassen von SharePoint** die URL zu Ihrer Ziel-SharePoint-Website, wählen Sie **Als Farmlösung bereitstellen**, und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="caa54-131">In the **SharePoint Customization Wizard** dialog box, enter the URL to your target SharePoint site, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="caa54-132">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für dasUserProfilesJSOM-Projekt, und fügen Sie dann einen zugeordneten SharePoint-Ordner "Layouts" hinzu.</span><span class="sxs-lookup"><span data-stu-id="caa54-132">In **Solution Explorer**, open the shortcut menu for the UserProfilesJSOM project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="caa54-133">Öffnen Sie im Ordner **Layouts** das Kontextmenü für den Ordner „UserProfilesJSOM“, und fügen Sie anschließend eine neue SharePoint-Anwendungsseite mit dem Namen „UserProfiles.aspx“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="caa54-133">In the **Layouts** folder, open the shortcut menu for theUserProfilesJSOM folder, and then add a new SharePoint application page namedUserProfiles.aspx.</span></span>
    
   > <span data-ttu-id="caa54-134">Hinweis: Die Codebeispiele in diesem Artikel legen benutzerdefinierten Code im Seitenmarkup fest, verwenden aber nicht die Code-Behind Class-Datei, die Visual Studio für die Seite erstellt.</span><span class="sxs-lookup"><span data-stu-id="caa54-134">Note: The code examples in this article define custom code in the page markup but do not use the code-behind class file that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="caa54-135">Öffnen Sie das Kontextmenü für die Seite „UserProfiles.aspx“, und wählen Sie dann **Als Startelement festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="caa54-135">Open the shortcut menu for the UserProfiles.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="caa54-p104">Fügen Sie in das Markup der Seite "UserProfiles.aspx" den folgenden Code zwischen die Haupt- **asp:Content**-Tags ein. Dieser Code fügt ein **span**-Steuerelement, das die Abfrageergebnisse anzeigt, **SharePoint:ScriptLink**-Steuerelemente, die SharePoint JavaScript Class-Bibliotheksdateien und **script**-Tags einfügt, die Ihre benutzerdefinierte Logik enthalten.</span><span class="sxs-lookup"><span data-stu-id="caa54-p104">In the markup for the UserProfiles.aspx page, paste the following code inside the "Main" **asp:Content** tags. This code adds a **span** control that displays the results of the query, **SharePoint:ScriptLink** controls that reference SharePoint JavaScript class library files, and **script** tags to contain your custom logic.</span></span>
    
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

10. <span data-ttu-id="caa54-138">Um Logik für das Abrufen von Benutzerprofileigenschaften hinzuzufügen, ersetzen Sie den Kommentar zwischen den **script**-Tags durch das Codebeispiel für eines der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="caa54-138">To add logic to retrieve user profile properties, replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="caa54-139">Abrufen von Benutzerprofileigenschaften aus dem "PersonProperties"-Objekt und der "userProfileProperties"-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="caa54-139">Retrieve user profile properties from the PersonProperties object and its userProfileProperties property</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_examplePersonPropsObj)  
  -  [<span data-ttu-id="caa54-140">Abrufen einer Gruppe von Benutzerprofileigenschaften mithilfe der "getUserProfilePropertiesFor"-Methode</span><span class="sxs-lookup"><span data-stu-id="caa54-140">Retrieve a set of user profile properties by using the getUserProfilePropertiesFor method</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_exampleGetUPMethod)
    
  
11. <span data-ttu-id="caa54-p105">Um die Anwendungsseite zu testen, wählen Sie in der Menüleiste die Optionen **Debuggen**, **Debuggen starten**. Wenn Sie aufgefordert werden, die Datei "web.config" zu ändern, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="caa54-p105">To test the application page, on the menu bar, choose **Debug**, **Start Debugging**. If you're prompted to modify the web.config file, choose the **OK** button.</span></span>
    
  

## <a name="code-example-retrieving-user-profile-properties-from-the-personproperties-object-and-its-userprofileproperties-property-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="caa54-143">Codebeispiel: Abrufen von Benutzerprofileigenschaften aus dem "PersonProperties"-Objekt und der "userProfileProperties-Eigenschaft im SharePoint JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="caa54-143">Code example: Retrieving user profile properties from the PersonProperties object and its userProfileProperties property in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="caa54-144"><a name="bk_examplePersonPropsObj"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-144"><a name="bk_examplePersonPropsObj"> </a></span></span>

<span data-ttu-id="caa54-p106">Das folgende Codebeispiel erklärt, wie Sie Benutzerprofileigenschaften für einen Zielbenutzer abrufen, indem Sie das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt und seine  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft anfordern. Es zeigt die Vorgehensweise:</span><span class="sxs-lookup"><span data-stu-id="caa54-p106">The following code example shows how to get user profile properties for a target user by querying the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object and its [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="caa54-p107">Rufen Sie das  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt ab, das für den Zielbenutzer steht, indem Sie die  [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx)-Methode anwenden. (Zum Abrufen des  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekts für den aktuellen Benutzer verwenden Sie die  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx)-Methode.)</span><span class="sxs-lookup"><span data-stu-id="caa54-p107">Get the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object that represents the target user by using the [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) method. (To get the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object for the current user, use the [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) method.)</span></span>
    
  
- <span data-ttu-id="caa54-p108">Rufen Sie eine Eigenschaft direkt aus dem  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekt ab. In diesem Beispiel wird die  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx)-Eigenschaft abgerufen.</span><span class="sxs-lookup"><span data-stu-id="caa54-p108">Get a property directly from the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object. This example gets the [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx) property.</span></span>
    
  
- <span data-ttu-id="caa54-p109">Erhalten Sie eine Eigenschaft von der [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx)-Eigenschaft des [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)-Objekts. In diesem Beispiel wird die **Department**-Eigenschaft abgerufen.</span><span class="sxs-lookup"><span data-stu-id="caa54-p109">Get a property from the  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property of the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object. This example gets the **Department** property.</span></span>
    
> [!NOTE]
> <span data-ttu-id="caa54-153">Fügen Sie den folgenden Code zwischen den **script**-Tags ein, den Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) zur Seite „UserProfiles.aspx“ hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="caa54-153">Note: Paste the following code between the **script** tags that you added to the UserProfiles.aspx file in the [Create the application page](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) procedure.</span></span> <span data-ttu-id="caa54-154">Ersetzen Sie den `domainName\\userName`-Platzhalterwert, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="caa54-154">Replace the `domainName\\userName` placeholder value before you run the code.</span></span> <span data-ttu-id="caa54-155">(In diesem Codebeispiel wird die Code-Behind Class-Datei nicht verwenden.)</span><span class="sxs-lookup"><span data-stu-id="caa54-155">(This code example does not use the code-behind class file.)</span></span>
  
    
    


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


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-getuserprofilepropertiesfor-method-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="caa54-156">Codebeispiel: Abrufen einer Gruppe von Benutzerprofileigenschaften mithilfe der „getUserProfilePropertiesFor“-Methode im SharePoint JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="caa54-156">Code example: Retrieving a set of user profile properties by using the getUserProfilePropertiesFor method in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="caa54-157"><a name="bk_exampleGetUPMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-157"><a name="bk_exampleGetUPMethod"> </a></span></span>

<span data-ttu-id="caa54-p111">Im folgenden Codebeispiel werden die Werte einer bestimmten Gruppe von Benutzerprofileigenschaften für einen Zielbenutzer mithilfe der  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode abgerufen. Es zeigt die Vorgehensweise:</span><span class="sxs-lookup"><span data-stu-id="caa54-p111">The following code example retrieves the values for a specified set of user profile properties for a target user by using the  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="caa54-p112">Erstellen Sie ein  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx)-Objekt, das den Zielbenutzer und die abzurufenden Benutzerprofileigenschaften angibt. In diesem Beispiel werden die **PreferredName**-Eigenschaft und die **Department**-Eigenschaft abgerufen.</span><span class="sxs-lookup"><span data-stu-id="caa54-p112">Create a  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx) object that specifies the target user and the user profile properties to retrieve. This example gets the **PreferredName** property and the **Department** property.</span></span>
    
  
- <span data-ttu-id="caa54-p113">Rufen Sie die Werte der angegebenen Eigenschaft mithilfe der  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)-Methode ab, und übergeben Sie die Werte an das  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx)-Objekt. (Zum Abrufen des Werts von nur einer Benutzerprofileigenschaft verwenden Sie die  [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx)-Methode.)</span><span class="sxs-lookup"><span data-stu-id="caa54-p113">Get the values of the specified properties by using the  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method and passing in the [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx) object. (To retrieve the value for only one user profile property, use the [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) method.)</span></span>
    
  
- <span data-ttu-id="caa54-164">Rufen Sie die Werte aus dem zurückgegebenen Array von Eigenschaftswerten ab.</span><span class="sxs-lookup"><span data-stu-id="caa54-164">Get the values from the returned array of property values.</span></span>
    
> [!NOTE]
> <span data-ttu-id="caa54-165">Fügen Sie den folgenden Code zwischen den **script**-Tags ein, den Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) zur Seite „UserProfiles.aspx“ hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="caa54-165">Note: Paste the following code between the **script** tags that you added to the UserProfiles.aspx file in the [Create the application page](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) procedure.</span></span> <span data-ttu-id="caa54-166">Ersetzen Sie den `domainName\\\\userName`-Platzhalterwert, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="caa54-166">Replace the `domainName\\\\userName` placeholder value before you run the code.</span></span> <span data-ttu-id="caa54-167">(In diesem Codebeispiel wird die Code-Behind Class-Datei nicht verwenden.)</span><span class="sxs-lookup"><span data-stu-id="caa54-167">(This code example does not use the code-behind class file.)</span></span>
  
    
    


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


## <a name="see-also"></a><span data-ttu-id="caa54-168">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="caa54-168">See also</span></span>
<span data-ttu-id="caa54-169"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="caa54-169"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="caa54-170">Arbeiten mit Benutzerprofilen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="caa54-170">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="caa54-171">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="caa54-171">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [<span data-ttu-id="caa54-172">Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="caa54-172">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [<span data-ttu-id="caa54-173">SP.UserProfiles-Namespace (sp.userprofiles)</span><span class="sxs-lookup"><span data-stu-id="caa54-173">SP.UserProfiles namespace (sp.userprofiles)</span></span>](http://msdn.microsoft.com/library/8c1fcceb-cd9a-b25c-32f4-1cfb0578278c%28Office.15%29.aspx)
    
  

