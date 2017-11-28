---
title: "Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 1742bdc985fa133bb6866803ce37aac74c419e17
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a><span data-ttu-id="0a954-102">Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="0a954-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>


<span data-ttu-id="0a954-103">_**Gilt für:** SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="0a954-103">_**Applies to:** SharePoint Online_</span></span>

<span data-ttu-id="0a954-104">Im Rahmen von der neuen Client Side Objekt Modell (CSOM) Version (4622.1208 oder höher) hat SharePoint die Möglichkeit, benutzerdefinierte Benutzerprofileigenschaften Import Massen.</span><span class="sxs-lookup"><span data-stu-id="0a954-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span></span> <span data-ttu-id="0a954-105">Nur die Option musste vor dieser Version des Benutzers Profil CSOM Vorgänge für die Aktualisierung bestimmter Eigenschaften für einzelne Benutzerprofile nutzen.</span><span class="sxs-lookup"><span data-stu-id="0a954-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span></span> <span data-ttu-id="0a954-106">Dieser Ansatz ist jedoch ineffiziente und zu zeitaufwendig (insbesondere dann, wenn mehrere tausend Profile zu tun).</span><span class="sxs-lookup"><span data-stu-id="0a954-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span></span>

<span data-ttu-id="0a954-107">Viele Unternehmen müssen benutzerdefinierte Attribute auf der SharePoint-Benutzerprofildienst replizieren und so eine weitere leistungsfähige Benutzerprofil Bulk API freigegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="0a954-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span></span>

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a><span data-ttu-id="0a954-108">Eine Übersicht über die Massen Benutzer Profile Update-Prozess</span><span class="sxs-lookup"><span data-stu-id="0a954-108">An Overview of the Bulk User Profile Update Process</span></span>
<span data-ttu-id="0a954-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-109"></span></span>

