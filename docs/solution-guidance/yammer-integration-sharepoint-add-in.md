---
title: Yammer-Integration in die SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: a83623a32b398ae32ce7cebc7ac5d37c823a2e3f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="yammer-integration-in-the-sharepoint-add-in-model"></a><span data-ttu-id="d6bc3-102">Yammer-Integration in die SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="d6bc3-102">Yammer integration in the SharePoint add-in model</span></span>
=================================================

<a name="summary"></a><span data-ttu-id="d6bc3-103">Summary</span><span class="sxs-lookup"><span data-stu-id="d6bc3-103">Summary</span></span>
-------

<span data-ttu-id="d6bc3-104">Der gewählten Ansatz zum Integrieren von Yammer mit SharePoint ist in das neue SharePoint-Add-in-Modell identisch mit vollständigen vertrauen Code unverändert.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-104">The approach you take to integrate Yammer with SharePoint is the same in the new SharePoint Add-in model as it is with Full Trust Code.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="d6bc3-105">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="d6bc3-105">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="d6bc3-106">In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Integrieren von Yammer mit SharePoint enthalten.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-106">As a rule of a thumb, we would like to provide the following high level guidelines to integrate Yammer with SharePoint.</span></span>

- <span data-ttu-id="d6bc3-107">Yammer-Integration in lokalen und Office 365 SharePoint-Umgebungen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-107">Yammer integration may be used in both on-premises and Office 365  SharePoint environments.</span></span>
- <span data-ttu-id="d6bc3-108">Das remote provisioning Muster können zum Erstellen von Yammer-Gruppen und/oder OpenGraph Yammer-Objekte, um Unterhaltungen zu erleichtern, wenn Sie neue SharePoint-Websites erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-108">You can use the remote provisioning pattern to create Yammer groups and/or Yammer OpenGraph objects to facilitate conversations when you create new SharePoint sites.</span></span>
- <span data-ttu-id="d6bc3-109">Sie können die Out-of-the-Box einbetten Funktionalität, um schnell und einfach zu Yammer mit SharePoint integrieren.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-109">You can use the out-of-the-box embed functionality to quickly and easily integrate Yammer with SharePoint.</span></span>
    + <span data-ttu-id="d6bc3-110">Zum Einbetten verwenden Sie benötigen Sie eine HTML-Container 400 Pixel oder größer in der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-110">To use embed you need a HTML container 400 pixels or larger in your application.</span></span>
- <span data-ttu-id="d6bc3-111">Die Yammer-SDKs und REST-APIs können Sie benutzerdefinierte Integration-Funktionalität erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-111">You can use the Yammer SDKs and REST APIs to create customized integration functionality.</span></span>

<a name="options-to-integrate-yammer-with-sharepoint"></a><span data-ttu-id="d6bc3-112">Optionen zum Integrieren von Yammer mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6bc3-112">Options to integrate Yammer with SharePoint</span></span>
-------------------------------------------

<span data-ttu-id="d6bc3-113">Sie müssen einige Optionen zum Integrieren von Yammer mit SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-113">You have a few options to integrate Yammer with SharePoint.</span></span>

- <span data-ttu-id="d6bc3-114">Einbinden</span><span class="sxs-lookup"><span data-stu-id="d6bc3-114">Embed</span></span>
    + <span data-ttu-id="d6bc3-115">Gruppe, Thema My, und Benutzer Feeds</span><span class="sxs-lookup"><span data-stu-id="d6bc3-115">Group, Topic, My, and User Feeds</span></span>
    + <span data-ttu-id="d6bc3-116">OpenGraph-Feeds</span><span class="sxs-lookup"><span data-stu-id="d6bc3-116">OpenGraph Feeds</span></span>
- <span data-ttu-id="d6bc3-117">Yammer-OpenGraph API und/oder Yammer-REST-API mit Yammer SDKs</span><span class="sxs-lookup"><span data-stu-id="d6bc3-117">Yammer OpenGraph API and/or Yammer REST API with Yammer SDKs</span></span>
    
