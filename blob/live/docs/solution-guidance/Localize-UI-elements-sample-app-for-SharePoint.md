---
title: "Lokalisieren von UI-Elemente Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 2bf8abc77c9cbe3058fba8544400bea1a6b405c7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="localize-ui-elements-sample-add-in-for-sharepoint"></a><span data-ttu-id="2c2d1-102">Lokalisieren von UI-Elemente Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2c2d1-102">Localize UI elements sample add-in for SharePoint</span></span>

<span data-ttu-id="2c2d1-103">Sie können SharePoint-UI-Elemente lokalisieren, mithilfe von JavaScript ersetzen den Textwert der ein UI-Elementwert mit einem übersetzten Text-Wert aus einer Ressource JavaScript-Datei geladen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-103">You can localize SharePoint UI elements by using JavaScript to replace the text value of a UI element value with a translated text value loaded from a JavaScript resource file.</span></span> 

<span data-ttu-id="2c2d1-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2c2d1-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="2c2d1-105">[Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) -Beispiel-add-in zeigt, wie JavaScript verwenden, um der Textwert der SharePoint-UI-Element mit einem Wert übersetzten Text zu ersetzen, die aus einer Ressourcendatei JavaScript wiedergegeben wird.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-105">The [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) sample add-in shows you how to use JavaScript to replace the text value of a SharePoint UI element with a translated text value, which is read from a JavaScript resource file.</span></span> 

> [!NOTE] 
> <span data-ttu-id="2c2d1-106">Sie sind verantwortlich für die Verwaltung der übersetzten Textwerte in der JavaScript-Ressourcendatei.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-106">You are responsible for maintaining the translated text values in the JavaScript resource file.</span></span> 

<span data-ttu-id="2c2d1-107">In diesem Codebeispiel wird eine vom Anbieter gehosteten add-in, verwendet:</span><span class="sxs-lookup"><span data-stu-id="2c2d1-107">This code sample uses a provider-hosted add-in to:</span></span>

- <span data-ttu-id="2c2d1-108">Lokalisieren einer Websiteseite oder Schnellstartleiste Link Titel mit bestimmten Textwerten.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-108">Localize a site page or Quick Launch link title with specific text values.</span></span>
    
- <span data-ttu-id="2c2d1-109">Beibehalten Sie einer Websiteseite oder Schnellstartleiste Link Titel in eine primäre Sprache und Bereitstellen Sie übersetzte Versionen der Websiteseite und Schnellstartleiste Link Titel in einer anderen Sprache zur Laufzeit.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-109">Preserve a site page or Quick Launch link title in a primary language, and provide translated versions of the site page and Quick Launch link title in another language at run time.</span></span>
    
- <span data-ttu-id="2c2d1-110">Verwenden von JavaScript-Ressourcendateien für die Lokalisierung von Client Side.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-110">Use JavaScript resource files for client side localization.</span></span>
    
- <span data-ttu-id="2c2d1-111">Verknüpfen Sie eine JavaScript-Datei mit einer SharePoint-Website mithilfe einer benutzerdefinierten Aktion.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-111">Link a JavaScript file to a SharePoint site using a custom action.</span></span>
    
- <span data-ttu-id="2c2d1-112">Überprüfen Sie die Benutzeroberflächenkultur der Website, und Laden Sie kulturspezifische Textwerte aus einer JavaScript-Ressourcendatei.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-112">Check the UI culture of the site and then load culture-specific text values from a JavaScript resource file.</span></span>
    
- <span data-ttu-id="2c2d1-113">Überschreiben Sie Websiteseite und Schnellstartleiste Link Titel mit kulturspezifische Textwerte jQuery verwenden.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-113">Overwrite site page and Quick Launch link titles with culture-specific text values using jQuery.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2c2d1-114">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="2c2d1-114">Before you begin</span></span>
<span data-ttu-id="2c2d1-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="2c2d1-115"></span></span>

