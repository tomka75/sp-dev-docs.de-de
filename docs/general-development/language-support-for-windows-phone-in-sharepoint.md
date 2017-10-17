---
title: "Sprachenunterstützung für Windows Phone in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2c396a91-0fc1-4e25-942b-fffad49bd2c6
ms.openlocfilehash: 3cb2a1bfd23e9d533a53597437afec41d56d84c1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="language-support-for-windows-phone-in-sharepoint"></a><span data-ttu-id="27690-102">Sprachenunterstützung für Windows Phone in SharePoint</span><span class="sxs-lookup"><span data-stu-id="27690-102">Language support for Windows Phone in SharePoint</span></span>
<span data-ttu-id="27690-p101">Informationen Sie zu sprachunterstützung für die Visual Studio-Vorlagen, die von SharePoint Software Development Kit (SDK) für Windows Phone für die Entwicklung mobiler Apps installiert werden. Um die mobile Anwendung für mehrere Sprachen zu entwickeln, müssen Sie zum Globalisieren und lokalisieren Sie die Anwendung. Die meisten Globalisierung und Lokalisierung Funktionen, die Sie benötigen, um zu implementieren ist bereits in die .NET Framework integriert. Mithilfe dieser Funktion können Sie Kunden in anderen Ländern und Regionen erreichen.</span><span class="sxs-lookup"><span data-stu-id="27690-p101">Learn about language support for the Visual Studio templates that are installed by the SharePoint Software Development Kit (SDK) for Windows Phone for mobile app development. To develop your mobile application for more than one language, you need to globalize and localize the application. Most of the globalization and localization functionality that you need to implement is already built into the .NET Framework. By using this functionality, you can reach customers in many other countries and regions.</span></span>
  
    
    

<span data-ttu-id="27690-p102">Windows Phone SDK enthält Visual Studio 2010 Express für Windows Phone, Windows Phone-Emulator, XNA Spiel Studio und Expression Blend. Installieren Sie Sie zuerst die  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570) für die Entwicklung für Windows Phone. Installieren Sie dann den [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476) zum Installieren von SharePoint-Vorlagen für Windows Phone. Nachdem Sie Ihre Entwicklungsumgebung einrichten und des SharePoint-SDK für Windows Phone installieren, finden Sie unter  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="27690-p102">The Windows Phone SDK includes Visual Studio 2010 Express for Windows Phone, Windows Phone Emulator, XNA Game Studio, and Expression Blend. To get started, install the  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570) for Windows Phone development. Then install the [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476) to install the SharePoint templates for Windows Phone. After you set up your development environment and install the SharePoint SDK for Windows Phone, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span>
  
    
    

<span data-ttu-id="27690-111">Weitere Informationen zu den SharePoint-Vorlagen für Windows Phone finden Sie unter  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="27690-111">For more information about the SharePoint templates for Windows Phone, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span>
## <a name="templates-and-libraries-installed-by-the-sharepoint-sdk-for-windows-phone"></a><span data-ttu-id="27690-112">Vorlagen und Bibliotheken installiert, indem Sie im SharePoint SDK für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="27690-112">Templates and libraries installed by the SharePoint SDK for Windows Phone</span></span>
<span data-ttu-id="27690-113"><a name="LanguageSupportForWindowsPhoneForSharePoint2013_TemplatesInstalledBySharePointSDKForWindowsPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="27690-113"></span></span>

<span data-ttu-id="27690-114">SharePoint SDK für Windows Phone 7.1 installiert die Client-Objektmodell (CSOM) Objektbibliotheken für Windows Phone, die SharePoint Auth-Bibliothek für Windows Phone und Windows Phone-Projektvorlagen, die Sie zum Erstellen von Windows Phone 7.1 Applications gegen SharePoint oder SharePoint 2010 verwenden können.</span><span class="sxs-lookup"><span data-stu-id="27690-114">The SharePoint SDK for Windows Phone 7.1 installs the client object model (CSOM) libraries for Windows Phone, the SharePoint Auth library for Windows Phone, and the Windows Phone project templates, which you can use to build Windows Phone 7.1 applications against SharePoint or SharePoint 2010.</span></span>
  
    
    
