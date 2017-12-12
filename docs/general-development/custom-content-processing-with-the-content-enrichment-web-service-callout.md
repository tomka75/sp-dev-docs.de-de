---
title: Benutzerdefinierte Inhaltsverarbeitung mit der Content Enrichment-Webdienstlegende
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bdda92c8-9c8d-416e-9a6b-4a9373686fa0
ms.openlocfilehash: 7aa11f7002ab6c8440311d69a1869c303d6da617
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="custom-content-processing-with-the-content-enrichment-web-service-callout"></a>Benutzerdefinierte Inhaltsverarbeitung mit der Content Enrichment-Webdienstlegende
Informationen Sie zu den Content inhaltsanreicherung in SharePoint, die Entwickler zum Erstellen eines externen Webdiensts um verwaltete Eigenschaften für durchforsteten Elemente während der inhaltsverarbeitung ändern können. Suche in SharePoint ermöglicht Benutzern, die verwalteten Eigenschaften der durchforsteten Elemente zu ändern, bevor sie durch Aufrufen von an einen Webdienst externe inhaltserweiterung indiziert sind. Die Möglichkeit zum Ändern von verwalteter Eigenschaften für Elemente während der inhaltsverarbeitung ist hilfreich, beim Ausführen von Aufgaben wie DatenBereinigung, entitätsextraktion, Klassifizierung und Kategorien.
  
    
    


**Abbildung 1. Inhaltserweiterung innerhalb der inhaltsverarbeitung**

  
    
    

  
    
    
![Inhaltserweiterung innerhalb der Inhaltsverarbeitung](../images/SP15_Content_Enrichment.gif)
  
    
    
Abbildung 1 zeigt einen Teil des Prozesses, der in der inhaltsverarbeitungskomponente stattfindet. Der inhaltserweiterung-Webdienst ist eine SOAP-basierten Dienst, den Sie erstellen können, um eine Legende aus dem Web-Service-Client innerhalb der inhaltsverarbeitungskomponente empfangen. Basierend auf Abbildung 1, verweist der WebClient-Dienst auf den Operator Anreicherung Inhalte innerhalb der inhaltsverarbeitungskomponente; derWebdienst bezieht sich auf die SOAP-Webdienst, den Sie implementieren.Der Webdienst erhält eine konfigurierbare Nutzlast von der inhaltsverarbeitungskomponente. Klicken Sie dann, wird die resultierende Antwort vom Webdienst mit durchforsteten Elements zusammengeführt, bevor es dem Suchindex hinzugefügt wird.Der Dienst WebClient arbeitet mit verwalteten Eigenschaften, die Sie als Eingabeeigenschaften oder als Ausgabeeigenschaften konfigurieren können. Eingabeeigenschaften werden an den Webdienst gesendet. Ausgabeeigenschaften werden durch den Webdienst zurückgegeben. Bestimmte verwalteten Eigenschaften werden ausgeblendet oder sind schreibgeschützt und können nicht an den Webdienst gesendet oder empfangen aus dem Webdienst werden. Informationen zum überprüfen die verwalteten Eigenschaften schreibgeschützt sind finden Sie unter  [Gewusst wie: Auflisten aller schreibgeschützte verwaltete Eigenschaften für den Webdienst Inhaltserweiterung](#SP15contentprocess_read-only_managed_properties) .
    
> **Wichtig:** Der Schritt der Inhaltserweiterungslegende kann nur mit einem einzigen Webdienstendpunkt konfiguriert werden. Jegliche Art von Fehlertoleranz oder Routingfunktionen zur Unterstützung mehrerer Implementierungen müssen vom Entwickler bei der Implementierung des Webdiensts behandelt werden. Darüber hinaus kann der Entwickler über verschiedene Webdienstimplementierungen verfügen, die auf unterschiedlichen Endpunkten gehostet werden. Es kann jedoch immer nur einer dieser Endpunkte in der Konfiguration verwendet werden. 
  
    
    


## <a name="content-enrichment-web-service-contract"></a>Vertrag für den Inhaltserweiterungs-Webdienst
<a name="SP15webservcallout_enrich"> </a>

Web-Service-Client ist ein SOAP (Version 1.1) RPC-Client mit einer vordefinierten Verhalten. Servicevertrag Web weist folgende Merkmale auf:
  
    
    

- Die inhaltsverarbeitungskomponente sendet einen SOAP-RPC-Aufruf an einen konfigurierbaren Endpunkt über HTTP.
    
  
- Nutzlast enthält ein Array von Property-Objekten.
    
  
- Der Webdienst führt eine benutzerdefinierte Logik für das Array von Property-Objekte und gibt ein Array von geänderten oder neuen Property-Objekten.
    
  
- Der Webdienst muss eine Antwort an den Dienst WebClient einer angegebenen Timeout senden.
    
  
- Keine bestimmten Authentifizierung oder Verschlüsselung Mechanismen werden im Rahmen des Vertrags unterstützt. Sie können jedoch eigene Sicherheit des Transport-Mechanismus anwenden.
    
  

## <a name="configuring-the-content-enrichment-web-service-client"></a>Konfigurieren des Inhaltserweiterung Web Service-Clients
<a name="content_enrichment_configuration"> </a>

Um die Webdienstclients zu konfigurieren, verwenden Sie die folgenden Windows PowerShell-Cmdlets:
  
    
    

-  [Get-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219783%28office.15%29.aspx)
    
  
-  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)
    
  
-  [Remove-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219742%28office.15%29.aspx)
    
  
-  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx)
    
  
Tabelle 1 enthält die Eigenschaften, die Sie über die weiter oben erwähnten Windows PowerShell-Cmdlets konfigurieren können.
  
    
    

