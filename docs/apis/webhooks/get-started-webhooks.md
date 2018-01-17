---
title: Erste Schritte mit SharePoint-Webhooks
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 57bdb8406760d8951900353418e6794e9cdf45c9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-with-sharepoint-webhooks"></a><span data-ttu-id="8c8f6-102">Erste Schritte mit SharePoint-Webhooks</span><span class="sxs-lookup"><span data-stu-id="8c8f6-102">Get started with SharePoint webhooks</span></span>

<span data-ttu-id="8c8f6-103">In diesem Artikel wird beschrieben, wie Sie eine Anwendung zum Hinzufügen und Bearbeiten von SharePoint-Webhook-Anforderungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-103">This article describes how to build an application that adds and handles SharePoint webhook requests.</span></span> <span data-ttu-id="8c8f6-104">Sie erfahren, wie Sie SharePoint-Webhook-Anforderungen mit dem [Postman-Client](https://www.getpostman.com/) schnell erstellen und ausführen können, unter Verwendung einer einfachen ASP.NET-Web-API als Webhook-Empfänger.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-104">You will learn how to use [Postman client](https://www.getpostman.com/) to construct and execute SharePoint webhook requests quickly while interacting with a simple ASP.NET Web API as the webhook receiver.</span></span>

<span data-ttu-id="8c8f6-105">Für das Beispiel in diesem Artikel werden Sie mit einfachen HTTP-Anforderungen arbeiten. Sie eignen sich ideal, um Ihnen einen ersten Einblick in die Funktionsweise von Webhooks zu geben.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-105">In this article, you will use plain HTTP requests, which is useful for helping you to understand how webhooks work.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8c8f6-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="8c8f6-106">Prerequisites</span></span>

<span data-ttu-id="8c8f6-107">Damit Sie die Schritt-für-Schritt-Anleitungen in diesem Artikel nachvollziehen können, müssen Sie die folgenden Tools herunterladen und installieren:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-107">To complete the step-by-step instructions in this article, download and install the following tools:</span></span>

* <span data-ttu-id="8c8f6-108">[Google Chrome-Browser](http://google.com/chrome)</span><span class="sxs-lookup"><span data-stu-id="8c8f6-108">[Google Chrome Browser](http://google.com/chrome)</span></span>
* <span data-ttu-id="8c8f6-109">[Postman](https://www.getpostman.com/)</span><span class="sxs-lookup"><span data-stu-id="8c8f6-109">[Postman](https://www.getpostman.com/)</span></span>
* [<span data-ttu-id="8c8f6-110">Visual Studio Community Edition</span><span class="sxs-lookup"><span data-stu-id="8c8f6-110">Visual Studio Community Edition</span></span>](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)
* <span data-ttu-id="8c8f6-111">[ngrok](https://ngrok.com/) - Informationen zur Installation von ngrok finden Sie in Englisch unter [Download and Installation](https://ngrok.com/download) auf der ngrok-Website.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-111">[ngrok](https://ngrok.com/) - See [Download and Installation](https://ngrok.com/download) to install ngrok.</span></span>
* <span data-ttu-id="8c8f6-112">Ein Office 365-Abonnement mit SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-112">An Office 365 Subscription with SharePoint Online.</span></span> <span data-ttu-id="8c8f6-113">Wenn Sie neu bei Office 365 sind, können Sie sich auch [für ein Office 365-Entwicklerkonto registrieren](http://dev.office.com/devprogram).</span><span class="sxs-lookup"><span data-stu-id="8c8f6-113">If you are new to Office 365, you can also [sign up for an Office 365 developer account](http://dev.office.com/devprogram).</span></span>

## <a name="step-1-register-a-microsoft-azure-active-directory-ad-application-for-postman-client"></a><span data-ttu-id="8c8f6-114">Schritt 1: Registrieren einer Microsoft Azure Active Directory (AD)-Anwendung für den Postman-Client</span><span class="sxs-lookup"><span data-stu-id="8c8f6-114">Step 1: Register a Microsoft Azure Active Directory (AD) application for Postman client</span></span>

<span data-ttu-id="8c8f6-115">Damit der Postman-Client mit SharePoint kommunizieren kann, müssen Sie eine Azure AD-App in dem Azure AD-Mandanten registrieren, der mit Ihrem Office 365-Mandanten verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-115">In order for the Postman client to communicate with SharePoint, you will need to register an Azure AD app in your Azure AD tenant associated with your Office 365 tenant.</span></span> 

<span data-ttu-id="8c8f6-116">Registrieren Sie die Anwendung unbedingt als „Webanwendung“.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-116">Ensure that you register the application as a "Web Application".</span></span>

<span data-ttu-id="8c8f6-117">Für den Zugriff auf SharePoint Online ist es wichtig, der Azure AD-App Berechtigungen für die **Office 365 SharePoint Online**-Anwendung zu gewähren und die Berechtigung **read and write items and lists in all site collections** auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-117">To access SharePoint Online, it's important to grant the Azure AD app permissions to the **Office 365 SharePoint Online** application and select the **read and write items and lists in all site collections** permission.</span></span>

> <span data-ttu-id="8c8f6-118">Weitere Informationen dazu, wie Sie Azure AD-Anwendungen hinzufügen und Anwendungen Berechtigungen gewähren können, finden Sie unter [Hinzufügen einer Anwendung](https://azure.microsoft.com/en-us/documentation/articles/active-directory-integrating-applications/#adding-an-application).</span><span class="sxs-lookup"><span data-stu-id="8c8f6-118">For more information about adding an Azure AD application and granting permissions to applications, see [Adding an application](https://azure.microsoft.com/en-us/documentation/articles/active-directory-integrating-applications/#adding-an-application).</span></span> 

<span data-ttu-id="8c8f6-p103">Geben Sie den folgenden Endpunkt als Antwort (Umleitungs)-URL für die App ein. An diesen Endpunkt wird Azure AD die Authentifizierungsantwort senden. Bei erfolgreicher Authentifizierung enthält diese das Zugriffstoken.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p103">Enter the following endpoint as the Reply (Redirect) URL for the app. This is the endpoint to which Azure AD will send the authentication response; including the access token if authentication was successful.</span></span>

```html
https://www.getpostman.com/oauth2/callback
```

<span data-ttu-id="8c8f6-121">Generieren Sie auch einen „Schlüssel“, der als geheimer Clientschlüssel fungiert.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-121">Also generate a "Key", which will be the client secret.</span></span>

<span data-ttu-id="8c8f6-122">Die folgenden Eigenschaften werden in späteren Schritten benötigt. Kopieren Sie sie also an einen sicheren Ort:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-122">The following properties are required in later steps, so copy them to a safe place:</span></span>

* <span data-ttu-id="8c8f6-123">Client-ID</span><span class="sxs-lookup"><span data-stu-id="8c8f6-123">Client Id</span></span>
* <span data-ttu-id="8c8f6-124">Client Secret</span><span class="sxs-lookup"><span data-stu-id="8c8f6-124">Client Secret</span></span> 

## <a name="step-2-build-a-webhook-receiver"></a><span data-ttu-id="8c8f6-125">Schritt 2: Erstellen eines Webhook-Empfängers</span><span class="sxs-lookup"><span data-stu-id="8c8f6-125">Step 2: Build a webhook receiver</span></span>

<span data-ttu-id="8c8f6-126">In diesem Beispiel erstellen Sie den Webhook-Empfänger mit einem Visual Studio-Web-API-Projekt.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-126">For this project, use the Visual Studio Web API project to build the webhook receiver.</span></span>

### <a name="create-a-new-aspnet-web-api-project"></a><span data-ttu-id="8c8f6-127">Erstellen eines neuen ASP.NET-Web-API-Projekts</span><span class="sxs-lookup"><span data-stu-id="8c8f6-127">Create a new ASP.NET Web API project</span></span>

* <span data-ttu-id="8c8f6-128">Öffnen Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-128">Open Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-129">Wählen Sie **Datei > Neu > Projekt** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-129">Choose **File > New > Project**.</span></span>
* <span data-ttu-id="8c8f6-130">Wählen Sie im Bereich **Vorlagen** die Option **Installed Templates** aus, und erweitern Sie den Knoten **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-130">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> 
* <span data-ttu-id="8c8f6-131">Wählen Sie unter **Visual C#** die Option **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-131">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="8c8f6-132">Wählen Sie aus der Liste der Projektvorlagen die Option **ASP.NET-Webanwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-132">In the list of project templates, select **ASP.NET Web Application**.</span></span> 
* <span data-ttu-id="8c8f6-133">Nennen Sie das Projekt **SPWebhooksReceiver**, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-133">Name the project **SPWebhooksReceiver** and choose **OK**.</span></span>
* <span data-ttu-id="8c8f6-134">Wählen Sie im Dialogfeld **Neues ASP.NET-Projekt** die Vorlage **Web API** aus der Gruppe **ASP.NET 4.5.\*** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-134">In the **New ASP.NET Project** dialog, select the **Web API** template from the **ASP.NET 4.5.\*** group.</span></span> 
* <span data-ttu-id="8c8f6-135">Ändern Sie die Authentifizierungsoption in **Keine Authentifizierung**. Klicken Sie dazu auf die Schaltfläche **Authentifizierung ändern**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-135">Change the authentication to **No Authentication** by choosing the **Change Authentication** button.</span></span>
* <span data-ttu-id="8c8f6-136">Klicken Sie auf **OK**, um das Web-API-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-136">Choose **OK** to create the Web API project.</span></span>

> [!NOTE]
> <span data-ttu-id="8c8f6-137">Sie können die Option **In der Cloud hosten** deaktivieren, da Sie dieses Projekt nicht in der Cloud bereitstellen werden.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-137">**Note:** You can uncheck the Host in the cloud option because this project will not be deployed to the cloud.</span></span>

<span data-ttu-id="8c8f6-138">Visual Studio erstellt nun Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-138">Visual Studio will create your project.</span></span>

### <a name="webhook-receiver"></a><span data-ttu-id="8c8f6-139">Webhook-Empfänger</span><span class="sxs-lookup"><span data-stu-id="8c8f6-139">Webhook receiver</span></span>

#### <a name="install-nuget-packages"></a><span data-ttu-id="8c8f6-140">Installieren der NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="8c8f6-140">Install Nuget packages</span></span>

<span data-ttu-id="8c8f6-p105">Verwenden Sie die ASP.NET-Web-API-Ablaufverfolgung zur Protokollierung der eingehenden SharePoint-Anforderungen. Gehen Sie wie folgt vor, um das Paket für die Ablaufverfolgung zu installieren:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p105">Use ASP.NET Web API Tracing to log the requests coming from SharePoint. The following steps will install the tracing package:</span></span>

* <span data-ttu-id="8c8f6-143">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-143">Go to the **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-144">Öffnen Sie per Rechtsklick das Kontextmenü des Projekts, und wählen Sie **NuGet-Pakete verwalten...** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-144">Open the context menu (right-click) for the project and choose **Manage Nuget Packages...**.</span></span>
* <span data-ttu-id="8c8f6-145">Geben Sie **Microsoft.AspNet.WebApi.Tracing** in das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-145">In the search box, enter **Microsoft.AspNet.WebApi.Tracing**.</span></span> 
* <span data-ttu-id="8c8f6-146">Wählen Sie aus den Suchergebnissen das Paket **Microsoft.AspNet.WebApi.Tracing** aus, und klicken Sie auf **Installieren**, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-146">In the search results, select the **Microsoft.AspNet.WebApi.Tracing** package and choose **Install** to install the package.</span></span>

#### <a name="spwebhooknotification-model"></a><span data-ttu-id="8c8f6-147">SPWebhookNotification-Modell</span><span class="sxs-lookup"><span data-stu-id="8c8f6-147">SPWebhookNotification model</span></span>

<span data-ttu-id="8c8f6-148">Jede vom Dienst generierte Benachrichtigung wird in eine **WebhookNotification**-Instanz serialisiert.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-148">Each notification generated by the service is serialized into a **webhookNotifiation** instance.</span></span> <span data-ttu-id="8c8f6-149">Sie müssen ein einfaches Modell erstellen, das diese Benachrichtigungsinstanz abbildet.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-149">You need to build a simple model that represents this notification instance.</span></span>

* <span data-ttu-id="8c8f6-150">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-150">Go to **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-151">Öffnen Sie per Rechtsklick das Kontextmenü des Ordners **Models**, und wählen Sie **Hinzufügen -> Klasse** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-151">Open the context menu (right-click) for the **Models** folder and choose **Add->Class**.</span></span>
* <span data-ttu-id="8c8f6-152">Geben Sie **SPWebhookNotification** als Name für die Klasse ein, und klicken Sie auf **Hinzufügen**, um die Klasse zu Ihrem Projekt hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-152">Enter **SPWebhookNotification** as the class name and choose **Add** to add the class to your project.</span></span>
* <span data-ttu-id="8c8f6-153">Tragen Sie den folgenden Code in den Body der Klasse **SPWebhookNotification** ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-153">Add the following code to the body of the **SPWebhookNotification** class:</span></span>

    ```cs
    public string SubscriptionId { get; set; }

    public string ClientState { get; set; }

    public string ExpirationDateTime { get; set; }

    public string Resource { get; set; }

    public string TenantId { get; set; }

    public string SiteUrl { get; set; }

    public string WebId { get; set; }
    ```

#### <a name="spwebhookcontent-model"></a><span data-ttu-id="8c8f6-154">SPWebhookContent-Modell</span><span class="sxs-lookup"><span data-stu-id="8c8f6-154">SPWebhookContent model</span></span>

<span data-ttu-id="8c8f6-p107">Da in einer einzigen Anforderung mehrere Benachrichtigungen an einen Webhook-Empfänger gesendet werden können, werden alle Anforderungen in einem Objekt mit einem einzigen Arraywert zusammengefasst. Erstellen Sie ein einfaches Modell, das dieses Array abbildet.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p107">Because multiple notifications can be submitted to your webhook receiver in a single request, they are combined together in an object with a single array value. Build a simple model that represents the array.</span></span>

* <span data-ttu-id="8c8f6-157">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-157">Go to **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-158">Öffnen Sie per Rechtsklick das Kontextmenü des Ordners **Models**, und wählen Sie **Hinzufügen -> Klasse** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-158">Open the context menu (right-click) for the **Models** folder and choose **Add->Class**.</span></span>
* <span data-ttu-id="8c8f6-159">Geben Sie **SPWebhookContent** als Name für die Klasse ein, und klicken Sie auf **Hinzufügen**, um die Klasse zu Ihrem Projekt hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-159">Enter **SPWebhookContent** as the class name and choose **Add** to add the class to your project.</span></span>
* <span data-ttu-id="8c8f6-160">Tragen Sie den folgenden Code in den Body der Klasse **SPWebhookContent**ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-160">Add the following code to the body of the **SPWebhookContent** class:</span></span>

    ```cs
     public List<SPWebhookNotification> Value { get; set; }
    ```

#### <a name="sharepoint-webhook-client-state"></a><span data-ttu-id="8c8f6-161">SharePoint-Webhook-Clientstatus</span><span class="sxs-lookup"><span data-stu-id="8c8f6-161">SharePoint webhook client state</span></span>

<span data-ttu-id="8c8f6-p108">Webhooks erlauben die Verwendung eines optionalen Zeichenfolgenwerts, der in der Benachrichtigungsmitteilung für Ihr Abonnement zurückgegeben wird. Anhand dieses Werts lässt sich verifizieren, dass die Anforderung wirklich von einer vertrauenswürdigen Quelle stammt, in diesem Fall von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p108">Webhooks provide the ability to use an optional string value that is passed back in the notification message for your subscription. This can be used to verify that the request is indeed coming from the source you trust, which in this case is SharePoint.</span></span> 

<span data-ttu-id="8c8f6-164">Fügen Sie einen Clientzustandswert hinzu, mit dem die Anwendung die eingehenden Anforderungen verifizieren kann.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-164">Add a client state value with which the application can verify the incoming requests.</span></span>

* <span data-ttu-id="8c8f6-165">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-165">Go to **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-166">Öffnen Sie die Datei **web.config**, und fügen Sie den folgenden Schlüssel als Clientzustand im Abschnitt `<appSettings>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-166">Open the **web.config** file and add the following key as the client state to the `<appSettings>` section:</span></span>

    ```xml
    <add key="webhookclientstate" value="A0A354EC-97D4-4D83-9DDB-144077ADB449"/>
    ```

#### <a name="enable-tracing"></a><span data-ttu-id="8c8f6-167">Aktivieren der Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="8c8f6-167">Enable tracing</span></span>

<span data-ttu-id="8c8f6-168">Aktivieren Sie in der Datei **web.config** die Ablaufverfolgung, indem Sie den folgenden Schlüssel im Element `<system.web>` im Abschnitt `<configuration>` hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-168">In the **web.config** file, enable tracing by adding the following key inside the `<system.web>` element in the `<configuration>` section:</span></span>

```xml
<trace enabled="true"/>
```

<span data-ttu-id="8c8f6-169">Da ein Ablauf-Writer erforderlich ist, müssen Sie einen Ablauf-Writer zur Controllerkonfiguration hinzufügen. (Verwenden Sie für dieses Beispiel den Writer unter **System.Diagnostics**.)</span><span class="sxs-lookup"><span data-stu-id="8c8f6-169">A trace writer is required, so you must add a trace writer to the controller configuration (in this case use the one from **System.Diagnostics**).</span></span>

* <span data-ttu-id="8c8f6-170">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-170">Go to **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-171">Öffnen Sie **WebApiConfig.cs** im Ordner **App_Start**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-171">Open **WebApiConfig.cs** in the **App_Start** folder.</span></span>
* <span data-ttu-id="8c8f6-172">Fügen Sie die folgende Zeile in die Methode **Register** ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-172">Add the following line inside the **Register** method:</span></span>

    ```cs
    config.EnableSystemDiagnosticsTracing();
    ```

#### <a name="sharepoint-webhook-controller"></a><span data-ttu-id="8c8f6-173">SharePoint-Webhook-Controller</span><span class="sxs-lookup"><span data-stu-id="8c8f6-173">SharePoint webhook controller</span></span>

<span data-ttu-id="8c8f6-174">Jetzt erstellen Sie den Webhook-Empfänger-Controller, der die eingehenden Anforderungen von SharePoint bearbeiten und die entsprechenden Aktionen einleiten wird.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-174">Now build the webhook receiver controller that will handle the incoming requests from SharePoint and take action accordingly.</span></span>

* <span data-ttu-id="8c8f6-175">Wechseln Sie in Visual Studio zum **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-175">Go to **Solution Explorer** in Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-176">Öffnen Sie per Rechtsklick das Kontextmenü des Ordners **Controllers**, und wählen Sie **Hinzufügen -> Controller** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-176">Open the context menu (right-click) for the **Controllers** folder and choose **Add->Controller**.</span></span>
* <span data-ttu-id="8c8f6-177">Wählen Sie im Dialogfeld **Gerüst hinzufügen** die Option **Web API 2-Controller – Leer** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-177">In the **Add Scaffold** dialog, select **Web API 2 Controller - Empty**.</span></span>
* <span data-ttu-id="8c8f6-178">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-178">Choose **Add**.</span></span>
* <span data-ttu-id="8c8f6-179">Nennen Sie den Controller **SPWebhookController**, und klicken Sie auf **Hinzufügen**, um den API-Controller zu Ihrem Projekt hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-179">Name the controller **SPWebhookController** and choose **Add** to add the API controller to your project.</span></span>
* <span data-ttu-id="8c8f6-180">Ersetzen Sie die Anweisungen des Typs `using` durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-180">Replace the `using` statements with the following code:</span></span>

    ```cs
    using Newtonsoft.Json;
    using SPWebhooksReceiver.Models;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web;
    using System.Web.Http;
    using System.Web.Http.Tracing;
    ```

* <span data-ttu-id="8c8f6-181">Ersetzen Sie den Code in der Klasse **SPWebhookController** durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-181">Replace the code in the **SPWebhookController** class with the following code:</span></span>

    ```cs
    [HttpPost]
    public HttpResponseMessage HandleRequest()
    {
        HttpResponseMessage httpResponse = new HttpResponseMessage(HttpStatusCode.BadRequest);
        var traceWriter = Configuration.Services.GetTraceWriter();
        string validationToken = string.Empty;
        IEnumerable<string> clientStateHeader = new List<string>();
        string webhookClientState = ConfigurationManager.AppSettings["webhookclientstate"].ToString();

        if (Request.Headers.TryGetValues("ClientState", out clientStateHeader))
        {
            string clientStateHeaderValue = clientStateHeader.FirstOrDefault() ?? string.Empty;

            if (!string.IsNullOrEmpty(clientStateHeaderValue) && clientStateHeaderValue.Equals(webhookClientState))
            {
                traceWriter.Trace(Request, "SPWebhooks", 
                    TraceLevel.Info, 
                    string.Format("Received client state: {0}", clientStateHeaderValue));

                var queryStringParams = HttpUtility.ParseQueryString(Request.RequestUri.Query);

                if (queryStringParams.AllKeys.Contains("validationtoken"))
                {
                    httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
                    validationToken = queryStringParams.GetValues("validationtoken")[0].ToString();
                    httpResponse.Content = new StringContent(validationToken);

                    traceWriter.Trace(Request, "SPWebhooks", 
                        TraceLevel.Info, 
                        string.Format("Received validation token: {0}", validationToken));                        
                    return httpResponse;
                }
                else
                {
                    var requestContent = Request.Content.ReadAsStringAsync().Result;

                    if (!string.IsNullOrEmpty(requestContent))
                    {
                        SPWebhookNotification notification = null;

                        try
                        {
                            var objNotification = JsonConvert.DeserializeObject<SPWebhookContent>(requestContent);
                            notification = objNotification.Value[0];
                        }
                        catch (JsonException ex)
                        {
                            traceWriter.Trace(Request, "SPWebhooks", 
                                TraceLevel.Error, 
                                string.Format("JSON deserialization error: {0}", ex.InnerException));
                            return httpResponse;
                        }

                        if (notification != null)
                        {
                            Task.Factory.StartNew(() =>
                            {
                                 //handle the notification here
                                 //you can send this to an Azure queue to be processed later
                                //for this sample, we just log to the trace

                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("Resource: {0}", notification.Resource));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("SubscriptionId: {0}", notification.SubscriptionId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("TenantId: {0}", notification.TenantId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("SiteUrl: {0}", notification.SiteUrl));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("WebId: {0}", notification.WebId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("ExpirationDateTime: {0}", notification.ExpirationDateTime));

                            });

                            httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
                        }
                    }
                }
            }
            else
            {
                httpResponse = new HttpResponseMessage(HttpStatusCode.Forbidden);
            }
        }

        return httpResponse;
    }
    ```

* <span data-ttu-id="8c8f6-182">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-182">Save the file.</span></span>

## <a name="step-3-debug-the-webhook-receiver"></a><span data-ttu-id="8c8f6-183">Schritt 3: Debuggen des Webhook-Empfängers</span><span class="sxs-lookup"><span data-stu-id="8c8f6-183">Step 3: Debug the webhook receiver</span></span>

* <span data-ttu-id="8c8f6-184">Drücken Sie **F5**, um den Webhook-Empfänger zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-184">Choose **F5** to debug the webhook receiver.</span></span>
* <span data-ttu-id="8c8f6-185">Kopieren Sie die Portnummer aus der Adressleiste, sobald sich der Browser öffnet.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-185">When you have the browser open, copy the port number from the address bar.</span></span> <span data-ttu-id="8c8f6-186">Beispiel: **http://localhost:<_Portnummer_>**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-186">For example: **http://localhost:<_port-number_>**.</span></span>

## <a name="step-4-run-ngrok-proxy"></a><span data-ttu-id="8c8f6-187">Schritt 4: Ausführen des ngrok-Proxys</span><span class="sxs-lookup"><span data-stu-id="8c8f6-187">Step 4: Run ngrok proxy</span></span>

* <span data-ttu-id="8c8f6-188">Öffnen Sie ein Konsolenterminal.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-188">Open a console terminal.</span></span>
* <span data-ttu-id="8c8f6-189">Wechseln Sie zum extrahierten ngrok-Ordner.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-189">Go to the extracted ngrok folder.</span></span>
* <span data-ttu-id="8c8f6-190">Geben Sie Folgendes mit der Portnummern-URL aus dem vorherigen Schritt ein, um ngrok zu starten:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-190">Enter the following with the port number URL from the previous step to start ngrok:</span></span>

    ```
    ./ngrok http port-number --host-header=localhost:port-number
    ```

* <span data-ttu-id="8c8f6-191">ngrok sollte jetzt ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-191">You should see ngrok running.</span></span>
* <span data-ttu-id="8c8f6-192">Kopieren Sie die HTTPS-Adresse unter **Forwarding**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-192">Copy the **Forwarding** HTTPS address.</span></span> <span data-ttu-id="8c8f6-193">Diese Adresse wird der Dienstproxy, an den SharePoint Anforderungen sendet.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-193">You will use this address as the service proxy for SharePoint to send requests.</span></span> 

## <a name="step-5-add-webhook-subscription-using-postman"></a><span data-ttu-id="8c8f6-194">Schritt 5: Hinzufügen eines Webhook-Abonnements mit Postman</span><span class="sxs-lookup"><span data-stu-id="8c8f6-194">Step 5: Add webhook subscription using Postman</span></span>

### <a name="get-new-access-token"></a><span data-ttu-id="8c8f6-195">Abrufen eines neuen Zugriffstokens</span><span class="sxs-lookup"><span data-stu-id="8c8f6-195">Get new access token</span></span>

<span data-ttu-id="8c8f6-p111">Postman macht die Arbeit mit APIs sehr einfach. Im ersten Schritt konfigurieren Sie Postman für die Azure AD-Authentifizierung, damit Sie API-Anforderungen an SharePoint senden können. Dazu verwenden Sie die Azure AD-App, die Sie in Schritt 1 registriert haben.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p111">Postman makes it really simple to work with APIs. The first step is to configure Postman to authenticate with Azure AD so you can send API requests to SharePoint. You will use the Azure AD app that you registered in Step 1.</span></span>

* <span data-ttu-id="8c8f6-199">Öffnen Sie Postman.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-199">Open Postman.</span></span>
* <span data-ttu-id="8c8f6-200">Sie sehen die **Sidebar** und den **Request Editor**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-200">You will be presented with a **Sidebar** and **Request Editor**.</span></span>
* <span data-ttu-id="8c8f6-201">Gehen Sie zur Registerkarte **Authorization** im **Request Editor**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-201">Choose the **Authorization** tab in the **Request Editor**.</span></span>
* <span data-ttu-id="8c8f6-202">Wählen Sie **OAuth 2.0** aus der Dropdownliste **Type** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-202">Choose **OAuth 2.0** in the **Type** dropdown list.</span></span>
* <span data-ttu-id="8c8f6-203">Klicken Sie auf die Schaltfläche **Get New Access Token**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-203">Choose the **Get New Access Token** button.</span></span>
* <span data-ttu-id="8c8f6-204">Geben Sie im Dialogfenster Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-204">In the dialog window, enter the following:</span></span> 
    * <span data-ttu-id="8c8f6-205">Auth URL:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-205">Auth URL:</span></span> 
       * <span data-ttu-id="8c8f6-206">**https://login.microsoftonline.com/common/oauth2/authorize?resource=https%3A%2F%2F<_your-sharepoint-tenant-url-without-https_>**</span><span class="sxs-lookup"><span data-stu-id="8c8f6-206">**https://login.microsoftonline.com/common/oauth2/authorize?resource=https%3A%2F%2F<_your-sharepoint-tenant-url-without-https_>**</span></span>
       * <span data-ttu-id="8c8f6-207">Tragen Sie für _your-sharepoint-site-collection-url-without-https_ Ihre Websitesammlung ohne das Präfix **https** ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-207">Replace _your-sharepoint-tenant-url-without-https_ with your tenant url without the **https** prefix.</span></span>
    * <span data-ttu-id="8c8f6-208">Zugriffstoken-URL:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-208">Access Token URL:</span></span>
        * <span data-ttu-id="8c8f6-209">**https://login.microsoftonline.com/common/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="8c8f6-209">**https://login.microsoftonline.com/common/oauth2/token**</span></span>
    * <span data-ttu-id="8c8f6-210">Client Id:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-210">Client Id:</span></span> 
        * <span data-ttu-id="8c8f6-211">Client-ID der App, die Sie zuvor in Schritt 1 registriert haben</span><span class="sxs-lookup"><span data-stu-id="8c8f6-211">Client Id of the app you registered previously in Step one.</span></span>
    * <span data-ttu-id="8c8f6-212">Client Secret:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-212">Client Secret:</span></span> 
        * <span data-ttu-id="8c8f6-213">Geheimer Clientschlüssel der App, die Sie zuvor in Schritt 1 registriert haben</span><span class="sxs-lookup"><span data-stu-id="8c8f6-213">Client Secret of the app you registered previously in Step one.</span></span>
    * <span data-ttu-id="8c8f6-214">Token name:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-214">Token name:</span></span>
        * <span data-ttu-id="8c8f6-215">sp_webhooks_token</span><span class="sxs-lookup"><span data-stu-id="8c8f6-215">sp_webhooks_token</span></span>
    * <span data-ttu-id="8c8f6-216">Grant type:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-216">Grant type:</span></span>
        * <span data-ttu-id="8c8f6-217">Authorization Code</span><span class="sxs-lookup"><span data-stu-id="8c8f6-217">Authorization Code</span></span>
* <span data-ttu-id="8c8f6-218">Wählen Sie **Request Token** aus, um sich anzumelden, zuzustimmen und das Token für die Sitzung abzurufen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-218">Choose the **Request Token** to sign in, consent, and get the token for the session.</span></span>
* <span data-ttu-id="8c8f6-219">Sobald das Token abgerufen wurde, sollte die Variable **access\_token** auf der Registerkarte **Authorization** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-219">When the token is successfully retrieved, you should see **access\_token** variable added to the **Authorization** tab</span></span>
* <span data-ttu-id="8c8f6-220">Wählen Sie die Option **Add token to header** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-220">Select the option to **Add token to header**.</span></span>
* <span data-ttu-id="8c8f6-221">Doppelklicken Sie auf die Variable **access\_token**, um das Token zum Header der Anforderung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-221">Double-click the **access\_token** variable to add the token to the header for the request.</span></span>

![Abrufen eines neuen Zugriffstokens von Postman](../../images/postman-get-new-access-token.png)

### <a name="get-documents-list-id"></a><span data-ttu-id="8c8f6-223">Abrufen der ID der Liste „Dokumente“</span><span class="sxs-lookup"><span data-stu-id="8c8f6-223">Get Documents list Id</span></span>

<span data-ttu-id="8c8f6-224">Sie müssen die Webhooks für die Standarddokumentbibliothek verwalten, die in Ihrer Standardwebsitesammlung unter dem Namen **Dokumente** bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-224">You need to manage webhooks for the default document library, which is provisioned in your default site collection under the name **Documents**.</span></span> <span data-ttu-id="8c8f6-225">Senden Sie zum Abrufen der ID dieser Liste eine **GET**-Anforderung:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-225">Get the Id of this list by issuing a **GET** request:</span></span>

* <span data-ttu-id="8c8f6-226">Geben Sie die folgende Anforderungs-URL ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-226">Enter the following request URL:</span></span>

    ```
    https://site-collection/_api/web/lists/getbytitle('Documents')?$select=Title,Id
    ```

> <span data-ttu-id="8c8f6-227">Tragen Sie für _site-collection_ Ihre Websitesammlung ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-227">Replace _site-collection_ with your site collection.</span></span>
    
<span data-ttu-id="8c8f6-228">Postman führt nun Ihre Anforderung aus. Ist die Ausführung erfolgreich, wird das Ergebnis angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-228">Postman will execute your request and if successful, you should see the result.</span></span>

<span data-ttu-id="8c8f6-229">Kopieren Sie aus den Ergebnissen den Wert für **Id**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-229">Copy the **Id** from the results.</span></span> <span data-ttu-id="8c8f6-230">Den Wert **Id** verwenden Sie später zur Erstellung von Webhook-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-230">Later you will use the **Id** to make webhook requests.</span></span>   

### <a name="add-webhook-subscription"></a><span data-ttu-id="8c8f6-231">Hinzufügen eines Webhook-Abonnements</span><span class="sxs-lookup"><span data-stu-id="8c8f6-231">Add webhook subscription</span></span>

<span data-ttu-id="8c8f6-p114">Da Sie nun alle erforderlichen Informationen haben, können Sie die Abfrage und die Anforderung zum Hinzufügen eines Webhook-Abonnements erstellen. Führen Sie im Request Editor die folgenden Schritte durch:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p114">Now that you have the required information, construct the query and the request to add a webhook subscription. Use the request editor for the following steps:</span></span>

* <span data-ttu-id="8c8f6-234">Ändern Sie die Anforderung in **POST** statt **GET**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-234">Change the request to **POST** from **GET**.</span></span>
* <span data-ttu-id="8c8f6-235">Geben Sie die folgende Anforderungs-URL ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-235">Enter the following as the request URL:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions
    ```

> <span data-ttu-id="8c8f6-236">Tragen Sie für _site-collection_ Ihre Websitesammlung ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-236">Replace _site-collection_ with your site collection.</span></span>

* <span data-ttu-id="8c8f6-237">Wechseln Sie zur Registerkarte **Headers**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-237">Go to the **Headers** tab.</span></span>
* <span data-ttu-id="8c8f6-238">Vergewissern Sie sich, dass der **Authorization**-Header übernommen wurde.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-238">Make sure you still have the **Authorization** header.</span></span> <span data-ttu-id="8c8f6-239">Ist das nicht der Fall, müssen Sie ein neues Zugriffstoken anfordern.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-239">If not, you will need to request a new access token.</span></span>
* <span data-ttu-id="8c8f6-240">Fügen Sie die folgenden Paare des Typs **key -> value** für den Header hinzu:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-240">Add the following header **key -> value** pairs:</span></span>
    * <span data-ttu-id="8c8f6-241">Accept -> application/json;odata=nometadata</span><span class="sxs-lookup"><span data-stu-id="8c8f6-241">Accept -> application/json;odata=nometadata</span></span>
    * <span data-ttu-id="8c8f6-242">Content-Type -> application/json</span><span class="sxs-lookup"><span data-stu-id="8c8f6-242">Content-Type -> application/json</span></span>

* <span data-ttu-id="8c8f6-243">Wechseln Sie zur Registerkarte **Body**, und wählen Sie als Format **raw** aus.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-243">Go to the **Body** tab and select **raw** format.</span></span>
* <span data-ttu-id="8c8f6-244">Fügen Sie den folgenden JSON-Text als Body ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-244">Paste the following JSON as the body:</span></span>

    ```json
    {
      "resource": "https://site-collection/_api/web/lists('list-id')",
      "notificationUrl": "https://ngrok-forwarding-address/api/spwebhook/handlerequest",
      "expirationDateTime": "2016-10-27T16:17:57+00:00",
      "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449"
    }
    ```

    ![Hinzufügen eines Webhook-Bodys in Postman](../../images/postman-add-webhook-body.png)

> <span data-ttu-id="8c8f6-246">Stellen Sie sicher, dass der Wert **expirationDateTime** höchstens 6 Monate in der Zukunft liegt, gerechnet vom aktuellen Datum.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-246">Make sure the **expirationDateTime** is at most 6 months from today.</span></span> 

* <span data-ttu-id="8c8f6-247">Stellen Sie sicher, dass Sie den Webhook-Empfänger wie in Schritt 4 beschrieben debuggen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-247">Make sure you are debugging the webhook receiver as in Step 4.</span></span>
* <span data-ttu-id="8c8f6-248">Klicken Sie auf **Send**, um die Anforderung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-248">Choose **Send** to execute the request.</span></span>
* <span data-ttu-id="8c8f6-p116">Kann die Anforderung ausgeführt werden, sollten Sie eine Antwort von SharePoint mit den Abonnementdetails sehen. Hier ein Beispiel einer Antwort für ein neu erstelltes Abonnement:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p116">If the request is successful, you should see the response from SharePoint that provides the subscription details. The following example shows a response for a newly created subscription:</span></span>

    ```json
    {
      "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449",
      "expirationDateTime": "2016-10-27T16:17:57Z",
      "id": "32b95d9-4d20-4a17-bfa3-2957cb38ead8",
      "notificationUrl": "https://85557d4b.ngrok.io/api/spwebhook/handlerequest",
      "resource": "c34420f9-2ad7-4e54-94c9-b67798d2299b"
    }
    ```

* <span data-ttu-id="8c8f6-251">Kopieren Sie den Wert **id** des Abonnements. Sie benötigen ihn für die nächsten Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-251">Copy the subscription **id**. You will need it for the next set of requests.</span></span>
* <span data-ttu-id="8c8f6-252">Gehen Sie zum Webhook-Empfänger-Projekt in Visual Studio, und schauen Sie ins Fenster **Ausgabe**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-252">Go to the webhook receiver project in Visual Studio and examine the **Output** window.</span></span> <span data-ttu-id="8c8f6-253">Hier sollten die Ablaufprotokolle und andere Nachrichten angezeigt werden. Die Ablaufprotokolle sollten in etwa wie diese Ablaufverfolgung aussehen:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-253">You should see the trace logs that look similar to the following trace, along with other messages:</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Received client state: A0A354EC-97D4-4D83-9DDB-144077ADB449'
    iisexpress.exe Information: 0 : Message='Received validation token: daf2803c-43cf-44c7-8dff-7066eaa40f13'
    ```

<span data-ttu-id="8c8f6-p118">Die Ablaufverfolgung meldet, dass der anfänglich empfangene Webhook eine Prüfungsanforderung empfangen hat. Sie sehen im Code, dass das Prüfungstoken sofort zurückgegeben wird, so dass SharePoint die Anforderungen überprüfen kann:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p118">The trace indicates that the webhook received initially received a validation request. If you look at the code, you'll see that it returns the validation token immediately so that SharePoint can validate the request:</span></span>

```cs
if (queryStringParams.AllKeys.Contains("validationtoken"))
{
    httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
    validationToken = queryStringParams.GetValues("validationtoken")[0].ToString();
    httpResponse.Content = new StringContent(validationToken);

    traceWriter.Trace(Request, "SPWebhooks", 
        TraceLevel.Info, 
        string.Format("Received validation token: {0}", validationToken));                        
    return httpResponse;
}
```

## <a name="step-6-get-subscription-details"></a><span data-ttu-id="8c8f6-256">Schritt 6: Abrufen der Abonnementdetails</span><span class="sxs-lookup"><span data-stu-id="8c8f6-256">Step 6: Get subscription details</span></span>

<span data-ttu-id="8c8f6-257">Jetzt führen Sie Abfragen in Postman aus, um die Abonnementdetails abzurufen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-257">Now you'll run queries in Postman to get the subscription details.</span></span>

* <span data-ttu-id="8c8f6-258">Öffnen Sie den Postman-Client.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-258">Open the Postman client.</span></span>
* <span data-ttu-id="8c8f6-259">Ändern Sie die Anforderung in **GET** statt **POST**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-259">Change the request to **GET** from **POST**.</span></span>
* <span data-ttu-id="8c8f6-260">Geben Sie Folgendes als Anforderung ein:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-260">Enter the following as the request:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions
    ```

> <span data-ttu-id="8c8f6-261">Tragen Sie für _site-collection_ Ihre Websitesammlung ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-261">Replace _site-collection_ with your site collection.</span></span>

* <span data-ttu-id="8c8f6-262">Klicken Sie auf **Send**, um die Anforderung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-262">Choose **Send** to execute the request.</span></span>

<span data-ttu-id="8c8f6-p119">Kann die Anforderung ausgeführt werden, gibt SharePoint die Abonnements für diese Listenressource zurück. Da Sie gerade eins hinzugefügt haben, sollte mindestens ein Abonnement zurückgegeben werden. Hier ein Beispiel für eine Antwort mit einem Abonnement:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p119">If successful, you should see SharePoint return the subscriptions for this list resource. Because we just added one, you should at least see one subscription returned. The following example shows a response with one subscription:</span></span>

    ```json
    {
      "value": [
        {
          "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449",
          "expirationDateTime": "2016-10-27T16:17:57Z",
          "id": "32b95add-4d20-4a17-bfa3-2957cb38ead8",
          "notificationUrl": "https://85557d4b.ngrok.io/api/spwebhook/handlerequest",
          "resource": "c34420f9-2a67-4e54-94c9-b67798229f9b"
        }
      ]
    }
    ```

<span data-ttu-id="8c8f6-266">Mit der folgenden Abfrage können Sie die Details dieses Abonnements abrufen:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-266">You can run the following query to get details of the specific subscription:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions('subscription-id')
    ```

> <span data-ttu-id="8c8f6-267">Tragen Sie für „subscription-id“ Ihre Abonnement-ID ein.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-267">Replace subscription-id with your subscription id</span></span> 

## <a name="step-7-test-webhook-notification"></a><span data-ttu-id="8c8f6-268">Schritt 7: Testen der Webhook-Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="8c8f6-268">Step 7: Test webhook notification</span></span>

<span data-ttu-id="8c8f6-269">Nun fügen Sie eine Datei zur Bibliothek „Dokumente“ hinzu und testen, ob Sie im Webhook-Empfänger eine Benachrichtigung von SharePoint erhalten.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-269">Now add a file to the Documents library and test if you get a notification from SharePoint in the webhook receiver.</span></span>

* <span data-ttu-id="8c8f6-270">Wechseln Sie zu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-270">Go to Visual Studio.</span></span>
* <span data-ttu-id="8c8f6-271">Platzieren Sie im **SPWebhookController** einen Breakpoint in der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-271">In the **SPWebhookController** place a breakpoint on the following line of code:</span></span>

    ```cs
    var requestContent = Request.Content.ReadAsStringAsync().Result;
    ```

* <span data-ttu-id="8c8f6-272">Gehen Sie zur Bibliothek **Dokumente**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-272">Go to the **Documents** library.</span></span> <span data-ttu-id="8c8f6-273">In Ihrer Standardwebsitesammlung ist dies die Bibliothek **Freigegebene Dokumente**.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-273">It will be named **Shared Documents** library in your default site collection.</span></span>
* <span data-ttu-id="8c8f6-274">Fügen Sie eine neue Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-274">Add a new file.</span></span>
* <span data-ttu-id="8c8f6-275">Gehen Sie zu Visual Studio, und warten Sie, bis der Breakpoint erreicht wird.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-275">Go to Visual Studio and wait for the breakpoint to be hit.</span></span>
   * <span data-ttu-id="8c8f6-p121">Die Wartezeit kann zwischen einigen Sekunden und 5 Minuten betragen. In dem Moment, in dem der Breakpoint erreicht ist, hat der Webhook-Empfänger eine Benachrichtigung von SharePoint erhalten.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p121">Wait time may vary from a few seconds up to five minutes. When the breakpoint is hit, the webhook receiver has just received a notification from SharePoint.</span></span>
* <span data-ttu-id="8c8f6-278">Drücken Sie auf **F5**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-278">Choose **F5** to continue.</span></span>
* <span data-ttu-id="8c8f6-279">Die Benachrichtigungsdaten finden Sie im Fenster **Ausgabe** in den folgenden Einträgen, da Sie sie zum Ablaufprotokoll hinzugefügt haben:</span><span class="sxs-lookup"><span data-stu-id="8c8f6-279">To see the notification data, look in the **Output** window for the following entries, since you added the notification data into the trace log:</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Resource: c34420f9-2a67-4e54-94c9-b6770892299b'
    iisexpress.exe Information: 0 : Message='SubscriptionId: 32b95ad9-4d20-4a17-bfa3-2957cb38ead8'
    iisexpress.exe Information: 0 : Message='TenantId: 7a17cb7d-6898-423f-8839-45f363076f06'
    iisexpress.exe Information: 0 : Message='SiteUrl: /'
    iisexpress.exe Information: 0 : Message='WebId: 62b80e0b-f889-4974-a519-cc138413be40'
    iisexpress.exe Information: 0 : Message='ExpirationDateTime: 2016-10-27T16:17:57.0000000Z'
    ```

<span data-ttu-id="8c8f6-p122">Dieses Projekt schreibt die Informationen nur ins Ablaufprotokoll. Im Empfänger werden die Informationen jedoch an eine Tabelle oder eine Warteschlange gesendet, die die empfangenen Daten verarbeiten und die von SharePoint gesendeten Informationen auswerten kann.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-p122">This project just writes the information to the trace log. However, in your receiver, you will send this information into a table or a queue that can process the received data to get information from SharePoint.</span></span> 

<span data-ttu-id="8c8f6-282">Mit diesen Daten können Sie die URL erstellen und über die [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges)-API die neuesten Änderungen abrufen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-282">With this data, you can construct the URL and use the [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) API to get the latest changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c8f6-283">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="8c8f6-283">Next steps</span></span>

<span data-ttu-id="8c8f6-284">In diesem Artikel haben Sie mithilfe des Postman-Clients und einer einfachen Web-API Webhook-Benachrichtigungen von SharePoint abonniert und empfangen.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-284">In this article, you used Postman client and a simple web API to subscribe and receive webhook notifications from SharePoint.</span></span>

<span data-ttu-id="8c8f6-285">Sehen Sie sich als nächstes die [Beispielreferenzimplementierung für SharePoint-Webhooks](./webhooks-reference-implementation.md) an. Sie gibt ein End-to-End-Beispiel, das Azure-Speicherwarteschlangen verwendet, um die Informationen zu verarbeiten, Änderungen von SharePoint abzurufen und diese Änderungen an eine SharePoint-Liste zurückzusenden.</span><span class="sxs-lookup"><span data-stu-id="8c8f6-285">Next, take a look at [SharePoint webhooks sample reference implementation](./webhooks-reference-implementation.md), which shows an end-to-end sample that uses Azure Storage Queues to process the information, get changes from SharePoint, and push those changes back into a SharePoint list.</span></span>