<span data-ttu-id="27690-115">Bei der Installation von SharePoint SDK für Windows Phone stehen zwei zusätzliche Silverlight für Windows Phone-Vorlagen für Projekte:</span><span class="sxs-lookup"><span data-stu-id="27690-115">When you install the SharePoint SDK for Windows Phone, two additional Silverlight for Windows Phone templates are available for projects:</span></span>
  
    
    

- <span data-ttu-id="27690-116">Windows Phone leeres SharePoint-Anwendung</span><span class="sxs-lookup"><span data-stu-id="27690-116">Windows Phone Empty SharePoint Application</span></span>
    
  
- <span data-ttu-id="27690-117">Windows Phone-SharePoint-Listen-App</span><span class="sxs-lookup"><span data-stu-id="27690-117">Windows Phone SharePoint List Application</span></span>
    
  

## <a name="localized-versions-of-the-sharepoint-sdk-for-windows-phone"></a><span data-ttu-id="27690-118">Lokalisierte Versionen von SharePoint SDK für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="27690-118">Localized versions of the SharePoint SDK for Windows Phone</span></span>
<span data-ttu-id="27690-119"><a name="LanguageSupportForWindowsPhoneForSharePoint2013_LocalizedVersionsOfSharePointSDKForWindowsPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="27690-119"></span></span>

<span data-ttu-id="27690-p103">Neun verschiedenen Sprachen werden von SharePoint SDK für Windows Phone Developer Toolkit 7.1 unterstützt. Die meisten Aufgaben beim Erstellen einer Anwendung erfolgt zur Entwurfszeit, einschließlich des Erstellens von Projekten, Entwerfen von Formularen, entwickeln Steuerelemente und Code hinzufügen. Sie können Windows Phone-Anwendungen schreiben, mit einer der folgenden lokalisierten Versionen von SharePoint SDK für Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="27690-p103">Nine languages are supported by the SharePoint SDK for Windows Phone Developer Toolkit 7.1. Most of the work of creating an application is done at design time, including creating projects, designing forms, developing controls, and adding code. You can write Windows Phone applications by using any of the following localized versions of the SharePoint SDK for Windows Phone:</span></span>
  
    
    

- <span data-ttu-id="27690-123">Englisch (En-US)</span><span class="sxs-lookup"><span data-stu-id="27690-123">English (en-US)</span></span>
    
  
- <span data-ttu-id="27690-124">Französisch (fr-FR)</span><span class="sxs-lookup"><span data-stu-id="27690-124">French (fr-FR)</span></span>
    
  
- <span data-ttu-id="27690-125">Deutsch (de-DE)</span><span class="sxs-lookup"><span data-stu-id="27690-125">German (de-DE)</span></span>
    
  
- <span data-ttu-id="27690-126">Italienisch (it-IT)</span><span class="sxs-lookup"><span data-stu-id="27690-126">Italian (it-IT)</span></span>
    
  
- <span data-ttu-id="27690-127">Japanisch (ja-JP)</span><span class="sxs-lookup"><span data-stu-id="27690-127">Japanese (ja-JP)</span></span>
    
  
- <span data-ttu-id="27690-128">Koreanisch (Ko-KR)</span><span class="sxs-lookup"><span data-stu-id="27690-128">Korean (Ko-KR)</span></span>
    
  
- <span data-ttu-id="27690-129">Russisch (ru-RU)</span><span class="sxs-lookup"><span data-stu-id="27690-129">Russian (ru-RU)</span></span>
    
  
- <span data-ttu-id="27690-130">Spanisch (es-ES)</span><span class="sxs-lookup"><span data-stu-id="27690-130">Spanish (es-ES)</span></span>
    
  
- <span data-ttu-id="27690-131">Chinesisch (traditionell) (Zh-TW)</span><span class="sxs-lookup"><span data-stu-id="27690-131">Traditional Chinese (zh-TW)</span></span>
    
  

## <a name="supported-localized-languages-for-sharepoint-windows-phone-applications"></a><span data-ttu-id="27690-132">Unterstützte lokalisierte Sprachen für Windows Phone SharePoint-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="27690-132">Supported localized languages for SharePoint Windows Phone applications</span></span>
<span data-ttu-id="27690-133"><a name="bk_supplocallangs"> </a></span><span class="sxs-lookup"><span data-stu-id="27690-133"></span></span>

