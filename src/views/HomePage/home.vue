<template>
  <div class="Homepage-container DefaultContainerStyle">
    <!-- 轮播大图 -->
    <swiperImg :imglist="imgArr"></swiperImg>
    <!-- 产品列表展示 -->
    <div class="content">
      <div class="productBox">
        <el-row :gutter="30">
          <el-col
            v-for="(item, index) in productList"
            :xs="24"
            :sm="12"
            :md="6"
            :lg="6"
            :xl="6"
            :key="index + item"
          >
            <productDiscribe :productInfo="item" :isEven="(index + 1) % 2 == 0"></productDiscribe>
          </el-col>
        </el-row>
      </div>
    </div>

    <!-- 产品海报图 -->
    <div class="content" v-show="false">
      <div class="provideGoodPro">
        <img :src="require(`$assets/CommonImg/HomePage/provideGoodPro.jpg`)" alt />
      </div>
    </div>
    <!-- 公司主营产品 -->
    <!-- <div class="content">
      <div class="mainProductTitle" v-show="false">
        <p class="name">
          公司
          <span class="keyWord">主营</span>
          产品
        </p>
        <p
          class="details"
        >半导体和MEMS领域微细加工设备的研发、生产和销售。公司目前主要的产品是晶圆键合设备、晶圆喷胶设备、基础工艺设备和检测设备等半导体先进工艺设备，经过几年的研发和实验验证，目前这些产品均已为广大用户所接受。</p>
        <div class="line">
          <span></span>
          <span class="blue"></span>
          <span></span>
        </div>
      </div>
      <div class="mainProductBox">
        <el-row :gutter="30">
          <el-col
            v-for="(item, index) in mainProductList"
            :xs="12"
            :sm="12"
            :md="6"
            :lg="6"
            :xl="6"
            :key="index + item"
          >
            <div class="mainProduct" @click="gotoProduct">
              <img class="imgPic" :src="require(`$assets/CommonImg/HomePage/${item.iconUrl}`)" alt />
              <p class="name">{{item.title}}</p>
              <div class="introduce">
                <p class="introduce_name">{{item.title}}</p>
                <p class="details">{{item.subTitle}}</p>
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
    </div>-->
    <div class="content">
      <div class="prod-list">
        <el-row v-for="(rowList, i) in showList" :key="`prod-${i}`" :gutter="30">
          <el-col
            v-for="(item, index) in rowList"
            :xs="24"
            :sm="12"
            :md="12"
            :lg="6"
            :xl="6"
            :key="`${i}-${index}`"
          >
            <div class="prod-item">
              <div class="item-img">
                <img :src="item.src" alt="图片" />
              </div>
              <div class="item-title">{{ item.title }}</div>
              <div class="item-desc" @click="viewDetail(item)">
                <span class="title">{{ item.title }}</span>
                <span class="desc">{{ item.desc }}</span>
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
    </div>
    <!-- 数字动效 -->
    <div class="content">
      <div class="numberDanceBox" id="numberDance">
        <div class="numberDance" v-for="(item, index) in numberDanceList" :key="index + item">
          <img class="imgPic" :src="require(`$static/icon/${item.iconUrl}`)" alt />
          <p class="number" v-if="!numberDanceStart">0</p>
          <IcountUp
            class="number"
            v-if="numberDanceStart"
            :endVal="item.num"
            :options="options"
            @ready="onReady"
          ></IcountUp>

          <p class="name">{{item.name}}</p>
        </div>
      </div>
    </div>

    <!-- 联系我们 -->
    <div class="content">
      <div class="ContactUs-main">
        <div class="main-left" />
        <div class="submit-main" v-loading="loading">
          <div class="main-title">留言</div>
          <div
            class="main-desc"
          >欢迎来到苏州研材微纳科技有限公司官方网站。 关于产品的使用问题、改进建议，或举报不良信息，您都可以填写下方信息告诉我们，我们重视您的每一个想法</div>
          <input v-model="data.name" type="text" maxlength="10" placeholder="姓名*" />
          <input v-model="data.email" type="text" maxlength="20" placeholder="邮箱*" />
          <input v-model="data.phone" type="text" maxlength="11" placeholder="手机*" />
          <textarea v-model="data.remark" type="text" placeholder="需要 / 改进 / 建议" />
          <button @click="submitInfo">提交</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import config from "@/config/index";
