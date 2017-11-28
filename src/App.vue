<template>
  <div id="app">
    <el-container>
      <el-header class="header" style="height: 128px">
        <div class="logo">
          <img src="./../static/img/icons/favicon_128X128.png"/>
          <div id="theLove"></div>
        </div>
      </el-header>
      <el-container>
        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
          <el-menu :default-openeds="['0']">
            <!--导航-->
            <el-submenu  v-for="(value, key) in navData" :index="key" :key="this">
              <!--导航标题-->
              <template slot="title"><i :class="menuClass(key)"></i>{{value.submenu}}</template>
              <!--分组1-->
              <el-menu-item-group v-if="value.submenu !== 'Reading'">
                <!--分组标题-->
                <template slot="title">{{value.submenu}}</template>
                <el-menu-item v-for="(value1, key1) in value.nav_item" :index="key+'-'+key1" :key="this">{{value1.name||value1}}</el-menu-item>
              </el-menu-item-group>
              <!--分组2-n-->
              <el-submenu v-else v-for="(value1, key1) in value.nav_item" :key="this">
                <template slot="title">{{value1.status | readStatus}}</template>
                <el-menu-item v-for="(value2, key2) in value1.items" :index="key+'-'+key1+'-'+key2" :key="this">{{value2.name}}</el-menu-item>
              </el-submenu>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  export default {
    name: 'app',
    components: {
//    AppHeader,
//    AppSidebar,
//    AppBottomNavigator
    },
    data () {
      const auther = {
        date: '2017-11-28',
        name: 'webwang',
        address: '广东省深圳市龙岗区长坑路东一巷'
      }
      return {
        navData: [
          {
            submenu: 'Front-end',
            nav_item: [
              { name: 'html5', router: '' },
              { name: 'css3', router: '' },
              { name: 'ES6', router: '' },
              { name: 'less', router: '' },
              { name: 'bootstrap4', router: '' },
              { name: 'jquery', router: '' },
              { name: 'WX-xcx', router: '' },
              { name: 'vue2x', router: '' },
              { name: 'react', router: '' },
              { name: 'angular2', router: '' },
              { name: 'node', router: '' },
              { name: 'webpack', router: '' },
              { name: 'more', router: '#' }
            ]
          }, {
            submenu: 'Reading',
            nav_item: [
              {
                status: 0,
                items:[
                  { name: '《ES6标准入门(阮一峰)》'},
                  { name: '《Vue.js实战(梁灏)》'},
                  { name: '《Git教程(廖雪峰)》'},
                  { name: '《精通jQuery(第2版)》'}
                ]
              },{
                status: 1,
                items:[
                  { name: '《JavaScript权威指南(第6版)》'},
                  { name: '《JavaScript&jQuery交互式Web前端开发(Jon Duckett)》'},
                  { name: '《HTML & CSS设计与构建网站(Jon Duckett)》'},
                  { name: '《HTML5权威指南》'},
                  { name: '《三体》'},
                  { name: '《诛仙》'},
                  { name: '《守住中国人的底线》'}
                ]
              },
              {
                status: 2,
                items:[
                  { name: 'more', router: '' }
                ]
              }
            ]
          }, {
            submenu: 'Future',
            nav_item: ['python', 'WebAR', 'A-Frame', 'VR', 'AI', { name: 'more', router: '#' }]
          }, {
            submenu: 'Games',
            nav_item: ['LOL', 'WOW', 'DNF', '冒险岛2', { name: 'more', router: '#' }]
          }, {
            submenu: 'Contact',
            nav_item: [
              { name: '微博关注我', router: '#' },
              { name: 'more', router: '#' }]
          }
        ],
        menuClass: function (v) {
          switch (v) {
            case 0:
              return 'el-icon-view'
              break
            case 1:
              return 'el-icon-tickets'
              break
            case 2:
              return 'el-icon-mobile-phone'
              break
            case 3:
              return 'el-icon-service'
              break
            default:
              return 'el-icon-message'
          }
        }
      }
    },
    computed: {
//    ...mapState('appShell', [
//      'appHeader',
//      'appBottomNavigator',
//      'pageTransitionName'
//    ])
    },
    methods: {
//    ...mapActions('appShell', [
//      'setPageSwitching'
//    ]),
//    ...mapActions('appShell/appSidebar', [
//      'showSidebar',
//      'hideSidebar'
//    ]),
//    ...mapActions('appShell/appBottomNavigator', [
//      'activateBottomNav'
//    ]),
      handleBeforeEnter (el) {
        this.setPageSwitching(true)
      },
      handleAfterEnter (el) {
        el.scrollTop = el.dataset.scrollTop
        this.setPageSwitching(false)
      },
      handleBeforeLeave (el) {
        el.dataset.scrollTop = el.scrollTop
      },
      handleClickHeaderBack () {
        this.$router.go(-1)
      },
      handleClickHeaderMenu () {
        this.showSidebar()
      },
      handleHideSidebar () {
        this.hideSidebar()
      },
      handleShowSidebar () {
        this.showSidebar()
      },
      handleClickBottomNav ({ name }) {
        this.activateBottomNav(name)
      }
    },
    filters:{
      readStatus: function (v) {
        switch (v) {
          case 0:
            return '正在阅读'
            break
          case 1:
            return '已读完'
            break
          default:
            return '未读'
        }
      }
    }
  }
</script>

<style>
  body {
    margin: 0;
   }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /*margin-top: 60px;*/
   }
</style>
