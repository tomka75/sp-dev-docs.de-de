---
title: SharePoint-Entwicklung und Design Tools und Methoden
ms.date: 11/03/2017
ms.openlocfilehash: 21d48416cdf3b556200e3f7fc2cb29d4d99ad4a6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-development-and-design-tools-and-practices"></a>SharePoint-Entwicklung und Design Tools und Methoden

Entwurf und Entwicklung SharePoint-Tools können branding zu Ihrer SharePoint-Websites anwenden.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Dieser Artikel enthält Informationen zu den Entwicklungs- und Optionen, die in SharePoint zur Verfügung stehen. Hier finden Sie Informationen zur Verwendung von remote provisioning Muster branding-Objekte auf einer SharePoint-Website anwenden.

## <a name="key-sharepoint-development-and-design-terms-and-concepts"></a>SharePoint-Taste Entwicklungs- und Begriffe und Konzepte
<a name="sectionSection0"> </a>

|**Begriff oder Konzept**|**Definition**|**Weitere Informationen**|
|:-----|:-----|:-----|
|Design-Manager|Ein Feature in der SharePoint-Veröffentlichung Websites oder Teamwebsites mit aktivierter Veröffentlichung, die verwendet wird, importieren und Verwalten von Website-branding-Objekte und Exportieren eines entwurfspakets aktiviert.|Mit Design Manager branding in anderen Tools wie Adobe PhotoShop oder Adobe DreamWeaver in SharePoint erstellten Objekte zu importieren.<br/>SharePoint Designer ist nicht verfügbar für die Verwendung mit OneDrive für Unternehmen oder SharePoint Team-Websites, auf dem Veröffentlichung nicht aktiviert ist.|
|Design-Paket|Für die Verwendung mit SharePoint 2013-Veröffentlichungswebsites vereinfacht, enthält der branding-Objekte, die im Entwurfs-Manager gespeichert sind.| [SharePoint 2013 Design Manager Designpakete](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)|
|Remotebereitstellung|Ein Modell, bei dem Bereitstellen von Websites mithilfe von Vorlagen und Code, ausgeführt wird, außerhalb von SharePoint in einer vom Anbieter gehosteten-add-in.| [Websitebereitstellungsmethoden und Remotebereitstellung in SharePoint 2013](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)<br/>[Self-service Site-Bereitstellung von apps in SharePoint 2013](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)|
|Stammwebsite|Das erste Web innerhalb einer Websitesammlung. Das Stammweb wird manchmal auch als the Web Application Root bezeichnet.||
|Sandkastenlösungen (engl.)|WSP-Dateien, die enthalten Assemblys, andere nicht kompilierten Komponenten und eine XML-Manifestdatei. Eine Sandkasten-Lösung wird teilweise vertrauenswürdigem Code verwendet.| [Sandkastenlösungen (engl.)](https://msdn.microsoft.com/en-us/library/ff798382.aspx)|
|SharePoint Designer 2013|Ein HTML-Designer und Entwurf Asset Management-Tools für die Verwaltung in SharePoint-branding-Elemente. In SharePoint 2013 unterstützt SharePoint Designer hauptsächlich benutzerdefinierte Workflows.| [Was ist in SharePoint Designer 2013 geändert?](https://msdn.microsoft.com/en-us/library/office/jj728659.aspx)<br/>[What's new in SharePoint 2013-Websiteentwicklung?](https://msdn.microsoft.com/en-us/library/office/jj163942.aspx)|
|WSP-Datei|Eine SharePoint-Lösungsdatei. Eine WSP-Datei ist eine CAB-Datei, die Website-Objekten kategorisiert und mit einer manifest.xml-Datei organisiert.| [Lösungsübersicht](https://msdn.microsoft.com/en-us/library/office/aa543214%28v=office.14%29.aspx)|

## <a name="development-options"></a>Entwicklungsoptionen
<a name="sectionSection1"> </a>

Wenn Sie SharePoint 2013 als Entwicklungsplattform verwenden, müssen Sie zum Erstellen einer Umgebung zum Entwickeln, testen, erstellen und Bereitstellen von Inhalten. Informationen zu den Optionen für die Entwicklung finden Sie unter [Überlegungen zur Entwicklungsumgebung](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) in die [Anwendungslebenszyklus-Verwaltung von SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)-Artikel. In Tabelle 2 sind die Kriterien für die verschiedenen Entwicklungsoptionen. 

**Optionen für die SharePoint-Entwicklung, testen und Abnahme**

|**Option**|**Überlegungen**|
|:-----|:-----|
|Team Foundation server|-Für den einfachen Zugriff auf Visual Studio Online befinden.<br/>-Enthält eine zentrale Quelle Code und Lebenszyklus-Management-System.|
|Test und Abnahme Cloud-Umgebungen|-Verwenden Sie einen separaten Mandanten für Tests der Benutzerakzeptanz.<br/>-Separate testumgebung für lokale testen.|
|Lokale Test- und Akzeptanz Umgebungen|-Verwendung für lokale SharePoint-Bereitstellungen.<br/>-Durch Kunden lokalen oder in Microsoft Azure gehostet.|
 
In den meisten Fällen benötigen mindestens die folgenden Mandanten, Sie Obwohl dies je nach Ihren Anforderungen variieren kann:

-  **Entwickler-Mandanten**. Es empfiehlt sich bereitstellen und Verwenden von Ihrer eigenen Developer Site. Auf diese Weise vermeiden Sie Ihre Daten mit der produktionsumgebung mischen. Melden Sie sich für und Bereitstellen einer Entwicklerwebsite, finden Sie unter [Sign up for an Office 365 Developer Site](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) im Artikel [Melden Sie sich für ein Office 365 Developer-Abonnement und richten Sie Ihre Tools und die Umgebung](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).
    
-  **Integrationstests/Mandanten**. Verwenden Sie diese Website, um sicherzustellen, dass neue apps und Funktionen in mehr als eine Websitesammlung und gegen die Dienste und Daten in der produktionsumgebung funktionieren. Konfigurieren der Umgebung, um Funktionen enthalten, die in der Vorschau sind. (Dazu in Ihrem Mandanten-Verwaltungskonsole wählen Sie **Einstellungen für den Webdienst**, und wählen Sie dann unter der Einstellung für **Updates** , die **Erste Version**.) Visual Studio können online automatisierte Tests und alle anderen Fortlaufende Integrationstests ausführen.
    
-  **Produktionsmandanten**. Version getestet, akzeptiert und genehmigt apps, die diese Mandanten. Erstellen einer Entwicklerwebsite können Sie auf diesen Mandanten zu entwickeln und Testen von apps, die im Gültigkeitsbereich klein sind oder haben Auswirkungen isoliert. Im Allgemeinen vermeiden Sie Ihren Umgebungen für Entwicklung und Produktion mischen.
    
## <a name="design-tools"></a>Designtools
<a name="sectionSection2"> </a>

Mithilfe von standardmäßigen-Entwurf und Entwicklung Tools wie HTML, Bilder, CSS-Dateien und JavaScript-Dateien branding Anlagen SharePoint-Website erstellen. Beispielsweise können Sie Adobe DreamWeaver und Adobe PhotoShop entwerfen, die HTML, CSS, JavaScript und Bilddateien, mit denen Sie Ihre SharePoint-Websites mit Branding versehen werden. Alternativ können Sie SharePoint Designer 2013 erstellen, verwalten und Anpassen von Anlagen von branding oder erstellen benutzerdefinierte Lösungen in Visual Studio 2013 verwenden.

### <a name="sharepoint-design-packages-and-wsp-files"></a>SharePoint-Designpakete und WSP-Dateien

Designpakete sind durch Entwurfs-Manager erstellte WSP-Dateien, die vorhersehbare Regeln für die Verpackung Entwurfsressourcen einhalten. Sie sind im Wesentlichen sandboxed Solutions. Wenn Sie ein anderes Tool Paket branding-Objekte in eine WSP-Datei verwenden, werden Ihre branding Anlagen in einem Zustand weniger festen und vorhersehbar bleibt.

Das Design-Paket enthält alle Dateien, die angepasst wurden. Wenn Sie ein Seitenlayout, die einen benutzerdefinierten Inhaltstyp verwendet wird erstellen, umfasst das Design-Paket beispielsweise das Seitenlayout, den benutzerdefinierten Inhaltstyp verwendeten und alle benutzerdefinierten Websitespalten. Das Design-Paket enthält auch mehrere Dateien im Zusammenhang mit jeder zusammengesetzten, die auf der SharePoint-Website, einschließlich Dateien, die an den folgenden Orten hochgeladen angewendet wurden:

- Website-Ressourcen-Bibliothek
    
- Formatbibliothek
    
- Masterseitenkatalog
    
Falls zusammengesetzten werden auf eine Website angewendet, bevor Sie benutzerdefiniertes branding angewendet wird, muss das Design-Paket-Dateien mit .themedcss und .themedpng Dateierweiterungen enthalten. Zum Anwenden der branding-Objekte in einem Paket Design auf einer SharePoint-Website exportieren Sie das Design-Paket, und verwenden Sie das remote provisioning Muster, um den Inhalt des designpakets übernehmen.

SharePoint 2013 enthält die APIs, die Sie verwenden können, Designpakete entwickelt. Wenn Sie entweder SSOM, CSOM oder JSOM verwenden, können Sie die Klassen [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) oder [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) verwenden.

#### <a name="using-the-design-package-csom-to-apply-the-contents-of-design-packages-to-a-sharepoint-site"></a>Mithilfe des entwurfspakets CSOM den Inhalt der Designpakete auf einer SharePoint-Website anwenden

Das folgende Beispiel veranschaulicht die Design-Paket-APIs in das remote provisioning Muster verwenden, um den Inhalt der Designpakete auf einer SharePoint-Website anwenden.

Dieser Code wurde für die Verwendung mit Veröffentlichungswebsites entwickelt. Es ist zwar möglich, die Design-Pakete-API verwenden, einem Branding Teamwebsites, die dem Standardseitenlayout Feature aktiviert ist, kann dies langfristige Supportanfragen führen.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```
using Microsoft.SharePoint.Client;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.SharePoint.Client.Publishing;
namespace ProviderSharePointAppWeb
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_PreInit(object sender, EventArgs e)
        {
            Uri redirectUrl;
            switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
            {
                case RedirectionStatus.Ok:
                    return;
                case RedirectionStatus.ShouldRedirect:
                    Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                    break;
                case RedirectionStatus.CanNotRedirect:
                    Response.Write("An error occurred while processing your request.");
                    Response.End();
                    break;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            // Use TokenHelper to get the client context and Title property.
            // To access other properties, the add-in might need to request permissions
            // on the host web.
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            
            // Publishing feature GUID to use the infrastructure for publishing. 
            Guid PublishingFeature = Guid.Parse("f6924d36-2fa8-4f0b-b16d-06b7250180fa");

            // The site-relative URL of the design package to install.
            // This sandbox design package should be uploaded to a document library.
            // For practical purposes, this can be a configuration setting in web.config.
            string fileRelativePath = @"/sites/devsite/brand/Dev.wsp";

            //string fileUrl = @"https://SPXXXXX.com/sites/devsite/brand/Dev.wsp";
            
        
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load the site context explicitly or while installing the API, the path for
// the package will not be resolved.
                // If the package cannot be found, an exception is thrown. 
                var site = clientContext.Site;
                clientContext.Load(site);
                clientContext.ExecuteQuery();
              
                // Validate whether the Publishing feature is active. 
                if (IsSiteFeatureActivated(clientContext,PublishingFeature))
                {
                    DesignPackageInfo info = new DesignPackageInfo()
                    {
                        PackageGuid = Guid.Empty,
                        MajorVersion = 1,
                        MinorVersion = 1,
                        PackageName = "Dev"
                    };
                    Console.WriteLine("Installing design package ");
                    
                    DesignPackage.Install(clientContext, clientContext.Site, info, fileRelativePath);
                    clientContext.ExecuteQuery();

                    Console.WriteLine("Applying design package");
                    DesignPackage.Apply(clientContext, clientContext.Site, info);
                    clientContext.ExecuteQuery();
                }
            }
        }
        public  bool IsSiteFeatureActivated( ClientContext context, Guid guid)
        {
            var features = context.Site.Features;
            context.Load(features);
            context.ExecuteQuery();

            foreach (var f in features)
            {
                if (f.DefinitionId.Equals(guid))
                    return true;
            }
            return false;
        }
 
    }
}
```

#### <a name="using-filecreationinformation-to-upload-branding-assets-and-a-master-page-to-a-team-site"></a>Verwenden komplexer FileCreationInformation zum Hochladen von Anlagen von branding und einer Gestaltungsvorlage auf eine Teamwebsite

Funktionen von SharePoint 2013-Clientobjektmodell können zum Installieren und deinstallieren Designpakete und Exportieren von Designpakete in SharePoint Online-Websites. Verwenden Sie beispielsweise die [SP. Publishing.DesignPackage.install-Methode (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) , klicken Sie auf der Website das Design-Paket zu installieren, wie im folgenden Beispiel dargestellt.

```
public static void Install(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info,
        string path
)
```

Die [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) -Klasse gibt Metadaten, die beschreiben, den Inhalt des designpakets installiert werden soll. Verwenden Sie die [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) -Methode zum Deinstallieren des designpakets von der Website, wie im folgenden Beispiel dargestellt.

```
public static void UnInstall(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info
)
```

Wenn Sie mit der Veröffentlichung eine Teamwebsite mit Branding versehen müssen feature aktiviert ist, oder eine Veröffentlichung Website auf SharePoint Online, können die [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) oder die [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) -Methode zum Exportieren von Designpakete für Websitevorlagen in der Lösung Katalog. Verwenden Sie die **ExportSmallBusiness** -Methode mit der small Business-Websitevorlage, und verwenden Sie die Methode **ExportEnterprise** für alle anderen Websitevorlagen, wie im folgenden Beispiel dargestellt. Im Beispiel ist Hinweis ThatpackageName eine Zeichenfolge, die den Namen des entwurfspakets darstellt.

```
public static ClientResult<DesignPackageInfo> ExportEnterprise(
        ClientRuntimeContext context,
        Site site,
        bool includeSearchConfiguration
)
```

Wenn Sie diese Methode verwenden, können Sie die Suchkonfiguration in das Design-Paket einschließen, wie im nächsten Beispiel dargestellt. Beachten Sie, dass alle Design Paket Methoden auf der Ebene der Websitesammlung ausgeführt werden.

```
public static ClientResult<DesignPackageInfo> ExportSmallBusiness(
        ClientRuntimeContext context,
        Site site,
        string packageName,
        bool includeSearchConfiguration
)
```

## <a name="design-tool-options-for-sharepoint-online"></a>Tool Entwurfsoptionen für SharePoint Online
<a name="sectionSection3"> </a>

Die Tools, die Sie verwenden können, um eine SharePoint Online-Website mit Branding versehen ist abhängig von Ihrer SharePoint Online-Edition und den Typ der Website, den Sie erstellen möchten. Die Small Business Edition enthält beispielsweise eine Teamwebsite und eine öffentliche Website. Enthält keine Veröffentlichung Website. Des Website-Generator-add-Ins können in SharePoint Online öffentliche Websitebranding anpassen.

Die Enterprise Edition enthält eine teamwebsitesammlung am Stamm Webanwendung an, für die Domäne, die Veröffentlichung nicht enthalten ist. Es ist nicht öffentliche Website enthalten. Verwendung Entwurfs-Manager zum Verwalten von SharePoint-Website-branding-Elemente für die Veröffentlichung der Website in der SharePoint Online Enterprise Edition.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
-  [Anwendungslebenszyklus-Verwaltung in SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)
    
-  [Sandkastenlösungen (engl.)](https://msdn.microsoft.com/en-us/library/ff798382.aspx)
    
-  [Websitebereitstellungsmethoden und Remotebereitstellung in SharePoint 2013](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)
    
-  [SharePoint 2013 Design Manager Designpakete](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)
