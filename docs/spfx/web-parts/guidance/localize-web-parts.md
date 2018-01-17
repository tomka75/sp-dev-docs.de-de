---
title: Lokalisieren von clientseitigen SharePoint-Framework-Webparts
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 7ea0ef5723102b791f1db98824cc477dd36f4d9f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="localize-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="dcf95-102">Lokalisieren von clientseitigen SharePoint-Framework-Webparts</span><span class="sxs-lookup"><span data-stu-id="dcf95-102">Localize SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="dcf95-p101">Sie können die Darstellung Ihres SharePoint Framework mithilfe des clientseitigen-Webparts erweitern, indem Sie ihn für die verschiedenen Sprachen lokalisieren, die von SharePoint-Benutzern weltweit gesprochen werden. In diesem Artikel lokalisieren Sie einen Webpart für das Gebietsschema Niederländisch (Niederlande), und stellen Sie sicher, dass die lokalisierten Werte ordnungsgemäß angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p101">You can broaden the appeal of your SharePoint Framework client-side web part by localizing it for different languages spoken by SharePoint users all over the world. In this article, you will localize a web part to the Dutch (Netherlands) locale, and verify that the localized values are displayed correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="dcf95-105">Bevor Sie die Schritte in diesem Artikel ausführen, müssen Sie [die Entwicklungsumgebung für Ihr clientseitiges SharePoint-Webpart einrichten](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="dcf95-105">Note: Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="prepare-the-project"></a><span data-ttu-id="dcf95-106">Vorbereiten des Projekts</span><span class="sxs-lookup"><span data-stu-id="dcf95-106">Prepare the project</span></span>

### <a name="create-a-new-project"></a><span data-ttu-id="dcf95-107">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="dcf95-107">Create a new project</span></span>

<span data-ttu-id="dcf95-108">Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-108">Start by creating a new folder for your project.</span></span>

```sh
md react-localization
```

<span data-ttu-id="dcf95-109">Wechseln Sie zum Projektordner.</span><span class="sxs-lookup"><span data-stu-id="dcf95-109">Go to the project folder.</span></span>

```sh
cd react-localization
```

<span data-ttu-id="dcf95-110">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-110">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="dcf95-111">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="dcf95-111">When prompted, enter the following values:</span></span>

- <span data-ttu-id="dcf95-112">**react-localization** als Ihr Lösungsname.</span><span class="sxs-lookup"><span data-stu-id="dcf95-112">**react-localization** as your solution name.</span></span>
- <span data-ttu-id="dcf95-113">**SharePoint Online only (latest)** als Basispaketsatz.</span><span class="sxs-lookup"><span data-stu-id="dcf95-113">**SharePoint Online only (latest)** as the baseline package set.</span></span>
- <span data-ttu-id="dcf95-114">**Use the currecnt folder** als Speicherort für die Dateien.</span><span class="sxs-lookup"><span data-stu-id="dcf95-114">**Use the current folder** for the location to place the files.</span></span>
- <span data-ttu-id="dcf95-115">**y**, um die mandantenweite Bereitstellung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-115">**y** to allow tenant-wide deployment.</span></span>
- <span data-ttu-id="dcf95-116">**WebPart** als den Typ der zu erstellenden Komponente</span><span class="sxs-lookup"><span data-stu-id="dcf95-116">**WebPart** as the type of client-side component to create.</span></span>
- <span data-ttu-id="dcf95-117">**Begrüßung** als Name des Webparts.</span><span class="sxs-lookup"><span data-stu-id="dcf95-117">**Greeting** as your web part name.</span></span>
- <span data-ttu-id="dcf95-118">**Grüßt den Benutzer ** als Beschreibung Ihres Webparts.</span><span class="sxs-lookup"><span data-stu-id="dcf95-118">**Greets the user** as your web part description.</span></span>
- <span data-ttu-id="dcf95-119">**React** als Startpunkt für die Webpart-Erstellung.</span><span class="sxs-lookup"><span data-stu-id="dcf95-119">**React** as the starting point to build the web part.</span></span>

![Der SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/localization-yo-sharepoint.png)

<span data-ttu-id="dcf95-121">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-121">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="dcf95-122">Öffnen Sie dann den Projektordner im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="dcf95-122">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="dcf95-123">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-123">This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Das SharePoint-Framework-Projekt in Visual Studio-Code](../../../images/localization-visual-studio-code.png)

### <a name="replace-the-default-code"></a><span data-ttu-id="dcf95-125">Ersetzen des standardmäßigen Code</span><span class="sxs-lookup"><span data-stu-id="dcf95-125">Replace the default code</span></span>

<span data-ttu-id="dcf95-126">Öffnen Sie im Code-Editor Die Datei **./src/webparts/greeting/GreetingWebPart.ts** und aktualisieren Sie Definition der `IGreetingWebPartProps`-Schnittstelle mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="dcf95-126">In the code editor, open the **./src/webparts/greeting/GreetingWebPart.ts** file and update the definition of the `IGreetingWebPartProps` interface to the following code:</span></span>

```ts
export interface IGreetingWebPartProps {
  greeting: string;
}
```

