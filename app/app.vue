<style scoped lang="less">
.box {
    width: 600px;
    height: 400px;
    border: 1px solid #333;
    margin: 10px auto;
    padding: 10px;
}
</style>
<template>
    <div class="box">
    <input type="text" v-model.trim="txt" @keyup.enter="add">
    <button @click="add">提交</button>
    <ul>
        <li is="todoList" v-for="item of todos" :item="item"></li>
    </ul>
    <p>
        全部{{$store.state.todos.length}}件事&emsp;&emsp;已做{{$store.getters.yizuo.length}}件事&emsp;&emsp;未做{{$store.getters.weizuo.length}}件事
    </p>
    <p>
        <button @click="all">查看全部</button>
        <button @click="yizuo">查看已做</button>
        <button @click="weizuo">查看未做</button>
    </p>
    </div>
</template>
<script>
import todoList from "./components/todolist.vue"
export default {

  data(){
      return{
          txt:'',
          state:'all'
      }
  },
  created(){
      this.$store.dispatch("GETALL")
  },
  computed:{
      todos(){
        if(this.state == "all"){
            return this.$store.state.todos
        }else if(this.state == "yizuo"){
            return this.$store.getters.yizuo
        }else if(this.state == "weizuo"){
            return this.$store.getters.weizuo
        }
          
      }
  },methods:{
      add(){
          if(this.txt=="")return 
          var id = '';
          var str = '123456789';
          console.log(~~(Math.random()*str.length))
          for(var i = 0;i < 8;i++){
              id += str[~~(Math.random()*str.length)]
          }
          this.$store.dispatch("ADD",{
              id:id,
              title:this.txt,
              done:false
          })
          this.txt='';
      },
      all(){
          this.state = "all";
      },
      yizuo(){
          this.state = "yizuo";
      },
      weizuo(){
          this.state = "weizuo";
      }
  },
  components:{
      todoList
  }
}
</script>

