<template>
  <el-container style="min-height:2000px"
                direction="vertical">

    <div class="background">
      <img :src="home_bg" width="100%" height="100%"/>
    </div>
    
    <el-header :class="navBarFixed == true ? 'headColor1' : 'headColor2'">
      <div>
        <el-link :underline="false" href="http://localhost:8080/" target="_blank" class="demo-txt">Jerry's BLOG</el-link>
      </div>
      <el-menu
        :background-color="navBarFixed == true ? 'rgba(18,18,18)' : 'rgba(0,0,0,0)'"
        mode="horizontal"
        text-color="rgb(230, 223, 223)"
        active-text-color="#ffd04b"
        style="border-bottom: none;float: right;">
        <el-menu-item index="1">搜索</el-menu-item>
        <el-menu-item index="2">首页</el-menu-item>

        <el-submenu index="3">
          <template slot="title">网站</template>
          <el-menu-item index="2-1">打赏</el-menu-item>
          <el-menu-item index="2-2">友链</el-menu-item>
          <el-menu-item index="2-3">朋友圈</el-menu-item>
          <el-menu-item index="2-3">留言板</el-menu-item>
        </el-submenu>

        <el-submenu index="4">
            <template slot="title">归档</template>
            <el-menu-item index="2-4-1">标签</el-menu-item>
            <el-menu-item index="2-4-2">分类</el-menu-item>
            <el-menu-item index="2-4-3">时间轴</el-menu-item>
            <el-menu-item index="2-4-3">文章</el-menu-item>
        </el-submenu>

        <el-submenu index="5">
            <template slot="title">关于</template>
            <el-menu-item index="2-5-1">我</el-menu-item>
            <el-menu-item index="2-5-2">网易云</el-menu-item>
            <el-menu-item index="2-5-3">博客日志</el-menu-item>
        </el-submenu>
      </el-menu>
    </el-header>

    <el-main overflow: auto>
      <template>
        <div class="demo-type">
          <el-avatar src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png" :size="150"></el-avatar>
        </div>
      </template>
      <template>
        <el-row>
          <el-button type="primary" icon="el-icon-edit" circle></el-button>
          <el-button type="success" icon="el-icon-check" circle></el-button>
          <el-button type="info" icon="el-icon-message" circle></el-button>
          <el-button type="warning" icon="el-icon-star-off" circle></el-button>
        </el-row>
      </template>

      <template>
        <el-row :gutter="20">
          <el-col :span="18" style="border-top:100px;">
            <el-card shadow="hover">
              <div class="text item">
                <i class="el-icon-magic-stick"></i>
              </div>
            </el-card>
            <el-card shadow="hover" style="height:230px">
            </el-card>
            <el-card shadow="hover" style="height:200px">
            </el-card>
            <el-card shadow="hover" style="height:280px" v-for="item in pageData" :key="item.id">
              <el-table>

              </el-table>
            </el-card>
            <div class="block">
              <el-pagination
                @current-change="handleCurrentChange"
                :current-page="currentPage"
                :page-size="pagesize"
                layout="pager,next"
                :total="articleData.length"
                background>
              </el-pagination>
            </div>
          </el-col>

          <el-col :span="6">
            <el-card shadow="hover" style="height:440px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:440px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:440px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:440px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:440px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:180px;width:270px">
            </el-card>

            <el-card shadow="hover" style="height:230px;width:270px">
            </el-card>
          </el-col>
        </el-row>
      </template>

    </el-main>
  </el-container>
</template>

<script>
    export default {
        name: "HelloWeb",
        data(){
          return{
            home_bg: require('@/assets/darkmodepicture6.jpg'),
            //滑动时样式改变
            navBarFixed: false,
            //滑动时透明度
            // opacityStyle:{opacity: 0},
            articleData: [1,2,3,4,5,6,7,8,9,10],
            pageData:[1,2,3,4,5,6,7],
            pagesize: 6,
            currentPage: 1,

            y: 0,
          }
        },
        mounted(){
          window.addEventListener('scroll', this.watchScroll)
        },
        methods:{
          handleCurrentChange(val){
            this.currentPage = val;
          },
          watchScroll(){
            let scrollNow = window.pageYOffset
            let scrollTop = scrollNow - this.y
            this.y = scrollNow
            if(scrollTop < 0)
            {
              this.navBarFixed = true;
              // const opacity = (scrollTop + 50) / 61.25;
              // this.opacityStyle = {opacity};
              // console.log("ss" + scrollTop);
            }
            else
            {
              this.navBarFixed = false;
            }
          }
        }
    }
</script>

<style scoped>

  /* .el-menu--horizontal > .el-menu-item {
    float: right;
    height: 60px;
    line-height: 60px;
    margin: 0;
    border-bottom: 2px solid transparent; 
    color: beige;
  } */
  .text {
    font-size: 14px;
  }

  .item {
    padding: 18px 0;
    line-height: 20px;
  }
  .el-card{
    background-color: rgba(17, 22, 34, 1);
    border-radius: 8px;
    border-bottom: 0;
    margin-bottom: 20px;
  }
  .background{
    width: 100%;
    height: 100%;
    z-index: -1;
    position: fixed;
  }
  /* .el-menu-demo{
    position: fixed;
    top: 0;
    z-index: 999;
  } */
  .headColor1{
    padding: 0%;
    position: fixed;
    width: 100%;
    top: 0;
    background-color: rgba(18,18,18);
  }
  .headColor2{
    padding: 0%;
    position: relative;
    top: 0;
    background-color: rgba(0,0,0,0);
  }
  .el-main {
    color: #333;
    text-align: center;
    line-height: 160px;
    padding-left: 20%;
    padding-right: 20%;
  }

  .demo-type{
    margin-top: 200px;
    height: 150px;
  }
  .demo-txt{
    float: left;
    margin-left: 35px;
    margin-top: 16px;
    font-size: 16px !important;
    color: rgb(230, 223, 223) !important;
    font-weight: 700;
  }

  /deep/ .el-submenu__title:hover{
    background-color: #00c4b6 !important; 

  }
  .el-menu-item:hover {
    background-color: #00c4b6 !important;
  }

</style>
<style>
  body{
    /* 设置内部填充为0，几个布局元素之间没有间距
    padding: 0px; */
    /*外部间距也是如此设置*/
    margin: 0px;
    cursor: url(https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/image/cursor.ico),default;
  }
</style>

