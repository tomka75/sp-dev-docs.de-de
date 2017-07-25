<span data-ttu-id="056c7-p131">Die allgemeine, nicht konfigurierte Version des Webparts wird zusätzlich zu den Konfigurationen hinzugefügt, die auf bestimmte Szenarien abzielen. Wenn es keine spezifische Konfiguration gibt, die auf die Anforderungen der Benutzer abzielt, können diese so die allgemeine Version verwenden und diese gemäß ihren Anforderungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="056c7-p131">The generic unconfigured version of the web part is added beside the configurations that target specific scenarios. This way, if there is no specific configuration addressing users' needs, they can always use the generic version and configure it according to their requirements.</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent images" },
    "description": { "default": "Shows 5 most recent images" },
    "officeFabricIconFontName": "Picture",
    "properties": {
      "listName": "Images",
      "order": "reversed",
      "numberOfItems": 5,
      "style": "thumbnails"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent documents" },
    "description": { "default": "Shows 10 most recent documents" },
    "officeFabricIconFontName": "Documentation",
    "properties": {
      "listName": "Documents",
      "order": "reversed",
      "numberOfItems": 10,
      "style": "list"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "CustomList",
    "properties": {
      "listName": "",
      "order": "",
      "numberOfItems": 5,
      "style": ""
    }
  }]
}
```

Die allgemeine, nicht konfigurierte Version des Webparts wird zusätzlich zu den Konfigurationen hinzugefügt, die auf bestimmte Szenarien abzielen. Wenn es keine spezifische Konfiguration gibt, die auf die Anforderungen der Benutzer abzielt, können diese so die allgemeine Version verwenden und diese gemäß ihren Anforderungen konfigurieren.

<span data-ttu-id="056c7-255">Um das Ergebnis zu sehen, starten Sie das Debuggen des Projekts, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="056c7-255">To see the result start debugging the project by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="056c7-256">Wenn Sie die Webpart-Toolbox öffnen, um das Webpart dem Zeichenbereich hinzuzufügen, werden Sie sehen, dass es nun drei Webparts gibt, aus denen Benutzer auswählen können.</span><span class="sxs-lookup"><span data-stu-id="056c7-256">When you open the web part toolbox to add the web part to the canvas, you will see that there are now three web parts that users can choose from.</span></span>

![Webpart-Toolbox mit der vorkonfigurierten Version des Webparts](../../../../images/preconfiguredentries-three-configurations-toolbox.png)