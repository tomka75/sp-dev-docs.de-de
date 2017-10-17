---
title: URL-Zeichenfolgen und Tokens in SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f72b508740db3653cc9515fe3eb9800a0038b1aa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="url-strings-and-tokens-in-sharepoint-add-ins"></a>URL-Zeichenfolgen und Tokens in SharePoint-Add-Ins
Erfahren Sie, welche URL-Tokens für die Verwendung in SharePoint-Add-Ins verfügbar sind.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


 **Wichtig** Allgemeine Informationen zur Erstellung von URLs in SharePoint und zur Verwendung von Token in diesen URLs finden Sie unter [URLs und Token in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx). In diesem Thema werden die in SharePoint-Add-Ins verfügbaren Token beschrieben.
 


## 
<a name="URLtokens"> </a>

SharePoint unterstützt die in der folgenden Tabelle aufgeführten Token in SharePoint-Add-Ins.
 

 
Die Token in den Tabellen dieses Abschnitts können in einer Vielzahl von Situationen bei der Entwicklung von SharePoint-Add-Ins in URLs verwendet werden, so beispielsweise in benutzerdefinierten Aktionen und in Links auf benutzerdefinierten Seiten. In einigen Kontexten können einige dieser URLs nicht verwendet werden. Drei der wichtigsten Orte, an denen nur eine eingeschränkte Liste der Token verwendet werden kann, sind die Startseite eines Add-Ins, eine benutzerdefinierte Aktion im Hostweb und die **Src**-Eigenschaft eines Add-In-Webparts. Diese werden in separaten Spalten aufgeführt. * Es handelt sich dabei **jedoch nicht um eine erschöpfende Liste der Orte, an denen Token verwendet werden können.*** 
 

 
Die Spalte **StartPage** gibt an, ob das Token im **StartPage**-Element eines Add-In-Manifests verwendet werden kann. Die Spalte **Benutzerdefinierte Aktion** gibt an, ob das Token in der URL einer benutzerdefinierten Aktion in einem Hostweb verwendet werden kann. Die Spalte **Add-In-Webpart** gibt an, ob das Token in der **Src**-Eigenschaft des Add-In-Webparts verwendet werden kann.
 

 

**Token, die am Anfang einer URL in einer SharePoint-Add-In verwendet werden können**


|**Token**|**Wird aufgelöst zu**|**StartPage**|**Benutzerdefinierte Aktion**|**Add-In-Webpart**|**Bemerkungen**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|~appWebUrl|Die URL des Add-In-Webs einer SharePoint-Add-In.|Ja|Ja|Ja|Dieses Token sollte nur außerhalb des Add-In-Webparts verwendet werden. Innerhalb des Add-In-Webparts verwenden Sie **~site** als URL des Add-In-Webparts.|
|~controlTemplates|Die URL des virtuellen Ordners ControlTemplates der aktuellen Website|Nein|Nein|Nein||
|~hostUrl|Die URL des Hostweb|Nein|Nein|Ja||
|~hostLogoUrl|Die URL des Logos des Hostweb|Nein|Nein|Nein||
|~layouts|Die URL des virtuellen Ordners Layouts für die aktuelle Website|Nein|Nein|Nein||
|~remoteAppUrl|Die URL einer Remotewebanwendung in einer SharePoint-Add-In.|Ja|"Ja" im Hostweb, aber "Nein" im Add-In-Webpart|Ja|Wenn Sie nicht Microsoft Office Developer Tools für Visual Studio zum Entwickeln Ihres SharePoint-Add-Ins verwenden, können Sie **~remoteAppUrl** nicht in der **StartPage**-URL verwenden. Wenn Sie jedoch Visual Studio und die Tools verwenden, können Sie dieses Token für jedes von einem Anbieter gehostete Add-In verwenden. Es wird aufgelöst, wenn das Add-In von Visual Studio gepackt wird. Bei dieser Art der Nutzung handelt es sich dann eher um ein Visual Studio-Token als um ein SharePoint-Token. Es kann außerhalb des Add-In-Manifests verwendet werden, auch wenn Sie Microsoft Office Developer Tools für Visual Studio nicht verwenden.|
|~site|Die URL der aktuellen Website.|Nein|Nein|Ja||
|~sitecollection|Die URL der übergeordneten Websitesammlung der aktuellen Website.|Nein|Nein|Ja||
Sofern nicht anders angegeben, kann keines der Token in der nächsten Tabelle im  *Pfad*  -Teil des **Src** -Eigenschaftenwerts des Add-In-Webparts verwendet werden. Die Spalte **Add-In-Webpart** bezieht sich auf deren Verwendung im *Abfragezeichenfolge*  -Teil des Werts.
 

 

