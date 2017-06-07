# <a name="ondisplaymodechangedolddisplaymode"></a>onDisplayModeChanged(oldDisplayMode)




Diese API wird aufgerufen, wenn der Anzeigemodus eines Webparts geändert wird. Die standardmäßige Implementierung dieser API ruft die Webpart-Rendermethode auf, um das Webpart mit dem neuen Anzeigemodus erneut zu rendern. Wenn ein Webpartentwickler nicht möchte, dass bei einer Änderung des Anzeigemodus ein erneutes Rendern auftritt, kann er diese API überschreiben und bestimmte Updates für das Webpart-DOM ausführen, um den Anzeigemodus zu wechseln.

**Signatur:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `oldDisplayMode`    | [`DisplayMode`](../sp-core-library/displaymode.md) | Der alte Anzeigemodus. |


