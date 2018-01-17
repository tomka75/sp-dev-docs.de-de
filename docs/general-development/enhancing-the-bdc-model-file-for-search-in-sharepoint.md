---
title: "Optimieren der BDC-Modelldatei für die Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c67b1cf-5fca-4805-a1b5-c9ac1ff8aede
ms.openlocfilehash: 26b06db6e478c15d47257b8a88de30da1f0bb0c1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="enhancing-the-bdc-model-file-for-search-in-sharepoint"></a><span data-ttu-id="f208e-102">Optimieren der BDC-Modelldatei für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f208e-102">Enhancing the BDC model file for Search in SharePoint</span></span>
<span data-ttu-id="f208e-103">Informationen Sie zu den Eigenschaften im BDC-Metadatenmodell, die die BCS-indizierungskonnektoren betreffen die Suche in SharePoint zum Durchforsten der externer Daten zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="f208e-103">Learn about the properties in the BDC metadata model that are applicable to BCS indexing connectors which enable Search in SharePoint to crawl external data.</span></span>
## <a name="search-properties-for-bdc-model-files"></a><span data-ttu-id="f208e-104">Sucheigenschaften für BDC-Modelldateien</span><span class="sxs-lookup"><span data-stu-id="f208e-104">Search properties for BDC model files</span></span>
<span data-ttu-id="f208e-105"><a name="SearchBDCModelProperties_SearchProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="f208e-105"><a name="SearchBDCModelProperties_SearchProperties"> </a></span></span>

<span data-ttu-id="f208e-p101">Das konnektorframework in Suche können Sie zum Durchforsten der externer Daten, die in den Suchergebnissen über BCS-indizierungskonnektoren verfügbar zu machen. BCS-Indizierungsconnector wird vom Crawler verwendet, mit der externen Datenquelle kommunizieren. Bei der Durchforstung ruft der Crawler den BCS-Indizierungsconnector zum Abrufen der Daten aus dem externen System, und geben Sie ihn an dem Crawler.</span><span class="sxs-lookup"><span data-stu-id="f208e-p101">The connector framework in Search enables you to crawl external data, making it available in search results through BCS indexing connectors. The BCS indexing connector is used by the crawler to communicate with the external data source. At crawl time, the crawler calls the BCS indexing connector to fetch the data from the external system and pass it back to the crawler.</span></span> 
  
    
    
<span data-ttu-id="f208e-109">BCS-Indizierungsconnectors bestehen aus Folgendem:</span><span class="sxs-lookup"><span data-stu-id="f208e-109">BCS indexing connectors are composed of the following:</span></span>
  
    
    


  
    
    
> <span data-ttu-id="f208e-110">**BDC-Modelldatei** Die Datei, die Verbindungsinformationen für das externe System und die Struktur der Daten bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="f208e-110">**BDC model file** The file that provides the connection information to the external system and the structure of the data.</span></span>
    
  

  
    
    
> <span data-ttu-id="f208e-111">**Connector** Die Komponente mit dem Code, der eine Verbindung mit dem externen System und analysiert das Access-URLs und BCS-IDs.</span><span class="sxs-lookup"><span data-stu-id="f208e-111">**Connector** The component containing the code that connects to the external system and parses the access URLs and BCS identifiers.</span></span>
    
  
<span data-ttu-id="f208e-112">Das BDC-Metadatenmodell enthält verschiedene Eigenschaften, die gelten für Suche, von die viele zur Unterstützung von BCS-Indizierungsconnector Durchforstung erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="f208e-112">The BDC metadata model includes several properties that are applicable to Search, many of which are required to support BCS indexing connector crawling.</span></span> 
  
    
    
<span data-ttu-id="f208e-113">In der folgenden Tabelle wird beschrieben, die BDC-Modell-Eigenschaften, die auf Suche angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="f208e-113">The following table describes the BDC model properties that are applicable to Search.</span></span>
  
    
    

<span data-ttu-id="f208e-114">**Tabelle 1. Suchdiensteigenschaften für BDC-Modelldateien**</span><span class="sxs-lookup"><span data-stu-id="f208e-114">**Table 1. Search properties for BDC model files**</span></span>


