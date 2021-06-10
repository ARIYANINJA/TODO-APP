<template>
  <div class="container">
    <h1 class = "text-center mt-5 "> TODO APP VUE JS </h1>
    <div class = "d-flex mt-5" >
    <input  v-model = "task" type = "text" class = "form-control" placeholder="type a  list item ">
    <button @click="submitTask" class="btn - btn-warning rounded-0">CLICK HERE </button>
  </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
      <th scope="col">CHECK</th>
      <th scope="col">ITEMS</th>
      <th  scope="col">DELETE ITEM</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
            <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': task.status === 'unchecked',
                'text-success': task.status === 'checked',
              }"
            >
            <span class="fas fa-check"></span>
            </span>
          </td>
          <td>
            <span :class="{ 'line-through': task.status === 'checked' }">
              {{ task.name }}
            </span>
          </td>
        
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["unchecked","checked"],

      tasks: [
        {
          name: " hello world",
          status: "unchecked",
        },
      ],
    };
  },

  methods: {
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 1) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    submitTask() {
      if (this.task.length === 0) return;
        this.tasks.push({
          name: this.task,
          status: "unchecked",
        });
      }
    },
}
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
.line-through {
  text-decoration: line-through;
}
</style>