**In Tabelle 1. Eigenschaften, die für den Client konfiguriert werden mithilfe von Windows PowerShell-cmdlets**


|**Configuration-Eigenschaft**|**Beschreibung**|**Standardwert**|
|:-----|:-----|:-----|
|**Endpunkt** <br/> |Gibt die URL des externen Webdiensts.  <br/> |Leer  <br/> |
|**InputProperties** <br/> |Die verwalteten Eigenschaften, die der externen Webdienst empfängt.  <br/> |Leer  <br/> |
|**OutputProperties** <br/> |Die verwalteten Eigenschaften, die vom externen Webdienst zurückgegeben.  <br/> |Leer  <br/> |
|**Timeout** <br/> |Die Zeitdauer, bis die Web Servicezeiten in Millisekunden.  <br/> Je nach **FailureMode** das Element kann nicht verarbeitet werden, oder eine Warnung ausgegeben wird in den ULS-Protokolldateien geschrieben. <br/> |5000 Millisekunden; Gültige Bereich [100, 30000].  <br/> |
|**SendRawData** <br/> |Aktiviert oder deaktiviert unformatierte Daten an den Webdienst senden.  <br/> |Falsch.  <br/> |
|**MaxRawDataSize** <br/> |Die maximale Größe des unformatierte Daten an den Webdienst in Kilobyte (KB) gesendet. Wenn die binären Daten eines Elements diesen Grenzwert überschreitet, wird das Element nicht gesendet. Dies verhindert nicht die **InputProperties** gesendet werden, und die **OutputProperties** empfangen wird. <br/> |5120 KB.  <br/> |
|**FailureMode** <br/> |Steuert das Verhalten des Web Service-Clients treten Fehler auf. Wenn **FailureMode** auf **ERROR**festgelegt ist, Senden von Problemen, die während der Verarbeitung inhaltserweiterung auftreten einen fehlerhaften Rückruf für den betreffenden Artikel. <br/> Wenn **FailureMode** auf **WARNING**festgelegt ist, das Element wird ohne Modifikationen vom Webdienst indiziert und eine Warnung ausgegeben wird in den ULS-Protokolldateien geschrieben.  <br/> |Fehler  <br/> |
|**DebugMode** <br/> |Ein Modus, die bei Festlegung auf **true** ermöglicht den Client die inhaltserweiterung alle verwaltete Eigenschaften an den Client gesendet, ohne alle Eigenschaften in den Rückgabetypen erwartet. Alle konfigurierten **Trigger** -Eigenschaft, die **InputProperties** -Eigenschaft und die **OutputProperties** -Eigenschaft werden ignoriert. <br/> |Falsch.  <br/> |
|**Trigger** <br/> |Ein **Boolean** -Prädikat, das für alle durchforsteten Elemente ausgeführt wird. Wenn das Prädikat **true** ergibt, wird der Datensatz an den Webdienst gesendet. Andernfalls wird das Element über dem Suchindex übergeben. <br/> |Leer  <br/> |
   

### <a name="how-to-list-all-read-only-managed-properties-for-the-content-enrichment-web-service"></a>Gewusst wie: Auflisten aller schreibgeschützte verwaltete Eigenschaften für den Webdienst Inhaltserweiterung
<a name="SP15contentprocess_read-only_managed_properties"> </a>

