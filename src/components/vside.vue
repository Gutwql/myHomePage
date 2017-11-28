<template>
  <el-aside class="el-aside">
    <el-radio-group v-model="isCollapse" style="margin-bottom: 20px;">
      <el-radio-button :label="false">展开</el-radio-button>
      <el-radio-button :label="true">收起</el-radio-button>
    </el-radio-group>
    <el-menu @open="handleOpen" @close="handleClose" class="el-menu-vertical" :collapse="isCollapse" :unique-opened="true">
      <!--导航-->
      <el-submenu class="el-submenu"  v-for="(value, key) in navData" :index="key.toString()" :key="this">
        <!--导航标题-->
        <template slot="title"><i :class="menuClass(key)"></i><span slot="title">{{value.submenu}}</span></template>
        <!--分组1-->
        <el-menu-item-group v-if="value.submenu !== 'Reading'">
          <!--分组标题-->
          <span slot="title">{{value.submenu}}</span>
          <el-menu-item v-for="(value1, key1) in value.nav_item" :index="key+'-'+key1" :key="this" :title.sync="value1.name||value1">{{value1.name||value1}}</el-menu-item>
        </el-menu-item-group>
        <!--分组2-n-->
        <el-submenu v-else v-for="(value1, key1) in value.nav_item" :index="key+'-'+key1" :key="this">
          <span slot="title">{{value1.status | readStatus}}</span>
          <el-menu-item v-for="(value2, key2) in value1.items" :index="key+'-'+key1+'-'+key2" :key="this" :title.sync="value2.name">{{value2.name}}</el-menu-item>
        </el-submenu>
      </el-submenu>
    </el-menu>
  </el-aside>
</template>

<script>
/* eslint-disable */
export default {
  data () {
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
              items: [
                {name: '《ES6标准入门(阮一峰)》'},
                {name: '《Vue.js实战(梁灏)》'},
                {name: '《Git教程(廖雪峰)》'},
                {name: '《精通jQuery(第2版)》'}
              ]
            }, {
              status: 1,
              items: [
                {name: '《JavaScript权威指南(第6版)》'},
                {name: '《JavaScript&jQuery交互式Web前端开发(Jon Duckett)》'},
                {name: '《HTML & CSS设计与构建网站(Jon Duckett)》'},
                {name: '《HTML5权威指南》'},
                {name: '《三体》'},
                {name: '《诛仙》'},
                {name: '《守住中国人的底线》'}
              ]
            }, {
              status: 2,
              items: [{ name: 'more', router: '' }]
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
            { name: '关注我', router: '#' },
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
      },
      isCollapse: false
    }
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath)
    }
  },
  filters: {
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .el-aside{
    overflow: inherit;
  }
  .el-menu-vertical:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
  }
</style>
