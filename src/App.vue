<template>
  
  <UserAdd :users="users" @addUser="addUser($event)" class="text-center" />
  <v-simple-table>
    <div class="tableData">
      <table class="table table-hover">
        <thead>
          <tr>
            <th class="text-center">Name</th>
            <th class="text-center">Username</th>
            <th class="text-center">E-mail</th>
            <th class="text-center">Phone</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td class="text-center">{{ user.name }}</td>
            <td class="text-center">{{ user.username }}</td>
            <td class="text-center">{{ user.email }}</td>
            <td class="text-center">{{ user.phone }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </v-simple-table>
</template>

<script>
import UserAdd from "./components/UserAdd.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    UserAdd,
  },
  data() {
    return {
      users: null,
    };
  },
  //methods directive içerisinde kullanıcı ekleme ve get post işlemi yapıldı.
  methods: {
    addUser: function (item) {
      console.log(item);
      axios
        .post("https://jsonplaceholder.typicode.com/users", item)
        .then((response) => {
          this.users.unshift(response.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created: function () {
    axios.get("https://jsonplaceholder.typicode.com/users").then((res) => {
      this.users = res.data;
      console.log(this.users);
    });
  },

}
</script>

<style>

.tableData {
  margin-top: 30px;
  background-color: antiquewhite;
  border-radius: 20px;
  width: 50%;
  margin-left: auto;
  margin-right: auto;
}

</style>
