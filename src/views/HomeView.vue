
<template>
  <div :class="modalView   ? 'body--active' : ''">

 
  <header class="header">
    <div class="container">
      <nav class="nav">
        <a href="#">
          <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="218px" height="50px" /></a> 
        <button class="btn" @click="modalView = true">
          <svg width="34" height="34" viewBox="0 0 34 34" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M6.3079 4.54487C5.90926 4.92711 5.89596 5.56013 6.2782 5.95877C6.66044 6.35741 7.29347 6.3707 7.6921 5.98846L6.3079 4.54487ZM7.6921 28.0115C7.29347 27.6293 6.66044 27.6426 6.2782 28.0412C5.89596 28.4399 5.90926 29.0729 6.3079 29.4551L7.6921 28.0115ZM1 16C0.447715 16 0 16.4477 0 17C0 17.5523 0.447715 18 1 18V16ZM23 17L23.7071 17.7071C24.0976 17.3166 24.0976 16.6834 23.7071 16.2929L23 17ZM16.2929 22.2929C15.9024 22.6834 15.9024 23.3166 16.2929 23.7071C16.6834 24.0976 17.3166 24.0976 17.7071 23.7071L16.2929 22.2929ZM17.7071 10.2929C17.3166 9.90237 16.6834 9.90237 16.2929 10.2929C15.9024 10.6834 15.9024 11.3166 16.2929 11.7071L17.7071 10.2929ZM32 17C32 25.3158 25.4872 32 17.5227 32V34C26.6539 34 34 26.3573 34 17H32ZM17.5227 2C25.4872 2 32 8.68416 32 17H34C34 7.64273 26.6539 0 17.5227 0V2ZM7.6921 5.98846C10.2781 3.50887 13.7316 2 17.5227 2V0C13.1867 0 9.2448 1.72879 6.3079 4.54487L7.6921 5.98846ZM17.5227 32C13.7316 32 10.2781 30.4911 7.6921 28.0115L6.3079 29.4551C9.2448 32.2712 13.1867 34 17.5227 34V32ZM1 18H23V16H1V18ZM22.2929 16.2929L16.2929 22.2929L17.7071 23.7071L23.7071 17.7071L22.2929 16.2929ZM23.7071 16.2929L17.7071 10.2929L16.2929 11.7071L22.2929 17.7071L23.7071 16.2929Z" fill="white"/>
          </svg>
          Вход
        </button>
      </nav>
    </div>
  </header>
  <main class="main">
    <div class="container main_left-container">
      <div class="main_left">
        <h1 class="title-1">
          Мои заметки
        </h1>
        <p class="main_left-text">Не забывай о важном, храни его в облаке.</p>
      </div>
    </div>

  </main>
  <modal @modalClose="modalClose" @entry="entry" :eror="eror" @modalViewRegisterToggle="modalViewRegisterToggle" title="Вход в ваш аккаунт" textGray="У вас нет аккаунта? "  link="Зарегистрируйтесь" v-if="modalView" btnName="Войти" />
  <modal @modalClose="modalClose" :eror="eror" @registration="registration"  @modalViewRegisterToggle="modalViewRegisterToggle" title="Регистрация" textGray="У вас есть аккаунт? "  link="Войдите" v-if="modalViewRegister" btnName="Зарегистрироваться" >
    <div class="modal_inputs">
      <label for="">Пароль ещё раз</label>
      <input :type="eye == true ? 'text' : 'password'" placeholder="Введите пароль">
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
  </modal>
</div>
</template>
<script setup>
import modal from '@/components/modal.vue';
import axios from 'axios';
import { useRouter } from 'vue-router'

import { ref } from 'vue';
const modalView = ref(false);
const eye = ref(false)
const router = useRouter()
const eror = ref({});
const modalViewRegister = ref(false);
const modalClose = (item) => {
  modalView.value = item
  modalViewRegister.value = item
}
const modalViewRegisterToggle = (item) => {
  modalViewRegister.value = item
}
const url = 'https://dist.nd.ru'
const registration = (email,password,confirm) => {
 const response = axios.post(url + '/api/reg', {
  email: email,
  password: password, 
  confirm_password: confirm
})
.then(function (response) {
    console.log(response, '1');
    eror.value = {
      type:false,
      resp:''
    }
    localStorage.setItem('email',  response.data.email)
    // router.push('/about');
    modalViewRegister.value = false
  })
  .catch(function (error) {
    eror.value = {
      type:true,
      resp:error.response.data.message[0]
    }
    console.log(error.response.data.message[0], '2');

});
}
const entry = (email,password) => {
 const response = axios.post(url + '/api/auth', {
  email: email,
  password: password, 
})
.then(function (response) {
    console.log(response, '1');
    eror.value = {
      type:false,
      resp:''
    }
    localStorage.setItem('email',  email)
    localStorage.setItem('token',  response.data.accessToken)
    router.push('/about');
  })
  .catch(function (error) {
    eror.value = {
      type:true,
      resp:error.response.data.message
    }
    console.log(error.response.data.message[0], '2');

});
}
</script>


<style>
.main {
  position: relative;
  height: 83vh;
  background-image: url("@/assets/bg.png");
  background-repeat: no-repeat;
  background-size: contain;
  background-position: right 100px bottom 10%;
}
.header {
  padding-top: 40px;
  padding-bottom: 40px;
}
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.btn {
  background-color: var(--green-light);
  border-radius: 32px;
  padding: 12px 24px;
  display: flex;
  align-items: center;
  gap: 12px;
  color: var(--white);
  font-size: 20px;
  transition: all .3s;
  font-weight: 500;
}
.btn:hover {
  background-color: var(--green-middle);
}
.btn:active {
  background-color: var(--green-dark);
}
.btn:disabled {
  background-color: var(--gray);
}
.main_left {
    max-width: 394px;
}
.main_left-text {
  font-size: 32px;
  font-weight: 400;
  color: var(--gray);
  margin-top: 40px;
}
.main_left-container {
  height: 100%;
  display: flex;
  align-items: center;
}
.body--active {
  overflow-y: hidden;
  height: 100vh;
}
.body--active::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 101;
  background-color: var(--dark);
  opacity: .7;
}
</style>
