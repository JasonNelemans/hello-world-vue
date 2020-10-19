<template>
  <div class="about">
    <h1>This is an about page</h1>
    <Header />
  </div>
</template>

<script lang="ts">
import Header from "@/components/Header.vue";

export default {
  name: 'about',
  components: {
    Header
  },
  mounted: function() {
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151'", {
      method: "get"
    })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        console.log('poke data: ', jsonData)
      });
  }
}
</script>
