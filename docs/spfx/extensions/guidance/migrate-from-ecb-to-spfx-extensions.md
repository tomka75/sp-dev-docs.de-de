---
title: "Lernprogramm: Migrieren vom Edit Control Block-Menüelement (ECB) zur SharePoint-Framework-Erweiterung"
ms.date: 12/19/2017
ms.prod: sharepoint
ms.openlocfilehash: f285cdbe3ac5e771b0afc0286dcaedd361e643e2
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="migrating-from-edit-control-block-ecb-menu-item-to-sharepoint-framework-extensions"></a><span data-ttu-id="a6b89-102">Migrieren vom Edit Control Block-Menüelement (ECB) zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="a6b89-102">Migrating from Edit Control Block (ECB) menu item to SharePoint Framework Extensions</span></span>

<span data-ttu-id="a6b89-103">In den letzten Jahren haben die meisten Unternehmenslösungen, die auf Office 365 und SharePoint Online aufbauen, die Funktion _CustomAction_ des SharePoint-Feature-Framework genutzt, um die Benutzeroberfläche von Seiten zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="a6b89-103">During the last few years, most of the enterprise solutions built on top of Office 365 and SharePoint Online leveraged the site _CustomAction_ capability of the SharePoint Feature Framework to extend the UI of pages.</span></span> <span data-ttu-id="a6b89-104">Heute stehen die meisten dieser Anpassungsmöglichkeiten in der „modernen“ Benutzeroberfläche von SharePoint Online jedoch nicht mehr zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="a6b89-104">However nowdays, within the new "modern" UI of SharePoint Online, most of those customizations are no more available.</span></span> <span data-ttu-id="a6b89-105">Mit den neuen SharePoint-Framework-Erweiterungen können Sie jedoch fast die gleichen Funktionen auch in der modernen Benutzeroberfläche bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-105">Luckily, with the new SharePoint Framework Extensions you can provide similar functionality in the "modern" UI.</span></span> <span data-ttu-id="a6b89-106">In diesem Lernprogramm erfahren Sie, wie Sie die alten, klassischen Anpassungen zu dem neuen Modell basierend auf SharePoint-Framework-Erweiterungen migrieren können.</span><span class="sxs-lookup"><span data-stu-id="a6b89-106">In this tutorial you will learn how to migrate from old "classic" customizations to the new model based on SharePoint Framework Extensions.</span></span>

## <a name="understanding-sharepoint-framework-extensions"></a><span data-ttu-id="a6b89-107">Grundlegendes zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="a6b89-107">Understanding SharePoint Framework Extensions</span></span>
<span data-ttu-id="a6b89-108"><a name="spfxExtensions"> </a> Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:</span><span class="sxs-lookup"><span data-stu-id="a6b89-108"><a name="spfxExtensions"> </a> First of all, let's introduce the available options when developing SharePoint Framework Extensions:</span></span>

* <span data-ttu-id="a6b89-109">**Application Customizer**: Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="a6b89-109">**Application Customizer**: extend the native "modern" UI of SharePoint Online by adding custom HTML elements and client-side code to pre-defined placeholders of "modern" pages.</span></span> <span data-ttu-id="a6b89-110">Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.</span><span class="sxs-lookup"><span data-stu-id="a6b89-110">At the time of this writing, the available placeholders are the header and the footer of every "modern" page.</span></span>
* <span data-ttu-id="a6b89-111">**Command Set**: Benutzerdefinierte ECB-Menüelemente oder benutzerdefinierte Schaltflächen können der Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="a6b89-111">**Command Set**: allow to add custom ECB menu items or custom buttons to the command bar of a list view for a list or a library.</span></span> <span data-ttu-id="a6b89-112">Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-112">You can associate any JavaScript (TypeScript) action to these commands.</span></span>
* <span data-ttu-id="a6b89-113">**Field Customizer**: Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.</span><span class="sxs-lookup"><span data-stu-id="a6b89-113">**Field Customizer**: customize the rendering of a field in a list view using custom HTML elements and client-side code.</span></span>

<span data-ttu-id="a6b89-114">Wie bereits aus der obigen Beschreibung hervorgeht, ist die „Command Set“-Erweiterung die nützlichste in diesem Kontext.</span><span class="sxs-lookup"><span data-stu-id="a6b89-114">As you can argue from the above descriptions, the most useful one in our context is the "Command Set" extension.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b89-115">Weitere Informationen zum Erstellen von SharePoint-Framework-Erweiterungen finden Sie im Artikel [Übersicht über SharePoint-Framework-Erweiterungen]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/overview-extensions)).</span><span class="sxs-lookup"><span data-stu-id="a6b89-115">For further details about how to build SharePoint Framework Extensions you can read the article ["Overview of SharePoint Framework Extensions"]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/overview-extensions)).</span></span>

