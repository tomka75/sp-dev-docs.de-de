---
title: Architektur der Windows Phone SharePoint-Listenanwendungsvorlage
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2c09bd02-bed0-4293-a4d4-1778692e246a
ms.openlocfilehash: 0e2c348460bf4095b684e1e7f76ebe6e61974fd4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="architecture-of-the-windows-phone-sharepoint-list-application-template"></a>Architektur der Windows Phone SharePoint-Listenanwendungsvorlage
Verstehen Sie das Entwurfsmuster von Projekten, die aus der Vorlage für Windows Phone SharePoint List Application erstellt. Die Windows Phone SharePoint List Application-Vorlage vom Windows Phone SharePoint Software Development Kit installiert wurde entwickelt, um Windows Phone-apps basierend auf einem Muster, die Teile des Projekts in verschiedenen Komponenten trennt generieren. Die Vorlage funktioniert über das Erstellen der Klassen und Dateien herstellen das Muster, da Entwickler zur Erweiterung konzentrieren generiert Projekten basierend auf ihren bestimmte Anforderungen, die Geschäftslogik und die Daten.
  
    
    


## <a name="the-windows-phone-sharepoint-list-application-template-and-the-mvvm-design-pattern"></a>Die Vorlage Windows Phone SharePoint List Application und den Entwurf MVVM-Muster
<a name="BKMK_MVVMDesignPattern"> </a>

Die Vorlage Windows Phone SharePoint List Application generiert ein Visual Studio 2010-Projekt für eine Silverlight-basierte Windows Phone-app entwickelt wurden, nach einem Software Design Muster das Muster View-Modell-ViewModel (MVVM) genannt. Das MVVM-Muster ist eine Möglichkeit zum Organisieren und Code in einem Projekt in verwaltbare Ebenen, die unabhängig voneinander entwickelt, getestet und geändert werden können, unterteilen. Es ist ein Entwicklungsmuster besonders effizient für Windows Presentation Foundation (WPF) und Silverlight-Projekten, da ein Vorteil das Muster der Darstellungsschicht einer Anwendung auf die Struktur der zugrunde liegenden Daten, Freigeben von Entwicklern die Darstellungsschicht für die verschiedenen Kontexten (als, z. B. Web Browser, Mobilgerät Schnittstellen oder desktopanwendungen) angepasst werden kann, Bildschirmdarstellung dieselben zugrunde liegenden Datenstrukturen weniger strengen abhängig sind ermöglicht.
  
    
    
Im Gegensatz zu einer einfacheren Ansatz umfasst sagen, Schreiben aller Daten-Management-Code in der CodeBehind-Dateien mit bestimmten XAML-Dateien in einer Silverlight-Anwendung ein Projekt entsprechend der MVVM-Muster organisieren verknüpft ist eine zusätzliche anfängliche Investition von Aufwand zu planen und entwickeln die erforderlichen Klassen, die Vererbungsmodell und die Methoden der Kommunikation zwischen den Komponenten des Musters. Die Vorlage Windows Phone SharePoint List Application kümmert dieser anfänglichen Konfiguration und Entwicklung Aufgaben zum Einrichten von dem Muster für Sie, sodass Sie anpassen und Erweitern des Projekts, um eine funktionsfähige MVVM-Anwendung schnell zu entwickeln.
  
    
    
Die drei Hauptkomponenten oder Ebenen der MVVM-Muster werden die Ansicht, das Modell und das Ansichtsmodell. In Projekten basierend auf der Vorlage Windows Phone SharePoint List Application werden diese Komponenten von verschiedenen Project-Dateien implementiert, wie in Abbildung 1 dargestellt.
  
    
    

**Abbildung 1. Windows Phone SharePoint List Application Dateien in das MVVM-Muster**

  
    
    

  
    
    
![Vorlagendateien im MVVM-Muster](../images/96681da7-ceab-40f3-8d08-441aea9b4a6f.gif)
  
    
    
