---
title: "BDC-Modell-Schemareferenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 979a5ffc-f033-4e72-b2d1-11d8cb1b294a
ms.openlocfilehash: 712bc6e2413be359159f6bc7389ac0d05c3ded5d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="bdc-model-schema-reference-for-sharepoint"></a><span data-ttu-id="dc651-102">BDC-Modell-Schemareferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-102">BDC model schema reference for SharePoint</span></span>
<span data-ttu-id="dc651-p101">Enthält die Referenzdokumentation für das BDC-Modell-Schema (BDCMetadata.xsd), die Sie zum Erstellen von externer Inhaltstypen in SharePoint verwenden können. [BDCMetadata.xsd](http://schemas.microsoft.com/windows/2007/BusinessDataCatalog)</span><span class="sxs-lookup"><span data-stu-id="dc651-p101">Contains reference documentation for the BDC model schema (BDCMetadata.xsd), which you can use to create external content types in SharePoint. [BDCMetadata.xsd](http://schemas.microsoft.com/windows/2007/BusinessDataCatalog)</span></span>
  
    
    


## <a name="accesscontrolentry-element"></a><span data-ttu-id="dc651-105">AccessControlEntry (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-105">AccessControlEntry element</span></span>
<span data-ttu-id="dc651-106"><a name="bkmk_AccessControlEntry"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-106"></span></span>

<span data-ttu-id="dc651-107">Enthält einen Zugriffssteuerungseintrag (ACE), der Zugriffsrechte für das übergeordnete Element angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-107">Contains an access control entry (ACE) that specifies access rights for the parent element.</span></span>
  
    
    
<span data-ttu-id="dc651-108">Weitere Informationen zu Business Connectivity Services und zur Sicherheit finden Sie unter  [Business Connectivity Services-Sicherheit (Übersicht)](http://technet.microsoft.com/en-us/library/ee661734%28office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc651-108">See  [Business Connectivity Services security overview](http://technet.microsoft.com/en-us/library/ee661734%28office.14%29.aspx) to learn more about the Business Connectivity Services and security.</span></span>
  
    
    
 <span data-ttu-id="dc651-109">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-109">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-110">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-110">**Schema:** BDCMetadata</span></span>
  
    
    



```XML

<AccessControlEntry Principal = "String"> </AccessControlEntry>
```

<span data-ttu-id="dc651-111">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-111">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-112">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-112">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-113">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-113">**Attribute**</span></span>|<span data-ttu-id="dc651-114">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-114">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-115">Direktor</span><span class="sxs-lookup"><span data-stu-id="dc651-115">Principal</span></span>  <br/> |<span data-ttu-id="dc651-116">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-116">Required.</span></span>  <br/> <span data-ttu-id="dc651-117">Der Name des Sicherheitsprinzipals, der diesen ACE aufweist.</span><span class="sxs-lookup"><span data-stu-id="dc651-117">The name of the security principal that has this ACE.</span></span>  <br/> <span data-ttu-id="dc651-118">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-118">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="dc651-119">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-119">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-120">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-120">**Element**</span></span>|<span data-ttu-id="dc651-121">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-121">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-122">Right-Element in AccessControlEntry (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-122">Right Element in AccessControlEntry (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a2e4bd6c-2306-b657-7290-cc9c9b262911%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-123">Ein **Right**-Element, das die für den Sicherheitsprinzipal verfügbaren Berechtigungen angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-123">A **Right** element that specifies the permissions available to the security principal.</span></span> <br/> |
   
 <span data-ttu-id="dc651-124">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-124">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-125">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-125">**Element**</span></span>|<span data-ttu-id="dc651-126">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-127">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-127">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-128">Die Zugriffssteuerungsliste (Access Control List, ACL), die diesen ACE enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-128">The access control list (ACL) that contains this ACE.</span></span>  <br/> |
   

## <a name="accesscontrollist-element"></a><span data-ttu-id="dc651-129">AccessControlList (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-129">AccessControlList element</span></span>
<span data-ttu-id="dc651-130"><a name="bkmk_AccessControlList"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-130"></span></span>

<span data-ttu-id="dc651-131">Gibt eine Zugriffssteuerungsliste (Access Control List, ACL) für das übergeordnete Element an.</span><span class="sxs-lookup"><span data-stu-id="dc651-131">Specifies an access control list (ACL) for the parent element.</span></span>
  
    
    
 <span data-ttu-id="dc651-132">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-132">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-133">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-133">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AccessControlList></AccessControlList>
```

<span data-ttu-id="dc651-134">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-134">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-135">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-135">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-136">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-136">None</span></span>
  
    
    
 <span data-ttu-id="dc651-137">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-137">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-138">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-138">**Element**</span></span>|<span data-ttu-id="dc651-139">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-139">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-140">AccessControlEntry-Element in "AccessControlList" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-140">AccessControlEntry Element in AccessControlList (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-141">Ein Zugriffssteuerungseintrag (Access Control Entry, ACE).</span><span class="sxs-lookup"><span data-stu-id="dc651-141">An access control entry (ACE).</span></span>  <br/> |
   
 <span data-ttu-id="dc651-142">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-142">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-143">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-143">**Element**</span></span>|<span data-ttu-id="dc651-144">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-145">"Model"-Element ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-145">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-146">Ein Modell, externe Inhaltstypen in einer Geschäftsanwendung enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-146">A model that contains external content types in a business application.</span></span>  <br/> |
| [<span data-ttu-id="dc651-147">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-147">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-148">Die in dem Modell enthaltenen LobSystems.</span><span class="sxs-lookup"><span data-stu-id="dc651-148">The LobSystems contained inside the model.</span></span>  <br/> |
| [<span data-ttu-id="dc651-149">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-149">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-150">Ein externer Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="dc651-150">An external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-151">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-151">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-152">Eine Methode eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-152">A method of an external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-153">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-153">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-154">Eine Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-154">An association.</span></span>  <br/> |
| [<span data-ttu-id="dc651-155">MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-155">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-156">Eine Methodeninstanz eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-156">A method instance of an external content type.</span></span>  <br/> |
   

## <a name="action-element"></a><span data-ttu-id="dc651-157">Action-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-157">Action element</span></span>
<span data-ttu-id="dc651-158"><a name="bkmk_Action"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-158"></span></span>

<span data-ttu-id="dc651-159">Gibt eine von einem externen Inhaltstyp unterstützte Aktion an.</span><span class="sxs-lookup"><span data-stu-id="dc651-159">Specifies an action supported by an external content type.</span></span>
  
    
    
 <span data-ttu-id="dc651-160">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-160">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-161">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-161">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="dc651-162">Aktionen schließen die Lücke zwischen SharePoint und Office 2013 und einem externen System-Benutzeroberfläche durch eine Verknüpfung zurück zum externen System bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="dc651-162">Actions bridge the gap between SharePoint and Office 2013 and an external system's user interface by providing a link back to the external system.</span></span> 
  
    
    
<span data-ttu-id="dc651-p102">Standardmäßig enthält die Business Data Connectivity (BDC)-Dienst Aktionen wie **View Item**, **Edit Item**und **Delete Item**, nachdem Sie diese Vorgänge im Modell BDC modellieren. Zusätzlich zu diesen Standardaktionen können Sie Aktionen für andere Funktionen erstellen, den, die Sie Ihren externen Inhaltstyp zuordnen möchten. Sie können beispielsweise Aktionen verwenden, um einfache Aktionen auszuführen wie das Senden von e-Mail-Nachrichten an einen Kunden in den externen Inhaltstyp Customer oder einer Kunden-Homepage in einem Browser öffnen.</span><span class="sxs-lookup"><span data-stu-id="dc651-p102">By default, the Business Data Connectivity (BDC) service provides actions such as **View Item**, **Edit Item**, and **Delete Item** after you model these operations in the BDC model. In addition to these default actions, you can create actions for other functionality you want to attach to your external content type. For example, you can use actions to perform simple actions, such as sending email messages to a customer from the Customer external content type or opening a customer's home page in a browser.</span></span>
  
    
    
<span data-ttu-id="dc651-p103">Aktionen werden mit einem externen Inhaltstyp übertragen. Das bedeutet, dass eine Aktion, nachdem Sie sie für einen externen Inhaltstyp definiert haben, überall angezeigt wird, wo dieser externe Inhaltstyp angezeigt wird - ob in einer externen Liste, in einem Geschäftsdaten-Webpart oder in einer Spalte mit externen Daten.</span><span class="sxs-lookup"><span data-stu-id="dc651-p103">Actions travel with an external content type. That is, after you define an action for an external content type, the action appears everywhere you display that external content type—whether in an external list or Business Data Web Part or in an External Data column.</span></span> 
  
    
    



```XML
<Action Position = "Integer" IsOpenedInNewWindow = "Boolean" Url = "String" ImageUrl = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Action>
```

<span data-ttu-id="dc651-168">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-168">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-169">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-169">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-170">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-170">**Attribute**</span></span>|<span data-ttu-id="dc651-171">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-171">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-172">**Position**</span><span class="sxs-lookup"><span data-stu-id="dc651-172">**Position**</span></span> <br/> |<span data-ttu-id="dc651-173">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-173">Required.</span></span>  <br/> <span data-ttu-id="dc651-174">Die vorgeschlagene Position dieser Aktion unter den anderen Aktionen dieses externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-174">The suggested position of this action among the other actions of this external content type.</span></span>  <br/> <span data-ttu-id="dc651-175">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-175">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="dc651-176">**IsOpenedInNewWindow**</span><span class="sxs-lookup"><span data-stu-id="dc651-176">**IsOpenedInNewWindow**</span></span> <br/> |<span data-ttu-id="dc651-177">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-177">Optional.</span></span>  <br/> <span data-ttu-id="dc651-178">Gibt an, ob die Ergebnisse der Ausführung einer Aktion in einem neuen Fenster auf der Benutzeroberfläche angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-178">Specifies whether the results of executing an action are presented in a new user interface window.</span></span>  <br/> <span data-ttu-id="dc651-179">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-179">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-180">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-180">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-181">**Url**</span><span class="sxs-lookup"><span data-stu-id="dc651-181">**Url**</span></span> <br/> |<span data-ttu-id="dc651-182">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-182">Required.</span></span>  <br/> <span data-ttu-id="dc651-p104">Die URL, zu wechseln, wenn die Aktion aufgerufen wird. Die URL-Zeichenfolge ist eine Formatzeichenfolge .NET Framework. Jede-Formatspezifizierer (beispielsweise ' {0} ') entspricht einem **Action** -Parameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-p104">The URL to go to when the action is invoked. The URL string is a .NET Framework format string. Each format specifier (for example, {0}) corresponds to an **Action** parameter. </span></span><br/> <span data-ttu-id="dc651-186">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-186">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-187">**ImageUrl**</span><span class="sxs-lookup"><span data-stu-id="dc651-187">**imageUrl**</span></span> <br/> |<span data-ttu-id="dc651-188">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-188">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p105">Der absolute oder relative Pfad zu dem Symbolbild für die Aktion. Das Symbolbild sollte ein Format von 16 x 16 Pixeln aufweisen.</span><span class="sxs-lookup"><span data-stu-id="dc651-p105">The absolute or relative path to the icon image for the action. The icon image should be 16 x 16 pixels.  </span></span><br/> <span data-ttu-id="dc651-191">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-191">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-192">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-192">**Name**</span></span> <br/> |<span data-ttu-id="dc651-193">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-193">Required.</span></span>  <br/> <span data-ttu-id="dc651-194">Der Name dieser Aktion.</span><span class="sxs-lookup"><span data-stu-id="dc651-194">The name of this action.</span></span>  <br/> <span data-ttu-id="dc651-195">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-195">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-196">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-196">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-197">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-197">Optional.</span></span>  <br/> <span data-ttu-id="dc651-198">Der Standardanzeigename für diese Aktion.</span><span class="sxs-lookup"><span data-stu-id="dc651-198">The default display name for this action.</span></span>  <br/> <span data-ttu-id="dc651-199">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-199">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-200">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-200">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-201">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-201">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p106">Gibt an, ob diese Aktion häufig verwendet wird. Wird von der BDC-Clientlaufzeit zum Zwischenspeichern dieser Aktion verwendet.</span><span class="sxs-lookup"><span data-stu-id="dc651-p106">Specifies whether this action is used frequently. This is used by the BDC client runtime to cache this action.  </span></span><br/> <span data-ttu-id="dc651-204">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-204">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-205">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-205">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-206">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-206">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-207">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-207">**Element**</span></span>|<span data-ttu-id="dc651-208">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-208">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-209">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-209">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-210">Die lokalisierten Namen der Aktion.</span><span class="sxs-lookup"><span data-stu-id="dc651-210">The localized names of the action.</span></span>  <br/> |
| [<span data-ttu-id="dc651-211">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-211">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-212">Die Eigenschaften der Aktion.</span><span class="sxs-lookup"><span data-stu-id="dc651-212">The properties of the action.</span></span>  <br/> |
| [<span data-ttu-id="dc651-213">"ActionParameters"-Element in Aktion ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-213">ActionParameters Element in Action (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-214">Die Parameter der Aktion.</span><span class="sxs-lookup"><span data-stu-id="dc651-214">The parameters of the action.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-215">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-215">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-216">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-216">**Element**</span></span>|<span data-ttu-id="dc651-217">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-217">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-218">Actions-Element in "Entity" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-218">Actions Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-219">Die Liste der Aktionen eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-219">The list of actions of an external content type.</span></span>  <br/> |
   

## <a name="actionparameter-element"></a><span data-ttu-id="dc651-220">ActionParameter-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-220">ActionParameter element</span></span>
<span data-ttu-id="dc651-221"><a name="bkmk_ActionParameter"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-221"></span></span>

<span data-ttu-id="dc651-p107">Gibt die Parameter einer URL-basierten Aktion an. Hiermit wird definiert, wie die URL einer Aktion mit **EntityInstance**-spezifischen Daten parametrisiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="dc651-p107">Specifies the parameters of a URL-based action. It defines how to parameterize the URL of an action with **EntityInstance**-specific data.</span></span>
  
    
    
 <span data-ttu-id="dc651-224">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-224">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-225">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-225">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="dc651-226">Das URL-Attribut einer URL-basierten kann Parameter mithilfe des **ActionParameter**-Elements empfangen.</span><span class="sxs-lookup"><span data-stu-id="dc651-226">The URL attribute of a URL-based action can receive parameters by using the **ActionParameter** element.</span></span>
  
    
    

> <span data-ttu-id="dc651-227">**Wichtig:**
> **ActionParameters** können entweder Bezeichnerwerte oder Werte darstellen, die **TypeDescriptors** in einem **SpecificFinder** der **Entity** entsprechen.</span><span class="sxs-lookup"><span data-stu-id="dc651-227">**Important:**
**ActionParameters** can either represent identifier values, or values that correspond to **TypeDescriptors** in a **SpecificFinder** of the **Entity**.</span></span> <span data-ttu-id="dc651-228">Der **ActionParameter** stellt einen Bezeichnerwert dar, wenn die **IdOrdinal**-Eigenschaft vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-228">The **ActionParameter** represents an identifier value when the **IdOrdinal** property is present.</span></span> <span data-ttu-id="dc651-229">Der Wert der Eigenschaft gibt den Index des Bezeichners an, dessen Wert dieser **ActionParameter** darstellt.</span><span class="sxs-lookup"><span data-stu-id="dc651-229">The value of the property specifies the index of the identifier whose value this **ActionParameter** represents.</span></span> <span data-ttu-id="dc651-230">Wenn die **IdOrdinal**-Eigenschaft nicht angegeben ist, stellt der **ActionParameter** einen **TypeDescriptor** dar, und das **Name**-Attribut gibt an, welcher Typdeskriptor dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-230">If the **IdOrdinal** property is not specified, the **ActionParameter** represents a **TypeDescriptor**, and the **Name** attribute specifies which type descriptor is being represented.</span></span> <span data-ttu-id="dc651-231">Das **Name**-Attribut wird als **gepunkteter Pfad** angegeben.</span><span class="sxs-lookup"><span data-stu-id="dc651-231">The **Name** attribute is specified as a **Dotted Path**.</span></span> 
  
    
    

<span data-ttu-id="dc651-232">Das **ActionParameter**-Element akzeptiert die folgende Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="dc651-232">The **ActionParameter** element accepts the following property.</span></span>
  
    
    

> <span data-ttu-id="dc651-233">**Wichtig:** Bei Eigenschaften wird die Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="dc651-233">**Important** Properties are case-sensitive.</span></span> 
  
    
    


<span data-ttu-id="dc651-234">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="dc651-234">**Properties**</span></span>


|<span data-ttu-id="dc651-235">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="dc651-235">**Property**</span></span>|<span data-ttu-id="dc651-236">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-236">**Type**</span></span>|<span data-ttu-id="dc651-237">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-237">**Description**</span></span>|<span data-ttu-id="dc651-238">**Erforderlich**</span><span class="sxs-lookup"><span data-stu-id="dc651-238">**Required.**</span></span>|<span data-ttu-id="dc651-239">**Standardwert**</span><span class="sxs-lookup"><span data-stu-id="dc651-239">**Default Value**</span></span>|<span data-ttu-id="dc651-240">**Grenzwerte/akzeptierte Werte**</span><span class="sxs-lookup"><span data-stu-id="dc651-240">**Limits/Accepted Values**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="dc651-241">**IdOrdinal**</span><span class="sxs-lookup"><span data-stu-id="dc651-241">**IdOrdinal**</span></span> <br/> |<span data-ttu-id="dc651-242">**System.Int32**</span><span class="sxs-lookup"><span data-stu-id="dc651-242">**System.Int32**</span></span> <br/> |<span data-ttu-id="dc651-243">Gibt an, ob **ActionParameter** einen Bezeichner anstelle eines Felds darstellt.</span><span class="sxs-lookup"><span data-stu-id="dc651-243">Specifies if the **ActionParameter** represents an identifier instead of a field.</span></span> <br/> |<span data-ttu-id="dc651-244">Optional</span><span class="sxs-lookup"><span data-stu-id="dc651-244">Optional</span></span>  <br/> |||
   



```XML
<ActionParameter Index = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </ActionParameter>
```

<span data-ttu-id="dc651-245">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-245">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-246">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-246">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-247">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-247">**Attribute**</span></span>|<span data-ttu-id="dc651-248">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-248">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-249">**Index**</span><span class="sxs-lookup"><span data-stu-id="dc651-249">**Index**</span></span> <br/> |<span data-ttu-id="dc651-250">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-250">Required.</span></span>  <br/> <span data-ttu-id="dc651-251">Ein Ordnungszahlenattribut, das die Position dieses **ActionParameter**-Elements unter anderen **ActionParameters** in der URL angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-251">An ordinal attribute that specifies the position of this **ActionParameter** among other **ActionParameters** in the URL.</span></span> <br/> <span data-ttu-id="dc651-252">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-252">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="dc651-253">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-253">**Name**</span></span> <br/> |<span data-ttu-id="dc651-254">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-254">Required.</span></span>  <br/> <span data-ttu-id="dc651-255">Der Name des **ActionParameter**-Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-255">The name of the **ActionParameter**.</span></span>  <br/> <span data-ttu-id="dc651-256">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-256">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-257">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-257">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-258">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-258">Optional.</span></span>  <br/> <span data-ttu-id="dc651-259">Der Standardanzeigename für **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="dc651-259">The default display name for the **ActionParameter**.</span></span>  <br/> <span data-ttu-id="dc651-260">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-260">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-261">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-261">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-262">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-262">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p109"> Gibt an, ob dieses **ActionParameter**-Element häufig verwendet wird. Dieses Attribut wird von der BDC-Client-Laufzeitumgebung zum Zwischenspeichern dieses **Action**-Elements verwendet. </span><span class="sxs-lookup"><span data-stu-id="dc651-p109">Specifies whether this **ActionParameter** is used frequently. This attribute is used by the BDC client runtime to cache this **Action**.  </span></span><br/> <span data-ttu-id="dc651-265">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-265">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-266">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-266">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-267">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-267">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-268">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-268">**Element**</span></span>|<span data-ttu-id="dc651-269">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-269">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-270">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-270">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-271">Die lokalisierten Anzeigenamen für **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="dc651-271">The localized display names for the **ActionParameter**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-272">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-272">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-273">Die Eigenschaften des **ActionParameter**-Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-273">The properties of the **ActionParameter**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-274">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-274">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-275">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-275">**Element**</span></span>|<span data-ttu-id="dc651-276">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-276">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-277">"ActionParameters"-Element in Aktion ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-277">ActionParameters Element in Action (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-278">Das **ActionParameters**-Element, das diesen **ActionParameter**-Parameter enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-278">The **ActionParameters** element that contains this **ActionParameter**.</span></span>  <br/> |
   

## <a name="actionparameters-element"></a><span data-ttu-id="dc651-279">"ActionParameters"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-279">ActionParameters element</span></span>
<span data-ttu-id="dc651-280"><a name="bkmk_ActionParameters"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-280"></span></span>

<span data-ttu-id="dc651-281">Gibt eine Liste von **ActionParameters** für eine Aktion an.</span><span class="sxs-lookup"><span data-stu-id="dc651-281">Specifies a list of **ActionParameters** for an action.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-282">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-282">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-283">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-283">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<ActionParameters></ActionParameters>
```

<span data-ttu-id="dc651-284">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-284">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-285">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-285">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-286">Keine.</span><span class="sxs-lookup"><span data-stu-id="dc651-286">None.</span></span>
  
    
    
 <span data-ttu-id="dc651-287">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-287">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-288">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-288">**Element**</span></span>|<span data-ttu-id="dc651-289">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-289">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-290">ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-290">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-291">Ein **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="dc651-291">An **ActionParameter**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-292">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-292">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-293">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-293">**Element**</span></span>|<span data-ttu-id="dc651-294">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-294">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-295">"Action"-Element in "Actions" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-295">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-296">Die **Action**, zu dem diese **ActionParameters** gehören.</span><span class="sxs-lookup"><span data-stu-id="dc651-296">The **Action** that these **ActionParameters** belong to.</span></span> <br/> |
   

## <a name="actions-element"></a><span data-ttu-id="dc651-297">"Actions"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-297">Actions element</span></span>
<span data-ttu-id="dc651-298"><a name="bkmk_Actions"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-298"></span></span>

<span data-ttu-id="dc651-299">Gibt eine Liste mit Aktionen eines externen Inhaltstyps an.</span><span class="sxs-lookup"><span data-stu-id="dc651-299">Specifies a list of actions of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-300">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-300">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-301">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-301">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Actions></Actions>
```

<span data-ttu-id="dc651-302">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-302">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-303">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-303">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-304">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-304">None</span></span>
  
    
    
 <span data-ttu-id="dc651-305">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-305">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-306">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-306">**Element**</span></span>|<span data-ttu-id="dc651-307">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-307">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-308">"Action"-Element in "Actions" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-308">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-309">Eine Aktion eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-309">An action of an external content type.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-310">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-310">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-311">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-311">**Element**</span></span>|<span data-ttu-id="dc651-312">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-312">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-313">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-313">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-314">Der externe Inhaltstyp, dem diese Aktionen angehören.</span><span class="sxs-lookup"><span data-stu-id="dc651-314">The external content type that these actions belong to.</span></span>  <br/> |
   

## <a name="association-element"></a><span data-ttu-id="dc651-315">"Association"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-315">Association element</span></span>
<span data-ttu-id="dc651-316"><a name="bkmk_Association"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-316"></span></span>

<span data-ttu-id="dc651-p110">Das Association-Element verknüpft verwandte externe Inhaltstypen in einem System. Angenommen, ein Kunde zugeordnet ist einen Auftrag im System AdventureWorks: ein Kunde macht Aufträge. Eine Zuordnung enthält dann Zeiger auf die Quell- und Ziel externe Inhaltstypen und einen Zeiger auf die Geschäftslogik (ein **MethodInstance** -Objekt), die einen Client zum Abrufen des externen zielinhaltstyp von der externen quellinhaltstyp ermöglicht. Das Traversieren der ein **Association** ist ein Aufruf der Methode für das externe System.</span><span class="sxs-lookup"><span data-stu-id="dc651-p110">The Association element links related external content types within a system. For example, a customer is associated with a sales order in the AdventureWorks system: a customer makes sales orders. An Association holds pointers to the source and destination external content types and a pointer to the business logic (a **MethodInstance** object) that allows a client to get the destination external content type from the source external content type. The traversal of an **Association** is a method call on the external system.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-321">**Namespace:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog</span><span class="sxs-lookup"><span data-stu-id="dc651-321">**Namespace:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog</span></span>
  
    
    
 <span data-ttu-id="dc651-322">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-322">**Schema:** BDCMetadata</span></span>
  
    
    

> <span data-ttu-id="dc651-323">**Wichtig:** Bei Eigenschaften wird die Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="dc651-323">**Important** Properties are case-sensitive.</span></span> 
  
    
    


<span data-ttu-id="dc651-324">**Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="dc651-324">**Properties**</span></span>


|<span data-ttu-id="dc651-325">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="dc651-325">**Property**</span></span>|<span data-ttu-id="dc651-326">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-326">**Type**</span></span>|<span data-ttu-id="dc651-327">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-327">**Description**</span></span>|<span data-ttu-id="dc651-328">**Erforderlich**</span><span class="sxs-lookup"><span data-stu-id="dc651-328">**Required**</span></span>|<span data-ttu-id="dc651-329">**Standardwert**</span><span class="sxs-lookup"><span data-stu-id="dc651-329">**Default Value**</span></span>|<span data-ttu-id="dc651-330">**Grenzwerte/akzeptierte Werte**</span><span class="sxs-lookup"><span data-stu-id="dc651-330">**Limits/Accepted Values**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="dc651-331">**HideOnProfilePage**</span><span class="sxs-lookup"><span data-stu-id="dc651-331">**HideOnProfilePage**</span></span> <br/> |<span data-ttu-id="dc651-332">**System.Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-332">**System.Boolean**</span></span> <br/> |<span data-ttu-id="dc651-333">Gibt an, ob der verwandte externe Inhaltstyp der Profilseite des externen Masterinhaltstyps hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="dc651-333">Specifies whether the related external content type should be added to the profile page of the master external content type.</span></span>  <br/> |<span data-ttu-id="dc651-334">Optional</span><span class="sxs-lookup"><span data-stu-id="dc651-334">Optional</span></span>  <br/> |||
   



```XML
<Association Type = "String" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Association>
```

<span data-ttu-id="dc651-335">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-335">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-336">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-336">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-337">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-337">**Attribute**</span></span>|<span data-ttu-id="dc651-338">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-338">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-339">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-339">**Type**</span></span> <br/> |<span data-ttu-id="dc651-340">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-340">Required.</span></span>  <br/> <span data-ttu-id="dc651-341">Die **MethodInstanceType**, die den Typ der Zuordnung angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-341">The **MethodInstanceType** that specifies the type of the Association.</span></span> <br/> <span data-ttu-id="dc651-342">In der folgenden Tabelle sind die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-342">The following table lists the possible values for this attribute.</span></span>  <br/>         <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-343">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-343">Value</span></span></p></th><th><p><span data-ttu-id="dc651-344">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-344">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-345">AssociationNavigator</span><span class="sxs-lookup"><span data-stu-id="dc651-345">AssociationNavigator</span></span></p></td><td><p><span data-ttu-id="dc651-346">Die **MethodInstance** ist ein **AssociationNavigator**.</span><span class="sxs-lookup"><span data-stu-id="dc651-346">The **MethodInstance** is an **AssociationNavigator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-347">Associator</span><span class="sxs-lookup"><span data-stu-id="dc651-347">Associator</span></span></p></td><td><p><span data-ttu-id="dc651-348">Die **MethodInstance** ist ein **Associator**.</span><span class="sxs-lookup"><span data-stu-id="dc651-348">The **MethodInstance** is an **Associator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-349">Disassociator</span><span class="sxs-lookup"><span data-stu-id="dc651-349">Disassociator</span></span></p></td><td><p><span data-ttu-id="dc651-350">Die **MethodInstance** ist eine **Disassociator**.</span><span class="sxs-lookup"><span data-stu-id="dc651-350">The **MethodInstance** is a **Disassociator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-351">**BulkAssociatedIdEnumerator**</span><span class="sxs-lookup"><span data-stu-id="dc651-351">**BulkAssociatedIdEnumerator**</span></span></p></td><td><p><span data-ttu-id="dc651-352">Die **MethodInstance** ist eine **BulkAssociatedIdEnumerator**.</span><span class="sxs-lookup"><span data-stu-id="dc651-352">The **MethodInstance** is a **BulkAssociatedIdEnumerator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-353">**BulkAssociationNavigator**</span><span class="sxs-lookup"><span data-stu-id="dc651-353">**BulkAssociationNavigator**</span></span></p></td><td><p><span data-ttu-id="dc651-354">Die **MethodInstance** ist ein **BulkAssociationNavigator**.</span><span class="sxs-lookup"><span data-stu-id="dc651-354">The **MethodInstance** is a **BulkAssociationNavigator**.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="dc651-355">Standard</span><span class="sxs-lookup"><span data-stu-id="dc651-355">Default</span></span>  <br/> |<span data-ttu-id="dc651-356">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-356">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p111"> Gibt an, ob die Zuordnung der Standardwert zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. Wenn es sich bei Festlegung auf **true**, die Zuordnung der Standardwert zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. Wenn auf **false**, die Zuordnung nicht die Standardeinstellung zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. </span><span class="sxs-lookup"><span data-stu-id="dc651-p111">Specifies whether the Association is the default among all Associations sharing its type within the containing external content type. If set to **true**, the Association is the default among all Associations sharing its type within the containing external content type. If set to **false**, the Association is not the default among all Associations sharing its type within the containing external content type.  </span></span><br/> <span data-ttu-id="dc651-360">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-360">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-361">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-361">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-362">ReturnParameterName</span><span class="sxs-lookup"><span data-stu-id="dc651-362">ReturnParameterName</span></span>  <br/> |<span data-ttu-id="dc651-363">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-363">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p112"> Der Name des Parameters, der die **ReturnTypeDescriptor** der Zuordnung enthält. Das **Direction** -Attribut des Parameters muss entweder ",", "INOUT-" oder "Zurück" den Wert enthalten. </span><span class="sxs-lookup"><span data-stu-id="dc651-p112">The name of the parameter that contains the **ReturnTypeDescriptor** of the Association. The **Direction** attribute of the parameter must contain a value of either "Out", "InOut", or "Return". </span></span><br/> <span data-ttu-id="dc651-366">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-366">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-367">ReturnTypeDescriptorName</span><span class="sxs-lookup"><span data-stu-id="dc651-367">ReturnTypeDescriptorName</span></span>  <br/> |<span data-ttu-id="dc651-368">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-368">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p113">Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="dc651-p113">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="dc651-371">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-371">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-372">ReturnTypeDescriptorLevel</span><span class="sxs-lookup"><span data-stu-id="dc651-372">ReturnTypeDescriptorLevel</span></span>  <br/> |<span data-ttu-id="dc651-373">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-373">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p114">Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="dc651-p114">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="dc651-376">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-376">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="dc651-377">ReturnTypeDescriptorPath</span><span class="sxs-lookup"><span data-stu-id="dc651-377">ReturnTypeDescriptorPath</span></span>  <br/> |<span data-ttu-id="dc651-378">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-378">Optional.</span></span>  <br/> <span data-ttu-id="dc651-379">Der gepunktete Pfad des **TypeDescriptors** der Zuordnung. </span><span class="sxs-lookup"><span data-stu-id="dc651-379">The dotted path of the **TypeDescriptor** of the Association.</span></span> <br/> <span data-ttu-id="dc651-380">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-380">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-381">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-381">Name</span></span>  <br/> |<span data-ttu-id="dc651-382">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-382">Required.</span></span>  <br/> <span data-ttu-id="dc651-383">Der Name der Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-383">The name of the Association.</span></span>  <br/> <span data-ttu-id="dc651-384">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-384">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-385">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-385">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-386">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-386">Optional.</span></span>  <br/> <span data-ttu-id="dc651-387">Der Standardanzeigename für die Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-387">The default display name for the Association.</span></span>  <br/> <span data-ttu-id="dc651-388">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-388">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-389">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-389">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-390">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-390">Optional.</span></span>  <br/> <span data-ttu-id="dc651-391">Gibt an, ob diese Zuordnung häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-391">Specifies whether this Association is frequently used.</span></span>  <br/> <span data-ttu-id="dc651-392">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-392">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-393">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-393">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-394">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-394">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-395">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-395">**Element**</span></span>|<span data-ttu-id="dc651-396">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-396">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-397">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-397">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-398">Das **LocalizedDisplayNames** -Element gibt eine Liste der lokalisierten Namen für die Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-398">The **LocalizedDisplayNames** element specifies a list of localized names for the Association.</span></span> <br/> |
| [<span data-ttu-id="dc651-399">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-399">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-400">Das Properties-Element gibt die Eigenschaften der Zuordnung an.</span><span class="sxs-lookup"><span data-stu-id="dc651-400">The Properties element specifies the properties of the Association.</span></span>  <br/> |
| [<span data-ttu-id="dc651-401">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-401">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-402">Das **AccessControlList** -Element gibt einen Satz von Zugriffsrechten für die Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-402">The **AccessControlList** element specifies a set of access rights for the Association.</span></span> <br/> |
| [<span data-ttu-id="dc651-403">SourceEntity-Element in "Association" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-403">SourceEntity Element in Association (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/19fb5f38-4e85-7fb0-2562-281b9a9ffbef%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-404">Das **SourceEntity** -Element gibt die externen quellinhaltstyp in der Zuordnung angegeben.</span><span class="sxs-lookup"><span data-stu-id="dc651-404">The **SourceEntity** element specifies the source external content type in the association.</span></span> <br/> |
| [<span data-ttu-id="dc651-405">DestinationEntity-Element in "Association" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-405">DestinationEntity Element in Association (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/15c53c3b-888d-67c7-af7d-ef36922eeebc%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-406">Das **DestinationEntity** -Element gibt den externen zielinhaltstyp in der Zuordnung angegeben.</span><span class="sxs-lookup"><span data-stu-id="dc651-406">The **DestinationEntity** element specifies the destination external content type in the Association.</span></span> <br/> |
   
 <span data-ttu-id="dc651-407">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-407">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-408">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-408">**Element**</span></span>|<span data-ttu-id="dc651-409">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-409">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-410">"MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-410">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-411">Die **MethodInstances** -Element, das die Zuordnung enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-411">The **MethodInstances** element that contains the Association.</span></span> <br/> |
   

## <a name="associationgroup-element"></a><span data-ttu-id="dc651-412">"AssociationGroup"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-412">AssociationGroup element</span></span>
<span data-ttu-id="dc651-413"><a name="bkmk_AssociationGroup"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-413"></span></span>

<span data-ttu-id="dc651-p115">Legt ein **AssociationGroup**-Element fest. **AssociationGroup** ist ein Konstrukt, das die zugehörigen **AssociationMethods** zusammenbindet. Beispielsweise sind **GetOrdersForCustomer**, **GetCustomerForOrder** und **AssociateCustomerToOrder** zugeordnete Methoden, die in der gleichen Beziehung zwischen Kunde und Bestellung arbeiten.</span><span class="sxs-lookup"><span data-stu-id="dc651-p115">Specifies an **AssociationGroup**. **AssociationGroup** is a construct that ties the related **AssociationMethods** together. For example, **GetOrdersForCustomer**, **GetCustomerForOrder**, and **AssociateCustomerToOrder** are all association methods that work on the same relationship between Customer and Order.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-417">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-417">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-418">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-418">**Schema:** BDCMetadata</span></span>
  
    
    
 <span data-ttu-id="dc651-419">AssociationGroup muss für das Entity-Element definiert werden, das das Ziel der AssociationReferences darstellt, die nicht als Reverse gekennzeichnet sind, oder die Quelle der AssociationReferences, die als Reverse gekennzeichnet sind.</span><span class="sxs-lookup"><span data-stu-id="dc651-419">**AssociationGroup** must be defined on the Entity element that is the Destination of the **AssociationReferences** that are not marked as **Reverse**, or the Source of the **AssociationReferences** that are marked as Reverse.</span></span>
  
    
    



```XML
<AssociationGroup Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </AssociationGroup>
```

<span data-ttu-id="dc651-420">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-420">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-421">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-421">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-422">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-422">**Attribute**</span></span>|<span data-ttu-id="dc651-423">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-423">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-424">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-424">**Name**</span></span> <br/> |<span data-ttu-id="dc651-425">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-425">Required.</span></span>  <br/> <span data-ttu-id="dc651-426">Der Name des **AssociationGroup**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-426">The name of the **AssociationGroup**.</span></span>  <br/> <span data-ttu-id="dc651-427">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-427">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-428">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-428">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-429">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-429">Optional.</span></span>  <br/> <span data-ttu-id="dc651-430">Der Standardanzeigename des **AssociationGroup**-Elements.</span><span class="sxs-lookup"><span data-stu-id="dc651-430">The default display name of the **AssociationGroup**.</span></span>  <br/> <span data-ttu-id="dc651-431">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-431">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-432">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-432">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-433">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-433">Optional.</span></span>  <br/> <span data-ttu-id="dc651-434">Gibt an, ob das **AssociationGroup** häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-434">Specifies whether the **AssociationGroup** is used frequently.</span></span> <br/> <span data-ttu-id="dc651-435">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-435">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-436">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-436">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-437">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-437">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-438">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-438">**Element**</span></span>|<span data-ttu-id="dc651-439">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-439">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-440">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-440">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-441">Die lokalisierten Namen des **AssociationGroup**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-441">The localized names of the **AssociationGroup**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-442">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-442">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-443">Die Eigenschaften des **AssociationGroup**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-443">The properties of the **AssociationGroup**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-444">"AssociationReference"-Element in "AssociationGroup" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-444">AssociationReference Element in AssociationGroup (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e32c5267-53b0-9ff0-6e9a-1cb00d9f1d57%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-445">Ein **AssociationReference**-Element eines **AssociationGroup**-Elements.</span><span class="sxs-lookup"><span data-stu-id="dc651-445">An **AssociationReference** of an **AssociationGroup**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-446">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-446">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-447">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-447">**Element**</span></span>|<span data-ttu-id="dc651-448">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-448">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-449">AssociationGroups-Element in "Entity" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-449">AssociationGroups Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-450">Das **AssociationGroups**-Element, das diesen **AssociationGroup**-Parameter enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-450">The **AssociationGroups** element that contains this **AssociationGroup**.</span></span>  <br/> |
   

## <a name="associationgroups-element"></a><span data-ttu-id="dc651-451">AssociationGroups (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-451">AssociationGroups element</span></span>
<span data-ttu-id="dc651-452"><a name="bkmk_AssociationGroups"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-452"></span></span>

<span data-ttu-id="dc651-453">Gibt eine Liste von **AssociationGroup**-Elementen an.</span><span class="sxs-lookup"><span data-stu-id="dc651-453">Specifies a list of **AssociationGroup** elements.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-454">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-454">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-455">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-455">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AssociationGroups></AssociationGroups>
```

<span data-ttu-id="dc651-456">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-456">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-457">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-457">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-458">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-458">None</span></span>
  
    
    
 <span data-ttu-id="dc651-459">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-459">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-460">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-460">**Element**</span></span>|<span data-ttu-id="dc651-461">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-461">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-462">"AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-462">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-463">Eine Einstellung für **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="dc651-463">An **AssociationGroup**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-464">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-464">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-465">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-465">**Element**</span></span>|<span data-ttu-id="dc651-466">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-466">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-467">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-467">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-468">Der externe Inhaltstyp, dem dieses **AssociationGroups**-Element zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-468">The external content type that this **AssociationGroups** element is associated with.</span></span> <br/> |
   

## <a name="associationreference-element"></a><span data-ttu-id="dc651-469">"AssociationReference"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-469">AssociationReference element</span></span>
<span data-ttu-id="dc651-470"><a name="bkmk_AssociationReference"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-470"></span></span>

<span data-ttu-id="dc651-471">Gibt einen **AssociationReference** in einer **AssociationGroup** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-471">Specifies an **AssociationReference** in an **AssociationGroup**.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-472">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-472">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-473">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-473">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AssociationReference EntityNamespace = "String" EntityName = "String" AssociationName = "String" Reverse = "Boolean"> </AssociationReference>
```

<span data-ttu-id="dc651-474">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-474">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-475">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-475">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-476">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-476">**Attribute**</span></span>|<span data-ttu-id="dc651-477">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-477">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-478">EntityNamespace</span><span class="sxs-lookup"><span data-stu-id="dc651-478">EntityNamespace</span></span>  <br/> |<span data-ttu-id="dc651-479">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-479">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p116"> Der Namespace des externen Inhaltstyps, in dem die **Association** definiert ist. Wenn **EntityName** angegeben ist, wird **EntityNamespace** benötigt. </span><span class="sxs-lookup"><span data-stu-id="dc651-p116">The namespace of the external content type where the **Association** is defined. If **EntityName** is specified, **EntityNamespace** is required. </span></span><br/> <span data-ttu-id="dc651-482">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-482">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-483">EntityName</span><span class="sxs-lookup"><span data-stu-id="dc651-483">EntityName</span></span>  <br/> |<span data-ttu-id="dc651-484">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-484">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p117"> Der Name des externen Inhaltstyps, in dem die **Association** definiert ist. Wenn **EntityNamespace** angegeben ist, wird **EntityName** benötigt. </span><span class="sxs-lookup"><span data-stu-id="dc651-p117">The name of the external content type where the **Association** is defined. If **EntityNamespace** is specified, **EntityName** is required. </span></span><br/> <span data-ttu-id="dc651-487">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-487">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-488">AssociationName</span><span class="sxs-lookup"><span data-stu-id="dc651-488">AssociationName</span></span>  <br/> |<span data-ttu-id="dc651-489">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-489">Required.</span></span>  <br/> <span data-ttu-id="dc651-490">Der Name des **Association**-Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-490">The name of the **Association**.</span></span>  <br/> <span data-ttu-id="dc651-491">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-491">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-492">Reverse</span><span class="sxs-lookup"><span data-stu-id="dc651-492">Reverse</span></span>  <br/> |<span data-ttu-id="dc651-493">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-493">Optional.</span></span>  <br/> <span data-ttu-id="dc651-494">Gibt an, dass Quelle und Ziel der **Zuordnung**, auf die verwiesen wird,  umgekehrt wurden.</span><span class="sxs-lookup"><span data-stu-id="dc651-494">Specifies that the referenced **Association** has its source and destination reversed.</span></span> <span data-ttu-id="dc651-495">Dies würde darauf hinweisen, dass die **Zuordnung** in der entgegengesetzten Richtung im Vergleich zu anderen Zuordnungen in derselben **AssociationGroup** arbeitet.</span><span class="sxs-lookup"><span data-stu-id="dc651-495">This would indicate the **Association** is working in the opposite direction compared to other associations in the same **AssociationGroup**.</span></span> <span data-ttu-id="dc651-496">Wenn die **AssociationGroup** beispielsweise auf eine **Association** „GetOrdersForCustomer“ verweist und dabei Auftragsartikel für das angegebene Kundenelement zurückgibt, so weist die **AssociationGroup** die Richtung „Kunde“ zu „Auftrag“ auf.</span><span class="sxs-lookup"><span data-stu-id="dc651-496">For example, if the **AssociationGroup** references an **Association** "GetOrdersForCustomer", returning Order items for the given Customer item, then the **AssociationGroup** is in the direction of Customer to Order.</span></span> <span data-ttu-id="dc651-497">Der andere **AssociationReference**, der auf eine andere Zuordnung „GetCustomerForOrder“ verweist, muss als umgekehrt gekennzeichnet werden, da diese Zuordnung die Richtung „Auftrag“ zu „Kunde“ aufweist.</span><span class="sxs-lookup"><span data-stu-id="dc651-497">The other **AssociationReference**, referencing another association "GetCustomerForOrder", must be marked as reverse, because this association is in the direction of Order to Customer.</span></span>  <br/> <span data-ttu-id="dc651-498">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-498">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-499">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-499">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-500">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-500">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-501">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-501">None</span></span>
  
    
    
 <span data-ttu-id="dc651-502">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-502">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-503">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-503">**Element**</span></span>|<span data-ttu-id="dc651-504">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-504">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-505">"AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-505">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-506">Die **AssociationGroup**, zu der dieser **AssociationReference** gehört.</span><span class="sxs-lookup"><span data-stu-id="dc651-506">The **AssociationGroup** that this **AssociationReference** belongs to.</span></span> <br/> |
   

## <a name="converttype-element"></a><span data-ttu-id="dc651-507">ConvertType (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-507">ConvertType element</span></span>
<span data-ttu-id="dc651-508"><a name="bkmk_ConvertType"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-508"></span></span>

<span data-ttu-id="dc651-509">Gibt die Regel zur Konvertierung des Datentyps eines Datenwerts in einen anderen Datentyp an.</span><span class="sxs-lookup"><span data-stu-id="dc651-509">Specifies the rule to convert the data type of a data value into another data type.</span></span>
  
    
    
 <span data-ttu-id="dc651-510">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-510">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-511">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-511">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="dc651-512">Das Convert-Element gibt die Regel zur Konvertierung des Datentyps eines Datenwerts in einen anderen Datentyp an.</span><span class="sxs-lookup"><span data-stu-id="dc651-512">Specifies the rule to convert the data type of a data value into another data type.</span></span> <span data-ttu-id="dc651-513">Wenn die Regeln in der Reihenfolge angewendet werden, gibt diese Regel den Datentyp des Datenwert an, der in den vom BDCType-Attribut angegebenen Datentyp konvertiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="dc651-513">When the rules are applied in order, this rule specifies the data type of the data value to be converted to the data type specified by the BDCType attribute.</span></span> <span data-ttu-id="dc651-514">Wenn die Regeln in umgekehrter Reihenfolge angewendet werden, gibt diese Regel den Datentyp des Datenwert an, der in den vom  **LOBType**-Attribut angegebenen Datentyp konvertiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="dc651-514">When the rules are applied in reverse order, this rule specifies the data type of the data value to be converted to the data type specified by the **LOBType** attribute.</span></span> <span data-ttu-id="dc651-515">Diese Regel kann beispielsweise einen Datumswert aus einem externen System in eine kultur- oder gebietsschemasensible Zeichenfolge konvertieren, die dem Benutzer angezeigt wird. Außerdem wird der aktualisierte Wert für diese Zeichenfolge zurück in das Datum konvertiert, das mit dem externen System kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-515">For example, this rule can specify converting a date value obtained from an external system, into a culture and locale sensitive string which will eventually be displayed to the user, and converting the updated value for that string back into the date that is compatible with the external system.</span></span>
  
    
    

> <span data-ttu-id="dc651-516">**Achtung: **
> **ConvertType** unterstützt ausschließlich den gregorianischen Kalender für Konvertierungen zwischen **System.String** und **System.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="dc651-516">**Caution**
**ConvertType** does not support non-Gregorian calendars for conversions between **System.String** and **System.DateTime**.</span></span> 
  
    
    




```XML
<ConvertType LOBType = "String" BDCType = "String"> </ConvertType>
```

<span data-ttu-id="dc651-517">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-517">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-518">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-518">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-519">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-519">**Attribute**</span></span>|<span data-ttu-id="dc651-520">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-520">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-521">LOBType</span><span class="sxs-lookup"><span data-stu-id="dc651-521">LOBType</span></span>  <br/> |<span data-ttu-id="dc651-522">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-522">Required.</span></span>  <br/> <span data-ttu-id="dc651-523">Der Datentyp für die Konvertierung des Datenwerts, wenn die Regeln in umgekehrter Reihenfolge angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-523">The data type to convert the data value into when the rules are applied in reverse order.</span></span>  <br/> <span data-ttu-id="dc651-524">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-524">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-525">BDCType</span><span class="sxs-lookup"><span data-stu-id="dc651-525">BDCType</span></span>  <br/> |<span data-ttu-id="dc651-526">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-526">Required.</span></span>  <br/> <span data-ttu-id="dc651-527">Der Datentyp für die Konvertierung des Datenwerts, wenn die Regeln nacheinander angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-527">The data type to convert the data value into when the rules are applied in order.</span></span>  <br/> <span data-ttu-id="dc651-528">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-528">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-529">LOBLocale</span><span class="sxs-lookup"><span data-stu-id="dc651-529">LOBLocale</span></span>  <br/> |<span data-ttu-id="dc651-530">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-530">Optional.</span></span>  <br/> <span data-ttu-id="dc651-531">Das Gebietsschema der Daten vom externen System.</span><span class="sxs-lookup"><span data-stu-id="dc651-531">The locale of the data that is received from the external system.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-532">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-532">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-533">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-533">None</span></span>
  
    
    
 <span data-ttu-id="dc651-534">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-534">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-535">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-535">**Element**</span></span>|<span data-ttu-id="dc651-536">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-536">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-537">Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-537">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-538">Die Regeln, die auf die in den Datenstrukturen gespeicherten Daten, welche durch **TypeDescriptor** dargestellt sind, angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-538">The rules to apply to the data stored in the data structures that are represented by a **TypeDescriptor**.</span></span>  <br/> |
   

## <a name="defaultvalue-element"></a><span data-ttu-id="dc651-539">"DefaultValue"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-539">DefaultValue element</span></span>
<span data-ttu-id="dc651-540"><a name="bkmk_DefaultValue"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-540"></span></span>

<span data-ttu-id="dc651-541">Stellt einen Standardwert dar.</span><span class="sxs-lookup"><span data-stu-id="dc651-541">Represents a default value.</span></span>
  
    
    
 <span data-ttu-id="dc651-542">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-542">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-543">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-543">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DefaultValue MethodInstanceName = "String" Type = "String"> </DefaultValue>
```

<span data-ttu-id="dc651-544">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-544">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-545">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-545">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-546">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-546">**Attribute**</span></span>|<span data-ttu-id="dc651-547">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-547">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-548">**MethodInstanceName**</span><span class="sxs-lookup"><span data-stu-id="dc651-548">**MethodInstanceName**</span></span> <br/> |<span data-ttu-id="dc651-549">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-549">Required.</span></span>  <br/> <span data-ttu-id="dc651-550">Der Name der **MethodInstance** für das dieser Standardwert gilt.</span><span class="sxs-lookup"><span data-stu-id="dc651-550">The name of the **MethodInstance** to which this DefaultValue applies.</span></span> <br/> <span data-ttu-id="dc651-551">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-551">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-552">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-552">**Type**</span></span> <br/> | <span data-ttu-id="dc651-553">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-553">Required.</span></span> <br/>  <span data-ttu-id="dc651-554">Der Datentyp des Standardwerts</span><span class="sxs-lookup"><span data-stu-id="dc651-554">The data type of the default value.</span></span> <br/>  <span data-ttu-id="dc651-555">Die folgenden Werte können für dieses Attribut verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-555">The following are the acceptable values for this attribute.</span></span> <br/> <span data-ttu-id="dc651-556">**System.Int16**</span><span class="sxs-lookup"><span data-stu-id="dc651-556">**System.Int16**</span></span> <br/> <span data-ttu-id="dc651-557">**System.Int32**</span><span class="sxs-lookup"><span data-stu-id="dc651-557">**System.Int32**</span></span> <br/> <span data-ttu-id="dc651-558">**System.Int64**</span><span class="sxs-lookup"><span data-stu-id="dc651-558">**System.Int64**</span></span> <br/> <span data-ttu-id="dc651-559">**System.Single**</span><span class="sxs-lookup"><span data-stu-id="dc651-559">**System.Single**</span></span> <br/> <span data-ttu-id="dc651-560">**System.Double**</span><span class="sxs-lookup"><span data-stu-id="dc651-560">**System.Double**</span></span> <br/> <span data-ttu-id="dc651-561">**System.Decimal**</span><span class="sxs-lookup"><span data-stu-id="dc651-561">**System.Decimal**</span></span> <br/> <span data-ttu-id="dc651-562">**System.Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-562">**System.Boolean**</span></span> <br/> <span data-ttu-id="dc651-563">**System.Byte**</span><span class="sxs-lookup"><span data-stu-id="dc651-563">**System.Byte**</span></span> <br/> <span data-ttu-id="dc651-564">**System.UInt16**</span><span class="sxs-lookup"><span data-stu-id="dc651-564">**System.UInt16**</span></span> <br/> <span data-ttu-id="dc651-565">**System.UInt32**</span><span class="sxs-lookup"><span data-stu-id="dc651-565">**System.UInt32**</span></span> <br/> <span data-ttu-id="dc651-566">**System.UInt64**</span><span class="sxs-lookup"><span data-stu-id="dc651-566">**System.UInt64**</span></span> <br/> <span data-ttu-id="dc651-567">**System.Guid**</span><span class="sxs-lookup"><span data-stu-id="dc651-567">**System.Guid**</span></span> <br/> <span data-ttu-id="dc651-568">**System.String**</span><span class="sxs-lookup"><span data-stu-id="dc651-568">**System.String**</span></span> <br/> <span data-ttu-id="dc651-569">**System.DateTime**</span><span class="sxs-lookup"><span data-stu-id="dc651-569">**System.DateTime**</span></span> <br/>  <span data-ttu-id="dc651-570">Alle anderen serialisierbaren Typen (beispielsweise  `Type.IsSerializable == true`)</span><span class="sxs-lookup"><span data-stu-id="dc651-570">Any other serializable type (such as where `Type.IsSerializable == true`)</span></span>  <br/>  <span data-ttu-id="dc651-571">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-571">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="dc651-572">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-572">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-573">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-573">None</span></span>
  
    
    
 <span data-ttu-id="dc651-574">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-574">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-575">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-575">**Element**</span></span>|<span data-ttu-id="dc651-576">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-576">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-577">DefaultValues-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-577">DefaultValues Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx)||
   

## <a name="defaultvalues-element"></a><span data-ttu-id="dc651-578">DefaultValues-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-578">DefaultValues element</span></span>
<span data-ttu-id="dc651-579"><a name="bkmk_DefaultValues"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-579"></span></span>

<span data-ttu-id="dc651-580">Gibt eine Liste von **DefaultValues** von einem **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-580">Specifies a list of **DefaultValues** of a **TypeDescriptor**.</span></span>
  
    
    
 <span data-ttu-id="dc651-581">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-581">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-582">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-582">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DefaultValues></DefaultValues>
```

<span data-ttu-id="dc651-583">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-583">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-584">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-584">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-585">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-585">None</span></span>
  
    
    
 <span data-ttu-id="dc651-586">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-586">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-587">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-587">**Element**</span></span>|<span data-ttu-id="dc651-588">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-588">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-589">"DefaultValue"-Element in "DefaultValues" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-589">DefaultValue Element in DefaultValues (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ddb67f64-6361-7b59-6724-4680484d585d%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-590">Der Standardwert eines **TypeDescriptor**-Elements für ein **MethodInstance**-Element.</span><span class="sxs-lookup"><span data-stu-id="dc651-590">The default value of a **TypeDescriptor** for a **MethodInstance**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-591">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-591">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-592">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-592">**Element**</span></span>|<span data-ttu-id="dc651-593">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-593">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-594">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-594">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-595">Das **TypeDescriptor**-Element, zu dem diese **DefaultValues**-Elemente gehören.</span><span class="sxs-lookup"><span data-stu-id="dc651-595">The **TypeDescriptor** that these **DefaultValues** belong to.</span></span> <br/> |
   

## <a name="destinationentity-element"></a><span data-ttu-id="dc651-596">DestinationEntity-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-596">DestinationEntity element</span></span>
<span data-ttu-id="dc651-597"><a name="bkmk_DestinationEntity"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-597"></span></span>

<span data-ttu-id="dc651-598">Gibt den externen Inhaltstyp des Ziels im **Association**-Element an.</span><span class="sxs-lookup"><span data-stu-id="dc651-598">Specifies the destination external content type in the **Association**.</span></span>
  
    
    
 <span data-ttu-id="dc651-599">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-599">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-600">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-600">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DestinationEntity Namespace = "String" Name = "String"> </DestinationEntity>
```

<span data-ttu-id="dc651-601">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-601">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-602">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-602">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-603">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-603">**Attribute**</span></span>|<span data-ttu-id="dc651-604">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-604">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-605">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="dc651-605">**Namespace**</span></span> <br/> |<span data-ttu-id="dc651-606">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-606">Required.</span></span>  <br/> <span data-ttu-id="dc651-607">Der Name des Entitätsnamespaces.</span><span class="sxs-lookup"><span data-stu-id="dc651-607">The name of the entity namespace.</span></span>  <br/> <span data-ttu-id="dc651-608">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-608">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-609">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-609">**Name**</span></span> <br/> |<span data-ttu-id="dc651-610">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-610">Required.</span></span>  <br/> <span data-ttu-id="dc651-611">Der Name der Zielentität.</span><span class="sxs-lookup"><span data-stu-id="dc651-611">The name of the destination entity.</span></span>  <br/> <span data-ttu-id="dc651-612">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-612">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="dc651-613">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-613">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-614">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-614">None</span></span>
  
    
    
 <span data-ttu-id="dc651-615">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-615">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-616">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-616">**Element**</span></span>|<span data-ttu-id="dc651-617">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-617">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-618">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-618">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)||
   

## <a name="entities-element"></a><span data-ttu-id="dc651-619">"Entities"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-619">Entities element</span></span>
<span data-ttu-id="dc651-620"><a name="bkmk_Entities"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-620"></span></span>

<span data-ttu-id="dc651-621">Gibt eine Liste der externen Inhaltstypen in einem externen System an.</span><span class="sxs-lookup"><span data-stu-id="dc651-621">Specifies a list of external content types in an external system.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-622">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-622">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-623">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-623">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Entities></Entities>
```

<span data-ttu-id="dc651-624">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-624">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-625">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-625">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-626">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-626">None</span></span>
  
    
    
 <span data-ttu-id="dc651-627">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-627">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-628">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-628">**Element**</span></span>|<span data-ttu-id="dc651-629">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-629">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-630">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-630">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-631">Ein externer Inhaltstyp in einem externen System.</span><span class="sxs-lookup"><span data-stu-id="dc651-631">An external content type in an external system.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-632">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-632">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-633">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-633">**Element**</span></span>|<span data-ttu-id="dc651-634">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-634">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-635">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-635">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-636">Ein externes System.</span><span class="sxs-lookup"><span data-stu-id="dc651-636">An external system.</span></span>  <br/> |
   

## <a name="entity-element"></a><span data-ttu-id="dc651-637">Entity (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-637">Entity element</span></span>
<span data-ttu-id="dc651-638"><a name="bkmk_Entity"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-638"></span></span>

<span data-ttu-id="dc651-639">Gibt einen externen Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="dc651-639">Specifies an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-640">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-640">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-641">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-641">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Entity Namespace = "String" Version = "String" EstimatedInstanceCount = "Integer" DefaultOperationMode = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Entity>
```

<span data-ttu-id="dc651-642">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-642">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-643">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-643">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-644">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-644">**Attribute**</span></span>|<span data-ttu-id="dc651-645">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-645">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-646">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="dc651-646">**Namespace**</span></span> <br/> |<span data-ttu-id="dc651-647">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-647">Required.</span></span>  <br/> <span data-ttu-id="dc651-648">Der Namespace, zu dem dieser externe Inhaltstyp gehört.</span><span class="sxs-lookup"><span data-stu-id="dc651-648">The namespace that this external content type belongs to.</span></span>  <br/> <span data-ttu-id="dc651-649">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-649">Attribute type: **String**</span></span> <br/> <span data-ttu-id="dc651-650">**Hinweis:** Der Namespace sollte nicht das Sonderzeichen Sternchen „**\***“ enthalten.</span><span class="sxs-lookup"><span data-stu-id="dc651-650">The namespace should not contain the asterisk special character " *****".</span></span>           |
|<span data-ttu-id="dc651-651">**Version**</span><span class="sxs-lookup"><span data-stu-id="dc651-651">**Version**</span></span> <br/> |<span data-ttu-id="dc651-652">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-652">Required.</span></span>  <br/> <span data-ttu-id="dc651-653">Die Versionsnummer dieses externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-653">The version number of this external content type.</span></span>  <br/> <span data-ttu-id="dc651-654">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-654">Attribute type: **String**</span></span> <br/> <span data-ttu-id="dc651-655">**Vorsicht:** Wenn sich das BDC-Modell ändert, müssen Sie die Versionsnummer des externen Inhaltstyps erhöhen.</span><span class="sxs-lookup"><span data-stu-id="dc651-655">**Caution:** When the BDC model changes, you must increase the version number of the external content type.</span></span> <span data-ttu-id="dc651-656">Wenn sich die Struktur eines externen Inhaltstyps ändert, sollten Sie die Hauptversionsnummer erhöhen.</span><span class="sxs-lookup"><span data-stu-id="dc651-656">If the structure of an external content type changes, you should increase the major number.</span></span> <span data-ttu-id="dc651-657">Zu Beispielen für strukturelle Änderungen gehört das Hinzufügen eines Felds zu einem **SpecificFinder** oder das Ändern eines Bezeichnerfelds.</span><span class="sxs-lookup"><span data-stu-id="dc651-657">Examples of structural changes include adding a field to a **SpecificFinder** or changing an identifier field.</span></span> <span data-ttu-id="dc651-658">Wenn die Änderung keine Auswirkungen auf die Struktur des externen Inhaltstyps hat, wenn beispielsweise eine Creator-Methode hinzugefügt wird, wenn Verbindungsinformationen geändert werden oder wenn Namen von  **LobSystems** und Typdeskriptoren geändert werden, sollten Sie die Buildnummer und die Revisionsnummer ändern.</span><span class="sxs-lookup"><span data-stu-id="dc651-658">When the BDC model changes, you must increase the version number of the external content type. If the structure of an external content type changes, you should increase the major number. Examples of structural changes include adding a field to a SpecificFinder or changing an identifier field. If the change does not affect the structure of the external content type, for example, when adding a creator method, changing connection information, or when changing names of **LobSystems** and type descriptors, you should change the build number and revision number.</span></span>          |
|<span data-ttu-id="dc651-659">**EstimatedInstanceCount**</span><span class="sxs-lookup"><span data-stu-id="dc651-659">**EstimatedInstanceCount**</span></span> <br/> |<span data-ttu-id="dc651-660">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-660">Optional.</span></span>  <br/> <span data-ttu-id="dc651-661">Die geschätzte Anzahl der im externen System enthaltenen externen Elemente.</span><span class="sxs-lookup"><span data-stu-id="dc651-661">The estimated number of external items contained by the external system.</span></span>  <br/> <span data-ttu-id="dc651-662">Standardwert: 10000</span><span class="sxs-lookup"><span data-stu-id="dc651-662">Default value: 10000</span></span>  <br/> <span data-ttu-id="dc651-663">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-663">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="dc651-664">**DefaultOperationMode**</span><span class="sxs-lookup"><span data-stu-id="dc651-664">**DefaultOperationMode**</span></span> <br/> |<span data-ttu-id="dc651-665">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-665">Optional.</span></span>  <br/> <span data-ttu-id="dc651-666">Gibt das Standardverhalten bei Interaktionen mit dem externen System beim Erstellen, Löschen, Aktualisieren oder Lesen externer Elemente an.</span><span class="sxs-lookup"><span data-stu-id="dc651-666">Specifies the default behavior when interacting with the external system while creating, deleting, updating, or reading external items.</span></span>  <br/> <span data-ttu-id="dc651-667">Standardwert: Default</span><span class="sxs-lookup"><span data-stu-id="dc651-667">Default value: Default</span></span>  <br/> <span data-ttu-id="dc651-668">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-668">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-669">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-669">Value</span></span></p></th><th><p><span data-ttu-id="dc651-670">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-670">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-671">Online</span><span class="sxs-lookup"><span data-stu-id="dc651-671">Online</span></span></p></td><td><p><span data-ttu-id="dc651-672">Zwischengespeicherte Elemente für alle Vorgänge umgehen und direkt mit dem externen System interagieren.</span><span class="sxs-lookup"><span data-stu-id="dc651-672">Bypass the cached external items for all operations and interact with the external system directly.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-673">Cached</span><span class="sxs-lookup"><span data-stu-id="dc651-673">Cached</span></span></p></td><td><p><span data-ttu-id="dc651-p121"><b>Create</b> -, <b>Read</b> -, <b>Update</b> - und <b>Delete</b> -Vorgänge direkt für die zwischengespeicherten externen Elemente ausführen. Bei <b>Read</b> -Vorgängen, wenn die angeforderten externen Elemente im Cache verfügbar sind, die externen Elemente im Cache verwenden. Anderenfalls den Cache umgehen, um die externen Elemente aus dem externen System abzurufen, und die externen Elemente zur späteren Verwendung im Cache ablegen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p121">Perform <b>Create</b>, <b>Read</b>, <b>Update</b>, and <b>Delete</b> operations directly against the cached external items. For <b>Read</b> operations, if the requested external items are available in the cache, use the external items in the cache. Otherwise, bypass the cache to obtain the external items from the external system, and put it in the cache for later use.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-677">Offline</span><span class="sxs-lookup"><span data-stu-id="dc651-677">Offline</span></span></p></td><td><p><span data-ttu-id="dc651-678"><b>Create</b> -, <b>Read</b> -, <b>Update</b> - und <b>Delete</b> -Vorgänge nur für die zwischengespeicherten externen Elemente ausführen.</span><span class="sxs-lookup"><span data-stu-id="dc651-678">Perform <b>Create</b>, <b>Read</b>, <b>Update</b>, and <b>Delete</b> operations against only the cached external items.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-679">Standard</span><span class="sxs-lookup"><span data-stu-id="dc651-679">Default</span></span></p></td><td><p><span data-ttu-id="dc651-p122">Standardverhalten des Systems verwenden. Dabei wird der Cache-Modus verwendet, wenn die Zwischenspeicherung externer Elemente von der Umgebung unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-p122">Use the System default behavior. This uses Cached mode if the environment supports caching external items.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="dc651-682">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-682">Name</span></span>  <br/> |<span data-ttu-id="dc651-683">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-683">Required.</span></span>  <br/> <span data-ttu-id="dc651-684">Der Name des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-684">The name of the external content type.</span></span>  <br/> <span data-ttu-id="dc651-685">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-685">Attribute type: **String**</span></span> <br/> <span data-ttu-id="dc651-686">**Hinweis:** Der Name eines externen Inhaltstyps sollte nicht das Sonderzeichen „**\***“ (Sternchen) enthalten.          | |DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-686">The name of an external content type should not contain the asterisk special character " *****".           | |DefaultDisplayName</span></span>           |
|<span data-ttu-id="dc651-687">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-687">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-688">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-688">Optional.</span></span>  <br/> <span data-ttu-id="dc651-689">Der Standardanzeigename des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-689">The default display name of the external content type.</span></span>  <br/> <span data-ttu-id="dc651-690">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-690">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-691">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-691">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-692">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-692">Optional.</span></span>  <br/> <span data-ttu-id="dc651-693">Gibt an, ob dieser externe Inhaltstyp häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-693">Specifies whether this external content type will be frequently used. If set to true, ossbdc will cache this external content type in memory.</span></span> <span data-ttu-id="dc651-694">Wenn dies auf „true“ festgelegt wird, wird dieser externe Inhaltstyp vom Business Data Connectivity (BDC)-Dienst im Speicher zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="dc651-694">If set to true, Business Data Connectivity (BDC) service will cache this external content type in memory.</span></span>  <br/> <span data-ttu-id="dc651-695">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-695">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-696">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-696">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-697">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-697">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-698">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-698">**Element**</span></span>|<span data-ttu-id="dc651-699">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-699">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-700">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-700">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-701">Die lokalisierten Anzeigenamen dieses externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-701">The localized display names of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-702">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-702">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-703">Die Eigenschaften dieses externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-703">The properties of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-704">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-704">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-705">Die Zugriffssteuerungsliste (Access Control List, ACL) dieses externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-705">The access control list (ACL) of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-706">Identifiers-Element in Entity (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-706">Identifiers Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-707">Die Bezeichner des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-707">The identifiers of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-708">Methods-Element in Entity (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-708">Methods Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-709">Die Methoden des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-709">The methods of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-710">AssociationGroups-Element in "Entity" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-710">AssociationGroups Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-711">Die Zuordnungsgruppen des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-711">The association groups of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="dc651-712">Actions-Element in "Entity" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-712">Actions Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-713">Die Aktionen des externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-713">The actions of the external content type.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-714">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-714">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-715">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-715">**Element**</span></span>|<span data-ttu-id="dc651-716">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-716">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-717">"Entities"-Element in "LobSystem" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-717">Entities Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-718">Die Liste der externen Inhaltstypen in diesem externen System.</span><span class="sxs-lookup"><span data-stu-id="dc651-718">The list of external content types in this external system.</span></span>  <br/> |
   

## <a name="filterdescriptor-element"></a><span data-ttu-id="dc651-719">"FilterDescriptor"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-719">FilterDescriptor element</span></span>
<span data-ttu-id="dc651-720"><a name="bkmk_FilterDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-720"></span></span>

<span data-ttu-id="dc651-721">Gibt einen Filterdeskriptor einer Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-721">Specifies a filter descriptor of a method.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-722">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-722">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-723">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-723">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<FilterDescriptor Type = "String" FilterField = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </FilterDescriptor>
```

<span data-ttu-id="dc651-724">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-724">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-725">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-725">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-726">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-726">**Attribute**</span></span>|<span data-ttu-id="dc651-727">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-727">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-728">Typ</span><span class="sxs-lookup"><span data-stu-id="dc651-728">Type</span></span>  <br/> |<span data-ttu-id="dc651-729">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-729">Required.</span></span>  <br/> <span data-ttu-id="dc651-730">Der Typ des Filterdeskriptors.</span><span class="sxs-lookup"><span data-stu-id="dc651-730">The type of the filter descriptor.</span></span>  <br/> <span data-ttu-id="dc651-731">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-731">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-732">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-732">Value</span></span></p></th><th><p><span data-ttu-id="dc651-733">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-733">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-734">Limit</span><span class="sxs-lookup"><span data-stu-id="dc651-734">Limit</span></span></p></td><td><p><span data-ttu-id="dc651-735">Wird beim Durchführen einer Abfrage in einem externen System verwendet, wenn der Attributwert als Höchstwert für die Anzahl der externen Elemente (**EntityInstances**), die beim Aufruf der Methode, zu der das Attribut gehört, zurückgegeben werden, interpretiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc651-735">Used while querying an external system and the value of which can be interpreted as a limit on the number of external items (**EntityInstances**) that are returned when the method that it belongs to is called.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-736">PageNumber</span><span class="sxs-lookup"><span data-stu-id="dc651-736">PageNumber</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="dc651-737">Platzhalter</span><span class="sxs-lookup"><span data-stu-id="dc651-737">Wildcard</span></span></p></td><td><p><span data-ttu-id="dc651-p124">Beim Abfragen von einem externen System verwendet. Der Wert stellt ein Muster der reguläre und Platzhalterzeichen, das den Wert eines bestimmten Felds des Satzes von **EntityInstances**verglichen wird. Das externe System gibt nur die **EntityInstances**, deren Feldwerte mit dem angegebene Muster übereinstimmen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p124">Used while querying an external system. Its value represents a pattern of regular and wildcard characters that is matched against the value of a particular field of the set of **EntityInstances**. The external system returns only those **EntityInstances** whose field values match the specified pattern.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-741">UserContext</span><span class="sxs-lookup"><span data-stu-id="dc651-741">UserContext</span></span></p></td><td><p><span data-ttu-id="dc651-p125">Wird beim Durchführen einer Abfrage in einem externen System verwendet. Der Wert kann von jeder Clientanwendung automatisch auf die Identität des Benutzers festgelegt werden, der das externe System aufruft. Anhand dieses Werts kann das externe System die Autorisierung durchführen und anschließend die zurückgegebenen Ergebnisse filtern.</span><span class="sxs-lookup"><span data-stu-id="dc651-p125">Used while querying an external system. Its value can be set automatically by any client application to the identity of the user who is calling the external system. This value can then be used by the external system to authorize and then filter the results returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-745">UserCulture</span><span class="sxs-lookup"><span data-stu-id="dc651-745">UserCulture</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="dc651-746">Benutzername</span><span class="sxs-lookup"><span data-stu-id="dc651-746">Username</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="dc651-747">Kennwort</span><span class="sxs-lookup"><span data-stu-id="dc651-747">Password</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-748">LastId</span><span class="sxs-lookup"><span data-stu-id="dc651-748">LastId</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-749">SsoTicket</span><span class="sxs-lookup"><span data-stu-id="dc651-749">SsoTicket</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-750">UserProfile</span><span class="sxs-lookup"><span data-stu-id="dc651-750">UserProfile</span></span></p></td><td><p><span data-ttu-id="dc651-p126">Wird beim Durchführen einer Abfrage in einem externen System verwendet. Der Wert kann durch Analysieren des Profils des aktuellen Benutzers abgerufen werden. Anhand dieses Werts kann das externe System die zurückgegebenen Ergebnisse filtern.</span><span class="sxs-lookup"><span data-stu-id="dc651-p126">Used while querying an external system. Its value can be obtained by examining the current user's profile. The external system can use its value to filter the results returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-754">Comparison</span><span class="sxs-lookup"><span data-stu-id="dc651-754">Comparison</span></span></p></td><td><p><span data-ttu-id="dc651-p127">Wird beim Durchführen einer Abfrage in einem externen System verwendet. Ein externes System kann einen **ComparisonFilter**-Wert mit dem Wert eines bestimmten Felds einer Gruppe von **EntityInstances** vergleichen und nur die **EntityInstances** zurückgeben, bei denen das Feld den Vergleichstest besteht. </span><span class="sxs-lookup"><span data-stu-id="dc651-p127">Used while querying an external system. An external system can compare a **ComparisonFilter** value with the value of a particular field of a set of **EntityInstances** and only those **EntityInstances** where the field values pass the comparison test can be returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-757">Timestamp</span><span class="sxs-lookup"><span data-stu-id="dc651-757">Timestamp</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-758">Eingabe</span><span class="sxs-lookup"><span data-stu-id="dc651-758">Input</span></span></p></td><td><p><span data-ttu-id="dc651-p128">Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Der Wert eines **InputFilter**-Typs kann von einem externen System als zusätzliches Argument für den Vorgang verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-p128">Used while calling an operation in an external system. An external system can use the value of an **InputFilter** as additional arguments for the operation.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-761">Ausgabe</span><span class="sxs-lookup"><span data-stu-id="dc651-761">Output</span></span></p></td><td><p><span data-ttu-id="dc651-p129">Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Zusätzliche Ergebnisse eines Vorgangs, die von **ReturnTypeDescriptor** nicht erfasst werden können, lassen sich als ein Wert des **InputOutputFilter**-Typs abrufen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p129">Used while calling an operation in an external system. Additional results of an operation that cannot be captured by **ReturnTypeDescriptor** can be retrieved as a value of the **InputOutputFilter**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-764">InputOutput</span><span class="sxs-lookup"><span data-stu-id="dc651-764">InputOutput</span></span></p></td><td><p><span data-ttu-id="dc651-p130">Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Der Wert eines **InputOutputFilter**-Typs kann von einem externen System als zusätzliches Argument für den Vorgang verwendet werden, und zusätzliche Ergebnisse eines Vorgangs, die von **ReturnTypeDescriptor** nicht erfasst werden können, lassen sich als ein Wert des **InputOutputFilter**-Typs abrufen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p130">Used while calling an operation in an external system. An external system can use the value of an **InputOutputFilter** as additional arguments for the operation, and additional results of an operation that cannot be captured by **ReturnTypeDescriptor** can be retrieved as a value of the **InputOutputFilter**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-767">Batchverarbeitung</span><span class="sxs-lookup"><span data-stu-id="dc651-767">Batching</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-768">BatchingTermination</span><span class="sxs-lookup"><span data-stu-id="dc651-768">BatchingTermination</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="dc651-769">ActivityId</span><span class="sxs-lookup"><span data-stu-id="dc651-769">ActivityId</span></span></p></td><td><p><span data-ttu-id="dc651-p131">**ActivityId** wird beim Aufrufen eines Vorgangs im externen System verwendet. Der Wert ist eine GUID, die den aktuellen Vorgangskontext darstellt. Ist kein solcher Wert vorhanden, generiert dieser Filter eine Zufalls-GUID. In SharePoint Foundation 2010 wird für diesen Filter die **CorrelationID** verwendet. </span><span class="sxs-lookup"><span data-stu-id="dc651-p131">**ActivityId** is used when calling an operation on the external system. Its value is set to a GUID that represents the current operation context. If no such value is available, this filter generates a random GUID. On SharePoint Foundation 2010, this filter uses the **CorrelationID**.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="dc651-774">FilterField</span><span class="sxs-lookup"><span data-stu-id="dc651-774">FilterField</span></span>  <br/> |<span data-ttu-id="dc651-775">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-775">Optional.</span></span>  <br/> <span data-ttu-id="dc651-776">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-776">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-777">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-777">Name</span></span>  <br/> |<span data-ttu-id="dc651-778">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-778">Required.</span></span>  <br/> <span data-ttu-id="dc651-779">Der Name des Filterdeskriptors.</span><span class="sxs-lookup"><span data-stu-id="dc651-779">The name of the filter descriptor.</span></span>  <br/> <span data-ttu-id="dc651-780">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-780">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-781">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-781">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-782">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-782">Optional.</span></span>  <br/> <span data-ttu-id="dc651-783">Der Standardanzeigename des Filterdeskriptors.</span><span class="sxs-lookup"><span data-stu-id="dc651-783">The default display name of the filter descriptor.</span></span>  <br/> <span data-ttu-id="dc651-784">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-784">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-785">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-785">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-786">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-786">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p132">Gibt an, ob dieser Filterdeskriptor häufig verwendet wird. Wenn dies auf **true** festgelegt wird, wird dieser Filterdeskriptor vom Business Data Connectivity (BDC)-Dienst im Arbeitsspeicher zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="dc651-p132">Specifies whether this filter descriptor is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches this filter descriptor in memory.  </span></span><br/> <span data-ttu-id="dc651-789">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-789">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-790">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-790">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-791">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-791">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-792">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-792">**Element**</span></span>|<span data-ttu-id="dc651-793">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-793">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-794">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-794">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-795">Die lokalisierten Anzeigenamen dieses Filterdeskriptors.</span><span class="sxs-lookup"><span data-stu-id="dc651-795">The localized display names of this filter descriptor.</span></span>  <br/> |
| [<span data-ttu-id="dc651-796">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-796">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-797">Die Eigenschaften dieses Filterdeskriptors.</span><span class="sxs-lookup"><span data-stu-id="dc651-797">The properties of this filter descriptor.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-798">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-798">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-799">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-799">**Element**</span></span>|<span data-ttu-id="dc651-800">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-800">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-801">FilterDescriptors-Element in Method (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-801">FilterDescriptors Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-802">Eine Liste der Filterdeskriptoren einer Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-802">A list of filter descriptors of a method.</span></span>  <br/> |
   

## <a name="filterdescriptors-element"></a><span data-ttu-id="dc651-803">FilterDescriptors-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-803">FilterDescriptors element</span></span>
<span data-ttu-id="dc651-804"><a name="bkmk_FilterDescriptors"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-804"></span></span>

<span data-ttu-id="dc651-805">Gibt eine Liste mit Filterdeskriptoren einer Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-805">Specifies a list of filter descriptors of a method.</span></span>
  
    
    
 <span data-ttu-id="dc651-806">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-806">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-807">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-807">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<FilterDescriptors></FilterDescriptors>
```

<span data-ttu-id="dc651-808">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-808">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-809">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-809">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-810">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-810">None</span></span>
  
    
    
 <span data-ttu-id="dc651-811">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-811">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-812">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-812">**Element**</span></span>|<span data-ttu-id="dc651-813">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-813">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-814">"FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-814">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-815">Ein Filterdeskriptor.</span><span class="sxs-lookup"><span data-stu-id="dc651-815">A filter descriptor.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-816">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-816">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-817">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-817">**Element**</span></span>|<span data-ttu-id="dc651-818">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-818">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-819">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-819">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-820">Die Methode, zu der diese Liste mit Filterdeskriptoren gehört.</span><span class="sxs-lookup"><span data-stu-id="dc651-820">The method this list of filter descriptors belongs to.</span></span>  <br/> |
   

## <a name="identifier-element"></a><span data-ttu-id="dc651-821">"Identifier"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-821">Identifier element</span></span>
<span data-ttu-id="dc651-822"><a name="bkmk_Identifier"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-822"></span></span>

<span data-ttu-id="dc651-823">Gibt einen Bezeichner eines externen Inhaltstyps an.</span><span class="sxs-lookup"><span data-stu-id="dc651-823">Specifies an identifier of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-824">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-824">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-825">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-825">**Schema:** BDCMetadata</span></span>
  
    
    

> <span data-ttu-id="dc651-826">**Hinweis:** Der Business Data Connectivity (BDC)-Dienst ermöglicht die Zuordnung der Bezeichner zu Feldern mit Datentypen, die Nullwerte zulassen.</span><span class="sxs-lookup"><span data-stu-id="dc651-826">**Note** Business Data Connectivity (BDC) service enables the mapping of identifiers to fields with nullable data types. However, for primary identifiers, BDC will cause an error when the value of these identifiers are null.</span></span> <span data-ttu-id="dc651-827">Für primäre Bezeichner verursacht BDC jedoch einen Fehler, wenn der Wert dieser Bezeichner **null** ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-827">Note Business Data Connectivity (BDC) service enables the mapping of identifiers to fields with nullable data types. However, for primary identifiers, BDC will cause an error when the value of these identifiers are **null**.</span></span> 
  
    
    




```XML
<Identifier TypeName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Identifier>
```

<span data-ttu-id="dc651-828">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-828">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-829">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-829">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-830">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-830">**Attribute**</span></span>|<span data-ttu-id="dc651-831">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-831">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-832">TypeName</span><span class="sxs-lookup"><span data-stu-id="dc651-832">TypeName</span></span>  <br/> |<span data-ttu-id="dc651-833">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-833">Required.</span></span>  <br/> <span data-ttu-id="dc651-834">Der Datentyp des Werts, der dem Bezeichner entspricht.</span><span class="sxs-lookup"><span data-stu-id="dc651-834">The data type of the value that corresponds to the identifier.</span></span>  <br/> <span data-ttu-id="dc651-835">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-835">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-836">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-836">Value</span></span></p></th><th><p><span data-ttu-id="dc651-837">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-837">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-838">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="dc651-838">System.Boolean</span></span></p></td><td><p><span data-ttu-id="dc651-839">Ein Bit.</span><span class="sxs-lookup"><span data-stu-id="dc651-839">A bit.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-840">System.Byte</span><span class="sxs-lookup"><span data-stu-id="dc651-840">System.Byte</span></span></p></td><td><p><span data-ttu-id="dc651-841">Eine Zahl zwischen 0 und 255 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-841">A number ranging from 0 to 255 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-842">System.Char</span><span class="sxs-lookup"><span data-stu-id="dc651-842">System.Char</span></span></p></td><td><p><span data-ttu-id="dc651-843">Ein Unicode-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="dc651-843">A Unicode character.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-844">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="dc651-844">System.DateTime</span></span></p></td><td><p><span data-ttu-id="dc651-p134">Ein Datum und eine Uhrzeit zwischen 12:00:00 Mitternacht, 1. Januar 1 Anno Domini (Christliche Zeitrechnung) und inklusive 23:59:59, 31. Dezember 9999 Anno Domini (Christliche Zeitrechnung), in einer Auflösung von 100 Nanosekunden.</span><span class="sxs-lookup"><span data-stu-id="dc651-p134">A date and time ranging from 12:00:00 midnight, January 1, 1 Anno Domini (Common Era) to 11:59:59 P.M. December 31, 9999 Anno Domini (Common Era) inclusive, in resolution of 100 nanoseconds.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-847">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="dc651-847">System.Decimal</span></span></p></td><td><p><span data-ttu-id="dc651-848">Eine Zahl von -79.228.162.514.264.337.593.543.950.335 bis +79.228.162.514.264.337.593.543.950.335 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-848">A number ranging from negative 79,228,162,514,264,337,593,543,950,335 to positive 79,228,162,514,264,337,593,543,950,335 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-849">System.Double</span><span class="sxs-lookup"><span data-stu-id="dc651-849">System.Double</span></span></p></td><td><p><span data-ttu-id="dc651-850">Eine Zahl mit doppelter Genauigkeit zwischen -1,79769313486232e308 und +1,79769313486232e308 inklusive sowie positive Null, negative Null, positiv unendlich, negativ unendlich und NaN (not-a-number).</span><span class="sxs-lookup"><span data-stu-id="dc651-850">A double precision number ranging from negative 1.79769313486232e308 to positive 1.79769313486232e308 inclusive, and positive zero, negative zero, positive infinity, negative infinity, and not-a-number (NaN).</span></span> </p></td></tr><tr><td><p><span data-ttu-id="dc651-851">System.Guid</span><span class="sxs-lookup"><span data-stu-id="dc651-851">System.Guid</span></span></p></td><td><p><span data-ttu-id="dc651-852">Eine GUID.</span><span class="sxs-lookup"><span data-stu-id="dc651-852">A GUID.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-853">System.Int16</span><span class="sxs-lookup"><span data-stu-id="dc651-853">System.Int16</span></span></p></td><td><p><span data-ttu-id="dc651-854">Eine Zahl zwischen -32.768 und +32.768 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-854">A number ranging from negative 32768 to positive 32767 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-855">System.Int32</span><span class="sxs-lookup"><span data-stu-id="dc651-855">System.Int32</span></span></p></td><td><p><span data-ttu-id="dc651-856">Eine Zahl zwischen 0 und 4.294.967.295 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-856">A number ranging from 0 to 4,294,967,295 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-857">System.Int64</span><span class="sxs-lookup"><span data-stu-id="dc651-857">System.Int64</span></span></p></td><td><p><span data-ttu-id="dc651-858">Eine Zahl zwischen 0 und 18.446.744.073.709.551.615 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-858">A number ranging from 0 to 18,446,744,073,709,551,615 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-859">System.SByte</span><span class="sxs-lookup"><span data-stu-id="dc651-859">System.SByte</span></span></p></td><td><p><span data-ttu-id="dc651-860">Eine Zahl zwischen -128 und +127 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-860">A number ranging from negative 128 to positive 127 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-861">System.Single</span><span class="sxs-lookup"><span data-stu-id="dc651-861">System.Single</span></span></p></td><td><p><span data-ttu-id="dc651-862">Eine Zahl mit einfacher Genauigkeit zwischen -3,402823e38 und +3,402823e38 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-862">A single precision number ranging from negative 3.402823e38 to positive 3.402823e38 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-863">System.String</span><span class="sxs-lookup"><span data-stu-id="dc651-863">System.String</span></span></p></td><td><p><span data-ttu-id="dc651-864">Eine Zeichenfolge mit Unicode-Text.</span><span class="sxs-lookup"><span data-stu-id="dc651-864">A string of Unicode text.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-865">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="dc651-865">System.TimeSpan</span></span></p></td><td><p><span data-ttu-id="dc651-866">Eine Dauer zwischen -10.675.199 Tagen 2 Stunden 48 Minuten 5 Sekunden 477 Millisekunden 580 Mikrosekunden 800 Nanosekunden und +10.675.199 Tagen 2 Stunden 48 Minuten 5 Sekunden 477 Millisekunden 580 Mikrosekunden 800 Nanosekunden inklusive, in einer Auflösung von 100 Nanosekunden.</span><span class="sxs-lookup"><span data-stu-id="dc651-866">A duration ranging from negative 10675199 days 2 hours 48 minutes 5 seconds 477 milliseconds 580 microseconds 800 nanoseconds to positive 10675199 days 2 hours 48 minutes 5 seconds 477 milliseconds 580 microseconds 800 nanoseconds inclusive, in resolution of 100 nanoseconds.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-867">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="dc651-867">System.UInt16</span></span></p></td><td><p><span data-ttu-id="dc651-868">Eine Zahl zwischen 0 und 65.535 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-868">A number ranging from 0 to 65535 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-869">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="dc651-869">System.UInt32</span></span></p></td><td><p><span data-ttu-id="dc651-870">Eine Zahl zwischen 0 und 4.294.967.295 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-870">A number ranging from 0 to 4,294,967,295 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-871">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="dc651-871">System.UInt64</span></span></p></td><td><p><span data-ttu-id="dc651-872">Eine Zahl zwischen 0 und 18.446.744.709.551.615 inklusive.</span><span class="sxs-lookup"><span data-stu-id="dc651-872">A number ranging from 0 to 18,446,744,709,551,615 inclusive.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="dc651-873">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-873">Name</span></span>  <br/> |<span data-ttu-id="dc651-874">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-874">Required.</span></span>  <br/> <span data-ttu-id="dc651-875">Der Name des Bezeichners.</span><span class="sxs-lookup"><span data-stu-id="dc651-875">The name of the identifier.</span></span>  <br/> <span data-ttu-id="dc651-876">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-876">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-877">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-877">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-878">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-878">Optional.</span></span>  <br/> <span data-ttu-id="dc651-879">Der Standardanzeigename des Bezeichners.</span><span class="sxs-lookup"><span data-stu-id="dc651-879">The default display name of the identifier.</span></span>  <br/> <span data-ttu-id="dc651-880">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-880">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-881">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-881">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-882">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-882">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p135">Gibt an, ob dieser Bezeichner häufig verwendet wird. Wenn dies auf **true** festgelegt wird, wird dieser Bezeichner vom Business Data Connectivity (BDC)-Dienst im Arbeitsspeicher zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="dc651-p135">Specifies whether this identifier is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches the identifier in memory.  </span></span><br/> <span data-ttu-id="dc651-885">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-885">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-886">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-886">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-887">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-887">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-888">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-888">**Element**</span></span>|<span data-ttu-id="dc651-889">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-889">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-890">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-890">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-891">Die lokalisierten Anzeigenamen des Bezeichners.</span><span class="sxs-lookup"><span data-stu-id="dc651-891">The localized display names of the identifier.</span></span>  <br/> |
| [<span data-ttu-id="dc651-892">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-892">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-893">Die Eigenschaften des Bezeichners.</span><span class="sxs-lookup"><span data-stu-id="dc651-893">The properties of the identifier.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-894">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-894">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-895">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-895">**Element**</span></span>|<span data-ttu-id="dc651-896">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-896">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-897">Identifiers-Element in Entity (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-897">Identifiers Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-898">Eine Liste der Bezeichner eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-898">A list of identifiers of an external content type.</span></span>  <br/> |
   

## <a name="identifiers-element"></a><span data-ttu-id="dc651-899">Identifiers-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-899">Identifiers element</span></span>
<span data-ttu-id="dc651-900"><a name="bkmk_Identifiers"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-900"></span></span>

<span data-ttu-id="dc651-901">Gibt eine Liste mit Bezeichnern eines externen Inhaltstyps an.</span><span class="sxs-lookup"><span data-stu-id="dc651-901">Specifies a list of identifiers of an external content type.</span></span>
  
    
    
 <span data-ttu-id="dc651-902">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-902">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-903">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-903">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Identifiers></Identifiers>
```

<span data-ttu-id="dc651-904">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-904">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-905">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-905">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-906">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-906">None</span></span>
  
    
    
 <span data-ttu-id="dc651-907">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-907">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-908">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-908">**Element**</span></span>|<span data-ttu-id="dc651-909">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-909">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-910">Identifier-Element in "Identifiers" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-910">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-911">Gibt einen Bezeichner an.</span><span class="sxs-lookup"><span data-stu-id="dc651-911">Specifies an identifier.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-912">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-912">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-913">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-913">**Element**</span></span>|<span data-ttu-id="dc651-914">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-914">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-915">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-915">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-916">Der externe Inhaltstyp, der diese Liste mit Bezeichnern enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-916">The external content type that contains this list of identifiers.</span></span>  <br/> |
   

## <a name="interpretation-element"></a><span data-ttu-id="dc651-917">Interpretation-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-917">Interpretation element</span></span>
<span data-ttu-id="dc651-918"><a name="bkmk_Interpretation"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-918"></span></span>

<span data-ttu-id="dc651-919">Gibt die Regeln an, die auf die in den Datenstrukturen gespeicherten Daten, dargestellt durch **TypeDescriptor**, angewendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="dc651-919">An Interpretation element that specifies the rules to apply to the data that is stored in the data structures represented by a **TypeDescriptor**.</span></span> <span data-ttu-id="dc651-920">Diese Regeln werden in der Regel angegeben, um die Datenwerte zu ändern, die von einem externen System zurückgegeben werden, damit diese in der Benutzeroberfläche leichter dargestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="dc651-920">These rules are typically specified to change the data values returned by an external system to make it easier to represent them in the user interface.</span></span> <span data-ttu-id="dc651-921">Wenn der Datenwert aus dem externen System abgerufen wird, müssen die angegebenen Regeln in der Reihenfolge angewendet werden, in der Sie im **Interpretation**-Element angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="dc651-921">When the data value is obtained from the external system, the specified rules must be applied in the order they are specified in the **Interpretation** element.</span></span> <span data-ttu-id="dc651-922">Die erste Regel muss auf den vom externen System empfangenen Datenwert angewendet werden; die nachfolgenden Regeln werden auf den Datenwert angewendet, der aus der Anwendung der vorherigen Regel resultiert.</span><span class="sxs-lookup"><span data-stu-id="dc651-922">The first rule must be applied to the data value received from the external system; the consecutive rules apply to the data value that result from the application of the previous rule.</span></span> <span data-ttu-id="dc651-923">Wenn der Datenwert an das externe System gesendet wird, müssen die angegebenen Regeln in der umgekehrten Reihenfolge angewendet werden, in der Sie im **Interpretation**-Element angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="dc651-923">When the data value is sent to external system, the specified rules must be applied in the reverse order they are specified in the **Interpretation** element.</span></span> <span data-ttu-id="dc651-924">Die erste Regel muss auf den vom Benutzer empfangenen Datenwert angewendet werden; die nachfolgenden Regeln werden auf den Datenwert angewendet, der aus der Anwendung der vorherigen Regel resultiert.</span><span class="sxs-lookup"><span data-stu-id="dc651-924">The first rule must be applied to the data value received from the user; the consecutive rules apply to the data value that result from the application of the previous rule.</span></span>
  
    
    
 <span data-ttu-id="dc651-925">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-925">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-926">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-926">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Interpretation></Interpretation>
```

<span data-ttu-id="dc651-927">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-927">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-928">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-928">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-929">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-929">None</span></span>
  
    
    
 <span data-ttu-id="dc651-930">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-930">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-931">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-931">**Element**</span></span>|<span data-ttu-id="dc651-932">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-932">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-933">ConvertType-Element in "Interpretation" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-933">ConvertType Element in Interpretation (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c474cf2c-b631-f3c9-daf1-f05d3e0d385f%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-934">Ein **ConvertType**-Element, das die Konvertierung eines Datentyps in einen anderen Datentyp angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-934">A **ConvertType** element that specifies the conversion of a data type to another data type.</span></span> <br/> |
| [<span data-ttu-id="dc651-935">NormalizeDateTime-Element in "Interpretation" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-935">NormalizeDateTime Element in Interpretation (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/bbae3bfa-0754-d576-2bee-1ac0e8508a57%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-936">Ein **NormalizeDateTime**-Element, das die Konvertierung der Datums- und Zeitdarstellung eines von einem externen System erhaltenen Werts in eine andere Darstellung angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-936">A **NormalizeDateTime** element that specifies the conversion of the date and time representation of a value obtained from an external system into another representation.</span></span> <br/> |
|<span data-ttu-id="dc651-937">NormalizeString</span><span class="sxs-lookup"><span data-stu-id="dc651-937">NormalizeString</span></span>  <br/> |<span data-ttu-id="dc651-938">Ein **NormalizeString**-Element, das die Konvertierung der Zeichenfolgendarstellung eines von einem externen System erhaltenen Werts in eine andere Darstellung angibt.</span><span class="sxs-lookup"><span data-stu-id="dc651-938">A **NormalizeString** element that specifies the conversion of the string representation of a value obtained from an external system into another representation.</span></span> <br/> |
   
 <span data-ttu-id="dc651-939">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-939">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-940">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-940">**Element**</span></span>|<span data-ttu-id="dc651-941">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-941">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-942">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-942">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-943">Das **TypeDescriptor**-Element.</span><span class="sxs-lookup"><span data-stu-id="dc651-943">The **TypeDescriptor** element.</span></span> <br/> |
   

## <a name="lobsystem-element"></a><span data-ttu-id="dc651-944">"LobSystem"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-944">LobSystem element</span></span>
<span data-ttu-id="dc651-945"><a name="bkmk_LobSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-945"></span></span>

<span data-ttu-id="dc651-946">Stellt eine externe Datenquelle dar.</span><span class="sxs-lookup"><span data-stu-id="dc651-946">Represents an external data source.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-947">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-947">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-948">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-948">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystem Type = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystem>
```

<span data-ttu-id="dc651-949">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-949">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-950">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-950">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-951">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-951">**Attribute**</span></span>|<span data-ttu-id="dc651-952">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-952">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-953">Typ</span><span class="sxs-lookup"><span data-stu-id="dc651-953">Type</span></span>  <br/> |<span data-ttu-id="dc651-954">Der Typ des der **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="dc651-954">The type of the **LobSystem**.</span></span>  <br/> <span data-ttu-id="dc651-955">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-955">Required.</span></span>  <br/> <span data-ttu-id="dc651-956">Die folgende Tabelle listet die möglichen Werte für dieses Attribut auf.</span><span class="sxs-lookup"><span data-stu-id="dc651-956">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-957">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-957">Value</span></span></p></th><th><p><span data-ttu-id="dc651-958">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-958">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-959">Datenbank</span><span class="sxs-lookup"><span data-stu-id="dc651-959">Database</span></span></p></td><td><p><span data-ttu-id="dc651-960">Die dargestellte externe Datenquelle ist eine Datenbank.</span><span class="sxs-lookup"><span data-stu-id="dc651-960">The represented external data source is a database.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-961">DotNetAssembly</span><span class="sxs-lookup"><span data-stu-id="dc651-961">DotNetAssembly</span></span></p></td><td><p><span data-ttu-id="dc651-962">Die dargestellte externe Datenquelle ist ein Satz von .NET Framework-Klassen.</span><span class="sxs-lookup"><span data-stu-id="dc651-962">The represented external data source is a set of .NET Framework classes.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-963">Wcf</span><span class="sxs-lookup"><span data-stu-id="dc651-963">Wcf</span></span></p></td><td><p><span data-ttu-id="dc651-964">Die dargestellte externe Datenquelle ist ein WCF-Dienst-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="dc651-964">The represented external data source is a WCF Service endpoint.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-965">WebService</span><span class="sxs-lookup"><span data-stu-id="dc651-965">WebService</span></span></p></td><td><p><span data-ttu-id="dc651-966">Die dargestellte externe Datenquelle ist ein Webdienst.</span><span class="sxs-lookup"><span data-stu-id="dc651-966">The represented external data source is a Web service. This has been deprecated, use Wcf instead.</span></span> <span data-ttu-id="dc651-967">Dies ist veraltet, verwenden Sie stattdessen WCF.</span><span class="sxs-lookup"><span data-stu-id="dc651-967">This has been deprecated, use WCF instead.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-968">Benutzerdefiniert</span><span class="sxs-lookup"><span data-stu-id="dc651-968">Custom</span></span></p></td><td><p><span data-ttu-id="dc651-969">In der dargestellten externen Datenquelle ist ein benutzerdefinierter Konnektor implementiert, um die Verbindung und die Datenübertragung zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="dc651-969">The represented external data source has a custom connector implemented to manage the connection and data transfer.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="dc651-970">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-970">Name</span></span>  <br/> |<span data-ttu-id="dc651-971">Der Name des **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="dc651-971">The name of the LobSystem.</span></span>  <br/> <span data-ttu-id="dc651-972">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-972">Required.</span></span>  <br/> <span data-ttu-id="dc651-973">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-973">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-974">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-974">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-975">Der Standardanzeigename des **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="dc651-975">The default display name of the LobSystem.</span></span>  <br/> <span data-ttu-id="dc651-976">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-976">Optional.</span></span>  <br/> <span data-ttu-id="dc651-977">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-977">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-978">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-978">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-979">Gibt an, ob das **LobSystem** häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-979">Specifies whether the LobSystem is frequently used. If frequently used, ossbdc caches the LobSystem.</span></span> <span data-ttu-id="dc651-980">Wenn es häufig verwendet wird, wird das **LobSystem** vom Business Data Connectivity (BDC)-Dienst zwischengespeichert. </span><span class="sxs-lookup"><span data-stu-id="dc651-980">|Specifies whether the LobSystem is frequently used. If frequently used, Business Data Connectivity (BDC) service caches the **LobSystem**.</span></span>  <br/> <span data-ttu-id="dc651-981">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-981">Optional.</span></span>  <br/> <span data-ttu-id="dc651-982">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-982">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-983">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-983">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-984">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-984">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-985">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-985">**Element**</span></span>|<span data-ttu-id="dc651-986">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-986">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-987">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-987">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-988">Die lokalisierten Namen des **LobSystem**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-988">The localized names of the **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-989">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-989">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-990">Gibt die Eigenschaften eines **LobSystem** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-990">Specifies the properties of an **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-991">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-991">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-992">Gibt die Zugriffssteuerungsliste (Access Control List, ACL) eines **LobSystem** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-992">Specifies the access control list (ACL) of an **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-993">Proxy-Element in "LobSystem" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-993">Proxy Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ec2e7b0-156f-ff4a-a87b-fe5764e4875b%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-994">Gibt einen vom Benutzer bereitgestellten Proxy an, der identisch mit demjenigen ist, der generiert würde, wenn dieses Element nicht vorhanden wäre.</span><span class="sxs-lookup"><span data-stu-id="dc651-994">Specifies a user-provided proxy that is identical to the one that would be generated if this element was not present.</span></span>  <br/> |
| [<span data-ttu-id="dc651-995">LobSystemInstances-Element in "LobSystem" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-995">LobSystemInstances Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-996">Gibt die externen Systeminstanzen für dieses externe System an.</span><span class="sxs-lookup"><span data-stu-id="dc651-996">Specifies the external system instances for this external system.</span></span>  <br/> |
| [<span data-ttu-id="dc651-997">"Entities"-Element in "LobSystem" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-997">Entities Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-998">Gibt die externen Inhaltstypen in diesem externen System an.</span><span class="sxs-lookup"><span data-stu-id="dc651-998">Specifies the external content types in this external system.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-999">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-999">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1000">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1000">**Element**</span></span>|<span data-ttu-id="dc651-1001">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1001">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1002">"LobSystems"-Element im Modell ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1002">LobSystems Element in Model (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1003">Gibt eine Liste externer Systeme in diesem Modell an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1003">Specifies a list of external systems in this model.</span></span>  <br/> |
   

## <a name="lobsysteminstance-element"></a><span data-ttu-id="dc651-1004">LobSystemInstance-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1004">LobSystemInstance element</span></span>
<span data-ttu-id="dc651-1005"><a name="bkmk_LobSystemInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1005"></span></span>

<span data-ttu-id="dc651-1006">Gibt eine externe Systeminstanz an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1006">Specifies an external system instance.</span></span>
  
    
    
 <span data-ttu-id="dc651-1007">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1007">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1008">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1008">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystemInstance Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystemInstance>
```

<span data-ttu-id="dc651-1009">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1009">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1010">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1010">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1011">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1011">**Attribute**</span></span>|<span data-ttu-id="dc651-1012">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1012">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1013">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-1013">Name</span></span>  <br/> |<span data-ttu-id="dc651-1014">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1014">Required.</span></span>  <br/> <span data-ttu-id="dc651-1015">Der Name der externen Systeminstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1015">The name of the external system instance.</span></span>  <br/> <span data-ttu-id="dc651-1016">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1016">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1017">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-1017">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-1018">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1018">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1019">Der Standardanzeigename der externen Systeminstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1019">The default display name of the external system instance.</span></span>  <br/> <span data-ttu-id="dc651-1020">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1020">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1021">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-1021">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-1022">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1022">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p139">Gibt an, ob diese externe Systeminstanz häufig verwendet wird. Wenn **true** festgelegt ist, wird die externe Systeminstanz von Business Data Connectivity (BDC)-Dienst zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="dc651-p139">Specifies whether this external system instance is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches the external system instance.  </span></span><br/> <span data-ttu-id="dc651-1025">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1025">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1026">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1026">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1027">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1027">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1028">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1028">**Element**</span></span>|<span data-ttu-id="dc651-1029">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1029">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1030">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1030">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1031">Die lokalisierten Namen dieser externen Systeminstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1031">The localized names of this external system instance.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1032">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1032">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1033">Die Eigenschaften dieser externen Systeminstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1033">The properties of this external system instance.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1034">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1034">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1035">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1035">**Element**</span></span>|<span data-ttu-id="dc651-1036">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1036">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1037">LobSystemInstances-Element in "LobSystem" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1037">LobSystemInstances Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1038">Eine Liste von externen Systeminstanzen.</span><span class="sxs-lookup"><span data-stu-id="dc651-1038">A list of external system instances.</span></span>  <br/> |
   

## <a name="lobsysteminstances-element"></a><span data-ttu-id="dc651-1039">LobSystemInstances-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1039">LobSystemInstances element</span></span>
<span data-ttu-id="dc651-1040"><a name="bkmk_LobSystemInstances"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1040"></span></span>

<span data-ttu-id="dc651-1041">Gibt eine Liste externer Systeminstanzen an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1041">Specifies a list of external system instances.</span></span>
  
    
    
 <span data-ttu-id="dc651-1042">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1042">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1043">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1043">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystemInstances></LobSystemInstances>
```

<span data-ttu-id="dc651-1044">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1044">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1045">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1045">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1046">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1046">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1047">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1047">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1048">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1048">**Element**</span></span>|<span data-ttu-id="dc651-1049">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1049">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1050">LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1050">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1051">Eine externe Systeminstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1051">An external system instance.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1052">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1052">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1053">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1053">**Element**</span></span>|<span data-ttu-id="dc651-1054">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1054">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1055">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1055">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1056">Ein externes System.</span><span class="sxs-lookup"><span data-stu-id="dc651-1056">An external system.</span></span>  <br/> |
   

## <a name="lobsystems-element"></a><span data-ttu-id="dc651-1057">"LobSystems"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1057">LobSystems element</span></span>
<span data-ttu-id="dc651-1058"><a name="bkmk_LobSystems"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1058"></span></span>

<span data-ttu-id="dc651-1059">Gibt eine Liste von **LobSystem**-Elementen eines Modells an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1059">Specifies a list of **LobSystem** elements of a model.</span></span>
  
    
    
 <span data-ttu-id="dc651-1060">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1060">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1061">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1061">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystems></LobSystems>
```

<span data-ttu-id="dc651-1062">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1062">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1063">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1063">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1064">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1064">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1065">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1065">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1066">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1066">**Element**</span></span>|<span data-ttu-id="dc651-1067">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1067">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1068">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1068">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1069">Ein **LobSystem** -Element, das ein externes System festlegt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1069">A **LobSystem** element that specifies a external system.</span></span> <br/> |
   
 <span data-ttu-id="dc651-1070">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1070">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1071">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1071">**Element**</span></span>|<span data-ttu-id="dc651-1072">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1072">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1073">"Model"-Element ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1073">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1074">Eine Anwendungsdefinition (BDC-Modell)</span><span class="sxs-lookup"><span data-stu-id="dc651-1074">An application definition (BDC model).</span></span>  <br/> |
   

## <a name="localizeddisplayname-element"></a><span data-ttu-id="dc651-1075">"LocalizedDisplayName"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1075">LocalizedDisplayName element</span></span>
<span data-ttu-id="dc651-1076"><a name="bkmk_LocalizedDisplayName"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1076"></span></span>

<span data-ttu-id="dc651-1077">Gibt einen lokalisierten Namen an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1077">Specifies a localized name.</span></span>
  
    
    
 <span data-ttu-id="dc651-1078">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1078">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1079">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1079">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LocalizedDisplayName LCID = "Integer"> </LocalizedDisplayName>
```

<span data-ttu-id="dc651-1080">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1080">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1081">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1081">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1082">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1082">**Attribute**</span></span>|<span data-ttu-id="dc651-1083">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1083">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1084">LCID</span><span class="sxs-lookup"><span data-stu-id="dc651-1084">LCID</span></span>  <br/> |<span data-ttu-id="dc651-1085">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1085">Required.</span></span>  <br/> <span data-ttu-id="dc651-1086">Die Sprachcode-ID (Language Code Identifier, LCID).</span><span class="sxs-lookup"><span data-stu-id="dc651-1086">The language code identifier (LCID).</span></span>  <br/> <span data-ttu-id="dc651-1087">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-1087">Attribute type: **Integer**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1088">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1088">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1089">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1089">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1090">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1090">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1091">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1091">**Element**</span></span>|<span data-ttu-id="dc651-1092">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1092">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1093">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1093">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1094">Das **LocalizedDisplayNames**-Element, das diesen **LocalizedDisplayName**-Parameter enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1094">The **LocalizedDisplayNames** element that contains this **LocalizedDisplayName**.</span></span>  <br/> |
   

## <a name="localizeddisplaynames-element"></a><span data-ttu-id="dc651-1095">"LocalizedDisplayNames"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1095">LocalizedDisplayNames element</span></span>
<span data-ttu-id="dc651-1096"><a name="bkmk_LocalizedDisplayNames"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1096"></span></span>

<span data-ttu-id="dc651-1097">Gibt eine Liste lokalisierter Namen für ein **MetadataObject** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1097">Specifies a list of localized names of a **MetadataObject**.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-1098">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1098">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1099">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1099">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LocalizedDisplayNames></LocalizedDisplayNames>
```

<span data-ttu-id="dc651-1100">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1100">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1101">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1101">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1102">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1102">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1103">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1103">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1104">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1104">**Element**</span></span>|<span data-ttu-id="dc651-1105">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1105">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1106">LocalizedDisplayName-Element in LocalizedDisplayNames (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1106">LocalizedDisplayName Element in LocalizedDisplayNames (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/93fb80ef-6347-b463-da90-4980d872678e%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1107">Ein lokalisierter Name.</span><span class="sxs-lookup"><span data-stu-id="dc651-1107">A localized name.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1108">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1108">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1109">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1109">**Element**</span></span>|<span data-ttu-id="dc651-1110">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1110">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1111">"Model"-Element ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1111">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1112">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1112">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1113">LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1113">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1114">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1114">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1115">Identifier-Element in "Identifiers" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1115">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1116">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1116">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1117">"FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1117">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1118">Parameter-Element in "Parameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1118">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1119">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1119">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1120">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1120">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1121">MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1121">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1122">"AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1122">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1123">"Action"-Element in "Actions" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1123">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1124">ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1124">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="metadataobject-element"></a><span data-ttu-id="dc651-1125">"MetadataObject"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1125">MetadataObject element</span></span>
<span data-ttu-id="dc651-1126"><a name="bkmk_MetadataObject"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1126"></span></span>

 <span data-ttu-id="dc651-1127">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="dc651-1127">**Namespace:**</span></span>
  
    
    
 <span data-ttu-id="dc651-1128">**Schema:**</span><span class="sxs-lookup"><span data-stu-id="dc651-1128">**Schema:**</span></span>
  
    
    



```XML

```

<span data-ttu-id="dc651-1129">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1129">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1130">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1130">**Attributes**</span></span>
  
    
    
 <span data-ttu-id="dc651-1131">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1131">**Child elements**</span></span>
  
    
    
 <span data-ttu-id="dc651-1132">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1132">**Parent element**</span></span>
  
    
    

## <a name="method-element"></a><span data-ttu-id="dc651-1133">Method-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1133">Method element</span></span>
<span data-ttu-id="dc651-1134"><a name="bkmk_Method"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1134"></span></span>

<span data-ttu-id="dc651-1135">Gibt eine Methode eines externen Inhaltstyps an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1135">Specifies a method of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-1136">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1136">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1137">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1137">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Method IsStatic = "Boolean" LobName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Method>
```

<span data-ttu-id="dc651-1138">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1138">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1139">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1139">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1140">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1140">**Attribute**</span></span>|<span data-ttu-id="dc651-1141">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1141">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1142">IsStatic</span><span class="sxs-lookup"><span data-stu-id="dc651-1142">IsStatic</span></span>  <br/> |<span data-ttu-id="dc651-1143">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1143">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p140"> Gibt an, ob für die Ausführung dieser Methode ein externes Element ( **EntityInstance**) erforderlich ist, das als Ausführungskontext fungiert. Wird das Attribut auf **true** festgelegt, stellt die Methode eine statische Methode dar, für die kein bestimmtes **EntityInstance**-Element zur Bereitstellung eines Ausführungskontextes erforderlich ist. Wird das Attribut auf **false** festgelegt, stellt die Methode eine Instanzmethode dar und erfordert ein **EntityInstance**-Element, um den Kontext für die Ausführung bereitzustellen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p140">Specifies whether the execution of this method requires an external item ( **EntityInstance**) to serve as a context for execution. If set to **true**, the method represents a static method and does not require a specific **EntityInstance** to provide context for execution. If set to **false**, the method represents an instance method and requires an **EntityInstance** to provide the context for execution. </span></span><br/> <span data-ttu-id="dc651-1147">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1147">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1148">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1148">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1149">LobName</span><span class="sxs-lookup"><span data-stu-id="dc651-1149">LobName</span></span>  <br/> |<span data-ttu-id="dc651-1150">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1150">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1151">Der Name der im externen System definierten Operation, die von dieser Methode dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1151">The name of the operation defined in the external system that is represented by this method.</span></span>  <br/> <span data-ttu-id="dc651-1152">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1152">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1153">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-1153">Name</span></span>  <br/> |<span data-ttu-id="dc651-1154">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1154">Required.</span></span>  <br/> <span data-ttu-id="dc651-1155">Der Name dieser Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1155">The name of this method.</span></span>  <br/> <span data-ttu-id="dc651-1156">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1156">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1157">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-1157">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-1158">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1158">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1159">Der Standardanzeigename der Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1159">The default display name of the method.</span></span>  <br/> <span data-ttu-id="dc651-1160">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1160">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1161">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-1161">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-1162">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1162">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p141">Gibt an, ob diese Methode häufig verwendet wird. Wird das Attribut auf **true** festgelegt, speichert der Business Data Connectivity (BDC)-Dienst diese Methode im Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="dc651-p141">Specifies whether this method is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches this method in memory.  </span></span><br/> <span data-ttu-id="dc651-1165">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1165">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1166">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1166">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1167">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1167">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1168">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1168">**Element**</span></span>|<span data-ttu-id="dc651-1169">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1169">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1170">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1170">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1171">Die lokalisierten Anzeigenamen der Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1171">The localized display names of the method.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1172">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1172">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1173">Die Eigenschaften der Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1173">The properties of the method.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1174">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1174">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1175">Die Zugriffssteuerungsliste (Access Control List, ACL) dieser Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1175">The access control list (ACL) of this method.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1176">FilterDescriptors-Element in Method (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1176">FilterDescriptors Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1177">Die Filterdeskriptoren der Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1177">The filter descriptors of the method.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1178">Parameters-Element in "Method" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1178">Parameters Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-p142">Die Parameter der Methode. Eine Methode kann nicht mehr als einen Rückgabeparameter aufweisen.</span><span class="sxs-lookup"><span data-stu-id="dc651-p142">The parameters of the method. A method cannot have more than one return parameter.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1181">"MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1181">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1182">Die Methodeninstanzen der Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1182">The method instances of the method.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1183">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1183">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1184">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1184">**Element**</span></span>|<span data-ttu-id="dc651-1185">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1185">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1186">Methods-Element in Entity (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1186">Methods Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1187">Eine Liste der Methoden eines externen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="dc651-1187">A list of methods of an external content type.</span></span>  <br/> |
   

## <a name="methodinstance-element"></a><span data-ttu-id="dc651-1188">MethodInstance-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1188">MethodInstance element</span></span>
<span data-ttu-id="dc651-1189"><a name="bkmk_MethodInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1189"></span></span>

<span data-ttu-id="dc651-1190">Gibt ein **MethodInstance**-Element an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1190">Specifies a **MethodInstance**.</span></span>
  
    
    
 <span data-ttu-id="dc651-1191">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1191">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1192">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1192">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="dc651-1193">Die folgenden beiden Situationen in einem Modell BDC bewirken ein  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) zur Laufzeit:</span><span class="sxs-lookup"><span data-stu-id="dc651-1193">The following two cases in a BDC model result in an  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) at run time:</span></span>
  
    
    

- <span data-ttu-id="dc651-1194">Zwei **SpecificFinder**-Methodeninstanzen, von denen dieselben Felder zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1194">Two **SpecificFinder** method instances that return the same set of fields.</span></span>
    
  
- <span data-ttu-id="dc651-1195">Zwei **SpecificFinder**-Methodeninstanzen, die die gleiche Anzahl von Feldern aufweisen und die gleiche Anzahl von Feldern mit einer anderen Methodeninstanz gemeinsam verwenden, wie z. B. die **Finder**-Methode.</span><span class="sxs-lookup"><span data-stu-id="dc651-1195">Two **SpecificFinder** method instances that have the same number of fields and that share the same number of fields with another method instance, such as a **Finder**.</span></span>
    
  



```XML
<MethodInstance Type = "Strig" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </MethodInstance>
```

<span data-ttu-id="dc651-1196">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1196">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1197">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1197">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1198">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1198">**Attribute**</span></span>|<span data-ttu-id="dc651-1199">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1199">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1200">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-1200">**Type**</span></span> <br/> |<span data-ttu-id="dc651-1201">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1201">Required.</span></span>  <br/> <span data-ttu-id="dc651-1202">Gibt den Typ des **MethodInstance**-Elements an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1202">Specifies the type of the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="dc651-1203">In der folgenden Tabelle sind die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1203">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-1204">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-1204">Value</span></span></p></th><th><p><span data-ttu-id="dc651-1205">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-1205">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-1206">Finder</span><span class="sxs-lookup"><span data-stu-id="dc651-1206">Finder</span></span></p></td><td><p><span data-ttu-id="dc651-p143">Ein **MethodInstance**-Typ, der aufgerufen werden kann, um eine Sammlung von null oder mehr **EntityInstances**-Elementen eines bestimmten **Entity**-Elements zurückzugeben. Eingaben für **Finder** werden durch die **FilterDescriptors**-Elemente im **Method**-Element definiert, in dem sich **Finder** befindet. </span><span class="sxs-lookup"><span data-stu-id="dc651-p143">A type of **MethodInstance** that can be called to return a collection of zero or more **EntityInstances** of a particular **Entity**. **Finder** input is defined by the **FilterDescriptors** that are contained in the **Method** that contains the **Finder**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1209">SpecificFinder</span><span class="sxs-lookup"><span data-stu-id="dc651-1209">SpecificFinder</span></span></p></td><td><p><span data-ttu-id="dc651-p144">Ein **MethodInstance**-Typ, der aufgerufen werden kann, um anhand von **EntityInstanceId** ein spezielles **EntityInstance**-Element eines bestimmten **Entity**-Elements zurückzugeben. Eingaben für **SpecificFinder** werden durch die **Identifiers**-Elemente definiert und geordnet, die der **Entity** zugeordnet sind. </span><span class="sxs-lookup"><span data-stu-id="dc651-p144">A type of **MethodInstance** that can be called to return a specific **EntityInstance** of a specific **Entity** given its **EntityInstanceId**. **SpecificFinder** input is defined and ordered by the **Identifiers** that are associated with the **Entity**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1212">GenericInvoker</span><span class="sxs-lookup"><span data-stu-id="dc651-1212">GenericInvoker</span></span></p></td><td><p><span data-ttu-id="dc651-p145">Ein **MethodInstance**-Typ, der aufgerufen werden kann, um eine bestimmte Aufgabe in einem externen System auszuführen. Die Eingaben und Ausgaben von **GenericInvoker** sind spezifisch für das **Method**-Element. </span><span class="sxs-lookup"><span data-stu-id="dc651-p145">A type of **MethodInstance** that can be called to perform a specific task in an external system. **GenericInvoker** input and output is specific to the **Method**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1215">IdEnumerators</span><span class="sxs-lookup"><span data-stu-id="dc651-1215">IdEnumerator</span></span></p></td><td><p><span data-ttu-id="dc651-p146">Ein Typ von **MethodInstance**, die aufgerufen werden können, um die **Field** Werte zurückzugeben, die die Identität des **EntityInstances** von einer bestimmten **Entity**darstellen. Die Eingabe **IdEnumerator** wird definiert, durch die **FilterDescriptors**, die in der Methode enthalten sind, die enthält die **IdEnumerator**, um die Liste der IDs, abzurufen, die die eindeutigen Schlüssel für jede Entität sind, die durchsucht werden soll. Diese Methodeninstanz kann externe Datensuche in SharePoint Server. </span><span class="sxs-lookup"><span data-stu-id="dc651-p146">A type of **MethodInstance** that can be called to return the **Field** values that represent the identity of **EntityInstances** of a specific **Entity**. The **IdEnumerator** input is defined by the **FilterDescriptors** that are contained in the method that contains the **IdEnumerator** to get the list of IDs, which are the unique keys for each entity that should be searchable. This method instance enables external data search in SharePoint Server.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1219">ChangedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="dc651-1219">ChangedIdEnumerator</span></span></p></td><td><p><span data-ttu-id="dc651-1220">Ein **MethodInstance**-Typ, der aufgerufen werden kann, um **EntityInstanceIds**-Elemente von **EntityInstances**-Elementen abzurufen, die nach einem angegebenen Zeitpunkt in einem externen System geändert wurden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1220">A type of **MethodInstance** that can be called to retrieve **EntityInstanceIds** of **EntityInstances** that were modified in an external system after a specified time.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1221">DeletedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="dc651-1221">DeletedIdEnumerator</span></span></p></td><td><p><span data-ttu-id="dc651-1222">Ein **MethodInstance**-Typ, der aufgerufen werden kann, um **EntityInstanceIds**-Elemente von **EntityInstances**-Elementen abzurufen, die nach dem angegebenen Zeitpunkt in einem externen System gelöscht wurden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1222">A type of **MethodInstance** that can be called to retrieve **EntityInstanceIds** of **EntityInstances** that were deleted from an external system after the specified time.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1223">Scalar</span><span class="sxs-lookup"><span data-stu-id="dc651-1223">Scalar</span></span></p></td><td><p><span data-ttu-id="dc651-p147">Eine **MethodInstance**, die einen einzelnen Wert zurückgibt, den Sie im externen System aufrufen können. Beispielsweise können Sie mithilfe einer skalaren Methodeninstanz den Gesamtumsatz bis dato aus dem externen System abrufen. **Entities**-Elemente haben null oder mehr skalare Methodeninstanzen. </span><span class="sxs-lookup"><span data-stu-id="dc651-p147">A **MethodInstance** that returns a single value that you can invoke in the external system. For example, you can use a scalar method instance to get the total sales made to date from the external system. **Entities** have zero or more scalar method instances.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1227">AccessChecker</span><span class="sxs-lookup"><span data-stu-id="dc651-1227">AccessChecker</span></span></p></td><td><p><span data-ttu-id="dc651-1228">Ein Typ von **MethodInstance**, durch dessen Aufruf die Berechtigungen abgerufen werden können, über die der aufrufende Sicherheitsprinzipal für die einzelnen Elemente einer Auflistung von **EntityInstances** verfügt, die durch die angegebenen **EntityInstanceIds** identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1228">A type of **MethodInstance** that can be called to retrieve the permissions that the calling security principal has for each of a collection of **EntityInstances** that are identified by the specified **EntityInstanceIds**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1229">Creator</span><span class="sxs-lookup"><span data-stu-id="dc651-1229">Creator</span></span></p></td><td><p><span data-ttu-id="dc651-1230">Ein Typ von **MethodInstance**, der zum Erstellen einer neuen **EntityInstance** aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc651-1230">A type of **MethodInstance** that can be called to delete an **EntityInstance** with a specified EntityInstanceId.</span></span> <span data-ttu-id="dc651-1231">Der Satz von Feldern, die zum Erstellen der **EntityInstance** erforderlich sind, wird die Creator-Ansicht bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="dc651-1231">A type of **MethodInstance** that can be called to create an EntityInstance. The set of fields that are required to create the EntityInstance is referred to as the Creator View.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1232">Deleter</span><span class="sxs-lookup"><span data-stu-id="dc651-1232">Deleter</span></span></p></td><td><p><span data-ttu-id="dc651-1233">Ein Typ von **MethodInstance**, durch dessen Aufruf eine **EntityInstance** mit einer bestimmten **EntityInstanceId** gelöscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc651-1233">A type of **MethodInstance** that can be called to delete an **EntityInstance** with a specified **EntityInstanceId**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1234">Updater</span><span class="sxs-lookup"><span data-stu-id="dc651-1234">Updater</span></span></p></td><td><p><span data-ttu-id="dc651-1235">Ein Typ von **MethodInstance**, der zum Aktualisieren einer **EntityInstance** aufgerufen werden kann, die von einer angegebenen **EntityInstanceId** identifiziert wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1235">A type of **MethodInstance** that can be called to delete an **EntityInstance** with a specified **EntityInstanceId**.</span></span> <span data-ttu-id="dc651-1236">Der Satz von Feldern, die zum Aktualisieren der **EntityInstance** erforderlich sind, wird als Updater-Ansicht bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="dc651-1236">The set of fields that is required to update the **EntityInstance** is known as the Updater View.</span></span> <span data-ttu-id="dc651-1237">Der Satz von Feldern, deren Werte übergeben werden sollten, bevor sie geändert werden, wird als die PreUpdater-Ansicht bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="dc651-1237">The set of fields whose values should be passed before they are changed is known as the PreUpdater View.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1238">StreamAccessor</span><span class="sxs-lookup"><span data-stu-id="dc651-1238">StreamAccessor</span></span></p></td><td><p><span data-ttu-id="dc651-1239">Ein Typ von **MethodInstance**, durch dessen Aufruf ein Feld einer **EntityInstance** in Form eines Datenstroms von Bytes abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc651-1239">A type of **MethodInstance** that can be called to retrieve a field of an **EntityInstance** in the form of a data stream of bytes.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1240">BinarySecurityDescriptorAccessor</span><span class="sxs-lookup"><span data-stu-id="dc651-1240">BinarySecurityDescriptorAccessor</span></span></p></td><td><p><span data-ttu-id="dc651-p150">Ein Typ von **MethodInstance**, durch dessen Aufruf eine Bytesequenz von einem externen System abgerufen werden kann. Die systemspezifische Bytesequenz beschreibt einen Satz von Sicherheitsprinzipalen und die Berechtigungen, die jedem Sicherheitsprinzipal für die durch eine **EntityInstanceId** identifizierte **EntityInstance** zugeordnet sind. </span><span class="sxs-lookup"><span data-stu-id="dc651-p150">A type of **MethodInstance** that can be called to retrieve a sequence of bytes from an external system. The system-specific byte sequence describes a set of security principals and the associated permissions that each security principal has for the **EntityInstance** identified by a specified **EntityInstanceId**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1243">Des BulkSpecificFinder</span><span class="sxs-lookup"><span data-stu-id="dc651-1243">BulkSpecificFinder</span></span></p></td><td><p><span data-ttu-id="dc651-1244">Ein Typ von **MethodInstance**, bei dessen Aufruf eine Menge spezifischer **EntityInstances** einer **Entity**, identifiziert durch eine Menge entsprechender **EntityInstanceIds**, zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1244">A type of **MethodInstance** that can be called to return a set of specific **EntityInstances** of an **Entity**, given a set of corresponding **EntityInstanceIds**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1245">BulkIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="dc651-1245">BulkIdEnumerator</span></span></p></td><td><p><span data-ttu-id="dc651-p151">Ein Typ von **MethodInstance**, durch dessen Aufruf minimale Informationen zu den externen Elementen abgerufen werden, die den angegebenen Identitäten entsprechen. Mit dieser Methodeninstanz kann die Synchronisierung zwischengespeicherter Daten optimiert werden. Die Methode sollte nur die Identitäten und Versionsinformationen der externen Elemente zurückgeben, die den angegebenen **Identities** entsprechen. Diese können von der aufrufenden Anwendung mit der lokalen Version verglichen werden, um Änderungen zu erkennen und ggf. die Aktualisierung der zwischengespeicherten Daten durch die geänderten externen Elemente anzufordern. </span><span class="sxs-lookup"><span data-stu-id="dc651-p151">A type of **MethodInstance** that can be called to retrieve minimal information about the external items corresponding to the given identities. This method instance can be used to optimize synchronization of cached data. This method should return only the identities and version information of the external items that correspond to given **Identities**, which the calling application can compare with the local version to identify if anything has changed, and if so, request the changed external items to update the cached data.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="dc651-1249">**Standard**</span><span class="sxs-lookup"><span data-stu-id="dc651-1249">**Default**</span></span> <br/> |<span data-ttu-id="dc651-1250">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1250">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1251">Gibt an, ob die **MethodInstance** bei allen **MethodInstances**, die den gleichen Typ innerhalb des enthaltenden externen Inhaltstyps verwenden (**Entität**) Standard ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-1251">Specifies whether the **MethodInstance** is the default among all **MethodInstances** that share its type within the containing external content type ( **Entity**).</span></span>  <br/> <span data-ttu-id="dc651-1252">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1252">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1253">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1253">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1254">**ReturnParameterName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1254">**ReturnParameterName**</span></span> <br/> |<span data-ttu-id="dc651-1255">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1255">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p152"> Der Name des **Parameter**-Elements, das den **ReturnTypeDescriptor** des **MethodInstance**-Elements enthält. Das **Direction**-Attribut von **Parameter** muss ein **ParameterDirection**-Attribut mit dem Wert **Out**, **InOut** oder **Return** sein. </span><span class="sxs-lookup"><span data-stu-id="dc651-p152">The name of the **Parameter** that contains the **ReturnTypeDescriptor** of the **MethodInstance**. The **Direction** attribute of the **Parameter** must be a **ParameterDirection** attribute with a value of **Out**, **InOut**, or **Return**.  </span></span><br/> <span data-ttu-id="dc651-1258">Dieses Attribut muss für alle Typen von **MethodInstances** außer **GenericInvoker**, **Creator**, **Deleter** und **Updater** angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1258">This attribute must be specified for all types of **MethodInstances** except **GenericInvoker**, **Creator**, **Deleter**, and **Updater**.</span></span>  <br/> <span data-ttu-id="dc651-1259">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1259">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1260">**ReturnTypeDescriptorLevel**</span><span class="sxs-lookup"><span data-stu-id="dc651-1260">**ReturnTypeDescriptorLevel**</span></span> <br/> |<span data-ttu-id="dc651-1261">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1261">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p153">Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="dc651-p153">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="dc651-1264">Attributtyp: **Integer**</span><span class="sxs-lookup"><span data-stu-id="dc651-1264">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="dc651-1265">**ReturnTypeDescriptorPath**</span><span class="sxs-lookup"><span data-stu-id="dc651-1265">**ReturnTypeDescriptorPath**</span></span> <br/> |<span data-ttu-id="dc651-1266">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1266">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1267">Der gepunktete Pfad des **TypeDescriptors** der Zuordnung. </span><span class="sxs-lookup"><span data-stu-id="dc651-1267">The dotted path of the **TypeDescriptor** of the Association.</span></span> <br/> <span data-ttu-id="dc651-1268">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1268">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1269">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-1269">**Name**</span></span> <br/> |<span data-ttu-id="dc651-1270">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1270">Required.</span></span>  <br/> <span data-ttu-id="dc651-1271">Gibt den Namen der **MethodInstance** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1271">Specifies the name of the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="dc651-1272">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1272">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1273">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1273">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-1274">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1274">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1275">Gibt den Standardanzeigenamen für die **MethodInstance** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1275">Specifies the default display name for the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="dc651-1276">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1276">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1277">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-1277">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-1278">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1278">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1279">Gibt an, ob die **MethodInstance** häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1279">Specifies whether the **MethodInstance** is used frequently.</span></span> <br/> <span data-ttu-id="dc651-1280">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1280">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1281">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1281">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1282">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1282">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1283">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1283">**Element**</span></span>|<span data-ttu-id="dc651-1284">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1284">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1285">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1285">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1286">Die lokalisierten Anzeigenamen von **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1286">The localized display names of the **MethodInstance**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1287">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1287">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1288">Die Eigenschaften des **MethodInstance**-Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1288">The properties of the **MethodInstance**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1289">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1289">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1290">Die Zugriffssteuerungslisten (Access Control Lists, ACLs) von **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1290">The access control lists (ACLs) of the **MethodInstance**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1291">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1291">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1292">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1292">**Element**</span></span>|<span data-ttu-id="dc651-1293">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1293">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1294">"MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1294">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1295">Das **MethodInstances**-Element, das diesen **MethodInstance**-Parameter enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1295">The **MethodInstances** element that contains this **MethodInstance**.</span></span>  <br/> |
   

## <a name="methodinstances-element"></a><span data-ttu-id="dc651-1296">"MethodInstances"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1296">MethodInstances element</span></span>
<span data-ttu-id="dc651-1297"><a name="bkmk_MethodInstances"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1297"></span></span>

<span data-ttu-id="dc651-1298">Gibt eine Liste der Zuordnungen und Methodeninstanzen einer Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1298">Specifies a list of associations and method instances of a method.</span></span>
  
    
    
 <span data-ttu-id="dc651-1299">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1299">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1300">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1300">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<MethodInstances></MethodInstances>
```

<span data-ttu-id="dc651-1301">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1301">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1302">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1302">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1303">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1303">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1304">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1304">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1305">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1305">**Element**</span></span>|<span data-ttu-id="dc651-1306">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1306">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1307">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1307">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1308">Eine Zuordnung.</span><span class="sxs-lookup"><span data-stu-id="dc651-1308">An association.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1309">MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1309">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1310">Eine Methodeninstanz.</span><span class="sxs-lookup"><span data-stu-id="dc651-1310">A method instance.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1311">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1311">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1312">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1312">**Element**</span></span>|<span data-ttu-id="dc651-1313">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1313">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1314">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1314">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1315">Die Methode, zu der diese Methodeninstanz gehört.</span><span class="sxs-lookup"><span data-stu-id="dc651-1315">The method that this method instance belongs to.</span></span>  <br/> |
   

## <a name="methods-element"></a><span data-ttu-id="dc651-1316">Methods-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1316">Methods element</span></span>
<span data-ttu-id="dc651-1317"><a name="bkmk_Methods"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1317"></span></span>

<span data-ttu-id="dc651-1318">Gibt eine Liste mit Methoden eines externen Inhaltstyps an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1318">Specifies a list of methods of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-1319">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1319">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1320">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1320">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Methods></Methods>
```

<span data-ttu-id="dc651-1321">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1321">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1322">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1322">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1323">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1323">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1324">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1324">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1325">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1325">**Element**</span></span>|<span data-ttu-id="dc651-1326">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1326">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1327">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1327">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1328">Gibt eine Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1328">Specifies a method.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1329">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1329">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1330">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1330">**Element**</span></span>|<span data-ttu-id="dc651-1331">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1331">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1332">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1332">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1333">Der externe Inhaltstyp, zu dem diese Liste mit Methoden gehört.</span><span class="sxs-lookup"><span data-stu-id="dc651-1333">The external content type that this list of methods belongs to.</span></span>  <br/> |
   

## <a name="model-element"></a><span data-ttu-id="dc651-1334">"Model"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1334">Model element</span></span>
<span data-ttu-id="dc651-1335"><a name="bkmk_Model"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1335"></span></span>

<span data-ttu-id="dc651-p154">Legt das Stammelement fest, das eine Anwendungsdefinition darstellt. Modelle definieren externe Inhaltstypen, die in externen Anwendungen enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="dc651-p154">Specifies the root element that represents an application definition. Models define external content types that are contained by external applications.</span></span> 
  
    
    
 <span data-ttu-id="dc651-1338">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1338">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1339">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1339">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Model Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Model>
```

<span data-ttu-id="dc651-1340">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1340">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1341">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1341">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1342">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1342">**Attribute**</span></span>|<span data-ttu-id="dc651-1343">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1343">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1344">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-1344">Name</span></span>  <br/> |<span data-ttu-id="dc651-1345">Der Name des **Model**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-1345">The name of the **Model**.</span></span>  <br/> <span data-ttu-id="dc651-1346">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1346">Required.</span></span>  <br/> <span data-ttu-id="dc651-1347">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1347">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1348">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="dc651-1348">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="dc651-1349">Der Standardanzeigename des **Model**-Elements.</span><span class="sxs-lookup"><span data-stu-id="dc651-1349">The default display name of the **Model**.</span></span>  <br/> <span data-ttu-id="dc651-1350">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1350">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1351">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1351">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1352">IsCached</span><span class="sxs-lookup"><span data-stu-id="dc651-1352">IsCached</span></span>  <br/> |<span data-ttu-id="dc651-p155">Gibt an, ob das **Model** häufig verwendet wird. Wenn dies auf **true** festgelegt ist, wird das **Model** vom Business Data Connectivity (BDC)-Dienst zwischengespeichert. </span><span class="sxs-lookup"><span data-stu-id="dc651-p155">Specifies whether the **Model** is used frequently. If this is set to **true**, then the **Model** is cached by the Business Data Connectivity (BDC) service. </span></span><br/> <span data-ttu-id="dc651-1355">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1355">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1356">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1356">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1357">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1357">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1358">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1358">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1359">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1359">**Element**</span></span>|<span data-ttu-id="dc651-1360">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1360">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1361">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1361">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1362">Die lokalisierten Namen des **Model**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-1362">The localized names of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1363">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1363">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1364">Die Eigenschaften des **Model**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-1364">The properties of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1365">AccessControlList-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1365">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1366">Die Zugriffssteuerungsliste (Access Control List, ACL) des **Model**-Elements</span><span class="sxs-lookup"><span data-stu-id="dc651-1366">The access control list (ACL) of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1367">"LobSystems"-Element im Modell ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1367">LobSystems Element in Model (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1368">Das in diesem **Model**-Element enthaltene **LobSystems**</span><span class="sxs-lookup"><span data-stu-id="dc651-1368">The **LobSystems** contained inside this **Model**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1369">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1369">**Parent element**</span></span>
  
    
    
<span data-ttu-id="dc651-1370">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1370">None</span></span>
  
    
    

## <a name="normalizedatetime-element"></a><span data-ttu-id="dc651-1371">NormalizeDateTime (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-1371">NormalizeDateTime element</span></span>
<span data-ttu-id="dc651-1372"><a name="bkmk_NormalizeDateTime"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1372"></span></span>

<span data-ttu-id="dc651-p156">Gibt die Regel an, die zur Konvertierung der Darstellung des Datums- und Zeitwertes in eine andere Darstellung verwendet wird. Diese Regel kann beispielsweise angeben, dass ein in koordinierter Weltzeit (Coordinated Universal Time, UTC) angegebener Wert in eine lokale Zeitzone konvertiert wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-p156">Specifies the rule used to convert the representation of a date and time value to another representation. For example, this rule can specify converting a value represented in Coordinated Universal Time (UTC) into a local time zone.</span></span> 
  
    
    
 <span data-ttu-id="dc651-1375">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1375">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1376">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1376">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<NormalizeDateTime LobDateTimeMode = "String"> </NormalizeDateTime>
```

<span data-ttu-id="dc651-1377">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1377">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1378">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1378">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1379">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1379">**Attribute**</span></span>|<span data-ttu-id="dc651-1380">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1380">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1381">**LobDateTimeMode**</span><span class="sxs-lookup"><span data-stu-id="dc651-1381">**LobDateTimeMode**</span></span> <br/> |<span data-ttu-id="dc651-1382">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1382">Required.</span></span>  <br/> <span data-ttu-id="dc651-1383">Gibt die gewünschte Konvertierung an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1383">Specifies the conversion to apply.</span></span>  <br/> <span data-ttu-id="dc651-1384">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1384">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-1385">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-1385">Value</span></span></p></th><th><p><span data-ttu-id="dc651-1386">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-1386">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-1387">UTC</span><span class="sxs-lookup"><span data-stu-id="dc651-1387">UTC</span></span></p></td><td><p><span data-ttu-id="dc651-p157">Der Wert, der vom externen System empfangen wird, ist in koordinierter Weltzeit (Coordinated Universal Time, UTC) angegeben. Wenn der empfangene Wert **Local** ist, wird dieser in koordinierte Weltzeit konvertiert. BDC sendet koordinierte Weltzeit an das externe System.</span><span class="sxs-lookup"><span data-stu-id="dc651-p157">The value that is received from the external system is UTC (Coordinated Universal Time). If the value received is **Local**, it is converted to UTC. BDC sends UTC to the external system.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1391">Lokal</span><span class="sxs-lookup"><span data-stu-id="dc651-1391">Local</span></span></p></td><td><p><span data-ttu-id="dc651-p158">Der vom externen System empfangene Wert ist **Local**. Wenn der vom externen System empfangene Wert **Local** ist, wird dieser in koordinierte Weltzeit konvertiert. **Local** wird von BDC an das externe System gesendet. </span><span class="sxs-lookup"><span data-stu-id="dc651-p158">The value received from the external system is **Local**. If the value received from the external system is **Local**, then it will be converted to UTC. BDC sends **Local** to the external system.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1395">Unspecified</span><span class="sxs-lookup"><span data-stu-id="dc651-1395">Unspecified</span></span></p></td><td><p><span data-ttu-id="dc651-p159">Der vom externen System gesendete Wert weist einen nicht definierten Typ auf. BDC geht davon aus, dass es sich um einen Wert in koordinierter Weltzeit handelt, indem der Wert als koordinierte Weltzeit überschrieben wird. Werte in koordinierter Weltzeit werden von BDC als Werte eines nicht definierten Typs an das externe System gesendet.</span><span class="sxs-lookup"><span data-stu-id="dc651-p159">The value sent by the external system has Unspecified kind. BDC assumes the value is in UTC by overwriting the kind to be UTC. BDC sends UTC values as Unspecified kind to the external system.</span></span></p></td></tr></tbody></table>
|
   
 <span data-ttu-id="dc651-1399">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1399">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1400">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1400">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1401">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1401">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1402">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1402">**Element**</span></span>|<span data-ttu-id="dc651-1403">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1403">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1404">Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1404">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1405">Ein **Interpretation**-Element, das die Regeln angibt, die auf die in den Datenstrukturen gespeicherten Daten dargestellt durch **TypeDescriptor** angewendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="dc651-1405">An **Interpretation** element that specifies the rules to apply to the data that is stored in the data structures represented by a **TypeDescriptor**.</span></span>  <br/> |
   

## <a name="normalizestring-element"></a><span data-ttu-id="dc651-1406">NormalizeString-element</span><span class="sxs-lookup"><span data-stu-id="dc651-1406">NormalizeString element</span></span>
<span data-ttu-id="dc651-1407"><a name="bkmk_NormalizeString"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1407"></span></span>

<span data-ttu-id="dc651-1408">Gibt einen Parameter für eine Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1408">Specifies a parameter of a method.</span></span>
  
    
    
 <span data-ttu-id="dc651-1409">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1409">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1410">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1410">**Schema:** BDCMetadata</span></span>
  
    
    



```XML

```

<span data-ttu-id="dc651-1411">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1411">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1412">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1412">**Attributes**</span></span>
  
    
    
 <span data-ttu-id="dc651-1413">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1413">**Child elements**</span></span>
  
    
    
 <span data-ttu-id="dc651-1414">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1414">**Parent element**</span></span>
  
    
    

## <a name="parameter-element"></a><span data-ttu-id="dc651-1415">Parameter-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1415">Parameter element</span></span>
<span data-ttu-id="dc651-1416"><a name="bkmk_Parameter"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1416"></span></span>

<span data-ttu-id="dc651-1417">Gibt einen Parameter für eine Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1417">Specifies a parameter of a method.</span></span>
  
    
    
 <span data-ttu-id="dc651-1418">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1418">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1419">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1419">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Parameter Direction = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Parameter>
```

<span data-ttu-id="dc651-1420">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1420">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1421">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1421">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1422">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1422">**Attribute**</span></span>|<span data-ttu-id="dc651-1423">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1423">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1424">Direction</span><span class="sxs-lookup"><span data-stu-id="dc651-1424">Direction</span></span>  <br/> |<span data-ttu-id="dc651-1425">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1425">Required.</span></span>  <br/> <span data-ttu-id="dc651-1426">Die Richtung des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1426">The direction of the parameter.</span></span>  <br/> <span data-ttu-id="dc651-1427">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1427">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-1428">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-1428">Value</span></span></p></th><th><p><span data-ttu-id="dc651-1429">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-1429">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-1430">In</span><span class="sxs-lookup"><span data-stu-id="dc651-1430">In</span></span></p></td><td><p><span data-ttu-id="dc651-1431">Der dargestellte **Parameter** ist ein Eingabeparameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-1431">The represented **Parameter** is an input parameter.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1432">Out</span><span class="sxs-lookup"><span data-stu-id="dc651-1432">Out</span></span></p></td><td><p><span data-ttu-id="dc651-1433">Der dargestellte Parameter ist ein Ausgabeparameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-1433">The represented parameter is an output parameter.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1434">InOut</span><span class="sxs-lookup"><span data-stu-id="dc651-1434">InOut</span></span></p></td><td><p><span data-ttu-id="dc651-1435">Der dargestellte Parameter ist ein Eingabe- und Ausgabeparameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-1435">The represented parameter is an input and output parameter. In C#, these correspond to "ref".</span></span> <span data-ttu-id="dc651-1436">In C# entspricht dies "**ref**".</span><span class="sxs-lookup"><span data-stu-id="dc651-1436">In C#, these correspond to "**ref**".</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1437">Return</span><span class="sxs-lookup"><span data-stu-id="dc651-1437">Return</span></span></p></td><td><p><span data-ttu-id="dc651-1438">Der dargestellte Parameter ist ein Rückgabeparameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-1438">The represented parameter is a return parameter.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="dc651-1439">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-1439">**Name**</span></span> <br/> |<span data-ttu-id="dc651-1440">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1440">Required.</span></span>  <br/> <span data-ttu-id="dc651-1441">Der Name des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1441">The name of the parameter.</span></span>  <br/> <span data-ttu-id="dc651-1442">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1442">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1443">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1443">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-1444">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1444">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1445">Der Standardanzeigename des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1445">The default display name of the parameter.</span></span>  <br/> <span data-ttu-id="dc651-1446">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1446">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1447">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-1447">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-1448">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1448">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1449">Gibt an, ob der **Parameter** häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1449">Specifies whether the **Parameter** is used frequently.</span></span> <br/> <span data-ttu-id="dc651-1450">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1450">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1451">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1451">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1452">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1452">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1453">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1453">**Element**</span></span>|<span data-ttu-id="dc651-1454">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1454">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1455">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1455">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1456">Die lokalisierten Namen des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1456">The localized names of the parameter.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1457">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1457">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1458">Die Eigenschaften des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1458">The properties of the parameter.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1459">TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="dc651-1459">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> |<span data-ttu-id="dc651-1460">Der Stammtypdeskriptor des Parameters.</span><span class="sxs-lookup"><span data-stu-id="dc651-1460">The root type descriptor of the parameter.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1461">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1461">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1462">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1462">**Element**</span></span>|<span data-ttu-id="dc651-1463">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1463">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1464">Parameters-Element in "Method" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1464">Parameters Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1465">Das **Parameters**-Element, das diesen Parameter enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1465">The **Parameters** element that contains this parameter.</span></span> <br/> |
   

## <a name="parameters-element"></a><span data-ttu-id="dc651-1466">"Parameters"-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1466">Parameters element</span></span>
<span data-ttu-id="dc651-1467"><a name="bkmk_Parameters"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1467"></span></span>

<span data-ttu-id="dc651-1468">Gibt eine Liste mit Parametern einer Methode an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1468">Specifies a list of parameters of a method.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="dc651-1469">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1469">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1470">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1470">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Parameters></Parameters>
```

<span data-ttu-id="dc651-1471">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1471">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1472">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1472">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1473">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1473">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1474">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1474">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1475">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1475">**Element**</span></span>|<span data-ttu-id="dc651-1476">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1476">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1477">Parameter-Element in "Parameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1477">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1478">Ein Parameter.</span><span class="sxs-lookup"><span data-stu-id="dc651-1478">A parameter.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1479">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1479">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1480">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1480">**Element**</span></span>|<span data-ttu-id="dc651-1481">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1481">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1482">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1482">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1483">Die Methode, zu der diese Parameter gehören.</span><span class="sxs-lookup"><span data-stu-id="dc651-1483">The method these parameters belong to.</span></span>  <br/> |
   

## <a name="properties-element"></a><span data-ttu-id="dc651-1484">Properties-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1484">Properties element</span></span>
<span data-ttu-id="dc651-1485"><a name="bkmk_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1485"></span></span>

<span data-ttu-id="dc651-1486">Gibt eine Liste der Eigenschaften eines Metadatenobjekts an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1486">Specifies a list of properties of a metadata object.</span></span>
  
    
    
 <span data-ttu-id="dc651-1487">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1487">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1488">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1488">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Properties></Properties>
```

<span data-ttu-id="dc651-1489">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1489">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1490">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1490">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1491">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1491">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1492">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1492">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1493">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1493">**Element**</span></span>|<span data-ttu-id="dc651-1494">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1494">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1495">Property-Element in "Properties" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1495">Property Element in Properties (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/2e6e8d5d-ef3b-c536-f3d1-ad2039b92c24%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1496">Gibt eine Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1496">Specifies a property.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1497">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1497">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1498">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1498">**Element**</span></span>|<span data-ttu-id="dc651-1499">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1499">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1500">"Model"-Element ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1500">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1501">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1501">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1502">LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1502">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1503">Entity-Element in Entities (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1503">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1504">Identifier-Element in "Identifiers" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1504">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1505">Method-Element in Methods (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1505">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1506">"FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1506">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1507">Parameter-Element in "Parameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1507">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1508">TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="dc651-1508">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
| [<span data-ttu-id="dc651-1509">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1509">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1510">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1510">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1511">MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1511">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1512">"AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1512">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1513">"Action"-Element in "Actions" ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1513">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1514">ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1514">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="property-element"></a><span data-ttu-id="dc651-1515">Property-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1515">Property element</span></span>
<span data-ttu-id="dc651-1516"><a name="bkmk_Property"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1516"></span></span>

<span data-ttu-id="dc651-1517">Gibt den Name und den Typ für eine Eigenschaft eines Metadatenobjekts an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1517">Specifies the name and type of a property of a metadata object.</span></span>
  
    
    
 <span data-ttu-id="dc651-1518">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1518">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1519">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1519">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Property Name = "String" Type = "String"> </Property>
```

<span data-ttu-id="dc651-1520">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1520">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1521">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1521">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1522">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1522">**Attribute**</span></span>|<span data-ttu-id="dc651-1523">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1523">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1524">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-1524">**Name**</span></span> <br/> |<span data-ttu-id="dc651-1525">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1525">Required.</span></span>  <br/> <span data-ttu-id="dc651-1526">Gibt den Namen der Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1526">Specifies the name of the property.</span></span>  <br/> <span data-ttu-id="dc651-1527">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1527">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1528">**Typ**</span><span class="sxs-lookup"><span data-stu-id="dc651-1528">**Type**</span></span> <br/> |<span data-ttu-id="dc651-1529">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1529">Required.</span></span>  <br/> <span data-ttu-id="dc651-1530">Gibt den Datentyp der Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1530">Specifies data type of the property.</span></span>  <br/> <span data-ttu-id="dc651-1531">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1531">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1532">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1532">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1533">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1533">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1534">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1534">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1535">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1535">**Element**</span></span>|<span data-ttu-id="dc651-1536">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1536">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1537">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1537">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1538">Das **Properties**-Element, das diese Eigenschaft enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1538">The **Properties** element that contains this property.</span></span> <br/> |
   

## <a name="proxy-element"></a><span data-ttu-id="dc651-1539">Proxy-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1539">Proxy element</span></span>
<span data-ttu-id="dc651-1540"><a name="bkmk_Proxy"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1540"></span></span>

<span data-ttu-id="dc651-p161">Gibt einen vom Benutzer bereitgestellten Proxy an, der mit dem Proxy identisch ist, der generiert würde, wenn dieses Element nicht vorhanden wäre. Durch die Eliminierung des Mehraufwands für die Proxygenerierung wird die Leistung verbessert. Externe Systeme vom Typ ".NET-Verbindungsassembly" müssen verwendet werden, um benutzerdefinierte Geschäftslogik anzugeben, mit der eine Verbindung mit einem externen System hergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-p161">Specifies a user-provided proxy that is identical to the one that would be generated if this element was not present. This is used to improve performance by removing the proxy generation overhead. To specify custom business logic that connects to an external system, .NET Connectivity Assembly type external systems must be used.</span></span>
  
    
    
 <span data-ttu-id="dc651-1544">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1544">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1545">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1545">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Proxy></Proxy>
```

<span data-ttu-id="dc651-1546">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1546">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1547">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1547">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1548">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1548">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1549">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1549">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1550">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1550">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1551">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1551">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1552">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1552">**Element**</span></span>|<span data-ttu-id="dc651-1553">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1553">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1554">"LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1554">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1555">Das **LobSystem**-Element, für das dieser Proxy gilt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1555">The **LobSystem** element that this proxy applies to.</span></span> <br/> |
   

## <a name="right-element"></a><span data-ttu-id="dc651-1556">Right-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1556">Right element</span></span>
<span data-ttu-id="dc651-1557"><a name="bkmk_Right"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1557"></span></span>

<span data-ttu-id="dc651-1558">Gibt eine einzelne Zugriffsberechtigung für einen Zugriffssteuerungseintrag (Access Control Entry, ACE) an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1558">Specifies a single access permission for an access control entry (ACE).</span></span>
  
    
    
 <span data-ttu-id="dc651-1559">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1559">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1560">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1560">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Right BdcRight = "String"> </Right>
```

<span data-ttu-id="dc651-1561">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1561">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1562">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1562">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1563">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1563">**Attribute**</span></span>|<span data-ttu-id="dc651-1564">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1564">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1565">BdcRight</span><span class="sxs-lookup"><span data-stu-id="dc651-1565">BdcRight</span></span>  <br/> |<span data-ttu-id="dc651-1566">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1566">Required.</span></span>  <br/> <span data-ttu-id="dc651-1567">Die verfügbare Berechtigung für den Sicherheitsprinzipal, der über das Recht verfügt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1567">The permission available to the security principal holding the right.</span></span>  <br/> <span data-ttu-id="dc651-1568">In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1568">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="dc651-1569">Wert</span><span class="sxs-lookup"><span data-stu-id="dc651-1569">Value</span></span></p></th><th><p><span data-ttu-id="dc651-1570">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dc651-1570">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="dc651-1571">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1571">None</span></span></p></td><td><p><span data-ttu-id="dc651-1572">Keine Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="dc651-1572">No permissions.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1573">Ausführen</span><span class="sxs-lookup"><span data-stu-id="dc651-1573">Execute</span></span></p></td><td><p><span data-ttu-id="dc651-1574">Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, eine **MethodInstance** aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="dc651-1574">The represented security principal has the permission to invoke a **MethodInstance**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1575">Bearbeiten</span><span class="sxs-lookup"><span data-stu-id="dc651-1575">Edit</span></span></p></td><td><p><span data-ttu-id="dc651-1576">Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, die Attribute eines Metadatenobjekts oder die Attribute von dessen Beziehung zu anderen Metadatenobjekten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="dc651-1576">The represented security principal has permission to change the attributes of a metadata object or its relationship to other metadata objects.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1577">SetPermissions</span><span class="sxs-lookup"><span data-stu-id="dc651-1577">SetPermissions</span></span></p></td><td><p><span data-ttu-id="dc651-1578">Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, den Satz der Berechtigungen für ein Metadatenobjekt zu ändern.</span><span class="sxs-lookup"><span data-stu-id="dc651-1578">The represented security principal has permission to change the set of permissions for a metadata object.</span></span></p></td></tr><tr><td><p><span data-ttu-id="dc651-1579">SelectableInClients</span><span class="sxs-lookup"><span data-stu-id="dc651-1579">SelectableInClients</span></span></p></td><td><p><span data-ttu-id="dc651-p162">Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, das Metadatenobjekt, auf das sich dieses Recht bezieht, auszuwählen. Wenn ein Benutzer nicht über diese Berechtigung verfügt, sollte das Metadatenobjekt nicht auswählbar sein.</span><span class="sxs-lookup"><span data-stu-id="dc651-p162">The represented security principal has permission to select the metadata object this right refers to. If a user does not have this permission, the metadata object should not be selectable.</span></span></p></td></tr></tbody></table>
|
   
 <span data-ttu-id="dc651-1582">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1582">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1583">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1583">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1584">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1584">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1585">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1585">**Element**</span></span>|<span data-ttu-id="dc651-1586">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1586">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1587">AccessControlEntry-Element in "AccessControlList" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1587">AccessControlEntry Element in AccessControlList (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1588">Das **AccessControlEntry**-Element, das dieses Recht enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1588">The **AccessControlEntry** element that contains this right.</span></span> <br/> |
   

## <a name="sourceentity-element"></a><span data-ttu-id="dc651-1589">SourceEntity-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1589">SourceEntity element</span></span>
<span data-ttu-id="dc651-1590"><a name="bkmk_SourceEntity"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1590"></span></span>

<span data-ttu-id="dc651-1591">Gibt einen externen Quellinhaltstyp eines **Association**-Elements an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1591">Specifies a source external content type of an **Association**.</span></span>
  
    
    
 <span data-ttu-id="dc651-1592">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1592">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1593">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1593">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<SourceEntity Namespace = "String" Name = "String"> </SourceEntity>
```

<span data-ttu-id="dc651-1594">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1594">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1595">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1595">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1596">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1596">**Attribute**</span></span>|<span data-ttu-id="dc651-1597">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1597">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1598">Namespace</span><span class="sxs-lookup"><span data-stu-id="dc651-1598">Namespace</span></span>  <br/> |<span data-ttu-id="dc651-1599">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1599">Required.</span></span>  <br/> <span data-ttu-id="dc651-1600">Der Namespace des externen Inhaltstyps, der die Quelle des **Association**-Elements darstellt, das dieses Element enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1600">The namespace of the external content type that is the source of the **Association** that contains this element.</span></span> <br/> <span data-ttu-id="dc651-1601">Attributtyp: String</span><span class="sxs-lookup"><span data-stu-id="dc651-1601">Attribute type: String</span></span>  <br/> |
|<span data-ttu-id="dc651-1602">Name</span><span class="sxs-lookup"><span data-stu-id="dc651-1602">Name</span></span>  <br/> |<span data-ttu-id="dc651-1603">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1603">Required.</span></span>  <br/> <span data-ttu-id="dc651-1604">Der Name des externen Inhaltstyps, der die Quelle des **Association**-Elements darstellt, das dieses Element enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1604">The name of the external content type that is the source of the **Association** that contains this element.</span></span> <br/> <span data-ttu-id="dc651-1605">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1605">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1606">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1606">**Child elements**</span></span>
  
    
    
<span data-ttu-id="dc651-1607">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1607">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1608">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1608">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1609">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1609">**Element**</span></span>|<span data-ttu-id="dc651-1610">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1610">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1611">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1611">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1612">Das **Association**-Element, das dieses Element enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1612">The **Association** that contains this element.</span></span> <br/> |
   

## <a name="typedescriptor-element"></a><span data-ttu-id="dc651-1613">TypeDescriptor (Element)</span><span class="sxs-lookup"><span data-stu-id="dc651-1613">TypeDescriptor element</span></span>
<span data-ttu-id="dc651-1614"><a name="bkmk_TypeDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1614"></span></span>

<span data-ttu-id="dc651-1615">Gibt einen **TypeDescriptor** an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1615">Specifies a **TypeDescriptor**.</span></span>
  
    
    
 <span data-ttu-id="dc651-1616">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1616">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1617">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1617">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<TypeDescriptor TypeName = "String" LobName = "String" IdentifierEntityNamespace = "String" IdentifierEntityName = "String" IdentifierName = "String" ForeignIdentifierAssociationName = "String" ForeignIdentifierAssociationEntityName = "String" ForeignIdentifierAssociationEntityNamespace = "String" AssociatedFilter = "String" IsCollection = "Boolean" ReadOnly = "Boolean" CreatorField = "Boolean" UpdaterField = "Boolean" PreUpdaterField = "Boolean" Significant = "Boolean" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </TypeDescriptor>
```

<span data-ttu-id="dc651-1618">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1618">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1619">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1619">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="dc651-1620">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="dc651-1620">**Attribute**</span></span>|<span data-ttu-id="dc651-1621">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1621">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dc651-1622">**TypeName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1622">**TypeName**</span></span> <br/> |<span data-ttu-id="dc651-1623">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1623">Required.</span></span>  <br/> <span data-ttu-id="dc651-1624">Der Bezeichner des Datentyps der Datenstruktur, die durch den **TypeDescriptor** dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1624">The identifier of the data type of the data structure that is represented by the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="dc651-1625">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1625">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1626">**LobName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1626">**LobName**</span></span> <br/> |<span data-ttu-id="dc651-1627">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1627">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1628">Die Datenstruktur, die durch den **TypeDescriptor** dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1628">The identifier of the data type of the data structure that is represented by the **TypeDescriptor**.</span></span> <span data-ttu-id="dc651-1629">Der Standardwert dieses Attributs ist der Name für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1629">The default value of this attribute is the name of the **TypeDescriptor**.</span></span> <span data-ttu-id="dc651-1630">So kann beispielsweise eine Datenstruktur eines Branchensystems (Line of Business, LOB) mit dem Namen CN1A durch einen **TypeDescriptor** dargestellt werden, dessen **Name**-Attribut „Kundenname“ entspricht, wenn das **LobName**-Attribut für den **TypeDescriptor** „CN1A“ entspricht.</span><span class="sxs-lookup"><span data-stu-id="dc651-1630">The data structure that is represented by the **TypeDescriptor**. The default value of this attribute is the name of the **TypeDescriptor**. For example, a line-of-business (LOB) system data structure named "CN1A" can be represented by a **TypeDescriptor** with **Name** attribute equal to "Customer Name", if the LobName attribute of this TypeDescriptor is equal to "CN1A".</span></span> <br/> <span data-ttu-id="dc651-1631">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1631">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1632">**IdentifierEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="dc651-1632">**IdentifierEntityNamespace**</span></span> <br/> |<span data-ttu-id="dc651-1633">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1633">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p164"> Der Namespace des externen Inhaltstyps, der den Bezeichner enthält, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **IdentifierEntityName** und **IdentifierName** vorhanden sein. Der Standardwert dieses Attributs ist der Namespace des externen Inhaltstyps, der die Methode enthält, die den Parameter enthält, der wiederum den **TypeDescriptor** enthält. </span><span class="sxs-lookup"><span data-stu-id="dc651-p164">The namespace of the external content type that contains the identifier that the **TypeDescriptor** references. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present. When this attribute is present, the **IdentifierEntityName** and **IdentifierName** attributes must also be present. The default value of this attribute is the namespace of the external content type that contains the method containing the parameter that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="dc651-1638">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1638">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1639">**IdentifierEntityName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1639">**IdentifierEntityName**</span></span> <br/> |<span data-ttu-id="dc651-1640">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1640">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p165"> Der Name der **Entity**, die den **Identifier** enthält, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **IdentifierEntityNamespace** und **IdentifierName** vorhanden sein. Der Standardwert des Attributs ist der Name der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. </span><span class="sxs-lookup"><span data-stu-id="dc651-p165">The name of the **Entity** that contains the **Identifier** that the c **TypeDescriptor** references. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present. When this attribute is present, the **IdentifierEntityNamespace** and **IdentifierName** attributes must also be present. The default value of this attribute is the name of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="dc651-1645">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1645">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1646">**IdentifierName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1646">**IdentifierName**</span></span> <br/> |<span data-ttu-id="dc651-1647">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1647">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p166"> Der Name für den **Identifier**, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. </span><span class="sxs-lookup"><span data-stu-id="dc651-p166">The name of the **Identifier** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present.  </span></span><br/> <span data-ttu-id="dc651-1650">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1650">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1651">**ForeignIdentifierAssociationName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1651">**ForeignIdentifierAssociationName**</span></span> <br/> |<span data-ttu-id="dc651-1652">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1652">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p167"> Der Name der **Association**, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, muss auch das **IdentifierName**-Attribut vorhanden sein. Das **ForeignIdentifierAssociationName**-Attribut muss angegeben werden, wenn der **Identifier**, auf den dieser **TypeDescriptor** verweist, zu einer **Association** gehört und der **Identifier** in einer Quell- **Entity** der **Association** enthalten ist. </span><span class="sxs-lookup"><span data-stu-id="dc651-p167">The name of the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **IdentifierName** attribute must also be present. The **ForeignIdentifierAssociationName** attribute must be specified when the **Identifier** referenced by this **TypeDescriptor** is related to an **Association**, and the **Identifier** is contained by a source **Entity** of the **Association**.  </span></span><br/> <span data-ttu-id="dc651-1657">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1657">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1658">**ForeignIdentifierAssociationEntityName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1658">**ForeignIdentifierAssociationEntityName**</span></span> <br/> |<span data-ttu-id="dc651-1659">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1659">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p168"> Der Name der **Entity**, die die **Association** enthält, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **ForeignIdentifierAssociationEntityNamespace** und **ForeignIdentifierAssociationName** vorhanden sein. Der Standardwert des Attributs ist der Name der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. </span><span class="sxs-lookup"><span data-stu-id="dc651-p168">The name of the **Entity** that contains the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **ForeignIdentifierAssociationEntityNamespace** and **ForeignIdentifierAssociationName** attributes must also be present. The default value of this attribute is the name of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="dc651-1664">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1664">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1665">**ForeignIdentifierAssociationEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="dc651-1665">**ForeignIdentifierAssociationEntityNamespace**</span></span> <br/> |<span data-ttu-id="dc651-1666">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1666">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p169"> Der Namespace der **Entity**, die die **Association** enthält, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **ForeignIdentifierAssociationEntityName** und **ForeignIdentifierAssociationName** vorhanden sein. Der Standardwert des Attributs ist der Namespace der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. </span><span class="sxs-lookup"><span data-stu-id="dc651-p169">The namespace of the **Entity** that contains the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **ForeignIdentifierAssociationEntityName** and **ForeignIdentifierAssociationName** attributes must also be present. The default value of this attribute is the namespace of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="dc651-1671">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1671">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1672">**AssociatedFilter**</span><span class="sxs-lookup"><span data-stu-id="dc651-1672">**AssociatedFilter**</span></span> <br/> |<span data-ttu-id="dc651-1673">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1673">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p170"> Der Name für einen **FilterDescriptor**, der dem **TypeDescriptor** zugeordnet ist. Wenn der **TypeDescriptor** nicht einem **FilterDescriptor** zugeordnet ist, darf das Attribut nicht vorhanden sein. </span><span class="sxs-lookup"><span data-stu-id="dc651-p170">The name of a **FilterDescriptor** that is associated with the **TypeDescriptor**. If the **TypeDescriptor** is not associated with a **FilterDescriptor** this attribute must not be present. </span></span><br/> <span data-ttu-id="dc651-1676">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1676">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1677">**IsCollection**</span><span class="sxs-lookup"><span data-stu-id="dc651-1677">**IsCollection**</span></span> <br/> |<span data-ttu-id="dc651-1678">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1678">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1679">Gibt an, ob der **TypeDescriptor** eine einzelne Datenstruktur oder eine Auflistung von Datenstrukturen darstellt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1679">Specifies whether the **TypeDescriptor** represents a single data structure or a collection of data structures.</span></span> <br/> <span data-ttu-id="dc651-1680">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1680">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1681">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1681">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1682">**ReadOnly**</span><span class="sxs-lookup"><span data-stu-id="dc651-1682">**ReadOnly**</span></span> <br/> |<span data-ttu-id="dc651-1683">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1683">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1684">Gibt an, ob die Daten, die von der Datenstruktur gespeichert werden, die durch den **TypeDescriptor** dargestellt wird, geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc651-1684">Specifies whether the data stored by the data structure represented by the **TypeDescriptor** can be modified. This attribute must not be specified if the value of the Direction attribute of the Parameter that contains the TypeDescriptor is "In".</span></span> <span data-ttu-id="dc651-1685">Dieses Attribut muss nicht angegeben werden, wenn der Wert des **Direction**-Attributs des **Parameters**, der den **TypeDescriptor** enthält, „In“ ist.</span><span class="sxs-lookup"><span data-stu-id="dc651-1685">This attribute must not be specified if the value of the **Direction** attribute of the **Parameter** that contains the **TypeDescriptor** is "In".</span></span> <br/> <span data-ttu-id="dc651-1686">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1686">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1687">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1687">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1688">**CreatorField**</span><span class="sxs-lookup"><span data-stu-id="dc651-1688">**CreatorField**</span></span> <br/> |<span data-ttu-id="dc651-1689">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1689">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1690">Gibt an, ob der **TypeDescriptor** ein Feld für **MethodInstances** vom Typ **Creator** darstellt, die in der **Method** enthalten sind, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält.</span><span class="sxs-lookup"><span data-stu-id="dc651-1690">Specifies whether the **TypeDescriptor** represents a field for **MethodInstances** of type **Creator** that are contained by the **Method** that contains the **Parameter** containing the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="dc651-1691">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1691">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1692">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1692">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1693">**UpdaterField**</span><span class="sxs-lookup"><span data-stu-id="dc651-1693">**UpdaterField**</span></span> <br/> |<span data-ttu-id="dc651-1694">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1694">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p172"> Gibt an, ob der **TypeDescriptor** ein Feld für **MethodInstances** vom Typ **Updater** darstellt, die in der **Method** enthalten sind, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. Wenn das Attribut angegeben ist, darf kein **PreUpdaterField**-Attribut angegeben werden. </span><span class="sxs-lookup"><span data-stu-id="dc651-p172">Specifies whether the **TypeDescriptor** represents a field for **MethodInstances** of type **Updater** that are contained by the **Method** that contains the **Parameter** containing the **TypeDescriptor**. When this attribute is specified, a **PreUpdaterField** attribute must not be specified. </span></span><br/> <span data-ttu-id="dc651-1697">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1697">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1698">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1698">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1699">**PreUpdaterField**</span><span class="sxs-lookup"><span data-stu-id="dc651-1699">**PreUpdaterField**</span></span> <br/> |<span data-ttu-id="dc651-1700">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1700">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p173"> Gibt an, ob in der durch den **TypeDescriptor** dargestellten Datenstruktur der letzte Wert gespeichert wird, der vom externen System für ein Feld für **MethodInstances** vom Typ **Updater** empfangen wird. Wenn das Attribut angegeben ist, darf kein **UpdaterField**-Attribut angegeben werden. </span><span class="sxs-lookup"><span data-stu-id="dc651-p173">Specifies whether data structure represented by the **TypeDescriptor** stores the latest data value received from the external system of a field for **MethodInstances** of type **Updater**. When this attribute is specified, a **UpdaterField** attribute must not be specified. </span></span><br/> <span data-ttu-id="dc651-1703">Standardwert: **false**</span><span class="sxs-lookup"><span data-stu-id="dc651-1703">Default value: **false**</span></span> <br/> <span data-ttu-id="dc651-1704">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1704">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1705">**Significant**</span><span class="sxs-lookup"><span data-stu-id="dc651-1705">**Significant**</span></span> <br/> |<span data-ttu-id="dc651-1706">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1706">Optional.</span></span>  <br/> <span data-ttu-id="dc651-p174"> Gibt an, ob in der durch diesen **TypeDescriptor** dargestellten Datenstruktur gespeicherte Werte bei der Berechnung eines Hashcodes oder beim Vergleichen von in den Datenstrukturen gespeicherten Werten enthalten sind. Beispielsweise wird ein **TypeDescriptor**, der den Nachnamen eines Kunden darstellt, berücksichtigt, wenn ermittelt wird, ob ein Datensatz geändert wurde, und ist daher signifikant. Der **TypeDescriptor**, der das Datum der letzten Änderung des Kundendatensatzes darstellt, wird normalerweise nicht berücksichtigt, wenn ermittelt wird, ob ein Datensatz geändert wurde, und ist daher nicht signifikant. </span><span class="sxs-lookup"><span data-stu-id="dc651-p174">Specifies whether values stored by the data structure represented by this **TypeDescriptor** are included in calculating a hash code or comparing values stored in the data structures. For example, a **TypeDescriptor** representing a customer's last name is taken into account when determining whether a record has been modified, and so it is significant, whereas the **TypeDescriptor** representing the date on which the customer record is last modified typically is not taken into account to determine whether a record has been modified, and so it is not significant. </span></span><br/> <span data-ttu-id="dc651-1709">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1709">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1710">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1710">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="dc651-1711">**Name**</span><span class="sxs-lookup"><span data-stu-id="dc651-1711">**Name**</span></span> <br/> |<span data-ttu-id="dc651-1712">Erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dc651-1712">Required.</span></span>  <br/> <span data-ttu-id="dc651-1713">Der Name für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1713">The name of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="dc651-1714">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1714">Attribute type: **String**</span></span> <br/> <span data-ttu-id="dc651-1715">**Hinweis:** Der Name für einen **TypeDescriptor** sollte nicht die Sonderzeichen "/" (Schrägstrich), "." (Punkt) oder "[" (öffnende eckige Klammer) enthalten.</span><span class="sxs-lookup"><span data-stu-id="dc651-1715">The name of a **TypeDescriptor** should not contain the special characters for forward slash ("/"), period ("."), or opening bracket ("[").</span></span>          |
|<span data-ttu-id="dc651-1716">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="dc651-1716">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="dc651-1717">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1717">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1718">Der Anzeigename für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1718">The display name of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="dc651-1719">Attributtyp: **String**</span><span class="sxs-lookup"><span data-stu-id="dc651-1719">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="dc651-1720">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="dc651-1720">**IsCached**</span></span> <br/> |<span data-ttu-id="dc651-1721">Optional.</span><span class="sxs-lookup"><span data-stu-id="dc651-1721">Optional.</span></span>  <br/> <span data-ttu-id="dc651-1722">Gibt an, ob der **TypeDescriptor** häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc651-1722">Specifies whether the **TypeDescriptor** is used frequently.</span></span> <br/> <span data-ttu-id="dc651-1723">Standardwert: **true**</span><span class="sxs-lookup"><span data-stu-id="dc651-1723">Default value: **true**</span></span> <br/> <span data-ttu-id="dc651-1724">Attributtyp: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="dc651-1724">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="dc651-1725">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1725">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1726">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1726">**Element**</span></span>|<span data-ttu-id="dc651-1727">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1727">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1728">LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1728">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1729">Die lokalisierten Namen für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1729">The localized names of the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1730">Properties-Element in MetadataObject (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1730">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1731">Die Eigenschaften für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1731">The properties of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="dc651-p175"> Wenn die **TypeDescriptor** vom Typ **System.String**ist, kann das **Properties** -Element eine **Property** des Typs **System.Int32** mit dem **Name** -Attribut auf **Size**festgelegt enthalten. Der Wert der **Property** gibt die erwartete maximale Länge der Zeichenfolge des Werts der Datenstruktur, die von diesem **TypeDescriptor**beschrieben. </span><span class="sxs-lookup"><span data-stu-id="dc651-p175">When the **TypeDescriptor** is of type **System.String**, the **Properties** element can contain a **Property** of type **System.Int32** with the **Name** attribute set to **Size**. The value of the **Property** specifies the expected maximum string length of the value of the data structure described by this **TypeDescriptor**.  </span></span><br/> |
| [<span data-ttu-id="dc651-1734">Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1734">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1735">Die Regeln für die in der Datenstruktur gespeicherten Daten, die durch den **TypeDescriptor** dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="dc651-1735">The rules for the data stored by the data structure represented by the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1736">DefaultValues-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1736">DefaultValues Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1737">Die Standardwerte für den **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="dc651-1737">The default values of the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="dc651-1738">TypeDescriptors-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1738">TypeDescriptors Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1739">Die untergeordneten **TypeDescriptors** des **TypeDescriptor**s.</span><span class="sxs-lookup"><span data-stu-id="dc651-1739">The child **TypeDescriptors** of the **TypeDescriptor**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1740">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1740">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1741">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1741">**Element**</span></span>|<span data-ttu-id="dc651-1742">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1742">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1743">TypeDescriptors-Element in "TypeDescriptor" (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1743">TypeDescriptors Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx)||
   

## <a name="typedescriptors-element"></a><span data-ttu-id="dc651-1744">TypeDescriptors-Element</span><span class="sxs-lookup"><span data-stu-id="dc651-1744">TypeDescriptors element</span></span>
<span data-ttu-id="dc651-1745"><a name="bkmk_TypeDescriptors"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1745"></span></span>

<span data-ttu-id="dc651-1746">Gibt eine Liste von **TypeDescriptors** eines übergeordneten TypeDescriptors an.</span><span class="sxs-lookup"><span data-stu-id="dc651-1746">Specifies a list of **TypeDescriptors** of a parent TypeDescriptor.</span></span>
  
    
    
 <span data-ttu-id="dc651-1747">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="dc651-1747">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="dc651-1748">**Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="dc651-1748">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<TypeDescriptors></TypeDescriptors>
```

<span data-ttu-id="dc651-1749">In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.</span><span class="sxs-lookup"><span data-stu-id="dc651-1749">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="dc651-1750">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dc651-1750">**Attributes**</span></span>
  
    
    
<span data-ttu-id="dc651-1751">Keine</span><span class="sxs-lookup"><span data-stu-id="dc651-1751">None</span></span>
  
    
    
 <span data-ttu-id="dc651-1752">**Untergeordnete Elemente**</span><span class="sxs-lookup"><span data-stu-id="dc651-1752">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="dc651-1753">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1753">**Element**</span></span>|<span data-ttu-id="dc651-1754">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1754">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1755">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1755">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="dc651-1756">Ein **TypeDescriptor**-Objekt.</span><span class="sxs-lookup"><span data-stu-id="dc651-1756">A **TypeDescriptor**.</span></span>  <br/> |
   
 <span data-ttu-id="dc651-1757">**Übergeordnetes Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1757">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="dc651-1758">**Element**</span><span class="sxs-lookup"><span data-stu-id="dc651-1758">**Element**</span></span>|<span data-ttu-id="dc651-1759">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dc651-1759">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="dc651-1760">TypeDescriptor-Element (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="dc651-1760">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="dc651-1761">TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="dc651-1761">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
   

## <a name="additional-resources"></a><span data-ttu-id="dc651-1762">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dc651-1762">Additional resources</span></span>
<span data-ttu-id="dc651-1763"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="dc651-1763"></span></span>


-  [<span data-ttu-id="dc651-1764">Änderungen in der BDC-Modell-Schema für SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1764">Changes in the BDC model schema for SharePoint</span></span>](changes-in-the-bdc-model-schema-for-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1765">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1765">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1766">Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1766">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1767">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1767">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1768">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1768">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1769">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1769">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="dc651-1770">Business Connectivity Services-Programmierreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc651-1770">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
