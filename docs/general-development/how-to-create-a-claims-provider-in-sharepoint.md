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
# <a name="how-to-create-a-claims-provider-in-sharepoint"></a>Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint
In diesem Artikel erfahren Sie, wie ein SharePoint-Anspruchsanbieter erstellt und implementiert wird, der die Voraussetzungen für die Steigerung von Ansprüchen und die Auswahl von Ansprüchen erfüllt. Ein Forderungsanbieter gibt Forderungen heraus und packt Forderungen in Sicherheitstoken. Ein Forderungsanbieter erfüllt zwei Aufgaben: Erweiterung und Auswahl.
  
    
    

Die anspruchserweiterung kann eine Anwendung zusätzliche Ansprüchen Token des Benutzers. Beispielsweise kann mit Windows-basierten Log-in der Active Directory-Verzeichnisdienst aller Sicherheitsgruppen des Benutzers in Windows-Token des Benutzers ergänzen. Mit anspruchsbasierten anmelden kann eine Anwendung Customer Relationship Management (CRM) Rollen aus einer Datenbank CRM ergänzen. Da Sie diese Ansprüche im Token des Benutzers, können Ressourcen gegen diese Ansprüche autorisiert werden. D. h., werden diese Ansprüche verwendet, um festzustellen, ob ein bestimmter Benutzer Zugriff auf bestimmte Ressourcen hat. Ansprüche können im Auswahlsteuerelement über anspruchsauswahl Personen angezeigt werden. Anspruchsauswahl ermöglicht Ansprüche Offenlegen eine Anwendung in der Personenauswahl, beispielsweise beim Konfigurieren der Sicherheits einer SharePoint-Website oder die SharePoint-Dienst. Diese Funktionalität können Sie suchen, auflösen und benutzerfreundliche Anzeige von Ansprüchen bereitstellen.
  
    
    


> **Hinweis:** Eine Personenauswahl mit Funktionen zur Auswahl von Ansprüchen wird manchmal auch als Anspruchsauswahl bezeichnet. Weitere Informationen finden Sie unter [Planen für die Personenauswahl und für Anspruchsanbieter](http://technet.microsoft.com/en-us/library/gg602063.aspx). 
  
    
    

Zum Schreiben eines Anspruchsanbieters erstellen Sie im ersten Schritt eine Klasse, die von der Klasse **SPClaimProvider** abgeleitet wird.
> **Tipp:** Ein Codebeispiel und weitere Informationen zur Klasse **SPClaimProvider** und ihren Membern finden Sie unter [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx). Exemplarische Vorgehensweisen, Tipps und Codebeispiele finden Sie unter [Ansprüche und Sicherheit: Technische Artikel](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx) auf MSDN. 
  
    
    


## <a name="required-implementations"></a>Erforderliche Implementierungen
<a name="SP15_HowToCreateClaimsProvider_ReqImplementations"> </a>

Es folgen die erforderlichen Methoden und Eigenschaften zum Schreiben eines Forderungsanbieters.
  
    
    

### <a name="required"></a>Erforderlich

Die folgende  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) -Eigenschaft ist erforderlich. Der Name muss in der Farm eindeutig sein.
  
    
    

```cs

public abstract String Name
      
```


### <a name="required-for-claims-picker"></a>Erforderlich für Anspruchsauswahl

Ansprüche können im Personenauswahl-Steuerelement durch Auswahl von Ansprüchen angezeigt werden. Die folgenden Methoden in der Klasse [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) sind erforderliche Methoden, wenn Sie die Anspruchsauswahl im Personenauswahl-Steuerelement implementieren möchten.
  
    
    

```cs

protected abstract void FillSchema(SPProviderSchema schema);
     protected abstract void FillClaimTypes(List<String> claimTypes);
     protected abstract void FillClaimValueTypes(List<String> claimValueTypes);
     protected abstract void FillEntityTypes(List<String> entityTypes);

```


### <a name="required-for-claims-augmentation"></a>Erforderlich für Anspruchsaugmentation

Wenn Sie zusätzliche Forderungen in das Sicherheitstoken eines Benutzers einschließen, erweitern Sie Forderungen. Wenn Sie Forderungen erweitern möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.
  
    
    

```cs

public abstract bool SupportsEntityInformation
      protected abstract void FillClaimsForEntity(Uri context, SPClaim entity, List<SPClaim> claims);

```


### <a name="required-for-displaying-hierarchy-on-the-left-pane-of-the-claims-picker"></a>Erforderlich zum Anzeigen der Hierarchie im linken Bereich der Forderungsauswahl

Wenn Sie die Hierarchie im linken Bereich der Forderungsauswahl anzeigen möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.
  
    
    

```cs

public abstract bool SupportsHierarchy
     protected abstract void FillHierarchy(Uri context, String[] entityTypes, String hierarchyNodeID, int numberOfLevels, bool includeEntityData, SPProviderHierarchyTree hierarchy);

```


### <a name="required-for-resolving-claims-in-the-type-in-control-of-the-claims-picker"></a>Erforderlich für das Auflösen von Forderungen im Eingabesteuerelement der Forderungsauswahl

Wenn Sie Forderungen mithilfe des Eingabesteuerelements der Forderungsauswahl auflösen möchten, müssen Sie die folgenden Methoden in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.
  
    
    

```cs

public abstract bool SupportsResolve
     protected abstract void FillResolve(Uri context, String[] entityTypes, String resolveInput, List<PickerEntity> resolved);
     protected abstract void FillResolve(Uri context, String[] entityTypes, SPClaim resolveInput, List<PickerEntity> resolved);

```


### <a name="required-for-searching-for-claims-in-the-claims-picker"></a>Erforderlich für die Suche nach Forderungen in der forderungsauswahl

Wenn Sie nach Forderungen in der Forderungsauswahl suchen möchten, müssen Sie die folgende Eigenschaft und Methode in der  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) -Klasse implementieren.
  
    
    

```cs

public abstract bool SupportsSearch
     protected abstract void FillSearch(Uri context, String[] entityTypes, String searchPattern, String hierarchyNodeID, int maxCount, SPProviderHierarchyTree searchTree);

```


## <a name="useful-helper-method"></a>Nützliche Hilfsmethode
<a name="SP15_HowToCreateClaimsProvider_UsefulHelperMethod"> </a>

Sie können auch eine Hilfsmethode implementieren, die Sie beim Erstellen von  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) -Objekten unterstützt.
  
    
    

### <a name="useful-helper-method-for-creating-spclaim-objects"></a>Nützliche Hilfsmethode zum Erstellen von SPClaim-Objekten

Die folgende Hilfsmethode können Sie implementieren, damit Sie sie beim Erstellen von  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) -Objekten unterstützt.
  
    
    

```cs

protected SPClaim CreateClaim(String claimType, String value, String valueType)
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_HowToCreateClaimsProvider_AdditionalResources"> </a>


-  [Anspruchsbasierte Identität in SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md)
    
  
-  [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Vorgehensweise: POST eines anspruchsanbieters in SharePoint](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

