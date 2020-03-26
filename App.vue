<template>
  <div id="app">
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About2</router-link> |
      <router-link to="/login" v-if='!isLogin'>Login</router-link>
      <a href="" v-if='isLogin'>Logout</a> -->
      <transition name='route-move'>
        <router-view class='child-view' />
      </transition>
      <cube-tab-bar show-slider 
        v-model="selectLabel" 
        @change="changeHandler">
        <cube-tab v-for="(item, index) in tabs" :key="index" 
          :icon="item.icon" :label="item.value">
          <span>{{item.label}}</span>
          <!-- <span class="badge" v-if="showBadge(item.label)">{{cartTotal}}</span> -->
        </cube-tab>
      </cube-tab-bar>

  </div>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
  data() {
    return {
      selectLabel: '/', // tab选中的默认值
      tabs: [
        {label : 'Home',value:'/',icon:'cubeic-home'},
        {label : 'Cart',value:'/cart',icon:'cubeic-mall'},
        {label : 'Me',value:'/login',icon:'cubeic-person'}
      ]

    }
  },
  created() {
    // 初始化页签设置
    this.selectLabel = this.$route.path
  },
  watch:{
    // 路由发生变化时，同步tabs选中 用watch来监听路由变化
    $route() {
      this.selectLabel = this.$route.path
    }
  },
  methods:{
    changeHandler(val) {
      this.$router.push(val)
    }
  },
  computed: {
  	
    ...mapGetters(['isLogin'])
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.cube-tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #edf0f4;
}
.cube-tab-bar-slider {
  top: 0;
}
.route-move-enter {
  transform: translate3d(-100%,0,0)
}
.route-move-leave-to {
  transform: translate3d(100%,0,0)
}
.route-move-enter-active,
.route-move-leave-active{
  transition: 0.3s
}
.child-view {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  padding-bottom: 36px;
}
</style>
