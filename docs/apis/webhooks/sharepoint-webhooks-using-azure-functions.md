<span data-ttu-id="0aa3c-p109">Zur Vermeidung der unbefugten Verwendung Ihrer Azure-Funktion muss der Anrufer einen Code eingeben, wenn er die Funktion aufruft. Dieser Code kann über den Bildschirm **Verwalten** abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="0aa3c-p109">To avoid unathorized usage of your Azure Function the caller will need to specify a code when calling your function. This code can be retreived via the **Manage** screen:</span></span>](../../../images/webhook-azure-function8.png)

Zur Vermeidung der unbefugten Verwendung Ihrer Azure-Funktion muss der Anrufer einen Code eingeben, wenn er die Funktion aufruft. Dieser Code kann über den Bildschirm **Verwalten** abgerufen werden:

![Webhook-URL der Azure-Funktion](../../../images/webhook-azure-function7.png)

<span data-ttu-id="0aa3c-142">In unserem Fall lautet die zu verwendende Webhook-URL also wie folgt: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span><span class="sxs-lookup"><span data-stu-id="0aa3c-142">So in our case the webhook URL to use is the following: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span></span>



