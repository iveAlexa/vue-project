
<script>
import axios from "axios";

export default {
  name:"UserEditView",
  data() {
    return{
      userId:'',
      visible: false,
      model: {
        user:{
          username: '',
          password: '',
          email:'',
          first_name:'',
          last_name:'',
          age:'',
          birth_day:''
        }
      }
    }
  },
  methods:{
    getUserById(userId){
      axios.get(`http://localhost:8081/v1/users/${userId}`).then(res=> {
        this.model.user = res.data;
      }).catch(function (error){
        //handle error on UI Site
      })
    },
    editUser(){
      axios.put(`http://localhost:8081/v1/users/${this.userId} `,this.model.user)
          .then(res=>{
            alert('User was edited successful');

          }).catch(function (error){
        // hangle error on UI site
      })
    }
  },

  mounted() {
    this.userId=this.$route.params.id;
    this.getUserById(this.userId);
  }
}
</script>
<template>

  <!-- Acciones de la tarjeta, como botones, detallas, etc. -->
  <div>

    <v-card
        class="mx-auto pa-12 pb-8"
        elevation="8"
        max-width="800"
        rounded="lg"
    >
      <v-card-item class="d-flex justify-center mb-6"><h4>EDIT A USER</h4></v-card-item>
      <v-text-field
          density="compact"
          placeholder="Insert username"
          variant="outlined"
          v-model="model.user.username"
          label="Username"
      ></v-text-field>
      <v-text-field

          density="compact"
          placeholder="Insert password"
          label="Password"
          variant="outlined"
          v-model="model.user.password"

      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert email"
          variant="outlined"
          v-model="model.user.email"
          label="Email"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert first name"
          variant="outlined"
          v-model="model.user.first_name"
          label="First Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert last name"
          variant="outlined"
          v-model="model.user.last_name"
          label="Last Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert Age"
          variant="outlined"
          v-model="model.user.age"
          label="Age"
      ></v-text-field>

      <v-text-field
          density="compact"
          placeholder="Insert birthday"
          variant="outlined"
          v-model="model.user.birth_day"
          type="date"
          label="Birthday"
          class="mt-3"
      ></v-text-field>

      <v-btn

          class="mb-1"
          color="green-accent-4"
          size="large"
          @click="editUser"
      >
        save a changes
      </v-btn>

    </v-card>
  </div>
</template>

<style scoped>

</style>