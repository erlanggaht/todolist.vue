<script setup>
import todolist from './components/todolist.vue'
import alert from './components/alert.vue';
import { onUpdated, reactive } from 'vue';

const alerts = reactive({ boolean: false })

function setAlert (bool) {
  alerts.boolean = bool
}

onUpdated(()=>{
})
</script>

<template>
  
  <main class="main">
  <section class="section">
    <alert :alerts="alerts" />
    <todolist title="Todo List" :alerts={setAlert}  />
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
  position: relative;
}

@media (max-width: 640px) { 

  .main {
    margin:1rem
  }
  .section {
    width: 100%;
  }
}
</style>
