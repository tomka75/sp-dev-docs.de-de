---
title: "Übersicht über Designs für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ae585dd3-82fe-46bb-ac93-065edc0a16f4
ms.openlocfilehash: 71c89a8e86f50e4716d0a817b0ab818b563ff473
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="themes-overview-for-sharepoint"></a>Übersicht über Designs für SharePoint
In diesem Artikel erfahren Sie mehr über die Designoberfläche in SharePoint und darüber, wie das Erscheinungsbild von Websites mithilfe von Designs angepasst werden kann.
## <a name="themes-overview"></a>Designübersicht
<a name="section1"> </a>

Designs stellen einen einfachen und schnellen Weg zur Verfügung, einer SharePoint-Website einfaches Branding hinzuzufügen. Mit einem Design kann ein Websitebesitzer oder ein Benutzer mit Designerrechten eine Website anpassen, indem er das Layout der Website, die Farbpalette, das Schriftartenschema und das Hintergrundbild ändert.
  
    
    
Die Designoberfläche in SharePoint wurde neu gestaltet, um das Verfahren zur Anpassung von Websites zu vereinfachen. Die Designbenutzeroberfläche wurde neu entworfen, und es gibt es eine Reihe neuer Dateiformate für Designs. Der Assistent **Erscheinungsbild ändern** ist der Einstiegspunkt in die Designoberfläche. Hier können Sie das Erscheinungsbild Ihrer Website ändern. Sie können ein Design für die Website auswählen. Anschließend können Sie das Design durch Ändern des Websitelayouts, des Hintergrunds, der Farbpalette oder des Schriftartenschemas anpassen. Bevor Sie das Design übernehmen, können Sie eine Vorschau der Website anzeigen. Weitere Informationen finden Sie unter [Auswählen eines Designs für Ihre Veröffentlichungswebsite](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx) auf Office.com.
  
    
    

> **Hinweis:** In SharePoint 2010 erstellte Designs können nicht auf SharePoint-Websites verwendet werden. In SharePoint 2010 erstellte Designs können jedoch weiterhin in Websitesammlungen verwendet werden, die nicht aktualisiert wurden, oder in Websitesammlungen, in denen die Oberflächenversion von 2010 verwendet wird. 
  
    
    


## <a name="theming-experience-components"></a>Komponenten der Designoberfläche
<a name="section2"> </a>

Die Designoberfläche besteht aus den folgenden Komponenten:
  
    
    
 **Farbpalette**: Über eine Farbpalette (oder einem Farbschema) wird die Kombination der Farben definiert, die auf einer Website verwendet werden. Mit SharePoint sind 32 Farbpaletten installiert. Sie stehen Benutzern zur Verfügung, wenn diese ein Design in der Design Gallery ändern möchten.
  
    
    
