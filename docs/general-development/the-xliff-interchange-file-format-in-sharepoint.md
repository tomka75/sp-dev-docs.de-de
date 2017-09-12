---
title: Das XLIFF-Interchange-Dateiformat in SharePoint
ms.prod: SHAREPOINT
ms.assetid: 660c0f07-7030-4576-957e-b9f2cd0fa895
ms.openlocfilehash: 4a0aeecc8323a6a1f24b6c09ca9f2fb99c4fdb40
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="the-xliff-interchange-file-format-in-sharepoint"></a><span data-ttu-id="dceab-102">Das XLIFF-Interchange-Dateiformat in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dceab-102">The XLIFF interchange file format in SharePoint</span></span>
<span data-ttu-id="dceab-103">Abrufen von Informationen über die SharePoint Implementierung der XLIFF-Austauschdateiformat, einschließlich Schema Referenzinformationen und ein Beispiel für XML.</span><span class="sxs-lookup"><span data-stu-id="dceab-103">Get information about the SharePoint implementation of the XLIFF interchange file format, including schema reference information and an XML example.</span></span>
## <a name="the-xliff-interchange-file-format-implementation-in-sharepoint"></a><span data-ttu-id="dceab-104">XLIFF Interchange File Format Implementierung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dceab-104">The XLIFF interchange file format implementation in SharePoint</span></span>

<span data-ttu-id="dceab-p101">SharePoint bietet Unterstützung von XML-Lokalisierung Interchange File Format (XLIFF) für das Variationsfeature und das Feature für die Übersetzungsdienste. SharePoint Server verwendet XLIFF aus SharePoint Server auf ein Übersetzer in einem Format, das der Übersetzer auf einfache Weise verstehen, welche zu Transportinformationen zu einer Datei und seinen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="dceab-p101">SharePoint provides XML Localization Interchange File Format (XLIFF) application support for the Variations feature and the Translation Services feature. SharePoint Server uses XLIFF to transport information about a file and its contents from SharePoint Server to a human translator in a format that the translator can easily understand.</span></span>
  
    
    
<span data-ttu-id="dceab-p102">SharePoint entspricht der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) von OASIS veröffentlicht werden, wenn SharePoint Server HTML-Seiten in XLIFF-Format extrahiert werden. Zur Verringerung der der Mischung der übersetzbare Elemente und Code-Elemente, die in XLIFF-Paketen angezeigt würden, würde eine unveränderte SharePoint Server CDATA Content übertragen werden, wird SharePoint übermittelt, die Möglichkeit, vollständig XLIFF-kompatiblen XLIFF-Dokumente zu erstellen, die auch gut SharePoint integriert sind. Beim Exportieren von XML-Dateien in XLIFF-Format aus `sharepointservernv`sind die Daten, die der Übersetzer empfängt clean und übersetzen bereit.</span><span class="sxs-lookup"><span data-stu-id="dceab-p102">SharePoint adheres to the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) published by OASIS when SharePoint Server HTML pages are extracted to XLIFF format. To eliminate the mix of translatable elements and code elements that would appear in XLIFF packages if unmodified SharePoint Server CDATA content were to be transported, SharePoint is delivered with the ability to produce fully XLIFF-compliant XLIFF documents that are also well-integrated with SharePoint. When exporting XML files in XLIFF format from `sharepointservernv`, the data that the human translator receives is clean and ready to translate.</span></span>
  
    
    
<span data-ttu-id="dceab-p103">In diesem Artikel Dokumente bestimmte SharePoint Server Implementierungen von XLIFF-Elementen und Attributen, die im Allgemeinen in XLIFF geöffneten standard Dokuments von OASIS veröffentlichte Version 1.2 definiert sind. Weitere Informationen zu bestimmten XLIFF-Elementen und Attributen finden Sie unter der  [XLIFF 1.2-Spezifikation](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel).</span><span class="sxs-lookup"><span data-stu-id="dceab-p103">This article documents specific SharePoint Server implementations of XLIFF elements and attributes that are defined more generally in version 1.2 of the XLIFF open standard document published by OASIS. For more information about specific XLIFF elements and attributes, see the  [XLIFF 1.2 Specification](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel).</span></span>
  
    
    

  
    
    

