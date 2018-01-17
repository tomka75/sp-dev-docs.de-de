---
title: JSON-Schema eines Websitedesigns
description: "JSON-Schemareferenz zum Erstellen von Websitedesigns für SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: 8fcc88c854b948c785db6181fa66e307128b343d
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="79927-103">JSON-Schema eines Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="79927-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="79927-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="79927-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="79927-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="79927-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="79927-106">Das Websitedesign besteht aus einer Liste von Aktionen.</span><span class="sxs-lookup"><span data-stu-id="79927-106">The site design is a list of actions.</span></span> <span data-ttu-id="79927-107">Für komplexere Aktionen, z. B. das Erstellen einer Liste, gibt es auch Unteraktionen.</span><span class="sxs-lookup"><span data-stu-id="79927-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="79927-108">Jede Aktion wird durch den Wert „verb“ angegeben.</span><span class="sxs-lookup"><span data-stu-id="79927-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="79927-109">Verb-Aktionen werden in der Reihenfolge ausgeführt, in der Sie im JSON-Skript angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="79927-109">Verb actions are run in the order they appear in the JSON script.</span></span>

<span data-ttu-id="79927-110">Die allgemeine JSON-Struktur wird wie folgt angegeben:</span><span class="sxs-lookup"><span data-stu-id="79927-110">The overall JSON structure is specified as follows:</span></span>

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

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="79927-111">Erstellen einer neuen SharePoint-Liste</span><span class="sxs-lookup"><span data-stu-id="79927-111">Create a new SharePoint list</span></span>

<span data-ttu-id="79927-112">Verwenden Sie das Verb **createSPList**, um eine neue SharePoint-Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="79927-112">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="79927-113">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="79927-113">JSON values:</span></span>

