---
title: "Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins"
description: "Hier erfahren Sie, wie Sie auf einer SharePoint Online-Website oder in einer lokalen Farm eine Entwicklungsumgebung für SharePoint-Add-Ins erstellen können."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 22c5a3cdff4d7d829a401edd1b170aafd6ca577d
ms.sourcegitcommit: 074f3a7983a7b253f56f8c670a0290c27bb7734b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a>Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins

Es gibt zwei grundlegende Muster für Entwicklungsumgebungen für SharePoint-Add-Ins. Die SharePoint-Website für Tests und Debugging kann gehostet werden:

-  **Auf einer SharePoint Online-Website in einem Office 365-Abonnement:** In der Regel wird Visual Studio auf einem lokalen Computer installiert. Eine cloudbasierte Visual Studio-Instanz ist aber ebenfalls eine Option.

-  **In einer lokalen SharePoint-Farm mit einem einzigen Server:** Visual Studio wird auf demselben Computer installiert.
 
Dabei ist Folgendes zu berücksichtigen:

- Fast alle Add-Ins, die Sie erstellen, können sowohl in SharePoint Online als auch in einer lokalen SharePoint-Farm bereitgestellt werden, unabhängig von der verwendeten Umgebung. Allgemein gilt: Add-Ins, die nicht in SharePoint Online bereitgestellt werden können, können auch nicht mit SharePoint Online entwickelt werden. Das sind beispielsweise Add-Ins, die die [Berechtigung „Vollzugriff“](add-in-permissions-in-sharepoint.md) benötigen, sowie Add-Ins, die das [besonders vertrauenswürdige Autorisierungssystem](creating-sharepoint-add-ins-that-use-high-trust-authorization.md) verwenden.

- Sie können mit jeder Umgebung sowohl SharePoint-gehostete SharePoint-Add-Ins als auch anbietergehostete SharePoint-Add-Ins entwickeln.

- Sie können sowohl mit lokalen Testwebsites als auch mit SharePoint Online-Testwebsites arbeiten.

- Insgesamt sind beide Optionen gleich unkompliziert in der Einrichtung.
    
Die **Erstellung einer SharePoint Online-Umgebung** mithilfe eines SharePoint Online-Abonnements für die Entwicklung wird im Artikel [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md) beschrieben.
 
Eine Anleitung zur **Erstellung einer lokalen Umgebung** finden Sie im Artikel [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).
 
> [!NOTE]
> In diesem Artikel geht es ausschließlich um Umgebungen für die Entwicklung von SharePoint-Add-Ins. Wenn Sie Farmlösungen entwickeln möchten, finden Sie entsprechende Informationen im Artikel [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). 

> Wenn Sie Entwicklungsprojekte beider Typen umsetzen möchten, sollten Sie mit letzterem Artikel beginnen und anschließend den Artikel [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md) lesen. Dort finden Sie weitere erforderliche Schritte für die Entwicklung von SharePoint-Add-Ins.


## <a name="additional-resources"></a>Weitere Ressourcen
<a name="bk_addresources"> </a>

- [SharePoint Add-ins](sharepoint-add-ins.md)
- [Erstellen von SharePoint-Add-Ins in Visual Studio](create-sharepoint-add-ins-in-visual-studio.md)
    
 

