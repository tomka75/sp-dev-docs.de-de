---
title: Verwenden von Benutzerprofilen in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 75880f9811d299cd14a66467fac73439aefa1818
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="work-with-user-profiles-in-a-sharepoint-multi-geo-tenant"></a><span data-ttu-id="e3ce8-102">Verwenden von Benutzerprofilen in einem SharePoint Multi-Geo-Mandanten</span><span class="sxs-lookup"><span data-stu-id="e3ce8-102">Work with user profiles in a SharePoint Multi-Geo tenant</span></span>

> <span data-ttu-id="e3ce8-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="e3ce8-104">In einem Mandanten Multi-Geo können Sie eine bevorzugte Datenspeicherort für einen Benutzer definieren.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-104">In a Multi-Geo tenant, you can define a preferred data location for a user.</span></span> <span data-ttu-id="e3ce8-105">Dieser Artikel beschreibt auch zum Suchen der Website eines Benutzers OneDrive und zum Lesen und Aktualisieren von Standard und benutzerdefinierten Benutzerprofileigenschaften.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-105">This article also describes how to find a user's OneDrive site and how to read and update default and custom user profile properties.</span></span>

## <a name="where-are-user-profiles-located-in-a-multi-geo-tenant"></a><span data-ttu-id="e3ce8-106">Wo befinden sich die Benutzerprofile in einem Mandanten Multi-Geo?</span><span class="sxs-lookup"><span data-stu-id="e3ce8-106">Where are user profiles located in a Multi-Geo tenant?</span></span>
<span data-ttu-id="e3ce8-107">In einem Multi-Geo-Mandanten SharePoint Benutzer Zeitspanne, die die Speicherorte der verschiedenen Geo - beispielsweise einige Benutzer in Nordamerika, sind einige in Europa und So weiter.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-107">In a Multi-Geo tenant, SharePoint users span the different geo locations - for example, some users are in North America, some are in Europe, and so on.</span></span> <span data-ttu-id="e3ce8-108">Dieses Modell gilt auch für Benutzerkonten und persönliche Websites von (OneDrive für Unternehmen).</span><span class="sxs-lookup"><span data-stu-id="e3ce8-108">This model also applies to user accounts and personal (OneDrive for Business) sites.</span></span> <span data-ttu-id="e3ce8-109">Idealerweise werden die Benutzer und ihre Benutzerkonten und Websites am selben Speicherort Geo an.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-109">Ideally, the users and their user accounts and sites are in the same geo location.</span></span> <span data-ttu-id="e3ce8-110">Um dies, stellen Sie sicher, bevor Sie persönliche Websites erstellen, legen Sie bevorzugte Datenspeicherort des Benutzers auf ihrem Standort Geo.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-110">To ensure this, before you create personal sites, you set the user's preferred data location to their geo location.</span></span> 

<span data-ttu-id="e3ce8-111">Im Beispiel in der folgenden Abbildung dargestellt Benutzer vesa@contoso.onmicrosoft.com in Europa Leben ist und eine bevorzugte Datenspeicherort auf **EUR**festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-111">In the example shown in the following image, user vesa@contoso.onmicrosoft.com is living in Europe and has a preferred data location set to **EUR**.</span></span> <span data-ttu-id="e3ce8-112">Als solche:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-112">As such:</span></span>
 
- <span data-ttu-id="e3ce8-113">Die Standard-Kopie der Profil des Benutzers befindet sich in den Europa Geo-Speicherort.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-113">The default copy of the user's profile is in the Europe geo location.</span></span>
- <span data-ttu-id="e3ce8-114">Persönliche Website des Benutzers wird in den Europa Geo Speicherort erstellt.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-114">The user's personal site is created in the Europe geo location.</span></span>

<span data-ttu-id="e3ce8-115">Benutzer bert@contoso.onmicrosoft.com hat seine bevorzugte Datenspeicherort auf **Name**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-115">User bert@contoso.onmicrosoft.com has his preferred data location set to **NAM**.</span></span> <span data-ttu-id="e3ce8-116">Da er eine persönliche Website in Europa gehostet werden hatte, bevor seine bevorzugte Datenspeicherort festgelegt wurde, bleibt seinem Profil in Europa.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-116">Because he  had a personal site hosted in Europe before his preferred data location was set, his profile stays in Europe.</span></span> 

