<!--:checked="todo.selected === true"-->

<template>
  <li>
    <input type="checkbox" v-model="model1" :checked="todo.selected === true" value="test" v-on:change="change" />
<!--    <input type="checkbox" v-modal="checked" />-->
    {{ todo.text }}
    <button @click="$emit('remove', todo.id)">
      X
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data: function () {
    return {
      // TODO checked thì ko cần thiết, vì đã dùng sang v-model rồi, dùng checked thì sẽ phải quản lý cả việc render lại của Vue, ko nên dùng
      checked: this.todo.selected,
      model1: this.todo.selected ? ['test'] : [],
    };
  },
  methods: {
    change: function(event) {
      // TODO: Cảm thấy cách này vẫn bị rồi => Cần tìm ra cách đơn giản hơn.
      console.log(this.model1);
      if(this.todo.id === 2) {
        this.model1 = [];
        return;
      }
      $emit('onselect', todo.id, $event.target.checked)
    }
  },
  watch: {
    todo: function() {
      console.log("checkbox watch todo", this.todo.id);
    },
    model1: function(newV, oldV) {
      // console.log('model1: ', newV, oldV);
    },
  },
  updated: function () {
    console.log("checkbox updated", this.todo.id);
  }
}
</script>