---
title: Aktualisieren eines Abonnements
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6638ad3f3919f9e14497adb7dacc1c1a09c139f6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-a-subscription"></a><span data-ttu-id="2b109-102">Aktualisieren eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="2b109-102">Update a subscription</span></span>

<span data-ttu-id="2b109-103">Aktualisiert ein Webhook-Abonnement in einer SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="2b109-103">Updates a webhook subscription on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="2b109-104">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="2b109-104">Permissions</span></span>

<span data-ttu-id="2b109-105">Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, in der das Abonnement aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="2b109-105">The application must have at least edit permissions to the SharePoint list where the subscription will be updated.</span></span>  

<span data-ttu-id="2b109-106">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="2b109-106">**If your application is an Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="2b109-p101">Sie müssen der Azure AD-Anwendung die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="2b109-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be updated by the Azure AD application that created it.</span></span>

<span data-ttu-id="2b109-109">Anwendung</span><span class="sxs-lookup"><span data-stu-id="2b109-109">Application</span></span> | <span data-ttu-id="2b109-110">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="2b109-110">Permission</span></span> 
------------|------------
<span data-ttu-id="2b109-111">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2b109-111">Office 365 SharePoint Online</span></span>|<span data-ttu-id="2b109-112">Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="2b109-112">Read and write items and lists in all site collections.</span></span> 

<span data-ttu-id="2b109-113">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="2b109-113">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="2b109-p102">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="2b109-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be updated by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="2b109-116">Umfang</span><span class="sxs-lookup"><span data-stu-id="2b109-116">Scope</span></span> | <span data-ttu-id="2b109-117">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="2b109-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="2b109-118">Liste</span><span class="sxs-lookup"><span data-stu-id="2b109-118">List</span></span>|<span data-ttu-id="2b109-119">Verwalten</span><span class="sxs-lookup"><span data-stu-id="2b109-119">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="2b109-120">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="2b109-120">HTTP request</span></span>

```
PATCH _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="2b109-121">Beispiel</span><span class="sxs-lookup"><span data-stu-id="2b109-121">Example</span></span>

```http
PATCH _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
Content-Type: application/json

{
  "notificationUrl": "https://contoso.azurewebsites.net/api/v2/webhook-receiver",
  "expirationDateTime": "2016-01-03T11:23:00.000Z"
}
```

## <a name="request-body"></a><span data-ttu-id="2b109-122">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="2b109-122">Request body</span></span>

<span data-ttu-id="2b109-123">Schließen Sie die folgenden Eigenschaften in die Anforderung ein.</span><span class="sxs-lookup"><span data-stu-id="2b109-123">Include the following properties in the request body.</span></span>

<span data-ttu-id="2b109-124">Name</span><span class="sxs-lookup"><span data-stu-id="2b109-124">Name</span></span> | <span data-ttu-id="2b109-125">Typ</span><span class="sxs-lookup"><span data-stu-id="2b109-125">Type</span></span> | <span data-ttu-id="2b109-126">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2b109-126">Description</span></span> 
-----|------|------------
<span data-ttu-id="2b109-127">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="2b109-127">notificationUrl</span></span>|<span data-ttu-id="2b109-128">string</span><span class="sxs-lookup"><span data-stu-id="2b109-128">string</span></span>|<span data-ttu-id="2b109-129">Die Dienst-URL, an den Benachrichtigungen gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="2b109-129">The service URL to send notifications to.</span></span>
<span data-ttu-id="2b109-130">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="2b109-130">expirationDateTime</span></span>|<span data-ttu-id="2b109-131">date</span><span class="sxs-lookup"><span data-stu-id="2b109-131">date</span></span>|<span data-ttu-id="2b109-132">Das Datum, an dem die Benachrichtigung abläuft und gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="2b109-132">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="2b109-133">client-clientState</span><span class="sxs-lookup"><span data-stu-id="2b109-133">client-clientState</span></span>|<span data-ttu-id="2b109-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="2b109-134">string</span></span>|<span data-ttu-id="2b109-p103">Optional. Verschlüsselte Zeichenfolge, die bei allen Benachrichtigungen zurück an den Client übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen oder zum Kategorisieren unterschiedlicher Abonnements verwenden.</span><span class="sxs-lookup"><span data-stu-id="2b109-p103">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


## <a name="response"></a><span data-ttu-id="2b109-138">Antwort</span><span class="sxs-lookup"><span data-stu-id="2b109-138">Response</span></span>

<span data-ttu-id="2b109-139">Wenn das Abonnement gefunden und erfolgreich aktualisiert wird, wird eine `204 No Content`-Antwort zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2b109-139">If the subscription is found and successfully updated, then a `204 No Content` response is returned:</span></span>

### <a name="example"></a><span data-ttu-id="2b109-140">Beispiel</span><span class="sxs-lookup"><span data-stu-id="2b109-140">Example</span></span>

```http
HTTP/1.1 204 No Content
```
