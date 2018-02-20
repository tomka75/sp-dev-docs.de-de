---
title: Feature Heften in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 204f53d47256b51ef6c2495deae4c69ce810fa23
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
<a name="feature-stapling-in-the-sharepoint-add-in-model"></a>Feature Heften in der SharePoint-add-in-Objektmodell
===============================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Ausführen von Code, und stellen Sie Artefakte aus, wenn eine SharePoint-Website bereitgestellt wird unterscheidet in das neue SharePoint-Add-in-Modell es von der Benutzeroberfläche mit vollständigen Code, der als vertrauenswürdig.  In einer typischen vollständige vertrauen Code (FTC) / Out-of-Box-Website, die Definitionen mit geändert wurden Farmlösung Szenario geheftet Features.  Features zum Verpacken und Bereitstellen von Artefakten, Konfigurationen und branding-Objekte mit einer SharePoint-Website verknüpft ist verwendet wurden, und Features auf die Websitedefinition geheftet wurden.  Die geheftet Features wurden dann automatisch installiert und bei der websitebereitstellung aktiviert.

In einem Modell Szenario SharePoint-Add-in können Sie Heften Features, heften-Add-ins oder SharePoint Client Side Object Model (CSOM), zu erstellen und Konfigurieren von Websitesammlungen und Websites sub Bereitstellen von Artefakten, Konfigurationen und branding-Objekten für diese verwenden. Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir bieten die folgenden high Level Richtlinien zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.

- Ist die einzige Möglichkeit, die Sie weiterhin Heften Feature verwenden können, wenn Sie Features für Websitesammlungen für das Heften werden und Sie sandkastenlösungen verwenden, um die Websitedefinitionen und die geheftet Features bereitstellen.    
- Sie können das Add-In Modell mit Mandanten Heften-Add-ins zum Implementieren der Funktion Heften ähnliche Funktionalität bereitgestellt.
- Das remote provisioning Muster können Sie mit der Aktivierung der zusätzlichen Features auf der Basis der Websitedefinition Out-of-Box-Feld über remote-APIs Heften Feature ähnliche Funktionalität implementieren.

<a name="options-to-create-and-configure-site-collections-and-sub-sites-then-deploy-artifacts-configurations-and-branding-assets-to-them"></a>Optionen zum Erstellen und Konfigurieren von Websitesammlungen und Websites dann sub Bereitstellen von Artefakten, Konfigurationen und branding-Objekte für diese
---------------------------------------------------------------------------------------------------------------------------------

Sie müssen einige Optionen zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.

- Heften features
- Heften-Add-ins
- Verwenden Sie das remote provisioning Muster   

<a name="staple-features"></a>Heften features
---------------
In diesem Muster heften Sie Features, Websitedefinitionen.
    
- Dieses Muster ist nur auf der Ebene der Websitesammlung verfügbar.
- Es ist nicht möglich, Funktionen, die in Sub Websites heften.
- Dies ist keine optimale oder empfohlene Ansatz, da sie veraltete sandkastenlösungen verwendet und nicht mehr geeignet für Upgrades Sie legen.

**Wenn sie geeignet ist?**

Wenn Sie legacy-Code in einer lokalen SharePoint-Umgebung migrieren, und Sie haben keine Zeit, es ordnungsgemäß erneut schreiben.

**Erste Schritte**

Im folgende Artikel beschreibt die Funktionen, die in einer Websitedefinition heften.

