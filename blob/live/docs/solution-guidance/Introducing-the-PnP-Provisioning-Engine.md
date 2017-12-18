---
title: "Einführung in das Modul für Plug & Play-Bereitstellung"
ms.date: 11/03/2017
ms.openlocfilehash: 5ffce93158a74f43b6428ba9ab04143eebd68c48
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-pnp-provisioning-engine"></a><span data-ttu-id="96536-102">Einführung in das Modul für Plug & Play-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="96536-102">Introducing the PnP Provisioning Engine</span></span>

<span data-ttu-id="96536-103">**Autor:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)</span><span class="sxs-lookup"><span data-stu-id="96536-103">**Author:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)</span></span>

<span data-ttu-id="96536-104">_**Gilt für:** SharePoint 2013 | SharePoint Online | Office 365_</span><span class="sxs-lookup"><span data-stu-id="96536-104">_**Applies to:** SharePoint 2013 | SharePoint Online | Office 365_</span></span>

<span data-ttu-id="96536-105">Dieses kurze Whitepaper werden die Plug & Play-Bereitstellung Engine, die im April 2015 innerhalb des Projekts [OfficeDev Plug & Play-](http://aka.ms/officedevpnp) veröffentlicht wurde und die werden monatlich, in die Office Developer Plug & Play-Core-Bibliothek mit dem Release-Plan Ausrichtung aktualisiert vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="96536-105">This short whitepaper introduces the PnP Provisioning Engine, which was released in April 2015 within the [OfficeDev PnP](http://aka.ms/officedevpnp) project, and which will be updated on a monthly basis, in alignment with the release schedule of the Office Dev PnP Core Library.</span></span> <span data-ttu-id="96536-106">Hier sehen Sie ist dank die Verfügbarkeit einiger Office Dev Plug & Play-Core Teammitglieder ([Vesa Juvonen](https://twitter.com/vesajuvonen), [Bert Jansen](https://twitter.com/O365Bert), [Frank Marasco](https://twitter.com/frank_marasco), [Erwin van Hunen](https://twitter.com/erwinvanhunen)und [mich](https://twitter/paolopia)) sowie die gesamte OfficeDev Plug & Play-Gemeinschaft unterstützt .</span><span class="sxs-lookup"><span data-stu-id="96536-106">What you will see here is available thanks to the efforts of some of the Office Dev PnP Core Team members ([Vesa Juvonen](https://twitter.com/vesajuvonen), [Bert Jansen](https://twitter.com/O365Bert), [Frank Marasco](https://twitter.com/frank_marasco), [Erwin van Hunen](https://twitter.com/erwinvanhunen), and [me](https://twitter/paolopia)), as well as the whole OfficeDev PnP community.</span></span>

<span data-ttu-id="96536-107"><a name="thegoal"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-107"></span></span>
## <a name="the-goal"></a><span data-ttu-id="96536-108">Das Ziel</span><span class="sxs-lookup"><span data-stu-id="96536-108">The Goal</span></span>

<span data-ttu-id="96536-109">Lassen Sie uns über die wichtigsten Ziel gesetzt, müssen eine Bereitstellung Engine starten.</span><span class="sxs-lookup"><span data-stu-id="96536-109">Let’s start from the main goal of having a provisioning engine.</span></span> <span data-ttu-id="96536-110">Mit der Einführung von Microsoft Office 365 und Microsoft SharePoint Online müssen Entwickler das neue Cloud-Add-in-Modell (auch bekannt als CAM) als eine neue Möglichkeit zum Erstellen von benutzerdefinierten softwarelösungen für Microsoft SharePoint 2013, Microsoft SharePoint Online und Microsoft durchgeführt. Office 365 im Allgemeinen.</span><span class="sxs-lookup"><span data-stu-id="96536-110">With the introduction of Microsoft Office 365 and Microsoft SharePoint Online, developers are facing the new Cloud Add-in Model (aka CAM) as a new way of creating custom software solutions for Microsoft SharePoint 2013, Microsoft SharePoint Online, and Microsoft Office 365 in general.</span></span> <span data-ttu-id="96536-111">Jedoch sollte während der letzten Entwickler bereitgestellten benutzerdefinierte Artefakte mit CAML, XML-basierte Features Framework mit vollständigen vertrauen Code (auch bekannt als FTC) Lösungen oder Sandkastenlösungen, Bereitstellen von Artefakten in das neue Modell CAM über Remote"erfolgen Bereitstellen von"Technik.</span><span class="sxs-lookup"><span data-stu-id="96536-111">However, while in the past developers provisioned custom artifacts using the CAML/XML-based features framework, either with Full Trust Code (aka FTC) solutions or Sandbox Solutions, provisioning artifacts in the new CAM model should be done via the "remote provisioning" technique.</span></span> <span data-ttu-id="96536-112">Jedoch, was bedeutet es, führen Sie "remote-Bereitstellung"?</span><span class="sxs-lookup"><span data-stu-id="96536-112">However, what does it mean to do "remote provisioning"?</span></span> <span data-ttu-id="96536-113">Sie bedeutet, dass Client Side Object Model (CSOM) zum Bereitstellen von Artefakten, anstatt das Feature Framework verwenden.</span><span class="sxs-lookup"><span data-stu-id="96536-113">It means using the Client Side Object Model (CSOM) to provision artifacts, instead of using the feature framework.</span></span>

<span data-ttu-id="96536-114">Was geschieht, wenn Sie modellieren und Artefakte mit einer Test- und eine produktionsumgebung bereitstellen möchten, oder was geschieht, wenn Sie zum Automatisieren der Bereitstellung von Artefakten, nur weil Sie Ihre Anpassungen für mehrere Kunden verkaufen möchten?</span><span class="sxs-lookup"><span data-stu-id="96536-114">What if you want to model and provision artifacts using a test and a production environment, or what if you want to automate provisioning of artifacts, just because you want to sell your customizations to multiple customers?</span></span> <span data-ttu-id="96536-115">Dienstanbieter entscheidet auch, was geschieht, wenn Sie eine benutzerdefinierten Vorlage definieren möchten, die Sie über mehrere Instanzen von Website, wie kundenorientierte Websites oder Websites Project-orientierten wiederverwenden können?</span><span class="sxs-lookup"><span data-stu-id="96536-115">Likewise, what if you want to define a custom site template that you can reuse across multiple site instances, like customer-oriented sites, or project-oriented sites?</span></span>

<span data-ttu-id="96536-116">Verwenden das neue Plug & Play-Bereitstellung Modul, können Sie eine Website modellieren, durch den Entwurf von Websitespalten, Inhaltstypen, Listendefinitionen und Instanzen, zusammengesetzten, Seiten (WebPart-Seiten oder Wiki-Seiten) und vieles mehr über Ihren Webbrowser konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="96536-116">Using the new PnP Provisioning Engine, you can model a site by configuring the design of Site Columns, Content Types, List Definitions and Instances, Composed Looks, Pages (either WebPart Pages or Wiki Pages), and much more, via your web browser.</span></span> <span data-ttu-id="96536-117">Wenn Sie mit dem Entwurf fertig sind, können Sie exportieren, was Sie in einem persistenten provisioning Vorlage-Format (XML, JSON oder beliebig) getan haben, und Sie können, dass die Vorlage anwenden, wie viele Websites adressieren wie soll.</span><span class="sxs-lookup"><span data-stu-id="96536-117">When you are done with the design, you can export what you have done into a persistent provisioning template format (XML, JSON, or whatever you like), and you can apply that template to as many target sites as you would like.</span></span>

<span data-ttu-id="96536-118">Wenn es interessant... Lesen Sie weiter, und lassen Sie uns hier erfahren Sie, wie es!</span><span class="sxs-lookup"><span data-stu-id="96536-118">If it sounds interesting... keep reading, and let’s learn how to do it!</span></span>

<span data-ttu-id="96536-119"><a name="creatingtemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-119"></span></span>
## <a name="creating-a-provisioning-template"></a><span data-ttu-id="96536-120">Erstellen einer Bereitstellung Vorlage</span><span class="sxs-lookup"><span data-stu-id="96536-120">Creating a Provisioning Template</span></span>

<span data-ttu-id="96536-121">Wie bereits erwähnt, die einfachste Möglichkeit zum Erstellen einer benutzerdefinierten Vorlage für die Bereitstellung wird zum Erstellen einer neuen Websitesammlung aktuell in Microsoft SharePoint Online, konfigurieren die Artefakte (zusammengesetzt aussehen, Websitespalten, Inhaltstypen, Listen Instanzen, Seiten, Dateien usw.) und zu Speichern Sie das Ergebnis als Vorlage bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="96536-121">As already stated, the easiest way to create a custom provisioning template is to create a fresh new site collection in Microsoft SharePoint Online, configure your artifacts (Composed Look, Site Columns, Content Types, Lists Instances, Pages, Files, etc.) and to save the result as a Provisioning Template.</span></span>

<span data-ttu-id="96536-122">Folglich angenommen, Sie haben eine Beispiel-Website mit einem benutzerdefinierten definiert (benutzerdefinierten Farbdesigns, benutzerdefiniertes Logo, benutzerdefinierten Hintergrundbilds) suchen.</span><span class="sxs-lookup"><span data-stu-id="96536-122">Thus, let's say you have defined a sample site with a custom look (custom color theme, custom logo, custom background image).</span></span> <span data-ttu-id="96536-123">Sie können die resultierende Homepage in der folgenden Abbildung sehen.</span><span class="sxs-lookup"><span data-stu-id="96536-123">You can see the resulting Home Page in the following figure.</span></span>

![Die Homepage einer Website Vorlage](./media/Introducing-the-PnP-Provisioning-Engine/Figure-1-SiteTemplate01.png)

<span data-ttu-id="96536-125">Darüber hinaus haben Sie eine Reihe von Websitespalten, eines Inhaltstyps und einer Bibliothek Rechnungen mit einer benutzerdefinierten Ansicht definiert.</span><span class="sxs-lookup"><span data-stu-id="96536-125">Moreover, you have defined a couple of Site Columns, a Content Type and a Library of Invoices with a custom View.</span></span> <span data-ttu-id="96536-126">In den folgenden beiden Abbildungen sehen Sie das Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="96536-126">In the two following figures you can see the result.</span></span>

![Eine Bibliothek mit Rechnungen mit eines benutzerdefinierten Inhaltstyps](./media/Introducing-the-PnP-Provisioning-Engine/Figure-2-SiteTemplate02.png)

![Der Einstellungsseite der Bibliothek Rechnungen](./media/Introducing-the-PnP-Provisioning-Engine/Figure-3-SiteTemplate03.png)

<span data-ttu-id="96536-129">Um diese Website als Vorlage Provisioning exportieren möchten, können Sie entweder PowerShell (Dank die Arbeit von [Erwin](https://twitter.com/erwinvanhunen)!) oder CSOM-Code mit einigen Erweiterungsmethoden verwenden die von der OfficeDev Plug & Play-Hauptbibliothek bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="96536-129">In order to export that site as a Provisioning Template, you can either use PowerShell (thanks to the efforts of [Erwin](https://twitter.com/erwinvanhunen)!) or CSOM code, with some extension methods, which are provided by the OfficeDev PnP Core Library.</span></span> 

<span data-ttu-id="96536-130">Um die PowerShell-Erweiterungen verwenden, können Sie einfach auf die richtige URL ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) für Microsoft SharePoint Online) oder [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) für Microsoft SharePoint 2013 durchsuchen, und installieren Sie die OfficeDev Plug & Play-Kern-PowerShell-Erweiterungen.</span><span class="sxs-lookup"><span data-stu-id="96536-130">In order to use the PowerShell extensions, you can simply browse to the proper URL ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) for Microsoft SharePoint Online, or [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) for Microsoft SharePoint 2013) and install the OfficeDev PnP Core PowerShell extensions.</span></span> <span data-ttu-id="96536-131">Nachdem Sie der PowerShell-Umgebung mit Microsoft Office 365 mit dem Cmdlet *Connect-SPOnline* verbunden haben, können Sie das folgende PowerShell-Cmdlet verwenden können:</span><span class="sxs-lookup"><span data-stu-id="96536-131">After you have connected your PowerShell environment to Microsoft Office 365, by using the *Connect-SPOnline* cmdlet, you will be able to use the following PowerShell cmdlet:</span></span>

