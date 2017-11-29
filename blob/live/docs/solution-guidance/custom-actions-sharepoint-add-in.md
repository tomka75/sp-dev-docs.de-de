---
title: Benutzerdefinierte Aktionen in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: d721746d8db8b5a6b01e71a1ea8d031bfd7b4330
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="custom-actions-in-the-sharepoint-add-in-model"></a><span data-ttu-id="72c54-102">Benutzerdefinierte Aktionen in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="72c54-102">Custom actions in the SharePoint add-in model</span></span>
=============================================

<a name="summary"></a><span data-ttu-id="72c54-103">Summary</span><span class="sxs-lookup"><span data-stu-id="72c54-103">Summary</span></span>
-------

<span data-ttu-id="72c54-104">Der Ansatz für die Liste elementmenüs ändern und des Menübands in SharePoint unterscheidet sich im neuen SharePoint-Add-in-Modell befand mit vollständigen Code, der als vertrauenswürdig.</span><span class="sxs-lookup"><span data-stu-id="72c54-104">The approach you take to modify list item menus and the ribbon in SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="72c54-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, elementmenüs Liste Menüband Änderungen wurden in XML (benutzerdefinierte Aktionen) definiert, in Features gepackt und über SharePoint-Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="72c54-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list item menus and ribbon modifications were defined in XML (custom actions), packaged in features, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="72c54-106">In einem Modell Szenario SharePoint-Add-in verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) oder die REST-API, um benutzerdefinierte Aktionen zu erstellen, die Liste elementmenüs und des Menübands ändern.</span><span class="sxs-lookup"><span data-stu-id="72c54-106">In an SharePoint Add-in model scenario, you use the SharePoint Client-side Object Model (CSOM) or REST API to create custom actions that modify list item menus and the ribbon.</span></span> <span data-ttu-id="72c54-107">Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="72c54-107">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="72c54-108">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="72c54-108">High-level guidelines</span></span>
---------------------

