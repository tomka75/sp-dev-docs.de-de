---
title: Erstellen von Seiten auf einer SharePoint-Website
ms.date: 9/25/2017
ms.openlocfilehash: 349de6ef579d2313ddaa27a178cab9c31654e223
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="authoring-pages-in-a-sharepoint-site"></a>Erstellen von Seiten auf einer SharePoint-Website

Das Erstellen von Seiten in SharePoint ist unkompliziert, erfordert jedoch einige Kenntnisse der SharePoint-Umgebung. Außerdem müssen Sie sich in grundlegenden Zügen bewusst sein, was Sie entwerfen und für wen. Ein paar Grundprinzipien – wie „Einfach beginnen“ und „Auf dem aufsetzen, was funktioniert“ – sind zu Beginn eines Projekts hilfreich. Es ist auch sinnvoll, immer Ihre Zielgruppe und die Ziele im Hinterkopf zu behalten, bei deren Umsetzung Sie sie unterstützen möchten.

<!-- Do we have content about the design principles that we can link to here? -->

Die Erstellungsumgebung für SharePoint Seiten hat zwei Modi: 

- Bearbeitungsmodus: In diesem Modus können Seitenautoren Webparts hinzufügen und konfigurieren, um einer Seite Inhalte hinzuzufügen.
- Modus „Veröffentlicht“: In diesem Modus kann Ihr Team oder Ihre Zielgruppe die Inhalte sehen und mit Webparts interagieren. 

## <a name="edit-mode"></a>Bearbeitungsmodus

Beim Erstellen einer neuen Seite haben Benutzer Zugriff auf die Erstellungsbenutzeroberfläche, um Inhalte hinzuzufügen und den Seiteninhalt anzupassen. 


![Steuerelement „Bearbeiten“](../images/design-authoring-edit-01.png)

![Steuerelement „Bearbeiten“ mit Cursor mit Hervorhebung](../images/design-authoring-edit-02.png)


### <a name="add-hint-and-toolbox"></a>Hinweis zum Hinzufügen und Toolbox

Der Hinweis zum Hinzufügen besteht aus einer horizontalen Linie mit einem Pluszeichen, die angezeigt wird, wenn ein Webpart ausgewählt wird oder wenn auf ein Webpart gezeigt wird. Er markiert, wo Autoren neue Webparts zu ihrer Seite hinzufügen können. Die Toolbox wird geöffnet, wenn ein Benutzer auf das Pluszeichen klickt. Die Toolbox enthält alle Webparts, die einer Seite hinzugefügt werden können.

![Hinweis und Toolbox mit Tools](../images/design-authoring-add-hint.png)


### <a name="toolbar"></a>Symbolleiste

Eine vertikale Symbolleiste und ein umgebendes Feld sind Teil des Frameworks für jedes Webpart und werden von der Seite bereitgestellt. Jedes Webpart stellt in der Symbolleiste eine Bearbeitungs- und eine Löschaktion bereit. 

![Erweiterte Symbolleiste](../images/design-authoring-toolbar.png)


### <a name="active-and-hover-states"></a>Aktiver Zustand und Hover-Zustand

Im Hover-Zustand oder im aktiven Zustand haben die Hinweisleisten als Farbe das primäre Blau oder das primäre Farbdesign für die Website.

![Hover-Zustand und aktiver Zustand](../images/design-authoring-active-hover-01.png)

Das umgebende Feld für ein Webpart ist standardmäßig Grau, wird aber in Primärblau oder dem primären Farbdesign der Website angezeigt, wenn der Mauszeiger auf ihm platziert wird oder wenn das Webpart ausgewählt wird.

![Umgebendes Feld bei Aktivierung und Deaktivierung](../images/design-authoring-active-hover-02.png)


### <a name="contextual-edits"></a>Kontextbezogene Bearbeitungen

Entwerfen Sie eine WYSIWYG-Umgebung für Webparts, sodass Benutzer Informationen eingeben oder Inhalte hinzufügen können, die beim Veröffentlichen angezeigt werden. Diese Inhalte sollten auf der Seite eingegeben werden, sodass der Benutzer nachvollziehen kann, wie sie im Viewer gerendert werden. Titel und Beschreibungen sollten beispielsweise dort eingegeben werden, wo der Text angezeigt werden soll; neue Aufgaben sollten im Kontext der Seite hinzugefügt und geändert werden.

![Formularelement für kontextbezogeneBearbeitungen](../images/design-authoring-contextual-edits.png)


### <a name="item-level-edits"></a>Bearbeitungen auf Elementebene

Die Benutzeroberfläche kann sich innerhalb des Webpart ändern. Text wird zum Beispiel in ein Textfeld umgewandelt, oder auf der Benutzeroberfläche werden Elemente neu angeordnet oder Aufgaben als erledigt markiert. Sie können interaktive Funktionen für Webparts im Bearbeitungsmodus, im Lesemodus oder in beiden Modi aktivieren, je nach Designabsicht.

![Bearbeitung auf Elementebene im ausgewählten Zustand](../images/design-authoring-item-level.png)


### <a name="property-panes"></a>Eigenschaftenbereiche

Eigenschaftenbereiche werden über das **Bearbeiten**-Symbol auf der Symbolleiste aufgerufen. Eigenschaftenbereiche sollten in erster Linie Konfigurationseinstellungen zur Aktivierung oder Deaktivierung von Features enthalten, die entweder auf der Seite angezeigt werden oder Inhalte über den Aufruf eines Diensts rendern. 

![Erweiterter Bereich](../images/design-authoring-panes.png)


## <a name="published-mode"></a>Modus „Veröffentlicht“

Sobald die Seite veröffentlicht wurde, wird die gesamte Bearbeitungsoberfläche für den Betrachter oder Leser der Seite deaktiviert. Will der Benutzer die Seite weiter bearbeiten, muss er oben rechts auf der Befehlsleiste auf die Schaltfläche **Bearbeiten** klicken.

![Schaltfläche „Veröffentlichen“ hervorgehoben](../images/design-authoring-published.png)


## <a name="mobile-view"></a>Mobile Ansicht

Alle SharePoint-Seiten sind [dynamisch](grid-and-responsive-design.md), damit die Seiteninhalte auf mobilen Geräten optimal dargestellt werden. Beim Entwerfen eines Webparts müssen Sie immer vor Augen haben, wie die neuen Seiten Ihrer SharePoint-Website auf unterschiedlichen Geräten gerendert werden.



![Website auf einem Mobilgerät](../images/design-authoring-mobile.png)