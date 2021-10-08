<template>
  <!-- 引入container布局 -->
  <el-container class="home-container">
    <!-- 头部 -->
    <el-header>
      <div class="div1">
        <img src="../assets/th.png" class="img1" alt />
        <span class="span1">个人运动平台</span>
      </div>

      <el-button type="info" @click="logout" class="btn1">安全退出</el-button>
    </el-header>
    <!-- 主体 -->
    <el-container>
      <!-- 主体侧边栏 -->
      <el-aside :width="isCollapse?'64px':'200px'">
          <div class="toggle-button" @click="toggleCollapase">|||</div>
        <el-menu
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#409eff"
          unique-opened=""
          :collapse="isCollapse"
          :collapse-transition="false"
          :router="true"
          :default-active="activePath">
          <!-- 一级菜单 -->
          <el-submenu :index="item.id+''" v-for="item in menuList" :key="item.id">
            <template slot="title">
              <i :class="iconsObject[item.id]"></i>
              <span>{{item.title}}</span>
            </template>
            <!-- 二级菜单 -->
            <el-menu-item :index="item2.path+''" v-for="item2 in item.slist" :key="item2.id" @click="saveNavState(item2.path)">
              <template slot="title">
                 <i :class="iconsObject[item2.id]"></i>
              <span>{{item2.title}}</span>
            </template>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <!-- 主体内容 -->
      <el-main>
          <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
    data(){
        return{
            //菜单列表
            menuList:[],
            //导航伸缩
            isCollapse:false,
            //
            iconsObject:{
                '100':'iconfont icon-guanliyuan',
                '200':'iconfont icon-yundong',
                '101':'iconfont icon-denglu-copy',
                '102':'iconfont icon-mima',
                '103':'iconfont icon-yundong',
                '104':'iconfont icon-shangpin',
                '201':'iconfont icon-shu',
                '202':'iconfont icon-qialuli',
                '203':'iconfont icon-shiwu-',
                '204':'iconfont icon-denglu-copy',
            },
            activePath:'/welcome',//默认路径
        }
    },
    // onload事件
    created(){
        // 查询menuList
        this.getMenuList();
        this.activePath=window.sessionStorage.getItem('activePath');//取出session里的path,动态修改
    },
  methods: {
    //安全退出
    logout() {
      window.sessionStorage.clear(); //清除session
      this.$router.push("/login"); //回到主页
    },
    //获取导航菜单方法
    async getMenuList(){
        const {data:res}=await this.$http.get("menus");
        console.log(res);
        if(res.flag!=200) return this.$message.error("获取列表失败！！！")//访问失败的错误信息
        this.menuList=res.menus;//数据回填
    },
    //控制伸缩
    toggleCollapase(){
        this.isCollapse = !this.isCollapse;
    },
    //保存路径
    saveNavState(activePath){
      window.sessionStorage.setItem('activePath',activePath);//存放在session里
      this.activePath=activePath;
    }
  },
};
</script>

<style  scoped>
/* 布局器样式 */
.home-container {
  height: 100vh;
}
.el-header {
  background-color: #373d41;
  display: flex;
  /* 左右贴边 */
  justify-content: space-between; 
  padding-left: 0vh;
  align-items: center;
  color: #fff;
  font-size: 20px;
}
.div1 {
  display: flex;
  align-items: center;
}
.span1 {
  top: 5px;
  margin-left: 15px;
}
.btn1{
    background-color:#0ee;
    color:rgb(34, 29, 29);
    font-weight: bold;
}
.el-aside {
  background-color: #333744;
}
.el-menu{
    border-right: none;
    
}
.el-main {
  background-color: #eaedf1;
}
.img1 {
  width: 55px;
  height: 55px;
}
/* |||按钮样式 */
.toggle-button{
    background-color: #4A5064;
    font-size: 10px;
    line-height: 24px;
    color: #fff;
    text-align: center;
    letter-spacing: 0.2em;
    /* 显示小手 */
    cursor: pointer;
}
</style>