import swiperImg from "@/components/public/swiperImg";
import productDiscribe from "@/components/public/productDiscribe";
import IcountUp from "vue-countup-v2";
import commonInfo from "@/assets/CommonJs/commonInfo";
import { mapState } from 'vuex'
export default {
  name: "Home",
  data() {
    return {
      loading: false,
      data: {
        name: "",
        phone: "",
        email: "",
        remark: ""
      },
      numberDanceStart: false,
      options: {
        useEasing: true,
        useGrouping: true,
        separator: ",",
        decimal: ".",
        prefix: "",
        suffix: ""
      },
      imgArr: commonInfo.swiperImgs,
      numberDanceList: [
        { name: "成立", iconUrl: `smile.png`, num: 2015 },
        { name: "合作客户", iconUrl: `rocket.png`, num: 1010 },
        { name: "员工", iconUrl: `worker.png`, num: 96 },
        { name: "获奖", iconUrl: `medal.png`, num: 25 }
      ],
      mainProductList: [
        {
          title: "晶圆喷胶机SC-50",
          subTitle: "产品介绍产品介绍产品介绍产品介绍产品介绍产品介绍",
          iconUrl: `home-main-pro-1.jpg`
        },
        {
          title: "键合机TWB-150A",
          subTitle: "产品介绍产品介绍产品介绍产品介绍产品介绍产品介绍",
          iconUrl: `home-main-pro-2.jpg`
        },
        {
          title: "桌面显影机",
          subTitle: "产品介绍产品介绍产品介绍产品介绍产品介绍产品介绍",
          iconUrl: `home-main-pro-3.jpg`
        },
        {
          title: "可编程热板PHP-8",
          subTitle: "产品介绍产品介绍产品介绍产品介绍产品介绍产品介绍",
          iconUrl: `home-main-pro-4.jpg`
        }
      ],
      productList: commonInfo.productList
    };
  },
  computed: {
    ...mapState({
      prodList: state => state.prod.prodList
    }),
    showList() {
      const copNum = Math.ceil(this.prodList.length / 4);
      const arr = [];
      for (let i = 0; i < copNum; i++) {
        const rowArr = [];
        for (let j = 0; j < 4; j++) {
          const index = i * 4 + j;
          if (this.prodList[index]) rowArr.push(this.prodList[index]);
        }
        arr.push(rowArr);
      }
      return arr;
    }
  },
  mounted() {
    // setTimeout(() => {
    //   this.numberDanceStart = true
    // }, 5000);
    window.addEventListener("scroll", this.handleScroll, true);
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll, true);
  },
  methods: {
    submitInfo() {
      const { name, phone, email, remark } = this.data
      const fields = ['name', 'phone', 'email', 'remark']
      const tips = ['姓名', '手机号', '邮箱', '需要 / 改进 / 建议']
      let res = true
      for (let i = 0; i < fields.length; i++) {
        if (!this.data[fields[i]]) {
          this.$message.closeAll()
          this.$message.error(`请填写${tips[i]}`)
          res = false
          break
        }
      }
      if (!res) return
      this.loading = true
      this.$store.dispatch('submitFeedBack', this.data).then(res => {
        this.$message.closeAll()
        if (res.data.Code === 1) {
          this.$message.success('提交成功')
          this.data = {
            name: '',
            phone: '',
            email: '',
            remark: ''
          }
        } else {
          this.$message.error('提交失败')
        }
      }).catch(err => {
        this.$message.error('服务异常,请稍候再试')
      }).finally(() => {
        this.loading = false
      })
    },
    viewDetail(info) {
      this.$router.push("/prod/introduction/" + info.id);
      setTimeout(() => {
        document.documentElement.scrollTop = 0;
      }, 100);
    },
    gotoProduct() {
      window.scrollTo(0, 0);
      this.$router.push({ path: "/prod/list" });
    },
    handleScroll() {
      var scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;

      var offsetTop = document.querySelector("#numberDance").offsetTop;
      // console.log(scrollTop, offsetTop)
      if (scrollTop > 880) {
        this.numberDanceStart = true;
      }
    },
    onReady: function(instance, CountUp) {
      // console.log("进来了");
      // const that = this;
      // instance.start(that.endVal + 100);
    }
  },
  components: { swiperImg, productDiscribe, IcountUp }
};
</script>

