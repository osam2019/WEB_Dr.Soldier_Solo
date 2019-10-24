<style scoped>
    
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
import Body from './PAGE2/Body.vue';
import Fitness from './PAGE2/Fitness.vue';
import Goal from './PAGE2/Goal.vue';

export default {
    components:{
        'Body' : Body,
        'Fitness' : Fitness,
        'Goal' : Goal
    },
    methods:{
        changeSmallTab(tab){
            this.currentSmallTab = tab;
        }
    },
    data(){
        return {
            smalltabs : ["Body", "Fitness", "Goal"],
            currentSmallTab : "Body"
        }
    }
}
</script>
