<template>
    <div class="modal">
        <h2 class="title-2">{{title}}</h2>
        <div class="modal_inputs">
            <label for="">Email</label>
            <input type="text" v-model="email" placeholder="Введите значение">
        </div>
        <div class="modal_inputs">
            <label for="">Пароль</label>
            <input :type="eye == true ? 'text' : 'password'" v-model="password" placeholder="Введите пароль">
            
            <svg @click="eye = !eye" v-if="eye" class="eye" width="18" height="14" viewBox="0 0 18 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M17 7C17 8.15478 16.2206 9.64926 14.7228 10.9006C13.2537 12.128 11.2258 13 9 13C6.77424 13 4.7463 12.128 3.27718 10.9006C1.77936 9.64926 1 8.15478 1 7C1 5.84522 1.77936 4.35074 3.27718 3.09941C4.7463 1.87204 6.77424 1 9 1C11.2258 1 13.2537 1.87204 14.7228 3.09941C16.2206 4.35074 17 5.84522 17 7Z" stroke="#B1C909" stroke-width="2"/>
                <circle cx="9" cy="7" r="3" stroke="#B1C909" stroke-width="2"/>
            </svg>
          
            <svg @click="eye = !eye" v-else  class="eye" width="18" height="15" viewBox="0 0 18 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M17 8C17 9.15478 16.2206 10.6493 14.7228 11.9006C13.2537 13.128 11.2258 14 9 14C6.77424 14 4.7463 13.128 3.27718 11.9006C1.77936 10.6493 1 9.15478 1 8C1 6.84522 1.77936 5.35074 3.27718 4.09941C4.7463 2.87204 6.77424 2 9 2C11.2258 2 13.2537 2.87204 14.7228 4.09941C16.2206 5.35074 17 6.84522 17 8Z" stroke="#B1C909" stroke-width="2"/>
                <circle cx="9" cy="8" r="3" stroke="#B1C909" stroke-width="2"/>
                <path d="M2 1L16 15" stroke="#B1C909" stroke-width="2"/>
            </svg>
        </div>
        <slot>
        </slot>
        <div class="close" @click="$emit('modalClose', false)">
            <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 1L17 17M17 1L1 17" stroke="white" stroke-width="2" stroke-linecap="round"/>
            </svg>
        </div>
       <div class="modal_bottom">
            <p class="text_grey">{{ textGray }} <a href="#" @click="textGray == 'У вас есть аккаунт? ' ? $emit('modalViewRegisterToggle', false) : $emit('modalViewRegisterToggle', true)" class="link">{{link}}</a></p>
            <RouterLink class="btn btn-2" @click="btnName == 'Войти' ? $emit('entry', email,password) : $emit('registration', email,password,password)" to="/">{{btnName}}</RouterLink>
       </div>
       <div class="eror" v-if="eror.type">
            <p>{{eror.resp}}</p>
       </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
defineProps({
    btnName: String,
    title: String,
    textGray: String,
    link: String,
    eror: Object,
})
defineEmits(['modalClose','modalViewRegisterToggle', 'registration', 'entry'])
const email = ref('')
const password = ref('')
const eye = ref(false)
</script>


<style>
.modal {
    background-color: var(--dark-middle);
    border-radius: 40px;
    padding: 80px;
    position: absolute;
    top: 50%;
    max-width: 780px;
    width: 100%;
    z-index: 103;
    left: 50%;
    transform: translate(-50%, -50%);
}
.modal h2{
    color: white;
    margin-bottom: 40px;
}
.modal_inputs {
    display: flex;
    flex-direction: column;
    gap: 8px;
    position: relative;
    margin-bottom: 24px;
}

.modal_inputs label{
    color: var(--gray);
    font-size: 18px;
    padding-left: 24px;
   
}
.modal_inputs input{
    background-color: var(--white);
    border-radius: 36px;
    padding: 22px 28px;
}
.modal_inputs input:focus {
    outline: 2px  solid var(--green-light);
}
.modal_bottom {
    margin-top: 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.close {
    position: absolute;
    padding: 20px;
    background-color: var(--green-light);
    border-radius: 32px;
    max-width: 56px;
    top: 20px;
    right: 20px;
    height: 56px;
    transform: all .3s;
    cursor: pointer;
}
.close:hover {
  background-color: var(--green-middle);
}
.close:active {
  background-color: var(--green-dark);
}
.close:disabled {
  background-color: var(--gray);
}
.text_grey {
    color: var(--gray);
    font-size: 18px;
}
.link {
    font-weight: 700;
    color: var(--green-light);
    transition: all .3s;
}
.link:hover {
    color: var(--white);
}
.eror {
    color: #FF7461;
    border-radius: 24px;
    font-size: 18px;
    margin-top: 20px;
    padding: 8px 20px;
    background-color: #FF74611A;
}
.eye   {
    position: absolute;
    right: 28px;
    top: 55px;
    cursor: pointer;
}
@media (max-width: 1366px) {
    .modal {
        max-width: 594px;
        padding: 56px;
      }
    .modal h2 {
        line-height: 72px;
    }
}
@media (max-width: 768px) {
    .modal {
        max-width: 688px;
    }
}
</style>