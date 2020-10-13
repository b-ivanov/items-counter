<template>
  <button
    v-on:click="onClickButton"
    :disabled="isDisabled === false"
    class="btnCls"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "CustomButton",
  props: {
    text: {
      type: String,
      required: true,
    },
    isDisabled: {
      type: Boolean,
      required: false,
    },
  },
  methods: {
    onClickButton(event) {
      this.$emit("button-clicked", event.target.innerText);
    },
  },
};
</script>

<style>
.btnCls {
  width: 200px;
  height: 20px;
  margin: 5px;
}
</style>