<span data-ttu-id="dcf95-127">Ändern Sie Als Nächstes in derselben Datei die **GreetingWebPart**-Klasse in:</span><span class="sxs-lookup"><span data-stu-id="dcf95-127">Next, open the ./src/webparts/greeting/GreetingWebPart.ts file and change the GreetingWebPart class to:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {

  public render(): void {
    const element: React.ReactElement<IGreetingProps > = React.createElement(
      Greeting,
      {
        greeting: this.properties.greeting
      }
    );

    ReactDom.render(element, this.domElement);
  }

  protected get dataVersion(): Version {
    return Version.parse('1.0');
  }

  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.DisplayGroupName,
              groupFields: [
                PropertyPaneTextField('greeting', {
                  label: strings.GreetingFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }
}
```

<span data-ttu-id="dcf95-128">Aktualisieren Sie die zentrale React-Komponente, indem Sie die Datei **./src/webparts/greeting/components/Greeting.tsx** öffnen und den Code folgendermaßen ändern:</span><span class="sxs-lookup"><span data-stu-id="dcf95-128">Update the main React component by opening the **./src/webparts/greeting/components/Greeting.tsx** file and changing its code to:</span></span>

```ts
import * as React from 'react';
import styles from './Greeting.module.scss';
import { IGreetingProps } from './IGreetingProps';
import { escape } from '@microsoft/sp-lodash-subset';

export default class Greeting extends React.Component<IGreetingProps, {}> {
  public render(): JSX.Element {
    return (
      <div className={styles.greeting}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className='ms-font-xl ms-fontColor-white'>
                Welcome to SharePoint!
              </span>
              <p className='ms-font-l ms-fontColor-white'>
                Customize SharePoint experiences using Web Parts.
              </p>
              <p className='ms-font-l ms-fontColor-white'>
                {escape(this.props.greeting)}
              </p>
              <a href="https://aka.ms/spfx" className={styles.button}>
                <span className={styles.label}>Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

<span data-ttu-id="dcf95-129">Aktualisieren Sie die Schnittstelle der zentralen React-Komponente, indem Sie die Datei **./src/webparts/greeting/components/IGreetingProps.tsx** öffnen und den Code folgendermaßen ändern:</span><span class="sxs-lookup"><span data-stu-id="dcf95-129">Update the main React component interface by opening the **./src/webparts/greeting/components/IGreetingProps.tsx** file and changing its code to:</span></span>

```tsx
import { IGreetingWebPartProps } from '../GreetingWebPart';

export interface IGreetingProps extends IGreetingWebPartProps {
}
```

<span data-ttu-id="dcf95-130">Aktualisieren Sie die Lokalisierungsdatei mit den TypeScript-Typdefinitionen, indem Sie die Datei **./src/webparts/greeting/loc/mystrings.d.ts** öffnen und den Code folgendermaßen ändern:</span><span class="sxs-lookup"><span data-stu-id="dcf95-130">Update the localization TypeScript type definition file by opening the **./src/webparts/greeting/loc/mystrings.d.ts** file and changing its code to:</span></span>

```ts
declare interface IGreetingWebPartStrings {
  PropertyPaneDescription: string;
  DisplayGroupName: string;
  GreetingFieldLabel: string;
}

declare module 'GreetingWebPartStrings' {
  const strings: IGreetingWebPartStrings;
  export = strings;
}
```

<span data-ttu-id="dcf95-131">Aktualisieren Sie die US-englische Gebietsschema-Datei durch Öffnen der **./src/webparts/greeting/loc/en-us.js**-Datei und ändern Sie den zugehörigen Code folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-131">Update the US English locale file by opening the **./src/webparts/greeting/loc/en-us.js** file and changing its code to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Greeting web part configuration",
    "DisplayGroupName": "Display",
    "GreetingFieldLabel": "Greeting to show in the web part"
  }
});
```

<span data-ttu-id="dcf95-132">Aktualisieren Sie im Webpart-Manifest den Standardwert für die **greeting**-Eigenschaft durch Öffnen der **./src/webparts/greeting/GreetingWebPart.manifest.json**-Datei und ändern Sie den **Eigenschaften**-Abschnitt folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-132">In the web part manifest update the default value of the **greeting** property by opening the **./src/webparts/greeting/GreetingWebPart.manifest.json** file and changing the **properties** section to:</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
    "group": { "default": "Other" },
    "title": { "default": "Greeting" },
    "description": { "default": "Greets the user" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "greeting": "Hello"
    }
  }]
}
```

<span data-ttu-id="dcf95-133">Stellen Sie sicher, dass Sie alle Änderungen ordnungsgemäß angewendet haben, indem Sie folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-133">Verify that you have applied all changes correctly by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="dcf95-134">Fügen Sie in der SharePoint-Worbench fügen den Webpart zu der Seite hinzu, und öffnen Sie seine Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="dcf95-134">In the SharePoint workbench add the web part to the page and open its configuration.</span></span>

![Greeting-Webpart mit geöffnetem Eigenschaftbereich zur Seite hinzugefügt](../../../images/localization-initial-changes.png)

## <a name="localize-the-web-part-manifest"></a><span data-ttu-id="dcf95-136">Lokalisieren des Webpart-Manifests</span><span class="sxs-lookup"><span data-stu-id="dcf95-136">Localize the web part manifest</span></span>

<span data-ttu-id="dcf95-p103">Jeder clientseitige Webpart des SharePoint Framework besteht aus Code und einem Manifest. Das Manifest enthält Informationen über den Webpart, wie z. B. den Titel, die Beschreibung und das Symbol. Wenn Sie einen Webpart zu der Seite hinzufügen, werden den Benutzern die Informationen aus dem Webpart-Manifest angezeigt. Mithilfe dieser Informationen können die Benutzer entscheiden, ob es sich bei dem Webpart um den gesuchten handelt. Das Angeben eines Titels und einer Beschreibung, die die Funktionalität des Webparts ordnungsgemäß widerspiegeln, ist sehr wichtig, wenn Ihr Webpart verwendet werden soll. Wenn der Webpart auf nicht-englischen Websites verwendet werden soll, kann die Benutzererfahrung durch die Lokalisierung der Metadaten noch weiter optimiert werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p103">Every SharePoint Framework client-side web part consists of code, and a manifest. The manifest provides information about the web part such as its title, description, and icon. When adding a web part to the page, the information from the web part manifest is displayed to users. Using this information users decide if the web part is the one that they are looking for. Providing a title and description that correctly reflect the web part's functionality is essential if you want your web part to be used. If your web part will be used in non-English sites, then localizing its metadata can improve the user experience even further.</span></span>

<span data-ttu-id="dcf95-143">Einige Eigenschaften, die im Webpart-Manifest definiert sind, wie z. B. Titel oder Beschreibung, unterstützen das Angeben lokalisierter Werte.</span><span class="sxs-lookup"><span data-stu-id="dcf95-143">Some properties defined in the web part manifest, such as title or description, support specifying localized values.</span></span> <span data-ttu-id="dcf95-144">Die vollständige Liste aller Webpart-Manifesteigenschaften, die eine Lokalisierung unterstützen, finden Sie im Artikel [Vereinfachen des Hinzufügens von Webparts mit vorkonfigurierten Einträgen](./simplify-adding-web-parts-with-preconfigured-entries.md#properties-of-a-preconfiguredentries-array-item).</span><span class="sxs-lookup"><span data-stu-id="dcf95-144">For the complete list of all web part manifest properties that support localization read the [Simplify adding web parts with preconfigured entries](./simplify-adding-web-parts-with-preconfigured-entries.md#properties-of-a-preconfiguredentries-array-item) article.</span></span> <span data-ttu-id="dcf95-145">Eigenschaften, die die Lokalisierung unterstützen, sind vom Typ **ILocalizedString**.</span><span class="sxs-lookup"><span data-stu-id="dcf95-145">Properties that support localization are of type **ILocalizedString**.</span></span> <span data-ttu-id="dcf95-146">Jede lokalisierte Zeichenfolge muss mindestens den Standardwert und optional Werte für andere Gebietsschemas angeben.</span><span class="sxs-lookup"><span data-stu-id="dcf95-146">Each localized string must specify at least the default value and optionally values for other locales.</span></span>

### <a name="add-localized-values-for-title-description-and-group-name"></a><span data-ttu-id="dcf95-147">Hinzufügen lokalisierter Werte für Titel, Beschreibung und Gruppenname</span><span class="sxs-lookup"><span data-stu-id="dcf95-147">Add localized values for title, description, and group name</span></span>

<span data-ttu-id="dcf95-148">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="dcf95-148">In the code editor open the **./src/webparts/greeting/GreetingWebPart.manifest.json file, and remove the greeting property from the properties** property:</span></span> <span data-ttu-id="dcf95-149">Fügen Sie im **PreconfiguredEntries**-Array Übersetzungen für die Eigenschaften **title**, **description** und **group** in Niederländisch (Niederlande) hinzu, indem Sie den Code folgendermaßen ändern:</span><span class="sxs-lookup"><span data-stu-id="dcf95-149">In the code editor open the ./src/webparts/greeting/GreetingWebPart.manifest.json file. In the **preconfiguredEntries** array add translations for the **title**, **description**, and **group** properties in Dutch (Netherlands), by changing the code to:</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
    "group": { "default": "Other", "nl-nl": "Anders" },
    "title": { "default": "Greeting", "nl-nl": "Begroeting" },
    "description": { "default": "Greets the user", "nl-nl": "Begroet de gebruiker" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "greeting": "Hello"
    }
  }]
}
```

<span data-ttu-id="dcf95-150">Führen Sie den folgenden Befehl aus, um sicherzustellen, dass das Projekt ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="dcf95-150">Run the following command to verify that the project is working:</span></span>

```sh
gulp serve
```

> [!NOTE] 
> <span data-ttu-id="dcf95-151">Leider unterstützt die SharePoint-Workbench derzeit keine Vorschau für die lokalisierten Werte aus dem Webpart-Manifest.</span><span class="sxs-lookup"><span data-stu-id="dcf95-151">Note: Unfortunately, the SharePoint workbench doesn't currently support previewing the localized values from the web part manifest. It always uses the default translation.</span></span> <span data-ttu-id="dcf95-152">Es wird immer die Standard-Übersetzung verwendet.</span><span class="sxs-lookup"><span data-stu-id="dcf95-152">It always uses the default translation.</span></span>

## <a name="localize-the-web-part-property-pane"></a><span data-ttu-id="dcf95-153">Lokalisieren des Webpart-Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="dcf95-153">Localize the web part property pane</span></span>

<span data-ttu-id="dcf95-p107">Wenn Sie häufig mit Webparts arbeiten, müssen Benutzer Sie häufig entsprechend ihrer spezifischen Anforderungen konfigurieren. Durch das Angeben aussagekräftiger Bezeichnungen für die verschiedenen Konfigurationen wird die Nutzbarkeit des Webparts verbessert und die Anzahl von Support-Anfragen von Benutzer hinsichtlich Fragen zur Konfiguration von Webparts verringert.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p107">When working with web parts users often need to configure it for their specific needs. Providing descriptive labels for the different configuration settings improves the usability of the web part, and decreases the number of support requests from users for help configuring web parts.</span></span>

<span data-ttu-id="dcf95-p108">Der Webpart-Eigenschaftenbereich besteht aus Abschnitten. Jeder Abschnitt besitzt eine Überschrift und ein oder mehrere Steuerelemente, sodass Benutzer den Webpart konfigurieren können. Jedes dieser Steuerelemente enthält eine Beschriftung, die dessen Zweck beschreibt. Standardmäßig laden Webparts die Zeichenfolge-Beschriftungen aus einer JavaScript-Ressourcendatei. Wenn Sie klassische-Webparts mit vollständig vertrauenswürdigen Lösungen erstellt haben, ähnen sie RESX-Ressourcendateien. Es ist nicht erforderlich, diese Ressourcendateien zu verwenden, und Sie können die Zeichenfolgen direkt in den Code einbinden. Es wird jedoch dringend empfohlen, die Ressourcendateien zu verwenden. Der kleine zeitliche Mehraufwand wiegt den Aufwand auf, der zum Extrahieren aller Beschriftungen erforderlich ist, um den Webpart zu einem späteren Zeitpunkt zu übersetzen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p108">The web part property pane consists of sections. Each section has a header and one or more controls allowing users to configure the web part. Each of these controls contains a label that describes its purpose. By default, web parts load the string labels from a JavaScript resource file. If you've built classic web parts with full-trust solutions, they resemble .resx resource files. It's not required to use these resource files and you could include the strings directly in code. However, it's highly recommended that you use resource files. The little additional overhead they add outweighs the effort required to extract all labels afterwards should you need to translate the web part later on.</span></span>

<span data-ttu-id="dcf95-164">Die Lokalisierungsdateien, die durch den Webpart verwendet werden, sind im **./src/webparts/greeting/loc**-Ordner gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dcf95-164">The localization files used by the web part are stored in the **./src/webparts/greeting/loc** folder.</span></span>

![Die Lokalisierungsdateien, die von einem clientseitigen SharePoint-Framework-Webpart verwendet werden, sind im Visual Studio-Code hervorgehoben.](../../../images/localization-loc-folder.png)

<span data-ttu-id="dcf95-166">Der **loc**-Ordner enthält eine TypeScript-Typ-Definitionsdatei (**./src/webpart/greeting/loc/mystrings.d.ts**), die TypeScript mitteilt, welche verschiedenen Zeichenfolgen in den lokalisierten Dateien enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="dcf95-166">The **loc** folder contains a TypeScript type definition file (**./src/webpart/greeting/loc/mystrings.d.ts**) that informs TypeScript of the different strings included in the localized files.</span></span> <span data-ttu-id="dcf95-167">Anhand der Informationen aus dieser Datei kann der Code-Editor Ihnen IntelliSense bereitstellen, wenn Sie im Code mit Zeichenfolgen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="dcf95-167">Using the information from this file, your code editor can provide you with IntelliSense when working with strings in code.</span></span> <span data-ttu-id="dcf95-168">Darüber hinaus kann TypeScript beim Erstellen des Projekts sicherstellen, dass Sie auf keine Zeichenfolge verweisen, die noch nicht definiert wurde.</span><span class="sxs-lookup"><span data-stu-id="dcf95-168">Additionally, while building your project, TypeScript can verify that you're not referring to a string that hasn't been defined.</span></span>

![IntelliSense für lokalisierte Zeichenfolgen in Visual Studio-Code](../../../images/localization-intellisense.png)

<span data-ttu-id="dcf95-170">Für jedes von Ihrem Webpart unterstützte Gebietsschema gibt es eine einfache JavaScript-Datei (nicht TypeScript) in Kleinschreibung nach das Gebietsschema (z. B. **en-us.js**), die die übersetzten Zeichenfolgen enthält.</span><span class="sxs-lookup"><span data-stu-id="dcf95-170">For each locale supported by your web part, there is also a plain JavaScript file (not TypeScript) named in lowercase after the locale (for example **en-us.js**) containing the translated strings.</span></span>

![Standard-Lokalisierungsdatei mit einem neuen SharePoint Framework-Projekt](../../../images/localization-standard-locale-file.png)

> <span data-ttu-id="dcf95-172">**Wichtig:** Sie sollten zusätzlich sicherstellen, dass für alle in der TypeScript-Typ-Definitionsdatei für die Lokalisierung angegebenen Schlüssel Übersetzungen in allen Lokalisierung JavaScript-Dateien vorliegen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-172">**Important:** You should pay extra attention to verifying that all keys specified in the TypeScript type definition file for localization have translations in all localization JavaScript files.</span></span>

<span data-ttu-id="dcf95-173">en-US ist das standardmäßig vom SharePoint-Framework verwendete Gebietsschema.</span><span class="sxs-lookup"><span data-stu-id="dcf95-173">en-US is the default locale used by the SharePoint Framework.</span></span> <span data-ttu-id="dcf95-174">Wenn der Webpart auf einer Website mit einem Gebietsschema verwendet wird, das durch den Webpart nicht unterstützt wird, verwendet das SharePoint-Framework en-US als Standardgebietsschema.</span><span class="sxs-lookup"><span data-stu-id="dcf95-174">If your web part is used on a site using a locale not supported by your web part, the SharePoint Framework will use en-US as the default locale.</span></span> <span data-ttu-id="dcf95-175">Sie können dieses Verhalten umgehen, indem Sie eine Gebietsschema-Datei mit dem Namen **default.js** mit der Übersetzung in Ihrer bevorzugten Sprache erstellen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-175">You can override this behavior by creating a locale file named **default.js** with the translations in your preferred language.</span></span> <span data-ttu-id="dcf95-176">Während der Name **default.js** nicht der Gebietsschema-Namenskonvention folgt, signalisiert er dem SharePoint-Framework-Erstellvorgang, diese spezielle Gebietsschema-Datei als Fallback-Gebietsschema anstelle des Standard-US-Englisch-Gebietsschemas zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-176">While the name **default.js** doesn't follow the locale naming convention, it signals to the SharePoint Framework build process to use that particular locale file as the fallback locale instead of the standard US English locale.</span></span>

### <a name="add-localized-values-for-web-part-property-pane-strings"></a><span data-ttu-id="dcf95-177">Hinzufügen von lokalisierten Werten für Zeichenfolgen für den Webparteigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="dcf95-177">Add localized values for web part property pane strings</span></span>

<span data-ttu-id="dcf95-178">Erstellen Sie im Ordner **./src/webparts/greetings/loc** eine neue Datei mit dem Namen **IListInfo.ts**, und geben Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="dcf95-178">In the **./src/webparts/greetings/loc** folder create new file named **nl-nl.js** and enter the following code:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
    "DisplayGroupName": "Weergave",
    "GreetingFieldLabel": "Begroeting die in het webonderdeel getoond wordt"
  }
});
```

