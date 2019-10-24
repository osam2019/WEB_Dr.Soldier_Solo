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
import Communication from './PAGE3/Communication.vue';

export default {
    components:{
        'Communication' : Communication,
    },
    methods:{
        changeSmallTab(tab){
            this.currentSmallTab = tab;
        }
    },
    data(){
        return {
            smalltabs : ["Communication"],
            currentSmallTab : "Communication"
        }
    }
}
</script>
