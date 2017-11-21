---
title: "Vorgehensweise Erstellen von Anbietern für tabellarische Datenquellen für PerformancePoint Services in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8d734ed6-7636-40c5-a99b-bc038362cffe
ms.openlocfilehash: 9e74fd9d39a3db99eecbba4b2eb2f640606fd8a5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="97fc4-102">Vorgehensweise: Erstellen von Anbietern für tabellarische Datenquellen für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97fc4-102">How to: Create tabular data source providers for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="97fc4-103">In diesem Artikel erfahren Sie, wie die Datenquellenanbieter-Komponente in einer benutzerdefinierten Datenquellenerweiterung in Tabellenform für PerformancePoint-Dienste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="97fc4-103">Learn how to create the data source provider component in a custom tabular data source extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-data-source-providers-for-performancepoint-services"></a><span data-ttu-id="97fc4-104">Was sind benutzerdefinierte Datenquellenanbieter für PerformancePoint-Dienste ?</span><span class="sxs-lookup"><span data-stu-id="97fc4-104">What are custom data source providers for PerformancePoint Services?</span></span>
<span data-ttu-id="97fc4-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="97fc4-105"></span></span>

<span data-ttu-id="97fc4-p101">Datenquellenanbieter Verbinden mit einer Datenquelle, Zugriff auf seine Daten und dann Abfrageergebnisse. PerformancePoint-Dienste verwendet Anbietern für tabellarische Datenquellen, um Daten in Arbeitsblättern Excel und Excel Services, SharePoint-Listen und Tabellen Microsoft SQL Server zugreifen. Sie können Erstellen einer benutzerdefinierten Datenquellenanbieter, um Daten aus einer tabellarischen Datenquelle verwenden, die von PerformancePoint-Dienste nicht unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p101">Data source providers connect to a data source, access its data, and then return query results. PerformancePoint Services uses tabular data source providers to access data from Excel and Excel Services worksheets, SharePoint lists, and Microsoft SQL Server tables. You can create a custom data source provider to use data from a tabular data source that is not supported by PerformancePoint Services.</span></span>
  
    
    
<span data-ttu-id="97fc4-p102">Die Hauptfunktion der eine tabellarische Datenquellenanbieter ist zu erstellen, und füllen eine Datentabelle mit Daten aus der Datenquelle. Darüber hinaus erstellt spaltenzuordnungen, um den Typ der Daten definieren, dass jeder Spalte (Fakten-, Dimensions- oder Zeitdimension) enthält. Dies gilt eine multidimensionale grundlegende Struktur für die Tabellendaten.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p102">The main function of a tabular data source provider is to create and populate a data table with data from the data source. It also creates column mappings to define the type of data that each column contains (fact, dimension, or time dimension). This applies a basic multidimensional structure to the tabular data.</span></span>
  
    
    
