<template>
<div>
    <div class="container">
        <h1>2 Api Fetched in single table</h1>

    </div>

    <div class="d-flex align-items-center justify-content-space-between search-box" style="padding:10px 30px; justify-content:space-between">
        <div class="search-box-main text-start">
            <input placeholder="Search Name" type="text" class="search" v-model="search" />
            <i class="icon fa-solid fa-magnifying-glass"></i>
        </div>

        <div class="clearbtn">
            <button @click="cleared()" class="btn btn-danger">Clear</button>
        </div>

    </div>

    <table class="table table-dark">
        <thead>
            <tr>
            </tr>
        </thead>
        <tbody>
            <div class="d-flex justify-content-center">
                <div class="box">
                    <h4>ID</h4>
                    <ul v-for="(user, index) in searchBox" :key="index">
                        <li>{{ user.id }}</li>
                    </ul>
                </div>
                <div class="box">
                    <h4>UserID</h4>
                    <ul v-for="(user, index) in searchBox" :key="index">
                        <li>{{ user.userId }}</li>
                    </ul>
                </div>
                <div class="box">
                    <h4>Name</h4>
                    <ul v-for="(user, index) in lists" :key="index">
                        <li>{{ user.name }}</li>
                    </ul>
                </div>
                <div class="box">
                    <h4>Title</h4>
                    <ul v-for="(user, index) in searchBox" :key="index">
                        <li>{{ user.title }}</li>
                    </ul>
                </div>
                <div class="box pe-5">
                    <h4>Status</h4>
                    <ul v-for="(user, index) in searchBox" :key="index">
                        <li>{{ user.completed }}</li>
                    </ul>
                </div>
            </div>
        </tbody>
    </table>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: "Notes",
    data() {
        return {
            list: [],
            lists: [],
            search:'',
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
        cleared() {
            console.log('clicked');
            console.log(this.search);
            this.search = ""
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
                            (data) => item.title.toLowerCase().includes(data) 
                            // item.title.toLowerCase().includes(data) ||
                        );
                });
            } else {
                return this.list;
            }
        },
    },
    async mounted() {
        this.loadData();
        this.loadUsers();
    },
}
</script>

<style>
ul {
    list-style-type: none;
}
</style>
