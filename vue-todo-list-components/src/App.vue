<template>
    <div id="app">
        <h2>
            Vue To Do List
            Simple Todo List with adding and filter by diff status.
        </h2>
        
        <div id="List">
            <ul>
                <li v-for="(item,index) in filteredTodoList" v-bind:key="index">
                    <input type="checkbox" @click="handlevent(index)">
                   {{item.content}}
                </li>
            </ul>
        </div>
        <div id="filter">
            当前状态:{{currentFilter}}
            <!-- <a>All</a> -->
            <button  @click="handleStatus('active')">Active</button>
            <button  @click="handleStatus('computed')">Complete</button>
             <createform @addNewToDo="add"></createform>
        </div>
    </div>

</template>

<script>
   import createform from './components/createform.vue'
    console.log(createform)
    export default {
        name: 'app',
        components: {
          createform 
        },
        data: function () {
            return {
                /**
                 * 定义了 todo item 中属性为 {content:'吃饭',status:'active'}
                 * 定义了 todo 的两种状态 completed、active，默认为 active
                 */
                todoList: [
                    {content:"吃饭",status:'active'},
                    {content:"写作业",status:'computed'}
                ],
                inputingText:"",
                currentFilter:'computed',
            }
        },
        methods:{
               add:function(inputingText){
                   console.log("45",this.inputingText)
                   this.todoList.push({
                       content:inputingText,
                       status:"active"
                   })
                   this.inputingText = "";
               },
            handleStatus:function(status){
                this.currentFilter=status;
            },
            handlevent:function(index){
                this.todoList[index].status = 'computed';
            }
         },
          
    computed : {
            filteredTodoList : function() {
                return this.todoList.filter(item=>item.status === this.currentFilter)
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
        margin-top: 60px;
    }

    .items {
        list-style: none;
        text-align: left;
        line-height: 30px;
    }

    .items li.completed {
        text-decoration: line-through;
    }

    .filter a {
        margin: 0 10px;
        line-height: 30px;
    }

    .filter a.active {
        color: #f60;
        border: 1px solid #ccc;
        border-radius: 2px;
        padding: 3px;
        cursor: pointer;
    }
</style>
