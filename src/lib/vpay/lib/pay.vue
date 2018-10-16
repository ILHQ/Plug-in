<template>
  <div class="pay_box" v-if="isShow">
    <div class="content">
      <div class="title">
        <i class="iconfont icon-back" @click="cancel"></i>
        <span>
          {{title}}
        </span>
        <i></i>
      </div>
      <div class="position">
        <div class="pay_content">
          <div class="pwd-box">
            <ul class="pass-area">
              <li class="pass-item"
                  :class="{on: password.length > index}"
                  v-for="(item, index) in digit"
                  :key="index"></li>
            </ul>
          </div>
          <div class="forget" @click="forget">
            <span>忘记密码?</span>
          </div>
        </div>
        <ul class="keyboard">
          <li class="key" v-for="(item, index) in keyboard" :key="index" @click="onKeyboard(item.num)">
            <p class="num"><strong>{{item.num}}</strong></p>
            <p class="character">{{item.English}}</p>
          </li>
          <li class="key option">
          </li>
          <li class="key last" @click="onKeyboard(0)">
            <p class="num"><strong>0</strong></p>
          </li>
          <li class="key last option delete" @click="deleteNum">
            <i class="iconfont icon-delete1"></i>
          </li>
        </ul>
        <div class="loading-box" v-if="payStatus !== 0">
          <div class="center" v-if="payStatus === 1">
            <img class="loading" src="./static/image/loading.png" alt="">
            <p>{{loadingText}}</p>
          </div>
          <div class="center" v-if="payStatus === 2">
            <img class="success" src="./static/image/success.png" alt="">
            <p>{{finishedText}}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="prompt-box" v-if="fileStatus">
      <div class="tips-box">
        <p class="title">支付密码不正确</p>
        <div class="flex-box">
          <span class="left" @click="reInput">重新输入</span>
          <span class="right" @click="forget">忘记密码</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import './static/iconfont.css';

  export default {
    model: {
      prop: 'isShow',
      event: 'change'
    },
    props: {
      isShow: {
        type: Boolean,
        required: true,
        default: false,
      },
      // 支付密码框位数
      digit: {
        type: Number,
        default: 6
      },
      // 弹窗标题
      title: {
        type: String,
        default: '请输入支付密码'
      },
      // 正在支付的文字提示
      loadingText: {
        type: String,
        default: '正在支付'
      },
      // 支付成功的文字提示
      finishedText: {
        type: String,
        default: '支付成功'
      },
      // 支付成功的提示显示时间
      duration: {
        type: Number,
        default: 500
      }
    },
    components: {},
    computed: {},
    data() {
      return {
        payStatus: 0, // 支付状态 0未支付 1正在支付 2支付成功
        password: '',
        keyboard: [
          {
            num: 1
          },
          {
            num: 2,
            English: 'ABC'
          },
          {
            num: 3,
            English: 'DEF'
          },
          {
            num: 4,
            English: 'GHI'
          },
          {
            num: 5,
            English: 'JKL'
          },
          {
            num: 6,
            English: 'MNO'
          },
          {
            num: 7,
            English: 'PQRS'
          },
          {
            num: 8,
            English: 'TUV'
          },
          {
            num: 9,
            English: 'WXYZ'
          }
        ],
        fileStatus: false // 支付失败
      };
    },
    methods: {
      onKeyboard(key) {
        this.password = (this.password + key).slice(0, this.digit);
      },
      deleteNum() {
        if (this.password) {
          this.password = this.password.slice(0, this.password.length - 1);
        }
      },
      cancel() {
        // 支付过程中，不允许取消支付
        if (this.payStatus !== 0) return false;
        // 清空密码
        this.password = '';
        // 恢复支付状态
        this.payStatus = 0;
        // 关闭组件，并触发父子组件数据同步
        this.$emit('change', false);
        // 触发父组件close自定义事件
        this.$emit('close');
      },
      //支付成功
      success() {
        return new Promise((resolve, reject) => {
          this.payStatus = 2;
          setTimeout(() => {
            this.cancel();
            resolve();
          }, this.duration);
        })
      },
      error() {
        return new Promise((resolve, reject) => {
          this.fileStatus = true;
          this.payStatus = 0;
          resolve();
        })
      },
      reInput() {
        this.password = '';
        this.payStatus = 0;
        this.fileStatus = false;
      },
      forget () {
        this.password = '';
        this.payStatus = 0;
        this.fileStatus = false;
        // 关闭组件，并触发父子组件数据同步
        this.$emit('change', false);
        this.$emit('forget');
      }
    },
    created() {
    },
    mounted() {
    },
    watch: {
      password(newVal) {
        if (newVal.length === this.digit) {
          this.payStatus = 1;
          this.$emit('input-end', this.password)
        }
      }
    }
  };
