<style scoped>
    h1 {
        margin:0px;
        margin-top : 20px;
        color : #42b983;
    }
    img {
        width:100px;
        height:100px;
        margin:20px;
    }
</style>

<template>
<div>
    <h1>로그인</h1>
    <div class="imageWrapper">
        <img src="../assets/icon_fb.png"
        v-on:click="Login"/>
        <img src="../assets/icon_g.jpg"
        v-on:click="Login"/>
    </div>
    <div class="imageWrapper">
        <img src="../assets/icon_n.png"
        v-on:click="Login"/>
        <img src="../assets/icon_k.svg"
        v-on:click="Login"/>
    </div>
</div>
</template>

<script>
export default {
    methods:{
        Login(){
            this.$emit('Login');
        }
    }
}
</script>
