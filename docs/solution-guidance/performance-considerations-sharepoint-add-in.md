---
title: Unter Leistungsgesichtspunkten in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 1a7313fd7b8c783268b54ef1ecb06f2e06fb8b44
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="performance-considerations-in-the-sharepoint-add-in-model"></a><span data-ttu-id="824a3-102">Unter Leistungsgesichtspunkten in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="824a3-102">Performance considerations in the SharePoint add-in model</span></span>
=========================================================

<a name="summary"></a><span data-ttu-id="824a3-103">Summary</span><span class="sxs-lookup"><span data-stu-id="824a3-103">Summary</span></span>
-------

<span data-ttu-id="824a3-104">Die Ansätze gelangen Sie sicherstellen, dass eine optimale Leistung mit SharePoint sich im neuen SharePoint-Add-in-Modell gegenüber mit vollständigen vertrauen Code geändert wird.</span><span class="sxs-lookup"><span data-stu-id="824a3-104">The approaches you take to ensure optimal performance with SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="824a3-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario die meisten Code Vorgänge stattgefunden im Code SharePoint Server-Side Object Model.</span><span class="sxs-lookup"><span data-stu-id="824a3-105">In a typical Full Trust Code (FTC) / Farm Solution scenario most code operations took place in the SharePoint Server-side Object Model code.</span></span>

<span data-ttu-id="824a3-106">In einem Szenario mit SharePoint-Add-Ins Modell werden SharePoint-Client-Side-Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-API zum Ausführen von Code verwendet.</span><span class="sxs-lookup"><span data-stu-id="824a3-106">In an SharePoint Add-in model scenario, the SharePoint Client-side Object Model (CSOM) and/or the SharePoint REST API are used to execute code.</span></span>

<span data-ttu-id="824a3-107">Der wesentliche Unterschied zwischen den beiden Modellen ist serverseitigen Code im Vergleich zu den clientseitigen Code.</span><span class="sxs-lookup"><span data-stu-id="824a3-107">The major difference between the two models is server-side code versus client-side code.</span></span> <span data-ttu-id="824a3-108">Da Code, über den Clients ausgeführt wird, tritt ein im SharePoint-Add-in-Modell, zusätzliche Netzwerkdatenverkehr.</span><span class="sxs-lookup"><span data-stu-id="824a3-108">In the SharePoint Add-in model, because code is executed via clients, additional network traffic occurs.</span></span>  <span data-ttu-id="824a3-109">Minimieren der Anzahl der API-Aufruf wird Roundtrips an den SharePoint-Server Steigerung der Leistung von SharePoint-Add-ins und reduziert die Größe der Ressourcen, die von Ihrer SharePoint-Website belegt.</span><span class="sxs-lookup"><span data-stu-id="824a3-109">Minimizing the number of API call round trips to the SharePoint server will increase the performance of your SharePoint Add-ins and reduce the amount of resources consumed by your SharePoint site.</span></span>

<span data-ttu-id="824a3-110">Darüber hinaus im SharePoint-Add-in-Modell kann, weil Code, über den Clients ausgeführt wird es sehr lange dauert, bevor eine Antwort empfangen wird.</span><span class="sxs-lookup"><span data-stu-id="824a3-110">Additionally, in the SharePoint Add-in model, because code is executed via clients there could be long delays before a response is received.</span></span> <span data-ttu-id="824a3-111">Zwischenspeichern von Daten für lange ausgeführte Vorgänge (wie die Benutzerprofil-APIs) kann den Reduzieren des Zeitaufwands zum Zurückgeben von Informationen oder Bestätigung erhalten einen Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="824a3-111">Caching data for long running operations (like the User Profile APIs) can reduce the amount of time it takes to return information or receive confirmation a process is complete.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="824a3-112">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="824a3-112">High-level guidelines</span></span>
---------------------

