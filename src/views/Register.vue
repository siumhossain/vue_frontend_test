<template>
    

    <div class="container">
        <div class="card" style="width: 30rem;">
        <div class="card-header my-3">
            <h2>Register</h2>
        </div>
        <div class="card-body">
            <div v-for="data in errors" :key="data.id">
                <div class="row mb-1">
                    <span v-if="data.username" class="info">
                        <i class="fas fa-info-circle"></i>
                    username = {{data.username}}
                    </span>
                    <span v-if="data.password" class="info">
                    <i class="fas fa-info-circle"></i>
                        password = {{data.password}}
                    </span>
                    <span v-if="data.email" class="info">
                        <i class="fas fa-info-circle"></i>
                    email = {{data.email}}
                    </span>
                </div>
                
                
                
                
                

            </div>
            <form autocomplete="off" @submit.prevent="submit">
                <div class="row">
                    <div class="col">
                        <div class="mb-3">
                            <label for="fname" class="form-label">First Name</label>
                            <input autocomplete="off" type="text" v-model="first_name" class="form-control" id="fname" required>
                    
                        </div>
                    </div>
                    <div class="col">
                        <div class="mb-3">
                            <label for="lname" class="form-label">Last Name</label>
                            <input autocomplete="off" type="text" v-model="last_name" class="form-control" id="lname" required>
                    
                        </div>
                    </div>
                   
                
                </div>
                <div class="mb-3">
                            <label for="username" class="form-label">User Name</label>
                            <input autocomplete="off" type="text" v-model="username" class="form-control" id="username" required>
                    
                        </div>
                <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input autocomplete="off" type="text" v-model="email" class="form-control" id="email" required>
                    
                        </div>

                
                <div class="mb-3">
                    <label for="exampleInputPassword1" class="form-label">Password</label>
                    <input type="password" v-model="password" class="form-control" id="exampleInputPassword1" required>
                </div>
                
                

                <button type="submit" class="btn btn-primary">Submit</button>
            </form>
            
        </div>
    </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data(){
        return{
            first_name:'',
            last_name:'',
            username:'',
            email:'',
            password:'',
            errors:[]
        }

    },
    methods:{
        async submit(){
            let _this = this
            const formdata = {
                first_name:this.first_name,
                last_name:this.last_name,
                username:this.username,
                email:this.email,
                password:this.password
            }
            delete  axios.defaults.headers.common["Authorization"];
            this.errors = [];
            await axios.post('api/auth/users/',formdata)
            .then(res =>{
                console.log(res)
                
                this.$router.push('/login')
            })
            .catch(function (error) {
                if (error.response) {
                // Request made and server responded
                
                //console.log(error.response.data);
                _this.errors = error.response
                console.log(_this.errors)
                
                
                
                } 

            });
        }
    }
}
</script>
<style>
.container{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    
}
.card{
    margin-top: 3rem;
} 
h2{
    font-weight: 900;
}
.info{
  color:crimson
}
</style>