<span data-ttu-id="30e87-p107">Der reaktive Modus ist zwar für viele Szenarios ausreichend, manchmal benötigen Sie aber das nicht reaktive Verhalten. Beim nicht reaktiven Verhalten wird das Webpart nicht automatisch aktualisiert, es sei denn, der Benutzer bestätigt die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="30e87-p107">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span>

Der reaktive Modus ist zwar für viele Szenarios ausreichend, manchmal benötigen Sie aber das nicht reaktive Verhalten. Beim nicht reaktiven Verhalten wird das Webpart nicht automatisch aktualisiert, es sei denn, der Benutzer bestätigt die Änderungen.

## <a name="custom-field-example"></a><span data-ttu-id="30e87-146">Beispiele für das benutzerdefinierte Feld</span><span class="sxs-lookup"><span data-stu-id="30e87-146">Custom field example</span></span>

<span data-ttu-id="30e87-147">Fügen Sie die folgende Felddefinition zu einem **groupFields**-Array hinzu.</span><span class="sxs-lookup"><span data-stu-id="30e87-147">Add the following field definition in a **groupFields** array.</span></span>

```ts
{
  type: IPropertyPaneFieldType.Custom,
  targetProperty: 'custom',
  properties: {
    onRender: this._customFieldRender.bind(this),
    value: undefined,
    context: undefined
  }
}
```

<span data-ttu-id="30e87-148">Fügen Sie die folgenden Typen zu den **@microsoft/sp-webpart-base**-Importen hinzu.</span><span class="sxs-lookup"><span data-stu-id="30e87-148">Add the following types to the **@microsoft/sp-webpart-base** imports.</span></span>

```ts
IPropertyPaneFieldType
```

<span data-ttu-id="30e87-149">Fügen Sie die folgende private Methode zum Rendern des benutzerdefinierten Felds hinzu.</span><span class="sxs-lookup"><span data-stu-id="30e87-149">Add the following private method to render the custom field.</span></span>

```ts
private _customFieldRender(elem: HTMLElement, context: any, onChanged?: IOnCustomPropertyFieldChanged): void {
    elem.innerHTML = '<input id="password" type="password" name="password" class="ms-TextField-field">';
}
```
