<span data-ttu-id="6ec73-p113">Geben Sie dann“ gulp serve“ auf der Konsole ein, um die lokale Workbench anzuzeigen, die jetzt mit den simulierten Daten arbeitet. (Falls der Server bereits ausgeführt wird, halten Sie ihn mit STRG + C an, und starten Sie ihn dann erneut)</span><span class="sxs-lookup"><span data-stu-id="6ec73-p113">Finally type gulp serve in the console to bring up the local workbench, which now will work with the mock data. (If you already have the server running stop it using Ctrl+C and then restart it)</span></span>

```TypeScript
private _registerComponent(tagName: string): void {

  if (Environment.type === EnvironmentType.Local) {
    console.log("here I am.")
    ko.components.register(
      tagName,
      {
        viewModel: MockSpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  } else {
    ko.components.register(
      tagName,
      {
        viewModel: SpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  }
}
```
Geben Sie dann“ gulp serve“ auf der Konsole ein, um die lokale Workbench anzuzeigen, die jetzt mit den simulierten Daten arbeitet. (Falls der Server bereits ausgeführt wird, halten Sie ihn mit STRG + C an, und starten Sie ihn dann erneut)

```sh
gulp serve
```

![Angezeigtes Projekt, das in der lokalen Workbench mit simulierten Daten ausgeführt wird](../../../../images/sp-pnp-js-guide-with-mock-data.png)


## <a name="download-full-example-code"></a><span data-ttu-id="6ec73-169">Herunterladen des vollständigen Beispielcodes</span><span class="sxs-lookup"><span data-stu-id="6ec73-169">Download Full Example Code</span></span>

<span data-ttu-id="6ec73-170">Zur Erinnerung: Sie finden Sie das vollständige Beispiel [hier](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span><span class="sxs-lookup"><span data-stu-id="6ec73-170">Remember you can find the full sample [here](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span></span>

## <a name="provide-feedback--report-issues"></a><span data-ttu-id="6ec73-171">Geben Sie Ihr Feedback / melden Sie Probleme</span><span class="sxs-lookup"><span data-stu-id="6ec73-171">Provide Feedback / Report Issues</span></span>

<span data-ttu-id="6ec73-172">Wenn Sie uns Ihr Feedback senden oder ein Problem mit sp-pnp-js melden möchten, verwenden Sie die [Problemliste](https://github.com/SharePoint/PnP-JS-Core/issues) in diesem Bericht.</span><span class="sxs-lookup"><span data-stu-id="6ec73-172">If you have any feedback or need to report as issue with sp-pnp-js please use the [issues list](https://github.com/SharePoint/PnP-JS-Core/issues) in that repo.</span></span>
