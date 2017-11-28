---
title: Der websitebereitstellung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c45236c0c66aafdad1669354b50291fc2c009495
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="site-provisioning-in-the-sharepoint-add-in-model"></a>Der websitebereitstellung in der SharePoint-add-in-Objektmodell
================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Bereitstellen von Websitesammlungen und Websites sub unterscheidet sich im neuen SharePoint-Add-in-Modell im Vergleich zu, wie es in den vollständigen Code, der als vertrauenswürdig war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, die Sie Erstellen von Websitesammlungen und Unterwebsites mit den Websitedefinitionen und Webvorlagen und anschließend deklarativen Code zum Konfigurieren der Websites und Anwenden von Anpassungen verwenden würden. In diesem Modell ist in der Regel verwenden Sie deklarativen Code Erstellen von Websitespalten, Inhaltstypen und Listen in XML definierten anschließend zum SharePoint Feature Frameworkelemente zu packen und bereitstellen.

In einem Modell Szenario SharePoint-Add-in können Sie SharePoint Client Side Object Model (CSOM) verwenden, erstellen und Konfigurieren von Websitesammlungen und Websites sub. Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.

Auf allgemeiner Ebene sieht das remote provisioning Muster:

![(1) eine remote Zeitgeberauftrag auf (2) Initial Bereitstellung basierend auf der Website im Feld Out geht. In der Regel team eine Website oder Veröffentlichungswebsite. Objekte werden aus der Bereitstellung Engine mit CSOM/REST hochgeladen. (3) übernehmen Sie die erforderlichen (Konfigurationen usw.) auf der Basis Out der im Feld Website basierend auf der Auswahl des Benutzers die Projektwebsite, Organisationseinheit Website oder Arbeitsgruppe-Website erstellen. Dies ist der Teil Spezialisierung, aber da wir von OOB Website beginnen, möchten wir immer die neuesten Verbesserungen an ihn als Base Linie.](media/Recipes/SiteProvisioning/overview.png)

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt wir empfehlen die folgenden allgemeinen Richtlinien für das Erstellen von Websitesammlungen und sub-Websites.

- Bereitstellen von Websitesammlungen und sub-Websites basierend auf den Out-of-Box-Websitevorlagen, die im Lieferumfang von SharePoint.
    + Verwenden des SharePoint-CSOM zum Erstellen von Websitesammlungen und Websites sub.
- Gelten Anpassung und Einstellungen für die Out-of-Box-Websitesammlungen und Websites auf Ihre Bedürfnisse zugeschnitten sub.
    + Verwenden des SharePoint-CSOM, Anpassung und Einstellungen anzuwenden.
- Es wird empfohlen, dass Sie bei der Erstellung von nicht featureelementen Framework verwenden erstellen Websitesammlungen und Websites sub.
    + Die einzige Ausnahme dieser Richtlinie wird bei Verwendung der deklarativen XML-basierte Bereitstellung einer Web-Add-in in einer SharePoint-hosted SharePoint Add-in. Dies ist, da das CSOM nicht in einer SharePoint-hosted SharePoint Add-in zur Verfügung steht.

<a name="challenges-when-creating-site-collections-and-sub-sites"></a>Probleme beim Erstellen von Websitesammlungen und Unterwebsites
--------------------------------------------------

**Erstellen Sie in einem Webbrowser im Vergleich zu erstellen, mit code** 

Es ist wichtig zu verstehen, Erstellen von Websitesammlungen und Sub-über den Webbrowser Websites und unterscheiden sich über Code. In dieser Liste werden die verschiedenen Optionen beschrieben.

- **Erstellen über einen Webbrowser**
    + Bei dieser Option werden Benutzer auf eine SharePoint-Website über einen Webbrowser zugreifen und verwenden Sie die Administrative Seiten zum Erstellen von Websitesammlungen und Websites sub.
    + In der Regel ist nur dann Sie den Webbrowser verwenden müssen manuell erstellen von Websitesammlungen und Unterwebsites wird, wenn Sie sind Prototypen oder Ändern einer einzelnen SharePoint-Website, die nicht eingeschlossen andere Websitesammlungen oder Websites sub wachsen geplant ist.  
- **Erstellen mithilfe von code**
    + Bei dieser Option würden Sie SharePoint-CSOM-Code zum Erstellen von Websitesammlungen und Websites sub ausführen. 
    + Weiter unten in diesem Artikel erhalten Sie Informationen zu einigen Ansätze, Sie verwenden können, um den SharePoint-CSOM-Code auszuführen.

