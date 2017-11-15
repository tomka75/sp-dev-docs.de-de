---
title: Vorgehensweise Abrufen die URL einer Bibliothek Seiten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d9922e4b-4948-4c4a-a8ca-1623168143a3
ms.openlocfilehash: c1ad399ddf59d928ca46356be1fc762b2312443e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-retrieve-the-url-of-a-pages-library"></a>Vorgehensweise: Abrufen die URL einer Bibliothek Seiten
Hier erfahren Sie, wie Sie die URL für die Liste der Seiten für eine Web Veröffentlichen in einer Websitesammlung, die unterscheidet sich aus dem aktuellen Kontext abrufen.
## <a name="core-concepts-to-know-for-retrieving-the-url-of-a-pages-list"></a>Kernkonzepte für das Abrufen des URL einer Liste von Seiten
<a name="SP15_Core_Concepts_URL_MP"> </a>

Beim Entwickeln von benutzerdefinierter Anwendungen für Veröffentlichungssites können Sie feststellen, dass das Objektmodell  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) eine Möglichkeit zum Abrufen der URL für die Liste der Seiten eines Verö Webs in einer Websitesammlung, die unterscheidet sich im aktuellen Kontext nicht verfügbar machen. Obwohl die **PublishingWeb** -Klasse die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) -Klasse ist ein Wrapper für Instanzen, die Features für die Veröffentlichung aktiviert, die Klasse ist nicht zum Instanziieren von Objekten außerhalb des aktuellen Kontext **SPWeb** verwendet werden soll.
  
    
    
Wenn die URL für die Liste der Seiten für eine andere Webanwendung abgerufen werden müssen, können Sie die  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft abfragen. Da das Objekt [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) -Objekt einer Veröffentlichungswebsite ist, können Sie die [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft Abfragen und schreiben den Inhalt in eine Konsolenanwendung. Wenn der Eintrag `Key = vti_pageslistname, Value = {the URL to the Pages library}` in der Konsole zurückgegeben wird, ist *{die URL zu der Bibliothek für Seiten}*  Seiten-Listen-URL.
  
    
    

**In Tabelle 1. Kernkonzepte für das Abrufen der URL der Seitenbibliothek**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
|Pages Library  <br/> |Eine Dokumentbibliothek, die alle Inhaltsseiten für eine Veröffentlichungswebsite enthält.  <br/> |
| [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) <br/> |Steht für eine Website SharePoint Foundation.  <br/> |
| [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) <br/> |Ruft ein Objekt  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) mit Metadaten für die aktuelle Website ab. <br/> |
| [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) <br/> |Speichert beliebige Schlüssel-Wert-Paaren, die Einstellungen für die benutzerdefinierte Eigenschaft enthalten.  <br/> |
| [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) <br/> |Stellt Veröffentlichungsverhalten für eine Instanz von **SPWeb**, die Veröffentlichung unterstützt bereit. <br/> |
   

## <a name="retrieve-the-url-of-a-pages-list-for-a-publishing-web-in-a-site-collection-that-differs-from-the-current-context"></a>Abrufen einer Liste Seiten für ein Web Veröffentlichen in einer Websitesammlung, die unterscheidet sich der URL aus dem aktuellen Kontext
<a name="SP15_Code_URL_Pages_List"> </a>

In diesem Beispiel Konsolenanwendung greift auf die  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft, die Auflistung durchlaufen und schreibt jedes Schlüssel/Wert-Paar in der Konsole angezeigt.
  
    
    

### <a name="to-query-the-spwebproperties-property-for-the-url-to-the-pages-list"></a>Abfrage der SPWeb.Properties-Eigenschaft für die Liste der Seiten-URL


1. Schreiben Sie die Konsolenanwendung.
    
  
2. Zeigen Sie die Ausgabe in der Konsole an.
    
  

## <a name="example-query-spwebproperties-property-for-the-url-to-the-pages-list"></a>Beispiel: Abfrage SPWeb.Properties-Eigenschaft für die Liste der Seiten-URL
<a name="SP15_Example_SPWeb_Properties"> </a>

Die Anwendung fragt das  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) -Objekt, dessen Wörterbucheinträge durchläuft und schreibt diese Einträge in der Konsole angezeigt.
  
    
    

```cs

using System;
using System.Collections;
using Microsoft.SharePoint;
using Microsoft.SharePoint.Utilities;

namespace Test
{
    class Program
    {
        static void Main(string[] args)
        {
            using (SPSite site = new SPSite("http://localhost"))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    SPPropertyBag props = web.Properties;
                    foreach (DictionaryEntry de in props)
                    {
                        Console.WriteLine("Key = {0}, Value = {1}", de.Key, de.Value);
                    }
                }
            }
            Console.ReadLine();
        }
    }
}

```

Die Ausgabe, die diese Anwendung in der Konsole gedruckt variiert Website in Website, aber er kann wie folgt aussehen:
  
    
    



```

Key = vti_associatemembergroup, Value = 5
Key = vti_extenderversion, Value = 14.0.0.4016
Key = vti_associatevisitorgroup, Value = 4
Key = vti_associategroups, Value = 5;4;3
Key = vti_createdassociategroups, Value = 3;4;5
Key = vti_siteusagetotalbandwidth, Value = 547
Key = vti_siteusagetotalvisits, Value = 9
Key = vti_associateownergroup, Value = 3
Key = vti_defaultlanguage, Value = en-us
Key = vti_pageslistname, Value = {the URL to the Pages list}
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  

