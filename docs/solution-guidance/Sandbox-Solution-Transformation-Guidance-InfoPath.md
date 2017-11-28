---
title: Sandkasten-Transformation ausgesprochen - InfoPath
ms.date: 11/03/2017
ms.openlocfilehash: 62a6d4015cbfba99468d47ac11aa1a8cd8271fb0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---infopath"></a>Sandkasten-Transformation ausgesprochen - InfoPath
Bei Verwendung mit Code-Behind in InfoPath forms, dann diese InfoPath-Formulare sind auf codebasierte sandkastenlösungen für die Ausführung von Code-Behind abhängig. In diesem Artikel helfen Ihnen, entweder korrigieren oder Transformieren von InfoPath-Formularen, damit es nicht mehr ist keine Abhängigkeit der Sandkasten-Lösung.

_**Gilt für:** InfoPath-Formulare für SharePoint Online | SharePoint 2013 | SharePoint-2016_

Sandkasten codebasierte Lösungen [als veraltet gekennzeichnet wurden](https://blogs.msdn.microsoft.com/sharepointdev/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions/) , wieder in 2014 und SharePoint online gestartet Upgradeprozess für diese Funktion vollständig zu entfernen. Codebasierte sandkastenlösungen sind auch in SharePoint 2013 und SharePoint 2016 veraltet.

## <a name="analyze-and-if-possible-fix-your-infopath-forms"></a>Analyse und möglichst Korrektur von InfoPath-Formularen
<a name="sectionSection1"> </a>

In diesem Abschnitt lernen Sie, eine Analyse und Beheben von Modell, das Sie zu InfoPath-Formularen anwenden können. Je nach Ihrem Formular können Sie einfach **beheben** des Formulars und erneut es oder Sie müssen **Navigieren Weg von InfoPath** und einen anderen Ansatz benötigte Funktionen zu erkennen. Jedoch vor dem Ausführen dieser Aktionen, die **Es ist wichtig, den unternehmensanforderungen für Ihr Formular bewerten**: wir oft finden Sie eine große Anzahl alter Formulare, die nicht Business relevanten mehr und in diesen Fällen ist es einfacher, um das Formular einfach zu löschen. 

### <a name="how-do-i-know-that-ive-infopath-forms-with-code-behind"></a>Wie weiß ich, dass ich die InfoPath-Formularen mit Code-behind haben?
Die empfohlene Option ist mit dem **[SharePoint-Sandkasten-Lösung Scanner Tool](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool)** wie der Bericht aus diesem Tool angegeben wird, wenn die Sandkasten-Lösung aus einer InfoPath-Datei stammt. Darüber hinaus wird das Tool auch Sie feststellen, ob die verwendete Assembly in der Projektmappe "nicht verwendbar", wie später in diesem Artikel beschrieben wird.

### <a name="are-my-forms-still-relevant"></a>Sind meine Formulare noch relevant?
Vor dem Einstieg in die Arbeit Remediation-Transformation es ist wichtig, die Frage: ist diese weiterhin entscheidend für mein Unternehmen. Wenn also anschließend, fahren Sie mit der nächsten Kapitel Wenn nicht die Daten berücksichtigen müssen Sie mithilfe dieses Formulars erstellt. In der Regel wurde die Daten erstellt InfoPath XML welche in einer SharePoint-Liste live Dateien. Wenn Sie das Formular entfernen kann Sie werden nicht mehr Visualisieren von Daten sein: manchmal kann, die kein Problem seit Formular- und Daten sind nicht relevant mehr, aber für den Fall, dass Sie Zugriff auf die Daten sicherstellen wollen können Sie die InfoPath-XML-Dateien in SharePoint-Listendaten (Elemente) konvertieren. Die [PnP-Transformation Repository enthält ein Beispiel, das zeigt, wie Sie dies erreichen können](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Migration/EmpRegConsole "Beispiel zeigt, wie Sie Transformieren von InfoPath-XML-auf Listendaten").

### <a name="downloading-the-infopath-form-xsn-file-for-inspection"></a>Herunterladen von InfoPath-Formular (XSN-Datei) für die Überprüfung
Im Abschnitt Schritt, den Sie sichergestellt haben, dass Sie InfoPath-Formulare verfügen, die Arbeit erfordern, in diesem Abschnitt erfahren zum Herunterladen dieser Formulare Sie. InfoPath-Formularen mit Code-behind handelt es sich entweder als "Formularbibliothek" oder als "Websiteinhaltstyp" bereitgestellt. Abhängig von der gewählten veröffentlichungsmodell können Sie die Formulare wie folgt herunterladen.

#### <a name="download-form-library-deployed-infopath-forms"></a>"Formularbibliothek" Download bereitgestellt InfoPath-Formularen
In diesem Fall wird die XSN-Datei in den Ordner Formularen der Formularbibliothek, die das InfoPath-Formular bereitgestellt wurde. Die Formularbibliothek wissen Sie können sehen Sie sich den Namen der WSP-Paket wie folgt dieser Konvention: "InfoPath Form_**LibName**_id". Nachdem Sie die Bibliothek verfügen müssen Sie damit Formularordner die Bibliothek die template.xsn-Datei heruntergeladen werden. Hierzu können Sie eine Url wie folgt erstellen: **Bibliothek Url + "Forms/template.xsn"** wie in diesem Beispiel dargestellt `https://contoso.sharepoint.com/sites/infopath1/IHaveCodeBehind/Forms/template.xsn` und mit dem Browser zum Herunterladen der Datei.

#### <a name="download-site-content-type-deployed-infopath-forms"></a>Download "Websiteinhaltstyp" bereitgestellte InfoPath-Formulare
InfoPath-Formulare, die als Inhaltstyp bereitgestellt haben ihre XSN-Datei gespeichert, die in einer Formularbibliothek, die für den Inhaltstyp als Formular Bereitstellungszeit verbunden wurde. Wie im vorherigen Abschnitt können Sie den Bibliotheksnamen aus dem Namen der WSP-Paket erhalten. Was ist verschiedene diesmal, dass das Formular tatsächlich als in der Bibliothek gefundenen Datei gespeichert wird, sodass Sie einfach aus der Bibliothek herunterladen können. 

### <a name="fixing-your-infopath-forms"></a>Beheben von InfoPath-Formularen
Vorangehenden Abschnitten dargestellt und Sie die InfoPath-Formularen mit Code-behind angegeben haben, aber enthalten sie wirklich nützlich CodeBehind? Was sehen wir besteht darin, dass eine Reihe von Formularen für den Autor des Formulars versehentlich auf die Schaltfläche **Code-Editor** in das Menüband **für Entwickler** von InfoPath geklickt haben:

![Code für InfoPath](media/Sandbox-Solution-Transformation-Guidance-InfoPath/InfoPathCodeBehind.png)

Nachdem Sie dies getan haben Sie Code-behind aber dieses Codes müssen hinter ist nicht jegliche, und Sie können das InfoPath-Formular mit CodeBehind zu einem regulären InfoPath-Formular, das kein Code zurück und ist daher keine Abhängigkeit für sandkastenlösungen verfügt konvertieren, entfernen Sie es!

#### <a name="how-do-i-know-the-code-behind-is-useless"></a>Wissen ich, dass der Code-behind "nicht verwendbar" ist?
Die [SharePoint-Sandkasten-Lösung Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool) informiert Sie zurück, wenn Sie möchten erfahren mehr, und Lesen Sie weiter, die InfoPath nicht verwendbar Code hat jedoch. Sie vielleicht, wie Sie nicht verwendbar und erforderliche CodeBehind unterscheiden, wie Sie nur die erste Kategorie beheben können. Wenn Sie noch das ursprüngliche bereitgestellte Formular (also nicht angegeben, die Sie in den vorherigen Schritten heruntergeladen haben) können Sie einfach einen Blick auf den Code verfügen. Der Standardwert ist leer, Code wird unten gezeigt und wenn Sie ähnlichen Code haben dann dieses Formular kann behoben werden durch den Code ablegen:

```C#
using Microsoft.Office.InfoPath;
using System;
using System.Xml;
using System.Xml.XPath;

namespace Form1
{
    public partial class FormCode
    {
        // Member variables are not supported in browser-enabled forms.
        // Instead, write and read these values from the FormState
        // dictionary using code such as the following:
        //
        // private object _memberVariable
        // {
        //     get
        //     {
        //         return FormState["_memberVariable"];
        //     }
        //     set
        //     {
        //         FormState["_memberVariable"] = value;
        //     }
        // }

        // NOTE: The following procedure is required by Microsoft InfoPath.
        // It can be modified using Microsoft InfoPath.
        public void InternalStartup()
        {
        }
    }
}
```

Für den Fall, dass Sie nur die XSN-Datei verfügen, die Sie im vorherigen Schritt, den Sie umbenennen können heruntergeladen haben Ihre XSN-Datei in eine CAB-Datei (z. B. template.cab), extrahieren Sie die Assembly und mithilfe von .net Reflection-Tools (wie die open-Source- [ILSpy](http://ilspy.net/ "ILSpy der Open-Source-.NET Assembly-Browser und dekompilieren")), mit dem Code zu überprüfen. Eine normale Ansicht der unnötigen Code-behind sieht in ILSpy folgendermaßen aus:

![Unnötigen Code in ILSpy gesehen](media/Sandbox-Solution-Transformation-Guidance-InfoPath/ilspyoutput.png)

#### <a name="dropping-code-behind-from-infopath-forms-to-fix-them"></a>Ablegen von InfoPath-Formularen, deren Korrektur CodeBehind
Wenn Sie sichergestellt haben, dass Ihr Code hinter nicht verwendbar ist können Sie sie auf einfache Weise durch Löschen:
- Öffnen Sie das Formular im **InfoPath-Designer** (Rechtsklick-Design)
- Wechseln Sie zur **Formularoptionen** über Datei - Info
- Wählen Sie aus der Kategorie **Programmierung** , und klicken Sie auf **Code entfernen**
- **Veröffentlichen Sie das Formular erneut** über den Datei - Info - schnell veröffentlichen
- **Deaktivieren der verknüpften Sandkasten-Lösung** über Site Settings - Lösungen
- **Bestätigen** des Formulars funktioniert wie erwartet
- **Löschen** Sie die Sandkasten-Lösung

Wenn Sie den Code für InfoPath XSN-Datei und Quelle mehr **Sie weiterhin beheben, können diese Formulare einfach deaktivieren, die sandkastenlösungen, die nur "nicht verwendbar" Code haben,**keinen Zugriff haben. Führen Sie dies nur für diejenigen, die in der Ausgabe des Sandkasten-Lösung Bericht erwähnten mit IsEmptyInfoPathAssembly = True.

## <a name="migrate-your-infopath-forms"></a>Migrieren von InfoPath-Formularen
<a name="sectionSection2"></a> Wenn die Anleitung im vorhergehenden Kapitel wurde im Wesentlichen bedeutet, dass das Formular wird weiterhin Business relevant und enthält Code-behind, die nicht für das InfoPath-Formular kann nicht gelöscht. Wenn dies der Fall ist ist die typische Lösung Weg von InfoPath verschieben auf verschiedene Weise ausgeführt werden:
- Erstellen einer app mithilfe von [Azure PowerApps](https://powerapps.microsoft.com/en-us/ "Azure PowerApps") oder [Microsoft Fluss](https://flow.microsoft.com/en-us/search/?q=sharepoint "Microsoft Fluss") 

![Azure PowerApps und Microsoft-Flussdiagramm](media/Sandbox-Solution-Transformation-Guidance-InfoPath/powerappsflow.png)

- Erstellen einer SharePoint-Add-In, das nutzt remote API Schreib-/SharePoint-Daten

### <a name="building-sharepoint-add-ins-to-replace-your-infopath-forms"></a>Erstellen von SharePoint Add-In's Ersetzen von InfoPath-Formularen
Wenn Sie zu bestätigen, regulären SharePoint Add-In verwenden, um von InfoPath-Formularen zu ersetzen, müssen Sie mehrere Optionen. Im folgenden sind drei Optionen, die wir noch ausführlicher gearbeitet haben, aber als genannten perfekt können Variationen dieser. Die drei Optionen, die, denen wir in befassen möchten, sind:
- [Eine einzelne Seite Anwendung (SPA) basierend auf knockout.js] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.KnockOut.SinglePageApp "SPA Beispiel mit knockout.js")

![Knockout-Beispiel](media/Sandbox-Solution-Transformation-Guidance-InfoPath/knockoutsample.png)

- [Ein ASP.Net MVC-SharePoint-Add-In] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.MVC "Verwenden von SharePoint-Add-In ASP.Net MVC")
- [ASP.Net Forms-SharePoint-Add-Ins] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.Forms "Verwenden von SharePoint-Add-In ASP.NET-Formulare")

In eine bessere Hilfe zu bilden Sie mit der Konvertierung von Ihrem InfoPath **Wir haben 11 allgemeinen InfoPath Codierungsmuster aufgeführt, und Sie veranschaulichen die Implementierung dieser Muster mithilfe der oben genannten 3 weiter oben erwähnt SharePoint Add-In - Optionen**. Dazu zuerst einen [Verweis InfoPath-Formular](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Reference/EmployeeRegistration "Verweis InfoPath-Formular") der verwendet, die am häufigsten verwendete InfoPath Codierungsmuster entwickelt haben, und klicken Sie dann haben wir dieses Formular zu SharePoint-Add-In Varianten 3 migriert. Unten Links zeigen Sie diese gängiger Muster an:
- [Auffüllen der Felder beim Laden des Formulars - Satz von Benutzerinformationen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-set%20user%20information.md "Auffüllen der Felder beim Laden des Formulars - Satz von Benutzerinformationen")
- [Auffüllen der Felder beim Laden des Formulars - Listeninformationen lesen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-read%20list%20information.md "Auffüllen der Felder beim Laden des Formulars - Listeninformationen lesen")
- [Auffüllen der Felder beim Laden des Formulars - Listendaten lesen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-read%20list%20data.md "Auffüllen der Felder beim Laden des Formulars - Listendaten lesen")
- [Senden Sie das Formular über code] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Submit%20the%20form%20via%20code.md "Senden Sie das Formular über code")
- [Wechsel der Ansicht nach des Sendens von Formularen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Switching%20view%20after%20form%20submission.md "Wechsel der Ansicht nach des Sendens von Formularen")
- [Abrufen von Benutzerdaten] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Retrieving%20user%20data.md "Abrufen von Benutzerdaten")
- [Lesen Sie die Datensammlung und legen Sie mehrere Steuerelemente] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Read%20data%20collection%20and%20set%20multiple%20controls.md "Lesen Sie die Datensammlung und legen Sie mehrere Steuerelemente")
- [Laden von verknüpften Daten] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Cascading%20data%20load.md "Laden von verknüpften Daten")
- [Hochladen oder Löschen von Anlagen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Upload%20or%20Delete%20Attachments.md "Hochladen oder Löschen von Anlagen")
- [Benutzer von hinzufügen oder Entfernen von Websitegruppen] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Add%20or%20remove%20user%20from%20site%20groups.md "Benutzer von hinzufügen oder Entfernen von Websitegruppen")
- [Vorhandene Load-Element im Formular] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Load%20existing%20item%20in%20form.md "Vorhandene Load-Element im Formular")