<span data-ttu-id="72c54-109">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für das Erstellen und Bereitstellen von benutzerdefinierten Aktionen in das neue SharePoint-Add-in-Modell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="72c54-109">As a rule of a thumb, we would like to provide the following high-level guidelines for creating and deploying custom actions in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="72c54-110">Benutzerdefinierte Aktionen können zum Ändern der Liste elementmenüs und des Menübands verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="72c54-110">Custom actions may be used to modify list item menus and the ribbon.</span></span>
- <span data-ttu-id="72c54-111">Sie können nicht mithilfe einer benutzerdefinierten Aktion direkt über ein Add-in, das eine benutzerdefinierte Aktion implementiert Menüelemente ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="72c54-111">You cannot hide menu items using a custom action directly from an Add-in that implements a custom action.</span></span>
    + <span data-ttu-id="72c54-112">Dies ist, da das [HideCustomAction-Element (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) nicht in der SharePoint ECMA Clients Ide Object Model (CSOM) - [UserCustomAction-Eigenschaften (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx)oder die REST-APIs in SharePoint/Office 365 - verfügbar ist [SP. UserCustomActionCollection Object (sp.js) (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).</span><span class="sxs-lookup"><span data-stu-id="72c54-112">This is because the [HideCustomAction Element (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) is not available in the SharePoint ECMA Clients-ide Object Model (CSOM) - [UserCustomAction properties (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx), or the SharePoint/Office 365 REST APIs - [SP.UserCustomActionCollection object (sp.js) (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).</span></span>
    + <span data-ttu-id="72c54-113">Wenn Sie Menüelemente ausblenden möchten, müssen Sie eine benutzerdefinierte Aktion verwenden, JavaScript oder angepasste CSS in SharePoint-Seiten eingebettet.</span><span class="sxs-lookup"><span data-stu-id="72c54-113">If you need to hide menu items, you must use a custom action to embed JavaScript or customized CSS in SharePoint pages.</span></span> <span data-ttu-id="72c54-114">Die JavaScript- oder -CSS in der SharePoint-Seiten eingebettet werden das Menüelement ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="72c54-114">The JavaScript or CSS embedded in the SharePoint pages hides the menu item.</span></span>
- <span data-ttu-id="72c54-115">Verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) und/oder der REST-APIs in SharePoint/Office 365, um benutzerdefinierte Aktionen zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="72c54-115">Use the SharePoint Client-side Object Model (CSOM), and/or the SharePoint/Office 365 REST APIs to implement custom actions.</span></span>

<span data-ttu-id="72c54-116">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="72c54-116">**Getting started**</span></span>

<span data-ttu-id="72c54-117">Das folgende Beispiel veranschaulicht, wie eine benutzerdefinierte Aktion im Einstellungsmenü in der Hostwebsite hinzugefügt, wie ein Dialogfeld in einer benutzerdefinierten Aktion angezeigt, wie ein Dialogfeld ausgeblendet wird, die eine Seite aus einem remote-add-ins Web gehostet wird und wie Sie mithilfe einer benutzerdefinierten Aktion zum Erstellen von Listen und Festlegen der Design eines Webs.</span><span class="sxs-lookup"><span data-stu-id="72c54-117">The following sample demonstrates how to add a custom action to the site settings menu in the host web, how to show a dialog in a custom action, how to hide a dialog that hosts a page from a remote add-in web, and how to use a custom action to create lists and set the theme of a web.</span></span>

- [<span data-ttu-id="72c54-118">Provisioning.SiteModifier (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="72c54-118">Provisioning.SiteModifier (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)

    <span data-ttu-id="72c54-119">Hier können Sie sehen, dass die Verknüpfung im Beispiel für die benutzerdefinierte Aktion im Menü Websiteeinstellungen hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="72c54-119">Here you can see the link the custom action in the sample adds to the Site Settings menu.</span></span>
    
    ![Im Einstellungsmenü von Office 365 wird die Menüoption Website ändern hervorgehoben angezeigt.](media/Recipes/CustomActions/Custom-Action-In-Site-Settings.png)
    
    <span data-ttu-id="72c54-121">Hier sehen Sie das Popup-Fenster geöffnet wird, über den Link Site ändern.</span><span class="sxs-lookup"><span data-stu-id="72c54-121">Here you can see the popup window opened via the Modify Site link.</span></span>
    
    ![Website ändern Popup-Fenster wird mit einer das Kontrollkästchen Gruppe mit dem Namen Listen angezeigt, die zwei Kontrollkästchen Projekte und Kontakte enthält.](media/Recipes/CustomActions/Custom-Action-Popup-Menu.png)

<a name="related-links"></a><span data-ttu-id="72c54-125">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="72c54-125">Related links</span></span>
=============

- [<span data-ttu-id="72c54-126">Benutzersteuerelemente und Websteuerelemente (SharePoint-Add-in-Anleitung)</span><span class="sxs-lookup"><span data-stu-id="72c54-126">User controls and Web controls (SharePoint Add-in Recipe)</span></span>](user-controls-and-web-controls-sharepoint-add-in.md)
- <span data-ttu-id="72c54-127">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="72c54-127">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="72c54-128">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="72c54-128">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="72c54-129">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="72c54-129">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="72c54-130">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="72c54-130">Related PnP samples</span></span>
===================

- [<span data-ttu-id="72c54-131">Provisioning.SiteModifier (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="72c54-131">Provisioning.SiteModifier (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)
- <span data-ttu-id="72c54-132">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="72c54-132">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="72c54-133">Gilt für</span><span class="sxs-lookup"><span data-stu-id="72c54-133">Applies to</span></span>
==========
- <span data-ttu-id="72c54-134">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="72c54-134">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="72c54-135">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="72c54-135">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="72c54-136">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="72c54-136">SharePoint 2013 on-premises</span></span>
