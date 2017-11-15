---
title: "Vorgehensweise Erstellen Filter von Datenanbietern für PerformancePoint Services in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 25508ec6-86bf-4eea-acf0-00f88e4faa55
ms.openlocfilehash: 14b0b02b1fdd365bb0f300ccf19ce6e7b9b21f98
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="4c500-102">Vorgehensweise: Erstellen Filter von Datenanbietern für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c500-102">How to: Create filter data providers for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="4c500-103">In diesem Artikel erfahren Sie, wie die Datenanbieterkomponente in einer benutzerdefinierten Filtererweiterung für PerformancePoint-Dienste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="4c500-103">Learn how to create the data provider component in a custom filter extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-data-providers-for-performancepoint-services"></a><span data-ttu-id="4c500-104">Was sind benutzerdefinierte Datenanbieter für PerformancePoint-Dienste ?</span><span class="sxs-lookup"><span data-stu-id="4c500-104">What are custom data providers for PerformancePoint Services?</span></span>
<span data-ttu-id="4c500-105"><a name="bk_introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="4c500-105"></span></span>

<span data-ttu-id="4c500-p101">In PerformancePoint-Dienste benutzerdefinierte Datenanbieter abrufen von Daten aus der zugrunde liegenden Datenquelle des Filters und definieren Sie, wie die Daten verwenden. Datenanbieter angeben, vor allem die Datenwerte verfügbar zu machen, in dem Filtersteuerelement und die Daten, die als die des filteranfangspunkt verwendet werden können. Ein Datenanbieter speichert auch den Wert, den ein Benutzer aus dem Filtersteuerelement auswählt, die dann zur Consumer Filtern gesendet wird. Datenanbieter verwenden zwei  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekte zu organisieren und Speichern von Daten. Weitere Informationen finden Sie unter [PerformancePoint Services-Filter](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c500-p101">In PerformancePoint Services, custom data providers retrieve data from a filter's underlying data source and define how to use the data. Most importantly, data providers specify the data values to expose in the filter control and the data that can be used as the filter's beginpoint. A data provider also stores the value that a user selects from the filter control, which is then sent to filter consumers. Data providers use two  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) objects to organize and store data. For more information, see [Filters Overview](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="4c500-111">Die folgenden Verfahren und Beispiele, die zeigen, wie Sie einen Filterdatenanbieter erstellen, konfigurieren und definieren, basieren auf der Klasse **SampleFilterDataProvider** aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c500-111">The following procedures and examples that show you how to create, configure, and define a filter data provider are based on the **SampleFilterDataProvider** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). The editor is a thin web application that enables users to modify the report's name and description. For the complete code for the class, see  Code example: Create a data provider for custom PerformancePoint Services filters in SharePoint Server 2013.</span></span> <span data-ttu-id="4c500-112">Der Editor ist eine schlanke Webanwendung, die es Benutzern ermöglicht, den Namen und die Beschreibung des Berichts zu ändern.</span><span class="sxs-lookup"><span data-stu-id="4c500-112">The editor is a thin web application that enables users to modify the report's name and description.</span></span> <span data-ttu-id="4c500-113">Den vollständigen Code für die Klasse finden Sie unter [Codebeispiel: Erstellen eines Datenanbieters für benutzerdefinierte PerformancePoint-Dienste-Filter in SharePoint](#bk_example)</span><span class="sxs-lookup"><span data-stu-id="4c500-113">For the complete code for the class, see  [Code example: Create a data provider for custom PerformancePoint Services filters in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="4c500-p103">Es wird empfohlen, dass Sie den beispieldatenanbieter als Vorlage verwenden. Das Beispiel zeigt, wie Objekte in der PerformancePoint-Dienste-API-aufrufen und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="4c500-p103">We recommend that you use the sample data provider as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Servicesdevelopment.</span></span> 
  
    
    

## <a name="create-data-providers-for-custom-performancepoint-services-filters"></a><span data-ttu-id="4c500-116">Erstellen von Datenanbietern für benutzerdefinierte PerformancePoint-Dienste Filter</span><span class="sxs-lookup"><span data-stu-id="4c500-116">Create data providers for custom PerformancePoint Services filters</span></span>
<span data-ttu-id="4c500-117"><a name="bk_createconfig"> </a></span><span class="sxs-lookup"><span data-stu-id="4c500-117"></span></span>


1. <span data-ttu-id="4c500-p104">Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c500-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="4c500-p105">Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="4c500-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="4c500-p106">Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c500-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="4c500-125">Fügen Sie die folgenden PerformancePoint-Dienste DLLs als Assemblyverweise zum Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="4c500-125">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="4c500-126">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="4c500-126">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="4c500-127">Microsoft.PerformancePoint.Scorecards.Server.dll</span><span class="sxs-lookup"><span data-stu-id="4c500-127">Microsoft.PerformancePoint.Scorecards.Server.dll</span></span>
    
  

    <span data-ttu-id="4c500-128">Je nach Funktionalität der Erweiterung sind u. U. andere Projektverweise erforderlich.</span><span class="sxs-lookup"><span data-stu-id="4c500-128">Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="4c500-129">Fügen Sie in der Anbieterklasse **using** Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:</span><span class="sxs-lookup"><span data-stu-id="4c500-129">In your provider class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="4c500-130">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="4c500-130">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="4c500-131">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span><span class="sxs-lookup"><span data-stu-id="4c500-131">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  

    <span data-ttu-id="4c500-132">Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.</span><span class="sxs-lookup"><span data-stu-id="4c500-132">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
5. <span data-ttu-id="4c500-133">Erben Sie von der [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx)-Basisklasse.</span><span class="sxs-lookup"><span data-stu-id="4c500-133">Inherit from the  [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx) base class.</span></span>
    
  
6. <span data-ttu-id="4c500-134">Legen Sie den Zeichenfolgenbezeichner für den Namen des Datenanbieters fest.</span><span class="sxs-lookup"><span data-stu-id="4c500-134">Set the string identifier for the data provider name.</span></span> <span data-ttu-id="4c500-135">Dieser muss mit dem Schlüssel übereinstimmen, den Sie beim Registrieren der Erweiterung zum Abschnitt **CustomParameterDataProviders** der Datei „web.config“ hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="4c500-135">Set the string identifier for the data provider name. This must match the key that you add to the **CustomParameterDataProviders** section of the web.config file when you register the extension. For more information, see How to: Manually Register PerformancePoint Services Extensions.</span></span> <span data-ttu-id="4c500-136">Weitere Informationen finden Sie unter [Vorgehensweise: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c500-136">For more information about extension metadata, see  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
    
  
7. <span data-ttu-id="4c500-137">Überschreiben Sie die [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx)-Methode, um den Bezeichner für Ihren Datenanbieter zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="4c500-137">Override the  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx) method to return the identifier for your data provider.</span></span>
    
  
8. <span data-ttu-id="4c500-p108">Überschreiben Sie die  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) -Methode, um ein [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekt zum Speichern der Datenwerte aus der zugrunde liegenden Datenquelle zu definieren. Diese Methode wird vom Filter zum Auffüllen des Filterauswahlsteuerelements verwendet. Die Anzeigedatentabelle muss die folgenden Spaltennamen enthalten:</span><span class="sxs-lookup"><span data-stu-id="4c500-p108">Override the  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) method to define a [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) object to store the data values from the underlying data source. The filter uses this method to populate the filter selection control. The display data table must contain the following column names:</span></span>
    
  - <span data-ttu-id="4c500-p109">**Key** Der eindeutige Bezeichner für den Datensatz. Dieser Wert darf nicht NULL sein. Aus Leistungs- und Sicherheitsgründen wird von Steuerelementen nur ein Schlüssel ausgegeben; aus den anderen Spalten werden keine Werte ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="4c500-p109">**Key** The unique identifier for the record. This value cannot be null. For performance and security purposes, controls emit only a key; they do not emit values from the other columns.</span></span>
    
  
  - <span data-ttu-id="4c500-144">**Display** Der Wert, der im Filtersteuerelement angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="4c500-144">**Display** The value that appears in the filter control.</span></span>
    
  
  - <span data-ttu-id="4c500-145">**ParentKey** Dieser Wert wird zum Anordnen hierarchischer Daten in einem Struktursteuerelement verwendet.</span><span class="sxs-lookup"><span data-stu-id="4c500-145">**ParentKey** This value is used to arrange hierarchical data in a tree control.</span></span>
    
  
  - <span data-ttu-id="4c500-146">**IsDefault** Dieser Wert wird für Filterpersistenz verwendet.</span><span class="sxs-lookup"><span data-stu-id="4c500-146">**IsDefault** This value is used for filter persistence.</span></span>
    
    > <span data-ttu-id="4c500-147">**Tipp:** Sie können weitere Spalten hinzufügen, um die Filterfunktionalität zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="4c500-147">**TIP** You can add more columns to extend the filter's functionality.</span></span> 

     <span data-ttu-id="4c500-148">[GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) ruft die [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx)-Methode auf, um den Typ der Datenquelle anhand des Namens zu überprüfen, wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4c500-148">[GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) calls the [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx) method to verify the data source type by name, as follows:</span></span>
    
  - <span data-ttu-id="4c500-149">Es verweist auf einen benutzerdefinierten Datenquellentyp mithilfe der  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) -Eigenschaft der Datenquelle, die den gleichen Wert wie das Attribut **subType** ist, die in der PerformancePoint-Dienste web.config-Datei für die datenquellenerweiterung registriert ist.</span><span class="sxs-lookup"><span data-stu-id="4c500-149">It references a custom data source type by using the  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) property of the data source, which is the same value as the **subType** attribute that is registered in the PerformancePoint Services web.config file for the data source extension.</span></span>
    
  
  - <span data-ttu-id="4c500-150">Es wird auf eine systemeigene Datenquelle verwiesen, indem die  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) -Eigenschaft verwendet wird, mit der ein Feld aus der [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) -Klasse zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="4c500-150">It references a native data source by using the  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) property, which returns a field from the [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) class.</span></span>
    
  
