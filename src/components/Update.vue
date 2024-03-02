<template>
  <div>
  <HeaderPage />
    <h1>hello there, Welcome to update page</h1>
      <form class="add">
    <input type="text" name='name' placeholder="Enter name" v-model="users.name"/>
    <input type="text" name='job' placeholder="Enter job"  v-model="users.job"/>
    <input type="text" name='company' placeholder="Enter company"  v-model="users.company"/>
    
    <button type="button" v-on:click="updateUsers">Update user</button>
    </form>
    
  </div>
</template>

<script>
import HeaderPage from "./HeaderPage.vue"; 
import axios from "axios";

export default {
  name: "Update",
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
     async updateUsers()
    {
        console.log(this.users);
        const result= await axios.put("http://localhost:3000/users/"+this.$route.params.id ,{
          name:this.users.name,
          job: this.users.job,
          company: this.users.company,
        });
        if(result.status==200){
          this.$router.push({name:'Home'})
        }
        console.log("result",result)
    }
  },


async  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "LoginPage" });  
    }
      const result =await axios.get("http://localhost:3000/users/"+this.$route.params.id)
    //  console.log(this.$route.params.id)
    console.log(result.data)
    this.users=result.data;

  },
};
</script>

<style>
/* Add your component-specific styles here */
</style>
