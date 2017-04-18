# <a name="whenfinishedcallback"></a>whenFinished(callback)




Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt.

**Signatur:** _public whenFinished(callback: () => void): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `callback`    | `() => void` | Ein Codeblock, der ServiceScope.consume() aufrufen muss |


