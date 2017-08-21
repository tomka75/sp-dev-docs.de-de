# <a name="creating-sharepoint-add-ins-that-use-the-cross-domain-library"></a><span data-ttu-id="5892c-101">Erstellen von SharePoint-Add-Ins, die die domänenübergreifende Bibliothek verwenden</span><span class="sxs-lookup"><span data-stu-id="5892c-101">Creating SharePoint Add-ins that use the cross-domain library</span></span>
<span data-ttu-id="5892c-102">Erfahren Sie mehr über die domänenübergreifende JavaScript-Bibliothek in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5892c-102">Learn about the SharePoint cross-domain JavaScript library.</span></span>
 

 <span data-ttu-id="5892c-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="5892c-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="5892c-p102">Es gibt einige Szenarios, in denen weder das Autorisierungssystem mit niedriger Vertrauensebene noch das besonders vertrauenswürdige Autorisierungssystem von einem SharePoint-Add-In verwendet werden kann oder sie keine gute Wahl als einzige Methode sind, mit der das Add-In die Autorisierung für SharePoint-Ressourcen erhält. Beispiele:</span><span class="sxs-lookup"><span data-stu-id="5892c-p102">Learn about the SharePoint cross-domain JavaScript library. There are some scenarios in which neither the low-trust nor the high-trust authorization systems can be used by a SharePoint Add-in, or they are not a good choice as the only means for the add-in to gain authorization to SharePoint resources. Examples:</span></span>
 

