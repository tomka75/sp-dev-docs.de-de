---
title: Zugriff auf die SOAP-API
ms.date: 09/25/2017
keywords: soap
f1_keywords: soap
ms.prod: sharepoint
ms.assetid: 36e8e3d5-83ac-4bd3-b556-1af132add3eb
ms.openlocfilehash: 41b6656034d9e67fedca44684444bfb73d667e02
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-the-soap-api"></a>Zugriff auf die SOAP-API

Excel Web Services verwendet SOAP (Simple Object Access-Protokoll) über HTTP und dient als Kommunikationsschnittstelle zwischen Clientprogrammen und Excel Services. Der Webdienst besteht aus Methoden und einer Reihe komplexer Objekte, mit denen Sie auf die gesamten Funktionen von Excel Web Services zugreifen können. Zum Aufrufen dieses Diensts müssen Sie Web Services Description Language (WSDL) von Excel Web Services verwenden.
  
    
    


## <a name="referencing-the-wsdl"></a>Verwenden von WSDL

Für den erfolgreichen Aufruf eines Webdiensts müssen Sie wissen, wie auf den Dienst zugegriffen wird, welche Vorgänge von dem Dienst unterstützt werden, welche Parameter von dem Dienst erwartet werden und was von dem Dienst zurückgegeben wird. WSDL stellt diese Informationen in einem XML-Dokument bereit, das von einem Computer gelesen oder verarbeitet werden kann.
  
    
    
Der Zugriff auf WSDL für den Endpunkt von Excel Web Services erfolgt über  `ExcelServices.asmx?wsdl`. WSDL kann von Development Kits verwendet werden, die SOAP und Webdienste unterstützen, wie z. B. das Microsoft .NET Framework SDK.
  
    
    
Im folgenden Beispiel wird das Format der URL zur WSDL-Datei von Excel Web Services gezeigt:
  
    
    
 `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
Wenn keine benutzerdefinierte Website vorhanden ist, kann temporär die folgende URL verwendet werden:
  
    
    
 `http://<server>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
Es wird empfohlen, eine benutzerdefinierte Website zu erstellen und dann die URL, die die benutzerdefinierte Website enthält, im URL-Format zu verwenden.
  
    
    
In der folgenden Tabelle werden die jeweiligen Elemente in der URL erläutert.
  
    
    


|**URL-Element**|**Beschreibung**|
|:-----|:-----|
| _server_ <br/> |Der Name des Servers, auf dem Microsoft SharePoint Server 2010 bereitgestellt wird.  <br/> |
| _customsite_ <br/> |Eine benutzerdefinierte SharePoint Server 2010-Website, die vom Serveradministrator erstellt wird.  <br/> |
| _<endpointname>.asmx_ <br/> |Der Name des Webdienstendpunkts. Für Excel Web Services ist dies  `ExcelService.asmx`.<br/> |
   
Weitere Informationen über das WSDL-Format finden Sie in der World Wide Web Consortium (W3C) WSDL-Spezifikation unter http://www.w3.org/TR/wsdl.
  
    
    

## <a name="see-also"></a>Siehe auch


#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Step 1: Creating the Web Service Client Project](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Step 2: Adding a Web Reference](step-2-adding-a-web-reference.md)
  
    
    
 [Step 3: Accessing the Web Service](step-3-accessing-the-web-service.md)
  
    
    
 [Step 4: Building and Testing the Application](step-4-building-and-testing-the-application.md)
  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