## <a name="migrating-a-ecb-to-an-spfx-command-set"></a><span data-ttu-id="a6b89-116">Migrieren eines ECB zu einem Command Set von SPFx</span><span class="sxs-lookup"><span data-stu-id="a6b89-116">Migrating a ECB to an SPFx Command Set</span></span>
<span data-ttu-id="a6b89-117"><a name="FromECBtoCommandSet"> </a> Angenommen Sie verfügen über eine _CustomAction_ in SharePoint Online, damit für Dokumente in einer Bibliothek ein benutzerdefiniertes ECB-Menü verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="a6b89-117"><a name="FromECBtoCommandSet"> </a> Assume that you have a _CustomAction_ in SharePoint Online, in order to have a custom ECB menu item for documents in a library.</span></span> <span data-ttu-id="a6b89-118">Die Funktion des ECB-Menüelements besteht darin, eine benutzerdefinierte Seite zu öffnen, auf der die Listen-ID und die Listenelement-ID des aktuell ausgewählten Elements in der Abfragezeichenfolge der Zielseite bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="a6b89-118">The scope of the ECB menu item is to open a custom page, providing the list ID and the list item ID of the currently selected item in the querystring of the target page.</span></span>
<span data-ttu-id="a6b89-119">Im folgenden Codeausschnitt ist der XML-Code enthalten, der _CustomAction_ mithilfe des SharePoint-Feature-Frameworks definiert.</span><span class="sxs-lookup"><span data-stu-id="a6b89-119">In the following code snippet you can see the XML code defining that _CustomAction_ using the SharePoint Feature Framework.</span></span>

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

<span data-ttu-id="a6b89-120">Wie Sie sehen können, definiert die Funktionselementdatei ein Element des Typs _CustomAction_, um ein neues Element am Ort von _EditControlBlock_ (d. h. ECB) für ein beliebiges Dokument in einer beliebigen Bibliothek hinzuzufügen (_ RegistrationType_ ist _List_ und _RegistrationId_ ist _101_).</span><span class="sxs-lookup"><span data-stu-id="a6b89-120">As you can see, the feature elements file defines an element of type _CustomAction_ to add a new item in the _EditControlBlock_ location (i.e. ECB) for any document in any library (_RegistrationType_ is _List_ and _RegistrationId_ is _101_).</span></span>

<span data-ttu-id="a6b89-121">In der folgenden Abbildung sehen Sie die Ausgabe der vorherigen benutzerdefinierten Aktion in der Listenansicht einer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="a6b89-121">In the following figure you can see the output of the previous custom action, within the list view of a library.</span></span>

![Die benutzerdefinierte Fußzeile auf einer klassischen Seite](../../../images/ecb-menu-classic-output.png)

<span data-ttu-id="a6b89-123">Beachten Sie, dass das benutzerdefinierte ECB-Element des SharePoint-Feature-Framework auch in einer „modernen“ Liste funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a6b89-123">Notice that the SharePoint Feature Framework ECB custom item works in a "modern" list, too.</span></span> <span data-ttu-id="a6b89-124">Tatsächlich funktioniert eine benutzerdefinierte Listenaktion auch in „modernen“ Listen, solange Sie keinen JavaScript-Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="a6b89-124">In fact, as long as you don't use JavaScript code, a list custom action still works in "modern" lists, too.</span></span>

<span data-ttu-id="a6b89-125">Um die oben aufgeführte Lösung in das SharePoint-Framework zu migrieren, müssen Sie die folgenden Schritte ausführen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-125">In order to migrate the above solution to the SharePoint Framework, you will have to accomplish the following steps.</span></span>

### <a name="create-a-new-sharepoint-framework-solution"></a><span data-ttu-id="a6b89-126">Erstellen einer neuen SharePoint-Framework-Lösung</span><span class="sxs-lookup"><span data-stu-id="a6b89-126">Create a new SharePoint Framework solution</span></span>
<span data-ttu-id="a6b89-127"><a name="CreateCommandSet"> </a> Nachdem Sie die Entwicklungsumgebung für SharePoint-Framework-Lösungen entsprechend den Anweisungen im Dokument [Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/set-up-your-development-environment)) eingerichtet haben, können Sie mit dem Erstellen einer SharePoint-Framework-Erweiterung beginnen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-127"><a name="CreateCommandSet"> </a> Once you have prepared you development environment to develop SharePoint Framework solutions, by following the instructions provided in the document ["Set up your SharePoint client-side web part development environment"]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/set-up-your-development-environment)), you can start creating a SharePoint Framework extension.</span></span>

