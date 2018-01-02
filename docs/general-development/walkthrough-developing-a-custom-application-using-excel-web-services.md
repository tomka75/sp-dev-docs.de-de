---
title: Walkthrough Developing a Custom Application Using Excel Web Services
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f9bf243-281a-4d70-917e-9eaf0b867631
ms.openlocfilehash: 57f6eb6d15510b1147b82fdce53436dded5fa47a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="walkthrough-developing-a-custom-application-using-excel-web-services"></a>Walkthrough: Developing a Custom Application Using Excel Web Services

Die exemplarische Vorgehensweise in diesem Abschnitt beschreibt das Verfahren für den Zugriff auf die Excel Web Services von einer mit Microsoft Visual C# erstellten Anwendung.
  
    
    

Diese exemplarische Vorgehensweise vermittelt Folgendes:
- Erstellen einer Clientanwendung mithilfe der Visual Studio-Projektvorlage für Konsolenanwendungen.
    
  
- Hinzufügen eines Webverweises für die Excel Web Services.
    
  
- Schreiben von Code für den Zugriff auf den Webdienst. Sie erfahren, wie eine Arbeitsmappe geöffnet wird, die Sitzungs-ID abgerufen wird, die Standardanmeldeinformationen übergeben werden, Webdienst-Versionsinformationen abgerufen werden, das Bereichskoordinatenobjekt definiert wird, der Bereich, der das Bereichskoordinatenobjekt verwendet, abgerufen wird, die Arbeitsmappe geschlossen wird und die SOAP-Ausnahme aufgefangen wird.
    
  
- Testen und Ausführen der Konsolenanwendung im Debugmodus.
    
  
Eine Clientkonsolenanwendung ist nur eine Möglichkeit, um auf den Webdienst zuzugreifen. Ein gängigeres Verfahren ist die Verwendung von Serveranwendungen wie Microsoft ASP.NET-Anwendungen. Im Rahmen dieser exemplarischen Vorgehensweise wird der Einfachheit halber eine Konsolenanwendung als Beispiel verwendet, um die Aspekte der Excel Web Services-API zu beleuchten.
## <a name="prerequisites"></a>Voraussetzungen

In order to complete this walkthrough, you will need: 
  
    
    

- Microsoft SharePoint Server 2010.
    
  
- Visual Studio oder ein vergleichbares mit Microsoft .NET Framework kompatibles Entwicklungstool.
    
  
- Ausreichende Berechtigungen (mindestens die Berechtigung "Anzeigen"), um auf die Excel Web Services auf dem Computer zugreifen zu können, auf dem sich SharePoint Server 2010 befindet. 
    
    > [!NOTE] 
    > Weitere Informationen zu Arbeitsmappenberechtigungen finden Sie weiter unten im Abschnitt „Arbeitsmappenberechtigungen“. 

- Eine auf einem lokalen Laufwerk oder in einer lokalen SharePoint-Dokumentbibliothek installierte Beispiel-Arbeitsmappe. 
    
  
- Einen vertrauenswürdigen Speicherort zum Speichern von Arbeitsmappen, auf die Sie mithilfe der Excel Web Services zugreifen möchten. Wenn die Arbeitsmappen nicht an einem vertrauenswürdigen Speicherort gespeichert sind, führen die Excel Web Services-Aufrufe zum Öffnen der Arbeitsmappe zu einem Fehler. Bei dieser exemplarischen Vorgehensweise wird davon ausgegangen, dass sich die Arbeitsmappe auf dem lokalen Computer befindet. 
    
    > [!NOTE] 
    > Informationen zum Festlegen eines vertrauenswürdigen Speicherorts finden Sie unter [Gewusst wie: Festlegen eines vertrauenswürdigen Speicherorts](how-to-trust-a-location.md) und unter [Gewusst wie: Festlegen von vertrauenswürdigen Speicherorten für Arbeitsmappen mithilfe von Skripts](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx). 

- Erstellen der Arbeitsmappe mithilfe von Excel.
    
  
- Sie müssen die Arbeitsmappe als XLSX- oder XLSB-Datei speichern.
    
  
Die Arbeitsmappe, die in diesem Beispiel verwendet wird, trägt den Namen "Sheet1". Das Arbeitsblatt enthält 11 Spalten und 19 Zeilen. Jede Zelle von A1 bis K19 enthält einen numerischen Wert, z. B. 4245,955, 6960,673 usw.
  
    
    

## <a name="workbook-permissions"></a>Arbeitsmappenberechtigungen


- Zum Abrufen der gesamten Arbeitsmappe (z. B. durch Aufrufen der **GetWorkbook**-Methode) benötigt der Aufrufer die Berechtigung "Öffnen" für die Arbeitsmappe.
    
  
- Zum Aufrufen der **GetApiVersion**-Methode sind keine Berechtigungen erforderlich.
    
  
- Für die übrigen Excel Web Services-Methoden benötigt der Aufrufer die Berechtigung "Anzeigen" (in Microsoft SharePoint Foundation) oder "Lesen" (auf einer Dateifreigabe ) für die Arbeitsmappe.
    
    > [!NOTE] 
    > Weitere Informationen zum Festlegen von Berechtigungen finden Sie in der Dokumentation zu SharePoint Foundation. 

## <a name="see-also"></a>Siehe auch

- [Zugriff auf die SOAP-API](accessing-the-soap-api.md)
- [Excel Services Alerts](excel-services-alerts.md)
- [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
- [Loop-Back von SOAP-Aufrufen und Direct Linking](loop-back-soap-calls-and-direct-linking.md)
- [Schritt 1: Erstellen des Webdienst-Client-Projekts](step-1-creating-the-web-service-client-project.md)
- [Step 2: Adding a Web Reference](step-2-adding-a-web-reference.md)
- [Step 3: Accessing the Web Service](step-3-accessing-the-web-service.md)
- [Step 4: Building and Testing the Application](step-4-building-and-testing-the-application.md)
