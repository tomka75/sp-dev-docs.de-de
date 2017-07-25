<span data-ttu-id="6003f-p101">Diese API sollte zum Aktualisieren des Inhalts des PropertyPane verwendet werden. Diese API wird am Ende des Lebenszyklus des Webparts auf einer Seite aufgerufen. Sie sollte zum Entfernen lokaler Ressourcen (d. h. DOM-Elemente) verwendet werden, die das Webpart speichert. Diese API wird in Szenarien wie z. B. die Seitennavigation aufgerufen, der Host geht daher von einer Seite auf eine andere über und entfernt die Seite, die er verlässt.</span><span class="sxs-lookup"><span data-stu-id="6003f-p101">This API should be used to refresh the contents of the PropertyPane. This API is called at the end of the web part lifecycle on a page. It should be used to dispose any local resources (i.e. DOM elements) that the web part is holding onto. This API is expected to be called in scenarios like page navigation i.e. the host is transitioning from one page to another and disposes the page that is being transitioned out.</span></span>




Diese API sollte zum Aktualisieren des Inhalts des PropertyPane verwendet werden. Diese API wird am Ende des Lebenszyklus des Webparts auf einer Seite aufgerufen. Sie sollte zum Entfernen lokaler Ressourcen (d. h. DOM-Elemente) verwendet werden, die das Webpart speichert. Diese API wird in Szenarien wie z. B. die Seitennavigation aufgerufen, der Host geht daher von einer Seite auf eine andere über und entfernt die Seite, die er verlässt.

<span data-ttu-id="6003f-106">**Signatur:** _@virtual protected onDispose(): void;_</span><span class="sxs-lookup"><span data-stu-id="6003f-106">**Signature:** _@virtual protected onDispose(): void;_</span></span>

<span data-ttu-id="6003f-107">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="6003f-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="6003f-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="6003f-108">Parameters</span></span>
<span data-ttu-id="6003f-109">Keine</span><span class="sxs-lookup"><span data-stu-id="6003f-109">None</span></span>


