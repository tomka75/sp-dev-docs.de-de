---
title: "Lernprogramm: Migrieren vom Edit Control Block-Menüelement (ECB) zur SharePoint-Framework-Erweiterung"
description: "Migrieren von alten „klassischen“ Anpassungen zum neuen Modell basierend auf SharePoint-Framework-Erweiterungen."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 6c790e47b826193029395ef9ca27a8abe2f6b9ca
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="migrating-from-edit-control-block-ecb-menu-item-to-sharepoint-framework-extensions"></a><span data-ttu-id="e8dee-103">Migrieren vom Edit Control Block-Menüelement (ECB) zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="e8dee-103">Migrating from Edit Control Block (ECB) menu item to SharePoint Framework Extensions</span></span>

<span data-ttu-id="e8dee-104">In den letzten Jahren profitierten die meisten auf Office 365 und SharePoint Online aufbauenden Enterprise-Lösungen von den _CustomAction_-Funktionen von SharePoint-Feature-Framework zur Erweiterung der Benutzeroberfläche von Seiten.</span><span class="sxs-lookup"><span data-stu-id="e8dee-104">During the last few years, most of the enterprise solutions built on top of Office 365 and SharePoint Online leveraged the site _CustomAction_ capability of the SharePoint Feature Framework to extend the UI of pages.</span></span> <span data-ttu-id="e8dee-105">Innerhalb der modernen Benutzeroberfläche von SharePoint Online stehen die meisten dieser Anpassungen jedoch nicht mehr zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="e8dee-105">However nowdays, within the new "modern" UI of SharePoint Online, most of those customizations are no more available.</span></span> <span data-ttu-id="e8dee-106">Mit den neuen SharePoint-Framework-Erweiterungen können Sie jedoch fast die gleichen Funktionen auch in der modernen Benutzeroberfläche bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-106">Luckily, with the new SharePoint Framework Extensions you can provide similar functionality in the "modern" UI.</span></span> 

<span data-ttu-id="e8dee-107">In diesem Lernprogramm erfahren Sie, wie Sie die alten, klassischen Anpassungen zu dem neuen Modell basierend auf SharePoint-Framework-Erweiterungen migrieren können.</span><span class="sxs-lookup"><span data-stu-id="e8dee-107">In this tutorial you will learn how to migrate from old "classic" customizations to the new model based on SharePoint Framework Extensions.</span></span>

