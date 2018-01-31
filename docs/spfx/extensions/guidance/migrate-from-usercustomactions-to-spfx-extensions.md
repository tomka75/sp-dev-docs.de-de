---
title: 'Lernprogramm: Migrieren von UserCustomAction zu SharePoint-Framework-Erweiterungen'
description: "Migrieren von alten „klassischen“ Anpassungen zum neuen Modell basierend auf SharePoint-Framework-Erweiterungen."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 69e2268b01b0bc42959991d15d7f8d90aaa86b5c
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="migrating-from-usercustomaction-to-sharepoint-framework-extensions"></a><span data-ttu-id="52319-103">Migrieren von UserCustomAction zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="52319-103">Migrating from UserCustomAction to SharePoint Framework Extensions</span></span>

<span data-ttu-id="52319-104">In den letzten Jahren profitierten die meisten auf Office 365 und SharePoint Online aufbauenden Enterprise-Lösungen von den _CustomAction_-Funktionen von SharePoint-Feature-Framework zur Erweiterung der Benutzeroberfläche von Seiten.</span><span class="sxs-lookup"><span data-stu-id="52319-104">During the last few years, most of the enterprise solutions built on top of Office 365 and SharePoint Online leveraged the site _CustomAction_ capability of the SharePoint Feature Framework to extend the UI of pages.</span></span> <span data-ttu-id="52319-105">Innerhalb der modernen Benutzeroberfläche von SharePoint Online stehen die meisten dieser Anpassungen jedoch nicht mehr zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="52319-105">However nowdays, within the new "modern" UI of SharePoint Online, most of those customizations are no more available.</span></span> <span data-ttu-id="52319-106">Mit den neuen SharePoint-Framework-Erweiterungen können Sie jedoch fast die gleichen Funktionen auch in der modernen Benutzeroberfläche bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="52319-106">Luckily, with the new SharePoint Framework Extensions you can provide similar functionality in the "modern" UI.</span></span>

<span data-ttu-id="52319-107">In diesem Lernprogramm erfahren Sie, wie Sie die alten, klassischen Anpassungen zu dem neuen Modell basierend auf SharePoint-Framework-Erweiterungen migrieren können.</span><span class="sxs-lookup"><span data-stu-id="52319-107">In this tutorial you will learn how to migrate from old "classic" customizations to the new model based on SharePoint Framework Extensions.</span></span>