Den folgenden Abschnitten werden einige der Details im Zusammenhang mit der Implementierung dieser Komponenten in die Vorlage Windows Phone SharePoint List Application.
  
    
    

### <a name="the-model-component"></a>Die Model-Komponente

Die Komponente Model in MVVM-Muster bezieht sich auf die Klassen und Strukturen verwendet, um die Daten für eine Anwendung darstellen. Für eine app basierend auf einer SharePoint-Liste zu der Liste und seine Elemente als die zugrunde liegenden Daten verarbeiten. In Windows Phone SharePoint List Application übernimmt die Klasse **ListDataProvider** SharePoint-Client-Objektmodell Standardfunktionen für die Verbindung mit einer SharePoint-Liste. beispielsweise erstellen eine Instanz der Klasse **ClientContext** und Festlegen seiner Eigenschaften. Die genaue Implementierungsdetails der **ListDataProvider** -Klasse in der Vorlage hängen die Optionen in den Schritten des Assistenten für SharePoint Phone-Anwendung angegeben wird, wenn Sie ein Projekt basierend auf der Vorlage erstellen.
  
    
    
Die Basisklasse implementiert **ListDataProviderBase** (in Microsoft.SharePoint.Phone.Application.dll), von denen die **ListDataProvider** -Klasse abgeleitet ist einen Mechanismus für das Zwischenspeichern für SharePoint-Listendaten. Listenelemente aus dem Server abgerufen werden, werden sie von der **ListDataProvider** -Klasse in der lokalen Speichers zu Phone-app zwischengespeichert, und diese Elemente in der app benötigt, des Caches zum Einsparen von Ressourcen und Reduzierung von Reisen an den Server zuerst aktiviert wird.
  
    
    
Wenn das Filtern der Daten von der SharePoint-Liste abgerufen, oder geben Sie genau welche Daten abgerufen werden soll, können Sie den Code in der **ListDataProvider** -Klasse (in der Datei ListDataProvider.cs) ändern. Die Teile der Datei, die Sie für diese Zwecke wahrscheinlich ändern würde werden die **LoadDataFromServer** -Methode und die Implementierung der statischen **CamlQueryBuilder** -Klasse. Sie können auch eine eigene Klasse von der Klasse **ListDataProviderBase** ableiten. Wenn Sie dies tun, müssen Sie unbedingt die abstrakten Methoden aus der Basisklasse, **LoadData** und **LoadItem**implementieren, und auch Implementieren des **Context** -Eigenschaft Mitglieds der Basisklasse, eine geeignete **get** Accessor-Methode bereitgestellt.
  
    
    

### <a name="the-view-component"></a>Die Komponente anzeigen

Die Ansichtskomponente in MVVM-Muster bezieht sich auf der Benutzeroberfläche (UI) einer app. In Silverlight-basierten Windows Phone-app wird die Ansichtskomponente darstellten von XAML-Dateien zum Deklarieren und Kennzeichnen von Benutzeroberflächenelementen und CodeBehind-Dateien, die die Verwendung von XAML-Dateien, die implementieren Ereignishandler und anderen Code zum Bestimmen der Interaktion zwischen Benutzern mit der UI-Elemente zugeordnet.
  
    
    
Es ist wichtig, zwischen zwei Sinne des Worts "anzeigen" im Zusammenhang mit der Entwicklung von apps für SharePoint-Liste für Windows Phone zu unterscheiden. Eine SharePoint-Liste ist eine oder mehrere Ansichten, wie beispielsweise, alle Elemente als Standardansicht für eine Liste oder eine Liste basierend auf der Listenvorlage Kalender in der Ansicht Aktuelle Ereignisse zugeordnet. Diese Ansichten stellen Möglichkeiten zum Organisieren und Anzeigen von Listenelementen in einer SharePoint-Liste dar. Je nach Art der SharePoint-Liste (und gibt an, ob benutzerdefinierte Ansichten der Liste hinzugefügt wurden) Ziel für Ihre app, die Ansichten der Liste aus, wie alle Aufgaben oder aktuelle Ereignisse zugeordnet werden zur Verfügung gestellt, die festlegen, dass Ihre app in den Assistenten für SharePoint Phone-Anwendung einschließen, wenn Sie ein Projekt aus der Vorlage erstellen. Wenn Sie eine bestimmte Ansicht einfügen, generiert die Vorlage ein **PivotItem** -Steuerelement (ein **Pivot** Steuerelement enthaltene) zum Rendern der Ansicht der Liste.
  
    
    
