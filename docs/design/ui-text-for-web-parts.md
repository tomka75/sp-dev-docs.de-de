---
title: "Richtlinien für Benutzeroberflächentext in SharePoint-Webparts"
ms.date: 9/25/2017
ms.openlocfilehash: a274b2e0b5394d2af0946a166171f05769f57626
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="ui-text-guidelines-for-sharepoint-web-parts"></a>Richtlinien für Benutzeroberflächentext in SharePoint-Webparts
 
Eine wichtige Voraussetzung für die Erstellung effektiver Webparts in SharePoint ist die Verwendung von einfachem, verständlichem und präzisem Benutzeroberflächentext. Klare und leicht nachvollziehbare Formulierungen stellen sicher, dass Kunden schnell in der Oberfläche des Webparts navigieren und unkompliziert die Inhalte finden können, die sie suchen. In diesem Artikel finden Sie eine Anleitung für die Formulierung von Benutzeroberflächentext für wichtige Bereiche innerhalb von SharePoint-Webparts. (Die Anleitung bezieht sich auf englischsprachigen Text.)


## <a name="capitalization"></a>Großschreibung

Verwenden Sie den sogenannten „sentence case“ (Groß- und Kleinschreibung im Satz: erster Buchstabe des ersten Worts großgeschrieben, der Rest vollständig in Kleinbuchstaben) für alle Benutzeroberflächenelemente, einschließlich Schaltflächen, Seitentiteln und Steuerelementbeschriftungen. 


Schreiben Sie Folgendes immer groß:

- Das erste Wort eines neuen Satzes
- Das Wort nach einem Doppelpunkt in einem Titel oder einer Überschrift (Beispiel: „Step 1: Begin by entering your account information.“)
- Eigennamen, zum Beispiel Namen von Personen und Städten 
 
![Ein Bild-Webpart mit hervorgehobenem „sentence case“](../images/design-uitext-01.png)
![Ein Bild-Webpart mit hervorgehobenem „sentence case“](../images/design-uitext-02.png)


## <a name="punctuation"></a>Zeichensetzung

Befolgen Sie die grundlegenden Zeichensetzungsregeln, um Grammatikfehler in Ihrer Oberfläche zu vermeiden. Die folgende Tabelle enthält einen kurzen Überblick darüber, welche Satzzeichen wann verwendet werden sollten und warum (für die Sprache Englisch).

| Satzzeichen  | Tipp                                                                                                                                                       | Beispiel                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| Doppelpunkte (:)   | Verwenden Sie Doppelpunkte nach der Einleitung einer Liste in der Webpartbeschreibung. Verwenden Sie keine Doppelpunkte in Benutzeroberflächenbeschriftungen.                                                           | Choose one of the following: Cats, Dogs, Quokkas                                                                 |
| Kommas (,)   | Verwenden Sie Kommas in Aufzählungen (auch vor dem Wort „and“).                                                                                                           | I like cats, birds, and dogs.                                                                                  |
| Auslassungspunkte (...) | Verwenden Sie Auslassungspunkte zur Kennzeichnung von abgeschnittenem Text sowie für Fortschrittsmeldungen. Verwenden Sie Auslassungspunkte nicht als Hinweis darauf, dass der Benutzer eine weitere Auswahl treffen muss.          | Abgeschnittener Text: Last modified by John Armstr…<br/>Fortschrittsmeldung: Uploading…                                       |
| Punkte (.)  | Verwenden Sie keine Punkte in Titeln, Überschriften oder Beschriftungen. Verwenden Sie keine Punkte für den Text von Optionsfeldern oder Kontrollkästchen. Verwenden Sie Punkte in Beschreibungen wie gewohnt. | Select the content you want to highlight and how you want it displayed. Use a filter to narrow your selection. |



## <a name="voice-and-tone"></a>Stil und Umgangston

Innerhalb Ihres Produkts den richtigen Ton bei der Kommunikation mit dem Benutzer zu treffen, ist für den Aufbau einer stabilen, langfristigen Beziehung zu Ihrer Zielgruppe sehr wichtig. Versuchen Sie, klare und deutliche Worte zu finden und herzlich, entspannt und zugänglich zu klingen. Die Art und Weise, wie Sie mit Ihrer Zielgruppe sprechen, beeinflusst, wie sich diese auf Ihre Website und Ihre Inhalte einlässt und wie viel Nutzen sie daraus zieht.

**Dos:**

- Verwenden Sie in der Benutzeroberfläche einen zwanglosen Umgangston. 
- Verwenden Sie Schmelzworte. (Beispiel: „can‘t“ statt „cannot“)
- Lesen Sie Ihren Benutzeroberflächentext laut vor, um ein Gefühl dafür zu bekommen, wie er wirkt. Klingt er wie Alltagssprache?
- Verwenden Sie einfache Wörter. 
- Erwähnen Sie keine technischen Details, wenn sie für den Benutzer nicht relevant sind. 
- Verwenden Sie „Please“ nur, wenn Sie dem Benutzer Unannehmlichkeiten bereiten. Vermeiden Sie eine übermäßige Verwendung.
- Verwenden Sie „Sorry“ nur in Fehlermeldungen in SharePoint, die zu schwerwiegenden Problemen für den Kunden führen. 


**Don’ts:**

- Überladen Sie Benutzeroberflächentext nicht mit unnötigen Wiederholungen. Jedes Wort sollte aussagekräftig sein. 


## <a name="pronouns"></a>Pronomen

Vermeiden Sie nach Möglichkeit Pronomen in Benutzeroberflächenelementen. Wenn Sie etwas genauso gut auch ohne ein Pronomen sagen können, dann verwenden Sie keins.