<span data-ttu-id="824a3-113">In der Regel von einer Ziehpunkt möchten wir bieten die folgenden allgemeinen Richtlinien, um eine optimale Leistung mit SharePoint in das neue SharePoint-Add-in-Modell sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="824a3-113">As a rule of a thumb, we would like to provide the following high-level guidelines to ensure optimal performance with SharePoint in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="824a3-114">Clientseitige API-Aufrufe an den SharePoint-Server zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="824a3-114">Minimize client-side API calls to the SharePoint server.</span></span>
- <span data-ttu-id="824a3-115">Verwenden Sie serverseitige und clientseitige Zwischenspeicherungsverfahren zum Speichern von Informationen.</span><span class="sxs-lookup"><span data-stu-id="824a3-115">Use server-side and client-side caching techniques to store information.</span></span>
- <span data-ttu-id="824a3-116">Es wird nicht empfohlen, ClientIDs, ClientSecrets, Benutzernamen, Kennwörter, Token oder andere vertrauliche Informationen im Zwischenspeicher zu speichern.</span><span class="sxs-lookup"><span data-stu-id="824a3-116">It is not recommended that you store clientIDs, clientSecrets, usernames, passwords, tokens, or other sensitive security information in caches.</span></span>

<a name="options-to-ensure-optimal-performance-with-sharepoint"></a><span data-ttu-id="824a3-117">Optionen, um sicherzustellen, dass eine optimale Leistung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="824a3-117">Options to ensure optimal performance with SharePoint</span></span>
-----------------------------------------------------
<span data-ttu-id="824a3-118">Sie haben verschiedene Optionen, um sicherzustellen, dass eine optimale Leistung mit SharePoint.</span><span class="sxs-lookup"><span data-stu-id="824a3-118">You have a couple of options to ensure optimal performance with SharePoint.</span></span>

- <span data-ttu-id="824a3-119">Verwenden Sie clientseitige Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="824a3-119">Use client-side caching</span></span> 
- <span data-ttu-id="824a3-120">Verwenden Sie die serverseitige Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="824a3-120">Use server-side caching</span></span> 

<a name="use-client-side-caching"></a><span data-ttu-id="824a3-121">Verwenden Sie clientseitige Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="824a3-121">Use client-side caching</span></span> 
-----------------------
<span data-ttu-id="824a3-122">In diesem Muster werden mithilfe der clientseitigen Zwischenspeicherungsverfahren wie HTML5 LocalStorage und Cookies zum Zwischenspeichern von Daten verwendet.</span><span class="sxs-lookup"><span data-stu-id="824a3-122">In this pattern, client-side caching techniques such as HTML5 LocalStorage and cookies are used to cache data.</span></span> <span data-ttu-id="824a3-123">In diesen Speicherorten gespeicherten Informationen wird verwendet, um zu bestimmen, ob die API-Aufrufe an einen SharePoint-Server erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="824a3-123">Information stored in these locations is used to determine if it is necessary to make API calls to a SharePoint server.</span></span>

- <span data-ttu-id="824a3-124">Dieses Muster speichert die Daten aus SharePoint-API-Aufrufe in den clientseitigen Cache zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="824a3-124">This pattern stores data returned from SharePoint API calls in client-side caches.</span></span>
- <span data-ttu-id="824a3-125">Dieses Muster verwendet clientseitigen Code (JavaScript) zum Auswerten von Daten in den clientseitigen Cache gespeichert.</span><span class="sxs-lookup"><span data-stu-id="824a3-125">This pattern uses client-side code (JavaScript) to evaluate data stored in client-side caches.</span></span>
- <span data-ttu-id="824a3-126">Cookies sind zum Speichern von 4095 Bytes Daten beschränkt.</span><span class="sxs-lookup"><span data-stu-id="824a3-126">Cookies are limited to storing 4095 bytes of data.</span></span>
    + <span data-ttu-id="824a3-127">Cookies müssen einen integrierten Daten Ablauf Mechanismus.</span><span class="sxs-lookup"><span data-stu-id="824a3-127">Cookies have a built-in data expiration mechanism.</span></span>
