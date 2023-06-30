<script setup>
import todolist from './components/todolist.vue'

</script>

<template>
  
  <main class="main">
  <section class="section">
    <todolist title="Todo List" />
  </section>
  </main>

</template>

<style scoped>

.main {
  margin: 0 0;
  padding: 0 ;
  display: flex;align-items: center;
  min-height: 95vh;
}

.section {
  padding: 10px 0px 0px 0px;
  width: 680px;
  margin:1rem auto 1rem auto;
  background-color: #222;color: #eee;
  box-shadow: 0px 2px 12px 1px #111;
  border-radius: 3rem;

}

@media (max-width: 640px) { 
  .section {
    width: 100%;
  }
}
</style>
