---
title: "Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: acaf556d-e20d-478d-8c59-2efd8efb9dcb
ms.openlocfilehash: 9c18eb3fa355abd5f96b2620bd0ee8aed825cdb4
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="set-up-an-environment-for-developing-mobile-apps-for-sharepoint"></a><span data-ttu-id="9acdd-102">Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9acdd-102">How to: Set up an environment for developing mobile apps for SharePoint</span></span>

<span data-ttu-id="9acdd-p101">In diesem Artikel erhalten Sie Informationen zu den Systemanforderungen und zum Konfigurieren einer Entwicklungsumgebung für SharePoint-Mobilitätsprojekte. Mindestkonfiguration für die Arbeit mit SharePoint-Mobilitätsprojekte erfordert einen Server mit SharePoint (oder ein Konto SharePoint Online ) und einer Entwicklungsumgebung auf einem separaten Client-Betriebssystem. Installieren von SharePoint auf Clientbetriebssysteme (beispielsweise Windows 7 ) ist nicht unterstützte und Installieren von erforderlichen Tools für die Entwicklung für Windows Phone wird nicht auf Server-Betriebssystemen (beispielsweise Windows Server 2008 ).</span><span class="sxs-lookup"><span data-stu-id="9acdd-p101">Learn about the system requirements and configuring a development environment for SharePoint mobility projects. A minimal configuration for working with SharePoint mobility projects requires a server running SharePoint (or a SharePoint Online account) and a development environment on a separate client operating system. Installing SharePoint on client operating systems (such as Windows 7) is not supported, and installing the tools necessary for Windows Phone development is not supported on server operating systems (such as Windows Server 2008).</span></span>
  
    
    


## <a name="windows-phone-development-projects-and-sharepoint-server"></a><span data-ttu-id="9acdd-106">Windows Phone-Entwicklungsprojekte und SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="9acdd-106">Windows Phone development projects and SharePoint Server</span></span>
<span data-ttu-id="9acdd-107"><a name="SP15Setupmobile_winphone"> </a></span><span class="sxs-lookup"><span data-stu-id="9acdd-107"><a name="SP15Setupmobile_winphone"> </a></span></span>

<span data-ttu-id="9acdd-p102">Zum Erstellen und Testen von Windows Phone-apps, die mit SharePoint interagieren, benötigen Sie Zugriff auf einen Server mit SharePoint oder ein Konto SharePoint Online und benötigen Sie ausreichende Berechtigungen für die Websites und Listen Sie in Ihren Lösungen verwenden möchten. Es wird empfohlen, dass Sie eine Installation von SharePoint Server, der zum Testen und Entwicklung als Zielserver vorgesehen ist verwenden, während Sie Ihre Projekte entwickeln. Verwenden Sie SharePoint Server in einer produktionsumgebung als Zielserver erst nach Ihrer entwickelte Lösung ausreichende Tests unterzogen wurde.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p102">To create and test Windows Phone apps that interact with SharePoint, you need access to a server running SharePoint or a SharePoint Online account, and you need sufficient permissions on the sites and lists you intend to use in your solutions. We recommend that you use an installation of SharePoint Server that is dedicated to testing and development as a target server while you develop your projects. Use SharePoint Server in a production environment as your target server only after your developed solution has undergone sufficient testing.</span></span>
  
    
    