- [Feature Heften In SharePoint 2010 (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)

<a name="staple-add-ins"></a>Heften-Add-ins
--------------
In diesem Muster stellen Sie in der app-Katalog bestimmte Websitesammlungen, verwaltete Pfade und Websitevorlagen gespeicherten-Add-ins bereit.

- Finden Sie unter der [SharePoint 2013-App-Bereitstellung über ' App Heften ' (MSDN-Blogartikel - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx) ausführliche Informationen zum Anordnen-Modell-Add-in.
- Da das Add-in von einem Administrator abgelegt ist, werden Websitebesitzer werden nicht an das Add-in aus einer Website zu entfernen, die die Bereitstellungskriterien erfüllt.  Nicht auch ein Websitesammlungsadministrator kann das Add-in entfernen.
- Diese zentralisierte Bereitstellung freigegeben dieselben zentralisierten Add-in-Ressourcen (Web-Add-in und Remotewebsite).  Im Wesentlichen ist das Add-in bereitgestellt, aber nicht auf den Websites installiert.  Alle Websites werden die Add-Ins Web und die Remotewebsite aus der Instanz in der app-Katalog installiert nutzen.
- Aufgrund von zentrale Bereitstellung werden remote Ereignisse wie "Handle App Installed", 'Behandeln App deinstalliert' und 'Behandeln App Upgrade' nur einmal ausgelöst werden (wenn das Add-in in der app-Katalog installiert ist).
    + Dies kann erschweren Heften-Muster-Add-in verwenden, um automatisch Änderungen auf Websites angewendet, auf dem sie bereitgestellt wird, da diese Ereignisse nicht ausgelöst werden, wenn es Websites bereitgestellt wird.
- Add-in-Komponenten werden bei-Add-ins auf Websites geheftet werden nicht unterstützt.
- Dieses Muster erfordert die manuelle Benutzeraktionen zum Bereitstellen von Add-Ins.

<a name="use-the-remote-provisioning-pattern"></a>Verwenden Sie das remote provisioning Muster
-----------------------------------

In diesem Muster verwenden Sie SharePoint Client Side Object Model (CSOM) zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.

- Dieses Muster erforderlich keine Packen Artefakte, Konfigurationen und branding-Objekte in separaten Features oder -Add-ins.  Alles kann in ein einzelnes Add-in gepackt.
- Bei Verwendung dieses Muster für die websitebereitstellung überschreiben Sie in der Regel die Abwesenheitsnotiz der Feld-Seite, um eine neue Website erstellen.
- Weitere Informationen zu diesem Muster finden Sie unter der [Website-Bereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md)
- Wenn Sie-Add-ins auf einer SharePoint-Website bereitstellen möchten, kann dies über CSOM erfolgen.  Es folgt ein Beispiel der lädt ein Office-Add-in über ein manifest-Datei am Seitenrand und werden in einer SharePoint-Website installiert.

    ```
    //Create a FileStream object to access the Mail Office Add-in .app file 
    using (FileStream fsSource = new FileStream(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Innovation.Management.AFO.app",
    FileMode.Open, FileAccess.Read))
    {
        //Return the subweb where you want to install the Add-in
        var subweb = ctx.Web;
        ctx.Load(subweb);
        ctx.ExecuteQuery();

        //Load and Install the Add-in on the subweb
        AppInstance appInstance = subweb.LoadAndInstallApp(fsSource);
        ctx.Load(appInstance);
        ctx.ExecuteQuery();
    }
    ```

    + Überwachen der [Erstellen Cloud gehostet Zeile Of Business Applications mit der Add-ins für Office, Office 365, Azure und WP8 (Todd Baginski, Michael Sherman - SharePoint-Konferenz 2014)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361) video sehen, wie diese Vorgehensweise zum Installieren von Office-Add-ins in SharePoint-Websites verwendet wurde Bei der websitebereitstellung.
    + Vollständige Automation kann nur mit-Add-ins, die vollständige Mandanten Berechtigung verfügen, die bereits als vertrauenswürdig eingestuft haben.
        + Finden Sie ein Beispiel für die [Core.Sideloading (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SideLoading) . 

<a name="related-links"></a>Verwandte links
=============
- [Feature Heften In SharePoint 2010 (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)
- [Self-Service Site Provisioning von Add-Ins für SharePoint 2013 (MSDN-Blog)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)
- [SharePoint 2013-App-Bereitstellung über 'App Heften' (MSDN-Blogartikel - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx)
- [Website-Bereitstellung (SharePoint-Add-Ins Anleitung)](site-provisioning-sharepoint-add-in.md)
- [Erstellen der Cloud gehostet Geschäftsanwendungen mit-Add-ins für Office, Office 365, Azure und WP8 (Todd Baginski, Michael Sherman - SharePoint-Konferenz 2014)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Provisioning.Cloud.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
- [Provisioning.SubSiteCreationApp (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SubSiteCreationApp)
- [Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