<span data-ttu-id="97fc4-112">Die Verfahren und Codebeispiele in diesem Thema basieren auf der **WSTabularDataSourceProvider**-Klasse aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="97fc4-112">The procedures and code examples in this topic are based on the **WSTabularDataSourceProvider** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="97fc4-113">Der Anbieter ruft von einem externen Webdienst Aktienkurse für bestimmte Aktiensymbole ab.</span><span class="sxs-lookup"><span data-stu-id="97fc4-113">The provider retrieves stock quotes from an external web service for specified stock symbols.</span></span> <span data-ttu-id="97fc4-114">Er speichert Verlaufsdaten für Aktienkurse in einer Cachedatei, sodass die Daten in Zeit-Slices aufgeteilt werden können.</span><span class="sxs-lookup"><span data-stu-id="97fc4-114">It stores historical stock quote data in a cache file, which enables the data to be sliced by time.</span></span> <span data-ttu-id="97fc4-115">Den vollständigen Code für die Klasse finden Sie unter  [Codebeispiel: Erstellen eines Datenquellenanbieters für benutzerdefinierte tabellarische PerformancePoint-Dienste-Datenquellen in SharePoint](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="97fc4-115">For the complete code for the class, see  [Code example: Create a data source provider for custom PerformancePoint Services tabular data sources in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="97fc4-p104">Es wird empfohlen, dass Sie den Datenquellenanbieter Beispiel als Vorlage verwenden. Das Beispiel zeigt, wie Objekte in der PerformancePoint-Dienste-API-aufrufen und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p104">We recommend that you use the sample data source provider as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-data-source-providers-for-custom-performancepoint-services-tabular-data-sources"></a><span data-ttu-id="97fc4-118">Erstellen von Datenquellenanbieter für benutzerdefinierte PerformancePoint-Dienste tabellarische Datenquellen</span><span class="sxs-lookup"><span data-stu-id="97fc4-118">Create data source providers for custom PerformancePoint Services tabular data sources</span></span>
<span data-ttu-id="97fc4-119"><a name="BKMK_CreateClass"> </a></span><span class="sxs-lookup"><span data-stu-id="97fc4-119"></span></span>


1. <span data-ttu-id="97fc4-p105">Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Anweisungen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="97fc4-p105">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For instructions, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="97fc4-p106">Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p106">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="97fc4-p107">Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="97fc4-p107">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="97fc4-127">Fügen Sie die folgenden PerformancePoint-Dienste DLLs als Assemblyverweise zum Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="97fc4-127">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="97fc4-128">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="97fc4-128">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="97fc4-129">Microsoft.PerformancePoint.Scorecards.DataSourceProviders.Standard.dll</span><span class="sxs-lookup"><span data-stu-id="97fc4-129">Microsoft.PerformancePoint.Scorecards.DataSourceProviders.Standard.dll</span></span>
    
  

    <span data-ttu-id="97fc4-p108">Der Beispiel-Datenquellenanbieter enthält ebenfalls Assemblyverweise auf System.Core.dll, System.ServiceModel.dll, System.Web.dll, System.Web.Services.dll und System.Xml.Linq.dll. Je nach Funktionalität Ihrer Erweiterung sind u. U. weitere Projektverweise erforderlich.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p108">The sample data source provider also contains assembly references to System.Core.dll, System.ServiceModel.dll, System.Web.dll, System.Web.Services.dll, and System.Xml.Linq.dll. Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="97fc4-p109">Fügen Sie einen Dienstverweis mit dem Namen **StockQuotes** hinzu, mit dem auf den Webdienst mit der Adresse `http://www.webservicex.net/stockquote.asmx` verwiesen wird. Dieser Webdienst liefert Aktienkurse für die Beispieldatenquelle.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p109">Add a service reference named **StockQuotes** that references the Web service located at the address `http://www.webservicex.net/stockquote.asmx`. This is the Web service that provides stock quotes for the sample data source.</span></span>
    
  
5. <span data-ttu-id="97fc4-p110">Fügen Sie dem Projekt die Klassen **BasicTabularDataSourceProvider** und **SampleDSCacheHandler** aus dem Beispiel hinzu. **BasicTabularDataSourceProvider** erbt von der [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) -Klasse, die eine Basisklasse für Anbieter für tabellarische Datenquellen ist.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p110">Add the **BasicTabularDataSourceProvider** and **SampleDSCacheHandler** classes from the sample to your project. **BasicTabularDataSourceProvider** inherits from the [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) class, which is the base class for tabular data source providers.</span></span>
    
    <span data-ttu-id="97fc4-136">Die Klasse wird von der Beispieldatenquelle auch als Container für die überschriebenen abstrakten Methoden verwendet, die von  [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) nicht implementiert werden ( [GetDatabaseNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetDatabaseNames.aspx) , [GetCubeNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNames.aspx) , [GetCubeNameInfos()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNameInfos.aspx) , [GetCubeMetaData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeMetaData.aspx) und [Validate()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.Validate.aspx) ).</span><span class="sxs-lookup"><span data-stu-id="97fc4-136">The sample data source also uses the class as a container for the overridden abstract methods that  [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) does not implement ( [GetDatabaseNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetDatabaseNames.aspx) , [GetCubeNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNames.aspx) , [GetCubeNameInfos()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNameInfos.aspx) , [GetCubeMetaData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeMetaData.aspx) , and [Validate()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.Validate.aspx) ).</span></span>
    
  
6. <span data-ttu-id="97fc4-137">Fügen Sie in der Anbieterklasse **using** Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:</span><span class="sxs-lookup"><span data-stu-id="97fc4-137">In your provider class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="97fc4-138">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="97fc4-138">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="97fc4-139">Microsoft.PerformancePoint.Scorecards.ServerCommon</span><span class="sxs-lookup"><span data-stu-id="97fc4-139">Microsoft.PerformancePoint.Scorecards.ServerCommon</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.aspx)
    
  
  - <span data-ttu-id="97fc4-140">**Microsoft.PerformancePoint.SDK.Samples.StockQuotes** (steht für den in Schritt 4 erstellten StockQuotes-Dienstbezug)</span><span class="sxs-lookup"><span data-stu-id="97fc4-140">**Microsoft.PerformancePoint.SDK.Samples.StockQuotes** (represents the StockQuotes service reference created in step 4)</span></span>
    
  

    <span data-ttu-id="97fc4-141">Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.</span><span class="sxs-lookup"><span data-stu-id="97fc4-141">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
7. <span data-ttu-id="97fc4-142">Erben Sie von der **BasicTabularDataSourceProvider**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="97fc4-142">Inherit from the **BasicTabularDataSourceProvider** class.</span></span>
    
  
8. <span data-ttu-id="97fc4-143">Deklarieren Sie Variablen, und definieren Sie Eigenschaften, mit denen Sie Aktiensymbole, den Speicherort für die Cachedatei sowie den URI des Proxyservers analysieren, speichern und abrufen.</span><span class="sxs-lookup"><span data-stu-id="97fc4-143">Declare variables and define properties that are used for parsing, storing, and retrieving stock symbols, the cache file location, and the URI of the proxy server.</span></span>
    
  
9. <span data-ttu-id="97fc4-p111">Überschreiben Sie die  [IsConnectionStringSecure](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.IsConnectionStringSecure.aspx) -Eigenschaft. Diese Eigenschaft wird nicht vom PerformancePoint-Dienste verwendet, aber es ist für die benutzerdefinierte Anwendungen, optional verwenden, um festzustellen, ob eine Verbindungszeichenfolge-Informationen verfügbar macht, die ein Sicherheitsrisiko vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p111">Override the  [IsConnectionStringSecure](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.IsConnectionStringSecure.aspx) property. This property is not used by PerformancePoint Services, but it is intended for custom applications to optionally use to identify whether a connection string exposes information that might pose a security risk.</span></span>
    
    <span data-ttu-id="97fc4-p112">Es wird **true** zurückgegeben, wenn von der Erweiterung vertrauliche Informationen (z. B. ein Benutzername oder Kennwort) in der Verbindungszeichenfolge für Ihre Datenquelle gespeichert werden. **false** wird zurückgegeben, wenn keine vertraulichen Informationen gespeichert werden oder wenn von der Datenquelle keine Verbindungszeichenfolge verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p112">Return **true** if your extension stores sensitive information—such as a user name or password—in the connection string for your data source. Return **false** if it does not store sensitive information or if your data source does not use a connection string.</span></span>
    
  
10. <span data-ttu-id="97fc4-p113">Überschreiben Sie die  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) -Methode, um den eindeutigen Bezeichner für den Anbieter zurückzugeben. [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) muss die gleiche Zeichenfolge wie das Attribut **key** zurückgeben, die in der PerformancePoint-Dienste web.config-Datei für den benutzerdefinierten Datenquellenanbieter registriert ist.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p113">Override the  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) method to return the unique identifier for your provider. [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) must return the same string as the **key** attribute that is registered in the PerformancePoint Services web.config file for the custom data source provider.</span></span>
    
  
11. <span data-ttu-id="97fc4-p114">Überschreiben Sie die  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) -Methode, um Spaltenzuordnungen zu definieren. [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) ruft die **CreateDataColumnMappings**-Methode auf, um Datenquellenspalten vom Typ  [Fact](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Fact.aspx) , [Dimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Dimension.aspx) und [TimeDimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.TimeDimension.aspx) zu definieren.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p114">Override the  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) method to define column mappings. [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) calls the **CreateDataColumnMappings** method to define data source columns as [Fact](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Fact.aspx) , [Dimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Dimension.aspx) , and [TimeDimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.TimeDimension.aspx) types.</span></span>
    
     <span data-ttu-id="97fc4-p115">Mit  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) werden auch die Aktiensymbole, der Speicherort für die Cachedatei und die Proxyserveradresse aus der [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) -Eigenschaft des benutzerdefinierten Datenquellenobjekts abgerufen. Diese Werte werden von Dashboardautoren im Beispiel-Datenquellen-Editor definiert.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p115">[SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) also retrieves the stock symbols, cache file location, and proxy server address from the [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) property of the custom data source object. These values are defined by dashboard authors in the sample data source editor.</span></span>
    
  
