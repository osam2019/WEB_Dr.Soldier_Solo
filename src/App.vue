<template>
    <div id="app">
      <MainHeader></MainHeader>
      <LoginForm v-if=!isLogined
      v-on:Login="Login"
      ></LoginForm>

      <transition 
      v-on:before-enter="beforeEnter"
      v-on:enter="enter"

      v-on:before-leave="beforeLeave"
      v-on:leave="leave"
      >
        <component
        v-if=isLogined
        v-bind:is="currentTab"
        style="height:100%;">
        </component>
      </transition>

      <MainFooter 
      v-if=isLogined
      v-bind:tabs="tabs"
      v-bind:currentTab="currentTab"
      v-on:changeTab="changeTab"
      ></MainFooter>
    </div>    
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import LoginForm from './components/LoginForm.vue'
import MainFooter from './components/MainFooter.vue'
import PAGE1 from './components/PAGE1.vue'
import PAGE2 from './components/PAGE2.vue'
import PAGE3 from './components/PAGE3.vue'

export default {
    data(){
      return {
        tabs : ["PAGE1", "PAGE2", "PAGE3"],
        currentTab : "PAGE1",
        beforeTab : "PAGE1",
        isLogined : true,
        test : true
      }
    },
    computed:{
      newSlideLeft: function(){
        if (this.tabs.indexOf(this.currentTab) <= this.tabs.indexOf(this.beforeTab))
          return true;
        else
          return false;
      }
    },
    components:{
      'MainHeader' : MainHeader,
      'MainFooter' : MainFooter,
      'LoginForm' : LoginForm,
      'PAGE1' : PAGE1,
      'PAGE2' : PAGE2,
      'PAGE3' : PAGE3,
    },
    methods:{
      changeTab(newTab){
        this.currentTab = newTab;
      },
      Login(){
        this.isLogined=true;
      },
      beforeEnter: function (el) {
        let move;
        if(this.newSlideLeft){
          move = '-400px';
        }else
          move = '400px';
        el.style.position = 'absolute';
        el.style.width = '100%';
        Velocity(el, { translateX:move}, { duration: 0})
      },
      enter: function (el, done) {
        Velocity(el, { translateX:'0px'}, { duration: 300, complete:done});
        this.beforeTab = this.currentTab;
        el.style.position = 'static';
      },
      

      beforeLeave: function (el) {
        el.style.position = 'absolute';
        el.style.width = '100%';
      },
      leave: function (el, done) {
        let move;
        if(this.newSlideLeft){
          move = '400px';
        }else
          move = '-400px';
        Velocity(el, { translateX: move}, { duration: 300, complete:done})        
      }
    },

    created(){

    }
}
</script>



<style>
  html {
    height:100%;
    margin:0;
  }
  body {
    height:100%;
    text-align: center;
    background-color: #F6F6F8;
    margin : 0;
  }
  #app{
    height: 100%;
    margin:0;
  }
  .shadow{
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
  ul {
    list-style-type: none;
    padding:20px;
  }

  * {
    font-family: 'Noto Sans KR', sans-serif;
  }
  
</style>

