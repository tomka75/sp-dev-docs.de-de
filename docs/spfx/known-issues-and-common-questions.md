---
title: "SharePoint-Framework – Bekannte Probleme und häufig gestellte Fragen"
description: "Lösungen für Probleme und Antworten auf häufig gestellte Fragen zum SharePoint-Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 79b580fd263636ccab392f99f11983c24ac08e8b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-known-issues-and-frequently-asked-questions"></a><span data-ttu-id="35c5e-103">SharePoint-Framework – Bekannte Probleme und häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="35c5e-103">SharePoint Framework known issues and frequently asked questions</span></span>

<span data-ttu-id="35c5e-104">Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint-Framework sowie Antworten auf häufig gestellte Fragen.</span><span class="sxs-lookup"><span data-stu-id="35c5e-104">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="35c5e-105">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="35c5e-105">Known issues</span></span>

### <a name="dev-certificate-issue-with-chrome-v58-"></a><span data-ttu-id="35c5e-106">Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)</span><span class="sxs-lookup"><span data-stu-id="35c5e-106">Dev certificate issue with Chrome (v58-)</span></span>

- <span data-ttu-id="35c5e-107">*Datum: 28. April 2017*</span><span class="sxs-lookup"><span data-stu-id="35c5e-107">*Date - April 28, 2017*</span></span>
- <span data-ttu-id="35c5e-108">*Aktualisiert: 2. Mai 2017*</span><span class="sxs-lookup"><span data-stu-id="35c5e-108">*Updated - May 2, 2017*</span></span>

<span data-ttu-id="35c5e-109">Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen.</span><span class="sxs-lookup"><span data-stu-id="35c5e-109">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span> <span data-ttu-id="35c5e-110">Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="35c5e-110">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing  command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span>

<span data-ttu-id="35c5e-111">Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="35c5e-111">You should update your Yeoman template packages.</span></span> <span data-ttu-id="35c5e-112">Wir haben die Zertifizierungserstellungslogik im Paket [*@microsoft/gulp-core-build-serve* aktualisiert](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve).</span><span class="sxs-lookup"><span data-stu-id="35c5e-112">We have updated certification creation logic in the [*@microsoft/gulp-core-build-serve* package](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve).</span></span> 

<span data-ttu-id="35c5e-113">In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen.</span><span class="sxs-lookup"><span data-stu-id="35c5e-113">In existing solutions, you can simply delete this folder and run `npm install` to get the updated package.</span></span> <span data-ttu-id="35c5e-114">Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem der Zertifizierungserstellungslogik zu behoben.</span><span class="sxs-lookup"><span data-stu-id="35c5e-114">You also need to execute `untrust-dev-cert` and `trust-dev-cert` commands on your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="35c5e-115">Häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="35c5e-115">Frequently asked questions</span></span>

### <a name="when-will-custom-actions-and-jslink-be-available-in-the-sharepoint-framework"></a><span data-ttu-id="35c5e-116">Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint-Framework verfügbar sein?</span><span class="sxs-lookup"><span data-stu-id="35c5e-116">When will custom actions and JSLink be available in the SharePoint Framework?</span></span>

- <span data-ttu-id="35c5e-117">*Datum: 6. Juni 2017*</span><span class="sxs-lookup"><span data-stu-id="35c5e-117">*Date - June 6, 2017*</span></span>

<span data-ttu-id="35c5e-118">SharePoint-Framework-Erweiterungen mit zusätzlichen Anpassungsmöglichkeiten sind jetzt in SharePoint Online verfügbar.</span><span class="sxs-lookup"><span data-stu-id="35c5e-118">SharePoint Framework Extensions with additional customizations capabilities is now available in SharePoint Online.</span></span> <span data-ttu-id="35c5e-119">Weitere Informationen zu den SharePoint-Framework-Erweiterungen finden Sie in unserer Dokumentation:</span><span class="sxs-lookup"><span data-stu-id="35c5e-119">You can find more information about SharePoint Framework Extensions from our documentation:</span></span>

- [<span data-ttu-id="35c5e-120">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="35c5e-120">SharePoint Framework Extensions Overview</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="35c5e-121">Lernprogramme zu SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="35c5e-121">SharePoint Framework Extensions Tutorials</span></span>](./extensions/get-started/build-a-hello-world-extension.md)

### <a name="will-sharepoint-framework-be-available-in-on-premises"></a><span data-ttu-id="35c5e-122">Wird SharePoint-Framework auch in lokalen Bereitstellungen verfügbar sein?</span><span class="sxs-lookup"><span data-stu-id="35c5e-122">Will SharePoint Framework be available in on-premises?</span></span>

- <span data-ttu-id="35c5e-123">*Datum: 6. Juni 2017*</span><span class="sxs-lookup"><span data-stu-id="35c5e-123">*Date - June 6, 2017*</span></span>

<span data-ttu-id="35c5e-124">Die clientseitigen Webparts von SharePoint-Framework auf klassischen Seiten werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="35c5e-124">SharePoint Framework client-side web parts on classic pages were released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> <span data-ttu-id="35c5e-125">Es gibt derzeit keine Pläne, SharePoint-Framework-Funktionen für SharePoint 2013 bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="35c5e-125">There are no plans currently to provide SharePoint Framework capabilities to SharePoint 2013.</span></span> <span data-ttu-id="35c5e-126">Es gibt keine bestimmte Liste der SharePoint-Framework-Funktionen, die in der SharePoint 2019-Version enthalten sein werden.</span><span class="sxs-lookup"><span data-stu-id="35c5e-126">There's no specific list of SharePoint Framework capabilities which will be included in the SharePoint 2019 release.</span></span>

## <a name="see-also"></a><span data-ttu-id="35c5e-127">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="35c5e-127">See also</span></span>

<span data-ttu-id="35c5e-128">Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="35c5e-128">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

- [<span data-ttu-id="35c5e-129">SharePoint-Entwicklungsdokumente auf GitHub zu Problemen</span><span class="sxs-lookup"><span data-stu-id="35c5e-129">GitHub sp-dev-docs issues</span></span>](https://github.com/SharePoint/sp-dev-docs/issues)
- [<span data-ttu-id="35c5e-130">Microsoft Tech Community-Bereich für SharePoint-Entwickler</span><span class="sxs-lookup"><span data-stu-id="35c5e-130">SharePoint Developer MS Tech Community space</span></span>](https://aka.ms/sppnp-community)

