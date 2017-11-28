---
title: "Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 1742bdc985fa133bb6866803ce37aac74c419e17
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a>Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online


_**Gilt für:** SharePoint Online_

Im Rahmen von der neuen Client Side Objekt Modell (CSOM) Version (4622.1208 oder höher) hat SharePoint die Möglichkeit, benutzerdefinierte Benutzerprofileigenschaften Import Massen. Nur die Option musste vor dieser Version des Benutzers Profil CSOM Vorgänge für die Aktualisierung bestimmter Eigenschaften für einzelne Benutzerprofile nutzen. Dieser Ansatz ist jedoch ineffiziente und zu zeitaufwendig (insbesondere dann, wenn mehrere tausend Profile zu tun).

Viele Unternehmen müssen benutzerdefinierte Attribute auf der SharePoint-Benutzerprofildienst replizieren und so eine weitere leistungsfähige Benutzerprofil Bulk API freigegeben wurde.

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a>Eine Übersicht über die Massen Benutzer Profile Update-Prozess
<a name="sectionSection0"> </a>

![Massen UPA Update-Datenfluss](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. Benutzerattribute werden aus Active Directory des Unternehmens mit Azure Active Directory synchronisiert. Sie können auswählen, welche Attribute in lokalen und Azure repliziert werden.
2. Ein standardisierter Satz mit Attributen werden von Azure Active Directory mit SharePoint Online-Benutzerprofilspeicher in Office 365 repliziert. Unlke lokale SharePoint, diese Attribute können nicht angepasst werden.
3. Eine benutzerdefinierte Synchronisierungstool Nutzen der Vorteile des neuen Bulk Updates APIs. Dieses Tool eine JSON-Datei, die dem Office 365-Mandanten hochlädt und in die Warteschlange des Importvorgangs. Dieses Tool kann implementiert werden, mithilfe von verwaltetem Code (.NET) oder als eine PowerShell Skript mithilfe der neuen CSOM-APIs.
4. Eine Zeile des Business (LOB) System oder für alle externen Systeme ist die Quelle der Informationen in der Datei JSON. Dies kann auch eine Kombination von Daten aus Active Directory und alle externen Systeme sein. Beachten Sie, dass aus der Sicht API LOB-System selbst einer lokalen SharePoint 2013 oder 2016 Farm werden konnte.
5. Ein außerhalb des im Feld Server Seite Zeitgeberauftrags in SharePoint online mit dem überprüft importanforderungen in der Warteschlange und führt die tatsächlichen Importvorgangs basierend auf die API-Aufrufe und die Informationen in der bereitgestellten JSON-Datei.
6. Erweiterte Benutzerprofilinformationen ist innerhalb von Benutzerprofilen verfügbar und kann aus einem aus der im Feld oder benutzerdefinierte Funktionen in SharePoint online verwendet werden.

>**Hinweis**: der Import funktioniert nur für Benutzerprofileigenschaften die wurden **nicht** durch Endbenutzer bearbeitet werden festgelegt. Dies ist, um zu verhindern, dass der Importprozess für Benutzerprofildaten überschreiben alle Informationen, die ein Endbenutzer bereits aktualisiert wurde. Darüber hinaus erlaubt der Import nur benutzerdefinierte Eigenschaften, die nicht active Directory Kerneigenschaften sind. Diese müssen mit Azure Active Directory synchronisiert werden. Der Liste der diese Directory Kerneigenschaften finden Sie unter der Tabelle im Abschnitt häufig gestellte Fragen zu aufgeführt.

Es folgt ein kurzes Video an, das mithilfe der neuen CSOM-API aus beiden verwaltetem Code (.NET) und PowerShell veranschaulicht. Sie können den Beispielcode verwendet, einschließlich des PowerShell-Beispielskripts im [Office Dev Plug & Play-Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202)suchen.

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a>Import-Dateiformat
<a name="sectionSection1"> </a>

Der Importvorgang verwendet eine JSON-Datei, die Eigenschaften und deren Werte enthält. Hier finden Sie die erwartete Struktur der Datei:   

```JSON
{
   "value": [
     {
       "<IdName>": "<UserIdValue_1>",
       "<AttributeName_1>": "<User1_AttributeValue_1>",
       "<AttributeName_2>": "<User1_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_2>",
       "<AttributeName_1>": "<User2_AttributeValue_1>",
       "<AttributeName_2>": "<User2_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_n>",
       "<AttributeName_1>": "<Usern_AttributeValue_1>",
       "<AttributeName_2>": "<Usern_AttributeValue_2>",
     }
   ]
}
```

Im folgenden ist eine einfaches Beispiel für die Datei das oben genannten-Format verwenden:

```JSON
{
  "value": [
    {
      "IdName": "vesaj@contoso.com",
      "City": "Helsinki",
      "Office": "Viper"
    },
    {
      "IdName": "bjansen@contoso.com",
      "City": "Brussels",
      "Office": "Beetle"
    },
    {
      "IdName": "unknowperson@contoso.com",
      "City": "None",
      "Office": ""
    },
    {
      "IdName": "erwin@contoso.com",
      "City": "Stockholm",
      "Office": "Elite"
    }
  ]
}
```

Im obigen Beispiel ist Identity Lösung basierend auf der `IdName` -Eigenschaft und es werden zwei Eigenschaften, die zu aktualisierenden aufgerufen `City` und `Office`. Die Datei enthält Informationen für vier verschiedene Konten in den Mandanten. Eigenschaftennamen, die in dieser Quelldatei verwendet stimmen nicht unbedingt die Namen in der SharePoint Online-Benutzerprofildienst verwendet werden, da wir die richtigen eigenschaftenzuordnung in unserem Code bereitgestellt werden. 

### <a name="source-data-file-restrictions"></a>Quelle Daten Datei Einschränkungen
Es gibt einige Einschränkungen für einzelne Quelldateien für Daten:
- Maximale Dateigröße: 2GB
- Maximale Anzahl von Eigenschaften: 500.000
- Die Quelldatei muss auf dem gleichen SharePoint Online-Mandanten hochgeladen werden, auf dem der Prozess gestartet wurde


## <a name="user-profile-property-import-process"></a>Importprozess für Benutzerprofildaten-Eigenschaft
<a name="sectionSection2"> </a>

Hier ist der vollständige Vorgang aus:

1. Erstellen oder zum Synchronisieren von Benutzern in einem Office 365-Mandanten oder zugeordnet Azure AD
     - Wenn Benutzer in Azure Active Directory synchronisiert werden, wird es auch einen standardisierten Satz mit Attributen zu SharePoint Online User Profile Service synchronisieren.
2. Erstellen Sie alle erforderlichen benutzerdefinierten Eigenschaften innerhalb des Benutzerprofildiensts
     - Da es keine remote-APIs zum Erstellen von benutzerdefinierten Eigenschaften in der Benutzerprofildienst ist, dieser Schritt muss manuell ausgeführt werden für jede der Mandanten, in dem benutzerdefinierte Benutzerprofileigenschaften erforderlich sind (Dies ist nur einmal pro Mandant ausgeführt werden).
     - Nur Benutzerprofileigenschaften "Unzulässige durch Endbenutzer bearbeitet werden" importiert werden können. Ein JSON importieren möchten-Objekteigenschaft auf einer Benutzerprofileigenschaft, die als "bearbeitbaren durch Endbenutzer" markiert ist eine Ausnahme ausgegeben, wenn die CSOM-API aufgerufen wird.
3. Erstellen und Hochladen der Datei JSON in Office 365-Mandanten
     - Sie müssen die JSON-Daten-Datei mit den Informationen, die dem Office 365-Mandanten aktualisiert werden hoch.
     - Im Fall einer Ausnahme während des Importvorgangs bieten SharePoint zusätzliche Protokollierungsinformationen in derselben Dokumentbibliothek, in dem die Datei in einem neuen Ordner Sub vorhanden war, gespeichert.
     - Bereinigen der Protokolldateien und JSON-Dateien werden nicht automatisch ausgeführt und liegt in der Verantwortung der benutzerdefinierten Lösung mithilfe der API. Sie sollten den Lebenszyklus von diese Dateien in der Implementierung. Diese Dateien werden in Dokumentbibliotheken gespeichert, so wird einen Teil des zugewiesenen Speichers für die Websitesammlung genutzt werden.
4. Rufen Sie das gleichzeitige UPA importieren-API für den Importauftrag queuing
     - Verwenden Sie die CSOM-API, um den Importvorgang in die Warteschlange. Dies kann durch Ausführen von CSOM Code mit einer verwalteten Code (.NET) oder PowerShell.
     - Die Methode, um den Auftrag in die Warteschlange erfordert Eigenschaftenzuordnungsinformationen und den Speicherort der Datei. Diese Methode führt schnell, da es nur die tatsächlichen Importvorgangs Warteschlangen, die später im Rahmen einer Back-End-Prozess in SharePoint Online ausgeführt wird.
5. Überprüfen Sie den Status des Auftrags für import
     - Remote-APIs können auch den Status einer bestimmten Importauftrag oder alle der letzte Importaufträge überprüfen. Um den Status für einen bestimmten Aufruf überprüfen können, sollten Sie speichern die eindeutige Auftrags-ID als Rückgabewert empfangen, wenn der Auftrag in der Warteschlange befinden.


## <a name="csom-api-for-the-bulk-import-process"></a>CSOM-API für den Massenimportvorgang
<a name="sectionSection3"> </a>

### <a name="queue-import"></a>Importieren von Warteschlangen.
Sie können die Warteschlange des Importvorgangs durch Aufrufen der [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) Methode befindet sich der [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) Objekt. Dies ist ein asynchroner Aufruf, dass er nicht die Quelldaten herunterladen oder führen Sie den Import, sondern einfach eine Arbeitsaufgabe der Warteschlange für dies später hinzugefügt. Hier wird die vollständige Signatur der Methode:

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a>Parameter

**ID-Typ**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_

Der Typ der Id, die bei der Suche nach dem Benutzerprofil verwendet. Mögliche Werte sind `Email`, `CloudId`, und `PrincipalName`. Beachten Sie, dass unabhängig von der Art der Benutzer in der Benutzerprofildienst für den Import arbeiten bereits vorhanden sein. Es wird empfohlen, verwenden Sie die `CloudId` um Eindeutigkeit zu gewährleisten.

Zuordnung zwischen ID-Typ und Azure AD-Eigenschaft:

UPA Bulk Import-ID-Typ | Azure-Directory-Attribut
--- | ---
CloudId | ObjectID
' PrincipalName ' | userPrincipalName
E-Mail | mail

**SourceDataIdProperty**:_`System.String`_

Der Name der Id-Eigenschaft in den Quelldaten. Der Wert der Eigenschaft aus der Datenquelle wird den Benutzer nachschlagen verwendet werden. Die für die Suche zu verwendenden Benutzerprofildienst-Eigenschaft hängt vom Wert der `idType`.

**PropertyMap**:_`IDictionary<string, string>`_

Eine Zuordnung aus der Name der Eigenschaft auf den Namen der Benutzerprofildienst-Eigenschaft. Beachten Sie, dass die Benutzerprofildienst-Eigenschaften bereits vorhanden sein müssen. Der Schlüssel ist der Name der Eigenschaft in der Quelldatei verwendet, der Wert ist der Name der Eigenschaft, die in der Benutzerprofildienst verwendet.

**SourceUri**:_`System.String`_

Der URI der Quelldatei Daten zu importieren. Die Datei sollte nicht verschoben oder sofort gelöscht werden, da er für einige Zeit nicht heruntergeladen werden kann.

#### <a name="return-value"></a>Return value
Eine Guid, die den Importauftrag identifiziert, der in die Warteschlange gestellt wurde.

#### <a name="example"></a>Beispiel
Es folgt ein Beispiel zur Verwendung von C#-dafür, wie Sie den Prozess, indem die oben genannten Beispiel-Eingabedatei starten:

```c#
// Create an instance of the Office 365 Tenant object. Loading this object is not technically needed for this operation. 
Office365Tenant tenant = new Office365Tenant(ctx);
ctx.Load(tenant);
ctx.ExecuteQuery();

// Type of user identifier ["PrincipalName", "Email", "CloudId"] in the 
// User Profile Service. In this case, we use Email as the identifier at the UPA storage
ImportProfilePropertiesUserIdType userIdType = 
      ImportProfilePropertiesUserIdType.Email;

// Name of the user identifier property within the JSON file
var userLookupKey = "IdName";

var propertyMap = new System.Collections.Generic.Dictionary<string, string>();

// The key is the property in the JSON file, 
// The value is the user profile property Name in the User Profile Service
// Notice that we have 2 custom properties in UPA called 'City' and 'OfficeCode'
propertyMap.Add("City", "City");
propertyMap.Add("Office", "OfficeCode");

// Returns a GUID which can be used to check the status of the execution and the end results
var workItemId = tenant.QueueImportProfileProperties(
      userIdType, userLookupKey, propertyMap, fileUrl
      );

ctx.ExecuteQuery();
```

### <a name="check-the-status-of-an-import-job"></a>Überprüfen Sie den Status eines Auftrags für den Import
Sie können auch den Status der Benutzerprofildienst-Importaufträge suchen, mithilfe der neuen CSOM-APIs. Es gibt zwei neue Methoden für dieses im Mandanten-Objekt.

Sie können ein einzelnes Importauftrag Status überprüfen, mithilfe der [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) Methode befindet sich der [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) Objekt. Sie müssen den eindeutigen Bezeichner eines bestimmten importieren Auftrag als Parameter an diese Methode bereitgestellt haben. Hier wird die vollständige Signatur der Methode:

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a>Parameter
**JobID**:_`System.Guid`_

Die Id des Auftrags, für den den allgemeinen Status abzurufen.

#### <a name="return-value"></a>Return value

Ein [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) -Objekt mit Informationen über den angegebenen Auftrag Statusbericht.

#### <a name="example"></a>Beispiel
Im folgenden ist ein Beispiel für c# zum Abrufen von den Status einer bestimmten Importauftrag mit einer gespeicherten-ID verwenden:

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

Überprüfen des Status aller Importaufträge können mithilfe von der [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) Methode befindet sich im [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) -Objekt. Hier wird die vollständige Signatur der Methode:

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a>Return value
Ein [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) Objekt eine Sammlung von [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Objekte mit Informationen zu den einzelnen der Aufträge Statusbericht.

#### <a name="example"></a>Beispiel
Im folgenden ist ein Beispiel für c# Abrufen von den Status aller Import Aufträge, die derzeit im Mandanten gespeichert verwenden. Diese bereits verarbeitet werden konnte oder Aufträge in der Warteschlange:

```c#
// Load all import jobs – old and queued ones
Office365Tenant tenant = new Office365Tenant(ctx);
var jobs = tenant.GetImportProfilePropertyJobs();
ctx.Load(jobs);
ctx.ExecuteQuery();
foreach (var item in jobs)
{
   // Check whatever properties needed
   var state = item.State;
}
```

Ein [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) die Statusinformationen Import zurückgegebene Objekt hat die folgenden Eigenschaften. 

**JobId**:_`System.Guid`_

Die Id des den Importauftrag

**Status**:_[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_

Eine Enumeration mit der folgenden Werte:
- `Unknown`-Es kann den Status des Auftrags nicht ermitteln.
- `Submitted`– Der Auftrag wurde an das System übermittelt
- `Processing`-Der Auftrag wird verarbeitet
- `Queued`-Der Auftrag hat erfolgreich validiert wurde und in der Warteschlange für den Import in UPA
- `Succeeded`– Der Auftrag abgeschlossen ohne Fehlermeldung
- `Error`– Der Auftrag abgeschlossen

**SourceUri**:_`System.String`_

Der URI der Quelldatei Daten

**Fehler**:_[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_

Eine Enumeration, den möglichen Fehler darstellt:
- `NoError`-Keine Fehler gefunden
- `InternalError`– Durch einen Fehler im Dienst wurde der Fehler verursacht.
- `DataFileNotExist`-Die Datenquelldatei konnte nicht gefunden werden
- `DataFileNotInTenant`-Die Datenquelldatei nicht zu derselben mandantenorganisation gehören.
- `DataFileTooBig`-Die Größe der Datendatei war zu groß
- `InvalidDataFile`-Die Datenquelldatei bestanden nicht Überprüfung (möglicherweise zusätzliche Details in der Protokolldatei)
- `ImportCompleteWithError`-Die Daten importiert, aber es wurde ein Fehler aufgetreten

**ErrorMessage**:_`System.String`_

Die Fehlermeldung

**LogFileUri**:_`System.String`_

Der Uri, der den Ordner, in dem die Protokolle geschrieben wurden

## <a name="calling-the-import-api-from-powershell"></a>Aufrufen des Imports-API in PowerShell
<a name="sectionSection4"> </a>

Sie können die Benutzerprofildienst-Bulk Import-API mit PowerShell nutzen. Dies bedeutet, dass Sie den CSOM-Code direkt in einer PowerShell-Skript mit den erforderlichen Parametern verwenden. Dies erfordert, dass das aktualisierte CSOM redistributable-Paket auf dem Computer installiert ist, auf dem das Skript ausgeführt wird.

Mithilfe von PowerShell, müssen Sie nicht Kompilieren des Codes in Visual Studio, die möglicherweise ein Modell besser geeignet für einige Kunden.

### <a name="sample-powershell-script"></a>PowerShell-Beispielskript
Im folgenden finden Sie ein PowerShell-Beispielskript die die gleichen Vorgänge als dem oben angegebenen Code ausführt: 

```Powershell
# Get needed information from the end user
$adminUrl = Read-Host -Prompt 'Enter the admin URL of your tenant'
$userName = Read-Host -Prompt 'Enter your user name'
$pwd = Read-Host -Prompt 'Enter your password' -AsSecureString
$importFileUrl = Read-Host -Prompt 'Enter the URL to the file located in your tenant'

# Get instances to the Office 365 tenant using CSOM
$uri = New-Object System.Uri -ArgumentList $adminUrl
$context = New-Object Microsoft.SharePoint.Client.ClientContext($uri)

$context.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($userName, $pwd)
$o365 = New-Object Microsoft.Online.SharePoint.TenantManagement.Office365Tenant($context)
$context.Load($o365)

# Type of user identifier ["Email", "CloudId", "PrincipalName"] in the User Profile Service
$userIdType=[Microsoft.Online.SharePoint.TenantManagement.ImportProfilePropertiesUserIdType]::Email

# Name of user identifier property in the JSON
$userLookupKey="idName"

# Create property mapping between the source file property name and the O365 property name
# Notice that we have here 2 custom properties in UPA called 'City' and 'OfficeCode'
$propertyMap = New-Object -type 'System.Collections.Generic.Dictionary[String,String]'
$propertyMap.Add("City", "City")
$propertyMap.Add("Office", "OfficeCode")

# Call to queue UPA property import 
$workItemId = $o365.QueueImportProfileProperties($userIdType, $userLookupKey, $propertyMap, $importFileUrl);

# Execute the CSOM command for queuing the import job
$context.ExecuteQuery();

# Output the unique identifier of the job
Write-Host "Import job created with the following identifier:" $workItemId.Value 
```

## <a name="handling-exceptions"></a>Behandeln von Ausnahmen
<a name="sectionSection5"></a> Stehen zwei Stufen der Überprüfung wird, wenn diese API verwendet wird. Wenn Sie den Importvorgang mit CSOM in die Warteschlange wird eine erste Ebene der Überprüfung der bereitgestellten Werte vorhanden sein. Dazu gehören zur Bestätigung, dass die bereitgestellten Zuordnungseigenschaften in der Benutzerprofildienst vorhanden sind und diese Eigenschaften nicht vom Benutzer bearbeitet werden. Wenn die Warteschlange API aufgerufen wird, wird nur eine erste Ebene der Überprüfung angewendet und endgültige Überprüfung der bereitgestellten Informationen erfolgt bei der Importauftrag tatsächlich ausgeführt wird.

Wenn während der Ausführung des tatsächlichen Importvorgangs für alle Ausnahmen sind, wird eine Protokolldatei mit zusätzlichen Einzelheiten in derselben Dokumentbibliothek generiert, in dem die Importdatei gefunden wurde. Protokolldateien für bestimmte Importaufträge werden gespeichert, um eine sub-Ordnern mit dem eindeutigen Bezeichner des Auftrags für bestimmte importieren.

Es folgt ein Beispiel für die Ergebnisse der Ausführung ein Importauftrag. In der folgenden Abbildung sehen Sie zwei Unterordner für zwei unterschiedliche Ausführungen erstellt in der Dokumentbibliothek, in dem die Importdatei gespeichert ist:

![Job-Ausnahme Unterordner](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

Die aktuelle Protokolldatei wird im Ordner "Sub" gespeichert und können Sie Herunterladen von Office 365 für die detaillierte Analyse:

![Job-Ausnahme-Protokolldatei](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a>Allgemeine Ausnahmen

In der folgenden Tabelle enthält die typische Ausnahmen aus, die Sie auftreten können, wenn Sie beginnen, mit der Benutzerprofildienst-Bulk-API.

Beispiel-Ausnahme | Details
--- | ---
_Eigenschaftennamen [mich-Seite] können vom Benutzer bearbeitet werden._ | Dies beim Aufruf von CSOM-API ausgelöst werden würde der `ExecuteQuery` -Methode, wenn Sie den Auftrag an Ihrem Mandanten zu senden. Die API wird überprüft, dass alle derzeit zugeordnete Eigenschaften nicht Benutzer bearbeitet werden. Die Ausnahme wird, die-Eigenschaft verweisen, die nicht verwendet werden kann. In diesem Beispiel haben wir versucht, eine JSON-Eigenschaft zum Zuordnen der `AboutMe` -Eigenschaft in die Benutzerprofildienst-Eigenschaften, aber dies ist nicht zulässig, seit `AboutMe` ist eine Benutzereigenschaft bearbeitet werden.
_InvalidProperty - Eigenschaft 'Mich-Seite' vesaj@contoso.com ist, eine Eigenschaft in der Benutzerprofildienst-Anwendung nicht zugeordnet._ | Die Datendatei JSON enthalten eine Eigenschaft, die zur Benutzerprofildienst-Eigenschaft in SharePoint Online nicht zugeordnet wurde. Dies bedeutet, dass die Quelldatendatei Eigenschaften enthält, für die Sie eine Zuordnung in nicht bereitgestellt haben, die `propertyMap` Parameter. Sie müssen für jede der Eigenschaften in das JSON-Objekt eine Zuordnungsdefinition verfügen.
_MissingIdentity - fehlt die Identität für das Benutzerobjekt_ | Die Identity-Eigenschaft konnte nicht in das Benutzerobjekt gefunden werden. Meistens verursachen, die die `sourceDataIdProperty` -Attribut wird fälschlicherweise festgelegt, für die `QueueImportProfileProperties` Methode. Stellen Sie sicher, dass Sie die right-Eigenschaft in der Quelldatei JSON haben und Ihr Code/Skript entsprechend dieses Attribut zugewiesen ist.
_IdentityNotResolvable unknown@contoso.com Benutzeridentität kann nicht aufgelöst werden_ | Die Datendatei, die eine Identität, die nicht aufgelöst werden kann oder ist nicht vorhanden, in dem der Benutzerprofildienst enthalten sind. In diesem Fall konnte das Benutzerprofil mit e-Mail-Adresse des _unknown@contoso.com_ nicht in der Benutzerprofildienst befinden.
_DataFileNotJson - JsonToken EndObject ist nicht gültig für JsonType Array zu schließen. Pfad "Wert", Zeile 8, position 10._ | Format der Importdatei ist keine gültige JSON und das erwartete Format stimmt nicht überein. 

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
<a name="sectionSection6"> </a>

**Kann den app-only/Add-in-Berechtigungen mit Code werden ausgeführt?**

Ja, müssen Sie die Client-Id und geheimen Clientschlüssel werden sollen, führen Sie die APIs registrieren. Da der tatsächliche Import der Datei mit der Identität des Aufrufers nicht synchron auftritt, funktioniert dies ohne Probleme.

**Diese API ist Aktualisieren von Eigenschaften in den Benutzerprofildienst, doch wie würde ich diese Eigenschaften im Mandanten erstellen?**

Es ist keine remote-API, um benutzerdefinierte Profileigenschaften programmgesteuert erstellen Dies manuelle Verarbeitung der angegebenen Mandanten einmal pro ausgeführt werden muss. Sie können Sie [in diesem Artikel](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) eine Anleitung zum Erstellen dieser benutzerdefinierten Eigenschaften verweisen.

**Ist diese Funktion in lokalen SharePoint?**

Diese Funktion ist leider derzeit nur für SharePoint Online. In der lokalen SharePoint würden diese Funktion nützlich, aber nicht als kritisch sein, da die Zuordnung Attribut in die lokale Benutzerprofildienst-Anwendung geändert werden können. Sie können auch Importieren von Benutzerprofil-Attribute von Business Connectivity Service (BCS) in SharePoint 2013 nutzen. Jedoch ist diese Option nicht verfügbar in SharePoint 2016, was bedeutet, dass für SharePoint 2016 die einzige Option derzeit ist Anpassungen Implementieren des Benutzers Profil Webdienste nutzen.

**Konnte diese API werden verwendet, für das Synchronisieren von Benutzerprofil Eigenschaftswerte über meine lokalen SharePoint 2013 oder 2016 Mastbetriebs mit SharePoint Online?**
Ja, kann der lokale SharePoint genau wie alle anderen Quellsystem verwendet werden. Sie müssen die Benutzerprofil Werte aus Ihrer lokalen SharePoint das JSON-Dateiformat exportieren und klicken Sie dann der Prozess wäre genau das Importieren von Werten aus einem anderen System identisch.

**Kann ich Zeichenfolge basiert, mehrwertige Eigenschaften Importieren?**
Nein, ist dies nicht aktuell mit diese API unterstützt.

**Welche Berechtigungen sind zum Ausführen dieser API? erforderlich?**
Sie müssen derzeit globaler Administrator-Berechtigungen verfügen. SharePoint Admin ist nicht ausreichend.

**Kann ich die Taxonomie basierende Eigenschaften Importieren?**
Nein, ist dies nicht aktuell mit diese API unterstützt.

**Was passiert, wenn ich definieren eine Zuordnung, in der Code, der nicht verwendet wird oder Eigenschaften in der JSON-Datei, die nicht zugeordnet werden?**
Wenn Ihr Code/Skript definiert eine Zuordnung, die nicht verwendet wird oder die Datendatei keine Eigenschaften für die Zuordnung enthält, die Ausführung ohne Ausnahmen fortgesetzt wird und der Import wird angewendet werden soll, basierend auf den zugeordneten Eigenschaften. Wenn Sie, jedoch eine Eigenschaft in der Datei JSON, die nicht zugeordnet ist verfügen, wird der Importvorgang abgebrochen werden, und Details der Ausnahme in der Protokolldatei für die Ausführung des Auftrags bestimmte bereitgestellt werden.

**Was geschieht, wenn ich muss eine benutzerdefinierte Eigenschaften zu aktualisieren, die die Größe Einschränkungen dieser Massen API sprengen (d. h. > 2 GB-Datei oder > 500.000 Eigenschaften)?**
Sie müssen Ihre Aufträge auslösen entsprechend durch mehrere Aufträge in der Abfolge (d. h. einem Auftrag zu einem Zeitpunkt mit der maximale Grenzwert für diese API Enddatum) Batch. Sie sollten erwarten, diese hoher Bandbreite Imports eine lange dauern werden. Darüber hinaus sollten Sie die Importaufträge nur für Delta Änderungen benutzerdefinierter Profileigenschaften, sondern eine umfassende Auswahl an Werte in allen Projekten importieren in optimieren.

**Welche Azure Active Directory-Attribute sind Sync wird standardmäßig SharePoint Online Benutzerprofil mussten?**
Finden Sie in der folgenden Tabelle für die offizielle Liste der synchronisierten Attribute und deren Zuordnung zwischen Azure Active Directory und SharePoint Online User Profile Service.

Azure-Directory-Attribut  | SharePoint Online-Profileigenschaft
---------|----------
Objekt-SID | SPS-SavedSID
MSOnline UserPrincipalName | Benutzername
MSOnline UserPrincipalName | Kontoname
MSOnline UserPrincipalName | SPS-ClaimID
MSOnline UserPrincipalName | SPS-UserPrincipalName
Vorname | Vorname
Sn | Nachname
Manager | Manager
DisplayName | PreferredName
telephoneNumber | WorkPhone
Proxyadressen | WorkEmail
Proxyadressen | SPS-"SipAddress"
PhysicalDeliveryOfficeName | Office
Titel | Titel
Titel | SPS-JobTitle
Abteilung | Abteilung
Abteilung | SPS-Abteilung
Objekt-GUID | ADGuid
WWWHomePage | PublicSiteRedirect
DistinguishedName | SPS-DistinguishedName
MsOnline-ObjectId | MsOnline-ObjectId
PreferredLanguage | SPS-"MUILanguages"
msExchHideFromAddressList | SPS-HideFromAddressLists
msExchRecipientTypeDetails | SPS-"RecipientTypeDetails"
MSOnline groupType | IsUnifiedGroup
MsOnline IsPublic | IsPublic
MsOnline-ObjectId | MsOnline-ObjectId
MsOnline UserType | SPS-Benutzertyp
GroupType | GroupType
SPO-IsSharePointOnlineObject | SPO-IsSPO

