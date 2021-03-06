# <a name="sharepoint-site-theming-powershell-cmdlets"></a>SharePoint-Websitedesign: PowerShell-Cmdlets

Mithilfe von PowerShell-Cmdlets können SharePoint-Mandantenadministratoren Websitedesigns erstellen, abrufen und entfernen. Entwickler können zur Verwaltung von Designs außerdem die [REST-API](sharepoint-site-theming-rest-api.md) verwenden.

Informationen zur Definition und Speicherung von Designs finden Sie in der [JSON-Schemareferenz](sharepoint-site-theming-json-schema.md).

## <a name="getting-started"></a>Erste Schritte

Bevor Sie die PowerShell-Cmdlets zur Verwaltung von Designs nutzen können, müssen Sie Folgendes tun:

1. Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren. Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.
2. Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx).

Überprüfen Sie nun Ihr Setup. Rufen Sie dazu mithilfe des Cmdlets **Get-HideDefaultThemes** den Wert für die Einstellung „HideDefaultThemes“ ab. Wenn das Cmdlet fehlerfrei ausgeführt wird und den Wert „False“ zurückgibt (siehe Beispiel unten), können Sie fortfahren.

```powershell
c:\> Get-HideDefaultThemes
False
```
## <a name="site-theme-cmdlets"></a>Cmdlets für das Websitedesign

Zur Verwaltung von Websitedesigns über die PowerShell stehen Ihnen die folgenden Cmdlets zur Verfügung:

* **Add-SPOTheme** &mdash; Erstellt ein neues benutzerdefiniertes Design oder überschreibt ein vorhandenes Design mit neuen Einstellungen.
* **Get-SPOTheme** &mdash; Ruft die Einstellungen eines vorhandenen Designs ab.
* **Remove-SPOTheme** &mdash; Entfernt ein Design aus dem Designkatalog.
* **Set-HideDefaultThemes** &mdash; Legt fest, ob die Standarddesigns verfügbar sein sollen.
* **Get-HideDefaultThemes** &mdash; Fragt den aktuellen Wert der Einstellung „HideDefaultThemes“ ab.

## <a name="add-spotheme"></a>Add-SPOTheme

Das Cmdlet **Add-SPOTheme** erstellt ein neues Design oder aktualisiert ein vorhandenes Design. Dabei werden die Farbpaletteneinstellungen als Schlüsselverzeichnis übergeben.

Im folgenden Beispiel wird ein neues Design namens „Custom Cyan“ erstellt, mit Farbpaletteneinstellungen, die verschiedene Zyanschattierungen definieren. Wie Sie sehen, nutzen wir in diesem Beispiel eine Funktion des Typs ```HashToDictionary```, um eine mit der Notation ```@{}``` erstellte Hashtabelle in ein Schlüsselverzeichnis zu konvertieren, wie es für das Cmdlet **Add-SPOTheme** erforderlich ist.

```powershell
function HashToDictionary {
  Param ([Hashtable]$ht)
  $dictionary = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
  foreach ($entry in $ht.GetEnumerator()) {
    $dictionary.Add($entry.Name, $entry.Value)
  }
  return $dictionary
}

$themepallette = HashToDictionary(
 @{
  "themePrimary" = "#00ffff";
  "themeLighterAlt" = "#f3fcfc";
  "themeLighter" = "#daffff";
  "themeLight" = "#affefe";
  "themeTertiary" = "#76ffff";
  "themeSecondary" = "#39ffff";
  "themeDarkAlt" = "#00c4c4";
  "themeDark" = "#009090";
  "themeDarker" = "#005252";
  "neutralLighterAlt" = "#f8f8f8";
  "neutralLighter" = "#f4f4f4";
  "neutralLight" = "#eaeaea";
  "neutralQuaternaryAlt" = "#dadada";
  "neutralQuaternary" = "#d0d0d0";
  "neutralTertiaryAlt" = "#c8c8c8";
  "neutralTertiary" = "#a6a6a6";
  "neutralSecondaryAlt" = "#767676";
  "neutralSecondary" = "#666666";
  "neutralPrimary" = "#333";
  "neutralPrimaryAlt" = "#3c3c3c";
  "neutralDark" = "#212121";
  "black" = "#000000";
  "white" = "#fff";
  "primaryBackground" = "#fff";
  "primaryText" = "#333"
 }
)

Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false
```
Wenn Sie ein vorhandenes Design aktualisieren möchten (beispielsweise mit neuen Farbeinstellungen), verwenden Sie dieselbe Syntax wie im vorherigen Beispiel, fügen jedoch das Flag *-Overwrite* zum Cmdlet **Add-SPOTheme** hinzu.

```powershell
Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false -Overwrite
```
Wenn Sie ein Design hinzufügen, wird es noch nicht auf Websites angewendet. Das Design wird lediglich zum Store Ihres Mandanten hinzugefügt und steht dann auf modernen Seiten in der Designliste unter **Change the look** zur Verfügung.

## <a name="get-spotheme"></a>Get-SPOTheme

