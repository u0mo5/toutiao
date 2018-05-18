<template>
  <div>
    <c-back class="header"></c-back>
    <div class="content">
      <swiper auto height="100px">
      <swiper-item class="black"><h2 class="title fadeInUp animated">它无孔不入</h2></swiper-item>
      <swiper-item class="black"><h2 class="title fadeInUp animated">你无处可藏</h2></swiper-item>
      <swiper-item class="black"><h2 class="title fadeInUp animated">不是它可恶</h2></swiper-item>
      <swiper-item class="black"><h2 class="title fadeInUp animated">而是它不懂你</h2></swiper-item>
      <swiper-item class="black"><h2 class="title fadeInUp animated">我们试图</h2></swiper-item>
      <swiper-item class="black"><h2 class="title fadeInUp animated">做些改变</h2></swiper-item>
      </swiper>




      <!-- start -->

      <!-- end -->



  <div class="demo-list-box" id="demo_list_box" :style="{height: `${height}px`}">
      <flexbox :gutter="0" v-for="(row,i) in listTemp" >
        <flexbox-item :span="1/3"  v-for="(cell,j) in row" class="cbox vux-1px-t vux-tap-active" @click.native="go(cell.uri.toLowerCase(), cell.action)">
          <div class="vux-1px-r cbox-inner">
            <span class="demo-icon demo-icon-big"  :style="{color: cell.color}">
              <img :src="cell.icon" class="img-icon" />
    
            </span>
            <br>
            <span :style="{fontSize: cell.length > 12 ? '12px' : ''}">{{cell.media_name | camelCase}}</span>
          </div>
        </flexbox-item>
      </flexbox>
    </div>

<iframe scrolling="no" frameborder="0" allowtransparency="true" src="http://i.tianqi.com/index.php?c=code&id=36&icon=5&num=5"></iframe>  


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
          content: ("Do you agree?"),
          onShow() {
            console.log("Module: I'm showing");
          },
          onHide() {
            console.log("Module: I'm hiding now");
          }
        });
      } else if (!action) {
        this.$router.push(`${name}`);
      } else{
        this.$router.push(`${name}`);
      }
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
    this.fetchData(this.params);
    this.height = window.innerHeight - 46 - 53;
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

