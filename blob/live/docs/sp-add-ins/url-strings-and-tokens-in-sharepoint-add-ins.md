---
title: URL-Zeichenfolgen und Tokens in SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f72b508740db3653cc9515fe3eb9800a0038b1aa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="url-strings-and-tokens-in-sharepoint-add-ins"></a><span data-ttu-id="59020-102">URL-Zeichenfolgen und Tokens in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="59020-102">URL strings and tokens in SharePoint Add-ins</span></span>
<span data-ttu-id="59020-103">Erfahren Sie, welche URL-Tokens für die Verwendung in SharePoint-Add-Ins verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="59020-103">Learn which URL tokens are available for use in SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="59020-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="59020-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="59020-p102">**Wichtig** Allgemeine Informationen zur Erstellung von URLs in SharePoint und zur Verwendung von Token in diesen URLs finden Sie unter [URLs und Token in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx). In diesem Thema werden die in SharePoint-Add-Ins verfügbaren Token beschrieben.</span><span class="sxs-lookup"><span data-stu-id="59020-p102">**Important**  For general information about constructing URLs in SharePoint and the use of tokens in those URLs, see  [URLs and tokens in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx). This topic describes the tokens that are available in SharePoint Add-ins.</span></span>
 


## 
<span data-ttu-id="59020-109"><a name="URLtokens"> </a></span><span class="sxs-lookup"><span data-stu-id="59020-109"></span></span>

<span data-ttu-id="59020-110">SharePoint unterstützt die in der folgenden Tabelle aufgeführten Token in SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="59020-110">SharePoint supports the tokens listed in the following tables for use in SharePoint Add-ins.</span></span>
 

 
<span data-ttu-id="59020-p103">Die Token in den Tabellen dieses Abschnitts können in einer Vielzahl von Situationen bei der Entwicklung von SharePoint-Add-Ins in URLs verwendet werden, so beispielsweise in benutzerdefinierten Aktionen und in Links auf benutzerdefinierten Seiten. In einigen Kontexten können einige dieser URLs nicht verwendet werden. Drei der wichtigsten Orte, an denen nur eine eingeschränkte Liste der Token verwendet werden kann, sind die Startseite eines Add-Ins, eine benutzerdefinierte Aktion im Hostweb und die **Src**-Eigenschaft eines Add-In-Webparts. Diese werden in separaten Spalten aufgeführt. * Es handelt sich dabei **jedoch nicht um eine erschöpfende Liste der Orte, an denen Token verwendet werden können.***</span><span class="sxs-lookup"><span data-stu-id="59020-p103">The tokens in the tables of this section can be used in URLs in a wide variety of situations in development of SharePoint Add-ins, such as in Custom Actions and in links on custom pages. In some contexts, some of these tokens cannot be used. Three of the most important places where only a restricted list of tokens can be used are the start page of an add-in, a custom action on the host web, and the  **Src** property of an add-in part. These are called out in separate columns, * **but these three are not an exhaustive list of places where tokens can be used.***</span></span> 
 

 
<span data-ttu-id="59020-p104">Die Spalte **StartPage** gibt an, ob das Token im **StartPage**-Element eines Add-In-Manifests verwendet werden kann. Die Spalte **Benutzerdefinierte Aktion** gibt an, ob das Token in der URL einer benutzerdefinierten Aktion in einem Hostweb verwendet werden kann. Die Spalte **Add-In-Webpart** gibt an, ob das Token in der **Src**-Eigenschaft des Add-In-Webparts verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="59020-p104">The  **StartPage** column specifies whether the token can be used in the **StartPage** element of an add-in manifest. The **Custom Action** column specifies whether the token can be used in the URL of a custom action on a host web. The **Add-in Part** column specifies whether the token can be used in the **Src** property of the add-in part.</span></span>
 

 

<span data-ttu-id="59020-118">**Token, die am Anfang einer URL in einer SharePoint-Add-In verwendet werden können**</span><span class="sxs-lookup"><span data-stu-id="59020-118">**Tokens that can be used at the beginning of a URL in a SharePoint Add-in**</span></span>