> [!NOTE]
> <span data-ttu-id="e8dee-108">Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen  finden Sie unter [Übersicht über SharePoint-Framework-Erweiterungen](../overview-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="e8dee-108">For more information about how to build SharePoint Framework Extensions, see [Overview of SharePoint Framework Extensions](../overview-extensions.md).</span></span>

<span data-ttu-id="e8dee-109">Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:</span><span class="sxs-lookup"><span data-stu-id="e8dee-109"> First of all, let's introduce the available options when developing SharePoint Framework Extensions:</span></span>

* <span data-ttu-id="e8dee-110">**Application Customizer**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-110">Application customizer</span></span> <span data-ttu-id="e8dee-111">Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="e8dee-111">Application Customizer: extend the native "modern" UI of SharePoint Online by adding custom HTML elements and client-side code to pre-defined placeholders of "modern" pages.</span></span> <span data-ttu-id="e8dee-112">Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.</span><span class="sxs-lookup"><span data-stu-id="e8dee-112">At the time of this writing, the available placeholders are the header and the footer of every "modern" page.</span></span>
* <span data-ttu-id="e8dee-113">**Command Set**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-113">Command set</span></span> <span data-ttu-id="e8dee-114">Hinzufügen benutzerdefinierter ECB-Menüelemente oder benutzerdefinierter Schaltflächen zur Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="e8dee-114">Command Set: allow to add custom ECB menu items or custom buttons to the command bar of a list view for a list or a library.</span></span> <span data-ttu-id="e8dee-115">Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-115">You can associate any JavaScript (TypeScript) action to these commands.</span></span>
* <span data-ttu-id="e8dee-116">**Field Customizer**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-116">Field Customizer</span></span> <span data-ttu-id="e8dee-117">Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.</span><span class="sxs-lookup"><span data-stu-id="e8dee-117">Field Customizer: customize the rendering of a field in a list view using custom HTML elements and client-side code.</span></span>

<span data-ttu-id="e8dee-118">Die nützlichste Option in diesem Kontext ist die Erweiterung „Command Set“.</span><span class="sxs-lookup"><span data-stu-id="e8dee-118">The most useful option in our context is the Command Set extension.</span></span>

<span data-ttu-id="e8dee-119">Angenommen Sie verfügen über eine _CustomAction_ in SharePoint Online, damit für Dokumente in einer Bibliothek ein benutzerdefiniertes ECB-Menü verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="e8dee-119"> Assume that you have a _CustomAction_ in SharePoint Online, in order to have a custom ECB menu item for documents in a library.</span></span> <span data-ttu-id="e8dee-120">Die Funktion des ECB-Menüelements besteht darin, eine benutzerdefinierte Seite zu öffnen, auf der die Listen-ID und die Listenelement-ID des aktuell ausgewählten Elements in der Abfragezeichenfolge der Zielseite bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="e8dee-120">The scope of the ECB menu item is to open a custom page, providing the list ID and the list item ID of the currently selected item in the querystring of the target page.</span></span>

<span data-ttu-id="e8dee-121">Im folgenden Codeausschnitt ist der XML-Code enthalten, der _CustomAction_ mithilfe des SharePoint-Feature-Frameworks definiert.</span><span class="sxs-lookup"><span data-stu-id="e8dee-121">In the following code snippet you can see the XML code defining that _CustomAction_ using the SharePoint Feature Framework.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="OpenDetailsPageWithItemReference"
                Title="Show Details"
                Description="Opens a new page with further details about the currently selected item"
                Sequence="1001"
                RegistrationType="List"
                RegistrationId="101"                
                Location="EditControlBlock">
    <UrlAction Url="ShowDetails.aspx?ID={ItemId}&amp;List={ListId}" />
  </CustomAction>
</Elements>
```

<span data-ttu-id="e8dee-122">Wie Sie sehen können, definiert die Funktionselementdatei ein Element des Typs _CustomAction_, um ein neues Element am Ort von _EditControlBlock_ (also ECB) für ein beliebiges Dokument in einer beliebigen Bibliothek hinzuzufügen (_ RegistrationType_ ist _List_ und _RegistrationId_ ist _101_).</span><span class="sxs-lookup"><span data-stu-id="e8dee-122">As you can see, the feature elements file defines an element of type _CustomAction_ to add a new item in the _EditControlBlock_ location (i.e. ECB) for any document in any library (_RegistrationType_ is _List_ and _RegistrationId_ is _101_).</span></span>

<span data-ttu-id="e8dee-123">In der folgenden Abbildung sehen Sie die Ausgabe der vorherigen benutzerdefinierten Aktion in der Listenansicht einer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="e8dee-123">In the following figure you can see the output of the previous custom action, within the list view of a library.</span></span>

![Die benutzerdefinierte Fußzeile auf einer klassischen Seite](../../../images/ecb-menu-classic-output.png)

<span data-ttu-id="e8dee-125">Beachten Sie, dass das benutzerdefinierte ECB-Element des SharePoint-Feature-Framework in einer „modernen“ Liste funktioniert.</span><span class="sxs-lookup"><span data-stu-id="e8dee-125">Notice that the SharePoint Feature Framework ECB custom item works in a "modern" list, too.</span></span> <span data-ttu-id="e8dee-126">Tatsächlich funktioniert eine benutzerdefinierte Listenaktion auch in „modernen“ Listen, solange Sie keinen JavaScript-Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="e8dee-126">In fact, as long as you don't use JavaScript code, a list custom action still works in "modern" lists, too.</span></span>

<span data-ttu-id="e8dee-127">Zum Migrieren der vorherigen Lösung zum SharePoint-Framework führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="e8dee-127">To migrate the previous solution to the SharePoint Framework, see the following steps.</span></span>

> [!NOTE]
> <span data-ttu-id="e8dee-128">Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihre Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="e8dee-128">Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment.md).</span></span>

<span data-ttu-id="e8dee-129"><a name="CreateCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="e8dee-129"></span></span>

## <a name="create-a-new-sharepoint-framework-solution"></a><span data-ttu-id="e8dee-130">Erstellen einer neuen SharePoint-Framework-Lösung</span><span class="sxs-lookup"><span data-stu-id="e8dee-130">Create a new SharePoint Framework solution</span></span>

1. <span data-ttu-id="e8dee-131">Öffnen Sie das Befehlszeilentool Ihrer Wahl (z. B. PowerShell, CMD.EXE, Cmder).</span><span class="sxs-lookup"><span data-stu-id="e8dee-131">Open the command-line tool of your choice (for example, PowerShell, CMD.EXE, Cmder).</span></span> <span data-ttu-id="e8dee-132">Erstellen Sie einen neuen Ordner für die Lösung namens **spfx-ecb-extension**, und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="e8dee-132">Open the command line tool of your choice (PowerShell, CMD.EXE, Cmder, etc.), create a new folder for the solution (call it **spfx-ecb-extension**), and create a new SharePoint Framework solution by running the Yeoman generator with the following command:</span></span>

2. <span data-ttu-id="e8dee-133">Geben Sie bei Aufforderung durch das Tool Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="e8dee-133">When prompted by the tool, provide the following answers:</span></span>

  * <span data-ttu-id="e8dee-134">Bestätigen Sie den Standardnamen **spfx-ecb-extension** für Ihre Lösung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="e8dee-134">Accept the default name (**spfx-ecb-extension**) for your solution, and press Enter.</span></span>
  * <span data-ttu-id="e8dee-135">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="e8dee-135">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
  * <span data-ttu-id="e8dee-136">Wählen Sie **Use the current folder** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="e8dee-136">Select **Use the current folder**, and select Enter.</span></span>
  * <span data-ttu-id="e8dee-137">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e8dee-137">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
  * <span data-ttu-id="e8dee-138">Wählen Sie **Extension** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="e8dee-138">Select **Extension** as the client-side component type to be created.</span></span>
  * <span data-ttu-id="e8dee-139">Wählen Sie **ListView Command Set** als den zu erstellenden Typ von Erweiterung aus.</span><span class="sxs-lookup"><span data-stu-id="e8dee-139">Select **ListView Command Set** as the extension type to be created.</span></span>
  * <span data-ttu-id="e8dee-140">Geben Sie **CustomECB** als Namen für Ihr Command Set an.</span><span class="sxs-lookup"><span data-stu-id="e8dee-140">Provide "CustomECB" as the name for your Command Set.</span></span>

  ![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-ecb-extension-yeoman.png)

  <span data-ttu-id="e8dee-142">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die **CustomFooter**-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="e8dee-142">At this point, Yeoman will install the required dependencies and scaffold the solution files and folders along with the **CustomFooter** extension.</span></span> <span data-ttu-id="e8dee-143">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="e8dee-143">This might take a few minutes.</span></span>

  <span data-ttu-id="e8dee-144">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="e8dee-144">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

  ![Gerüsterstellung abgeschlossen](../../../images/spfx-ecb-extension-yeoman-completed.png)

3. <span data-ttu-id="e8dee-146">Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:</span><span class="sxs-lookup"><span data-stu-id="e8dee-146">To lock down the version of the project dependencies, run the following command:</span></span>

  ```
  npm shrinkwrap
  ```

4. <span data-ttu-id="e8dee-147">Starten Sie Visual Studio Code (oder den Code-Editor Ihrer Wahl), und beginnen Sie, die Lösung zu entwickeln.</span><span class="sxs-lookup"><span data-stu-id="e8dee-147">Now start Visual Studio Code (or whatever else is the code editor of your choice) and start developing the solution.</span></span> <span data-ttu-id="e8dee-148">Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-148">To start Visual Studio Code, you can execute the following statement.</span></span>

  ```
  code .
  ```

<span data-ttu-id="e8dee-149"><a name="DefineCommandSetECB"> </a></span><span class="sxs-lookup"><span data-stu-id="e8dee-149"></span></span>

## <a name="define-the-new-ecb-item"></a><span data-ttu-id="e8dee-150">Definieren des neuen ECB-Elements</span><span class="sxs-lookup"><span data-stu-id="e8dee-150">Define the new ECB item</span></span>

<span data-ttu-id="e8dee-151">Um das gleiche Verhalten des ECB-Menüelements zu reproduzieren, das mit dem SharePoint-Feature-Framework erstellt wurde, müssen Sie die gleiche Logik mithilfe von clientseitigem Code innerhalb der neuen SharePoint-Framework-Lösung implementieren.</span><span class="sxs-lookup"><span data-stu-id="e8dee-151"> In order to reproduce the same behavior of the ECB menu item built using the SharePoint Feature Framework, you simply need to implement the same logic using client-side code, within the new SharePoint Framework solution.</span></span> <span data-ttu-id="e8dee-152">Gehen Sie hierzu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="e8dee-152">To accomplish this task, complete the following steps.</span></span>

1. <span data-ttu-id="e8dee-153">Öffnen Sie die Datei **CustomEcbCommandSet.manifest.json** im Ordner **src/extensions/customEcb**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-153">Open the **CustomEcbCommandSet.manifest.json** file in the **src/extensions/customEcb** folder.</span></span> <span data-ttu-id="e8dee-154">Kopieren Sie den Wert der Eigenschaft `id`, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-154">Copy the value of the `id` property and store it in a safe place, because you will need it later.</span></span>

2. <span data-ttu-id="e8dee-155">Bearbeiten Sie in derselben Datei das Array von **items** im unteren Bereich der Datei, um einen einzelnen Befehl für das Command Set zu definieren.</span><span class="sxs-lookup"><span data-stu-id="e8dee-155">Within the same file edit the array of **"items"** in the lower part of the file, in order to define a single command for the Command Set.</span></span> <span data-ttu-id="e8dee-156">Rufen Sie den Befehl **ShowDetails** auf, und geben Sie dann einen Titel sowie einen Befehlstyp ein.</span><span class="sxs-lookup"><span data-stu-id="e8dee-156">Call the command **ShowDetails**, and then provide a title and a command type.</span></span> <span data-ttu-id="e8dee-157">Im folgenden Screenshot sehen Sie, wie die Manifestdatei aussehen soll.</span><span class="sxs-lookup"><span data-stu-id="e8dee-157">In the following screenshot you can see how the manifest file should look like.</span></span>

  ![Die Manifestdatei für das benutzerdefinierte Command Set](../../../images/spfx-ecb-extension-manifest.png)

3. <span data-ttu-id="e8dee-159">Öffnen Sie die Datei **CustomEcbCommandSet.ts** im Ordner **src/extensions/customEcb**, und bearbeiten Sie den Inhalt entsprechend dem folgenden Codeausschnitt:</span><span class="sxs-lookup"><span data-stu-id="e8dee-159">Open the **CustomEcbCommandSet.ts** file in the **src/extensions/customEcb** folder and edit the content according to the following code snippet:</span></span>

  ``` TypeScript
  import { Guid } from '@microsoft/sp-core-library';
  import { override } from '@microsoft/decorators';
  import {
    BaseListViewCommandSet,
    Command,
    IListViewCommandSetListViewUpdatedParameters,
    IListViewCommandSetExecuteEventParameters
  } from '@microsoft/sp-listview-extensibility';
  import { Dialog } from '@microsoft/sp-dialog';

  import * as strings from 'CustomEcbCommandSetStrings';

  export interface ICustomEcbCommandSetProperties {
    targetUrl: string;
  }

  export default class CustomEcbCommandSet extends BaseListViewCommandSet<ICustomEcbCommandSetProperties> {

    @override
    public onInit(): Promise<void> {
      return Promise.resolve();
    }

    @override
    public onListViewUpdated(event: IListViewCommandSetListViewUpdatedParameters): void {
      const compareOneCommand: Command = this.tryGetCommand('ShowDetails');
      if (compareOneCommand) {
        // This command should be hidden unless exactly one row is selected.
        compareOneCommand.visible = event.selectedRows.length === 1;
      }
    }

    @override
    public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
      switch (event.itemId) {
        case 'ShowDetails':

          const itemId: number = event.selectedRows[0].getValueByName("ID");
          const listId: Guid = this.context.pageContext.list.id;

          window.location.replace(`${this.properties.targetUrl}?ID=${itemId}&List=${listId}`);

          break;
        default:
          throw new Error('Unknown command');
      }
    }
  }
  ```

  <span data-ttu-id="e8dee-160">Beachten Sie die `import`-Anweisung am Anfang der Datei, die auf den Typ `Guid` verweist, der die ID der aktuellen Liste enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="e8dee-160">Notice the `import` statement at the very beginning of the file, in order to reference the `Guid` type, which will be used to hold the ID of the current list.</span></span> 
  
  <span data-ttu-id="e8dee-161">Darüber hinaus deklariert die Schnittstelle `ICustomEcbCommandSetProperties` eine einzelne Eigenschaft mit der Bezeichnung `targetUrl`, die verwendet werden kann, um die URL der Zielseite anzugeben, die beim Auswählen des ECB-Menüelements geöffnet werden soll.</span><span class="sxs-lookup"><span data-stu-id="e8dee-161">Moreover, the interface `ICustomEcbCommandSetProperties` declares a single property called `targetUrl` that can be used to provide the URL of the target page to open when clicking on the ECB menu item.</span></span>

  <span data-ttu-id="e8dee-162">Darüber hinaus behandelt die Überschreibung der `onExecute`-Methode die Ausführung der benutzerdefinierten Aktion.</span><span class="sxs-lookup"><span data-stu-id="e8dee-162">Furthermore, the override of the `onExecute` method handles the execution of the custom action.</span></span> <span data-ttu-id="e8dee-163">Beachten Sie den Codeauszug, der die ID des aktuell ausgewählten Elements aus dem `event`-Argument sowie die ID der Quellliste aus dem `pageContext`-Objekt abruft.</span><span class="sxs-lookup"><span data-stu-id="e8dee-163">Notice the code excerpt that reads the ID of the currently selected item, from the `event` argument, and the ID of the source list from the the `pageContext` object.</span></span>

  <span data-ttu-id="e8dee-164">Beachten Sie schließlich auch die Überschreibung der `onListViewUpdated`-Methode, die standardmäßig den Befehl `'ShowDetails'` nur dann aktivierte, wenn ein einzelnes Element ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="e8dee-164">Lastly, notice the override of the `onListViewUpdated` method, which by default enabled the `'ShowDetails'` command only if a single item is selected.</span></span>

  <span data-ttu-id="e8dee-165">Die Umleitung an die Ziel-URL erfolgt durch die Verwendung von klassischem JavaScript-Code und der Funktion `window.location.replace`.</span><span class="sxs-lookup"><span data-stu-id="e8dee-165">The redirection to the target URL is handled by using classic JavaScript code and using the `window.location.replace` function.</span></span> <span data-ttu-id="e8dee-166">Sie können natürlich jede Art von TypeScript-Code in die `onExecute`-Methode schreiben.</span><span class="sxs-lookup"><span data-stu-id="e8dee-166">Of course, you can write whatever kind of TypeScript code you like inside the `onExecute` method.</span></span> <span data-ttu-id="e8dee-167">Um hier nur ein Beispiel zu nennen, können Sie das Dialog-Framework des SharePoint-Frameworks verwenden, um ein neues Dialogfeld zu öffnen und mit Benutzern zu interagieren.</span><span class="sxs-lookup"><span data-stu-id="e8dee-167">Just for the sake of making an example, you can leverage the SharePoint Framework Dialog Framework to open a new dialog window and to interact with the end users.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e8dee-168">Weitere Informationen zum Dialog-Framework des SharePoint-Frameworks finden Sie unter [Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint-Framework-Erweiterungen](./using-custom-dialogs-with-spfx.md).</span><span class="sxs-lookup"><span data-stu-id="e8dee-168">For further details about the SharePoint Framework Dialog Framework you can read the document [Use custom dialog boxes with SharePoint Framework Extensions](./using-custom-dialogs-with-spfx.md).</span></span>

  <br/>

  <span data-ttu-id="e8dee-169">In der folgenden Abbildung ist die resultierende Ausgabe enthalten.</span><span class="sxs-lookup"><span data-stu-id="e8dee-169">In the following figure you can see the resulting output.</span></span>

  ![Das Command Set von ECB, gerendert in einer „modernen“ Liste](../../../images/spfx-ecb-extension-output.png)

<span data-ttu-id="e8dee-171"><a name="DebugCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="e8dee-171"></span></span>

## <a name="test-the-solution-in-debug-mode"></a><span data-ttu-id="e8dee-172">Testen der Lösung im Debugmodus</span><span class="sxs-lookup"><span data-stu-id="e8dee-172">Test the solution in debug mode</span></span>

1. <span data-ttu-id="e8dee-173">Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus, um die Lösung zu erstellen und den lokalen Node.js-Server zum Hosten der Lösung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-173">Go back to the console window and run the following command to build the solution and run the local Node.js server to host it.</span></span>

  ```
  gulp serve --nobrowser
  ```

2. <span data-ttu-id="e8dee-174">Öffnen Sie Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Bibliothek einer beliebigen „modernen“ Teamwebsite.</span><span class="sxs-lookup"><span data-stu-id="e8dee-174">Now open your favorite browser and go to a "modern" library of any "modern" team site.</span></span> <span data-ttu-id="e8dee-175">Hängen Sie die folgenden Abfragezeichenfolgeparameter an die **AllItems.aspx**-Seiten-URL an.</span><span class="sxs-lookup"><span data-stu-id="e8dee-175">Append the following query string parameters to the URL.</span></span>

  ```
  ?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6c5b8ee9-43ba-4cdf-a106-04857c8307be":{"location":"ClientSideExtension.ListViewCommandSet.ContextMenu","properties":{"targetUrl":"ShowDetail.aspx"}}}
  ```

  <span data-ttu-id="e8dee-176">Ersetzen Sie in der vorherigen Abfragezeichenfolge die GUID durch den `id`-Wert aus der Datei **CustomEcbCommandSet.manifest.json** ersetzen, den Sie gespeichert und aufbewahrt haben.</span><span class="sxs-lookup"><span data-stu-id="e8dee-176">In the above querystring, you will have to replace the GUID with the `id` value you saved from the **CustomEcbCommandSet.manifest.json** file.</span></span> 
  
  <span data-ttu-id="e8dee-177">Es ist außerdem eine `location`-Eigenschaft vorhanden, die den Wert von **ClientSideExtension.ListViewCommandSet.ContextMenu** annimmt. Dieser weist SPFx an, das Command Set als ein ECB-Menüelement zu rendern.</span><span class="sxs-lookup"><span data-stu-id="e8dee-177">Moreover, there is a `location` property which assumes the value of **ClientSideExtension.ListViewCommandSet.ContextMenu**, which instructs SPFx to render the Command Set as an ECB menu item.</span></span> <span data-ttu-id="e8dee-178">Nachfolgend finden Sie alle Optionen für die `location`-Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="e8dee-178">Here are all the available options for the `location` property:</span></span>
  
  * <span data-ttu-id="e8dee-179">**ClientSideExtension.ListViewCommandSet.ContextMenu**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-179">**ClientSideExtension.ListViewCommandSet.ContextMenu**.</span></span>  <span data-ttu-id="e8dee-180">Im Kontextmenü für die Elemente.</span><span class="sxs-lookup"><span data-stu-id="e8dee-180">ClientSideExtension.ListViewCommandSet.ContextMenu:  The context menu of the item(s)</span></span>
  * <span data-ttu-id="e8dee-181">**ClientSideExtension.ListViewCommandSet.CommandBar**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-181">**ClientSideExtension.ListViewCommandSet.CommandBar**.</span></span> <span data-ttu-id="e8dee-182">Das obere Befehlssatzmenü in einer Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="e8dee-182">ClientSideExtension.ListViewCommandSet.CommandBar: The top command set menu in a list or library</span></span>
  * <span data-ttu-id="e8dee-183">**ClientSideExtension.ListViewCommandSet**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-183">**ClientSideExtension.ListViewCommandSet**.</span></span> <span data-ttu-id="e8dee-184">Sowohl im Kontextmenü als auch auf der Befehlsleiste (entspricht `SPUserCustomAction.Location="CommandUI.Ribbon"`).</span><span class="sxs-lookup"><span data-stu-id="e8dee-184">`SPUserCustomAction.Location="CommandUI.Ribbon"` Both the context menu and the command bar (Corresponds to SPUserCustomAction.Location="CommandUI.Ribbon")</span></span>

  <span data-ttu-id="e8dee-185">Schließlich befindet sich in der Abfragezeichenfolge noch die Eigenschaft `properties`, die die JSON-Serialisierung eines Objekts vom Typ `ICustomEcbCommandSetProperties` darstellt. Dies ist der Typ der benutzerdefinierten Eigenschaften, die das benutzerdefinierte Command Set zum Rendern anfordert.</span><span class="sxs-lookup"><span data-stu-id="e8dee-185">Lastly, still in the querystring there is a property called `properties`, which represents the JSON serialization of an object of type `ICustomEcbCommandSetProperties` that is the type of the custom properties requested by the custom Command Set for rendering.</span></span>

  <span data-ttu-id="e8dee-186">Beachten Sie, dass beim Ausführen der Seitenanforderung ein Warnmeldungsfeld „Debugskripts zulassen?“ angezeigt wird, in dem Sie aus Sicherheitsgründen nach der Zustimmung für die Ausführung des Codes von Localhost gefragt werden.</span><span class="sxs-lookup"><span data-stu-id="e8dee-186">Notice that, when executing the page request, you will be prompted with a warning message box with title "Allow debug scripts?", which asks your consent to run code from localhost, for security reasons.</span></span> <span data-ttu-id="e8dee-187">Wenn Sie die Lösung lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-187">Of course, if you want to locally debug and test the solution, you will have to allow to "Load debug scripts".</span></span>

<span data-ttu-id="e8dee-188"><a name="PackageAndHostCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="e8dee-188"></span></span>

## <a name="package-and-host-the-solution"></a><span data-ttu-id="e8dee-189">Packen und Hosten der Lösung</span><span class="sxs-lookup"><span data-stu-id="e8dee-189">Package and host the solution</span></span>

<span data-ttu-id="e8dee-190">Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.</span><span class="sxs-lookup"><span data-stu-id="e8dee-190">If you are happy with the result, you are now ready to package the solution and host it in a real hosting infrastructure.</span></span>
<span data-ttu-id="e8dee-191">Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature-Framework-Datei deklarieren, um die Erweiterung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-191">Before building the bundle and the package, you need to declare an XML feature framework file to provision the extension.</span></span>

### <a name="review-feature-framework-elements"></a><span data-ttu-id="e8dee-192">Überprüfen von Feature-Framework-Elementen</span><span class="sxs-lookup"><span data-stu-id="e8dee-192">Review feature framework elements</span></span>

1. <span data-ttu-id="e8dee-193">Öffnen Sie im Code-Editor den Unterordner **/sharepoint/assets** der Lösung, und bearbeiten Sie die Datei **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-193">Within the code editor, open the **/sharepoint/assets** sub-folder of the solution folder and edit the **elements.xml** file.</span></span> <span data-ttu-id="e8dee-194">Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.</span><span class="sxs-lookup"><span data-stu-id="e8dee-194">In the following code excerpt you can see how the file should look like.</span></span>

  ```XML
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction
          Title="CustomEcb"
          RegistrationId="101"
          RegistrationType="List"
          Location="ClientSideExtension.ListViewCommandSet.ContextMenu"
          ClientSideComponentId="6c5b8ee9-43ba-4cdf-a106-04857c8307be"
          ClientSideComponentProperties="{&quot;targetUrl&quot;:&quot;ShowDetails.aspx&quot;}">
      </CustomAction>
  </Elements>
  ```

  <span data-ttu-id="e8dee-195">Wie Sie sehen, ähnelt sie der SharePoint-Feature-Framework-Datei des „klassischen“ Modells. Sie verwendet jedoch das Attribut `ClientSideComponentId`, um die `id` der benutzerdefinierten Erweiterung zu referenzieren, sowie das Attribut `ClientSideComponentProperties`, um die benutzerdefinierten Konfigurationseigenschaften zu konfigurieren, die für die Erweiterung erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="e8dee-195">As you can see, it reminds the SharePoint Feature Framework file that we saw in the "classic" model, but it uses the `ClientSideComponentId` attribute to reference the `id` of the custom extension, and the `ClientSideComponentProperties` attribute, to configure the custom configuration properties required by the extension.</span></span>

2. <span data-ttu-id="e8dee-196">Öffnen Sie die Datei **package-solution.json** im Lösungsordner **/config**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-196">Now, open the **package-solution.json** file under the **/config** folder of the solution.</span></span> <span data-ttu-id="e8dee-197">In der Datei können Sie sehen, dass ein Verweis auf die Datei **elements.xml** im Abschnitt `assets` vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="e8dee-197">Within the file you can see that there is a reference to the **elements.xml** file, within the `assets` section.</span></span>

  ```JSON
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "spfx-ecb-extension-client-side-solution",
      "id": "b8ff6fdf-16e9-4434-9fdb-eac6c5f948ee",
      "version": "1.0.2.0",
      "features": [
        {
          "title": "Custom ECB Menu Item.",
          "description": "Deploys a custom ECB menu item sample extension",
          "id": "f30a744c-6f30-4ccc-a428-125a290b5233",
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
      "zippedPackage": "solution/spfx-ecb-extension.sppkg"
    }
  }
  ```

### <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="e8dee-198">Aktivieren des CDN im Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="e8dee-198">Enable the CDN in your Office 365 tenant</span></span>

<span data-ttu-id="e8dee-199">Sie müssen die Erweiterung nun in einer Hostingumgebung hosten.</span><span class="sxs-lookup"><span data-stu-id="e8dee-199">Now you need to host the extension in a hosting environment.</span></span> <span data-ttu-id="e8dee-200">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-200">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="e8dee-201">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="e8dee-201">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="e8dee-202">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="e8dee-202">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```powershell
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="e8dee-203">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="e8dee-203">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="e8dee-204">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="e8dee-204">Enable public CDN in the tenant:</span></span>
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="e8dee-205">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-205">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="e8dee-206">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="e8dee-206">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="e8dee-p126">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-p126">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="e8dee-210">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens **CDN**, und fügen Sie ihr einen Ordner namens **customecb** hinzu.</span><span class="sxs-lookup"><span data-stu-id="e8dee-210">Create a new document library on your site collection called **CDN** and add a folder named **customecb** to it.</span></span>
    
