
# <a name="ux-design-for-sharepoint-add-ins"></a>UX-Design für SharePoint-Add-Ins
Erfahren Sie mehr über die UX-Optionen (User Experience), die Ihnen beim Erstellen von Add-Ins in SharePoint zur Verfügung stehen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Als Entwickler sollten Sie der User Experience (UX), d. h. dem umfassenden Nutzungserlebnis des Benutzers, einen hohen Stellenwert beimessen, wenn Sie Add-Ins erstellen. Das Modell für SharePoint-Add-Ins bietet zahlreiche UX-Komponenten und Mechanismen, die Sie dabei unterstützen, ein optimales Nutzungserlebnis zu bieten. Die User Experience im Add-In-Modell ist außerdem so flexibel, dass Sie die Verfahren und Plattformen verwenden können, die sich am besten an die Anforderungen der Endbenutzer anpassen.
 

## <a name="high-level-overview-of-add-in-ux-in-sharepoint"></a>Allgemeine Übersicht über Add-In-UX in SharePoint
<a name="SP15_UXdesignapps_overview"> </a>

Als Add-In-Entwickler müssen Sie die Architektur Ihres Add-Ins kennen. Nachdem Sie bestimmt haben, wie Ihr Add-In in Remote- und SharePoint-Plattformen verteilt werden soll, können Sie unter den verfügbaren Alternativen zum Erstellen Ihrer Add-In-UX eine Wahl treffen. Sie können sich folgende Fragen stellen:
 

 

- Was kann ich verwenden, wenn ich ein in der Cloud gehostetes Add-In erstelle?
    
 
- Was kann ich verwenden, wenn ich ein in SharePoint gehostetes Add-In erstelle? Weitere Informationen finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in).
    
 
- Wie kann ich meine UX mit dem Hostweb verbinden? Weitere Informationen finden Sie unter [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).
    
 
Das folgende Diagramm zeigt die wichtigsten Szenarios und Optionen, die beim Entwerfen der Add-In-UX berücksichtigt werden sollten.
 

 

**Abbildung 1. Wichtigste Szenarios und Optionen für die Add-In-UX**

 

 
![App-UX-Hauptszenarien](../../images/AppUX_landscape.png)
 
Bei der Wahl Ihres Entwurfs sollten Sie grundsätzlich überlegen, welche Teile Ihres Add-Ins in SharePoint gehostet werden und welche nicht. Sie sollten außerdem überlegen, wie Ihr Add-In mit der Hostwebsite interagiert.
 

 

## <a name="add-in-ux-scenarios-in-cloud-hosted-add-ins"></a>Add-In-UX-Szenarios für in der Cloud gehostete Add-Ins
<a name="SP15_UXdesignapps_devhosted"> </a>

Angenommen, Sie bestimmen, dass ein Teil Ihrer User Experience nicht in SharePoint gehostet werden soll. Bei diesen Szenarien wird davon ausgegangen, dass Ihre Endbenutzer zwischen einer SharePoint-Website und dem in der Cloud gehosteten Add-In hin und her wechseln. Sie können die auf der Plattform verfügbaren Verfahren und Tools verwenden, jedoch bietet SharePoint ebenfalls Ressourcen, damit Sie eine nahtlose Erfahrung für Ihre Benutzer entwerfen können.
 

 
Die folgenden UX-Ressourcen sind für in der Cloud gehostete Add-Ins in SharePoint verfügbar:
 

 

-  **Chromsteuerelement:** DasChromsteuerelement ermöglicht Ihnen, den Navigationsheader einer bestimmten SharePoint-Website in Ihrem Add-In zu verwenden, ohne eine Serverbibliothek registrieren zu müssen oder eine bestimmte Technologie bzw. ein bestimmtes Tool zu verwenden. Um diese Funktion zu nutzen, müssen Sie eine SharePoint-JavaScript-Bibliothek durch standardmäßige <script>-Tags registrieren. Sie können einen Platzhalter bereitstellen, indem Sie ein HTML- **div**-Element verwenden und das Steuerelement mithilfe der verfügbaren Optionen weiter anpassen. Das Steuerelement erhält sein Aussehen durch die angegebene SharePoint-Website. Weitere Informationen finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins).
    
    **Video ansehen: SharePoint-Chromsteuerelement**

 

 
![Videos](../../images/mod_icon_video.png)
 

 

 
-  **Stylesheet:** Sie können in Ihrer SharePoint-Add-In auf das Stylesheet einer SharePoint-Website verweisen und es zum Formatieren Ihrer Webseiten nutzen, indem Sie die verfügbaren Klassen verwenden. Wenn die Endbenutzer das Design der SharePoint-Website ändern, kann Ihr Add-In außerdem die neuen Formate übernehmen, ohne dass der Verweis in Ihrem Add-In geändert werden muss. Weitere Informationen finden Sie unter [Verwenden des Stylesheets einer SharePoint-Website in Add-Ins für SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins).
    
 
Abbildung 2 zeigt die Ressourcen im Modell für SharePoint-Add-Ins für in der Cloud gehostete Add-Ins.
 

 