1. <span data-ttu-id="a6b89-128">Öffnen Sie ein beliebiges Befehlszeilentool (PowerShell, CMD.EXE, Cmder usw.), erstellen Sie einen neuen Ordner für die Lösung (mit dem Namen _spfx-ecb-extension_), und erstellen Sie eine neue SharePoint-Framework-Lösung, indem Sie den Yeoman-Generator mit dem folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="a6b89-128">Open the command line tool of your choice (PowerShell, CMD.EXE, Cmder, etc.), create a new folder for the solution (call it _spfx-ecb-extension_), and create a new SharePoint Framework solution by running the Yeoman generator with the following command:</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="a6b89-129">Geben Sie bei Aufforderung durch das Tool Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="a6b89-129">When prompted by the tool, provide the following answers:</span></span>
* <span data-ttu-id="a6b89-130">Bestätigen Sie den Standardnamen (_spfx-ecb-extension_) für Ihre Lösung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a6b89-130">Accept the default name (_spfx-ecb-extension_) for your solution, and press Enter.</span></span>
* <span data-ttu-id="a6b89-131">Wählen Sie „SharePoint Online only (latest)“, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a6b89-131">Choose SharePoint Online only (latest), and press Enter.</span></span>
* <span data-ttu-id="a6b89-132">Wählen Sie „Use the current folder“ aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="a6b89-132">Choose Use the current folder, and press Enter.</span></span>
* <span data-ttu-id="a6b89-133">Wählen Sie „N“, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a6b89-133">Choose N to require the extension to be installed on each site explicitly when it's being used.</span></span>
* <span data-ttu-id="a6b89-134">Wählen Sie „Extension“ als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="a6b89-134">Choose Extension as the client-side component type to be created.</span></span>
* <span data-ttu-id="a6b89-135">Wählen Sie _ListView Command Set_ als den zu erstellenden Typ von Erweiterung aus.</span><span class="sxs-lookup"><span data-stu-id="a6b89-135">Choose _"ListView Command Set"_ as the extension type to be created.</span></span>
* <span data-ttu-id="a6b89-136">Geben Sie „CustomECB“ als Namen für Ihr Command Set an.</span><span class="sxs-lookup"><span data-stu-id="a6b89-136">Provide "CustomECB" as the name for your Command Set.</span></span>

![Die Benutzeroberfläche des Yeoman-Generators beim Erstellen der benutzerdefinierten Fußzeilenlösung](../../../images/spfx-ecb-extension-yeoman.png)

<span data-ttu-id="a6b89-138">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien und Ordner sowie die _CustomFooter_-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="a6b89-138">At this point, Yeoman will install the required dependencies and scaffold the solution files and folders along with the _CustomFooter_ extension.</span></span> <span data-ttu-id="a6b89-139">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="a6b89-139">This might take a few minutes.</span></span>

<span data-ttu-id="a6b89-140">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="a6b89-140">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Gerüsterstellung abgeschlossen](../../../images/spfx-ecb-extension-yeoman-completed.png)

2. <span data-ttu-id="a6b89-142">Führen Sie den folgenden Befehl aus, um die Version der Projektabhängigkeiten zu sperren:</span><span class="sxs-lookup"><span data-stu-id="a6b89-142">To lock down the version of the project dependencies, run the following command:</span></span>

```
npm shrinkwrap
```

3. <span data-ttu-id="a6b89-143">Starten Sie jetzt Visual Studio Code (oder einen anderen Code-Editor), und beginnen Sie mit der Entwicklung der Lösung.</span><span class="sxs-lookup"><span data-stu-id="a6b89-143">Now start Visual Studio Code (or whatever else is the code editor of your choice) and start developing the solution.</span></span> <span data-ttu-id="a6b89-144">Zum Starten von Visual Studio Code können Sie die folgende Anweisung ausführen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-144">To start Visual Studio Code, you can execute the following statement.</span></span>

```
code .
```

### <a name="define-the-new-ecb-item"></a><span data-ttu-id="a6b89-145">Definieren des neuen ECB-Elements</span><span class="sxs-lookup"><span data-stu-id="a6b89-145">Define the new ECB item</span></span>
<span data-ttu-id="a6b89-146"><a name="DefineCommandSetECB"> </a> Um das gleiche Verhalten des ECB-Menüelements zu reproduzieren, das mit dem SharePoint-Feature-Framework erstellt wurde, müssen Sie einfach die gleiche Logik mit clientseitigem Code innerhalb der neuen SharePoint-Framework-Lösung implementieren.</span><span class="sxs-lookup"><span data-stu-id="a6b89-146"><a name="DefineCommandSetECB"> </a> In order to reproduce the same behavior of the ECB menu item built using the SharePoint Feature Framework, you simply need to implement the same logic using client-side code, within the new SharePoint Framework solution.</span></span> <span data-ttu-id="a6b89-147">Gehen Sie hierzu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="a6b89-147">To accomplish this task, complete the following steps.</span></span>

