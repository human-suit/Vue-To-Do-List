<template>
  <div id="app">
    <h1>Список задач</h1>
    <!-- <ul>
      <li v-for="(item, index) in tasks" :key="item.id">
        {{ index + 1 }} - {{ item.text }} - State:
        {{ item.complete ? "True" : "False" }}
      </li>
    </ul>
    <input v-model="newTask" placeholder="Invate text" type="text" />
    <button @click="addTask">ADD</button>
    <br /><br /><br />
    <form @submit.prevent="handleSubmit">
      <input v-model="formInput" type="text" />
      <button type="submit">Send</button>
    </form>
    <p>{{ sumbitMessage }}</p>
    <br />
    <input @input="handleInput" type="text" />
    <p>{{ inputText }}</p> -->

    <TodoItem
      v-model="tasks"
      :nameValue="newTask"
      @button-clicked="handleButtonClick"
    />
    <TodoList
      v-model="tasks"
      :nameValue="newTask"
      @button-clicked="handleButtonClick"
    />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TodoItem from "./components/TodoItem.vue";
export default {
  data() {
    return {
      tasks: [
        { id: 1, text: "like1", complete: false },
        { id: 2, text: "like2", complete: false },
        { id: 3, text: "like3", complete: false },
      ],
      newTask: "",
      inputText: "",
      formInput: "",
      sumbitMessage: "",
    };
  },
  methods: {
    handleButtonClick(receivedTasks) {
      console.log(receivedTasks);
      this.tasks = receivedTasks;
      console.log(this.tasks);
    },
    handleInput(event) {
      this.inputText = event.target.value;
    },
    handleSubmit() {
      this.sumbitMessage = this.formInput;
      this.formInput = "";
    },
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({
          id: this.tasks.length + 1,
          text: this.newTask,
          complete: false,
        });
        this.newTask = "";
      }
    },
  },
  components: {
    TodoList,
    TodoItem,
  },
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  font-size: 18px;
  color: blueviolet;
  margin-bottom: 10px;
}
</style>
