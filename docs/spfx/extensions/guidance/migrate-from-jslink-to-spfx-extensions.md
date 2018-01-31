---
title: 'Lernprogramm: Migrieren von JSLink zu SharePoint-Framework-Erweiterungen'
description: "Migrieren von alten „klassischen“ Anpassungen zum neuen Modell basierend auf SharePoint-Framework-Erweiterungen."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: a65e90c56a03cdceaad93aef2a318c1903cf1571
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="migrating-from-jslink-to-sharepoint-framework-extensions"></a><span data-ttu-id="a039c-103">Migrieren von JSLink zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="a039c-103">Migrating from JSLink to SharePoint Framework Extensions</span></span>

<span data-ttu-id="a039c-104">Seit Microsoft SharePoint 2013 nutzen die meisten Unternehmenslösungen, die auf Office 365 und SharePoint Online aufbauen, die `JSLink`-Eigenschaft von Feldern und Listenansichten, um das Rendern von Feldern anzupassen.</span><span class="sxs-lookup"><span data-stu-id="a039c-104">Since Microsoft SharePoint version 2013, most of the enterprise solutions built on top of Office 365 and SharePoint Online leveraged the `JSLink` property of fields and list views to customize the rendering of fields.</span></span> <span data-ttu-id="a039c-105">Innerhalb der modernen Benutzeroberfläche von SharePoint Online stehen die meisten dieser Anpassungen jedoch nicht mehr zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="a039c-105">However nowdays, within the new "modern" UI of SharePoint Online, most of those customizations are no more available.</span></span> <span data-ttu-id="a039c-106">Mit den neuen SharePoint-Framework-Erweiterungen können Sie fast die gleichen Funktionen auf der modernen Benutzeroberfläche bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a039c-106">Luckily, with the new SharePoint Framework Extensions you can now provide almost the same functionality in the "modern" UI.</span></span> 

<span data-ttu-id="a039c-107">In diesem Lernprogramm erfahren Sie, wie Sie die alten, klassischen Anpassungen zu dem neuen Modell basierend auf SharePoint-Framework-Erweiterungen migrieren können.</span><span class="sxs-lookup"><span data-stu-id="a039c-107">In this tutorial you will learn how to migrate from old "classic" customizations to the new model based on SharePoint Framework Extensions.</span></span>

