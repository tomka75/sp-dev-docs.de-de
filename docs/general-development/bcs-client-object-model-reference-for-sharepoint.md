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
# <a name="bcs-client-object-model-reference-for-sharepoint"></a>BCS-Client-Objektmodellreferenz für SharePoint

  
    
    
![Klassenbibliotheken und -verweise](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
Informationen Sie zu den Objekten, die für das Erstellen von clientseitigen Skripts mithilfe des Clientobjektmodells SharePoint Zugriff auf externe Daten verfügbar gemacht werden, indem Business Connectivity Services (BCS) verfügbar sind. Die folgenden Objekte stehen für die Erstellung von clientseitigen Skripts mithilfe des Clientobjektmodells SharePoint Zugriff auf externe Daten, die von Business Connectivity Services (BCS) verfügbar gemacht wird. Die BCS-Objektmodell Komponenten, die dem Client-Objektmodell verfügbar gemacht werden, in denen Microsoft.SharePoint.Client.dll befinden.
  
    
    


## <a name="entity-object"></a>Entity-Objekt
<a name="bkmk_Entity"> </a>

Das **Entity** -Objekt stellt im Wesentlichen eine Tabelle in einer Datenbank. Die Methoden und Eigenschaften, die hier aufgeführten die Objekte anzeigen, die bearbeitet werden können durch Verwendung der Clientbibliothek Code. Jede dieser Anrufe ordnet direkt zu einem Modell-Anruf von Server-Objekt. Jedoch können sie von einem getrennten Client, wie in einem Webbrowser mit JavaScript aufgerufen werden.
  
    
    

**Methoden**


|**Methoden**|**Methodensignatur**|**Beschreibung**|
|:-----|:-----|:-----|
|**Create** <br/> | `Identity Create(FieldValueDictionary fieldValues, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindSpecificDefault** <br/> | `EntityInstance FindSpecificDefault(Identity identity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindspecificByBdcIDDefault** <br/> | `EntityInstance FindSpecific(Identity identity, string specificFinderName, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindSpecificByBdcID** <br/> | `EntityInstance FindSpecificByBdcIDDefault(string BdcIdentity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**GetCreatorView** <br/> | `EntityInstance FindSpecificByBdcID(string BdcIdentity, string specificFinderName,LobSystemInstance LobSystemInstanceName)` <br/> ||
|**GetDefaultSpecificFinderView** <br/> | `View GetCreatorView(string methodInstanceName)` <br/> ||
|**GetSpecificFinderView_Client** <br/> | `View GetDefaultSpecificFinderView()` <br/> ||
|**GetUpdaterView_Client** <br/> | `View GetSpecificFinderView_Client( string specificFinderName)` <br/> ||
|**GetIdentifiers** <br/> | `View GetUpdaterView_Client(string updaterName)` <br/> ||
|**GetIdentifiers()** <br/> |||
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
| `long EstimatedInstanceCount { get; }` <br/> |Ruft die Anzahl der erwarteten externen Elemente dieses externen Inhaltstyps ab.  <br/> |
| `string Name { get; }` <br/> |Ruft den Namen des Metadatenobjekts ab.  <br/> |
| `string Namespace { get; }` <br/> |Ruft den Namespace der angegebenen Daten-Klasse.  <br/> |
| `int GetIdentifierCount()` <br/> ||
   

## <a name="entityinstance-method"></a>EntityInstance-Methode
<a name="bkmk_EntityInstance"> </a>


**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP.BusinessData.Runtime** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**Delete** <br/> |void  <br/> |Löscht das externe Element.  <br/> |
|**FromXml** <br/> |void  <br/> |Die Werte festgelegt aus der angegebenen XML in diesem Wörterbuch.  <br/> **Methodensignatur**          `FromXml(string xml)` <br/> |
|**GetIdentity** <br/> |Identität  <br/> |Ruft die Identität des externen Elements ab.  <br/> |
|**Delete** <br/> |void  <br/> |Löscht das externe Element.  <br/> |
|**ToXml** <br/> |string  <br/> |Ruft die Werte im XML-Format ab.  <br/> |
|**Update** <br/> |void  <br/> |Sendet Änderungen an externen Elements an.  <br/> |
   

  
    
    

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
| `this[string fieldDotNotation] { get; set; }` <br/> |Object  <br/> |Dient zum Abrufen oder Festlegen des Werts des Felds, die durch die punktierte Schreibweise bezeichnet wird.  <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |string  <br/> ||
   

## <a name="entityview-method"></a>EntityView-Methode
<a name="bkmk_entityview"> </a>

Gibt eine benutzerdefinierte Ansicht der **Entität** Daten
  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP.BusinessData** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**GetDefaultValues_Client()** <br/> |**FieldValueDictionary** <br/> |Ruft ein Wörterbuch der Feld-Wert, der die Standardwerte für diese Ansicht enthält.  <br/> |
|**GetXmlSchema()** <br/> |**Zeichenfolge** <br/> |Ruft das XML-Schema der Ansicht ab.  <br/> |
|**GetType(string fieldDotNotation)** <br/> |**Zeichenfolge** <br/> |Ruft den Typ des angegebenen Felds ab.  <br/> |
|**GetType(string fieldDotNotation)** <br/> |**TypeDescriptor** <br/> |Ruft das **TypeDescriptor** -Objekt, das die angegebene punktierte Schreibweise entspricht. <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
| `Fields { get; }` <br/> |**FieldCollection** <br/> |Ruft die Auflistung von Feldern in der Ansicht ab.  <br/> |
| `Name { get; }` <br/> |**Zeichenfolge** <br/> |Ruft den Namen dieses **View** -Objekts <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |**Zeichenfolge** <br/> |Ruft den Namen der spezifischen Finder- **MethodInstance**, die in dieser Ansicht an gebunden ist. <br/> |
   

## <a name="lobsystem-method"></a>LobSystem-Methode
<a name="bkmk_LobSystem"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP.BusinessData** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**GetLobSystemInstances()** <br/> |**void** <br/> |Gibt die Liste der LOB-Systeminstanzen an.  <br/> |
|**Name** <br/> |**void** <br/> |Ruft den Namen der **LobSystem**ab.  <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|Keine.  <br/> ||
   

## <a name="lobsysteminstance-method"></a>LobSystemInstance-Methode
<a name="bkmk_LobSystemInstance"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP.BusinessData** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|Keine.  <br/> |**void** <br/> ||
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|Keine.  <br/> ||
   

## <a name="identifier-method"></a>ID-Methode
<a name="bkmk_Identifier"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP.BusinessData** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName** <br/> |**bool** <br/> |Bestimmt, ob das Metadatenobjekt lokalisierten Anzeigenamen enthält.  <br/> |
|**GetDefaultDisplayName** <br/> |**Zeichenfolge** <br/> |Der standardmäßige Anzeigename zurückgegeben.  <br/> |
|**GetLocalizedDisplayName** <br/> |**Zeichenfolge** <br/> |Gibt den lokalisierten Anzeigenamen zurück.  <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
| `IdentifierType {get;}` <br/> |**Zeichenfolge** <br/> |Gibt den Typ des Bezeichners.  <br/> |
| `Name {get;}` <br/> |**Zeichenfolge** <br/> |Ruft den Namen des Bezeichners ab.  <br/> |
   

## <a name="identifiercollection-method"></a>IdentifierCollection-Methode
<a name="bkmk_IdentifierCollection"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel.Collections** <br/> |**SP.BusinessData.Collections** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|Keine.  <br/> |**void** <br/> ||
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|Keine.  <br/> ||
   

## <a name="identity-method"></a>Identity-Methode
<a name="bkmk_Identity"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP.BusinessData.Runtime** <br/> |
   

**Konstruktor**


|**Konstruktor**|**Beschreibung**|
|:-----|:-----|
| `public Identity (Object[] identifierValues)` <br/> |Erstellt eine neue Instanz der Klasse mithilfe von ein Array von ID-Werte.  <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**Serialize** <br/> |**Zeichenfolge** <br/> |Ruft eine Zeichenfolgendarstellung der Identität ab.  <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
| `IdentifierCount { get; }` <br/> |**int** <br/> |Gibt die Anzahl der Bezeichner zurück.  <br/> |
| `IsTemporary { get; }` <br/> |**bool** <br/> |Überprüft, ob die Identität temporär ist.  <br/> |
| `this[int identifierIndex] { get; }` <br/> |**Objekt** <br/> |Ruft das Element am angegebenen Index ab. CSOM unterstützt Int-basierte Indizierung nicht. Basis-Accessor für den gleichen implementiert.  <br/> |
| `TemporaryId { get; }` <br/> |**Guid** <br/> |Gibt den temporären Teil der Identität zurück.  <br/> |
   

## <a name="fieldvaluedictionary-method"></a>Abgerufenen "FieldValueDictionary"-Methode
<a name="bkmk_FieldValueDictionary"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP.BusinessData.Runtime** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**FromXml** <br/> |**void** <br/> |Die Werte festgelegt aus der angegebenen XML in diesem Wörterbuch.  <br/> |
|**GetCollectionSize** <br/> |int  <br/> |Gibt die Größe der Auflistung, der auf die punktierte Schreibweise verweist.  <br/> |
|**ToXml** <br/> |string  <br/> |Ruft die Werte im XML-Format ab.  <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
| `Object this[string fieldDotNotation] { get; set; }` <br/> |Dient zum Abrufen oder Festlegen des Werts des Felds, die durch die punktierte Schreibweise bezeichnet wird.  <br/> |
   

## <a name="entityfieldcollection-method"></a>EntityFieldCollection-Methode
<a name="bkmk_EntityFieldCollection"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP.BusinessData.Runtime** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|Keine.  <br/> |**void** <br/> ||
   

**Eigenschaften**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|Keine.  <br/> ||
   

## <a name="entityfield-method"></a>EntityField-Methode
<a name="bkmk_Entityfield"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP.BusinessData.Runtime** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|Keine.  <br/> |void  <br/> ||
   

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Schreibgeschützt**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName** <br/> |**Boolean** <br/> |Ja  <br/> |Bestimmt, ob das Feld einen lokalisierten Anzeigenamen enthält.  <br/> |
|**DefaultDisplayName** <br/> |**Zeichenfolge** <br/> |Ja  <br/> |Der standardmäßige Anzeigename des Felds abgerufen.  <br/> |
|**GetLocalizedDisplayName** <br/> |**Zeichenfolge** <br/> ||Ruft den lokalisierten Anzeigenamen des Felds ab.  <br/> |
|**Name** <br/> |**Zeichenfolge** <br/> |Ja  <br/> |Ruft den Namen des Felds ab.  <br/> |
   

## <a name="typedescriptor-class"></a>TypeDescriptor-Klasse
<a name="bkmk_TypeDescriptor"> </a>


  
    
    

**Namespaces**


|**Verwaltet**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP.BusinessData** <br/> |
   

**Methoden**


|**Methode**|**Rückgabetyp**|**Schreibgeschützt**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName()** <br/> |**Boolean** <br/> |Ja  <br/> |Bestimmt, ob der Typdeskriptor einen lokalisierten Anzeigenamen enthält.  <br/> |
|**GetLocalizedDisplayName()** <br/> |**Zeichenfolge** <br/> |Ja  <br/> |Gibt den lokalisierten Anzeigenamen zurück.  <br/> |
|**GetDefaultDisplayName()** <br/> |**Zeichenfolge** <br/> ||Der standardmäßige Anzeigename zurückgegeben.  <br/> |
   

**Eigenschaften**


|**Eigenschaft**|**Rückgabetyp**|**Beschreibung**|
|:-----|:-----|:-----|
|**Name** <br/> |string  <br/> |Ruft den Namen des Felds ab.  <br/> |
|**TypeName** <br/> |string  <br/> |Ruft den Namen des Datentyps durch diesen Typdeskriptor dargestellt.  <br/> |
|**IsReadOnly** <br/> |Boolescher Wert  <br/> |Bestimmt, ob dieser Typdeskriptor eine nur-Lese-Datenstruktur darstellt.  <br/> |
|**ContainsReadOnly** <br/> |Boolescher Wert  <br/> |Bestimmt, ob dieser Typdeskriptor oder eines der untergeordneten eine nur-Lese-Datenstruktur darstellen.  <br/> |
|**IsCollection** <br/> |Boolescher Wert  <br/> |Bestimmt, ob der beschriebene Typ eine Datenstruktur Auflistung darstellt.  <br/> |
   

## <a name="interfaces"></a>Schnittstellen
<a name="bkmk_Interfaces"> </a>

Der Namespace ist **Microsoft.BusinessData.MetadataModel**.
  
    
    


|**Schnittstelle**|**Beschreibung**|
|:-----|:-----|
|**IMetadataCatalog** <br/> |Der Einstiegspunkt in das BDC-Objektmodell. Verwenden Sie die **DatabaseBasedMetadataCatalog** auf dem Server.<br/> |
|**ILobSystem** <br/> |Enthält die Details zu einem externen System.  <br/> |
|**IEntity** <br/> |Ein externer Inhaltstyp im BDC-Metadatenspeicher.  <br/> |
|**IMethod** <br/> |Ein Vorgang, der für den externen Inhaltstyp ausgeführt werden kann.  <br/> |
|**IEntityInstance** <br/> |Eine Entitätsinstanz (auch bekannt als externes Element) ist ein einzelnes Element in einem externen System im BDC zurückgegeben.  <br/>  Die Schnittstelle **IEntityInstance** abstrahiert die zugrunde liegenden Datenquellen und isoliert von anwendungsspezifischen Codierung Paradigmen erfahren, dass die Clients; Sie können alle Geschäftsdaten in eine einzige, vereinfachte Möglichkeit zugreifen. Mithilfe der **IEntityInstance** -Schnittstelle können Sie mit einer Reihe von Daten aus einer Datenbank in genauso wie Arbeiten mit einer komplexen .NET Framework-Struktur, die von einem Webdienst zurückgegeben arbeiten. <br/>  Eine Entitätsinstanz im BDC-hat spezielle Semantik angefügt. Er hat die Möglichkeit, wissen, welches Feld oder Felder in der Zeile den Bezeichner für die Entitätsinstanz darstellen, und es ermöglicht Ihnen das Aufrufen von Methoden, wie **GetAssociated**, **GetIdentifierValues**und **Execute**, für diese Entitätsinstanz. <br/> |
|**IEntityInstanceEnumerator** <br/> |Enumeratoren zum Lesen der Daten in der externen Items-Auflistung verwendet werden, jedoch nicht zum Ändern der zugrunde liegenden Auflistung verwendet werden. **IEntityInstanceEnumerator** unterstützt streaming und ist daher sehr nützlich, wenn die Back-End-Anwendung große Datenmengen zurückgibt.<br/> |
   

## <a name="client-object-model-faq"></a>Client Object Model - häufig gestellte Fragen
<a name="bkmk_ClientObjectModelFAQ"> </a>


- **Muss das <Method>-Tag beim Abfragen einer externen Liste in einer CAML-Abfrage enthalten sein?**
    
    Nein. 
    
  
- **Müssen alle Felder in der externen Liste in der CAML-Abfrage angegeben werden?**
    
    Über den ViewXML-Tag im BDC-Modell der Entwickler kann angeben, dass nur die Felder, die erforderlich sind, und die CSOM-APIs für Listen gibt nur die Felder zurück.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_Addres"> </a>


-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [.NET-Client-API-Referenz für SharePoint](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx)
    
  
-  [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Vorgehensweise: Verwenden Sie die Code-Clientbibliothek Zugriff auf externe Daten in SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
