---
title: "Vereinfachen des Hinzufügens von Webparts mit vorkonfigurierten Einträgen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6adeab3325aa9ba73b16ee9a182825d48b2eb300
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/20/2017
---
# <a name="simplify-adding-web-parts-with-preconfigured-entries"></a><span data-ttu-id="343be-102">Vereinfachen des Hinzufügens von Webparts mit vorkonfigurierten Einträgen</span><span class="sxs-lookup"><span data-stu-id="343be-102">Simplify adding web parts with preconfigured entries</span></span>

<span data-ttu-id="343be-p101">Komplexere clientseitige SharePoint Framework-Webparts können zahlreiche Eigenschaften haben, die vom Benutzer konfiguriert werden müssen. Sie können Benutzer unterstützen, indem Sie vorkonfigurierte Eigenschafteneinträge für bestimmte Szenarien hinzufügen. Ein vorkonfigurierte Eintrag initialisiert das Webpart mit vordefinierten Werten. In diesem Artikel erfahren Sie, wie Sie vorkonfigurierte Einträge in einem clientseitigen SharePoint Framework-Webpart verwenden, um Benutzern vorkonfigurierte Versionen Ihres Webparts bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="343be-p101">More complex SharePoint Framework client-side web parts will likely have many properties that the user must configure. You can help users by adding preconfigured property entries for specific scenarios. A preconfigured entry will initialize the web part with preset values. In this article you will learn how you to use preconfigured entries in a SharePoint Framework client-side web part to provide users with preconfigured versions of your web part.</span></span>

> <span data-ttu-id="343be-107">**Hinweis:** Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für Ihr clientseitiges SharePoint-Webpart einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="343be-107">**Note:** Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="what-are-web-part-preconfigured-entries"></a><span data-ttu-id="343be-108">Was sind vorkonfigurierte Einträge für Webparts?</span><span class="sxs-lookup"><span data-stu-id="343be-108">What are web part preconfigured entries</span></span>

<span data-ttu-id="343be-109">Jedes clientseitige SharePoint Framework-Webpart besteht aus zwei Teilen: dem Manifest, das das Webpart beschreibt, und dem Webpartcode.</span><span class="sxs-lookup"><span data-stu-id="343be-109">Each SharePoint Framework client-side web part consists of two pieces: the manifest, that describes the web part, and the web part code.</span></span>

