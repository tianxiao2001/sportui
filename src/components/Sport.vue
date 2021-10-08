<template>

  <el-carousel :interval="4000" type="card" height="400px">
      <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-carousel-item  v-for="item in imagebox" :key="item">
      <img :src="item.idView" class="image" />
    </el-carousel-item>
  </el-carousel>
  

  
</template>
<script>
export default {
    name:'sport',
  data() {
    return {
      imagebox: [
        { id: 0, idView: require("../assets/sport/jianshen.png") },
        { id: 1, idView: require("../assets/sport/basketball.png") },
        { id: 2, idView: require("../assets/sport/football.png") },
        { id: 3, idView: require("../assets/sport/pingpang.png") },
        { id: 4, idView: require("../assets/sport/running.png") },
        { id: 5, idView: require("../assets/sport/yumaoqiu.png") },
      ],
      // 浏览器宽度
        screenWidth :0
    };
  },
  methods:{
              setSize:function () {
                // 通过浏览器宽度(图片宽度)计算高度
                this.bannerHeight = 400 / 1920 * this.screenWidth;
              },
            },
          mounted() {
              // 首次加载时,需要调用一次
              this.screenWidth =  window.innerWidth;
              this.setSize();
              // 窗口大小发生改变时,调用一次
              window.onresize = () =>{
              this.screenWidth =  window.innerWidth;
              this.setSize();
            }
          }
};
</script>
<style scoped>
.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 200px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
  margin-top: 20px;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
  margin-top: 20px;
}

img{
     /*设置图片宽度和浏览器宽度一致*/
      width:100%;
      height:inherit;
    }
    /* 面包屑样式 */
.el-breadcrumb {
  margin-bottom: 15px;
  font-size: 17px;
}
</style>