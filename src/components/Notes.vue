<template>
  <div>
    <table
      id="tableflow"
      class="tableflow table table-bordered table-secondary table-striped"
    >
      <thead class="table-dark">
        <tr>
          <th scope="col">ID</th>
          <th scope="col">User ID</th>
          <th scope="col">User Name</th>
          <th scope="col">Title</th>
          <th scope="col">Status</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="user in list" :key="user.id">
          <!-- <th scope="row">{{ index + 1 }}</th> -->
          <td v-text="user.id"></td>
          <td v-text="user.userId"></td>
          <td v-text="user.name"></td>
          <td v-text="user.title"></td> 
          <td v-text="user.completed"></td>
        </tr>
      </tbody>
    </table>
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
  

  methods:{
    

    async loadData() {
      const result = await axios.get("https://jsonplaceholder.typicode.com/todos");

      console.log(result);
      console.log("Notes", result.data);
      this.list = result.data;
    },
    async loadUsers() {
      const result = await axios.get("https://jsonplaceholder.typicode.com/users");

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

<style>
</style>