**Token, die innerhalb einer URL verwendet werden können**


|**Token**|**Wird aufgelöst zu**|**StartPage**|**Benutzerdefinierte Aktion**|**Add-In-Webpart**|**Bemerkungen**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|{AppContextToken}|Das OAuth-Kontexttoken für das Add-In|Nein|Nein|Nein||
|{AppWebUrl}|Die URL des Add-In-Webparts in einer SharePoint-Add-In|Ja|Ja|Ja|Dieses Token sollte nur außerhalb eines Add-In-Webparts verwendet werden. Innerhalb des Add-In-Webparts verwenden Sie **{Site}** als URL des Add-In-Webparts.|
|{ClientTag}|Die Clientcache-Kontrollnummer (Clienttag) für die aktuelle Website|Ja|Ja|Ja||
|{HostLogoUrl}|Das Logo für das Hostweb einer SharePoint-Add-In.|Ja|Ja|Ja||
|{HostTitle}|Der Titel des Hostwebs einer SharePoint-Add-In.|Ja|Ja|Ja||
|{HostUrl}|Die URL des Hostwebs einer SharePoint-Add-In.|Ja|Ja|Ja||
|{ItemId}|Die ID eines Elements in einer Liste oder Bibliothek (eine ganze Zahl)|Nein|Ja|Nein||
|{ItemUrl}|Die URL des Elements, an dem eine Aktion ausgeführt wird. |Nein|Ja|Nein||
|{Language}|Die aktuelle Sprach-/Kultureinstellung des Hostwebs einer SharePoint-Add-In.|Ja|Ja|Ja||
|{ListId}|Die ID der aktuellen Liste (eine GUID).|Nein|Ja|Nein||
|{ProductNumber}|Die vollständige Buildversionsnummer der SharePoint-Farm|Ja|Ja|Ja|Beispielwert: "15.0.4433.1011"|
|{RecurrenceId}|Der Wiederholungsindex eines sich wiederholenden Ereignisses.|Nein|Ja|Nein|In Kontextmenüs von Listenelementen wird die Verwendung dieses Tokens nicht unterstützt.|
|{RemoteAppUrl}|Die URL einer Remotewebanwendung in einer SharePoint-Add-In.|Ja|Ja|Ja||
|{Site}|Die URL der aktuellen Website.|Nein|Ja|Ja||
|{SiteCollection}|Die URL der übergeordneten Website der aktuellen Website.|Nein|Ja|Ja||
|{SiteUrl}|Die URL der aktuellen Website.|Nein|Ja|Nein||
|{Source}|Die URL der HTTP-Anforderung|Nein|Ja|Nein||
|{StandardTokens}|Weitere Informationen finden Sie in der "Anmerkungen".|Ja|Ja|Ja|Dieses Token ist die Kombination von fünf anderen Token. Es wird anfänglich in  `SPHostUrl={HostUrl}&amp;SPAppWebUrl={AppWebUrl}&amp;SPLanguage={Language}&amp;SPClientTag={ClientTag}&amp;SPProductNumber={ProductNumber}` aufgelöst. Dann wird jedes dieser Token aufgelöst. Wenn kein Add-In-Webpart vorhanden ist, ist `&amp;SPAppWebUrl={AppWebUrl}` nicht enthalten. |

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15URLstrings_bk_addlresources"> </a>


-  [Erweiterte Extranetunterstützung](http://msdn.microsoft.com/library/21d67796-23c5-4339-8f0e-124208d21ab2%28Office.15%29.aspx)
    
 
-  [Abrufen von Verweisen auf Websites, Webanwendungen und andere Schlüsselobjekte](http://msdn.microsoft.com/library/8623ef1d-e3cc-426c-84a3-6379e0ae284f%28Office.15%29.aspx)
    
 
-  [Arbeiten mit Listenobjekten und Auflistungen](http://msdn.microsoft.com/library/d4167b10-6f1e-49f1-8b22-16ce20012a27%28Office.15%29.aspx)
    
 
-  [Verwenden des Objektmodells für grundlegende Aufgaben](http://msdn.microsoft.com/library/94d6898d-6a0f-43a7-ad06-1b27ec6916ea%28Office.15%29.aspx)
    
 

