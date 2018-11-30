<template>
  <div class="range-slider-wrapper">
    <range-slider
      :class="{ 'range-slider--w-tooltip': tooltip === true }"
      :min="min"
      :max="max"
      :step="step"
      :prefix="prefix"
      :suffix="suffix"
      :tooltip="tooltip"
      :disabled="disabled"
      v-model="internalValue"
      >
    </range-slider>
    <div
      class="range-slider-tooltip"
      :class="{ disabled: disabled === true }"
      v-if="tooltip === true"
      :style="{ left: value + '%' }">
      {{ prefix }}{{ value }}{{ suffix }}
    </div>
  </div>
</template>


<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import RangeSlider from "vue-range-slider";
import "vue-range-slider/dist/vue-range-slider.css";

export default {
  name: "Slider",
  extends: RangeSlider,

  components: {
    RangeSlider
  },

  props: {
    prefix: {
      type: String,
      default: ""
    },
    suffix: {
      type: String,
      default: ""
    },
    tooltip: {
      type: Boolean,
      default: true
    },
    value: {
      type: [String, Number],
      default: null
    }
  },

  watch: {
    internalValue(v: String | Number) {
      this.$emit("input", v);
    }
  },

  computed: {
    // this.internalValue = this.value;
    internalValue(): String | Number {
      if (this.value) {
        return this.value;
      } else {
        return "0";
      }
    }
  }
};
</script>

<style lang="less">
@import "./../styles/Imports";
.range-slider-wrapper {
  position: relative;
}

.range-slider {
  padding: 0;
  height: 16px;
}

.range-slider--w-tooltip {
  margin-bottom: 24px;
}

.range-slider {
  width: 100% !important;

  &.disabled {
    opacity: 0.4 !important;
  }
}

.range-slider-rail,
.range-slider-fill {
  height: 8px !important;
  .radius() !important;
}

.range-slider-rail {
  background-color: @light-3 !important;
}

.range-slider-fill {
  background-color: @teal !important;
}

.range-slider-knob {
  background-color: @dark-2;
  box-shadow: none;
  .radius(3);
  position: relative;
  width: calc(~"3 * " @spacing);
  height: calc(~"2 * " @spacing);
  border: 0;

  &:before,
  &:after {
    border: none;
    font-family: "icomoon";
    font-weight: 900;
    position: absolute;
    top: 0px;
    color: @light-3;
    font-size: 11px;
    line-height: 15px;
    content: "\e996";
    display: inline-block;
  }

  &:before {
    transform: rotate(90deg);
    left: 2px;
  }

  &:after {
    transform: rotate(-90deg);
    right: 2px;
  }
}

.range-slider-tooltip {
  position: absolute;
  bottom: -10px;
  transform: translate(-50%, -50%);
  color: @day-title;

  &.disabled {
    opacity: 0.4 !important;
  }
}

.night,
.night-theme {
  .range-slider-rail {
    background-color: @dark-4 !important;
  }

  .range-slider-knob {
    background-color: @light-1;

    &:before,
    &:after {
      color: @dark-5;
    }
  }

  .range-slider-tooltip {
    color: @night-title;
  }
}
</style>
