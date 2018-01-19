---
title: Erstellen eines Workflows mit erweiterten Berechtigungen mithilfe der SharePoint-Workflow-Plattform
description: "Erstellen von SharePoint-Workflows, die auf Objekte in SharePoint zugreifen, für die erhöhte Berechtigungen erforderlich sind. Diese Lösungen erteilen der Workflow-App Berechtigungen und umhüllen Aktionen mit dem App-Schritt."
ms.date: 12/29/2017
ms.prod: sharepoint
ms.assetid: 4656f6a0-36fd-4b7d-898e-8cd4bdbbda57
ms.openlocfilehash: 2efa1810d3d6a0c579daa356599ef9dfffda230f
ms.sourcegitcommit: 469ce248552201a47ebea1b6c85bc5c90a97c7ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflow-platform"></a><span data-ttu-id="84540-104">Erstellen eines Workflows mit erweiterten Berechtigungen mithilfe der SharePoint-Workflow-Plattform</span><span class="sxs-lookup"><span data-stu-id="84540-104">Create a workflow with elevated permissions by using the SharePoint Workflow platform</span></span>

<span data-ttu-id="84540-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="84540-105"></span></span>

<span data-ttu-id="84540-p102">Dieser Artikel beschreibt, wie Sie SharePoint-Workflows erstellen, die auf Objekte in SharePoint zugreifen, die erweiterte Berechtigungen erfordern. Diese Lösungen verwenden zwei Features: Erteilen von Berechtigungen für die Workflow-App und Umhüllen der Aktionen mit dem App-Schritt.</span><span class="sxs-lookup"><span data-stu-id="84540-p102">This article describes how to create SharePoint workflows that access objects in SharePoint that require elevated permissions. These solutions use two features: granting permissions to the workflow app and wrapping actions with the App Step.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="84540-108">In diesem Artikel wird davon ausgegangen, dass die SharePoint-Workflow-Plattform installiert und konfiguriert sowie SharePoint für Add-Ins konfiguriert wurde. Weitere Informationen zu SharePoint-Workflow und Add-Ins für SharePoint, einschließlich Installation und Konfiguration, finden Sie unter  [Workflow in SharePoint](workflows-in-sharepoint.md) und [Installieren und Verwalten von Apps für SharePoint](../sp-add-ins/sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="84540-108">Important This article assumes that the SharePoint Workflow platform has been installed and configured and that SharePoint has been configured for apps. For more information on SharePoint Workflow and apps for SharePoint, including installation and configuration, see  Workflow in SharePoint and Install and manage apps for SharePoint.</span></span> 

<span data-ttu-id="84540-109">Angenommen Sie als SharePoint-Administrator möchten einige Prozesse zum Verwalten von Benutzeranforderungen zum Erwerb von Add-Ins aus dem Office Store definieren.</span><span class="sxs-lookup"><span data-stu-id="84540-109">Imagine that as a SharePoint administrator, you would like to define some processes for managing user requests for purchases of add-ins from the Office Store.</span></span> <span data-ttu-id="84540-110">Im einfachsten Fall möchten Sie eine Bestätigungs-E-Mail senden, wenn ein Benutzer ein Add-In anfordert.</span><span class="sxs-lookup"><span data-stu-id="84540-110">In the simplest case, you want to send an acknowledgment email when a user requests an add-in.</span></span> <span data-ttu-id="84540-111">Außerdem möchten Sie dem Anforderungsgenehmigungsprozess vielleicht eine Struktur hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="84540-111">In addition, you might also want to add structure to the request approval process.</span></span>
  
<span data-ttu-id="84540-112">Standardmäßig verfügt der Workflow nicht über die Berechtigung zum Zugreifen auf den App-Katalog.</span><span class="sxs-lookup"><span data-stu-id="84540-112">By default, workflow does not have permissions to access the app catalog.</span></span> <span data-ttu-id="84540-113">Für Kataloglisten in SharePoint sind Besitzerberechtigungen (Vollzugriff) erforderlich.</span><span class="sxs-lookup"><span data-stu-id="84540-113">Catalog lists in SharePoint require owner (full control) permissions.</span></span> <span data-ttu-id="84540-114">Workflows werden im Allgemeinen auf einer Berechtigungsstufe ausgeführt, die einer Schreibberechtigung entspricht.</span><span class="sxs-lookup"><span data-stu-id="84540-114">Workflows generally run at a permission level equivalent to write.</span></span> 
  
<span data-ttu-id="84540-115">Um dies zu beheben, müssen Sie einen Workflow mit erweiterten Berechtigungen erstellen, indem Sie auf der Websitesammlungs-Website folgendermaßen vorgehen:</span><span class="sxs-lookup"><span data-stu-id="84540-115">To solve this, you have to create a workflow with elevated permissions by doing the following in the Site Collection site:</span></span>

1. <span data-ttu-id="84540-116">Lassen Sie zu, dass der Workflow Add-In-Berechtigungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="84540-116">Allow workflow to use app permissions.</span></span>

2. <span data-ttu-id="84540-117">Erteilen Sie dem Workflow die Berechtigung für den Vollzugriff.</span><span class="sxs-lookup"><span data-stu-id="84540-117">Grant full control permission to workflow.</span></span>
 
3. <span data-ttu-id="84540-118">Entwickeln Sie den Workflow entsprechend, dass Aktionen innerhalb eines App-Schritts umhüllt werden.</span><span class="sxs-lookup"><span data-stu-id="84540-118">Develop the workflow to wrap actions inside an App Step.</span></span>

## <a name="allow-a-workflow-to-use-add-in-permissions-on-a-sharepoint-site"></a><span data-ttu-id="84540-119">Zulassen der Verwendung von Add-In-Berechtigungen auf einer SharePoint-Website für Workflows</span><span class="sxs-lookup"><span data-stu-id="84540-119">Allow a workflow to use add-in permissions on a SharePoint site</span></span>

<span data-ttu-id="84540-120">Der erste Schritt besteht darin, die Verwendung von Add-In-Berechtigungen in Workflows zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="84540-120">The first step is to allow workflow to use app permissions.</span></span> <span data-ttu-id="84540-121">Sie konfigurieren Workflows zum Verwenden von Add-In-Berechtigungen auf der Seite **Websiteeinstellungen** der SharePoint-Website, auf der der Workflow ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="84540-121">You configure workflow to use app permissions on the **Site Settings** page of the SharePoint site where the workflow will run.</span></span> <span data-ttu-id="84540-122">Mit dem folgenden Verfahren wird die SharePoint-Website zum Verwenden von Add-In-Berechtigungen in Workflows konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="84540-122">The following procedure configures the SharePoint site to allow workflow to use app permissions.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="84540-123">Das Verfahren muss von einem Benutzer abgeschlossen werden, der über die **Websitebesitzer**-Berechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="84540-123">The procedure must be completed by a user that has **Site Owner** permissions.</span></span>

### <a name="to-allow-workflow-to-use-add-in-permissions"></a><span data-ttu-id="84540-124">So lassen Sie zu, dass der Workflow Add-In-Berechtigungen verwendet:</span><span class="sxs-lookup"><span data-stu-id="84540-124">To allow workflow to use app permissions</span></span>

1. <span data-ttu-id="84540-125">Wählen Sie das Symbol **Einstellungen**, wie in der Abbildung gezeigt, aus, um die Seite **Websiteeinstellungen** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="84540-125">Select the **Settings** icon as shown in the figure to open the **Site settings** page.</span></span>

  ![Einstellungen-Menü](../images/SPD15-WFAppPermissions1.png)

2. <span data-ttu-id="84540-127">Wechseln Sie zu **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="84540-127">Go to **Site Settings**.</span></span>
 
3. <span data-ttu-id="84540-128">Wählen Sie im Abschnitt **Websiteaktionen** die Option **Websitefeatures verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="84540-128">In the **Site Actions** section, select **Manage site features**.</span></span>

4. <span data-ttu-id="84540-129">Suchen Sie das Feature **Workflows dürfen App-Berechtigungen verwenden**, wie in der Abbildung gezeigt, und klicken Sie dann auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="84540-129">Locate the feature called **Workflows can use app permissions**, as shown in the figure, and then click **Activate**.</span></span>
    
  > [!WARNING] 
  > <span data-ttu-id="84540-130">Dieses Feature wird nicht aktiviert, sofern Sie die SharePoint-Workflow-Plattform und auch die SharePoint-Add-Ins nicht ordnungsgemäß konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="84540-130">Caution This feature will not activate unless you have properly configured the SharePoint Workflow platform and also apps for SharePoint.</span></span> 

  ![Workflow kann App-Berechtigungen-Feature verwenden](../images/SPD15-WFAppPermissions2.png)
  

## <a name="grant-full-control-permission-to-a-workflow"></a><span data-ttu-id="84540-132">Erteilen der Berechtigung „Vollzugriff“ für einen Workflow</span><span class="sxs-lookup"><span data-stu-id="84540-132">Grant full control permission to workflow.</span></span>

<span data-ttu-id="84540-133">Damit der Workflow ordnungsgemäß funktioniert, muss er über Vollzugriff auf die Website verfügen.</span><span class="sxs-lookup"><span data-stu-id="84540-133">For the workflow to function properly, it must be granted full control on the site.</span></span> <span data-ttu-id="84540-134">Im folgenden Verfahren wir dem Workflow Vollzugriff gewährt.</span><span class="sxs-lookup"><span data-stu-id="84540-134">The following procedure grants full control permission to the workflow.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="84540-135">Das Verfahren muss von einem Benutzer abgeschlossen werden, der über die **Websitebesitzer**-Berechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="84540-135">The procedure must be completed by a user that has **Site Owner** permissions.</span></span> <span data-ttu-id="84540-136">Der Workflow muss bereits auf der SharePoint-Website veröffentlicht worden sein.</span><span class="sxs-lookup"><span data-stu-id="84540-136">The workflow must already be published to the SharePoint Server 2013 site.</span></span>

### <a name="to-grant-full-control-permission-to-a-workflow"></a><span data-ttu-id="84540-137">So erteilen Sie einem Workflow die Berechtigung „Vollzugriff“</span><span class="sxs-lookup"><span data-stu-id="84540-137">To grant full control permission to a workflow</span></span>

1. <span data-ttu-id="84540-138">Klicken Sie auf das Symbol **Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="84540-138">Select the **Settings** icon.</span></span>
 
  ![Einstellungen-Menü](../images/SPD15-WFAppPermissions1.png)

2. <span data-ttu-id="84540-140">Wechseln Sie zu **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="84540-140">Go to **Site Settings**.</span></span>    
  
3. <span data-ttu-id="84540-141">Wählen Sie im Abschnitt **Benutzer und Berechtigungen** die Option **Website-App-Berechtigungen** aus.</span><span class="sxs-lookup"><span data-stu-id="84540-141">In the **Users and Permissions** section, select **Site app permissions**.</span></span>    
  
4. <span data-ttu-id="84540-p108">Kopieren Sie den Abschnitt **Client** der **App-ID**. Dies ist die ID zwischen dem letzten "|" und dem Zeichen "@", wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-p108">Copy the **client** section of the **App Identifier**. This is the identifier between the last "|" and the "@" sign, as shown in the figure.</span></span>
    
  ![Auswählen des App-Bezeichners](../images/SPD15-WFAppPermissions3.png)

5. <span data-ttu-id="84540-145">Wechseln Sie zur Seite **Einer App Berechtigungen erteilen**.</span><span class="sxs-lookup"><span data-stu-id="84540-145">Go to the **Grant permission to an app** page.</span></span> <span data-ttu-id="84540-146">Dies muss durch Navigieren zur Seite „appinv.aspx“ der Website erfolgen.</span><span class="sxs-lookup"><span data-stu-id="84540-146">Navigate to the Grant permission to an app page. This must be done by browsing to the appinv.aspx page of the site.</span></span>
    
  <span data-ttu-id="84540-147">Beispiel: `http://{hostname}/{the Site Collection}/_layouts/15/appinv.aspx`.</span><span class="sxs-lookup"><span data-stu-id="84540-147">Example:`http://{hostname}/{the Site Collection}/_layouts/15/appinv.aspx` "\:"</span></span> 
    
  > [!NOTE]
  > <span data-ttu-id="84540-148">Die „App“ bezieht sich in diesem Schritt auf das Workflow-Add-In im Allgemeinen und nicht auf einen bestimmten Workflow.</span><span class="sxs-lookup"><span data-stu-id="84540-148">The 'app' in this step refers to the Workflow app in general and not just a specific workflow.</span></span> <span data-ttu-id="84540-149">Der Zugriff auf einzelne Workflows kann nicht gesteuert werden.</span><span class="sxs-lookup"><span data-stu-id="84540-149">Individual workflows cannot be access controlled.</span></span> <span data-ttu-id="84540-150">Wenn Sie Add-In-Berechtigungen aktivieren, sind sie für alle Workflows in der Websitesammlung aktiviert.</span><span class="sxs-lookup"><span data-stu-id="84540-150">When you enable app permissions you are enabling for all workflows within the Site Collection.</span></span> 

  <span data-ttu-id="84540-151">Weitere Informationen zum Einrichten eines Workflows finden Sie unter  [Blogartikel von Sympraxis Consulting: Durchlaufen von Inhalten in einem Website-Workflow in SharePoint](http://sympmarc.com/series/looping-through-content-in-a-sharepoint-2013-site-workflow/)</span><span class="sxs-lookup"><span data-stu-id="84540-151">For more information about setting up a workflow, see  [Blog article from Sympraxis Consulting: Looping Through Content in a SharePoint Site Workflow](http://sympmarc.com/series/looping-through-content-in-a-sharepoint-2013-site-workflow/)</span></span>
    
  <span data-ttu-id="84540-152">Die folgende Abbildung zeigt ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="84540-152">The following figure shows an example.</span></span>
 
  !["appinv.aspx"-URL-Beispiel und -Seite.](../images/SPD15-WFAppPermissions4.png)

6. <span data-ttu-id="84540-154">Fügen Sie die Client-ID in das Feld **App-ID** ein, und klicken Sie dann auf **Nachschlagen**, wie in der vorherigen Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-154">Paste the client id in the **App Id** field and then click **Lookup**, as shown in the figure.</span></span>

7. <span data-ttu-id="84540-155">Fügen Sie den folgenden Code in das Feld **Berechtigungsanforderungs-XML** ein, um die Berechtigung „Vollzugriff“ zu erteilen *(Hinweis: Dieser Codeblock wurde am 29.12.2017 aktualisiert und enthält nun `AllowAppOnlyPolicy`)*.</span><span class="sxs-lookup"><span data-stu-id="84540-155">Paste the following code in the **Permission Request XML** field to grant full control permission *(note: this code block was updated on 12/29/17 to include the `AllowAppOnlyPolicy`)*.</span></span>
    
  ```XML 
    <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="FullControl" />
    </AppPermissionRequests>

  ```

  > [!WARNING] 
  > <span data-ttu-id="84540-156">Der **Scope**-Wert enthält keine Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="84540-156">Caution: There are no placeholders in the Scope value above.</span></span> <span data-ttu-id="84540-157">Es ist ein Literalwert.</span><span class="sxs-lookup"><span data-stu-id="84540-157">It is a literal value.</span></span> <span data-ttu-id="84540-158">Geben Sie ihn genau so ein, wie er hier dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="84540-158">Enter it exactly as it appears here.</span></span>

  <span data-ttu-id="84540-159">In der folgenden Abbildung ist ein Beispiel der abgeschlossenen Seite _ dargestellt (beachten Sie, dass der Code im Bereich **Berechtigungsanforderungs-XML** nicht das kürzliche Update am Code in Schritt 7 widerspiegelt_.</span><span class="sxs-lookup"><span data-stu-id="84540-159">The following figure shows an example of the completed page _(note that the code in the **Permission Request XML** area does not reflect the recent update to the code in Step 7)_.</span></span> 
  
  ![Nachschlagen einer App-ID.](../images/SPD15-WFAppPermissions5.png)

8. <span data-ttu-id="84540-161">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="84540-161">Select **Create**</span></span>
    
9. <span data-ttu-id="84540-162">Sie werden dann aufgefordert, dem Workflow-Add-In zu vertrauen, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="84540-162">You are then asked to trust the workflow add-in, as shown in the following figure.</span></span> <span data-ttu-id="84540-163">Wählen Sie **Vertrauen** aus.</span><span class="sxs-lookup"><span data-stu-id="84540-163">Select the **Trust It** button.</span></span>
    
  ![Der Workflow-App vertrauen.](../images/SPD15-WFAppPermissions6.png)
  

## <a name="wrap-actions-inside-an-app-step"></a><span data-ttu-id="84540-165">Umhüllen von Aktionen innerhalb eines App-Schritts</span><span class="sxs-lookup"><span data-stu-id="84540-165">Wrapping actions inside an App Step</span></span>

<span data-ttu-id="84540-p113">Abschließend müssen Sie die Workflowaktionen in einem App-Schritt umhüllen. Das folgende Verfahren umhüllt die Aktion **E-Mail senden** innerhalb eines App-Schritts. Der Workflow in diesem Beispiel sendet eine Bestätigungs-E-Mail aus einer benutzerdefinierten Liste.</span><span class="sxs-lookup"><span data-stu-id="84540-p113">Finally, you need to wrap the workflow actions inside an App Step. The following procedure wraps a **Send an Email** action inside an App Step. The workflow in this example sends an acknowledgement email message from a custom list.</span></span>

### <a name="to-wrap-actions-inside-an-app-step"></a><span data-ttu-id="84540-169">So umhüllen Sie Aktionen innerhalb von App-Schritten</span><span class="sxs-lookup"><span data-stu-id="84540-169">To wrap actions inside an App Step</span></span>

1. <span data-ttu-id="84540-170">Öffnen Sie die App-Katalogwebsite in SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="84540-170">Open the App Catalog site in SharePoint Designer 2013.</span></span>    
  
2. <span data-ttu-id="84540-171">Erstellen Sie eine benutzerdefinierte Liste, für die der Workflow ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="84540-171">Create a new Custom List on which to run the workflow. In this example the list name is App Demo.</span></span> <span data-ttu-id="84540-172">In diesem Beispiel ist der Listenname **App-Demo**.</span><span class="sxs-lookup"><span data-stu-id="84540-172">Create a new Custom List on which to run the workflow. In this example the list name is **App Demo**.</span></span>    
  
3. <span data-ttu-id="84540-173">Klicken Sie im Navigationsfenster auf **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="84540-173">Click **Workflows** in the navigation window.</span></span>    
  
4. <span data-ttu-id="84540-174">Erstellen Sie einen neuen **Listenworkflow** für die Liste **App Demo**, wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-174">Create a new List Workflow for the App Demo list, as shown in the figure.</span></span>

  ![Einen neuen Listenworkflow erstellen.](../images/SPD15-WFAppPermissions7.png)

5. <span data-ttu-id="84540-176">Fügen Sie einen **App-Schritt** hinzu, wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-176">Insert an **App Step**, as shown in the figure.</span></span>
    
  ![Hinzufügen eines App-Schritts.](../images/SPD15-WFAppPermissions8.png)

6. <span data-ttu-id="84540-178">Fügen Sie die Aktion **E-Mail senden** im **App-Schritt** ein.</span><span class="sxs-lookup"><span data-stu-id="84540-178">Insert a **Send an Email** action in the **App Step**.</span></span>
 
7. <span data-ttu-id="84540-179">Klicken Sie auf die Schaltfläche **Adressbuch**.</span><span class="sxs-lookup"><span data-stu-id="84540-179">Select the **Address book** button.</span></span> <span data-ttu-id="84540-180">Wählen Sie im Feld **An**  die Option **Workflow-Nachschlagevorgang für einen Benutzer** aus, und klicken Sie dann auf **Hinzufügen**, wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-180">In the **To** field, select **Workflow Lookup for a User**, and then select **Add** as shown in the figure.</span></span>

  ![Workflow-Nachschlagevorgang für einen Benutzer auswählen.](../images/SPD15-WFAppPermissions9.png)
  
8. <span data-ttu-id="84540-182">Geben Sie das Feld **Erstellt von** als Suchwert ein, wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-182">Enter the **Created By** field as the lookup value, as shown in the figure.</span></span>

  ![Dialog zum Nachschlagen von Personen.](../images/SPD15-WFAppPermissions10.png)
  
9. <span data-ttu-id="84540-184">Geben Sie** E-Mail** aus der Liste **App Demo** in den Nachrichtentext der E-Mail ein.</span><span class="sxs-lookup"><span data-stu-id="84540-184">Enter Email from App Demo list in the email message body.</span></span>
     
10. <span data-ttu-id="84540-185">Klicken Sie auf **OK**, um zum Workflow zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="84540-185">Select **OK** to return to the workflow.</span></span> <span data-ttu-id="84540-186">Der abgeschlossene Workflow ist in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="84540-186">Click OK to return to the workflow. The completed workflow is shown in the figure.</span></span>

  ![E-Mail-Aktion im App-Schritt.](../images/SPD15-WFAppPermissions11.png)
    
11. <span data-ttu-id="84540-188">Klicken Sie auf dem Menüband auf das Symbol **Workfloweinstellungen**, wie in der Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="84540-188">Click the **Workflow Settings** icon in the ribbon, as shown in the figure.</span></span>
    
  ![Symbol für Workfloweinstellungen im Menüband.](../images/SPD15-WFAppPermissions12.png)

12. <span data-ttu-id="84540-190">Deaktivieren Sie das Kontrollkästchen neben **Workflowstatus automatisch auf dem aktuellen Phasennamen aktualisieren**, und klicken Sie dann auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="84540-190">Clear the check box next to **Automatic updates to workflow status to the current stage name**, and then click **Publish**, as shown in the figure.</span></span>
    
  ![Häkchen für automatische Updates entfernen und veröffentlichen.](../images/SPD15-WFAppPermissions13.png)
  

<span data-ttu-id="84540-192"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="84540-192"></span></span>

## <a name="understand-how-it-works"></a><span data-ttu-id="84540-193">Erläuterung der Funktionsweise</span><span class="sxs-lookup"><span data-stu-id="84540-193">Understanding how it works</span></span>

<span data-ttu-id="84540-194">Um zu verstehen, warum das Erhöhen von Berechtigungen für einen Workflow erforderlich ist, müssen Sie bedenken, dass Workflows im Grunde genommen Add-Ins für SharePoint sind und dass sie denselben Autorisierungsregeln des Add-In-Modells folgen.</span><span class="sxs-lookup"><span data-stu-id="84540-194">To understand why elevating permissions for a workflow is required, consider that workflows are fundamentally apps for SharePoint and they follow the same authorization rules of the app model. The default configuration for workflow is that the effective permissions of the workflow are an intersection of user permissions and the app permissions, as shown in the figure.</span></span> <span data-ttu-id="84540-195">Die Standardkonfiguration für den Workflow besteht darin, dass effektive Berechtigungen des Workflows eine Schnittmenge von Benutzerberechtigungen und den Add-In-Berechtigungen sind, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="84540-195">To understand why elevating permissions for a workflow is required, consider that workflows are fundamentally apps for SharePoint and they follow the same authorization rules of the app model. The default configuration for workflow is that the effective permissions of the workflow are an intersection of user permissions and the app permissions, as shown in the figure.</span></span>
    
![Berechtigungendiagramm.](../images/SPD15-WFAppPermissions14.png)
  
<span data-ttu-id="84540-197">Es gibt zwei Gründe, warum es erforderlich ist, die Berechtigungen zum Erstellen eines Workflows in der Liste der App-Anforderungen zu erhöhen. Dies sind:</span><span class="sxs-lookup"><span data-stu-id="84540-197">There are two reasons why it is necessary to elevate permissions to create a workflow in the App Request list. These are:</span></span>

- <span data-ttu-id="84540-198">Standardmäßig verfügt der Workflow nur über die Schreibberechtigung.</span><span class="sxs-lookup"><span data-stu-id="84540-198">By default, workflow only has write permission.</span></span>

- <span data-ttu-id="84540-199">Der Benutzer verfügt über keine Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="84540-199">The user has no permissions.</span></span>
  
<span data-ttu-id="84540-p118">Der erste Schritt zur Lösung dieses Problems besteht darin, der Anwendung die Autorisierung zu gestatten, indem nur ihre Identität verwendet und die Identität des Benutzers ignoriert wird. Dies erfolgt durch das Aktivieren des App-Schritt-Features. Im zweite Schritt wird dem Workflow der Vollzugriff gewährt.</span><span class="sxs-lookup"><span data-stu-id="84540-p118">The first step to solve this problem is to allow the application to authorize by using only its identity and ignoring that of the user. This is done by enabling the App Step feature. The second step grants full control permission to the workflow.</span></span> 
  
<span data-ttu-id="84540-203">Das folgende Diagramm veranschaulicht die Änderung der Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="84540-203">The following diagram illustrates the change in permissions</span></span>
  
![Berechtigungenmatrix.](../images/SPD15-WFAppPermissions15.png)
  
<span data-ttu-id="84540-205"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="84540-205"></span></span>

## <a name="see-also"></a><span data-ttu-id="84540-206">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="84540-206">See also</span></span>

- [<span data-ttu-id="84540-207">Blogartikel des SharePoint Designer-Teams: Verpackungs- und Bereitstellungsszenario für Workflows</span><span class="sxs-lookup"><span data-stu-id="84540-207">Blog article from the SharePoint Designer team: Workflow package and deploy scenario</span></span>](https://blogs.msdn.microsoft.com/sharepointdesigner/2012/08/29/packaging-sharepoint-2013-list-site-and-reusable-workflow-and-how-to-deploy-the-package/)
- [<span data-ttu-id="84540-208">Neuerungen bei SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="84540-208">What's new in workflow in SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
- [<span data-ttu-id="84540-209">Erste Schritte mit SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="84540-209">Getting started with SharePoint workflow</span></span>](get-started-with-workflows-in-sharepoint.md) 
- [<span data-ttu-id="84540-210">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="84540-210">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
- [<span data-ttu-id="84540-211">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="84540-211">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)

    
