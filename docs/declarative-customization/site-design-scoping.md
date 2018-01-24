---
title: "Bereichsdefinition für den Zugriff auf SharePoint-Websitedesigns"
description: "Legen Sie den Bereich für SharePoint-Websitedesigns fest, um zu steuern, wer diese anzeigen und darauf zugreifen kann."
ms.date: 12/14/2017
ms.openlocfilehash: c0896cab28a4c9cba3f74fbad8120061311004a2
ms.sourcegitcommit: d9372f6009de1c1e48e272fd3629a99aed7fef9f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="scoping-access-to-site-designs"></a><span data-ttu-id="00b0d-103">Bereichsdefinition für den Zugriff auf Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="00b0d-103">Scoping access to site designs</span></span>

> [!NOTE]
> <span data-ttu-id="00b0d-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="00b0d-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="00b0d-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="00b0d-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="00b0d-106">Websitedesigns stehen standardmäßig allen Benutzern zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="00b0d-106">Site designs are available to everyone by default.</span></span> <span data-ttu-id="00b0d-107">Sie können den Bereich von Websitedesigns jedoch so festlegen, dass diese nur für bestimmte Benutzer oder Gruppen verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="00b0d-107">But you can scope site designs so that they are only available to specific users or groups.</span></span> <span data-ttu-id="00b0d-108">Die Buchhaltungsabteilung verfügt beispielsweise über spezielle Websitedesigns, es macht aber vielleicht keinen Sinn, diese Websitedesigns für alle Personen freizugeben.</span><span class="sxs-lookup"><span data-stu-id="00b0d-108">For example, the accounting apartment may have specific site designs they use, but it may not make sense to share those site designs with everyone.</span></span> <span data-ttu-id="00b0d-109">In diesem Artikel wird erläutert, wie Sie steuern können, welche Benutzer und Gruppen bestimmte Websitedesigns anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="00b0d-109">This article will explain how you can control which users and groups can see specific site designs.</span></span>

## <a name="granting-rights-to-a-site-design"></a><span data-ttu-id="00b0d-110">Erteilen von Berechtigungen für ein Websitedesign</span><span class="sxs-lookup"><span data-stu-id="00b0d-110">Granting rights to a site design</span></span>

<span data-ttu-id="00b0d-111">Bei der Erstellung eines Websitedesigns ist dieses zunächst für alle Benutzer verfügbar.</span><span class="sxs-lookup"><span data-stu-id="00b0d-111">When a site design is first created it is available to everyone.</span></span> <span data-ttu-id="00b0d-112">Sie können Berechtigungen des Typs **Anzeigen** für das Websitedesign erteilen.</span><span class="sxs-lookup"><span data-stu-id="00b0d-112">You can grant **View** rights to the site design.</span></span> <span data-ttu-id="00b0d-113">Sobald Berechtigungen erteilt wurden, haben nur die angegebenen Benutzer oder Gruppen (Prinzipale) Zugriff.</span><span class="sxs-lookup"><span data-stu-id="00b0d-113">Once rights are granted, only the users or groups (principals) specified have access.</span></span> <span data-ttu-id="00b0d-114">Mit nachfolgenden API-Aufrufen können Sie weiteren Prinzipalen Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="00b0d-114">You can continue granting rights to more principals with subsequent API calls.</span></span>

## <a name="granting-rights-to-security-groups"></a><span data-ttu-id="00b0d-115">Erteilen von Berechtigungen für Sicherheitsgruppen</span><span class="sxs-lookup"><span data-stu-id="00b0d-115">Granting rights to security groups</span></span>

<span data-ttu-id="00b0d-116">Nachfolgend finden Sie ein Beispiel, wie der Bereich eines vorhandenen Websitedesigns so festgelegt werden kann, dass nur die E-Mail-aktivierte Sicherheitsgruppe **accounting** das Websitedesign anzeigen und verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="00b0d-116">Here's an example of how to scope an existing site design so that only the mail-enabled security group **accounting** can view and use the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

<span data-ttu-id="00b0d-117">Vielleicht möchten Sie Berechtigungen auch direkt bei der Erstellung eines Websitedesigns erteilen. Das funktioniert wie in diesem Beispiel demonstriert:</span><span class="sxs-lookup"><span data-stu-id="00b0d-117">You may want to create a new site design and grant rights at the same time as shown in the next example.</span></span>

```powershell
Add-SPOSiteDesign `
  -Title "Scoped site design" `
  -Description "Scoped to only the accounting email security group" `
  -SiteScripts 256494cb-bd31-4f60-9eba-285308d7a863 `
  -WebTemplate 64 `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/scope-image.png" `
| Grant-SPOSiteDesignRights `
  -Principals ("accounting@contoso.com") `
  -Rights View
```

## <a name="granting-rights-to-users"></a><span data-ttu-id="00b0d-118">Erteilen von Berechtigungen für Benutzer</span><span class="sxs-lookup"><span data-stu-id="00b0d-118">Granting rights to users</span></span>

<span data-ttu-id="00b0d-119">Im folgenden Beispiel wird gezeigt, wie Sie einem Benutzer (Nestor) auf der fiktiven Contoso-Website Anzeigeberechtigungen für ein Websitedesign erteilen können.</span><span class="sxs-lookup"><span data-stu-id="00b0d-119">Here's an example of how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="viewing-rights-assigned-to-a-site-design"></a><span data-ttu-id="00b0d-120">Anzeigeberechtigungen, die einem Websitedesign zugewiesen sind</span><span class="sxs-lookup"><span data-stu-id="00b0d-120">Viewing rights assigned to a site design</span></span>

<span data-ttu-id="00b0d-121">Verwenden Sie zum Anzeigen von Berechtigungen das Cmdlet **Get-SPOSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="00b0d-121">To view rights, use the **Get-SPOSiteDesignRights** cmdlet.</span></span> <span data-ttu-id="00b0d-122">Im folgenden Beispiel wird gezeigt, wie dieses Cmdlet und eine Antwort verwendet wird, wenn nur der Nestor über Anzeigeberechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="00b0d-122">The following example shows how to use this cmdlet and a response in the case where only Nestor has view rights.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="revoking-rights-from-a-site-design"></a><span data-ttu-id="00b0d-123">Widerrufen von Berechtigungen von einem Websitedesign</span><span class="sxs-lookup"><span data-stu-id="00b0d-123">Revoking rights from a site design</span></span>

<span data-ttu-id="00b0d-124">Sie können die Berechtigungen jedes Prinzipals jederzeit widerrufen.</span><span class="sxs-lookup"><span data-stu-id="00b0d-124">You can revoke rights for any principal.</span></span> <span data-ttu-id="00b0d-125">Wenn Sie die Anzeigeberechtigungen für alle Prinzipale widerrufen, steht das Websitedesign wieder für alle Benutzer zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="00b0d-125">If you revoke view rights for all principles, then the site design will again be available to everyone.</span></span>

<span data-ttu-id="00b0d-126">Nachfolgend finden Sie ein Beispiel dafür, wie sich die Zugriffsberechtigungen der E-Mail-aktivierten Sicherheitsgruppe „accounting“ und des Benutzers „Nestor“ widerrufen lassen.</span><span class="sxs-lookup"><span data-stu-id="00b0d-126">Here's an example of revoking access for the accounting mail-enabled security group and Nestor.</span></span>

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
