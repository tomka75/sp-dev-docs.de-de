---
title: Vorgehensweise Verwenden von SAP-Workflows mit Duet Enterprise 2.0
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 816e28ed-8cea-4e33-98e5-d3d27136e2e6
ms.openlocfilehash: 516e0ee220db2d6ebaea1db3cdff9a6dc98c346c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-sap-workflow-with-duet-enterprise-20"></a><span data-ttu-id="14ec6-102">Vorgehensweise: Verwenden von SAP-Workflows mit Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="14ec6-102">How to: Use SAP workflow with Duet Enterprise 2.0</span></span>

## <a name="introduction"></a><span data-ttu-id="14ec6-103">Einführung</span><span class="sxs-lookup"><span data-stu-id="14ec6-103">Introduction</span></span>
<span data-ttu-id="14ec6-104"><a name="bkmk_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-104"></span></span>

<span data-ttu-id="14ec6-105">SAP Business Workflow bietet eine Möglichkeit zum Automatisieren von Geschäftsprozessen und mit Duet Enterprise 2.0, die Workflows innerhalb einer SharePoint-Add-In integriert werden können.</span><span class="sxs-lookup"><span data-stu-id="14ec6-105">SAP Business Workflow provides a way to automate business processes, and with Duet Enterprise 2.0, those workflows can be integrated within an SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="14ec6-106">Die folgenden Schritte zeigen, wie eine app erstellen, konfigurieren, und klicken Sie dann wie die Informationen anzeigen aus der SAP-Workflows abgerufen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-106">The following steps show how to create an app, configure it, and then how to display the information retrieved from the SAP workflows.</span></span>
  
    
    

## <a name="create-an-app-for-sharepoint-and-duet-enterprise-20"></a><span data-ttu-id="14ec6-107">Erstellen einer app für SharePoint und Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="14ec6-107">Create an app for SharePoint and Duet Enterprise 2.0</span></span>
<span data-ttu-id="14ec6-108"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-108"></span></span>

<span data-ttu-id="14ec6-109">Der erste Schritt besteht darin ein SharePoint-Add-In erstellen, das die Verbindungsinformationen mithilfe eines externen Inhaltstyps für Business Connectivity Services (BCS), externe Listen und Anpassungen möglicherweise verwenden, um die Daten zu präsentieren möchten.</span><span class="sxs-lookup"><span data-stu-id="14ec6-109">The first step is to create an SharePoint Add-in that will contain the connection information using an external content type for Business Connectivity Services (BCS), external lists and any customizations you might want to use to present the data.</span></span>
  
    
    

### <a name="to-create-an-app-for-sharepoint"></a><span data-ttu-id="14ec6-110">So erstellen eine app für SharePoint:</span><span class="sxs-lookup"><span data-stu-id="14ec6-110">To create an app for SharePoint:</span></span>


1. <span data-ttu-id="14ec6-111">Starten Sie Visual Studio 2012 als Administrator.</span><span class="sxs-lookup"><span data-stu-id="14ec6-111">Start Visual Studio 2012 as an administrator.</span></span>
    
  
2. <span data-ttu-id="14ec6-112">Wählen Sie **Datei**, **neu**, **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-112">Choose **File**, **New**, **New Project**.</span></span>
    
  
3. <span data-ttu-id="14ec6-113">Klicken Sie im Dialogfeld **Neues Projekt** erweitern Sie den Knoten **Visual c#**, erweitern Sie den Knoten **Office/SharePoint** und wählen Sie dann den Knoten **Apps**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-113">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose the **Apps** node.</span></span>
    
  
4. <span data-ttu-id="14ec6-114">Wählen Sie **die App für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-114">Choose **App for SharePoint**.</span></span>
    
  
5. <span data-ttu-id="14ec6-115">Nennen Sie das Projekt, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-115">Name the project and click **OK**.</span></span>
    
  
6. <span data-ttu-id="14ec6-p101">Klicken Sie im ersten App für SharePoint-Einstellungen im Dialogfeld **angeben** Namens für Ihre app, und wählen Sie unter **Wie möchten Sie hosten Ihre app für SharePoint** **in SharePoint gehostet**. Geben Sie auch die URL der **Duet-Workflow-Website** soll gegen unter **welche SharePoint-Website soll für das debugging Ihrer app** Debuggen, und wählen **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p101">In the first **Specify the App for SharePoint Settings** dialog box, name your app and choose **SharePoint-hosted** under **How do you want to host your app for SharePoint**. Also specify the URL of the **Duet Workflow site** you want to debug against under **What SharePoint site do you want to use for debugging your app** and choose **Finish**.</span></span>
    
  
7. <span data-ttu-id="14ec6-118">Klicken Sie im Menü „Erstellen“ auf *\<Name Ihrer App\>* **bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-118">On the Build menu, choose **Deploy** *\<your app name\>*  .</span></span>
    
  
<span data-ttu-id="14ec6-119">Sobald die App bereitgestellt wurde, öffnet Visual Studio die Standardseite der App.</span><span class="sxs-lookup"><span data-stu-id="14ec6-119">After the app is deployed, Visual Studio will launch the default page for the app.</span></span>
  
    
    

## <a name="add-the-external-content-type-and-external-lists-to-the-app"></a><span data-ttu-id="14ec6-120">Fügen Sie den externen Inhaltstyp und externe Listen der App</span><span class="sxs-lookup"><span data-stu-id="14ec6-120">Add the external content type and external lists to the app</span></span>
<span data-ttu-id="14ec6-121"><a name="bkmk_AddECT"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-121"></span></span>

<span data-ttu-id="14ec6-p102">BCS müssen der externen Datenquelle darauf aufmerksam gemacht werden. Dies erfolgt mithilfe eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p102">BCS must be made aware of the external data source. This is done using an external content type.</span></span>
  
    
    