<span data-ttu-id="96536-132">*Get-SPOProvisioningTemplate-, "PnP-Provisioning-File.xml"*</span><span class="sxs-lookup"><span data-stu-id="96536-132">*Get-SPOProvisioningTemplate -Out "PnP-Provisioning-File.xml"*</span></span>

<span data-ttu-id="96536-133">Die *– Out* Argument weist das Cmdlet Informationen dazu, wo die Bereitstellung Vorlage zu speichern.</span><span class="sxs-lookup"><span data-stu-id="96536-133">The *–Out* argument instructs the cmdlet about where to save the Provisioning Template.</span></span>

<span data-ttu-id="96536-134">Auf der anderen Seite, um die CSOM-Erweiterungen verwenden können Sie einfach erstellen beliebigen (Windows-Konsole SharePoint Add-in, was Sie wollen) des .NET Softwareprojekts, und fügen die OfficeDev Plug & Play-NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="96536-134">On the other side, in order to use the CSOM extensions, you can simply create any kind (Console, Windows, SharePoint Add-in, whatever you like) of .NET software project, and add the OfficeDev PnP NuGet Package.</span></span> <span data-ttu-id="96536-135">NuGet-Paket ist in zwei Varianten verfügbar: OfficeDev Plug & Play-Core V15, dem Microsoft SharePoint 2013 lokal bezieht, und OfficeDev Plug & Play-Core, die Microsoft SharePoint Online beruht.</span><span class="sxs-lookup"><span data-stu-id="96536-135">The NuGet Package is available in two flavors: OfficeDev PnP Core V15, which targets Microsoft SharePoint 2013 on-premises, and OfficeDev PnP Core, which targets Microsoft SharePoint Online.</span></span>