<span data-ttu-id="27690-p104">Wenn eine Anwendung die Steuerung übernimmt, interagieren Sie mit der Anwendung auf die gleiche Weise wie ein Benutzer. Sie können Code anzuzeigen, führen Sie die Anwendung und Debuggen, aber den Code kann nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="27690-p104">When an application takes control, you interact with the application in the same way a user does. You can view code, run the application, and debug it, but you cannot change the code.</span></span>
  
    
    
<span data-ttu-id="27690-136">Obwohl Sie den programmgesteuerten Zugriff auf neun verschiedenen Sprachen haben, können Sie Ihre mobilen SharePoint-Anwendungen in den zwanzig Sprachen, die in Tabelle 1 dargestellt ausführen.</span><span class="sxs-lookup"><span data-stu-id="27690-136">Although you have programmatic access to nine languages, you can run your SharePoint mobile applications in the twenty languages shown in Table 1.</span></span>
  
    
    

<span data-ttu-id="27690-137">**In Tabelle 1. Unterstützte anzeigen/Laufzeitfehler Sprachen im SharePoint SDK für Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="27690-137">**Table 1. Supported display/run-time languages in the SharePoint SDK for Windows Phone**</span></span>


|<span data-ttu-id="27690-138">**Kulturnamen**</span><span class="sxs-lookup"><span data-stu-id="27690-138">**Culture name**</span></span>|<span data-ttu-id="27690-139">**Kulturcode**</span><span class="sxs-lookup"><span data-stu-id="27690-139">**Culture code**</span></span>|
|:-----|:-----|
|<span data-ttu-id="27690-140">Vereinfachtes Chinesisch (VR China)</span><span class="sxs-lookup"><span data-stu-id="27690-140">Chinese Simplified (PRC)</span></span>  <br/> |<span data-ttu-id="27690-141">zh-CN</span><span class="sxs-lookup"><span data-stu-id="27690-141">zh-CN</span></span>  <br/> |
|<span data-ttu-id="27690-142">Traditionelles Chinesisch (Taiwan)</span><span class="sxs-lookup"><span data-stu-id="27690-142">Chinese Traditional (Taiwan)</span></span>  <br/> |<span data-ttu-id="27690-143">zh-TW</span><span class="sxs-lookup"><span data-stu-id="27690-143">zh-TW</span></span>  <br/> |
|<span data-ttu-id="27690-144">Tschechisch (Tschechische Republik)</span><span class="sxs-lookup"><span data-stu-id="27690-144">Czech (Czech Republic)</span></span>  <br/> |<span data-ttu-id="27690-145">cs</span><span class="sxs-lookup"><span data-stu-id="27690-145">cs</span></span>  <br/> |
|<span data-ttu-id="27690-146">Dänisch (Dänemark)</span><span class="sxs-lookup"><span data-stu-id="27690-146">Danish (Denmark)</span></span>  <br/> |<span data-ttu-id="27690-147">da</span><span class="sxs-lookup"><span data-stu-id="27690-147">da</span></span>  <br/> |
|<span data-ttu-id="27690-148">Niederländisch (Königreich der Niederlande)</span><span class="sxs-lookup"><span data-stu-id="27690-148">Dutch (Netherlands)</span></span>  <br/> |<span data-ttu-id="27690-149">nl</span><span class="sxs-lookup"><span data-stu-id="27690-149">nl</span></span>  <br/> |
|<span data-ttu-id="27690-150">Finnisch (Finnland)</span><span class="sxs-lookup"><span data-stu-id="27690-150">Finnish (Finland)</span></span>  <br/> |<span data-ttu-id="27690-151">fi</span><span class="sxs-lookup"><span data-stu-id="27690-151">fi</span></span>  <br/> |
|<span data-ttu-id="27690-152">Französisch (Frankreich)</span><span class="sxs-lookup"><span data-stu-id="27690-152">French (France)</span></span>  <br/> |<span data-ttu-id="27690-153">fr</span><span class="sxs-lookup"><span data-stu-id="27690-153">fr</span></span>  <br/> |
|<span data-ttu-id="27690-154">Deutsch (Deutschland)</span><span class="sxs-lookup"><span data-stu-id="27690-154">German (Germany)</span></span>  <br/> |<span data-ttu-id="27690-155">de</span><span class="sxs-lookup"><span data-stu-id="27690-155">de</span></span>  <br/> |
|<span data-ttu-id="27690-156">Griechisch (Griechenland)</span><span class="sxs-lookup"><span data-stu-id="27690-156">Greek (Greece)</span></span>  <br/> |<span data-ttu-id="27690-157">el</span><span class="sxs-lookup"><span data-stu-id="27690-157">el</span></span>  <br/> |
|<span data-ttu-id="27690-158">Ungarisch (Ungarn)</span><span class="sxs-lookup"><span data-stu-id="27690-158">Hungarian (Hungary)</span></span>  <br/> |<span data-ttu-id="27690-159">hu</span><span class="sxs-lookup"><span data-stu-id="27690-159">hu</span></span>  <br/> |
|<span data-ttu-id="27690-160">Italienisch (Italien)</span><span class="sxs-lookup"><span data-stu-id="27690-160">Italian (Italy)</span></span>  <br/> |<span data-ttu-id="27690-161">it</span><span class="sxs-lookup"><span data-stu-id="27690-161">it</span></span>  <br/> |
|<span data-ttu-id="27690-162">Japanisch (Japan)</span><span class="sxs-lookup"><span data-stu-id="27690-162">Japanese (Japan)</span></span>  <br/> |<span data-ttu-id="27690-163">ja</span><span class="sxs-lookup"><span data-stu-id="27690-163">ja</span></span>  <br/> |
|<span data-ttu-id="27690-164">Koreanisch (Korea)</span><span class="sxs-lookup"><span data-stu-id="27690-164">Korean (Korea)</span></span>  <br/> |<span data-ttu-id="27690-165">ko</span><span class="sxs-lookup"><span data-stu-id="27690-165">ko</span></span>  <br/> |
|<span data-ttu-id="27690-166">Norwegisch (Norwegen)</span><span class="sxs-lookup"><span data-stu-id="27690-166">Norwegian (Norway)</span></span>  <br/> |<span data-ttu-id="27690-167">nb</span><span class="sxs-lookup"><span data-stu-id="27690-167">nb</span></span>  <br/> |
|<span data-ttu-id="27690-168">Polnisch (Polen)</span><span class="sxs-lookup"><span data-stu-id="27690-168">Polish (Poland)</span></span>  <br/> |<span data-ttu-id="27690-169">pl</span><span class="sxs-lookup"><span data-stu-id="27690-169">pl</span></span>  <br/> |
|<span data-ttu-id="27690-170">Portugiesisch (Brasilien)</span><span class="sxs-lookup"><span data-stu-id="27690-170">Portuguese (Brazil)</span></span>  <br/> |<span data-ttu-id="27690-171">pt-BR</span><span class="sxs-lookup"><span data-stu-id="27690-171">pt-BR</span></span>  <br/> |
|<span data-ttu-id="27690-172">Portugiesisch (Portugal)</span><span class="sxs-lookup"><span data-stu-id="27690-172">Portuguese (Portugal)</span></span>  <br/> |<span data-ttu-id="27690-173">pt-PT</span><span class="sxs-lookup"><span data-stu-id="27690-173">pt-PT</span></span>  <br/> |
|<span data-ttu-id="27690-174">Russisch (Russland)</span><span class="sxs-lookup"><span data-stu-id="27690-174">Russian (Russia)</span></span>  <br/> |<span data-ttu-id="27690-175">ru</span><span class="sxs-lookup"><span data-stu-id="27690-175">ru</span></span>  <br/> |
|<span data-ttu-id="27690-176">Spanisch (Spanien)</span><span class="sxs-lookup"><span data-stu-id="27690-176">Spanish (Spain)</span></span>  <br/> |<span data-ttu-id="27690-177">es</span><span class="sxs-lookup"><span data-stu-id="27690-177">es</span></span>  <br/> |
|<span data-ttu-id="27690-178">Schwedisch (Schweden)</span><span class="sxs-lookup"><span data-stu-id="27690-178">Swedish (Sweden)</span></span>  <br/> |<span data-ttu-id="27690-179">sv</span><span class="sxs-lookup"><span data-stu-id="27690-179">sv</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="27690-180">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="27690-180">Additional resources</span></span>
<span data-ttu-id="27690-181"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="27690-181"></span></span>


-  [<span data-ttu-id="27690-182">Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27690-182">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [<span data-ttu-id="27690-183">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="27690-183">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="27690-184">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="27690-184">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="27690-185">Microsoft SharePoint SDK für Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="27690-185">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  

  
    
    