Beachten Sie beim **Erstellen von über einen Webbrowser** die folgenden Punkte.

- Erstellen von Websitesammlungen und Websites über den Webbrowser Sub ist in der Regel ein Prozess kompliziert und zeitraubend.
    + Diese Faktoren stellen Erstellen von Websitesammlungen und Websites über das Web Browser- **fehleranfällig,**sub.   
- Es gibt keine Möglichkeit zum erneuten Erstellen von Websitesammlungen und Sub-Websites (und die darin enthaltenen Komponenten) erstellt werden, über den Webbrowser wiederholbare. 
    + Dies macht es **schwierig** , schnell und konsistent bereitstellen die Websitesammlungen und Websites auf unterschiedliche Umgebungen sub, beim Wechseln von Entwicklung Test zur Produktion.

Wenn **mit Code erstellen**, müssen Sie die folgenden Punkte beachten.

- Erstellen von Websitesammlungen und Unterwebsites durch Code in der Regel beinhaltet die Verwendung von benutzerdefinierten Dienstprogramm-Bibliotheken, SharePoint-CSOM-Code auszuführen.
    + Im Repository OfficeDev Plug & Play-GitHub finden Sie diese Bibliotheken in viele Projekte verfügbar. Sie sind in der gesamten Artikel und am Ende verwiesen.
    + Diese Faktoren machen Erstellen von Websitesammlungen und Websites mit Code **anfällig für Erfolg**sub.
- Können Sie **ganz einfach und konsistent replizieren** von Websitesammlungen und Unterwebsites (und die darin enthaltenen Komponenten) über Code in einer Weise Differenzierte Sicherung erstellt.
    + Sie können **auf einfache Weise** Bereitstellen von Websitesammlungen und Websites auf unterschiedliche Umgebungen sub und beim Wechseln von Entwicklung Test zur Produktion zu verweisen.

**Muss schnell passieren!**

Endbenutzer werden nicht akzeptiert, warten Sie einige Stunden für ihre neue SharePoint-Websites bereitgestellt werden müssen.

**Muss konsistent perfekte!**

Websitesammlungen und Unterwebsites und die verschiedenen Komponenten enthalten sie beispielsweise Websitespalten, Inhaltstypen, Listen, Gestaltungsvorlagen, JavaScript-Dateien, Bilder usw., bilden die Grundlage, die Ihrer Informationsarchitektur, *muss es sich um perfekte*definieren Content!

Falsche Websitesammlung und Sub der websitebereitstellung auswirken können, eine gesamte LOB Anwendung in der SharePoint-Website, in dem sie bereitgestellt werden, sowie andere Teile von SharePoint, und anderen Line-of-Business-Clientanwendungen, die Zugriff auf SharePointServices .

Beispiel: Wenn Sie SharePoint-Websites, die zum Verwalten von Projekten in Ihrem Unternehmen verwendet haben, in den meisten Fällen erstellen Sie eine allgemeine Liste Farbschema für alle Folien. Dafür ist erforderlich, Erstellen von Websitespalten und Inhaltstypen. Wenn Sie Informationen in diesen Websites über die SharePoint-Suchseite suchen, Filtern Sie die Ergebnisse nach Inhaltstyp oder Tag (Websitespalte). Wenn Ihre Websitespalten und Inhaltstypen nicht perfekt konsistent auf allen Projektwebsites sind, erhalten Sie nicht präzise Suchergebnisse.

In diesem Beispiel wird möglicherweise auch auf Inhalte von Such-Webparts, angewendet werden SharePoint-Add-ins, mobilen apps und allen anderen Systemen, die die Informationen in der SharePoint-Websites zugreifen.

<a name="options-to-create-site-collections-and-sub-sites"></a>Optionen zum Erstellen von Websitesammlungen und Websites sub
------------------------------------------------

Es gibt mehrere Optionen, die Sie zum Erstellen von Websitesammlungen und Websites mit dem neuen SharePoint-Add-in-Modell sub verwenden können. Diese Optionen, die alle in der oben beschriebenen **Erstellen mit Code** -Option fallen.

- Überschreiben Sie den Link der Website erstellen
- Überschreiben Sie den Link erstellen Sub-Website
- Verwenden einer vom Anbieter gehosteten SharePoint Add-Ins
- Verwenden Sie .NET/Java/Objective-C Anwendungen oder PowerShell-Skripts