- <span data-ttu-id="824a3-128">HTML5 LocalStorage ist auf 5MB der Daten beschränkt.</span><span class="sxs-lookup"><span data-stu-id="824a3-128">HTML5 LocalStorage is limited to 5MB of data.</span></span>
    - <span data-ttu-id="824a3-129">HTML5 LocalStorage ist einen integrierte Daten Ablauf Mechanismus nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="824a3-129">HTML5 LocalStorage does not have a built-in data expiration mechanism.</span></span> <span data-ttu-id="824a3-130">Jedoch möglicherweise solchen ein Ablaufdatum Mechanismus schnell und einfach in JavaScript implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="824a3-130">However, such an expiration mechanism may be quickly and easily implemented in JavaScript.</span></span>
    
        <span data-ttu-id="824a3-131">Finden Sie die Funktionen **SetLocalStorageKeyExpiry** und **IsLocalStorageExpired** in der [App.js-JavaScript-Datei](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) in ein Beispiel für die [Performance.LocalStorage (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) .</span><span class="sxs-lookup"><span data-stu-id="824a3-131">See the **setLocalStorageKeyExpiry** and **isLocalStorageExpired** functions in the [App.js JavaScript file](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) in the [Performance.LocalStorage (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) for an example.</span></span>

        <span data-ttu-id="824a3-132">**Festlegen von einem Schlüssel Ablauf in LocalStorage:**</span><span class="sxs-lookup"><span data-stu-id="824a3-132">**Setting an expiration key in LocalStorage:**</span></span>

        ```
        function setLocalStorageKeyExpiry(key) 
        {       
            // Check for expiration config values
            var expiryConfig = localStorage.getItem(expiryConfigKey);
            
            // Check for existing expiration stamp
            var existingStamp = localStorage.getItem(key + expiryKeySuffix);    
        
            // Override cached setting if a user has entered a value that is different than what is stored
            if (expiryConfig != null) 
            {                       
                var currentTime = Math.floor((new Date().getTime()) / 1000);
                expiryConfig = parseInt(expiryConfig);
                
                var newStamp = Math.floor((currentTime + expiryConfig));
                localStorage.setItem(key + expiryKeySuffix, newStamp);
                
                // Log status to window        
                cachingStatus += "\n" + "Setting expiration for the " + key + " key...";
                $('#status').val(cachingStatus);
            }    
            else 
            {
               
            }
        }
        ```

        <span data-ttu-id="824a3-133">**Überprüfen Sie, wenn der Schlüssel Ablauf in LocalStorage abgelaufen ist:**</span><span class="sxs-lookup"><span data-stu-id="824a3-133">**Check to see if the expiration key is expired in LocalStorage:**</span></span>
        ```
        function isLocalStorageExpired(key, keyTimeStampName) 
        {
            // Retrieve the example setting for expiration in seconds
            var expiryConfig = localStorage.getItem(expiryConfigKey);
            
            // Retrieve the example setting for expiration in seconds
            var expiryStamp = localStorage.getItem(keyTimeStampName);
        
            if (expiryStamp != null && expiryConfig != null) {
        
                // Retrieve the expiration stamp and compare against specified settings to see if it is expired
                var currentTime = Math.floor((new Date().getTime()) / 1000);
        
                if (currentTime - parseInt(expiryStamp) > parseInt(expiryConfig)) {
                    cachingStatus += "\n" + "The " + key + " key time stamp has expired...";
                    $('#status').val(cachingStatus);
                    return true;
                }
                else 
                {
                    var estimatedSeconds = parseInt(expiryStamp) - currentTime;
                    cachingStatus += "\n" + "The " + key + " time stamp expires in " + estimatedSeconds + " seconds...";
                    $('#status').val(cachingStatus);
                    return false;
                }
            }
            else 
            {
                //default
                return true;
            }
        }
        ```

<span data-ttu-id="824a3-134">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="824a3-134">**When is it a good fit?**</span></span>

<span data-ttu-id="824a3-135">Wenn müssen Sie die SharePoint ECMA mithilfe der clientseitigen Objektmodell-API (sp.js) verwenden und Auswerten von clientseitigen Daten, um festzustellen, ob die API-Aufrufe getroffen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="824a3-135">When you need to use the SharePoint ECMA Client-side Object Model API (sp.js) and evaluate client-side data to determine if the API calls need to be made.</span></span>

<span data-ttu-id="824a3-136">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="824a3-136">**Getting started**</span></span>

<span data-ttu-id="824a3-137">Die [Performance.Caching (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) wird gezeigt, wie die Implementierung sowohl LocalStorage und Cookie-basierte mithilfe der clientseitigen Zwischenspeichern im Add-In-Modell und enthält Links zu mehreren Artikeln und Beispiele.</span><span class="sxs-lookup"><span data-stu-id="824a3-137">The [Performance.Caching (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) demonstrates how to implement both LocalStorage and cookie-based client-side caching in the Add-in model and provides links to several samples and articles.</span></span>

<a name="use-server-side-caching"></a><span data-ttu-id="824a3-138">Verwenden Sie die serverseitige Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="824a3-138">Use server-side caching</span></span> 
-----------------------
<span data-ttu-id="824a3-139">In diesem Muster werden serverseitige Zwischenspeicherungsverfahren wie Sitzung und serverseitige Cookie Bewertung Zugriff auf zwischengespeicherte Daten verwendet.</span><span class="sxs-lookup"><span data-stu-id="824a3-139">In this pattern, server-side caching techniques such as session and server-side cookie evaluation are used to access cached data.</span></span> <span data-ttu-id="824a3-140">In diesen Speicherorten gespeicherten Informationen wird verwendet, um zu bestimmen, ob die API-Aufrufe an einen SharePoint-Server erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="824a3-140">Information stored in these locations is used to determine if it is necessary to make API calls to a SharePoint server.</span></span>

- <span data-ttu-id="824a3-141">Dieses Muster speichert die Daten aus SharePoint-API-Aufrufe in serverseitigen Caches zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="824a3-141">This pattern stores data returned from SharePoint API calls in server-side caches.</span></span>    
- <span data-ttu-id="824a3-142">In diesem Muster verwendet serverseitigen Code für serverseitige Speicherorten gespeicherte Daten ausgewertet werden soll.</span><span class="sxs-lookup"><span data-stu-id="824a3-142">This pattern uses server-side code to evaluate data stored in server-side locations.</span></span>
    + <span data-ttu-id="824a3-143">Serverseitige Speicherorte können sitzungsbasierte Daten beinhalten, serverseitige gespeicherte im RAM oder anderen Drittanbieter-Server-basierten Zwischenspeichern Technologien zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="824a3-143">Server-side locations may include session-based data, server-side caches stored in RAM, or other third-party server-based caching technologies.</span></span>
- <span data-ttu-id="824a3-144">Dieses Muster verwendet serverseitigen Code zum Auswerten von Daten in Cookies gespeichert.</span><span class="sxs-lookup"><span data-stu-id="824a3-144">This pattern uses server-side code to evaluate data stored in cookies.</span></span>
- <span data-ttu-id="824a3-145">Cookies sind zum Speichern von 4095 Bytes Daten beschränkt.</span><span class="sxs-lookup"><span data-stu-id="824a3-145">Cookies are limited to storing 4095 bytes of data.</span></span>
    + <span data-ttu-id="824a3-146">Cookies müssen einen integrierten Daten Ablauf Mechanismus.</span><span class="sxs-lookup"><span data-stu-id="824a3-146">Cookies have a built-in data expiration mechanism.</span></span>
    
    <span data-ttu-id="824a3-147">Siehe **CookieCheckSkip** -Methode in der [Customizer.aspx.cs-Klasse](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) in der [OD4B. Configuration.Async (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) sehen wie serverseitigen Code wird verwendet, um Cookies ausgewertet werden soll.</span><span class="sxs-lookup"><span data-stu-id="824a3-147">See the **CookieCheckSkip** method in the [Customizer.aspx.cs Class](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) in the [OD4B.Configuration.Async (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) to see how server-side code is used to evaluate cookies.</span></span>

<span data-ttu-id="824a3-148">**Implementieren Sie Ihre eigene Layer "Man-in-the-Middle" cache** In manchen Fällen ist es sinnvoll zum Erstellen Ihrer eigenen benutzerdefinierten Cache Ebene.</span><span class="sxs-lookup"><span data-stu-id="824a3-148">**Implementing your own 'man-in-the-middle' cache layer** Sometimes, it makes sense to create your own custom cache layer.</span></span> <span data-ttu-id="824a3-149">Ein gutes Beispiel ist, wenn Sie Informationen aus dem Profil des Benutzers zurückzugeben müssen.</span><span class="sxs-lookup"><span data-stu-id="824a3-149">A good example is when you need to return information from a user's profile.</span></span> <span data-ttu-id="824a3-150">Die Benutzer-Profil-APIs dauern in einigen Fällen eine lange ausführen.</span><span class="sxs-lookup"><span data-stu-id="824a3-150">The User Profile APIs sometimes take a long time to execute.</span></span> <span data-ttu-id="824a3-151">Um eine schnelle-Benutzeroberfläche Endbenutzer bereitzustellen, können Sie einen remote Zeitgeberauftrag zum Abfragen des Benutzerprofildiensts und speichern die Informationen in einer Vielzahl von Datenspeichern erstellen.</span><span class="sxs-lookup"><span data-stu-id="824a3-151">To provide end users with a fast user interface experience, you can create a remote timer job to query the user profile service and store the information in a variety of data stores.</span></span> <span data-ttu-id="824a3-152">Anschließend können Sie einen Dienst, um Sie auf Abfrage zulassen, die Daten über JavaScript-Aufrufe aus SharePoint-Add-ins speichert, erstellen.</span><span class="sxs-lookup"><span data-stu-id="824a3-152">Then, you can create a service to allow you to query the data stores via JavaScript calls from SharePoint Add-ins.</span></span>  

<span data-ttu-id="824a3-153">Azure hat viele verschiedene Speichermechanismen, die verwendet werden können, um Informationen zu speichern, von die viele sehr schnelle, wie die folgende Tabelle und BLOB-Speicher ausführen.</span><span class="sxs-lookup"><span data-stu-id="824a3-153">Azure has many different storage mechanisms that may be used to store information, many of which perform extremely fast, like Table storage and Blob storage.</span></span> <span data-ttu-id="824a3-154">Azure ermöglicht Ihnen das Erstellen einer Web-app zum Hosten des Diensts und Sichern aller Daten und den Dienst mit dem gleichen Azure Active Directory als ein Office 365 SharePoint-Mandanten oder sogar eine lokale SharePoint-Umgebung mit DirSync aktiviert.</span><span class="sxs-lookup"><span data-stu-id="824a3-154">Azure also allows you to create a web app to host the service and secure all of the data and the service with the same Azure Active Directory as an Office 365 SharePoint tenancy, or even an on-premises SharePoint environment with DirSync enabled.</span></span>

<span data-ttu-id="824a3-155">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="824a3-155">**When is it a good fit?**</span></span>

- <span data-ttu-id="824a3-156">Wenn müssen Sie die SharePoint-verwaltetem Code mithilfe der clientseitigen Objektmodell-API (Microsoft.SharePoint.Client.dll) verwenden und Auswerten von serverseitigen Daten oder Cookies zu ermitteln, ob die API-Aufrufe getroffen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="824a3-156">When you need to use the SharePoint Managed Code Client-side Object Model API (Microsoft.SharePoint.Client.dll) and evaluate server-side data or cookies to determine if the API calls need to be made.</span></span>
- <span data-ttu-id="824a3-157">Wenn langer Vorgänge, wie etwa einer Azure-Web-Auftrag vorhanden sind, die nur einmal pro initiiert sollten versucht angegebenen Zeitrahmen, unabhängig davon, wie oft Initiieren eines Vorgangs ein Benutzer.</span><span class="sxs-lookup"><span data-stu-id="824a3-157">When you have long-running operations, such as an Azure Web Job, that should only be initiated once per given time frame, no matter how many times a user tries to initiate an operation.</span></span>  
    + <span data-ttu-id="824a3-158">Anwenden von benutzerdefinierten OneDrive for Business-Konfigurationen sind ein gutes Beispiel für ein solches Szenario.</span><span class="sxs-lookup"><span data-stu-id="824a3-158">Applying customized OneDrive for Business configurations are a good example of such a scenario.</span></span>

<span data-ttu-id="824a3-159">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="824a3-159">**Getting started**</span></span>

<span data-ttu-id="824a3-160">Die [Performance.Caching (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) beschreibt, wie Sie die Implementierung sowohl LocalStorage und Cookie-basierte mithilfe der clientseitigen Zwischenspeichern im Add-In-Modell und enthält Links zu mehreren Artikeln und Beispiele.</span><span class="sxs-lookup"><span data-stu-id="824a3-160">The [Performance.Caching (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) describes how to implement both LocalStorage and cookie-based client-side caching in the Add-in model and provides links to several samples and articles.</span></span>

<a name="related-links"></a><span data-ttu-id="824a3-161">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="824a3-161">Related links</span></span>
=============
- <span data-ttu-id="824a3-162">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="824a3-162">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="824a3-163">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="824a3-163">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="824a3-164">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="824a3-164">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="824a3-165">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="824a3-165">Related PnP samples</span></span>
===================

- <span data-ttu-id="824a3-166">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="824a3-166">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="824a3-167">Gilt für</span><span class="sxs-lookup"><span data-stu-id="824a3-167">Applies to</span></span>
==========
- <span data-ttu-id="824a3-168">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="824a3-168">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="824a3-169">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="824a3-169">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="824a3-170">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="824a3-170">SharePoint 2013 on-premises</span></span>
