

## 2.Hot Module Replacement 模块热替换

webpac-dev-server支持Hot Module Replacement，即模块热替换，在前端代码变动的时候无需整个刷新页面，只把变化的部分替换掉。使用HMR功能也有两种方式：命令行方式和Node.js API。


```
// 1.cli命令行方式
webpack-dev-server --inline --hot
```


```
// 2.Node.js API方式
entry: [
  'webpack/hot/dev-server',
  path.resolve(__dirname, 'src/index.js')
],
devServer: {
  hot: true
},
plugins: [
  new webpack.HotModuleReplacementPlugin(),
]

```

更多内容可以参见[这篇文章](http://www.jianshu.com/p/941bfaf13be1)，文章将webpack官网上对webpack-dev-server的代码刷新部分的介绍进行了翻译。