<a name="override-the-create-site-link"></a>Überschreiben Sie den Link der Website erstellen
-----------------------------

In diesem Muster wird die Verknüpfung zum Erstellen einer Websitesammlung mit einem Link außer Kraft gesetzt, die auf eine vom Anbieter gehosteten SharePoint-Add-in verweist. CSOM-Code in ein vom Anbieter gehosteten SharePoint Add-in ausgeführt wird über die remote provisioning Muster als Teil des websiteerstellungsprozesses ausgeführt.

- Das Muster wird nur verwendet, bei der Erstellung der Websitesammlung adressieren. Es wird kein Sub-Websites erstellen.
- Die URL für die Außerkraftsetzung wird in der SharePoint-Verwaltungskonsole konfiguriert. Diese URL verweist auf eine vom Anbieter gehosteten SharePoint-Add-in.
- Der vom Anbieter gehosteten SharePoint Add-in verwendet CSOM-APIs zum Erstellen von Websitesammlungen.
    + CSOM/REST-APIs können auch so konfigurieren Sie andere Aspekte der Website während der Bereitstellungsprozess verwendet werden.
- Dieser Ansatz kann in Office 365-Mandanten und in lokalen SharePoint verwendet werden.
- Bietet eine enorme Flexibilität zum Erstellen und Konfigurieren von SharePoint-Websitesammlungen.
- Einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.

**Konfiguration**

Außer Kraft setzen, um der Link erstellen Website öffnen die Einstellungsseite im SharePoint Administrationscenter (siehe unten).

![Klicken Sie im SharePoint Admin Center Menü mit den Einstellungen Menüoption hervorgehoben.](media/Recipes/SiteProvisioning/sp-admin-center.png)

Klicken Sie dann, überprüfen Sie die Verwendung der Form zu dieser URL das Kontrollkästchen, und geben Sie die URL für das vom Anbieter gehosteten SharePoint Add-in, das die Site Creation-Funktionalität (siehe unten) implementiert.