7. <span data-ttu-id="e8dee-211">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="e8dee-211">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="e8dee-212">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen **cdn** als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="e8dee-212">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** acts as a CDN origin.</span></span>
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="e8dee-213">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="e8dee-213">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
  <span data-ttu-id="e8dee-214">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="e8dee-214">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="e8dee-215">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie mit dem Bereitstellen der Erweiterung fortfahren, die anschließend im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="e8dee-215">Final configuration of the origin takes approximately 15 minutes, so we can continue provisioning the extension, which will be hosted from the origin after deployment is completed.</span></span> 

  ![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

  <span data-ttu-id="e8dee-217">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e8dee-217">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="e8dee-218">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="e8dee-218">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a><span data-ttu-id="e8dee-219">Aktualisieren der Lösungseinstellungen und Veröffentlichen im CDN</span><span class="sxs-lookup"><span data-stu-id="e8dee-219">Update the solution settings and publish it on the CDN</span></span>

<span data-ttu-id="e8dee-220">Als Nächstes müssen Sie die Lösung aktualisieren, um das gerade erstellte CDN als Hostingumgebung zu verwenden. Sie müssen das Lösungsbundle im CDN veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-220">Now, you need to update the solution in order to use the just created CDN as the hosting enviroment and you will need to publish the solution bundle to the CDN.</span></span> <span data-ttu-id="e8dee-221">Um diese Aufgabe auszuführen, gehen Sie folgendermaßen vor.</span><span class="sxs-lookup"><span data-stu-id="e8dee-221">To accomplish this task, just follow the upcoming steps.</span></span>

1. <span data-ttu-id="e8dee-222">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderlichen URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-222">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="e8dee-223">Aktualisieren Sie die Datei **write-manifests.json** (im Ordner **config**) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="e8dee-223">Update the **write-manifests.json** file (under the **config** folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="e8dee-224">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="e8dee-224">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="e8dee-225">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="e8dee-225">The format of the CDN URL is as follows:</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-write-manifest.png)

3. <span data-ttu-id="e8dee-227">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-227">Save your changes.</span></span>

4. <span data-ttu-id="e8dee-228">Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="e8dee-228">Execute the following task to bundle your solution.</span></span> <span data-ttu-id="e8dee-229">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei **write-manifests.json** angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="e8dee-229">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="e8dee-230">Die Ausgabe dieses Befehls finden Sie im Ordner **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-230">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="e8dee-231">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="e8dee-231">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="e8dee-232">Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-232">Execute the following task to package your solution.</span></span> <span data-ttu-id="e8dee-233">Dieser Befehl erstellt ein Paket namens **spfx-ecb-extension.sppkg** im Ordner **sharepoint/solution** und bereitet die Ressourcen im Ordner **temp/deploy** für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="e8dee-233">This command creates an **spfx-ecb-extension.sppkg** package in the **sharepoint/solution** folder and also prepares the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="e8dee-234">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="e8dee-234">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the **Deploy** button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-cdn-address.png)

