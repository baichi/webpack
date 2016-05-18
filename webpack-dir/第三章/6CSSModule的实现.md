## 6.CSS Module的实现

webpack 的 css-loader 是解决这个问题的最好办法之一。简单配置一下：

```
module: {
  loaders: [{
    test: /\.css$/,
    loaders: [
      'style-loader',
      'css-loader?modules&localIdentName=[name]__[local]___[hash:base64:5]',
      'postcss-loader'
    ]
  }]
},
postcss: [
  require('postcss-nested')(),
  require('cssnext')(),
  require('autoprefixer-core')({ browsers: ['last 2 versions'] })
]
```
然后把下面的代码交给 webpack：

`js`
```
import styles from './ChatMessage.css';

class ChatMessage extends React.Component {
  render() {
    return (
      <div className={styles.root}>
        <img src="http://very.cute.png" />
        <p className={styles.text}> woooooow </p>
      </div>
    );
  }
}
```

`css`
```
.root {
  background-color: #f0f0f0;
  > img {
    width: 32px;
    height: 32px;
    border-radius: 16px;
  }
}

.text {
  font-size: 22px;
}
```

最后输出

`HTML`
```
<div class="ChatMessage__root__1aF8de0">
  <img src="http://very.cute.png" />
  <p class="ChatMessage__text__fo40mmi"> woooooow </p>
</div>
```

`CSS`
```
.ChatMessage__root__1aF8de0 {
  background-color: #f0f0f0;
}
.ChatMessage__root__1aF8de0 > img {
  width: 32px;
  height: 32px;
  border-radius: 16px;
}
.ChatMessage__text__fo40mmi {
  font-size: 22px;
}
```

简而言之，我们通过编译期 renaming 的方式为 CSS 引入了局部变量。