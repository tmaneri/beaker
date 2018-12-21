<template>
  <div class="carousel">
    <ul class="carousel__list">
      <li
        v-for="slide in truncatedSlides"
        :key="`carouselitem${slide.id}`"
        class="carousel__item"
      >
        <a v-if="slide.link" :href="slide.link" target="_blank">
          <video v-if="videos" muted>
            <source :src="slide.src">
          </video>
          <img v-else :src="slide.src" :alt="slide.alt">
        </a>

        <video v-if="videos && !slide.link" muted>
          <source :src="slide.src">
        </video>
        <img v-if="!slide.link" :src="slide.src" :alt="slide.alt">
      </li>
    </ul>
  </div>
</template>


<script lang="ts">
interface slideGroup {
  id: number;
  src: string;
}

import { Component, Prop, Vue } from "vue-property-decorator";

@Component({})
export default class Carousel extends Vue {
  @Prop({ required: true })
  slides!: (string | { src: string })[];

  @Prop({ default: 5000 })
  interval!: number;

  @Prop({ default: false })
  videos!: boolean;

  formattedSlides = this.formatSlides();
  truncatedSlides = this.formattedSlides.filter(
    (slide: string | { src: string }, idx: number) => idx < 4
  );
  intervalState: number = 0;
  remainingTime: number = 0;
  startTime = new Date();
  timerId = window.setInterval(this.next, this.interval);

  created() {
    if (this.slides.length < 2) {
      throw "There must be at least 2 slides in order for the Carousel component to function.";
    }

    window.onblur = () => {
      this.pauseInterval();
    };

    window.onfocus = () => {
      // this.resumeInterval();
    };
  }

  destroyed() {
    window.onblur = () => {
      this.pauseInterval();
    };

    window.onfocus = () => {
      this.resumeInterval();
    };
  }

  mounted() {
    this.intervalState = 1;
  }

  formatSlides() {
    if (this.slides.length === 2) {
      return [...this.slides, ...this.slides].map(this.mapSlides);
    } else if (this.slides.length === 3) {
      return [...this.slides, this.slides[0]].map(this.mapSlides);
    } else {
      return this.slides.map(this.mapSlides);
    }
  }

  truncateSlides() {
    return this.formattedSlides.filter((slide: object, idx: number) => idx < 4);
  }

  next() {
    if (this.slides.length === 3) {
      const lastId: any = this.formattedSlides.pop();
      const last: slideGroup = Object.assign({}, this.formattedSlides[2]);
      last.id = lastId.id;
      this.formattedSlides = [last].concat(this.formattedSlides);
    } else {
      const last: any = this.formattedSlides.pop();
      this.formattedSlides = [last].concat(this.formattedSlides);
    }

    this.truncatedSlides = this.truncateSlides();
  }

  pauseInterval() {
    if (this.intervalState != 1) return;

    this.remainingTime =
      this.interval - (Number(new Date()) - Number(this.startTime));
    window.clearInterval(this.timerId);
    this.intervalState = 2;
  }

  resumeInterval() {
    if (this.intervalState != 2) return;

    this.intervalState = 3;
    window.setTimeout(this.timeoutCallback, this.remainingTime);
  }

  timeoutCallback() {
    if (this.intervalState != 3) return;

    this.next();

    this.startTime = new Date();
    this.timerId = window.setInterval(this.next, this.interval);
    this.intervalState = 1;
  }

  mapSlides(slide: string | { src: string }, idx: number) {
    if (typeof slide === "object") {
      return Object.assign({ id: idx + 1 }, slide);
    }

    return {
      id: idx + 1,
      src: slide
    };
  }

  getLastSlide(slide: slideGroup, idx: number, arr: slideGroup[]): boolean {
    return idx === arr.length - 1;
  }
}
</script>


<style lang="less" scoped>
@import "./../styles/Imports";

.carousel {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  position: relative;

  &__list {
    position: relative;
    top: 0;
    list-style-type: none;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    padding-top: 56.25%;
    border-radius: 8px;
    background-color: transparent;
  }

  &__item {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    transform: translateX(-50%) scale(0.9);
    border-radius: 8px;
    background-color: transparent;
    background-blend-mode: lighten;
    opacity: 0.5;
    overflow: hidden;
    transition: transform 1.25s cubic-bezier(0.4, 0, 0.2, 1),
      opacity 0.75s ease-in-out, filter 1.25s cubic-bezier(0.4, 0, 0.2, 1),
      left 1.25s cubic-bezier(0.4, 0, 0.2, 1);

    img,
    video {
      position: relative;
      display: block;
      width: 100%;
      height: 100%;

      &:before {
        content: "\e923" " " attr(alt);
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-family: "icomoon", "Roboto";
        font-size: 16px;
        font-weight: 500;
        background-color: @white;
      }
    }

    &:nth-child(1) {
      left: ~"calc(-45% - 32px)";
      filter: grayscale(100%);
      opacity: 0;
      animation: fade-in-half 0.275s ease-in-out 1s forwards;
    }

    &:nth-child(2) {
      left: 50%;
      opacity: 1;
      transform: translateX(-50%) scale(1);
    }

    &:nth-child(3) {
      left: ~"calc(145% + 32px)";
      filter: grayscale(100%);
    }

    &:nth-child(4) {
      left: 240%;
      filter: grayscale(100%);
      opacity: 0;
    }
  }
}

@keyframes fade-in-half {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 0.5;
  }
}

.night {
  .carousel {
    &__list {
      background-color: @dark-3;
    }
  }
}
</style>
