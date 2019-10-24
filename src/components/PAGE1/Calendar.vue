<style scoped>
    table {
        margin: 20px auto;
        width:91%;
        border-collapse: collapse;
    }
    thead td{
        text-align: center;
    }
    table > tr > td {
        height:50px;
    }
    td {
        border: 1px #CDCDCD solid;
        padding : 0;
        width:13%;
        text-align:left;
        vertical-align: top;
        color:gray;
    }
    
    .generaltd{
        height: 50px;
    }

    .redHead{
        color:red
    }
    .redTd{
        background-color:#ff7373;
        color:white;
    }
    .whiteTd{
        background-color: white;
        color:gray;
    }
    .greenTd{
        background-color: #5ac18e;
        color:white;
    }
    .blueTd{
        background-color:#22A39F;
        color:white;
    }
    .orangeTd{
        background-color: #e8a87c;
        color:white;
    }
    .brownTd{
        background-color:#bc986a;
        color:white;
    }

    .el-input {
        width : 60%;
    }
    .el-select{
        width: 100px;
    }
    .colorbox{
        display: inline-block;
        width: 10px;
        height: 10px;
        margin:2px;
    }
    .grayTd{
        color:gray;
    }
</style>

<template>
<div>
    <el-input
        placeholder="친구의 일정을 확인해요"
        v-model="otherid">
    </el-input>
    <span class="el-icon-search"
        @click="print"
    ></span>
    <br>
    <div>
        <p style="inline-block">
            <el-button icon="el-icon-caret-left" circle
            style="color:#22A39F; margin:0 5px"
            @click = "beforeMonth"
            ></el-button>
            {{today.getFullYear()}}년 {{today.getMonth()+1}}월
            <el-button icon="el-icon-caret-right" circle
            @click="nextMonth"
            style="color:#22A39F; margin:0 5px"></el-button>
        </p>
        </div>
    <table>
        <thead>
            <tr>
                <td v-for="(d,index) in dw" :key=index
                    v-bind:class="[[0,6].indexOf(index) > -1  ? redHeadClass : '']"
                >{{d}}</td>
            </tr>
        </thead>
        <tr v-for="(row,index) in rows" :key="index" >
                <td v-for="(date,index) in row" :key=index
                     v-bind:class="[ [0,6].indexOf(index) > -1  ? redClass : '', 
                        color[info[date-1]]
                     ]"
                     v-on:click="changeColor(date)" 
                >{{date}}</td>
        </tr>
    </table>
    <el-select v-model="value" placeholder="편집">
        <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value">
        </el-option>
    </el-select>
    <br>
    <div style="display:flex; justify-content:center; align-items:center">
    <span class="colorbox"
    style="background:#42b983"
    ></span>휴가
    <span class="colorbox"
    style="background:#e8a87c"></span>훈련
    <span class="colorbox"
    style="background:#22a39f"></span>파견
    <span class="colorbox"
    style="background:#bc986a;"></span>외출
    </div>
</div>
</template>

<script>
export default {
    methods:{
        print(){
            this.info = this.user2.info;
        },
        build(){
            //DB 휴가에 따른 색변경..
            let nMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 1); //현재달의 첫째 날
            let lastDate = new Date(this.today.getFullYear(), this.today.getMonth() + 1, 0); //현재 달의 마지막 날

            let rows = [];
            let row = [];
            
            for(let i=0; i<nMonth.getDay(); i++) {
                row.push(undefined);
            }
            
            for(let i=1; i<=lastDate.getDate(); i++){
                row.push(i);
                if(i==lastDate.getDate()) rows.push(row);
                else if(row.length == 7){
                    rows.push(row);
                    row = [];
                }
            }
            while(rows[rows.length-1].length < 7){
                rows[rows.length-1].push(undefined);
            }
            this.rows = rows;
       },
       nextMonth(){
           this.today = new Date(this.today.getFullYear(), this.today.getMonth() + 1, this.today.getDate());
           this.build();
       },
       beforeMonth(){
           this.today = new Date(this.today.getFullYear(), this.today.getMonth() - 1, this.today.getDate());
           this.build();
       },
       changeColor(index){
           var newValue = this.value;
           this.info.splice(index-1, 1, newValue);
       }
    },
    data(){
        return{
            dw : ['SUN','MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'],
            today : new Date(),
            date : new Date(),
            rows:undefined,
            info:undefined, //출타 정보
            color:['', 'greenTd', 'orangeTd','blueTd','brownTd','whiteTd'],
            redHeadClass: 'redHead',
            redClass:'redTd',
            otherid : '',
            options: [{
                value: 1,
                label: '휴가'
                }, {
                value: 2,
                label: '훈련'
                }, {
                value: 3,
                label: '파견'
                }, {
                value: 4,
                label: '외출'
                }, {
                value: 5,
                label: '삭제'
                }
            ],
            value: '편집',
            user1:{
                info : [0,0,0,2,2,1,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3,3,0]
            },
            user2:{
                info : [3,3,3,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,4,4,4,4,0,0,0,0,0,0],
            }
        }
    },
    beforeMount:function(){
        this.info = this.user1.info;
        this.build();
        /*실제로는 DB 추출*/
    },
}
</script>