<span data-ttu-id="dceab-112">**In Tabelle 1. Wichtige XLIFF-Elemente und-Attribute in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="dceab-112">**Table 1. Notable XLIFF elements and attributes in SharePoint**</span></span>


|<span data-ttu-id="dceab-113">**Element**</span><span class="sxs-lookup"><span data-stu-id="dceab-113">**Element**</span></span>|<span data-ttu-id="dceab-114">**Attribute**</span><span class="sxs-lookup"><span data-stu-id="dceab-114">**Attributes**</span></span>|<span data-ttu-id="dceab-115">**Hinweise**</span><span class="sxs-lookup"><span data-stu-id="dceab-115">**Notes**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="dceab-116">XML</span><span class="sxs-lookup"><span data-stu-id="dceab-116">Xml</span></span>  <br/> | `version` <br/>  `encoding` <br/> |<span data-ttu-id="dceab-117">Deklarieren die XML-Version und die Codierung.</span><span class="sxs-lookup"><span data-stu-id="dceab-117">Declares the XML version and encoding.</span></span>  <br/> |
|<span data-ttu-id="dceab-118">XLIFF</span><span class="sxs-lookup"><span data-stu-id="dceab-118">Xliff</span></span>  <br/> | `version` <br/>  `xmlns` <br/> |<span data-ttu-id="dceab-119">Enthält das  `version` -Attribut und das Schema Validation Mechanismus.</span><span class="sxs-lookup"><span data-stu-id="dceab-119">Contains the  `version` attribute and the schema validation mechanism.</span></span> <br/> |
|<span data-ttu-id="dceab-120">Datei</span><span class="sxs-lookup"><span data-stu-id="dceab-120">File</span></span>  <br/> | `original` <br/>  `source-language` <br/>  `target-language` <br/>  `datatype` <br/>  `tool-id` <br/> |<span data-ttu-id="dceab-121">Entspricht der ursprünglichen Quelle-Datei, die in einseitiges GUID aus das Variationsfeature ist, enthält die Ausgangs- und Zielsprache ( `source-language` und `target-language`), die von maschinelle Übersetzung Tools und Human Translation Tools verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dceab-121">Corresponds to the original source file, which in is one page GUID from the Variations feature that includes the source and target languages ( `source-language` and `target-language`) that are used by both machine-translation tools and human-translation tools.</span></span>  <br/><span data-ttu-id="dceab-p104">Das  `original` -Attribut enthält eine GUID, die Inhalt der ursprünglichen Quelle identifiziert. Dieser Wert sollte zur Sicherstellung eines erfolgreichen Imports statisch bleiben.</span><span class="sxs-lookup"><span data-stu-id="dceab-p104"> The  `original` attribute contains a GUID that is used to identify the original source content. This value should remain static to help ensure a successful import. </span></span><br/> <span data-ttu-id="dceab-124">Das  `datatype` -Attribut wird auch im **File** -Element im HTML-Format für alle SharePoint-Seiten gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dceab-124">The  `datatype` attribute is also stored in the **File** element in HTML format for all SharePoint pages.</span></span> <br/> <span data-ttu-id="dceab-125">Das Attribut  `tool-id` ist die GUID, die das Tool identifiziert, das die XLIFF-Datei generiert.</span><span class="sxs-lookup"><span data-stu-id="dceab-125">The  `tool-id` attribute is the GUID that identifies the tool that generated the XLIFF file.</span></span> <br/> |
|<span data-ttu-id="dceab-126">Kopfzeile</span><span class="sxs-lookup"><span data-stu-id="dceab-126">Header</span></span>  <br/> |||
|<span data-ttu-id="dceab-127">Tool</span><span class="sxs-lookup"><span data-stu-id="dceab-127">Tool</span></span>  <br/> | `tool-id` <br/>  `tool-name` <br/> |<span data-ttu-id="dceab-128">Gibt an, mit die XLIFF-Datei generiert wurde.</span><span class="sxs-lookup"><span data-stu-id="dceab-128">Identifies the tool that generated the XLIFF file.</span></span>  <br/> |
|<span data-ttu-id="dceab-129">Hinweis</span><span class="sxs-lookup"><span data-stu-id="dceab-129">Note</span></span>  <br/> ||<span data-ttu-id="dceab-130">Enthält Informationen, die möglicherweise sinnvoll, die den Lokalisierungsexperten, Developer oder andere Benutzer, die die XLIFF-Datei zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="dceab-130">Contains information that may be useful to the localizer, developer, or others who process the XLIFF file.</span></span>  <br/>  <span data-ttu-id="dceab-p105">`note` -Elementwerte werden von generiert. `note` Attribute enthalten GUIDs, mit denen Speicherort und Inhaltstypen Kontext bereitzustellen. </span><span class="sxs-lookup"><span data-stu-id="dceab-p105">`note` element values are generated by . `note` attributes contain GUIDs that identify location and types of content to provide context. </span></span><br/> |
|<span data-ttu-id="dceab-133">Body</span><span class="sxs-lookup"><span data-stu-id="dceab-133">Body</span></span>  <br/> |||
|<span data-ttu-id="dceab-134">Trans-Einheit</span><span class="sxs-lookup"><span data-stu-id="dceab-134">Trans-unit</span></span>  <br/> | `id` <br/>  `datatype` <br/> |<span data-ttu-id="dceab-135">Das  `id` -Attribut enthält eine GUID, die den Speicherort des Imports angibt.</span><span class="sxs-lookup"><span data-stu-id="dceab-135">The  `id` attribute contains a GUID that identifies the location of the import.</span></span> <br/><span data-ttu-id="dceab-p106"> Das  `datatype` -Attribut definiert den Typ der Daten, die im **trans-unit** -Element enthalten sind. Eine Liste der verfügbaren `datatype` Attributwerte finden Sie unter das geöffnete standard XLIFF-Dokument. </span><span class="sxs-lookup"><span data-stu-id="dceab-p106"> The  `datatype` attribute defines the type of data contained in the **trans-unit** element. For a list of available `datatype` attribute values, see the XLIFF open standard document. </span></span><br/> |
|<span data-ttu-id="dceab-138">Quelle</span><span class="sxs-lookup"><span data-stu-id="dceab-138">Source</span></span>  <br/> ||<span data-ttu-id="dceab-p107">HTML-Inhalt enthält häufig Markup, die beibehalten werden. Aus diesem Grund umschließt SharePoint Markup im HTML-Inhalte mit Tags, die in der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l)definiert sind.</span><span class="sxs-lookup"><span data-stu-id="dceab-p107">HTML content often contains markup that has to be preserved. For this reason, SharePoint wraps markup in HTML content with tags that are defined in the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).  </span></span><br/> |
|<span data-ttu-id="dceab-141">Ziel</span><span class="sxs-lookup"><span data-stu-id="dceab-141">Target</span></span>  <br/> |<span data-ttu-id="dceab-142">pH (optional)</span><span class="sxs-lookup"><span data-stu-id="dceab-142">ph (optional)</span></span>  <br/> <span data-ttu-id="dceab-143">BPT (optional)</span><span class="sxs-lookup"><span data-stu-id="dceab-143">bpt (optional)</span></span>  <br/> <span data-ttu-id="dceab-144">EPT (optional)</span><span class="sxs-lookup"><span data-stu-id="dceab-144">ept (optional)</span></span>  <br/> <span data-ttu-id="dceab-145">Sub (optional)</span><span class="sxs-lookup"><span data-stu-id="dceab-145">sub (optional)</span></span>  <br/> |<span data-ttu-id="dceab-p108">HTML-Inhalt enthält häufig Markup, die beibehalten werden. Aus diesem Grund umschließt SharePoint Markup im HTML-Inhalte mit Tags, die in der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l)definiert sind.</span><span class="sxs-lookup"><span data-stu-id="dceab-p108">HTML content often contains markup that has to be preserved. For this reason, SharePoint wraps markup in HTML content with tags that are defined in the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).  </span></span><br/> |
|<span data-ttu-id="dceab-148">Bin-unit</span><span class="sxs-lookup"><span data-stu-id="dceab-148">Bin-unit</span></span>  <br/> ||<span data-ttu-id="dceab-p109">Für die Lokalisierung über XLIFF über die **bin-unit** Elemente können in SharePoint gespeicherte Dateien gesendet werden. Die Datei wieder in seiner ursprünglichen Dateiformat extrahiert werden kann, mithilfe der [SharePoint: Extrahieren und Einfügen von Bin-Unit-Elementen in XLIFF-Dateien](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) Codebeispiel. </span><span class="sxs-lookup"><span data-stu-id="dceab-p109">Files stored in SharePoint can be sent for localization via XLIFF through the **bin-unit** elements. The file can be extracted back into its original file format by using the [SharePoint: Extract and insert bin-unit elements in XLIFF files](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) code sample. </span></span><br/> |
|<span data-ttu-id="dceab-151">Bin-Quelle</span><span class="sxs-lookup"><span data-stu-id="dceab-151">Bin-source</span></span>  <br/> |||
|<span data-ttu-id="dceab-152">Bin-Ziel</span><span class="sxs-lookup"><span data-stu-id="dceab-152">Bin-target</span></span>  <br/> |||
|<span data-ttu-id="dceab-153">Interne Datei</span><span class="sxs-lookup"><span data-stu-id="dceab-153">Internalfile</span></span>  <br/> |<span data-ttu-id="dceab-154">Formular</span><span class="sxs-lookup"><span data-stu-id="dceab-154">form</span></span>  <br/> ||
   

