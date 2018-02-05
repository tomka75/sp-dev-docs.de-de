---
title: "Anpassen der standardmäßigen Websitedesigns in SharePoint"
description: "Anpassen der standardmäßigen Websitedesigns auf der SharePoint-Teamwebsite oder auf der Kommunikations-Websitevorlage"
ms.date: 12/18/2017
ms.openlocfilehash: 34107e7028400cec62b0f6454f3474b92ca288be
ms.sourcegitcommit: 9f492519d4eeb3f62a1fddc71cdca79263651a56
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="customize-a-default-site-design"></a><span data-ttu-id="aa06d-103">Anpassen eines standardmäßigen Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="aa06d-103">Customize a default site design</span></span>

> [!NOTE]
> <span data-ttu-id="aa06d-104">Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="aa06d-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="aa06d-105">Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.</span><span class="sxs-lookup"><span data-stu-id="aa06d-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="aa06d-106">SharePoint enthält zahlreiche Websitedesigns, die bereits in den SharePoint Online-Websitevorlagen verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="aa06d-106">SharePoint contains several site designs already available in the SharePoint Online site templates.</span></span> <span data-ttu-id="aa06d-107">Dies sind die standardmäßigen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="aa06d-107">These are the default site designs.</span></span> <span data-ttu-id="aa06d-108">Sie können diese mit PowerShell oder den REST-APIs so ändern, dass sie die gesamte Websitebereitstellung steuern.</span><span class="sxs-lookup"><span data-stu-id="aa06d-108">You can modify them using PowerShell or the REST APIs to control the entire site provisioning experience.</span></span> <span data-ttu-id="aa06d-109">Sie können zum Beispiel sicherstellen, dass das Unternehmensdesign auf jede Website angewendet wird, die erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="aa06d-109">For example, you can ensure that your company theme is applied to every site that gets created.</span></span> <span data-ttu-id="aa06d-110">Sie können auch sicherstellen, dass ein Protokollierungsmechanismus immer ausgeführt wird, unabhängig davon, welcher Websitedesign ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="aa06d-110">Or you can make sure a logging mechanism always runs regardless of which site design is chosen.</span></span>

## <a name="apply-a-site-design-to-the-default-site-designs"></a><span data-ttu-id="aa06d-111">Anwenden eines Websitedesigns auf die standardmäßigen Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="aa06d-111">Apply a site design to the default site designs</span></span>

<span data-ttu-id="aa06d-112">Um die standardmäßigen Websitedesigns anzupassen, wenden Sie ein neues Design mit dem Powershell-Cmdlet **Add-SPOSiteDesign** oder der REST-API **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="aa06d-112">To customize the default site designs, apply a new one with the Powershell **Add-SPOSiteDesign** cmdlet, or the **CreateSiteDesign** REST API.</span></span> <span data-ttu-id="aa06d-113">Geben Sie die Option **IsDefault** an, damit das Websitedesign standardmäßig angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="aa06d-113">Specify the **IsDefault** switch to apply the site design as default.</span></span>

<span data-ttu-id="aa06d-114">Das folgende Beispiel zeigt, wie Sie mithilfe der **IsDefault**-Option das Contoso-Unternehmensdesign auf die standardmäßigen Websitedesigns anwenden.</span><span class="sxs-lookup"><span data-stu-id="aa06d-114">The following example shows how to use the **IsDefault** switch to apply the Contoso company theme to the default site designs.</span></span> <span data-ttu-id="aa06d-115">Das Website-Skript, auf das durch die ID verwiesen wird, enthält das JSON-Skript zum Anwenden des richtigen Designs.</span><span class="sxs-lookup"><span data-stu-id="aa06d-115">The site script referenced by ID contains the JSON script to apply the correct theme.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso company theme" `
  -WebTemplate "68" `
  -SiteScripts "89516c6d-9f4d-4a57-ae79-36b0c95a817b" `
  -Description "Applies standard company theme to site" `
  -IsDefault
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"Contoso company theme", Description:"Applies standard company theme to site", SiteScriptIds:["89516c6d-9f4d-4a57-ae79-36b0c95a817b"],  WebTemplate:"68", IsDefault: true}});
```

