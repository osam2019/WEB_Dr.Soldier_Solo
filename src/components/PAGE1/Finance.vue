
<style scoped>
.el-input {
    width: 40%;
}
p{
    line-height: 1.5em;
}

.blue{
    color:#22A39F;
    font-size: 900;
}

.green{
    color:#5ac18e;
    font-size: 900;
}
.small{
    width: 20%;
}
.small2{
    width:15%;
}
</style>

<template>
<div>
    <p>{{user.grade}} 월급은 
        <span class="blue">
            {{monthPay[0].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}
        </span>
    원이에요.<br>
    군대에서 총 <span class="blue"> {{totalPay.toFixed(0).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}
        </span>원을 받아요.<br>
    오늘부터 전역까지 <span class="blue"> {{(todaytoFuturePay.toFixed(0) - monthPay[0]).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")  }}
        </span>원을 모을 수 있어요.</p>
    <el-input
    placeholder="현재 저축금액"
    prefix-icon="el-icon-coin"
    v-model="current">
  </el-input>
  <span class="el-icon-right"></span>
  <el-input
    placeholder="목표 저축금액"
    prefix-icon="el-icon-coin"
    v-model="future">
  </el-input>
    <p>전역까지 하루에 <span class="green">{{computedPay.toFixed(0).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span>원씩,<br>
    한달에 <span class="green">{{(computedPay * 30).toFixed(0).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span>원씩 저축 하세요.</p>

    <p style="padding: 15px 0">
        매 달 
        <el-input
        placeholder="적금 금액"
        prefix-icon="el-icon-coin"
        v-model.number="save"
        class="small">
        </el-input> 만원씩
        <el-input
    placeholder="개월"
    prefix-icon="el-icon-date"
    v-model.number="savemonth"
    class="small"
        >  </el-input> 달동안<br>
        연이율
  <el-input
    placeholder="연이율"
    v-model.number="savepercent"
    class="small2"
    >
  </el-input>
   % 상품에 적금 한다면  
    </p>
    <p>
        <span class="blue">{{computeSavePercent.total.toFixed(0).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span> 원이 모이겠군요.<br>
        이자로 받는 금액은 <span class="blue">{{ computeSavePercent.profit.toFixed(0).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span> 원이에요.
    </p>
</div>
</template>

<script>
export default {
    methods:{
        calc(start, end){
            let day = [31,28,31,30,31,30,31,31,30,31,30,31];
            let total = 0;

            while(start <= end){
                let i;
                for(i=0; i<3; i++){
                    if(start < this.upgrade[i]) break;
                }
                let monthPay = this.monthPay[3-i];
                let dayPrice = monthPay / day[start.getMonth()];
                total += dayPrice;
                start.setDate(start.getDate()+1);
            }
            return (total);
        },
    },
    data(){
        return{
            save:'',
            savemonth:'',
            savepercent:'',
            totalsave:0,
            current:0,
            future:0,
            monthPay:[405669,366229,331296,306130],
            totalPay:0,
            todaytoFuturePay:0,
            upgrade:[new Date('2018','09','01'),
            new Date('2018','04','01'),
            new Date('2019','10','01')],
            user:{
               name : "이도현",
               grade : "병장",
               start : '2018-05-14',
               end : '2020-01-08',
               weight : 82,
               goalweight : 77,
               height : 182,
           },
        }
    },
    created:function(){
        this.totalPay = this.calc(new Date('2018','05','14'));
        this.todaytoFuturePay = this.calc(new Date(), new Date('2020', '01', '08'));
    },
    computed:{
        computedPay:function(){
            let m = this.future - this.current;
            if(m < 0) return 0;
            let t1 = new Date('2020', '01', '08');
            let t2 = new Date('2019', '10', '24');
            let remain = (t1-t2) / (1000 * 60 * 60 * 24);
            return m / remain;
        },
        computeSavePercent:function(){
            let ret = 0 ;
            if(this.savemonth === '' || this.save === '' || this.savepercent === '') return {total:0, profit:0};
            
            for(let i=1; i<= this.savemonth ; i++){
                let temp =  ((this.save * 10000) * (1 + ( (i / 12)*(this.savepercent/100)))) ;
                ret += temp;
            }
            return { 
                total : ret,
                profit : ret - (this.savemonth * this.save * 10000)
            }
        }
    }
}
</script>