<span data-ttu-id="96536-136">Ziel: wir Microsoft SharePoint Online, die mehr getestet wurde, und die wichtigsten als Ziel für die Arbeit Plug & Play-Kern-Team.</span><span class="sxs-lookup"><span data-stu-id="96536-136">Let's target Microsoft SharePoint Online, which has been tested more, and is the main target of the PnP Core Team efforts.</span></span> <span data-ttu-id="96536-137">Sie müssen nur eine Verbindung mit Microsoft Office 365, erstellen eine Instanz des *ClientContext* und rufen Sie einen Verweis auf ein *Web* -Objekt.</span><span class="sxs-lookup"><span data-stu-id="96536-137">You will simply need to connect to Microsoft Office 365, create a *ClientContext* instance and retrieve a reference to a *Web* object.</span></span> <span data-ttu-id="96536-138">Dank einer neuen Erweiterungsmethode namens *GetProvisioningTemplate*können Sie ein *ProvisioningTemplate* -Objekt abrufen, die mit einer Vorlage Provider und eine Serialisierung mit gespeichert werden kann.</span><span class="sxs-lookup"><span data-stu-id="96536-138">Thanks to a new extension method, called *GetProvisioningTemplate*, you will be able to retrieve a *ProvisioningTemplate* object that can be saved using a template provider and a serialization formatter.</span></span> <span data-ttu-id="96536-139">Die Vorlagenanbieter und die Serialisierung mit-Objekte können angepasst werden, sodass Sie unabhängig Persistenz Speicher- und Serialisierung Sie formatieren implementieren können.</span><span class="sxs-lookup"><span data-stu-id="96536-139">Both the template provider and the serialization formatter objects can be customized, so that you can implement whatever persistence storage and serialization format you like.</span></span> <span data-ttu-id="96536-140">Sofort einsetzbar bietet das Plug & Play-Bereitstellung Modul Unterstützung für Anbieter von Vorlagen Dateisystem, SharePoint und Azure BLOB-Speicher sowie für XML und JSON Serialisierungsformatierer.</span><span class="sxs-lookup"><span data-stu-id="96536-140">Out of the box, the PnP Provisioning Engine provides support for File System, SharePoint, and Azure Blob Storage template providers, as well as for XML and JSON serialization formatters.</span></span> <span data-ttu-id="96536-141">In der folgenden Abbildung (haben, [Vesa](https://twitter.com/vesajuvonen)) sehen Sie einen Überblick über die allgemeine Architektur des Plug & Play-Provisioning-Datenbankmoduls.</span><span class="sxs-lookup"><span data-stu-id="96536-141">In the following figure (credits to [Vesa](https://twitter.com/vesajuvonen)) you can see an outline of the overall architecture of the PnP Provisioning Engine.</span></span>

