---
title: Verbessern der Leistung in SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 495d4900418447ccb1738a0a33020dc9940389d8
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="improve-performance-in-sharepoint-provider-hosted-add-ins"></a>Verbessern der Leistung in SharePoint gehostet durch Drittanbieter-add-ins

Verbessern der Leistung von SharePoint gehostet durch Drittanbieter Add-in durch Begrenzen der Anrufe von remote.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können die Leistung von SharePoint gehostet durch Drittanbieter Add-in durch Beschränken der Anzahl und Häufigkeit der remote-Aufrufe von SharePoint verbessern. Zu viele Aufrufe an die Hostwebsite beeinträchtigt die Leistung. Um die Anzahl der remote-Aufrufe zu begrenzen, können Sie entweder HTTP-Cookies oder HTML5 lokalen Speicher implementieren.

Das [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) -Beispiel zeigt, wie HTTP-Cookies und HTML5 lokalen Speicher zum Zwischenspeichern von Daten verwendet. Das Beispiel enthält zwei Anbieter-Hosting-add-ins, mit denen Sie im Abschnitt **Über mich** Ihres Benutzerprofils anzeigen, Hinzufügen von Daten und speichern es später. Das Add-In wird nicht von Benutzerprofilinformationen aktualisiert. Es zwischengespeichert, damit sie später verwendet werden kann. Ein Beispiel http-Cookies verwendet, um die Daten im cache, und die andere HTML5 lokalen Speicher verwendet.

## <a name="use-http-cookies-for-caching"></a>Verwenden Sie zum Zwischenspeichern von HTTP-cookies

Die Startseite des Beispiels HTTP-Cookies werden Informationen aus dem Abschnitt **Über mich** Ihres Benutzerprofils in einem Textfeld angezeigt. Ein zweites Textfeld erfahren Sie, ob ein neues Cookie erstellt wurde und wann das vorhandene Cookie abläuft. Die Informationen in Cookies darf nicht größer als 4095 Bytes sein.

**Abbildung 1. Daten in der HTTP-Cookie Zwischenspeichern Beispiel gerendert**

![Daten in der HTTP-Cookie Zwischenspeichern Beispiel gerendert](media/improve-performance-in-sharepoint-provider-hosted-add-ins/c9427295-4242-48df-9aa8-392b58d7f4c6.png)

Die Datei app.js, die sich in den Ordner Scripts des Webprojekts befindet, definiert das Verhalten der Schaltfläche **zur späteren Verwendung speichern** . Der Code zuerst überprüft, ob Cookies im Browser aktiviert sind, indem ein TestCookie festlegen. Wenn Cookies aktiviert sind, bestimmt den Code an, ob die Benutzerprofilinformationen bereits in einem Cookie gespeichert ist. Wenn nicht, verwendet er JSON zum Nachschlagen von Informationen **Über mich** , es in einem Cookie gespeichert und anschließend die Informationen im Browser anzuzeigen.

In der folgenden Funktion wird das Cookie und das Ablaufdatum.

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

## <a name="use-html5-local-storage-for-caching"></a>Verwenden Sie zum Zwischenspeichern von HTML5 lokalen Speicher

Die Startseite des Beispiels lokalen Speicher HTML5 zeigt Informationen im Abschnitt **Über mich** , der die Benutzerprofilinformationen über die zwischengespeicherten Daten. Das Textfeld zeigt diese Informationen sowie die Ablaufzeit zwischengespeicherter Informationen (falls vorhanden).

**In Abbildung 2. Daten im HTML 5 lokalen Speicher Zwischenspeichern Beispiel gerendert** die Datei app.js, die sich in den Ordner Scripts des Webprojekts befindet, definiert das Verhalten der Schaltfläche **zur späteren Verwendung speichern** . Das Add-in zuerst überprüft, ob lokaler Speicher mithilfe der folgenden Funktion aktiviert ist.

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

Wenn lokaler Speicher unterstützt wird, bestimmt die Funktion, ob die Benutzerprofilinformationen es bereits gespeichert ist. Falls nicht, verwendet er JSOM nachzuschlagen, die **Über mich** -Informationen lokal speichern und dann die Informationen im Browser anzuzeigen. Mit dem folgende Code werden die Informationen **Über mich** in ein Schlüssel mit dem Namen "AboutMeValue" gespeichert.

```c#
var aboutMeValue = personProperties.get_userProfileProperties()['AboutMe'];
    $('#aboutMeText').val(aboutMeValue);

    // Add to local storage.
    localStorage.setItem("aboutMeValue", aboutMeValue);
    setLocalStorageKeyExpiry("aboutMeValue");

    cachingStatus += "\n" + "Populated local storage with profile properties...";
    $('#status').val(cachingStatus);

```

Die Schaltfläche **Clear Cache** entfernt, Schlüssel, schlägt die Informationen **Über mich** in Ihrem Benutzerprofil und erstellt einen Schlüssel frische lokalen Speicher, um diese Informationen zu speichern. Das Add-in nicht Ablaufzeit standardmäßig festgelegt, aber die Datei app.js enthält die folgende Funktion, die Ablaufzeit für die zwischengespeicherten Daten festgelegt.

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

Bevor Sie für die Informationen aus dem lokalen Speicher-Schlüssel, der Code verwendet die **IsKeyExpired** Funktion, um festzustellen, ob der Schlüssel abläuft. Weitere Informationen finden Sie unter [Anpassen der UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [UX-Komponenten in SharePoint 2013 und SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md)
    
- [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization)
    
- [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching)
