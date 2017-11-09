---
title: "Durchführen von Batchanforderungen mit den REST-APIs"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b415b086175b366fbbc6d920186198b096cc85c7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="make-batch-requests-with-the-rest-apis"></a><span data-ttu-id="e2b11-102">Durchführen von Batchanforderungen mit den REST-APIs</span><span class="sxs-lookup"><span data-stu-id="e2b11-102">Make batch requests with the REST APIs</span></span>
<span data-ttu-id="e2b11-103">Erfahren Sie, wie Sie die Abfrageoption `$batch` mit den REST-/OData-APIs verwenden.</span><span class="sxs-lookup"><span data-stu-id="e2b11-103">Learn how to use the  `$batch` query option with the REST/OData APIs.</span></span>
 
<span data-ttu-id="e2b11-p101">In diesem Artikel wird beschrieben, wie Sie Vorgänge und Abfragen an die REST-/OData-API von Microsoft SharePoint Online (sowie des lokalen SharePoint 2016 und höher) und die [Unterklasse Dateien und Ordner](http://msdn.microsoft.com/en-us/office/office365/api/files-rest-operations) der Office 365 REST-APIs zusammenfassen. Mit diesem Verfahren können Sie die Leistung Ihrer Add-ins verbessern, indem Sie mehrere Vorgänge in einer einzelnen Anforderung an den Server und einer einzelnen Antwort kombinieren.</span><span class="sxs-lookup"><span data-stu-id="e2b11-p101">This article describes how you can batch queries and operations against the REST/OData API of Microsoft SharePoint Online (and on-premise SharePoint 2016 and later) and the  [Files and folders subset](http://msdn.microsoft.com/en-us/office/office365/api/files-rest-operations) of the Office 365 REST APIs. With this technique you can improve the performance of your add-in by combining many operations into a single request to the server and a single response back.</span></span>

## <a name="executive-summary-of-the-batch-option"></a><span data-ttu-id="e2b11-106">Zusammenfassung der $batch-Option</span><span class="sxs-lookup"><span data-stu-id="e2b11-106">Executive summary of the $batch option</span></span>
<span data-ttu-id="e2b11-p102">SharePoint Online (sowie das lokale SharePoint 2016 und höher) und die Office 365-APIs implementieren die OData-`$batch`-Abfrageoption. Details zu ihrer Verwendung können Sie der [offiziellen Dokumentation](http://www.odata.org/documentation/odata-version-3-0/batch-processing) entnehmen. Sie können auch die Blogbeiträge von Andrew Connell zu diesem Thema lesen, beginnend bei [Part 1 - SharePoint REST API Batching](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests) (Teil 1: Batchverarbeitung mit der SharePoint REST-API). Im Folgenden finden Sie eine Zusammenfassung der wichtigsten Punkte:</span><span class="sxs-lookup"><span data-stu-id="e2b11-p102">SharePoint Online (and on-premise SharePoint 2016 and later) and the Office 365 APIs implement the OData  `$batch` query option, so you can rely on [the official documentation](http://www.odata.org/documentation/odata-version-3-0/batch-processing) for details about how to use it. (Another option is to see Andrew Connell's blog posts on the subject beginning at [Part 1 - SharePoint REST API Batching](http://www.andrewconnell.com/blog/part-1-sharepoint-rest-api-batching-understanding-batching-requests).) The following is only a reminder of the major points:</span></span>
 
- <span data-ttu-id="e2b11-109">Die URL der Anforderung besteht aus der Stammdienst-URL und der Option `$batch`. Beispiel: `https://fabrikam.sharepoint.com/_api/$batch` oder `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span><span class="sxs-lookup"><span data-stu-id="e2b11-109">The request URL consists of the root service URL and the  `$batch` option; for example, `https://fabrikam.sharepoint.com/_api/$batch` or `https://fabrikam.office365.com/api/v1.0/me/$batch`.</span></span>
    
- <span data-ttu-id="e2b11-110">Der HTTP-Anforderungstext ist im MIME-Typ *multipart/mixed*.</span><span class="sxs-lookup"><span data-stu-id="e2b11-110">The HTTP request body is MIME type  *multipart/mixed*  .</span></span>
    
- <span data-ttu-id="e2b11-111">Der Text der Anforderung ist in Bereiche unterteilt, die durch eine Trennzeichenfolge voneinander getrennt sind, die im Header der Anforderung angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="e2b11-111">The body of the request is divided into parts that are separated from each other by a boundary string that is specified in the header of the request.</span></span>
    
- <span data-ttu-id="e2b11-112">Jeder Teil des Textkörpers verfügt über ein eigenes HTTP-Verb, eine eigene REST-URL sowie einen eigenen internen Textkörper, falls zutreffend.</span><span class="sxs-lookup"><span data-stu-id="e2b11-112">Each part of the body has its own HTTP verb and REST URL, and its own internal body when applicable.</span></span>
    
- <span data-ttu-id="e2b11-p103">Ein Teil kann ein Lesevorgang (oder Funktionsaufruf) sein, bzw. ein ChangeSet einer oder mehrerer Schreibvorgänge (oder Funktionsaufrufe). Ein ChangeSet ist selbst ein MIME-Typ *multipart/mixed* mit Unterteilen, die Einfüge-, Aktualisierungs- oder Löschvorgänge enthalten.</span><span class="sxs-lookup"><span data-stu-id="e2b11-p103">A part can be a read operation (or function invocation), or a ChangeSet of one or more write operations (or function invocations). A ChangeSet is itself a MIME type  *multipart/mixed*  with subparts that contain insert, update, or delete operations.</span></span>
    
     <span data-ttu-id="e2b11-p104">**Wichtig** Derzeit unterstützen SharePoint- und Office 365-APIs nicht die Funktion „alles oder nichts“ für ChangeSets mit mehr als einem Vorgang. Wenn einer der untergeordneten Vorgänge fehlschlägt, werden die anderen ausgeführt und nicht rückgängig gemacht.</span><span class="sxs-lookup"><span data-stu-id="e2b11-p104">**Important**  At this time, SharePoint and Office 365 APIs do not support "all or nothing" functionality for ChangeSets that have more than one operation within them. If any of the child operations fails, the others still complete and are not rolled back.</span></span>

## <a name="code-samples"></a><span data-ttu-id="e2b11-117">Codebeispiele</span><span class="sxs-lookup"><span data-stu-id="e2b11-117">Code samples</span></span>
<span data-ttu-id="e2b11-118">Beispiele für Code, der die Abfrageoption `$batch` für die SharePoint REST/OData-APIs verwendet:</span><span class="sxs-lookup"><span data-stu-id="e2b11-118">Samples of code that uses the  `$batch` query option against the SharePoint REST/OData APIs:</span></span> 

-  <span data-ttu-id="e2b11-119">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span><span class="sxs-lookup"><span data-stu-id="e2b11-119">**C#:** [OfficeDev/Core.ODataBatch](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.ODataBatch)</span></span>
-  <span data-ttu-id="e2b11-120">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span><span class="sxs-lookup"><span data-stu-id="e2b11-120">**JavaScript:** [andrewconnell/sp-o365-rest](https://github.com/andrewconnell/sp-o365-rest/blob/master/SpRestBatchSample/Scripts/App.js)</span></span>
    

## <a name="example-requests-and-responses"></a><span data-ttu-id="e2b11-121">Beispielanforderungen und -antworten</span><span class="sxs-lookup"><span data-stu-id="e2b11-121">Example requests and responses</span></span>
<span data-ttu-id="e2b11-122">Das folgende Beispiel zeigt eine unformatierte HTTP-Anforderung, die zwei GET-Vorgänge zusammenfasst, die die Titel aller Elemente in zwei verschiedenen Listen abrufen.</span><span class="sxs-lookup"><span data-stu-id="e2b11-122">The following is an example of a raw HTTP request that batches two GET operations that retrieve the titles of all the items in two different lists.</span></span>

```
POST https://fabrikam.sharepoint.com/_api/$batch HTTP/1.1
Authorization: Bearer <access token omitted>
Content-Type: multipart/mixed; boundary=batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Host: fabrikam.sharepoint.com
Content-Length: 527
Expect: 100-continue

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('Composed%20Looks')/items?$select=Title HTTP/1.1

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('User%20Information%20List')/items?$select=Title HTTP/1.1

--batch_e3b6819b-13c3-43bb-85b2-24b14122fed1--

```

<span data-ttu-id="e2b11-123">Das folgende Beispiel zeigt den Textkörper einer unformatierten HTTP-Anforderung, die ein DELETE einer Liste und ein GET der SharePoint-Liste der Listen zusammenfasst.</span><span class="sxs-lookup"><span data-stu-id="e2b11-123">The following is an example of the body of a raw HTTP request that batches a DELETE of a list and a GET of the SharePoint list-of-lists.</span></span>
 
```
POST https://fabrikam.sharepoint.com/_api/$batch HTTP/1.1
Authorization: Bearer <access token omitted>
Content-Type: multipart/mixed; boundary=batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Host: fabrikam.sharepoint.com
Content-Length: 647
Expect: 100-continue

--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Content-Type: multipart/mixed; boundary=changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d

--changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d
Content-Type: application/http
Content-Transfer-Encoding: binary

DELETE https://fabrikam.sharepoint.com/_api/Web/lists/getbytitle('OldList') HTTP/1.1
If-Match: "1"

--changeset_efb6b37c-a5cd-45cb-8f5f-4d648006e65d--
--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://fabrikam.sharepoint.com/_api/Web/lists HTTP/1.1

--batch_7ba8d60b-efce-4a2f-b719-60c27cc0e70e--
```


## <a name="links-to-helpful-libraries"></a><span data-ttu-id="e2b11-124">Links zu hilfreichen Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="e2b11-124">Links to helpful libraries</span></span>
<span data-ttu-id="e2b11-p105">Es gibt zahlreiche OData-Bibliotheken, die die OData-Batchverarbeitung für viele Sprachen unterstützen. Zwei Beispiele sind nachstehend aufgeführt. Eine vollständige Liste finden Sie unter [OData Libraries OData-Bibliotheken](http://www.odata.org/libraries/).</span><span class="sxs-lookup"><span data-stu-id="e2b11-p105">There are OData libraries that support OData batching for many languages. Two examples are below. For a more complete list, see  [OData Libraries](http://www.odata.org/libraries/).</span></span>

-  <span data-ttu-id="e2b11-p106">[.NET OData-Bibliothek](http://msdn.microsoft.com/en-us/office/microsoft.data.odata%28v=vs.90%29). Siehe insbesondere die **ODataBatch***-Klassen.</span><span class="sxs-lookup"><span data-stu-id="e2b11-p106">[.NET OData library](http://msdn.microsoft.com/en-us/office/microsoft.data.odata%28v=vs.90%29). See especially the  **ODataBatch*** classes.</span></span>
-  <span data-ttu-id="e2b11-p107">[Datajs-Bibliothek](http://datajs.codeplex.com/documentation). Siehe insbesondere [Batchvorgänge](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span><span class="sxs-lookup"><span data-stu-id="e2b11-p107">[Datajs library](http://datajs.codeplex.com/documentation). See especially  [Batch operations](http://datajs.codeplex.com/wikipage?title=datajs%20OData%20API&amp;referringTitle=Documentation#Batch).</span></span>