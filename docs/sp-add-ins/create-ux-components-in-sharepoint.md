---
title: Erstellen von Benutzerfreundlichkeitskomponenten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a5aadb874d4a3e9c7f86d9604cf985cbe7bebdd7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-ux-components-in-sharepoint"></a>Erstellen von Benutzerfreundlichkeitskomponenten in SharePoint
Erfahren Sie, wie Sie UX-Komponenten für Ihre Add-Ins in SharePoint erstellen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="creating-ux-components-in-sharepoint-add-ins"></a>Erstellen von UX-Komponenten in SharePoint-Add-Ins
<a name="SP15CreateUX_Creating"> </a>

Das Modell für SharePoint-Add-Ins bietet viele UX-Komponenten und Mechanismen, die Ihnen ermöglichen, in SharePoint-Add-Ins ein optimales Nutzungserlebnis zu bieten. Das Nutzungserlebnis im Add-In-Modell ist außerdem so flexibel, dass Sie die Verfahren und Plattformen verwenden können, die sich am besten an die Anforderungen von Endbenutzern anpassen lassen. In Tabelle 1 sind Ressourcen aufgeführt, die Informationen zum Erstellen und Verwenden von UX-Komponenten in Add-Ins bieten.
 

 

**Tabelle 1. Ressourcen und Anweisungen zum Erstellen von UX-Komponenten in SharePoint-Add-Ins**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md)|Sie können in Ihrem SharePoint-Add-In auf das Stylesheet einer SharePoint-Website verweisen und es zum Formatieren Ihrer Webseiten nutzen, indem Sie das Stylesheet in SharePoint verwenden. Wenn ein Benutzer das Stylesheet oder Design der SharePoint-Website ändert, können Sie außerdem die neue Gruppe von Formatvorlagen in Ihr Add-In übernehmen, ohne den Stylesheet-Verweis im Add-In ändern zu müssen.|
| [Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins](use-the-client-chrome-control-in-sharepoint-add-ins.md)|Dank des Chromsteuerelements in SharePoint können Sie den Kopfzeilenstil einer bestimmten SharePoint-Website in Ihrem Add-In verwenden, ohne eine Serverbibliothek registrieren zu müssen oder eine bestimmte Technologie bzw. ein bestimmtes Tool zu verwenden. Sie müssen dazu eine SharePoint-JavaScript-Bibliothek durch ein standardmäßiges <script>-Tag registrieren. Sie können einen Platzhalter bereitstellen, indem Sie ein HTML- **div**-Element verwenden und das Steuerelement mit den verfügbaren Optionen weiter anpassen. Das Steuerelement erhält sein Aussehen durch die angegebene SharePoint-Website.  |
| [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)|Mit Add-In-Webparts können Sie die Benutzeroberfläche Ihres Add-Ins direkt im Hostweb anzeigen. Ein Add-In-Webpart zeigt Ihren Add-In-Inhalt mithilfe eines **IFrame** an. Endbenutzer können die Oberfläche mithilfe der benutzerdefinierten Eigenschaften, die Sie für Ihr Add-In-Webpart bereitstellen können, individuell anpassen. Die Add-In-Webseite erhält die benutzerdefinierten Eigenschaftswerte durch Parameter in der Abfragezeichenfolge.|
| [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md)|Bei der SharePoint-Add-In-Erstellung ermöglichen Ihnen benutzerdefinierte Aktionen die Interaktion mit Listen und dem Menüband in der Hostwebsite. Eine benutzerdefinierte Aktion wird für die Hostwebsite bereitgestellt, wenn Endbenutzer Ihr Add-In installieren. Benutzerdefinierte Aktionen können eine Remotewebseite öffnen und durch die Abfragezeichenfolge Informationen übergeben. Für Add-Ins sind zwei Typen von benutzerdefinierten Aktionen verfügbar: Menüband und ECB (Edit Control Block).|
| [Anpassen einer Listenansicht in SharePoint-Add-Ins durch clientseitiges Rendering](customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering.md)|Durch clientseitiges Rendering wird ein Mechanismus verfügbar, mit dem Sie Ihre eigene Ausgabe für eine Gruppe von Steuerelementen, die in einer SharePoint-Seite gehostet sind, generieren können. Dieser Mechanismus ermöglicht Ihnen die Verwendung bekannter Technologien, wie HTML und JavaScript, um die Rendering-Logik von SharePoint-Listenansichten zu definieren. Beim clientseitigen Rendering können Sie Ihre eigenen JavaScript-Ressourcen angeben und sie in den für Ihre Add-Ins verfügbaren Datenspeicheroptionen, wie z. B. eine Dokumentbibliothek, hosten.|
| [Verwenden des clientseitigen Personenauswahl-Steuerelements in von SharePoint gehosteten SharePoint-Add-Ins](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins.md)|Erfahren Sie, wie das clientseitige Steuerelement „Personenauswahl" in SharePoint-Add-Ins verwendet wird. Mit dem clientseitigen Personenauswahl-Steuerelement können Benutzer schnell nach gültigen Benutzerkonten von Personen, Gruppen und Ansprüchen in ihrer Organisation suchen und diese auswählen. Bei der Auswahl handelt es sich um ein HTML- und JavaScript-Steuerelement mit browserübergreifender Unterstützung.|

## <a name="next-steps-working-with-data-in-sharepoint-add-ins"></a>Nächste Schritte: Arbeiten mit Daten in SharePoint-Add-Ins
<a name="SP15CreateUX_Next"> </a>

Haben Sie die Entwicklung einer optimalen UX für Ihr Add-In abgeschlossen? Integrieren Sie Daten mit den Mechanismen, die Ihnen im Modell für SharePoint-Add-Ins zur Verfügung stehen. Weitere Informationen finden Sie unter  [Arbeiten mit externen Daten in SharePoint](work-with-external-data-in-sharepoint.md).
 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15CreateUX_AddRes"> </a>


-  [SharePoint-Add-Ins](sharepoint-add-ins.md)
    
 
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md)
    
 
-  [Entwickeln von SharePoint-Add-ins](develop-sharepoint-add-ins.md)
    
 

