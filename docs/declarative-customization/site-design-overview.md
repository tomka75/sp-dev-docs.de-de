---
title: "Übersicht über das SharePoint-Websitedesign und -Websiteskripts"
description: Verwenden Sie SharePoint-Websiteskripts und -Websitedesigns, um die Bereitstellung neuer SharePoint-Websites mit neuen Konfigurationen zu automatisieren.
ms.date: 12/14/2017
ms.openlocfilehash: 5821c4a48ecccbfc23ff5eaaf1c7941c6026d06e
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="sharepoint-site-design-and-site-script-overview"></a><span data-ttu-id="607c4-103">Übersicht über das SharePoint-Websitedesign und -Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="607c4-103">SharePoint site design and site script overview</span></span>

> [!NOTE]
> <span data-ttu-id="607c4-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="607c4-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="607c4-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="607c4-106">Verwenden Sie Websiteskripts und Websitedesigns, um die Bereitstellung neuer SharePoint-Websites mit Ihren eigenen benutzerdefinierten Konfigurationen zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="607c4-106">Use site designs and site scripts to automate provisioning new SharePoint sites using your own custom configurations.</span></span> <span data-ttu-id="607c4-107">Wenn Personen in Ihrem Unternehmen neue SharePoint-Websites erstellen, müssen Sie häufig ein gewisses Maß an Konsistenz sicherstellen.</span><span class="sxs-lookup"><span data-stu-id="607c4-107">When people in your organization create new SharePoint sites, you often need to ensure some level of consistency.</span></span> <span data-ttu-id="607c4-108">Vielleicht benötigen Sie für jede neue Website ein entsprechendes Branding und passende Designs.</span><span class="sxs-lookup"><span data-stu-id="607c4-108">For example, you may need proper branding and theming applied to each new site.</span></span> <span data-ttu-id="607c4-109">Vielleicht haben Sie auch detaillierte Bereitstellungsskripts, z. B. die Verwendung des PnP-Bereitstellungsmoduls, die immer dann angewendet werden müssen, wenn eine neue Website erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="607c4-109">You may also have detailed site provisioning scripts, such as using the PnP provisioning engine, that need to be applied each time a new site is created.</span></span> <span data-ttu-id="607c4-110">In diesem Artikel wird beschrieben, wie Sie Websitedesigns und Websiteskripts verwenden können, um benutzerdefinierte Konfigurationen bereitzustellen, die angewendet werden, wenn neue Websites erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-110">This article describes how you can use site designs and site scripts to provide custom configurations to apply when new sites are created.</span></span>

## <a name="how-site-designs-work"></a><span data-ttu-id="607c4-111">Funktionsweise von Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="607c4-111">How site designs work</span></span>

<span data-ttu-id="607c4-112">Websitedesigns sind wie eine Vorlage.</span><span class="sxs-lookup"><span data-stu-id="607c4-112">Site designs are like a template.</span></span> <span data-ttu-id="607c4-113">Sie können immer dann verwendet werden, wenn eine neue Website erstellt wird, um einen konsistenten Satz von Aktionen anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="607c4-113">They can be used each time a new site is created to apply a consistent set of actions.</span></span> <span data-ttu-id="607c4-114">Die meisten Aktionen betreffen in der Regel die Website selbst, z. B. das Festlegen des Designs oder das Erstellen von Listen.</span><span class="sxs-lookup"><span data-stu-id="607c4-114">Most actions typically affect the site itself, such as setting the theme, or creating lists.</span></span> <span data-ttu-id="607c4-115">Ein Websitedesign kann jedoch auch andere Aktionen umfassen, z. B. das Aufzeichnen der URL der neuen Website in einem Protokoll oder das Senden eines Tweets.</span><span class="sxs-lookup"><span data-stu-id="607c4-115">But a site design can also include other actions, such as recording the new site URL to a log, or sending a tweet.</span></span>

<span data-ttu-id="607c4-116">Websitedesigns werden in SharePoint auf einer der modernen Vorlagenwebsites erstellt und registriert: auf der Teamwebsite oder auf der Kommunikationswebsite.</span><span class="sxs-lookup"><span data-stu-id="607c4-116">You create site designs and register them in SharePoint to one of the modern template sites: the team site, or communication site.</span></span> <span data-ttu-id="607c4-117">In den folgenden Schritten können Sie sehen, wie dies funktioniert.</span><span class="sxs-lookup"><span data-stu-id="607c4-117">You can see how this works in the following steps.</span></span>

