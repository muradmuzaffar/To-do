<template>
  <div id="app">
    <h1 style="text-align:center;">To do List</h1>
    <hr />

    <!--to do input-->
    <div class="input-group mb-3">
      <input
        v-model="myTodo.todo"
        type="text"
        class="form-control"
        placeholder="Add to do"
        aria-label="Recipient's username"
        aria-describedby="basic-addon2"
      />
      <div class="input-group-append">
        <button
          @click="addTodo"
          class="btn btn-outline-secondary"
          type="button"
        >
          +
        </button>
      </div>
    </div>

    <!--todos-->
    <table class="table" v-if="myTodo.todos.length != 0">
      <thead>
        <tr>
          <th scope="col">Index</th>
          <th scope="col">Todo</th>
          <th scope="col">Status</th>
          <th scope="col">Delete</th>
          <th scope="col">Update</th>
        </tr>
      </thead>
      <tbody v-for="(todo, index) in myTodo.todos">
        <tr>
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ todo }}</td>
          <td class="status" @click="changeStatus(index)">
            {{ myTodo.statuses[1] }}
          </td>
          <td>
            <button @click="rv(index)" class="btn btn-danger btn-sm">
              Delete
            </button>
          </td>
          <td v-show="(updated = 1)">
            <button @click="up" class="btn btn-success btn-sm">
              Update
            </button>
          </td>
          <td v-show="(updated = 0)">
            <h1>aa</h1>
          </td>
        </tr>
      </tbody>
    </table>

    <!--alert-->
    <div class="alert alert-danger" role="alert" v-else>
      Please add a new task!
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myTodo: {
        todo: "",
        todos: [],
        statuses: ["to-do", "in-progress", "finished"]
      },
      updated: 0
    };
  },

  methods: {
    addTodo: function() {
      if (this.myTodo.todo != "") {
        this.myTodo.todos.push(this.myTodo.todo);
        this.myTodo.todo = "";
        this.myTodo.i += 1;
      }
    },
    rv: function(index) {
      this.myTodo.todos.splice(index, 1);
    },

    up: function() {
      if (this.updated === 0) {
        this.updated = 1;
        console.log(this.updated);
      } else {
        this.updated = 0;
        console.log(this.updated);
      }
    },
    changeStatus: function(index) {
      console.log(this.myTodo.statuses.indexOf("finished"));
    }
  }
};
</script>

<style>
body {
  display: flex;
  justify-content: center;
  align-items: center;
}

#app {
  width: 50%;
}

.status {
  cursor: pointer;
}
</style>
