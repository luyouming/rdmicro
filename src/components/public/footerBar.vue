<template>
<div class="footer-container">
  <div class="footerInfo">
    <div class="footerBox">
      <img class="imgPic" :src="require(`$static/icon/logo-mens.png`)" alt="">
      <p class="paragraph">苏州研材微纳科技有限公司成立于2015年，是一家专门从事半导体、MEMS、生物芯片等方面耗材和委托加工业务的科技创新公司。</p>
      <!-- <div><img class="iconPic" v-for="(item, index) in footerIcons" :key="item + index" :src="require(`$static/icon/${item}`)" alt=""></div> -->
    </div>
    <div class="footerBox">
      <div class="title">
        <div >公司动态</div>
        <div><span class="left"></span><span class="right"></span></div>
      </div>
      <div class="newsBox" @click="gotoNews(item)" v-for="(item, index) in footerNews" :key="item + index">
        <img :src="item.src" alt="">
        <div class="news">
          <p class="title">{{item.title}}</p>
          <p class="content">{{item.time}}</p>
        </div>
      </div>
    </div>
    <div class="footerBox">
      <div class="title">
        <div >联系方式</div>
        <div><span class="left"></span><span class="right"></span></div>
      </div>
      <div class="contactWay">
        <p class="main" :class="{longMain: item.name === '地址'}" v-for="(item, index) in footerContactWay" :key="item + index">
        <span class="name" :class="{longInfo: item.name === '地址'}">{{item.name + ':'}}</span> <span :class="{longInfo: item.name === '地址'}" class="tel">{{item.contactWay}}</span>
        </p>
      </div>
    </div>
  </div>
  <div class="Tips">
    <p>苏ICP备18021576号-1&演示系统&</p>
    <!-- <p>本站暂为&演示系统&使用，请勿用于正式运营</p> -->
    <p>版权所有 © 2011-2020 苏州研材微纳科技有限公司</p>
  </div>
  </div>
</template>

<script>
import commonInfo from "@/assets/CommonJs/commonInfo";
export default {
  name: 'FooterBar',
  data () {
    return {
      footerIcons: ['person.png','person.png','person.png','person.png'],
      footerNews: commonInfo.latestNews,
      footerContactWay: [{name: '咨询热线', contactWay: '0512-68636965'},
                        //  {name: '联系人-冒小姐', contactWay: '18360485933'},
                         {name: '传真', contactWay: '0512-62872362'},
                         {name: '网址', contactWay: 'www.memstools.cn'},
                         {name: '邮箱', contactWay: 'sales@rdmicro.com'},
                         {name: '地址', contactWay: '江苏省苏州市工业园区若水路398号  中科院苏州纳米所B705'},]
    }
  },
  mounted() {
    console.log(commonInfo.latestNews)
  },
  methods: {
    gotoNews(info){
      // window.scrollTo(0, 0)
      // this.$router.push({ path: '/news/all' });
      this.$router.push('/news/details/' + info.id)
      setTimeout(() => {
        document.documentElement.scrollTop = 0
      }, 100)
    }
  }
}
</script>

<style lang="scss" scoped>
.footer-container{
  .footerInfo {
    background-color: #000;
    display: flex;
    flex-direction:row;
    justify-content: center;
    align-items: flex-start;
    font-size: 26PX;
    color: white;
    min-height: 580px;
    // padding: 120px 0 0 0;
    .footerBox{
      width: calc(100% / 3);
      // height: 100%;
      margin-top: 120px;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: flex-start;
      color: #bbb;
      padding: 0 80px 90px 80px;
      .imgPic{
        width: 210PX;
        height: 150PX;
        // margin-bottom:-30PX;
      }
      .paragraph{
        text-align: left;
        font-size: 18PX;
        line-height: 22PX;
        font-family: "微软雅黑";
        font-weight: 300;
        margin: 30px 0;
      }
      div {
        .iconPic{
          width: 32px;
          height: 32px;
          border: 1px solid skyblue;
          border-radius: 10px;
          margin-right: 30px;
        }
      }
      .title{
        width: 100%;
        div {
          font-size: 24PX;
          color: #ffffff;
          font-weight: bold;
          letter-spacing: 2px;
          font-family: "微软雅黑";
          text-align: left;
          width: 100%;
          margin-bottom: 15px;
          .left, .right{
            display: block;
            background-color: #00c3ed;
            height: 4px;
            width: 75px;
            float: left;
          }
          .right{
            width: calc(100% - 80px);
            background-color: rgba(65, 65, 65, 0.3);
          }
        }
     }
     .newsBox{
        width: 100%;
        margin: 20px auto;
        cursor:pointer;
        img {
          float: left;
          width: 120PX;
          height: 90PX;
          border-radius: 2px;
        }
        .news {
           float: left;
           width: calc(100% - 120PX);
           padding: 0 20px;
           height: 45PX;
           line-height: 45PX;
           text-align: left;
           box-sizing: border-box;
           .title{
             font-weight: 500;
             font-size: 18PX;
             font-family: "微软雅黑";
             line-height: 28PX;
             color: #ccc;
           }
           .content{
             color: #666;
             font-family: "微软雅黑";
             font-weight: 500;
             font-size: 14PX;
           }
        }
      }
      .contactWay{
        width: 100%;
        .main{
          font-size: 18PX;
          line-height: 1PX;
          padding: 15PX 0;
          border-bottom: 1px solid #444;
         .name{
          float: left;
          font-family: "微软雅黑";
          font-weight: 300;
         }
        .tel{
          float: right;
          color: #ccc;
        }
        .longInfo{
          width: 100%;
          text-align: left;
          height: 25PX;
          line-height: 25PX;
        }
       }
       .longMain{
         padding: 10px 0 0 0;
         border: none;
       }
        

      }
    }
  }
  .Tips{
    width: 100%;
    min-height: 60PX;
    line-height: 60PX;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    background: rgb(42, 42, 42);
    color: #bbb;
    padding: 0 160px;
    box-sizing: border-box;
    p{
      font-size: 18PX;
    }
  }
}
// 移动端
@media screen and (max-width: 1200px) {
      .footer-container {
        .footerInfo{
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          align-items: center;
          .footerBox{
            width: 80%;
            .newsBox > .news > .title{
              font-size: 14PX;
            }
          }
        }
        // .newsBox{
        //   .img{
        //     width: 200px;
        //     height: 150px;
        //   }
        // }
        .contactWay{
          margin-bottom: 40PX;
          .main{
            margin: 30px 0;
            padding-bottom:55px !important;
          }
        }
        // 移动端字体需要大一些展示的时候
        .Tips{
          p{
            font-size: 15PX;
            line-height: 15PX;
            width: 50%;
            padding: 0;
          }
        }
      }
    }
</style>