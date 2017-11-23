---
title: "Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fbbf0cc4-e135-426a-9996-34eb954dbd5a
ms.openlocfilehash: d42bb0cbc5bf1976fd772b0ad900c5f550907d9f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="custom-security-trimming-for-search-in-sharepoint"></a><span data-ttu-id="2f354-102">Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f354-102">Custom security trimming for Search in SharePoint Server 2013</span></span>
<span data-ttu-id="2f354-p101">Erfahren Sie mehr über die zwei Arten von benutzerdefinierten Security Trimmer Schnittstellen, **ISecurityTrimmerPre** und **ISecurityTrimmerPost**, und die Schritte, die Sie ausführen müssen, um ein benutzerdefinierter Security Trimmer zu erstellen. Zum Zeitpunkt der Abfrage führt Suche in SharePoint sicherheitskürzung von Suchergebnissen, die auf die Identität des Benutzers, senden Sie die Abfrage, mithilfe der Sicherheitsinformationen aus der Durchforstungskomponente basieren.</span><span class="sxs-lookup"><span data-stu-id="2f354-p101">Learn about the two kinds of custom security trimmer interfaces, **ISecurityTrimmerPre** and **ISecurityTrimmerPost**, and the steps you must take to create a custom security trimmer. At query time, Search in SharePoint performs security trimming of search results that are based on the identity of the user submitting the query, by using the security information obtained from the crawl component.</span></span>
  
    
    

<span data-ttu-id="2f354-p102">Sie müssen bestimmte Szenarien, jedoch in denen die integrierte Sicherheit verkürzen Ergebnisse für Ihren Anforderungen nicht ausreichend. In solchen Szenarien müssen Sie benutzerdefinierte sicherheitskürzung implementieren. Suche in SharePoint bietet Unterstützung für benutzerdefinierte sicherheitskürzung durch die  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) Benutzeroberflächen, [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) Benutzeroberflächen und [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) Benutzeroberflächen (veraltet) im Namespace [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) . **Hinweis:** Benutzerdefinierte Pre Rasentrimmer unterstützt nicht Windows SIDs in Zugriffssteuerungslisten, nur Ansprüche. Wenn der SID Ansprüche, die Typen von einer benutzerdefinierten Pre Trimmer zurückgegeben werden, werden die resultierende ACE-Einträge in den Index als Anspruch, nicht als SID codiert werden. Sie daher nicht Windows-Benutzeridentitäten übereinstimmen, die auf SIDs basieren.</span><span class="sxs-lookup"><span data-stu-id="2f354-p102">You might have certain scenarios, however, in which the built-in security trimming results aren't sufficient for your requirements. In such scenarios, you need to implement custom security trimming. Search in SharePoint provides support for custom security trimming through the  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) interface, [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) interface, and [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) interface (deprecated) in the [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace. **Note:** Custom pre-trimmers don't support Windows SIDs in ACLs, only claims. If any of the SID claim types are returned from a custom pre-trimmer, the resulting ACEs in the index will be encoded as a claim, not as SID. Hence they do not match Windows user identities that are based on SIDs.</span></span>
  
    
    


## <a name="implementing-the-interfaces-for-custom-security-trimming"></a><span data-ttu-id="2f354-111">Implementieren der Schnittstellen für benutzerdefinierte sicherheitskürzung</span><span class="sxs-lookup"><span data-stu-id="2f354-111">Implementing the interfaces for custom security trimming</span></span>
<span data-ttu-id="2f354-112"><a name="Implementing_the_interfaces"> </a></span><span class="sxs-lookup"><span data-stu-id="2f354-112"></span></span>

<span data-ttu-id="2f354-p103">Die Benutzeroberfläche **ISecurityTrimmerPre** führt vor dem Zuschneiden oder vor dem Abfrage Auswertung, wo die Suchabfrage portiert ist Sicherheitsinformationen hinzufügen, bevor die Suchabfrage an den Suchindex verglichen wird. Die Benutzeroberfläche **ISecurityTrimmerPost** führt nach der verkürzen, oder nach der Abfrage Auswertung, wo die Suchergebnisse gelöscht werden, bevor sie an den Benutzer zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2f354-p103">The **ISecurityTrimmerPre** interface carries out pre-trimming, or pre-query evaluation, where the search query is rewritten to add security information before the search query is matched to the search index. The **ISecurityTrimmerPost** interface carries out post-trimming, or post-query evaluation, where the search results are pruned before they are returned to the user.</span></span>
  
    
    