## <a name="example-xliff-markup-from-sharepoint"></a><span data-ttu-id="dceab-155">Beispiel: XLIFF-Markup aus SharePoint</span><span class="sxs-lookup"><span data-stu-id="dceab-155">Example: XLIFF markup from SharePoint</span></span>

<span data-ttu-id="dceab-156">Im folgenden Beispiel wird eine XML-Dokuments in XLIFF-Austauschdateiformat veranschaulicht SharePoint einige Elemente und Attribute im Standard definiert implementiert.</span><span class="sxs-lookup"><span data-stu-id="dceab-156">The following example of an XML document in XLIFF interchange file format demonstrates how SharePoint implements some of the elements and attributes defined in the standard.</span></span> 
  
    
    

```XML

<?xml version="1.0" encoding="utf-8"?>
<xliff version="1.2" xmlns="urn:oasis:names:tc:xliff:document:1.2">
  <file original="ce2b8e40-b802-4196-b6cb-93e63eb4bb42" source-language="en-US" target-language="fr-CA" datatype="html">
    <header>
      <note>type=ListItem</note>
      <note>translatorType=Vendor</note>
      <note>packageGroupId=fb98837d-c4e0-48f1-9e59-874b61802cda</note>
      <note>webId=1c013046-821b-40d7-a1e0-689dd920f37d</note>
      <note>listId=58b11f3f-6549-47c5-bf13-a2dc4dfa03b3</note>
      <note>url=Pages/Type-or-edit-text-in-a-different-language.aspx</note>
      <note>sourceVersion=2</note>
    </header>
<body>
      <trans-unit id="fa564e0f-0c70-4ab9-b863-0177e6ddd247" datatype="plaintext">
        <source>Type or edit text in a different language</source>
        <note>fieldTitle=Title</note>
      </trans-unit>
      <trans-unit id="f55c4d88-1f2e-4ad9-aaa8-819af4ee7ee8" datatype="html">
        <source>
          <bpt id="1">&amp;lt;strong&amp;gt;</bpt>When you want to type documents in different languages, you can change your keyboard layout language--the language-specific characters typed when keyboard keys are pressed--so that you can type the special characters for each language. 
  <ept id="1">&amp;lt;/strong&amp;gt;</ept>
        </source>
        <note>fieldTitle=Page Content</note>
      </trans-unit>
    </body>
  </file>

```


  
    
    

## <a name="additional-resources"></a><span data-ttu-id="dceab-157">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dceab-157">Additional resources</span></span>
<span data-ttu-id="dceab-158"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dceab-158"></span></span>


-  [<span data-ttu-id="dceab-159">Hinzufügen von SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="dceab-159">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities)
    
  
- <span data-ttu-id="dceab-160">Codebeispiel:  [SharePoint: Extrahieren und Einfügen von Bin-Unit-Elementen in XLIFF-Dateien](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)</span><span class="sxs-lookup"><span data-stu-id="dceab-160">Code sample:  [SharePoint: Extract and insert bin-unit elements in XLIFF files](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)</span></span>
    
  
-  [<span data-ttu-id="dceab-161">Dienste für maschinelle Übersetzung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dceab-161">Machine Translation Services in SharePoint</span></span>](machine-translation-services-in-sharepoint)
    
  

  
    
    

