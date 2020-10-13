
<template>
  <!-- to enabvle or disable the component call respectively:
    enableComponent and disableComponent-->
  <div v-bind:class="{ disabledClass: !isEnabled }">
    <h1>Items counter</h1>
    <h2>Current items count: {{ itemsCount }}</h2>
    <CustomButton
      v-on:button-clicked="buttonactions"
      :isDisabled="isEnabled"
      :text="removeText"
    />
    <CustomButton
      v-on:button-clicked="buttonactions"
      :isDisabled="isEnabled"
      :text="addText"
    />
    <!-- The best way to call a parent function is to emit an event from
    the child component, which the parent is listening to. However, if we have to pass
    down a function, it should be passed to the child component using props (see down)
    and we should add the Process button like so:
    <button :click="callback">Process</button> -->
    <div class="smallRealCounter">Real counter: {{ counter }}</div>
  </div>
</template>

<script>
import CustomButton from "./CustomButton.vue";

export default {
  name: "App",
  components: {
    CustomButton,
  },
  methods: {
    buttonactions(name) {
      if (name === this.addText) {
        this.incrementItems();
      } else {
        this.decrementItems();
      }
      if (this.counter > 10) {
        this.itemsCount = "10+";
      } else {
        this.itemsCount = this.counter;
      }
    },
    incrementItems() {
      this.counter++;
    },
    decrementItems() {
      this.counter--;
    },
    enableComponent() {
      this.isEnabled = true;
    },
    disableComponent() {
      this.isEnabled = false;
    },
  },
  props: {
    callback: {
      type: Function,
      required: false,
    },
  },
  data: function () {
    return {
      itemsCount: 0,
      counter: 0,
      addText: "Add item",
      removeText: "Remove item",
      isEnabled: true,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
}
.disabledClass {
  background-color: #e4e4e4;
}
.smallRealCounter {
  margin-top: 20px;
  text-align: right;
  font-size: 10px;
}
</style>
