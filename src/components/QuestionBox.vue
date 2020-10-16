<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />
      
      <b-list-group>
        <b-list-group-item 
          v-for="(answer, index) in answers" 
          :key="index"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    currentQuestion: Object,
    next: Function,
  },
  computed: {
    answers(): string[] {
      const answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      return answers;
    }
  },
  mounted() {
    console.log(this.currentQuestion);
    console.log(this.answers);
  },
};
</script>


<style scoped>
  .list-group {
    margin-bottom: 15px;
  }
  .btn {
    margin: 0 5px;
  }
</style>