<span data-ttu-id="dcf95-179">Stellen Sie sicher, dass die Schlüssel in der TypeScript-Typ-Definitionsdatei für die Lokalisierung dem Inhalt der Gebietsschemadateien für US-Englisch und Niederländisch entspricht.</span><span class="sxs-lookup"><span data-stu-id="dcf95-179">Verify that the keys in the TypeScript type definition file for localization match the contents of the locale files for US English and Dutch (Netherlands).</span></span>

![Die TypeScript-Typ-Definitionsdatei für die Lokalisierung und die Gebietsschemadateien für US-Englisch und Niederländisch (Niederlande) werden im Visual Studio-Code nebeneinander geöffnet](../../../images/localization-keys-comparison.png)

### <a name="verify-the-localized-web-part-property-pane-strings"></a><span data-ttu-id="dcf95-181">Überprüfen der lokalisierten Zeichenfolgen für den Webparteigenschaftenbereich</span><span class="sxs-lookup"><span data-stu-id="dcf95-181">Verify the localized web part property pane strings</span></span>

<span data-ttu-id="dcf95-182">Beim Testen der Webparts anhand der gehosteten Version von SharePoint-Workbench oder Team-Websites mit einem Entwickler-Mandanten des Gebietsschemas der Kontext-Website, die durch die **spPageContextInfo.currentUICultureName**-Eigenschaft ausgedrückt werden, werden als Standard-Gebietsschema verwendet.</span><span class="sxs-lookup"><span data-stu-id="dcf95-182">When testing web parts using the hosted version of the SharePoint workbench or team sites on a developer tenant the locale of the context site expressed by the **spPageContextInfo.currentUICultureName** property is used as the default locale. When testing web parts using the local SharePoint workbench, the SharePoint Framework uses by default the en-US locale to display web part property pane strings. There are two ways in which you can test the values from other locales supported by your web part.</span></span> <span data-ttu-id="dcf95-183">Beim Testen der Webparts unter Verwendung der lokalen SharePoint-Workbench verwendet SharePoint-Framework standardmäßig das Gebietsschema en-US, um die Zeichenfolgen für den Webparteigenschaftenbereich anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-183">When testing web parts using the local SharePoint workbench, the SharePoint Framework uses by default the en-US locale to display web part property pane strings.</span></span> <span data-ttu-id="dcf95-184">Es gibt zwei Möglichkeiten, mit denen Sie die Werte aus den anderen Gebietsschemas testen können, die von Ihrem Webpart unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-184">There are two ways in which you can test the values from other locales supported by your web part.</span></span>

#### <a name="specify-the-locale-to-be-tested-in-the-project-configuration"></a><span data-ttu-id="dcf95-185">Angeben des zu testenden Gebietsschemas in der Konfiguration des Projekts</span><span class="sxs-lookup"><span data-stu-id="dcf95-185">Specify the locale to be tested in the project configuration</span></span>

<span data-ttu-id="dcf95-186">Eine Möglichkeit zum Angeben des Gebietsschemas, das in der SharePoint-Workbench getestet werden soll, ist das Bearbeiten der Konfiguration des Projekts.</span><span class="sxs-lookup"><span data-stu-id="dcf95-186">One way to specify the locale to be tested in the SharePoint workbench is by editing the project configuration.</span></span> <span data-ttu-id="dcf95-187">Dieser Ansatz ist hilfreich, wenn Sie und Ihre Teammitglieder für längere Zeit mit einem anderen Gebietsschema arbeiten oder Sie einen Webpart erstellen, der US-Englisch unterstützt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-187">One way to specify the locale to be tested in the SharePoint workbench is by editing the project configuration. This approach is useful if you and your team members are working with a locale for a longer period of time or if you're building a web part that doesn't support US English. In the code editor open the ./config/write-manifests.json file and change its code to:</span></span> <span data-ttu-id="dcf95-188">Öffnen Sie im Code-Editor die **./config/write-manifests.json**-Datei und ändern Sie den Code folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-188">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file and change its code to:</span></span>

```json
{
  "cdnBasePath": "<!-- PATH TO CDN -->",
  "debugLocale": "nl-nl"
}
```

<span data-ttu-id="dcf95-189">Starten Sie die SharePoint-Workbench, indem Sie folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-189">Start the SharePoint workbench by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="dcf95-190">Wenn Sie den Webpart zu der Seite hinzufügen, und die Konfiguration öffnen, werden Ihnen die Zeichenfolgen für den Webparteigenschaftenbereich in Niederländisch (Niederlande) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-190">When you add the web part to the page and open its configuration you will see the strings in the web part property pane displayed in Dutch (Netherlands).</span></span>

![In Niederländisch (Niederlande) angezeigte Webparteigenschaftenbereich-Zeichenfolge](../../../images/localization-property-pane-nl-nl.png)

#### <a name="specify-the-locale-to-be-tested-using-the-command-line-argument"></a><span data-ttu-id="dcf95-192">Geben Sie das zu testende Gebietsschema mit dem Befehlszeilen-Argument an</span><span class="sxs-lookup"><span data-stu-id="dcf95-192">Specify the locale to be tested using the command line argument</span></span>

<span data-ttu-id="dcf95-p113">Eine andere Möglichkeit zum Angeben des von der lokalen SharePoint-Worbench zu verwendenden Gebietsschemas ist das Angeben eines Arguments für die Gulp-Aufgabe. Starten Sie die SharePoint-Workbench, indem Sie folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-p113">Another way to specify the locale to be used by the local SharePoint workbench is to specify it as an argument for the gulp task. Start the SharePoint workbench by running the following command:</span></span>

```sh
gulp serve --locale=nl-nl
```

<span data-ttu-id="dcf95-195">Noch mal, wenn Sie die Konfiguration Ihres Webparts öffnen, können Sie sehen, dass alle Eigenschaftenbereich-Zeichenfolgen in Niederländisch (Niederlande) angezeigt, statt in Standard-US-Englisch.</span><span class="sxs-lookup"><span data-stu-id="dcf95-195">Once again, when you open your web part's configuration you will see that all property pane strings are displayed in Dutch (Netherlands) rather than the default US English.</span></span>

![In Niederländisch (Niederlande) angezeigte Webparteigenschaftenbereich-Zeichenfolge](../../../images/localization-property-pane-nl-nl.png)

## <a name="localize-web-part-contents"></a><span data-ttu-id="dcf95-197">Lokalisieren der Webpart-Inhalte</span><span class="sxs-lookup"><span data-stu-id="dcf95-197">Localize web part contents</span></span>

<span data-ttu-id="dcf95-p114">Genauso wie Sie Webparteigenschaftenbereich-Zeichenfolgen lokalisieren, sollten Sie alle vom Webpart im Text angezeigten Zeichenfolgen lokalisieren. Sie können den gleichen Ansatz verwenden, den Sie beim Lokalisieren der Zeichenfolgen für den Webparteigenschaftenbereich verwendet haben. Fügen Sie für jede zu lokalisierende Zeichenfolge in der TypeScript-Definitionsdatei einen Schlüssel hinzu und übersetzen Sie die Zeichenfolge in die unterstützten Gebietsschemas in der entsprechenden JavaScript-Datei des Gebietsschemas.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p114">The same way you localize web part property pane strings, you should localize all strings displayed by the web part in its body. You can use the same approach that you use when localizing web part property pane strings. For every string to be localized, add a key in the localization TypeScript definition file, and then translate the string to each of the supported locales in the corresponding locale JavaScript file.</span></span>

