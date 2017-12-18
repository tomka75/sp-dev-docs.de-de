---
title: "Hinzufügen eines Sicherheitstrim-Codeausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4beaab08-760b-408a-b768-906312779379
ms.openlocfilehash: 823a5fdc6f6f9d229a0020fd42211ffb05df03af
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="add-a-security-trim-snippet-in-sharepoint"></a><span data-ttu-id="069f0-102">Hinzufügen eines Sicherheitstrim-Codeausschnitts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="069f0-102">How to: Add a Security Trim snippet in SharePoint</span></span>

<span data-ttu-id="069f0-103">Sie können einen Codeausschnitt für die Sicherheitskürzung verwenden, um Inhalte nur bestimmten Benutzern basierend auf einer bestimmten Berechtigung, über die diese Benutzer verfügen müssen, und abhängig davon, ob es sich um authentifizierte oder anonyme Benutzer handelt, anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="069f0-103">You can use a Security Trim snippet to display content only to specific users, based on a specific permission that those users must have and whether the users are authenticated or anonymous.</span></span>

## <a name="introduction-to-the-security-trim-snippet"></a><span data-ttu-id="069f0-104">Einführung in die Sicherheit erhöhen, Ausschnitt</span><span class="sxs-lookup"><span data-stu-id="069f0-104">Introduction to the Security Trim snippet</span></span>
<span data-ttu-id="069f0-105"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="069f0-105"><a name="Introduction"> </a></span></span>

<span data-ttu-id="069f0-p101">Sie können einen Ausschnitt Sicherheit erhöhen, anzuzeigenden Inhalt nur für bestimmte Benutzer, basierend auf eine bestimmte Berechtigung, die diese Benutzer verfügen müssen, und gibt an, ob die Benutzer sind, authentifiziert oder anonym. Sie können eine Gestaltungsvorlage oder Seitenlayout ein Bereich Sicherheit erhöhen, hinzugefügt. Ein Bereich Sicherheit erhöhen, ist ein Container, der andere Komponenten oder Ausschnitte, wie Webparts, zusätzlich zu statischer Inhalt enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="069f0-p101">You can use a Security Trim snippet to display content only to specific users, based on a specific permission that those users must have, and whether those users are authenticated or anonymous. You can add a Security Trim panel to a master page or page layout. A Security Trim panel is a container that can include other components or snippets, such as Web Parts, in addition to static content.</span></span>
  
    
    
<span data-ttu-id="069f0-109">Einen Bereich Sicherheit erhöhen, können Sie beispielsweise die folgende Inhalte für bestimmte Benutzer anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="069f0-109">For example, you can use a Security Trim panel to display the following content to specific users:</span></span>
  
    
    

- <span data-ttu-id="069f0-110">Ein Inhalt-nach-Search-Webpart, welche Dokumente angezeigt, als authentifizierter Benutzer gerade arbeitet.</span><span class="sxs-lookup"><span data-stu-id="069f0-110">A Content by Search Web Part that displays which documents an authenticated user is currently working on.</span></span>
    
  
- <span data-ttu-id="069f0-111">Eine Liste der zuletzt geänderte Dokumente anzeigen, damit authentifizierte Benutzer sehen, was auf der Website neue ist.</span><span class="sxs-lookup"><span data-stu-id="069f0-111">A list view of recently modified documents so that authenticated users can see what's new on the site.</span></span>
    
  
- <span data-ttu-id="069f0-p102">Ein Inhalt-nach-Search Web Part, die für Besucher von nicht authentifizierten eine Liste der zeigt empfohlene Links, die basierend auf den aktuellen Artikel. Diese Liste enthält Empfehlungen möglicherweise Noise authentifizierten Inhaltsautoren arbeiten in der Website, aber es ist wichtig für Besucher von nicht authentifizierten.</span><span class="sxs-lookup"><span data-stu-id="069f0-p102">A Content by Search Web Part that displays to non-authenticated visitors a list of recommended links based on the current article. Such a list of recommendations might be noise to authenticated content authors working in the site, but it's important for non-authenticated visitors.</span></span>
    
  
- <span data-ttu-id="069f0-114">Ein vom Menüband unabhängiger Anmeldelink für nicht authentifizierte Benutzer oder Benutzer, die noch authentifiziert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="069f0-114">A sign-in link separate from the ribbon, for non-authenticated users or users who have yet to be authenticated.</span></span>
    
    > <span data-ttu-id="069f0-115">**Hinweis:** Dieser Anmeldelink wird automatisch in eine Gestaltungsvorlage eingefügt, die mithilfe des Entwurfs-Manager erstellt wird, Sie können ihn jedoch löschen, wenn er nicht benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="069f0-115">**Note:** This sign-in link is inserted automatically into a master page that is created by using Design Manager, but you can delete it if it's not needed.</span></span> 
      > <span data-ttu-id="069f0-116">Ein Sicherheitskürzungsbereich hat zwei wichtige Eigenschaftseinstellungen, eine für die Authentifizierung und eine für Berechtigungen (oder Autorisierung).</span><span class="sxs-lookup"><span data-stu-id="069f0-116">A Security Trim panel has two important property settings, one for authentication and one for permissions (or authorization).</span></span> <span data-ttu-id="069f0-117">Sie können einen Sicherheitskürzungsbereich z. B. verwenden, um bestimmten Benutzern den folgenden Inhalt anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="069f0-117">For example, you can use a Security Trim panel to display the following content to specific users:</span></span>
  
    
    

