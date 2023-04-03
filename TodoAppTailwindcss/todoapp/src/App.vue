<script setup>
import "bootstrap/dist/css/bootstrap.min.css"
import "bootstrap"

</script>

<template>
<div class="new w-screen h-screen bg-black justify-center flex items-center">
<div class="box w-2/4 bg-slate-800 h-5/6 rounded">
  <h3 class="text-white text-center mt-10 mb-3">TO DO APP</h3>
  <div class="flex justify-center items-center"><input v-model="task" type="text" placeholder="Type in your task Here... " class=" left-10 w-2/4 h-10 px-5 outline-none">
    <button @click ="submitTask" class=" btn btn-warning rounded-0 h-10 ">submit </button>
  
  </div>
  <!-- <div class="flex justify-center items-center text-3xl text-center"> -->
  <!-- </div> -->
   <div><table class="table text-sm text-white text-center rounded relative -top-0 mt-2">
  <thead>
    <tr>
      <th scope="col">Tasks</th>
      <th scope="col">Status</th>
      <th scope="col">Edit</th>
      <th scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <th scope="row">{{ task.name }}</th>
      <td ><span @click="changeStatus(index)" class="cursor-auto hover:cursor-auto">{{ task.status }}</span></td>
      <td> <div @click = "editTask(index)"><i class="bi bi-pencil-square"></i></div></td>
      <td><div @click = "deleteTask(index)"><i class="bi bi-trash3"></i></div></td>
    </tr>

  </tbody>
</table>
</div>
</div>
</div>
</template>

<style scoped>

</style>
<script>
  export default{
    data(){
      return{
        task: '',
        editedTask: null,
        avalaibleStatus: ['Todo', 'In-Progress', 'Finished'],
        tasks: [
        {
          name: 'Learn Programming.',
          status: 'Todo',
        },
        {
          name: 'Research International Studies',
          status: 'In-Progress'
        }
        ]
      }
    },
    methods: {
      submitTask(){
        if(this.task.length === 0) return alert("Your Task is empty!");

        if(this.editedTask === null){
          this.tasks.push({
            name: this.task,
            status: 'todo'
          });
        }else{ 
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
        }
        
        this.task = "";
      },
      deleteTask(index){
        this.tasks.splice(index, 1);
      },
      editTask(index){
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },
      changeStatus(index){
          let newIndex = this.avalaibleStatus.indexOf(this.tasks[index].status);
          if (++newIndex > 2) newIndex = 0;
          this.tasks[index].status = this.avalaibleStatus[newIndex];
      },
    }
  }
</script>