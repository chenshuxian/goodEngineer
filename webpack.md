# webpack 前端自動化打包器
webpack 問題集:
----
1. 如何將 jquery 其他的 plugins 放到 CommonsChunkPlugin 中。  
```
  一般在 chunks 中會自動對映 entry 中的名字，然後預設會從 node_modules
  中找出，若不是 npm 內有的模塊，就需要用 alias 自行定義，這時在進行
  chunk 時就會到我們所指定的資料夾下去找出，然後進行封裝。
  new webpack.optimize.CommonsChunkPlugin({
    name: 'vender',   //對映 entry 中的 vender[]
    // minChunks: Infinity
    filename: 'commons.js'
    // chunks: ['jquery']
  }),
  entry: {
    index: `./public/js/test.js`,
    vender: ['jquery', 'ui', 'alert']
  },
  resolve: {
    alias: {
      alert: `${publicJs}/commons/jquery.alerts.js`,
      ui: "./public/js/commons/jquery.ui.draggable.js"
    }
  }
```
這個 plugin 主要的目的，是將共用的模塊組合原一個 js，減少其子模塊重
覆引用，同時也可以減少 http request 請求。  
2. 進行 CommonsChunkPlugin 後，出現 jQuery is not defined。
```
Provide Plugin 的主要功能是當在程式中遇到特定字元且沒被定義時會
自動載入特定模組。上例的設定是在碰到 $，jQuery，window.jQuery
或 root.jQuery 時都載入 jquery 套件。所以，當在某檔案中不定義
$ 直接使用 $("#item") 時，程式不會報錯。

還需要注意的第三方的 plugins 最好不要用 min 的不然有可能在進行
ProvidePlugin 替換時還是會失敗。

  //webpack.config.js

  //...other webpack settings

  plugins: [
      new Webpack.ProvidePlugin({
          $: 'jquery',
          jQuery: 'jquery',
          'window.jQuery': 'jquery',
          'root.jQuery': 'jquery'
      }),
  ]

```
3. webpack breakpoint 無法使用
```
妖瘦生為一個前端工程師，breakpoint 等同廢人，但好在找到解決方法了，
解決方法如下:
//webpack.config.js 中加這個就行了，但只能在 chrome 上用。
//網路也有很多人碰到同樣問題，可上以下網址找自己的解答:
//https://github.com/webpack/webpack/issues/2145
devtool: '#inline-source-map'
```