![Ein Dialogfeld OK Abbrechen Anspruch Nachricht aus der Webseite mit dem Hinweis, dass durch das Ändern des Speicherorts, in dem Benutzer Websites erstellen, Sie können werden Möglichkeit erhalten, bis benutzerdefinierte Skripts ausgeführt werden, die andere Websites (für weitere Details finden Sie unter http://go.microsoft.com/fwlink/?LinkId=164264) zugreifen können. Um dies zu verhindern, führen Sie den folgenden Befehl für SharePoint Online-Verwaltungsshell: Set-SPOsite < SiteURL > - DenyAddAndCustomizePages 1 Führen Sie dennoch möchten, ändern Sie den Speicherort, in dem Benutzer Websites erstellen?](media/Recipes/SiteProvisioning/override-warning.png)

Beachten Sie die SharePoint gewarnt (klicken Sie im Dialogfeld unten) zu Sicherheitsfragen bei diesem Ansatz verknüpft ist und bietet Ihnen eine Option, um diese Art von Funktionalität zu deaktivieren.

![Auf dieser Seite ein Pfeil verweist auf das Kontrollkästchen berechtigt ist, verwenden Sie das Formular unter dieser URL, die nicht überprüft. Andere Text und die Steuerelemente auf dieser Seite: erteilen den Benutzern eine Verknüpfung zum Erstellen von neuen Teamwebsites an einer definierten Position. "Radio Button" Ausblenden der Link nicht ausgewählt ist, Optionsfeld Anzeigen der Link ausgewählt wird. Websitefeld-Klassifikation ist für Benutzer ausgeblendet. Sekundäre Contact-Feld ist nicht erforderlich.](media/Recipes/SiteProvisioning/override-form.png)

**Wenn sie geeignet ist?**

Diese Option funktioniert gut, wenn Sie Ihre Endbenutzer mit einem Self-service-Möglichkeit zum Erstellen von SharePoint-Websitesammlungen basierend auf benutzerdefinierten Vorlagen bereitstellen müssen.

**Erste Schritte**

Die folgenden Artikel beschreiben die Überschreibung Site Link Muster erstellen und bereitstellen, Codebeispiele, um Ihnen den Einstieg erleichtern.

- [Self-Service Site Provisioning von Add-Ins für SharePoint 2013 (MSDN-Blog)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)
    + End-to-End-Artikel zu diesem Muster mit begleitendem Video.
- [Provisioning.Cloud.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
    + Diese Lösung zeigt das Modell für die synchrone Website-Auflistung oder Sub Site Creation-Funktionalität für Websitevorlagen Vorstellung ohne tatsächliche sandkastenlösungen oder stp-Dateien zu verwenden, um. 

<a name="override-the-create-sub-site-link"></a>Überschreiben Sie den Link erstellen Sub-Website
---------------------------------

In diesem Muster wird der Link zum Erstellen einer Sub-Website mit einem Link außer Kraft gesetzt, die auf eine vom Anbieter gehosteten SharePoint-Add-in verweist. CSOM-Code in ein vom Anbieter gehosteten SharePoint Add-in ausgeführt wird über die remote provisioning Muster als Teil des websiteerstellungsprozesses ausgeführt.
 
- Das Muster wird nur verwendet, wenn Sub Site Creation adressieren. Es wird nicht verwendet, um Websitesammlungen zu erstellen.
- Die Überschreibung-URL ist mit einer benutzerdefinierten Aktion konfiguriert, JavaScript verwendet, um den Link zu ändern. Diese URL verweist auf eine vom Anbieter gehosteten SharePoint-Add-in.
- Der vom Anbieter gehosteten SharePoint Add-in verwendet CSOM APIs Sub-Websites erstellen.
    + CSOM/REST-APIs können auch so konfigurieren Sie andere Aspekte der Website während der Bereitstellungsprozess verwendet werden.
- Dieser Ansatz kann in Office 365-Mandanten und in lokalen SharePoint verwendet werden.
- Stellt eine enorme Flexibilität zum Erstellen und Konfigurieren von SharePoint-Websites bereit.
- Einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.

**Wenn sie geeignet ist?**

Diese Option funktioniert gut, wenn Sie Ihre Endbenutzer mit einer Self-service-Möglichkeit zum Erstellen von SharePoint-Sub-Websites basierend auf benutzerdefinierten Vorlagen bereitstellen müssen.

**Erste Schritte**

Die folgenden Artikel beschreiben die Überschreibung Sub Site Link Muster erstellen und bereitstellen, Codebeispiele, um Ihnen den Einstieg erleichtern.

- [Provisioning.Cloud.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
    + Diese Lösung zeigt das Modell für die Bereitstellung von synchrone Website-Auflistung oder Sub Site Creation wünschen, um ein Modell für Websitevorlagen einführen ohne tatsächliche sandkastenlösungen oder stp-Dateien. 
- [Provisioning.SubSiteCreationApp (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SubSiteCreationApp)
    + Diese Lösung verwendet das so genannte remote provisioning Muster, um als flexible Sub Website Vorlage System möglichst bereitzustellen. Darüber hinaus eine zugehörige Video.


<a name="use-a-provider-hosted-sharepoint-add-in"></a>Verwenden einer vom Anbieter gehosteten SharePoint Add-Ins
---------------------------------------

CSOM-Code in ein vom Anbieter gehosteten SharePoint Add-in ausgeführt wird in diesem Muster über die remote provisioning Muster als Teil des websiteerstellungsprozesses ausgeführt.
 
- Das Muster kann zum Ziel Sub-Auflistung und Ihre Website websiteerstellung verwendet werden
- Das SharePoint-Hosting-Add-in muss die Berechtigung Vollzugriff für die SharePoint-Umgebung erteilt werden.
    + Dieses Muster kann in den Microsoft-Marketplace verwendet werden, da sie Vollzugriff-Berechtigungen benötigt.
- SharePoint-Add-in vom Anbieter gehosteten verwendet CSOM-APIs zum Erstellen von Websitesammlungen und Websites sub.
    + CSOM/REST-APIs können auch so konfigurieren Sie andere Aspekte der Website während der Bereitstellungsprozess verwendet werden.
- Dieser Ansatz kann in Office 365-Mandanten und in lokalen SharePoint verwendet werden.
- Stellt eine enorme Flexibilität zum Erstellen und Konfigurieren von SharePoint-Websites bereit.
- Einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.

**Wenn sie geeignet ist?**

Diese Option funktioniert gut, wenn Sie Ihre Endbenutzer mit einem Self-service Möglichkeit zum Erstellen von SharePoint-Websitesammlungen und Websites basierend auf benutzerdefinierten Vorlagen sub bereitstellen müssen. *Beachten Sie, dass Sie benötigen, um Ihren Benutzern einen Link zu den vom Anbieter gehostete Anwendung bereitzustellen, damit sie darauf zugreifen können.*

- [Async provisioning mit hybridszenarien (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/vesku/archive/2015/03/05/hybrid-site-collection-provisioning-from-azure-to-on-premises-sharepoint.aspx)
- [Provisioning.Hybrid.Simple (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Hybrid.Simple)
    + Dieses Beispiel veranschaulicht das einfachste mögliche Hybrid Setup mit Azure-Speicher-Warteschlangen, WebJobs und Service Bus Relay. Dies ist eine Demonstration Hosting Anbieter SharePoint-Add-in in der Azure-Website, die für die Bereitstellung verwendet werden kann neuen benutzerdefinierten Branding-Anforderungen für lokale Websitesammlungen auf lokale Farm, ohne alle SharePoint-Add-in-Infrastruktur.
- [Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
    + In diesem Beispiel wird das lokale Farm zur Unterstützung der Erstellung der Websitesammlung aus einer vom Anbieter gehosteten SharePoint-Add-in zu erweitern.
- [Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
    + Veranschaulicht, wie mit CSOM für Office 365 aus einer vom Anbieter gehosteten SharePoint-Add-in Websitesammlungen erstellen.

<a name="use-netjavaobjective-c-applications-or-powershell-scripts"></a>Verwenden Sie .NET/Java/Objective-C Anwendungen oder PowerShell-Skripts
----------------------------------------------------

In diesem Muster wird CSOM-Code über .NET/Objective-C/iOS Anwendungen oder PowerShell-Skripts ausgeführt.  Dieses Muster umfasst auch mithilfe von remote-Zeitgeberaufträgen; beispielsweise ein Azure Webauftrag.
 
- Das Muster kann zum Ziel Sub-Auflistung und Ihre Website websiteerstellung verwendet werden.
- Die SharePoint-Add-ins muss die Berechtigung Vollzugriff für die SharePoint-Umgebung erteilt werden.
- Authentifizierung kann je nach Art der SharePoint-Add-in zu erstellende und die SharePoint-Sicherheitseinstellungen für eine Herausforderung sein.
- Der vom Anbieter gehosteten SharePoint Add-in verwendet CSOM-APIs zum Erstellen von Websitesammlungen und Websites sub.
    + CSOM/REST-APIs können auch so konfigurieren Sie andere Aspekte der Website während der Bereitstellungsprozess verwendet werden.
- Dieser Ansatz kann in Office 365-Mandanten und in lokalen SharePoint verwendet werden.
- Stellt eine enorme Flexibilität zum Erstellen und Konfigurieren von SharePoint-Websites bereit.
- Einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.

**Wenn sie geeignet ist?**

Diese Option eignet sich für Dev-Vorgängen in Szenarien. Es ermöglicht Ihnen das Erstellen benutzerdefinierter Anwendungen oder Skripts, die speziell für die Verwendung mit Ihrer Prozesse Dev-Vorgängen in integriert sind. Diese Option bietet die höchste Stufe der Automatisierung, da die SharePoint-Add-ins und Skripts erstellt werden können, um ohne Eingriffe des Benutzers ausgeführt werden. 

-   [Async-Bereitstellung für Office 365 mit WebJobs (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/vesku/archive/2015/03/04/asynchronous-on-demand-site-collection-provisioning-to-office-365-with-azure-webjobs.aspx) 
- [Provisioning.Cloud.Async.WebJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Cloud.Async.WebJob)
    + Lösung wird demonstriert, wie Sie eine Lösung mithilfe von Azure Storage Warteschlangen und Azure WebJobs provisioning asynchronen Self-service Site-Auflistung zu erstellen.
-   [Provisioning.Framework.Console (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/samples/Provisioning.Framework.Console) – Site Provisioning Framework Beispiel die Leistungsfähigkeit des neuen Moduls angezeigt.
-   [Provisioning.Cloud.Async (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Cloud.Async) - veranschaulicht Erstellen von Websitesammlungen in Office 365/SharePoint asynchron. Anfragen werden in einer Liste in der SharePoint-Hostwebsite gespeichert. Die Konsolenanwendung enthalten, die in diesem Beispiel wird in Azure oder einer lokalen Umgebung bereitgestellt & geplant. 
 

<a name="related-links"></a>Verwandte links
=============
- [Self-Service Site Provisioning von Add-Ins für SharePoint 2013 (MSDN-Blog)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Provisioning.Cloud.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
- [Provisioning.SubSiteCreationApp (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SubSiteCreationApp)
- [Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