<span data-ttu-id="2f354-p104">Es empfiehlt sich die Verwendung von vor dem Zuschneiden für Leistung und allgemeine Richtigkeit; vor dem Zuschneiden verhindert Datenverlust für Einschränkung Daten und die Anzahl der Zugriffe Instanzen. Nach der Rasentrimmer können in Fällen verwendet werden, in dem die sicherheitskürzung am genauesten mit Abfrage Filter dargestellt werden kann. Es ist Dokumente einer müssen abwesend filtern beispielsweise je nach der lokalen Zeit des Benutzers, der die Abfrage, wie z. B. offizielle üblichen Geschäftszeiten nur ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="2f354-p104">We recommend the use of pre-trimming for performance and general correctness; pre-trimming prevents information leakage for refiner data and hit count instances. Post-trimmers can be used in cases where the security trimming cannot be represented accurately with query filters; for example, if there is a need to filter away documents depending on the local time of the user issuing the query, such as during official business hours only.</span></span>
  
    
    

### <a name="implementing-the-isecuritytrimmerpre-interface"></a><span data-ttu-id="2f354-117">Implementieren der ISecurityTrimmerPre-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="2f354-117">Implementing the ISecurityTrimmerPre interface</span></span>

<span data-ttu-id="2f354-118">Um ein benutzerdefinierter Security Pre Trimmer für Suchergebnisse zu erstellen, müssen Sie eine Komponente erstellen, die die **ISecurityTrimmerPre** Schnittstelle implementiert.</span><span class="sxs-lookup"><span data-stu-id="2f354-118">To create a custom security pre-trimmer for search results, you must create a component that implements the **ISecurityTrimmerPre** interface.</span></span>
  
    
    
<span data-ttu-id="2f354-119">Die Benutzeroberfläche **ISecurityTrimmerPre** enthält zwei Methoden, mit denen Sie implementieren müssen: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) und [AddAccess(Boolean, Claims)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2f354-119">The **ISecurityTrimmerPre** interface contains two methods that you must implement: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) and [AddAccess(Boolean, Claims)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .</span></span>
  
    
    

#### <a name="initialize-method"></a><span data-ttu-id="2f354-120">"Initialize"-Methode</span><span class="sxs-lookup"><span data-stu-id="2f354-120">Initialize Method</span></span>

<span data-ttu-id="2f354-p105">Die **Initialize** -Methode wird ausgeführt, wenn die Vorabversion Trimmer Sicherheit in Worker-Prozess geladen wird, und nicht erneut ausgeführt wird, bis der Worker-Prozess wieder verwendet wird. Zwei Parameter werden an die Methode übergeben:</span><span class="sxs-lookup"><span data-stu-id="2f354-p105">The **Initialize** method is executed when the security pre-trimmer is loaded into the worker process, and does not execute again until the worker process is recycled. Two parameters are passed into the method:</span></span>
  
    
    

-  <span data-ttu-id="2f354-123">_staticProperties_: ein  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) Objekt, enthält die Konfigurationseigenschaften, die für die Sicherheit Trimmer angegeben werden, wenn sie mit der Suchdienstanwendung registriert wird.</span><span class="sxs-lookup"><span data-stu-id="2f354-123">_staticProperties_: A  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) object containing the configuration properties that are specified for the security trimmer when it is registered with the Search service application.</span></span>
    
  
-  <span data-ttu-id="2f354-124">_searchApplication_: ein  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) -Objekt, das die Suchdienstanwendung darstellt.</span><span class="sxs-lookup"><span data-stu-id="2f354-124">_searchApplication_: A  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) object that represents the Search service application.</span></span>
    
  

