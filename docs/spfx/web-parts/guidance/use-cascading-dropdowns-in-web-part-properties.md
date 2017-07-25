<span data-ttu-id="1f164-p124">**Hinweis:** Ab Drop 6 des SharePoint Frameworks gibt es einen Fehler in der React-Dropdownkomponente der Office UI Fabric, der dazu führt, dass das Dropdownsteuerelement nicht ordnungsgemäß funktioniert. Eine temporäre Problemumgehung besteht darin, die Datei **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** zu bearbeiten und die Zeile **12027** von:</span><span class="sxs-lookup"><span data-stu-id="1f164-p124">**Note:** In drop 6 of the SharePoint Framework there is a bug in the Office UI Fabric React Dropdown component that causes the dropdown control to work incorrectly. A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line **12027** from:</span></span>

> **Hinweis:** Ab Drop 6 des SharePoint Frameworks gibt es einen Fehler in der React-Dropdownkomponente der Office UI Fabric, der dazu führt, dass das Dropdownsteuerelement nicht ordnungsgemäß funktioniert. Eine temporäre Problemumgehung besteht darin, die Datei **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** zu bearbeiten und die Zeile **12027** von:
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="1f164-235">in:</span><span class="sxs-lookup"><span data-stu-id="1f164-235">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

![Elementdropdown im Webpart-Eigenschaftenbereich, in dem verfügbare Listenelemente für die ausgewählte Liste angezeigt werden](../../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)
