---
title: "Durchforsten binärer großer Objekte (BLOBs) in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 99b3dd51-1651-4300-a2de-33681f4cc258
ms.openlocfilehash: d7fec8ce2a152b72c80d0a6776947d136638fb13
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="crawl-binary-large-objects-blobs-in-sharepoint"></a>Durchforsten binärer großer Objekte (BLOBs) in SharePoint

In diesem Artikel erfahren sie, wie Sie die BDC-Modelldatei für den BCS-Indizierungsconnector einer Datenbank ändern können, um es dem Suche in SharePoint-Crawler zu ermöglichen, in einer SQL Server-Datenbank gespeicherte BLOB-Daten (Binary Large Object) zu durchforsten.

## <a name="crawling-blob-data"></a>Durchforsten von BLOB-Daten
<a name="HowToCrawlBlobs_CrawlingBlobData"> </a>

Das Business Data Connectivity (BDC)-Dienst unterstützt das Lesen von BLOB-Datentypen eignet sich für das streaming von BLOB-Daten aus externen Systemen. Dies funktioniert müssen Sie sicherstellen, dass die Datenbanktabelle mit den externen Daten eingerichtet ist, um dies zu unterstützen. Sie fügen dann eine **StreamAccessor** -Methode der BDC-Modelldatei für die externe Inhaltsquelle BCS-Indizierungsconnector.
  
    
    

## <a name="configuring-the-sql-server-database-table-for-blob-data"></a>Konfigurieren der SQL Server-Datenbanktabelle für BLOB-Daten
<a name="HowToCrawlBlobs_ConfiguringSQL"> </a>

Die Microsoft SQL Server-Datenbanktabelle muss eine Spalte enthalten, die entweder die Erweiterung oder den MIME-Typ der BLOB-Daten angibt. Wenn das Datenbanktabellenschema keine Spalte mit diesen Informationen aufweist, müssen Sie dem Schema eine solche Spalte hinzufügen. Die folgenden Tabellen enthalten ein Beispiel eines Datenbanktabellenschemas mit dieser Spalte und dazugehörige Beispielwerte, die in der Datenbanktabelle gespeichert sind.
  
    
    

**Tabelle 1. Schema der Beispieldatenbanktabelle**


|**Spaltenname**|**Datentyp**|
|:-----|:-----|
|Id  <br/> |Int  <br/> |
|DisplayName  <br/> |nvarchar(50)  <br/> |
|Erweiterung  <br/> |nvarchar(50)  <br/> |
|Daten  <br/> |varbinary(MAX)  <br/> |
|ContentType  <br/> |nvarchar(MAX)  <br/> |
   

**Tabelle 2. Werte der Beispieldatenbanktabelle**


|**Id**|**Anzeigename**|**Erweiterung**|**Daten**|**Inhaltstyp**|
|:-----|:-----|:-----|:-----|:-----|
|1  <br/> |File1  <br/> |DOCX  <br/> |0x504B…  <br/> |application/vnd.openxmlformats-officedocument.wordprocessingml.document  <br/> |
|2  <br/> |File2  <br/> |.doc  <br/> |0xD…  <br/> |application/msword  <br/> |
|3  <br/> |File3  <br/> |.txt  <br/> |OxE…  <br/> |text/plain  <br/> |
   

## <a name="modifying-the-bdc-model-file-to-enable-crawling-of-blob-data"></a>Ändern der BDC-Modelldatei zum Durchforsten von BLOB-Daten aktivieren
<a name="HowToCrawlBlobs_BDCModelFile"> </a>

Bestätigen Sie, dass die Datenbanktabelle, die Erweiterung oder MIME-Typinformationen für die BLOB-Daten enthält, können Sie Microsoft SharePoint Designer verwenden, um einen externen Inhaltstyp erstellen, der auf die Tabelle mit BLOB-Daten basiert. Anschließend können Sie alle Vorgänge erstellen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen externer Inhaltstypen](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) und [Gewusst wie: Erstellen eines externen Inhaltstyps basierend auf einer SQL Server-Tabelle](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx). 
  
    
    
Nachdem Sie den externen BLOB-Inhaltstyp erstellen, können Sie die BDC-Modelldatei zum ermöglichen der Durchforstung zu ändern. Sie können nicht in SharePoint Designer diese Änderungen vornehmen. Sie müssen so exportieren die Modelldatei BDC und einen XML-Editor verwenden, um diese Änderungen manuell vornehmen.
  
    
    

### <a name="to-export-the-bdc-model-file-for-the-blob-external-content-type"></a>So exportieren Sie die BDC-Modelldatei für den externen BLOB-Inhaltstyp


