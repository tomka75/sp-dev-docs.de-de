---
title: "Integrieren von gulp-Tasks in die SharePoint Framework-Toolkette"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: bbcda74a98b91e02ab681d0d3777cf6c7e5be869
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="integrate-gulp-tasks-in-sharepoint-framework-toolchain"></a><span data-ttu-id="7d089-102">Integrieren von gulp-Tasks in die SharePoint Framework-Toolkette</span><span class="sxs-lookup"><span data-stu-id="7d089-102">Integrate gulp tasks in SharePoint Framework toolchain</span></span>

<span data-ttu-id="7d089-103">Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) zur Ausführung von Tasks im Buildprozess, so beispielsweise für folgende Tasks:</span><span class="sxs-lookup"><span data-stu-id="7d089-103">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="7d089-104">Bündeln und Minimieren von JavaScript- und CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="7d089-104">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="7d089-105">Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build</span><span class="sxs-lookup"><span data-stu-id="7d089-105">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="7d089-106">Kompilieren von LESS- oder SASS-Dateien in CSS</span><span class="sxs-lookup"><span data-stu-id="7d089-106">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="7d089-107">Kompilieren von TypeScript-Dateien in JavaScript</span><span class="sxs-lookup"><span data-stu-id="7d089-107">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="7d089-108">Eine gängige Aufgabe, die Sie zu Ihrer SharePoint Framework-Toolkette hinzufügen sollten, ist die Integration von benutzerdefinierten gulp-Tasks in die Buildpipeline.</span><span class="sxs-lookup"><span data-stu-id="7d089-108">One common task you would want to add to the SharePoint Framework toolchain is to integrate your custom gulp tasks in the build pipeline.</span></span>

## <a name="gulp-tasks"></a><span data-ttu-id="7d089-109">gulp-Tasks</span><span class="sxs-lookup"><span data-stu-id="7d089-109">Gulp tasks</span></span>
<span data-ttu-id="7d089-110">In der Regel werden gulp-Tasks wie folgt in der Datei `gulpfile.js` definiert:</span><span class="sxs-lookup"><span data-stu-id="7d089-110">Normally gulp tasks are defined in the `gulpfile.js` as:</span></span>

```js
gulp.task('somename', function() {
  // Do stuff
});
```

<span data-ttu-id="7d089-p101">Wenn Sie mit der SharePoint Framework-Toolkette arbeiten, müssen Sie Tasks in der Buildpipeline des Frameworks definieren. Sobald Sie ein Task in der Pipeline definiert und registriert haben, wird es der Toolkette hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7d089-p101">When working with the SharePoint Framework toolchain, it is necessary to define your tasks in the framework's build pipeline. Once defined and registered with the pipeline, the task will be added to the toolchain.</span></span>

<span data-ttu-id="7d089-p102">SharePoint Framework verwendet eine [gemeinsame Buildtoolkette](sharepoint-framework-toolchain.md#common-build-tool-packages) aus einem Satz von npm-Paketen, die jeweils dieselben Buildtasks verwenden. Aus diesem Grund sind die Standardtasks im gemeinsamen Paket definiert statt in der Datei `gulpfile.js` in Ihrem clientseitigen Projekt. Führen Sie den folgenden Befehl über eine Konsole in Ihrem Projektverzeichnis aus, um die verfügbaren Tasks anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="7d089-p102">SharePoint Framework uses a [common build toolchain](sharepoint-framework-toolchain.md#common-build-tool-packages) which consists of a set of npm packages that share common build tasks. And hence, the default tasks are defined in the common package as opposed to your client-side project's `gulpfile.js`. To see the available tasks, you can execute the following command in a console within your project directory:</span></span>

```
gulp --tasks
```

<span data-ttu-id="7d089-116">Der Befehl oben listet alle verfügbaren Tasks auf.</span><span class="sxs-lookup"><span data-stu-id="7d089-116">The command above will list all the available tasks.</span></span>

![Verfügbare gulp-Tasks](../../images/gulp-tasks-available.png)

## <a name="custom-gulp-tasks"></a><span data-ttu-id="7d089-118">Benutzerdefinierte gulp-Tasks</span><span class="sxs-lookup"><span data-stu-id="7d089-118">Custom gulp tasks</span></span>
<span data-ttu-id="7d089-p103">Benutzerdefinierte Tasks, die Sie hinzufügen möchten, werden in der Datei `gulpfile.js` definiert. Öffnen Sie die Datei `gulpfile.js` in einem Code-Editor. Der Standardcode initialisiert die SharePoint Framework-Toolkette sowie die globale `gulp`-Instanz für die Toolkette. Die Definitionen aller hinzugefügten benutzerdefinierten Tasks müssen vor dem Code zur Initialisierung der globalen `gulp`-Instanz stehen.</span><span class="sxs-lookup"><span data-stu-id="7d089-p103">To add your custom tasks, you will define the custom tasks in the `gulpfile.js`. Open the `gulpfile.js` in your code editor. The default code initializes the SharePoint Framework toolchain and the global `gulp` instance for the toolchain. Any custom tasks added should be defined before initializing the global `gulp` instance.</span></span>

### <a name="add-your-custom-task"></a><span data-ttu-id="7d089-123">Hinzufügen eines benutzerdefinierten Tasks</span><span class="sxs-lookup"><span data-stu-id="7d089-123">Add your custom task</span></span>
<span data-ttu-id="7d089-124">Wenn Sie ein benutzerdefiniertes gulp-Task hinzufügen möchten, müssen Sie der SharePoint Framework-Buildpipeline ein neues Untertask hinzufügen. Dazu verwenden Sie die Funktion [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task):</span><span class="sxs-lookup"><span data-stu-id="7d089-124">To add your custom gulp task, you will add a new sub task to the SharePoint Framework build pipeline using the [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task) function:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  this.log('Hello, World!');   
  // use functions from gulp task here  
});
```

<span data-ttu-id="7d089-125">Handelt es sich um einen Stream, geben Sie den Stream zurück:</span><span class="sxs-lookup"><span data-stu-id="7d089-125">In the case of a stream, you will return the stream:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  return gulp.src('images/*.png')
             .pipe(gulp.dest('public'));
});
```

