<template>
  <div>
    <c-back class="header"></c-back>
    <div class="content">


    <div v-for="src in list" style="background-color:white;text-align:center;">
      <span style="font-size:20px;">Loading</span>
      <x-img :src="src" :webp-src="`${src}?type=webp`" @on-success="success" @on-error="error" class="ximg-demo" error-class="ximg-error" :offset="-100" container="#vux_view_box_body"></x-img>
    </div>


      <!-- <c-loadmore :flag="loadmoreSession" :ifFlag="ifReturnSession" @event="$store.dispatch('getSession')"></c-loadmore> -->
    </div>
    <c-footer></c-footer>
  </div>
</template>
<script>
import CFooter from '../components/Footer.vue'
import CBack from '../components/Back.vue'
import CLoadmore from '../components/Loadmore.vue'
import { XImg } from 'vux'
// import { mapState } from 'vuex'


import { Group, Cell } from 'vux'
import { Card } from 'vux'


export default {
  components: {
    Group,
    Cell,
    CFooter,
    CBack,
    CLoadmore,
    Card,
    XImg
  },
    methods: {
    success (src, ele) {
      console.log('success load', src)
      const span = ele.parentNode.querySelector('span')
      ele.parentNode.removeChild(span)
    },
    error (src, ele, msg) {
      console.log('error load', msg, src)
      const span = ele.parentNode.querySelector('span')
      span.innerText = 'load error'
    }
  },
  data () {
    return {
      list: [
        'https://o5omsejde.qnssl.com/demo/test1.jpg',
        'https://o5omsejde.qnssl.com/demo/test2.jpg',
        'https://o5omsejde.qnssl.com/demo/test0.jpg',
        'https://o5omsejde.qnssl.com/demo/test4.jpg',
        'https://o5omsejde.qnssl.com/demo/test5.jpg',
        'https://o5omsejde.qnssl.com/demo/test6.jpg',
        'https://o5omsejde.qnssl.com/demo/test7.jpg',
        'https://o5omsejde.qnssl.com/demo/test8.jpg'
      ]
    }
  }
}
</script>

<style>
.ximg-demo {
  width: 100%;
  height: auto;
}
.ximg-error {
  background-color: white;
}
.ximg-error:after {
  content: '加载失败';
  color: red;
}
</style>

