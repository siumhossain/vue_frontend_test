<template>
  <div class="home">
    <div class="container">
      <div class="row">
        <div v-for="i in about" :key="i.id" class="col">
          <h3 class="display-5 mt-5 mb-3 ">About Us</h3>
          <h4 class="my-3">{{i.description}}</h4>
        </div>
      </div>
      
      
    </div>
    <section>
      <div class="container bg-light">
        <div class="row ">
          <div class="col">
          <!-- show only small -->
          

          <!-- show only mid screen -->
          <h3 class="display-5 mt-5 mb-3 ">Justice delayed is justice denied</h3>
          <button class="btn btn-primary my-2">
            <router-link to='/team'>
              meet the team
            </router-link>
            
          </button>
          
        </div>
        
      </div>
      </div>
      
    </section>
    
  </div>
  <router-view></router-view>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src


export default {
  name: 'Home',
  data(){
    return{
      about:[]
    }
  },
  async created(){
    delete  axios.defaults.headers.common["Authorization"];
    axios.get('api/about/')
    .then(res => {
      this.about = res.data
      axios.defaults.headers.common['Authorization'] =  "Token "  +  localStorage.getItem('token')
    })
  }
  
}
</script>
<style>
.display-5{
  font-weight: 800;
  }
.btn a{
  color:white
}
</style>