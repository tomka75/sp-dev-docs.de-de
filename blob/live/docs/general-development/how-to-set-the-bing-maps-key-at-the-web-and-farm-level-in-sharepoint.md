---
title: "Festlegen des Bing Maps-Schlüssels auf Web- und Farmebene in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 507ed9de-c349-44b5-b182-e838795dd862
ms.openlocfilehash: bef24775bb6e5bafc64d3d21ef4dcb25ed6c2be3
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint"></a><span data-ttu-id="7b317-102">Festlegen des Bing Maps-Schlüssels auf Web- und Farmebene in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b317-102">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>

![Thema mit Anleitung](../images/mod_icon_howto.png)

<span data-ttu-id="7b317-104">In diesem Artikel erfahren Sie, wie Sie den Bing Maps-Schlüssel programmgesteuert auf der Web- und der Farmebene mithilfe des SharePoint-Clientobjektmodells und von Windows PowerShell festlegen, um die Bing Maps-Funktionen in SharePoint-Listen sowie standortbasierten Web-Apps und mobilen Apps zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7b317-104">Learn how to set the Bing Maps key programmatically at the web and farm level by using the SharePoint client object model and Windows PowerShell, to enable the Bing Maps functionality in SharePoint lists and location-based web and mobile apps.</span></span>

## <a name="prerequisites-for-setting-the-bing-maps-key"></a><span data-ttu-id="7b317-105">Erforderliche Komponenten für die Festlegung des Bing Maps-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="7b317-105">Prerequisites for setting the Bing Maps key</span></span>
<span data-ttu-id="7b317-106"><a name="SP15Bing_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="7b317-106"><a name="SP15Bing_prereq"> </a></span></span>

<span data-ttu-id="7b317-107">Zum Ausführen der Schritte in diesem Beispiel sollten Sie über Folgendes verfügen:</span><span class="sxs-lookup"><span data-stu-id="7b317-107">To follow the steps in this example, you should have the following:</span></span>
  
    
    