### <a name="migrating-your-infopath-data"></a>Migrieren der InfoPath-Daten
Sobald Sie über das InfoPath-Formular in einer neuen Lösung, die sollten Sie auch Ihre Daten aus InfoPath XML regulären SharePoint-Listendaten oder der Datenebene Ihrer Wahl zu migrieren verschoben haben. Da von InfoPath-Dateien XML-Dateien ist es relativ einfach gelesen und die umgewandelt. Die [PnP-Transformation Repository enthält ein Beispiel, das zeigt, wie Sie dies erreichen können](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Migration/EmpRegConsole "Beispiel zeigt, wie Sie Transformieren von InfoPath-XML-auf Listendaten").

### <a name="code-based-operations-are-disabled-and-now-my-existing-forms-dont-open-anymore"></a>Codebasierte Vorgänge sind deaktiviert, und Meine Formulare nicht jetzt nicht mehr geöffnet
Als Grundlage Code Vorgänge deaktiviert sind bedeutet dies, dass kein Code nicht mehr im Sandkasten ausgeführt werden kann. Wenn Sie Formulare haben, die Code ausführen bedeutet auch, dass das Öffnen von mit vorhandener Formulare nicht mehr funktionsfähig ist. Unten beschriebenen Schritte helfen Ihnen dies behandeln:
 - Wenn Sie das InfoPath-Formular zu einer neuen Lösung migriert haben dann Sie haben wahrscheinlich bereits konvertiert Ihre Daten und als solche sind gut
 -  Wenn Sie sich entschieden, lassen Sie das Formular wie ist (z. B. da es sich nicht um Business critical mehr) jedoch weiterhin die vorhandenen Formulare öffnen möchten, dann können Sie führen einen der folgenden Schritte:
    - Den Code-behind aus dem Formular zu entfernen und die Veröffentlichung (siehe oben **Ablegen von InfoPath-Formularen, deren Korrektur CodeBehind** )
    - Verwenden von InfoPath-Client die Formulare öffnen
    - Migrieren Sie die Formulardaten zu einfache SharePoint-Listendaten (siehe oben **Migrieren der Daten InfoPath** )