> [!NOTE]
> <span data-ttu-id="52319-108">Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen  finden Sie unter [Übersicht über SharePoint-Framework-Erweiterungen](../overview-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="52319-108">For more information about how to build SharePoint Framework Extensions, see [Overview of SharePoint Framework Extensions](../overview-extensions.md).</span></span>

<span data-ttu-id="52319-109">Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:</span><span class="sxs-lookup"><span data-stu-id="52319-109"> First of all, let's introduce the available options when developing SharePoint Framework Extensions:</span></span>

* <span data-ttu-id="52319-110">**Application Customizer**.</span><span class="sxs-lookup"><span data-stu-id="52319-110">Application customizer</span></span> <span data-ttu-id="52319-111">Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="52319-111">Application Customizer: extend the native "modern" UI of SharePoint Online by adding custom HTML elements and client-side code to pre-defined placeholders of "modern" pages.</span></span> <span data-ttu-id="52319-112">Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.</span><span class="sxs-lookup"><span data-stu-id="52319-112">At the time of this writing, the available placeholders are the header and the footer of every "modern" page.</span></span>
* <span data-ttu-id="52319-113">**Command Set**.</span><span class="sxs-lookup"><span data-stu-id="52319-113">Command set</span></span> <span data-ttu-id="52319-114">Hinzufügen benutzerdefinierter ECB-Menüelemente oder benutzerdefinierter Schaltflächen zur Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="52319-114">Command Set: allow to add custom ECB menu items or custom buttons to the command bar of a list view for a list or a library.</span></span> <span data-ttu-id="52319-115">Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.</span><span class="sxs-lookup"><span data-stu-id="52319-115">You can associate any JavaScript (TypeScript) action to these commands.</span></span>
* <span data-ttu-id="52319-116">**Field Customizer**.</span><span class="sxs-lookup"><span data-stu-id="52319-116">Field Customizer</span></span> <span data-ttu-id="52319-117">Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.</span><span class="sxs-lookup"><span data-stu-id="52319-117">Field Customizer: customize the rendering of a field in a list view using custom HTML elements and client-side code.</span></span>

<span data-ttu-id="52319-118">Die nützlichste Option in diesem Kontext ist die Erweiterung „Application Customizer“.</span><span class="sxs-lookup"><span data-stu-id="52319-118">The most useful option in our context is the Application Customizer extension.</span></span>

<span data-ttu-id="52319-119">Angenommen, Sie verfügen über eine _CustomAction_ in SharePoint Online, damit alle Websiteseiten eine benutzerdefinierte Fußzeile enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-119">Assume that you have a _CustomAction_ in SharePoint Online, in order to have a custom footer in all of the site's pages.</span></span>

<span data-ttu-id="52319-120">Im folgenden Codeausschnitt ist der XML-Code enthalten, der _CustomAction_ mithilfe des SharePoint-Feature-Frameworks definiert.</span><span class="sxs-lookup"><span data-stu-id="52319-120">In the following code snippet you can see the XML code defining that _CustomAction_ using the SharePoint Feature Framework.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="jQueryCDN"
                Title="jQueryCDN"
                Description="Loads jQuery from the public CDN"
                ScriptSrc="https://code.jquery.com/jquery-3.2.1.slim.min.js"
                Location="ScriptLink"
                Sequence="100" />
  <CustomAction Id="spoCustomBar"
                Title="spoCustomBar"
                Description="Loads a script to rendere a custom footer"
                Location="ScriptLink"
                ScriptSrc="SiteAssets/SPOCustomUI.js"
                Sequence="200" />
</Elements>
```

<span data-ttu-id="52319-121">Wie Sie sehen können, definiert die Datei mit den Feature-Elementen einige Elemente vom Typ _CustomAction_, die in den Seiten der Zielwebsite enthalten sind. Diese umfassen die über das öffentliche CDN geladene jQuery und eine benutzerdefinierte JavaScript-Datei, die die benutzerdefinierte Fußzeile rendert.</span><span class="sxs-lookup"><span data-stu-id="52319-121">As you can see, the feature elements file defines a couple of elements of type _CustomAction_ to include in the pages of the target site both jQuery, loaded through the public CDN, and a custom JavaScript file that renders the custom footer.</span></span>

<span data-ttu-id="52319-122">Der Vollständigkeit halber finden Sie den JavaScript-Code, der eine benutzerdefinierte Fußzeile rendert, deren Menüelemente der Einfachheit halber im Code vordefiniert sind.</span><span class="sxs-lookup"><span data-stu-id="52319-122">Moreover and for the sake of completeness, here you can see the JavaScript code that renders a custom footer, whose menu items are pre-defined in code for the sake of simplicity.</span></span>

```JavaScript
var SPOCustomUI = SPOCustomUI || {};

SPOCustomUI.setUpCustomFooter = function () {
    if ($("#SPOCustomFooter").length)
        return;

    var footerContainer = $("<div>");
    footerContainer.attr("id", "SPOCustomFooter");

    footerContainer.append("<ul>");

    $("#s4-workspace").append(footerContainer);
}

SPOCustomUI.addCustomFooterText = function (id, text) {
    if ($("#" + id).length)
        return;

    var customElement = $("<div>");
    customElement.attr("id", id);
    customElement.html(text);

    $("#SPOCustomFooter > ul").before(customElement);

    return customElement;
}

SPOCustomUI.addCustomFooterLink = function (id, text, url) {
    if ($("#" + id).length)
        return;

    var customElement = $("<a>");
    customElement.attr("id", id);
    customElement.attr("href", url);
    customElement.html(text);

    $("#SPOCustomFooter > ul").append($("<li>").append(customElement));

    return customElement;
}

SPOCustomUI.loadCSS = function (url) {
    var head = document.getElementsByTagName('head')[0];
    var style = document.createElement('link');
    style.type = 'text/css';
    style.rel = 'stylesheet';
    style.href = url;
    head.appendChild(style);
}

SPOCustomUI.init = function (whenReadyDoFunc) {
    // avoid executing inside iframes (used by Sharepoint for dialogs)
    if (self !== top) return;

    if (!window.jQuery) {
        // jQuery is needed for Custom Bar to run
        setTimeout(function () { SPOCustomUI.init(whenReadyDoFunc); }, 50);
    } else {
        $(function () {
            SPOCustomUI.setUpCustomFooter();
            whenReadyDoFunc();
        });
    }
}

// The following initializes the custom footer with some fake links
SPOCustomUI.init(function () {

    var currentScriptUrl;

    var currentScript = document.querySelectorAll("script[src*='SPOCustomUI']");
    if (currentScript.length > 0) {
        currentScriptUrl = currentScript[0].src;
    }
    if (currentScriptUrl != undefined) {
        var currentScriptBaseUrl = currentScriptUrl.substring(0, currentScriptUrl.lastIndexOf('/') + 1);
        SPOCustomUI.loadCSS(currentScriptBaseUrl + 'SPOCustomUI.css');
    }

    SPOCustomUI.addCustomFooterText('SPOFooterCopyright', '&copy; 2017, Contoso Inc.');
    SPOCustomUI.addCustomFooterLink('SPOFooterCRMLink', 'CRM', 'CRM.aspx');
    SPOCustomUI.addCustomFooterLink('SPOFooterSearchLink', 'Search Center', 'SearchCenter.aspx');
    SPOCustomUI.addCustomFooterLink('SPOFooterPrivacyLink', 'Privacy Policy', 'Privacy.aspx');
});
```

<br/>

<span data-ttu-id="52319-123">In der folgenden Abbildung ist die Ausgabe der vorherigen benutzerdefinierten Aktion auf der Startseite einer klassischen Website enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-123">In the following figure you can see the output of the previous custom action, within the home page of a classic site.</span></span>

![Die benutzerdefinierte Fußzeile auf einer klassischen Seite](../../../images/user-custom-action-footer-sample.png)

<br/>

<span data-ttu-id="52319-125">Zum Migrieren der vorherigen Lösung zur modernen Benutzeroberfläche führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="52319-125">To migrate the previous solution to the "modern" UI, see the following steps.</span></span>

> [!NOTE]
> <span data-ttu-id="52319-126">Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihre Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="52319-126">Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-a-new-sharepoint-framework-solution"></a><span data-ttu-id="52319-127">Erstellen einer neuen SharePoint-Framework-Lösung</span><span class="sxs-lookup"><span data-stu-id="52319-127">Create a new SharePoint Framework solution</span></span>

1. <span data-ttu-id="52319-128">Öffnen Sie das Befehlszeilentool Ihrer Wahl (z. B. PowerShell, CMD.EXE, Cmder).</span><span class="sxs-lookup"><span data-stu-id="52319-128">Open the command line tool of your choice (for example, PowerShell, CMD.EXE, Cmder).</span></span> <span data-ttu-id="52319-129">Erstellen Sie einen neuen Ordner für die Lösung namens **spfx-react-custom-footer**, und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="52319-129">Open the command line tool of your choice (PowerShell, CMD.EXE, Cmder, etc.), create a new folder for the solution (call it **spfx-ecb-extension**), and create a new SharePoint Framework solution by running the Yeoman generator with the following command:</span></span>

    ```
    yo @microsoft/sharepoint
    ```

2. <span data-ttu-id="52319-130">Geben Sie bei Aufforderung durch das Tool Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="52319-130">When prompted by the tool, provide the following answers:</span></span>

    * <span data-ttu-id="52319-131">Bestätigen Sie den Standardnamen **spfx-react-custom-footer** für Ihre Lösung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="52319-131">Accept the default name (**spfx-ecb-extension**) for your solution, and press Enter.</span></span>
    * <span data-ttu-id="52319-132">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="52319-132">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
    * <span data-ttu-id="52319-133">Wählen Sie **Use the current folder** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="52319-133">Select **Use the current folder**, and select Enter.</span></span>
    * <span data-ttu-id="52319-134">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="52319-134">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
    * <span data-ttu-id="52319-135">Wählen Sie **Extension** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="52319-135">Select **Extension** as the client-side component type to be created.</span></span>
    * <span data-ttu-id="52319-136">Wählen Sie **Application Customizer** als den zu erstellenden Erweiterungstyp aus.</span><span class="sxs-lookup"><span data-stu-id="52319-136">Select **Field Customizer** as the extension type to be created.</span></span>
    * <span data-ttu-id="52319-137">Geben Sie **CustomFooter** als Namen für den Application Customizer an.</span><span class="sxs-lookup"><span data-stu-id="52319-137">Provide "CustomFooter" as the name for your Application Customizer.</span></span>

    ![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-react-custom-footer-yeoman.png)

    <span data-ttu-id="52319-139">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die **CustomFooter**-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="52319-139">At this point, Yeoman will install the required dependencies and scaffold the solution files and folders along with the **CustomFooter** extension.</span></span> <span data-ttu-id="52319-140">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="52319-140">This might take a few minutes.</span></span>

    <span data-ttu-id="52319-141">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="52319-141">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

    ![Gerüsterstellung abgeschlossen](../../../images/spfx-react-custom-footer-yeoman-completed.png)

3. <span data-ttu-id="52319-143">Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:</span><span class="sxs-lookup"><span data-stu-id="52319-143">To lock down the version of the project dependencies, run the following command:</span></span>

    ```
    npm shrinkwrap
    ```

4. <span data-ttu-id="52319-144">Starten Sie Visual Studio Code (oder den Code-Editor Ihrer Wahl), und beginnen Sie, die Lösung zu entwickeln.</span><span class="sxs-lookup"><span data-stu-id="52319-144">Now start Visual Studio Code (or whatever else is the code editor of your choice) and start developing the solution.</span></span> <span data-ttu-id="52319-145">Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.</span><span class="sxs-lookup"><span data-stu-id="52319-145">To start Visual Studio Code, you can execute the following statement.</span></span>

    ```
    code .
    ```

## <a name="define-the-new-ui-elements"></a><span data-ttu-id="52319-146">Definieren der neuen Benutzeroberflächenelemente</span><span class="sxs-lookup"><span data-stu-id="52319-146">Define the new UI elements</span></span>

<span data-ttu-id="52319-147">Die Benutzeroberflächenelemente der benutzerdefinierte Fußzeile werden mit React und einer benutzerdefinierten React-Komponente gerendert.</span><span class="sxs-lookup"><span data-stu-id="52319-147">The UI elements of the custom footer will be rendered using React and a custom React component.</span></span> <span data-ttu-id="52319-148">Sie können die Benutzeroberflächenelemente der Beispielfußzeile mit einer beliebigen Technologie erstellen.</span><span class="sxs-lookup"><span data-stu-id="52319-148">Of course, you can create the UI elements of the sample footer with whatever technology you like.</span></span> <span data-ttu-id="52319-149">In diesem Lernprogramm verwenden wir React, um die Office UI Fabric-Komponenten für React zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="52319-149">In this tutorial, we use React in order to leverage the Office UI Fabric components for React.</span></span>

> [!NOTE]
> <span data-ttu-id="52319-150">Weitere Informationen zur Entwicklung von Lösungen mit React finden Sie unter [Lernprogramm: Einführung in React](https://reactjs.org/tutorial/tutorial.html).</span><span class="sxs-lookup"><span data-stu-id="52319-150">For more information about developing solutions with React, see [Tutorial: Intro to React](https://reactjs.org/tutorial/tutorial.html).</span></span>

1. <span data-ttu-id="52319-151">Öffnen Sie die Datei **CustomFooterApplicationCustomizer.manifest.json** im Ordner **src/extensions/customFooter**.</span><span class="sxs-lookup"><span data-stu-id="52319-151">First of all, open the file **CustomFooterApplicationCustomizer.manifest.json** under the **src/extensions/customFooter** folder.</span></span> <span data-ttu-id="52319-152">Kopieren Sie den Wert der Eigenschaft `id`, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.</span><span class="sxs-lookup"><span data-stu-id="52319-152">Copy the value of the `id` property and store it in a safe place, because you will need it later.</span></span>

2. <span data-ttu-id="52319-153">Öffnen Sie die Datei **CustomFooterApplicationCustomizer.ts** im Ordner **src/extensions/customFooter**, und importieren Sie die Typen `PlaceholderContent` und `PlaceholderName` aus dem Paket `'@microsoft/sp-application-base'`.</span><span class="sxs-lookup"><span data-stu-id="52319-153">Now, open the CustomFooterApplicationCustomizer.ts file, still under the same folder as before and import the types PlaceholderContent and PlaceholderName from the package '@microsoft/sp-application-base'.</span></span> <span data-ttu-id="52319-154">Fügen Sie am Anfang der Datei die Importanweisungen für React hinzu.</span><span class="sxs-lookup"><span data-stu-id="52319-154">Moreover, at the very beginning of the file, add the import directives for React.</span></span>

    <span data-ttu-id="52319-155">Im folgenden Codeauszug ist der Abschnitt für die Importe der Datei **CustomFooterApplicationCustomizer.ts** enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-155">In the following code excerpt you can see the imports section of the **CustomFooterApplicationCustomizer.ts** file.</span></span>

    ``` TypeScript
    import * as React from 'react';
    import * as ReactDom from 'react-dom';

    import { override } from '@microsoft/decorators';
    import { Log } from '@microsoft/sp-core-library';
    import {
    BaseApplicationCustomizer,
    PlaceholderContent,
    PlaceholderName
    } from '@microsoft/sp-application-base';
    import { Dialog } from '@microsoft/sp-dialog';

    import * as strings from 'CustomFooterApplicationCustomizerStrings';
    import CustomFooter from './components/CustomFooter';
    ```

3. <span data-ttu-id="52319-156">Suchen Sie nach der Definition der `CustomFooterApplicationCustomizer`-Klasse, und deklarieren Sie einen neuen privaten Member namens `bottomPlaceholder` des Typs `PlaceholderContent | undefined`.</span><span class="sxs-lookup"><span data-stu-id="52319-156">Locate the definition of the class `CustomFooterApplicationCustomizer` and declare a new private member called _`bottomPlaceholder` of type `PlaceholderContent | undefined`.</span></span> 

4. <span data-ttu-id="52319-157">Rufen Sie nun innerhalb der Außerkraftsetzung der `onInit`-Methode eine benutzerdefinierte Funktion namens `renderPlaceHolders` auf, und definieren Sie diese Funktion.</span><span class="sxs-lookup"><span data-stu-id="52319-157">Now within the override of the `onInit` method invoke a custom function called _`renderPlaceHolders`, and define that function.</span></span>

    <span data-ttu-id="52319-158">Der folgende Codeauszug enthält die Implementierung der benutzerdefinierten Fußzeilenklasse des Application Customizers.</span><span class="sxs-lookup"><span data-stu-id="52319-158">In the following code excerpt you can see the implementation of the custom footer application customizer class.</span></span>

    ``` TypeScript
    /** A Custom Action which can be run during execution of a Client Side Application */
    export default class CustomFooterApplicationCustomizer
    extends BaseApplicationCustomizer<ICustomFooterApplicationCustomizerProperties> {

    // This private member holds a reference to the page's footer
    private _bottomPlaceholder: PlaceholderContent | undefined;

    @override
    public onInit(): Promise<void> {
        Log.info(LOG_SOURCE, `Initialized ${strings.Title}`);

        let message: string = this.properties.testMessage;
        if (!message) {
        message = '(No properties were provided.)';
        }

        // Call render method for rendering the needed html elements
        this._renderPlaceHolders();

        return Promise.resolve();
    }

    private _renderPlaceHolders(): void {

        // Handling the bottom placeholder
        if (!this._bottomPlaceholder) {
        this._bottomPlaceholder =
            this.context.placeholderProvider.tryCreateContent(
            PlaceholderName.Bottom);

        // The extension should not assume that the expected placeholder is available.
        if (!this._bottomPlaceholder) {
            console.error('The expected placeholder (Bottom) was not found.');
            return;
        }

        const element: React.ReactElement<{}> = React.createElement(CustomFooter);
        
        ReactDom.render(element, this._bottomPlaceholder.domElement);
        }
    }
    }
    ```

    <span data-ttu-id="52319-159">Die `renderPlaceHolders`-Methode sucht zunächst nach dem Platzhalter des Typs `Bottom` und zeigt ggf. den Inhalt an.</span><span class="sxs-lookup"><span data-stu-id="52319-159">First of all, the  _`renderPlaceHolders` method searches for the placeholder of type `Bottom` and if any it renders its content.</span></span> <span data-ttu-id="52319-160">Am Ende der `renderPlaceHolders`-Methode erstellt der Code eine neue Instanz der React-Komponente `CustomFooter` und rendert sie im Platzhalter für den unteren Bereich der Seiten (d. h. wo die Fußzeile gerendert werden sollte).</span><span class="sxs-lookup"><span data-stu-id="52319-160">In fact, at the very end of the _`renderPlaceHolders` method the code creates a new instance of a `CustomFooter` React component, and renders it within the placeholder of the pages' bottom (i.e. where the footer should be rendered).</span></span>

    > [!NOTE]
    > <span data-ttu-id="52319-161">Die React-Komponente ersetzt in der modernen Benutzeroberfläche die JavaScript-Datei des klassischen Modells.</span><span class="sxs-lookup"><span data-stu-id="52319-161">The React component will be the replacement, in the "modern" UI for the JavaScript file in the "classic" model.</span></span> <span data-ttu-id="52319-162">Sie können die gesamte Fußzeile mithilfe von reinem JavaScript-Code rendern und den größten Teil des bereits vorhandenen Codes wiederverwenden.</span><span class="sxs-lookup"><span data-stu-id="52319-162">Of course, you can render the entire footer still using pure JavaScript code and reusing most of the code that you already have.</span></span> <span data-ttu-id="52319-163">Es wird jedoch empfohlen, die Implementierung nicht nur im Hinblick auf Technologie, sondern auch im Hinblick auf den Code zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="52319-163">However, it is better to consider to upgrade the implementation not only from a technology perspective, but also from a code perspective.</span></span>

5. <span data-ttu-id="52319-164">Fügen Sie einen neuen Ordner namens **components** im Ordner **src/extensions/customFooter** hinzu.</span><span class="sxs-lookup"><span data-stu-id="52319-164">Add a new folder called components within the **src/extensions/customFooter** folder.</span></span> <span data-ttu-id="52319-165">Erstellen Sie in dem neuen Ordner eine neue Datei, und nennen Sie sie **CustomFooter.tsx**.</span><span class="sxs-lookup"><span data-stu-id="52319-165">Create a new file within the new folder, call it **CustomFooter.tsx**.</span></span>

    <span data-ttu-id="52319-166">Im folgenden Codeauszug ist die Komponentenquelldatei enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-166">In the following code excerpt you can see the component source file.</span></span>

    ```TypeScript
    import * as React from 'react';

    import { CommandButton } from 'office-ui-fabric-react/lib/Button';

    export default class CustomFooter extends React.Component<{}, {}> {

    public render(): React.ReactElement<{}> {

        return (
        <div className={`ms-bgColor-neutralLighter ms-fontColor-white`}>
            <div className={`ms-bgColor-neutralLighter ms-fontColor-white`}>
                <div className={`ms-Grid`}>
                    <div className="ms-Grid-row">
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                            <CommandButton 
                                data-automation="CopyRight"
                                href={`CRM.aspx`}>&copy; 2017, Contoso Inc.</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                        <CommandButton 
                                data-automation="CRM"
                                iconProps={ { iconName: 'People' } }
                                href={`CRM.aspx`}>CRM</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                        <CommandButton 
                                data-automation="SearchCenter"
                                iconProps={ { iconName: 'Search' } }
                                href={`SearchCenter.aspx`}>Search Center</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                            <CommandButton 
                                data-automation="Privacy"
                                iconProps={ { iconName: 'Lock' } }
                                href={`Privacy.aspx`}>Privacy Policy</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm4 ms-md4 ms-lg4">
                        </div>
                    </div>
                </div>
            </div>
        </div>
        );
    }
    }
    ```

    <span data-ttu-id="52319-167">Informationen zum Schreiben einer React-Komponente sind in diesem Dokument nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-167">Teaching you how to write a React component is out of scope for this document.</span></span> <span data-ttu-id="52319-168">Beachten Sie dennoch die `import`-Anweisungen am Anfang, mit denen die Komponente React importiert, sowie die React-Komponente `CommandButton` aus der Office UI Fabric-Komponentenbibliothek.</span><span class="sxs-lookup"><span data-stu-id="52319-168">Nevertheless, notice the `import` statements at the beginning, where the component imports React, and the `CommandButton` React component from the Office UI Fabric components library.</span></span>
    
    <span data-ttu-id="52319-169">In der `render`-Methode der Komponente wird die Ausgabe von `CustomFooter` mit einigen Instanzen der `CommandButton`-Komponente für die Links in der Fußzeile definiert.</span><span class="sxs-lookup"><span data-stu-id="52319-169">Moreover, in the `render` method of the component, it is defined the output of the `CustomFooter` with few instances of the `CommandButton` component for the links in the footer.</span></span> <span data-ttu-id="52319-170">Die HTML-Ausgabe ist in ein Rasterlayout von Office UI Fabric eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="52319-170">All the HTML output is wrapped within a Grid layout of Office UI Fabric.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="52319-171">Weitere Informationen zum Rasterlayout von Office UI Fabric finden Sie unter [Dynamisches Layout](https://developer.microsoft.com/de-DE/fabric#/styles/layout).</span><span class="sxs-lookup"><span data-stu-id="52319-171">For more information about the grid layout of Office UI Fabric, see [Responsive Layout](https://developer.microsoft.com/de-DE/fabric#/styles/layout).</span></span>

    <span data-ttu-id="52319-172">In der folgenden Abbildung ist die resultierende Ausgabe enthalten.</span><span class="sxs-lookup"><span data-stu-id="52319-172">In the following figure you can see the resulting output.</span></span>

    ![Die auf einer modernen Website gerenderte benutzerdefinierte Fußzeile](../../../images/spfx-react-custom-footer-output.png)

## <a name="test-the-solution-in-debug-mode"></a><span data-ttu-id="52319-174">Testen der Lösung im Debugmodus</span><span class="sxs-lookup"><span data-stu-id="52319-174">Test the solution in debug mode</span></span>

1. <span data-ttu-id="52319-175">Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus, um die Lösung zu erstellen und den lokalen Node.js-Server zum Hosten der Lösung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="52319-175">Go back to the console window and run the following command to build the solution and run the local Node.js server to host it.</span></span>

    ```
    gulp serve --nobrowser
    ```

2. <span data-ttu-id="52319-176">Öffnen Sie jetzt Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Seite einer beliebigen „modernen“ Teamwebsite.</span><span class="sxs-lookup"><span data-stu-id="52319-176">Now open your favorite browser and go to a "modern" page of any "modern" team site.</span></span> <span data-ttu-id="52319-177">Hängen Sie jetzt die folgenden Abfragezeichenfolgeparameter an die Seiten-URL an.</span><span class="sxs-lookup"><span data-stu-id="52319-177">Now, append the following querystring parameters to the page's URL.</span></span>

    ```
    ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"82242bbb-f951-4c71-a978-80eb8f35e4c1":{"location":"ClientSideExtension.ApplicationCustomizer"}}
    ```

    <span data-ttu-id="52319-178">Ersetzen Sie in dieser Abfragezeichenfolge die GUID durch den `id`-Wert aus der Datei **CustomFooterApplicationCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="52319-178">In the above querystring, you will have to replace the GUID with the `id` value you saved from the **CustomFooterApplicationCustomizer.manifest.json** file.</span></span> 
    
    <span data-ttu-id="52319-179">Beachten Sie, dass beim Ausführen der Seitenanforderung ein Warnmeldungsfeld „Debugskripts zulassen?“ angezeigt wird, in dem Sie aus Sicherheitsgründen nach der Zustimmung für die Ausführung des Codes von Localhost gefragt werden.</span><span class="sxs-lookup"><span data-stu-id="52319-179">Notice that, when executing the page request, you will be prompted with a warning message box with title "Allow debug scripts?", which asks your consent to run code from localhost, for security reasons.</span></span> <span data-ttu-id="52319-180">Wenn Sie die Lösung lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.</span><span class="sxs-lookup"><span data-stu-id="52319-180">Of course, if you want to locally debug and test the solution, you will have to allow to "Load debug scripts".</span></span>

## <a name="package-and-host-the-solution"></a><span data-ttu-id="52319-181">Packen und Hosten der Lösung</span><span class="sxs-lookup"><span data-stu-id="52319-181">Package and host the solution</span></span>

<span data-ttu-id="52319-182">Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.</span><span class="sxs-lookup"><span data-stu-id="52319-182">If you are happy with the result, you are now ready to package the solution and host it in a real hosting infrastructure.</span></span>
<span data-ttu-id="52319-183">Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature-Framework-Datei deklarieren, um die Erweiterung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="52319-183">Before building the bundle and the package, you need to declare an XML feature framework file to provision the extension.</span></span>

### <a name="review-feature-framework-elements"></a><span data-ttu-id="52319-184">Überprüfen von Feature-Framework-Elementen</span><span class="sxs-lookup"><span data-stu-id="52319-184">Review feature framework elements</span></span>

1. <span data-ttu-id="52319-185">Öffnen Sie im Code-Editor den Unterordner **/sharepoint/assets** der Lösung, und bearbeiten Sie die Datei **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="52319-185">Within the code editor, open the **/sharepoint/assets** sub-folder of the solution folder and edit the **elements.xml** file.</span></span> <span data-ttu-id="52319-186">Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.</span><span class="sxs-lookup"><span data-stu-id="52319-186">In the following code excerpt you can see how the file should look like.</span></span>

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
        <CustomAction
            Title="CustomFooter"
            Location="ClientSideExtension.ApplicationCustomizer"
            ClientSideComponentId="82242bbb-f951-4c71-a978-80eb8f35e4c1">
        </CustomAction>
    </Elements>
    ```

    <span data-ttu-id="52319-187">Wie Sie sehen können, ähnelt sie der SharePoint-Feature-Framework-Datei des klassischen Modells, sie verwendet jedoch das `ClientSideComponentId`-Attribut für den Verweis auf die `id` der benutzerdefinierten Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="52319-187">As you can see, it reminds the SharePoint Feature Framework file that we saw in the "classic" model, but it uses the `ClientSideComponentId` attribute to reference the `id` of the custom extension.</span></span> <span data-ttu-id="52319-188">Sie können auch ein `ClientSideComponentProperties`-Attribut hinzufügen, wenn Sie benutzerdefinierte Einstellungen für die Erweiterung bereitstellen möchten, was in diesem Lernprogramm nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="52319-188">You can also add a `ClientSideComponentProperties` attribute, if you need to provide custom settings to the extension, which is not the case in this tutorial.</span></span>

