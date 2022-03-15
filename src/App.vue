<script>
export default {
  data () {
     return {
          isEditing: false,
          todo: "",
          todos: [],
          selectedTodo: null,
          }
        },

        methods: {
          storeTodo() {
            this.todos.push(this.todo);
            this.todo = "";
          },
          removeTodo(index) {
            this.todos.splice(index, 1);
          },

          updateTodo() {
            this.todos.splice(this.selectedIndex, 1, this.todo);
            this.todo = "";
            this.isEditing = false;
          },

          editTodo(index, todo) {
            this.isEditing = true;
            this.todo = todo;
            this.selectedIndex = index;
          },
        },
  }    
</script>

<template>
  <div id="app" class="container">
    <h1>Adisty's Todo List</h1>

    <div v-if="!isEditing">
      <input
        type="text"
        v-model="todo"
        style="border: 1px solid#C0C0C0; background-color: #fff"
      />
      <input
        type="submit"
        value="Save"
        style="background-color: #89b088; border: 0"
        @click="storeTodo"
      />
    </div>
    <div v-else>
      <input type="text" v-model="todo" style="background-color: #89b088" />
      <input type="submit" value="Update" @click="updateTodo" />
    </div>

    <ol>
       <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
        <button
          @click="editTodo(index, todo)"
          style="background-color: #89b088; border: 0"
        >
          Edit
        </button>
        <button
          @click="removeTodo(index)"
          style="background-color: #89b088; border: 0"
        >
          Delete
        </button>
      </li>
    </ol>
  </div>
</template>

<style>
.container {
  max-width: 960px;
  margin: 0 auto;
}
h1 {
  padding-top: 40px;
  font-size: 35px;
}
</style>
