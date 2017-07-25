<span data-ttu-id="d7f96-p101">Diese API wird aufgerufen, bevor das Webpart serialisiert wird. Für die Standardimplementierung ist keine Aktion erforderlich. Ein Webpartentwickler kann diese API überschreiben, wenn der Status des Webparts nicht vollständig im Eigenschaftenbehälter, d. h. in diesen Eigenschaften nicht vollständig wiedergegeben wird. Auf diese Weise können Webentwickler den Eigenschaftenbehälter direkt vor der Serialisierung aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="d7f96-p101">This API is called before the web part is serialized. The default implementation is a no-op. A web part developer can override this API when the web part's state is not fully reflected in the property bag i.e. this.properties. This gives the web part developer a chance to update the property bag right before serialization.</span></span>




Diese API wird aufgerufen, bevor das Webpart serialisiert wird. Für die Standardimplementierung ist keine Aktion erforderlich. Ein Webpartentwickler kann diese API überschreiben, wenn der Status des Webparts nicht vollständig im Eigenschaftenbehälter, d. h. in diesen Eigenschaften nicht vollständig wiedergegeben wird. Auf diese Weise können Webentwickler den Eigenschaftenbehälter direkt vor der Serialisierung aktualisieren.

<span data-ttu-id="d7f96-106">**Signatur:** _@virtual protected onBeforeSerialize(): void;_</span><span class="sxs-lookup"><span data-stu-id="d7f96-106">**Signature:** _@virtual protected onBeforeSerialize(): void;_</span></span>

<span data-ttu-id="d7f96-107">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="d7f96-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="d7f96-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="d7f96-108">Parameters</span></span>
<span data-ttu-id="d7f96-109">Keine</span><span class="sxs-lookup"><span data-stu-id="d7f96-109">None</span></span>