7. <span data-ttu-id="e8dee-236">Laden Sie die Dateien im Ordner **temp/deploy** in den Ordner **CDN/customfooter** hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="e8dee-236">Upload or drag-and-drop the files in the **temp/deploy** folder to the **CDN/customfooter** folder created earlier.</span></span>

<span data-ttu-id="e8dee-237"><a name="InstallCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="e8dee-237"></span></span>

## <a name="install-and-run-the-solution"></a><span data-ttu-id="e8dee-238">Installieren und Ausführen der Lösung</span><span class="sxs-lookup"><span data-stu-id="e8dee-238">Install and run the solution</span></span>

1. <span data-ttu-id="e8dee-239">Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="e8dee-239">Open the browser and navigate to any target "modern" site.</span></span>

2. <span data-ttu-id="e8dee-240">Navigieren Sie zur Seite **Websiteinhalte**, und wählen Sie **App**, um eine neue App hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-240">Go to the **"Site Contents"** page and select to add a new **App**.</span></span>

3. <span data-ttu-id="e8dee-241">Wählen Sie zum Installieren einer neuen App **Von Ihrer Organisation** aus, um die im App-Katalog verfügbaren Lösungen zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-241">Select to install a new app "From Your Organization" to browse the solutions available in the AppCatalog.</span></span>