<span data-ttu-id="2c2d1-116">Laden Sie Sie zuerst [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-116">To get started, download the  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="2c2d1-117">Konfigurieren Sie bevor Sie dieses Codebeispiel ausführen die Language-Einstellungen auf Ihrer Website, und die Anzeigesprache auf der Profilseite des Benutzers festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-117">Before you run this code sample, configure the language settings on your site, and set the display language on your user's profile page.</span></span>

### <a name="to-configure-the-language-settings-on-your-site"></a><span data-ttu-id="2c2d1-118">So konfigurieren Sie die spracheinstellungen auf Ihrer Website</span><span class="sxs-lookup"><span data-stu-id="2c2d1-118">To configure the language settings on your site</span></span>

1. <span data-ttu-id="2c2d1-119">Wählen Sie auf der Teamwebsite **Einstellungen** > **websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-119">On your team site, choose  **Settings** > **Site settings**.</span></span>
    
2. <span data-ttu-id="2c2d1-120">Wählen Sie in der **Die Verwaltung von** **spracheinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-120">In  **Site Administration**, choose  **Language settings**.</span></span>
    
3. <span data-ttu-id="2c2d1-121">Wählen Sie auf der Seite **Spracheinstellungen** im **alternative Sprache(n)**, die alternativen Sprachen, die Ihre Website unterstützt werden soll.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-121">On the  **Language Settings** page, in **Alternate language(s)**, choose the alternate languages your site should support.</span></span> <span data-ttu-id="2c2d1-122">Wählen Sie beispielsweise **Französisch** und **Finnisch**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-122">For example, choose  **French** and **Finnish**, as shown in Figure 1.</span></span>
    
4. <span data-ttu-id="2c2d1-123">Wählen Sie  **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-123">Choose  **OK**.</span></span>

### <a name="to-set-the-display-language-on-your-users-profile-page"></a><span data-ttu-id="2c2d1-124">So legen Sie die Anzeigesprache auf der Profilseite des Benutzers fest</span><span class="sxs-lookup"><span data-stu-id="2c2d1-124">To set the display language on your user's profile page</span></span>

1. <span data-ttu-id="2c2d1-125">Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich,** wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-125">At the top of your Office 365 site, choose your profile picture, and then choose  **About me,** as shown in Figure 2.</span></span>
    
2. <span data-ttu-id="2c2d1-126">Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-126">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="2c2d1-127">Wählen Sie den drei Punkten (...) für zusätzliche Optionen, und wählen Sie dann **Sprache und Region**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-127">Choose the ellipsis (...) for additional options, and then choose  **Language and Region**.</span></span>
    
4. <span data-ttu-id="2c2d1-128">**Meine Anzeigesprachen**wählen Sie eine neue Sprache in der Dropdownliste **Wählen Sie eine neue Sprache aus** , und wählen Sie dann **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-128">In  **My Display Languages**, choose a new language in the  **Pick a new language** dropdown, then choose **Add**.</span></span> <span data-ttu-id="2c2d1-129">Wählen Sie beispielsweise Französisch und Finnisch, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-129">For example, choose French and Finnish, as shown in Figure 3.</span></span> <span data-ttu-id="2c2d1-130">Möglicherweise müssen Sie die gewünschte Sprache nach oben oder unten verschieben, indem Sie auf den Pfeil nach oben und nach unten weisenden Pfeil.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-130">You might need to move your preferred language up or down by choosing the up and down arrows.</span></span>
    
5. <span data-ttu-id="2c2d1-131">Wählen Sie **Speichern und schließen**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-131">Choose  **Save all and close**.</span></span>

> [!NOTE] 
> <span data-ttu-id="2c2d1-132">Es kann für Ihre Website, um die ausgewählten Sprache(n) Rendern ein paar Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-132">It might take a few minutes for your site to render in the selected language(s).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2c2d1-133">Das CSOM ist mit neuen Features in regelmäßigen Abständen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-133">The CSOM is periodically updated with new features.</span></span> <span data-ttu-id="2c2d1-134">Wenn das CSOM neue Features zum Aktualisieren der Websiteseite oder Schnellstartleiste Link Titel bereitstellt, wird empfohlen, dass Sie die neuen Features in der CSOM nicht die hier beschriebenen Optionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-134">If the CSOM provides new features to update site page or Quick Launch link titles, we recommend that you use the new features in the CSOM instead of the options discussed here.</span></span>

<span data-ttu-id="2c2d1-135">**Abbildung 1. Festlegen der Sprache für eine Website**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-135">**Figure 1. Setting the language for a site**</span></span>

![Screenshot der Seite Spracheinstellungen der Websiteeinstellungen](media/0265dd57-cf25-4879-a6df-68072ffa5270.png)

<span data-ttu-id="2c2d1-137">**Abbildung 2. Navigieren zu Profilseite des Benutzers über mich auswählen**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-137">**Figure 2. Navigating to a user's profile page by choosing About me**</span></span>

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben](media/e3971203-7011-40ad-ab1b-341af2df28fc.png)

