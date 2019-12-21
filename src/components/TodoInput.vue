<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="오늘은 또 무슨일을 할까" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
        <modal v-if="showModal" @close="showModal = false">
            <span class="header" slot="header">이런!</span>
            <span class="body" slot="body" @click="showModal = false">
                할 일을 입력하세요 :)
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    props: ['propsdata'],
    data(){
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo(){
            if(this.newTodoItem !== ""){
                var value = this.newTodoItem && this.newTodoItem.trim();
                // localStorage.setItem(this.newTodoItem, this.newTodoItem);
                this.$emit('addTodo',value);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newTodoItem = '';
        }
    },
    components: {
        Modal : Modal
    }
}
</script>

<style scoped>
    input:focus{
        outline:none;
    }
    .inputBox{
        background:white;
       height: 50px;
       line-height: 50px;
        border-radius:5px;
    }
    .inputBox input{
        border-style: none;
        font-size:0.9rem;
        padding:-1px;
    }
    .addContainer{
        float:right;
        background:linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width:3rem;
        border-radius:0 5px 5px 0;
    }
    .addBtn{
        color:white;
        vertical-align: middle;
    }
    .closeModalBtn{
        color: #62acde;
        margin-left:10px;
    }
    .header{
        
        line-height: 40px;
    }
   .body{
      color: #de4343;
      font-weight:500;
      line-height: 50px;
   }
   
</style>