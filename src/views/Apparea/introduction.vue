<template>
  <div class="Apparea-intro-container">
    <title-bar :text="prodInfo.name" />
    <div class="contentBox">
      <!-- <img :src="require(`$assets/CommonImg/AppArea/${prodInfo.imgUrl}`)" alt="">
      <p>{{prodInfo.desc}}</p>-->
      <img :src="require(`$assets/CommonImg/AppArea/${prodInfo.imgUrl}`)" alt />
      <div class="news">
        <p class="content">
          <span>产品名称:</span>
          <span>{{prodInfo.desc}}</span>
        </p>
        <p class="content">
          <span>基片尺寸:</span>
          <span>{{prodInfo.size}}</span>
        </p>
        <p class="content">
          <span>适用材料:</span>
          <span>{{prodInfo.material}}</span>
        </p>
        <p class="content">
          <span>适用工艺:</span>
          <span>{{prodInfo.technique}}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import titleBar from "$components/public/titleBar";
import commonInfo from "@/assets/CommonJs/commonInfo";
export default {
  name: "appareaIntroduction",
  data() {
    return {
      productList: commonInfo.productList,
      prodInfo: {
        id: "1",
        name: "生物芯片",
        desc: "生物芯片专用设备",
        size: "200mm * 100mm",
        material: "硅胶纳米材料",
        technique: "工艺23432",
        iconUrl: `product1.png`,
        imgUrl: `appArea1.jpg`,
        discription:
          "产品描述产产品描述产产品描述产品描述产品描述产品描述产品描述产品描述"
      }
    };
  },
  components: { titleBar },
  mounted() {
    this.initInfo();
  },
  methods: {
    initInfo() {
      this.id = this.$route.params.id;
      const info = this.productList.find(a => a.id === this.id);
      this.prodInfo = info || this.productList[0];
      console.log(this.prodInfo);
    }
  }
};
</script>

<style scoped lang="scss">
.Apparea-intro-container {
  width: 100%;
  .contentBox {
    width: 100%;
    height:350PX;
    padding: 0 130px 60PX 130px;
    box-sizing: border-box;
    margin: 60PX auto;
    img {
      float: left;
      width: 8rem;
      height: 280PX;
      border-radius: 2PX;
    }
    .news {
      float: left;
      width: calc(100% - 8rem);
      padding: 0 20px;
      height: 90px;
      line-height: 90px;
      text-align: left;
      box-sizing: border-box;
      .title {
        font-weight: 500;
        font-size: 25PX;
        font-family: "微软雅黑";
        line-height: 28PX;
        color: #ccc;
      }
      .content {
        color: #666;
        font-family: "微软雅黑";
        font-weight: 500;
        line-height: 70PX;
        font-size: 0.4rem;
        text-indent: 100PX;
    min-width: 9rem;

      }
    }
  }
}
// 移动端
    @media screen and (max-width: 750px) {
      .Apparea-intro-container{
        .contentBox {
          img{
            width:100%;
            height:5rem;
          }
          .news{
            // width: calc(100% - 5rem);
            width: 100%;
            .content{
            font-size: 18PX;
            line-height: 30PX;
            text-indent: 0px;
            }
          }
          
        }
      }
    }
</style>