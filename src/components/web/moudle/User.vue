<template>
  <div class="slide" :class="{'slidefix': isscroll,'maskshow': hide,'hidemenu':!hide}">
    <div class="slide_animate" :class="{'showmenu': hide,'hidemenu':!hide}">
      <div class="user" id="user">
        <div class="user_head">
          <img src="http://jiaopianjun.cc/assets/blogImg/hd.gif"/>
        </div>
        <h3 class="name">故事胶片</h3>
        <h3 class="user_autograph">以照片的方式定格故事的乐趣</h3>
        <div id="sns-links" class="sns-links">
          <a href="" target="_blank">
            <i class="iconfont icon-weibo"></i>
          </a>
          <a href="" target="_blank">
            <i class="iconfont icon-juejin"></i>
          </a>
          <a href="" target="_blank">
            <i class="iconfont icon-jianshu"></i>
          </a>
          <a href="//github.com/jiaopianjun" target="_blank">
            <i class="iconfont icon-github"></i>
          </a>
        </div>
      </div>
      <nav class="menu" id="navmenu">
        <ul>
           <li class="cur" :class="{'current' : isContTab === 0 }">
              <router-link :to="{name:'home', params: {}}" @click.native="clickTab(0)">
                <icon name="home" :w="24" :h="24" class="icon"></icon>
                <icon name="home_h" :w="24" :h="24" class="icon_h"></icon>
                <icon name="home_w" :w="24" :h="24" class="icon_w"></icon>
                Home
              </router-link>
           </li>
           <li class="cur" :class="{'current' : isContTab === 1 }" @click="clickTab(1)">
              <router-link :to="{name:'Entrance', params: {}}" @click.native="clickTab(1)">
                <icon name="label" :w="22" :h="22" class="icon"></icon>
                <icon name="label_h" :w="22" :h="22" class="icon_h"></icon>
                <icon name="label_w" :w="22" :h="22" class="icon_w"></icon>
                Entrance
              </router-link>
           </li>
           <li class="cur" :class="{'current' : isContTab === 2 }">
              <router-link :to="{name:'about', params: {}}" @click.native="clickTab(2)">
                <icon name="about" :w="23" :h="23" class="icon"></icon>
                <icon name="about_h" :w="23" :h="23" class="icon_h"></icon>
                <icon name="about_w" :w="23" :h="23" class="icon_w"></icon>
                About
              </router-link>
           </li>
        </ul>
        <div id="sns-links" class="sns-links">
          <a href="" target="_blank">
            <i class="iconfont icon-weibo"></i>
          </a>
          <a href="" target="_blank">
            <i class="iconfont icon-juejin"></i>
          </a>
          <a href="" target="_blank">
            <i class="iconfont icon-jianshu"></i>
          </a>
          <a href="//github.com/jiaopianjun" target="_blank">
            <i class="iconfont icon-github"></i>
          </a>
        </div>
      </nav>
    </div>
    <div class="mask" @click="hidemenu" ></div>
  </div>
</template>

<script>
export default {
  name: 'slide',
    data () {
    return {
      scrolled: false,
      scrolled: false,
      isscroll: false,
      ispt: 'pc',
      hide: false,
      isContTab: this.$store.state.menu.tab
    }
  },
  watch:{
    "$store.state.menu.status":function(){
      this.hide = this.$store.state.menu.status
      // $(".slide_animate").css('left','0')
    },
    "$store.state.menu.tab":function(){
      this.isContTab = this.$store.state.menu.tab
    },
  },
  ready () {
    window.addEventListener('scroll', this.handleScroll)
  },
  methods:{
    clickTab:function(s,name){
      this.isContTab = s
      this.$store.commit('menustate',{status:true,tab:s})
      if(this.ispt === 'mobile'){
        this.hidemenu()
      }
    },
    handleScroll () {
      this.scrolled = window.scrollY
      this.ispt = $(".app").attr('data-mobile')
      if (this.ispt === 'pc') {
        if (this.scrolled > 470) {
          this.isscroll = true
        } else {
          this.isscroll = false
        }
      } else {
        // if (this.scrolled > 275) {
        //   this.isscroll = true
        // } else {
        //   this.isscroll = false
        // }
      }
    },
    hidemenu:function(){
      var _this = this
      _this.hide = false
      _this.$store.commit('menustate',{status:false,tab:_this.$store.state.menu.tab})
    }
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  mounted () {
    this.ispt = $(".app").attr('data-mobile')
  },
  created: function () {
    window.addEventListener('scroll', this.handleScroll)
    var str = this.$route.path,
        _this = this;
    if(this.$route.path === '/Entrance' || str.indexOf('tags') != -1 || str.indexOf('label') != -1){
      this.isContTab = 1
      _this.$store.commit('menustate',{status:false,tab:1})
    }else if(this.$route.path === '/about'){
      this.isContTab = 2
      _this.$store.commit('menustate',{status:false,tab:2})
    }else{
      this.isContTab = 0
      _this.$store.commit('menustate',{status:false,tab:0})
    }
  }
}
</script>

<style scoped>
  @import './../../../sass/stylesheets/user.css'
</style>
