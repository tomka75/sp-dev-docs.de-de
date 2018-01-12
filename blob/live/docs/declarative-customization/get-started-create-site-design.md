---
title: Erste Schritte mit dem Erstellen von SharePoint-Websitedesigns und -Websiteskripts
description: Erste Schritte mit dem Erstellen von SharePoint-Websitedesigns und -Websiteskripts, aus denen Benutzer ihre eigenen Websites erstellen.
ms.date: 12/14/2017
ms.openlocfilehash: 81879d169c9f82aed3e93bf2eda598dacc184b5f
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="get-started-creating-site-designs-and-site-scripts"></a><span data-ttu-id="c1e22-103">Erste Schritte mit dem Erstellen von Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="c1e22-103">Get started creating site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="c1e22-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="c1e22-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="c1e22-106">Erstellen Sie Websitedesigns, um wiederverwendbare Listen, Designs, Layouts, Seiten oder benutzerdefinierte Aktionen bereitzustellen, damit Ihre Benutzer schnell neue SharePoint-Websites mit den benötigten Features erstellen können.</span><span class="sxs-lookup"><span data-stu-id="c1e22-106">Build site designs to provide reusable lists, themes, layouts, pages, or custom actions so that your users can quickly build new SharePoint sites with the features they need.</span></span> <span data-ttu-id="c1e22-107">In diesem Artikel erstellen Sie ein einfaches Websitedesign, das eine SharePoint-Liste zum Nachverfolgen von Kundenbestellungen hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-107">In this article you'll build a simple site design that adds a SharePoint list for tracking customer orders.</span></span> <span data-ttu-id="c1e22-108">Sie verwenden dann das Websitedesign, um eine neue SharePoint-Website mit der benutzerdefinierten Liste zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1e22-108">Then you'll use the site design to create a new SharePoint site with the custom list.</span></span>

<span data-ttu-id="c1e22-109">In diesem Artikel wird gezeigt, wie Sie PowerShell-Cmdlets in SharePoint zum Erstellen von Websiteskripts und Websitedesigns verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-109">This article shows how to use SharePoint PowerShell cmdlets to create site scripts and site designs.</span></span> <span data-ttu-id="c1e22-110">Sie können auch REST-API für dieselben Aktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-110">You can also use REST APIs to perform the same actions.</span></span> <span data-ttu-id="c1e22-111">Die entsprechenden REST-Aufrufe sind zur Referenz in jedem Schritt dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-111">The corresponding REST calls are shown for reference in each step.</span></span>

## <a name="create-the-site-script-in-json"></a><span data-ttu-id="c1e22-112">Erstellen des Websiteskripts in JSON</span><span class="sxs-lookup"><span data-stu-id="c1e22-112">Create the site script in JSON</span></span>

<span data-ttu-id="c1e22-113">Ein Websitedesign ist eine Sammlung von Aktionen, die SharePoint beim Erstellen einer neuen Website ausführt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-113">A site design is a collection of actions that SharePoint will run when creating a new site.</span></span> <span data-ttu-id="c1e22-114">Aktionen beschreiben Änderungen, die auf die neue Website angewendet werden sollen, z. B. das Erstellen einer neuen Liste oder das Anwenden eines Designs.</span><span class="sxs-lookup"><span data-stu-id="c1e22-114">Actions describe changes to apply to the new site, such as creating a new list, or applying a theme.</span></span> <span data-ttu-id="c1e22-115">Die Aktionen werden in einem JSON-Skript angegeben.</span><span class="sxs-lookup"><span data-stu-id="c1e22-115">The actions are specified in a JSON script.</span></span> <span data-ttu-id="c1e22-116">Das JSON-Skript ist eine Liste aller anzuwendenden Aktionen.</span><span class="sxs-lookup"><span data-stu-id="c1e22-116">The JSON script is a list of all actions to apply.</span></span> <span data-ttu-id="c1e22-117">Wenn ein Skript ausgeführt wird, schließt SharePoint jede Aktion in der aufgeführten Reihenfolge ab.</span><span class="sxs-lookup"><span data-stu-id="c1e22-117">When a script runs, SharePoint completes each action in the order listed.</span></span>

