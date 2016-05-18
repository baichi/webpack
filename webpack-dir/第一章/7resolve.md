
## 7.resolve

resolve下常用的是extension和alias字段的配置：
- extension 不用在require或是import的时候加文件后缀
```
/* webpack.config.js */
resolve: {
    extensions: ["", ".js", ".jsx", ".css", ".json"],
},
```

```
/* src/component.js */

export default () => {
  alert('component');
}

```

```
/* src/index.js */
'use strict';

import React, { Component } from 'react';
import ReactDOM from 'react-dom';

import component from './component';

component();

class HelloWorld extends Component {
  render(){
    return (
      <h1>Hello world</h1>
    )
  }
}

ReactDOM.render(<HelloWorld />, document.getElementById('app'));

```

刷新看到运行效果，而此时import的时候直接没有写文件后缀。

- alias 配置别名，加快webpack构建的速度

```
var path = require('path');

var pathToReact = path.join(__dirname, "./node_modules/react/dist/react.js");
var pathToReactDOM = path.join(__dirname, "./node_modules/react-dom/dist/react-dom.js");

module.exports = {
    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
    },
    devServer: {
      publicPath: "/static/",
      stats: { colors: true },
      port: 3000,
      contentBase: 'build',
      inline: true
    },
    resolve: {
      extensions: ["", ".js", ".jsx", ".css", ".json"],
      alias: {
        'react': pathToReact,
        'react-dom': pathToReactDOM
      }
    },
    module: {
      loaders: [
        {
          test: /\.js$/,
          loader: 'babel-loader'
        }
      ],
      noParse: [pathToReact, pathToReactDOM]
    }
};

```

我们这里做了两件事情：
1.每当 "react" 在代码中被引入，它会使用压缩后的 React JS 文件，而不是到 node_modules 中找。
2.每当 Webpack 尝试去解析那个压缩后的文件，我们阻止它，因为这不必要。