### <a name="to-add-an-external-content-type"></a><span data-ttu-id="14ec6-124">So fügen Sie einen externen Inhaltstyp hinzu:</span><span class="sxs-lookup"><span data-stu-id="14ec6-124">To add an external content type:</span></span>


1. <span data-ttu-id="14ec6-125">Klicken Sie im **Projektmappen-Explorer** öffnen Sie das Kontextmenü für das Projekt zu, und wählen Sie **Hinzufügen** **von Inhaltstypen für die externe Datenquelle**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-125">In the **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="14ec6-p103">Geben Sie auf der Seite **OData-Quelle anzugeben** die URL der Duet Enterprise-Workflow-Dienst. Es folgt ein Beispiel für eine Duet-Dienst-URL:</span><span class="sxs-lookup"><span data-stu-id="14ec6-p103">On the **Specify OData Source** page, enter the URL of the Duet Enterprise Workflow Service. The following is an example of a Duet service URL:</span></span>
    
     <span data-ttu-id="14ec6-128">*https://\<\<DUETGATEWAY\>\>:\<\<PORT\>\>/sap/opu/odata/IWWRK/DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE*</span><span class="sxs-lookup"><span data-stu-id="14ec6-128">*https://\<\<DUETGATEWAY\>\>:\<\<PORT\>\>/sap/opu/odata/IWWRK/DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE*</span></span> 
    
  
3. <span data-ttu-id="14ec6-129">Legen Sie einen Namen für die ODATA-Quelle fest, zum Beispiel „SAPWorkflows“. Klicken Sie anschließend auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-129">Choose a name for your ODATA source, for example, SAPWorkflows, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="14ec6-130">Geben Sie den SAP-Benutzername und das Kennwort zum Herstellen der Webdienst-Metadaten.</span><span class="sxs-lookup"><span data-stu-id="14ec6-130">Specify the SAP username and password to connect to the service metadata.</span></span>
    
  
5. <span data-ttu-id="14ec6-p104">Es wird eine Liste von Datenentitäten, die vom OData Service verfügbar gemacht werden angezeigt. Wählen Sie die Entitäten, die Sie in den externen Inhaltstyp aufnehmen möchten. Wählen Sie in diesem Beispiel wird mit der SAP-Workflow-Dienste aus den folgenden:</span><span class="sxs-lookup"><span data-stu-id="14ec6-p104">A list of data entities that are being exposed by the OData Service appears. Select the entities you wish to include in the external content type. In this example, using the SAP workflow services, select from the following:</span></span>
    
  - <span data-ttu-id="14ec6-134">**AttachmentCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-134">**AttachmentCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-135">**CommentCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-135">**CommentCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-136">**DecisionOptionCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-136">**DecisionOptionCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-137">**ExtensibleElementCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-137">**ExtensibleElementCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-138">**ParticipantCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-138">**ParticipantCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-139">**ServiceOperations**</span><span class="sxs-lookup"><span data-stu-id="14ec6-139">**ServiceOperations**</span></span>
    
  
  - <span data-ttu-id="14ec6-140">**TaskDescriptionCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-140">**TaskDescriptionCollection**</span></span>
    
  
  - <span data-ttu-id="14ec6-141">**WorkflowTaskCollection**</span><span class="sxs-lookup"><span data-stu-id="14ec6-141">**WorkflowTaskCollection**</span></span>
    
  
6. <span data-ttu-id="14ec6-142">Aktivieren Sie das Kontrollkästchen **Listeninstanzen für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge) erstellen**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-142">Select the **Create list instances for the selected data entities (except Service Operations)** check box.</span></span>
    
  
7. <span data-ttu-id="14ec6-143">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-143">Choose **Finish**.</span></span>
    
  

> <span data-ttu-id="14ec6-144">**Hinweis:** Stellen Sie sicher, dass der SAP-Workflowdienst Standardauthentifizierung zulässt, wie die BDC-Autogenerierungstools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14ec6-144">**Note** Make sure SAP workflow service allows basic authentication as the BDC auto-generation tools in Visual Studio.</span></span> 
  
    
    


## <a name="add-a-custom-action-feature-to-a-duet-enterprise-20-workflow-list"></a><span data-ttu-id="14ec6-145">Hinzufügen einer benutzerdefinierten Aktion zu einer Duet Enterprise 2.0-Workflowliste</span><span class="sxs-lookup"><span data-stu-id="14ec6-145">Add a custom action feature to a Duet Enterprise 2.0 workflow list</span></span>
<span data-ttu-id="14ec6-146"><a name="bkmk_AddCustomAction"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-146"></span></span>

<span data-ttu-id="14ec6-147">Um eine Möglichkeit für den Benutzer zum Arbeiten mit der neuen Funktionalität einer SharePoint-Liste hinzugefügt zu gewährleisten, werden die folgenden Schritte im Menü Websiteaktionen ein Element hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-147">In order to provide a way for the user to work with the new functionality added to a SharePoint list, the following steps will add an item to the Site Actions menu.</span></span>
  
    
    

### <a name="to-add-a-custom-action"></a><span data-ttu-id="14ec6-148">So fügen Sie eine benutzerdefinierte Aktion hinzu:</span><span class="sxs-lookup"><span data-stu-id="14ec6-148">To add a custom action:</span></span>


