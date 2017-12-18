---
title: Verbessern der Leistung in SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: d876d0a14eebdcef940c6d22997f96182b51af28
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="improve-performance-in-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="dc813-102">Verbessern der Leistung in SharePoint gehostet durch Drittanbieter-add-ins</span><span class="sxs-lookup"><span data-stu-id="dc813-102">Improve performance in SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="dc813-103">Verbessern der Leistung von SharePoint gehostet durch Drittanbieter Add-in durch Begrenzen der Anrufe von remote.</span><span class="sxs-lookup"><span data-stu-id="dc813-103">Improve the performance of your SharePoint provider-hosted add-in by limiting remote calls.</span></span>

<span data-ttu-id="dc813-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="dc813-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="dc813-105">Sie können die Leistung von SharePoint gehostet durch Drittanbieter Add-in durch Beschränken der Anzahl und Häufigkeit der remote-Aufrufe von SharePoint verbessern.</span><span class="sxs-lookup"><span data-stu-id="dc813-105">You can improve the performance of your SharePoint provider-hosted add-in by limiting the number and frequency of remote calls to SharePoint.</span></span> <span data-ttu-id="dc813-106">Zu viele Aufrufe an die Hostwebsite beeinträchtigt die Leistung.</span><span class="sxs-lookup"><span data-stu-id="dc813-106">Too many calls to the host site degrades performance.</span></span> <span data-ttu-id="dc813-107">Um die Anzahl der remote-Aufrufe zu begrenzen, können Sie entweder HTTP-Cookies oder HTML5 lokalen Speicher implementieren.</span><span class="sxs-lookup"><span data-stu-id="dc813-107">To limit the number of remote calls, you can implement either HTTP cookies or HTML5 local storage.</span></span>

<span data-ttu-id="dc813-108">Das [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) -Beispiel zeigt, wie HTTP-Cookies und HTML5 lokalen Speicher zum Zwischenspeichern von Daten verwendet.</span><span class="sxs-lookup"><span data-stu-id="dc813-108">The [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) sample shows you how to use HTTP cookies and HTML5 local storage to cache data.</span></span> <span data-ttu-id="dc813-109">Das Beispiel enthält zwei Anbieter-Hosting-add-ins, mit denen Sie im Abschnitt **Über mich** Ihres Benutzerprofils anzeigen, Hinzufügen von Daten und speichern es später.</span><span class="sxs-lookup"><span data-stu-id="dc813-109">The sample includes two provider-hosted add-ins that allow you to view the **About Me** section of your user profile, add data, and save it for later.</span></span> <span data-ttu-id="dc813-110">Das Add-In wird nicht von Benutzerprofilinformationen aktualisiert. Es zwischengespeichert, damit sie später verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="dc813-110">The add-in does not update user profile information; it caches it so that it can be used later.</span></span> <span data-ttu-id="dc813-111">Ein Beispiel http-Cookies verwendet, um die Daten im cache, und die andere HTML5 lokalen Speicher verwendet.</span><span class="sxs-lookup"><span data-stu-id="dc813-111">One sample uses HTTP cookies to cache the data, and the other uses HTML5 local storage.</span></span>

## <a name="use-http-cookies-for-caching"></a><span data-ttu-id="dc813-112">Verwenden Sie zum Zwischenspeichern von HTTP-cookies</span><span class="sxs-lookup"><span data-stu-id="dc813-112">Use HTTP cookies for caching</span></span>

<span data-ttu-id="dc813-113">Die Startseite des Beispiels HTTP-Cookies werden Informationen aus dem Abschnitt **Über mich** Ihres Benutzerprofils in einem Textfeld angezeigt.</span><span class="sxs-lookup"><span data-stu-id="dc813-113">The start page of the HTTP cookie sample displays information from the  **About Me** section of your user profile in a text box.</span></span> <span data-ttu-id="dc813-114">Ein zweites Textfeld erfahren Sie, ob ein neues Cookie erstellt wurde und wann das vorhandene Cookie abläuft.</span><span class="sxs-lookup"><span data-stu-id="dc813-114">A second text box tells you whether a new cookie was created and when the existing cookie will expire.</span></span> <span data-ttu-id="dc813-115">Die Informationen in Cookies darf nicht größer als 4095 Bytes sein.</span><span class="sxs-lookup"><span data-stu-id="dc813-115">The information stored in cookies can't be larger than 4095 bytes.</span></span>

<span data-ttu-id="dc813-116">**Abbildung 1. Daten in der HTTP-Cookie Zwischenspeichern Beispiel gerendert**</span><span class="sxs-lookup"><span data-stu-id="dc813-116">**Figure 1. Data rendered in the HTTP cookie caching sample**</span></span>