12. <span data-ttu-id="97fc4-p116">Überschreiben Sie die  [GetDataSet()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.GetDataSet.aspx) -Methode, um ein [DataSet](https://msdn.microsoft.com/library/System.Data.DataSet.aspx) -Objekt zum Speichern der Daten aus der Datenquelle zu erstellen. Der Beispiel-Datenquellenanbieter verwendet die Methoden **FillResultsTable** und **GetLiveQuote** zum Auffüllen einer Datentabelle mit Daten eines Webdiensts.</span><span class="sxs-lookup"><span data-stu-id="97fc4-p116">Override the  [GetDataSet()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.GetDataSet.aspx) method to create a [DataSet](https://msdn.microsoft.com/library/System.Data.DataSet.aspx) object to store the data from the data source. The sample data source provider uses the **FillResultsTable** and **GetLiveQuote** methods to populate a data table with data from a Web service.</span></span>
    
  

## <a name="code-example-create-a-data-source-provider-for-custom-performancepoint-services-tabular-data-sources-in-sharepoint"></a><span data-ttu-id="97fc4-156">Codebeispiel: Erstellen eines Datenquellenanbieters für benutzerdefinierte tabellarische PerformancePoint-Dienste-Datenquellen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97fc4-156">Code example: Create a data source provider for custom PerformancePoint Services tabular data sources in SharePoint Server 2013</span></span>
<span data-ttu-id="97fc4-157"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="97fc4-157"></span></span>

<span data-ttu-id="97fc4-158">Mithilfe der Klasse im folgenden Codebeispiel wird ein Anbieter für tabellarische Datenquellen erstellt, mit dem Aktienkurse von einem externen Webdienst abgerufen und die Daten anschließend in ein tabellarisches Format transformiert werden.</span><span class="sxs-lookup"><span data-stu-id="97fc4-158">The class in the following code example creates a tabular data source provider that retrieves stock quotes from an external Web service and then transforms the data into a tabular format.</span></span>
  
    
    
<span data-ttu-id="97fc4-159">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie Ihre Entwicklungsumgebung konfigurieren, wie beschrieben in  [Erstellen von Datenquellenanbieter für benutzerdefinierte PerformancePoint-Dienste tabellarische Datenquellen](#BKMK_CreateClass).</span><span class="sxs-lookup"><span data-stu-id="97fc4-159">Before you can compile this code example, you must configure your development environment as described in  [Create data source providers for custom PerformancePoint Services tabular data sources](#BKMK_CreateClass).</span></span>
  
    
    



```cs

using System;
using System.Data;
using System.IO;
using System.Linq;
using System.Xml.Linq;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.ServerCommon;
using Microsoft.PerformancePoint.SDK.Samples.StockQuotes;
using System.ServiceModel;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleDataSource
{

    // Represents the class that defines the sample data source provider.
    // It inherits from the BasicTabularDataSourceProvider class, which
    // contains overridden abstract methods that are not implemented.
    public class WSTabularDataSourceProvider : BasicTabularDataSourceProvider
    {
        #region Constants
        private const int StockSymbolsIndex = 0;
        private const int CacheFileLocationIndex = 1;
        private const int ProxyAddressIndex = 2;
        #endregion

        #region Properties

        // This property stores the stock symbols that are used
        // to query the Web service.
        // Its value is obtained by parsing the CustomData property
        // of the data source object. 
        private string[] StockSymbols
        {
            get;
            set;
        }

        // The address of the proxy server.
        private Uri ProxyAddress
        {
            get;
            set;
        }

        // This property is not used by PerformancePoint Services.
        // Its intended use is for custom applications to indicate
        // whether a provider stores sensitive information in the
        // connection string, such as user name and password.
        // This sample does not, so it returns false. 
        public override bool IsConnectionStringSecure
        {
            get { return false; }
        }
        #endregion

        #region Overridden methods

        // The source name for your data source. This value must match the key
        // attribute that is registered in the web.config file.
        public override string GetId()
        {
            return "WSTabularDataSource";
        }

        // Add column mappings for the sample columns if they do not exist.
        // Column mappings may be missing if the custom data source has never
        // been edited or if the workspace was not refreshed, which saves
        // changes to the server.
        public override void SetDataSource(DataSource dataSource)
        {

            base.SetDataSource(dataSource);

            // Check for symbols stored in the CustomData
            // property of the data source.
            if (null == dataSource ||
                 string.IsNullOrEmpty(dataSource.CustomData))
            {

                // Create a symbol for testing purposes.
                StockSymbols = new[] { "MSFT" };
            }
            else
            {
                string[] splitCustomData = dataSource.CustomData.Split('&amp;');
                if (splitCustomData.Length > 2)
                {
                    StockSymbols = splitCustomData[StockSymbolsIndex].ToUpper().Split(',');
                    for (int iLoop = 0; iLoop < StockSymbols.Length; iLoop++)
                    {
                        StockSymbols[iLoop] = StockSymbols[iLoop].Trim();
                    }

                    SampleDSCacheHandler.CacheFileLocation = splitCustomData[CacheFileLocationIndex];
                    ProxyAddress = new Uri(splitCustomData[ProxyAddressIndex]);
                }
            }

            // Check whether column mappings exist. Do not overwrite them.
            if (dataSource.DataTableMapping.ColumnMappings.Count == 0)
            {
                dataSource.DataTableMapping = CreateDataColumnMappings();
            }
        }

        // Get the data from the data source.
        // GetDataSet contains the core logic for the provider.
        public override DataSet GetDataSet()
        {

            // Create a dataset and a data table to store the data.
            DataSet resultSet = new DataSet();
            DataTable resultTable = resultSet.Tables.Add();

            // Define column names and the type of data that they contain. 
            resultTable.Columns.Add("Symbol", typeof(string));
            resultTable.Columns.Add("Value", typeof(float));
            resultTable.Columns.Add("P-E Ratio", typeof(float));
            resultTable.Columns.Add("Percentage Change", typeof(float));
            resultTable.Columns.Add("Date", typeof(DateTime));

            FillResultTable(ref resultTable);

            return resultSet;
        }
        #endregion

        #region Internal methods

        // Fill the data table with the stock quote values from
        // the Web service and local cache file.
        protected void FillResultTable(ref DataTable resultsTable)
        {

            // Check the sematic validity of symbols (out of scope for this sample).
            if (null != StockSymbols &amp;&amp;
                StockSymbols.Length > 0 &amp;&amp;
                !string.IsNullOrEmpty(SampleDSCacheHandler.CacheFileLocation))
            {
                try
                {
                    if (!File.Exists(SampleDSCacheHandler.CacheFileLocation))
                    {

                        // Create the cache file.
                        XDocument doc = SampleDSCacheHandler.DefaultCacheFileContent;
                        doc.Save(@SampleDSCacheHandler.CacheFileLocation);
                    }

                    // Get real-time quotes and update cache file.
                    string wsResult = GetLiveQuote();

                    SampleDSCacheHandler.UpdateXMLCacheFile(wsResult);

                    // Check if a valid cache file location exists.
                    if (SampleDSCacheHandler.CacheFileContent != null)
                    {
                        var query = from c in SampleDSCacheHandler.CacheFileContent.Elements("StockQuotes").Elements("StockQuote")
                                    where StockSymbols.Contains(c.Attribute("Symbol").Value)
                                    select c;

                        foreach (var stockQuote in query)
                        {
                            DataRow row = resultsTable.NewRow();
                            row["Symbol"] = stockQuote.Attribute("Symbol").Value;
                            row["Value"] = stockQuote.Element("Value").Value;
                            row["Percentage Change"] = stockQuote.Element("PercentageChange").Value;
                            row["Date"] = stockQuote.Element("Date").Value;

                            decimal peRatio;

                            // Handle symbols that return 'N/A' for this field.
                            if (decimal.TryParse(stockQuote.Element("PERatio").Value, out peRatio))
                            {
                                row["P-E Ratio"] = peRatio;
                            }

                            resultsTable.Rows.Add(row);
                        }
                    }
                }
                catch (Exception ex)
                {
                    ServerUtils.HandleException(ex);
                }
            }
        }

        // Get real-time quotes from the Web service.
        protected string GetLiveQuote()
        {
            EndpointAddress endpoint = new EndpointAddress("http://www.webservicex.net/stockquote.asmx");
            BasicHttpBinding binding = new BasicHttpBinding();
            binding.ReceiveTimeout = new TimeSpan(0, 0, 120);
            binding.ProxyAddress = ProxyAddress;
            binding.UseDefaultWebProxy = false;

            StockQuotes.StockQuoteSoapClient wsStockQuoteService = new StockQuoteSoapClient(binding, endpoint);

            // Check the sematic validity of symbols (out of scope for this sample).
            if (null != StockSymbols &amp;&amp;
                StockSymbols.Length > 0)
            {
                try
                {
                    string quoteRequest = StockSymbols[0];
                    for (int iLoop = 1; iLoop < StockSymbols.Length; iLoop++)
                    {
                        quoteRequest = string.Format("{0}, {1}", quoteRequest, StockSymbols[iLoop]);
                    }

                    string wsResult = wsStockQuoteService.GetQuote(quoteRequest);
                    return wsResult;
                }
                catch (Exception ex)
                {
                    ServerUtils.HandleException(ex);
                }
            }
            return string.Empty;
        }

        // Create the column mappings.
        internal static DataTableMapping CreateDataColumnMappings()
        {
            DataTableMapping dtTableMapping = new DataTableMapping();

            // Define the data in the Symbol column as dimension data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Symbol",
                FriendlyColumnName = "Symbol",
                UniqueName = "Symbol",
                ColumnType = MappedColumnTypes.Dimension,
                FactAggregation = FactAggregations.None,
                ColumnDataType = MappedColumnDataTypes.String
            });

            // Define the data in the Value column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Value",
                FriendlyColumnName = "Value",
                UniqueName = "Value",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the data in the P-E Ratio column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "P-E Ratio",
                FriendlyColumnName = "P-E Ratio",
                UniqueName = "P-E Ratio",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the data in the Percentage Change column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Percentage Change",
                FriendlyColumnName = "Percentage Change",
                UniqueName = "Percentage Change",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the Date column as a time dimension.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Date",
                FriendlyColumnName = "Date",
                UniqueName = "Date",
                ColumnType = MappedColumnTypes.TimeDimension,
                FactAggregation = FactAggregations.None,
                ColumnDataType = MappedColumnDataTypes.DateTime
            });

            // Increase the granularity of the time dimension.
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Quarter;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Month;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Week;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Day;

            return dtTableMapping;
        }
        #endregion
    }
}

```


## <a name="next-steps"></a><span data-ttu-id="97fc4-160">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="97fc4-160">Next steps</span></span>
<span data-ttu-id="97fc4-161"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="97fc4-161"></span></span>

<span data-ttu-id="97fc4-162">Nach dem Erstellen Sie eines Datenquellenanbieters und einer Datenquelle-Editors (einschließlich der Benutzeroberfläche, falls erforderlich), Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="97fc4-162">After you create a data source provider and a data source editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span> 
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="97fc4-163">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="97fc4-163">Additional resources</span></span>
<span data-ttu-id="97fc4-164"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="97fc4-164"></span></span>


-  [<span data-ttu-id="97fc4-165">Vorgehensweise: Erstellen tabellarische Datenquelle-Editoren für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97fc4-165">How to: Create tabular data source editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
-  [<span data-ttu-id="97fc4-166">PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97fc4-166">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

