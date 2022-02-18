<template>
  <div class="conteiner">
      <h2 class="text-center mt-5 mx-5">To Do List</h2>
      
      <div class="d-flex">
          <input v-model="task" type="text" placeholder="Enter task" class="form-control ">
          <button @click="submitTask" style="background-color:brown" class="btn btn-waring my-3 mx-4">Create</button>
  </div>
    <table class="table table-bordered table-dark mt-4 ">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Completed</th>
      <th scope="col" class="text-center">Edit</th>
      <th scope="col" class="text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <th>
        <td>
          <span :class="{'Yes' : task.completed === 'Yes'}">{{task.title}}</span>
          </td>

          </th>
      <td style="width:120px">
      <span @click="changeCompleted(index)" class="pointer"
        :class="{'text-danger': task.completed === 'No',
        'text-success':task.completed === 'Yes'
        }"
      
      >
          {{ firstCharUpper(task.completed) }}
          </span>
        </td>
      <td>
          <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
          </div>
      </td>
      <td>
          <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>
          </div>
      </td>
    </tr>
   
  </tbody>
</table>
  </div>
</template>
<script>
export default{
    title: "Hello",
    props:{
        msg:String,
    },

    data(){
        return{
            task:'',
            editedTask: null,
            availableCompleteds:['No','Yes'],
            tasks:[]
        }

    },

    methods:{
      submitTask(){
            if(this.task.length === 0)return;

            if(this.editedTask === null){
              this.tasks.push({
                title: this.task,
                completed: 'No'
              });
            }else{
              this.tasks[this.editedTask].title = this.task;
              this.editedTask = null;
            }
            this.task = '';
      },

      deleteTask(index){
        this.tasks.splice(index,1);
      },
      editTask(index){
        this.task = this.tasks[index].title;
        this.editedTask =index;
      },
      changeCompleted(index){
        let newIndex = this.availableCompleteds.indexOf(this.tasks[index].completed);
        if(++newIndex > 1) newIndex=0;
        this.tasks[index].completed = this.availableCompleteds[newIndex];
      },
      firstCharUpper(str){
        return str.charAt(0).toUpperCase() + str.slice(1);
      }
    }
};
</script>
<style scoped>
.pointer {
    cursor: pointer;
}
.Yes{
    text-decoration: line-through;
}
</style>

