<script>
import axios from "axios";

export default {
  name:"UserView",
  data(){

    return{

      users:[],
      show: null
    }
  },
  methods:{
    getUsers(){
      axios.get('http://localhost:8081/v1/users?detailed=1').then(res=> {
        this.users = res.data;
      })
    },

    deleteUserById(userId){
      if(confirm("Are you sure, you want to delete this data?")){
        axios.delete(`http://localhost:8081/v1/users/${userId}`).then(res=> {
          this.getUsers();
        }).catch(function (error){
          //erro
        })
      }
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      const day = date.getDate().toString().padStart(2, '0');
      const month = (date.getMonth() + 1).toString().padStart(2, '0');
      const year = date.getFullYear();

      return `${day}/${month}/${year}`;
    },
    toggleDetail(userId) {
      this.show = this.show === userId ? null : userId;

    }
  },
  mounted() {
    this.getUsers();
  }
}
</script>

<template>
  <div class="users col-9 mx-auto" >
    <div class="">
      <div class="text-center">
        <RouterLink to="/users/create" tag="v-btn">
            <div class="d-grid mt-5 gap-2 col-9 mx-auto">
              <button class="btn btn-primary" type="button"> Agregate new user </button>
           </div>
        </RouterLink>
      </div>


  <div class="table-responsive  mt-5">
    <table class="table table-hover table-bordered"  >
      <thead >
      <tr>
        <th>User</th>
        <th>Options</th>
      </tr>
      </thead>

        <tbody v-if="users.length > 0">
        <tr v-for="(user, index) in users" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ user.username }}</td>
          <td>
            <button class="btn btn-info" type="button" @click="toggleDetail(user.id)">
              Detail
            </button>

          </td>
          <td>
            <RouterLink :to="{ path: '/users/' + user.id + '/edit' }" tag="button" class="text-uppercase">
              <button class="btn btn-warning" type="button"> Edit </button>
            </RouterLink>
          </td>
          <td>
            <button class="btn btn-danger" type="button" @click="deleteUserById(user.id)" >
              Delete
            </button>
          </td>

          <div v-show="show === user.id">
              <v-card width="500">
                <v-card-title> Detail </v-card-title>
                <v-card-text>
                  First Name: {{ user.first_name }}
                  <v-divider></v-divider>
                  Last Name: {{ user.last_name }}
                  <v-divider></v-divider>
                  Password: {{ user.password }}
                  <v-divider></v-divider>
                  Age: {{ user.age }}
                  <v-divider></v-divider>
                  Birthday: {{ formatDate(user.birth_day) }}
                  <v-divider></v-divider>
                </v-card-text>
              </v-card>
          </div>

        </tr>



        </tbody>

      </table>

     </div>

    </div>
  </div>

</template>

<style scoped>

</style>