### <a name="register-your-task-with-gulp-command-line"></a><span data-ttu-id="7d089-126">Registrieren des Tasks über die gulp-Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="7d089-126">Register your task with gulp command line</span></span>
<span data-ttu-id="7d089-127">Sobald Sie das benutzerdefinierte Task definiert haben, können Sie es über die gulp-Befehlszeile registrieren. Dazu verwenden Sie die Funktion `build.task`:</span><span class="sxs-lookup"><span data-stu-id="7d089-127">Once the custom task is defined, you can then register this custom task with the gulp command line using the `build.task` function:</span></span>

```js
// Register the task with gulp command line
let helloWorldTask = build.task('hello-world', helloWorldSubtask);
```

><span data-ttu-id="7d089-128">Hinweis: Die Definitionen aller hinzugefügten benutzerdefinierten Tasks müssen vor dem Code zur Initialisierung der `gulp`-Instanz stehen, d. h. vor der Codezeile `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="7d089-128">Note: Any custom tasks added should be defined before initializing the global `gulp` instance, that is before the following line of code: `build.initialize(gulp);`</span></span>

<span data-ttu-id="7d089-129">Nun können Sie Ihren benutzerdefinierten Befehl wie folgt über die Befehlszeile ausführen:</span><span class="sxs-lookup"><span data-stu-id="7d089-129">Now you can execute your custom command in the command line as follows:</span></span>

```js
gulp hello-world
```

><span data-ttu-id="7d089-p104">Hinweis: Sie können das mit der Funktion `build.subTask` registrierte Untertask nicht direkt über die Befehlszeile ausführen. Sie können nur das mit der Funktion `build.task` registrierte Task ausführen.</span><span class="sxs-lookup"><span data-stu-id="7d089-p104">Note: You cannot execute the sub task registered using the `build.subTask` function directly from the command line. You can only execute the task registered using the `build.task` function.</span></span>

### <a name="execute-your-custom-task-before-or-after-available-tasks"></a><span data-ttu-id="7d089-132">Ausführen des benutzerdefinierten Tasks vor oder nach verfügbaren Tasks</span><span class="sxs-lookup"><span data-stu-id="7d089-132">Execute your custom task before or after available tasks</span></span>
<span data-ttu-id="7d089-p105">Sie können auch festlegen, dass das hinzugefügte benutzerdefinierte Task vor oder nach bestimmten verfügbaren gulp-Tasks ausgeführt wird. Benutzerdefinierte Tasks können vor oder nach den folgenden gulp-Tasks ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="7d089-p105">You can also add this custom task to be executed before or after certain available gulp tasks. The following gulp tasks allow you to inject your custom task before or after task:</span></span>

- <span data-ttu-id="7d089-135">Allgemeines Build-Task (bestehend aus allen verfügbaren Tasks)</span><span class="sxs-lookup"><span data-stu-id="7d089-135">Generic build task (that consists all the available tasks)</span></span>
- <span data-ttu-id="7d089-136">TypeScript-Task</span><span class="sxs-lookup"><span data-stu-id="7d089-136">TypeScript task</span></span>

<span data-ttu-id="7d089-p106">Die SharePoint Framework-Tasks stehen in der Standard-Buildrig zur Verfügung. Die Buildrig ist eine Sammlung von Tasks, die für einen bestimmten Zweck definiert wurden, in unserem Fall also für die Erstellung clientseitiger Pakete. Sie können über das Objekt `build.rig` auf diese Standardrig sowie die Pre-Task- und Post-Task-Funktionen zugreifen:</span><span class="sxs-lookup"><span data-stu-id="7d089-p106">The SharePoint Framework tasks are available in the default build rig. The build rig is a collection of tasks defined for a specific purpose. In our case, building client-side packages. You can access this default rig using the `build.rig` object and get access to the pre and post task functions:</span></span>
 
```js
// execute before the TypeScript subtask
build.rig.addPreBuildTask(helloWorldTask);

