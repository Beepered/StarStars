<script setup>
import ChoiceBar from './components/ChoiceBar.vue';
</script>

<template>
  <header>
    <div style="color: rgb(255, 247, 12);">
      <h1>
        Star Stars
      </h1>
    </div>
    <div>
      <p>The Star Wars API getter thing</p>
      <p>API link: <a target="_blank" href="https://www.swapi.tech/" style="font-size: large;">SWAPI</a></p>

    </div>
  </header>

  <main>
    <div class="container">
      <ChoiceBar id="ChoiceBar" @click-event="ChoiceClicked"></ChoiceBar>
    </div>

    <div class="data-holder">
      <p>Name: {{ name }}</p>
      <p>Description: {{ desc }}</p>
      <p>{{ info[0] }}</p>
      <p>{{ info[1] }}</p>
    </div>

    <p style="color: grey; margin-top: 60px;">I don't know what to do with this</p>
  </main>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      desc: "",
      info: ["", ""]
    };
  },
  methods: {
    ChoiceClicked(data) {
      // The 'data' argument receives the payload from the child's $emit
      const parsed = JSON.parse(data);

      switch (parsed.description) {
        case ("A Star Wars Film"):
          this.name = parsed.properties.title;
          this.desc = parsed.description;
          this.info[0] = "Series number: " + parsed.properties.episode_id;
          this.info[1] = "Release date: " + parsed.properties.release_date;
          break;
        case ("A person within the Star Wars universe"):
          this.name = parsed.properties.name;
          this.desc = parsed.description;
          this.info[0] = "Gender: " + parsed.properties.gender;
          this.info[1] = "Height: " + parsed.properties.height;
          break;
        case ("A planet."):
          this.name = parsed.properties.name;
          this.desc = parsed.description;
          this.info[0] = "Climate: " + parsed.properties.climate;
          this.info[1] = "Terrain: " + parsed.properties.terrain;
          break;
        case ("A Starship"):
          this.name = parsed.properties.name;
          this.desc = parsed.description;
          this.info[0] = "Class: " + parsed.properties.starship_class;
          this.info[1] = "Model: " + parsed.properties.model;
          break;
        default:
          this.name = "ERROR";
          this.desc = "ERROR";
          this.info = ["", ""]
      }

    }
  }
}
</script>


<style scoped>
header {
  max-height: 30vh;
  line-height: 1.5;
  background-color: rgb(224, 224, 224);
  padding: 15px;
  position: absolute;
  top: 0;
}

header p {
  margin: 5px;
}

.container {
  width: 100vh;
}

.data-holder {
  min-width: 30vw;
  max-width: 70vw;
  height: auto;
  border: 2px solid grey;
  background-color: rgb(224, 224, 224);
  padding: 12px;
  margin-top: 12px;
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