<span data-ttu-id="2c2d1-139">**Abbildung 3. Ändern eines Benutzers anzeigen Sprachoptionen auf der Profilseite des Benutzers**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-139">**Figure 3. Changing a user's display language settings on the user's profile page**</span></span>

![Screenshot der Seite Details bearbeiten im Abschnitt Sprache und Region](media/ff41b24e-42eb-48ca-83cd-00d88ef753bd.png)

<span data-ttu-id="2c2d1-141">Bevor Sie dieses Codebeispiel [Szenario 2](#bk_Scenario2) ausführen, führen Sie die folgenden Aufgaben aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-141">Before you run  [Scenario 2](#bk_Scenario2) of this code sample, complete the following tasks.</span></span>

### <a name="to-create-a-quick-launch-link"></a><span data-ttu-id="2c2d1-142">Erstellen Sie eine Verknüpfung zur Schnellstartleiste</span><span class="sxs-lookup"><span data-stu-id="2c2d1-142">To create a Quick Launch link</span></span>

1. <span data-ttu-id="2c2d1-143">Wählen Sie auf der Hostwebsite **LINKS bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-143">On the host web, choose  **EDIT LINKS**.</span></span>
    
2. <span data-ttu-id="2c2d1-144">Wählen Sie die **Verknüpfung**, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-144">Choose  **link**, as shown in Figure 4.</span></span>
    
3. <span data-ttu-id="2c2d1-145">Geben Sie in **den anzuzeigenden Text** **Meine Websitedesign Eintrag**aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-145">In  **Text to display**, enter  **My quicklaunch entry**.</span></span>
    
4. <span data-ttu-id="2c2d1-146">Geben Sie im Feld **Adresse**die URL einer Website ein.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-146">In  **Address**, enter the URL of a website.</span></span>
    
5. <span data-ttu-id="2c2d1-147">Wählen Sie **OK** > **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-147">Choose  **OK** > **Save**.</span></span>

<span data-ttu-id="2c2d1-148">**Abbildung 4. Hinzufügen eines Links zur Schnellstartleiste**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-148">**Figure 4. Adding a link to the Quick Launch**</span></span>

![Screenshot der Seite Hyperlinks bearbeiten mit Link hervorgehoben](media/fcb28647-1576-4e86-8ca7-15f3ce8d85fb.png)

### <a name="to-create-a-site-page"></a><span data-ttu-id="2c2d1-150">Erstellen Sie eine Websiteseite</span><span class="sxs-lookup"><span data-stu-id="2c2d1-150">To create a site page</span></span>

1. <span data-ttu-id="2c2d1-151">Wählen Sie auf der Hostwebsite **Websiteinhalte** > **Websiteseiten** > **neue**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-151">On the host web, choose  **Site Contents** > **Site Pages** > **new**.</span></span>
    
2. <span data-ttu-id="2c2d1-152">Geben Sie in **Name der neuen Seite** **Hello SharePoint**aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-152">In  **New page name,** enter **Hello SharePoint**.</span></span>
    
3. <span data-ttu-id="2c2d1-153">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-153">Choose  **Create**.</span></span>
    
4. <span data-ttu-id="2c2d1-154">Geben Sie im Textkörper der Seite **Testseite** .</span><span class="sxs-lookup"><span data-stu-id="2c2d1-154">Enter  **Test page** in the body of the page.</span></span>
    
5. <span data-ttu-id="2c2d1-155">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-155">Choose  **Save**.</span></span>

## <a name="using-the-corejavascriptcustomization-sample-app"></a><span data-ttu-id="2c2d1-156">Verwenden die Core.JavaScriptCustomization Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="2c2d1-156">Using the Core.JavaScriptCustomization sample app</span></span>
<span data-ttu-id="2c2d1-157"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="2c2d1-157"></span></span>

<span data-ttu-id="2c2d1-158">Wenn Sie dieses Codebeispiel ausführen, wird eine vom Anbieter gehostete Anwendung angezeigt, wie in Abbildung 5 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-158">When you run this code sample, a provider-hosted application appears, as shown in Figure 5.</span></span> <span data-ttu-id="2c2d1-159">Dieser Artikel beschreibt Szenario 1 und 2 Szenario, da Sie die Techniken, die in Szenario 1 und 2 Szenario verwenden könnten, um lokalisierte Versionen der Websiteseite und Schnellstartleiste Link Titel bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-159">This article describes Scenario 1 and Scenario 2 because you might use the techniques in Scenario 1 and Scenario 2 to provide localized versions of your site page and Quick Launch link titles.</span></span> 

<span data-ttu-id="2c2d1-160">**Abbildung 5. Startseite der app Core.JavaScriptCustomization**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-160">**Figure 5. Start page of the Core.JavaScriptCustomization app**</span></span>

![Screenshot, der zeigt der Startseite der app Core.JavaScriptCustomization](media/133a6c15-7b96-4418-b795-a7bdab63ead4.png)
### <a name="scenario-1"></a><span data-ttu-id="2c2d1-162">Szenario 1</span><span class="sxs-lookup"><span data-stu-id="2c2d1-162">Scenario 1</span></span>

<span data-ttu-id="2c2d1-163">Szenario 1 zeigt, wie Sie einen Verweis auf eine JavaScript-Datei in einer SharePoint-Website mithilfe einer benutzerdefinierten Aktion hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-163">Scenario 1 shows how to add a reference to a JavaScript file on a SharePoint site using a custom action.</span></span> <span data-ttu-id="2c2d1-164">Auswahl der Schaltfläche **einlegen Anpassung** Ruft die **BtnSubmit_Click** -Methode im scenario1.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-164">Choosing the  **Inject customization** button calls the **btnSubmit_Click** method in scenario1.aspx.cs.</span></span> <span data-ttu-id="2c2d1-165">Die **BtnSubmit_Click** -Methode ruft **AddJsLink** um JavaScript-Dateien mit einer benutzerdefinierten Aktion auf dem hostweb Verweise hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-165">The **btnSubmit_Click** method calls **AddJsLink** to add references to JavaScript files using a custom action on the host web.</span></span>

<span data-ttu-id="2c2d1-166">Abbildung 6 zeigt die Startseite für Szenario 1.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-166">Figure 6 shows the start page for Scenario 1.</span></span>

<span data-ttu-id="2c2d1-167">**Abbildung 6. Szenario 1-Startseite**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-167">**Figure 6. Scenario 1 start page**</span></span>

![Screenshot der Startseite für Szenario 1](media/16972165-5f94-497f-b58c-0e1075d9616a.png)

<span data-ttu-id="2c2d1-169">Die **AddJSLink** -Methode ist Teil der Datei JavaScriptExtensions.cs in **OfficeDevPnP.Core**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-169">The  **AddJSLink** method is part of the JavaScriptExtensions.cs file in **OfficeDevPnP.Core**.</span></span>  <span data-ttu-id="2c2d1-170">**AddJSLink** erfordert, dass eine Zeichenfolge zur Darstellung des Bezeichners der benutzerdefinierten Aktion zugewiesen bereit, und eine Zeichenfolge mit einer durch Semikolons getrennte Liste der URLs auf die JavaScript-Dateien, die Sie mit der Hostwebsite hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-170">**AddJSLink** requires that you supply a string representing the identifier to assign to the custom action, and a string containing a semicolon delimited list of URLs to the JavaScript files that you want to add to the host web.</span></span> <span data-ttu-id="2c2d1-171">Beachten Sie, dass dieses Codebeispiel einen Verweis auf Scripts\scenario1.js, fügt die eine Meldung in der Statusleiste mit der Hostwebsite hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-171">Note that this code sample adds a reference to Scripts\scenario1.js, which adds a status bar message to the host web.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="2c2d1-172">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-172">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
protected void btnSubmit_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var cc = spContext.CreateUserClientContextForSPHost())
            {
                cc.Web.AddJsLink(Utilities.Scenario1Key, Utilities.BuildScenarioJavaScriptUrl(Utilities.Scenario1Key, this.Request));
            }
        }
