---
title: Vorgehensweise Erstellen ein anspruchsanbieters in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8f3228ca-57fd-4253-a07d-abeb63298c58
ms.openlocfilehash: 12d42c832cfe9741306adf78ba3d1bc4a708ac5d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-claims-provider-in-sharepoint"></a><span data-ttu-id="e126a-102">Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e126a-102">How to: Create a claims provider in SharePoint</span></span>
<span data-ttu-id="e126a-p101">In diesem Artikel erfahren Sie, wie ein SharePoint-Anspruchsanbieter erstellt und implementiert wird, der die Voraussetzungen für die Steigerung von Ansprüchen und die Auswahl von Ansprüchen erfüllt. Ein Forderungsanbieter gibt Forderungen heraus und packt Forderungen in Sicherheitstoken. Ein Forderungsanbieter erfüllt zwei Aufgaben: Erweiterung und Auswahl.</span><span class="sxs-lookup"><span data-stu-id="e126a-p101">Learn how to create and implement a SharePoint claims provider that fulfills the requirements for claims augmentation and claims picking. A claims provider issues claims and packages claims into security tokens. A claims provider has two roles: augmentation and picking.</span></span>
  
    
    

<span data-ttu-id="e126a-p102">Die anspruchserweiterung kann eine Anwendung zusätzliche Ansprüchen Token des Benutzers. Beispielsweise kann mit Windows-basierten Log-in der Active Directory-Verzeichnisdienst aller Sicherheitsgruppen des Benutzers in Windows-Token des Benutzers ergänzen. Mit anspruchsbasierten anmelden kann eine Anwendung Customer Relationship Management (CRM) Rollen aus einer Datenbank CRM ergänzen. Da Sie diese Ansprüche im Token des Benutzers, können Ressourcen gegen diese Ansprüche autorisiert werden. D. h., werden diese Ansprüche verwendet, um festzustellen, ob ein bestimmter Benutzer Zugriff auf bestimmte Ressourcen hat. Ansprüche können im Auswahlsteuerelement über anspruchsauswahl Personen angezeigt werden. Anspruchsauswahl ermöglicht Ansprüche Offenlegen eine Anwendung in der Personenauswahl, beispielsweise beim Konfigurieren der Sicherheits einer SharePoint-Website oder die SharePoint-Dienst. Diese Funktionalität können Sie suchen, auflösen und benutzerfreundliche Anzeige von Ansprüchen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e126a-p102">Claims augmentation enables an application to augment additional claims into the user's token. For example, with Windows-based log-in, the Active Directory directory service can augment all of a user's security groups into the user's Windows token. With claims-based log-in, a customer relationship management (CRM) application can augment roles from a CRM database. By having these claims in the user's token, resources can be authorized against these claims. That is, these claims are used to determine whether a particular user has access to specific resources. Claims can be displayed in the people picker control through claims picking. Claims picking enables an application to surface claims in the people picker, for example, when configuring the security of a SharePoint site or SharePoint service. This functionality enables you to provide search, resolve, and friendly display of claims.</span></span>
  
    
    


