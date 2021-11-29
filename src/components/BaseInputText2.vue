/* eslint-disable */
<template>
  <input type="text" class="input" :value="text" v-on="listeners" />
</template>

<script>
export default {
  inheritAttrs: false, // TODO: Chặn event tự pass vào input.
  props: ['text'],
  computed: {
    listeners() {
      return {
        // Pass all component listeners directly to input
        // eslint-disable-next-line vue/no-deprecated-dollar-listeners-api
        // TODO: Vue 3 đã xóa $listeners, event nó tự ghi đề vào input. Nếu dùng thì có thể thay bằng this.$attrs
        ...this.$listeners,
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
