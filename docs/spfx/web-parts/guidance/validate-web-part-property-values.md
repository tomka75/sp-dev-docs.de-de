<span data-ttu-id="32723-p120">Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts**. Ändern Sie den Code der Methode **getPropertyPaneConfiguration** in:</span><span class="sxs-lookup"><span data-stu-id="32723-p120">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. Change the code of the **getPropertyPaneConfiguration** method to:</span></span>

Öffnen Sie im Code-Editor die Datei **./src/webparts/listInfo/ListInfoWebPart.ts**. Ändern Sie den Code der Methode **getPropertyPaneConfiguration** in:

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

<span data-ttu-id="32723-198">Die Eigenschaft **deferredValidationTime** gibt die Anzahl Millisekunden an, die das SharePoint Framework abwartet, bevor es den Überprüfungsprozess startet.</span><span class="sxs-lookup"><span data-stu-id="32723-198">The **deferredValidationTime** property specifies the number of milliseconds that the SharePoint Framework will wait before starting the validation process.</span></span>

<span data-ttu-id="32723-199">Überprüfen Sie mit dem folgenden Befehl, ob die angewandte Verzögerung wie erwartet funktioniert:</span><span class="sxs-lookup"><span data-stu-id="32723-199">Run the following command to see that the applied delay is working as expected:</span></span>

```sh
gulp serve --nobrowser
```