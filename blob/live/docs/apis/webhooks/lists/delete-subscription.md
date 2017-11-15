---
title: "Löschen eines Abonnements"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 553a20757c0849f5033bc3345c4645f1754945bc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="delete-a-subscription"></a><span data-ttu-id="ecd58-102">Löschen eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="ecd58-102">Delete a subscription</span></span>

<span data-ttu-id="ecd58-p101">Löscht ein Webhook-Abonnement aus einer SharePoint-Liste. Nach dem Löschen des Abonnements werden keine Benachrichtigungen mehr übermittelt.</span><span class="sxs-lookup"><span data-stu-id="ecd58-p101">Deletes a webhook subscription from a SharePoint list. After deleting the subscription notifications will no longer be delivered.</span></span>

## <a name="permissions"></a><span data-ttu-id="ecd58-105">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="ecd58-105">Permissions</span></span>

<span data-ttu-id="ecd58-106">Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, aus der das Abonnement gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="ecd58-106">The application must have at least edit permissions to the SharePoint list where the subscription will be deleted.</span></span>

<span data-ttu-id="ecd58-107">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="ecd58-107">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="ecd58-p102">Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="ecd58-p102">You must grant the Azure AD app the permissions specified in the following table. A subscription can only be deleted by the Azure AD application that created it.</span></span>

<span data-ttu-id="ecd58-110">Anwendung</span><span class="sxs-lookup"><span data-stu-id="ecd58-110">Application</span></span> | <span data-ttu-id="ecd58-111">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="ecd58-111">Permission</span></span> 
------------|------------
<span data-ttu-id="ecd58-112">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="ecd58-112">Office 365 SharePoint Online</span></span>|<span data-ttu-id="ecd58-113">Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="ecd58-113">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="ecd58-114">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="ecd58-114">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="ecd58-p103">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="ecd58-p103">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be deleted by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="ecd58-117">Umfang</span><span class="sxs-lookup"><span data-stu-id="ecd58-117">Scope</span></span> | <span data-ttu-id="ecd58-118">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="ecd58-118">Permission Rights</span></span> 
------|------------
<span data-ttu-id="ecd58-119">Liste</span><span class="sxs-lookup"><span data-stu-id="ecd58-119">List</span></span>|<span data-ttu-id="ecd58-120">Verwalten</span><span class="sxs-lookup"><span data-stu-id="ecd58-120">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="ecd58-121">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="ecd58-121">HTTP request</span></span>

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="ecd58-122">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ecd58-122">Example</span></span>

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a><span data-ttu-id="ecd58-123">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="ecd58-123">Request body</span></span>

<span data-ttu-id="ecd58-124">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="ecd58-124">Do not supply a request body for this method.</span></span>

## <a name="response"></a><span data-ttu-id="ecd58-125">Antwort</span><span class="sxs-lookup"><span data-stu-id="ecd58-125">Response</span></span>

<span data-ttu-id="ecd58-126">Wenn das Abonnement gefunden und erfolgreich gelöscht wird, wird eine `204 No Content`-Antwort zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="ecd58-126">If the subscription is found and successfully deleted, then a `204 No Content` response is returned.</span></span>

### <a name="example"></a><span data-ttu-id="ecd58-127">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ecd58-127">Example</span></span>

```http
HTTP/1.1 204 No Content
```