```
   
> [!NOTE] 
> <span data-ttu-id="2c2d1-173">SharePoint 2013 verwendet minimale Downloadstrategie, um die Datenmenge zu reduzieren Browser heruntergeladen wird, wenn Benutzer zwischen den Seiten auf einer SharePoint-Website navigieren.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-173">SharePoint 2013 uses Minimal Download Strategy to reduce the amount of data the browser downloads when users navigate between pages on a SharePoint site.</span></span> <span data-ttu-id="2c2d1-174">Weitere Informationen finden Sie unter [Übersicht über die minimale Downloadstrategie](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c2d1-174">For more information, see  [Minimal Download Strategy overview](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx).</span></span> <span data-ttu-id="2c2d1-175">In scenario1.js stellt der folgende Code, und zwar unabhängig davon, ob minimale Downloadstrategie auf Ihrer SharePoint-Website verwendet wird, die **RemoteManager_Inject** -Methode immer aufgerufen wird, um den JavaScript-Code zum Hinzufügen von Meldung in der Statuszeile mit der Hostwebsite ausführen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-175">In scenario1.js, the following code ensures that whether or not Minimal Download Strategy is used on your SharePoint site, the  **RemoteManager_Inject** method is always called to run the JavaScript code to add the status bar message to the host web.</span></span>

```
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible.
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS scenario
} else {
    RemoteManager_Inject();
}
```

> [!NOTE] 
> <span data-ttu-id="2c2d1-176">Einige JavaScript-Dateien möglicherweise hängen von anderen JavaScript-Dateien geladen zuerst sein, bevor sie ausgeführt und erfolgreich abgeschlossen werden können.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-176">Some JavaScript files may depend on other JavaScript files to be loaded first, before they can run and complete successfully.</span></span> <span data-ttu-id="2c2d1-177">Das folgende Codekonstrukt aus **RemoteManager_Inject** verwendet die **LoadScript** -Funktion in scenario1.js erste Laden von jQuery, und gehen Sie den verbleibenden JavaScript-Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-177">The following code construct from  **RemoteManager_Inject** uses the **loadScript** function in scenario1.js to first load jQuery, then continue running the remaining JavaScript code.</span></span>

```
var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery first, then continue running the rest of the code.
    loadScript(jQuery, function () {
     // Add additional JavaScript code here to complete your task. 
});
```

<span data-ttu-id="2c2d1-178">Wählen Sie **zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-178">Choose  **Back to Site**.</span></span> <span data-ttu-id="2c2d1-179">Wie in Abbildung 7 dargestellt, die Hostwebsite jetzt eine Meldung angezeigt, Status Leiste, die von scenario1.js hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-179">As shown in Figure 7, the host web now displays a status bar message that was added by scenario1.js.</span></span>

<span data-ttu-id="2c2d1-180">**Abbildung 7. Meldung in der Statusleiste für eine Teamwebsite mithilfe von JavaScript hinzugefügt**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-180">**Figure 7. Status bar message added to a team site using JavaScript**</span></span>

![Screenshot der Meldung in der Statuszeile mithilfe von JavaScript zu einer Teamwebsite hinzugefügt](media/c5d6fb6d-f05f-49aa-a3c5-af1240ee9135.png)

### <a name="scenario-2"></a><span data-ttu-id="2c2d1-182">Szenario 2</span><span class="sxs-lookup"><span data-stu-id="2c2d1-182">Scenario 2</span></span>
<span data-ttu-id="2c2d1-183"><a name="bk_Scenario2"> </a></span><span class="sxs-lookup"><span data-stu-id="2c2d1-183"></span></span>

<span data-ttu-id="2c2d1-184">Szenario 2 mithilfe das in Szenario 1 beschriebenen Verfahren Benutzeroberflächentext mit übersetzten Text aus einer Ressourcendatei JavaScript lesen ersetzt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-184">Scenario 2 uses the technique described in Scenario 1 to replace UI text with translated text read from a JavaScript resource file.</span></span> <span data-ttu-id="2c2d1-185">Szenario 2 ersetzt die Schnellstartleiste Link Titel ( **Meine Websitedesign Eintrag**) und Website Seite Titel ( **Hello SharePoint**), die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-185">Scenario 2 replaces the Quick Launch link title ( **My quicklaunch entry**) and site page title ( **Hello SharePoint**) that you created earlier.</span></span> <span data-ttu-id="2c2d1-186">Szenario 2 Fügt eine JavaScript-Datei, welche Lesevorgänge Textwerte von Variablen in kulturspezifische JavaScript-Ressourcendateien übersetzt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-186">Scenario 2 attaches a JavaScript file which reads translated text values from variables in culture-specific JavaScript resource files.</span></span> <span data-ttu-id="2c2d1-187">Szenario 2 aktualisiert anschließend die Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-187">Scenario 2 then updates the UI.</span></span> <span data-ttu-id="2c2d1-188">Abbildung 8 zeigt die Startseite für Szenario 2 an.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-188">Figure 8 shows the start page for Scenario 2.</span></span>

<span data-ttu-id="2c2d1-189">**Abbildung 8. Szenario 2-Startseite**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-189">**Figure 8. Scenario 2 start page**</span></span>

![Screenshot der Startseite für Szenario 2](media/c706060b-e77d-4ae6-99c4-43dee80ff7d3.png)

<span data-ttu-id="2c2d1-191">Wie in Abbildung 8 gezeigt, betrifft **einlegen Anpassung** auswählen die folgenden Änderungen der Website:</span><span class="sxs-lookup"><span data-stu-id="2c2d1-191">As shown in Figure 8, choosing  **Inject customization** applies the following changes to the site:</span></span>

- <span data-ttu-id="2c2d1-192">**Meine Websitedesign Eintrag** Schnellstartleiste Link Titel wird auf **Contoso-Link**geändert.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-192">The Quick Launch link title  **My quicklaunch entry** is changed to **Contoso link**.</span></span>
    
- <span data-ttu-id="2c2d1-193">Den Titel der Seite **Hello SharePoint** -Website wird zur **Seite "Contoso"**geändert.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-193">The  **Hello SharePoint** site page title is changed to **Contoso page**.</span></span>

<span data-ttu-id="2c2d1-194">**Abbildung 9. Szenario 2 Anpassungen**</span><span class="sxs-lookup"><span data-stu-id="2c2d1-194">**Figure 9. Scenario 2 customizations**</span></span>

![Szenario 2 Anpassungen](media/47e8ec40-d291-496f-8677-01eb46441df2.png)
    
> [!NOTE] 
> <span data-ttu-id="2c2d1-196">Wenn Ihre Werte für die Schnellstartleiste Link Titel und Titel der Website Seite unterscheidet sich von in Abbildung 8 dargestellt die Variablen **quickLauch_Scenario2** und **PageTitle_HelloSharePoint** in Bearbeiten Dateien die JavaScript-Ressource scenario2.en us.js oder scenario2.nl-nl.js.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-196">If your values for the Quick Launch link title and site page title differ from those shown in Figure 8, edit the  **quickLauch_Scenario2** and **pageTitle_HelloSharePoint** variables in the JavaScript resource files scenario2.en-us.js or scenario2.nl-nl.js.</span></span> <span data-ttu-id="2c2d1-197">Führen Sie das Codebeispiel erneut aus.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-197">Then run the code sample again.</span></span> <span data-ttu-id="2c2d1-198">Die Datei scenario2.en us.js speichert Englisch (USA) kulturspezifische Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-198">The scenario2.en-us.js file stores English (US) culture-specific resources.</span></span> <span data-ttu-id="2c2d1-199">Die Datei scenario2.nl nl.js speichert niederländische kulturspezifische Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-199">The scenario2.nl-nl.js file stores Dutch culture-specific resources.</span></span> <span data-ttu-id="2c2d1-200">Wenn Sie dieses Codebeispiel mit einer anderen Sprache testen, sollten Sie eine andere Ressourcendatei für JavaScript in der gleichen Namenskonvention erstellen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-200">If you are testing this code sample using another language, consider creating another JavaScript resource file using the same naming convention.</span></span>

<span data-ttu-id="2c2d1-201">Szenario 1, Ähnlichkeit mit **BtnSubmit_Click** in scenario2.aspx.cs **AddJsLink** , um einen Verweis auf die Datei Scripts\scenario2.js hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-201">Similar to Scenario 1,  **btnSubmit_Click** in scenario2.aspx.cs calls **AddJsLink** to add a reference to the Scripts\scenario2.js file.</span></span> <span data-ttu-id="2c2d1-202">In scenario2.js Ruft die **RemoteManager_Inject** -Funktion die **TranslateQuickLaunch** -Funktion, die folgenden Aufgaben ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="2c2d1-202">In scenario2.js, the **RemoteManager_Inject** function calls the **TranslateQuickLaunch** function, which performs the following tasks:</span></span>

- <span data-ttu-id="2c2d1-203">**_SpPageContextInfo.currentUICultureName**mithilfe der Website Kultur bestimmt.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-203">Determines the site's culture using  **_spPageContextInfo.currentUICultureName**.</span></span>
    
- <span data-ttu-id="2c2d1-204">Lädt JavaScript Ressourcendatei mit der Kultur bestimmte Ressourcen, die die Benutzeroberflächenkultur der Website entsprechen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-204">Loads the JavaScript resource file containing culture specific resources that match the UI culture of the site.</span></span> <span data-ttu-id="2c2d1-205">Beispielsweise, wenn die Website Kultur Englisch (USA) wurde, wird die scenario2.en us.js-Datei geladen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-205">For example, if the site's culture was English (United States), the scenario2.en-us.js file is loaded.</span></span>
    
- <span data-ttu-id="2c2d1-206">Ersetzt **Meine Websitedesign-Eintrag** mit dem Wert der Variablen **quickLauch_Scenario2** aus der JavaScript-Ressourcendatei zu lesen.</span><span class="sxs-lookup"><span data-stu-id="2c2d1-206">Replaces  **my quicklaunch entry** with the value of the **quickLauch_Scenario2** variable read from the JavaScript resource file.</span></span>

```
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";
    
    loadScript(jQuery, function () {
        SP.SOD.executeOrDelayUntilScriptLoaded(function () { TranslateQuickLaunch(); }, 'sp.js');
    });
}

