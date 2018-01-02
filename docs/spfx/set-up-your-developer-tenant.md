---
title: Einrichten des Office 365-Mandanten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 77de8b0b91c0c67cb9149bd5bbc38b21c1e432f9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-your-office-365-tenant"></a>Einrichten des Office 365-Mandanten

Zum Erstellen und Bereitstellen von clientseitigen Webparts mithilfe der Preview-Version von SharePoint Framework benötigen Sie einen Office 365-Mandanten. 

## <a name="sign-up-for-an-office-365-tenant"></a>Registrieren für einen Office 365-Mandanten
Wenn Sie bereits einen Office 365-Mandanten haben, finden Sie Informationen unter [Erstellen der App-Katalogwebsite](#create-app-catalog-site).

Wenn Sie keinen Mandanten haben, können Sie einen Testmandanten erstellen, oder melden Sie sich beispielsweise für das [Office Developer-Programm](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=7a6e3d71-b057-49cc-b2aa-158ff23432f3&lcid=1033&culture=en-us&dir=LTR) an. Sie erhalten eine Willkommens-E-Mail mit einem Link zum Registrieren für einen Office 365-Entwicklermandanten. 

> [!NOTE] 
> Stellen Sie sicher, dass Sie von allen vorhandenen Office 365-Mandanten abgemeldet sind, bevor Sie sich anmelden.

## <a name="create-app-catalog-site"></a>Erstellen der App-Katalogwebsite
Sie benötigen einen App-Katalog zum Hochladen und Bereitstellen von Webparts. Wenn Sie bereits einen App-Katalog eingerichtet haben, finden Sie Informationen unter [Erstellen einer neuen Entwicklerwebsitesammlung](#create-a-new-developer-site-collection).  

Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben. Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
Wählen Sie in der linken Randleiste das Menüelement **Apps** und dann **App-Katalog** aus.

Wählen Sie **OK** aus, um eine neue App-Katalogwebsite zu erstellen.

Geben Sie auf der nächsten Seite die folgenden Informationen ein:

* **Titel**: Geben Sie **App-Katalog** ein.
* **Websiteadressen_-Suffix_**: Geben Sie Ihren bevorzugten Suffix für den App-Katalog ein. Beispiel: **Apps**.
* **Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.

Wählen Sie **OK** aus, um die App-Katalogwebsite zu erstellen.

SharePoint erstellt die App-Katalogwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen.

## <a name="create-a-new-developer-site-collection"></a>Erstellen einer neuen Entwicklerwebsitesammlung
Sie benötigen ferner eine Websitesammlung und eine Website zum Testen. Sie können eine neue Websitesammlung mit jeder der verfügbaren Vorlagen erstellen. Sie können die **Entwicklerwebsitesammlung** verwenden, dies hat aber nicht wirklich einen Mehrwert, da Workbench- und Basistests mit einer beliebigen Website ausgeführt werden können.

Im Folgenden sind die Schritte zum Erstellen einer neuen Entwicklerwebsitesammlung aufgeführt.

 Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben. Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
Wählen Sie im SharePoint-Menüband **Neu** -> **Private Websitesammlung** aus.

Geben Sie in das Dialogfeld die folgenden Informationen ein:

* **Titel**: Geben Sie einen Titel für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Entwicklerwebsite**.
* **Websiteadressen_-Suffix_**: Geben Sie einen Suffix für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Dev**
* **Vorlagenauswahl**: Wählen Sie **Entwicklerwebsite** als die Vorlage für die Websitesammlung aus.
* **Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.

Klicken Sie auf **OK**, um die Websitesammlung zu erstellen.

SharePoint erstellt die Entwicklerwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen. Nachdem die Website erstellt wurde, können Sie zu Ihrer Entwicklerwebsitesammlung wechseln.

## <a name="sharepoint-workbench"></a>SharePoint Workbench
SharePoint Workbench ist eine Designoberfläche für Entwickler, mit der Sie schnell Webpart-Tests durchführen und eine Webpart-Vorschau anzeigen können, und zwar ohne die Webparts in SharePoint bereitstellen zu müssen. Die SharePoint Framework Developer-Toolkette enthält eine Version der Workbench, die lokal ausgeführt wird und Ihnen hilft, erstellte Lösungen schnell zu testen und zu überprüfen. Sie lässt sich auch in Ihrem Mandanten hosten, um während der Entwicklung lokaler Webparts eine Webpart-Vorschau anzuzeigen und Tests durchzuführen. Unter der folgenden URL können Sie auf die SharePoint Workbench von jeder SharePoint-Website in Ihrem Mandanten aus zugreifen:

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a>Nächste Schritte
Da Sie jetzt Ihren SharePoint-Mandanten konfiguriert, [richten Sie Ihre Entwicklungsumgebung ein](./set-up-your-development-environment.md), um clientseitige Webparts zu erstellen.
