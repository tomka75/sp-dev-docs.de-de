---
title: URLs und Tokens in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 46db672ebf75166154351dc3b35b89ec803914e6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="urls-and-tokens-in-sharepoint"></a>URLs und Tokens in SharePoint
Erfahren Sie, wie Sie URLs bilden und URL-Token in SharePoint verwenden.

## <a name="types-of-urls-in-sharepoint"></a>Typen von URLs in SharePoint
<a name="TypesOfURLs"> </a>

SharePoint analysiert URL-Zeichenfolgen, um die Form von URLs auf Basis eines angegebenen Protokolls (z. B. **http:**) oder anhand der Position eines Schrägstrichs (/) innerhalb einer Zeichenfolge zu ermitteln. In Abhängigkeit von dem bestimmten Element können Sie die folgenden URL-Formen verwenden:
  
    
    

- Eine **absolute URL** gibt einen vollständigen Pfad an und beginnt mit einem Protokoll. Beispiel: `http://` _Domäne_oder_Server_/[ `sites/`] _Website_/ `Lists`/ _Listentitel_/ `AllItems.aspx`.
    
  
- Eine **domänenbezogene URL** basiert auf der Domänenadresse (die aus dem Namen eines Servers bestehen kann) und beginnt immer mit einem Schrägstrich. Sie gibt einen vollständigen Pfad von der Website auf höchster Ebene bis zum Dateinamen an. Beispiel: /[ `sites/`] _Website_/ `Lists`/ _Listentitel_/ `AllItems.aspx`. 
    
  
- Eine **websitebezogene URL** basiert auf der Adresse eines Websiteobjekts ( [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) ). Sie beginnt _nicht_ mit einem Schrägstrich und gibt einen vollständigen Pfad von der Websiteadresse bis zum Dateinamen an. Beispiel: `Lists/` _Listentitel_/ `AllItems.aspx`.
    
  
- Eine **auf eine Datei oder einen Ordner bezogene URL** basiert auf dem Ordner, der die Datei enthält. Sie enthält _keine_ Schrägstriche. Sie gibt einfach den Namen der Datei an. Beispiel: `AllItems.aspx`.
    
  

> **Hinweis:** Es gibt kein Konzept einer auf Websitesammlungen bezogenen URL. Die Übergabe einer derartigen URL kann zu einem Codefehler führen. 
  
    
    


## <a name="good-practice-for-image-urls"></a>Bewährte Methoden für Bild-URLs
<a name="GoodPracticeImageURL"> </a>

Wenn Sie eine URL für eine Bilddatei erstellen, die sich im Verzeichnis %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\IMAGES befindet, geben Sie einen Pfad an, der die Stammwebsite der Websitesammlung verwendet, aber im Pfad keine untergeordnete Website einbezieht. Verwenden Sie z. B. "/_layouts/images/MyImage.gif" für eine Bilddatei, nicht "/MySubsite/_layouts/images/MyImage.gif". Der Grund hierfür ist, dass die URLs der untergeordneten Website in Abhängigkeit davon, wo sie verwendet werden, auf andere Weise aufgelöst werden. Sie können diese Varianten ignorieren, wenn Sie immer die auf die Stammwebsite bezogene URL verwenden.
  
    
    

## <a name="url-tokens-in-sharepoint"></a>URL-Token in SharePoint
<a name="URLtokens"> </a>

SharePoint unterstützt die in den folgenden Tabellen aufgeführten Token für SharePoint-Add-Ins oder Farmlösungen. Zudem können einige Token nur in Apps verwendet werden. Weitere Informationen dazu finden Sie unter  [URL-Zeichenfolgen und Tokens in Add-Ins für SharePoint](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).
  
    
    
Die Token in den Tabellen dieses Abschnitts können bei der SharePoint-Entwicklung in verschiedenen Situationen in URLs verwendet werden, z. B. in benutzerdefinierten Aktionen sowie in Links auf benutzerdefinierte Seiten. Einige dieser Token können in gewissen Kontexten nicht verwendet werden. Drei der wichtigsten Positionen, an denen nur eine eingeschränkte Liste von Token verwendet werden kann, sind die Startseite einer App, eine benutzerdefinierte Aktion für das Hostweb und die  [Src](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPAppIFrame.Src.aspx) -Eigenschaft eines App-Webparts. Diese werden in separaten Spalten angegeben. Diese drei Positionen stellen keine vollständige Liste der Positionen dar, an denen Token verwendet werden können.
  
    
    