### <a name="globalize-the-web-part-strings"></a><span data-ttu-id="dcf95-201">Globalisieren der Webpartzeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="dcf95-201">Globalize the web part strings</span></span>

<span data-ttu-id="dcf95-202">Bei dem mit dem erstellten SharePoint-Framework-Projekt angegebenen Standard-Webpart sind die Zeichenfolgen in den Code eingebunden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-202">The default web part provided with the scaffolded SharePoint Framework project has its strings embedded in the code.</span></span> <span data-ttu-id="dcf95-203">Bevor Sie diese Zeichenfolgen lokalisieren, müssen Sie sie durch Verweise auf die lokalisierten Zeichenfolgen ersetzen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-203">Before you can localize these strings you have to replace them with references to the localized strings.</span></span> <span data-ttu-id="dcf95-204">Dieser Vorgang wird oftmals als **Globalisierung** oder **Internationalisierung** (oder **kurz i18n**) bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="dcf95-204">This process is often referred to as **globalization** or **internationalization** (or **i18n** for short).</span></span>

<span data-ttu-id="dcf95-205">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/components/Greetings.tsx**.</span><span class="sxs-lookup"><span data-stu-id="dcf95-205">In the code editor, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and paste the following code:</span></span> <span data-ttu-id="dcf95-206">Fügen Sie im oberen Bereich der Datei direkt nach der letzten `import`-Anweisung einen Verweis auf die lokalisierten Zeichenfolgen zu:</span><span class="sxs-lookup"><span data-stu-id="dcf95-206">In the code editor, open the ./src/webparts/greeting/components/Greetings.tsx file. In the top section of the file, directly after the last `import` statement, add a reference to the localized strings:</span></span>

```ts
import * as strings from 'GreetingWebPartStrings';
```

<span data-ttu-id="dcf95-207">Im nächsten Schritt ersetzen Sie den Inhalt der Klasse **Greeting** durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="dcf95-207">Next, replace the contents of the **Greeting** class with the following code:</span></span>

```ts
// ...
export default class Greeting extends React.Component<IGreetingProps, {}> {
  public render(): JSX.Element {
    return (
      <div className={styles.greeting}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className='ms-font-xl ms-fontColor-white'>
                Welcome to SharePoint!
              </span>
              <p className='ms-font-l ms-fontColor-white'>
                Customize SharePoint experiences using Web Parts.
              </p>
              <p className='ms-font-l ms-fontColor-white'>
                {escape(this.props.greeting)}
              </p>
              <a href="https://aka.ms/spfx" className={styles.button}>
                <span className={styles.label}>{strings.LearnMoreButtonLabel}</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

### <a name="add-the-new-string-to-the-localization-typescript-type-definition-file"></a><span data-ttu-id="dcf95-208">Hinzufügen der neuen Zeichenfolge zur Lokalisierungsdatei mit den TypeScript-Typdefinitionen</span><span class="sxs-lookup"><span data-stu-id="dcf95-208">Add the new string to the localization TypeScript type definition file</span></span>

<span data-ttu-id="dcf95-209">Nach dem Ersetzen der Zeichenfolge durch einen Verweis besteht der nächste Schritt darin, die Zeichenfolge mit den Lokalisierungsdateien zu ersetzen, die vom Webpart verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-209">Having replaced the string with a reference, the next step is to add that string to the localization files used by the web part. In the code editor open the ./src/webparts/greetings/loc/mystrings.d.ts file, and change its code to:</span></span> <span data-ttu-id="dcf95-210">Öffnen Sie im Code-Editor die Datei **./src/webparts/greetings/loc/mystrings.d.ts**, und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dcf95-210">In the code editor, open the **./src/webparts/gallery/loc/mystrings.d.ts** file. Change its code to:</span></span>

```ts
declare interface IGreetingWebPartStrings {
  PropertyPaneDescription: string;
  DisplayGroupName: string;
  GreetingFieldLabel: string;
  LearnMoreButtonLabel: string;
}

declare module 'greetingStrings' {
  const strings: IGreetingWebPartStrings;
  export = strings;
}

```

### <a name="add-localized-values-for-the-new-string"></a><span data-ttu-id="dcf95-211">Hinzufügen von lokalisierten Werte für die neue Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="dcf95-211">Add localized values for the new string</span></span>

<span data-ttu-id="dcf95-212">Der letzte Schritt besteht darin, die lokalisierten Versionen für die neue Zeichenfolge in allen vom Webpart unterstützten Gebietsschemas bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-212">The last step is to provide localized versions for the new string in all locales supported by the web part. In the code editor, open the ./src/webparts/greeting/loc/en-us.js file and change its code to:</span></span> <span data-ttu-id="dcf95-213">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/loc/en-us.js**, und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dcf95-213">In the code editor, open the **./src/webparts/greeting/loc/en-us.js** file and change its code to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Greeting web part configuration",
    "DisplayGroupName": "Display",
    "GreetingFieldLabel": "Greeting to show in the web part",
    "LearnMoreButtonLabel": "Learn more"
  }
});
```

<span data-ttu-id="dcf95-214">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/loc/nl-nl.js**, und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dcf95-214">Next, open the **./src/webparts/greeting/loc/nl-nl.js** file and change its code to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
    "DisplayGroupName": "Weergave",
    "GreetingFieldLabel": "Begroeting die in het webonderdeel getoond wordt",
    "LearnMoreButtonLabel": "Meer informatie"
  }
});
```

<span data-ttu-id="dcf95-215">Bestätigen Sie, dass die übersetzte Zeichenfolge richtig angezeigt wird, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-215">Confirm that the translated string is correctly displayed by running the following command:</span></span>

```sh
gulp serve --locale=nl-nl
```

![Die Bezeichnung der Schaltfläche „Weitere Informationen“ wird in Niederländisch (Niederlande) angezeigt statt in Standard-US-Englisch](../../../images/localization-learn-more-nl-nl.png)

## <a name="improve-globalizing-and-localizing-web-parts-using-pseudo-locales"></a><span data-ttu-id="dcf95-217">Verbessern der Globalisierung und Lokalisierung von Pseudogebietsschemas mit Webparts</span><span class="sxs-lookup"><span data-stu-id="dcf95-217">Improve globalizing and localizing web parts using pseudo-locales</span></span>

<span data-ttu-id="dcf95-p119">Die Lokalisierung bietet beim Erstellen von Webparts klare Vorteile, wird jedoch manchmal von Entwicklern leicht übersehen. Oftmals erfolgen Übersetzungen in andere Gebietsschemas zu einem späteren Zeitpunkt im Projekt und es ist schwierig für Tester, sicherzustellen, dass der gesamte Code die unterschiedlichen Gebietsschemas korrekt unterstützt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p119">Using localization when building web parts offers clear benefits but is also something that developers overlook easily. Often, translations to other locales are provided later in the project and it's hard for testers to verify that all code will properly support the different locales.</span></span>

<span data-ttu-id="dcf95-p120">Die gleichen Wörter in anderen Gebietsschemas weisen unterschiedliche Längen auf. Beispielsweise kann der gleiche Satz bei der Übersetzung von Englisch in Deutsch oder Niederländisch übersetzt 35 % länger werden. Wenn nicht alle Übersetzungen von vornherein verfügbar sind, ist es für Entwickler und Designer schwierig, sicherzustellen, dass die Benutzeroberfläche ordnungsgemäß längere Zeichenfolgen aufnehmen kann.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p120">The same words in different locales have different lengths. For example, the same sentence translated from English to German or Dutch can become 35% longer. Without all translations available up front, it's hard for developers and designers to ensure that the user interface can properly accommodate longer strings.</span></span>

<span data-ttu-id="dcf95-p121">In einigen Sprachen werden Sonderzeichen verwendet, die über den Standard-ASCII-Zeichensatz hinaus gehen. Wenn Designer eine nicht standardmäßige Schriftart verwenden, ist es möglich, dass die Schriftart einige Sonderzeichen nicht ordnungsgemäß unterstützt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p121">Some languages use special characters beyond the standard ASCII character set. If designers use a non-standard font, it is possible that the font doesn't properly support some special characters.</span></span>

<span data-ttu-id="dcf95-p122">Diese Probleme zu einem späten Zeitpunkt im Projekt herauszufinden, führt wahrscheinlich zu Verzögerungen und teuren Korrekturen. Mit dem SharePoint Framework können Entwickler Pseudogebietsschemas verwenden, um diese Probleme während der Erstellung von Webparts zu beheben.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p122">Finding out about all these issues late in the project will likely lead to delays and costly fixes. The SharePoint Framework allows developers to use pseudo-locales to address these issues while building web parts.</span></span>

> <span data-ttu-id="dcf95-227">**Was sind Pseudogebietsschemas?**</span><span class="sxs-lookup"><span data-stu-id="dcf95-227">**What are pseudo-locales?**</span></span> <span data-ttu-id="dcf95-228">Pseudogebietsschemas sind Gebietsschemas, die entwickelt wurden, um die Software auf die Unterstützung der verschiedenen Aspekte des Lokalisierungsprozesses zu testen, z. B. Unterstützung für Sonderzeichen, Rechts-nach-links-Sprachen oder zum Unterbringen von längeren Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-228">What are pseudo-locales? Pseudo-locales are locales designed to test software for proper support of the different aspects of the localization process such as support for special characters, right-to-left languages, or accommodating longer strings in the user interface.</span></span>

### <a name="add-the-base-pseudo-locale"></a><span data-ttu-id="dcf95-229">Hinzufügen des Basis-Pseudogebietsschemas</span><span class="sxs-lookup"><span data-stu-id="dcf95-229">Add the base pseudo-locale</span></span>

<span data-ttu-id="dcf95-230">Erstellen Sie im Ordner **./src/webparts/greeting/loc** eine neue Datei mit dem Namen **qps-ploc.js** und fügen Sie folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="dcf95-230">In the **./src/webparts/greeting/loc** folder, add a new file named **qps-ploc.js** and paste the following code:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "[!!! Gřèèƭïñϱ ωèβ ƥářƭ çôñƒïϱúřáƭïôñ ℓôřè₥ ïƥƨú !!!]",
    "DisplayGroupName": "[!!! Ðïƨƥℓá¥ ℓ !!!]",
    "GreetingFieldLabel": "[!!! Gřèèƭïñϱ ƭô ƨλôω ïñ ƭλè ωèβ ƥářƭ ℓôřè₥ ïƥƨú !!!]",
    "LearnMoreButtonLabel": "[!!! £èářñ ₥ôřè ℓôř !!!]"
  }
});
```

