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
          <td>
            <input class="check" type="checkbox" />
          </td>
          <td>
            <button @click="rv(index)" class="btn btn-danger btn-sm">
              Delete
            </button>
          </td>

          <td v-if="updated == 0">
            <button @click="up(index)" class="btn btn-success btn-sm">
              Update
            </button>
          </td>
          <td v-else="updated == 1">
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
                  update
                </button>
              </div>
            </div>
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
        todos: []
      },
      updated: 0
    };
  },

  methods: {
    addTodo: function() {
      if (this.myTodo.todo.length != 0) {
        this.myTodo.todos.push(this.myTodo.todo);
        this.myTodo.todo = "";
      }
    },
    rv: function(index) {
      this.myTodo.todos.splice(index, 1);
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

.check {
  text-align: center;
  width: 20px;
  height: 20px;
}
</style>
