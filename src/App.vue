<script setup>
  import { ref } from 'vue';
  
  const taskArr = ref([]);
  const newTask = ref("");

  let indexCounter = 0;
  let noOfCompleted = 0;
  let noOfUncompleted = 0;
  

  const addTask = () => {
    taskArr.value.push({
      id: indexCounter,
      task: newTask.value,
      isDone: false,
      show: false,
    });
    newTask.value = "";
    indexCounter++;
    noOfUncompleted++;
  }

  const toggleTaskStatus = (x) => {
    if (taskArr.value.at(x).isDone){
      taskArr.value.at(x).isDone = false
      noOfUncompleted++;
      noOfCompleted--;
    }else{
      taskArr.value.at(x).isDone = true
      noOfUncompleted--;
      noOfCompleted++;
    }
    
  }

  const toggleShow = (x) => {
    if (taskArr.value.at(x).show){
      taskArr.value.at(x).show = false

    }else{
      taskArr.value.at(x).show = true
    }
    
  }

  
  

</script>

<template>
  <main class="main">
    <div class="container">
      <h1>To Do List</h1>
      <header class="header">
        <textarea name="text" id="text" placeholder="Add Task here" v-model.trim="newTask"></textarea>
        <button @click="addTask" class="add-button">Add</button>
      </header>
      <div class="task-heading">
        <h1>Task List</h1>
      </div>
      <div class="task-container">
        <div v-for="task in taskArr" class="task-card" >
          <div class="task">
            <input type="checkbox" name="check-button" id="check-button" @click="toggleTaskStatus(task.id)">
            <textarea class="task.task" v-model="task.task" v-show="task.show"></textarea>
            <s v-if="task.isDone" >{{ task.task }}</s>             
            <p v-if="!task.isDone && !task.show"> {{ task.task }}</p>
          </div>
          <div class="task-buttons">
            <button class="delete-button" @click="taskArr.splice(x);">Delete</button>
            <button class="edit-button" @click="toggleShow(task.id)">Edit</button>
          </div>
        </div>
        
        
      </div>
      <div class="footer">
          <hr>
          <footer>Compeleted: {{ noOfCompleted }} | Uncompleted: {{ noOfUncompleted }}</footer>
        </div>
    </div>
    
  </main>
  
</template>

<style scoped>
  .task {
    display: flex;
    align-items: center;
    width: 300px; /* Set a width for the container */
    padding: 10px;
  }

  .task p s {
    word-wrap:break-word;
    overflow-wrap: break-word;
    white-space: normal;
  }

  .task-card {
    display: flex;
    align-items:center;
    justify-content: space-between;
    border: 2px solid black;
    margin-bottom: 10px;
    border-radius: 10px;
    gap: 300px;
    
  }

  .task-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
  }

  .main {
     width: 100vw;
     height: 100vh;
  }

  .delete-button {
    float: right;
    color:crimson;
    cursor: pointer;
    margin: 3px 5px;
    border: 2px solid black;
    border-radius: 5px;
    padding: 3px 5px;
    background: none;
  }

  textarea {
  min-height: 50px;      /* Minimum height */
  max-height: 300px;     /* Optional: Limit maximum height */
  overflow-y: auto;      /* Enable scrolling if needed */
  resize: none;          /* Disable manual resizing */
  width: 50%;           /* Full width for the container */
}

  .edit-button {
    float: right;
    color: blue;
    cursor: pointer;
    margin: 3px 5px;
    border: none;
    padding: 3px 5px;
    background: transparent;
    border-radius: 5px;
    border: 2px solid black;
  }

  .add-button {
    float: right;
    color: black;
    cursor: pointer;
    margin: 3px 5px;
    border: none;
    padding: 3px 5px;
    background: rgb(109, 159, 216);
    border-radius: 5px;
    border: 2px solid black;
  }

  .header {
    display: flex;
    gap: 10px;
    justify-content: center;
  }

  h1 {
    text-align: center;
  }

  .footer {
    text-align: center;
  }
</style>