---
layout: post
title: "webpack打包入门教程"
date: 2016-06-28 20:05:01
category: android
tags: [webpack, 打包, 入门教程]
---
最近学习React Native开发，了解了不少相关知识。顺便尝试了一下webpack，总结了几点其基本用法。<!-- more -->

####  一、单个文件打包

```
webpack test.js bundle.js
```

指定输入文件为test.js，打包输出文件为bundle.js。

#### 二、多个文件打包

多个js或相关文件时，输入文件指定为js入口文件，如main.js中require了common.js模块:

```
//main.js
require('style-loader!css-loader!./css/main.css');
require('./common.js');
```

打包命令是：

```
webpace  main.js bundle.js 
```

即只需指定入文件文件main.js。

#### 三、使用相应loader

如require时css使用了css-loader条件，(二)中提到的在require时可指定loader，但不推荐这样做。 使用命令行执行webpack可以通过--module-bind指定loader，如下：

```
webpack main.js bundle.js --module-bind "css=style-loader!css-loader" --progress --display-modules --display-reasons 
```

#### 四、配置webpack.config.js

除了直接在命令行中指定输出，输出等参数来打包，还可以通过设置配置文件来完成。配置webpack打包的config.js文件，然后运行：

```
webpack --config webpack.config.js
```

来打包。当配置文件为webpack.config.js，可省掉--config选项，直接运行webpack。

#### 五、配置示例

```
/webpack.config.js
module.exports={
	entry:{
		index:'./src/main.js',
	},
	output:{
		path:'./dist',
		filename:'bundle.js'
	},
	resolve: {
        extensions: ['', '.js', '.jsx', '.css']
    },
    module: {	
		loaders: [
				{ 
					test: /\.css$/, 
					loader: "style-loader!css-loader" 
				},
				{ 
					test: /\.js$/, 
					loader: 'babel-loader'
				},
				{ 
					test: /\.jsx$/, 
					loader: 'babel?presets[]=react&presets[]=es2015' 
				},
			]
    }
}
```