<a name="embed"></a><span data-ttu-id="d6bc3-118">Einbinden</span><span class="sxs-lookup"><span data-stu-id="d6bc3-118">Embed</span></span>
-----

<span data-ttu-id="d6bc3-119">Bei dieser Option betten Sie einen Yammer-Feeds in einer SharePoint-Webseite.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-119">In this option you embed a Yammer feed in a SharePoint web page.</span></span>
    
- <span data-ttu-id="d6bc3-120">Diese Option ist schnell und einfach implementiert.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-120">This option is quickly and easily implemented.</span></span>
- <span data-ttu-id="d6bc3-121">Diese Option können Sie steuern, beschränkt Aspekte des Feeds und wie es angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-121">This option allows you to control limited aspects of the feed and how it appears.</span></span>

<span data-ttu-id="d6bc3-122">Sieht folgendermaßen aus Ihrer SharePoint-Seite einbetten verwenden:</span><span class="sxs-lookup"><span data-stu-id="d6bc3-122">Using embed looks like this in your SharePoint page:</span></span>

![Eine standard SharePoint Seite der Teamwebsite mit einem Textfeld mit dem Text, eine Unterhaltung beginnen.](media/Recipes/Yammer/YammerEmbed.png)

<span data-ttu-id="d6bc3-125">In der folgenden Tabelle wird beschrieben, jede Art von Yammer können Sie mit zugreifen Feed Out-of-Box einbetten.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-125">The following table describes each type of Yammer feed you can access with embed out-of-the-box.</span></span>

<span data-ttu-id="d6bc3-126">Feed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-126">Feed</span></span> | <span data-ttu-id="d6bc3-127">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6bc3-127">Description</span></span> | <span data-ttu-id="d6bc3-128">FeedType</span><span class="sxs-lookup"><span data-stu-id="d6bc3-128">FeedType</span></span> | <span data-ttu-id="d6bc3-129">Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="d6bc3-129">Use Case</span></span>
---- | ----------- | -------- | --------
<span data-ttu-id="d6bc3-130">Mein Newsfeed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-130">My Feed</span></span> | <span data-ttu-id="d6bc3-131">Meine Feeds sind, in dem Unterhaltungen für Yammer-Benutzer übermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-131">My Feeds are where conversations are delivered for Yammer users.</span></span> | <span data-ttu-id="d6bc3-132">MyFeed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-132">MyFeed</span></span> | <span data-ttu-id="d6bc3-133">Meine Website-Homepage oder einen Arbeitsbereich-Website.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-133">My Site homepage or workspace site.</span></span>
<span data-ttu-id="d6bc3-134">Benutzer-Feed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-134">User Feed</span></span> | <span data-ttu-id="d6bc3-135">Alle Unterhaltungen von einem bestimmten Benutzer in Yammer veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-135">All the conversations posted by a specific user in Yammer.</span></span> | <span data-ttu-id="d6bc3-136">Benutzer</span><span class="sxs-lookup"><span data-stu-id="d6bc3-136">User</span></span> | <span data-ttu-id="d6bc3-137">Profilseiten für Benutzer in ein Verzeichnis des Systems.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-137">Profile pages for users in a system directory.</span></span>
<span data-ttu-id="d6bc3-138">Thema-Feed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-138">Topic Feed</span></span> | <span data-ttu-id="d6bc3-139">Ein Feed der Unterhaltungen an, die mit einem Thema in Yammer markiert wurden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-139">A feed of conversations that have been tagged with a topic in Yammer.</span></span> | <span data-ttu-id="d6bc3-140">Thema</span><span class="sxs-lookup"><span data-stu-id="d6bc3-140">Topic</span></span> | <span data-ttu-id="d6bc3-141">Die Seite ein Ereignis in einem Intranet.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-141">An event page on an intranet.</span></span>
<span data-ttu-id="d6bc3-142">Gruppenfeed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-142">Group Feed</span></span> | <span data-ttu-id="d6bc3-143">Ein Feed der Unterhaltungen an, die in einer angegebenen Gruppe gebucht wurden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-143">A feed of conversations that have been posted in a specified group.</span></span> | <span data-ttu-id="d6bc3-144">Gruppe</span><span class="sxs-lookup"><span data-stu-id="d6bc3-144">Group</span></span> | <span data-ttu-id="d6bc3-145">Eine Seite Team in einem Intranet.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-145">A team page on an intranet.</span></span>

