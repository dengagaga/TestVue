<template>
   <div class="modal modal_add">
        <h2 class="title-2">Добавление заметки</h2>
        <div class="modal_inputs">
            <label for="">Название заметки</label>
            <input type="text" v-model="title" placeholder="Введите название">
            <span class="span">{{ title.length }}/100</span>
        </div>
        <div class="modal_inputs">
            <label for="">Текст заметки</label>
            <textarea v-model="content" class="textarea" type="text" placeholder="Введите текст"> </textarea>
            <div v-if="erorText.type" class="eror_text">{{erorText.resp[0]}}</div>
            <span class="span">{{ content.length }}/500</span>
        </div>
        <div class="close" @click="$emit('modalClose', false)">
            <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 1L17 17M17 1L1 17" stroke="white" stroke-width="2" stroke-linecap="round"/>
            </svg>
        </div>
       <div class="modal_bottom modal_bottom-add">
            <button @click="$emit('addListTodo', title, content)" class="btn" >Добавить</button>
       </div>
    </div>
</template>
<script setup>
import {ref} from 'vue';
const title = ref('')
const content = ref('')
defineProps({
    erorText: Object
})
defineEmits(['modalClose', 'addListTodo'])
</script>
<style>
.span {
    color: var(--gray);
    font-size: 18px;
    margin-left: auto;
}
.textarea {
    background-color: var(--white);
    border-radius: 36px;
    padding: 22px 28px;
    height: 244px;
    resize:none;
}
.textarea:focus {
    outline: 2px solid var(--green-light);
}
.modal_bottom-add {
    justify-content: end;
}
.eror_text {
    position: absolute;
    bottom: 3px;
    font-size: 18px;
    color: #FF7461;
}
@media (max-width: 1366px) {
    .textarea {

        height: 168px;
    }
}
</style>