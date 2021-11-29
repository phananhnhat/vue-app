/* eslint-disable */
<template>
  <input type="text" class="input" v-model="text" v-on="{input: input, 'keydown.enter': testMethods}" v-on:keydown.enter="testMethods" />
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
  inheritAttrs: false,
  props: ['modelValue'],
  data: function () {
    return {
      text: "12",
    };
  },
  computed: {
    listeners() {
      debugger;
      return {
        // Pass all component listeners directly to input
        // eslint-disable-next-line vue/no-deprecated-dollar-listeners-api
        ...this.$attrs,
        // Override input listener to work with v-model
        // TODO keydown.enter thì ko thể dùng cách này, bắt buộc phải bỏ vào trên template luôn
        'keydown.enter': this.testMethods,
        input: this.input,
      };
    },
    attr() {
      return {
        ...this.$attrs,
      }
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
    },
    testMethods: function() {
      debugger;
      alert('test');
    },
    // 'keydown.enter': function () {
    //   alert('enter');
    // }
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
