<template>
  <div>
    <header>待办事项</header>
    <div>
      <label for="">待办标题</label>
      <el-input style="width: 30vw;margin-right: 1vw;margin-top: 20px" placeholder="请输入待办事项" v-model="text"></el-input>
      <el-button type="primary" size="small" round @click="addTodo">添加待办</el-button>
    </div>
    <el-row style="margin-top: 20px" v-for="(item,index) in todolist" :key="index">
      <el-col :span="24">
        <el-card shadow="hover">
          <el-row>
            <el-col :span="18">{{item.title}}</el-col>
            <el-col :span="6">
              <el-button type="success" size="small" @click="todoOver(item,index)" round>完成待办</el-button>
              <el-button type="danger" size="small" @click="deleteTodo(index,1)" round>删除待办</el-button>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
    <header>完成事项</header>
    <el-row style="margin-top: 20px" v-for="(item,index) in todoOvers" :key="item.title">
      <el-col :span="24">
        <el-card shadow="hover">
          <el-row>
            <el-col :span="18">{{item.title}}</el-col>
            <el-col :span="6">
              <el-button type="success" size="small" @click="recovery(item,index)" round>恢复待办</el-button>
              <el-button type="danger" size="small" @click="deleteTodo(index,2)" round>删除记录</el-button>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
     todolist:[
       {title:'待办事项1'}
     ],
      todoOvers:[
        {title:'待办事项2'}
      ],
      text:'',
    }
  },
  methods:{
    addTodo(){
      if(this.text !== ''){
        this.todolist.push({title:this.text})
        this.text=''
      }else {
        this.$message({
          message: '待办标题不能为空,请填写内容在点击添加!',
          type: 'warning'
        });
      }

    },
    todoOver(item,index){
      this.todoOvers.push(item)
      this.todolist.splice(index,1)
    },
    recovery(item,index){
      this.todolist.push(item)
      this.todoOvers.splice(index,1)
    },
    deleteTodo(index,flag){
      if(flag == 1){
        this.todolist.splice(index,1)
      }else{
        this.todoOvers.splice(index,1)
      }

    }
  },

}
</script>
<style scoped>
  header{
    font-size: 22px;
    color: #666666;
    font-weight: bold;
    text-align: center;
    height: 40px;
    line-height: 40px;
    margin-top: 20px;
  }
</style>
