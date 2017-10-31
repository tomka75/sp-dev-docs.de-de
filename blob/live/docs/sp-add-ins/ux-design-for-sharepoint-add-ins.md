---
title: "UX-Design für SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1608492d2208b8986113c9103a1cae666b7e3911
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="ux-design-for-sharepoint-add-ins"></a><span data-ttu-id="f34ff-102">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-102">UX design for SharePoint Add-ins</span></span>
<span data-ttu-id="f34ff-103">Erfahren Sie mehr über die UX-Optionen (User Experience), die Ihnen beim Erstellen von Add-Ins in SharePoint zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="f34ff-103">Learn about the user experience (UX) options that you have when you build add-ins in SharePoint.</span></span>
 

 <span data-ttu-id="f34ff-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="f34ff-p102">Als Entwickler sollten Sie der User Experience (UX), d. h. dem umfassenden Nutzungserlebnis des Benutzers, einen hohen Stellenwert beimessen, wenn Sie Add-Ins erstellen. Das Modell für SharePoint-Add-Ins bietet zahlreiche UX-Komponenten und Mechanismen, die Sie dabei unterstützen, ein optimales Nutzungserlebnis zu bieten. Die User Experience im Add-In-Modell ist außerdem so flexibel, dass Sie die Verfahren und Plattformen verwenden können, die sich am besten an die Anforderungen der Endbenutzer anpassen.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p102">As a developer, you should always give high priority to the user experience (UX) when you are creating add-ins. The model for SharePoint Add-ins offers many UX components and mechanisms that help you build a great user experience. The user experience in the add-in model is also flexible enough to let you use the techniques and platforms that best adapt to the needs of end users.</span></span>
 

## <a name="high-level-overview-of-add-in-ux-in-sharepoint"></a><span data-ttu-id="f34ff-109">Allgemeine Übersicht über Add-In-UX in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f34ff-109">High-level overview of add-in UX in SharePoint</span></span>
<span data-ttu-id="f34ff-110"><a name="SP15_UXdesignapps_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="f34ff-110"><a name="SP15_UXdesignapps_overview"> </a></span></span>

<span data-ttu-id="f34ff-p103">Als Add-In-Entwickler müssen Sie die Architektur Ihres Add-Ins kennen. Nachdem Sie bestimmt haben, wie Ihr Add-In in Remote- und SharePoint-Plattformen verteilt werden soll, können Sie unter den verfügbaren Alternativen zum Erstellen Ihrer Add-In-UX eine Wahl treffen. Sie können sich folgende Fragen stellen:</span><span class="sxs-lookup"><span data-stu-id="f34ff-p103">As the add-in developer, you have to know the architecture of your add-in. After you determine how your add-in will be distributed in remote and SharePoint platforms, you can decide among the available alternatives for building your add-in UX. You might ask yourself the following questions:</span></span>
 

 

