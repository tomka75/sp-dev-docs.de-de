---
title: "Erstellen lokalisierter Anwendungen für Windows Phone basierend auf den SharePoint-Vorlagen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c12d7fd4-8c6b-446b-970b-1eb0e5d0a9b2
ms.openlocfilehash: 3c55a33469bc580d15a126585ce7ecac4babc841
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="build-localized-applications-for-windows-phone-based-on-the-sharepoint-templates"></a>Erstellen lokalisierter Anwendungen für Windows Phone basierend auf den SharePoint-Vorlagen
Hier erfahren Sie, wie eine lokalisierbare Windows Phone-app mithilfe der neuen SharePoint-Vorlagen erstellen Erstellen von einem anderen Windows Phone-Vorlagen mithilfe unterscheidet. SharePoint SDK für Windows Phone 7.1 installiert Windows Phone-Projektvorlagen, die Sie zum Erstellen von Windows Phone 7.1 Applications gegen SharePoint oder SharePoint 2010 verwenden können. Weitere Informationen finden Sie unter  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md). 
  
    
    

Visual Studio verwendet sprachspezifische Ressourcendateien Assemblys erstellen, die die mobile Anwendung viele Sprachen unterstützen können. Weitere Informationen zu diesem Vorgang finden Sie unter  [Verpacken und Bereitstellen von Ressourcen in Desktop-Apps](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).
> **Wichtig:** Wenn Sie die Anwendung für ostasiatische Sprachen lokalisieren möchten, müssen Sie unbedingt den Abschnitt „Schriftarten und Ihre Anwendung“ unter [Schriftartunterstützung für Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx) lesen.
  
    
    


## <a name="differences-when-building-localized-applications-for-windows-phone-using-the-sharepoint-templates"></a>Unterschiede beim Erstellen lokalisierter Anwendungen für Windows Phone unter Verwendung der SharePoint-Vorlagen

Erstellen eine lokalisierbare Windows Phone-app mithilfe der neuen SharePoint-Vorlagen ist geringfügig von einem anderen Windows Phone-Vorlagen mithilfe erstellen. Wenn Sie die SharePoint-Vorlagen verwenden, ist das **SupportedCultures** -Element ein etwas anderes Format erforderlich. Beispielsweise in einer standard Windows Phone-app, Englisch (Vereinigte Staaten) für die standardmäßige Kultur verwendet, aber auch unterstützt Deutsch (Deutschland) und Spanisch (Spanien), das **SupportedCultures**-Element wird wie folgt angezeigt:
  
    
    
 `<SupportedCultures>de-DE;es-ES;</SupportedCultures>`
  
    
    
Dieses Format funktioniert nicht, wenn Sie eine lokalisierte Windows Phone-app erstellen, die auf der SharePoint-Vorlagen basiert. Stattdessen suchen Sie das **SupportedCultures**-Element in der Datei csproj, und fügen Sie die Namen der einzelnen Kultur (Sprache), die Ihre Anwendung (andere als die standardmäßige Kultur) unterstützen muss. Trennen Sie die Namen durch Semikolons. Sie haben einen Eintrag für jede RESX-Datei, die im Projekt vorhanden ist.
  
    
    
Für das vorherige Beispiel sollte das **SupportedCultures**-Element wie folgt aussehen:
  
    
    
 `<SupportedCultures>de;es;</SupportedCultures>`
  
    
    
Eine schrittweise erklärt wird, wie Sie eine lokalisierte Anwendung für Windows Phone erstellen, finden Sie unter  [Vorgehensweise: Erstellen einer lokalisierten Anwendung für Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen einer lokalisierte Anwendung für Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).
    
  
-  [Globalisierung und Lokalisierung für Windows Phone](http://msdn.microsoft.com/library/e82118a4-6247-4d75-a16f-749677349be4%28Office.15%29.aspx)
    
  

  
    
    

