<style scoped>
    #wrapper{
        display: flex;
        flex-direction: column;
    }
    #wrapper div {
        margin:5px;
    }
    #imgWrapper{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    p {
        margin:5px;
    }
    #img{
        width: 100px;
        height: 100px;
        border-radius: 50%;
        background-size: cover;
        background-image: url( "https://scontent-icn1-1.xx.fbcdn.net/v/t1.0-1/c1.0.160.160a/p160x160/56578170_574311579738337_5297769097927327744_n.jpg?_nc_cat=104&_nc_oc=AQloEMO3R-6Mhdj24TXtRvieIwKVQRpCiXPwbd8WPlgQN490KcMtqHbxLIRqHgwFEC8&_nc_ht=scontent-icn1-1.xx&oh=7af3daa000bb4aa1e95b1b76c0b73f76&oe=5E62FDDF" );
    }
    #info {
        width: 180px;
    }
    ul {
        margin:0;
    }
    ul li{
        text-align:left;
        margin:5px auto;
        padding :5px;
    }
    ul li span{
        float: right;
    }

    .el-icon-warning {
        color:gray;
    }
    span {
        color:#22A39F;
    }
    .el-icon-loading{
        color:#22A39F;
    }
    progress{
        background : yellow;
        width:80%;
        height:1.5em;
    }
    progress::-webkit-progress-bar {  
        background: #EFEFEF;
    }
    progress::-webkit-progress-value {  
        background: #22A39F;
    }
    
    .orange { border-left: 5px solid #F5876E; }

    .blue{ border-left: 5px solid #22A39F; }

    .green{ border-left: 5px solid #5ac18e; }

    .gold { border-left: 5px solid #D8C86E; }
    
    hr {
        width:100%;
        height:1px;
        border:0px;
        background: #CDCDCD;
    }

</style>

<template>
    <div>
        <div id="wrapper">
            <div id="imgWrapper">
                <div id="img"></div>
                <div id="info">
                    <p> {{user.grade}} {{user.name}}</p>
                    <el-input type="date"
                    suffix-icon="el-icon-date"
                    v-model="start"
                    @change="compute"
                    ></el-input>

                    <el-input type="date"
                    suffix-icon="el-icon-date"
                    v-model="end"
                    @change="compute"
                    ></el-input>

                </div>
            </div>
        </div>

        <progress max="100" :value="animatedPercent"> 
        </progress>
        
        <p v-if="computedDay.Remain === '계산중'" >
            <span class="el-icon-warning">
                입대일과 전역일을 입력해주세요.
            </span>
        </p>
        <p v-else-if="computedDay.Remain === '설정을 다시해주세요.'" >
            <span class="el-icon-warning">
                입대일과 전역일을 입력해주세요.
            </span>
        </p>
        
        <p id="number1" style="margin-bottom:0"
        v-else>{{animatedPercent}}%
        </p>
        <div style="height:1px; display:block;">
            <span id="airplane" class="el-icon-s-promotion"
            style="color:#5ac18e;"
            ></span>
        </div>

        <ul>
            <hr>
            <li class="green">
                <p>총 일
                    <span class='el-icon-loading'
                    v-if="computedDay.Remain === '계산중'"
                    ></span>
                    <span
                    v-if="computedDay.Remain !== '계산중'"
                    >{{computedDay.Total}}</span>
                </p>
            </li>
            <hr>
            <li class="blue">
                <p>한 날
                    <span class='el-icon-loading'
                    v-if="computedDay.Remain === '계산중'"></span>
                    <span
                    v-if="computedDay.Remain !== '계산중'"
                    >{{computedDay.Today}}</span>
                </p>
            </li>
            <hr>
            <li class="green">
                <p>남은 날
                    <span class='el-icon-loading'
                    v-if="computedDay.Remain === '계산중'"></span>
                    <span
                    v-if="computedDay.Remain !== '계산중'"
                    >{{computedDay.Remain}}</span>
                    </p>
            </li>
            <hr>
            <li class="blue">
                <p>남은 평일
                    <span class='el-icon-loading'
                    v-if="computedDay.Remain === '계산중'"></span>
                    <span
                    v-if="computedDay.Remain !== '계산중'"
                    >{{computedDay.Count}}</span>
                </p>
            </li>
            <hr>
        </ul>
    </div>
</template>

<script>

export default {
   data(){
       return{
           start:'',
           end:'',
           percent:'',
           animatedPercent:0,
           timerid:null,
           
           computedDay : {
               Remain : '계산중',
               Total : '계산중',
               Today : '계산중',
               Count : '계산중'
           },
           
           user:{
               name : "이도현",
               grade : "병장",
               start : '2018-05-14',
               end : '2020-01-08',
               weight : 82,
               goalweight : 77,
               height : 182,
           }
       }
   },
   methods:{
       increase(){
            //console.log('call increae()');
            var vm = this;
            let t1 = new Date(this.start.substr(0,4), this.start.substr(5,2) - 1, this.start.substr(8,2)); //입대일
            let Total = this.computedDay.Total;
            
            if(Total === this.computedDay.Today && Total != '계산중'){
                return this.animatedPercent = 100;
            }

            if(t1 > new Date()){
                return this.animatedPercent = 0;
            }
            
            let Future = (new Date() - t1 + 100000) / (1000 * 60 * 60 * 24);
            let newValue = Future / Total * 100;
            //console.log(Total);
            function animate () {
                if (TWEEN.update()) {
                    requestAnimationFrame(animate)
                }
            }

            this.animatedPercent *= 1;
            new TWEEN.Tween({ tweeningNumber: vm.animatedPercent })
                .easing(TWEEN.Easing.Quadratic.Out)
                .to({ tweeningNumber: newValue }, 100000)
                .onUpdate(function () {
                    vm.animatedPercent = this.tweeningNumber.toFixed(7);
                })
                .start()
            animate()
        },
        
        controllSetinerval() {
            var vm = this;
            vm.increase();
             if(this.timerid !== null){
                    clearInterval(this.timerId);
                    this.timerid = setInterval(function(){vm.increase()}, 100000);
             }else{
                 this.timerid = setInterval(function(){vm.increase()}, 100000);
             }
        },
        
        compute:function(){
            if(this.start !== '' && this.end !== ''){
                let t1 = new Date(this.start.substr(0,4), this.start.substr(5,2) - 1, this.start.substr(8,2)); //입대일
                let t2 = new Date(this.end.substr(0,4), this.end.substr(5,2) - 1, this.end.substr(8,2)) //전역일
                let diffTime = Math.abs(t1 - t2);
                let temp = new Date();
                let cnt = 0;

                while(temp < t2){
                    if(temp.getDay() == 0 || temp.getDay() == 6){

                    }else{
                        cnt++;
                    }
                    temp.setDate(temp.getDate()+1);
                }

                let Total = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                this.computedDay.Total = Total;
                let Today = (new Date() - t1) / (1000 * 60 * 60 * 24);
                
                this.animatedPercent = (Today / Total * 100).toFixed(8);
                Today = Math.floor(Today);
                let vm = this;
                
                if(this.timerid !== null){
                    clearInterval(this.timerId);
                    this.controllSetinerval()
                }else{
                    this.controllSetinerval()
                }

                if(Today > Total) Today = Total;

                if(t1 > t2){
                    return 
                    
                    this.computedDay = {
                        Total : '설정을 다시해주세요.',
                        Today : '설정을 다시해주세요.',
                        Remain : '설정을 다시해주세요.',
                        Count : '설정을 다시해주세요.',
                    }
                }else if(new Date() < t1){
                    return this.computedDay = {
                        Total : Total,
                        Today : 0,
                        Remain : Total,
                        Count : cnt
                    }
                }else
                    return  this.computedDay = {
                        Total : Total,
                        Today : Today,
                        Remain : Total - Today,
                        Count : cnt,
                    };
            }else{
                return this.computedDay =  {
                    Total : '계산중',
                    Today : '계산중',
                    Remain : '계산중',
                    Count : '계산중',
                }
            }
        }
   },

   created: function(){
       this.start = this.user.start;
       this.end = this.user.end;
       this.animatedPercent = 0;
       this.compute();
       
        setInterval(function(){
		    $("#airplane").animate({paddingTop:"10px"},1000);
	        $("#airplane").animate({paddingTop:"0px"},1000);
        }, 0);
   },
   destroyed:function(){
        if(this.timerid !== null){
            clearInterval(this.timerId);
        }
   }

}

</script>