![Massen UPA Update-Datenfluss](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. <span data-ttu-id="0a954-111">Benutzerattribute werden aus Active Directory des Unternehmens mit Azure Active Directory synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="0a954-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span></span> <span data-ttu-id="0a954-112">Sie können auswählen, welche Attribute in lokalen und Azure repliziert werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-112">You can select which attributes are replicated across on-premises and Azure.</span></span>
2. <span data-ttu-id="0a954-113">Ein standardisierter Satz mit Attributen werden von Azure Active Directory mit SharePoint Online-Benutzerprofilspeicher in Office 365 repliziert.</span><span class="sxs-lookup"><span data-stu-id="0a954-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span></span> <span data-ttu-id="0a954-114">Unlke lokale SharePoint, diese Attribute können nicht angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span></span>
3. <span data-ttu-id="0a954-115">Eine benutzerdefinierte Synchronisierungstool Nutzen der Vorteile des neuen Bulk Updates APIs.</span><span class="sxs-lookup"><span data-stu-id="0a954-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span></span> <span data-ttu-id="0a954-116">Dieses Tool eine JSON-Datei, die dem Office 365-Mandanten hochlädt und in die Warteschlange des Importvorgangs.</span><span class="sxs-lookup"><span data-stu-id="0a954-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span></span> <span data-ttu-id="0a954-117">Dieses Tool kann implementiert werden, mithilfe von verwaltetem Code (.NET) oder als eine PowerShell Skript mithilfe der neuen CSOM-APIs.</span><span class="sxs-lookup"><span data-stu-id="0a954-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span></span>
4. <span data-ttu-id="0a954-118">Eine Zeile des Business (LOB) System oder für alle externen Systeme ist die Quelle der Informationen in der Datei JSON.</span><span class="sxs-lookup"><span data-stu-id="0a954-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span></span> <span data-ttu-id="0a954-119">Dies kann auch eine Kombination von Daten aus Active Directory und alle externen Systeme sein.</span><span class="sxs-lookup"><span data-stu-id="0a954-119">This could also be a combination of data from Active Directory and any external system.</span></span> <span data-ttu-id="0a954-120">Beachten Sie, dass aus der Sicht API LOB-System selbst einer lokalen SharePoint 2013 oder 2016 Farm werden konnte.</span><span class="sxs-lookup"><span data-stu-id="0a954-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span></span>
5. <span data-ttu-id="0a954-121">Ein außerhalb des im Feld Server Seite Zeitgeberauftrags in SharePoint online mit dem überprüft importanforderungen in der Warteschlange und führt die tatsächlichen Importvorgangs basierend auf die API-Aufrufe und die Informationen in der bereitgestellten JSON-Datei.</span><span class="sxs-lookup"><span data-stu-id="0a954-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span></span>
6. <span data-ttu-id="0a954-122">Erweiterte Benutzerprofilinformationen ist innerhalb von Benutzerprofilen verfügbar und kann aus einem aus der im Feld oder benutzerdefinierte Funktionen in SharePoint online verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span></span>

><span data-ttu-id="0a954-123">**Hinweis**: der Import funktioniert nur für Benutzerprofileigenschaften die wurden **nicht** durch Endbenutzer bearbeitet werden festgelegt.</span><span class="sxs-lookup"><span data-stu-id="0a954-123">**Note**: The import only works for user profile properties which have **not** been set to be editable by end users.</span></span> <span data-ttu-id="0a954-124">Dies ist, um zu verhindern, dass der Importprozess für Benutzerprofildaten überschreiben alle Informationen, die ein Endbenutzer bereits aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="0a954-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span></span> <span data-ttu-id="0a954-125">Darüber hinaus erlaubt der Import nur benutzerdefinierte Eigenschaften, die nicht active Directory Kerneigenschaften sind.</span><span class="sxs-lookup"><span data-stu-id="0a954-125">Additionally, the import only allows custom properties that are not active directory core properties.</span></span> <span data-ttu-id="0a954-126">Diese müssen mit Azure Active Directory synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-126">These must be synchronized to Azure Active Directory.</span></span> <span data-ttu-id="0a954-127">Der Liste der diese Directory Kerneigenschaften finden Sie unter der Tabelle im Abschnitt häufig gestellte Fragen zu aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="0a954-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span></span>

<span data-ttu-id="0a954-128">Es folgt ein kurzes Video an, das mithilfe der neuen CSOM-API aus beiden verwaltetem Code (.NET) und PowerShell veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="0a954-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span></span> <span data-ttu-id="0a954-129">Sie können den Beispielcode verwendet, einschließlich des PowerShell-Beispielskripts im [Office Dev Plug & Play-Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202)suchen.</span><span class="sxs-lookup"><span data-stu-id="0a954-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span></span>

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a><span data-ttu-id="0a954-130">Import-Dateiformat</span><span class="sxs-lookup"><span data-stu-id="0a954-130">Import File Format</span></span>
<span data-ttu-id="0a954-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-131"></span></span>

<span data-ttu-id="0a954-132">Der Importvorgang verwendet eine JSON-Datei, die Eigenschaften und deren Werte enthält.</span><span class="sxs-lookup"><span data-stu-id="0a954-132">The import process uses a JSON file containing the properties and their values.</span></span> <span data-ttu-id="0a954-133">Hier finden Sie die erwartete Struktur der Datei:</span><span class="sxs-lookup"><span data-stu-id="0a954-133">Below is the expected structure of that file:</span></span>   

```JSON
{
   "value": [
     {
       "<IdName>": "<UserIdValue_1>",
       "<AttributeName_1>": "<User1_AttributeValue_1>",
       "<AttributeName_2>": "<User1_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_2>",
       "<AttributeName_1>": "<User2_AttributeValue_1>",
       "<AttributeName_2>": "<User2_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_n>",
       "<AttributeName_1>": "<Usern_AttributeValue_1>",
       "<AttributeName_2>": "<Usern_AttributeValue_2>",
     }
   ]
}
```

<span data-ttu-id="0a954-134">Im folgenden ist eine einfaches Beispiel für die Datei das oben genannten-Format verwenden:</span><span class="sxs-lookup"><span data-stu-id="0a954-134">Below is a simple example file using the format above:</span></span>

```JSON
{
  "value": [
    {
      "IdName": "vesaj@contoso.com",
      "City": "Helsinki",
      "Office": "Viper"
    },
    {
      "IdName": "bjansen@contoso.com",
      "City": "Brussels",
      "Office": "Beetle"
    },
    {
      "IdName": "unknowperson@contoso.com",
      "City": "None",
      "Office": ""
    },
    {
      "IdName": "erwin@contoso.com",
      "City": "Stockholm",
      "Office": "Elite"
    }
  ]
}
```

<span data-ttu-id="0a954-135">Im obigen Beispiel ist Identity Lösung basierend auf der `IdName` -Eigenschaft und es werden zwei Eigenschaften, die zu aktualisierenden aufgerufen `City` und `Office`.</span><span class="sxs-lookup"><span data-stu-id="0a954-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span></span> <span data-ttu-id="0a954-136">Die Datei enthält Informationen für vier verschiedene Konten in den Mandanten.</span><span class="sxs-lookup"><span data-stu-id="0a954-136">The file contains information for four different accounts within the tenant.</span></span> <span data-ttu-id="0a954-137">Eigenschaftennamen, die in dieser Quelldatei verwendet stimmen nicht unbedingt die Namen in der SharePoint Online-Benutzerprofildienst verwendet werden, da wir die richtigen eigenschaftenzuordnung in unserem Code bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span></span> 

### <a name="source-data-file-restrictions"></a><span data-ttu-id="0a954-138">Quelle Daten Datei Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="0a954-138">Source Data File Restrictions</span></span>
<span data-ttu-id="0a954-139">Es gibt einige Einschränkungen für einzelne Quelldateien für Daten:</span><span class="sxs-lookup"><span data-stu-id="0a954-139">There are few restrictions on individual source data files:</span></span>
- <span data-ttu-id="0a954-140">Maximale Dateigröße: 2GB</span><span class="sxs-lookup"><span data-stu-id="0a954-140">Maximum file size: 2GB</span></span>
- <span data-ttu-id="0a954-141">Maximale Anzahl von Eigenschaften: 500.000</span><span class="sxs-lookup"><span data-stu-id="0a954-141">Maximum number of properties: 500,000</span></span>
- <span data-ttu-id="0a954-142">Die Quelldatei muss auf dem gleichen SharePoint Online-Mandanten hochgeladen werden, auf dem der Prozess gestartet wurde</span><span class="sxs-lookup"><span data-stu-id="0a954-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span></span>


## <a name="user-profile-property-import-process"></a><span data-ttu-id="0a954-143">Importprozess für Benutzerprofildaten-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="0a954-143">User Profile Property Import Process</span></span>
<span data-ttu-id="0a954-144"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-144"></span></span>

<span data-ttu-id="0a954-145">Hier ist der vollständige Vorgang aus:</span><span class="sxs-lookup"><span data-stu-id="0a954-145">Here’s the full process:</span></span>

1. <span data-ttu-id="0a954-146">Erstellen oder zum Synchronisieren von Benutzern in einem Office 365-Mandanten oder zugeordnet Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a954-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span></span>
     - <span data-ttu-id="0a954-147">Wenn Benutzer in Azure Active Directory synchronisiert werden, wird es auch einen standardisierten Satz mit Attributen zu SharePoint Online User Profile Service synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="0a954-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span></span>
2. <span data-ttu-id="0a954-148">Erstellen Sie alle erforderlichen benutzerdefinierten Eigenschaften innerhalb des Benutzerprofildiensts</span><span class="sxs-lookup"><span data-stu-id="0a954-148">Create any needed custom properties within the User Profile Service</span></span>
     - <span data-ttu-id="0a954-149">Da es keine remote-APIs zum Erstellen von benutzerdefinierten Eigenschaften in der Benutzerprofildienst ist, dieser Schritt muss manuell ausgeführt werden für jede der Mandanten, in dem benutzerdefinierte Benutzerprofileigenschaften erforderlich sind (Dies ist nur einmal pro Mandant ausgeführt werden).</span><span class="sxs-lookup"><span data-stu-id="0a954-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span></span>
     - <span data-ttu-id="0a954-150">Nur Benutzerprofileigenschaften "Unzulässige durch Endbenutzer bearbeitet werden" importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="0a954-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span></span> <span data-ttu-id="0a954-151">Ein JSON importieren möchten-Objekteigenschaft auf einer Benutzerprofileigenschaft, die als "bearbeitbaren durch Endbenutzer" markiert ist eine Ausnahme ausgegeben, wenn die CSOM-API aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="0a954-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span></span>
3. <span data-ttu-id="0a954-152">Erstellen und Hochladen der Datei JSON in Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="0a954-152">Create and upload the JSON file to the Office 365 tenant</span></span>
     - <span data-ttu-id="0a954-153">Sie müssen die JSON-Daten-Datei mit den Informationen, die dem Office 365-Mandanten aktualisiert werden hoch.</span><span class="sxs-lookup"><span data-stu-id="0a954-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span></span>
     - <span data-ttu-id="0a954-154">Im Fall einer Ausnahme während des Importvorgangs bieten SharePoint zusätzliche Protokollierungsinformationen in derselben Dokumentbibliothek, in dem die Datei in einem neuen Ordner Sub vorhanden war, gespeichert.</span><span class="sxs-lookup"><span data-stu-id="0a954-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span></span>
     - <span data-ttu-id="0a954-155">Bereinigen der Protokolldateien und JSON-Dateien werden nicht automatisch ausgeführt und liegt in der Verantwortung der benutzerdefinierten Lösung mithilfe der API.</span><span class="sxs-lookup"><span data-stu-id="0a954-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span></span> <span data-ttu-id="0a954-156">Sie sollten den Lebenszyklus von diese Dateien in der Implementierung.</span><span class="sxs-lookup"><span data-stu-id="0a954-156">You should consider the life cycle of these files within your implementation.</span></span> <span data-ttu-id="0a954-157">Diese Dateien werden in Dokumentbibliotheken gespeichert, so wird einen Teil des zugewiesenen Speichers für die Websitesammlung genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span></span>
4. <span data-ttu-id="0a954-158">Rufen Sie das gleichzeitige UPA importieren-API für den Importauftrag queuing</span><span class="sxs-lookup"><span data-stu-id="0a954-158">Call the bulk UPA Import API for queuing the import job</span></span>
     - <span data-ttu-id="0a954-159">Verwenden Sie die CSOM-API, um den Importvorgang in die Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="0a954-159">Use the CSOM API to queue the import process.</span></span> <span data-ttu-id="0a954-160">Dies kann durch Ausführen von CSOM Code mit einer verwalteten Code (.NET) oder PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a954-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span></span>
     - <span data-ttu-id="0a954-161">Die Methode, um den Auftrag in die Warteschlange erfordert Eigenschaftenzuordnungsinformationen und den Speicherort der Datei.</span><span class="sxs-lookup"><span data-stu-id="0a954-161">The method to queue the job requires property mapping information and the location of the data file.</span></span> <span data-ttu-id="0a954-162">Diese Methode führt schnell, da es nur die tatsächlichen Importvorgangs Warteschlangen, die später im Rahmen einer Back-End-Prozess in SharePoint Online ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0a954-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span></span>
5. <span data-ttu-id="0a954-163">Überprüfen Sie den Status des Auftrags für import</span><span class="sxs-lookup"><span data-stu-id="0a954-163">Check the status of the import job</span></span>
     - <span data-ttu-id="0a954-164">Remote-APIs können auch den Status einer bestimmten Importauftrag oder alle der letzte Importaufträge überprüfen.</span><span class="sxs-lookup"><span data-stu-id="0a954-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span></span> <span data-ttu-id="0a954-165">Um den Status für einen bestimmten Aufruf überprüfen können, sollten Sie speichern die eindeutige Auftrags-ID als Rückgabewert empfangen, wenn der Auftrag in der Warteschlange befinden.</span><span class="sxs-lookup"><span data-stu-id="0a954-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span></span>


## <a name="csom-api-for-the-bulk-import-process"></a><span data-ttu-id="0a954-166">CSOM-API für den Massenimportvorgang</span><span class="sxs-lookup"><span data-stu-id="0a954-166">CSOM API for the Bulk Import Process</span></span>
<span data-ttu-id="0a954-167"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-167"></span></span>

### <a name="queue-import"></a><span data-ttu-id="0a954-168">Importieren von Warteschlangen.</span><span class="sxs-lookup"><span data-stu-id="0a954-168">Queue Import</span></span>
<span data-ttu-id="0a954-169">Sie können die Warteschlange des Importvorgangs durch Aufrufen der [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) Methode befindet sich der [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) Objekt.</span><span class="sxs-lookup"><span data-stu-id="0a954-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="0a954-170">Dies ist ein asynchroner Aufruf, dass er nicht die Quelldaten herunterladen oder führen Sie den Import, sondern einfach eine Arbeitsaufgabe der Warteschlange für dies später hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="0a954-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span></span> <span data-ttu-id="0a954-171">Hier wird die vollständige Signatur der Methode:</span><span class="sxs-lookup"><span data-stu-id="0a954-171">Here’s the full signature of the method:</span></span>

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a><span data-ttu-id="0a954-172">Parameter</span><span class="sxs-lookup"><span data-stu-id="0a954-172">Parameters</span></span>

<span data-ttu-id="0a954-173">**ID-Typ**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span><span class="sxs-lookup"><span data-stu-id="0a954-173">**idType**: _[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span></span>

<span data-ttu-id="0a954-174">Der Typ der Id, die bei der Suche nach dem Benutzerprofil verwendet.</span><span class="sxs-lookup"><span data-stu-id="0a954-174">The type of id to use when looking up the user profile.</span></span> <span data-ttu-id="0a954-175">Mögliche Werte sind `Email`, `CloudId`, und `PrincipalName`.</span><span class="sxs-lookup"><span data-stu-id="0a954-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span></span> <span data-ttu-id="0a954-176">Beachten Sie, dass unabhängig von der Art der Benutzer in der Benutzerprofildienst für den Import arbeiten bereits vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="0a954-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span></span> <span data-ttu-id="0a954-177">Es wird empfohlen, verwenden Sie die `CloudId` um Eindeutigkeit zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="0a954-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span></span>

<span data-ttu-id="0a954-178">Zuordnung zwischen ID-Typ und Azure AD-Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="0a954-178">Property mapping between ID Type and Azure AD property:</span></span>

<span data-ttu-id="0a954-179">UPA Bulk Import-ID-Typ</span><span class="sxs-lookup"><span data-stu-id="0a954-179">UPA Bulk Import ID Type</span></span> | <span data-ttu-id="0a954-180">Azure-Directory-Attribut</span><span class="sxs-lookup"><span data-stu-id="0a954-180">Azure Directory Attribute</span></span>
--- | ---
<span data-ttu-id="0a954-181">CloudId</span><span class="sxs-lookup"><span data-stu-id="0a954-181">CloudId</span></span> | <span data-ttu-id="0a954-182">ObjectID</span><span class="sxs-lookup"><span data-stu-id="0a954-182">ObjectID</span></span>
<span data-ttu-id="0a954-183">' PrincipalName '</span><span class="sxs-lookup"><span data-stu-id="0a954-183">PrincipalName</span></span> | <span data-ttu-id="0a954-184">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-184">userPrincipalName</span></span>
<span data-ttu-id="0a954-185">E-Mail</span><span class="sxs-lookup"><span data-stu-id="0a954-185">Email</span></span> | <span data-ttu-id="0a954-186">mail</span><span class="sxs-lookup"><span data-stu-id="0a954-186">mail</span></span>

<span data-ttu-id="0a954-187">**SourceDataIdProperty**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="0a954-187">**sourceDataIdProperty**: _`System.String`_</span></span>

<span data-ttu-id="0a954-188">Der Name der Id-Eigenschaft in den Quelldaten.</span><span class="sxs-lookup"><span data-stu-id="0a954-188">The name of the id property in the source data.</span></span> <span data-ttu-id="0a954-189">Der Wert der Eigenschaft aus der Datenquelle wird den Benutzer nachschlagen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-189">The value of the property from the source data will be used to lookup the user.</span></span> <span data-ttu-id="0a954-190">Die für die Suche zu verwendenden Benutzerprofildienst-Eigenschaft hängt vom Wert der `idType`.</span><span class="sxs-lookup"><span data-stu-id="0a954-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span></span>

<span data-ttu-id="0a954-191">**PropertyMap**:_`IDictionary<string, string>`_</span><span class="sxs-lookup"><span data-stu-id="0a954-191">**propertyMap**: _`IDictionary<string, string>`_</span></span>

<span data-ttu-id="0a954-192">Eine Zuordnung aus der Name der Eigenschaft auf den Namen der Benutzerprofildienst-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="0a954-192">A map from the source property name to the User Profile Service property name.</span></span> <span data-ttu-id="0a954-193">Beachten Sie, dass die Benutzerprofildienst-Eigenschaften bereits vorhanden sein müssen.</span><span class="sxs-lookup"><span data-stu-id="0a954-193">Note that the User Profile Service properties must already exist.</span></span> <span data-ttu-id="0a954-194">Der Schlüssel ist der Name der Eigenschaft in der Quelldatei verwendet, der Wert ist der Name der Eigenschaft, die in der Benutzerprofildienst verwendet.</span><span class="sxs-lookup"><span data-stu-id="0a954-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span></span>

<span data-ttu-id="0a954-195">**SourceUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="0a954-195">**sourceUri**: _`System.String`_</span></span>

<span data-ttu-id="0a954-196">Der URI der Quelldatei Daten zu importieren.</span><span class="sxs-lookup"><span data-stu-id="0a954-196">The URI of the source data file to import.</span></span> <span data-ttu-id="0a954-197">Die Datei sollte nicht verschoben oder sofort gelöscht werden, da er für einige Zeit nicht heruntergeladen werden kann.</span><span class="sxs-lookup"><span data-stu-id="0a954-197">The file should not be moved or deleted right away as it may not be downloaded for some time.</span></span>

#### <a name="return-value"></a><span data-ttu-id="0a954-198">Return value</span><span class="sxs-lookup"><span data-stu-id="0a954-198">Return value</span></span>
<span data-ttu-id="0a954-199">Eine Guid, die den Importauftrag identifiziert, der in die Warteschlange gestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="0a954-199">A Guid that identifies the import job that has been queued.</span></span>

#### <a name="example"></a><span data-ttu-id="0a954-200">Beispiel</span><span class="sxs-lookup"><span data-stu-id="0a954-200">Example</span></span>
<span data-ttu-id="0a954-201">Es folgt ein Beispiel zur Verwendung von C#-dafür, wie Sie den Prozess, indem die oben genannten Beispiel-Eingabedatei starten:</span><span class="sxs-lookup"><span data-stu-id="0a954-201">Below is an example using C# of how to start the process using the sample input file above:</span></span>

```c#
// Create an instance of the Office 365 Tenant object. Loading this object is not technically needed for this operation. 
Office365Tenant tenant = new Office365Tenant(ctx);
ctx.Load(tenant);
ctx.ExecuteQuery();

// Type of user identifier ["PrincipalName", "Email", "CloudId"] in the 
// User Profile Service. In this case, we use Email as the identifier at the UPA storage
ImportProfilePropertiesUserIdType userIdType = 
      ImportProfilePropertiesUserIdType.Email;

// Name of the user identifier property within the JSON file
var userLookupKey = "IdName";

var propertyMap = new System.Collections.Generic.Dictionary<string, string>();

// The key is the property in the JSON file, 
// The value is the user profile property Name in the User Profile Service
// Notice that we have 2 custom properties in UPA called 'City' and 'OfficeCode'
propertyMap.Add("City", "City");
propertyMap.Add("Office", "OfficeCode");

// Returns a GUID which can be used to check the status of the execution and the end results
var workItemId = tenant.QueueImportProfileProperties(
      userIdType, userLookupKey, propertyMap, fileUrl
      );

ctx.ExecuteQuery();
```

### <a name="check-the-status-of-an-import-job"></a><span data-ttu-id="0a954-202">Überprüfen Sie den Status eines Auftrags für den Import</span><span class="sxs-lookup"><span data-stu-id="0a954-202">Check the Status of an Import Job</span></span>
<span data-ttu-id="0a954-203">Sie können auch den Status der Benutzerprofildienst-Importaufträge suchen, mithilfe der neuen CSOM-APIs.</span><span class="sxs-lookup"><span data-stu-id="0a954-203">You can also check the status of the User Profile Service import jobs by using the new CSOM APIs.</span></span> <span data-ttu-id="0a954-204">Es gibt zwei neue Methoden für dieses im Mandanten-Objekt.</span><span class="sxs-lookup"><span data-stu-id="0a954-204">There are two new methods for this in the Tenant object.</span></span>

<span data-ttu-id="0a954-205">Sie können ein einzelnes Importauftrag Status überprüfen, mithilfe der [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) Methode befindet sich der [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) Objekt.</span><span class="sxs-lookup"><span data-stu-id="0a954-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="0a954-206">Sie müssen den eindeutigen Bezeichner eines bestimmten importieren Auftrag als Parameter an diese Methode bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="0a954-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span></span> <span data-ttu-id="0a954-207">Hier wird die vollständige Signatur der Methode:</span><span class="sxs-lookup"><span data-stu-id="0a954-207">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a><span data-ttu-id="0a954-208">Parameter</span><span class="sxs-lookup"><span data-stu-id="0a954-208">Parameters</span></span>
<span data-ttu-id="0a954-209">**JobID**:_`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="0a954-209">**jobID**: _`System.Guid`_</span></span>

<span data-ttu-id="0a954-210">Die Id des Auftrags, für den den allgemeinen Status abzurufen.</span><span class="sxs-lookup"><span data-stu-id="0a954-210">The id of the job for which to get the high-level status.</span></span>

#### <a name="return-value"></a><span data-ttu-id="0a954-211">Return value</span><span class="sxs-lookup"><span data-stu-id="0a954-211">Return value</span></span>

<span data-ttu-id="0a954-212">Ein [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) -Objekt mit Informationen über den angegebenen Auftrag Statusbericht.</span><span class="sxs-lookup"><span data-stu-id="0a954-212">An [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object with high level status information about the specified job.</span></span>

#### <a name="example"></a><span data-ttu-id="0a954-213">Beispiel</span><span class="sxs-lookup"><span data-stu-id="0a954-213">Example</span></span>
<span data-ttu-id="0a954-214">Im folgenden ist ein Beispiel für c# zum Abrufen von den Status einer bestimmten Importauftrag mit einer gespeicherten-ID verwenden:</span><span class="sxs-lookup"><span data-stu-id="0a954-214">Below is an example using C# of retrieving the status of a specific import job using a stored identifier:</span></span>

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

<span data-ttu-id="0a954-215">Überprüfen des Status aller Importaufträge können mithilfe von der [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) Methode befindet sich im [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) -Objekt.</span><span class="sxs-lookup"><span data-stu-id="0a954-215">You can check the status of all import jobs by using the [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) method located in the [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="0a954-216">Hier wird die vollständige Signatur der Methode:</span><span class="sxs-lookup"><span data-stu-id="0a954-216">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a><span data-ttu-id="0a954-217">Return value</span><span class="sxs-lookup"><span data-stu-id="0a954-217">Return value</span></span>
<span data-ttu-id="0a954-218">Ein [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) Objekt eine Sammlung von [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Objekte mit Informationen zu den einzelnen der Aufträge Statusbericht.</span><span class="sxs-lookup"><span data-stu-id="0a954-218">An [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) object which is a collection of [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) objects with high level status information about each of the jobs.</span></span>

#### <a name="example"></a><span data-ttu-id="0a954-219">Beispiel</span><span class="sxs-lookup"><span data-stu-id="0a954-219">Example</span></span>
<span data-ttu-id="0a954-220">Im folgenden ist ein Beispiel für c# Abrufen von den Status aller Import Aufträge, die derzeit im Mandanten gespeichert verwenden.</span><span class="sxs-lookup"><span data-stu-id="0a954-220">Below is an example using C# of getting the status of all import jobs currently saved in the tenant.</span></span> <span data-ttu-id="0a954-221">Diese bereits verarbeitet werden konnte oder Aufträge in der Warteschlange:</span><span class="sxs-lookup"><span data-stu-id="0a954-221">These could be already processed or queued jobs:</span></span>

```c#
// Load all import jobs – old and queued ones
Office365Tenant tenant = new Office365Tenant(ctx);
var jobs = tenant.GetImportProfilePropertyJobs();
ctx.Load(jobs);
ctx.ExecuteQuery();
foreach (var item in jobs)
{
   // Check whatever properties needed
   var state = item.State;
}
```

<span data-ttu-id="0a954-222">Ein [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) die Statusinformationen Import zurückgegebene Objekt hat die folgenden Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="0a954-222">An [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object returned with the import status information has the following properties.</span></span> 

<span data-ttu-id="0a954-223">**JobId**:_`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="0a954-223">**JobId**: _`System.Guid`_</span></span>

<span data-ttu-id="0a954-224">Die Id des den Importauftrag</span><span class="sxs-lookup"><span data-stu-id="0a954-224">The Id of the import job</span></span>

<span data-ttu-id="0a954-225">**Status**:_[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span><span class="sxs-lookup"><span data-stu-id="0a954-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span></span>

<span data-ttu-id="0a954-226">Eine Enumeration mit der folgenden Werte:</span><span class="sxs-lookup"><span data-stu-id="0a954-226">An enum with following values:</span></span>
- <span data-ttu-id="0a954-227">`Unknown`-Es kann den Status des Auftrags nicht ermitteln.</span><span class="sxs-lookup"><span data-stu-id="0a954-227">`Unknown` - We cannot determine the state of the job</span></span>
- <span data-ttu-id="0a954-228">`Submitted`– Der Auftrag wurde an das System übermittelt</span><span class="sxs-lookup"><span data-stu-id="0a954-228">`Submitted` - The job has been submitted to the system</span></span>
- <span data-ttu-id="0a954-229">`Processing`-Der Auftrag wird verarbeitet</span><span class="sxs-lookup"><span data-stu-id="0a954-229">`Processing` - The job is being processed</span></span>
- <span data-ttu-id="0a954-230">`Queued`-Der Auftrag hat erfolgreich validiert wurde und in der Warteschlange für den Import in UPA</span><span class="sxs-lookup"><span data-stu-id="0a954-230">`Queued` - The job has passed validation and queued for import to UPA</span></span>
- <span data-ttu-id="0a954-231">`Succeeded`– Der Auftrag abgeschlossen ohne Fehlermeldung</span><span class="sxs-lookup"><span data-stu-id="0a954-231">`Succeeded` - The job completed with no error</span></span>
- <span data-ttu-id="0a954-232">`Error`– Der Auftrag abgeschlossen</span><span class="sxs-lookup"><span data-stu-id="0a954-232">`Error` - The job completed with error</span></span>

<span data-ttu-id="0a954-233">**SourceUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="0a954-233">**SourceUri**: _`System.String`_</span></span>

<span data-ttu-id="0a954-234">Der URI der Quelldatei Daten</span><span class="sxs-lookup"><span data-stu-id="0a954-234">The URI to the data source file</span></span>

<span data-ttu-id="0a954-235">**Fehler**:_[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span><span class="sxs-lookup"><span data-stu-id="0a954-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span></span>

<span data-ttu-id="0a954-236">Eine Enumeration, den möglichen Fehler darstellt:</span><span class="sxs-lookup"><span data-stu-id="0a954-236">An enum representing the possible error:</span></span>
- <span data-ttu-id="0a954-237">`NoError`-Keine Fehler gefunden</span><span class="sxs-lookup"><span data-stu-id="0a954-237">`NoError` - No error found</span></span>
- <span data-ttu-id="0a954-238">`InternalError`– Durch einen Fehler im Dienst wurde der Fehler verursacht.</span><span class="sxs-lookup"><span data-stu-id="0a954-238">`InternalError` - The error was caused by a failure in the service</span></span>
- <span data-ttu-id="0a954-239">`DataFileNotExist`-Die Datenquelldatei konnte nicht gefunden werden</span><span class="sxs-lookup"><span data-stu-id="0a954-239">`DataFileNotExist` - The data source file could not be found</span></span>
- <span data-ttu-id="0a954-240">`DataFileNotInTenant`-Die Datenquelldatei nicht zu derselben mandantenorganisation gehören.</span><span class="sxs-lookup"><span data-stu-id="0a954-240">`DataFileNotInTenant` - The data source file did not belong to the same tenant</span></span>
- <span data-ttu-id="0a954-241">`DataFileTooBig`-Die Größe der Datendatei war zu groß</span><span class="sxs-lookup"><span data-stu-id="0a954-241">`DataFileTooBig` - The size of the data file was too big</span></span>
- <span data-ttu-id="0a954-242">`InvalidDataFile`-Die Datenquelldatei bestanden nicht Überprüfung (möglicherweise zusätzliche Details in der Protokolldatei)</span><span class="sxs-lookup"><span data-stu-id="0a954-242">`InvalidDataFile` - The data source file did not pass validation (There may be additional details in the log file)</span></span>
- <span data-ttu-id="0a954-243">`ImportCompleteWithError`-Die Daten importiert, aber es wurde ein Fehler aufgetreten</span><span class="sxs-lookup"><span data-stu-id="0a954-243">`ImportCompleteWithError` - The data has been imported, but there was an error encountered</span></span>

<span data-ttu-id="0a954-244">**ErrorMessage**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="0a954-244">**ErrorMessage**: _`System.String`_</span></span>

<span data-ttu-id="0a954-245">Die Fehlermeldung</span><span class="sxs-lookup"><span data-stu-id="0a954-245">The error message</span></span>

<span data-ttu-id="0a954-246">**LogFileUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="0a954-246">**LogFileUri**: _`System.String`_</span></span>

<span data-ttu-id="0a954-247">Der Uri, der den Ordner, in dem die Protokolle geschrieben wurden</span><span class="sxs-lookup"><span data-stu-id="0a954-247">The Uri to the folder where the logs have been written</span></span>

## <a name="calling-the-import-api-from-powershell"></a><span data-ttu-id="0a954-248">Aufrufen des Imports-API in PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a954-248">Calling the Import API from PowerShell</span></span>
<span data-ttu-id="0a954-249"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-249"></span></span>

<span data-ttu-id="0a954-250">Sie können die Benutzerprofildienst-Bulk Import-API mit PowerShell nutzen.</span><span class="sxs-lookup"><span data-stu-id="0a954-250">You can take advantage of the User Profile Service bulk import API with PowerShell.</span></span> <span data-ttu-id="0a954-251">Dies bedeutet, dass Sie den CSOM-Code direkt in einer PowerShell-Skript mit den erforderlichen Parametern verwenden.</span><span class="sxs-lookup"><span data-stu-id="0a954-251">This means that you’ll use the CSOM code directly in a PowerShell script using the necessary parameters.</span></span> <span data-ttu-id="0a954-252">Dies erfordert, dass das aktualisierte CSOM redistributable-Paket auf dem Computer installiert ist, auf dem das Skript ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0a954-252">This requires that the updated CSOM redistributable package has been installed on the computer where the script is executed.</span></span>

<span data-ttu-id="0a954-253">Mithilfe von PowerShell, müssen Sie nicht Kompilieren des Codes in Visual Studio, die möglicherweise ein Modell besser geeignet für einige Kunden.</span><span class="sxs-lookup"><span data-stu-id="0a954-253">By using PowerShell, you do not need to compile your code within Visual Studio, which may be a more suitable model for some customers.</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="0a954-254">PowerShell-Beispielskript</span><span class="sxs-lookup"><span data-stu-id="0a954-254">Sample PowerShell Script</span></span>
<span data-ttu-id="0a954-255">Im folgenden finden Sie ein PowerShell-Beispielskript die die gleichen Vorgänge als dem oben angegebenen Code ausführt:</span><span class="sxs-lookup"><span data-stu-id="0a954-255">Below is a sample PowerShell script which performs the same operations as the code above:</span></span> 

```Powershell
# Get needed information from the end user
$adminUrl = Read-Host -Prompt 'Enter the admin URL of your tenant'
$userName = Read-Host -Prompt 'Enter your user name'
$pwd = Read-Host -Prompt 'Enter your password' -AsSecureString
$importFileUrl = Read-Host -Prompt 'Enter the URL to the file located in your tenant'

# Get instances to the Office 365 tenant using CSOM
$uri = New-Object System.Uri -ArgumentList $adminUrl
$context = New-Object Microsoft.SharePoint.Client.ClientContext($uri)

$context.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($userName, $pwd)
$o365 = New-Object Microsoft.Online.SharePoint.TenantManagement.Office365Tenant($context)
$context.Load($o365)

# Type of user identifier ["Email", "CloudId", "PrincipalName"] in the User Profile Service
$userIdType=[Microsoft.Online.SharePoint.TenantManagement.ImportProfilePropertiesUserIdType]::Email

# Name of user identifier property in the JSON
$userLookupKey="idName"

# Create property mapping between the source file property name and the O365 property name
# Notice that we have here 2 custom properties in UPA called 'City' and 'OfficeCode'
$propertyMap = New-Object -type 'System.Collections.Generic.Dictionary[String,String]'
$propertyMap.Add("City", "City")
$propertyMap.Add("Office", "OfficeCode")

# Call to queue UPA property import 
$workItemId = $o365.QueueImportProfileProperties($userIdType, $userLookupKey, $propertyMap, $importFileUrl);

# Execute the CSOM command for queuing the import job
$context.ExecuteQuery();

# Output the unique identifier of the job
Write-Host "Import job created with the following identifier:" $workItemId.Value 
```

## <a name="handling-exceptions"></a><span data-ttu-id="0a954-256">Behandeln von Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="0a954-256">Handling Exceptions</span></span>
<span data-ttu-id="0a954-257"><a name="sectionSection5"></a> Stehen zwei Stufen der Überprüfung wird, wenn diese API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0a954-257"><a name="sectionSection5"> </a> There are two levels of validation when this API is used.</span></span> <span data-ttu-id="0a954-258">Wenn Sie den Importvorgang mit CSOM in die Warteschlange wird eine erste Ebene der Überprüfung der bereitgestellten Werte vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="0a954-258">When you queue the import process with CSOM there will be an initial level of validation of the provided values.</span></span> <span data-ttu-id="0a954-259">Dazu gehören zur Bestätigung, dass die bereitgestellten Zuordnungseigenschaften in der Benutzerprofildienst vorhanden sind und diese Eigenschaften nicht vom Benutzer bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-259">This includes confirmation that the provided mapping properties exist in the User Profile Service and that these properties are not editable by the end user.</span></span> <span data-ttu-id="0a954-260">Wenn die Warteschlange API aufgerufen wird, wird nur eine erste Ebene der Überprüfung angewendet und endgültige Überprüfung der bereitgestellten Informationen erfolgt bei der Importauftrag tatsächlich ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0a954-260">When the queue API is called, only an initial level of validation is applied and final validation of the provided information is performed when the import job is actually executed.</span></span>

<span data-ttu-id="0a954-261">Wenn während der Ausführung des tatsächlichen Importvorgangs für alle Ausnahmen sind, wird eine Protokolldatei mit zusätzlichen Einzelheiten in derselben Dokumentbibliothek generiert, in dem die Importdatei gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="0a954-261">If there are any exceptions during the actual import job execution, a logging file with additional details is generated in the same document library where the import file was located.</span></span> <span data-ttu-id="0a954-262">Protokolldateien für bestimmte Importaufträge werden gespeichert, um eine sub-Ordnern mit dem eindeutigen Bezeichner des Auftrags für bestimmte importieren.</span><span class="sxs-lookup"><span data-stu-id="0a954-262">Log files for specific import jobs are saved to sub folders named using the unique identifier of the specific import job.</span></span>

<span data-ttu-id="0a954-263">Es folgt ein Beispiel für die Ergebnisse der Ausführung ein Importauftrag.</span><span class="sxs-lookup"><span data-stu-id="0a954-263">Below is an example of the results of running an import job.</span></span> <span data-ttu-id="0a954-264">In der folgenden Abbildung sehen Sie zwei Unterordner für zwei unterschiedliche Ausführungen erstellt in der Dokumentbibliothek, in dem die Importdatei gespeichert ist:</span><span class="sxs-lookup"><span data-stu-id="0a954-264">In the picture below, you can see two sub folders for two different executions created in the document library where the import file is stored:</span></span>

![Job-Ausnahme Unterordner](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

<span data-ttu-id="0a954-266">Die aktuelle Protokolldatei wird im Ordner "Sub" gespeichert und können Sie Herunterladen von Office 365 für die detaillierte Analyse:</span><span class="sxs-lookup"><span data-stu-id="0a954-266">The actual log file is saved in the sub folder and you can download that from Office 365 for detailed analysis:</span></span>

![Job-Ausnahme-Protokolldatei](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a><span data-ttu-id="0a954-268">Allgemeine Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="0a954-268">Common Exceptions</span></span>

<span data-ttu-id="0a954-269">In der folgenden Tabelle enthält die typische Ausnahmen aus, die Sie auftreten können, wenn Sie beginnen, mit der Benutzerprofildienst-Bulk-API.</span><span class="sxs-lookup"><span data-stu-id="0a954-269">Following table contains typical exceptions which you could encounter when you start using the User Profile Service bulk API.</span></span>

<span data-ttu-id="0a954-270">Beispiel-Ausnahme</span><span class="sxs-lookup"><span data-stu-id="0a954-270">Example Exception</span></span> | <span data-ttu-id="0a954-271">Details</span><span class="sxs-lookup"><span data-stu-id="0a954-271">Details</span></span>
--- | ---
<span data-ttu-id="0a954-272">_Eigenschaftennamen [mich-Seite] können vom Benutzer bearbeitet werden._</span><span class="sxs-lookup"><span data-stu-id="0a954-272">_Property Names [AboutMe] are editable by user._</span></span> | <span data-ttu-id="0a954-273">Dies beim Aufruf von CSOM-API ausgelöst werden würde der `ExecuteQuery` -Methode, wenn Sie den Auftrag an Ihrem Mandanten zu senden.</span><span class="sxs-lookup"><span data-stu-id="0a954-273">This would be thrown by the CSOM API when you call the `ExecuteQuery` method when submitting the job to your tenant.</span></span> <span data-ttu-id="0a954-274">Die API wird überprüft, dass alle derzeit zugeordnete Eigenschaften nicht Benutzer bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-274">The API will validate that all properties currently being mapped are NOT user editable.</span></span> <span data-ttu-id="0a954-275">Die Ausnahme wird, die-Eigenschaft verweisen, die nicht verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="0a954-275">The exception will point out the property which cannot be used.</span></span> <span data-ttu-id="0a954-276">In diesem Beispiel haben wir versucht, eine JSON-Eigenschaft zum Zuordnen der `AboutMe` -Eigenschaft in die Benutzerprofildienst-Eigenschaften, aber dies ist nicht zulässig, seit `AboutMe` ist eine Benutzereigenschaft bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-276">In this example, we have tried to map a JSON property to the `AboutMe` property in the User Profile Service properties, but this is not allowed since `AboutMe` is a user editable property.</span></span>
<span data-ttu-id="0a954-277">_InvalidProperty - Eigenschaft 'Mich-Seite' vesaj@contoso.com ist, eine Eigenschaft in der Benutzerprofildienst-Anwendung nicht zugeordnet._</span><span class="sxs-lookup"><span data-stu-id="0a954-277">_InvalidProperty - vesaj@contoso.com Property 'AboutMe' is not mapped to any property in the user profile application._</span></span> | <span data-ttu-id="0a954-278">Die Datendatei JSON enthalten eine Eigenschaft, die zur Benutzerprofildienst-Eigenschaft in SharePoint Online nicht zugeordnet wurde.</span><span class="sxs-lookup"><span data-stu-id="0a954-278">The JSON data file contained a property which has not been mapped to the User Profile Service property in SharePoint Online.</span></span> <span data-ttu-id="0a954-279">Dies bedeutet, dass die Quelldatendatei Eigenschaften enthält, für die Sie eine Zuordnung in nicht bereitgestellt haben, die `propertyMap` Parameter.</span><span class="sxs-lookup"><span data-stu-id="0a954-279">This means that the source data file contains properties for which you have not provided a mapping in the `propertyMap` parameter.</span></span> <span data-ttu-id="0a954-280">Sie müssen für jede der Eigenschaften in das JSON-Objekt eine Zuordnungsdefinition verfügen.</span><span class="sxs-lookup"><span data-stu-id="0a954-280">You will need to have a mapping definition for each of the properties in the JSON data object.</span></span>
<span data-ttu-id="0a954-281">_MissingIdentity - fehlt die Identität für das Benutzerobjekt_</span><span class="sxs-lookup"><span data-stu-id="0a954-281">_MissingIdentity - The identity is missing for the user object_</span></span> | <span data-ttu-id="0a954-282">Die Identity-Eigenschaft konnte nicht in das Benutzerobjekt gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-282">The identity property could not be found in the user object.</span></span> <span data-ttu-id="0a954-283">Meistens verursachen, die die `sourceDataIdProperty` -Attribut wird fälschlicherweise festgelegt, für die `QueueImportProfileProperties` Methode.</span><span class="sxs-lookup"><span data-stu-id="0a954-283">The most likely cause is that the `sourceDataIdProperty` attribute is wrongly set for the `QueueImportProfileProperties` method.</span></span> <span data-ttu-id="0a954-284">Stellen Sie sicher, dass Sie die right-Eigenschaft in der Quelldatei JSON haben und Ihr Code/Skript entsprechend dieses Attribut zugewiesen ist.</span><span class="sxs-lookup"><span data-stu-id="0a954-284">Ensure that you have the right property in the JSON source file and that your code/script is assigning this attribute accordingly.</span></span>
<span data-ttu-id="0a954-285">_IdentityNotResolvable unknown@contoso.com Benutzeridentität kann nicht aufgelöst werden_</span><span class="sxs-lookup"><span data-stu-id="0a954-285">_IdentityNotResolvable unknown@contoso.com User identity cannot be resolved_</span></span> | <span data-ttu-id="0a954-286">Die Datendatei, die eine Identität, die nicht aufgelöst werden kann oder ist nicht vorhanden, in dem der Benutzerprofildienst enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="0a954-286">The data file contained an identity, which could not be resolved or was not present in the User Profile Service.</span></span> <span data-ttu-id="0a954-287">In diesem Fall konnte das Benutzerprofil mit e-Mail-Adresse des _unknown@contoso.com_ nicht in der Benutzerprofildienst befinden.</span><span class="sxs-lookup"><span data-stu-id="0a954-287">In this case, the user profile with email of _unknown@contoso.com_ could not be located in the User Profile Service.</span></span>
<span data-ttu-id="0a954-288">_DataFileNotJson - JsonToken EndObject ist nicht gültig für JsonType Array zu schließen. Pfad "Wert", Zeile 8, position 10._</span><span class="sxs-lookup"><span data-stu-id="0a954-288">_DataFileNotJson - JsonToken EndObject is not valid for closing JsonType Array. Path 'value', line 8, position 10._</span></span> | <span data-ttu-id="0a954-289">Format der Importdatei ist keine gültige JSON und das erwartete Format stimmt nicht überein.</span><span class="sxs-lookup"><span data-stu-id="0a954-289">Your import file format is not valid JSON and does not match the expected format.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="0a954-290">Häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="0a954-290">Frequently Asked Questions</span></span>
<span data-ttu-id="0a954-291"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="0a954-291"></span></span>

<span data-ttu-id="0a954-292">**Kann den app-only/Add-in-Berechtigungen mit Code werden ausgeführt?**</span><span class="sxs-lookup"><span data-stu-id="0a954-292">**Can I execute the code using app-only/add-in only permissions?**</span></span>

<span data-ttu-id="0a954-293">Ja, müssen Sie die Client-Id und geheimen Clientschlüssel werden sollen, führen Sie die APIs registrieren.</span><span class="sxs-lookup"><span data-stu-id="0a954-293">Yes, you’ll need to register the client id and secret to be able to execute the APIs.</span></span> <span data-ttu-id="0a954-294">Da der tatsächliche Import der Datei mit der Identität des Aufrufers nicht synchron auftritt, funktioniert dies ohne Probleme.</span><span class="sxs-lookup"><span data-stu-id="0a954-294">Since the actual import of the file does not occur synchronously with the identity of the caller, this works without any issues.</span></span>

<span data-ttu-id="0a954-295">**Diese API ist Aktualisieren von Eigenschaften in den Benutzerprofildienst, doch wie würde ich diese Eigenschaften im Mandanten erstellen?**</span><span class="sxs-lookup"><span data-stu-id="0a954-295">**This API is updating properties in the User Profile Service, but how would I create those properties in the tenant?**</span></span>

<span data-ttu-id="0a954-296">Es ist keine remote-API, um benutzerdefinierte Profileigenschaften programmgesteuert erstellen Dies manuelle Verarbeitung der angegebenen Mandanten einmal pro ausgeführt werden muss.</span><span class="sxs-lookup"><span data-stu-id="0a954-296">There’s no remote API to create custom user profile properties programmatically, so this is manual operation which needs to be completed once per given tenant.</span></span> <span data-ttu-id="0a954-297">Sie können Sie [in diesem Artikel](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) eine Anleitung zum Erstellen dieser benutzerdefinierten Eigenschaften verweisen.</span><span class="sxs-lookup"><span data-stu-id="0a954-297">You can refer to [this article](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) for instructions on how to create these custom properties.</span></span>

<span data-ttu-id="0a954-298">**Ist diese Funktion in lokalen SharePoint?**</span><span class="sxs-lookup"><span data-stu-id="0a954-298">**Is this capability available in on-premises SharePoint?**</span></span>

<span data-ttu-id="0a954-299">Diese Funktion ist leider derzeit nur für SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0a954-299">Unfortunately, this capability is currently only for SharePoint Online.</span></span> <span data-ttu-id="0a954-300">In der lokalen SharePoint würden diese Funktion nützlich, aber nicht als kritisch sein, da die Zuordnung Attribut in die lokale Benutzerprofildienst-Anwendung geändert werden können.</span><span class="sxs-lookup"><span data-stu-id="0a954-300">In on-premises SharePoint this capability would be useful but not as critical since you can modify the attribute mapping in the on-premises User Profile Service Application.</span></span> <span data-ttu-id="0a954-301">Sie können auch Importieren von Benutzerprofil-Attribute von Business Connectivity Service (BCS) in SharePoint 2013 nutzen.</span><span class="sxs-lookup"><span data-stu-id="0a954-301">You can also take advantage of importing user profile attributes using the Business Connectivity Service (BCS) in SharePoint 2013.</span></span> <span data-ttu-id="0a954-302">Jedoch ist diese Option nicht verfügbar in SharePoint 2016, was bedeutet, dass für SharePoint 2016 die einzige Option derzeit ist Anpassungen Implementieren des Benutzers Profil Webdienste nutzen.</span><span class="sxs-lookup"><span data-stu-id="0a954-302">However, this option is not available in SharePoint 2016, which means that for SharePoint 2016 the only option currently is to implement customizations which take advantage of the user profile web services.</span></span>

<span data-ttu-id="0a954-303">**Konnte diese API werden verwendet, für das Synchronisieren von Benutzerprofil Eigenschaftswerte über meine lokalen SharePoint 2013 oder 2016 Mastbetriebs mit SharePoint Online?**</span><span class="sxs-lookup"><span data-stu-id="0a954-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span></span>
<span data-ttu-id="0a954-304">Ja, kann der lokale SharePoint genau wie alle anderen Quellsystem verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-304">Yes, on-premises SharePoint can be used just like any other source system.</span></span> <span data-ttu-id="0a954-305">Sie müssen die Benutzerprofil Werte aus Ihrer lokalen SharePoint das JSON-Dateiformat exportieren und klicken Sie dann der Prozess wäre genau das Importieren von Werten aus einem anderen System identisch.</span><span class="sxs-lookup"><span data-stu-id="0a954-305">You'll need to export the user profile values from your on-premises SharePoint to the JSON file format and then the process would be exactly the same as importing values from any other system.</span></span>

<span data-ttu-id="0a954-306">**Kann ich Zeichenfolge basiert, mehrwertige Eigenschaften Importieren?**</span><span class="sxs-lookup"><span data-stu-id="0a954-306">**Can I import string based, multi-value properties?**</span></span>
<span data-ttu-id="0a954-307">Nein, ist dies nicht aktuell mit diese API unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0a954-307">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="0a954-308">**Welche Berechtigungen sind zum Ausführen dieser API? erforderlich?**</span><span class="sxs-lookup"><span data-stu-id="0a954-308">**What permissions are required for executing this API??**</span></span>
<span data-ttu-id="0a954-309">Sie müssen derzeit globaler Administrator-Berechtigungen verfügen.</span><span class="sxs-lookup"><span data-stu-id="0a954-309">You will need to have Global Admin permissions currently.</span></span> <span data-ttu-id="0a954-310">SharePoint Admin ist nicht ausreichend.</span><span class="sxs-lookup"><span data-stu-id="0a954-310">SharePoint Admin is not sufficient.</span></span>

<span data-ttu-id="0a954-311">**Kann ich die Taxonomie basierende Eigenschaften Importieren?**</span><span class="sxs-lookup"><span data-stu-id="0a954-311">**Can I import taxonomy based properties?**</span></span>
<span data-ttu-id="0a954-312">Nein, ist dies nicht aktuell mit diese API unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0a954-312">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="0a954-313">**Was passiert, wenn ich definieren eine Zuordnung, in der Code, der nicht verwendet wird oder Eigenschaften in der JSON-Datei, die nicht zugeordnet werden?**</span><span class="sxs-lookup"><span data-stu-id="0a954-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span></span>
<span data-ttu-id="0a954-314">Wenn Ihr Code/Skript definiert eine Zuordnung, die nicht verwendet wird oder die Datendatei keine Eigenschaften für die Zuordnung enthält, die Ausführung ohne Ausnahmen fortgesetzt wird und der Import wird angewendet werden soll, basierend auf den zugeordneten Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="0a954-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span></span> <span data-ttu-id="0a954-315">Wenn Sie, jedoch eine Eigenschaft in der Datei JSON, die nicht zugeordnet ist verfügen, wird der Importvorgang abgebrochen werden, und Details der Ausnahme in der Protokolldatei für die Ausführung des Auftrags bestimmte bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span></span>

<span data-ttu-id="0a954-316">**Was geschieht, wenn ich muss eine benutzerdefinierte Eigenschaften zu aktualisieren, die die Größe Einschränkungen dieser Massen API sprengen (d. h. > 2 GB-Datei oder > 500.000 Eigenschaften)?**</span><span class="sxs-lookup"><span data-stu-id="0a954-316">**What if I have a need to update custom properties that are beyond the size limitations of this bulk API (i.e. >2 GB file or >500,000 properties)?**</span></span>
<span data-ttu-id="0a954-317">Sie müssen Ihre Aufträge auslösen entsprechend durch mehrere Aufträge in der Abfolge (d. h. einem Auftrag zu einem Zeitpunkt mit der maximale Grenzwert für diese API Enddatum) Batch.</span><span class="sxs-lookup"><span data-stu-id="0a954-317">You would need to batch your jobs accordingly by triggering multiple jobs in sequence (i.e. finishing one job at a time with the maximum limit on this API).</span></span> <span data-ttu-id="0a954-318">Sie sollten erwarten, diese hoher Bandbreite Imports eine lange dauern werden.</span><span class="sxs-lookup"><span data-stu-id="0a954-318">You should expect these high bandwidth imports will take a long time to complete.</span></span> <span data-ttu-id="0a954-319">Darüber hinaus sollten Sie die Importaufträge nur für Delta Änderungen benutzerdefinierter Profileigenschaften, sondern eine umfassende Auswahl an Werte in allen Projekten importieren in optimieren.</span><span class="sxs-lookup"><span data-stu-id="0a954-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span></span>

<span data-ttu-id="0a954-320">**Welche Azure Active Directory-Attribute sind Sync wird standardmäßig SharePoint Online Benutzerprofil mussten?**</span><span class="sxs-lookup"><span data-stu-id="0a954-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span></span>
<span data-ttu-id="0a954-321">Finden Sie in der folgenden Tabelle für die offizielle Liste der synchronisierten Attribute und deren Zuordnung zwischen Azure Active Directory und SharePoint Online User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="0a954-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span></span>

<span data-ttu-id="0a954-322">Azure-Directory-Attribut</span><span class="sxs-lookup"><span data-stu-id="0a954-322">Azure Directory Attribute</span></span>  | <span data-ttu-id="0a954-323">SharePoint Online-Profileigenschaft</span><span class="sxs-lookup"><span data-stu-id="0a954-323">SharePoint Online Profile Property</span></span>
---------|----------
<span data-ttu-id="0a954-324">Objekt-SID</span><span class="sxs-lookup"><span data-stu-id="0a954-324">ObjectSid</span></span> | <span data-ttu-id="0a954-325">SPS-SavedSID</span><span class="sxs-lookup"><span data-stu-id="0a954-325">SPS-SavedSID</span></span>
<span data-ttu-id="0a954-326">MSOnline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-326">msonline-UserPrincipalName</span></span> | <span data-ttu-id="0a954-327">Benutzername</span><span class="sxs-lookup"><span data-stu-id="0a954-327">UserName</span></span>
<span data-ttu-id="0a954-328">MSOnline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-328">msonline-UserPrincipalName</span></span> | <span data-ttu-id="0a954-329">Kontoname</span><span class="sxs-lookup"><span data-stu-id="0a954-329">AccountName</span></span>
<span data-ttu-id="0a954-330">MSOnline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-330">msonline-UserPrincipalName</span></span> | <span data-ttu-id="0a954-331">SPS-ClaimID</span><span class="sxs-lookup"><span data-stu-id="0a954-331">SPS-ClaimID</span></span>
<span data-ttu-id="0a954-332">MSOnline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-332">msonline-UserPrincipalName</span></span> | <span data-ttu-id="0a954-333">SPS-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0a954-333">SPS-UserPrincipalName</span></span>
<span data-ttu-id="0a954-334">Vorname</span><span class="sxs-lookup"><span data-stu-id="0a954-334">GivenName</span></span> | <span data-ttu-id="0a954-335">Vorname</span><span class="sxs-lookup"><span data-stu-id="0a954-335">FirstName</span></span>
<span data-ttu-id="0a954-336">Sn</span><span class="sxs-lookup"><span data-stu-id="0a954-336">sn</span></span> | <span data-ttu-id="0a954-337">Nachname</span><span class="sxs-lookup"><span data-stu-id="0a954-337">LastName</span></span>
<span data-ttu-id="0a954-338">Manager</span><span class="sxs-lookup"><span data-stu-id="0a954-338">Manager</span></span> | <span data-ttu-id="0a954-339">Manager</span><span class="sxs-lookup"><span data-stu-id="0a954-339">Manager</span></span>
<span data-ttu-id="0a954-340">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0a954-340">DisplayName</span></span> | <span data-ttu-id="0a954-341">PreferredName</span><span class="sxs-lookup"><span data-stu-id="0a954-341">PreferredName</span></span>
<span data-ttu-id="0a954-342">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="0a954-342">telephoneNumber</span></span> | <span data-ttu-id="0a954-343">WorkPhone</span><span class="sxs-lookup"><span data-stu-id="0a954-343">WorkPhone</span></span>
<span data-ttu-id="0a954-344">Proxyadressen</span><span class="sxs-lookup"><span data-stu-id="0a954-344">proxyAddresses</span></span> | <span data-ttu-id="0a954-345">WorkEmail</span><span class="sxs-lookup"><span data-stu-id="0a954-345">WorkEmail</span></span>
<span data-ttu-id="0a954-346">Proxyadressen</span><span class="sxs-lookup"><span data-stu-id="0a954-346">proxyAddresses</span></span> | <span data-ttu-id="0a954-347">SPS-"SipAddress"</span><span class="sxs-lookup"><span data-stu-id="0a954-347">SPS-SIPAddress</span></span>
<span data-ttu-id="0a954-348">PhysicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="0a954-348">PhysicalDeliveryOfficeName</span></span> | <span data-ttu-id="0a954-349">Office</span><span class="sxs-lookup"><span data-stu-id="0a954-349">Office</span></span>
<span data-ttu-id="0a954-350">Titel</span><span class="sxs-lookup"><span data-stu-id="0a954-350">Title</span></span> | <span data-ttu-id="0a954-351">Titel</span><span class="sxs-lookup"><span data-stu-id="0a954-351">Title</span></span>
<span data-ttu-id="0a954-352">Titel</span><span class="sxs-lookup"><span data-stu-id="0a954-352">Title</span></span> | <span data-ttu-id="0a954-353">SPS-JobTitle</span><span class="sxs-lookup"><span data-stu-id="0a954-353">SPS-JobTitle</span></span>
<span data-ttu-id="0a954-354">Abteilung</span><span class="sxs-lookup"><span data-stu-id="0a954-354">Department</span></span> | <span data-ttu-id="0a954-355">Abteilung</span><span class="sxs-lookup"><span data-stu-id="0a954-355">Department</span></span>
<span data-ttu-id="0a954-356">Abteilung</span><span class="sxs-lookup"><span data-stu-id="0a954-356">Department</span></span> | <span data-ttu-id="0a954-357">SPS-Abteilung</span><span class="sxs-lookup"><span data-stu-id="0a954-357">SPS-Department</span></span>
<span data-ttu-id="0a954-358">Objekt-GUID</span><span class="sxs-lookup"><span data-stu-id="0a954-358">ObjectGuid</span></span> | <span data-ttu-id="0a954-359">ADGuid</span><span class="sxs-lookup"><span data-stu-id="0a954-359">ADGuid</span></span>
<span data-ttu-id="0a954-360">WWWHomePage</span><span class="sxs-lookup"><span data-stu-id="0a954-360">WWWHomePage</span></span> | <span data-ttu-id="0a954-361">PublicSiteRedirect</span><span class="sxs-lookup"><span data-stu-id="0a954-361">PublicSiteRedirect</span></span>
<span data-ttu-id="0a954-362">DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="0a954-362">DistinguishedName</span></span> | <span data-ttu-id="0a954-363">SPS-DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="0a954-363">SPS-DistinguishedName</span></span>
<span data-ttu-id="0a954-364">MsOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="0a954-364">msOnline-ObjectId</span></span> | <span data-ttu-id="0a954-365">MsOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="0a954-365">msOnline-ObjectId</span></span>
<span data-ttu-id="0a954-366">PreferredLanguage</span><span class="sxs-lookup"><span data-stu-id="0a954-366">PreferredLanguage</span></span> | <span data-ttu-id="0a954-367">SPS-"MUILanguages"</span><span class="sxs-lookup"><span data-stu-id="0a954-367">SPS-MUILanguages</span></span>
<span data-ttu-id="0a954-368">msExchHideFromAddressList</span><span class="sxs-lookup"><span data-stu-id="0a954-368">msExchHideFromAddressList</span></span> | <span data-ttu-id="0a954-369">SPS-HideFromAddressLists</span><span class="sxs-lookup"><span data-stu-id="0a954-369">SPS-HideFromAddressLists</span></span>
<span data-ttu-id="0a954-370">msExchRecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="0a954-370">msExchRecipientTypeDetails</span></span> | <span data-ttu-id="0a954-371">SPS-"RecipientTypeDetails"</span><span class="sxs-lookup"><span data-stu-id="0a954-371">SPS-RecipientTypeDetails</span></span>
<span data-ttu-id="0a954-372">MSOnline groupType</span><span class="sxs-lookup"><span data-stu-id="0a954-372">msonline-groupType</span></span> | <span data-ttu-id="0a954-373">IsUnifiedGroup</span><span class="sxs-lookup"><span data-stu-id="0a954-373">IsUnifiedGroup</span></span>
<span data-ttu-id="0a954-374">MsOnline IsPublic</span><span class="sxs-lookup"><span data-stu-id="0a954-374">msOnline-IsPublic</span></span> | <span data-ttu-id="0a954-375">IsPublic</span><span class="sxs-lookup"><span data-stu-id="0a954-375">IsPublic</span></span>
<span data-ttu-id="0a954-376">MsOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="0a954-376">msOnline-ObjectId</span></span> | <span data-ttu-id="0a954-377">MsOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="0a954-377">msOnline-ObjectId</span></span>
<span data-ttu-id="0a954-378">MsOnline UserType</span><span class="sxs-lookup"><span data-stu-id="0a954-378">msOnline-UserType</span></span> | <span data-ttu-id="0a954-379">SPS-Benutzertyp</span><span class="sxs-lookup"><span data-stu-id="0a954-379">SPS-UserType</span></span>
<span data-ttu-id="0a954-380">GroupType</span><span class="sxs-lookup"><span data-stu-id="0a954-380">GroupType</span></span> | <span data-ttu-id="0a954-381">GroupType</span><span class="sxs-lookup"><span data-stu-id="0a954-381">GroupType</span></span>
<span data-ttu-id="0a954-382">SPO-IsSharePointOnlineObject</span><span class="sxs-lookup"><span data-stu-id="0a954-382">SPO-IsSharePointOnlineObject</span></span> | <span data-ttu-id="0a954-383">SPO-IsSPO</span><span class="sxs-lookup"><span data-stu-id="0a954-383">SPO-IsSPO</span></span>

