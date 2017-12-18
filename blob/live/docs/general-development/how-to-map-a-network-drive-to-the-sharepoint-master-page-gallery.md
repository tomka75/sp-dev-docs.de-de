---
title: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d416f6e-2471-4d03-97ae-4e8d907784c6
ms.openlocfilehash: 2e9cc092f719c419e21500916f5a4a5ffbe17c36
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="map-a-network-drive-to-the-sharepoint-master-page-gallery"></a><span data-ttu-id="b957e-102">Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog</span><span class="sxs-lookup"><span data-stu-id="b957e-102">How to: Map a network drive to the SharePoint Master Page Gallery</span></span>

<span data-ttu-id="b957e-103">In diesem Artikel erfahren Sie, wie Sie dem Gestaltungsvorlagenkatalog ein Netzlaufwerk zuordnen, damit Sie den Entwurfs-Manager zum Hochladen von Designdateien in SharePoint verwenden können.</span><span class="sxs-lookup"><span data-stu-id="b957e-103">Learn how to map a network drive to the Master Page Gallery so that you can use Design Manager to upload design files in SharePoint.</span></span>
<span data-ttu-id="b957e-104">Sie können mithilfe eines beliebigen Webdesigntools oder HTML-Editors ein visuelles Design für Ihre Website erstellen und dieses Design dann mit dem Entwurfs-Manager in SharePoint importieren.</span><span class="sxs-lookup"><span data-stu-id="b957e-104">You can create a visual design for your website by using any web design tool or HTML editor, and then use Design Manager to import the design into SharePoint.</span></span> <span data-ttu-id="b957e-105">Zu diesem Zweck müssen Sie sicherstellen, dass das Designtool seine Dateien im Gestaltungsvorlagenkatalog Ihrer Website speichert; dies ist der Ort, an dem SharePoint die Dateien zu finden erwartet.</span><span class="sxs-lookup"><span data-stu-id="b957e-105">To do this, you have to make sure that the design tool stores its files in your site's Master Page Gallery, which is where SharePoint expects to find the files.</span></span> <span data-ttu-id="b957e-106">Es wird empfohlen, dem Gestaltungsvorlagenkatalog ein Netzlaufwerk zuzuordnen, um das Speichern von Dateien am richtigen Speicherort zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="b957e-106">We recommend that you map a network drive to the Master Page Gallery to make it easier to save files in the correct location.</span></span>
  
    
    

<span data-ttu-id="b957e-107">Ermitteln Sie zunächst den Speicherort des Gestaltungsvorlagenkatalogs.</span><span class="sxs-lookup"><span data-stu-id="b957e-107">First, find the location of the Master Page Gallery.</span></span>
### <a name="to-find-the-location-of-the-master-page-gallery"></a><span data-ttu-id="b957e-108">So suchen Sie den Speicherort des Gestaltungsvorlagenkatalogs</span><span class="sxs-lookup"><span data-stu-id="b957e-108">To find the location of the Master Page Gallery</span></span>


