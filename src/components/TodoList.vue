/* eslint-disable */
<template>
  <div>
    <BaseInputText2
      :text="inputText"
      @change1="changeInputString"
    />
    <BaseInputText1
        :obj="inputObj"
        @change1="changeInputObj"
    />
    <BaseInputText3
        v-model="inputModelObj"
        placeholder="New todo"
    />
    <BaseInputText
        v-model="newTodoText"
        placeholder="New todo"
        @keydown.enter="addTodo"
    />
    <ul v-if="todos.length">
      <TodoListItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @remove="removeTodo"
          @onselect="selectTodo"
      />
    </ul>
    <p v-else>
      Nothing left in the list. Add a new todo in the input above.
    </p>
    <button @click="submit">Submut</button>
  </div>
</template>

<script>
import BaseInputText from './BaseInputText.vue'
import BaseInputText1 from './BaseInputText1.vue'
import BaseInputText2 from './BaseInputText2.vue'
import BaseInputText3 from './BaseInputText3.vue'
import TodoListItem from './TodoListItem.vue'

let nextTodoId = 1

export default {
  components: {
    BaseInputText, TodoListItem, BaseInputText1, BaseInputText2,BaseInputText3
  },
  data() {
    return {
      newTodoText: 'input props modal string',
      todos: [
        {
          id: nextTodoId++,
          text: 'Learn Vue',
          selected: true,
        },
        {
          id: nextTodoId++,
          text: 'Checkbox vào đây thì ko đc đâu',
          selected: false,
        },
        {
          id: nextTodoId++,
          text: 'Fall in love',
          selected: false,
        }
      ],
      inputObj: {
        a: 1, b : 2,c : 3,
        textInput: 'input props obj',
      },
      inputText: 'input props string',
      inputModelObj: {
        a: 1, b : 2,c : 3,
        textInput: 'input props modal obj',
      },
    }
  },
  methods: {
    changeInputObj(text) {
      // this.inputObj.textInput = text + 'a';
      this.inputObj = {
        ...this.inputObj,
        // textInput: text + 'a',
      };
    },

    changeInputString(text) {
      this.inputText = text;
    },

    addTodo() {
      const trimmedText = this.newTodoText.trim()
      if (trimmedText) {
        this.todos.push({
          id: nextTodoId++,
          text: trimmedText,
          selected: false,
        })
        this.newTodoText = ''
      }
    },
    removeTodo(idToRemove) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== idToRemove
      })
    },

    selectTodo(id, value) {
      // if(id === 2) {
      //   console.log('Ko check được');
      //   return;
      // }

      // this.todos = this.todos.filter(todo => {
      //   if (todo.id === id) {
      //     todo.selected = value;
      //   }
      //   return true;
      // })


      // this.todos = this.todos.map(todo => {
      //   if (todo.id === id) {
      //     todo.selected = value;
      //   }
      //   return todo;
      // })

      this.todos.forEach(todo => {
        // if(id === 2 && todo.id =) {
        //   todo.selected = false;
        //   return;
        // }
        if (todo.id === id) {
          if(id === 2) {
            todo.selected = true;
            return;
          }
          todo.selected = value;
        }
      })

      console.log('selectTodo', this.todos);
    },

    submit() {
      console.log(this.todos);
    },

  },
  updated: function () {
    console.log("List updated");
  },
  watch: {
    inputObj: function(p, c) {
    },
    inputText: function(p, c) {
    },
  }
}
</script>