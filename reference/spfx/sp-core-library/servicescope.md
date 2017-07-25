<span data-ttu-id="d1e29-p107">Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d1e29-p107">It is an error to call ServiceScope.consume() before finish() has been called. The most reliable way to protect your component against this error is to perform the consume() calls inside a whenFinished() callback. If the service scope is already finished, then the callback will be executed immediately; otherwise, it will be executed later when the scope is finished.</span></span> |
|[`whenFinished(callback)`](whenfinished-servicescope.md)     | `public` | `void` | Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt. |





