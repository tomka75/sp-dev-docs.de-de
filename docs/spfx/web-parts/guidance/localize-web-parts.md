<span data-ttu-id="e78a4-p145">Beim Laden des Webparts auf der Seite lädt das SharePoint Framework automatisch die Ressourcendatei für das entsprechende Gebietsschema, indem es die Informationen von der Kontext-Website verwendet. Wenn keine übereinstimmende Ressourcendatei gefunden wird, lädt das SharePoint Framework die in der **efaultPath**Eigenschaft angegebene Datei. Durch die Trennung der Ressourcendateien minimiert das SharePoint Framework die auf der Seite für das Gebietsschema geladenen Datenmenge, das mit dem auf der Website verwendeten Gebietsschema übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="e78a4-p145">When loading the web part on the page, the SharePoint Framework will automatically load the resource file for the corresponding locale by using the information from the context site. If no matching resource file is found, the SharePoint Framework will load the file specified in the **defaultPath** property. By keeping the resource files separate, the SharePoint Framework minimizes the amount of data loaded on the page to the locale that matches the one used in the site.</span></span>

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting.bundle",
    "internalModuleBaseUrls": [
      "https://cdn.contoso.com/"
    ],
    "scriptResources": {
      "greeting.bundle": {
        "type": "internal",
        "path": "greeting.bundle_734e78a24ec5779bbc7a5a10603d4904.js"
      },
      "greetingStrings": {
        "defaultPath": "react-localization-greetingstrings_en-us_60a6b3dba7cc244bcc28781a2e292f85.js",
        "type": "localized",
        "paths": {
          "en-US": "react-localization-greetingstrings_en-us_60a6b3dba7cc244bcc28781a2e292f85.js",
          "nl-NL": "react-localization-greetingstrings_nl-nl_ecae5f3385f9e9bef23817b91d1a0bf1.js",
          "qps-ploc": "react-localization-greetingstrings_qps-ploc_dc97c611a9edc88818c84871f3749afb.js"
        }
      },
      // ...
    }
  }
}
```

Beim Laden des Webparts auf der Seite lädt das SharePoint Framework automatisch die Ressourcendatei für das entsprechende Gebietsschema, indem es die Informationen von der Kontext-Website verwendet. Wenn keine übereinstimmende Ressourcendatei gefunden wird, lädt das SharePoint Framework die in der **efaultPath**Eigenschaft angegebene Datei. Durch die Trennung der Ressourcendateien minimiert das SharePoint Framework die auf der Seite für das Gebietsschema geladenen Datenmenge, das mit dem auf der Website verwendeten Gebietsschema übereinstimmt.