- <span data-ttu-id="5892c-108">Die Remotekomponenten des SharePoint-Add-Ins sind nicht lokal vorhanden, eine Unternehmensfirewall blockiert jedoch die Server-zu-Server-Kommunikation zwischen SharePoint und ACS, sodass das System mit niedriger Vertrauensebene nicht verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="5892c-108">The remote components of the SharePoint Add-in are not on-premise, but a corporate firewall blocks server-to-server communication between SharePoint and ACS, thereby preventing the use of the low-trust system.</span></span>
    
 
- <span data-ttu-id="5892c-109">Das SharePoint-Add-In ist als einseitige Webanwendung ausgelegt, die für Datenvorgänge mit SharePoint clientseitiges JavaScript verwendet.</span><span class="sxs-lookup"><span data-stu-id="5892c-109">The SharePoint Add-in is designed as a single-page web application that relies on client-side JavaScript for data operations with SharePoint.</span></span>
    
 
- <span data-ttu-id="5892c-p103">Das SharePoint-Add-In basiert hauptsächlich auf Server-zu-Server-Aufrufen, um auf SharePoint-Daten zuzugreifen (und ist vom System mit niedriger Vertrauensebene oder vom besonders vertrauenswürdigen System autorisiert), es muss jedoch durch einige JavaScript-Aufrufe ergänzt werden. Eine zum Großteil aus Grafiken bestehende Seite kann beispielsweise JavaScript verwenden, um kleinere Aktualisierungen an den angezeigten Daten vorzunehmen, ohne die komplette Seite neu laden zu müssen.</span><span class="sxs-lookup"><span data-stu-id="5892c-p103">The SharePoint Add-in relies mainly on server-to-server calls to access SharePoint data (and is authorized by either the low-trust or high-trust systems), but it needs to be supplemented with some JavaScript calls. For example, a graphics-heavy page can use JavaScript to make minor updates to displayed data without having to reload the entire page.</span></span>
    
 
<span data-ttu-id="5892c-p104">[Aus Sicherheitsgründen](http://msdn.microsoft.com/en-us/library%28d=robot%29/cc709423(d=robot,l=en-us,v=vs.85).aspx) können Browser jedoch kein JavaScript verwenden, der auf einer Domäne gehostet wird, um auf Ressourcen in einer anderen Domäne zuzugreifen, es ist deshalb ein spezielles Verfahren erforderlich, damit Remote-JavaScript auf SharePoint-Ressourcen zugreifen kann. Mit der SharePoint domänenübergreifenden JavaScript-Bibliothek wird die Verwendung des Verfahrens durch Ihre Remotewebanwendung erleichtert.</span><span class="sxs-lookup"><span data-stu-id="5892c-p104">However,  [for security](http://msdn.microsoft.com/en-us/library%28d=robot%29/cc709423(d=robot,l=en-us,v=vs.85).aspx), browsers do not allow JavaScript that is hosted on one domain to access resources on another domain, so a special technique is required to allow the remote JavaScript to access SharePoint resources. The SharePoint cross-domain JavaScript library makes it easy for your remote web application to use the technique.</span></span>
 

 <span data-ttu-id="5892c-p105">**Hinweis** Die domänenübergreifende Bibliothek wird außerdem verwendet, damit in umgekehrter Richtung auf die Daten zugegriffen werden kann; d. h. JavaScript kann auf einer SharePoint-Seite verwendet werden, um auf Daten in einer Remotedomäne zuzugreifen. Weitere Informationen dazu finden Sie unter [Zugreifen auf Remotedaten von einer SharePoint-Seite](#ReverseDirection).</span><span class="sxs-lookup"><span data-stu-id="5892c-p105">**Note** The cross-domain library is also used to allow access to data in the reverse direction; that is, to allow JavaScript on a SharePoint page to access data in a remote domain. See  [Access remote data from a SharePoint page](#ReverseDirection) for more information.</span></span>
 


## <a name="understand-the-architecture-of-the-cross-domain-library"></a><span data-ttu-id="5892c-116">Grundlegendes zur Architektur der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="5892c-116">Understand the architecture of the cross-domain library</span></span>

<span data-ttu-id="5892c-p106">Die SharePoint domänenübergreifende Bibliothek ist in der Datei SP.RequestExecutor.js enthalten, die sich in dem virtuellen Ordner "/_layouts/15/" jeder SharePoint-Website befindet. Die Skripts in dieser Datei umfassen eine sichere, bekannte Methode zur Überwindung der Einschränkung des Browsers beim domänenübergreifenden Skripting: Ein iFrame kann mit der  `window.postMessage()`-Funktion mit der übergeordneten Seite kommunizieren, selbst wenn sich die Seite im iFrame in einer anderen Domäne befindet. Datenanforderungen und -antworten werden also mit Aufrufen an  `postMessage()` über die Domänengrenze hinweg übergeben.</span><span class="sxs-lookup"><span data-stu-id="5892c-p106">The SharePoint cross-domain library is contained in the file SP.RequestExecutor.js which is located in the /_layouts/15/ virtual folder of every SharePoint website. The scripts in this file encapsulate a secure well-known technique for overcoming the browser's restriction on cross-domain scripting: An iFrame can communicate with its parent page by means of the  `window.postMessage()` function, even if the page in the iFrame is in a different domain. So data requests and responses are passed over the domain boundary by using calls to `postMessage()`.</span></span>
 

 

 <span data-ttu-id="5892c-120">**Vorsicht** Die Funktion `postMessage()` funktioniert nur mit Browsern, die HTML 5 unterstützen, d. h. SharePoint-Add-Ins, die die domänenübergreifende Bibliothek verwenden, funktionieren nicht mit älteren Browsern.</span><span class="sxs-lookup"><span data-stu-id="5892c-120">**Caution** The  `postMessage()` function works only on browsers that support HTML 5, so SharePoint Add-ins that use the cross-domain library will not work on older browsers.</span></span>
 

<span data-ttu-id="5892c-p107">Bei SharePoint wird die domänenübergreifende Bibliothek auf einer Seite der Remotewebanwendung geladen, auf der sie einen verborgenen iFrame erstellt, der eine spezielle Proxyseite von der SharePoint-Domäne hostet. Die Proxyseite ist bereits auf jeder SharePoint-Website vorhanden. Die Bibliothek wird zum Erstellen eines JavaScript Object Notation (JSON)-Objekts verwendet, dass alle benötigten Informationen zum Ausführen eines CRUD-Aufrufs an die REST APIs der SharePoint enthält. Das JSON-Objekt wird mit  `postMessage()` an die Proxyseite übergeben. Auf der Proxyseite, auf der die Bibliothek ebenfalls geladen wird, wird das JSON-Objekt als REST-Aufruf an SharePoint analysiert und wiederhergestellt. Da sich die Proxyseite in der SharePoint-Domäne befindet,lässt der Browser den Aufruf zu.</span><span class="sxs-lookup"><span data-stu-id="5892c-p107">For SharePoint, the cross-domain library is loaded on a page of the remote web application where it creates a hidden iFrame that hosts a special proxy page from the SharePoint domain. The proxy page already exists on every SharePoint website. The library is used to create a JavaScript Object Notation (JSON) object which contains all the information needed to make a CRUD call to the REST APIs of SharePoint. The JSON object is passed to the proxy page by using  `postMessage()`. On the proxy page, where the library is also loaded, the JSON object is parsed and reconstructed as a REST call to SharePoint. Since the proxy page is in the SharePoint domain, the browser allows the call.</span></span>
 

 
<span data-ttu-id="5892c-p108">Die Remotekomponenten des SharePoint-Add-Ins benötigen natürlich dennoch autorisierten Zugriff auf die SharePoint-Ressourcen. Dazu gibt es zwei Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="5892c-p108">Of course, the remote components of the SharePoint Add-in still have to have authorized access to the SharePoint resources. There are two ways to do this:</span></span>
 

 

- <span data-ttu-id="5892c-p109">Legen Sie den Prinzipaltyp des Add-Ins auf **RemoteWebApplication** (der Standard für von einem Anbieter gehostete Add-Ins) im Add-In-Manifest fest. Wenn das Add-In bei ACS registriert ist, schließt die Registrierung die Domäne der Remotewebanwendung ein. SharePoint vertraut bei ACS registrierten Domänen, auch wenn es in diesem Szenario keine der Tokenübergabeabläufe verwendet, die Teil des serverseitigen Systems mit niedriger Vertrauensebene sind. Ausführliche Informationen zum Registrieren von Add-Ins finden Sie unter [Registrieren von SharePoint-Add-Ins 2013](register-sharepoint-add-ins-2013).</span><span class="sxs-lookup"><span data-stu-id="5892c-p109">Set the add-in principal type to **RemoteWebApplication** (the default for provider-hosted apps) in the add-in manifest. When the add-in is registered with ACS, the registration includes the domain of the remote web application. SharePoint trusts domains that are registered with ACS, even though it is not, in this scenario, using any of the token passing flows that are part of the server-side low-trust system. For detailed information about registering add-ins, see [Register SharePoint Add-ins 2013](register-sharepoint-add-ins-2013).</span></span> 
    
 
- <span data-ttu-id="5892c-p110">Bei einem von SharePoint gehosteten Add-In können Sie für den Prinzipaltyp des Add-Ins den Standardwert **Internal** übernehmen. Legen Sie anschließend für das **AllowedRemoteHostUrl**-Attribut des **Internal**-Elements die URL der Remotewebanwendung fest, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="5892c-p110">In a SharePoint-hosted add-in, you can leave the add-in principal type set to its default, which is **Internal**. Then set the **AllowedRemoteHostUrl** attribute of the **Internal** element to the URL of the remote web application, as in the following example.</span></span>
    
```
  <AppPrincipal>
  <Internal AllowedRemoteHostUrl="https://example.com/Home.html" />
</AppPrincipal>
```


 <span data-ttu-id="5892c-p111">**Hinweis** Wenn Sie die zweite Option verwenden (einen **Internal**-Add-In-Prinzipal), können Sie nur JavaScript und die domänenübergreifende Bibliothek zum Zugreifen auf SharePoint verwenden. Das SharePoint-Clientobjektmodell ist für **Internal**-SharePoint-Add-Ins gesperrt, Sie können also kein duales Autorisierungssystem nutzen, das die domänenübergreifende Bibliothek und Systeme mit niedriger Vertrauensebene oder besonders vertrauenswürdige Systeme verwendet.</span><span class="sxs-lookup"><span data-stu-id="5892c-p111">**Note** If you use the second option (an **Internal** add-in principal), then you can use only JavaScript and the cross-domain library to access SharePoint. The SharePoint client object model is blocked for **Internal**SharePoint Add-ins, so you cannot have a dual authorization system that uses both the cross-domain library and either the low-trust or high-trust systems.</span></span>
 

<span data-ttu-id="5892c-137">Details zur Verwendung der Bibliothek finden Sie unter [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).</span><span class="sxs-lookup"><span data-stu-id="5892c-137">For details on how to use the library, see  [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).</span></span>
 

 

## <a name="access-remote-data-from-a-sharepoint-page"></a><span data-ttu-id="5892c-138">Zugreifen auf Remotedaten von einer SharePoint-Seite</span><span class="sxs-lookup"><span data-stu-id="5892c-138">Access remote data from a SharePoint page</span></span>
<span data-ttu-id="5892c-139"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="5892c-139"></span></span>

<span data-ttu-id="5892c-p112">Die SharePoint domänenübergreifende Bibliothek kann ebenfalls in die umgekehrte Richtung verwendet werden; d. h., JavaScript auf einer SharePoint-Seite kann die Bibliothek verwenden, um Daten von den Remotekomponenten des Add-Ins abzurufen. Dazu müssen Sie die domänenübergreifende Architektur umkehren: Erstellen Sie eine Proxyseite in der Remotewebanwendung. Die Bibliothek wird von einer SharePoint-Seite aufgerufen, auf der sie einen iFrame erstellt, um die Proxyseite zu hosten. Details zur Verwendung der Bibliothek auf diese Weise finden Sie unter  [Erstellen einer benutzerdefinierten Proxyseite für die domänenübergreifende Bibliothek in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="5892c-p112">The SharePoint cross-domain library can also be used in the reverse direction; that is, JavaScript on a SharePoint page can use the library to get data from the remote components of the add-in. To do this, you reverse the cross-domain architecture: you create a proxy page in the remote web application. The library is called from a SharePoint page where it creates an iFrame to host the proxy page. For details on how to use the library in this way, see  [Create a custom proxy page for the cross-domain library in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013).</span></span>
 

 

## <a name="in-this-section"></a><span data-ttu-id="5892c-144">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="5892c-144">In this section</span></span>
<span data-ttu-id="5892c-145"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="5892c-145"></span></span>


-  [<span data-ttu-id="5892c-146">Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="5892c-146">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library)
    
 
-  [<span data-ttu-id="5892c-147">Arbeiten mit der domänenübergreifenden Bibliothek in verschiedenen Internet Explorer-Sicherheitszonen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="5892c-147">Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins</span></span>](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="5892c-148">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5892c-148">Additional resources</span></span>
<span data-ttu-id="5892c-149"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="5892c-149"></span></span>


-  [<span data-ttu-id="5892c-150">Beheben von domänenübergreifenden Problemen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="5892c-150">Solving cross-domain problems in SharePoint Add-ins</span></span>](http://blogs.msdn.com/b/officeapps/archive/2012/11/29/solving-cross-domain-problems-in-apps-for-sharepoint.aspx)
    
 

