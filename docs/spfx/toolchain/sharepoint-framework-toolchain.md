<span data-ttu-id="e1b2a-p121">In der Regel setzen Sie SHIP als Ziel, wenn das Webpart-Projekt zur Auslieferung an oder Bereitstellung auf einem Produktionsserver bereit ist. Für andere Szenarien wie Tests und Debugging würden Sie BUILD als Ziel setzen. Das Ziel SHIP stellt auch sicher, dass die minimierte Version des Webpart-Bundles erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="e1b2a-p121">Usually, when your web part project is ready to ship or deploy in a production server, you will target SHIP. For other scenarios like testing and debugging you would target BUILD. The SHIP target also ensures that the minified version of the web part bundle is built.</span></span>

In der Regel setzen Sie SHIP als Ziel, wenn das Webpart-Projekt zur Auslieferung an oder Bereitstellung auf einem Produktionsserver bereit ist. Für andere Szenarien wie Tests und Debugging würden Sie BUILD als Ziel setzen. Das Ziel SHIP stellt auch sicher, dass die minimierte Version des Webpart-Bundles erstellt wird. 

<span data-ttu-id="e1b2a-219">Um den SHIP-Modus als Ziel zu setzen, hängen Sie `--ship` an den Task an:</span><span class="sxs-lookup"><span data-stu-id="e1b2a-219">To target SHIP mode, you append the task with `--ship`:</span></span>

```
gulp --ship
```

<span data-ttu-id="e1b2a-220">Im DEBUG-Modus kopieren die Buildtasks alle Webpart-Objekte inklusive des Webpart-Bundles in den Ordner `dist`.</span><span class="sxs-lookup"><span data-stu-id="e1b2a-220">In DEBUG mode, the build tasks copy all of the web part assets, including the web part bundle, into the `dist` folder.</span></span>

<span data-ttu-id="e1b2a-221">Im SHIP-Modus kopieren die Buildtasks alle Webpart-Objekte inklusive des Webpart-Bundles in den Ordner `temp\deploy`.</span><span class="sxs-lookup"><span data-stu-id="e1b2a-221">In SHIP mode, the build tasks copy all of the web part assets, including the web part bundle, into the `temp\deploy` folder.</span></span>
