<style scoped>
   footer {
       width:100%;
       position:fixed;
       
       bottom:0;
   }

   button {
       width: 33.33%;
       height:50px;
   }

   button{
        background:#F6F6F8;
        color:#5ac18e;
        border:none;
        position:relative;
        height:50px;
        font-size:1.4em;
        padding:0 1em;
        cursor:pointer;
        transition:800ms ease all;
        outline:none;
    }

    button:hover{
        background:#5ac18e;
        color:#F6F6F8;
    }

    .active {
        background:#5ac18e;
        color:#F6F6F8;
    }
    
</style>

<template>
    <footer>
        <button v-for="tab in tabs" :key="tab"
                v-bind:class="{active: currentTab === tab}"
                v-on:click="changeTab(tab)"
        >
            <span v-if="tab==='PAGE1'"
            class="el-icon-user"></span>
            <span v-if="tab==='PAGE2'"
            class="el-icon-edit"></span>
            <span v-if="tab==='PAGE3'"
            class="el-icon-chat-line-square"></span>    
        </button>
    </footer>
</template>

<script>
export default {
    props:['tabs', 'currentTab'],
    methods:{
        changeTab(newTab){
            this.$emit('changeTab', newTab);
        }
    }
}
</script>