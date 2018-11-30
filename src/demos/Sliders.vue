<template>
  <div>
    <div class="section">
      <h1>Sliders</h1>
      <p>Our slider component is extended from <a target="_blank" href="https://github.com/ktsn/vue-range-slider">Vue Range Slider</a>
      </p>

      <div class="section">
        <h3>With prefix</h3>
        <accordion
          :openedTitle="'Hide Code'"
          :closedTitle="'Show Code'">
          <div slot="content">
            <pre>
<code>&lt;slider
  :min=&quot;0&quot;
  :max=&quot;100&quot;
  :step=&quot;5&quot;
  :value=&quot;50&quot;
  :prefix=&quot;'$'&quot;&gt;
&lt;/slider&gt;</code></pre>
          </div>
        </accordion>

        <slider
          :min="0"
          :max="100"
          :step="5"
          v-model="selectedValue"
          :prefix="'$'">
        </slider>
      </div>

      <!-- <div class="section">
        <h3>With suffix</h3>
        <accordion
          :openedTitle="'Hide Code'"
          :closedTitle="'Show Code'">
          <div slot="content">
            <pre>
<code>&lt;slider
  :min=&quot;0&quot;
  :max=&quot;100&quot;
  :step=&quot;5&quot;
  :value=&quot;50&quot;
  :suffix=&quot;'%'&quot;&gt;
&lt;/slider&gt;</code></pre>
          </div>
        </accordion>
        <slider
          :min="0"
          :max="100"
          :step="5"
          :value="85"
          :suffix="'%'">
        </slider>
      </div>

      <div class="section">
        <h3>No tooltip</h3>
        <accordion
          :openedTitle="'Hide Code'"
          :closedTitle="'Show Code'">
          <div slot="content">
            <pre>
<code>&lt;slider
  :min=&quot;0&quot;
  :max=&quot;100&quot;
  :step=&quot;5&quot;
  :value=&quot;50&quot;
  :tooltip=&quot;false&quot;&gt;
&lt;/slider&gt;</code></pre>
          </div>
        </accordion>
        <slider
          :min="0"
          :max="100"
          :step="1"
          :value="23"
          :tooltip="false">
        </slider>
      </div>

      <div class="section">
        <h3>Disabled</h3>
        <accordion
          :openedTitle="'Hide Code'"
          :closedTitle="'Show Code'">
          <div slot="content">
            <pre>
<code>&lt;slider
  :min=&quot;0&quot;
  :max=&quot;100&quot;
  :step=&quot;5&quot;
  :value=&quot;50&quot;
  :disabled=&quot;true&quot;&gt;
&lt;/slider&gt;</code></pre>
          </div>
        </accordion>
        <slider
          :min="0"
          :max="100"
          :step="1"
          :value="63"
          :disabled="true">
        </slider>
      </div> -->

      <table class="docs-table">
        <thead>
          <tr>
            <th>Props</th>
            <th>Type</th>
            <th>Default</th>
            <th>Description</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>disabled</td>
            <td>Boolean</td>
            <td>false</td>
            <td>Disable the slider from being used.</td>
          </tr>
          <tr>
            <td>max</td>
            <td>Number</td>
            <td>100</td>
            <td>The maximum numerical value that can be selected.</td>
          </tr>
          <tr>
            <td>min</td>
            <td>Number</td>
            <td>0</td>
            <td>The minimum numerical value that can be selected.</td>
          </tr>
          <tr>
            <td>step</td>
            <td>String, Number</td>
            <td>1</td>
            <td>The steps between the values.</td>
          </tr>
          <tr>
            <td>suffix</td>
            <td>String</td>
            <td>px</td>
            <td>Suffix label that will be displayed next to the value in the tooltip.</td>
          </tr>
          <tr>
            <td>tooltip</td>
            <td>Boolean</td>
            <td>true</td>
            <td>Show the tooltip or not</td>
          </tr>
          <tr>
            <td>value</td>
            <td>Number, String</td>
            <td>null</td>
            <td>Initial value of the slider.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import Slider from "./../components/Slider.vue";
import Accordion from "./../components/Accordion.vue";

@Component({
  components: {
    Slider,
    Accordion
  }
})
export default class Sliders extends Vue {
  selectedValue = 50;
}
</script>
