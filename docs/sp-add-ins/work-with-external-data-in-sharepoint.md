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
# <a name="work-with-external-data-in-sharepoint"></a>Arbeiten mit externen Daten in SharePoint
In diesem Artikel finden Sie Ressourcen und Anweisungen für das Zugreifen auf und das Bearbeiten von externen Daten mit JavaScript auf Seiten in SharePoint-Add-Ins.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="use-javascript-in-sharepoint-add-ins"></a>Verwenden von JavaScript in SharePoint-Add-Ins
<a name="SP15Workdata_Working"> </a>

In Ihren SharePoint-Add-Ins müssen Sie häufig Daten abrufen und bearbeiten, die über eine Remote-Webanwendung oder einen Dienst einer SharePoint-Seite oder Komponente verfügbar gemacht werden. Da benutzerdefinierter Corde auf den SharePoint-Servern nicht zulässig ist, muss Ihr Add-In zu diesem Zweck JavaScript verwenden. Das Modell für SharePoint-Add-Ins stellt mehrere Optionen für den Zugriff auf Remotedaten und -dienste bereit.
 

 

### <a name="use-the-sharepoint-cross-domain-javascript-library-to-access-external-data"></a>Verwenden Sie die SharePoint domänenübergreifende JavaScript-Bibliothek, um auf externe Daten zuzugreifen

Sie können mit der domänenübergreifenden Bibliothek auf Daten in Ihrer Remote-Webanwendung zugreifen, wenn Sie eine benutzerdefinierte Proxyseite bereitstellen, die in der Remoteinfrastruktur gehostet wird. Als Entwickler sind Sie für die Implementierung der benutzerdefinierten Proxyseite zuständig und Sie müssen mit der benutzerdefinierten Logik umgehen, wie z. B. dem Authentifizierungsmechanismus, falls einer vorhanden ist, zu der Remoteanwendung. Verwenden Sie die domänenübergreifende Bibliothek, wenn die Kommunikation zwischen der Remotedatenquelle und der SharePoint-Seite auf Clientebene erfolgen soll.
 

 
Details zur Verwendung der Bibliothek auf diese Weise finden Sie unter [Erstellen einer benutzerdefinierten Proxyseite für die domänenübergreifende Bibliothek in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).
 

 

 **Hinweis** Die domänenübergreifende SharePoint-Bibliothek kann auch in die andere Richtung verwendet werden; d. h. JavaScript auf Remotewebseiten kann die Bibliothek verwenden, um auf Daten aus SharePoint zuzugreifen. Weitere Informationen zu dieser Verwendung der Bibliothek finden Sie unter [Erstellen von SharePoint-Add-Ins, die die domänenübergreifende Bibliothek verwenden](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).
 


### <a name="use-the-sharepoint-web-proxy-to-access-external-data"></a>Verwenden des SharePoint-Webproxys für den Zugriff auf externe Daten

Sie können den Webproxy verwenden, der in dem JavaScript-Clientobjektmodell für den Zugriff auf Remotedaten verfügbar gemacht wird. (Der Proxy ist auch in dem clientseitigen .NET-Objektmodell (CSOM) verfügbar, Sie können das Objektmodell jedoch nicht in Code verwenden, der auf den SharePoint-Servern ausgeführt wird). Wenn Sie den Webproxy verwenden, senden Sie die ursprüngliche Anforderung an SharePoint. SharePoint fordert wiederum die Daten des angegebenen Endpunkts an und gibt die Antwort zurück an Ihre Seite. Verwenden Sie den Webproxy, wenn die Kommunikation zwischen der Remotedatenquelle und der SharePoint-Seite auf Serverebene erfolgen soll.
 

 
Details zum Verwenden des Proxys finden Sie unter [Abfragen eines Remotediensts mithilfe des Webproxys in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).
 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Workdata_AddRes"> </a>


-  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [Entwickeln von SharePoint-Add-ins](develop-sharepoint-add-ins.md)
    
 

