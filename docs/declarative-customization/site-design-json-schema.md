---
title: JSON-Schema eines Websitedesigns
description: "JSON-Schemareferenz zum Erstellen von Websitedesigns für SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: ed952df480601945f1214282658c55d5eb63b5a9
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="aabe3-103">JSON-Schema eines Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="aabe3-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="aabe3-104">Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="aabe3-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="aabe3-105">Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.</span><span class="sxs-lookup"><span data-stu-id="aabe3-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="aabe3-106">Das Websitedesign besteht aus einer Liste von Aktionen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-106">The site design is a list of actions.</span></span> <span data-ttu-id="aabe3-107">Für komplexere Aktionen, z. B. das Erstellen einer Liste, gibt es auch Unteraktionen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="aabe3-108">Jede Aktion wird durch den Wert „verb“ angegeben.</span><span class="sxs-lookup"><span data-stu-id="aabe3-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="aabe3-109">Verb-Aktionen werden in der Reihenfolge ausgeführt, in der sie im JSON-Skript angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="aabe3-109">Verb actions are run in the order they appear in the JSON script.</span></span> <span data-ttu-id="aabe3-110">Nur die hier aufgeführten Verb-Aktionen können verwendet werden. Andernfalls wird ein Fehler vom Typ „Aktion kann nicht verarbeitet werden“ ausgelöst, wenn Sie versuchen, ein Websiteskript hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-110">Only the verb actions listed here can be used, otherwise an "unable to handle action" error will be thrown when trying to upload a site script.</span></span> <span data-ttu-id="aabe3-111">Weitere Aktionen werden im Laufe der Zeit hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="aabe3-111">More actions will be added over time.</span></span> 

<span data-ttu-id="aabe3-112">Die allgemeine JSON-Struktur wird wie folgt angegeben:</span><span class="sxs-lookup"><span data-stu-id="aabe3-112">The overall JSON structure is specified as follows:</span></span>

```json
{
    "$schema": "schema.json",
        "actions": [
            ...
            <one or more verb actions>
            ...
        ],
        "bindata": { },
        "version": 1
};
```

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="aabe3-113">Erstellen einer neuen SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="aabe3-113">Create a new SharePoint list</span></span>

<span data-ttu-id="aabe3-114">Verwenden Sie das Verb **createSPList**, um eine neue SharePoint-Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-114">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="aabe3-115">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="aabe3-115">JSON values:</span></span>

