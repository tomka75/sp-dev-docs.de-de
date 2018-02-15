---
title: "Veröffentlichen von SharePoint-Add-Ins"
description: "Entscheiden Sie, wo Ihre SharePoint-Add-Ins veröffentlicht werden sollen."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 49d66a8b82272537d92bdab40e361f9794914ee9
ms.sourcegitcommit: 843caaf543cdc2cf43fbb783e95164fbf99a586a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="publish-sharepoint-add-ins"></a>Veröffentlichen von SharePoint-Add-Ins

Nachdem Sie Ihr SharePoint-Add-In fertig gestellt haben, besteht der letzte Schritt darin, das Add-In Ihren Benutzern verfügbar zu machen. Zu diesem Zweck können Sie das Add-In an zwei verschiedenen Orten veröffentlichen:

- **Im öffentlichen Office Store.** Wenn Sie Ihr Add-In im Office Store öffentlich anbieten, steht es allen Benutzern von SharePoint-Bereitstellungen zur Verfügung.

- **Im internen Add-In-Katalog einer Organisation.** Wenn Sie Ihre Add-Ins im internen Add-In-Katalog einer Organisation veröffentlichen, der in Ihrer SharePoint-Bereitstellung gehostet wird, machen Sie sie für Benutzer verfügbar, die auf diese SharePoint-Bereitstellung zugreifen können.

Informationen darüber, wie Sie Ihr Add-In zur Veröffentlichung mit Visual Studio 2012 packen, finden Sie unter [Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md).

## <a name="publishing-to-the-office-store"></a>Veröffentlichen im Office Store