![Die Architektur von Plug & Play-Bereitstellung Engine-Framework](./media/Introducing-the-PnP-Provisioning-Engine/Figure-4-PnP-Provisioning-Framework-Outline.png)

<span data-ttu-id="96536-143">Das Ergebnis der extrahieren und Speichern einer *ProvisioningTemplate* Instanz-Objekts werden beispielsweise eine XML-Datei wie im folgenden Auszug XML-Code dargestellt:</span><span class="sxs-lookup"><span data-stu-id="96536-143">The result of extracting and saving a *ProvisioningTemplate* instance object will be for instance an XML file like the one shown in the following XML code excerpt:</span></span>
    
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
    

<span data-ttu-id="96536-144">Wie Sie sehen können, sind die XML-Elemente verständlich.</span><span class="sxs-lookup"><span data-stu-id="96536-144">As you can see, the XML elements are fairly self-explanatory.</span></span> <span data-ttu-id="96536-145">Das im Beispiel verwendete XML-Schema verweist auf die 201505 Version des Schemas Plug & Play-Bereitstellung (XML-Namespace: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), die zusammen mit der OfficeDev Plug & Play-Gemeinschaft definiert wurde und die finden Sie auf GitHub über die folgende URL: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/).</span><span class="sxs-lookup"><span data-stu-id="96536-145">The XML schema used in the example references the 201505 version of the PnP Provisioning Schema (XML Namespace: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), which has been defined together with the OfficeDev PnP Community, and which can be found on GitHub at the following URL: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/).</span></span> <span data-ttu-id="96536-146">In demselben Repository finden Sie auch ein Abzugsverteilung(en) (MD) automatisch generierten Dokument die beschreibt die Hauptelemente, Typen und Attribute, die eine Bereitstellung XML-Vorlage manuell zu definieren.</span><span class="sxs-lookup"><span data-stu-id="96536-146">Within the same repository, you will also find a markdown (MD) auto-generated document, which describes the main elements, types, and attributes available to manually define an XML provisioning template.</span></span>