9. <span data-ttu-id="4c500-p110">Überschreiben Sie die  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) -Methode, um die Auswahl des Benutzers aus dem Filtersteuerelement zu speichern. Diese Methode wird vom Filter verwendet, wenn die Auswahl des Benutzers an Consumer gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="4c500-p110">Override the  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) method to store the user's selection from the filter control. The filter uses this method when it sends the user's selections to consumers.</span></span>
    
  

## <a name="code-example-create-a-data-provider-for-custom-performancepoint-services-filters-in-sharepoint"></a><span data-ttu-id="4c500-153">Codebeispiel: Erstellen eines Datenanbieters für benutzerdefinierte PerformancePoint-Dienste-Filter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c500-153">Code example: Create a data provider for custom PerformancePoint Services filters in SharePoint Server 2013</span></span>
<span data-ttu-id="4c500-154"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="4c500-154"></span></span>

<span data-ttu-id="4c500-155">Im folgenden Codebeispiel wird zeigt, wie ein Datenanbieter Werte aus einem Webdienst oder ein Arbeitsblatt Excel abgerufen und  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekte für die Anzeige von Daten und Meldungsdaten des Filters zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="4c500-155">The following code example shows how a data provider retrieves values from a web service or an Excel worksheet and returns  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) objects for the filter's display data and message data.</span></span>
  
    
    