![World Karte zur Erläuterung von Geo Standardspeicherort in Nordamerika und Satelliten Speicherorte in Europa und Asien, mit Benutzern, geografisch Speicherorte und bevorzugte Datenspeicherorte festlegen](media/multigeo/multigeouserprofiles_intro.png)

<span data-ttu-id="e3ce8-118">Profile und der persönlichen Websites der Benutzer befinden sich in den gleichen Speicherort Geo.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-118">Users' profiles and personal sites are in the same geo location.</span></span> <span data-ttu-id="e3ce8-119">Für Benutzer, die nicht mit eine persönliche Website verfügen:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-119">For users who do not have a personal site:</span></span>

- <span data-ttu-id="e3ce8-120">Wenn sie eine bevorzugte Datenspeicherort festgelegt, befindet sich ihr Profil in diesen Speicherort Geo.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-120">If they set a preferred data location, their profile is located in that geo location.</span></span>
- <span data-ttu-id="e3ce8-121">Wenn sie eine bevorzugte Datenspeicherort nicht eingerichtet haben, ist ihr Profil den Standardspeicherort Geo gespeichert.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-121">If they have not set a preferred data location, their profile is located in the default geo location.</span></span>

<span data-ttu-id="e3ce8-122">Zum Speicherort des Profils eines Benutzers programmgesteuert zu ermitteln, können Sie eine der folgenden Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-122">To programmatically discover a user's profile location, you can do one of the following:</span></span>

- <span data-ttu-id="e3ce8-123">Verwenden Sie das SharePoint-Benutzerprofil API.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-123">Use the SharePoint User Profile API.</span></span> <span data-ttu-id="e3ce8-124">Diese Vorgehensweise wird empfohlen, da sie in allen Szenarien funktioniert.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-124">We recommend this approach because it works in all scenarios.</span></span> 
- <span data-ttu-id="e3ce8-125">Verwenden Sie Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-125">Use Microsoft Graph.</span></span> <span data-ttu-id="e3ce8-126">Dies gilt für Benutzer, die auch persönliche Websites haben, aber nicht für Benutzer, die nicht über persönliche Websites verfügen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-126">This works for users who also have personal sites, but not for users who don't have personal sites.</span></span>

### <a name="use-the-sharepoint-user-profile-api-to-detect-the-profile-location"></a><span data-ttu-id="e3ce8-127">Verwenden Sie die SharePoint-Benutzer-Profil-API, um den Speicherort des Profils erkennen</span><span class="sxs-lookup"><span data-stu-id="e3ce8-127">Use the SharePoint User Profile API to detect the profile location</span></span>
<span data-ttu-id="e3ce8-128">Rufen Sie die SharePoint-Benutzer-Profil-API über REST oder CSOM, um die persönliche Website-Host-URL für ein bestimmtes Konto abzurufen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-128">You can call the SharePoint User Profile API via REST or CSOM to retrieve the personal site host URL for a given account.</span></span> <span data-ttu-id="e3ce8-129">Diese URL enthält Hosts der persönlichen Websites für persönliche Websites des Benutzers, unabhängig davon, ob die persönliche Website erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-129">This URL contains the personal site host for the user's personal site, regardless of whether the personal site has been created.</span></span> <span data-ttu-id="e3ce8-130">Das folgende Beispiel zeigt die REST-Aufrufs.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-130">The following example shows the REST call.</span></span>

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/personalsitehosturl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

<span data-ttu-id="e3ce8-131">Wenn Sie c# verwenden, ist CSOM, wie im folgenden Beispiel dargestellt einfacher zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-131">If you're using C#, CSOM, as shown in the following example, is easier to use.</span></span>