> <span data-ttu-id="e126a-114">**Hinweis:** Eine Personenauswahl mit Funktionen zur Auswahl von Ansprüchen wird manchmal auch als Anspruchsauswahl bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="e126a-114">**Note** A people picker with claims picking functionality is sometimes referred to as a claims picker. For more information, see  People picker and claims provider planning.</span></span> <span data-ttu-id="e126a-115">Weitere Informationen finden Sie unter [Planen für die Personenauswahl und für Anspruchsanbieter](http://technet.microsoft.com/en-us/library/gg602063.aspx).</span><span class="sxs-lookup"><span data-stu-id="e126a-115">For more information, see  [People picker and claims provider planning](http://technet.microsoft.com/en-us/library/gg602063.aspx).</span></span> 
  
    
    

<span data-ttu-id="e126a-116">Zum Schreiben eines Anspruchsanbieters erstellen Sie im ersten Schritt eine Klasse, die von der Klasse **SPClaimProvider** abgeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="e126a-116">To write a claims provider, your first step is to create a class that derives from the **SPClaimProvider** class.</span></span>
> <span data-ttu-id="e126a-117">**Tipp:** Ein Codebeispiel und weitere Informationen zur Klasse **SPClaimProvider** und ihren Membern finden Sie unter [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx).</span><span class="sxs-lookup"><span data-stu-id="e126a-117">For a code example and more information about the **SPClaimProvider** class and its members, see [T:Microsoft.SharePoint.Administration.Claims.SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx).</span></span> <span data-ttu-id="e126a-118">Exemplarische Vorgehensweisen, Tipps und Codebeispiele finden Sie unter [Ansprüche und Sicherheit: Technische Artikel](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx) auf MSDN.</span><span class="sxs-lookup"><span data-stu-id="e126a-118">TIP For a code example and more information about the SPClaimProvider class and its members, see SPClaimProvider . For walkthroughs, tips, and code samples, see [Claims and Security: Technical articles and code samples on MSDN](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="required-implementations"></a><span data-ttu-id="e126a-119">Erforderliche Implementierungen</span><span class="sxs-lookup"><span data-stu-id="e126a-119">Required implementations</span></span>
<span data-ttu-id="e126a-120"><a name="SP15_HowToCreateClaimsProvider_ReqImplementations"> </a></span><span class="sxs-lookup"><span data-stu-id="e126a-120"></span></span>

<span data-ttu-id="e126a-121">Es folgen die erforderlichen Methoden und Eigenschaften zum Schreiben eines Forderungsanbieters.</span><span class="sxs-lookup"><span data-stu-id="e126a-121">The following are required methods and properties when writing a claims provider.</span></span>
  
    
    

### <a name="required"></a><span data-ttu-id="e126a-122">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="e126a-122">Required</span></span>

<span data-ttu-id="e126a-p105">Die folgende  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) -Eigenschaft ist erforderlich. Der Name muss in der Farm eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="e126a-p105">The following  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) property is a required property. The name should be unique across the farm.</span></span>
  
    
    

```cs

public abstract String Name
      
```


### <a name="required-for-claims-picker"></a><span data-ttu-id="e126a-125">Erforderlich für Anspruchsauswahl</span><span class="sxs-lookup"><span data-stu-id="e126a-125">Required for claims picker</span></span>