Wenn Ihr Design den Einsatz von Pronomen rechtfertigt, sollten Sie die folgenden Richtlinien beherzigen, um sicherzustellen, dass Sie sie auch korrekt verwenden:

**Dos:**

- Verwenden Sie die zweite Person („you“ oder „your“), wenn Sie sich auf etwas beziehen, das dem Benutzer gehört. (Beispiel: „Your drafts“ oder „Your images“)
- Verwenden Sie die erste Person („me“ oder „my“) für Benutzeroberflächenelemente, mit denen der Benutzer den Dienst anweist, etwas zu tun. (Beispiel: „Alert me when someone responds to my post.“)
- Verwenden Sie „they“ oder „their“ als Possessivbestimmungswort im Singular, um umständliche „he/she“- bzw. „his/her“-Konstruktionen zu vermeiden. Schreiben Sie den Satz im Idealfall in den Plural um.
- Vermeiden Sie die Verwendung von „them“; verwenden Sie stattdessen Wörter wie „someone“ oder „people“. (Beispiel: „Enter a user name and domain to give someone permission to use this PC.“)

![Eine Abbildung der richtigen Verwendung der zweiten Person „you“ und der falschen Verwendung der dritten Person „Users“ in der Benutzeroberfläche ](../images/design-uitext-03.png)
 ![Eine Abbildung der richtigen Verwendung des Benutzeroberflächentexts „Select the page you want people to see first“](../images/design-uitext-04.png)


**Don’ts:**

- Verwenden Sie nicht die dritte Person. Das klingt unpersönlich und kann dazu führen, dass sich der Kunde kaum angesprochen fühlt. Verwenden Sie statt „Users can change the layout“ eine Formulierung wie „You can change the layout“.



## <a name="error-messages"></a>Fehlermeldungen

Fehler treten in jeder Software und jedem Dienst auf. Ihre Fehlermeldungen können direkten Einfluss auf die Gesamtzufriedenheit der Benutzer mit Ihrem Produkt haben. Eine gute Fehlermeldung sollte folgende Merkmale aufweisen:

- Sie sollte eindeutig darüber informieren, was geschehen ist und warum.
- Sie sollte eine provisorische oder permanente Lösung vorschlagen.
- Sie sollte Mitgefühl ausdrücken.

<!-- You might need to explain how to show empathy in an error message, without using "sorry". -->

Unten sehen Sie ein Beispiel für eine Fehlermeldung, die angezeigt wird, wenn ein Benutzer versucht, eine Seite zu bearbeiten, die von einem anderen Benutzer ausgecheckt wurde.


| Keine Bearbeitung möglich                                                |
|-------------------------------------------------------------------------|
| Die Seite wird zurzeit von einem anderen Benutzer bearbeitet. Versuchen Sie es in einigen Minuten erneut. |


## <a name="links-to-help-articles"></a>Links zu Hilfeartikeln

Bemühen Sie sich darum, Links zu Hilfeartikeln strategisch zu setzen. Versuchen Sie, vorherzusehen, wo der Benutzer Hilfe benötigen könnte, und platzieren Sie einen Link zu dem passenden Hilfeartikel nahe bei dem betreffenden Benutzeroberflächenelement. Unten haben wir einige wichtige Tipps zusammengestellt, die Sie beachten sollten, wenn Sie in Ihrer Benutzeroberfläche Links zu Hilfeartikeln platzieren:

**Dos:**

- Hilfelinks im Produkt sollten spezifisch sein. Stellen Sie sicher, dass der Zielartikel thematisch passt. Wenn Benutzer den Artikel öffnen, sollten sie die benötigten Informationen finden können. 
- Formulieren Sie den Linktext in natürlicher Sprache.  

<!-- You might want to provide an example of "natural" language. -->

**Don’ts:**

- Platzieren Sie nicht neben jedem Benutzeroberflächenelement einen Link zu einem Hilfeartikel. Dadurch wirkt die Oberfläche schnell überladen.
- Platzieren Sie nicht mehrere Links zum gleichen Ziel in ein und derselben Benutzeroberfläche.
- Verwenden Sie nicht „click here“ als Linktext. 

![Eine Abbildung mit dem Hilfelinktext „More information and examples“](../images/design-uitext-05.png)


## <a name="hint-text"></a>Hinweistext

Hinweistext oder Geistertext sind Textelemente, die in einem Benutzeroberflächenelement (in der Regel in Textfeldern) angezeigt werden, um dem Benutzer Tipps zur Interaktion mit dem Element zu geben. Der Hinweistext informiert den Benutzer darüber, was er in das Feld eingeben soll. So kann er über Einschränkungen für das Feld informieren oder ein Beispiel geben.

**Dos:**

- Verwenden Sie Hinweistext sparsam und nur, wenn er den Benutzern hilft. Nicht alle Benutzeroberflächenelemente erfordern einen Hinweistext. Bei einigen komplexen Feldern kann Hinweistext mehr Kontext und Klarheit bieten. Beispiel: Bei einem Feld, in das der Benutzer eine sichere URL eingeben muss, ist der Hinweistext „https://www.example.com“ möglicherweise hilfreicher als der Text **Hier sichere URL eingeben.**

**Don’ts**

- Wiederholen Sie nicht einfach nur die Beschriftung: Bei einem Textfeld mit der Beschriftung **Name** beispielsweise ist der Hinweistext **Namen eingeben** redundant und eventuell sogar verwirrend.

Der folgende Hinweistext ist für das Einbetten-Webpart gedacht. In das Textfeld kann eine sichere Websiteadresse oder ein iFrame-Einbettungscode eingegeben werden. Der Text zeigt ein Beispiele für jede der beiden Varianten. 

![Webpart-Hinweistext](../images/design-uitext-06.png)