> <span data-ttu-id="dcf95-231">**Tipp:** Sie können die US-englischen Zeichenfolgen unter [(http://www.pseudolocalize.com)](http://www.pseudolocalize.com) in die entsprechenden Basis-Pseudogebietsschema-Äquivalente konvertieren. Durch eine Erhöhung der Länge der generierten Zeichenfolge von 35 % sollten Sie die Länge der übersetzten Zeichenfolgen in längere Gebietsschemas wie z. B. Deutsch oder Niederländisch simulieren können.</span><span class="sxs-lookup"><span data-stu-id="dcf95-231">**Tip:** you can convert US English strings to their base pseudo-locale equivalent at [(http://www.pseudolocalize.com)](http://www.pseudolocalize.com). By increasing the length of the generated string with 35% you should be able to simulate the length of strings translated to longer locales such as German or Dutch. Additionally, by surrounding the translations with brackets and exclamation marks you can more easily see if the whole string is displayed on the screen.</span></span> <span data-ttu-id="dcf95-232">Durch das Umschließen der Übersetzungen mit Klammern und Ausrufezeichen können Sie leichter sehen, ob die gesamte Zeichenfolge auf dem Bildschirm angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="dcf95-232">Additionally, by surrounding the translations with brackets and exclamation marks you can more easily see if the whole string is displayed on the screen.</span></span>

<span data-ttu-id="dcf95-233">Testen Sie das Projekt mit dem Basis-Pseudogebietsschema, indem Sie folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-233">Test the project using the base pseudo-locale by running the following command:</span></span>

```sh
gulp serve --locale=qps-ploc
```

<span data-ttu-id="dcf95-234">Nachdem Sie den Webpart zu der Seite hinzugefügt haben, können Sie schnell feststellen, dass zwei Zeichenfolgen im Textkörper des Webparts vorhanden sind, die nicht internationalisiert wurden und weiterhin in US-Englisch statt im Basis-Pseudogebietsschema angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-234">After adding the web part to the page, you can quickly see that there are two strings in the web part body that have not been internationalized and are still displayed in US English rather than in the base pseudo-locale.</span></span>

![Zwei Zeichenfolgen im Textkörper des Webparts werden in US-Englisch angezeigt, obwohl der Test mit dem Basis-Pseudogebietsschema erfolgt](../../../images/localization-web-part-body-qps-ploc.png)

<span data-ttu-id="dcf95-236">Wenn Sie den Eigenschaftenbereich des Webparts öffnen, können Sie feststellen, dass alle Zeichenfolgen und Sonderzeichen ordnungsgemäß angezeigt werden und in den verfügbaren Raum passen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-236">If you open the web part property pane, you can confirm that all strings and their special characters are displayed properly and that they fit in the available space correctly.</span></span>

![Geöffneter Webpart-Eigenschaftenbereich beim Testen des Webparts in der lokalen Workbench mit dem Basis-Pseudogebietsschema](../../../images/localization-web-part-property-pane-qps-ploc.png)

## <a name="localize-web-part-settings-values"></a><span data-ttu-id="dcf95-238">Lokalisierung der Webpart-Einstellungswerte</span><span class="sxs-lookup"><span data-stu-id="dcf95-238">Localize web part settings values</span></span>

<span data-ttu-id="dcf95-p125">Microsoft SharePoint unterstützt Multilingual User Interface (MUI), in dem der Administrator der Website mehrere Sprachen für die Benutzeroberfläche aktivieren kann. Wenn der Benutzer die Website besucht, wird die Benutzeroberfläche automatisch in der für den Benutzer in den Einstellungen festgelegten bevorzugten Sprache angezeigt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p125">Microsoft SharePoint supports Multilingual User Interface (MUI) where the site administrator can enable multiple languages for the user interface. When the user visits the site, its UI will automatically be displayed using the preferred language based on that user's preferences.</span></span>

<span data-ttu-id="dcf95-p126">Auf mehrsprachigen Websites verwendete Webparts sollten automatisch die aktuell im Unternehmen verwendete Sprache und zeigen Sie deren Inhalte in dieser Sprache an. Das SharePoint Framework vereinfacht diesen Prozess, indem es die Ressourcendatei automatisch in der aktuell verwendeten Sprache lädt. Darüber hinaus wird beim Testen von SharePoint Framework-Webparts mit der gehosteten Version der SharePoint-Workbench ebenfalls automatisch die vom Benutzer bevorzugte Sprache verwendet.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p126">Web parts used on multilingual sites should automatically detect the currently used language and display their contents in that language. The SharePoint Framework simplifies this process by automatically loading the resource file corresponding to the currently used language. Additionally, when testing SharePoint Framework web parts using the hosted version of the SharePoint workbench, the workbench also automatically uses the language preferred by the user.</span></span>

<span data-ttu-id="dcf95-p127">Über die Webparteigenschaften konfigurierte Werte werden nicht in den Ressourcendateien gespeichert. Standardmäßig wird der konfigurierte Wert in der vorliegenden Form verwendet, das kann zu Inkonsistenzen führen, z. B. zu einer englischen Begrüßung des Benutzers, obwohl die bevorzugte Sprache des Benutzers Niederländisch ist.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p127">Values configured through web part properties are not stored in resource files. By default, the configured value is used as-is, which might lead to inconsistencies such as greeting the user in English when the user's preferred language is Dutch.</span></span>

![Die Begrüßungsmeldung wird in US-Englisch angezeigt, obwohl die Workbench auf Niederländisch (Niederlande) einstellt ist.](../../../images/localization-english-greeting-dutch-workbench.png)

<span data-ttu-id="dcf95-p128">Mit vom SharePoint Framework bereitgestellten Bausteinen können Sie Ihren Webpart durch die Unterstützung zum Speichern von Webpart-Konfigurationswerten in mehreren Sprachen erweitern. Für jede der unterstützten Sprachen wird im Eigenschaftenbereich ein separates Textfeld angezeigt, in das der Benutzer den übersetzten Wert für diese Eigenschaft eingeben kann.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p128">Using the building blocks provided with the SharePoint Framework, you can extend your web part with support for storing web part configuration values in multiple languages. For each of the supported languages the property pane will display a separate text field in which the user can enter the translated value for that property.</span></span>

![Mit mehreren im Webparteigenschaftenbereich wiedergegebenen Textfeldern ist die Übersetzung von Webpartwerten möglich](../../../images/localization-multilingual-properties.png)

> [!NOTE] 
> <span data-ttu-id="dcf95-250">Bei der zum Testen des in diesem Artikel veranschaulichten Webparts verwendeten SharePoint-Website handelt es sich um eine mehrsprachige Website, bei der als Sprachen US-Englisch, Niederländisch und Deutsch aktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="dcf95-250">Note: The SharePoint site used to test the web part shown in this article is a multilingual site with the US English, Dutch, and German languages enabled. For more information about enabling additional languages in SharePoint sites see the Choose the languages you want to make available for a site’s user interface support article.</span></span> <span data-ttu-id="dcf95-251">Weitere Informationen zum Aktivieren von zusätzlicher Sprachen auf SharePoint-Websites finden Sie in dem Support-Artikel [Auswahl der Sprachen für die Benutzeroberfläche einer Website](https://support.office.com/de-DE/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8).</span><span class="sxs-lookup"><span data-stu-id="dcf95-251">Note: The SharePoint site used to test the web part shown in this article is a multilingual site with the US English, Dutch, and German languages enabled. For more information about enabling additional languages in SharePoint sites see the [Choose the languages you want to make available for a site’s user interface](https://support.office.com/de-DE/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) support article.</span></span>

### <a name="add-list-of-languages-supported-by-sharepoint-online"></a><span data-ttu-id="dcf95-252">Hinzufügen einer von SharePoint Online unterstützten Liste von Sprachen</span><span class="sxs-lookup"><span data-stu-id="dcf95-252">Add list of languages supported by SharePoint Online</span></span>

<span data-ttu-id="dcf95-253">Die Liste der Sprachen, die bei einer mehrsprachigen SharePoint-Website aktiviert sind, wird als Array von Gebietsschema-IDs (LCIDS) zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="dcf95-253">The list of languages enabled on a multilingual SharePoint site is returned as an array of locale identifiers (LCID).</span></span> <span data-ttu-id="dcf95-254">Beispielsweise **1033** für Englisch (USA).</span><span class="sxs-lookup"><span data-stu-id="dcf95-254">For example, **1033** for US English.</span></span> <span data-ttu-id="dcf95-255">Die aktuell verwendete Sprache wird jedoch als Zeichenfolge zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="dcf95-255">The currently used language is however returned as a string.</span></span> <span data-ttu-id="dcf95-256">Beispielsweise **en-US** für Englisch (USA).</span><span class="sxs-lookup"><span data-stu-id="dcf95-256">For example, **en-US** for US English.</span></span> <span data-ttu-id="dcf95-257">Da JavaScript über keine systemeigene Methode zum Konvertieren der LCID-Nummer des Gebietsschemanamens verfügt und umgekehrt, müssen Sie dies manuell vornehmen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-257">As JavaScript doesn't have a native way of converting the LCID number to the locale name, and vice-versa, you have to do it yourself.</span></span>

<span data-ttu-id="dcf95-258">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.ts**, und fügen Sie eine neue Klassenvariable namens **locales** unter **GreetingWebPart** hinzu, mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="dcf95-258">In the code editor, open the **./src/webparts/greeting/GreetingWebPart.ts** file and add a new class variable named **locales** inside of existing **GreetingWebPart** with the following code:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  private locales = {
    1025: 'ar-SA',
    1026: 'bg-BG',
    1027: 'ca-ES',
    1028: 'zh-TW',
    1029: 'cs-CZ',
    1030: 'da-DK',
    1031: 'de-DE',
    1032: 'el-GR',
    1033: 'en-US',
    1035: 'fi-FI',
    1036: 'fr-FR',
    1037: 'he-IL',
    1038: 'hu-HU',
    1040: 'it-IT',
    1041: 'ja-JP',
    1042: 'ko-KR',
    1043: 'nl-NL',
    1044: 'nb-NO',
    1045: 'pl-PL',
    1046: 'pt-BR',
    1048: 'ro-RO',
    1049: 'ru-RU',
    1050: 'hr-HR',
    1051: 'sk-SK',
    1053: 'sv-SE',
    1054: 'th-TH',
    1055: 'tr-TR',
    1057: 'id-ID',
    1058: 'uk-UA',
    1060: 'sl-SI',
    1061: 'et-EE',
    1062: 'lv-LV',
    1063: 'lt-LT',
    1066: 'vi-VN',
    1068: 'az-Latn-AZ',
    1069: 'eu-ES',
    1071: 'mk-MK',
    1081: 'hi-IN',
    1086: 'ms-MY',
    1087: 'kk-KZ',
    1106: 'cy-GB',
    1110: 'gl-ES',
    1164: 'prs-AF',
    2052: 'zh-CN',
    2070: 'pt-PT',
    2074: 'sr-Latn-CS',
    2108: 'ga-IE',
    3082: 'es-ES',
    5146: 'bs-Latn-BA',
    9242: 'sr-Latn-RS',
    10266: 'sr-Cyrl-RS',
  };

  // ...
}
```

<span data-ttu-id="dcf95-259">Die Variable **locales** führt alle Sprachen auf, die von SharePoint Online unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-259">The **locales** variable lists all languages supported by SharePoint Online.</span></span>

<span data-ttu-id="dcf95-260">Fügen Sie als Nächstes zwei Klassenmethoden hinzu, mit denen Sie die LCID aus den Gebietsschemanamen und den Gebietsschemaname der LCID abrufen können:</span><span class="sxs-lookup"><span data-stu-id="dcf95-260">Next, add two class methods that will allow you to get the LCID from the locale name, and the locale name from the LCID:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...

  private getLocaleId(localeName: string): number {
    const pos: number = (Object as any).values(this.locales).indexOf(localeName);
    if (pos > -1) {
      return parseInt(Object.keys(this.locales)[pos]);
    }
    else {
      return 0;
    }
  }

  private getLocaleName(localeId: number): string {
    const pos: number = Object.keys(this.locales).indexOf(localeId.toString());
    if (pos > -1) {
      return (Object as any).values(this.locales)[pos];
    }
    else {
      return '';
    }
  }
}
```

### <a name="remove-the-standard-greeting-web-part-property"></a><span data-ttu-id="dcf95-261">Entfernen der Standardbegrüßung-Webparteigenschaft</span><span class="sxs-lookup"><span data-stu-id="dcf95-261">Remove the standard greeting web part property</span></span>

<span data-ttu-id="dcf95-262">Ursprünglich war in dem Begrüßung-Webpart die **greeting**-Eigenschaft definiert, in der der Benutzer die auf dem Bildschirm anzuzeigende Begrüßung angeben konnte.</span><span class="sxs-lookup"><span data-stu-id="dcf95-262">Originally, the Greeting web part had the **greeting** property defined where the user could specify the greeting to be displayed on the screen.</span></span> <span data-ttu-id="dcf95-263">Um Webparts anzupassen, damit mehrsprachige SharePoint-Websites unterstützt werden, müssen Sie mehrere Werte speichern; einen für jede Sprache.</span><span class="sxs-lookup"><span data-stu-id="dcf95-263">To adapt the web part to support multilingual SharePoint sites, you need to store multiple values; one for each language.</span></span> <span data-ttu-id="dcf95-264">Da Sie nicht wissen können, welche Sprachen auf der Website aktiviert sind, können Sie statt einer statischen Webparteigenschaft Webparteigenschaften dynamisch zur Laufzeit generieren.</span><span class="sxs-lookup"><span data-stu-id="dcf95-264">Originally, the Greeting web part had the greeting property defined where the user could specify the greeting to be displayed on the screen. To adapt the web part to support multilingual SharePoint sites, you need to store multiple values; one for each language. Because you cannot know up front which languages will be enabled on the site, rather than using one static web part property, you will dynamically generate web part properties at runtime.</span></span>

<span data-ttu-id="dcf95-265">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.manifest.json** und entfernen Sie die **greeting**-Eigenschaft aus der **properties**Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="dcf95-265">In the code editor open the **./src/webparts/greeting/GreetingWebPart.manifest.json** file, and remove the **greeting** property from the **properties** property:</span></span>

```json
{
  // ...

  "preconfiguredEntries": [{
    "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
    "group": { "default": "Other", "nl-nl": "Anders" },
    "title": { "default": "Greeting", "nl-nl": "Begroeting" },
    "description": { "default": "Greets the user", "nl-nl": "Begroet de gebruiker" },
    "officeFabricIconFontName": "Page",
    "properties": {
    }
  }]
}
```

<span data-ttu-id="dcf95-266">Öffnen Sie nun im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.ts**, und entfernen Sie die Eigenschaft **greeting** aus der `IGreetingWebPartProps`-Schnittstellendefinition:</span><span class="sxs-lookup"><span data-stu-id="dcf95-266">Next, open the **./src/webparts/greeting/IGreetingWebPartProps.ts** file, and remove the greeting property from the interface definition:</span></span>

```ts
export interface IGreetingWebPartProps {
}
```

<span data-ttu-id="dcf95-267">Da die zentrale React-Komponente eine Begrüßung anzeigen sollte, öffnen Sie jetzt die Datei **./src/webparts/greeting/components/IGreetingProps.ts** und ändern die Schnittstelle **IGreetingProps** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dcf95-267">Because the main React component should display a greeting, open the **./src/webparts/greeting/components/IGreetingProps.ts** file, and change the **IGreetingProps** interface to:</span></span>

```ts
export interface IGreetingProps {
  greeting: string;
}
```

<span data-ttu-id="dcf95-268">Mit dieser Änderung können Sie die anzuzeigende Begrüßung aus dem Webpart an die React-Komponente übergeben.</span><span class="sxs-lookup"><span data-stu-id="dcf95-268">With this modification, you can pass the greeting to be displayed from the web part to the React component.</span></span>

### <a name="display-property-pane-text-fields-for-all-enabled-languages"></a><span data-ttu-id="dcf95-269">Anzeigen von Eigenschaftenbereich-Textfeldern für alle aktivierten Sprachen</span><span class="sxs-lookup"><span data-stu-id="dcf95-269">Display property pane text fields for all enabled languages</span></span>

<span data-ttu-id="dcf95-p132">Zunächst kann der Benutzer Webpartkonfiguration eine Willkommensnachricht konfigurieren. Mit dem Webpart konnte der Benutzer einen einzelnen Wert konfigurieren, der für alle Benutzer unabhängig von deren bevorzugter Sprache angezeigt wurde. Durch Abrufen der Liste der auf der aktuellen Website aktivierten Sprachen können Textfelder dynamisch angezeigt werden, damit Benutzer Übersetzungen für alle auf der Website aktivierten Sprachen erhalten.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p132">Initially, by using the web part configuration the user could configure a welcome message. The web part allowed the user to configure a single value which was displayed to all users no matter their language preference. By retrieving the list of languages enabled in the current site, you can dynamically display text fields to allow the user to provide translations for all the languages enabled in the site.</span></span>

#### <a name="load-information-about-languages-enabled-in-the-current-site"></a><span data-ttu-id="dcf95-273">Laden der Informationen zu den auf der aktuellen Website aktivierten Sprachen</span><span class="sxs-lookup"><span data-stu-id="dcf95-273">Load information about languages enabled in the current site</span></span>

<span data-ttu-id="dcf95-274">Der erste Schritt besteht darin, die Informationen zu allen auf der aktuellen Website aktivierten Sprachen zu laden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-274">The first step is to load the information about all languages enabled in the current site. In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named supportedLanguageIds:</span></span> <span data-ttu-id="dcf95-275">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.ts** und fügen Sie eine neue Klassenvariable namens **supportedLanguageIds** hinzu:</span><span class="sxs-lookup"><span data-stu-id="dcf95-275">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named greetingFields to the GreetingWebPart class:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...
  private supportedLanguageIds: number[];
  // ...
}
```

<span data-ttu-id="dcf95-276">Da wir Daten aus SharePoint abfragen werden, verwenden wir für die Vorgänge den SharePoint-HTTP-Client.</span><span class="sxs-lookup"><span data-stu-id="dcf95-276">Since we will be querying data in SharePoint, we will be using SharePoint Http Client for the operations. Add following imports just above the GreetingWebPart.</span></span> <span data-ttu-id="dcf95-277">Fügen Sie die nachfolgend aufgeführten Importe direkt über **GreetingWebPart** ein.</span><span class="sxs-lookup"><span data-stu-id="dcf95-277">Add following imports just above the **GreetingWebPart**.</span></span>

```ts
import {
  SPHttpClient,
  SPHttpClientResponse
} from '@microsoft/sp-http';
```

<span data-ttu-id="dcf95-278">Fügen Sie als Nächstes in der Klasse **GreetingWebPart** eine neue Methode mit dem Namen **getSupportedLanguageIds** hinzu:</span><span class="sxs-lookup"><span data-stu-id="dcf95-278">Next, in the **GreetingWebPart** class, add a new method named **getSupportedLanguageIds**:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...

  private getSupportedLanguageIds(): Promise<number[]> {
    return new Promise<number[]>((resolve: (supportedLanguageIds: number[]) => void, reject: (error: any) => void): void => {
      if (this.supportedLanguageIds) {
        resolve(this.supportedLanguageIds);
        return;
      }

      this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + '/_api/web?$select=SupportedUILanguageIds', SPHttpClient.configurations.v1)
      .then((response: SPHttpClientResponse): Promise<{ SupportedUILanguageIds: number[] }> => {
        return response.json();
      }).then((siteInfo: { SupportedUILanguageIds: number[] }): void => {
        this.supportedLanguageIds = siteInfo.SupportedUILanguageIds;
        resolve(siteInfo.SupportedUILanguageIds);
      }, (error: any): void => {
        reject(error);
      });
    });
  }
}
```

<span data-ttu-id="dcf95-p135">Die Liste der auf der aktuellen Website aktivierten Sprachen sollte nur einmal geladen werden. Wenn die Informationen zu den Sprachen noch nicht geladen wurden, verwendet die Methode den standardmäßigen SharePoint Framework-HTTP-Client, um die SharePoint-REST-API aufzurufen und die Informationen zu auf der aktuellen Website aktivierten Sprachen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p135">The list of languages enabled in the current site should be loaded only once. If the information about the languages hasn't been loaded yet, the method uses the standard SharePoint Framework HTTP Client to call the SharePoint REST API and retrieve the information about languages enabled on the current site.</span></span>

#### <a name="dynamically-render-text-fields-for-all-languages"></a><span data-ttu-id="dcf95-281">Dynamisches Erstellen von Textfelder für alle Sprachen</span><span class="sxs-lookup"><span data-stu-id="dcf95-281">Dynamically render text fields for all languages</span></span>

<span data-ttu-id="dcf95-282">Nun, da Sie die Informationen zu den auf der aktuellen Website aktivierten Sprachen abgerufen haben, können Sie die Textfelder für diese Sprachen anzeigen, damit der Benutzer die übersetzten Werte für die Begrüßungsmeldung angeben kann.</span><span class="sxs-lookup"><span data-stu-id="dcf95-282">Now that you can retrieve the information about the languages enabled on the current site, you will display text fields for each of these languages so that the user can specify translated values for the greeting message.</span></span>

<span data-ttu-id="dcf95-283">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/GreetingWebPart.ts** und fügen Sie eine neue Klassenvariable namens **greetingFields** zur **GreetingWebPart**-Klasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="dcf95-283">In the code editor, open the **./src/webparts/greeting/GreetingWebPart.ts** file, and add a new class variable named **greetingFields** to the **GreetingWebPart** class:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...
  private greetingFields: IPropertyPaneField<any>[] = [];
  // ...
}
```

<span data-ttu-id="dcf95-284">Ändern Sie die **import**-Anweisung für das **@microsoft/sp-webpart-base**-Paket folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="dcf95-284">Change the **import** statement for the **@microsoft/sp-webpart-base** package to:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  IPropertyPaneField
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="dcf95-285">Ändern Sie den **PropertyPaneSettings**-Getter zum Abrufen der Liste der Textfelder aus der neu hinzugefügten **GreetingFields**-Klassenvariable:</span><span class="sxs-lookup"><span data-stu-id="dcf95-285">Change the **propertyPaneSettings** getter to get the list of text fields from the newly added **greetingFields** class variable:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...

    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.GreetingGroupName,
              groupFields: this.greetingFields
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="dcf95-286">Wenn auf der Website mehrere Sprachen aktiviert sind, erstellt der Webpart mehrere Felder für den Benutzer zur Eingabe der Willkommensmeldung.</span><span class="sxs-lookup"><span data-stu-id="dcf95-286">If the site has multiple languages enabled, the web part will render multiple fields for the user to enter the greeting message. To make it clear that these fields belong together, put them in a separate group. In the code editor, open the ./src/webparts/greeting/loc/mystrings.d.ts file, and change its code to:</span></span> <span data-ttu-id="dcf95-287">Um zu verdeutlichen, dass diese Felder zusammen gehören, erstellen Sie dafür eine separate Gruppe.</span><span class="sxs-lookup"><span data-stu-id="dcf95-287">To make it clear that these fields belong together, put them in a separate group.</span></span> <span data-ttu-id="dcf95-288">Öffnen Sie im Code-Editor die Datei **./src/webparts/greeting/loc/mystrings.d.ts** und ändern Sie den Code in der Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dcf95-288">In the code editor, open the **./src/webparts/gallery/loc/mystrings.d.ts** file. Change its code to:</span></span>

```ts
declare interface IGreetingWebPartStrings {
  PropertyPaneDescription: string;
  GreetingGroupName: string;
  LearnMoreButtonLabel: string;
}