1. Klicken Sie in SharePoint Designer um die externen Inhaltstypen anzuzeigen, die definiert sind, dass der Website-Anwendung BDC Metadaten speichern im linken Navigationsbereich auf **Externe Inhaltstypen**.
    
  
2. Wählen Sie in der Liste **Externe Inhaltstypen** den externen Inhaltstyp BLOB aus. Klicken Sie dann im Servermenüband auf **BDC-Modell exportieren**.
    
  
3. Geben Sie in das Textfeld **Name des BDC-Modells** einen Namen ein, und klicken Sie dann auf **OK**.
    
  
4. Wählen Sie den Speicherort zum Speichern der BDC-Modelldatei (.bdcm) aus, und klicken Sie dann auf **Speichern**.
    
  

### <a name="to-enable-crawling-of-the-blob-external-content-type"></a>So ermöglichen Sie die Durchforstung des externen BLOB-Inhaltstyps


1. Öffnen Sie in einem XML-Editor die BDC-Modelldatei, die Sie im vorherigen Abschnitt erstellt haben.
    
  
2. Erstellen Sie eine neue Methode, die das BLOB-Feld zurückgibt. Sie müssen eine Methodeninstanz vom Typ **StreamAccessor** für dieses Methode definieren (siehe das folgende Beispiel).
    
    > **Hinweis:** Der Tabellenname lautet in diesem Beispiel „Anlage“. 

```XML
  
<Method Name="GetData">
  <Properties>
    <Property Name="RdbCommandText" Type="System.String">SELECT Data FROM [dbo].[Attachment] WHERE [Id] = @Id </Property>
    <Property Name="RdbCommandType" Type="System.Data.CommandType, System.Data, Version=2.0.0.0, Culture=neutral, 
      PublicKeyToken=b77a5c561934e089">Text</Property>
  </Properties>
  <Parameters>
    <Parameter Direction="In" Name="@Id">
      <TypeDescriptor TypeName="System.Int32" IdentifierName="Id" Name="Id" />
    </Parameter>
    <Parameter Name="StreamData" Direction="Return">
      <TypeDescriptor TypeName="System.Data.IDataReader, System.Data, 
        Version=2.0.3600.0, Culture=neutral, 
        PublicKeyToken=b77a5c561934e089" 
        IsCollection="true" Name="DataReaderTypeDescriptorName">
        <TypeDescriptors>
          <TypeDescriptor TypeName="System.Data.IDataRecord, System.Data, 
            Version=2.0.3600.0, 
            Culture=neutral, 
            PublicKeyToken=b77a5c561934e089" 
            Name="DataRecordTypeDescriptorName">
            <TypeDescriptors>
              <TypeDescriptor TypeName="System.Data.SqlTypes.SqlBytes, System.Data, 
                Version=2.0.3600.0, 
                Culture=neutral, 
                PublicKeyToken=b77a5c561934e089" Name="Data" />
            </TypeDescriptors>
          </TypeDescriptor>
        </TypeDescriptors>
      </TypeDescriptor>
     </Parameter>
    </Parameters>
  <MethodInstances>
    <MethodInstance Name="DataAccessor" 
      Type="StreamAccessor" 
      ReturnParameterName="StreamData" 
      ReturnTypeDescriptorName="Data">
      <Properties>
<!-- If extension field is available-->
        <Property Name="Extension" Type="System.String">Extension</Property>
<!--If MimeType is available-->
        <Property Name="ContentType" Type="System.String">ContentType</Property>
<!--If attachments is to be displayed in profile pages, add the following property-->
        <Property Name="MimeTypeField" Type="System.String">ContentType</Property>
      </Properties>
    </MethodInstance>
  </MethodInstances>
</Method>
```


    If the MIME type is the same for all the BLOBs, you can replace this line of code from the previous example: 
  
    
    
 `<Property Name="ContentType" Type="System.String">ContentType</Property>`
  
    
    
durch den folgenden Code: 
  
    
    
 `<Property Name=" ContentType " Type="System.String">application/vnd.openxmlformats-officedocument.wordprocessingml.document</Property>`
    
  
3. Erneutes Importieren der Modelldatei mithilfe der Business Connectivity Services Service-Anwendung administrationsanwendungs-Benutzeroberfläche. 
    
  
4. Erstellen Sie die Inhaltsquelle für den externen Inhaltstyp.
    
  
5. Starten Sie eine vollständige Durchforstung der Inhaltsquelle. 
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Crawlblobs_addlresources"> </a>


-  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen externer Inhaltstypen](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx)
    
  
-  [XML-Ausschnitt: Modellieren einer StreamAccessor-Methode](http://msdn.microsoft.com/library/bd60cc2e-f7f6-421c-9d2a-60e8512b9893%28Office.15%29.aspx)
    
  

