---
title: Vorgehensweise durchforsten binary large Objects () in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 99b3dd51-1651-4300-a2de-33681f4cc258
ms.openlocfilehash: 6189c821032c5e6707bdc6d699dace29cdb77f64
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-crawl-binary-large-objects-blobs-in-sharepoint"></a><span data-ttu-id="8d5ba-102">Vorgehensweise: durchforsten binary large Objects () in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8d5ba-102">How to: Crawl binary large objects (BLOBs) in SharePoint</span></span>
<span data-ttu-id="8d5ba-103">In diesem Artikel erfahren sie, wie Sie die BDC-Modelldatei für den BCS-Indizierungsconnector einer Datenbank ändern können, um es dem Suche in SharePoint-Crawler zu ermöglichen, in einer SQL Server-Datenbank gespeicherte BLOB-Daten (Binary Large Object) zu durchforsten.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-103">Learn how to modify the BDC model file for a database BCS indexing connector to enable the Search in SharePoint crawler to crawl binary large object (BLOB) data stored in a SQL Server database.</span></span>
## <a name="crawling-blob-data"></a><span data-ttu-id="8d5ba-104">Durchforsten von BLOB-Daten</span><span class="sxs-lookup"><span data-stu-id="8d5ba-104">Crawling BLOB data</span></span>
<span data-ttu-id="8d5ba-105"><a name="HowToCrawlBlobs_CrawlingBlobData"> </a></span><span class="sxs-lookup"><span data-stu-id="8d5ba-105"></span></span>

<span data-ttu-id="8d5ba-p101">Das Business Data Connectivity (BDC)-Dienst unterstützt das Lesen von BLOB-Datentypen eignet sich für das streaming von BLOB-Daten aus externen Systemen. Dies funktioniert müssen Sie sicherstellen, dass die Datenbanktabelle mit den externen Daten eingerichtet ist, um dies zu unterstützen. Sie fügen dann eine **StreamAccessor** -Methode der BDC-Modelldatei für die externe Inhaltsquelle BCS-Indizierungsconnector.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-p101">The Business Data Connectivity (BDC) service supports reading BLOB data types, which is useful for streaming BLOB data from external systems. For this to work, you need to ensure that the database table containing the external data is set up to support this. You then add a **StreamAccessor** method to the BDC model file for the external content source's BCS indexing connector.</span></span>
  
    
    

## <a name="configuring-the-sql-server-database-table-for-blob-data"></a><span data-ttu-id="8d5ba-109">Konfigurieren der SQL Server-Datenbanktabelle für BLOB-Daten</span><span class="sxs-lookup"><span data-stu-id="8d5ba-109">Configuring the SQL Server database table for BLOB data</span></span>
<span data-ttu-id="8d5ba-110"><a name="HowToCrawlBlobs_ConfiguringSQL"> </a></span><span class="sxs-lookup"><span data-stu-id="8d5ba-110"></span></span>

<span data-ttu-id="8d5ba-p102">Die Microsoft SQL Server-Datenbanktabelle muss eine Spalte enthalten, die entweder die Erweiterung oder den MIME-Typ der BLOB-Daten angibt. Wenn das Datenbanktabellenschema keine Spalte mit diesen Informationen aufweist, müssen Sie dem Schema eine solche Spalte hinzufügen. Die folgenden Tabellen enthalten ein Beispiel eines Datenbanktabellenschemas mit dieser Spalte und dazugehörige Beispielwerte, die in der Datenbanktabelle gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-p102">The Microsoft SQL Server database table must have a column that specifies either the extension or the MIME type of the BLOB data. If the database table schema does not include a column with this information, you must add it to the schema. The following tables contain an example of a database table schema with this column and sample values for it that are stored in the database table.</span></span>
  
    
    

<span data-ttu-id="8d5ba-114">**Tabelle 1. Schema der Beispieldatenbanktabelle**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-114">**Table 1. Sample database table schema**</span></span>


