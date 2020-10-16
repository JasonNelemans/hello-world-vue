<template>
  <div class="home">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

import { QuizQuestionsArray } from '@/types';

import Header from '@/components/Header.vue';
import QuestionBox from '@/components/QuestionBox.vue';

export default {
  name: 'home' as string,
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions: [] as QuizQuestionsArray,
      index: 0 as number,
    };
  },
  methods: {
    next() {
      // next: function() {}
      this.index++;
    },
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get',
    })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      });
  },
};
</script>
