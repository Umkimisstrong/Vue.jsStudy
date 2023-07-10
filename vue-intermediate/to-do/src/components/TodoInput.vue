<template>
    <!-- TodoInput -->
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <button class="addBtn">add</button>
        </span>

          <Modal v-if="showModal" @close="showModal = false" v-on:closeModal="closeModal">
            <!--
             you can use custom content here to overwrite
             default content
            -->
            <h3 slot="header">
                경고!
                <hr>
            </h3>
            
        <!-- <h3 slot="header">custom header</h3> -->

            <h3 slot="body">
                내용을 입력하세요    
            </h3>
      </Modal>
    </div>
</template>

<script>
import Modal from './common/CommonModal.vue'

export default {
    //data : function ()  {
    data ()  {
        return  {
            newTodoItem: ""
            , showModal:false
        }
    },
    methods: {

        addTodo(){
            //console.log(this.newTodoItem);
            // 저장하는 로직
            // 개발자도구의 애플리케이션 - 로컬스토리지에 key / value 로 저장이 된다.

            if(this.newTodoItem !== '')
            {
                // 상위 컴포넌트로 addTodoItem 이라는 이벤트 발생시킨다.
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            } // 값이 안담기면 모달을 띄운다
            else
            {
                this.showModal = !this.showModal;
            }
            
        },
        clearInput() {
            this.newTodoItem = '';
        }
        , closeModal(){
            this.showModal = !this.showModal;
        }

   },
   // 모달 컴포넌트 등록
    components : {
        Modal:Modal
    }

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