|<span data-ttu-id="59020-119">**Token**</span><span class="sxs-lookup"><span data-stu-id="59020-119">**Token**</span></span>|<span data-ttu-id="59020-120">**Wird aufgelöst zu**</span><span class="sxs-lookup"><span data-stu-id="59020-120">**Resolves to**</span></span>|<span data-ttu-id="59020-121">**StartPage**</span><span class="sxs-lookup"><span data-stu-id="59020-121">**StartPage**</span></span>|<span data-ttu-id="59020-122">**Benutzerdefinierte Aktion**</span><span class="sxs-lookup"><span data-stu-id="59020-122">**Custom Action**</span></span>|<span data-ttu-id="59020-123">**Add-In-Webpart**</span><span class="sxs-lookup"><span data-stu-id="59020-123">**Add-in Part**</span></span>|<span data-ttu-id="59020-124">**Bemerkungen**</span><span class="sxs-lookup"><span data-stu-id="59020-124">**Remarks**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="59020-125">~appWebUrl</span><span class="sxs-lookup"><span data-stu-id="59020-125">~appWebUrl</span></span>|<span data-ttu-id="59020-126">Die URL des Add-In-Webs einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-126">The URL of the add-in web of a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-127">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-127">Yes</span></span>|<span data-ttu-id="59020-128">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-128">Yes</span></span>|<span data-ttu-id="59020-129">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-129">Yes</span></span>|<span data-ttu-id="59020-p105">Dieses Token sollte nur außerhalb des Add-In-Webparts verwendet werden. Innerhalb des Add-In-Webparts verwenden Sie **~site** als URL des Add-In-Webparts.</span><span class="sxs-lookup"><span data-stu-id="59020-p105">This token should be used only outside an add-in web. Within the add-in web itself, use  **~site** for the URL of the add-in web.</span></span>|
|<span data-ttu-id="59020-132">~controlTemplates</span><span class="sxs-lookup"><span data-stu-id="59020-132">~controlTemplates</span></span>|<span data-ttu-id="59020-133">Die URL des virtuellen Ordners ControlTemplates der aktuellen Website</span><span class="sxs-lookup"><span data-stu-id="59020-133">The URL of the ControlTemplates virtual folder for the current website.</span></span>|<span data-ttu-id="59020-134">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-134">No</span></span>|<span data-ttu-id="59020-135">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-135">No</span></span>|<span data-ttu-id="59020-136">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-136">No</span></span>||
|<span data-ttu-id="59020-137">~hostUrl</span><span class="sxs-lookup"><span data-stu-id="59020-137">~hostUrl</span></span>|<span data-ttu-id="59020-138">Die URL des Hostweb</span><span class="sxs-lookup"><span data-stu-id="59020-138">The URL of the host web.</span></span>|<span data-ttu-id="59020-139">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-139">No</span></span>|<span data-ttu-id="59020-140">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-140">No</span></span>|<span data-ttu-id="59020-141">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-141">Yes</span></span>||
|<span data-ttu-id="59020-142">~hostLogoUrl</span><span class="sxs-lookup"><span data-stu-id="59020-142">~hostLogoUrl</span></span>|<span data-ttu-id="59020-143">Die URL des Logos des Hostweb</span><span class="sxs-lookup"><span data-stu-id="59020-143">The URL of the logo of the host web.</span></span>|<span data-ttu-id="59020-144">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-144">No</span></span>|<span data-ttu-id="59020-145">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-145">No</span></span>|<span data-ttu-id="59020-146">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-146">No</span></span>||
|<span data-ttu-id="59020-147">~layouts</span><span class="sxs-lookup"><span data-stu-id="59020-147">~layouts</span></span>|<span data-ttu-id="59020-148">Die URL des virtuellen Ordners Layouts für die aktuelle Website</span><span class="sxs-lookup"><span data-stu-id="59020-148">The URL of the Layouts virtual folder for the current website.</span></span>|<span data-ttu-id="59020-149">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-149">No</span></span>|<span data-ttu-id="59020-150">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-150">No</span></span>|<span data-ttu-id="59020-151">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-151">No</span></span>||
|<span data-ttu-id="59020-152">~remoteAppUrl</span><span class="sxs-lookup"><span data-stu-id="59020-152">~remoteAppUrl</span></span>|<span data-ttu-id="59020-153">Die URL einer Remotewebanwendung in einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-153">The URL of a remote web application in a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-154">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-154">Yes</span></span>|<span data-ttu-id="59020-155">"Ja" im Hostweb, aber "Nein" im Add-In-Webpart</span><span class="sxs-lookup"><span data-stu-id="59020-155">Yes, in the host web, but No in the add-in web.</span></span>|<span data-ttu-id="59020-156">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-156">Yes</span></span>|<span data-ttu-id="59020-p106">Wenn Sie nicht Microsoft Office Developer Tools für Visual Studio zum Entwickeln Ihres SharePoint-Add-Ins verwenden, können Sie **~remoteAppUrl** nicht in der **StartPage**-URL verwenden. Wenn Sie jedoch Visual Studio und die Tools verwenden, können Sie dieses Token für jedes von einem Anbieter gehostete Add-In verwenden. Es wird aufgelöst, wenn das Add-In von Visual Studio gepackt wird. Bei dieser Art der Nutzung handelt es sich dann eher um ein Visual Studio-Token als um ein SharePoint-Token. Es kann außerhalb des Add-In-Manifests verwendet werden, auch wenn Sie Microsoft Office Developer Tools für Visual Studio nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="59020-p106">If you are not using Microsoft Office Developer Tools for Visual Studio to develop your SharePoint Add-in, you cannot use  **~remoteAppUrl** in the **StartPage** URL. However, when you are using Visual Studio and the tools, you can use this token for any provider-hosted add-in and it is resolved when Visual Studio packages the add-in. In this usage, it is really more of a Visual Studio token than a SharePoint token. It can be used outside the add-in manifest, even when you are not using Microsoft Office Developer Tools for Visual Studio.</span></span>|
|<span data-ttu-id="59020-161">~site</span><span class="sxs-lookup"><span data-stu-id="59020-161">~site</span></span>|<span data-ttu-id="59020-162">Die URL der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="59020-162">The URL of the current website.</span></span>|<span data-ttu-id="59020-163">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-163">No</span></span>|<span data-ttu-id="59020-164">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-164">No</span></span>|<span data-ttu-id="59020-165">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-165">Yes</span></span>||
|<span data-ttu-id="59020-166">~sitecollection</span><span class="sxs-lookup"><span data-stu-id="59020-166">~sitecollection</span></span>|<span data-ttu-id="59020-167">Die URL der übergeordneten Websitesammlung der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="59020-167">The URL of the parent site collection of the current website.</span></span>|<span data-ttu-id="59020-168">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-168">No</span></span>|<span data-ttu-id="59020-169">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-169">No</span></span>|<span data-ttu-id="59020-170">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-170">Yes</span></span>||
<span data-ttu-id="59020-p107">Sofern nicht anders angegeben, kann keines der Token in der nächsten Tabelle im  *Pfad*  -Teil des **Src** -Eigenschaftenwerts des Add-In-Webparts verwendet werden. Die Spalte **Add-In-Webpart** bezieht sich auf deren Verwendung im *Abfragezeichenfolge*  -Teil des Werts.</span><span class="sxs-lookup"><span data-stu-id="59020-p107">Except where indicated otherwise, none of the tokens in the next table can be used in the  *path*  portion of the **Src** property value of the add-in part. The **Add-in Part** column refers to their use in the *query string*  portion of the value.</span></span>
 

 