#### <a name="addaccess-method"></a><span data-ttu-id="2f354-125">AddAccess-Methode</span><span class="sxs-lookup"><span data-stu-id="2f354-125">AddAccess Method</span></span>

<span data-ttu-id="2f354-126">Die Methode **AddAccess** wird einmal ausgeführt, pro Pre Trimmer, für jede eingehende Abfrage, bevor die Abfrage ausgewertet wird.</span><span class="sxs-lookup"><span data-stu-id="2f354-126">The **AddAccess** method is executed once per pre-trimmer, for each incoming query before the query is evaluated.</span></span>
  
    
    
<span data-ttu-id="2f354-127">In dieser Methode werden zwei Parameter übergeben:</span><span class="sxs-lookup"><span data-stu-id="2f354-127">Two parameters are passed into this method:</span></span> 
  
    
    

-  <span data-ttu-id="2f354-128">_sessionProperties_: ein **[T:System.Collections.Generic.IDictionary<String,Object>]** -Objekt, das die Eigenschaften der Abfrage enthält.</span><span class="sxs-lookup"><span data-stu-id="2f354-128">_sessionProperties_: A **[T:System.Collections.Generic.IDictionary<String,Object>]** object that contains the properties of the query.</span></span>
    
  
-  <span data-ttu-id="2f354-129">_userIdentity_: ein  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) -Objekt, das die Identität des Benutzers enthält.</span><span class="sxs-lookup"><span data-stu-id="2f354-129">_userIdentity_: A  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) object that contains the user identity.</span></span>
    
  

### <a name="implementing-the-isecuritytrimmerpost-interface"></a><span data-ttu-id="2f354-130">Implementieren der ISecurityTrimmerPost-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="2f354-130">Implementing the ISecurityTrimmerPost interface</span></span>

<span data-ttu-id="2f354-131">Um ein benutzerdefinierter Security nach der Trimmer für Suchergebnisse zu erstellen, müssen Sie eine Komponente erstellen, die die **ISecurityTrimmerPost** Schnittstelle implementiert.</span><span class="sxs-lookup"><span data-stu-id="2f354-131">To create a custom security post-trimmer for search results, you must create a component that implements the **ISecurityTrimmerPost** interface.</span></span>
  
    
    
<span data-ttu-id="2f354-132">Die Benutzeroberfläche **ISecurityTrimmerPost** enthält zwei Methoden, mit denen Sie implementieren müssen: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) und **CheckAccess(IList<String>, IList<String>, IDictionary<String, Object>, IIdentity)**.</span><span class="sxs-lookup"><span data-stu-id="2f354-132">The **ISecurityTrimmerPost** interface contains two methods that you must implement: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) and **CheckAccess(IList<String>, IList<String>, IDictionary<String, Object>, IIdentity)**.</span></span>
  
    
    

#### <a name="initialize-method"></a><span data-ttu-id="2f354-133">"Initialize"-Methode</span><span class="sxs-lookup"><span data-stu-id="2f354-133">Initialize method</span></span>

<span data-ttu-id="2f354-p106">Die **Initialize** Methode wird ausgeführt, wenn Security Trimmer in der Worker-Prozess geladen wird, und nicht erneut ausgeführt wird, bis der Worker-Prozess wieder verwendet wird. Zwei Parameter werden an die Methode übergeben: und</span><span class="sxs-lookup"><span data-stu-id="2f354-p106">The **Initialize** method is executed when the security trimmer is loaded into the worker process, and does not execute again until the worker process is recycled. Two parameters are passed into the method:and</span></span>
  
    
    

-  <span data-ttu-id="2f354-136">_staticProperties_: ein  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) Objekt, enthält die Konfigurationseigenschaften für die Sicherheit Trimmer angegeben werden, wenn sie mit der Suchdienstanwendung registriert wird.</span><span class="sxs-lookup"><span data-stu-id="2f354-136">_staticProperties_: A  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) object containing the configuration properties specified for the security trimmer when it is registered with the Search service application.</span></span>
    
  
-  <span data-ttu-id="2f354-137">_searchApplication_: ein  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) -Objekt, das die Suchdienstanwendung darstellt.</span><span class="sxs-lookup"><span data-stu-id="2f354-137">_searchApplication_: A  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) object that represents the Search service application.</span></span>
    
  

