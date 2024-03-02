<template>
  <div>
  <HeaderPage />
    <h1>hello there, Welcome to Add user page</h1>
    <form class="add">
    <input type="text" name='name' placeholder="Enter name" v-model="users.name"/>
    <input type="text" name='job' placeholder="Enter job"  v-model="users.job"/>
    <input type="text" name='company' placeholder="Enter company"  v-model="users.company"/>
    
    <button type="button" v-on:click="addUsers">Add New user</button>
    </form>
    
  </div>
</template>

<script>
import HeaderPage from "./HeaderPage.vue";  
import axios from "axios"
export default {
  name: "Add",
  components: {
    HeaderPage,
  },
  data(){
    return {
        users:{
            name:"",
            job:"",
            company:""
        }
    }
  },
  methods:{
     async addUsers()
    {
        console.log(this.users);
        const result= await axios.post("http://localhost:3000/users", {
          name:this.users.name,
          job: this.users.job,
          company: this.users.company,
        });
        if(result.status==201){
          this.$router.push({name:'Home'})
        }
        console.log("result",result)
    }
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "LoginPage" });  
    }
  },
};
</script>

<style>
/* Add your component-specific styles here */
</style>
