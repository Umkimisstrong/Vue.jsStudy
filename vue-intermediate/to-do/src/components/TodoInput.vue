<template>
    <!-- TodoInput -->
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <button class="addBtn">add</button>
        </span>


    </div>
</template>

<script>
export default {
    data : function ()  {
        return  {
            newTodoItem: ""
        }
    },
    methods: {

        addTodo : function (){
            //console.log(this.newTodoItem);
            // 저장하는 로직
            // 개발자도구의 애플리케이션 - 로컬스토리지에 key / value 로 저장이 된다.
             localStorage.setItem(this.newTodoItem, this.newTodoItem);
            this.clearInput();
        },
        clearInput : function () {
            this.newTodoItem = '';
        }
   },
}

</script>

<style scoped>

input:focus {
    outline : none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style:none;
    font-size : 0.9rem;
}
.addContainer {
    float : right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    vertical-align: middle;
}

</style>