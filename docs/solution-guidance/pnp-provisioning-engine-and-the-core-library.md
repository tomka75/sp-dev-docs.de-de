---
title: Plug & Play-Bereitstellung Modul- und die Core-Bibliothek
ms.date: 11/03/2017
ms.openlocfilehash: 274c9796be400d3ae305358ff93d9dd6d28fa8bf
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="pnp-provisioning-engine-and-the-core-library"></a>Plug & Play-Bereitstellung Modul- und die Core-Bibliothek

Betrachten Sie allgemeine remote Bereitstellungsprozess, einschließlich eine nähere Betrachtung der OfficeDevPnP.Core-Bibliothek.

Das Plug & Play-Bereitstellung Modul ist das Herzstück von provisioning Framework und auf Grundlage ist die OfficeDevPnP.Core-Bibliothek. Das provisioning Modul ist Bestandteil der Hauptbibliothek und sie die zentrale Bibliothek Erweiterungen in der Implementierung von Bereitstellungsaufgaben nutzt. Erweiterungsmethoden auf dem SharePoint-CSOM/REST-Objektmodell umfasst, ermöglicht der Hauptbibliothek provisioning Aufgaben wie das Aufzählen von und erste Bereitstellung Vorlagen als auch speichern und Anwenden von Vorlagen klicken Sie dann auf neuer und vorhandener Websites. Darüber hinaus können Sie Bereitstellungsaufgaben automatisieren und codierten Logik in Ihrer Bereitstellung Routinen einführen.

**Hinweis:**  Um ein video Exemplarische Vorgehensweise zum Erstellen und Speichern von Anwenden einer Bereitstellung Vorlage anzuzeigen, wechseln Sie zu [Erste Schritte mit Plug & Play-Bereitstellung Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).

## <a name="pnp-provisioning-engine"></a>Plug & Play-Modul für die Bereitstellung

Das Plug & Play-Bereitstellung Modul ist die strukturierte Implementierung der Klassen in der Hauptbibliothek in durchführen und automatisieren remote Bereitstellungsaufgaben. In der neuen Microsoft Querformat dieser Features der SharePoint-Add-in-Objektmodell, Bereitstellung von Lösungen für SharePoint Online, SharePoint 2013 und Office 365 jetzt verwenden Sie das Clientobjektmodell (CSOM) und die Bereitstellung Framework websiteartefakte bereit.

Die Plug & Play-Bereitstellung Engine können Sie den Entwurf von Websitespalten, Inhaltstypen, Listendefinitionen, zusammengesetzten und Seiten modellieren. Sie können diese Features und vieles mehr von Verweisen auf vorhandene Website zur Verfügung, durch das Design erstellen Meine Hand oder eine Mischung aus beiden Ansätze mit entwerfen. Sie können dann optional können Sie den Entwurf als provisioning Vorlage beibehalten, die Sie speichern und wiederverwenden können.

Sie können zwei Ansätze Extrahieren von Ihrer Website entwerfen als provisioning Vorlage verwenden. Verwenden Sie CSOM/REST-Code, bereitgestellte von der Hauptbibliothek (OfficeDevPnP.Core) oder mithilfe von Windows PowerShell-Skripts (SharePointPnP.PowerShell) Erweiterungsmethoden implementiert.

### <a name="using-windows-powershell-scripting-to-extract-a-provisioning-template"></a>Mithilfe von Windows PowerShell-Skripts zum Extrahieren einer Bereitstellung Vorlage