2. <span data-ttu-id="52319-189">Öffnen Sie die Datei **package-solution.json** im Lösungsordner **/config**.</span><span class="sxs-lookup"><span data-stu-id="52319-189">Now, open the **package-solution.json** file under the **/config** folder of the solution.</span></span> <span data-ttu-id="52319-190">In der Datei können Sie sehen, dass ein Verweis auf die Datei **elements.xml** im Abschnitt `assets` vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="52319-190">Within the file you can see that there is a reference to the **elements.xml** file, within the `assets` section.</span></span>

    ```JSON
    {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
        "name": "spfx-react-custom-footer-client-side-solution",
        "id": "911728a5-7bde-4453-97b2-2eba59277ed3",
        "version": "1.0.0.0",
        "features": [
        {
            "title": "Application Extension - Deployment of custom action.",
            "description": "Deploys a custom action with ClientSideComponentId association",
            "id": "f16a2612-3163-46ad-9664-3d3daac68cff",
            "version": "1.0.0.0",
            "assets": {
            "elementManifests": [
                "elements.xml"
            ]
            }
        }
        ]
    },
    "paths": {
        "zippedPackage": "solution/spfx-react-custom-footer.sppkg"
    }
    }
    ```

### <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="52319-191">Aktivieren des CDN im Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="52319-191">Enable the CDN in your Office 365 tenant</span></span>

