##  2.Vendor chunk 应用代码和第三方代码分离

修改webpack配置中的entry入口，并且添加CommonsChunkPlugin插件抽取出第三方资源。

代码清单：`webpack.config.js`
```
entry: {
 index: [
    'webpack/hot/dev-server',
    'webpack-dev-server/client?http://localhost:8080',
    path.resolve(__dirname, 'src/index.js')
  ],
  vendor: ['react', 'react-dom']
},
plugins: [
   new webpack.HotModuleReplacementPlugin(),
   new webpack.NoErrorsPlugin(),
   new webpack.optimize.CommonsChunkPlugin('vendor', 'vendor.js'),
   new ExtractTextPlugin("bundle.css")
 ]
```

同时我们还有修改index.html文件的引用。
代码清单：`build/index.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>React Demo</title>
  <link rel="stylesheet" href="bundle.css">
</head>
<body>
  <div id="app"></div>
  <script src="vendor.js"></script>
  <script src="index.js"></script>
</body>
</html>

```