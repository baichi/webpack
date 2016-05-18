
## 3.Common chunk 提取出应用中公共的代码

```

module.exports = {
  entry: {
    bundle1: './a.jsx',
    bundle2: './b.jsx'
  },
  output: {
    filename: '[name].js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      },
    ]
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin('init.js')
  ]
}
```
