<template>
  <div>
    <slot name="left"></slot>

    <slot name="middle"> </slot>

    <slot name="right"> </slot>

  </div>
</template>

<script>
export default {
  props:{
    removeCompleted:{
      type:Function,
      required:true
    },
    completeAll:{
      type:Function,
      required:true
    },
    todos:{
      type:Array,
      required:true
    }
  },
  computed: {
 
  },
  methods: {
   
  },
}
</script>

<style scoped>
  div{
    display: flex;
    padding-left: 10px;
    height: 35px;
    justify-content: space-between;
    align-items: center;
  }
  button{
    background-color: rgb(230, 97, 97);
    border: none;
    border-radius: 3px;
    width: 150px;
    align-self: stretch;
    outline: none;
    color: white;
  }
  button:hover{
      cursor: pointer;
      background-color: rgb(230, 97, 55);
  }
</style>