Die Spalte **StartPage** gibt an, ob das Token im **StartPage**-Element eines App-Manifests verwendet werden kann. Die Spalte **Benutzerdefinierte Aktion** gibt an, ob das Token in der URL einer benutzerdefinierten Aktion in einem Hostweb verwendet werden kann. Die Spalte **App-Webpart** gibt an, ob das Token in der [Src](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPAppIFrame.Src.aspx) -Eigenschaft des App-Webparts verwendet werden kann.
  
    
    

**Token, die am Anfang einer URL verwendet werden können**


|**Token**|**Wird aufgelöst zu**|**StartPage**|**Benutzerdefinierte Aktion**|**App-Webpart**|**Bemerkungen**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|~controlTemplates  <br/> |Die URL des virtuellen Ordners ControlTemplates der aktuellen Website  <br/> |Nein  <br/> |Nein  <br/> |Nein  <br/> ||
|~layouts  <br/> |Die URL des virtuellen Ordners Layouts für die aktuelle Website  <br/> |Nein  <br/> |Nein  <br/> |Nein  <br/> ||
|~site  <br/> |Die URL der aktuellen Website.  <br/> |Nein  <br/> |Nein  <br/> |Ja  <br/> ||
|~sitecollection  <br/> |Die URL der übergeordneten Websitesammlung der aktuellen Website.  <br/> |Nein  <br/> |Nein  <br/> |Ja  <br/> ||
   
Sofern nicht anders angegeben, kann keines dieser Token in der nächsten Tabelle im  *Pfad*  -Teil des [Src](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPAppIFrame.Src.aspx) -Eigenschaftenwerts des App-Webparts verwendet werden. Die Spalte **App-Webpart** bezieht sich auf deren Verwendung im *Abfragezeichenfolge*  -Teil des Werts.
  
    
    

**Token, die innerhalb einer URL verwendet werden können**


|**Token**|**Wird aufgelöst zu**|**StartPage**|**Benutzerdefinierte Aktion**|**App-Webpart**|**Bemerkungen**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|{ControlTemplates}  <br/> |Die URL des virtuellen Ordners ControlTemplates der aktuellen Website  <br/> |Nein  <br/> |Nein  <br/> |Nein  <br/> ||
|{ItemId}  <br/> |Die ID eines Elements in einer Liste oder Bibliothek (eine ganze Zahl)  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> ||
|{ItemUrl}  <br/> |Die URL des Elements, an dem eine Aktion ausgeführt wird.  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> ||
|{Layouts}  <br/> |Die URL des virtuellen Ordners Layouts für die aktuelle Website  <br/> |Nein  <br/> |Nein  <br/> |Nein  <br/> ||
|{ListId}  <br/> |Die ID der aktuellen Liste (eine GUID).  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> ||
|{RecurrenceId}  <br/> |Der Wiederholungsindex eines sich wiederholenden Ereignisses.  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> |In Kontextmenüs von Listenelementen wird die Verwendung dieses Tokens nicht unterstützt.  <br/> |
|{Site}  <br/> |Die URL der aktuellen Website.  <br/> |Nein  <br/> |Ja  <br/> |Ja  <br/> ||
|{SiteCollection}  <br/> |Die URL der übergeordneten Website der aktuellen Website.  <br/> |Nein  <br/> |Ja  <br/> |Ja  <br/> ||
|{SiteUrl}  <br/> |Die URL der aktuellen Website.  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> ||
|{Source}  <br/> |Die URL der HTTP-Anforderung  <br/> |Nein  <br/> |Ja  <br/> |Nein  <br/> ||
   

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15URLS_addlresources"> </a>


-  
  [Erstellen von Farmlösungen in SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163902.aspx)
    
  
-  [Erweiterte Extranetunterstützung](http://msdn.microsoft.com/library/21d67796-23c5-4339-8f0e-124208d21ab2%28Office.15%29.aspx)
    
  
-  [Abrufen von Verweisen auf Websites, Webanwendungen und andere Schlüsselobjekte](http://msdn.microsoft.com/library/8623ef1d-e3cc-426c-84a3-6379e0ae284f%28Office.15%29.aspx)
    
  
-  [Arbeiten mit Listenobjekten und Auflistungen](http://msdn.microsoft.com/library/d4167b10-6f1e-49f1-8b22-16ce20012a27%28Office.15%29.aspx)
    
  
-  [Verwenden des Objektmodells für grundlegende Aufgaben](http://msdn.microsoft.com/library/94d6898d-6a0f-43a7-ad06-1b27ec6916ea%28Office.15%29.aspx)
    
  