In diesem Sinne "anzeigen" ist von im Sinne des Worts unterschieden werden, wie sie auf die Ansichten in der Vorlage angewendet wird. Finden Sie in einem Projekt basierend auf der Vorlage Windows Phone SharePoint List Application (implementierten als XAML-Dateien im Ordner "Ansichten" des Projekts) Konzept in der Ansicht-Komponente des MVVM-Muster. D. h., stellen die Ansichten im Projekt die Darstellungsschicht für die Daten (oder Modell) einer gegebenen Entität dar. In diesem Fall ist die Entität einer SharePoint-Liste oder eine SharePoint-Listenelement.
  
    
    
Obwohl das Listenformular (List.xaml) im Projekt bezeichnet werden kann, um die Standardansicht einer SharePoint-Liste, die konzeptionelle Unterschied zwischen Standardansicht des einer SharePoint-Liste und der Ansicht durch die Liste dargestellt, das Formular weiterhin beibehalten werden soll, zugeordnet, da das Listenformular im Projekt unbedingt die Standardansicht der Liste auf dem Server zugeordnet ist, entspricht. Wenn Sie beispielsweise ändern Sie die standardmäßige Listenansicht auf dem Server (durch, beispielsweise eine bestimmte Sortierreihenfolge angeben oder Anzeigen bestimmter Felder und andere nicht), die Änderungen werden nicht in der XAML-Code, der das Listenformular im Projekt, bildet dargestellt werden. Legen Sie die Reihenfolge der Elemente, wie sie in der Liste angezeigt werden, Formular in Ihrer app basierend auf Ihrer Auswahl im Application-Assistent für SharePoint-Telefon (oder basierend auf der nachfolgenden Anpassungen des Listenformulars), unabhängig von der Reihenfolge für die Standardansicht zugeordneten SharePoint-Liste auf dem Server konfiguriert sind.
  
    
    
Das Listenformular stellt die Ansicht (oder der Darstellungsschicht) für die SharePoint-Liste. Die drei Ansichtsdateien beziehen sich auf einzelne Listenelemente, und sie gilt der verfügbaren Formulare (Allgemein) entsprechen der Liste Element im Menü für ein Listenelement in SharePoint.
  
    
    

- Das Formular anzeigen (DisplayForm.xaml) entspricht dem Element anzeigen-Formular (DispForm.aspx) für eine SharePoint-Liste. Dieses Formular stellt eine Ansicht für ein einzelnes Element in einer SharePoint-Liste.
    
  
- Mit dem Bearbeitungsformular (EditForm.xaml) entspricht dem Eintrag bearbeiten-Formular (EditForm.aspx) für eine SharePoint-Liste. Dieses Formular stellt eine Ansicht für ein bestimmtes Element zur Bearbeitung verfügbar gemacht wird.
    
  
- Die neue Formulardatei (NewForm.xaml) entspricht dem Formular neues Element (NewForm.aspx), für eine SharePoint-Liste. Dieses Formular stellt eine Ansicht für ein bestimmtes Element, das erstellt und der Liste hinzugefügt werden soll.
    
  
Das Listenformular ist immer in einem Projekt auf Grundlage der Vorlage Windows Phone SharePoint List Application standardmäßig enthalten. Die XAML-Dateien für die anderen Formulare im Ordner "Ansichten" des Projekts werden generiert basierend auf der List-Vorgängen (New, anzeigen oder bearbeiten) in den Assistenten für SharePoint Phone-Anwendung aktiviert.
  
    
    

