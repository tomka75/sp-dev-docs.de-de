---
title: "Übersicht über Windows Phone SharePoint-Anwendungsvorlagen in Visual Studio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6ae27957-fa41-4e6f-92e3-db11dae1f6c2
ms.openlocfilehash: c1cd9e144b5fa71d64b0a3bac46420bcc86c8b85
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-windows-phone-sharepoint-application-templates-in-visual-studio"></a>Übersicht über Windows Phone SharePoint-Anwendungsvorlagen in Visual Studio
Hier erfahren Sie mehr über die Visual Studio-Vorlagen, die vom Windows Phone SharePoint Software Development Kit für die Entwicklung mobiler Apps installiert werden.
## <a name="templates-installed-by-the-windows-phone-sharepoint-software-development-kit"></a>Vorlagen installiert, indem Sie im Windows Phone SharePoint Software Development Kit
<a name="BKMK_TemplatesInstalled"> </a>

Nachdem Sie Ihre Entwicklungsumgebung einrichten und Windows Phone SharePoint Software Development Kit (SDK) installieren, werden zwei zusätzliche Silverlight für Windows Phone-Vorlagen für Projekte verfügbar:
  
    
    

- Die Vorlage Windows Phone leeres SharePoint-Anwendung
    
  
- Die Vorlage Windows Phone SharePoint List Application
    
  
Diese Vorlagen dienen derzeit nur in C#-Projekten verwendet werden. Sie sind nicht verfügbar für Visual Basic Projekte. Die Vorlagen sind verfügbar, jedoch für die Verwendung in Visual Studio 2012 und Visual Studio Express 2012 für Windows Phone 8 und Visual Studio 2010 und Visual Studio 2010 Express für Windows Phone 7.
  
    
    

> **Hinweis:** Windows Phone SharePoint-Vorlagen werden nicht im Menü **Neues Projekt** von Expression Blend angezeigt. Sie können jedoch ein Projekt in Expression Blend bearbeiten, indem Sie **In Expression Blend öffnen** aus dem Kontextmenü in Visual Studio wählen.
  
    
    

Wenn Sie ein Projekt basierend auf einer der folgenden Vorlagen erstellen, erhalten Sie nicht die Möglichkeit, eine Windows Phone-Zielplattform. Wie bei von Visual Studio Express 2012 erstellten Projekten mithilfe dieser zielanwendungen Vorlagen Windows Phone 8 für SharePoint; Und von Visual Studio 2010 Express mithilfe von Vorlagen erstellte Projekten Windows Phone OS Version 7.1 ist standardmäßig verweisen, das **AppPlatformVersion** -Attribut des **Deployment** -Elements in der Datei WMAppManifest.xml hat den Wert 7.1.
  
    
    



```XML

<Deployment xmlns="http://schemas.microsoft.com/windowsphone/2009/deployment" AppPlatformVersion="7.1">
```


