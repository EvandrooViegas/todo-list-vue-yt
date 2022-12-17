<script setup>
import { ref } from "vue"

const tasks = ref([])

const text = ref("")
const isDone = ref(false)
const category = ref("work")


const addTask = () => {
  if (!text.value) return
  const newTask = {
    text: text.value,
    id: Math.random(), 
    isDone: isDone.value,
    category: category.value
  }
  console.log(category.value)
  text.value = ""
  tasks.value.push(newTask)
}

const removeTask = (id) => {
  const filtredList = tasks.value.filter(task => task.id !== id)
  tasks.value = filtredList
}

const updateTask = (id) => {
  const newTaskText = prompt("New Text Value: ")
  tasks.value.map(task => {
    if(task.id === id) {
      task.text = newTaskText
    } 
    return task 
  })
}

</script>

<template>
  <div class="app">
    <div class="red">

      <form @submit.prevent="addTask()" class="form-container">
        <div class="input-container">
          <input 
            type="text"
            v-model="text"
            class="input-text"
          />
          <input 
          type="checkbox"
          v-model="isDone"
          class="input-checkbox"
          />
        </div>
     
        <div class="select-container">
          <select @change="(e) => category = e.target.value">
            <option value="work">Work</option>
            <option value="school">School</option>
          </select>
        </div>
        <button class="btn add">Add Task</button>
      </form>
    </div>

    <div class="tasks-container">
      <div v-for="task in tasks" >
        <div class="task-container">
          <p class="task-text">{{ task.text }}</p>

          <div class="actions-container">
            <button @click="updateTask(task.id)" class="btn update">Update</button>
            <button @click="removeTask(task.id)" class="btn delete">X</button>
          </div>
        </div>
        <div class="category-container">
          <select :value="task.category">
            <option value="work">Work</option>
            <option value="school">School</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  padding: 80px;
  height: 80vh;
  display: grid;
  grid-template-rows: 1fr 3fr;
  max-width: 700px;
  margin: auto;
}

.btn {
  padding: 9px;
  border-radius: 4px;
}

.btn.delete {
  background-color: black;
  color: white;
}

.btn.update {
  background-color: white;
  border: 1px solid black;
}

.category-container {
  background-color: #EEE;
  width: fit-content;
  padding: 8px 10px;
  border-radius: 10px;
}
.category-container select {
  background-color: transparent;
}
.tasks-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
}


.task-container {
  display: flex; 
  justify-content: space-between;
  align-items: center;
} 

.actions-container {
  display: flex;
  gap: 10px;
}
.form-container {
  padding: 20px;
}

.input-container {
    display: flex;
    justify-content: space-between;
}

.input-container .input-text {
  width: 100%;
  border-radius: 4px;
  padding: 10px;
  border: 1px solid #ddd;
}

.input-container .input-checkbox {
    accent-color: #ccc;
    width: 15%;
}

.select-container select{
  width: 100%;
  margin-top: 9px;
  border-radius: 4px;
  padding: 10px;
  border: 1px solid #ddd;
}

.form-container button {
  background-color: black;
  padding: 10px;
  width: 100%;
  margin-top: 9px;
  border-radius: 4px;
  text-align: center;
  color: white;
  font-weight: bold;
  font-size: 16px;
}
</style>
