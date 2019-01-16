# vue.config.js

```coffeescript
module.exports = {
  //   lintOnSave：{ type:Boolean default:true } 问你是否使用eslint
  lintOnSave: process.env.NODE_ENV !== 'production',

  // productionSourceMap：{ type:Bollean,default:true } 生产源映射
  // 如果您不需要生产时的源映射，那么将此设置为false可以加速生产构建
  productionSourceMap: false,

  configureWebpack: {
    entry: {
      argusServerConfig: '@/config/serverConfig'
    }
  },
  chainWebpack: config => {
    config.externals({
      vue: 'Vue',
      'vue-router': 'VueRouter',
      vuex: 'Vuex',
      axios: 'axios',
      'element-ui': 'ELEMENT',
      argusServerConfig: 'argusServerConfig'
    })
    // 一个规则里的 基础Loader
    // svg是个基础loader
    const svgRule = config.module.rule('svg')
    // 清除已有的所有 loader。
    // 如果你不这样做，接下来的 loader 会附加在该规则现有的 loader 之后。
    svgRule.uses.clear()
    // 添加要替换的 loader
    svgRule
      .use('svg-sprite-loader')
      .loader('svg-sprite-loader')
      .options({
        symbolId: 'icon-[name]'
      })
  },

  devServer: {
    port: 8085, // 端口号
    host: 'localhost',
    https: false, // https:{type:Boolean}
    open: true, //配置自动启动浏览器
    // proxy: 'http://localhost:4000' // 配置跨域处理,只有一个代理
    proxy: {
      '/api': {
        target: '<url>',
        ws: true,
        changeOrigin: true
      },
      '/foo': {
        target: '<other_url>'
      }
    } // 配置多个代理
  }
}

```

