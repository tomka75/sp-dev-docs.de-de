---
title: "Excel Services-REST-API (Übersicht)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5872f311-e180-4578-ac80-2519c1081951
ms.openlocfilehash: 624336e751c28d7bacce26f88e6d9f7dc570c93c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-rest-api-overview"></a>Excel Services-REST-API (Übersicht)

Die REST-API in Excel Services ist neu in Microsoft SharePoint Server 2010. Mit der REST-API können Sie direkt über eine URL auf Arbeitsmappenteile oder Elemente zugreifen.
  
> [!NOTE]
> Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden. Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph]((http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel))-Endpunkts sind.
  
    
    


REST-Dienste basieren auf zwei Anforderungen:
  
    
    


- Ein zum Suchen von Netzwerkressourcen verwendetes Adressierungsschema
    
  
- Eine Methodik zum Zurückgeben von Darstellungen dieser Ressourcen
    
  
REST-Dienste sind ressourcenorientiert. Mit REST werden Daten in Ressourcen unterteilt, jede Ressource erhält eine URL, und Standardvorgänge werden in den Ressourcen implementiert, die Vorgänge wie das Erstellen, Abrufen, Aktualisieren und Löschen ermöglichen. 

> [!NOTE]
> Weitere Informationen zum Unterschied zwischen REST-Diensten und benutzerdefinierten Webdiensten finden Sie unter [Benutzerdefinierter Dienst oder REST-Dienst]((http://msdn.microsoft.com/de-DE/magazine/dd882522.aspx)). 
  
    
    

Mit einer REST-API für Excel Services können Vorgänge für Excel-Arbeitsmappen mithilfe von im HTTP-Standard angegebenen Vorgängen ausgeführt werden. Dies ermöglicht einen flexiblen, sicheren und einfacheren Mechanismus, um auf Excel Services-Inhalte zuzugreifen und diese zu bearbeiten.Mit den in die REST-API von Excel Services integrierten Ermittlungsmechanismen können Entwickler und Benutzer auch den Inhalt der Arbeitsmappe manuell oder programmgesteuert durchsuchen, indem sie einen  [ATOM]((http://tools.ietf.org/html/rfc4287))-Feed bereitstellen, der Informationen zu den in einer bestimmten Arbeitsmappe vorhandenen Elementen enthält. Beispiele für die Ressourcen, auf die Sie über die REST-API zugreifen können, sind Diagramme, PivotTables und Tabellen.Mit dem ATOM-Feed der REST-API gelangen Sie einfacher zu den gewünschten Daten. Der Feed enthält durchsuchbare Elemente, mit denen jeder Codeabschnitt ermitteln kann, welche Elemente in einer Arbeitsmappe vorhanden sind.Weitere Informationen zum Zugriff auf den REST-Dienst und zu Beispiel-URIs für den REST-Dienst in Excel Services finden Sie unter  [Grundlegende URI-Struktur und Pfad](basic-uri-structure-and-path.md) und [Beispiel-URI für die REST-API in Excel Services](sample-uri-for-excel-services-rest-api.md).
