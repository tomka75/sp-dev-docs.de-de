<span data-ttu-id="57ad9-p147">Viele clientseitige Anpassungen verwenden jQuery zur Ausführung von AJAX-Anforderungen, aufgrund seiner Einfachheit und seiner browserübergreifenden Kompatibilität. Falls Sie jQuery nur dafür verwenden: Sie können AJAX-Aufrufe auch über den Standard-HTTP-Client von SharePoint Framework ausführen. SharePoint Framework bietet zwei Typen von HTTP-Clients: [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient) zur Ausführung von Anforderungen an die SharePoint-REST-API und [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient) zur Ausgabe von Webanforderungen an andere REST-APIs. Einen Aufruf mit SPHttpClient zum Abrufen des Titels der aktuellen SharePoint-Website würden Sie wie folgt ausführen:</span><span class="sxs-lookup"><span data-stu-id="57ad9-p147">Many client-side customizations use jQuery for executing AJAX requests for its simplicity and cross-browser compatibility. If this is all that you're using jQuery for, you can execute the AJAX calls using the standard HTTP client provided with the SharePoint Framework. SharePoint Framework offers you two types of HTTP client: the [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient), meant for executing requests to the SharePoint REST API, and the [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient) designed for issuing web requests to other REST APIs. Here is how you would execute a call using the SPHttpClient to get the title of the current SharePoint site:</span></span>

Viele clientseitige Anpassungen verwenden jQuery zur Ausführung von AJAX-Anforderungen, aufgrund seiner Einfachheit und seiner browserübergreifenden Kompatibilität. Falls Sie jQuery nur dafür verwenden: Sie können AJAX-Aufrufe auch über den Standard-HTTP-Client von SharePoint Framework ausführen. SharePoint Framework bietet zwei Typen von HTTP-Clients: [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient) zur Ausführung von Anforderungen an die SharePoint-REST-API und [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient) zur Ausgabe von Webanforderungen an andere REST-APIs. Einen Aufruf mit SPHttpClient zum Abrufen des Titels der aktuellen SharePoint-Website würden Sie wie folgt ausführen:

```ts
this.context.spHttpClient.get(`${this.context.pageContext.web.absoluteUrl}/_api/web?$select=Title`,
SPHttpClient.configurations.v1,
{
  headers: {
    'Accept': 'application/json;odata=nometadata',
    'odata-version': ''
  }
})
.then((response: SPHttpClientResponse): Promise<{Title: string}> => {
  return response.json();
})
.then((web: {Title: string}): void => {
  // web.Title
}, (error: any): void => {
  // error
});
```

## <a name="more-information"></a><span data-ttu-id="57ad9-271">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="57ad9-271">More information</span></span>

- [<span data-ttu-id="57ad9-272">Migrate SharePoint JavaScript customizations to SharePoint Framework - reference functions from script files</span><span class="sxs-lookup"><span data-stu-id="57ad9-272">Migrate SharePoint JavaScript customizations to SharePoint Framework - reference functions from script files</span></span>](https://blog.mastykarz.nl/migrate-sharepoint-javascript-customizations-sharepoint-framework-reference-functions/)
- [<span data-ttu-id="57ad9-273">Migrate SharePoint JavaScript customizations to SharePoint Framework – jQuery AJAX calls and showing data</span><span class="sxs-lookup"><span data-stu-id="57ad9-273">Migrate SharePoint JavaScript customizations to SharePoint Framework – jQuery AJAX calls and showing data</span></span>](https://rencore.com/blog/migrate-sharepoint-javascript-customizations-to-sharepoint-framework-jquery-ajax-calls-and-showing-data/)
