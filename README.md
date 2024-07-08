

小程序一键上传脚本，开发者可不打开小程序开发者工具，独立使用 wx-ci 进行小程序代码的打包、上传等操作。

## 安装

### 方式一：全局安装（**推荐**）

使用前你需要安装 `wx-ci`脚手架工具:

```console
npm install wx-ci -g
```

或者

```console
yarn global add wx-ci
```

查看版本，表示安装成功

```console
wx-ci -v
```

### 方式二：本地安装

```console
npm install wx-ci --save-dev
```

或者

```console
yarn  add wx-ci -D
```

查看版本，表示安装成功

```console
npx wx-ci -v
```

## 快速开始

### 快速生成配置文件

```console
wx-ci init
```

执行完成后，会在当前目录生成 wxci.config.js 配置文件，**各参数含义均有备注，也可参考本文档**

### 上传版本

在 package.json 同级目录执行上传流程

#### 上传体验版本

```console
wx-ci upload
```

#### 上传预览版本

```console
wx-ci preview
```

执行这段脚本，如果最后提示上传成功，恭喜，小程序已经成功上传啦！

如果需要关闭**命令行输入版本号和上传描述**
可以增加参数选项`-q` 开启静默模式

```console
wx-ci upload -q
```

此时将不再提示手动输入版本号及上传描述，而是读取配置文件的上传描述

如果需要指定特定文件作为配置文件
可以增加参数选项`-f` 指定文件

```console
wx-ci upload -f <filename>
```

此时将使用指定的文件作为 wx-ci 配置文件

## 可用配置

你可以根据项目需要手动修改`wx-ci`.
可配置选项如下
|字段名|类型|必填|默认值|描述|
|:--:|:--:|:-----:|:--------:|:----------:|
|**`title`**|`{String}`|false|正在上传小程序|显示上传标题语句|
|**`appid`**|`{String}`|true|-|小程序 appid|
|**`type`**|`{String}`|true|miniProgram|请勿修改|
|**`projectPath`**|`{String}`|true|dist|小程序生成目录|
|**`privateKeyPath`**|`{String}`|true|miniprogram.upload.key|小程序钥匙目录，需要在小程序后台下载|
|**`previewMode`**|`{Boolean}`|false|false|是否是小程序预览模式|
|**`previewConfig`**| [previewConfig](https://www.npmjs.com/package/miniprogram-ci#%E5%8F%82%E6%95%B0-1) |false|false|小程序预览模式配置|
|**`preCommand`**|`command[]`|false|[]|上传小程序源码前执行的脚本|
|**`version`**|`{String}`|false|1.0.0|小程序默认上传的版本号(上传时可修改)|
|**`desc`**|`{String}`|false|{m}月{day}日更新|小程序默认上传的备注信息(上传时可修改)|
|**`noQuestions`**|`{Boolean}`|false|false|上传时不显示问题|
|**`setting`**|`setting`|false|{}|小程序每次上传的项目配置信息|
|**`robot`**|`{Number}`|false|1|小程序每次上传的项目配置信息|
|**`qrcodeFormat`**|`{String}`|false|{}|返回二维码文件的格式 "image" 或 "base64"， 默认值 "terminal" 供调试用|
|**`qrcodeOutputDest`**|`{String}`|true|{}|二维码文件保存路径|
|**`scene`**|`{Number}`|false|{}|[见场景值列表](https://developers.weixin.qq.com/miniprogram/dev/reference/scene-list.html)|
|**`searchQuery`**|`{String}`|false|{}|预览页面路径启动参数|

`command`可配置选项如下

|    字段名     |    类型    | 必填  | 默认值 |      描述      |
| :-----------: | :--------: | :---: | :----: | :------------: |
| **`command`** | `{String}` | true  |   -    |   执行的命令   |
|  **`desc`**   | `{String}` | false |   -    | 执行命令的描述 |

`setting`可配置选项如下

|        字段名        |    类型     | 必填  | 默认值 |                            描述                             |
| :------------------: | :---------: | :---: | :----: | :---------------------------------------------------------: |
|      **`es6`**       | `{boolean}` | false |  true  |          对应于微信开发者工具的 "es6 转 es6" es5"           |
|      **`es7`**       | `{boolean}` | false | false  |              对应于微信开发者工具的 "增强编译"              |
|    **`minifyJS`**    | `{boolean}` | false | false  |                     上传时压缩 JS 代码                      |
|   **`minifyWXML`**   | `{boolean}` | false | false  |                    上传时压缩 WXML 代码                     |
|   **`minifyWXSS`**   | `{boolean}` | false | false  |                    上传时压缩 WXSS 代码                     |
|     **`minify`**     | `{boolean}` | false | false  | 上传时压缩所有代码，对应于微信开发者工具的 "上传时压缩代码" |
|  **`codeProtect`**   | `{boolean}` | false | false  |         对应于微信开发者工具的 "上传时进行代码保护"         |
| **`autoPrefixWXSS`** | `{boolean}` | false | false  |         对应于微信开发者工具的 "上传时样式自动补全"         |

默认配置表如下:

```js
module.exports = {
  /** ---基础配置-- */
  //显示上传标题语句
  title: '----------正在上传小程序----------',
  //小程序appid
  appid: '',
  type: 'miniProgram',
  //小程序生成目录
  projectPath: 'dist',
  //小程序钥匙目录
  privateKeyPath: 'miniprogram.upload.key',
  /** ---上传前执行脚本-- */
  preCommand: [
    {
      command: 'yarn',
      desc: '安装依赖',
    },
    {
      command: 'yarn build',
      desc: '打包',
    },
  ],
  /** ---上传配置-- */
  //小程序自定义版本号
  version: '',
  //小程序自定义备注
  desc: '',
  //编译设置
  setting: {
    //对应于微信开发者工具的 "es6 转 es5"
    es6: true,
    //对应于微信开发者工具的 "增强编译"
    es7: false,
    //上传时压缩 JS 代码
    minifyJS: false,
    //上传时压缩 WXML 代码
    minifyWXML: false,
    //上传时压缩 WXSS 代码
    minifyWXSS: false,
    //上传时压缩所有代码，对应于微信开发者工具的 "上传时压缩代码"
    minify: true,
    //对应于微信开发者工具的 "上传时进行代码保护"
    codeProtect: false,
    //对应于微信开发者工具的 "上传时样式自动补全"
    autoPrefixWXSS: false,
  },
  //指定使用哪一个 ci 机器人，可选值：1 ~ 30
  robot: 1,
  //返回二维码文件的格式 "image" 或 "base64"， 默认值 "terminal" 供调试用
  qrcodeFormat: 'terminal',
  //二维码文件保存路径
  qrcodeOutputDest: 'destination.jpg',
  //见场景值列表
  scene: '',m
  //预览页面路径启动参数
  searchQuery: '',
};
```