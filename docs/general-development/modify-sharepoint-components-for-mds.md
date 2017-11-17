---
title: "Ändern der SharePoint-Komponenten für MDS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c967be7c-f29f-481a-9ce2-915ead315dcd
ms.openlocfilehash: 697a284f3d07c6b3ddcdad005578ba3f9f7700ac
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="modify-sharepoint-components-for-mds"></a>Ändern der SharePoint-Komponenten für MDS
Erfahren Sie, wie die Komponenten in Ihrem Projekt SharePoint die Vorteile der minimale herunterladen Strategie (MDS) in SharePoint ändern. Minimale herunterladen Strategie (MDS) wurde die benutzerfreundlichkeit verbessert, indem nur die Teile einer Seite erforderlich, um diese ordnungsgemäß im Browser zu rendern vom Server zurückgegeben. Da die Seite vollständig gerendert nicht an den Client zurückgegeben wird, muss der Server sein um genau die Teile zu identifizieren, die zum Rendern der Seite erforderlich sind. Sie müssen möglicherweise die Komponenten in Ihrem Projekt SharePoint ändern, sodass sie als MDS-kompatiblen erkannt werden, und können mit dem Modul MDS arbeiten. Erfahren Sie mehr über MDS in  [Übersicht über die minimale Strategie herunterladen](minimal-download-strategy-overview.md).
  
    
    


## <a name="why-modify-sharepoint-components"></a>Gründe für das Ändern SharePoint Komponenten?
<a name="bk_whymodify"> </a>

Wie unter  [Übersicht über die minimale Strategie herunterladen](minimal-download-strategy-overview.md)erläutert, arbeiten SharePoint Steuerelemente, unabhängig davon, ob Sie diese MDS voll ausschöpfen ändern. Wenn Ihre Komponenten nicht MDS kompatibel sind, gibt das Modul MDS jedoch einen Failover aus. In der ein Failover benötigt das Modul MDS ein zusätzlicher Roundtrip zum Umleiten von im Browsers auf die Vollversion der neuen Seite, die Zeit in Anspruch nimmt. Benutzer haben die beste Erfahrung beim Arbeiten mit MDS und einen Failover zu vermeiden, jedes Mal, wenn eine neue Seite in SharePoint Besuch Komponenten ändern. Sie müssen in der Regel Masterseiten, ASP.NET Seiten, Steuerelemente und Webparts ändern. 
  
    
    

  
    
    

## <a name="master-pages"></a>Gestaltungsvorlagen
<a name="SP15MDSDev_MasterPages"> </a>

Die Gestaltungsvorlage bietet eine Vorlage, mit der MDS Inhaltsbereiche zu identifizieren, die möglicherweise aktualisiert werden, wenn eine Person zu einer neuen Seite navigiert. Optimieren Ihre Gestaltungsvorlagen gehört zu die wichtigsten Schritte bei der Optimierung der Leistung, da Masterseiten Abschnitte, die erfordern identifizieren, aktualisiert Content. Die Gestaltungsvorlage Seattle.master enthaltene SharePoint ist ein gutes Beispiel für eine optimierte Gestaltungsvorlage. Abbildung 1 zeigt Beispiele für Komponenten in der Gestaltungsvorlage Seattle.master, die sich über mehrere Seiten, wie (1) Content Hauptbereich, (2) der linken Navigationsleiste und Titel (3) Seite ändern.
  
    
    

**Abbildung 1. Komponenten, die Updates in eine Gestaltungsvorlage erfordern**

  
    
    

  
    
    
![Komponenten, die Aktualisierungen in der Gestaltungsvorlage erfordern](../images/MDS_SeattleMaster.png)
  
    
    

    
> **Hinweis:** Es gibt viele weitere Komponenten in der Gestaltungsvorlage Seattle.master, wie etwa Stylesheets und JavaScript Dateien, die von Seite zu Seite ändern. Abbildung 1 zeigt nur einige Beispiele. 
  
    
    

Es gibt verschiedene Muster zur Optimierung der Komponenten in einer Gestaltungsvorlage. Sie können ein Muster für die folgenden Komponenten verwenden:
  
    
    

