---
title: "Änderungen im BDC-Modellschema für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 882ea867-9acb-4313-99c9-865a523b72fd
ms.openlocfilehash: c95208da93af349ae768df7069c425eb088b8b30
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="changes-in-the-bdc-model-schema-for-sharepoint"></a><span data-ttu-id="ffa2a-102">Änderungen im BDC-Modellschema für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-102">Changes in the BDC model schema for SharePoint</span></span>
<span data-ttu-id="ffa2a-p101">Hier erfahren Sie, was in SharePoint für das BDC-Modellschema geändert hat. Die Anzahl der Änderungen im Schema (BDCMetadata.xsd) für das Erstellen von BDC-Modelle auf SharePoint ist relativ gering. Aber diese Änderungen erhebliche Auswirkungen auf das Feature Angebote von Business Connectivity Services (BCS) festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-p101">Learn what has changed in SharePoint for the BDC model schema. The number of changes in the schema (BDCMetadata.xsd) for creating BDC models in SharePoint is relatively small. But these changes have significant impact on the feature set offerings of Business Connectivity Services (BCS).</span></span>
  
    
    

<span data-ttu-id="ffa2a-106">Weitere Informationen zum BDCMetadata-Schema finden Sie unter  [BDC-Modell-Schemareferenz für SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ffa2a-106">For more information about the BDCMetadata schema, see  [BDC model schema reference for SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span></span>
## <a name="changes-to-complex-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="ffa2a-107">Änderungen an den komplexen Typelemente in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="ffa2a-107">Changes to complex type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="ffa2a-108"><a name="bkmk_ChangesToElements"> </a></span><span class="sxs-lookup"><span data-stu-id="ffa2a-108"><a name="bkmk_ChangesToElements"> </a></span></span>

<span data-ttu-id="ffa2a-109">In der folgenden Tabelle zeigt, welche Änderungen an den Elemente der obersten Ebene im BDCMetadata-Schema vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-109">The following table shows what changes have been made to the top-level elements in the BDCMetadata schema.</span></span>
  
    
    

<span data-ttu-id="ffa2a-110">**In Tabelle 1. Neue komplexe Typen**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-110">**Table 1. New complex types**</span></span>


|<span data-ttu-id="ffa2a-111">**Element**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-111">**Element**</span></span>|<span data-ttu-id="ffa2a-112">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-112">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ffa2a-113">IndividuallySecurableMetadataObject</span><span class="sxs-lookup"><span data-stu-id="ffa2a-113">IndividuallySecurableMetadataObject</span></span>  <br/> |<span data-ttu-id="ffa2a-114">Verwendet, um festzulegen, dass die angegebenen **MetadataObject** explizit gesichert werden kann und nicht über seine Zuordnung zu seinem übergeordneten Element.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-114">Used to designate that the specified **MetadataObject** is able to be secured explicitly and not by association to its parent.</span></span> <br/> |
|<span data-ttu-id="ffa2a-115">MetadataObject</span><span class="sxs-lookup"><span data-stu-id="ffa2a-115">MetadataObject</span></span>  <br/> |<span data-ttu-id="ffa2a-116">Zum Speichern der zusätzlichen Metadaten für die Verbindung mit der externen Datenquelle verwendet.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-116">Used to store additional metadata about the connection to the external data source.</span></span>  <br/> |
   

## <a name="changes-to-simple-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="ffa2a-117">Änderungen an den einfachen Typ der Elemente in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="ffa2a-117">Changes to simple type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="ffa2a-118"><a name="bkmk_ChangesToSimpleTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="ffa2a-118"><a name="bkmk_ChangesToSimpleTypes"> </a></span></span>

<span data-ttu-id="ffa2a-119">Die folgende Tabelle enthält die Änderungen, die an die Attribute der einzelnen Elemente vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-119">The following table lists the changes that have been made to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="ffa2a-120">**In Tabelle 2. Änderungen an einfache Typen**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-120">**Table 2. Changes to simple types**</span></span>


|<span data-ttu-id="ffa2a-121">**Element**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-121">**Element**</span></span>|<span data-ttu-id="ffa2a-122">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-122">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ffa2a-123">Keine Änderungen</span><span class="sxs-lookup"><span data-stu-id="ffa2a-123">No changes</span></span>  <br/> ||
   

## <a name="changes-to-attributes-in-bdcmetadataxsd"></a><span data-ttu-id="ffa2a-124">Ändern von Attributen in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="ffa2a-124">Changes to attributes in BDCMetadata.xsd</span></span>
<span data-ttu-id="ffa2a-125"><a name="bkmk_ChangesToAttributes"> </a></span><span class="sxs-lookup"><span data-stu-id="ffa2a-125"><a name="bkmk_ChangesToAttributes"> </a></span></span>

<span data-ttu-id="ffa2a-126">Die folgende Tabelle enthält die Änderungen an der Attribute der einzelnen Elemente.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-126">The following table lists the changes to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="ffa2a-127">**Tabelle 3. Ändern von Attributen**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-127">**Table 3. Changes to attributes**</span></span>


|<span data-ttu-id="ffa2a-128">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-128">**Attribute**</span></span>|<span data-ttu-id="ffa2a-129">**Übergeordneter Schlüssel**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-129">**Parent**</span></span>|<span data-ttu-id="ffa2a-130">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ffa2a-130">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="ffa2a-131">Keine Änderungen</span><span class="sxs-lookup"><span data-stu-id="ffa2a-131">No changes</span></span>  <br/> |||
   

## <a name="see-also"></a><span data-ttu-id="ffa2a-132">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ffa2a-132">See also</span></span>
<span data-ttu-id="ffa2a-133"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="ffa2a-133"><a name="bkmk_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="ffa2a-134">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-134">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ffa2a-135">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-135">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ffa2a-136">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-136">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ffa2a-137">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-137">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ffa2a-138">BDC-Modell-Schemareferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffa2a-138">BDC model schema reference for SharePoint</span></span>](bdc-model-schema-reference-for-sharepoint.md)
    
  