<span data-ttu-id="96536-147">Die wirkliche Stärke dieses provisioning Modul ist jedoch die Verfügbarkeit von einem allgemeinen, Serialisierungsformat, unabhängig von der Domänenmodell ist.</span><span class="sxs-lookup"><span data-stu-id="96536-147">However, the real power of this provisioning engine is the availability of a high-level, serialization format that is independent of the Domain Model.</span></span> <span data-ttu-id="96536-148">Tatsächlich intern das Plug & Play-Bereitstellung Modul vollständig aus beliebigen Serialisierungsformat abgekoppelt und das gesamte Modul einfach Instanzen des Typs *ProvisioningTemplate* behandelt.</span><span class="sxs-lookup"><span data-stu-id="96536-148">In fact, internally the PnP Provisioning Engine is completely decoupled from any kind of serialization format, and the whole engine simply handles instances of the *ProvisioningTemplate* type.</span></span> <span data-ttu-id="96536-149">In der folgenden Abbildung können Sie beispielsweise das "Schnellansicht" Fenster von Microsoft Visual Studio 2013 zeigt eine Objektinstanz ProvisioningTemplate angezeigt.</span><span class="sxs-lookup"><span data-stu-id="96536-149">For instance, in the following figure you can see the "Quick Watch" window of Microsoft Visual Studio 2013 showing a ProvisioningTemplate object instance.</span></span>

![Die Struktur - innerhalb einer Debugger Watch - eines ProvisioningTemplate-Objekts](./media/Introducing-the-PnP-Provisioning-Engine/Figure-5-Domain-Model.png)

<span data-ttu-id="96536-151">Es ist zum Schluss kommen die *ProvisioningTemplate* manuell definieren mithilfe einer Modellsite oder durch Erstellen eines XML-Dokuments, das anhand des Plug & Play-Bereitstellung XSD-Schemas überprüft oder indem Sie einfach .NET Code schreiben und erstellen die Hierarchie der Objekte.</span><span class="sxs-lookup"><span data-stu-id="96536-151">It is up to you to define the *ProvisioningTemplate* manually, using a model site, or by composing an XML document that validates against the PnP Provisioning XSD Schema, or by simply writing .NET code and constructing the hierarchy of objects.</span></span> <span data-ttu-id="96536-152">Auch möglich, eine Kombination dieser Ansätze: Sie die Bereitstellung mit einer Modellsite Vorlage entwerfen, in eine XML-Datei zu speichern, tun können und einige Anpassungen in-Memory während der Bearbeitung der *ProvisioningTemplate* -Instanz in Ihrem Code.</span><span class="sxs-lookup"><span data-stu-id="96536-152">You can even do a mix of these approaches: you can design the provisioning template using a model site, save it into an XML file, and do some in-memory customizations, while handling the *ProvisioningTemplate* instance in your code.</span></span>