1. <span data-ttu-id="a6b89-148">Öffnen Sie zunächst die Datei _CustomEcbCommandSet.manifest.json_ im Ordner _src/extensions/customEcb_.</span><span class="sxs-lookup"><span data-stu-id="a6b89-148">First of all, open the file _CustomEcbCommandSet.manifest.json_ under the _src/extensions/customEcb_ folder.</span></span> <span data-ttu-id="a6b89-149">Kopieren Sie den Wert der Eigenschaft _id_, und bewahren Sie ihn an einem sicheren Ort auf, da Sie ihn später benötigen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-149">Copy the value of the _id_ property and store it in a safe place, because you will need it later.</span></span>

2. <span data-ttu-id="a6b89-150">Bearbeiten Sie in derselben Datei das Array von _items_ im unteren Bereich der Datei, um einen einzelnen Befehl für das Command Set zu definieren.</span><span class="sxs-lookup"><span data-stu-id="a6b89-150">Within the same file edit the array of _"items"_ in the lower part of the file, in order to define a single command for the Command Set.</span></span> <span data-ttu-id="a6b89-151">Rufen Sie den Befehl _ShowDetails_ auf, und geben Sie einen Titel sowie einen Befehlstyp ein.</span><span class="sxs-lookup"><span data-stu-id="a6b89-151">Call the command _"ShowDetails"_, provide a Title, and a command type.</span></span> <span data-ttu-id="a6b89-152">Im folgenden Screenshot sehen Sie, wie die Manifestdatei aussehen soll.</span><span class="sxs-lookup"><span data-stu-id="a6b89-152">In the following screenshot you can see how the manifest file should look like.</span></span>

![Die Manifestdatei für das benutzerdefinierte Command Set](../../../images/spfx-ecb-extension-manifest.png)

3. <span data-ttu-id="a6b89-154">Öffnen Sie jetzt die Datei _CustomEcbCommandSet.ts_, die sich in demselben Ordner wie zuvor befindet, und bearbeiten Sie den Inhalt entsprechend dem folgenden Codeauszug.</span><span class="sxs-lookup"><span data-stu-id="a6b89-154">Now, open the _CustomEcbCommandSet.ts_ file, still under the same folder as before and edit the content accordingly to the following code excerpt.</span></span>

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

<span data-ttu-id="a6b89-155">Beachten Sie die _import_-Anweisung ganz am Anfang der Datei, die den _Guid_-Typ referenziert und die ID der aktuellen Liste beinhaltet.</span><span class="sxs-lookup"><span data-stu-id="a6b89-155">Notice the _import_ statement at the very beginning of the file, in order to reference the _Guid_ type, which will be used to hold the ID of the current list.</span></span> <span data-ttu-id="a6b89-156">Darüber hinaus deklariert die Schnittstelle _ICustomEcbCommandSetProperties_ eine einzelne Eigenschaft mit der Bezeichnung _targetUrl_, die verwendet werden kann, um die URL der Zielseite anzugeben, die beim Klicken auf das ECB-Menüelement geöffnet werden soll.</span><span class="sxs-lookup"><span data-stu-id="a6b89-156">Moreover, the interface _ICustomEcbCommandSetProperties_ declares a single property called _targetUrl_ that can be used to provide the URL of the target page to open when clicking on the ECB menu item.</span></span>
<span data-ttu-id="a6b89-157">Darüber hinaus behandelt die Überschreibung der _onExecute_-Methode die Ausführung der benutzerdefinierten Aktion.</span><span class="sxs-lookup"><span data-stu-id="a6b89-157">Furthermore, the override of the _onExecute_ method handles the execution of the custom action.</span></span> <span data-ttu-id="a6b89-158">Beachten Sie den Codeauszug, der die ID des aktuell ausgewählten Elements aus dem _event_-Argument sowie die ID der Quellliste aus dem _PageContext_-Objekt abruft.</span><span class="sxs-lookup"><span data-stu-id="a6b89-158">Notice the code excerpt that reads the ID of the currently selected item, from the _event_ argument, and the ID of the source list from the the _pageContext_ object.</span></span>
<span data-ttu-id="a6b89-159">Beachten Sie schließlich auch die Überschreiben der _OnListViewUpdated_-Methode, die standardmäßig den Befehl _ShowDetails_ nur dann aktivierte, wenn ein einzelnes Element ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="a6b89-159">Lastly, notice the override of the _onListViewUpdated_ method, which by default enabled the _'ShowDetails'_ command only if a single item is selected.</span></span>

