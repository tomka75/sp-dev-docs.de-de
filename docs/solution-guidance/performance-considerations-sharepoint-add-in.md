---
title: Unter Leistungsgesichtspunkten in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 1a7313fd7b8c783268b54ef1ecb06f2e06fb8b44
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="performance-considerations-in-the-sharepoint-add-in-model"></a>Unter Leistungsgesichtspunkten in der SharePoint-add-in-Objektmodell
=========================================================

<a name="summary"></a>Summary
-------

Die Ansätze gelangen Sie sicherstellen, dass eine optimale Leistung mit SharePoint sich im neuen SharePoint-Add-in-Modell gegenüber mit vollständigen vertrauen Code geändert wird. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario die meisten Code Vorgänge stattgefunden im Code SharePoint Server-Side Object Model.

In einem Szenario mit SharePoint-Add-Ins Modell werden SharePoint-Client-Side-Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-API zum Ausführen von Code verwendet.

Der wesentliche Unterschied zwischen den beiden Modellen ist serverseitigen Code im Vergleich zu den clientseitigen Code. Da Code, über den Clients ausgeführt wird, tritt ein im SharePoint-Add-in-Modell, zusätzliche Netzwerkdatenverkehr.  Minimieren der Anzahl der API-Aufruf wird Roundtrips an den SharePoint-Server Steigerung der Leistung von SharePoint-Add-ins und reduziert die Größe der Ressourcen, die von Ihrer SharePoint-Website belegt.

Darüber hinaus im SharePoint-Add-in-Modell kann, weil Code, über den Clients ausgeführt wird es sehr lange dauert, bevor eine Antwort empfangen wird. Zwischenspeichern von Daten für lange ausgeführte Vorgänge (wie die Benutzerprofil-APIs) kann den Reduzieren des Zeitaufwands zum Zurückgeben von Informationen oder Bestätigung erhalten einen Vorgang abgeschlossen ist.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir bieten die folgenden allgemeinen Richtlinien, um eine optimale Leistung mit SharePoint in das neue SharePoint-Add-in-Modell sicherzustellen.

- Clientseitige API-Aufrufe an den SharePoint-Server zu minimieren.
- Verwenden Sie serverseitige und clientseitige Zwischenspeicherungsverfahren zum Speichern von Informationen.
- Es wird nicht empfohlen, ClientIDs, ClientSecrets, Benutzernamen, Kennwörter, Token oder andere vertrauliche Informationen im Zwischenspeicher zu speichern.

<a name="options-to-ensure-optimal-performance-with-sharepoint"></a>Optionen, um sicherzustellen, dass eine optimale Leistung mit SharePoint
-----------------------------------------------------
Sie haben verschiedene Optionen, um sicherzustellen, dass eine optimale Leistung mit SharePoint.

- Verwenden Sie clientseitige Zwischenspeichern 
- Verwenden Sie die serverseitige Zwischenspeichern 

<a name="use-client-side-caching"></a>Verwenden Sie clientseitige Zwischenspeichern 
-----------------------
In diesem Muster werden mithilfe der clientseitigen Zwischenspeicherungsverfahren wie HTML5 LocalStorage und Cookies zum Zwischenspeichern von Daten verwendet. In diesen Speicherorten gespeicherten Informationen wird verwendet, um zu bestimmen, ob die API-Aufrufe an einen SharePoint-Server erforderlich ist.

- Dieses Muster speichert die Daten aus SharePoint-API-Aufrufe in den clientseitigen Cache zurückgegeben.
- Dieses Muster verwendet clientseitigen Code (JavaScript) zum Auswerten von Daten in den clientseitigen Cache gespeichert.
- Cookies sind zum Speichern von 4095 Bytes Daten beschränkt.
    + Cookies müssen einen integrierten Daten Ablauf Mechanismus.
