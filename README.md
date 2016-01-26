# min-server
Minimal and fast Server with Live Reload and [*Package*](https://www.npmjs.com/package/min-server) &mdash; never again manually reload your browser!

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)


## LiveReload
[**LiveReload**](http://livereload.com/) monitors changes in your files and instantly updates all changes in your browser. It is very useful when you are updating your site and **don't want to keep manually reloading** the page in your browser again and again after every edit.


## Why?
- Many setups are bloated with unnecessary options and packages.
- Start clean and minimal and extend as you go.
- Add single package to your project instead of many, to get your live reload server up and running.


## Why not something else?
- [`live-server`](https://github.com/tapio/live-server) is small and awesome but unfortunately slow; there is noticeable delay between the change in your file and its effect in the browser. 
- [`browser-sync`](https://github.com/BrowserSync/browser-sync) is incredibly powerful and fast but (a) is massive with 25MB total to download and (b) flashes "Connected with Browser-Sync" in a large black on box top of your page on every reload.


## Why [Gulp](https://github.com/gulpjs/gulp) plugins?
- Fast: use streams, no temporary files.
- Gulp plugins have uniform API: stream in, stream out; no massive command line options.
- Convenient and expressive [node-glob](https://github.com/isaacs/node-glob) abstraction to select files/directories to be watched.


## Use cases
- You have a project and want to add server and live reload &mdash; [install the package](#to-use-as-package-add-to-your-project).
- You want to quickly play and evaluate LiveReload in a clean folder &mdash; [clone or download the repository](#to-use-as-separate-repository).


## Features
- Minimal functional Server setup with Live Reload setup.
- Use as *repository* (`git clone`) or *package* (`npm install`).
- Installs all dependency packages, no need to install them manually. Keeps your `package.json` clean.
- Automatically and gracefully (without overwriting) copied to your project directory:
  - Minimal `Gulpfile.js` (with comments) includes:
    - Gulp task `gulp connect` with 4 lines of code to start [connect server](https://github.com/senchalabs/connect):

    ```js
    gulp.task('connect', function () {
      connect()
        .use(connectLivereload())
        .use(connect.static(config.rootDir))
        .listen(8081)
    })
    ```

    - Gulp task `gulp watch` with 4 lines of code to watch your files for changes:

    ```js
    gulp.task('watch', ['connect'], function () {
      gulpLivereload.listen()
      gulp.watch(['*.{html,css,js}', '!Gulpfile.js'], function (file) {
        gulp.src(file.path)
          .pipe(gulpLivereload())
      })
    })
    ```

    - Featuring the awesome [better stuff opener](https://github.com/sindresorhus/opn):

    ```js
    gulp.task('serve', ['connect'], function () {
      opn('http://localhost:8081')
    })
    ```


## If you are new to Node
[Download and Install Node.js](https://nodejs.org/download/), see [How do I get started with Node.js](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-node-js) for more information.


## To use as separate Repository: 
### Clone
```sh
git clone https://github.com/dmitriz/min-server
```
or simply [Download this Repository](https://github.com/dmitriz/min-server/archive/master.zip),
unzip it and `cd min-server-master`.


### Install dependencies
```sh
npm install --save-dev
```

## To use as Package (add to your project):
In your main project directory (should contain `package.json`):
```sh
npm install min-server --save
```

## Getting started
Simply run the default Gulp task:
```sh
gulp
```
Now try to edit and save `index.html` and see how your changes instantly appear in the browser!

Enjoy!
