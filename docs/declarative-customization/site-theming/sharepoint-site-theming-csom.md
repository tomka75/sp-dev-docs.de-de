# <a name="sharepoint-site-theming-csom-development"></a><span data-ttu-id="9bc1a-101">SharePoint-Websitedesign: CSOM-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="9bc1a-101">SharePoint site theming: CSOM development</span></span>

<span data-ttu-id="9bc1a-102">Das clientseitige SharePoint-Objektmodell (Client-Side Object Model, CSOM) bietet Zugriff auf das SharePoint-Objektmodell von Code, der lokal oder auf einem anderen Server als SharePoint ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-102">The SharePoint client-side object model (CSOM) provides access to the SharePoint object model from code that is running locally or on a different server than SharePoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9bc1a-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="9bc1a-103">Prerequisites</span></span>
<span data-ttu-id="9bc1a-104">Machen Sie sich mit den folgenden Themen vertraut, bevor Sie mit den ersten Schritten beginnen:</span><span class="sxs-lookup"><span data-stu-id="9bc1a-104">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="9bc1a-105">Verwenden des Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="9bc1a-105">Using the Client Object Model</span></span>](https://msdn.microsoft.com/de-DE/library/ff798388.aspx)
- [<span data-ttu-id="9bc1a-106">Gängige Programmieraufgaben im verwalteten Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="9bc1a-106">Common Programming Tasks in the Managed Client Object Model</span></span>](https://msdn.microsoft.com/de-DE/library/ee537013.aspx)

<span data-ttu-id="9bc1a-107">Sie müssen auch auf das [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/)-NuGet-Paket (Version 16.1.6906.1200 oder höher) verweisen.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-107">You will also need to reference the [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) NuGet package (version 16.1.6906.1200 or later).</span></span>

## <a name="csom-code-example"></a><span data-ttu-id="9bc1a-108">CSOM-Codebeispiel</span><span class="sxs-lookup"><span data-stu-id="9bc1a-108">CSOM code example</span></span>

<span data-ttu-id="9bc1a-109">Das folgende Beispiel zeigt, wie Sie das Objekt __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ erstellen und die Methode __GetAllTenantThemes__ aufrufen, um eine Liste mit Designs zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-109">The following example shows how to create a __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ object and call the __GetAllTenantThemes__ method to return a list of themes.</span></span> 

> [!NOTE]
> * <span data-ttu-id="9bc1a-110">Die URL zum Erstellen des Kontextobjekts enthält das Suffix _-admin_, da **TenantAdministration**-Methoden mit der Adminwebsite funktionieren.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-110">The URL used to create the context object includes the _-admin_ suffix, because **TenantAdministration** methods work with the admin site.</span></span>
> * <span data-ttu-id="9bc1a-111">Erstellen Sie eine __Tenant__-Instanz mit dem [Tenant-Konstruktor](https://msdn.microsoft.com/de-DE/library/dn174852.aspx), und rufen Sie dann die Methoden für diese Instanz auf.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-111">Create a __Tenant__ instance with the [Tenant constructor](https://msdn.microsoft.com/de-DE/library/dn174852.aspx), and then call the methods on that instance.</span></span>
> * <span data-ttu-id="9bc1a-112">Die können den gleichen Ansatz zum Aufrufen anderer Methoden für die Designverwaltung verwenden.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-112">You can use the same approach to call other theme management methods.</span></span>

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

## <a name="theme-definition-example"></a><span data-ttu-id="9bc1a-113">Beispiel für Designdefinition</span><span class="sxs-lookup"><span data-stu-id="9bc1a-113">Theme definition example</span></span>

<span data-ttu-id="9bc1a-114">Bei Methoden, die ein Designargument akzeptieren, definiert der folgende Code eine __SPOTheme__-Klasse, die Sie zum Erstellen von benutzerdefinierten Designs verwenden können.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-114">For methods that take a theme argument, the following code defines an __SPOTheme__ class that you can use to create custom themes.</span></span>

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

## <a name="applying-a-theme"></a><span data-ttu-id="9bc1a-115">Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="9bc1a-115">Applying a theme</span></span>

<span data-ttu-id="9bc1a-116">Es ist aktuell keine unterstützte API zum programmgesteuerten Anwenden eines Designs auf eine spezielle Website vorhanden.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-116">There's currently no supported API to programmatically apply a theme to specific site.</span></span>

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a><span data-ttu-id="9bc1a-117">Methoden/Eigenschaften der Klasse „Microsoft.Online.SharePoint.TenantAdministration.Tenant“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-117">Methods/properties of the Microsoft.Online.SharePoint.TenantAdministration.Tenant class</span></span>

<span data-ttu-id="9bc1a-118">Verwenden Sie die folgenden Methoden, um die Gruppe der verfügbaren Designs für eine SharePoint-Mandantenverwaltungswebsite anzupassen.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-118">Use the following methods to customize the set of available themes for a SharePoint tenant administration site.</span></span> <span data-ttu-id="9bc1a-119">Sie können ein neues benutzerdefiniertes Design hinzufügen, ein vorhandenes Design aktualisieren oder ein Design löschen und ein bestimmtes Design oder alle Designs abrufen.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-119">You can add a new custom theme, update an existing theme, or delete a theme, and you can retrieve a specific theme or all themes.</span></span> <span data-ttu-id="9bc1a-120">Sie können auch die Standarddesigns ausblenden oder wiederherstellen, die SharePoint bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-120">You can also hide or restore the default themes that come with SharePoint.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="9bc1a-121">Öffentliche Methode „AddTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-121">AddTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-122">Fügen Sie dem Mandanten ein Design hinzu.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-122">Add a theme to the tenant.</span></span>

<span data-ttu-id="9bc1a-123">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-123">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-124">__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="9bc1a-124">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="9bc1a-125">__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="9bc1a-125">__Return type:__ ClientResult<bool></span></span>

### <a name="deletetenanttheme-public-method"></a><span data-ttu-id="9bc1a-126">Öffentliche Methode „DeleteTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-126">DeleteTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-127">Löschen Sie ein Design aus dem Mandanten.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-127">Delete a theme from the tenant.</span></span>

<span data-ttu-id="9bc1a-128">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-128">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-129">__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="9bc1a-129">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="9bc1a-130">__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="9bc1a-130">__Return type:__ void</span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="9bc1a-131">Öffentliche Methode „GetAllTenantThemes“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-131">GetAllTenantThemes public method</span></span>
<span data-ttu-id="9bc1a-132">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-132">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="9bc1a-133">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="9bc1a-133">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="9bc1a-134">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-134">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-135">__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="9bc1a-135">__Parameters:__ none</span></span><br/>
<span data-ttu-id="9bc1a-136">__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="9bc1a-136">__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="9bc1a-137">Öffentliche Methode „GetTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-137">GetTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-138">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-138">Retrieve a theme by name.</span></span>

<span data-ttu-id="9bc1a-139">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-139">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-140">__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="9bc1a-140">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="9bc1a-141">__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="9bc1a-141">__Return type:__ ThemeProperties</span></span>

### <a name="hidedefaultthemes-public-property"></a><span data-ttu-id="9bc1a-142">Öffentliche Eigenschaft „HideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-142">HideDefaultThemes public property</span></span>
<span data-ttu-id="9bc1a-143">Diese Eigenschaft gibt an, ob die Standarddesigns in der Benutzeroberfläche der Designauswahl  zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-143">This property indicates whether the default themes are available in the theme picker UI.</span></span> <span data-ttu-id="9bc1a-144">Die Standardeinstellung ist __false__ (Standarddesigns sind verfügbar). Sie möchten diese Eigenschaft nach dem Definieren benutzerdefinierter Designs evtl. auf __true__ festlegen, um nur bestimmte Designs zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-144">The default setting is __false__ (the default themes are available), but you might want to set this property to __true__ after you define custom themes, to allow only specific themes to be used.</span></span>

<span data-ttu-id="9bc1a-145">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-145">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-146">__Typ:__ Boolesch</span><span class="sxs-lookup"><span data-stu-id="9bc1a-146">__Type:__ Boolean</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="9bc1a-147">Öffentliche Methode „UpdateTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-147">UpdateTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-148">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-148">Update the settings for an existing theme.</span></span>

<span data-ttu-id="9bc1a-149">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-149">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-150">__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="9bc1a-150">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="9bc1a-151">__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="9bc1a-151">__Return type:__ ClientResult<bool></span></span>

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a><span data-ttu-id="9bc1a-152">Methoden der Klasse „Microsoft.Online.SharePoint.TenantManagement.Tenant“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-152">Methods of the Microsoft.Online.SharePoint.TenantManagement.Tenant class</span></span>

<span data-ttu-id="9bc1a-153">Dies sind alternative APIs zum Verwalten von Designs auf Mandantenebene.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-153">These are alternative APIs to manage your themes in tenant level.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="9bc1a-154">Öffentliche Methode „AddTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-154">AddTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-155">Fügen Sie dem Mandanten ein Design hinzu.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-155">Add a theme to the tenant.</span></span>

<span data-ttu-id="9bc1a-156">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-156">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-157">__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="9bc1a-157">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="9bc1a-158">__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="9bc1a-158">__Return type:__ ClientResult<bool></span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="9bc1a-159">Öffentliche Methode „GetAllTenantThemes“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-159">GetAllTenantThemes public method</span></span>
<span data-ttu-id="9bc1a-160">Rufen Sie alle Designs ab, die zurzeit im Mandanten verfügbar sind, einschließlich aller benutzerdefinierten Designs, die hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-160">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="9bc1a-161">Standarddesigns werden nur hinzugefügt, wenn die Eigenschaft __HideDefaultThemes__ __false__ ist (Standardwert).</span><span class="sxs-lookup"><span data-stu-id="9bc1a-161">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="9bc1a-162">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-162">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-163">__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="9bc1a-163">__Parameters:__ none</span></span><br/>
<span data-ttu-id="9bc1a-164">__Rückgabetyp:__ ClientObjectList<ThemeProperties></span><span class="sxs-lookup"><span data-stu-id="9bc1a-164">__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gethidedefaultthemes-public-method"></a><span data-ttu-id="9bc1a-165">Öffentliche Methode „GetHideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-165">GetHideDefaultThemes public method</span></span>
<span data-ttu-id="9bc1a-166">Prüfen Sie die aktuelle Einstellung zum Ausblenden von Standarddesigns in der Benutzeroberfläche der Designauswahl.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-166">Read the current setting for whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="9bc1a-167">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-167">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-168">__Parameter:__ none</span><span class="sxs-lookup"><span data-stu-id="9bc1a-168">__Parameters:__ none</span></span><br/>
<span data-ttu-id="9bc1a-169">__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="9bc1a-169">__Return type:__ ClientResult<bool></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="9bc1a-170">Öffentliche Methode „GetTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-170">GetTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-171">Rufen Sie ein Design anhand des Namens ab.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-171">Retrieve a theme by name.</span></span>

<span data-ttu-id="9bc1a-172">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-172">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-173">__Parameter:__ string name</span><span class="sxs-lookup"><span data-stu-id="9bc1a-173">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="9bc1a-174">__Rückgabetyp:__ ThemeProperties</span><span class="sxs-lookup"><span data-stu-id="9bc1a-174">__Return type:__ ThemeProperties</span></span>

### <a name="sethidedefaultthemes-public-method"></a><span data-ttu-id="9bc1a-175">Öffentliche Methode „SetHideDefaultThemes“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-175">SetHideDefaultThemes public method</span></span>
<span data-ttu-id="9bc1a-176">Geben Sie an, ob Standarddesigns in der Benutzeroberfläche der Designauswahl ausgeblendet werden.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-176">Specify whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="9bc1a-177">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-177">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-178">__Parameter:__ Boolean</span><span class="sxs-lookup"><span data-stu-id="9bc1a-178">__Parameters:__ Boolean</span></span><br/>
<span data-ttu-id="9bc1a-179">__Rückgabetyp:__ void</span><span class="sxs-lookup"><span data-stu-id="9bc1a-179">__Return type:__ void</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="9bc1a-180">Öffentliche Methode „UpdateTenantTheme“</span><span class="sxs-lookup"><span data-stu-id="9bc1a-180">UpdateTenantTheme public method</span></span>
<span data-ttu-id="9bc1a-181">Aktualisieren Sie die Einstellungen für ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="9bc1a-181">Update the settings for an existing theme.</span></span>

<span data-ttu-id="9bc1a-182">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="9bc1a-182">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="9bc1a-183">__Parameter:__ string name, string themeJson</span><span class="sxs-lookup"><span data-stu-id="9bc1a-183">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="9bc1a-184">__Rückgabetyp:__ ClientResult<bool></span><span class="sxs-lookup"><span data-stu-id="9bc1a-184">__Return type:__ ClientResult<bool></span></span>

## <a name="see-also"></a><span data-ttu-id="9bc1a-185">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9bc1a-185">See also</span></span>

* [<span data-ttu-id="9bc1a-186">Überblick über SharePoint-Websitedesign</span><span class="sxs-lookup"><span data-stu-id="9bc1a-186">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="9bc1a-187">SharePoint-Websitedesign: JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="9bc1a-187">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="9bc1a-188">SharePoint-Websitedesign: PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="9bc1a-188">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="9bc1a-189">SharePoint-Websitedesign: REST-API</span><span class="sxs-lookup"><span data-stu-id="9bc1a-189">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* [<span data-ttu-id="9bc1a-190">Verwenden des Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="9bc1a-190">Using the Client Object Model</span></span>](https://msdn.microsoft.com/de-DE/library/ff798388.aspx)
* [<span data-ttu-id="9bc1a-191">Gängige Programmieraufgaben im verwalteten Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="9bc1a-191">Common Programming Tasks in the Managed Client Object Model</span></span>](https://msdn.microsoft.com/de-DE/library/ee537013.aspx)
