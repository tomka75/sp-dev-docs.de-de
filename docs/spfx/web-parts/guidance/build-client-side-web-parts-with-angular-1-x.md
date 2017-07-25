<span data-ttu-id="1bc49-p126">Öffnen Sie im Code-Editor die Datei **app/HomeController.ts**. Erweitern Sie den Konstruktor wie folgt:</span><span class="sxs-lookup"><span data-stu-id="1bc49-p126">In the code editor open the **app/HomeController.ts** file. Extend the constructor as follows:</span></span>

Öffnen Sie im Code-Editor die Datei **app/HomeController.ts**. Erweitern Sie den Konstruktor wie folgt:

```ts
constructor(private dataService: IDataService, private $window: angular.IWindowService, private $rootScope: angular.IRootScopeService) {
  const vm: HomeController = this;
  this.init();

  $rootScope.$on('configurationChanged', (event: angular.IAngularEvent, args: { hideFinishedTasks: boolean }): void => {
    vm.init(args.hideFinishedTasks);
  });
}
```

![Konstruktordefinition in der Datei „HomeController.ts“ in Visual Studio Code](../../../../images/ng-intro-homecontroller-event.png)

<span data-ttu-id="1bc49-224">Geben Sie Folgendes in die Befehlszeile ein, um zu überprüfen, ob die Angular-Anwendung wie erwartet arbeitet und korrekt auf die Eigenschaftenänderung antwortet:</span><span class="sxs-lookup"><span data-stu-id="1bc49-224">To verify that the Angular application is working as expected and correctly responds to property changed, in the command line run:</span></span>

```sh
gulp serve
```

<span data-ttu-id="1bc49-225">Wenn Sie auf die Umschaltfläche **Hide finished tasks** klicken, sollten abgeschlossene Aufgaben im Webpart eingeblendet bzw. ausgeblendet werden.</span><span class="sxs-lookup"><span data-stu-id="1bc49-225">If you toggle the value of the **Hide finished tasks** property, web part should show or hide finished tasks accordingly.</span></span>

![Webpart, das nur noch offene Aufgaben zeigt, mit aktivierter Option „Hide finished tasks“](../../../../images/ng-intro-hide-finished-tasks.png)