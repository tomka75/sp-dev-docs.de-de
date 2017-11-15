---
title: "Benutzerdefinierte Wörtertrennungen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18b48d4-987c-4228-9932-30d5b30f86a2
ms.openlocfilehash: 55cbfc603c1ea778625c7ccd7de4db411d66226c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="custom-word-breakers-in-sharepoint"></a><span data-ttu-id="83f13-102">Benutzerdefinierte Wörtertrennungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f13-102">Custom word breakers in SharePoint Server 2013</span></span>
<span data-ttu-id="83f13-103">In diesem Artikel finden Sie Informationen zu Wörtertrennungen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="83f13-103">Learn about word breaking in SharePoint.</span></span> <span data-ttu-id="83f13-104">Die Wörtertrennung ist eines der wichtigsten Features bei der Verarbeitung natürlicher Sprache (Natural Language Processing, NLP), die Suchläufe ermöglichen und Suchergebnisse (oder Abrufe) verbessern.</span><span class="sxs-lookup"><span data-stu-id="83f13-104">Word breaking is one of the key Natural Language Processing (NLP) features that enable search and improve search results (or recall).</span></span> <span data-ttu-id="83f13-105">Durch Wörtertrennungen wird ein Textfluss in einzelne Wörter oder Token aufgeteilt, die Sie als Basis für die weitere Sprachverarbeitung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="83f13-105">Word breakers split a stream of text into individual words or tokens on which you can base additional language processing.</span></span> <span data-ttu-id="83f13-106">Wörtertrennungen sind sprachspezifisch.</span><span class="sxs-lookup"><span data-stu-id="83f13-106">Word breakers are language-specific.</span></span> <span data-ttu-id="83f13-107">Zusätzlich zu integrierten Wörtertrennungen ermöglicht die Suche in SharePoint die Verwendung von benutzerdefinierten Wörtertrennungen, sodass Benutzer das Wörtertrennungsverhalten entsprechend ihren Anforderungen anpassen können.</span><span class="sxs-lookup"><span data-stu-id="83f13-107">In addition to built-in word breakers, Search in SharePoint enables the use of custom word breakers so that users can tune word breaking behavior according to their needs.</span></span> <span data-ttu-id="83f13-108">Eine Liste der Sprachen, die die Anpassung der Wörtertrennung unterstützt, finden Sie unter [Unterstützte Sprachen für die Anpassung der Wörtertrennung in SharePoint](#SP15_SupportedLanguages).</span><span class="sxs-lookup"><span data-stu-id="83f13-108">See  [Supported languages for word breaker customizations in SharePoint](#SP15_SupportedLanguages) for a list languages supported for word breaker customization.</span></span>
  
    
    

<span data-ttu-id="83f13-109">Informationen zum Schreiben einer Wörtertrennung finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="83f13-109">For information on how to write a word breaker refer to the following articles</span></span> 
-  <span data-ttu-id="83f13-110">
  [Implementieren von einem Worttrennmodul](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="83f13-110">[Implementing a Word Breaker](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)</span></span>
    
  
-  <span data-ttu-id="83f13-111">
  [IWordBreaker-Schnittstelle](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="83f13-111">[IWordBreaker interface](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)</span></span>
    
  

## <a name="how-to-switch-to-a-custom-word-breaker-in-sharepoint"></a><span data-ttu-id="83f13-112">Wechseln zu einer benutzerdefinierten Wörtertrennung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f13-112">How to switch to a custom word breaker in SharePoint Server 2013</span></span>
<span data-ttu-id="83f13-113"><a name="SP15wordbreaker_howto"> </a></span><span class="sxs-lookup"><span data-stu-id="83f13-113"></span></span>


> <span data-ttu-id="83f13-114">**Vorsicht:** Beim Ersetzen vorhandener Wörtertrennungen ändern Sie die Registrierung auf eigene Verantwortung.</span><span class="sxs-lookup"><span data-stu-id="83f13-114">**Caution:** When you replace existing word breakers, you modify the registry at your own risk.</span></span> <span data-ttu-id="83f13-115">Es können schwerwiegende Probleme auftreten, wenn Sie die Registrierung nicht ordnungsgemäß mithilfe des Registrierungs-Editors oder einer anderen Methode ändern.</span><span class="sxs-lookup"><span data-stu-id="83f13-115">Serious problems might occur if you modify the registry incorrectly by using Registry Editor or by using another method. These problems might require that you reinstall the operating system. Microsoft cannot guarantee that these problems can be solved. Modify the registry at your own risk.</span></span> <span data-ttu-id="83f13-116">Diese Probleme erfordern möglicherweise eine Neuinstallation des Betriebssystems.</span><span class="sxs-lookup"><span data-stu-id="83f13-116">These problems might require that you reinstall the operating system.</span></span> <span data-ttu-id="83f13-117">Microsoft kann nicht sicherstellen, dass diese Probleme behoben werden können.</span><span class="sxs-lookup"><span data-stu-id="83f13-117">Microsoft cannot ensure that these problems can be solved.</span></span> <span data-ttu-id="83f13-118">Der Wechsel zu einer anderen Wörtertrennung kann auch schwerwiegende Probleme beim Indizieren und Abfragen verursachen.</span><span class="sxs-lookup"><span data-stu-id="83f13-118">Switching to a different word breaker might also cause serious problems during indexing and querying.</span></span> <span data-ttu-id="83f13-119">Bevor Sie die Registrierung ändern, sichern Sie die Registrierung, und stellen Sie sicher, dass Sie wissen, wie Sie die Registrierung im Falle ein Problems wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="83f13-119">Before you modify the registry, back up the registry and ensure that you know how to restore the registry if a problem occurs.</span></span> 
  
    
    

<span data-ttu-id="83f13-120">Führen Sie die folgenden Schritte aus, ersetzen Sie das vorhandene Worttrennmodul mit einem benutzerdefinierten Worttrennmodul oder ersetzen das vorhandene Worttrennmodul mit einem Worttrennmodul in einer anderen Sprache.</span><span class="sxs-lookup"><span data-stu-id="83f13-120">Take the following steps to replace the existing word breaker with a custom word breaker or replace the existing word breaker with a word breaker in another language.</span></span>
  
    
    

1. <span data-ttu-id="83f13-121">Öffnen Sie den Registrierungs-Editor wie folgt:</span><span class="sxs-lookup"><span data-stu-id="83f13-121">Open the Registry Editor, as follows:</span></span>
    
1. <span data-ttu-id="83f13-122">Wählen Sie **Start**, und wählen Sie dann **Run**.</span><span class="sxs-lookup"><span data-stu-id="83f13-122">Choose **Start**, and then choose **Run**.</span></span>
    
  
2. <span data-ttu-id="83f13-123">Klicken Sie im Dialogfeld **Open** Geben Sie **Regedit**, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="83f13-123">In the **Open** dialog box, type **Regedit**, and then choose **OK**.</span></span>
    
  
2. <span data-ttu-id="83f13-124">Wählen Sie im Registrierungs-Editor den folgenden Registrierungsunterschlüssel:</span><span class="sxs-lookup"><span data-stu-id="83f13-124">In Registry Editor, select the following registry subkey:</span></span>
    
    <span data-ttu-id="83f13-125">**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Office Server\\15.0\\Search\\Setup\\ContentIndexCommon\\LanguageResources\\Default\\** _language from the list below_</span><span class="sxs-lookup"><span data-stu-id="83f13-125">**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Office Server\\15.0\\Search\\Setup\\ContentIndexCommon\\LanguageResources\\Default\\** _language from the list below_</span></span>
    
  
3. <span data-ttu-id="83f13-126">Klicken Sie im rechten Bereich öffnen Sie das Kontextmenü für den Registrierungswert **WBDLLPathOverride**, und wählen Sie **Modify**.</span><span class="sxs-lookup"><span data-stu-id="83f13-126">In the right pane, open the shortcut menu for the **WBDLLPathOverride** registry value, and then choose **Modify**.</span></span>
    
  
4. <span data-ttu-id="83f13-p103">Klicken Sie im Dialogfeld **Edit String** **Value data** Sie im Feld Geben Sie den Pfad zu Ihrer benutzerdefinierten Worttrennmodul DLL-Datei, und wählen Sie dann **OK**. Die neue DLL sollte sich in demselben Pfad wie die vorhandene DLL befinden, die ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="83f13-p103">In the **Edit String** dialog box, in the **Value data** box, type the path to your custom word breaker DLL, and then choose **OK**. The new DLL should be located in the same path as the existing DLL that is being replaced.</span></span>
    
  
5. <span data-ttu-id="83f13-129">Klicken Sie im rechten Bereich öffnen Sie das Kontextmenü für den Registrierungswert **WBreakerClass**, und wählen Sie **Modify**.</span><span class="sxs-lookup"><span data-stu-id="83f13-129">In the right pane, open the shortcut menu for the **WBreakerClass** registry value, and then choose **Modify**.</span></span>
    
  
6. <span data-ttu-id="83f13-130">Klicken Sie im Dialogfeld **Edit String** **Value data** Sie im Feld Geben Sie die Klassen-ID der benutzerdefinierten Worttrennmodul, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="83f13-130">In the **Edit String** dialog box, in the **Value data** box, type the class ID of your custom word breaker, and then choose **OK**.</span></span>
    
  
7. <span data-ttu-id="83f13-131">Starten Sie den SharePoint-Suchhostcontroller und SharePoint neu.</span><span class="sxs-lookup"><span data-stu-id="83f13-131">Restart the SharePoint Search Host Controller and SharePoint Server 2013.</span></span>
    
  
8. <span data-ttu-id="83f13-132">Führen Sie eine vollständige erneute Durchforstung durch.</span><span class="sxs-lookup"><span data-stu-id="83f13-132">Do a full re-crawl.</span></span>
    
  

## <a name="supported-languages-for-word-breaker-customizations-in-sharepoint"></a><span data-ttu-id="83f13-133">Unterstützte Sprachen für die Anpassung der Wörtertrennung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f13-133">Supported languages for word breaker customizations in SharePoint Server 2013</span></span>
<span data-ttu-id="83f13-134"><a name="SP15_SupportedLanguages"> </a></span><span class="sxs-lookup"><span data-stu-id="83f13-134"></span></span>

<span data-ttu-id="83f13-135">Die folgenden Sprachen werden für die Anpassung von Word wörtertrennung unterstützt:</span><span class="sxs-lookup"><span data-stu-id="83f13-135">The following languages are supported for word breaker customization:</span></span>
  
    
    
<span data-ttu-id="83f13-136">Arabisch</span><span class="sxs-lookup"><span data-stu-id="83f13-136">Arabic</span></span>
  
    
    
<span data-ttu-id="83f13-137">Bengali</span><span class="sxs-lookup"><span data-stu-id="83f13-137">Bengali</span></span>
  
    
    
<span data-ttu-id="83f13-138">Bulgarisch</span><span class="sxs-lookup"><span data-stu-id="83f13-138">Bulgarian</span></span>
  
    
    
<span data-ttu-id="83f13-139">Katalanisch</span><span class="sxs-lookup"><span data-stu-id="83f13-139">Catalan</span></span>
  
    
    
<span data-ttu-id="83f13-140">Chinesisch (Volksrepublik China)</span><span class="sxs-lookup"><span data-stu-id="83f13-140">Chinese (People's Republic of China)</span></span>
  
    
    
<span data-ttu-id="83f13-141">Chinesisch (Taiwan)</span><span class="sxs-lookup"><span data-stu-id="83f13-141">Chinese (Taiwan)</span></span>
  
    
    
<span data-ttu-id="83f13-142">Kroatisch</span><span class="sxs-lookup"><span data-stu-id="83f13-142">Croatian</span></span>
  
    
    
<span data-ttu-id="83f13-143">Tschechisch</span><span class="sxs-lookup"><span data-stu-id="83f13-143">Czech</span></span>
  
    
    
<span data-ttu-id="83f13-144">Dänisch</span><span class="sxs-lookup"><span data-stu-id="83f13-144">Danish</span></span>
  
    
    
<span data-ttu-id="83f13-145">Niederländisch (Niederländisch)</span><span class="sxs-lookup"><span data-stu-id="83f13-145">Dutch (Dutch)</span></span>
  
    
    
<span data-ttu-id="83f13-146">Deutsch (Deutschland)</span><span class="sxs-lookup"><span data-stu-id="83f13-146">English (United States)</span></span>
  
    
    
<span data-ttu-id="83f13-147">Estnisch</span><span class="sxs-lookup"><span data-stu-id="83f13-147">Estonian</span></span>
  
    
    
<span data-ttu-id="83f13-148">Finnisch</span><span class="sxs-lookup"><span data-stu-id="83f13-148">Finnish</span></span>
  
    
    
<span data-ttu-id="83f13-149">Französisch (Standard)</span><span class="sxs-lookup"><span data-stu-id="83f13-149">French (Standard)</span></span>
  
    
    
<span data-ttu-id="83f13-150">Deutsch (Standard)</span><span class="sxs-lookup"><span data-stu-id="83f13-150">German (Standard)</span></span>
  
    
    
<span data-ttu-id="83f13-151">Griechisch</span><span class="sxs-lookup"><span data-stu-id="83f13-151">Greek</span></span>
  
    
    
<span data-ttu-id="83f13-152">Gudscharati</span><span class="sxs-lookup"><span data-stu-id="83f13-152">Gujarati</span></span>
  
    
    
<span data-ttu-id="83f13-153">Hebräisch</span><span class="sxs-lookup"><span data-stu-id="83f13-153">Hebrew</span></span>
  
    
    
<span data-ttu-id="83f13-154">Hindi</span><span class="sxs-lookup"><span data-stu-id="83f13-154">Hindi</span></span>
  
    
    
<span data-ttu-id="83f13-155">Ungarisch</span><span class="sxs-lookup"><span data-stu-id="83f13-155">Hungarian</span></span>
  
    
    
<span data-ttu-id="83f13-156">Isländisch</span><span class="sxs-lookup"><span data-stu-id="83f13-156">Icelandic</span></span>
  
    
    
<span data-ttu-id="83f13-157">Indonesisch</span><span class="sxs-lookup"><span data-stu-id="83f13-157">Indonesian</span></span>
  
    
    
<span data-ttu-id="83f13-158">Italienisch (Standard)</span><span class="sxs-lookup"><span data-stu-id="83f13-158">Italian (Default)</span></span>
  
    
    
<span data-ttu-id="83f13-159">Japanisch</span><span class="sxs-lookup"><span data-stu-id="83f13-159">Japanese</span></span>
  
    
    
<span data-ttu-id="83f13-160">Kannada</span><span class="sxs-lookup"><span data-stu-id="83f13-160">Kannada</span></span>
  
    
    
<span data-ttu-id="83f13-161">Kasachisch</span><span class="sxs-lookup"><span data-stu-id="83f13-161">Kazakh</span></span>
  
    
    
<span data-ttu-id="83f13-162">Koreanisch</span><span class="sxs-lookup"><span data-stu-id="83f13-162">Korean</span></span>
  
    
    
<span data-ttu-id="83f13-163">Lettisch</span><span class="sxs-lookup"><span data-stu-id="83f13-163">Latvian</span></span>
  
    
    
<span data-ttu-id="83f13-164">Litauisch</span><span class="sxs-lookup"><span data-stu-id="83f13-164">Lithuanian</span></span>
  
    
    
<span data-ttu-id="83f13-165">Malaiisch</span><span class="sxs-lookup"><span data-stu-id="83f13-165">Malay</span></span>
  
    
    
<span data-ttu-id="83f13-166">Malayalam</span><span class="sxs-lookup"><span data-stu-id="83f13-166">Malayalam</span></span>
  
    
    
<span data-ttu-id="83f13-167">Marathi</span><span class="sxs-lookup"><span data-stu-id="83f13-167">Marathi</span></span>
  
    
    
<span data-ttu-id="83f13-168">Norwegisch</span><span class="sxs-lookup"><span data-stu-id="83f13-168">Norwegian</span></span>
  
    
    
<span data-ttu-id="83f13-169">Polnisch</span><span class="sxs-lookup"><span data-stu-id="83f13-169">Polish</span></span>
  
    
    
<span data-ttu-id="83f13-170">Portugiesisch (Portugiesisch)</span><span class="sxs-lookup"><span data-stu-id="83f13-170">Portuguese (Portuguese)</span></span>
  
    
    
<span data-ttu-id="83f13-171">Punjabi</span><span class="sxs-lookup"><span data-stu-id="83f13-171">Punjabi</span></span>
  
    
    
<span data-ttu-id="83f13-172">Rumänisch</span><span class="sxs-lookup"><span data-stu-id="83f13-172">Romanian</span></span>
  
    
    
<span data-ttu-id="83f13-173">Russisch</span><span class="sxs-lookup"><span data-stu-id="83f13-173">Russian</span></span>
  
    
    
<span data-ttu-id="83f13-174">Serbisch (Kyrillisch)</span><span class="sxs-lookup"><span data-stu-id="83f13-174">Serbian (Cyrillic)</span></span>
  
    
    
<span data-ttu-id="83f13-175">Slowakisch</span><span class="sxs-lookup"><span data-stu-id="83f13-175">Slovak</span></span>
  
    
    
<span data-ttu-id="83f13-176">Slowenisch</span><span class="sxs-lookup"><span data-stu-id="83f13-176">Slovenian</span></span>
  
    
    
<span data-ttu-id="83f13-177">Spanisch (Moderne Sortierung)</span><span class="sxs-lookup"><span data-stu-id="83f13-177">Spanish (Modern Sort)</span></span>
  
    
    
<span data-ttu-id="83f13-178">Schwedisch</span><span class="sxs-lookup"><span data-stu-id="83f13-178">Swedish</span></span>
  
    
    
<span data-ttu-id="83f13-179">Tamil</span><span class="sxs-lookup"><span data-stu-id="83f13-179">Tamil</span></span>
  
    
    
<span data-ttu-id="83f13-180">Telugu</span><span class="sxs-lookup"><span data-stu-id="83f13-180">Telugu</span></span>
  
    
    
<span data-ttu-id="83f13-181">Thailändisch</span><span class="sxs-lookup"><span data-stu-id="83f13-181">Thai</span></span>
  
    
    
<span data-ttu-id="83f13-182">Türkisch</span><span class="sxs-lookup"><span data-stu-id="83f13-182">Turkish</span></span>
  
    
    
<span data-ttu-id="83f13-183">Ukrainisch</span><span class="sxs-lookup"><span data-stu-id="83f13-183">Ukrainian</span></span>
  
    
    
<span data-ttu-id="83f13-184">Urdu</span><span class="sxs-lookup"><span data-stu-id="83f13-184">Urdu</span></span>
  
    
    
<span data-ttu-id="83f13-185">Vietnamesisch</span><span class="sxs-lookup"><span data-stu-id="83f13-185">Vietnamese</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="83f13-186">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="83f13-186">Additional resources</span></span>
<span data-ttu-id="83f13-187"><a name="SP15wordbreakers_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="83f13-187"></span></span>


-  [<span data-ttu-id="83f13-188">Konfigurieren der Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f13-188">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  <span data-ttu-id="83f13-189">
  [Implementieren von einem Worttrennmodul](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="83f13-189">[Implementing a Word Breaker](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)</span></span>
    
  
-  <span data-ttu-id="83f13-190">
  [IWordBreaker-Schnittstelle](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="83f13-190">[IWordBreaker interface](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)</span></span>
    
  