- <span data-ttu-id="f34ff-114">Was kann ich verwenden, wenn ich ein in der Cloud gehostetes Add-In erstelle?</span><span class="sxs-lookup"><span data-stu-id="f34ff-114">What can I use if I am creating a cloud-hosted add-in?</span></span>
    
 
- <span data-ttu-id="f34ff-p104">Was kann ich verwenden, wenn ich ein in SharePoint gehostetes Add-In erstelle? Weitere Informationen finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p104">What can I use if I am creating a SharePoint-hosted add-in? For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span></span>
    
 
- <span data-ttu-id="f34ff-p105">Wie kann ich meine UX mit dem Hostweb verbinden? Weitere Informationen finden Sie unter [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p105">How can I connect my UX to the host web? For more information, see  [Host webs, add-in webs, and SharePoint components in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span></span>
    
 
<span data-ttu-id="f34ff-119">Das folgende Diagramm zeigt die wichtigsten Szenarios und Optionen, die beim Entwerfen der Add-In-UX berücksichtigt werden sollten.</span><span class="sxs-lookup"><span data-stu-id="f34ff-119">The following diagram shows the main scenarios and options to consider when you are designing your add-in UX.</span></span>
 

 

<span data-ttu-id="f34ff-120">**Abbildung 1. Wichtigste Szenarios und Optionen für die Add-In-UX**</span><span class="sxs-lookup"><span data-stu-id="f34ff-120">**Figure 1. Add-in UX main scenarios and options**</span></span>

 

 
![App-UX-Hauptszenarien](../images/AppUX_landscape.png)
 
<span data-ttu-id="f34ff-p106">Bei der Wahl Ihres Entwurfs sollten Sie grundsätzlich überlegen, welche Teile Ihres Add-Ins in SharePoint gehostet werden und welche nicht. Sie sollten außerdem überlegen, wie Ihr Add-In mit der Hostwebsite interagiert.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p106">In choosing your design, you should fundamentally consider which parts of your add-in are hosted in SharePoint and which are not. You should also consider how your add-in interacts with the host web.</span></span>
 

 

## <a name="add-in-ux-scenarios-in-cloud-hosted-add-ins"></a><span data-ttu-id="f34ff-124">Add-In-UX-Szenarios für in der Cloud gehostete Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-124">Add-in UX scenarios in cloud-hosted add-ins</span></span>
<span data-ttu-id="f34ff-125"><a name="SP15_UXdesignapps_devhosted"> </a></span><span class="sxs-lookup"><span data-stu-id="f34ff-125"><a name="SP15_UXdesignapps_devhosted"> </a></span></span>

<span data-ttu-id="f34ff-p107">Angenommen, Sie bestimmen, dass ein Teil Ihrer User Experience nicht in SharePoint gehostet werden soll. Bei diesen Szenarien wird davon ausgegangen, dass Ihre Endbenutzer zwischen einer SharePoint-Website und dem in der Cloud gehosteten Add-In hin und her wechseln. Sie können die auf der Plattform verfügbaren Verfahren und Tools verwenden, jedoch bietet SharePoint ebenfalls Ressourcen, damit Sie eine nahtlose Erfahrung für Ihre Benutzer entwerfen können.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p107">Suppose that you determine that some of your user experience is not hosted in SharePoint. In these scenarios, it is expected that your end users go back and forth between a SharePoint website and the cloud-hosted add-in. You can use the techniques and tools in the platform, but SharePoint also provides resources to help you design a smooth experience for users.</span></span>
 

 
<span data-ttu-id="f34ff-129">Die folgenden UX-Ressourcen sind für in der Cloud gehostete Add-Ins in SharePoint verfügbar:</span><span class="sxs-lookup"><span data-stu-id="f34ff-129">The following UX resources are available for cloud-hosted add-ins in SharePoint:</span></span>
 

 

-  <span data-ttu-id="f34ff-p108">**Chromsteuerelement:** DasChromsteuerelement ermöglicht Ihnen, den Navigationsheader einer bestimmten SharePoint-Website in Ihrem Add-In zu verwenden, ohne eine Serverbibliothek registrieren zu müssen oder eine bestimmte Technologie bzw. ein bestimmtes Tool zu verwenden. Um diese Funktion zu nutzen, müssen Sie eine SharePoint-JavaScript-Bibliothek durch standardmäßige <script>-Tags registrieren. Sie können einen Platzhalter bereitstellen, indem Sie ein HTML- **div**-Element verwenden und das Steuerelement mithilfe der verfügbaren Optionen weiter anpassen. Das Steuerelement erhält sein Aussehen durch die angegebene SharePoint-Website. Weitere Informationen finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p108">**Chrome control:** Thechrome control enables you to use the navigation header of a specific SharePoint site in your add-in without needing to register a server library or use a specific technology or tool. To use this functionality, you must register a SharePoint JavaScript library through standard <script> tags. You can provide a placeholder by using an HTML **div** element and further customize the control by using the available options. The control inherits its appearance from the specified SharePoint website. For more information, see [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span>
    
    <span data-ttu-id="f34ff-135">**Video ansehen: SharePoint-Chromsteuerelement**</span><span class="sxs-lookup"><span data-stu-id="f34ff-135">**Watch the video: SharePoint chrome control**</span></span>

 

 
![Videos](../images/mod_icon_video.png)
 

 

 
-  <span data-ttu-id="f34ff-p109">**Stylesheet:** Sie können in Ihrer SharePoint-Add-In auf das Stylesheet einer SharePoint-Website verweisen und es zum Formatieren Ihrer Webseiten nutzen, indem Sie die verfügbaren Klassen verwenden. Wenn die Endbenutzer das Design der SharePoint-Website ändern, kann Ihr Add-In außerdem die neuen Formate übernehmen, ohne dass der Verweis in Ihrem Add-In geändert werden muss. Weitere Informationen finden Sie unter [Verwenden des Stylesheets einer SharePoint-Website in Add-Ins für SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p109">**Stylesheet:** You can reference a SharePoint website's style sheet in your SharePoint Add-in and use it to style your webpages using the available classes. In addition, if the end users change the SharePoint website's theme, your add-in can adopt the new set of styles without modifying the reference in your add-in. For more information, see [Use a SharePoint website's style sheet in SharePoint Add-ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span></span>
    
 
<span data-ttu-id="f34ff-140">Abbildung 2 zeigt die Ressourcen im Modell für SharePoint-Add-Ins für in der Cloud gehostete Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="f34ff-140">Figure 2 shows the resources in the model for SharePoint Add-ins for cloud-hosted add-ins.</span></span>
 

 

<span data-ttu-id="f34ff-141">**Abbildung 2. Add-In-UX Ressourcen für in der Cloud gehostete Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="f34ff-141">**Figure 2. Add-in UX resources for cloud-hosted add-ins**</span></span>

 

 
![Add-In-UX-Ressourcen für vom Entwickler gehostete Add-Ins](../images/AppUX_devhosted.png)
 

 

 

## <a name="add-in-ux-scenarios-in-sharepoint-hosted-add-ins"></a><span data-ttu-id="f34ff-143">Add-In-UX-Szenarios für von SharePoint gehostete Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-143">Add-in UX scenarios in SharePoint-hosted add-ins</span></span>
<span data-ttu-id="f34ff-144"><a name="SP15_UXdesignapps_SPhosted"> </a></span><span class="sxs-lookup"><span data-stu-id="f34ff-144"><a name="SP15_UXdesignapps_SPhosted"> </a></span></span>

<span data-ttu-id="f34ff-p110">Wenn Ihr Add-In in SharePoint gehostet wird, ist es weniger wahrscheinlich, dass sich die User Experience stark ändert, wenn Benutzer zwischen der Hostwebsite und der Add-In-Website hin und her wechseln. Wenn das Add-In bereitgestellt wird, übernimmt die Add-In-Website das Stylesheet und Design der Hostwebsite. Sie können das Chromsteuerelement und das Stylesheet in einem in SharePoint gehosteten Add-In weiterhin verwenden, der signifikanteste Unterschied bei in der Cloud gehosteten Szenarien besteht jedoch in der Verfügbarkeit der Add-In-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p110">If your add-in is hosted in SharePoint, the user experience is less likely to change very much when users move back and forth between the host web and the add-in web. When the add-in is deployed, the add-in web takes the style sheet and theme from the host web. You can still use the chrome control and style sheet in a SharePoint-hosted add-in, but the most significant difference with cloud-hosted scenarios is the availability of the add-in template.</span></span>
 

 
<span data-ttu-id="f34ff-148">Die folgenden UX-Ressourcen sind für von SharePoint gehostete Add-Ins verfügbar:</span><span class="sxs-lookup"><span data-stu-id="f34ff-148">The following UX resource is available for SharePoint-hosted add-ins:</span></span>
 

 

-  <span data-ttu-id="f34ff-p111">**Add-In-Vorlage:** Die Add-In-Vorlage umfasst die **app.master**-Masterpage. Dies ist die Standardoption beim Erstellen eines Add-In-Webs.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p111">**Add-in template:** The add-in template includes the **app.master** masterpage. It is the default option when you create an add-in web.</span></span>
    
 
<span data-ttu-id="f34ff-151">Von SharePoint gehostete Add-Ins profitieren auch selbst von in SharePoint vorhandenen Ressourcen und Technologien, z. B. Multifunktionsleiste, Webpart-Infrastruktur und clientseitiges Rendering.</span><span class="sxs-lookup"><span data-stu-id="f34ff-151">SharePoint-hosted add-ins also benefit themselves from existing resources and technologies in SharePoint such as the Ribbon, web part infrastructure and client-side rendering.</span></span>
 

 

## <a name="scenarios-for-connecting-the-add-in-ux-to-the-host-web"></a><span data-ttu-id="f34ff-152">Szenarios für das Herstellen einer Verbindung zwischen Add-In-UX und Hostweb</span><span class="sxs-lookup"><span data-stu-id="f34ff-152">Scenarios for connecting the add-in UX to the host web</span></span>
<span data-ttu-id="f34ff-153"><a name="SP15_UXdesignapps_connectingappUX"> </a></span><span class="sxs-lookup"><span data-stu-id="f34ff-153"><a name="SP15_UXdesignapps_connectingappUX"> </a></span></span>

<span data-ttu-id="f34ff-p112">Einige Verwendungsfälle für Ihr Add-In können innerhalb der Hostwebsite ausgelöst werden. SharePoint bietet zwei Möglichkeiten zum Öffnen Ihres Add-Ins über eine Dokumentbibliothek oder Liste, zusätzlich zu den Möglichkeiten, einen Teil der Add-In-UX innerhalb von Seiten anzuzeigen, die in SharePoint gehostet sind.</span><span class="sxs-lookup"><span data-stu-id="f34ff-p112">Some of the use cases for your add-in can be triggered from within the host web. SharePoint provides ways to open your add-in from a document library or list in addition to ways to show some of your add-in UX within SharePoint-hosted pages.</span></span>
 

 
<span data-ttu-id="f34ff-156">Die folgenden UX-Ressourcen sind verfügbar, um Ihre Add-In-UX mit dem Hostweb zu verbinden:</span><span class="sxs-lookup"><span data-stu-id="f34ff-156">The following UX resources are available to connect your add-in UX to the host web:</span></span>
 

 

-  <span data-ttu-id="f34ff-p113">**Benutzerdefinierte Aktionen**: Sie können benutzerdefinierte Aktionen verwenden, um die Hostwebsite-UX mit Ihrem Add-In zu verbinden. Es gibt zwei Typen von benutzerdefinierten Aktionen:Menüband oderECB. Eine benutzerdefinierte Aktion kann Parameter, wie z. B. die Liste oder das Element, in der bzw. dem sie aufgerufen wurde, an eine Remoteseite senden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p113">**Custom actions**: You can use custom actions to connect the host web UX with your add-in. There are two types of custom actions:Ribbon orECB. A custom action can send parameters such as the list or item on which it was invoked to a remote page. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="f34ff-p114">**Add-In-Parts:** Sie können einen Teil der User Experience Ihres Add-Ins mithilfe von Add-In-Parts der Hostwebsite hinzufügen. Das Add-In-Part ist bei der Bereitstellung des Add-Ins im Webpartkatalog auf der Hostwebsite verfügbar. Benutzer können das Add-In-Part einer Seite hinzufügen, indem sie das Steuerelement zum **Hinzufügen von Webparts** verwenden. Weitere Informationen finden Sie unter [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-p114">**Add-in parts:** You can include some of your add-in user experience in the host web by using add-in parts. The add-in part is available in the Web Part gallery in the host web when you deploy the add-in. Users can add the add-in part to a page by using the **Web Part Adder** control. For more information, see [Create add-in parts to install with your SharePoint Add-in](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span></span>
    
 
<span data-ttu-id="f34ff-165">Abbildung 3 zeigt die Ressourcen im Modell für SharePoint-Add-Ins zum Verbinden der Add-In-UX mit dem Hostweb.</span><span class="sxs-lookup"><span data-stu-id="f34ff-165">Figure 3 shows the resources in the model for SharePoint Add-ins to connect your add-in UX to the host web.</span></span>
 

 

<span data-ttu-id="f34ff-166">**Abbildung 3. Add-In-UX-Ressourcen für das Hostweb**</span><span class="sxs-lookup"><span data-stu-id="f34ff-166">**Figure 3. Add-in UX resources for the host web**</span></span>

 

 
![Add-In-UX-Ressourcen für das Hostweb](../images/AppUX_hostweb.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="f34ff-168">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f34ff-168">Additional resources</span></span>
<span data-ttu-id="f34ff-169"><a name="SP15_UXdesignapps_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f34ff-169"><a name="SP15_UXdesignapps_addresources"> </a></span></span>

<span data-ttu-id="f34ff-170">Informationen zur Verwendung der Add-In-UX-Optionen in SharePoint-Add-Ins finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="f34ff-170">To learn how to use the add-in UX options in SharePoint Add-ins, see the following resources:</span></span>
 

 

-  [<span data-ttu-id="f34ff-171">Entwerfen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-171">Design SharePoint Add-ins</span></span>](design-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f34ff-172">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-172">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f34ff-173">Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen</span><span class="sxs-lookup"><span data-stu-id="f34ff-173">Three ways to think about design options for SharePoint Add-ins</span></span>](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f34ff-174">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-174">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 
-  [<span data-ttu-id="f34ff-175">Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f34ff-175">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f34ff-176">Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f34ff-176">SharePoint Add-ins UX design guidelines</span></span>](sharepoint-add-ins-ux-design-guidelines.md)
    
 
-  [<span data-ttu-id="f34ff-177">Erstellen von UX-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f34ff-177">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f34ff-178">Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-178">Use a SharePoint website's style sheet in SharePoint Add-ins</span></span>](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f34ff-179">Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-179">Use the client chrome control in SharePoint Add-ins</span></span>](use-the-client-chrome-control-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f34ff-180">Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="f34ff-180">Create add-in parts to install with your SharePoint Add-in</span></span>](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="f34ff-181">Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f34ff-181">Create custom actions to deploy with SharePoint Add-ins</span></span>](create-custom-actions-to-deploy-with-sharepoint-add-ins.md)
    
 