<span data-ttu-id="9acdd-p103">Informationen zur Installation und Konfiguration von SharePoint finden Sie in die Dokumentation in der  [SharePoint-Produkte](http://technet.microsoft.com/de-DE/library/ee428287.aspx) -Abschnitt der Microsoft TechNet Library. Informationen zur Verwendung von SharePoint Online Ihre Entwicklung von Lösungen finden Sie auf der [SharePoint Online-Entwicklerressourcencenter](http://msdn.microsoft.com/de-DE/sharepoint/gg153540.aspx).</span><span class="sxs-lookup"><span data-stu-id="9acdd-p103">For information on installing and configuring SharePoint, see the documentation in the  [SharePoint Products](http://technet.microsoft.com/de-DE/library/ee428287.aspx) section of the Microsoft TechNet Library. For information on using SharePoint Online in your development solutions, visit the [SharePoint Online Developer Resource Center](http://msdn.microsoft.com/de-DE/sharepoint/gg153540.aspx).</span></span>
  
    
    
<span data-ttu-id="9acdd-113">Die Codebeispiele in dieser Dokumentation wird davon ausgegangen, dass ein Entwickler mit dem Beispiel hat oder erhalten Sie über ausreichende Berechtigungen für SharePoint-Websites und Listen werden sollen, hinzufügen, bearbeiten und Löschen von Daten.</span><span class="sxs-lookup"><span data-stu-id="9acdd-113">For the code samples in this documentation, it is assumed that a developer working with the sample has or can obtain sufficient permissions on SharePoint sites and lists to be able to add, edit, and delete data.</span></span>
  
    
    

## <a name="configure-a-client-development-environment-for-sharepoint-mobility-projects"></a><span data-ttu-id="9acdd-114">Konfigurieren einer Client-Entwicklungsumgebung für Mobilität von SharePoint-Projekten</span><span class="sxs-lookup"><span data-stu-id="9acdd-114">Configure a client development environment for SharePoint mobility projects</span></span>
<span data-ttu-id="9acdd-115"><a name="SP15Setupmobile_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="9acdd-115"><a name="SP15Setupmobile_configure"> </a></span></span>

<span data-ttu-id="9acdd-116">Informationen zum Entwickeln von SharePoint-Add-Ins für die Verwendung auf Windows Phone-Geräten, müssen Sie Ihre Entwicklungstools auf einem Computer einrichten, die einem Clientbetriebssystem nicht auf einem Server-Betriebssystem ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9acdd-116">To develop SharePoint Add-ins for use on Windows Phone devices, you need to set up your development tools on a computer that is running a client operating system, not a server operating system.</span></span>
  
    
    

### <a name="configuring-windows-phone-sdk-80"></a><span data-ttu-id="9acdd-117">Konfigurieren von Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="9acdd-117">Configuring Windows Phone SDK 8.0</span></span>

<span data-ttu-id="9acdd-p104">Informationen zum Entwickeln von SharePoint-Add-Ins für die Verwendung auf Windows Phone 8, müssen Sie Ihre Entwicklungstools auf einem Computer einrichten, die Clientversionen Windows 8 64-Bit (X 64) oder Windows 8 Pro ausgeführt wird. Windows Phone 8-Emulator erfordert Windows 8 Pro und erfordert einen Prozessor, der Second Level Address Translation (SLAT) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p104">To develop SharePoint Add-ins for use on Windows Phone 8, you need to set up your development tools on a computer that is running Windows 8 64-bit (x64) client versions or Windows 8 Pro. The Windows Phone 8 Emulator requires Windows 8 Pro, and requires a processor that supports Second Level Address Translation (SLAT).</span></span>
  
    
    

1. <span data-ttu-id="9acdd-p105">Installieren Sie auf einem Computer mit einem unterstützten Client-Betriebssystem  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471). Die Windows Phone Software Development Kit (SDK) 8.0 enthält die Tools, die Sie zum Entwickeln von apps und Spiele für Windows Phone 8 und Windows Phone 7.5 benötigen.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p105">On a computer with a supported client operating system, install  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471). The Windows Phone Software Development Kit (SDK) 8.0 provides you with the tools that you need to develop apps and games for Windows Phone 8 and Windows Phone 7.5.</span></span>
    
    <span data-ttu-id="9acdd-p106">Die Windows Phone SDK 8.0 ist eine voll funktionsfähige Entwicklungsumgebung zum Erstellen von apps und Spiele für Windows Phone 8.0 und Windows Phone 7.5 verwenden. Windows Phone SDK bietet eine eigenständige Version von Visual Studio Express 2012 für Windows Phone oder als ein Add-in auf Visual Studio 2012 Professional, Premium oder Ultimate Edition funktioniert. Mit dem SDK können Sie Ihre vorhandenen programming Fähigkeiten und Code verwenden, verwalteten oder systemeigenen Code apps erstellen. Das SDK enthält darüber hinaus mehrere Emulatoren und weitere Tools für das Profil erstellen und Testen Ihrer Windows Phone-app unter Umständen Praxis.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p106">The Windows Phone SDK 8.0 is a full-featured development environment to use for building apps and games for Windows Phone 8.0 and Windows Phone 7.5. The Windows Phone SDK provides a stand-alone Visual Studio Express 2012 edition for Windows Phone or works as an add-in to Visual Studio 2012 Professional, Premium or Ultimate editions. With the SDK, you can use your existing programming skills and code to build managed or native code apps. In addition, the SDK includes multiple emulators and additional tools for profiling and testing your Windows Phone app under real-world conditions.</span></span>
    
    > <span data-ttu-id="9acdd-126">**Hinweis:** Wenn Ihr Computer die Hardware- und Betriebssystemanforderungen erfüllt, nicht jedoch die Anforderungen für den Windows Phone 8-Emulator, lässt sich Windows Phone SDK 8.0 installieren und ausführen.</span><span class="sxs-lookup"><span data-stu-id="9acdd-126">**Note:** If your computer meets the hardware and operating system requirements, but does not meet the requirements for the Windows Phone 8 Emulator, the Windows Phone SDK 8.0 will install and run.</span></span> <span data-ttu-id="9acdd-127">Der Windows Phone 8-Emulator jedoch funktioniert dann nicht. Das heißt: Sie können keine Apps im Windows Phone 8-Emulator bereitstellen oder testen.</span><span class="sxs-lookup"><span data-stu-id="9acdd-127">However, the Windows Phone 8 Emulator will not function and you will not be able to deploy or test apps on the Windows Phone 8 Emulator.</span></span> <span data-ttu-id="9acdd-128">Informationen zu den Systemanforderungen für den Windows Phone-Emulator finden Sie unter [Setup and System Requirements for Windows Phone Emulator](http://msdn.microsoft.com/de-DE/library/ff626524).</span><span class="sxs-lookup"><span data-stu-id="9acdd-128">For information about the system requirements for running the Windows Phone Emulator, see  [Setup and System Requirements for Windows Phone Emulator](http://msdn.microsoft.com/de-DE/library/ff626524).</span></span> 
2. <span data-ttu-id="9acdd-129">Installieren Sie das [Microsoft SharePoint-SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818).</span><span class="sxs-lookup"><span data-stu-id="9acdd-129">Install  [Microsoft SharePoint SDK for Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818).</span></span>
    
    <span data-ttu-id="9acdd-p108">SharePoint SDK für Windows Phone installiert zwei Silverlight für Windows Phone-Vorlagen (neben von Windows Phone SDK installiert): die Vorlage Windows Phone leeres SharePoint-Anwendung und die Vorlage Windows Phone SharePoint List Application. Das SDK auch installiert, SharePoint-CSOM-Bibliotheken, eine Authentifizierungsbibliothek und Windows Phone-Projektvorlagen und es nun die NTLM-Authentifizierung unterstützt. Die gebündelten-APIs und Vorlagen können Sie um Windows Phone 8 Applications gegen SharePoint zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p108">The SharePoint SDK for Windows Phone installs two Silverlight for Windows Phone templates (in addition to those installed by the Windows Phone SDK): the Windows Phone Empty SharePoint Application template and the Windows Phone SharePoint List Application template. The SDK also installs SharePoint CSOM libraries, an authentication library, and Windows Phone project templates, and it now supports NTLM authentication. You can use the bundled APIs and templates to build Windows Phone 8 applications against SharePoint.</span></span>
    
    <span data-ttu-id="9acdd-133">Darüber hinaus wird im SharePoint SDK für Windows Phone mehrere unterstützenden Laufzeit-Assemblys (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v8.0\\Libraries` für eine Standardinstallation) installiert.</span><span class="sxs-lookup"><span data-stu-id="9acdd-133">Additionally, the SharePoint SDK for Windows Phone installs several supporting run-time assemblies (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v8.0\\Libraries` for a standard installation).</span></span>
    
  - <span data-ttu-id="9acdd-134">Microsoft.SharePoint.Client.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-134">Microsoft.SharePoint.Client.Phone.dll</span></span>
    
  
  - <span data-ttu-id="9acdd-135">Microsoft.SharePoint.Client.Phone.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-135">Microsoft.SharePoint.Client.Phone.Runtime.dll</span></span>
    
  
  - <span data-ttu-id="9acdd-136">Microsoft.SharePoint.Client.Phone.Auth.UI</span><span class="sxs-lookup"><span data-stu-id="9acdd-136">Microsoft.SharePoint.Client.Phone.Auth.UI</span></span>
    
  
  - <span data-ttu-id="9acdd-137">Microsoft.SharePoint.Phone.Application.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-137">Microsoft.SharePoint.Phone.Application.dll</span></span>
    
  

    > <span data-ttu-id="9acdd-138">**Hinweis:** Die Vorlagen im SharePoint-SDK für Windows Phone sind derzeit nur für C#-Projekte verfügbar.</span><span class="sxs-lookup"><span data-stu-id="9acdd-138">**Note:** The templates in the SharePoint SDK for Windows Phone are currently available for C# projects only.</span></span> 
      > <span data-ttu-id="9acdd-139">Weitere Informationen zu den Vorlagen im SharePoint-SDK für Windows Phone finden Sie unter [Übersicht über Windows Phone SharePoint-Anwendungsvorlagen in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9acdd-139">For more information about the templates in SharePoint SDK for Windows Phone, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span>
  
    
    

### <a name="configuring-windows-phone-sdk-71"></a><span data-ttu-id="9acdd-140">Konfigurieren von Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="9acdd-140">Configuring Windows Phone SDK 7.1</span></span>

<span data-ttu-id="9acdd-p110">Informationen zum Entwickeln von SharePoint-Add-Ins für die Verwendung auf Windows Phone 7, müssen Sie richten Sie Ihre Entwicklungstools auf einem Computer mit Windows 7 (32-Bit oder 64-Bit) oder Windows Vista Service Pack 2 (32-Bit oder 64-Bit). Die Windows Phone Software Development Kit (SDK) 7.1 wird nicht auf Windows Server 2008 oder in Windows XP unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9acdd-p110">To develop SharePoint Add-ins for use on Windows Phone 7, you need to set up your development tools on a computer that is running Windows 7 (32-bit or 64-bit) or Windows Vista Service Pack 2 (32-bit or 64-bit). The Windows Phone Software Development Kit (SDK) 7.1 is not supported on Windows Server 2008 or on Windows XP.</span></span>
  
    
    

1. <span data-ttu-id="9acdd-143">Installieren Sie [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570) auf einem Computer mit einem unterstützten Clientbetriebssystem.</span><span class="sxs-lookup"><span data-stu-id="9acdd-143">On a computer with a supported client operating system, install  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570).</span></span>
    
    > <span data-ttu-id="9acdd-144">**Hinweis:** Eine frühere Version des Windows Phone SDK hieß Windows Phone Developer Tools.</span><span class="sxs-lookup"><span data-stu-id="9acdd-144">**Note:** An earlier version of the Windows Phone SDK was named the Windows Phone Developer Tools.</span></span> 

    <span data-ttu-id="9acdd-p111">Windows Phone SDK installiert Microsoft Visual Studio 2010 Express für Windows Phone, die Windows Phone-Emulator, XNA Spiel Studio und Microsoft Expression Blend für Windows Phone. Visual Studio 2010 Express For Windows Phone ist eine geeignete Entwicklungsumgebung für die meisten Windows Phone-Lösungen. Sie können auch Visual Studio 2010 Professional als Ihre bevorzugten Entwicklungsumgebung, aber noch Windows Phone SDK, installieren Sie die Visual Studio die erforderliche add-ins installiert werden müssen. (Windows Phone SDK wird nicht aktuell für die Verwendung mit Visual Studio 2012 unterstützt.)</span><span class="sxs-lookup"><span data-stu-id="9acdd-p111">The Windows Phone SDK installs Microsoft Visual Studio 2010 Express for Windows Phone, the Windows Phone Emulator, XNA Game Studio, and Microsoft Expression Blend for Windows Phone. Visual Studio 2010 Express for Windows Phone is a suitable development environment for most Windows Phone solutions. You can also use Visual Studio 2010 Professional as your preferred development environment, but you still need to install the Windows Phone SDK, which installs the necessary add-ins to Visual Studio. (The Windows Phone SDK is not currently supported for use with Visual Studio 2012.)</span></span>
    
    <span data-ttu-id="9acdd-p112">Informationen zu zusätzlichen Systemanforderungen und Anweisungen für die Installation von Windows Phone SDK finden Sie unter  [Installieren von Windows Phone SDK](http://msdn.microsoft.com/de-DE/library/ff402530). Informationen zu den Systemanforderungen für die Ausführung der Windows Phone-Emulator finden Sie unter  [Setup und System Requirements für Windows Phone-Emulator](http://msdn.microsoft.com/de-DE/library/ff626524).</span><span class="sxs-lookup"><span data-stu-id="9acdd-p112">For information on additional system requirements and instructions for installing the Windows Phone SDK, see  [Installing the Windows Phone SDK](http://msdn.microsoft.com/de-DE/library/ff402530). For information about the system requirements for running the Windows Phone Emulator, see  [Setup and System Requirements for Windows Phone Emulator](http://msdn.microsoft.com/de-DE/library/ff626524).</span></span>
    
  
2. <span data-ttu-id="9acdd-151">Installieren Sie  [Microsoft SharePoint SDK für Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476).</span><span class="sxs-lookup"><span data-stu-id="9acdd-151">Install  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476).</span></span>
    
    <span data-ttu-id="9acdd-152">SharePoint SDK für Windows Phone installiert zwei Silverlight für Windows Phone-Vorlagen (neben von Windows Phone SDK installiert): die Vorlage Windows Phone leeres SharePoint-Anwendung und die Vorlage Windows Phone SharePoint List Application.</span><span class="sxs-lookup"><span data-stu-id="9acdd-152">The SharePoint SDK for Windows Phone installs two Silverlight for Windows Phone templates (in addition to those installed by the Windows Phone SDK): the Windows Phone Empty SharePoint Application template and the Windows Phone SharePoint List Application template.</span></span>
    
    <span data-ttu-id="9acdd-153">Darüber hinaus wird im SharePoint SDK für Windows Phone mehrere unterstützenden Laufzeit-Assemblys (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v7.1\\Libraries` für eine Standardinstallation) installiert.</span><span class="sxs-lookup"><span data-stu-id="9acdd-153">Additionally, the SharePoint SDK for Windows Phone installs several supporting run-time assemblies (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v7.1\\Libraries` for a standard installation).</span></span>
    
  - <span data-ttu-id="9acdd-154">Microsoft.SharePoint.Client.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-154">Microsoft.SharePoint.Client.Phone.dll</span></span>
    
  
  - <span data-ttu-id="9acdd-155">Microsoft.SharePoint.Client.Phone.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-155">Microsoft.SharePoint.Client.Phone.Runtime.dll</span></span>
    
  
  - <span data-ttu-id="9acdd-156">Microsoft.SharePoint.Client.Phone.Auth.UI</span><span class="sxs-lookup"><span data-stu-id="9acdd-156">Microsoft.SharePoint.Client.Phone.Auth.UI</span></span>
    
  
  - <span data-ttu-id="9acdd-157">Microsoft.SharePoint.Phone.Application.dll</span><span class="sxs-lookup"><span data-stu-id="9acdd-157">Microsoft.SharePoint.Phone.Application.dll</span></span>
    
  

    > <span data-ttu-id="9acdd-158">**Hinweis:** Die Vorlagen im SharePoint-SDK für Windows Phone sind derzeit nur für C#-Projekte verfügbar.</span><span class="sxs-lookup"><span data-stu-id="9acdd-158">**Note:** The templates in the SharePoint SDK for Windows Phone are currently available for C# projects only.</span></span> 
      > <span data-ttu-id="9acdd-159">Weitere Informationen zu den Vorlagen im SharePoint-SDK für Windows Phone finden Sie unter [Übersicht über Windows Phone SharePoint-Anwendungsvorlagen in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9acdd-159">For more information about the templates in SharePoint SDK for Windows Phone, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="9acdd-160">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9acdd-160">Additional resources</span></span>
<span data-ttu-id="9acdd-161"><a name="SP15Setupmobile_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9acdd-161"><a name="SP15Setupmobile_addlresources"> </a></span></span>


-  [<span data-ttu-id="9acdd-162">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="9acdd-162">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="9acdd-163">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="9acdd-163">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="9acdd-164">Microsoft SharePoint SDK für Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9acdd-164">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="9acdd-165">Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="9acdd-165">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="9acdd-166">Microsoft SharePoint SDK für Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="9acdd-166">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

