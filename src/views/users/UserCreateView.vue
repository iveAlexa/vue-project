
<script>
import axios from "axios";

export default{
  name:"UserCreateView",
  data() {
    return{
      usernameRules: [
        (v) => !!v || 'Username is required',
        (v) =>
            (v && v.length >= 4 && v.length <= 10) ||
            'Username must be between 4 and 10 characters',
      ],
      passwordRules: [
        (v) => !!v || 'Password is required',
        (v) =>
            (v && v.length >= 6) ||
            'Password must be at least 6 characters',
      ],emailRules: [
        (v) => !!v || 'Email is required',
        (v) =>
            /.+@.+\..+/.test(v) || 'Email must be valid',
      ],
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
    saveUser(){
      axios.post('http://localhost:8081/v1/users',this.model.user)
          .then(res=>{
            alert('User was saved successful');
            this.model.user ={
              username: '',
              password: '',
              email:'',
              first_name:'',
              last_name:'',
              age:'',
              birth_day:''
            }
          }).catch(function (error){
        // hangle error on UI site
      })
    }
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
      <v-card-item class="d-flex justify-center mb-6"><h4>New User</h4></v-card-item>
      <v-text-field
          density="compact"
          placeholder="Insert an username"
          variant="outlined"
          v-model="model.user.username"
          label="Username"
          :rules="usernameRules"
      ></v-text-field>
      <v-text-field

          density="compact"
          placeholder="Insert a password"
          label="Password"
          variant="outlined"
          v-model="model.user.password"
          :rules="passwordRules"

      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert an email"
          variant="outlined"
          v-model="model.user.email"
          label="Email"
          :rules="emailRules"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert a first name"
          variant="outlined"
          v-model="model.user.first_name"
          label="First Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert a last name"
          variant="outlined"
          v-model="model.user.last_name"
          label="Last Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Insert an age"
          variant="outlined"
          v-model="model.user.age"
          label="Age"
      ></v-text-field>

      <v-text-field
          density="compact"
          placeholder="Insert a birthday (YYYY-MM-DD)"
          variant="outlined"
          v-model="model.user.birth_day"
          type="date"
          label="Birthday"
          class="mt-4"
      ></v-text-field>

      <div  class="d-flex flex-wrap ga-3">
      <v-btn

          class="mb-1"
          color="blue-darken-3"
          size="small"
          @click="saveUser"
      >
        save a new user
      </v-btn>
      </div>
    </v-card>
  </div>

</template>

<style scoped>

</style>