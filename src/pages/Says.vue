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
      <ul class="local_collection_items" v-if="says.length">
      <li 
        v-for="(item, index) in says"
        v-bind:item="item"
        v-bind:index="index"
        v-bind:key="item.id"
      >
        <card>
        <img slot="header" :src="item.img" style="width:100%;display:block;">
          <div slot="content" class="card-padding">
            <p style="color:#999;font-size:12px;">{{ item.date }}</p>
            <p style="font-size:14px;line-height:1.2;">{{ item.title }}</p>
          </div>
        </card>
        <divider></divider>
    </li>
    <ul>
    </div>
    <c-footer></c-footer> 
  </div>
</template>
<script>
import CNewslist from "../components/Newslist.vue";
import CFooter from "../components/Footer.vue";
import CBack from "../components/Back.vue";
import axios from "axios";
import { mapState, mapMutations } from "vuex";
import { Swiper, GroupTitle, SwiperItem, XButton, Divider, Card } from "vux";
import http from "@/service/http";
import api from "@/config/api";

export default {
  data() {
    return {
      collection_tag: "initial",
      direction: "",
      ifModal: false,
      id: "",
      says: [],
      params: {} //筛选条件参数
    };
  },
  methods: {
    //获取数据
    fetchData: async function(params) {
      http.post(api.getList, params).then(response => {
        this.says = response.data.data;

      });
    }
  },
  components: {
    Swiper,
    SwiperItem,
    CFooter,
    CBack,
    CNewslist,
    Card,
    Divider
  },
  mounted() {
    this.fetchData(this.params);
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
</style>