1. <span data-ttu-id="607c4-118">Gehen Sie in Ihrem Entwicklermandanten auf die SharePoint-Startseite.</span><span class="sxs-lookup"><span data-stu-id="607c4-118">Go to the SharePoint home page on your developer tenant.</span></span>
1. <span data-ttu-id="607c4-119">Wählen Sie **Website erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="607c4-119">Choose **Create site**.</span></span>

    <span data-ttu-id="607c4-120">Sie sehen die beiden modernen Vorlagenwebsites: die **Teamwebsite** und **Kommunikationswebsite**.</span><span class="sxs-lookup"><span data-stu-id="607c4-120">You'll see the two modern template sites: **Team site**, and **Communication site**.</span></span>

1. <span data-ttu-id="607c4-121">Wählen Sie **Kommunikationswebsite** aus.</span><span class="sxs-lookup"><span data-stu-id="607c4-121">Choose **Communication site**.</span></span>

    <span data-ttu-id="607c4-122">Die Kommunikationswebsite weist das Feld **Design auswählen**, in dem die folgenden Websitedesigs zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="607c4-122">The communication site has a **Choose a design** box in which comes with the following site designs.</span></span>

    - <span data-ttu-id="607c4-123">Thema</span><span class="sxs-lookup"><span data-stu-id="607c4-123">Topic</span></span>
    - <span data-ttu-id="607c4-124">Showcase</span><span class="sxs-lookup"><span data-stu-id="607c4-124">Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span></span>
    - <span data-ttu-id="607c4-125">Leer</span><span class="sxs-lookup"><span data-stu-id="607c4-125">Blank</span></span>

<span data-ttu-id="607c4-126">Dies sind die standardmäßigen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="607c4-126">These are the default site designs.</span></span> <span data-ttu-id="607c4-127">Jedes Websitedesign weist einen Titel, eine Beschreibung und ein Bild auf.</span><span class="sxs-lookup"><span data-stu-id="607c4-127">For each site design there is a title, description, and image.</span></span>

![Titel, Beschreibung und Bild im standardmäßigen Websitedesign in der Kommunikationswebsite-Vorlage](images/site-designs-listed-on-communication-site-template.png)

<span data-ttu-id="607c4-129">Wenn Sie die Vorlage für die Teamwebsite ausgewählt hätten, würde diese nur das standardmäßige Websitedesign mit dem Namen **Teamwebsite** enthalten.</span><span class="sxs-lookup"><span data-stu-id="607c4-129">Had you chosen the team site template, it contains only one default site design named **Team site**.</span></span> <span data-ttu-id="607c4-130">Weitere Informationen dazu, wie Sie die standardmäßigen Websitedesigns ändern können, finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="607c4-130">For additional information on how you can change the default site designs, see [Customize a default site design](customize-default-site-design.md).</span></span>

<span data-ttu-id="607c4-131">Nachdem ein Websitedesign ausgewählt wurde, erstellt SharePoint die neue Website und führt Websiteskripts für das Websitedesign aus.</span><span class="sxs-lookup"><span data-stu-id="607c4-131">Once a site design is selected, SharePoint creates the new site, and runs site scripts for the site design.</span></span> <span data-ttu-id="607c4-132">In den Websiteskripts ist die Arbeit wie z. B. das Erstellen neuer Listen oder das Anwenden eines Designs aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="607c4-132">The site scripts detail the work such as creating new lists, or applying a theme.</span></span> <span data-ttu-id="607c4-133">Wenn die Aktionen in den Skripts abgeschlossen sind, zeigt SharePoint die ausführlichen Ergebnisse dieser Aktionen in einer Statusanzeige an.</span><span class="sxs-lookup"><span data-stu-id="607c4-133">When the actions in the scripts are completed, SharePoint displays detailed results of those actions in a progress pane.</span></span>

![Statusanzeige, in der die abgeschlossenen Aktionen in einem Websitedesign aufgeführt sind](images/progress-pane.png)

## <a name="anatomy-of-a-site-script"></a><span data-ttu-id="607c4-135">Anatomie eines Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="607c4-135">Anatomy of a site script</span></span>