**Abbildung 2. Add-In-UX Ressourcen für in der Cloud gehostete Add-Ins**

 

 
![Add-In-UX-Ressourcen für vom Entwickler gehostete Add-Ins](../../images/AppUX_devhosted.png)
 

 

 

## <a name="add-in-ux-scenarios-in-sharepoint-hosted-add-ins"></a>Add-In-UX-Szenarios für von SharePoint gehostete Add-Ins
<a name="SP15_UXdesignapps_SPhosted"> </a>

Wenn Ihr Add-In in SharePoint gehostet wird, ist es weniger wahrscheinlich, dass sich die User Experience stark ändert, wenn Benutzer zwischen der Hostwebsite und der Add-In-Website hin und her wechseln. Wenn das Add-In bereitgestellt wird, übernimmt die Add-In-Website das Stylesheet und Design der Hostwebsite. Sie können das Chromsteuerelement und das Stylesheet in einem in SharePoint gehosteten Add-In weiterhin verwenden, der signifikanteste Unterschied bei in der Cloud gehosteten Szenarien besteht jedoch in der Verfügbarkeit der Add-In-Vorlage.
 

 
Die folgenden UX-Ressourcen sind für von SharePoint gehostete Add-Ins verfügbar:
 

 

-  **Add-In-Vorlage:** Die Add-In-Vorlage umfasst die **app.master**-Masterpage. Dies ist die Standardoption beim Erstellen eines Add-In-Webs.
    
 
Von SharePoint gehostete Add-Ins profitieren auch selbst von in SharePoint vorhandenen Ressourcen und Technologien, z. B. Multifunktionsleiste, Webpart-Infrastruktur und clientseitiges Rendering.
 

 

## <a name="scenarios-for-connecting-the-add-in-ux-to-the-host-web"></a>Szenarios für das Herstellen einer Verbindung zwischen Add-In-UX und Hostweb
<a name="SP15_UXdesignapps_connectingappUX"> </a>

Einige Verwendungsfälle für Ihr Add-In können innerhalb der Hostwebsite ausgelöst werden. SharePoint bietet zwei Möglichkeiten zum Öffnen Ihres Add-Ins über eine Dokumentbibliothek oder Liste, zusätzlich zu den Möglichkeiten, einen Teil der Add-In-UX innerhalb von Seiten anzuzeigen, die in SharePoint gehostet sind.
 

 
Die folgenden UX-Ressourcen sind verfügbar, um Ihre Add-In-UX mit dem Hostweb zu verbinden:
 

 

-  **Benutzerdefinierte Aktionen**: Sie können benutzerdefinierte Aktionen verwenden, um die Hostwebsite-UX mit Ihrem Add-In zu verbinden. Es gibt zwei Typen von benutzerdefinierten Aktionen:Menüband oderECB. Eine benutzerdefinierte Aktion kann Parameter, wie z. B. die Liste oder das Element, in der bzw. dem sie aufgerufen wurde, an eine Remoteseite senden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins).
    
 
-  **Add-In-Parts:** Sie können einen Teil der User Experience Ihres Add-Ins mithilfe von Add-In-Parts der Hostwebsite hinzufügen. Das Add-In-Part ist bei der Bereitstellung des Add-Ins im Webpartkatalog auf der Hostwebsite verfügbar. Benutzer können das Add-In-Part einer Seite hinzufügen, indem sie das Steuerelement zum **Hinzufügen von Webparts** verwenden. Weitere Informationen finden Sie unter [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in).
    
 
Abbildung 3 zeigt die Ressourcen im Modell für SharePoint-Add-Ins zum Verbinden der Add-In-UX mit dem Hostweb.
 

 

**Abbildung 3. Add-In-UX-Ressourcen für das Hostweb**

 

 
![Add-In-UX-Ressourcen für das Hostweb](../../images/AppUX_hostweb.png)
 

 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_UXdesignapps_addresources"> </a>

Informationen zur Verwendung der Add-In-UX-Optionen in SharePoint-Add-Ins finden Sie in den folgenden Ressourcen:
 

 

-  [Entwerfen von SharePoint-Add-Ins](design-sharepoint-add-ins)
    
 
-  [SharePoint-Add-Ins](sharepoint-add-ins)
    
 
-  [Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)
    
 
-  [Designrichtlinien für die Benutzerfreundlichkeit von SharePoint-Add-Ins](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 
-  [Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins](create-custom-actions-to-deploy-with-sharepoint-add-ins)
    
 