|<span data-ttu-id="8d5ba-115">**Spaltenname**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-115">**Column Name**</span></span>|<span data-ttu-id="8d5ba-116">**Datentyp**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-116">**Data Type**</span></span>|
|:-----|:-----|
|<span data-ttu-id="8d5ba-117">Id</span><span class="sxs-lookup"><span data-stu-id="8d5ba-117">Id</span></span>  <br/> |<span data-ttu-id="8d5ba-118">Int</span><span class="sxs-lookup"><span data-stu-id="8d5ba-118">Int</span></span>  <br/> |
|<span data-ttu-id="8d5ba-119">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8d5ba-119">DisplayName</span></span>  <br/> |<span data-ttu-id="8d5ba-120">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="8d5ba-120">nvarchar(50)</span></span>  <br/> |
|<span data-ttu-id="8d5ba-121">Erweiterung</span><span class="sxs-lookup"><span data-stu-id="8d5ba-121">Extension</span></span>  <br/> |<span data-ttu-id="8d5ba-122">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="8d5ba-122">nvarchar(50)</span></span>  <br/> |
|<span data-ttu-id="8d5ba-123">Daten</span><span class="sxs-lookup"><span data-stu-id="8d5ba-123">Data</span></span>  <br/> |<span data-ttu-id="8d5ba-124">varbinary(MAX)</span><span class="sxs-lookup"><span data-stu-id="8d5ba-124">varbinary(MAX)</span></span>  <br/> |
|<span data-ttu-id="8d5ba-125">ContentType</span><span class="sxs-lookup"><span data-stu-id="8d5ba-125">ContentType</span></span>  <br/> |<span data-ttu-id="8d5ba-126">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="8d5ba-126">nvarchar(MAX)</span></span>  <br/> |
   

<span data-ttu-id="8d5ba-127">**Tabelle 2. Werte der Beispieldatenbanktabelle**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-127">**Table 2. Sample database table values**</span></span>


|<span data-ttu-id="8d5ba-128">**Id**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-128">**Id**</span></span>|<span data-ttu-id="8d5ba-129">**Anzeigename**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-129">**Display Name**</span></span>|<span data-ttu-id="8d5ba-130">**Erweiterung**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-130">**Extension**</span></span>|<span data-ttu-id="8d5ba-131">**Daten**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-131">**Data**</span></span>|<span data-ttu-id="8d5ba-132">**Inhaltstyp**</span><span class="sxs-lookup"><span data-stu-id="8d5ba-132">**Content Type**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="8d5ba-133">1</span><span class="sxs-lookup"><span data-stu-id="8d5ba-133">1</span></span>  <br/> |<span data-ttu-id="8d5ba-134">File1</span><span class="sxs-lookup"><span data-stu-id="8d5ba-134">File1</span></span>  <br/> |<span data-ttu-id="8d5ba-135">DOCX</span><span class="sxs-lookup"><span data-stu-id="8d5ba-135">.docx</span></span>  <br/> |<span data-ttu-id="8d5ba-136">0x504B…</span><span class="sxs-lookup"><span data-stu-id="8d5ba-136">0x504B…</span></span>  <br/> |<span data-ttu-id="8d5ba-137">application/vnd.openxmlformats-officedocument.wordprocessingml.document</span><span class="sxs-lookup"><span data-stu-id="8d5ba-137">application/vnd.openxmlformats-officedocument.wordprocessingml.document</span></span>  <br/> |
|<span data-ttu-id="8d5ba-138">2</span><span class="sxs-lookup"><span data-stu-id="8d5ba-138">2</span></span>  <br/> |<span data-ttu-id="8d5ba-139">File2</span><span class="sxs-lookup"><span data-stu-id="8d5ba-139">File2</span></span>  <br/> |<span data-ttu-id="8d5ba-140">.doc</span><span class="sxs-lookup"><span data-stu-id="8d5ba-140">Doc</span></span>  <br/> |<span data-ttu-id="8d5ba-141">0xD…</span><span class="sxs-lookup"><span data-stu-id="8d5ba-141">0xD…</span></span>  <br/> |<span data-ttu-id="8d5ba-142">application/msword</span><span class="sxs-lookup"><span data-stu-id="8d5ba-142">application/msword</span></span>  <br/> |
|<span data-ttu-id="8d5ba-143">3</span><span class="sxs-lookup"><span data-stu-id="8d5ba-143">3</span></span>  <br/> |<span data-ttu-id="8d5ba-144">File3</span><span class="sxs-lookup"><span data-stu-id="8d5ba-144">File3</span></span>  <br/> |<span data-ttu-id="8d5ba-145">.txt</span><span class="sxs-lookup"><span data-stu-id="8d5ba-145">.txt</span></span>  <br/> |<span data-ttu-id="8d5ba-146">OxE…</span><span class="sxs-lookup"><span data-stu-id="8d5ba-146">OxE…</span></span>  <br/> |<span data-ttu-id="8d5ba-147">text/plain</span><span class="sxs-lookup"><span data-stu-id="8d5ba-147">text/plain</span></span>  <br/> |
   

