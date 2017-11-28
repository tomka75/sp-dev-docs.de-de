---
title: Gestaltungsvorlagen in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 1db93cc9e993dd09e83974ce254d3b4031281a4a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="master-pages-in-the-sharepoint-add-in-model"></a>Gestaltungsvorlagen in SharePoint-add-in-Objektmodell
===========================================

<a name="summary"></a>Summary
-------

Der Ansatz, die Sie für das Implementieren von benutzerdefinierter Gestaltungsvorlagen in SharePoint-Websites erforderlich ist unterschiedlich in das neue SharePoint-Add-in-Modell befand mit vollständigen vertrauen Code / Farmlösungen. In einer typischen vollständige vertrauen Code (FTC) / branding Szenario Farmlösung, benutzerdefinierte Masterseiten werden zum Implementieren einer benutzerdefinierten Marke erstellt. Die Gestaltungsvorlagen in der Regel in einer Funktion, die deklarativen Code und eine FTC verwendet verpackt / Farmlösung Bereitstellen der Gestaltungsvorlagen und mit der SharePoint-Website zu registrieren.

In einer SharePoint-Add-Ins Modell branding Szenario benutzerdefinierte Gestaltungsvorlagen möglicherweise auch verwendet werden. Sie können bereitstellen und registrieren Ihre benutzerdefinierten Gestaltungsvorlagen auf SharePoint-Websites über die Bereitstellung von Remote Muster.

<a name="high-level-guidelines-for-custom-master-pages"></a>Allgemeine Richtlinien für die benutzerdefinierten Gestaltungsvorlagen
---------------------------------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für benutzerdefinierte Masterseiten bereitstellen.

- Sie können SharePoint-Websites mithilfe von benutzerdefinierten Gestaltungsvorlagen anpassen, aber Bedenken Sie dadurch werden Sie zusätzliche langfristige Kosten und Probleme mit zukünftige Updates.
    + In den meisten Fällen können Sie alle branding Standardszenarien mit Designs, zusammengesetzten und alternative CSS erzielen.
    
        Finden Sie unter [Branding von SharePoint-Websites (SharePoint-Add-in-Anleitung)](branding-sharepoint-sites-sharepoint-add-in.md) Hier erfahren alles über die verschiedenen Optionen branding für SharePoint-Websites mit dem SharePoint-Add-in-Objektmodell haben.  Die Anleitung hilft Ihnen bei die kurze und der langfristige Auswirkungen der Anpassung von eine betriebsbereite und Sicht der Wartung berücksichtigen. Sie können erkennen, dass eine benutzerdefinierte Gestaltungsvorlage zum Implementieren von bestimmten branding Standarddateispeicherort nicht erforderlich ist. 

    + Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie Änderungen der benutzerdefinierten Gestaltungsvorlagen anwenden, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden.
- Verwenden Sie remote-Bereitstellung bereitstellen und Registrieren des benutzerdefinierte Gestaltungsvorlagen mit SharePoint-Websites.
- Verwenden Sie nicht deklarativen Code oder Sandkasten-Code zum Bereitstellen und Registrieren von Gestaltungsvorlagen mit SharePoint-Websites.  

<a name="team-sites-vs-publishing-sites"></a>Teamwebsites im Vergleich zu Veröffentlichungssites
-------------------------------

**Wann wird eine benutzerdefinierte Gestaltungsvorlage benötigt?**

Beim Anwenden von benutzerdefiniertem branding auf die SharePoint-Websites, treten Sie Teamwebsites und Veröffentlichung von Websites mit Branding versehen werden müssen. Im Allgemeinen verwenden Intranets in lokalen und Office 365-Szenarien in SharePoint erstellt eine Kombination von Teamwebsites und Veröffentlichung von Websites.  

Benutzerdefiniertes branding Anforderungen erfordern oft bestimmtes Layout ändert, Designs und JavaScript Einbetten von Techniken kann nicht erreichen.

In diesem Fall benötigen Teamwebsites in der Regel nicht die Menge an benutzerdefiniertes branding, führen Sie Veröffentlichungswebsites und die Out-of-Box SharePoint moderne Ansicht für mobile Geräte in der Regel ausreichend ist, um die Unterstützung von mobilen Geräten für Teamwebsites. Da dies der Fall ist, wird empfohlen, für die ausschließliche Verwendung benutzerdefinierte Gestaltungsvorlagen für Veröffentlichungssites und AlternativeCSS und benutzerdefinierte SharePoint-Designs (.spcolor-Dateien), Schriftartenschemas (.spfont-Dateien) und Hintergrundbilder definiert als zusammengesetzten Marke Teamwebsites zu verwenden.

**Bereitstellungsaspekte**