![Daten in der HTTP-Cookie Zwischenspeichern Beispiel gerendert](media/improve-performance-in-sharepoint-provider-hosted-add-ins/c9427295-4242-48df-9aa8-392b58d7f4c6.png)

<span data-ttu-id="dc813-118">Die Datei app.js, die sich in den Ordner Scripts des Webprojekts befindet, definiert das Verhalten der Schaltfläche **zur späteren Verwendung speichern** .</span><span class="sxs-lookup"><span data-stu-id="dc813-118">The app.js file, which is located in the Scripts folder of the web project, defines the behavior of the  **Save for later** button.</span></span> <span data-ttu-id="dc813-119">Der Code zuerst überprüft, ob Cookies im Browser aktiviert sind, indem ein TestCookie festlegen.</span><span class="sxs-lookup"><span data-stu-id="dc813-119">The code first verifies that cookies are enabled in the browser by setting a test cookie.</span></span> <span data-ttu-id="dc813-120">Wenn Cookies aktiviert sind, bestimmt den Code an, ob die Benutzerprofilinformationen bereits in einem Cookie gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="dc813-120">If cookies are enabled, the code determines whether the user profile information is already stored in a cookie.</span></span> <span data-ttu-id="dc813-121">Wenn nicht, verwendet er JSON zum Nachschlagen von Informationen **Über mich** , es in einem Cookie gespeichert und anschließend die Informationen im Browser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="dc813-121">If it isn't, it uses JSON to look up the **About Me** information, store it in a cookie, and then display the information in the browser.</span></span>

<span data-ttu-id="dc813-122">In der folgenden Funktion wird das Cookie und das Ablaufdatum.</span><span class="sxs-lookup"><span data-stu-id="dc813-122">The following function sets the cookie and its expiration date.</span></span>

```c#
function setCookie(key, value, expiry, path, domain, secure) {
    var todaysDate = new Date();
    todaysDate.setTime(todaysDate.getTime());

    if (expiry == "") { expiry = "1"; }

    // The following line sets for n number of days. For hours, remove * 24. For minutes, remove * 60 * 24.
    if (expiry) {
        expiry = expiry * 1000 * 60 * 60 * 24;
    }

    var newExpiry = new Date(todaysDate.getTime() + (expiry));

    document.cookie = key + "=" + escape(value) +
        ( ( expiry ) ? ";expires=" + newExpiry : "" ) +
        ( ( path ) ? ";path=" + path : "" ) +
        ( ( domain ) ? ";domain=" + domain : "" ) +
        ((secure) ? ";secure" : "");

    cachingStatus += "\n" + "Creating http cookie for AboutMe data...";
    cachingStatus += "\n" + "Cookie will expire " + newExpiry;
    $('#status').text(cachingStatus);
}

```

## <a name="use-html5-local-storage-for-caching"></a><span data-ttu-id="dc813-123">Verwenden Sie zum Zwischenspeichern von HTML5 lokalen Speicher</span><span class="sxs-lookup"><span data-stu-id="dc813-123">Use HTML5 local storage for caching</span></span>

<span data-ttu-id="dc813-124">Die Startseite des Beispiels lokalen Speicher HTML5 zeigt Informationen im Abschnitt **Über mich** , der die Benutzerprofilinformationen über die zwischengespeicherten Daten.</span><span class="sxs-lookup"><span data-stu-id="dc813-124">The start page of the HTML5 local storage sample displays information from the  **About Me** section of your user profile information about the cached data.</span></span> <span data-ttu-id="dc813-125">Das Textfeld zeigt diese Informationen sowie die Ablaufzeit zwischengespeicherter Informationen (falls vorhanden).</span><span class="sxs-lookup"><span data-stu-id="dc813-125">The text box displays this information as well as the expiration time (if any) of the cached information.</span></span>

<span data-ttu-id="dc813-126">**In Abbildung 2. Daten im HTML 5 lokalen Speicher Zwischenspeichern Beispiel gerendert** die Datei app.js, die sich in den Ordner Scripts des Webprojekts befindet, definiert das Verhalten der Schaltfläche **zur späteren Verwendung speichern** .</span><span class="sxs-lookup"><span data-stu-id="dc813-126">**Figure 2. Data rendered in the HTML 5 local storage caching sample** The app.js file, which is located in the Scripts folder of the web project, defines the behavior of the  **Save for later** button.</span></span> <span data-ttu-id="dc813-127">Das Add-in zuerst überprüft, ob lokaler Speicher mithilfe der folgenden Funktion aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="dc813-127">The add-in first verifies that local storage is enabled by using the following function.</span></span>

