## Electron 桌面应用
- Electron 是一个可以将网页打包桌面应用平台 并且可以使用纯 JavaScript 调用丰富的原生 APIs
- electron-builder是Electron打包各类系统(MacOS, Windows和Linux)与“自动更新”的工具

## 特性
- 打造第一个 Electron 案例;
- 通过electron-builder 将 Electron案例 制作成 Windows程序 以及 安装包

## 创建第一个Electron案例

大体上，目录结构如下：
```bash
your-app/
├── package.json
├── main.js
└── index.html
```

#新建index.html

```bash
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	这是我的第一个Electron 应用~
</body>
</html>
```


#新建package.json

```bash
{
  "name": "electron-builder-real",
  "version": "1.0.0",
  "description": "#",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "test": "echo \"Error: no test specified\" && exit 1",
    "postinstall": "electron-builder install-app-deps",
    "pack": "electron-builder --dir",
    "dist": "electron-builder"
  },
  "build": {
    "appId": "your.id",
    "mac": {
      "category": "your.app.category.type"
    }
  },
  "devDependencies":{
    "electron": "^1.7.9",
    "electron-builder": "^19.37.2"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
#新建main.js

```bash
const electron = require('electron'); // 控制应用生命周期的模块。
const app = electron.app; // 创建原生浏览器窗口的模块
const BrowserWindow = electron.BrowserWindow;

// 保持一个对于 window 对象的全局引用，不然，当 JavaScript 被 GC，
// window 会被自动地关闭
var mainWindow = null;

// 当所有窗口被关闭了，退出。
app.on('window-all-closed', function() {
  // 在 OS X 上，通常用户在明确地按下 Cmd + Q 之前
  // 应用会保持活动状态
  if (process.platform != 'darwin') {
    app.quit();
  }
});

// 当 Electron 完成了初始化并且准备创建浏览器窗口的时候
// 这个方法就被调用
app.on('ready', function() {
  // 创建浏览器窗口。
  mainWindow = new BrowserWindow({width: 800, height: 600});

  // 加载应用的 index.html
  mainWindow.loadURL('file://' + __dirname + '/index.html');

  // 打开开发工具
  mainWindow.openDevTools();

  // 当 window 被关闭，这个事件会被发出
  mainWindow.on('closed', function() {
    // 取消引用 window 对象，如果你的应用支持多窗口的话，
    // 通常会把多个 window 对象存放在一个数组里面，
    // 但这次不是。
    mainWindow = null;
  });
});
```

### 安装依赖
```bash
$ npm install
```

### 启动 案例
```bash
$ npm start
```

### electron-builder 打包
```bash
$ npm run dist
```
#打包成功后会出现程序文件夹和一个安装包

###温馨提示：
###  1.此案例及打包是针对快速完成为主,如需设置图标-系统64位等具体参数可通过其他资料获取；
###  2.在打包的过程偶尔会出现因墙内、网速、断包等因素导致失败，可删除dist文件夹重新执行打包命令；
###  3.此案例是通过多个资料整理得出的，如需要了解更多请看下面资料链接；
###  4.此案例已亲测多次通过，有其他问题或者交流可发送到我的Email(422972230@qq.com);

###相关链接：
###  [electron](https://electron.atom.io)。
###  [electron-builder](https://www.npmjs.com/package/electron-builder)。
