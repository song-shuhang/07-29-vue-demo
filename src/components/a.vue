<template>
 <div class="course" id="course">
    <div class="editPanel">
        <label for="">序号：<input type="text" v-model="id"></label> 
        <!-- //v-model指令可以实现表单元素和model中数据的双向数据绑定 -->
        <label for="b">课程：<input type="text" id="b" v-model="cName"></label>    
        <label for="">教师：<input type="text" v-model="teacher" @keyup.enter="add"></label>
        <input type="button" value="添加" @click="add">
        <label class="search" for="">
            搜索：<input type="text" v-model="keyword" @keyup.enter="search(keyword)"></input>
        </label>
    </div>

    <div class="list">
        <table>
            <thead>
                <tr>
                  <th class="firstCol">序号</th>
                    <th>课程</th>
                    <th>教师</th>
                    <th>时间</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in list" :key="item.id"> 
                  <!-- //v-for循环的时候，key属性只能使用number获取string -->
<!-- 　　　　　　　　　//注意：key在使用的时候，必须使用v-bind属性绑定的形式，指定key的值。
　　　　　　　　　　　　　　　//加上一个key（能够保证数据的唯一性） -->
                    <td>{{item.id}}</td>
                    <td>{{item.cName}}</td>
                    <td>{{item.teacher}}</td>
                    <!-- <td>{{item.time | timeFormat('cn')}}</td> -->
                    <td>{{item.time}}</td>
                   <td>
                     <a href=""  @click.prevent="del(item.id)">删除</a>
                     <a href=""  @click.prevent="change(item)">编辑</a>
                   </td> 
                    <!-- //需要根据id传参 --> 
                </tr>
            </tbody>
        </table>
    </div>
    <!-- <div class="two" v-if="isShow"></div> -->
 </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data(){
      return{
          // isHo = false;
          number: "",
          id:'',

          cName:'',

          teacher:'',

          time:new Date().toLocaleString(),

          keyword:'',

          list:[

              {'id':1,'cName':'语文','teacher':'小明','time':'2020-1-3', aa: 1},

              {'id':2,'cName':'数学','teacher':'小红','time':'2020-2-3', aa: 2},

              {'id':3,'cName':'英语','teacher':'小华','time':'2020-3-3', aa: 3}

          ],
          rowtemplate: { 'id':'','cName':'','teacher':'','time':this.time }

      }
    },
    methods:{
      //增
      add(){
        let panduan = true
        console.log(this.number)
        this.list.forEach(item => {
          if (item.aa == this.number) {
            item.id = this.id
            item.cName = this.cName
            item.teacher = this.teacher
            // console.log("object")
            panduan = false
            // return
          }
        })

        console.log("add")
        if (panduan) {
          if (this.id.length>0 && this.cName.length>0 && this.teacher.length>0) {
            this.list.push({'id':this.id,'cName':this.cName,'teacher':this.teacher,'time':this.time,aa:this.time})
          }
          this.id='',this.teacher='', this.cName=''
        }
      },
      //查
      search(word){
        console.log(word)
        console.log('执行') 
        // debugger
        console.log(this.list)
        const rusult= []
        const lists = this.list
        const words = word.trim()
        // lists.forEach(item=>{
        //   if (item.cName.indexOf>-1) {
        //     rusult.push(item)
        //   }
        // })
        for (let i = 0; i < lists.length; i++) {
         if (words==lists[i].cName || words==lists[i].teacher || words==lists[i].id) {
            rusult.push(lists[i])
          }         
        }
        return this.list = rusult
                
      },
      //删
      del(id){
        // debugger
        for (let i = 0; i < this.list.length; i++) {
          if (this.list[i].id==id) {
             this.list.splice(i,1)
          }
          
        }
       
      },
      //改
 
      change(item){
          // console.log(item)
          console.log("chage")
          console.log(item)
          this.number = item.aa

          this.id = item.id
          this.cName = item.cName
          this.teacher = item.teacher

          // this.rowtemplate = item
        //   for (let i = 0; i < this.list.length; i++) {
        //   if (this.list[i].id==id) {
        //     // debugger
        //      this.rowtemplate= this.list[i]
        //     // this.list.filter()
        //   }
          
        // }
       
          // return this.rowtemplate
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
.course{

    width: 1200px;

    margin: 50px auto;

    border: 1px solid #ccc;

    border-radius: 5px;

}

.course .editPanel{

    border-bottom: 1px solid #ccc;

    padding: 20px;

}

.course .editPanel label{

    margin-right: 20px;

}

.course .editPanel input{            

    width: 150px;

    padding: 5px 10px;

    font-size: 14px;

    border-radius: 4px;

    outline: none;

    border: 1px solid #aaa;

}

.course .editPanel input[type=button]{

    width: 70px;

    background-color: rgb(50,120,180);

    padding: 5px 20px;

    letter-spacing: 5px;

    color: #eee;

}

.course .editPanel .search{

    margin-left: 50px;

}

.course .list{

    padding: 20px;

}

.course .list table{

    width: 100%;

    border: 1px solid #ccc;

    border-collapse: collapse;

}

.course .list table tr td,.course .list table tr th{
    // width 100%
    padding: 10px;

    border: 1px solid #ccc;

    text-align: center;

    font-size: 14px;

    line-height: 14px;

}

.course .list table tr td a{

    color: #369;

    text-decoration: none;

}

.course .list table .firstCol{

    width: 50px;

}
.two {
  width: 500px;
  height: 500px;
  z-index: 9999;
}

 
</style>