<span data-ttu-id="343be-110">Eine der im Webpartmanifest angegebenen Eigenschaften ist die **preconfiguredEntries**-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="343be-110">One of the properties specified in the web part manifest is the **preconfiguredEntries** property.</span></span>

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "6737645a-4443-4210-a70e-e5e2a219133a",
  "alias": "GalleryWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Under Development" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "Gallery"
    }
  }]
}
```

<span data-ttu-id="343be-p102">Die **preconfiguredEntries**-Eigenschaft enthält Informationen zu Ihrem Webpart zur Verwendung in der Webpart-Toolbox. Wenn Benutzer Webparts zu der Seite hinzufügen, werden die Informationen aus der **preconfiguredEntries**-Eigenschaft verwendet, um das Webpart in der Toolbox anzuzeigen und seine Standardeinstellungen zu definieren,wenn es zu der Seite hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="343be-p102">The **preconfiguredEntries** property provides information about your web part for use in the web part toolbox. When users add web parts to the page, the information from the **preconfiguredEntries** property is used to display the web part in the toolbox and define its default settings when it's added to the page.</span></span>

<span data-ttu-id="343be-p103">Wenn Sie klassische Webparts mit vollständig vertrauenswürdigen Lösungen erstellt haben, können Sie sich jeden Eintrag im **preconfiguredEntries**-Array so vorstellen, dass er einer **.webpart**-Datei entspricht. Genau wie eine **.webpart**-Datei ist jeder Eintrag in der **preconfiguredEntries**-Eigenschaft mit dem Webpartcode verknüpft und gibt grundlegende Informationen zu dem Webpart an, z. B. den Titel oder die Beschreibung sowie Standardwerte für seine Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="343be-p103">If you've built classic web parts with full-trust solutions, then you can think of each entry in the **preconfiguredEntries** array as corresponding to a **.webpart** file. Just like a **.webpart** file, each entry in the **preconfiguredEntries** property is linked to the web part code and specifies basic information about the web part such as its title or description as well as default values for its properties.</span></span>

### <a name="properties-of-a-preconfiguredentries-array-item"></a><span data-ttu-id="343be-115">Eigenschaften eines **preconfiguredEntries**-Arrayelements</span><span class="sxs-lookup"><span data-stu-id="343be-115">Properties of a **preconfiguredEntries** array item</span></span>

<span data-ttu-id="343be-p104">Jedes Element im **preconfiguredEntries**-Array umfasst mehrere Eigenschaften. In der folgenden Tabelle wird der Zweck jeder Eigenschaft erläutert.</span><span class="sxs-lookup"><span data-stu-id="343be-p104">Each item in the **preconfiguredEntries** array consists of several properties. The following table explains the purpose of each property.</span></span>

<span data-ttu-id="343be-118">Eigenschaftsname</span><span class="sxs-lookup"><span data-stu-id="343be-118">Property name</span></span>           |<span data-ttu-id="343be-119">Werttyp</span><span class="sxs-lookup"><span data-stu-id="343be-119">Value type</span></span>      |<span data-ttu-id="343be-120">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="343be-120">Required</span></span>|<span data-ttu-id="343be-121">Zweck</span><span class="sxs-lookup"><span data-stu-id="343be-121">Purpose</span></span>                                               |<span data-ttu-id="343be-122">Beispielwert</span><span class="sxs-lookup"><span data-stu-id="343be-122">Sample value</span></span>
------------------------|----------------|:------:|------------------------------------------------------|------------
<span data-ttu-id="343be-123">title</span><span class="sxs-lookup"><span data-stu-id="343be-123">title</span></span>                   |<span data-ttu-id="343be-124">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="343be-124">ILocalizedString</span></span>|<span data-ttu-id="343be-125">ja</span><span class="sxs-lookup"><span data-stu-id="343be-125">yes</span></span>     |<span data-ttu-id="343be-126">Der Webparttitel, der in der Toolbox angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="343be-126">The web part title that is displayed in the toolbox.</span></span>              |`"title": { "default": "Weather", "nl-nl": "Weerbericht" }`
<span data-ttu-id="343be-127">description</span><span class="sxs-lookup"><span data-stu-id="343be-127">description</span></span>             |<span data-ttu-id="343be-128">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="343be-128">ILocalizedString</span></span>|<span data-ttu-id="343be-129">ja</span><span class="sxs-lookup"><span data-stu-id="343be-129">yes</span></span>     |<span data-ttu-id="343be-130">Die Webpartbeschreibung, die in den Toolbox-QuickInfos angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="343be-130">The web part description that is displayed in the toolbox tooltips.</span></span>|`"description": { "default": "Shows weather in the given location", "nl-nl": "Toont weerbericht voor de opgegeven locatie" } `
<span data-ttu-id="343be-131">officeFabricIconFontName</span><span class="sxs-lookup"><span data-stu-id="343be-131">officeFabricIconFontName</span></span>|<span data-ttu-id="343be-132">string</span><span class="sxs-lookup"><span data-stu-id="343be-132">string</span></span>          |<span data-ttu-id="343be-133">nein</span><span class="sxs-lookup"><span data-stu-id="343be-133">no</span></span>      |<span data-ttu-id="343be-p105">Das Symbol für das Webpart, das in der Toolbox angezeigt wird. Dessen Wert muss einer der [Office UI Fabric-Symbolnamen](https://dev.office.com/fabric#/styles/icons) sein. Wenn diese Eigenschaft einen Wert hat, wird die **iconImageUrl**-Eigenschaft ignoriert.</span><span class="sxs-lookup"><span data-stu-id="343be-p105">The icon for the web part that is displayed in the toolbox. Its value must be one of the [Office UI Fabric icon names](https://dev.office.com/fabric#/styles/icons). If this property has a value, the **iconImageUrl** property will be ignored.</span></span>|`"officeFabricIconFontName": "Sunny"`
<span data-ttu-id="343be-137">iconImageUrl</span><span class="sxs-lookup"><span data-stu-id="343be-137">iconImageUrl</span></span>            |<span data-ttu-id="343be-138">string</span><span class="sxs-lookup"><span data-stu-id="343be-138">string</span></span>          |<span data-ttu-id="343be-139">nein</span><span class="sxs-lookup"><span data-stu-id="343be-139">no</span></span>      |<span data-ttu-id="343be-p106">Das Symbol für das Webpart, das in der Toolbox angezeigt und von einer Bild-URL dargestellt wird. Das Bild an der URL muss genau 40x28 px sein. Wenn die **officeFabricIconName**-Eigenschaft nicht über einen Wert verfügt, muss diese Eigenschaft einen Wert aufweisen.</span><span class="sxs-lookup"><span data-stu-id="343be-p106">The icon for the web part that is displayed in the toolbox and is represented by an image URL. The image at the URL must be exactly 40 x 28 px. If the **officeFabricIconName** property does not have a value, this property must have a value.</span></span>|`"iconImageUrl": "https://cdn.contoso.com/weather.png"`
<span data-ttu-id="343be-143">groupId</span><span class="sxs-lookup"><span data-stu-id="343be-143">groupId</span></span>                 |<span data-ttu-id="343be-144">string</span><span class="sxs-lookup"><span data-stu-id="343be-144">string</span></span>          |<span data-ttu-id="343be-145">ja</span><span class="sxs-lookup"><span data-stu-id="343be-145">yes</span></span>     |<span data-ttu-id="343be-p107">Die Gruppen-ID bestimmt, welche Toolboxgruppe das Webpart enthalten soll. Das SharePoint Framework reserviert Gruppen-IDs für Standardgruppen. Der Entwickler kann eine dieser Gruppen auswählen. Wenn eine Gruppen-ID angegeben ist, wird die **group**-Eigenschaft ignoriert. Alternativ kann der Entwickler eine eindeutige ID und einen eindeutigen Gruppennamen auswählen. In der Toolbox wird das Webpart dann in seiner eigenen Gruppe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="343be-p107">The group id determines which toolbox group will contain the web part. The SharePoint Framework reserves group ids for default groups. The developer can pick one of those groups. If a group id is specified, then the **group** property will be ignored. Alternatively, the developer can pick a completely unique id and a group name. The toolbox will then show the web part in its own group.</span></span>|`"groupId": "6737645a-4443-4210-a70e-e5e2a219133a"`
<span data-ttu-id="343be-152">Gruppe</span><span class="sxs-lookup"><span data-stu-id="343be-152">group</span></span>                   |<span data-ttu-id="343be-153">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="343be-153">ILocalizedString</span></span>|<span data-ttu-id="343be-154">nein</span><span class="sxs-lookup"><span data-stu-id="343be-154">no</span></span>      |<span data-ttu-id="343be-p108">Der Name der Gruppe in der Toolbox, in der das Webpart angezeigt werden soll. Wenn kein Wert angegeben ist, wird das Webpart in der **Custom**-Gruppe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="343be-p108">The name of the group in the toolbox in which the web part will be displayed. If no value is provided, then the web part will be displayed in the **Custom** group.</span></span>|`"group": { "default": "Content", "nl-nl": "Inhoud" }`
<span data-ttu-id="343be-157">dataVersion</span><span class="sxs-lookup"><span data-stu-id="343be-157">dataVersion</span></span>             |<span data-ttu-id="343be-158">string</span><span class="sxs-lookup"><span data-stu-id="343be-158">string</span></span>          |<span data-ttu-id="343be-159">nein</span><span class="sxs-lookup"><span data-stu-id="343be-159">no</span></span>      |<span data-ttu-id="343be-p109">Verwenden Sie dieses Feld, um die Datenversion der vorkonfigurierten Daten anzugeben, die dem Webpart bereitgestellt werden. Beachten Sie, dass sich die Datenversion vom Versionsfeld im Manifest unterscheidet. Die Manifestversion wird zum Steuern der Versionsverwaltung des Webpartcodes verwendet, die Datenversion wird hingegen zum Steuern der Versionsverwaltung der serialisierten Daten des Webparts verwendet. Weitere Informationen finden Sie im dataVersion-Feld Ihres Webparts. Unterstützte Werte: MAJOR.MINOR Version.</span><span class="sxs-lookup"><span data-stu-id="343be-p109">Use this field to specify the data version of the pre-configured data provided to the web part. Note that data version is different from the version field in the manifest. The manifest version is used to control the versioning of the web part code, while data version is used to control the versioning of the serialized data of the web part. Refer to dataVersion field of your web part for more information. Supported values format: MAJOR.MINOR version</span></span>|`"dataVersion": "1.0"`
<span data-ttu-id="343be-165">properties</span><span class="sxs-lookup"><span data-stu-id="343be-165">properties</span></span>              |<span data-ttu-id="343be-166">TProperties</span><span class="sxs-lookup"><span data-stu-id="343be-166">TProperties</span></span>     |<span data-ttu-id="343be-167">ja</span><span class="sxs-lookup"><span data-stu-id="343be-167">yes</span></span>     |<span data-ttu-id="343be-168">Ein Schlüssel-Wert-Paarobjekt mit Standardwerten für Webparteigenschaften.</span><span class="sxs-lookup"><span data-stu-id="343be-168">A Key-value pair object with default values for web part properties.</span></span>|`"properties": { "location": "Redmond", "numberOfDays": 3, "showIcon": true }`

<span data-ttu-id="343be-169">Folgende vordefinierte Kategorien können für die `groupId`-Eigenschaft verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="343be-169">Out of the box Categories are following, which can be used for the `groupId` property.</span></span>

<span data-ttu-id="343be-170">Kategoriename</span><span class="sxs-lookup"><span data-stu-id="343be-170">Category Name</span></span> |<span data-ttu-id="343be-171">Guid</span><span class="sxs-lookup"><span data-stu-id="343be-171">Guid</span></span> |<span data-ttu-id="343be-172">Webpart-Auswahl zuordnen</span><span class="sxs-lookup"><span data-stu-id="343be-172">Map to web part picker</span></span> |<span data-ttu-id="343be-173">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="343be-173">Description</span></span>        
--- |--- |--- |---
<span data-ttu-id="343be-174">Text, Medien und Inhalt</span><span class="sxs-lookup"><span data-stu-id="343be-174">Text, media, and content</span></span> | `cf066440-0614-43d6-98ae-0b31cf14c7c3`| <span data-ttu-id="343be-175">Medien und Inhalt</span><span class="sxs-lookup"><span data-stu-id="343be-175">Media and Content</span></span>  |<span data-ttu-id="343be-176">Diese Kategorie enthält Webparts, die Text, Multimedia, Dokumente, Informationen aus dem Web und andere formatierte Inhalte anzeigen.</span><span class="sxs-lookup"><span data-stu-id="343be-176">This category includes web parts that display text, multi-media, documents, information from the web, and other rich content.</span></span>   
<span data-ttu-id="343be-177">Ermitteln</span><span class="sxs-lookup"><span data-stu-id="343be-177">Discover</span></span> | `1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489`| <span data-ttu-id="343be-178">Suche</span><span class="sxs-lookup"><span data-stu-id="343be-178">Discovery</span></span>  |<span data-ttu-id="343be-179">Diese Kategorie enthält Webparts, die Inhalte organisieren, gruppieren und filtern, um Benutzer bei der Suche nach Informationen zu helfen.</span><span class="sxs-lookup"><span data-stu-id="343be-179">This category includes web parts that organize, group, and filter content to help users discover information.</span></span> 
<span data-ttu-id="343be-180">Kommunikation und Zusammenarbeit</span><span class="sxs-lookup"><span data-stu-id="343be-180">Communication and collaboration</span></span> | `75e22ed5-fa14-4829-850a-c890608aca2d`| <span data-ttu-id="343be-181">Zusammenarbeit im sozialen Netzwerk</span><span class="sxs-lookup"><span data-stu-id="343be-181">Social Collaboration</span></span> |<span data-ttu-id="343be-182">Diese Kategorie enthält Webparts, die die gemeinsame Nutzung von Informationen, Teamarbeit und soziale Interaktionen vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="343be-182">This category includes web parts that facilitate information sharing, team work, and social interactions.</span></span>
<span data-ttu-id="343be-183">Planung und Durchführung</span><span class="sxs-lookup"><span data-stu-id="343be-183">Planning and process</span></span> | `1bc7927e-4a5e-4520-b540-71305c79c20a`| <span data-ttu-id="343be-184">Geschäftsdaten</span><span class="sxs-lookup"><span data-stu-id="343be-184">Business Data</span></span> | <span data-ttu-id="343be-185">Diese Kategorie enthält Webparts, die die Produktivität im Team durch Verwendung von Planungs- und Durchführungstools fördern.</span><span class="sxs-lookup"><span data-stu-id="343be-185">This category includes web parts that empower team productivity with the use of planning and process tools.</span></span> 
<span data-ttu-id="343be-186">Business und Intelligence</span><span class="sxs-lookup"><span data-stu-id="343be-186">Business and intelligence</span></span> | `4aca9e90-eff5-4fa1-bac7-728f5f157b66`| <span data-ttu-id="343be-187">Geschäftsdaten</span><span class="sxs-lookup"><span data-stu-id="343be-187">Business Data</span></span> | <span data-ttu-id="343be-188">Diese Kategorie enthält Webparts für das Nachverfolgen und Analysieren von Daten sowie für die Integration von geschäftlichen Abläufen in Seiten.</span><span class="sxs-lookup"><span data-stu-id="343be-188">This category includes web parts for tracking and analyzing data, and for integrating business flow with pages.</span></span> 
<span data-ttu-id="343be-189">Websitetools</span><span class="sxs-lookup"><span data-stu-id="343be-189">Site tools</span></span> | `070951d7-94da-4db8-b06e-9d581f1f55b1`| <span data-ttu-id="343be-190">Websitetools</span><span class="sxs-lookup"><span data-stu-id="343be-190">Site tools</span></span>  |<span data-ttu-id="343be-191">Diese Kategorie enthält Webparts für Websiteinformationen und -verwaltung.</span><span class="sxs-lookup"><span data-stu-id="343be-191">This category includes web parts for site information and management.</span></span> 
<span data-ttu-id="343be-192">Sonstiges</span><span class="sxs-lookup"><span data-stu-id="343be-192">Other</span></span> | `5c03119e-3074-46fd-976b-c60198311f70`| <span data-ttu-id="343be-193">Sonstige</span><span class="sxs-lookup"><span data-stu-id="343be-193">Others</span></span> | <span data-ttu-id="343be-194">Diese Kategorie enthält Webparts, die nicht in anderen Kategorien enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="343be-194">This category includes web parts not in other categories.</span></span>            

<span data-ttu-id="343be-p110">Einige Webparteigenschaften weisen einen Wert vom Typ **ILocalizedString** auf. Dieser Typ ist ein Schlüssel-Wert-Paarobjekt, mit dem Entwickler Zeichenfolgen für die unterschiedlichen Gebietsschemas angeben können. Mindestens ein Wert vom Typ **ILocalizedString** muss den **Standardwert** enthalten. Entwickler können optional die Übersetzungen dieses Werts in die unterschiedlichen Gebietsschemas bereitstellen, die ihr Webpart unterstützt. Wenn das Webpart auf einer Seite in einem Gebietsschema platziert wird, das nicht in der lokalisierten Zeichenfolge aufgeführt ist, wird stattdessen der Standardwert verwendet.</span><span class="sxs-lookup"><span data-stu-id="343be-p110">Some web part properties have a value of type **ILocalizedString**. This type is a key-value pair object that allows developers to specify strings for the different locales. At a minimum, a value of type **ILocalizedString** must contain the **default** value. Optionally developers can provide the translations of that value to the different locales that their web part supports. If the web part is placed on a page in a locale that isn't listed in the localized string, the default value is used instead.</span></span>

<span data-ttu-id="343be-200">Gültige **ILocalizedString**-Werte:</span><span class="sxs-lookup"><span data-stu-id="343be-200">Valid **ILocalizedString** values:</span></span>

```json
"title": {
  "default": "Weather",
  "nl-nl": "Weerbericht"
}
```

```json
"title": {
  "default": "Weather"
}
```

<span data-ttu-id="343be-201">Ein **ILocalizedString**-Wert, der nicht gültig ist, da der **default** -Schlüssel fehlt:</span><span class="sxs-lookup"><span data-stu-id="343be-201">A **ILocalizedString** value that is not valid because the **default** key is missing:</span></span>

```json
"title": {
  "en-us": "Weather"
}
```

## <a name="using-preconfigured-entries-in-web-parts"></a><span data-ttu-id="343be-202">Verwenden vorkonfigurierter Einträge in Webparts</span><span class="sxs-lookup"><span data-stu-id="343be-202">Using preconfigured entries in web parts</span></span>

<span data-ttu-id="343be-p111">Um anzuzeigen, wie Sie beim Erstellen von Webparts vorkonfigurierte Einträge verwenden können, erstellen Sie ein Beispiel-Katalog-Webpart. Benutzer können mithilfe mehrerer Eigenschaften dieses Webpart konfigurieren, um Elemente aus einer ausgewählten Liste auf eine bestimmte Weise anzuzeigen. Aus Platzgründen wird die eigentliche Implementierung der Webpartlogik ausgelassen, und Sie konzentrieren sich auf die Verwendung der **preconfiguredEntries**-Eigenschaft, um vorkonfigurierte Versionen des Katalog-Webparts bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="343be-p111">To see how you can use preconfigured entries when building web parts, you will build a sample gallery web part. Using several properties, users can configure this web part to show items from a selected list in a specific way. For brevity, you will omit the actual implementation of the web part logic and will focus on using the **preconfiguredEntries** property to provide preconfigured versions of the gallery web part.</span></span>

![Webparteigenschaftenbereich, in dem die unterschiedlichen Eigenschaften angezeigt werden, die Benutzer konfigurieren müssen, damit das Webpart funktioniert](../../../images/preconfiguredentries-needs-configuration.png)

### <a name="create-a-new-project"></a><span data-ttu-id="343be-207">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="343be-207">Create a new project</span></span>

<span data-ttu-id="343be-208">Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="343be-208">Start by creating a new folder for your project.</span></span>

```sh
md react-preconfiguredentries
```

<span data-ttu-id="343be-209">Wechseln Sie zum Projektordner.</span><span class="sxs-lookup"><span data-stu-id="343be-209">Go to the project folder.</span></span>

```sh
cd react-preconfiguredentries
```

<span data-ttu-id="343be-210">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="343be-210">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="343be-211">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="343be-211">When prompted, enter the following values:</span></span>

- <span data-ttu-id="343be-212">**react-preconfiguredentries** als Lösungsname</span><span class="sxs-lookup"><span data-stu-id="343be-212">**react-preconfiguredentries** as your solution name</span></span>
- <span data-ttu-id="343be-213">**Aktuellen Ordner verwenden** als Speicherort für die Dateien</span><span class="sxs-lookup"><span data-stu-id="343be-213">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="343be-214">**Katalog** als Name des Webparts</span><span class="sxs-lookup"><span data-stu-id="343be-214">**Gallery** as your web part name</span></span>
- <span data-ttu-id="343be-215">**Zeigt Elemente aus der ausgewählten Liste an** als Beschreibung Ihres Webparts</span><span class="sxs-lookup"><span data-stu-id="343be-215">**Shows items from the selected list** as your web part description</span></span>
- <span data-ttu-id="343be-216">**React** als Eintrittspunkt für die Webpart-Erstellung</span><span class="sxs-lookup"><span data-stu-id="343be-216">**React** as the starting point to build the web part</span></span>

![SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../images/preconfiguredentries-yeoman.png)

<span data-ttu-id="343be-218">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="343be-218">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="343be-219">Öffnen Sie dann den Projektordner im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="343be-219">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="343be-220">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="343be-220">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![SharePoint Framework-Projekt in Visual Studio Code](../../../images/preconfiguredentries-visual-studio-code.png)

### <a name="add-web-part-properties"></a><span data-ttu-id="343be-222">Hinzufügen von Webparteigenschaften</span><span class="sxs-lookup"><span data-stu-id="343be-222">Add web part properties</span></span>

<span data-ttu-id="343be-p113">Fügen Sie im Webpartmanifest Webparteigenschaften hinzu, damit Benutzer das Katalog-Webpart konfigurieren können. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ersetzen Sie den Abschnitt **Eigenschaften** durch den folgenden JSON-Code:</span><span class="sxs-lookup"><span data-stu-id="343be-p113">In the web part manifest, add web part properties so that users can configure the gallery web part. In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Replace the **properties** section with the following JSON:</span></span>

```json
{
  //...
  "preconfiguredEntries": [{
    //...
    "properties": {
      "listName": "",
      "order": "",
      "numberOfItems": 10,
      "style": ""
    }
  }]
}
```

<span data-ttu-id="343be-p114">Die **listName**-Eigenschaft gibt den Namen der Liste an, aus der Listenelemente angezeigt werden sollen. Die **order**-Eigenschaft gibt die Reihenfolge an, in der Elemente angezeigt werden sollen, z. B. chronologisch oder umgekehrt chronologisch. Die **numberOfItems**-Eigenschaft gibt an, wie viele Elemente angezeigt werden sollen. Die **style**-Eigenschaft gibt schließlich an, wie die Elemente angezeigt werden sollen, z. B. als Miniaturansichten, was beim Anzeigen von Bildern hilfreich sein kann, oder als Liste, was für Dokumente besser geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="343be-p114">The **listName** property specifies the name of the list from which list items should be displayed. The **order** property specifies the order in which items should be shown, that is chronological, or reverse chronological order. The **numberOfItems** property specifies how many items should be displayed. Finally, the **style** property specifies how the items should be displayed, such as thumbnails, which is useful for showing images, or as a list which is more suitable for documents.</span></span>

<span data-ttu-id="343be-p115">Webparteigenschaften, die im Manifest angegeben werden, müssen auch der Webparteigenschaften-Schnittstelle hinzugefügt werden. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/IGalleryWebPartProps.ts**. Ändern Sie deren Code in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p115">Web part properties specified in the manifest must also be added to the web part properties interface. In the code editor, open the **./src/webparts/gallery/IGalleryWebPartProps.ts** file. Change its code to:</span></span>

```ts
export interface IGalleryWebPartProps {
  listName: string;
  order: string;
  numberOfItems: number;
  style: string;
}
```

<span data-ttu-id="343be-p116">Beim Erstellen von clientseitigen SharePoint Framework-Webparts mithilfe von React müssen Sie nach dem Ändern der Webparteigenschaften-Schnittstelle die **render**-Methode des Webparts aktualisieren, die diese Schnittstelle verwendet, um eine Instanz der React-Hauptkomponente zu erstellen Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.ts**. Ändern Sie die **render**-Methode des Webparts in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p116">When building SharePoint Framework client-side web parts using React, after changing the web part properties interface, you need to update the web part's **render** method that uses that interface to create an instance of the main React component. In the code editor, open the **./src/webparts/gallery/GalleryWebPart.ts** file. Change the web part **render** method to:</span></span>

```ts
export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
  // ...
  public render(): void {
    const element: React.ReactElement<IGalleryProps> = React.createElement(Gallery, {
      listName: this.properties.listName,
      order: this.properties.order,
      numberOfItems: this.properties.numberOfItems,
      style: this.properties.style
    });

    ReactDom.render(element, this.domElement);
  }
  // ...
}
```

<span data-ttu-id="343be-p117">Aktualisieren Sie React-Hauptkomponente so, dass die Werte der Eigenschaften angezeigt werden. Wenn das Webpart nicht konfiguriert wurde, zeigen Sie den standardmäßigen Platzhalter für das Webpart an. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/components/Gallery.tsx**, und ändern Sie ihren Code in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p117">Update the main React component to display the values of the properties. If the web part hasn't been configured, show the standard web part placeholder. In the code editor, open the **./src/webparts/gallery/components/Gallery.tsx** file and change its code to:</span></span>

```ts
import * as React from 'react';
import styles from './Gallery.module.scss';
import { IGalleryProps } from './IGalleryProps';