function TranslateQuickLaunch() {
    // Load jQuery and if complete, load the JS resource file.
    var scriptUrl = "";
    var scriptRevision = "";
    // iterate over the scripts loaded on the page to find the scenario2 script. Then use the script URL to dynamically build the URL for the resource file to be loaded.
    $('script').each(function (i, el) {
        if (el.src.toLowerCase().indexOf('scenario2.js') > -1) {
            scriptUrl = el.src;
            scriptRevision = scriptUrl.substring(scriptUrl.indexOf('.js') + 3);
            scriptUrl = scriptUrl.substring(0, scriptUrl.indexOf('.js'));
        }
    })

    var resourcesFile = scriptUrl + "." + _spPageContextInfo.currentUICultureName.toLowerCase() + ".js" + scriptRevision;
    // Load the JS resource file based on the user's language settings.
    loadScript(resourcesFile, function () {

        // General changes that apply to all loaded pages.
        // ----------------------------------------------

        // Update the Quick Launch labels.
        // Note that you can use the jQuery  function to iterate over all elements that match your jQuery selector.
        $("span.ms-navedit-flyoutArrow").each(function () {
            if (this.innerText.toLowerCase().indexOf('my quicklaunch entry') > -1) {
                // Update the label.
                $(this).find('.menu-item-text').text(quickLauch_Scenario2);
                // Update the tooltip.
                $(this).parent().attr("title", quickLauch_Scenario2);
            }
        });

        // Page specific changes require an IsOnPage call.
        // ----------------------------------------------------------

        // Change the title of the "Hello SharePoint" page.
        if (IsOnPage("Hello%20SharePoint.aspx")) {
            $("#DeltaPlaceHolderPageTitleInTitleArea").find("A").each(function () {
                if ($(this).text().toLowerCase().indexOf("hello sharepoint") > -1) {
                    // Update the label.
                    $(this).text(pageTitle_HelloSharePoint);
                    // Update the tooltip.
                    $(this).attr("title", pageTitle_HelloSharePoint);
                }
            });
        }

    });
}
```

## <a name="see-also"></a><span data-ttu-id="2c2d1-207">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2c2d1-207">See also</span></span>
<span data-ttu-id="2c2d1-208"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2c2d1-208"></span></span>

-  [<span data-ttu-id="2c2d1-209">Lokalisierung Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2c2d1-209">Localization solutions for SharePoint 2013 and SharePoint Online</span></span>](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [<span data-ttu-id="2c2d1-210">Core.JavaScriptCustomization</span><span class="sxs-lookup"><span data-stu-id="2c2d1-210">Core.JavaScriptCustomization</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
