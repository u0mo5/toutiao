<template>
  <div>
    <c-back class="header"></c-back>
    <div class="content">

        <!-- 详情{{this.$route.query.link}} -->

      <!-- start -->

      <!-- end -->

    <iframe v-show="iframeState" id="show-iframe" frameborder=0 name="showHere" scrolling=auto src=""></iframe>


<!-- sdf -->
    </div>
    <c-footer></c-footer> 
  </div>
</template>
<script>
import collectlist from "../../static/apps.json";
console.log(collectlist);
import { Flexbox, FlexboxItem } from "vux";
import { AlertModule } from "vux";
import CNewslist from "../components/Newslist.vue";
import CFooter from "../components/Footer.vue";
import CBack from "../components/Back.vue";
import axios from "axios";
import { mapState, mapMutations } from "vuex";
import { Grid, GridItem } from "vux";
import { Swiper, GroupTitle, SwiperItem, XButton, Divider, Card } from "vux";
import http from "@/service/http";
import api from "@/config/api";
export default {
  data() {
    return {
      iframeState: false,
      goBackState: false,
      list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      params: {}, //筛选条件参数
      height: 10,
      length: 12
    };
  },
  computed: {
    listTemp: function() {
      var list = this.list;
      var arrTemp = [];
      var index = 0;
      var sectionCount = 3;
      for (var i = 0; i < list.length; i++) {
        index = parseInt(i / sectionCount);
        if (arrTemp.length <= index) {
          arrTemp.push([]);
        }
        arrTemp[index].push(list[i]);
      }
      return arrTemp;
    }
  },

  methods: {
    //获取数据
    fetchData: async function(params) {
      // http.post("api.getList", params).then(response => {
      //   this.list = response.data.data.slice(0,9);
      // });
      this.list = collectlist.data.slice(0, 9);
    },
    go(name, action) {
      console.log(action);
      if (action == "alert") {
        AlertModule.show({
          title: "VUX is Cool",
          content: "Do you agree?",
          onShow() {
            console.log("Module: I'm showing");
          },
          onHide() {
            console.log("Module: I'm hiding now");
          }
        });
      } else if (!action) {
        this.$router.push(`${name}`);
      } else {
        this.$router.push(`${name}`);
      }
    },
    offIframe() {
      this.goBackState = false;
      this.iframeState = false;
    },
    showIframe() {
      this.goBackState = true;
      this.iframeState = true;
    }
  },
  components: {
    Swiper,
    SwiperItem,
    CFooter,
    CBack,
    CNewslist,
    Card,
    Divider,
    Grid,
    GridItem,
    Flexbox,
    FlexboxItem
  },
  mounted() {
    console.log("mounted");
    console.log(this.$route.query.link);
    const oIframe = document.getElementById('show-iframe');
    const deviceWidth = document.documentElement.clientWidth;
    const deviceHeight = document.documentElement.clientHeight;
    oIframe.style.width = deviceWidth + 'px';
    oIframe.style.height = deviceHeight + 'px';
   


    this.showIframe();
    let link=this.$route.query.link;
    console.log(link);
    document.getElementById('show-iframe').src=""+link;//跳转
    // document.getElementById('show-iframe').contentWindow.location.reload(true);
     console.log("mounted ok");
     console.log( document.getElementById('show-iframe'));
    // window.location.reload();

            // DOM is now updated
            //改变iframe src的值试试

   
  },
  beforeUpdate(){
    console.log("beforeUpdate");

  },
  destroyed(){
    console.log("destory");
    this.offIframe();
    console.log("destory ok");
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/common.scss";

.copyright {
  font-size: 12px;
  color: #ccc;
  text-align: center;
}
.text-scroll {
  border: 1px solid #ddd;
  border-left: none;
  border-right: none;
}
.text-scroll p {
  font-size: 12px;
  text-align: center;
  line-height: 30px;
}
.black {
  background-color: #000;
}
.title {
  line-height: 100px;
  text-align: center;
  color: #fff;
}
.animated {
  animation-duration: 1s;
  animation-fill-mode: both;
}
.vux-indicator.custom-bottom {
  bottom: 30px;
}
@-webkit-keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 100%, 0);
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 100%, 0);
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
.fadeInUp {
  animation-name: fadeInUp;
}
.swiper-demo-img img {
  width: 100%;
}

.cbox {
  text-align: center;
}
.cbox-inner {
  padding: 15px 0;
  width: 100%;
  height: 100%;
}
.demo-list-box {
  margin-bottom: 10px;
  background-color: #fff;
  width: 100%;
  overflow: scroll;
  -webkit-overflow-scrolling: touch;
}
.img-icon {
  width: 50%;
  height: 50%;
}
</style>

