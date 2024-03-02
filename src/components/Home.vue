<template>
  <div>
  <HeaderPage />
    <h1>hello {{name}}, Welcome to home page</h1>
    <table border=1>

    <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Job</th>
          <th>Company</th>
          <th>Actions</th>
        </tr>
    
    <tr v-for="user in users" :key="user.id">
    <td>{{user.id}}</td>
     <td>{{user.name}}</td>
      <td>{{user.job}}</td>
       <td>{{user.company}}</td>
        <td>
        <router-link :to="'/update/'+user.id">Update</router-link>
        <button v-on:click="deleteUsers(user.id)">Delete</button>
        </td>
    </tr>
    
    </table>
    
  </div>
</template>

<script>
import HeaderPage from "./HeaderPage.vue";  
import axios from "axios"
export default {
  name: "Home",
  data(){
    return {
        name:"",
        users:[],
        
    }
  },
  components: {
    HeaderPage,
  },

  methods:{
  async  deleteUsers(id){
  //  console.log(id)
   let result= await axios.delete("http://localhost:3000/users/"+id);
   console.log(result);
   if(result.status==200){
      this.loadData()
   }
    },
     async loadData()
    {
      let user = localStorage.getItem("user-info");
    this.name=JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: "LoginPage" });  
    }
    let result= await axios.get("http://localhost:3000/users");
    console.log(result);
    this.users=result.data;
    }
  },




 async mounted() {
    this.loadData();
  },
};
</script>

<style>
/* Add your component-specific styles here */
th{
    width:160px;
    height:40px;
    margin-left:20px;
    color:black;
}

tr{
    width:160px;
    height:40px;
    margin-left:20px;
    color:black;
}
</style>