<span data-ttu-id="52319-192">Sie müssen die Erweiterung nun in einer Hostingumgebung hosten.</span><span class="sxs-lookup"><span data-stu-id="52319-192">Now you need to host the extension in a hosting environment.</span></span> <span data-ttu-id="52319-193">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="52319-193">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="52319-194">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="52319-194">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="52319-195">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="52319-195">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```powershell
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="52319-196">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="52319-196">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="52319-197">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="52319-197">Enable public CDN in the tenant:</span></span>
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="52319-198">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="52319-198">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="52319-199">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="52319-199">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="52319-p124">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="52319-p124">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="52319-203">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens **CDN**, und fügen Sie ihr einen Ordner namens **customfooter** hinzu.</span><span class="sxs-lookup"><span data-stu-id="52319-203">Create a new document library on your site collection called **CDN** and add a folder named **customfooter** to it.</span></span>
    
7. <span data-ttu-id="52319-204">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="52319-204">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="52319-205">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen **cdn** als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="52319-205">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** acts as a CDN origin.</span></span>
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="52319-206">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="52319-206">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
    <span data-ttu-id="52319-207">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="52319-207">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="52319-208">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie mit dem Bereitstellen der Erweiterung fortfahren, die anschließend im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="52319-208">Final configuration of the origin takes approximately 15 minutes, so we can continue provisioning the extension, which will be hosted from the origin after deployment is completed.</span></span> 

    ![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

    <span data-ttu-id="52319-210">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="52319-210">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="52319-211">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="52319-211">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a><span data-ttu-id="52319-212">Aktualisieren der Lösungseinstellungen und Veröffentlichen im CDN</span><span class="sxs-lookup"><span data-stu-id="52319-212">Update the solution settings and publish it on the CDN</span></span>

<span data-ttu-id="52319-213">Als Nächstes müssen Sie die Lösung aktualisieren, um das gerade erstellte CDN als Hostingumgebung zu verwenden. Sie müssen das Lösungsbundle im CDN veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="52319-213">Now, you need to update the solution in order to use the just created CDN as the hosting enviroment and you will need to publish the solution bundle to the CDN.</span></span> <span data-ttu-id="52319-214">Um diese Aufgabe auszuführen, gehen Sie folgendermaßen vor.</span><span class="sxs-lookup"><span data-stu-id="52319-214">To accomplish this task, just follow the upcoming steps.</span></span>

1. <span data-ttu-id="52319-215">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderlichen URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="52319-215">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="52319-216">Aktualisieren Sie die Datei _write-manifests.json_ (im Ordner _config_) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="52319-216">Update the _write-manifests.json_ file (under the _config_ folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="52319-217">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="52319-217">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="52319-218">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="52319-218">The format of the CDN URL is as follows:</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-react-custom-footer-write-manifest.png)

3. <span data-ttu-id="52319-220">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="52319-220">Save your changes.</span></span>

4. <span data-ttu-id="52319-221">Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="52319-221">Execute the following task to bundle your solution.</span></span> <span data-ttu-id="52319-222">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei **write-manifests.json** angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="52319-222">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="52319-223">Die Ausgabe dieses Befehls finden Sie im Ordner **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="52319-223">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="52319-224">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="52319-224">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="52319-225">Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="52319-225">Execute the following task to package your solution.</span></span> <span data-ttu-id="52319-226">Dieser Befehl erstellt ein Paket namens **spfx-react-custom-footer.sppkg** im Ordner **sharepoint/solution** und bereitet die Ressourcen im Ordner **temp/deploy** für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="52319-226">This command creates an **spfx-react-custom-footer.sppkg** package in the **sharepoint/solution** folder and also prepares the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="52319-227">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche _Bereitstellen_.</span><span class="sxs-lookup"><span data-stu-id="52319-227">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the _Deploy_ button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-react-custom-footer-cdn-address.png)

7. <span data-ttu-id="52319-229">Laden Sie die Dateien im Ordner **temp/deploy** in den Ordner **CDN/customfooter** hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="52319-229">Upload or drag-and-drop the files in the **temp/deploy** folder to the **CDN/customfooter** folder created earlier.</span></span>

### <a name="install-and-run-the-solution"></a><span data-ttu-id="52319-230">Installieren und Ausführen der Lösung</span><span class="sxs-lookup"><span data-stu-id="52319-230">Install and run the solution</span></span>

1. <span data-ttu-id="52319-231">Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="52319-231">Open the browser and navigate to any target "modern" site.</span></span>

2. <span data-ttu-id="52319-232">Navigieren Sie zur Seite **Websiteinhalte**, und wählen Sie **App**, um eine neue App hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="52319-232">Go to the **"Site Contents"** page and select to add a new **App**.</span></span>

3. <span data-ttu-id="52319-233">Wählen Sie zum Installieren einer neuen App **Von Ihrer Organisation** aus, um die im App-Katalog verfügbaren Lösungen zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="52319-233">Select to install a new app "From Your Organization" to browse the solutions available in the AppCatalog.</span></span>

4. <span data-ttu-id="52319-234">Wählen Sie die Lösung mit dem Namen **spfx-react-custom-footer-client-side-solution** aus, und installieren Sie sie auf der Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="52319-234">Select the solution called **"spfx-ecb-extension-client-side-solution"** and istall it on the target site.</span></span>

    ![Hinzufügen einer App-Benutzeroberfläche zum Hinzufügen der Lösung zu einer Website](../../../images/spfx-react-custom-footer-add-app.png)

5. <span data-ttu-id="52319-236">Aktualisieren Sie nach Abschluss der Installation der Anwendung die Seite, oder wechseln Sie zur Startseite der Website.</span><span class="sxs-lookup"><span data-stu-id="52319-236">Once the application installation will be completed, refresh the page or go to the home page of the site.</span></span> <span data-ttu-id="52319-237">Sie können nun die benutzerdefinierte Fußzeile in Aktion erleben.</span><span class="sxs-lookup"><span data-stu-id="52319-237">You should be able to see the custom footer in action.</span></span>

<span data-ttu-id="52319-238">Sie können nun Ihre neue benutzerdefinierte Fußzeile nutzen, die Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="52319-238">Enjoy your new custom footer built using the SharePoint Framework extensions!</span></span>

## <a name="see-also"></a><span data-ttu-id="52319-239">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="52319-239">See also</span></span>

- [<span data-ttu-id="52319-240">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="52319-240">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)