declare module 'GreetingWebPartStrings' {
  const strings: IGreetingWebPartStrings;
  export = strings;
}
```

<span data-ttu-id="dcf95-289">Aktualisieren die Ressourcendateien entsprechend der für die **GreetingGroupName**Zeichenfolge angegebenen Werte.</span><span class="sxs-lookup"><span data-stu-id="dcf95-289">Update the resource files accordingly to provide values for the **GreetingGroupName** string.</span></span>

<span data-ttu-id="dcf95-290">**./src/webparts/greeting/loc/en-us.js**:</span><span class="sxs-lookup"><span data-stu-id="dcf95-290">**./src/webparts/greeting/loc/en-us.js**:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Greeting web part configuration",
    "GreetingGroupName": "Greeting to show in the web part",
    "LearnMoreButtonLabel": "Learn more"
  }
});
```

<span data-ttu-id="dcf95-291">**./src/webparts/greeting/loc/nl-nl.js**:</span><span class="sxs-lookup"><span data-stu-id="dcf95-291">**./src/webparts/greeting/loc/nl-nl.js**:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
    "GreetingGroupName": "Begroeting die in het webonderdeel getoond wordt",
    "LearnMoreButtonLabel": "Meer informatie"
  }
});
```

<span data-ttu-id="dcf95-292">**./src/webparts/greeting/loc/qps-ploc.js**:</span><span class="sxs-lookup"><span data-stu-id="dcf95-292">**./src/webparts/greeting/loc/qps-ploc.js**:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "[!!! Gřèèƭïñϱ ωèβ ƥářƭ çôñƒïϱúřáƭïôñ ℓôřè₥ ïƥƨú !!!]",
    "GreetingGroupName": "[!!! Gřèèƭïñϱ ƭô ƨλôω ïñ ƭλè ωèβ ƥářƭ ℓôřè₥ ïƥƨú !!!]",
    "LearnMoreButtonLabel": "[!!! £èářñ ₥ôřè ℓôř !!!]"
  }
});
```

