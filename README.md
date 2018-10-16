# vue-pay

> 测试插件

## 插件安装
```javascript
npm i lpay
```
## 引入插件
```javascript
import Vue from 'vue';
import lpay from 'lpay';

Vue.use(lpay);
```

## 基本用法
```javascript
    <vpay ref="vpay"
          v-model:show="show"
          @close="close"
          @forget="forget"
          @input-end="toOptions">
    </vpay>
```

## API
| 事件名 | 说明 | 参数 |
| - | :- | :- | :-: |
| input-end | 密码输入完成后的回调函数 | - |
| close | 密码弹窗关闭后的回调函数 | - |
| forget | 点击忘记密码的回调函数 | - |

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
