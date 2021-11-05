<template>
    <div class="container center text-center">
        <h2 class="my-3">Our Team</h2>
        <p>
            Our team is made up of dedicated and talented individuals from diverse backgrounds, who combine the ability to deliver local knowledge with an experience of international business.
        </p>
        <h3>Search By</h3>
    <div class="container my-3">
        <div class="row">
            <div class="col">
                <button @click="category" class="btn btn-primary">Category</button>
                <button v-on:click="name" class="btn btn-primary mx-3">Name</button>
            </div>
            
            
        </div>
    </div>

    <!-- for search category-->
    <!-- <div  class="container">
        <div class="row">
            <div class="col">
                <form>
                    <div class="mb-3">
                        
                        <input type="text" class="form-control" placeholder='Search...' required>
                    </div>
                </form>
            </div>
            
            
        </div>
    </div> -->
    <div v-for="i in lawyer" :key="i.id" class="container my-5">
        <div class="card">
            <div class="bg-image hover-overlay ripple" data-mdb-ripple-color="light">
                <img
                src="../assets/avatar.jpg"
                class="img-fluid"
                />
                
            </div>
            
            <div class="card-body">
                <h3 class="card-title">{{i.name}}</h3>
                <h5>Category: {{i.category}}</h5>
                <h5>Position: {{i.position}}</h5>
                <button class="btn btn-primary">Contact</button>
            </div>
            </div>
            
    </div>
    
    </div>
</template>
<script>
import axios from 'axios'

export default {

    

    data(){
        return{
            position_value:'',
            position:{},
            search_value:'',
            lawyer:{},
            category:false,
            name:false,
        }
    },

    watch:{
        search_value: async function(value){
            //console.log(value)
            await axios.get(`api/lawyer/?name=${value}&category=${value}`)
            .then(res => {
                
            })
            
        }
        

    },
    
    async created() {
        delete  axios.defaults.headers.common
        await axios.get('api/position/')
        .then(res => {
            this.position = res.data
            
            console.log('done')
            axios.get('api/all-lawyer/')
            .then(res => {
                
                this.lawyer = res.data
                console.log(this.lawyer)
            })

            
            
        })
        
       
    },
    methods:{
        category: function(){
            console.log('category click')
            
        },
        name: function(){
            console.log('name_click')
        }
    },
    
    
}
</script>
<style>
 .form-col{
     
     margin: 10px 30px;
     width: 300px;
 }   
</style>