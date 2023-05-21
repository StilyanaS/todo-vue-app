<template>
  <div class="hello">
    <h1>Add your tasks</h1>
    <div class="container-sm">
    <a href="#" v-if="tasks.length > 0" @click="emptyList" class="empty btn btns">Delete list</a>
      <div class="card">
        <h2 class="card-header">To Do</h2>
        <div class="card-body" v-for="(task,index) in tasks" :key="index">
          <h5 class="card-title">{{task.name}}</h5>
          <div class="buttons">
            <a href="#" @click="toEdit(index)" class="btn btns ">Edit</a>
            <a href="#" @click="toDelete(index)" class="btn btns ">Delete</a>
          </div>
        </div>
      </div>
    </div>
      <div class="mb-3 form-check d-flex mt-2 task">
        <input v-model="task" type="text" class="form-control task">
        <button @click="submitTask" type="submit" class="new-task btn btns ">Create</button>
      </div>

  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },
  data() {
    return {
      task: "",
      editTask: null,
      tasks : []
    }
  },
  methods: {
    submitTask() {
      if (this.editTask == null){
        if (this.task.length === 0 || this.task == " ") return;
        this.tasks.push({
          name:this.task,
        })
      } else {
        this.tasks[this.editTask].name = this.task
        document.querySelector(".new-task").innerHTML = "Create"
        this.editTask = null
        
      }
      this.task = ""
    },
    toDelete(index){
      this.tasks.splice(index,1)
    },
    toEdit(index){
      this.task = this.tasks[index].name
      this.editTask = index
      document.querySelector(".new-task").innerHTML = "Update"
    },
    emptyList(){
      this.tasks = []
      document.querySelector(".new-task").innerHTML = "Create"
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btns {
  bakground-color: transparent !important;
  border:1px solid salmon;
  color:salmon;
}
h1 {
  margin:1rem;
}
.empty {
  margin-bottom:2rem;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.buttons {
  display:flex;
  gap:1rem;
}
.card-body {
  display:flex;
  justify-content: space-between;
}
.container-sm {
  margin-bottom:2rem;
  max-width: 800px;
}
.task {
  max-width:40vw;
  margin: 0 auto;
  gap: 1rem;
}

</style>
