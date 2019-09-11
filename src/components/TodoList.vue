<template>
  <ul>
      <TodoItem v-for=" {id,title,completed} in todos "
       :key="id" 
       :completed="completed"
       :setCompleted="setCompleted"
       :title="title"
       :id="id" 
       >
       </TodoItem>
  </ul>
</template>

<script>
import TodoItem from './TodoItem'
export default {
  props:{
    todos:{
      type:Array,
      required:true
    },
    setCompleted:{
      type:Function,
      required:true
    }
  },
  components:{
    TodoItem
  }
}

</script>

<style scoped>
  ul{
    min-height: 300px;
    overflow-y: auto;
    border: 1px solid #bbb;
    border-radius: 2px;
    padding: 3px;
  }

</style>