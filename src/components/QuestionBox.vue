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
          @click="selectAnswer(index, answer)"
          :class="answerClass(index)"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
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
      selectedAnswer: '',
      answered: false,
      correctIndex: null as null | number,
    };
  },
  computed: {
    answers(): string[] {
      const answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      // this.shuffleAnswers(answers);
      return answers;
    }
  },
  methods: {
    answerClass(index: number) {
      let answerClass = ''

      if (!this.answered && this.selectedIndex === index) {
        answerClass = 'selected'
      } else if (this.answered && this.correctIndex === index) {
        answerClass = 'correct'
      } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
        answerClass = 'incorrect'
      }

      return answerClass;
    },
    selectAnswer(index: null & number, answer: string) {
      this.selectedIndex = index;
      this.selectedAnswer = answer;
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
      let isCorrect = false;
      this.correctIndex = this.answers.indexOf(this.currentQuestion.correct_answer);

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }

      this.answered = true;
      this.increment(isCorrect);
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,  // <-- makes the handler method run on the first time.
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers(this.answers);
      }
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
