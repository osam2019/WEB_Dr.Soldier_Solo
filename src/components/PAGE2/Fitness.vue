
<style scoped>
.fit{
    display: inline-block;
}
.block{
    margin:40px 0;
}

.el-select{
    width:100px;
}
.el-slider{
    width:60%;
    display: inline-block;
}
.el-slider__runway {
    width:100%;
    margin:0 auto;
    height: 10px;
}
.el-slider__bar{
    background-color: #42b983;
    height: 10px;
}

.el-slider__button {
    border: 3px solid #42b983;
}
img {
    width: 2em;
}

.el-icon-success {
   font-size:30px;
   color:gray;
}
.change{
   color:#5ac18e;
}
svg {
    fill:#22A39F;
}
.block{
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin:0px;
}
.blue_text{
    color:#42b398;
    font-weight: 900;
}

.rowWrapper{
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>

<template>
<div>
    <div>
        <p class="fit">목표등급</p>
        <el-select v-model="value" placeholder="Select">
            <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value">
            </el-option>
        </el-select>
    </div>
    
    <div class="block">
        <svg width="2em" height="2em" viewBox="0 -87 511.99995 511" xmlns="http://www.w3.org/2000/svg"><path d="m452.066406 120.503906c7.082032 0 14.28125-1.265625 21.28125-3.929687 30.917969-11.773438 46.496094-46.503907 34.722656-77.421875-11.773437-30.917969-46.503906-46.496094-77.421874-34.722656-30.917969 11.769531-46.492188 46.503906-34.71875 77.417968 9.105468 23.921875 31.945312 38.65625 56.136718 38.65625zm-7.183594-78.691406c2.332032-.890625 4.734376-1.3125 7.09375-1.3125 8.0625 0 15.679688 4.914062 18.714844 12.882812 3.921875 10.308594-1.269531 21.886719-11.574218 25.808594-10.304688 3.925782-21.882813-1.265625-25.808594-11.574218-3.921875-10.304688 1.269531-21.882813 11.574218-25.804688zm-55.941406 57.582031c-7.519531-25.28125-30.292968-42.523437-56.664062-42.898437-8-.101563-15.839844 1.359375-23.253906 4.355468l-135.542969 54.265626c-15.015625 5.859374-26.816407 17.230468-33.230469 32.023437-6.429688 14.828125-6.652344 31.257813-.621094 46.253906l7.730469 19.222657-147.359375 58.246093.078125.199219h-.078125v67h511.988281v-40h-63.417969zm-212.203125 79.074219c-2.007812-5-1.9375-10.476562.207031-15.417969 2.144532-4.941406 6.089844-8.738281 11.113282-10.6875l135.890625-54.402343c2.503906-1.011719 5.105469-1.511719 7.757812-1.46875 8.792969.125 16.390625 5.875 18.914063 14.355468l56.1875 187.214844h-366.804688l290.554688-114.851562-11.449219-38.484376-134.550781 53.1875zm0 0"/></svg>
        <el-slider v-model="pushup" :max="mpushup[value]"
         status="warning"
         :format-tooltip="formatTooltip2"
        > </el-slider>
        <span class="el-icon-success"
        :class="{change : pushup == mpushup[value]}"> </span>
    </div>
    <p style="margin:0">{{pushup}}회 / 2분</p>

    <div class="block">
        <svg height="2em" viewBox="0 -70 512 512" width="2em" xmlns="http://www.w3.org/2000/svg"><path d="m381.679688 184.265625-57.03125 60.171875-135.441407-121.753906 64.792969-73.09375v-28.589844h-137.460938c-11.011718-12.839844-27.335937-21-45.539062-21-33.085938 0-60 26.914062-60 60s26.914062 60 60 60c32.75 0 59.4375-26.378906 59.976562-59h59.457032l-70.648438 79.699219c-10.691406 12.0625-16.011718 27.566406-14.976562 43.652343 1.035156 16.085938 8.296875 30.78125 20.449218 41.371094l105.679688 92.136719c8.921875 7.78125 19.476562 12.472656 30.359375 14.140625h-261.296875v40h512v-56.230469zm-310.679688-104.265625c-11.027344 0-20-8.972656-20-20s8.972656-20 20-20 20 8.972656 20 20-8.972656 20-20 20zm186.222656 207.710938-105.679687-92.136719c-4.050781-3.53125-6.472657-8.429688-6.816407-13.792969-.34375-5.359375 1.429688-10.527344 4.992188-14.550781l12.957031-14.613281 134.445313 120.859374-12.238282 12.914063c-7.402343 7.808594-19.550781 8.390625-27.660156 1.320313zm22.21875 44.289062c12.722656-1.949219 24.917969-8.011719 34.46875-18.089844l68.410156-72.175781 89.449219 90.265625zm0 0"/></svg>
        <el-slider v-model="situp" :max="msitup[value]"
         status="warning"
         :format-tooltip="formatTooltip2"
        ></el-slider>
        <span class="el-icon-success"
        :class="{change : situp == msitup[value]}"> </span>
    </div>
    <p style="margin:0">{{situp}}회 / 2분</p>

    <div class="block">
        <svg height="2em" viewBox="-13 0 512 512" width="2em" xmlns="http://www.w3.org/2000/svg"><path d="m425.851562 120.421875c33.199219 0 60.210938-27.007813 60.210938-60.210937 0-33.199219-27.011719-60.210938-60.210938-60.210938-33.199218 0-60.210937 27.011719-60.210937 60.210938 0 33.203124 27.011719 60.210937 60.210937 60.210937zm0-80.28125c11.066407 0 20.070313 9.003906 20.070313 20.070313 0 11.066406-9.003906 20.070312-20.070313 20.070312-11.066406 0-20.070312-9.003906-20.070312-20.070312 0-11.066407 9.003906-20.070313 20.070312-20.070313zm-24.085937 123.335937-156.390625-137.40625-89.398438 97.878907 29.640626 27.070312 62.84375-68.804687 44.292968 38.914062-95 105.683594c-22.058594 24.542969-20.152344 62.574219 4.25 84.785156l89.378906 81.347656-81.316406 92.5625 30.15625 26.492188 107.347656-122.195312-73.925781-67.285157 87.980469-97.875v80.429688h123.433594v-40.144531h-83.292969zm-172.742187 118.433594c-8.136719-7.402344-8.769532-20.082031-1.417969-28.261718l95.304687-106.019532 30.15625 26.492188-109.113281 121.378906zm-85.039063 3.601563c2.644531 14.253906 8.359375 28.007812 17.09375 40.164062l-55.925781 60.554688-105.152344-94.316407 26.804688-29.878906 76.09375 68.253906zm0 0"/></svg>
        <el-slider v-model="run" :max="mrun[value]"
         status="warning"
         :format-tooltip="formatTooltip"
        ></el-slider>
        <span class="el-icon-success"
        :class="{change : run == mrun[value]}"> </span>
    </div>
    <p style="margin:0">{{formatTooltip(run)}} / 3km</p>

    <p>
        현재 당신의 체력은 <span class="blue_text">{{label[grade]}}</span> 입니다.
    </p>
    <p>
        {{user.grade}} 기준 체력은 {{condition}}급입니다.<br>
    </p>
    <div v-if="grade <= condition"
        class="rowWrapper"
    >
        <span class="el-icon-info" style="color:#22A39F;font-size:1.5em; margin:2px;"></span>
        훌륭한 체력을 가지고 있군요!
    </div>
    <div class="rowWrapper"
    v-else>
        <span class="el-icon-info" style="color:palevioletred;font-size:1.5em; margin:2px;"></span>
        기준체력을 달성하도록 조금 더 분발하세요!
    </div>

</div>
</template>

<script>
export default {
   data() {
      return {
            condition:1,
            pushup:36,
            situp:43,
            run :50,
            label : ['특급', '1급', '2급', '3급', '불합격'],
            mpushup:[72, 64, 56, 48],
            msitup:[86, 78, 70, 62],
            mrun:[100, 92.59, 86.20, 80.64],
            options: [{
            value: 0,
            label: '특급',
            }, {
            value: 1,
            label: '1급'
            }, {
            value: 2,
            label: '2급'
            }, {
            value: 3,
            label: '3급'
            }],
            value: 0,
            user:{
                grade:"병장",
                pushup:68,
                situp:86,
                run:95
            }
        }
    },
    methods: {
        formatTooltip(val) {
            let a = 75000;
            if (val == 0) val = 1;
            let b = a / val;
            return Math.floor(b/60)+ '분' + Math.round(b%60) +'초';
        },
        formatTooltip2(val) {
            return val + '회/2분'
        },
    },
    computed: {
        grade : function(){
            let grade = 0;
            for(let i=0; i<4; i++){
                if(this.pushup < this.mpushup[i] ||
                this.situp < this.msitup[i] ||
                this.run < this.mrun[i] ){
                    grade = grade > i + 1 ? grade : i + 1;
                }
            }
            return grade;
        }
    },
    created:function(){
        this.pushup = this.user.pushup;
        this.situp = this.user.situp;
        this.run = this.user.run;
    }
}
</script>
