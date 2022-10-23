<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo"><!--v-model 텍스트 값 인식할 수있게 씀 -->
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
        </span><!--v-on:click 특정동작을 수행할 수있게 씀/ 여기선 로컬스토리지에 저장 -->
    </div>
    <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @close="showModal = false">
        <template #header>
            <h3>경고</h3>
            <span id="footer" @click="showModal = false">
                할일을 입력하세요.
                <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
            </span>
        </template>
    </modal>
  </Teleport>
</template>

<script>
import Modal from '../components/common/PopModal.vue'

    export default {
        data(){
            return {
                newTodoItem:'',
                showModal: false
            }
        },
        methods: {
            addTodo(){
                if(this.newTodoItem !== ""){
                    let value = this.newTodoItem && this.newTodoItem.trim();
                    this.$emit('addTodo', value)
                    this.clearInput();
                } else {
                    this.showModal = !this.showModal
                }
            },
            clearInput(){
                this.newTodoItem = '';
            }
        },
        components: {
            Modal: Modal
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
        display: inline-block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn{
        color: #fff;
        vertical-align: middle;
    }
</style>