<span data-ttu-id="d6bc3-146">Wenn Sie die Funktionen des Out-of-Box-Yammer-Feeds in der Tabelle oben hinausgehen müssen kann verwenden die OpenGraph Option einbetten.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-146">If you need to go beyond the capabilities of the out-of-the-box Yammer feeds in the table above you can use the OpenGraph embed option.</span></span>  <span data-ttu-id="d6bc3-147">Diese Option gibt Ihnen mehr Kontrolle des Feeds.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-147">This option gives you more control of the feed.</span></span>  <span data-ttu-id="d6bc3-148">Die folgende Tabelle veranschaulicht ein Beispiel dafür.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-148">The following table illustrates such an example.</span></span>

<span data-ttu-id="d6bc3-149">Feed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-149">Feed</span></span> | <span data-ttu-id="d6bc3-150">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6bc3-150">Description</span></span> | <span data-ttu-id="d6bc3-151">FeedType</span><span class="sxs-lookup"><span data-stu-id="d6bc3-151">FeedType</span></span> | <span data-ttu-id="d6bc3-152">Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="d6bc3-152">Use Case</span></span>
---- | ----------- | -------- | --------
<span data-ttu-id="d6bc3-153">Kommentar-Feed</span><span class="sxs-lookup"><span data-stu-id="d6bc3-153">Comment  Feed</span></span> | <span data-ttu-id="d6bc3-154">Mithilfe des Yammer-API Open Diagramm um Unterhaltung, um ein Application-Objekt zu erleichtern.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-154">Uses Yammer’s Open Graph API to facilitate conversation around an application object.</span></span> | <span data-ttu-id="d6bc3-155">Benutzerdefiniert</span><span class="sxs-lookup"><span data-stu-id="d6bc3-155">Custom</span></span> | <span data-ttu-id="d6bc3-156">Eine Möglichkeit zur Nutzung in einer benutzerdefinierten CRM-Anwendung oder ein Medium Projektdetailseite in einer digital Asset Management-System.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-156">An opportunity in a custom CRM application, or a media detail page in a digital asset management system.</span></span>

<span data-ttu-id="d6bc3-157">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="d6bc3-157">**When is it a good fit?**</span></span>

<span data-ttu-id="d6bc3-158">Wenn Sie versuchen, Integrieren von Bedürfnisse Yammer-Feeds mit SharePoint-Websites und die Out-of-Box-Funktionen von den Feed Embed Ihre.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-158">When you are trying to integrate Yammer feeds with SharePoint sites and the out-of-the-box capabilities of the embed feed meet your needs.</span></span>

<span data-ttu-id="d6bc3-159">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="d6bc3-159">**Getting Started**</span></span>

<span data-ttu-id="d6bc3-160">Im folgende Beispiel veranschaulicht, wie Websites mit einer Yammer-Feeds des Standorts anstelle der Standard-Newsfeed für die Website bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-160">The following sample demonstrates how to provision sites with a Yammer feed associated with the site in place of the default news feed for the site.</span></span>

