---
title: Erstellen eines neuen Abonnements
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 374200568aa1151e58b9ae76fc48fb2465921af7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-new-subscription"></a><span data-ttu-id="b5278-102">Erstellen eines neuen Abonnements</span><span class="sxs-lookup"><span data-stu-id="b5278-102">Create a new subscription</span></span> 

<span data-ttu-id="b5278-103">Erstellt ein neues Webhook-Abonnement in einer SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="b5278-103">Creates a new webhook subscription on a SharePoint list.</span></span> 

## <a name="permissions"></a><span data-ttu-id="b5278-104">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="b5278-104">Permissions</span></span>

<span data-ttu-id="b5278-105">Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, in der das Abonnement erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="b5278-105">The application must have at least edit permissions to the SharePoint list where the subscription will be created.</span></span>

<span data-ttu-id="b5278-106">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="b5278-106">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="b5278-107">Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen:</span><span class="sxs-lookup"><span data-stu-id="b5278-107">You must grant the Azure AD app the permissions specified in the following table:</span></span>

<span data-ttu-id="b5278-108">Anwendung</span><span class="sxs-lookup"><span data-stu-id="b5278-108">Application</span></span> | <span data-ttu-id="b5278-109">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="b5278-109">Permission</span></span> 
------------|------------
<span data-ttu-id="b5278-110">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b5278-110">Office 365 SharePoint Online</span></span>|<span data-ttu-id="b5278-111">Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="b5278-111">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="b5278-112">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="b5278-112">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="b5278-113">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen:</span><span class="sxs-lookup"><span data-stu-id="b5278-113">You must grant the SharePoint add-in the following permission(s) or higher:</span></span>

<span data-ttu-id="b5278-114">Bereich</span><span class="sxs-lookup"><span data-stu-id="b5278-114">Scope</span></span> | <span data-ttu-id="b5278-115">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="b5278-115">Permission Rights</span></span> 
------|------------
<span data-ttu-id="b5278-116">Liste</span><span class="sxs-lookup"><span data-stu-id="b5278-116">List</span></span>|<span data-ttu-id="b5278-117">Verwalten</span><span class="sxs-lookup"><span data-stu-id="b5278-117">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="b5278-118">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="b5278-118">HTTP request</span></span>

```
POST /_api/web/lists('list-id')/subscriptions
```

## <a name="request-body"></a><span data-ttu-id="b5278-119">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="b5278-119">Request body</span></span>

<span data-ttu-id="b5278-120">Schließen Sie die folgenden Eigenschaften in die Anforderung ein.</span><span class="sxs-lookup"><span data-stu-id="b5278-120">Include the following properties in the request body.</span></span>

<span data-ttu-id="b5278-121">Name</span><span class="sxs-lookup"><span data-stu-id="b5278-121">Name</span></span> | <span data-ttu-id="b5278-122">Typ</span><span class="sxs-lookup"><span data-stu-id="b5278-122">Type</span></span> | <span data-ttu-id="b5278-123">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b5278-123">Description</span></span> 
-----|------|------------
<span data-ttu-id="b5278-124">resource</span><span class="sxs-lookup"><span data-stu-id="b5278-124">resource</span></span>|<span data-ttu-id="b5278-125">string</span><span class="sxs-lookup"><span data-stu-id="b5278-125">string</span></span>|<span data-ttu-id="b5278-126">Die URL der Liste, aus der Benachrichtigungen empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="b5278-126">The URL of the list to receive notifications from.</span></span>
<span data-ttu-id="b5278-127">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="b5278-127">notificationUrl</span></span>|<span data-ttu-id="b5278-128">string</span><span class="sxs-lookup"><span data-stu-id="b5278-128">string</span></span>|<span data-ttu-id="b5278-129">Die Dienst-URL, an den Benachrichtigungen gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="b5278-129">The service URL to send notifications to.</span></span>
<span data-ttu-id="b5278-130">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="b5278-130">expirationDateTime</span></span>|<span data-ttu-id="b5278-131">date</span><span class="sxs-lookup"><span data-stu-id="b5278-131">date</span></span>|<span data-ttu-id="b5278-132">Das Datum, an dem die Benachrichtigung abläuft und gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="b5278-132">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="b5278-133">client-clientState</span><span class="sxs-lookup"><span data-stu-id="b5278-133">client-clientState</span></span>|<span data-ttu-id="b5278-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="b5278-134">string</span></span>|<span data-ttu-id="b5278-p101">Optional. Verschlüsselte Zeichenfolge, die bei allen Benachrichtigungen zurück an den Client übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen oder zum Kategorisieren unterschiedlicher Abonnements verwenden.</span><span class="sxs-lookup"><span data-stu-id="b5278-p101">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


### <a name="example"></a><span data-ttu-id="b5278-138">Beispiel</span><span class="sxs-lookup"><span data-stu-id="b5278-138">Example</span></span>

```http
POST /_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
Accept: application/json
Content-Type: application/json

{
  "resource": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')",
  "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
  "expirationDateTime": "2016-04-27T16:17:57+00:00"
}
```

## <a name="response"></a><span data-ttu-id="b5278-139">Antwort</span><span class="sxs-lookup"><span data-stu-id="b5278-139">Response</span></span>

<span data-ttu-id="b5278-140">Wenn das Abonnement hinzugefügt wird, wird eine `201 Created`-Antwort zurückgegeben, die das neu erstellte Abonnementobjekt enthält.</span><span class="sxs-lookup"><span data-stu-id="b5278-140">If the subscription is added, then a `201 Created` response is returned that includes the newly created subscription object.</span></span>

### <a name="example"></a><span data-ttu-id="b5278-141">Beispiel</span><span class="sxs-lookup"><span data-stu-id="b5278-141">Example</span></span>

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
    "expirationDateTime": "2016-04-27T16:17:57Z",    
    "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
    "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

## <a name="url-validation"></a><span data-ttu-id="b5278-142">URL-Überprüfung</span><span class="sxs-lookup"><span data-stu-id="b5278-142">URL validation</span></span>

<span data-ttu-id="b5278-p102">Bevor ein neues Abonnement erstellt wird, sendet SharePoint eine Anforderung mit einem Überprüfungstoken im Textkörper der Anfrage an die bereitgestellt Dienst-URL. Ihr Dienst muss auf diese Anforderung durch Zurückgeben des Überprüfungstokens antworten.</span><span class="sxs-lookup"><span data-stu-id="b5278-p102">Before a new subscription is created, SharePoint will send a request with a validation token in the body of the request to the service URL provided. Your service must respond to this request by returning the validation token.</span></span>

<span data-ttu-id="b5278-145">Wenn der Dienst die Anforderung auf diese Weise nicht überprüfen kann, wird das Abonnement nicht erstellt.</span><span class="sxs-lookup"><span data-stu-id="b5278-145">If your service fails to validate the request in this way, the subscription will fail to be created.</span></span> <span data-ttu-id="b5278-146">Weitere Informationen finden Sie unter [Übersicht über SharePoint-Webhooks](../overview-sharepoint-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b5278-146">See [Overview of SharePoint webhooks](../overview-sharepoint-webhooks.md) for more information.</span></span>
