<span data-ttu-id="ae96d-p101">Wenn ein ServiceScope zum ersten Mal gestartet wird, ist er ein "nicht beendeter" Zustand, in dem provide() zulässig ist, consume() aber nicht zulässig ist. Nach dem Aufrufen von finish() gefolgt von consume() ist consume() zulässig, provide() aber nicht. Dieser Formalismus beseitigt vollständig eine Anzahl von schwierigen Fehlern, z. B.: Scope2 ist ein untergeordnetes Element von Scope1 und Scope1 stellt Instanz A1 von Schnittstelle A bereit; Wenn jemand A1 aus Scope2 (über die Vererbung) nutzt, bevor Scope2.provide() mit A2 aufgerufen wird, gibt ein nachfolgender Aufruf von Scope2.consume() möglicherweise ein anderes Ergebnis als der vorherige Aufruf zurück, was für Entwickler sehr verwirrend wäre.</span><span class="sxs-lookup"><span data-stu-id="ae96d-p101">When a ServiceScope is first started, it is in an "unfinished" state where provide() is allowed but consume() is not allowed. After calling finish(), then consume() is allowed but provide() is not allowed. This formalism completely eliminates a number of tricky bugs such as: Scope2 is a child of Scope1, and Scope1 provides instance A1 of interface A; if someone consumes A1 from Scope2 (via inheritance) before Scope2.provide() is called with A2, then a subsequent call to Scope2.consume() might return a different result than the previous call, which would be very confusing for developers.</span></span>




Wenn ein ServiceScope zum ersten Mal gestartet wird, ist er ein "nicht beendeter" Zustand, in dem provide() zulässig ist, consume() aber nicht zulässig ist. Nach dem Aufrufen von finish() gefolgt von consume() ist consume() zulässig, provide() aber nicht. Dieser Formalismus beseitigt vollständig eine Anzahl von schwierigen Fehlern, z. B.: Scope2 ist ein untergeordnetes Element von Scope1 und Scope1 stellt Instanz A1 von Schnittstelle A bereit; Wenn jemand A1 aus Scope2 (über die Vererbung) nutzt, bevor Scope2.provide() mit A2 aufgerufen wird, gibt ein nachfolgender Aufruf von Scope2.consume() möglicherweise ein anderes Ergebnis als der vorherige Aufruf zurück, was für Entwickler sehr verwirrend wäre.

<span data-ttu-id="ae96d-105">**Signature:** _public finish(): void;_</span><span class="sxs-lookup"><span data-stu-id="ae96d-105">**Signature:** _public finish(): void;_</span></span>

<span data-ttu-id="ae96d-106">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="ae96d-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="ae96d-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae96d-107">Parameters</span></span>
<span data-ttu-id="ae96d-108">Keine</span><span class="sxs-lookup"><span data-stu-id="ae96d-108">None</span></span>