### <a name="the-viewmodel-component"></a>Der ViewModel-Komponente

Die ViewModel-Komponente in MVVM-Muster soll dienen als eine Art Broker vereinfachen die Interaktionen zwischen der Ansichtskomponente und das Modell-Komponente, während die Ansichtskomponente aus der Komponente Modell entkoppeln, daher es einfacher ist, eine oder anderen ändern, wirkt sich negativ auf die andere. Genau genommen konnte die ViewModel-Komponente Teil der Darstellungsschicht angesehen werden, da sie häufig Logik für die zugrunde liegenden Daten für die Präsentation in der Ansichtskomponente "Gestaltung" enthält. In Projekten basierend auf der Vorlage Windows Phone SharePoint List Application, implementieren Sie die ViewModels den Code für das Binden von SharePoint-Listendaten aus der Objektmodell-Komponente abgerufen (d. h., ein Objekt von der Klasse **ListDataProvider** ) zu UI-Steuerelementen in einem Teil der Ansicht-Komponente (beispielsweise dem Formular bearbeiten). Abhängig von der Art des Steuerelements zum Anzeigen der Daten aus der Liste und den Typ der Daten (d. h., ob der Feldtyp für das Listenelement Text oder numerische Daten oder etwa ein Auswahlfeld mit SharePoint ist), das Ansichtsmodell zuerst verarbeitet oder konvertiert die Daten, sodass es für ein bestimmtes UI-Steuerelement gebunden werden kann.
  
    
    
Insbesondere das Ansichtsmodell Steuerelementklassen im Projekt (wie, beispielsweise die **EditItemViewModel** -Klasse) eine Basisklasse **ViewModelBase** (in Microsoft.SharePoint.Phone.Application.dll), die die **INotifyPropertyChanged** -Schnittstelle implementiert, damit die Silverlight-Steuerelemente die Benutzeroberfläche der app bildet aktualisiert werden können, wenn Werte in der zugrunde liegenden Daten geändert werden (und sollte in der anderen Richtung) Ändern der Werte in der UI-Steuerelemente gespeichert (wenn bidirektionale auf die zugrunde liegenden Daten angewendet werden abgeleitet sind oder "bidirektionale" Bindung für ein Steuerelement konfiguriert).
  
    
    
Abbildung 2 zeigt eine vereinfachte Darstellung der Klassenvererbungshierarchie für die **EditItemViewModel** -Klasse und die Bindung für ein angegebenes UI-Steuerelement in dem Formular bearbeiten, mit das entsprechende Feld in der ViewModel.
  
    
    

**Abbildung 2. Die Klassen EditItemViewModel und EditForm**

  
    
    

  
    
    
![Die Klassen "EditItemViewModel" und "EditForm"](../images/9faa4fbc-5fd6-4960-ba25-8a8cc0195562.gif)
  
    
    
Die **EditForm** -Klasse (die die Ansicht-Komponente aus dem MVVM-Muster darstellt) ist definiert und von zwei Dateien, die EditForm.xaml und die zugeordneten Code-Behind-Datei EditForm.xaml.cs implementiert. In der Datei EditForm.xaml.cs ist die **EditItemViewModel** -Klasse (für die ViewModel-Komponente von MVVM-Muster) auf die Ansicht in der Datei EditForm.xaml.cs durch Festlegen der **DataContext** -Eigenschaft der **EditForm** -Klasse auf ein Objekt der Klasse **EditItemViewModel** gebunden.
  
    
    