- HTML-Regionen und Steuerelemente
    
  
- Stylesheets
    
  
- JavaScript-Dateien
    
  
- Seitentitel
    
  
HTML-Regionen und Steuerelemente sind MDS kompatibel, wenn sie in **SharePoint:AjaxDelta** Tags eingeschlossen sind. Durch Umschließen des Inhalts in **SharePoint:AjaxDelta** -Tags, sind Sie signalisieren, dass das MDS-Modul die eingeschlossenen Steuerelemente und HTML-aktualisiert werden soll. Wenn ein Steuerelement oder ein HTML-Abschnitt nicht von einer Seite zu ändern, sollten sie nicht an den Client gesendet werden. Aus diesem Grund sollten Sie diese Steuerelemente außerhalb **AjaxDelta** Tags beibehalten. In der Seattle.master Gestaltungsvorlage in der in Abbildung 1 dargestellt ist (1) Content Hauptbereich in **AjaxDelta** -Tags eingeschlossen, wie hier gezeigt.
  
    
    



```cs
<SharePoint:AjaxDelta
            id="DeltaPlaceHolderMain"
            BlockElement="true"
            IsMainContent="true"
            runat="server">
    <a id="mainContent" name="mainContent" tabindex="-1"></a>
    <asp:ContentPlaceHolder id="PlaceHolderMain" runat="server" />
</SharePoint:AjaxDelta>
```

Ein weiteres Beispiel für das Muster **AjaxDelta** ist der (2) linken Navigationsleiste in Abbildung 1. Der folgende Code zeigt, wie das Steuerelement in **AjaxDelta** Tags zusammen mit anderen Steuerelemente und HTML-umgebrochen wird.
  
    
    



```cs
<SharePoint:AjaxDelta
            id="DeltaPlaceHolderLeftNavBar"
            BlockElement="true"
            CssClass="ms-core-navigation"
            role="navigation"
            runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderLeftNavBar" runat="server">
        <a id="startNavigation" name="startNavigation" tabIndex="-1"></a>
        <asp:ContentPlaceHolder id="PlaceHolderLeftNavBarTop" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderQuickLaunchTop" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderLeftNavBarDataSource" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderCalendarNavigator" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderLeftActions" runat="server" />
        <!-- There are more controls and HTML in this placeholder in the Seattle master page -->
    </asp:ContentPlaceHolder>
</SharePoint:AjaxDelta>
```

Eine Sache zu **AjaxDelta** Tags merken ist, dass sie zu schachteln. Sie sollten in der Gestaltungsvorlage in der Struktur **AjaxDelta** Tags auf der höchsten Ebene erforderlichen angeben.
  
    
    
Das letzte Beispiel in Abbildung 1 ist (3) Seitentitel, der eine spezielle Muster erforderlich sind, die das Tag **SharePoint:PageTitle** verwendet. Der folgende Code zeigt das Tag **PageTitle** wie in der Gestaltungsvorlage Seattle.master.
  
    
    



```cs

<SharePoint:PageTitle runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">
        <SharePoint:ProjectProperty Property="Title" runat="server" />
    </asp:ContentPlaceHolder>
</SharePoint:PageTitle>
```

Die Masterseite kann auch Stylesheets und die JavaScript Dateien enthalten. Das Server-Datenbankmodul muss CSS- und JavaScript Dateien nach Bedarf zu identifizieren. Verwenden Sie das folgende Muster, um die CSS-Dateiressourcen nach Bedarf zu identifizieren.
  
    
    



```cs

<SharePoint:CssLink runat="server" Version="15"/>
<SharePoint:CssRegistration Name="my_styles.css" runat="server" />
```

Beachten Sie, dass können Sie nur ein **CssLink** Tag pro Gestaltungsvorlage verfügen, können aber viele **CssRegistration** -Tags, damit viele CSS-Dateien hinzugefügt werden können. Verwenden Sie das folgende Muster für JavaScript-Dateien.
  
    
    



```cs

<SharePoint:ScriptLink language="javascript" name="my_javascript.js" runat="server" />
```