- [<span data-ttu-id="d6bc3-161">Provisioning.Yammer (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-161">Provisioning.Yammer (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)

<span data-ttu-id="d6bc3-162">Die **CreateYammerGroupDiscussionPartXml** -Methode in der Klasse [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) stammen aus dem Beispiel [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-162">The **CreateYammerGroupDiscussionPartXml** method in the [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) class comes from the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) sample.</span></span>  <span data-ttu-id="d6bc3-163">Diese Methode erstellt das XML für eine Webpart-Add-in-Definition, die einer SharePoint-Seite hinzugefügt wird, wenn eine Website bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-163">This method creates the XML for an Add-in Part definition that is added to a SharePoint page when a site is provisioned.</span></span>  <span data-ttu-id="d6bc3-164">Beachten Sie die **FeedType: "Gruppe"** Teil des Codes.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-164">Notice the **feedType: 'group'** portion of the code.</span></span>  <span data-ttu-id="d6bc3-165">Hier können Sie sehen, dass die FeedType gesetzt ist, verwenden Sie die FeedType Out-of-Box-Gruppe.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-165">Here you can see the feedType is set to use the out-of-the-box group feedType.</span></span>

    public static string CreateYammerGroupDiscussionPartXml(string yammerNetworkName, int yammerGroupId, bool showHeader, bool showFooter, bool useSSO = true)
    {
        StringBuilder wp = new StringBuilder(100);
        wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
        wp.Append("<webParts>");
        wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
        wp.Append("     <metaData>");
        wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
        wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
        wp.Append("     </metaData>");
        wp.Append("     <data>");
        wp.Append("         <properties>");
        wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
        wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
        wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
        wp.Append("             <property name='Content' type='string'>");
        wp.Append("             <![CDATA[");
        wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
        wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
        wp.Append("                 <script type='text/javascript'>  
                                        yam.connect.embedFeed({ container: '#embedded-feed', network: '"
                                        + yammerNetworkName
                                        + @"', feedType: 'group', feedId: '" + yammerGroupId            
                                        + @"', config: { use_sso: " + useSSO.ToString().ToLower()           
                                        + @", header: " + showHeader.ToString().ToLower()
                                        + @", footer: " + showFooter.ToString().ToLower()
                                        + " }}); </script>");
        wp.Append("             ]]>");
        wp.Append("             </property>");
        wp.Append("         </properties>");
        wp.Append("     </data>");
        wp.Append(" </webPart>");
        wp.Append("</webParts>");

        return wp.ToString();
    }

<span data-ttu-id="d6bc3-166">Die **CreateYammerOpenGraphDiscussionPartXml** -Methode in der Klasse [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) stammen aus dem Beispiel [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-166">The **CreateYammerOpenGraphDiscussionPartXml** method in the [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) class comes from the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) sample.</span></span>  <span data-ttu-id="d6bc3-167">Diese Methode erstellt das XML für eine Webpart-Add-in-Definition, die einer SharePoint-Seite hinzugefügt wird, wenn eine Website bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-167">This method creates the XML for an Add-in Part definition that is added to a SharePoint page when a site is provisioned.</span></span>  <span data-ttu-id="d6bc3-168">Beachten Sie die **FeedType: 'Öffnen-Diagramm'** Teil des Codes.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-168">Notice the **feedType: 'open-graph'** portion of the code.</span></span>  <span data-ttu-id="d6bc3-169">Hier können Sie sehen, dass die FeedType festgelegt ist, die OpenGraph-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-169">Here you can see the feedType is set to use the OpenGraph API.</span></span>

    public static string CreateYammerOpenGraphDiscussionPartXml(string yammerNetworkName, string url, bool showHeader, 
                                                                    bool showFooter, string postTitle="", string postImageUrl="", 
                                                                    bool useSso = true, string groupId = "")
        {
            StringBuilder wp = new StringBuilder(100);
            wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
            wp.Append("<webParts>");
            wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
            wp.Append("     <metaData>");
            wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
            wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
            wp.Append("     </metaData>");
            wp.Append("     <data>");
            wp.Append("         <properties>");
            wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
            wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
            wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
            wp.Append("             <property name='Content' type='string'>");
            wp.Append("             <![CDATA[");
            wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
            wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
            wp.Append("                 <script>");
            wp.Append("                     yam.connect.embedFeed({");
            wp.Append("                       container: '#embedded-feed'");
            wp.Append("                             , feedType: 'open-graph'");
            wp.Append("                             , feedId: ''");
            wp.Append("                             , config: {");
            wp.Append("                                  use_sso: " + useSso.ToString().ToLower());
            wp.Append("                                  , header: " + showHeader.ToString().ToLower());
            wp.Append("                                  , footer: " + showFooter.ToString().ToLower());
            wp.Append("                                  , showOpenGraphPreview: false");
            wp.Append("                                  , defaultToCanonical: false");
            wp.Append("                                  , hideNetworkName: false");
            wp.Append("                                  , promptText: 'Start a conversation'");
            if (!string.IsNullOrEmpty(groupId))
            {
                wp.Append("                              , defaultGroupId: '" + groupId + "'"); 
            }
            wp.Append("                             }");
            wp.Append("                             , objectProperties: {"); 
            wp.Append("                               url: '" + url + "'");
            wp.Append("                               , type: 'page'");
            wp.Append("                               , title: '" + postTitle + "'");
            wp.Append("                               , image: '" + postImageUrl + "'");
            wp.Append("                             }");
            wp.Append("                         });");
            wp.Append("                     </script>");
            wp.Append("             ]]>");
            wp.Append("             </property>");
            wp.Append("         </properties>");
            wp.Append("     </data>");
            wp.Append(" </webPart>");
            wp.Append("</webParts>");

            return wp.ToString();
        }

<span data-ttu-id="d6bc3-170">Sehen Sie sich das [Integrieren von Yammer-Feeds für SharePoint-Websites (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) um einen Durchlauf finden Sie unter über der- [Provisioning.Yammer (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).</span><span class="sxs-lookup"><span data-stu-id="d6bc3-170">Watch the [Integrate Yammer feeds to SharePoint sites (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) to see a walk through of the - [Provisioning.Yammer (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).</span></span>

<span data-ttu-id="d6bc3-171">Weitere Informationen zu Yammer einbetten finden Sie im Artikel [Yammer einbetten Feed (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/embed) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-171">For more information about Yammer embed see the [Yammer Embed Feed (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/embed) article.</span></span>

<span data-ttu-id="d6bc3-172">Weitere Informationen zu Yammer-OpenGraph finden Sie im Artikel [Einführung in Open Diagramm & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-172">For more information about Yammer OpenGraph see the [Open Graph Introduction & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) article.</span></span>

<a name="yammer-opengraph-api--yammer-rest-api-with-yammer-sdks"></a><span data-ttu-id="d6bc3-173">Yammer-OpenGraph API & Yammer-REST-API mit Yammer SDKs</span><span class="sxs-lookup"><span data-stu-id="d6bc3-173">Yammer OpenGraph API & Yammer REST API with Yammer SDKs</span></span>
-------------------------------------------------------

<span data-ttu-id="d6bc3-174">Bei dieser Option verwenden Sie die Yammer-OpenGraph API und/oder Yammer-REST-API mit Yammer-SDKs Yammer mit SharePoint integriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-174">In this option you use the Yammer OpenGraph API and/or Yammer REST API with Yammer SDKs to integrate Yammer with SharePoint.</span></span>  <span data-ttu-id="d6bc3-175">Diese APIs kann auch zur Integration von Yammer mit Prozessen außerhalb von Webseiten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-175">These APIs may also be used to integrate Yammer with processes outside of web pages.</span></span>  <span data-ttu-id="d6bc3-176">Beispiele für solche Szenarien sind Dienste und lange ausgeführte Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-176">Examples of such scenarios include services and long running operations.</span></span> 
    
- <span data-ttu-id="d6bc3-177">Diese Option dauert länger implementieren.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-177">This option takes longer to implement.</span></span>
- <span data-ttu-id="d6bc3-178">Dieser Option können Sie steuern, alle Aspekte der Feed und wie angezeigt wird und wie Sie mit ihm interagieren.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-178">This option allows you to control all aspects of the feed and how it appears and how you interact with it.</span></span>

<span data-ttu-id="d6bc3-179">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="d6bc3-179">**When is it a good fit?**</span></span>

- <span data-ttu-id="d6bc3-180">Wenn Sie versuchen, zu Yammer-Feeds in SharePoint-Websites integrieren und die Out-of-Box-Funktionen der Embed Feeds nicht Ihren Anforderungen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-180">When you are trying to integrate Yammer feeds with SharePoint sites and the out-of-the-box capabilities of the embed feeds do not meet your needs.</span></span>
- <span data-ttu-id="d6bc3-181">Wenn Sie versuchen, Yammer-Feeds in Dienste oder lange ausgeführte Vorgänge zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-181">When you are trying to integrate Yammer feeds into services or long running operations.</span></span>

<span data-ttu-id="d6bc3-182">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="d6bc3-182">**Getting Started**</span></span>

<span data-ttu-id="d6bc3-183">Weitere Informationen zu Yammer-OpenGraph finden Sie im Artikel [Einführung in Open Diagramm & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-183">For more information about Yammer OpenGraph see the [Open Graph Introduction & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) article.</span></span>

<span data-ttu-id="d6bc3-184">Yammer-SDKs bieten Sie die Möglichkeit zum Authentifizieren bei Yammer.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-184">Yammer SDKs provide you the ability to authenticate to Yammer.</span></span>  <span data-ttu-id="d6bc3-185">Weitere Informationen zu den SDKs Yammer finden Sie unter den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="d6bc3-185">For more information about the Yammer SDKs see the following articles:</span></span>

- [<span data-ttu-id="d6bc3-186">JavaScript-SDK</span><span class="sxs-lookup"><span data-stu-id="d6bc3-186">JavaScript SDK</span></span>](https://developer.yammer.com/v1.0/docs/js-sdk)
- [<span data-ttu-id="d6bc3-187">Ruby SDK</span><span class="sxs-lookup"><span data-stu-id="d6bc3-187">Ruby SDK</span></span>](https://developer.yammer.com/v1.0/docs/ruby-sdk)
- [<span data-ttu-id="d6bc3-188">Python SDK (engl.)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-188">Python SDK</span></span>](https://developer.yammer.com/v1.0/docs/python-sdk)
- [<span data-ttu-id="d6bc3-189">iOS-SDK</span><span class="sxs-lookup"><span data-stu-id="d6bc3-189">iOS SDK</span></span>](https://developer.yammer.com/v1.0/docs/ios-sdk)
- [<span data-ttu-id="d6bc3-190">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d6bc3-190">.NET SDK</span></span>](https://developer.yammer.com/v1.0/docs/net-sdk)
- [<span data-ttu-id="d6bc3-191">Windows Phone 8 SDK</span><span class="sxs-lookup"><span data-stu-id="d6bc3-191">Windows Phone 8 SDK</span></span>](https://developer.yammer.com/v1.0/docs/windows-phone-8-sdk)

<span data-ttu-id="d6bc3-192">Nachdem Sie bei Yammer über die Yammer-SDKs authentifiziert haben, können Sie die Yammer-REST-APIs aufrufen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-192">After you have authenticated to Yammer via the Yammer SDKs you can call the Yammer REST APIs.</span></span>  

<span data-ttu-id="d6bc3-193">Weitere Informationen zu Yammer-REST-APIs finden Sie im Artikel [REST-API & Rate Grenzwerte (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) .</span><span class="sxs-lookup"><span data-stu-id="d6bc3-193">For more information about Yammer REST APIs see the [REST API & Rate Limits (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) article.</span></span>

<span data-ttu-id="d6bc3-194">**Hinweis Authentifizierung**</span><span class="sxs-lookup"><span data-stu-id="d6bc3-194">**Authentication Note**</span></span>

<span data-ttu-id="d6bc3-195">In einem Szenario, in dem Sie mit den Anmeldeinformationen anmelden, die von der Anmeldeinformationen unterscheiden, die Sie verwenden Sie zum Anmelden an SharePoint mit Ihnen, möglicherweise eine Single-Sign-on-Funktion für Ihre Benutzer entwickeln möchten.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-195">In a scenario where you sign into SharePoint with credentials that differ from the credentials you use to sign into SharePoint with you may wish to develop a single-sign-on capability for your users.</span></span>  <span data-ttu-id="d6bc3-196">Ein Beispiel für ein solches Szenario ist, wenn Sie in SharePoint mit einer Live-ID anmelden und Sie in Yammer mit einem Microsoft persönliche oder Arbeit Konto anmelden müssen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-196">An example of such a scenario is when you sign into SharePoint with a LiveID and you need to sign into Yammer with a Microsoft personal or work account.</span></span>

<span data-ttu-id="d6bc3-197">Zum Implementieren eines Single-Sign-on-Szenarios können Sie steuern, die Benutzer zum Anmelden bei der ersten Yammer, den sie zu einer SharePoint-Seite mit der benutzerdefinierten Komponente Yammer darauf stammen.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-197">To implement a single-sign-on scenario you can direct your users to sign into Yammer the first time they come to a SharePoint page with your custom Yammer component on it.</span></span> <span data-ttu-id="d6bc3-198">Nachdem der Benutzer in Yammer über die Yammer-SDK signiert können Sie die Aktualisierungstoken für den Benutzer in ihrem Benutzerprofil speichern.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-198">After the user signs into Yammer via the Yammer SDK you can store the refresh token for the user in their user profile.</span></span>  <span data-ttu-id="d6bc3-199">Anschließend können Sie bei nachfolgenden Besuchen auf der Seite Abrufen der Aktualisierungstoken aus dem Benutzerprofil und Authentifizierung verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-199">Then, on subsequent visits to the page you can retrieve the refresh token from the user profile and use it to authenticate.</span></span>  <span data-ttu-id="d6bc3-200">Bei diesem Ansatz müssen Ihre Endbenutzer nur zum Anmelden bei Yammer, wenn ihre Aktualisierungstoken abläuft.</span><span class="sxs-lookup"><span data-stu-id="d6bc3-200">With this approach your end users only need to sign into Yammer when their refresh token expires.</span></span>

<a name="related-links"></a><span data-ttu-id="d6bc3-201">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="d6bc3-201">Related links</span></span>
=============
- [<span data-ttu-id="d6bc3-202">Integrieren von Yammer-Feeds für SharePoint-Websites (Office 365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-202">Integrate Yammer feeds to SharePoint sites (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites)
- [<span data-ttu-id="d6bc3-203">Yammer einbetten Feed (Yammer Developer Center)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-203">Yammer Embed Feed (Yammer Developer Center)</span></span>](https://developer.yammer.com/v1.0/docs/embed)
- [<span data-ttu-id="d6bc3-204">Einführung in Open Diagramm & Format (Yammer Developer Center)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-204">Open Graph Introduction & Format (Yammer Developer Center)</span></span>](https://developer.yammer.com/v1.0/docs/open-graph)
- <span data-ttu-id="d6bc3-205">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="d6bc3-205">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="d6bc3-206">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="d6bc3-206">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="d6bc3-207">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="d6bc3-207">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="d6bc3-208">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="d6bc3-208">Related PnP samples</span></span>
===================
- [<span data-ttu-id="d6bc3-209">Provisioning.Yammer (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-209">Provisioning.Yammer (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)
- [<span data-ttu-id="d6bc3-210">OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="d6bc3-210">OfficeDevPnP.Core</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
- <span data-ttu-id="d6bc3-211">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-211">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="d6bc3-212">Gilt für</span><span class="sxs-lookup"><span data-stu-id="d6bc3-212">Applies to</span></span>
==========
- <span data-ttu-id="d6bc3-213">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-213">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="d6bc3-214">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="d6bc3-214">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="d6bc3-215">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="d6bc3-215">SharePoint 2013 on-premises</span></span>
