/* eslint-disable */
<template>
  <input type="text" class="input" :value="text" v-on="listeners" />
</template>

<script>
export default {
  props: ['text'],
  computed: {
    listeners() {
      return {
        // Pass all component listeners directly to input
        // eslint-disable-next-line vue/no-deprecated-dollar-listeners-api
        ...this.$listeners,
        // Override input listener to work with v-model
        input: (event) => {
          this.$emit("change1", event.target.value);
        },
      };
    },
  },
  created() {
    console.log(this)
  },
  updated: function () {
    console.log("input props string: updated", this.text);
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