Einschließlich CSS- und JavaScript-Dateien mithilfe von HTML-Tags für **style** und **script** wird in MDS nicht unterstützt.
  
    
    

## <a name="aspnet-pages"></a>ASP.NET-Seiten
<a name="SP15MDSDev_ASPNET"> </a>

Wenn Ihr Projekt ASP.NET Seiten enthält, müssen Sie CSS- und JavaScript-Dateien zu verweisen. Die HTML-Tags **style** und **script** sind nicht kompatibel mit MDS. Verwenden Sie stattdessen die **CssRegistration** und **ScriptLink** Muster, die im vorherigen Abschnitt erläutert.
  
    
    
Ihre Seiten ASP.NET können auch die **Response.Output** -Methode zum Schreiben des Inhalts auf der Seite, der nicht in MDS zulässig ist. Stattdessen können Sie die folgenden MDS-kompatiblen Methoden der [SPHttpUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.aspx) -Klasse:
  
    
    

-  [WriteNoEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteNoEncode.aspx)
    
  
-  [WriteHtmlEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncode.aspx)
    
  
-  [WriteEcmaScriptStringLiteralEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteEcmaScriptStringLiteralEncode.aspx)
    
  
-  [WriteHtmlEncodeAllowSimpleTextFormatting()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncodeAllowSimpleTextFormatting.aspx)
    
  
-  [WriteHtmlUrlAttributeEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlUrlAttributeEncode.aspx)
    
  
-  [WriteUrlKeyValueEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlKeyValueEncode.aspx)
    
  
-  [WriteUrlPathEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlPathEncode.aspx)
    
  
Zusätzlich zum Verweisen auf JavaScript Dateien können Seiten ASP.NETJavaScript Inlinecode enthalten. Mit dem folgenden Muster stellen Sie das Skript blockiert MDS kompatibel.
  
    
    



```cs
<SharePoint:ScriptBlock runat="server" >
    // Your JavaScript code here.
</SharePoint:ScriptBlock>
```


## <a name="controls-and-web-parts"></a>Steuerelemente und Webparts
<a name="SP15MDSDev_WebParts"> </a>

Außerdem müssen Sie die Steuerelemente und Webparts als MDS kompatibel zu kennzeichnen. Der folgende Code zeigt das zu verwendende Muster.
  
    
    

```cs

[assembly: Microsoft.SharePoint.WebControlssCompliantAttribute(IsCompliant = true)]
namespace VisualWebPartProject2.VisualWebPart1
{
    // Rest of your control logic
```

Darüber hinaus müssen die Steuerelemente und Webparts ihre Ressourcen mithilfe der Methoden in der Klasse  [SPPageContentManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPPageContentManager.aspx) zu registrieren. Die am häufigsten verwendeten Ressourcen sind JavaScript Snippets und versteckte mithilfe von der **RegisterClientScriptBlock** und **RegisterHiddenField**, registriert werden können.
  
    
    
Die Steuerelemente und Webparts können XSLT-Dateien auch Renderingprozess steuern. Ihre XSLT-Dateien können JavaScript Code oder Dateien eingebettet haben. Das Modul MDS muss diese Ressourcen kennen. Sie können die JavaScript Ressourcen mithilfe eines XSLT-Erweiterung-Objekts mit dem Namen **pcm**registrieren. Ein hervorragendes Beispiel zur Verwendung des **pcm** -Objekts ist in der %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ TEMPLATE\\LAYOUTS\\XSL\\fldtypes.xsl-Datei. Der folgende Code zeigt, wie die Datei **fldtypes.xsl** das **pcm** -Objekt verwendet, um JavaScript Ressourcen zu registrieren.
  
    
    



```XML

<xsl:value-of select="pcm:RegisterScriptBlock(concat('block1',$ViewCounter), string($scriptbody1))"/>
<xsl:value-of select="pcm:RegisterScriptLink('/_layouts/15/wssactionmenu.js')"/>
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Übersicht über die minimale Strategie herunterladen](minimal-download-strategy-overview.md)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  