1. <span data-ttu-id="b957e-p102">Starten Sie den Entwurfs-Manager auf der Website, für die Sie ein Design erstellen. (Wählen Sie z. B. im Menü **Einstellungen** die Option **Entwurfs-Manager** aus.)</span><span class="sxs-lookup"><span data-stu-id="b957e-p102">On the site for which you are creating a design, start Design Manager. (For example, on the **Settings** menu, choose **Design Manager**.)</span></span>
    
    > <span data-ttu-id="b957e-111">**Wichtig:** Wenn Ihre Website in SharePoint Online gehostet wird, vergewissern Sie sich, dass Sie beim Anmelden bei der Website mit Ihren Office 365-Anmeldeinformationen das Kontrollkästchen **Angemeldet bleiben** aktivieren.</span><span class="sxs-lookup"><span data-stu-id="b957e-111">**Important:** If your site is hosted in SharePoint Online, when you sign in to the site by using your Office 365 credentials, make sure that you select the **Keep me signed in** check box.</span></span> <span data-ttu-id="b957e-112">Weitere Informationen finden Sie im Artikel zur [Konfiguration und Problembehandlung von zugeordneten Laufwerken, die eine Verbindung mit SharePoint Online-Websites in Office 365 für Unternehmen herstellen](http://support.microsoft.com/kb/2616712).</span><span class="sxs-lookup"><span data-stu-id="b957e-112">For more information, see [How to configure and to troubleshoot mapped network drives that connect to SharePoint Online sites in Office 365 for enterprises](http://support.microsoft.com/kb/2616712).</span></span> 
2. <span data-ttu-id="b957e-113">Wählen Sie in der nummerierten Liste den Eintrag **Designdateien hochladen** aus.</span><span class="sxs-lookup"><span data-stu-id="b957e-113">In the numbered list, select **Upload Design Files**.</span></span>
    
  
3. <span data-ttu-id="b957e-p104">Die Seite "Entwurfs-Manager: Designdateien hochladen" enthält den Speicherort des Gestaltungsvorlagenkatalogs. Der Speicherort endet vermutlich mit  `/_catalogs/masterpage/`. Dies ist der Speicherort, dem Sie ein Netzlaufwerk zuordnen.</span><span class="sxs-lookup"><span data-stu-id="b957e-p104">The Design Manager: Upload Design Files page contains the location of the Master Page Gallery. The location probably ends in  `/_catalogs/masterpage/`. This is the location to which you will map a network drive.</span></span>
    
  
4. <span data-ttu-id="b957e-117">Notieren Sie sich den Speicherort des Gestaltungsvorlagenkatalogs, oder kopieren Sie ihn in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="b957e-117">Make a note of the location of the Master Page Gallery, or copy it to the Clipboard.</span></span>
    
  
<span data-ttu-id="b957e-p105">Ordnen Sie auf dem Computer, auf dem das Designtool oder der HTML-Editor ausgeführt wird, dem soeben kopierten Speicherort ein Netzlaufwerk zu. Das Verfahren zum Zuordnen von Netzwerklaufwerken unterscheidet sich je nach Betriebssystem des Computers:</span><span class="sxs-lookup"><span data-stu-id="b957e-p105">On the computer that runs your design tool or HTML editor, map a network drive to the location that you just copied. The procedure for mapping a network drive differs depending on the computer's operating system:</span></span>
- <span data-ttu-id="b957e-120">Führen Sie für einen Computer unter Windows 8 die Schritte aus, die in der Windows 8-Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows-8/create-shortcut-to-map-network-drive) beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="b957e-120">If the computer is running Windows 8, follow the steps that are described in the Windows 8 version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/de-DE/windows-8/create-shortcut-to-map-network-drive).</span></span>
    
  
- <span data-ttu-id="b957e-121">Führen Sie für einen Computer unter Windows 7 die Schritte aus, die in der Windows 7-Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows7/Create-a-shortcut-to-map-a-network-drive) beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="b957e-121">If the computer is running Windows 7, follow the steps that are described in the Windows 7 version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/de-DE/windows7/Create-a-shortcut-to-map-a-network-drive).</span></span>
    
  
- <span data-ttu-id="b957e-122">Führen Sie für einen Computer unter Windows Vista die Schritte aus, die in der -Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows-vista/Create-a-shortcut-to-map-a-network-drive) beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="b957e-122">If the computer is running Windows Vista, follow the steps that are described in the version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/de-DE/windows-vista/Create-a-shortcut-to-map-a-network-drive).</span></span>
    
  
- <span data-ttu-id="b957e-123">Führen Sie auf einem Computer unter Windows XP die im Artikel  [Verbinden und Trennen eines Netzlaufwerks in Windows XP](http://support.microsoft.com/kb/308582) beschriebenen Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="b957e-123">If the computer is running Windows XP, follow the steps that are described in the article  [How to connect and disconnect a network drive in Windows XP](http://support.microsoft.com/kb/308582).</span></span>
    
  
- <span data-ttu-id="b957e-124">***Wenn auf dem Computer ein anderes Betriebssystem ausgeführt wird, führen Sie die Schritte zum Erstellen einer Verknüpfung mit einem neuen Speicherort für dieses Betriebssystem aus.***</span><span class="sxs-lookup"><span data-stu-id="b957e-124">***If the computer is running another operating system, follow the instructions for creating a shortcut to a new location for that operating system.***</span></span> <span data-ttu-id="b957e-125">Möglicherweise müssen Sie für die Verbindung mit der SharePoint-Website andere Anmeldeinformationen bereitstellen und angeben, dass die Verbindung bei jeder Anmeldung beim Computer erneut hergestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b957e-125">You might have to provide different credentials for connecting to the SharePoint site, and you might have to specify that the connection be re-established every time that you log on to the computer.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="b957e-126">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b957e-126">See also</span></span>
<span data-ttu-id="b957e-127"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b957e-127"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b957e-128">Vorgehensweise: Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b957e-128">How to: Apply a master page to a site in SharePoint</span></span>](how-to-apply-a-master-page-to-a-site-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b957e-129">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b957e-129">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b957e-130">SharePoint-Design-Manager-Gerätekanäle</span><span class="sxs-lookup"><span data-stu-id="b957e-130">SharePoint Design Manager device channels</span></span>](sharepoint-design-manager-device-channels.md)
    
  
-  [<span data-ttu-id="b957e-131">Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager</span><span class="sxs-lookup"><span data-stu-id="b957e-131">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="b957e-132">SharePoint Design Manager - Bilddarstellungen</span><span class="sxs-lookup"><span data-stu-id="b957e-132">SharePoint Design Manager image renditions</span></span>](sharepoint-design-manager-image-renditions.md)
    
  