<style scoped lang="scss">
.Homepage-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .content {
    width: 100%;
    .productBox {
      width: 100%;
      padding: 0 130px;
      box-sizing: border-box;
      margin: 20PX 0 0 0;
    }
    .provideGoodPro {
      box-sizing: border-box;
      padding: 0 130px;
      margin: 0px 0 120px 0;
      img {
        width: 100%;
        height: 100%;
      }
    }
    .numberDanceBox {
      display: flex;
      flex-direction: row;
      justify-content: space-around;
      align-items: center;
      margin-bottom: 20PX;
      height: 6rem;
      background: url("~@/assets/CommonImg/HomePage/numberDance-bg.png") no-repeat;
      background-size: cover;
      .numberDance {
        text-align: center;
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        .imgPic {
          width: 40PX;
          height: 40PX;
        }
        .number {
          font-weight: 800;
          font-family: "Ping Fang SC";
          font-size: .6rem;
          margin: 10PX 0;
        }
        .name {
          font-family: "微软雅黑";
          font-size: .6rem;
          font-weight: 600;
        }
      }
    }
    .prod-list {
      width: 100%;
      padding: 0 130px;
      box-sizing: border-box;
      margin: 0px 0 0px 0;
      .prod-item {
        position: relative;
        margin-bottom: 30PX;
        .item-img {
          img {
            width: 100%;
          }
        }
        .item-title {
          cursor: default;
          position: absolute;
          color: #00c3ed;
          bottom: 0;
          height: 50PX;
          font-size: 20PX;
          line-height: 50PX;
          width: 100%;
          font-weight: 700;
          transition: all 900ms ease;
          background: rgba(0, 46, 90, 0.9);
        }
        .item-desc {
          position: absolute;
          width: 100%;
          opacity: 0;
          transition: all 900ms ease;
          display: flex;
          align-items: center;
          top: 0;
          left: 0;
          display: flex;
          flex-direction: column;
          justify-content: center;
          background: rgba(0, 46, 90, 0.9);
          height: 100%;
          box-sizing: border-box;
          user-select: none;
          padding: 20px;
          cursor: pointer;
          .title {
            margin-bottom: 10px;
            color: #00c3ed;
            font-size: 20PX;
            font-weight: 700;
          }
          .desc {
            font-size: 14PX;
            line-height: 0.3rem;
            color: white;
          }
        }
        &:hover {
          .item-desc {
            opacity: 1;
          }
        }
      }
    }
    .ContactUs-main {
      width: 100%;
      display: flex;
      padding: 0;
      box-sizing: border-box;
      margin-bottom: 20PX;
      .main-title {
        text-align: left;
        user-select: none;
        font-size: 0.5rem;
        font-weight: 600;
        cursor: default;
        color: white;
      }
      .main-left {
        width: 50%;
        background: url("~@/assets/CommonImg/ContactUs/bg88.jpg") no-repeat;
        background-size: cover;
      }
      .main-desc {
        user-select: none;
        cursor: default;
        color: white;
        padding: 10PX 0;
        text-align: left;
        line-height: 0.35rem;
        font-size: 0.25rem;
      }
      .submit-main {
        padding: 0.5rem 0.2rem !important;
        background: url("~@/assets/CommonImg/ContactUs/worldmap.png") no-repeat;
        background-size: cover;
        background-position: center;
        background-color: #002e5a !important;
        box-sizing: border-box;
        display: inline-flex;
        width: 50%;
        flex-direction: column;
        input,
        textarea {
          color: white;
          background-color: rgba(255, 255, 255, 0);
          box-sizing: border-box;
          width: 100%;
          padding: 10PX;
          line-height: 20px;
          font-size: 0.2rem;
          outline: none;
          border: none;
          transition: all 0.5s;
          border-bottom: 1px solid #ddd;
          margin-bottom: 20px;
          &:focus {
            border-bottom: 1px solid #00c3ed;
          }
        }
        textarea {
          height: 1.5rem;
          resize: none;
          &::-webkit-input-placeholder {
            color: #ccc;
          }
        }
        button {
          border: none;
          user-select: none;
          outline: none;
          border-radius: 1rem;
          width: 2rem;
          height: 0.6rem;
          background-color: #0099ba;
          color: white;
          font-size: 0.3rem;
          letter-spacing: 0.2rem;
          border: 3px solid #0099ba;
          transition: all 0.3s;
          margin-top: 30px;
          cursor: pointer;
          &:hover {
            background-color: transparent;
            color: #00c3ed;
          }
        }
      }
    }
  }
}
@keyframes topEaseInAnimate {
  /*定义从上边滑入文字的动画*/
  0% {
    transform: translateY(200px);
    opacity: 0;
  }
  100% {
    transform: translateY(0px);
    opacity: 1;
  }
}
</style>