## <a name="modifying-the-bdc-model-file-to-enable-crawling-of-blob-data"></a><span data-ttu-id="8d5ba-148">Ändern der BDC-Modelldatei zum Durchforsten von BLOB-Daten aktivieren</span><span class="sxs-lookup"><span data-stu-id="8d5ba-148">Modifying the BDC model file to enable crawling of BLOB data</span></span>
<span data-ttu-id="8d5ba-149"><a name="HowToCrawlBlobs_BDCModelFile"> </a></span><span class="sxs-lookup"><span data-stu-id="8d5ba-149"></span></span>

<span data-ttu-id="8d5ba-p103">Bestätigen Sie, dass die Datenbanktabelle, die Erweiterung oder MIME-Typinformationen für die BLOB-Daten enthält, können Sie Microsoft SharePoint Designer verwenden, um einen externen Inhaltstyp erstellen, der auf die Tabelle mit BLOB-Daten basiert. Anschließend können Sie alle Vorgänge erstellen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen externer Inhaltstypen](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) und [Gewusst wie: Erstellen eines externen Inhaltstyps basierend auf einer SQL Server-Tabelle](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d5ba-p103">After you confirm that the database table contains the extension or MIME type information for the BLOB data, you can use Microsoft SharePoint Designer to create an external content type that is based on the table containing the BLOB data. Then, you can create all the operations. For more information, see  [How to: Create External Content Types](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) and [How to: Create an External Content Type Based on a SQL Server Table](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx).</span></span> 
  
    
    
<span data-ttu-id="8d5ba-p104">Nachdem Sie den externen BLOB-Inhaltstyp erstellen, können Sie die BDC-Modelldatei zum ermöglichen der Durchforstung zu ändern. Sie können nicht in SharePoint Designer diese Änderungen vornehmen. Sie müssen so exportieren die Modelldatei BDC und einen XML-Editor verwenden, um diese Änderungen manuell vornehmen.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-p104">After you create the BLOB external content type, you are ready to modify the BDC model file to enable crawling. You cannot make these modifications in SharePoint Designer. So you must export the BDC model file, and use an XML editor to make these changes manually.</span></span>
  
    
    

### <a name="to-export-the-bdc-model-file-for-the-blob-external-content-type"></a><span data-ttu-id="8d5ba-156">So exportieren Sie die BDC-Modelldatei für den externen BLOB-Inhaltstyp</span><span class="sxs-lookup"><span data-stu-id="8d5ba-156">To export the BDC model file for the BLOB external content type</span></span>


1. <span data-ttu-id="8d5ba-157">Klicken Sie in SharePoint Designer um die externen Inhaltstypen anzuzeigen, die definiert sind, dass der Website-Anwendung BDC Metadaten speichern im linken Navigationsbereich auf **Externe Inhaltstypen**.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-157">In SharePoint Designer, click **External Content Types** in the left navigation to display the external content types that are defined in that site's service application's BDC metadata store.</span></span>
    
  
2. <span data-ttu-id="8d5ba-158">Wählen Sie in der Liste **Externe Inhaltstypen** den externen Inhaltstyp BLOB aus.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-158">In the **External Content Types** list, select the BLOB external content type. Then, click Export BDC Model on the spservrib.</span></span> <span data-ttu-id="8d5ba-159">Klicken Sie dann im Servermenüband auf **BDC-Modell exportieren**.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-159">Then, click **Export BDC Model** on the Server ribbon.</span></span>
    
  
3. <span data-ttu-id="8d5ba-160">Geben Sie in das Textfeld **Name des BDC-Modells** einen Namen ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-160">Type a name in the **BDC Model Name** text box, and then click **OK**.</span></span>
    
  
4. <span data-ttu-id="8d5ba-161">Wählen Sie den Speicherort zum Speichern der BDC-Modelldatei (.bdcm) aus, und klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-161">Select the location where you want to save the BDC model (.bdcm) file, and then click **Save**.</span></span>
    
  

### <a name="to-enable-crawling-of-the-blob-external-content-type"></a><span data-ttu-id="8d5ba-162">So ermöglichen Sie die Durchforstung des externen BLOB-Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="8d5ba-162">To enable crawling of the BLOB external content type</span></span>


1. <span data-ttu-id="8d5ba-163">Öffnen Sie in einem XML-Editor die BDC-Modelldatei, die Sie im vorherigen Abschnitt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-163">In an XML editor, open the BDC model file you created in the previous section.</span></span>
    
  
2. <span data-ttu-id="8d5ba-p106">Erstellen Sie eine neue Methode, die das BLOB-Feld zurückgibt. Sie müssen eine Methodeninstanz vom Typ **StreamAccessor** für dieses Methode definieren (siehe das folgende Beispiel).</span><span class="sxs-lookup"><span data-stu-id="8d5ba-p106">Create a new method that returns the BLOB field. You should define a **StreamAccessor** type method instance for this method, as shown in the following example.</span></span>
    
    > <span data-ttu-id="8d5ba-166">**Hinweis:** Der Tabellenname lautet in diesem Beispiel „Anlage“.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-166">**Note** The table name in this example is Attachment.</span></span> 

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
  
    
    
<span data-ttu-id="8d5ba-167">durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="8d5ba-167">with the following line of code:</span></span> 
  
    
    
 `<Property Name=" ContentType " Type="System.String">application/vnd.openxmlformats-officedocument.wordprocessingml.document</Property>`
    
  
3. <span data-ttu-id="8d5ba-168">Erneutes Importieren der Modelldatei mithilfe der Business Connectivity Services Service-Anwendung administrationsanwendungs-Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-168">Re-import the model file by using the Business Connectivity Services service application administration UI.</span></span> 
    
  
4. <span data-ttu-id="8d5ba-169">Erstellen Sie die Inhaltsquelle für den externen Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-169">Create the content source for the external content type.</span></span>
    
  
5. <span data-ttu-id="8d5ba-170">Starten Sie eine vollständige Durchforstung der Inhaltsquelle.</span><span class="sxs-lookup"><span data-stu-id="8d5ba-170">Launch a full crawl of the content source.</span></span> 
    
  

## <a name="additional-resources"></a><span data-ttu-id="8d5ba-171">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8d5ba-171">Additional resources</span></span>
<span data-ttu-id="8d5ba-172"><a name="SP15Crawlblobs_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8d5ba-172"></span></span>


-  [<span data-ttu-id="8d5ba-173">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8d5ba-173">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8d5ba-174">Gewusst wie: Erstellen externer Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="8d5ba-174">How to: Create External Content Types</span></span>](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="8d5ba-175">XML-Ausschnitt: Modellieren einer StreamAccessor-Methode</span><span class="sxs-lookup"><span data-stu-id="8d5ba-175">XML Snippet: Modeling a StreamAccessor Method</span></span>](http://msdn.microsoft.com/library/bd60cc2e-f7f6-421c-9d2a-60e8512b9893%28Office.15%29.aspx)
    
  

