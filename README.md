## 初识webpack
webpack默认配置文件webpack.config.js
可以通过webpack --config指定配置文件

entry 打包入口文件
ouput 打包的输出
mode 打包环境
module rules loader配置
plugins 插件配置

## 环境搭建：安装webpack
安装node和npm
初始化仓库 `npm init -y`
安装webpack和webpack-cli
`npm i webpack webpack-cli --save-dev`
检查安装情况 `./node_modules/.bin/webpack -v`

## 第一个例子
新建webpack.config.js文件
``` js
'use strict'
const path = require('path');

module.exports = {
    mode:'production',
    entry: './main.js',
    output: {
        path: path.join(__dirname,'dist'),
        filename: 'bundle.js'
    }
};
```

自定义命令
``` json
"scripts": {
    "build": "webpack"
},
```
执行`npm run build`进行打包

# webpack基础用法
## entry
用来指定打包入口
- 单入口
一般是单页面应用，entry是一个字符串
- 多入口
entry是一个对象

## output
将编译的文件输出到磁盘
如果是多入口，打包后的文件名filename需要使用`[name]`占位
``` js
const path = require('path');
module.exports = {
    mode:'production',
    entry: {
        index : './main.js',
        main1: './main1.js'    },
    output: {
        path: path.join(__dirname,'dist'),
        filename: '[name].js'
    }
};
```

## loader
支持其他类型文件并且转化为有效模块
本身是一个函数，接受源文件为参数，返回转化结果
- babel-loader转换ES6、ES7等新特性语法
- css-loader支持.css文件的加载和解析
- file-loader进行图片字体的打包
- raw-loader将文件以字符串形式导入
- thread-loader多进程打包css和js


## plugins
插件用于bundle文件优化，资源管理和环境变量注入
作用于整个构建过程
- CommonsChunkPlugin 将chunks相同的模块代码提取成公共js
- CleanWebpackPlugin 清理构建目录
- HtmlWebpackPlugin 创建html文件承载输出的bundle
- UglifyWebpackPlugin 压缩js

## mode
mode用来指定当前的构建环境是：production、development、none
设置mode可以使用webpack内置的函数，默认为production




