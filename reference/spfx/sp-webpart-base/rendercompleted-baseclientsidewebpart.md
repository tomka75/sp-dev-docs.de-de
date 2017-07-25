<span data-ttu-id="1cff7-p101">Diese API sollte von Webparts aufgerufen werden, die ein asynchrones Rendering durchführen. Diese Webparts müssen die IsRenderAsync-API überschreiben und „true“ zurückgeben. Ein Beispiel hierfür sind Webparts, die Inhalte in einem IFrame rendern. Das Webpart initiiert die IFrame-Darstellung in der render()-API, aber das tatsächliche Rendern wird erst abgeschlossen, nachdem der Ladevorgang des IFrame abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="1cff7-p101">This API should be called by web parts that perform Async rendering. Those web part are required to override the isRenderAsync API and return true. One such example is web parts that render content in an IFrame. The web part initiates the IFrame rendering in the render() API but the actual rendering is complete only after the iframe loading completes.</span></span>




Diese API sollte von Webparts aufgerufen werden, die ein asynchrones Rendering durchführen. Diese Webparts müssen die IsRenderAsync-API überschreiben und „true“ zurückgeben. Ein Beispiel hierfür sind Webparts, die Inhalte in einem IFrame rendern. Das Webpart initiiert die IFrame-Darstellung in der render()-API, aber das tatsächliche Rendern wird erst abgeschlossen, nachdem der Ladevorgang des IFrame abgeschlossen ist.

<span data-ttu-id="1cff7-106">**Signatur:** _protected renderCompleted(): void;_</span><span class="sxs-lookup"><span data-stu-id="1cff7-106">**Signature:** _protected renderCompleted(): void;_</span></span>

<span data-ttu-id="1cff7-107">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="1cff7-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="1cff7-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="1cff7-108">Parameters</span></span>
<span data-ttu-id="1cff7-109">Keine</span><span class="sxs-lookup"><span data-stu-id="1cff7-109">None</span></span>


