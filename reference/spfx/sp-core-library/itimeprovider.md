# <a name="itimeprovider-interface"></a><span data-ttu-id="600d6-101">ITimeProvider-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="600d6-101">ITimeProvider interface</span></span>







<span data-ttu-id="600d6-102">Dies ist eine ServiceScope-Schnittstelle, über die Komponententests die Systemuhr simulieren können.</span><span class="sxs-lookup"><span data-stu-id="600d6-102">This is a ServiceScope interface that enables unit tests to simulate the system clock.</span></span>







## <a name="methods"></a><span data-ttu-id="600d6-103">Methoden</span><span class="sxs-lookup"><span data-stu-id="600d6-103">Methods</span></span>

| <span data-ttu-id="600d6-104">Methode</span><span class="sxs-lookup"><span data-stu-id="600d6-104">Method</span></span>       |  <span data-ttu-id="600d6-105">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="600d6-105">Returns</span></span>   | <span data-ttu-id="600d6-106">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="600d6-106">Description</span></span>|
|:-------------|:-------|:-----------|
|[`getDate()`](getdate-itimeprovider.md)      | `Date` | <span data-ttu-id="600d6-107">Gibt das aktuelle Datum/die aktuelle Uhrzeit zurück.</span><span class="sxs-lookup"><span data-stu-id="600d6-107">Returns the current date/time.</span></span> |
|[`getTimestamp()`](gettimestamp-itimeprovider.md)      | `number` | <span data-ttu-id="600d6-108">Gibt eine DOMHighResTimeStamp-Zeitmessung, wie von der Standard-API performance.now() definiert, zurück.</span><span class="sxs-lookup"><span data-stu-id="600d6-108">Returns a DOMHighResTimeStamp timing measurement, as defined by the standard performance.now() API.</span></span> |