- Beim Bereitstellen von benutzerdefinierten Gestaltungsvorlagen mit *Veröffentlichungswebsites* müssen Sie nur für die Bereitstellung von benutzerdefinierten Gestaltungsvorlagen auf der Stammwebsite.
    + Die [Provisioning.PublishingFeatures (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.PublishingFeatures) wird gezeigt, wie benutzerdefinierte Masterseiten für die Veröffentlichung von Websites bereitstellen. 
    + Die [Bereitstellung von SharePoint Veröffentlichungsfeatures (O365 Plug & Play-Video)](http://channel9.msdn.com/Blogs/Office-365-Dev/Provisioning-SharePoint-Publishing-Features-Office-365-Developer-Patterns-and-Practices) führt Sie durch das Beispiel.   
- Wenn Sie benutzerdefinierte Masterseiten für *nicht - Veröffentlichungssites* bereitstellen müssen Sie zum Bereitstellen von benutzerdefinierten Gestaltungsvorlagen für jeden Standort.

Benutzerdefinierte Masterseiten werden in der Regel angewendet, wenn eine Website bereitgestellt wird. Der Bereitstellungsprozess remote passt sehr gut bei diesem Ansatz. In der Regel ist nur dann mithilfe des Webbrowsers wird zum Anpassen von SharePoint-branding manuell anwenden Prototypen oder Ändern einer einzelnen SharePoint-Website, die nicht eingeschlossen andere Websitesammlungen oder Websites sub wachsen geplant ist. 

+ Weitere Deployment-Details und weitere Beispiele finden Sie unter der [Module (SharePoint-Add-in-Anleitung)](modules-sharepoint-add-in.md) und [Der Websitebereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md) .

<a name="more-details-about-custom-master-pages-and-page-layouts-for-sharepoint-sites"></a>Weitere Informationen zu benutzerdefinierten Gestaltungsvorlagen und Seitenlayouts für SharePoint-Websites
----------------------------------------------------------------------------

In Szenarien, in denen eine benutzerdefinierte Gestaltungsvorlage die einzige Möglichkeit zum Implementieren der benutzerdefinierten branding Anforderungen können Sie eine benutzerdefinierte Gestaltungsvorlage und Seitenlayouts erstellen. Behalten Sie im Hinterkopf die Punkte am Anfang dieses Artikels in Bezug auf die langfristige Wartungskosten im Zusammenhang mit diesem Ansatz vorgenommen.

- Verwenden von benutzerdefinierten Gestaltungsvorlagen für SharePoint-Websites enthält die höchste Stufe der Anpassung (unbegrenzt).
- Verwenden von benutzerdefinierten Gestaltungsvorlagen für SharePoint-Websites erfordert die größte Zeitspanne zu implementieren und verwalten Sie die kurz- und langfristigen.
- Alle Änderungen an Out-of-Box-Masterseiten, die im Lieferumfang von Service-Updates werden nicht in benutzerdefinierten Gestaltungsvorlagen wiedergegeben werden.
- Sie können benutzerdefinierte Masterseiten auf einer Ebene pro Website anwenden.
- Bei Verwendung eine benutzerdefinierte Gestaltungsvorlage es wird empfohlen zu eines der Out-of-the-Box Masterseiten und ändern sie Ihre Bedürfnisse.
    + Versuchen Sie, den Umfang der Anpassung zu minimieren, die Sie mit benutzerdefinierten Gestaltungsvorlagen vornehmen. Dies erleichtert die aktualisieren, wenn Office 365-dienständerungen Out-of-Box Gestaltungsvorlagen in benutzerdefinierten Gestaltungsvorlagen repliziert werden müssen.  
- Befinden sich viele erforderlichen Inhaltsplatzhalter in SharePoint-Gestaltungsvorlagen, die nicht entfernt werden müssen, oder sie Seiten, Fehler verursacht. Wenn Sie einen Platzhalter für den Inhalt erforderlichen, da die Minute Sie bereitstellen und zuweisen die Gestaltungsvorlage der Website treten Fehler auf, entfernt haben wissen Sie.

**Wann sind benutzerdefinierte Masterseiten und Seitenlayouts für eine SharePoint-Website geeignet?**

Diese Option funktioniert gut, wenn Ihre Bedürfnisse branding sehr spezifisch sind, oder Sie Veröffentlichungssites.

**Empfohlene bereitstellungsansätzen**

- Benutzerdefinierte Masterseiten können manuell über den Webbrowser hochgeladen und zusammengesetzten manuell zugewiesen werden.
- Benutzerdefinierte Masterseiten möglicherweise hochgeladen und einer SharePoint-Website über das remote provisioning Muster sowie zugewiesen werden.
    + Weitere Deployment-Details und weitere Beispiele finden Sie unter der [Module (SharePoint-Add-in-Anleitung)](modules-sharepoint-add-in.md) und [Der Websitebereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md) .

<a name="related-links"></a>Verwandte links
=============
- [Module (Anleitung SharePoint-Add-Ins)](modules-sharepoint-add-in.md)
- [Website-Bereitstellung (SharePoint-Add-Ins Anleitung)](site-provisioning-sharepoint-add-in.md)
- [Branding von SharePoint-Websites (SharePoint-Add-Ins Anleitung)](branding-sharepoint-sites-sharepoint-add-in.md)
- Hands-2015 - [ausführliche Behandlung von sicheren SharePoint-Branding in Office 365 mithilfe von wiederholbare Muster und Methoden](https://channel9.msdn.com/Events/Ignite/2015/BRK3164)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Design Management mit CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DeployCustomThemeWeb)
- [AlternateCSSUrl und SiteLogoUrl-Eigenschaften in das Webobjekt (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
- [Set-Design auf Website (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.SetThemeToSite)
- [Beim Festlegen eines SharePoint-Designs in einer App für SharePoint (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.Themes)
- [Tätigen von sofort einsatzbereit Seattle master schnell (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.InjectResponsiveCSS)
- Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
