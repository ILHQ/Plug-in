<template>
  <div>
    <button @click="show = true">open</button>
    <vpay ref="vpay"
          v-model:isShow="isShow"
          @close="close"
          @forget="forget"
          @input-end="toOptions"></vpay>
  </div>
</template>
<script>
//  import vpay from '../test/pay.vue'
  export default {
    components: {
//      vpay
    },
    computed: {},
    data() {
      return {
        isShow: false
      };
    },
    methods: {
      forget() {
        console.log('forget');
      },
      close() {
        console.log('close');
      },
      toOptions() {
        setTimeout(() => {
          this.$refs.vpay.error();
        }, 1000)
//        setTimeout(() => {
//          this.$refs.vpay.success();
//        }, 1000)
      }
    },
    created() {
    },
    mounted() {
    },
    watch: {}
  };
</script>
<style lang="scss">
</style>