```C#
public string GetUserPersonalSiteHostUrlCSOM(string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(this.clientContext);
    var userProperties = peopleManager.GetPropertiesFor($"i:0#.f|membership|{userPrincipalName}");
    this.clientContext.Load(userProperties);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalSiteHostUrl;

    return result;
}
```

<span data-ttu-id="e3ce8-132">Wenn Sie die Host-URL für persönliche Websites haben, können Sie, die zusammen mit der [Serverfarm mit mehreren geografisch](multigeo-discovery.md) Ermittlungsinformationen den Mandanten Admin-Website-URL für den Speicherort der Geo abgerufen, die dem Profil des Benutzers hostet.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-132">When you have the personal site host URL, you can use that along with the [Multi-Geo discovery](multigeo-discovery.md) information to get the tenant admin site URL for the geo location that hosts the user's profile.</span></span>

<span data-ttu-id="e3ce8-133">Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="e3ce8-133">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

### <a name="use-microsoft-graph-to-detect-the-users-personal-site-url"></a><span data-ttu-id="e3ce8-134">Verwenden von Microsoft Graph zum Erkennen von persönlichen Website-URL des Benutzers</span><span class="sxs-lookup"><span data-stu-id="e3ce8-134">Use Microsoft Graph to detect the user's personal site URL</span></span>
<span data-ttu-id="e3ce8-135">Zum Ermitteln des Benutzers persönliche Website-URL in einem Multi-Geo-Mandanten können Sie den folgenden Aufruf von Microsoft Graph verwenden:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-135">To discover a user's personal site URL in a Multi-Geo tenant, you can use the following Microsoft Graph call:</span></span>

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=mySite
```

<span data-ttu-id="e3ce8-136">Wenn Sie die Host-URL für persönliche Websites haben, können Sie, die zusammen mit der [Serverfarm mit mehreren geografisch](multigeo-discovery.md) Ermittlungsinformationen den Mandanten Admin-Website-URL für den Speicherort der Geo abgerufen, die dem Profil des Benutzers hostet.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-136">When you have the personal site host URL, you can use that along with the [Multi-Geo discovery](multigeo-discovery.md) information to get the tenant admin site URL for the geo location that hosts the user's profile.</span></span>

> [!NOTE] 
> <span data-ttu-id="e3ce8-137">Wenn der Benutzer eine persönliche Website vorhanden ist, funktionieren diese Vorgehensweise nicht.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-137">If the user doesn't have a personal site, this approach will not work.</span></span> <span data-ttu-id="e3ce8-138">Verwenden Sie stattdessen die SharePoint-Benutzer-Profil-API.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-138">Instead, you should use the SharePoint User Profile API.</span></span>

<span data-ttu-id="e3ce8-139">Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="e3ce8-139">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

## <a name="updating-user-profile-properties"></a><span data-ttu-id="e3ce8-140">Aktualisieren von Benutzerprofileigenschaften</span><span class="sxs-lookup"><span data-stu-id="e3ce8-140">Updating user profile properties</span></span>
<span data-ttu-id="e3ce8-141">Verfügbarmachen von Massenupdates für Benutzerprofileigenschaften ist ein häufiges Szenario für Unternehmenskunden.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-141">Making bulk updates to user profile properties is a common scenario for enterprise customers.</span></span> <span data-ttu-id="e3ce8-142">Der Prozess zum Verwenden variiert basierend auf dem Typ der Benutzerprofileigenschaft, den Sie aktualisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-142">The process to use varies based on the type of user profile property you want to update.</span></span>

### <a name="updating-default-user-profile-properties"></a><span data-ttu-id="e3ce8-143">Aktualisieren die standardmäßigen Benutzerprofileigenschaften</span><span class="sxs-lookup"><span data-stu-id="e3ce8-143">Updating default user profile properties</span></span>
<span data-ttu-id="e3ce8-144">Einige Benutzerprofileigenschaften sind standardmäßig verfügbar. beispielsweise **Abteilung**, **Mich-Seite**und **PreferredDataLocation**.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-144">Some user profile properties are available by default; for example, **Department**, **AboutMe**, and **PreferredDataLocation**.</span></span> <span data-ttu-id="e3ce8-145">Es wird empfohlen, die Microsoft Graph-API verwenden, um diese Eigenschaften zu aktualisieren, da Microsoft Graph Geo-geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-145">We recommend that you use the Microsoft Graph API to update these properties, because Microsoft Graph is geo-aware.</span></span> <span data-ttu-id="e3ce8-146">Im folgenden Beispiel wird veranschaulicht, wie die **Mich-Seite** -Eigenschaft für den Benutzer bert@contoso.onmicrosoft.com zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-146">The following example shows how to update the **AboutMe** property for the user bert@contoso.onmicrosoft.com.</span></span>

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=aboutme
```

