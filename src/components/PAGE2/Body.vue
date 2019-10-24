<style scoped>

button{
    border:none;
    position:relative;
    font-size:1em;
    height:2em;
    padding:0 0.5em;
    cursor:pointer;
    transition:800ms ease all;
    outline:none;
    background:#22a39f;
    color:#F6F6F8;
    margin : 10px;
}

.el-input{
    width:30%;
}

.el-input-number__increase {
    width:20px;
    height:20px;
}

.el-icon-warning {
    color: #42b983;
}

.el-input-number{
    width:140px;
}
.el-select{
    width:30%;
}

p{
    margin-top:0;
}
table{
    margin: 0 auto;
    border-collapse: collapse;
}
td{
    color:gray;
    background-color: white;
    border:1px solid gray;
}

.blue_text{
    font-weight: 900;
    color:#22A39F
}

.green_text{
    font-weight: 900;
    color:#42b983;
}

</style>
<template>
<div>
    <el-input placeholder="키(cm)" v-model="height"
    suffix-icon="el-icon-edit"
    ></el-input>
    <el-input placeholder="무게(kg)" v-model="weight"
    suffix-icon="el-icon-edit"
    ></el-input>
    <el-input placeholder="목표(kg)" v-model="goalweight"
    suffix-icon="el-icon-edit"
    ></el-input>
    <el-input-number v-model="age" :min="1" :max="100">
    </el-input-number>
    <el-select v-model="value" placeholder="Select">
        <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value">
        </el-option>
  </el-select>
    <button
    @click = "updateData"
    >기록</button>
    <div id="chart">
      <apexchart type=area height=200 :options="chartOptions" :series="series" />
    </div>
    <p v-if="BMR==''" style="line-height:2em;">
         <span class='el-icon-loading' style="color:red"></span> 데이터를 입력해주세요.<br>
         계산된 결과를 알려드릴게요.
    </p>

    <p v-if="BMR!=''">
        당신의 비만도 지수는 {{BMI}} 으로<br>
        <span class="blue_text">{{status}}</span>입니다.<br>
        
        <span class="el-icon-warning"></span>지금부터 
        <el-input-number v-model="totaldate" :min="1" :max="365"
        @change="handleChange">
        </el-input-number>일간 <span class="blue_text"> {{this.goalweight}}kg</span>가 되시려면, 하루에 
        <span class="blue_text">{{dynamicCal}}kcal</span>를 섭취해주세요.
    </p>
    <table v-if="BMR!=''">
        <tr>
            <td> 기초대사량 </td>
            <td> 활동대사량 </td>
            <td> 소화대사량 </td>
            <td style="font-weight:900"> 총 대사량 </td>
        </tr>
        <tr>
            <td> {{BMR}}kcal </td>
            <td> {{MR}}kcal</td>
            <td> {{TMR}}kcal</td>
            <td class="green_text"> {{totalR}}kcal </td>
        </tr>
    </table>

</div>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

export default {
    components: {
        apexchart: VueApexCharts,
    },
    
    data(){ return {
        dynamicCal:0,
        status:'',
        BMR:'',
        MR:'',
        TMR:'',
        BMI:'',
        dayminus:'',
        totaldate:30,
        totalR:'',
        options: [{
          value: 1,
          label: '매우 적음'
        }, {
          value: 2,
          label: '적음'
        }, {
          value: 3,
          label: '보통'
        }, {
          value: 4,
          label: '많음'
        }, {
          value: 5,
          label: '매우 많음'
        }],
        value: '활동량',
        age:20,
        height:'',
        weight:'',
        goalweight:'',
        selection: 'all',
        series: [{
            data: [
            ]
        }],
        chartOptions: {
            annotations: {
                yaxis: [{
                    y: 70,
                    borderColor: '#999',
                    label: {
                        show: true,
                        text: '목표 몸무게',
                        style: {
                            color: "#fff",
                            background: '#00E396'
                        }
                    }
                }]
            },
            dataLabels: {
                enabled: false
            },
            markers: {
                size: 6,
                style: 'hollow',
            },
            xaxis: {
                type: 'datetime',
                min: undefined,
                max: undefined,
                tickAmount: 1,
            },
            yaxis:{
                min: undefined,
                max: undefined,
            },
            tooltip: {
                x: {
                    format: 'dd MMM yyyy'
                }
            },
            fill: {
                type: 'gradient',
                gradient: {
                    shadeIntensity: 0,
                    opacityFrom: 0,
                    opacityTo: 0,
                    stops: [0, 0]
                }
            },
             stroke: {
                curve: 'straight'
            },
        }
    }},
    methods: {
        updateData: function () {
            let newData = [new Date(), this.weight*=1];
            this.series[0].data.push(newData);
            this.chartOptions = {
                 annotations: {
                yaxis: [{
                    y: (this.goalweight*=1),
                    borderColor: '#999',
                    label: {
                        show: true,
                        text: '목표 몸무게',
                        style: {
                            color: "#fff",
                            background: '#00E396'
                        }
                    }
                }]
            },
                xaxis: {
                    min: undefined,
                    max: undefined
                },
            }
            this.calc();
            this.calcBMI();
        },
        calc(){
            let arr = [0.2, 0.375, 0.555, 0.725, 0.9];
            this.BMR =  10 * this.weight + 6.25 * this.height - 5.0 * this.age + 5;
            this.BMR = this.BMR.toFixed(0);
            this.MR = this.BMR * arr[this.value - 1];
            this.MR = this.MR.toFixed(0);
            this.TMR = (this.BMR*1 + this.MR*1) * 0.1;
            this.TMR = this.TMR.toFixed(0);
            this.totalR = this.BMR*1 + this.MR*1 + this.TMR*1;
            let minus = (this.weight*1 - this.goalweight*1) * 7000;
            this.dayminus = (minus / this.totaldate).toFixed(0);
            this.handleChange();
        },
        calcBMI(){
            let BMI = this.weight / ((this.height/100.0) *  (this.height/100.0));
            BMI = BMI.toFixed(1);
            let status;
            if(BMI < 18.5) status = '저체중';
            else if (BMI < 25) status = '정상';
            else if (BMI < 30) status = '과체중';
            else if (BMI < 35) status = '중등도 비만';
            else status = '고도비만';
            this.BMI = BMI;
            this.status = status;
        },
        handleChange(){
            let minus = (this.weight*1 - this.goalweight*1) * 7000;
            this.dayminus = (minus / this.totaldate).toFixed(0);
            this.dynamicCal = this.totalR - this.dayminus;
        }
    },
    computed:{
    }
}
    
</script>
