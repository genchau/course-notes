## hackernoon - gulp 
##### Date started: 06/01/2018. [Link to course](https://hackernoon.com/how-to-automate-all-the-things-with-gulp-b21a3fc96885) 
- - -   

### Gulp
- It can simulate the server environment where we will ultimately be hosting our code.
- Files and directory management
- Compile, minify, and concatenate
- Goal of getting our code bases footprint down to the absolute minimum.
- Making it ready for shipping to production. 

### TLDR;
1. Three main Gulp commands: gulp.task, gulp.src, gulp.dest.
2. pipe() method is built into Node.js and is used to copy files from one folder to another.
3. Logical folder structure
    - src (pre-processed files)
    - tmp (local development server)
    - dist (processed and minified files)
4. Creating separate tasks for pipe-ing HTML, CSS, and JavaScript files from src to tmp.
5. Combine the HTML, CSS and JavaScript tasks into one main 'copy' task. This will copy all the files with just one command.
6. After all files have been copied we want them automatically referenced in our main index.html. We use "inject" task for this.
7. We can run a development server on the tmp folder.
8. While the server is running we can "watch" for changes and enable live reloading on the local development server.
9. Once we are satisfy we can go ahead and fully build our production files and place them in the dist directory.
10. Delete tmp and dist before pushing to GitHub. (Or just add them to our .gitignore)

### Install the tools
- Node needs to be installed on our system. `node -v`.
- Run `npm install -g gulp` to install gulp on our system globally.

### Introduce yourself
- `gulp.task` defines a new task giving it a name, an array of dependencies and a callback function, which will be called when the task is run. 
- `gulp.src` sets the source folder where files are located.
- `gulp.dest` sets the destination folder where files will be placed.
- `.pipe` is simple copying files

`gulp.src` => `.pipe` => `gulp.dest`

Gulp by itself only provides a basic framework for task automation, task runner. We rely on the community of plugins to add functionality to this engine.

### Baby steps
#### Instructions:
- create directory `super-awesome-gulp-tutorial`
- open command prompt to this folder
- run `npm init`
- run `npm install gulp --save-dev` (save-dev is used to save this dependency in package.json so when we transfer this project to another computing system, it can automatically install all dependencies.)
- create file gulpfile.js
```
var gulp = require('gulp');
gulp.task('default', function () {
  console.log('Hello World!');
});
```
- run `gulp` in command prompt to execute the default task

### Full hacker mode, ON
Basic folder structure:
- `src` source files, pre-processed, un-minified.
- `tmp` development files, pre-processed, un-minified. The directory where we will be running the web sever.
- `dist` production files, processed, minified.

#### Instructions:
- create `src` folder in our project folder
- create index.html
- create script.js
- create style.css

#### gulpfile.js:
#### Step 1 - folder structure:
paths variable for our folder structure.
```
var gulp = require('gulp');

var paths = {
  src: 'src/**/*',
  srcHTML: 'src/**/*.html',
  srcCSS: 'src/**/*.css',
  srcJS: 'src/**/*.js',
  tmp: 'tmp',
  tmpIndex: 'tmp/index.html',
  tmpCSS: 'tmp/**/*.css',
  tmpJS: 'tmp/**/*.js',
  dist: 'dist',
  distIndex: 'dist/index.html',
  distCSS: 'dist/**/*.css',
  distJS: 'dist/**/*.js'
};

gulp.task('default', function () {
  console.log('Hello World!');
});
```
note: `/**/*` will include all files within the folder and subfolders.

#### Step 2 - HTML task
Copies all HTML files from src to tmp.
```
gulp.task('html', function () {
  return gulp.src(paths.srcHTML).pipe(gulp.dest(paths.tmp));
});
```

#### Step 3 - Set up the CSS task
Copies all CSS files from src to tmp.
```
gulp.task('css', function () {
  return gulp.src(paths.srcCSS).pipe(gulp.dest(paths.tmp));
});
```

#### Step 4 - Set up the JavaScript task
Copies all JS files from src to tmp.
```
gulp.task('js', function () {
  return gulp.src(paths.srcJS).pipe(gulp.dest(paths.tmp));
});
```

#### Step 5 - Combine all tasks into one task
We can combine tasks in Gulp, adding tasks to other tasks as dependencies.
```
gulp.task('copy', ['html', 'css', 'js']);
```
The above command will run in this sequence: 
1. html
2. css
3. js
4. copy
5. FINISHED

