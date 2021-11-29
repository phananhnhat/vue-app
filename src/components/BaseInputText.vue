/* eslint-disable */
<template>
  <input type="text" class="input" v-model="text" v-on="listeners" />
  <p>{{ text }}</p>
</template>

// TODO: Cách sai 1.
<!--<template>-->
<!--  <input type="text" class="input" v-bind:value="text" v-on="input1" />-->
<!--  <p>{{ text }}</p>-->
<!--</template>-->

// TODO: Cách sai 2
<!--<template>-->
<!--  <input type="text" class="input" v-bind:value="modelValue" v-on="input2" />-->
<!--  <p>{{ text }}</p>-->
<!--</template>-->

<script>
export default {
  props: ['modelValue'],
  data: function () {
    return {
      text: "12",
    };
  },
  computed: {
    listeners() {
      return {
        // Pass all component listeners directly to input
        // eslint-disable-next-line vue/no-deprecated-dollar-listeners-api
        ...this.$listeners,
        // Override input listener to work with v-model
        input: this.input,
      };
    },
  },
  methods: {
    // TODO: Tạo ra 1 data mới dành cho input. Đây là cách làm chuẩn nhất
    input: function (event) {
      if (event.target.value.length > 10) {
        this.text = this.modelValue;
        return;
      }
      this.$emit("update:modelValue", this.text)
    },
    // TODO: Cách làm sai. Thừa, dùng v-modal="text" luôn cho tiện.
    input1: function (event) {
      this.text = event.target.value;
      if (event.target.value.length > 10) {
        this.text = this.modelValue;
        return;
      }
      this.$emit("update:modelValue", event.target.value)
    },
    // TODO: Cách làm sai. Do cần sử dụng thêm watch => phức tạp
    input2: function (event) {
      this.$emit("update:modelValue", event.target.value);
    }
  },
  watch: {
    // TODO: Cách làm sai, gán trực tiếp modalValue vào cho tag input, vì có 1 thời điểm dữ liệu bị sai, ko như mong muốn
    // TODO: Ngoài ra, dùng watch cũng khiến code phức tạp hơn
    // modelValue: function (curren, prev) {
    //   if(curren.length > 10) {
    //     this.$emit("update:modelValue", prev)
    //   }
    // }
  },
  created() {
    console.log(this)
  },
  updated: function () {
    console.log("input updated", this.modelValue);
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
