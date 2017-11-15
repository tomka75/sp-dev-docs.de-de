---
title: "BCS-Client-Objektmodellreferenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe7d12a3-6ea9-47f9-b69e-f66da9e661dc
ms.openlocfilehash: 648dd7c17e0ac4c7869d93df88ae155dcfde7b84
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="bcs-client-object-model-reference-for-sharepoint"></a><span data-ttu-id="47b7b-102">BCS-Client-Objektmodellreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-102">BCS client object model reference for SharePoint</span></span>

  
    
    
![Klassenbibliotheken und -verweise](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="47b7b-p101">Informationen Sie zu den Objekten, die für das Erstellen von clientseitigen Skripts mithilfe des Clientobjektmodells SharePoint Zugriff auf externe Daten verfügbar gemacht werden, indem Business Connectivity Services (BCS) verfügbar sind. Die folgenden Objekte stehen für die Erstellung von clientseitigen Skripts mithilfe des Clientobjektmodells SharePoint Zugriff auf externe Daten, die von Business Connectivity Services (BCS) verfügbar gemacht wird. Die BCS-Objektmodell Komponenten, die dem Client-Objektmodell verfügbar gemacht werden, in denen Microsoft.SharePoint.Client.dll befinden.</span><span class="sxs-lookup"><span data-stu-id="47b7b-p101">Learn about the objects that are available for creating client-side scripts using the SharePoint client object model to access external data exposed by Business Connectivity Services (BCS). The following objects are available for creating client-side scripts using the SharePoint client object model to access external data that is exposed by Business Connectivity Services (BCS). The BCS object model components that are exposed to the client object model are located in Microsoft.SharePoint.Client.dll.</span></span>
  
    
    


## <a name="entity-object"></a><span data-ttu-id="47b7b-107">Entity-Objekt</span><span class="sxs-lookup"><span data-stu-id="47b7b-107">Entity object</span></span>
<span data-ttu-id="47b7b-108"><a name="bkmk_Entity"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-108"></span></span>

<span data-ttu-id="47b7b-p102">Das **Entity** -Objekt stellt im Wesentlichen eine Tabelle in einer Datenbank. Die Methoden und Eigenschaften, die hier aufgeführten die Objekte anzeigen, die bearbeitet werden können durch Verwendung der Clientbibliothek Code. Jede dieser Anrufe ordnet direkt zu einem Modell-Anruf von Server-Objekt. Jedoch können sie von einem getrennten Client, wie in einem Webbrowser mit JavaScript aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="47b7b-p102">The **Entity** object essentially represents a table in a database. The methods and properties presented here show the objects that can be manipulated through the use of the client code library. Each of these calls maps directly to a server object model call. However, they are callable by a detached client, such as in a web browser using JavaScript.</span></span>
  
    
    

<span data-ttu-id="47b7b-113">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-113">**Methods**</span></span>


|<span data-ttu-id="47b7b-114">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-114">**Methods**</span></span>|<span data-ttu-id="47b7b-115">**Methodensignatur**</span><span class="sxs-lookup"><span data-stu-id="47b7b-115">**Method signature**</span></span>|<span data-ttu-id="47b7b-116">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-116">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-117">**Create**</span><span class="sxs-lookup"><span data-stu-id="47b7b-117">**Create**</span></span> <br/> | `Identity Create(FieldValueDictionary fieldValues, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-118">**FindSpecificDefault**</span><span class="sxs-lookup"><span data-stu-id="47b7b-118">**FindSpecificDefault**</span></span> <br/> | `EntityInstance FindSpecificDefault(Identity identity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-119">**FindspecificByBdcIDDefault**</span><span class="sxs-lookup"><span data-stu-id="47b7b-119">**FindspecificByBdcIDDefault**</span></span> <br/> | `EntityInstance FindSpecific(Identity identity, string specificFinderName, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-120">**FindSpecificByBdcID**</span><span class="sxs-lookup"><span data-stu-id="47b7b-120">**FindSpecificByBdcID**</span></span> <br/> | `EntityInstance FindSpecificByBdcIDDefault(string BdcIdentity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-121">**GetCreatorView**</span><span class="sxs-lookup"><span data-stu-id="47b7b-121">**GetCreatorView**</span></span> <br/> | `EntityInstance FindSpecificByBdcID(string BdcIdentity, string specificFinderName,LobSystemInstance LobSystemInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-122">**GetDefaultSpecificFinderView**</span><span class="sxs-lookup"><span data-stu-id="47b7b-122">**GetDefaultSpecificFinderView**</span></span> <br/> | `View GetCreatorView(string methodInstanceName)` <br/> ||
|<span data-ttu-id="47b7b-123">**GetSpecificFinderView_Client**</span><span class="sxs-lookup"><span data-stu-id="47b7b-123">**GetSpecificFinderView_Client**</span></span> <br/> | `View GetDefaultSpecificFinderView()` <br/> ||
|<span data-ttu-id="47b7b-124">**GetUpdaterView_Client**</span><span class="sxs-lookup"><span data-stu-id="47b7b-124">**GetUpdaterView_Client**</span></span> <br/> | `View GetSpecificFinderView_Client( string specificFinderName)` <br/> ||
|<span data-ttu-id="47b7b-125">**GetIdentifiers**</span><span class="sxs-lookup"><span data-stu-id="47b7b-125">**GetIdentifiers**</span></span> <br/> | `View GetUpdaterView_Client(string updaterName)` <br/> ||
|<span data-ttu-id="47b7b-126">**GetIdentifiers()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-126">**GetIdentifiers()**</span></span> <br/> |||
   

<span data-ttu-id="47b7b-127">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-127">**Properties**</span></span>


|<span data-ttu-id="47b7b-128">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-128">**Property**</span></span>|<span data-ttu-id="47b7b-129">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-129">**Description**</span></span>|
|:-----|:-----|
| `long EstimatedInstanceCount { get; }` <br/> |<span data-ttu-id="47b7b-130">Ruft die Anzahl der erwarteten externen Elemente dieses externen Inhaltstyps ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-130">Gets the number of expected external items of this external content type.</span></span>  <br/> |
| `string Name { get; }` <br/> |<span data-ttu-id="47b7b-131">Ruft den Namen des Metadatenobjekts ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-131">Gets the name of the metadata object.</span></span>  <br/> |
| `string Namespace { get; }` <br/> |<span data-ttu-id="47b7b-132">Ruft den Namespace der angegebenen Daten-Klasse.</span><span class="sxs-lookup"><span data-stu-id="47b7b-132">Gets the namespace of the given data class.</span></span>  <br/> |
| `int GetIdentifierCount()` <br/> ||
   

## <a name="entityinstance-method"></a><span data-ttu-id="47b7b-133">EntityInstance-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-133">EntityInstance method</span></span>
<span data-ttu-id="47b7b-134"><a name="bkmk_EntityInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-134"></span></span>


<span data-ttu-id="47b7b-135">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-135">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-136">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-136">**Managed**</span></span>|<span data-ttu-id="47b7b-137">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-137">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-138">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-138">**Microsoft.BusinessData.Runtime. IFilter**</span></span> <br/> |<span data-ttu-id="47b7b-139">**SP.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-139">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="47b7b-140">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-140">**Methods**</span></span>


|<span data-ttu-id="47b7b-141">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-141">**Method**</span></span>|<span data-ttu-id="47b7b-142">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-142">**Return type**</span></span>|<span data-ttu-id="47b7b-143">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-143">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-144">**Delete**</span><span class="sxs-lookup"><span data-stu-id="47b7b-144">**Delete**</span></span> <br/> |<span data-ttu-id="47b7b-145">void</span><span class="sxs-lookup"><span data-stu-id="47b7b-145">void</span></span>  <br/> |<span data-ttu-id="47b7b-146">Löscht das externe Element.</span><span class="sxs-lookup"><span data-stu-id="47b7b-146">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="47b7b-147">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="47b7b-147">**FromXml**</span></span> <br/> |<span data-ttu-id="47b7b-148">void</span><span class="sxs-lookup"><span data-stu-id="47b7b-148">void</span></span>  <br/> |<span data-ttu-id="47b7b-149">Die Werte festgelegt aus der angegebenen XML in diesem Wörterbuch.</span><span class="sxs-lookup"><span data-stu-id="47b7b-149">Sets the values in this dictionary from specified XML.</span></span>  <br/> <span data-ttu-id="47b7b-150">**Methodensignatur**          `FromXml(string xml)`</span><span class="sxs-lookup"><span data-stu-id="47b7b-150">**Method signature**          `FromXml(string xml)`</span></span> <br/> |
|<span data-ttu-id="47b7b-151">**GetIdentity**</span><span class="sxs-lookup"><span data-stu-id="47b7b-151">**GetIdentity**</span></span> <br/> |<span data-ttu-id="47b7b-152">Identität</span><span class="sxs-lookup"><span data-stu-id="47b7b-152">Identity</span></span>  <br/> |<span data-ttu-id="47b7b-153">Ruft die Identität des externen Elements ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-153">Gets the identity of this External Item.</span></span>  <br/> |
|<span data-ttu-id="47b7b-154">**Delete**</span><span class="sxs-lookup"><span data-stu-id="47b7b-154">**Delete**</span></span> <br/> |<span data-ttu-id="47b7b-155">void</span><span class="sxs-lookup"><span data-stu-id="47b7b-155">void</span></span>  <br/> |<span data-ttu-id="47b7b-156">Löscht das externe Element.</span><span class="sxs-lookup"><span data-stu-id="47b7b-156">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="47b7b-157">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="47b7b-157">**ToXml**</span></span> <br/> |<span data-ttu-id="47b7b-158">string</span><span class="sxs-lookup"><span data-stu-id="47b7b-158">string</span></span>  <br/> |<span data-ttu-id="47b7b-159">Ruft die Werte im XML-Format ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-159">Retrieves the values in XML format.</span></span>  <br/> |
|<span data-ttu-id="47b7b-160">**Update**</span><span class="sxs-lookup"><span data-stu-id="47b7b-160">**Update**</span></span> <br/> |<span data-ttu-id="47b7b-161">void</span><span class="sxs-lookup"><span data-stu-id="47b7b-161">void</span></span>  <br/> |<span data-ttu-id="47b7b-162">Sendet Änderungen an externen Elements an.</span><span class="sxs-lookup"><span data-stu-id="47b7b-162">Submits the changes made to the External Item.</span></span>  <br/> |
   

  
    
    

<span data-ttu-id="47b7b-163">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-163">**Properties**</span></span>


|<span data-ttu-id="47b7b-164">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-164">**Property**</span></span>|<span data-ttu-id="47b7b-165">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-165">**Return type**</span></span>|<span data-ttu-id="47b7b-166">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-166">**Description**</span></span>|
|:-----|:-----|:-----|
| `this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="47b7b-167">Object</span><span class="sxs-lookup"><span data-stu-id="47b7b-167">Object</span></span>  <br/> |<span data-ttu-id="47b7b-168">Dient zum Abrufen oder Festlegen des Werts des Felds, die durch die punktierte Schreibweise bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="47b7b-168">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="47b7b-169">string</span><span class="sxs-lookup"><span data-stu-id="47b7b-169">string</span></span>  <br/> ||
   

## <a name="entityview-method"></a><span data-ttu-id="47b7b-170">EntityView-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-170">EntityView method</span></span>
<span data-ttu-id="47b7b-171"><a name="bkmk_entityview"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-171"></span></span>

<span data-ttu-id="47b7b-172">Gibt eine benutzerdefinierte Ansicht der **Entität** Daten</span><span class="sxs-lookup"><span data-stu-id="47b7b-172">Specifies a customized view of the **Entity** data</span></span>
  
    
    

<span data-ttu-id="47b7b-173">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-173">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-174">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-174">**Managed**</span></span>|<span data-ttu-id="47b7b-175">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-175">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-176">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="47b7b-176">**Microsoft.BusinessData.MetadataModel. IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-177">**SP.BusinessData**</span><span class="sxs-lookup"><span data-stu-id="47b7b-177">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="47b7b-178">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-178">**Methods**</span></span>


|<span data-ttu-id="47b7b-179">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-179">**Method**</span></span>|<span data-ttu-id="47b7b-180">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-180">**Return type**</span></span>|<span data-ttu-id="47b7b-181">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-181">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-182">**GetDefaultValues_Client()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-182">**GetDefaultValues_Client()**</span></span> <br/> |<span data-ttu-id="47b7b-183">**FieldValueDictionary**</span><span class="sxs-lookup"><span data-stu-id="47b7b-183">**FieldValueDictionary method**</span></span> <br/> |<span data-ttu-id="47b7b-184">Ruft ein Wörterbuch der Feld-Wert, der die Standardwerte für diese Ansicht enthält.</span><span class="sxs-lookup"><span data-stu-id="47b7b-184">Gets a field value dictionary that contains the default values for this view.</span></span>  <br/> |
|<span data-ttu-id="47b7b-185">**GetXmlSchema()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-185">**GetXmlSchema()**</span></span> <br/> |<span data-ttu-id="47b7b-186">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-186">**string**</span></span> <br/> |<span data-ttu-id="47b7b-187">Ruft das XML-Schema der Ansicht ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-187">Gets the XML Schema of the view.</span></span>  <br/> |
|<span data-ttu-id="47b7b-188">**GetType(string fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="47b7b-188">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="47b7b-189">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-189">**string**</span></span> <br/> |<span data-ttu-id="47b7b-190">Ruft den Typ des angegebenen Felds ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-190">Gets the type of the specified field.</span></span>  <br/> |
|<span data-ttu-id="47b7b-191">**GetType(string fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="47b7b-191">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="47b7b-192">**TypeDescriptor**</span><span class="sxs-lookup"><span data-stu-id="47b7b-192">**TypeDescriptor**</span></span> <br/> |<span data-ttu-id="47b7b-193">Ruft das **TypeDescriptor** -Objekt, das die angegebene punktierte Schreibweise entspricht.</span><span class="sxs-lookup"><span data-stu-id="47b7b-193">Gets the **TypeDescriptor** object that corresponds to the given dot notation.</span></span> <br/> |
   

<span data-ttu-id="47b7b-194">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-194">**Properties**</span></span>


|<span data-ttu-id="47b7b-195">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-195">**Property**</span></span>|<span data-ttu-id="47b7b-196">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-196">**Return type**</span></span>|<span data-ttu-id="47b7b-197">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-197">**Description**</span></span>|
|:-----|:-----|:-----|
| `Fields { get; }` <br/> |<span data-ttu-id="47b7b-198">**FieldCollection**</span><span class="sxs-lookup"><span data-stu-id="47b7b-198">**FieldCollection**</span></span> <br/> |<span data-ttu-id="47b7b-199">Ruft die Auflistung von Feldern in der Ansicht ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-199">Gets the collection of fields in the view.</span></span>  <br/> |
| `Name { get; }` <br/> |<span data-ttu-id="47b7b-200">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-200">**string**</span></span> <br/> |<span data-ttu-id="47b7b-201">Ruft den Namen dieses **View** -Objekts</span><span class="sxs-lookup"><span data-stu-id="47b7b-201">Gets the name of this **View** object</span></span> <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="47b7b-202">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-202">**string**</span></span> <br/> |<span data-ttu-id="47b7b-203">Ruft den Namen der spezifischen Finder- **MethodInstance**, die in dieser Ansicht an gebunden ist.</span><span class="sxs-lookup"><span data-stu-id="47b7b-203">Retrieves the name of the specific finder **MethodInstance** that this view is tied to.</span></span> <br/> |
   

## <a name="lobsystem-method"></a><span data-ttu-id="47b7b-204">LobSystem-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-204">LobSystem method</span></span>
<span data-ttu-id="47b7b-205"><a name="bkmk_LobSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-205"></span></span>


  
    
    

<span data-ttu-id="47b7b-206">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-206">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-207">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-207">**Managed**</span></span>|<span data-ttu-id="47b7b-208">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-208">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-209">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="47b7b-209">**Microsoft.BusinessData.MetadataModel. IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-210">**SP.BusinessData**</span><span class="sxs-lookup"><span data-stu-id="47b7b-210">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="47b7b-211">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-211">**Methods**</span></span>


|<span data-ttu-id="47b7b-212">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-212">**Method**</span></span>|<span data-ttu-id="47b7b-213">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-213">**Return type**</span></span>|<span data-ttu-id="47b7b-214">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-214">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-215">**GetLobSystemInstances()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-215">**GetLobSystemInstances()**</span></span> <br/> |<span data-ttu-id="47b7b-216">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-216">**void**</span></span> <br/> |<span data-ttu-id="47b7b-217">Gibt die Liste der LOB-Systeminstanzen an.</span><span class="sxs-lookup"><span data-stu-id="47b7b-217">Gives the list of LOB system instances.</span></span>  <br/> |
|<span data-ttu-id="47b7b-218">**Name**</span><span class="sxs-lookup"><span data-stu-id="47b7b-218">**Name**</span></span> <br/> |<span data-ttu-id="47b7b-219">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-219">**void**</span></span> <br/> |<span data-ttu-id="47b7b-220">Ruft den Namen der **LobSystem**ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-220">Gets the name of the **LobSystem**.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-221">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-221">**Properties**</span></span>


|<span data-ttu-id="47b7b-222">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-222">**Property**</span></span>|<span data-ttu-id="47b7b-223">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-223">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-224">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-224">None.</span></span>  <br/> ||
   

## <a name="lobsysteminstance-method"></a><span data-ttu-id="47b7b-225">LobSystemInstance-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-225">LobSystemInstance method</span></span>
<span data-ttu-id="47b7b-226"><a name="bkmk_LobSystemInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-226"></span></span>


  
    
    

<span data-ttu-id="47b7b-227">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-227">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-228">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-228">**Managed**</span></span>|<span data-ttu-id="47b7b-229">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-229">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-230">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="47b7b-230">**Microsoft.BusinessData.MetadataModel. IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-231">**SP.BusinessData**</span><span class="sxs-lookup"><span data-stu-id="47b7b-231">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="47b7b-232">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-232">**Methods**</span></span>


|<span data-ttu-id="47b7b-233">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-233">**Method**</span></span>|<span data-ttu-id="47b7b-234">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-234">**Return type**</span></span>|<span data-ttu-id="47b7b-235">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-235">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-236">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-236">None.</span></span>  <br/> |<span data-ttu-id="47b7b-237">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-237">**void**</span></span> <br/> ||
   

<span data-ttu-id="47b7b-238">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-238">**Properties**</span></span>


|<span data-ttu-id="47b7b-239">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-239">**Property**</span></span>|<span data-ttu-id="47b7b-240">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-240">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-241">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-241">None.</span></span>  <br/> ||
   

## <a name="identifier-method"></a><span data-ttu-id="47b7b-242">ID-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-242">Identifier method</span></span>
<span data-ttu-id="47b7b-243"><a name="bkmk_Identifier"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-243"></span></span>


  
    
    

<span data-ttu-id="47b7b-244">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-244">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-245">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-245">**Managed**</span></span>|<span data-ttu-id="47b7b-246">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-246">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-247">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="47b7b-247">**Microsoft.BusinessData.MetadataModel. IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-248">**SP.BusinessData**</span><span class="sxs-lookup"><span data-stu-id="47b7b-248">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="47b7b-249">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-249">**Methods**</span></span>


|<span data-ttu-id="47b7b-250">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-250">**Method**</span></span>|<span data-ttu-id="47b7b-251">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-251">**Return type**</span></span>|<span data-ttu-id="47b7b-252">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-252">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-253">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-253">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-254">**bool**</span><span class="sxs-lookup"><span data-stu-id="47b7b-254">**bool**</span></span> <br/> |<span data-ttu-id="47b7b-255">Bestimmt, ob das Metadatenobjekt lokalisierten Anzeigenamen enthält.</span><span class="sxs-lookup"><span data-stu-id="47b7b-255">Determines whether the metadata object contains localized display name.</span></span>  <br/> |
|<span data-ttu-id="47b7b-256">**GetDefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-256">**GetDefaultDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-257">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-257">**string**</span></span> <br/> |<span data-ttu-id="47b7b-258">Der standardmäßige Anzeigename zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="47b7b-258">Returns the default display name.</span></span>  <br/> |
|<span data-ttu-id="47b7b-259">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-259">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-260">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-260">**string**</span></span> <br/> |<span data-ttu-id="47b7b-261">Gibt den lokalisierten Anzeigenamen zurück.</span><span class="sxs-lookup"><span data-stu-id="47b7b-261">Returns the localized display name.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-262">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-262">**Properties**</span></span>


|<span data-ttu-id="47b7b-263">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-263">**Property**</span></span>|<span data-ttu-id="47b7b-264">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-264">**Return type**</span></span>|<span data-ttu-id="47b7b-265">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-265">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierType {get;}` <br/> |<span data-ttu-id="47b7b-266">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-266">**string**</span></span> <br/> |<span data-ttu-id="47b7b-267">Gibt den Typ des Bezeichners.</span><span class="sxs-lookup"><span data-stu-id="47b7b-267">Returns the type of identifier.</span></span>  <br/> |
| `Name {get;}` <br/> |<span data-ttu-id="47b7b-268">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-268">**string**</span></span> <br/> |<span data-ttu-id="47b7b-269">Ruft den Namen des Bezeichners ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-269">Gets the name of the identifier.</span></span>  <br/> |
   

## <a name="identifiercollection-method"></a><span data-ttu-id="47b7b-270">IdentifierCollection-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-270">IdentifierCollection method</span></span>
<span data-ttu-id="47b7b-271"><a name="bkmk_IdentifierCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-271"></span></span>


  
    
    

<span data-ttu-id="47b7b-272">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-272">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-273">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-273">**Managed**</span></span>|<span data-ttu-id="47b7b-274">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-274">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-275">**Microsoft.BusinessData.MetadataModel.Collections**</span><span class="sxs-lookup"><span data-stu-id="47b7b-275">**Microsoft.BusinessData.MetadataModel.Collections**</span></span> <br/> |<span data-ttu-id="47b7b-276">**SP.BusinessData.Collections**</span><span class="sxs-lookup"><span data-stu-id="47b7b-276">**SP.BusinessData.Collections**</span></span> <br/> |
   

<span data-ttu-id="47b7b-277">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-277">**Methods**</span></span>


|<span data-ttu-id="47b7b-278">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-278">**Method**</span></span>|<span data-ttu-id="47b7b-279">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-279">**Return type**</span></span>|<span data-ttu-id="47b7b-280">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-280">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-281">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-281">None.</span></span>  <br/> |<span data-ttu-id="47b7b-282">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-282">**void**</span></span> <br/> ||
   

<span data-ttu-id="47b7b-283">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-283">**Properties**</span></span>


|<span data-ttu-id="47b7b-284">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-284">**Property**</span></span>|<span data-ttu-id="47b7b-285">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-285">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-286">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-286">None.</span></span>  <br/> ||
   

## <a name="identity-method"></a><span data-ttu-id="47b7b-287">Identity-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-287">Identity method</span></span>
<span data-ttu-id="47b7b-288"><a name="bkmk_Identity"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-288"></span></span>


  
    
    

<span data-ttu-id="47b7b-289">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-289">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-290">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-290">**Managed**</span></span>|<span data-ttu-id="47b7b-291">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-291">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-292">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-292">**Microsoft.BusinessData.Runtime. IFilter**</span></span> <br/> |<span data-ttu-id="47b7b-293">**SP.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-293">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="47b7b-294">**Konstruktor**</span><span class="sxs-lookup"><span data-stu-id="47b7b-294">**Constructor**</span></span>


|<span data-ttu-id="47b7b-295">**Konstruktor**</span><span class="sxs-lookup"><span data-stu-id="47b7b-295">**Constructor**</span></span>|<span data-ttu-id="47b7b-296">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-296">**Description**</span></span>|
|:-----|:-----|
| `public Identity (Object[] identifierValues)` <br/> |<span data-ttu-id="47b7b-297">Erstellt eine neue Instanz der Klasse mithilfe von ein Array von ID-Werte.</span><span class="sxs-lookup"><span data-stu-id="47b7b-297">Constructs a new instance of the class by using an array of identifier values.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-298">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-298">**Methods**</span></span>


|<span data-ttu-id="47b7b-299">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-299">**Method**</span></span>|<span data-ttu-id="47b7b-300">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-300">**Return type**</span></span>|<span data-ttu-id="47b7b-301">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-301">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-302">**Serialize**</span><span class="sxs-lookup"><span data-stu-id="47b7b-302">**Serialize**</span></span> <br/> |<span data-ttu-id="47b7b-303">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-303">**string**</span></span> <br/> |<span data-ttu-id="47b7b-304">Ruft eine Zeichenfolgendarstellung der Identität ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-304">Gets a string representation of the identity.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-305">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-305">**Properties**</span></span>


|<span data-ttu-id="47b7b-306">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-306">**Property**</span></span>|<span data-ttu-id="47b7b-307">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-307">**Return type**</span></span>|<span data-ttu-id="47b7b-308">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-308">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierCount { get; }` <br/> |<span data-ttu-id="47b7b-309">**int**</span><span class="sxs-lookup"><span data-stu-id="47b7b-309">**int**</span></span> <br/> |<span data-ttu-id="47b7b-310">Gibt die Anzahl der Bezeichner zurück.</span><span class="sxs-lookup"><span data-stu-id="47b7b-310">Returns the number of identifiers.</span></span>  <br/> |
| `IsTemporary { get; }` <br/> |<span data-ttu-id="47b7b-311">**bool**</span><span class="sxs-lookup"><span data-stu-id="47b7b-311">**bool**</span></span> <br/> |<span data-ttu-id="47b7b-312">Überprüft, ob die Identität temporär ist.</span><span class="sxs-lookup"><span data-stu-id="47b7b-312">Checks whether the identity is temporary.</span></span>  <br/> |
| `this[int identifierIndex] { get; }` <br/> |<span data-ttu-id="47b7b-313">**Objekt**</span><span class="sxs-lookup"><span data-stu-id="47b7b-313">**Object**</span></span> <br/> |<span data-ttu-id="47b7b-p103">Ruft das Element am angegebenen Index ab. CSOM unterstützt Int-basierte Indizierung nicht. Basis-Accessor für den gleichen implementiert.</span><span class="sxs-lookup"><span data-stu-id="47b7b-p103">Retrieves the element at the given index. CSOM does not support int-based indexing. String-based accessor implemented for the same.</span></span>  <br/> |
| `TemporaryId { get; }` <br/> |<span data-ttu-id="47b7b-317">**Guid**</span><span class="sxs-lookup"><span data-stu-id="47b7b-317">**Guid**</span></span> <br/> |<span data-ttu-id="47b7b-318">Gibt den temporären Teil der Identität zurück.</span><span class="sxs-lookup"><span data-stu-id="47b7b-318">Returns the temporary part of the identity.</span></span>  <br/> |
   

## <a name="fieldvaluedictionary-method"></a><span data-ttu-id="47b7b-319">Abgerufenen "FieldValueDictionary"-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-319">FieldValueDictionary method</span></span>
<span data-ttu-id="47b7b-320"><a name="bkmk_FieldValueDictionary"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-320"></span></span>


  
    
    

<span data-ttu-id="47b7b-321">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-321">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-322">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-322">**Managed**</span></span>|<span data-ttu-id="47b7b-323">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-323">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-324">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-324">**Microsoft.BusinessData.Runtime. IFilter**</span></span> <br/> |<span data-ttu-id="47b7b-325">**SP.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-325">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="47b7b-326">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-326">**Methods**</span></span>


|<span data-ttu-id="47b7b-327">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-327">**Method**</span></span>|<span data-ttu-id="47b7b-328">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-328">**Return type**</span></span>|<span data-ttu-id="47b7b-329">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-329">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-330">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="47b7b-330">**FromXml**</span></span> <br/> |<span data-ttu-id="47b7b-331">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-331">**void**</span></span> <br/> |<span data-ttu-id="47b7b-332">Die Werte festgelegt aus der angegebenen XML in diesem Wörterbuch.</span><span class="sxs-lookup"><span data-stu-id="47b7b-332">Sets the values in this dictionary from specified XML.</span></span>  <br/> |
|<span data-ttu-id="47b7b-333">**GetCollectionSize**</span><span class="sxs-lookup"><span data-stu-id="47b7b-333">**GetCollectionSize**</span></span> <br/> |<span data-ttu-id="47b7b-334">int</span><span class="sxs-lookup"><span data-stu-id="47b7b-334">int</span></span>  <br/> |<span data-ttu-id="47b7b-335">Gibt die Größe der Auflistung, der auf die punktierte Schreibweise verweist.</span><span class="sxs-lookup"><span data-stu-id="47b7b-335">Returns the size of the collection that the dot notation refers to.</span></span>  <br/> |
|<span data-ttu-id="47b7b-336">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="47b7b-336">**ToXml**</span></span> <br/> |<span data-ttu-id="47b7b-337">string</span><span class="sxs-lookup"><span data-stu-id="47b7b-337">string</span></span>  <br/> |<span data-ttu-id="47b7b-338">Ruft die Werte im XML-Format ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-338">Retrieves the values in XML format.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-339">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-339">**Properties**</span></span>


|<span data-ttu-id="47b7b-340">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-340">**Property**</span></span>|<span data-ttu-id="47b7b-341">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-341">**Description**</span></span>|
|:-----|:-----|
| `Object this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="47b7b-342">Dient zum Abrufen oder Festlegen des Werts des Felds, die durch die punktierte Schreibweise bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="47b7b-342">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
   

## <a name="entityfieldcollection-method"></a><span data-ttu-id="47b7b-343">EntityFieldCollection-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-343">EntityFieldCollection method</span></span>
<span data-ttu-id="47b7b-344"><a name="bkmk_EntityFieldCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-344"></span></span>


  
    
    

<span data-ttu-id="47b7b-345">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-345">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-346">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-346">**Managed**</span></span>|<span data-ttu-id="47b7b-347">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-347">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-348">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-348">**Microsoft.BusinessData.Runtime. IFilter**</span></span> <br/> |<span data-ttu-id="47b7b-349">**SP.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-349">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="47b7b-350">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-350">**Methods**</span></span>


|<span data-ttu-id="47b7b-351">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-351">**Method**</span></span>|<span data-ttu-id="47b7b-352">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-352">**Return type**</span></span>|<span data-ttu-id="47b7b-353">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-353">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-354">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-354">None.</span></span>  <br/> |<span data-ttu-id="47b7b-355">**void**</span><span class="sxs-lookup"><span data-stu-id="47b7b-355">**void**</span></span> <br/> ||
   

<span data-ttu-id="47b7b-356">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-356">**Properties**</span></span>


|<span data-ttu-id="47b7b-357">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-357">**Property**</span></span>|<span data-ttu-id="47b7b-358">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-358">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-359">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-359">None.</span></span>  <br/> ||
   

## <a name="entityfield-method"></a><span data-ttu-id="47b7b-360">EntityField-Methode</span><span class="sxs-lookup"><span data-stu-id="47b7b-360">EntityField method</span></span>
<span data-ttu-id="47b7b-361"><a name="bkmk_Entityfield"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-361"></span></span>


  
    
    

<span data-ttu-id="47b7b-362">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-362">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-363">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-363">**Managed**</span></span>|<span data-ttu-id="47b7b-364">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-364">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-365">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-365">**Microsoft.BusinessData.Runtime. IFilter**</span></span> <br/> |<span data-ttu-id="47b7b-366">**SP.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="47b7b-366">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="47b7b-367">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-367">**Methods**</span></span>


|<span data-ttu-id="47b7b-368">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-368">**Method**</span></span>|<span data-ttu-id="47b7b-369">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-369">**Return type**</span></span>|<span data-ttu-id="47b7b-370">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-370">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-371">Keine.</span><span class="sxs-lookup"><span data-stu-id="47b7b-371">None.</span></span>  <br/> |<span data-ttu-id="47b7b-372">void</span><span class="sxs-lookup"><span data-stu-id="47b7b-372">void</span></span>  <br/> ||
   

<span data-ttu-id="47b7b-373">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-373">**Properties**</span></span>


|<span data-ttu-id="47b7b-374">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-374">**Property**</span></span>|<span data-ttu-id="47b7b-375">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-375">**Return type**</span></span>|<span data-ttu-id="47b7b-376">**Schreibgeschützt**</span><span class="sxs-lookup"><span data-stu-id="47b7b-376">**Read Only**</span></span>|<span data-ttu-id="47b7b-377">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-377">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-378">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-378">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-379">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="47b7b-379">**Boolean**</span></span> <br/> |<span data-ttu-id="47b7b-380">Ja</span><span class="sxs-lookup"><span data-stu-id="47b7b-380">Yes</span></span>  <br/> |<span data-ttu-id="47b7b-381">Bestimmt, ob das Feld einen lokalisierten Anzeigenamen enthält.</span><span class="sxs-lookup"><span data-stu-id="47b7b-381">Determines whether the field contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="47b7b-382">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-382">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-383">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-383">**string**</span></span> <br/> |<span data-ttu-id="47b7b-384">Ja</span><span class="sxs-lookup"><span data-stu-id="47b7b-384">Yes</span></span>  <br/> |<span data-ttu-id="47b7b-385">Der standardmäßige Anzeigename des Felds abgerufen.</span><span class="sxs-lookup"><span data-stu-id="47b7b-385">Retrieves the default display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="47b7b-386">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-386">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="47b7b-387">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-387">**string**</span></span> <br/> ||<span data-ttu-id="47b7b-388">Ruft den lokalisierten Anzeigenamen des Felds ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-388">Retrieves the localized display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="47b7b-389">**Name**</span><span class="sxs-lookup"><span data-stu-id="47b7b-389">**Name**</span></span> <br/> |<span data-ttu-id="47b7b-390">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-390">**string**</span></span> <br/> |<span data-ttu-id="47b7b-391">Ja</span><span class="sxs-lookup"><span data-stu-id="47b7b-391">Yes</span></span>  <br/> |<span data-ttu-id="47b7b-392">Ruft den Namen des Felds ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-392">Retrieves the name of the Field.</span></span>  <br/> |
   

## <a name="typedescriptor-class"></a><span data-ttu-id="47b7b-393">TypeDescriptor-Klasse</span><span class="sxs-lookup"><span data-stu-id="47b7b-393">TypeDescriptor class</span></span>
<span data-ttu-id="47b7b-394"><a name="bkmk_TypeDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-394"></span></span>


  
    
    

<span data-ttu-id="47b7b-395">**Namespaces**</span><span class="sxs-lookup"><span data-stu-id="47b7b-395">**Namespaces**</span></span>


|<span data-ttu-id="47b7b-396">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="47b7b-396">**Managed**</span></span>|<span data-ttu-id="47b7b-397">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="47b7b-397">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-398">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="47b7b-398">**Microsoft.BusinessData.MetadataModel. IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-399">**SP.BusinessData**</span><span class="sxs-lookup"><span data-stu-id="47b7b-399">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="47b7b-400">**Methoden**</span><span class="sxs-lookup"><span data-stu-id="47b7b-400">**Methods**</span></span>


|<span data-ttu-id="47b7b-401">**Methode**</span><span class="sxs-lookup"><span data-stu-id="47b7b-401">**Method**</span></span>|<span data-ttu-id="47b7b-402">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-402">**Return type**</span></span>|<span data-ttu-id="47b7b-403">**Schreibgeschützt**</span><span class="sxs-lookup"><span data-stu-id="47b7b-403">**Read Only**</span></span>|<span data-ttu-id="47b7b-404">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-404">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-405">**ContainsLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-405">**ContainsLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="47b7b-406">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="47b7b-406">**Boolean**</span></span> <br/> |<span data-ttu-id="47b7b-407">Ja</span><span class="sxs-lookup"><span data-stu-id="47b7b-407">Yes</span></span>  <br/> |<span data-ttu-id="47b7b-408">Bestimmt, ob der Typdeskriptor einen lokalisierten Anzeigenamen enthält.</span><span class="sxs-lookup"><span data-stu-id="47b7b-408">Determines whether the type descriptor contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="47b7b-409">**GetLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-409">**GetLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="47b7b-410">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-410">**string**</span></span> <br/> |<span data-ttu-id="47b7b-411">Ja</span><span class="sxs-lookup"><span data-stu-id="47b7b-411">Yes</span></span>  <br/> |<span data-ttu-id="47b7b-412">Gibt den lokalisierten Anzeigenamen zurück.</span><span class="sxs-lookup"><span data-stu-id="47b7b-412">Returns the localized display name.</span></span>  <br/> |
|<span data-ttu-id="47b7b-413">**GetDefaultDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="47b7b-413">**GetDefaultDisplayName()**</span></span> <br/> |<span data-ttu-id="47b7b-414">**Zeichenfolge**</span><span class="sxs-lookup"><span data-stu-id="47b7b-414">**string**</span></span> <br/> ||<span data-ttu-id="47b7b-415">Der standardmäßige Anzeigename zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="47b7b-415">Returns the default display name.</span></span>  <br/> |
   

<span data-ttu-id="47b7b-416">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="47b7b-416">**Properties**</span></span>


|<span data-ttu-id="47b7b-417">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="47b7b-417">**Property**</span></span>|<span data-ttu-id="47b7b-418">**Rückgabetyp**</span><span class="sxs-lookup"><span data-stu-id="47b7b-418">**Return type**</span></span>|<span data-ttu-id="47b7b-419">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-419">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="47b7b-420">**Name**</span><span class="sxs-lookup"><span data-stu-id="47b7b-420">**Name**</span></span> <br/> |<span data-ttu-id="47b7b-421">string</span><span class="sxs-lookup"><span data-stu-id="47b7b-421">string</span></span>  <br/> |<span data-ttu-id="47b7b-422">Ruft den Namen des Felds ab.</span><span class="sxs-lookup"><span data-stu-id="47b7b-422">Retrieves the name of the Field.</span></span>  <br/> |
|<span data-ttu-id="47b7b-423">**TypeName**</span><span class="sxs-lookup"><span data-stu-id="47b7b-423">**typeName**</span></span> <br/> |<span data-ttu-id="47b7b-424">string</span><span class="sxs-lookup"><span data-stu-id="47b7b-424">string</span></span>  <br/> |<span data-ttu-id="47b7b-425">Ruft den Namen des Datentyps durch diesen Typdeskriptor dargestellt.</span><span class="sxs-lookup"><span data-stu-id="47b7b-425">Retrieves the name of the data type represented by this type descriptor.</span></span>  <br/> |
|<span data-ttu-id="47b7b-426">**IsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="47b7b-426">**IsReadOnly**</span></span> <br/> |<span data-ttu-id="47b7b-427">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="47b7b-427">Boolean</span></span>  <br/> |<span data-ttu-id="47b7b-428">Bestimmt, ob dieser Typdeskriptor eine nur-Lese-Datenstruktur darstellt.</span><span class="sxs-lookup"><span data-stu-id="47b7b-428">Determines whether this type descriptor represents a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="47b7b-429">**ContainsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="47b7b-429">**ContainsReadOnly**</span></span> <br/> |<span data-ttu-id="47b7b-430">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="47b7b-430">Boolean</span></span>  <br/> |<span data-ttu-id="47b7b-431">Bestimmt, ob dieser Typdeskriptor oder eines der untergeordneten eine nur-Lese-Datenstruktur darstellen.</span><span class="sxs-lookup"><span data-stu-id="47b7b-431">Determines whether this type descriptor or one of its children represent a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="47b7b-432">**IsCollection**</span><span class="sxs-lookup"><span data-stu-id="47b7b-432">**IsCollection**</span></span> <br/> |<span data-ttu-id="47b7b-433">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="47b7b-433">Boolean</span></span>  <br/> |<span data-ttu-id="47b7b-434">Bestimmt, ob der beschriebene Typ eine Datenstruktur Auflistung darstellt.</span><span class="sxs-lookup"><span data-stu-id="47b7b-434">Determines whether the described type represents a collection data structure.</span></span>  <br/> |
   

## <a name="interfaces"></a><span data-ttu-id="47b7b-435">Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="47b7b-435">Interfaces</span></span>
<span data-ttu-id="47b7b-436"><a name="bkmk_Interfaces"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-436"></span></span>

<span data-ttu-id="47b7b-437">Der Namespace ist **Microsoft.BusinessData.MetadataModel**.</span><span class="sxs-lookup"><span data-stu-id="47b7b-437">The namespace is **Microsoft.BusinessData.MetadataModel**.</span></span>
  
    
    


|<span data-ttu-id="47b7b-438">**Schnittstelle**</span><span class="sxs-lookup"><span data-stu-id="47b7b-438">**Interface**</span></span>|<span data-ttu-id="47b7b-439">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47b7b-439">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="47b7b-440">**IMetadataCatalog**</span><span class="sxs-lookup"><span data-stu-id="47b7b-440">**IMetadataCatalog**</span></span> <br/> |<span data-ttu-id="47b7b-p104">Der Einstiegspunkt in das BDC-Objektmodell. Verwenden Sie die **DatabaseBasedMetadataCatalog** auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="47b7b-p104">The entry point into the BDC object model. Use the **DatabaseBasedMetadataCatalog** on the server. </span></span><br/> |
|<span data-ttu-id="47b7b-443">**ILobSystem**</span><span class="sxs-lookup"><span data-stu-id="47b7b-443">**ILobSystem**</span></span> <br/> |<span data-ttu-id="47b7b-444">Enthält die Details zu einem externen System.</span><span class="sxs-lookup"><span data-stu-id="47b7b-444">Contains the details about an external system.</span></span>  <br/> |
|<span data-ttu-id="47b7b-445">**IEntity**</span><span class="sxs-lookup"><span data-stu-id="47b7b-445">**IEntity**</span></span> <br/> |<span data-ttu-id="47b7b-446">Ein externer Inhaltstyp im BDC-Metadatenspeicher.</span><span class="sxs-lookup"><span data-stu-id="47b7b-446">An external content type in the BDC Metadata Store.</span></span>  <br/> |
|<span data-ttu-id="47b7b-447">**IMethod**</span><span class="sxs-lookup"><span data-stu-id="47b7b-447">**IMethod**</span></span> <br/> |<span data-ttu-id="47b7b-448">Ein Vorgang, der für den externen Inhaltstyp ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="47b7b-448">An operation that can be performed on the external content type.</span></span>  <br/> |
|<span data-ttu-id="47b7b-449">**IEntityInstance**</span><span class="sxs-lookup"><span data-stu-id="47b7b-449">**IEntityInstance**</span></span> <br/> |<span data-ttu-id="47b7b-450">Eine Entitätsinstanz (auch bekannt als externes Element) ist ein einzelnes Element in einem externen System im BDC zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="47b7b-450">An entity instance (also known as external item) is a single item returned from an external system in BDC.</span></span>  <br/> <span data-ttu-id="47b7b-p105"> Die Schnittstelle **IEntityInstance** abstrahiert die zugrunde liegenden Datenquellen und isoliert von anwendungsspezifischen Codierung Paradigmen erfahren, dass die Clients; Sie können alle Geschäftsdaten in eine einzige, vereinfachte Möglichkeit zugreifen. Mithilfe der **IEntityInstance** -Schnittstelle können Sie mit einer Reihe von Daten aus einer Datenbank in genauso wie Arbeiten mit einer komplexen .NET Framework-Struktur, die von einem Webdienst zurückgegeben arbeiten. </span><span class="sxs-lookup"><span data-stu-id="47b7b-p105">The **IEntityInstance** interface abstracts the underlying data sources and insulates the clients from having to learn application-specific coding paradigms; it enables them to access all business data in a single, simplified way. By using the **IEntityInstance** interface, you can work with a row of data from a database in just the same way as working with a complex .NET Framework structure returned by a web service. </span></span><br/> <span data-ttu-id="47b7b-p106"> Eine Entitätsinstanz im BDC-hat spezielle Semantik angefügt. Er hat die Möglichkeit, wissen, welches Feld oder Felder in der Zeile den Bezeichner für die Entitätsinstanz darstellen, und es ermöglicht Ihnen das Aufrufen von Methoden, wie **GetAssociated**, **GetIdentifierValues**und **Execute**, für diese Entitätsinstanz. </span><span class="sxs-lookup"><span data-stu-id="47b7b-p106">An entity instance in BDC has special semantics attached to it. For example, it has the ability to know which field or fields in the row represent the identifier for the entity instance, and it enables you to call methods, such as **GetAssociated**, **GetIdentifierValues**, and **Execute**, on that entity instance.  </span></span><br/> |
|<span data-ttu-id="47b7b-455">**IEntityInstanceEnumerator**</span><span class="sxs-lookup"><span data-stu-id="47b7b-455">**IEntityInstanceEnumerator**</span></span> <br/> |<span data-ttu-id="47b7b-p107">Enumeratoren zum Lesen der Daten in der externen Items-Auflistung verwendet werden, jedoch nicht zum Ändern der zugrunde liegenden Auflistung verwendet werden. **IEntityInstanceEnumerator** unterstützt streaming und ist daher sehr nützlich, wenn die Back-End-Anwendung große Datenmengen zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="47b7b-p107">Enumerators can be used to read the data in the external items collection, but they cannot be used to modify the underlying collection. **IEntityInstanceEnumerator** supports streaming and is therefore very useful when the back-end application returns large amounts of data. </span></span><br/> |
   

## <a name="client-object-model-faq"></a><span data-ttu-id="47b7b-458">Client Object Model - häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="47b7b-458">Client Object model FAQ</span></span>
<span data-ttu-id="47b7b-459"><a name="bkmk_ClientObjectModelFAQ"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-459"></span></span>


- <span data-ttu-id="47b7b-460">**Muss das <Method>-Tag beim Abfragen einer externen Liste in einer CAML-Abfrage enthalten sein?**</span><span class="sxs-lookup"><span data-stu-id="47b7b-460">**Does the <Method> tag need to be included in a CAML query when querying an external list**</span></span>
    
    <span data-ttu-id="47b7b-461">Nein.</span><span class="sxs-lookup"><span data-stu-id="47b7b-461">No.</span></span> 
    
  
- <span data-ttu-id="47b7b-462">**Müssen alle Felder in der externen Liste in der CAML-Abfrage angegeben werden?**</span><span class="sxs-lookup"><span data-stu-id="47b7b-462">**Do all fields in the external list need to be specified in the CAML query?**</span></span>
    
    <span data-ttu-id="47b7b-463">Über den ViewXML-Tag im BDC-Modell der Entwickler kann angeben, dass nur die Felder, die erforderlich sind, und die CSOM-APIs für Listen gibt nur die Felder zurück.</span><span class="sxs-lookup"><span data-stu-id="47b7b-463">Using the ViewXML tag in the BDC model, the developer can specify only those fields that are required and the CSOM APIs for Lists will return only those fields.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="47b7b-464">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="47b7b-464">Additional resources</span></span>
<span data-ttu-id="47b7b-465"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="47b7b-465"></span></span>


-  [<span data-ttu-id="47b7b-466">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-466">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="47b7b-467">.NET-Client-API-Referenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-467">.NET client API reference for SharePoint Online</span></span>](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="47b7b-468">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-468">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47b7b-469">Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-469">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47b7b-470">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-470">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47b7b-471">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b7b-471">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