export default class Gallery extends React.Component<IGalleryProps, void> {
  public render(): JSX.Element {
    if (this.needsConfiguration()) {
      return <div className="ms-Grid" style={{ color: "#666", backgroundColor: "#f4f4f4", padding: "80px 0", alignItems: "center", boxAlign: "center" }}>
        <div className="ms-Grid-row" style={{ color: "#333" }}>
          <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
          <div className="ms-Grid-col ms-u-sm12 ms-u-md6" style={{ height: "100%", whiteSpace: "nowrap", textAlign: "center" }}>
            <i className="ms-fontSize-su ms-Icon ms-Icon--ThumbnailView" style={{ display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}></i><span className="ms-fontWeight-light ms-fontSize-xxl" style={{ paddingLeft: "20px", display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}>Gallery</span>
          </div>
          <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
        </div>
        <div className="ms-Grid-row" style={{ width: "65%", verticalAlign: "middle", margin: "0 auto", textAlign: "center" }}>
          <span style={{ color: "#666", fontSize: "17px", display: "inline-block", margin: "24px 0", fontWeight: 100 }}>Show items from the selected list</span>
        </div>
        <div className="ms-Grid-row"></div>
      </div>;
    }
    else {
      return (
        <div className={styles.gallery}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className='ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1'>
                <span className="ms-font-xl ms-fontColor-white">
                  Welcome to SharePoint!
                </span>
                <p className='ms-font-l ms-fontColor-white'>
                  Customize SharePoint experiences using Web Parts.
                </p>
                <p className='ms-font-l ms-fontColor-white'>
                  List: {this.props.listName}<br />
                  Order: {this.props.order}<br />
                  Number of items: {this.props.numberOfItems}<br />
                  Style: {this.props.style}
                </p>
                <a href="https://aka.ms/spfx" className={styles.button}>
                  <span className={styles.label}>Learn more</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      );
    }
  }

  private needsConfiguration(): boolean {
    return Gallery.isEmpty(this.props.listName) ||
      Gallery.isEmpty(this.props.order) ||
      Gallery.isEmpty(this.props.style);
  }

  private static isEmpty(value: string): boolean {
    return value === undefined ||
      value === null ||
      value.length === 0;
  }
}
```

<span data-ttu-id="343be-p118">Aktualisieren Sie die Schnittstelle der zentralen React-Komponente so, dass sie der Schnittstelle der Webparteigenschaften entspricht. Dies ist nötig, da alle Webparteigenschaften an diese Komponente umgeleitet werden. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/components/IGalleryProps.ts**, und ändern Sie den Code wie folgt:</span><span class="sxs-lookup"><span data-stu-id="343be-p118">Update the main React component Interface to match on the web part property Interface, since we are bypassing all the web part properties to this component. In the code editor, open the **./src/webparts/gallery/components/IGalleryProps.ts** file and change its code to:</span></span>

```ts
import { IGalleryWebPartProps } from '../IGalleryWebPartProps';

export interface IGalleryProps extends IGalleryWebPartProps {
}
```

### <a name="render-web-part-properties-in-the-property-pane"></a><span data-ttu-id="343be-241">Rendern von Webparteigenschaften im Eigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="343be-241">Render web part properties in the property pane</span></span>

<span data-ttu-id="343be-p119">Damit Benutzer die neu definierten Eigenschaft verwenden können, um das Webpart zu konfigurieren, müssen die Eigenschaften im Webparteigenschaftenbereich angezeigt werden. Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/galleryWebPart.ts**. Ändern Sie im oberen Bereich der Datei die **@microsoft/sp-webpart-base**-Anweisung zum Importieren in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p119">For users to be able to use the newly defined properties to configure the web part, the properties must be displayed in the web part property pane. In the code editor, open the **./src/webparts/gallery/GalleryWebPart.ts** file. In the top section of the file change the **@microsoft/sp-webpart-base** import statement to:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneDropdown,
  PropertyPaneSlider,
  PropertyPaneChoiceGroup
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="343be-245">Aktualisieren Sie dann den Code des **propertyPaneSettings**-Getters auf Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-245">Next, change the **propertyPaneSettings** getter to:</span></span>

```ts
export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
  // ...
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneDropdown('listName', {
                  label: strings.ListNameFieldLabel,
                  options: [{
                    key: 'Documents',
                    text: 'Documents'
                  },
                  {
                    key: 'Images',
                    text: 'Images'
                  }]
                }),
                PropertyPaneChoiceGroup('order', {
                  label: strings.OrderFieldLabel,
                  options: [{
                    key: 'chronological',
                    text: strings.OrderFieldChronologicalOptionLabel
                  },
                  {
                    key: 'reversed',
                    text: strings.OrderFieldReversedOptionLabel
                  }]
                }),
                PropertyPaneSlider('numberOfItems', {
                  label: strings.NumberOfItemsFieldLabel,
                  min: 1,
                  max: 10,
                  step: 1
                }),
                PropertyPaneChoiceGroup('style', {
                  label: strings.StyleFieldLabel,
                  options: [{
                    key: 'thumbnails',
                    text: strings.StyleFieldThumbnailsOptionLabel
                  },
                  {
                    key: 'list',
                    text: strings.StyleFieldListOptionLabel
                  }]
                })
              ]
            }
          ]
        }
      ]
    };
  }
}
```

<span data-ttu-id="343be-p120">In einem realen Szenario würden Sie die Liste von Elementen von der aktuellen SharePoint-Website abrufen. Aus Platzgründen verwenden Sie in diesem Beispiel stattdessen eine feste Liste.</span><span class="sxs-lookup"><span data-stu-id="343be-p120">In a real-life scenario, you would retrieve the list of lists from the current SharePoint site. For brevity, in this example you use a fixed list instead.</span></span>

### <a name="add-localization-labels"></a><span data-ttu-id="343be-248">Hinzufügen von Lokalisierungsbezeichnungen</span><span class="sxs-lookup"><span data-stu-id="343be-248">Add localization labels</span></span>

<span data-ttu-id="343be-p121">Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/loc/mystrings.d.ts**. Ändern Sie deren Code in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p121">In the code editor, open the **./src/webparts/gallery/loc/mystrings.d.ts** file. Change its code to:</span></span>

```ts
declare interface IGalleryStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
  OrderFieldLabel: string;
  OrderFieldChronologicalOptionLabel: string;
  OrderFieldReversedOptionLabel: string;
  NumberOfItemsFieldLabel: string;
  StyleFieldLabel: string;
  StyleFieldThumbnailsOptionLabel: string;
  StyleFieldListOptionLabel: string;
}

