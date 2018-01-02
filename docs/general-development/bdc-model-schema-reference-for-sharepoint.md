---
title: "BDC-Modell-Schemareferenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 979a5ffc-f033-4e72-b2d1-11d8cb1b294a
ms.openlocfilehash: dd78f6a347894eff60149df672d251cfa4c26bd7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="bdc-model-schema-reference-for-sharepoint"></a>BDC-Modell-Schemareferenz für SharePoint
Enthält die Referenzdokumentation für das BDC-Modell-Schema (BDCMetadata.xsd), die Sie zum Erstellen von externer Inhaltstypen in SharePoint verwenden können. [BDCMetadata.xsd](http://schemas.microsoft.com/windows/2007/BusinessDataCatalog)
  
    
    


## <a name="accesscontrolentry-element"></a>AccessControlEntry (Element)
<a name="bkmk_AccessControlEntry"> </a>

Enthält einen Zugriffssteuerungseintrag (ACE), der Zugriffsrechte für das übergeordnete Element angibt.
  
    
    
Weitere Informationen zu Business Connectivity Services und zur Sicherheit finden Sie unter  [Business Connectivity Services-Sicherheit (Übersicht)](http://technet.microsoft.com/de-DE/library/ee661734%28office.14%29.aspx).
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML

<AccessControlEntry Principal = "String"> </AccessControlEntry>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Direktor  <br/> |Erforderlich.  <br/> Der Name des Sicherheitsprinzipals, der diesen ACE aufweist.  <br/> Attributtyp: **String** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Right-Element in AccessControlEntry (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a2e4bd6c-2306-b657-7290-cc9c9b262911%28Office.15%29.aspx) <br/> |Ein **Right**-Element, das die für den Sicherheitsprinzipal verfügbaren Berechtigungen angibt. <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Die Zugriffssteuerungsliste (Access Control List, ACL), die diesen ACE enthält.  <br/> |
   

## <a name="accesscontrollist-element"></a>AccessControlList (Element)
<a name="bkmk_AccessControlList"> </a>

Gibt eine Zugriffssteuerungsliste (Access Control List, ACL) für das übergeordnete Element an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<AccessControlList></AccessControlList>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [AccessControlEntry-Element in "AccessControlList" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |Ein Zugriffssteuerungseintrag (Access Control Entry, ACE).  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Model"-Element ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |Ein Modell, externe Inhaltstypen in einer Geschäftsanwendung enthält.  <br/> |
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Die in dem Modell enthaltenen LobSystems.  <br/> |
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Ein externer Inhaltstyp.  <br/> |
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Eine Methode eines externen Inhaltstyps.  <br/> |
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |Eine Zuordnung.  <br/> |
| [MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |Eine Methodeninstanz eines externen Inhaltstyps.  <br/> |
   

## <a name="action-element"></a>Action-Element
<a name="bkmk_Action"> </a>

Gibt eine von einem externen Inhaltstyp unterstützte Aktion an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    
Aktionen schließen die Lücke zwischen SharePoint und Office 2013 und einem externen System-Benutzeroberfläche durch eine Verknüpfung zurück zum externen System bereitstellen. 
  
    
    
Standardmäßig enthält die Business Data Connectivity (BDC)-Dienst Aktionen wie **View Item**, **Edit Item**und **Delete Item**, nachdem Sie diese Vorgänge im Modell BDC modellieren. Zusätzlich zu diesen Standardaktionen können Sie Aktionen für andere Funktionen erstellen, den, die Sie Ihren externen Inhaltstyp zuordnen möchten. Sie können beispielsweise Aktionen verwenden, um einfache Aktionen auszuführen wie das Senden von e-Mail-Nachrichten an einen Kunden in den externen Inhaltstyp Customer oder einer Kunden-Homepage in einem Browser öffnen.
  
    
    
Aktionen werden mit einem externen Inhaltstyp übertragen. Das bedeutet, dass eine Aktion, nachdem Sie sie für einen externen Inhaltstyp definiert haben, überall angezeigt wird, wo dieser externe Inhaltstyp angezeigt wird - ob in einer externen Liste, in einem Geschäftsdaten-Webpart oder in einer Spalte mit externen Daten. 
  
    
    



```XML
<Action Position = "Integer" IsOpenedInNewWindow = "Boolean" Url = "String" ImageUrl = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Action>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Position** <br/> |Erforderlich.  <br/> Die vorgeschlagene Position dieser Aktion unter den anderen Aktionen dieses externen Inhaltstyps.  <br/> Attributtyp: **Integer** <br/> |
|**IsOpenedInNewWindow** <br/> |Optional.  <br/> Gibt an, ob die Ergebnisse der Ausführung einer Aktion in einem neuen Fenster auf der Benutzeroberfläche angezeigt werden.  <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**Url** <br/> |Erforderlich.  <br/> Die URL, zu wechseln, wenn die Aktion aufgerufen wird. Die URL-Zeichenfolge ist eine Formatzeichenfolge .NET Framework. Jede-Formatspezifizierer (beispielsweise ' {0} ') entspricht einem **Action** -Parameter.<br/> Attributtyp: **String** <br/> |
|**ImageUrl** <br/> |Optional.  <br/> Der absolute oder relative Pfad zu dem Symbolbild für die Aktion. Das Symbolbild sollte ein Format von 16 x 16 Pixeln aufweisen.<br/> Attributtyp: **String** <br/> |
|**Name** <br/> |Erforderlich.  <br/> Der Name dieser Aktion.  <br/> Attributtyp: **String** <br/> |
|**DefaultDisplayName** <br/> |Optional.  <br/> Der Standardanzeigename für diese Aktion.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/> Gibt an, ob diese Aktion häufig verwendet wird. Wird von der BDC-Clientlaufzeit zum Zwischenspeichern dieser Aktion verwendet.<br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen der Aktion.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften der Aktion.  <br/> |
| ["ActionParameters"-Element in Aktion ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |Die Parameter der Aktion.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Actions-Element in "Entity" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |Die Liste der Aktionen eines externen Inhaltstyps.  <br/> |
   

## <a name="actionparameter-element"></a>ActionParameter-Element
<a name="bkmk_ActionParameter"> </a>

Gibt die Parameter einer URL-basierten Aktion an. Hiermit wird definiert, wie die URL einer Aktion mit **EntityInstance**-spezifischen Daten parametrisiert werden soll.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    
Das URL-Attribut einer URL-basierten kann Parameter mithilfe des **ActionParameter**-Elements empfangen.
  
    
    

> **Wichtig:**
> **ActionParameters** können entweder Bezeichnerwerte oder Werte darstellen, die **TypeDescriptors** in einem **SpecificFinder** der **Entity** entsprechen. Der **ActionParameter** stellt einen Bezeichnerwert dar, wenn die **IdOrdinal**-Eigenschaft vorhanden ist. Der Wert der Eigenschaft gibt den Index des Bezeichners an, dessen Wert dieser **ActionParameter** darstellt. Wenn die **IdOrdinal**-Eigenschaft nicht angegeben ist, stellt der **ActionParameter** einen **TypeDescriptor** dar, und das **Name**-Attribut gibt an, welcher Typdeskriptor dargestellt wird. Das **Name**-Attribut wird als **gepunkteter Pfad** angegeben. 
  
    
    

Das **ActionParameter**-Element akzeptiert die folgende Eigenschaft.
  
    
    

> **Wichtig:** Bei Eigenschaften wird die Groß-/Kleinschreibung beachtet. 
  
    
    


**Eigenschaften**


|**Eigenschaft**|**Typ**|**Beschreibung**|**Erforderlich**|**Standardwert**|**Grenzwerte/akzeptierte Werte**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|**IdOrdinal** <br/> |**System.Int32** <br/> |Gibt an, ob **ActionParameter** einen Bezeichner anstelle eines Felds darstellt. <br/> |Optional  <br/> |||
   



```XML
<ActionParameter Index = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </ActionParameter>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Index** <br/> |Erforderlich.  <br/> Ein Ordnungszahlenattribut, das die Position dieses **ActionParameter**-Elements unter anderen **ActionParameters** in der URL angibt. <br/> Attributtyp: **Integer** <br/> |
|**Name** <br/> |Erforderlich.  <br/> Der Name des **ActionParameter**-Parameters.  <br/> Attributtyp: **String** <br/> |
|**DefaultDisplayName** <br/> |Optional.  <br/> Der Standardanzeigename für **ActionParameter**.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/>  Gibt an, ob dieses **ActionParameter**-Element häufig verwendet wird. Dieses Attribut wird von der BDC-Client-Laufzeitumgebung zum Zwischenspeichern dieses **Action**-Elements verwendet. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen für **ActionParameter**.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des **ActionParameter**-Parameters.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["ActionParameters"-Element in Aktion ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |Das **ActionParameters**-Element, das diesen **ActionParameter**-Parameter enthält.  <br/> |
   

## <a name="actionparameters-element"></a>"ActionParameters"-Element
<a name="bkmk_ActionParameters"> </a>

Gibt eine Liste von **ActionParameters** für eine Aktion an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<ActionParameters></ActionParameters>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine.
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> |Ein **ActionParameter**.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Action"-Element in "Actions" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |Die **Action**, zu dem diese **ActionParameters** gehören. <br/> |
   

## <a name="actions-element"></a>"Actions"-Element
<a name="bkmk_Actions"> </a>

Gibt eine Liste mit Aktionen eines externen Inhaltstyps an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Actions></Actions>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Action"-Element in "Actions" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |Eine Aktion eines externen Inhaltstyps.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Der externe Inhaltstyp, dem diese Aktionen angehören.  <br/> |
   

## <a name="association-element"></a>"Association"-Element
<a name="bkmk_Association"> </a>

Das Association-Element verknüpft verwandte externe Inhaltstypen in einem System. Angenommen, ein Kunde zugeordnet ist einen Auftrag im System AdventureWorks: ein Kunde macht Aufträge. Eine Zuordnung enthält dann Zeiger auf die Quell- und Ziel externe Inhaltstypen und einen Zeiger auf die Geschäftslogik (ein **MethodInstance** -Objekt), die einen Client zum Abrufen des externen zielinhaltstyp von der externen quellinhaltstyp ermöglicht. Das Traversieren der ein **Association** ist ein Aufruf der Methode für das externe System.
  
    
    

  
    
    
 **Namespace:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog
  
    
    
 **Schema:** BDCMetadata
  
    
    

> **Wichtig:** Bei Eigenschaften wird die Groß-/Kleinschreibung beachtet. 
  
    
    


**Eigenschaften**


|**Eigenschaft**|**Typ**|**Beschreibung**|**Erforderlich**|**Standardwert**|**Grenzwerte/akzeptierte Werte**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|**HideOnProfilePage** <br/> |**System.Boolean** <br/> |Gibt an, ob der verwandte externe Inhaltstyp der Profilseite des externen Masterinhaltstyps hinzugefügt werden soll.  <br/> |Optional  <br/> |||
   



```XML
<Association Type = "String" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Association>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Typ** <br/> |Erforderlich.  <br/> Die **MethodInstanceType**, die den Typ der Zuordnung angibt. <br/> In der folgenden Tabelle sind die möglichen Werte für dieses Attribut aufgeführt.  <br/>         <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>AssociationNavigator</p></td><td><p>Die **MethodInstance** ist ein **AssociationNavigator**.</p></td></tr><tr><td><p>Associator</p></td><td><p>Die **MethodInstance** ist ein **Associator**.</p></td></tr><tr><td><p>Disassociator</p></td><td><p>Die **MethodInstance** ist eine **Disassociator**.</p></td></tr><tr><td><p>**BulkAssociatedIdEnumerator**</p></td><td><p>Die **MethodInstance** ist eine **BulkAssociatedIdEnumerator**.</p></td></tr><tr><td><p>**BulkAssociationNavigator**</p></td><td><p>Die **MethodInstance** ist ein **BulkAssociationNavigator**.</p></td></tr></tbody></table>|
|Standard  <br/> |Optional.  <br/>  Gibt an, ob die Zuordnung der Standardwert zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. Wenn es sich bei Festlegung auf **true**, die Zuordnung der Standardwert zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. Wenn auf **false**, die Zuordnung nicht die Standardeinstellung zwischen alle Zuordnungen Freigabe dieses Typs innerhalb der externe Inhaltstyp enthalten ist. <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|ReturnParameterName  <br/> |Optional.  <br/>  Der Name des Parameters, der die **ReturnTypeDescriptor** der Zuordnung enthält. Das **Direction** -Attribut des Parameters muss entweder ",", "INOUT-" oder "Zurück" den Wert enthalten. <br/> Attributtyp: **String** <br/> |
|ReturnTypeDescriptorName  <br/> |Optional.  <br/> Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.<br/> Attributtyp: **String** <br/> |
|ReturnTypeDescriptorLevel  <br/> |Optional.  <br/> Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.<br/> Attributtyp: **Integer** <br/> |
|ReturnTypeDescriptorPath  <br/> |Optional.  <br/> Der gepunktete Pfad des **TypeDescriptors** der Zuordnung.  <br/> Attributtyp: **String** <br/> |
|Name  <br/> |Erforderlich.  <br/> Der Name der Zuordnung.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename für die Zuordnung.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob diese Zuordnung häufig verwendet wird.  <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Das **LocalizedDisplayNames** -Element gibt eine Liste der lokalisierten Namen für die Zuordnung. <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Das Properties-Element gibt die Eigenschaften der Zuordnung an.  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Das **AccessControlList** -Element gibt einen Satz von Zugriffsrechten für die Zuordnung. <br/> |
| [SourceEntity-Element in "Association" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/19fb5f38-4e85-7fb0-2562-281b9a9ffbef%28Office.15%29.aspx) <br/> |Das **SourceEntity** -Element gibt die externen quellinhaltstyp in der Zuordnung angegeben. <br/> |
| [DestinationEntity-Element in "Association" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/15c53c3b-888d-67c7-af7d-ef36922eeebc%28Office.15%29.aspx) <br/> |Das **DestinationEntity** -Element gibt den externen zielinhaltstyp in der Zuordnung angegeben. <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Die **MethodInstances** -Element, das die Zuordnung enthält. <br/> |
   

## <a name="associationgroup-element"></a>"AssociationGroup"-Element
<a name="bkmk_AssociationGroup"> </a>

Legt ein **AssociationGroup**-Element fest. **AssociationGroup** ist ein Konstrukt, das die zugehörigen **AssociationMethods** zusammenbindet. Beispielsweise sind **GetOrdersForCustomer**, **GetCustomerForOrder** und **AssociateCustomerToOrder** zugeordnete Methoden, die in der gleichen Beziehung zwischen Kunde und Bestellung arbeiten.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    
 AssociationGroup muss für das Entity-Element definiert werden, das das Ziel der AssociationReferences darstellt, die nicht als Reverse gekennzeichnet sind, oder die Quelle der AssociationReferences, die als Reverse gekennzeichnet sind.
  
    
    



```XML
<AssociationGroup Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </AssociationGroup>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Name** <br/> |Erforderlich.  <br/> Der Name des **AssociationGroup**-Elements  <br/> Attributtyp: **String** <br/> |
|**DefaultDisplayName** <br/> |Optional.  <br/> Der Standardanzeigename des **AssociationGroup**-Elements.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/> Gibt an, ob das **AssociationGroup** häufig verwendet wird. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen des **AssociationGroup**-Elements  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des **AssociationGroup**-Elements  <br/> |
| ["AssociationReference"-Element in "AssociationGroup" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/e32c5267-53b0-9ff0-6e9a-1cb00d9f1d57%28Office.15%29.aspx) <br/> |Ein **AssociationReference**-Element eines **AssociationGroup**-Elements.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [AssociationGroups-Element in "Entity" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |Das **AssociationGroups**-Element, das diesen **AssociationGroup**-Parameter enthält.  <br/> |
   

## <a name="associationgroups-element"></a>AssociationGroups (Element)
<a name="bkmk_AssociationGroups"> </a>

Gibt eine Liste von **AssociationGroup**-Elementen an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<AssociationGroups></AssociationGroups>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |Eine Einstellung für **AssociationGroup**.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Der externe Inhaltstyp, dem dieses **AssociationGroups**-Element zugeordnet ist. <br/> |
   

## <a name="associationreference-element"></a>"AssociationReference"-Element
<a name="bkmk_AssociationReference"> </a>

Gibt einen **AssociationReference** in einer **AssociationGroup** an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<AssociationReference EntityNamespace = "String" EntityName = "String" AssociationName = "String" Reverse = "Boolean"> </AssociationReference>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|EntityNamespace  <br/> |Optional.  <br/>  Der Namespace des externen Inhaltstyps, in dem die **Association** definiert ist. Wenn **EntityName** angegeben ist, wird **EntityNamespace** benötigt. <br/> Attributtyp: **String** <br/> |
|EntityName  <br/> |Optional.  <br/>  Der Name des externen Inhaltstyps, in dem die **Association** definiert ist. Wenn **EntityNamespace** angegeben ist, wird **EntityName** benötigt. <br/> Attributtyp: **String** <br/> |
|AssociationName  <br/> |Erforderlich.  <br/> Der Name des **Association**-Parameters.  <br/> Attributtyp: **String** <br/> |
|Reverse  <br/> |Optional.  <br/> Gibt an, dass Quelle und Ziel der **Zuordnung**, auf die verwiesen wird,  umgekehrt wurden. Dies würde darauf hinweisen, dass die **Zuordnung** in der entgegengesetzten Richtung im Vergleich zu anderen Zuordnungen in derselben **AssociationGroup** arbeitet. Wenn die **AssociationGroup** beispielsweise auf eine **Association** „GetOrdersForCustomer“ verweist und dabei Auftragsartikel für das angegebene Kundenelement zurückgibt, so weist die **AssociationGroup** die Richtung „Kunde“ zu „Auftrag“ auf. Der andere **AssociationReference**, der auf eine andere Zuordnung „GetCustomerForOrder“ verweist, muss als umgekehrt gekennzeichnet werden, da diese Zuordnung die Richtung „Auftrag“ zu „Kunde“ aufweist.  <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |Die **AssociationGroup**, zu der dieser **AssociationReference** gehört. <br/> |
   

## <a name="converttype-element"></a>ConvertType (Element)
<a name="bkmk_ConvertType"> </a>

Gibt die Regel zur Konvertierung des Datentyps eines Datenwerts in einen anderen Datentyp an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    
Das Convert-Element gibt die Regel zur Konvertierung des Datentyps eines Datenwerts in einen anderen Datentyp an. Wenn die Regeln in der Reihenfolge angewendet werden, gibt diese Regel den Datentyp des Datenwert an, der in den vom BDCType-Attribut angegebenen Datentyp konvertiert werden soll. Wenn die Regeln in umgekehrter Reihenfolge angewendet werden, gibt diese Regel den Datentyp des Datenwert an, der in den vom  **LOBType**-Attribut angegebenen Datentyp konvertiert werden soll. Diese Regel kann beispielsweise einen Datumswert aus einem externen System in eine kultur- oder gebietsschemasensible Zeichenfolge konvertieren, die dem Benutzer angezeigt wird. Außerdem wird der aktualisierte Wert für diese Zeichenfolge zurück in das Datum konvertiert, das mit dem externen System kompatibel ist.
  
    
    

> **Achtung: **
> **ConvertType** unterstützt ausschließlich den gregorianischen Kalender für Konvertierungen zwischen **System.String** und **System.DateTime**. 
  
    
    




```XML
<ConvertType LOBType = "String" BDCType = "String"> </ConvertType>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|LOBType  <br/> |Erforderlich.  <br/> Der Datentyp für die Konvertierung des Datenwerts, wenn die Regeln in umgekehrter Reihenfolge angewendet werden.  <br/> Attributtyp: **String** <br/> |
|BDCType  <br/> |Erforderlich.  <br/> Der Datentyp für die Konvertierung des Datenwerts, wenn die Regeln nacheinander angewendet werden.  <br/> Attributtyp: **String** <br/> |
|LOBLocale  <br/> |Optional.  <br/> Das Gebietsschema der Daten vom externen System.  <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Die Regeln, die auf die in den Datenstrukturen gespeicherten Daten, welche durch **TypeDescriptor** dargestellt sind, angewendet werden.  <br/> |
   

## <a name="defaultvalue-element"></a>"DefaultValue"-Element
<a name="bkmk_DefaultValue"> </a>

Stellt einen Standardwert dar.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<DefaultValue MethodInstanceName = "String" Type = "String"> </DefaultValue>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**MethodInstanceName** <br/> |Erforderlich.  <br/> Der Name der **MethodInstance** für das dieser Standardwert gilt. <br/> Attributtyp: **String** <br/> |
|**Typ** <br/> | Erforderlich. <br/>  Der Datentyp des Standardwerts <br/>  Die folgenden Werte können für dieses Attribut verwendet werden. <br/> **System.Int16** <br/> **System.Int32** <br/> **System.Int64** <br/> **System.Single** <br/> **System.Double** <br/> **System.Decimal** <br/> **System.Boolean** <br/> **System.Byte** <br/> **System.UInt16** <br/> **System.UInt32** <br/> **System.UInt64** <br/> **System.Guid** <br/> **System.String** <br/> **System.DateTime** <br/>  Alle anderen serialisierbaren Typen (beispielsweise  `Type.IsSerializable == true`)  <br/>  Attributtyp: **String** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [DefaultValues-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx)||
   

## <a name="defaultvalues-element"></a>DefaultValues-Element
<a name="bkmk_DefaultValues"> </a>

Gibt eine Liste von **DefaultValues** von einem **TypeDescriptor**.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<DefaultValues></DefaultValues>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["DefaultValue"-Element in "DefaultValues" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ddb67f64-6361-7b59-6724-4680484d585d%28Office.15%29.aspx) <br/> |Der Standardwert eines **TypeDescriptor**-Elements für ein **MethodInstance**-Element.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |Das **TypeDescriptor**-Element, zu dem diese **DefaultValues**-Elemente gehören. <br/> |
   

## <a name="destinationentity-element"></a>DestinationEntity-Element
<a name="bkmk_DestinationEntity"> </a>

Gibt den externen Inhaltstyp des Ziels im **Association**-Element an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<DestinationEntity Namespace = "String" Name = "String"> </DestinationEntity>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Namespace** <br/> |Erforderlich.  <br/> Der Name des Entitätsnamespaces.  <br/> Attributtyp: **String** <br/> |
|**Name** <br/> |Erforderlich.  <br/> Der Name der Zielentität.  <br/> Attributtyp: **String** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)||
   

## <a name="entities-element"></a>"Entities"-Element
<a name="bkmk_Entities"> </a>

Gibt eine Liste der externen Inhaltstypen in einem externen System an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Entities></Entities>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Ein externer Inhaltstyp in einem externen System.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Ein externes System.  <br/> |
   

## <a name="entity-element"></a>Entity (Element)
<a name="bkmk_Entity"> </a>

Gibt einen externen Inhaltstyp an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Entity Namespace = "String" Version = "String" EstimatedInstanceCount = "Integer" DefaultOperationMode = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Entity>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Namespace** <br/> |Erforderlich.  <br/> Der Namespace, zu dem dieser externe Inhaltstyp gehört.  <br/> Attributtyp: **String** <br/> **Hinweis:** Der Namespace sollte nicht das Sonderzeichen Sternchen „**\***“ enthalten.           |
|**Version** <br/> |Erforderlich.  <br/> Die Versionsnummer dieses externen Inhaltstyps.  <br/> Attributtyp: **String** <br/> **Vorsicht:** Wenn sich das BDC-Modell ändert, müssen Sie die Versionsnummer des externen Inhaltstyps erhöhen. Wenn sich die Struktur eines externen Inhaltstyps ändert, sollten Sie die Hauptversionsnummer erhöhen. Zu Beispielen für strukturelle Änderungen gehört das Hinzufügen eines Felds zu einem **SpecificFinder** oder das Ändern eines Bezeichnerfelds. Wenn die Änderung keine Auswirkungen auf die Struktur des externen Inhaltstyps hat, wenn beispielsweise eine Creator-Methode hinzugefügt wird, wenn Verbindungsinformationen geändert werden oder wenn Namen von  **LobSystems** und Typdeskriptoren geändert werden, sollten Sie die Buildnummer und die Revisionsnummer ändern.          |
|**EstimatedInstanceCount** <br/> |Optional.  <br/> Die geschätzte Anzahl der im externen System enthaltenen externen Elemente.  <br/> Standardwert: 10000  <br/> Attributtyp: **Integer** <br/> |
|**DefaultOperationMode** <br/> |Optional.  <br/> Gibt das Standardverhalten bei Interaktionen mit dem externen System beim Erstellen, Löschen, Aktualisieren oder Lesen externer Elemente an.  <br/> Standardwert: Default  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>Online</p></td><td><p>Zwischengespeicherte Elemente für alle Vorgänge umgehen und direkt mit dem externen System interagieren.</p></td></tr><tr><td><p>Cached</p></td><td><p><b>Create</b> -, <b>Read</b> -, <b>Update</b> - und <b>Delete</b> -Vorgänge direkt für die zwischengespeicherten externen Elemente ausführen. Bei <b>Read</b> -Vorgängen, wenn die angeforderten externen Elemente im Cache verfügbar sind, die externen Elemente im Cache verwenden. Anderenfalls den Cache umgehen, um die externen Elemente aus dem externen System abzurufen, und die externen Elemente zur späteren Verwendung im Cache ablegen. </p></td></tr><tr><td><p>Offline</p></td><td><p><b>Create</b> -, <b>Read</b> -, <b>Update</b> - und <b>Delete</b> -Vorgänge nur für die zwischengespeicherten externen Elemente ausführen.</p></td></tr><tr><td><p>Standard</p></td><td><p>Standardverhalten des Systems verwenden. Dabei wird der Cache-Modus verwendet, wenn die Zwischenspeicherung externer Elemente von der Umgebung unterstützt wird.</p></td></tr></tbody></table>|
|Name  <br/> |Erforderlich.  <br/> Der Name des externen Inhaltstyps.  <br/> Attributtyp: **String** <br/> **Hinweis:** Der Name eines externen Inhaltstyps sollte nicht das Sonderzeichen „**\***“ (Sternchen) enthalten.          | |DefaultDisplayName           |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename des externen Inhaltstyps.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob dieser externe Inhaltstyp häufig verwendet wird. Wenn dies auf „true“ festgelegt wird, wird dieser externe Inhaltstyp vom Business Data Connectivity (BDC)-Dienst im Speicher zwischengespeichert.  <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen dieses externen Inhaltstyps.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften dieses externen Inhaltstyps.  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Die Zugriffssteuerungsliste (Access Control List, ACL) dieses externen Inhaltstyps.  <br/> |
| [Identifiers-Element in Entity (BDCMetadata-Schema)](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |Die Bezeichner des externen Inhaltstyps.  <br/> |
| [Methods-Element in Entity (BDCMetadata-Schema)](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |Die Methoden des externen Inhaltstyps.  <br/> |
| [AssociationGroups-Element in "Entity" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |Die Zuordnungsgruppen des externen Inhaltstyps.  <br/> |
| [Actions-Element in "Entity" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |Die Aktionen des externen Inhaltstyps.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Entities"-Element in "LobSystem" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |Die Liste der externen Inhaltstypen in diesem externen System.  <br/> |
   

## <a name="filterdescriptor-element"></a>"FilterDescriptor"-Element
<a name="bkmk_FilterDescriptor"> </a>

Gibt einen Filterdeskriptor einer Methode an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<FilterDescriptor Type = "String" FilterField = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </FilterDescriptor>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Typ  <br/> |Erforderlich.  <br/> Der Typ des Filterdeskriptors.  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>Limit</p></td><td><p>Wird beim Durchführen einer Abfrage in einem externen System verwendet, wenn der Attributwert als Höchstwert für die Anzahl der externen Elemente (**EntityInstances**), die beim Aufruf der Methode, zu der das Attribut gehört, zurückgegeben werden, interpretiert werden kann.</p></td></tr><tr><td><p>PageNumber</p></td><td><p /></td></tr><tr><td><p>Platzhalter</p></td><td><p>Beim Abfragen von einem externen System verwendet. Der Wert stellt ein Muster der reguläre und Platzhalterzeichen, das den Wert eines bestimmten Felds des Satzes von **EntityInstances**verglichen wird. Das externe System gibt nur die **EntityInstances**, deren Feldwerte mit dem angegebene Muster übereinstimmen. </p></td></tr><tr><td><p>UserContext</p></td><td><p>Wird beim Durchführen einer Abfrage in einem externen System verwendet. Der Wert kann von jeder Clientanwendung automatisch auf die Identität des Benutzers festgelegt werden, der das externe System aufruft. Anhand dieses Werts kann das externe System die Autorisierung durchführen und anschließend die zurückgegebenen Ergebnisse filtern.</p></td></tr><tr><td><p>UserCulture</p></td><td><p /></td></tr><tr><td><p>Benutzername</p></td><td><p /></td></tr><tr><td><p>Kennwort</p></td><td /></tr><tr><td><p>LastId</p></td><td /></tr><tr><td><p>SsoTicket</p></td><td /></tr><tr><td><p>UserProfile</p></td><td><p>Wird beim Durchführen einer Abfrage in einem externen System verwendet. Der Wert kann durch Analysieren des Profils des aktuellen Benutzers abgerufen werden. Anhand dieses Werts kann das externe System die zurückgegebenen Ergebnisse filtern.</p></td></tr><tr><td><p>Comparison</p></td><td><p>Wird beim Durchführen einer Abfrage in einem externen System verwendet. Ein externes System kann einen **ComparisonFilter**-Wert mit dem Wert eines bestimmten Felds einer Gruppe von **EntityInstances** vergleichen und nur die **EntityInstances** zurückgeben, bei denen das Feld den Vergleichstest besteht. </p></td></tr><tr><td><p>Timestamp</p></td><td /></tr><tr><td><p>Eingabe</p></td><td><p>Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Der Wert eines **InputFilter**-Typs kann von einem externen System als zusätzliches Argument für den Vorgang verwendet werden.</p></td></tr><tr><td><p>Ausgabe</p></td><td><p>Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Zusätzliche Ergebnisse eines Vorgangs, die von **ReturnTypeDescriptor** nicht erfasst werden können, lassen sich als ein Wert des **InputOutputFilter**-Typs abrufen. </p></td></tr><tr><td><p>InputOutput</p></td><td><p>Wird beim Aufrufen eines Vorgangs in einem externen System verwendet. Der Wert eines **InputOutputFilter**-Typs kann von einem externen System als zusätzliches Argument für den Vorgang verwendet werden, und zusätzliche Ergebnisse eines Vorgangs, die von **ReturnTypeDescriptor** nicht erfasst werden können, lassen sich als ein Wert des **InputOutputFilter**-Typs abrufen. </p></td></tr><tr><td><p>Batchverarbeitung</p></td><td /></tr><tr><td><p>BatchingTermination</p></td><td /></tr><tr><td><p>ActivityId</p></td><td><p>**ActivityId** wird beim Aufrufen eines Vorgangs im externen System verwendet. Der Wert ist eine GUID, die den aktuellen Vorgangskontext darstellt. Ist kein solcher Wert vorhanden, generiert dieser Filter eine Zufalls-GUID. In SharePoint Foundation 2010 wird für diesen Filter die **CorrelationID** verwendet. </p></td></tr></tbody></table>
|FilterField  <br/> |Optional.  <br/> Attributtyp: **String** <br/> |
|Name  <br/> |Erforderlich.  <br/> Der Name des Filterdeskriptors.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename des Filterdeskriptors.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob dieser Filterdeskriptor häufig verwendet wird. Wenn dies auf **true** festgelegt wird, wird dieser Filterdeskriptor vom Business Data Connectivity (BDC)-Dienst im Arbeitsspeicher zwischengespeichert.<br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen dieses Filterdeskriptors.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften dieses Filterdeskriptors.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [FilterDescriptors-Element in Method (BDCMetadata-Schema)](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |Eine Liste der Filterdeskriptoren einer Methode.  <br/> |
   

## <a name="filterdescriptors-element"></a>FilterDescriptors-Element
<a name="bkmk_FilterDescriptors"> </a>

Gibt eine Liste mit Filterdeskriptoren einer Methode an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<FilterDescriptors></FilterDescriptors>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> |Ein Filterdeskriptor.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Die Methode, zu der diese Liste mit Filterdeskriptoren gehört.  <br/> |
   

## <a name="identifier-element"></a>"Identifier"-Element
<a name="bkmk_Identifier"> </a>

Gibt einen Bezeichner eines externen Inhaltstyps an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
> [!NOTE]
> 
> Der Business Data Connectivity (BDC)-Dienst ermöglicht die Zuordnung der Bezeichner zu Feldern mit Datentypen, die Nullwerte zulassen. Für primäre Bezeichner verursacht BDC jedoch einen Fehler, wenn der Wert dieser Bezeichner **null** ist. 
  
    
    




```XML
<Identifier TypeName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Identifier>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|TypeName  <br/> |Erforderlich.  <br/> Der Datentyp des Werts, der dem Bezeichner entspricht.  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>System.Boolean</p></td><td><p>Ein Bit.</p></td></tr><tr><td><p>System.Byte</p></td><td><p>Eine Zahl zwischen 0 und 255 inklusive.</p></td></tr><tr><td><p>System.Char</p></td><td><p>Ein Unicode-Zeichen.</p></td></tr><tr><td><p>System.DateTime</p></td><td><p>Ein Datum und eine Uhrzeit zwischen 12:00:00 Mitternacht, 1. Januar 1 Anno Domini (Christliche Zeitrechnung) und inklusive 23:59:59, 31. Dezember 9999 Anno Domini (Christliche Zeitrechnung), in einer Auflösung von 100 Nanosekunden.</p></td></tr><tr><td><p>System.Decimal</p></td><td><p>Eine Zahl von -79.228.162.514.264.337.593.543.950.335 bis +79.228.162.514.264.337.593.543.950.335 inklusive.</p></td></tr><tr><td><p>System.Double</p></td><td><p>Eine Zahl mit doppelter Genauigkeit zwischen -1,79769313486232e308 und +1,79769313486232e308 inklusive sowie positive Null, negative Null, positiv unendlich, negativ unendlich und NaN (not-a-number). </p></td></tr><tr><td><p>System.Guid</p></td><td><p>Eine GUID.</p></td></tr><tr><td><p>System.Int16</p></td><td><p>Eine Zahl zwischen -32.768 und +32.768 inklusive.</p></td></tr><tr><td><p>System.Int32</p></td><td><p>Eine Zahl zwischen 0 und 4.294.967.295 inklusive.</p></td></tr><tr><td><p>System.Int64</p></td><td><p>Eine Zahl zwischen 0 und 18.446.744.073.709.551.615 inklusive.</p></td></tr><tr><td><p>System.SByte</p></td><td><p>Eine Zahl zwischen -128 und +127 inklusive.</p></td></tr><tr><td><p>System.Single</p></td><td><p>Eine Zahl mit einfacher Genauigkeit zwischen -3,402823e38 und +3,402823e38 inklusive.</p></td></tr><tr><td><p>System.String</p></td><td><p>Eine Zeichenfolge mit Unicode-Text.</p></td></tr><tr><td><p>System.TimeSpan</p></td><td><p>Eine Dauer zwischen -10.675.199 Tagen 2 Stunden 48 Minuten 5 Sekunden 477 Millisekunden 580 Mikrosekunden 800 Nanosekunden und +10.675.199 Tagen 2 Stunden 48 Minuten 5 Sekunden 477 Millisekunden 580 Mikrosekunden 800 Nanosekunden inklusive, in einer Auflösung von 100 Nanosekunden.</p></td></tr><tr><td><p>System.UInt16</p></td><td><p>Eine Zahl zwischen 0 und 65.535 inklusive.</p></td></tr><tr><td><p>System.UInt32</p></td><td><p>Eine Zahl zwischen 0 und 4.294.967.295 inklusive.</p></td></tr><tr><td><p>System.UInt64</p></td><td><p>Eine Zahl zwischen 0 und 18.446.744.709.551.615 inklusive.</p></td></tr></tbody></table>
|Name  <br/> |Erforderlich.  <br/> Der Name des Bezeichners.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename des Bezeichners.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob dieser Bezeichner häufig verwendet wird. Wenn dies auf **true** festgelegt wird, wird dieser Bezeichner vom Business Data Connectivity (BDC)-Dienst im Arbeitsspeicher zwischengespeichert.<br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen des Bezeichners.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des Bezeichners.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Identifiers-Element in Entity (BDCMetadata-Schema)](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |Eine Liste der Bezeichner eines externen Inhaltstyps.  <br/> |
   

## <a name="identifiers-element"></a>Identifiers-Element
<a name="bkmk_Identifiers"> </a>

Gibt eine Liste mit Bezeichnern eines externen Inhaltstyps an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Identifiers></Identifiers>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Identifier-Element in "Identifiers" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> |Gibt einen Bezeichner an.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Der externe Inhaltstyp, der diese Liste mit Bezeichnern enthält.  <br/> |
   

## <a name="interpretation-element"></a>Interpretation-Element
<a name="bkmk_Interpretation"> </a>

Gibt die Regeln an, die auf die in den Datenstrukturen gespeicherten Daten, dargestellt durch **TypeDescriptor**, angewendet werden sollen. Diese Regeln werden in der Regel angegeben, um die Datenwerte zu ändern, die von einem externen System zurückgegeben werden, damit diese in der Benutzeroberfläche leichter dargestellt werden können. Wenn der Datenwert aus dem externen System abgerufen wird, müssen die angegebenen Regeln in der Reihenfolge angewendet werden, in der Sie im **Interpretation**-Element angegeben sind. Die erste Regel muss auf den vom externen System empfangenen Datenwert angewendet werden; die nachfolgenden Regeln werden auf den Datenwert angewendet, der aus der Anwendung der vorherigen Regel resultiert. Wenn der Datenwert an das externe System gesendet wird, müssen die angegebenen Regeln in der umgekehrten Reihenfolge angewendet werden, in der Sie im **Interpretation**-Element angegeben sind. Die erste Regel muss auf den vom Benutzer empfangenen Datenwert angewendet werden; die nachfolgenden Regeln werden auf den Datenwert angewendet, der aus der Anwendung der vorherigen Regel resultiert.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Interpretation></Interpretation>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [ConvertType-Element in "Interpretation" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c474cf2c-b631-f3c9-daf1-f05d3e0d385f%28Office.15%29.aspx) <br/> |Ein **ConvertType**-Element, das die Konvertierung eines Datentyps in einen anderen Datentyp angibt. <br/> |
| [NormalizeDateTime-Element in "Interpretation" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/bbae3bfa-0754-d576-2bee-1ac0e8508a57%28Office.15%29.aspx) <br/> |Ein **NormalizeDateTime**-Element, das die Konvertierung der Datums- und Zeitdarstellung eines von einem externen System erhaltenen Werts in eine andere Darstellung angibt. <br/> |
|NormalizeString  <br/> |Ein **NormalizeString**-Element, das die Konvertierung der Zeichenfolgendarstellung eines von einem externen System erhaltenen Werts in eine andere Darstellung angibt. <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |Das **TypeDescriptor**-Element. <br/> |
   

## <a name="lobsystem-element"></a>"LobSystem"-Element
<a name="bkmk_LobSystem"> </a>

Stellt eine externe Datenquelle dar.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LobSystem Type = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystem>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Typ  <br/> |Der Typ des der **LobSystem**.  <br/> Erforderlich.  <br/> Die folgende Tabelle listet die möglichen Werte für dieses Attribut auf.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>Datenbank</p></td><td><p>Die dargestellte externe Datenquelle ist eine Datenbank.</p></td></tr><tr><td><p>DotNetAssembly</p></td><td><p>Die dargestellte externe Datenquelle ist ein Satz von .NET Framework-Klassen.</p></td></tr><tr><td><p>Wcf</p></td><td><p>Die dargestellte externe Datenquelle ist ein WCF-Dienst-Endpunkt.</p></td></tr><tr><td><p>WebService</p></td><td><p>Die dargestellte externe Datenquelle ist ein Webdienst. Dies ist veraltet, verwenden Sie stattdessen WCF.</p></td></tr><tr><td><p>Benutzerdefiniert</p></td><td><p>In der dargestellten externen Datenquelle ist ein benutzerdefinierter Konnektor implementiert, um die Verbindung und die Datenübertragung zu verwalten.</p></td></tr></tbody></table>|
|Name  <br/> |Der Name des **LobSystem**.  <br/> Erforderlich.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Der Standardanzeigename des **LobSystem**.  <br/> Optional.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Gibt an, ob das **LobSystem** häufig verwendet wird. Wenn es häufig verwendet wird, wird das **LobSystem** vom Business Data Connectivity (BDC)-Dienst zwischengespeichert.   <br/> Optional.  <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen des **LobSystem**-Elements  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Gibt die Eigenschaften eines **LobSystem** an.  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Gibt die Zugriffssteuerungsliste (Access Control List, ACL) eines **LobSystem** an.  <br/> |
| [Proxy-Element in "LobSystem" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/8ec2e7b0-156f-ff4a-a87b-fe5764e4875b%28Office.15%29.aspx) <br/> |Gibt einen vom Benutzer bereitgestellten Proxy an, der identisch mit demjenigen ist, der generiert würde, wenn dieses Element nicht vorhanden wäre.  <br/> |
| [LobSystemInstances-Element in "LobSystem" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |Gibt die externen Systeminstanzen für dieses externe System an.  <br/> |
| ["Entities"-Element in "LobSystem" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |Gibt die externen Inhaltstypen in diesem externen System an.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["LobSystems"-Element im Modell ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |Gibt eine Liste externer Systeme in diesem Modell an.  <br/> |
   

## <a name="lobsysteminstance-element"></a>LobSystemInstance-Element
<a name="bkmk_LobSystemInstance"> </a>

Gibt eine externe Systeminstanz an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LobSystemInstance Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystemInstance>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Name  <br/> |Erforderlich.  <br/> Der Name der externen Systeminstanz.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename der externen Systeminstanz.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob diese externe Systeminstanz häufig verwendet wird. Wenn **true** festgelegt ist, wird die externe Systeminstanz von Business Data Connectivity (BDC)-Dienst zwischengespeichert.<br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen dieser externen Systeminstanz.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften dieser externen Systeminstanz.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LobSystemInstances-Element in "LobSystem" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |Eine Liste von externen Systeminstanzen.  <br/> |
   

## <a name="lobsysteminstances-element"></a>LobSystemInstances-Element
<a name="bkmk_LobSystemInstances"> </a>

Gibt eine Liste externer Systeminstanzen an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LobSystemInstances></LobSystemInstances>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> |Eine externe Systeminstanz.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Ein externes System.  <br/> |
   

## <a name="lobsystems-element"></a>"LobSystems"-Element
<a name="bkmk_LobSystems"> </a>

Gibt eine Liste von **LobSystem**-Elementen eines Modells an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LobSystems></LobSystems>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Ein **LobSystem** -Element, das ein externes System festlegt. <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Model"-Element ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |Eine Anwendungsdefinition (BDC-Modell)  <br/> |
   

## <a name="localizeddisplayname-element"></a>"LocalizedDisplayName"-Element
<a name="bkmk_LocalizedDisplayName"> </a>

Gibt einen lokalisierten Namen an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LocalizedDisplayName LCID = "Integer"> </LocalizedDisplayName>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|LCID  <br/> |Erforderlich.  <br/> Die Sprachcode-ID (Language Code Identifier, LCID).  <br/> Attributtyp: **Integer** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Das **LocalizedDisplayNames**-Element, das diesen **LocalizedDisplayName**-Parameter enthält.  <br/> |
   

## <a name="localizeddisplaynames-element"></a>"LocalizedDisplayNames"-Element
<a name="bkmk_LocalizedDisplayNames"> </a>

Gibt eine Liste lokalisierter Namen für ein **MetadataObject** an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<LocalizedDisplayNames></LocalizedDisplayNames>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayName-Element in LocalizedDisplayNames (BDCMetadata-Schema)](http://msdn.microsoft.com/library/93fb80ef-6347-b463-da90-4980d872678e%28Office.15%29.aspx) <br/> |Ein lokalisierter Name.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Model"-Element ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [Identifier-Element in "Identifiers" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| ["FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [Parameter-Element in "Parameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| ["AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| ["Action"-Element in "Actions" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="metadataobject-element"></a>"MetadataObject"-Element
<a name="bkmk_MetadataObject"> </a>

 **Namespace**
  
    
    
 **Schema:**
  
    
    



```XML

```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
 **Untergeordnete Elemente**
  
    
    
 **Übergeordnetes Element**
  
    
    

## <a name="method-element"></a>Method-Element
<a name="bkmk_Method"> </a>

Gibt eine Methode eines externen Inhaltstyps an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Method IsStatic = "Boolean" LobName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Method>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|IsStatic  <br/> |Optional.  <br/>  Gibt an, ob für die Ausführung dieser Methode ein externes Element ( **EntityInstance**) erforderlich ist, das als Ausführungskontext fungiert. Wird das Attribut auf **true** festgelegt, stellt die Methode eine statische Methode dar, für die kein bestimmtes **EntityInstance**-Element zur Bereitstellung eines Ausführungskontextes erforderlich ist. Wird das Attribut auf **false** festgelegt, stellt die Methode eine Instanzmethode dar und erfordert ein **EntityInstance**-Element, um den Kontext für die Ausführung bereitzustellen. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
|LobName  <br/> |Optional.  <br/> Der Name der im externen System definierten Operation, die von dieser Methode dargestellt wird.  <br/> Attributtyp: **String** <br/> |
|Name  <br/> |Erforderlich.  <br/> Der Name dieser Methode.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Optional.  <br/> Der Standardanzeigename der Methode.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Optional.  <br/> Gibt an, ob diese Methode häufig verwendet wird. Wird das Attribut auf **true** festgelegt, speichert der Business Data Connectivity (BDC)-Dienst diese Methode im Arbeitsspeicher.<br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen der Methode.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften der Methode.  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Die Zugriffssteuerungsliste (Access Control List, ACL) dieser Methode.  <br/> |
| [FilterDescriptors-Element in Method (BDCMetadata-Schema)](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |Die Filterdeskriptoren der Methode.  <br/> |
| [Parameters-Element in "Method" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |Die Parameter der Methode. Eine Methode kann nicht mehr als einen Rückgabeparameter aufweisen.  <br/> |
| ["MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Die Methodeninstanzen der Methode.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Methods-Element in Entity (BDCMetadata-Schema)](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |Eine Liste der Methoden eines externen Inhaltstyps.  <br/> |
   

## <a name="methodinstance-element"></a>MethodInstance-Element
<a name="bkmk_MethodInstance"> </a>

Gibt ein **MethodInstance**-Element an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    
Die folgenden beiden Situationen in einem Modell BDC bewirken ein  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) zur Laufzeit:
  
    
    

- Zwei **SpecificFinder**-Methodeninstanzen, von denen dieselben Felder zurückgegeben werden.
    
  
- Zwei **SpecificFinder**-Methodeninstanzen, die die gleiche Anzahl von Feldern aufweisen und die gleiche Anzahl von Feldern mit einer anderen Methodeninstanz gemeinsam verwenden, wie z. B. die **Finder**-Methode.
    
  



```XML
<MethodInstance Type = "Strig" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </MethodInstance>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Typ** <br/> |Erforderlich.  <br/> Gibt den Typ des **MethodInstance**-Elements an.  <br/> In der folgenden Tabelle sind die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>Finder</p></td><td><p>Ein **MethodInstance**-Typ, der aufgerufen werden kann, um eine Sammlung von null oder mehr **EntityInstances**-Elementen eines bestimmten **Entity**-Elements zurückzugeben. Eingaben für **Finder** werden durch die **FilterDescriptors**-Elemente im **Method**-Element definiert, in dem sich **Finder** befindet. </p></td></tr><tr><td><p>SpecificFinder</p></td><td><p>Ein **MethodInstance**-Typ, der aufgerufen werden kann, um anhand von **EntityInstanceId** ein spezielles **EntityInstance**-Element eines bestimmten **Entity**-Elements zurückzugeben. Eingaben für **SpecificFinder** werden durch die **Identifiers**-Elemente definiert und geordnet, die der **Entity** zugeordnet sind. </p></td></tr><tr><td><p>GenericInvoker</p></td><td><p>Ein **MethodInstance**-Typ, der aufgerufen werden kann, um eine bestimmte Aufgabe in einem externen System auszuführen. Die Eingaben und Ausgaben von **GenericInvoker** sind spezifisch für das **Method**-Element. </p></td></tr><tr><td><p>IdEnumerators</p></td><td><p>Ein Typ von **MethodInstance**, die aufgerufen werden können, um die **Field** Werte zurückzugeben, die die Identität des **EntityInstances** von einer bestimmten **Entity**darstellen. Die Eingabe **IdEnumerator** wird definiert, durch die **FilterDescriptors**, die in der Methode enthalten sind, die enthält die **IdEnumerator**, um die Liste der IDs, abzurufen, die die eindeutigen Schlüssel für jede Entität sind, die durchsucht werden soll. Diese Methodeninstanz kann externe Datensuche in SharePoint Server. </p></td></tr><tr><td><p>ChangedIdEnumerator</p></td><td><p>Ein **MethodInstance**-Typ, der aufgerufen werden kann, um **EntityInstanceIds**-Elemente von **EntityInstances**-Elementen abzurufen, die nach einem angegebenen Zeitpunkt in einem externen System geändert wurden.</p></td></tr><tr><td><p>DeletedIdEnumerator</p></td><td><p>Ein **MethodInstance**-Typ, der aufgerufen werden kann, um **EntityInstanceIds**-Elemente von **EntityInstances**-Elementen abzurufen, die nach dem angegebenen Zeitpunkt in einem externen System gelöscht wurden.</p></td></tr><tr><td><p>Scalar</p></td><td><p>Eine **MethodInstance**, die einen einzelnen Wert zurückgibt, den Sie im externen System aufrufen können. Beispielsweise können Sie mithilfe einer skalaren Methodeninstanz den Gesamtumsatz bis dato aus dem externen System abrufen. **Entities**-Elemente haben null oder mehr skalare Methodeninstanzen. </p></td></tr><tr><td><p>AccessChecker</p></td><td><p>Ein Typ von **MethodInstance**, durch dessen Aufruf die Berechtigungen abgerufen werden können, über die der aufrufende Sicherheitsprinzipal für die einzelnen Elemente einer Auflistung von **EntityInstances** verfügt, die durch die angegebenen **EntityInstanceIds** identifiziert werden.</p></td></tr><tr><td><p>Creator</p></td><td><p>Ein Typ von **MethodInstance**, der zum Erstellen einer neuen **EntityInstance** aufgerufen werden kann. Der Satz von Feldern, die zum Erstellen der **EntityInstance** erforderlich sind, wird die Creator-Ansicht bezeichnet.</p></td></tr><tr><td><p>Deleter</p></td><td><p>Ein Typ von **MethodInstance**, durch dessen Aufruf eine **EntityInstance** mit einer bestimmten **EntityInstanceId** gelöscht werden kann.</p></td></tr><tr><td><p>Updater</p></td><td><p>Ein Typ von **MethodInstance**, der zum Aktualisieren einer **EntityInstance** aufgerufen werden kann, die von einer angegebenen **EntityInstanceId** identifiziert wird. Der Satz von Feldern, die zum Aktualisieren der **EntityInstance** erforderlich sind, wird als Updater-Ansicht bezeichnet. Der Satz von Feldern, deren Werte übergeben werden sollten, bevor sie geändert werden, wird als die PreUpdater-Ansicht bezeichnet.</p></td></tr><tr><td><p>StreamAccessor</p></td><td><p>Ein Typ von **MethodInstance**, durch dessen Aufruf ein Feld einer **EntityInstance** in Form eines Datenstroms von Bytes abgerufen werden kann.</p></td></tr><tr><td><p>BinarySecurityDescriptorAccessor</p></td><td><p>Ein Typ von **MethodInstance**, durch dessen Aufruf eine Bytesequenz von einem externen System abgerufen werden kann. Die systemspezifische Bytesequenz beschreibt einen Satz von Sicherheitsprinzipalen und die Berechtigungen, die jedem Sicherheitsprinzipal für die durch eine **EntityInstanceId** identifizierte **EntityInstance** zugeordnet sind. </p></td></tr><tr><td><p>Des BulkSpecificFinder</p></td><td><p>Ein Typ von **MethodInstance**, bei dessen Aufruf eine Menge spezifischer **EntityInstances** einer **Entity**, identifiziert durch eine Menge entsprechender **EntityInstanceIds**, zurückgegeben wird.</p></td></tr><tr><td><p>BulkIdEnumerator</p></td><td><p>Ein Typ von **MethodInstance**, durch dessen Aufruf minimale Informationen zu den externen Elementen abgerufen werden, die den angegebenen Identitäten entsprechen. Mit dieser Methodeninstanz kann die Synchronisierung zwischengespeicherter Daten optimiert werden. Die Methode sollte nur die Identitäten und Versionsinformationen der externen Elemente zurückgeben, die den angegebenen **Identities** entsprechen. Diese können von der aufrufenden Anwendung mit der lokalen Version verglichen werden, um Änderungen zu erkennen und ggf. die Aktualisierung der zwischengespeicherten Daten durch die geänderten externen Elemente anzufordern. </p></td></tr></tbody></table>
|**Standard** <br/> |Optional.  <br/> Gibt an, ob die **MethodInstance** bei allen **MethodInstances**, die den gleichen Typ innerhalb des enthaltenden externen Inhaltstyps verwenden (**Entität**) Standard ist.  <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**ReturnParameterName** <br/> |Optional.  <br/>  Der Name des **Parameter**-Elements, das den **ReturnTypeDescriptor** des **MethodInstance**-Elements enthält. Das **Direction**-Attribut von **Parameter** muss ein **ParameterDirection**-Attribut mit dem Wert **Out**, **InOut** oder **Return** sein. <br/> Dieses Attribut muss für alle Typen von **MethodInstances** außer **GenericInvoker**, **Creator**, **Deleter** und **Updater** angegeben werden.  <br/> Attributtyp: **String** <br/> |
|**ReturnTypeDescriptorLevel** <br/> |Optional.  <br/> Veraltet. Verwenden Sie stattdessen **ReturnTypeDescriptorPath**.<br/> Attributtyp: **Integer** <br/> |
|**ReturnTypeDescriptorPath** <br/> |Optional.  <br/> Der gepunktete Pfad des **TypeDescriptors** der Zuordnung.  <br/> Attributtyp: **String** <br/> |
|**Name** <br/> |Erforderlich.  <br/> Gibt den Namen der **MethodInstance** an.  <br/> Attributtyp: **String** <br/> |
|**DefaultDisplayName** <br/> |Optional.  <br/> Gibt den Standardanzeigenamen für die **MethodInstance** an.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/> Gibt an, ob die **MethodInstance** häufig verwendet wird. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Anzeigenamen von **MethodInstance**.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des **MethodInstance**-Parameters.  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Die Zugriffssteuerungslisten (Access Control Lists, ACLs) von **MethodInstance**.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["MethodInstances"-Element in "Method" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Das **MethodInstances**-Element, das diesen **MethodInstance**-Parameter enthält.  <br/> |
   

## <a name="methodinstances-element"></a>"MethodInstances"-Element
<a name="bkmk_MethodInstances"> </a>

Gibt eine Liste der Zuordnungen und Methodeninstanzen einer Methode an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<MethodInstances></MethodInstances>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |Eine Zuordnung.  <br/> |
| [MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |Eine Methodeninstanz.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Die Methode, zu der diese Methodeninstanz gehört.  <br/> |
   

## <a name="methods-element"></a>Methods-Element
<a name="bkmk_Methods"> </a>

Gibt eine Liste mit Methoden eines externen Inhaltstyps an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Methods></Methods>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Gibt eine Methode an.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Der externe Inhaltstyp, zu dem diese Liste mit Methoden gehört.  <br/> |
   

## <a name="model-element"></a>"Model"-Element
<a name="bkmk_Model"> </a>

Legt das Stammelement fest, das eine Anwendungsdefinition darstellt. Modelle definieren externe Inhaltstypen, die in externen Anwendungen enthalten sind. 
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Model Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Model>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Name  <br/> |Der Name des **Model**-Elements  <br/> Erforderlich.  <br/> Attributtyp: **String** <br/> |
|DefaultDisplayName  <br/> |Der Standardanzeigename des **Model**-Elements.  <br/> Optional.  <br/> Attributtyp: **String** <br/> |
|IsCached  <br/> |Gibt an, ob das **Model** häufig verwendet wird. Wenn dies auf **true** festgelegt ist, wird das **Model** vom Business Data Connectivity (BDC)-Dienst zwischengespeichert. <br/> Optional.  <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen des **Model**-Elements  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des **Model**-Elements  <br/> |
| [AccessControlList-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Die Zugriffssteuerungsliste (Access Control List, ACL) des **Model**-Elements  <br/> |
| ["LobSystems"-Element im Modell ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |Das in diesem **Model**-Element enthaltene **LobSystems**  <br/> |
   
 **Übergeordnetes Element**
  
    
    
Keine
  
    
    

## <a name="normalizedatetime-element"></a>NormalizeDateTime (Element)
<a name="bkmk_NormalizeDateTime"> </a>

Gibt die Regel an, die zur Konvertierung der Darstellung des Datums- und Zeitwertes in eine andere Darstellung verwendet wird. Diese Regel kann beispielsweise angeben, dass ein in koordinierter Weltzeit (Coordinated Universal Time, UTC) angegebener Wert in eine lokale Zeitzone konvertiert wird. 
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<NormalizeDateTime LobDateTimeMode = "String"> </NormalizeDateTime>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**LobDateTimeMode** <br/> |Erforderlich.  <br/> Gibt die gewünschte Konvertierung an.  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>UTC</p></td><td><p>Der Wert, der vom externen System empfangen wird, ist in koordinierter Weltzeit (Coordinated Universal Time, UTC) angegeben. Wenn der empfangene Wert **Local** ist, wird dieser in koordinierte Weltzeit konvertiert. BDC sendet koordinierte Weltzeit an das externe System.</p></td></tr><tr><td><p>Lokal</p></td><td><p>Der vom externen System empfangene Wert ist **Local**. Wenn der vom externen System empfangene Wert **Local** ist, wird dieser in koordinierte Weltzeit konvertiert. **Local** wird von BDC an das externe System gesendet. </p></td></tr><tr><td><p>Unspecified</p></td><td><p>Der vom externen System gesendete Wert weist einen nicht definierten Typ auf. BDC geht davon aus, dass es sich um einen Wert in koordinierter Weltzeit handelt, indem der Wert als koordinierte Weltzeit überschrieben wird. Werte in koordinierter Weltzeit werden von BDC als Werte eines nicht definierten Typs an das externe System gesendet.</p></td></tr></tbody></table>
|
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Ein **Interpretation**-Element, das die Regeln angibt, die auf die in den Datenstrukturen gespeicherten Daten dargestellt durch **TypeDescriptor** angewendet werden sollen.  <br/> |
   

## <a name="normalizestring-element"></a>NormalizeString-element
<a name="bkmk_NormalizeString"> </a>

Gibt einen Parameter für eine Methode an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML

```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
 **Untergeordnete Elemente**
  
    
    
 **Übergeordnetes Element**
  
    
    

## <a name="parameter-element"></a>Parameter-Element
<a name="bkmk_Parameter"> </a>

Gibt einen Parameter für eine Methode an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Parameter Direction = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Parameter>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Direction  <br/> |Erforderlich.  <br/> Die Richtung des Parameters.  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>In</p></td><td><p>Der dargestellte **Parameter** ist ein Eingabeparameter.</p></td></tr><tr><td><p>Out</p></td><td><p>Der dargestellte Parameter ist ein Ausgabeparameter.</p></td></tr><tr><td><p>InOut</p></td><td><p>Der dargestellte Parameter ist ein Eingabe- und Ausgabeparameter. In C# entspricht dies "**ref**".</p></td></tr><tr><td><p>Return</p></td><td><p>Der dargestellte Parameter ist ein Rückgabeparameter.</p></td></tr></tbody></table>
|**Name** <br/> |Erforderlich.  <br/> Der Name des Parameters.  <br/> Attributtyp: **String** <br/> |
|**DefaultDisplayName** <br/> |Optional.  <br/> Der Standardanzeigename des Parameters.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/> Gibt an, ob der **Parameter** häufig verwendet wird. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen des Parameters.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften des Parameters.  <br/> |
| [TypeDescriptor](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> |Der Stammtypdeskriptor des Parameters.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Parameters-Element in "Method" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |Das **Parameters**-Element, das diesen Parameter enthält. <br/> |
   

## <a name="parameters-element"></a>"Parameters"-Element
<a name="bkmk_Parameters"> </a>

Gibt eine Liste mit Parametern einer Methode an.
  
    
    

  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Parameters></Parameters>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Parameter-Element in "Parameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> |Ein Parameter.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Die Methode, zu der diese Parameter gehören.  <br/> |
   

## <a name="properties-element"></a>Properties-Element
<a name="bkmk_Properties"> </a>

Gibt eine Liste der Eigenschaften eines Metadatenobjekts an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Properties></Properties>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Property-Element in "Properties" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/2e6e8d5d-ef3b-c536-f3d1-ad2039b92c24%28Office.15%29.aspx) <br/> |Gibt eine Eigenschaft an.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["Model"-Element ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [LobSystemInstance-Element in LobSystemInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [Entity-Element in Entities (BDCMetadata-Schema)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [Identifier-Element in "Identifiers" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [Method-Element in Methods (BDCMetadata-Schema)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| ["FilterDescriptor"-Element in "FilterDescriptors" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [Parameter-Element in "Parameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [TypeDescriptor](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [MethodInstance-Element in "MethodInstances" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| ["AssociationGroup"-Element in "AssociationGroups" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| ["Action"-Element in "Actions" ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [ActionParameter-Element in "ActionParameters" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="property-element"></a>Property-Element
<a name="bkmk_Property"> </a>

Gibt den Name und den Typ für eine Eigenschaft eines Metadatenobjekts an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Property Name = "String" Type = "String"> </Property>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**Name** <br/> |Erforderlich.  <br/> Gibt den Namen der Eigenschaft an.  <br/> Attributtyp: **String** <br/> |
|**Typ** <br/> |Erforderlich.  <br/> Gibt den Datentyp der Eigenschaft an.  <br/> Attributtyp: **String** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Das **Properties**-Element, das diese Eigenschaft enthält. <br/> |
   

## <a name="proxy-element"></a>Proxy-Element
<a name="bkmk_Proxy"> </a>

Gibt einen vom Benutzer bereitgestellten Proxy an, der mit dem Proxy identisch ist, der generiert würde, wenn dieses Element nicht vorhanden wäre. Durch die Eliminierung des Mehraufwands für die Proxygenerierung wird die Leistung verbessert. Externe Systeme vom Typ ".NET-Verbindungsassembly" müssen verwendet werden, um benutzerdefinierte Geschäftslogik anzugeben, mit der eine Verbindung mit einem externen System hergestellt wird.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Proxy></Proxy>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| ["LobSystem"-Element in LobSystems ("BDCMetadata"-Schema)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Das **LobSystem**-Element, für das dieser Proxy gilt. <br/> |
   

## <a name="right-element"></a>Right-Element
<a name="bkmk_Right"> </a>

Gibt eine einzelne Zugriffsberechtigung für einen Zugriffssteuerungseintrag (Access Control Entry, ACE) an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<Right BdcRight = "String"> </Right>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|BdcRight  <br/> |Erforderlich.  <br/> Die verfügbare Berechtigung für den Sicherheitsprinzipal, der über das Recht verfügt.  <br/> In der folgenden Tabelle werden die möglichen Werte für dieses Attribut aufgeführt.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Wert</p></th><th><p>Beschreibung</p></th></tr></thead><tbody><tr><td><p>Keine</p></td><td><p>Keine Berechtigungen.</p></td></tr><tr><td><p>Ausführen</p></td><td><p>Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, eine **MethodInstance** aufzurufen.</p></td></tr><tr><td><p>Bearbeiten</p></td><td><p>Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, die Attribute eines Metadatenobjekts oder die Attribute von dessen Beziehung zu anderen Metadatenobjekten zu ändern.</p></td></tr><tr><td><p>SetPermissions</p></td><td><p>Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, den Satz der Berechtigungen für ein Metadatenobjekt zu ändern.</p></td></tr><tr><td><p>SelectableInClients</p></td><td><p>Der dargestellte Sicherheitsprinzipal verfügt über die Berechtigung, das Metadatenobjekt, auf das sich dieses Recht bezieht, auszuwählen. Wenn ein Benutzer nicht über diese Berechtigung verfügt, sollte das Metadatenobjekt nicht auswählbar sein.</p></td></tr></tbody></table>
|
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [AccessControlEntry-Element in "AccessControlList" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |Das **AccessControlEntry**-Element, das dieses Recht enthält. <br/> |
   

## <a name="sourceentity-element"></a>SourceEntity-Element
<a name="bkmk_SourceEntity"> </a>

Gibt einen externen Quellinhaltstyp eines **Association**-Elements an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<SourceEntity Namespace = "String" Name = "String"> </SourceEntity>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|Namespace  <br/> |Erforderlich.  <br/> Der Namespace des externen Inhaltstyps, der die Quelle des **Association**-Elements darstellt, das dieses Element enthält. <br/> Attributtyp: String  <br/> |
|Name  <br/> |Erforderlich.  <br/> Der Name des externen Inhaltstyps, der die Quelle des **Association**-Elements darstellt, das dieses Element enthält. <br/> Attributtyp: **String** <br/> |
   
 **Untergeordnete Elemente**
  
    
    
Keine
  
    
    
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |Das **Association**-Element, das dieses Element enthält. <br/> |
   

## <a name="typedescriptor-element"></a>TypeDescriptor (Element)
<a name="bkmk_TypeDescriptor"> </a>

Gibt einen **TypeDescriptor** an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<TypeDescriptor TypeName = "String" LobName = "String" IdentifierEntityNamespace = "String" IdentifierEntityName = "String" IdentifierName = "String" ForeignIdentifierAssociationName = "String" ForeignIdentifierAssociationEntityName = "String" ForeignIdentifierAssociationEntityNamespace = "String" AssociatedFilter = "String" IsCollection = "Boolean" ReadOnly = "Boolean" CreatorField = "Boolean" UpdaterField = "Boolean" PreUpdaterField = "Boolean" Significant = "Boolean" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </TypeDescriptor>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**TypeName** <br/> |Erforderlich.  <br/> Der Bezeichner des Datentyps der Datenstruktur, die durch den **TypeDescriptor** dargestellt wird.  <br/> Attributtyp: **String** <br/> |
|**LobName** <br/> |Optional.  <br/> Die Datenstruktur, die durch den **TypeDescriptor** dargestellt wird. Der Standardwert dieses Attributs ist der Name für den **TypeDescriptor**. So kann beispielsweise eine Datenstruktur eines Branchensystems (Line of Business, LOB) mit dem Namen CN1A durch einen **TypeDescriptor** dargestellt werden, dessen **Name**-Attribut „Kundenname“ entspricht, wenn das **LobName**-Attribut für den **TypeDescriptor** „CN1A“ entspricht. <br/> Attributtyp: **String** <br/> |
|**IdentifierEntityNamespace** <br/> |Optional.  <br/>  Der Namespace des externen Inhaltstyps, der den Bezeichner enthält, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **IdentifierEntityName** und **IdentifierName** vorhanden sein. Der Standardwert dieses Attributs ist der Namespace des externen Inhaltstyps, der die Methode enthält, die den Parameter enthält, der wiederum den **TypeDescriptor** enthält. <br/> Attributtyp: **String** <br/> |
|**IdentifierEntityName** <br/> |Optional.  <br/>  Der Name der **Entity**, die den **Identifier** enthält, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **IdentifierEntityNamespace** und **IdentifierName** vorhanden sein. Der Standardwert des Attributs ist der Name der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. <br/> Attributtyp: **String** <br/> |
|**IdentifierName** <br/> |Optional.  <br/>  Der Name für den **Identifier**, auf den der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf einen **Identifier** verweist, darf das Attribut nicht vorhanden sein. <br/> Attributtyp: **String** <br/> |
|**ForeignIdentifierAssociationName** <br/> |Optional.  <br/>  Der Name der **Association**, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, muss auch das **IdentifierName**-Attribut vorhanden sein. Das **ForeignIdentifierAssociationName**-Attribut muss angegeben werden, wenn der **Identifier**, auf den dieser **TypeDescriptor** verweist, zu einer **Association** gehört und der **Identifier** in einer Quell- **Entity** der **Association** enthalten ist. <br/> Attributtyp: **String** <br/> |
|**ForeignIdentifierAssociationEntityName** <br/> |Optional.  <br/>  Der Name der **Entity**, die die **Association** enthält, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **ForeignIdentifierAssociationEntityNamespace** und **ForeignIdentifierAssociationName** vorhanden sein. Der Standardwert des Attributs ist der Name der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. <br/> Attributtyp: **String** <br/> |
|**ForeignIdentifierAssociationEntityNamespace** <br/> |Optional.  <br/>  Der Namespace der **Entity**, die die **Association** enthält, auf die der **TypeDescriptor** verweist. Wenn der **TypeDescriptor** nicht auf eine **Association** verweist, darf das Attribut nicht vorhanden sein. Wenn das Attribut vorhanden ist, müssen auch die Attribute **ForeignIdentifierAssociationEntityName** und **ForeignIdentifierAssociationName** vorhanden sein. Der Standardwert des Attributs ist der Namespace der **Entity**, die die **Method** enthält, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. <br/> Attributtyp: **String** <br/> |
|**AssociatedFilter** <br/> |Optional.  <br/>  Der Name für einen **FilterDescriptor**, der dem **TypeDescriptor** zugeordnet ist. Wenn der **TypeDescriptor** nicht einem **FilterDescriptor** zugeordnet ist, darf das Attribut nicht vorhanden sein. <br/> Attributtyp: **String** <br/> |
|**IsCollection** <br/> |Optional.  <br/> Gibt an, ob der **TypeDescriptor** eine einzelne Datenstruktur oder eine Auflistung von Datenstrukturen darstellt. <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**ReadOnly** <br/> |Optional.  <br/> Gibt an, ob die Daten, die von der Datenstruktur gespeichert werden, die durch den **TypeDescriptor** dargestellt wird, geändert werden kann. Dieses Attribut muss nicht angegeben werden, wenn der Wert des **Direction**-Attributs des **Parameters**, der den **TypeDescriptor** enthält, „In“ ist. <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**CreatorField** <br/> |Optional.  <br/> Gibt an, ob der **TypeDescriptor** ein Feld für **MethodInstances** vom Typ **Creator** darstellt, die in der **Method** enthalten sind, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält.  <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**UpdaterField** <br/> |Optional.  <br/>  Gibt an, ob der **TypeDescriptor** ein Feld für **MethodInstances** vom Typ **Updater** darstellt, die in der **Method** enthalten sind, die den **Parameter** enthält, der wiederum den **TypeDescriptor** enthält. Wenn das Attribut angegeben ist, darf kein **PreUpdaterField**-Attribut angegeben werden. <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**PreUpdaterField** <br/> |Optional.  <br/>  Gibt an, ob in der durch den **TypeDescriptor** dargestellten Datenstruktur der letzte Wert gespeichert wird, der vom externen System für ein Feld für **MethodInstances** vom Typ **Updater** empfangen wird. Wenn das Attribut angegeben ist, darf kein **UpdaterField**-Attribut angegeben werden. <br/> Standardwert: **false** <br/> Attributtyp: **Boolean** <br/> |
|**Significant** <br/> |Optional.  <br/>  Gibt an, ob in der durch diesen **TypeDescriptor** dargestellten Datenstruktur gespeicherte Werte bei der Berechnung eines Hashcodes oder beim Vergleichen von in den Datenstrukturen gespeicherten Werten enthalten sind. Beispielsweise wird ein **TypeDescriptor**, der den Nachnamen eines Kunden darstellt, berücksichtigt, wenn ermittelt wird, ob ein Datensatz geändert wurde, und ist daher signifikant. Der **TypeDescriptor**, der das Datum der letzten Änderung des Kundendatensatzes darstellt, wird normalerweise nicht berücksichtigt, wenn ermittelt wird, ob ein Datensatz geändert wurde, und ist daher nicht signifikant. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
|**Name** <br/> |Erforderlich.  <br/> Der Name für den **TypeDescriptor**.  <br/> Attributtyp: **String** <br/> **Hinweis:** Der Name für einen **TypeDescriptor** sollte nicht die Sonderzeichen „/“ (Schrägstrich), „.“ (Punkt) oder „[“ (öffnende eckige Klammer) enthalten.          |
|**DefaultDisplayName** <br/> |Optional.  <br/> Der Anzeigename für den **TypeDescriptor**.  <br/> Attributtyp: **String** <br/> |
|**IsCached** <br/> |Optional.  <br/> Gibt an, ob der **TypeDescriptor** häufig verwendet wird. <br/> Standardwert: **true** <br/> Attributtyp: **Boolean** <br/> |
   
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [LocalizedDisplayNames-Element in "MetadataObject" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Die lokalisierten Namen für den **TypeDescriptor**.  <br/> |
| [Properties-Element in MetadataObject (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Die Eigenschaften für den **TypeDescriptor**.  <br/>  Wenn die **TypeDescriptor** vom Typ **System.String**ist, kann das **Properties** -Element eine **Property** des Typs **System.Int32** mit dem **Name** -Attribut auf **Size**festgelegt enthalten. Der Wert der **Property** gibt die erwartete maximale Länge der Zeichenfolge des Werts der Datenstruktur, die von diesem **TypeDescriptor**beschrieben. <br/> |
| [Interpretation-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Die Regeln für die in der Datenstruktur gespeicherten Daten, die durch den **TypeDescriptor** dargestellt werden.  <br/> |
| [DefaultValues-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx) <br/> |Die Standardwerte für den **TypeDescriptor**.  <br/> |
| [TypeDescriptors-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx) <br/> |Die untergeordneten **TypeDescriptors** des **TypeDescriptor**s.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [TypeDescriptors-Element in "TypeDescriptor" (BDCMetadata-Schema)](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx)||
   

## <a name="typedescriptors-element"></a>TypeDescriptors-Element
<a name="bkmk_TypeDescriptors"> </a>

Gibt eine Liste von **TypeDescriptors** eines übergeordneten TypeDescriptors an.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Schema:** BDCMetadata
  
    
    



```XML
<TypeDescriptors></TypeDescriptors>
```

In den folgenden Abschnitten werden Attribute, untergeordnete und übergeordnete Elemente erläutert.
  
    
    
 **Attribute**
  
    
    
Keine
  
    
    
 **Untergeordnete Elemente**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |Ein **TypeDescriptor**-Objekt.  <br/> |
   
 **Übergeordnetes Element**
  
    
    


|**Element**|**Beschreibung**|
|:-----|:-----|
| [TypeDescriptor-Element (BDCMetadata-Schema)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [TypeDescriptor](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
   

## <a name="see-also"></a>Siehe auch
<a name="bkmk_Addres"> </a>


-  [Änderungen in der BDC-Modell-Schema für SharePoint](changes-in-the-bdc-model-schema-for-sharepoint.md)
    
  
-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