#### <a name="checkaccess-method"></a><span data-ttu-id="2f354-138">"CheckAccess"-Methode</span><span class="sxs-lookup"><span data-stu-id="2f354-138">CheckAccess method</span></span>

<span data-ttu-id="2f354-139">Die **CheckAccess** -Methode wird einmal pro nach der Trimmer, für jede Abfrage Ergebnis festlegen, ausgeführt, nachdem die Abfrage ausgewertet wird.</span><span class="sxs-lookup"><span data-stu-id="2f354-139">The **CheckAccess** method is executed once per post-trimmer, for each result set query, after the query is evaluated.</span></span>
  
    
    
<span data-ttu-id="2f354-140">An diese Methode werden vier Parameter übergeben:</span><span class="sxs-lookup"><span data-stu-id="2f354-140">Four parameters are passed into this method:</span></span>
  
    
    

-  <span data-ttu-id="2f354-141">
  _documentUrls_: Ein  [IList\<T\>](http://msdn2.microsoft.com/de-de/library/5y536ey6)-Objekt, das die URLs für jedes Inhaltselement in den Suchergebnissen enthält, das der Durchforstungsregel entspricht.</span><span class="sxs-lookup"><span data-stu-id="2f354-141">documentUrls: A  IList  object that contain the URLs for each content item from the search results that match the crawl rule.</span></span>
    
  
-  <span data-ttu-id="2f354-142">
  _documentAcls_: Ein [IList\<T\>](http://msdn2.microsoft.com/de-de/library/5y536ey6)-Objekt, das Element-ACLs für jedes Inhaltselement enthält, dessen Zugriff von der Security Trimmer-Implementierung zu bestimmen ist.</span><span class="sxs-lookup"><span data-stu-id="2f354-142">documentAcls: A  IList  object containing item ACLs for each content item whose access is to be determined by the security trimmer implementation.</span></span>
    
  
-  <span data-ttu-id="2f354-143">
  _sessionProperties_: Ein [IDictionary\<TKey, TValue\>](http://msdn2.microsoft.com/de-de/library/s4ys34ea)-Objekt, das den vorübergehenden Eigenschaftenbehälter enthält.</span><span class="sxs-lookup"><span data-stu-id="2f354-143">sessionProperties: A  IDictionary<TKey, TValue> object containing the transient property bag.</span></span>
    
  
-  <span data-ttu-id="2f354-144">_userIdentity_: Ein  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx)-Objekt, aus dem Implementierer die Identität des Benutzers abrufen können.</span><span class="sxs-lookup"><span data-stu-id="2f354-144">_userIdentity_: An  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) object from which implementers can retrieve the user's identity.</span></span>
    
  
<span data-ttu-id="2f354-p107">Die Methode **CheckAccess** gibt ein [BitArray](https://msdn.microsoft.com/library/System.Collections.BitArray.aspx) -Objekt, das ein Array von Werten **true** oder **false**, eine für jede Inhaltselement URL in das Objekt **IList** darstellt, der als erster Parameter der Methode übergeben wird. Verarbeitung Komponente die Abfrage verwendet diese Werte, um die nach der sicherheitskürzung der Ergebnisse durchzuführen. Wenn der Matrix-Wert für ein besonderes Inhaltselement **true**ist, ist das Element in die zurückgegebenen Ergebnisse enthalten; Wenn der Arraywert **false**ist, wird das Element entfernt.</span><span class="sxs-lookup"><span data-stu-id="2f354-p107">The **CheckAccess** method returns a [BitArray](https://msdn.microsoft.com/library/System.Collections.BitArray.aspx) object that represents an array of **true** or **false** values, one for each content item URL in the **IList** object that is passed as the first parameter of the method. The query processing component uses these values to perform the security post-trimming of the results. If the array value for a particular content item is **true**, the item is included in the returned results; if the array value is **false**, the item is removed.</span></span>
  
    
    
<span data-ttu-id="2f354-p108">Beim Implementieren der **CheckAccess** -Methode können Sie zweierlei Informationen für jedes Element verwenden, um festzustellen, ob **true** oder **false** für das Element zurückgeben: die Identität des Benutzers, der die Abfrage und die URL für das Inhaltselement übermittelt. Alternativ können Sie auch benutzerdefinierte ACL Dokumentinformationen aus der Verbinder an die Methode **CheckAccess** übergeben.</span><span class="sxs-lookup"><span data-stu-id="2f354-p108">When implementing the **CheckAccess** method, you can use two pieces of information for each item to determine whether to return **true** or **false** for the item: the identity of the user who submitted the query and the URL of the content item. Alternatively, you can also pass custom document ACL information from the connector to the **CheckAccess** method.</span></span>
  
    
    

#### <a name="retrieving-the-user-identity-for-your-security-trimmer"></a><span data-ttu-id="2f354-150">Abrufen von der Identität des Benutzers für Ihre Trimmer Sicherheit</span><span class="sxs-lookup"><span data-stu-id="2f354-150">Retrieving the user identity for your security trimmer</span></span>

<span data-ttu-id="2f354-151">Sie können die Identität des Benutzers abrufen, indem Sie den Zugriff auf den Thread des aktuellen Tilgungsanteile, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="2f354-151">You can retrieve the user's identity by accessing the thread's current principal, as shown in the following code example.</span></span>
  
    
    

```cs

IIdentity userIdentity = System.Threading.Thread.CurrentPrincipal.Identity;
```

<span data-ttu-id="2f354-152">Außerdem müssen Sie die folgende Namespacedirektive einfügen.</span><span class="sxs-lookup"><span data-stu-id="2f354-152">You must also include the following namespace directive.</span></span>
  
    
    



```cs
using System.Security.Principal;
```

<span data-ttu-id="2f354-153">Sie können die Identität des Benutzers auch aus dem **passedUserIdentity**-Parameter der **CheckAccess**-Methode abrufen.</span><span class="sxs-lookup"><span data-stu-id="2f354-153">You can also retrieve the identity of the user from the **CheckAccess** method's **passedUserIdentity** parameter.</span></span>
  
    
    

#### <a name="passing-document-acls-from-the-connector-to-your-security-trimmers"></a><span data-ttu-id="2f354-154">Dokument ACLs aus den Verbinder zu Ihrer Sicherheit Rasentrimmer übergeben</span><span class="sxs-lookup"><span data-stu-id="2f354-154">Passing document ACLs from the connector to your security trimmers</span></span>

<span data-ttu-id="2f354-p109">Ein Verbinder, ist wie der Name sagt, zwischen SharePoint und externen Systems, die externen Daten befindet. Wenn Sie mit den benutzerdefinierten Verbinder arbeiten, können Sie direkt auf den nach der Trimmer ACL-Informationen des Dokuments übergeben, mithilfe der Eigenschaft **docaclmeta** Dokument. Der Verbinder konfiguriert und nach der Rasentrimmer das Format und die Interpretation des Felds besitzen, können Sie kostenlose zur gemeinsamen Nutzung von benutzerdefinierten Daten zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="2f354-p109">A connector, as the name implies, is a communication bridge between SharePoint and the external system that hosts the external data. If you are working with custom connectors, you can pass the document's ACL information directly to the post-trimmer by setting the **docaclmeta** document property. As long as the configured connectors and post-trimmers have the same format and interpretation of the field, you are free to use it to pass custom data.</span></span>
  
    
    
<span data-ttu-id="2f354-p110">Die Zeichenfolgen in **docaclmeta** gespeichert, von der Verbinder werden in den Parameter _documentAcls_ bereitstellen, wenn die **CheckAccess** -Methode der benutzerdefinierten Security Trimmer aufgerufen wird. Das normale Dokument ACLs in der Eigenschaft **docacl** von grundlegende sicherheitskürzung verarbeitet werden und sind für die benutzerdefinierter Security Trimmer nicht sichtbar. Die Eigenschaft **docaclmeta** verfügt ebenso nicht Auswirkung auf grundlegende sicherheitskürzung.</span><span class="sxs-lookup"><span data-stu-id="2f354-p110">The strings stored in **docaclmeta** by the connector will surface in the _documentAcls_ parameter when the **CheckAccess** method of the custom security trimmer is invoked. The regular document ACLs in the **docacl** property are processed by basic security trimming and are not visible to the custom security trimmer. Similarly, the **docaclmeta** property does not have any effect on basic security trimming.</span></span>
  
    
    

#### <a name="post-trimmers-and-their-effect-on-refiner-count-for-security-trimmers"></a><span data-ttu-id="2f354-161">Nach der Rasentrimmer und deren Einfluss auf die Anzahl der Einschränkung für Sicherheit Rasentrimmer</span><span class="sxs-lookup"><span data-stu-id="2f354-161">Post-trimmers and their effect on refiner count for security trimmers</span></span>

<span data-ttu-id="2f354-p111">Bei der Arbeit mit nach der Rasentrimmer ist zu beachten, dass es zwei Arten von Ergebnistabellen gibt: **RelevantResults** und der **RefinementResults**. Nach der Rasentrimmer, die nur auf dem Ergebnis Zugriffe in den **RelevantResults** angewendet werden. Daher können vorhanden sein, dass die Einschränkungen auf dem neuen gekürzte Zugriffe beziehen, und die Anzahl der **RefinementResults** möglicherweise größer als oder gleich der **RelevantResults**. Sie können dieses Verhalten auf zwei Arten beheben:</span><span class="sxs-lookup"><span data-stu-id="2f354-p111">When working with post-trimmers, it is important to notice that there are two types of result tables: **RelevantResults** and the **RefinementResults**. Post-trimmers are applied only to the result hits in the **RelevantResults**. Consequently, there may be refiners related to the post-trimmed hits and the **RefinementResults** count may be larger than or equal to the **RelevantResults**. You can address this behavior in two ways:</span></span>
  
    
    

- <span data-ttu-id="2f354-166">Ausschließen von der vertraulichen Einschränkungen aus der Einschränkungsbereich in Standard-Webpart, damit es werden keine Informationen über die Einschränkungen offengelegt werden.</span><span class="sxs-lookup"><span data-stu-id="2f354-166">Exclude the sensitive refiners from the refinement panel in the default Web Part so that no information is leaked via the refiners.</span></span>
    
  
- <span data-ttu-id="2f354-167">Verwenden Sie ein benutzerdefiniertes Webpart, um die Ergebnisse oder Einschränkungen angezeigt, wenn Sie nach der Rasentrimmer verwenden, damit die **RefinementResults** elegante in Fällen ausgeblendet werden kann, wenn die Anzahl der **RefinementResults** die Anzahl der **RelevantResults** übersteigt.</span><span class="sxs-lookup"><span data-stu-id="2f354-167">Use a custom Web Part to display results or refiners when using post-trimmers so that the **RefinementResults** may be elegantly hidden in cases where the **RefinementResults** count exceeds the **RelevantResults** count.</span></span>
    
  

### <a name="retrieving-individual-configuration-properties-for-your-security-trimmer"></a><span data-ttu-id="2f354-168">Abrufen von Eigenschaften für Ihre Sicherheit Trimmer einzelne Konfiguration</span><span class="sxs-lookup"><span data-stu-id="2f354-168">Retrieving individual configuration properties for your security trimmer</span></span>

<span data-ttu-id="2f354-p112">Sie können eine einzelne Konfigurationseigenschaft zugreifen, mit dem Namen der Eigenschaft, der beim Erstellen der Sicherheit nach der Trimmer registriert wurde angegeben wurde. Mit dem folgende Code wird beispielsweise der Wert für eine Konfigurationseigenschaft mit dem Namen **CheckLimit**abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2f354-p112">You can access an individual configuration property by using the property name that was specified when the security post-trimmer was registered. For example, the following code retrieves the value for a configuration property named **CheckLimit**.</span></span>
  
    
    

```cs
public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{
    if (staticProperties["CheckLimitProperty"] != null)
    {
         intCheckLimit = Convert.ToInt32(staticProperties["CheckLimitProperty"]);
    }
}
```


## <a name="deploying-the-custom-security-trimmer-component"></a><span data-ttu-id="2f354-171">Bereitstellen der benutzerdefinierten Komponente mit dem Security Trimmer</span><span class="sxs-lookup"><span data-stu-id="2f354-171">Deploying the custom security trimmer component</span></span>
<span data-ttu-id="2f354-172"><a name="Deploying_the_trimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="2f354-172"></span></span>

<span data-ttu-id="2f354-p113">Nachdem Sie die benutzerdefinierter Security Trimmer erstellt haben, müssen Sie es zum globalen Assemblycache auf einem beliebigen Server in der Abfrage Rolle bereitstellen. Schritt 2 im  [Vorgehensweise: verwenden ein benutzerdefinierten Security Trimmer für SharePoint Server-Suchergebnisse](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md) beschreibt die für die Bereitstellung von benutzerdefinierten Security Trimmer zum globalen Assemblycache.</span><span class="sxs-lookup"><span data-stu-id="2f354-p113">After you create the custom security trimmer, you must deploy it to the global assembly cache on any server in the Query role. Step 2 in  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md) describes the process for deploying the custom security trimmer to the global assembly cache.</span></span>
  
    
    

## <a name="registering-the-custom-security-trimmer"></a><span data-ttu-id="2f354-175">Registrieren des benutzerdefinierten Security Trimmers</span><span class="sxs-lookup"><span data-stu-id="2f354-175">Registering the custom security trimmer</span></span>
<span data-ttu-id="2f354-176"><a name="Registering_the_trimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="2f354-176"></span></span>

<span data-ttu-id="2f354-177">Für nach der Rasentrimmer müssen Sie eine benutzerdefinierte Security Trimmer Registrierung mit einem bestimmten Suchdienstanwendung und Durchforstungsregel zuordnen; für die Vorabversion Rasentrimmer ist dies optional.</span><span class="sxs-lookup"><span data-stu-id="2f354-177">For post-trimmers, you must associate a custom security trimmer registration with a specific Search service application and crawl rule; for pre-trimmers, this is optional.</span></span>
  
    
    
<span data-ttu-id="2f354-178">Verwenden Sie das Cmdlet **SPEnterpriseSearchSecurityTrimmer**, der die SharePoint-Verwaltungsshell, um ein benutzerdefinierter Security Trimmer zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="2f354-178">You use the **SPEnterpriseSearchSecurityTrimmer** cmdlet of the SharePoint Management Shell to register a custom security trimmer.</span></span>
  
    
    
<span data-ttu-id="2f354-179">Die folgende Tabelle beschreibt die Parameter, die das Cmdlet verwendet.</span><span class="sxs-lookup"><span data-stu-id="2f354-179">The following table describes the parameters that the cmdlet uses.</span></span>
  
    
    

<span data-ttu-id="2f354-180">**Tabelle 1. Parameter, die vom SPEnterpriseSearchSecurityTrimmer-Cmdlet verwendet werden**</span><span class="sxs-lookup"><span data-stu-id="2f354-180">**Table 1. Parameters used by the SPEnterpriseSearchSecurityTrimmer cmdlet**</span></span>


|<span data-ttu-id="2f354-181">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="2f354-181">**Parameter**</span></span>|<span data-ttu-id="2f354-182">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2f354-182">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="2f354-183">_SearchApplication_</span><span class="sxs-lookup"><span data-stu-id="2f354-183">_SearchApplication_</span></span> <br/> |<span data-ttu-id="2f354-p114">Erforderlich ist. Der Name der Suchdienstanwendung, beispielsweise "Suchdienstanwendung".</span><span class="sxs-lookup"><span data-stu-id="2f354-p114">Required. The name of the Search service application, for example "Search Service Application".</span></span>  <br/> |
| <span data-ttu-id="2f354-186">_typeName_</span><span class="sxs-lookup"><span data-stu-id="2f354-186">_TypeName_</span></span> <br/> |<span data-ttu-id="2f354-p115">Erforderlich. Der starke Name der Assembly für den benutzerdefinierten Security Trimmer.</span><span class="sxs-lookup"><span data-stu-id="2f354-p115">Required. The strong name of the custom security trimmer assembly.</span></span>  <br/> |
| <span data-ttu-id="2f354-189">_RulePath_</span><span class="sxs-lookup"><span data-stu-id="2f354-189">_RulePath_</span></span> <br/> |<span data-ttu-id="2f354-p116">Erforderlich für Post-Trimmer; Optional für Prä-Trimmer. Die Durchforstungsregel für den Security Trimmer. </span><span class="sxs-lookup"><span data-stu-id="2f354-p116">Required for post-trimmers; optional for pre-trimmers. The crawl rule for the security trimmer.  </span></span><br/> <span data-ttu-id="2f354-192">**Hinweis:** Es empfiehlt sich, eine Durchforstungsregel pro Inhaltsquelle zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="2f354-192">We recommend using one crawl rule per content source.</span></span>           |
| <span data-ttu-id="2f354-193">_id_</span><span class="sxs-lookup"><span data-stu-id="2f354-193">_id_</span></span> <br/> |<span data-ttu-id="2f354-p117">Erforderlich. Der Bezeichner (ID) des Security Trimmers. Dieser Wert ist eindeutig. Wird ein Security Trimmer mit einem Bezeichner registriert, der bereits für einen anderen Security Trimmer registriert ist, wird die Registrierung des ersten Trimmers mit der Registrierung für den zweiten Trimmer überschrieben.</span><span class="sxs-lookup"><span data-stu-id="2f354-p117">Required. The security trimmer identifier (ID). This value is unique; if a security trimmer is registered with an ID that is already registered for another security trimmer, the registration for the first trimmer is overwritten with the registration for the second trimmer.</span></span>  <br/> |
| <span data-ttu-id="2f354-197">_properties_</span><span class="sxs-lookup"><span data-stu-id="2f354-197">_properties_</span></span> <br/> |<span data-ttu-id="2f354-p118">Optional. Die Name/Wert-Paare, die die Konfigurationseigenschaften angeben. Erforderliches Format:  `Name1~Value1~Name2~Value~???`</span><span class="sxs-lookup"><span data-stu-id="2f354-p118">Optional. The name-value pairs specifying the configuration properties. Must be in the following format:  `Name1~Value1~Name2~Value~???`</span></span> <br/> |
   
<span data-ttu-id="2f354-201">Ein Beispiel für einen einfachen Befehl für die Registrierung ein benutzerdefinierter Security Trimmer und einer Stichprobe, die angibt, die Konfigurationseigenschaften, finden Sie unter  [Vorgehensweise: verwenden ein benutzerdefinierten Security Trimmer für SharePoint Server-Suchergebnisse](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span><span class="sxs-lookup"><span data-stu-id="2f354-201">For an example of a basic command for registering a custom security trimmer and a sample that specifies the configuration properties, see  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2f354-202">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2f354-202">Additional resources</span></span>
<span data-ttu-id="2f354-203"><a name="bk_sectrimmer_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2f354-203"></span></span>


-  [<span data-ttu-id="2f354-204">Vorgehensweise: verwenden ein benutzerdefinierten Security Trimmer für SharePoint Server-Suchergebnisse</span><span class="sxs-lookup"><span data-stu-id="2f354-204">How to: Use a custom security trimmer for SharePoint Server search results</span></span>](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md)
    
  
-  [<span data-ttu-id="2f354-205">ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="2f354-205">ISecurityTrimmerPre</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [<span data-ttu-id="2f354-206">ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="2f354-206">ISecurityTrimmerPost</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  <span data-ttu-id="2f354-207">
  [Übersicht über Business Connectivity Services in SharePoint](http://technet.microsoft.com/de-de/library/ee661740.aspx)</span><span class="sxs-lookup"><span data-stu-id="2f354-207">[Overview of Business Connectivity Services in SharePoint](http://technet.microsoft.com/de-de/library/ee661740.aspx)</span></span>
    
  
