
## 9.devtool


我们在配置中新增devtool字段，并设置值为source-map，这样我们就可以在浏览器中直接调试我们的源码，在控制台的sources下，点开可以看到`webpack://`目录，点开有惊喜哦。

代码清单：`webpack.config.js`
```
devtool: 'cheap-module-source-map'
```

devtool可以有几个配置项：

|devtool|	build speed	| rebuild speed	|production supported |quality|
|---|---|---|---|---|
|eval|	+++	|+++	|no	|generated code|
|cheap-eval-source-map	|+|	++|	no|	transformed code (lines only)|
|cheap-source-map|	+	|o	|yes|	transformed code (lines only)|
|cheap-module-eval-source-map|	o	|++|	no|	original source (lines only)|
|cheap-module-source-map	|o|	-	|yes|	original source (lines only)|
|eval-source-map|	–	|+	|no|	original source|
|source-map|	–|	–	|yes	|original source|
