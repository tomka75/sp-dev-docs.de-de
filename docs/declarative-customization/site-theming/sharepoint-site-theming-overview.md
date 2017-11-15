# <a name="sharepoint-site-theming"></a>SharePoint-Websitedesign

SharePoint-Websitebesitzer haben neue Optionen zum Anwenden benutzerdefinierter Formatvorlagen und Farben auf Websites, die das Definieren und Verwalten von Designs für Websitesammlungen vereinfachen. Die neuen Features umfassen Folgendes:

* Die Möglichkeit zum Definieren von benutzerdefinierten Designs und Verfügbarmachen für Websitebesitzer . Designs werden in einem [JSON-Schema](sharepoint-site-theming-json-schema.md) definiert, das Farbeinstellungen und verwandte Metadaten für jedes Design speichert.
* Ein vereinfachter Satz von Standarddesigns mit sechs hellen Designs und zwei dunklen Designs ist momentan verfügbar.
* Steuern Sie, welche Designs für die Verwendung auf Seiten auf Ihren Websites zur Verfügung stehen. Sie können z. B. benutzerdefinierte Designs basierend auf dem Branding oder der Identität Ihrer Organisation definieren und diese zu den einzig verfügbaren Designs auf Ihren Websites machen.

Diese Funktionen stehen für Administratoren über [PowerShell-Cmdlets](sharepoint-site-theming-powershell.md) und für Entwickler über das [clientseitige SharePoint-Objektmodell (Client Side Object Model, CSOM)](sharepoint-site-theming-csom.md) oder die SharePoint- [REST-API-](sharepoint-site-theming-rest-api.md) zur Verfügung.

Allgemeine Informationen zum Arbeiten mit Designs, um das Aussehen Ihrer Websites anzupassen, finden Sie unter [Ändern des Aussehens Ihrer SharePoint-Website](https://support.office.com/en-us/article/Change-the-look-of-your-SharePoint-site-06bbadc3-6b04-4a60-9d14-894f6a170818).

## <a name="default-themes"></a>Standardmäßige Designs

Die folgenden vordefinierten Designs sind standardmäßig verfügbar:

* __Blau__
* __Orange__
* __Rot__
* __Lila__
* __Grün__
* __Grau__
* __Dunkelgelb__ (invertiertes Design)
* __Dunkelblau__ (invertiertes Design)

Diese Designs wurde zur besseren Lesbarkeit entwickelt. Sie sind möglicherweise hilfreich als Ausgangspunkte für das Erstellen von benutzerdefinierten Designs. Weitere Informationen zu Standarddesigns finden Sie unter [SharePoint-Websitedesign: JSON-Schema](sharepoint-site-theming-json-schema.md).

## <a name="selecting-a-modern-theme"></a>Auswählen eines modernen Designs

<!-- Verify that it's okay to use the concept of "modern" themes/pages here? -->

Um aus den verfügbaren Designs einer SharePoint-Website auszuwählen, wählen Sie in der oberen rechten Ecke des Bildschirms das __Zahnradsymbol (⚙️)__, und wählen Sie dann __ Erscheinungsbild ändern__ aus. Es wird eine Liste von Designs zur Auswahl präsentiert, die Standarddesigns und/oder benutzerdefinierte Designs enthalten kann, je nachdem, wie Ihre Website konfiguriert wurde.

Die folgende Abbildung zeigt, wie die Standarddesigns im Dialogfeld der Designauswahl angezeigt werden.

![Abbildung mit einer Liste von standardmäßigen und dunklen (invertierten) Designs](../../images/theme-defaults.png)

Wenn Sie in der Liste ein Design auswählen, werden diese Farbeinstellungen sofort auf der Seite angewendet, damit Sie sehen können, wie das ausgewählte Design aussieht. Die folgende Abbildung zeigt ein Beispiel mit dem Standarddesign __Grün__.

![Abbildung einer SharePoint-Website mit einem grünen Design](../../images/theme-greenselected.png)

Nachdem Sie ein Design gefunden haben, das Sie verwenden möchten, wählen Sie **Speichern**, um Ihre Auswahl zu speichern, oder **Abbrechen**, um das aktuelle Design wiederherzustellen.

## <a name="working-with-classic-themes"></a>Arbeiten mit klassischen Designs

Sie können weiterhin die klassischen Designs verwenden, indem Sie den Link zu _klassischen Optionen (Erscheinungsbild ändern)_ unter den modernen Designs unter _ Erscheinungsbild ändern_ wählen. Da sich die moderne SharePoint-Benutzeroberfläche von der klassischen Benutzeroberfläche unterscheidet, gelten jedoch einige Einschränkungen, wenn Sie klassische Designs mit modernen Seiten verwenden.

Wenn Sie ein klassisches Design auswählen, wird ein modernes Design aus den Einstellungen im klassischen Design generiert, einschließlich der isInverted-Kennzeichnung, des Hintergrundbilds und der Farbeinstellungen für COntentAccent1, PageBackground und BackgroundOverlay. Wenn isInverted auf „True“ festgelegt ist, werden neutrale Farben wie NeutralDark und NeutralLight umgekehrt.

Für Benutzerfreundlichkeit empfehlen wir, dass Sie moderne Designs mit modernen Seiten verwenden. Wenn Sie klassische Designs mit modernen Seiten verwenden müssen, testen Sie Ihre Website sorgfältig, um sicherzustellen, dass Ihre Inhalte lesbar und zugänglich sind.

## <a name="see-also"></a>Siehe auch

* [SharePoint-Websitedesign: JSON-Schema](sharepoint-site-theming-json-schema.md)
* [SharePoint-Websitedesign: PowerShell-Cmdlets](sharepoint-site-theming-powershell.md)
* [SharePoint-Websitedesign: CSOM](sharepoint-site-theming-csom.md)
* [SharePoint-Websitedesign: REST-API](sharepoint-site-theming-rest-api.md)
