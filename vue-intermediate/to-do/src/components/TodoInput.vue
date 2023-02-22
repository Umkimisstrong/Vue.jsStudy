<template>
    <!-- TodoInput -->
    <div>
        <input type="text" v-model="newTodoItem">
        <button v-on:click="addTodo">add</button>
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
            this.newTodoItem = '';
        }
   },
}

</script>

<style scoped>

</style>