// execute after TypeScript subtask
build.rig.addPostTypescriptTask(helloWorldTask);

// execute after all tasks
build.rig.addPostBuildTask(helloWorldTask);
```

## <a name="example-custom-image-resize-task"></a><span data-ttu-id="7d089-141">Beispiel: Benutzerdefiniertes Task „image-resize“</span><span class="sxs-lookup"><span data-stu-id="7d089-141">Example: Custom image resize task</span></span>
<span data-ttu-id="7d089-p107">Verwenden wir als Beispiel das [gulp-Task „image-resize“](https://www.npmjs.com/package/gulp-image-resize).  Hierbei handelt es sich um ein einfaches Task, mit dem sich die Größe eines Bildes ändern lässt.</span><span class="sxs-lookup"><span data-stu-id="7d089-p107">As an example, let's use the [image resize gulp task](https://www.npmjs.com/package/gulp-image-resize).  It's a simple task that allows you to resize images.</span></span>

<span data-ttu-id="7d089-144">Sie können das vollständige Beispiel [hier](https://aka.ms/spfx-extend-gulp-sample) herunterladen.</span><span class="sxs-lookup"><span data-stu-id="7d089-144">You can download the completed sample [here](https://aka.ms/spfx-extend-gulp-sample).</span></span>

<span data-ttu-id="7d089-145">In der [Dokumentation zum Task „image-resize“](https://www.npmjs.com/package/gulp-image-resize#example) können Sie nachlesen, wie dieses benutzerdefinierte Task eingesetzt wird:</span><span class="sxs-lookup"><span data-stu-id="7d089-145">In the [image resize task's documentation](https://www.npmjs.com/package/gulp-image-resize#example), it shows how to use this custom task:</span></span>

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

<span data-ttu-id="7d089-146">Ausgehend von diesen Informationen fügen wir das Task nun unserem Projekt hinzu. Dazu verwenden wir die Funktionen `build.subTask` und `build.task`:</span><span class="sxs-lookup"><span data-stu-id="7d089-146">We will use this information to add this task in our project using the `build.subTask` and `build.task` functions:</span></span>

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

<span data-ttu-id="7d089-p108">Da wir den Stream definieren, geben wir den Stream in der Funktion `build.subTask` an die Buildpipeline zurück. Die Buildpipeline führt diesen gulp-Stream anschließend asynchron aus.</span><span class="sxs-lookup"><span data-stu-id="7d089-p108">Since we are defining the stream, we return the stream in the `build.subTask` function to the build pipeline. The build pipeline will then asynchronously execute this gulp stream.</span></span> 

<span data-ttu-id="7d089-149">Nun können Sie das Task wie folgt über die gulp-Befehlszeile ausführen:</span><span class="sxs-lookup"><span data-stu-id="7d089-149">Now, you can execute this task from the gulp command line as follows:</span></span>

```js
gulp resize-images
```

![Task „image-resize“](../../images/gulp-extend-image-resize-task.png)

<span data-ttu-id="7d089-151">Außerdem wird das Task `resize-images` in den für Ihr Projekt verfügbaren Tasks aufgeführt, wenn Sie `gulp --tasks` ausführen:</span><span class="sxs-lookup"><span data-stu-id="7d089-151">You will also see this `resize-images` task in the available tasks for your project when you execute `gulp --tasks`:</span></span>

![Task „image-resize“ in der Liste der verfügbaren Tasks](../../images/gulp-extend-image-resize-available-tasks.png)




