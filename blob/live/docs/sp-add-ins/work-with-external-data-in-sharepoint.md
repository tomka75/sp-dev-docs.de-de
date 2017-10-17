---
title: Arbeiten mit externen Daten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a3d356feac69517b2d0f0e443460ea984605f8fe
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-external-data-in-sharepoint"></a><span data-ttu-id="0a2f1-102">Arbeiten mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a2f1-102">Work with external data in SharePoint</span></span>
<span data-ttu-id="0a2f1-103">In diesem Artikel finden Sie Ressourcen und Anweisungen für das Zugreifen auf und das Bearbeiten von externen Daten mit JavaScript auf Seiten in SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-103">Find resources and guidance for accessing and manipulating external data with JavaScript on pages in SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="0a2f1-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="use-javascript-in-sharepoint-add-ins"></a><span data-ttu-id="0a2f1-107">Verwenden von JavaScript in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0a2f1-107">Use JavaScript in SharePoint Add-ins</span></span>
<span data-ttu-id="0a2f1-108"><a name="SP15Workdata_Working"> </a></span><span class="sxs-lookup"><span data-stu-id="0a2f1-108"></span></span>

<span data-ttu-id="0a2f1-p102">In Ihren SharePoint-Add-Ins müssen Sie häufig Daten abrufen und bearbeiten, die über eine Remote-Webanwendung oder einen Dienst einer SharePoint-Seite oder Komponente verfügbar gemacht werden. Da benutzerdefinierter Corde auf den SharePoint-Servern nicht zulässig ist, muss Ihr Add-In zu diesem Zweck JavaScript verwenden. Das Modell für SharePoint-Add-Ins stellt mehrere Optionen für den Zugriff auf Remotedaten und -dienste bereit.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-p102">In your SharePoint Add-ins, you will frequently have to retrieve and manipulate data that is exposed by a remote web application or service from within a SharePoint page or component. Because custom code is not allowed on the SharePoint servers, your add-in must use JavaScript for this purpose. The model for SharePoint Add-ins provides multiple options for accessing the remote data and services.</span></span>
 

 

### <a name="use-the-sharepoint-cross-domain-javascript-library-to-access-external-data"></a><span data-ttu-id="0a2f1-112">Verwenden Sie die SharePoint domänenübergreifende JavaScript-Bibliothek, um auf externe Daten zuzugreifen</span><span class="sxs-lookup"><span data-stu-id="0a2f1-112">Use the SharePoint cross-domain JavaScript library to access external data</span></span>

<span data-ttu-id="0a2f1-p103">Sie können mit der domänenübergreifenden Bibliothek auf Daten in Ihrer Remote-Webanwendung zugreifen, wenn Sie eine benutzerdefinierte Proxyseite bereitstellen, die in der Remoteinfrastruktur gehostet wird. Als Entwickler sind Sie für die Implementierung der benutzerdefinierten Proxyseite zuständig und Sie müssen mit der benutzerdefinierten Logik umgehen, wie z. B. dem Authentifizierungsmechanismus, falls einer vorhanden ist, zu der Remoteanwendung. Verwenden Sie die domänenübergreifende Bibliothek, wenn die Kommunikation zwischen der Remotedatenquelle und der SharePoint-Seite auf Clientebene erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-p103">You can use the cross-domain library to access data in your remote web application if you provide a custom proxy page that is hosted in the remote infrastructure. As the developer, you are responsible for implementing the custom proxy page and you have to deal with custom logic such as the authentication mechanism, if there is one, to the remote application. Use the cross-domain library if you want the communication between the remote data source and the SharePoint page to occur at the client level.</span></span>
 

 
<span data-ttu-id="0a2f1-116">Details zur Verwendung der Bibliothek auf diese Weise finden Sie unter [Erstellen einer benutzerdefinierten Proxyseite für die domänenübergreifende Bibliothek in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-116">For details about how to use the library in this way, see  [Create a custom proxy page for the cross-domain library in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span></span>
 

 

 <span data-ttu-id="0a2f1-p104">**Hinweis** Die domänenübergreifende SharePoint-Bibliothek kann auch in die andere Richtung verwendet werden; d. h. JavaScript auf Remotewebseiten kann die Bibliothek verwenden, um auf Daten aus SharePoint zuzugreifen. Weitere Informationen zu dieser Verwendung der Bibliothek finden Sie unter [Erstellen von SharePoint-Add-Ins, die die domänenübergreifende Bibliothek verwenden](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-p104">**Note**  The SharePoint cross-domain library can also be used in the other direction; that is, JavaScript on remote web pages can use it to access data from SharePoint. For more information about this use of the library, see  [Creating SharePoint Add-ins that use the cross-domain library](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).</span></span>
 


### <a name="use-the-sharepoint-web-proxy-to-access-external-data"></a><span data-ttu-id="0a2f1-119">Verwenden des SharePoint-Webproxys für den Zugriff auf externe Daten</span><span class="sxs-lookup"><span data-stu-id="0a2f1-119">Use the SharePoint web proxy to access external data</span></span>

<span data-ttu-id="0a2f1-p105">Sie können den Webproxy verwenden, der in dem JavaScript-Clientobjektmodell für den Zugriff auf Remotedaten verfügbar gemacht wird. (Der Proxy ist auch in dem clientseitigen .NET-Objektmodell (CSOM) verfügbar, Sie können das Objektmodell jedoch nicht in Code verwenden, der auf den SharePoint-Servern ausgeführt wird). Wenn Sie den Webproxy verwenden, senden Sie die ursprüngliche Anforderung an SharePoint. SharePoint fordert wiederum die Daten des angegebenen Endpunkts an und gibt die Antwort zurück an Ihre Seite. Verwenden Sie den Webproxy, wenn die Kommunikation zwischen der Remotedatenquelle und der SharePoint-Seite auf Serverebene erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-p105">You can use the web proxy that is exposed in the JavaScript client object model to access remote data. (The proxy is also available in the .NET client-side object model (CSOM), but you cannot use that object model in code that runs on the SharePoint servers.) When you use the web proxy, you issue the initial request to SharePoint. In turn, SharePoint requests the data to the specified endpoint and forwards the response back to your page. Use the web proxy when you want the communication between the remote data source and the SharePoint page to occur at the server level.</span></span>
 

 
<span data-ttu-id="0a2f1-124">Details zum Verwenden des Proxys finden Sie unter [Abfragen eines Remotediensts mithilfe des Webproxys in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-124">For details about how to use the proxy, see  [Query a remote service using the web proxy in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="0a2f1-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0a2f1-125">Additional resources</span></span>
<span data-ttu-id="0a2f1-126"><a name="SP15Workdata_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="0a2f1-126"></span></span>


-  [<span data-ttu-id="0a2f1-127">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0a2f1-127">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="0a2f1-128">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="0a2f1-128">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 