<span data-ttu-id="96536-153"><a name="applyingtemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-153"></span></span>
## <a name="applying-a-provisioning-template"></a><span data-ttu-id="96536-154">Anwenden einer Bereitstellung Vorlage</span><span class="sxs-lookup"><span data-stu-id="96536-154">Applying a Provisioning Template</span></span>

<span data-ttu-id="96536-155">Nun, was haben eine Vorlage Bereitstellung ist und wie die Domänenmodell extrahieren-Objekt aus einer vorhandenen Website, sind Sie bereit, in eine Zielwebsite zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="96536-155">Now that you have seen what a Provisioning Template is, and how to extract the Domain Model object from an existing site, you are ready to apply it to a target site.</span></span> <span data-ttu-id="96536-156">Nehmen wir an, dass Sie eine andere frische neue Websitesammlung in Microsoft SharePoint Online verfügen, die mit der Vorlage Teamwebsite, wie er in der folgenden Abbildung dargestellt ist erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="96536-156">Let's say that you have another fresh new Site Collection in Microsoft SharePoint Online that has been created using the Team Site template, like it is shown in the following figure.</span></span>
 
![SharePoint Online-Seite für die Erstellung einer neuen Websitesammlung](./media/Introducing-the-PnP-Provisioning-Engine/Figure-6-Target-Site-Creation.png)

<span data-ttu-id="96536-158">Standardmäßig wird die Website wie in der folgenden Abbildung aussehen, das Standardlayout einer SharePoint Online-Website ist.</span><span class="sxs-lookup"><span data-stu-id="96536-158">By default, the site will look like the following figure, which is the default layout of a SharePoint Online site.</span></span>

![Die Homepage einer aktuell neuer Zielwert](./media/Introducing-the-PnP-Provisioning-Engine/Figure-7-Target-Site-Created.png)

<span data-ttu-id="96536-160">Sie können nun durch den Einsatz von PowerShell oder indem Sie .NET Code schreiben ein benutzerdefiniertes *ProvisioningTemplate* Instanz Objekts anwenden.</span><span class="sxs-lookup"><span data-stu-id="96536-160">You can now apply a custom *ProvisioningTemplate* instance object either by utilizing PowerShell, or by writing .NET code.</span></span> <span data-ttu-id="96536-161">Wenn Sie PowerShell verwenden möchten, zeigt der folgende Auszug aus, wie das *Anwenden-SPOProvisioningTemplate* -Cmdlet verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="96536-161">If you want to use PowerShell, the following excerpt shows how you can utilize the *Apply-SPOProvisioningTemplate* cmdlet.</span></span>

<span data-ttu-id="96536-162">*Anwenden von SPOProvisioningTemplate-Pfad "PnP-Provisioning-File.xml"*</span><span class="sxs-lookup"><span data-stu-id="96536-162">*Apply-SPOProvisioningTemplate -Path "PnP-Provisioning-File.xml"*</span></span>

<span data-ttu-id="96536-163">Die *– Pfad* -Argument verweist auf die Quelldatei für die Vorlage, die das Cmdlet zu der aktuell verbundenen Website (durch das Cmdlet *Connect-SPOnline* impliziert) automatisch angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="96536-163">The *–Path* argument refers to the source template file, which the cmdlet will automatically apply to the currently connected site (implied by the *Connect-SPOnline* cmdlet).</span></span> <span data-ttu-id="96536-164">In der folgenden Abbildung sehen Sie das letzte Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="96536-164">In the following figure you can see the final result.</span></span>

![Die Homepage einer Ziel-Website basierend auf einer Bereitstellung mit Vorlagen](./media/Introducing-the-PnP-Provisioning-Engine/Figure-8-Target-Site-Provisioned.png)

<span data-ttu-id="96536-166">Wie Sie sehen können, die Website ist dasselbe aussehen wie die ursprüngliche Vorlage und die Rechnungen-Bibliothek mit allen der gleichen zugrunde liegenden Struktur und-Konfiguration (Websitespalten, Inhaltstypen usw.) enthält.</span><span class="sxs-lookup"><span data-stu-id="96536-166">As you can see, the site has the same look as the original template, and it includes the Invoices library, with all of the same underlying structure and configuration (Site Columns, Content Types, etc.).</span></span>