Das Cmdlet **Get-SPOTheme** gibt die Einstellungen eines vorhandenen Designs zurück. Mit dem folgenden Code beispielsweise können Sie über das Cmdlet **Get-SPOTheme** die Einstellungen des Designs „Custom Cyan“ abrufen, das Sie im vorherigen Beispiel erstellt haben.

```powershell
C:\> Get-SPOTheme -Name "Custom Cyan" | ConvertTo-Json
```
```json
{
    "Name":  "Custom Cyan",
    "Palette":  {
                    "themeLight":  "#affefe",
                    "themeTertiary":  "#76ffff",
                    "black":  "#000000",
                    "neutralSecondary":  "#666666",
                    "neutralTertiaryAlt":  "#c8c8c8",
                    "themeSecondary":  "#39ffff",
                    "themeDarker":  "#005252",
                    "primaryBackground":  "#fff",
                    "neutralQuaternary":  "#d0d0d0",
                    "neutralPrimaryAlt":  "#3c3c3c",
                    "neutralPrimary":  "#333",
                    "themeDark":  "#009090",
                    "themeLighter":  "#daffff",
                    "neutralTertiary":  "#a6a6a6",
                    "neutralQuaternaryAlt":  "#dadada",
                    "themeLighterAlt":  "#f3fcfc",
                    "white":  "#fff",
                    "neutralSecondaryAlt":  "#767676",
                    "neutralLighter":  "#f4f4f4",
                    "neutralLight":  "#eaeaea",
                    "neutralDark":  "#212121",
                    "themeDarkAlt":  "#00c4c4",
                    "neutralLighterAlt":  "#f8f8f8",
                    "primaryText":  "#333",
                    "themePrimary":  "#00ffff"
                },
    "IsInverted":  false
}
```
Wie Sie sehen, verwenden wir in diesem Beispiel den PowerShell-Filter _ConvertTo-Json_, um das Design im JSON-Format abzurufen.

## <a name="remove-spotheme"></a>Remove-SPOTheme

Das Cmdlet **Remove-SPOTheme** entfernt ein Design aus dem Store Ihres Mandanten. Das Cmdlet unten beispielsweise entfernt das Design „Custom Cyan“, das wir in den vorherigen Beispielen verwendet haben.

```powershell
c:\> Remove-SPOTheme -Name "Custom Cyan"
```
## <a name="set-hidedefaultthemes"></a>Set-HideDefaultThemes

_Hinweis: Dieses Cmdlet wird in einer zukünftigen Version in ```Set-SPOHideDefaultThemes``` umbenannt, zwecks Konsistenz mit anderen SharePoint-PowerShell-Cmdlets._

Das Cmdlet **Set-HideDefaultThemes** gibt an, ob die in SharePoint integrierten Standarddesigns in der Liste aufgeführt werden sollen, die Ihnen in der Designauswahl zur Verfügung steht. Beispiel: Sie möchten benutzerdefinierte Designs für Ihre Websites erstellen und anschließend die Standarddesigns entfernen, damit auf alle Seiten Ihre benutzerdefinierten Designs angewendet werden.

Wenn Sie die Einstellung auf _$true_ setzen, werden die Standarddesigns ausgeblendet, wenn Sie sie auf _$false_ setzen (Standardeinstellung) werden sie angezeigt. Das Cmdlet unten blendet die Standarddesigns aus:

```powershell
Set-HideDefaultThemes $true
```
Wenn Sie das Design „Custom Cyan“ erstellen und anschließend die Standarddesigns ausblenden, wird in der Designliste unter **Change the look** nur noch dieses eine benutzerdefinierte Design angezeigt.

![Feld „Change the look“ mit dem Design „Custom Cyan“ und ausgeblendeten Standarddesigns](../../images/theme-hidedefaults.png)

Sollen die Standarddesigns wieder in der Designauswahl angezeigt werden, können Sie das folgende Cmdlet verwenden.
```powershell
Set-HideDefaultThemes $false
```

## <a name="get-hidedefaultthemes"></a>Get-HideDefaultThemes

_Hinweis: Dieses Cmdlet wird in einer zukünftigen Version in ```Get-SPOHideDefaultThemes``` umbenannt, zwecks Konsistenz mit anderen SharePoint-PowerShell-Cmdlets._

Das Cmdlet **Get-HideDefaultThemes** ruft den aktuellen Wert für die Einstellung **Set-HideDefaultThemes** ab. Sie können dieses Cmdlet in ein PowerShell-Skript aufnehmen, um diese Einstellung auszulesen und eine bestimmte Aktion einzuleiten, je nachdem, ob die Standarddesigns angezeigt werden oder nicht. Dieses Cmdlet hat keine Parameter.

```powershell
c:\> Get-HideDefaultThemes
False
```

## <a name="see-also"></a>Weitere Artikel

* [Überblick über das SharePoint-Websitedesign](sharepoint-site-theming-overview.md)
* [SharePoint-Websitedesign: JSON-Schema](sharepoint-site-theming-json-schema.md)
* [SharePoint-Websitedesign: CSOM](sharepoint-site-theming-csom.md)
* [SharePoint-Websitedesign: REST-API](sharepoint-site-theming-rest-api.md)
* [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)
* [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx)
