---
title: Das XLIFF-Interchange-Dateiformat in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 660c0f07-7030-4576-957e-b9f2cd0fa895
ms.openlocfilehash: 106110eb458cf6cd76ebc67fd8516cbcb4358a4f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="the-xliff-interchange-file-format-in-sharepoint"></a>Das XLIFF-Interchange-Dateiformat in SharePoint
Abrufen von Informationen über die SharePoint Implementierung der XLIFF-Austauschdateiformat, einschließlich Schema Referenzinformationen und ein Beispiel für XML.
## <a name="the-xliff-interchange-file-format-implementation-in-sharepoint"></a>XLIFF Interchange File Format Implementierung in SharePoint

SharePoint bietet Unterstützung von XML-Lokalisierung Interchange File Format (XLIFF) für das Variationsfeature und das Feature für die Übersetzungsdienste. SharePoint Server verwendet XLIFF aus SharePoint Server auf ein Übersetzer in einem Format, das der Übersetzer auf einfache Weise verstehen, welche zu Transportinformationen zu einer Datei und seinen Inhalt.
  
    
    
SharePoint entspricht der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) von OASIS veröffentlicht werden, wenn SharePoint Server HTML-Seiten in XLIFF-Format extrahiert werden. Zur Verringerung der der Mischung der übersetzbare Elemente und Code-Elemente, die in XLIFF-Paketen angezeigt würden, würde eine unveränderte SharePoint Server CDATA Content übertragen werden, wird SharePoint übermittelt, die Möglichkeit, vollständig XLIFF-kompatiblen XLIFF-Dokumente zu erstellen, die auch gut SharePoint integriert sind. Beim Exportieren von XML-Dateien in XLIFF-Format aus `sharepointservernv`sind die Daten, die der Übersetzer empfängt clean und übersetzen bereit.
  
    
    
In diesem Artikel Dokumente bestimmte SharePoint Server Implementierungen von XLIFF-Elementen und Attributen, die im Allgemeinen in XLIFF geöffneten standard Dokuments von OASIS veröffentlichte Version 1.2 definiert sind. Weitere Informationen zu bestimmten XLIFF-Elementen und Attributen finden Sie unter der  [XLIFF 1.2-Spezifikation](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel).
  
    
    

  
    
    

**In Tabelle 1. Wichtige XLIFF-Elemente und-Attribute in SharePoint**


|**Element**|**Attribute**|**Hinweise**|
|:-----|:-----|:-----|
|XML  <br/> | `version` <br/>  `encoding` <br/> |Deklarieren die XML-Version und die Codierung.  <br/> |
|XLIFF  <br/> | `version` <br/>  `xmlns` <br/> |Enthält das  `version` -Attribut und das Schema Validation Mechanismus. <br/> |
|Datei  <br/> | `original` <br/>  `source-language` <br/>  `target-language` <br/>  `datatype` <br/>  `tool-id` <br/> |Entspricht der ursprünglichen Quelle-Datei, die in einseitiges GUID aus das Variationsfeature ist, enthält die Ausgangs- und Zielsprache ( `source-language` und `target-language`), die von maschinelle Übersetzung Tools und Human Translation Tools verwendet werden.  <br/> Das  `original` -Attribut enthält eine GUID, die Inhalt der ursprünglichen Quelle identifiziert. Dieser Wert sollte zur Sicherstellung eines erfolgreichen Imports statisch bleiben. <br/> Das  `datatype` -Attribut wird auch im **File** -Element im HTML-Format für alle SharePoint-Seiten gespeichert. <br/> Das Attribut  `tool-id` ist die GUID, die das Tool identifiziert, das die XLIFF-Datei generiert. <br/> |
|Kopfzeile  <br/> |||
|Tool  <br/> | `tool-id` <br/>  `tool-name` <br/> |Gibt an, mit die XLIFF-Datei generiert wurde.  <br/> |
|Hinweis  <br/> ||Enthält Informationen, die möglicherweise sinnvoll, die den Lokalisierungsexperten, Developer oder andere Benutzer, die die XLIFF-Datei zu verarbeiten.  <br/>  `note` -Elementwerte werden von generiert. `note` Attribute enthalten GUIDs, mit denen Speicherort und Inhaltstypen Kontext bereitzustellen. <br/> |
|Body  <br/> |||
|Trans-Einheit  <br/> | `id` <br/>  `datatype` <br/> |Das  `id` -Attribut enthält eine GUID, die den Speicherort des Imports angibt. <br/> Das  `datatype` -Attribut definiert den Typ der Daten, die im **trans-unit** -Element enthalten sind. Eine Liste der verfügbaren `datatype` Attributwerte finden Sie unter das geöffnete standard XLIFF-Dokument. <br/> |
|Quelle  <br/> ||HTML-Inhalt enthält häufig Markup, die beibehalten werden. Aus diesem Grund umschließt SharePoint Markup im HTML-Inhalte mit Tags, die in der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l)definiert sind.<br/> |
|Ziel  <br/> |pH (optional)  <br/> BPT (optional)  <br/> EPT (optional)  <br/> Sub (optional)  <br/> |HTML-Inhalt enthält häufig Markup, die beibehalten werden. Aus diesem Grund umschließt SharePoint Markup im HTML-Inhalte mit Tags, die in der  [XLIFF 1.2 Darstellung Guide für HTML-](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l)definiert sind.<br/> |
|Bin-unit  <br/> ||Für die Lokalisierung über XLIFF über die **bin-unit** Elemente können in SharePoint gespeicherte Dateien gesendet werden. Die Datei wieder in seiner ursprünglichen Dateiformat extrahiert werden kann, mithilfe der [SharePoint: Extrahieren und Einfügen von Bin-Unit-Elementen in XLIFF-Dateien](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) Codebeispiel. <br/> |
|Bin-Quelle  <br/> |||
|Bin-Ziel  <br/> |||
|Interne Datei  <br/> |Formular  <br/> ||
   

## <a name="example-xliff-markup-from-sharepoint"></a>Beispiel: XLIFF-Markup aus SharePoint

Im folgenden Beispiel wird eine XML-Dokuments in XLIFF-Austauschdateiformat veranschaulicht SharePoint einige Elemente und Attribute im Standard definiert implementiert. 
  
    
    

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


  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Hinzufügen von SharePoint-Funktionen](add-sharepoint-capabilities.md)
    
  
- Codebeispiel:  [SharePoint: Extrahieren und Einfügen von Bin-Unit-Elementen in XLIFF-Dateien](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)
    
  
-  [Dienste für maschinelle Übersetzung in SharePoint](machine-translation-services-in-sharepoint.md)
    
  

  
    
    

