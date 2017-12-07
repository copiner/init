### package scripts

npm run xxx，可以执行package.json里script对应的命令，并且是shell脚本。但是在执行的时候有一个小处理。

>npm run新建的这个 Shell，会将当前目录的node_modules/.bin子目录加入PATH变量，执行结束后，再将PATH变量恢复原样。

### sample
```
scripts: {
  "prebuild" : "echo \" this is pre build \"",
  "build" : "echo \" this is build \"",
  "postbuild" : "echo \" this is post build \""
}
```
npm run build

```
> init@1.0.0 prebuild E:\Keypoint\init
> echo " this is pre build "

" this is pre build "

> init@1.0.0 build E:\Keypoint\init
> echo " this is build "

" this is build "

> init@1.0.0 postbuild E:\Keypoint\init
> echo " this is post build "

" this is post build "

```
### 默认值
npm会默认设置一些script的值，比如`start`和`install`，当然你可以覆盖这2个值。

>如果你在项目里根目录有一个server.js，然后你又没自己定义start script，那么npm run start，就会执行server.js

可以设置prestart 和poststart脚本
```
"prestart" : "echo \" this is pre start \"",
"poststart" : "echo \" this is post start \""
```
npm run start
```
​
> test-npm-script@1.0.0 prestart /Users/jan/workspace/web/test-npm-script
> echo " this is pre start "
​
 this is pre start
​
> test-npm-script@1.0.0 start /Users/jan/workspace/web/test-npm-script
> node server.js
​
this is server.js
​
> test-npm-script@1.0.0 poststart /Users/jan/workspace/web/test-npm-script
> echo " this is post start "
​
 this is post start
```

### install

当你的模块被安装时，会默认执行这个脚本。前提是你没自己定义install脚本，然后有一个binding.gyp 文件。具体的npm会执行

```
"install": "node-gyp rebuild"
```
这个脚本可以帮助node模块编译 c++ 模块。

### restart
restart脚本比较特殊，如果你设置了restart脚本则只会执行：prerestart, restart, postrestart，但是如果你没有设置restart，则会执行stop，start脚本。比如我们设置如下脚本配置。
```
"scripts": {
    "prestop" : "echo \" this is pre stop \"",
    "stop" : "echo \" this is stop \"",
    "poststop" : "echo \" this is post stop \"",
​
    "prestart" : "echo \" this is pre start \"",
    "start" : "echo \" this is start \"",
    "poststart" : "echo \" this is post start \"",

    "prerestart" : "echo \" this is pre start \"",
    "postrestart" : "echo \" this is post start \"",
  }
```
npm run restart
```
this is pre restart
this is pre stop
this is stop
this is post stop
this is pre start
this is start
this is post start
this is post restart

```

### 简写
有几个简写：
```
npm start === npm run start
npm stop === npm run stop
npm test === npm run test
npm restart === npm run rerestart
```

### package.json
```
{
  "name": "test-npm-script",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "bin" : {
    "main":"bin/main.js",
    "dev":"bin/dev.js"
  },
  "scripts": {
    "pretest" : "echo \" this is pre test \"",
    "test" : "echo \" this is test \"",
    "posttest" : "echo \" this is post test \"",
​
    "prerestart" : "echo \" this is pre restart \"",
    "restart" : "echo \" this is restart \"",
    "postrestart" : "echo \" this is post restart \"",

    "prestop" : "echo \" this is pre stop \"",
    "stop" : "echo \" this is stop \"",
    "poststop" : "echo \" this is post stop \"",
​
    "prestart" : "echo \" this is pre start \"",
    "start" : "echo \" this is start \"",
    "poststart" : "echo \" this is post start \"",
​
    "preinstall" : "echo \" this is pre install \"",
    "install" : "echo \" this is install \"",
    "postinstall" : "echo \" this is post install \"",
​
    "prepublish" : "echo \" this is pre install \"",
    "publish" : "echo \" this is publish \"",
    "postpublish" : "echo \" this is post install \"",
​
    "preuninstall" : "echo \" this is pre uninstall \"",
    "uninstall" : "echo \" this is uninstall \"",
    "postuninstall" : "echo \" this is post uninstall \"",

    "prebuild" : "echo \" this is pre build \"",
    "build" : "echo \" this is build \"",
    "postbuild" : "echo \" this is post build \""
  },
  "author": "",
  "license": "ISC"
}　
```
