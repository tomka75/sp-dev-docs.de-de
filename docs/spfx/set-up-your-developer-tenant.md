---
title: Einrichten des Office 365-Mandanten
description: Erstellen Sie clientseitige Webparts mithilfe von SharePoint Framework, und stellen Sie diese bereit, indem Sie einen Office 365-Mandanten einrichten.
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 5981b4eaca349700a78cbbdf39eef376cb6d56e4
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="set-up-your-office-365-tenant"></a>Einrichten des Office 365-Mandanten

Zum Erstellen und Bereitstellen von clientseitigen Webparts mithilfe von SharePoint Framework benötigen Sie einen Office 365-Mandanten. 

Wenn Sie bereits einen Office 365-Mandanten haben, finden Sie Informationen unter [Erstellen der App-Katalogwebsite](#create-app-catalog-site).

Wenn Sie keinen Mandanten haben, können Sie einen Testmandanten erstellen, oder melden Sie sich für das [Office 365 Developer-Programm](https://dev.office.com/devprogram) an.  

> [!NOTE] 
> Stellen Sie sicher, dass Sie von allen vorhandenen Office 365-Mandanten abgemeldet sind, bevor Sie sich anmelden.

## <a name="create-app-catalog-site"></a>Erstellen der App-Katalogwebsite

Sie benötigen einen App-Katalog zum Hochladen und Bereitstellen von Webparts. Wenn Sie bereits einen App-Katalog eingerichtet haben, finden Sie Informationen unter [Erstellen einer neuen Entwicklerwebsitesammlung](#create-a-new-developer-site-collection).  

### <a name="to-create-an-app-catalog-site"></a>So erstellen Sie eine App-Katalogwebsite

1. Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben. Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. Wählen Sie in der linken Randleiste das Menüelement **Apps** und dann **App-Katalog** aus.

3. Wählen Sie **OK** aus, um eine neue App-Katalogwebsite zu erstellen.

4. Geben Sie auf der nächsten Seite die folgenden Informationen ein:

    - **Titel**: Geben Sie **App-Katalog** ein.
    - **Websiteadressen_-Suffix_**: Geben Sie Ihren bevorzugten Suffix für den App-Katalog ein. Beispiel: **Apps**.
    - **Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.

5. Wählen Sie **OK** aus, um die App-Katalogwebsite zu erstellen.

SharePoint erstellt die App-Katalogwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen.

## <a name="create-a-new-developer-site-collection"></a>Erstellen einer neuen Entwicklerwebsitesammlung

Sie benötigen ferner eine Websitesammlung und eine Website zum Testen. Sie können eine neue Websitesammlung mit jeder der verfügbaren Vorlagen erstellen. Sie können die **Entwicklerwebsitesammlung** verwenden, dies hat aber nicht wirklich einen Mehrwert, da Workbench- und Basistests mit einer beliebigen Website ausgeführt werden können.

### <a name="to-create-a-new-developer-site-collection"></a>So erstellen Sie eine neue Entwicklerwebsitesammlung

1. Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben. Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. Wählen Sie im SharePoint-Menüband **Neu** > **Private Websitesammlung** aus.

3. Geben Sie in das Dialogfeld die folgenden Informationen ein:

    - **Titel**: Geben Sie einen Titel für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Entwicklerwebsite**.
    - **Websiteadressen_-Suffix_**: Geben Sie einen Suffix für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Dev**
    - **Vorlagenauswahl**: Wählen Sie **Entwicklerwebsite** als die Vorlage für die Websitesammlung aus.
    - **Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.

4. Klicken Sie auf **OK**, um die Websitesammlung zu erstellen.

SharePoint erstellt die Entwicklerwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen. Nachdem die Website erstellt wurde, können Sie zu Ihrer Entwicklerwebsitesammlung wechseln.

## <a name="sharepoint-workbench"></a>SharePoint Workbench

SharePoint Workbench ist eine Designoberfläche für Entwickler, mit der Sie schnell Webpart-Tests durchführen und eine Webpart-Vorschau anzeigen können, und zwar ohne die Webparts in SharePoint bereitstellen zu müssen. Die SharePoint Framework Developer-Toolkette enthält eine Version der Workbench, die lokal ausgeführt wird und Ihnen hilft, erstellte Lösungen schnell zu testen und zu überprüfen. Sie lässt sich auch in Ihrem Mandanten hosten, um während der Entwicklung lokaler Webparts eine Webpart-Vorschau anzuzeigen und Tests durchzuführen. Unter der folgenden URL können Sie auf die SharePoint Workbench von jeder SharePoint-Website in Ihrem Mandanten aus zugreifen:

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a>Nächste Schritte

Da Sie jetzt Ihren SharePoint-Mandanten konfiguriert, [richten Sie Ihre Entwicklungsumgebung ein](./set-up-your-development-environment.md), um clientseitige Webparts zu erstellen.