```c#
isHtml5StorageSupported = function () {
    try {
        return 'localStorage' in window &amp;&amp; window['localStorage'] !== null;
    } catch (e) {
        return false;
    }
    return false;
}

```

<span data-ttu-id="dc813-128">Wenn lokaler Speicher unterstützt wird, bestimmt die Funktion, ob die Benutzerprofilinformationen es bereits gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="dc813-128">If local storage is supported, the function determines whether the user profile information is already stored there.</span></span> <span data-ttu-id="dc813-129">Falls nicht, verwendet er JSOM nachzuschlagen, die **Über mich** -Informationen lokal speichern und dann die Informationen im Browser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="dc813-129">If it isn't, it uses JSOM to look up the  **About Me** information, to store it locally, and then to display the information in the browser.</span></span> <span data-ttu-id="dc813-130">Mit dem folgende Code werden die Informationen **Über mich** in ein Schlüssel mit dem Namen "AboutMeValue" gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dc813-130">The following code stores the **About Me** information in a key named "aboutMeValue".</span></span>

```c#
var aboutMeValue = personProperties.get_userProfileProperties()['AboutMe'];
    $('#aboutMeText').val(aboutMeValue);

    // Add to local storage.
    localStorage.setItem("aboutMeValue", aboutMeValue);
    setLocalStorageKeyExpiry("aboutMeValue");

    cachingStatus += "\n" + "Populated local storage with profile properties...";
    $('#status').val(cachingStatus);

```

<span data-ttu-id="dc813-131">Die Schaltfläche **Clear Cache** entfernt, Schlüssel, schlägt die Informationen **Über mich** in Ihrem Benutzerprofil und erstellt einen Schlüssel frische lokalen Speicher, um diese Informationen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="dc813-131">The  **Clear the cache** button removes that key, looks up the **About Me** information in your user profile, and creates a fresh local storage key to store that information.</span></span> <span data-ttu-id="dc813-132">Das Add-in nicht Ablaufzeit standardmäßig festgelegt, aber die Datei app.js enthält die folgende Funktion, die Ablaufzeit für die zwischengespeicherten Daten festgelegt.</span><span class="sxs-lookup"><span data-stu-id="dc813-132">The add-in doesn't set an expiration time by default, but the app.js file does contain the following function, which sets an expiration time for the cached data.</span></span>

```c#
function setLocalStorageKeyExpiry(key) {

    // Check for expiration config values.
    var expiryConfig = localStorage.getItem(expiryConfigKey);
    
    // Check for existing expiration stamp.
    var existingStamp = localStorage.getItem(key + expiryKeySuffix);    

    // Override cached setting if a user has entered a value that is different than what is stored.
    if (expiryConfig != null) {
                
        var currentTime = Math.floor((new Date().getTime()) / 1000);
        expiryConfig = parseInt(expiryConfig);
        
        var newStamp = Math.floor((currentTime + expiryConfig));
        localStorage.setItem(key + expiryKeySuffix, newStamp);
        
        // Log status to window.        
        cachingStatus += "\n" + "Setting expiration for the " + key + " key...";
        $('#status').val(cachingStatus);
    }    
    else {
       
    }
}

```

<span data-ttu-id="dc813-133">Bevor Sie für die Informationen aus dem lokalen Speicher-Schlüssel, der Code verwendet die **IsKeyExpired** Funktion, um festzustellen, ob der Schlüssel abläuft.</span><span class="sxs-lookup"><span data-stu-id="dc813-133">Before looking for the information stored in the local storage key, the code uses the  **isKeyExpired** function to determine whether the key is expired.</span></span> <span data-ttu-id="dc813-134">Weitere Informationen finden Sie unter [Anpassen der UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="dc813-134">For more information, see [Customize the UX by using SharePoint provider-hosted add-ins](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dc813-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="dc813-135">See also</span></span>
<span data-ttu-id="dc813-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dc813-136"></span></span>

- [<span data-ttu-id="dc813-137">UX-Komponenten in SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="dc813-137">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="dc813-138">Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins</span><span class="sxs-lookup"><span data-stu-id="dc813-138">Customize the UX by using SharePoint provider-hosted add-ins</span></span>](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md)
    
- [<span data-ttu-id="dc813-139">Branding.UIElementPersonalization</span><span class="sxs-lookup"><span data-stu-id="dc813-139">Branding.UIElementPersonalization</span></span>](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization)
    
- [<span data-ttu-id="dc813-140">Performance.Caching</span><span class="sxs-lookup"><span data-stu-id="dc813-140">Performance.Caching</span></span>](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching)
