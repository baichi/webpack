## 5.使用Babel-loader来解析es6和jsx

我们在src/index.js里面尝试写一个最基本的组件代码，暂时不用理会代码为什么要这么写，这里先把ES6语法和JSX语法加进来，用于跑通我们的开发环境，后续会有专题内容来详细讲述。

代码清单：`src/index.js`
```
'use strict';

import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class HelloWorld extends Component {
  render(){
    return (
      <h1>Hello world</h1>
    )
  }
}

ReactDOM.render(<HelloWorld />, document.getElementById('app'));
```

ok，我们看到，我们的代码用到了基本的react.js和react-dom.js，而且使用的是ES6的语法来封装的组件和应用模块。

所以接下来我们要做两件事：
1. 下载相应的模块：
```
$ npm install --save react react-dom
```
2. 下载并配置babel，以解析ES6语法和JSX语法。

babel是一款强大的解析器，拥有活跃而且完善的生态，不仅可以做JS相关的各种语法的解析，还提供丰富的插件功能。

```

$ npm install babel-loader babel-core --save-dev
```

安装后我们需要配置webapck.config.js文件

代码清单：`webpack.config.js`
```
var path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
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

这里指定了使用babel-loader来解析js文件，但是并没有告诉babel应该如何来解析，所以我们需要创建一个babelrc配置文件

```
$ touch .babelrc
```

然后编辑babelrc
代码清单：`.babelrc`
```
{
  "presets": ["es2015", "react", "stage-0"],
  "plugins": []
}
```

为什么配置的是这两个参数，解释一下，配置的preset字段是在为babel解析做预设，告诉babel需要使用相关的预设插件来解析代码，plugins字段，顾名思义，就是用来配置使用babel相关的插件的，这里暂且按下不表。

这里使用到了三个预设需要下载安装
```
$ npm install --save-dev babel-preset-es2015 babel-preset-react babel-preset-stage-0
// 其中stage-0预设是用来说明解析ES7其中一个阶段语法提案的转码规则
```

到这里我们可以重新来运行一次webpack以查看效果，为方便运行，我们把webpack-dev-server的相关代码放到package.json的script里面去

代码清单：`package.json`

```
"scripts": {
    "dev": "./node_modules/.bin/webpack-dev-server --progress --colors --content-base build"
}
```

好了，开始运行试一下吧

```
$ npm run dev
```

在浏览器中访问：`http://localhost:8080/`