1. <span data-ttu-id="14ec6-149">Klicken Sie mit der rechten Maustaste auf das SharePoint-Add-In-Projekt und fügen Sie ein neues Element **Benutzerdefinierte UI-Aktion** hinzu.</span><span class="sxs-lookup"><span data-stu-id="14ec6-149">Right-click the SharePoint Add-in project, and add a new **UI Custom Action** item.</span></span>
    
  
2. <span data-ttu-id="14ec6-p105">Öffnen Sie die Datei **Elements.xml** der benutzerdefinierten Aktion Host-Web-Feature. Durch den Code in der Datei durch den folgenden XML-Code ersetzen, wird die benutzerdefinierte Aktion:</span><span class="sxs-lookup"><span data-stu-id="14ec6-p105">Open the **Elements.xml** file of the custom action host web feature. By replacing the code in the file with the following XML, the custom action will:</span></span>
    
  - <span data-ttu-id="14ec6-152">Deklarieren einer benutzerdefinierten ECB-Aktion und ihrer Attribute.</span><span class="sxs-lookup"><span data-stu-id="14ec6-152">Declare an ECB custom action and its attributes.</span></span>
    
  
  - <span data-ttu-id="14ec6-153">Deklarieren Sie eine benutzerdefinierte Aktion und ihrer Attribute.</span><span class="sxs-lookup"><span data-stu-id="14ec6-153">Declare a Ribbon custom action and its attributes.</span></span>
    
  
  - <span data-ttu-id="14ec6-154">Deklarieren Sie das app-Webseite Ziel und die Werte, die durch die Abfragezeichenfolge übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="14ec6-154">Declare the app webpage target and the values that are passed to it through the query string.</span></span> 
    
    <span data-ttu-id="14ec6-p106">Das Element **UrlAction** verwendet mehrere Token. Weitere Informationen finden Sie unter [URL-Zeichenfolgen und Tokens in Add-Ins für SharePoint](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="14ec6-p106">The **UrlAction** element uses several tokens. For more information, see [URL strings and tokens in SharePoint Add-ins](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).</span></span>
    
  

```XML
  
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="ViewDetailsECBCustomAction"
          RegistrationType="List"
          RegistrationId="107"
          Location="EditControlBlock"
          Sequence="1"
          ImageUrl="_layouts/15/images/placeholder16x16.png"
          Title="View Details">
     <UrlAction Url="~appWebUrl/Pages/ViewDetails.aspx?
            {StandardTokens}&amp;amp;ListId={ListId}&amp;amp;ItemId={ItemId}"/>
  </CustomAction>

  <CustomAction
          Id="ViewDetailsRibbonAction"
          RegistrationId="107"
          RegistrationType="List"
          Location="CommandUI.Ribbon"
          Title="View Details"
          HostWebDialog="false"
          HostWebDialogHeight="500"
          HostWebDialogWidth="500">
    <CommandUIExtension>
      <CommandUIDefinitions>
        <CommandUIDefinition 
              Location="Ribbon.ListItem.Workflow.Controls._children">
          <Button
              Id="Ribbon.ListItem.Workflow.ViewDetails"
              Alt="View Details"
              Sequence="25"
              Command="Invoke_ViewDetailsSAPWorkflow"
              LabelText="View Details"
              TemplateAlias="o1"
              Image32by32="_layouts/15/images/placeholder32x32.png"
              Image16by16="_layouts/15/images/placeholder16x16.png"/>
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler
          Command="Invoke_ViewDetailsSAPWorkflow"
          CommandAction="~appWebUrl/Pages/ViewDetails.aspx?
           {StandardTokens}&amp;amp;ListId={ListId}&amp;amp;ItemId={SelectedItemId}"/>
      </CommandUIHandlers>
    </CommandUIExtension>
  </CustomAction>
</Elements>
```

3. <span data-ttu-id="14ec6-157">Fügen Sie dem Projekt ViewDetails.aspx Seite und eine neue Seite hinzu.</span><span class="sxs-lookup"><span data-stu-id="14ec6-157">Add a new page, ViewDetails.aspx page to the project.</span></span>
    
  
4. <span data-ttu-id="14ec6-158">Drücken Sie **F5** zum Erstellen und Bereitstellen der SharePoint-app.</span><span class="sxs-lookup"><span data-stu-id="14ec6-158">Press **F5** to build and deploy the SharePoint app.</span></span>
    
  
5. <span data-ttu-id="14ec6-p107">Wechseln Sie zur Liste **WorkItem** im Hostweb, und klicken Sie im Kontextmenü auf **Details anzeigen**. Sie werden auf die Seite **ViewDetails.aspx** umgeleitet.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p107">Go to the **WorkItem** list in the host web and choose **View Details** in the context menu. You will be redirected to **ViewDetails.aspx**.</span></span>
    
  

> <span data-ttu-id="14ec6-161">**Hinweis:** Stellen Sie sicher, dass der SAP-Workflowdienst Standardauthentifizierung zulässt.</span><span class="sxs-lookup"><span data-stu-id="14ec6-161">**Note** Make sure SAP workflow service allows basic authentication as the BDC auto-generation tools in Visual Studio.</span></span> <span data-ttu-id="14ec6-162">Die BDC-Autogenerierungstools in Visual Studio unterstützen derzeit lediglich anonyme Authentifizierung und Standardauthentifizierung.</span><span class="sxs-lookup"><span data-stu-id="14ec6-162">Note Make sure the SAP workflow service allows basic authentication. The BDC auto-generation tools in Visual Studio currently only support anonymous and basic authentication.</span></span> 
  
    
    

<span data-ttu-id="14ec6-163">Wenn Sie die App nun bereitstellen und in der App zu **Lists/WorkflowTaskCollection** wechseln, wird die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="14ec6-163">If you deploy the app and then navigate to **Lists/WorkflowTaskCollection** inside your app, you will see the following message:</span></span>
  
    
    
<span data-ttu-id="14ec6-164">"Nachricht vom externen System:"LobSystem (externes System) hat Authentifizierungsfehler zurückgegeben."".</span><span class="sxs-lookup"><span data-stu-id="14ec6-164">"Message from External System: 'LobSystem (External System) returned authentication error.'".</span></span>
  
    
    
<span data-ttu-id="14ec6-165">Um dieses Problem zu beheben, müssen Sie die Bereitstellung von Authentifizierungsanmeldeinformationen BCS und dem SAP-Back-End-app-auf Hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-165">To fix this, you will need to add single sign-on to the app to provide authentication credentials to BCS and the SAP backend.</span></span>
  
    
    

## <a name="add-single-sign-on-security-to-the-app"></a><span data-ttu-id="14ec6-166">Sicherheit für einmaliges Anmelden an die app hinzufügen</span><span class="sxs-lookup"><span data-stu-id="14ec6-166">Add single sign-on security to the app</span></span>
<span data-ttu-id="14ec6-167"><a name="bkmk_AddSSO"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-167"></span></span>

<span data-ttu-id="14ec6-168">Duet Enterprise Single Sign-On können Benutzer authentifiziert werden, damit sie auf SharePoint und SAP-Seiten mit einem anmelden Ressourcen zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="14ec6-168">Duet Enterprise Single Sign-On will allow users to be authenticated so that they can access resources on both the SharePoint and SAP sides with one sign in.</span></span>
  
    
    

### <a name="to-add-single-sign-on"></a><span data-ttu-id="14ec6-169">So fügen Sie einmaliges Anmelden hinzu:</span><span class="sxs-lookup"><span data-stu-id="14ec6-169">To add single sign-on:</span></span>


1. <span data-ttu-id="14ec6-170">Erstellen einer OData-Verbindungs den folgenden Befehl auf der SharePoint-Verwaltungsshell ausführen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-170">Create an OData connection by executing the following command on the SharePoint Management Shell.</span></span>
    
```XML
  
New-SPODataConnectionSetting -Name SAPWorkflow
-ServiceContext "http://localhost" -ExtensionProvider 
"OBA.Server.Canary.ObaOdataServerExtensionProvider, OBA.Server.SSOProvider, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" 
-AuthenticationMode passthrough -ServiceAddressURL 
"https://<<DUETGATEWAY>>:<<PORT>>/sap/opu/odata/IWWRK/
DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE"

```

2. <span data-ttu-id="14ec6-171">Doppelklick auf **WorkflowTaskCollection.ect**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-171">Double click on **WorkflowTaskCollection.ect**.</span></span>
    
  
3. <span data-ttu-id="14ec6-172">Aktualisieren Sie im Fenster Eigenschaften den Wert der  `ODataConnectionSettingId` auf *SAPWorkflow*  .</span><span class="sxs-lookup"><span data-stu-id="14ec6-172">In the Properties window, update the value of  `ODataConnectionSettingId` to *SAPWorkflow*  .</span></span>
    
  
4. <span data-ttu-id="14ec6-173">Zulassen der App, die Verbindung zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="14ec6-173">Allow the App to use the Connection.</span></span>
    
  
5. <span data-ttu-id="14ec6-174">Öffnen Sie die **Datei AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-174">Open the **AppManifest.xml**.</span></span>
    
  
6. <span data-ttu-id="14ec6-175">In **Berechtigungsanfragen**, select **Bereich**, **BCS** dann **Berechtigung** = lesen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-175">In **Permission Requests**, select **Scope**, **BCS** then **Permission** = Read.</span></span>
    
  
7. <span data-ttu-id="14ec6-176">Drücken Sie **F5**, um die app bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-176">Press **F5** to deploy the app.</span></span>
    
  
8. <span data-ttu-id="14ec6-177">Wählen Sie auf der Seite **Berechtigungen** für die app die OData-Verbindung, die diese app verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="14ec6-177">On the **Permissions** page for the app, select the OData connection this app will use.</span></span>
    
  
9. <span data-ttu-id="14ec6-178">Klicken Sie auf die Schaltfläche **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-178">Choose the **Trust It** button.</span></span>
    
  
10. <span data-ttu-id="14ec6-p109">Navigieren Sie zu **. / Listen/WorkflowTaskCollection**. Die SAP-Aufgaben zugewiesen, die direkt aus dem SAP-System stammen sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p109">Navigate to **../Lists/WorkflowTaskCollection**. You should see the SAP tasks assigned to you coming directly from the SAP system.</span></span>
    
  

## <a name="access-workflow-tasks-and-associated-items-using-jsom"></a><span data-ttu-id="14ec6-181">Access-Workflowaufgaben und zugehörigen Elemente mit JSOM</span><span class="sxs-lookup"><span data-stu-id="14ec6-181">Access workflow tasks and associated items using JSOM</span></span>
<span data-ttu-id="14ec6-182"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-182"></span></span>

<span data-ttu-id="14ec6-183">Da SharePoint-Add-Ins Clientcode Kommunikation mit SharePoint verwenden müssen, wird die folgenden Interaktion mit der SAP-Workflowaufgaben mithilfe des JavaScript-Objektmodells veranschaulichen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-183">Since SharePoint Add-ins must use client code to communicate with SharePoint, the following will demonstrate how to interact with the SAP workflow tasks using the JavaScript object model.</span></span>
  
    
    

### <a name="to-create-the-code"></a><span data-ttu-id="14ec6-184">So erstellen Sie den Code:</span><span class="sxs-lookup"><span data-stu-id="14ec6-184">To create the code:</span></span>


1. <span data-ttu-id="14ec6-185">Mit der rechten Maustaste in des Ordners **Seiten** im **Projektmappen-Explorer**, fügen Sie eine Seite .NET und nennen Sie es **ViewDetails.aspx**</span><span class="sxs-lookup"><span data-stu-id="14ec6-185">Right-click the **Pages** folder in the **Solution Explorer**, add a .NET page and name it **ViewDetails.aspx**</span></span>
    
  
2. <span data-ttu-id="14ec6-p110">Fügen Sie den folgenden HTML-Code im Abschnitt  `PlaceHolderAdditionalPageHead` . Wird den Stylesheet-Verweis festgelegt, laden Sie das Skript, und klicken Sie dann die zugehörige Workflowaufgaben aus SAP zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p110">Paste the following HTML in the  `PlaceHolderAdditionalPageHead` section. This will set the style sheet reference, load the script and then return the related workflow tasks from SAP.</span></span>
    
```XML
  
<link
    rel="Stylesheet" 
    type="text/css"
    href="../Content/App.css"/>

<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script 
    src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js" 
    type="text/javascript">
</script>      
<script 
    src="../Scripts/ViewDetails.js" 
    type="text/javascript">
</script>

```

3. <span data-ttu-id="14ec6-p111">Mit der rechten Maustaste in des Ordners **Scripts**, und fügen Sie eine JavaScript-Datei. Nennen Sie es **ViewDetails.js**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p111">Right-click the **Scripts** folder and add a JavaScript file. Name it **ViewDetails.js**.</span></span>
    
  
4. <span data-ttu-id="14ec6-190">Mit diesem Markup wird Folgendes:</span><span class="sxs-lookup"><span data-stu-id="14ec6-190">This markup will do the following:</span></span>
    
  - <span data-ttu-id="14ec6-191">Ruft die  `ClientContext` für die übergeordnete Website.</span><span class="sxs-lookup"><span data-stu-id="14ec6-191">Retrieves the  `ClientContext` for the parent web.</span></span>
    
  
  - <span data-ttu-id="14ec6-192">Ruft die  `TaskInstanceParentId` für die ausgewählte Workflowaufgabe mithilfe der Duet Workflow Listen-GUID und das ausgewählte Element-ID.</span><span class="sxs-lookup"><span data-stu-id="14ec6-192">Retrieves the  `TaskInstanceParentId` for the selected workflow task using the Duet workflow list GUID and the selected item ID.</span></span>
    
  
  - <span data-ttu-id="14ec6-193">Analysiert die  `TaskInstanceParentId` zum Abrufen von SAP-Ursprung und die ID für den Workflow in SAP.</span><span class="sxs-lookup"><span data-stu-id="14ec6-193">Parses the  `TaskInstanceParentId` to get SAP Origin and the ID for the workflow in SAP.</span></span>
    
  
  - <span data-ttu-id="14ec6-194">Lädt die Entitäten für externen Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-194">Loads the entities for the external content types.</span></span>
    
  
  - <span data-ttu-id="14ec6-195">Liest die bestimmten Workflow-Aufgabe von SAP mit bestimmten Suchmethode, indem Sie SAP Ursprung und der Workflow Vorgangsnummer für SAP als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="14ec6-195">Reads the specific workflow task from SAP using specific finder by passing SAP Origin and the workflow task ID for SAP as parameters.</span></span>
    
  
  - <span data-ttu-id="14ec6-196">Liest die zugeordneten Elemente für die Workflowaufgabe von SAP an.</span><span class="sxs-lookup"><span data-stu-id="14ec6-196">Reads the associated elements for the workflow task from SAP.</span></span>
    
  
5. <span data-ttu-id="14ec6-197">Es folgt der vollständige HTML und JavaScript für die Seite.</span><span class="sxs-lookup"><span data-stu-id="14ec6-197">The following is the complete HTML and JavaScript for the page.</span></span>
    
```
  
// This code runs when the DOM is ready. It ensures the SharePoint
// script files are loaded and then executes execOperation().
$(document).ready(function () {
  SP.SOD.executeFunc("sp.js", "SP.ClientContext", execOperation);
});

function execOperation() {
  retrieveTaskFromList();
}

function retrieveTaskFromList() {
  // Retrieves the ClientContext of the parent web.
  var clientContext = 
  new SP.ClientContext.get_current();
  var appContextSite = 
  new SP.AppContextSite(clientContext, 
      decodeURIComponent(getQueryStringParameter("SPHostUrl")));
  var web = appContextSite.get_web();
  // Loads the selected workflow task from the duet workflow list.
  var listGuid = decodeURIComponent(getQueryStringParameter("ListId"));
  var itemId = decodeURIComponent(getQueryStringParameter("ItemId"))
  this.workflowItem = web.get_lists().getById(
      listGuid.substring(1, listGuid.length - 1)).getItemById(itemId);
  clientContext.load(workflowItem);

  clientContext.executeQueryAsync(
    Function.createDelegate(this, this.onLoadingTaskSucceeded),
    Function.createDelegate(this, this.onError)
  );
}

function onLoadingTaskSucceeded() {
  var sapParameters = parseParentTaskId(workflowItem.
      get_item("TaskInstanceParentId"));
  getDataFromSAP(sapParameters);
}

// Parses the TaskInstanceParentId 
// to get SAP Origin and the id for the workflow in SAP.
function parseParentTaskId(parentTaskId) {
  var idlength = parseInt(parentTaskId.substring(0, 2));
  var sapParameters = new Object();
  if (parentTaskId.length > (17 + idlength)) {
    sapParameters.workitemId = parentTaskId.substring(5, 5 + idlength);
    sapParameters.sapOrigin = parentTaskId.substring(17 + idlength);
  }
  return sapParameters;
}
    
// Retrieves the workflow task and associated elements from SAP.
function getDataFromSAP(sapParameters) {
  context = new SP.ClientContext.get_current();
  //Loads the entities for the external content types.
  wfEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "WorkflowTaskCollection");
  context.load(wfEntity);
  wfExtensibleElementEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "ExtensibleElementCollection");
  context.load(wfExtensibleElementEntity);
  wfCommentsEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "CommentCollection");
  context.load(wfCommentsEntity);
  wfDecisionsEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "DecisionOptionCollection");
  context.load(wfDecisionsEntity);
  wfParticipantEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "ParticipantCollection");
  context.load(wfParticipantEntity);
  wfDescriptionEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "TaskDescriptionCollection");
  context.load(wfDescriptionEntity);
  wfAttachmentEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "AttachmentCollection");
  context.load(wfAttachmentEntity);

  // Loads a LOB system instances.
  lobSystem = wfEntity.getLobSystem();
  lobSystemInstanceCollection = lobSystem.getLobSystemInstances();
  context.load(lobSystemInstanceCollection);

  context.executeQueryAsync(onLoadingLOBInstanceSucceeded, onError);

  function onLoadingLOBInstanceSucceeded() {
    lobSystemInstance = lobSystemInstanceCollection.get_item(0);
    // Reads the workflow task from SAP using specific finder.
    var identifierValues = [sapParameters.sapOrigin, sapParameters.workitemId];
    var entityIdentity = SP.BusinessData.Runtime.EntityIdentity.
          newObject(context, identifierValues);
    wfEntityInstance = wfEntity.findSpecific(entityIdentity, 
          "ReadSpecificWorkflowTask", lobSystemInstance);
    context.load(wfEntityInstance);

    context.executeQueryAsync(onLoadingWorkflowSucceeded, onError);
  }

  function onLoadingWorkflowSucceeded() {
    // Reads the associated elements for the workflow task.
    var exFilterCollection = wfExtensibleElementEntity.getFilters(
        "GetExtensibleElementsFromWorkflowTaskCollection");
    context.load(exFilterCollection);
    exElementsCollection = wfExtensibleElementEntity.findAssociated(
        wfEntityInstance, "GetExtensibleElementsFromWorkflowTaskCollection", 
        exFilterCollection, lobSystemInstance);
    context.load(exElementsCollection);

    var comFilterCollection = wfCommentsEntity.getFilters(
        "GetCommentsFromWorkflowTaskCollection");
    context.load(comFilterCollection);
    commentsCollection = wfCommentsEntity.findAssociated(
        wfEntityInstance, "GetCommentsFromWorkflowTaskCollection", 
        comFilterCollection, lobSystemInstance);
    context.load(commentsCollection);

    var decFilterCollection = wfDecisionsEntity.getFilters(
        "GetDecisionOptionsFromWorkflowTaskCollection");
    context.load(decFilterCollection);
    decisionsCollection = wfDecisionsEntity.findAssociated(
        wfEntityInstance, "GetDecisionOptionsFromWorkflowTaskCollection", 
        decFilterCollection, lobSystemInstance);
    context.load(decisionsCollection);

    var partFilterCollection = wfParticipantEntity.getFilters(
        "GetParticipantsFromWorkflowTaskCollection");
    context.load(partFilterCollection);
    participantsCollection = wfParticipantEntity.findAssociated(
        wfEntityInstance, "GetParticipantsFromWorkflowTaskCollection", 
        partFilterCollection, lobSystemInstance);
    context.load(participantsCollection);

    var descFilterCollection = wfDescriptionEntity.getFilters(
        "GetDescriptionFromWorkflowTaskCollection");
    context.load(descFilterCollection);
    descriptionCollection = wfDescriptionEntity.findAssociated(
        wfEntityInstance, "GetDescriptionFromWorkflowTaskCollection", 
        descFilterCollection, lobSystemInstance);
    context.load(descriptionCollection);

    var attaFilterCollection = wfAttachmentEntity.getFilters(
        "GetAttachmentsFromWorkflowTaskCollection");
    context.load(attaFilterCollection);
    attachmentCollection = wfAttachmentEntity.findAssociated(
        wfEntityInstance, "GetAttachmentsFromWorkflowTaskCollection", 
        attaFilterCollection, lobSystemInstance);
    context.load(attachmentCollection);

    context.executeQueryAsync(getUpdatedDataSucceeded, onError);
  }

  function getUpdatedDataSucceeded() {
    alert("# of extensible elements: " + exElementsCollection.get_count() + 
      "\\n# of comments: " + commentsCollection.get_count() + 
      "\\n# of decision options: " + decisionsCollection.get_count() + 
      "\\n# of attachments: " + attachmentCollection.get_count() + 
      "\\n# of participants: " + participantsCollection.get_count());
  }

  function onError(sender, e) {
    alert("Request failed. " + e.get_message() +
          "\\n" + e.get_stackTrace());
  }
}

// Retrieves a query string value.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve)
      return singleParam[1];
  }
}

```

6. <span data-ttu-id="14ec6-198">Öffnen Sie die **Datei AppManifest.xml** aus.</span><span class="sxs-lookup"><span data-stu-id="14ec6-198">Open the **AppManifest.xml** file.</span></span>
    
  
7. <span data-ttu-id="14ec6-199">**Berechtigungsanfragen** wählen Sie **Bereich**, **Web- und Berechtigung** aus und legen Sie den Wert zum *Lesen von*  .</span><span class="sxs-lookup"><span data-stu-id="14ec6-199">In **Permission Requests**, select **Scope**, **Web and Permission** and set the value to *Read*  .</span></span>
    
  
8. <span data-ttu-id="14ec6-200">Drücken Sie **F5**, um die Lösung in der Duet-Workflow-Website bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="14ec6-200">Press **F5** to deploy the solution to the duet workflow site.</span></span>
    
  
9. <span data-ttu-id="14ec6-p112">Wechseln Sie auf **Meine Workflowaufgaben**. Wählen Sie in der ECB-Menü **Anzeigen** oder wählen Sie eine Aufgabe aus, und drücken Sie **Details anzeigen** im Menüband. Sie werden zur **ViewDetails.aspx** umgeleitet werden, in dem Sie eine Benachrichtigung mit der Anzahl für einige der Elemente, die den Workflow zugeordnet sind angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p112">Go to **My Workflow Tasks**. Select **View Details** in the ECB menu or select a task and press **View Details** in the ribbon. You will be redirected to **ViewDetails.aspx** where you will see an alert containing the count for some of the elements associated to the workflow.</span></span>
    
  

## <a name="using-html-and-javascript-to-render-custom-ui"></a><span data-ttu-id="14ec6-204">Mithilfe von HTML und JavaScript zum Rendern von Custom UI</span><span class="sxs-lookup"><span data-stu-id="14ec6-204">Using HTML and JavaScript to render Custom UI</span></span>
<span data-ttu-id="14ec6-205"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-205"></span></span>

<span data-ttu-id="14ec6-206">Ersetzen Sie den folgenden Code in ViewDetails.aspx mit eigenen HTML und JavaScript zum Rendern von einer eigene benutzerdefinierten Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="14ec6-206">In ViewDetails.aspx, replace the following code with your own HTML and JavaScript to render your own custom UI.</span></span>
  
    
    

```

alert("# of extensible elements: " + exElementsCollection.get_count() +
"\\n# of comments: " + commentsCollection.get_count() + 
"\\n# of decision options: " + decisionsCollection.get_count() + 
"\\n# of attachments: " + attachmentCollection.get_count() + 
"\\n# of participants: " + participantsCollection.get_count());

```


## <a name="adding-lync-control-to-your-details-page"></a><span data-ttu-id="14ec6-207">Hinzufügen von Lync-Steuerelement auf der Detailseite an</span><span class="sxs-lookup"><span data-stu-id="14ec6-207">Adding Lync Control to your details page</span></span>
<span data-ttu-id="14ec6-208"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-208"></span></span>

<span data-ttu-id="14ec6-p113">Hier ist eine Option für die benutzerdefinierte Benutzeroberfläche. Hinzufügen eines Steuerelements Lync erhalten Sie die Möglichkeit, die Lync-Kontakte aus der benutzerdefinierten Seite kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="14ec6-p113">Here is one option for your custom user interface. Adding a Lync control will give you the ability to communicate with your Lync contacts from the custom page.</span></span>
  
    
    

### <a name="to-add-a-lync-control"></a><span data-ttu-id="14ec6-211">So fügen Sie ein Lync-Steuerelement hinzu:</span><span class="sxs-lookup"><span data-stu-id="14ec6-211">To add a Lync control:</span></span>


1. <span data-ttu-id="14ec6-212">Mit der rechten Maustaste im Projektmappen-Explorer Ordner **Scripts**, fügen Sie eine JavaScript-Datei, und nennen Sie sie **People.js**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-212">Right-click the **Scripts** folder in solution explorer, add a JavaScript file and name it **People.js**.</span></span>
    
  
2. <span data-ttu-id="14ec6-213">Das folgende Markup wird:</span><span class="sxs-lookup"><span data-stu-id="14ec6-213">The following markup will:</span></span>
    
  - <span data-ttu-id="14ec6-214">Fügen Sie Anwesenheitsinformationen-Steuerelement für die Teilnehmer des Vorgangs.</span><span class="sxs-lookup"><span data-stu-id="14ec6-214">Add presence control for the participants of the task.</span></span>
    
  
  - <span data-ttu-id="14ec6-215">Lync-Integration in Legende für Teilnehmer für die Zusammenarbeit mit einem Klick für den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="14ec6-215">Lync integration in callout for participants for one-click collaboration for the task.</span></span>
    
  

    <span data-ttu-id="14ec6-216">Fügen Sie den nachfolgenden Code auf der Seite **People.js** ein.</span><span class="sxs-lookup"><span data-stu-id="14ec6-216">Paste the following code into the **People.js** page.</span></span>
    


```
  
var presenceControlCount = 0;
var appWebURL = '';

function AddPeopleControl(userName) {
  var id = "pc_participants_" + presenceControlCount++;
  var prevId = null;

  return "<div id='" + id + "' ></div>" + 
    "<script>" + 
      "LoadPeopleControl('" +id+ "', '" +prevId+ "', '" +userName+ "');" + 
    "</script>";
}

function LoadPeopleControl(elemId, prevId, user) {
  var prevElement = null;
  var element = $("#" + elemId);
  user = "fareast\\\\" + user.toLowerCase();

  GetUsersInfo(user, element, prevElement);
}

function GetUsersInfo(accountName, htmlElement, waitforElement) {
  var clientContext = SP.ClientContext.get_current();
  var website = clientContext.get_web();

  clientContext.load(website);
  clientContext.executeQueryAsync(onRequestSucceeded, onRequestFailed);

  function onRequestSucceeded() {
    appWebURL = website.get_url();
    var queryURL = appWebURL + 
    "/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)?@v='"
     + accountName + "'";

    jQuery.ajax({
      url: queryURL,
      type: "GET",
      headers: {
        "ACCEPT": "application/json;odata=verbose"
      },
      success: function (data) {
        var html = [];
        var i = 0;

        var id = htmlElement[0].id + "_";

        var about_info;

        if (data.d.UserProfileProperties != null) {
          for (i = 0; i < data.d.UserProfileProperties.results.length; i++) {
            if (data.d.UserProfileProperties.results[i].Key == "AboutMe") {
              about_info = data.d.UserProfileProperties.results[i].Value;
            }
          }
        }

        var email = data.d.Email;
        var profileUrl = data.d.UserUrl;
        var pictureUrl = data.d.PictureUrl;
        var name = data.d.DisplayName;

        if (name == null) {
          name = accountName;
        }

        var isFollowed = data.d.IsFollowed;

        var html = [
          "<table>",
          "<tr>",
          "<td>",
            "<span class='ms-spimn-presenceWrapper ms-spimn-imgSize-5x48'> ",
              "<img id='imn_" + id + "_" + i++ + ",type=smtp'" ,
                "onload=\\"IMNRC('", email, "')\\" ",
                "class='ms-spimn-img ms-spimn-presence-offline-5x48x32 '", 
                "title='' name='imnmark' alt='Offline' ", 
                "src='/_layouts/15/images/spimn.png' ", 
                "sip='" + email + "' showofflinepawn='1'>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-imnSpan'>",
              "<a class='ms-imnlink' tabindex='-1'", 
                "onclick='IMNImageOnClick(event);return false;' href='#'>",
                "<img id='imn_" + id + "_" + i++ + ",type=smtp'",
                  "onload=\\"IMNRC('", email, "')\\"",
                  "class=' ms-hide' title='' name='imnmark' alt='Away' ",
                  "src='/_layouts/15/images/spimn.png' ",
                  "sip='" + email + "' showofflinepawn='1'>",
              "</a>",
              "<a class='ms-subtleLink ms-peopleux-imgUserLink' ",
                "onclick='GoToLinkOrDialogNewWindow(this);return false;' ",
                "href='" + profileUrl + "'>",
                "<span style='width: 48px; height: 48px;'" ,
                  "class='ms-peopleux-userImgWrapper'>",
                "<img style='cliptop: 0px; clipright: 48px;" ,
                  "clipbottom: 48px; clipleft: 0px; ",
                  "min-height: 48px; min-width: 48px; max-width: 48px;' ",
                  "class='ms-peopleux-userImg' alt='' src='" +pictureUrl+ "'>",
                "</span>",
              "</a>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-spimn-presenceWrapper ms-spimn-imgSize-5x48'>",
            "<img id='imn_" + id + "_" + i++ + ",type=smtp' ",
              "onload=\\"IMNRC('", email, "')\\" ",
              "class='ms-spimn-img ms-spimn-presence-offline-5x48x32' ",
              "title='' name='imnmark' alt='Offline' ",
              "src='/_layouts/15/images/spimn.png' ",
              "sip='" + email + "' showofflinepawn='1'>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-microfeed-userName ms-textLarge' ",
              "style='font-size: medium;'>" + name + "<br/>",
              "<div id='people_callout_" + id + "_" + i + "' ",
                "class='ms-microfeed-button ms-textSmall" + 
                "ms-secondaryCommandLink ms-microfeed-footerButton' ",
                "align='center' ",
                "style='cursor:pointer; font-size:small;' > more... </div>",
                  "<script>",
                    "RegisterCallOut(\\"people_callout_" + id + "_" + i + 
                      "\\",\\"" + name + "\\",\\"" + encodeURI(about_info) + 
                      "\\",\\"" + profileUrl + "\\",\\"" + isFollowed + "\\");",
                  "</script>",
            "</span>",
          "</td>",
          "</tr>",
          "</table>",
        ];

        htmlElement.html(html.join(''));
      }

    });
  }
  function onRequestFailed(sender, args) {
    alert('Error: ' + args.get_message());
  }

}

function RegisterCallOut(divId, displayName, aboutme, userUrl, isFollowed) {
  if (typeof CalloutManager !== "object" || typeof Callout !== "function" || typeof CalloutAction !== "function")
    return;

  var launchdiv = document.getElementById(divId);
  var calloutId = divId + "_callout";
  var html = [];

  html.push("<br/>");

  if (aboutme == "") {
    html.push("No Information Found about this person.");
  }
  else {
    html.push(decodeURI(aboutme));
  }

  html.push("<hr/>");

  if (isFollowed == true) {
    html.push("<div>You are <b>following</b> this person</div>");
  }
  else {
    html.push("<div >You are <b>not following</b> this person</div>");
  }

  var callout = CalloutManager.createNew({
    launchPoint: launchdiv,
    openOptions: {
      closeCalloutOnBlur: true,
      event: "click",
      showCloseButton: true
    },
    ID: calloutId,
    title: displayName,
    content: html.join("")
  });

  callout.addAction(new CalloutAction({
    text: "View Profile", onClickCallback: 
    function (calloutActionClickEvent, calloutAction) {
      window.open(userUrl);
    }
  }));
}

```


    > **Note:**
      > The user name of the participant in company's network is same as that in SAP. 
3. <span data-ttu-id="14ec6-217">Öffnen Sie die Seite **AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-217">Open the **AppManifest.xml** page.</span></span>
    
  
4. <span data-ttu-id="14ec6-218">**Berechtigungsanfragen** wählen Sie **Bereich**, **Benutzerprofile und Berechtigung** und legen Sie dessen Wert zum *Lesen*  .</span><span class="sxs-lookup"><span data-stu-id="14ec6-218">In **Permission Requests**, select **Scope**, **User Profiles and Permission** and set its value to *Read*  .</span></span>
    
  
5. <span data-ttu-id="14ec6-219">Kopieren Sie das folgende Markup, und fügen Sie ihn im Abschnitt  `PlaceHolderAdditionalPageHead` **ViewDetails.aspx**.</span><span class="sxs-lookup"><span data-stu-id="14ec6-219">Copy the following markup and paste it in the  `PlaceHolderAdditionalPageHead` section in **ViewDetails.aspx**.</span></span>
    
```HTML
  
<script src="../Scripts/People.js" type="text/javascript"></script>
```

6. <span data-ttu-id="14ec6-220">Rufen Sie auf, um das Steuerelement Anwesenheitsinformationen für einen Teilnehmer hinzuzufügen, Folgendes:</span><span class="sxs-lookup"><span data-stu-id="14ec6-220">To add the presence control for a participant, call the following:</span></span> 
    
```
  AddPeopleControl(userName);
```


## <a name="additional-resources"></a><span data-ttu-id="14ec6-221">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="14ec6-221">Additional resources</span></span>
<span data-ttu-id="14ec6-222"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="14ec6-222"></span></span>


-  [<span data-ttu-id="14ec6-223">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="14ec6-223">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="14ec6-224">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="14ec6-224">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="14ec6-225">Eine Einführung in SAP Business Workflow</span><span class="sxs-lookup"><span data-stu-id="14ec6-225">An introduction to SAP Business Workflow</span></span>](http://scn.sap.com/docs/DOC-31056)
    
  

