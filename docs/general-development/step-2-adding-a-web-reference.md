---
title: Step 2 Adding a Web Reference
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e9175863-ddb4-4750-847d-d53cb59b33cb
ms.openlocfilehash: ced2da0e9fcbdfdca79175d0219f13dcce4e63d4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-adding-a-web-reference"></a>Step 2: Adding a Web Reference

Webdiensterkennung ist der Prozess, durch den ein Client einen Webdienst findet und die Dienstbeschreibung abruft. In Visual Studio umfasst die Webdiensterkennung das Abfragen einer Website nach einem vordefinierten Algorithmus. Das Ziel des Prozesses ist es, die Dienstbeschreibung zu finden, ein in Web Services Description Language (WSDL) erstelltes XML-Dokument.
  
    
    

In der Dienstbeschreibung werden die verfügbaren Dienste und die Interaktion mit diesen Diensten beschrieben. Ohne Dienstbeschreibung ist keine programmgesteuerte Interaktion mit einem Webdienst möglich. Die Anwendung muss in der Lage sein, mit dem Webdienst zu kommunizieren und ihn zur Laufzeit zu finden. Das geschieht beim Hinzufügen eines Webverweises zu Ihrem Projekt, indem eine Proxyklasse generiert wird, die eine Schnittstelle zu dem Webdienst und eine lokale Darstellung des Webdiensts bereitstellt. Weitere Informationen finden Sie unter "Webverweise und Generieren eines XML-Webdienstproxys" in der Dokumentation zu Microsoft Visual Studio 2005.
  
    
    


## <a name="to-add-a-web-reference"></a>So fügen Sie einen Webverweis hinzu


1. Klicken Sie im Menü **Projekt** auf **Webverweis hinzufügen**.
    
  
2. Geben Sie im Feld **URL** im Dialogfeld **Webverweis hinzufügen** die URL zum Abrufen der Dienstbeschreibung des Excel Web Services ein, z. B. `http://<server>/<customsite>/_vti_bin/excelservice.asmx` oder `http://<server>/_vti_bin/excelservice.asmx`. Klicken Sie dann auf **Los**, um Informationen über den Webdienst abzurufen.
    
    > **Hinweis:** Sie können das Dialogfeld **Webverweis hinzufügen** auch im Bereich **Projektmappen-Explorer** öffnen, indem Sie mit der rechten Maustaste auf **Verweise** klicken und **Webverweis hinzufügen** auswählen. 
3. Benennen Sie im Feld **Webverweis-Name** den Webverweis in toExcelWebService um.
    
  
4. Klicken Sie auf **Verweis hinzufügen**, um einen Webverweis für den Zielwebdienst hinzuzufügen.
    
  
5. Visual Studio lädt die Dienstbeschreibung herunter und generiert eine Proxyklasse, die als Schnittstelle zwischen der Anwendung und Excel Web Services fungiert. 
    
  
6. Weitere Informationen finden Sie unter  [Accessing the SOAP API](accessing-the-soap-api.md).
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="concepts"></a>Konzepte


  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Step 1: Creating the Web Service Client Project](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Step 3: Accessing the Web Service](step-3-accessing-the-web-service.md)
  
    
    
 [Step 4: Building and Testing the Application](step-4-building-and-testing-the-application.md)
  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
