<template>
  <div class="AboutUs-container DefaultContainerStyle">
    <title-bar text="关于我们" />
    <!-- 关于我们的介绍 -->
    <div class="introduction">
       <p> <span class="title">苏州研材微纳科技有限公司</span>是专门从事半导体、MEMS、生物芯片等方面耗材和委托加工业务的科技创新公司。</p>
       <p>公司提供各类微细加工服务和工艺流程设计咨询，为各大科研院所提供多种单项加工或综合类器件开发服务。公司与国内多家研究单位和公司机构有长期的委托加工合作关系，设备齐全，服务及时，适合各类加工需求。</p>
       <p>主要从事半导体和MEMS领域微细加工设备的销售。公司目前主要销售的产品是晶圆键合设备、晶圆喷胶设备、基础工艺设备和检测设备等半导体先进工艺设备。</p>
       <p>公司主要业务面向国内科研院所和高校、以及科技创新型的中小企业，帮助客户实现最快速度取得最优质量的科研和生产用耗材。公司目前经营的产品有各类委托加工、设备、硅片、特殊衬底、光刻胶、高纯度试剂、超净耗材、货源优质，响应速度快，国内外货源充实。</p>
       <p>公司拥有一只高素质的服务队伍，长期从事微细加工领域的工作，致力于帮助广大科研和科技创新工作者实现梦想，为您提供最全面最优质的服务。公司已与国内众多知名科研单位进行了广泛的业务合作，高质量的产品与服务为我们赢得了良好的信誉，期待更多的用户能够和我们建立更长久的合作关系。</p>
    </div>
     <!-- 产品海报图 -->
    <div class="content">
      <div class="provideGoodPro">
      <img :src="require(`$assets/CommonImg/HomePage/companyPic.jpg`)" alt="">
      </div>
    </div>
    <!-- 友情链接 -->
    <div class="friendLink" v-if="false">
      <span>友情链接:</span>
      <img @click="gotoFriendNet" :src="require(`$assets/CommonImg/AboutUs/friendLink.png`)" alt="">
    </div>
  </div>
</template>

<script>
import titleBar from "$components/public/titleBar";
export default {
  name: "aboutUsAbout",
  components: { titleBar },
  methods: {
    gotoFriendNet() {
      window.location.href = 'http://www.baidu.com'
    }
  }
};
</script>

<style scoped lang="scss">
.AboutUs-container {
   display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 width: 100%;
 .introduction{
   box-sizing: border-box;
   padding: 0 130px;
   margin-top: 120px;
   color: #000;
   max-width: 18rem;
   background-color: #fff;
   padding: 80px;
   p{
     text-align: left;
    //  font-family: "Ping Fang SC";
    //  height: 50px;
    //  line-height: 50px;
    //  font-size: 30px;
     color: rgb(0, 0, 0);
    font-family: "Ping Fang SC";
    font-size: 15.6pt;
    letter-spacing: 0pt;
    line-height: 24pt;
    text-indent: 28pt;
    font-weight: 300;
    .title{
      font-size: 24pt;
      font-weight: bold;
    }
   }
 }
 .content {
    width: 100%;
    .provideGoodPro{
      box-sizing: border-box;
      padding: 0 130px;
      margin: 120px 0;
      img{
        width: 100%;
        max-width: 18rem;
        height: 100%;
      }
    }
 }
 .friendLink{
   width: 100%;
   height: 500px;
   background:#0B2F57;
   display: flex;
   justify-content: center;
   align-items: center;
   span{
    //  display: inline-block;
    font-size: 36px;
    padding-top: 60px;
    color: #ccc;
   }
   img{
     cursor: pointer;
     height: 260px;
     width: 350px;
   }
 }
}
// 移动端
    @media screen and (max-width: 1200px) {
      .AboutUs-container{
        .content {
         .provideGoodPro{
           img{
             width: 100%;
             height: 6rem;
           }
         }
        }
      }
    }
</style>