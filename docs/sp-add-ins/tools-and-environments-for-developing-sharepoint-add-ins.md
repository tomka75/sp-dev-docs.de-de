
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a>Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins
Erfahren Sie mehr über die Optionen zum Erstellen einer Entwicklungsumgebung für SharePoint-Add-Ins.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Es gibt zwei grundlegende Muster für Entwicklungsumgebungen für SharePoint-Add-Ins:
 

-  **Die SharePoint-Website für Test und Debugging ist in einer SharePoint Online-Website in einem Office 365-Abonnement enthalten.** Normalerweise wird Visual Studio auf einem lokalen Computer installiert, aber auch eine cloudbasierte Visual Studio-Installation ist eine Option.
    
 
-  **Das Testen und Debuggen von SharePoint-Websites findet in einer lokalen SharePoint-Farm mit einem Server statt. ** Visual Studio ist auf demselben Computer installiert.
    
 
Berücksichtigen Sie dabei Folgendes:
 

- Nahezu jedes von Ihnen erstellte Add-In kann entweder an SharePoint Online oder lokale SharePoint-Farmen bereitgestellt werden, unabhängig davon, welche Art von Umgebung Sie verwenden. Allgemein gilt, dass Apps, die nicht an SharePoint Online bereitgestellt werden können, auch nicht damit entwickelt werden können. Beispiele: Add-Ins, die  [Vollzugriffberechtigungen](add-in-permissions-in-sharepoint-2013) benötigen, und Add-Ins, die das [besonders vertrauenswürdige Autorisierungssystem](creating-sharepoint-add-ins-that-use-high-trust-authorization) verwenden.
    
 
- Sie können sowohl von SharePoint gehostete als auch von einem Anbieter gehostete SharePoint-Add-Ins entwickeln, unabhängig davon, welche Art von Umgebung Sie verwenden.
    
 
- Sie können sowohl lokale als auch SharePoint Online-Testwebsites haben.
    
 
- Die beiden Optionen sind im Großen und Ganzen beide gleichermaßen problemlos einzurichten.
    
 
 **Informationen zum Erstellen der SharePoint Online-Umgebung** mithilfe eines SharePoint Online-Abonnements finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription)
 
 **Informationen zum Erstellen der lokalen Umgebung** finden Sie unter [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).
 

 **Hinweis** Dieses Thema befasst sich nur mit Umgebungen für die Entwicklung von SharePoint-Add-Ins. Wenn Sie die Entwicklung von Farmlösungen planen, finden Sie weitere Informationen unter [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). Wenn Sie beide Arten von Entwicklung planen, beginnen Sie mit dem letzteren Artikel, und sehen Sie sich dann [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins) für weitere Schritte an, die für die Entwicklung von SharePoint-Add-Ins erforderlich sind.
 


## <a name="other-tooling-information"></a>Informationen zu anderen Tools

 
-  [Erstellen von SharePoint-Add-Ins in Visual Studio](create-sharepoint-add-ins-in-visual-studio)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [SharePoint-Add-Ins](sharepoint-add-ins)
    
 

