<span data-ttu-id="661d2-p101">Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="661d2-p101">It is an error to call ServiceScope.consume() before finish() has been called. The most reliable way to protect your component against this error is to perform the consume() calls inside a whenFinished() callback. If the service scope is already finished, then the callback will be executed immediately; otherwise, it will be executed later when the scope is finished.</span></span>




Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt.

<span data-ttu-id="661d2-105">**Signatur:** _public whenFinished(callback: () => void): void;_</span><span class="sxs-lookup"><span data-stu-id="661d2-105">**Signature:** _public whenFinished(callback: () => void): void;_</span></span>

<span data-ttu-id="661d2-106">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="661d2-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="661d2-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="661d2-107">Parameters</span></span>


| <span data-ttu-id="661d2-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="661d2-108">Parameter</span></span>    | <span data-ttu-id="661d2-109">Typ</span><span class="sxs-lookup"><span data-stu-id="661d2-109">Type</span></span>    | <span data-ttu-id="661d2-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="661d2-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `callback`    | `() => void` | <span data-ttu-id="661d2-111">Ein Codeblock, der ServiceScope.consume() aufrufen muss</span><span class="sxs-lookup"><span data-stu-id="661d2-111">A block of code that needs to call ServiceScope.consume()</span></span> |