<span data-ttu-id="e126a-126">Ansprüche können im Personenauswahl-Steuerelement durch Auswahl von Ansprüchen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="e126a-126">Claims can be displayed in the people picker control through claims picking.</span></span> <span data-ttu-id="e126a-127">Die folgenden Methoden in der Klasse [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) sind erforderliche Methoden, wenn Sie die Anspruchsauswahl im Personenauswahl-Steuerelement implementieren möchten.</span><span class="sxs-lookup"><span data-stu-id="e126a-127">Claims can be displayed in the People Picker control through claims picking. The following methods in the [T:Microsoft.SharePoint.Administration.Claims.SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class are required methods if you want to implement claim picking in the People Picker control.</span></span>
  
    
    

```cs

protected abstract void FillSchema(SPProviderSchema schema);
     protected abstract void FillClaimTypes(List<String> claimTypes);
     protected abstract void FillClaimValueTypes(List<String> claimValueTypes);
     protected abstract void FillEntityTypes(List<String> entityTypes);

```


### <a name="required-for-claims-augmentation"></a><span data-ttu-id="e126a-128">Erforderlich für Anspruchsaugmentation</span><span class="sxs-lookup"><span data-stu-id="e126a-128">Required for claims augmentation</span></span>

<span data-ttu-id="e126a-p107">Wenn Sie zusätzliche Forderungen in das Sicherheitstoken eines Benutzers einschließen, erweitern Sie Forderungen. Wenn Sie Forderungen erweitern möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.</span><span class="sxs-lookup"><span data-stu-id="e126a-p107">When you include additional claims in a user's security token, you are augmenting claims. If you want to augment claims, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsEntityInformation
      protected abstract void FillClaimsForEntity(Uri context, SPClaim entity, List<SPClaim> claims);

```


### <a name="required-for-displaying-hierarchy-on-the-left-pane-of-the-claims-picker"></a><span data-ttu-id="e126a-131">Erforderlich zum Anzeigen der Hierarchie im linken Bereich der Forderungsauswahl</span><span class="sxs-lookup"><span data-stu-id="e126a-131">Required for displaying hierarchy on the left pane of the claims picker</span></span>

<span data-ttu-id="e126a-132">Wenn Sie die Hierarchie im linken Bereich der Forderungsauswahl anzeigen möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.</span><span class="sxs-lookup"><span data-stu-id="e126a-132">If you want to display hierarchy on the left pane of the claims picker, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsHierarchy
     protected abstract void FillHierarchy(Uri context, String[] entityTypes, String hierarchyNodeID, int numberOfLevels, bool includeEntityData, SPProviderHierarchyTree hierarchy);

```


### <a name="required-for-resolving-claims-in-the-type-in-control-of-the-claims-picker"></a><span data-ttu-id="e126a-133">Erforderlich für das Auflösen von Forderungen im Eingabesteuerelement der Forderungsauswahl</span><span class="sxs-lookup"><span data-stu-id="e126a-133">Required for resolving claims in the type-in control of the claims picker</span></span>

<span data-ttu-id="e126a-134">Wenn Sie Forderungen mithilfe des Eingabesteuerelements der Forderungsauswahl auflösen möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.</span><span class="sxs-lookup"><span data-stu-id="e126a-134">If you want to be able to resolve claims by using the type-in control of the claims picker, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsResolve
     protected abstract void FillResolve(Uri context, String[] entityTypes, String resolveInput, List<PickerEntity> resolved);
     protected abstract void FillResolve(Uri context, String[] entityTypes, SPClaim resolveInput, List<PickerEntity> resolved);

```


### <a name="required-for-searching-for-claims-in-the-claims-picker"></a><span data-ttu-id="e126a-135">Erforderlich für die Suche nach Forderungen in der forderungsauswahl</span><span class="sxs-lookup"><span data-stu-id="e126a-135">Required for searching for claims in the claims picker</span></span>

<span data-ttu-id="e126a-136">Wenn Sie nach Forderungen in der Forderungsauswahl suchen möchten, müssen Sie die folgende Eigenschaft und Methode in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.</span><span class="sxs-lookup"><span data-stu-id="e126a-136">If you want to be able to search for claims in the claims picker, you must implement the following property and method in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsSearch
     protected abstract void FillSearch(Uri context, String[] entityTypes, String searchPattern, String hierarchyNodeID, int maxCount, SPProviderHierarchyTree searchTree);

```


## <a name="useful-helper-method"></a><span data-ttu-id="e126a-137">Nützliche Hilfsmethode</span><span class="sxs-lookup"><span data-stu-id="e126a-137">Useful helper method</span></span>
<span data-ttu-id="e126a-138"><a name="SP15_HowToCreateClaimsProvider_UsefulHelperMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="e126a-138"></span></span>

<span data-ttu-id="e126a-139">Sie können auch eine Hilfsmethode implementieren, die Sie beim Erstellen von  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) -Objekten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e126a-139">You can also implement a helper method to help you create  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) objects.</span></span>
  
    
    

### <a name="useful-helper-method-for-creating-spclaim-objects"></a><span data-ttu-id="e126a-140">Nützliche Hilfsmethode zum Erstellen von SPClaim-Objekten</span><span class="sxs-lookup"><span data-stu-id="e126a-140">Useful helper method for creating SPClaim objects</span></span>

<span data-ttu-id="e126a-141">Die folgende Hilfsmethode können Sie implementieren, damit Sie sie beim Erstellen von  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) -Objekten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e126a-141">The following is a helper method that you can implement to help you create  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) objects.</span></span>
  
    
    

```cs

protected SPClaim CreateClaim(String claimType, String value, String valueType)
```


## <a name="additional-resources"></a><span data-ttu-id="e126a-142">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e126a-142">Additional resources</span></span>
<span data-ttu-id="e126a-143"><a name="SP15_HowToCreateClaimsProvider_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="e126a-143"></span></span>


-  [<span data-ttu-id="e126a-144">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e126a-144">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e126a-145">Eingehende Ansprüche: Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="e126a-145">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="e126a-146">Anspruchsanbieter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e126a-146">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e126a-147">Vorgehensweise: POST eines anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e126a-147">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