declare module 'galleryStrings' {
  const strings: IGalleryStrings;
  export = strings;
}
```

<span data-ttu-id="343be-251">Fügen Sie die fehlenden Ressourcenzeichenfolgen hinzu, indem Sie im Code-Editor die Datei **./src/webparts/gallery/loc/en-us.js** öffnen und ihren Code in Folgendes ändern:</span><span class="sxs-lookup"><span data-stu-id="343be-251">Add the missing resource strings by opening in the code editor the **./src/webparts/gallery/loc/en-us.js** file and changing its code to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ListNameFieldLabel": "List",
    "OrderFieldLabel": "Items order",
    "OrderFieldChronologicalOptionLabel": "chronological",
    "OrderFieldReversedOptionLabel": "reversed chronological",
    "NumberOfItemsFieldLabel": "Number of items to show",
    "StyleFieldLabel": "Items display style",
    "StyleFieldThumbnailsOptionLabel": "thumbnails",
    "StyleFieldListOptionLabel": "list"
  }
});
```

<span data-ttu-id="343be-252">Stellen Sie sicher, dass das Projekt erstellt wird, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="343be-252">Confirm that the project is building by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="343be-p122">Fügen Sie im Webbrowser das Webpart zum Zeichenbereich hinzu, und öffnen Sie dessen Eigenschaftenbereich. Sie sollten alle Eigenschaften sehen, die von Benutzern konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="343be-p122">In the web browser add the web part to the canvas and open its property pane. You should see all properties available for users to configure.</span></span>

