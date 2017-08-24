
# <a name="register-sharepoint-add-ins-2013"></a><span data-ttu-id="8af68-101">Registrieren von SharePoint 2013-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8af68-101">Register SharePoint Add-ins 2013</span></span>
<span data-ttu-id="8af68-102">Registrieren Sie Ihre SharePoint-Add-Ins in Azure ACS mithilfe von Visual Studio, dem Verkäuferdashboard oder einer AppRegNew.aspx-Seite, und rufen Sie Registrierungsinformationen ab.</span><span class="sxs-lookup"><span data-stu-id="8af68-102">Register your SharePoint Add-ins in Azure ACS by using Visual Studio, the Seller Dashboard, or an AppRegNew.aspx page, and retrieve registration information.</span></span>
 

 <span data-ttu-id="8af68-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="8af68-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="8af68-p102">Damit die Remotekomponenten eines vom Anbieter gehosteten SharePoint-Add-Ins mit SharePoint über OAuth interagieren können, muss das Add-In zunächst beim cloudbasierten Dienst [Azure ACS](https://msdn.microsoft.com/en-us/library/azure/gg429788.aspx) sowie beim SharePoint App-Verwaltungsdienst der Mandantschaft oder der Farm registriert werden (Er wird als „App-Verwaltungsdienst“ bezeichnet, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ hießen).</span><span class="sxs-lookup"><span data-stu-id="8af68-p102">Register your SharePoint Add-ins in Azure ACS by using Visual Studio, the Seller Dashboard, or an AppRegNew.aspx page, and retrieve registration information. For the remote components of a provider-hosted SharePoint Add-in to interact with SharePoint using OAuth, the add-in must first register with the  [Azure ACS](https://msdn.microsoft.com/en-us/library/azure/gg429788.aspx) cloud-based service and the SharePoint App Management Service of the tenancy or farm. (It is called "App Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".)</span></span>
 

 <span data-ttu-id="8af68-108">**Hinweis** Dies ist für von SharePoint gehostete Add-Ins nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="8af68-108">**Note** This is not required for SharePoint-hosted add-ins.</span></span>
 

<span data-ttu-id="8af68-109">Um das Add-In bei Azure ACS zu registrieren, geben Sie die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="8af68-109">To register your add-in with Azure ACS, you specify the following information:</span></span>
 

- <span data-ttu-id="8af68-110">Eine GUID für das Add-In, die als Client-ID bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="8af68-110">A GUID for the add-in, called a client ID.</span></span>
    
 
- <span data-ttu-id="8af68-111">Ein Kennwort für das Add-In, das als geheimer Clientschlüssel bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="8af68-111">A password for the add-in, called a client secret.</span></span>
    
 
- <span data-ttu-id="8af68-112">Ein Anzeigename für das Add-In, der auf der Zustimmungsseite verwendet wird, auf der der Benutzer aufgefordert wird, dem Add-In zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="8af68-112">A display name of the add-in that is used on the consent page where the user is prompted to trust the add-in.</span></span>
    
 
- <span data-ttu-id="8af68-113">Eine URL für die Domäne, in der das Remote-Add-In gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="8af68-113">A URL for the domain where the remote add-in is hosted.</span></span>
    
 
- <span data-ttu-id="8af68-114">Eine Umleitungs-URL.</span><span class="sxs-lookup"><span data-stu-id="8af68-114">A redirect URL.</span></span>
    
 
<span data-ttu-id="8af68-p103">Nachdem Sie das Add-In registriert haben, verfügt es über eine Add-In-Identität und ist ein *Sicherheitsprinzipal*, der als Add-In-Prinzipal bezeichnet wird. Wenn Sie das Add-In installieren, können SharePoint-Administratoren Informationen zum jeweiligen Add-In-Prinzipal abrufen.</span><span class="sxs-lookup"><span data-stu-id="8af68-p103">After you register your add-in, it has an add-in identity and is a security principal, referred to as an add-in principal. When you install your add-in, spnv administrators can retrieve information about that particular add-in principal.</span></span>
 
<span data-ttu-id="8af68-p104">Wenn ein Benutzer zum ersten Mal Add-In-Berechtigungen zum Zugreifen auf SharePoint-Ressourcen gewährt (dies kann entweder während der Installation oder zur Laufzeit erfolgen, abhängig vom Design des Add-Ins), erhält SharePoint Informationen über das Add-In von Azure ACS. SharePoint speichert diese Informationen dann in der Datenbank des App-Verwaltungsdiensts in der SharePoint-Mandantschaft oder -Farm. Der geheime Clientschlüssel wird nur mit Azure ACS gespeichert. SharePoint ist das Geheimnis des Add-Ins niemals bekannt. Der Inhaltsdatenbankdienst und andere Komponenten, wie z. B. der Benutzerprofildienst, können den Anzeigenamen und andere grundlegende Informationen über das Add-In direkt vom freigegebenen App-Verwaltungsdienst abrufen. Weitere Informationen finden Sie unter [Abrufen von Informationen zur Add-In-Registrierung und zum Add-In-Prinzipal ](register-sharepoint-add-ins-2013#Retrieve) in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="8af68-p104">After you register your add-in, it has an add-in identity and is a  security principal  , referred to as anadd-in principal. When you install your add-in, SharePoint administrators can retrieve information about that particular add-in principal.When a user first grants an add-in permissions to access SharePoint resources (which can happen either at installation or runtime, depending on the design of the app), SharePoint gets information about the add-in from Azure ACS. SharePoint then stores this information in the App Management Service database of the SharePoint tenancy or farm. The client secret is stored only with Azure ACS. SharePoint never knows the add-in's secret. The content database service and other components, such as the user profile service, can get the display name and other basic information about the add-in directly from the app management shared service. For more information, see  [Retrieve add-in registration and add-in principal information ](register-sharepoint-add-ins-2013#Retrieve) in this article.</span></span>
 

 <span data-ttu-id="8af68-p105">**Hinweis** In diesem Artikel wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten und Prinzipien des OAuth 2.0-Frameworks vertraut sind. Weitere Informationen finden Sie unter [OAuth.net](http://oauth.net/) und [Web-Autorisierungsprotokoll (oauth)](http://datatracker.ietf.org/doc/active/).</span><span class="sxs-lookup"><span data-stu-id="8af68-p105">**Note** This article assumes that you are familiar with the basic concepts and principles behind the OAuth 2.0 Framework. For more information, see  [OAuth.net](http://oauth.net/) and [Web Authorization Protocol (oauth)](http://datatracker.ietf.org/doc/active/).</span></span>
 


## <a name="register-your-sharepoint-add-in-in-azure-acs"></a><span data-ttu-id="8af68-125">Registrieren Ihres SharePoint-Add-Ins bei Azure ACS</span><span class="sxs-lookup"><span data-stu-id="8af68-125">Register your SharePoint Add-in in Azure ACS</span></span>

<span data-ttu-id="8af68-126">Es gibt drei Möglichkeiten zum Registrieren eines Add-Ins. Welche Methode Sie auswählen, hängt davon ab, an welcher Stelle des Add-In-Entwicklungslebenszyklus Sie sich befinden, sowie von der Architektur Ihres Add-Ins und dem geplanten Markteinführungsverfahren.</span><span class="sxs-lookup"><span data-stu-id="8af68-126">You can register your add-in in one of three ways, depending on where you are in the add-in development life cycle, the architecture of your add-in, and how you plan to market it.</span></span>
 

 


|<span data-ttu-id="8af68-127">**Registrierungsmethode**</span><span class="sxs-lookup"><span data-stu-id="8af68-127">**Registration method**</span></span>|<span data-ttu-id="8af68-128">**Details**</span><span class="sxs-lookup"><span data-stu-id="8af68-128">**Details**</span></span>|
|:-----|:-----|
|<span data-ttu-id="8af68-129">Verwenden von Visual Studio und Microsoft Office Developer Tools für Visual Studio zum Erstellen einer temporären Add-In-Identität</span><span class="sxs-lookup"><span data-stu-id="8af68-129">Use Visual Studio and Microsoft Office Developer Tools for Visual Studio to create a temporary add-in identity.</span></span>|<span data-ttu-id="8af68-p106">Der Assistent der Office Developer Tools für Visual Studio erstellt eine temporäre Registrierung für Ihr Add-In bei ACS und beim App-Verwaltungsdienst Ihrer SharePoint-Testwebsite. Wenn Sie das Add-In in Visual Studio ausführen (F5), wird diese Identität verwendet. Die Tools fügen außerdem die Client-ID und den geheimen Clientschlüssel in die Dateien „web.config“ und „AppManifest.xml“ ein. Wenn Sie Ihr Add-In veröffentlichen möchten, können Sie den Visual Studio-Veröffentlichungs-Assistenten verwenden, um zum Verkäuferdashboard zu wechseln und das Add-In zu registrieren. Wenn Sie Ihre SharePoint-Add-Ins nicht im Office Store vermarkten, verwenden Sie „AppRegNew.aspx“ für die Registrierung. (Die genauen Schritte finden Sie unten.) **Hinweis** Wenn das Add-In die Berechtigung zum Zugreifen auf SharePoint-Ressourcen dynamisch zur Laufzeit anfordert anstatt bei der Add-In-Installation, können Sie Visual Studio nicht zum Erstellen von Add-In-Identitäten verwenden.</span><span class="sxs-lookup"><span data-stu-id="8af68-p106">The Office Developer Tools for Visual Studio wizard creates a temporary registration for your add-in with ACS and the App Management Service of your SharePoint test website. When you run the add-in from Visual Studio (F5), this identity is used. The tools also insert the client ID and secret in the web.config and AppManifest.xml files.When you're ready to publish your add-in, you can use the Visual Studio publish wizard to go to the Seller Dashboard to register it. If you are not marketing your SharePoint Add-in in the Office Store, use AppRegNew.aspx to register it. (Exact steps are below.) **Note**  If your add-in requests permission to access SharePoint resources dynamically at run time, instead of on add-in installation, you cannot use Visual Studio to create add-in identities.</span></span> |
|<span data-ttu-id="8af68-135">Registrieren des Add-Ins über das Verkäuferdashboard.</span><span class="sxs-lookup"><span data-stu-id="8af68-135">Register the add-in through the Seller Dashboard.</span></span>|<span data-ttu-id="8af68-p107">Wenn Sie Ihr Add-In in mehreren SharePoint-Mandanten oder -Farmen verwenden möchten, verwenden Sie das Verkäuferdashboard zum Registrieren des Add-Ins, unabhängig davon, ob Sie es im Office Store vermarkten oder über den Add-In-Katalog zur Verfügung stellen möchten. Bei der Registrierung im Verkäuferdashboard können Sie Ihr Add-In mit einer mehrinstanzfähigen Architektur entwerfen, ohne dass Mandanten- oder Farmadministratoren es separat registrieren müssen. Wenn Sie beabsichtigen, Ihr Add-In im Office Store zu veröffentlichen, müssen Sie das Verkäuferdashboard zum Registrieren des Add-Ins verwenden. Sie müssen nicht den Store verwenden, um ein Add-In zu veröffentlichen, das beim Verkäuferdashboard registriert ist. Weitere Informationen finden Sie unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](http://msdn.microsoft.com/library/create-or-update-client-ids-and-secrets-in-the-seller-dashboard%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="8af68-p107">If you're going to use your add-in in more than one SharePoint tenant or farm, use the Seller Dashboard to register your add-in, regardless of whether you will market it in the Office Store or make it available via the add-in catalog. When you register in the Seller Dashboard, you can design your add-in with a multitenant architecture without requiring tenant or farm administrators to register it separately. Also, if you plan to publish your add-in in the Office Store, you have to use the Seller Dashboard to register your add-in. You don't have to use the store to publish an add-in that is registered with the Seller Dashboard.</span></span>|
|<span data-ttu-id="8af68-140">Verwenden der Seite „AppRegNew.aspx“</span><span class="sxs-lookup"><span data-stu-id="8af68-140">Use the AppRegNew.aspx page.</span></span>|<span data-ttu-id="8af68-p108">Verwenden Sie das AppRegNew-Formular zum Registrieren Ihres SharePoint-Add-Ins, wenn Sie das Add-In nur in einem Mandanten oder einer Farm verwenden möchten. Beispiel: Wenn Sie Add-Ins für eine einzelne Organisation erstellen und sie über den Add-In-Katalog der Organisation verteilen werden, können Sie die Seite „AppRegNew.aspx“ jeder Website in einem Mandanten oder einer Farm verwenden, um das Add-In zu registrieren. Add-Ins, die bei „AppRegNew.aspx“ registriert sind, können nicht im Office Store veröffentlicht werden. Für Add-Ins, die im Office Store veröffentlicht werden sollen, müssen Sie eine Identität aus dem Verkäuferdashboard abrufen.</span><span class="sxs-lookup"><span data-stu-id="8af68-p108">Use the AppRegNew form to register your SharePoint Add-in if you are going to use the add-in only in one tenant or farm. For example, if you're creating add-ins for a single organization and you're going to distribute them via the organization add-in catalog, you can use the AppRegNew.aspx page of any website in a tenancy or farm to register the add-in.You cannot publish an add-in that is registered with AppRegNew.aspx to the Office Store. For add-ins that are published to the Office Store, you must get an identity from the Seller Dashboard.</span></span>|

### <a name="to-register-by-using-appregnewaspx"></a><span data-ttu-id="8af68-144">So führen Sie die Registrierung mit „AppRegNew.aspx“ durch</span><span class="sxs-lookup"><span data-stu-id="8af68-144">To register by using AppRegNew.aspx</span></span>


1.  <span data-ttu-id="8af68-145">Navigieren Sie zu `http://` *<SharePointWebsite>* `/_layouts/15/AppRegNew.aspx` im Mandanten oder der Farm.</span><span class="sxs-lookup"><span data-stu-id="8af68-145">Navigate to `http://` *<SharePointWebsite>*  `/_layouts/15/AppRegNew.aspx` on the tenancy or farm.</span></span>
    
    <span data-ttu-id="8af68-146">**AppRegNew-Seitenformular**</span><span class="sxs-lookup"><span data-stu-id="8af68-146">**AppRegNew page form**</span></span>

 

  ![Das Formular auf der Seite „AppRegNew“ mit Feldern für die Client-ID, den geheimen Clientschlüssel, den Titel, die App-Domäne &amp; die Umleitungs-URL. Neben den ersten beiden werden Schaltflächen namens „Generieren“ angezeigt. In der Ecke befinden sich die Schaltflächen „Erstellen“ und „Abbrechen“.](../../images/9a38d876-2189-418c-9314-ae493a4cab61.PNG)
 

 

 
2. <span data-ttu-id="8af68-150">Geben Sie Werte für die folgenden Formularfelder ein:</span><span class="sxs-lookup"><span data-stu-id="8af68-150">Enter values for the follow form fields:</span></span>
    
      -  <span data-ttu-id="8af68-p110">**Add-In-ID**: Die Add-In-ID, die auch als Client-ID bezeichnet wird, ist eine GUID, die generiert (wenn Sie **Generieren** wählen) oder in AppRegNew.aspx eingefügt werden kann. Der Wert muss für jedes Add-In eindeutig sein und *kleingeschrieben*  werden.</span><span class="sxs-lookup"><span data-stu-id="8af68-p110">**Add-in ID** - Also known as client ID, is a GUID that can be generated (when you choose **Generate**) or pasted into AppRegNew.aspx. The value must be unique for each add-in, and  *must be lower case*  .</span></span>
    
 
  -  <span data-ttu-id="8af68-p111">**Geheimer Add-In-Schlüssel**: Der geheime Add-In-Schlüssel, der auch als geheimer Clientschlüssel bezeichnet wird, ist eine opake Zeichenkette. Er wird auf der Seite AppRegNew.aspx über die Schaltfläche **Generieren** generiert. Im Folgenden sehen Sie ein Beispiel für einen geheimen Add-In-Schlüssel: **xvVpG0AgVIJfch6ldu4dLUlcZyysmGqBRbpFDu6AfJw=**.</span><span class="sxs-lookup"><span data-stu-id="8af68-p111">**Add-in Secret** - Also known as the client secret, an opaque string. It is generated on the AppRegNew.aspx page by using the **Generate** button. The following is an example of an add-in secret: **xvVpG0AgVIJfch6ldu4dLUlcZyysmGqBRbpFDu6AfJw=**.</span></span>
    
     <span data-ttu-id="8af68-p112">**Wichtig** Geheime Add-In-Schlüssel laufen ab. Wenn Sie das Add-In im Verkäuferdashboard registrieren, können Sie die Ablaufdauer auf bis zu 3 Jahre festlegen. Im Dashboard können Sie außerdem neue geheime Schlüssel hinzufügen, wenn sich die alten ihrem Ablaufdatum nähern. Der neue geheime Schlüssel wird in allen Instanzen des Add-Ins aktiviert. Wenn Sie das Add-In bei AppRegNew.aspx registrieren, läuft der geheime Schlüssel nach einem Jahr ab. Ausführliche Informationen finden Sie unter [Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In](replace-an-expiring-client-secret-in-a-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="8af68-p112">**Important** Add-in secrets expire. If you register the add-in on the Seller Dashboard, you can set the expiration for up to three years. In the dashboard, you can also add new secrets when the old ones reach their expiration date. The new secret will be enabled in all instances of the add-in. If you register the add-in with AppRegNew.aspx, the secret expires in one year. For details, see  [Replace an expiring client secret in a SharePoint Add-in](replace-an-expiring-client-secret-in-a-sharepoint-add-in).</span></span>
  -  <span data-ttu-id="8af68-p113">**Titel**: Ein benutzerfreundlicher Titel, zum BeispielContoso-Fotodruck-Add-In. Benutzer werden aufgefordert, dem Add-In die Berechtigungen zu gewähren oder zu verweigern, die das Add-In anfordert. Dieser Titel wird als Name des Add-Ins bei der Zustimmungseingabeaufforderung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8af68-p113">**Title** - A user-friendly title; for example,Contoso photo printing add-in. Users are prompted to grant or deny the add-in the permissions that the add-in is requesting. This title appears as the name of the add-in on the consent prompt.</span></span> 
    
 
  -  <span data-ttu-id="8af68-p114">**Add-In-Domäne**: Der Hostname der Remotekomponente des SharePoint-Add-In. Wenn die Remoteanwendung nicht Port 443 verwendet, muss die Add-In-Domäne auch die Portnummer enthalten. Die Add-In-Domäne muss mit den URL-Bindungen übereinstimmen, die Sie für Ihre Webanwendung verwenden. Geben Sie in diesem Wert kein Protokoll („https:") oder „/"-Zeichen an. (Wenn Ihr Webanwendungshost einen DNS-CNAME-Aliasnamen verwendet, benutzen Sie den Alias.) Nachfolgend sind einige Beispiele aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="8af68-p114">**Add-in Domain** - The host name of the remote component of the SharePoint Add-in. If the remote application isn't using port 443, the add-in domain must also include the port number. The add-in domain must match the URL bindings you use for your web application. Do not include protocol ("https:") or "/" characters in this value. If your web application host is using a DNS CNAME alias, use the alias. Some examples:</span></span>
    
      - <span data-ttu-id="8af68-171">www.contoso.com:3333</span><span class="sxs-lookup"><span data-stu-id="8af68-171">www.contoso.com:3333</span></span>
    
 
  - <span data-ttu-id="8af68-172">www.fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="8af68-172">www.fabrikam.com</span></span>
    
 
  -  <span data-ttu-id="8af68-p115">**Umleitungs-URI:**: Der Endpunkt in Ihrer Remoteanwendung oder dem Dienst, an die bzw. den ACS einen Authentifizierungscode sendet. Genau genommen verwenden SharePoint-Add-Ins diesen Wert nicht. Der Umleitungs-URI ist für Webanwendungen erforderlich, die außerhalb von SharePoint gestartet werden und den [Authentifizierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization#Flows) verwenden, um autorisierten Zugriff auf SharePoint-Daten zu erhalten. Der Umleitungs-URI wird für echte SharePoint-Add-Ins ignoriert (die von SharePoint gestartet werden und den [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization#Flows) verwenden). Der Umleitungs-URI ist in der Regel dieselbe Seite, Controllermethode oder Webdienstmethode, die den Authentifizierungscode von ACS angefordert hat, es kann sich jedoch auch um einen anderen Endpunkt handeln. Der Endpunkt muss über Logik verfügen, die den Autorisierungscode aus der von ACS gesendeten HTTP-Antwort abruft und dann diesen Code verwendet, um ein Zugriffs- und Aktualisierungstoken anzufordern. Weitere Informationen finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](authorization-code-oauth-flow-for-sharepoint-add-ins). Das Formular erfordert, dass Sie auch für echte SharePoint-Add-Ins einen gültigen Wert eingeben, obwohl er nicht verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8af68-p115">**Redirect URI:** - The endpoint in your remote application or service to which ACS sends an authentication code. Strictly speaking, SharePoint Add-ins don't use this value. The redirect URI is required for web applications that are launched outside of SharePoint and that use the [Authentication Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization#Flows) to get authorized access to SharePoint data. The Redirect URI is ignored for true SharePoint Add-ins (which are launched from SharePoint and use the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization#Flows)). The Redirect URI is usually the same page, controller method, web service method that requested the authentication code from ACS, but it can be a different endpoint. The endpoint must have logic that gets the authorization code from the HTTP Response that is sent by ACS and then uses that code to request an access and refresh token. For more information, see  [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins). The form requires that you enter a valid value even for true SharePoint Add-ins, although it is not used.</span></span>
    
    <span data-ttu-id="8af68-p116">Der Wert muss eine vollständige Endpunkt-URL, einschließlich des Protokolls sein; dieses muss *HTTPS* sein. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8af68-p116">The value must be a complete endpoint URL including the protocol,  *which must be HTTPS*  . For example:</span></span>
    
      - <span data-ttu-id="8af68-183">https://www.contoso.com/Default.aspx</span><span class="sxs-lookup"><span data-stu-id="8af68-183">https://www.contoso.com/Default.aspx</span></span>
    
 
  - <span data-ttu-id="8af68-184">https://www.fabrikam.com/RedirectAccept.aspx</span><span class="sxs-lookup"><span data-stu-id="8af68-184">https://www.fabrikam.com/RedirectAccept.aspx</span></span>
    
 
  - <span data-ttu-id="8af68-185">https://www.northwindtraders.com/home/index</span><span class="sxs-lookup"><span data-stu-id="8af68-185">https://www.northwindtraders.com/home/index</span></span>
    
 
  - <span data-ttu-id="8af68-186">https://adventureworks.com/vacationdata.svc</span><span class="sxs-lookup"><span data-stu-id="8af68-186">https://adventureworks.com/vacationdata.svc</span></span>
    
 
3. <span data-ttu-id="8af68-p117">Wählen Sie im Formular **Erstellen** aus. Die Seite wird neu geladen und zeigt eine Bestätigung der von Ihnen eingegebenen Werte an. Zeichnen Sie diese Werte in einer Form auf, die einfach kopiert und eingefügt werden kann. Sie müssen die Werte in die Dateien „web.config“ und „AppManifest.xml“ oder den Visual Studio-Assistenten zum **Veröffentlichen** eingeben.</span><span class="sxs-lookup"><span data-stu-id="8af68-p117">Choose **Create** on the form. The page will reload and show a confirmation of the values you entered. Make a record of these values in a form that is eay to copy and paste. You will need to enter the values in web.config and AppManifest.xml files or in the Visual Studio **Publish** wizard.</span></span>
    
 
<span data-ttu-id="8af68-p118">Unabhängig davon, wie Sie Ihr SharePoint-Add-In registrieren, wenn Sie bereit sind, das Add-In für Staging oder Produktion bereitzustellen, müssen Sie  [Eingeben der Registrierungswerte in die Dateien web.config und AppManifest.xml](#EditConfigFiles). Wenn Sie Visual Studio verwenden, übernehmen die Microsoft Office-Entwicklertools für Visual Studio diese Konfiguration für Sie.</span><span class="sxs-lookup"><span data-stu-id="8af68-p118">Regardless of how you register your SharePoint Add-in, when you are ready to deploy the add-in to staging or production, you'll need to  [Enter the registration values into the web.config and AppManifest.xml files](#EditConfigFiles). If you are using Visual Studio, the Microsoft Office Developer Tools for Visual Studio do this configuration for you.</span></span>
 

 

## <a name="enter-the-registration-values-into-the-webconfig-and-appmanifestxml-files"></a><span data-ttu-id="8af68-193">Eingeben der Registrierungswerte in die Dateien „web.config“ und „AppManifest.xml“</span><span class="sxs-lookup"><span data-stu-id="8af68-193">Enter the registration values into the web.config and AppManifest.xml files</span></span>
<span data-ttu-id="8af68-194"><a name="EditConfigFiles"> </a></span><span class="sxs-lookup"><span data-stu-id="8af68-194"></span></span>

<span data-ttu-id="8af68-195">Bevor Sie das SharePoint-Add-In verpacken und seine Remotekomponenten bereitstellen, geben Sie einige der Registrierungswerte in die Dateien „AppManifest.xml" und „web.config" ein.</span><span class="sxs-lookup"><span data-stu-id="8af68-195">Before you package the SharePoint Add-in and before you deploy its remote components, enter some of the registration values in the AppManifest.xml and the web.config file.</span></span>
 

 

 <span data-ttu-id="8af68-196">**Tipp** Wenn Sie Ihr SharePoint-Add-In mithilfe des Visual Studio-Veröffentlichungs-Assistenten veröffentlichen, werden Sie von Visual Studio während des Veröffentlichungsprozesses zur Eingabe einer Client-ID und eines geheimen Clientschlüssels aufgefordert. Diese Informationen werden für Sie jeweils an der richtigen Stelle eingefügt.</span><span class="sxs-lookup"><span data-stu-id="8af68-196">**TIP** If you publish your SharePoint Add-in by using the Visual Studio publish wizard, Visual Studio will prompt you for a client ID and client secret during the publishing process, and it will put the information in the correct places for you.</span></span>
 


1. <span data-ttu-id="8af68-197">Geben Sie im Visual Studio-Projekt in der Datei „Web.config“ den Add-In-ID-Wert als **ClientId**-Wert ein (der den temporären Wert ersetzt, den die Tools eingegeben haben).</span><span class="sxs-lookup"><span data-stu-id="8af68-197">In the Web.config file in your Visual Studio project, enter the add-in ID value as the **ClientId** value (replacing the temporary value that the tools entered).</span></span>
    
     <span data-ttu-id="8af68-198">**Wichtig** Alle Buchstaben in der Client-ID-GUID müssen kleingeschrieben sein.</span><span class="sxs-lookup"><span data-stu-id="8af68-198">**Important** All the letters in the client ID GUID must be lowercase.</span></span>

    <span data-ttu-id="8af68-199">Es folgt ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="8af68-199">The following is an example.</span></span>
    


```XML
  <appSettings>
  <add key="ClientId" value="a044e184-7de2-4d05-aacf-52118008c44e " />
   .  .  .
</appSettings>
```

2. <span data-ttu-id="8af68-200">Geben Sie den Wert für den geheimen Add-In-Schlüssel als **ClientSecret**-Wert ein (der den temporären Wert ersetzt, den die Tools eingegeben haben).</span><span class="sxs-lookup"><span data-stu-id="8af68-200">Enter the add-in secret value as the **ClientSecret** value (replacing the temporary value that the tools entered).</span></span>
    
    <span data-ttu-id="8af68-201">Nachfolgend sehen Sie ein Beispiel für die Verwendung der Werte in der Datei „Web.config“ einer Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="8af68-201">The following is an example of how the values are used in the Web.config file of a web application.</span></span>
    


```XML
  <appSettings>
  <add key="ClientId" value="a044e184-7de2-4d05-aacf-52118008c44e " />
  <add key="ClientSecret" value="l0z/8TzWN0yQBzMBSEZtYts2Vt3Eo/oE3rfCdPaogKQ= " />
</appSettings>
```

3. <span data-ttu-id="8af68-202">Geben Sie im Visual Studio-Projekt in der Datei „AppManifest.xml“ den Add-In-ID-Wert als **ClientId** *in Kleinbuchstaben* ein.</span><span class="sxs-lookup"><span data-stu-id="8af68-202">In the AppManifest.xml file in your Visual Studio project, enter the add-in ID value as the **ClientId** value, *with lower case letters*  .</span></span>
    
     <span data-ttu-id="8af68-p119">**Hinweis** Das Add-In-Manifest gilt nicht für Webanwendungen, bei denen die Berechtigung für den Zugriff auf SharePoint-Ressourcen spontan abgerufen wird. Diese sind eigentlich keine „SharePoint-Add-Ins“. Sie werden nicht in SharePoint installiert und haben kein Add-In-Manifest. Weitere Informationen finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](authorization-code-oauth-flow-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="8af68-p119">**Note** The add-in manifest does not apply to web applications that request permission to access SharePoint resources on the fly. These are not really "SharePoint Add-ins". They are not installed on SharePoint and do not have an add-in manifest. For more information, see  [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins).</span></span>

    <span data-ttu-id="8af68-207">Das folgende Beispiel veranschaulicht die Verwendung des **ClientId**-Werts in der Datei „AppManifest.xml“.</span><span class="sxs-lookup"><span data-stu-id="8af68-207">The following example shows how the **ClientId** value is used in the AppManifest.xml file.</span></span>
    


```XML
  <AppPrincipal>
  <RemoteWebApplication ClientId="a044e184-7de2-4d05-aacf-52118008c44e "/>
</AppPrincipal>
```

4. <span data-ttu-id="8af68-p120">Die Office Developer Tools für Visual Studio verwenden das Token `~remoteAppUrl` im **StartPage**-Element (z. B. `<StartPage>~remoteAppUrl/Pages/Default.aspx?{StandardTokens}</StartPage>`). Dieses Token löst sich in die URL der Remotekomponente auf, wenn Sie den **Veröffentlichungs**-Assistenten in Visual Studio verwenden. Wenn Sie den Assistenten nicht verwenden (oder wenn Sie ihn verwenden, die Remotekomponente jedoch in Azure veröffentlichen), müssen Sie das Token manuell durch den Wert **Add-In-Domäne** ersetzen, den Sie bei der Registrierung des Add-Ins verwendet haben. Verwenden Sie dabei *exakt* denselben Wert, einschließlich Portnummer (falls vorhanden), es sei denn, dass Sie auch das HTTPS-Protokoll einschließen. Nachfolgend ist ein Beispiel hierfür aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="8af68-p120">The Office Developer Tools for Visual Studio use the token  `~remoteAppUrl` in **StartPage** element. (For example, `<StartPage>~remoteAppUrl/Pages/Default.aspx?{StandardTokens}</StartPage>`.) This token resolves to the URL of the remote component if you are using the **Publish** wizard in Visual Studio. If you don't use the wizard (or if you do but you are publishing the remote component to Azure), you have to manually replace the token with the **Add-in Domain** value that you used when registering the add-in. It must be *exactly*  the same value, including port number, if any, except that you include the HTTPS protocol as well. The following is an example.</span></span>
    
```XML
  <StartPage>https://www.contoso.com/Pages/Default.aspx?{StandardTokens}</StartPage>
```

5. <span data-ttu-id="8af68-p121">Ziehen Sie die Verwendung desselben Werts für das **Title**-Element in der AppManifest.xml-Datei in Betracht, den Sie für das Feld **Titel** in AppRegNew.aspx verwendet haben. Der Wert für das **Title**-Element ist der Name des Add-Ins, den Benutzer nach der Installation des Add-Ins sehen. Für Benutzer ist es möglicherweise verwirrend, wenn das Add-In im Zustimmungsdialogfeld einen anderen Namen hat als in der SharePoint-Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8af68-p121">Consider using the same value for the **Title** element in the AppManifest.xml file that you used for the **Title** field in AppRegNew.aspx. The **Title** element value is the name of the add-in that users see after it is installed. It might be confusing to users for the add-in to have a different name in the consent dialog than it has in the SharePoint UI.</span></span>
    
    <span data-ttu-id="8af68-216">Das folgende Beispiel zeigt diese Werte im Add-In-Manifest.</span><span class="sxs-lookup"><span data-stu-id="8af68-216">The following example shows these values in the add-in manifest.</span></span>
    


```XML
  <Properties>
  <Title>Contoso photo printing app</Title>
  <StartPage>https://www.contoso.com/Pages/Default.aspx?{StandardTokens}</StartPage>
</Properties>
```


## <a name="use-the-redirect-url-in-an-add-in-that-asks-for-permissions-on-the-fly"></a><span data-ttu-id="8af68-217">Verwenden der Umleitungs-URL in einem Add-In, das Berechtigungen im laufenden Betrieb anfordert</span><span class="sxs-lookup"><span data-stu-id="8af68-217">Use the redirect URL in an add-in that asks for permissions on the fly</span></span>
<span data-ttu-id="8af68-218"><a name="UseRedirectUrl"> </a></span><span class="sxs-lookup"><span data-stu-id="8af68-218"></span></span>

<span data-ttu-id="8af68-p122">Wenn Ihre Webanwendung außerhalb von SharePoint gestartet wird (und daher kein wirkliches SharePoint-Add-In ist), muss sie so ausgelegt sein, dass sie zur Laufzeit Berechtigungen von SharePoint anfordert. Darüber hinaus muss sie Code enthalten, der den Umleitungs-URI zusammen mit anderen Informationen verwendet, um ein Zugriffstoken von ACS abzurufen. Suchen Sie die Stelle, an der dieser URI festgelegt ist, und verwenden Sie  *exakt*  den Wert, den Sie für das Feld **Umleitungs-URI** auf der Seite „AppRegNew.aspx" oder im Verkäuferdashboard verwendet haben. Dieser kann sich in einer Codedatei oder einer Konfigurationsdatei befinden.</span><span class="sxs-lookup"><span data-stu-id="8af68-p122">If your web application is launched from outside SharePoint (and is, thus, not a true SharePoint Add-in), then it has to be designed to ask for permissions from SharePoint at runtime. It has to have code that uses the redirect URI, along with other information, to obtain an access token from ACS. Find the place where this URI is set and use the  *exact*  value that you used for the **Redirect URI** field on AppRegNew.aspx or in the Seller Dashboard. This might be in a code file or a configuration file.</span></span>
 

 

## <a name="retrieve-add-in-registration-and-add-in-principal-information"></a><span data-ttu-id="8af68-223">Abrufen von Informationen zu Add-In-Registrierung und Add-In-Prinzipal</span><span class="sxs-lookup"><span data-stu-id="8af68-223">Retrieve add-in registration and add-in principal information</span></span>
<span data-ttu-id="8af68-224"><a name="Retrieve"> </a></span><span class="sxs-lookup"><span data-stu-id="8af68-224"></span></span>

<span data-ttu-id="8af68-225">Sie können die Informationen zu Add-In-Registrierung und Add-In-Prinzipal für Ihre Add-Ins abrufen, die Sie unter SharePoint installiert oder registriert haben.</span><span class="sxs-lookup"><span data-stu-id="8af68-225">You can retrieve add-in registration information and add-in principal information for the add-ins you've installed or registered on SharePoint.</span></span> 
 

 
<span data-ttu-id="8af68-226">Um nach Registrierungsinformationen für ein Add-In zu suchen, das Sie registriert haben, wechseln Sie zu `http://` *<SharePointWebsite>* `/_layouts/15/AppInv.aspx`.</span><span class="sxs-lookup"><span data-stu-id="8af68-226">To look up registration information for an add-in that you have registered, go to  `http://` *<SharePointWebsite>*  `/_layouts/15/AppInv.aspx`.</span></span>
 

 
<span data-ttu-id="8af68-p123">Zum Nachschlagen benötigen Sie die Client-ID (auch als Add-In-ID bezeichnet), die Sie bei der Registrierung des Add-Ins verwendet haben. Der Nachschlagevorgang gibt für die entsprechende Client-ID die folgenden Informationen zurück:</span><span class="sxs-lookup"><span data-stu-id="8af68-p123">To do a lookup, you have to remember the client ID (also known as the add-in ID) that was used to register the add-in. The lookup returns the following information for a particular client ID:</span></span>
 

 

- <span data-ttu-id="8af68-229">Titel</span><span class="sxs-lookup"><span data-stu-id="8af68-229">Title</span></span>
    
 
- <span data-ttu-id="8af68-230">Add-In-Domäne</span><span class="sxs-lookup"><span data-stu-id="8af68-230">Add-in domain</span></span>
    
 
- <span data-ttu-id="8af68-231">Umleitungs-URL (entspricht dem Umleitungs-URI)</span><span class="sxs-lookup"><span data-stu-id="8af68-231">Redirect URL (this is the same as the redirect URI.)</span></span>
    
 
<span data-ttu-id="8af68-232">Der Nachschlagevorgang gibt nicht den Wert des geheimen Add-In-Schlüssels zurück.</span><span class="sxs-lookup"><span data-stu-id="8af68-232">The lookup does not return the add-in secret value.</span></span>
 

 
<span data-ttu-id="8af68-233">Um eine Liste der registrierten Add-In-Prinzipale anzuzeigen, wechseln Sie zu:</span><span class="sxs-lookup"><span data-stu-id="8af68-233">To see a list of registered add-in principals, go to:</span></span>
 

 
 <span data-ttu-id="8af68-234">`http://` *<SharePointWebsite>*  `/_layouts/15/AppPrincipals.aspx`</span><span class="sxs-lookup"><span data-stu-id="8af68-234"></span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="8af68-235">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8af68-235">Additional resources</span></span>
<span data-ttu-id="8af68-236"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="8af68-236"></span></span>


-  [<span data-ttu-id="8af68-237">Autorisierung und Authentifizierung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8af68-237">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="8af68-238">Drei Autorisierungssysteme für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8af68-238">Three authorization systems for SharePoint Add-ins</span></span>](three-authorization-systems-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="8af68-239">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8af68-239">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
