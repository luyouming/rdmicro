<template>
  <div class="swiper-Box">
    <!-- v-show="activeIndex === 2" -->
    <div class="back1" @click="gotoNews(0)" v-show="activeIndex !== 2">
      <p class="title"><span class="year">2018</span>公司举办了</p>
      <p class="award">"研材微纳杯"</p>
      <p class="award">优秀论文征集活动</p>
    </div>
    <div class="back2" @click="gotoNews(1)" v-show="activeIndex === 2">
      <div>
      <p class="title">2017年"研材微纳杯"</p>
      <p class="award">论文征集活动获奖名单</p>
      </div>
    </div>
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="slide in imglist" :key="slide.id">
          <img :src="slide.src" />
        </div>
      </div>
      <div class="swiper-pagination"></div>
    </div>
  </div>
</template>

<script>
import config from "@/config/index";
import "swiper/dist/css/swiper.css";
import Swiper from "swiper";
import commonInfo from "@/assets/CommonJs/commonInfo";

export default {
  props: {
    imglist: {
      type: Array,
      default: () => [
        { id: "1", src: `${config.swiperImgUrl}first.png` },
        { id: "2", src: `${config.swiperImgUrl}second.jpg` },
        { id: "3", src: `${config.swiperImgUrl}third.jpg` }
      ]
    }
  },
  data() {
    return {
      msg: "hello，轮播图",
      activeIndex: 0,
      newsInfo: commonInfo.latestNews
    };
  },
  mounted() {
    // 初始化swiper插件
    this.initSwiper();
  },
  methods: {
    initSwiper() {
      var that = this
      var mySwiper = new Swiper(".swiper-container", {
        loop: true,
        pagination: ".swiper-pagination",
        onSlideChangeEnd: function(swiperHere) {
          // console.log(swiperHere.activeIndex);
          that.activeIndex = swiperHere.activeIndex
        },
        paginationClickable: true, // 点击切换
        autoplay: 5000,
        preventLinksPropagation: true,
        autoplayDisableOnInteraction: false
      });
      if (mySwiper) {
        this.msg = "初始化轮播图成功";
      }
    },
    gotoNews(index){
      if(!this.newsInfo || !this.newsInfo[index]) {
        console.log('没有这条新闻')
      }
      this.$router.push('/news/details/' + this.newsInfo[index].id)
      setTimeout(() => {
        document.documentElement.scrollTop = 0
      }, 100)
    }
  }
};
</script>

<style lang="scss" >
.swiper-Box {
  width: 100%;
  // height: 600PX;
  height:auto;
  position: relative;
  .back1 {
    position: absolute;
    z-index: 3;
    top: .75rem;
    left: 20PX;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: flex-start;
    cursor: pointer;
    .title{
      color: rgb(0, 195, 237);
      font-size: 0.9rem;
      font-weight: 500;
      padding: 15px;
      font-family: "微软雅黑";
      border-left: 8px solid rgb(0, 195, 237);
      border-top: 3px solid rgb(0, 195, 237);
      background: #333;
      animation: bottomEaseInAnimate 2s ease 1; /*调用动画：动画名、时间、时间线条、播放次数*/
    animation-fill-mode: forwards;/*定义动画结束的状态*/
      .year{
       font-size: 0.8rem;
       font-weight: bold;
      }
    }
    .award{
      text-align: left;
      color: #fff;
      font-size: 1.6rem;
      font-weight: 800;
      font-family: "微软雅黑";
      animation: topEaseInAnimate 2s ease 1; /*调用动画：动画名、时间、时间线条、播放次数*/
    animation-fill-mode: forwards;/*定义动画结束的状态*/
    }
  }
  .back2 {
    position: absolute;
    width: 100%;
    height: 100%;
    cursor: pointer;
    z-index: 3;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    // .back2 > div{
    //   border:1px solid red;
    // }
    .title{
      color: rgb(0, 195, 237);
      font-size: .9rem;
      font-weight: 500;
      padding: 15px;
      font-family: "微软雅黑";
      margin: auto;
      max-width: 500PX;
      border-top: 5px solid rgb(0, 195, 237);
      background: #333;
      animation: rightEaseInAnimate 2s ease 1; /*调用动画：动画名、时间、时间线条、播放次数*/
      animation-fill-mode: forwards;/*定义动画结束的状态*/
    }
    .award{
      color: #fff;
      font-size: 1.8rem;
      font-weight: 800;
      font-family: "微软雅黑";
      animation: leftEaseInAnimate 2s ease 1; /*调用动画：动画名、时间、时间线条、播放次数*/
    animation-fill-mode: forwards;/*定义动画结束的状态*/
    }
  }
 
  /* 以下是swiper的轮播图 */
  .swiper-container {
    width: 100%;
    // height: 600PX;
    height:auto;
    display: block;

    .swiper-slide img {
      width: 100%;
      // height: 100%;
      height:auto;
      min-height:500PX;
    }
    .swiper-wrapper {
      // height: 600PX;
      height:auto;
    }
    .swiper-slide {
      text-align: center;
      background: #fff;
      /* Center slide text vertically */
      display: -webkit-box;
      display: -ms-flexbox;
      display: -webkit-flex;
      display: flex;
      -webkit-box-pack: center;
      -ms-flex-pack: center;
      -webkit-justify-content: center;
      justify-content: center;
      -webkit-box-align: center;
      -ms-flex-align: center;
      -webkit-align-items: center;
      align-items: center;
    }
    .swiper-pagination {
      margin-bottom: 15px;
      .swiper-pagination-bullet {
        display: inline-block;
        width: 20px;
        height: 20px;
        border-radius: 0;
        background: #666;
      }
    }
    .swiper-pagination-bullet-active {
      background: #fff !important;
    }
  }
}
// 移动端
    @media screen and (max-width: 1200px) {
      .swiper-Box {
        height: 300PX;
        .swiper-container {
          height: 300PX;
          .swiper-wrapper {
           height: 300PX;
          }  
        }
        .back2, .back1{
          .title{
            font-size: 0.8rem;
            .year{
            font-size: 0.8rem;
          }
          }
            .award{
              font-size: 1.0rem;
            }
          }
      }
    }
    // and (max-width:2400px)  pc端 这里不需要上限
    @media screen and (min-width:1200px){
      .swiper-Box {
        height: 600PX;
        .swiper-container {
          height: 600PX;
          .swiper-wrapper {
           height: 600PX;
          }  
        }
      }
    }
 @keyframes rightEaseInAnimate{/*定义从右边滑入文字的动画*/
    0%{transform: translateX(400px);opacity: 0;}
    100%{transform:translateX(0px);opacity: 1; }
}
 @keyframes leftEaseInAnimate{/*定义从左边滑入文字的动画*/
    0%{transform: translateX(-400px);opacity: 0;}
    100%{transform:translateX(0px);opacity: 1; }
}
 @keyframes topEaseInAnimate{/*定义从上边滑入文字的动画*/
    0%{transform: translateY(200px);opacity: 0;}
    100%{transform:translateY(0px);opacity: 1; }
}
 @keyframes bottomEaseInAnimate{/*定义从下边滑入文字的动画*/
    0%{transform: translateY(-200px);opacity: 0;}
    100%{transform:translateY(0px);opacity: 1; }
}
</style>