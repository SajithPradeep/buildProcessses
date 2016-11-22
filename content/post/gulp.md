+++
Categories = []
Tags = []
title = "Gulp"
draft = false
+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class="custom-heading"> What is Gulp? </p>
<p>Gulp is a tool that helps you out with several tasks when it comes to web development. It's often used to do front end tasks like:</p>
<p>•	Spinning up a web server</p>
<p>•	Reloading the browser automatically whenever a file is saved</p>
<p>•	Using preprocessors like Sass or LESS</p>
<p>•	Optimizing assets like CSS, JavaScript, and images</p>


<p class="custom-heading"> What gulp does  </p>
<p>Before we dive into working with Gulp, let's talk about why you may want to use Gulp as opposed to other similar tools.</p>
<p>•	Spins up a web server</p>
<p>•	Compiles Sass to CSS</p>
<p>•	Refreshes the browser automatically whenever you save a file</p>
<p>•	Optimizes all assets (CSS, JS, fonts, and images) for production</p>

<p class="custom-heading"> Gulp example structure  </p>
<img src="/img/gulp1.jpg" />
<p>
In this structure, we'll use the <highlight>app</highlight> folder for development purposes, while the <highlight>dist</highlight> (as in "distribution") folder is used to contain optimized files for the production site.
Since <highlight>app</highlight> is used for development purposes, all our code will be placed in <highlight>app</highlight>.
We'll have to keep this folder structure in mind when we work on our Gulp configurations. Now, let's begin by creating your first Gulp task in <highlight>gulpfile.js</highlight>, which stores all Gulp configurations.
</p>


<p class="custom-heading"> Best Practices  </p>
<p class="custom-sub-heading"> 1. Automate all Imports </p>
<p>The number of files in a project grows daily, and so do the places these files get imported in. Under an ES5/Angular 1.x environment normally all files are included inside an index.html file, however when working with a more complex environment which includes testing, coverage reports, and automated builds, it pays off to automate the imports, and even try to unify them into a few generic importing tasks that can be reused in multiple workflows.
Gulp has quite a few great plugins for dealing with such automated imports,<highlight> gulp-inject, wiredep, useref </highlight>and <highlight>angular-file-sort </highlight>being a few good examples, however initial configuration could be challenging.
</p>


<p class="custom-sub-heading">2. Understand directory structure requirements</p>
<p>A well thought out directory structure can go a long way in preventing issues that can occur in the era of precompiled languages, transpilers and multiple environment modes. Due to this we understand that:
</p>
<p>1.	Our source code is not the same code (and most of the time not in the same programming language) that's being served to the browser.
</p>
<p>2.	Our source code is served minified and concatenated in production, but this can be confusing for development.
</p>
<p>Here is an example directory structure in which source code (src) is separated from temporary precompiled assets (.tmp), which are separated from the final distribution folder (dist). The src folder contains higher level languages such as jade, typescript and scss; the .tmp contains compiled js, css and html files; while the dist folder contains only concatenated and minified files optimized to be served in production.</p>

<img src="/img/gulp2.jpg" />


<p class="custom-sub-heading">3. Provide distinct development and production builds</p>
<p>With the right directory structure, injection automation and build automation in place, we can use browser-sync, the tool recommended by the gulp team, to serve either a production or a development version of our app.
</p>

<pre>
<code>
function browserSyncInit(baseDir, files) {  
  browserSync.instance = browserSync.init(files, {
    startPath: '/', server: { baseDir: baseDir }
  });
}

// starts a development server
// runs preprocessor tasks before,
// and serves the src and .tmp folders
gulp.task(  
    'serve',
    ['typescript', 'jade', 'sass', 'inject' ],
function () {
  browserSyncInit([
    paths.tmp
    paths.src
  ], [
    paths.tmp + '/**/*.css',
    paths.tmp + '/**/*.js',
    paths.tmp + '/**/*.html'
  ]);
});

// starts a production server
// runs the build task before,
// and serves the dist folder
gulp.task('serve:dist', ['build'], function () {  
  browserSyncInit(paths.dist);
});
</code>
</pre>

<p>Now we can run our development server with<highlight> gulp serve</highlight> and simulate a production build with <highlight>gulp serve:dist</highlight>.</p>


<p class="custom-sub-heading">4. Inject files with gulp-inject and wiredep</p>
<p>Between gulp-inject and wiredep there is no excuse to ever have to manually inject a file into index.html. gulp-inject does a great job at selecting all your javascript and css files, while wiredep assists with selecting the right files from any installed bower packages.
</p>

<pre>
<code>
gulp.task('inject', function () {

  var injectStyles = gulp.src([
      // selects all css files from the .tmp dir
      paths.tmp + '/**/*.css'
    ], { read: false }
  );

  var injectScripts = gulp.src([
    // selects all js files from .tmp dir
    paths.tmp + '/**/*.js',
    // but ignores test files
    '!' + paths.src + '/**/*.test.js'
    // then uses the gulp-angular-filesort plugin
    // to order the file injection
]).pipe($.angularFilesort()
          .on('error', $.util.log));
  // tell wiredep where your bower_components are
  var wiredepOptions = {
    directory: 'bower_components'
  };

  return gulp.src(paths.src + '/*.html')
    .pipe($.inject(injectStyles, injectOptions))
    .pipe($.inject(injectScripts, injectOptions))
    .pipe(wiredep(wiredepOptions))
    // write the injections to the .tmp/index.html file
    .pipe(gulp.dest(paths.tmp));
    // so that src/index.html file isn't modified  
    // with every commit by automatic injects
});
</code>
</pre>



<p class="custom-sub-heading">5. Create production builds with gulp-useref </p>
<p>gulp-useref is a hidden gem within the gulp ecosystem. It's a wonderful plugin which reads all the files included in a html file, then concatenates and minifies them, returning and including a single file.
That means that during your gulp build process you can use gulp-useref to turn your index.html imports from this:
</p>
<pre>
<code>
...
  <!-- build:js scripts/minified.js -->
  < body>
  < script type="text/javascript" src="scripts/one.js"></script >
  < script type="text/javascript" src="scripts/deux.js"></script >
  < script type="text/javascript" src="scripts/drie.js"></script >
  < /body>
  <!-- endbuild -->
...
</code>
</pre>

<p> to this: </p>
<pre>
<code>
< body>< script src="scripts/minified.js">< /script >< /body>
</code>
</pre>
<p> with relative ease: </p>
<pre>
<code>
return gulp.src('src/index.html')
    .pipe(useref())
    .pipe(gulp.dest('dist'));
</pre>
</code>


<p class="custom-sub-heading">6. Separate Gulp tasks into multiple files</p>
<p>As the project grows, so does the number of gulp tasks. This can leave you with a very large and messy gulpfile.js. A usefull trick is to split the file into multiple files inside a directory, then use require-dir to require all the task files within gulpfile.js.
A gulp structure we've been using is :
</p>
<img src="/img/gulp3.jpg" />
<p>Now we can separate task concerns across multiple files, by adding the following to the bottom of our gulpfile.js (after we've done: <highlight>npm install --save-dev require-dir</highlight>):</p>

<pre>
<code>
require('require-dir')('./gulp');  
</code>
</pre>
