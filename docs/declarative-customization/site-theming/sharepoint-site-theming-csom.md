# <a name="sharepoint-site-theming-csom-development"></a>SharePoint-Websitedesigns: CSOM-Entwicklung

Das SharePoint-Clientobjektmodell (CSOM) ermöglicht den Zugriff auf das SharePoint-Objektmodell über Code, der lokal oder auf einem anderen Server als SharePoint ausgeführt wird. 

## <a name="prerequisites"></a>Voraussetzungen
Machen Sie sich mit den folgenden Themen vertraut, bevor Sie mit den ersten Schritten beginnen:
- 
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/en-us/library/ff798388.aspx)
- 
  [Allgemeine Programmieraufgaben des Objektmodells des verwalteten Clients](https://msdn.microsoft.com/en-us/library/ee537013.aspx)

Sie müssen auch auf das [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/)-NuGet-Paket (Version 16.1.6906.1200 oder höher) verweisen.

## <a name="csom-code-example"></a>CSOM-Codebeispiel

Das folgende Beispiel zeigt, wie Sie ein __Microsoft.Online.SharePoint.TenantAdministration.Tenant__-Objekt erstellen und die __GetAllTenantThemes__-Methode aufrufen, um eine Liste der Designs zurückzugeben. 

>**Hinweis:**
>* Die zum Erstellen des Kontextobjekts verwendete URL enthält den Suffix _-admin_, da die **TenantAdministration**-Methoden mit der Administratorwebsite verwendet werden.
>* Erstellen Sie eine __Tenant__-Instanz mit dem [Mandantenkonstruktor](https://msdn.microsoft.com/en-us/library/dn174852.aspx), und rufen Sie dann die Methoden auf dieser Instanz auf.
>* Die können den gleichen Ansatz zum Aufrufen anderer Methoden für die Designverwaltung verwenden.

```C#
using System.Security;
using Microsoft.SharePoint.Client;
using Microsoft.Online.SharePoint.TenantAdministration;
using Microsoft.Online.SharePoint.TenantManagement;

...

ClientContext ctx = new ClientContext("https://mysite-admin.sharepoint.com/");
var pwd = "mypassword";
var passWord = new SecureString();
foreach (char c in pwd.ToCharArray()) passWord.AppendChar(c);
ctx.Credentials = new SharePointOnlineCredentials("admin@mydomain.com", passWord);
Tenant tenant = new Tenant(ctx);
ClientObjectList<ThemeProperties> themes = tenant.GetAllTenantThemes();
```

## <a name="theme-definition-example"></a>Beispiel für Designdefinition

Bei Methoden, die ein Designargument akzeptieren, definiert der folgende Code eine __SPOTheme__-Klasse, die Sie zum Erstellen von benutzerdefinierten Designs verwenden können.

```C#
/// <summary> 
/// Properties defining a theme in SharePoint Online. 
/// </summary> 
public class SPOTheme 
{ 
    /// <summary> 
    /// Specifies the name of the theme. This must uniquely identify the theme. 
    /// </summary> 
    public string Name 
    { 
        get; private set; 
    } 
    /// <summary> 
    /// Specifies the palette of colors in the theme, as a dictionary of theme slot values. 
    /// </summary> 
    public IDictionary<String, String> Palette 
    { 
        get; private set; 
    } 
    /// <summary> 
    /// Specifies whether the theme is inverted, with a dark background and a light foreground. 
    /// </summary> 
    public bool IsInverted 
    { 
        get; private set; 
    } 
} 
```

## <a name="applying-a-theme"></a>Anwenden eines Designs

Es ist aktuell keine unterstützte API zum programmatischen Anwenden eines Designs auf eine spezielle Website vorhanden.

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a>Methoden/Eigenschaften der Klasse Microsoft.Online.SharePoint.TenantAdministration.Tenant

Verwenden Sie die folgenden Methoden, um die Gruppe der verfügbaren Designs für eine SharePoint-Mandantenverwaltungswebsite anzupassen. Sie können ein neues benutzerdefiniertes Design hinzufügen, ein vorhandenes Design aktualisieren oder ein Design löschen und ein bestimmtes Design oder alle Designs abrufen. Sie können auch die Standarddesigns ausblenden oder wiederherstellen, die SharePoint bereitstellt.

### <a name="addtenanttheme-public-method"></a>Öffentliche Methode AddTenantTheme
Fügen Sie dem Mandanten ein Design hinzu.

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Parameters:__ string name, string themeJson<br/>
__Rückgabetyp:__ ClientResult<bool>

### <a name="deletetenanttheme-public-method"></a>Öffentliche Methode DeleteTenantTheme
Löschen Sie ein Design aus dem Mandanten.

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Parameter:__ string name<br/>
__Rückgabetyp:__ void

### <a name="getalltenantthemes-public-method"></a>Öffentliche Methode GetAllTenantThemes
Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden. Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Parameter:__ none<br/>
__Rückgabetyp:__ ClientObjectList<ThemeProperties>

### <a name="gettenanttheme-public-method"></a>Öffentliche Methode GetTenantTheme
Rufen Sie ein Design anhand des Namens ab.

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Parameter:__ string name<br/>
__Rückgabetyp:__ ThemeProperties

### <a name="hidedefaultthemes-public-property"></a>Öffentliche Eigenschaft HideDefaultThemes
Diese Eigenschaft gibt an, ob die Standarddesigns in der Benutzeroberfläche mit der Designauswahl  zur Verfügung stehen. Die Standardeinstellung ist __false__ (Standarddesigns sind verfügbar). Sie möchten diese Eigenschaft nach dem Definieren benutzerdefinierter Designs evtl. auf __true festlegen__, um nur bestimmte Designs zuzulassen.

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Typ:__ Boolesch

### <a name="updatetenanttheme-public-method"></a>Öffentliche Methode UpdateTenantTheme
Aktualisieren Sie die Einstellungen für ein vorhandenes Design.

__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant<br/>
__Parameters:__ string name, string themeJson<br/>
__Rückgabetyp:__ ClientResult<bool>

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a>Methoden der Microsoft.Online.SharePoint.TenantManagement.Tenant-Klasse

Dies sind alternative APIs zum Verwalten von Designs auf Mandantenebene.

### <a name="addtenanttheme-public-method"></a>Öffentliche Methode AddTenantTheme
Fügen Sie dem Mandanten ein Design hinzu.

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameters:__ string name, string themeJson<br/>
__Rückgabetyp:__ ClientResult<bool>

### <a name="getalltenantthemes-public-method"></a>Öffentliche Methode GetAllTenantThemes
Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden. Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameter:__ none<br/>
__Rückgabetyp:__ ClientObjectList<ThemeProperties>

### <a name="gethidedefaultthemes-public-method"></a>Öffentliche Methode GetHideDefaultThemes
Rufen Sie die aktuelle Einstellung für das Ausblenden von Standarddesigns in der Designauswahl-Benutzeroberfläche ab.

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameter:__ none<br/>
__Rückgabetyp:__ ClientResult<bool>

### <a name="gettenanttheme-public-method"></a>Öffentliche Methode GetTenantTheme
Rufen Sie ein Design anhand des Namens ab.

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameter:__ string name<br/>
__Rückgabetyp:__ ThemeProperties

### <a name="sethidedefaultthemes-public-method"></a>Öffentliche Methode SetHideDefaultThemes
Geben Sie an, ob Standarddesigns in der Designauswahl-Benutzeroberfläche ausgeblendet werden sollen.

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameter:__ Boolean<br/>
__Rückgabetyp:__ void

### <a name="updatetenanttheme-public-method"></a>Öffentliche Methode UpdateTenantTheme
Aktualisieren Sie die Einstellungen für ein vorhandenes Design.

__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant<br/>
__Parameters:__ string name, string themeJson<br/>
__Rückgabetyp:__ ClientResult<bool>

## <a name="see-also"></a>Siehe auch

* [Überblick über SharePoint-Websitedesigns](sharepoint-site-theming-overview.md)
* [SharePoint-Websitedesigns: JSON-Schema](sharepoint-site-theming-json-schema.md)
* [SharePoint-Websitedesigns: PowerShell-Cmdlets](sharepoint-site-theming-powershell.md)
* [SharePoint-Websitedesigns: REST-API](sharepoint-site-theming-rest-api.md)
* 
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/en-us/library/ff798388.aspx)
* 
  [Allgemeine Programmieraufgaben des Objektmodells des verwalteten Clients](https://msdn.microsoft.com/en-us/library/ee537013.aspx)
