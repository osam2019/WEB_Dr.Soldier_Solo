<style>
    .el-tabs__active-bar{
        background-color: #22a39f;
    }
    .el-tabs__item.is-active{
        color:#22a39f;
    }
</style>

<template>
<div>
    <el-tabs v-model="currentSmallTab" 
        style="display:flex; justify-content:center"
    >
        <el-tab-pane v-for="(tab, index) in smalltabs" :key=index
        :label="tab" :name="tab"
        ></el-tab-pane>
    </el-tabs>
    <component
        v-bind:is="currentSmallTab">
    </component>
</div>
</template>

<script>
import Info from './PAGE1/Info.vue';
import Finance from './PAGE1/Finance.vue';
import Calendar from './PAGE1/Calendar.vue';

export default {
    components:{
        'Info' : Info,
        'Finance' : Finance,
        'Calendar' : Calendar
    },
    methods:{
        changeSmallTab(tab){
            this.currentSmallTab = tab;
        },
        handleClick(tab, event) {
            console.log(tab, '1!@#!', event);
        },
        print(){
            console.log('hi');
        }
    },
    data(){
        return {
            smalltabs : ["Finance", "Info", "Calendar"],
            currentSmallTab : "Info",
            activeName: 'first'
        }
    }
}
</script>
