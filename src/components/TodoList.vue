<template>
    <section>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{todoItem}}
                <span class="editBtn" Type="button" @click="editTodo(todoItem, index)">
                    <i class="far fa-edit" aria-hidden="true"></i>    
                </span>
                <span class="removeBtn" Type="button" @click="removeTodo(todoItem, index)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>    
                </span>
            </li>
        </transition-group>
        <modal v-if="editModal" @close="editModal = false">
            <span class="header" slot="header" @click="editModal = false">수정
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i></span>
            <span slot="body" class="inputBox">
                <input type="text" v-model="editTodoItem" v-on:keyup.enter="saveTodo(), editModal=false">
                <span class="saveBtn" Type="button" @click="editModal = false, saveTodo()">
                    <i class="far fa-save"></i>
                </span>
            </span>
             
        </modal>
    </section>
</template>

<script>
import Modal from './common/EModal.vue'

export default {
    props: ['propsdata'],
    data(){
        return {
            editTodoItem: '',
            editModal: false
        }        
    },    
    methods:{
        removeTodo(todoItem, index){
            this.$emit('removeTodo', todoItem, index);
        },
        editTodo(todoItem, index){
           this.editModal = !this.editModal;
           this.$emit('editTodo', todoItem, index);
        },
        saveTodo(){
            if(this.editTodoItem !== ""){
                var value = this.editTodoItem && this.editTodoItem.trim();
                this.$emit('saveTodo',value);
                this.clearInput();
            }
        },
        clearInput(){
            this.editTodoItem = '';
        }
    },
    components: {
        Modal: Modal
    }
}
</script>

<style scoped>
    .list-enter-active, .list-leave-active{
        transition: all 1s;
    }
    .list-enter, .list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }
    ul{
        list-style-type:none;
        padding-left:0px;
        margin-top:0;
        text-align: left;
    }
    li{
        display:flex;
        min-height: 50px;
        height:50px;
        line-height:50px;
        margin:0.5rem 0;
        padding: 0 0.9rem;
        background:white;
        border-radius:5px;
    }
    .checkBtn {
        line-height: 45px;
        color:#62acde;
        margin-right:5px;
    }
    .removeBtn{
        margin-left:10px;
        color: #de4343;
    }
    .editBtn{
        margin-left:auto;
        color: #6478FB;
    }
    .closeModalBtn{
        color: #62acde;
        margin-left:10px;
    }
    .saveBtn{
        margin-left:10px;
        line-height: 30px;
        
        color: #6478FB;
    }
  
   
    .inputBox{
       
        font-size:20px;
        line-height:30px;
        height:30px;
        font:30px;
       
    }
    .inputBox input{
        outline:none;
        border-style: none;
       padding-top:5px;  
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
    }
</style>