<span data-ttu-id="607c4-136">Bei Websiteskripts handelt es sich um JSON-Dateien, die eine sortierte Liste von Aktionen angeben, die beim Erstellen der neuen Website ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-136">Site scripts are JSON files that specify an ordered list of actions to run when creating the new site.</span></span> <span data-ttu-id="607c4-137">Die Aktionen werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="607c4-137">The actions are run in the order listed.</span></span> <span data-ttu-id="607c4-138">Das folgende Beispiel ist ein Skript, das über zwei Aktionen auf oberster Ebene verfügt.</span><span class="sxs-lookup"><span data-stu-id="607c4-138">The following example is a script that has two top-level actions.</span></span> <span data-ttu-id="607c4-139">Zuerst wird ein Design angewendet, das zuvor mit dem Namen **Contoso Explorers** erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="607c4-139">First it applies a theme that was previously created named **Contoso Explorers**.</span></span> <span data-ttu-id="607c4-140">Anschließend wird die Liste **Kundennachverfolgung** erstellt.</span><span class="sxs-lookup"><span data-stu-id="607c4-140">Then it creates a **Customer Tracking** list.</span></span>

```json
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
}
```

<span data-ttu-id="607c4-141">Jede Aktion in einem Websiteskript wird vom Wert **verb** im JSON-Skript angegeben.</span><span class="sxs-lookup"><span data-stu-id="607c4-141">Each action in a site script is specified by a **verb** value in the JSON.</span></span> <span data-ttu-id="607c4-142">Im vorherigen Skript wird die erste Aktion vom Verb **applyTheme** angegeben.</span><span class="sxs-lookup"><span data-stu-id="607c4-142">In the previous script the first action is specified by the **applyTheme** verb.</span></span> <span data-ttu-id="607c4-143">Dann erstellt das Verb **createSPList** die Liste.</span><span class="sxs-lookup"><span data-stu-id="607c4-143">Then the **createSPList** verb creates the list.</span></span> <span data-ttu-id="607c4-144">Beachten Sie, dass das Verb **createSPList** seinen eigenen Satz von Verben enthält, die zusätzliche Aktionen nur für die Liste ausführen.</span><span class="sxs-lookup"><span data-stu-id="607c4-144">Notice that the **createSPList** verb contains its own set of verbs which run additional actions on just the list.</span></span>

<span data-ttu-id="607c4-145">Verfügbare Aktionen umfassen:</span><span class="sxs-lookup"><span data-stu-id="607c4-145">Available actions include:</span></span>

- <span data-ttu-id="607c4-146">Erstellen einer neuen Liste</span><span class="sxs-lookup"><span data-stu-id="607c4-146">Creating a new list</span></span>
- <span data-ttu-id="607c4-147">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="607c4-147">Applying a theme</span></span>
- <span data-ttu-id="607c4-148">Erstellen einer Seite</span><span class="sxs-lookup"><span data-stu-id="607c4-148">Creating a simple page using REST</span></span>
- <span data-ttu-id="607c4-149">Festlegen eines Websitelogos</span><span class="sxs-lookup"><span data-stu-id="607c4-149">Setting a site logo</span></span>
- <span data-ttu-id="607c4-150">Hinzufügen einer Nagivation</span><span class="sxs-lookup"><span data-stu-id="607c4-150">Adding navigation</span></span>
- <span data-ttu-id="607c4-151">Auslösen eines Microsoft-Flusses</span><span class="sxs-lookup"><span data-stu-id="607c4-151">Triggering a Microsoft flow</span></span>

<span data-ttu-id="607c4-152">Websiteskripts können nach der Bereitstellung erneut auf derselben Website ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-152">Site scripts can be run again on the same site after provisioning.</span></span> <span data-ttu-id="607c4-153">Dies kann nur programmgesteuert erfolgen.</span><span class="sxs-lookup"><span data-stu-id="607c4-153">This can only be done programmatically.</span></span> <span data-ttu-id="607c4-154">Websiteskripts sind nicht destruktiv, wenn sie also erneut ausgeführt werden, wird sichergestellt, dass die Website der Konfiguration im Skript entspricht.</span><span class="sxs-lookup"><span data-stu-id="607c4-154">Site scripts are non-destructive, so when they run again, they ensure that the site matches the configuration in the script.</span></span> <span data-ttu-id="607c4-155">Wenn die Website beispielsweise bereits eine Liste mit demselben Namen aufweist, den das Websiteskript erstellt, fügt das Websiteskripts nur fehlende Felder zu der vorhandenen Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="607c4-155">For example, if the site already has a list with the same name that the site script is creating, the site script will only add missing fields to the existing list.</span></span>

