---
title: "BCS-REST-API-Referenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 364fb8d7-87d9-4be7-affd-90caba3cd0c0
ms.openlocfilehash: bf638d39e90dc46df61676625be9ffb11e84f10a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="bcs-rest-api-reference-for-sharepoint"></a>BCS-REST-API-Referenz für SharePoint

  
    
    
![Klassenbibliotheken und -verweise](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
Enthält Referenzinformationen zum Erstellen von URLs zum Aufrufen und Bearbeiten von externen Datenquellen, die mit Business Connectivity Services (BCS) in SharePoint Representational State Transfer (REST).
## <a name="using-restful-apis-to-access-external-data-in-sharepoint"></a>Mithilfe von Rest-APIs Zugriff auf externe Daten in SharePoint
<a name="bkmk_Overview"> </a>

Die REST-Schnittstelle bereitgestellt von SharePoint können Sie die meisten SharePoint Ressourcen durch speziell gestalteten URLs zugreifen. Business Connectivity Services (BCS) verwendet diese Architektur für den Zugriff auf externe Daten.
  
    
    
Sie können auf externe Daten zugreifen, indem Sie URLs auf gleiche Weise erstellen wie beim Zugriff auf Standardlistenelemente.
  
> [!NOTE]
> Zugriff auf Entitäten über BDC direkt wird nicht bereitgestellt. Zum Arbeiten mit externen Daten müssen Sie eine externe Liste erstellen und die REST-URLs für den Zugriff auf Listenelemente in einer externen Liste verwenden. 
  
    
    

Die unterstützten HTTP-Verben für die Arbeit mit externen Listen sind **GET**, **PUT**, **POST** und **DELETE**.
  
    
    
Im Gegensatz zu mit normalen Listen können nicht Sie eine externe Liste mithilfe von REST erstellen. Sie müssen dies tun, durch das Erstellen eines BDC-Modells und einer externen Liste mithilfe von Visual Studio 2012.
  
    
    
Die Informationen in Tabelle 1 veranschaulicht das Erstellen von Rest-URLs und die entsprechenden Client Objektmodellaufrufe und Bearbeiten von Daten aus externen Datenquellen zugreifen.
  
    
    

**In Tabelle 1. Rest-URL-Formate für den Zugriff auf externe Daten**


|**URL**|**Beschreibung**|**HTTP-Methode**|
|:-----|:-----|:-----|
| `http://[sharepointsite]/_api` <br/> |Die Basis des eine REST-Anforderung. Das virtuelle Verzeichnis _api zugeordnet ist, um Aufrufe client.svc, wo das Clientobjektmodell verwendet werden.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/web/title` <br/> |Ruft den Titel des aktuellen Web ab.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists` <br/> |Ruft alle Listen auf einer Website ab  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')` <br/> |Ruft die Metadaten für eine angegebene Liste.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')/items` <br/> |Ruft die Listenelemente in einer angegebenen Liste ab.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')?select=Title` <br/> |Ruft den Titel einer bestimmten Liste ab.  <br/> |GET  <br/> |
   

## <a name="constructing-query-strings-for-filtering-data"></a>Erstellen von Abfragezeichenfolgen zum Filtern von Daten
<a name="bkmk_constructquery"> </a>

Um die zurückgegebene Datenmenge beschränken oder mehr Stellen für den Benutzer relevant die Filteroperationen gefunden in Tabelle 2 können Sie.
  
    
    

**In Tabelle 2. Operatoren zum Filtern von Daten**


|**Operator**|**Beschreibung**|
|:-----|:-----|
|EQ  <br/> |Gleich  <br/> **Hinweis:** Wenn Sie **EQ** zum Filtern verwenden, werden die Filterkriterien an das externe System übergeben, in dem Fall die Filterung auf dem Server.          |
|GT  <br/> |Größer als  <br/> **Hinweis:** Wenn Sie den **GT**-Operator verwenden, wird nur eine clientseitige Filterung ausgeführt. > Beispiel: `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` gibt alle Titel mit einer durchschnittlichen Bewertung über 3 zurück.          |
   
> [!NOTE]
> Zum Abrufen von Spalten, die Teil einer Zuordnung sind, müssen Sie explizit die Spalte in der URL mithilfe von **$select** in der Abfragezeichenfolge mit einbeziehen.
  
    
    


## <a name="see-also"></a>Siehe auch
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [SharePoint: Durchführen grundlegender Datenzugriffsoperationen mit REST in Apps](http://code.msdn.microsoft.com/SharePoint-Perform-335d925b)
    
  
-  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
