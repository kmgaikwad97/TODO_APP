<template>
  <div>
  
    <div class="main-div d-flex justify-content-center">
      <div class="another-div">
        <div class="box heading text-center">
          <h4 class="heading">ID</h4>
        </div>
        <ul class="main-list" v-for="user in list" :key="user.id">
          <li class="list-data">{{ user.id }}</li>
        </ul>
      </div>

      <div class="box">
        <h4>UserID</h4>

        <ul v-for="user in list" :key="user.id">
          <li>{{ user.title }}</li>
        </ul>
      </div>

      <div class="box">
        <h4>Name</h4>
        <ul v-for="user in lists" :key="user.id">
          <li>{{ user.name }}</li>
        </ul>
      </div>

      <div class="box">
        <h4>Status</h4>
        <ul v-for="user in list" :key="user.id">
          <li>{{ user.completed }}</li>
        </ul>
      </div>
    </div>

    
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Notes",
  data() {
    return {
      list: [],
      lists: [],
    };
  },

  methods: {
    async loadData() {
      const result = await axios.get(
        "https://jsonplaceholder.typicode.com/todos"
      );

      console.log(result);
      console.log("Notes", result.data);
      this.list = result.data;
    },
    async loadUsers() {
      const result = await axios.get(
        "https://jsonplaceholder.typicode.com/users"
      );

      console.log(result);
      console.log("Users", result.data);
      this.lists = result.data;
    },
  },

  async mounted() {
    this.loadData();
    this.loadUsers();
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
}
h4 {
  border: 1px solid black;
}
ul {
  border: 1px solid black;
}
li {
  border: 1px solid black;
}
</style>