- <span data-ttu-id="069f0-118">**AuthenticationRestrictions** Mit dieser Eigenschaft können Sie die Systemsteuerung auf authentifizierte oder anonyme Benutzer beschränken, oder wählen Sie alle Benutzer (alle Benutzer ist die Standardeinstellung).</span><span class="sxs-lookup"><span data-stu-id="069f0-118">**AuthenticationRestrictions** With this property, you can restrict the panel to either authenticated or anonymous users, or choose all users (all users is the default setting).</span></span>
    
  
- <span data-ttu-id="069f0-119">**Berechtigungen** Mit dieser Eigenschaft können Sie eine bestimmte Berechtigung auswählen, die Benutzer benötigen, um den Inhalt im Bereich anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="069f0-119">**Permissions** With this property, you can select a specific permission that users must have to view the content in the panel.</span></span>
    
    > <span data-ttu-id="069f0-120">**Hinweis:** Sie wählen eine einzelne Berechtigung aus, keine Berechtigungsstufe.</span><span class="sxs-lookup"><span data-stu-id="069f0-120">**Note:** You are selecting an individual permission, not a permission level.</span></span> <span data-ttu-id="069f0-121">(Eine Berechtigungsstufe ist ein Satz erteilter Berechtigungen.) Wenn Sie die Authentifizierung nur auf anonyme Benutzer beschränken, ist es normalerweise nicht erforderlich, eine bestimmte Berechtigung anzugeben, da anonymen Benutzern in der Regel keine SharePoint-Berechtigungen zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="069f0-121">(A permission level is a set of granted permissions.) Of course, if you restrict the authentication to only anonymous users, it's typically not necessary to specify a specific permission because anonymous users have usually not been given any SharePoint permissions.</span></span> <span data-ttu-id="069f0-122">Es ist sinnvoll, Berechtigungen nur für alle Benutzer oder für alle authentifizierten Benutzer zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="069f0-122">It makes sense to use permissions only with all users or with all authenticated users.</span></span>
  
    
    
<span data-ttu-id="069f0-p105">Die Sicherheit erhöhen, Systemsteuerung verfügt über drei Optionen klicken Sie im Menüband in der linken Spalte von Tabelle 1 aufgeführt. Tabelle 1 zeigt, wie diese Einstellungen bestimmen, die bestimmte Berechtigung, die Benutzer verfügen müssen, die niedrigste Standardberechtigungsstufe, die diese bestimmte Berechtigung enthält und die Gruppe, die mit dieser Berechtigungsstufe standardmäßig verknüpft ist.)</span><span class="sxs-lookup"><span data-stu-id="069f0-p105">The Security Trim panel has three options on the ribbon, listed in the left column of Table 1. Table 1 shows how these settings determine the specific permission that users are required to have, the lowest default permission level that includes that specific permission, and the group that is linked to that permission level by default.)</span></span>
  
    
    

> <span data-ttu-id="069f0-125">**Hinweis** Dies sind die Standardeinstellungen, die für jeden gegebenen Bereich, wie eine Websitesammlung, Website, Liste oder ein Element, geändert werden können.</span><span class="sxs-lookup"><span data-stu-id="069f0-125">**Note:** These are the default settings, which can be changed for any given scope, such as a site collection, site, list, or item.</span></span> 
  
    
    

<span data-ttu-id="069f0-126">Wenn Sie einen Bereich erhöhen, Sicherheit **für Autoren** anzeigen festlegen, ist beispielsweise durch Standardinhalt innerhalb dieses Bereichs für Benutzer in der Gruppe Mitglieder und der Gruppe "Besitzer" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="069f0-126">For example, if you set a Security Trim panel to **Show to authors**, by default content inside that panel is visible to users in the Members group and the Owners group.</span></span>
  
    
    

<span data-ttu-id="069f0-127">**In Tabelle 1. Zuordnung von Optionen im standardmäßigen Berechtigungsebenen und Gruppen**</span><span class="sxs-lookup"><span data-stu-id="069f0-127">**Table 1. Mapping of panel options to default permission levels and groups**</span></span>


