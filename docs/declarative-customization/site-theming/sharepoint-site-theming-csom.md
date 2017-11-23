# <a name="sharepoint-site-theming-csom-development"></a><span data-ttu-id="4adca-101">SharePoint-Websitedesign: CSOM-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="4adca-101">SharePoint site theming: CSOM development</span></span>

<span data-ttu-id="4adca-102">Das clientseitige SharePoint-Objektmodell (Client-Side Object Model, CSOM) bietet Zugriff auf das SharePoint-Objektmodell von Code, der lokal oder auf einem anderen Server als SharePoint ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4adca-102">The SharePoint client-side object model (CSOM) provides access to the SharePoint object model from code that is running locally or on a different server than SharePoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4adca-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="4adca-103">Prerequisites</span></span>
<span data-ttu-id="4adca-104">Machen Sie sich mit Folgendem vertraut, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="4adca-104">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="4adca-105">
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/de-de/library/ff798388.aspx)</span><span class="sxs-lookup"><span data-stu-id="4adca-105">[Using the Client Object Model](https://msdn.microsoft.com/de-de/library/ff798388.aspx)</span></span>
- <span data-ttu-id="4adca-106">
  [Gängige Programmieraufgaben im verwalteten Clientobjektmodell](https://msdn.microsoft.com/de-de/library/ee537013.aspx)</span><span class="sxs-lookup"><span data-stu-id="4adca-106">[Common Programming Tasks in the Managed Client Object Model](https://msdn.microsoft.com/de-de/library/ee537013.aspx)</span></span>

<span data-ttu-id="4adca-107">Sie müssen auch das [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/)-NuGet-Paket (Version 16.1.6906.1200 oder höher) referenzieren.</span><span class="sxs-lookup"><span data-stu-id="4adca-107">You will also need to reference the [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) NuGet package (version 16.1.6906.1200 or later).</span></span>

## <a name="csom-code-example"></a><span data-ttu-id="4adca-108">CSOM-Codebeispiel</span><span class="sxs-lookup"><span data-stu-id="4adca-108">CSOM code example</span></span>

<span data-ttu-id="4adca-109">Das folgende Beispiel zeigt, wie Sie das Objekt __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ erstellen und die Methode __GetAllTenantThemes__ aufrufen, um eine Liste mit Designs zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="4adca-109">The following example shows how to create a __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ object and call the __GetAllTenantThemes__ method to return a list of themes.</span></span> 

><span data-ttu-id="4adca-110">**Hinweis:**</span><span class="sxs-lookup"><span data-stu-id="4adca-110">**Note**</span></span>
>* <span data-ttu-id="4adca-111">Die URL zum Erstellen des Kontextobjekts enthält das Suffix _-admin_, da **TenantAdministration**-Methoden mit der Adminwebsite funktionieren.</span><span class="sxs-lookup"><span data-stu-id="4adca-111">The URL used to create the context object includes the _-admin_ suffix, because **TenantAdministration** methods work with the admin site.</span></span>
>* <span data-ttu-id="4adca-112">Erstellen Sie eine __Tenant__-Instanz mit dem [Tenant-Konstruktor](https://msdn.microsoft.com/de-de/library/dn174852.aspx), und rufen Sie dann die Methoden für diese Instanz auf.</span><span class="sxs-lookup"><span data-stu-id="4adca-112">Create a __Tenant__ instance with the [Tenant constructor](https://msdn.microsoft.com/de-de/library/dn174852.aspx), and then call the methods on that instance.</span></span>
>* <span data-ttu-id="4adca-113">Sie können denselben Ansatz verwenden, um andere Designverwaltungsmethoden aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="4adca-113">You can use the same approach to call other theme management methods.</span></span>

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

## <a name="theme-definition-example"></a><span data-ttu-id="4adca-114">Beispiel für die Definition von Designs</span><span class="sxs-lookup"><span data-stu-id="4adca-114">Theme definition example</span></span>

<span data-ttu-id="4adca-115">Für Methoden, die ein Designargument verwenden können, definiert der folgende Code eine __SPOTheme__-Klasse zum Erstellen benutzerdefinierter Designs.</span><span class="sxs-lookup"><span data-stu-id="4adca-115">For methods that take a theme argument, the following code defines an __SPOTheme__ class that you can use to create custom themes.</span></span>

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

## <a name="applying-a-theme"></a><span data-ttu-id="4adca-116">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="4adca-116">Applying a theme</span></span>

<span data-ttu-id="4adca-117">Es ist aktuell keine unterstützte API zum programmgesteuerten Anwenden eines Designs auf eine spezielle Website vorhanden.</span><span class="sxs-lookup"><span data-stu-id="4adca-117">There's currently no supported API to programmatically apply a theme to specific site.</span></span>

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a><span data-ttu-id="4adca-118">Methoden/Eigenschaften der Klasse „Microsoft.Online.SharePoint.TenantAdministration.Tenant“</span><span class="sxs-lookup"><span data-stu-id="4adca-118">Methods/properties of the Microsoft.Online.SharePoint.TenantAdministration.Tenant class</span></span>

<span data-ttu-id="4adca-119">Verwenden Sie die folgenden Methoden, um die Gruppe der verfügbaren Designs für eine SharePoint-Mandantenverwaltungswebsite anzupassen.</span><span class="sxs-lookup"><span data-stu-id="4adca-119">Use the following methods to customize the set of available themes for a SharePoint tenant administration site.</span></span> <span data-ttu-id="4adca-120">Sie können ein neues benutzerdefiniertes Design hinzufügen, ein vorhandenes Design aktualisieren oder ein Design löschen und ein bestimmtes Design oder alle Designs abrufen.</span><span class="sxs-lookup"><span data-stu-id="4adca-120">You can add a new custom theme, update an existing theme, or delete a theme, and you can retrieve a specific theme or all themes.</span></span> <span data-ttu-id="4adca-121">Sie können auch die Standarddesigns ausblenden oder wiederherstellen, die SharePoint bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="4adca-121">You can also hide or restore the default themes that come with SharePoint.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="4adca-122">Öffentliche Methode „AddTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-122">AddTenantTheme public method</span></span>
<span data-ttu-id="4adca-123">Fügen Sie ein Design zum Mandanten hinzu.</span><span class="sxs-lookup"><span data-stu-id="4adca-123">Add a theme to the tenant.</span></span>

<span data-ttu-id="4adca-124">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-124">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-125">
__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="4adca-125">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="4adca-126">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="4adca-126">
__Return type:__ ClientResult<bool></span></span>

### <a name="deletetenanttheme-public-method"></a><span data-ttu-id="4adca-127">Öffentliche Methode „DeleteTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-127">DeleteTenantTheme public method</span></span>
<span data-ttu-id="4adca-128">Löschen Sie ein Design aus dem Mandanten.</span><span class="sxs-lookup"><span data-stu-id="4adca-128">Delete a theme from the tenant.</span></span>

<span data-ttu-id="4adca-129">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-129">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-130">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="4adca-130">
__Parameters:__ string name</span></span><br/><span data-ttu-id="4adca-131">
__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="4adca-131">
__Return type:__ void</span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="4adca-132">Öffentliche Methode „GetAllTenantThemes“</span><span class="sxs-lookup"><span data-stu-id="4adca-132">GetAllTenantThemes public method</span></span>
<span data-ttu-id="4adca-133">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="4adca-133">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="4adca-134">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="4adca-134">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="4adca-135">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-135">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-136">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="4adca-136">
__Parameters:__ none</span></span><br/><span data-ttu-id="4adca-137">
__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="4adca-137">
__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="4adca-138">Öffentliche Methode „GetTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-138">GetTenantTheme public method</span></span>
<span data-ttu-id="4adca-139">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="4adca-139">Retrieve a theme by name.</span></span>

<span data-ttu-id="4adca-140">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-140">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-141">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="4adca-141">
__Parameters:__ string name</span></span><br/><span data-ttu-id="4adca-142">
__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="4adca-142">
__Return type:__ ThemeProperties</span></span>

### <a name="hidedefaultthemes-public-property"></a><span data-ttu-id="4adca-143">Öffentliche Eigenschaft „HideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="4adca-143">HideDefaultThemes public property</span></span>
<span data-ttu-id="4adca-144">Diese Eigenschaft gibt an, ob die Standarddesigns in der Benutzeroberfläche der Designauswahl  zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="4adca-144">This property indicates whether the default themes are available in the theme picker UI.</span></span> <span data-ttu-id="4adca-145">Die Standardeinstellung ist __false__ (Standarddesigns sind verfügbar). Sie möchten diese Eigenschaft nach dem Definieren benutzerdefinierter Designs evtl. auf __true__ festlegen, um nur bestimmte Designs zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="4adca-145">The default setting is __false__ (the default themes are available), but you might want to set this property to __true__ after you define custom themes, to allow only specific themes to be used.</span></span>

<span data-ttu-id="4adca-146">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-146">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-147">
__Typ:__ Boolean</span><span class="sxs-lookup"><span data-stu-id="4adca-147">   Type:  boolean</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="4adca-148">Öffentliche Methode „UpdateTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-148">UpdateTenantTheme public method</span></span>
<span data-ttu-id="4adca-149">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="4adca-149">Update the settings for an existing theme.</span></span>

<span data-ttu-id="4adca-150">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-150">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/><span data-ttu-id="4adca-151">
__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="4adca-151">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="4adca-152">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="4adca-152">
__Return type:__ ClientResult<bool></span></span>

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a><span data-ttu-id="4adca-153">Methoden der Klasse „Microsoft.Online.SharePoint.TenantManagement.Tenant“</span><span class="sxs-lookup"><span data-stu-id="4adca-153">Methods of the Microsoft.Online.SharePoint.TenantManagement.Tenant class</span></span>

<span data-ttu-id="4adca-154">Dies sind alternative APIs, um Ihre Designs auf Mandantenebene zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="4adca-154">These are alternative APIs to manage your themes in tenant level.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="4adca-155">Öffentliche Methode „AddTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-155">AddTenantTheme public method</span></span>
<span data-ttu-id="4adca-156">Fügen Sie ein Design zum Mandanten hinzu.</span><span class="sxs-lookup"><span data-stu-id="4adca-156">Add a theme to the tenant.</span></span>

<span data-ttu-id="4adca-157">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-157">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-158">
__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="4adca-158">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="4adca-159">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="4adca-159">
__Return type:__ ClientResult<bool></span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="4adca-160">Öffentliche Methode „GetAllTenantThemes“</span><span class="sxs-lookup"><span data-stu-id="4adca-160">GetAllTenantThemes public method</span></span>
<span data-ttu-id="4adca-161">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="4adca-161">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="4adca-162">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="4adca-162">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="4adca-163">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-163">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-164">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="4adca-164">
__Parameters:__ none</span></span><br/><span data-ttu-id="4adca-165">
__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="4adca-165">
__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gethidedefaultthemes-public-method"></a><span data-ttu-id="4adca-166">Öffentliche Methode „GetHideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="4adca-166">GetHideDefaultThemes public method</span></span>
<span data-ttu-id="4adca-167">Prüfen Sie die aktuelle Einstellung zum Ausblenden von Standarddesigns in der Benutzeroberfläche der Designauswahl.</span><span class="sxs-lookup"><span data-stu-id="4adca-167">Read the current setting for whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="4adca-168">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-168">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-169">
__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="4adca-169">
__Parameters:__ none</span></span><br/><span data-ttu-id="4adca-170">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="4adca-170">
__Return type:__ ClientResult<bool></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="4adca-171">Öffentliche Methode „GetTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-171">GetTenantTheme public method</span></span>
<span data-ttu-id="4adca-172">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="4adca-172">Retrieve a theme by name.</span></span>

<span data-ttu-id="4adca-173">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-173">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-174">
__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="4adca-174">
__Parameters:__ string name</span></span><br/><span data-ttu-id="4adca-175">
__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="4adca-175">
__Return type:__ ThemeProperties</span></span>

### <a name="sethidedefaultthemes-public-method"></a><span data-ttu-id="4adca-176">Öffentliche Methode „SetHideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="4adca-176">SetHideDefaultThemes public method</span></span>
<span data-ttu-id="4adca-177">Geben Sie an, ob Standarddesigns in der Benutzeroberfläche der Designauswahl ausgeblendet werden.</span><span class="sxs-lookup"><span data-stu-id="4adca-177">Specify whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="4adca-178">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-178">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-179">
__Parameter:__ Boolean</span><span class="sxs-lookup"><span data-stu-id="4adca-179">
__Parameters:__ Boolean</span></span><br/><span data-ttu-id="4adca-180">
__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="4adca-180">
__Return type:__ void</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="4adca-181">Öffentliche Methode „UpdateTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="4adca-181">UpdateTenantTheme public method</span></span>
<span data-ttu-id="4adca-182">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="4adca-182">Update the settings for an existing theme.</span></span>

<span data-ttu-id="4adca-183">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="4adca-183">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/><span data-ttu-id="4adca-184">
__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="4adca-184">
__Parameters:__ string name, string themeJson</span></span><br/><span data-ttu-id="4adca-185">
__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="4adca-185">
__Return type:__ ClientResult<bool></span></span>

## <a name="see-also"></a><span data-ttu-id="4adca-186">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4adca-186">See also</span></span>

* [<span data-ttu-id="4adca-187">Überblick über SharePoint-Websitedesign</span><span class="sxs-lookup"><span data-stu-id="4adca-187">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="4adca-188">SharePoint-Websitedesign: JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="4adca-188">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="4adca-189">SharePoint-Websitedesign: PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="4adca-189">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="4adca-190">SharePoint-Websitedesign: REST-API</span><span class="sxs-lookup"><span data-stu-id="4adca-190">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* <span data-ttu-id="4adca-191">
  [Verwenden des Clientobjektmodells](https://msdn.microsoft.com/de-de/library/ff798388.aspx)</span><span class="sxs-lookup"><span data-stu-id="4adca-191">[Using the Client Object Model](https://msdn.microsoft.com/de-de/library/ff798388.aspx)</span></span>
* <span data-ttu-id="4adca-192">
  [Gängige Programmieraufgaben im verwalteten Clientobjektmodell](https://msdn.microsoft.com/de-de/library/ee537013.aspx)</span><span class="sxs-lookup"><span data-stu-id="4adca-192">[Common Programming Tasks in the Managed Client Object Model](https://msdn.microsoft.com/de-de/library/ee537013.aspx)</span></span>