> [!NOTE]
> <span data-ttu-id="a039c-108">Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen  finden Sie unter [Übersicht über SharePoint-Framework-Erweiterungen](../overview-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="a039c-108">For more information about how to build SharePoint Framework Extensions, see [Overview of SharePoint Framework Extensions](../overview-extensions.md).</span></span>

<span data-ttu-id="a039c-109">Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:</span><span class="sxs-lookup"><span data-stu-id="a039c-109"> First of all, let's introduce the available options when developing SharePoint Framework Extensions:</span></span>

* <span data-ttu-id="a039c-110">**Application Customizer**.</span><span class="sxs-lookup"><span data-stu-id="a039c-110">Application customizer</span></span> <span data-ttu-id="a039c-111">Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="a039c-111">Application Customizer: extend the native "modern" UI of SharePoint Online by adding custom HTML elements and client-side code to pre-defined placeholders of "modern" pages.</span></span> <span data-ttu-id="a039c-112">Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.</span><span class="sxs-lookup"><span data-stu-id="a039c-112">At the time of this writing, the available placeholders are the header and the footer of every "modern" page.</span></span>
* <span data-ttu-id="a039c-113">**Command Set**.</span><span class="sxs-lookup"><span data-stu-id="a039c-113">Command set</span></span> <span data-ttu-id="a039c-114">Hinzufügen benutzerdefinierter ECB-Menüelemente oder benutzerdefinierter Schaltflächen zur Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="a039c-114">Command Set: allow to add custom ECB menu items or custom buttons to the command bar of a list view for a list or a library.</span></span> <span data-ttu-id="a039c-115">Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.</span><span class="sxs-lookup"><span data-stu-id="a039c-115">You can associate any JavaScript (TypeScript) action to these commands.</span></span>
* <span data-ttu-id="a039c-116">**Field Customizer**.</span><span class="sxs-lookup"><span data-stu-id="a039c-116">Field Customizer</span></span> <span data-ttu-id="a039c-117">Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.</span><span class="sxs-lookup"><span data-stu-id="a039c-117">Field Customizer: customize the rendering of a field in a list view using custom HTML elements and client-side code.</span></span>

<span data-ttu-id="a039c-118">Die nützlichste Option in diesem Kontext ist die Erweiterung „Field Customizer“.</span><span class="sxs-lookup"><span data-stu-id="a039c-118">The most useful option in our context is the Field Customizer extension.</span></span>

<span data-ttu-id="a039c-119">Nehmen Sie an, dass Sie sich in SharePoint Online befinden und Sie über eine benutzerdefinierte Liste mit einem angepassten Feld mit der Bezeichnung „Color“ verfügen, das den Typ **Choice** hat und die folgenden Werte übernehmen kann: _Red_, _Green_, _Blue_, _Yellow_.</span><span class="sxs-lookup"><span data-stu-id="a039c-119">Assume that you are in SharePoint Online, and you have a custom list with a custom field called "Color", which is of type **Choice** and which can assume the following values: _Red_, _Green_, _Blue_, _Yellow_.</span></span> <span data-ttu-id="a039c-120">Nehmen Sie an, dass Sie einen benutzerdefinierten Wert für die `JSLink`-Eigenschaft des Webparts haben, das die Listenansicht der benutzerdefinierten Liste rendert.</span><span class="sxs-lookup"><span data-stu-id="a039c-120">Then, assume that you have custom value for the `JSLink` property of the list view rendering web part of the custom list.</span></span> 

<span data-ttu-id="a039c-121">Im folgenden Codeausschnitt sehen Sie den JavaScript-Code, der von der `JSLink`-Eigenschaft (**customColorRendering.js**) referenziert wird.</span><span class="sxs-lookup"><span data-stu-id="a039c-121">In the following code snippet you can see the JavaScript code referenced by the `JSLink` property (**customColorRendering.js**).</span></span>

```JavaScript
// Define a namespace for the custom rendering code
var customJSLinkRendering = customJSLinkRendering || {}; 

// Define a function that declare the custom rendering rules for the target list view
customJSLinkRendering.CustomizeFieldRendering = function () {  

    // Define a custom object to configure the rendering template overrides
    var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = 
    { 
        // Declare the custom rendering function for the 'View' of field 'Color'
        'Color': 
        { 
            'View': customJSLinkRendering.RenderColorField 
        } 
    }; 

    // Register the custom rendering template
    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride); 
}; 

// Declare the custom rendering function for the 'View' of field 'Color'
customJSLinkRendering.RenderColorField = function (context)  
{ 
    var colorField = context.CurrentItem.Color; 

    // Declare a local variable to hold the output color
    var color = '';

    // Evaluate the values of the 'Color' field and render it accordingly
    switch (colorField)
    {
        case 'Red':
            color = 'red';
            break;
        case 'Green':
            color = 'green';
            break;
        case 'Blue':
            color = 'blue';
            break;
        case 'Yellow':
            color = 'yellow';
            break;
        default:
            color = 'white';
            break;
    }

    // Render the output for the 'Color' field
    return "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
}; 

// Invoke the custom rendering function
customJSLinkRendering.CustomizeFieldRendering();
```

<br/>

<span data-ttu-id="a039c-122">Im folgenden Screenshot sehen Sie darüber hinaus, wie die `JSLink`-Eigenschaft im Listenansicht-Webpart konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="a039c-122">Moreover, in the following screenshot you can see how the JSLink is configured in the list view web part.</span></span>

![Konfiguration der JSLink-Eigenschaft im Listenansicht-Webpart](../../../images/jslink-field-configuration.png)

<br/>

<span data-ttu-id="a039c-124">Wenn Sie die JavaScript-Datei in die Bibliothek **Site Assets** hochgeladen haben, kann der Wert für die `JSLink`-Eigenschaft `"~site/SiteAssets/customColorRendering.js"` lauten.</span><span class="sxs-lookup"><span data-stu-id="a039c-124">If you uploaded the JavaScript file into the **"Site Assets"** library, the value for the `JSLink` property can be `"~site/SiteAssets/customColorRendering.js"`.</span></span>

<span data-ttu-id="a039c-125">Aus Gründen der Vollständigkeit sehen Sie, wie das benutzerdefinierte Rendern der Liste funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a039c-125">And here, for the sake of completeness, you can see how the custom rendering of the list works.</span></span>

![Benutzerdefiniertes Rendern des Felds „Color“ in der benutzerdefinierten Liste](../../../images/jslink-field-output.png)

<span data-ttu-id="a039c-127">Wie Sie sehen können, rendern die Felder „Color“ auf der Elementebene ein farbiges Feld mit der ausgewählten Farbe.</span><span class="sxs-lookup"><span data-stu-id="a039c-127">As you can see "Color" fields render a colored box filled with the color selected at the item level.</span></span>

> [!NOTE]
> <span data-ttu-id="a039c-128">Um diese Art von Lösung für eine „klassische“ Website bereitstellen zu können, können Sie letztendlich eine PnP-Bereitstellungsvorlage verwenden, die sowohl die Liste mit dem benutzerdefinierten Feld als auch gleichzeitig die `JSLink`-Eigenschaft bereitstellen kann.</span><span class="sxs-lookup"><span data-stu-id="a039c-128">In order to provision this kind of solution in a "classic" site you can eventually use a PnP Provisioning Template, which can provision both the list with the custom field, and the JSLink at once.</span></span>

<span data-ttu-id="a039c-129">Zum Migrieren der vorherigen Lösung zum SharePoint-Framework führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="a039c-129">To migrate the previous solution to the SharePoint Framework, see the following steps.</span></span>

> [!NOTE]
> <span data-ttu-id="a039c-130">Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihre Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="a039c-130">Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-a-new-sharepoint-framework-solution"></a><span data-ttu-id="a039c-131">Erstellen einer neuen SharePoint-Framework-Lösung</span><span class="sxs-lookup"><span data-stu-id="a039c-131">Create a new SharePoint Framework solution</span></span>

1. <span data-ttu-id="a039c-132">Öffnen Sie das Befehlszeilentool Ihrer Wahl (z. B. PowerShell, CMD.EXE, Cmder).</span><span class="sxs-lookup"><span data-stu-id="a039c-132">Open the command line tool of your choice (for example, PowerShell, CMD.EXE, Cmder).</span></span> <span data-ttu-id="a039c-133">Erstellen Sie einen neuen Ordner für die Lösung namens **spfx-custom-field-extension**, und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="a039c-133">Open the command line tool of your choice (PowerShell, CMD.EXE, Cmder, etc.), create a new folder for the solution (call it **spfx-ecb-extension**), and create a new SharePoint Framework solution by running the Yeoman generator with the following command:</span></span>

    ```
    yo @microsoft/sharepoint
    ```

2. <span data-ttu-id="a039c-134">Geben Sie bei Aufforderung durch das Tool Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="a039c-134">When prompted by the tool, provide the following answers:</span></span>
    
    * <span data-ttu-id="a039c-135">Bestätigen Sie den Standardnamen **spfx-custom-field-extension** für Ihre Lösung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a039c-135">Accept the default name (**spfx-ecb-extension**) for your solution, and press Enter.</span></span>
    * <span data-ttu-id="a039c-136">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a039c-136">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
    * <span data-ttu-id="a039c-137">Wählen Sie **Use the current folder** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a039c-137">Select **Use the current folder**, and select Enter.</span></span>
    * <span data-ttu-id="a039c-138">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a039c-138">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
    * <span data-ttu-id="a039c-139">Wählen Sie **Extension** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="a039c-139">Select **Extension** as the client-side component type to be created.</span></span>
    * <span data-ttu-id="a039c-140">Wählen Sie **Field Customizer** als den zu erstellenden Erweiterungstyp aus.</span><span class="sxs-lookup"><span data-stu-id="a039c-140">Select **Field Customizer** as the extension type to be created.</span></span>
    * <span data-ttu-id="a039c-141">Geben Sie **CustomColorField** als Namen für den Field Customizer an.</span><span class="sxs-lookup"><span data-stu-id="a039c-141">Provide "CustomColorField" as the name for your Field Customizer.</span></span>
    * <span data-ttu-id="a039c-142">Wählen Sie aus, dass kein bestimmtes JavaScript-Framework verwendet werden soll, indem Sie die Option **Kein JavaScript-Framework** aktivieren.</span><span class="sxs-lookup"><span data-stu-id="a039c-142">Select to not use any specific JavaScript framework by selecting the **"No JavaScript framework"** option.</span></span>

    ![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-custom-field-extension-yeoman.png)

    <span data-ttu-id="a039c-144">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die **CustomColorField**-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="a039c-144">At this point, Yeoman will install the required dependencies and scaffold the solution files and folders along with the **CustomColorField** extension.</span></span> <span data-ttu-id="a039c-145">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="a039c-145">This might take a few minutes.</span></span>

    <span data-ttu-id="a039c-146">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="a039c-146">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

    ![Gerüsterstellung abgeschlossen](../../../images/spfx-custom-field-extension-yeoman-completed.png)

3. <span data-ttu-id="a039c-148">Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:</span><span class="sxs-lookup"><span data-stu-id="a039c-148">To lock down the version of the project dependencies, run the following command:</span></span>

    ```
    npm shrinkwrap
    ```

4. <span data-ttu-id="a039c-149">Starten Sie Visual Studio Code (oder den Code-Editor Ihrer Wahl), und beginnen Sie, die Lösung zu entwickeln.</span><span class="sxs-lookup"><span data-stu-id="a039c-149">Now start Visual Studio Code (or whatever else is the code editor of your choice) and start developing the solution.</span></span> <span data-ttu-id="a039c-150">Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.</span><span class="sxs-lookup"><span data-stu-id="a039c-150">To start Visual Studio Code, you can execute the following statement.</span></span>

    ```
    code .
    ```

## <a name="define-the-new-field-customizer-with-javascript"></a><span data-ttu-id="a039c-151">Definieren des neuen Field Customizer mit JavaScript</span><span class="sxs-lookup"><span data-stu-id="a039c-151">Define the new Field Customizer with JavaScript</span></span>

<span data-ttu-id="a039c-152">Um das gleiche Verhalten beim Rendern des benutzerdefinierten `JSLink`-Felds zu reproduzieren, müssen Sie die gleiche Logik mit clientseitigem Code innerhalb der neuen SharePoint-Framework-Lösung implementieren.</span><span class="sxs-lookup"><span data-stu-id="a039c-152">In order to reproduce the same behavior of the `JSLink` custom field rendering, you simply need to implement the same logic using client-side code, within the new SharePoint Framework solution.</span></span> <span data-ttu-id="a039c-153">Gehen Sie hierzu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="a039c-153">To accomplish this task, complete the following steps.</span></span>

1. <span data-ttu-id="a039c-154">Öffnen Sie die Datei **CustomColorFieldFieldCustomizer.manifest.json** im Ordner **src/extensions/customColorField**.</span><span class="sxs-lookup"><span data-stu-id="a039c-154">First of all, open the file **CustomColorFieldFieldCustomizer.manifest.json** under the **src/extensions/customColorField** folder.</span></span> <span data-ttu-id="a039c-155">Kopieren Sie den Wert der Eigenschaft `id`, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.</span><span class="sxs-lookup"><span data-stu-id="a039c-155">Copy the value of the `id` property and store it in a safe place, because you will need it later.</span></span>

2. <span data-ttu-id="a039c-156">Öffnen Sie die Datei **CustomColorFieldFieldCustomizer.ts** im Ordner **src/extensions/customColorField**, und bearbeiten Sie den Inhalt entsprechend dem folgenden Codeausschnitt:</span><span class="sxs-lookup"><span data-stu-id="a039c-156">Open the **CustomColorFieldFieldCustomizer.ts** file in the **src/extensions/customColorField** folder, and edit the content according to the following code snippet:</span></span>

    ``` TypeScript
    import { Log } from '@microsoft/sp-core-library';
    import { override } from '@microsoft/decorators';
    import {
    BaseFieldCustomizer,
    IFieldCustomizerCellEventParameters
    } from '@microsoft/sp-listview-extensibility';

    import * as strings from 'CustomColorFieldFieldCustomizerStrings';
    import styles from './CustomColorFieldFieldCustomizer.module.scss';

    /**
    * If your field customizer uses the ClientSideComponentProperties JSON input,
    * it will be deserialized into the BaseExtension.properties object.
    * You can define an interface to describe it.
    */
    export interface ICustomColorFieldFieldCustomizerProperties {
    // This is an example; replace with your own property
    sampleText?: string;
    }

    const LOG_SOURCE: string = 'CustomColorFieldFieldCustomizer';

    export default class CustomColorFieldFieldCustomizer
    extends BaseFieldCustomizer<ICustomColorFieldFieldCustomizerProperties> {

    @override
    public onInit(): Promise<void> {
        // Add your custom initialization to this method.  The framework will wait
        // for the returned promise to resolve before firing any BaseFieldCustomizer events.
        Log.info(LOG_SOURCE, 'Activated CustomColorFieldFieldCustomizer with properties:');
        Log.info(LOG_SOURCE, JSON.stringify(this.properties, undefined, 2));
        Log.info(LOG_SOURCE, `The following string should be equal: "CustomColorFieldFieldCustomizer" and "${strings.Title}"`);
        return Promise.resolve();
    }

    @override
    public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

        var colorField = event.fieldValue; 
        
        // Declare a local variable to hold the output color
        var color = '';

        // Evaluate the values of the 'Color' field and render it accordingly
        switch (colorField)
        {
            case 'Red':
                color = 'red';
                break;
            case 'Green':
                color = 'green';
                break;
            case 'Blue':
                color = 'blue';
                break;
            case 'Yellow':
                color = 'yellow';
                break;
            default:
                color = 'white';
                break;
        }
        
        // Render the output for the 'Color' field
        event.domElement.innerHTML = "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
    }

    @override
    public onDisposeCell(event: IFieldCustomizerCellEventParameters): void {
        // This method should be used to free any resources that were allocated during rendering.
        // For example, if your onRenderCell() called ReactDOM.render(), then you should
        // call ReactDOM.unmountComponentAtNode() here.
        super.onDisposeCell(event);
    }
    }
    ```

    <span data-ttu-id="a039c-157">Wie Sie sehen können, ist der Inhalt der Methode `onRenderCell` fast identisch mit der vorherigen `RenderColorField`-Methode in der `JSLink`-Implementierung.</span><span class="sxs-lookup"><span data-stu-id="a039c-157">As you can see, the content of method `onRenderCell` is almost the same of the previous `RenderColorField` method in the `JSLink` implementation.</span></span> <span data-ttu-id="a039c-158">Die einzigen Unterschiede sind:</span><span class="sxs-lookup"><span data-stu-id="a039c-158">The only differences are:</span></span>

    - <span data-ttu-id="a039c-159">Um den aktuellen Feldwert abzurufen, müssen Sie die `event.fieldValue`-Eigenschaft des Eingabearguments der `onRenderCell`-Methode lesen.</span><span class="sxs-lookup"><span data-stu-id="a039c-159">To retrieve the current field value you need to read the `event.fieldValue` property of the input argument of the `onRenderCell` method.</span></span>
    - <span data-ttu-id="a039c-160">Um den benutzerdefinierten HTML-Code zum Rendern des Felds zurückzugeben, müssen Sie der `innerHTML`-Eigenschaft des `event.domElement`-Objekts einen Wert zuweisen, der den Ausgabe-HTML-Container des Feldrenderings darstellt.</span><span class="sxs-lookup"><span data-stu-id="a039c-160">To return the custom HTML code to render the field, you need to assign a value to the `innerHTML` property of the `event.domElement` object, which represents the output HTML container of the field rendering.</span></span>

    <span data-ttu-id="a039c-161">Abgesehen von diesen geringfügigen Änderungen können Sie fast den gesamten JavaScript-Code wie zuvor verwenden.</span><span class="sxs-lookup"><span data-stu-id="a039c-161">Aside from these small changes, you can reuse almost the same JavaScript code as before.</span></span>

    <span data-ttu-id="a039c-162">In der folgenden Abbildung ist die resultierende Ausgabe enthalten.</span><span class="sxs-lookup"><span data-stu-id="a039c-162">In the following figure you can see the resulting output.</span></span>

    ![Der in einer modernen Liste gerenderte Field Customizer](../../../images/spfx-custom-field-extension-output.png)

## <a name="test-the-solution-in-debug-mode"></a><span data-ttu-id="a039c-164">Testen der Lösung im Debugmodus</span><span class="sxs-lookup"><span data-stu-id="a039c-164">Test the solution in debug mode</span></span>

1. <span data-ttu-id="a039c-165">Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus, um die Lösung zu erstellen und den lokalen Node.js-Server zum Hosten der Lösung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a039c-165">Go back to the console window and run the following command to build the solution and run the local Node.js server to host it.</span></span>

    ```
    gulp serve --nobrowser
    ```

2. <span data-ttu-id="a039c-166">Öffnen Sie Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Liste, die über ein benutzerdefiniertes Feld mit dem Namen **Color** verfügt, und geben Sie **Choice** mit den gleichen Werten wie zuvor ein (Red, Green, Blue, Yellow).</span><span class="sxs-lookup"><span data-stu-id="a039c-166">Now open your favorite browser and go to a "modern" list, which has a custom field with name **"Color"** and type **Choice** with the same value options as before (Red, Green, Blue, Yellow).</span></span> <span data-ttu-id="a039c-167">Sie können letztendlich die Liste verwenden, die Sie in der „klassischen“ Website erstellt haben, und sie einfach in der „modernen“ Benutzerumgebung anzeigen.</span><span class="sxs-lookup"><span data-stu-id="a039c-167">You can eventually use the list you created in the "classic" site, just viewing it with the new "modern" experience.</span></span> <span data-ttu-id="a039c-168">Hängen Sie nun die folgenden Abfragezeichenfolgeparameter an die **AllItems.aspx**-Seiten-URL an.</span><span class="sxs-lookup"><span data-stu-id="a039c-168">Now, append the following querystring parameters to the **AllItems.aspx** page URL.</span></span>

    ```
    ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Color":{"id":"c3070978-d85e-4298-8758-70b5b5933076"}}
    ```

    <span data-ttu-id="a039c-169">In dieser Abfragezeichenfolge müssen Sie die GUID durch den `id`-Wert aus der Datei **CustomColorFieldFieldCustomizer.manifest.json** ersetzen, den Sie zuvor gespeichert oder notiert haben. Der **Color**-Objektname bezieht sich auf das anzupassende Feld.</span><span class="sxs-lookup"><span data-stu-id="a039c-169">In the above querystring, you will have to replace the GUID with the `id` value you saved from the **CustomColorFieldFieldCustomizer.manifest.json** file, and the **"Color"** object name refers to the name of the field to customize.</span></span> <span data-ttu-id="a039c-170">Wenn Sie möchten, können Sie auch ein benutzerdefiniertes Konfigurationsobjekt, das im JSON-Format serialisiert ist, als einen zusätzlichen Parameter für die Field Customizer-Konstruktion bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a039c-170">If you like, you can also provide a custom configuration object, serialized in JSON format, as an additional parameter for the field customizer construction.</span></span>

    <span data-ttu-id="a039c-171">Beachten Sie, dass beim Ausführen der Seitenanforderung ein Warnmeldungsfeld „Debugskripts zulassen?“ angezeigt wird, in dem Sie aus Sicherheitsgründen nach der Zustimmung für die Ausführung des Codes von Localhost gefragt werden.</span><span class="sxs-lookup"><span data-stu-id="a039c-171">Notice that, when executing the page request, you will be prompted with a warning message box with title "Allow debug scripts?", which asks your consent to run code from localhost, for security reasons.</span></span> <span data-ttu-id="a039c-172">Wenn Sie die Lösung lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.</span><span class="sxs-lookup"><span data-stu-id="a039c-172">Of course, if you want to locally debug and test the solution, you will have to allow to "Load debug scripts".</span></span>

## <a name="define-the-new-field-customizer-with-typescript"></a><span data-ttu-id="a039c-173">Definieren des neuen Field Customizer mit TypeScript</span><span class="sxs-lookup"><span data-stu-id="a039c-173">Define the new Field Customizer with TypeScript</span></span>

<span data-ttu-id="a039c-174">Sie können nun den JavaScript-Code durch TypeScript ersetzen, um den vollständig typisierten Ansatz von TypeScript nutzen zu können.</span><span class="sxs-lookup"><span data-stu-id="a039c-174">You are now ready to replace the JavaScript code with TypeScript, in order to benefit of the fully typed approach of TypeScript.</span></span>

1. <span data-ttu-id="a039c-175">Öffnen Sie die Datei **CustomColorFieldFieldCustomizer.module.scss** im Ordner **src/extensions/customColorField**.</span><span class="sxs-lookup"><span data-stu-id="a039c-175">Open the file **CustomColorFieldFieldCustomizer.module.scss** under the **src/extensions/customColorField** folder.</span></span> <span data-ttu-id="a039c-176">Diese Datei, eine Sass CSS, stellt die Formatvorlage der Benutzeroberfläche für den Field Customizer dar.</span><span class="sxs-lookup"><span data-stu-id="a039c-176">This file, which is a Sassy CSS, represents the UI style for the field customizer.</span></span> <span data-ttu-id="a039c-177">Ersetzen Sie den Inhalt der SCSS-Datei durch den folgenden.</span><span class="sxs-lookup"><span data-stu-id="a039c-177">Replace the content of the SCSS file with the following one.</span></span>

    ``` SCSS
    .CustomColorField {
    .cell {
        float: left;
        width: 20px; 
        height: 20px; 
        margin: 5px; 
        border: 1px solid rgba(0,0,0,.2);
    }

    .cellRed {
        background: red;
    }

    .cellGreen {
        background: green;
    }

    .cellBlue {
        background: blue;
    }

    .cellYellow {
        background: yellow;
    }

    .cellWhite {
        background: white;
    }
    }
    ```

2. <span data-ttu-id="a039c-178">Ersetzen Sie die Implementierung der `onRenderCell`-Methode durch den folgenden Codeauszug.</span><span class="sxs-lookup"><span data-stu-id="a039c-178">Replace the implementation of the `onRenderCell` method with the following code excerpt.</span></span>

    ``` TypeScript
    @override
    public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

    // Read the current field value
    let colorField: String = event.fieldValue; 

    // Add the main style to the field container element
    event.domElement.classList.add(styles.CustomColorField);

    // Get a reference to the output HTML
    let fieldHtml: HTMLDivElement = event.domElement.firstChild as HTMLDivElement;

    // Add the standard style
    fieldHtml.classList.add(styles.cell);

    // Add the colored style
    switch(colorField)
    {
        case "Red":
        fieldHtml.classList.add(styles.cellRed);
        break;
        case "Green":
        fieldHtml.classList.add(styles.cellGreen);
        break;
        case "Blue":
        fieldHtml.classList.add(styles.cellBlue);
        break;
        case "Yellow":
        fieldHtml.classList.add(styles.cellYellow);
        break;
        default:
        fieldHtml.classList.add(styles.cellWhite);
        break;
    }
    }
    ```

    <span data-ttu-id="a039c-179">Beachten Sie, dass die neue Methodenimplementierung einen vollständig typisierten Ansatz verwendet und die CSS-Klasse `cell` dem untergeordneten `DIV`-Element des aktuellen Feldelements zusammen mit einer anderen CSS-Klasse zuweist, um die Zielfarbe von `DIV` basierend auf dem derzeit ausgewählten Feldwert zu definieren.</span><span class="sxs-lookup"><span data-stu-id="a039c-179">Notice that the new method implementation uses a fully typed approach, and assigns the `cell` CSS class to the `DIV` element child of the current field element, together with another custom CSS class to define the target color of the `DIV` based on the currently selected value for the field.</span></span>

3. <span data-ttu-id="a039c-180">Führen Sie den Field Customizer noch einmal im Debugmodus aus, und sehen Sie sich die Ergebnisse an.</span><span class="sxs-lookup"><span data-stu-id="a039c-180">Run the Field Customizer one more time in debug mode and view the results.</span></span>

## <a name="package-and-host-the-solution"></a><span data-ttu-id="a039c-181">Packen und Hosten der Lösung</span><span class="sxs-lookup"><span data-stu-id="a039c-181">Package and host the solution</span></span>

<span data-ttu-id="a039c-182">Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.</span><span class="sxs-lookup"><span data-stu-id="a039c-182">If you are happy with the result, you are now ready to package the solution and host it in a real hosting infrastructure.</span></span>
<span data-ttu-id="a039c-183">Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature-Framework-Datei deklarieren, um die Erweiterung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="a039c-183">Before building the bundle and the package, you need to declare an XML feature framework file to provision the extension.</span></span>

### <a name="review-feature-framework-elements"></a><span data-ttu-id="a039c-184">Überprüfen von Feature-Framework-Elementen</span><span class="sxs-lookup"><span data-stu-id="a039c-184">Review feature framework elements</span></span>

1. <span data-ttu-id="a039c-185">Öffnen Sie im Code-Editor den Unterordner **/sharepoint/assets** der Lösung, und bearbeiten Sie die Datei **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="a039c-185">Within the code editor, open the **/sharepoint/assets** sub-folder of the solution folder and edit the **elements.xml** file.</span></span> <span data-ttu-id="a039c-186">Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.</span><span class="sxs-lookup"><span data-stu-id="a039c-186">In the following code excerpt you can see how the file should look like.</span></span>

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
        <Field ID="{40475661-efaf-447a-a220-c992b20ec1c3}"
                Name="SPFxColor"
                DisplayName="Color"
                Title="Color"
                Type="Choice"
                Required="FALSE"
                Group="SPFx Columns"
                ClientSideComponentId="c3070978-d85e-4298-8758-70b5b5933076">
        </Field>
    </Elements>
    ```

    <span data-ttu-id="a039c-187">Wie Sie sehen, ähnelt sie der SharePoint-Feature-Framework-Datei. Sie definiert jedoch ein benutzerdefiniertes `Field`-Element mit dem Feldtyp `Choice`, der das `ClientSideComponentId`-Attribut zum Verweisen auf die `id` des Field Customizer verwendet. Es könnte auch ein `ClientSideComponentProperties`-Attribut vorhanden sein, um die für die Erweiterung erforderlichen benutzerdefinierten Konfigurationseigenschaften zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="a039c-187">As you can see, it reminds a SharePoint Feature Framework file, it defines a custom `Field` element with a field type `Choice`, which uses the `ClientSideComponentId` attribute to reference the `id` of the field customizer, and there could be a `ClientSideComponentProperties` attribute, to configure the custom configuration properties required by the extension.</span></span>

2. <span data-ttu-id="a039c-188">Öffnen Sie die Datei **package-solution.json** im Lösungsordner **/config**.</span><span class="sxs-lookup"><span data-stu-id="a039c-188">Now, open the **package-solution.json** file under the **/config** folder of the solution.</span></span> <span data-ttu-id="a039c-189">In der Datei können Sie sehen, dass ein Verweis auf die Datei **elements.xml** im Abschnitt `assets` vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a039c-189">Within the file you can see that there is a reference to the **elements.xml** file, within the `assets` section.</span></span>

    ```JSON
    {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
        "name": "spfx-custom-field-extension-client-side-solution",
        "id": "ab0fbbf8-01ba-4633-8498-46cfd5652619",
        "version": "1.0.0.0",
        "features": [
        {
            "title": "Application Extension - Deployment of custom action.",
            "description": "Deploys a custom action with ClientSideComponentId association",
            "id": "090dc976-878d-44fe-8f8e-ac603d094aa1",
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
        "zippedPackage": "solution/spfx-custom-field-extension.sppkg"
    }
    }
    ```

### <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="a039c-190">Aktivieren des CDN im Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="a039c-190">Enable the CDN in your Office 365 tenant</span></span>

<span data-ttu-id="a039c-191">Sie müssen die Erweiterung nun in einer Hostingumgebung hosten.</span><span class="sxs-lookup"><span data-stu-id="a039c-191">Now you need to host the extension in a hosting environment.</span></span> <span data-ttu-id="a039c-192">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="a039c-192">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="a039c-193">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="a039c-193">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="a039c-194">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="a039c-194">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```powershell
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="a039c-195">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="a039c-195">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="a039c-196">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="a039c-196">Enable public CDN in the tenant:</span></span>
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="a039c-197">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="a039c-197">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="a039c-198">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="a039c-198">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="a039c-p121">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="a039c-p121">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="a039c-202">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens **CDN**, und fügen Sie ihr einen Ordner namens **customcolorfield** hinzu.</span><span class="sxs-lookup"><span data-stu-id="a039c-202">Create a new document library on your site collection called **CDN** and add a folder named **customcolorfield** to it.</span></span>
    
7. <span data-ttu-id="a039c-203">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="a039c-203">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="a039c-204">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen **cdn** als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="a039c-204">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** acts as a CDN origin.</span></span>
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="a039c-205">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="a039c-205">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
    <span data-ttu-id="a039c-206">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="a039c-206">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="a039c-207">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie mit dem Bereitstellen der Erweiterung fortfahren, die anschließend im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="a039c-207">Final configuration of the origin takes approximately 15 minutes, so we can continue provisioning the extension, which will be hosted from the origin after deployment is completed.</span></span> 

    ![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

    <span data-ttu-id="a039c-209">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a039c-209">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="a039c-210">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="a039c-210">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a><span data-ttu-id="a039c-211">Aktualisieren der Lösungseinstellungen und Veröffentlichen im CDN</span><span class="sxs-lookup"><span data-stu-id="a039c-211">Update the solution settings and publish it on the CDN</span></span>

<span data-ttu-id="a039c-212">Als Nächstes müssen Sie die Lösung aktualisieren, um das gerade erstellte CDN als Hostingumgebung zu verwenden. Sie müssen das Lösungsbundle im CDN veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="a039c-212">Now, you need to update the solution in order to use the just created CDN as the hosting enviroment and you will need to publish the solution bundle to the CDN.</span></span> <span data-ttu-id="a039c-213">Um diese Aufgabe auszuführen, gehen Sie folgendermaßen vor.</span><span class="sxs-lookup"><span data-stu-id="a039c-213">To accomplish this task, just follow the upcoming steps.</span></span>

1. <span data-ttu-id="a039c-214">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderlichen URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a039c-214">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="a039c-215">Aktualisieren Sie die Datei **write-manifests.json** (im Ordner **config**) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="a039c-215">Update the **write-manifests.json** file (under the **config** folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="a039c-216">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="a039c-216">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="a039c-217">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="a039c-217">The format of the CDN URL is as follows:</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-custom-field-extension-manifest.png)

3. <span data-ttu-id="a039c-219">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="a039c-219">Save your changes.</span></span>

4. <span data-ttu-id="a039c-220">Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="a039c-220">Execute the following task to bundle your solution.</span></span> <span data-ttu-id="a039c-221">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei **write-manifests.json** angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="a039c-221">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="a039c-222">Die Ausgabe dieses Befehls finden Sie im Ordner **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="a039c-222">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="a039c-223">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="a039c-223">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="a039c-224">Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="a039c-224">Execute the following task to package your solution.</span></span> <span data-ttu-id="a039c-225">Dieser Befehl erstellt ein Paket namens **spfx-custom-field-extension.sppkg** im Ordner **sharepoint/solution** und bereitet außerdem die Ressourcen im Ordner **temp/deploy** für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="a039c-225">This command creates an **spfx-custom-field-extension.sppkg** package in the **sharepoint/solution** folder and also prepares the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="a039c-226">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="a039c-226">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the **Deploy** button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-custom-field-extension-address.png)

7. <span data-ttu-id="a039c-228">Laden Sie die Dateien im Ordner **temp/deploy** in den Ordner **CDN/customcolorfield** hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="a039c-228">Upload or drag-and-drop the files in the **temp/deploy** folder to the **CDN/customcolorfield** folder created earlier.</span></span>

## <a name="install-and-run-the-solution"></a><span data-ttu-id="a039c-229">Installieren und Ausführen der Lösung</span><span class="sxs-lookup"><span data-stu-id="a039c-229">Install and run the solution</span></span>

1. <span data-ttu-id="a039c-230">Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="a039c-230">Open the browser and navigate to any target "modern" site.</span></span>

2. <span data-ttu-id="a039c-231">Navigieren Sie zur Seite **Websiteinhalte**, und wählen Sie **App**, um eine neue App hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="a039c-231">Go to the **"Site Contents"** page and select to add a new **App**.</span></span>

3. <span data-ttu-id="a039c-232">Wählen Sie zum Installieren einer neuen App **Von Ihrer Organisation** aus, um die im App-Katalog verfügbaren Lösungen zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="a039c-232">Select to install a new app "From Your Organization" to browse the solutions available in the AppCatalog.</span></span>

4. <span data-ttu-id="a039c-233">Wählen Sie die Lösung mit dem Namen **spfx-custom-field-extension-client-side-solution**, und installieren Sie sie auf der Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="a039c-233">Select the solution called **"spfx-ecb-extension-client-side-solution"** and istall it on the target site.</span></span>

    ![Hinzufügen einer App-Benutzeroberfläche zum Hinzufügen der Lösung zu einer Website](../../../images/spfx-custom-field-extension-add-app.png)

5. <span data-ttu-id="a039c-235">Nachdem die Anwendung installiert wurde, erstellen Sie eine neue benutzerdefinierte Liste, bearbeiten Sie die Listeneinstellungen, und fügen Sie eine neue Spalte aus den bereits vorhandenen Websitespalten hinzu.</span><span class="sxs-lookup"><span data-stu-id="a039c-235">Once the application installation will be completed, create a new custom list, edit the list settings, and add a new column from already existing site columns.</span></span> <span data-ttu-id="a039c-236">Wählen Sie die Spaltengruppe **SPFx Columns**, und fügen Sie das Feld **Color** hinzu.</span><span class="sxs-lookup"><span data-stu-id="a039c-236">Select the group of columns called **"SPFx Columns"** and add the **"Color"** field.</span></span>

    ![Der Field Customizer in Aktion](../../../images/spfx-custom-field-extension-add-field.png)

6. <span data-ttu-id="a039c-238">Bearbeiten Sie das gerade hinzugefügte Feld, und konfigurieren Sie einige Farbwerte (z. B. Red, Green, Blue, Yellow). Speichern Sie die Feldeinstellungen anschließend.</span><span class="sxs-lookup"><span data-stu-id="a039c-238">Edit the just added field and configure some color values (like: Red, Green, Blue, Yellow) and save the field settings.</span></span>

7. <span data-ttu-id="a039c-239">Fügen Sie der Liste einige Elemente hinzu, und sehen Sie sich die Ausgabe in der Listenansicht an.</span><span class="sxs-lookup"><span data-stu-id="a039c-239">Add some items to the list and see the output in the list view.</span></span> <span data-ttu-id="a039c-240">Sie sollte in etwa wie im folgenden Screenshot aussehen.</span><span class="sxs-lookup"><span data-stu-id="a039c-240">It should look like the one in the following screenshot.</span></span>

    ![Der Field Customizer in Aktion](../../../images/spfx-custom-field-extension-final-output.png)

<span data-ttu-id="a039c-242">Sie können nun den Field Customizer nutzen, den Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a039c-242">Enjoy your new Field Customizer built using the SharePoint Framework extensions!</span></span>

## <a name="see-also"></a><span data-ttu-id="a039c-243">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a039c-243">See also</span></span>

- [<span data-ttu-id="a039c-244">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="a039c-244">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)
