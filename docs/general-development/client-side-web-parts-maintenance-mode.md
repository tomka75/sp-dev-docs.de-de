---
title: "Wartungsmodus für clientseitige Webparts"
ms.date: 12/18/2017
ms.prod: sharepoint
ms.assetid: 3ebd2a11-8291-4228-add0-9e0cd899dd3c
ms.openlocfilehash: 208a9ef5fea879fa7d27811595ebc8d37881d3b2
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="maintenance-mode-for-client-side-web-parts"></a><span data-ttu-id="146a8-102">Wartungsmodus für clientseitige Webparts</span><span class="sxs-lookup"><span data-stu-id="146a8-102">Maintenance mode for client-side web parts</span></span>

<span data-ttu-id="146a8-103">_**Gilt für:** Office 365_</span><span class="sxs-lookup"><span data-stu-id="146a8-103">\*Applies to: Office 365</span></span>

<span data-ttu-id="146a8-104">Wenn Sie mit clientseitigen Webparts arbeiten, können Sie diese im Wartungsmodus laden.</span><span class="sxs-lookup"><span data-stu-id="146a8-104">When working with client-side web parts, you can load them in maintenance mode.</span></span> <span data-ttu-id="146a8-105">Der Wartungsmodus kann hilfreich sein, wenn Sie versuchen, Probleme im Zusammenhang mit Webparts auf der Seite zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="146a8-105">The maintenance mode can be helpful when trying to debug issues related to web parts placed on the page.</span></span>

## <a name="switch-to-maintenance-mode"></a><span data-ttu-id="146a8-106">Wechseln in den Wartungsmodus</span><span class="sxs-lookup"><span data-stu-id="146a8-106">Switch to maintenance mode</span></span>

> [!NOTE]
> <span data-ttu-id="146a8-107">Um eine Seite im Wartungsmodus zu laden, benötigen Sie Bearbeitungsberechtigungen für diese spezielle Seite.</span><span class="sxs-lookup"><span data-stu-id="146a8-107">In order to load a page in the maintenance mode, you have to have edit permissions for that specific page.</span></span>

<span data-ttu-id="146a8-108">Navigieren Sie zu der Seite, und fügen Sie in der URL `?maintenancemode=true` an, um zum Wartungsmodus zu wechseln. Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="146a8-108">To switch to the maintenance mode, navigate to the page and in the URL append `?maintenancemode=true`, for example:</span></span>

```text
https://contoso.sharepoint.com/sites/team?maintenancemode=true
```

<span data-ttu-id="146a8-109">Um den Wartungsmodus zu verlassen, entfernen Sie `?maintenancemode=true` aus der URL, und laden Sie die Seite erneut.</span><span class="sxs-lookup"><span data-stu-id="146a8-109">To leave the maintenance mode, remove `?maintenancemode=true` from the URL and reload the page.</span></span>

## <a name="available-information"></a><span data-ttu-id="146a8-110">Verfügbare Informationen</span><span class="sxs-lookup"><span data-stu-id="146a8-110">Available information</span></span>

<span data-ttu-id="146a8-111">Im Wartungsmodus werden unterschiedliche Informationen zu jedem Webpart auf der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="146a8-111">The maintenance mode shows various information about each web part on the page.</span></span>

### <a name="web-part-summary"></a><span data-ttu-id="146a8-112">Webpart-Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="146a8-112">Web part summary</span></span>

<span data-ttu-id="146a8-113">Wenn Sie sich im Wartungsmodus befinden, wird für jedes Webpart die folgende Zusammenfassung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="146a8-113">When in maintenance mode, for each web part you will see the following summary information:</span></span>

![Zusammenfassende Webpartinformationen, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-summary.png)