## <a name="using-powershell-or-rest-to-work-with-site-designs-and-site-scripts"></a><span data-ttu-id="607c4-156">Verwenden von PowerShell oder REST zum Arbeiten mit Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="607c4-156">Using PowerShell or REST to work with site designs and site scripts</span></span>

<span data-ttu-id="607c4-157">Sie können Websitedesigns und Websiteskripts mithilfe von PowerShell oder der REST-API erstellen.</span><span class="sxs-lookup"><span data-stu-id="607c4-157">You can create site designs and site scripts by using PowerShell, or the REST API.</span></span> <span data-ttu-id="607c4-158">Im folgenden Beispiel wird ein Websiteskript und ein Websitedesign erstellt, das das Websiteskript verwendet.</span><span class="sxs-lookup"><span data-stu-id="607c4-158">The following example creates a site script and a site design that uses the site script.</span></span> <!-- The PowerShell example loads the script from a file, while the REST example has the script inline. -->

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' `
     -Raw | `
     Add-SPOSiteScript `
    -Title "Contoso theme and list"

Id          : 2756067f-d818-4933-a514-2a2b2c50fb06
Title       : Contoso theme and list
Description :
Content     :
Version     : 0

C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "2756067f-d818-4933-a514-2a2b2c50fb06" `
  -Description "Creates customer list and applies standard theme"
```

<!-- 
```javascript
var site_script = {
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='Contoso theme and list'", site_script);

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking", Description:"Creates customer list and applies standard theme",  SiteScriptIds:["607aed52-6d61-490a-b692-c0f58a6981a1"],  WebTemplate:"64"
   }
  });
```
-->

<span data-ttu-id="607c4-159">Im vorherigen Beispiel gibt das Cmdlet **Add-SPOSiteScript** oder die REST-API **CreateSiteScript** eine Websiteskript-ID zurück. Diese wird für den Parameter **SiteScripts** im nachfolgenden Aufruf des Cmdlets **Add-SPO-SiteDesign** oder der REST-API **CreateSiteDesign** verwendet.</span><span class="sxs-lookup"><span data-stu-id="607c4-159">In the previous example, the **Add-SPOSiteScript** cmdlet, or **CreateSiteScript** REST API returns a site script id. This is used for the **SiteScripts** parameter in the subsequent call to the **Add-SPO-SiteDesign** cmdlet, or **CreateSiteDesign** REST API.</span></span>

<span data-ttu-id="607c4-160">Der auf den Wert „64“ festgelegte Parameter **WebTemplate** gibt an, dass das Websitedesign bei der Teamwebsitevorlage registriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="607c4-160">The **WebTemplate** parameter set to the value 64 indicates to register this site design with the team site template.</span></span> <span data-ttu-id="607c4-161">Der Wert „68“ würde auf die Kommunikationswebsitevorlage hinweisen.</span><span class="sxs-lookup"><span data-stu-id="607c4-161">The value 68 would indicate the communication site template.</span></span> <span data-ttu-id="607c4-162">Die Parameter **Title** und **Description** werden angezeigt, wenn ein Benutzer Websitedesigns beim Erstellen einer neuen Teamwebsite ansieht.</span><span class="sxs-lookup"><span data-stu-id="607c4-162">The **Title** and **Description** parameters will be displayed when a user views site designs as they create a new team site.</span></span>

> [!NOTE]
> <span data-ttu-id="607c4-163">Ein Websitedesign kann mehrere Skripts ausführen.</span><span class="sxs-lookup"><span data-stu-id="607c4-163">A site design can run multiple scripts.</span></span> <span data-ttu-id="607c4-164">Die Skript-IDs werden in einem Array übergeben und werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="607c4-164">The script IDs are passed in an array, and they will run in the order listed.</span></span>

