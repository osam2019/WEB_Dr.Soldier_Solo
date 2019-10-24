<style scoped>
  table{
      width: 80%;
      margin : 0 auto;
      border-collapse: collapse;
  }
  tr {
      text-align: left;
      border-top: 1px solid #CDCDCD;
      border-bottom: 1px solid #CDCDCD;
  }

  .title{
      font-weight: 900;
      color:rgb(90,90,90);
  }

  .content{
      font-size: 13px;
      color:gray;
  }

  .right {
      float:right;
  }

  .red {
      color:red;
  }

  .blue{
      color:#22A39F;
  }

  .green{
      color:#42b983;
  }
  .block{
      width: 100%;
  }

  .el-pagination{
      padding-top:16px;
  }
</style>

<template>
<div>
    
    <table>
        <tr v-for="(item, index) in write_list" :key="index">
            <div class="title">{{item.title}}</div>
            <div class="content">{{item.content}}
                <div>
                    <span class="el-icon-edit green"></span>{{item.writer}} 
                    <span class="el-icon-date green"></span>{{item.date}}
                
                    <span class="right">
                            <span class="el-icon-thumb red">{{item.good}}</span>
                            <span class="el-icon-chat-line-square blue">{{item.comment}}</span>
                    </span>
                </div>
            </div>
        </tr>
    </table>
    <el-pagination
    @current-change="handleCurrentChange"
    background
    layout="prev, pager, next"
    :total="50"
    >
    </el-pagination>
    <img src="/public/ad.png" style="width:100%">
</div>
</template>

  <script>
    export default {
        methods:{
            print:function(){
                console.log(1);
            },
            shuffle:function(array){
                var currentIndex = array.length, temporaryValue, randomIndex;
                while (0 !== currentIndex) {
                    randomIndex = Math.floor(Math.random() * currentIndex);
                    currentIndex -= 1;
                    temporaryValue = array[currentIndex];
                    array[currentIndex] = array[randomIndex];
                    array[randomIndex] = temporaryValue;
                }

                return array;
            },
            handleCurrentChange(val) {
                this.write_list = this.shuffle(this.write_list);
                this.write_list.reverse();
            }
      },
      data() {
          return {
            write_list:[
                {
                    title:"안녕하세요.",
                    content:"가입인사 드려요.",
                    good:3,
                    comment:2,
                    date:'2020-10-23',
                    writer:'leedh2004',
                },
                {
                    title:"오픈 소스 아카데미",
                    content:"매우 유익해요.",
                    good:6,
                    comment:5,
                    date:'2020-10-24',
                    writer:'xenos233'
                },
                {
                    title:"이제 전역까지",
                    content:"2달 남았어요.",
                    good:0,
                    comment:4,
                    date:'2020-10-24',
                    writer:'leedh2004',
                },
                {
                    title:"전곡 택시 같이타실분?",
                    content:"내일 휴가에요",
                    good:7,
                    comment:1,
                    date:'2020-10-24',
                    writer:'user4885',
                },
                {
                    title:"같이 사지방에서 코딩해요",
                    content:"사지방 신설됐어요.",
                    good:7,
                    comment:1,
                    date:'2020-10-24',
                    writer:'user4885',
                },
                
                {
                    title:"다음주 휴가에요",
                    content:"기대돼요!",
                    good:7,
                    comment:1,
                    date:'2020-10-24',
                    writer:'user4885',
                },
            ],
          }
      }
    }
  </script>