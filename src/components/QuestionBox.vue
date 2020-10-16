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
          @click="selectAnswer(index, answer.correct_answer)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null"
      >
        Submit
      </b-button>
      <b-button @click="next" variant="success">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data() {
    return {
      selectedIndex: null,
      selectedAnswer: ''
    };
  },
  computed: {
    answers(): string[] {
      const answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffleAnswers(answers);
      return answers;
    }
  },
  methods: {
    selectAnswer(index: null & number, answer: string) {
      this.selectedIndex = index;
      this.selectedAnswer = answer;
      console.log("Selected answer: ", this.selectedAnswer);
    },
    shuffleAnswers(array: string[]) {
      for (let i = array.length - 1; i >= 0; i--) {
        const j = Math.round(Math.random() * i);
        const temp = array[i];
        array[i] = array[j];
        array[j] = temp;
        return temp;
      }
    },
    submitAnswer() {
      const isCorrect = false;

      // if (this.selectedIndex === this.correctIndex) {
      //   isCorrect = true;
      // }

      this.increment(isCorrect);
    }
  },
  watch: {
    // currentQuestion: {
    //   immediate: true,  <-- makes the handler method run on the first time.
    //   handler() {
    //     this.selectedIndex = null;
    //     this.shuffleAnswers(this.answers);
    //   }
    // }
    currentQuestion() {
      this.selectedIndex = null;
    }
  }
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}

.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: lightblue;
}

.correct {
  background-color: lightgreen;
}

.incorrect {
  background-color: red;
}
</style>
