<template>
  <div class="hello">
    <!-- {{ modelValue }} -->
    <ul>
      <li v-for="(item, index) in modelValue" :key="item.id">
        {{ index + 1 }} - <h3 v-if="item.complete" class="prov">{{ item.text }}</h3>
        <h3 v-else>{{ item.text }}</h3> - State:
        {{ item.complete ? "True" : "False" }}
        <button @click="deletTask(item.id)">Delet</button>
        <button @click="readyTask(index)">Ready</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: Array,
  },
  data() {
    return {
      newTasks: this.modelValue,
    };
  },
  emits: ["update:modelValue"],
  methods: {
    deletTask(event) {
      this.newTasks = this.modelValue.filter((item) => item.id !== event);
      this.$emit("update:modelValue", this.newTasks);
      this.$emit("button-clicked", this.newTasks);
      this.newTasks = this.modelValue;
    },
    readyTask(event) {
      // console.log(this.modelValue[event].complete);
      if (this.modelValue[event].complete == false) {
        this.newTasks[event].complete = true;
        this.$emit("update:modelValue", this.newTasks);
        this.newTasks = this.modelValue;
        this.$emit("button-clicked", this.newTasks);
      }
    },
  },
};
</script>

<style scoped>
li {
  padding: 10px;
  border: 1px solid darkcyan;
  color: black;
  font-weight: 900;
}
.prov {
  text-decoration: line-through;
  font-size: 18px;
  color: blueviolet;
  margin-bottom: 10px;
}  
button {
  margin-left: 10px;
  padding: 10px 10px;
  background: darkcyan;
  border: 0px;
  color: white;
  font-weight: 900;
}
button:hover {
  cursor: pointer;
  padding: 12px;
}
</style>
