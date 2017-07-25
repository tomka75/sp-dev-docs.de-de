# <a name="irandomnumbergenerator-interface"></a><span data-ttu-id="1a69c-101">IRandomNumberGenerator-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="1a69c-101">IRandomNumberGenerator interface</span></span>







<span data-ttu-id="1a69c-102">Dies ist eine ServiceScope-Schnittstelle, über die Komponententests eine deterministische Quelle für Pseudozufallszahlen bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="1a69c-102">This is a ServiceScope interface that enables unit tests to provide a deterministic source of pseudorandom numbers.</span></span>







## <a name="methods"></a><span data-ttu-id="1a69c-103">Methoden</span><span class="sxs-lookup"><span data-stu-id="1a69c-103">Methods</span></span>

| <span data-ttu-id="1a69c-104">Methode</span><span class="sxs-lookup"><span data-stu-id="1a69c-104">Method</span></span>       |  <span data-ttu-id="1a69c-105">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="1a69c-105">Returns</span></span>   | <span data-ttu-id="1a69c-106">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a69c-106">Description</span></span>|
|:-------------|:-------|:-----------|
|[`generate()`](generate-irandomnumbergenerator.md)      | `number` | <span data-ttu-id="1a69c-107">Gibt eine Pseudozufallszahl zwischen 0 (einschließlich) und 1 (ausschließlich) gemäß des Math.random()-Vertrags zurück.</span><span class="sxs-lookup"><span data-stu-id="1a69c-107">Returns a psuedorandom number between 0 (inclusive) and 1 (exclusive), following the contract of Math.random().</span></span> |




