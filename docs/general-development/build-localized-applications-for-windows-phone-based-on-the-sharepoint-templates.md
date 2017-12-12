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
# <a name="build-localized-applications-for-windows-phone-based-on-the-sharepoint-templates"></a><span data-ttu-id="14610-102">Erstellen lokalisierter Anwendungen für Windows Phone basierend auf den SharePoint-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="14610-102">Build localized applications for Windows Phone based on the SharePoint templates</span></span>
<span data-ttu-id="14610-p101">Hier erfahren Sie, wie eine lokalisierbare Windows Phone-app mithilfe der neuen SharePoint-Vorlagen erstellen Erstellen von einem anderen Windows Phone-Vorlagen mithilfe unterscheidet. SharePoint SDK für Windows Phone 7.1 installiert Windows Phone-Projektvorlagen, die Sie zum Erstellen von Windows Phone 7.1 Applications gegen SharePoint oder SharePoint 2010 verwenden können. Weitere Informationen finden Sie unter  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="14610-p101">Learn how building a localizable Windows Phone app using the new SharePoint templates is different from building one using other Windows Phone templates. The SharePoint SDK for Windows Phone 7.1 installs Windows Phone project templates, which you can use to build Windows Phone 7.1 applications against SharePoint or SharePoint 2010. For more information, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span> 
  
    
    

<span data-ttu-id="14610-p102">Visual Studio verwendet sprachspezifische Ressourcendateien Assemblys erstellen, die die mobile Anwendung viele Sprachen unterstützen können. Weitere Informationen zu diesem Vorgang finden Sie unter  [Verpacken und Bereitstellen von Ressourcen in Desktop-Apps](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="14610-p102">Visual Studio uses language-specific resource files to create assemblies that allow your mobile application to support many languages. For more information about this process, see  [Packaging and Deploying Resources in Desktop Apps](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).</span></span>
> <span data-ttu-id="14610-108">**Wichtig:** Wenn Sie die Anwendung für ostasiatische Sprachen lokalisieren möchten, müssen Sie unbedingt den Abschnitt „Schriftarten und Ihre Anwendung“ unter [Schriftartunterstützung für Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx) lesen.</span><span class="sxs-lookup"><span data-stu-id="14610-108">**Important:** If you plan to localize your application for East Asian languages, be sure to read the "Fonts and Your Application" section of  [Font Support for Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx)</span></span>
  
    
    


## <a name="differences-when-building-localized-applications-for-windows-phone-using-the-sharepoint-templates"></a><span data-ttu-id="14610-109">Unterschiede beim Erstellen lokalisierter Anwendungen für Windows Phone unter Verwendung der SharePoint-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="14610-109">Differences when building localized applications for Windows Phone using the SharePoint templates</span></span>

<span data-ttu-id="14610-p103">Erstellen eine lokalisierbare Windows Phone-app mithilfe der neuen SharePoint-Vorlagen ist geringfügig von einem anderen Windows Phone-Vorlagen mithilfe erstellen. Wenn Sie die SharePoint-Vorlagen verwenden, ist das **SupportedCultures** -Element ein etwas anderes Format erforderlich. Beispielsweise in einer standard Windows Phone-app, Englisch (Vereinigte Staaten) für die standardmäßige Kultur verwendet, aber auch unterstützt Deutsch (Deutschland) und Spanisch (Spanien), das **SupportedCultures**-Element wird wie folgt angezeigt:</span><span class="sxs-lookup"><span data-stu-id="14610-p103">Building a localizable Windows Phone app using the new SharePoint templates is slightly different from building one using other Windows Phone templates. When you use the SharePoint templates, the **SupportedCultures** element requires a slightly different format. For example, in a standard Windows Phone app that uses English (United States) for its default culture but also supports German (Germany) and Spanish (Spain), the **SupportedCultures** element appears as follows:</span></span>
  
    
    
 `<SupportedCultures>de-DE;es-ES;</SupportedCultures>`
  
    
    
<span data-ttu-id="14610-p104">Dieses Format funktioniert nicht, wenn Sie eine lokalisierte Windows Phone-app erstellen, die auf der SharePoint-Vorlagen basiert. Stattdessen suchen Sie das **SupportedCultures**-Element in der Datei csproj, und fügen Sie die Namen der einzelnen Kultur (Sprache), die Ihre Anwendung (andere als die standardmäßige Kultur) unterstützen muss. Trennen Sie die Namen durch Semikolons. Sie haben einen Eintrag für jede RESX-Datei, die im Projekt vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="14610-p104">This format does not work when you build a localized Windows Phone app that is based on the SharePoint templates. Instead, locate the **SupportedCultures** element in the .csproj file and add the names of each culture (language) that your application needs to support (other than the default culture). Separate the names using semicolons. You should have an entry for each .resx file that is in the project.</span></span>
  
    
    
<span data-ttu-id="14610-117">Für das vorherige Beispiel sollte das **SupportedCultures**-Element wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="14610-117">For the previous example, the **SupportedCultures** element should appear as follows:</span></span>
  
    
    
 `<SupportedCultures>de;es;</SupportedCultures>`
  
    
    
<span data-ttu-id="14610-118">Eine schrittweise erklärt wird, wie Sie eine lokalisierte Anwendung für Windows Phone erstellen, finden Sie unter  [Vorgehensweise: Erstellen einer lokalisierten Anwendung für Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="14610-118">To see a step-by-step process of how to build a localized application for Windows Phone, see  [How to: Build a Localized Application for Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="14610-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="14610-119">See also</span></span>
<span data-ttu-id="14610-120"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="14610-120"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="14610-121">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="14610-121">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  <span data-ttu-id="14610-122">[Vorgehensweise: Erstellen einer lokalisierte Anwendung für Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="14610-122">[How to: Build a Localized Application for Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span></span>
    
  
-  [<span data-ttu-id="14610-123">Globalisierung und Lokalisierung für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="14610-123">Globalization and Localization for Windows Phone</span></span>](http://msdn.microsoft.com/library/e82118a4-6247-4d75-a16f-749677349be4%28Office.15%29.aspx)
    
  

  
    
    

