<template>
  <div class="wrapper">
    <form @submit.prevent="submitAnswer" v-if="!showScore">
      <div class="question">
        <div class="q"> {{questionCount}}) {{selectQuestion.question}}</div>
        <div class="option" v-for="(item , i ) in selectQuestion.answers">
          <input type="radio" :id="`option${i}`" name="answers" v-model="selectedOption" :value="item" />
          <label :for="`option${i}`">{{item}}</label>
        </div>
      </div>
      <button type="submit">submit</button>
    </form>
    <div class="score" v-else>
      <p>Score is :  {{ score }} out of {{ questions.length }}</p>

    </div>
  </div>
</template>


<script lang="ts">
import { ref, defineComponent } from "vue";
export default defineComponent({
  name: "QuizCard",
  setup() {
    const questions = ref([
      {
        question: "What is 1 + 1 ?",
        answers: ["2", "3", "4", "8"],
        correctAnswer: "2",
      },
      {
        question: "What is 1 + 3 ?",
        answers: ["2", "3", "4", "8"],
        correctAnswer: "4",
      },
      {
        question: "What is 3 + 5 ?",
        answers: ["2", "3", "4", "8"],
        correctAnswer: "8",
      },
      {
        question: "What is 4 + 5 ?",
        answers: ["2", "3", "4", "9"],
        correctAnswer: "9",
      },
      {
        question: "What is 4 + 10 ?",
        answers: ["2", "8", "13", "14"],
        correctAnswer: "14",
      },
    ]);

    const score = ref(0);
    const questionCount = ref(1)
    const selectedOption = ref('')
    const showScore = ref(false)
    const selectQuestion = ref(questions.value[0]);
    const submitAnswer =()=>{
      
      if(selectQuestion.value.correctAnswer== selectedOption.value){
        score.value++;
      }
      if(questionCount.value < questions.value.length){
        selectQuestion.value = questions.value[questionCount.value]
        questionCount.value++;
        selectedOption.value = ''; 

      }
      else{
        showScore.value = true
      }

    }
    return {
      questions,
      score,
      selectQuestion,
      selectedOption,
      submitAnswer,
      questionCount,
      showScore,
      
    };
  },
 
});
</script>

<style scoped>
.wrapper {
  height: 300px;
  width: 400px;
  background-color: white;
  border-radius: 10px;
  padding: 1rem; /* added padding for better form layout */
}

form {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Ensures the submit button is at the bottom */
}

.question {
  flex: 1;
}

form > button {
  background-color: blue;
  border: none;
  padding: 1rem;
  color: #fff;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  border-radius: 5px;
  cursor: pointer; /* optional for better appearance */
}
.q {
  height: 40px;
}
.option{
  padding: 0.5em 0;
}
.score {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