- <span data-ttu-id="aabe3-116">**listName** - Der Name der Liste, anhand der Benutzer diese identifzieren können.</span><span class="sxs-lookup"><span data-stu-id="aabe3-116">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="aabe3-117">**templateType** - Welche Vorlage auf die Liste angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="aabe3-117">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="aabe3-118">In der Regel wird der Wert „100“ verwendet.</span><span class="sxs-lookup"><span data-stu-id="aabe3-118">Typically you would use value 100.</span></span> <span data-ttu-id="aabe3-119">Vorlagentypwerte sind in [SPListTemplateType-Enumeration](https://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.splisttemplatetype.aspx) dokumentiert.</span><span class="sxs-lookup"><span data-stu-id="aabe3-119">Template type values are documented in [SPListTemplateType enumeration](https://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.splisttemplatetype.aspx).</span></span>
- <span data-ttu-id="aabe3-120">**subactions** - Ein Array von Aktionen, die in der aufgeführten Reihenfolge ausgeführt werden, um Ihre Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-120">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="aabe3-121">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-121">Example:</span></span>

```json
{
    "verb": "createSPList",
    "listName": "Customer Tracking",
    "templateType": 100,
    "subactions": [
        {
            "verb": "setDescription",
            "description": "List of Customers and Orders"
         }
    ]
}
```

<span data-ttu-id="aabe3-122">Das Array mit Unteraktionen bietet zusätzliche Aktionen, um anzugeben, wie die Liste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="aabe3-122">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="aabe3-123">Unteraktionen werden auch mithilfe eines **verb**-Werts angegeben.</span><span class="sxs-lookup"><span data-stu-id="aabe3-123">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="aabe3-124">setTitle</span><span class="sxs-lookup"><span data-stu-id="aabe3-124">setTitle</span></span>

<span data-ttu-id="aabe3-125">Legt einen Titel fest, der die Liste in Ansichten identifiziert.</span><span class="sxs-lookup"><span data-stu-id="aabe3-125">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="aabe3-126">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-126">JSON value:</span></span>

- <span data-ttu-id="aabe3-127">**title** - Der Titel der neuen Liste.</span><span class="sxs-lookup"><span data-stu-id="aabe3-127">**title** - The title of the new list.</span></span>

<span data-ttu-id="aabe3-128">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-128">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="aabe3-129">setDescription</span><span class="sxs-lookup"><span data-stu-id="aabe3-129">setDescription</span></span>

<span data-ttu-id="aabe3-130">Legt die Beschreibung der Liste fest.</span><span class="sxs-lookup"><span data-stu-id="aabe3-130">Sets the description of the list.</span></span>

<span data-ttu-id="aabe3-131">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-131">JSON value:</span></span>

- <span data-ttu-id="aabe3-132">**description** - Die Beschreibung der neuen Liste.</span><span class="sxs-lookup"><span data-stu-id="aabe3-132">**description** - The description of the new list.</span></span>

<span data-ttu-id="aabe3-133">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-133">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="aabe3-134">addSPField</span><span class="sxs-lookup"><span data-stu-id="aabe3-134">addSPField</span></span>

<span data-ttu-id="aabe3-135">Fügt ein neues Feld hinzu.</span><span class="sxs-lookup"><span data-stu-id="aabe3-135">Adds a new field.</span></span>

<span data-ttu-id="aabe3-136">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="aabe3-136">JSON values:</span></span>

- <span data-ttu-id="aabe3-137">**fieldType** - Der Feldtyp kann auf **Text**, **Note**, **Number**, **Boolean**, **User** oder **DateTime** festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="aabe3-137">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="aabe3-138">**displayName** - Der Anzeigename des Felds.</span><span class="sxs-lookup"><span data-stu-id="aabe3-138">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="aabe3-139">**isRequired** - „True“, wenn dieses Feld Informationen enthalten muss, andernfalls „False“.</span><span class="sxs-lookup"><span data-stu-id="aabe3-139">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="aabe3-140">**addToDefaultView** - „True“, wenn das Feld der Standardansicht hinzugefügt wird, andernfalls „False“.</span><span class="sxs-lookup"><span data-stu-id="aabe3-140">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="aabe3-141">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-141">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="aabe3-142">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="aabe3-142">deleteSPField</span></span>

<span data-ttu-id="aabe3-143">Löscht ein Standardfeld, das vom ausgewählten Vorlagentyp bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="aabe3-143">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="aabe3-144">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-144">JSON value:</span></span>

- <span data-ttu-id="aabe3-145">**displayName** - Der Anzeigename, um das zu löschende Feld zu identifzieren.</span><span class="sxs-lookup"><span data-stu-id="aabe3-145">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="aabe3-146">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-146">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="aabe3-147">addContentType</span><span class="sxs-lookup"><span data-stu-id="aabe3-147">addContentType</span></span>

<span data-ttu-id="aabe3-148">Fügte einen Inhaltstyp zu der Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="aabe3-148">Adds a content type to the list.</span></span>

<span data-ttu-id="aabe3-149">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-149">JSON value:</span></span>

- <span data-ttu-id="aabe3-150">**name** - Der Name des hinzuzufügenden Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="aabe3-150">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="aabe3-151">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-151">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="aabe3-152">removeContentType</span><span class="sxs-lookup"><span data-stu-id="aabe3-152">removeContentType</span></span>

<span data-ttu-id="aabe3-153">Entfernt einen Inhaltstyp, der vom ausgewählten Vorlagentyp bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="aabe3-153">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="aabe3-154">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-154">JSON value:</span></span>

- <span data-ttu-id="aabe3-155">**name** - Der Name des zu entfernenden Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="aabe3-155">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="aabe3-156">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-156">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="aabe3-157">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="aabe3-157">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="aabe3-158">Legt die Spaltenformatierung für ein Feld fest.</span><span class="sxs-lookup"><span data-stu-id="aabe3-158">Sets column formatting for a field.</span></span> <span data-ttu-id="aabe3-159">Weitere Informationen zur Spaltenformatierung finden Sie unter [Anpassen von SharePoint mithilfe von Spaltenformatierungen](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="aabe3-159">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="aabe3-160">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="aabe3-160">JSON values:</span></span>

- <span data-ttu-id="aabe3-161">**fieldDisplayName** - Der Anzeigename des zu verwendenden Felds.</span><span class="sxs-lookup"><span data-stu-id="aabe3-161">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="aabe3-162">**formatterJSON** - Ein JSON-Objekt, das als das CustomFormatter-Feld verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="aabe3-162">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="aabe3-163">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-163">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="aabe3-164">Hinzufügen eines Navigationslinks</span><span class="sxs-lookup"><span data-stu-id="aabe3-164">Add a navigation link</span></span>

<span data-ttu-id="aabe3-165">Verwenden Sie das Verb **addNavLink**, um der Website einen neuen Navigationslink hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-165">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="aabe3-166">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="aabe3-166">JSON values:</span></span>

- <span data-ttu-id="aabe3-167">**url** - Die URL des hinzuzufügenden Links.</span><span class="sxs-lookup"><span data-stu-id="aabe3-167">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="aabe3-168">**displayName** - Der Anzeigename des Links.</span><span class="sxs-lookup"><span data-stu-id="aabe3-168">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="aabe3-169">**isWebRelative** - „True“, wenn der Link relativ zum Web ist, andernfalls „False.“</span><span class="sxs-lookup"><span data-stu-id="aabe3-169">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="aabe3-170">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-170">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="aabe3-171">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="aabe3-171">Apply a theme</span></span>

<span data-ttu-id="aabe3-172">Verwenden Sie das Verb **applyTheme**, um der Website ein benutzerdefiniertes Design hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-172">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="aabe3-173">Weitere Informationen zum Erstellen und Hochladen von Designs finden Sie unter [SharePoint-Websitedesign](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aabe3-173">For more information on how to construct and upload these themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span> <span data-ttu-id="aabe3-174">Beachten Sie, dass diese Websiteaktion nur für das Anwenden benutzerdefinierter Designs funktioniert. Um ein SharePoint-Produktdesign anzuwenden, müssen Sie eine Kopie eines benutzerdefinierten Designs erstellen und auf dieses Design verweisen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-174">Note that this site action only works for applying custom themes; to apply one of our in-product SharePoint themes, create a copy as a custom one and reference that one.</span></span>

<span data-ttu-id="aabe3-175">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-175">JSON value:</span></span>

- <span data-ttu-id="aabe3-176">**themeName** - Der Name des anzuwendenden Designs.</span><span class="sxs-lookup"><span data-stu-id="aabe3-176">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="aabe3-177">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-177">Example:</span></span>

<!-- TBD: add link to Doug's Blue Yonder theme with note you need to create it first -->

```json
{
   "verb": "applyTheme",
   "themeName": "Blue Yonder"
}
```

<!-- 
## Create a page

Use the **createPage** verb to create a new page on the site.

JSON values:

- **fileName** - The name of the file.
- **setAsHomePage** - True if this page is the home page; otherwise, false.
- **pageData** - An object with additional information about the page. **pageData** requires the following values:
  - **Title** - The title of the page.
  - **BannerImageUrl** - A URL specifying the location of an image to display for the banner. <TBD: need more info>
  - **CanvasContent1** - Content for the page specified as XML. <TBD: need more info>
  - **LayoutWebpartsContent** - JSON for the layout. <TBD: need more info>

Example:

```json
{
   "verb": "createPage",
   "fileName": "event-collateral.aspx",
   "pageData":
        {
            "Title": "Comment customer events",
            "BannerImageUrl": "/Customer Event Collateral/customer.jpg",
            "CanvasContent1": "<xml>",
            "LayoutWebpartsContent": "{json}"
        },
    "setAsHomePage": true
}
```
-->

## <a name="set-a-site-logo"></a><span data-ttu-id="aabe3-178">Festlegen eines Websitelogos</span><span class="sxs-lookup"><span data-stu-id="aabe3-178">Set a site logo</span></span>

<span data-ttu-id="aabe3-179">Verwenden Sie das Verb **setSiteLogo**, um ein Logo für Ihre Website anzugeben.</span><span class="sxs-lookup"><span data-stu-id="aabe3-179">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="aabe3-180">Diese Aktion funktioniert nur für die Kommunikationswebsitevorlage (68).</span><span class="sxs-lookup"><span data-stu-id="aabe3-180">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="aabe3-181">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-181">JSON value:</span></span>

- <span data-ttu-id="aabe3-182">**url** - Die URL des zu verwendenden Logobilds.</span><span class="sxs-lookup"><span data-stu-id="aabe3-182">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="aabe3-183">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-183">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="aabe3-184">Beitreten zu einem Hub-Standort</span><span class="sxs-lookup"><span data-stu-id="aabe3-184">Join a hub site</span></span>

<span data-ttu-id="aabe3-185">Verwenden Sie das Verb **joinHubSite**, um die Website einem Hub hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-185">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="aabe3-186">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="aabe3-186">JSON value:</span></span>

- <span data-ttu-id="aabe3-187">**hubSiteId** - Die ID des Hub-Standorts für den Beitritt.</span><span class="sxs-lookup"><span data-stu-id="aabe3-187">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="aabe3-188">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-188">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="aabe3-189">Auslösen eines Flusses</span><span class="sxs-lookup"><span data-stu-id="aabe3-189">Trigger a flow</span></span>

<span data-ttu-id="aabe3-190">Verwenden Sie das Verb **triggerFlow**, um einen benutzerdefinierten Fluss auzulösen.</span><span class="sxs-lookup"><span data-stu-id="aabe3-190">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="aabe3-191">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="aabe3-191">JSON values:</span></span>

- <span data-ttu-id="aabe3-192">**url** - Eine Trigger-URL des Flusses.</span><span class="sxs-lookup"><span data-stu-id="aabe3-192">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="aabe3-193">**name** - Der Name des Flusses.</span><span class="sxs-lookup"><span data-stu-id="aabe3-193">**name** - The name of the flow.</span></span>
- <span data-ttu-id="aabe3-194">**parameters** - Ein optionaler Satz von Parameter, die an den Fluss übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="aabe3-194">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="aabe3-195">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aabe3-195">Example:</span></span>

```json
 {
    "verb": "triggerFlow",
    "url": "<A trigger URL of the Flow.>",
    "name": "Record and tweet site creation event",
    "parameters": {
        "event": "Microsoft Event",
        "product": "SharePoint"
    }
}
```