4. <span data-ttu-id="e8dee-242">Wählen Sie die Lösung mit dem Namen **spfx-ecb-extension-client-side-solution** aus, und installieren Sie sie auf der Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="e8dee-242">Select the solution called **"spfx-ecb-extension-client-side-solution"** and istall it on the target site.</span></span>

    ![Hinzufügen einer App-Benutzeroberfläche zum Hinzufügen der Lösung zu einer Website](../../../images/spfx-ecb-extension-add-app.png)

5. <span data-ttu-id="e8dee-244">Nachdem die Installation der Anwendung abgeschlossen ist, öffnen Sie die **Documents**-Bibliothek der Website, und sehen Sie sich das funktionsfähige ECB-Menüelement an, indem Sie ein einzelnes Dokument auswählen.</span><span class="sxs-lookup"><span data-stu-id="e8dee-244">Once the application installation will be completed, open the **"Documents"** library of the site and see the custom ECB menu item in action by selecting a single document.</span></span>

<span data-ttu-id="e8dee-245">Sie können nun Ihr neues benutzerdefiniertes ECB-Menüelement nutzen, das Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e8dee-245">Enjoy your new custom ECB menu item built using the SharePoint Framework extensions!</span></span>

## <a name="see-also"></a><span data-ttu-id="e8dee-246">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e8dee-246">See also</span></span>

- [<span data-ttu-id="e8dee-247">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="e8dee-247">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)
