---
title: "Überprüfen von Webpart-Eigenschaftswerten"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d2e042743a2c374a811fce9bc54f4e6dfd5ea3d2
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="validate-web-part-property-values"></a><span data-ttu-id="19215-102">Überprüfen von Webpart-Eigenschaftswerten</span><span class="sxs-lookup"><span data-stu-id="19215-102">Validate web part property values</span></span>

<span data-ttu-id="19215-p101">Wenn Sie mit Webparts arbeiten, können Benutzer diese mithilfe der Eigenschaften entsprechend der jeweiligen Bedürfnisse konfigurieren. Überprüfen Sie die bereitgestellten Konfigurationswerte und erleichtern Sie es Benutzern auf diese Weise, den Webpart zu konfigurieren und das Arbeiten mit dem Webpart insgesamt zu verbessern. In diesem Artikel erfahren Sie, wie Sie Eigenschaftswerte in clientseitigen Webparts in SharePoint Framework überprüfen.</span><span class="sxs-lookup"><span data-stu-id="19215-p101">When working with web parts, users can configure them to meet their needs using their properties. By validating the provided configuration values you can make it easier for users to configure the web part and improve the overall user experience of working with your web part. In this article you will learn how to validate web part property values in SharePoint Framework client-side web parts.</span></span>

> [!NOTE] 
> <span data-ttu-id="19215-106">Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint-Framework-Lösungen erstellen können.</span><span class="sxs-lookup"><span data-stu-id="19215-106">[Note:](../../set-up-your-development-environment.md) Before following the steps in this article, be sure to set up your development environment for building SharePoint Framework solutions.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="19215-107">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="19215-107">Create new project</span></span>

<span data-ttu-id="19215-108">Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="19215-108">Start by creating a new folder for your project.</span></span>

```sh
md react-listinfo
```

<span data-ttu-id="19215-109">Wechseln Sie zum Projektordner.</span><span class="sxs-lookup"><span data-stu-id="19215-109">Go to the project folder.</span></span>

```sh
cd react-listinfo
```

<span data-ttu-id="19215-110">Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="19215-110">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="19215-111">Geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:</span><span class="sxs-lookup"><span data-stu-id="19215-111">When prompted, enter the following values:</span></span>

- <span data-ttu-id="19215-112">**react-listinfo** als Name der Lösung</span><span class="sxs-lookup"><span data-stu-id="19215-112">**react-listinfo** as your solution name</span></span>
- <span data-ttu-id="19215-113">**Use the current folder** als Speicherort für die Dateien</span><span class="sxs-lookup"><span data-stu-id="19215-113">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="19215-114">**React** als Startpunkt für die Webparterstellung</span><span class="sxs-lookup"><span data-stu-id="19215-114">**React** as the starting point to build the web part</span></span>
- <span data-ttu-id="19215-115">**List Info** als Namen des Webparts</span><span class="sxs-lookup"><span data-stu-id="19215-115">**List info** as your web part name</span></span>
- <span data-ttu-id="19215-116">**Shows information about the selected list** als Beschreibung Ihres Webparts</span><span class="sxs-lookup"><span data-stu-id="19215-116">**Shows information about the selected list** as your web part description</span></span>

![SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../images/property-validation-yeoman-generator.png)

<span data-ttu-id="19215-118">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="19215-118">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="19215-119">Öffnen Sie dann den Projektordner im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="19215-119">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="19215-120">In diesem Artikel wird Visual Studio Code in den Schritten und Screenshots verwendet, Sie können jedoch einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="19215-120">This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![SharePoint Framework-Projekt in Visual Studio Code](../../../images/property-validation-visual-studio-code.png)

## <a name="validate-web-part-property-values-in-the-sharepoint-framework"></a><span data-ttu-id="19215-122">Überprüfen von Webpart-Eigenschaftswerten in SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="19215-122">Validate web part property values in the SharePoint Framework</span></span>

