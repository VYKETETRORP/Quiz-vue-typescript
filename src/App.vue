<template>
<div class="container">

  <QuizCard />

</div>
</template>






<script lang="ts">
import { ref } from 'vue'
import { defineComponent } from 'vue';
import QuizCard from "./components/QuizCard.vue";

export default defineComponent({
  name: 'App',
  components :{
    QuizCard,
  },

  setup () {
    const questions = ref([
      {}
    ])
  }
});
</script>




<style scoped>
.container {
background: #bdc3c7;
background: -webkit-linear-gradient(to right, #2c3e50, #bdc3c7);  
background: linear-gradient(to right, #2c3e50, #bdc3c7);
height: 100vh; 
display: flex;
align-items: center;
justify-content: center;

 }
</style>
