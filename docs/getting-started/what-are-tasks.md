<!-- front-matter
id: what-are-tasks
title: What are Tasks
hide_title: true
sidebar_label: What are Tasks
-->

# What are Tasks

Each gulp task is an asynchronous JavaScript function - a function that accepts a callback or returns a stream, promise, observable, etc ([more on that later][node-async]). Due to some platform limitations, synchronous tasks aren’t supported, though there is a pretty nifty [alternative][async-await-sync-tasks].

## Exporting

Tasks can be considered **public** or **private**.

* **Public tasks** are exported from your gulpfile, which allows them to be run by the `gulp` command.
* **Private tasks** are made to be used internally, usually used as part of `series()` or `parallel()` composition.

A private task looks and acts like any other task, but an end-user can’t ever execute it independently.  To register a task publicly, export it from your gulpfile.

```js
const { series } = require('gulp');

// The `clean` function is not exported so it can be considered a private task.
// It can still be used within the `series()` composition.
function clean(cb) {
  // body omitted
  cb();
}

// The `build` function is exported so it is public and can be run with the `gulp` command.
// It can also be used within the `series()` composition.
function build(cb) {
  // body omitted
  cb();
}

exports.build = build;
exports.default = series(clean, build);
```

![ALT TEXT MISSING][img-gulp-tasks-command]

<small>In the past, `task()` was used to register your functions as tasks. While that API is still available, exporting should be the primary registration mechanism, except in edge cases where exports won’t work.</small>


[img-gulp-tasks-command]: https://gulpjs.com/img/docs-gulp-tasks-command.png
