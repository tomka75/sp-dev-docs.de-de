---
title: "Einführung in das Modul für Plug & Play-Bereitstellung"
ms.date: 11/03/2017
ms.openlocfilehash: 5ffce93158a74f43b6428ba9ab04143eebd68c48
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-pnp-provisioning-engine"></a>Einführung in das Modul für Plug & Play-Bereitstellung

**Autor:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)

_**Gilt für:** SharePoint 2013 | SharePoint Online | Office 365_

Dieses kurze Whitepaper werden die Plug & Play-Bereitstellung Engine, die im April 2015 innerhalb des Projekts [OfficeDev Plug & Play-](http://aka.ms/officedevpnp) veröffentlicht wurde und die werden monatlich, in die Office Developer Plug & Play-Core-Bibliothek mit dem Release-Plan Ausrichtung aktualisiert vorgestellt. Hier sehen Sie ist dank die Verfügbarkeit einiger Office Dev Plug & Play-Core Teammitglieder ([Vesa Juvonen](https://twitter.com/vesajuvonen), [Bert Jansen](https://twitter.com/O365Bert), [Frank Marasco](https://twitter.com/frank_marasco), [Erwin van Hunen](https://twitter.com/erwinvanhunen)und [mich](https://twitter/paolopia)) sowie die gesamte OfficeDev Plug & Play-Gemeinschaft unterstützt .

<a name="thegoal"> </a>
## <a name="the-goal"></a>Das Ziel

Lassen Sie uns über die wichtigsten Ziel gesetzt, müssen eine Bereitstellung Engine starten. Mit der Einführung von Microsoft Office 365 und Microsoft SharePoint Online müssen Entwickler das neue Cloud-Add-in-Modell (auch bekannt als CAM) als eine neue Möglichkeit zum Erstellen von benutzerdefinierten softwarelösungen für Microsoft SharePoint 2013, Microsoft SharePoint Online und Microsoft durchgeführt. Office 365 im Allgemeinen. Jedoch sollte während der letzten Entwickler bereitgestellten benutzerdefinierte Artefakte mit CAML, XML-basierte Features Framework mit vollständigen vertrauen Code (auch bekannt als FTC) Lösungen oder Sandkastenlösungen, Bereitstellen von Artefakten in das neue Modell CAM über Remote"erfolgen Bereitstellen von"Technik. Jedoch, was bedeutet es, führen Sie "remote-Bereitstellung"? Sie bedeutet, dass Client Side Object Model (CSOM) zum Bereitstellen von Artefakten, anstatt das Feature Framework verwenden.

Was geschieht, wenn Sie modellieren und Artefakte mit einer Test- und eine produktionsumgebung bereitstellen möchten, oder was geschieht, wenn Sie zum Automatisieren der Bereitstellung von Artefakten, nur weil Sie Ihre Anpassungen für mehrere Kunden verkaufen möchten? Dienstanbieter entscheidet auch, was geschieht, wenn Sie eine benutzerdefinierten Vorlage definieren möchten, die Sie über mehrere Instanzen von Website, wie kundenorientierte Websites oder Websites Project-orientierten wiederverwenden können?

Verwenden das neue Plug & Play-Bereitstellung Modul, können Sie eine Website modellieren, durch den Entwurf von Websitespalten, Inhaltstypen, Listendefinitionen und Instanzen, zusammengesetzten, Seiten (WebPart-Seiten oder Wiki-Seiten) und vieles mehr über Ihren Webbrowser konfigurieren. Wenn Sie mit dem Entwurf fertig sind, können Sie exportieren, was Sie in einem persistenten provisioning Vorlage-Format (XML, JSON oder beliebig) getan haben, und Sie können, dass die Vorlage anwenden, wie viele Websites adressieren wie soll.

Wenn es interessant... Lesen Sie weiter, und lassen Sie uns hier erfahren Sie, wie es!

<a name="creatingtemplate"> </a>
## <a name="creating-a-provisioning-template"></a>Erstellen einer Bereitstellung Vorlage

Wie bereits erwähnt, die einfachste Möglichkeit zum Erstellen einer benutzerdefinierten Vorlage für die Bereitstellung wird zum Erstellen einer neuen Websitesammlung aktuell in Microsoft SharePoint Online, konfigurieren die Artefakte (zusammengesetzt aussehen, Websitespalten, Inhaltstypen, Listen Instanzen, Seiten, Dateien usw.) und zu Speichern Sie das Ergebnis als Vorlage bereitstellen.

Folglich angenommen, Sie haben eine Beispiel-Website mit einem benutzerdefinierten definiert (benutzerdefinierten Farbdesigns, benutzerdefiniertes Logo, benutzerdefinierten Hintergrundbilds) suchen. Sie können die resultierende Homepage in der folgenden Abbildung sehen.

![Die Homepage einer Website Vorlage](./media/Introducing-the-PnP-Provisioning-Engine/Figure-1-SiteTemplate01.png)

Darüber hinaus haben Sie eine Reihe von Websitespalten, eines Inhaltstyps und einer Bibliothek Rechnungen mit einer benutzerdefinierten Ansicht definiert. In den folgenden beiden Abbildungen sehen Sie das Ergebnis.

![Eine Bibliothek mit Rechnungen mit eines benutzerdefinierten Inhaltstyps](./media/Introducing-the-PnP-Provisioning-Engine/Figure-2-SiteTemplate02.png)

![Der Einstellungsseite der Bibliothek Rechnungen](./media/Introducing-the-PnP-Provisioning-Engine/Figure-3-SiteTemplate03.png)

Um diese Website als Vorlage Provisioning exportieren möchten, können Sie entweder PowerShell (Dank die Arbeit von [Erwin](https://twitter.com/erwinvanhunen)!) oder CSOM-Code mit einigen Erweiterungsmethoden verwenden die von der OfficeDev Plug & Play-Hauptbibliothek bereitgestellt werden. 

Um die PowerShell-Erweiterungen verwenden, können Sie einfach auf die richtige URL ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) für Microsoft SharePoint Online) oder [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) für Microsoft SharePoint 2013 durchsuchen, und installieren Sie die OfficeDev Plug & Play-Kern-PowerShell-Erweiterungen. Nachdem Sie der PowerShell-Umgebung mit Microsoft Office 365 mit dem Cmdlet *Connect-SPOnline* verbunden haben, können Sie das folgende PowerShell-Cmdlet verwenden können:

*Get-SPOProvisioningTemplate-, "PnP-Provisioning-File.xml"*

Die *– Out* Argument weist das Cmdlet Informationen dazu, wo die Bereitstellung Vorlage zu speichern.

Auf der anderen Seite, um die CSOM-Erweiterungen verwenden können Sie einfach erstellen beliebigen (Windows-Konsole SharePoint Add-in, was Sie wollen) des .NET Softwareprojekts, und fügen die OfficeDev Plug & Play-NuGet-Paket. NuGet-Paket ist in zwei Varianten verfügbar: OfficeDev Plug & Play-Core V15, dem Microsoft SharePoint 2013 lokal bezieht, und OfficeDev Plug & Play-Core, die Microsoft SharePoint Online beruht.

Ziel: wir Microsoft SharePoint Online, die mehr getestet wurde, und die wichtigsten als Ziel für die Arbeit Plug & Play-Kern-Team. Sie müssen nur eine Verbindung mit Microsoft Office 365, erstellen eine Instanz des *ClientContext* und rufen Sie einen Verweis auf ein *Web* -Objekt. Dank einer neuen Erweiterungsmethode namens *GetProvisioningTemplate*können Sie ein *ProvisioningTemplate* -Objekt abrufen, die mit einer Vorlage Provider und eine Serialisierung mit gespeichert werden kann. Die Vorlagenanbieter und die Serialisierung mit-Objekte können angepasst werden, sodass Sie unabhängig Persistenz Speicher- und Serialisierung Sie formatieren implementieren können. Sofort einsetzbar bietet das Plug & Play-Bereitstellung Modul Unterstützung für Anbieter von Vorlagen Dateisystem, SharePoint und Azure BLOB-Speicher sowie für XML und JSON Serialisierungsformatierer. In der folgenden Abbildung (haben, [Vesa](https://twitter.com/vesajuvonen)) sehen Sie einen Überblick über die allgemeine Architektur des Plug & Play-Provisioning-Datenbankmoduls.

![Die Architektur von Plug & Play-Bereitstellung Engine-Framework](./media/Introducing-the-PnP-Provisioning-Engine/Figure-4-PnP-Provisioning-Framework-Outline.png)

Das Ergebnis der extrahieren und Speichern einer *ProvisioningTemplate* Instanz-Objekts werden beispielsweise eine XML-Datei wie im folgenden Auszug XML-Code dargestellt:
    
    <?xml version="1.0"?>
    <pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema">
      <pnp:Preferences Generator="OfficeDevPnP.Core, Version=1.2.515.0, Culture=neutral, PublicKeyToken=null" />
      <pnp:Templates ID="CONTAINER-TEMPLATE-1D3F60898418437E8B275147BEC7B0F5">
    <pnp:ProvisioningTemplate ID="TEMPLATE-1D3F60898418437E8B275147BEC7B0F5" Version="1">
      <pnp:Security>
    <pnp:AdditionalAdministrators>
      <pnp:User Name="i:0#.f|membership|paolo@piasysdev.onmicrosoft.com" />
    </pnp:AdditionalAdministrators>
      </pnp:Security>
      <pnp:Files>
    <pnp:File Src="PnP.png" Folder="SiteAssets" Overwrite="true" />
    <pnp:File Src="STB13_Rick_01_small.png" Folder="SiteAssets" Overwrite="true" />
      </pnp:Files>
      <pnp:SiteFields>
    <Field Type="DateTime" DisplayName="Invoice Date" Required="FALSE" EnforceUniqueValues="FALSE"
        Indexed="FALSE" Format="DateOnly" Group="PnP Columns" FriendlyDisplayFormat="Disabled"
        ID="{f1c6f202-f976-4f4e-b0a3-8b984991d00d}" SourceID="{5a15b9ca-4410-4854-bc61-d7fb0ff84e56}"
        StaticName="PnPInvoiceDate" Name="PnPInvoiceDate" CalType="0">
      <Default>[today]</Default>
    </Field>
    <Field Type="Text" DisplayName="Invoice Number" Required="FALSE" 
        EnforceUniqueValues="FALSE" Indexed="FALSE" MaxLength="20" Group="PnP Columns"
        ID="{5049a822-424c-4479-9648-79c4b3214375}" SourceID="{5a15b9ca-4410-4854-bc61-d7fb0ff84e56}"
        StaticName="PnPInvoiceNumber" Name="PnPInvoiceNumber">
    </Field>
      </pnp:SiteFields>
      <pnp:ContentTypes>
    <pnp:ContentType ID="0x01010097931365769EE34E9078576A150FF52E" Name="Invoice"
        Description="" Group="PnP Content Types">
      <pnp:FieldRefs>
    <pnp:FieldRef ID="5049a822-424c-4479-9648-79c4b3214375" Name="PnPInvoiceNumber" />
    <pnp:FieldRef ID="f1c6f202-f976-4f4e-b0a3-8b984991d00d" Name="PnPInvoiceDate" />
      </pnp:FieldRefs>
    </pnp:ContentType>
      </pnp:ContentTypes>
      <pnp:Lists>
    <pnp:ListInstance Title="Invoices" Description=""
        DocumentTemplate="{site}/Invoices/Forms/template.dotx" TemplateType="101" Url="Invoices"
        EnableVersioning="true" MinorVersionLimit="0" MaxVersionLimit="500"
        TemplateFeatureID="00bfea71-e717-4e80-aa17-d0c71b360101" ContentTypesEnabled="true"
        EnableAttachments="false">
      <pnp:ContentTypeBindings>
    <pnp:ContentTypeBinding ContentTypeID="0x01010097931365769EE34E9078576A150FF52E" Default="true" />
      </pnp:ContentTypeBindings>
      <pnp:Views>
    <View Name="{3D715498-8FA2-4B80-8D35-885B2A4CCBDE}" MobileView="TRUE" MobileDefaultView="TRUE"
            Type="HTML" DisplayName="All Documents"
            Url="/sites/PnPProvisioningDemo/Invoices/Forms/AllItems.aspx" Level="1"
            BaseViewID="1" ContentTypeID="0x" ImageUrl="/_layouts/15/images/dlicon.png?rev=38">
      <Query>
    <OrderBy>
      <FieldRef Name="FileLeafRef" />
    </OrderBy>
      </Query>
      <ViewFields>
    <FieldRef Name="DocIcon" />
    <FieldRef Name="LinkFilename" />
    <FieldRef Name="Modified" />
    <FieldRef Name="Editor" />
      </ViewFields>
      <RowLimit Paged="TRUE">30</RowLimit>
      <JSLink>clienttemplates.js</JSLink>
      <XslLink Default="TRUE">main.xsl</XslLink>
      <Toolbar Type="Standard" />
    </View>
    <View Name="{D9BC935E-2154-47EE-A9E2-7C9490389007}" DefaultView="TRUE" MobileView="TRUE"
            Type="HTML" DisplayName="All Invoices"
            Url="/sites/PnPProvisioningDemo/Invoices/Forms/All Invoices.aspx" Level="1"
            BaseViewID="1" ContentTypeID="0x" ImageUrl="/_layouts/15/images/dlicon.png?rev=38">
      <Query>
    <OrderBy>
      <FieldRef Name="FileLeafRef" />
    </OrderBy>
      </Query>
      <ViewFields>
    <FieldRef Name="DocIcon" />
    <FieldRef Name="LinkFilename" />
    <FieldRef Name="Modified" />
    <FieldRef Name="Editor" />
    <FieldRef Name="PnPInvoiceDate" />
    <FieldRef Name="PnPInvoiceNumber" />
      </ViewFields>
      <RowLimit Paged="TRUE">30</RowLimit>
      <Aggregations Value="Off" />
      <JSLink>clienttemplates.js</JSLink>
      <XslLink Default="TRUE">main.xsl</XslLink>
      <Toolbar Type="Standard" />
    </View>
      </pnp:Views>
      <pnp:FieldRefs>
    <pnp:FieldRef ID="5049a822-424c-4479-9648-79c4b3214375" Name="PnPInvoiceNumber"
            DisplayName="Invoice Number" />
    <pnp:FieldRef ID="f1c6f202-f976-4f4e-b0a3-8b984991d00d" Name="PnPInvoiceDate"
            DisplayName="Invoice Date" />
      </pnp:FieldRefs>
    </pnp:ListInstance>
      </pnp:Lists>
      <pnp:Features />
      <pnp:CustomActions />
      <pnp:ComposedLook
    BackgroundFile="{sitecollection}/SiteAssets/STB13_Rick_01_small.png"
    ColorFile="{sitecollection}/_catalogs/theme/15/Palette012.spcolor"
    SiteLogo="{sitecollection}/SiteAssets/PnP.png"
    Name="RED"
    MasterPage="{sitecollection}/_catalogs/masterpage/seattle.master"
    FontFile="" />
    </pnp:ProvisioningTemplate>
      </pnp:Templates>
    </pnp:Provisioning>
    

Wie Sie sehen können, sind die XML-Elemente verständlich. Das im Beispiel verwendete XML-Schema verweist auf die 201505 Version des Schemas Plug & Play-Bereitstellung (XML-Namespace: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), die zusammen mit der OfficeDev Plug & Play-Gemeinschaft definiert wurde und die finden Sie auf GitHub über die folgende URL: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/). In demselben Repository finden Sie auch ein Abzugsverteilung(en) (MD) automatisch generierten Dokument die beschreibt die Hauptelemente, Typen und Attribute, die eine Bereitstellung XML-Vorlage manuell zu definieren.

Die wirkliche Stärke dieses provisioning Modul ist jedoch die Verfügbarkeit von einem allgemeinen, Serialisierungsformat, unabhängig von der Domänenmodell ist. Tatsächlich intern das Plug & Play-Bereitstellung Modul vollständig aus beliebigen Serialisierungsformat abgekoppelt und das gesamte Modul einfach Instanzen des Typs *ProvisioningTemplate* behandelt. In der folgenden Abbildung können Sie beispielsweise das "Schnellansicht" Fenster von Microsoft Visual Studio 2013 zeigt eine Objektinstanz ProvisioningTemplate angezeigt.

![Die Struktur - innerhalb einer Debugger Watch - eines ProvisioningTemplate-Objekts](./media/Introducing-the-PnP-Provisioning-Engine/Figure-5-Domain-Model.png)

Es ist zum Schluss kommen die *ProvisioningTemplate* manuell definieren mithilfe einer Modellsite oder durch Erstellen eines XML-Dokuments, das anhand des Plug & Play-Bereitstellung XSD-Schemas überprüft oder indem Sie einfach .NET Code schreiben und erstellen die Hierarchie der Objekte. Auch möglich, eine Kombination dieser Ansätze: Sie die Bereitstellung mit einer Modellsite Vorlage entwerfen, in eine XML-Datei zu speichern, tun können und einige Anpassungen in-Memory während der Bearbeitung der *ProvisioningTemplate* -Instanz in Ihrem Code.

<a name="applyingtemplate"> </a>
## <a name="applying-a-provisioning-template"></a>Anwenden einer Bereitstellung Vorlage

Nun, was haben eine Vorlage Bereitstellung ist und wie die Domänenmodell extrahieren-Objekt aus einer vorhandenen Website, sind Sie bereit, in eine Zielwebsite zu übernehmen. Nehmen wir an, dass Sie eine andere frische neue Websitesammlung in Microsoft SharePoint Online verfügen, die mit der Vorlage Teamwebsite, wie er in der folgenden Abbildung dargestellt ist erstellt wurde.
 
![SharePoint Online-Seite für die Erstellung einer neuen Websitesammlung](./media/Introducing-the-PnP-Provisioning-Engine/Figure-6-Target-Site-Creation.png)

Standardmäßig wird die Website wie in der folgenden Abbildung aussehen, das Standardlayout einer SharePoint Online-Website ist.

![Die Homepage einer aktuell neuer Zielwert](./media/Introducing-the-PnP-Provisioning-Engine/Figure-7-Target-Site-Created.png)

Sie können nun durch den Einsatz von PowerShell oder indem Sie .NET Code schreiben ein benutzerdefiniertes *ProvisioningTemplate* Instanz Objekts anwenden. Wenn Sie PowerShell verwenden möchten, zeigt der folgende Auszug aus, wie das *Anwenden-SPOProvisioningTemplate* -Cmdlet verwendet werden kann.

*Anwenden von SPOProvisioningTemplate-Pfad "PnP-Provisioning-File.xml"*

Die *– Pfad* -Argument verweist auf die Quelldatei für die Vorlage, die das Cmdlet zu der aktuell verbundenen Website (durch das Cmdlet *Connect-SPOnline* impliziert) automatisch angewendet wird. In der folgenden Abbildung sehen Sie das letzte Ergebnis.

![Die Homepage einer Ziel-Website basierend auf einer Bereitstellung mit Vorlagen](./media/Introducing-the-PnP-Provisioning-Engine/Figure-8-Target-Site-Provisioned.png)

Wie Sie sehen können, die Website ist dasselbe aussehen wie die ursprüngliche Vorlage und die Rechnungen-Bibliothek mit allen der gleichen zugrunde liegenden Struktur und-Konfiguration (Websitespalten, Inhaltstypen usw.) enthält.

Was geschieht mit .NET Code? Hier ist ein Auszug zum CSOM und die OfficeDev Plug & Play-Hauptbibliothek Erweiterungsmethoden verwenden, um die Vorlage anwenden.

    using (var context = new ClientContext(destinationUrl))
    {
      context.Credentials = new SharePointOnlineCredentials(userName, password);
      Web web = context.Web;
      context.Load(web, w => w.Title);
      context.ExecuteQueryRetry();
    
      // Configure the XML file system provider
      XMLTemplateProvider provider =
      new XMLFileSystemTemplateProvider(
        String.Format(@"{0}\..\..\",
        AppDomain.CurrentDomain.BaseDirectory),
        "");
    
      // Load the template from the XML stored copy
      ProvisioningTemplate template = provider.GetTemplate(
        "PnP-Provisioning-Demo-201505-Polished.xml");
    
      // Apply the template to another site
      Console.WriteLine("Start: {0:hh.mm.ss}", DateTime.Now);
    
      // We can also use Apply-SPOProvisioningTemplate
      web.ApplyProvisioningTemplate(template);
     
      Console.WriteLine("End: {0:hh.mm.ss}", DateTime.Now);
    }
    
Zum Starten, müssen Sie eine Instanz eines Objekts Vorlagenanbieter, je nachdem, welche Art von Permanenz verwendet zum Speichern und Laden Sie die Vorlage erstellen.  Im nächsten Schritt laden Sie die Vorlage aus dem Repository Quelle mithilfe der *GetTemplate* -Methode. Schließlich wenden die Vorlage auf der Zielwebsite Sie mit der Erweiterung *ApplyProvisioningTemplate* -Methode des Typs Web.

Durchschnittlich dauert die Bibliothek ein paar Minuten, wenden Sie die Vorlage, unabhängig davon, ob Sie PowerShell oder .NET Code verwenden. Bei Bedarf können Sie registrieren ein Stellvertreters für den Gesamtprozess überwachen, während der Bereitstellung ausgeführt wird. Wir sind noch verbessern Leistungsmerkmalen des Moduls und bisher haben haben wir uns unsere Aufmerksamkeit Funktionen und Funktionen.

<a name="advancedtopics"> </a>
## <a name="advanced-topics"></a>Weiterführende Themen

Dies ist nur ein einführende Artikel in naher Zukunft tiefer, um einige erweiterten Themen laufend wird. Dennoch ist es wichtig zu verstehen, dass die neue Plug & Play-Bereitstellung Engine verwenden, Sie können auch Taxonomien bereitstellen als auch mithilfe von Variablen und Token, das zur Laufzeit, basierend auf was Sie bereitstellen werden ersetzt werden können (Liste-IDs, Parameter, Begriff IDs usw.). Sie können die Bereitstellung Engine aus den Timer-Job-Dienste, vom Anbieter gehosteten-add-ins, externen Websites und aufrufen. Das Plug & Play-Modul Bereitstellung können Sie schließlich Artefakte von Test/Staging-Umgebungen produktionsumgebungen verschieben.

Darüber hinaus auf Channel 9 ist ein [Abschnitt für Plug & Play-OfficeDev](http://aka.ms/OfficeDevPnPVideos), in dem Sie einige Videos über die Plug & Play-Bereitstellung Engine und die Plug & Play-PowerShell-Erweiterungen überwachen können:

- [Erste Schritte mit Plug & Play-Bereitstellung Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine)
- [Betrachtung der Sequenzierung Plug & Play-Bereitstellung Engine-Schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
- [Einführung in die PowerShell-Cmdlets PnP](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)

<a name="wrapup"> </a>
## <a name="requirements-and-wrap-up"></a>Anforderungen und – Zusammenfassung ##

Um mit der Plug & Play-Bereitstellung Engine lokalen wiedergegeben werden sollen, benötigen Sie mindestens die SharePoint 2013 März 2015 kumulative Update installiert haben, wie das Modul nutzt einige [neue Funktionen](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) von der clientseitigen Objektmodell, die nicht verfügbar sind frühere Versionen des Produkts. Wenn Sie auf Microsoft SharePoint Online abzielen, sind die Anforderungen automatisch Dank der Software als Dienstmodell erfüllt.

Geben Sie mit der Plug & Play-Bereitstellung Engine wiedergegeben werden sollen Sie, geben Sie uns Feedback und genießen Sie die Zukunft der SharePoint-Add-in-Modell und remote-Bereitstellung!

<a name="bk_addresources"> </a>
## <a name="see-also"></a>Siehe auch

-  [Office 365 Development Patterns & Practices auf GitHub](https://github.com/SharePoint/PnP/)
-  [SharePoint-Gruppe der Entwickler](http://aka.ms/sppnp-community) bei Microsoft Tech-Community