|<span data-ttu-id="f208e-115">**Name**</span><span class="sxs-lookup"><span data-stu-id="f208e-115">**Name**</span></span>|<span data-ttu-id="f208e-116">**Metadatenobjekt**</span><span class="sxs-lookup"><span data-stu-id="f208e-116">**Metadata Object**</span></span>|<span data-ttu-id="f208e-117">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f208e-117">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f208e-118">ShowInSearchUI</span><span class="sxs-lookup"><span data-stu-id="f208e-118">ShowInSearchUI</span></span>  <br/> |<span data-ttu-id="f208e-119">Model</span><span class="sxs-lookup"><span data-stu-id="f208e-119">Model</span></span>  <br/> |<span data-ttu-id="f208e-p102">Gibt an, dass ein **LobSystemInstance**-Element in der Modelldatei in der Benutzeroberfläche des Suchdiensts angezeigt werden soll. Dieser Wert wird für benutzerdefinierte Konnektoren ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f208e-p102">Specifies that an **LobSystemInstance** element in the model file should be displayed in the search user interface. This value is ignored for custom connectors. </span></span><br/> |
|<span data-ttu-id="f208e-122">InputUriProcessor</span><span class="sxs-lookup"><span data-stu-id="f208e-122">InputUriProcessor</span></span>  <br/> |<span data-ttu-id="f208e-123">LobSystem</span><span class="sxs-lookup"><span data-stu-id="f208e-123">LobSystem</span></span>  <br/> |<span data-ttu-id="f208e-p103">Gibt den Namen der Klasse, die die eingegebene URL vor der Übergabe an den Connector verarbeitet. Gilt für .NET und benutzerdefinierten BCS Indizierung Connectors. Weitere Informationen finden Sie unter  [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f208e-p103">Specifies the name of the class that processes the input URL before passing it to the connector. Applies to .NET and custom BCS indexing connectors. For more information, see  [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="f208e-127">OutputUriProcessor</span><span class="sxs-lookup"><span data-stu-id="f208e-127">OutputUriProcessor</span></span>  <br/> |<span data-ttu-id="f208e-128">LobSystem</span><span class="sxs-lookup"><span data-stu-id="f208e-128">LobSystem</span></span>  <br/> |<span data-ttu-id="f208e-p104">Gibt den Namen der Klasse, die die URL für die Ausgabe vor der Übergabe an das Suchsystem aus den Connector verarbeitet. Gilt für .NET und benutzerdefinierten BCS Indizierung Connectors. Weitere Informationen finden Sie unter  [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f208e-p104">Specifies the name of the class that processes the output URL before passing it to the search system from the connector. Applies to .NET and custom BCS indexing connectors. For more information, see  [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="f208e-132">SystemUtilityTypeName</span><span class="sxs-lookup"><span data-stu-id="f208e-132">SystemUtilityTypeName</span></span>  <br/> |<span data-ttu-id="f208e-133">LobSystem</span><span class="sxs-lookup"><span data-stu-id="f208e-133">LobSystem</span></span>  <br/> |<span data-ttu-id="f208e-p105">Gibt den Namen der Klasse, die die **StructuredRepositorySystemUtility** -Klasse implementiert. Gilt für benutzerdefinierte BCS Indizierung Connectors. Weitere Informationen finden Sie unter [Erstellen eines benutzerdefinierten Indizierungskonnektors](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx). </span><span class="sxs-lookup"><span data-stu-id="f208e-p105">Specifies the name of the class that implements the **StructuredRepositorySystemUtility** class. Applies to custom BCS indexing connectors. For more information, see [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="f208e-137">Title</span><span class="sxs-lookup"><span data-stu-id="f208e-137">Title</span></span>  <br/> |<span data-ttu-id="f208e-138">Entität</span><span class="sxs-lookup"><span data-stu-id="f208e-138">Entity</span></span>  <br/> |<span data-ttu-id="f208e-139">Gibt den Titel des externen Inhaltstyps an, der in Suchergebnissen angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="f208e-139">Specifies the title of the external content type to display in search results.</span></span>  <br/> |
|<span data-ttu-id="f208e-140">DefaultLocale</span><span class="sxs-lookup"><span data-stu-id="f208e-140">DefaultLocale</span></span>  <br/> |<span data-ttu-id="f208e-141">Entität</span><span class="sxs-lookup"><span data-stu-id="f208e-141">Entity</span></span>  <br/> |<span data-ttu-id="f208e-p106">Gibt die Gebietsschema-Zeichenfolge an. Diesen Wert können Sie mit der **LCIDField**-Eigenschaft oder der **CultureField**-Eigenschaft überschreiben. </span><span class="sxs-lookup"><span data-stu-id="f208e-p106">Specifies the locale string. You can override this value by using the **LCIDField** property or the **CultureField** property. </span></span><br/> |
|<span data-ttu-id="f208e-144">RootFinder</span><span class="sxs-lookup"><span data-stu-id="f208e-144">RootFinder</span></span>  <br/> |<span data-ttu-id="f208e-145">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-145">Method</span></span>  <br/> |<span data-ttu-id="f208e-p107">Gibt die **Finder**-Methode an, die zum Aufzählen der zu durchforstenden Elemente verwendet werden soll. Beispielsweise könnte dies beim Herstellen einer Verbindung mit einer Datenbank die **SELECT**-Anweisung oder die Liste der zu durchforstenden Tabellen sein. </span><span class="sxs-lookup"><span data-stu-id="f208e-p107">Specifies the **Finder** method to use to enumerate the items to crawl. For example, when connecting to a database, this could be the **SELECT** statement or the list of tables to crawl. </span></span><br/> |
|<span data-ttu-id="f208e-148">DirectoryLink</span><span class="sxs-lookup"><span data-stu-id="f208e-148">DirectoryLink</span></span>  <br/> |<span data-ttu-id="f208e-149">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-149">Method</span></span>  <br/> |<span data-ttu-id="f208e-p108">Gibt an, dass BCS Zuordnungen navigieren soll. Erforderlich für das hierarchische crawlen.</span><span class="sxs-lookup"><span data-stu-id="f208e-p108">Specifies that BCS should navigate associations. Required for hierarchical crawling.</span></span>  <br/> |
|<span data-ttu-id="f208e-152">DeletedCountField</span><span class="sxs-lookup"><span data-stu-id="f208e-152">DeletedCountField</span></span>  <br/> |<span data-ttu-id="f208e-153">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-153">Method</span></span>  <br/> |<span data-ttu-id="f208e-p109">Gibt den Wert für die Anzahl gelöschter Elemente an. Diese Eigenschaft wird ignoriert, außer sie enthält eine ganze Zahl, die größer als Null ist.</span><span class="sxs-lookup"><span data-stu-id="f208e-p109">Specifies the deleted count value. This property is ignored unless it contains an integer greater than zero.</span></span>  <br/> |
|<span data-ttu-id="f208e-156">WindowsSecurityDescriptorField</span><span class="sxs-lookup"><span data-stu-id="f208e-156">WindowsSecurityDescriptorField</span></span>  <br/> |<span data-ttu-id="f208e-157">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-157">Method</span></span>  <br/> |<span data-ttu-id="f208e-p110">Gibt die Windows-Sicherheitsbeschreibung für das Element an. Wenn diese Eigenschaft nicht angegeben ist, wird die **GetSecurityDescriptor**-Methode aufgerufen. Wenn **GetSecurityDescriptor** nicht definiert ist, werden alle externen Elemente der Zugriffssteuerungsliste (Access Control List, ACL) "Jeder" zugewiesen. </span><span class="sxs-lookup"><span data-stu-id="f208e-p110">Specifies the Windows Security descriptor for the item. If not specified, the **GetSecurityDescriptor** method is called. If the **GetSecurityDescriptor** is not defined, all external items are assigned the Everyone access control list (ACL). </span></span><br/> |
|<span data-ttu-id="f208e-161">AuthorField</span><span class="sxs-lookup"><span data-stu-id="f208e-161">AuthorField</span></span>  <br/> |<span data-ttu-id="f208e-162">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-162">Method</span></span>  <br/> |<span data-ttu-id="f208e-163">Gibt den Namen des Autors an, der in Suchergebnissen angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="f208e-163">Specifies the author name to display in search results.</span></span>  <br/> |
|<span data-ttu-id="f208e-164">DisplayUriField</span><span class="sxs-lookup"><span data-stu-id="f208e-164">DisplayUriField</span></span>  <br/> |<span data-ttu-id="f208e-165">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-165">Method</span></span>  <br/> |<span data-ttu-id="f208e-p111">Gibt die URL in den Suchergebnissen angezeigt. Wenn angegeben, überschreibt diese Eigenschaft die URL für die Profile von BCS bereitgestellt. Wenn nicht angegeben wird, beginnt die URL in den Suchergebnissen angezeigt mit **bdc3: / /**, und wird nicht vom Browser verstanden.</span><span class="sxs-lookup"><span data-stu-id="f208e-p111">Specifies the URL to display in search results. If specified, this property overrides the profile page URL provided by BCS. If not specified, the URL displayed in search results starts with **bdc3://**, and is not understood by the browser. </span></span><br/> |
|<span data-ttu-id="f208e-169">LastModifiedTimeStampField</span><span class="sxs-lookup"><span data-stu-id="f208e-169">LastModifiedTimeStampField</span></span>  <br/> |<span data-ttu-id="f208e-170">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-170">Method</span></span>  <br/> |<span data-ttu-id="f208e-p112">Gibt den Zeitstempel des externen Elements an, der in Suchergebnissen angezeigt werden soll. Dieser Wert wird auch für die inkrementelle Durchforstung verwendet.</span><span class="sxs-lookup"><span data-stu-id="f208e-p112">Specifies the external item's timestamp to display in search results. This value is also used for incremental crawling.</span></span>  <br/> |
|<span data-ttu-id="f208e-173">DescriptionField</span><span class="sxs-lookup"><span data-stu-id="f208e-173">DescriptionField</span></span>  <br/> |<span data-ttu-id="f208e-174">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-174">Method</span></span>  <br/> |<span data-ttu-id="f208e-175">Gibt die Beschreibung an, die in Suchergebnissen angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="f208e-175">Specifies the description to display in search results.</span></span>  <br/> |
|<span data-ttu-id="f208e-176">LCIDField</span><span class="sxs-lookup"><span data-stu-id="f208e-176">LCIDField</span></span>  <br/> |<span data-ttu-id="f208e-177">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-177">Method</span></span>  <br/> |<span data-ttu-id="f208e-p113">Gibt die Gebietsschema-ID (LCID) für **DescriptionField** an. Wenn diese Eigenschaft nicht angegeben ist, wird die standardmäßige Wörtertrennung verwendet.</span><span class="sxs-lookup"><span data-stu-id="f208e-p113">Specifies the locale ID (LCID) for the **DescriptionField**. If this is not specified, the default word breaker is used.  </span></span><br/> |
|<span data-ttu-id="f208e-180">CultureField</span><span class="sxs-lookup"><span data-stu-id="f208e-180">CultureField</span></span>  <br/> |<span data-ttu-id="f208e-181">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-181">Method</span></span>  <br/> |<span data-ttu-id="f208e-182">Gibt die Kultur für **DescriptionField** an.</span><span class="sxs-lookup"><span data-stu-id="f208e-182">Specifies the culture for the **DescriptionField**.</span></span>  <br/> |
|<span data-ttu-id="f208e-183">Extension</span><span class="sxs-lookup"><span data-stu-id="f208e-183">Extension</span></span>  <br/> |<span data-ttu-id="f208e-184">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-184">Method</span></span>  <br/> |<span data-ttu-id="f208e-p114">Gibt die Dateinamenerweiterung für den Datenstrom an, der durchforstet werden kann. Wenn diese Eigenschaft nicht angegeben ist, lautet die Standarderweiterung **.txt**.</span><span class="sxs-lookup"><span data-stu-id="f208e-p114">Specifies the file name extension for the crawlable stream. If not specified, the default extension is **.txt**. </span></span><br/> |
|<span data-ttu-id="f208e-187">MimeType</span><span class="sxs-lookup"><span data-stu-id="f208e-187">MimeType</span></span>  <br/> |<span data-ttu-id="f208e-188">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-188">Method</span></span>  <br/> |<span data-ttu-id="f208e-p115">Gibt den MIME-Typ für den Datenstrom an, der durchforstet werden kann. Wenn diese Eigenschaft nicht angegeben ist, lautet die Standarderweiterung **.txt**. Wenn die Felder **Extension** und **MimeType** beide angegeben sind, wird der im Feld angegebene **MimeType** Wert verwendet. </span><span class="sxs-lookup"><span data-stu-id="f208e-p115">Specifies the MIME type for the crawlable stream. If not specified, the default extension is **.txt**. If the **Extension** field and **MimeType** field are both specified, the value specified in the **MimeType** field is used. </span></span><br/> |
|<span data-ttu-id="f208e-192">UseClientCachingForSearch</span><span class="sxs-lookup"><span data-stu-id="f208e-192">UseClientCachingForSearch</span></span>  <br/> |<span data-ttu-id="f208e-193">Methode</span><span class="sxs-lookup"><span data-stu-id="f208e-193">Method</span></span>  <br/> |<span data-ttu-id="f208e-p116">Gibt an, ob der Crawler den Inhalt während Enumeration zwischengespeichert. Wenn der Inhalt zwischengespeichert wird, werden der Crawler keine gestellt einer anderen Reise zur Inhaltsquelle beim Crawlen einzelne Elemente.</span><span class="sxs-lookup"><span data-stu-id="f208e-p116">Specifies whether the crawler caches the content during enumeration. If the content is cached, the crawler does not make another trip to the content source when it crawls individual items.</span></span>  <br/> |
|<span data-ttu-id="f208e-196">EnumerateIdsOnly</span><span class="sxs-lookup"><span data-stu-id="f208e-196">EnumerateIdsOnly</span></span>  <br/> |<span data-ttu-id="f208e-197">FilterDescriptor</span><span class="sxs-lookup"><span data-stu-id="f208e-197">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="f208e-198">Gibt an, ob in **IDEnumerator** nur IDs zurückgegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f208e-198">Specifies whether to return IDs only in the **IDEnumerator**.</span></span>  <br/> |
|<span data-ttu-id="f208e-199">CrawlStartTime</span><span class="sxs-lookup"><span data-stu-id="f208e-199">CrawlStartTime</span></span>  <br/> |<span data-ttu-id="f208e-200">FilterDescriptor</span><span class="sxs-lookup"><span data-stu-id="f208e-200">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="f208e-201">Enthält die Startzeit der letzten Durchforstung.</span><span class="sxs-lookup"><span data-stu-id="f208e-201">Contains the start time of the last crawl.</span></span>  <br/> |
|<span data-ttu-id="f208e-202">SynchronizationCookie</span><span class="sxs-lookup"><span data-stu-id="f208e-202">SynchronizationCookie</span></span>  <br/> |<span data-ttu-id="f208e-203">FilterDescriptor</span><span class="sxs-lookup"><span data-stu-id="f208e-203">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="f208e-p117">Gibt an, dass die externe Inhaltsquelle nach einer Durchforstung ein Cookie zurückgibt, das anschließend vom Indizierungskonnektor während des nächsten Aufzählungsaufrufs erneut gesendet wird. Die externe Inhaltsquelle nutzt das Cookie, um zu bestimmen, was sich seit der letzten Durchforstung geändert hat. Diese Eigenschaft wird mit Instanzen der Methoden **ChangedIDEnumerator** und **DeletedIDEnumerator** verwendet. </span><span class="sxs-lookup"><span data-stu-id="f208e-p117">Specifies that the external content source returns a cookie after a crawl, which is then resent by the indexing connector during the next enumeration call. The external content source uses the cookie to determine what has changed since the last crawl. This property is used with **ChangedIDEnumerator** and **DeletedIDEnumerator** method instances. </span></span><br/> |
|<span data-ttu-id="f208e-207">Property</span><span class="sxs-lookup"><span data-stu-id="f208e-207">Property</span></span>  <br/> |<span data-ttu-id="f208e-208">TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="f208e-208">TypeDescriptor</span></span>  <br/> | <span data-ttu-id="f208e-p118">Gibt das **struct**-Array an, das bei der Suche nach Eigenschaften verwendet wird und aus Folgendem besteht:</span><span class="sxs-lookup"><span data-stu-id="f208e-p118">Specifies the **struct** array used by search for properties. Consists of the following: </span></span><br/> <ul><li><span data-ttu-id="f208e-211">**PropertyName**</span><span class="sxs-lookup"><span data-stu-id="f208e-211">**PropertyName**</span></span></li><li><span data-ttu-id="f208e-212">**PropertyValue**</span><span class="sxs-lookup"><span data-stu-id="f208e-212">**PropertyValue**</span></span></li><li><span data-ttu-id="f208e-213">**PropertyCulture**</span><span class="sxs-lookup"><span data-stu-id="f208e-213">**PropertyCulture**</span></span></li></ul> |
|<span data-ttu-id="f208e-214">Text</span><span class="sxs-lookup"><span data-stu-id="f208e-214">Text</span></span>  <br/> |<span data-ttu-id="f208e-215">TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="f208e-215">TypeDescriptor</span></span>  <br/> | <span data-ttu-id="f208e-p119">Gibt das **struct**-Array an, das von der Suche für Anlagen verwendet wird. Dies besteht aus Folgendem:</span><span class="sxs-lookup"><span data-stu-id="f208e-p119">Specifies the **struct** array used by search for attachments. Consists of the following: </span></span><br/> <ul><li><span data-ttu-id="f208e-218">**TextExtension**</span><span class="sxs-lookup"><span data-stu-id="f208e-218">**TextExtension**</span></span></li><li><span data-ttu-id="f208e-219">**TextContentType**</span><span class="sxs-lookup"><span data-stu-id="f208e-219">**TextContentType**</span></span></li><li><span data-ttu-id="f208e-220">**TextValue**</span><span class="sxs-lookup"><span data-stu-id="f208e-220">**TextValue**</span></span></li></ul> <br/> |
   

## <a name="bdc-model-file-changes-to-improve-performance-when-crawling-external-data"></a><span data-ttu-id="f208e-221">BDC-Modell Datei Änderungen zum Verbessern der Leistung beim Crawlen von externer Daten</span><span class="sxs-lookup"><span data-stu-id="f208e-221">BDC model file changes to improve performance when crawling external data</span></span>
<span data-ttu-id="f208e-222"><a name="SearchBDCModelProperties_Performance"> </a></span><span class="sxs-lookup"><span data-stu-id="f208e-222"><a name="SearchBDCModelProperties_Performance"> </a></span></span>

<span data-ttu-id="f208e-p120">Wenn Sie möchten eine BDC-Modelldatei für ein externes System zu erstellen, die Sie für die Suche aktivieren möchten, können Sie die Modelldatei zum Optimieren der Leistung beim Durchforsten externer Systeme verbessern. In diesem Abschnitt werden Verfahren zum Ändern der BDC-Modelldatei zum Verbessern der Leistung.</span><span class="sxs-lookup"><span data-stu-id="f208e-p120">When you want to create a BDC model file for an external system that you want to enable for search, you can enhance the model file to optimize performance when crawling external systems. This section describes ways to modify the BDC model file to improve performance.</span></span>
  
    
    

### <a name="use-inline-property-io-when-retrieving-large-scale-data"></a><span data-ttu-id="f208e-225">Verwenden der eingebetteten Eigenschafts-E/A beim Abrufen großer Datenmengen</span><span class="sxs-lookup"><span data-stu-id="f208e-225">Use inline property I/O when retrieving large-scale data</span></span>

<span data-ttu-id="f208e-226">Wenn für ein einzelnes Element große Datenmengen zurückgegeben werden, sollten Sie für die Rückgabe generell nicht die **SpecificFinder**-Methode, sondern eine der folgenden Spezialmethoden zum Abrufen der Daten verwenden:</span><span class="sxs-lookup"><span data-stu-id="f208e-226">In general, if some of the data returned for an item is large scale, instead of returning it with the **SpecificFinder** method, you should use one of the following specialized methods to retrieve the data:</span></span>
  
    
    

- <span data-ttu-id="f208e-227">Verwenden Sie die **BinarySecurityDescriptorAccessor**-Methode, wenn eine Sicherheits-Zugriffssteuerungsliste (Security Access Control List, SACL) anstelle der **WindowsSecurityDescriptor**-Eigenschaft übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="f208e-227">Use the **BinarySecurityDescriptorAccessor** method when passing a security access control list (ACL) instead of the **WindowsSecurityDescriptor** property.</span></span>
    
  
- <span data-ttu-id="f208e-228">Verwenden Sie zum Übergeben von Datenströmen die **StreamAccessor**-Methode.</span><span class="sxs-lookup"><span data-stu-id="f208e-228">Use the **StreamAccessor** method when passing streams.</span></span>
    
  
<span data-ttu-id="f208e-229">Außer bei einer langen Netzwerkwartezeit ist die Leistung meist besser als bei einem zusätzlichen Abrufvorgang des externen Systems.</span><span class="sxs-lookup"><span data-stu-id="f208e-229">Unless network latency is high, the improved performance is usually better than the cost of an extra trip to the external system.</span></span>
  
    
    

### <a name="enumeration-optimization-when-crawling-external-systems"></a><span data-ttu-id="f208e-230">Aufzählungsoptimierung beim Durchforsten externer Systeme</span><span class="sxs-lookup"><span data-stu-id="f208e-230">Enumeration optimization when crawling external systems</span></span>

<span data-ttu-id="f208e-p121">Zählen Sie pro Aufruf an das externe System nicht mehr als 100.000 Elemente auf. Lang andauernde Aufzählungen können zwischenzeitliche Unterbrechungen verursachen und den Abschluss einer Durchforstung verhindern. Es wird empfohlen, dass Ihr BDC-Modell die Daten in logischen Ordnern strukturiert, die einzeln aufgezählt werden können (siehe das folgende Beispiel).</span><span class="sxs-lookup"><span data-stu-id="f208e-p121">Do not enumerate more than 100,000 items per call to the external system. Long-running enumerations can cause intermittent interruptions and prevent a crawl from completing. We recommend that your BDC model structures the data into logical folders that can be enumerated individually, as shown in the following example.</span></span> 
  
    
    
<span data-ttu-id="f208e-p122">Dieses Beispiel veranschaulicht das Aufzählen für eine Datenbanktabelle mit einer Million Zeilen, aber mit einer festen Gruppe von Werten in der Spalte "ColumnA". In diesem Szenario können Sie "ColumnA" als den externen Inhaltstyp betrachten und mithilfe der folgenden SQL-Anweisung einen Enumerator für diese Wertegruppe schreiben.</span><span class="sxs-lookup"><span data-stu-id="f208e-p122">This example demonstrates enumerating against a database table with one million rows, but with a fixed set of values in ColumnA. In this scenario, you can consider ColumnA as the external content type and write an enumerator for this set of values by using the following SQL statement.</span></span> 
  
    
    



```sql

SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table
```

<span data-ttu-id="f208e-236">Definieren Sie nun mit der folgenden SQL-Anweisung den spezifischen Finder.</span><span class="sxs-lookup"><span data-stu-id="f208e-236">Next, define the specific finder using the following SQL statement.</span></span> 
  
    
    



```sql
SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table where ColumnA = @Value
```

<span data-ttu-id="f208e-237">Schließlich müssen Sie den Zuordnungsnavigationsvorgang wie folgt definieren.</span><span class="sxs-lookup"><span data-stu-id="f208e-237">Finally, you must define the association navigation operation, as follows.</span></span> 
  
    
    



```sql
Select * from table where ColumnA=@value
```

<span data-ttu-id="f208e-p123">Eine Methode muss binnen zwei Minuten mit der Rückgabe von Ergebnissen beginnen. Andernfalls bricht der Crawler den Aufruf ab. Die Ausführung einer komplexen SQL-Anweisung mit der **LIKE**-Klausel kann beispielsweise länger als zwei Minuten dauern, was den Crawler zum Abbrechen des Aufrufs veranlassen würde.</span><span class="sxs-lookup"><span data-stu-id="f208e-p123">Any method should begin returning results within two minutes, or the crawler will cancel the call. For example, a complex SQL statement that uses a **LIKE** clause may take longer than two minutes to complete, and would cause the crawler to cancel the call.</span></span>
  
    
    

### <a name="improving-crawl-speed-with-the-useclientcachingforsearch-property"></a><span data-ttu-id="f208e-240">Erhöhen der Durchforstungsgeschwindigkeit mithilfe der "UseClientCachingForSearch"-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f208e-240">Improving crawl speed with the UseClientCachingForSearch property</span></span>

<span data-ttu-id="f208e-p124">Die **UseClientCachingForSearch**-Eigenschaft beschleunigt vollständige Durchforstungen, indem das Element während der Aufzählung zwischengespeichert wird. Diese Eigenschaft wird auch empfohlen, wenn inkrementelle auf Änderungsprotokollen basierende Durchforstungen implementiert werden, da dadurch inkrementelle Durchforstungen beschleunigt.</span><span class="sxs-lookup"><span data-stu-id="f208e-p124">The **UseClientCachingForSearch** property improves the speed of full crawls by caching the item during enumeration. Using this property is also recommended when implementing incremental crawls that are based on change logs, because it improves incremental crawl speed.</span></span>
  
    
    

> <span data-ttu-id="f208e-243">**Wichtig:** Wenn Elemente durchschnittlich größer als 30 KB sind, legen Sie diese Eigenschaft nicht fest, da sie eine beträchtliche Anzahl von Cachefehlern verursacht und Leistungsvorteile zunichte macht.</span><span class="sxs-lookup"><span data-stu-id="f208e-243">**Important:** If items are larger than 30 kilobytes on average, do not set this property, as it will lead to a significant number of cache misses and negate performance gains.</span></span> 
  
    
    


## <a name="security-in-bdc-model-files"></a><span data-ttu-id="f208e-244">Sicherheit in BDC-Modelldateien</span><span class="sxs-lookup"><span data-stu-id="f208e-244">Security in BDC model files</span></span>
<span data-ttu-id="f208e-245"><a name="SearchBDCModelProperties_Security"> </a></span><span class="sxs-lookup"><span data-stu-id="f208e-245"><a name="SearchBDCModelProperties_Security"> </a></span></span>

<span data-ttu-id="f208e-246">Wenn das Repository die NTLM-Authentifizierung verwendet, wird empfohlen, für Durchforstungen die PassThrough-Authentifizierung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="f208e-246">If the repository uses NTLM authentication, we recommend that you specify PassThrough authentication for crawling.</span></span>
  
    
    
<span data-ttu-id="f208e-p125">Profilseiten können erfordern, dass Sie den Dienst für Einmaliges Anmelden aufgrund des Delegierungsproblems bei Mehrfachhops auf dem Front-End-Webserver verwenden müssen. Bei Auftreten dieses Problems können Sie die Durchforstung optimieren und gleichzeitig das Erstellen von Profilseiten zulassen, indem Sie zwei ähnliche **LobSystemInstance**-Instanzen erstellen. Die erste Instanz muss Anmeldeinformationen aus der Authentifizierung für Einmaliges Anmelden verwenden. Diese Instanz darf nicht die **ShowInSearchUI**-Eigenschaft enthalten. Die zweite Instanz muss die PassThrough-Authentifizierung verwenden und die **ShowInSearchUI**-Eigenschaft enthalten. Profilseiten verwenden die erste **LobSystemInstance**-Instanz, der Crawler die zweite Instanz.</span><span class="sxs-lookup"><span data-stu-id="f208e-p125">Profile pages may require that you use the Secure Store Service because of the multi-hop delegation problem from the front-end web server. If you encounter this problem, you can optimize the crawl while still allowing profile pages by creating two similar **LobSystemInstance** instances. The first instance should use credentials from the Secure Store Service authentication. This instance should not contain the **ShowInSearchUI** property. The second instance should use PassThrough authentication, and should contain the **ShowInSearchUI** property. Profile pages use the first **LobSystemInstance** instance, and the crawler uses the second instance.</span></span>
  
> [!NOTE]
> <span data-ttu-id="f208e-253">Dies erfordert, dass Sie die **ShowInSearchUI**-Eigenschaft auf **LobSystemInstance**-Ebene anstatt auf **LobSystem**-Ebene festlegen.</span><span class="sxs-lookup"><span data-stu-id="f208e-253">This requires that you set the **ShowInSearchUI** property at the **LobSystemInstance** level instead of at the **LobSystem** level.</span></span>


## <a name="see-also"></a><span data-ttu-id="f208e-254">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f208e-254">See also</span></span>
<span data-ttu-id="f208e-255"><a name="SP15enhanceBDC_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f208e-255"><a name="SP15enhanceBDC_addlresources"> </a></span></span>


-  [<span data-ttu-id="f208e-256">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f208e-256">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  <span data-ttu-id="f208e-257">[Infrastruktur des BDC-Modells](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="f208e-257">[BDC Model Infrastructure](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="f208e-258">[Erstellen von BDC-Modellen](http://msdn.microsoft.com/library/170d1cfd-cf19-4162-b79f-ba6d3b4ad23b%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="f208e-258">[Authoring BDC Models](http://msdn.microsoft.com/library/170d1cfd-cf19-4162-b79f-ba6d3b4ad23b%28Office.15%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="f208e-259">Einrichten einer Entwicklungsumgebung für BCS in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f208e-259">Setting up a development environment for BCS in SharePoint</span></span>](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  <span data-ttu-id="f208e-260">[Vorgehensweise: Erstellen einer BDC-Modelldatei für einen benutzerdefinierten Konnektor in SharePoint Designer](http://msdn.microsoft.com/library/8f239482-0c82-4b60-817d-b0c4392e7e2e%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="f208e-260">[How to: Use SharePoint Designer to Create a BDC Model File for a Custom Connector](http://msdn.microsoft.com/library/8f239482-0c82-4b60-817d-b0c4392e7e2e%28Office.15%29.aspx)</span></span>
    
  

