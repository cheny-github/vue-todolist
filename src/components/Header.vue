<template >
    <input type="text" placeholder="添加待办事项" @keypress.enter="handleEnter" v-model="title">
</template>

<script>
export default {
    props:{
        addTodo:{
            type:Function,
        }
    },
    data() {
        return {
            title:''      
        }
    },
    methods: {
        handleEnter(){
            const todo ={
                id:Date.now(),
                completed:false,
                title:this.title
            }
            this.$emit('addTodo',todo)
            this.title=''
        }
    },
}
</script>

<style scoped>
    input{
        display: block;
        box-sizing: border-box;
        width: 100%;
        height: 35px;
        font-size:16px;
        border-radius: 5px;
        outline: none;
        border: 2px solid #ccc;
        padding: 0 1px;
    }
    input::placeholder{
        font-size: 16px;
    }
</style>