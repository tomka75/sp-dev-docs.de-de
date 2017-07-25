<span data-ttu-id="c10bd-p123">Dieses Projekt schreibt die Informationen nur ins Ablaufprotokoll. Im Empfänger werden die Informationen jedoch an eine Tabelle oder eine Warteschlange gesendet, die die empfangenen Daten verarbeiten und die von SharePoint gesendeten Informationen auswerten kann.</span><span class="sxs-lookup"><span data-stu-id="c10bd-p123">This project just writes the information to the trace log. However, in your receiver, you will send this information into a table or a queue that can process the received data to get information from SharePoint.</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Resource: c34420f9-2a67-4e54-94c9-b6770892299b'
    iisexpress.exe Information: 0 : Message='SubscriptionId: 32b95ad9-4d20-4a17-bfa3-2957cb38ead8'
    iisexpress.exe Information: 0 : Message='TenantId: 7a17cb7d-6898-423f-8839-45f363076f06'
    iisexpress.exe Information: 0 : Message='SiteUrl: /'
    iisexpress.exe Information: 0 : Message='WebId: 62b80e0b-f889-4974-a519-cc138413be40'
    iisexpress.exe Information: 0 : Message='ExpirationDateTime: 2016-10-27T16:17:57.0000000Z'
    ```

Dieses Projekt schreibt die Informationen nur ins Ablaufprotokoll. Im Empfänger werden die Informationen jedoch an eine Tabelle oder eine Warteschlange gesendet, die die empfangenen Daten verarbeiten und die von SharePoint gesendeten Informationen auswerten kann. 

<span data-ttu-id="c10bd-282">Mit diesen Daten können Sie die URL erstellen und über die [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges)-API die neuesten Änderungen abrufen.</span><span class="sxs-lookup"><span data-stu-id="c10bd-282">With this data, you can construct the URL and use the [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) API to get the latest changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c10bd-283">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c10bd-283">Next steps</span></span>

<span data-ttu-id="c10bd-284">In diesem Artikel haben Sie mithilfe des Postman-Clients und einer einfachen Web-API Webhook-Benachrichtigungen von SharePoint abonniert und empfangen.</span><span class="sxs-lookup"><span data-stu-id="c10bd-284">In this article, you used Postman client and a simple web API to subscribe and receive webhook notifications from SharePoint.</span></span>

<span data-ttu-id="c10bd-285">Sehen Sie sich als nächstes die [Beispielreferenzimplementierung für SharePoint-Webhooks](./webhooks-reference-implementation) an. Sie gibt ein End-to-End-Beispiel, das Azure-Speicherwarteschlangen verwendet, um die Informationen zu verarbeiten, Änderungen von SharePoint abzurufen und diese Änderungen an eine SharePoint-Liste zurückzusenden.</span><span class="sxs-lookup"><span data-stu-id="c10bd-285">Next, take a look at [SharePoint webhooks sample reference implementation](./webhooks-reference-implementation), which shows an end-to-end sample that uses Azure Storage Queues to process the information, get changes from SharePoint, and push those changes back into a SharePoint list.</span></span>