- <span data-ttu-id="79927-114">**listName** - Der Name der Liste, anhand der Benutzer diese identifzieren können.</span><span class="sxs-lookup"><span data-stu-id="79927-114">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="79927-115">**templateType** - Welche Vorlage auf die Liste angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="79927-115">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="79927-116">In der Regel wird der Wert „100“ verwendet.</span><span class="sxs-lookup"><span data-stu-id="79927-116">Typically you would use value 100.</span></span> <span data-ttu-id="79927-117">Vorlagentypwerte sind in [SPListTemplateType-Enumeration](https://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.splisttemplatetype.aspx) dokumentiert.</span><span class="sxs-lookup"><span data-stu-id="79927-117">Template type values are documented in [SPListTemplateType enumeration](https://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.splisttemplatetype.aspx).</span></span>
- <span data-ttu-id="79927-118">**subactions** - Ein Array von Aktionen, die in der aufgeführten Reihenfolge ausgeführt werden, um Ihre Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="79927-118">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="79927-119">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-119">Example:</span></span>

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

<span data-ttu-id="79927-120">Das Array mit Unteraktionen bietet zusätzliche Aktionen, um anzugeben, wie die Liste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="79927-120">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="79927-121">Unteraktionen werden auch mithilfe eines **verb**-Werts angegeben.</span><span class="sxs-lookup"><span data-stu-id="79927-121">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="79927-122">setTitle</span><span class="sxs-lookup"><span data-stu-id="79927-122">setTitle</span></span>

<span data-ttu-id="79927-123">Legt einen Titel fest, der die Liste in Ansichten identifiziert.</span><span class="sxs-lookup"><span data-stu-id="79927-123">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="79927-124">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-124">JSON value:</span></span>

- <span data-ttu-id="79927-125">**title** - Der Titel der neuen Liste.</span><span class="sxs-lookup"><span data-stu-id="79927-125">**title** - The title of the new list.</span></span>

<span data-ttu-id="79927-126">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-126">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="79927-127">setDescription</span><span class="sxs-lookup"><span data-stu-id="79927-127">setDescription</span></span>

<span data-ttu-id="79927-128">Legt die Beschreibung der Liste fest.</span><span class="sxs-lookup"><span data-stu-id="79927-128">Sets the description of the list.</span></span>

<span data-ttu-id="79927-129">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-129">JSON value:</span></span>

- <span data-ttu-id="79927-130">**description** - Die Beschreibung der neuen Liste.</span><span class="sxs-lookup"><span data-stu-id="79927-130">**description** - The description of the new list.</span></span>

<span data-ttu-id="79927-131">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-131">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="79927-132">addSPField</span><span class="sxs-lookup"><span data-stu-id="79927-132">addSPField</span></span>

<span data-ttu-id="79927-133">Fügt ein neues Feld hinzu.</span><span class="sxs-lookup"><span data-stu-id="79927-133">Adds a new field.</span></span>

<span data-ttu-id="79927-134">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="79927-134">JSON values:</span></span>

- <span data-ttu-id="79927-135">**fieldType** - Der Feldtyp kann auf **Text**, **Note**, **Number**, **Boolean**, **User** oder **DateTime** festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="79927-135">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="79927-136">**displayName** - Der Anzeigename des Felds.</span><span class="sxs-lookup"><span data-stu-id="79927-136">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="79927-137">**isRequired** - „True“, wenn dieses Feld Informationen enthalten muss, andernfalls „False“.</span><span class="sxs-lookup"><span data-stu-id="79927-137">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="79927-138">**addToDefaultView** - „True“, wenn das Feld der Standardansicht hinzugefügt wird, andernfalls „False“.</span><span class="sxs-lookup"><span data-stu-id="79927-138">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="79927-139">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-139">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="79927-140">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="79927-140">deleteSPField</span></span>

<span data-ttu-id="79927-141">Löscht ein Standardfeld, das vom ausgewählten Vorlagentyp bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="79927-141">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="79927-142">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-142">JSON value:</span></span>

- <span data-ttu-id="79927-143">**displayName** - Der Anzeigename, um das zu löschende Feld zu identifzieren.</span><span class="sxs-lookup"><span data-stu-id="79927-143">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="79927-144">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-144">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="79927-145">addContentType</span><span class="sxs-lookup"><span data-stu-id="79927-145">addContentType</span></span>

<span data-ttu-id="79927-146">Fügte einen Inhaltstyp zu der Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="79927-146">Adds a content type to the list.</span></span>

<span data-ttu-id="79927-147">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-147">JSON value:</span></span>

- <span data-ttu-id="79927-148">**name** - Der Name des hinzuzufügenden Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="79927-148">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="79927-149">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-149">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="79927-150">removeContentType</span><span class="sxs-lookup"><span data-stu-id="79927-150">removeContentType</span></span>

<span data-ttu-id="79927-151">Entfernt einen Inhaltstyp, der vom ausgewählten Vorlagentyp bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="79927-151">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="79927-152">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-152">JSON value:</span></span>

- <span data-ttu-id="79927-153">**name** - Der Name des zu entfernenden Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="79927-153">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="79927-154">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-154">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="79927-155">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="79927-155">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="79927-156">Legt die Spaltenformatierung für ein Feld fest.</span><span class="sxs-lookup"><span data-stu-id="79927-156">Sets column formatting for a field.</span></span> <span data-ttu-id="79927-157">Weitere Informationen zur Spaltenformatierung finden Sie unter [Anpassen von SharePoint mithilfe von Spaltenformatierungen](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="79927-157">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="79927-158">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="79927-158">JSON values:</span></span>

- <span data-ttu-id="79927-159">**fieldDisplayName** - Der Anzeigename des zu verwendenden Felds.</span><span class="sxs-lookup"><span data-stu-id="79927-159">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="79927-160">**formatterJSON** - Ein JSON-Objekt, das als das CustomFormatter-Feld verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="79927-160">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="79927-161">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-161">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="79927-162">Hinzufügen eines Navigationslinks</span><span class="sxs-lookup"><span data-stu-id="79927-162">Add a navigation link</span></span>

<span data-ttu-id="79927-163">Verwenden Sie das Verb **addNavLink**, um der Website einen neuen Navigationslink hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="79927-163">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="79927-164">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="79927-164">JSON values:</span></span>

- <span data-ttu-id="79927-165">**url** - Die URL des hinzuzufügenden Links.</span><span class="sxs-lookup"><span data-stu-id="79927-165">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="79927-166">**displayName** - Der Anzeigename des Links.</span><span class="sxs-lookup"><span data-stu-id="79927-166">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="79927-167">**isWebRelative** - „True“, wenn der Link relativ zum Web ist, andernfalls „False.“</span><span class="sxs-lookup"><span data-stu-id="79927-167">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="79927-168">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-168">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="79927-169">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="79927-169">Apply a theme</span></span>

<span data-ttu-id="79927-170">Verwenden Sie das Verb **applyTheme**, um der Website ein Design hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="79927-170">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="79927-171">Weitere Informationen zu Designs finden Sie unter [SharePoint-Websitedesign](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79927-171">For more information on themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span>

<span data-ttu-id="79927-172">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-172">JSON value:</span></span>

- <span data-ttu-id="79927-173">**themeName** - Der Name des anzuwendenden Designs.</span><span class="sxs-lookup"><span data-stu-id="79927-173">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="79927-174">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-174">Example:</span></span>

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

## <a name="set-a-site-logo"></a><span data-ttu-id="79927-175">Festlegen eines Websitelogos</span><span class="sxs-lookup"><span data-stu-id="79927-175">Set a site logo</span></span>

<span data-ttu-id="79927-176">Verwenden Sie das Verb **setSiteLogo**, um ein Logo für Ihre Website anzugeben.</span><span class="sxs-lookup"><span data-stu-id="79927-176">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="79927-177">Diese Aktion funktioniert nur für die Kommunikationswebsitevorlage (68).</span><span class="sxs-lookup"><span data-stu-id="79927-177">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="79927-178">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-178">JSON value:</span></span>

- <span data-ttu-id="79927-179">**url** - Die URL des zu verwendenden Logobilds.</span><span class="sxs-lookup"><span data-stu-id="79927-179">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="79927-180">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-180">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="79927-181">Beitreten zu einem Hub-Standort</span><span class="sxs-lookup"><span data-stu-id="79927-181">Join a hub site</span></span>

<span data-ttu-id="79927-182">Verwenden Sie das Verb **joinHubSite**, um die Website einem Hub hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="79927-182">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="79927-183">JSON-Wert:</span><span class="sxs-lookup"><span data-stu-id="79927-183">JSON value:</span></span>

- <span data-ttu-id="79927-184">**hubSiteId** - Die ID des Hub-Standorts für den Beitritt.</span><span class="sxs-lookup"><span data-stu-id="79927-184">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="79927-185">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-185">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="79927-186">Auslösen eines Flusses</span><span class="sxs-lookup"><span data-stu-id="79927-186">Trigger a flow</span></span>

<span data-ttu-id="79927-187">Verwenden Sie das Verb **triggerFlow**, um einen benutzerdefinierten Fluss auzulösen.</span><span class="sxs-lookup"><span data-stu-id="79927-187">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="79927-188">JSON-Werte:</span><span class="sxs-lookup"><span data-stu-id="79927-188">JSON values:</span></span>

- <span data-ttu-id="79927-189">**url** - Eine Trigger-URL des Flusses.</span><span class="sxs-lookup"><span data-stu-id="79927-189">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="79927-190">**name** - Der Name des Flusses.</span><span class="sxs-lookup"><span data-stu-id="79927-190">**name** - The name of the flow.</span></span>
- <span data-ttu-id="79927-191">**parameters** - Ein optionaler Satz von Parameter, die an den Fluss übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="79927-191">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="79927-192">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="79927-192">Example:</span></span>

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
