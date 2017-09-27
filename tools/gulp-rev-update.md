## gulp静态资源版本号 {#gulp静态资源版本号}

> 手动修改gulp插件——最新版

原始代码

```js
<link rel="stylesheet" href="../css/default.css">
<script src="../js/app.js"></script>
```

1. 打开node\_modules\gulp-rev\index.js

```js
第144行:
manifest[originalFile] = revisionedFile;
更新为: 
manifest[originalFile] = originalFile + '?v=' + file.revHash;
```

1. 打开node\_modules\rev-path\index.js

```js
10行:
return filename + '-' + hash + ext;
更新为:
return filename + ext;
```

1. 打开node\_modules\gulp-rev-collector\index.js

```js
40行:
let cleanReplacement =  path.basename(json[key]).replace(new RegExp( opts.revSuffix ), '' );
更新为: 
let cleanReplacement =  path.basename(json[key]).split('?')[0];
```

最终结果

```js
<link rel="stylesheet" href="../css/default.css?v=5a636d79c4">
<script src="../js/app.js?v=3a0d844594"></script>
```



