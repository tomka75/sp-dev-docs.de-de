# <a name="iclientsidewebpartstatusrenderer-interface"></a><span data-ttu-id="e461b-101">IClientSideWebPartStatusRenderer-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e461b-101">IClientSideWebPartStatusRenderer interface</span></span>







<span data-ttu-id="e461b-102">Die Schnittstelle, die von einer Komponente implementiert wird, die den Ladeindikator und Fehlermeldungen für ein Webpart anzeigen soll.</span><span class="sxs-lookup"><span data-stu-id="e461b-102">Interface to be implemented by a component that should display the loading indicator and error messages for a webpart.</span></span>







## <a name="methods"></a><span data-ttu-id="e461b-103">Methoden</span><span class="sxs-lookup"><span data-stu-id="e461b-103">Methods</span></span>

| <span data-ttu-id="e461b-104">Methode</span><span class="sxs-lookup"><span data-stu-id="e461b-104">Method</span></span>       |  <span data-ttu-id="e461b-105">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="e461b-105">Returns</span></span>   | <span data-ttu-id="e461b-106">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e461b-106">Description</span></span>|
|:-------------|:-------|:-----------|
|[`clearError(domElement)`](clearerror-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="e461b-107">Deaktiviert die Webpart-Fehlermeldung.</span><span class="sxs-lookup"><span data-stu-id="e461b-107">Clear the webpart error message.</span></span> |
|[`clearLoadingIndicator(domElement)`](clearloadingindicator-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="e461b-108">Deaktiviert die Ladeanzeige.</span><span class="sxs-lookup"><span data-stu-id="e461b-108">Clear the loading indicator.</span></span> |
|[`displayLoadingIndicator(domElement,loadingMessage,timeout)`](displayloadingindicator-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="e461b-109">Zeigt eine Ladedrehfeld an.</span><span class="sxs-lookup"><span data-stu-id="e461b-109">Display a loading spinner.</span></span> |
|[`renderError(domElement,error)`](rendererror-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="e461b-110">Rendert die bereitgestellte Fehlermeldung im div-Webpartcontainer</span><span class="sxs-lookup"><span data-stu-id="e461b-110">Render the provided error message in the webpart container div.</span></span> |