## <a name="which-default-site-designs-are-updated"></a><span data-ttu-id="aa06d-116">Welche standardmäßigen Websitedesigns werden aktualisiert?</span><span class="sxs-lookup"><span data-stu-id="aa06d-116">Which default site designs are updated?</span></span>

<span data-ttu-id="aa06d-117">Im vorherigen Beispiel verweist der **WebTemplate**-Wert 68 auf die Websitevorlage für SharePoint Online-Kommunikation.</span><span class="sxs-lookup"><span data-stu-id="aa06d-117">In the previous example, the **WebTemplate** value of "68" refers to the SharePoint Online communication site template.</span></span> <span data-ttu-id="aa06d-118">Diese Vorlage enthält die folgenden standardmäßigen Websitedesigns:</span><span class="sxs-lookup"><span data-stu-id="aa06d-118">That template contains the following default site designs:</span></span>

- <span data-ttu-id="aa06d-119">Thema</span><span class="sxs-lookup"><span data-stu-id="aa06d-119">Topic</span></span>
- <span data-ttu-id="aa06d-120">Showcase</span><span class="sxs-lookup"><span data-stu-id="aa06d-120">Showcase</span></span>
- <span data-ttu-id="aa06d-121">Leer</span><span class="sxs-lookup"><span data-stu-id="aa06d-121">Blank</span></span>

<span data-ttu-id="aa06d-122">Wenn Sie ein neues Websitedesign anwenden, werden alle drei der standardmäßigen Websitedesigns aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="aa06d-122">When you apply a new site design, it will update all three of the default site designs at the same time.</span></span>

<span data-ttu-id="aa06d-123">Die Vorlage für SharePoint Online-Teamwebsite enthält nur das standardmäßige Websitedesign mit dem Namen **Team**.</span><span class="sxs-lookup"><span data-stu-id="aa06d-123">The SharePoint Online team site template contains only one default site design named **Team**.</span></span> <span data-ttu-id="aa06d-124">In diesem Fall wird beim Anwenden eines standardmäßigen Websitedesigns nur das Websitedesign mit dem Namen **Team** aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="aa06d-124">In this case when you apply a default site design, only the **Team** site design is updated.</span></span>

## <a name="restoring-the-default-site-designs"></a><span data-ttu-id="aa06d-125">Wiederherstellen standardmäßiger Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="aa06d-125">Restoring the default site designs</span></span>

<span data-ttu-id="aa06d-126">Entfernen Sie das angewendete Websitedesign, um ein Websitedesign auf die Standardeinstellungen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="aa06d-126">To restore a site design to the defaults, remove the site design you applied.</span></span> <span data-ttu-id="aa06d-127">Wenn Sie im vorherigen Beispiel das Websitedesign mit der ID db752673-18fd-44db-865a-aa3e0b28698e erstellt haben, würden Sie es entfernen, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="aa06d-127">In the previous example, if the site design created had the ID db752673-18fd-44db-865a-aa3e0b28698e, you would remove it as shown in the following example.</span></span>

```powershell
C:\> Remove-SPOSiteDesign db752673-18fd-44db-865a-aa3e0b28698e
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"db752673-18fd-44db-865a-aa3e0b28698e"});
```

> [!NOTE]
> <span data-ttu-id="aa06d-128">Wenn Sie nicht sicher sind, welche Websitedesigns die Standardeinstellung sind, führen Sie das Cmdlet **Get-SPOSiteDesign** aus.</span><span class="sxs-lookup"><span data-stu-id="aa06d-128">If you're not sure which site design is the default, run the **Get-SPOSiteDesign** cmdlet.</span></span> <span data-ttu-id="aa06d-129">Damit werden alle Websitedesigns aufgeführt und es wird angegeben, welche die standardmäßigen sind.</span><span class="sxs-lookup"><span data-stu-id="aa06d-129">It will list all site designs, and indicates which ones are defaults.</span></span>
