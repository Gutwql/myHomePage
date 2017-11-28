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
        <vSide></vSide>
        <el-main></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  import vSide from './components/vside'

  export default {
    name: 'app',
    components: {
//    AppHeader,
//    AppSidebar,
//    AppBottomNavigator,
      vSide
    },
    data () {
//      const auther = {
//        date: '2017-11-28',
//        name: 'webwang',
//        address: '广东省深圳市龙岗区长坑路东一巷'
//      }
      return {

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
