<script setup>
import ChoiceBar from './components/ChoiceBar.vue';
</script>

<template>
  <header>
    <div style="font-size: 5vw; color: rgb(255, 247, 12);">Star Stars</div>
    The Star Wars API getter thing
    <p>API link: <a href="https://www.swapi.tech/" style="color: green; font-size: large;">SWAPI</a></p>
  </header>

  <main>
    <div class="container">
      <ChoiceBar id="ChoiceBar" @click-event="ChoiceClicked"></ChoiceBar>
    </div>

    <div class="image-holder">
      <p>Name: {{ name }}</p>
      <p>Description: {{ desc }}</p>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      desc: "",
    };
  },
  methods: {
    ChoiceClicked(data) {
      // The 'data' argument receives the payload from the child's $emit
      // this.parentData = data;
      const parsed = JSON.parse(data);
      this.desc = parsed.description;
      this.name = parsed.properties.name;
      console.log(parsed)
    }
  }
}
</script>


<style scoped>
header {
  line-height: 1.5;
  background-color: rgb(224, 224, 224);
}

.container {
  width: 100vh;
}

.image-holder {
  min-width: 40vw;
  max-width: 70vw;
  height: auto;
  border: 2px solid grey;
  background-color: rgb(224, 224, 224);
  align-content: center;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