Für die Verwendung der Windows PowerShell-Skripts mit der Bereitstellung Engine müssen Sie zuerst heruntergeladen und installiert die Plug & Play-PowerShell-Cmdlets. Alles, was Sie zum Ausführen von Windows PowerShell benötigen, einschließlich Download und Anleitungen für die Installation sowie der Windows PowerShell-Befehl-Dokumentation ist im Repository [SharePointPnP.PowerShell Befehle](https://github.com/SharePoint/PnP-PowerShell) auf GitHub verfügbar.

**Hinweis:**  Das Repository SharePointPnP.PowerShell Befehle enthält drei Versionen von Windows PowerShell-Befehle MSI-Datei. Zwei sind für lokale (einer für SharePoint 2013) und für SharePoint 2016 verwenden, und die dritte für SharePoint Online ist.

Das Repository SharePointPnP.PowerShell Befehle enthält, mit denen Sie einer Bibliothek mit Windows PowerShell-Befehle, die auf SharePoint Online abzielen erstellen können. Die Befehle CSOM verwenden können und für beide SharePoint Online und lokalem SharePoint, Sie je nach der MSI-Paket installieren.

Außerdem ist ein kurzes [Channel 9](https://channel9.msdn.com/) -Video&mdash;Einführung in die [Plug & Play-PowerShell-Cmdlets](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)&mdash;, die Installation des Windows PowerShell-Pakets und Herstellen einer Verbindung mit Office 365-Website erläutert. Neben der Installation und Verbindung Aktivitäten behandelt das Video andere wichtige Informationen zur Verwendung von Windows PowerShell remote-Bereitstellung.

### <a name="using-csom-code-to-extract-a-provisioning-template"></a>Verwendung von CSOM-Code zum Extrahieren von einer Bereitstellung Vorlage

Um CSOM/REST-Code zum Extrahieren von einer Bereitstellung Vorlage einsetzen möchten, erstellen Sie einfach ein Entwicklungsprojekt mithilfe von Visual Studio oder einer anderen Entwicklungsumgebung. Erstellen Sie jede Art von Projekt&mdash;beispielsweise eine Konsole oder Windows-Anwendung oder ein SharePoint-Add-in. Nachdem Sie ein Entwicklungsprojekt erstellt haben, müssen Sie der Hauptbibliothek Installieren der als ein NuGet-Paket verfügbar ist.

**Hinweis:**  Anweisungen zum Suchen und installieren die zentrale Bibliothek NuGet-Paket und eine exemplarische Vorgehensweise für eine Bereitstellung Beispiel Konsole Remoteanwendung, stehen in [Provisioning Console Application Sample](provisioning-console-application-sample.md). Beachten Sie, dass der Hauptbibliothek in zwei Versionen stammen: eine beruht auf SharePoint Online, SharePoint 2013 und Office 365; und eine SharePoint 2013 lokal beruht.

Ausführliche Informationen zur Verwendung von CSOM in der [Bereitstellung Console Application Beispiel](provisioning-console-application-sample.md)sind, ist die allgemeine Übersicht über die wie folgt:

1. Erstellen einer Verbindung mit Office 365.
    
2. Erstellen einer **ClientContext** -Instanz, und rufen Sie einen Verweis auf ein **Web** -Objekt.
    
3. Verwenden Sie die Core-Bibliothek Erweiterungsmethode, **GetProvisioningTemplate**, um ein **ProvisioningTemplate** -Objekt zu extrahieren.
    
4. Speichern Sie die Bereitstellung Vorlageninstanz mit einem Speicherort Ihrer Wahl mithilfe einer Vorlage Anbieter und Serialisierung mit.
    
    **Hinweis:**  Da der Vorlagenanbieter und die Serialisierung mit Objekte angepasst werden können, können Sie jegliches Persistenz Speicher- und Serialisierung Sie formatieren implementieren. Out-of-the-Box, unterstützt die Plug & Play-Bereitstellung Engine Dateisystem, SharePoint und Azure BLOB-Speicheranbieter-Vorlage. Es unterstützt auch XML und JSON Serialisierungsformatierer.

Sie können finden Sie ein Beispiel für die XML-Ausgabe Serialisierung und erfahren Sie mehr über die XML-Serialisierungsschema im Artikel [Plug & Play-Bereitstellung Schema](pnp-provisioning-schema.md) . Auch zu können abrufen, das Schema und die zugehörige Dokumentation GitHub:[SharePoint/PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema/). Außerdem ist ein [Channel 9](https://channel9.msdn.com/) -Video&mdash;[tief die kurz-Plug & Play-Bereitstellung Engine Schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)&mdash;, die stellt und erläutert das Schema.

Es ist wichtig, jedoch beachten Sie, dass die Bereitstellung Engine eine Serialisierung Format unabhängigen Domänenmodell unterstützt. Tatsächlich ist das provisioning Modul vollständig entkoppelte aus einem beliebigen Serialisierungsformat. Es ist zum Schluss kommen die Instanz **ProvisioningTemplate** manuell zu definieren. Entweder zeigen Sie auf einer Modellsite oder Verfassen Sie ein XML-Dokument, das anhand des Plug & Play-Bereitstellung Schemas überprüft oder Schreiben Sie .NET Code und erstellen Sie die Hierarchie der Objekte zu. Sie können sogar Ansätze verwenden. Sie können auch die Bereitstellung Entwurfsvorlage mithilfe einer Modellsite, und klicken Sie dann in eine XML-Datei zu speichern tun und einige Anpassungen in-Memory während der Bearbeitung der **ProvisioningTemplate** -Instanz in Ihrem Code.

#### <a name="example-code-to-extract-a-template-using-getprovisioningtemplate"></a>Beispiel-Code zum Extrahieren von einer Vorlage mithilfe von GetProvisioningTemplate

Im Beispiel dargestellt im Artikel [Provisioning Console Application Beispiel](provisioning-console-application-sample.md) veranschaulicht die Verwendung von der **GetProvisioningTemplate** -Methode. Im Beispiel erfolgt beim Exportieren von der Bereitstellung Vorlage in den folgenden Codeblock.

```
ProvisioningTemplateCreationInformation ptci = new ProvisioningTemplateCreationInformation(ctx.Web);

// Create FileSystemConnector, so that we can store composed files somewhere temporarily 
ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
ptci.PersistComposedLookFiles = true;
ptci.ProgressDelegate = delegate (String message, Int32 progress, Int32 total)
{

// Use this to simply output progress to the console application UI
Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
};

// Execute actual extraction of the tepmplate
ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
```

### <a name="apply-the-provisioning-template"></a>Wenden Sie die Bereitstellung Vorlage

Wie mit die Bereitstellung Vorlage extrahieren, Sie Ihre benutzerdefinierte **ProvisioningTemplate** -Objektinstanz anwenden können mithilfe von CSOM/REST Code oder Windows PowerShell-Befehle. Sie können die [Befehle SharePointPnP.PowerShell](https://github.com/SharePoint/PnP-PowerShell) aus dem Repository auf GitHub herunterladen.

Wenn die Bereitstellung Vorlage mithilfe von der Hauptbibliothek Erweiterungsmethoden, müssen Sie hier einen Codeblock ähnlich dem Beispiel. Im Beispiel wird die Vorlage auf der Zielwebsite angewendet, mithilfe der **ApplyProvisioningTemplate** Erweiterung-Methode des Typs **Web** .

```
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
    "<template name>.xml");

  // Apply the template to another site
  Console.WriteLine("Start: {0:hh.mm.ss}", DateTime.Now);

  // We can also use Apply-PnPProvisioningTemplate
  web.ApplyProvisioningTemplate(template);

  Console.WriteLine("End: {0:hh.mm.ss}", DateTime.Now);
}
```

Nachdem Sie eine Verbindung mit SharePoint Online mit Windows PowerShell-Befehlen erstellt haben, verwenden Sie das Cmdlet **Übernehmen PnPProvisioningTemple** wie hier gezeigt.

```
Apply-PnProvisioningTemplate -Path "PnP-Provisioning-File.xml"
```

Beachten Sie, dass die `-Path` -Argument verweist auf den Dateipfad der Bereitstellung Vorlagendatei, die Sie auf das Dateisystem beibehalten. Im obigen Codeblock die gespeicherten Datei ist eine XML-Datei in einem beliebigen serialisierten Format, das Sie möchten diese Vorlagendateien beibehalten werden können.

## <a name="pnp-core-library"></a>Plug & Play-Core-Bibliothek

Die Core-Bibliothek (OfficeDevPnP.Core) ist ein CSOM/REST-Objektmodell, die das Plug & Play-Bereitstellung Framework unterstützt und aktiviert das Plug & Play-Bereitstellung Modul. Mehrere Namespaces, einschließlich einer Reihe von [Erweiterungsmethoden](https://msdn.microsoft.com/en-us/library/bb383977.aspx)besteht. Diese Methoden Erweitern des SharePoint-Objektmodells zur Unterstützung der remote-Bereitstellung sowie Objekte für die Behandlung von Entitäten, Zeitgeberaufträge, provisioning Vorlagen und die gesamte Bereitstellung Framework. In Tabelle 1 werden die Namespaces in der Hauptbibliothek aufgelistet.

**In Tabelle 1. Namespaces in der Bibliothek OfficeDevPnP.Core**

|**Namespace**|**Beschreibung**|
|:-----|:-----|
|OfficeDevPnP.Core||
|OfficeDevPnP.Core.AppModelExtensions|.NET Klassen, die einen vorhandenen Typ mit zusätzlichen Methoden zu erweitern.|
|OfficeDevPnP.Core.Entities|Klassen, die verwendet werden, um zu bieten und komplexe Objekte aus der Erweiterungsmethoden in AppModelExtensions abrufen.|
|OfficeDevPnP.Core.Enums|Eine Reihe von Enumerationen, die Bereitstellung Operationen unterstützen.|
|OfficeDevPnP.Core.Extensions|Erweiterungsmethoden, die nicht verbunden, beispielsweise Methoden, die bei Zeichenfolgen unterstützen SharePoint sind.|
|OfficeDevPnP.Core.Framework.ObjectHandlers.TokenDefinitions|Token verwendet, um bestimmte Websiteinhalt in der Template-Objekt zu ersetzen.|
|OfficeDevPnP.Core.Framework.Provisioning.Connectors|Connectors dienen zum unterschiedlichen Datenquellen verbinden, in dem Vorlagen und Objekte gespeichert werden.|
|OfficeDevPnP.Core.Framework.Provisioning.Extensibility|Erweiterbarkeit des Codes. Erweiterbarkeit des Providers können verwendet werden, um Funktionalität hinzuzufügen, das durch das Modul nicht nativ unterstützt wird.|
|OfficeDevPnP.Core.Framework.Provisioning.Model|Modell Datenobjekte Vorlage. Vorlagen sind entweder extrahiert oder Aufheben der tatsächlichen C#-Code serialisiert. Dieser Namespace enthält Klassen, die für diese Struktur.|
|OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers|Handler für andere SharePoint-Elemente, die Unterstützung von Vorlage Extraction und erstellen.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers|Namespace für Vorlagenanbieter Basiskalender. Anbieter von Vorlagen dienen zum Serialisierung und Deserialisierung codebasierte-Modelle, um ein bestimmtes Format.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Json|JSON-Vorlagenanbieter zum Serialisieren oder deserialisiert codebasierte Vorlagen oder von JSON-Format dar.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml|XML-Vorlagenanbieter zum Serialisieren oder deserialisiert codebasierte Vorlagen oder von XML-Format.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201503|Automatisch generierte Schemadateien für v201503 Version des Schemas.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201505|Automatisch generierte Schemadateien für v201505 Version des Schemas.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201508|Automatisch generierte Schemadateien für v201508 Version des Schemas.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Beispiel einer Anwendung in Konsole-Bereitstellung](provisioning-console-application-sample.md)
    
- [SharePointPnP.PowerShell Befehle](https://github.com/SharePoint/PnP-PowerShell)
    
- [Beispiel einer Anwendung in Konsole-Bereitstellung](provisioning-console-application-sample.md)
    
- [SharePoint/PnP-Provisioning-Schema](https://github.com/SharePoint/Pnp-Provisioning-Schema/)
    
- [Erweiterungsmethoden](https://msdn.microsoft.com/en-us/library/bb383977.aspx)
