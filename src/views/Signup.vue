<template>
    <div id="main-container">
        <div id="container">
            <img class="mr-6" :src="require('@/assets/logo1.png')" />
            <h1 id="title">Create your account
                </h1>
            <form action="">
                <div class="input-group">
                    <input type="email" class="input" name="email" 
                    placeholder="Email" v-model="user.email">
                </div>
                <div class="input-group">
                    <input type="text" class="input" name="name" 
                    placeholder="Name" v-model="user.name">
                </div>
                <div class="input-group">
                    <input type="text" class="input" name="number" 
                    placeholder="Phone Number" v-model="user.number">
                </div>
                <div class="input-group">
                    <input type="password" class="input pass" name="password" 
                    placeholder="Password" v-model="user.password">
                </div>
                <div class="input-group">
                    <input type="password" class="input pass" name="confirm-password" 
                    placeholder="Confirm Password">
                </div>
                <v-alert v-if="show" dismissible dense outlined>
                    {{error}}
                </v-alert>
                <v-btn @click="Signup" id="submit">SIGN UP</v-btn>
                <v-col ><v-btn @click="back" icon> Back to Login </v-btn></v-col>
            </form>
        </div>
    </div>
</template>
<script>
  import axios from "axios";
  export default {
      name: "Signup",
      data () {
        return {
            user: {
                email:"",
                name: "",
                number: "",
                password:"",
                role: "owner"
            },
            show: false,
            error: "" 
        }
      },
      methods: {
        Signup() {
            this.show = false
            axios({
                    method: "post",
                    url: "http://164.92.174.146/sign_up",
                    data: JSON.stringify(this.user),
                    headers:{ 'content-type':'application/json'}
                }).then((response) => {
                    if (response.data.value != "sign up successful") {
                        this.error = response.data.value
                        this.show = true;
                    }
                    else {
                        this.$router.push({ name: "Login" });
                    }
                    
                })
                .catch((err) => {
                    this.error = "Error with user fields"
                    this.show = true;
                });
        },
        back() {
            this.$router.push({ name: "Login" });
        }  
    }
  } 
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped src="../style/signup.css" lang="css">
</style>