# <a name="integrate-gulp-tasks-in-sharepoint-framework-toolchain"></a>Integrieren von gulp-Tasks in die SharePoint Framework-Toolkette

Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) zur Ausführung von Tasks im Buildprozess, so beispielsweise für folgende Tasks:

* Bündeln und Minimieren von JavaScript- und CSS-Dateien
* Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build
* Kompilieren von LESS- oder SASS-Dateien in CSS
* Kompilieren von TypeScript-Dateien in JavaScript

Eine gängige Aufgabe, die Sie zu Ihrer SharePoint Framework-Toolkette hinzufügen sollten, ist die Integration von benutzerdefinierten gulp-Tasks in die Buildpipeline.

## <a name="gulp-tasks"></a>gulp-Tasks
In der Regel werden gulp-Tasks wie folgt in der Datei `gulpfile.js` definiert:

```js
gulp.task('somename', function() {
  // Do stuff
});
```

Wenn Sie mit der SharePoint Framework-Toolkette arbeiten, müssen Sie Tasks in der Buildpipeline des Frameworks definieren. Sobald Sie ein Task in der Pipeline definiert und registriert haben, wird es der Toolkette hinzugefügt.

SharePoint Framework verwendet eine [gemeinsame Buildtoolkette](sharepoint-framework-toolchain.md#common-build-tools-packages) aus einem Satz von npm-Paketen, die jeweils dieselben Buildtasks verwenden. Aus diesem Grund sind die Standardtasks im gemeinsamen Paket definiert statt in der Datei `gulpfile.js` in Ihrem clientseitigen Projekt. Führen Sie den folgenden Befehl über eine Konsole in Ihrem Projektverzeichnis aus, um die verfügbaren Tasks anzuzeigen:

```
gulp --tasks
```

Der Befehl oben listet alle verfügbaren Tasks auf.

![Verfügbare gulp-Tasks](../../images/gulp-tasks-available.png)

## <a name="custom-gulp-tasks"></a>Benutzerdefinierte gulp-Tasks
Benutzerdefinierte Tasks, die Sie hinzufügen möchten, werden in der Datei `gulpfile.js` definiert. Öffnen Sie die Datei `gulpfile.js` in einem Code-Editor. Der Standardcode initialisiert die SharePoint Framework-Toolkette sowie die globale `gulp`-Instanz für die Toolkette. Die Definitionen aller hinzugefügten benutzerdefinierten Tasks müssen vor dem Code zur Initialisierung der globalen `gulp`-Instanz stehen.

### <a name="add-your-custom-task"></a>Hinzufügen eines benutzerdefinierten Tasks
Wenn Sie ein benutzerdefiniertes gulp-Task hinzufügen möchten, müssen Sie der SharePoint Framework-Buildpipeline ein neues Untertask hinzufügen. Dazu verwenden Sie die Funktion [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task):

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  this.log('Hello, World!');   
  // use functions from gulp task here  
});
```

Handelt es sich um einen Stream, geben Sie den Stream zurück:

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  return gulp.src('images/*.png')
             .pipe(gulp.dest('public'));
});
```

### <a name="register-your-task-with-gulp-command-line"></a>Registrieren des Tasks über die gulp-Befehlszeile
Sobald Sie das benutzerdefinierte Task definiert haben, können Sie es über die gulp-Befehlszeile registrieren. Dazu verwenden Sie die Funktion `build.task`:

```js
// Register the task with gulp command line
let helloWorldTask = build.task('hello-world', helloWorldSubtask);
```

>Hinweis: Die Definitionen aller hinzugefügten benutzerdefinierten Tasks müssen vor dem Code zur Initialisierung der `gulp`-Instanz stehen, d. h. vor der Codezeile `build.initialize(gulp);`.

Nun können Sie Ihren benutzerdefinierten Befehl wie folgt über die Befehlszeile ausführen:

```js
gulp hello-world
```

>Hinweis: Sie können das mit der Funktion `build.subTask` registrierte Untertask nicht direkt über die Befehlszeile ausführen. Sie können nur das mit der Funktion `build.task` registrierte Task ausführen.

### <a name="execute-your-custom-task-before-or-after-available-tasks"></a>Ausführen des benutzerdefinierten Tasks vor oder nach verfügbaren Tasks
Sie können auch festlegen, dass das hinzugefügte benutzerdefinierte Task vor oder nach bestimmten verfügbaren gulp-Tasks ausgeführt wird. Benutzerdefinierte Tasks können vor oder nach den folgenden gulp-Tasks ausgeführt werden:

- Allgemeines Build-Task (bestehend aus allen verfügbaren Tasks)
- TypeScript-Task

Die SharePoint Framework-Tasks stehen in der Standard-Buildrig zur Verfügung. Die Buildrig ist eine Sammlung von Tasks, die für einen bestimmten Zweck definiert wurden, in unserem Fall also für die Erstellung clientseitiger Pakete. Sie können über das Objekt `build.rig` auf diese Standardrig sowie die Pre-Task- und Post-Task-Funktionen zugreifen:
 
```js
// execute after TypeScript task
build.rig.addPostTypescriptTask(helloWorldTask);

//execute before TypeScript task
build.rig.addBuildTasks(helloWorldTask);

//execute after all tasks
build.rig.addPostBuildTask(helloWorldTask);

//execute before all tasks
build.rig.addPreBuildTask(helloWorldTask);
```

## <a name="example-custom-image-resize-task"></a>Beispiel: Benutzerdefiniertes Task „image-resize“
Verwenden wir als Beispiel das [gulp-Task „image-resize“](https://www.npmjs.com/package/gulp-image-resize).  Hierbei handelt es sich um ein einfaches Task, mit dem sich die Größe eines Bildes ändern lässt.

Sie können das vollständige Beispiel [hier](https://aka.ms/spfx-extend-gulp-sample) herunterladen.

In der [Dokumentation zum Task „image-resize“](https://www.npmjs.com/package/gulp-image-resize#example) können Sie nachlesen, wie dieses benutzerdefinierte Task eingesetzt wird:

```js
var gulp = require('gulp');
var imageResize = require('gulp-image-resize');
 
gulp.task('default', function () {
  gulp.src('test.png')
    .pipe(imageResize({
      width : 100,
      height : 100,
      crop : true,
      upscale : false
    }))
    .pipe(gulp.dest('dist'));
});
```

Ausgehend von diesen Informationen fügen wir das Task nun unserem Projekt hinzu. Dazu verwenden wir die Funktionen `build.subTask` und `build.task`:

```js
var imageResize = require('gulp-image-resize');

let imageResizeSubTask = build.subTask('image-resize-subtask', function(gulp, buildOptions, done){
    return gulp.src('images/*.jpg')
               .pipe(imageResize({
                   width: 100,
                   height: 100,
                   crop: false                   
               }))
               .pipe(gulp.dest(path.join(buildOptions.libFolder, 'images')))
});

let imageResizeTask = build.task('resize-images', imageResizeSubTask);
```

Da wir den Stream definieren, geben wir den Stream in der Funktion `build.subTask` an die Buildpipeline zurück. Die Buildpipeline führt diesen gulp-Stream anschließend asynchron aus. 

Nun können Sie das Task wie folgt über die gulp-Befehlszeile ausführen:

```js
gulp resize-images
```

![Task „image-resize“](../../images/gulp-extend-image-resize-task.png)

Außerdem wird das Task `resize-images` in den für Ihr Projekt verfügbaren Tasks aufgeführt, wenn Sie `gulp --tasks` ausführen:

![Task „image-resize“ in der Liste der verfügbaren Tasks](../../images/gulp-extend-image-resize-available-tasks.png)