<span data-ttu-id="19215-p103">SharePoint Framework bietet Entwicklern zwei Methoden zum Überprüfen der Werte von Webpart-Eigenschaften. Sie können den Wert direkt innerhalb des Webpart-Codes überprüfen, oder Sie können eine externe API zum Durchführen der Überprüfung aufrufen. Die Inline-Überprüfung eignet sich zur Durchführung einfacher Überprüfungen wie z. B. auf minimale/maximale Länge, erforderliche Eigenschaften oder zur Erkennung einfacher Muster, wie z. B. Postleitzahlen. Bei auf Geschäftslogik basierenden Überprüfungen, z. B. der Sozialversicherungsnummer oder Mitgliedschaft in Sicherheitsgruppen, ist das Aufrufen externer APIs der bessere Ansatz.</span><span class="sxs-lookup"><span data-stu-id="19215-p103">SharePoint Framework offers developers two ways for validating values of web part properties. You can validate the value directly, inside web part's code, or you can call an external API to perform the validation there. Validating values inline is useful for performing simple validations such as minimal/maximum length, required properties or simple pattern recognition, like a ZIP code. Whenever the validation is based on business logic, such as checking a social security number or a security group membership, calling external APIs is a better approach.</span></span>

<span data-ttu-id="19215-p104">Um den Wert einer Webpart-Eigenschaft zu überprüfen, müssen Sie den Ereignishandler für das Ereignis **onGetErrorMessage** der jeweiligen Eigenschaft implementieren. Bei der Inline-Überprüfung sollte der Ereignishandler eine Zeichenfolge mit dem Fehler oder eine leere Zeichenfolge zurückgeben, wenn der angegebene Wert gültig ist. Für die Überprüfung mithilfe von Remote-APIs gibt der Ereignishandler eine Zusage der Zeichenfolge zurück. Wenn der angegebene Wert ungültig ist, wird die Zusage mit der Fehlermeldung aufgelöst. Ist der angegebene Wert gültig, wird die Zusage mit einer leeren Zeichenfolge aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="19215-p104">In order to validate the value of a web part property, you have to implement the event handler for the **onGetErrorMessage** event of that particular property. For inline validation the event handler should return a string with the validation error or an empty string if the provided value is valid. For validation using remote APIs the event handler returns a promise of string. If the provided value is invalid the promise resolves with the error message. If the provided value is valid then the promise resolves with an empty string.</span></span>

### <a name="validate-web-part-property-values-inline"></a><span data-ttu-id="19215-132">Inline-Überprüfung von Webpart-Eigenschaftswerten</span><span class="sxs-lookup"><span data-stu-id="19215-132">Validate web part property values inline</span></span>

<span data-ttu-id="19215-p105">In diesem Schritt überprüfen Sie, dass die Webpart-Eigenschaft einer Beschreibung angegeben ist und ihr Wert nicht mehr als 40 Zeichen beträgt. Dazu verwenden Sie das Inline-Überprüfungsverfahren.</span><span class="sxs-lookup"><span data-stu-id="19215-p105">In this step you will verify that the description web part property is specified and its value is not longer than 40 characters. You will do this using the inline validation process.</span></span>

