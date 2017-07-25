<span data-ttu-id="e1dc5-p101">Diese API wird aufgerufen, wenn die Konfiguration im PropertyPane abgeschlossen ist. Sie wird in den folgenden Fällen aufgerufen: – Wenn CONFIGURATION_COMPLETE_TIMEOUT (der aktuelle Wert beträgt 5 Sekunden) nach der letzten Änderung abläuft. – Wenn der Benutzer auf die Schaltfläche 'x' (Schließen) klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer auf „Anwenden“ klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer Webparts wechselt, erhält das aktuelle Webpart dieses Ereignis.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-p101">This API is invoked when the configuration is completed on the PropertyPane. It's invoked in the following cases: - When the CONFIGURATION_COMPLETE_TIMEOUT((currently the value is 5 secs) elapses after the last change. - When user clicks 'x'(close) button before the CONFIGURATION_COMPLETE_TIMEOUT elapses. - When user clciks 'Apply' button before the CONFIGURATION_COMPLETE_TIMEOUT elapses. - When the user switches web parts then the current web part gets this event.</span></span>




Diese API wird aufgerufen, wenn die Konfiguration im PropertyPane abgeschlossen ist. Sie wird in den folgenden Fällen aufgerufen: – Wenn CONFIGURATION_COMPLETE_TIMEOUT (der aktuelle Wert beträgt 5 Sekunden) nach der letzten Änderung abläuft. – Wenn der Benutzer auf die Schaltfläche 'x' (Schließen) klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer auf „Anwenden“ klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer Webparts wechselt, erhält das aktuelle Webpart dieses Ereignis.

<span data-ttu-id="e1dc5-107">**Signatur:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_</span><span class="sxs-lookup"><span data-stu-id="e1dc5-107">**Signature:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_</span></span>

<span data-ttu-id="e1dc5-108">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="e1dc5-108">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="e1dc5-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="e1dc5-109">Parameters</span></span>
<span data-ttu-id="e1dc5-110">Keine</span><span class="sxs-lookup"><span data-stu-id="e1dc5-110">None</span></span>


