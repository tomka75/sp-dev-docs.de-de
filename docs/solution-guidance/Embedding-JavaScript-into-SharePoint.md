---
title: Einbetten von JavaScript in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: efb690bf90fcba627287e6d25f8bb3bb0442752a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="embedding-javascript-into-sharepoint"></a><span data-ttu-id="9dca1-102">Einbetten von JavaScript in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dca1-102">Embedding JavaScript into SharePoint</span></span>

<span data-ttu-id="9dca1-103">Namespaces können Sie Konflikte zwischen Ihrem JavaScript Anpassungen und standard durch andere Entwickler bereitgestellte SharePoint JavaScript oder JavaScript Anpassungen zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="9dca1-103">You can use namespaces to avoid conflicts between your JavaScript customizations and standard SharePoint JavaScript or JavaScript customizations deployed by other developers.</span></span> 

<span data-ttu-id="9dca1-104">Die Beispiele [OfficeDev/PnP](https://github.com/SharePoint/PnP/) und -Lösungen enthalten häufig JavaScript-Code.</span><span class="sxs-lookup"><span data-stu-id="9dca1-104">The [OfficeDev/PnP](https://github.com/SharePoint/PnP/) samples and solutions often include JavaScript code.</span></span> <span data-ttu-id="9dca1-105">Um der Techniken, die einfach zu verstehen stellen Sie, in diesen Beispielen werden in der Regel einfach und Namespaces beim Einbetten von JavaScript-Code in SharePoint nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="9dca1-105">In order to make the techniques easy to understand, these samples are usually simple and do not use namespaces when embedding JavaScript code into SharePoint.</span></span> <span data-ttu-id="9dca1-106">Es ist wichtig, um sicherzustellen, dass Sie führen Sie die Schritte in diesem Artikel beschriebenen, wenn Sie Plug & Play-Beispiele in Ihre Lösungen integrieren.</span><span class="sxs-lookup"><span data-stu-id="9dca1-106">It is important to ensure that you follow the simple steps outlined in this article when you incorporate PnP samples into your solutions.</span></span>

## <a name="why-using-namespaces-is-important"></a><span data-ttu-id="9dca1-107">Warum ist die Verwendung von Namespaces wichtig</span><span class="sxs-lookup"><span data-stu-id="9dca1-107">Why using namespaces is important</span></span>
<span data-ttu-id="9dca1-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9dca1-108"></span></span>

<span data-ttu-id="9dca1-109">JavaScript ist eine locker Sprache.</span><span class="sxs-lookup"><span data-stu-id="9dca1-109">JavaScript is a loosely typed language.</span></span> <span data-ttu-id="9dca1-110">Wenn Sie eine Variable oder Funktion definieren und eine Variable oder eine Funktion mit dem gleichen Namen bereits im aktuellen Kontext vorhanden ist, wird der neue Wert oder Implementierung vorhandenen ersetzen.</span><span class="sxs-lookup"><span data-stu-id="9dca1-110">If you define a variable or function, and a variable or function with the same name already exists in the current context, the new value or implementation will replace the existing one.</span></span>
<span data-ttu-id="9dca1-111">Vorkommen, wenn Sie JavaScript-Code in SharePoint einbetten, ist es einfach standard SharePoint JavaScript-Code oder von anderen Entwicklern bereitgestellte Anpassungen außer Kraft gesetzt.</span><span class="sxs-lookup"><span data-stu-id="9dca1-111">As a result, when you embed JavaScript code into SharePoint, it is easy to override standard SharePoint JavaScript code or customizations deployed by other developers.</span></span>
<span data-ttu-id="9dca1-112">Dadurch kann Konflikte erstellen, die möglicherweise schwer zu identifizieren und zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="9dca1-112">This can create conflicts that might be hard to identify and debug.</span></span>

<span data-ttu-id="9dca1-113">Um dies zu vermeiden, sollten Sie benutzerdefinierte Namespaces für Ihren JavaScript-Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="9dca1-113">To avoid this, we recommend that you use custom namespaces for your JavaScript code.</span></span>

## <a name="how-to-use-namespaces"></a><span data-ttu-id="9dca1-114">Gewusst wie: Verwenden von namespaces</span><span class="sxs-lookup"><span data-stu-id="9dca1-114">How to use namespaces</span></span>
<span data-ttu-id="9dca1-115"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9dca1-115"></span></span>

<span data-ttu-id="9dca1-116">Das folgende Beispiel zeigt ein einfaches Muster verwendet, um JavaScript-Code in Namespaces und Klassen zu organisieren.</span><span class="sxs-lookup"><span data-stu-id="9dca1-116">The following example shows a simple pattern used to organize JavaScript code in namespaces and classes.</span></span>

```JavaScript
var MySolution = MySolution || {};

MySolution.MyClass1 = (function () {
    // private members
    var privateVar1 = 1;
    var privateVar2 = 2;
    
    function privateFunction1(){
      return "";
    }
    
    return {
        // public interface
        myFunction1: function() {
          return privateVar1;
        },
        myFunction2: function(){
          return privateVar2;
        }
    };
})();
```

<span data-ttu-id="9dca1-117">Funktionen in öffentliche Schnittstelle können als aufgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="9dca1-117">Functions defined in public interface can be invoked as:</span></span>

```JavaScript
MySolution.MyClass1.myFunction1();

MySolution.MyClass1.myFunction2();
```

<span data-ttu-id="9dca1-118">Da alle Codes den benutzerdefinierten *MySolution* Namespace verwendet wird, können Sie Namenskonflikte vermeiden.</span><span class="sxs-lookup"><span data-stu-id="9dca1-118">Because all your code uses the custom *MySolution* namespace, you can avoid any naming conflicts.</span></span>

## <a name="namespaces-and-minimal-download-strategy-mds"></a><span data-ttu-id="9dca1-119">Namespaces und minimale Downloadstrategie (MDS)</span><span class="sxs-lookup"><span data-stu-id="9dca1-119">Namespaces and Minimal Download Strategy (MDS)</span></span>

<span data-ttu-id="9dca1-120">Die [Minimale herunterladen Strategie Feature](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) aktiviert ist werden globale Namespaces und Variablen auf MDS Navigationsbereich deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="9dca1-120">With the [Minimal Download Strategy Feature](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) enabled, Global Namespaces and Variables are cleared on MDS navigation.</span></span>   
<span data-ttu-id="9dca1-121">Um Ihre Namespace beizubehalten, deklarieren Sie sie als:</span><span class="sxs-lookup"><span data-stu-id="9dca1-121">To retain your Namespace, declare it as:</span></span>

```JavaScript
    Type.registerNamespace('MySolution');
```

<span data-ttu-id="9dca1-122">Der Typ Namespace gilt nur für SharePoint, für eine generische Verwendung des JavaScript-Bibliothek:</span><span class="sxs-lookup"><span data-stu-id="9dca1-122">The Type Namespace is specific to SharePoint,  for a generic JavaScript library use:</span></span>

```JavaScript
if (window.hasOwnProperty('Type')) {
    Type.registerNamespace('MySolution');
} else {
    window.MySolution = window.MySolution || {};
}
```

#### <a name="namespaces-mds-and-csr-client-side-rendering"></a><span data-ttu-id="9dca1-123">Namespaces, MDS und CSR (Client Side Rendering)</span><span class="sxs-lookup"><span data-stu-id="9dca1-123">Namespaces, MDS and CSR (Client Side Rendering)</span></span>

<span data-ttu-id="9dca1-124">Die ``RegisterModuleInit`` Funktion deklariert eine richtige ``Type`` Namespace.</span><span class="sxs-lookup"><span data-stu-id="9dca1-124">The ``RegisterModuleInit`` function declares a proper ``Type`` Namespace.</span></span>  
<span data-ttu-id="9dca1-125">Dateien mit JSLink angefügt sind **nicht** auf MDS Navigation erneut ausgeführt, verwenden Sie die AsyncDeltaManager-Funktionen, die für die.</span><span class="sxs-lookup"><span data-stu-id="9dca1-125">Files attached with JSLink are **not** re-executed on MDS navigation, use the AsyncDeltaManager functions for that.</span></span>

### <a name="resources"></a><span data-ttu-id="9dca1-126">Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="9dca1-126">Resources:</span></span>

* [<span data-ttu-id="9dca1-127">Wictor Wilén - ordnungsgemäße auszuführende Javascript-Funktionen in SharePoint MDS-fähige Websites</span><span class="sxs-lookup"><span data-stu-id="9dca1-127">Wictor Wilén - The correct way to execute javascript functions in SharePoint MDS enabled sites</span></span>](http://www.wictorwilen.se/the-correct-way-to-execute-javascript-functions-in-sharepoint-2013-mds-enabled-sites)
* [<span data-ttu-id="9dca1-128">Hugh Wood - Kontext-Entwicklung für SharePoint JavaScript - AsyncDeltaManager</span><span class="sxs-lookup"><span data-stu-id="9dca1-128">Hugh Wood - SharePoint JavaScript context development - AsyncDeltaManager</span></span>](https://www.spcaf.com/blog/sharepoint-javascript-context-development-part-4-the-way-of-the-async-delta-manager/)
* [<span data-ttu-id="9dca1-129">Marc Anderson - JavaScript ausführen nach MDS (Load neu)</span><span class="sxs-lookup"><span data-stu-id="9dca1-129">Marc Anderson - Execute JavaScript after MDS (re)load</span></span>](http://blog.symprogress.com/2013/09/sharepoint-2013-execute-javascript-function-after-mds-load/)
