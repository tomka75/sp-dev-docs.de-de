---
title: "Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint"
description: "Bereitstellen von SharePoint-Add-Ins für SharePoint-Mandanten mit Mandantenbereichen und Webbereichen."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: ecd8176cb3cfd69b9264444fbcb6d34704372e6a
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="tenancies-and-deployment-scopes-for-sharepoint-add-ins"></a>Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint

Eine SharePoint-**Mandanteneinheit** ist ein Satz von Websitesammlungen entweder in einer SharePoint-Farm oder in SharePoint Online. In SharePoint Online gehören die Websitesammlungen zu einem einzelnen Kundenkonto. In einer SharePoint-Farm kann es sich bei den Websitesammlungen um alle Websitesammlungen in einer SharePoint-Webanwendung oder um eine Teilmenge davon handeln, oder es kann sich um einen Satz von Websitesammlungen über mehrere Webanwendungen in der Farm hinweg handeln. Eine Mandantschaft kann genau wie eine SharePoint-Webanwendung einen SharePoint-Add-In-Katalog aufweisen.

<a name="AppScope"> </a>
## <a name="tenancies-and-add-in-scope"></a>Mandantschaften und Add-In-Bereich

Ein SharePoint-Add-In weist einen **Add-In-Bereich** auf. Die zwei möglichen Add-In-Bereiche sind Webbereich und Mandantenbereich. Der Unterschied ist keine systeminterne Eigenschaft des Add-Ins, und Sie als Entwickler können den Bereich Ihres Add-Ins nicht festlegen. Diese Entscheidung wird von Mandantenadministratoren als Nebeneffekt der Installationsweise des Add-Ins getroffen. 

Nachdem ein Add-In in den Add-In-Katalog einer Mandantschaft hochgeladen wurde, kann es sofort auf einzelnen Websites innerhalb der Mandantschaft installiert werden. Add-Ins, die auf diese Weise installiert werden, weisen einen **Webbereich** auf. 

Mandantenadministratoren haben jedoch eine weitere Option. Sie können das Add-In im Batch in eine Untermenge von Websites innerhalb der Mandantschaft installieren. Add-Ins, die auf diese Weise installiert werden, weisen einen **Mandantenbereich** auf. Der Mandantenadministrator kann über eine Liste verwalteter Pfade, eine Liste von Websitevorlagen oder eine Liste von Websitesammlungen angeben, auf welchen Websites das Add-In installiert wird. Ein Add-In, das im Batch installiert wurde, kann nur von einem Mandantenadministrator deinstalliert werden. Wenn der Mandantenadministrator das Add-In deinstalliert, wird es von jeder Website in der Mandantschaft deinstalliert. Benutzer können ein im Batch installiertes Add-In nicht auf einzelnen Websites deinstallieren. Die gleichen Grundsätze gelten für das Aktualisieren eines im Batch installierten Add-Ins: Nur ein Mandantenadministrator kann das Add-In aktualisieren, und dieses wird auf jeder Website in der Mandantschaft, auf der es installiert ist, im Batch aktualisiert.

Bei der Batchinstallation eines Add-Ins, das ein Add-In-Web enthält, wird nur ein einzelnes Add-In-Web erstellt und von allen Hostwebsites verwendet, auf denen das Add-In installiert wird. Das Add-In-Web befindet sich in der Websitesammlung des Add-In-Katalogs des Unternehmens.

Wenn neue Websitesammlungen in der Mandantschaft erstellt werden, werden Add-Ins, die zuvor im Batch installiert wurden, automatisch in der neuen Websitesammlung installiert.

> [!NOTE]
> Der Add-In-Bereich sollte nicht mit dem Featurebereich verwechselt werden. Der Featurebereich bestimmt, wo die Elemente in einem Feature bereitgestellt werden. Die Optionen beinhalten **Farm**, **WebApplication**, **Site** (d.h. Websitesammlung) und **Web**. Für Features in SharePoint-Add-Ins (sowohl Hostwebfeatures als auch Features innerhalb einer WSP-Datei in einem Add-In-Paket) ist nur **Web** zulässig. 

