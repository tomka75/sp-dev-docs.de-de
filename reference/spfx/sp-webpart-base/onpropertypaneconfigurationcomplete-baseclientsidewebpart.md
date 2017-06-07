# <a name="onpropertypaneconfigurationcomplete"></a>onPropertyPaneConfigurationComplete()




Diese API wird aufgerufen, wenn die Konfiguration im PropertyPane abgeschlossen ist. Sie wird in den folgenden Fällen aufgerufen: – Wenn CONFIGURATION_COMPLETE_TIMEOUT (der aktuelle Wert beträgt 5 Sekunden) nach der letzten Änderung abläuft. – Wenn der Benutzer auf die Schaltfläche 'x' (Schließen) klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer auf „Anwenden“ klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer Webparts wechselt, erhält das aktuelle Webpart dieses Ereignis.

**Signatur:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter
Keine


