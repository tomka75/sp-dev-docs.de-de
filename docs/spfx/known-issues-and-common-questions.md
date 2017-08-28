# <a name="known-issues-and-frequently-asked-questions"></a><span data-ttu-id="a49ea-101">Bekannte Probleme und häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="a49ea-101">Known issues and frequently asked questions</span></span>

<span data-ttu-id="a49ea-102">Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint Framework sowie Antworten auf häufig gestellte Fragen.</span><span class="sxs-lookup"><span data-stu-id="a49ea-102">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="a49ea-103">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="a49ea-103">Known issues</span></span>

<span data-ttu-id="a49ea-104">**Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)**</span><span class="sxs-lookup"><span data-stu-id="a49ea-104">**Dev certificate issue with Chrome (v58-)**</span></span>

- <span data-ttu-id="a49ea-105">*Datum – 28. April*</span><span class="sxs-lookup"><span data-stu-id="a49ea-105">*Date - 28th of April*</span></span>
- <span data-ttu-id="a49ea-106">*Aktualisiert – 2. Mai*</span><span class="sxs-lookup"><span data-stu-id="a49ea-106">*Updated - 2nd of May*</span></span>

<span data-ttu-id="a49ea-p101">Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen. Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a49ea-p101">If you are using a Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed it's model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing local workbench.</span></span>

<span data-ttu-id="a49ea-p102">Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren. Wir haben die Zertifizierungserstellungslogik im Paket *@microsoft/gulp-core-build-serve* aktualisiert. In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen. Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem mit der Zertifizierungserstellungslogik zu beheben.</span><span class="sxs-lookup"><span data-stu-id="a49ea-p102">You should updated your Yeoman template packages. We have updated certification creation logic in the *@microsoft/gulp-core-build-serve* package. In existing solutions, you can simply delete this folder and run `npm install` to get the updated package. You will also need to execute `untrust-dev-cert` and `trust-dev-cert` commands in your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="a49ea-113">Häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="a49ea-113">Frequently asked questions</span></span>

<span data-ttu-id="a49ea-114">**Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint Framework verfügbar sein?**</span><span class="sxs-lookup"><span data-stu-id="a49ea-114">**When will custom actions and JSLink be available in the SharePoint Framework?**</span></span>

- <span data-ttu-id="a49ea-115">*Datum - 6. Juni*</span><span class="sxs-lookup"><span data-stu-id="a49ea-115">*Date - 6th of June*</span></span>

<span data-ttu-id="a49ea-p103">SharePoint Extensions mit weiteren anpassbaren Funktionen für SharePoint Online sind nun für die Entwicklervorschau verfügbar. Derzeit ist noch kein Datum für die allgemeine Verfügbarkeit (GA) festgelegt. Mithilfe der folgenden Lernprogramme können Sie sich mit dem Erstellen von Erweiterungen vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="a49ea-p103">SharePoint Extensions with additional customizations capabilities for the SharePoint Online is now available for dev preview. We do not have public GA date currently. You can start learning how to build these extensions reading following tutorials.</span></span>

* [<span data-ttu-id="a49ea-119">Erste Schritte mit SharePoint Framework Extensions</span><span class="sxs-lookup"><span data-stu-id="a49ea-119">Getting started with SharePoint Framework Extensions</span></span>](http://aka.ms/spfx-extensions)

<span data-ttu-id="a49ea-120">**Wird SharePoint Framework auch in lokalen Bereitstellungen verfügbar sein?**</span><span class="sxs-lookup"><span data-stu-id="a49ea-120">**Will SharePoint Framework be available in on-premises?**</span></span>

- <span data-ttu-id="a49ea-121">*Datum - 6. Juni*</span><span class="sxs-lookup"><span data-stu-id="a49ea-121">*Date - 6th of June*</span></span>

<span data-ttu-id="a49ea-122">Die clientseitigen Webparts von SharePoint-Framework werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="a49ea-122">SharePoint Framework client-side web parts will be released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a49ea-123">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a49ea-123">Additional resources</span></span>
<span data-ttu-id="a49ea-124">Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen:</span><span class="sxs-lookup"><span data-stu-id="a49ea-124">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

* [<span data-ttu-id="a49ea-125">Problemliste unter „sp-dev-docs“ in GitHub</span><span class="sxs-lookup"><span data-stu-id="a49ea-125">sp-dev-docs GitHub issue list</span></span>](https://github.com/SharePoint/sp-dev-docs/issues)
* [<span data-ttu-id="a49ea-126">SharePoint Developer-Bereich in der Microsoft Tech Community</span><span class="sxs-lookup"><span data-stu-id="a49ea-126">SharePoint Developer MS Tech Community space</span></span>](https://aka.ms/sppnp-community)
