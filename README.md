# fecs-loader [![Build Status](http://img.shields.io/travis/MoOx/eslint-loader.svg)](https://travis-ci.org/MoOx/eslint-loader)
fecs loader (for webpack) —— webpack中的fecs检查工具
## Usage
安装fecs-loader

```shell
$ npm install fecs-loader
```
如果less/css/js文件都check，可直接在原有webpack.config.js配置中的module.loaders的基础上加多一项

```js
{
    test: /\.(less|css|js)$/,
    loader: 'fecs-loader'
}
```
或者只针对某一类文件check，可在原有的loader配置中添加loader，如：

```js
{
    test: /\.js$/,
    loader: 'fecs-loader'
},
{
    test: /\.css$/,
    loader: 'style-loader!css-loader!fecs-loader'
},
{
    test: /\.less$/,
    loader: 'style-loader!css-loader!less-loader!fecs-loader'
}
```
因为webpack的loader调用的顺序是从后往前的，所以为了fecs-loader能check最原始的代码，请将fecs-loader放置在数组or叹号相连的loader中的最后

## Options
可以直接将参数加在loader后，形如```fecs-loader?key=value```，也可以将参数罗列在webpack.config.js全局配置中形如：

```js
module: {
	fecs: {
		key: value
	}
}
```
建议将参数写在全局配置中
### ```faileOnError```(default: false)
是否在fecs检测到模块内容有error时使模块编译失败，若failOnError为true则模块内容遇到fecs error时模块内容将不出现在编译结果中
### ```faileOnWarning```(default: false)
是否在fecs检测到模块内容有warning时使模块编译失败，若failOnWarning为true则模块内容遇到fecs warning时模块内容将不出现在编译结果中
### ```exclude```（default: ''）
指定要忽略的```glob```文件模式，如```./index.js``````./index.js,./src/config/*.js```，文件模式若有多条，模式之间使用逗号```,```分隔


### Example

```
module.exports = {
    module: {
        loaders: [
            {test: /\.(less|css|js|vue)$/, loader: 'fecs-loader'}
        ]
    },
    fecs: {
        failOnError: true,
        failOnWarning: true,
        exclude: './index.js,./index2.js'
    }
};

```