<span data-ttu-id="19215-p106">Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts**. Fügen Sie in der Klasse **ListInfoWebPart** die Methode **validateDescription** mit dem folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="19215-p106">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. In the **ListInfoWebPart** class, add the **validateDescription** method with the following code:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

  private validateDescription(value: string): string {
    if (value === null ||
      value.trim().length === 0) {
      return 'Provide a description';
    }

    if (value.length > 40) {
      return 'Description should not be longer than 40 characters';
    }

    return '';
  }
}
```

<span data-ttu-id="19215-p107">Mit der Methode **validateDescription** wird überprüft, ob die Beschreibung angegeben wurde und 40 Zeichen nicht überschreitet. Ist die bereitgestellte Beschreibung ungültig, gibt die Methode eine Fehlermeldung zurück, die dem Überprüfungsfehler entspricht. Ist der angegebene Wert korrekt, wird eine leere Zeichenfolge zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="19215-p107">The **validateDescription** method checks if the description is provided and if it isn't longer than 40 characters. If the provided description is invalid, the method returns an error message corresponding to the validation error. If the provided value is correct it returns an empty string.</span></span>

<span data-ttu-id="19215-p108">Als Nächstes müssen Sie die Methode **validateDescription** der Webpart-Eigenschaft **description** zuordnen. Ändern Sie in der Klasse **ListInfoWebPart** die Implementierung der Methode **getPropertyPaneConfiguration** in:</span><span class="sxs-lookup"><span data-stu-id="19215-p108">Next, you have to associate the **validateDescription** method with the **description** web part property. In the **ListInfoWebPart** class change the implementation of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
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
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="19215-142">Sie haben die Definition des Webparts **description** durch Definieren der Methode **validateDescription** als Ereignishandler für das Ereignis **onGetErrorMessage** erweitert.</span><span class="sxs-lookup"><span data-stu-id="19215-142">You have extended the definition of the **description** web part with defining the **validateDescription** method as the event handler for the **onGetErrorMessage** event.</span></span>

<span data-ttu-id="19215-143">Führen Sie den folgenden Befehl aus, um das Ergebnis der Überprüfung zu sehen:</span><span class="sxs-lookup"><span data-stu-id="19215-143">Run the following command to see the result of the validation:</span></span>

```sh
gulp serve
```

<span data-ttu-id="19215-p109">Fügen Sie in der Workbench den Webpart zum Zeichenbereich hinzu, und öffnen Sie dessen Eigenschaften. Wenn Sie die Beschreibung entfernen, sollte der erste Fehler angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="19215-p109">In the workbench, add the web part to canvas and open its properties. If you remove the description you should see the first validation error.</span></span>

![Angezeigter Überprüfungsfehler in einer erforderlichen Eigenschaft ohne angegebenen Wert](../../../images/property-validation-empty-description-error.png)

<span data-ttu-id="19215-p110">Geben Sie danach einen Wert an, der länger als 40 Zeichen ist. Unterhalb des Textfelds sollte ein weiterer Überprüfungsfehler angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="19215-p110">Next, try providing a value that's longer than 40 characters. You should see another validation error displayed below the text field.</span></span>

![Angezeigter Überprüfungsfehler, wenn der angegebene Wert länger als zulässig ist](../../../images/property-validation-description-too-long-error.png)

<span data-ttu-id="19215-p111">Beachten Sie, dass bei Angabe eines ungültigen Werts der Webpart mit dem letzten gültigen Wert gerendert wird. Darüber hinaus wird im nichtreaktiven Modus des Eigenschaftenbereichs bei Ungültigkeit einer Webpart-Eigenschaft die Schaltfläche **Apply** deaktiviert, damit die ungültige Konfiguration nicht vom Benutzer angewendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="19215-p111">Notice, that when providing an invalid value, the web part is rendered showing the last valid value. Additionally, in the non-reactive property pane mode, if one of the web part properties is invalid, the **Apply** button is disabled, preventing the user from applying the invalid configuration.</span></span>

![Als deaktiviert gerenderte Apply-Schaltfläche, wenn eine Webpart-Eigenschaft einen ungültigen Wert aufweist.](../../../images/property-validation-description-error-apply-disabled.png)

### <a name="validate-web-part-property-values-using-remote-apis"></a><span data-ttu-id="19215-153">Überprüfung von Webpart-Eigenschaftswerten mithilfe von Remote-APIs</span><span class="sxs-lookup"><span data-stu-id="19215-153">Validate web part property values using remote APIs</span></span>

<span data-ttu-id="19215-p112">In einigen Szenarien kann das Überprüfen von Webpart-Eigenschaftswerten komplexer sein und eine bestimmte Geschäftslogik erfordern. In solchen Fällen kann es effizienter sein, den Wert mit einer vorhandenen API zu überprüfen, anstatt die Geschäftslogik im Webpart zu implementieren und aufrechtzuerhalten.</span><span class="sxs-lookup"><span data-stu-id="19215-p112">In some scenarios, validating web part property values can be more complex and require specific business logic. In such cases it might be more efficient for you to validate the value using an existing API rather than implementing and maintaining the business logic in the web part.</span></span>

<span data-ttu-id="19215-156">In diesem Schritt implementieren Sie eine Validierungslogik, die überprüft, ob die Liste mit dem in den Webpart-Eigenschaften angegebenen Namen auf der aktuellen SharePoint-Website vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="19215-156">In this step you will implement validation logic that checks if the list with the name specified in the web part properties exists in the current SharePoint site.</span></span>

#### <a name="add-the-listname-web-part-property"></a><span data-ttu-id="19215-157">Hinzufügen der Webpart-Eigenschaft listName</span><span class="sxs-lookup"><span data-stu-id="19215-157">Add the listName web part property</span></span>

<span data-ttu-id="19215-p113">Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.manifest.json**. Fügen Sie in der Eigenschaft **properties** eine neue Eigenschaft mit dem Namen **listName** hinzu, deren Standardwert auf eine leere Zeichenfolge festgelegt ist:</span><span class="sxs-lookup"><span data-stu-id="19215-p113">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.manifest.json** file. In the **properties** property add a new property named **listName** with the default value set to an empty string:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "1ec8f92d-ea55-4584-bf50-bac435c916bf",
  "alias": "ListInfoWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "preconfiguredEntries": [{
    "groupId": "1ec8f92d-ea55-4584-bf50-bac435c916bf",
    "group": { "default": "Under Development" },
    "title": { "default": "List info" },
    "description": { "default": "Shows information about the selected list" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "List info"
    }
  }]
}
```

