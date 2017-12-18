---
title: "Erstellen Filterdatenanbietern für PerformancePoint-Dienste in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 25508ec6-86bf-4eea-acf0-00f88e4faa55
ms.openlocfilehash: 8b1057a13b9ae052d86b6d507d8f6e6bc0ece9f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-filter-data-providers-for-performancepoint-services-in-sharepoint"></a>Erstellen Filterdatenanbietern für PerformancePoint-Dienste in SharePoint

In diesem Artikel erfahren Sie, wie die Datenanbieterkomponente in einer benutzerdefinierten Filtererweiterung für PerformancePoint-Dienste erstellt wird.

## <a name="what-are-custom-data-providers-for-performancepoint-services"></a>Was sind benutzerdefinierte Datenanbieter für PerformancePoint-Dienste ?
<a name="bk_introduction"> </a>

In PerformancePoint-Dienste benutzerdefinierte Datenanbieter abrufen von Daten aus der zugrunde liegenden Datenquelle des Filters und definieren Sie, wie die Daten verwenden. Datenanbieter angeben, vor allem die Datenwerte verfügbar zu machen, in dem Filtersteuerelement und die Daten, die als die des filteranfangspunkt verwendet werden können. Ein Datenanbieter speichert auch den Wert, den ein Benutzer aus dem Filtersteuerelement auswählt, die dann zur Consumer Filtern gesendet wird. Datenanbieter verwenden zwei  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekte zu organisieren und Speichern von Daten. Weitere Informationen finden Sie unter [PerformancePoint Services-Filter](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).
  
    
    
Die folgenden Verfahren und Beispiele, die zeigen, wie Sie einen Filterdatenanbieter erstellen, konfigurieren und definieren, basieren auf der Klasse **SampleFilterDataProvider** aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Der Editor ist eine schlanke Webanwendung, die es Benutzern ermöglicht, den Namen und die Beschreibung des Berichts zu ändern. Den vollständigen Code für die Klasse finden Sie unter [Codebeispiel: Erstellen eines Datenanbieters für benutzerdefinierte PerformancePoint-Dienste-Filter in SharePoint](#bk_example)
  
    
    
Es wird empfohlen, dass Sie den beispieldatenanbieter als Vorlage verwenden. Das Beispiel zeigt, wie Objekte in der PerformancePoint-Dienste-API-aufrufen und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht. 
  
    
    

## <a name="create-data-providers-for-custom-performancepoint-services-filters"></a>Erstellen von Datenanbietern für benutzerdefinierte PerformancePoint-Dienste Filter
<a name="bk_createconfig"> </a>


1. Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.
    
    Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Fügen Sie die folgenden PerformancePoint-Dienste DLLs als Assemblyverweise zum Projekt hinzu:
    
  - Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Server.dll
    
  

    Je nach Funktionalität der Erweiterung sind u. U. andere Projektverweise erforderlich.
    
  
4. Fügen Sie in der Anbieterklasse **using** Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:
    
  -  [Microsoft.PerformancePoint.Scorecards](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Server.Extensions](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  

    Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.
    
  
5. Erben Sie von der [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx)-Basisklasse.
    
  
6. Legen Sie den Zeichenfolgenbezeichner für den Namen des Datenanbieters fest. Dieser muss mit dem Schlüssel übereinstimmen, den Sie beim Registrieren der Erweiterung zum Abschnitt **CustomParameterDataProviders** der Datei „web.config“ hinzufügen. Weitere Informationen finden Sie unter [Vorgehensweise: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
    
  
7. Überschreiben Sie die [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx)-Methode, um den Bezeichner für Ihren Datenanbieter zurückzugeben.
    
  
8. Überschreiben Sie die  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) -Methode, um ein [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekt zum Speichern der Datenwerte aus der zugrunde liegenden Datenquelle zu definieren. Diese Methode wird vom Filter zum Auffüllen des Filterauswahlsteuerelements verwendet. Die Anzeigedatentabelle muss die folgenden Spaltennamen enthalten:
    
  - **Key** Der eindeutige Bezeichner für den Datensatz. Dieser Wert darf nicht NULL sein. Aus Leistungs- und Sicherheitsgründen wird von Steuerelementen nur ein Schlüssel ausgegeben; aus den anderen Spalten werden keine Werte ausgegeben.
    
  
  - **Display** Der Wert, der im Filtersteuerelement angezeigt wird.
    
  
  - **ParentKey** Dieser Wert wird zum Anordnen hierarchischer Daten in einem Struktursteuerelement verwendet.
    
  
  - **IsDefault** Dieser Wert wird für Filterpersistenz verwendet.
    
    > **Tipp:** Sie können weitere Spalten hinzufügen, um die Filterfunktionalität zu erweitern. 

     [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) ruft die [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx)-Methode auf, um den Typ der Datenquelle anhand des Namens zu überprüfen, wie folgt:
    
  - Es verweist auf einen benutzerdefinierten Datenquellentyp mithilfe der  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) -Eigenschaft der Datenquelle, die den gleichen Wert wie das Attribut **subType** ist, die in der PerformancePoint-Dienste web.config-Datei für die datenquellenerweiterung registriert ist.
    
  
  - Es wird auf eine systemeigene Datenquelle verwiesen, indem die  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) -Eigenschaft verwendet wird, mit der ein Feld aus der [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) -Klasse zurückgegeben wird.
    
  
9. Überschreiben Sie die  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) -Methode, um die Auswahl des Benutzers aus dem Filtersteuerelement zu speichern. Diese Methode wird vom Filter verwendet, wenn die Auswahl des Benutzers an Consumer gesendet wird.
    
  

## <a name="code-example-create-a-data-provider-for-custom-performancepoint-services-filters-in-sharepoint"></a>Codebeispiel: Erstellen eines Datenanbieters für benutzerdefinierte PerformancePoint-Dienste-Filter in SharePoint
<a name="bk_example"> </a>

Im folgenden Codebeispiel wird zeigt, wie ein Datenanbieter Werte aus einem Webdienst oder ein Arbeitsblatt Excel abgerufen und  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) -Objekte für die Anzeige von Daten und Meldungsdaten des Filters zurückgegeben.
  
    
    
Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung wie unter  [So erstellen und konfigurieren Sie die Anbieterklasse](#bk_createconfig) beschrieben konfigurieren.
  
    
    



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


## <a name="next-steps"></a>Nächste Schritte
<a name="bk_next"> </a>

Nach dem Erstellen Sie eines Datenanbieters und ein Filter-Editor (einschließlich der Benutzeroberfläche, falls erforderlich), Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_next"> </a>


-  [Vorgehensweise: Erstellen Filter-Editoren für PerformancePoint Services in SharePoint](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [PerformancePoint-Dienste in SharePoint](performancepoint-services-in-sharepoint.md)
    
  

