<template>
  <div id="app">
    <NavBar></NavBar>
	<vue-canvas-nest :config="{color:'0,117,169', count: 200, opacity: 0.7, pointColor: '0,0,0', zIndex: -2}" :el="'.content-app'"></vue-canvas-nest>
    <div class="content-app theme1">
      <transition name="fadeInUp" mode="out-in">
        <router-view></router-view>
      </transition>
      <div class="footer">
        <!-- <p v-html="website.website_footer"></p> -->
        <p> Copyright © 2021 <a href="https://hoctructuyen123.net" target="_blank">HocTrucTuyen123.NET</a> &nbsp;-&nbsp; Powered by <a target="_blank" rel="nofollow noopener noreferrer" href="https://github.com/luyencode/OnlineJudgeDeploy">OnlineJudge</a></p>
      </div>
    </div>
	<BackTop></BackTop>
  </div>
</template>

<script>
  import { mapActions, mapState } from 'vuex'
  import NavBar from '@oj/components/NavBar.vue'
  import vueCanvasNest from 'vue-canvas-nest'

  export default {
    name: 'app',
    components: {
      NavBar, vueCanvasNest
    },
    data () {
      return {
        version: process.env.VERSION
      }
    },
    created () {
      try {
        document.body.removeChild(document.getElementById('app-loader'))
      } catch (e) {
      }
    },
    mounted () {
      this.getWebsiteConfig()
    },
    methods: {
      ...mapActions(['getWebsiteConfig', 'changeDomTitle'])
    },
    computed: {
      ...mapState(['website'])
    },
    watch: {
      'website' () {
        this.changeDomTitle()
      },
      '$route' () {
        this.changeDomTitle()
      }
    }
  }
</script>

<style lang="less">

  * {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }

  a {
    text-decoration: none;
    background-color: transparent;
    &:active, &:hover {
      outline-width: 0;
    }
  }


  @media screen and (max-width: 1200px) {
  .content-app {
    margin-top: 160px;
    padding: 0 2%;
  }
}

@media screen and (min-width: 1200px) {
  .content-app {
    margin-top: 80px;
    padding: 0 2%;
  }
}

  .footer {
    margin-top: 20px;
    margin-bottom: 10px;
    text-align: center;
    font-size: small;
  }

  .fadeInUp-enter-active {
    animation: fadeInUp .8s;
  }
  
  .CodeMirror-gutters {
    z-index: 1;
  }

  .theme(@ivu-btn-info: #2db7f5, @color: #2d8cf0, @word2: #57a3f3, @color2: rgba(255, 255, 255, 0.7)) {
    .ivu-menu-light.ivu-menu-horizontal .ivu-menu-item-active, .ivu-menu-light.ivu-menu-horizontal .ivu-menu-item:hover, .ivu-menu-light.ivu-menu-horizontal .ivu-menu-submenu-active{
      color: @color;
      border-bottom: 2px solid @color;
    }
	  .ivu-menu-horizontal .ivu-menu-submenu .ivu-select-dropdown .ivu-menu-item-selected, .ivu-menu-horizontal .ivu-menu-submenu .ivu-select-dropdown .ivu-menu-item-selected:hover {
      color: #fff;
    }
	  .ivu-menu-horizontal .ivu-menu-submenu .ivu-select-dropdown .ivu-menu-item-selected, .ivu-menu-horizontal .ivu-menu-submenu .ivu-select-dropdown .ivu-menu-item-selected:hover {
      background: @color;
    }
    .ivu-btn-info {
      background-color: @ivu-btn-info;
      border-color: @ivu-btn-info;
    }
    .ivu-page-item-active {
      background-color: @color;
		  border-color: @color;
    }

    li.ivu-page-item.ivu-page-item-active > a {
      color: #fff;
    }

  	.ivu-page-item:hover {
      border-color: @color;
    }
	  .announcements-container li .flex-container .title a.entry[data-v-5fab8d1a]:hover {
      color: @color;
      border-bottom: 1px solid @color;
    }
	  .ivu-btn-info:hover {
      background-color: @word2;
      border-color: @word2;
    }
	  .ivu-card {
      background: @color2;
    }
    .ivu-layout {
      background: transparent;
    }
	  .ivu-menu-light.ivu-menu-horizontal .ivu-menu-submenu:hover{
	    color: @color;
		  border-bottom: 2px solid @color;
	  }
  }

  .theme1{  //胖次蓝
    .theme();
  }

  .theme2{  //少女粉
    .theme(#f58f98, #f58f98, #d93a49, rgba(245, 143, 152, 0.35));
  }

  .theme3{  //基佬紫
    .theme(#3F51B5, #673AB7, #673AB7, rgba(103, 58, 183, 0.25));
  }

  .theme4{  //姨妈红
    .theme(#EF4136, #d63031, #ed1941cc, rgba(255, 118, 117, 0.3))
  }

  .theme5{  //原谅绿
    .theme(#00b894, #00b894, #55efc4, rgba(129, 236, 236, 0.35))
  }

</style>