<span data-ttu-id="a6b89-160">Die Umleitung an die Ziel-URL erfolgt durch die Verwendung von klassischem JavaScript-Code und der Funktion _window.location.replace_.</span><span class="sxs-lookup"><span data-stu-id="a6b89-160">The redirection to the target URL is handled by using classic JavaScript code and using the _window.location.replace_ function.</span></span> <span data-ttu-id="a6b89-161">Sie können natürlich jede Art von TypeScript-Code in die _OnExecute_-Methode schreiben.</span><span class="sxs-lookup"><span data-stu-id="a6b89-161">Of course, you can write whatever kind of TypeScript code you like inside the _onExecute_ method.</span></span> <span data-ttu-id="a6b89-162">Um hier nur ein Beispiel zu nennen, können Sie das Dialog-Framework des SharePoint-Frameworks verwenden, um ein neues Dialogfeld zu öffnen und mit den Endbenutzern zu interagieren.</span><span class="sxs-lookup"><span data-stu-id="a6b89-162">Just for the sake of making an example, you can leverage the SharePoint Framework Dialog Framework to open a new dialog window and to interact with the end users.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b89-163">Weitere Informationen zum Dialog-Framework von SharePoint-Framework finden Sie im Dokument [Verwenden von benutzerdefinierten Dialogfeldern mit SharePoint Framework Extensions]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/guidance/using-custom-dialogs-with-spfx)).</span><span class="sxs-lookup"><span data-stu-id="a6b89-163">For further details about the SharePoint Framework Dialog Framework you can read the document [Use custom dialog boxes with SharePoint Framework Extensions]((https://docs.microsoft.com/de-DE/sharepoint/dev/spfx/extensions/guidance/using-custom-dialogs-with-spfx)).</span></span>

<span data-ttu-id="a6b89-164">Die folgende Abbildung zeigt die resultierende Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="a6b89-164">In the following figure you can see the resulting output.</span></span>

![Das Command Set von ECB, gerendert in einer „modernen“ Liste](../../../images/spfx-ecb-extension-output.png)

### <a name="test-the-solution-in-debug-mode"></a><span data-ttu-id="a6b89-166">Testen der Lösung im Debugmodus</span><span class="sxs-lookup"><span data-stu-id="a6b89-166">Test the solution in debug mode</span></span>
<span data-ttu-id="a6b89-167"><a name="DebugCommandSet"> </a> Sie können die Lösung jetzt im Debugmodus testen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-167"><a name="DebugCommandSet"> </a> You are now ready to test your solution in debug mode.</span></span> 

1. <span data-ttu-id="a6b89-168">Kehren Sie zum Konsolenfenster zurück, und führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="a6b89-168">Go back to the console window and run the following command:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="a6b89-169">Der oben angegebene Befehl erstellt die Lösung und führt den lokalen Node.js-Server aus, um sie zu hosten.</span><span class="sxs-lookup"><span data-stu-id="a6b89-169">The above command will build the solution and run the local Node.js server to host it.</span></span>

