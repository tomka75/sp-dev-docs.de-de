---
title: Abrufen von Abonnements
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6dea5da88388c0787c9295141cee2fed50a5fa65
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-subscriptions"></a><span data-ttu-id="f3f51-102">Abrufen von Abonnements</span><span class="sxs-lookup"><span data-stu-id="f3f51-102">Get subscriptions</span></span>

<span data-ttu-id="f3f51-103">Ruft ein oder mehrere Webhook-Abonnements in einer SharePoint-Liste ab.</span><span class="sxs-lookup"><span data-stu-id="f3f51-103">Gets one or more webhook subscriptions on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="f3f51-104">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="f3f51-104">Permissions</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="f3f51-105">Abrufen eines einzelnen Abonnements</span><span class="sxs-lookup"><span data-stu-id="f3f51-105">Get a single subscription</span></span>

<span data-ttu-id="f3f51-106">Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, aus der das Abonnement abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="f3f51-106">The application must have at least edit permissions to the SharePoint list where the subscription will be retreived.</span></span>

<span data-ttu-id="f3f51-107">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="f3f51-107">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="f3f51-p101">Sie müssen der Azure AD-Anwendung die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="f3f51-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be retrieved by the Azure AD application that created it.</span></span> 

<span data-ttu-id="f3f51-110">Anwendung</span><span class="sxs-lookup"><span data-stu-id="f3f51-110">Application</span></span> | <span data-ttu-id="f3f51-111">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="f3f51-111">Permission</span></span> 
------------|------------
<span data-ttu-id="f3f51-112">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f3f51-112">Office 365 SharePoint Online</span></span>|<span data-ttu-id="f3f51-113">Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="f3f51-113">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="f3f51-114">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="f3f51-114">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="f3f51-p102">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="f3f51-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be retrieved by the SharePoint add-in that created it.</span></span> 

<span data-ttu-id="f3f51-117">Umfang</span><span class="sxs-lookup"><span data-stu-id="f3f51-117">Scope</span></span> | <span data-ttu-id="f3f51-118">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="f3f51-118">Permission Rights</span></span> 
------|------------
<span data-ttu-id="f3f51-119">Liste</span><span class="sxs-lookup"><span data-stu-id="f3f51-119">List</span></span>|<span data-ttu-id="f3f51-120">Verwalten</span><span class="sxs-lookup"><span data-stu-id="f3f51-120">Manage</span></span>

### <a name="get-all-subscriptions"></a><span data-ttu-id="f3f51-121">Abrufen aller Abonnements</span><span class="sxs-lookup"><span data-stu-id="f3f51-121">Get all subscriptions</span></span>

<span data-ttu-id="f3f51-122">Die Anwendung muss mindestens Berechtigungen zum Verwalten von Listen für die SharePoint-Liste haben, aus der das Abonnement abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="f3f51-122">The application must have manage list permissions to the SharePoint list where the subscription will be retrieved.</span></span>

<span data-ttu-id="f3f51-123">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="f3f51-123">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="f3f51-124">Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="f3f51-124">You must grant the Azure AD app the permissions specified in the following table.</span></span> 

<span data-ttu-id="f3f51-125">Anwendung</span><span class="sxs-lookup"><span data-stu-id="f3f51-125">Application</span></span> | <span data-ttu-id="f3f51-126">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="f3f51-126">Permission</span></span> 
------------|------------
<span data-ttu-id="f3f51-127">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f3f51-127">Office 365 SharePoint Online</span></span>|<span data-ttu-id="f3f51-128">Sie benötigen Vollzugriff auf alle Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="f3f51-128">Have full control of all site collections.</span></span>

<span data-ttu-id="f3f51-129">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="f3f51-129">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="f3f51-130">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="f3f51-130">You must grant the SharePoint add-in the following permission(s) or higher.</span></span> 

<span data-ttu-id="f3f51-131">Bereich</span><span class="sxs-lookup"><span data-stu-id="f3f51-131">Scope</span></span> | <span data-ttu-id="f3f51-132">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="f3f51-132">Permission Rights</span></span> 
------|------------
<span data-ttu-id="f3f51-133">Liste</span><span class="sxs-lookup"><span data-stu-id="f3f51-133">List</span></span>|<span data-ttu-id="f3f51-134">Vollzugriff</span><span class="sxs-lookup"><span data-stu-id="f3f51-134">Full control</span></span>

## <a name="http-request"></a><span data-ttu-id="f3f51-135">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="f3f51-135">HTTP request</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="f3f51-136">Abrufen eines einzelnen Abonnements</span><span class="sxs-lookup"><span data-stu-id="f3f51-136">Get a single subscription</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="f3f51-137">Listen-Webhook</span><span class="sxs-lookup"><span data-stu-id="f3f51-137">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a><span data-ttu-id="f3f51-138">Beispiel</span><span class="sxs-lookup"><span data-stu-id="f3f51-138">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a><span data-ttu-id="f3f51-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="f3f51-139">Request body</span></span>

<span data-ttu-id="f3f51-140">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="f3f51-140">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="f3f51-141">Antwort</span><span class="sxs-lookup"><span data-stu-id="f3f51-141">Response</span></span>

<span data-ttu-id="f3f51-142">Dies gibt das Abonnement für die Anzeige durch die aufrufende Anwendung zurück.</span><span class="sxs-lookup"><span data-stu-id="f3f51-142">This returns the subscription viewable by the calling application.</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://contoso.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions/@Element",
  "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
  "odata.id": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "odata.editLink": "web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "expirationDateTime": "2016-04-30T16:17:57Z",
  "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
  "notificationUrl": "https://contoso.azurewebistes.net/api/webhook/handlerequest",
  "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

### <a name="get-all-subscriptions"></a><span data-ttu-id="f3f51-143">Abrufen aller Abonnements</span><span class="sxs-lookup"><span data-stu-id="f3f51-143">Get all subscriptions</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="f3f51-144">Listen-Webhook</span><span class="sxs-lookup"><span data-stu-id="f3f51-144">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a><span data-ttu-id="f3f51-145">Beispiel</span><span class="sxs-lookup"><span data-stu-id="f3f51-145">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a><span data-ttu-id="f3f51-146">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="f3f51-146">Request body</span></span>

<span data-ttu-id="f3f51-147">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="f3f51-147">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="f3f51-148">Antwort</span><span class="sxs-lookup"><span data-stu-id="f3f51-148">Response</span></span>

<span data-ttu-id="f3f51-149">Dies gibt eine Auflistung aller Abonnements in einer SharePoint-Ressource zurück.</span><span class="sxs-lookup"><span data-stu-id="f3f51-149">This returns a collection of all subscriptions on a SharePoint resource.</span></span> 

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://a830edad9050849295j16032914.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions",
  "value": [
    {
      "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
      "odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "odata.editLink": "Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "clientState": "{A0A354EC-97D4-4D83-9DDB-144077ADB449}",
      "expirationDateTime": "2016-04-30T16:17:57Z",
      "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
      "notificationUrl": "https://contoso.azurewebsites.net/api/webhook/handlerequest",
      "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
    }
  ]
}
```
