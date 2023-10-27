<script setup lang="ts">
import {ref} from "vue";
import deleteTask from '/public/delete.svg'

interface TaskInterface {
  title: string,
  id: number,
  completed: boolean
}

const todos = ref([
  {
    title: 'Task1',
    id: 1,
    completed: false
  },
  {
    title: 'Task2',
    id: 2,
    completed: false
  },
  {
    title: 'Task3',
    id: 3,
    completed: false
  }
]);
const text = ref('');

function checkedSet(todo: boolean) {
  if(todo) {
    todo = true;
  }

  todo = false;
}

function deleteTaskCompleted(id: number) {
  todos.value = todos.value.filter((task: TaskInterface) => task.id !== id)
}

function addTask(task: TaskInterface) {
  todos.value.push(task);
}

</script>

<template>
  <div class="greetings">
    <input v-model="text" type="text">
    <button @click="addTask({
        title: text,
        id: todos.length + 1,
        completed: false
      })">Создать задачу</button>

    <div class="todos">
      <div class="todo" v-bind:class="{active: todo.completed}" v-for="todo in todos">
        <input v-bind:class="{complete: todo.completed}" v-model="todo.completed" type="checkbox" @change="checkedSet(todo.completed)"/>
        {{ todo.title }}
        <img class="delete" v-bind:src="deleteTask" @click="deleteTaskCompleted(todo.id)" alt="">
      </div>
    </div>
  </div>
</template>

<style scoped>

.todo {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.delete {
  width: 18px;
  margin-left: auto;
}

.active {
  color: #7a7a7a;
  text-decoration: line-through;
}

.complete {
  display: none;
}

</style>