![Webparteigenschaftenbereich, in dem die unterschiedlichen Eigenschaften angezeigt werden, die Benutzer konfigurieren müssen, damit das Webpart funktioniert](../../../images/preconfiguredentries-needs-configuration.png)

<span data-ttu-id="343be-p123">Da Sie für das Webpart keine Standardwerte angegeben haben, müssen Benutzer jedes Mal, wenn sie das Webpart der Seite hinzufügen, dieses zuerst konfigurieren. Sie können dies vereinfachen, indem Sie für die häufigsten Szenarien Standardwerte angeben.</span><span class="sxs-lookup"><span data-stu-id="343be-p123">Because you didn't specify any default values for the web part, every time users add the web part to the page they have to configure it first. You can simplify this experience by providing default values for the most common scenarios.</span></span>

### <a name="specify-default-values-for-the-web-part"></a><span data-ttu-id="343be-258">Angeben von Standardwerten für das Webpart</span><span class="sxs-lookup"><span data-stu-id="343be-258">Specify default values for the web part</span></span>

<span data-ttu-id="343be-p124">Stellen Sie sich vor, dass Benutzer häufig das Katalog-Webpart verwenden, um die fünf zuletzt hinzugefügten Bilder anzuzeigen. Anstatt zu verlangen, dass Benutzer das Webpart jedes Mal manuell konfigurieren, könnten Sie ihnen eine vorkonfigurierte Version mit korrekten Einstellungen bereitstellen. </span><span class="sxs-lookup"><span data-stu-id="343be-p124">Imagine that users often use the gallery web part to show the five most recently added images. Rather than requiring users to configure the web part each time manually, you could provide them with a preconfigured version using correct settings.</span></span>

