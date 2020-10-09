<template>
  <div class="home">
    <Header />
    <QuestionBox />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Header from "@/components/Header.vue";
import QuestionBox from "@/components/QuestionBox.vue";

@Component({
  components: {
    Header,
    QuestionBox
  }
})
export default class Home extends Vue {}
</script>