|<span data-ttu-id="069f0-128">**Sicherheit Trim Systemsteuerung option**</span><span class="sxs-lookup"><span data-stu-id="069f0-128">**Security Trim panel option**</span></span>|<span data-ttu-id="069f0-129">**Permissions-Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="069f0-129">**Permissions property**</span></span>|<span data-ttu-id="069f0-130">**Berechtigung**</span><span class="sxs-lookup"><span data-stu-id="069f0-130">**Permission**</span></span>|<span data-ttu-id="069f0-131">**Berechtigungsstufe**</span><span class="sxs-lookup"><span data-stu-id="069f0-131">**Permission level**</span></span>|<span data-ttu-id="069f0-132">**Group**</span><span class="sxs-lookup"><span data-stu-id="069f0-132">**Group**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="069f0-133">Autoren anzeigen</span><span class="sxs-lookup"><span data-stu-id="069f0-133">Show to authors</span></span>  <br/> |<span data-ttu-id="069f0-134">**AddAndCustomizePages**</span><span class="sxs-lookup"><span data-stu-id="069f0-134">**AddAndCustomizePages**</span></span> <br/> |<span data-ttu-id="069f0-135">Seiten hinzufügen und anpassen</span><span class="sxs-lookup"><span data-stu-id="069f0-135">Add and Customize Pages</span></span>  <br/> |<span data-ttu-id="069f0-136">Contribute (oder höher)</span><span class="sxs-lookup"><span data-stu-id="069f0-136">Contribute (or higher)</span></span>  <br/> |<span data-ttu-id="069f0-137">Elemente</span><span class="sxs-lookup"><span data-stu-id="069f0-137">Members</span></span>  <br/> |
|<span data-ttu-id="069f0-138">Für authentifizierte Benutzer anzeigen</span><span class="sxs-lookup"><span data-stu-id="069f0-138">Show to Authenticated Users</span></span>  <br/> |<span data-ttu-id="069f0-139">**ViewPages**</span><span class="sxs-lookup"><span data-stu-id="069f0-139">**ViewPages**</span></span> <br/> |<span data-ttu-id="069f0-140">Seiten anzeigen</span><span class="sxs-lookup"><span data-stu-id="069f0-140">View Pages</span></span>  <br/> |<span data-ttu-id="069f0-141">Lesen (oder höher)</span><span class="sxs-lookup"><span data-stu-id="069f0-141">Read (or higher)</span></span>  <br/> |<span data-ttu-id="069f0-142">Besucher</span><span class="sxs-lookup"><span data-stu-id="069f0-142">Visitors</span></span>  <br/> |
|<span data-ttu-id="069f0-143">Für Administratoren anzeigen</span><span class="sxs-lookup"><span data-stu-id="069f0-143">Show to Administrators</span></span>  <br/> |<span data-ttu-id="069f0-144">**FullMask**</span><span class="sxs-lookup"><span data-stu-id="069f0-144">**FullMask**</span></span> <br/> |<span data-ttu-id="069f0-145">Alles markieren</span><span class="sxs-lookup"><span data-stu-id="069f0-145">Select All</span></span>  <br/> |<span data-ttu-id="069f0-146">Vollzugriff</span><span class="sxs-lookup"><span data-stu-id="069f0-146">Full Control</span></span>  <br/> |<span data-ttu-id="069f0-147">Besitzer</span><span class="sxs-lookup"><span data-stu-id="069f0-147">Owners</span></span>  <br/> |
   

### <a name="inserting-a-security-trim-panel"></a><span data-ttu-id="069f0-148">Einfügen eines Bereichs Sicherheit erhöhen</span><span class="sxs-lookup"><span data-stu-id="069f0-148">Inserting a Security Trim panel</span></span>
<span data-ttu-id="069f0-149"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="069f0-149"><a name="InsertSnippet"> </a></span></span>

<span data-ttu-id="069f0-p106">Wie alle Ausschnitte fügen Sie den Codeausschnitt Sicherheit erhöhen, aus der Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.</span><span class="sxs-lookup"><span data-stu-id="069f0-p106">Like all snippets, you add the Security Trim snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-security-trim-panel"></a><span data-ttu-id="069f0-152">So fügen Sie einen Bereich Sicherheit erhöhen, ein</span><span class="sxs-lookup"><span data-stu-id="069f0-152">To insert a Security Trim panel</span></span>