> Der Add-In-Bereich sollte außerdem nicht mit Add-In-Berechtigungsstufen verwechselt werden. SharePoint-Add-Ins können Berechtigungen für alle oder für ausgewählte Teile von SharePoint-Inhalten auf den Ebenen Liste, Web, Websitesammlung und Mandantschaft anfordern. Durch Installieren eines Add-Ins mit Mandantenbereich erhält das Add-In keine Berechtigungen, die es ansonsten nicht hätte, und es werden auch keine wichtigen Bereitstellungen des SharePoint-Sicherheitsmodells abgebrochen. Weitere Informationen über Add-In-Berechtigungen finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).

<a name="Tenant"> </a>
## <a name="limitations-of-tenant-scoped-add-ins"></a>Einschränkungen für Add-Ins mit Mandantenbereich

Die folgenden Typen von Add-Ins funktionieren bei Batchinstallation nicht ordnungsgemäß:

- Add-Ins, die eine benutzerdefinierte Aktion für das Menüband enthalten. (Als Menüelemente bereitgestellte benutzerdefinierte Aktionen sind zulässig.)
- Add-Ins, die ein Add-In-Webpart enthalten.

Denken Sie außerdem daran, dass die Installation mit Mandantenbereich in der Office 365 Small Business Premium-Version von SharePoint Online nicht möglich ist.

<a name="Web"> </a>
## <a name="how-to-install-uninstall-and-update-an-add-in-on-multiple-websites-in-a-tenancy"></a>Installieren, Deinstallieren und Aktualisieren eines Add-Ins auf mehreren Websites eines Mandanten

Add-Ins aus dem Office Store oder aus einem Add-In-Katalog können von Mandantenadministratoren mit dem folgenden Verfahren auf mehreren Websites eines Mandanten installiert, deinstalliert und aktualisiert werden.

### <a name="to-install-a-sharepoint-add-in-to-multiple-websites"></a>So installieren Sie ein SharePoint-Add-In auf mehreren Websites

1. Gehen Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog.

2. Wählen Sie **Add-In hinzufügen** aus, und installieren Sie das Add-In so, wie Sie bei jeder anderen SharePoint-Website vorgehen würden.

3. Nachdem das Add-In installiert wurde, zeigen Sie auf der Seite **Websiteinhalte** auf den Link zu dem Add-In. Ein „**...**“-Link wird angezeigt.

4. Wählen Sie den Link aus. Ein Popup wird angezeigt.

5. Wählen Sie im Menü den Befehl **Bereitstellung** aus.

6. Geben Sie auf der Benutzeroberfläche für die Bereitstellung die Websitesammlungen an, in denen das Add-In installiert werden soll. Sie können nach verwalteten Pfaden, Websitevorlagen oder URLs filtern.

7. Wählen Sie **OK** aus.
    

### <a name="to-uninstall-a-batch-installed-sharepoint-add-in"></a>So deinstallieren Sie ein per Batch installiertes SharePoint-Add-In

1. Gehen Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog.

2. Zeigen Sie auf der Seite **Websiteinhalte** auf den Link zu dem Add-In. Ein „**...**“-Link wird angezeigt.

3. Wählen Sie den Link aus. Ein Popup wird angezeigt.

4. Wählen Sie im Popup **Entfernen** aus.    
 

### <a name="to-update-a-batch-installed-sharepoint-add-in"></a>So aktualisieren Sie ein per Batch installiertes SharePoint-Add-In

1. Gehen Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog. Wenn ein Update für ein Add-In verfügbar ist, wird neben dem Add-In eine Meldung angezeigt. Es gibt einen Link zum Aktualisieren des Add-Ins.

2. Klicken Sie auf den Link, um das Add-In zu aktualisieren.

3. Wenn Sie zur Genehmigung der Berechtigungsanforderungen des Add-Ins aufgefordert werden, wählen Sie **Vertrauen** aus.   
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15tenancies_addlresources"> </a>

-  [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md)    
-  [Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)   
-  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) 
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md)
    
