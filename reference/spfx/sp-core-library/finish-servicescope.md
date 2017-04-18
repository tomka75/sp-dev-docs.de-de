# <a name="finish"></a>finish()




Wenn ein ServiceScope zum ersten Mal gestartet wird, ist er ein "nicht beendeter" Zustand, in dem provide() zulässig ist, consume() aber nicht zulässig ist. Nach dem Aufrufen von finish() gefolgt von consume() ist consume() zulässig, provide() aber nicht. Dieser Formalismus beseitigt vollständig eine Anzahl von schwierigen Fehlern, z. B.: Scope2 ist ein untergeordnetes Element von Scope1 und Scope1 stellt Instanz A1 von Schnittstelle A bereit; Wenn jemand A1 aus Scope2 (über die Vererbung) nutzt, bevor Scope2.provide() mit A2 aufgerufen wird, gibt ein nachfolgender Aufruf von Scope2.consume() möglicherweise ein anderes Ergebnis als der vorherige Aufruf zurück, was für Entwickler sehr verwirrend wäre.

**Signature:** _public finish(): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter
Keine