<span data-ttu-id="e3ce8-147">Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="e3ce8-147">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

#### <a name="updating-the-preferred-data-location-property"></a><span data-ttu-id="e3ce8-148">Aktualisieren die bevorzugten Daten Location-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="e3ce8-148">Updating the preferred data location property</span></span>
<span data-ttu-id="e3ce8-149">Bevorzugte Datenspeicherort (**PreferredDataLocation** -Eigenschaft) des Benutzers gibt die bevorzugte Geo-Position für den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-149">The user's preferred data location (**preferredDataLocation** property) indicates the preferred geo location for the user.</span></span> <span data-ttu-id="e3ce8-150">Dies wirkt sich auf Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-150">This affects the following:</span></span>

- <span data-ttu-id="e3ce8-151">Die Geo-Speicherort an, in dem Benutzer persönliche Websites bereitgestellt wird</span><span class="sxs-lookup"><span data-stu-id="e3ce8-151">The geo location where the user's personal site is provisioned</span></span>
- <span data-ttu-id="e3ce8-152">Die Geo-Speicherort, in dem der Benutzer Gruppe Websites erstellt werden</span><span class="sxs-lookup"><span data-stu-id="e3ce8-152">The geo location where the user's group sites are created</span></span> 

<span data-ttu-id="e3ce8-153">Da die bevorzugte Datenspeicherort eine Standardeigenschaft ist, wird empfohlen, die Microsoft Graph-API verwenden, um diese Konfiguration wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-153">Because the preferred data location is a default property, we recommend that you use the Microsoft Graph API  to configure it, as shown in the following example.</span></span> 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=preferredDataLocation

PATCH https://graph.microsoft.com/beta/users/bert@contoso.onmicrosoft.com

JSON payload:
{
    "preferredDataLocation" : "eur"
}

```

<span data-ttu-id="e3ce8-154">Finden Sie weitere Informationen finden Sie [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) .</span><span class="sxs-lookup"><span data-stu-id="e3ce8-154">To learn more, see the [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) sample.</span></span>

### <a name="custom-sharepoint-user-profile-properties"></a><span data-ttu-id="e3ce8-155">Benutzerdefinierte SharePoint-Benutzerprofileigenschaften</span><span class="sxs-lookup"><span data-stu-id="e3ce8-155">Custom SharePoint user profile properties</span></span>
<span data-ttu-id="e3ce8-156">Sie können unternehmensspezifische Benutzerprofileigenschaften von Benutzerprofilen in SharePoint hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-156">You can add company-specific user profile properties to user profiles in SharePoint.</span></span> <span data-ttu-id="e3ce8-157">Für SharePoint Multi-Geo-Mandanten gelten die folgenden Aspekte:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-157">For SharePoint Multi-Geo tenants, the following considerations apply:</span></span>

- <span data-ttu-id="e3ce8-158">Benutzerdefinierte Benutzerprofileigenschaften werden auf Standortebene Geo erstellt.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-158">Custom user profile properties are created at the geo location level.</span></span> <span data-ttu-id="e3ce8-159">Wenn Sie eine Eigenschaft in den Europa Geo Speicherort erstellen, ist diese Eigenschaft in den anderen Geo Speicherorten nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-159">If you create a property in the Europe geo location, that property is not available in the other geo locations.</span></span> <span data-ttu-id="e3ce8-160">Es empfiehlt sich erstellen Sie benutzerdefinierte Profileigenschaften an allen Speicherorten von geografisch.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-160">As a best practice, create custom user profile properties in all geo locations.</span></span> <span data-ttu-id="e3ce8-161">Dadurch wird das Risiko, dass Daten bei einer Verschiebung Benutzer über Geo Standorte verloren.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-161">This reduces the risk that data will be lost when a user move across geo locations.</span></span>
- <span data-ttu-id="e3ce8-162">Sie müssen Lesen und Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften auf Standortebene Geo.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-162">You must read and update custom user profile properties at the geo location level.</span></span> <span data-ttu-id="e3ce8-163">Wenn Sie eine benutzerdefinierte Eigenschaft an allen Speicherorten von Geo erstellt haben, müssen Sie die Speicherorte der Geo durchlaufen und aktualisieren Sie die Eigenschaft für alle Benutzer.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-163">If you created a custom property in all geo locations, you need to iterate over the geo locations and update the property for all  users.</span></span>

```C#
// For SharePoint Online custom properties, use the following approach.
string userPrincipalName = "bert@contoso.onmicrosoft.com";
string userAccountName = $"i:0#.f|membership|{userPrincipalName}";
PeopleManager peopleManager = new PeopleManager(tenantAdminContext);
var propsToRetrieve = new string[] { "CostCenter", "CustomProperty" };
var props = peopleManager.GetUserProfilePropertiesFor(new UserProfilePropertiesForUser(tenantAdminContext, userAccountName, propsToRetrieve));
tenantAdminContext.ExecuteQuery();

