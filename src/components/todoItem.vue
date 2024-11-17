<template>
    <div class="todo_all">
        <div class="note" v-for="todo in todoList" :key="todo.id">
            <div class="note-top">
              <h4 class="title-4">{{todo.title}}</h4>
              <!-- <img class="note-top-img" src="../assets/todo.png" alt=""> -->
            </div>
            <div class="note-mid">
              <p class="text">{{todo.content}}</p>
            </div>
            <div class="note-bot">
              <button @click="$emit('deleteTodo', todo.id)" class="note-bot-btn">
                <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 1L17 17M17 1L1 17" stroke="white" stroke-width="2" stroke-linecap="round"/>
                </svg>
                Удалить
              </button>
            </div>
          </div>
    </div>
</template>
<script setup>
defineProps({
  todoList:Array
})
defineEmits(['deleteTodo'])
</script>

<style>


.note {
    max-width: 480px;
    position: relative;
    width: 100%;
    height: max-content;
    border-radius: 12px;
    background-color: var(--green-light);
    box-shadow: 0px 15px 15px -10px #00000066;

  }
  .note:before {
    content: '';
    position: absolute;
    top: 0; right: 0;
    border-top: 40px solid var(--dark);
    border-left: 40px solid var(--green-middle) ;
    border-radius:0 0 0px 10px ;
    width: 0;
}
  .note-top {
    padding: 20px 28px;
    padding-right: 0px;
    border-bottom:1px solid var(--green-middle) ;
  }
  .note-mid {
    padding: 20px 28px;
    color: var(--white);
  }
  .note-top-img {
    position: absolute;
    top: 0;
    height: 69px;
    right: 0;
  }
  .note-bot {
    padding: 8px;
    color: var(--white);
    display: flex;
    justify-content: end;
    width: 100%;
    
  }
  .note-bot-btn  {
    display: flex;
    gap: 12px;
    padding: 12px 24px;
    font-size: 20px;
    font-weight: 500;
    align-items: center;
  }
  @media (max-width: 1366px) {
    .note {

        max-width: 374px;
    }
}
  @media (max-width: 768px) {
    .note {

        max-width: 768px;
    }
}
  
</style>