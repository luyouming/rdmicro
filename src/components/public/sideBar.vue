<template>
  <div class="side-bar">
    <div class="tel">
      <div class="Box">
        <span class="el-icon-phone-outline icon"></span>
        <span class="number">18112606475</span>
      </div>
    </div>
    <div class="qq">
      <div class="Box">
        <img :src="require(`$assets/CommonImg/sideBar/qq.png`)" class="qqImg" alt />
        <span class="number">2178862890</span>
      </div>
    </div>
     <div class="friend">
      <div class="topBox">
        <img :src="require(`$assets/CommonImg/AboutUs/friendLink.png`)" @click="gotoFriendNet" class="friendImg" alt />
        <!-- <span class="number">13584888970</span> -->
      </div>
    </div>
    <div class="goToTop">
      <div class="topBox" @click="gotoTop">
      <span class="el-icon-arrow-up icon"></span>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  // props: {

  // },
  name: "sideBar",
  data() {
    return {
      msg: "hello, sideBar"
    };
  },
  methods: {
    gotoTop() {
        window.scrollTo(0, 0)
      },
      gotoFriendNet() {
      window.open('http://www.memstools.cn') 
    }
  }
};
</script>

<style lang="scss" scoped>
.side-bar {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 40PX;
  position: fixed;
  z-index: 999;
  top: calc(50% - 160PX);
  right: 5PX;
  div {
    width: 100%;
    height: 40PX;
    border-bottom: 1px solid white;
    background: #6db0f9;
    cursor: default;
    position: relative;
    .icon {
      font-size: 24PX;
      color: #fff;
      font-weight: bold;
    }
    .qqImg {
      width: 30PX;
      height: 30PX;
    }
    .friendImg{
      height: 30PX;
      width: 30PX;
      background: #fff;
    }
    .Box, .topBox {
      position: absolute;
      top: 0;
      right: 0;
      // width: 260px;
      height: 40PX;
      // border: 1px solid red;
      display: flex;
      justify-content: center;
      align-items: center;
      .number {
        color: white;
        font-size: 22PX;
        line-height: 1px;
        margin-left: 10px;
        display: none;
      }
    }
    .topBox:hover{
     cursor: pointer;
    }
    .Box{
      transition: all .3s;
    }
    .Box:hover{
      width: 230PX;
    }
    .Box:hover .number{
      display: block;
    }
  }
}
</style>