# gulp-qn-sync-mp

gulp-qn-sync-mp 是针对[gulp-qn-sync](https://www.npmjs.com/package/gulp-qn-sync)的一个多平台适配版本.

## Usage

```javascript
npm install gulp-qn-sync-mp --registry http://registry.local.easyar/  --save-dev
```

```javascript
var jeditor = require("gulp-json-editor");
```

## content

以同步的方式上传文件到七牛云

基于 node4.0 gulp4.0 的环境下。

主要为了配合 gulp4.0 的 gulp.series 方法

当前的上传任务不完成，则无法进行下一个任务。

## demo gulpfile.js

```javascript
var qiniu = require("gulp-qn-sync-mp");

gulp.task(
  "js",
  gulp.series(
    /** 其他任务，如js，css打包预编译 */
    // 	task_js,
    //	task_css,
    uploadQiniu
  )
);
/** function task_js(callback){...} */
/** function task_css(callback){...} */

function uploadQiniu(callback) {
  gulp
    .src([files /** filespath */])
    .pipe(
      qiniu(
        {
          accessKey: ACCESSKEY,
          secretKey: SECRETKEY,
          bucket: BUCKET,
          private: false
        },
        {
          dir: "release/",
          versioning: true,
          recordInFile: "./staticfiles.json"
        }
      )
    )
    .on("finish", callback);
}
```
