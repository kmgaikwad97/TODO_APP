<template>
  <div>

    <div class="d-flex align-items-center justify-content-space-between search-box" style="padding:10px 30px; justify-content:space-between">
      <div class="search-box-main text-start">
        <input
          placeholder="Search Name"
          type="text"
          class="search"
          v-model="search"
        />
        <i class="icon fa-solid fa-magnifying-glass"></i>
      </div>


        <div class="clearbtn">
            <button @click="cleared()" class="btn btn-danger">Clear</button>
        </div>

    </div>


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
        </tr>
      </thead>

      <tbody>
        <tr v-for="(user, index) in searchBox" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td v-text="user.id"></td>
          <td v-text="user.name"></td>
          <!-- <td v-text="user.userId"></td> -->
          <td v-text="user.title"></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Filters",
  data() {
    return {
      list: "",
      search: "",
    };
  },
  async mounted() {
    const result = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );
    console.log(result.data);
    this.list = result.data;
    if (this.list.completed === "false") {
    }
  },
  computed: {
    searchBox() {
      if (this.search) {
        return this.list.filter((item) => {
          console.log("items", item);
          return this.search
            .toLowerCase()
            .split("")
            .every(
              (data) => item.name.toLowerCase().includes(data)
              // || item.lastname.toLowerCase().includes(data) ||
              // item.age.toLowerCase().includes(data) ||
              // item.email.toLowerCase().includes(data)
            );
        });
      } else {
        return this.list;
      }
    },
  },
  methods:{
     cleared(){
      console.log('clicked');
      console.log(this.search);
      this.search = ""
    }
  }
};
</script>

<style>
</style>
