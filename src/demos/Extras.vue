<template>
  <div>
    <div class="section">
      <h1>Extras</h1>
      <p>
        Premade designs you can slot into modals, marketing sections, etc to
        make your lives easier.
      </p>
    </div>
    <div class="section">
      <h2>Fake Alert</h2>
      <pre><code>import { FakeAlert } from 'streamlabs-beaker';

components: {
  FakeAlert
}</code></pre>

      <Accordion :openedTitle="'Hide Code'" :closedTitle="'Show Code'">
        <div slot="content"></div>
      </Accordion>

      <div class="section section__components">
        <FakeAlert :username="'SalmanSux19'"></FakeAlert>
      </div>
    </div>

    <table class="docs-table">
      <thead>
        <tr>
          <th>Prop</th>
          <th>Type</th>
          <th>Default</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>alertText</td>
          <td>string</td>
          <td>'galazy83 donated $50.00'</td>
          <td>First line of text in the alert.</td>
        </tr>
        <tr>
          <td>alertMessage</td>
          <td>string</td>
          <td>'Thanks for the stream. Go CivRyan!'</td>
          <td>Second line of text in the alert.</td>
        </tr>
        <tr>
          <td>alertImage</td>
          <td>string</td>
          <td>'https://thumbs.gfycat.com/PleasedIcyCod-size_restricted.gif'</td>
          <td>Alert graphic.</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

import Accordion from "./../components/Accordion.vue";
import FakeAlert from "./../components/FakeAlert.vue";

@Component({
  components: {
    Accordion,
    FakeAlert
  }
})
export default class Extras extends Vue {}
</script>
