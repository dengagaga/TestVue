<template>
  <div :class="modalView   ? 'body--active' : ''">
   <header class="header">
    <div class="container">
      <nav class="nav">
        <RouterLink to="/about">
          <img alt="Vue logo" class="logo logo1" src="@/assets/logo.svg" width="218px" height="50px" />
          <img alt="Vue logo" class="logo logo2" src="@/assets/logo2.png" width="218px" height="50px" />
        </RouterLink> 
        <div class="person" >
          <p>{{ lc ? lc : 'e-mail@mail.mail'}} </p>
          <a href="#" @click="exit = !exit"  class="person_icon">
            <svg width="22" height="28" viewBox="0 0 22 28" fill="none" xmlns="http://www.w3.org/2000/svg">
              <circle cx="11" cy="6" r="5" stroke="white" stroke-width="2"/>
              <path d="M21 28V20C21 17.7909 19.2091 16 17 16H5C2.79086 16 1 17.7909 1 20V28" stroke="white" stroke-width="2"/>
            </svg>
          </a>
          <div v-if="exit" class="modal_exit"><RouterLink class="modal_exit-link" @click="exitTodo" to="/">Выйти</RouterLink></div>
        </div>
      </nav>
    </div>
  </header>
  <main>
    <div class="container">
      <div>
        <todoItem @deleteTodo="deleteTodo" :todoList="todoList"/>
      </div>
    </div>
  </main>
  <button class="btn btn_abs" @click="modalView = !modalView">
      <svg width="22px" height="22px" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M1 9H17M9 1L9 17" stroke="white" stroke-width="2" stroke-linecap="round"/>
      </svg>
  </button>
  <modalAddItem :erorText="erorText" @addListTodo="addListTodo" v-if="modalView" @modalClose="modalClose"></modalAddItem>
</div>
</template>
<script setup>
import { onMounted, ref, watch } from 'vue';
import modalAddItem from '@/components/modalAddItem.vue';
import todoItem from '../components/todoItem.vue';
import axios from 'axios';
  onMounted(() => {
    const response = axios.get(url + '/api/notes', { headers: { Authorization: 'Bearer ' + lcToken } })
      .then(function (response) {
        console.log(response);
        todoList.value = response.data
        
        })
        .catch(function (error) {
        console.log(error);
      });
  })
  // watch(
  //     () => response.data,
  //     (state) => {
  //       todoList.value.push(state)
  //     },
  //     { deep: true }
  //  )
  const todoList = ref([]);
  const lc = localStorage.getItem('email')
  const lcToken = localStorage.getItem('token')
  const url = 'https://dist.nd.ru'
  const erorText = ref({
    type: false,
    resp: ''})
  const exit = ref(false);
  const modalView = ref(false);
  const modalClose = (item) => {

  modalView.value = item
}
const addListTodo = (title, content) => {
  
  const response = axios.post(url + '/api/notes', {  title: title,
  content: content, }, { headers: { Authorization: 'Bearer ' + lcToken } })
    .then(function (response) {
      console.log(response);
      modalView.value =false
      erorText.value = {
          type:false,
          resp:''
        }
      const response2 = axios.get(url + '/api/notes', { headers: { Authorization: 'Bearer ' + lcToken } })
      .then(function (response) {
        console.log(response);
        todoList.value = response.data
        
        })
        .catch(function (error) {
        console.log(error);
      });
      })
      .catch(function (error) {
        erorText.value = {
          type:true,
          resp:error.response.data.message
        }
      console.log(error);
    });
    
}
const exitTodo = () => {
    const response = axios.delete(url + '/api/auth', { headers: { Authorization: 'Bearer ' + lcToken } })
    .then(function (response) {
      console.log(response);
      })
      .catch(function (error) {
      console.log(error);
    });
    localStorage.removeItem('email')
    localStorage.removeItem('token')
}
const deleteTodo = (id) => {
  const response = axios.delete(url + `/api/notes/${id}`, { headers: { Authorization: 'Bearer ' + lcToken } })
    .then(function (response) {
      const response2 = axios.get(url + '/api/notes', { headers: { Authorization: 'Bearer ' + lcToken } })
      .then(function (response) {
        console.log(response);
        todoList.value = response.data
        
        })
        .catch(function (error) {
        console.log(error);
      });
      })
      .catch(function (error) {
      console.log(error);
    });
}





</script>
<style>
.person {
  position: relative;
  display: flex;
  gap: 12px;
  align-items: center;
  color: var(--white);
  font-size: 18px;
}
.logo2 {
  display: none;
}
.person_icon {
  background-color: var(--dark-middle);
  padding: 14px 18px;
  width: 56px;
  height: 56px;
  border-radius: 50%;
}
.btn_abs {
  box-shadow: 0px 15px 46px -10px #00000099;

  height: 56px;
  width: 56px;
  position: fixed;
  bottom: 40px;
  right: 40px;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
.btn_abs svg {
  width: 16px!important;
}
.modal_exit {
  position: absolute;
  top: 75px;
  right: 0;
  z-index: 2;
  padding: 40px;
  border-radius: 12px;
  background-color: var(--dark-middle);
  box-shadow: 0px 15px 46px -10px #00000099;

}
.modal_exit::after {
  content: '';
  position: absolute;
  top: -9px;
  right: 15px;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 9px solid transparent;
  border-right: 9px solid transparent;
  border-bottom: 9px solid var(--dark-middle);
}
.modal_exit-link {
  color: var(--green-light);
  color:18px;
  font-weight: 700;
}
.todo_all {
  display: flex;
  gap: 40px;
  flex-wrap: wrap;
}
</style>