<span data-ttu-id="607c4-165">Schrittweise Anweisungen zum Erstellen eines Websitedesigns finden Sie unter [Erste Schritte mit dem Erstellen von Websitedesigns](get-started-create-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="607c4-165">For step-by-step information on creating a site design, see [Get started creating site designs](get-started-create-site-design.md)</span></span>

## <a name="pnp-provisioning-and-customization-using-microsoft-flow"></a><span data-ttu-id="607c4-166">PnP-Bereitstellung und Anpassung mithilfe von Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="607c4-166">PnP Provisioning and customization using Microsoft Flow</span></span>

<span data-ttu-id="607c4-167">Eine von Websiteskripts bereitgestellte Aktion ist die Möglichkeit, einen Microsoft-Fluss auszulösen.</span><span class="sxs-lookup"><span data-stu-id="607c4-167">One action provided by site scripts is the ability to trigger a Microsoft flow.</span></span> <span data-ttu-id="607c4-168">Auf diese Weise können Sie beliebige benutzerdefinierte Aktionen angeben, die Sie über die systemeigen in Websiteskripts bereitgestellten Aktionen benötigen.</span><span class="sxs-lookup"><span data-stu-id="607c4-168">This allows you to specify any custom action you need beyond the actions provided natively in site scripts.</span></span>

<span data-ttu-id="607c4-169">Wenn Sie das PnP-Bereitstellungsmodul zum Automatisieren der Websiteerstellung verwenden, können Sie einen Microsoft Flow zur Integration in Websitedesigns verwenden.</span><span class="sxs-lookup"><span data-stu-id="607c4-169">If you use the PnP provisioning engine to automate site creation, then you can use a Microsoft flow to integrate with site designs.</span></span> <span data-ttu-id="607c4-170">Mithilfe dieser Technik können Sie alle vorhandenen Bereitstellungsskripts beibehalten und auch neue benutzerdefinierte Bereitstellungsskripts erstellen.</span><span class="sxs-lookup"><span data-stu-id="607c4-170">You can maintain all of your existing provisioning scripts as well as create new custom provisioning scripts using this technique.</span></span>

![Prozess des Auslösens eines Microsoft-Flusses](images/process-for-triggering-a-custom-flow.png)

<span data-ttu-id="607c4-172">Dieser Prozess funktioniert folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="607c4-172">The process works as follows:</span></span>

1. <span data-ttu-id="607c4-173">Das Skript instanziiert Ihren Microsoft-Fluss mithilfe einer URL mit zusätzlichen Details.</span><span class="sxs-lookup"><span data-stu-id="607c4-173">The script instantiates your Microsoft flow using a URL with additional details.</span></span>
1. <span data-ttu-id="607c4-174">Der Flow sendet eine Nachricht an die Azure-Speicherwarteschlage, die Sie konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="607c4-174">The flow sends a message to an Azure storage queue that you have configured.</span></span>
1. <span data-ttu-id="607c4-175">Die Nachricht löst einen Aufruf einer Azure-Funktion aus, die Sie konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="607c4-175">The message triggers a call to an Azure function that you have configured.</span></span>
1. <span data-ttu-id="607c4-176">Die Azure-Funktion führt Ihr benutzerdefiniertes Skript aus, z. B. das PnP-Bereitstellungsmoduls, um Ihre benutzerdefinierten Konfigurationen anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="607c4-176">The Azure function runs your custom script, such as the PnP provisioning engine, to apply your custom configurations.</span></span>

<span data-ttu-id="607c4-177">Ein schrittweises Lernprogramm zum Konfigurieren Ihres eigenen Microsoft-Flusses mit der PnP-Bereitstellung finden Sie unter [Erstellen eines vollständigen Websitedesigns mithilfe des PnP-Bereitstellungsmoduls](site-design-pnp-provisioning.md)</span><span class="sxs-lookup"><span data-stu-id="607c4-177">For a step-by-step tutorial on how to configure your own Microsoft flow with PnP provisioning, see [Build a complete site design using the PnP provisioning engine](site-design-pnp-provisioning.md)</span></span>

## <a name="scoping"></a><span data-ttu-id="607c4-178">Bereichsdefinition</span><span class="sxs-lookup"><span data-stu-id="607c4-178">Scoping</span></span>

<span data-ttu-id="607c4-179">Sie können Websitedesigns so konfigurieren, dass sie nur für bestimmte Gruppen oder Personen in Ihrer Organisation angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-179">You can configure site designs to only appear for specific groups or people in your organization.</span></span> <span data-ttu-id="607c4-180">Dies ist hilfreich, um sicherzustellen, dass Personen nur die für sie beabsichtigten Websitedesigns sehen.</span><span class="sxs-lookup"><span data-stu-id="607c4-180">This is useful to ensure that people only see the site designs intended for them.</span></span> <span data-ttu-id="607c4-181">Vielleicht möchten Sie, dass die Buchhaltungsabteilung nur Websitedesigns sieht, die für sie gedacht sind.</span><span class="sxs-lookup"><span data-stu-id="607c4-181">For example, you may want the accounting department to only see site designs specifically for them.</span></span> <span data-ttu-id="607c4-182">Und die Websitedesigns der Buchhaltung sind möglicherweise für andere Personen nicht sinnvoll.</span><span class="sxs-lookup"><span data-stu-id="607c4-182">And the accounting site designs may not make sense to show to anyone else.</span></span>

<span data-ttu-id="607c4-183">Ein Websitedesign kann standardmäßig bei Erstellung von jeder Person angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-183">By default a site design can be viewed by everyone when it is created.</span></span> <span data-ttu-id="607c4-184">Bereiche werden mit dem Cmdlet **Grant-SPOSiteDesignRights** oder der REST-API **GrantSiteDesignRights** angewendet.</span><span class="sxs-lookup"><span data-stu-id="607c4-184">Scopes are applied by using the **Grant-SPOSiteDesignRights** cmdlet, or the **GrantSiteDesignRights** REST API.</span></span>  <span data-ttu-id="607c4-185">Sie können den Bereich nach Benutzer oder nach einer E-Mail-aktivierten Sicherheitsgruppe angeben.</span><span class="sxs-lookup"><span data-stu-id="607c4-185">You can specify the scope by user, or a mail-enabled security group.</span></span> <span data-ttu-id="607c4-186">Im folgenden Beispiel wird gezeigt, wie Anzeigeberechtigungen für einen Nestor (ein Benutzer auf der fiktiven Contoso-Website) in einem Websitedesign hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="607c4-186">The following example shows how to add Nestor (a user at the fictional Contoso site) view rights on a site design.</span></span>

> [!div class="tabbedCodeSnippets"]
```powershell
Grant-SPOSiteDesignRights `
  -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
  -Principals "nestorw@contoso.onmicrosoft.com" `
  -Rights View
```

<!--
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"44252d09-62c4-4913-9eb0-a2a8b8d7f863", principalNames:["nestorw@contoso.onmicrosoft.com”], grantedRights:1});
```
-->
<span data-ttu-id="607c4-187">Weitere Informationen zum Arbeiten mit Bereichen finden Sie unter [Bereichsdefinition für den Zugriff auf Websitedesigns](site-design-scoping.md).</span><span class="sxs-lookup"><span data-stu-id="607c4-187">For more information on working with scopes, see [Scoping access to site designs](site-design-scoping.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="607c4-188">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="607c4-188">See also</span></span>

- [<span data-ttu-id="607c4-189">Erste Schritte mit dem Erstellen von Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="607c4-189">Get started creating site designs</span></span>](get-started-create-site-design.md)
- [<span data-ttu-id="607c4-190">Anwenden eines Bereichs auf Ihr Websitedesign</span><span class="sxs-lookup"><span data-stu-id="607c4-190">Apply a scope to your site design</span></span>](site-design-scoping.md)
- [<span data-ttu-id="607c4-191">JSON-Schema eines Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="607c4-191">Site design JSON schema</span></span>](site-design-json-schema.md)
- [<span data-ttu-id="607c4-192">PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="607c4-192">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>](site-design-powershell.md)
- [<span data-ttu-id="607c4-193">REST-API von Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="607c4-193">Site design and site script REST API</span></span>](site-design-rest-api.md)
- <span data-ttu-id="607c4-194">[Beispiele für die Websitedesign]((https://github.com/SharePoint/sp-dev-site-scripts))</span><span class="sxs-lookup"><span data-stu-id="607c4-194">[Site design examples]((https://github.com/SharePoint/sp-dev-site-scripts))</span></span>