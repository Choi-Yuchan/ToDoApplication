<template lang="">
    <div>
        <div class="inputBox shadow">
            <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
            <span class="addContainer" @click="addTodo" >
                <i class="fa-solid fa-plus addBtn"></i>
            </span>
        </div>
        <ModalVue v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                Warning!
                <button class="modal-default-button" @click="showModal = false">
                    <i class="closeModalBtn fa-solid fa-x"></i>
                </button>
            </h3>

            <div slot="body">You should write anything!</div>
            <p slot="footer">©Logan</p>
        </ModalVue>
    </div>
</template>

<script>
import ModalVue from './common/Modal.vue';

export default {
    data(){
        return{
            newTodoItem: "",
            showModal: false  
        }
    },
    methods:{
        clearInput(){
            this.newTodoItem = '';
        },
        addTodo(){
            if(this.newTodoItem !== ''){
                const text = this.newTodoItem.trim(); 
                this.$store.commit('addAnItem', text);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },

    },
    components: {
        ModalVue
    }
}
</script>

<style scoped>
    input:focus{
        outline: none;
    }
    .inputBox{
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input{
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer{
        float: right;
        background: linear-gradient(to right, #6478fb, #8763fb);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
    }
    .closeModalBtn {
        color: #42b983;
    }
</style>