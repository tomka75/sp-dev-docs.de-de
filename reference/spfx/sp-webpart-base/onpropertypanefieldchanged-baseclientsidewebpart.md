# <a name="onpropertypanefieldchangedpropertypatholdvaluenewvalue"></a>onPropertyPaneFieldChanged(propertyPath,oldValue,newValue)




Diese API wird nach dem Aktualisieren des neuen Werts der Eigenschaft im Eigenschaftenbehälter aufgerufen, wenn der PropertyPane im reaktiven Modus verwendet wird. Die grundlegende Implementierung dieser API rendert das Webpart erneut.

**Signatur:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `propertyPath`    | `string` | JSON-Pfad der Eigenschaft im Eigenschaftenbehälter. |
| `oldValue`    | `any` | Der alte Wert der Eigenschaft. |
| `newValue`    | `any` | Der neue Wert der Eigenschaft. |