<span data-ttu-id="343be-p125">Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie den vorhandenen Eintrag in der **preconfiguredEntries**-Eigenschaft in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p125">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the existing entry in the **preconfiguredEntries** property to:</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent images" },
    "description": { "default": "Shows 5 most recent images" },
    "officeFabricIconFontName": "Picture",
    "properties": {
      "listName": "Images",
      "order": "reversed",
      "numberOfItems": 5,
      "style": "thumbnails"
    }
  }]
}
```

<span data-ttu-id="343be-263">Starten Sie das Debuggen des Projekts, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="343be-263">Start debugging the project by running the following command:</span></span>

```sh
gulp serve
```

> <span data-ttu-id="343be-p126">**Hinweis**: Wenn Sie das Projekt zuvor bereits gedebuggt haben, stoppen Sie das Debuggen, und starten Sie es erneut. Änderungen, die am Webpartmanifest vorgenommen wurden, werden beim Debuggen nicht automatisch in der Workbench widergespiegelt, und Sie müssen das Projekt neu erstellen, um diese zu sehen.</span><span class="sxs-lookup"><span data-stu-id="343be-p126">**Note**: If you were debugging the project previously, stop debugging and start it again. Changes made to the web part manifest are not automatically reflected in the workbench while debugging, and you have to rebuild the project in order to see them.</span></span>

<span data-ttu-id="343be-266">Wenn Sie die Webpart-Toolbox öffnen, um das Webpart zum Zeichenbereich hinzuzufügen, werden Sie sehen, dass sich der Name und das Symbol geändert haben und nun die vorkonfigurierten Einstellungen widerspiegeln.</span><span class="sxs-lookup"><span data-stu-id="343be-266">When you open the web part toolbox to add the web part to the canvas, you will see that its name and icon changed to reflect the preconfigured settings.</span></span>

![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-recent-images-toolbox.png)

<span data-ttu-id="343be-268">Nach dem Hinzufügen des Webparts zu der Seite funktioniert dieses sofort mit den vorkonfigurierten Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="343be-268">After adding the web part to the page, it works immediately using the preconfigured settings.</span></span>

![Vorkonfiguriertes Webpart, das sofort funktioniert, nachdem es der Seite hinzugefügt wurde](../../../images/preconfiguredentries-recent-images-canvas.png)

### <a name="specify-multiple-preconfigured-web-part-entries"></a><span data-ttu-id="343be-270">Eingeben mehrerer vorkonfigurierter Webparteinträge</span><span class="sxs-lookup"><span data-stu-id="343be-270">Specify multiple preconfigured web part entries</span></span>

<span data-ttu-id="343be-p127">Stellen Sie sich vor, dass eine andere Gruppe von Benutzern häufig Ihr Katalog-Webpart verwendet, um Dokumente anzuzeigen, die kürzlich ihrer Website hinzugefügt wurden. Damit diese Ihr Webpart verwenden können, können Sie einen weiteren Satz von Voreinstellungen hinzufügen, die deren Konfigurationsanforderungen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="343be-p127">Imagine that another group of users often uses your gallery web part to show documents recently added to their site. To help them use your web part, you can add another set of presets that addresses their configuration needs.</span></span>

<span data-ttu-id="343be-p128">Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie die **preconfiguredEntries**-Eigenschaft in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p128">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the **preconfiguredEntries** property to:</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent images" },
    "description": { "default": "Shows 5 most recent images" },
    "officeFabricIconFontName": "Picture",
    "properties": {
      "listName": "Images",
      "order": "reversed",
      "numberOfItems": 5,
      "style": "thumbnails"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent documents" },
    "description": { "default": "Shows 10 most recent documents" },
    "officeFabricIconFontName": "Documentation",
    "properties": {
      "listName": "Documents",
      "order": "reversed",
      "numberOfItems": 10,
      "style": "list"
    }
  }]
}
```

