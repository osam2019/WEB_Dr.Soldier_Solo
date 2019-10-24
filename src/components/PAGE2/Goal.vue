<style scoped>
    ul {
        padding:0;
    }
    li {
        list-style: none;
        text-align: left;
        width:80%;
        padding:5%;
        margin-left:5%;
        margin-bottom:5px;
        background:white;
        font-size : 1em;
    }

    .active {
        background:#5ac18e;
        color:white; 
    }

   .ul-enter, .ul-leave-to
    {
        opacity: 0;
        transform: translateY(30px);
    }

    .ul-leave-active {
        position: absolute;

    }

    .list-complete-item {
        transition: all 1s;
        display: block;
    }

    .el-input {
        width:70%;
    }

    .el-icon-circle-plus {
        font-size: 2.5em;
        color : #5ac18e;
    }

    .el-icon-circle-check{
        font-size:2em;
        border-radius: 50%;
        color:#22A39F;
    }

    .el-icon-circle-close{
        font-size:2em;
        border-radius: 50%;
        max-width: 32px;
        color:white;
        float:right;
        background-color: #ff7373;
    }

    .flex-row-wrapper{
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .activeBtn{
        color:white;
    }
    li p {
        margin : 5px;
    }
</style>

<template>
<div>
    <div class="flex-row-wrapper">
        <el-input
        placeholder="목표를 입력해주세요."
        suffix-icon="el-icon-edit"
        v-model="input"
        @click="ClearInput"
        >
        </el-input>

        <span class='el-icon-circle-plus'
        style="margin-left:0.1em"
            @click ="addList(input,false,false)"
        ></span>
    </div>

    <transition-group name="ul" tag="ul">
        <li class="list-complete-item" 
        v-for="(li, index) in list" :key=li
        v-bind:class="{active : listClass[index]}"
        >
            <div style="display:flex; align-items:center">
                <span class='el-icon-circle-check'
                style="flex:1"
                @click ="Toggle(index)"
                :class="{activeBtn:listClass[index]}"
                ></span>
                <p style="display:inline-block; flex:5"> {{li}} </p>
                <span class='el-icon-circle-close'
                style="flex:0.5"
                @click ="removeItem(index)"
                ></span>
            </div>
        </li>
    </transition-group>
    <p>
        <span class="el-icon-info" style="color:#22A39F"></span> 총 {{list.length}} 개의 목표중에 <br>
        {{list.length - startIndex}}개를 달성했어요!
    </p>
</div>
</template>
<script>
export default {
    data(){
        return {
            list : ['특급전사 달성', '프로젝트 완성', 'Node.js 공부','오픈소스 아카데미 제출'],
            listClass : [false, false, false, false],
            input : ""
        }
    },
    methods:{
        addList(value, check, toggle){
            value = value.trim();
            if(value === "") return;
            else{
                let startIndex = this.startIndex;
                if(check===false){
                    if(toggle===true){
                        this.list.splice(startIndex, 0, value);
                        this.listClass.splice(startIndex, 0, check);
                    }else{
                        this.list.splice(0, 0, value);
                        this.listClass.splice(0, 0, check);
                    }
                }else{
                    this.list.splice(startIndex, 0, value);
                    this.listClass.splice(startIndex, 0, check);
                }
                this.ClearInput();
            }
        },
        ClearInput(){
            this.input = "";
        },
        removeItem(index){
            this.list.splice(index,1);
            this.listClass.splice(index,1);
        },
        Toggle(index){
            let value = this.list[index];
            let check = this.listClass[index];
            let toggle = true;
            this.removeItem(index);
            this.addList(value, !check, toggle);
        }
    },
    computed:{
        startIndex : function() {
            let ret = this.list.length;
            for(let i=0; i<this.list.length;i++)
                if(this.listClass[i]) ret--;
            return ret;
        }
    },
}
</script>