2. <span data-ttu-id="a6b89-170">Öffnen Sie jetzt Ihren bevorzugten Browser, und wechseln Sie zu einer „modernen“ Bibliothek einer beliebigen „modernen“ Teamwebsite.</span><span class="sxs-lookup"><span data-stu-id="a6b89-170">Now open your favorite browser and go to a "modern" library of any "modern" team site.</span></span> <span data-ttu-id="a6b89-171">Hängen Sie jetzt die folgenden Abfragezeichenfolgeparameter an die _AllItems.aspx_-Seiten-URL an.</span><span class="sxs-lookup"><span data-stu-id="a6b89-171">Now, append the following querystring parameters to the _AllItems.aspx_ page URL.</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6c5b8ee9-43ba-4cdf-a106-04857c8307be":{"location":"ClientSideExtension.ListViewCommandSet.ContextMenu","properties":{"targetUrl":"ShowDetail.aspx"}}}
```

<span data-ttu-id="a6b89-172">In der oben aufgeführten Abfragezeichenfolge müssen Sie die GUID durch den _id_-Wert aus der Datei _CustomEcbCommandSet.manifest.json_ ersetzen, den Sie gespeichert und aufbewahrt haben.</span><span class="sxs-lookup"><span data-stu-id="a6b89-172">In the above querystring, you will have to replace the GUID with the _id_ value you saved from the _CustomEcbCommandSet.manifest.json_ file.</span></span> <span data-ttu-id="a6b89-173">Es ist außerdem eine _location_-Eigenschaft vorhanden, die den Wert von _ClientSideExtension.ListViewCommandSet.ContextMenu_ annimmt. Dieser weist SPFx an, das Command Set als ein ECB-Menüelement zu rendern.</span><span class="sxs-lookup"><span data-stu-id="a6b89-173">Moreover, there is a _location_ property which assumes the value of _ClientSideExtension.ListViewCommandSet.ContextMenu_, which instructs SPFx to render the Command Set as an ECB menu item.</span></span> <span data-ttu-id="a6b89-174">Nachfolgend sind alle für die _location_-Eigenschaft verfügbaren Optionen aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="a6b89-174">Here are all the available options for the _location_ property:</span></span>
* <span data-ttu-id="a6b89-175">**ClientSideExtension.ListViewCommandSet.ContextMenu:** im Kontextmenü der Elemente</span><span class="sxs-lookup"><span data-stu-id="a6b89-175">**ClientSideExtension.ListViewCommandSet.ContextMenu:**  The context menu of the item(s)</span></span>
* <span data-ttu-id="a6b89-176">**ClientSideExtension.ListViewCommandSet.CommandBar:** im oberen Befehlssatzmenü in einer Liste oder Bibliothek</span><span class="sxs-lookup"><span data-stu-id="a6b89-176">**ClientSideExtension.ListViewCommandSet.CommandBar:** The top command set menu in a list or library</span></span>
* <span data-ttu-id="a6b89-177">**ClientSideExtension.ListViewCommandSet:** sowohl im Kontextmenü als auch auf der Befehlsleiste (entspricht SPUserCustomAction.Location="CommandUI.Ribbon")</span><span class="sxs-lookup"><span data-stu-id="a6b89-177">**ClientSideExtension.ListViewCommandSet:** Both the context menu and the command bar (Corresponds to SPUserCustomAction.Location="CommandUI.Ribbon")</span></span>

<span data-ttu-id="a6b89-178">Schließlich befindet sich in der Abfragezeichenfolge auch noch die Eigenschaft _properties_, die die JSON-Serialisierung eines Objekts vom Typ _ICustomEcbCommandSetProperties_ darstellt. Dies ist der Typ der benutzerdefinierten Eigenschaften, die das benutzerdefinierte Command Set zum Rendern anfordert.</span><span class="sxs-lookup"><span data-stu-id="a6b89-178">Lastly, still in the querystring there is a property called _properties_, which represents the JSON serialization of an object of type _ICustomEcbCommandSetProperties_ that is the type of the custom properties requested by the custom Command Set for rendering.</span></span>

<span data-ttu-id="a6b89-179">Beachten Sie, dass beim Ausführen der Seitenanforderung eine Warnmeldung angezeigt wird, ob Sie Debugskripts zulassen möchten. Sie müssen aus Sicherheitsgründen bestätigen, dass Code von localhost ausgeführt werden darf.</span><span class="sxs-lookup"><span data-stu-id="a6b89-179">Notice that, when executing the page request, you will be prompted with a warning message box with title "Allow debug scripts?", which asks your consent to run code from localhost, for security reasons.</span></span> <span data-ttu-id="a6b89-180">Wenn Sie lokal debuggen und testen möchten, müssen Sie das Laden von Debugskripts zulassen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-180">Of course, if you want to locally debug and test the solution, you will have to allow to "Load debug scripts".</span></span>

### <a name="package-and-host-the-solution"></a><span data-ttu-id="a6b89-181">Packen und Hosten der Lösung</span><span class="sxs-lookup"><span data-stu-id="a6b89-181">Package and host the solution</span></span>
<span data-ttu-id="a6b89-182"><a name="PackageAndHostCommandSet"> </a> Wenn Sie mit dem Ergebnis zufrieden sind, können Sie die Lösung nun packen und in der eigentlichen Hostinginfrastruktur hosten.</span><span class="sxs-lookup"><span data-stu-id="a6b89-182"><a name="PackageAndHostCommandSet"> </a> If you are happy with the result, you are now ready to package the solution and host it in a real hosting infrastructure.</span></span>
<span data-ttu-id="a6b89-183">Bevor Sie das Bundle und das Paket erstellen, müssen Sie eine XML-Feature Frameworkdatei deklarieren, um die Erweiterung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-183">Before building the bundle and the package, you need to declare an XML feature framework file to provision the extension.</span></span>

#### <a name="review-feature-framework-elements"></a><span data-ttu-id="a6b89-184">Überprüfen von Feature-Framework-Elementen</span><span class="sxs-lookup"><span data-stu-id="a6b89-184">Review feature framework elements</span></span>
<span data-ttu-id="a6b89-185">Öffnen Sie im Code-Editor den Unterordner _/sharepoint/assets_ der Lösung, und bearbeiten Sie die Datei _elements.xml_.</span><span class="sxs-lookup"><span data-stu-id="a6b89-185">Within the code editor, open the _/sharepoint/assets_ sub-folder of the solution folder and edit the _elements.xml_ file.</span></span>
<span data-ttu-id="a6b89-186">Der folgende Codeauszug gibt an, wie die Datei aussehen sollte.</span><span class="sxs-lookup"><span data-stu-id="a6b89-186">In the following code excerpt you can see how the file should look like.</span></span>

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

<span data-ttu-id="a6b89-187">Wie Sie sehen, ähnelt sie der SharePoint-Feature-Framework-Datei des „klassischen“ Modells. Sie verwendet jedoch das Attribut _ClientSideComponentId_, um die _id_ der benutzerdefinierten Erweiterung zu referenzieren, sowie das Attribut _ClientSideComponentProperties_, um die benutzerdefinierten Konfigurationseigenschaften zu konfigurieren, die für die Erweiterung erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="a6b89-187">As you can see, it reminds the SharePoint Feature Framework file that we saw in the "classic" model, but it uses the _ClientSideComponentId_ attribute to reference the _id_ of the custom extension, and the _ClientSideComponentProperties_ attribute, to configure the custom configuration properties required by the extension.</span></span>

<span data-ttu-id="a6b89-188">Öffnen Sie nun die Datei _package-solution.json_ im Ordner _/config_ der Lösung.</span><span class="sxs-lookup"><span data-stu-id="a6b89-188">Now, open the _package-solution.json_ file under the _/config_ folder of the solution.</span></span> <span data-ttu-id="a6b89-189">In der Datei können Sie sehen, dass ein Verweis auf die _elements.xml_ im Abschnitt _assets_ vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a6b89-189">Within the file you can see that there is a reference to the _elements.xml_ file, within the _assets_ section.</span></span>

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

#### <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="a6b89-190">Aktivieren des CDN im Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="a6b89-190">Enable the CDN in your Office 365 tenant</span></span>
<span data-ttu-id="a6b89-191">Sie müssen die Erweiterung nun in einer Hostingumgebung hosten.</span><span class="sxs-lookup"><span data-stu-id="a6b89-191">Now you need to host the extension in a hosting environment.</span></span> <span data-ttu-id="a6b89-192">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-192">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="a6b89-193">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="a6b89-193">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="a6b89-194">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="a6b89-194">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="a6b89-195">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="a6b89-195">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="a6b89-196">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="a6b89-196">Enable public CDN in the tenant:</span></span>
    
    ```
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="a6b89-197">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-197">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="a6b89-198">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="a6b89-198">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="a6b89-p121">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-p121">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we will create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="a6b89-202">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens _CDN_, und fügen Sie ihr einen Ordner namens _customecb_ hinzu.</span><span class="sxs-lookup"><span data-stu-id="a6b89-202">Create a new document library on your site collection called _CDN_ and add a folder named _customecb_ to it.</span></span>
    