<span data-ttu-id="146a8-115">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="146a8-115">Property</span></span>|<span data-ttu-id="146a8-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="146a8-116">Description</span></span>
--------|-----------
<span data-ttu-id="146a8-117">Alias</span><span class="sxs-lookup"><span data-stu-id="146a8-117">Alias</span></span>|<span data-ttu-id="146a8-118">Webpart-Alias</span><span class="sxs-lookup"><span data-stu-id="146a8-118">Web part alias</span></span>
<span data-ttu-id="146a8-119">Id</span><span class="sxs-lookup"><span data-stu-id="146a8-119">Id</span></span>|<span data-ttu-id="146a8-120">Die eindeutige ID des Webparts.</span><span class="sxs-lookup"><span data-stu-id="146a8-120">The unique ID of the web part</span></span>
<span data-ttu-id="146a8-121">InstanceID</span><span class="sxs-lookup"><span data-stu-id="146a8-121">InstanceID</span></span>|<span data-ttu-id="146a8-122">Die ID einer bestimmten Instanz eines Webparts (wenn auf einer Seite zwei oder mehr gleiche Webparts vorhanden sind, weisen diese jeweils dieselbe Webpart-ID auf, haben jedoch eine andere Instanz-ID).</span><span class="sxs-lookup"><span data-stu-id="146a8-122">The ID of a specific instance of a web part (that is, if you have two more of the same web parts on a page, they will each have the same web part ID, but a different instance ID.</span></span>
<span data-ttu-id="146a8-123">IsInternal</span><span class="sxs-lookup"><span data-stu-id="146a8-123">IsInternal</span></span>|<span data-ttu-id="146a8-124">Gibt an, ob das Webpart von Microsoft oder von einem Drittanbieter erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="146a8-124">Indicates whether the web part was made by Microsoft or a third party.</span></span> <span data-ttu-id="146a8-125">Bei `true` wurde das Webpart von Microsoft erstellt.</span><span class="sxs-lookup"><span data-stu-id="146a8-125">If `true`, it is made by Microsoft.</span></span> <span data-ttu-id="146a8-126">Bei `false` wurde das Webpart von einem Drittanbieter erstellt.</span><span class="sxs-lookup"><span data-stu-id="146a8-126">If `false`, it is made by a third party.</span></span>
<span data-ttu-id="146a8-127">Version</span><span class="sxs-lookup"><span data-stu-id="146a8-127">Version</span></span>|<span data-ttu-id="146a8-128">Die Versionsnummer des Webparts.</span><span class="sxs-lookup"><span data-stu-id="146a8-128">The version number of the web part.</span></span>
<span data-ttu-id="146a8-129">Umgebung</span><span class="sxs-lookup"><span data-stu-id="146a8-129">Environment</span></span>|<span data-ttu-id="146a8-130">Eine Aufzählung, die die Umgebung angibt, in der das Webpart ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="146a8-130">Enumeration indicating the environment on which the web part is running.</span></span> <span data-ttu-id="146a8-131">Mögliche Werte: `1` - Lokale Workbench, `2` - SharePoint</span><span class="sxs-lookup"><span data-stu-id="146a8-131">Possible values: `1` - Local Workbench, `2` - SharePoint</span></span>
<span data-ttu-id="146a8-132">UserAgent</span><span class="sxs-lookup"><span data-stu-id="146a8-132">UserAgent</span></span>|<span data-ttu-id="146a8-133">Eine Zeichenfolge, die Informationen zu dem verwendeten Gerät und zu der verwendeten Software enthält (z. B. Browsertyp und Version).</span><span class="sxs-lookup"><span data-stu-id="146a8-133">A string that contains information about the device and software in use (such as browser type and version).</span></span>

### <a name="web-part-manifest"></a><span data-ttu-id="146a8-134">Webpart-Manifest</span><span class="sxs-lookup"><span data-stu-id="146a8-134">Web part manifest</span></span>

<span data-ttu-id="146a8-135">Wechseln Sie zur Registerkarte **Manifest**, um weitere Informationen zu dem Webpart zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="146a8-135">To get more information about the web part, switch to the **Manifest** tab.</span></span>

![Webpart-Manifestinformationen, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-manifest.png)

<span data-ttu-id="146a8-137">Wenn Sie sich die Manifestinformationen näher ansehen, erhalten Sie Details über Folgendes:</span><span class="sxs-lookup"><span data-stu-id="146a8-137">By exploring the manifest information, you can learn details such as:</span></span>

- <span data-ttu-id="146a8-138">Wo das Webpart-Bundle gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="146a8-138">where the web part bundle is hosted</span></span>
- <span data-ttu-id="146a8-139">Welche externen Skripts das Webpart lädt und von wo.</span><span class="sxs-lookup"><span data-stu-id="146a8-139">which external scripts is the web part loading and from where</span></span>
- <span data-ttu-id="146a8-140">Auf welcher Version von SharePoint Framework das Webpart basiert.</span><span class="sxs-lookup"><span data-stu-id="146a8-140">what version of the SharePoint Framework has the web part been built on</span></span>
- <span data-ttu-id="146a8-141">Welche Komponenten von SharePoint Framework das Webpart verwendet.</span><span class="sxs-lookup"><span data-stu-id="146a8-141">which components of the SharePoint Framework does the web part use</span></span>

<span data-ttu-id="146a8-142">Diese Informationen können hilfreich sein, wenn Sie herausfinden möchten, warum ein bestimmtes Webpart nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="146a8-142">This information can be invaluable when trying to find a reason why the particular web part is malfunctioning.</span></span>

### <a name="web-part-data"></a><span data-ttu-id="146a8-143">Webpartdaten</span><span class="sxs-lookup"><span data-stu-id="146a8-143">Web part data</span></span>

<span data-ttu-id="146a8-144">Weitere Angaben, die im Wartungsmodus verfügbar sind, sind die Webpartdaten.</span><span class="sxs-lookup"><span data-stu-id="146a8-144">Another piece of information available in the maintenance mode, is web part data.</span></span>

![Webpartdaten, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-data.png)

<span data-ttu-id="146a8-146">Anhand der Informationen der Registerkarte **Daten** können Sie die Konfiguration jedes Webparts ermitteln.</span><span class="sxs-lookup"><span data-stu-id="146a8-146">Using the information from the **Data** tab, you can see the configuration for each web part.</span></span> <span data-ttu-id="146a8-147">Dies ist hilfreich, wenn Sie versuchen, Fehler zu reproduzieren, die von Benutzern gemeldet wurden, die von der Konfiguration eines bestimmten Webparts verursacht worden sein könnten.</span><span class="sxs-lookup"><span data-stu-id="146a8-147">This is helpful when trying to reproduce errors reported by users which could be caused by a specific web part configuration.</span></span>

<span data-ttu-id="146a8-148">Wenn [die Eigenschaften des Webparts in SharePoint integriert sind](../spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint.md), werden im Datenabschnitt die Typen und Werte angezeigt, die zur weiteren Verarbeitung an SharePoint übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="146a8-148">If the web part [integrates its properties with SharePoint](../spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint.md), the data section shows the types and values that are passed to SharePoint for further processing.</span></span>

## <a name="considerations"></a><span data-ttu-id="146a8-149">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="146a8-149">Considerations</span></span>

- <span data-ttu-id="146a8-150">Der Wartungsmodus eignet sich für clientseitige Webparts  auf modernen und klassischen SharePoint-Seiten.</span><span class="sxs-lookup"><span data-stu-id="146a8-150">the maintenance mode works for client-side web parts placed on both modern and classic SharePoint pages.</span></span> <span data-ttu-id="146a8-151">Im Supportartikel [Öffnen und Verwenden der Webpart-Wartungsseite]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2)#PickTab=2016,_2013) erhalten Sie weitere Informationen zum Öffnen von klassischen Webparts in der Wartungsansicht.</span><span class="sxs-lookup"><span data-stu-id="146a8-151">See the [Open and use the web part maintenance page]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2)#PickTab=2016,_2013) support article, to get more information about opening classic web parts in maintenance view</span></span>
- <span data-ttu-id="146a8-152">Um eine Seite im Wartungsmodus zu öffnen, benötigen Sie Bearbeitungsberechtigungen für diese spezielle Seite.</span><span class="sxs-lookup"><span data-stu-id="146a8-152">to open page in maintenance mode, you have to have edit permissions for that page</span></span>
- <span data-ttu-id="146a8-153">Während Sie sich im Wartungsmodus befinden, wird der Code des Webparts nicht ausgeführt, und die Webparteigenschaften können nicht bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="146a8-153">when in maintenance mode, web part code is not being executed and you cannot edit web part properties</span></span>
- <span data-ttu-id="146a8-154">Im Wartungsmodus können Sie Webparts auf der Seite löschen oder verschieben.</span><span class="sxs-lookup"><span data-stu-id="146a8-154">in maintenance mode, you can delete or move web parts on the page</span></span>
- <span data-ttu-id="146a8-155">Im Wartungsmodus werden nur Informationen zu Webparts angezeigt.</span><span class="sxs-lookup"><span data-stu-id="146a8-155">the maintenance mode shows only information about web parts.</span></span> <span data-ttu-id="146a8-156">Sie können ihn nicht verwenden, um Informationen zu SharePoint Framework-Erweiterungen anzuzeigen, die auf der Seite ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="146a8-156">You cannot use it to show information about SharePoint Framework extensions that are executed on the page</span></span>
- <span data-ttu-id="146a8-157">Durch Wechseln in den Wartungsmodus wird nur das Ausführen des Webpartcodes deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="146a8-157">switching to maintenance mode only disables executing web part code.</span></span> <span data-ttu-id="146a8-158">Alle SharePoint Framework-Erweiterungen, die auf der Seite registriert sind, werden weiterhin ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="146a8-158">Any SharePoint Framework extensions registered on the page will still execute</span></span>

## <a name="see-also"></a><span data-ttu-id="146a8-159">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="146a8-159">See also</span></span>

- <span data-ttu-id="146a8-160">[Öffnen und Verwenden der Webpart-Wartungsseite]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2))</span><span class="sxs-lookup"><span data-stu-id="146a8-160">[Open and use the web part maintenance page]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2))</span></span>