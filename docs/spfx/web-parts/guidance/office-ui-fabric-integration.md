<span data-ttu-id="ca642-p130">**Offenlegung von nicht bereichsbezogenen Klassen** – Es gibt ein weiteres Problem mit Nachfolgerselektoren. Beachten Sie im obigen Beispiel, dass die Formatvorlagen für Höhe und Breite aus der nicht bereichsbezogenen myButton-Klasse auf alle Schaltflächen angewendet werden. Dies impliziert, dass eine Änderung in dieser Formatvorlage die HTML, die das bereichsbezogene Markup verwendet, versehentlich beschädigen könnte. Nehmen wir beispielsweise an, dass wir die Höhe auf App-Ebene auf 0px in der myButton-Klasse festlegen. Dies führt dazu, dass alle Drittanbieter-Webparts, die die myButton-Klasse verwenden, eine Höhe von 0 haben, also eine wesentliche Regression in der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="ca642-p130">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0 i.e. a serious regression in the user experience.</span></span>

```HTML
  <html>
  <head>
  <title>CSS specifity test</title>
  <style>
  .myButton {
      background-color: brown;
      color:brown;
      height:20px;
      width:40px;
  }
  </style>
  <style>
  .scope2 .myButton {
      background-color: green;
      color:green;
  }
  </style>
  <style>
  .scope3 .myButton {
      background-color: yellow;
      color:yellow;
  }
  </style>
  <style>
  .scope1 .myButton {
      background-color: red;
      color:red;
  }
  </style>
</head>
<body>
  <div>
    <span>These tests demonstrate descendant selectors, nesting and load order problems.</span>

    <div>
      <br/>
      <span>This test depicts that a descendant selector with the same specificity do not allow nesting.
      All buttons below do not take the innermost scope i.e. they should be different colors, but they are red.
      Further, if you change the ordering of the style tags, the colors will change. i.e. the UI is load order dependant.</span> 
      <div class='scope1'>
        <button class='myButton'</button>
        <div class='scope2'>
          <button class='myButton'></button>
          <div class='scope3'>
            <button class='myButton'></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

**Offenlegung von nicht bereichsbezogenen Klassen** – Es gibt ein weiteres Problem mit Nachfolgerselektoren. Beachten Sie im obigen Beispiel, dass die Formatvorlagen für Höhe und Breite aus der nicht bereichsbezogenen myButton-Klasse auf alle Schaltflächen angewendet werden. Dies impliziert, dass eine Änderung in dieser Formatvorlage die HTML, die das bereichsbezogene Markup verwendet, versehentlich beschädigen könnte. Nehmen wir beispielsweise an, dass wir die Höhe auf App-Ebene auf 0px in der myButton-Klasse festlegen. Dies führt dazu, dass alle Drittanbieter-Webparts, die die myButton-Klasse verwenden, eine Höhe von 0 haben, also eine wesentliche Regression in der Benutzeroberfläche.

## <a name="updating-an-existing-project"></a><span data-ttu-id="ca642-232">Aktualisieren bereits vorhandener Projekte</span><span class="sxs-lookup"><span data-stu-id="ca642-232">Updating an existing project</span></span>

<span data-ttu-id="ca642-233">Aktualisieren Sie in der Datei `package.json` Ihres Projekts die Abhängigkeit `@microsoft/sp-build-web` mindestens auf Version 1.0.1, löschen Sie das Verzeichnis `node_modules` Ihres Projekts, und führen Sie den Befehl `npm install` aus.</span><span class="sxs-lookup"><span data-stu-id="ca642-233">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>