1. <span data-ttu-id="069f0-153">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="069f0-153">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="069f0-154">Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="069f0-154">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="069f0-155">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="069f0-155">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="069f0-156">Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="069f0-156">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="069f0-157">Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.</span><span class="sxs-lookup"><span data-stu-id="069f0-157">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="069f0-158">Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** **Sicherheit zu erhöhen**.</span><span class="sxs-lookup"><span data-stu-id="069f0-158">On the ribbon, on the **Design** tab, choose **Security Trim**.</span></span>
    
    <span data-ttu-id="069f0-159">In der Dropdown-Liste auf die Schaltfläche **Sicherheit zu erhöhen**, können Sie optional die Benutzer auswählen, denen der Inhalt des Bereichs werden angezeigt, oder Sie können weitere Optionen anzeigen, indem die wichtige Eigenschaftswerte für den Bereich konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="069f0-159">Optionally, in the drop-down list on the **Security Trim** button, you can select the users to whom the panel content will be visible, or you can see more options by configuring the important property values for the panel.</span></span>
    
  
7. <span data-ttu-id="069f0-160">Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="069f0-160">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
  
8. <span data-ttu-id="069f0-p107">Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="069f0-p107">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="069f0-164">Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.</span><span class="sxs-lookup"><span data-stu-id="069f0-164">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="069f0-165">Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="069f0-165">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
  
11. <span data-ttu-id="069f0-166">Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="069f0-166">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="069f0-167">Wenn Sie den Codeausschnitt, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**einfügen.</span><span class="sxs-lookup"><span data-stu-id="069f0-167">If you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="069f0-168">Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="069f0-168">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
  
13. <span data-ttu-id="069f0-169">Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass die Sicherheit erhöhen, wird angezeigt, wie erwartet.</span><span class="sxs-lookup"><span data-stu-id="069f0-169">Save the page, and then refresh the server-side preview in Design Manager to make sure the Security Trim panel appears as expected.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="069f0-170">Grundlegendes zum Codeausschnittmarkup</span><span class="sxs-lookup"><span data-stu-id="069f0-170">Understanding the snippet markup</span></span>
<span data-ttu-id="069f0-171"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="069f0-171"><a name="UnderstandMarkup"> </a></span></span>

<span data-ttu-id="069f0-p108">Die wichtigsten Teile des einen Ausschnitt Sicherheit erhöhen, sind die **AuthenticationRestrictions** -Eigenschaft und die **Permissions** -Eigenschaft und die **<div>** in Fettschrift unten. **AuthenticationRestrictions** im Markup nur, wenn von **AllUsers**, geändert Standard wird angezeigt. Wenn Sie **Zurücksetzen** für den Ausschnitt im Codeausschnittkatalog auswählen, wird **AuthenticationRestrictions** aus dem Markup entfernt, was bedeutet, dass der Ausschnitt den Standardwert **AllUsers**verwendet.</span><span class="sxs-lookup"><span data-stu-id="069f0-p108">The most important parts of a Security Trim snippet are the **AuthenticationRestrictions** property and the **Permissions** property, and the **<div>** in bold below. **AuthenticationRestrictions** appears in the markup only when changed from **AllUsers**, which is the default. If you choose **Reset** for the snippet in the Snippet Gallery, **AuthenticationRestrictions** is removed from the markup, which means the snippet uses the default value, **AllUsers**.</span></span>
  
    
    
<span data-ttu-id="069f0-175">Die **<div>**, wobei `class="DefaultContentBlock"` ist, was Sie mit Ihren eigenen Inhalt ersetzen die anderen Snippets und Steuerelemente enthalten können.</span><span class="sxs-lookup"><span data-stu-id="069f0-175">The **<div>** where `class="DefaultContentBlock"` is what you replace with your own content, which can include other snippets and controls.</span></span>
  
    
    



```HTML

<div data-name="SecurityTrimmedAuthors">
    <!--CS: Start Security Trim Snippet-->
    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AuthenticatedUsersOnly" Permissions="AddAndCustomizePages" PermissionContext="RootSite">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Security Trim Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--></span><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
    <!--CE: End Security Trim Snippet-->
</div>
```


## <a name="additional-resources"></a><span data-ttu-id="069f0-176">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="069f0-176">Additional resources</span></span>
<span data-ttu-id="069f0-177"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="069f0-177"><a name="AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="069f0-178">Einführung: Steuern des Benutzerzugriffs mit Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="069f0-178">Introduction: Control user access with permissions</span></span>](http://office.microsoft.com/en-us/sharepoint-foundation-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=1)
    
  
-  [<span data-ttu-id="069f0-179">Grundlegendes zu Berechtigungsstufen</span><span class="sxs-lookup"><span data-stu-id="069f0-179">Understanding permission levels</span></span>](http://office.microsoft.com/en-us/products/default-permission-levels-HA102772313.aspx?CTT=5&amp;origin=HA102771919)
    
  
-  [<span data-ttu-id="069f0-180">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="069f0-180">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="069f0-181">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="069f0-181">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="069f0-182">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="069f0-182">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