Farbpaletten sind XML-Dateien (SPCOLOR-Dateien). Sie sind im Designkatalog der Stammwebsite der Websitesammlung im Ordner **15** gespeichert (http:// _SiteCollectionName_/_catalogs/theme/15/).
  
    
    
 **Schriftartenschema**: Mit einem Schriftartenschema werden die auf einer Website verwendeten Schriftarten definiert. Sieben Schriftartenschemas sind in SharePoint enthalten. Sie stehen Benutzern zur Verfügung, wenn sie ein Design in der Design Gallery ändern möchten.
  
    
    
Schriftartenschemas sind XML-Dateien (SPFONT-Dateien). Sie sind im Designkatalog der Stammwebsite der Websitesammlung im Ordner **15** gespeichert (http:// _SiteCollectionName_/_catalogs/theme/15/).
  
    
    
 **Hintergrundbild**: Das auf der Website verwendete Hintergrundbild.
  
    
    
 **Gestaltungsvorlage**: Mit einer Gestaltungsvorlage wird das Chrome (die gemeinsam genutzten Rahmenelemente) einer Website definiert. Auf der Designoberfläche können Benutzer die Gestaltungsvorlage auswählen, die auf eine Website angewendet werden soll.
  
    
    
 **Gestaltungsvorlagenvorschau**: Eine Gestaltungsvorlagenvorschau wird verwendet, um ein Vorschaubild der ausgewählten Designkomponenten zu rendern. Jede Gestaltungsvorlage muss über eine entsprechende Vorschaudatei für die Gestaltungsvorlage verfügen, damit die Gestaltungsvorlage auf der Designoberfläche verfügbar ist.
  
    
    
Vorschaudateien für Gestaltungsvorlagen (PREVIEW-Dateien) werden im Gestaltungsvorlagenkatalog der Website gespeichert (http://  _SiteName_/_catalogs/masterpage/).
  
    
    
 **Durchkomponierter Look**: Ein durchkomponierter Look bzw. ein Design besteht aus der Farbpalette, dem Schriftartenschema, dem Hintergrundbild und der Gestaltungsvorlage, die das Erscheinungsbild einer Website bestimmen. Die Begriffe Entwurf und Design sind austauschbar und beschreiben beide das Gesamterscheinungsbild einer Website.
  
    
    
Auf der Designoberfläche werden verfügbare Entwürfe anhand der Liste der durchkomponierten Looks ermittelt. Zusätzliche Entwürfe können Sie erstellen, indem Sie Listenelemente in der Liste der durchkomponierten Looks erstellen. Um auf die Liste der durchkomponierten Looks zuzugreifen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** die Option **Durchkomponierte Looks** aus.
  
    
    
 **Erscheinungsbild ändern**: Der Assistent **Erscheinungsbild ändern** ist der Einstiegspunkt in die Designoberfläche. Hier können Benutzer das Erscheinungsbild ihrer Website ändern. Sie greifen auf den Assistenten **Erscheinungsbild ändern** zu, indem Sie das Symbol **Einstellungen** auswählen und anschließend **Erscheinungsbild ändern** auswählen.
  
    
    
 **Design Gallery**: Die Design Gallery ist die erste Seite des Assistenten **Erscheinungsbild ändern**. In der Design Gallery wird eine Miniaturansicht sämtlicher verfügbarer Designs angezeigt.
  
    
    

## <a name="using-themes"></a>Verwenden von Designs
<a name="section3"> </a>

SharePoint enthält vorinstallierte Designs (auch als Entwürfe oder durchkomponierte Looks bezeichnet). Sie können die vorinstallierten Designs verwenden oder eigene benutzerdefinierte Designs erstellen.
  
    
    

### <a name="preinstalled-themes"></a>Vorinstallierte Designs

Auf der Designoberfläche können Benutzer vorinstallierte Designs anpassen, indem sie die Farben, die Schriftarten, das Layout oder das Hintergrundbild ändern. Sie müssen keine benutzerdefinierten Designs erstellen, es sei denn, Sie benötigen zusätzliche Schriftartenschemas oder Farbpaletten.
  
    
    
Wenn ein vorinstalliertes Design geändert wird, wird automatisch ein neues Design mit der Bezeichnung Aktuell erstellt, nachdem die Designänderungen angewendet wurden. Es gibt nur ein aktuelles Design für eine Website. SharePoint ermöglicht es dem Benutzer nicht, Designs über die Benutzeroberfläche zu speichern. Wenn Sie ein vorinstalliertes Design ändern, die Änderungen anwenden (ein neues Design mit der Bezeichnung Aktuell wird erstellt) und dann ein zweites vorinstalliertes Design ändern, wird das zweite vorinstallierte Design zum aktuellen Design, wenn die Einstellungen angewendet werden. Wenn Sie ein geändertes Design speichern möchten, können Sie in der Liste der zusammengesetzten Designs ein Listenelement erstellen, das dieselbe Masterseite-URL, Farbschema-URL, Schriftartenschema-URL und Hintergrundbild-URL enthält (das geänderte Design erhält in der Liste der zusammengesetzten Designs die Bezeichnung Aktuell).
  
    
    

### <a name="custom-themes"></a>Benutzerdefinierte Designs

Sie können benutzerdefinierte Designs erstellen, indem Sie zusätzliche Farbpaletten und Schriftartenschemas erstellen und diese in den Designkatalog hochladen. Die neuen Farbpaletten und Schriftartenschemas stehen Ihnen dann auf der Designoberfläche zur Verfügung oder wenn Sie ein Design programmgesteuert anwenden möchten. Wenn Sie weitere Websitelayouts wünschen, um daraus wählen zu können, können Sie auf ähnliche Weise zusätzliche Gestaltungsvorlagen sowie entsprechende Vorschaudateien in den Gestaltungsvorlagenkatalog hochladen.
  
    
    
Neue Designs können Sie erstellen, indem Sie neue Listenelemente in der Liste der durchkomponierten Looks erstellen. Erstellen Sie ein Listenelement, und geben Sie dann die Gestaltungsvorlage, die Farbpalette, das Schriftartenschema und das Hintergrundbild für das neue Design an.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="section4"> </a>


-  [SharePoint Design Manager - Branding- und Designfunktionen](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  
-  [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  

