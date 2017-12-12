# <a name="introduction"></a>Einführung
Die meisten SharePoint Online Mandanten behandelt die Datei open Erfahrung mit dem **strict** Objektmodell. Daher alle Dateien, die potenziell Schaden (z. B. eine HTML-Datei mit dem Skript eingebettet) führen können nicht im Browser ausgeführt, aber heruntergeladen oder als unformatierten Inhalt (html Preview die moderne Benutzeroberfläche) angezeigt. Wenn Ihre Mandanten mit konfiguriert wurde die **permissive** modellieren, und klicken Sie dann die Datei öffnen Erfahrung führen Sie die Datei wird, beispielsweise eine HTML-Datei in einer Dokumentbibliothek ausgeführt und Seite im Browser angezeigt wird. Würde strict dieser Datei heruntergeladen werden.

Die Standardeinstellung ist heute strict, und Sie können nicht bereits auf das Objektmodell permissive wechseln Ihres Mandanten. Für Mandanten, die die letzten Schritte zu permissive gewechselt geändert werden: permissive Mandanten Modell wird als veraltet markiert, an dieser Stelle alle Mandanten werden umgestellt werden strikte.


# <a name="is-my-tenant-impacted"></a>Betroffen Meine Mandanten ist davon?
Es wird empfohlen, Sie können diese durch die Einstellung der PermissiveBrowserFileHandlingOverride von [Office 365 PowerShell für SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx)überprüfen:

```PowerShell
Connect-SPOService -url https://contoso-admin.sharepoint.com
$tenant = get-spotenant
$tenant.PermissiveBrowserFileHandlingOverride
```

Wenn dies **False** führt ist dann Ihres Mandanten nicht betroffen sind, wenn dies auf **True** festgelegt ist, und klicken Sie dann die bevorstehende das Verwerfen der Vorbereitung müssen. 

# <a name="how-can-i-prepare-for-changing-permissive-into-strict"></a>Wie kann ich Vorbereiten für permissive in strict ändern?

![Zeigt permissive strict Modell](media/permissivetostrictmodel.png)

## <a name="step-1-assess-the-impact"></a>Schritt 1: Bewerten der Auswirkungen
Grundlegendes zu viele Dateien betroffen sind, ist ein erster Schritt und Sie können, die über den Dateiscanner permissive. Finden Sie in der [SharePoint-Permissive Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) erfahren Sie mehr über den Scanner und Verwendungsweise. In der Standardkonfiguration dieser Scanner sucht nach html/html-Dateien, aber Sie können mithilfe der Befehlszeilenoptionen den Scanner zu suchenden zusätzliche Filetypes anfordern.

Das Ergebnis der Scanner mit allen CSV-Datei ist die betroffener (html/Htm + optional andere Dateitypen) Dateien, einschließlich Informationen zu den html/Htm-Dateien (Anzahl der Links und Skripts, die verwendet werden).

## <a name="step-2-analyze-the-scan-results"></a>Schritt 2: Analysieren der Überprüfungsergebnisse
Nachdem Sie die Liste der betroffenen Dateien haben müssen Sie die bewerten, wenn diese Dateien und die Websites, halten diese Dateien weiterhin Business relevant sind. Die Datei und/oder Website möglicherweise veraltet und, wenn also Remediation dieser Dateien/Sites übersprungen werden kann. Unterstützen Sie beim Verständnis der geschäftlicher Bedarf der Bericht enthält die Website-Auflistung Administratoren und Websitebesitzer, bietet Ihnen die benötigte Informationen, um sie zu kontaktieren.

## <a name="step-3-remediate-the-files"></a>Schritt 3: Warten von Dateien
Wenn die Dateien wichtig sind und Sie weiterhin die Dateien sollten nach der Mandanten, um die Einstellung strict verschoben wurde ausgeführt werden müssen Sie die Dateien zu warten, wie in den nächsten Kapiteln erläutert. 