Bestimmte verwalteten Eigenschaften sind schreibgeschützt und können nicht aus dem Webdienst ausgegeben werden. Diese Eigenschaften können aufgelistet werden, mithilfe von  [Get-SPEnterpriseSearchServiceApplication](http://technet.microsoft.com/de-DE/library/ff608050%28office.15%29.aspx) und [Get-SPEnterpriseSearchMetadataManagedProperty](http://technet.microsoft.com/de-DE/library/ff607560%28office.15%29.aspx)Windows PowerShell-Cmdlets, im folgenden Beispiel dargestellt:
  
    
    

```

$ssa = Get-SPEnterpriseSearchServiceApplication
Get-SPEnterpriseSearchMetadataManagedProperty -SearchApplication $ssa  | ?{$_.IsReadOnly -or $_.MappingDisallowed -or $_.DeleteDisallowed}

```


## <a name="about-trigger-conditions-for-configuring-the-web-service-callout"></a>Informationen zu Trigger Bedingungen für die Konfiguration des Webdienst-callout
<a name="SP15contentprocess_trigger"> </a>

Eine Trigger-Bedingung ist ein Ausdruck, mit denen das Webdienst-Callout konfiguriert ist. Ergibt eine Bedingung für den Auslöser **true**, führt der Web Service-Client eine Legende für diesen Datensatz. Ergibt eine Bedingung für den Auslöser **false**, der Web-Service-Client führt keine Legende und übergibt das durchforstete Element an den Suchindex. Sie können auch, wenn die Bedingung keine Trigger konfiguriert ist. alle Elemente werden an den Webdienst gesendet.
  
    
    
Trigger verwendet eine Ausdruckssprache verweisen auf die Werte der verwalteten Eigenschaften. Sie können Operatoren und Funktionen in der Ausdruckssprache verwenden, einfache oder komplexe Trigger Conditions erstellen, damit Sie ermitteln können, wenn ein Webdienst-Callout ausführen. 
  
    
    
Tabelle 2 enthält Beispiele für Trigger Bedingungen.
  
    
    

**In Tabelle 2. Trigger-Bedingung-Beispiele für die Konfiguration von inhaltsanreicherung**


|**Ausdruck**|**Beschreibung**|**Anforderungen**|
|:-----|:-----|:-----|
|MP1 > 2  <br/> |Gibt **true** zurück, wenn der Wert der verwalteten Eigenschaft namens MP1 größer als 2 ist. <br/> |MP1 muss es sich um einen numerischen Typ verfügen.  <br/> |
|IsNull(MP2)  <br/> |Gibt die **true** zurück, wenn die verwaltete Eigenschaft namens MP2 nicht für die durchforsteten Element vorhanden ist, oder leere/Null ist. <br/> |MP2 kann eines beliebigen Typs sein.  <br/> |
|StartsWith(MP1, "sample") und MP2! = 18  <br/> |Gibt **true** zurück, wenn der Wert in der verwalteten Eigenschaft MP1 mit "Sample beginnt" und des Werts der verwalteten Eigenschaft MP2 nicht 18. <br/> |MP1 muss vom Typ **string** und MP2 muss einen numerischen Typ. <br/> |
|IsDay (MP1, 2009, 12, 24)  <br/> |Überprüft, ob die verwaltete Eigenschaft MP1 eine **DateTime** enthält, die auf 24 Dezember 2009 fällt. <br/> |MP1 muss vom Typ **DateTime**sein.  <br/> |
   
Finden Sie unter  [Syntax für Trigger Ausdrücken in SharePoint](trigger-expressions-syntax-in-sharepoint.md) für Elemente, die in einem Ausdruck Trigger und eine Liste der unterstützten Funktionen verwendet werden können.
  
    
    

## <a name="implementing-the-content-enrichment-external-web-service"></a>Implementieren den externen Webdienst Inhaltserweiterung
<a name="SP15contentprocess_implement"> </a>

Führen Sie für eine einfache Implementierung folgende Schritte aus: 
  
    
    

1. Enthalten Sie die **Microsoft.Office.Server.Search.ContentProcessingEnrichment.dll** befindet sich im `C:\\Program Files\\Microsoft Office Servers\\15.0\\Search\\Applications\\External` in Ihrem Projekt als Referenz.
    
  
2. Implementieren Sie **IContentProcessingEnrichmentService** als Webdienst.
    
  

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Konfigurieren der Suche in SharePoint](configure-search-in-sharepoint.md)
    
  
-  [Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

