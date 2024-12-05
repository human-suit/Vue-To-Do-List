<template>
  <div class="hello">
    <!-- {{ nameValue }} -->
    <input v-model="nameValue" placeholder="Invate text" type="text" />
    <button @click="addTask">ADD</button>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: Array,
  },
  data() {
    return {
      nameValue: "",
      newTasks: this.modelValue,
    };
  },
  emits: ["update:modelValue"],
  methods: {
    addTask() {
      if (this.nameValue.trim() !== "") {
        this.newTasks.push({
          id: Date.now(),
          text: this.nameValue,
          complete: false,
        });
        this.nameValue = "";
        this.$emit("update:modelValue", this.newTasks);
        this.newTasks = this.modelValue;
        this.$emit("button-clicked", this.newTasks);
      }
    },
    handleInput(event) {
      this.nameValue = event.target.value;
    },
  },
};
</script>

<style scoped>
input {
  padding: 10px 100px 10px 10px;
}
button {
  margin-left: 10px;
  padding: 10px 50px;
  background: darkcyan;
  border: 0px;
  color: white;
  font-weight: 900;
}
button:hover {
  cursor: pointer;
  padding: 12px 52px;
}
</style>