# <a name="remediation-process-for-htmlhtm-files"></a>Remediation-Prozess für html/Htm-Dateien
Der Hauptgrund für Kunden permissive Modus wann immer möglich ist, da sie HTML-Dateien aus innerhalb einer Dokumentbibliothek verwenden können möchten. Wie bereits erwähnt, sobald auf strict verschoben diese Dateien einfach herunterladen und mehr nicht automatisch geöffnet werden.
Für diese html/HTML-Dateien der Wartung ist einfach: Wenn eine Benutzer /-app mit Websitebesitzer oder Berechtigungen der Websitesammlung Admin die html/Htm-Dateien in ASPX-Dateien benennt, und klicken Sie dann diese Dateien erneut geöffnet. [Plug & Play-PowerShell für SharePoint](https://aka.ms/sppnp-powershell) -zeigt ein wie dies möglich. Angenommen, Sie haben eine HTML-Datei mit der folgenden Url: https://contoso.sharepoint.com/sites/permissive/html/newfile.html. 

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Rename-PnPFile -ServerRelativeUrl /sites/permissive/html/newfile.html -TargetFileName newfile.aspx -OverwriteIfAlreadyExists
```

## <a name="who-can-perform-this-rename"></a>Wer umbenennen ausführen können?
Die Rename muss ausgeführt werden, von Benutzern mit der Berechtigung AddAndCustomizePages (ACP), die standardmäßig Websitesammlungs-Administratoren oder Websitebesitzer erteilt wird. Bearbeiten Sie das Umbenennen von einem Benutzer mit erfolgt die Berechtigungsstufe (in diesem Fall Websitemitglieder) und klicken Sie dann die Rename erfolgt, aber die resultierende ASPX-Datei ist nicht für die Ausführung markiert und als solche werden heruntergeladen und nicht ausgeführt. 

Bei einer Sammeloperation umbenannt werden soll Sie wahrscheinlich einen app-Prinzipal anstelle eines Benutzerkontos und es gilt: app-Prinzipals benötigt eine Berechtigung für die ACP (z. B. Vollzugriff Berechtigungsstufe) für diesen Vorgang.

## <a name="what-about-embedded-links-to-other-htmlhtm-files"></a>Was geschieht mit eingebetteten Links zu anderen html/Htm-Dateien?
Mein html/Htm-Dateilink zu anderen html/Htm-Dateien im selben Ordner oder in einem Unterordner... wird diese Links Unterbrechung, wenn die Dateien auf Aspx umbenannt werden? Die zugrunde liegende Rename erfolgt den MoveTo-API-Aufruf verwenden, und klicken Sie dann die meisten der relativen Links in der HTML-Datei automatisch aktualisiert werden, um Links zu... Aspx-Dateien werden Umbenennen im Wesentlichen eine Struktur der geschachtelten html/Htm-Dateien, die miteinander verknüpft nur möglich durch die tatsächlichen Dateien umbenennen, werden alle Links in die Dokumente durch die Rename behandelt.

> [!NOTE]
> Die automatische Umbenennung funktioniert nicht, wenn das html-Dokument Links, die in einer anderen Websitesammlung oder enthält Wenn die Links dynamisch generiert werden mithilfe von JavaScript-Dateien zeigen. In diesen Fällen müssen manuelle Aktionen Fixup die Links.

## <a name="what-about-sites-having-the-noscript-feature-enabled"></a>Was geschieht mit Websites mit der Funktion "Noscript" aktiviert
Alle "modernen" Websites (moderne Teamwebsite, Kommunikation Site) haben das "Noscript" Feature standardmäßig aktiviert. Das Ergebnis dieses ist, niemand, der die Berechtigung AddAndCustomizePages (ACP) verwendet werden, damit niemand eine erfolgreiche Umbenennen von html/Htm auf Aspx durchführen können. In der Regel live die html/Htm-Dateien in (migrierten) klassische Teamwebsites, damit dieses Problem nicht vorhanden ist. In der Groß-/Kleinschreibung, den, die Sie in einer Website "Noscript" arbeiten, müssen Sie erste Deaktivieren des Features "Noscript" führen Sie die benennt und klicken Sie dann auf "Noscript" erneut aktivieren. Dementsprechend die html/Htm-Dateien erneut ausgeführt werden können, aber führen Sie beachten Sie, dass jede Änderung für diese Dateien werden als nicht ausführbar erneut markieren, wird. Deaktivieren "Noscript" erneut aus, und Aktualisieren der Datei werden dies behandelt.

## <a name="in-the-modern-document-library-experience-the-aspx-file-initially-do-not-seem-to-open"></a>Moderne Document Library Oberfläche die Aspx-Datei zunächst nicht scheinen öffnen?
Die moderne Document Library Erfahrung "wird davon ausgegangen" ein bestimmten Dateityps, wenn die Datei wurde hinzugefügt, und beim Zugriff auf die Datei zum ersten Mal sehen Sie, dass fälschlicherweise Aspx-Dateien geöffnet werden. Zweiter Versuch führt jedoch die Datei aus. Geben Sie die vermeiden dieses Problems, die zum programmgesteuerten Pull nach unten einmal für jede umbenannte Datei empfohlen wird die SharePoint die Möglichkeit, die Datei richtig festgelegt haben. Zeigt eine wie [SharePoint Plug & Play-PowerShell](https://aka.ms/sppnp-powershell) kann dies erfolgen:

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Get-PnPFile -Url /sites/permissive/html/newfile.aspx -Path c:\temp -Filename newfile.aspx -AsFile
```

# <a name="remediation-of-other-file-types"></a>Behebung von anderen Dateitypen
HTML/Htm-Dateien sind als Hauptgrund für Kunden, die permissive Modus, aber was zu anderen Dateitypen verwenden? Für viele Dateiformate bietet SharePoint Online eine einer Vorschaufunktion wie in diesem [Blog](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040)erläutert. SharePoint Online können die folgenden Formate eine Vorschau anzeigen:

## <a name="documents"></a>Dokumente
CSV, Doc, Docm, DOCX-, DOTX-, Eml, msg, Odp, ods Odt, Pdf, POT-, potm-, Potx, Pps, Ppsx, ppt, Pptm, Pptx, Rtf, Vsd, Vsdx, Xls, Xlsb, Xlsm, Xlsx

## <a name="images"></a>Bilder
AI, Arw, Bmp, cr2, Eps, gibt Erf, Gif, Ico, Symbol, Jpeg, Jpg, Mrw, Nef, Orf, Pict, Png, Psd, Tif, tiff

## <a name="video"></a>Video
3GP, m4v, Mov, MP4 (engl.), WMV (engl.)

## <a name="3d"></a>3D
3mf, Fbx, Obj, Blatt, stl

## <a name="medical"></a>Medizinische
DCM, dcm30, Dic, Dicm, dicom

## <a name="text-and-code"></a>Text und code
ABAP, Ada, adp, Ahk, als, as3, Asc, ASCX-Datei, Asm, Asp, Awk, Bash, Bash_login, Bash_logout, Bash_profile, Bashrc, Bat, Literaturverzeichnis, Bsh, Build, Generator, C, C ++ Capfile, cc, cfc, cfm, Cfml, cl, Clj, Cls, Cmake, Cmd, Kaffee, Cpp, cpt, Cpy, Cs, Cshtml, Cson, Csproj, Css, CTP-Version , cxx aufweisen, d, Ddl, di, Dif, Diff, Disco, Dml, Dtd, Dtml, el, Emakefile, Erb, Erl, f, f90, f95, fs, Fsi, Fsscript, Fsx, Gemfile, Gemspec, Gitconfig, wechseln Sie, einzigartige, Gvy, h, h-, Haml, Lenkern, HB, Hcp, Hh, Hpp, Hrl, hs, Htc, Hxx, Idl, Iim, inc, inf, Ini, Inl, Ipp , Irbrc, Jade, Jav, Java, Js, Jsp, Jsx, l, weniger Lhs, Lisp, melden Sie sich, Lst, Ltx, Lua, m, stellen, Markdn, Abzugsverteilung(en), Md, Mdown, Mkdn, ml, Mli, Mll, Mly, mm, weitere, Nfo, Opml, Osascript, auszuchecken, p, Pas, Patch, Php, php2, php3, php4, php5, Phtml, pl, Plist, pm, Pod, pp , profile, Eigenschaften, ps1, pt, hierhin, Pyw, R, Kielfall, Rb, Rbx, rc, re Infodatei, Reg, Rest, Resw, Resx, Rhtml, Rjs, Rprofile, Rpy, Rss, Rst, Rxml, s, Sass, Scala, Scm, Sconscript, Sconstruct, Skripts, Scss, sgml, sh Shtml, Sml, Sql, Sty, Tcl, tex, Text, mit, Tld, Tli, Aktivitätenvorlagenstatistik, Tpl, Txt, Vb, vi, Vim, Wsdl, Xhtml, Xml, Xoml, Xsd, Xsl, Xslt, Yaml, Yaws, Yml, Zip, zsh


