<template>
    <li @mouseenter="showBtn=true" @mouseleave="showBtn=false">
        <div>
            <span :style="{color:statusColor}">{{status}}</span> |
            {{title}}
        </div>
        <div class="btn-group">
            <button
                class="btn btn-complete"
                @click="handleClickComplete"
                :style="{background:completedColor}" >
                {{completeText}}
            </button>
            <button  @click="handleClick" class="btn btn-delete">删除</button>
        </div>
    </li>
</template>

<script>
export default {
    name:'todoItem',
    props:{
        id:{
            type:Number,
            required:true
        },
        title:{
            type:String ,
            required:true
        },
        completed:{
            type:Boolean,
            required:true
        },
        setCompleted:{
            type:Function,
            required:true
        },
    },
    data() {
        return {
            showBtn:false
        }
    },
    methods: {
        handleClick(){
            this.$bus.$emit('deleteTodo',this.id)
        },
        handleClickComplete(){
            this.setCompleted(this.id,!this.completed)
        }
    },
    computed:{
        statusColor(){
           return  this.completed ? '#34BB5C':'gray';
        },
        status(){
            return this.completed ? '完成':'未完成';
        },
        completeText(){
            return !this.completed ? '完成':'未完成';
        },
        completedColor(){
            return  !this.completed ? '#34BB5C':'gray';
        }
    }
}
</script>

<style scoped>
    li{
        list-style-type: none;
        border: 2px solid peachpuff;
        min-height: 35px;
        margin-bottom: 3px;
        display: flex;
        padding: 3px 3px;
        justify-content: space-between;
        align-items: center;
        
    }  
    li:hover{
        background: #2C72E8;
        color: white;
    }
    .btn-group{
        display: flex;
        align-self: stretch;
    }
    .btn{
        border: none;
        border-radius: 3px;
        width: 60px;
        align-self: stretch;
        outline: none;
        color: white;
        margin: 3px;
    }
    .btn-delete{
        background-color: #E93B2C;
      
    }
    .btn-delete:hover{
        cursor: pointer;
        background-color: rgb(230, 97, 55);
    }
    .btn-complete{
        cursor: pointer;
    }
    .btn-complete:hover{
        opacity: .7;
    }

</style>