---
title: Abrufen der URL einer Seitenbibliothek
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d9922e4b-4948-4c4a-a8ca-1623168143a3
ms.openlocfilehash: 8f132495459b0b581be648942c81dbf60382cac0
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="retrieve-the-url-of-a-pages-library"></a><span data-ttu-id="3ffee-102">Abrufen der URL einer Seitenbibliothek</span><span class="sxs-lookup"><span data-stu-id="3ffee-102">How to: Retrieve the URL of a Pages library</span></span>

<span data-ttu-id="3ffee-103">Hier erfahren Sie, wie Sie die URL für die Liste der Seiten für eine Web Veröffentlichen in einer Websitesammlung, die unterscheidet sich aus dem aktuellen Kontext abrufen.</span><span class="sxs-lookup"><span data-stu-id="3ffee-103">Learn how to retrieve the URL for the pages list for a publishing web in a site collection that differs from the current context.</span></span>

## <a name="core-concepts-to-know-for-retrieving-the-url-of-a-pages-list"></a><span data-ttu-id="3ffee-104">Kernkonzepte für das Abrufen des URL einer Liste von Seiten</span><span class="sxs-lookup"><span data-stu-id="3ffee-104">Core concepts to know for retrieving the URL of a Pages list</span></span>
<span data-ttu-id="3ffee-105"><a name="SP15_Core_Concepts_URL_MP"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffee-105"><a name="SP15_Core_Concepts_URL_MP"> </a></span></span>

<span data-ttu-id="3ffee-p101">Beim Entwickeln von benutzerdefinierter Anwendungen für Veröffentlichungssites können Sie feststellen, dass das Objektmodell  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) eine Möglichkeit zum Abrufen der URL für die Liste der Seiten eines Verö Webs in einer Websitesammlung, die unterscheidet sich im aktuellen Kontext nicht verfügbar machen. Obwohl die **PublishingWeb** -Klasse die [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) -Klasse ist ein Wrapper für Instanzen, die Features für die Veröffentlichung aktiviert, die Klasse ist nicht zum Instanziieren von Objekten außerhalb des aktuellen Kontext **SPWeb** verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="3ffee-p101">When developing custom applications for publishing sites, you may notice that the  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) object model does not expose a way to retrieve the URL for the Pages list of a publishing web in a site collection that differs from the current context. Although the **PublishingWeb** class wraps the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) class for instances that have the publishing feature activated, the class is not intended to be used to instantiate **SPWeb** objects outside of the current context.</span></span>
  
    
    
<span data-ttu-id="3ffee-p102">Wenn die URL für die Liste der Seiten für eine andere Webanwendung abgerufen werden müssen, können Sie die  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft abfragen. Da das Objekt [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) -Objekt einer Veröffentlichungswebsite ist, können Sie die [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft Abfragen und schreiben den Inhalt in eine Konsolenanwendung. Wenn der Eintrag `Key = vti_pageslistname, Value = {the URL to the Pages library}` in der Konsole zurückgegeben wird, ist *{die URL zu der Bibliothek für Seiten}*  Seiten-Listen-URL.</span><span class="sxs-lookup"><span data-stu-id="3ffee-p102">If you need to retrieve the URL for the Pages list for a different web application, you can query the  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property. Since the [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) object is the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) object of a publishing site, you can query the [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property and write its contents to a console application. If the entry `Key = vti_pageslistname, Value = {the URL to the Pages library}` is returned in the console, *{the URL to the Pages library}*  is the Pages list URL.</span></span>
  
    
    

<span data-ttu-id="3ffee-111">**In Tabelle 1. Kernkonzepte für das Abrufen der URL der Seitenbibliothek**</span><span class="sxs-lookup"><span data-stu-id="3ffee-111">**Table 1. Core concepts for retrieving the URL of a Pages library**</span></span>


|<span data-ttu-id="3ffee-112">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="3ffee-112">**Article title**</span></span>|<span data-ttu-id="3ffee-113">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="3ffee-113">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="3ffee-114">Pages Library</span><span class="sxs-lookup"><span data-stu-id="3ffee-114">Pages Library</span></span>  <br/> |<span data-ttu-id="3ffee-115">Eine Dokumentbibliothek, die alle Inhaltsseiten für eine Veröffentlichungswebsite enthält.</span><span class="sxs-lookup"><span data-stu-id="3ffee-115">A document library that contains all the content pages for a publishing site.</span></span>  <br/> |
| [<span data-ttu-id="3ffee-116">SPWeb</span><span class="sxs-lookup"><span data-stu-id="3ffee-116">SPWeb</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) <br/> |<span data-ttu-id="3ffee-117">Steht für eine Website SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="3ffee-117">Represents a SharePoint Foundation website.</span></span>  <br/> |
| [<span data-ttu-id="3ffee-118">Properties</span><span class="sxs-lookup"><span data-stu-id="3ffee-118">Properties</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) <br/> |<span data-ttu-id="3ffee-119">Ruft ein Objekt  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) mit Metadaten für die aktuelle Website ab.</span><span class="sxs-lookup"><span data-stu-id="3ffee-119">Gets a  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) object with metadata for the current website.</span></span> <br/> |
| [<span data-ttu-id="3ffee-120">SPPropertyBag</span><span class="sxs-lookup"><span data-stu-id="3ffee-120">SPPropertyBag</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) <br/> |<span data-ttu-id="3ffee-121">Speichert beliebige Schlüssel-Wert-Paaren, die Einstellungen für die benutzerdefinierte Eigenschaft enthalten.</span><span class="sxs-lookup"><span data-stu-id="3ffee-121">Stores arbitrary key and value pairs that contain custom property settings.</span></span>  <br/> |
| [<span data-ttu-id="3ffee-122">PublishingWeb</span><span class="sxs-lookup"><span data-stu-id="3ffee-122">PublishingWeb</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) <br/> |<span data-ttu-id="3ffee-123">Stellt Veröffentlichungsverhalten für eine Instanz von **SPWeb**, die Veröffentlichung unterstützt bereit.</span><span class="sxs-lookup"><span data-stu-id="3ffee-123">Provides publishing behavior for an instance of **SPWeb** that supports publishing.</span></span> <br/> |
   

