---
title: "Änderungen im BDC-Modellschema für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 882ea867-9acb-4313-99c9-865a523b72fd
ms.openlocfilehash: 95048677b9ef34f394c58d4a13c3edf5ab538754
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="changes-in-the-bdc-model-schema-for-sharepoint"></a><span data-ttu-id="f29a3-102">Änderungen im BDC-Modellschema für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-102">Changes in the BDC model schema for SharePoint</span></span>
<span data-ttu-id="f29a3-p101">Hier erfahren Sie, was in SharePoint für das BDC-Modellschema geändert hat. Die Anzahl der Änderungen im Schema (BDCMetadata.xsd) für das Erstellen von BDC-Modelle auf SharePoint ist relativ gering. Aber diese Änderungen erhebliche Auswirkungen auf das Feature Angebote von Business Connectivity Services (BCS) festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="f29a3-p101">Learn what has changed in SharePoint for the BDC model schema. The number of changes in the schema (BDCMetadata.xsd) for creating BDC models in SharePoint is relatively small. But these changes have significant impact on the feature set offerings of Business Connectivity Services (BCS).</span></span>
  
    
    

<span data-ttu-id="f29a3-106">Weitere Informationen zum BDCMetadata-Schema finden Sie unter  [BDC-Modell-Schemareferenz für SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f29a3-106">For more information about the BDCMetadata schema, see  [BDC model schema reference for SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span></span>
## <a name="changes-to-complex-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="f29a3-107">Änderungen an den komplexen Typelemente in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="f29a3-107">Changes to complex type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="f29a3-108"><a name="bkmk_ChangesToElements"> </a></span><span class="sxs-lookup"><span data-stu-id="f29a3-108"></span></span>

<span data-ttu-id="f29a3-109">In der folgenden Tabelle zeigt, welche Änderungen an den Elemente der obersten Ebene im BDCMetadata-Schema vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="f29a3-109">The following table shows what changes have been made to the top-level elements in the BDCMetadata schema.</span></span>
  
    
    

<span data-ttu-id="f29a3-110">**In Tabelle 1. Neue komplexe Typen**</span><span class="sxs-lookup"><span data-stu-id="f29a3-110">**Table 1. New complex types**</span></span>


|<span data-ttu-id="f29a3-111">**Element**</span><span class="sxs-lookup"><span data-stu-id="f29a3-111">**Element**</span></span>|<span data-ttu-id="f29a3-112">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f29a3-112">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f29a3-113">IndividuallySecurableMetadataObject</span><span class="sxs-lookup"><span data-stu-id="f29a3-113">IndividuallySecurableMetadataObject</span></span>  <br/> |<span data-ttu-id="f29a3-114">Verwendet, um festzulegen, dass die angegebenen **MetadataObject** explizit gesichert werden kann und nicht über seine Zuordnung zu seinem übergeordneten Element.</span><span class="sxs-lookup"><span data-stu-id="f29a3-114">Used to designate that the specified **MetadataObject** is able to be secured explicitly and not by association to its parent.</span></span> <br/> |
|<span data-ttu-id="f29a3-115">MetadataObject</span><span class="sxs-lookup"><span data-stu-id="f29a3-115">MetadataObject element</span></span>  <br/> |<span data-ttu-id="f29a3-116">Zum Speichern der zusätzlichen Metadaten für die Verbindung mit der externen Datenquelle verwendet.</span><span class="sxs-lookup"><span data-stu-id="f29a3-116">Used to store additional metadata about the connection to the external data source.</span></span>  <br/> |
   

## <a name="changes-to-simple-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="f29a3-117">Änderungen an den einfachen Typ der Elemente in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="f29a3-117">Changes to simple type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="f29a3-118"><a name="bkmk_ChangesToSimpleTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="f29a3-118"></span></span>

<span data-ttu-id="f29a3-119">Die folgende Tabelle enthält die Änderungen, die an die Attribute der einzelnen Elemente vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="f29a3-119">The following table lists the changes that have been made to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="f29a3-120">**In Tabelle 2. Änderungen an einfache Typen**</span><span class="sxs-lookup"><span data-stu-id="f29a3-120">**Table 2. Changes to simple types**</span></span>


|<span data-ttu-id="f29a3-121">**Element**</span><span class="sxs-lookup"><span data-stu-id="f29a3-121">**Element**</span></span>|<span data-ttu-id="f29a3-122">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f29a3-122">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f29a3-123">Keine Änderungen</span><span class="sxs-lookup"><span data-stu-id="f29a3-123">No changes</span></span>  <br/> ||
   

## <a name="changes-to-attributes-in-bdcmetadataxsd"></a><span data-ttu-id="f29a3-124">Ändern von Attributen in BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="f29a3-124">Changes to attributes in BDCMetadata.xsd</span></span>
<span data-ttu-id="f29a3-125"><a name="bkmk_ChangesToAttributes"> </a></span><span class="sxs-lookup"><span data-stu-id="f29a3-125"></span></span>

<span data-ttu-id="f29a3-126">Die folgende Tabelle enthält die Änderungen an der Attribute der einzelnen Elemente.</span><span class="sxs-lookup"><span data-stu-id="f29a3-126">The following table lists the changes to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="f29a3-127">**Tabelle 3. Ändern von Attributen**</span><span class="sxs-lookup"><span data-stu-id="f29a3-127">**Table 3. Changes to attributes**</span></span>


|<span data-ttu-id="f29a3-128">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="f29a3-128">**Attribute**</span></span>|<span data-ttu-id="f29a3-129">**Übergeordneter Schlüssel**</span><span class="sxs-lookup"><span data-stu-id="f29a3-129">**Parent**</span></span>|<span data-ttu-id="f29a3-130">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f29a3-130">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f29a3-131">Keine Änderungen</span><span class="sxs-lookup"><span data-stu-id="f29a3-131">No changes</span></span>  <br/> |||
   

## <a name="additional-resources"></a><span data-ttu-id="f29a3-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f29a3-132">Additional resources</span></span>
<span data-ttu-id="f29a3-133"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="f29a3-133"></span></span>


-  [<span data-ttu-id="f29a3-134">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-134">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f29a3-135">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-135">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f29a3-136">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-136">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f29a3-137">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-137">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="f29a3-138">BDC-Modell-Schemareferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f29a3-138">BDC model schema reference for SharePoint</span></span>](bdc-model-schema-reference-for-sharepoint.md)
    
  

