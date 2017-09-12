---
title: "Veröffentlichen von SharePoint-Websites"
ms.prod: SHAREPOINT
ms.assetid: 46b5a79c-962f-4a07-8316-d5005eabd0e0
ms.openlocfilehash: 8a8e9b072d03f7cc8f456e4e047aaf8630046c59
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="publish-sharepoint-sites"></a>Veröffentlichen von SharePoint-Websites

Nachdem Sie entwerfen oder Websitekomponenten und Inhalt zu entwickeln, können Sie diese stellen diese in der aktuellen Websitesammlung und andere Websitesammlungen - auch für Websitesammlungen, die das Intranet/Internetgrenze schneidet.
  
    
    


## <a name="cross-site-publishing"></a>Websiteübergreifende Veröffentlichung

Informationen Sie über  [websiteübergreifende Veröffentlichung](cross-site-publishing-in-sharepoint) und wie wirkt wie planen und Veröffentlichen von Websites und deren Inhalte und zugehörige Designelemente.
  
    
    

## <a name="publishing-considerations-for-variations-and-multilingual-sites"></a>Veröffentlichen von Überlegungen für Variationen und mehrsprachige Websites

Verschiedene Märkten haben verschiedene Geschmack. Das Variationsfeature unterstützt diesen Geschmack stellen bereit, mit denen Sie lokalisieren und Inhalte zu übersetzen, sondern auch Veröffentlichen dieser Inhalte und dessen zugehörige Designelemente für Websitesammlungen auf der ganzen Welt, aufzunehmen. Mit denen die Veröffentlichung von Inhalten in lokalen Märkten Erfolg zu machen, sollten Sie die folgenden Tipps, die zeigen, wie Entwurf und Inhalte Entscheidungen bezüglich der, die Sie vornehmen können beeinflussen wie veröffentlichten Websiteinhalt und Struktur rendern kann:
  
    
    

- Duplizierung der Entwurfsressourcen positiv wirkt sich auf die Leistung der Website veröffentlichen und Rendern und stellt, Verwalten von komplexen Websites, die für Variationen weniger komplexen aktiviert sind. Eine Gestaltungsvorlage ist eine ASP.NET-Datei, die Inhaltsplatzhalter enthält, die durch Seitenlayouts und Seiten einzelne Instanzen aufgefüllt werden. 
    
  
- Wenn bestimmte Inhaltstypen für alle Gebietsschemas in Ihrer Websitesammlung anwenden, empfiehlt es sich als Website Inhaltstypen des Stammwebs erstellt. Sie können auch unter Variationswebsites Inhaltstypen erstellen. 
    
  
- Wenn Sie zusätzliche Spalten hinzufügen einer Quellliste durch Hinzufügen eines Elements zu einem Inhaltstyp, der zuvor nicht in dieser Liste vorhanden war, Variationen aktualisiert das Schema der einzelnen Zielliste entsprechend die neuen Spalten das nächste Mal dieser Zielliste ein Element hinzu. 
    
  
- Verwaltete Navigation arbeitet mit Variationen. Strukturierte Navigation - basierend auf der SharePoint-Website-Struktur - auch noch funktioniert: Es Inhalt und Struktur zwischen den Quell- und Variationen Etiketten synchronisiert. 
    
  
- Das Gerät Kanäle Feature abstrahiert das Problem die Präsentation von Inhalten für mobile Geräte aus der zugrunde liegenden Websiteinhalt und-Struktur variieren. Sie können auf Masterseiten erstellen, die den Benutzern basierend auf Benutzer-Agent des Benutzers angezeigt. Vermeiden Sie hartcodierten in eine Gestaltungsvorlage Inhalte, die lokalisiert werden muss.
    
  
- Websites mit dynamischen Inhalt zusammengestellt aus mehreren Quellen Risiko müssen Inhalte in mehreren Sprachen auf derselben Seite gerendert wurde. Vermeiden Sie beispielsweise Fällen, in denen Artikel Seiteninhalt einer Sprache während Inhalt gerendert, indem eine Inhalt-Webpart in eine andere Sprache gerendert werden. 
    
  
- Bei der Arbeit mit Anzeigevorlagen, die mit mehreren Sprachen verwendet werden, erstellen Sie Sprachdateien, und platzieren Sie diese unter-Ordner, die mit dem Gebietsschema, denen sie lauten auf anwenden. Sie können dann die Sprachdateien mit der  `$includeLanguageScript` -Funktion und das Token `{Locale}` verweisen.
    
    Wenn die Inhaltssuche-Webpart die **Language** -Eigenschaft beim Suchen der entsprechenden Datei CustomStrings.js nutzt enthalten eine ist nicht vorhanden, und Code in der Vorlage eine Zeichenfolge, die fordert mithilfe der Funktionen `$resource()` oder `Srch.U.loadResource()` nicht gefunden werden kann, um anzuzeigen, wird die Inhaltssuche-Webpart eine Fehlermeldung angezeigt.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint)
    
  
-  [Neuerung bei SharePoint-Websiteentwicklung](what-s-new-with-sharepoint-site-development)
    
  

