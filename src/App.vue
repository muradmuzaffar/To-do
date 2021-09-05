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

    <!--todos
    <ul v-for="(todo, index) in todos" class="list-group list-group-flush">
      <li class="list-group-item bg-primary">
        {{ todo
        }}<button @click="rv(index)" class="btn btn-danger btn-sm">
          Delete
        </button>
      </li>
    </ul>-->

    <!--todos-->
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Index</th>
          <th scope="col">Todo</th>
          <th scope="col">Status</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody v-for="(todo, index) in myTodo.todos">
        <tr>
          <th scope="row">{{ index }}</th>
          <td>{{ todo }}</td>
          <td @click="changeStatus(index)">{{ myTodo.status }}</td>
          <td>
            <button @click="rv(index)" class="btn btn-danger btn-sm">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myTodo: {
        todo: "",
        todos: [],
        status: "to-do",
        index: -1
      }
    };
  },

  methods: {
    addTodo: function() {
      if (this.myTodo.todo != "") {
        this.myTodo.todos.push(this.myTodo.todo);
        this.myTodo.todo = "";
        this.myTodo.index += 1;
      }
    },
    rv: function(index) {
      this.myTodo.todos.splice(index, 1);
    },
    changeStatus: function(index) {
      if (index === this.myTodo.index) {
        this.myTodo.status = "finished";
      }
      console.log(index);
      console.log(this.myTodo.index);
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
</style>