<span data-ttu-id="c1e22-118">Jede Aktion wird vom Wert „verb“ im JSON-Skript angegeben.</span><span class="sxs-lookup"><span data-stu-id="c1e22-118">Each action is specified by the "verb" value in the JSON script.</span></span> <span data-ttu-id="c1e22-119">Aktionen können auch Unteraktionen aufweisen, die auch „verb“-Werte sind.</span><span class="sxs-lookup"><span data-stu-id="c1e22-119">Also, actions can have subactions which are also "verb" values.</span></span> <span data-ttu-id="c1e22-120">Im folgenden JSON-Code gibt das Skript an, dass eine neue Liste mit dem Namen „Kundenverfolgung“ erstellt werden sollen; Unteraktionen legen dann die Beschreibung fest und fügen mehrere Felder zum Definieren der Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="c1e22-120">In the JSON below, the script specifies to create a new list named Customer Tracking, and then subactions set the description and add several fields to define the list.</span></span>

1. <span data-ttu-id="c1e22-121">Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="c1e22-121">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="c1e22-122">Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.</span><span class="sxs-lookup"><span data-stu-id="c1e22-122">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="c1e22-123">Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell]((https://technet.microsoft.com/de-DE/library/fp161372.aspx)).</span><span class="sxs-lookup"><span data-stu-id="c1e22-123">Follow the instructions at [Connect to SharePoint Online PowerShell]((https://technet.microsoft.com/de-DE/library/fp161372.aspx)) to connect to your SharePoint tenant.</span></span>
1. <span data-ttu-id="c1e22-124">Weisen Sie den JSON-Code, der das neue Skript beschreibt, einer Variablen zu, wie im folgenden PowerShell-Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-124">Create and assign the JSON that describes the new script to a variable as shown in the PowerShell code below.</span></span>

```powershell
$site_script = @'
{
    "$schema": "schema.json",
        "actions": [
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
'@
```

<span data-ttu-id="c1e22-125">Das vorherige Skript erstellt eine neue SharePoint-Liste mit dem Namen „Kundenverfolgung“.</span><span class="sxs-lookup"><span data-stu-id="c1e22-125">The previous script will create a new SharePoint list named Customer Tracking.</span></span> <span data-ttu-id="c1e22-126">Es legt die Beschreibung fest und fügt der Liste auch vier weitere Felder hinzu.</span><span class="sxs-lookup"><span data-stu-id="c1e22-126">It will set the description, and also add four fields to the list.</span></span>

## <a name="add-the-site-script"></a><span data-ttu-id="c1e22-127">Hinzufügen des Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="c1e22-127">Add the site script</span></span>

<span data-ttu-id="c1e22-128">Jedes Websiteskript muss in SharePoint registriert werden, damit es verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="c1e22-128">Each site script must be registered in SharePoint so that it is available to.</span></span> <span data-ttu-id="c1e22-129">Fügen Sie ein neues Websitedesign mithilfe des Cmdlets **Add-SPOSiteScript** hinzu.</span><span class="sxs-lookup"><span data-stu-id="c1e22-129">Add a new site design by using the **Add-SPOSiteScript** cmdlet.</span></span> <span data-ttu-id="c1e22-130">Im folgenden Beispiel wird gezeigt, wie das zuvor beschriebene JSON-Skript hinzugefügt wird. </span><span class="sxs-lookup"><span data-stu-id="c1e22-130">The following example shows how to add the JSON script described previously.</span></span>

```powershell
C:\> Add-SPOSiteScript -Title "Create customer tracking list" -Content $site_script -Description "Creates list for tracking customer contact information"
```

<span data-ttu-id="c1e22-131">Nach dem Ausführen des Cmdlets erhalten Sie ein Ergebnis, in dem die Websiteskript-**ID** des hinzugefügten Skripts aufgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c1e22-131">After running the cmdlet you will get a result that lists the site script **ID** of the added script.</span></span> <span data-ttu-id="c1e22-132">Notieren Sie sich diese ID, denn Sie werden sie später benötigen, wenn Sie das Websitedesign erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1e22-132">Keep track of this ID somewhere because you will need it later when you create the site design.</span></span>

<span data-ttu-id="c1e22-133">Die REST-API, die dem neuen Websiteskript hinzugefügt wird, ist **CreateSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="c1e22-133">The REST API to add a new site script is **CreateSiteScript**.</span></span>

## <a name="create-the-site-design"></a><span data-ttu-id="c1e22-134">Erstellen des Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="c1e22-134">Create the site design</span></span>

<span data-ttu-id="c1e22-135">Als Nächstes müssen Sie das Websitedesign erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1e22-135">Next you need to create the site design.</span></span> <span data-ttu-id="c1e22-136">Das Websitedesign wird in einer Dropdownliste angezeigt, wenn jemand eine neue Website aus einer der Vorlagen erstellt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-136">The site design will appear in a drop down list when someone creates a new site from one of the templates.</span></span> <span data-ttu-id="c1e22-137">Es kann ein oder mehrere Websiteskripts ausführen, die bereits hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-137">It can run one or more site scripts that have already been added.</span></span>

- <span data-ttu-id="c1e22-138">Führen Sie das folgende Cmdlet aus, um ein neues Websitedesign hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c1e22-138">Run the following cmdlet to add a new site design.</span></span> <span data-ttu-id="c1e22-139">Ersetzen Sie \<ID\> durch die Websiteskript-ID beim Hinzufügen des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="c1e22-139">Replace \<ID\> with the site script ID from when you added the site script.</span></span>

```powershell
C:\> Add-SPOSiteDesign -Title "Contoso customer tracking" -WebTemplate "64" -SiteScripts "<ID>" -Description "Tracks key customer data in a list"
```

<span data-ttu-id="c1e22-140">Das vorherige Cmdlet erstellt ein neues Websitedesign mit dem Namen „Contoso-Kundenverfolgung“.</span><span class="sxs-lookup"><span data-stu-id="c1e22-140">The previous cmdlet creates a new site design named Contoso customer tracking.</span></span> <span data-ttu-id="c1e22-141">Durch den Wert „-WebTemplate“ wird ausgewählt, welche Basisvorlage verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="c1e22-141">The -WebTemplate value selects which base template to associate with.</span></span> <span data-ttu-id="c1e22-142">Der Wert „64“ gibt die Teamwebsite-Vorlage an, der Wert „68“ gibt die Kommunikationswebsitevorlage an.</span><span class="sxs-lookup"><span data-stu-id="c1e22-142">The value "64" indicates Team site template, and the value "68" indicates the communication site template.</span></span>

<span data-ttu-id="c1e22-143">In der JSON-Antwort wird die **ID** des neuen Websitedesigns angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-143">The JSON response will display the **ID** of the new site design.</span></span> <span data-ttu-id="c1e22-144">Sie können diese in nachfolgenden Cmdlets verwenden, um das Websitedesign zu aktualisieren oder zu ändern.</span><span class="sxs-lookup"><span data-stu-id="c1e22-144">You can use in subsequent cmdlets to update or modify the site design.</span></span>

<span data-ttu-id="c1e22-145">Die REST-API, die dem neuen Websiteskript hinzugefügt wird, ist **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="c1e22-145">The REST API to add a new site design is **CreateSiteDesign**.</span></span>

## <a name="use-the-new-site-design"></a><span data-ttu-id="c1e22-146">Verwenden des neuen Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="c1e22-146">Use the new site design</span></span>

<span data-ttu-id="c1e22-147">Da Sie nun ein Websiteskript und ein Websitedesign hinzugefügt haben, können Sie diese zum Erstellen neuer Websites verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-147">Now that you've added a site script and site design, you can use it to create new sites.</span></span>

1. <span data-ttu-id="c1e22-148">Gehen Sie zur Startseite der SharePoint-Website, die Sie für die Entwicklung verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1e22-148">Go to the home page of the SharePoint site you are using for development.</span></span>
1. <span data-ttu-id="c1e22-149">Wählen Sie **Website erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c1e22-149">Choose **Create site**.</span></span>
1. <span data-ttu-id="c1e22-150">Wählen Sie **Teamwebsite** aus.</span><span class="sxs-lookup"><span data-stu-id="c1e22-150">Choose **Team site**.</span></span>
1. <span data-ttu-id="c1e22-151">Wählen Sie in der Dropdownliste **Design auswählen** Ihr Websitedesign **Kundenbestellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="c1e22-151">In the **Choose a design** drop down, select your site design **customer orders**.</span></span>
1. <span data-ttu-id="c1e22-152">Geben Sie unter „Websitename“ einen Namen für die neue Website **Kundenauftragsverfolgung** ein.</span><span class="sxs-lookup"><span data-stu-id="c1e22-152">In Site name enter a name for the new site **Customer order tracking**.</span></span>
1. <span data-ttu-id="c1e22-153">Wählen Sie **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="c1e22-153">Choose **Next**.</span></span>
1. <span data-ttu-id="c1e22-154">Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c1e22-154">Choose **Finish**.</span></span>
1. <span data-ttu-id="c1e22-155">In einem Bereich wird angegeben, dass Ihr Skript angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="c1e22-155">A pane will indicate that your script is being applied.</span></span> <span data-ttu-id="c1e22-156">Wenn dieser Vorgang abgeschlossen ist, wählen Sie **Aktualisierte Website anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="c1e22-156">When it is done, choose **View updated site**.</span></span>
1. <span data-ttu-id="c1e22-157">Die benutzerdefinierte Liste wird auf der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c1e22-157">You will see the custom list on the page.</span></span>