<span data-ttu-id="19215-160">Öffnen Sie als Nächstes im Code-Editor die Datei **./src/webparts/listInfo/IListInfoWebPartProps.ts** und erweitern Sie die Schnittstellendefinition mit der Typzeichenfolgen-Eigenschaft **listName**.</span><span class="sxs-lookup"><span data-stu-id="19215-160">Next, in the code editor open the **./src/webparts/listInfo/IListInfoWebPartProps.ts** file and extend the interface definition with the **listName** property of type string.</span></span>

```ts
export interface IListInfoWebPartProps {
  description: string;
  listName: string;
}
```

<span data-ttu-id="19215-161">Fügen Sie als Letztes die neue Webpart-Eigenschaft hinzu, indem Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts** öffnen und die Implementation der Methode **getPropertyPaneConfiguration** wie folgt ändern:</span><span class="sxs-lookup"><span data-stu-id="19215-161">Finish adding the new web part property, by opening in the code editor the **./src/webparts/listInfo/ListInfoWebPart.ts** file and changing the implementation of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
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
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="19215-162">Fügen Sie die fehlende Ressourcenzeichenfolge **ListNameFieldLabel** hinzu, indem Sie den Code der Datei **./src/webparts/listInfo/loc/mystrings.d.ts** wie folgt ändern:</span><span class="sxs-lookup"><span data-stu-id="19215-162">Add the missing **ListNameFieldLabel** resource string by changing the code of the **./src/webparts/listInfo/loc/mystrings.d.ts** file to:</span></span>

```ts
declare interface IListInfoStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  DescriptionFieldLabel: string;
  ListNameFieldLabel: string;
}

declare module 'listInfoStrings' {
  const strings: IListInfoStrings;
  export = strings;
}
```