#### Step 6 - Inject files into the index.html
This plugin will modify index.html to reference the correct css and js files.
1. run `npm install gulp-inject --save-dev`
2. add a reference to index.html where gulp-inject will add the files.
```
<!DOCTYPE html>
<html>
  <head>
    <!-- src/index.html -->
  
    <!-- inject:css -->
    <!-- endinject -->
  </head>
  <body>
    <!-- inject:js -->
    <!-- endinject -->
  </body>
</html>
```
3. gulpfile.js:
```
var inject = require('gulp-inject');

gulp.task('inject', ['copy'], function () {
  var css = gulp.src(paths.tmpCSS);
  var js = gulp.src(paths.tmpJS);
  return gulp.src(paths.tmpIndex)
    .pipe(inject( css, { relative:true } ))
    .pipe(inject( js, { relative:true } ))
    .pipe(gulp.dest(paths.tmp));
});
```
The code above:
- `copy` is a dependency, so it will run first and copy all the files from src to tmp.
- Then it will inject.
- We store the path to css in var css.
- We store the path to js in var js.
- We then run return on index.html in tmp folder, piping in inject for css and js in the tmp folder.
- Just add relative:true as option for inject, just do it.

#### Step 7 - Serve the development web server
- run `npm install gulp-webserver --save-dev`
- gulpfile.js:
```
var webserver = require('gulp-webserver');

gulp.task('serve', ['inject'], function () {
  return gulp.src(paths.tmp)
    .pipe(webserver({
      port: 3000,
      livereload: true
    }));
});
```
- index.html
```
<!DOCTYPE html>
<html>
  <head>
    <!-- inject:css -->
    <!-- endinject -->
  </head>
  <body>
    <div class="awesome">This is awesome!</div>
    <!-- inject:js -->
    <!-- endinject -->
  </body>
</html>
```
- style.css
```
.awesome {
  color: red;
}
```
- script.js
```
console.log('Awesome!');
```
- run `gulp serve`
- open localhost:3000

#### Step 8 - Watch for changes
We can watch for changes and have Gulp do something about it. 
```
gulp.task('watch', ['serve'], function () {
  gulp.watch(paths.src, ['inject']);
});
```
The task above will watch for any changes in the src folder

```
gulp.task('default', ['watch']);
```
The task above will add watch into the default gulp task.

#### Step 9 - Building the dist
Production files are usually built for performance which means cleaning, concatenating, and minifying.
- install the following:
```
npm install gulp-htmlclean --save-dev
npm install gulp-clean-css --save-dev
npm install gulp-concat --save-dev
npm install gulp-uglify --save-dev
```
- gulpfile.js:
```
var htmlclean = require('gulp-htmlclean');
var cleanCSS = require('gulp-clean-css');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');

gulp.task('html:dist', function () {
  return gulp.src(paths.srcHTML)
    .pipe(htmlclean())
    .pipe(gulp.dest(paths.dist));
});
gulp.task('css:dist', function () {
  return gulp.src(paths.srcCSS)
    .pipe(concat('style.min.css'))
    .pipe(cleanCSS())
    .pipe(gulp.dest(paths.dist));
});
gulp.task('js:dist', function () {
  return gulp.src(paths.srcJS)
    .pipe(concat('script.min.js'))
    .pipe(uglify())
    .pipe(gulp.dest(paths.dist));
});
gulp.task('copy:dist', ['html:dist', 'css:dist', 'js:dist']);
gulp.task('inject:dist', ['copy:dist'], function () {
  var css = gulp.src(paths.distCSS);
  var js = gulp.src(paths.distJS);
  return gulp.src(paths.distIndex)
    .pipe(inject( css, { relative:true } ))
    .pipe(inject( js, { relative:true } ))
    .pipe(gulp.dest(paths.dist));
});
gulp.task('build', ['inject:dist']);
```
- index.html:
```
<!DOCTYPE html>
<html>
  <head>
    <!--[htmlclean-protect]-->
    <!-- inject:css -->
    <!-- endinject -->
    <!--[/htmlclean-protect]-->
  </head>
  <body>
    <div class="awesome">This is awesome!</div>
    <!--[htmlclean-protect]-->
    <!-- inject:js -->
    <!-- endinject -->
    <!--[/htmlclean-protect]-->
</body>
</html>
```
Thie above code will prevent html clean from cleaning the inject comments.

- run `gulp build`

#### Step 10 - Cleaning Up
We should not include tmp nor dist folders in our GitHub repo. 
- run `npm install del --save-dev`
- gulpfile.js
```
var del = require('del');

gulp.task('clean', function () {
  del([paths.tmp, paths.dist]);
});
```
- run `gulp clean`

Or just add tmp and dist to .gitignore.

[Cheatsheet](https://github.com/adnanrahic/gulp-all-the-things)

<img src="https://raw.githubusercontent.com/genchau/course-notes/master/notes/hackernoon_gulp-01.jpg">

- - -
Return to [Table of Contents](TableOfContents.md)
