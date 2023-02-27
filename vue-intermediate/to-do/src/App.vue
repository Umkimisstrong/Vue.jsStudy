<template>
    <div id="app">
        <todo-header></todo-header>
        <!-- 
            v-on
            하위 컴포넌트에서 상위컴포넌트로 발생시킨 이벤트 이름="메소드명"
         -->
        <todo-input v-on:addTodoItem="addOneItem"></todo-input>
        <!-- 
            props
            내려보낼 프롭스(Props) 속성 이름 = todoItems
         -->
        <todo-list v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleComplete="toggleOneItem"></todo-list>
        <todo-footer v-on:clearTodo="clearAllItems"></todo-footer>
    </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
    data : function () {
        return {
            todoItems : []
        }
    },
    methods: {
        addOneItem:function (todoItem){
            var obj = {completed:false, item:todoItem};
            localStorage.setItem(todoItem, JSON.stringify(obj));
            this.todoItems.push(obj);
        }
        , removeOneItem : function (todoItem, index){
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1); 
        }
        , toggleOneItem : function (todoItem, index){
            //todoItem.completed = !todoItem.completed;
            this.todoItems[index].completed = !this.todoItems[index].completed;
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));

        }
        , clearAllItems : function ()
        {
            localStorage.clear();
            this.todoItems = [];
        }
    },
    created : function () {
        if(localStorage.length > 0) {
            for(var i = 0; i < localStorage.length; i++) {
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    var obj = JSON.parse(localStorage.getItem(localStorage.key(i)));
                    this.todoItems.push(obj);
                }
            }
        }
    },
    components: {
        // 컴포넌트 태그명 :내용
        'TodoHeader': TodoHeader,
        'TodoInput': TodoInput,
        'TodoList': TodoList,
        'TodoFooter': TodoFooter,

    }
}
</script>

<style>

body { text-align: center; background-color: #f6f6f6;}

input { border-style: groove; width: 200px;}

button {border-style: groove;}

.shadow {box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.3); }
</style>
