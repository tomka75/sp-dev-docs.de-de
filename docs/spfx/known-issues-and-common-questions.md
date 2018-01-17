---
title: "Bekannte Probleme und häufig gestellte Fragen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6fba3eac7cca5200b7593dd51243df41211f6bc1
ms.sourcegitcommit: 8384d549db4ff023aacac273d74786928ebdeece
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/11/2017
---
# <a name="known-issues-and-frequently-asked-questions"></a><span data-ttu-id="6e352-102">Bekannte Probleme und häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="6e352-102">Known issues and frequently asked questions</span></span>

<span data-ttu-id="6e352-103">Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint Framework sowie Antworten auf häufig gestellte Fragen.</span><span class="sxs-lookup"><span data-stu-id="6e352-103">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="6e352-104">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="6e352-104">Known issues</span></span>

<span data-ttu-id="6e352-105">**Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)**</span><span class="sxs-lookup"><span data-stu-id="6e352-105">**Dev certificate issue with Chrome (v58-)**</span></span>

- <span data-ttu-id="6e352-106">*Datum – 28. April*</span><span class="sxs-lookup"><span data-stu-id="6e352-106">*Date - 28th of April*</span></span>
- <span data-ttu-id="6e352-107">*Aktualisiert – 2. Mai*</span><span class="sxs-lookup"><span data-stu-id="6e352-107">*Updated - 2nd of May*</span></span>

<span data-ttu-id="6e352-p101">Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen. Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6e352-p101">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span>

<span data-ttu-id="6e352-p102">Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren. Wir haben die Zertifizierungserstellungslogik im Paket *@microsoft/gulp-core-build-serve* aktualisiert. In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen. Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem mit der Zertifizierungserstellungslogik zu beheben.</span><span class="sxs-lookup"><span data-stu-id="6e352-p102">You should update your Yeoman template packages. We have updated certification creation logic in the *@microsoft/gulp-core-build-serve* package. In existing solutions, you can simply delete this folder and run `npm install` to get the updated package. You will also need to execute `untrust-dev-cert` and `trust-dev-cert` commands in your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="6e352-114">Häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="6e352-114">Frequently asked questions</span></span>

<span data-ttu-id="6e352-115">**Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint Framework verfügbar sein?**</span><span class="sxs-lookup"><span data-stu-id="6e352-115">**When will custom actions and JSLink be available in the SharePoint Framework?**</span></span>

- <span data-ttu-id="6e352-116">*Datum - 6. Juni*</span><span class="sxs-lookup"><span data-stu-id="6e352-116">*Date - 6th of June*</span></span>

<span data-ttu-id="6e352-117">SharePoint-Framework-Erweiterungen mit zusätzlichen Anpassungsmöglichkeiten sind jetzt in SharePoint Online verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6e352-117">SharePoint Extensions with additional customizations capabilities for the SharePoint Online is now available in SharePoint Online.</span></span> <span data-ttu-id="6e352-118">Weitere Informationen zu den SharePoint-Framework-Erweiterungen finden Sie in unserer Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="6e352-118">You can find more details on the SharePoint Framework extensions from our documentation.</span></span>

- [<span data-ttu-id="6e352-119">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="6e352-119">SharePoint Framework Extensions Overview</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="6e352-120">Lernprogramme zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="6e352-120">SharePoint Framework Extensions Tutorials</span></span>](./extensions/get-started/build-a-hello-world-extension.md)

<span data-ttu-id="6e352-121">**Wird SharePoint-Framework auch in lokalen Bereitstellungen verfügbar sein?**</span><span class="sxs-lookup"><span data-stu-id="6e352-121">**Will SharePoint Framework be available in on-premises?**</span></span>

- <span data-ttu-id="6e352-122">*Datum - 6. Juni*</span><span class="sxs-lookup"><span data-stu-id="6e352-122">*Date - 6th of June*</span></span>

<span data-ttu-id="6e352-123">Die clientseitigen Webparts von SharePoint-Framework auf klassischen Seiten werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="6e352-123">SharePoint Framework client-side web parts on classic pages were released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> <span data-ttu-id="6e352-124">Es gibt derzeit keine Pläne, SharePoint-Framework-Funktionen für SharePoint 2013 bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6e352-124">There are no plans currently to provide SharePoint Framework capabilities to SharePoint 2013.</span></span> <span data-ttu-id="6e352-125">Es gibt keine bestimmte Liste der SharePoint-Framework-Funktionen, die in der SharePoint 2019-Version enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="6e352-125">There's no specific list of SharePoint Framework capabilities which will be included in the SharePoint 2019 release.</span></span>

## <a name="see-also"></a><span data-ttu-id="6e352-126">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="6e352-126">See also</span></span>
<span data-ttu-id="6e352-127">Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen:</span><span class="sxs-lookup"><span data-stu-id="6e352-127">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

* <span data-ttu-id="6e352-128">[Problemliste unter „sp-dev-docs“ in GitHub](https://github.com/SharePoint/sp-dev-docs/issues)</span><span class="sxs-lookup"><span data-stu-id="6e352-128">[sp-dev-docs GitHub issue list](https://github.com/SharePoint/sp-dev-docs/issues)</span></span>
* <span data-ttu-id="6e352-129">[SharePoint Developer-Bereich in der Microsoft Tech Community](https://aka.ms/sppnp-community)</span><span class="sxs-lookup"><span data-stu-id="6e352-129">[SharePoint Developer MS Tech Community space](https://aka.ms/sppnp-community)</span></span>
