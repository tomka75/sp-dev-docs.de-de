---
title: "Festlegen des Bing Maps-Schlüssels auf Web- und Farmebene in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 507ed9de-c349-44b5-b182-e838795dd862
ms.openlocfilehash: 2414eef9bc3f1781d02c33fbfeaa5824e161b5d9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint"></a>Festlegen des Bing Maps-Schlüssels auf Web- und Farmebene in SharePoint

![Thema mit Anleitung](../images/mod_icon_howto.png)

In diesem Artikel erfahren Sie, wie Sie den Bing Maps-Schlüssel programmgesteuert auf der Web- und der Farmebene mithilfe des SharePoint-Clientobjektmodells und von Windows PowerShell festlegen, um die Bing Maps-Funktionen in SharePoint-Listen sowie standortbasierten Web-Apps und mobilen Apps zu aktivieren.

## <a name="prerequisites-for-setting-the-bing-maps-key"></a>Erforderliche Komponenten für die Festlegung des Bing Maps-Schlüssels
<a name="SP15Bing_prereq"> </a>

Zum Ausführen der Schritte in diesem Beispiel sollten Sie über Folgendes verfügen:
  
    
    

- SharePoint, mit Administratorrechten.
    
  
- Ein gültiger Bing Maps-Schlüssel, den Sie beim [Bing Maps-Kontocenter]((https://www.bingmapsportal.com/)) erhalten.
    
    > **Wichtig:** Bitte beachten Sie, dass Sie für die Einhaltung der für Ihre Nutzung des Bing Maps-Schlüssels anwendbaren Geschäftsbedingungen und alle erforderlichen Veröffentlichungen gegenüber Benutzern Ihrer Anwendung bezüglich an den Bing Daten-Dienst übermittelter Daten verantwortlich sind. 

## <a name="code-example-set-the-bing-maps-key-at-the-farm-or-web-level"></a>Codebeispiel: Einrichten des Bing Maps-Schlüssels auf Farm- oder Webebene.
<a name="SP15Setbing_farm"> </a>

Ebene der Farm oder Web kann der Bing Maps-Schlüssel festgelegt werden. Um den Bing Maps-Schlüssel auf Farmebene festgelegt, benötigen Sie Administratorrechte auf dem Server; Sie können den Schlüssel dann mithilfe der SharePoint-Verwaltungsshell hinzufügen. Um den Bing Maps-Schlüssel auf der Ebene der Webserver festzulegen, Schreiben Sie eine Konsolenanwendung, die das SharePoint-Clientobjektmodell verwendet.
  
    
    

> **Tipp:** Der auf der Webserverebene festgelegte Bing Maps-Schlüssel hat eine höhere Rangfolge als der auf der Farmebene festgelegte Bing Maps-Schlüssel. 
  
    
    


### <a name="to-set-the-bing-maps-key-at-the-farm-level-using-windows-powershell"></a>Verwenden Sie Windows PowerShell, um den Bing Maps-Schlüssel auf der Farbebene festzulegen.


1. Melden Sie sich an den SharePoint-Server als Administrator, und öffnen Sie die SharePoint-Verwaltungsshell.
    
  
2. Führen Sie den folgenden Befehl aus: 
    
     `Set-SPBingMapsKey -BingKey "<Enter a valid Bing Maps key>"`
    
    Der Bing Maps-Schlüssel wird nun auf der Farmebene in SharePoint festgelegt. 
    
    > [!NOTE]
    > Wenn Sie Windows PowerShell verwenden, kann der Bing Maps-Schlüssel nur auf der Farmebene festgelegt werden. Wenn Sie den Bing Maps-Schlüssel auf der Webebene festlegen möchten, können Sie den Schlüssel, wie im folgenden Abschnitt beschrieben, programmgesteuert festlegen. 

### <a name="to-set-the-bing-maps-key-at-the-farm-or-web-level-using-the-client-object-model"></a>Einrichten des Bing Maps-Schlüssels auf Farm- oder Webebene mithilfe des Clientobjektmodells


1. Starten Sie Visual Studio.
    
  
2. Wählen Sie auf der Menüleiste **Datei**, **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird geöffnet.
    
  
3. Klicken Sie im Dialogfeld **Neues Projekt** wählen Sie **c#** im Feld **Installierte Vorlagen**, und wählen Sie dann die Vorlage **Konsolenanwendung**.
    
  
4. Benennen Sie dem Projekt, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
5. Visual Studio erstellt das Projekt. Fügen Sie einen Verweis auf die folgenden Assemblys hinzu, und wählen Sie **OK**.
    
  - Microsoft.SharePoint.Client.dll
    
  
  - Microsoft.SharePoint.Client.Runtime.dll
    
  
6. Fügen Sie eine Richtlinie **using** in der Standard-cs-Datei wie folgt.
    
     `using Microsoft.SharePoint.Client;`
    
  
7. Fügen Sie der Main-Methode in der Datei den folgenden Code.
    
```cs
  
class Program
    {
        static void Main(string[] args)
        {
            SetBingMapsKey();
            Console.WriteLine("Bing Maps set successfully");
        }
     static private void SetBingMapsKey()
        {

            ClientContext context = new ClientContext("<Site Url>");
            Web web = context.Web;
            web.AllProperties["BING_MAPS_KEY"] = "<Valid Bing Maps Key>"
            web.Update();
            context.ExecuteQuery();
        }    
    }

```

8. Ersetzen Sie  <Site Url> und _<Valid Bing Maps Key>_ durch gültige Werte.
    
  
9. Legen Sie das Zielframework in den Projekteigenschaften als .NET Framework 4.0, und führen Sie das Beispiel.
    
  
10. Der Schlüssel sollte jetzt auf der Ebene der Webserver festgelegt werden. 
    
  

## <a name="next-steps"></a>Nächste Schritte
<a name="SP15Bing_nextsteps"> </a>

Weitere Informationen zum Arbeiten mit Standort- und Karten-Funktionalität in SharePoint, finden Sie in der folgenden:
  
    
    

-  [Vorgehensweise: Hinzufügen einer Geolocation-Spalte einer Liste in SharePoint programmgesteuert](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [Vorgehensweise: erweitern den Geolocation-Feldtyp verwenden clientseitiges Rendering](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  