> 
>   **Hinweis:** Weitere Informationen zu den Einstellungen in der Datei WMAppManifest.xml finden Sie unter  [Application Manifest-Datei für Windows Phone](http://msdn.microsoft.com/en-us/library/ff769509.aspx). 
  
    
    


## <a name="starting-a-project-based-on-the-windows-phone-empty-sharepoint-application-template"></a>Starten eines Projekts basierend auf der Vorlage für Windows Phone Empty SharePoint-Anwendung
<a name="BKMK_EmptySPAppTemplate"> </a>

Wenn Sie ein Visual Studio Projekt basierend auf der Vorlage Windows Phone leeres SharePoint-Anwendung erstellen, ähnelt das Startprojekt eines Projekts mithilfe der Windows Phone-Anwendung-Basisvorlage (von der Windows Phone SDK 7.1 installiert), durch das Hinzufügen von Verweisen auf DLLs von Windows Phone SharePoint SDK (Microsoft.SharePoint.Client.Phone.dll, Microsoft.SharePoint.Client.Phone.Auth.UI und Microsoft.SharePoint.Client.Phone.Runtime.dll wie in Abbildung 1 dargestellt), und einigen andere Neukonfiguration installiert erstellt.
  
    
    

> **Hinweis:** Die gleichen Vorlagen stehen für Windows Phone 8 in Visual Studio Express 2012 zur Verfügung. 
  
    
    


**Abbildung 1. Dateien in einem Windows Phone Empty SharePoint-Anwendungsprojekt**

  
    
    

  
    
    
![Leeres SharePoint-Anwendungsprojekt für Windows Phone](../images/SP15_OverviewOfWinPhoneSPTemplatesInVisualStudio_fig1.PNG)
  
    
    
Die Dateien in einem Projekt auf Grundlage der Vorlage Windows Phone leeres SharePoint-Anwendung sind die standard-Dateien einer Silverlight Windows Phone-App. Die Datei MainPage.xaml enthält XAML-Deklarationen, die die Benutzeroberfläche (UI) der app zu bilden. Eine Code-Behind-Datei MainPage.xaml.cs, ist die Verwendung des Mechanismus für das partielle Klassen zugeordnet, mit der Datei MainPage.xaml, wie die anderen CodeBehind-Dateien im Projekt sind. (Siehe  [partielle Klassen und Code-Behind](http://msdn.microsoft.com/en-us/library/cc221357.aspx).) Die Datei MainPage.xaml.cs enthält Prozedurcode zum Implementieren der Logik für Vorgänge und Ereignisse in der Benutzeroberfläche zu unterstützen. Objektebene stellt die allgemeine Windows-app. Die zugeordneten Code-Behind-Datei App.xaml.cs, umfasst Prozedurcode zum Behandeln von Ereignissen für die app-Lebenszyklus.
  
    
    

## <a name="starting-a-project-based-on-the-windows-phone-sharepoint-list-application-template"></a>Starten eines Projekts basierend auf der Vorlage Windows Phone SharePoint List Application
<a name="BKMK_SPListAppTemplate"> </a>

Die Vorlage Windows Phone SharePoint List Application ist erheblich leistungsstärker als die Vorlage Windows Phone leeres SharePoint-Anwendung. Diese Vorlage wurde entwickelt, beim Erstellen von Windows Phone-apps zur Verarbeitung von einem wahrscheinlich Szenario in die Entwicklung mobiler Anwendungen für SharePoint: Zugreifen auf und Bearbeiten von Daten in einer SharePoint-Liste aus einer Windows Phone gespeichert. Wenn Sie ein auf dieser Vorlage basierende Visual Studio-Projekt erstellen, ist ein Assistent führt Sie durch die erforderlichen Konfigurationsschritte aus und generiert Lösungsdateien für eine funktionale Windows Phone-app, die mit SharePoint-Listendaten arbeiten können. Sie können erstellen und Bereitstellen die app aus dem generierten Dateien mit geringer oder ohne Änderung.
  
    
    

> **Hinweis:** Die gleichen Vorlagen stehen für Windows Phone 8 in Visual Studio Express 2012 zur Verfügung. 
  
    
    


### <a name="understanding-the-solution-files-in-a-windows-phone-sharepoint-list-application-project"></a>Grundlegendes zu den Lösungsdateien in einem Windows Phone SharePoint-Listenanwendungs-Projekt

Die für ein Visual Studio Projekt mithilfe der Vorlage Windows Phone SharePoint List Application-Dateien sind in Abbildung 2 dargestellt. (Verweise auf andere Assemblys - nicht in Abbildung 2 dargestellten - wie System.Runtime.Serialization.dll und Microsoft.Phone.Controls.dll zusätzlich zu diese Verweise durch die Vorlage Windows Phone leeres SharePoint-Anwendung enthalten sind. Diese zusätzliche Assemblys unterstützen die Verwaltung von SharePoint-Listendaten und die visuelle Steuerelemente auf diese Daten darstellen.)
  
    
    

**Abbildung 2. Dateien in einem Projekt auf Windows Phone SharePoint List Application**

  
    
    

  
    
    
![Windows Phone SharePoint-Listenanwendungs-Projekt](../images/1a9680d3-7a96-4d82-b0b9-9a9384bf96c2.gif)
  
    
    
In Tabelle 1 werden die Projektdateien für beschrieben.
  
    
    

**In Tabelle 1. Windows Phone SharePoint List Application Projektdateien**


|**Datei**|**Beschreibung**|
|:-----|:-----|
|App.xaml  <br/> |Stellt die allgemeine Windows Phone-Anwendung dar. Enthält Deklarationen der Elemente im Zusammenhang mit der Anwendung (statt auf einzelne Seiten innerhalb der Anwendung), wie die Anwendung Lebenszyklusereignisse wie **Application_Deactivated** und **Application_Closing**. <br/> |
|App.xaml.cs  <br/> |Die CodeBehind-Datei App.xaml (mithilfe des partiellen Klasse Mechanismus, wie die Groß-/Kleinschreibung für die anderen CodeBehind-Dateien in das Projekt ist) zugeordnet. So behandeln Sie die Vorgänge in Lebenszyklusereignisse wie **Application_Deactivated** und **Application_Closing**Prozedurcode enthält. Schreiben Sie Code in dieser Datei offline (local) Speicherung von Daten zu verwalten. <br/> |
|ListDataProvider.cs  <br/> |Enthält Code für den Zugriff auf Daten auf die SharePoint Server und bietet Zugriff auf die Grundlage für die verschiedenen Listenansichten der Anwendung-Abfragesyntax.  <br/> |
|List.xaml  <br/> |Definiert die Elemente der Benutzeroberfläche für das Standardformular für die Ansicht in der Anwendung Telefon; vergleichbar mit der alle Elemente (oder für alle Vorgänge, alle Kontakte oder eine ähnliche) Ansicht in SharePoint. Die Datei List.xaml enthält das **Pivot** -Steuerelement, das den primären Container für visuelle Elemente in der Anwendung, einschließlich der **PivotItem** -Steuerelemente, die die vom Entwickler in der Windows Phone-app enthalten sein gewählte Listenansichten gerendert, bildet. <br/> |
|List.xaml.cs  <br/> |Der Code-Behind-Datei List.xaml zugeordnet. Enthält Code zur Implementierung der Methoden und Ereignishandler für die Schaltflächen auf dem Formular, wie **neu** und **Aktualisieren**. <br/> |
|DisplayForm.xaml  <br/> |Definiert die Elemente der Benutzeroberfläche für das Formular zum **Anzeigen eines** Eintrags (oder die Seite) in der Anwendung; entspricht dem **Element anzeigen** Formular in SharePoint. In der Windows Phone-app werden die Felder in einer vertikalen "Stapel" mithilfe eines **StackPanel** -Steuerelements in einem Silverlight **Pivot** Steuerelement enthaltene gerendert. <br/> |
|DisplayForm.xaml.cs  <br/> |Der Code-Behind-Datei DisplayForm.xaml zugeordnet. Enthält Code zur Implementierung der Methoden und Ereignishandler für die Schaltflächen auf dem Formular, wie etwa **Bearbeiten** und **Löschen**. <br/> |
|EditForm.xaml  <br/> |Definiert die Elemente der Benutzeroberfläche für das **Element bearbeiten** Formular in der Anwendung Telefon. entspricht dem **Eintrag bearbeiten** Formular in SharePoint. Wie bei einem Formular für das **Anzeigen** werden die Felder in einem Steuerelement **StackPanel** gerendert. <br/> |
|EditForm.xaml.cs  <br/> |Der Code-Behind-Datei EditForm.xaml zugeordnet. Enthält Code zur Implementierung der Methoden und Ereignishandler für die Schaltflächen auf dem Formular, wie **Senden** und **Abbrechen**. <br/> |
|NewForm.xaml  <br/> |Definiert die Elemente der Benutzeroberfläche für das Formular **Neues Element** in der Anwendung Telefon. entspricht dem Formular **Neues Element** in SharePoint. Felder werden in einem Steuerelement **StackPanel** gerendert. <br/> |
|NewForm.xaml.cs  <br/> |Der Code-Behind-Datei NewForm.xaml zugeordnet. Enthält Code zur Implementierung der Methoden und Ereignishandler für die Schaltflächen auf dem Formular, wie **Senden** und **Abbrechen**. <br/> |
|DisplayItemViewModel.cs  <br/> |Dient als Datenquelle für die DisplayForm.xaml-Datei.  <br/> |
|EditItemViewModel.cs  <br/> |Dient als Datenquelle für die EditForm.xaml-Datei. Schreiben Sie Code in der Datei beim Bearbeiten eines Listenelements vom Benutzer eingegebenen Daten zu überprüfen.  <br/> |
|ListViewModel.cs  <br/> |Dient als Datenquelle für die List.xaml-Datei.  <br/> |
|NewItemViewModel.cs  <br/> |Dient als Datenquelle für die NewForm.xaml-Datei. Schreiben Sie Code in der Datei, die beim Hinzufügen eines neuen Listenelements vom Benutzer eingegebenen Daten zu überprüfen.  <br/> |
   
Die Informationen über die Schritte zum Erstellen einer Windows Phone-app mithilfe der Vorlage Windows Phone SharePoint List Application finden Sie unter  [Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app](how-to-create-a-windows-phone-sharepoint-list-app.md).
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15winphoneover_addlresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
-  
  [Windows Phone-Entwicklung](http://msdn.microsoft.com/en-us/library/ff402535%28v=vs.92%29.aspx)
    
  

