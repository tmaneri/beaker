<template>
  <div class="section">
    <h1>Galleries</h1>

    <div class="section carousel-section">
      <h2>Carousel</h2>
      <div class="carousel-container">
        <carousel :slides="slides"></carousel>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Accordion from "./../components/Accordion.vue";
import Carousel from "./../components/Carousel.vue";

@Component({
  components: {
    Accordion,
    Carousel
  }
})
export default class Galleries extends Vue {
  slides = [
    "https://picsum.photos/1120/630",
    "https://picsum.photos/1120/630?image=243",
    "https://picsum.photos/1120/630?image=461",
    "https://picsum.photos/1120/630?image=261",
    "https://picsum.photos/1120/630?image=61",
    "https://picsum.photos/1120/630?image=23",
    "https://picsum.photos/1120/630?image=41",
    "https://picsum.photos/1120/630?image=21"
  ];
}
</script>

<style lang="less" scoped>
@import "./../styles/Imports";

.carousel {
  &-section {
    overflow: hidden;
  }

  &-container {
    width: 75%;
    margin: 0 auto;
  }
}
</style>
