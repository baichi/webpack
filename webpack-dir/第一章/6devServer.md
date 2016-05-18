
## 6.devServer

刚才我们看到，在运行webpack-dev-server的时候，后面带了一串参数，这里我们可以使用devServer字段统一在webpack.config.js文件里面维护。

```
/* webpack.config.js */
var path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
    },
    devServer: {
      publicPath: "/static/",
      stats: { colors: true },
      port: 8080,
      contentBase: 'build',
      inline: true
    },
    module: {
      loaders: [
        {
          test: /\.js$/,
          loader: 'babel-loader'
        }
      ]
    }
};

```

同时，我们可以简化scripts字段的配置了
```
"scripts": {
    "dev": "./node_modules/.bin/webpack-dev-server"
}
```

对应的修改index.html文件中的资源引用地址
```
<script src="/static/bundle.js"></script>
```

ok, npm run dev即可

另外，也有同学问到，怎么mock数据呢，我们可以用proxy代理的方式。


```
var path = require('path');

function rewriteUrl(replacePath) {
  return function (req, opt) {
    var queryIndex = req.url.indexOf('?');
    var query = queryIndex >= 0 ? req.url.substr(queryIndex) : "";

    req.url = req.path.replace(opt.path, replacePath) + query;
    console.log("rewriting ", req.originalUrl, req.url);
  };
}

module.exports = {
    entry: {
      index: "./src/index.js"
    },
    output: {
      publicPath: "/static/",
      path: path.resolve(__dirname, "build"),

      filename: "bundle.js"
    },
    devServer: {
      publicPath: "/static/",
      stats: { colors: true },
      port: 8080,
      contentBase: 'build',
      inline: true,
      proxy: [
          {
            path: /^\/api\/(.*)/,
            target: "http://localhost:8080/",
            rewrite: rewriteUrl('/$1\.json'),
            changeOrigin: true
          }
      ]
    },

};

```

更多请看[这里](http://webpack.github.io/docs/webpack-dev-server.html)