<span data-ttu-id="dcf95-293">Umgehen Sie die **./src/webparts/greeting/GreetingWebPart.ts**-Datei der **onPropertyPaneConfigurationStart**Methode mithilfe des folgenden Codes:</span><span class="sxs-lookup"><span data-stu-id="dcf95-293">In the **./src/webparts/greeting/GreetingWebPart.ts** file override the **onPropertyPaneConfigurationStart** method using the code:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...
  protected onPropertyPaneConfigurationStart(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'languages');

    this.getSupportedLanguageIds()
      .then((supportedLanguageIds: number[]): void => {
        this.greetingFields = [];
        supportedLanguageIds.forEach(localeId => {
          this.greetingFields.push(PropertyPaneTextField(`greeting_${localeId}`, {
            label: this.getLocaleName(localeId)
          }));
        });

        this.context.propertyPane.refresh();
        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        this.render();
      });
  }
}
```

<span data-ttu-id="dcf95-294">Wenn der Benutzer im Webpart-Eigenschaftenbereich geöffnet wird, lädt die Methode die Informationen zu den auf der aktuellen Website aktivierten Sprachen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-294">When the user opens the web part property pane, the method will load the information about the languages enabled in the current site.</span></span> <span data-ttu-id="dcf95-295">Da das Laden dieser Informationen einen Moment dauern kann, zeigt die Methode eine Ladeanzeige zur Kommunikation des Status an den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="dcf95-295">Because loading this information might take a moment, the method displays a loading indicator communicating its status to the user.</span></span> <span data-ttu-id="dcf95-296">Nachdem Sie die Informationen zu den aktivierten Sprachen geladen haben, erstellt die Methode ein neues Eigenschaftenbereich-Textfeld, das mit einer dynamischen Webparteigenschaft namens **Greeting__lcid_** verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="dcf95-296">Once the information about the enabled languages is loaded, the method creates a new property pane text field linked to a dynamic web part property named **greeting__lcid_**.</span></span> <span data-ttu-id="dcf95-297">Beispielsweise **greeting_1033** für Englisch (USA).</span><span class="sxs-lookup"><span data-stu-id="dcf95-297">For example, **greeting_1033** for US English.</span></span>

<span data-ttu-id="dcf95-298">Sobald Textfelder für alle aktivierten Sprachen erstellt werden, aktualisiert die Methode den Eigenschaftenbereich durch Aufrufen der **IPropertyPaneAccessor.refresh**-Methode.</span><span class="sxs-lookup"><span data-stu-id="dcf95-298">Once text fields for all enabled languages are constructed, the method refreshes the property pane by calling the **refreshPropertyPane** method. Finally, the method clears the web part loading indicator and re-renders the web part body.</span></span> <span data-ttu-id="dcf95-299">Zum Schluss entfernt die Methode die Webpart-Ladeanzeige und erstellt den Textkörper des Webparts neu.</span><span class="sxs-lookup"><span data-stu-id="dcf95-299">Once text fields for all enabled languages are constructed, the method refreshes the property pane by calling the refreshPropertyPane method. Finally, the method clears the web part loading indicator and re-renders the web part body.</span></span>

![Textfelder für alle aktivierten Sprachen werden im Webpart-Eigenschaftenbereich angezeigt](../../../images/localization-multilingual-properties.png)

### <a name="show-the-greeting-for-the-preferred-user-language"></a><span data-ttu-id="dcf95-301">Anzeigen der Begrüßung für die bevorzugte Sprache des Benutzers</span><span class="sxs-lookup"><span data-stu-id="dcf95-301">Show the greeting for the preferred user language</span></span>

<span data-ttu-id="dcf95-p139">Der Webpart zeigte ursprünglich die gleiche Begrüßung für alle Benutzer unabhängig von ihrer bevorzugten Sprache an. Nun, da in dem Webpart unterschiedliche Übersetzungen der Willkommensnachricht gespeichert wurden, sollte die Begrüßung in der vom aktuellen Benutzer bevorzugten Sprache angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p139">Originally the web part showed the same greeting for all users no matter their preferred language. Now that the web part has different translations of the welcome message stored, it should display the greeting using the language preferred by the current user.</span></span>

<span data-ttu-id="dcf95-304">Ändern Sie in der **./src/webparts/greeting/GreetingWebPart.ts**-Datei die **ender**-Methode des Webparts:</span><span class="sxs-lookup"><span data-stu-id="dcf95-304">In the **./src/webparts/greeting/GreetingWebPart.ts** file, change the web part's **render** method to:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...

  public render(): void {
    const element: React.ReactElement<IGreetingProps> = React.createElement(Greeting, {
      greeting: this.getGreeting()
    });

    ReactDom.render(element, this.domElement);
  }
}
```