<span data-ttu-id="4c500-156">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung wie unter  [So erstellen und konfigurieren Sie die Anbieterklasse](#bk_createconfig) beschrieben konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="4c500-156">Before you can compile this code example, you must configure your development environment as described in  [To create and configure the provider class](#bk_createconfig).</span></span>
  
    
    



```cs

using System.Data;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Server.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleFilter
{

    // Represents the sample filter's data provider.
    public class SampleFilterDataProvider : CustomParameterDataProvider
    {

        // This value must match the key that you register for this extension
        // in the CustomParameterDataProviders section in the web.config file.
        private const string dataProviderName = "SampleFilterDataProvider";

        // Returns a table of all possible values (rows) for the
        // filter's beginpoints. The filter's BeginPoint property returns
        // one ParameterDefinition object.
        protected override DataTable GetDisplayDataInternal(ParameterDefinition parameterDefinition, RepositoryLocation parameterSourceLocation, object custom)
        {
            DataTable retrievedData = null;

            // Get the data source.
            DataSource parameterDataSource = SafeGetDataSource(parameterSourceLocation);
            if (null != parameterDataSource)
            {

                // Verify that the data source is the sample data source
                // or an Excel workbook, which are the types that the
                // sample supports.
                // If you modify these types of data source, you must make
                // the corresponding change in the filter's editor.
                if (parameterDataSource.SourceName == "WSTabularDataSource" || parameterDataSource.SourceName == DataSourceNames.ExcelWorkbook)
                {
                    IDataSourceProvider parameterDataSourceProvider =
                        DataSourceRegistry.GetDataSource(parameterDataSource);
                    if (null != parameterDataSourceProvider)
                    {
                        var dataSourceMetadata = parameterDataSourceProvider as IDataSourceMetadata;
                        if (null != dataSourceMetadata)
                        {

                            // Get the data and store it in the retrievedDataSet
                            // variable. The -1 parameter returns all records
                            // from the data source.
                            DataSet retrievedDataSet = dataSourceMetadata.GetPreviewDataSet(-1);

                            // Verify that the dataset contains data.  
                            if (retrievedDataSet != null &amp;&amp;
                                retrievedDataSet.Tables != null &amp;&amp;
                                retrievedDataSet.Tables.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0] != null &amp;&amp;
                                retrievedDataSet.Tables[0].Columns != null &amp;&amp;
                                retrievedDataSet.Tables[0].Columns.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0].Rows != null &amp;&amp;
                                retrievedDataSet.Tables[0].Rows.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0].Columns.Contains(parameterDefinition.KeyColumn))
                            {
                                retrievedData = retrievedDataSet.Tables[0];
                            }
                        }
                    }
                }

                if (null != retrievedData)
                {
                    // Name the display data table.
                    retrievedData.TableName = "ParamData";

                    // Verify that the table has the correct structure. 
                    EnsureDataColumns(retrievedData, parameterDefinition);

                    bool firstRowSeen = false;
                    foreach (DataRow row in retrievedData.Rows)
                    {
                        // Set the ParentKeyColumn to null because the data
                        // does not have a hierarchical structure.
                        row[parameterDefinition.ParentKeyColumn] = null;

                        // Set the IsDefaultColumn column in the first row to true.
                        row[parameterDefinition.IsDefaultColumn] = !firstRowSeen;
                        if (!firstRowSeen)
                        {
                            firstRowSeen = true;
                        }
                    }

                    // Set the column visibility.
                    SetColumnVisibility(retrievedData);
                }
            }
            
            return retrievedData;
        }

        // Adds the ShowColumn extended property to a column in the display data table
        // and sets it to true. This exposes the column in Dashboard Designer as 
        // a source value for the beginpoint. 
        private static void SetColumnVisibility(DataTable displayData)
        {
            for (int i = 0; i < displayData.Columns.Count; i++)
            {
                if (!displayData.Columns[i].ExtendedProperties.Contains("ShowColumn"))
                {
                    displayData.Columns[i].ExtendedProperties.Add("ShowColumn", true);
                }
            }
        }

        // Verify that all required columns are in the data table.
        // The data table returned by this method is expected to contain a
        // Key, ParentKey, IsDefault, Display, and an arbitrary number of
        // Value columns.
        // The specific column names (except for Value columns) are defined
        // in the filter's ParameterDefinition object, which is referenced by
        // the filter's BeginPoint property.
        private static void EnsureDataColumns(DataTable dataTable, ParameterDefinition parameterDefinition)
        {
            if (!string.IsNullOrEmpty(parameterDefinition.KeyColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.KeyColumn))
            {
                dataTable.Columns.Add(parameterDefinition.KeyColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.DisplayColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.DisplayColumn))
            {
                dataTable.Columns.Add(parameterDefinition.DisplayColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.ParentKeyColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.ParentKeyColumn))
            {
                dataTable.Columns.Add(parameterDefinition.ParentKeyColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.IsDefaultColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.IsDefaultColumn))
            {
                dataTable.Columns.Add(parameterDefinition.IsDefaultColumn, typeof(bool));
            }
        }

        // Returns the unique string identifier of the data provider.
        // This value must match the key that you register for this extension
        // in the CustomParameterDataProviders section in the web.config file.
        public override string GetId()
        {
            return dataProviderName;
        }

        // Returns a table of rows that match the keys in the passed
        // ParameterMessage object.
        // This method is used by controls that accept parameters, such as
        // scorecard and reports. It can also apply a Post Formula.
        public override DataTable GetMessageData(RepositoryLocation providerLocation, ParameterMessage parameterMessage, RepositoryLocation parameterSourceLocation, ParameterMapping parameterMapping, object custom)
        {   
            DataTable msgTable = null;

            // The ParameterMapping object contains information about
            // linked dashboard items.
            // The CustomData object is optionally used to store information
            // that is not stored in other properties.
            DataTable displayTable = GetDisplayDataInternal(parameterMessage, parameterSourceLocation, custom);

            if (null != displayTable)
            {
                msgTable = displayTable.Clone();
                for (int i = 0;i < parameterMessage.Values.Rows.Count; i++)
                {
                    for (int j = 0;j < displayTable.Rows.Count; j++)
                    {
                        if (!parameterMessage.Values.Rows[i][parameterMessage.KeyColumn].Equals(displayTable.Rows[j][parameterMessage.KeyColumn].ToString())) 
                            continue;

                        msgTable.ImportRow(displayTable.Rows[j]);
                        break;
                    }
                }
            }

            return msgTable;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="4c500-157">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="4c500-157">Next steps</span></span>
<span data-ttu-id="4c500-158"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="4c500-158"></span></span>

<span data-ttu-id="4c500-159">Nach dem Erstellen Sie eines Datenanbieters und ein Filter-Editor (einschließlich der Benutzeroberfläche, falls erforderlich), Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="4c500-159">After you create a data provider and a filter editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="4c500-160">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4c500-160">Additional resources</span></span>
<span data-ttu-id="4c500-161"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="4c500-161"></span></span>


-  [<span data-ttu-id="4c500-162">Vorgehensweise: Erstellen Filter-Editoren für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c500-162">How to: Create filter editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4c500-163">PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c500-163">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