Zum Veröffentlichen eines Add-Ins im Office Store müssen Sie sich zunächst [als Microsoft-Entwickler registrieren](https://sellerdashboard.microsoft.com/Registration). 

Wenn Sie ein Add-In zur Veröffentlichung in den Office Store hochladen, führt Microsoft eine Reihe von Überprüfungen durch, um sicherzustellen, dass Ihr Add-In den Add-In-Inhalts- und -verhaltensrichtlinien entspricht. Beispielsweise wird geprüft, ob das Add-In-Manifestmarkup gültig und vollständig ist, und sichergestellt, dass im Add-In enthaltene SharePoint-Lösungspakete (WSP-Dateien) keine unzulässigen Elemente oder SharePoint-Features mit einem Geltungsbereich enthalten, der über "Web" hinausgeht. Das Paket wird zudem auf unzulässigen Inhalt geprüft. Wenn das Add-In alle Tests besteht, wird es in eine Datei verpackt und von Microsoft signiert.

Wenn Sie Ihr Add-In zur Veröffentlichung in den Office Store hochladen, können Sie Lizenzbedingungen für Benutzer anbieten, die das Add-In herunterladen. Die Add-In-Lizenz definiert: 

- ob Sie Ihr Add-In kostenlos, als Testversion oder zum Kauf anbieten;
- ob Ihr Add-In auf Pro-Benutzer- oder Websitebasis erworben werden kann.

SharePoint erzwingt für die Add-In-Nutzung keine Lizenzbedingungen, sondern bietet ein Lizenzierungsmodell an, mit dem Sie Codelogik in das Add-In integrieren können, um die gewählten Lizenzbeschränkungen zu erzwingen. Sie können beispielsweise Codelogik in ein Add-In integrieren, das Benutzern den Zugriff auf bestimmte Add-In-Funktionen ermöglicht, wenn diese über eine kostenpflichtige Lizenz verfügen. Benutzer mit einer Testlizenz erhalten dann keinen Zugriff.  Weitere Informationen finden Sie unter [Lizenzieren von Office- und SharePoint-Add-Ins](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx).

## <a name="publishing-to-an-add-in-catalog"></a>Veröffentlichen in einem Add-In-Katalog

Wenn Sie SharePoint-Add-Ins für die Verwendung durch Ihr eigenes Unternehmen oder einen spezifischen Unternehmensclient und nicht die Allgemeinheit erstellen, möchten Sie Ihr Add-In wahrscheinlich in einem von SharePoint gehosteten internen Add-In-Katalog veröffentlichen. Ein privater Add-In-Katalog ist eine dedizierte Websitesammlung in einer SharePoint-Webanwendung (oder einer SharePoint Online-Instanz), die als Host für Dokumentbibliotheken für SharePoint-Add-Ins und Office-Add-Ins dient. Wenn der Katalog in eine eigene Websitesammlung eingefügt wird, ist es für den Webanwendungsadministrator oder Mandantenadministrator einfacher, Zugriffsberechtigungen für den Katalog zu begrenzen.

Das Hochladen einer SharePoint-Add-In in einen Unternehmens-Add-In-Katalog ist genauso einfach wie das Hochladen einer Datei in eine SharePoint-Dokumentbibliothek. Sie füllen Sie ein Popupformular aus, in dem Sie die lokale URL des Add-In-Pakets und weitere Informationen, wie z. B. den Namen des Add-Ins, angeben. Wenn Sie das Add-In in einen Add-In-Katalog hochladen, werden ähnliche Kontrolle durchgeführt, und Add-Ins, die diese Überprüfung nicht bestehen, werden im Katalog mit ungültig oder deaktiviert gekennzeichnet.

<a name="bk_decide"> </a>
## <a name="deciding-where-to-publish-your-sharepoint-add-in"></a>Entscheiden, wo Ihr SharePoint-Add-In veröffentlicht werden soll

In der folgenden Tabelle wird die Veröffentlichung im Office Store mit der Veröffentlichung in einem Add-In-Katalog verglichen. Zudem wird auf kritische Punkte hingewiesen, die bei der Entscheidung, wo ein Add-In veröffentlicht werden soll, zu berücksichtigen sind. Wir empfehlen, die Veröffentlichung des Add-Ins bereits vor dem Entwurf und der Entwicklung zu planen, da sich der Ort der Veröffentlichung in manchen Fällen auf den Entwurf und die Entwicklung des Add-Ins auswirkt.

**Tabelle 1: Überlegungen zum Ort der Veröffentlichung eines Add-Ins**

|**Office Store**|**Add-In-Katalog**|
|:-----|:-----|
|Das Add-In ist öffentlich zugänglich.|Das Add-In steht Benutzern zur Verfügung, die auf diese SharePoint-Bereitstellung zugreifen können.|
|Ein Lizenzierungsframework ist verfügbar.|Es steht kein Lizenzierungsframework zur Nutzung zur Verfügung.|
|Das Add-In-Paket wird von Microsoft auf die Einhaltung technischer und Inhaltsrichtlinien geprüft.|Die Überprüfung des Add-In-Pakets wird beim Hochladen von SharePoint durchgeführt.|
|Sie müssen beim Microsoft Seller Dashboard angemeldet sein, um Add-Ins hochladen zu können.|Es ist keine Registrierung bei Microsoft erforderlich.|

## <a name="see-also"></a>Weitere Artikel
<a name="bk_addresources"> </a>

-  [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](https://docs.microsoft.com/de-DE/office/dev/store/create-or-update-client-ids-and-secrets)
-  [Verwenden des Verkäuferdashboards zum Übermitteln von Office- und SharePoint-Add-Ins und Office 365-Apps an den Office Store](https://docs.microsoft.com/de-DE/office/dev/store/use-the-seller-dashboard-to-submit-to-the-office-store)
-  [Validierungsrichtlinien für an den Office Store übermittelte Apps und Add-Ins](https://docs.microsoft.com/de-DE/office/dev/store/validation-policies)
-  [Office-Entwicklung](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx)
-  [Lizenzieren von Office- und SharePoint-Add-Ins](https://docs.microsoft.com/de-DE/office/dev/store/license-your-add-ins)
-  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
-  [Mandantschaften und Bereitstellungsbereiche von SharePoint- Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)
-  [Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md)
-  [Übermitteln Ihrer Lösungen an den Office Store](https://docs.microsoft.com/de-DE/office/dev/store/submit-to-the-office-store)