int i = 0;
foreach (var prop in props)
{
    Console.WriteLine($"Prop: {propsToRetrieve[i]} Value: {prop}");
    i++;
}

// Update user profile properties
peopleManager.SetSingleValueProfileProperty(userAccountName, "CostCenter", "89786879");
tenantAdminContext.ExecuteQuery();
```

<span data-ttu-id="e3ce8-164">Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="e3ce8-164">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

### <a name="using-the-bulk-user-profile-update-api"></a><span data-ttu-id="e3ce8-165">Verwenden des Bulk Benutzer Profile Updates API</span><span class="sxs-lookup"><span data-stu-id="e3ce8-165">Using the bulk user profile update API</span></span>
<span data-ttu-id="e3ce8-166">Die [Massen Benutzerprofil aktualisieren API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) können Massenupdates an benutzerdefinierten Benutzerprofileigenschaften in einer Serverfarm mit mehreren geografisch Mandanten vornehmen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-166">You can use the [bulk user profile update API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) to make bulk updates to custom user profile properties in a Multi-Geo tenant.</span></span> <span data-ttu-id="e3ce8-167">Beachten Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e3ce8-167">Note the following:</span></span>

- <span data-ttu-id="e3ce8-168">Diese API auf Standortebene Geo funktioniert und ist nicht Multi-Geo berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-168">This API works at the geo location level and is not Multi-Geo aware.</span></span> <span data-ttu-id="e3ce8-169">Wenn Sie in den Europa Geo Speicherort die API verwenden, werden beispielsweise nur Konten in Europa aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-169">For example, if you use the API in the Europe geo location, only accounts in Europe are updated.</span></span>
- <span data-ttu-id="e3ce8-170">Wenn Sie eine Importdatei mit Konten in verschiedenen Geo Speicherorte angeben, wird die API nur die Eigenschaften für die Benutzer in diesen Speicherort Geo aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="e3ce8-170">If you specify an import file with accounts in different geo locations, the API will only update the properties for the users in that geo location.</span></span>


## <a name="see-also"></a><span data-ttu-id="e3ce8-171">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e3ce8-171">See also</span></span>

- [<span data-ttu-id="e3ce8-172">Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e3ce8-172">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>](bulk-user-profile-update-api-for-sharepoint-online.md)
- [<span data-ttu-id="e3ce8-173">User Profile Batch Update-API-Beispiel</span><span class="sxs-lookup"><span data-stu-id="e3ce8-173">User Profile Batch Update API sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.BatchUpdate.API)


