<template>
  <div class="home">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Header from '@/components/Header.vue';
import QuestionBox from '@/components/QuestionBox.vue';

@Component({
  components: {
    Header,
    QuestionBox,
  },
})
export default class Home extends Vue {}
</script>
