<span data-ttu-id="d89f2-p128">Nachdem die Daten geladen wurden, werden sie in der globalen Variable **loadedData** gespeichert. Der Wert der Variablen **loadingData** wird auf **false** festgelegt, und das Versprechen wird mit den abgerufenen Daten aufgelöst. Das nächste Mal, wenn ein Webpart seine Daten anfordert, gibt der Datendienst die zuvor geladenen Daten zurück, wodurch alle Anforderungen an die Remote-APIs gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="d89f2-p128">Once the data is loaded, it is stored in the **loadedData** global variable. The value of the **loadingData** variable is set to **false** and the promise is resolved with the retrieved data. The next time a web part requests its data, the data service will return the data loaded previously eliminating any requests to the remote APIs.</span></span>

Nachdem die Daten geladen wurden, werden sie in der globalen Variable **loadedData** gespeichert. Der Wert der Variablen **loadingData** wird auf **false** festgelegt, und das Versprechen wird mit den abgerufenen Daten aufgelöst. Das nächste Mal, wenn ein Webpart seine Daten anfordert, gibt der Datendienst die zuvor geladenen Daten zurück, wodurch alle Anforderungen an die Remote-APIs gelöscht werden.

<span data-ttu-id="d89f2-264">Bestätigen Sie, dass beide Webparts ordnungsgemäß arbeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="d89f2-264">Confirm, that both web parts are working correctly, by running the following command:</span></span>

```sh
gulp serve
```

![Die Webparts „Zuletzt verwendetes Dokument“ und „Zuletzt verwendete Dokumente“ zeigen Informationen zu den zuletzt geänderten Dokumenten an](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

<span data-ttu-id="d89f2-266">Wenn Sie in den verschiedenen Bereichen der **DocumentsService.ensureRecentDocuments**-Methode Protokollierungsanweisungen hinzugefügt haben, würden Sie sehen, dass die Daten einmal geladen und für das zweite Webpart wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d89f2-266">If you added logging statements in the different parts of the **DocumentsService.ensureRecentDocuments** method, you would see, that the data is loaded once and reused for the second web part.</span></span>

![Entwicklerkonsole, in der unterschiedliche Protokollierungsanweisungen in Microsoft Edge angezeigt werden](../../../../images/tutorial-sharingdata-console-log.png)

## <a name="see-also"></a><span data-ttu-id="d89f2-268">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d89f2-268">See also</span></span>

- [<span data-ttu-id="d89f2-269">Gemeinsame Verwendung von Daten zwischen clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="d89f2-269">Share data between client-side web parts</span></span>](./share-data-between-web-parts)