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

* **Public tasks** are tasks exported from your gulpfile, which allows them to be run by the `gulp` command.
* **Private tasks** are tasks that are made to be used internally, usually used as part of `series()` or `parallel()` composition.

A private task looks and acts like any other task, but an end-user can’t ever execute it independently.  To register a task publicly, export it from your gulpfile.

```js
var { series } = require('gulp');

function privateTask(cb) {
  // body omitted
  cb();
}

function publicTask(cb) {
  // body omitted
  cb();
}

exports.build = publicTask;
exports.default = series(privateTask, publicTask);
```

[SCREENSHOT]

> In the past, `task()` was used to register your functions as tasks. While that API is still available, exporting should be the primary registration mechanism, except in edge cases where exports won’t work.