<span data-ttu-id="dcf95-305">Fügen Sie als Nächstes in der **GreetingWebPart**-Klasse eine neue Methode mit dem Namen **getGreeting** hinzu:</span><span class="sxs-lookup"><span data-stu-id="dcf95-305">Next, in the **GreetingWebPart** add a new method named **getGreeting**:</span></span>

```ts
export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
  // ...

  private getGreeting(): string {
    let localeId: number = this.getLocaleId(this.context.pageContext.cultureInfo.currentUICultureName);
    if (localeId === 0) {
      localeId = 1033;
    }

    return this.properties[`greeting_${localeId}`];
  }

  // ...
}
```

<span data-ttu-id="dcf95-p140">Diese Methode ruft die derzeit verwendete Sprache ab und konvertiert sie in eine Gebietsschema-ID. Anschließend gibt sie den Wert der Begrüßungseigenschaft in der übersetzten Sprache zurück.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p140">This method gets the currently used language and converts it to a locale ID. Then it returns the value of the greeting property translated to that language.</span></span>

## <a name="localization-in-different-build-types"></a><span data-ttu-id="dcf95-308">Lokalisierung in andere Build-Typen</span><span class="sxs-lookup"><span data-stu-id="dcf95-308">Localization in different build types</span></span>

<span data-ttu-id="dcf95-p141">Das SharePoint Framework behandelt Lokalisierungsdateien je nach ausgewähltem Build-Modus unterschiedlich. Es folgen einige der Unterschiede zwischen den Dateien in einem Debug- und einem Release-Build.</span><span class="sxs-lookup"><span data-stu-id="dcf95-p141">Depending on the selected build mode, the SharePoint Framework handles localization files differently. Following are some of the differences between the files generated in a debug and a release build.</span></span>

### <a name="localization-files-in-the-debug-build"></a><span data-ttu-id="dcf95-311">Lokalisierungsdateien im Debug-Build</span><span class="sxs-lookup"><span data-stu-id="dcf95-311">Localization files in the debug build</span></span>

<span data-ttu-id="dcf95-312">Beim Erstellen von SharePoint-Framework-Projekten im Debugmodus sind nur die Informationen zu dem Standard-Gebietsschema im generierten Webpart-Manifest enthalten.</span><span class="sxs-lookup"><span data-stu-id="dcf95-312">When building SharePoint Framework projects in debug mode, only the information about the default locale is included in the generated web part manifest.</span></span> <span data-ttu-id="dcf95-313">Im Debugmodus verwendet SharePoint-Framework entweder das Standard-en-US-Gebietsschema oder das Gebietsschema, das in der Projektkonfiguration oder über das **locale**-Argument in der Befehlszeile angegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="dcf95-313">In debug mode SharePoint Framework either uses the default en-US locale or the locale that has been specified in the project configuration or using the **locale** argument in command line.</span></span> <span data-ttu-id="dcf95-314">Ressourcendateien mit übersetzten Zeichenfolgen sind im **dist**-Ausgabeordner nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="dcf95-314">Resource files with translated strings are not included in the output **dist** folder.</span></span> <span data-ttu-id="dcf95-315">Stattdessen werden sie zur Laufzeit aus dem vorläufigen **lib**-Ordner mithilfe des Pfads im generierten Webpart-Manifest geladen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-315">Instead they are loaded at runtime from the intermediate **lib** folder using the path in the generated web part manifest.</span></span>

<span data-ttu-id="dcf95-316">Wenn Sie sich de Informationen zum **GreetingWebPartStrings**-Modul im Webpart-Manifest ansehen, das während eines Debug-Builds generiert wurde, werden Sie feststellen, dass trotz der verschiedenen vom Webpart (en-US, nl_NL und qps-ploc) unterstützten Gebietsschemas der Pfad zur im vorläufigen Speicherort der gespeicherten en-Ressourcendatei als Standardpfad des Lokalisierungsmoduls zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="dcf95-316">Looking at the information about the **greetingStrings** module in the web part manifest generated during a debug build, you can see that despite the different locales supported by the web part (en-US, nl-NL and qps-ploc) the path to the en-US resource file stored in the intermediate location has been assigned as the default path of the localization module.</span></span>

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting-web-part",
    "internalModuleBaseUrls": [
      "https://localhost:4321/"
    ],
    "scriptResources": {
      "greeting-web-part": {
        "type": "path",
        "path": "dist/greeting-web-part.js"
      },
      "GreetingWebPartStrings": {
        "defaultPath": "lib/webparts/greeting/loc/en-us.js",
        "type": "localizedPath",
        "paths": {
          "en-US": "lib/webparts/greeting/loc/en-us.js",
          "nl-NL": "lib/webparts/greeting/loc/nl-nl.js",
          "qps-ploc": "lib/webparts/greeting/loc/qps-ploc.js"
        }
      },
      // ...
    }
  }
}
```

### <a name="localization-files-in-the-release-build"></a><span data-ttu-id="dcf95-317">Lokalisierungsdateien im Release-Build</span><span class="sxs-lookup"><span data-stu-id="dcf95-317">Localization files in the release build</span></span>

<span data-ttu-id="dcf95-318">Beim Erstellen von SharePoint-Framework-Projekten im Release-Modus werden die Informationen zu allen verfügbaren Gebietsschemas in das generierte Webpart-Manifest eingebunden.</span><span class="sxs-lookup"><span data-stu-id="dcf95-318">When building SharePoint Framework projects in release mode, the information about all available locales is included in the generated web part manifest.</span></span> <span data-ttu-id="dcf95-319">Außerdem werden Ressourcen für die einzelnen Gebietsschemas in einer separaten Datei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dcf95-319">Additionally, resources for each locale are stored in a separate file.</span></span> <span data-ttu-id="dcf95-320">Diese Ressourcendateien werden zusammen mit dem Webpart-Manifest und dem Webpart-Paket in den **./temp/deploy**-Ordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="dcf95-320">These resource files are copied, along with the web part manifest and the web part bundle to the **./temp/deploy** folder.</span></span>

> <span data-ttu-id="dcf95-321">**Wichtig:** Release-Builds in Ressourcendateien werden nur in den **./temp/deploy**-Ordner kopiert und nicht in den **./dist**-Ordner.</span><span class="sxs-lookup"><span data-stu-id="dcf95-321">**Important:** In release builds resource files are copied only to the **./temp/deploy** folder and not to the **./dist** folder.</span></span> <span data-ttu-id="dcf95-322">Bei der Bereitstellung des Webparts zur Produktion sollten Sie immer Dateien aus dem **./temp/deploy**-Ordner verwendet werden, um sicherzustellen, dass Sie alle für Ihren Webpart erforderlichen Dateien bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="dcf95-322">Important: In release builds resource files are copied only to the ./temp/deploy folder and not to the ./dist folder. When deploying your web part to production you should always use files from the **./temp/deploy** folder to ensure that you are deploying all files required by your web part.</span></span>

<span data-ttu-id="dcf95-323">Durch Untersuchen des aktuellsten im Release-Build generierten Webpart-Manifest werden Sie feststellen, dass das **GreetingWebPartStrings**-Modul nun die Referenzen zu allen unterstützten Gebietsschemas enthält.</span><span class="sxs-lookup"><span data-stu-id="dcf95-323">Examining the latest web part manifest generated in a release build, you can see that now the **greetingStrings** module contains references to all supported locales.</span></span>

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting-web-part",
    "internalModuleBaseUrls": [
      "https://cdn.contoso.com/"
    ],
    "scriptResources": {
      "greeting-web-part": {
        "type": "path",
        "path": "greeting-web-part_159d9eb591c6716cae6d0ff15b78a19a.js"
      },
      "GreetingWebPartStrings": {
        "defaultPath": "react-localization-greetingwebpartstrings_en-us_b5e89eba6e8d819bf1647b3ab505dae5.js",
        "type": "localizedPath",
        "paths": {
          "en-US": "react-localization-greetingwebpartstrings_en-us_b5e89eba6e8d819bf1647b3ab505dae5.js",
          "nl-NL": "react-localization-greetingwebpartstrings_nl-nl_d6e80ff75385975e7737774e0802641e.js",
          "qps-ploc": "react-localization-greetingwebpartstrings_qps-ploc_effe5ee4af9cadee91bbf84327eb7308.js"
        }
      },
      // ...
    }
  }
}
```

<span data-ttu-id="dcf95-324">Beim Laden des Webparts auf der Seite lädt das SharePoint-Framework automatisch die Ressourcendatei für das entsprechende Gebietsschema, indem es die Informationen von der Kontext-Website verwendet.</span><span class="sxs-lookup"><span data-stu-id="dcf95-324">When loading the web part on the page, the SharePoint Framework will automatically load the resource file for the corresponding locale by using the information from the context site.</span></span> <span data-ttu-id="dcf95-325">Wenn keine übereinstimmende Ressourcendatei gefunden wird, lädt das SharePoint-Framework die in der **efaultPath**Eigenschaft angegebene Datei.</span><span class="sxs-lookup"><span data-stu-id="dcf95-325">If no matching resource file is found, the SharePoint Framework will load the file specified in the **defaultPath** property.</span></span> <span data-ttu-id="dcf95-326">Durch die Trennung der Ressourcendateien minimiert das SharePoint-Framework die auf der Seite für das Gebietsschema geladenen Datenmenge, das mit dem auf der Website verwendeten Gebietsschema übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="dcf95-326">By keeping the resource files separate, the SharePoint Framework minimizes the amount of data loaded on the page to the locale that matches the one used in the site.</span></span>