<span data-ttu-id="343be-275">Beachten Sie, dass der zuvor vorkonfigurierte Eintrag intakt bleibt und Sie einen weiteren Eintrag daneben unter Verwendung anderer Werte für Eigenschaften hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="343be-275">Notice how you keep the previous preconfigured entry intact and add another one beside it using different values for properties.</span></span>

<span data-ttu-id="343be-276">Um das Ergebnis zu sehen, starten Sie das Debuggen des Projekts, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="343be-276">To see the result start debugging the project by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="343be-277">Wenn Sie die Webpart-Toolbox öffnen, um das Webpart dem Zeichenbereich hinzuzufügen, werden Sie sehen, dass es zwei Webparts gibt, aus denen Sie auswählen können.</span><span class="sxs-lookup"><span data-stu-id="343be-277">When you open the web part toolbox to add the web part to the canvas, you will see that there are two web parts for you to choose from.</span></span>

![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-multiple-web-parts-toolbox.png)

<span data-ttu-id="343be-279">Nach dem Hinzufügen des Webparts **Zuletzt verwendete Dokumente** zu der Seite verwendet dieses sofort die spezifischen vorkonfigurierten Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="343be-279">After adding the **Recent documents** web part to the page, it works immediately using its specific preconfigured settings.</span></span>

