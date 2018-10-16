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
    <lpay ref="lpay"
          v-model:show="show"
          @close="close"
          @forget="forget"
          @input-end="toOptions">
    </lpay>
```

## API
|列名1|列名2|
|:---|:---|
|列1的内容1|列2的内容1|
|列1的内容2|列2的内容2|

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