- <span data-ttu-id="7b317-108">SharePoint, mit Administratorrechten.</span><span class="sxs-lookup"><span data-stu-id="7b317-108">SharePoint, with administrative privileges.</span></span>
    
  
- <span data-ttu-id="7b317-109">Ein gültiger Bing Maps-Schlüssel, den Sie beim [Bing Maps-Kontocenter](https://www.bingmapsportal.com/) erhalten.</span><span class="sxs-lookup"><span data-stu-id="7b317-109">A valid Bing Maps key, which you can obtain from the  [Bing Maps Account Center](https://www.bingmapsportal.com/).</span></span>
    
    > <span data-ttu-id="7b317-110">**Wichtig:** Bitte beachten Sie, dass Sie für die Einhaltung der für Ihre Nutzung des Bing Maps-Schlüssels anwendbaren Geschäftsbedingungen und alle erforderlichen Veröffentlichungen gegenüber Benutzern Ihrer Anwendung bezüglich an den Bing Daten-Dienst übermittelter Daten verantwortlich sind.</span><span class="sxs-lookup"><span data-stu-id="7b317-110">**Important:** Please note that you are responsible for compliance with terms and conditions applicable to your use of the Bing Maps key, and any necessary disclosures to users of your application regarding data passed to the Bing Maps service.</span></span> 

## <a name="code-example-set-the-bing-maps-key-at-the-farm-or-web-level"></a><span data-ttu-id="7b317-111">Codebeispiel: Einrichten des Bing Maps-Schlüssels auf Farm- oder Webebene.</span><span class="sxs-lookup"><span data-stu-id="7b317-111">Code example: Set the Bing Maps key at the farm or web level</span></span>
<span data-ttu-id="7b317-112"><a name="SP15Setbing_farm"> </a></span><span class="sxs-lookup"><span data-stu-id="7b317-112"><a name="SP15Setbing_farm"> </a></span></span>

<span data-ttu-id="7b317-p101">Ebene der Farm oder Web kann der Bing Maps-Schlüssel festgelegt werden. Um den Bing Maps-Schlüssel auf Farmebene festgelegt, benötigen Sie Administratorrechte auf dem Server; Sie können den Schlüssel dann mithilfe der SharePoint-Verwaltungsshell hinzufügen. Um den Bing Maps-Schlüssel auf der Ebene der Webserver festzulegen, Schreiben Sie eine Konsolenanwendung, die das SharePoint-Clientobjektmodell verwendet.</span><span class="sxs-lookup"><span data-stu-id="7b317-p101">The Bing Maps key can be set at the farm or web level. To set the Bing Maps key at the farm level, you need administrator rights on the server; you can then add the key by using the SharePoint Management Shell. To set the Bing Maps key at the web level, write a console application that uses the SharePoint client object model.</span></span>
  
    
    

> <span data-ttu-id="7b317-116">**Tipp:** Der auf der Webserverebene festgelegte Bing Maps-Schlüssel hat eine höhere Rangfolge als der auf der Farmebene festgelegte Bing Maps-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="7b317-116">**Tip:** The Bing Maps key set at web level has higher precedence order than the Bing Maps key set at farm level.</span></span> 
  
    
    


### <a name="to-set-the-bing-maps-key-at-the-farm-level-using-windows-powershell"></a><span data-ttu-id="7b317-117">Verwenden Sie Windows PowerShell, um den Bing Maps-Schlüssel auf der Farbebene festzulegen.</span><span class="sxs-lookup"><span data-stu-id="7b317-117">To set the Bing Maps key at the farm level using Windows PowerShell</span></span>


1. <span data-ttu-id="7b317-118">Melden Sie sich an den SharePoint-Server als Administrator, und öffnen Sie die SharePoint-Verwaltungsshell.</span><span class="sxs-lookup"><span data-stu-id="7b317-118">Log on to the SharePoint server as an administrator, and open the SharePoint Management Shell.</span></span>
    
  
2. <span data-ttu-id="7b317-119">Führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="7b317-119">Execute the following command:</span></span> 
    
     `Set-SPBingMapsKey -BingKey "<Enter a valid Bing Maps key>"`
    
    <span data-ttu-id="7b317-120">Der Bing Maps-Schlüssel wird nun auf der Farmebene in SharePoint festgelegt.</span><span class="sxs-lookup"><span data-stu-id="7b317-120">The Bing Maps key is now set at the farm level in SharePoint.</span></span> 
    
    > <span data-ttu-id="7b317-121">**Hinweis:** Wenn Sie Windows PowerShell verwenden, kann der Bing Maps-Schlüssel nur auf der Farmebene festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="7b317-121">**Note:** When you use Windows PowerShell, the Bing Maps key can be set only at the farm level.</span></span> <span data-ttu-id="7b317-122">Wenn Sie den Bing Maps-Schlüssel auf der Webebene festlegen möchten, können Sie den Schlüssel, wie im folgenden Abschnitt beschrieben, programmgesteuert festlegen.</span><span class="sxs-lookup"><span data-stu-id="7b317-122">If you want to set the Bing Maps key at the web level, you can set the key programmatically, as shown in the following section.</span></span> 

### <a name="to-set-the-bing-maps-key-at-the-farm-or-web-level-using-the-client-object-model"></a><span data-ttu-id="7b317-123">Einrichten des Bing Maps-Schlüssels auf Farm- oder Webebene mithilfe des Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="7b317-123">To set the Bing Maps key at the farm or web level using the client object model</span></span>


1. <span data-ttu-id="7b317-124">Starten Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b317-124">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="7b317-p103">Wählen Sie auf der Menüleiste **Datei**, **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="7b317-p103">On the menu bar, choose **File**, **New Project**. The **New Project** dialog box opens.</span></span>
    
  
3. <span data-ttu-id="7b317-127">Klicken Sie im Dialogfeld **Neues Projekt** wählen Sie **c#** im Feld **Installierte Vorlagen**, und wählen Sie dann die Vorlage **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="7b317-127">In the **New Project** dialog box, choose **C#** in the **Installed Templates** box, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="7b317-128">Benennen Sie dem Projekt, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b317-128">Give the project a name, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="7b317-p104">Visual Studio erstellt das Projekt. Fügen Sie einen Verweis auf die folgenden Assemblys hinzu, und wählen Sie **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b317-p104">Visual Studio creates the project. Add a reference to the following assemblies, and choose **OK**.</span></span>
    
  - <span data-ttu-id="7b317-131">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="7b317-131">Microsoft.SharePoint.Client.dll</span></span>
    
  
  - <span data-ttu-id="7b317-132">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="7b317-132">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
6. <span data-ttu-id="7b317-133">Fügen Sie eine Richtlinie **using** in der Standard-cs-Datei wie folgt.</span><span class="sxs-lookup"><span data-stu-id="7b317-133">In the default .cs file, add a **using** directive as follows.</span></span>
    
     `using Microsoft.SharePoint.Client;`
    
  
7. <span data-ttu-id="7b317-134">Fügen Sie der Main-Methode in der Datei den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="7b317-134">Add the following code to the Main method in the .cs file.</span></span>
    
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

8. <span data-ttu-id="7b317-135">Ersetzen Sie  <Site Url> und _<Valid Bing Maps Key>_ durch gültige Werte.</span><span class="sxs-lookup"><span data-stu-id="7b317-135">Replace the <Site Url> and  _<Valid Bing Maps Key>_ with valid values.</span></span>
    
  
9. <span data-ttu-id="7b317-136">Legen Sie das Zielframework in den Projekteigenschaften als .NET Framework 4.0, und führen Sie das Beispiel.</span><span class="sxs-lookup"><span data-stu-id="7b317-136">Set the target framework in Project Properties as .NET Framework 4.0, and run the example.</span></span>
    
  
10. <span data-ttu-id="7b317-137">Der Schlüssel sollte jetzt auf der Ebene der Webserver festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="7b317-137">The key should now be set at the web level.</span></span> 
    
  

## <a name="next-steps"></a><span data-ttu-id="7b317-138">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7b317-138">Next steps</span></span>
<span data-ttu-id="7b317-139"><a name="SP15Bing_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="7b317-139"><a name="SP15Bing_nextsteps"> </a></span></span>

<span data-ttu-id="7b317-140">Weitere Informationen zum Arbeiten mit Standort- und Karten-Funktionalität in SharePoint, finden Sie in der folgenden:</span><span class="sxs-lookup"><span data-stu-id="7b317-140">To learn more about working with location and map functionality in SharePoint, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="7b317-141">Vorgehensweise: Hinzufügen einer Geolocation-Spalte einer Liste in SharePoint programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="7b317-141">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7b317-142">Vorgehensweise: erweitern den Geolocation-Feldtyp verwenden clientseitiges Rendering</span><span class="sxs-lookup"><span data-stu-id="7b317-142">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  