![Vorkonfiguriertes Webpart für zuletzt verwendete Dokumente, das sofort funktioniert, nachdem es der Seite hinzugefügt wurde](../../../images/preconfiguredentries-recent-documents-canvas.png)

### <a name="specify-an-unconfigured-instance-of-the-web-part"></a><span data-ttu-id="343be-281">Angeben einer nicht konfigurierten Instanz des Webparts</span><span class="sxs-lookup"><span data-stu-id="343be-281">Specify an unconfigured instance of the web part</span></span>

<span data-ttu-id="343be-p129">Beim Erstellen von Webparts gibt es häufig spezielle Szenarien, die das Webpart unterstützen sollte. Das Bereitstellen vorkonfigurierter Einträge für diese Szenarien erleichtert Benutzern die Verwendung des Webparts.</span><span class="sxs-lookup"><span data-stu-id="343be-p129">When building web parts there are often specific scenarios that the web part should support. Providing preconfigured entries for those scenarios makes it easier for users to use the web part.</span></span>

<span data-ttu-id="343be-p130">Je nachdem, wie Sie das Webpart erstellen, könnte das Webpart möglicherweise auch andere unvorhergesehene Szenarien unterstützen. Wenn Sie nur bestimmte vorkonfigurierte Einträge bereitstellen, ist für Benutzer möglicherweise nicht klar, dass sie Ihr Webpart für ein anderes Szenario verwenden können. Es bietet sich an, auch eine allgemeine, nicht konfigurierte Variante Ihres Webparts bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="343be-p130">Depending how you build your web part, it could be possible that the web part can support other unforeseen scenarios as well. If you only provide specific preconfigured entries, users might not realize they can use your web part for a different scenario. It might be a good idea to provide a generic unconfigured variant of your web part as well.</span></span>

<span data-ttu-id="343be-p131">Öffnen Sie im Code-Editor die Datei **./src/webparts/gallery/GalleryWebPart.manifest.json**. Ändern Sie die **preconfiguredEntries**-Eigenschaft in Folgendes:</span><span class="sxs-lookup"><span data-stu-id="343be-p131">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the **preconfiguredEntries** property to:</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent images" },
    "description": { "default": "Shows 5 most recent images" },
    "officeFabricIconFontName": "Picture",
    "properties": {
      "listName": "Images",
      "order": "reversed",
      "numberOfItems": 5,
      "style": "thumbnails"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent documents" },
    "description": { "default": "Shows 10 most recent documents" },
    "officeFabricIconFontName": "Documentation",
    "properties": {
      "listName": "Documents",
      "order": "reversed",
      "numberOfItems": 10,
      "style": "list"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "CustomList",
    "properties": {
      "listName": "",
      "order": "",
      "numberOfItems": 5,
      "style": ""
    }
  }]
}
```

<span data-ttu-id="343be-p132">Die allgemeine, nicht konfigurierte Version des Webparts wird zusätzlich zu den Konfigurationen hinzugefügt, die auf bestimmte Szenarien abzielen. Wenn es keine spezifische Konfiguration gibt, die auf die Anforderungen der Benutzer abzielt, können diese so die allgemeine Version verwenden und diese gemäß ihren Anforderungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="343be-p132">The generic unconfigured version of the web part is added beside the configurations that target specific scenarios. This way, if there is no specific configuration addressing users' needs, they can always use the generic version and configure it according to their requirements.</span></span>

<span data-ttu-id="343be-291">Um das Ergebnis zu sehen, starten Sie das Debuggen des Projekts, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="343be-291">To see the result start debugging the project by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="343be-292">Wenn Sie die Webpart-Toolbox öffnen, um das Webpart dem Zeichenbereich hinzuzufügen, werden Sie sehen, dass es nun drei Webparts gibt, aus denen Benutzer auswählen können.</span><span class="sxs-lookup"><span data-stu-id="343be-292">When you open the web part toolbox to add the web part to the canvas, you will see that there are now three web parts that users can choose from.</span></span>

![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../images/preconfiguredentries-three-configurations-toolbox.png)