</script>
<style lang="scss">
  .pay_box {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    font-size: 28px;
    background-color: rgba(128, 128, 128, 0.6);
    ul{
      list-style: none;
      margin: 0;
      padding: 0;
    }
    p{
      margin: 0;
      padding: 0;
    }
    .content {
      position: fixed;
      left: 0;
      bottom: 0;
      width: 100%;
      .title {
        width: 100%;
        height: 80px;
        padding: 0 20px 0 10px;
        box-sizing: border-box;
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 1px solid #b5b5b5;
        background-color: #fafafa;
        .icon-back {
          font-size: 30px;
        }
      }
      .pay_content{
        background-color: #fafafa;
        .pwd-box {
          padding: 40px 20px 20px 20px;
          box-sizing: border-box;
          display: flex;
          justify-content: center;
          .pass-area{
            border: 1px solid #b5b5b5;
            border-radius: 10px;
            height: 80px;
            .pass-item{
              position: relative;
              display: inline-block;
              width: 115px;
              height: 80px;
              border-right: 1px solid #b5b5b5;
              &.on::after{
                content: "";
                position: absolute;
                left: 50%;
                top: 50%;
                width: 16px;
                height: 16px;
                background: #000;
                border-radius: 50%;
                transform: translate(-50%, -50%);
              }
              &:last-child{
                border: none;
              }
            }
          }
        }
        .forget{
          padding: 0 20px 80px 30px;
          text-align: right;
          color: #0083e3;
        }
      }
      .keyboard{
        display: flex;
        flex-wrap: wrap;
        background-color: #fff;
        .key{
          width: 33.333%;
          height: 90px;
          text-align: center;
          border-right: 1px solid #d5d5d5;
          border-bottom: 1px solid #d5d5d5;
          box-sizing: border-box;
          &:nth-child(3n){
            border-right: none;
          }
          .num{
            font-size: 36px;
          }
          .character{
            font-size: 24px;
          }
          .icon-delete1{
            font-size: 50px;
            color: #000;
          }
          &.last{
            display: flex;
            justify-content: center;
            align-items: center;
          }
          &.option{
            background-color: #d1d5db;
          }
          &.delete{
            &:active{
              border-bottom: 0;
              background-color: #fff;
            }
          }
          &:active{
            border-bottom: 0;
            background-color: #d1d5db;
          }
        }
      }
      .position {
        position: relative;
        .loading-box {
          position: absolute;
          left: 0;
          top: 0;
          width: 100%;
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;
          background-color: #fff;
          .center{
            text-align: center;
            .loading{
              height: 60px;
              width: 60px;
              animation: rotate 0.6s linear infinite;
            }
            .success{
              height: 60px;
              width: 60px;
            }
            @keyframes rotate {
              0% {
                transform: rotate(0)
              }
              50% {
                transform: rotate(180deg)
              }
              100% {
                transform: rotate(360deg)
              }
            }
          }
        }
      }
    }
    .prompt-box{
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(128, 128, 128, 0.6);
      .tips-box{
        position: absolute;
        left: calc(50% - 225px);
        top: 50%;
        width: 450px;
        height: 150px;
        background-color: #fff;
        border-radius: 20px;
        .title{
          text-align: center;
          line-height: 80px;
          border-bottom: 1px solid #b5b5b5;
        }
        .flex-box{
          height: 70px;
          display: flex;
          align-items: center;
          justify-content: space-around;
          font-size: 32px;
          width: 100%;
          span{
            flex: 1;
            line-height: 70px;
            text-align: center;
          }
          .left{
            border-right: 1px solid #d5d5d5;
          }
          .right{
            color: #0083e3;
          }
        }
      }
    }
  }
</style>
