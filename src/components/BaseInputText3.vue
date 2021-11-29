/* eslint-disable */
<template>
  <input type="text" class="input" :value="modelValue.textInput" v-on="listeners" />
</template>

<script>
export default {
  props: ['modelValue'],
  computed: {
    listeners() {
      return {
        // Pass all component listeners directly to input
        // eslint-disable-next-line vue/no-deprecated-dollar-listeners-api
        ...this.$listeners,
        // Override input listener to work with v-model
        input: (event) => {
          // this.$emit("update:modelValue", event.target.value);
          this.modelValue.textInput = event.target.value;
        }
      };
    },
  },
  created() {
    console.log(this)
  },
  updated: function () {
    console.log("input props modal obj: updated", this.modelValue);
  },
  watch: {
    modelValue(current, prev) {
      debugger;
    }
  }
};
</script>

<style>

.input {
  width: 100%;
  padding: 8px 10px;
  border: 1px solid #32485F;
}
</style>