<span data-ttu-id="19215-163">Ändern Sie den Code von **./src/webparts/listInfo/loc/en-us.js** in:</span><span class="sxs-lookup"><span data-stu-id="19215-163">and the code of the **./src/webparts/listInfo/loc/en-us.js** to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "DescriptionFieldLabel": "Description Field",
    "ListNameFieldLabel": "List name"
  }
});
```

<span data-ttu-id="19215-164">Führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Projekt ausgeführt wird und die neu hinzugefügte Listennameneigenschaft im Eigenschaftenbereich des Webparts angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="19215-164">Run the following command to verify that the project is running and that the newly added list name property is displayed in the web part property pane:</span></span>

```sh
gulp serve
```

![Im Eigenschaftenbereich des Webparts angezeigte Listennameneigenschaft](../../../images/property-validation-list-name-property.png)

#### <a name="validate-the-name-of-the-list-using-the-sharepoint-rest-api"></a><span data-ttu-id="19215-166">Überprüfen des Listennamens mithilfe der SharePoint REST-API</span><span class="sxs-lookup"><span data-stu-id="19215-166">Validate the name of the list using the SharePoint REST API</span></span>

<span data-ttu-id="19215-167">In diesem Schritt überprüfen Sie den angegebenen Namen der Liste und prüfen, ob dieser einer vorhandenen Liste auf der aktuellen SharePoint-Website entspricht.</span><span class="sxs-lookup"><span data-stu-id="19215-167">In this step you will validate the provided list name and check if it corresponds to an existing list in the current SharePoint site.</span></span>

<span data-ttu-id="19215-168">Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts** und fügen Sie die folgenden Referenzen hinzu:</span><span class="sxs-lookup"><span data-stu-id="19215-168">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file and add the following references:</span></span>

```ts
import { SPHttpClient, SPHttpClientResponse } from '@microsoft/sp-http';
import { escape } from '@microsoft/sp-lodash-subset';
```

<span data-ttu-id="19215-169">Fügen Sie als Nächstes in der Klasse **ListInfoWebPart** die Methode **validateListName** mit dem folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="19215-169">Next, to the **ListInfoWebPart** class add the **validateListName** method with the following code:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

  private validateListName(value: string): Promise<string> {
    return new Promise<string>((resolve: (validationErrorMessage: string) => void, reject: (error: any) => void): void => {
      if (value === null ||
        value.length === 0) {
        resolve('Provide the list name');
        return;
      }

      this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + `/_api/web/lists/getByTitle('${escape(value)}')?$select=Id`, SPHttpClient.configurations.v1)
        .then((response: SPHttpClientResponse): void => {
          if (response.ok) {
            resolve('');
            return;
          }
          else if (response.status === 404) {
            resolve(`List '${escape(value)}' doesn't exist in the current site`);
            return;
          }
          else {
            resolve(`Error: ${response.statusText}. Please try again`);
            return;
          }
        })
        .catch((error: any): void => {
          resolve(error);
        });
    });
  }
}
```

<span data-ttu-id="19215-p114">Zuerst überprüft die Methode **validateListName**, ob ein Listenname bereitgestellt wurde. Wenn dies nicht der Fall ist, wird die Zusage mit dem entsprechenden Überprüfungsfehler aufgelöst. Hat der Benutzer einen Listennamen angegeben, verwendet die Methode **validateListName** den **SPHttpClient**, um die SharePoint REST-API aufzurufen und zu überprüfen, ob eine Liste mit diesem Namen existiert.</span><span class="sxs-lookup"><span data-stu-id="19215-p114">First, the **validateListName** method checks if a list name has been provided. If not, it resolves the promise with a relevant validation error. If the user has provided a list name, the **validateListName** method uses the **SPHttpClient** to call the SharePoint REST API and check if the list with the specified name exists.</span></span>

<span data-ttu-id="19215-p115">Wenn die Liste mit dem angegebenen Namen auf der aktuellen Website vorhanden ist, wird der Statuscode „200 OK“ zurückgegeben und die Methode **validateListName** löst die Zusage mit einer leeren Zeichenfolge auf, die bestätigt, dass der angegebene Wert eine gültige Liste darstellt. Ist die Liste mit dem angegebenen Namen nicht vorhanden, wird als Antwort ein anderer Code zurückgegeben. In der Regel lautet die Antwort „404 Not Found“; es kann jedoch auch ein anderer Statuscode zurückgegeben werden, wenn bei der Anforderung auf andere Weise ein Fehler aufgetreten ist. In beiden Fällen zeigt die Methode **validateListName** dem Benutzer die entsprechende Fehlermeldung an.</span><span class="sxs-lookup"><span data-stu-id="19215-p115">If the list with the specified name exists in the current site, the response will return a 200 OK status code and the **validateListName** method will resolve the promise with an empty string, confirming that the provided value represents a valid list. If the list with the specified name doesn't exist, the response will return a different code. Typically it will be a 404 Not Found response, but if the request failed in some other way a different status code can be returned. In both cases the **validateListName** method will display a relevant error message to the user.</span></span>

<span data-ttu-id="19215-p116">Nach dem Definieren der Überprüfungsmethode für den Listennamen wird diese im nächsten Schritt als Validierungshandler für die Webpart-Eigenschaft **listName** konfiguriert. Ersetzen Sie in der Klasse **ListInfoWebPart** den Code der Methode **getPropertyPaneConfiguration** durch:</span><span class="sxs-lookup"><span data-stu-id="19215-p116">With the list name validation method defined, the next step is to configure it as the validation handler for the **listName** web part property. In the **ListInfoWebPart** class replace the code of the **getPropertyPaneConfiguration** method with:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
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
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel,
                  onGetErrorMessage: this.validateListName.bind(this)
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="19215-179">Führen Sie den folgenden Befehl aus, um das Ergebnis der Überprüfung zu sehen:</span><span class="sxs-lookup"><span data-stu-id="19215-179">Run the following command to see the result of the validation:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="19215-180">Da die Listennamen-Überprüfungsmethode mit der SharePoint REST-API kommuniziert, müssen Sie den Webpart in der gehosteten Version der SharePoint-Workbench testen.</span><span class="sxs-lookup"><span data-stu-id="19215-180">Because the list name validation method communicates with the SharePoint REST API, you have to test the web part in the hosted version of the SharePoint workbench.</span></span>

<span data-ttu-id="19215-p117">Fügen Sie den Webpart zum Zeichenbereich hinzu, und öffnen Sie dessen Eigenschaften. Da Sie keinen Standardwert für den Listennamen angegeben haben, dies aber eine erforderliche Eigenschaft ist, wird Ihnen ein Überprüfungsfehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="19215-p117">Add the web part to the canvas and open its properties. Because you haven't specified a default value for the list name, which is a required property, you will see a validation error.</span></span>

![Angezeigter Überprüfungsfehler in einer erforderlichen Eigenschaft ohne angegebenen Wert](../../../images/property-validation-empty-list-name-error.png)

<span data-ttu-id="19215-184">Wenn Sie einen nicht vorhandenen Listennamen angeben, zeigt der Webpart einen Überprüfungsfehler an, der besagt, dass die angegebene Liste auf der aktuellen Website nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="19215-184">If you provide a name of a list that doesn't exist, the web part will display a validation error stating that the list you specified doesn't exist in the current site.</span></span>

![Angezeigter Überprüfungsfehler nach Angabe des Namens einer Liste, die auf der aktuellen Website nicht vorhanden ist](../../../images/property-validation-invalid-list-name-error.png)

<span data-ttu-id="19215-186">Wenn Sie den Namen einer vorhandenen Liste angeben, wird der Validierungsfehler ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="19215-186">If you specify a name of an existing list, the validation error will disappear.</span></span>

![Kein Fehler angezeigt bei gültigem Listennamen](../../../images/property-validation-valid-list-name.png)

#### <a name="optimize-validation-using-remote-apis"></a><span data-ttu-id="19215-188">Optimieren der Überprüfung mithilfe von Remote-APIs</span><span class="sxs-lookup"><span data-stu-id="19215-188">Optimize validation using remote APIs</span></span>

<span data-ttu-id="19215-p118">Beim Überprüfen von Webpart-Eigenschaften mit Remote-APIs überwacht SharePoint Framework Änderungen an den Steuerelementen des Eigenschaftenbereichs und sendet die aktualisierten Werte zur Überprüfung an den angegebenen Überprüfungshandler. Standardmäßig wartet SharePoint Framework 200 ms, bevor das Überprüfungsverfahren ausgelöst wird. Wenn der Benutzer den Wert von 200 ms nicht geändert hat, wird das Überprüfungsverfahren von SharePoint Framework gestartet. Wenn der Überprüfungshandler eine Remote-API verwendet, sendet diese Methode bei jedem Start des Überprüfungsverfahrens eine Webanforderung an die API, um den angegebenen Wert zu überprüfen. Schreibt der Benutzer nicht schnell genug, werden nur teilweise fertiggestellte Werte zur Überprüfung gesendet, was eine unnötige Belastung für das Netzwerk und die API darstellt. In solchen Fällen sollten Sie die Verzögerung der Überprüfung erhöhen.</span><span class="sxs-lookup"><span data-stu-id="19215-p118">When validating web part properties using remote APIs, SharePoint Framework monitors changes in the property pane controls and sends updated values for validation to the specified validation handler. By default, the SharePoint Framework waits 200ms before triggering the validation process. If the user hasn't changed the particular value for 200ms, the SharePoint Framework will start the validation process. When the validation handler uses a remote API, each time the validation process starts, that method will issue a web request to the API to validate the specified value. If users don't type fast enough, this will result in partially completed values being sent over for validation unnecessarily stressing the network and the API. In such cases you should consider increasing the validation delay.</span></span>

![Netzwerktools in Microsoft Edge zeigen Webanforderungen mit unvollständigen Listennamen, die zur Überprüfung gesendet werden](../../../images/property-validation-partial-list-name-validation.png)

<span data-ttu-id="19215-p119">Sie können die Überprüfungsverzögerung für jede Eigenschaft separat konfigurieren, je nach dem Typ des Werts, den der Benutzer angeben muss. Folgende Schritte veranschaulichen, wie die Überprüfungsverzögerung für die Eigenschaft **listName** erhöht wird.</span><span class="sxs-lookup"><span data-stu-id="19215-p119">You can configure the validation delay for each property separately, depending on the type of value that users need to provide. Following steps illustrate how to increase the validation delay for the **listName** property.</span></span>

<span data-ttu-id="19215-p120">Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts**. Ändern Sie den Code der Methode **getPropertyPaneConfiguration** in:</span><span class="sxs-lookup"><span data-stu-id="19215-p120">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. Change the code of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
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
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel,
                  onGetErrorMessage: this.validateListName.bind(this),
                  deferredValidationTime: 500
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}

```

<span data-ttu-id="19215-200">Die Eigenschaft **deferredValidationTime** gibt die Anzahl Millisekunden an, die das SharePoint Framework abwartet, bevor es den Überprüfungsprozess startet.</span><span class="sxs-lookup"><span data-stu-id="19215-200">The **deferredValidationTime** property specifies the number of milliseconds that the SharePoint Framework will wait before starting the validation process.</span></span>

<span data-ttu-id="19215-201">Überprüfen Sie mit dem folgenden Befehl, ob die angewandte Verzögerung wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="19215-201">Run the following command to see that the applied delay is working as expected:</span></span>

```sh
gulp serve --nobrowser
```
