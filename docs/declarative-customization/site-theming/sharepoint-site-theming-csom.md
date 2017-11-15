# <a name="sharepoint-site-theming-csom-development"></a><span data-ttu-id="0d513-101">SharePoint-Websitedesigns: CSOM-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="0d513-101">SharePoint site theming: CSOM development</span></span>

<span data-ttu-id="0d513-102">Das SharePoint-Clientobjektmodell (CSOM) ermöglicht den Zugriff auf das SharePoint-Objektmodell über Code, der lokal oder auf einem anderen Server als SharePoint ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0d513-102">The SharePoint client-side object model (CSOM) provides access to the SharePoint object model from code that is running locally or on a different server than SharePoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0d513-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="0d513-103">Prerequisites</span></span>
<span data-ttu-id="0d513-104">Machen Sie sich mit den folgenden Themen vertraut, bevor Sie mit den ersten Schritten beginnen:</span><span class="sxs-lookup"><span data-stu-id="0d513-104">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="0d513-105">
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/en-us/library/ff798388.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d513-105">[Using the Client Object Model](https://msdn.microsoft.com/en-us/library/ff798388.aspx)</span></span>
- <span data-ttu-id="0d513-106">
  [Allgemeine Programmieraufgaben des Objektmodells des verwalteten Clients](https://msdn.microsoft.com/en-us/library/ee537013.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d513-106">[Common Programming Tasks in the Managed Client Object Model](https://msdn.microsoft.com/en-us/library/ee537013.aspx)</span></span>

<span data-ttu-id="0d513-107">Sie müssen auch auf das [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/)-NuGet-Paket (Version 16.1.6906.1200 oder höher) verweisen.</span><span class="sxs-lookup"><span data-stu-id="0d513-107">You will also need to reference the [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) NuGet package (version 16.1.6906.1200 or later).</span></span>

## <a name="csom-code-example"></a><span data-ttu-id="0d513-108">CSOM-Codebeispiel</span><span class="sxs-lookup"><span data-stu-id="0d513-108">CSOM code example</span></span>

<span data-ttu-id="0d513-109">Das folgende Beispiel zeigt, wie Sie ein __Microsoft.Online.SharePoint.TenantAdministration.Tenant__-Objekt erstellen und die __GetAllTenantThemes__-Methode aufrufen, um eine Liste der Designs zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="0d513-109">The following example shows how to create a __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ object and call the __GetAllTenantThemes__ method to return a list of themes.</span></span> 

><span data-ttu-id="0d513-110">**Hinweis:**</span><span class="sxs-lookup"><span data-stu-id="0d513-110">**Note**</span></span>
>* <span data-ttu-id="0d513-111">Die zum Erstellen des Kontextobjekts verwendete URL enthält den Suffix _-admin_, da die **TenantAdministration**-Methoden mit der Administratorwebsite verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0d513-111">The URL used to create the context object includes the _-admin_ suffix, because **TenantAdministration** methods work with the admin site.</span></span>
>* <span data-ttu-id="0d513-112">Erstellen Sie eine __Tenant__-Instanz mit dem [Mandantenkonstruktor](https://msdn.microsoft.com/en-us/library/dn174852.aspx), und rufen Sie dann die Methoden auf dieser Instanz auf.</span><span class="sxs-lookup"><span data-stu-id="0d513-112">Create a __Tenant__ instance with the [Tenant constructor](https://msdn.microsoft.com/en-us/library/dn174852.aspx), and then call the methods on that instance.</span></span>
>* <span data-ttu-id="0d513-113">Die können den gleichen Ansatz zum Aufrufen anderer Methoden für die Designverwaltung verwenden.</span><span class="sxs-lookup"><span data-stu-id="0d513-113">You can use the same approach to call other theme management methods.</span></span>

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

## <a name="theme-definition-example"></a><span data-ttu-id="0d513-114">Beispiel für Designdefinition</span><span class="sxs-lookup"><span data-stu-id="0d513-114">Theme definition example</span></span>

<span data-ttu-id="0d513-115">Bei Methoden, die ein Designargument akzeptieren, definiert der folgende Code eine __SPOTheme__-Klasse, die Sie zum Erstellen von benutzerdefinierten Designs verwenden können.</span><span class="sxs-lookup"><span data-stu-id="0d513-115">For methods that take a theme argument, the following code defines an __SPOTheme__ class that you can use to create custom themes.</span></span>

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

## <a name="applying-a-theme"></a><span data-ttu-id="0d513-116">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="0d513-116">Applying a theme</span></span>

<span data-ttu-id="0d513-117">Es ist aktuell keine unterstützte API zum programmatischen Anwenden eines Designs auf eine spezielle Website vorhanden.</span><span class="sxs-lookup"><span data-stu-id="0d513-117">There's currently no supported API to programmatically apply a theme to specific site.</span></span>

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a><span data-ttu-id="0d513-118">Methoden/Eigenschaften der Klasse Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-118">Methods/properties of the Microsoft.Online.SharePoint.TenantAdministration.Tenant class</span></span>

<span data-ttu-id="0d513-119">Verwenden Sie die folgenden Methoden, um die Gruppe der verfügbaren Designs für eine SharePoint-Mandantenverwaltungswebsite anzupassen.</span><span class="sxs-lookup"><span data-stu-id="0d513-119">Use the following methods to customize the set of available themes for a SharePoint tenant administration site.</span></span> <span data-ttu-id="0d513-120">Sie können ein neues benutzerdefiniertes Design hinzufügen, ein vorhandenes Design aktualisieren oder ein Design löschen und ein bestimmtes Design oder alle Designs abrufen.</span><span class="sxs-lookup"><span data-stu-id="0d513-120">You can add a new custom theme, update an existing theme, or delete a theme, and you can retrieve a specific theme or all themes.</span></span> <span data-ttu-id="0d513-121">Sie können auch die Standarddesigns ausblenden oder wiederherstellen, die SharePoint bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="0d513-121">You can also hide or restore the default themes that come with SharePoint.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="0d513-122">Öffentliche Methode AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-122">AddTenantTheme public method</span></span>
<span data-ttu-id="0d513-123">Fügen Sie dem Mandanten ein Design hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d513-123">Add a theme to the tenant.</span></span>

<span data-ttu-id="0d513-124">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-124">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-125">
__Parameters:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="0d513-125">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="0d513-126">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="0d513-126">
__Return type:__ ClientResult<bool></span></span>

### <a name="deletetenanttheme-public-method"></a><span data-ttu-id="0d513-127">Öffentliche Methode DeleteTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-127">DeleteTenantTheme public method</span></span>
<span data-ttu-id="0d513-128">Löschen Sie ein Design aus dem Mandanten.</span><span class="sxs-lookup"><span data-stu-id="0d513-128">Delete a theme from the tenant.</span></span>

<span data-ttu-id="0d513-129">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-129">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-130">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="0d513-130">
__Parameters:__ string name</span></span><br/><span data-ttu-id="0d513-131">
__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="0d513-131">
__Return type:__ void</span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="0d513-132">Öffentliche Methode GetAllTenantThemes</span><span class="sxs-lookup"><span data-stu-id="0d513-132">GetAllTenantThemes public method</span></span>
<span data-ttu-id="0d513-133">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="0d513-133">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="0d513-134">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="0d513-134">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="0d513-135">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-135">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-136">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="0d513-136">
__Parameters:__ none</span></span><br/><span data-ttu-id="0d513-137">
__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="0d513-137">
__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="0d513-138">Öffentliche Methode GetTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-138">GetTenantTheme public method</span></span>
<span data-ttu-id="0d513-139">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="0d513-139">Retrieve a theme by name.</span></span>

<span data-ttu-id="0d513-140">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-140">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-141">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="0d513-141">
__Parameters:__ string name</span></span><br/><span data-ttu-id="0d513-142">
__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="0d513-142">
__Return type:__ ThemeProperties</span></span>

### <a name="hidedefaultthemes-public-property"></a><span data-ttu-id="0d513-143">Öffentliche Eigenschaft HideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="0d513-143">HideDefaultThemes public property</span></span>
<span data-ttu-id="0d513-144">Diese Eigenschaft gibt an, ob die Standarddesigns in der Benutzeroberfläche mit der Designauswahl  zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="0d513-144">This property indicates whether the default themes are available in the theme picker UI.</span></span> <span data-ttu-id="0d513-145">Die Standardeinstellung ist __false__ (Standarddesigns sind verfügbar). Sie möchten diese Eigenschaft nach dem Definieren benutzerdefinierter Designs evtl. auf __true festlegen__, um nur bestimmte Designs zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="0d513-145">The default setting is __false__ (the default themes are available), but you might want to set this property to __true__ after you define custom themes, to allow only specific themes to be used.</span></span>

<span data-ttu-id="0d513-146">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-146">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-147">
__Typ:__ Boolesch</span><span class="sxs-lookup"><span data-stu-id="0d513-147">   Type:  boolean</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="0d513-148">Öffentliche Methode UpdateTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-148">UpdateTenantTheme public method</span></span>
<span data-ttu-id="0d513-149">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="0d513-149">Update the settings for an existing theme.</span></span>

<span data-ttu-id="0d513-150">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-150">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="0d513-151">
__Parameters:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="0d513-151">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="0d513-152">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="0d513-152">
__Return type:__ ClientResult<bool></span></span>

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a><span data-ttu-id="0d513-153">Methoden der Microsoft.Online.SharePoint.TenantManagement.Tenant-Klasse</span><span class="sxs-lookup"><span data-stu-id="0d513-153">Methods of the Microsoft.Online.SharePoint.TenantManagement.Tenant class</span></span>

<span data-ttu-id="0d513-154">Dies sind alternative APIs zum Verwalten von Designs auf Mandantenebene.</span><span class="sxs-lookup"><span data-stu-id="0d513-154">These are alternative APIs to manage your themes in tenant level.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="0d513-155">Öffentliche Methode AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-155">AddTenantTheme public method</span></span>
<span data-ttu-id="0d513-156">Fügen Sie dem Mandanten ein Design hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d513-156">Add a theme to the tenant.</span></span>

<span data-ttu-id="0d513-157">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-157">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-158">
__Parameters:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="0d513-158">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="0d513-159">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="0d513-159">
__Return type:__ ClientResult<bool></span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="0d513-160">Öffentliche Methode GetAllTenantThemes</span><span class="sxs-lookup"><span data-stu-id="0d513-160">GetAllTenantThemes public method</span></span>
<span data-ttu-id="0d513-161">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="0d513-161">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="0d513-162">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="0d513-162">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="0d513-163">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-163">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-164">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="0d513-164">
__Parameters:__ none</span></span><br/><span data-ttu-id="0d513-165">
__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="0d513-165">
__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gethidedefaultthemes-public-method"></a><span data-ttu-id="0d513-166">Öffentliche Methode GetHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="0d513-166">GetHideDefaultThemes public method</span></span>
<span data-ttu-id="0d513-167">Rufen Sie die aktuelle Einstellung für das Ausblenden von Standarddesigns in der Designauswahl-Benutzeroberfläche ab.</span><span class="sxs-lookup"><span data-stu-id="0d513-167">Read the current setting for whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="0d513-168">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-168">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-169">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="0d513-169">
__Parameters:__ none</span></span><br/><span data-ttu-id="0d513-170">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="0d513-170">
__Return type:__ ClientResult<bool></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="0d513-171">Öffentliche Methode GetTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-171">GetTenantTheme public method</span></span>
<span data-ttu-id="0d513-172">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="0d513-172">Retrieve a theme by name.</span></span>

<span data-ttu-id="0d513-173">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-173">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-174">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="0d513-174">
__Parameters:__ string name</span></span><br/><span data-ttu-id="0d513-175">
__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="0d513-175">
__Return type:__ ThemeProperties</span></span>

### <a name="sethidedefaultthemes-public-method"></a><span data-ttu-id="0d513-176">Öffentliche Methode SetHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="0d513-176">SetHideDefaultThemes public method</span></span>
<span data-ttu-id="0d513-177">Geben Sie an, ob Standarddesigns in der Designauswahl-Benutzeroberfläche ausgeblendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="0d513-177">Specify whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="0d513-178">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-178">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-179">
__Parameter:__ Boolean</span><span class="sxs-lookup"><span data-stu-id="0d513-179">
__Parameters:__ Boolean</span></span><br/><span data-ttu-id="0d513-180">
__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="0d513-180">
__Return type:__ void</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="0d513-181">Öffentliche Methode UpdateTenantTheme</span><span class="sxs-lookup"><span data-stu-id="0d513-181">UpdateTenantTheme public method</span></span>
<span data-ttu-id="0d513-182">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="0d513-182">Update the settings for an existing theme.</span></span>

<span data-ttu-id="0d513-183">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="0d513-183">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="0d513-184">
__Parameters:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="0d513-184">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="0d513-185">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="0d513-185">
__Return type:__ ClientResult<bool></span></span>

## <a name="see-also"></a><span data-ttu-id="0d513-186">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="0d513-186">See also</span></span>

* [<span data-ttu-id="0d513-187">Überblick über SharePoint-Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="0d513-187">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="0d513-188">SharePoint-Websitedesigns: JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="0d513-188">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="0d513-189">SharePoint-Websitedesigns: PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="0d513-189">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="0d513-190">SharePoint-Websitedesigns: REST-API</span><span class="sxs-lookup"><span data-stu-id="0d513-190">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* <span data-ttu-id="0d513-191">
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/en-us/library/ff798388.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d513-191">[Using the Client Object Model](https://msdn.microsoft.com/en-us/library/ff798388.aspx)</span></span>
* <span data-ttu-id="0d513-192">
  [Allgemeine Programmieraufgaben des Objektmodells des verwalteten Clients](https://msdn.microsoft.com/en-us/library/ee537013.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d513-192">[Common Programming Tasks in the Managed Client Object Model](https://msdn.microsoft.com/en-us/library/ee537013.aspx)</span></span>
