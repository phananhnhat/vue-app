<template>
  <li>
    <input type="checkbox" :checked="todo.selected === true" v-on:change="$emit('onselect', todo.id, $event.target.checked)" />
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
  updated: function () {
    console.log("checkbox updated", this.todo.id);
  }
}
</script>