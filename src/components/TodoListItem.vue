<template>
  <li>
    <input type="checkbox" :checked="todo.selected === true" v-on:change="$emit('onselect', todo.id, $event.target.checked)" />
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
      checked: this.todo.selected,
    };
  },
  methods: {
    change: function(event) {
      debugger;
    }
  },
  watch: {
    todo: function() {
      console.log("checkbox watch todo", this.todo.id);
    },
  },
  updated: function () {
    console.log("checkbox updated", this.todo.id);
  }
}
</script>