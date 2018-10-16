# lpay

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
    成功回调
    this.$refs.lpay.success();
    失败回调
    this.$refs.lpay.error();
```

## API
|参数|说明|类型|默认值|
|:---|:---|:---|:---|
|isShow|组件的显示隐藏|Boolean|false|
|digit|密码框位数|Number|6|
|title|弹窗标题|String|请输入支付密码|
|loadingText|正在支付的文字提示|String|正在支付|
|finishedText|支付成功的文字提示|String|支付成功|
|duration|支付成功的提示显示时间|Number|500|

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
