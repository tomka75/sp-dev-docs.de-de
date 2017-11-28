---
title: Einbetten von JavaScript in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: efb690bf90fcba627287e6d25f8bb3bb0442752a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="embedding-javascript-into-sharepoint"></a>Einbetten von JavaScript in SharePoint

Namespaces können Sie Konflikte zwischen Ihrem JavaScript Anpassungen und standard durch andere Entwickler bereitgestellte SharePoint JavaScript oder JavaScript Anpassungen zu vermeiden. 

Die Beispiele [OfficeDev/PnP](https://github.com/SharePoint/PnP/) und -Lösungen enthalten häufig JavaScript-Code. Um der Techniken, die einfach zu verstehen stellen Sie, in diesen Beispielen werden in der Regel einfach und Namespaces beim Einbetten von JavaScript-Code in SharePoint nicht verwenden. Es ist wichtig, um sicherzustellen, dass Sie führen Sie die Schritte in diesem Artikel beschriebenen, wenn Sie Plug & Play-Beispiele in Ihre Lösungen integrieren.

## <a name="why-using-namespaces-is-important"></a>Warum ist die Verwendung von Namespaces wichtig
<a name="sectionSection0"> </a>

JavaScript ist eine locker Sprache. Wenn Sie eine Variable oder Funktion definieren und eine Variable oder eine Funktion mit dem gleichen Namen bereits im aktuellen Kontext vorhanden ist, wird der neue Wert oder Implementierung vorhandenen ersetzen.
Vorkommen, wenn Sie JavaScript-Code in SharePoint einbetten, ist es einfach standard SharePoint JavaScript-Code oder von anderen Entwicklern bereitgestellte Anpassungen außer Kraft gesetzt.
Dadurch kann Konflikte erstellen, die möglicherweise schwer zu identifizieren und zu debuggen.

Um dies zu vermeiden, sollten Sie benutzerdefinierte Namespaces für Ihren JavaScript-Code verwenden.

## <a name="how-to-use-namespaces"></a>Gewusst wie: Verwenden von namespaces
<a name="sectionSection1"> </a>

Das folgende Beispiel zeigt ein einfaches Muster verwendet, um JavaScript-Code in Namespaces und Klassen zu organisieren.

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

Funktionen in öffentliche Schnittstelle können als aufgerufen werden:

```JavaScript
MySolution.MyClass1.myFunction1();

MySolution.MyClass1.myFunction2();
```

Da alle Codes den benutzerdefinierten *MySolution* Namespace verwendet wird, können Sie Namenskonflikte vermeiden.

## <a name="namespaces-and-minimal-download-strategy-mds"></a>Namespaces und minimale Downloadstrategie (MDS)

Die [Minimale herunterladen Strategie Feature](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) aktiviert ist werden globale Namespaces und Variablen auf MDS Navigationsbereich deaktiviert.   
Um Ihre Namespace beizubehalten, deklarieren Sie sie als:

```JavaScript
    Type.registerNamespace('MySolution');
```

Der Typ Namespace gilt nur für SharePoint, für eine generische Verwendung des JavaScript-Bibliothek:

```JavaScript
if (window.hasOwnProperty('Type')) {
    Type.registerNamespace('MySolution');
} else {
    window.MySolution = window.MySolution || {};
}
```

#### <a name="namespaces-mds-and-csr-client-side-rendering"></a>Namespaces, MDS und CSR (Client Side Rendering)

Die ``RegisterModuleInit`` Funktion deklariert eine richtige ``Type`` Namespace.  
Dateien mit JSLink angefügt sind **nicht** auf MDS Navigation erneut ausgeführt, verwenden Sie die AsyncDeltaManager-Funktionen, die für die.

### <a name="resources"></a>Ressourcen:

* [Wictor Wilén - ordnungsgemäße auszuführende Javascript-Funktionen in SharePoint MDS-fähige Websites](http://www.wictorwilen.se/the-correct-way-to-execute-javascript-functions-in-sharepoint-2013-mds-enabled-sites)
* [Hugh Wood - Kontext-Entwicklung für SharePoint JavaScript - AsyncDeltaManager](https://www.spcaf.com/blog/sharepoint-javascript-context-development-part-4-the-way-of-the-async-delta-manager/)
* [Marc Anderson - JavaScript ausführen nach MDS (Load neu)](http://blog.symprogress.com/2013/09/sharepoint-2013-execute-javascript-function-after-mds-load/)