<span data-ttu-id="59020-173">**Token, die innerhalb einer URL verwendet werden können**</span><span class="sxs-lookup"><span data-stu-id="59020-173">**Tokens that can be used inside a URL**</span></span>


|<span data-ttu-id="59020-174">**Token**</span><span class="sxs-lookup"><span data-stu-id="59020-174">**Token**</span></span>|<span data-ttu-id="59020-175">**Wird aufgelöst zu**</span><span class="sxs-lookup"><span data-stu-id="59020-175">**Resolves to**</span></span>|<span data-ttu-id="59020-176">**StartPage**</span><span class="sxs-lookup"><span data-stu-id="59020-176">**StartPage**</span></span>|<span data-ttu-id="59020-177">**Benutzerdefinierte Aktion**</span><span class="sxs-lookup"><span data-stu-id="59020-177">**Custom Action**</span></span>|<span data-ttu-id="59020-178">**Add-In-Webpart**</span><span class="sxs-lookup"><span data-stu-id="59020-178">**Add-in Part**</span></span>|<span data-ttu-id="59020-179">**Bemerkungen**</span><span class="sxs-lookup"><span data-stu-id="59020-179">**Remarks**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="59020-180">{AppContextToken}</span><span class="sxs-lookup"><span data-stu-id="59020-180">{AppContextToken}</span></span>|<span data-ttu-id="59020-181">Das OAuth-Kontexttoken für das Add-In</span><span class="sxs-lookup"><span data-stu-id="59020-181">The OAuth context token for the add-in.</span></span>|<span data-ttu-id="59020-182">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-182">No</span></span>|<span data-ttu-id="59020-183">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-183">No</span></span>|<span data-ttu-id="59020-184">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-184">No</span></span>||
|<span data-ttu-id="59020-185">{AppWebUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-185">{AppWebUrl}</span></span>|<span data-ttu-id="59020-186">Die URL des Add-In-Webparts in einer SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="59020-186">The URL of the add-in web in a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-187">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-187">Yes</span></span>|<span data-ttu-id="59020-188">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-188">Yes</span></span>|<span data-ttu-id="59020-189">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-189">Yes</span></span>|<span data-ttu-id="59020-p108">Dieses Token sollte nur außerhalb eines Add-In-Webparts verwendet werden. Innerhalb des Add-In-Webparts verwenden Sie **{Site}** als URL des Add-In-Webparts.</span><span class="sxs-lookup"><span data-stu-id="59020-p108">This token should be used only outside an add-in web. Within the add-in web itself, use  **{Site}** for the URL of the add-in web.</span></span>|
|<span data-ttu-id="59020-192">{ClientTag}</span><span class="sxs-lookup"><span data-stu-id="59020-192">{ClientTag}</span></span>|<span data-ttu-id="59020-193">Die Clientcache-Kontrollnummer (Clienttag) für die aktuelle Website</span><span class="sxs-lookup"><span data-stu-id="59020-193">The client cache control number (client tag) for the current website.</span></span>|<span data-ttu-id="59020-194">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-194">Yes</span></span>|<span data-ttu-id="59020-195">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-195">Yes</span></span>|<span data-ttu-id="59020-196">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-196">Yes</span></span>||
|<span data-ttu-id="59020-197">{HostLogoUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-197">{HostLogoUrl}</span></span>|<span data-ttu-id="59020-198">Das Logo für das Hostweb einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-198">The logo for the host web of a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-199">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-199">Yes</span></span>|<span data-ttu-id="59020-200">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-200">Yes</span></span>|<span data-ttu-id="59020-201">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-201">Yes</span></span>||
|<span data-ttu-id="59020-202">{HostTitle}</span><span class="sxs-lookup"><span data-stu-id="59020-202">{HostTitle}</span></span>|<span data-ttu-id="59020-203">Der Titel des Hostwebs einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-203">The title of the host web of a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-204">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-204">Yes</span></span>|<span data-ttu-id="59020-205">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-205">Yes</span></span>|<span data-ttu-id="59020-206">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-206">Yes</span></span>||
|<span data-ttu-id="59020-207">{HostUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-207">{HostUrl}</span></span>|<span data-ttu-id="59020-208">Die URL des Hostwebs einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-208">The URL of the host web of a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-209">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-209">Yes</span></span>|<span data-ttu-id="59020-210">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-210">Yes</span></span>|<span data-ttu-id="59020-211">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-211">Yes</span></span>||
|<span data-ttu-id="59020-212">{ItemId}</span><span class="sxs-lookup"><span data-stu-id="59020-212">{ItemId}</span></span>|<span data-ttu-id="59020-213">Die ID eines Elements in einer Liste oder Bibliothek (eine ganze Zahl)</span><span class="sxs-lookup"><span data-stu-id="59020-213">The ID of an item in a list or library (an integer).</span></span>|<span data-ttu-id="59020-214">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-214">No</span></span>|<span data-ttu-id="59020-215">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-215">Yes</span></span>|<span data-ttu-id="59020-216">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-216">No</span></span>||
|<span data-ttu-id="59020-217">{ItemUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-217">{ItemUrl}</span></span>|<span data-ttu-id="59020-218">Die URL des Elements, an dem eine Aktion ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="59020-218">The URL of the item being acted upon.</span></span> |<span data-ttu-id="59020-219">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-219">No</span></span>|<span data-ttu-id="59020-220">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-220">Yes</span></span>|<span data-ttu-id="59020-221">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-221">No</span></span>||
|<span data-ttu-id="59020-222">{Language}</span><span class="sxs-lookup"><span data-stu-id="59020-222">{Language}</span></span>|<span data-ttu-id="59020-223">Die aktuelle Sprach-/Kultureinstellung des Hostwebs einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-223">The current language/culture of the host web of a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-224">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-224">Yes</span></span>|<span data-ttu-id="59020-225">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-225">Yes</span></span>|<span data-ttu-id="59020-226">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-226">Yes</span></span>||
|<span data-ttu-id="59020-227">{ListId}</span><span class="sxs-lookup"><span data-stu-id="59020-227">{ListId}</span></span>|<span data-ttu-id="59020-228">Die ID der aktuellen Liste (eine GUID).</span><span class="sxs-lookup"><span data-stu-id="59020-228">The ID of the current list (a GUID).</span></span>|<span data-ttu-id="59020-229">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-229">No</span></span>|<span data-ttu-id="59020-230">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-230">Yes</span></span>|<span data-ttu-id="59020-231">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-231">No</span></span>||
|<span data-ttu-id="59020-232">{ProductNumber}</span><span class="sxs-lookup"><span data-stu-id="59020-232">{ProductNumber}</span></span>|<span data-ttu-id="59020-233">Die vollständige Buildversionsnummer der SharePoint-Farm</span><span class="sxs-lookup"><span data-stu-id="59020-233">The full build version number of the SharePoint farm.</span></span>|<span data-ttu-id="59020-234">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-234">Yes</span></span>|<span data-ttu-id="59020-235">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-235">Yes</span></span>|<span data-ttu-id="59020-236">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-236">Yes</span></span>|<span data-ttu-id="59020-237">Beispielwert: "15.0.4433.1011"</span><span class="sxs-lookup"><span data-stu-id="59020-237">An example value is "15.0.4433.1011".</span></span>|
|<span data-ttu-id="59020-238">{RecurrenceId}</span><span class="sxs-lookup"><span data-stu-id="59020-238">{RecurrenceId}</span></span>|<span data-ttu-id="59020-239">Der Wiederholungsindex eines sich wiederholenden Ereignisses.</span><span class="sxs-lookup"><span data-stu-id="59020-239">The recurrence index of a recurring event.</span></span>|<span data-ttu-id="59020-240">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-240">No</span></span>|<span data-ttu-id="59020-241">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-241">Yes</span></span>|<span data-ttu-id="59020-242">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-242">No</span></span>|<span data-ttu-id="59020-243">In Kontextmenüs von Listenelementen wird die Verwendung dieses Tokens nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="59020-243">This token is not supported for use in the context menus of list items.</span></span>|
|<span data-ttu-id="59020-244">{RemoteAppUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-244">{RemoteAppUrl}</span></span>|<span data-ttu-id="59020-245">Die URL einer Remotewebanwendung in einer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="59020-245">The URL of a remote web application in a SharePoint Add-in.</span></span>|<span data-ttu-id="59020-246">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-246">Yes</span></span>|<span data-ttu-id="59020-247">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-247">Yes</span></span>|<span data-ttu-id="59020-248">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-248">Yes</span></span>||
|<span data-ttu-id="59020-249">{Site}</span><span class="sxs-lookup"><span data-stu-id="59020-249">{Site}</span></span>|<span data-ttu-id="59020-250">Die URL der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="59020-250">The URL of the current website.</span></span>|<span data-ttu-id="59020-251">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-251">No</span></span>|<span data-ttu-id="59020-252">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-252">Yes</span></span>|<span data-ttu-id="59020-253">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-253">Yes</span></span>||
|<span data-ttu-id="59020-254">{SiteCollection}</span><span class="sxs-lookup"><span data-stu-id="59020-254">{SiteCollection}</span></span>|<span data-ttu-id="59020-255">Die URL der übergeordneten Website der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="59020-255">The URL of the parent site of the current website.</span></span>|<span data-ttu-id="59020-256">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-256">No</span></span>|<span data-ttu-id="59020-257">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-257">Yes</span></span>|<span data-ttu-id="59020-258">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-258">Yes</span></span>||
|<span data-ttu-id="59020-259">{SiteUrl}</span><span class="sxs-lookup"><span data-stu-id="59020-259">{SiteUrl}</span></span>|<span data-ttu-id="59020-260">Die URL der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="59020-260">The URL of the current website.</span></span>|<span data-ttu-id="59020-261">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-261">No</span></span>|<span data-ttu-id="59020-262">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-262">Yes</span></span>|<span data-ttu-id="59020-263">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-263">No</span></span>||
|<span data-ttu-id="59020-264">{Source}</span><span class="sxs-lookup"><span data-stu-id="59020-264">{Source}</span></span>|<span data-ttu-id="59020-265">Die URL der HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="59020-265">The HTTP Request URL.</span></span>|<span data-ttu-id="59020-266">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-266">No</span></span>|<span data-ttu-id="59020-267">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-267">Yes</span></span>|<span data-ttu-id="59020-268">Nein</span><span class="sxs-lookup"><span data-stu-id="59020-268">No</span></span>||
|<span data-ttu-id="59020-269">{StandardTokens}</span><span class="sxs-lookup"><span data-stu-id="59020-269">{StandardTokens}</span></span>|<span data-ttu-id="59020-270">Weitere Informationen finden Sie in der "Anmerkungen".</span><span class="sxs-lookup"><span data-stu-id="59020-270">See Remarks.</span></span>|<span data-ttu-id="59020-271">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-271">Yes</span></span>|<span data-ttu-id="59020-272">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-272">Yes</span></span>|<span data-ttu-id="59020-273">Ja</span><span class="sxs-lookup"><span data-stu-id="59020-273">Yes</span></span>|<span data-ttu-id="59020-p109">Dieses Token ist die Kombination von fünf anderen Token. Es wird anfänglich in  `SPHostUrl={HostUrl}&amp;SPAppWebUrl={AppWebUrl}&amp;SPLanguage={Language}&amp;SPClientTag={ClientTag}&amp;SPProductNumber={ProductNumber}` aufgelöst. Dann wird jedes dieser Token aufgelöst. Wenn kein Add-In-Webpart vorhanden ist, ist `&amp;SPAppWebUrl={AppWebUrl}` nicht enthalten. </span><span class="sxs-lookup"><span data-stu-id="59020-p109">This combines five other tokens. It initially resolves to  `SPHostUrl={HostUrl}&amp;SPAppWebUrl={AppWebUrl}&amp;SPLanguage={Language}&amp;SPClientTag={ClientTag}&amp;SPProductNumber={ProductNumber}`. Then each of these tokens resolves. If there is no add-in web, the portion  `&amp;SPAppWebUrl={AppWebUrl}` is not present.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="59020-278">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="59020-278">Additional resources</span></span>
<span data-ttu-id="59020-279"><a name="SP15URLstrings_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="59020-279"></span></span>


-  [<span data-ttu-id="59020-280">Erweiterte Extranetunterstützung</span><span class="sxs-lookup"><span data-stu-id="59020-280">Advanced Extranet Support</span></span>](http://msdn.microsoft.com/library/21d67796-23c5-4339-8f0e-124208d21ab2%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="59020-281">Abrufen von Verweisen auf Websites, Webanwendungen und andere Schlüsselobjekte</span><span class="sxs-lookup"><span data-stu-id="59020-281">Getting References to Sites, Web Applications, and other Key Objects</span></span>](http://msdn.microsoft.com/library/8623ef1d-e3cc-426c-84a3-6379e0ae284f%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="59020-282">Arbeiten mit Listenobjekten und Auflistungen</span><span class="sxs-lookup"><span data-stu-id="59020-282">Working with List Objects and Collections</span></span>](http://msdn.microsoft.com/library/d4167b10-6f1e-49f1-8b22-16ce20012a27%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="59020-283">Verwenden des Objektmodells für grundlegende Aufgaben</span><span class="sxs-lookup"><span data-stu-id="59020-283">Sample Object Model Tasks</span></span>](http://msdn.microsoft.com/library/94d6898d-6a0f-43a7-ad06-1b27ec6916ea%28Office.15%29.aspx)
    
 
