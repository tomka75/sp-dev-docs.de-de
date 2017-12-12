---
title: "Sprachenunterstützung für Windows Phone in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2c396a91-0fc1-4e25-942b-fffad49bd2c6
ms.openlocfilehash: cf88870f273399d8dea044626f96766967fa071d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="language-support-for-windows-phone-in-sharepoint"></a>Sprachenunterstützung für Windows Phone in SharePoint
Informationen Sie zu sprachunterstützung für die Visual Studio-Vorlagen, die von SharePoint Software Development Kit (SDK) für Windows Phone für die Entwicklung mobiler Apps installiert werden. Um die mobile Anwendung für mehrere Sprachen zu entwickeln, müssen Sie zum Globalisieren und lokalisieren Sie die Anwendung. Die meisten Globalisierung und Lokalisierung Funktionen, die Sie benötigen, um zu implementieren ist bereits in die .NET Framework integriert. Mithilfe dieser Funktion können Sie Kunden in anderen Ländern und Regionen erreichen.
  
    
    

Windows Phone SDK enthält Visual Studio 2010 Express für Windows Phone, Windows Phone-Emulator, XNA Spiel Studio und Expression Blend. Installieren Sie Sie zuerst die  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570) für die Entwicklung für Windows Phone. Installieren Sie dann den [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476) zum Installieren von SharePoint-Vorlagen für Windows Phone. Nachdem Sie Ihre Entwicklungsumgebung einrichten und des SharePoint-SDK für Windows Phone installieren, finden Sie unter  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).
  
    
    

Weitere Informationen zu den SharePoint-Vorlagen für Windows Phone finden Sie unter  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).
## <a name="templates-and-libraries-installed-by-the-sharepoint-sdk-for-windows-phone"></a>Vorlagen und Bibliotheken installiert, indem Sie im SharePoint SDK für Windows Phone
<a name="LanguageSupportForWindowsPhoneForSharePoint2013_TemplatesInstalledBySharePointSDKForWindowsPhone"> </a>

SharePoint SDK für Windows Phone 7.1 installiert die Client-Objektmodell (CSOM) Objektbibliotheken für Windows Phone, die SharePoint Auth-Bibliothek für Windows Phone und Windows Phone-Projektvorlagen, die Sie zum Erstellen von Windows Phone 7.1 Applications gegen SharePoint oder SharePoint 2010 verwenden können.
  
    
    
Bei der Installation von SharePoint SDK für Windows Phone stehen zwei zusätzliche Silverlight für Windows Phone-Vorlagen für Projekte:
  
    
    

- Windows Phone leeres SharePoint-Anwendung
    
  
- Windows Phone-SharePoint-Listen-App
    
  

## <a name="localized-versions-of-the-sharepoint-sdk-for-windows-phone"></a>Lokalisierte Versionen von SharePoint SDK für Windows Phone
<a name="LanguageSupportForWindowsPhoneForSharePoint2013_LocalizedVersionsOfSharePointSDKForWindowsPhone"> </a>

Neun verschiedenen Sprachen werden von SharePoint SDK für Windows Phone Developer Toolkit 7.1 unterstützt. Die meisten Aufgaben beim Erstellen einer Anwendung erfolgt zur Entwurfszeit, einschließlich des Erstellens von Projekten, Entwerfen von Formularen, entwickeln Steuerelemente und Code hinzufügen. Sie können Windows Phone-Anwendungen schreiben, mit einer der folgenden lokalisierten Versionen von SharePoint SDK für Windows Phone:
  
    
    

- Englisch (En-US)
    
  
- Französisch (fr-FR)
    
  
- Deutsch (de-DE)
    
  
- Italienisch (it-IT)
    
  
- Japanisch (ja-JP)
    
  
- Koreanisch (Ko-KR)
    
  
- Russisch (ru-RU)
    
  
- Spanisch (es-ES)
    
  
- Chinesisch (traditionell) (Zh-TW)
    
  

## <a name="supported-localized-languages-for-sharepoint-windows-phone-applications"></a>Unterstützte lokalisierte Sprachen für Windows Phone SharePoint-Anwendungen
<a name="bk_supplocallangs"> </a>

Wenn eine Anwendung die Steuerung übernimmt, interagieren Sie mit der Anwendung auf die gleiche Weise wie ein Benutzer. Sie können Code anzuzeigen, führen Sie die Anwendung und Debuggen, aber den Code kann nicht geändert werden.
  
    
    
Obwohl Sie den programmgesteuerten Zugriff auf neun verschiedenen Sprachen haben, können Sie Ihre mobilen SharePoint-Anwendungen in den zwanzig Sprachen, die in Tabelle 1 dargestellt ausführen.
  
    
    

**In Tabelle 1. Unterstützte anzeigen/Laufzeitfehler Sprachen im SharePoint SDK für Windows Phone**


|**Kulturnamen**|**Kulturcode**|
|:-----|:-----|
|Vereinfachtes Chinesisch (VR China)  <br/> |zh-CN  <br/> |
|Traditionelles Chinesisch (Taiwan)  <br/> |zh-TW  <br/> |
|Tschechisch (Tschechische Republik)  <br/> |cs  <br/> |
|Dänisch (Dänemark)  <br/> |da  <br/> |
|Niederländisch (Königreich der Niederlande)  <br/> |nl  <br/> |
|Finnisch (Finnland)  <br/> |fi  <br/> |
|Französisch (Frankreich)  <br/> |fr  <br/> |
|Deutsch (Deutschland)  <br/> |de  <br/> |
|Griechisch (Griechenland)  <br/> |el  <br/> |
|Ungarisch (Ungarn)  <br/> |hu  <br/> |
|Italienisch (Italien)  <br/> |it  <br/> |
|Japanisch (Japan)  <br/> |ja  <br/> |
|Koreanisch (Korea)  <br/> |ko  <br/> |
|Norwegisch (Norwegen)  <br/> |nb  <br/> |
|Polnisch (Polen)  <br/> |pl  <br/> |
|Portugiesisch (Brasilien)  <br/> |pt-BR  <br/> |
|Portugiesisch (Portugal)  <br/> |pt-PT  <br/> |
|Russisch (Russland)  <br/> |ru  <br/> |
|Spanisch (Spanien)  <br/> |es  <br/> |
|Schwedisch (Schweden)  <br/> |sv  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  

  
    
    