## <a name="retrieve-the-url-of-a-pages-list-for-a-publishing-web-in-a-site-collection-that-differs-from-the-current-context"></a><span data-ttu-id="3ffee-124">Abrufen einer Liste Seiten für ein Web Veröffentlichen in einer Websitesammlung, die unterscheidet sich der URL aus dem aktuellen Kontext</span><span class="sxs-lookup"><span data-stu-id="3ffee-124">Retrieve the URL of a Pages list for a publishing web in a site collection that differs from the current context</span></span>
<span data-ttu-id="3ffee-125"><a name="SP15_Code_URL_Pages_List"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffee-125"><a name="SP15_Code_URL_Pages_List"> </a></span></span>

<span data-ttu-id="3ffee-126">In diesem Beispiel Konsolenanwendung greift auf die  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) -Eigenschaft, die Auflistung durchlaufen und schreibt jedes Schlüssel/Wert-Paar in der Konsole angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3ffee-126">This example console application accesses the  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property, iterates through the collection, and writes each key/value pair to the console.</span></span>
  
    
    

### <a name="to-query-the-spwebproperties-property-for-the-url-to-the-pages-list"></a><span data-ttu-id="3ffee-127">Abfrage der SPWeb.Properties-Eigenschaft für die Liste der Seiten-URL</span><span class="sxs-lookup"><span data-stu-id="3ffee-127">To query the SPWeb.Properties property for the URL to the Pages list</span></span>


1. <span data-ttu-id="3ffee-128">Schreiben Sie die Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="3ffee-128">Write the console application.</span></span>
    
  
2. <span data-ttu-id="3ffee-129">Zeigen Sie die Ausgabe in der Konsole an.</span><span class="sxs-lookup"><span data-stu-id="3ffee-129">View the output in the console.</span></span>
    
  

## <a name="example-query-spwebproperties-property-for-the-url-to-the-pages-list"></a><span data-ttu-id="3ffee-130">Beispiel: Abfrage SPWeb.Properties-Eigenschaft für die Liste der Seiten-URL</span><span class="sxs-lookup"><span data-stu-id="3ffee-130">Example: Query SPWeb.Properties property for the URL to the Pages list</span></span>
<span data-ttu-id="3ffee-131"><a name="SP15_Example_SPWeb_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffee-131"><a name="SP15_Example_SPWeb_Properties"> </a></span></span>

<span data-ttu-id="3ffee-132">Die Anwendung fragt das  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) -Objekt, dessen Wörterbucheinträge durchläuft und schreibt diese Einträge in der Konsole angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3ffee-132">The application queries the  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) object, iterates through its dictionary entries, and writes those entries to the console.</span></span>
  
    
    

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

<span data-ttu-id="3ffee-133">Die Ausgabe, die diese Anwendung in der Konsole gedruckt variiert Website in Website, aber er kann wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="3ffee-133">The output that this application prints to the console varies from website to website, but it might look like the following:</span></span>
  
    
    



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


## <a name="additional-resources"></a><span data-ttu-id="3ffee-134">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3ffee-134">Additional resources</span></span>
<span data-ttu-id="3ffee-135"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffee-135"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="3ffee-136">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffee-136">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

