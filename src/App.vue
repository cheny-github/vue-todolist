<template>
  <div id="app">
    <Header @addTodo="addTodo"></Header>
    <TodoList
     :todos="todos"
     :deleteTodo="deleteTodo" 
     :setCompleted="setCompleted"></TodoList>
    <Footer>
      <label slot="left">
        全部完成:
        <input type="checkbox" :checked="checked" @click="handleClickCompleteAll">
      </label> 

      <span slot="middle">
        已完成:{{completedCount}}/{{todos.length}}
      </span>
       <button slot="right" @click="handleClickRemoveCompleted">删除所有已完成项目</button>
    </Footer>
  </div>
</template>

<script>
import Header from './components/Header'
import TodoList from './components/TodoList'
import Footer from './components/Footer'

export default {
  name: 'app',
  data() {
    return {
      todos:[]
    }
  },
  components: {
    Header,
    TodoList,
    Footer,
  },
  methods: {
    addTodo(todo){
      this.todos.unshift(todo)
    },
    deleteTodo(id){
     this.todos = this.todos.reduce((pre,todo)=>{
        todo.id!==id && pre.push(todo)
        return pre
      },[])
    },
    setCompleted(id,flag){
      this.todos.find((todo)=>todo.id===id).completed=flag
    },
    completeAll(flag){
      this.todos.forEach(todo=>todo.completed=flag)
    },
    removeCompleted(){
     this.todos= this.todos.reduce((pre,todo)=>{
        !todo.completed && pre.push(todo)
        return pre
      },[])
    },
     handleClickCompleteAll(){
      // flag为true表示todos中存在至少一个没有完成的项目
      const flag = this.todos.some(todo => !todo.completed);
      this.completeAll(flag)
    },
    handleClickRemoveCompleted(){
      this.removeCompleted()
    }
  },
  mounted() {
    this.$bus.$on("deleteTodo",this.deleteTodo)
    try {
      this.todos = JSON.parse(localStorage.getItem("todos_key")||"[]")
    } catch (e) {
      
    }

  },

  computed: {
    completedCount(){
        return this.todos.reduce((pre,item)=>{
            return pre + item.completed
        },0)
    },
    checked(){
        return this.todos.length === this.completedCount
    }
  },
  watch: {
    todos:{
      deep:true,
      handler(value,oldValue){
        localStorage.setItem("todos_key",JSON.stringify(value))
       }
      }
    }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 400px;
  width: 700px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  border: 1px solid #ccc;
  border-radius: 13px;
  padding: 10px;
}
</style>
