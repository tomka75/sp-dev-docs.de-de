<span data-ttu-id="c5e91-p108">Diese Klasse stellt Versionen dar, die das Zeichenfolgenformat MAJOR.MINOR[.PATCH[.REVISION]] aufweisen, wobei MAJOR, MINOR, PATCH und REVISION ganze Zahlen sind. PATCH und REVISION sind optional. Vorangestellte Nullen sind zulässig, haben aber bei Vergleichen keine Bedeutung. Beispiele: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004</span><span class="sxs-lookup"><span data-stu-id="c5e91-p108">This class represents versions that follow the string format of MAJOR.MINOR[.PATCH[.REVISION]] where MAJOR, MINOR, PATCH and REVISION are integers. PATCH and REVISION are optional. Leading zeros are allowed, but have no meaning in comparisons. Examples: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004</span></span> |
| [`Version`](./sp-core-library/version.md)     | Diese Klasse stellt Versionen dar, die das Zeichenfolgenformat MAJOR.MINOR[.PATCH[.REVISION]] aufweisen, wobei MAJOR, MINOR, PATCH und REVISION ganze Zahlen sind. PATCH und REVISION sind optional. Vorangestellte Nullen sind zulässig, haben aber bei Vergleichen keine Bedeutung. Beispiele: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004 |



## <a name="interfaces"></a><span data-ttu-id="c5e91-154">Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="c5e91-154">Interfaces</span></span>

| <span data-ttu-id="c5e91-155">Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="c5e91-155">Interface</span></span>    |  <span data-ttu-id="c5e91-156">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c5e91-156">Description</span></span> |
|:-------------|:---------------|
| [`IRandomNumberGenerator`](./sp-core-library/irandomnumbergenerator.md)   | <span data-ttu-id="c5e91-157">Dies ist eine ServiceScope-Schnittstelle, über die Komponententests eine deterministische Quelle für Pseudozufallszahlen bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="c5e91-157">This is a ServiceScope interface that enables unit tests to provide a deterministic source of pseudorandom numbers.</span></span>  |
| [`IServiceCollection`](./sp-core-library/iservicecollection.md)   | <span data-ttu-id="c5e91-158">Ein Muster in Kurzschrift zum Extrahieren bekannter Dienste aus einem ServiceScope.</span><span class="sxs-lookup"><span data-stu-id="c5e91-158">A shorthand pattern for extracting well-known services from a ServiceScope.</span></span>  |
| [`ITimeProvider`](./sp-core-library/itimeprovider.md)   | <span data-ttu-id="c5e91-159">Dies ist eine ServiceScope-Schnittstelle, über die Komponententests die Systemuhr simulieren können.</span><span class="sxs-lookup"><span data-stu-id="c5e91-159">This is a ServiceScope interface that enables unit tests to simulate the system clock.</span></span>  |



## <a name="enumerations"></a><span data-ttu-id="c5e91-160">Enumerationen</span><span class="sxs-lookup"><span data-stu-id="c5e91-160">Enumerations</span></span>

| <span data-ttu-id="c5e91-161">Enumeration</span><span class="sxs-lookup"><span data-stu-id="c5e91-161">Enumeration</span></span>      | <span data-ttu-id="c5e91-162">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c5e91-162">Description</span></span>|
|:-----------|:------------|
|[`DisplayMode`](./sp-core-library/displaymode.md)    | <span data-ttu-id="c5e91-163">DisplayMode gibt den Modus an, in dem eine Seite und/oder deren Inhalt (z. B. Text und Webparts) angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c5e91-163">DisplayMode indicates the mode in which a page and/or its contents (e.g. text and web parts) are dislayed.</span></span> |
|[`EnvironmentType`](./sp-core-library/environmenttype.md)    | <span data-ttu-id="c5e91-164">Eine Aufzählung, die beschreibt, in welcher Art von Umgebung das Framework ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c5e91-164">An enum that describes which type of enviroment the framework is running in.</span></span> |




