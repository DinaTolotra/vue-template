<script setup>
import { ref } from "vue";
import Task from "@/models/Task";

const items = ref([]);
const label = ref("");
var last_id = 0;

function add_item() {
  if (label.value == "") return;
  let item = new Task(label.value);
  item.id = last_id++;
  items.value.push(item);

  reset();
}

function reset() {
  label.value = "";
}
</script>

<template>
  <div>
    <input type="text" placeholder="Task..." v-model="label" />
    <input type="button" value="Add" @click="add_item" />
  </div>

  <ul>
    <li v-for="item in items" :key="item.key">
      <input type="checkbox" v-model="item.complet" />
      <p>{{ item.label }}</p>
    </li>
  </ul>
</template>

<style scoped>
ul {
  padding-top: 20px;
  padding-left: 20px;
}

li {
  display: flex;
  gap: 12px;
}

input:checked + p {
  text-decoration: line-through;
}
</style>