- HTML5 LocalStorage ist auf 5MB der Daten beschränkt.
    - HTML5 LocalStorage ist einen integrierte Daten Ablauf Mechanismus nicht vorhanden. Jedoch möglicherweise solchen ein Ablaufdatum Mechanismus schnell und einfach in JavaScript implementiert werden.
    
        Finden Sie die Funktionen **SetLocalStorageKeyExpiry** und **IsLocalStorageExpired** in der [App.js-JavaScript-Datei](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) in ein Beispiel für die [Performance.LocalStorage (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) .

        **Festlegen von einem Schlüssel Ablauf in LocalStorage:**

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

        **Überprüfen Sie, wenn der Schlüssel Ablauf in LocalStorage abgelaufen ist:**
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

**Wenn sie geeignet ist?**

Wenn müssen Sie die SharePoint ECMA mithilfe der clientseitigen Objektmodell-API (sp.js) verwenden und Auswerten von clientseitigen Daten, um festzustellen, ob die API-Aufrufe getroffen werden müssen.

**Erste Schritte**

Die [Performance.Caching (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) wird gezeigt, wie die Implementierung sowohl LocalStorage und Cookie-basierte mithilfe der clientseitigen Zwischenspeichern im Add-In-Modell und enthält Links zu mehreren Artikeln und Beispiele.

<a name="use-server-side-caching"></a>Verwenden Sie die serverseitige Zwischenspeichern 
-----------------------
In diesem Muster werden serverseitige Zwischenspeicherungsverfahren wie Sitzung und serverseitige Cookie Bewertung Zugriff auf zwischengespeicherte Daten verwendet. In diesen Speicherorten gespeicherten Informationen wird verwendet, um zu bestimmen, ob die API-Aufrufe an einen SharePoint-Server erforderlich ist.

- Dieses Muster speichert die Daten aus SharePoint-API-Aufrufe in serverseitigen Caches zurückgegeben.    
- In diesem Muster verwendet serverseitigen Code für serverseitige Speicherorten gespeicherte Daten ausgewertet werden soll.
    + Serverseitige Speicherorte können sitzungsbasierte Daten beinhalten, serverseitige gespeicherte im RAM oder anderen Drittanbieter-Server-basierten Zwischenspeichern Technologien zwischengespeichert.
- Dieses Muster verwendet serverseitigen Code zum Auswerten von Daten in Cookies gespeichert.
- Cookies sind zum Speichern von 4095 Bytes Daten beschränkt.
    + Cookies müssen einen integrierten Daten Ablauf Mechanismus.
    
    Siehe **CookieCheckSkip** -Methode in der [Customizer.aspx.cs-Klasse](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) in der [OD4B. Configuration.Async (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) sehen wie serverseitigen Code wird verwendet, um Cookies ausgewertet werden soll.

**Implementieren Sie Ihre eigene Layer "Man-in-the-Middle" cache** In manchen Fällen ist es sinnvoll zum Erstellen Ihrer eigenen benutzerdefinierten Cache Ebene. Ein gutes Beispiel ist, wenn Sie Informationen aus dem Profil des Benutzers zurückzugeben müssen. Die Benutzer-Profil-APIs dauern in einigen Fällen eine lange ausführen. Um eine schnelle-Benutzeroberfläche Endbenutzer bereitzustellen, können Sie einen remote Zeitgeberauftrag zum Abfragen des Benutzerprofildiensts und speichern die Informationen in einer Vielzahl von Datenspeichern erstellen. Anschließend können Sie einen Dienst, um Sie auf Abfrage zulassen, die Daten über JavaScript-Aufrufe aus SharePoint-Add-ins speichert, erstellen.  

Azure hat viele verschiedene Speichermechanismen, die verwendet werden können, um Informationen zu speichern, von die viele sehr schnelle, wie die folgende Tabelle und BLOB-Speicher ausführen. Azure ermöglicht Ihnen das Erstellen einer Web-app zum Hosten des Diensts und Sichern aller Daten und den Dienst mit dem gleichen Azure Active Directory als ein Office 365 SharePoint-Mandanten oder sogar eine lokale SharePoint-Umgebung mit DirSync aktiviert.

**Wenn sie geeignet ist?**

- Wenn müssen Sie die SharePoint-verwaltetem Code mithilfe der clientseitigen Objektmodell-API (Microsoft.SharePoint.Client.dll) verwenden und Auswerten von serverseitigen Daten oder Cookies zu ermitteln, ob die API-Aufrufe getroffen werden müssen.
- Wenn langer Vorgänge, wie etwa einer Azure-Web-Auftrag vorhanden sind, die nur einmal pro initiiert sollten versucht angegebenen Zeitrahmen, unabhängig davon, wie oft Initiieren eines Vorgangs ein Benutzer.  
    + Anwenden von benutzerdefinierten OneDrive for Business-Konfigurationen sind ein gutes Beispiel für ein solches Szenario.

**Erste Schritte**

Die [Performance.Caching (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) beschreibt, wie Sie die Implementierung sowohl LocalStorage und Cookie-basierte mithilfe der clientseitigen Zwischenspeichern im Add-In-Modell und enthält Links zu mehreren Artikeln und Beispiele.

<a name="related-links"></a>Verwandte links
=============
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