7. <span data-ttu-id="a6b89-203">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="a6b89-203">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="a6b89-204">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen _cdn_ als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="a6b89-204">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of _cdn_ acts as a CDN origin.</span></span>
    
    ```
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="a6b89-205">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="a6b89-205">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
<span data-ttu-id="a6b89-206">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="a6b89-206">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="a6b89-207">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie mit dem Bereitstellen der Erweiterung fortfahren, die anschließend im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="a6b89-207">Final configuration of the origin takes approximately 15 minutes, so we can continue provisioning the extension, which will be hosted from the origin after deployment is completed.</span></span> 

![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

<span data-ttu-id="a6b89-209">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a6b89-209">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="a6b89-210">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="a6b89-210">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

#### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a><span data-ttu-id="a6b89-211">Aktualisieren der Lösungseinstellungen und Veröffentlichen im CDN</span><span class="sxs-lookup"><span data-stu-id="a6b89-211">Update the solution settings and publish it on the CDN</span></span>
<span data-ttu-id="a6b89-212">Sie müssen die Lösung jetzt aktualisieren, damit Sie das gerade erstellte CDN als Hostingumgebung verwenden können. Sie müssen das Lösungsbundle im CDN veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-212">Now, you need to update the solution in order to use the just created CDN as the hosting enviroment and you will need to publish the solution bundle to the CDN.</span></span> <span data-ttu-id="a6b89-213">Gehen Sie hierzu wie nachfolgend beschrieben vor.</span><span class="sxs-lookup"><span data-stu-id="a6b89-213">To accomplish this task, just follow the upcoming steps.</span></span>

1. <span data-ttu-id="a6b89-214">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderliche URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-214">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="a6b89-215">Aktualisieren Sie die Datei _write-manifests.json_ (im Ordner _config_) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="a6b89-215">Update the _write-manifests.json_ file (under the _config_ folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="a6b89-216">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="a6b89-216">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="a6b89-217">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="a6b89-217">The format of the CDN URL is as follows:</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-write-manifest.png)

3. <span data-ttu-id="a6b89-219">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-219">Save your changes.</span></span>

4. <span data-ttu-id="a6b89-220">Führen Sie die folgende Aufgabe aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="a6b89-220">Execute the following task to bundle your solution.</span></span> <span data-ttu-id="a6b89-221">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei _write-manifests.json_ angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="a6b89-221">This executes a release build of your project using the CDN URL specified in the _write-manifests.json_ file.</span></span> <span data-ttu-id="a6b89-222">Die Ausgabe dieses Befehls finden Sie im Ordner _./temp/deploy_.</span><span class="sxs-lookup"><span data-stu-id="a6b89-222">The output of this command is located in the _./temp/deploy_ folder.</span></span> <span data-ttu-id="a6b89-223">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="a6b89-223">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="a6b89-224">Führen Sie die folgende Aufgabe aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-224">Execute the following task to package your solution.</span></span> <span data-ttu-id="a6b89-225">Dieser Befehl erstellt ein Paket namens _spfx-ecb-extension.sppkg_ im Ordner _sharepoint/solution_ und bereitet außerdem die Ressourcen im Ordner _temp/deploy_ für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="a6b89-225">This command creates an _spfx-ecb-extension.sppkg_ package in the _sharepoint/solution_ folder and also prepares the assets in the _temp/deploy_ folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="a6b89-226">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche _Bereitstellen_.</span><span class="sxs-lookup"><span data-stu-id="a6b89-226">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the _Deploy_ button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/spfx-ecb-extension-cdn-address.png)

7. <span data-ttu-id="a6b89-228">Laden Sie die Dateien im Ordner _temp/deploy_ in den Ordner _CDN/customfooter_ hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="a6b89-228">Upload or drag-and-drop the files in the _temp/deploy_ folder to the _CDN/customfooter_ folder created earlier.</span></span>

### <a name="install-and-run-the-solution"></a><span data-ttu-id="a6b89-229">Installieren und Ausführen der Lösung</span><span class="sxs-lookup"><span data-stu-id="a6b89-229">Install and run the solution</span></span>
<span data-ttu-id="a6b89-230"><a name="InstallCommandSet"> </a> Sie können die Lösung jetzt auf jeder modernen Zielwebsite installieren.</span><span class="sxs-lookup"><span data-stu-id="a6b89-230"><a name="InstallCommandSet"> </a> You can now install the solution on any target "modern" site.</span></span>

1. <span data-ttu-id="a6b89-231">Öffnen Sie den Browser, und navigieren Sie zu der gewünschten modernen Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="a6b89-231">Open the browser and navigate to any target "modern" site.</span></span>

2. <span data-ttu-id="a6b89-232">Navigieren Sie zur Seite _Websiteinhalte_, und wählen Sie _App_, um eine neue App hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-232">Go to the _"Site Contents"_ page and select to add a new _App_.</span></span>

3. <span data-ttu-id="a6b89-233">Wählen Sie zum Installieren einer neuen App _Aus Ihrer Organisation_, um die im _AppCatalog_ verfügbaren Lösungen zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-233">Select to install a new app _"From Your Organization"_ to browse the solutions available in the _AppCatalog_.</span></span>

4. <span data-ttu-id="a6b89-234">Wählen Sie die Lösung mit dem Namen _spfx-ecb-extension-client-side-solution_, und installieren Sie sie auf der Zielwebsite.</span><span class="sxs-lookup"><span data-stu-id="a6b89-234">Select the solution called _"spfx-ecb-extension-client-side-solution"_ and istall it on the target site.</span></span>

    ![Hinzufügen einer App-Benutzeroberfläche, um die Lösung einer Website hinzuzufügen](../../../images/spfx-ecb-extension-add-app.png)

5. <span data-ttu-id="a6b89-236">Nachdem die Installation der Anwendung abgeschlossen ist, öffnen Sie die _Documents_-Bibliothek der Website, und sehen Sie sich das funktionsfähige ECB-Menüelement an, indem Sie ein einzelnes Dokument auswählen.</span><span class="sxs-lookup"><span data-stu-id="a6b89-236">Once the application installation will be completed, open the _"Documents"_ library of the site and see the custom ECB menu item in action by selecting a single document.</span></span>

<span data-ttu-id="a6b89-237">Sie können nun Ihr neues benutzerdefiniertes ECB-Menüelement nutzen, das Sie mit den SharePoint-Framework-Erweiterungen erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a6b89-237">Enjoy your new custom ECB menu item built using the SharePoint Framework extensions!</span></span>