<span data-ttu-id="96536-167">Was geschieht mit .NET Code?</span><span class="sxs-lookup"><span data-stu-id="96536-167">What about using .NET code?</span></span> <span data-ttu-id="96536-168">Hier ist ein Auszug zum CSOM und die OfficeDev Plug & Play-Hauptbibliothek Erweiterungsmethoden verwenden, um die Vorlage anwenden.</span><span class="sxs-lookup"><span data-stu-id="96536-168">Here is an excerpt on how to use CSOM and the OfficeDev PnP Core Library extension methods to apply the template.</span></span>

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
    
<span data-ttu-id="96536-169">Zum Starten, müssen Sie eine Instanz eines Objekts Vorlagenanbieter, je nachdem, welche Art von Permanenz verwendet zum Speichern und Laden Sie die Vorlage erstellen.</span><span class="sxs-lookup"><span data-stu-id="96536-169">To start, you need to create an instance of a Template Provider object, depending on what kind of persistence you will use to save and load the template.</span></span>  <span data-ttu-id="96536-170">Im nächsten Schritt laden Sie die Vorlage aus dem Repository Quelle mithilfe der *GetTemplate* -Methode.</span><span class="sxs-lookup"><span data-stu-id="96536-170">Next, you load the template from the source repository, by using the *GetTemplate* method.</span></span> <span data-ttu-id="96536-171">Schließlich wenden die Vorlage auf der Zielwebsite Sie mit der Erweiterung *ApplyProvisioningTemplate* -Methode des Typs Web.</span><span class="sxs-lookup"><span data-stu-id="96536-171">Lastly, you will apply the template to the target site, using the *ApplyProvisioningTemplate* extension method of the Web type.</span></span>

<span data-ttu-id="96536-172">Durchschnittlich dauert die Bibliothek ein paar Minuten, wenden Sie die Vorlage, unabhängig davon, ob Sie PowerShell oder .NET Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="96536-172">On average, the library will take a couple of minutes to apply the template, regardless of whether you are utilizing PowerShell or .NET code.</span></span> <span data-ttu-id="96536-173">Bei Bedarf können Sie registrieren ein Stellvertreters für den Gesamtprozess überwachen, während der Bereitstellung ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="96536-173">If desired, you can register a delegate to monitor the overall process, while the provisioning is in progress.</span></span> <span data-ttu-id="96536-174">Wir sind noch verbessern Leistungsmerkmalen des Moduls und bisher haben haben wir uns unsere Aufmerksamkeit Funktionen und Funktionen.</span><span class="sxs-lookup"><span data-stu-id="96536-174">We are still improving performances of the engine, and so far we have focused our attention on capabilities and functionalities.</span></span>

<span data-ttu-id="96536-175"><a name="advancedtopics"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-175"></span></span>
## <a name="advanced-topics"></a><span data-ttu-id="96536-176">Weiterführende Themen</span><span class="sxs-lookup"><span data-stu-id="96536-176">Advanced Topics</span></span>

<span data-ttu-id="96536-177">Dies ist nur ein einführende Artikel in naher Zukunft tiefer, um einige erweiterten Themen laufend wird.</span><span class="sxs-lookup"><span data-stu-id="96536-177">This is just an introductory article, as in the near future we will go deeper around some more advanced topics.</span></span> <span data-ttu-id="96536-178">Dennoch ist es wichtig zu verstehen, dass die neue Plug & Play-Bereitstellung Engine verwenden, Sie können auch Taxonomien bereitstellen als auch mithilfe von Variablen und Token, das zur Laufzeit, basierend auf was Sie bereitstellen werden ersetzt werden können (Liste-IDs, Parameter, Begriff IDs usw.).</span><span class="sxs-lookup"><span data-stu-id="96536-178">Nevertheless, it is important to understand that using the new PnP Provisioning Engine, you can also provision Taxonomies, as well as use variables and tokens, which can be replaced at runtime, based on what you are provisioning (List IDs, Parameters, Term IDs, etc.).</span></span> <span data-ttu-id="96536-179">Sie können die Bereitstellung Engine aus den Timer-Job-Dienste, vom Anbieter gehosteten-add-ins, externen Websites und aufrufen.</span><span class="sxs-lookup"><span data-stu-id="96536-179">You can invoke the provisioning engine from timer job services, provider-hosted add-ins, external sites, and more.</span></span> <span data-ttu-id="96536-180">Das Plug & Play-Modul Bereitstellung können Sie schließlich Artefakte von Test/Staging-Umgebungen produktionsumgebungen verschieben.</span><span class="sxs-lookup"><span data-stu-id="96536-180">Lastly, you can use the PnP Provisioning Engine to move artifacts from test/staging environments to production environments.</span></span>

