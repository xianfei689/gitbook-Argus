# main.js

```coffeescript
import Vue from 'vue'
import 'normalize.css/normalize.css' // A modern alternative to CSS resets
import Element from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import '@/styles/index.scss' // global css
import './assets/iconfont/iconfont.js'
import app from './app'
import router from './router'
import store from './store'
import argusServerConfig from 'argusServerConfig'
import i18n from './lang' // Internationalization
import axios from 'axios';
import './icons' // icon
import './errorLog' // error log
import './permission' // permission control
// import './mock' // simulation data
import * as filters from './filters' // global filters
import basicContainer from './argus/basic-container/main'
Vue.component('basicContainer', basicContainer)

Vue.use(Element, {
  i18n: (key, value) => i18n.t(key, value)
})

// register global utility filters.
Object.keys(filters).forEach(key => {
  Vue.filter(key, filters[key])
})

Vue.prototype.argusServerConfig = argusServerConfig;
axios.defaults.withCredentials = true;
Vue.prototype.$http = axios;

Vue.config.productionTip = false
new Vue({
  el: '#app',
  router,
  store,
  i18n,
  render: h => h(app)
})

```

