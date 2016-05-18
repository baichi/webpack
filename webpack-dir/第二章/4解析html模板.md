## 4.HTML Webpack Plugin 解析html模板


前面我们还是先在build目录手动加上的index.html，这样在项目中不是很适用，因为我们希望build产出的资源应该是通过工具来统一产出并发布上线，这样质量和工程化角度来思考是更合适的。下面我们来实现。

在src目录下新建一个index.html文件，并写上简单的代码。
```
$ cd src && touch index.html
```
代码清单：`src/index.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>React课堂demo</title>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

接下来需要下载一个webpack的插件html-webpack-plugin。
```
$ npm install --save-dev html-webpack-plugin
```

修改webpack配置。
代码清单：`webpack.config.js`
```
// 引用这个plugin
var HtmlWebpackPlugin = require('html-webpack-plugin');

// 这里省略其他配置代码

plugins: [
	  // 使用这个plugin，这是最简单的一个配置，更多资料可到github查看
      new HtmlWebpackPlugin({
        title: 'zhufeng-react',
        template: './src/index.html',
      })
]
```

ok，运行`npm run dev`跑一遍，效果正常。