<span data-ttu-id="96536-181">Darüber hinaus auf Channel 9 ist ein [Abschnitt für Plug & Play-OfficeDev](http://aka.ms/OfficeDevPnPVideos), in dem Sie einige Videos über die Plug & Play-Bereitstellung Engine und die Plug & Play-PowerShell-Erweiterungen überwachen können:</span><span class="sxs-lookup"><span data-stu-id="96536-181">Moreover, on Channel 9 there is a [section dedicated to OfficeDev PnP](http://aka.ms/OfficeDevPnPVideos), where you can watch some videos about the PnP Provisioning Engine and the PnP PowerShell Extensions:</span></span>

- [<span data-ttu-id="96536-182">Erste Schritte mit Plug & Play-Bereitstellung Engine</span><span class="sxs-lookup"><span data-stu-id="96536-182">Getting Started with PnP Provisioning Engine</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine)
- [<span data-ttu-id="96536-183">Betrachtung der Sequenzierung Plug & Play-Bereitstellung Engine-Schema</span><span class="sxs-lookup"><span data-stu-id="96536-183">Deep dive to PnP provisioning engine schema</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
- [<span data-ttu-id="96536-184">Einführung in die PowerShell-Cmdlets PnP</span><span class="sxs-lookup"><span data-stu-id="96536-184">Introduction to PnP PowerShell Cmdlets</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)

<span data-ttu-id="96536-185"><a name="wrapup"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-185"></span></span>
## <a name="requirements-and-wrap-up"></a><span data-ttu-id="96536-186">Anforderungen und – Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="96536-186">Requirements and Wrap Up</span></span> ##

<span data-ttu-id="96536-187">Um mit der Plug & Play-Bereitstellung Engine lokalen wiedergegeben werden sollen, benötigen Sie mindestens die SharePoint 2013 März 2015 kumulative Update installiert haben, wie das Modul nutzt einige [neue Funktionen](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) von der clientseitigen Objektmodell, die nicht verfügbar sind frühere Versionen des Produkts.</span><span class="sxs-lookup"><span data-stu-id="96536-187">In order to play with the PnP Provisioning Engine on-premises, you need to have at least the SharePoint 2013 March 2015 Cumulative Update installed, as the engine leverages some [new capabilities](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) of the Client Side Object Model, which are not available in previous versions of the product.</span></span> <span data-ttu-id="96536-188">Wenn Sie auf Microsoft SharePoint Online abzielen, sind die Anforderungen automatisch Dank der Software als Dienstmodell erfüllt.</span><span class="sxs-lookup"><span data-stu-id="96536-188">If you target Microsoft SharePoint Online, the requirements are automatically satisfied thanks to the Software as a Service model.</span></span>

<span data-ttu-id="96536-189">Geben Sie mit der Plug & Play-Bereitstellung Engine wiedergegeben werden sollen Sie, geben Sie uns Feedback und genießen Sie die Zukunft der SharePoint-Add-in-Modell und remote-Bereitstellung!</span><span class="sxs-lookup"><span data-stu-id="96536-189">Please, play with the PnP Provisioning Engine, give us feedback, and enjoy the future of the SharePoint Add-in Model and remote provisioning!</span></span>

<span data-ttu-id="96536-190"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="96536-190"></span></span>
## <a name="see-also"></a><span data-ttu-id="96536-191">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="96536-191">See also</span></span>

-  [<span data-ttu-id="96536-192">Office 365 Development Patterns & Practices auf GitHub</span><span class="sxs-lookup"><span data-stu-id="96536-192">Office 365 Development Patterns & Practices on GitHub</span></span>](https://github.com/SharePoint/PnP/)
-  <span data-ttu-id="96536-193">[SharePoint-Gruppe der Entwickler](http://aka.ms/sppnp-community) bei Microsoft Tech-Community</span><span class="sxs-lookup"><span data-stu-id="96536-193">[SharePoint Developer Group](http://aka.ms/sppnp-community) at Microsoft Tech Community</span></span>
