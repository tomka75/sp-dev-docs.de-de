# <a name="accessing-sharepoint-using-an-application-context-also-known-as-app-only"></a>Zugreifen auf SharePoint mit einem Anwendungskontext, auch bekannt als nur-app-

Es gibt zwei Ansätze für dadurch-nur-app für SharePoint: 
 - Mit einer **Azure AD-Anwendung**: Dies ist die bevorzugte Methode, wenn Sie SharePoint Online verwenden, da Sie auch mit anderen Office 365-Diensten Berechtigungen gewähren können (falls erforderlich) + haben eine Benutzeroberfläche (Azure-Verwaltungsportal) für Ihre app-Prinzipalen verwalten.
 - Verwenden eines **SharePoint-nur-App - Prinzipal**: Diese Methode ist die Funktionsweise der älteren und nur für den Zugriff auf SharePoint, aber immer noch relevant ist. Diese Methode ist auch empfohlen, wenn Sie noch in SharePoint lokal arbeiten, da dieses Modell in SharePoint lokal als SharePoint Online arbeitet.

Beide Methoden werden in den folgenden Artikeln beschrieben: 
 - [Gewähren des Zugriffs über App-Only Azure AD](security-apponly-azuread.md)
 - [Gewähren des Zugriffs von SharePoint-App-Only](security-apponly-azureacs.md)

## <a name="what-are-the-limitations-when-using-app-only"></a>Was sind die Einschränkungen bei Verwendung der nur-app-
Nur-App-funktioniert nicht in folgenden Fällen:
 - Aktualisieren der Taxonomie Diensteinträge (Schreiben) - Works lesen
 - Erstellen moderner Teamwebsites unterstützt keine nur-app-Wenn Sie es [mithilfe der SharePoint-API](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Sites/SiteCollection.cs) . Bei modernen Teamwebsites zum Erstellen der Gruppe dann nur-app- [Hilfe von Microsoft Graph](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs) erstellt werden, ist kein unterstütztes Szenario
 - Erstellen von kommunikationswebsites derzeit unterstützt nicht nur-app- [Verwenden der SharePoint-API](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Sites/SiteCollection.cs)
 - Suchen Sie bei Verwendung von lokalem SharePoint. SharePoint Online-Unterstützung wurden ([Blogbeitrag](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)) hinzugefügt
 - Profil CSOM Benutzervorgänge, mit der Ausnahme, dass der Benutzerprofil Bulk Update-API mit nur-app-Berechtigungen verwendet werden können
 - Bearbeiten von Dateien über WebDav-Protokoll und CSOM (mit `File.SaveBinaryDirect`) funktioniert nicht mit nur-app-

> [!IMPORTANT]
> Wenn die oben beschriebenen Szenarien für Sie wichtig sind hat empfohlen, ein Dienstkonto definieren, dass eine Berechtigungen erteilen, und klicken Sie dann in der Anwendung verwenden. Finden Sie das [Governance.EnsurePolicy](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.EnsurePolicy) Beispiel erfahren Sie mehr auf, wie Sie die Mandanten für ein Dienstkonto Breite Berechtigungen gewähren können. Außerdem enthält Artikel erklärt, ein [alternatives Modell zum Web app-Richtlinien in SharePoint Online](security-webapppolicies.md) eine Vielzahl von Informationen zu diesem Thema.