Auf MVVM-Mustern basierende Software-Designs beschränken häufig die Geschäftslogik und Überprüfungsroutinen für die Modellkomponente des Musters. In Projekten auf Grundlage der Listenanwendungsvorlage für Windows Phone SharePoint wurden einige Vorgänge, die in der Regel als Teil der Modellkomponente angesehen werden, in die ViewModel-Komponente implementiert, damit Entwickler die Projekte bequemer erweitern können, wodurch allerdings der konzeptionelle Unterschied zwischen der Datenschicht (Model) und der Darstellungsschicht (ViewModel) leicht verschwimmt. Zum Beispiel machen die ViewModel-Klassen für das Bearbeiten und Erstellen von Listenelementen (d.h. **EditItemViewModel**- und **NewItemViewModel**-Klassen) eine **Überprüfungsmethode** verfügbar, die Entwickler überschreiben können, um eine Überprüfung der von Benutzern eingegebenen Daten implementieren zu können. (Informationen zur Implementierung der Datenüberprüfung mit den ViewModels finden Sie unter [Vorgehensweise: Geschäftslogik und Datenüberprüfung in eine Windows Phone-App für SharePoint implementieren](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md))
  
    
    

    
> **Hinweis:** Das **ListDataProvider**-Objekt lädt die Daten nur vom Server. Andere Vorgänge, wie z. B. **Hinzufügen**, **Aktualisieren** und **Löschen**, werden im ViewModel selbst durchgeführt. Anschließend erfolgt ein Aktualisierungsaufruf, um die ViewModel-Daten vom Server zu aktualisieren. Dieses Design reduziert die Überladung des Codes. 
  
    
    


## <a name="the-appxaml-file-and-the-silverlight-application-model"></a>Die Datei App.xaml und das Silverlight-Anwendungsmodell
<a name="BKMK_ApplicationModel"> </a>

Objektebene und seine zugeordneten Code-Behind-Datei App.xaml.cs, sind Standardkomponenten einer verwalteten Silverlight-Anwendung. Anwendungen, mit denen die verwaltete API für Silverlight müssen eine Klasse, die von der Silverlight-  [Anwendung](http://msdn.microsoft.com/en-us/library/system.windows.application%28VS.95%29.aspx) -Klasse abgeleitet sind, um das Silverlight-Anwendungsmodell implementieren enthalten. Die **Application** -Klasse unterstützt Anwendung Lebenszyklusereignisse und Funktionen für die Verwaltung von Ressourcen wie Bilder, Zeichenfolgen und XAML-Vorlagen.
  
    
    
Informationen dazu, welche Arten von Änderungen, die Sie an der Datei App.xaml.cs in Projekten möglicherweise, finden Sie unter  [Vorgehensweise: anmelden und Fortsetzen von Anrufen SharePoint Listenelementen auf einem Telefon mit Windows](how-to-store-and-retrieve-sharepoint-list-items-on-a-windows-phone.md) zum Implementieren der Ereignishandler in der Datei App.xaml.cs Anwendung Zustandsinformationen und [Vorgehensweise: Verwenden mehrerer 2013 für SharePoint-in ein Windows Phone-app Listen](how-to-use-multiple-sharepoint-lists-in-a-windows-phone-app.md) für das Instanziieren und Konfigurieren von zusätzlichen **ListDataProvider** -Objekten in App.xaml.cs beibehalten.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Winphoneover_addlresources"> </a>


-  
  [Unter Verwendung des Model-View-ViewModel-Musters](http://msdn.microsoft.com/en-us/library/hh821028.aspx)
    
  
-  
  [Architektur des Pivot-Steuerelements für Windows Phone](http://msdn.microsoft.com/en-us/library/ff941097%28VS.92%29.aspx)
    
  
-  
  [Silverlight-Anwendungsmodell](http://msdn.microsoft.com/en-us/library/cc872869%28VS.95%29.aspx)
    
  
-  
  [Entwickeln einer Windows Phone-Anwendung mit dem MVVM-Muster](http://msdn.microsoft.com/en-us/library/hh848247.aspx)
    
  
-  [Die Model-View-ViewModel Entwurfsmuster WPF-Apps](http://msdn.microsoft.com/en-us/magazine/dd419663.aspx)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

